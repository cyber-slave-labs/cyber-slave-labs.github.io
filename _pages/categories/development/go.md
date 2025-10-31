---
title: "Go"
permalink: /categories/go
toc: true
toc_sticky: true
---

<p>Kubernetes의 주된 개발 언어인 Go에 대해 알아봅시다. </p>

<div class="cards">
  <div class="card">
    <h3>controllerutil.CreateOrUpdate 동작 기전</h3>
    <p>CreateOrUpdate는 어떻게 수행될까? Reflect란 무엇인가?</p>
    <a href="/2025/10/31/createorupdate/" class="btn">읽어보기</a>
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