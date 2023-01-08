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

- ファイルのアクセス権について。
    - 先ずはファイルを作成し、 `ls -l` で詳細情報を確認する。
        
        ```bash
        dotinstall:~ $ touch index.html # touchコマンドでindex.htmlファイルを作成。
        dotinstall:~ $ ls -l # lsコマンドに-lオプションを付けて、詳細情報を表示。
        total 0
        -rw-r--r--    1 dotinsta wheel            0 Aug 25 15:36 index.html
        # アクセス権に関係するのが、-rw-r--r--、dotoinsta、wheelの3つ。
        ```
        
        - `dotinsta`は、このファイルやディレクトリを所有するユーザーとグループのことで、通常はそれを作ったユーザーとそのユーザーが所属するグループになります。また、dotinstaがindex.htmlファイルに対してどういう操作を行うことができるのかを示すのが、`-rw-r--r--` です。
        - -rw-r--r-- の見方は、最初の1文字目はファイルの種別を表していて、- は通常のファイル、d はディレクトリ、l はシンボリックリンクとなる。
            - **次に続く9文字は、3文字ずつ分かれていて、最初の3文字 `rw-` は所有するユーザー(dotinsta)のアクセス権、次の3文字 `r--` は所有するグループ(wheel)のアクセス権、最後の3文字 `r--` はその他のユーザーのアクセス権です**。
            - また、 rw- の3文字は、通常、先頭から `rwx` か `rw-` で表示されます。
                - `r` は read 、読み取り可能。`w` は write 、書き込み可能。`x` は execute 、実行可能。という意味になります。
                - なお、ディレクトリの場合、実行できるものではないので、3文字目が x だったら開くことができるという意味になります。
                - したがって、今回のindex.htmlについて考えると、**dotinstallユーザーは、(rw- なので)読み書きすることはできるけど実行はできない**。
                - **wheel グループに所属しているユーザーに関しては、(r-- なので)読むことだけができる**。
                - **その他のユーザーに関しても、(r-- なので)読むことだけができる**。という意味になります。

※慣れないと、記号ばかりで分かりづらいのですが、ファイルやディレクトリには所有ユーザー(今回はdotinsta)とグループ(今回はwheel)が設定されていて、こちらの 9 文字( rw-r--r-- )でアクセス権が表現されているという点を意識しておきましょう。
### 要点
- r ： read 、読み取り可能
- w ： write 、書き込み可能
- x ： execute 、実行可能</details>


<details><summary>#18 chmodコマンドの使い方を理解しよう</summary>

- 以下のアクセス権( -rw-r--r-- )は、chmod(change mode)コマンドで変更することができます。その際 `rw-` の 3 文字は user の u 、次の 3 文字 `r--` は group の g 、 最後の 3 文字 `r--` は other の o 、もしくは9文字全てを all の a で扱うことができます。
    
    ```bash
    rw-r--r--    1 dotinsta wheel            0 Aug 25 15:36 index.html
    ```
    
    - 9文字全ての権限を `rwxrwxrwx` として一気に付けたかった場合、全てに対してなので a に対して = を使用して以下のように書きます。
        
        ```bash
        rwx rwx rwx   chmod a=rwxrwxrwx index.html
        ```
        
    - 若しくは `rwxrwxrwx` から `rwxrw-rw-` にしたい場合、group と other の権限を rw だけにすればいいので、以下のように書きます。
        
        ```bash
        rwx rw- rw-   chmod g=rw,o=rw index.html
        ```
        
    - さらに `rwxrwxrwx` から `rwxrwxr--` にしたい場合、+ や - で権限を追加したり、削除することもできて、 g に x を足す、 o から w を引くという操作になるので、以下のように書きます。
        
        ```bash
        rwx rwx r--   chmod g+x,o-w index.html
        ```
        
- それぞれの3文字を数値で表現することができます。**右から 2 の 0 乗、 2 の 1 乗、 2 の 2 乗で表現できる**ので、たとえばこういった権限を作りたい場合、 rwx は右から 1 2 4 になるので合計で 7 。**※2の0乗は、「1」になる。ということを理屈抜きで覚えておこう**。
    
    ```bash
    rwx
    # x = 2の0乗、w = 2の1乗、r = 2の2乗、で表現できる。
    # よって、rwxは右から、x = 1、w = 2、r = 4、となるので合計で7。
    
    rwx rwx rwx   chmod 777 index.html # rwx = 7で、それが3つあるので777、となる。
    
    # 以下のような権限を設定したい場合
    rws rw- rw-   chmod 766 index.html # rws = 4+2+1 = 7、rw- = 4+2+0 = 6、rw- = 4+2+0 = 6、よって766、となる。
    
    # 以下のような権限を設定したい場合
    rwx rwx r--   chmod # rws = 4+2+1 = 7、rws = 4+2+1 = 7、r-- = 4+0+0 = 4、よって774、となる。
    ```

</details>


<details><summary>#19 アクセス権限を変更してみよう</summary>

- アクセス権限を変更してみよう。
    - 先ずファイルを作成し、`ls -l` で確認する。
        
        ```bash
        dotinstall:~ $ touch index.html # (ファイルがないので)touchコマンドでファイルを作成する。
        dotinstall:~ $ ls -l # lsコマンドに-lオプションで作成したindex.htmlファイルの詳細を表示する。
        total 0
        -rw-r--r--    1 dotinsta wheel            0 Aug 26 13:44 index.html
        ```
        
    - ここで、全ての権限を与えます。 chmod コマンドを使用して、全てに対して全ての権限と書く。
        
        ```bash
        dotinstall:~ $ chmod a=rwxrwxrwx index.html # chmodコマンドで全てに対して全ての権限を与える。
        dotinstall:~ $ ls -l # lsコマンドに-lオプションでindex.htmlファイルの詳細を表示。
        total 0
        -rwxrwxrwx    1 dotinsta wheel            0 Aug 26 13:44 index.html # アクセス権が変更されたことが確認できる。
        ```
        
    - この状態から g に関しては rw だけ、そして o に関しては r だけにしてみます。chmod コマンドを使って、 g に関しては rw 、 o に関しては r だけとしてあげればいいでしょう。
        
        ```bash
        dotinstall:~ $ chmod g=rw,o=r index.html # chmodコマンドでg=rw、o=rにする。
        dotinstall:~ $ ls -l # lsコマンドに-lオプションでindex.htmlファイルの詳細を表示。
        total 0
        -rwxrw-r--    1 dotinsta wheel            0 Aug 26 13:44 index.html # アクセス権が変更されたことを確認。
        ```
        
    - 次にこの状態から g には x 権限を加えて、 o からは r 権限を外してみます。+ や - を使って、 g には x 、 o には r を引いてあげましょう。
        
        ```bash
        dotinstall:~ $ chmod g+x,o-r index.html
        dotinstall:~ $ ls -l
        total 0
        -rwxrwx---    1 dotinsta wheel            0 Aug 26 14:53 index.html
        ```
        
    - ここで全てを rw だけにしたかった場合、数値で表すと、右から 0 2 4 になるので、全てを 6 にしてあげればいいでしょう。
        
        ```bash
        dotinstall:~ $ chmod 666 index.html
        dotinstall:~ $ ls -l
        total 0
        -rw-rw-rw-    1 dotinsta wheel            0 Aug 26 14:53 index.html
        ```
        

