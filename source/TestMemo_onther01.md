iが０の時に3回  
iが１の特に2回  
iが２の時に1回  
  
3からiを引けばいい  
  
#  
##  
###  
  
if文を使う
半角スペースを入れて表示する
```
for(int i=0;i<4;i++){
  for(int j=0;j<4;j++){
    if(j<3-i){
      System.out.print(" ");
    }else{
       System.out.print("#");
    }
}
System.out.println();
```
  
  
### git
バージョン管理  
サービスを更新しておかしくなったときに前のバージョンに戻せるようにとか  
ファイルを間違えて消してしまったときとかに復元できる  
  
```git status```  
ってやるとどんな状態か教えてくれる  
赤で変更があった  
  
```git diff```  
差を教えてくれる(差分)  
緑で追加された分を教えてくれる  
  
```git add .```  
全部アドしていいよ  
  
```git commit```  
この時に"googleのリンクを追加"と書くとgit graphで見たときに何をしたのかわかりやすい  
  
```git graph```  
作業ログ？が見られる  
  
```git checkout``` (git graphのコミックオブジェクトの名前 1d2c5ddみたいな)  
で、そこに飛べるから前の情報に戻れたりする  
  
```git checkout master```  
で最新の状態に戻ってこれる  
  
ブランチ  
```desktop/hello(master)```←マスターブランチ  
マスターブランチはリリースできる状態(完全な状態)  
開発中は新しいブランチを切ってやる(マスターブランチを動かすのは怖すぎる)  
  
```git branch```  
ってやると、ブランチが見られる  
```git branch dev```  
で新しいブランチが作られる(この場合dev)  
  
```git checkout dev```  
で作ったブランチに移動できる  
  
```git init```  
すると、Gitの管理下に置かれる  
  
*```git graph``` はgit log ?graphを短いコマンドで実行できるようにgit講座の初回に設定してある  
  
gitはコミットする際にコメントは絶対つけなければいけない  
つけてもつけなくてもいいわけじゃない  
  
```git diff HEAD```  
HEADというのは今作業しているブランチの最新のコミットオブジェクトを指すポインターでGitではかなり重要な意味を持つ言葉だ。  
小文字で書いてもいいけど、HEADは大事な言葉なので大文字で書く事が多い  
  
ステージングエリアにあげてもそれだけだと、歴史を刻むのはコミットオブジェクトだから履歴に変更はない  
  
  
$ git graph  
* 961236a  **(HEAD -> master)** 2020-01-22 instantheaven second commit
* eb48fe6  2020-01-22 instantheaven first commit
  
```(HEAD -> master)```はHEADが移動したよってこと  
  
```git reset --hard ハッシュ名```  
完全にその時の状態に戻したい時には良い  
  
後腐れなくあの時の状態に戻れる  
(余計なしがらみなくそのタイミングに戻った状態)  
実際にはあんまりhardを使うことは少ない(一番強烈なやつ)  
  
```git reflog```  
で、今までの歴史を表示してくれる  

--------------------------------

## 実際の開発ではどうやるか
  
マスターブランチは神聖な状態(リリースできる状態)  
動いている状態は取っておいて、ブランチを切って開発する  
マスターブランチは一番完全な状態にしておかなきゃいけないから、マスターブランチで作業はしない  
  
```git branch ブランチ名*```  
でブランチを切る(分身を作る)  
  
```git checkout ブランチ名```  
でブランチを移動  
  
```git branch -d ブランチ名```  
作業に先行しているものがあるときは-D 大文字で削除できる  
歴史から消える  

```git checkout -b ブランチ名*```  
ブランチ切って(作って)すぐ移動できる  
  
```git commit -am"forth追加"```  
addしてコミットできる  
  

```git checkout master```  
で、masterブランチに移動して  
```git merge dev```  
マスターブランチに統合(更新完了)  
開発が上手くいったら反映させる  
```git branch -d dev```  
終わったら削除する  
  
が基本的な流れ  

----------------------------------
  
  
### Java時間計測
Javaで時間を計測するには以下の方法を用いればよい  
```
//開始のタイミング  
long start=System.currentTimeMillis();  
//何かしらの処理  
```
  
```
//終了のタイミング  
long end=System.currentTimeMillis();  
  
long diff=end-start;//かかった時間(ms)  
```
  
----------------------------------
  

```
共通要素は継承を利用すると楽
body{
text-align:center;
color:white;
}

body直下のdiv
body>div{
width:200px;
height:200px;
}　

クラスblueは青、クラスredは赤と決めている
.blue{
background:blue;
}

line-heightしたい時
body直下のdivの最初の1,2個に
body>div:nth-child(-n+2){
  line-height: 200px;
}

body直下のdivの二個目
二個目は丸くしたいから
body>div:nth-child(2){
  border-radius: 50%;　100pxと書いても同じ
}

一番簡単なのはfloatで並べる
親要素200pxに100pxのものを入れて、並び切らないのは下にまわる
#box>div{
 float:left;
 width:50%;
 height:50%;
 line-height: 100px;
}


use flex-box
折り返し
#box{
  display:flex;
  flex-wrap: wrap;
  line-height: 100px;
}

幅指定
#box>div{
  flex-basis:50%;
}
```
  
