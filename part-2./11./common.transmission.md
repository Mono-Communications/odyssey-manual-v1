# common.transmission (발송 경로 선택)

각 메시지 그룹별로 어떤 게이트웨이를 통해 발송할지 지정합니다. ([3-3. 발송 게이트웨이](../../part-1./3.-settings.md#id-3-2-commonexecute), [3-6. 게이트웨이 세션](../../part-1./3.-settings.md#id-3-5-commontablesfetch-count) 참고)

```yml
transmission:
  msg: KT
  rcs: KT
  kakao: CPAAS
```

### <mark style="color:blue;">msg</mark> - 문자(SMS/LMS/MMS/VMS) 발송 경로

<table><thead><tr><th width="239.5999755859375">값</th><th>의미</th></tr></thead><tbody><tr><td><strong><code>KT</code></strong></td><td>KT 크로샷(직접 연동)으로 발송</td></tr><tr><td><strong><code>CPAAS</code></strong></td><td>CPaaS API를 통해 발송 (VMS는 KT 발송만 가능)</td></tr></tbody></table>

### <mark style="color:blue;">rcs</mark> - RCS 발송 경로

<table><thead><tr><th width="241.2000732421875">값</th><th>의미</th></tr></thead><tbody><tr><td><strong><code>KT</code></strong></td><td>KT RCS Hermes API로 발송</td></tr><tr><td><strong><code>CPAAS</code></strong></td><td>CPaaS API를 통해 발송</td></tr></tbody></table>

### <mark style="color:blue;">kakao</mark> - 카카오 알림톡/친구톡 발송 경로

<table><thead><tr><th width="239.60003662109375">값</th><th>의미</th></tr></thead><tbody><tr><td><strong><code>MN</code></strong></td><td>엠앤와이즈 API로 발송</td></tr><tr><td><strong><code>CPAAS</code></strong></td><td>CPaaS API를 통해 발송</td></tr></tbody></table>

{% hint style="info" %}
<mark style="color:blue;">언제 바꾸나여?</mark> 계약된 발송 경로와 <mark style="color:blue;">**반드시 일치**</mark>해야 합니다. 경로가 이중화된 경우(KT 기본, CPaaS 백업 등) 장애 시에만 수동 변경하며, 평상시에는 주 경로를 유지합니다.
{% endhint %}
