---
title: FMC Advent Calendar 2024 18日目
author: uesyuu
type: post
date: 2024-12-18T00:00:00+09:00
categories:
  - 未分類

---
&nbsp;

この記事は[FMC Advent Calender 2024](https://adventar.org/calendars/10322)の18日目の記事です。

&nbsp;

こんにちは、うえしゅうです。

最後の3試技目やっていきましょう。

&nbsp;

## スクランブルと解答

```
Scramble:
R' U' F D2 B L2 U2 L2 F U2 B' D2 B2 L2 B U B' R D U' B U' B' D2 R' U' F
```
```
Solution:
L' D U2 F R L' D2 B2 U L D2 B2 U2 L U2 L2 R F2 R' F2 U2
(21moves)
```

&nbsp;

## 思考過程

### EO探索

FB軸が4EOだったため4手以下のEOは相当たくさんありました。ただ、時間の関係上半分くらいのEOはDR探索まで移れませんでした。

```
R2 D' B
D' R2 B
D2 R D' B
D R2 D2 B
R D' R B
U2 D L2 F
U2 L' D F
D U2 L2 F
D L2 U2 F
L' D U2 F
(R B)
(F2 R B)

他10個 (DR探索に移れなかったもの)
```

&nbsp;

### DR探索

4手以下のEOがたくさんあったため、RZPを4手以内に絞って探しました。また、3手以下のEOに限っては逆側も探しました。

```
EO: (R B)

(U L)
(B2 U' R), (R2, U L2 B2 U2 D' R) // 10, 4b5
(B2 R' U)
U R

EO: D R2 D2 B (RZP)
U2 D2 L F2 U' F2 U // 11, 4b3

EO: R D' R B (RZP)

EO: D L2 U2 F (RZP)

EO: L' D U2 F (RZP)
R L' D2 B2 U // 9, 4b2 4e
F2, D2 F2 R' L D // 9, 4b2 4e
F2, D2 B2 R L' U // 9, 4b2 4e
```

2手EOと3手EOを逆側まで探しきって、ノーマルの4手EOを探しきったタイミングで9手の4b2 4eが見つかりました。

ここで、これ以上DRを探すよりもこのDRのoptimalを探しにいったほうがいいと考え、DR探索をストップしHTR探索に入りました。

また、例によってDRのバリエーションも書いておき時間が余ったとき用に探せるようにしました。

&nbsp;

### HTR探索

```
L' D U2 F // EO, RZP
R L' D2 B2 U // DR, 4b2 4e
```

とりあえずこのDRをHTR探索していきます。

コーナーは3-1ですが、DR最後のUを逆にすると2-2になり、さらにパリティでもありません。その際エッジは3-1なのでcorner swap insertionを使います。

```
U2, F2 D2 B2 R' F2 U2 L // HTR

U2, F2 D2 B2 R' B2 U2 R // HTR
B2 * U2 D2 // 3e
* = B2 R2 B2 U2 B2 R2 B2 U2 // LS (22)
```

HTRから3eスケルトンを引き、インサートで22手LSを引きました。幸先いいですね。

+13手はoptimalの可能性も十分にあるのですが、4b2だからoptimalはもっと短いだろうと踏んでHTR探索を続行します。

続いて、2c3を介した4qtを探していきます。4b2 4eは4qtがoptimalの可能性が半分くらいあるらしいのでちゃんと探します。

コーナーが3-1になっている状態でR'し、B2するとsquare-squareの2c3 4eの6手トリガーになります。これはHTRが4つ作れるパターンなのでラッキーですね。

```
R' B2 R' U2 R' U2 F2 L // HTR
R' B2 R' U2 R' D2 B2 R // HTR
R' B2 R' D2 R' B2 D2 R // HTR

R' B2 R' D2 R' F2 U2 L' // HTR
B2 D2 B2 L2 // LS (21)
```

4つのバリエーションのうちの1つから21手LSが引けました。+12手もoptimalの可能性が相当ありますが、時間もあるのでもう少しだけ粘ってみます。

次はRして2c3 4eにしてからスイッチしてみます。本当はここでNISS traceして2c3 4eトリガーに近いか見たほうがいいのですが、めんどくさくてやっていませんでした。

スイッチ後はF2で2c3 4eの5手トリガーになりましたがパリティだったので、U2をつけて2パターンのHTRを作成しました。

```
R (F2 U2 R F2 L B2 L) // HTR

R (U2 F2 R F2 L B2 L') // HTR
(B2 D2 F2) // LS (20)
```

なんと20手LSが引けました。流石に+11手はoptimalだろうと思い、すぐにスライスインサートを行います。ただ結果は+1で21手でした。

ここでもう50分を超えていたので21手でほぼ確ですが、時間もあるのでもう一つのバリエーションもHTR探索してみます。

```
L' D U2 F' // EO
D2 F2 R' L D // DR, 4b2 4e
```

まず普通のcorner swap insertionから。

```
F2 D2 F2 R' F2 D2 R // HTR

F2 D2 B2 R' D2 F2 R // HTR
D2 B2 U2 F2 D2 // LS (21)
```

いきなり21手LSが見つかりました。ただすでに21手が出ているのでこれは使わずもう少し探します。

次はDR最後のDを逆にしてコーナーを3-1にしてからLして2c3 4eにします。ノーマルは特に何もなかったのでスイッチして探します。

```
D2, L (F2 U2 R F2 R D2 R) // HTR
D2, L (U2 F2 R F2 R D2 R) // HTR
```

特に何もなし。

ここで時間が来て、21手が最終回答となりました。

&nbsp;

## 最終結果

```
L' D U2 F // EO, RZP (4/4)
R L' D2 B2 U // DR, 4b2 4e (5/9)
R * (U2 F2 R F2 L ** B2 L') // HTR (8/17)
(B2 D2 F2) // LS (3/20)

* = w, ** = M' (+1/21)
```

Nissyでも確認しましたが、この+12手が全てのバリエーションの中で最短のoptimalのようでした。一安心。

&nbsp;

FMCアドカレ2024、最終結果は以下の通りです。

25, 26, 21 = mean 24.00

なんとmean PRタイ！21手が強すぎました。

今年はFMCについて結構成長できた年になったので、来年も練習してもう少し成長し日本の他のDRerに少しでも追いつけるように頑張りたいと思います。

&nbsp;

最後になりますが、FMCアドカレに参加していただいた皆さん、本当にありがとうございます。

まだ枠が少し余っているので、参加していただけたら嬉しいです。

&nbsp;

それでは。

&nbsp;

## 実際のメモ

<img src="/images/2024/12/fmc-advent-calender-2024-3-1.jpg" width="600" />