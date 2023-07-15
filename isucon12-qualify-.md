# Isucon12-Qualify 挑戦

## 2023/07/15

とりあえず動かしてみたい

参考にした資料: https://blog.magnolia.tech/entry/2022/11/06/002938

isucon/isucon12-qualify を YutaUra に fork した

```bash
gh repo clone YutaUra/isucon12-qualify
```

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

mysql-client を mariadb-client に変更した
