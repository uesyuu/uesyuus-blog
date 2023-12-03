---
title: WCA Live botを4年間運用してきた所感
author: uesyuu
type: post
date: 2023-12-04T00:00:00+09:00
categories:
  - 未分類
  
---
&nbsp;

この記事は[Speedcubing Advent Calendar 2023](https://adventar.org/calendars/8548) 4日目の記事です。3日目の記事はメガミンクス解けました！さんの「[OLL Transformation (from 3 OLL to Mega OLL)](https://xingfu771da.hatenablog.com/entry/2023/12/03/105809)」でした。5日目の記事はあむすさんの記事です。

&nbsp;

こんにちは、うえしゅうです。

&nbsp;

今回は僕が製作したTwitterのbot、WCA Live botについて紹介をし、使った技術や運用する上で苦労した話などを書いていこうと思います。

&nbsp;

## WCA Live botとは？

WCA Live botとは、WCA大会の記録がリアルタイムで反映されるサイト WCA Liveで世界記録(WR)、大陸記録(CR)、国内記録(NR)が入力された際に、その変更を即座に検知しTwitterに投稿するTwitter botです。

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Masato Fujiwara (藤原正人) (from Japan) just got the 3x3x3 Blindfolded single NR (19.86) at Minatomirai 2022 <a href="https://t.co/LIIEDbaLIV">https://t.co/LIIEDbaLIV</a></p>&mdash; WCA Live bot (unofficial) (@WCALive_bot) <a href="https://twitter.com/WCALive_bot/status/1519909414693654530?ref_src=twsrc%5Etfw">April 29, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

&nbsp;

### 作った経緯

元々WCA大会の記録反映サイトはcubecompsが使われており、その時はcubecompsのTwitterアカウントもあったため記録ツイートが常にTL上に投稿されていました。
日本のキューバーって大体がTwitterを使っているので、みんなで情報を共有するにはTwitter botという形はとても都合が良かったんですね。

しかし、2019年にcubecompsが廃止され、新たにWCA Liveというサイトで大会の記録情報が管理されるようになりました。
これ自体はとてもモダンなサイトでリアルタイム更新もあり使いやすかったのですが、唯一公式のTwitter botがありませんでした。
そのため日本人キューバーのTwitter界隈はTwitterで記録更新を知ることができず、少しばかり不満がありました。僕もそうでした。
やっぱりWRのツイートがTLに流れてきてみんなでRTとか引用RTとかしてTLが盛り上がるのを見たいじゃないですか。

なので、どうにかしてWCA LiveのTwitter botを自作できないかと常々考えていました。

2020年の正月休みに、一念発起してWCA Liveのbotを作ることに決め、色々調べつつなんとか作り終えました。
正月休みは6日間あったんですが、結局botを作るのに6日間全部溶けてしまいました。

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">WCA Liveの更新情報をツイートするbotを作りました！よかったらフォローお願いします！<a href="https://twitter.com/WCALive_bot?ref_src=twsrc%5Etfw">@WCALive_bot</a></p>&mdash; うえしゅう (@uesyuu_cube) <a href="https://twitter.com/uesyuu_cube/status/1213396217230544898?ref_src=twsrc%5Etfw">January 4, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

&nbsp;

WCA Live botを公開して少し経った時に、えすぷれ君がWCA Live botのいい感じのロゴを作ってくれました。めっちゃ良くないですかこれ？えすぷれ君には感謝しています。

<blockquote class="twitter-tweet"><p lang="zxx" dir="ltr"><a href="https://t.co/txoEXzn5Zm">pic.twitter.com/txoEXzn5Zm</a></p>&mdash; えすぷれ (@espr_cubes) <a href="https://twitter.com/espr_cubes/status/1216662437610455040?ref_src=twsrc%5Etfw">January 13, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

&nbsp;

こうしてWCA Live botが誕生し、色々な人に使われることになります。

&nbsp;

## 作ってみての反響

色々な人に使っていただきたいと思って製作したWCA Live botですが。予想を超えて本当に多くの人に使われているようです。
現在のフォロワーは2298人(2023/11/17時点 TODO: 投稿前に変更)で、日本と海外問わず色んな方からフォローされています。

当たり前ですが、日本のフォロワーの方はやっぱり多くて、日本のNRツイートのいいね数やRT数は段違いです。
やっぱり日本のNRツイートが出ると嬉しいし、作ってよかったなってこういう時一番思います。

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Ao Nogami (野上碧) (from Japan) just got the 3x3x3 Cube average NR (6.66) at Tokyo Challenge VIII 2023 <a href="https://t.co/OgyO1bP1Pu">https://t.co/OgyO1bP1Pu</a></p>&mdash; WCA Live bot (unofficial) (@WCALive_bot) <a href="https://twitter.com/WCALive_bot/status/1720713533627773192?ref_src=twsrc%5Etfw">November 4, 2023</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

&nbsp;

また、意外なところでいうと、スペインのキューバー界隈でこのbotが人気のようです。
スペインのNRツイートのいいね数とRTが他と比べてすごい伸びることが多いんですよね。
スペインってTwitter盛んなんですかね？

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Berta García Parra (from Spain) just got the 3x3x3 Blindfolded single CR (16.39) at Cervantes Cubea 2022 <a href="https://t.co/1AtHEplGQQ">https://t.co/1AtHEplGQQ</a></p>&mdash; WCA Live bot (unofficial) (@WCALive_bot) <a href="https://twitter.com/WCALive_bot/status/1512787456348901380?ref_src=twsrc%5Etfw">April 9, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

&nbsp;

そして、何よりもWRが出た時のツイートの伸びが半端ないです。
Maxが3x3 single WR出した時のツイートが635いいね、332RT、7.7万インプレッションと多分過去最高に伸びたツイートなんじゃないかと思います。
もちろん日本人のリアクションも多いんですが、海外の方からのリアクションも多く海外で相当使われてるんだなというのが見て取れます。

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Max Park (from United States) just got the 3x3x3 Cube single WR (3.13) at Pride in Long Beach 2023 <a href="https://t.co/YncMB7Yxn2">https://t.co/YncMB7Yxn2</a></p>&mdash; WCA Live bot (unofficial) (@WCALive_bot) <a href="https://twitter.com/WCALive_bot/status/1667960722511339521?ref_src=twsrc%5Etfw">June 11, 2023</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

&nbsp;

また、Yihengの3x3 avg WR 4.48のツイートについてはなんとあのFeliks Zemdegsから引用RTを頂いています！
他にもFeliksはいくつかのツイートを引用RTしてくれていて、WCA Live botの引用RTが並ぶFeliksのツイート一覧を見るとなんとも言えない気持ちになります。
Feliksに認知されてるなんてほんとに考えられないですね。

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Ok mind blown <a href="https://t.co/YybyEWyUsy">https://t.co/YybyEWyUsy</a></p>&mdash; Feliks Zemdegs (@Fazrulz) <a href="https://twitter.com/Fazrulz/status/1671116365690978304?ref_src=twsrc%5Etfw">June 20, 2023</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

&nbsp;

ちなみに他にもMats ValkやCiarán Beahan、Martin Vædele Egdal
などの名だたる有名海外キューバーにフォローされており本当に光栄です。

&nbsp;

## 使った技術変遷

WCA Live botはサーバー側でプログラムを動かしており、20分に1回WCA LiveのAPIにアクセスして前回との差分があればツイートし、ツイートし終わったらデータベースにその情報を保存しておく、というシステムで運用しています。

色々な事情があって、裏側のシステムは2回大幅な変更がされています。

### 初代

最初の実装では、botはVPS上で動かしていました。
ちょうどこの頃サーバー周りの学習用にさくらのVPSを契約しており、それを流用してPythonとMySQLをVPSに入れて運用していました。
定期実行は自分でcron書いて実行させてました。

そしてWCA Liveの情報を取得する部分ですが、なんとこの頃はスクレイピングでWCA Liveのサイトトップから必要な情報だけ抜き出して強引に取得していました。
WCA Liveって外部に公開しているAPIがなかったのでこうするほかなかったんですね。

スクレイピングって静的サイトであれば簡単なんですが、WCA Liveみたいな動的サイトでやろうとするとけっこう大変でした。
動的サイトって
1. HTMLファイルを取得
2. クライアントサイドでJavaScriptを使って通信を行いページ情報を更新する
という順番で行われるんですが、普通にスクレイピングのライブラリを使っても1しかやってくれないので普通にやっても空のHTMLしか取れないんですね。
なので少し工夫が必要です。

今回はPhantom JS Cloudというヘッドレスブラウザサービスを使うことで、解決しました。
流れとしては以下の通りです。
1. Phantom JS CloudのAPIにWCA LiveのURLを渡す
2. JavaScriptが実行された後のHTMLファイルを返してくれる

こんな感じで色々詰まりポイントがあったので、作るのには苦労しました。
また一度リリースしてもHTMLの構造が変わりうまくスクレイピングができなくてbotが暴走したりして、けっこう大変な時期でもありました。

結局、この年の3月辺りからコロナの影響でWCA大会が全く開かれなくなり、WCA Live botも2ヶ月間の運用で一旦ストップしてしまいます。

### 二代目

1年近くbotをVPSで動かしていたんですが、VPSの毎月の料金が結構する(月800円)のもあってVPSを解約することになり、無料運営する方法を模索し始めました。

結局Herokuの無料枠を使うことに決めました。HerokuにはPostgreSQLが無料で付いてるし、データベースの入った無料サーバーが借りられるのってここくらいしかなかったんですよね。

定期実行に関しては、Herokuの機能でcronをWeb上で設定できるサービスがあったので、VPSでやっていたときよりも簡単に定期実行を設定できました。

また、この辺りでWCA Live botのGitHubにWCA技術チームのJonatanからissueが飛んできて、なにかと思えば「WCA Liveの内部APIがあるからそれ使ってもいいよー」との事でした。

<img src="/images/2023/12/github_jonatan.png" width="600" />

&nbsp;

スクレイピングだとちょいちょい不安定な事があるのでこの方法に変更し、それ以降はAPI周りで特に変なことは起こっていません。
この内部API、一般的なREST APIではなく最近流行りのGraphQL APIが使われており、やっぱりキューバーって技術屋が多いから最近の流行りも取り入れるんだなーと思ったりしました。

### 三代目

2022年辺りに悲しいニュースが舞い込んできます。
Herokuが無料枠を廃止するとのことです。

Herokuみたいな何でも使えるサーバーを無料提供するサービスってほとんどないので、自分もそうだしエンジニア界隈は結構大騒ぎの様子でした。

WCA Live botをどこに移行するか考えた結果、Googleの提供するFirebaseに移行することに決めました。
Firebaseとは一般的にサーバーが行う機能を簡単に実装できるサービスを複数提供する便利サービスです。
その中でも今回はCloud FunctionとFirestoreを使用しました。
Cloud Functionはプログラムの定期実行を行うサービスです
Firestoreはいわゆるデータベースですね。

ここで少し苦労したのは、Cloud FunctionはJavaScriptがデフォルト言語でPythonは使えないというところです。
今までPythonでbotを動かしていたので、JavaScriptに書き直さなきゃいけないというのはちょっと大変でした。

ちなみにこのFirebaesは無料枠が結構大きく、個人開発でそんなに大きいものでなければ基本無料で使うことができます。
WCA Live botも無料で運営することができました。

&nbsp;

こんな感じで4年間の間に色々な技術変遷があり、最終的に今の形に落ち着いています。

&nbsp;

## 苦労話

botを4年間も運用していると色んなハプニングが起こってきます。
特に去年と今年は色んなことがあり、その度に本当に運用続けられるのか？と疑問に思いながら対応をしていました。

### Twitter APIに翻弄された

まあこれが一番ですね。

今年に入ってTwitterのCEOがイーロン・マスクに変わったことでTwitterも色々様変わりし、皆さんも色々翻弄されたと思います。
僕たち開発者ももちろんその影響を受け、API使用数が厳しく制限され有料版の価格は月10000円を超えたりと個人開発者が払える額ではありませんでした。
結局ツイートAPIに関しては月1500ツイートまで無料と発表され、WCA Live botは最高でも月800ツイートほどだったので無料枠の範囲内で運用することができました。
ほんとこういうのやめてほしいですね。

また他にも、Twitter APIの調子が頻繁に悪くなって記録がツイートされないこともしばしばあり、どうやったらツイート失敗したことを検知できるかを模索していました。
対処法としては、ツイートエラーなどが起きた際にエラーログを出力し、Firebaseのログを監視するツールを活用してエラーログがあったらメールで知らせるというシステムを作りました。
これが結構うまく動いていて、月に数回エラーメールが飛んでくるのでその度に手動でツイートし直したりしています。

### WCA LiveのAPIにアクセスできない時期があった

今年半ばに突然WCA Live botが動かなくなり、色々原因を探っていたのですが分からず、WCA LiveのAPI側の問題の可能性も考えてWCAソフトウェアチームにメールを投げてみました。
すると、ちょうどその頃アメリカでUS Nationalsが開催されており、セキュリティの関係上信頼できるクライアントからのアクセス以外を一時的にシャットアウトしていたようなのでした。
そのため、こちらが勝手にFirebaseからアクセスしていたAPIアクセスは通らなかったというわけです。
これはまあさすがに仕方ないですね。

原因がわかったので、海外の方への説明の意味も込めてbotで上記のことを英語でツイートしておきました。

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">[Info]<br>The WCA is strengthening the security of its site due to the US Nationals being held, so API access is not available.<br>Therefore, the WCA Live bot will not work during the comp.<br>I will restart the bot as soon as the comp is over.<br>Sorry.</p>&mdash; WCA Live bot (unofficial) (@WCALive_bot) <a href="https://twitter.com/WCALive_bot/status/1684955581390704640?ref_src=twsrc%5Etfw">July 28, 2023</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

&nbsp;

4日間のUS Nationalsが終わり、アクセス制限が解除されたと同時にWCA Live botが復活しWRやCRツイートを何十個もツイートしていました。

8月の世界大会でも同じことが起きるんじゃないかと危惧しており、案の定アクセス制限がかかりツイートが止まってしまいました。

大きい大会って有力選手も多数出場するので、必然的にWRやCRも出がちで本当はそういうときこそbotが動いてほしいんですよね。

ちょうど僕も世界大会に現地参戦していたので、世界大会の会場にいたWCAソフトウェアチームのリーダーのグレゴールさんにその旨を説明し、どうにか制限を解除してもらえないか頼んでみました。
しかしやはりセキュリティの関係上それは難しいとの答えでした。
また、公式で同じようなbotを作る案も上がっているが、他に優先すべきタスクがあるのでそちらにまだ手を回せてないとの事でした。
まあ仕方ないですね。
これからもこういった大きい大会中はbotが止まるかもしれませんが、その時はご了承ください。

ちなみにこのグレゴールさんは日本語が少し話せる方で、コミュニケーションがすんなりできたのは嬉しいポイントでした。

&nbsp;

## おわりに

WCA Live botが誕生してからもう4年が経ちます。
その間に日本のキューバーや海外のキューバーにbotの存在が広まり色んな方に使っていただけているようでとても嬉しい限りです。
世界大会でWCAの方にbotについて訪ねたときも、このbot知ってますよと言われて結構驚きでした。

これからもWCA LiveとTwitterが続く限りWCA Live botは動かしていこうと思っています。
応援よろしくお願いします。

&nbsp;

それでは。

&nbsp;