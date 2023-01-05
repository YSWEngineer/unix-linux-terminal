# 💻 ドットインストール UNIXコマンド入門
### UNIX互換OSで使える、基本的なコマンドを学んでいきます。

<details><summary>#01 UNIXコマンドの学習をしていこう</summary>

UNIX は Windows や macOS と同じく OS の一種で、インターネットを構成するサーバー用によく使われます。

また UNIX ですが、一時期オープンソースで配布されたこともあって、 無料の互換 OS がたくさん登場して広まったという経緯があります。広まった互換 OS には BSD や Minux など他にもたくさんあるのですが、特に広く使われているのが Linux です。

この Linux ですが、独自の設定や構成で配布している企業や団体がたくさんあって、その配布形式のことをディストリビューション (Distribution) と呼びます。

有名なディストリビューションにはいくつかあって、代表的なのは Red Hat Enterprise Linux 、 CentOS 、 Debian 、 Ubuntu そして今回使っていく Alpine など、他にもたくさんあります。

これらは微妙に異なる OS ではあるのですが、基本的なコマンドは POSIX という規格で統一されているので、このレッスンではそうした標準的なコマンドについて見ていきましょう。

ちなみに macOS も UNIX を源流に持つ OS なので、今回学習していくコマンドは macOS のターミナルでも使うことができます。

それから Windows や macOS のようにマウスで操るようなインターフェースを GUI (Graphical User Interface) 、コマンドだけで操るインターフェースを CUI (Character-based User Interface) というのですが、こちらの GUI のほうが分かりやすいのに、なぜわざわざ CUI を覚えなくてはいけないのかと思うかもしれません。

その理由は CUI のほうが効率的に作業ができるのと、自動化がしやすいからです。

たとえば GUI でフォルダを 100 個作らないといけないとなったときに、右クリックして New Folder として ... という作業を 100 回繰り返さないといけないのですが、 CUI だとコマンド一行で済んでしまいます。また、別の日に同じ作業をしなくてはいけなくなったとき、 CUI だとこのコマンドをスクリプトにしておいて実行するだけ OK ですし、 100 個のフォルダではなくて 300 個だったとしても、ここだけを変更すれば OK になります。

効率的に開発を進めるためにもコマンドを使った操作には慣れておくといいので、このレッスンで学習していきましょう。
### 要点
- UNIX：Windows や macOS と同じく OS の一種。
- Linux：UNIXとの互換OS。Linuxの他にもBSDやMinuxなどがある。
- GUI,CUI：マウスで操るようなインターフェースをGUI(Graphical User Interface)、コマンドだけで操るインターフェースをCUI(Character-based User Interface)という。
- Distribution(ディストリビューション)：配布形式の名称。</details>


<details><summary>#02 シェルコマンドを打ち込んでみよう</summary>

今回ですが、動画の横に Linux の実行環境を用意しておきました。また、コマンドを受け付けるための特殊なシェルというプログラムが稼働している状況です。

マシンに設定された日時を知るにはdateとしてあげます。

```bash
dotinstall:~ $ date
Mon Jul 25 15:57:11 JST 2022
```

それから UNIX では大文字、小文字が厳密に区別されます。したがって、Date としてもうまくいきませんので注意しましょう。

```bash
dotinstall:~ $ Date
bash: Date: command not found # 「commandは見つかりませんでした」と表示される
```

次に今月のカレンダーを表示する cal というコマンドも使ってみましょう。

```bash
dotinstall:~ $ cal
     July 2022
Su Mo Tu We Th Fr Sa
                1  2
 3  4  5  6  7  8  9
10 11 12 13 14 15 16
17 18 19 20 21 22 23
24 25 26 27 28 29 30
31
```

稼働しているシェルですが、矢印キーの上下でコマンドの履歴をさかのぼることができます。

コマンドが打たれた状態でエンターキーとするとこのコマンドを実行しますが、そうではなくて、やっぱり次のコマンドを打ちたいという場合、 Control キーを押しながらCキーを押せばこのコマンドを実行せずに新しいプロンプトに移ることができます。

```bash
dotinstall:~ $ cal^C
```

途中まで打ったコマンドをクリアしたい場合、 Control キーを押しながらUキーを押せばクリアすることができます。

画面全体をいったんクリアしたいという場合は clear エンターキーとするか、 Control キーを押しながらLキーでも OK です。
### 要点
- シェル：コマンドを受け付けるためのプログラム。
- プロンプト：入力待ちになっている箇所に表示されている初めの部分。今回の環境では、ログインユーザー名、コロン、$マークが表示されている。
- date：マシンに設定された日時を表示する。
- cal：今月のカレンダーを表示する。
- 上矢印キー、下矢印キー：コマンドの履歴を遡ったり、戻ることができる。
- Ctrl + U：途中まで打ったコマンドをクリア。
- Ctrl + C：コマンドを実行せずに新しいプロンプトに移る。
- Ctrl + L：画面全体をクリアする。</details>


<details><summary>#03 ディレクトリ構成を理解しておこう</summary>

大元となるディレクトリは / で表すのですが、 root ディレクトリと呼ばれています。

ディレクトリの下にあるディレクトリをサブディレクトリと呼びます。

サブディレクトリはどれもシステムを動かすのに必要なものですが、よく使うのは etc,home,var あたりです。

etc は各種設定ファイルを格納する場所(設定ファイル)、 home はユーザーが好きに使える場所(ユーザーのhomeディレクトリ)、そして var はアプリケーションが管理するデータを格納する場所(データファイル等、Web,DB,LOG)で、ウェブサイトやデータベースのデータ、 LOG ファイルなどを格納するのに使います。

なお、 home ディレクトリにはユーザーごとにサブディレクトリを作ることができて、今回は dotinstall ユーザー用のディレクトリが設定されています。また、 dotinstall ユーザーでログインした場合、ログイン直後はこのディレクトリにいるので、ここを dotinstall ユーザーの home ディレクトリと呼びます。

他にも bin(実行ファイル) や sbin(管理者用の実行ファイル) にはコマンド用の実行ファイルが入っていたり、 tmp(一時ファイル用) は一時ファイルを格納する場所ですが、このあたりは最初いじることはないので、興味があれば追々調べていけば良いでしょう。

ディレクトリをコマンドの中で表現する場合、ふたつの方法があります。

ひとつが絶対 PATH という書き方で、ルートディレクトリである / から始めます。

たとえば etc だったら /etc 、home内のdotinstallであればディレクトリの区切りは / になるので /home/dotinstall といった表現ですね。

なお、現在ログインしているユーザーの home ディレクトリはよく使われるので、特殊な PATH が用意されています。 ~ (チルダ) という記号で表すのでこの点にも注意しておいてください。

次に相対PATHは、今どこにいるかによって表現が異なります。

たとえば、今この dotinstall ディレクトリにいた場合、現在のディレクトリは . で示します。そして、ひとつ上のディレクトリは .. で表現します。root ディレクトリはさらにそのひとつ上なので、 ../.. となります。

コマンドによる操作ではディレクトリ間を移動したり、ディレクトリを指定して特定の操作をするので、どちらの方法も使いこなせるようになっておきましょう。
### 質問：ディレクトリはファイルのことですか？
回答：ファイルやディレクトリを入れる箱のようなものです。

ディレクトリとはファイルをいれる入れ物のような物とお考えいただけると良いかなと思います。

もちろんディレクトリの中にはファイルだけでなくディレクトリもいれることができます。
### 要点
- ディレクトリ構成：ディレクトリはフォルダと同じ。CUIではディレクトリと表現されることが多い。
- 絶対PATH：ディレクトリをコマンドの中で表現する方法。ルートディレクトリである/から始める。
- ~(チルダ)：ユーザーのhomeディレクトリを表す記号。
- 相対PATH：ディレクトリをコマンドの中で表現する方法。ホームディレクトリである.から始める。</details>


<details><summary>#04 絶対PATHでディレクトリを移動しよう</summary>

