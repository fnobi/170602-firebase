# firebase :fire:<footer>@fnobi</footer>

## firebaseとは？

[https://firebase.google.com/](https://firebase.google.com/)

> Firebase は、優れたアプリを開発し、ユーザー層を拡大し、より大きな収益を上げるためのツールです。インフラ構築に手間取ることなくビジネスを収益化し、ユーザーにとっての利便性に集中できます。

- ??

### 特徴

- いわゆるmBaaSと呼ばれているもの
  - (mobile Backend as a Service)
  - スマホアプリと連携して使われるケースが多い
- リアルタイム処理対応のデータベース提供を軸とする
  - 特定のパスに情報を配置できる / 配置された際にイベントを受け取れる
- オフラインでの動作にも対応

## つかってみよう

### 管理画面にログイン

[https://console.firebase.google.com/](https://console.firebase.google.com/)

- アカウントはgoogleアカウントに紐付きます。いきなりfirebaseトップにアクセスしても、googleログインすればもうプロジェクトが作成できる状態。
- てきとうにプロジェクトをつくっておこう。

### install

```
# CLIツールのインストール
$ npm install -g firebase-tools

# ログイン
$ firebase login
```

- loginを打つと、ブラウザが立ち上がって認証画面になる。すごい。
- 流れはaws-cliとかと似ている

### プロジェクトをつくる

```
$ mkdir nobi-nobi-sample
$ cd nobi-nobi-sample
$ firebase init
# => かっこいいロゴが出たあといろいろ聞かれる
```

- 対話方式で、どんな機能が必要か選んだり、依存モジュール(npm)のインストールをしたり、いろいろ済ませてくれます。

### 静的サイトをローカルで動かす

```
$ firebase serve
```

以上。

### データベースをつかう

- 管理画面から「ウェブアプリにFirebaseを追加」を選択
- 出てきたコードをコピペ

![ウェブアプリに追加するぞい](/images/webapp.png)

### 変更を検知: <span>リアルタイム</span>

```
var db = firebase.database();
var myChatAll = db.ref('/public/chat');

function changeData () {
  var text = document.getElementById('my_text').value;
  myChatAll.set({ title: 'example', text: text });
}

myChatAll.on('value', function(snapshot) {
  document.getElementById('chatText').innerText = snapshot.val().text;
});
```

## firebase functions

データベースに書き込みがあったときなどにフックして、サーバー側で行う処理を書くことができる！
  
```
# もちゃもちゃとjsを書く
$ vi functions/index.js

# デプロイ！（functions部分だけ）
$ firebase deploy --only functions
```

### 実装例

```
// データベースの更新にフックする処理
exports.dbHook = functions.database.ref('/public/chat').onWrite((event) => {
    const val = event.data.val();
    const text = val.text;
    return event.data.ref.child('doubleText').set(text + text);
});
```

```
// 特定のパスにアクセスした場合の処理
exports.httpHook = functions.https.onRequest((request, response) => {
    response.send("Hello from Firebase!");
});
```

## 疑問たち

### Q. でも、お高いんでしょう？

**A. 個人利用する分には大丈夫そう**

- [Pricing](https://firebase.google.com/pricing/?hl=ja)

### Q. API Key、めっちゃ<span>晒されてるけど</span><span>大丈夫？？？？</span>

**A. 大丈夫っちゃ大丈夫**

- セキュリティ面は、パスごとの権限設定で守るもの
- データベースへの接続自体が誰でもできちゃうことが気になるなら、hostの制限は追加できる（Map API使う時に近い）
- [FirebaseのApiKeyとAppIDはHTMLソースにコピペしてもセキュア - test.py](http://testpy.hatenablog.com/entry/2016/09/18/093000)

### Q. <span>Milkcocoa</span><span>ってやつと</span><span>どう違う？</span>

**A. かなり似てるけど、firebase functionsにあたるものが向こうにはない**

- cliが充実しているのも使いやすさの一助
- [Document | Milkcocoa](https://mlkcca.com/document/)

## まとめ

- リアルタイム処理も可能なサーバーサイドプログラムを、インフラ構築なしで実現可能
- all javascriptでいけるのでフロントエンジニアフレンドリー
- npm周り・cli周りがけっこう整備してあるので、ガッツリ開発にも対応しやすい

## おわり

## 参考資料

- [Firebaseの始め方 - Qiita](http://qiita.com/kohashi/items/43ea22f61ade45972881)
- [第1回　一歩進んだMBaas，Firebaseとは？：スマホアプリ開発を加速する，Firebaseを使ってみよう｜gihyo.jp … 技術評論社](http://gihyo.jp/dev/serial/01/firebase/0001)
- [Cloud Functions for Firebaseとは？ - Qiita](http://qiita.com/koki_cheese/items/013d4e6ab5aefc792388)
