# ライブデモンストレーション！

![alt text](images/02-live-demonstration/02-live-demonstration.jpg)

全体概要です。

![alt text](images/02-live-demonstration/02-live-demonstration-1.jpg)

Meta Quest 3（XR）の UI と IoT ライトデバイスです。

![alt text](images/02-live-demonstration/02-live-demonstration-5.jpg)

最初の音声録音ステップです。

![alt text](images/02-live-demonstration/02-live-demonstration-2.jpg)

ボタン A を押すと音声録音が開始されます。「ライトをつけて」と言います。

![alt text](images/02-live-demonstration/02-live-demonstration-3.jpg)

もう一度ボタン A を押すと音声録音が停止します。
録音された音声は公開されている Whisper API（文字起こし API）に送信されます。

Whisper API は音声をテキストに変換した結果「Turn on light」を返します。

![alt text](images/02-live-demonstration/02-live-demonstration-4.jpg)

AI 処理ステップに移ります。

![alt text](images/02-live-demonstration/02-live-demonstration-6.jpg)

- Node-RED
  - 「Turn on light」というメッセージで Ollama API を呼び出します。
  - MCP ツールリストを含む構造化出力 JSON スキーマを使用します。
- Ollama + Granite LLM
  - 「Turn on light」というメッセージを MCP ツールの選択に接続します。
  - Granite LLM は OpenAI の function calling JSON スキーマアクセスのような構造化出力を理解できます。

IoT 制御ステップに移ります。

![alt text](images/02-live-demonstration/02-live-demonstration-7.jpg)

- Node-RED
  - Node-RED がシンプルな MCP クライアントを呼び出します。
- シンプル MCP クライアント
  - IoT MCP 制御サーバーを実行します。
  - IoT MCP 制御サーバーが "true" のデータ状態で IoT ライトデバイスを呼び出します。
- IoT ライトデバイス
  - LED 点灯！