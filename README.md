# Unix, Linux, Terminal
### Unix、Linuxについての違いや使用方法について学んだ内容をまとめています。

### <概要> ※原文を引用

<details><summary>①UNIX とは</summary>

- 「そんなの説明されなくても知ってるよ！」な人は適当に読み飛ばしてください。OSは「パソコンさんの人格に相当するソフト」です。パソコンさんは、中にOSを入れることによって、パソコンとして動くことができます。「これが無いとパソコンじゃねーよ」な基本ソフトです。なお「OS」という用語が世間に広まったきっかけがパソコンなので「パソコン」と書きましたが、スマホやその他のコンピュータ類でも同じです。OSと呼ばれるソフトには、いくつかの種類があります。パソコンさんの世界では、Windows、Mac、Linuxあたりが有名どころです。スマホの世界であれば、iOSやAndroidなどが主流です。パソコンさんの中にWindowsを入れれば「はーい、ボクはWindowsだよー」な人格になりますし、Linuxを入れれば「ヘーイ、ミーはLinuxさー」な人格になります。
- 以上を踏まえていろいろあるOSのひとつが「UNIX（ユニックス）」です。UNIXは昔流行ったOSです。もちろん、今でも使われていますけどね。今はUNIXっぽいOSを使いたいときはLinuxを使うのが一般的です。たまに「UNIXとLinuxの違いが分からない」という意見を見かけますが「UNIXが師匠でLinuxが弟子」と考えてください。UNIXを参考にして作られたのがLinuxです。そのためLinuxとUNIXは、ひとまとめにして「UNIX系」と呼ばれたりします。「UNIX」って単語が出てきたら「OSなんだな～
」と、お考えください。</details>


<details><summary>②Linux とは</summary>

- フリーソフトとして公開されているUNIXっぽいOSの名前。もしくはとあるカーネルの名前です。カーネルは「OSの中核部分として頑張っているソフトウェア」です。OSを1つの組織と見なした場合、カーネルさんは中心人物です。こいつがいなければ始まりません。ただし、カーネルさんだけでは組織の運営が成り立ちません。シェルやデーモンといった、その他のソフトウェアを手足のように使うことによって、はじめて組織が回ります。「カーネルさんは大事なやつだけど、カーネルさんだけではOSは成り立たない」と理解してください。カーネルさんとあれやこれやのソフトウェアが組み合わさって、1つのOSが出来あがっているのです。
- Linuxの特徴は１．フリーソフトである２．UNIXと互換性がある３．性能の低いコンピュータでも結構動くといったところでしょうかね。一言でまとめると、LinuxというのはOSの名前です。……というのが間違ってはいないけど微妙に間違っている説明です。厳密に言うと、Linuxはカーネルの名前です。どこかのスゴい人が開発したOS用のカーネル、その名前が「Linux」です。ただし、カーネルであるLinuxは、それ単体ではOSとして動作しません。OSとして動作するためには、あれやこれやのソフトウェアが必要です。ということはですよ。「よーし！パパ、新しいパソコンにLinux入れちゃうぞ～！」と宣言した時に、カーネルであるLinuxだけをポンと渡されても困ってしまいます。他に必要なソフトウェアをえっちらおっちら集めてきて、上手く組み合わせないと、パパのパソコンでLinuxは動きません。めっちゃ、大変そうですね。そこで、優しい人が、あれやこれやのソフトウェアを集めてきて、カーネルであるLinuxと一緒に配ってくれています。「これで必要なものは全部だから、これを丸ごと入れれば、そのままLinuxなOSとして使えるよ～」という優しさです。一般的に「Linux」と呼ばれているOSは、この「カーネルのLinux＋諸々のソフトウェア」のことです。早口言葉みたいですがLinuxをカーネルとして使っているOSがLinuxなのです。
- つまり、単に「Linux」と言った場合１．カーネルとしてのLinux２．OSとしてのLinuxの2つの可能性があります。これは、ちょっと紛らわしいですね。そこで、カーネルとしてのLinuxは「Linuxカーネル」と呼んだりします。一方、OSとしてのLinux（カーネルのLinux＋諸々のソフトウェア）には「Linuxディストリビューション」という呼び名が付いています。あるいは、カーネルとしてのLinuxを「狭義のLinux」と呼んだりします。「厳密に言えば『Linux』というのはカーネルの名前だよ！」ということでしょう。それに対して、OSとしてのLinuxは「広義のLinux」と呼んだりします。「ゆるく捉えれば『Linux』ってOSの名前だよね」ということでしょう。
- 最後にまとめておきます。単に「Linux」と言った場合１．カーネルとしてのLinux２．OSとしてのLinuxの2つの可能性があります。このままだと紛らわしいので、必要に応じて１．カーネルとしてのLinux：Linuxカーネル（狭義のLinux）２．OSとしてのLinux：Linuxディストリビューション（広義のLinux）と呼び分けたりします。日常会話で「Linux」と出てきたのであれば、OSとしてのLinuxを指している可能性が高いと思いますけどね。たま～にカーネルとしてのLinuxを指している場合もあります。できれば全部まとめて覚えてあげてください。まぁ「Linux」って単語が出てきたら「OS、もしくは、カーネルなんだな～」と、お考えください。</details>


<details><summary>③UNIXとLinuxの違いについて</summary>

UnixとLinuxのもっとも大きな違いは、その形態にある。
- Unixは企業が開発して、知的財産権が企業に属している（Unixという名前を使わなければ無料でも使える）
- Linuxはオープンソースでとにかく無料だし改変も配布も自由だ
これが大きな違いとなっている。

結論的には、**親戚関係でライセンスのあり方が違う**とだけ覚えておけばいいだろう。身も蓋もないが、これだけの理解でまずは構わない。
