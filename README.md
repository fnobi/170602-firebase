# firebase :fire:<footer>@fnobi</footer>

## firebaseとは？

[https://firebase.google.com/](https://firebase.google.com/)

> Firebase は、優れたアプリを開発し、ユーザー層を拡大し、より大きな収益を上げるためのツールです。インフラ構築に手間取ることなくビジネスを収益化し、ユーザーにとっての利便性に集中できます。

- ??


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

### データベースをつかう


### 変更を検知: <span>リアルタイム</span>


## firebase functions



## 疑問たち

### Q. でも、お高いんでしょう？

**A. 個人利用する分には大丈夫そう**

### Q. API Key、めっちゃ<span>晒されてるけど</span><span>大丈夫？？？？</span>

**A. 大丈夫っちゃ大丈夫**

- セキュリティ面は、パスごとの権限設定で守るもの
- データベースへの接続自体が誰でもできちゃうことが気になるなら、hostの制限は追加できる（Map API使う時に近い）

- [FirebaseのApiKeyとAppIDはHTMLソースにコピペしてもセキュア - test.py](http://testpy.hatenablog.com/entry/2016/09/18/093000)

### Q. <span>Milkcocoa</span><span>ってやつと</span><span>どう違う？</span>

**A. かなり似てるけど、firebase functionsにあたるものが向こうにはない**

- [Document | Milkcocoa](https://mlkcca.com/document/)


## 参考資料

- [Firebaseの始め方 - Qiita](http://qiita.com/kohashi/items/43ea22f61ade45972881)
