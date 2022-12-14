# 概要
『Backrooms Hole ～Backroomsの穴～』は自作ゲームの開発で使っている共通システムのソースコードを公開するために、サンプル・技術デモを目的として作成された脱出ゲームです。  
探索向け・ウォーキングシミュレーター向けの機能を中心に実装している共通システムで、ホラーゲームや脱出ゲームの開発の雛形や参考になれば幸いです。  

# 注意
ゲームのソースコードは公開しますが、一般向けに全ての実装に対してマニュアルを作成したり、個別の質問に対応するのは負担が大きいすぎるので、基本的にサポートは期待しないでください。  
ゲームの実際動作とそのプログラミング箇所を見つけて、改造・コピペ・真似するつもりくらいの気持ちでご活用いただければと思います（ソースコードは自作ゲーム開発用作成したもののため、一部に未削除の使っていない処理などが残っている可能性があります）。  

マルチプレイには未対応で、モバイル端末やロースペックPCへの最適化を行っていないのでそれらの端末向けのゲームには適さない可能性があります。  

なおUnreal Engineで作成したゲームのソースコードに過ぎず、ツクール系のようなゲームを作れるゲームとは違い、このソースコードを雛形・参考にすればゲームを誰でも簡単に作れるようになるわけではありません。  
プログラミングやゲーム開発が初心者の方は、ゲームエンジン（Unreal Engine）のインストールからはじめ、その使い方なども勉強する必要はあります。  

# 初心者の方へ

はじめは自作ゲームを作るといった高い目標でなく、まずはこのゲームを改造して遊ぶといった感じでも良いと思います。  

Unreal Engineのライセンスは大雑把に説明すると1億円売上るまでは無料で、その無料の範囲内には高品質の3Dモデルやキャラクターなどが多数含まれています。  
まずはそれらをゲームマップ上に配置して遊ぶことからはじめてみてはどうでしょう。  

私がUnreal Engineをはじめた頃にこのソースコードがあったとしたら、そんなところからはじめますし、そんなことくらいからしかできませんでした。  

私自身、Unreal Engineではじめて作ったゲームは、頂上のゴールをジャンプで目指すだけの単純なものでした（ジャンプやゴールのサンプルはあったので、無料の3Dモデルを配置すれば作れそうだったゲーム）。  
まずはUnreal Engineの使い方を知り、ゲームの完成からリリースまでを経験するためと割切りました。  

# 動作環境
Unreal Engine 5.1  

Unreal Engineのバージョンが異なっている場合は正常に動作しない可能性が高くなります。  

## 追加プラグイン

標準搭載されているプラグインですが、初期設定では無効になっていることがあり、無効のままだと正常に動作しません。  

### Common UI Plugin
テキストやボタンの共通スタイルなどで使用。  

### Gameplay Abilities
現時点では主にGameplayTagをフラグとして使っているだけです。  

# 導入
1. Unreal Engineのインストール  
2. 新規プロジェクトの作成  
3. BackroomsHoleのソースコードでプロジェクトを上書き  
4. プロジェクトをUnreal Engineエディタで開く  

なおこの導入手順はGitHubにアップロードできるソースコードを各々の端末にダウンロードして、Unreal Engineのエディタ上で編集したり動作させたりパッケージ化させたりするためのものになります。  
通常のUnreal Engineでの使用方法とは異なっている可能性があります。  

## 1. Unreal Engineのインストール
Unreal Engineの公式サイトなどを参考にUnreal Engineでゲーム開発できるように環境構築を行います。  

## 2. 新規プロジェクトの作成

「BackroomsHole」というプロジェクト名で新規プロジェクトを作成します。  
異なるプロジェクト名の場合はパッケージ化（配布用のEXEファイルなどの作成）などで設定ファイルの書き換えなどが必要になる場合があるかもしれません。

ここではプロジェクトフォルダが「D:\Works\UnrealProjects\BackroomsHole」に作成されたものとして説明します。  

https://docs.unrealengine.com/5.1/ja/creating-a-new-project-in-unreal-engine/  

作成するプロジェクト設定は「Games」の「Blank」で、「Project Defaults」は次のようにします。  

*Blurprint  
*Target Platform: Desktop  
*Quality Preset: Maximum  
*Starter Content: オフ（チェックなし）  
*Raytracing: オン（チェックあり）  

作成後にそのプロジェクトをUnreal Engineのエディタで開いている場合は閉じます。  