シェル内でディレクトリの移動をしてみましょう。

ちなみにこちらのプロンプトには現在の位置が表示されていると説明しましたが、ログイン直後はユーザーの home ディレクトリなので、前回見たように ~ で表現されているのが分かります。

また、今いるディレクトリを表示するコマンドもあって、 pwd (print working directory) としてあげます。

```bash
dotinstall:~ $ pwd # ~はhomeディレクトリを指す
/home/dotinstall # rootディレクトリの中のhomeディレクトリの中のdotinstallディレクトリにいる
```

root ディレクトリの中の home ディレクトリの中の dotinstall ディレクトリにいるのが分かります。

先ずは、絶対パスで移動してみましょう。移動するにはcd(change directory)コマンドを使います。ルートディレクトリは/なので移動するにはcd /とします。

```bash
dotinstall:~ $ cd / # cdコマンドで、ルートディレクトリに移動(ルートディレクトリは/で表示)
dotinstall:/ $ # プロンプトが/に変わっている
dotinstall:/ $ pwd # pwdコマンドで現在いる場所を表示させる
/ # 今いる場所は/(ルートディレクトリ)だとわかる
```

次はetcディレクトリに移動します。

絶対パスで cd /etc とすればいいのですが、この環境で使っているシェルではタブによる補完が効くので /et としたあとにタブキーを押すと補完してくれます。

なお、ディレクトリの補完をすると、最後に / が付きますが、そのあとに何も書く必要がないときはつけてもつけなくても構いません。

```bash
dotinstall:/ $ cd /etc/
dotinstall:/etc $ # プロンプトが/etcに変わり、移動できていることを確認できる
```

次にhomeディレクトリに戻ってみましょう。

タブキーの補完を使いながら、 cd /ho タブ、 do タブ、とすると補完ができます。

ただ、ディレクトリに戻るには cd ~ としても OK ですし、実は home ディレクトリに戻る操作はよく行うので、 cd とするだけでも OK です。

```bash
dotinstall:/etc $ cd
dotinstall:~ $
```

それから補完の対象が複数ある場合、タブキーを二回押すことで一覧を見ることができます。

例えばroot ディレクトリ直下のどこかに移動したいと思った場合、 cd/ としたあとにタブを一回押しても複数候補があるので何も表示されませんが、もう一度押すと、こうですね、このように一覧で教えてくれます。

```bash
dotinstall:~ $ cd / # tabを2回押すと候補を一覧で表示してくれる
.dockerenv         index.js           package-lock.json  srv/
bin/               lib/               package.json       sys/
command.js         media/             proc/              tmp/
dev/               mnt/               root/              usr/
etc/               node_modules/      run/               var/
home/              opt/               sbin/              verify.js
```

あとはこの一覧を見ながら、たとえば dev ディレクトリにいきたかったら、 d タブとすれば OK です。

このようにタブによる補完は便利なので、使いこなせるようになっておきましょう。

```bash
# 処理を実行したくないときは control + C で中断する
dotinstall:~ $ cd /dev/^C
```

### 質問：cdの後にスペースが必要ですか？
回答：スペースはコマンドのオプションを区切るために使われます。

UNIXコマンドにおいて半角スペースは、コマンドとそのオプション（引数）との「区切り文字」としての意味を持っています。

コンピューターは人間のように柔軟に理解はしてくれないので、コマンドの後には必ず半角スペースを入れ、オプションと区別しなければならないのです。

> 具体的には、cd/etc/　や　cd / etc / とするとうまくいきませんが、 cd /etc/ と言うように、cdの後にだけスペースを入れるときちんと移動します。
> 

こちらの例で説明しますと、もし `cd/etc/` と書くと、コンピューターは「`cd/etc/` というコマンドだ」と理解してしまいます。当然そのようなコマンドはないため正しく動作しません。

また、`cd / etc /` と書くと、コンピューターは「`/` と `etc` と `/` のどこに移動するのか分からない」となり、エラーとなってしまいますね。
### 要点
- pwd：今いるディレクトリを表示する。
- cd：ディレクトリに移動する。
- TABキー補完：2回押すと候補を一覧で表示してくれる。</details>


<details><summary>#05 相対PATHでディレクトリを移動しよう</summary>

- 相対パスでディレクトリを移動する
    - 一つ上のhomeディレクトリは相対パスでは`..`
    
    ```bash
    dotinstall:~ $ pwd # 今いるディレクトリを表示する
    /home/dotinstall
    dotinstall:~ $ cd .. # .. で一つ上のディレクトリに移動する
    dotinstall:/home $
    dotinstall:/home $ cd .. # .. でさらに一つ上のディレクトリに移動する
    dotinstall:/ $ # rootディレクトリにいる状態
    ```
    
- ここで、rootディレクトリの下のetcディレクトリに移動したかった場合
    - 自分のディレクトリを表す`.`に`/etc`を繋げるか、今いるディレクトリの下のディレクトリ名を指定する。
    
    ```bash
    dotinstall:/ $ cd etc # etcディレクトリに移動する
    dotinstall:/etc $ # プロンプトを確認するとetcディレクトリに移動したことがわかる
    ```
    
- ユーザーのhomeディレクトリに戻る
    - `cd` returnキーを押す。
    
    ```bash
    dotinstall:/etc $ cd # ユーザーのhomeディレクトリに戻る
    dotinstall:~ $
    ```
    
- etcディレクトリに一気に移動する
    - 一つ上のディレクトリ、homeディレクトリに移動→homeディレクトリの上のrootディレクトリに移動→rootディレクトリの下のetcディレクトリに移動する。`cd ../../etc`
    
    ```bash
    dotinstall:~ $ cd ../../etc
    dotinstall:/etc $
    ```
    
- どのディレクトリに移動できるかわからなくなってしまった場合、tabキーによる補完を使用すると良い。
    
    ```bash
    dotinstall:/etc $ cd ../ # tabキーを2回押すと現在位置から移動可能なディレクトリが表示される
    .dockerenv         index.js           package-lock.json  srv/
    bin/               lib/               package.json       sys/
    command.js         media/             proc/              tmp/
    dev/               mnt/               root/              usr/
    etc/               node_modules/      run/               var/
    home/              opt/
    ```
    
- 相対パスは慣れないとやや難しく感じるのですが、tabキーによる補完を使用して使いこなせるようにしましょう。
### 要点
- .：一つ下のディレクトリに移動する。
- ..：一つ上のディレクトリに移動する。
- TABキーによるディレクトリ確認：tabキーを2回押して、現在位置から移動可能なディレクトリが表示される。</details>


<details><summary>#06 lsコマンドを使ってみよう</summary>

- ディレクトリの中身を見る。
    - `ls`(list)コマンドを使う。
    
    ```bash
    dotinstall:~ $ ls # lsコマンドでディレクトリの中身を確認する
    dotinstall:~ $ # 何も表示されないのはhomeディレクトリに何もないから
    ```
    
- 隠しファイルが存在していることもある。
    - lsにオプションを付ける。オプションは-で付ける。今回は-aとする。
    - UNIXでは、`.`で始まるファイルやディレクトリがlsコマンドでは表示されない隠しファイルになるので以下のような表示になっている。
    - 最初の二つはディレクトリ自身と、一つ上のディレクトリを示す。
    - .bashrcは設定ファイルで、簡単にいじられないように隠しファイルになっていると理解すること。
    - 青色はファイルではなく、ディレクトリという意味。
    
    ```bash
    dotinstall:~ $ ls -a
    .        ..       .bashrc  .config
    ```
    
    ![lsコマンドを使ってみよう.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6e83747b-3ce6-4a63-b6c8-1b7715097da5/ls%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%88%E3%82%99%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%A6%E3%81%BF%E3%82%88%E3%81%86.png)
    
