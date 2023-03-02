# 💻 dotinstall シェルスクリプト入門
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

- 複数の値を1つの変数で管理できる配列について。
    - 配列に入れたい複数の値は、 ( ) の中に書きます。
        
        それぞれの要素にアクセスしたい場合は、`${変数名[0から始まる添字]}` と書きます。`${colors[0]}` `${colors[1]}` `${colors[2]}` はそれぞれ0番目、1番目、2番目となり、red blue pink の結果になります。
        
        全ての要素を表示したい場合は、 [ ] の中を @ にします。
        
        要素の個数を表示したい場合は、変数名の前に # を付けます。
        
        ```bash
        colors=(red blue pink)
        echo ${colors[0]} # 0番目 red
        echo ${colors[1]} # 1番目 blue
        echo ${colors[2]} # 2番目 pink
        echo ${colors[@]} # 全ての要素が表示される red blue pink
        echo ${#colors[@]} # 要素の個数が表示される 3
        
        yoshiwo@Yoshiwos-MacBook-Pro shellscript_lessons % ./hello
        red
        blue
        pink
        red blue pink
        3
        ```
        
    - 要素の変更をしたい場合、例えば1番目の blue を silver に変更するには、`colors[1]=silver` と書きます。
        
        末尾にいくつか追加したい場合、+= 記号を使用して、例えば `colors+=(green orange)` と書きます。
        
        ```bash
        colors=(red blue pink)
        # echo ${colors[0]} # 0番目 red
        # echo ${colors[1]} # 1番目 blue
        # echo ${colors[2]} # 2番目 pink
        # echo ${colors[@]} # 全ての要素が表示される red blue pink
        # echo ${#colors[@]} # 要素の個数が表示される 3
        
        colors[1]=silver
        colors+=(green orange)
        echo ${colors[@]}
        
        yoshiwo@Yoshiwos-MacBook-Pro shellscript_lessons % ./hello
        red silver pink green orange
        ```

### 要点
複数の値をまとめて扱うことができる配列について見ていきます。

- 配列の作成：配列に入れたい複数の要素は ( ) の中に書く。
- 要素へのアクセス：`${変数名[0から始まる添字]}` と書く。
- すべての要素の取得： [ ] の中を @ にする。
- 要素の個数：変数名の前に # を付ける。
- 配列の変更
    - 要素の変更をしたい場合、例えば1番目の blue を silver に変更するには、`colors[1]=silver` と書きます。
  	- 末尾にいくつか追加したい場合、+= 記号を使用して、例えば `colors+=(green orange)` と書きます。</details>


<details><summary>#07 数値計算をしてみよう</summary>

