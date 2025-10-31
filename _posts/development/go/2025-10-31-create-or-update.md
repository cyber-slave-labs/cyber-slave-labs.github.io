---
title: "CreateOrUpdate in controllerutil and Reflect"
toc: true
toc_sticky: true
categories: ["Go"]
excerpt: CreateOrUpdate 동작 기전
---

## What is controllerutil.CreateOrUpdate?
- `controllerutil.CreateOrUpdate`는 Kubernetes 컨트롤러 개발에서 자주 사용되는 유틸리티 함수로, 리소스가 존재하지 않으면 생성하고, 존재하면 업데이트하는 작업을 수행합니다.
- `CreateOrUpdate` 함수는 다음과 같은 시그니처를 가집니다:
```go
func CreateOrUpdate(ctx context.Context, c client.Client, obj client.Object, mutate MutateFn) (OperationResult, error)
```
- 여기서 `ctx`는 컨텍스트, `c`는 Kubernetes 클라이언트, `obj`는 조작할 리소스 객체, `mutate`는 리소스의 상태를 변경하는 함수입니다.
- [git link](https://github.com/kubernetes-sigs/controller-runtime/blob/v0.22.3/pkg/controller/controllerutil/controllerutil.go#L320)

## How does CreateOrUpdate work?
- `CreateOrUpdate` 함수는 내부적으로 다음과 같은 단계를 거쳐 동작합니다:
  1. **Get**: 먼저, 지정된 리소스 객체가 Kubernetes 클러스터에 존재하는지 확인하기 위해 `Get` 메서드를 호출합니다.
  2. **NotFound 처리**: 리소스가 존재하지 않는 경우(`NotFound` 오류 발생), `mutate` 함수를 호출하여 리소스의 초기 상태를 설정한 후, `Create` 메서드를 사용하여 리소스를 생성합니다.
  3. **존재하는 경우 처리**: 리소스가 이미 존재하는 경우, `mutate` 함수를 호출하여 현재 상태를 원하는 상태로 변경합니다. 그런 다음, 변경된 상태를 비교하여 실제로 업데이트가 필요한지 확인합니다.
  4. **Update**: 만약 리소스의 상태가 변경되었다면, `Update` 메서드를 호출하여 리소스를 업데이트합니다.

## What is Reflect?
- `reflect` 패키지는 Go 언어에서 런타임에 타입과 값을 조작할 수 있는 기능을 제공합니다.

  ```go
  import "reflect"
  
  type Person struct {
      Name string
      age  int // private field
  }
  
  p := Person{Name: "Alice", age: 30}
  
  v := reflect.ValueOf(p)
  t := reflect.TypeOf(p)
  
  fmt.Println(t.Name())            // "Person"
  fmt.Println(t.NumField())        // 2
  fmt.Println(t.Field(0).Name)     // "Name"
  fmt.Println(t.Field(1).Name)     // "age"
  fmt.Println(v.Field(0).String()) // "Alice"
  ```

- 리플렉션 덕분에 프로그램은 타입을 미리 몰라도 구조체의 필드에 접근할 수 있습니다. 그래서 라이브러리들이 “generic(제네릭처럼)” 작동할 수 있습니다.

## Using Reflect in CreateOrUpdate
- `CreateOrUpdate` 함수는 리플렉션을 사용하여 리소스 객체의 필드에 동적으로 접근하고 조작합니다. 이를 통해 다양한 타입의 Kubernetes 리소스를 처리할 수 있습니다.
- 기존 리소스와 변경된 리소스를 비교할 때 equality.Semantic.DeepEqual 함수를 사용하여 두 객체의 필드 값을 비교합니다.
```go
if equality.Semantic.DeepEqual(existing, obj) {
  return OperationResultNone, nil
}
```
- equality package의 [Semantic](https://github.com/kubernetes/apimachinery/blob/master/pkg/api/equality/semantic.go?utm_source=chatgpt.com)에서는 conversion을 사용하고 있고, 
- conversion의 [EqualitiesOrDie 함수](https://github.com/kubernetes/apimachinery/blob/master/pkg/conversion/deep_equal.go#L31)에서는 reflect.Equalities를 사용하고 있습니다.
- reflect package는 private field(소문자로 시작하는 필드)를 안전하게 다루지 않습니다. 예를 들어 생성하거나 수정하려는 field에 'age'라는 private field가 있다면, 이 값을 변경하려고 할 때 아래와 같은 에러가 발생합니다.
```shell
panic: reflect.Value.Set using value obtained using unexported field
```
- 따라서, API Spec에 대해서 private field를 선언하는 것을 피해야 합니다.

## Example
- 실제로 아래와 같이 CiliumNetworkPolicy 리소스를 CreateOrUpdate하는 코드를 작성했을 때 private field가 있으면 panic이 발생합니다.

```go
result, err := controllerutil.CreateOrUpdate(ctx, r.Client, ciliumNetworkPolicy, func() error {
  ciliumNetworkPolicy.Spec = spec.DeepCopy()
  return controllerutil.SetControllerReference(project, ciliumNetworkPolicy, r.Scheme)
})
if err != nil {
  return false, fmt.Errorf("failed to create or update CiliumNetworkPolicy: %w", err)
}
```

- 따라서 controllerutil을 사용하지 않고 직접 동기화를 진행하였습니다.

```go
ciliumNetworkPolicy.Spec = spec.DeepCopy()
if err := controllerutil.SetControllerReference(project, ciliumNetworkPolicy, r.Scheme); err != nil {
  return false, fmt.Errorf("failed to set controller reference: %w", err)
}

// Create or update the CiliumNetworkPolicy
existingCiliumNetworkPolicy := &ciliumv2.CiliumNetworkPolicy{}
hasUpdated := false
if err := r.Get(ctx, client.ObjectKey{Namespace: project.Name, Name: project.Name}, existingCiliumNetworkPolicy); err != nil {
  if client.IgnoreNotFound(err) != nil {
    return false, fmt.Errorf("failed to get CiliumNetworkPolicy: %w", err)
  }
  // CiliumNetworkPolicy does not exist, create it
  if err := r.Create(ctx, ciliumNetworkPolicy); err != nil {
    return false, fmt.Errorf("failed to create CiliumNetworkPolicy: %w", err)
  }
  hasUpdated = true
} else {
  // CiliumNetworkPolicy exists, check if it needs to be updated
  if !reflect.DeepEqual(existingCiliumNetworkPolicy.Spec, ciliumNetworkPolicy.Spec) {
    // Update the CiliumNetworkPolicy if it has changed
    existingCiliumNetworkPolicy.Spec = ciliumNetworkPolicy.Spec
    if err := r.Update(ctx, existingCiliumNetworkPolicy); err != nil {
      return false, fmt.Errorf("failed to update CiliumNetworkPolicy: %w", err)
    }
    hasUpdated = true
  }
}
```
