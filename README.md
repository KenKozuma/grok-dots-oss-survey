# Grok Bot / OpenAI Dots 型 OSS の調査レポート

調査日: 2026-11-07

## 1. 概要

「Grok Bot」「OpenAI Dots」「Claude Duet」型の常駐パーソナルAIエージェント（自分のコンピュータを持つ AI 同僚）を OSS で再実装する動きが 2026 年 8〜10 月に急増し、明らかにトレンドになっている。本レポートでは、関連 OSS リポジトリをスター数順に並べ、実用フェーズ入りのもの、3 強の特徴とユーザーコメント、主な批判と解決状況、クローズド製品のサブスク要件をまとめる。

## 2. OSS リポジトリ ランキング（スター数順、2026-11-07 時点）

| # | リポジトリ | ★ | 概要 |
|---|---|---|---|
| 1 | milind-soni/OpenMausBot | 15,501 | Grok Bot / Dots / Muse の OSS 代替。各 bot が独自の PC・記憶・アプリ連携を持つ |
| 2 | elie222/rakazo | 7,343 | 「自分が所有する AI チームメイト」。BYO モデル＆コンピュータ |
| 3 | Anil-matcha/open-duet | 6,847 | 名前付き AI 同僚・隔離コンピュータ・承認フロー |
| 4 | CopilotKit/OpenDots | 6,450 | 常駐 AI 同僚テンプレート（テキスト/通話/Slack 横断） |
| 5 | b-nnett/grok-bot-0.18-reconstructed | 3,555 | Grok Bot 0.18 の非公式ソース再構成 |
| 6 | modelflare-ai/AnyModelBot | 2,728 | 70+ モデル対応のローカルファースト代替 |
| 7 | najmuzzaman-mohammad/gawkbot | 1,543 | 自分のマシンで動く常駐 bot |
| 8 | amplifthq/openmeld | 1,413 | 人と AI エージェントの協調システム |
| 9 | rome-os/rome | 893 | 再帰エージェント OS |
| 10 | composio-community/open-dot | 708 | OpenAI Dots の Mac 向け OSS 版 |
| 11 | OnlyTerp/opengrok | 507 | Grok Bot で任意モデルを動かすセットアップツール |
| 12 | opencoredev/akeru-bot | 130 | 名前付き AI チームメイト |
| 13 | 5dive-ai/5dive | 108 | スマホから AI チーム操作 |
| 14 | donvito/coworker | 62 | Grok Bot 風 UI のローカルファースト coworker |
| 15 | madebywelch/guaca | 54 | エージェント workspace |
| 16 | feder-cr/invisible_dots | 44 | アンチボット回避重視の代替 |
| 17 | Anil-matcha/open-grok-bot | 17 | プロトタイプ（FastAPI+Next.js） |
| 18 | Z4YT0N/OpenGrokBot | 12 | グループチャット型 AI 社員チーム |
| 19 | satiricalguru/OpenBot / xAmirHamza77/Poka-Bot / sarthakguptadev/appubot | 6/6/5 | 初期プロトタイプ群 |

### 著者ランキング（対象リポジトリ除外・スター数順）

| # | Author | 対象外リポジトリ | 他リポジトリ合計★ |
|---|---|---|---|
| 1 | CopilotKit | OpenDots | 70,715 |
| 2 | Anil-matcha | open-duet, open-grok-bot | 53,989 |
| 3 | feder-cr | invisible_dots | 38,355 |
| 4 | composio-community | open-dot | 26,578 |
| 5 | elie222 | rakazo | 14,198 |
| 6 | b-nnett | grok-bot-0.18-reconstructed | 7,688 |
| 7 | opencoredev | akeru-bot | 3,325 |
| 8 | donvito | coworker | 2,861 |
| 9 | OnlyTerp | opengrok | 2,139 |
| 10 | milind-soni | OpenMausBot | 849 |

## 3. 実用フェーズ入りリポジトリ

基準: リリースが存在 / 直近 2 週間以内に更新 / README に alpha/prototype/early development の明記なし。

