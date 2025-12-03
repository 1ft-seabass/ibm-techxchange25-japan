# 仕組み

## 現在のシステム（ローカル）

![alt text](images/01-how-it-works/01-how-it-works.jpg)

全体概要です。

![alt text](images/01-how-it-works/01-how-it-works-2.jpg)

Meta Quest 3 は優れたノイズキャンセリング機能を備えています。そのため、クリアな音声データを取得できます。音声データは Whisper API に送信されます。

録音された音声は公開されている Whisper API（文字起こし API）に送信されます。Whisper API は音声をテキストに変換して返します。

![alt text](images/01-how-it-works/01-how-it-works-3.jpg)

AI 処理ステップに移ります。

- Node-RED
  - 「ライトをつけて」というメッセージで Ollama API を呼び出します。
  - MCP ツールリストを含む構造化出力 JSON スキーマを使用します。
- Ollama + Granite LLM
  - 「ライトをつけて」というメッセージを MCP ツールの選択に接続します。
  - Granite LLM は OpenAI の function calling JSON スキーマアクセスのような構造化出力を理解できます。

![alt text](images/01-how-it-works/01-how-it-works-4.jpg)

IoT 制御ステップに移ります。

- Node-RED
  - Node-RED がシンプルな MCP クライアントを呼び出します。
- シンプル MCP クライアント
  - IoT MCP 制御サーバーを実行します。
  - IoT MCP 制御サーバーが "true" のデータ状態で IoT ライトデバイスを呼び出します。
- IoT ライトデバイス
  - LED 点灯！


## 以前の構成：IBM Code Engine（API 部分）と watsonx.ai（AI 部分）

![alt text](images/01-how-it-works/01-how-it-works-1.jpg)

全体概要です。