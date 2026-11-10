# CLAUDE.md — markdownReader

## 專案概述
純前端 Markdown 預覽工具，依賴 marked v4 + highlight.js + DOMPurify。

## 重要：marked 版本鎖定
CDN 一定要鎖定到 `marked@4.3.0`，**不能用無版本號**。
marked v5+ 移除了 `highlight` 和 `headerIds` option，對應 CDN 會默默讓語法高亮失效。

## 安全規則
- Markdown 支援 HTML 內嵌，但 `marked.parse()` 的輸出一定要經 `DOMPurify.sanitize()` 再寫進 `innerHTML`：線上版在 `cyhbench.github.io`，和其他工具同 origin、共用 localStorage，貼上別人的 .md 若有 `onerror` 之類的 script 會讀到其他工具的資料
- 錯誤訊息等非 Markdown 的文字用 `textContent`，不拼進 `innerHTML`
- 所有按鈕用 `addEventListener` 綁定，不用 `onclick` 屬性

## 已知風險與對策
| 風險 | 對策 |
|------|------|
| marked 版本升級破壞 API | CDN 鎖 `marked@4.3.0` |
| 內嵌 HTML 執行 script（XSS） | `DOMPurify.sanitize()`，CDN 鎖版本 |
| 觸控裝置看不到複製鈕 | `@media (hover: none) .copy-btn { opacity: 1 }` |
| localStorage QuotaExceededError | setItem 包 try/catch |
| URL.createObjectURL 洩漏 | setTimeout revokeObjectURL |
| clipboard 失敗無回應 | .catch() 顯示失敗狀態 |

## 不要做的事
- 不要擅自升級 marked CDN 版本
- 不要使用 `marked.setOptions` 外的 v5+ API（`marked.use()`），除非同時更改 CDN 到 v5+