**※こうしたアクセス権の操作もできるようになっておきましょう。**
### 要点
- chmod a=rwxrwxrwx index.html
- chmod g=rw,o=r index.html
- chmod g+x,o-r index.html
- chmod 666 index.html</details>


<details><summary>#20 sudoコマンドを使ってみよう</summary>

- 実は今回 dotinstall ユーザーにはルートユーザーの権限の一部が使えるように設定されています。では、ルートユーザーしか見ることができないファイルを見てみましょう。
    
    すると、ルートユーザーには読み・書き権限があり、 shadow グループに所属するユーザーには読み込み権限だけがあり、そのほかのユーザーに関しては何の権限もないのが分かります。**※最初の3文字は user、真ん中の3文字は group、最後の3文字は other。**
    
    ```bash
    dotinstall:~ $ ls -l /etc/shadow # lsコマンドに-lオプションを付け、etcディレクトリの中のshadowファイルの詳細を表示。
    -rw-r-----    1 root     shadow         454 Sep 23  2020 /etc/shadow # userには読み書きの権限が、groupには読み込みの権限だけが、otherには何の権限がない。
    ```
    
    - したがって、そのほかのユーザーである dotinstall ユーザーがその中身を見ようとすると、エラーになります。
        
        ```bash
        dotinstall:~ $ cat /etc/shadow # catコマンドでetcディレクトリの中のshadowファイルの中身を表示させる。
        cat: can't open '/etc/shadow': Permission denied # otherユーザー故にshadowファイルの中身を開くことができない。
        ```
        
    - ここで一時的にルートユーザーの権限を使用したい場合、 sudo コマンドを使用します。その上で実行したいコマンドを入力するのですが、実行したいコマンドは直前に打ってあるので、`!!` でも打つことができます。
        
        ```bash
        dotinstall:~ $ sudo !! # sudoコマンドでルートユーザーの権限を使用して、!!で直前のコマンド(catコマンド)を使用する。
        sudo cat /etc/shadow
        root:!::0:::::
        bin:!::0:::::
        daemon:!::0:::::
        adm:!::0:::::
        lp:!::0:::::
        sync:!::0:::::
        shutdown:!::0:::::
        halt:!::0:::::
        mail:!::0:::::
        news:!::0:::::
        uucp:!::0:::::
        operator:!::0:::::
        man:!::0:::::
        postmaster:!::0:::::
        cron:!::0:::::
        ftp:!::0:::::
        sshd:!::0:::::
        at:!::0:::::
        squid:!::0:::::
        xfs:!::0:::::
        games:!::0:::::
        cyrus:!::0:::::
        vpopmail:!::0:::::
        ntp:!::0:::::
        smmsp:!::0:::::
        guest:!::0:::::
        nobody:!::0:::::
        dotinstall:!:18528:0:99999:7:::
        ```
        

**※ルートユーザーは何でもできてしまうので、うっかり操作ミスをしてしまうと大変なことになります。そこで、今回のように特殊なコマンドである sudo を使うことで必要なときだけルートユーザーの権限を使って作業するのが一般的です。 sudo の設定にまで踏み込んでいきませんが、こうした仕組みになっているということを知っておくといいでしょう。**
### 要点
一時的にrootユーザーの権限を使うことができる、sudoコマンドについて学習していきます。

- 権限のないファイルへのアクセス
- sudo：**一時的にrootユーザーの権限を使用することができるコマンド。**</details>


<details><summary>#21 vi を起動してみよう</summary>

- UNIX上で使用できるエディターについて。
    
    多くの Linux ディストリビューションには標準で vi (ブイアイ)というエディターがついてくるので、最低限の使い方を見ていきましょう。
    
    - vi を起動するには vi と打って、作成や編集をしたいファイル名を入れてあげれば OK です。今回は hello とします。入力してreturnキーを押すとviの画面に切り替わります。
        
        ```bash
        dotinstall:~ $ vi hello # returnキーを押すとviの画面に切り替わる。
        
        # viの画面。
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        ~
        - hello 1/1 100%
        ```
        
    - vi の使い方：先ず理解しなくてはならないのは、 vi にはコマンドモードと編集モードがあるという点です。起動すると、コマンドモードになりますが、ここではカーソルの移動と様々な編集コマンドを使うことができます。うっかり変なキーを押すと、編集コマンドが起動してしまうので、落ち着いて insert の i を押してあげてください。すると編集モードになって左下に I が表示されます。編集モードにいるかどうかはこの左下の I で判断するようにしましょう。
        
        ```bash
        # viの画面に切り替わったら、他のキーは決して押さずに落ち着いてinsertを意味するIキーを押します。
        ~
        ~
        I hello 1/1 100% # (viの)編集モードに切り替わり、左下にIが表示されます。
        ```
        
        - 編集モードから抜けるには escキーを押します。
            
            ```bash
            # escキーを押す。
            ~
            ~
            - hello 1/1 100% # 左下のIがなくなり、編集モードから抜けたことになる。
            ```
            
        - vi モードを終了させるにはコマンドモードにいる必要があるので、左下に I がないことを確認して、落ち着いて :q (quitのq)入力して return キーを押しましょう。
            
            ```bash
            ~
            ~
            :q # :qと入力してreturnキーを押す。
            
            # viモードが終了して、プロンプトに戻る。
            dotinstall:~ $ vi hello
            dotinstall:~ $
            ```
            
### 要点
テキストを編集することができる、viエディタの起動と終了について見ていきます。

- vi：UNIX上で使用できる vi エディターを起動する。
    - また、ファイルがなかった場合新規作成してくれる。
- i：vi エディター起動時、Iキーを押すことで編集モードに切り替わる。I は insert を意味する。
- esc：vi エディターの編集モードを終了させる。
- :q：vi エディターを終了させる。</details>


<details><summary>#22 vi でファイルを編集してみよう</summary>

