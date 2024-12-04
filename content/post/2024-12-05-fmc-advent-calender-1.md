---
title: FMC Advent Calendar 2024 5日目
author: uesyuu
type: post
date: 2024-12-05T00:00:01+09:00
categories:
  - 未分類

---
&nbsp;

この記事は[FMC Advent Calender 2024](https://adventar.org/calendars/10322)の5日目の記事です。4日目の記事はY.Yさんの[3試技目](http://cubyy.blog.fc2.com/blog-entry-17.html)でした。

&nbsp;

こんにちは、うえしゅうです。

&nbsp;

今年もFMCアドカレを開催してみました。

参加してくださった皆さんありがとうございます。

今年は自分としては初めてDRでao12 sub25をしたりと成長の感じられた年でした。

そんな成長した自分がFMCアドカレでどこまで結果を残せるのか、やっていきたいと思います。

&nbsp;

今回は1試技目を行いました。

&nbsp;

## スクランブルと解答

```
Scramble:
R' U' F D R2 U F L' F2 U2 F R2 B2 D2 R U2 L2 F2 U2 B2 R U2 B2 R' U' F
```
```
Solution:
L' D' B R' F' U' F2 B2 R2 L2 U' F U' R2 U2 B2 R2 B2 D R2 U L2 B2 L2 R2
(25moves)
```

&nbsp;

## 思考過程

### EO探索

まず始めに自分は各軸を見てEOの個数だけ書き下すのですが、今回はFB軸/RL軸/UD軸がそれぞれ10/6/6でした。

カスですね。

やはりというか、4手以下のEOは以下の3つしか見つかりませんでした。

```
L' B D2 R
L' D' B R
(R) D2 B R
```

ちなみにNissyによると4手EOは11個あったみたいです。

R LとかR U2 LみたいなEOトリガーは探しづらいですねー。

```
B R' B2 L (4)
B L' D2 R (4)
D2 B R (R) (4)
L' B D2 R (4)
L' D' B R (4)
(L' B R L) (4)
(L' B' R L) (4)
(F D' R2 U) (4)
(F U' B2 D) (4)
(F' D' R2 U) (4)
(F' U' B2 D) (4)
```

&nbsp;

### DR探索

4手EOが3個だけだったのでRZPを6手以内に上限を上げて探し始めました。

するとあまり時間がなく、NISS EOに関しては手を付けられずEO2つのRZPしか探せませんでした。

見つけたRZPとDRは以下の通りです。

```
EO: L' B D2 R

R2 U B
R2 D F, U R2 L2 B2 U' D2 F // 13 2c5

EO: L' D' B R

R2 F, F2 U' F2 B2 R2 L2 U' F // 12 2c3 4e
R2 F, (L2 D B2 U' R2 D B) // 12 0c0 6e
R2 D
R2 D F, D B2 R2 L2 U2 D F // 13 4b2 6e
R2 B' D
```

13手4b2はエッジがいい位置関係だったので短めなHTRがありましたが、先が続かないのでボツ。

```
R2 D F, D B2 R2 L2 U2 D F // 13 4b2 6e
U2 F2 U' R2 D // HTR
```

12手0c0はコーナーは神なのですが6eなのが厄介です。4a1 4eにしてからNISSを試しましたが先が続かずボツ。

結局開始30分が経って、12手2c3 4eを選ぶことにしました。

&nbsp;

### HTR探索

まずDで4b2 2eにする愚直なルートを探してみました。

```
D' R2 F2 R2 L2 U' F2 U' // HTR
R2 F2 R2 D2 // FR
B2 R2 F2 R2 F2 // LS (29)
```

29手スライス残し、まあ悪いですが保険ということで。FR後5手かかる場合はやっぱりカスHTRなんでしょうね。

&nbsp;

次にDして4b2 2eにしてからスイッチしてみます。

```
D (R2 L2 B2 L2 U' R2 U') // HTR
(L2 B2 L2 D2 F2 D2) // LS (25)

D (R2 B2 L2 B2 U' R2 U) // HTR
(L R' U2 L R U2) // LS (26)
```

25手スライス残しがありました。DR後13手なのでワンチャンoptimalですね。

&nbsp;

最後に、DRの最後のmoveを逆に回したパターンもやってみました。

```
F2, B2 D' (F2 R2 U' L2 U) // HTR 
```

HTRがあまり良くなかったのでボツ。

&nbsp;

開始50分経って、結局25手スライス残しをスライスインサートで探し、+0手で25手でFinishしました。

&nbsp;

## 最終結果

```
L' D' B R' // EO (4/4)
F' // RZP (1/5)
U' F2 B2 R2 L2 U' F // DR 2c3 4e (7/12)
D * (R2 L2 B2 L2 U' R2 U' *) // HTR (8/20)
(L2 B2 L2 D2 * F2 D2) // LS (6-1/25)

* = w (0/25)
```

幸いにもこれがoptimal finishでした。よかったーーーーー。

最近大会練習とかで他の競技を主にやってるのでFMCは2ヶ月ぶりとかだったんですが、そこそこな記録が出て良かったです。

FMC(というかDR)は他が落ち着いたタイミングでまたちゃんとやりたいと思っているので、いつか常時sub25ができるようになれればいいなあと思っています。

&nbsp;

FMCアドカレはまだ割と空いているので、よかったら参加してみてはいかがでしょうか。

&nbsp;

それでは。

&nbsp;

## 実際のメモ

<img src="/images/2024/12/fmc-advent-calender-2024-1-1.jpg" width="600" />