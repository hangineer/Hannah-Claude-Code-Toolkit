# API 層

- API 呼叫必須透過 `src/plugins/api.ts` 注入的 `$api`，不能直接使用 fetch 或 ky
- API response 的型別定義要放在對應的 `src/api/*/types.ts`
