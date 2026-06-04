# discordbot-timer

日本語の短時間タイマーを作成する単機能 Discord Bot です。

## 機能

- `10秒` のように投稿すると、指定秒数の経過後に通知します。
- `3分` のように投稿すると、指定分数の経過後に通知します。
- `10秒!` / `3分!` のように `!` または `！` を付けると、終了前のカウントダウン通知も送ります。
- 10分を超えるタイマーは受け付けません。

## 環境変数

| 変数 | 必須 | 説明 |
| --- | --- | --- |
| `DISCORD_BOT_TOKEN` | はい | Discord Bot token |
| `OPS_LOG_HUB_URL` | いいえ | ops-log-hub 送信先 |
| `OPS_LOG_HUB_KEY` | いいえ | ops-log-hub 送信用 key |
| `OPS_LOG_PROJECT` | いいえ | ops-log project 名。既定値: `discordbot-timer` |
| `OPS_LOG_ENVIRONMENT` | いいえ | `production` / `development` など |

## 運用ログ

`OPS_LOG_HUB_URL` と `OPS_LOG_HUB_KEY` が設定されている場合のみ、以下のイベントを ops-log-hub に送信します。

- `startup`: Bot 起動完了
- `config_error`: extension 読み込み / command 同期の失敗
- `command_error`: timer 処理、slash command、prefix command の失敗

ログには message content や secret 値は含めず、guild/channel/message ID など調査に必要な最小限の情報だけを入れます。

## ローカル実行

```bash
cp .env.example .env
python -m pip install -r requirements.txt
python main.py
```

Bot はメッセージ本文を読むため、Discord Developer Portal で Message Content Intent を有効にしてください。
