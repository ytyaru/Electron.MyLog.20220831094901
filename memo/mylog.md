# GitHub Pagesにpushするファイル一式の作成

　HTTPSにアップロードすることで動作するようにした。詳細は以下ソースコード参照。

* src/js/app/github/site-maker.js

　ざっくりいうと以下の通り。

* mpurse APIを使い投げモナボタンを実装する
* sql.js（WASM版）でSQLファイルmylog.dbの内容を読み取る
* 必要な各ファイルをコピーなり一部書き換えなりパス変更なりをする
* つぶやきの日付表示バグを修正した

　Node.jsでなく、ブラウザ上で動作するコードにする必要があった。基本的には以下をベースにしている。

* [つぶやきを保存するツール6][]

[つぶやきを保存するツール6]:https://monaledge.com/article/482




Electronでつぶやきサイトファイル一式を作成する

　ローカルサーバで確認したらちゃんと動作した。

<!-- more -->

# ブツ

* [リポジトリ][]

[リポジトリ]:https://github.com/ytyaru/Electron.MyLog.20220831094901

## インストール＆実行

```sh
NAME='Electron.MyLog.20220831094901'
git clone https://github.com/ytyaru/$NAME
cd $NAME
npm install
npm start
```

### 準備

<!--
1. [GitHubアカウントを作成する](https://github.com/join)
1. `repo`スコープ権限をもった[アクセストークンを作成する](https://github.com/settings/tokens)
1. [インストール＆実行](#install_run)してアプリ終了する
	1. `db/setting.json`ファイルが自動作成される
1. `db/setting.json`に以下をセットしファイル保存する
	1. `username`に任意のGitHubユーザ名
	1. `token`に`repo`スコープ権限を持ったトークン
	1. `repo`に任意リポジトリ名（`mytestrepo`等）
1. `dst/mytestrepo/.git`が存在しないことを確認する（あれば`dst`ごと削除する）
1. GitHub上に同名リモートリポジトリが存在しないことを確認する（あれば削除する）
-->

1. [インストール＆実行](#install_run)してアプリ終了する
	1. `db/setting.json`ファイルが自動作成される
1. `db/setting.json`に以下をセットしファイル保存する
	1. `address`: 自分のモナコイン用アドレス
	1. `repo`: 任意リポジトリ名（`mytestrepo`等）
1. `dst/mytestrepo/.git`が存在しないことを確認する（あれば`dst`ごと削除する）

### 実行

<!--
1. `npm start`で起動またはアプリで<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>R</kbd>キーを押す（リロードする）
1. `git init`コマンドが実行される
	* `repo/リポジトリ名`ディレクトリが作成され、その配下に`.git`ディレクトリが作成される
1. [createRepo][]実行後、以下エラーが出る（リモートリポジトリも作成されず）
-->

　ローカルサーバを起動してつぶやきを表示する。

1. `npm start`で起動またはアプリで<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>R</kbd>キーを押す（リロードする）
    * `dst/mytestrepo/server.sh`などが出力される
1. `dst/mytestrepo/server.sh`を実行する
1. ブラウザで`https://localhost/`を表示する
    1. `この接続ではプライバシーが保護されません`的な表示がされる
    1. `詳細設定`ボタンを押す
    1. `localhost にアクセスする（安全ではありません）`リンクをクリックする
    1. ページが表示される

　`db/mylog.db`というSQLite3ファイルに入っているつぶやきデータをもとにHTML化して表示している。

　`server.sh`をみればわかるが、実行には`openssl`や`python3`コマンドが必要。

# 目的・経緯

　HTTPSにアップロードすることで動作するようにしたい。そのためのコードを作成する処理を書いた。詳細は以下ソースコード参照。

* src/js/app/github/site-maker.js

　ざっくりいうと以下の通り。

* [mpurse][] APIを使い投げモナボタンを実装する
* [sql.js][]（WASM版）でSQLファイルmylog.dbの内容を読み取る
* 必要な各ファイルをコピーなり一部書き換えなりパス変更なりをする
* つぶやきの日付表示バグを修正した

　Node.jsでなく、ブラウザ上で動作するコードにする必要があった。基本的には以下をベースにしている。

* [つぶやきを保存するツール6][]

[mpurse]:https://github.com/tadajam/mpurse
[sql.js]:https://github.com/sql-js/sql.js/
[つぶやきを保存するツール6]:https://monaledge.com/article/482

# 将来の展望

　あとはこのファイルをGitHubにpushしてPagesにデプロイできれば、自分用つぶやきサイトを作れるメドが立つ。[mpurse][] APIのおかげで投げモナボタンもつけれた。

　今までの挑戦ですでにアップロードできるはずだけど、今までも裏切られてきた。どんな罠があるかわからない。すんなりいってくれたらいいけど。

