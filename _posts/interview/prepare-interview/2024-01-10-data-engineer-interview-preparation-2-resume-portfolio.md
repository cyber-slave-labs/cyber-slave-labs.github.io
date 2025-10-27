---
title: "데이터 엔지니어 이직 준비법 (2) - 이력서 및 포트폴리오 작성"
toc: true
toc_sticky: true
categories: ["Interview"]
excerpt: 데이터 엔지니어 이직 준비법 (2) - 이력서 및 포트폴리오 작성
---

# 데이터 엔지니어 이직 준비법 (2) - 이력서 및 포트폴리오 작성

## 이력서 작성
이후 이력서를 직접 작성해보았는데, 이력서를 작성하고, 다시 끊임없이 읽어보며 고치고 또 고치는 과정을 반복했다. 이력서를 처음 작성해보는 사람들이 가장 많이 하는 실수가 너무 자신이 한 것을 detail하게 이력서에 적는 것인 것 같다. 나 또한 처음 이력서를 작성할 때 아무 생각 없이 너무 디테일적인 부분까지 이력서에 적어 넣어서 이력서가 너무 난잡해지는 느낌이었다. 

예를 들어 처음에 작성한 난잡한 예시는 다음과 같다.

```markdown
Events Pipeline 설계 및 유지보수
- 게임에서 발생하는 event들을 FastAPI를 통해 개발한 Event API Server을 통해 받아와서 Kafka를 통해 데이터를 받아옴
- IaC 툴인 pulumi를 이용하여 Infrastructure을 설계하였으며, knative, istio 등을 활용하여 EKS cluster 상에 서비스 환경을 구축함.
- knative의 hpa 기능을 이용하여 cpu metric을 기준으로 한 autoscaling을 적용함. 이에 따 라 변화하는 cpu 사용량에 자동으로 대응하여 autoscaling이 적절하게 일어나도록 함.
- 동일한 key를 가진 data는 동일한 partition으로 들어가며 순서가 보장된다는 kafka의 성질 을 이용하여 key를 user_id로 설정하여 같은 User에 대하여 event의 순서를 보장시켰으며, 이 를 활용하여 차후 project로 kafka streams를 이용하여 한 user의 purchase event 발생 이 전 context 분석을 수행해냄.
- Kafka Pipeline에 대한 Failover 정책으로 Kinesis Pipeline을 구축하여 동일 route53 endpoint에 대해 failover 정책으로 등록해둠. Kinesis Pipeline같은 경우에는 Kinesis와 Lambda의 조합을 통해 데이터를 받아오고 프로세싱함.
- Event Data의 경우 이슈가 발생하면 drop된 event를 복구하는 것이 불가능에 가깝기 때문 에 세심하게 다뤄야 함. 따라서, prometheus의 alert manager을 활용하여 confluent topic 에 대해 received_byte의 metric을 감지하여 적절한 PromQL 조건을 만족하였을 경우 slack으로 alert를 보내도록 구성함.
```

하지만 이는 읽는 사람 입장에서 한눈에 들어 오지 않을 뿐더러 디테일적인 측면이 너무 많이 적혀있어 이력서가 난잡해지게 만드는 요인이다. 따라서 여러번의 수정을 거쳐 이를 아래와 같이 바꾸었다.

```markdown
 Events Pipeline 관리 및 성능안정성 증대
- Kafka를 이용한 실시간 Event Pipeline 관리 및 ​failover-pipeline으로 Kinesis를 사용하 여 안정성 극대화 결과 99.9991% 이상의 가용률 달성
- ELK를 이용한 실시간 데이터 모니터링
- Prometheus의 alert manager을 활용하여 이상상황 발생 시 즉각 Alert 발생 + Grafana 를 이용한 모니터링
```

이력서를 읽는 면접관들은 이력서를 보고 내가 어떤 프로젝트를 어떤 식으로 진행했는지 디테일하게 알고 싶은것이 아니다. 그들에게 중요한것은 내가 어떤 프로젝트를 진행했고, 이를 통해 어떤 결과물을 도출했는지, 그 과정에서 가장 가치있었던 점은 무엇인지다.

따라서 이력서를 쓸 때는 너무 디테일하게 써서 이력서 자체를 난잡하게 쓰지 말고, 정말 core한 concept를 위주로 쓰도록 노력해보자. 또한, 실제 그 프로젝트를 통해 어떤 상과를 이루어냈는지 수치적인 측면을 강조하여 쓰면 매우 좋다.

이력서의 템플릿은 wanted에서 제공하는 기본 템플릿이 가장 깔끔한 것 같아서 나는 wanted의 템플릿을 사용했다. 실제 주변의 많은 다른 개발자들도 wanted 템플릿을 사용하여 이력서를 작성하더라 !

## 포트폴리오 작성

포트폴리오는 사실 이력서의 연장선인 것 같다. 이력서에서는 compact하게 자신이 한 프로젝트나 일을 소개했다면 포폴에서는 조금 더 deep dive하여 소개하는 느낌이다. 자신이 직접 한 프로젝트를 github 등에 올려두었다면 github link를 거는 것도 좋은 방법이 될 수 있으며, 개발한 코드의 core한 부분만을 설명하며 포트폴리오를 작성하는 방식도 좋을 것 같다. 이외에도 linkedin 계정이나 수상 내역, 학력, skill, 경력 등을 적는다.
