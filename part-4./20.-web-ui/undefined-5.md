# 20-4. 세션 설정

통신사별 세션(계정) 정보를 카드 형태로 관리합니다. <mark style="color:red;">**`appliaction.yml`**</mark>의 <mark style="color:green;">**`kt`**</mark> / <mark style="color:green;">**`rcs`**</mark> / <mark style="color:green;">**`cpaas`**</mark> / <mark style="color:green;">**`kakao`**</mark> 영역의 <mark style="color:green;">`sessions`</mark> 에 해당합니다.

* **KT 크로샷 세션**: RCS IP:PORT, SP ID, SP Password, End User, Auth file 등
* **KT RCS 세션**: Send URL, Auth URL, 인증 정보 (ID, Secret 등)
* **카카오 세션**: 엠앤와이즈 카카오 직접 연동 정보
* **CPaaS 세션**: KT CPaaS API 연동 정보

각 세션은 카드 UI로 표시되며, **추가/삭제** 버튼으로 세션을 관리할 수 있습니다.

<figure><img src="../../.gitbook/assets/15_세션_설정_xro.png" alt="그림 15. 세션 설정 — KT 크로샷 (SP ID, 접속 정보, SMS/LMS/MMS 토글)"><figcaption><p>그림 15. 세션 설정 — KT 크로샷 (SP ID, 접속 정보, SMS/LMS/MMS 토글)</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/16_세션_설정_rcs.png" alt="그림 16. 세션 설정 — KT RCS (Send/Auth URL, 인증 정보, Report Cycle)"><figcaption><p>그림 16. 세션 설정 — KT RCS (Send/Auth URL, 인증 정보, Report Cycle)</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/17_세션_설정_kko.png" alt="그림 17. 세션 설정 — 카카오 (엠앤와이즈 카카오 직접 연동)"><figcaption><p>그림 17. 세션 설정 — 카카오 (엠앤와이즈 카카오 직접 연동)</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/18_세션_설정_cpaas.png" alt="그림 18. 세션 설정 — CPaaS (KT CPaaS API)"><figcaption><p>그림 18. 세션 설정 — CPaaS (KT CPaaS API)</p></figcaption></figure>
