# SQL
**ストラクチャークエリランゲージ**

---

ローカル開発環境を構築
仮想的にDBやサーバーなどを自分のパソコンの中に作る

**HTTP**
ハイパーテキスト・トランスファ・プロトコル

**XAMPP**
クロスプラットフォーム、Apache、MariaDB(前はMySQL)、Peal、PHP

**Docker**
LinuxをOSの上にかぶせて(Linuxをインストール)

Windows10proはいいけどhomeは不具合も多くていまいち

XCODEは黒い画面を使ってやるため(Mac)

他はほとんどls なのにWindowsだけdir
Linuxコマンド使うためにGitBushをインストールした

phpMyAdmin を使う

# MySQL  
**CREATE TABLE members(**　//membersというテーブル
**id INT PRIMARY KEY AUTO_INCREMENT,**　//フィールドみたいなもの　主鍵(プライマリキー)は同じidのデータを作れないようにしてくれる　AUTO~は自動連番機能
**name VARCHAR(30),　**　//名前は30字まで
**depart VARCHAR(20) DEFAULT '無所属',**　//所属は20字まで　指定しなかったら無所属
**age INT,**　//年齢はint
**updated DATE**
**);**


サーバーを立てたら、
まずデータベースを作る
アプリごととか
テーブルは在庫とか客ごととか

カラムはJavaでいうフィールド
VARCHAR(バーチャー)は255字ぐらい
それ以上はTEXT(テキスト)
最初はintと文字列を覚えたらいい

### ●カラムには型を指定する。よく使う型の一覧
**INT**
**FLOAT**
**DOUBLE**
**CHAR** /*固定長文字列*/
**VARCHAR(len)** /*len桁の可変長文字列*/
**TEXT** /*長い文字列*/
**DATETIME** /*日付時刻 2017-08-31 23:10:20*/
**DATE** /*日付 2017-08-31*/
**TIME** /*23:10:20*/
**BLOB** /*バイナリデータ*/


### ●●4つの基本機能CRUD(CREATE,READ,UPDATE,DELETE)
CRUD(クラッド)
4つの基本機能は大事だから理解しよう
この４つを意識してやる

---


SQLでは
CREATE:**INSERT**
READ:**SELECT**
UPDATE=**UPDATE**
DELETE=**DELETE**

データを入れたい時は
**INSERT INTO** テーブル名

Javaと違って大文字小文字区別なし

数値以外はシングルかダブルクォーテーション
**普通はシングル**
日付型も文字列として

テーブルを作ってその中にデータを入れていっている

**WHERE句**
比較
```SELECT * FROM members WHERE age=25;```
Javaだと==だけど、SQLは違う

Command+SHIFT+Tでタブ復活

```SELECT * FROM members WHERE age<>25;```
**Javaの != と同じ**
95%動くけど5%は言語によって挙動が変わるから、
ダイヤモンド演算子を使う
(拡大解釈？拡張解釈？)

```SELECT * FROM members WHERE age>25 AND age <40```
**Javaの&&と同じだけど、ANDを使う**
25歳以上40歳未満

```SELECT * FROM members WHERE age>25 OR updated <='2015-01-15'```
**Javaの || と同じ**
25歳以上または2015/01/15より前

```SELECT * FROM members WHERE depart IN('営業部','人事部');```
**IN を使うと便利**
カンマ区切りで増やせる

```SELECT * FROM members WHERE updated IS NULL;```
結構大事
アップデートがヌルの項目
=とかでは比較できない
間違えやすいところ

```SELECT * FROM members WHERE name LIKE '鈴木%';```
```SELECT * FROM members WHERE name LIKE '%木%';```
```SELECT * FROM members WHERE name LIKE '%田';```
あいまい検索
%にはデータが入る

```SELECT * FROM members WHERE name NOT LIKE '%北%';```
北が含まれない

```SELECT * FROM members ORDER BY age DESC;```
降順
デフォルトは昇順
```SELECT * FROM members ORDER BY age ASC;```
```SELECT * FROM members ORDER BY age;```
は同じ