- 今回は hello と表示するスクリプトを書きます。
    - vi を起動、I キーで編集モードに切り替えてから、 `#!/bin/ash` と入力する。先頭の 2 文字 `#!` はシェバンと呼ばれていて、これがあったら次に続くプログラムで実行しなさいよ、という意味になります。今回はこの環境で使っているシェルのプログラムを指定してあげましょう。そのあとに文字列を表示するコマンドである echo を使って、 'Hello there!' という文字列を表示してみましょう。空白を含む文字列はシングルクオーテーションで囲む点にも注意しておいてください。
        
        ```bash
        #!/bin/ash
        echo 'Hello there!'
        ~
        ~
        
        # 次にescキーを押して、:wqを入力してreturnキーを押す。
        ~
        ~
        :wq # returnキーを押して、vi終了。
        ```
        
    - プロンプトに戻り、cat コマンドで見てみると変更が保存されている。
        
        ```bash
        dotinstall:~ $ vi hello
        dotinstall:~ $ cat hello
        #!/bin/ash
        echo 'Hello there!'
        ```
        
    - vi を起動したあとに編集モードに入るのを忘れてうっかり変なコマンドを打ってしまった場合。
        
        ```bash
        #!/bin/ash
        echo 'Hello there!'
        ~
        ~
        ~
        - hello 1/2 50% # 編集モードに入らず、例えば大文字のDを押してしまった時、
        
        echo 'Hello there!' # 大文字のDは行末まで削除というコマンドなので、#!/bin/ashが削除されている。
        ~                  
        ~
        
        ```
        
    - 間違えたので保存せずに終了したい場合、左下にI がないこと(コマンドモードになっていること)を確認して、`:q!` を入力します。すると、保存せずに強制終了してくれます。

※vi はもっと奥が深いのですが、最低限の操作方法だけでも知っておくと、その場でファイルの編集ができて便利なので、慣れておくといいでしょう。

### 質問：なぜ /bin/ash と指定するのですか？
回答：オンライン実行環境で使用しているシェルが ash であるためです。

コマンドを受け付けてくれるプログラムをシェルと言いますが、シェルには様々な種類があり、OSによって使用するシェルが異なります。このレッスンのオンライン実行環境で使用しているシェルが`ash`というものになります。`/bin/ash`と指定するのは、`bin`ディレクトリのなかにある`ash`というシェルがあるためですね。

`ls /bin`としてファイル一覧を表示すると、`ash`があるのがわかると思います。
### 要点
viを使ってテキストファイルを作成する方法について見ていきます。

- #!：シェバンと呼ばれていて、これがあったら次に続くプログラムで実行しなさい、という意味。
- :qw：(コマンドモード時に入力すること)変更を保存してviエディターを終了する。
- :q!：(コマンドモード時に入力すること)変更を保存せずにviエディターを終了する。</details>


<details><summary>#23 ファイルを実行してみよう</summary>

- 以下のファイルにはどこにも実行権限がついていないので、所有者が実行できるように設定します。
    
    ```bash
    dotinstall:~ $ ls -l # lsコマンドに-lオプションを付けて、ファイルの詳細を表示する。
    total 4
    -rw-r--r--    1 dotinsta wheel           31 Aug 26 16:19 hello # helloファイルには実行可能を意味するe(execute)がない。
    
    dotinstall:~ $ chmod u+x hello # chmodコマンドで、userにx(executo)の権限を付け加える。
    dotinstall:~ $ ls -l # lsコマンドに-lオプションを付けて、helloファイルの詳細を表示する。
    total 4
    -rwxr--r--    1 dotinsta wheel           31 Aug 26 21:05 hello # userにx(executo)権限が付与されている。
    ```
    
    - これを実行するには、今いるhelloファイルを実行するように入力する→ `./hello`
        
        ```bash
        dotinstall:~ $ ./hello # .は現在いる場所。/helloはhelloファイルを意味する。
        Hello there! # viエディターで編集した文字列が表示される。
        ```
        
    - この、 ./hello コマンドはディレクトリを指定せずに単に hello とだけ打ってもうまくいきません。これは UNIX ではコマンドを検索するディレクトリが決められているからで、そのディレクトリ以外にあるコマンドを実行したい場合、そのファイルがどこにあるか指定する必要があるからです。
        
        ```bash
        dotinstall:~ $ hello # helloだけで実行する。
        bash: hello: command not found # そのようなコマンドは見つかりません、と表示。
        ```
        
    - コマンドをどこから検索しているかですが、環境変数という仕組みで管理されていて、 `echo $PATH` で見ることができます。PATH が環境変数の名前で $ が環境変数の中身を表すので、このようにすると、環境変数の中身を出力します。たくさんのディレクトリがコロンで区切られて登録されていて、コマンドを実行する際にはこれらのディレクトリを先頭から探していくという仕組みになっています。
        
        ```bash
        dotinstall:~ $ echo $PATH # 環境変数の中身を表示する。PATHは環境変数の名前、$は環境変数の中身を示す。
        /usr/lib/node_modules/npm/node_modules/npm-lifecycle/node-gyp-bin:/node_modules/.bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
        ```
        
### 要点
実行権限のあるファイルを実行する方法について見たのち、環境変数という仕組みについて学んでいきます。

- ./hello：今いるディレクトリの hello を実行せよ、という意味。※hello だけだと実行されずエラーが表示される。
- echo $PATH：環境変数という仕組みを確認する。
    - echo は画面に文字列や数値、変数を表示するコマンド。
    - PATH が環境変数の名前、$ が環境変数の中身を表す。</details>


<details><summary>#24 PATHの設定をしてみよう</summary>

- 前回見た $PATH にホームディレクトリを追加します。
    - 今のディレクトリのこちら(dotinstall)を現在ある $PATH の先頭に加えるには記号を間違えないように打って欲しいのですが、 export PATH=/home/dotinstall:$PATH のようにしてあげてください。このコマンドの export は環境変数を設定するための命令で、 PATH という名前でこのディレクトリ(dotinstall)と、既に設定されている $PATH の内容を繋げて設定しなさい、という意味です。PATH は環境変数の内容なので $ が付く点に注意してください。
        
        ```bash
        dotinstall:~ $ pwd # pwdコマンドで今いるディレクトリを表示する。
        /home/dotinstall # 現在いるディレクトリが表示。
        dotinstall:~ $ export PATH=/home/dotinstall:$PATH # exportコマンドでPATHという名前でdotinstallディレクトリと既に設定されている$PATHの内容を紐付けせよ。
        dotinstall:~ $ echo $PATH # echoコマンドで$PATHの内容を表示する。
        /home/dotinstall:/usr/lib/node_modules/npm/node_modules/npm-lifecycle/node-gyp-bin:/node_modules/.bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
        # ↑先頭に /home/dotinstall ディレクトリが追加されていることが確認できる。
        ```
        
    - このように特定のディレクトリを $PATH に加えることをパスを通すというのですが、これで単に hello と実行しても OK です。
        
        ```bash
        dotinstall:~ $ hello # helloだけで実行する。
        Hello there! # 設定したスクリプトが表示される。
        ```
        
    - また、どこから実行してもいいはずなので、ひとつ上のディレクトリに移動してから hello としてみましょう。
        
        ```bash
        dotinstall:~ $ cd .. # cdコマンドはディレクトリに移動する。 ..は一つ上のディレクトリに移動する。
        dotinstall:/home $ hello # プロンプトには一つ上の階層のhomeディレクトリが表示され、helloでコマンドを実行する。
        Hello there! # 設定したプロンプトが表示される。
        ```
        
    - ちなみに、実行しようとしているコマンドがどこのディレクトリから呼び出されているかは which コマンドで調べることができます。実行したコマンドが期待通りの動作をしない場合、違うパスのコマンドを実行していたりするので、そうしたときは which で調べてあげるといいでしょう。
        
        ```bash
        dotinstall:/home $ which hello # whichコマンドで実行しているコマンド(hello)がどこのディレクトリから呼び出されているかを調べる。
        /home/dotinstall/hello # helloコマンドがhomeディレクトリの中のdotinstallディレクトリの中から呼び出されていることがわかる。
        ```
        
    - 今回設定したこちらの $PATH ですが、実はログアウトすると `/home/doiinstall:` が元に戻ってしまいます。ログアウトしてもそうならないように設定もできるのですが、慣れないうちはあまりいじらない方が良いでしょう。今の時点では $PATH という環境変数があって、シェルはそこからコマンドを探しているのだよ、という仕組みだけを理解するようにしておいてください。