- lsコマンドの他のオプション。
    - -lで詳細な情報を見ることができる。
    - オプションは複数指定することもできる。
        - `-l -a`
        - `-la`
        - `-al`
        
        と、-aを並べたり、くっつけたり、順不同で-laや-alと書いても同じ意味になる。
        
    
    ```bash
    dotinstall:~ $ ls -al
    total 20
    drwxr-sr-x    1 dotinsta wheel         4096 Aug 22 11:29 .
    drwxr-xr-x    1 root     root          4096 Sep 23  2020 ..
    -rw-r--r--    1 root     root            23 Sep 23  2020 .bashrc
    drwx--S---    3 dotinsta wheel         4096 Aug 22 11:29 .config
    ```
    
- lsにさらにディレクトリを渡して他のディレクトリの情報を見ることができる。今回はetcディレクトリの中身を見てみる。
    
    ```bash
    dotinstall:~ $ ls -al /etc/
    total 216
    drwxr-xr-x    1 root     root          4096 Aug 22 11:29 .
    drwxr-xr-x    1 root     root          4096 Aug 22 11:29 ..
    -rw-r--r--    1 root     root             7 May 29  2020 alpine-release
    drwxr-xr-x    1 root     root          4096 Sep 23  2020 apk
    drwxr-xr-x    3 root     root          4096 Sep 23  2020 ca-certificates
    -rw-r--r--    1 root     root          5613 Jun 18  2020 ca-certificates.conf
    drwxr-xr-x    2 root     root          4096 May 29  2020 conf.d
    drwxr-xr-x    2 root     root          4096 May 29  2020 crontabs
    -rw-r--r--    1 root     root            89 May 29  2020 fstab
    -rw-r--r--    1 root     root           693 Sep 23  2020 group
    -rw-r--r--    1 root     root           682 May 29  2020 group-
    -rw-r--r--    1 root     root            13 Aug 22 11:29 hostname
    -rw-r--r--    1 root     root           178 Aug 22 11:29 hosts
    drwxr-xr-x    2 root     root          4096 May 29  2020 init.d
    -rw-r--r--    1 root     root           570 May 29  2020 inittab
    -rw-r--r--    1 root     root          1748 Feb  9  2020 inputrc
    -rw-r--r--    1 root     root            54 May 29  2020 issue
    -rw-r--r--    1 root     root           309 Aug  9  2020 localtime
    drwxr-xr-x    2 root     root          4096 May 29  2020 logrotate.d
    drwxr-xr-x    2 root     root          4096 May 29  2020 modprobe.d
    -rw-r--r--    1 root     root            15 May 29  2020 modules
    drwxr-xr-x    2 root     root          4096 May 29  2020 modules-load.d
    -rw-r--r--    1 root     root           283 May 29  2020 motd
    lrwxrwxrwx    1 root     root            12 Aug 22 11:29 mtab -> /proc/mounts
    drwxr-xr-x    8 root     root          4096 May 29  2020 network
    drwxr-xr-x    2 root     root          4096 May 29  2020 opt
    -rw-r--r--    1 root     root           164 May 29  2020 os-release
    -rw-r--r--    1 root     root          1233 Sep 23  2020 passwd
    -rw-r--r--    1 root     root          1172 May 29  2020 passwd-
    drwxr-xr-x    7 root     root          4096 May 29  2020 periodic
    -rw-r--r--    1 root     root           238 May 29  2020 profile
    drwxr-xr-x    1 root     root          4096 Sep 23  2020 profile.d
    -rw-r--r--    1 root     root          1865 May 29  2020 protocols
    -rw-r--r--    1 root     root            54 Aug 22 11:29 resolv.conf
    -rw-r--r--    1 root     root            65 May 22  2020 securetty
    -rw-r--r--    1 root     root         14464 May 29  2020 services
    -rw-r-----    1 root     shadow         454 Sep 23  2020 shadow
    -rw-r-----    1 root     shadow         422 May 29  2020 shadow-
    -rw-r--r--    1 root     root            48 Sep 23  2020 shells
    drwxr-xr-x    1 root     root          4096 May 29  2020 ssl
    -rw-r--r--    1 root     root          3941 May 25  2020 sudo.conf
    -rw-r--r--    1 root     root          6169 May 25  2020 sudo_logsrvd.conf
    -rw-r--r--    1 root     root          3228 Sep 23  2020 sudoers
    drwxr-x---    2 root     root          4096 Sep 23  2020 sudoers.d
    -r--r-----    1 root     root          3174 May 25  2020 sudoers.dist
    -rw-r--r--    1 root     root            53 May 29  2020 sysctl.conf
    drwxr-xr-x    2 root     root          4096 May 29  2020 sysctl.d
    drwxr-xr-x   13 root     root          4096 Sep 23  2020 terminfo
    -rw-r--r--    1 root     root          5306 May 22  2020 udhcpd.conf
    ```
    
- 水色は別のファイルやディレクトリへのリンクを表している。
### 要点
- ls：ディレクトリの中身を確認する。
- -a：隠しファイルや隠しディレクトリを表示する。
- -l：詳細な情報を見ることができる。
- オプションの複数指定：オプションは、並べたり、くっつけたり、順不同で書くこともできる。</details>


<details><summary>#07 コマンドの詳細を調べてみよう</summary>

- どのようなオプションが使用できるかは、`ls --help`で確認できる。
    
    ```bash
    dotinstall:~ $ ls --help
    BusyBox v1.31.1 () multi-call binary.
    
    Usage: ls [-1AaCxdLHRFplinshrSXvctu] [-w WIDTH] [FILE]...
    
    List directory contents #各オプションの内容が表示されている
    
            -1      One column output
            -a      Include entries which start with .
            -A      Like -a, but exclude . and ..
            -x      List by lines
            -d      List directory entries instead of contents
            -L      Follow symlinks
            -H      Follow symlinks on command line
            -R      Recurse
            -p      Append / to dir entries
            -F      Append indicator (one of */=@|) to entries
            -l      Long listing format
            -i      List inode numbers
            -n      List numeric UIDs and GIDs instead of names
            -s      List allocated blocks
            -lc     List ctime
            -lu     List atime
            --full-time     List full date and time
            -h      Human readable sizes (1K 243M 2G)
            --group-directories-first
            -S      Sort by size
            -X      Sort by extension
            -v      Sort by version
            -t      Sort by mtime
            -tc     Sort by ctime
            -tu     Sort by atime
            -r      Reverse sort order
            -w N    Format N columns wide
            --color[={always,never,auto}]   Control coloring
    ```
    