- 数値計算をやっていきます。
    - Bash は基本的に値は文字列として処理されます。そのため `echo 5+2` と書いても、7 にはならず、単に 5+2 の文字列として表示されます。
        
        ```bash
        #!/bin/bash
        
        echo 5+2
        
        % ./hello
        5+2
        ```
        
        - 計算をするためのいくつかの方法。
            1. コマンドの実行結果を返す `` (バッククォート)を使用する方法。
                1. 例えば、式を評価する expr (エクスプレッション)コマンドを使用して `echo `expr 5 + 2`` と書くと 7 になります。
                    
                    ```bash
                    echo `expr 5 + 2`
                    
                    % ./hello
                    7
                    ```
                    
                    ただ、 `` (バッククォート)は一部の記号をエスケープする必要があり使いにくいので、最近では (( )) 二重丸括弧をよく使用します。
                    
            2. `` (バッククォート)ではなく、 (( )) 二重丸括弧を使用する方法。最近ではこちらがよく使用されている。但し、計算結果を取り出すときは変数と同じように $ をつける必要があります。
                
                ```bash
                echo $((5 + 2)) # 計算結果を取り出すためには、()の前に$を付けること。
                
                % ./hello
                7
                ```
                
                1. (( )) 二重丸括弧の中で使用する変数には、$ がいらない点に注意しましょう。
                2. 例えば n=5 で n に n+5 を足したかった場合は (($n=$n+5)) と書く必要はなく、単に `((n=n+5))` と書きましょう。
                    
                    ```bash
                    n=5 # 変数の定義。文字列nと数字5を紐付けろ。
                    # (($n=$n+5))
                    ((n=n+5)) # 計算式、n+5のnにn=5を代入して計算した値を左側のnに紐付けろ。
                    echo $n # (計算式の結果)nの値を表示せよ。
                    
                    % ./hello
                    10
                    ```
                    
            3. 計算に使用する演算子について。
                1. 足し算が + 、引き算が - 、そして掛け算が * 、 / が商、 % が余り、 ** がべき乗、 ++ が 1 足す、 -- が 1 引く、になります。
                    
                    ```bash
                    # + 足し算、 - 引き算、 * 掛け算、 / 割り算、 % 余り、 ** べき乗、 ++ 1足す、 -- 1引く
                    ```
                    
            4. ちなみに Bash では基本的に整数の演算しかできないので、例えば `echo $((10 / 3))` としてあげると 3.333 … ではなく単に 3 が返されます。
                
                ```bash
                echo $((10 / 3)) # 3 整数が表示される。
                
                % ./hello
                3
                ```
                
                数値演算をする方法は他にもありますが、まずはこの辺りを押さえましょう。
### 要点
Bashで数値計算をするいくつかの方法について見ていきます。

- `expr ...`：式を評価するexpr (エクスプレッション)コマンド。`` (バッククォート)でコマンドの実行結果を返す。が、一部の記号をエスケープする必要があったりと使用しにくいため、最近では (( )) 二重丸括弧が使われる。
- (( ))：二重丸括弧。この括弧の中で計算を行う。行った計算結果を表示させるには括弧の前に $ を付ける必要がある。
- 演算子：足し算が + 、引き算が - 、そして掛け算が * 、 / が商、 % が余り、 ** がべき乗、 ++ が 1 足す、 -- が 1 引く……などがある。</details>


<details><summary>#08 ifで条件分岐をしてみよう</summary>

- if を使用した条件分岐を見ていきます。
    - 例) `read -p “Name? “ name` で名前を訊いた時、もし name が taguchi なら welcome! と表示したいとします。その場合は `if test` と書き、次に `“$name” = “taguchi”` とチェックしたい条件を書きます。
        
        test をパスした場合の処理を `then` の後に書きます。
        
        最後に処理を終了させるには、 `if` を逆にした `fi` を書きます。
        
        尚、 `$name` には空白が含まれる可能性があるので、 “” で囲っている点に注意しましょう。
        
        ```bash
        #!/bin/bash
        # if
        
        read -p "Name? " name
        if test "$name" = "taguchi"
        then
          echo "welcome"
        fi
        ```
        
    - test にはもう1つの書き方が用意されています。`if [ “$name” = “taguchi” ]` のように [ ] 大括弧で囲っても同じ意味になります。ここの [ ] 大括弧はコマンドなので、続く文字列が引数になるようにそれぞれの間にきちんと空白を入れます。
        
        ```bash
        #!/bin/bash
        # if
        
        read -p "Name? " name
        # if test "$name" = "taguchi"
        if [ "$name" = "taguchi" ] # []はコマンド。スペースに気を付けること。
        then
          echo "welcome"
        fi
        
        yoshiwo@Yoshiwos-MacBook-Pro shellscript_lessons % ./hello
        Name? taguchi # Name?とテキストが表示され、入力待ちになる。
        welcome # testをパスすると、welcomeが表示される。
        
        # 別の名前を入れると
        yoshiwo@Yoshiwos-MacBook-Pro shellscript_lessons % ./hello
        Name? yoshiwo # 下にwelcomeが表示されない。
        ```
        
    - test に失敗した時の処理を書くには、else に繋いでさらに書いていきます。例えば `echo "you are not allowed!”` 。
        
        さらに条件を追加したい場合は、elif でさらに条件を `[ “$name” = “fkoji” ]` のように書きます。
        
        ```bash
        #!/bin/bash
        # if
        
        read -p "Name? " name
        # if test "$name" = "taguchi"
        if [ "$name" = "taguchi" ]
        then
          echo "welcome"
        elif [ "$name" = "fkoji" ]
        then
          echo "welcome, too"
        else
          echo "you are not allowed"
        fi
        ```
        
    - then に1行使わずに、条件の行と一緒に書く方法もよく見かけるので、それも覚えましょう。
        
        ```bash
        if [ "$name" = "taguchi" ]; then
          echo "welcome"
        elif [ "$name" = "fkoji" ]; then
          echo "welcome, too"
        else
          echo "you are not allowed"
        fi
        ```