### 要点
環境変数を設定し、どのディレクトリからも hello を実行できるようにしてみます。

- export：環境変数やシェル変数を設定するコマンド。
- which：実行しようとしているコマンドがどこのディレクトリから呼び出されているかを調べてくれるコマンド。</details>


<details><summary>#25 リダイレクションを使ってみよう</summary>

- コマンドの実行結果をファイルに保存する方法について。
    - 例えば date という文字列を表示する場合は空白を含まないので、シングルクオーテーションマークはあってもなくてもいいのですが、 echo を使ってこのようにすれば OK です。
        
        ```bash
        dotinstall:~ $ echo 'date' # echoコマンドは画面に文字列や数値、変数を表示する。文字列dateを表示する。dateには空白がないのでシングルクォーテーションがあってもなくてもよい。
        date
        ```
        
    - ここで文字列 date をファイルの中身として保存したかった場合、リダイレクションというのですが、 `>` (大なり記号)を使ってあげれば、ファイルに書き込んでくれます。
        
        ```bash
        dotinstall:~ $ echo 'date' > commands.txt # echoコマンドで表示する文字列'date'をリダイレクションを使ってcommands.txtファイルに書き込め。
        dotinstall:~ $ cat commands.txt # catコマンドでcommands.txtファイルの中身を表示せよ。
        date # commands.txtファイルの中身である、文字列'date'が表示される。
        ```
        
    - このリダイレクションはファイルを上書きするので、そのあとに cal を commands.txt にリダイレクションした場合、 commands.txt の中身は cal で上書きされます。
        
        ```bash
        dotinstall:~ $ echo 'cal' > commands.txt # echoコマンドで表示される文字列'cal'をリダイレクションを使ってcommands.txtファイルに書き込め。
        dotinstall:~ $ cat commands.txt # catコマンドでcommands.txtファイルの中身を表示せよ。
        cal # commands.txtファイルの中身である、文字列'cal'が表示される。
        ```
        
    - 上書きではなく、末尾に追記する方法もあって、その場合は `>>` (大なり記号2つ)を使ってあげます。
        
        ```bash
        dotinstall:~ $ echo 'date' >> commands.txt # 文字列'date'をcommands.txtファイルの末尾に追記せよ。
        dotinstall:~ $ cat commands.txt # catコマンドでcommands.txtファイルの中身を表示せよ。
        cal 
        date # commands.txtファイルの末尾に文字列'date'が追記された。
        ```
        
    - commands.txtファイルの中身をコマンドに流し込むこともできます。cal も date もシェルコマンドなので、この環境でシェルとして使っている /bin/ash というコマンドに流し込んで実行したい場合、今度は `<` (小なり記号)を使ってこのようにファイルの内容を流し込んであげます。
        
        ```bash
        dotinstall:~ $ /bin/ash < commands.txt # commands.txtファイルの内容を/bin/ashコマンドに流し込め。
            August 2022
        Su Mo Tu We Th Fr Sa
            1  2  3  4  5  6
         7  8  9 10 11 12 13
        14 15 16 17 18 19 20
        21 22 23 24 25 26 27
        28 29 30 31
                             
        Sat Aug 27 13:46:08 JST 2022
        # cal:カレンダー、date：現在の日時、表示してくれる。
        ```
        
    - この cal と date の結果をさらにファイルに保存したい場合は上矢印キーで先ほどのコマンドを呼び出してから `>` を使ってリダイレクションを行います。
        
        ```bash
        dotinstall:~ $ /bin/ash < commands.txt > results.txt # calとdateの結果をリダイレクションを使用してresults.txtファイルに保存せよ。
        dotinstall:~ $ cat results.txt # catコマンドでresults.txtファイルの中身を表示せよ。
            August 2022
        Su Mo Tu We Th Fr Sa
            1  2  3  4  5  6
         7  8  9 10 11 12 13
        14 15 16 17 18 19 20
        21 22 23 24 25 26 27
        28 29 30 31
                             
        Sat Aug 27 13:52:32 JST 2022 # results.txtファイルの中身が表示。
        ```
        

※UNIX では、リダイレクションを使うことで、ファイルの内容をコマンドに流し込んだり、もしくはコマンドの実行結果をファイルに流し込んだりすることもできるので、慣れておくといいでしょう。

### 質問：シェルコマンドとはなんですか？
    
回答：シェル上で実行できる cat や echo 、 date のようなコマンドのことです。

シェルコマンドはシェル上で実行できる cat や echo ，date のようなコマンドのことですね。今までコマンドといっていたものを丁寧に言いなおしただけと考えていただければと思います。
    
### 質問：hello はコマンドですか？
    
回答：この場合はコマンドと呼べます。

ご利用ありがとうございます。

> この授業で作ったhelloはファイルではなくコマンド扱いなんですか？
> 

コマンドの定義によると思いますが、`コンピュータに特定の機能の実行を指示する命令`というのが一般的な解釈ですので、実行権限がついていて、実行可能なファイルである`hello`もコマンドと言っても良いかと思います。

> viコマンドで作られたhelloはファイル扱いではないのですか？
> 

先の説明とも重複するのですが、実行可能なファイルですので`hello`は、ファイルでもありコマンドでもあると言えます。
### 要点
コマンドとファイルの間で、相互にやり取りをすることができるリダイレクションについて学んでいきます。

- >：コマンドからファイルに書き込むことができる。
- >>：末尾に追記することができる。
- <：ファイルの内容をコマンドに流し込む。
  - これらの記号は、リダイレクションと呼ぶ。</details>


<details><summary>#26 パイプを使ってみよう</summary>

