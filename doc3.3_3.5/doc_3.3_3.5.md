<!-- $theme: gaia -->

# <div style="text-align: center;">チーム開発実践入門</div>

### <div style="text-align: center;">3.3~3.5</div>

#### <div style="text-align: center;">手島　史裕</div>

---
<div style="font-size: 24pt">

# 目次
</div>

* 3.3 分散バージョン管理システム
* 3.4 バージョン管理システムをどう使うべきか
* 3.5 Gitを使ったスムーズな平行開発

---
## 3.3 分散バージョン管理システム
---

###### メリット
<div style="font-size: 14pt">

* リポジトリのコピーをローカルに配置可能
* 動作が速い
* 履歴管理が容易
* ブランチ、マージが容易
* 場所を選ばないコラボレーションが可能

</div>
	
###### デメリット
<div style="font-size: 14pt">

* 最新バージョンが存在しない
	* 中央リポジトリがシステム上に存在しないため任意に設定する必要がある
* 真の意味でのリビジョン番号がない
	* G分散バージョン管理システムでは **GUID** で変更が管理される
	* 直感的ではなくなるが、代わりにマージが容易になる
* ワークフローが柔軟に設定可能なため、混乱しやすい
	* どのリポジトリ間でも自由にPush/Pullが可能
	* 一般には中央リポジトリを設定し、各開発者がそこからcloneする
* 考え方に慣れるのに時間がかかる
	* 難しい

</div>

---
## 3.4 バージョン管理システムをどう使うべきか

---
## 管理すべきもの
###### ソースコード
<div style="font-size: 14pt">

* そもそもソースコード管理用に考えられたシステムである
</div>

###### ドキュメント
<div style="font-size: 14pt">

* プロジェクトの進行度合いでドキュメントにも変更がある
* Word, Excelのバイナリファイルは、バージョン管理には不向きのため、
**Markdown**、**Textile**、**reStructedText**など、textベースのものを利用するのが吉

</div>

###### データベーススキーマ、データ
<div style="font-size: 14pt">

* Webアプリを扱うにあたり、データのバージョン管理は必須
</div>

###### 設定ファイル
###### ライブラリなどの依存関係の定義

---
## 3.5 Gitを使ったスムーズな平行開発
## ブランチの使い方
---
###### クローンとブランチの作成
<div style="font-size: 14pt">

1. 中央リポジトリからローカルマシンにクローン
`git clone ***@github.com`
2. 機能追加のためにブランチを作成する
`git branch develop`
3. チェックアウトにより、ブランチを切り替える
`git checkout develop`
4. いくつかコミットする
`git commit -m "機能追加"`
`git commit -m "機能修正"`
`git commit -m "機能変更"`
コミット後は、以下のような状態になる
</div>

![3.2](image/3.2.jpg)

---
###### ブランチの切り替え
<div style="font-size: 14pt">

* 障害発生などで、masterに戻って作業するとき

1. チェックアウトでブランチを変える
`git checkout master`
2. 問題修正用のブランチを作成し、チェックアウトする
`git checkout -b issue345`
上記のコマンドでブランチ作成とチェックアウトを同時に行える
</div>

###### バグ修正後のコミット
<div style="font-size: 14pt">

1. バグ修正＆コミット
`git commit -m "メールバグ修正"`
`git commit -m "デッドロック修正"`
`git commit -m "無駄なコード削除"`
コミット後は、以下のような状態

![3.3](image/3.3.jpg)
</div>

---
###### masterへのマージ
<div style="font-size: 14pt">

* 修正結果をmasterにマージする
	`git checkout master`
    `git merge issue345`
    マージは、以下の図のような状態
</div>

###### masterへのPush
<div style="font-size: 14pt">

1. ローカルマシンのmasterにマージした修正を中央リポジトリにPushする
`git push origin master:master`
2. 元の開発をしていたブランチに戻る(図4のd)
`git checkout develop`

<div style="text-align: center;">

![3.4](image/3.4.jpg)
</div>
</div>

---
# タグの使い方
---

###### タグとは
<div style="font-size: 14pt">

* リリースタイミングをスナップショットとして記録できる機能
* 一般的にはバージョン番号を付けることが多い
* リリース時や障害対応ごとにタグを打つべきである
</div>

###### タグの作成
<div style="font-size: 14pt">

* タグをつけたいコミットを指定してタグを打つ
`git tag -a v0.1 GUID`
* タグの中身を確認する場合は、`git show v0.1`とすれば確認可能
* タグ作成後は中央リポジトリにPushする
`git push origin v0.1:v0.1`

</div>
