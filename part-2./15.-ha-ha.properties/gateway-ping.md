# Gateway PING 체크

게이트웨이 생존을 주기적으로 확인하여 네트워크 단절 시 자동으로 Failover를 트리거합니다.

| OS      | PING\_CMD                |
| ------- | ------------------------ |
| Linux   | ping -c 1 -W 1 \[target] |
| Windows | ping \[target] -n 1      |

{% hint style="info" %}
`[target]`은 게이트웨이 IP 또는 기본 게이트웨이(라우터) IP를 입력합니다. 설치 시 OS 유형에 맞춰 **한 번만** 수정하면 운영 중 바꿀 일이 없습니다.
{% endhint %}
