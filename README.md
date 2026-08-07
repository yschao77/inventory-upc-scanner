# inventory-upc-scanner

獨立的 UPC／EAN 相機掃碼頁，供 Google Apps Script 盤點系統以 `window.open` 呼叫。

## 為什麼要獨立 repo？

Google Apps Script 網頁跑在沙箱 iframe 內，**不能直接使用相機**。  
因此掃碼必須開到**公開 HTTPS 網域**；此 repo 專門託管掃碼頁。

## 技術

- ZBar WASM（`@undecaf/barcode-detector-polyfill`）
- 只辨識：`upc_a` / `upc_e` / `ean_8` / `ean_13`
- 橫向掃描框 + 後鏡頭 +（支援時）輕微 zoom
- 掃到後導向 GAS callback：`?action=scanResult&token=...&code=...`
- 盤點頁以 token 輪詢 `pollScanResult`，不依賴 `window.opener` / `postMessage`

## 網址（GitHub Pages）

```
https://yschao77.github.io/inventory-upc-scanner/?token=TOKEN&callback=GAS_WEBAPP_URL
```

## 本機測試

用任何靜態伺服器開 `index.html`（需 HTTPS 或 localhost 才能開相機）。
