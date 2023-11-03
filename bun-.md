# Bun ビルドしてみた

https://bun.sh/docs/project/contributing の内容を参考にする

bun 自体を install する

```sh
brew tap oven-sh/bun
brew install bun
```

llvm をインストールする

```sh
brew install llvm@16
```

パスを追加する。

```sh
export PATH="$(brew --prefix llvm@16)/bin:$PATH"
```

Bun の dependency をインストールする

```sh
brew install automake ccache cmake coreutils gnu-sed go libiconv libtool ninja pkg-config rust
```

次に zig をインストールする。 zig のバージョンが低いとビルドできないので、最新のものをインストールする。

https://github.com/marler8997/zigup/releases から zigup をダウンロードして、解凍した中身をパスの通ったところに置く。

````sh
```sh

````

Bun のビルドを開始する

```sh
bun setup
```

```

```
