# OpenCode Skills（教學用）

給老師們共用的 [OpenCode](https://opencode.ai) skills 集合。

## 內含 skills

| Skill | 用途 |
| --- | --- |
| [`canva-mcp`](canva-mcp/SKILL.md) | 把 OpenCode 連到 Canva（含 **Canva 教育版**）MCP |

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
