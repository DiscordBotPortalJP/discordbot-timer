# discordbot-timer

日本語の短時間タイマーを作成する単機能 Discord Bot です。

## 機能

- `10秒` のように投稿すると、指定秒数の経過後に通知します。
- `3分` のように投稿すると、指定分数の経過後に通知します。
- `10秒!` / `3分!` のように `!` または `！` を付けると、終了前のカウントダウン通知も送ります。
- 10分を超えるタイマーは受け付けません。

## 環境変数

| Name | Required | Description |
| --- | --- | --- |
| `DISCORD_BOT_TOKEN` | Yes | Discord Bot token |
| `OPS_LOG_HUB_URL` | No | ops-log-hub ingest endpoint |
| `OPS_LOG_HUB_KEY` | No | ops-log-hub ingest key |
| `OPS_LOG_PROJECT` | No | ops-log project name. Default: `discordbot-timer` |
| `OPS_LOG_ENVIRONMENT` | No | `production` / `development` など |

## Ops logging

`OPS_LOG_HUB_URL` と `OPS_LOG_HUB_KEY` が設定されている場合のみ、以下のイベントを ops-log-hub に送信します。

- `startup`: Bot 起動完了
- `config_error`: extension load / command sync の失敗
- `command_error`: timer 処理、slash command、prefix command の失敗

ログには message content や secret 値は含めず、guild/channel/message ID など調査に必要な最小限の情報だけを入れます。

## Local run

```bash
cp .env.example .env
python -m pip install -r requirements.txt
python main.py
```

Bot はメッセージ本文を読むため、Discord Developer Portal で Message Content Intent を有効にしてください。
