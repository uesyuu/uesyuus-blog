---
title: FMC Advent Calendar 2023 9日目
author: uesyuu
type: post
date: 2023-12-09T00:00:00+09:00
categories:
  - 未分類

---
&nbsp;

この記事は[FMC Advent Calender 2023](https://adventar.org/calendars/9097)の9日目の記事です。8日目の記事は樽川 高原さんの[DR](https://tarucube.fc2.net/e/fmc_advent_calendar_2023)でした。

&nbsp;

こんにちは、うえしゅうです。

FMCアドカレ2試技目、やっていきましょう。

&nbsp;

## スクランブルと解答

```
Scramble:
R' U' F D2 F' B R2 U B2 R2 F' R' D2 L F2 D2 F2 D2 R' L2 U2 D2 F' R' U' F
```
```
Solution:
U' R2 D' F R F2 R F2 U2 R F2 R2 F2 B2 L' B2 U2 D2 R L' B' R B' L2 R2 B2 F2 (27moves)
```

&nbsp;

## 思考過程

### EO探索

3手EOが2つ、4手EOが9個見つかりました。

そのうち探せたのは3手EO全てのノーマルのみと、4手EO 4つのみでした。
3手EOから大量に5手RZPが発生したのであまりたくさんのEOを見ることができませんでした。

探したEOは以下の通りです。

```
U' R2 D
D' F2 U
B2 U' R2 D
L2 U' R2 D
B2 D' F2 U
L2 D' F2 U
```

以下はDRが見つかったルートのみ書きます。

### U' R2 Dルート

RZPが計6個見つかり、その中でもD2 FでDR-2e3cになるものが使いやすかったです。

```
D2 F (F2 B2 R2 L2 B R' B) // 11 2c4
D2 F (B2 R' D2 R F' R F) // 11 4a4
```

結果的に上のDRを探索することになります。

### B2 D' F2 Uルート

RでDR-4e4cになったのでDRを作りましたが、ちょっと長かったです。

```
R' F' B' U2 F L2 F B2 R // 13 2c4
```

4qtですが2c4なので時間があれば探索しようかなと思ってました。

### L2 D' F2 Uルート

U2 BでDR-2e4cになります。

```
U2 B L2 R' D2 L2 U2 B R2 B // 13 4a2
```

2qtなんですが、3qtのFake HTRに近いためHalf Turnが結構多くなるんじゃないかと予想して敬遠していました。
なんですが、今ちょっと解いてみたら普通に短手数HTRたくさん作れますね、これやればよかったか。

&nbsp;

## HTR探索

RZPを書き終えた時点で30分を超過し、RZPのスイッチを6個くらい試した時点で時間が38分あたりになり、残りのスイッチを諦めて11手2c4のDRからHTRを作り始めました。

2c4はbad cornerをを同面に集めてqt回すと2c3になりますが、インバースではbad cornerがそれぞれ別の面にあります。
スイッチすると同面に来るのがインバースの時点で読めたので、スイッチしてノーマルからHTRを作り始めました。

L D2 Lで2e4c、L U2 Rで4e4cとなります。
それぞれHTRを作ってみます。

```
U' R2 D' // EO (3/3)
F (F2 B2 R2 L2 B R' B) // DR (8/11)

L D2 L B2 D2 R F2 R // HTR (8/19)
U2 F2 B2 R2 L2 // 2e2e+Slice (5/24)
or
L U2 R U2 R' B2 U2 R // HTR (8/19)
D2 F2 B2 // 2e2e+Slice (3/22)
```

下の回答は2e2eをインサートできる箇所がなかったんですが、上の回答はインサートの箇所があったためインサートしました。
また、時間が51分あたりになっていたので急いでスライスインサートを行いました。

&nbsp;

## 最終結果

```
U' R2 D' // EO (3/3)
F (F2 B2 R2 L2 B R' B) // DR (8/11)
L # D2 L # B2 D2 R F2 ^ R # // HTR (8/19)
U2 F2 B2 R2 L2 & // 2e2e+Slice (5/24)

^ = F2 B2 L2 $ F2 B2 R2 (6-3/27)
# = M, & = M', $ = M2 (10-10/27)
```

書き終わったのが残り1秒かそこらでした。
大会だとDNFだったかもしれません。

やっぱり自分はHTR探索やスライスインサートにまだ時間がかかるので、DR探索をもうちょっと早めに切り上げないといけないですね。

また、Slicey Finderに回答をかけたら-3の24手がoptimalだったようです。
R2 L2のところを消そうとどうにか頑張ってて結局消せなかったんですが、やっぱり時間が足りなかったようですね。

精進します。

次も頑張ります。

&nbsp;

## 実際のメモ

<img src="/images/2023/12/fmc-advent-calender-2023-2-1.jpg" width="600" />