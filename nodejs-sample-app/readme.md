# Node.js サンプルアプリ作成 チュートリアル

- [Node.js サンプルアプリ作成 チュートリアル](#nodejs-サンプルアプリ作成-チュートリアル)
  - [概要](#概要)
  - [対象者](#対象者)
  - [手順](#手順)
    - [1. Visual Studio Code のインストール](#1-visual-studio-code-のインストール)
    - [2. Node.js のインストール](#2-nodejs-のインストール)
    - [3. 初期設定](#3-初期設定)
    - [4. express のインストール](#4-express-のインストール)
    - [5. app.js を作成](#5-appjs-を作成)
    - [6. アプリを起動](#6-アプリを起動)

## 概要

本チュートリアルは、Node.js を使って Web アプリを作成するものです。
localhost でアプリを立ち上げ、ブラウザで Hello world と表示されることを目標とします。

## 対象者

以下のような方を対象としています。

- 初めてアプリケーションを作成する
- Node.js でのアプリの作り方を知りたい

## 手順

### 1. Visual Studio Code のインストール

Visual Studio Code は Microsoft が提供している軽量なコードエディターです。
こちらの[公式サイト](https://azure.microsoft.com/ja-jp/products/visual-studio-code/)からダウンロードしてください。

### 2. Node.js のインストール

Node.js とは JavaScript を動かすための環境のことです。
こちらの[公式サイト](https://nodejs.org/ja/download/)からダウンロードしてください。

LTS(推奨版)の中から OS にあったインストーラをダウンロードしてください。
インストーラを実行し、デフォルトの設定のまま、インストールを行ってください。

画面キャプチャを確認したい方は、以下の記事等を参照してください。
[Node.js をインストールする](https://qiita.com/sefoo0104/items/0653c935ea4a4db9dc2b)

コマンドプロンプト(Windows) / ターミナル(Mac) を開き、以下コマンドを実行してください。
バージョンの値が表示されれば OK です。

```sh
$ node --version
v12.18.3
# 表示されるバージョンは個人の環境に依存しますので、同じである必要はありません
```

合わせて npm がインストールされていることを確認します。

> npm(node package manager) とは Node.js のパッケージを管理するための CLI ツールです。
> 詳細は以下の記事等を参照してください。
> [【初心者向け】NPM と package.json を概念的に理解する](https://qiita.com/righteous/items/e5448cb2e7e11ab7d477#%E3%83%91%E3%83%83%E3%82%B1%E3%83%BC%E3%82%B8)

以下コマンドを実行して、バージョンの値が表示されれば OK です。

```sh
$ npm --version
6.14.6
# 表示されるバージョンは個人の環境に依存しますので、同じである必要はありません
```

### 3. 初期設定

サンプルアプリ用ディレクトリを作成します。

```sh
# 実行するコマンド
$ mkdir my-sample-app
$ cd my-sample-app
```

npm init コマンドを使用して、アプリケーション用の package.json ファイルを作成します。  
package.json について詳しくは、以下の記事等を参照してください。
[【初心者向け】NPM と package.json を概念的に理解する](https://qiita.com/righteous/items/e5448cb2e7e11ab7d477#%E3%83%91%E3%83%83%E3%82%B1%E3%83%BC%E3%82%B8)

```sh
# 実行するコマンド
$ npm init
```

コマンド実行時、アプリケーションの名前やバージョンなど、いくつかの項目の入力が要求されますが、全てデフォルトで大丈夫です。
全ての項目で Enter(Windows) / RETURN(Mac) キーを押して設定を完了してください。
設定が完了すると以下のような表示になるかと思います。

```sh
# コマンド実行時の表示例
$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help init` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (my-sample-app)
version: (1.0.0)
description:
entry point: (index.js)
test command:
git repository:
keywords:
author:
license: (ISC)
About to write to /Users/rui/Desktop/my-sample-app/package.json:

{
  "name": "my-sample-app",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}

# そのままEnter(Windows) / RETURN(Mac) キーを押下 or "yes"を入力
Is this OK? (yes)
$
```

ls コマンドを実行してみましょう。
package.json が作成されていることが確認できます。

```sh
# コマンド実行時の表示例
$ ls
package.json
```

### 4. express のインストール

続いて express をインストールしていきます。
以下コマンドを実行してください。

```sh
# 実行するコマンド
$ npm install express --save
```

以下のような表示になれば成功です。

```sh
# コマンド実行時の表示例
＄ npm install express --save
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN my-sample-app@1.0.0 No description
npm WARN my-sample-app@1.0.0 No repository field.

+ express@4.17.1
added 50 packages from 37 contributors and audited 50 packages in 2.509s
found 0 vulnerabilities

```

再度 ls コマンドを実行してみましょう。
node_modules と package-lock.json というものが作成されていることがわかります。
これらは Node.js を使用する上で必要となるディレクトリ/ファイルです。こちらについても以下の記事等を参照してください。
[【初心者向け】NPM と package.json を概念的に理解する](https://qiita.com/righteous/items/e5448cb2e7e11ab7d477#%E3%83%91%E3%83%83%E3%82%B1%E3%83%BC%E3%82%B8)

```sh
# コマンド実行時の表示例
$ ls
node_modules		package-lock.json	package.json
```

これで準備は完了です。

### 5. app.js を作成

では、アプリを実装していきましょう。
Visual Studio Code で my-sample-app ディレクトリを開きます。
my-sample-app ディレクトリ直下に、app.js というファイルを作成します。

作成した app.js を以下のように編集します。

```js
// expressをインポートする設定
const express = require("express");
const app = express();
// ポート設定
const port = 3000;

// http://localhost:3000/ にアクセスした際に以下の処理が実行される
app.get("/", (req, res) => {
  res.send("Hello World!");
});

// localhost:3000 でアプリが起動する
app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`);
});
```

### 6. アプリを起動

アプリを起動してみましょう。
以下コマンドを実行してください。

```sh
# 実行するコマンド
$ node app.js
```

以下のように表示されていれば成功です。

```sh
# コマンド実行時の表示例
$ node app.js
Example app listening at http://localhost:3000
```

任意のブラウザ（Google Chrome / safari など）で [http://localhost:3000](http://localhost:3000) にアクセスしてください。
画面に Hello World と表示されていれば成功です。

本チュートリアルは以上です。
