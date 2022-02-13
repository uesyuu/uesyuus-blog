---
title: スタックタイマーとcsTimerの繋げ方
author: uesyuu
type: post
date: 2019-02-07T12:37:03+00:00
url: /?p=448
categories:
  - その他

---
こんばんは。  
今までずっとスタックタイマーとPCやiPhoneを繋げて計測ができたらいいなあと思っていたのですが、その方法がやっとわかったので備忘録として記事にしておきます。

## PC

まずPCとスタックタイマーの接続についてです。

### 用意するもの

  * スタックタイマー　<a href="https://store.tribox.com/products/detail.php?product_id=1762" target="_blank" rel="noopener noreferrer">triboxリンク</a>
  * ステレオミニプラグケーブル(3極オス-3極オス)　<a href="https://www.amazon.co.jp/dp/B07L3XBWRM/" target="_blank" rel="noopener noreferrer">Amazonリンク</a>
  * 2.5mm-3.5mm変換ケーブル(3極オス-3極メス)　<a href="https://www.amazon.co.jp/dp/B01E8ULN12/" target="_blank" rel="noopener noreferrer">Amazonリンク</a>

3極というのは端子の種類のことです。それぞれの端子の特徴を表にまとめました。

<table>
  <tr>
    <th>
      端子
    </th>
    
    <th>
      端子の特徴
    </th>
    
    <th>
      性質
    </th>
    
    <th>
      備考
    </th>
  </tr>
  
  <tr>
    <td>
      2極
    </td>
    
    <td>
      黒線が1本
    </td>
    
    <td>
      モノラル
    </td>
    
    <td>
    </td>
  </tr>
  
  <tr>
    <td>
      3極
    </td>
    
    <td>
      黒線が2本
    </td>
    
    <td>
      ステレオ
    </td>
    
    <td>
      PCでヘッドホンとマイクが別端子になっているものはこれ
    </td>
  </tr>
  
  <tr>
    <td>
      4極
    </td>
    
    <td>
      黒線が3本
    </td>
    
    <td>
      ステレオ+マイク
    </td>
    
    <td>
      スマホは大体これ
    </td>
  </tr>
</table>

僕のPCはヘッドホンとマイクが別端子なので3極のケーブルで繋がりました。もしPCのヘッドホンとマイクが同じ端子の場合、後述する4極-3極変換ケーブルが必要となります。  
また、スタックタイマーは端子が2.5mmのため、普通のステレオミニプラグケーブルと繋ぐには2.5mm-3.5mm変換ケーブルが必要となります。  
またタイマーについては純正Gen2、純正Gen4、YuXin Timer v2で動作確認済みです。MoYuTimerは繋いでみるとバグが起こって変な動作をしてしまうので使わない方がいいと思います。

### 接続方法

まずスタックタイマーと2.5mm-3.5mm変換ケーブル、ステレオミニプラグケーブルを繋ぎ、PCのマイク入力に挿します。  
次にPCのブラウザでcsTimerを立ち上げ、オプション(歯車マーク)→timer→entering in times withの項目をstackmatに切り替えます。すると「csTimerが次の許可を求めています」というポップアップが出てくるので、許可を押します。最後にスタックタイマーの電源をオンにし、画面に0.00と表示されたら接続成功です。

## iPhone

続いてiPhoneとスタックタイマーの接続についてです。

### 用意するもの

  * スタックタイマー　<a href="https://store.tribox.com/products/detail.php?product_id=1762" target="_blank" rel="noopener noreferrer">triboxリンク</a>
  * ステレオミニプラグケーブル(3極オス-3極オス)　<a href="https://www.amazon.co.jp/dp/B07L3XBWRM/" target="_blank" rel="noopener noreferrer">Amazonリンク</a>
  * 2.5mm-3.5mm変換ケーブル(3極オス-3極メス)　<a href="https://www.amazon.co.jp/dp/B01E8ULN12/" target="_blank" rel="noopener noreferrer">Amazonリンク</a>
  * 4極-3極変換ケーブル(4極オス-3極メス)　<a href="https://www.amazon.co.jp/dp/B01BV916AQ" target="_blank" rel="noopener noreferrer">Amazonリンク</a>
  * Lightning-3.5mmイヤホンジャックアダプタ　<a href="https://www.amazon.co.jp/dp/B01LZ4RPHI/" target="_blank" rel="noopener noreferrer">Amazonリンク</a>

PCと異なる点は、iPhoneの端子がLightningでありヘッドホン・マイクが同端子になっている事です。なので、まずLightningを4極の端子に変換し、さらに4極を3極に変換する必要があります。

### 接続方法

まずiPhone、Lightning-3.5mmイヤホンジャックアダプタ、4極-3極変換ケーブル、ステレオミニプラグケーブル、2.5mm-3.5mm変換ケーブル、スタックタイマーの順で繋ぎます。4極-3極変換ケーブルはマイクの端子とヘッドホンの端子に分かれていますが、マイクの端子の方に繋いでください。  
次にiPhoneの設定→Safari→カメラとマイクのアクセス、をオンにします  
そしてブラウザ(Safari)でcsTimerを立ち上げ、PCと同じようにオプション(歯車マーク)→timer→entering in times withの項目をstackmatに切り替えます。すると「csTimerがマイクへのアクセスを求めています」というポップアップが出てくるので、許可を押します。最後にスタックタイマーの電源をオンにし、画面に0.00と表示されたら接続成功です。  
もし接続ができなかった場合は、設定のカメラとマイクのアクセスを一度オフにしてもう一度オンにすると接続できるかもしれないです。  
ちなみに僕はiPhoneには接続できませんでした。誰か教えて。  
以上が接続の方法になります。Androidスマホでは動作確認を行っていないので動くかはわからないです。