# Markdown Viewer

純前端 Markdown 即時預覽工具，無需安裝，開啟即用。

**線上版本：** https://cyhbench.github.io/markdownReader/

## 功能

- 即時預覽 — 輸入後 150ms 自動渲染
- 語法高亮 — 支援 100+ 程式語言（highlight.js）
- 程式碼複製按鈕 — 滑鼠懸停或觸控裝置直接顯示
- 匯出 HTML — 一鍵下載含樣式的靜態 HTML
- 自動儲存 — 內容存入 localStorage，重新整理不遺失
- 深色模式 — 跟隨系統偏好自動切換
- RWD — 手機單頁 tab 切換、桌面左右分割

## 使用方式

直接開啟線上版本，或將 `index.html` 下載後在瀏覽器開啟（離線可用）。

```
git clone https://github.com/cyhbench/markdownReader.git
# 直接用瀏覽器開啟 index.html 即可
```

## 技術細節

| 項目 | 版本 / 說明 |
|------|------------|
| [marked](https://github.com/markedjs/marked) | `4.3.0`（鎖版，v5+ 移除 `highlight` option）|
| [highlight.js](https://highlightjs.org/) | `11.9.0` |
| CDN | jsDelivr（marked via npm；highlight.js via cdn-release）|
| 儲存 | localStorage（無伺服器、無 cookie）|

> **注意：** highlight.js 的 browser bundle 不在 npm 套件內，需使用 `cdn-release` 路徑：
> `https://cdn.jsdelivr.net/gh/highlightjs/cdn-release@11.9.0/build/highlight.min.js`

## 版本記錄

| 版本 | 日期 | 變更 |
|------|------|------|
| v1.4 | 2026-04-08 | 修正 highlight.js CDN URL（404）、加 render() 錯誤處理、mangle:false |
| v1.3 | 2026-04-01 | 鎖定 marked@4.3.0、加語法高亮、觸控複製按鈕、addEventListener 重構 |
| v1.2 | 2026-03-21 | 修正小螢幕文字換行（break-word / overflow-wrap: anywhere）|
| v1.1 | 2026-03-21 | 初版 |
