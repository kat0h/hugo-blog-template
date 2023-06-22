---
title: "002 - 開発環境の構築(Windows版)"
date: 2023-05-17
categories: ["はじめに"]
menu: main
---

---

## 今回の内容
本チャレンジでは、Choreonoidというシミュレータを使用して開発作業を行います。

人型ロボットの基本的な機能を備えたvnoidというサンプルライブラリを
Choreonoidにインストールすることで、簡単なサンプルモーションのテストができます。

今回は開発環境としてWindowsを想定して、  
インストールからサンプルモーションのテストまでを解説しようと思います。

---

## 開発環境の構築手順
### Choreonoidのインストール

[Choreonoidの公式マニュアル](https://choreonoid.org/ja/documents/latest/install/build-windows.html#id35)
に詳細が記載されております。

「準備」、「ソースコードの取得」、「Choreonoidのビルド」の三章を順に読むことでインストールが可能です。
インストールには数時間かかる場合があります。

これらの章について、重要な補足事項を以下に記載しております。  
こちらを読みながら、公式マニュアルに則ってインストールするとスムーズかと思います。

-	[準備](https://choreonoid.org/ja/documents/latest/install/build-windows.html#id2)

	Choreonoidをインストールする事前の準備物として、  
	boostというc++の便利なライブラリ集があります。

	boostのインストール先は、  
	`C:/local/boost_1_xx_0`  
	となるよう、ご自身で設定してください。

	boostに限らず、今後必要となるライブラリに関しては、  
	`C:/local`フォルダにインストールするようにしましょう。

	また、こうしたライブラリは異なるバージョンを混在させず、  
	必ず最新バージョンを一つだけインストールするようにしましょう。

-	[ソースコードの取得](https://choreonoid.org/ja/documents/latest/install/build-windows.html#id8)

	Choreonoidのソースコードは必ず、gitリポジトリから開発版を取得してください。

	Choreonoidリポジトリのクローン先は、  
	できるだけ簡単なディレクトリパスにすることを推奨します。  
	(例)　`C:/choreonoid`, `C:/devel/choreonoid`  
	こうすることで、開発におけるディレクトリ移動が楽になります。

-	[Choreonoidのビルド](https://choreonoid.org/ja/documents/latest/install/build-windows.html#id13)

	Choreonoidのビルドは、  
	[CMakeとVisual Studio の GUI を用いる方法](https://choreonoid.org/ja/documents/latest/install/build-windows-gui.html)
	が簡単です。  
	こちらの方法でビルドすることを推奨します。

	Configureを実行して自動的にライブラリが検出されない場合は、  
	次のように設定してみてください。  
	①エントリの追加ボタンを押します。  
	{{<figure src="./add_entry.png" class="center" alt="エントリの追加" width="75%">}}  
	②ライブラリが格納されている大元のフォルダパス(prefix_path)をエントリに追加する。  
	{{<figure src="./cmake_prefix_path.png" class="center" alt="ライブラリのプリフィクス設定" width="75%">}}  
	以上の設定により、Configure時にライブラリが自動検出されるようになります。

	また、Choreonoidのインストール先には、`C:/local`を推奨します。  
	①先ほどの手順のようにエントリの追加ボタンを押します。  
	②インストール先を指定します。  
	{{<figure src="./cmake_install_prefix.png" class="center" alt="ライブラリのプリフィクス設定" width="75%">}} 

	以上の設定をしたのちに、  
	Configure、Generateすることで、ビルドの準備が整います。

	また、CMakeウィンドウのOpen Projectボタンをクリックすると、  
	`Choreonoid/build/Choreonoid.sln`というソリューションファイルが開きます。  
	{{<figure src="./open_sln.png" class="center" alt="ライブラリのプリフィクス設定" width="75%">}}

-	VisualStudioからChoreonoidを起動する

	Choreonoidのインストールまでの手順が終わりましたら、  
	いよいよChoreonoidを起動します。
	
	VisualStudioウィンドウのソリューションエクスプローラーに、  
	「Application」があると思います。  
	Applicationを選択した状態で右クリックし、「プロパティ」をクリックしてください。  
	プロパティウィンドウのデバッグというタブを開き、  
	「コマンド」と、「作業ディレクトリ」を以下の画像のように設定してください。  
	{{<figure src="./app_property.png" class="center" alt="ライブラリのプリフィクス設定" width="75%">}}  
	こうすることで、Applicationの実行を介して、  
	インストールしたchoreonoid.exeを起動できるようになります。

	次に、再度Applicationを選択した状態で右クリックし、  
	「スタートアッププロジェクトに設定」を選択してください。  
	このようにすることで、VisualStudio画面上部にある  
	「ローカルWindowsデバッガー」をクリックするだけで  
	Choreonoidを起動できるようになります。  
	{{<figure src="./local_debug.jpg" class="center" alt="ライブラリのプリフィクス設定" width="75%">}}
	

### vnoidのインストール
Choreonoidがインストールできましたら、vnoidライブラリをインストールします。

Choreonoidのローカルリポジトリに`choreonoid/ext`ディレクトリがあります。

`choreonoid/ext`ディレクトリに移動してから、  
```
git clone https://github.com/ytazz/vnoid
```  
を実行すると、`choreonoid/ext/vnoid`というフォルダ構造になります。

この状態でCMakeでConfigureとGenerateを実行し、  
Visual StudioでBuildとinstallを実行すると、  
Choreonoidにサンプルライブラリの機能が追加されます。

以下画像のように、  
「vnoid」から始まるソリューション内にサンプルコードが入っております。  
{{<figure src="./sample_code.png" class="center" alt="ライブラリのプリフィクス設定" width="75%">}}

---

## サンプルモーションのテスト
Choreonoidおよび、vnoidのインストールお疲れ様でした。  
いよいよサンプルモーションをテストしていきます。

まず、Choreonoidを起動します。  
画面上部の「ファイル」タブをクリックし、「プロジェクトを開く」を選択します。  
新たにウィンドウが開きますので、「share」、「project」の順で選択していきます。  
すると、プロジェクトの候補が多数出てくると思います。  
横にスクロールしていくと  
`vnoid_sample_project_2022_athletics.cnoid`があると思いますので、  
そちらを開きましょう。  
{{<figure src="./athletics_cnoid.png" class="center" alt="ライブラリのプリフィクス設定" width="75%">}}  
下記のような画面が表示されると思います。  
{{<figure src="./sample_start.png" class="center" alt="ライブラリのプリフィクス設定" width="75%">}}  
赤丸で印したボタンをクリックすることで、シミュレーションが開始します。  
{{<figure src="./sample_movie.gif" class="center" alt="ライブラリのプリフィクス設定" width="75%">}}

---

## まとめ・次回予告
今回はHVACのWindows版の開発環境構築手順について解説しました。

次回：環境構築(ubuntu版)