### 要点
ifを使って条件分岐をする方法について見ていきます。

- if ... then ... fi：条件分岐は if から始まり、条件をパスした時の処理を then の後に書き、 fi で処理を終了させる。
- if ... elif ... else ... fi：さらに条件を追加したい場合の elif（エルスイフ)、パスできなかった場合の処理を書くには else に繋いで書く。</details>


<details><summary>#09 文字列の比較をしてみよう</summary>

- 文字列の比較について。
    - #08で見た test や [ ] は古い書き方で、今は文字列やファイルの比較には [[ ]] 二重大括弧、数値の比較には (( )) 二重丸括弧がよく使われます。
        - 前回のコードでは、文字列の比較をしているので、[[ ]] 二重大括弧が使われます。[[ ]] 二重大括弧を使用した場合は、”$name” の “” は要りません。
            
            ```bash
            if [[ $name = "taguchi" ]]; then # 文字列の比較なので二重大括弧を使用。"$name"に""は不要。
              echo "welcome"
            fi
            ```
            
        - [[ ]] を使った場合、比較のための演算子は他にもあり、文字列の場合、等しいかどうかは = か == で調べることができて、等しくないは != 、もしくは文字列の長さが 0 かどうかは -z 、そして正規表現は =~ で調べることができます。
            
            ※正規表現：[文字列](https://wa3.i-3-i.info/word1436.html)を指定する際に「これ！」とピンポイントで指定するのではなく「こんな感じ！」とちょっと幅を持たせて指定できる書き方。
            
            ```bash
            # 比較のための演算子文字列の場合 等しいかどうかは = ==、
            # 等しくない !=
            # 文字列の長さが0かどうか -z
            # 正規表現 =~ で調べることができる。
            ```
            
            例）名前の長さが0だった場合に empty… というメッセージを出す。
            
            その場合には `if [[ -z $name ]]; then echo “empty …” fi` と書きます。
            
            ```bash
            if [[ -z $name ]]; then # もし文字列の長さが0の場合は以下の内容を処理せよ。
              echo "empty ..." # 文字列「empty ...」を表示。
            fi # 条件分岐終了。
            
            % ./hello
            Name? # 入力待ちの状態でreturnキーを押すと。
            empty ... # 「empty ...」が表示される。
            ```
            
            例）正規表現の場合。名前が t で始まる場合は starts with t… と表示させる。
            
            ```bash
            if [[ $name =~ ^t ]]; then # 変数nameの値がtから始まる場合は以下の内容を処理せよ。
              echo "starts with t..." # 文字列「starts with t...」を表示。
            fi # 条件分岐終了。
            
            % ./hello
            Name? yoshiwo
            % ./hello
            Name? tontyan
            starts with t...
            ```
            
            他にもいろいろなことができるのですが、まずは文字列の比較として、この辺りの挙動に慣れておいてください。

### 要点
文字列を比較するための記法について見ていきます。

- [[ ]]：文字列やファイルの比較に用いられる。二重大括弧を使用した場合は、”$name” の “” は不要。
- 演算子：[[ ]] を使った場合、比較のための演算子は他にもあり、文字列の場合、等しいかどうかは = か == で調べることができて、等しくないは != 、もしくは文字列の長さが 0 かどうかは -z 、そして正規表現は =~ で調べることができます。</details>


<details><summary>#10 ファイルや数値の比較をしてみよう</summary>

- 条件分岐でファイルの存在の判定にもよく使用されます。
    - 種類を問わず存在しているかどうか調べるには -e 、ファイルが存在しているかは -f 、ディレクトリが存在しているかどうかは -d で調べることができます。
        - 例）今使用しているこのスクリプトファイルが存在するかどうかの判定を行う。
            
            ファイルの判定には [[ ]] 二重大括弧を使用するので、 `if [[ -f $0 ]];` と書きます。
            
            もし存在していたら、 `file exists …` と書きましょう。※exist：存在する、実在する、という意味。
            
            $0 は特殊変数でスクリプトの名前を表示する。./hello はファイルなので、 file exists … になります。
            
            ※スクリプト：「書いて、すぐ実行できるプログラム」のことを指す。
            
            ```bash
            if [[ -f $0 ]]; then # $0は特殊変数でスクリプトの名前を表示する。もしもファイルの存在が真なら以下を実行せよ。
              echo "file exists ..." # 文字列「file exists ...」を表示せよ。
            fi # 条件分岐終了。
            
            % ./hello
            file exists ...
            ```
            
        - 例）もしも ./hello がディレクトリだった場合は `dir exists …` と表示する。※dir：ディレクトリのこと。
            
            ```bash
            if [[ -d $0 ]]; then # もしもディレクトリの存在が真なら以下を実行せよ。
              echo "dir exists ..." # 文字列「dir exists ...」を表示せよ。
            fi # 条件分岐終了。
            
            % ./hello
            ```
            
- 数値の比較について。
    - 数値演算の時に使用した (( )) 二重丸括弧を使います。
        - 例）Number をユーザーに入力してもらい、もしも n が10より大きかった場合はメッセージを出すようにします。
            
            (( )) を使用して `if((n > 10))` と書きます。
            
            二重丸括弧を使用した場合は、 `n > 10` の前後にスペースを入れる必要はないので覚えておきましょう。
            
            ```bash
            read -p "Number? " n
            if ((n > 10)); then
              echo "bigger than 10"
            fi
            
            % ./hello
            Number? 5
            % ./hello
            Number? 15
            bigger than 10
            ```
            
        - 比較のための演算子は、数値の場合では、等しいは == 、等しくないは !=、〇〇より大きい >、〇〇以上 >=、〇〇より小さい <、〇〇以下 <=、などが使えます。
            
            ```bash
            # == != > >= < <=
            ```
            
- (( )) 、[[ ]] には条件を組み合わせるための論理演算子も用意されています。
    - AND は &&、OR が ||、NOT は ! 、なのでそれらを使用して思った通りの条件を組み立てられるようになっておきましょう。
        
        ```bash
        # && || !
        ```

### 要点
ファイルの存在確認や数値の比較について説明していきます。

- ファイルの存在確認：ファイルの判定に必要な [[ ]] 二重大括弧を使用して、-f で調べることができる。
- 数値の比較方法：数値演算で用いる (( )) 二重丸括弧、比較演算子を使用する。</details>


<details><summary>#11 forでループ処理をしてみよう</summary>

- for によるループ処理を見ていきます。
    - 例）1 から 5 を出力したい場合、 `for i in 1 2 3 4 5` と書くと in の後の値の集合から一つずつ値を取り出して i に格納して、 `do … done` の間で処理で使用することができます。
        
        ```bash
        for i in 1 2 3 4 5
        do
        done
        ```
        
        ちなみに、単純な数の連番であれば bash のブレース展開を使用できるので覚えておきましょう。※ブレース：波括弧のこと。例えば {a..z} で a から z までの連番を1行にまとめて書くことができます。
        
        また、 do は1行にまとめて書くことが多いので、書けるようにしましょう。
        
        ```bash
        # for i in 1 2 3 4 5
        for i in {1..5} # ブレース展開で1から5をまとめることができる。
        do
          echo $i
        done
        
        for i in {1..5}; do # doは1行にまとめて書くことが多いので、このような書き方ができるようにすること。
          echo $i
        done
        
        % ./hello
        1
        2
        3
        4
        5
        ```
        
- 他のプログラミング言語で見るような構文も、用意されています。
    - 数値の演算で使用した (( )) 二重丸括弧で、 `for ((i=1; i<=; i++));` と書くと同じように 1 から 5 が表示されます。
        
        ```bash
        for ((i=1; i<=5; i++)); do
          echo $i
        done
        
        % ./hello
        1
        2
        3
        4
        5
        ```
        
- 配列を使用したい場合。
    - 例）`color=(red blue pink)` を for で回す。この時配列の全ての要素を取り出すには `for color in ${colors[@]};` と書きます。
        
        ```bash
        colors=(red blue pink)
        for color in ${colors[@]}; do
          echo $color
        done
        
        % ./hello
        red
        blue
        pink
        ```
        
- in の後に、コマンドの実行結果を使用する。
    - 例）シェルで date と入力して表示された結果を for に渡して空白ごとに区切られた要素を処理する。
        
        ```bash
        % date
        2022年 9月 1日 木曜日 14時15分37秒 JST
        ```
        
        コマンドの実行結果を受け取るには バッククォートを使って ``date`` としてあげても良いのですが、最近だとコマンドの実行結果を受け取るには $( ) を使うので `$(date)` のように書いてあげてください。
        
        ```bash
        # for item in `date`; do
        for item in $(date); do
          echo $item
        done # dateの要素が改行付きで表示されます。
        
        % ./hello
        2022年
        9月
        1日
        木曜日
        14時22分36秒
        JST
        ```

### 要点
forを使って繰り返し処理を実装する方法について見ていきます。

- for：ループ処理を行う。
- 配列との併用
- コマンドの実行結果との併用</details>


<details><summary>#12 while を使ってみよう</summary>

- while ついて。
    - 例）i=0 にして i < 10 の間、次の処理を行います。
        
        ```bash
        #!/bin/bash
        # whileを使用したループ処理
        
        i=0
        while ((i < 10)); do
          ((i++))
          echo $i
        done
        
        % ./hello
        1
        2
        3
        4
        5
        6
        7
        8
        9
        10
        ```
        
- ループをスキップするための continue 、ループを抜けるための break について。
    - 例）4 の時にループをスキップして、8 の時にループを抜ける処理を書きます。
        
        数値に関する条件なので (( )) 二重丸括弧を使い、
        
        ((i == 4)) の時は continue 、((i == 8)) の時は break、と書きます。
        
        ```bash
        #!/bin/bash
        # whileを使用したループ処理
        # ループをスキップするための continue、ループを抜けるための break
        # i=0
        # while ((i < 10)); do
        #   ((i++))
        #   echo $i
        # done
        
        i=0
        while ((i < 10)); do
          ((i++))
          if ((i == 4)); then
            continue
          fi
          if ((i == 8)); then
            break
          fi
          echo $i
        done
        
        % ./hello
        1
        2
        3
        5
        6
        7
        ```
        
- while で無限ループを回しつつ条件に応じてループを抜ける方法。
    - 無限ループにはいくつかの方法がありますが、今回には `while :` とします。
        
        ユーザーからコマンドを受け付けつつ、もしそれが `$cmd == "quit"` だった時はループを抜けて、そうではない場合はそのコマンドをシンプルに表示するといった処理を書いてあげましょう。
        
        ```bash
        while : # 無限ループ開始
        do
          read -p "Command? " cmd # 文字列「Command? 」を表示させ、コマンドの入力待ちにせよ。
          if [[ $cmd == "quit" ]]; then # もしもコマンドが「quit」という文字列ならば、以下を実行せよ。
            break # ループを抜けろ。
          else # そうでなければ以下を実行せよ。
            echo "$cmd" # コマンド入力した文字列を表示せよ。
          fi # 条件分岐終了。
        done
        
        % ./hello
        Command? yoshiwo
        yoshiwo
        Command? 1234556
        1234556
        Command? 9876
        9876
        Command? quit # quitと入力するとループから抜ける。
        ```

### 要点
ある条件が満たされている間、処理を繰り返し行うことができるwhileについて見ていきます。

- while：ループ処理を行う。`while :` を文頭に書く。
- continue：ループをスキップする。
- break：ループから抜ける
- 無限ループ</details>


<details><summary>#13 ファイルの内容を処理してみよう</summary>

- while はループ処理の他にファイルの内容を読み取って各行に対して何かをする処理もよく書きます。
    - その方法を見る前に、データファイルを用意します。いろいろな方法がありますが、今回はちょっとしたテクニックを使用して colors.txt というファイルをこの場で作成します。
        - cat にリダイレクション( > や < などの記号のこと)を書いて、colors.txt というファイルを作成します。return キーを押すと次の行から入力ができるようになっているので、 red blue pink を入力、最後に control + D で入力を終了させます。
            
            ```bash
            % cat > colors.txt # returnキーを押すと次の行から入力ができるようになります。
            
            % cat > colors.txt
            red
            blue
            pink # 入力を終えたら最後に control + D を押して、入力を終了させる。そして、txtファイルの完成。
                        
            % cat colors.txt
            red
            blue
            pink
            ```
            
    - 作成した txt ファイルの中身を while を使用して出力します。今回は行番号付きで出力します。※行番号付きでの表示：`echo $1 “$line”` と書く。
        
        ```bash
        #!/bin/bash
        # while ファイルの内容を読み取って各行に対して何かを行う、という処理について。
        
        i=1
        while read line; do
          echo $i "$line"
          ((i++)) # 1ずつ増加。
        done < colors.txt
        
        % ./hello
        1 red
        2 blue
        3 pink
        ```
        
    - スクリプト内でファイル名を表示するのではなく、実行時にパイプを使用して繋げる方法。
        
        ```bash
        #!/bin/bash
        # while ファイルの内容を読み取って各行に対して何かを行う、という処理について。
        
        i=1
        while read line; do
          echo $i "$line"
          ((i++))
        # done < colors.txt
        done
        
        % cat hello | ./hello
        1 #!/bin/bash
        2 # while ファイルの内容を読み取って各行に対して何かを行う、という処理について。
        3
        4 i=1
        5 while read line; do
        6 echo $i "$line"
        7 ((i++))
        8 # done < colors.txt
        9 done
        ```

### 要点
ファイルの内容を読み取ってwhileで処理する方法について見ていきます。

- データファイルの作成：cat にリダイレクションにファイル名でデータファイルを作成できる。
- whileによる処理：while を使用してファイルの中身を出力できる。
- パイプを使う方法：今回の場合、`$ cat hello | ./hello` とスクリプト自体にパイプを挟んで繋げた。</details>


<details><summary>#14 case で条件分岐をしてみよう</summary>

- case は変数の値によって処理を振り分けるためのものです。
    - 例）信号機を想定します。case の中で値に応じて処理を書くには red) のように値の後ろに丸括弧で閉じます。
        
        red の処理を終えるには ;; (セミコロン)を2つ書きます。
        
        どこにも当てはまらない場合は * (アスタリスク)を書きます。
        
        case の終わりには、case を逆にした `esac` を書きます。
        
        ```bash
        #!/bin/bash
        # case 変数の値によって処理を振り分けるためのもの。
        
        read -p "Signal color? " color
        case "$color" in
          red) # 値の後ろに丸括弧で閉じること。
            echo "stop"
            ;; # 処理を終えるには ;; アスタリスクを2つ。
          blue)
            echo "go"
            ;;
          yellow)
            echo "caution"
            ;;
          *)
            echo "wrong signal"
        esac # case の終わりには esac を書くこと。
        
        % ./hello
        Signal color? red
        stop
        % ./hello
        Signal color? yellow
        caution
        ```
        
        case の条件は高機能で、例えば `blue|green)` とすると、blue もしくは green 時には “go” の処理を行うという書き方になります。
        
        ```bash
        read -p "Signal color? " color
        case "$color" in
          red)
            echo "stop"
            ;;
          blue|green) # blueでもgreenでも"go"が処理される。
            echo "go"
            ;;
          yellow)
            echo "caution"
            ;;
          *)
            echo "wrong signal"
        esac
        
        % ./hello
        Signal color? green
        go
        ```
        
        他にもワイルドカードや部分一致なども使用できますので、興味がある人は調べてみてください。

