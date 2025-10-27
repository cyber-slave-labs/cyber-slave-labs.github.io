---
title: "Cilium"
permalink: /categories/cilium
toc: true
toc_sticky: true
---

<p>회사에서 k8s cluster의 CNI 플러그인으로 Cilium을 사용했습니다. Cilium이 무엇인지, 어떤 특징이 있는지 정리해봅니다. 🚀</p>
<p>그리고 cilium을 공부할 겸 준비한 Cilium Certificate Associate (CCA) 시험 후기 글도 작성해보았습니다. 🎉</p>

<div class="cards">
  <div class="card">
    <h3>What is Cilium?</h3>
    <p>Cilium의 기본 개념과 특징, 작동 원리에 대한 소개</p>
    <a href="/2025/10/27/what-is-cilium/" class="btn">읽어보기</a>
  </div>

  <div class="card">
    <h3>Cilium Certified Associate(CCA) 시험 후기 및 꿀팁</h3>
    <p>Cilium 자격증 시험 준비 과정과 합격 노하우 공유</p>
    <a href="/2025/10/27/cilium-certificate-review/" class="btn">읽어보기</a>
  </div>
</div>

<style>
.cards {
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin: 20px 0;
}

.card {
  border: 1px solid #eee;
  border-radius: 8px;
  padding: 20px;
  background-color: #fff;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
  transition: transform 0.2s ease-in-out;
  width: 100%;
}

.card:hover {
  transform: translateY(-3px);
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
}

.card h3 {
  margin-top: 0;
  color: #333;
  font-size: 1.4em;
}

.card p {
  color: #666;
  margin-bottom: 15px;
  font-size: 1em;
}

.btn {
  display: inline-block;
  background-color: #4285F4;
  color: white !important;
  padding: 8px 16px;
  border-radius: 4px;
  text-decoration: none;
  font-size: 0.9em;
  transition: background-color 0.2s;
}

.btn:hover {
  background-color: #3367D6;
}
</style>