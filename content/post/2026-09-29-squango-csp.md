---
title: SquanGo CSPを使った効率的なCSP習得方法
author: uesyuu
type: post
date: 2026-09-30T20:00:00+09:00
categories:
  - 未分類

---
&nbsp;

こんにちは、うえしゅうです。

&nbsp;

スクエア1を解く際にインスペクション時に分析してパリティを出さない、CSP(Cube Shape Parity)という手法があります。

このCSPを学ぶのに最適なサイト「SquanGo CSP」というサイトを最近知りました。

[SquanGo CSP](https://squan-go.web.app/csp/)

このSquanGo CSPを使ってCSPを学習してみたのですが、なんと2週間程度でCSPを覚え実践で使えるまでに成長することができ、とても感動しています。

今回はこのSquanGo CSPの使い方とCSP学習の流れを詳しく説明しようと思います。

&nbsp;

## CSPの概要

まずはこちらの動画でCSPの概要を学んでください。この動画はSquanGo CSPを監修した中国のSq1erのMatt MaoのCSPチュートリアル動画のパート1です。パート2以降は見なくて大丈夫です。ちなみにYouTubeの日本語音声もあるので、そちらをオンにして見ると理解しやすいかと思います。

[learn CSP in an hour: CSP tutorial part 1 - Matt](https://youtu.be/GNmrLHw86ss?si=zlPUDIBuWjcixDS2)

この記事ではCSPの基本的な説明は行わず、上記動画を理解した前提で説明を行います。

動画で説明された通り、CSPの全体の流れは以下のようになります。

- 1: 以下のトレースを行い、それぞれのパリティの偶奇を合算した偶奇を求める
  - トレース1: 白エッジパリティ
  - トレース2: 黒エッジパリティ
  - トレース3: 白コーナーパリティ
  - トレース4: 白コーナーパリティ
  - トレース5: エッジの位置パリティ
  - トレース6: コーナーの位置パリティ
- 2: 結果の偶奇に応じて成形手順を使い分け、パリティを回避する

&nbsp;

## トレースに関する前提知識

### トレース開始位置

SquanGo CSPでは、各shapeごとにトレース開始位置が一意に決まっています。これはユニバーサルトレースポジションと呼ばれています。

ユニバーサルトレースポジションの定義は以下の通りです。

1. 基本的にはエッジの塊が一番多い部分の左端から、時計回りに分析する
2. 同じ個数のエッジの塊が複数ある場合は、エッジの塊が早くトレースできるような方を選ぶ
3. もし1がスライス不可能な位置であれば、位置を反時計回りに1コーナー分ずらす
4. muffinのみ例外

この説明は以下の動画の以下タイムスタンプで説明されているので、わからない場合はそちらを参照ください。日本語音声もあります。

[an update to my CSP tutorials - Matt (7:48 where do I start tracing? より開始)](https://youtu.be/q3GED6kFNOs?si=mmaJh-JL6XCZXg9i&t=468)

ただし、僕の場合muffinのトレース開始位置がどうにも納得がいかず、これだけ以下のように変更しました。SquanGo標準ではmuffinは例外扱いされていますが、自分のmuffinのトレース開始位置はユニバーサルトレースポジションに則っています。

<img src="/images/2026/09/muffin_before.png" width="200" /> <img src="/images/2026/09/muffin_after.png" width="191" />

&nbsp;

### トレースの準備

トレースに入る前に、UD面のどちらの面を上にしてトレースするかを決めます。

SquanGo CSPの場合、必ずエッジが多い方の面をU面にしてトレースを開始してください。もしそれで中段が解くときと逆になっていても構いません。そういう場合はトレース後に正位置に持ち替えてソルブ開始すれば問題ないです。

エッジの数がUD面ともに同じ場合(どちらも4つ)は、特に持ち替えなくて大丈夫です。

&nbsp;

### エッジパリティ・コーナーパリティ

動画で説明のあった通り、ここでは各パーツに対して3色分分析し、その3色がパリティかどうかを判断します。

その際にパリティとなりうる隣接色2色の並び「赤・緑」「青・オレンジ」を、自分は「ペア色」と呼んでいます。

分析時にペア色があったら光って見えるイメージ、ペア色でない隣接色は光ってないイメージで分析すると自分はわかりやすかったです。

#### 3色パリティ判断のもう一つの方法

3色パリティ判断について、動画では対面色ペアの位置からそのどちらかの色を消し、残った2色で判断するという方法でした。

しかし自分はShota君から教わった以下の別のやり方で3色パリティ判断を行っています。

- 1色目、2色目が対面色 → +1
  - → 2色目、3色目がペア色/非ペア色 → +1/0
- 1色目、2色目が隣接色でペア色/非ペア色 → +1/0
  - → 2色目、3色目が対面色/隣接色 → 0/+1

この方法だと3色目を見ている時に覚えておくことが少し減るのでやりやすく、おすすめです。動画の方法かShota君の方法か、どちらか好きな方法を選んでください。

&nbsp;

### 位置パリティ

位置パリティはエッジ・コーナーのそれぞれ1,3,5,7番目のUD面色を見て偶奇を判断するものです。

実は、shapeごとに位置パリティで分析するパーツは一意に決まっているのです。

例えば、scallopの位置パリティでは以下の赤色のパーツを見ればよいです。

<img src="/images/2026/09/scallop_position_parity.png" width="150" />

そのため、各shapeごとにどのパーツを見ればよいかを事前に暗記しておくことをおすすめします。これをするだけで位置パリティの分析が格段に楽になります。

&nbsp;

### evilnessパリティ

evilnessパリティとは、SquanGo CSPで導入された新しい7つ目のパリティです。

まずはこの動画のevilnessパリティのタイムスタンプの部分をご覧ください。日本語音声もあります。

[an update to my CSP tutorials - Matt (01:31 the 7th parity より開始)](https://youtu.be/q3GED6kFNOs?si=1wa7j8ZptWPPUWRk&t=91)

簡単にまとめると次のようになります。

- トレース結果の偶奇(even/odd)によって成形手順が変わる
- even/oddの2つの成形手順は「goodな手順/badな手順」に分かれることが多いが、そのどちらがeven/oddになるかはケースごとにバラバラで覚えにくい
- それぞれの成形に「evilnessパリティ」を設定しトレース結果にそのパリティを加算することで、「goodな手順→even、badな手順→odd」に必ずなる

このようにevilnessパリティを用いると都合がいいので使っているという感じです。個人的にはこの発想は革命的だなと思います。

evilnessパリティはその成形の2つのshapeを現実世界の物に置き換えてストーリーを作ることで覚えます。このストーリーは自分で考える必要はなく、既にSquanGo CSPに書かれています。

例えばscallop/scallopを例に出します。scallopとはホタテのことです。「ホタテを2つ食べるとアレルギーになる」のでscallop/scallopはevil caseでありevilnessパリティは有り、とのことです。ストーリーはハチャメチャなものも多いですが、面白いので覚えやすいと思います。

<img src="/images/2026/09/evilness_parity_story.png" width="400" />

普通の成形であればnice(良)/evil(悪)のどちらか、right/leftやgood/badのある成形はnice(良)/evil(悪)/follow(普通)/invert(逆)のどれかになります。

後者については以下のような分類で決定されます。基本的にgoodやrightが良いもの、badやleftが悪いもの、という認識です。

<table>
  <tr>
    <th>good〇〇 or right〇〇</th><th>bad〇〇 or left〇〇</th><th>evilnessパリティ</th>
  </tr>
  <tr>
    <td>nice case</td><td>nice case</td><td>nice case</td>
  </tr>
  <tr>
    <td>evil case</td><td>evil case</td><td>evil case</td>
  </tr>
  <tr>
    <td>nice case</td><td>evil case</td><td>follow case</td>
  </tr>
  <tr>
    <td>evil case</td><td>nice case</td><td>invert case</td>
  </tr>
</table>

最終的に、CSPの全体の流れは以下のようになります。

- 1: 以下のトレースを行い、それぞれのパリティの偶奇を合算した偶奇を求める
  - トレース1: 白エッジパリティ
  - トレース2: 黒エッジパリティ
  - トレース3: 白コーナーパリティ
  - トレース4: 白コーナーパリティ
  - トレース5: エッジの位置パリティ
  - トレース6: コーナーの位置パリティ
  - トレース7: evilnessパリティ
- 2: 結果が偶数ならgoodな手順、奇数ならbadな手順を回し、パリティを回避する

&nbsp;

## 実行に関する前提知識

### 手順のgood/bad

先程のevilnessパリティの項目でお話したように、evenならgoodな手順、oddならbadな手順が選ばれます。

この手順のgood/badの基準については以下の動画のタイムスタンプで説明があるのでそちらをご覧ください。日本語音声もあります。

[learn CSP in an hour: CSP tutorial part 1 - Matt (05:34 "good" and "bad" cases より開始)](https://youtu.be/GNmrLHw86ss?si=uUehrJQXQNXcTSMN&t=334)

まとめると以下の通りです。

<table>
  <tr>
    <th>goodな手順</th><th>badな手順</th>
  </tr>
  <tr>
    <td>短い手順</td><td>長い手順</td>
  </tr>
  <tr>
    <td>基本となる手順</td><td>基本から外れた手順</td>
  </tr>
  <tr>
    <td>2genで解ける手順</td><td>3genで解ける手順</td>
  </tr>
  <tr>
    <td>activityがfrontslashである手順</td><td>activityがbackslashである手順</td>
  </tr>
</table>

各成形ごとのgood手順/bad手順についての説明はSquanGo CSPの以下の部分に書いてあります。

<img src="/images/2026/09/alg_good_bad.png" width="400" />

### activityとは

先程「activityが・・・」と書かれていましたが、これについて説明します。

activityについては以下の動画のタイムスタンプで説明があるのでそちらをご覧ください。日本語音声もあります。

[an update to my CSP tutorials - Matt (04:04 "activity": / and \ より開始)](https://youtu.be/q3GED6kFNOs?si=aVg03-MmB3-upprr&t=244)

まとめると、shape内の特定の部分に着目し(activity)、それがfrontslash上にあるか(/)、backslash上にあるか(\\)でgood/badを判断する、といったものです。

activityの例をいくつか出します。

<table>
  <tr>
    <th>shape</th><th>activity</th><th>frontslash状態</th><th>backslash状態</th>
  </tr>
  <tr>
    <td>pair</td><td>エッジペアから引いたスラッシュ</td><td><img src="/images/2026/09/pair_frontslash.png" width="100" /></td><td><img src="/images/2026/09/pair_backslash.png" width="100" /></td>
  </tr>
  <tr>
    <td>L</td><td>直角から引いたスラッシュ</td><td><img src="/images/2026/09/L_frontslash.png" width="100" /></td><td><img src="/images/2026/09/L_backslash.png" width="100" /></td>
  </tr>
</table>

&nbsp;

## CSPで覚えることまとめ

一旦ここで情報を整理します。

CSPを学ぶうえで覚えることは以下の通りです。

- 各shapeについて
  - トレース開始位置
  - 位置パリティの位置
- 各成形について
  - evilnessパリティ
  - good/badの手順
  - good/badの手順の開始位置(activityなど)

各shapeに関しては事前準備ですぐ覚えられるとして、各成形についての項目をSquanGo CSPでは効率的に覚えることができます。

&nbsp;

## CSPの習得方法

ここからはSquanGo CSPを使ってCSPを習得するための一連の流れを説明します。

その前に以下の準備を行います。

記事の最初の方で自分はmuffinのトレース開始位置を変更したと言いましたが、あれをするとevilnessパリティが一部変わってしまいます。そのため、自分で設定し直してevilnessパリティを変更した設定ファイルを作成しました。

また、自分は白がU面のため、それも設定を行いました。

これからCSPを学習する皆さんは設定とかはめんどくさいと思うので、以下の4つの設定ファイルを用意しました。

自分のやり方にあった設定ファイルをインポートして学習を始めてください。

<table>
  <tr>
    <th>muffinのトレース開始位置</th><th>U面色</th><th>JSONファイルのリンク</th>
  </tr>
  <tr>
    <td>デフォルトのまま</td><td>黒</td><td><a href="https://drive.google.com/file/d/1jX_Q4ccNPZnSH4eGutV9mTTLyPAE_NNS/view?usp=sharing">JSONファイルのリンク</a></td>
  </tr>
  <tr>
    <td>デフォルトのまま</td><td>白</td><td><a href="https://drive.google.com/file/d/1R3smGOIrB6pqp9QydXm2dAd9L51zB4NM/view?usp=sharing">JSONファイルのリンク</a></td>
  </tr>
  <tr>
    <td>トレース開始位置を変更</td><td>黒</td><td><a href="https://drive.google.com/file/d/1fitAq-mhKknhVq5Ih8aHm4uER2oOn8w-/view?usp=sharing">JSONファイルのリンク</a></td>
  </tr>
  <tr>
    <td>トレース開始位置を変更</td><td>白</td><td><a href="https://drive.google.com/file/d/1VCMUeLLvj5HaS3s_yw-4ymmEUzpHyL4w/view?usp=sharing">JSONファイルのリンク</a></td>
  </tr>
</table>

インポートは左上の3本線アイコンから「Import Data」を選ぶとインポートができます。

<img src="/images/2026/09/training_import.png" width="700" />

ではCSP学習の仕方を説明します。

まず学びたい成形を1つ決めます。今回はHighest Probabilityの並び順で一番上にあるleft 4-2/pairにしましょう。

その成形のeven手順(good手順)、odd手順(bad手順)を回し、何をしているのかを理解します。大体1〜3手で3手成形に帰着しているので、3手成形までのルートを理解しようとするとわかりやすいです。

下の部分に「good alg/bad alg」がどの3手成形に帰着させているのかが書いてあるので、それも理解の助けになります。

今回はgood alg→scallop/scallop、bad alg→shield/shieldになる、というものでした。

<img src="/images/2026/09/training_alg_good_bad.png" width="700" />

次に、その成形のevilnessパリティをストーリーから覚えます。これも下に書いてあります。

今回はfollow caseでした。followということはright 4-2/pairがniceでleft 4-2/pairがevilということですね。

ストーリーはこんな感じでした。

「普通だ。なぜなら、4-2/pairという組み合わせこそが、そもそも2つの4-2にevilnessをもたらした原因だからだ。」

これだけ見ると何言ってんの？って感じですが、実は4-2/Lと4-2/lineはどちらもinvert caseでこの4-2/pairだけfollow caseなんですよね。つまり入口のこいつのせいで他の4-2がinvertになってしまったんだ、ってことみたいです。

まあ、覚えにくかったら自分なりにストーリーを考えてみてください。自分は単純に「4-2はpairだけ普通で他は逆」と覚えてます。

<img src="/images/2026/09/training_evilness_parity_story.png" width="700" />

次にその成形に学習中フラグを立てます。成形のチェックマークアイコンをクリックすると黄色(学習中)に、もう一度クリックすると緑(学習済み)に、もう一度クリックすると元に戻る仕様になっています。

<img src="/images/2026/09/training_learning_flag.png" width="700" />

次にトレーナーに移って実際のスクランブルで練習します。左上の3本線アイコンからTrainer→Timer Trainingを選択します。

<img src="/images/2026/09/training_timer_training.png" width="700" />

次に左上の〇〇 case selectedの部分を押し、case選択画面に移ります。すると先程学習中にしたleft 4-2/pairだけが黄色になっているのがわかります。

Selectを押して、プルダウンメニューのSelect Learningを押すと、学習中のcaseが全て選択されます。バツボタンで閉じて練習を開始しましょう。

<img src="/images/2026/09/training_select_learning.png" width="700" />

最初はタイマーを使わずにトレースするだけでも良いと思います。スクランブルをクリックするとCale式の分析結果が表示されるので、自分のトレース結果がそれと合っているかを確認することができます。

<img src="/images/2026/09/training_cale_tracer.png" width="700" />

トレースに慣れてきたらタイマーを使って練習しましょう。普通のタイマーに加えて、インスペクション時間とソルブ時間の両方を測れるオプションもあるので、自分はそっちを推奨します。

もしトレーナーで解いてパリティが出てしまったらトレースにミスがあったということなので、スクランブルを一つ戻ってCale式の分析結果を確認しましょう。右上の左矢印ボタンで前のスクランブルに戻れます。

<img src="/images/2026/09/training_prev_scramble.png" width="700" />

ここまでが1つの成形に対する学習方法です。これを各成形について繰り返していく感じです。

自分はこれを以下のような感じで学習していきました。

1. 昨日以前に学んだ成形は学習済みフラグを立てておく
2. 今日学ぶ成形について、先程の手順で学んでいく(3つ学んだとする)
3. 学んだ成形3つについて学習中フラグを立て、トレーナーで「Select Learning」を選択し学習中の3つの成形を練習する
4. 最後にトレーナーで「Select Learning + Learned」を選択し、学習中+学習済みの成形を全て選択して練習する

SquanGo CSPは使い方動画もあるので、その動画も参考になるかと思います。日本語音声もあります。

[We changed CSP forever. - Matt](https://youtu.be/XVcp4yG54sk?si=hNHsWj31JQ1bK3J2)

&nbsp;

## SquanGoのその他の機能

実はSquanGo CSPはSquanGoというサイトの一部機能でして、CSP学習の他にもいろいろな機能があります。

[SquanGo](https://squan-go.web.app/)

まずはOBLトレーナー・PBLトレーナーです。

OBLやPBLの練習はもちろんですが、OBLトレーナーはCO手順やEO手順の練習、PBLトレーナーはCP手順やEP手順の練習にも使えて便利です。

[OBL/PBL Trainer - SquanGo](https://squan-go.web.app/oblpbl/)

次にスクエア1の手順探索ツール「Croissant」です。

これはweb上で使えるスクエア1の手順探索ツールで、何回か使ってみましたがレスポンスも早くとても使いやすかったです。

EP手順でどうにも良い手順が見つからない時にこれを使って自分好みの手順を探してみるのもありかと思います。

[Croissant - SquanGo](https://squan-go.web.app/croissant/web/)

最後にスクエア1の成長ロードマップです。

各タイム帯で自分が何をすべきか、何を覚えるべきかが書かれていてとても役立ちます。

各項目には動画のリンクやスプレッドシートのリンクなどが添付されていて、このロードマップを見るだけでスクエア1の成長の仕方が完璧にわかると思います。

[Progression Roadmap - SquanGo](https://squan-go.web.app/resources/roadmap/)

&nbsp;

## 終わりに

SquanGo CSPを使ったCSP学習方法について解説してきました。

このサイトを知ったのは今年の春頃でしたが、その時から「いつかCSPを学ぶ時はこのサイトを使ってみよう」とずっと思っていました。

そして実際に使って学んでみると本当に使いやすく2週間でCSPを覚えられてしまい、自分でもかなり衝撃でした。

もしスクエア1のパリティに苦しんでいる方がいましたら、このSquanGo CSPでCSPを学びパリティをこの世から無くしてみてはいかがでしょうか？

&nbsp;

&nbsp;

それでは。

&nbsp;