# テスト前に確認しておきたいメモ②

**MySQLとサーバーサイド・データベースの接続**

**[1回目のテスト用の確認まとめ](https://github.com/instantheaven/boilerplate/blob/master/source/TestMemo01.md)**  
**[3回目のテスト用の確認まとめ](https://github.com/instantheaven/boilerplate/blob/master/source/TestMemo03.md)**  
**[4回目のテスト用の確認まとめ](https://github.com/instantheaven/boilerplate/blob/master/source/TestMemo04.md)** 
2/15〜3/11までの分を以下にまとめ

# SQL [(SQL基本)](https://github.com/instantheaven/boilerplate/blob/master/source/sql_memo01.md)

○データベース  
fruitsApp  
を作成せよ。文字コードはutf8とすること。  
  
CREATE DATABASE fruitsApp DEFAULT CHARACTER SET utf8  
  
○fruitsAppにfruitsテーブルを以下の仕様で作成せよ  
id 整数　主キー　自動連番  
name 可変長文字列(30) NOTNULL制約  
price int  
updated 日付  
  
CREATE TABLE fruits(  
id INT PRIMARY KEY AUTO_INCREMENT,  
name VARCHAR(30) NOT NULL,  
price INT,  
updated DATE  
)  
  
○fruitsテーブルに以下の商品を登録せよ  
みかん,100円,2020-02-12  
ばなな,50円,2020-02-12  
りんご,150円,2020-02-13  
ナシ,80円,2020-02-15  
パイン,200円,2020-02-15  
いちご,300円,2020-02-15  
  
INSERT INTO fruits(name,price,updated)  
VALUES('みかん',100,'2020-02-12'),  
('ばなな',50,'2020-02-12'),  
('りんご',150,'2020-02-13'),  
('ナシ',80,'2020-02-15'),  
('パイン',200,'2020-02-15'),  
('いちご',300,'2020-02-15')  
  
○fruitsテーブルから、名前、値段の一覧を取得する。  
SELECT name,price FROM fruits  
  
○fruitsテーブルに以下のデータを追加する  
洋ナシ,220円  
INSERT INTO fruits(name,price) VALUES('洋ナシ',220)  
  
○fruitsテーブルから、IDが「3]のデータを抽出する。  
SELECT * FROM fruits WHERE id=3  
  
○fruitsテーブルから、登録日が2020-02-13以前のデータについて商品名の一覧を抽出する。  
SELECT name,updated FROM fruits WHERE updated<='2020-02-13'  
  
○fruitsテーブルから、価格が100円以上200円以下の商品を、名前、価格、の一覧で抽出する。  
SELECT name,price FROM fruits WHERE price>=100 AND price<=200  
  
○fruitsテーブルから、日付が2020-02-15でない商品を、名前、価格、の一覧で抽出する。  
  
SELECT name,price FROM fruits WHERE updated<>'20200215'  
○すべての商品を10円値上げせよ。  
UPDATE fruits SET price=price+10  
  
○名前にナシが含まれる商品を名前、価格、の一覧で抽出する。  
SELECT name,price FROM fruits WHERE name LIKE '%ナシ%'  
  
○日付データがnullの項目を商品名の一覧で抽出する。  
SELECT name FROM fruits WHERE updated IS NULL  
  
○一番高い商品の名前、価格を出力する。  
SELECT name,price FROM fruits ORDER BY price DESC LIMIT 1  
  
○パインのデータを削除する。  
DELETE FROM fruits WHERE name LIKE '%パイン%'  
  
○すべてのデータを*を使って一覧表示せよ  
SELECT * FROM fruits  
  

**このぐらいのSQL文は書けるようになったほうがいい**  
データベースを作るとかは見て書けたらいいけど、  
それ以外のところはテストで鉛筆使って書くことはある  
から、多分テスト出る  
  

**name 可変長文字列(30) NOTNULL制約**  
名前なしじゃ作れない  
  
**オートインクリメント**  
最初のidを100とかにすると101から連番になる  

---



|  操作 | メソッド定義  |
|---|---|
|  内容が等しいか調べる | public boolean equals(Object o)  |
| 大文字、小文字(※)を区別せず内容が等しいか調べる  | public boolean equalsIgnoreCase(String s)  |
| 文字列長を調べる  |  public int length() |
| 空文字か(長さが0か)を調べる  | public boolean isEmpty()  |
  

# 正規表現の基本文法
正規表現がもしテスト出るとしても教科書の範囲だけで大丈夫。  

### ①通常の文字：その文字でなければならない
```
String s="Java";
s.matches("Java") //true
s.matches("JavaJava") //false
```

### ②ピリオド：任意の1文字であればよい
```
"Java".matches("J.va") //true
```

### ③アスタリスク：直前の文字の0回以上の繰り返し
```
"Jaaaaava".matches("Ja*va") //true
"あいうxx019".matches(".*") //true
".*"はすべての文字列を許すという指示になる

s.matches("Ma.*") //Maで始まる任意の文字列
s.matches(".*ful") //fulで終わる任意の文字列
```

### ④波カッコ：指定回数の繰り返し

|  パターン記述 | 意味  |
|---|---|
| {n}  |   直前の文字のn回の繰り返し |
|  {n,} | 直前の文字のn回以上の繰り返し  |
| {n,m}  | 直前の文字のn回以上m回以下の繰り返し  |
|?   |  直前の文字の0回または1回の繰り返し |
|  + |  直前の文字の1回以上の繰り返し |
 
  


### ⑤角カッコ：いずれかの文字
**"UR[LIN]"**というパターンは**「1文字目がU、2文字目がR、3文字目がLかIかNであること」**を意味する

### ⑥角カッコ内のハイフン：指定範囲のいずれかの文字
```
"url".matches("[a-z]{3}") //true
```

### ⑦ハットとダラー
ハット記号(**^**)は**文字列の先頭**を、ダラー記号(**$**)は**文字列の末尾**を表す

### splitメソッド：文字列の分割
```
s.split("[,:]")
```
カンマかコロンの場所で文字列を分割

### replaceAllメソッド：文字列の置換
```
s.replaceAll("[beh]","X");
```

---
  

**三項演算子**もテストに出そう  
**int x=xStr==null? 0:IntegerparseInt(x);**  
取得を試みてそれがnullですか？という**三項演算子**  
  
まさかの第2回テストの再問題  
**2回目のテストは見直してできるようにしておいた方が良さそう**  
  

## 練習2-1
次の文章の(1)～(12)に適切な語句を入れてください

　Webページを公開するには[( 1 )]というコンピュータにHTMLファイルを配置し、ブラウザを使って要求する。どの[( 1 )]のどのHTMLファイルを要求するかを指定するのに使用されるのが[( 2 )]である。  
　ブラウザが[( 1 )]に要求することを[( 3 )]という。[( 3 )]には、いくつかの方法があり、代表的なものは[( 4 )]と[( 5 )]である。また、[( 1 )]がブラウザの[( 3 )]に応えることを[( 6 )]といい、応答するデータの種類を表す[( 7 )]と処理結果を表す「ステータスコード」を、ヘッダ部を使って送信する。この[( 1 )]とブラウザのやり取りは[( 8 )]というプロトコルで決められている。  
　Webアプリケーションはブラウザで実行できるアプリケーションで、その中核となるのがサーバサイドプログラムを実行する機能(環境)を備えた、[( 9 )]というコンピュータが必要となる。特にJavaによるサーバーサイドプログラムを[( 10 )]と呼び、[( 10 )]を実行できる環境を[( 11 )]という。  
　Javaによるサーバーサイドプログラムには[( 12 )]というものがあるが、これは[( 10 )]に変換され、最終的には同じものとなる。  


**[練習2-1の解答例](https://github.com/instantheaven/boilerplate/blob/master/source/Answer2-1.md)**

---


**request.getParamater()**は絶対テストに出る
中身がなかったときはnullになる



**request.setAttribute("x", x);**
オートボクシング
自動的にIntegerにしてくれる


# セッションスコープ

## 解説　セッションスコープの基本操作
セッションスコープにインスタンスを保存したり、保存したインスタンスを取得するには、
リクエストスコープのときと同様に、**setAttribute()メソッド**と**getAttribute()メソッド**を使用します。

セッションスコープに保存したインスタンスは、**removeAttribute()メソッド**で削除します。

---


### セッションスコープの取得
**HttpSession session=request.getSession();**

---


### セッションスコープに保存する
**session.setAttribute("属性名",インスタンス);**

---


### セッションスコープからインスタンスを取得する
**取得するインスタンスの型 変数名=(取得するインスタンスの型)session.getAttribute("属性名");**

---


### セッションスコープからインスタンスを削除する
**session.removeAttribute("属性名");**



---


**request.setCharacterEncoding("UTF-8");**
も、**テスト**で書かせると
Enco**r**ding になってることが多いから気を付けて
code(コード)だから

Q4を最大値を求めるメソッドとしてメモる

## 乱数[(乱数の求め方)](https://github.com/instantheaven/boilerplate/blob/master/source/random_memo01.md)
１～５だとするなら大きいほうから小さいほうを引いて１を足したものが個数  



**逆順**も**乱数**もまた**テスト**にでる  
乱数は次間違えたら大変なことになる  


## GET通信・POST通信
**ブラウザから入力してする通信はGET通信**  
**リンクを踏んで飛んでいくとかもGET通信**  
  
**計算の結果をリクエストする通信は  
POST通信**  
  
**GET通信**と**POST通信**の**大きな違い**は  
**GET通信**だと送った内容が見える(**URLに表示される**)  
表示されててほしいときはリンクに飛ばせたい時(飛びたい時)とか  
  
**<a href=""></a>**  
これが何通信かわからないと処理できない  
**リンクだからGET通信**  
  
**今できるPOST通信はformからmethod="post"としたときだけ**  
  
**リクエストで飛んでくるものは何を入れてもString**  
  
## ファイルの読み書き
ファイル読み込みの記述は暗記するだけ  
**読み込みしたい時**は**fis**  
**書きたい時**は**fos**  

### fis
**FileInputStream fis=new FileInputStream("./kaikei.txt");**  
どのファイルを読み込むか  
**InputStreamReader isr = new InputStreamReader(fis,"utf-8");**  
上の読み込みだと効率が悪いから、ラッピングする  
文字コードを指定できる  
**br = new BufferedReader(isr);**  
上の読み込みだと効率が悪いから、三段ラッピング  
  
```
BufferedReader br=null;
FileInputStream fis=new FileInputStream(path);
InputStreamReader isr=new InputStreamReader(fis,"UTF-8");
br=new BufferedReader(isr);
```
  
**鉛筆で書ける必要性がある**  
つまり**テスト**に出る  

### fos
**FileOutputStream fos=new FileOutputStream("./kaikei.txt");**  
**OutputStreamWriter osw=new OutputStreamWriter(fos,"utf-8");**  
**PrintWriter pw = new PrintWriter(osw);**  
　
**FileOutputStream fos=new FileOutputStream("./ssss.txt",true);**  
アペンドトゥルーにすると**追記**になる  
そのままだと上書き  
  
**br.readLine()**  
1行ずつ読み込んでいく  
1行あれば読み込んでなければnullを返す  

  

---

  
サーブレットの  
**@WebServlet("ここ")**　を**Index.html**にしたら**Index.html**を呼んでくれる  
  
**request.getParameter()**  
は、**テスト**に99%出てくる  
ほぼ書かされる  
サーバーサイドで値をとってくるのは重要  
  
**getParameter**だと**文字列を返す**  
**getAttribute**だと**Object型**、**だからダウンキャスト**が必要  
  
**Implements**　とか  
**Serializable**　は  
**テスト**で出る  
これが書けないとコーディングが進まない  
  
**public boolean execute(User user){}**  
**public **は、**アクセス修飾子**  
**boolean** は、**戻り値**  
これも**テスト**で出そう  
  
**HttpSession session=request.getSession();  
session.setAttribute("login",user);**  
**テスト**に出るとしか思えない  
補完できないから**HttpSession**が書けないと  
**Attribute**も  
  
**ServletContext application=this.getServletContext();**  
**アプリケーションスコープ**を使うために**ServletContext**のインスタンスを作っている  
acとかじゃなく**application**にしてるのはJSPで暗黙で用意されてる変数名がapplicationだから、  
同じにしている  
**ServletContext** は覚えなきゃいけない  
これも**テスト**に出そう  
  
**スコープは**  
**setAttribute()** で**セット**して  
**getAttribute()** で**ゲット**する  
  
取得を試みて  
あったら返ってくるし、なかったらnullが返ってくる  
大事な性質  
nullなら作る  
  
**if(loginUser==null){  
response.setRedirect("/docoTsubu");  
}**  
は、ログインせずにURLの直接飛んできたときにダメとする仕組み  
URLを直接入力で来た場合、**リダイレクト**で飛ばされる  
  
WEB-INFに入ってると直接リクエストできない  
入ってないと直接アクセスできてしまう  
  
**request.setCharacterEncoding("UTF-8");**  
**Encoding** はｒがない  
テストにでるかも？  
En code と ingで覚えるといいかもと思った  
  
**session.invalidate();**  
※スコープ自体が破棄され、保存していたすべてのインスタンスが消滅する。  
これも**テスト**に出うる  
  
**String[] data=csv.split(",",-1);**  
-1してないときは、hoge,fuga,空文字,barだけ。末尾のカンマは無視  
**-1すると,,だけの空文字でも要素にしてくれる**  
データがそろってない時などに重宝する  

---


### [練習5−1](https://github.com/instantheaven/boilerplate/blob/master/source/5-1.md)　[(練習5−1の解答)](https://github.com/instantheaven/boilerplate/blob/master/source/Answer5-1.md) 

  

---

  
**doPost**とか**doGet**の書き方はいざ**テスト**で書こうとするとよくみんな困る  
エクリプスにやらせちゃってるから  

### doGet
```doGet
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
```

### doPost
```doPost
protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
```

### フォワード
```フォワードの構文
RequestDispatcher dispatcher=request.getRequestDispatcher("");
dispatcher.forward(request,response);
※「javax.servlet.RequestDispatcher」をインポートする必要がある
```
**穴をあけてくださいと言わんばかり**  

```ps = db.prepareStatement("SELECT * FROM lunches");```  
  
プリペアは準備  
これで準備された  
**SELECT文は結果が欲しいから用意する**  
**rs = ps.executeQuery();**  
これで実際に**SQLを実行**  

```
while (rs.next()) {
int id = rs.getInt("id");
String name = rs.getString("name");
String menu = rs.getString("menu");
Lunch l = new Lunch(id, name, menu);
list.add(l);
}
```
  
**rs.next()**  
次の行があるか？ということ  
あればtrueを返して、ポイントを最初のレコードに移動  
  
これでインスタンスを作る情報がそろったから、  
ひとつひとつインスタンスを作っていく  

  

**application.getRealPath()**  
WebContentとかはサーバーにある  
**application.getRealPathでサーバーの本当のパスを教えてくれる**  

```<% @page language="java"```  
  
ここ(<%@)の次の単語が何か)の部分の穴埋め問題が**テスト**で出そう  
  
ここから先は全部**テスト**に出そう  
  
**db.commit();**で反映  
  
4000件書き込んでる途中に問題が起きた場合は、db.commit();せずに例外処理に行って終わり  
その場合メモリに書き込まれてるから中途半端なデータが書き込まれてるとかもない  
4000件OKだった場合にdb.commit();される  
  
context.xmlの中の**<Resourceタグ**を複数用意して名前を変えれば複数のDBにつなげられる  
  
**LIMIT**が**取得件数**  
**OFFSET**が**ないと先頭から**取得してくる  
**OFFSET**が**あったらずらして**取得してくる  
  

**prepareStatement**すると**PreparedStatement**で**返ってくる**  
**プリペアステートメント**すると**プリペアドステートメント**  
  
**ResultSet**  
rs  
**リザルトセット  
結果セット**  
結果を保持してる  
**主にSELECT文の時に使う**  
  
**list**は**add**  
**map**は**put**  

```("SELECT * FROM stock WHERE code LIKE ? LIMIT ? OFFSET ?")```  
  
**LIKE**は**あいまい検索**  
**ps.setString(1, code+"%");**  
は**前方一致**  
  
**SELECTほしいものFROMテーブル名**  
  
**テスト**に直結してる  
  
```"SELECT count(*) AS total FROM stocks"```  
**集計関数** ```count(*)```  
何件の結果があったか  

  

**<%=code %>**  
**式**  
System.out.printを意識する  
  
**jyan.setWin(jyan.getWin()+1);**  
これはイデオム的な書き方  
教科書にも昔乗ってたお手本的な書き方  
これで１セットしていける  
**getWin()までが評価されてるから＋１できる**  

---


### 練習2-1の解答例
(1)Webサーバ　(2)URL　(3)リクエスト  
(4)と(5)(順不同)GETリクエスト、POSTリクエスト　(6)レスポンス  
(7)Content-Typeヘッダ　(8)HTTP　(9)(Web)アプリケーションサーバ  
(10)サーブレット　(11)サーブレットコンテナ　(12)JSP  
