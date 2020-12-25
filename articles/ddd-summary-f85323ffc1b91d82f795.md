---
title: "ドメイン駆動設計にまつわる概念"
emoji: "🪐"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["ddd"]
published: true
---

# 背景
### 目的・意図

チームで開発している際にDDDの概念に対する認識の齟齬を感じたことがあった。
また私自身もDDDを使った開発経験は豊富ではないので、フィードバックをもらえるように自身の認識を言語化した。特に解釈に幅があった概念を中心に扱った。

### 意識した点
- 提唱者である著者の「[エリック・エヴァンスのドメイン駆動設計](https://www.amazon.co.jp/dp/4798121967)」と評価の高い「[実践ドメイン駆動設計](https://www.amazon.co.jp/dp/479813161X)」を情報源とした
- 自分の解釈の論拠を示すべく、できるだけ参照元を明らかにした

### 表記法
- 「[エリック・エヴァンスのドメイン駆動設計](https://www.amazon.co.jp/dp/4798121967)」からの引用、参照は[Evans]と記す
- 「[実践ドメイン駆動設計](https://www.amazon.co.jp/dp/479813161X)」からの引用、参照は[IDDD]と記す

# ドメイン駆動設計の基本
## 用語の定義
### ドメインモデル

ドメインとは、ソフトウェアが対象とするユーザーに纏わる活動や関心事を指す。

[Evans] p2
> すべてのソフトウェアプログラムは、それを使用するユーザの何かしらの活動や関心と関係がある。ユーザがプログラムを適用するこの対象領域が、ソフトウェアのドメインである。

[IDDD] p41
> ドメインとは、広い意味で言うと、組織が行う事業やそれを取り巻く世界のことだ。事業が市場を定義して、プロダクトやサービスを販売する。組織にはそれぞれ、自分たちの対象とする領域についてのノウハウや物事の進めかたがある。その領域、そして業務を進めていくための方法が、ドメインだ。

モデルとは、膨大な知識を意味のある観点で簡素化した現実に対する一つの解釈を指す。

[Evans] p2, 3
> モデルとは簡素化である。つまり、当面の問題を解決する上で関連する側面を抽象化し、それ以外の詳細を無視することによって行われた、現実に対する１つの解釈なのだ。

> ユーザーの活動において有効利用されるソフトウェアを作成するために、開発チームはその活動に関係する体系化された知識を身につけていなければならない。ここで要求される知識の幅広さに手こずるかもしれないし、情報の量と複雑さに圧倒されるかもしれない。モデルはこの重荷と格闘するためのツールなのだ。モデルとは、選び抜かれてシンプルにされ、意図的に組み立てられた知識の表現形式である。適切なモデルは情報の持つ意味を明らかにし、その情報を問題に集中させる。

ドメインモデルとは、ドメインにおけるモデルのこと。

[Evans] p3
> ドメインモデルとは特定の図ではなく、図が伝えようとしている考え方である。これはドメインエキスパートの頭の中にある単なる知識ではなく、その知識が厳密に構成され、選び抜かれて抽象化されたものなのだ。

### ユビキタス言語

ユビキタス言語とは、開発者やドメインエキスパートを含むチーム全体で共有された言語を指す。ドメインについての議論や実装でもそのまま表現できる。単に、業界で使われている用語でも開発者だけが使う言語でもない。

ユビキタス言語をチームで使うことによって、開発者とドメインエキスパート間の言葉の翻訳がなくなり、モデルの概念の認識の差異が取り除かれる。

[Evans] p25
> チームが意識的に努力すれば、ドメインモデルはその共通言語の基盤となれるし、その一方で、チームのコミュニケーションをソフトウェアの実装と結びつけることもできる。この言語はチーム行う作業のいたるところに（ユビキタスに）存在できるのだ。

[Evans] p23
> モデルを最大限に有効活用するには、コミュニケーションのためのあらゆる媒体にモデルを浸透させる必要がある。そうすれば、テキストで書かれたドキュメントだけでなく、略式の図や、くだけた会話も、より役に立つようになる。こうした図や会話は、アジャイルプロセスで再び強調されるようになったものだ。また、コード自体とそのコードに対するテストを通じて、コミュニケーションが改善される。

[Evans] p24
> 共通言語のないプロジェクトの場合、開発者は、ドメインエキスパートのための通訳をしなければならない。（中略） 通訳することでモデルの概念を混乱させてしまい、それがコードの破壊的なリファクタリングにつながる。間接的にしかコミュニケーションをしていないと、分裂が起きつつあることが見えなくなる。

[Evans] p25
> 日々の議論で使う用語法が、コードに埋め込まれる用語法から切り離されている。（だが、コードはソフトウェアプロジェクトにおいて最終的に最も重要な成果物である）。同一人物でさえ話し言葉と書き言葉で違いがあるので、ドメインについての最も鋭い表現は、たいてい一時的なかたちでしか現れず、コードや文章ではとらえられることがない。通訳はコミュニケーションを鈍らせ、知識の噛み砕きを停滞させる。

> 開発者が使うのと同じモデルによって提供される言語は、開発者とドメインエキスパートが互いに意思疎通する際にも用いられなければならないし、ドメインエキスパート同士が用件や開発計画、あるいは機能を伝え合う際にも用いられなければならない。言語が広く利用されるほど、理解もよりスムーズに進むようになるのだ。

[IDDD] p22
> ユビキタス言語はチームでのパターンだ。ソフトウェアモデルに含まれる、コアビジネスドメインの概念や用語を見つけ出すために用いられる。ソフトウェアモデルには、名詞や形容詞そして動詞、その他の豊かな表現が反映される。そのチームで練り上げた、実際の会話で使うものだ。

### ドメイン駆動設計

ドメイン駆動設計とは、ユビキタス言語を使ってドメインをモデルで表現し実装と一貫させる開発手法のこと。DDDと略される。

[Evans] p3
> ドメイン駆動設計では、次に示すモデルの3つの基本的用法によって、どのモデルを選択するかが決定される。

> 1. モデルと設計の核心が相互に形成し合う。モデルと実装が密接に結びつくことによって、モデルはドメインと深く関連したものになり、モデルに対する分析が、最終成果物である実際に動くプログラムに適用されることが保証される。このモデルと実装の結びつきは、保守や継続的開発においても有効だが、それは、モデルの理解に基づいてコードを解釈できるからである。

> 2. モデルは、チームメンバ全員が使用する言語の基礎である。モデルと実装が結びついているので、開発者はプログラムについて話す際にこの言語を使える。通訳せずにドメインエキスパートとコミュニケーションができるのだ。しかも、言語はモデルに基づいているから、生まれながらの言語能力を使ってモデルそのものを改良できる。

> 3. モデルとは、蒸留された知識である。モデルは、ドメインの知識を構成して最も関心のある要素を区別するための、チーム内で決めた方法である。我々が用語を選択し、概念を分解して関連づける際に、ドメインについてどう考えることにしたいかということが、１つのモデルによってとらえられる。共有された言語があれば、開発者とドメインエキスパートが、情報をモデルという形式に苦労して交換する際に、効果的に共同作業ができるようになる。モデルと実装が結びついていることで、ソフトウェアの初期バージョンで得た経験が、フィードバックとしてモデリングプロセスに適用できるようになる。

[Evans] p47
> モデル駆動設計は、分析モデルと設計という二分法を捨て去り、両方の目的に使える単一のモデルを探し出す。純粋に技術的問題はさておき、設計にあるオブジェクトはそれぞれモデルで記述されている概念的な役割を果たすことになる。そのため、我々は選択したモデルに対する要求をもっと厳しくしなければならない。そのモデルは全く別々の2つの目標を満たす必要があるからだ。（中略） この結びつきの代償として、分析が、技術的な配慮から致命的に妥協した貧弱なものになってはならない。同様に、ドメインに対する考え方を反映しているが、ソフトウェア設計の原則を避けた出来の悪い設計も、受け入れることはできない。モデル駆動開発のアプローチは、分析としても設計としてもうまく機能するモデルを要求する。

> モデルについて再検討し、より自然にソフトウェアに実装されるように修正すること。これは、ドメインに対するより深い洞察を反映させようとする時にも言える。強固なユビキタス言語を支えることに加えて、ドメインと実装両方の目的に使える単一のモデルを要求すること。

[Evans] p59
> ドメイン駆動設計は、モデルがアプリケーションの問題を解決できるようにする。知識をかみ砕くことで、チームは、混沌とした情報のとめどない流れを実用的なモデルへと蒸留する。モデル駆動設計では、モデルと実装を密接に結びつける。ユビキタス言語はそれらすべての情報のための水路であり、開発者、ドメインエキスパート、ソフトウェアの間で情報がよどみなく流れるようにしてくれる。

## ドメイン駆動開発の手法
### 効果的なモデリングの要素

[Evans] p13

1. モデルと実装を結びつける
荒削りなプロトタイプを使ってモデルが何を意味し、実際に機能するソフトウェアにどう関係するのかを、ドメインエキスパートが明確に理解できるようにする。

2. モデルに基づいて言語を洗練させる
モデルから用語をそのまま取り出し、モデルの構造と矛盾しない文章にまとめて、通訳しなくても正確に理解できるようにする。（ユビキタス言語を見つけていく）

3. 知識豊富なモデルを開発する
モデルの振る舞いや守るべきルールを知る。

4. モデルを蒸留する
役に立たない、或いは核心でない概念を取り除き、本質的な概念を見つけていく。

5. ブレインストーミングと実験を行う
チームでシナリオを検討する時など会話で使われる表現自体が、提案されたモデルを実現できるどうかについて調べる。表現が明確でわかりやすいか、ぎこちないかを把握する。

### 知識をかみ砕く

モデルを洗練させるためには、開発者がドメインエキスパートから情報を引き出し、ドメインについて学びながら、役立たない或いは不要な概念を取り除き、隠れた概念を見つけていく必要がある。

[Evans] p14
> 有能なドメインモデラは知識をかみ砕く。彼らは情報の奔流の中に重要な一滴を探る。次から次へと考えをまとめてみて、大部分の意味を理解できるシンプルな見方を見つけようとする。

> 知識のかみ砕きは独りで行う作業ではない。開発者とドメインエキスパートからなるチームが共同して行うもので、たいていは開発者が率いる。一緒になって、彼らは情報を引き出し、それを噛み砕いて役立つかたちにする。

[Evans] p16
> 高度に生産的なチームは、自分たちの知識を意識的に育てて、継続的学習（Kerievsky 2003）を実践する。開発者にとって、これが意味するものは、（本書にあるような）一般的なドメインモデリングのスキルと合わせて、技術的な知識を向上させるということだ。ただし、その時に取り組んでいる具体的なドメインについて真剣に学習することも、ここに含まれる。

[Evans] p20
> 役立つモデルがすぐに見つかる表層にあることはめったにない。ドメインとアプリケーションがやるべきことを我々が理解するようになるにつれて、たいていの場合、表層にあり最初は重要と思われたモデル要素を廃棄するか、それらのモデル要素を違った視点で見ることになる。すると、最初は考えつかなかった、それでいて問題の核心を突くような、うまい抽象が現れてくるのだ。

### コミュニケーションと言語の使い方

ユビキタス言語をチームで使うことによって、開発者とドメインエキスパート間の言葉の翻訳がなくなり、モデルの概念の認識の差異が取り除かれる。

また、登場する概念を共通言語にする過程で、ぎこちなかったり食い違いがある用語や用語の組み合わせを修正しモデルに対する認識も修正されていく。

[Evans] p26
> 知識をかみ砕くプロセスが、より役立つモデルを作り出せるかどうかは、モデルに基づく言語に対してチームが献身するかどうかにかかっている。粘り強くユビキタス言語を使用すれば、モデルの弱点は明らかにならざるを得ない。チームは実験を行って、用語や、用語の組み合わせがぎこちない場合に、その代わりとなる表現を探す。言語に食い違いが見つかると、新しい単語が議論で使われるようになる。言語に対するこうした変更は、ドメインモデルに対する変更として認識され、用語の意味が変わった場合には、チームがクラス図を更新して、コード中のクラスやメソッドの名前を変えたり、振る舞いを変更することにまでつながる。

そのためには以下のことを実践する必要がある。

- ユビキタス言語をチーム内の会話でどこでも使う
- 用語や言い回しを統一する（一つのチームに一つの言語）
- 表現に違和感や認識のずれがあれば修正していく
- ユビキタス言語を実装に反映する

# 境界付けられたコンテキスト
## 重複した概念と偽同族語

最初の兆候は言語の混乱として現れる。具体的には以下の二つの場合がある。

1. 重複した概念のモデル（及びその要素）が2つある
2. 一つモデルが異なる概念を表現している

[Evans] p347
> 別々のモデルの要素を組み合わせると、2種類の問題が生じる。それが、重複した概念と偽同族語（false cognate）だ。概念の重複とは、実際は同じ概念を表しているモデル要素（およびそれに付随する実装）が2つあるということだ。その情報が変更されるたびに、2か所で変換を伴う変更が必要になる。

> 偽同族語はそれほど一般的でないかもしれないが、知らないうちにより多くの害を与える。これは、2人の人が同じ用語（または実装されたオブジェクト）を使って、同じことを話しているつもりでいるのに、実はそうではないというものである。


[IDDD] p59
e.g. 同じアカウントという用語の意味の多様性
- 銀行取引コンテキスト
  - 意味
    - 口座（アカウント）とは、負債や信用取引の記録を保持するもの
  - 例
    - 当座預金口座、普通預金口座
- 文学コンテキスト
  - 意味
    - 報告書（アカウント）とは、ある期間における、関連する出来事についての文章を集めたもの
  - 例
    - Amazon.comで「Into Thin Air: Personal Account of the Mt.Everest Disaster」という書籍が売られている

[Evans] p339
e.g. 料金という意味の多様性
- 請求書を送るモジュール
  - 料金
- 支払アプリケーションのモジュール
  - 料金

## 境界づけられたコンテキストの役割

境界づけられたコンテキストとは、特定のモデルが一貫した定義や表現で適用できる範囲のこと。
したがって、ユビキタス言語はコンテキスト中で閉じる。つまり同じ単語でもコンテキストが異なれば、別の概念を表した異なるユビキタス言語となる。

[Evans] p344, 345
> 境界づけられたコンテキストは、特定のモデルが適用できる範囲を制限する。そうすることで、チームメンバは、何が一貫性を持つべきで、それを他のコンテキストと同関係づけるのかということについて、明確な理解を共有できるようになる。そのコンテキスト内では、モデルを論理的に統一された状態で保つこと。ただし、その教会の外に対して適用できるかどうかは気にする必要がない。他のコンテキストでは他のモデルが適用されるが、そのモデルとは用語法や概念とルール、ユビキタス言語の方言が異なっている。

境界づけられたコンテキストが明らかになることで、異なる概念が一つのモデルになったり、同じ概念が複数のモデルに分散したりすることを防ぐことができる。
大きな概念の単一のモデルを使って実装していくのは困難な一方で、どの程度まで複数のモデルに分けるべきなのかという指針になる。

[Evans] p340
> 明示的に考える機会はあまりないのだが、モデルに対する最も根本的な要件は、内部で一貫していることだ。これは、用語の意味が常に同じであることであり、矛盾したルールが含まれていないことでもある。各用語の意味が明瞭で矛盾したルールがないという、モデルの内部におけるこうした一貫性は、統一性（unification）と呼ばれる。

> システムのいろいろな部分で、複数のモデルを開発できるようにする必要があるが、システムのどの部分なら枝分かれしてもよく、それら相互の関係がどうなるかについては慎重に選択する必要がある。モデルにおけるきわめて重要な部分を、緊密に統一された状態に保つ方法が必要なのだ。（中略）巨大なシステム向けのドメインモデルを完全に統一することは、現実的ではないし、コストにも見合わない。

[Evans] p344
> 複数のモデルはどんな巨大なプロジェクトにも存在する。だが、別々のモデルに基づくコードが組み合わせると、ソフトウェアは、バグの温床となり、信頼できなくなり、理解しにくくなる。チームメンバ間のコミュニケーションは混乱し始める。あるモデルをどのコンテキストで適用すべきでないのかについては、ほとんどの場合不明瞭である。

> 複数のモデルに起因する問題を解決するにあたっては、ある特定のモデルのスコープを明示的に定義しなければならない。このスコープはあるソフトウェアシステムにおける境界づけられた部分として定義される。そこには単一のモデルが適用され、できる限り統一性が保たれる。

e.g. 書籍という用語の多様性

出版社は書籍位の誕生から最後までのあらゆる段階を扱う必要がある。

- 書籍の内容を案としてまとめ、起草する
- 著者と出版契約を結ぶ
- 書籍の執筆と編集のプロセスを管理する
- 書籍の装丁や挿絵をデザインする
- 書籍を他の言語に翻訳する
- 紙の書籍や電子版を作成する
- 書籍を宣伝する
- 書籍を再販業者に販売する（あるいは顧客に直販する）
- 紙の書籍を再販業者や顧客に出荷する

書籍をひとつのモデルで表現すべきだろうか？

[IDDD] p61
> 段階ごとに「書籍」の定義も変わってくる。出版契約を結ぶまでは書名案も確定しないだろうし、その書名案だって編集中に変わるかもしれない。執筆・編集段階の書籍と言えば、草稿とそれに付随するコメントや校正の集まりと最終草稿のことだ。グラフィックデザイナーはページレイアウトを固める。プロダクションはそのレイアウトを使って出版イメージを作り、印刷に回す。マーケティングの際には、執筆・編集段階の成果物はほとんど使えない。使うのは、せいぜい表紙のイメージと概要説明くらいだろう。出荷の際に書籍が抱える情報は、ID・倉庫の位置・在庫数・サイズ・重量などだ。

> そんな望まざる状況に対応するため、DDDでのモデリングの際には、書籍のライフサイクルの段階ごとに、別の境界づけられたコンテキストを利用する。これら複数の境界づけられたコンテキストのそれぞれに、書籍を表す型を用意する。これらの書籍オブジェクトにはおそらく識別子があって、それをコンテキスト間で共有するのだろう。

e.g. コラボレーション機能

[IDDD] p51
> ユーザーやパーミッションはコラボレーションとは何の関係もなく、コラボレーションのユビキタス言語にも含まれない。ユーザーやパーミッションは、認証やアクセスに関する概念であり、セキュリティに関わるものだ。コラボレーションコンテキストに含まれるすべての概念（コラボレーションドメインのモデルを取り囲む境界づけられたコンテキストの中にある概念）は、コラボレーションに関する言語的な関連を持つべきだ。

複数のユーザーが連携してディスカッションやフォーラムを開催するサービス

- コラボレーション
  - ユーザー
  - パーミッション
- フォーラム
- 投稿
- ディスカッション
- カレンダー
- カレンダーの項目

[IDDD] p61, 61
> コラボレーションコンテキストのドメインエキスパートは、コラボレーション機能の利用者のことを「パーミッションを持つユーザー」とは定義しなかった。そうではなく、そのコンテキストにおいて利用者が演ずる役割、つまり投稿者・所有者・参加者・モデレーターと定義したのだ。

> 一方認証・アクセスコンテキストでは、ユーザーについて考える。このコンテキストにおいては、ユーザーオブジェクトが各個人のユーザー名と詳細情報を保持する。詳細な連絡先もそこに含まれるだろう。

> まずは、認証・アクセスコンテキストにおいて適切なロールを演ずるユーザーの存在を確認する。認証ディスクリプタの属性が、認証・アクセスコンテキストへのリクエストとして渡される。モデレーターなどの新しいコラボレーターオブジェクトを作るには、ユーザーの属性の一部とロールの名前を使う。

> 今ここで重要なのは、これら二つの異なる概念が、同じものであるともいえるし違うものだともいえるということだ。その違いは、どの境界づけられたコンテキストで見るかによるものだ。

- 認証・アクセスコンテキスト
  - ユーザー
  - ロール
- コラボレーションコンテキスト
  - モデレータ

## 境界づけられたコンテキストの特定

境界づけられたコンテキストを特定するのはどうすれば良いか？具体的な手順が記された方法論は見つけられなかったが、少なくとも重複した概念と偽同族語を見つけ、そこに境界を引いていく必要があることは分かる。

そのためにはユースケースごとに登場するモデルの利用されるフィールドがどのようなものか、ユビキタス言語で説明した時に違和感がないか確認していくことができる。

[IDDD] p66
> 偽のコンテキストを作ってアーキテクチャ的な問題や開発者の問題に対応してしまうと、言語が分断されて、表現力を失ってしまう。そうならないように、コアドメインに注目し、単一の境界づけられたコンテキストに自然におさまる概念だけに注目する。その際には、ドメインエキスパートの用語に従う。そうしておけば、単一のモデルにうまくおさまるようなコンポーネントを見つけだせるだろう。

> 小型の境界づけられたコンテキストを作ってしまうという問題は、注意深くモジュールを利用すれば回避できることもある。複数の「境界づけられたコンテキスト」にまたがるサービス群をよく調べてみれば、モジュールを適切に活用すれば、実際には単一の境界づけられたコンテキストにまとめてしまえると気づけるだろう。

境界づけられたコンテキストの整合性を保つには概念の分断に気づけるように、コンテキストの範囲内で実装を頻繁にマージし、ユビキタス言語が一貫するように常に注意して会話する必要がある。

[Evans] p350
> すべてのコードと他の実装成果物を頻繁にマージさせるプロセスを策定すること。その際、分裂に対して素早く警告する自動化されたテストも一緒に用いること。ユビキタス言語の執拗な鍛錬を絶え間なく行い、モデルに対する共有された見方を練り上げること。概念は、別々の人の頭の中で進化していくのだ。

# 集約とは
## 定義とルール

不変条件とはオブジェクトが変更されても常に維持されなければならないルールのこと。

[Evans] p126
> 不変条件とは、データが変更される時は常に維持されなければならない一貫性のルールで、集約のメンバ間の関係も含んでいる。

[Evans] p124
> 複雑な関連を伴うモデルでは、オブジェクトに対する変更の一貫性を保証するのは難しい。維持すべき不変条件には、個々のオブジェクトに適用されるものだけではなく、密接に関連するオブジェクトのグループに適用されるものもある。だが、慎重にロックしすぎると、今度は複数のユーザが指針もなく相互に干渉試合、システムが使いものにならなくなる。

集約とはトランザクション整合性が保たれるべきオブジェクトの集まりで、ルートと境界を持つ。

[Evans] p125
> まず、モデル内にある参照をカプセル化するための抽象化が必要である。集約とは、関連するオブジェクトの集まりであり、データを変更するための単位として扱われる。各集約にはルートと境界がある。境界は集約の内部に何があるのかを定義するものだ。ルートは集約に含まれている特定の１エンティティである。集約のメンバの中で、外部のオブジェクトが参照を保持してよいのはルートだけである。

[IDDD] p340
> 整合性の境界の論理的な意味は、「その内部にあるあらゆるものは、どんな操作をするにもかかわらず、特定の不変条件のルールに従う」ということだ。この境界の外部にある、あらゆるものの整合性は、集約とは無関係になる。つまり、集約はトランザクション整合性の境界と同義である（中略）。

[Envas] p127
> ルートがアクセスを制御するので、内部が知らないうちに変更されることはなくなる。この取り決めにより、どんな状態変化においても、集約内にあるオブジェクトと集約全体に対して、不変条件をすべて強制することが現実的になる。 

以下のルールを強いることで、集約内部のオブジェクトに対する変更がコミットされる時には、集約全体の不変条件を満たすことができる。

- データベースに問い合わせて直接取得できるのは、集約ルートだけとなる
  - 集約ルートのエンティティは、グローバルな同一性を持つ
  - 集約内部のエンティティは、集約内でのみ一意となるローカルな同一性を持つ
- 集約外部からは集約ルートのエンティティの参照のみ保持できる
  - ルートエンティティから内部のエンティティへの参照を他のオブジェクトに渡せるが、一時的に利用することができるが保持してはならない

[Evans] p126
e.g. 自動車の集約

以下のユースケースがあるとする。

- 不変条件として、自動車は4つのタイヤと車輪を持っていなければならない
- 自動車の購入者は、自分の自動車を世界にあるどんな自動車とも区別したい
- タイヤの同一性などは特定の自動車というコンテキストの外部で気にされることはない

その場合以下の集約ができる。

- 自動車(集約ルート)
  - タイヤと車輪のIDのペア
  - 車両登録番号（グローバルな識別子）
- タイヤ（ローカルの同一性）
- 車輪（ローカルの同一性）
- 位置（ローカルの同一性）

タイヤの位置を変更したり、新しいものと入れ替えたりするには集約ルートを経由して行う。

## 適切な単位の特定

ドメインにおけるトランザクション整合性を分析した上で、集約を見つける。
また、大きすぎるトランザクションはパフォーマンスやスケーラビリティの問題をもたらすので、必要最小限に抑える。

[IDDD] p340
> 適切に設計された集約では、業務で必要とするあらゆる変更に対して、トランザクション内での不変条件の整合性を完全に維持できる。また、境界づけられたコンテキスト適切に設計すれば、どんな場合でも、ひとつのトランザクション内で変更する集約をひとつだけに絞り込める。さらに、トランザクションの分析をしてからでないと、集約の設計の善し悪しを正しく判断することはできない。

[IDDD] p343
> 必要な要素とは、いったいどれのことだろう？この問いに対するシンプルな答えは、「他の要素との整合性を保つ必要があるもの」である。

[IDDD] p344, 355
また集約をまとめて整合性を保つ必要がある場合は、不変条件を見落としていることになる。なぜなら個々の集約が不変条件を満たすべき単位だからである。

その場合、複数の集約をひとつの概念にして、新しい名前（ユビキタス言語）をつけることができる。しかし、それをひとつの大きな集約にすると、集約はロックにまつわる問題を引き起こす。
そこで、アトミックな整合性ではなく結果整合性でユースケースを満たせないか考える。

# ドメインイベント
## 定義

ドメインイベントはドメイン内で発生する何かしらの出来事を表す。

[IDDD] p273
> ドメイン（２）にイベントを実装することに関する議論の前に、ドメインイベントが現在どのように定義されているかを確認しておこう。「ドメインエキスパートが気にかける、何かの出来事」である。

[IDDD] p274
ドメインエキスパートにとってどの出来事が重要であるかは、ドメインエキスパートが以下のフレーズを話した場合を参考にする。

- 「...するときに、」
- 「もしそうなったら、...」
- 「...の場合は、私に知らせてほしい」、「...の場合は、通知して欲しい」
- 「...が発生したときに、」

そして、ドメインイベントをモデリングする場合は、ユビキタス言語に従い、コマンドの過去形を使う。

[IDDD] p277
> イベントをモデリングする際に、その名前やプロパティは、イベント発生元の境界づけられたコンテキストのユビキタス言語に沿ったものとする。集約上で何かしらのコマンドを実行した結果として発生するイベントの場合は、実行したコマンドにもとづくイベント名を使うことが多い。コマンドがイベントの発生要因なので、イベントの名前には、実行されたコマンドを用いるのが適切だ。

> 集約からのイベントを出版するときに重要なのは、その出来事が過去に発生したことがわかるような名前にすることだ。今まさに怒っているということではなく、「こういう出来事が発生した」ということだ。発生したという事実を反映した名前を選ぶのが望ましい。

## 役割

主に集約間の結果整合性を用いた連携に使われる。

前述の通り単一のトランザクションでは単一の集約だけが変更されるべきで、それができない場合は結果整合性を保つことで複数の集約を連携させる必要がある。イベントを使うことでそれが実現できる。

[IDDD] p284
> 最もありがちなドメインイベントの使用例は、集約がイベントを作成し、それを発行するという場面だろう。

[IDDD] p282
> イベントを捕捉するには、別の集約の状態に依存している集約を見つけるのが最も簡単だろう。そういう状況では、結果整合性を保つことが必須になるからだ。

[IDDD] p275
> イベントを他のコンテキストに配送する際には、それが同じシステムであろうが別のシステムであろうが、結果整合性を利用するのが一般的だ。これは、やむを得ずそうするのではなく、意図的に行うものだ。そうしてしておけば、グローバルなトランザクションにおける二相コミットや、集約（10）のルールを気にする必要がなくなる。集約のルールのひとつは、単一のトランザクション内では単一のインスタンスだけを変更しなければならないというものだ。それに依存するその他の変更は、別のトランザクションで行わなければならない。そこで、ローカルの境界づけられたコンテキスト内のその他の集約のインスタンスの同期にも、この手法を使う。


## ドメインイベントによる通信

[IDDD] p284~290
ドメインイベントをメッセージング基盤のミドルウェアを使って別のプロセスに転送することができる。しかし、ミドルウェアとイベントを発行するドメインモデルが密結合になってしまうと、ミドルウェアなど設定の知識がドメインモデルに漏れてしまう。

そのため、以下のようにオブザーバパターンを使ってドメインモデルとミドルウェアを疎結合にする。

- アプリケーションサービスがパブリッシャーにサブスクライバを登録する
- 集約がイベントを作成しパブリッシャーに渡す
- パブリッシャーは対応するサブスクライバにイベントを渡す

このようにすると、イベントが発行されると同じプロセスで一件ずつ同期的にサブスクライバに通知ができる。その一つにイベントをイベントストア（イベントを保持するためのテーブル）に保存するサブスクライバを登録しておくと、そこからイベントをメッセージング基盤が取り出して別のコンテキストに転送することができる。

このようにするには、イベントを発生させる振る舞いとイベントストアの保存がトランザクション整合性を持つ必要がある。これを一つの不変条件とみなすと、コマンドを受け取ったそのようなオブジェクトは集約として扱える。

[IDDD] p291
> これまで散々結果整合性について話してきたので、メッセージングのソリューションにおいて、少なくとも二つのメカニズムは常に整合性を保たないといけないと聞くと驚くかもしれない。その二つとは、ドメインモデルが使う永続化ストアと、モデルから発行されたイベントをメッセージング基盤が転送する際に使う永続化ストアだ。これらの整合性を保つことで、モデルへの変更が永続化されたときに、イベント配送されることが保証される。そして、イベントがメッセージングで配送されたときに、それが発行元のモデルの状況を正しく反映したものであることも保証される。もしこれらのうちひとつでも不確かになれば、お互いに依存しあうモデルの状態が、不正確なものになってしまう。

また、メッセージング基盤がドメインイベントを取り出して発行するには以下のデータの管理の仕方がある。

[IDDD] p291
1. ドメインモデルとメッセージング基盤が、永続化ストア（データソースなど）を共有
2. ドメインモデルの永続化ストアと、メッセージング用の永続化ストアをグローバルな二相コミットで制御する
3. イベント用の特別なストレージ領域（データベースのテーブルなど）をドメインモデルが使っているのと同じデータストア内に用意する（イベントストア）

[IDDD] p316, 317
そして、メッセージング基盤からイベントを受け取るサブスクライバは、同じイベントが重複して送られる場合に対処する必要がある。

具体的には以下の二つの手段がある。

- 何度も同じイベントを受け取っても一度だけ実行したときと同じ結果になるようにする（冪等な操作）
- サブスクライバ側で処理済みのイベントを確認できるようにしておく