| # | リポジトリ | ★ | 最新リリース | 備考 |
|---|---|---|---|---|
| 1 | milind-soni/OpenMausBot | 15,501 | v0.1.145 | β+production、毎日更新 |
| 2 | elie222/rakazo | 7,343 | android | β+production、Web/デスクトップ/iOS/Android |
| 3 | Anil-matcha/open-duet | 6,847 | v0.8.4 | α/β 表記なし |
| 4 | najmuzzaman-mohammad/gawkbot | 1,543 | v0.240.1 | Go+Bun |
| 5 | amplifthq/openmeld | 1,413 | v0.3.263 | 頻繁リリース |
| 6 | rome-os/rome | 893 | node-v0.1.8 | production/stable |
| 7 | alexsergivan/kwant | 176 | mac-v0.7.3 | 単一バイナリ |
| 8 | opencoredev/akeru-bot | 130 | v0.2.1 | T3 Code fork |
| 9 | 5dive-ai/5dive | 108 | v0.122.0 | スマホ操作 |
| 10 | donvito/coworker | 62 | v0.7.2 | 最終更新 33 日前 |
| 11 | madebywelch/guaca | 54 | v0.2.0 | 更新継続 |
| 12 | Z4YT0N/OpenGrokBot | 12 | v0.4.0 | 最終更新 37 日前 |
| 13 | satiricalguru/OpenBot | 6 | v0.2.0 | ローカル 100% |
| 14 | sarthakguptadev/appubot | 5 | v2026.11.7 | Telegram 連携 |

除外: CopilotKit/OpenDots（alpha/early development, リリースなし）、composio-community/open-dot（リリースなし, 停滞）、feder-cr/invisible_dots（alpha）、modelflare-ai/AnyModelBot・xAmirHamza77/Poka-Bot（prototype）、b-nnett/...・OnlyTerp/opengrok（リリースなし, 古い）。

## 4. 3 強の特徴とユーザーコメント

### 4.1 milind-soni/OpenMausBot（15,501★）

**特徴**
- メッセンジャー型 UI、各 bot が実プロセス（claude/codex/grok CLI）として動作
- bot ごとに独立した個性・モデル・記憶・コンピュータ・接続アプリ
- Bring Your Own Agent（既存ログイン/サブスク利用、プロキシなし）
- ローカルファースト（127.0.0.1 harness、~/.openmausbot）
- 承認カード（シェル/ファイル編集/質問がインラインカード）
- コンピュータ（クラウド Linux / ローカル VM / ホスト操作 opt-in）
- 500+ アプリ連携（Composio OAuth）
- チャンネル（Work/Personal 等の分離）
- Jev による自動振り分け、チームインポート（BotMRR Markdown）
- ルーチン（cron + webhook）、長期記憶、スキル（/）
- クロスプラットフォーム（Web/Electron/Android）
- Apache-2.0、無料（モデル費用別）

**ユーザーコメント**
- note (zephel01): インストール簡単だが設計判断（承認・ネットワーク境界）が本質。ローカル LLM は会話のみでツール不可。
- AutoDev Community: VPS+Tailscale 運用、MCP で Threads 自動投稿、複数モデル fallback を評価。
- AI Profit Boardroom / Julian Goldie: 「最も簡単なエージェントチーム体験」。承認カードが安全性の要。粗削り（フォーマット、承認疲れ、エージェント間連携未動作、クラウドモデル使用）。
- ttqq.dev (DeepSeek/GLM 実測): インストール 6.1 秒、定时准点、Chief of Staff の派活と検証、再起動後も長期記憶が有効。Chief の重複派单・報告不一致、常時起動必須、コスト増を報告。
- Sebastian Maniak: agentgateway 経由で秘密鍵を分離できる設計を評価。
- Android アプリ: Ronak Designs ★5「実際に仕事が完了する」。
- dev.to: リソース消費、Windows 互換性、学習曲線を指摘。

### 4.2 elie222/rakazo（7,343★）

