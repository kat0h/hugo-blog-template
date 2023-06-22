---
title: "003 - 開発環境の構築(Ubuntu版)"
date: 2023-05-25
categories: ["はじめに"]
menu: main
---

---

## 今回の内容
本チャレンジでは、Choreonoidというシミュレータを使用して開発作業を行います。

人型ロボットの基本的な機能を備えたvnoidというサンプルライブラリを  
Choreonoidにインストールすることで、簡単なサンプルモーションのテストができます。

今回は開発環境としてUbuntuを想定して、  
インストールからサンプルモーションのテストまでを解説しようと思います。

---

## 開発環境の構築手順
### Choreonoidのインストール

[Choreonoidの公式マニュアル](https://choreonoid.org/ja/documents/latest/install/build-ubuntu.html)
に則れば、スムーズにインストールができますが、  
いくつか補足事項がございます。

一点目は、choreonoidのバージョンについてです。  
必ず、githubから開発版をインストールするようにしてください。

二点目は、開発ツールのインストールについてです。  
cmakeのインストールには、openSSLパッケージが必要です。  
まだインストールできていない方は、  
以下のコマンドを実行して事前にインストールしておきましょう。
```
wget https://www.openssl.org/source/openssl-x.x.x.tar.gz
tar xzvf openssl-x.x.x.tar.gz
cd openssl-x.x.x.tar.gz
sudo ./config
sudo make
sudo make install
```
`openssl-`の後ろの`x.x.x`はバージョンの番号です。  
2023年5月時点でのLTSの最新バージョンは3.0.8でした。  
私の環境で3.0.8のバージョンをインストールして、  
問題なく動作することを確認しております。

また、cmakeのインストール手順は、  
cmakeパッケージ内の`README.rst`ファイル内に記述されております。  
そちらをご参照の上インストールしましょう。

### vnoidのインストール
Choreonoidがインストールできましたら、vnoidライブラリをインストールします。

Choreonoidのローカルリポジトリに`choreonoid/ext`ディレクトリがあります。

`choreonoid/ext`ディレクトリに移動してから、  
`git clone https://github.com/ytazz/vnoid`  
を実行すると、`choreonoid/ext/vnoid`というフォルダ構造になります。

この状態で、ビルドディレクトリ上でCMakeを実行します。
```
cd /choreonoid/build
cmake ..
```
続いて
```
make
sudo make install
```
を実行することで、vnoidが追加されたChoreonoidのインストールができます。

vnoidのサンプルコードは`/choreonoid/ext/vnoid`の中にあり、  
これを編集することで一部の機能を拡張することができます。

---

## サンプルモーションのテスト

ターミナルで
```
choreonoid
```
と実行することで、Choreonoidが起動するかと思います。  
その後は[Windows版](https://miyatanikoki.github.io/posts/setup_windows/)と同様に進めることで、  
サンプルモーションのテストができます。

---

## まとめ・次回予告
今回はHVACの開発環境の構築手順について解説しました。

次回：vnoidライブラリの概要
