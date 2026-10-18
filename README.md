# Playlist MV Player

Amazon Music のプレイリストの曲を、YouTube のミュージックビデオで順番に再生する単一 HTML アプリです。

## 使い方

1. `index.html` をブラウザで開く（または `python3 -m http.server` などでローカル配信）
2. **プレイリストを取得**
   - **テキスト貼り付け**（推奨）: 「曲名 - アーティスト」を1行1曲で貼り付け。Amazon Music Web 版の曲一覧をコピーしたテキストもそのまま解析を試みます
   - **Amazon Music API**: クローズドベータの Amazon Music Web API を使える場合のみ。アクセストークンと x-api-key が必要
3. **YouTube Data API v3 キー**を入力
4. 「▶ MVを検索して再生」で自動再生。曲が終わると次の曲へ進みます

## 仕様

- 各曲を「アーティスト 曲名 official music video」で検索し、埋め込み可能な上位 5 件を候補にします
- 埋め込み不可などで再生できない場合は次の候補 → それでもダメなら次の曲へスキップ
- 次の曲を先読み検索、検索結果は localStorage にキャッシュ（API クォータ節約）
- シャッフル / ループ、キューのクリックで任意の曲へジャンプ

## 制約

- Amazon Music には一般公開の API がないため、API 連携は承認済み開発者のみ利用可能です
- YouTube Data API の無料枠は 1 日 10,000 ユニット（検索 1 回 100 ユニット ≒ 約 100 曲/日）