- コマンドの実行結果をファイルではなくて、別のコマンドに渡す方法について。
    - パイプという仕組みについて。
        - たとえば `ls -l /etc` とすると、以下のような結果になりますが、この中から sudo という文字列が含まれる行を抜き出したかったとしましょう。その場合 `grep` と合わせて使いたいのですが、パイプを使うにはコマンドのあとに `|` を入力して、その後ろに渡したいコマンドを書きます。
            
            ```bash
            dotinstall:~ $ ls -l /etc/ # (lsコマンドに-lオプションを付けて)etcディレクトリの詳細を表示せよ。
            total 208
            -rw-r--r--    1 root     root             7 May 29  2020 alpine-release
            drwxr-xr-x    1 root     root          4096 Sep 23  2020 apk
            drwxr-xr-x    3 root     root          4096 Sep 23  2020 ca-certificates
            -rw-r--r--    1 root     root          5613 Jun 18  2020 ca-certificates.conf
            drwxr-xr-x    2 root     root          4096 May 29  2020 conf.d
            drwxr-xr-x    2 root     root          4096 May 29  2020 crontabs
            -rw-r--r--    1 root     root            89 May 29  2020 fstab
            -rw-r--r--    1 root     root           693 Sep 23  2020 group
            -rw-r--r--    1 root     root           682 May 29  2020 group-
            -rw-r--r--    1 root     root            13 Aug 27 13:17 hostname
            -rw-r--r--    1 root     root           178 Aug 27 13:17 hosts
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
            lrwxrwxrwx    1 root     root            12 Aug 27 13:17 mtab -> /proc/mounts
            drwxr-xr-x    8 root     root          4096 May 29  2020 network
            drwxr-xr-x    2 root     root          4096 May 29  2020 opt
            -rw-r--r--    1 root     root           164 May 29  2020 os-release
            -rw-r--r--    1 root     root          1233 Sep 23  2020 passwd
            -rw-r--r--    1 root     root          1172 May 29  2020 passwd-
            drwxr-xr-x    7 root     root          4096 May 29  2020 periodic
            -rw-r--r--    1 root     root           238 May 29  2020 profile
            drwxr-xr-x    1 root     root          4096 Sep 23  2020 profile.d
            -rw-r--r--    1 root     root          1865 May 29  2020 protocols
            -rw-r--r--    1 root     root            54 Aug 27 13:17 resolv.conf
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
            dotinstall:~ $ ls -l /etc/ | grep 'sudo' # ls -l /etc/コマンドの後に|、その後に渡したいコマンドを入力する。
            -rw-r--r--    1 root     root          3941 May 25  2020 sudo.conf
            -rw-r--r--    1 root     root          6169 May 25  2020 sudo_logsrvd.conf
            -rw-r--r--    1 root     root          3228 Sep 23  2020 sudoers
            drwxr-x---    2 root     root          4096 Sep 23  2020 sudoers.d
            -r--r-----    1 root     root          3174 May 25  2020 sudoers.dist
            ```
            
        - パイプは組み合わせることができて、さらにそのあとにパイプを使って `wc -l` としてみましょう。結果の行数を返してくれます。
            
            ```bash
            -rw-r--r--    1 root     root          3941 May 25  2020 sudo.conf
            -rw-r--r--    1 root     root          6169 May 25  2020 sudo_logsrvd.conf
            -rw-r--r--    1 root     root          3228 Sep 23  2020 sudoers
            drwxr-x---    2 root     root          4096 Sep 23  2020 sudoers.d
            -r--r-----    1 root     root          3174 May 25  2020 sudoers.dist
            dotinstall:~ $ ls -l /etc/ | grep 'sudo' | wc -l # 検索結果の数を行数で表示せよ。
            5
            ```
            
        - 前回見たリダイレクションと組み合わせることもできるので、たとえば results.txt というファイルに結果を書き出したい場合は以下のように入力します。
            
            ```bash
            dotinstall:~ $ ls -l /etc/ | grep 'sudo' | wc -l > results.txt # wc -lで得た結果をresultx.txtファイルに書き出せ。
            dotinstall:~ $ cat results.txt # (catコマンドで)results.txtファイルの中身を表示せよ。
            5
            ```

※UNIX ではこのようにパイプやリダイレクションを組み合わせることで複雑な処理を行うこともできるので、慣れておくといいでしょう。
### 要点
コマンドの実行結果を、別のコマンドに渡すためのパイプという仕組みについて見ていきます。

- |(パイプ)：コマンドの実行結果を別のコマンドに渡す。
- リダイレクションとの組み合わせ：コマンドの実行結果をファイルに書き出すことができる。
  - パイプやリダイレクションを組み合わせることで複雑な処理を行うこともできる。</details>


<details><summary>#27 ブレース展開を使ってみよう</summary>

- 今回使っているシェルではブレース展開という機能が使えるので見ていきましょう。
    - ブレースとは波括弧のことです。たとえば `echo {a,b,c}` とすると、それを展開してくれます。
        
        ```bash
        dotinstall:~ $ echo {a,b,c}
        a b c
        ```
        
    - さらに連続する値も表現することができて、 `echo {1..10}` とすると 1 から 10 、さらにアルフベットを組み合わせたいのだったら `{a..g}` とすると、数式のように組み合わせて展開します。
        
        ```bash
        dotinstall:~ $ echo {1..10}{a..g}
        1a 1b 1c 1d 1e 1f 1g 2a 2b 2c 2d 2e 2f 2g 3a 3b 3c 3d 3e 3f 3g 4a 4b 4c 4d 4e 4f 4g
        5a 5b 5c 5d 5e 5f 5g 6a 6b 6c 6d 6e 6f 6g 7a 7b 7c 7d 7e 7f 7g 8a 8b 8c 8d 8e 8f 8g
        9a 9b 9c 9d 9e 9f 9g 10a 10b 10c 10d 10e 10f 10g
        ```
        
    - これを知っておくと色々便利なので、練習用のフォルダを作って試してみましょう。
        
        ちなみに、ふたつのコマンドを連続して実行したい場合は `mkdir test` のようにひとつのコマンドを書いてあげて、それが成功したら次のコマンドを実行したい場合、 `&&` (アンパサンド2つ)で次のコマンド、と書いてあげます。
        
        ```bash
        dotinstall:~ $ mkdir test && cd test # mkdirコマンドでtestファイルを作成し、続けて、testファイルに移動せよ。
        dotinstall:~/test $ # testファイルが作成され、さらにtestファイルに移動した。そのためプロンプトの内容が変わっている。
        ```
        
    - ブレース展開を使用して一気にディレクトリを作成します。`mkdir app{1..5}` としてあげると、 app1 から app5 までが作られます。
        
        ```bash
        dotinstall:~/test $ mkdir app{1..5} # mkdirコマンドでappディレクトリを作成しその中身にはapp1からapp5までが作成されるようにしろ。。
        dotinstall:~/test $ ls
        app1  app2  app3  app4  app5
        ```
        
    - それぞれのディレクトリの中にたくさんのファイルを一気に作成します。touch コマンドを使ってあげて、 `app{1..5}/test{1..3}{.jpg,.png,.gif}` と書いてみましょう。これを実行してあげると、 app1 から 5 の中に test1 から test3 でそれぞれの拡張子がついたファイルができます。
        
        ```bash
        dotinstall:~/test $ touch app{1..5}/test{1..3}{.jpg,.png,.gif} # app1からapp5の中にtest1からtest3でそれぞれの拡張子がついたファイルを作成する。
        dotinstall:~/test $ ls app2 # app2ファイルの中身を確認せよ。
        test1.gif  test1.png  test2.jpg  test3.gif  test3.png # test1からtest3に拡張値がそれぞれ付いている。
        test1.jpg  test2.gif  test2.png  test3.jpg
        ```
        
    - ↑この中から .jpg と .gif だけを削除したいなら、同じようにブレース展開が使えて、 `rm app{1..5}/test{1..3}{.jpg,.gif}` と書きます。
        
        ```bash
        dotinstall:~/test $ rm app{1..5}/test{1..3}{.jpg,.gif} # app1からapp5の中のtest1からtest3の.jpgと.gifを削除せよ。
        dotinstall:~/test $ ls app2 # (lsコマンドでファイルの中身を確認)app2ファイルの中身を確認せよ。
        test1.png  test2.png  test3.png # .jpgと.gifが削除され、.pngが残っている。
        ```
        
    - 最後に、一旦 cd でホームディレクトリに戻り、 test ディレクトリの中身は一気に消します。
        
        ```bash
        dotinstall:~/test $ cd # (cdコマンドでディレクトリに戻る)ホームディレクトリに戻れ。
        dotinstall:~ $ rm -r test/ # (rmコマンドに-rオプションを付けてディレクトリを丸ごと削除する)testファイルを削除せよ。
        ```
        

