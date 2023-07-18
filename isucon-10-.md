# Isucon 10 挑戦

https://github.com/matsuu/aws-isucon/tree/main/isucon10-qualify

AWS で起動してみる

せっかくなので新しく AWS アカウントを作成した

[AMI](https://ap-northeast-1.console.aws.amazon.com/ec2/home?region=ap-northeast-1#ImageDetails:imageId=ami-03bbe60df80bdccc0) からインスタンスを起動する

インスタンスタイプはとりあえず t2.micro にした

キーペアを作成し、起動

ssh config を作成し、疎通確認

```
Host isucon10
    User ubuntu
    HostName xxx.ap-northeast-1.compute.amazonaws.com
    IdentityFile ~/.ssh/Isucon10KeyPair.pem
    IdentitiesOnly yes
    UseKeychain yes
    AddKeysToAgent yes
```

```
ssh -T isucon10
```

ssh 接続する

```
ssh isucon10
```

ユーザー切り替え

```
sudo -i -u isucon
```

bench

```
cd isuumo/bench
./bench -target-url http://127.0.0.1
```

おぉ〜

```
isucon@ip-172-31-35-66:~/isuumo/bench$ ./bench -target-url http://127.0.0.1
2023/07/18 00:34:29 bench.go:78: === initialize ===
2023/07/18 00:34:48 bench.go:90: === verify ===
2023/07/18 00:34:50 bench.go:100: === validation ===
2023/07/18 00:35:50 bench.go:102: 最終的な負荷レベル: 0
{"pass":true,"score":252,"messages":[],"reason":"OK","language":"go"}
```

VSCode の Remote SSH で接続する
フォルダは /home/isucon/isuumo にする

Go じゃなくて、 Node でうごかしてみる 

```
sudo systemctl stop    isuumo.go.service
sudo systemctl disable isuumo.go.service
sudo systemctl start   isuumo.nodejs.service
sudo systemctl enable  isuumo.nodejs.service
```

もう一度 bench を実行してみる

```
cd bench
./bench -target-url http://127.0.0.1
```

あれ、失敗だ

```
2023/07/18 00:43:28 bench.go:78: === initialize ===
2023/07/18 00:43:38 bench.go:90: === verify ===
2023/07/18 00:43:40 fails.go:105: [scenario.verifyEstateNazotte] /home/isucon/isuumo/bench/scenario/verifyWithSnapshot.go:432
    message("POST /api/estate/nazotte: レスポンスが不正です")
    code(error application)
[client.(*Client).SearchEstatesNazotte] /home/isucon/isuumo/bench/client/webapp.go:367
    message("POST /api/estate/nazotte: リクエストに失敗しました")
[client.(*Client).Do] /home/isucon/isuumo/bench/client/client.go:136
    code(error timeout)
    *url.Error("Post \"http://127.0.0.1/api/estate/nazotte\": context deadline exceeded (Client.Timeout exceeded while awaiting headers)")
    *http.httpError("context deadline exceeded (Client.Timeout exceeded while awaiting headers)")
[CallStack]
    [client.(*Client).Do] /home/isucon/isuumo/bench/client/client.go:136
    [client.(*Client).SearchEstatesNazotte] /home/isucon/isuumo/bench/client/webapp.go:361
    [scenario.verifyEstateNazotte] /home/isucon/isuumo/bench/scenario/verifyWithSnapshot.go:427
    [scenario.verifyWithSnapshot.func10] /home/isucon/isuumo/bench/scenario/verifyWithSnapshot.go:638
    [runtime.goexit] /home/isucon/local/go/src/runtime/asm_amd64.s:1373
2023/07/18 00:43:43 bench.go:94: verify failed
{"pass":false,"score":0,"messages":[{"text":"POST /api/estate/nazotte: レスポンスが不正です","count":1}],"reason":"スコアが0点を下回りました","language":"nodejs"
```

ログを見てみるか

```
journalctl -u isuumo.nodejs
```