# Isucon 9 挑戦

## 2023/07/15

参考にする
https://isucon.net/archives/53805209.html

```
cd initial_data
make
```

### 画像データの展開

```
cd webapp/public
curl -LO https://github.com/isucon/isucon9-qualify/releases/download/v2/initial.zip
unzip initial.zip
rm -rf upload
mv v3_initial_data upload

cd ../../initial-data/
curl -LO https://github.com/isucon/isucon9-qualify/releases/download/v2/bench1.zip
unzip bench1.zip
rm -rf images
mv v3_bench1 images

cd ..
```

### データベースの初期化

docker-compose を用いて mysql を立ち上げて、 mysql を事前にインストールしておく

```
brew install mysql
```

```
cd webapp/sql
# パスワードは root
cat 00_create_database.sql | mysql -h 127.0.0.1 -p
./init.sh
cd ../..
```

### アプリケーションの実行

node.js で起動してみる

```
cd webapp/nodejs
pnpm i
```

bcrypt のバージョンが古くて install に成功しなかったから 5.0.0 にあげて、もう一回インストール

```
pnpm i
```

起動

```
pnpm start
```

http://localhost:8000/ に起動した！

### 外部サービスを起動する

```
make
```

別のターミナルで以下のコマンドを実行する

```
./bin/payment
```

```
./bin/shipment
```

実行した。一旦終了させる

### ベンチマークを実行する

さっきの Node.js を起動されたじょうたいで以下のコマンドを実行する

なぜかデフォルトの 127.0.0.1 では失敗したので、 localhost に変更した

```
./bin/benchmarker -target-url http://localhost:8000
```

実行してもタイムアウトが発生し続けちゃって困ってたんだけど、

bench mark の方の timeout を伸ばしてあげたら解決した

```
ctx, cancel := context.WithTimeout(ctx, 120*time.Second)
```

そうするといっぱい bench mark が実行されるんだけど、タイムアウト発生しまくりで成功しない。

DB の接続がことごとく abort しちゃってる感じがするので、それが原因かも

一旦は成功せずだが、ベンチマークの実行はできた

### 古すぎるライブラリをアップデート

いろいろやっていく前に、ライブラリが古すぎるのでアップデートする

とりあえず全部最新に上げてみる

```
pnpm update --interactive --latest
```

### 計測ツール導入

ベンチマークすら成功しない状況なので、計測ツールを導入して、どこがボトルネックになっているのかを調べる

計測には OpenTelemetry を使う

```

```
