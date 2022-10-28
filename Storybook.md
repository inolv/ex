# Node.jsの導入
ここでは楽なので nodebrew を活用する。
その前段の Homebrew から記載。

## Homebrewのインストール

[公式サイト](https://brew.sh/index_ja)よりダウンロード（Terminal.appでの設定）。  
なおHomebrewとは？は上記公式サイトを参照。

> これをmacOSのターミナルまたはLinuxのシェルプロンプトに貼り付けて下さい。

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Nodebrewのインストール

### Node.jsの存在確認

もしすでにHomebrewからNode.jsをインストールしたことがある場合は以下で削除する。

```
brew ls  // nodeが表示されたら、以下のコマンドでアンインストール
brew uninstall --force node
```

### インストール
```
brew install nodebrew
```
※結構時間がかかる。

### 確認
```
nodebrew -v
```
バージョンが表示されればOK。

### 環境変数を追加

ターミナルで以下を実行。

```
echo $SHELL
```

もし表示が /bin/zsh であれば zsh なの以降の __zshのMacを使っている場合__ まで飛ばす。（やる大枠は同じ）  
そうでない場合は以下を進める。

```
vi ~/.bash_profile
```

で、以下を追加する。

```
export PATH=$HOME/.nodebrew/current/bin:$PATH
```

※以下の順にキー操作

```
⌘ + v
esc
:wq
return
```

bash_profileを更新して設定を反映させる。

```
source ~/.bash_profile
```

__最終セットアップ__ へ。

#### zshのMacを使っている場合

ファイルを生成する

```
touch ~/.zshrc // ファイル生成
vi ~/.zshrc
```

で、以下を追加する。

```
export PATH=$HOME/.nodebrew/current/bin:$PATH
```

※以下の順にキー操作

```
⌘ + v
esc
:wq
return
```

zshrcを更新して設定を反映させる。

```
source ~/.zshrc
```

以下 __最終セットアップ__ へ。


#### 最終セットアップ

セットアップ。これやらないとインストールできない。

```
nodebrew setup
```

## Nodebrew経由でNodeのインストール

### インストール可能なバージョンを確認
```
nodebrew ls-remote
```

びゃーっと出てくる。
io@がついているのは安定していないバージョンなので `v` で始まる一番数値が大きいやつを何も気にせずコピー。


```
v18.0.0   v18.1.0   v18.2.0   v18.3.0   v18.4.0   v18.5.0   v18.6.0   v18.7.0
v18.8.0   v18.9.0   v18.9.1   v18.10.0  v18.11.0  v18.12.0  

v19.0.0   ← 執筆時はこれ

io@v1.0.0 io@v1.0.1 io@v1.0.2 io@v1.0.3 io@v1.0.4 io@v1.1.0 io@v1.2.0 io@v1.3.0
io@v1.4.1 io@v1.4.2 io@v1.4.3 io@v1.5.0 io@v1.5.1 io@v1.6.0 io@v1.6.1 io@v1.6.2
io@v1.6.3 io@v1.6.4 io@v1.7.1 io@v1.8.1 io@v1.8.2 io@v1.8.3 io@v1.8.4 

io@v2.0.0 io@v2.0.1 io@v2.0.2 io@v2.1.0 io@v2.2.0 io@v2.2.1 io@v2.3.0 io@v2.3.1
io@v2.3.2 io@v2.3.3 io@v2.3.4 io@v2.4.0 io@v2.5.0 

io@v3.0.0 io@v3.1.0 io@v3.2.0 io@v3.3.0 io@v3.3.1 
```

### Nodeのインストール

```
nodebrew install-binary <Versionをペースト>
```

### インストールしたバージョンを確認
```
nodebrew ls
```

### 使いたいバージョンを指定
```
nodebrew use <Version>
```

### 最終確認

```
node -v
```
執筆時であれば v19.0.0 が表示されればOK。

#Storybookを導入
npxってもう入ってるっけ？後で調べる。

## インストール先を設定
```
cd hogehoge（好きな場所を指定）
```

## 大元となるプロジェクトのインストール

```
npx create-react-app react-storybook
```

多分以下の様に表示されるので `y → return`

```
% npx create-react-app react-storybook
Need to install the following packages:
  create-react-app@5.0.1
Ok to proceed? (y) 
```

自動的にReactの環境を構築してくれるので暫く待つ。  
終了するとフォルダに以下の様に react-storybook が生成されているはず。

```
react-storybook
 ├ node_modules
 ├ package-lock.json
 ├ package.json
 ├ public
 ├ README.md
 └ src
```

また、コンソールに以下が表示されているはず。

```
Success! Created react-storybook at {パス}/react-storybook
Inside that directory, you can run several commands:

  npm start
    Starts the development server.

  npm run build
    Bundles the app into static files for production.

  npm test
    Starts the test runner.

  npm run eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd react-storybook
  npm start

Happy hacking!
```

最後の方にある以下コマンドを入れてみる。

```
cd react-storybook
npm start
```

以下が表示されると共にターミナルがブラウザを制御するアクセス要求が出るのでOKを押す。

```
Starting the development server...
```

ブラウザが起動しReactのプロジェクトが表示されたらターミナルに戻り control+c を押す。

## プロジェクトにStorybookをインストール

前項で以下を実行した状態で進める。

```
cd react-storybook
```

以下を実行、Storybookを初期化。

```
npx storybook init
```

多分以下の様に表示されるので y → return  
※かなりかかる。

```
% npx storybook init
Need to install the following packages:
  storybook@6.5.13
Ok to proceed? (y) 
```

使用しているnpmのバージョンが合っていないと以下が出るので y


```
? Do you want to run the 'npm7' migration on your project? › (y/N)
```

完了すると以下の様に表示されるはず。

```
✅ migration check successfully ran


To run your Storybook, type:

   npm run storybook 

For more information visit: https://storybook.js.org
```

記載の通り以下を実行

```
npm run storybook
```

Storybookがブラウザに表示されたらOK。


# 開発環境とStorybookを同時に起動する

ターミナルを ⌘ + n で新しく開き、フォルダに移動し、それぞれの起動を実行する。


# 参考にしたサイト

- NodebrewでNodeをインストールする  
[https://qiita.com/mame_daifuku/items/373daf5f49ee585ea498](https://qiita.com/mame_daifuku/items/373daf5f49ee585ea498)
