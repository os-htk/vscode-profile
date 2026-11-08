# vscode-profile

AWS・Python・TypeScript を書くための VS Code プロファイル。Windows で使う前提で、1 つのプロファイルに絞り、拡張機能は最小限にしている。

## 入れ方

1. VS Code でコマンドパレットから「プロファイル: プロファイルの作成」を選び、空のプロファイルを `Work` という名前で作る。
2. PowerShell で拡張機能を入れる。`code` が見つからないときは、VS Code のインストール時に「PATH への追加」を有効にしたか確かめる。

```powershell
code --profile "Work" --install-extension ms-ceintl.vscode-language-pack-ja
code --profile "Work" --install-extension amazonwebservices.aws-toolkit-vscode
code --profile "Work" --install-extension ms-python.python
code --profile "Work" --install-extension charliermarsh.ruff
code --profile "Work" --install-extension redhat.vscode-yaml
code --profile "Work" --install-extension tamasfe.even-better-toml
code --profile "Work" --install-extension catppuccin.catppuccin-vsc
code --profile "Work" --install-extension catppuccin.catppuccin-vsc-icons
```

3. `Work` プロファイルを開いた状態でコマンドパレットから「基本設定: ユーザー設定を開く (JSON)」を選び、`settings.json` の中身を貼り付ける。

## 拡張機能

| ID | 用途 |
| --- | --- |
| `ms-ceintl.vscode-language-pack-ja` | 日本語 UI |
| `amazonwebservices.aws-toolkit-vscode` | AWS のリソース操作、Lambda・SAM のデバッグ |
| `ms-python.python` | Python 本体。Pylance・debugpy・Python Environments も一緒に入る |
| `charliermarsh.ruff` | Python のフォーマットと lint |
| `redhat.vscode-yaml` | YAML。CloudFormation の短縮記法を `yaml.customTags` で通す |
| `tamasfe.even-better-toml` | `pyproject.toml` など |
| `catppuccin.catppuccin-vsc`, `catppuccin.catppuccin-vsc-icons` | テーマとアイコン |

TypeScript は VS Code 組み込みの機能で書く。

## Windows で一度だけやること

### Python

Windows の設定の「アプリ > アプリの詳細設定 > アプリ実行エイリアス」で、`python.exe` と `python3.exe` をオフにする。オンのままだと、Python を入れていても Microsoft Store が開く。

### AWS

AWS Toolkit は AWS CLI と同じ `%USERPROFILE%\.aws` の設定を読む。AWS CLI v2 を入れ、SSO を使う場合は `aws configure sso` でプロファイルを作る。認証情報はこのリポジトリに置かない。

### 社内プロキシがある場合

VS Code の拡張機能のダウンロードが通らないときは、settings.json に `"http.proxy"` を足す。npm や pip が社内の証明書で失敗するときは、証明書ファイルのパスを環境変数 `NODE_EXTRA_CA_CERTS` と `REQUESTS_CA_BUNDLE` に入れる。

## Kiro CLI

v3 を入れてある前提のメモ。プロジェクトのフォルダで `kiro-cli` を実行して使う。ログイン中のアカウントは `kiro-cli whoami` で、入っている版は `kiro-cli --version` で確かめられる。

- `/guide` で使い方を聞ける。`Shift+Tab` で元のエージェントに戻る
- `/quit` で終了する
- 設定は `%USERPROFILE%\.kiro` に置かれる。MCP サーバーは `settings\mcp.json`、常に読ませたい前提は `steering\` に Markdown で書く。プロジェクトだけに効かせたいときは、リポジトリ直下の `.kiro\` に同じ構成で置く
- 調子が悪いときは `kiro-cli diagnostic` を実行し、ログは `%TEMP%\kiro-log\logs\kiro-chat.log` を見る。v3 では `doctor` はなくなっている