----------------------------------
  
# インタフェース

**インターフェースとして特別扱いできる２つの条件**  
①すべてのメソッドは抽象メソッドである。  
②基本的にフィールドを１つも持たない。  
  
**インタフェースの宣言**  
```
public interface インタフェース名{
}
```
  
インタフェースに宣言されたメソッドは、自動的にpublicかつabstractになるというルールがあるので、  
  
```
public interface Creature{
    void run();//←public abstractを省略しても大丈夫
}
```
  
**インタフェースにおける定数宣言**  
インタフェースは基本的にフィールドを持ちません。  
しかし、「public static fainalがついたフィールド(定数)」だけは宣言が許されます。  
さらにその場合は「public static final」を省略してもよいことになっています。  
インタフェース内でフィールドを宣言すると自動的に「public static final」、定数を宣言したことになる。  
  
```
public interface Circle{
    double PI=3.141592;//←自動的にpublic static finalが補われる
}

```
  
**インタフェースの実装**  
```
public class クラス名 implements インタフェース名{
}
```
  
```implements``` インプリメンツ  
  
インタフェースを実装  
継承という言い方ではない  
  
実装する(implements)という用語が使われるのは、  
**親インタフェースで未定だった各メソッドの内容を  
オーバーライドして実装し確定させるから**。  
  
**インタフェースの効果**  
①同じインタフェースを**implementsする複数の子クラスたちに、共通のメソッド群を実装するよう強制できる**。  
②あるクラスがインタフェースを実装していれば、**少なくともそのインタフェースが定めたメソッドは持っていることが保証**される。  
  
**クラスにはないインタフェースの特権**  
異なる実装が衝突する問題が発生しないため、複数の親インタフェースによる多重継承が認められている。  
  
**インタフェースによる多重継承**  
  
```
public class  クラス名  implements 親インタフェース名1,親インタフェース名2,{
}

```
  
多重継承が許されている  
  

テスト穴埋めで  
interface のフェースをsにするひとがいるけど気を付けて  
  
オラクルででるような試験問題  
public void sellTabacco の publicをなくすと  
オーバーライドのルールでアクセス修飾子は同じか弱める方法にしか変更しちゃいけない  
強める方向に変更するとコンパイルエラー  
インタフェースは暗黙でpublic  
publicが一番弱い、誰からでもアクセスできるから  
protected  
無印  
一番強いのはprivate  
  
インタフェースはpublic以外はだめ  
  
オーバーライドするときは絶対publicを書かないとだめ  

  
インタフェースの継承  
  
|  継承元 | 継承先  | 使用するキーワード  | 継承元の数  |
|---|---|---|---|
| クラス  | クラス  | extends  | 1つ  |
| インタフェース  |  インタフェース | implements | 1つ以上  |
| インタフェース  | インタフェース  |  extends |  1つ以上 |
  
**extendsとimplementsの両方を使ったクラス定義**  
```
public class  クラス名 extends 親クラス implements 親インタフェース1,親インタフェース2,{
}
```
  
----------------------------------
  
### 文字列処理  
  
|  操作 | メソッド定義  |
|---|---|
|  内容が等しいか調べる | public boolean equals(Object o)  |
| 大文字、小文字(※)を区別せず内容が等しいか調べる  | public boolean equalsIgnoreCase(String s)  |
| 文字列長を調べる  |  public int length() |
| 空文字か(長さが0か)を調べる  | public boolean isEmpty()  |
  
**不変** immutable(イミュータブル)  
**可変** mutable(ミュータブル)  
  
```while((line=br.readLine()) !=null)```  
行がなくなったら抜けるループ  
他に方法はあるけどファイル読み込みのときはこれがいい  
  
----------------------------------
  
```form.html FormsampleServlet.java```  
formで大事なことはaction属性で送信先がいる  
頭のスラッシュは忘れないように  
404エラーが出る  
今回はpost通信  
doPost  
  
@WebServlet("/ここ")は1対1で対応させれば大丈夫  
  
通信方法は2種類あると思っていると良い  
get通信とpost通信  
  
文字化けしないように  
```request.setCharacterEncoding("UTF-8");```  
マルチバイトの文字を扱うなら絶対必要  
  
utf-8は大文字小文字関係なく問題なさそう  
データベースだとutf8だったりとかもする  
  
formLessonというアプリを作って  
FormsampleServlet.java  
form.html  
のファイルを  
サーバーに置いてる  
  
数字を扱いたいときは  
```<input type= "number">```  
numberを使うといい  
```<input type="number" min="0" max="100">```  
これで最小は0、最大100を指定できる  
  

