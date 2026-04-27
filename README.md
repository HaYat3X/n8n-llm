# n8n-llm

n8n + Ollama + Notion を組み合わせた RAG (Retrieval-Augmented Generation) チャットボットです。

チャットで質問すると、Notion データベースから関連ページを検索し、その内容を元に LLM が回答を生成します。

## アーキテクチャ

```
チャット入力
  └─> Ollama (キーワード抽出)
        └─> Notion DB 検索
              └─> 各ページの本文取得 (ループ)
                    └─> Ollama (回答生成)
                          └─> チャット返答
```

## 前提条件

- [Docker](https://www.docker.com/) / Docker Compose
- [Ollama](https://ollama.com/) がホストマシンで起動していること
- 使用モデル (`minimax-m2.7:cloud`) が Ollama に pull 済みであること
- Notion API キー（インテグレーション設定済み）

## セットアップ

### 1. n8n を起動する

```bash
docker compose up -d
```

ブラウザで `http://localhost:5678` にアクセスしてアカウントを作成します。

### 2. Notion クレデンシャルを設定する

n8n の Credentials メニューから Notion の API キーを登録してください。

### 3. ワークフローをインポートする

n8n の Workflows 画面から `My workflow.json` をインポートします。

### 4. ワークフローを有効化する

インポートしたワークフローを開き、右上のトグルで有効化します。

## 使い方

ワークフローを有効化すると、n8n のチャット UI (`http://localhost:5678/webhook/...`) から質問を送信できます。

## ファイル構成

```
.
├── docker-compose.yml   # n8n コンテナ定義
└── My workflow.json     # n8n ワークフロー定義
```
# n8n-llm
