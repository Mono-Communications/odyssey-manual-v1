---
description: 폴링 주기
---

# 12-3. cycle

```yaml
cycle:
      fetch: 1000
      db-check-interval: 30000
```

<table><thead><tr><th width="195.4000244140625">옵션</th><th width="349.5999755859375">설명</th><th>권장값</th></tr></thead><tbody><tr><td>fetch</td><td>메시지 폴링(DB SELECT) 주기 (단위: 밀리초)</td><td>1000 (1초)</td></tr><tr><td>db-check-interval</td><td>DB 연결 상태 체크 주기 (단위: 밀리초)</td><td>30000 (30초)</td></tr></tbody></table>

