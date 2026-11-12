# Artifact Archive

A static snapshot of Claude artifacts, exported as plain HTML files.

## Contents

| File | Description |
|---|---|
| `index.html` | Landing page linking all article folders below |
| `<article>/index.html` | Per-article page linking its `en` / `ja` / `vi` versions |
| `<article>/<article>[-lang].html` + `.css` | The article and its extracted stylesheet |

Articles: `bao-cao-loi-viecoi`, `viecoi-fukugu-hokoku`, `quy-tac-bai-viet-vio-4028`, `cwv-lcp-investigation`, `viecoi-api-split` (en, ja, vi), `viecoi-cache-framework`.

## Note

One artifact — "Tóm tắt thay đổi VIO-4028 - Quy tắc hiển thị bài viết" — is a live Claude Docs document, not a standalone HTML artifact. Its content lives in the Claude Docs service rather than as static markup, so it couldn't be exported here. View it directly at:
https://claude.ai/artifact/KHW77nDn5EMRKHtybKkcRP

## Usage

Open `index.html` in a browser, or serve the folder with any static file server:

```
npx serve .
```
