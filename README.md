# VS Code GitHub Copilot 汎用Agent Skills集

Skillsはエージェントに専門的な知識やワークフローを教えるための仕組み。会話の内容に応じて必要なSkillだけが自動で読み込まれる。

このリポジトリは、プロジェクト横断で使える汎用的なSkillsをまとめたもの。

## セットアップ

プロジェクトディレクトリに移動し、`.github` ディレクトリとしてクローンする。配置場所の詳細は [VS Code Agent Skills ドキュメント](https://code.visualstudio.com/docs/copilot/customization/agent-skills) を参照。

```bash
cd <プロジェクトディレクトリ>
git clone https://github.com/ozuaq/github-copilot-config.git .github
```

## Skills一覧

| Skill | 説明 |
|-------|------|
| creating-skills | [Claude公式ドキュメント](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)に則ってSkillを作成・編集する |
| interacting-with-user | ユーザーとのやりとりのルールを定義する。ユーザーが明示しない限り、回答を終了せずにやりとりを続けられる |
| explaining-commands | ターミナルコマンドを実行前に詳しく説明する |

## 使用例

- `/interacting-with-user` でエージェントとのやりとりを始める
- Skillの作成・編集を依頼すると、creating-skillsに則って作成してくれる
- エージェントがコマンドを実行するときは、実行前にそのコマンドが何をするのかを説明してくれる
