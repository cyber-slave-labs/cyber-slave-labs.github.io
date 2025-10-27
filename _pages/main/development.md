---
title: Development
permalink: /topic/development
toc: false
---

<div class="cards">
  <div class="card">
    <h3>Cilium</h3>
    <p>eBPF 기반 쿠버네티스 네트워킹 솔루션</p>
    <a href="/categories/cilium" class="btn">자세히 보기</a>
  </div>

  <div class="card">
    <h3>Longhorn</h3>
    <p>클라우드 네이티브 분산 스토리지 시스템</p>
    <a href="/categories/longhorn" class="btn">자세히 보기</a>
  </div>

  <div class="card">
    <h3>Kubernetes</h3>
    <p>컨테이너 오케스트레이션 플랫폼</p>
    <a href="/categories/kubernetes" class="btn">자세히 보기</a>
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