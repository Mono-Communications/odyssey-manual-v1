# 8. 환경설정 파일 개요

Odyssey의 환경설정은 두 개의 파일로 구성됩니다.

<table><thead><tr><th width="212">파일</th><th>위치</th><th>용도</th></tr></thead><tbody><tr><td><strong><code>application.yml</code></strong></td><td>Odyssey 설치 폴더 / <mark style="color:red;"><code>config/</code></mark></td><td>DB, 사용 서비스, 세션, Pipeline, Poseidon 등 모든 운영 설정</td></tr><tr><td><strong><code>ha.properties</code></strong></td><td>Odyssey 설치 폴더 / <mark style="color:red;"><code>config/</code></mark></td><td>HA 이중화 노드 정보, DB Lease, 로드밸런싱 (HA 프로파일 전용)</td></tr><tr><td><strong><code>senderId.yml</code></strong></td><td>Odyssey 설치 폴더 / <mark style="color:red;"><code>config/</code></mark></td><td>GSMS 발송 전용 sender-id 매핑 설정</td></tr></tbody></table>

{% hint style="info" %}
설정 파일을 변경한 경우 Odyssey를 재구동해야 적용됩니다. 단, 일부 항목은 내장 Web UI를 통해 무중단 변경이 가능합니다.
{% endhint %}
