---
name: creating-skills
description: Provides best practices and rules to follow when creating or editing Agent Skills (SKILL.md files). Use when the user asks to create, edit, improve, or review a SKILL.md file or an Agent Skill directory.
---

# Creating and Editing Agent Skills

## 必須ルール

### ディレクトリ構成

```
.github/skills/
└── <skill-name>/        # name フィールドと一致させること
    └── SKILL.md         # 必須
    └── (任意の補助ファイル)
```

個人用スキルは `~/.copilot/skills/` に配置する。

### YAML フロントマター（必須）

```yaml
---
name: skill-name          # 小文字・数字・ハイフンのみ。最大64文字。ディレクトリ名と一致
description: ...          # 何をするか＋いつ使うか を明記。最大1024文字
---
```

- `name` にXMLタグ・`anthropic`・`claude` は使用禁止
- `description` にXMLタグは使用禁止
- `description` は **第三者視点**で書く（例: "Processes Excel files" ✅ / "I can help you" ❌）

---

## ネーミング規則

- 動名詞形（gerund）推奨: `creating-skills`, `processing-pdfs`, `managing-databases`
- 名詞句も可: `pdf-processing`, `spreadsheet-analysis`
- 避けるべき: `helper`, `utils`, `tools`, `documents`（曖昧すぎる）

---

## description の書き方

**良い例:**
```
Processes Excel spreadsheets, creates pivot tables, generates charts.
Use when analyzing Excel files, spreadsheets, tabular data, or .xlsx files.
```

**悪い例:**
```
Helps with documents
Does stuff with files
I can help you process Excel files
```

**ポイント:** Copilot は description でスキルを選択する。何をするか＋いつ使うかの両方を含める。

---

## SKILL.md 本文のルール

1. **簡潔に書く** — Claudeがすでに知っていることは書かない。1トークンも無駄にしない
2. **500行以内** に収める。超える場合は別ファイルに分割してプログレッシブ開示を使う
3. **参照は1階層まで** — SKILL.md → 参照ファイル。さらに深いネストは避ける
4. **時間依存情報を書かない** — "2025年8月以降は..." のような記述は禁止。レガシー情報は `<details>` タグで折りたたむ
5. **用語を統一する** — 同じ概念に複数の言葉を使わない
6. **パスはスラッシュのみ** — `scripts/helper.py` ✅ / `scripts\helper.py` ❌

---

## プログレッシブ開示パターン

大きなスキルは補助ファイルを使い、必要なときだけ読み込む:

```
skill-name/
├── SKILL.md          # 概要と参照リンク（500行以内）
├── advanced.md       # 高度な機能（必要时に読む）
├── reference.md      # APIリファレンス（必要時に読む）
└── scripts/
    └── helper.py     # 実行スクリプト
```

SKILL.md に参照を記載する例:
```markdown
**基本的な使い方**: [以下に記述]
**高度な機能**: [advanced.md](advanced.md) を参照
**APIリファレンス**: [reference.md](reference.md) を参照
```

---

## 自由度の設定

| 状況 | 自由度 | 書き方 |
|------|--------|--------|
| 複数のアプローチが有効 | 高 | テキスト指示のみ |
| 好ましいパターンがある | 中 | テンプレート＋パラメータ |
| 順序が重要・壊れやすい | 低 | 厳密なコマンド・手順 |

---

## ワークフローとフィードバックループ

複雑なタスクにはチェックリスト形式のワークフローを使う:

```markdown
## タスク進捗

- [ ] Step 1: ...
- [ ] Step 2: ...
- [ ] Step 3: ...
```

品質チェックが必要なタスクにはフィードバックループを実装する:
1. 実行
2. バリデーション
3. エラーがあれば修正して 2 へ戻る
4. 合格したら次のステップへ

---

## 避けるべきアンチパターン

- ❌ 多すぎる選択肢の提示（デフォルトを1つ提示し、代替案を添える）
- ❌ Windowsスタイルのパス（バックスラッシュ）
- ❌ 深いネスト参照（SKILL.md → A.md → B.md → ...）
- ❌ 長い参照ファイルにTOCなし（100行超は目次を付ける）
- ❌ 根拠のないマジックナンバー（コメントで理由を説明する）

---

## スキル作成のチェックリスト

### コア品質
- [ ] `description` が具体的で、何をするか＋いつ使うかを含む
- [ ] SKILL.md 本文が500行以内
- [ ] 時間依存情報なし
- [ ] 用語が統一されている
- [ ] ファイル参照が1階層のみ

### 構造
- [ ] ディレクトリ名が `name` フィールドと一致
- [ ] パスはすべてスラッシュ
- [ ] 100行超の参照ファイルに目次がある

### テスト
- [ ] 実際のユースケースでテスト済み
- [ ] スキルが期待通りに自動トリガーされる

---

## フロントマターの任意フィールド

| フィールド | 説明 |
|-----------|------|
| `argument-hint` | スラッシュコマンド使用時のヒントテキスト |
| `user-invokable: false` | `/` メニューに表示しない（自動トリガーのみ） |
| `disable-model-invocation: true` | 自動トリガーを無効化（手動のみ） |
