# OpenCode Skills（教學用）

給老師們共用的 [OpenCode](https://opencode.ai) skills 集合。

## 內含 skills

| Skill | 用途 |
| --- | --- |
| [`canva-mcp`](canva-mcp/SKILL.md) | 把 OpenCode 連到 Canva（含 **Canva 教育版**）MCP |

---

## ⚡ 一鍵安裝（最快）

把下面這段直接複製給 OpenCode：

```text
幫我安裝這個 skill：
https://github.com/wkl0830-glitch/opencode-skills
```

OpenCode 會自己讀這份說明，並把訂閱網址寫進設定檔。

> ⚠️ **改完設定要重開 OpenCode** 才會生效。

裝好後，跟 OpenCode 說「**幫我接上 Canva**」就會開始引導登入。

---

## 📨 分享給同事（直接轉傳）

把下面整段複製，貼到 LINE 或群組即可：

```text
【OpenCode × Canva 連線技能】

1. 安裝 OpenCode V2：https://opencode.ai

2. 打開設定檔（Windows：C:\Users\你的帳號\.config\opencode\opencode.json）

3. 加上這一行：
   "skills": ["https://raw.githubusercontent.com/wkl0830-glitch/opencode-skills/main/"]

   整份長這樣：
   {
     "skills": ["https://raw.githubusercontent.com/wkl0830-glitch/opencode-skills/main/"]
   }

4. 存檔後重開 OpenCode

5. 跟 OpenCode 說「幫我接上 Canva」，照指示登入 Canva 就完成了

詳情：https://github.com/wkl0830-glitch/opencode-skills
```

> 💡 懶得開設定檔的人，也可以直接把上面的網址貼給自己的 OpenCode，請它代勞。

### ⚠️ 兩個網址別搞混

| 網址 | 用途 |
| --- | --- |
| `https://github.com/wkl0830-glitch/opencode-skills` | 給**人**看的（讀說明） |
| `https://raw.githubusercontent.com/wkl0830-glitch/opencode-skills/main/` | 給 **OpenCode** 讀的（填進設定檔） |

把 `github.com` 的網址填進 `skills` 會失敗 —— 那是一頁網頁，不是可下載的檔案。

---

## 前置需求

- 已安裝 **OpenCode V2**
- 一個 **Canva 帳號**（教育版更好 —— 品牌工具組、Resize、Autofill 都能用，AI 額度也大得多）

---

## 安裝方式

### 方法 1：訂閱（最簡單，改動會自動同步）

在 `opencode.json` 加上 `skills` 陣列：

```jsonc
{
  "skills": ["https://raw.githubusercontent.com/wkl0830-glitch/opencode-skills/main/"]
}
```

存檔後重開 OpenCode 即生效。

### 方法 2：Clone 下來

```sh
git clone https://github.com/wkl0830-glitch/opencode-skills.git ~/opencode-skills
```

然後在 `opencode.json`：

```jsonc
{
  "skills": ["~/opencode-skills"]
}
```

### 方法 3：手動複製

把 `canva-mcp/` 整個資料夾複製到下列任一位置：

| 範圍 | 位置 |
| --- | --- |
| 全域（所有專案） | `~/.config/opencode/skills/canva-mcp/` |
| 單一專案 | `<專案資料夾>/.opencode/skills/canva-mcp/` |
| Claude Code 相容 | `~/.claude/skills/canva-mcp/` |

---

## 設定檔位置

| 系統 | 全域設定檔 |
| --- | --- |
| Windows | `C:\Users\<你>\.config\opencode\opencode.json` |
| macOS / Linux | `~/.config/opencode/opencode.json` |

---

## 怎麼用

安裝後有兩種觸發方式：

- **自動**：直接跟 OpenCode 說「幫我接上 Canva」、「Canva 連不上」→ 會自動載入
- **手動**：在對話中輸入 `@canva-mcp`

---

## 授權

歡迎自由使用與修改。若需要正式的開源授權，建議加上 MIT License。
