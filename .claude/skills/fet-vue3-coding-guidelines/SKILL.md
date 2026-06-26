---
name: fet-vue3-coding-guidelines
description: 依 FET 團隊規範審查（非 Vue 官方規範）審查 Vue 3 程式碼，包含 BEM 命名、on- 事件前綴、ESLint 規則、資料夾結構。當使用者要求 review MR/PR 或請 Claude 協助撰寫符合團隊規範的元件時使用。
---

# Vue 3 Coding Guidelines

依據團隊內部規範整理。審查 Vue 3 程式碼時，依下列項目逐一檢查，並指出違反項目與建議修正方式。

## 命名風格總則

- `camelCase`：`.js` / `.ts`、`.css|.scss|.sass|.less`
- `PascalCase`：`.vue` 畫面與模組（元件檔名）
- `kebab-case`：設定檔（`.yml`、`Dockerfile` 等）、媒體檔案、router path（如 `location-agreement/edit`）
- router name 使用 `camelCase`（如 `locationAgreement`）

## CSS 命名（Tailwind + BEM）

- 使用 Tailwind CSS JIT mode，搭配 BEM 命名規則
- Block：`.c-btn`、`.c-card`
- Element：兩個底線連接，如 `.c-btn__content`
- Modifier：兩個連字號連接，如 `.c-btn__content--large`
- 共用元件的 Default CSS 須與元件名稱相同（`<c-btn>` 對應 `.c-btn`）
- 不使用巢狀結構（SASS / CSS nesting）
- 非必要不得使用 `!important`

## Vue 元件規則

- 採用 `<script setup>` 風格，標籤順序固定為 `template -> script -> style`
- 自訂事件以 `on-` 開頭：`$emit('on-search')`，監聽端 `@on-search="handleDoSomething"`
- Props 為多字組合時使用 `camelCase`（`dataList`）；父層傳遞 props 給子層時使用 `kebab-case`（`:data-list="..."`）
- 常數 `const` 全域不變動值使用 `UPPERCASE`（如 `USER_NAME`），一般變數 `let` 使用 `camelCase`
- `ref()` / `reactive()` 變數使用 `camelCase`
- class 類別使用 `PascalCase`
- Element 上的 `ref` 使用 `camelCase` + `Ref` 後綴（如 `componentRef`）
- `v-on` 用法：有值才加括號（`@click="triggerAction"` vs `@click="triggerAction(state)"`）
- `<template>` 內不可寫註解
- 元件內不使用 `i18n`（i18n 屬於頁面層）
- 如使用原生元件，優先透過 `v-bind="$attrs"` 繼承原生功能；若 Web API 已提供功能，優先使用 Web API
- 不使用巢狀 CSS / `!important`，共用元件放在 `/utils`
- 透過 `computed()` 管理狀態：預設狀態設為 `true`，不同類別狀態使用不同 `computed()`

## 函式 / 變數命名慣例

- Pinia / Vuex actions：`create` / `get` / `update` / `delete`（CRUD）
- API request：`getUserList`、`postUserList`、`patchUserList` / `putUserList`、`deleteUserList`
- Boolean：
  - 判斷是否有/為某值：`has-`（`hasPermission`）、`is-`（`isPermission`）、`show-`（`showTimeAgo`）
  - 判斷是否可執行動作：`can-`（`canDuplicate`）
  - `disabled` 不需額外加前綴
- 函式（動詞 + 名詞）：
  - 取值：`get-`（`getCountryList`）
  - 設值：`set-`（`setPosition`）
  - 格式轉換：`to-`（`toThousands`、`toFormatDate`）
  - 篩選：`filter-`（`filterUserList`）
  - 清空/恢復預設：`reset-`（`resetForm`）
  - 狀態切換：`handle` / `change` / `toggle` / `trigger`
  - 驗證/比對：`validate`
- i18n key：`camelCase`，非共用 i18n 獨立拉到對應功能的 `custom` 分類下

## 短路求值

- 短路求值（`&&`）僅用於**有回傳值**的情境：
  ```javascript
  // 使用
  const callback = fn => {
      return typeof fn === "function" && fn()
  }
  // 避免（純執行 side effect 不應用短路求值）
  const callback = fn => {
      typeof fn === "function" && fn()
  }
  ```
- 單純執行（無回傳值）應使用 `if`：
  ```javascript
  const callFunction = fn => {
      if (typeof fn === "function") fn()
  }
  ```

## ESLint 重點規則

- 禁用 `new Function`（`no-new-func`）、禁用 `var`（`no-var`）
- 結尾須加分號（`semi`）、末尾禁用逗號（`comma-dangle`）
- 箭頭函式括號：單參數不加括號、多參數加括號、無參數加空括號（`arrow-parens`）
- 檢查未使用變數（`no-unused-vars`）、最大行長限制（`max-len`）
- 元件名稱需為兩個單字組成（`vue/multi-word-component-names`）
- 元件 tag 順序：`template -> script -> style`（`vue/component-tags-order`）
- 屬性排序（`vue/attributes-order`）、`defineProps`/`defineEmits` 順序（`vue/define-macros-order`）

## 資料夾與檔案結構

- `components/`：共用組件，依功能命名；耦合元件以父層名稱開頭（如 `TableHeader.vue`、`TableBody.vue`）
- `views/[PascalCase]/`：`index.vue` 為主頁面，子組件用 `PascalCase` 命名
- `stores/`：Pinia，每個功能一個檔案，`camelCase` 命名
- `api/`：`index.js` 為引入點，`common.js` 為共用 API，其餘 `camelCase.js`
- `locales/translations/`：依 RFC 4646 命名（`en.json`、`zh-TW.json`、`ja-JP.json` ...）
- `tests/unit/components|views`：測試檔案對應 `[PascalCase].test.ts`
- `.env`：變數以 `VITE_` 前綴，且依英文字首順序排列

## 審查輸出格式

針對提交的程式碼，逐項列出：

- ✅ 符合規範的項目（簡述）
- ❌ 違反項目：指出檔案/行號、違反的規則、建議修正方式

若規則未涵蓋的情境（例如新元件設計），可依共用元件開發指南提出建議：規劃 props/slots/events、CSS 與元件同名管理、撰寫測試案例、Storybook 整理。
