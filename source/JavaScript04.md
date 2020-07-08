letはブロックスコープ(スコープがJavaと同じ)  
varはスコープがもっと広い(有効範囲が広すぎて使いづらい)  
letの方がいい  
  
Javaには文字列が数値かどうかを判定するメソッドがない
JSはisNaN(値)がある

比較演算子
==   左辺は右辺と等しい(あいまいな比較)　3と3Aが等しくなる言語がある(PHPはそう)  
=== 左辺等辺は厳密に等しい(Javaの==と同じ感じ)  
  
型が違うものでも比較できる  
  
console.log(0=="")  
true  
  
配列は直カッコが世界的に標準  
JSは波カッコじゃない  
要素数の確保とかいらないからlistみたいなもの  
要素数の概念がない  
  
unshiftは先頭に  
  
先入れ先出しのキュー  

  

# [JSP & Servlet-14日目(英和辞書アプリの作成1)](https://joytas.net/programming/jspservlet14)


英単語と意味が**タブ**区切りで並ぶ**TSV**ファイルであることがわかる。  
  
取得できない時のデバッグワード  
実行したSQLを知りたい時  
```System.out.println(ps);```  
WordDAO.java  
51行目～  
```this.connect();```  
```ps=db.prepareStatement("SELECT * FROM words WHERE title LIKE ?");```  
→```ps.setString(1, searchWord);```  
  
コンソールに  
```com.mysql.jdbc.JDBC42PreparedStatement@107404b3: SELECT * FROM words WHERE title LIKE 'book%'```  
って表示される  
  
スクリプトレット  
```<option value="startsWith"<%if(mode.equals("startsWith")) out.print(" selected"); %>>で始まる</option>```  
  
今日やった書き方  
式  
```<option value="startsWith" <%=mode.equals("startsWith")? " selected":"" %>>で始まる</option>```  
  
メソッドは最初は小文字  