※このようにブレース展開を使えばかなり複雑なことも一気にできるようになるので、使いこなせるようになっておくといいでしょう。
### 要点
シェルで使えるブレース展開について解説していきます。

- {}：ブレースと呼び、波括弧を意味する。
- &&：二つのコマンドを連続して実行したい場合に使用する。</details>


<details><summary>#28 findでファイルを検索しよう</summary>

- ファイルの検索について見ていきますが、事前にブレース展開で幾つかファイルを作ります。
    - mkdir -p で test ディレクトリ内に app1 から app5 を作成する。
        
        その中にさらにファイルを作成する。
        
        ```bash
        dotinstall:~ $ mkdir -p test/app{1..5} # (mkdirコマンドに-pオプションを付けて、深い階層までディレクトリを作成する)testディレクトリ内にapp1からapp5までを作成せよ。
        
        dotinstall:~ $ touch test/app{1..5}/app{1..3}{.jpg,.png,.gif} # (touchコマンドでファイルを作成する)app1からapp5までを作成し、それぞれのファイルにはapp1からapp3まではそれぞれの拡張子を付けたものにせよ。。
        dotinstall:~ $ ls test # (lsコマンドでディレクトリの中身を確認)testディレクトリの中身を確認せよ。
        app1  app2  app3  app4  app5 # testディレクトリの中身にはapp1からapp5までが作成されている。
        dotinstall:~ $ ls test/app1 # (lsコマンドでディレクトリの中身を確認)testディレクトリの中のapp1ファイルの中身を確認せよ。
        app1.gif  app1.png  app2.jpg  app3.gif  app3.png
        app1.jpg  app2.gif  app2.png  app3.jpg
        ```
        
    - ↑ここから app3.png を検索します。検索するには find コマンドを使用する。 `find 場所を指定 -nameオプション 検索したいディレクトリの名前` と書く。
        
        ```bash
        dotinstall:~ $ find test -name 'app3.png' # (findコマンド、場所を指定(test)、-nameオプション、検索したいディレクトリ名)testディレクトリの中のapp3.pngファイルを検索せよ。
        test/app1/app3.png
        test/app2/app3.png
        test/app3/app3.png
        test/app4/app3.png
        test/app5/app3.png
        ```
        
    - ワイルドカードも使えるので、 `test -name 'app1*'` といった書き方もできます。
        
        ```bash
        dotinstall:~ $ find test -name 'app1*' # testディレクトリの中にapp1という文字列に該当するディレクトリを検索せよ。
        test/app1
        test/app1/app1.jpg
        test/app1/app1.png
        test/app1/app1.gif
        test/app2/app1.jpg
        test/app2/app1.png
        test/app2/app1.gif
        test/app3/app1.jpg
        test/app3/app1.png
        test/app3/app1.gif
        test/app4/app1.jpg
        test/app4/app1.png
        test/app4/app1.gif
        test/app5/app1.jpg
        test/app5/app1.png
        test/app5/app1.gif
        ```
        
    - ディレクトリではなくて、ファイルだけ検索したいという場合は最後に `-type f` と書きます。
        
        また、ディレクトリだけにしたい場合は `-type d` と書きます。
        
        ```bash
        dotinstall:~ $ find test -name 'app1*' -type f # 最後に-type fを付けるとファイルだけを検索してくれる。
        test/app1/app1.jpg # ディレクトリが除外されている。
        test/app1/app1.png
        test/app1/app1.gif
        test/app2/app1.jpg
        test/app2/app1.png
        test/app2/app1.gif
        test/app3/app1.jpg
        test/app3/app1.png
        test/app3/app1.gif
        test/app4/app1.jpg
        test/app4/app1.png
        test/app4/app1.gif
        test/app5/app1.jpg
        test/app5/app1.png
        test/app5/app1.gif
        
        dotinstall:~ $ find test -name 'app1*' -type d # 最後に-type dを付けるとディレクトリだけを検索してくれる。
        test/app1
        ```

※find は奥が深いのですが、使いこなせるようになっておくと便利です。
### 要点
ファイルの検索をすることができるfindコマンドについて学んでいきます。

- find：ディレクトリやファイルを検索してくれるコマンド。
    - `find 場所を指定 -nameオプション 検索したいディレクトリの名前` これが基本の型。
- ワイルドカードとの組み合わせ：`test -name 'app1*'`
- type f：`find 場所を指定 -nameオプション 検索したいディレクトリの名前 -type f` 、ファイルだけを検索してくれる。
- type d：`find 場所を指定 -nameオプション 検索したいディレクトリの名前 -type d`、ディレクトリだけを検索してくれる。</details>


# 💻 ドットインストール シェルスクリプト入門
### Unixのコマンドをまとめて実行できるシェルスクリプトについて学んでいきます。 

<details><summary>#01 シェルスクリプトを使ってみよう(レッスンを受けるためのローカル開発環境が必要なので、準備が要る)</summary>

- Unix を操作していると、よく行う処理をまとめたくなる場合があります。今回のレッスンでは、そうした場合に使えるシェルスクリプトについて見ていきます。
    - その前に shellscript_lessons という名前のディレクトリを作成。
        1. Desktop からフォルダを新規作成。名前は shellscript_lessons 。
        2. ターミナルまたは iTerm でプロンプトを作成した shellscript_lessons に移動。
        3. Visual Studio Code を起動→ファイルタブからフォルダーを開くをクリック→先ほど作成した shellscript_lessons ディレクトリを選択→shellscript_lessons ディレクトリから新しいファイルをクリック→hello という名前で新しくファイルを作成。
        4. 編集しやすいようにモードを変更する。
        5. Visual Studio Code 下部にある「プレーンテキスト」をクリックしてモードの変更を行う。
        6. モードは「Shell Script」を選択。
				7. ここまでできれば、Visual Studio Code にいろいろなコマンドを書きながらレッスンを進むことができる。