GameInstanceやGameModeなどに依存しているため、既存のプロジェクトに追加するのは難しいです。  
ただし個々の機能（インタラクトやダイアログ、通知など）は依存性が低くなるよう独立して作るようにしているので、一部機能だけを使用することもできるとは思います。  
この場合はそれなりのプログラミング知識などが求められます。  

## 3. BackroomsHoleのソースコードでプロジェクトを上書き

プロジェクトフォルダの直下にConfigフォルダとContentフォルダとPlatformsフォルダ（Platformsフォルダのみプロジェクトの設定などによっては作成されていない場合があります）があると思いますので、ダウンロードしたソースコードの同名フォルダをドラッグ＆ドロップなどで上書き保存します。  

*D:\Works\UnrealProjects\BackroomsHole\Config  
*D:\Works\UnrealProjects\BackroomsHole\Content  
*D:\Works\UnrealProjects\BackroomsHole\Platforms  

## 4. プロジェクトをUnreal Engineエディタで開く

以上でBackrooms Holeの導入は完了です。  

ゲームを改造してオリジナルのゲームを作成しても良いですし、まずはそのままパッケージ化（配布用のexe化）しても良いでしょう。  

# プログラムの構成

共通システムの基本ファイルは「Content\LelouFW」フォルダに入っており、ファイル名が「LelouFW_」からはじまります。  

ゲーム固有のファイルは「Content\BackroomsHole」フォルダに入っており、ファイル名が「Yndrr_」からはじまります。  
基本的に基本ファイルを直接使わずに、それらのクラスを継承して使っています。  

例えばUserWidget（UI）はゲームによってレイアウトなどが大幅に異なるため、親クラスとなる基本ファイルではロジック的共通処理だけ実装しておき、子クラスとなるゲーム固有ファイルでは表示向けやゲーム固有の処理を実装することが多いと思います。  
なおゲーム固有ファイルの中には基本ファイルを継承していても全くオーバーライドを行っていないものもあります。  

機能追加や仕様変更を行うような場合以外は、基本的にゲーム固有ファイル（「Yndrr_」からはじまるファイル）のみ編集すれば良いと思います。  

## 主な機能

## レベル（マップ）

3つのレベルので構成されています。  

1. 起動画面  
2. ゲーム本編  
3. クリア画面  

### 起動画面

Content\BackroomsHole\Level\Yndrr_Level_TopMenu  

基本的にトップメニュー（Content\BackroomsHole\Blurprint\Widget\UserWidget\TopMenu\Yndrr_WBP_TopMenu）を表示するだけのレベル。  

### ゲーム本編

Content\BackroomsHole\Level\Yndrr_Level_BackroomsHole  

このレベルに他の3Dモデルを配置するなどしていけば、オリジナルのマップにゲームが変わります。  

### クリア画面

Content\BackroomsHole\Level\Yndrr_Level_Ending  

エンドロール（Content\BackroomsHole\Blurprint\Widget\UserWidget\Yndrr_WBP_Ending）を表示するだけのレベル。  

2回目以降はエンドロールをスキップできるようになるので、スキップ機能のサンプルとして活用できるかもしれません。  

## GameMode

### Yndrr_BP_GameMode

Content\BackroomsHole\Blurprint\GameMode\Yndrr_BP_GameMode  

ゲーム固有の基本となるGameModeで、起動画面とクリア画面で使っています。  

### Yndrr_BP_GameMode_Gameplay

Content\BackroomsHole\Blurprint\GameMode\Yndrr_BP_GameMode_Gameplay  

ゲーム本編で使用するGameModeで、キャラクターなどを指定しています。  

# パッケージ化

パッケージ化のターゲットとなるプラットフォームによって、Unreal Engine以外にもインストールが必要なものがあるかもしれません。  
パッケージ化のための環境構築や手順は公式サイトやその他の解説等を参考にしてください。  

こちらではWindows向けのパッケージ化しか行っていないため、他のプラットフォーム向けのパッケージ化が可能かどうかすら不明です。

初回パッケージ化時やパッケージ化設定によってはコンパイルに何時間も掛かる場合があるかもしれません。  

## プロジェクト名が「BackroomsHole」以外でのパッケージ化

プロジェクト名が「BackroomsHole」以外の場合にパッケージ化する際に、「WARNING」が表示されることを確認しています。  

Config\Tags\Backrooms.iniファイルの「+AllowedConfigFiles=BackroomsHole/Config/Tags/Backrooms.ini」の行の「BackroomsHole」を現在のプロジェクト名に書き換えれば大丈夫だと思います（WARNINGのメッセージで同様の指示があると思います）。  
