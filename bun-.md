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

パスを追加する

```sh
export PATH="$PATH:$(brew --prefix llvm@16)/bin"
```

Bun の dependency をインストールする

```sh
brew install automake ccache cmake coreutils gnu-sed go libiconv libtool ninja pkg-config rust
```