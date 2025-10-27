---
title: "Cilium Certified Associate (CCA) 시험 후기 및 꿀팁"
toc: true
toc_sticky: true
categories: ["Cilium"]
excerpt: Cilium Certified Associate (CCA) 시험 후기 및 꿀팁
---

## What is CCA?
Linux Foundation에서 주관하는 Cilium Certified Associate (CCA) 시험이 있다. Cilium은 k8s cluster안에서 CNI 툴로 자주 사용되는 툴인데, 내가 속한 팀에서 manage하는 k8s cluster에서도 CNI 툴로 cilium을 사용 중이어서 공부도 할 겸 시험을 봤다.

사실 CCA 시험이 LF에서도 나온지 얼마 안된 시험이라 따로 소스를 찾아봐도 없고 한국어로 된 꿀팁같은건 당연히 없었다. 그래서 한국어로 된 후기나 꿀팁이 있으면 좋을 것 같아서 이렇게 글을 쓰게 되었다.

시험을 등록하는데에는 $250가 드는데, 나는 좋은 기회로 회사에서 공짜로 시험을 보게 해주셔서 돈을 안내고 볼 수 있었다.

## How to Prepare for CCA?

시험을 준비하는데에는 일주일 정도가 소요되었고, 나는 이미 회사에서 cilium을 사용하고 있었기 때문에 어느정도 조금의 지식은 있는채로 공부를 했다. 아마 노베이스로 공부를 시작한다면 (k8s 숙련자 기준) 2주에서 1달정도를 잡으면 적당하지 않을까 싶다.

시험은 4지선다 객관식으로 총 60문제가 나오며 90분이 주어진다. 생각보다 시간이 빡빡해서 30분만에 다 풀고 나오겠다는 시험 전의 포부와는 다르게 필자는 80분 정도가 소요되었다 ㅎㅎ;; 시험의 난이도에 대해서는 마지막쯔음에 다시 한번 이야기 하겠다.

시험은 PSI를 이용해서  보게 되는데 CKA나 다른 LF주관 시험을 본 사람이면 알겠지만 시험 시작 전에 감독관이 카메라를 이용해서 주변 검사를 하는게 정말 빡빡하다 ;; 2년 전 CKA 시험을 봤을 때보다 더 빡빡해진 느낌이라 참 귀찮았다 ...

필자가 시험 준비를 할 때 이용했던 사이트는 아래와 같다.

- [CCA Study Guide](https://github.com/isovalent/CCA-Study-Guide)

- [Example Questions](https://cca.purutuladhar.com/)

- [cilium docs](https://docs.cilium.io/en/stable/index.html)

## About CCA

Study Guide 사이트에도 나와 있듯이 CCA 시험은 총 8가지 섹션으로 나눠진다.

- Architecture (20%)

- Network Policy (18%)

- Service Mesh (16%)

- Network Observability (10%)

- Installation and Configuration (10%)

- Cluster Mesh (10%)

- eBPF (10%)

- BGP and External Networking (6%)


이렇게 cilium에 관련된 여러 분야에 대해 문제가 나오고 실제 시험에서 문제 순서는 뒤죽박죽 나온다. 그래서 조금 헷갈릴수도 있다 ;;

필자는 각 섹션별로 ChatGPT 선생님과 함께 cilium docs를 보면서 공부했다. GPT 선생님과 함께 공부하면서 내용을 정리했는데 링크는 아래와 같다.

>[CCA Notes](https://cyber-slave.notion.site/cca)

이건 그냥 보면서 슥슥 대충 정리한거라 이것만 보면 안된다 !!! 반드시 이것과 함께 각 섹션별 cilium docs를 참고해서 공부해야 통과할 수 있다.

시험의 난이도는 위에서 제공했던 [Example Questions](https://cca.purutuladhar.com/) 의 난이도보다 조금 높다고 생각하면 된다. 필자는 Example Question을 풀 때 1,2개정도 틀렸는데 시험은 생각보다 어려워서 당황했다 ㅎㅎ;;

그리고 Example Questions의 정답을 100% 신뢰하지 말자. 이것은 개인이 만든 사이트(나아님)기 때문에 내 생각엔 틀린 답변이 몇가지 있는 것 같다. 그러니 GPT 선생님과 함꼐 적당히 걸러가면서 참고하도록 하자.

그렇게 공부해서 시험을 통과하면 멋쟁이 뱃지를 얻을 수 있다 !

![Cilium CCA Badge](/images/development/cilium/cca.png)