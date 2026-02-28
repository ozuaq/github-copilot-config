# VS Code GitHub Copilot 汎用Agent Skill集

## Agent Skill一覧

| Agent Skill | 説明 |
|-------------|------|
| creating-skills | [Claude公式ドキュメントのAgent Skillsのベストプラクティス](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)に則ってAgent Skillを作成・編集する |
| interacting-with-user | ユーザーとのやりとりのルールを定義する。ユーザーが明示しない限り、回答を終了せずにやりとりを続けられる |
| explaining-commands | ターミナルコマンドを実行前に詳しく説明する |

## 使用例

- `/interacting-with-user` でエージェントとのやりとりを始める
- Agent Skillの作成・編集を依頼すると、creating-skillsに則って作成してくれる
- エージェントがコマンドを実行するときは、実行前にそのコマンドが何をするのかを説明してくれる
