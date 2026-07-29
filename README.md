# Odyssey 통합 매뉴얼

> **버전**: v1
>
> **작성일**: 2026.04.27
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

#### [Part 1. 시작 가이드](/broken/pages/QvbgeCLmWH83CPBF2Fg2) <a href="#part-1" id="part-1"></a>

1. [Odyssey 실행 환경](https://mono-communications.github.io/odyssey-manual/#1-odyssey-%EC%8B%A4%ED%96%89-%ED%99%98%EA%B2%BD)
2. [패키지 구성](https://mono-communications.github.io/odyssey-manual/#2-%ED%8C%A8%ED%82%A4%EC%A7%80-%EA%B5%AC%EC%84%B1)
3. [첫 실행에 꼭 필요한 설정](https://mono-communications.github.io/odyssey-manual/#3-%EC%B2%AB-%EC%8B%A4%ED%96%89%EC%97%90-%EA%BC%AD-%ED%95%84%EC%9A%94%ED%95%9C-%EC%84%A4%EC%A0%95)
4. [실행 / 정지](https://mono-communications.github.io/odyssey-manual/#4-%EC%8B%A4%ED%96%89--%EC%A0%95%EC%A7%80)
5. [Web UI 살펴보기](https://mono-communications.github.io/odyssey-manual/#5-web-ui-%EC%82%B4%ED%8E%B4%EB%B3%B4%EA%B8%B0-multi-%EB%AA%A8%EB%93%9C-%ED%95%9C%EC%A0%95)
6. [테스트 발송 — SMS 1건](https://mono-communications.github.io/odyssey-manual/#6-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EB%B0%9C%EC%86%A1--sms-1%EA%B1%B4)
7. [자주 막히는 지점](https://mono-communications.github.io/odyssey-manual/#7-%EC%9E%90%EC%A3%BC-%EB%A7%89%ED%9E%88%EB%8A%94-%EC%A7%80%EC%A0%90)

#### Part 2. 설정 항목 상세 <a href="#part-2" id="part-2"></a>

8. [환경설정 파일 개요](https://mono-communications.github.io/odyssey-manual/#8-%ED%99%98%EA%B2%BD%EC%84%A4%EC%A0%95-%ED%8C%8C%EC%9D%BC-%EA%B0%9C%EC%9A%94)
9. [패스워드 암호화](https://mono-communications.github.io/odyssey-manual/#9-%ED%8C%A8%EC%8A%A4%EC%9B%8C%EB%93%9C-%EC%95%94%ED%98%B8%ED%99%94)
10. [DB 설정](https://mono-communications.github.io/odyssey-manual/#10-db-%EC%84%A4%EC%A0%95)
11. [사용 서비스](https://mono-communications.github.io/odyssey-manual/#11-%EC%82%AC%EC%9A%A9-%EC%84%9C%EB%B9%84%EC%8A%A4)
12. [테이블명 & 건수 & 주기 설정](https://mono-communications.github.io/odyssey-manual/#12-%ED%85%8C%EC%9D%B4%EB%B8%94%EB%AA%85--%EA%B1%B4%EC%88%98--%EC%A3%BC%EA%B8%B0-%EC%84%A4%EC%A0%95)
13. [기본 설정 (common.user)](https://mono-communications.github.io/odyssey-manual/#13-%EA%B8%B0%EB%B3%B8-%EC%84%A4%EC%A0%95-commonuser)
14. [계정 설정 (sessions)](https://mono-communications.github.io/odyssey-manual/#14-%EA%B3%84%EC%A0%95-%EC%84%A4%EC%A0%95-sessions)
15. [HA 이중화 설정 (ha.properties)](https://mono-communications.github.io/odyssey-manual/#15-ha-%EC%9D%B4%EC%A4%91%ED%99%94-%EC%84%A4%EC%A0%95-haproperties)
16. [Poseidon 모니터링 연동](https://mono-communications.github.io/odyssey-manual/#16-poseidon-%EB%AA%A8%EB%8B%88%ED%84%B0%EB%A7%81-%EC%97%B0%EB%8F%99)

#### Part 3. 발송 쿼리 모음 <a href="#part-3" id="part-3"></a>

17. [메시지 타입별 INSERT](https://mono-communications.github.io/odyssey-manual/#17-%EB%A9%94%EC%8B%9C%EC%A7%80-%ED%83%80%EC%9E%85%EB%B3%84-insert)
18. [MSG\_TYPE / STATUS 코드](https://mono-communications.github.io/odyssey-manual/#18-msg_type--status-%EC%BD%94%EB%93%9C)
19. [테이블 레이아웃 (MySQL)](https://mono-communications.github.io/odyssey-manual/#19-%ED%85%8C%EC%9D%B4%EB%B8%94-%EB%A0%88%EC%9D%B4%EC%95%84%EC%9B%83-mysql)

#### Part 4. 운영 가이드 <a href="#part-4" id="part-4"></a>

20. [Web UI 상세](https://mono-communications.github.io/odyssey-manual/#20-web-ui-%EC%83%81%EC%84%B8)
21. [게이트웨이 IP / PORT](https://mono-communications.github.io/odyssey-manual/#21-%EA%B2%8C%EC%9D%B4%ED%8A%B8%EC%9B%A8%EC%9D%B4-ip--port)
22. [로그 / 에러 분석](https://mono-communications.github.io/odyssey-manual/#22-%EB%A1%9C%EA%B7%B8--%EC%97%90%EB%9F%AC-%EB%B6%84%EC%84%9D)
23. [부가 설명](https://mono-communications.github.io/odyssey-manual/#23-%EB%B6%80%EA%B0%80-%EC%84%A4%EB%AA%85)
24. [전송 결과 및 참고자료](https://mono-communications.github.io/odyssey-manual/#24-%EC%A0%84%EC%86%A1-%EA%B2%B0%EA%B3%BC-%EB%B0%8F-%EC%B0%B8%EA%B3%A0%EC%9E%90%EB%A3%8C)
