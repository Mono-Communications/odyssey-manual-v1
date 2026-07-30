# 11. 사용 서비스

<mark style="color:red;">`common.execute`</mark> 와 <mark style="color:red;">`common.transmission`</mark> 영역에서 사용할 메시지 종류와 발송 경로를 설정합니다.

```yaml
common:
  execute:
    sms: true
    lms: true
    mms: true
    vms: true
    rcs: true
    kakao: true
    fetch: true
  transmission:
    msg: KT
    rcs: KT
    kakao: CPAAS
```