**特徴**
- 永続 bot（会話・記憶・ルーチン・履歴）
- ボイスモード（ElevenLabs/OpenAI/Cartesia/Fish Audio）
- 共有 Team Computer + 隔離 Private computer
- ブラウザ/ターミナル/ファイル/グラフィカルデスクトップ
- bot 間委任・サブエージェント
- BYO モデル（Pi 経由）
- アプリ連携（Composio/Pipedream Connect/MCP/OpenAPI）
- ランタイム（Docker/E2B/Daytona/CreateOS/Boat/ローカル）
- クロスプラットフォーム（Web/Electron/iOS/Android）
- ルーチン（cron）、承認ゲート
- セルフホスト（Docker Compose published images）
- Apache-2.0（モデル/音声/E2B 等は別費用）

**ユーザーコメント**
- rakazo.com: Grok Bot から完全移行、Qwen 3.8 private HW 運用、eBay 掘り出し物検索、Hermes よりセットアップ簡単、Claude OAuth で 1 か月問題なし。
- GitHub #1404: Greylog MCP セットアップが認証ループで「基本的に使えない」。#2153 で部分改善、richardARPANET が再試行も未接続。
- voting.dev: ★5/5「最も信頼できる永続 AI エージェント」「Markdown ルーチンを diff/version 管理」。
- MrKeyoor: ソースビルド成功だがテスト 26 失敗、実デプロイ未検証、Team bot は共有ワークスペースで隔離なし。
- FollowAgents: 63/100（Trust 13/29）、β のため本番安定性なし。
- Legit.Show: 90/100（Security 45 が最低、Privacy 100）。
- YouTube: Composio 連携で YouTube stats 取得デモ。

### 4.3 Anil-matcha/open-duet（6,847★）

**特徴**
- 名前付きエージェント/チーム、リードが委任（リードは Claude/Codex 必須）
- 記憶（notes の保存・検索・編集）
- ルーチン（cron/webhook/手動、自動承認しない）
- 自由度設定（Ask first/Accept edits/Approve for me/Plan only）
- ツール連携（Composio: GitHub/Gmail/Calendar、MCP Marketplace）
- Today view（承認・質問・ルーチン結果・失敗・期限タスク）
- タスクボード/カレンダー
- スキル/テンプレート
- 電話アプリ（ペアリング、Android のみ）
- ファイル/履歴、音声文字起こし
- エンジン（Claude Code/Codex/Gemini/Antigravity/Cursor/ACP/OpenRouter/OpenAI 互換/Ollama/LM Studio）
- 実行形態（デスクトップ/セルフホスト/ホステッド Suparagent）
- SQLite/PostgreSQL、Apache-2.0

**ユーザーコメント**
- Issue #206: ウィンドウを閉じるとバックグラウンド実行しない → OpenClaw に留まる。radicor fork が通知・保留作業フィード・再開機能を提供。
- Issue #6/#23/#25/#33/#45: セットアップエラーの報告多数。
- HotRepo: 11/4 Python daily #10、6,748★、「実験段階の stage-1 ワークスペース」。
- DevTrends: コンテキスト再説明の煩わしさから記憶・委任を評価。リードは Claude 必須、未署名インストーラを指摘。
- atheel.ai: Composio は偽サービスでテスト済みと警告。
- gitwal: 「Claude Duet が waitlist の間に OSS で無料」と紹介。
- masskx: セキュリティ問題（API トークン露出等）を再現・報告、#122 で修正。

## 5. 主な批判と解決状況

### 5.1 milind-soni/OpenMausBot
| 批判 | 状況 | 根拠 |
|---|---|---|
| エージェント間連携未動作 | 部分解決 | #4321 CLOSED（2026-11-04）、PR #1126。ただし #2973/#1883/#4537 は OPEN |
| ローカル LLM がツールを使えない | 未解決 | #4555/#1533/#1856/#4376 が OPEN、アナウンスなし |
| 承認疲れ | 部分解決・継続中 | #3264 OPEN |
| Chief of Staff の重複派单・報告不一致 | 未解決 | #4537/#2973 OPEN |
| フォーマット粗削り | 部分解決 | #1706 CLOSED、#2608/#4459 OPEN |
| Windows 互換性 | 未解決 | #4508/#4660/#4038/#4341/#3588/#1230 が OPEN |
| リソース消費・学習曲線 | 未対応 | dev.to 指摘、専用 issue なし |