- 他のオプションを試してみる。
- オプションは大文字小文字が区別されるので、大文字のSを使ってetcディレクトリの中身をサイズ順に並び替えてみる。
    
    ```bash
    dotinstall:~ $ ls -alS /etc/
    total 216
    -rw-r--r--    1 root     root         14464 May 29  2020 services
    -rw-r--r--    1 root     root          6169 May 25  2020 sudo_logsrvd.conf
    -rw-r--r--    1 root     root          5613 Jun 18  2020 ca-certificates.conf
    -rw-r--r--    1 root     root          5306 May 22  2020 udhcpd.conf
    drwxr-xr-x    1 root     root          4096 Aug 22 11:29 .
    drwxr-xr-x    1 root     root          4096 Aug 22 11:29 ..
    drwxr-xr-x    1 root     root          4096 Sep 23  2020 apk
    drwxr-xr-x    3 root     root          4096 Sep 23  2020 ca-certificates
    drwxr-xr-x    2 root     root          4096 May 29  2020 conf.d
    drwxr-xr-x    2 root     root          4096 May 29  2020 crontabs
    drwxr-xr-x    2 root     root          4096 May 29  2020 init.d
    drwxr-xr-x    2 root     root          4096 May 29  2020 logrotate.d
    drwxr-xr-x    2 root     root          4096 May 29  2020 modprobe.d
    drwxr-xr-x    2 root     root          4096 May 29  2020 modules-load.d
    drwxr-xr-x    8 root     root          4096 May 29  2020 network
    drwxr-xr-x    2 root     root          4096 May 29  2020 opt
    drwxr-xr-x    7 root     root          4096 May 29  2020 periodic
    drwxr-xr-x    1 root     root          4096 Sep 23  2020 profile.d
    drwxr-xr-x    1 root     root          4096 May 29  2020 ssl
    drwxr-x---    2 root     root          4096 Sep 23  2020 sudoers.d
    drwxr-xr-x    2 root     root          4096 May 29  2020 sysctl.d
    drwxr-xr-x   13 root     root          4096 Sep 23  2020 terminfo
    -rw-r--r--    1 root     root          3941 May 25  2020 sudo.conf
    -rw-r--r--    1 root     root          3228 Sep 23  2020 sudoers
    -r--r-----    1 root     root          3174 May 25  2020 sudoers.dist
    -rw-r--r--    1 root     root          1865 May 29  2020 protocols
    -rw-r--r--    1 root     root          1748 Feb  9  2020 inputrc
    -rw-r--r--    1 root     root          1233 Sep 23  2020 passwd
    -rw-r--r--    1 root     root          1172 May 29  2020 passwd-
    -rw-r--r--    1 root     root           693 Sep 23  2020 group
    -rw-r--r--    1 root     root           682 May 29  2020 group-
    -rw-r--r--    1 root     root           570 May 29  2020 inittab
    -rw-r-----    1 root     shadow         454 Sep 23  2020 shadow
    -rw-r-----    1 root     shadow         422 May 29  2020 shadow-
    -rw-r--r--    1 root     root           309 Aug  9  2020 localtime
    -rw-r--r--    1 root     root           283 May 29  2020 motd
    -rw-r--r--    1 root     root           238 May 29  2020 profile
    -rw-r--r--    1 root     root           178 Aug 22 11:29 hosts
    -rw-r--r--    1 root     root           164 May 29  2020 os-release
    -rw-r--r--    1 root     root            89 May 29  2020 fstab
    -rw-r--r--    1 root     root            65 May 22  2020 securetty
    -rw-r--r--    1 root     root            54 May 29  2020 issue
    -rw-r--r--    1 root     root            54 Aug 22 11:29 resolv.conf
    -rw-r--r--    1 root     root            53 May 29  2020 sysctl.conf
    -rw-r--r--    1 root     root            48 Sep 23  2020 shells
    -rw-r--r--    1 root     root            15 May 29  2020 modules
    -rw-r--r--    1 root     root            13 Aug 22 11:29 hostname
    lrwxrwxrwx    1 root     root            12 Aug 22 11:29 mtab -> /proc/mounts
    -rw-r--r--    1 root     root             7 May 29  2020 alpine-release
    ```
    
- より詳細な使い方についてはマニュアルを見ることができる。
    - man lsでlsについての詳細なマニュアルが表示される。
    
    ```bash
    dotinstall:~ $ man ls
    LS(1P)                     POSIX Programmer's Manual                    LS(1P)
    
    PROLOG
           This manual page is part of the POSIX Programmer's Manual.  The Linux
           implementation of this interface may differ (consult the corresponding
           Linux manual page for details of Linux behavior), or the interface may
           not be implemented on Linux.
    
    NAME
           ls — list directory contents
    
    SYNOPSIS
           ls [−ikqrs] [−glno] [−A|−a] [−C|−m|−x|−1] \
               [−F|−p] [−H|−L] [−R|−d] [−S|−f|−t] [−c|−u] [file...]
    
    DESCRIPTION
           For each operand that names a file of a type other than directory or
           symbolic link to a directory, ls shall write the name of the file as
           well as any requested, associated information. For each operand that
           names a file of type directory, ls shall write the names of files
           contained within the directory as well as any requested, associated
           information. Filenames beginning with a <period> ('.') and any
           associated information shall not be written out unless explicitly
           referenced, the −A or −a option is supplied, or an implem--More-- (3% of 38335 bytes)
    ```
    
    - ↑この画面ではspaceキーで次のページに行くことができて、Qキー(quitのq)を押すと終了することができる。
### 質問：「ls --help」が 「illegal option -- -」と表示されてしまいます。
回答：macOS の zsh では --help を使うことはできません。

オンラインターミナルで採用している Linux 系統の OS と、 macOS が採用している BSD 系統の OS で、搭載されている ls コマンドのバージョンが違うようです。

BSD 版の ls コマンドでは `--help` オプションは利用できないので、 `man ls` としてマニュアルを見てみてください。
### 要点
- ls --help：使用可能なオプションを確認できる。
    - ※macOS の zsh では --help を使うことはできません。
        
        オンラインターミナルで採用している Linux 系統の OS と、 macOS が採用している BSD 系統の OS で、搭載されている ls コマンドのバージョンが違うようです。
        
        BSD 版の ls コマンドでは `--help` オプションは利用できないので、 `man ls` としてマニュアルを見てみてください。
        
- man ls：より詳細なマニュアルを表示する(manコマンド)。</details>


<details><summary>#08 ワイルドカードを使ってみよう</summary>

- ls -lで表示した情報の中から特定の項目だけを表示するにはワイルドカードという仕組みが使える。
    - 拡張子が.confだけの項目を抜き出す。
        - .を除く0文字以上の任意の文字列は*(アスタリスク)で表現できるので、`ls -l *.conf` と書く。
        
        ```bash
        dotinstall:/etc $ ls -l *.conf # *は0文字以上の任意の文字列を表現、.confだけの項目を表示
        -rw-r--r--    1 root     root          5613 Jun 18  2020 ca-certificates.conf
        -rw-r--r--    1 root     root            54 Aug 22 11:29 resolv.conf
        -rw-r--r--    1 root     root          3941 May 25  2020 sudo.conf
        -rw-r--r--    1 root     root          6169 May 25  2020 sudo_logsrvd.conf
        -rw-r--r--    1 root     root            53 May 29  2020 sysctl.conf
        -rw-r--r--    1 root     root          5306 May 22  2020 udhcpd.conf
        ```
        
        - ?マークは任意の1文字を表すので、`ls -l s?????` と書くと、sで始まる6文字の項目だけ表示。
        
        ```bash
        dotinstall:/etc $ ls -l s????? # sから始まる6文字の項目を表示
        -rw-r-----    1 root     shadow         454 Sep 23  2020 shadow
        -rw-r--r--    1 root     root            48 Sep 23  2020 shells
        ```
        
        - [ ] は任意の1文字か範囲を示すことができて、例えば `[ps]?????` とすれば、pかsで始まる6文字の項目だけを表示。
        
        ```bash
        dotinstall:/etc $ ls -l [ps]????? # pまたはsから始まる6文字の項目を表示
        -rw-r--r--    1 root     root          1233 Sep 23  2020 passwd
        -rw-r-----    1 root     shadow         454 Sep 23  2020 shadow
        -rw-r--r--    1 root     root            48 Sep 23  2020 shells
        ```
        
        - [ ] を使った時は、- で範囲を表せるので、`[f-h]*` とするとf g h で始まる項目だけを表示。
        
        ```bash
        dotinstall:/etc $ ls -l [f-h]* # fからh、要するにf,g,hから始まる項目を表示
        -rw-r--r--    1 root     root            89 May 29  2020 fstab
        -rw-r--r--    1 root     root           693 Sep 23  2020 group
        -rw-r--r--    1 root     root           682 May 29  2020 group-
        -rw-r--r--    1 root     root            13 Aug 23 15:14 hostname
        -rw-r--r--    1 root     root           178 Aug 23 15:14 hosts
        ```
        
        - 任意の文字列のどれかという指定をする場合は、`{ }` を使用する。※カンマの後ろに空白を入れないこと。
        
        ```bash
        dotinstall:/etc $ ls -l {sh,ho}* # 文字列の中に「sh」または「ho」で始まる項目を表示 # カンマの後ろには空白を入れてはいけない
        -rw-r--r--    1 root     root            13 Aug 23 15:14 hostname
        -rw-r--r--    1 root     root           178 Aug 23 15:14 hosts
        -rw-r-----    1 root     shadow         454 Sep 23  2020 shadow
        -rw-r-----    1 root     shadow         422 May 29  2020 shadow-
        -rw-r--r--    1 root     root            48 Sep 23  2020 shells
        ```
        
