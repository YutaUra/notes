# Isucon12-Qualify 挑戦

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
cat 00_create_database.sql | mysql -h 127.0.0.1 -p
# パスワードは root
./init.sh
```
