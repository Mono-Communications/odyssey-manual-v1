# Odyssey 통합 매뉴얼

> **버전**: v1
>
> **작성일**: 2026.04.27
>
> **최종수정일**: 2026.07.29
>
> **고객센터**: 02-333-7223

## 들어가기 전에

이 프로그램은 본질적으로 외부의 위험한 상황에서 사용하도록 개발된 것이 아닙니다. 따라서 그런 목적으로 사용된 경우, 사용자는 응용 프로그램의 안전한 사용을 보장하기 위한 모든 적절한 안전 조치, 백업, 대비 및 기타 조치를 반드시 취해야 합니다. 프로그램이 이러한 목적으로 사용되었을 경우 ㈜모노커뮤니케이션즈는 이러한 프로그램 사용으로 인한 피해를 책임지지 않습니다.

이 프로그램(소프트웨어와 설명서 포함)은 저작권법, 특허 및 기타 지적재산권 관련 법규에 의해 보호됩니다. 이 프로그램을 리버스 엔지니어링하거나 분해하거나 또는 역 컴파일하는 것은 금지되어 있습니다.

사용자는 시스템 해킹을 방지하기 위하여 백신 프로그램을 이용한 주기적인 PC 관리를 하여야 하며, 아이디/비밀번호를 외부로 노출할 수 없고, 지정된 장소에서만 프로그램을 사용하여야 합니다.

이 문서의 내용은 사전 공지 없이 변경될 수 있습니다.

***

목차

{% hint style="info" %}
Odyssey를 처음 설치한다면 [**Part 1. 시작 가이드**](https://mono-communications.github.io/odyssey-manual/#part-1-%EC%8B%9C%EC%9E%91-%EA%B0%80%EC%9D%B4%EB%93%9C) 부터 따라가세요. 첫 SMS 실발송까지 단계별로 안내합니다.\
운영 중에는 [Part 2. 설정 항목 상세](https://mono-communications.github.io/odyssey-manual/#part-2-%EC%84%A4%EC%A0%95-%ED%95%AD%EB%AA%A9-%EC%83%81%EC%84%B8) / [Part 3. 발송 쿼리 모음](https://mono-communications.github.io/odyssey-manual/#part-3-%EB%B0%9C%EC%86%A1-%EC%BF%BC%EB%A6%AC-%EB%AA%A8%EC%9D%8C) / [Part 4. 운영 가이드](https://mono-communications.github.io/odyssey-manual/#part-4-%EC%9A%B4%EC%98%81-%EA%B0%80%EC%9D%B4%EB%93%9C)를 reference로 활용합니다.
{% endhint %}

#### Part 1. 시작 가이드 <a href="#part-1" id="part-1"></a>

1. [Odyssey 실행 환경](part-1./1.-odyssey.md)
2. [패키지 구성](part-1./2./)
3. [첫 실행에 꼭 필요한 설정](part-1./3..md)
4. [실행 / 정지](part-1./4..md)
5. [Web UI 살펴보기](part-1./5.-web-ui-multi.md)
6. [테스트 발송 — SMS 1건](part-1./6.-sms-1.md)
7. [자주 막히는 지점](part-1./7./)

#### Part 2. 설정 항목 상세 <a href="#part-2" id="part-2"></a>

8. 환경설정 파일 개요
9. [패스워드 암호화](part-2./9..md)
10. [DB 설정](part-2./10.-db/)
11. [사용 서비스](part-2./11./)
12. [테이블명 & 건수 & 주기 설정](part-2./12.-and-and/)
13. [기본 설정 (common.user)](part-2./13.-common.user/)
14. [계정 설정 (sessions)](part-2./14.-sessions/)
15. [HA 이중화 설정 (ha.properties)](part-2./15.-ha-ha.properties/)
16. [Poseidon 모니터링 연동](part-2./16.-poseidon.md)

#### Part 3. 발송 쿼리 모음 <a href="#part-3" id="part-3"></a>

17. [메시지 타입별 INSERT](part-3./17.-insert/)
18. [MSG\_TYPE / STATUS 코드](part-3./18.-msg_type-status/)
19. [테이블 레이아웃 (MySQL)](part-3./19.-mysql/)

#### Part 4. 운영 가이드 <a href="#part-4" id="part-4"></a>

20. [Web UI 상세](part-4./20.-web-ui/)
21. [게이트웨이 IP / PORT](part-4./21.-ip-port/)
22. [로그 / 에러 분석](part-4./22./)
23. [부가 설명](part-4./23./)
24. [전송 결과 및 참고자료](part-4./24..md)