### 5.2 elie222/rakazo
| 批判 | 状況 | 根拠 |
|---|---|---|
| MCP 認証ループ（#1404） | 部分解決 | #1404 CLOSED（2026-10-25）、#2153 部分改善。richardARPANET が 11/4 に再試行も未接続 |
| Team bot 隔離なし | 未解決・設計上の制約として明記 | ドキュメントに共有ワークスペースと明記。隔離機能のアナウンスなし |
| β 安定性 | 継続中 | README に "in beta"。GA アナウンスなし |
| セキュリティ懸念 | 部分解決 | #3505 修正。MFA #3227/#3299 OPEN。Legit.Show Security 45/100 |
| セットアップ複雑 | 部分的に緩和 | published images ルートで clone/Node 不要に |

### 5.3 Anil-matcha/open-duet
| 批判 | 状況 | 根拠 |
|---|---|---|
| 背景実行不可（#206） | 未解決・ロードマップ記載なし | #206 OPEN。radicor fork が回避策提供。ROADMAP に daemon 記載なし |
| 未署名インストーラ | 計画あり（P0） | ROADMAP "Keep the unsigned/experimental label until the release path is dependable" |
| Composio 未検証 | 部分的に進行中 | ROADMAP P1 で live app 検証を計画。#234 OPEN |
| リードは Claude/Codex 必須 | 未解決・制約として明記 | README/ROADMAP に明記。非 Claude リードのアナウンスなし |
| モバイルは Android のみ・プッシュなし | 計画あり（P2） | ROADMAP "Finish the phone app" で iOS/プッシュ/ストアリリースを計画 |
| Docker コンピュータが実験的 | 計画あり（P0/P2） | ROADMAP "Qualify Linux server isolation" / "Improve file and computer reach" |
| セキュリティ脆弱性（masskx） | 解決済み | #117/#118/#123/#116 CLOSED（2026-09-30） |

### 5.4 横断的な重複批判
- バックエンド常時起動が必要: 3 者すべてに共通の構造的制約
- 承認疲れ/確認ステップ不足: 3 者共通。OpenMausBot は issue ベースで改善中、Rakazo は部分修正
- ローカル/オープンモデルのツール制限: 3 者共通の課題
- Windows 互換性: OpenMausBot に集中
- 隔離・セキュリティ: Rakazo と Open Duet で顕著
- モバイル未成熟: OpenMausBot と Open Duet で重複
- 未署名/インストール摩擦: 3 者共通だが Open Duet が最も明示的に計画

## 6. クローズド製品のサブスク要件

| 製品 | 必要な契約 | 利用可能なモデル | 外部/ローカルモデル | 実行環境 |
|---|---|---|---|---|
| Grok Bot (xAI) | SuperGrok または Cursor 有料プラン | Grok のみ | 不可 | xAI クラウド |
| OpenAI Dots | ChatGPT Pro / Business Premium | GPT のみ | 不可 | OpenAI クラウド |
| Claude Duet (Anthropic) | Claude Pro / Max / Ultra（米国のみ、waitlist） | Claude Opus 5.5 固定 | 不可 | Anthropic クラウド VM |

### まとめ
- サブスクなしで使いたい → クローズド 3 製品は不可。OSS 代替を使う。
- 外部/ローカルモデルを使いたい → クローズド 3 製品は不可。OSS 代替のうち Rakazo / Open Duet / gawkbot / Coworker がローカルモデル対応。OpenMausBot は会話のみ（ツールは Claude/Codex/Grok CLI 限定）。
- 「サブスク不要 + ローカルモデル」を満たすのは OSS 側のみ。Coworker（完全ローカル推論）や Open Duet / Rakazo（Ollama 対応）が有力候補。
