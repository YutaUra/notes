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
    User root
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