```SELECT * FROM members WHERE updated IS NOT NULL```
```ORDER BY age ASC;```
WHERE句で絞り込んだ後にupdatedがnullでないデータを年齢昇順

```SELECT * FROM members ORDER BY age DESC,name ASC;```
年齢で並び替えて、同じ年齢の人がいたら名前を辞書順
漢字は並ばないから、ふりがながいる

```SELECT * FROM members ORDER BY age DESC LIMIT 3;```
年齢を降順で並び替えた後に3件
取得数制限

```SELECT * FROM members ORDER BY age DESC LIMIT 3 OFFSET 1;```
3件とってくるけどOFFSET 1なので1つめはのぞく

ID 3の人を消して、ID 3を指定したら挿入できる
指定しないとこの場合9になる

---

  
**関数**
クラスに属しているものをメソッド

## 集計関数
特徴としては集計関数を用いた場合結果が一行

**SELECT depart,avg(age) FROM members 
GROUP BY depart;**

**GROUP BY**
項目ごと(この場合部署ごと)の平均年齢を求める集計関数
項目ごとに表示される
項目でグルーピング

**GROUP BY depart
HAVING avg(age)>=30;**

departでGROUP BYしてその平均年齢を集計し、平均年齢30以上を取得


--

●カラム別名 AS(取得項目名をAS句の内容で表示)
SELECT title AS タイトル,price AS 価格 FROM books;
見出しの部分の表記を変えられる
クォーテーションで囲む必要がない
AS句

●重複削除 DISTINCT(重複をなくした状態で取得する)
SELECT DISTINCT category FROM books;
(重複をなくした状態で取得するので)カテゴリー一覧を取得できる
SELECTだから削除はしていない

●取得カラムに書ける色々
SELECT price,price+100,'固定値' FROM books;
priceカラム、priceカラムに100足した値、固定値
データベースにない情報を追加して表示している

●切り捨て floor()
SELECT floor(120*1.08);
計算結果の小数部を切り捨てる
floorは床という意味、切り捨て計算

●３桁毎,挿入 format(値,小数点以下の桁数)
SELECT format(12345678,0);

●CASE WHEN (switch case的に分岐できる)
SELECT title AS 書名,category AS 分類,
CASE category WHEN '雑誌' THEN '1F'
WHEN '漫画' THEN '1F'
ELSE '2F' 
END AS 階
FROM books;
categoryによって販売階を表示
SQLには何階に売ってるとかの情報はないから、この場で動的にやってしまう

SELECT title AS 書名,category AS 分類,
CASE category 
WHEN '雑誌' THEN '1F'
WHEN '漫画' THEN '1F'
ELSE '2F' 
END AS 階 FROM books;

こうするとswitch caseっぽい


●CASE WHEN (if的に分岐できる)
SELECT title AS 書名,price AS 価格,
CASE WHEN price < 500 THEN 'えんぴつ'
WHEN price < 1000 THEN 'キーホルダー'
WHEN price < 3000 THEN 'ポスター'
END AS プレゼント
FROM books;

WHENは～のときと覚えるといい

関数は扱うSQLの種類で違ったりする
MySQLを今は使ってる

●文字数 char_length()
SELECT title,char_length(title) FROM books;

●現在日の入力 curdate()
INSERT INTO books(title,price,updated)
VALUES('SQL入門',2800,curdate());

●現在日時の入力 now()
SELECT now();

●文字列連結 concat(文字列,文字列,･・・)
SELECT concat(title,':',price,'円') FROM books;
数値が入っている場合自動的に文字列に変換

●最初のnullでない値を返す。 coalesce(引数,引数,･・・)
SELECT title,coalesce(updated,'更新日未記入')
FROM books;
updatedがnullのカラムは'更新日未記入'と表示
コアレス
使いどころが結構ある


●副問い合わせ(最初にカッコ内の処理を行いその結果を利用)
SELECT title,price FROM books 
WHERE price=(SELECT max(price) FROM books);
先にmaxを求めてその値を利用
max(price)は集計関数
副問い合わせはサブクエリ
