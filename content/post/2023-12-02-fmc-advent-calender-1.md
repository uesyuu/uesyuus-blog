---
title: FMC Advent Calendar 2023 2日目
author: uesyuu
type: post
date: 2023-12-02T00:00:00+09:00
categories:
  - 未分類

---
&nbsp;

この記事は[FMC Advent Calender 2023](https://adventar.org/calendars/9097)の2日目の記事です。1日目の記事はいかのおすしさんの[素人が時間制限無限でFMCをやる](https://note.com/squid_sushi/n/n70f0ed3ba8fc)でした。

&nbsp;

こんにちは、うえしゅうです。

FMC大会の開催をきっかけにFMC熱が猛烈に上がり、最近はFMCばかり練習しています。
RZPやHTR、スライスインサートの知識なども増え、DR4年目にしてやっとやり方がわかってきたような気がしています。

また、大会きっかけでFMCを始める人も増え、アドカレ作ったらFMCがより盛り上がりそうだなと思いFMCアドカレを(勝手に)復活させました。

それでは本題に入っていきましょうか。

&nbsp;

## スクランブルと解答

```
Scramble:
R' U' F D B' U' L U B' R U' L2 F2 U2 R2 D' R2 L2 U' L2 B2 F D R' U' F
```
```
Solution:
R2 D F L F2 U R2 L' U L F2 L2 U' L2 D' B2 R2 B' F' L2 B' F D2 B' (24moves)
```

&nbsp;

## 思考過程

### EO探索

4手EOは4つ、5手EOは20個見つかりました。

EO探索では基本的に4手EOしか書かないのですが、4手EOが5個以下になりそうな時は探索をもう一巡してNISSでない5手EOを探すようにしています。

見つかった4手EOは以下の通りです。

```
L' D (B2 D)
(B) R2 D F
(B) D R2 F
(D' R2 B U)
```

また、5手EOはそれ自体がRZPのもの以外採用しないのですが、探した中で1つだけRZPの5手EOを見つけました。

```
L' B U' F R
```

ただこれは状態が良くなかったのでDRには至りませんでした。

以下はDRが見つかったルートのみ書きます。

### L' D (B2 D)ルート

これはすでにDR-4e4cのRZPとなっていたため、ノーマルとインバースそれぞれ試し以下のDRが得られました。

```
(F R2 B U2 B2 L2 F L) // 12 2c5
B2 R2 L2 F' B L // 10 4a4
F2 R2 L2 F B' L // 10 4a4
```

2c5や4a4という表記はHTR subsetsというコーナーパターン判別方法の分類法で使われる表記です。
簡単に言うと2cや4aやHTR的に合っていないコーナーの個数、末尾の5や4はqt数(何回90度回転すればHTRが完成するか)を表しています。

詳しくはこちらの記事と動画をご参照ください。

[FMC: My recommended approach for recognizing all 12 HTR corner subsets](https://www.speedsolving.com/threads/fmc-my-recommended-approach-for-recognizing-all-12-htr-corner-subsets.90515/)

[HTR subset recognition tutorial (YouTube)](https://www.youtube.com/watch?v=ijBT4xHOF1w)

[HTR subsets解説 〜DRからHTRを作るために〜](https://blog.uesyuu.com/post/2023-11-23-htr-subsets/)

今回はどれも4qt以上で使えませんでした。

### (B) R2 D Fルート

LでDR-2e3cとなるため、複数個のDRが生まれる期待が持てます。

```
L F2 U R2 L' U L // 11 4b2
L (U2 R2 U2 L' D' L) // 11 4a3
```

1つ目のDRが4b2で結構良さげです。
時間は早いですが簡単そうなのでHTR以降も作ってみました。

```
F2 L2 U' L2 D // HTR (5/16)
B2 R2 B2 ^ U2 // 3e (4/20)
^ = B2 D2 B2 L2 B2 D2 B2 L2 (8-2/26)
```

とりあえず26手ができました。ただHTR後を少し変えるとスライスインサート可能な形に書き換わりました。

```
F2 L2 U' L2 D // HTR (5/16)
U2 # F2 L2 F2 ^ // 3e (4/20)
^ = F B' R2 F' B U2 # (6-1/25)
# = E2 (4-5/24)
```

これで24手です。やったぜ。思った通りスライスで1手減りました。

取り組んだ順番的には、26手の回答を作ってそのまま次のDR探索に入った後、30分を過ぎてDR探索を終えた後にもう一度この回答を見返して書き換え、スライスインサートを行ったという流れです。

### (D' R2 B2 U)ルート

```
U2 D2 R' L U2 L F // 11 2c3
```

2c3は3qtの中でもHTRまでの手数が少ない方なので、短手数HTRに期待が持てます。

&nbsp;

## HTR探索

まずは唯一の2qt DRを探索し、先程の24手を得ます。

またスイッチして探すと25手+Sliceが得られました。

```
(B) R2 D F // EO (4/4)
L F2 U R2 L' U L // DR 4b2 (7/11)
(B2 R2 B2 U F2 D) // HTR (6/17)
(R2 B2 R' L B2 R L' U2) // Slice (8/25)
```

次に2c3のDRを探索します。

今気づいたんですが、このスケルトン23手+Sliceでしたね…。24手だと思ってた。今スライス探した感じ+0はなさそうだったので安心しました。

```
(D' R2 B2 U) // EO (4/4)
U2 D2 R' L U2 L F // DR 2c3 (7/11)
(U2 L B2 R' D2 B2 D2 B2 R) // HTR (9-1/19)
(F B' D2 F' B) // Slice (5-1/23)
```

ここまでやって時間が来ました。

&nbsp;

## 最終結果

```
(B) R2 D F // EO (4/4)
L F2 U R2 L' U L // DR 4b2 (7/11)
F2 L2 U' L2 D // HTR (5/16)
U2 # F2 L2 F2 ^ // 3e (4/20)

^ = F B' R2 F' B U2 # (6-1/25)
# = E2 (4-5/24)
```

sub25は自分の中でもめちゃくちゃ良い記録なので非常に満足しています。
いつもはsub30がやっとのレベルなので。

次も頑張ります。

&nbsp;

## 実際のメモ

<img src="/images/2023/12/fmc-advent-calender-2023-1-1.jpg" width="600" />