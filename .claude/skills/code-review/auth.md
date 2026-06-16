# Auth / Keycloak

- Auth 流程走 router guard chain（Keycloak 驗證 → OAuth cleanup → profile fetch → permission check），不能跳過或重排
- 不在 component 裡直接呼叫 Keycloak SDK，auth 邏輯屬於 `src/stores/auth.ts` 和 `src/router/`
