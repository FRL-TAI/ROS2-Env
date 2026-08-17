# ROS2 開発環境
本リポジトリは、自律施工技術開発基盤OPERAシミュレータ（OperaSim）と連携するためのROS2-Humble 開発環境である。  
VS Codeの「Dev Containers」機能を利用し、**「環境構築（Docker）」と「ソースコード（ROS2ワークスペース）」を完全に分離して管理**する構成を採用している。


## 動作要件 (ホストOSのソフトウェア要件)
この環境を利用するために、ホストPC（手元のPC）に以下のソフトウェアがインストールされている必要がある。

- Docker Desktop または Docker Engine + Docker Compose
- Visual Studio Code (VS Code)
- VS Code拡張機能: Dev Containers
- Git


## ホスト側の想定ディレクトリ構成
本リポジトリ（`ros2-env`）と、ROS 2のソースコードを格納する複数のワークスペース群（`workspaces`）は、**並列の階層**に配置されることを想定している。

```text
任意の開発フォルダ/ (例: ~/ros2_development)
├── ros2-env/                   <-- 本リポジトリ (VS Codeで開く対象)
│   ├── .devcontainer/
│   │   ├── devcontainer.json
│   │   └── Dockerfile
│   └── README.md
└── workspaces/                 <-- 全ワークスペースをまとめるディレクトリ
    ├── ros2_ws_operasim/       <-- コードリポジトリ1
    │   └── src/
    └── ros2_ws_autonomous/     <-- コードリポジトリ2
        └── src/
```


## 実行環境の使用方法
1. 本リポジトリをVS Codeで開く
2. containerで開きなおす  
画面右下に表示される「Reopen in Container」という通知をクリックするか、コマンドパレット（Ctrl+Shift+P または Cmd+Shift+P）から Dev Containers: Reopen in Container を実行する
3. Dockerイメージのビルドが開始されコンテナ内のディレクトリがVS Codeで開きなおされる


## 新しいワークスペースを追加する方法
新しくROS 2のワークスペース（リポジトリ）を追加する場合、`devcontainer.json` や `Dockerfile` を書き換える必要は一切ない。

1. ホストPC側の workspaces/ ディレクトリ内に、新しいワークスペースのフォルダを作成（または git clone）する
2. VS Codeのコンテナを再起動（Rebuild）する  
VS Codeのコマンドパレット（Ctrl+Shift+P または Cmd+Shift+P）から Dev Containers: Rebuild Container を実行