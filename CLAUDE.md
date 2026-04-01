# CLAUDE.md — markdownReader

## 專案概述
純前端 Markdown 預覽工具，依賴 marked v4 + highlight.js。

## 重要：marked 版本鎖定
CDN 一定要鎖定到 `marked@4.3.0`，**不能用無版本號**。
marked v5+ 移除了 `highlight` 和 `headerIds` option，對應 CDN 會默默刺残語法高亮功能。

## 安全規則
- `preview.innerHTML = marked.parse(md)` 是故意設計（Markdown 支援 HTML 內嵌），這是个人工具不處理不可信輸入
- 所有按鈕用 `addEventListener` 綁定，不用 `onclick` 屬性

## 已知風險與對策
| 風險 | 對策 |
|------|------|
| marked 版本升級破壞 API | CDN 鎖 `marked@4.3.0` |
| 觸控裝置看不到複製鈕 | `@media (hover: none) .copy-btn {{ opacity: 1 }}` |
| localStorage QuotaExceededError | setItem 包 try/catch |
| URL.createObjectURL 浩漏 | setTimeout revokeObjectURL |
| clipboard 失敗無回應 | .catch() 顯示失敗狀態 |

## 不要做的事
- 不要空空升級 marked CDN 版本
- 不要使用 `marked.setOptions` 外的 v5+ API（`marked.use()`），除非同時更改 CDN 到 v5+