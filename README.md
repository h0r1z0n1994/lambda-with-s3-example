# lambda-with-s3-example
ハンズオン用S3の画像アップロードをトリガーにサムネイル画像を自動生成する

## バケットを作成

+ サムネイル画像の出力先バケットを作成します。ターゲットバケット名は、[姓].[名].seminar-resizeとして作成してください。

例）horizono.yoshihiro.seminar-resize


## デプロイパッケージをダウンロードする

デプロイパッケージは、Lambda 関数のコードと依存関係を含む .zip ファイルです。
今回のハンズオンではNode.jsを使用します。

+ lambda-with-s3-example.zipをダウンロードしてください。

ハンズオンでは以下のライブラリを使用します。
今回のハンズオンでは上記zipのnode_modules内にインストールしてあります。
また、実行用のコード（handler.js）はこちら側で準備しました。

++ Node.js内のAWS SDK for JavaScript（Lambdaランタイムにあるため不要）
++ gm(node.jsのGraphicsMagick)
++ 非同期ユーティリティモジュール


## Lambda関数を作成

+ Lambdaのマネジメントコンソールから「一から作成」を選択

+ 「名前」ボックスに任意の関数名を設定: 例）s3-thumbnail-horizono

+ 「既存のロール」はlambda_basic_executeを選択

+ 「関数の作成」を選択

+ 「関数コード」ペインの「コードエントリタイプ」を「.zipファイルをアップロード」に変更

+ 「関数パッケージ」から「アップロード」を選択、lambda-with-s3-example.zipをアップロードする

+ 「保存」を選択

+ 「関数コード」ペインのディレクトリ構造が以下の通りになっていることを確認

- 「Lambda関数名」ディレクトリ
-- node_modulesディレクトリ
-- handler.js
-- package.json
-- package-lock.json

+ 「ハンドラ」を「handler.handler」に修正

+ 「保存」を選択

## イベントソースを追加する（イベントを発行するようにS3を設定する）

+ Lambda関数の「Designer」のトリガーの追加から「S3」を選択

+ 追加された「S3」を選択

+ バケットに自身のバケットを設定

+ サフィックスに「.jpg」を入力する

+ 「追加」を選択する

+ 「保存」を選択

## S3にアップロードし、サムネイルの出力を確認する

+ [姓].[名].seminarバケットに.jpgオブジェクトをアップロードします。
