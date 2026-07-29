# 세션 매핑

`common.transmission` 설정에 따라 사용하는 세션 영역이 결정됩니다.

| common.transmission 값 | 사용 세션 영역       | 게이트웨이              |
| --------------------- | -------------- | ------------------ |
| msg: KT               | kt.sessions    | KT 크로샷 (문자 직접 연동)  |
| msg: CPAAS            | cpaas.sessions | KT CPaaS (문자 API)  |
| rcs: KT               | rcs.sessions   | KT RCS Hermes API  |
| rcs: CPAAS            | cpaas.sessions | KT CPaaS (RCS API) |
| kakao: MN             | kakao.sessions | 엠앤와이즈 직접 연동        |
| kakao: CPAAS          | cpaas.sessions | KT CPaaS (카카오 API) |