### 要点
- *：(ワイルドカードにおいて)任意の文字列を表現できる。
- ?：(ワイルドカードにおいて)任意の1文字を表す。
- [ ]：(ワイルドカードにおいて)任意の1文字か、範囲を表す。
- {, }：(ワイルドカードにおいて)任意の文字列のどれかを表す。,(カンマ)で区切ったその後ろには空白を入れないこと。</details>


<details><summary>#09 ファイルを操作してみよう</summary>

- ファイルを作成するには、touchコマンドを使用する。touchコマンドはファイルの更新日時を更新するためのものだが、ファイルがない場合は、空のファイルを作成する。UNIXは不親切でファイルを作成しました、というメッセージは表示されない。エラーがなければ正常に処理されたことを意味するので、慣れておくこと。

```bash
dotinstall:~ $ touch index.html
dotinstall:~ $ # エラーがなければ正常に処理されたことを意味する
```

```bash
dotinstall:~ $ ls # lsコマンドはディレクトリの中身を確認する
index.html # lsコマンドで確認すると、index.htmlファイルが作成されたことが確認できる
```

- ファイルをコピーして別のファイルを作成したい場合は、cp(copy)コマンドを使用する。index.htmlをprofile.htmlにコピーする作業を行う。

```bash
dotinstall:~ $ cp index.html profile.html # index.htmlをprofile.htmlにコピー
dotinstall:~ $ ls # lsコマンドでディレクトリの中身を確認
index.html    profile.html
```

- ファイル名を変更したい場合、mv(move)コマンドを使用するが、同じ場所に違う名前で移動させることで名前の変更ができる。
    - profile.htmlをabout.htmlに移動させる

```bash
dotinstall:~ $ mv profile.html about.html # profile.htmlをabout.htmlに移動する
dotinstall:~ $ ls
about.html  index.html # profile.htmlがabout.htmlに名前が変更
```

- ファイルを削除したい場合、rm(remove)コマンドを使用する。ちなみにUNIXの場合、ゴミ箱のような仕組みはないので、一度削除したファイルを復元することはできない。そのため、削除には十分注意すること。

```bash
dotinstall:~ $ rm about.html # rmコマンドでabout.htmlファイルを削除する
dotinstall:~ $ # エラー表示がないので削除に成功
dotinstall:~ $ ls
index.html # about.htmlファイルが削除されていることを確認
```

### 質問：なぜ移動させると名前が変わるのですか？
    
回答：mv profile.html about.html とすると profile.html を削除して同じ内容の about.html というファイルを配置するので、結果的に名前が変わったことになります。

`mv`コマンドは元のファイルを削除して同じ内容のファイルを指定先に配置するコマンドです。

`mv profile.html about.html` とすると profile.html を削除して同じ内容のファイルを about.html という名前で配置するので、結果的に名前が変わったことになります。
###　要点
- touch：ファイルの日時を更新するためのものだが、ファイルがない場合はファイルを作成する。
- cp：ファイルをコピーして別のファイルを作成する。
- mv：元のファイルを削除して同じ内容のファイルを指定先に配置する。
- rm(remove)：ファイルを削除する。削除されたファイルは復元できないことに注意。</details>


<details><summary>#10 ディレクトリを操作してみよう</summary>

- 作成したファイルをディレクトリを作成してその中に入れたい場合、
    - ディレクトリの作成：`mkdir ディレクトリ名` とする。

```bash
# 事前にindex.htmlファイルを作成した状態でディレクトリを作成する
dotinstall:~ $ mkdir mysite # mkdir ディレクトリ名 でディレクトリを作成
dotinstall:~ $ ls
index.html  mysite
```

- 作成したファイルをディレクトリに移動させるには、mvコマンドを使用する。

```bash
dotinstall:~ $ mv index.html mysite/ # index.htmlファイルをmysiteディレクトリに移動させる
dotinstall:~ $ ls
mysite # index.htmlファイルはmysiteディレクトリに移動したことが確認できる
dotinstall:~ $ ls mysite/ # mysiteディレクトリの状態を確認する
index.html # mysiteディレクトリの中には移動したindex.htmlファイルを確認できる
```

- ディレクトリの名前を変更したい場合も、mvコマンドを使用する。

```bash
dotinstall:~ $ mv mysite/ myprofile # mvコマンド 変更したいディレクトリ名 新しいディレクトリ名 の並びでreturnキーを押す
dotinstall:~ $ ls # ディレクトリを確認
myprofile # mysite から myprofile へと名前が変更していることがわかる
```

- ディレクトリの削除は rmdir を使用する。
    - が、このままでは実行できない。
    
    ```bash
    dotinstall:~ $ rmdir myprofile/ # rmdirコマンドでmyprofileディレクトリを削除する。
    rmdir: 'myprofile/': Directory not empty # myprofileディレクトリの中身が空ではないため削除できない、と表示。
    ```
    
    - ディレクトリの中にあるファイルを削除してから、ディレクトリを削除する。
    
    ```bash
    dotinstall:~ $ ls myprofile/ # myprofileディレクトリの中身を確認。
    index.html # myprofileディレクトリ内にindex.htmlファイルがあることを確認。
    dotinstall:~ $ rm myprofile/index.html # rmコマンドでmyprofileディレクトリの中にあるindex.htmlファイルを削除する。
    dotinstall:~ $ rmdir myprofile/ # rmdirコマンドでmyprofileディレクトリを削除する。
    dotinstall:~ $ ls # lsコマンドでディレクトリを確認する。
    dotinstall:~ $ # ディレクトリが表示されないので、myprofileディレクトリが削除されたことが確認できる。
    ```

**※ファイルの削除と同様、ディレクトリの削除においても復元することができないので注意すること。**
### 要点
- mkdir(make directory)：ディレクトリを作成する。
- rmdir(remove directory)：ディレクトリを削除する。rmコマンドと異なり、ディレクトリにしか使用できない。また、ディレクトリが空の場合にしか使用できない。</details>


<details><summary>#11 深い階層のディレクトリを操作してみよう</summary>

- mysite の中に css ディレクトリを作成してみる。
    - その場合、一つずつ作成しても良いが、 -p オプションで深い階層まで一気に作成することができる。
    
    ```bash
    dotinstall:~ $ mkdir -p mysite/css # mysiteディレクトリとその中にcssディレクトリを作成する。
    dotinstall:~ $ ls # lsコマンドでディレクトリを確認する。
    mysite # mysiteディレクトリを確認。
    dotinstall:~ $ ls mysite # lsコマンドでmysiteディレクトリ内を確認する。
    css # cssディレクトリを確認。
    dotinstall:~ $ ls css # lsコマンドでcssディレクトリを確認。
    ls: css: No such file or directory # cssディレクトリの中にファイルは何もないと表示。
    ```
    
- cssディレクトリ内にファイルを作成する。
    
    ```bash
    dotinstall:~ $ touch mysite/css/styles.css # touchコマンドでmysiteディレクトリの中のcssディレクトリの中にstyles.cssファイルを作成する。
    dotinstall:~ $ ls mysite/css # lsコマンドでmysiteディレクトリの中のcssディレクトリの中身を確認。
    styles.css # styles.cssファイルを確認。
    ```
    