- 準備したVisual Studio Code にいろいろなコマンドを書いていくのですが、その前にコマンドを実行するためのプログラムを1行目で指定します。
    1. `#!` (シェバンまたはシバン)を入力。
    2. シェルで `which bash` を入力、実行して、表示された `/bin/bash` をコピーして#!の後ろに貼り付ける。
        
        ```bash
        #!/bin/bash
        
        echo hello
        ```
        
- これを保存して実行したいのですが、 ls -l で確認すると実行権限(execute)がないことがわかります。
    
    そこで、 `chmod +x hello` で実行権限(execute)を与えます。
    
    実行するのですが、 shellscript_lessons ディレクトリはコマンドの実行PATH に含まれていないので、 `./hello` と書きます。
    
    ```bash
    % ls -l # (lsコマンドに-lオプションを付けて)ディレクトリの詳細を表示せよ。
    total 8
    -rw-r--r--  1 yoshiwo  staff  23  8 29 16:51 hello # userの権限がr(読み取り)とw(書き込み)の2つだけ。
    
    % chmod +x hello # (chmodコマンドでexecuteの権限を付与する)ユーザーに実行権限(execute)を付与せよ。
    % ls -l
    total 8
    -rwxrwxr-x  1 yoshiwo  staff  23  8 29 16:51 hello
    
    % ./hello # shellscript_lessonsディレクトリはコマンドの実行PATHに含まれていないため、./helloと書く。
    hello # 文字列helloが表示される。
    ```

※シンプルな例ですが、先ずはこのような流れに慣れておいてください。
### 要点
簡単なシェルスクリプトを作って実行するところまでを見ていきます。

- シェルスクリプトの作成：shellscript ディレクトリの作成→hello ファイルの作成→Visual Studio Code のモードをShellScript に変更。
- 実行権限の付与：chmod コマンドを使用して、ユーザーに実行権限(execute)を付与する。
- シェルスクリプトの実行：shellscript ディレクトリにはコマンドの実行PATH に含まれていないので、`./hello` で実行する。
	- ./hello で今いるディレクトリの中のhelloを実行せよ、という意味になる。</details>


<details><summary>#02 文字列を表示してみよう</summary>

- echo は改行付きで値を表示するための命令です。
    - 文字列はそのまま書かれることも多いのですが、文字列だと明示したり、空白を入れてまとめて文字列として扱いたい場合は " か、もしくは ' で囲います。
        - " と ' で動作に違いがあるのですが、その点についてはあとで説明していきます。
        - 命令は基本的に改行で区切って書いていけば OK なのですが、 1 行に複数の命令を書きたい場合は、;(セミコロン) で区切ります。
            
            ```bash
            #!/bin/bash
            
            echo "hello world"
            echo 'hello world'
            
            echo "foo"; echo "bar"
            
            % ./hello
            hello world
            hello world
            foo
            bar
            ```
            
    - コメントの書き方
        - #(パウンド記号)を先頭に書くと文末までがコメントになります。実行結果に関係ない自分だけのメモ書きや、例えば一時的に命令を実行させないようにするためにコメントを使うこともあるので、覚えておくといいかと思います。
### 要点
文字列を表示するための記法やコマンドについて見ていきます。

- echo：改行付きで値を表示するための命令。
- 文字列の表現：文字列を明示、空白を入れてまとめて文字列として扱いたい場合は ” または ‘ で囲う。
- ;：1行に複数の命令を書きたい場合、; で区切る。
- コメントの書き方：先頭に #(パウンド記号)を書くと、文末までコメント扱いになる。</details>


<details><summary>#03 変数を使ってみよう</summary>

- 以下の文字列のうち、名前だけを変更したかった場合を考えます。
    
    ```bash
    #!/bin/bash
    
    echo "morning taguchi"
    echo 'hello taguchi'
    echo 'hello taguchi'
    
    % ./hello
    morning taguchi
    hello taguchi
    hello taguchi
    ```
    
    - 1つずつ変更しても良いのですが、数が増えてきたら大変です。そうした場合に、値(今回は名前)を1箇所で管理できたら便利です。そのために使えるのが変数です。変数は値に付けるラベルのようなもので、ラベルの書かれた名前で演算をしたり、使いまわしたりすることができるので見ていきます。
        - taguchi という文字列を name という変数に割り当てます。
            
            ここで幾つか注意すべき点があります。
            
            1. 変数名は、英数字か _ (アンダーバー)しか使用できません。
            2. 大文字小文字は区別されます。
            3. 一番間違えやすいのですが、 `name = “taguchi”` のようにスペースを入れてしまうとエラーになります。値を割り当てるには、必ず、 = の前後に空白がないようにしてください。
            
            割り当てたら、 taguchi という値の代わりに name を使用します。
            
        - 割り当てた変数を使用するには、 $ の後に変数名を付けます。こうすることで、 taguchi と全く同じ意味になります。
            - 例えば `echo “bye$namesan"` のように、変数の後に文字が続く場合は、どこまでが変数名なのか分かりにくいです。その場合は `echo “bye ${name}san”` のように { } で囲うことで、変数を示すことができるので、どちらの書き方でもできるようにしましょう。
                
                ```bash
                #!/bin/bash
                # 変数
                
                # name = "taguchi"
                name="taguchi"
                
                # echo "morning taguchi"
                # echo "hello taguchi"
                # echo "hello taguchi"
                echo "morning $name"
                echo "hello $name"
                echo "hello ${name}san"
                
                % ./hello
                morning taguchi
                hello taguchi
                hello taguchisan
                
                # 変数の値を書き換えると結果が変わる
                #!/bin/bash
                # 変数
                
                # name = "taguchi"
                # name="taguchi"
                name="fkoji"
                
                # echo "morning taguchi"
                # echo "hello taguchi"
                # echo "hello taguchi"
                echo "morning $name"
                echo "hello $name"
                echo "hello ${name}san"
                
                % ./hello
                morning fkoji
                hello fkoji
                hello fkojisan
                ```
                
        - ちなみに内容を書き換えてほしくない変数を作成したいときには、 readonly というキーワードを付けます。
            
            ```bash
            readonly name="fkoji"
            name="dotinstall"
            
            # echo "morning taguchi"
            # echo "hello taguchi"
            # echo "hello taguchi"
            echo "morning $name"
            echo "hello $name"
            echo "hello ${name}san"
            
            % ./hello
            ./hello: line 7: name: readonly variable # 7行目変数nameのエラー、読み込みのみの変数が可能。
            morning fkoji
            hello fkoji
            hello fkojisan
            ```
            
- ‘ (シングルクォーテーション)と “ (ダブルクォーテーション)で囲んだ時の違いについて。
    - ‘ (シングルクォーテーション)を使用すると変数の中身が展開されません。そのまま表示されてしまいます。こういった挙動の違いも理解しましょう。
        
        ```bash
        echo "morning $name"
        echo "hello $name"
        echo "hello ${name}san"
        echo 'hello ${name}san'
        
        % ./hello
        morning fkoji
        hello fkoji
        hello fkojisan
        hello ${name}san # '(シングルクォーテーション)で囲った場合は、そのまま表示されてしまう。
        ```