### 要点
変数の値に応じて処理を振り分けることができるcaseについて見ていきます。

- case：
    - 値の後ろは丸括弧で閉じること。例）red)
    - 処理を終えるには ;; (セミコロン)2つ。
    - 値がどこにも当てはまらない場合は * (アスタリスク)。
    - case の終わりには esac を書く。</details>


<details><summary>#15 select でメニューを作ってみよう</summary>

- ユーザーに値を選んでもらう時に使用する select について。
    - `select color in` と書いて、選択肢を羅列してきます。
        
        do … done の中でユーザーが選んだ、red blue yellow greenどれかの値を color として使うことができます。
        
        しかし、select の処理はループ処理になるので、どこかで break 処理が必要となります。
        
        ```bash
        #!/bin/bash
        # select ユーザーに値を選んでもらう時に使用する。
        
        select color in red blue yellow green; do
        case "$color" in
          red)
            echo "stop"
            ;;
          blue|green)
            echo "go"
            ;;
          yellow)
            echo "caution"
            ;;
          *)
            echo "wrong signal"
            break
          esac
        done
        
        % ./hello
        1) red
        2) blue
        3) yellow
        4) green
        #? 4
        go
        ```
        
select は処理メニューなどを作成する時によく使用するので慣れるようにしてください。
### 要点
ユーザーに値を選んでもらうことができるselectについて説明していきます。

