---
name: Canva MCP 連線設定
description: 把 OpenCode 連到 Canva（含 Canva 教育版）MCP。用於新電腦安裝、重新登入、更換帳號、排除連線失敗，以及確認教育版權限是否生效。
---

# Canva MCP 連線設定

## 核心觀念：兩條路，一定要選對

OpenCode 連 Canva 有兩個端點，行為完全不同：

| 端點 | 需要自建 app？ | 誰能授權 | 用法 |
| --- | --- | --- | --- |
| `https://mcp.canva.com/mcp` | ❌ 不用 | **任何 Canva 帳號（含教育版）** | ✅ **一律用這個** |
| `https://api.canva.com/connect/v1/mcp` | ✅ 要 `client_id` / `client_secret` | **只有 app 擁有者本人** | ❌ 不要用 |

### 為什麼不要用第二個

`api.canva.com` 是「開發者自建 app」的路徑。未發布的 app（development 狀態）**只有建立它的帳號能授權**，所以其他帳號（例如教育帳號）會看到 **「用戶端 ID 無效」**。要讓別人能用，得把 app 送 Canva 審核發布 —— 對個人用途完全不值得。

`mcp.canva.com` 是 Canva 官方的 **AI Connector 公開端點**，用的是 Canva 自家的 app，所以**教育帳號可以正常授權**。它支援 **DCR（動態註冊）與 CIMD**，因此設定檔**不需要任何 `client_secret`**。

## 設定步驟（約 2 分鐘）

### 1. 加入伺服器

```sh
opencode mcp add canva-edu --global --url https://mcp.canva.com/mcp
```

`--global` 讓這台電腦的所有專案都能用；只給單一專案用就省略它。

或手動在 `opencode.json` 的 `mcp.servers` 底下加：

```jsonc
"canva-edu": {
  "type": "remote",
  "url": "https://mcp.canva.com/mcp"
}
```

> 不要加 `oauth` 區塊。留空 OpenCode 才會走 DCR / CIMD 自動註冊。

### 2. 確認狀態

```sh
opencode mcp list
```

應顯示：

```text
⚠ canva-edu  needs authentication
```

### 3. 登入

1. 開 OpenCode → 輸入 **`/mcps`**
2. 選 **`canva-edu`** → **Sign in**
3. 瀏覽器打開後 → **登入要用的 Canva 帳號** → 按「允許」

登入成功後再跑 `opencode mcp list`，會變成：

```text
✓ canva-edu connected
```

## 驗證權限是否生效

呼叫 **`list-brand-kits`**：

- 回傳含品牌工具組 ID → ✅ **Pro 等級／教育版權限已生效**
- 回傳 `{items: []}` → 可能是該帳號還沒建立品牌工具組，不代表失敗

其他可驗證項目：`search-brand-templates`、`resize-design`、`autofill-design`（這些是 Pro 以上才有的功能）。

## 常見問題排除

| 症狀 | 原因 | 解法 |
| --- | --- | --- |
| 授權頁出現「用戶端 ID 無效」 | 用了 `api.canva.com` 自建 app 端點，或 app 未發布 | 改用 `https://mcp.canva.com/mcp` |
| 登入後連到錯的帳號 | 瀏覽器停在另一個 Canva 帳號 | 先在 Canva 登出，改成正確帳號再 Sign in |
| 教育帳號被拒絕 | 學校管理員關閉了第三方整合／AI Connector | 請管理員到 **Admin Dashboard → Controls and Permissions → Third-party integrations** 開啟 |
| `EADDRINUSE`（授權埠被佔用） | 前一次失敗的授權留下監聽程序 | `opencode service restart` |
| 改了設定但沒生效 | 服務沒重讀設定 | `opencode service restart` |
| 想換帳號 | 舊憑證還在 | `opencode mcp logout canva-edu`，再重新 Sign in |

## 重要原則

- **OAuth 憑證存在本機，不會跟著設定檔移動** → **每台電腦都要各自 `/mcps` 登入一次**
- 同一個 Canva 帳號可以**同時授權多台電腦**，不會互相踢掉
- **設定檔裡不應該出現任何 `client_secret`**；公開端點不需要它
- 如果曾經把 `client_secret` 寫進設定檔或外流過，記得去 <https://www.canva.com/developers/apps> 刪除或輪替那個 app

## 移到另一台電腦

因為設定檔不含任何祕密，可以直接：

1. 在新電腦跑 `opencode mcp add canva-edu --global --url https://mcp.canva.com/mcp`
2. 或整份複製 `opencode.json`（如果該專案要用的話）
3. **然後在新電腦執行一次 `/mcps` → Sign in**（這步無法省略）

## 各方案功能與額度對照

| 項目 | 免費版 | 教育版／Pro 以上 |
| --- | --- | --- |
| 設計生成、編輯、搜尋、匯出、留言、上傳素材 | ✅ | ✅ |
| 品牌工具組、品牌範本、Autofill、Resize | ❌ | ✅ |
| 標準 AI（文字類） | 扣共用額度 | 不計次 |
| 進階 AI（生成設計、生圖） | 20 次/月（與標準 AI 共用） | 200 次/月 |

> 額度每月 1 號（UTC 00:00，台灣時間 08:00）重設。
