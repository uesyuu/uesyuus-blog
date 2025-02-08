---
title: 4b2のセットアップ手法「corner swap insertion」
author: uesyuu
type: post
date: 2025-02-08T22:00:00+09:00
categories:
  - 未分類
  
---

&nbsp;

こんにちは、うえしゅうです。

> 注: この記事はHTR subsetsを理解している方向けの記事です。HTR subsetsを知らない方は[こちらの記事](https://blog.uesyuu.com/post/2023-11-23-htr-subsets/)をご覧ください。

&nbsp;

FMCでDR後にHTRを作る時に、bad cornerだけではなくbad edgeも加味してHTRを作りにいくのは結構難しいです。

特に、どのルートからでもよく通る4b2状態でのHTR作成は初見だと戸惑うことが多いです。

この記事では、4b2のHTR作成に便利な考え方「corner swap insertion」を説明します。

corner swap insertionを使えば大体の4b2状態からHTRを作ることが可能になります。

&nbsp;

## corner swap insertionとは

`Scramble: U' R2 U R2 F2 R2`

<img src="/images/2025/02/1_1.png" width="80" />

まずこちらのスクランブルですが、bad cornerはUFR, UBR, DFR, DFLで4b2の状態、bad edgeはDF, DRで2e(2エッジ)となっています。画像はbadパーツのみを表しています。

ここからR2 F2 R2と回してみましょう。bad cornerはUFR, UFL, DFR, DBR、bad edgeはUF, DRとなり、U' R2 Uトリガーの形にセットアップすることができました。

この3手で何が起きたのか。

まずコーナーだけ見ると、R2 F2 R2でbad cornerの配置が左右対称に変わっています。

次にエッジを見るとR2 F2 R2の真ん中のF2の動きでDFとUFが交換されています。

まとめると、R2 F2 R2という動きはbad cornerの配置を左右対称に変え、真ん中のF2によりbad edgeの位置を変える働きがありました。

この3手こそがcorner swap insertionであり、これを応用すると4b2のセットアップが容易になります。

&nbsp;

## corner swap insertionのバリエーション

このR2 F2 R2という動きですが、この3手のどれを二層回しに変えてもコーナーには影響ありません。複数個を二層回しに変えても問題ないです。

さらに、R2 F2 R2ではなく左右対称のF2 R2 F2を行ってもコーナーは同じく左右対称に変わるのみで特に影響はありません。もちろんF2 R2 F2に二層回しを入れても同じです。

このように3手の動きに二層回しを入れてもコーナーは影響ないのですが、エッジの位置が変わります。

つまり、基本の3手の動きの中に適切なタイミングで二層回しを入れることで4b2トリガーの形にエッジをセットアップできる、というのがcorner swap insertionの醍醐味です。

&nbsp;

## corner swap insertionの準備

corner swap insertionでは、3手の動きを行う前に必ずbad cornerが上下に2個2個の状態にしないといけません。

`Scramble: U' R2 U R2 F2 R2 F2`

<img src="/images/2025/02/3_1.png" width="80" />

例えばこのスクランブルですが、bad cornerがUFR, UBR, UFL, DFLであり、U面に3個、D面に1個となっています。

corner swap insertionを行うには上下に2-2の状態にする必要があるので、F2もしくはB2することで2-2の状態にすることができました。

F2の状態、B2の状態はそれぞれbad edgeの位置が違うため、それぞれについてcorner swap insertionを考えることができます。

&nbsp;

## 実践例: 4b2 2e

### 例1

`Scramble: U' B2 U L2 F2 R2`

<img src="/images/2025/02/4_1.png" width="80" />

bad cornerはUFR, UBR, DFR, DFL、bad edgeはDB, DRです。

corner swap insertionをするとbad cornerの位置がUFR-UFL, DFR-DBRに変わります。つまり、corner swap insertion後にbad edgeはUFとDRにいてほしいということになります。

現在bad edgeはDB, DRであり、DRは位置を変えたくありません。また、DBはUFに位置を変えたいです。

DBをUFに持って来るにはRw2が必要です。つまりcorner swap insertionの3手のうち、DBはRw2でのみ干渉する必要があります。

また、DRは位置を変えたくありません。つまりDRがR2(w)と動いたらもう一度R2(w)と戻す必要があります。

結果として以下の3手が解答です。

```
R2 F2 Rw2
```

R2とF2ではDBエッジは干渉せず、Rw2でのみ動いています。また、DRエッジはR2とRw2でのみ干渉し、R2とR2で相殺されて位置は変わりません。

HTR解法は以下のようになります。

```
R2 F2 Rw2 U' R2 U
```

このように、corner swap insertionではまずbad edgeの現在の位置と持っていきたい位置を把握し、どうすればその位置に持っていけるかを独立に考え、最終的な3手を構築する、といったステップになります。

&nbsp;

### 例2

`Scramble: U' R2 U' R2 B2 L2 F2`

<img src="/images/2025/02/4_2.png" width="80" />

bad cornerはUFL, DFR, DFL, DBR、bad edgeはUR, DBです。

まずbad cornerが3-1の状態なので、F2して2-2の状態にします。

bad cornerはUFL, UFR, DFR, DBR、bad edgeはUR, DBとなりました。

corner swap insertionをするとbad cornerの位置がUFR-UBR, DFR-DFLに変わるため、bad edgeはUR, DFにいてほしいです。

つまり、URはURのままにしたく、DBはDFに位置変更をしたいです。

DBをDFに[R2(w), F2(w)]の動きで持っていくには、Rw2 F2(w)の動きが必須です。まずDBをRw2でUFに持っていき、その後F2(w)でDFに下ろすといった感じです。

そしてURは先程と同じく、R2したらR2で戻す、Fw2したらFw2で戻す、となります。

今回はR2 F2 R2基準とF2 R2 F2基準、両方でcorner swap insertionを考えてみましょう。

R2 F2 R2基準の場合、Rw2の次にFw2をしてしまうとURが動いてしまうのでRw2 F2で決まり、Rw2が1回のみで十分のため、結果として以下の3手が解答です。

```
Rw2 F2 R2
```

またF2 R2 F2基準の場合、一旦Fw2でURをL面に逃がし、Rw2 Fw2でURを戻しつつDBをDFにする、といった感じでセットアップもできます。

```
Fw2 Rw2 Fw2
```

最初にしたF2も含めると、以下の2つがHTR解法となります。この2つはHTR後の状態が違うため、どちらか簡単な方を選ぶことができます。

```
F2 Rw2 F2 R2 U F2 U
F2 Fw2 Rw2 Fw2 U F2 U
```

&nbsp;

### 補足情報

以下の2パターンのエッジの配置ではcorner swap insertionが使えないためご注意ください。

<img src="/images/2025/02/4_3_1.png" width="80" /><img src="/images/2025/02/4_3_2.png" width="80" />

&nbsp;

## 実践例: 4b2 4e

### 事前知識

まず、4eの状態というのは以下の4パターンあります。

|<img src="/images/2025/02/5_1_1.png" width="80" />|<img src="/images/2025/02/5_1_2.png" width="80" />|<img src="/images/2025/02/5_1_3.png" width="80" />|<img src="/images/2025/02/5_1_4.png" width="80" />|
|--|--|--|--|
|2-2 bar-slash|2-2 bars|3-1|2-2 plus|

このうち、4b2 4eトリガーであるU R2 F2 Uは下記画像のように2-2 bar-slashに相当します。つまり、corner swap insertionをすることでエッジの状態を2-2 bar-slashに持ち込むのが目標となります。

<img src="/images/2025/02/5_1_5.png" width="80" />

また上記の表のうち、2-2 bar-slashと3-1のみがcorner swap insertionが使えるパターンです。それ以外には使えません。

また、3-1であっても以下のように上下のエッジが縦に並んでいない場合も使えません。この場合はU2をして縦に並べてから行ってください。

<img src="/images/2025/02/5_1_6.png" width="80" />

&nbsp;

### 例1

`Scramble: U' R2 B2 U' L2 F2 R2`

<img src="/images/2025/02/5_2.png" width="80" />

bad cornerはUFR, UFL, DFR, DBR、bad edgeはUR, UB, DB, DLで、2-2 bar-slashの形になっています。

corner swap insertionをするとbad cornerの位置がUFR-UBR, DFR-DFLに変わります。

また、bad edgeのうち縦に並んでいるUB-DBはcorner swap insertion中必ず縦に並んだままになります。

これらを加味すると、corner swap insertion後にbad edgeはUF, DF, UR, DLにいてほしいことになります。

2-2 bar-slashではcorner swap insertionの始めの1手を必ずslashのエッジ(今回はUR or DL)が関わる回転にしないといけません。今回であればR2(w)ですね。

なぜなら、最初の1手をslashのエッジが関わらない1手にした場合(今回であればF2)、F2 R2 F2の真ん中のR2によってslashの一方のエッジの位置が変わり、2-2 bar-slashから3-1に状態が変わってしまうためです。4b2 4eトリガーのエッジの状態は2-2 bar-slashであり、3-1にしてしまってはトリガーの形にならないというわけです。

というわけで、最初の1手はR2(w)になりました。

bad edgeは現在UR, UB, DB, DLにあり、URとDLは位置をそのままにしておきたいです。そして縦に並んでいるUB-DBは1回のRw2によりUF-DFに移したいです。

これを実現するには以下の2通りの3手が挙げられます。どちらでもセットアップできます。

```
R2 F2 Rw2
Rw2 F2 R2
```

R2 F2 Rw2は最後のR2の時にUB-DBをUF-DFに持ってきており、Rw2 F2 R2の方は最初のR2でUB-DBをUF-DFに持ってきて次のF2でUF-DFの意味のない交換をしているというわけです。URとDLについてはR2とRw2で相殺され位置は変わりません。

結果として、以下の2つがHTR解法となります。

```
R2 F2 Rw2 U L2 F2 U
Rw2 F2 R2 U L2 F2 U
```

&nbsp;

### 例2

`Scramble: U' B2 R2 U' B2 R2 B2 U2`

<img src="/images/2025/02/5_3.png" width="80" />

bad cornerはUBR, UBL, DFR, DBR、bad edgeはUF, UR, UL, DBで、3-1の形になっています。

この3-1の形は縦のbad edgeペアが並んでいないためU2をするのでしたね。U2をすることで、bad cornerはUFR, UFL, DFR, DBR、bad edgeはUB, UR, UL, DBとなり、UB-DBの縦のbad edgeペアが並んでいるcorner swap insertionのできる3-1ケースとなりました。

ここからcorner swap insertionをするとbad cornerの位置がUFR-UBR, DFR-DFLに変わります。

また先ほどの通り、bad edgeのうち縦に並んでいるUB-DBはcorner swap insertion中必ず縦に並んだままになります。

これらを加味すると、corner swap insertion後にbad edgeはUF, DF, UR, DLにいてほしいことになります。

3-1の場合は、corner swap insertionの始めの1手を必ず縦のbad edgeペアが関わる回転にしないといけません。今回であればF2(w)ですね。

その理由はさっきの2-2 bar-slashのときとは逆で、F2 R2 F2の真ん中の1手が縦のbad edgeペア以外のエッジ(今回ならUR, UL)に干渉することで、3-1が2-2 bar-slashに変化してくれるからです。

というわけで、最初の1手はF2(w)になりました。

bad edgeは現在UB, UR, UL, DBにあり、URは位置をそのままにし、ULはDLに移動させたいです。そして縦に並んでいるUB-DBは1回のRw2によりUF-DFに移したいです。

ULをDLに[R2(w), F2(w)]の動きで移動させるには、Fw2 R2(w) Fw2とすればいいですね。Fw2でUL->DR、R2(w)でDR->UR、Fw2でUR->DL、と移動するからです。

ここまで来ればあとは分かりますね。Rw2が1回必要とのことなので、以下の3手がセットアップ方法です。

```
Fw2 Rw2 Fw2
```

ちなみに実は最後のFw2はF2でも問題ありません。なぜなら、Fw2 Rw2の時点でS列のbad edgeはslashの配置になっており、Fw2でもF2でもslashの配置は変わらないからです。基本的に、3-1の場合corner swap insertionの最後の1手は一層回しと二層回しどちらでもよく、その2つはHTR後の状態が違うためHTRが2つ作れてお得です。

最初にしたU2を含めると、結果として以下の2つがHTR解法となります。

```
Fw2 Rw2 Fw2 U L2 F2 U
Fw2 Rw2 F2 U L2 F2 U
```

&nbsp;

## 終わりに

corner swap insertionは慣れるまで少し難しいですが、慣れてしまえば4b2の2eだろうが4eだろうが簡単にHTRが作れてしまいます。

特に4b2 4eは何も知識がないとトリガーへのセットアップが非常に困難ですが、corner swap insertionを使えば意外とスラッとHTRが作れてしまいます。自分もこのcorner swap insertionを知ったことで4b2 4eへの苦手意識がなくなりました。

ぜひこの便利な手法を使ってHTRを大量生産してみてください。

&nbsp;

それでは。

&nbsp;