- select：select の処理はループ処理なので break が必要になる。
- break：ループ処理を終わらせる。</details>


<details><summary>#16 関数を使ってみよう</summary>

- 複数の処理をまとめて登録することができる関数について。
    - 例）レッスンの内容をシンプルにするために hello と表示するためだけの hello 関数を作成します。
        - 作り方、 function hello( ) { } を書いて { } 内に好きな処理を書きます。この時 hello は関数名です。
            
            また、function は省略することができます。
            
            ```bash
            #!/bin/bash
            # 関数 複数の処理をまとめて登録することができる。
            
            function hello() { # helloは関数名、{}の中に好きな処理を書いていく。
              
            }
            
            hello() { # functionを省略することができる。
            
            }
            ```
            
        - 関数を呼び出す時は、関数名を書きましょう。その際、 ( ) 丸括弧は不要です。
            
            ```bash
            #!/bin/bash
            # 関数 複数の処理をまとめて登録することができる。
            
            # function hello() {
            hello() {
              echo "hello ..."
            }
            
            hello
            hello
            
            % ./hello
            hello ...
            hello ...
            ```
            
        - 関数には引数を渡すことができます。渡された引数を特殊関数のように使用できます。したがって、 taguchi,fkoji の値を使いたい場合は $1 と書きましょう。※$1：特殊変数で、引数の番目を表す。
            
            ```bash
            # function hello() {
            hello() {
              # echo "hello ..."
              echo "hello ... $1" # $1は特殊変数で引数の番目を表す。今回の場合はtaguchi,fkojiが引数の値に該当する。
            }
            
            # hello
            # hello
            hello taguchi
            hello fkoji
            
            % ./hello
            hello ... taguchi
            hello ... fkoji
            ```
            
        - return を使って関数が正常終了したかどうかの終了ステータスを返すこともできます。
            
            例）引数が taguchi だったら終了ステータスは 0 、それ以外は 1 を返すようにします。
            
            if 構文を使用します。文字列の比較をするので、 `if [[ $1 == “taguchi” ]];` と書きます。
            
            $1 == “taguchi” の時、終了ステータスは 0 、それ以外は終了ステータスは 1 となるように書きます。
            
            なお、終了ステータスは 0 から 255 の間で指定できて UNIX の世界では 0 だったら正常終了、それ以外は(大抵の場合は 1 なのですが)は異常終了を意味します。
            
            また、return を付けないと最後に実行したコマンドの終了ステータスが、そのままその関数の終了ステータスになることも覚えておきましょう。
            
            終了ステータスを調べたいのですが、直前の実行結果の終了ステータスは $? で調べることができるので以下のように書きましょう。
            
            ```bash
            hello() {
              # echo "hello ..."
              # echo "hello ... $1"
            
              if [[ $1 == "taguchi" ]]; then
                return 0
              else
                return 1
              fi
            }
            
            # hello
            # hello
            # hello taguchi
            # hello fkoji
            hello taguchi; echo $? # 0
            hello fkoji; echo $? # 1
            
            % ./hello
            0
            1
            ```