- ここで、mysiteディレクトリを丸ごとコピーしたい場合、
    - `cp mysite/ myprofile` と書いても実行できない。
    
    ```bash
    dotinstall:~ $ cp mysite/ myprofile # cpコマンドでmysiteディレクトリをコピーし、それをmyprofileと名付ける。
    cp: omitting directory 'mysite' # (cpコマンドはデフォルトではコピーの対象がファイルだけなので)mysiteディレクトリはomit(除外する)されています、という意味。
    ```
    
    - そこで、サブディレクトリの中身まで一気にコピーするには再帰的を意味する recursive の -r オプションを使用し、`cp -r mysite/ myprofile` と書く。再帰的：自己の行為の結果が自己に戻ってくること。フィードバック。
    
    ```bash
    dotinstall:~ $ cp -r mysite/ myprofile # cpコマンドに -r オプションを付けて実行する。
    dotinstall:~ $ ls # lsコマンドで確認。
    myprofile  mysite # myprofile と mysite それぞれのディレクトリを確認。
    dotinstall:~ $ ls myprofile/css/ # myprofileディレクトリ内にあるcssディレクトリ内を確認。
    styles.css # cssディレクトリ内にstyles.cssファイルを確認。
    ```
    
- ディレクトリを丸ごと削除したい場合、
    - あらかじめ、ディレクトリの中身を削除しなくでも rmdir ではなく、 rm コマンドの -r オプションを使用すれば一気に削除することができる。
    
    ```bash
    dotinstall:~ $ rm -r myprofile/ # rmコマンドに-rオプションを付けて、myprofileディレクトリを丸ごと削除する。
    dotinstall:~ $ ls # lsコマンドでディレクトリを確認。
    mysite # myprofileディレクトリは削除され、mysiteディレクトリが残っている。
    ```
    

※ `rm -r` コマンドは**とても危険なコマンドなので、使用する際は十分注意すること**。
### 要点
- mkdir -p：深い階層までディレクトリを作成することができる。
- cp -r：ディレクトリを丸ごとコピーできる。
- rm -r：ディレクトリを丸ごと削除できる。※このコマンドはとても危険なので、使用する際は十分に注意すること。</details>


<details><summary>#12 シンボリックリンクを作ってみよう</summary>

