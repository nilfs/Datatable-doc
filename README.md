# UE C++ Header Parser PoC (Node.js)

目的:
- C++ ヘッダ (.h) を解析して、struct/class のメンバ情報（型・名前・直上コメント・UPROPERTY の生情報／meta）を JSON 化する PoC。

前提:
- Node.js LTS を使用
- ネイティブモジュールのビルドが必要なため、`node-gyp` のビルドツール（Python, C++ compiler, build essentials）が必要になる場合があります。
- 本PoCは軽量PoCであり、全ての C++ 構文に対応しているわけではありません。必要に応じて libclang ベースへ移行してください。

セットアップ:
1. 依存をインストール:
   npm install

2. 解析を実行:
   node scripts/parseHeaders.js --input samples/FCPPFruitDataTableRowInfo.h --out out/sample-output.json

出力:
- 指定した out ファイルに JSON が書き出されます。サンプル出力は `out/sample-output.json` を参照してください。

注意:
- UPROPERTY マクロの中身は `upropertyRaw` に丸ごと格納し、簡易に `meta=(...)` 内の key/value をパースして `upropertyMeta` に入れます。
- コメントは変換せず生で抽出します（複数行コメントや // コメントを結合）。