### 要点
データに名前を付けられる変数の使い方について見ていきます。

- 変数の付け方：`変数=値` とする。
    - 変数名は、英数字か _ (アンダーバー)しか使用できません。
    - 大文字小文字は区別されます。
    - 一番間違えやすいのですが、 `name = “taguchi”` のようにスペースを入れてしまうとエラーになります。値を割り当てるには、必ず、 = の前後に空白がないようにしてください。
- 値の取り出し方：$の後に変数名を付けること。
    - 今回の場合は `$name` 。
    - それ以外にも文字列と変数を分けるため、変数を { } で囲う方法がある。 `${name}san`</details>


<details><summary>#04 特殊変数を使ってみよう</summary>

- 実行時に値を渡し、その値を処理の中で使用したい場合を考えます。
    - その場合は、コマンドの引数を表す特殊変数を使用すれば良いです。
        - 特殊変数は、最初の引数は $1 、次の変数は $2 と表現します。
            
            例えば `echo "hello $1"` として、スクリプトの方で `./hello taguchi` を渡すと、 hello taguchi と表示されます。
            
            ```bash
            #!/bin/bash
            
            # $1, $2, ...
            echo "hello $1"
            
            % ./hello taguchi
            hello taguchi
            
            #!/bin/bash
            
            # $1, $2, ...
            echo "hello $1"
            
            % ./hello fkoji
            hello fkoji
            ```
            
        - 特殊変数には他にもあります。
            1. `$0` でスクリプトの名前
            2. `$#` で引数の数
            3. `$@` 若しくは `$*` で全ての引数
                
                を取得することができます。特殊変数はよく使用するので慣れておきましょう。
                
                ※スクリプト：「書いて、すぐ実行できるプログラム」のこと。
                
                ```bash
                # ./hello a aa aaa
                echo $0 # ./hello スクリプトの名前が表示される。
                echo $# # 3 引数の数が表示される。
                echo $@ # $* a aa aaa 全ての引数が表示される。
                
                % ./hello a aa aaa
                ./hello # スクリプトの名前
                3 # 引数の数
                a aa aaa # 全ての引数
                ```

### 要点
実行時のパラメーターなどを取得することができる特殊変数について見ていきます。

- $1, $2, ...：特殊変数。引数の番目を表す。
- $0：特殊変数。スクリプトの名前を表示する。※「書いて、すぐ実行できるプログラム」のことを指す。
- $#：特殊変数。引数の数を表示する。
- $@, $*：特殊変数。全ての変数を表示する。</details>


<details><summary>#05 ユーザーに入力してもらおう</summary>

- 実行時にユーザーから入力を受け付ける方法。
    - read という命令を使用して、 `read name` とすると、ユーザーから1行の入力を受け取って name に格納します。
        
        ```bash
        #!/bin/bash
        
        read name
        echo "hello $name"
        
        % ./hello # ここでreturnキーを押すと、次が入力待ちになる。
        yoshiwo # 入力待ちの状態で、入力してreturnキーを押す。
        hello yoshiwo # 文字列と入力した内容が表示される。
        ```
        
- 入力前にテキストを表示する方法。
    - -p (プロンプト)オプションを使用して、 `read -p “Name: “ name` と書きます。
        
        ```bash
        #!/bin/bash
        
        # read name
        # echo "hello $name"
        read -p "Name: " name # -p(プロンプト)オプション
        echo "hello $name"
        
        % ./hello
        Name: yoshiwo # 入力待ちの状態で、かつ、テキストを表示。
        hello yoshiwo
        ```
        
- 複数の値を一度に複数の変数に割り当てる方法。
    - 受け取る変数は c1 c2 c3 として、その後に $c1 $c2 $c3 を表示する。
        
        ```bash
        read -p "Pick 3 colors: " c1 c2 c3 # 受け取る変数はc1 c2 c3とする。その後に、$c1 $c2 $c3を表示させる。
        echo $c1
        echo $c2
        echo $c3
        
        % ./hello
        Pick 3 colors: red blue green
        red
        blue
        green
        ```
        
    - ちなみに、ここで4つの値を入れてしまうと、最後が2つになることに注意しましょう。
        
        ※余った部分は一番最後の変数に行く。
        
        ```bash
        read -p "Pick 3 colors: " c1 c2 c3 # 受け取る変数はc1 c2 c3とする。その後に、$c1 $c2 $c3を表示させる。
        echo $c1
        echo $c2
        echo $c3
        
        % ./hello
        Pick 3 colors: red blue green pink # 4つの値を入力すると......。
        red
        blue
        green pink # 最後の値が2つになる。 # 余った部分は一番最後の変数に行くので注意。
        ```
        
    - 2つの場合は、c1 c2 に値が格納され、 c3 には格納されないので知っておきましょう。
        
        ```bash
        read -p "Pick 3 colors: " c1 c2 c3 # 受け取る変数はc1 c2 c3とする。その後に、$c1 $c2 $c3を表示させる。
        echo $c1
        echo $c2
        echo $c3
        
        % ./hello
        Pick 3 colors: red blue
        red # c1 c2には値が格納されるがc3には格納されない。
        blue
        ```
        
### 質問：c1 や c2 と $1 や $2 の違いはなんですか？
    
回答：c1 、c2 は変数名、$1 、$2 は引数の番目を表します。

> readの引数で「c1」や「c2」と指定されていましたが前回(#4)の動画で紹介されていた「$1」や「$2」で指定するのとは若干意味合いが違いますでしょうか？
> 

そうですね、readに渡している引数は「この名前の変数に値を格納する」という意味になりますので、例えば`read $1`のように書いた場合、もしすでに`$1`になにか値が格納されていればその値の名前の変数に値が割り当てられます。`$1`になにも値がない場合は`read`を引数無しで実行した場合と同じです。

> 本動画内で利用している「c1」や「c2」は変数、「$1」や「$2」で指定すると◯番目の引数という意味合いになる認識であっていますでしょうか？
> 

そうですね、`read c1 c2`とした場合の`c1`、`c2`は変数名でこの名前の変数に`read`が値を格納します。格納された値は`$c1`、`$c2`として参照することができます。シェルスクリプトの`$1`、`$2`はコマンドの引数を意味する特殊な変数でご認識の通り◯番目の引数を意味します。
### 要点
readを使ってユーザーから入力を受け付ける方法を見ていきます。

- read：コマンド実行時にユーザーから入力を受け付ける。
- pオプション：プロンプトオプションのこと。入力受付前にテキストを表示することができる。
- 複数の値の取得：「受け取る変数」と「(それを)表示する特殊変数」をそれぞれ書くことで表示が可能になる。</details>


<details><summary>#06 配列を使ってみよう</summary>