※UNIX では終了ステータスを使って条件判断したり他の処理に繋げるか判断したりするので、興味がある人は調べてみてください。
### 要点
複数の処理をまとめて登録することができる関数の使い方について見ていきます。

- 関数の作り方：function hello( ) で作成できる。function は省略できるので、hello( ) だけでも作れる。※funciton：関数、という意味もある。
- 引数：関数に引数を渡すことができるし、渡された引数を特殊関数のように使用することもできる。
- 終了ステータス：終了ステータスは 0 から 255 の間で指定できる。UNIX の世界では 0 で正常終了、それ以外(大抵の場合は 1 )は異常終了を意味する。</details>


<details><summary>#17 変数のスコープを理解しよう</summary>

- bash (シェル)ですが、変数はどこからでもアクセスできます。※bash：シェルのこと。
    
    ```bash
    #!/bin/bash
    # 関数
    
    hello() {
      name="taguchi"
      echo "hello ..."
    }
    
    hello
    echo $name # taguchi
    
    yoshiwo@Yoshiwos-MacBook-Pro shellscript_lessons % ./hello
    hello ...
    taguchi
    ```
    
    - そうではなく、宣言した変数はこの関数の中でだけ有効にしたい場合。
        
        その場合は、local というキーワードを付けます。
        
        ```bash
        #!/bin/bash
        # 関数
        
        hello() {
          # name="taguchi"
          local name="taguchi" # localというキーワードを付ける。
          echo "hello ..."
        }
        
        hello
        echo $name # taguchi
        
        yoshiwo@Yoshiwos-MacBook-Pro shellscript_lessons % ./hello
        hello ... # 関数の外では変数が使えなくなっている。
        ```
        
    
※場合によっては local 指定して、変数をこの中でしか使用できないようにすることもあるので、使い方に慣れておきましょう。
### 要点
変数の有効範囲について例を出しながら説明していきます。

- 変数の有効範囲：bash (シェル)において、どこからでもアクセスすることができる。
- local：local を指定する(付ける)ことで、変数をこの中でしか使用できないようにすることができる。</details>
