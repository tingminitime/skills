# skills

個人的 Agent Skills 集合，遵循 [Agent Skills](https://code.claude.com/docs/en/skills) 格式，可安裝到 Claude Code、Codex、Cursor、OpenCode 等支援的 agent。

## Skills 一覽

| Skill | 用途 |
| --- | --- |
| [`readable-zh-output`](./readable-zh-output/) | 提升中文輸出的可讀性，校正翻譯腔、AI 風格修辭與結構鬆散問題。適用於協作開發時輸出給使用者閱讀的中文回覆：任務計畫、執行結果說明、問題分析、方案比較與審查意見。 |

## 安裝

使用 [`npx skills`](https://github.com/vercel-labs/skills) 安裝，不需要事先全域安裝任何套件。

### 安裝全部 skills

```bash
npx skills add tingminitime/skills
```

指令會列出這個 repo 裡的所有 skill，讓你選擇要安裝哪些、要裝到哪些 agent，以及要裝在專案還是使用者目錄。

### 只安裝單一 skill

用 `-s` 指定 skill 名稱，名稱就是 `SKILL.md` 的 `name` 欄位：

```bash
npx skills add tingminitime/skills -s readable-zh-output
```

也可以直接給 skill 目錄的 GitHub 網址：

```bash
npx skills add https://github.com/tingminitime/skills/tree/main/readable-zh-output
```

### 先看有哪些 skill 再決定

```bash
npx skills add tingminitime/skills --list
```

### 指定安裝範圍與目標 agent

預設安裝到目前專案，`-g` 改成安裝到使用者目錄，讓所有專案都能使用。`-a` 指定要安裝到哪些 agent，`-y` 跳過確認提示。

```bash
# 安裝到使用者目錄，只給 Claude Code 使用，全程不詢問
npx skills add tingminitime/skills -s readable-zh-output -g -a claude-code -y

# 同時安裝到多個 agent
npx skills add tingminitime/skills -a claude-code -a codex
```

以 Claude Code 為例，安裝後的位置：

| 範圍 | 路徑 |
| --- | --- |
| 專案（預設） | `./.claude/skills/` |
| 全域（`-g`） | `~/.claude/skills/` |

CLI 預設用 symlink 連結檔案，加上 `--copy` 改成複製一份。

## 管理已安裝的 skills

```bash
npx skills list              # 列出已安裝的 skill
npx skills update            # 更新到最新版本
npx skills remove readable-zh-output   # 移除
```

也可以不安裝、只在單次對話中載入某個 skill：

```bash
npx skills use tingminitime/skills@readable-zh-output | claude
```

## 目錄結構

```
skills/
└── readable-zh-output/
    ├── SKILL.md              # 觸發條件與核心規則
    └── references/
        ├── patterns.md       # 禁用句型、強度詞與對比句型的正反例
        ├── translationese.md # 翻譯腔的四類判準、例子與輸出前驗證步驟
        └── typography.md     # 空格、標點、backtick 與大小寫細則
```

每個 skill 目錄的 `SKILL.md` 需要 YAML frontmatter，至少包含 `name`（小寫、可含連字號）與 `description`（說明用途與觸發時機，agent 靠這段文字判斷何時載入這個 skill）。
