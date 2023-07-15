# Isucon12-Qualify 挑戦

## 2023/07/15

とりあえず動かしてみたい

参考にした資料: https://blog.magnolia.tech/entry/2022/11/06/002938

isucon/isucon12-qualify を YutaUra に fork した

```bash
gh repo clone YutaUra/isucon12-qualify
```

### Build する

```bash
docker-compose up
```

なんか build できない

```
#0 22.49
#0 22.57 E: Package 'mysql-client' has no installation candidate
------
failed to solve: process "/bin/sh -c apt-get update &&   apt-get -y upgrade &&   apt-get install -y wget gcc g++ make sqlite3 &&   wget -q https://dev.mysql.com/get/mysql-apt-config_0.8.22-1_all.deb &&   apt-get -y install ./mysql-apt-config_*_all.deb &&   apt-get -y update &&   apt-get -y install mysql-client" did not complete successfully: exit code: 100
```

mysql-client を mariadb-client に変更したら起動することができた

### 初期データを展開する

以下のコマンドを実行すると initial_data ディレクトリの中に色々作られる

```
cd initial_data
curl -LO https://github.com/isucon/isucon12-qualify/releases/download/data%2F20220712_1505-745a3fdfb5783afc048ecaebd054acd20151872d/initial_data.tar.gz
tar xvf initial_data.tar.gz
rm initial_data.tar.gz
```

### データベースを準備する?

```
cd data
make
make build-for-docker-compose
```

### ベンチマークを実行する

```
cd bench
make
```

bench が全然動かないんだけど

参考にする
https://isucon.net/archives/53805209.html

```
cd initial_data
make
```

画像データの展開

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
