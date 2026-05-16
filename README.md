# Event-Reservation-System

イベント予約＆リマインド管理API。API設計・AWSサービス連携・AWS SAM（IaC）の学習を目的として構築。

## 学習目的

- RESTful API設計の実践
- AWS Lambda × DynamoDB × SQS × EventBridge の連携
- AWS SAMによるInfrastructure as Code

## アーキテクチャ

```
API Gateway → Lambda → DynamoDB
                  └→ SQS → Lambda(メール送信) → SES
EventBridge(Cron) → Lambda(リマインド) → DynamoDB(GSI)
```

## 開発ステップ

| Step | 内容 | 学習ポイント |
|---|---|---|
| 1 | CRUD基礎（API Gateway + Lambda + DynamoDB） | SAMの基本、AWS SDK、パスパラメータ |
| 2 | 非同期処理（SQS + メール送信Lambda） | 疎結合設計、SQSトリガー |
| 3 | スケジュール実行（EventBridge Cron + GSI） | バッチ処理、DynamoDB GSI設計 |

## 主要APIエンドポイント

```
POST   /events                          # イベント登録
GET    /events                          # イベント一覧
POST   /events/{eventId}/reservations  # 予約
GET    /reservations/{reservationId}   # 予約詳細
DELETE /reservations/{reservationId}   # 予約キャンセル
```

## ローカル開発

```bash
sam local start-api     # ローカルAPIサーバー起動
sam local invoke        # Lambda単体実行
sam deploy              # AWSにデプロイ
```

## ノート

プロジェクト設計ノートは `obsidian/projects/Event-Reservation-system/` を参照。
