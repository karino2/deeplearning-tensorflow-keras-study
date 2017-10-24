---
title: "詳解ディープラーニング勉強会 ページ"
layout: page
---

内輪でやっている詳解ディープラーニングについての資料などを置くページです。

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="https://rcm-fe.amazon-adsystem.com/e/cm?ref=qf_sp_asin_til&t=karino203-22&m=amazon&o=9&p=8&l=as1&IS1=1&detail=1&asins=4839962510&linkId=361be02c7a24cdce29613b6a4b052489&bc1=ffffff&lt1=_top&fc1=333333&lc1=0066c0&bg1=ffffff&f=ifr">
    </iframe>

このページでは、自分が担当する第一回の環境設定について書いていきます。
あまり書籍とは関係なく、データ分析一般についてどう進めるべきかを話していきます。

# 事前準備

- githubアカウント作成
- GCPアカウン作成とチュートリアル
  - [GCE tutorial](http://cs231n.github.io/gce-tutorial/)を先頭から、 「Connect to Your Virtual Instance and Download the Assignment」のsshにつなげる所までやってくること（ダウンロードする所から先はやらなくてOK.ただJupyter Notebookとつなげる所はやっておくとついていくのは楽かも）
- 実装予定の節の周辺を読んでくる。実装予定は
   - 3.3.2
   - 3.4.3.1
   - 3.4.3.2
   - 3.5.3、3.6.3、3.7.3は、おそらく時間的にやれない気がするが、念の為軽く見ておくくらいはしていただけると幸い
- Python知らない人は後述の「Pythonの最低限の知識」くらいはやってあると望ましい（予習が間に合わなかったらサポートしますが）


## Pythonの最低限の知識

あまり専門的な知識を前提とする気はないので、関数とクラスが書けてリスト内包表記がわかるくらいの人なら、別段予習は必要ありませんが、苦手と思っている人は以下くらいをいやっておくと万全。

- [CS231nのPython Numpyチュートリアル](http://cs231n.github.io/python-numpy-tutorial/)
  - これ見るくらいで十分です。
- [Pythonチュートリアル](https://docs.python.jp/3/tutorial/index.html)
  - 上記のチュートリアルでは分からない、という人はこちらを先にやるのがオススメ。
  - CS231nのチュートリアルを見て、分からない所をこちらで調べる、という感じに使えば十分
  - CS231nの方がついていくのが辛くてこちらのPythonチュートリアルの方がやりやすい、という人は以下の感じで進める
    - 最低1から4まで
    - 出来たらさらに
      - 6
      - 9.1から9.3まで
      - 12くらいを読んでおくと万全
- [Python Cookbook](http://shop.oreilly.com/product/0636920027072.do)
  - こちらはさらに学びたい人用(事前準備というレベルでは不要です)
  - 辞書的に使う。目次に軽く目を通しておいて、調べたい事が出てきたら、調べるついでに付近を読む、という感じに使う
  - （この勉強会という枠を超えて）データ分析のPythonとしては、Pythonチュートリアルとcookbookだけで十分


# 基本コンセプト

- プログラミング初心者を想定して、自分が考えるベストのやり方を話す
  - 好きにして良い事も自分が良いと思う一つだけを話す
  - 複数選択肢がある時は自分の一番のオススメを一つだけ話す
  - 他の方法が好きな人はそれを使っても構いません
- 何故そうなのか、という事について、話すと長くなる事は説明しない
  - 初心者の人は、理由はおいといてとりあえず自分のオススメのやり方から始めてもらう
  - ある程度慣れてきたら違うやり方でやってもらって構わない
- ゼロから始められるように、全作業を自分で行う
- データ分析を個人でやる事を想定してそれ以外の話はなるべくしない
  - チーム開発は別に学んでください
  - ただし他の分析屋との協業くらいは意識した内容にはします

# 話す事

- Docker
- Notebook
- gitとgithub

# プログラミングの原則

- まず動かし、頻繁に動かす
   - Notebook
   - ユニットテスト
- YAGNI
- 3回出会ったら考える
- インタラクティブに使いやすい事
- ライフサイクルを意識した開発
- 作業をスクリプトに残す必要性
   - Jupyter Notebook
   - Dockerfile
   - gist
   - 作業メモ


# Docker入門

## Dockerとは何か？

- 軽い仮想環境（のようなもの）
- 環境の再現性
- 軽い

## プロセスとファイル

Unixは大雑把には、ファイルとプロセスを合わせた物と言える。これはDockerを知る上でも重要。

### プロセス

- init
- forkとexec

### ファイル

- rootfs
- mount pointとマウント


## イメージとwritable

- union mountによるレイヤー構造
   - append onlyと削除
   - 共有
- 最後にwritableなレイヤー
- イメージとは何か？

## コンテナ

- namespaceとcgroupによる分離
- プロセスのサブツリー

## Dockerfileとdocker build

- レイヤーを作る為のスクリプト
- 書く時の作業手順
- 何をDockerfileに書くべきか
- ハッシュとレイヤー

## dockerサーバーとdockerコマンド

- docker build
- docker run
- docker ps
- docker rmi


## 分析時のベストプラクティス

- 何をイメージにし、何をmountするべきか
- 何をホストに置くべきか
   - wget、ag、git、screen
   - gistでのセットアップ



# Jupyter Notebook入門


## Hello Notebook

まずは触ってみる。

- gcloudとポートフォワード、docker run。
- ホストでscreenを動かし、その中でdockerを動かし、その中でnotebookを動かす

## 利点

- 作業経過がスクリプトに残る
- セルによるゆるいモジュール化

## 簡単な解説

- カーネルとPythonプロセス
- セル
- SIGHUPとscreen

# データ分析の為のgit入門

## 分散ソース管理

分散で有る事の意義（はあまりデータ分析では関係ない）

## ドキュメントとしてのソース管理

- 最後に残るのはレポジトリ
  - wikiやチケットは失われる
- READMEとcommit log

## データ分析とタグ

## gitに依存した開発スタイル

## よく使うコマンド


# GCEとgcloudコマンド

- ポートフォワード
- gist
- screen

## 良く使うscreenのショートカット等

- C-a d
- C-a n
- C-a c
- screen -r
- screen -ls

## インスタンスに残さない

インスタンスはいつでも潰せるように。

- git
- S3やDropBox等
- gist