- 少し深い階層を作成する。
    
    ```bash
    dotinstall:~ $ mkdir -p myapp/css/common # mkdirコマンドに-pオプションを付けて一気に作成する。myappディレクトリの中のcssディレクトリの中のcommonファイルがある、という階層を作成。
    ```
    
    - ここでホームディレクトリで作業を行い、今作成したディレクトリによくアクセスするようになった時、毎回毎回全てを打ち込むのは面倒なので、シンボリックリンクという仕組みを使用して別名を付ける。
        - エイリアスとは、偽名、別名、通称などの意味を持つ英単語。ITの分野では、ある対象や[実体](https://e-words.jp/w/%E3%82%A8%E3%83%B3%E3%83%86%E3%82%A3%E3%83%86%E3%82%A3.html)を、複数の異なるシンボルや[識別子](https://e-words.jp/w/%E8%AD%98%E5%88%A5%E5%AD%90.html)で同じように参照できるする仕組みを指す。別名。
    - **lnコマンドの書式**
    
    ```bash
    ln オプション ディレクトリ（またはファイル）名 リンク名
    
    ln -s myapp/css/common/ mycommon
    ```
    
    ```bash
    dotinstall:~ $ ln -s myapp/css/common/ mycommon # lnコマンドに-sオプションを付けて、myapp/css/common/をmycommonという名前のシンボリックリンクを作成する。
    dotinstall:~ $ ls -l # lsコマンドに-lオプションを付けて、ディレクトリの詳細を表示させる。
    total 4
    drwxr-sr-x    3 dotinsta wheel         4096 Aug 24 14:02 myapp
    lrwxrwxrwx    1 dotinsta wheel           17 Aug 24 14:11 mycommon -> myapp/css/common/ # mycommonの実体はmyapp/css/common/であると表示。
    ```
    
    - この mycommonは通常のディレクトリと同様に使用できるので、例えばその中に新しくファイルを作成したい場合、
        - `touch mycommon/common.css` といった感じで、作成することができる。
        
        ```bash
        dotinstall:~ $ touch mycommon/common.css # mycommonディレクトリ内にcommon.cssという名のファイルを作成。
        dotinstall:~ $ ls mycommon # lsコマンドでmycommonディレクトリ内を確認。
        common.css # common.cssファイルが作成されている。
        ```
        
    - また、mycommonディレクトリはmyapp/css/common/と同じなので、`ls myapp/css/common/` でも作成したcommon.cssファイルを表示させることができる。
    
    ```bash
    dotinstall:~ $ ls myapp/css/common/ # lsコマンドでmyapp/css/common/内を確認。
    common.css # common.cssファイルを確認できた。
    ```
    

※`myapp/css/common/`が`/`で終わっているのでわかりにくいかもしれませんが、`/`で終わった場合はディレクトリを指定していると考えると良いと思います。

- シンボリックリンクを削除したい場合、通常のファイルと同様 rm コマンドを使用すれば良い。
    
    ```bash
    dotinstall:~ $ rm mycommon # rmコマンドでシンボリックリンクmycommonを削除する。
    dotinstall:~ $ ls # lsコマンドでディレクトリを確認する。
    myapp # シンボリックリンクmycommonは削除され、myappディレクトリだけが残っている。
    ```
    

**※シンボリックリンクはディレクトリだけでなく、ファイルにも使用できるので扱いに慣れておくこと。**
### 質問：新規ファイルやシンボリックマークを作成する際に / のあとに空白を開けない場合があるのはなぜですか？
**回答：空白で区切る場合はリンク名を指定、スラッシュで区切る場合はディレクトリ名を指定しています。**

**コマンドのルールとして、最初にコマンド名を入力し、スペース区切りでオプションやファイル名などを入力**します。**オプション等はそれぞれコマンド毎に決まっています**。

以下はシンボリックリンクを作成するコマンドですが、

```fortran
ln -s myapp/css/common/ mycommon
```

`ln`コマンドの書式は以下のようになっていて、それぞれスペースで区切る必要があります。

```
ln オプション ディレクトリ（またはファイル）名 リンク名

```

上のコードと照らし合わせると

`-s` ：オプション（シンボリックリンクを作成する意味のオプションです）

`myapp/css/common/`：ディレクトリ名

`mycommon`：リンク名

となります。

`myapp/css/common/mycommon` というファイル名を指定しているのではなく、それぞれ上記の意味になる、というわけですね。

`myapp/css/common/`が`/`で終わっているのでわかりにくいかもしれませんが、`/`で終わった場合は**ディレクトリを指定している**と考えると良いと思います。

一方で、`touch`コマンドの書式は以下のようになっています。

```
touch ファイル名
```

ファイル名には作成したいファイル名を指定します。今回は作成したシンボリックリンク`mycommon`の中に`common.css`というファイルを作りたいのですが、ディレクトリからすべて書く必要があるため、`mycommon/common.css`というように記述します。

書式はコマンド毎に異なるので、「Unix コマンド ln」などで検索してみると良いかと思います。</details>


<details><summary>#13 cat,more,lessコマンドを使ってみよう</summary>

- テキストファイルをの中身を見る。
    - 先ず、etcディレクトリ内のservicesをホームディレクトリにコピーする。コピー先は現在のディレクトリにするため、「.」を使用。
    
    ```bash
    dotinstall:~ $ cp /etc/services . # cpコマンドでetcディレクトリ内のservicesファイルをコピーする。コピー先は「.」、コピー元は/etc/services
    dotinstall:~ $ ls # lsコマンドでディレクトリを確認する。
    services # servicesファイルがコピーされている。
    ```
    
    - テキストファイルの中身を見るには cat コマンドを使用する。表示された内容はシステムの設定項目で、理解する必要はないが多くの項目が表示される。
    
    ```bash
    dotinstall:~ $ cat services
    # Network services, Internet style
    ...中略
    # Local services
    ```
    
- そこで、ページごとに見ることができるページャーというコマンドを使用する。
    - ページャーは2種類。1つは more 。全体の何%なのかを表示してくれる。次のページに進みたい場合は、spaceキーを押す。終了したい場合は、quitという意味のQキーを押せば良い。
    
    ```bash
    dotinstall:~ $ more services # servicesファイルの中身を％で表示してくれる。
    # Network services, Internet style
    #
    # Note that it is presently the policy of IANA to assign a single well-known
    # port number for both TCP and UDP; hence, officially ports have two entries
    # even if the protocol doesn't support UDP operations.
    #
    # Updated from https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml .
    #
    # New ports will be added on request if they have been officially assigned
    # by IANA and used in the real-world or are needed by a debian package.
    # If you need a huge list of used numbers please install the nmap package.
    
    tcpmux          1/tcp                           # TCP port service multiplexer
    echo            7/tcp
    echo            7/udp
    discard         9/tcp           sink null
    discard         9/udp           sink null
    systat          11/tcp          users
    daytime         13/tcp
    daytime         13/udp
    netstat         15/tcp
    qotd            17/tcp          quote
    chargen         19/tcp          ttytst source
    chargen         19/udp          ttytst source
    ftp-data        20/tcp
    ftp             21/tcp
    fsp             21/udp          fspd
    ssh             22/tcp                          # SSH Remote Login Protocol
    --More-- (6% of 14464 bytes) # 全体の何%なのかを表示してくれる。次ページに進む場合はspaceキー、終了する場合はQキーを押す。
    ```
    
    - 2つ目のページャー、 less 。 `less ファイル名` とする。more と同様、spaceキーで次ページで進むことができる。また、/の後ろに検索したい単語を入力するとその箇所まで移動する。nextという意味のNキーで次の検索結果まで飛ぶこともできる。終了したい場合はQキー。
### 質問：more と less の違いはなんですか？
回答：less は more と違い、前方後方にページ送りができたりと多機能です。

> 動画では、lessには / で検索機能があると紹介されていますが、そのほかにmoreとlessでどのような機能の違いがあるのでしょうか？
> 

主な違いとしては，`more`は前方にのみページ送りが可能な一方で`less`は前方と後方の両方にページ送りが可能な点があるかと思います。そのほか、検索機能もそうですが`less`のほうが多機能です。
### 質問：catコマンドとlsコマンドの違いはなんですか？
回答：lsはファイルの一覧を表示し、catはファイルの中身を表示します。

`ls`はディレクトリにあるファイルやディレクトリを一覧で表示するためのコマンドです。`ls -l` とすると、ファイルの実行権限や所有やサイズなどの情報が表示されるようになります。`ls`はあくまでもディレクトリの中にあるファイルの一覧を表示するためのコマンドなので、ファイルの中身を表示することはできません。

`cat`は上述の通りでファイルの中身を表示してくれます。
### 要点
- cat：**ファイルの中身を見るコマンド。**
- ページャー：ファイルの中身をページごとに表示する機能。
- more：ファイルの中身を見るコマンド。ページャーの機能が付いている。
- less：ファイルの中身を見るコマンド。ページャーの機能が付いている。/の後ろに検索したい単語を入力するとその箇所まで移動する。検索時Nキーで次の検索結果まで移動することができる。</details>


<details><summary>#14 wc,head,tail,grepコマンドを使ってみよう</summary>

- テキストを操作するためのコマンド。
    - wc(word count)は行数や単語数などを教えてくれる。左から行数、単語数、バイト数、ファイル名を表示。ちなみに、日本語のテキストの場合、英語と違い単語の区切りが分かりづらいため正確な単語数が表示されない点に注意すること。
        
        ```bash
        dotinstall:~ $ wc services # servicesファイルの行数、単語数、バイト数、ファイル名を表示。
              417      1994     14464 services # 左から行数、単語数、バイト数、ファイル名
        ```
        
        - 行数だけを表示する -l オプションもよく使われる。
        
        ```bash
        dotinstall:~ $ wc -l services # servicesファイルの行数を表示せよ
        417 services # 行数、ファイル名が表示
        ```
        
    - 先頭や末尾の何行かだけを確認したい場合に使用する、headとtail。先頭の3行を確認する場合、
        
        ```bash
        dotinstall:~ $ head -n 3 services # headコマンド -nオプション 3 ファイル名
        # または
        dotinstall:~ $ head -3 services # headコマンド -3 ファイル名
        
        # Network services, Internet style
        #
        # Note that it is presently the policy of IANA to assign a single well-known
        ```
        
        末尾の3行を確認する場合、
        
        ```bash
        dotinstall:~ $ tail -3 services # tailコマンド -3 ファイル名
        fido            60179/tcp                       # fidonet EMSI over TCP
        
        # Local services
        ```
        
    - grepについて、これはファイルの中身から特定の単語を検索するためのコマンド。これから backup という単語が services に含まれるかどうか検索する。grepは高機能なのが特徴。
        
        ```bash
        dotinstall:~ $ grep 'backup' services # grepコマンドでbackupという単語がservicesファイルに含まれているか検索せよ。
        amanda          10080/tcp                       # amanda backup services
        afbackup        2988/tcp                        # Afbackup system
        afbackup        2988/udp
        afmbackup       2989/tcp                        # Afmbackup system
        afmbackup       2989/udp
        kamanda         10081/tcp                       # amanda backup services (Kerberos)
        amandaidx       10082/tcp                       # amanda backup services
        amidxtape       10083/tcp                       # amanda backup services
        # 以上のようにbackupが含まれる行が表示された。
        ```

### 要点
- wc：wc(word count)は行数や単語数などを教えてくれる。
- head：先頭の何行かを表示するコマンド。
- tail：末尾の何行かを表示するコマンド。
- grep：ファイルの中にある特定の単語を検索するコマンド。</details>


<details><summary>#15 コマンドの履歴を活用してみよう</summary>

- コマンドの履歴について、
    - historyコマンドはコマンドの履歴を確認することができる。
        
        ```bash
        dotinstall:~ $ history
            1  ls
            2  ed /etc/
            3  ls
            4  cd /etc/
            5  pwd
            6  ls -al
            7  cat services
            8  cat alpine-release
            9  cd
           10  history
        ```
        
        - 矢印キーの↑でコマンドを遡ることができるが、一気に戻りたい場合、historyコマンドで表示された左側の番号を使用することで移動できる。例えば、5番のコマンドを呼び出したい場合は、`!5`と入力すれば良い。
            
            ```bash
            dotinstall:~ $ history # historyコマンドでコマンドの履歴を表示。
                1  ls
                2  ed /etc/
                3  ls
                4  cd /etc/
                5  pwd
                6  ls -al
                7  cat services
                8  cat alpine-release
                9  cd
               10  history
            dotinstall:~ $ !5 # historyコマンドで表示された番号を!と組み合わせてコマンドを呼び出すことができる。
            pwd # コマンドが呼び出され、
            /home/dotinstall #コマンドが実行された。
            ```
            
        - 直前のコマンドは `!!` でも実行できる。
            
            ```bash
            dotinstall:~ $ !5
            pwd
            /home/dotinstall
            dotinstall:~ $ !! # !!で直前のコマンドを実行できる。
            pwd
            /home/dotinstall
            ```
            
        - `!-2` とすると、二つ前のコマンドを実行することができる。
            
            ```bash
            dotinstall:~ $ !5
            pwd
            /home/dotinstall
            dotinstall:~ $ !!
            pwd
            /home/dotinstall
            dotinstall:~ $ !-2
            pwd
            /home/dotinstall
            ```
            
    - 直前のコマンドの引数だけを使用したい場合、例えば、`ls etc` で中身を確認した後、そのディレクトリに移動したいなら `cd etc` で実行してもよいが、直前のコマンドに渡した最後の引数は `!$` で書くことができる。
        
        ```bash
        dotinstall:~ $ ls /etc/
        alpine-release        logrotate.d           securetty
        apk                   modprobe.d            services
        ca-certificates       modules               shadow
        ca-certificates.conf  modules-load.d        shadow-
        conf.d                motd                  shells
        crontabs              mtab                  ssl
        fstab                 network               sudo.conf
        group                 opt                   sudo_logsrvd.conf
        group-                os-release            sudoers
        hostname              passwd                sudoers.d
        hosts                 passwd-               sudoers.dist
        init.d                periodic              sysctl.conf
        inittab               profile               sysctl.d
        inputrc               profile.d             terminfo
        issue                 protocols             udhcpd.conf
        localtime             resolv.conf
        dotinstall:~ $ cd !$
        cd /etc/
        dotinstall:/etc $
        ```
        
    - !の後ろに pw を入力すると、 pw から始まる直近のコマンドを実行することができる。
        
        ```bash
        dotinstall:/etc $ !pw # pwから始まる直近のコマンドを実行することができる。
        pwd
        /etc
        ```
        
    - 記憶が曖昧な場合、最後に :p を付けて実行せずにそのコマンドの表示だけを行うことができる。
        
        ```bash
        dotinstall:/etc $ !pw:p # pwから始まるコマンドの確認ができる。
        pwd
        ```
        
- 履歴を検索する。
    - control + R
        
        ```bash
        (reverse-i-search)`': # 表示が変わる。そのまま検索したい文字を入力する。
        (reverse-i-search)`ca': cat alpine-release
        ```
        
        - 次の候補に行くにはもう一度 control + R を押す。実行したければそのままreturnキーを押す。検索を中断するには control + C を押す。
            
            ```bash
            (reverse-i-search)`ca': cat services # control + R で次の候補へ。
            
            (reverse-i-search)`ca': ^Ct services # control + C で検索を中断。
            dotinstall:/etc $
            ```
            
### 要点
- history：コマンドの履歴を確認する。
- !：!の後ろにhistoryコマンドで表示された番号を入力すると、そのコマンドを実行できる。
- !!：**直前のコマンドを実行する**。
- !$：直前のコマンドの引数を使用する。
- :p： `!pw:p` で pw から始まる直近のコマンドを実行せずに表示する。</details>


<details><summary>#16 ユーザーとグループの一覧を見てみよう</summary>

- UNIXのユーザー管理について。
    - 先ずはこのシステムに設定されているユーザーの一覧を見る。
        
        ```bash
        dotinstall:~ $ cat /etc/passwd
        root:x:0:0:root:/root:/bin/ash
        bin:x:1:1:bin:/bin:/sbin/nologin
        daemon:x:2:2:daemon:/sbin:/sbin/nologin
        adm:x:3:4:adm:/var/adm:/sbin/nologin
        lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
        sync:x:5:0:sync:/sbin:/bin/sync
        shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
        halt:x:7:0:halt:/sbin:/sbin/halt
        mail:x:8:12:mail:/var/mail:/sbin/nologin
        news:x:9:13:news:/usr/lib/news:/sbin/nologin
        uucp:x:10:14:uucp:/var/spool/uucppublic:/sbin/nologin
        operator:x:11:0:operator:/root:/sbin/nologin
        man:x:13:15:man:/usr/man:/sbin/nologin
        postmaster:x:14:12:postmaster:/var/mail:/sbin/nologin
        cron:x:16:16:cron:/var/spool/cron:/sbin/nologin
        ftp:x:21:21::/var/lib/ftp:/sbin/nologin
        sshd:x:22:22:sshd:/dev/null:/sbin/nologin
        at:x:25:25:at:/var/spool/cron/atjobs:/sbin/nologin
        squid:x:31:31:Squid:/var/cache/squid:/sbin/nologin
        xfs:x:33:33:X Font Server:/etc/X11/fs:/sbin/nologin
        games:x:35:35:games:/usr/games:/sbin/nologin
        cyrus:x:85:12::/usr/cyrus:/sbin/nologin
        vpopmail:x:89:89::/var/vpopmail:/sbin/nologin
        ntp:x:123:123:NTP:/var/empty:/sbin/nologin
        smmsp:x:209:209:smmsp:/var/spool/mqueue:/sbin/nologin
        guest:x:405:100:guest:/dev/null:/sbin/nologin
        nobody:x:65534:65534:nobody:/:/sbin/nologin
        dotinstall:x:1000:10:Linux User,,,:/home/dotinstall:/bin/ash
        ```
        
    - ユーザーは2種類ある。管理者ユーザーであるルートユーザーとそれ以外の一般ユーザー。
        - ルートユーザーを使用すれば全ての操作ができるが、うっかり重大なミスをしないように、役割ごとに一般ユーザーを設定して作業するのが一般的。
        - dotinstallは今回のレッスン用に作成したユーザーで、それ以外のユーザーはシステムを動かすために必要なユーザーである。
        - なお、ユーザー名の後の項目はコロンで区切られていて、順番にパスワード、ユーザーの ID 、ユーザーが所属しているグループの ID 、コメント、ホームディレクトリの位置、そしてシェルとして使っているコマンドになります。
        - パスワードが x になっているのは、セキュリティの理由上で伏字になっているため。
        - ユーザーが所属しているグループの ID は、 dotinstall は ID が 10 のグループに所属しているのが分かる。
    - dotinstallではどのようなグループが設定されているか調べてみる。これもコロン区切りになっていて、wheel はグループの名前、次がグループのパスワードで X で伏字になっている。その次がグループのID。最後にそのグループに所属しているユーザーがカンマ区切りで指定されている。今回の場合は、wheelグループにrootユーザーとdotinstallユーザーが所属しているのが分かる。
        
        ```bash
        dotinstall:~ $ cat /etc/group # /etc/group でグループの情報を確認できる。
        root:x:0:root
        bin:x:1:root,bin,daemon
        daemon:x:2:root,bin,daemon
        sys:x:3:root,bin,adm
        adm:x:4:root,adm,daemon
        tty:x:5:
        disk:x:6:root,adm
        lp:x:7:lp
        mem:x:8:
        kmem:x:9:
        wheel:x:10:root,dotinstall # IDが10のグループ グループ名、パスワードxで伏字、グループID、グループに所属しているユーザー
        floppy:x:11:root
        mail:x:12:mail
        news:x:13:news
        uucp:x:14:uucp
        man:x:15:man
        cron:x:16:cron
        console:x:17:
        audio:x:18:
        cdrom:x:19:
        dialout:x:20:root
        ftp:x:21:
        sshd:x:22:
        input:x:23:
        at:x:25:at
        tape:x:26:root
        video:x:27:root
        netdev:x:28:
        readproc:x:30:
        squid:x:31:squid
        xfs:x:33:xfs
        kvm:x:34:kvm
        games:x:35:
        shadow:x:42:
        cdrw:x:80:
        usb:x:85:
        vpopmail:x:89:
        users:x:100:games
        ntp:x:123:
        nofiles:x:200:
        smmsp:x:209:smmsp
        locate:x:245:
        abuild:x:300:
        utmp:x:406:
        ping:x:999:
        nogroup:x:65533:
        nobody:x:65534:
        ```
        
    - 特定のユーザーがどのグループに所属しているかを groups コマンドで調べることができる。
        
        ```bash
        dotinstall:~ $ groups dotinstall # groupsコマンドでdotinstallがどのグループに所属しているかを調べる。
        wheel # dotinstallはwheelグループに所属していることが確認できた。
        dotinstall:~ $ groups root # groupsコマンドでrootがどのグループに所属しているかを調べる。
        root bin daemon sys adm disk wheel floppy dialout tape video # rootが所属しているグループ名が表示された。ここでのrootはユーザーではなく、所属しているグループ名である。
        ```
        

**※ユーザーとグループはファイルのアクセス権限において重要な意味を持っている。**
### 要点
- /etc/passwd：UNIXのシステムに設定されているユーザーの一覧を表示する。
- /etc/group：グループの情報を確認できる。
- groups：特定のユーザーがどのグループに所属しているかを調べてくれる。</details>


<details><summary>#17 アクセス権限について理解しよう</summary>

