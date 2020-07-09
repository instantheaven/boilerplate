# サーブレット

### 方法①　hiddenパラメータを使用
フォーム内にhiddenパラメータという部品を入れます。  
送信したいリクエストパラメータの名前と値を、name属性とvalue属性で指定します。  
  
```hiddenパラメータ
<input type="hidden" name=""名前" value="値">
※この部品は画面には表示されない
```
   
### 方法②　リクエスト先の指定に「？ 名前＝値」を付ける
リンクのhref属性、フォームのaction属性で指定するリクエスト先に「?」を付け、  
その後ろにリクエストパラメータを追加します。  
  
```リクエスト先の指定に「?名前=値」を付ける
<a href="リクエスト先?名前＝値">･･･</a>
<form action="?=" method="post">･･･</form>
※複数送る場合は「&」でつなぐ(例:a=10&b=20)
※リンクを使う場合、リンク先のサーブレットクラスはdoGet()を実行する
※フォームを使う場合、method="post"とする
```
  
```・リンクで送る例
<a href="/SampleServlet?hoge="foo"">リンク</a>
```

```・フォームで送る例
<form action="/SampleServlet?hoge=foo" methodo="post">
<input type="submit" value=""送信">
</form>
```
   
---
  
 
```
<form action="/RegisterApp/FormSampleServlet" method="post">
```
上のスラッシュ以降はURL  
URLにつけて?以降に付与できる  
リクエストパラメータに含めて送ることができる  
```http://~~~~~/~~~/~~~~?page=4```とかそういうの  
  
SELECT ほしいもの FROM  
24件とか  
でLIMITとかOFFSET 24件とかで  
取ってきたりしてリンク作ったり  
  
URLに書くのはよく使う  
  

## 練習5-1
**次のJSPファイルとサーブレットクラスがフォームで連携できるように、①～④に適切な語句を入れて完成させてください。**  
  
```■JSPファイル
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
･･･(省略)･･･
<form action="/example/"(1)" method="post">
名前：<br>
<input type="text" name="name"><br>
<input type="submit" value=""登録">
</form>
･･･(省略)･･･
```
  
```■サーブレットクラス
@webservlet("/Ex5_1")
public class Exercisel extends HttpServlet{
    protected void (2) (HttpServletRequest request,HttpServletResponse response)throws ServletException{
    request.setCharacterEncoding("(3)");
    String name=request.getParameter("(4)");
    ･･･(省略)･･･
    }
}

```
---
  
  
getPrameter  
送信パラメータ  

  
# MVCモデル

## MVCモデルとは
**MVCモデル**とは、GUIアプリケーションの為の模範的な構造です。  
ざっくり言うと  
「ユーザーがボタンなどを使って操作するアプリケーションはこんな内部構造で作ればいいことがあるよ、というお手本やガイドラインのようなもの」だと思えばいい。  
  
MVCモデルは、アプリケーションを表に挙げた3つの要素、**モデル(Model)**、**ビュー(View)**、**コントローラ(Controller)**に分けて開発することを定めています。  
**各要素は担当する役割が決められており、ほかの要素の役割は担いません。**  
  
**MVCモデルにおける開発の3つの要素**  
  
|  要素 | 役割  |
|---|---|
| モデル(Model)  |  アプリケーションの主たる処理(計算処理など)やデータの格納などを行う  |
| ビュー(View)  | ユーザーに対して画面の表示を行う  |
|コントローラ(Controller)|ユーザーからの要求を受け取り、処理の実行をモデルに依頼し、その結果の表示をビューに依頼する|
  
これらの要素が次の①～⑦のように連携して、アプリケーションの機能をユーザーに提供します  
　
  
①ユーザーが、アプリケーションの提供する機能(検索など)を要求する  
②コントローラが要求を受け付ける  
③コントローラがモデルに処理の実行を依頼する  
④モデルが処理を実行する  
⑤コントローラが処理結果の表示をビューに依頼する  
⑥ビューがユーザーの要求の結果を表示する  
⑦ユーザーは要求の結果を見る  

**役割を分担しておくことで、処理の修正や拡張を行う際にどの要素に手を加えたらよいかが明確になり、アプリケーションそのものの保守や拡張を行いやすくなる**というメリットがあります。  
  

リクエストは必ずコントローラ(サーブレット)が受け取る  
モデルは一般的なJavaが担当する  
ビューはJSPが担当する  
  
MVCはどの言語でも使われる  
  

# フォワード

**フォワードを使用すると、処理を他のサーブレットクラスやJSPファイルに移すことができます**  
  
フォワードの構文
```フォワードの構文
RequestDispatcher dispatcher=request.getRequestDispatcher("");
dispatcher.forward(request,response);
※「javax.servlet.RequestDispatcher」をインポートする必要がある
```
  
　

### フォワード先の指定方法
・JSPファイルの場合→　/WebContentからのパス  
・サーブレットクラスの場合　/URLパターン  
※フォワード先は同じWebアプリケーションでないとならない  
  
```RequestDispatcher```  
リクエストディスパッチャー  
  
WEB-INFフォルダに入れると  
ブラウザから直接リクエストできない状態になる  
  
ForwardSampleServlet.java  
forwardSample.jsp  
  
RequestDispatcherインスタンス  
newじゃなくどこの処理かのパスをリクエストする  
  
```RequestDispatcher rd=request.getRequestDispatcher("/WEB-INF/jsp/forwardSample.jsp");```  
これは準備しただけ。宛先指定しただけ  
  
```rd.forward(request, response);```  
これで処理をバトンタッチ  
(今回は何もせずにバトンタッチしてる)  
  
コントローラとビューだけ使っている感じ  
  


doGetにout.printlnでHTMLを書いた後に  
フォワードしたらどうなるのか？  
上書きされているのか、doGetの方に書いたものは表示されない  
コンソールではでる  
out.printlnは通ってるけどやってない  
  

リダイレクトの前に  
スコープ  
あとでリダイレクトに戻ってくる  
  

# スコープ

**スコープ4種類**  
**アプリケーションスコープ**が一番寿命が長い  
**リクエストスコープ**は一回だけ  
**セッションスコープ**はカートに入れたとかみたいな  
ページスコープ  
  
**なんでもいれられるということはオブジェクト型で入ってるということ**  

  
requestインスタンスの持っているメソッド  
  
**setAttribute** セットアトリビュート  
で**預けられる**  
**getAttribute** ゲットアトリビュート  
で**取得できる**  
  
unseiというラベル  
HashMapのキーとバリューのキーみたいなもの  
  

## 練習5-1の解答
**①Ex5_1　②doPost　③UTF-8　④name**
  
---

```implements Serializable```

JavaBeansのルール  
ルール①　直列化可能である(java.io.Serializableを実装している)  
ルール②　クラスはpublicでパッケージに所属する  
ルール③　publicで引数のないコンストラクタを持つ  
ルール④　フィールドはカプセル化(隠蔽化)する  
ルール⑤　命令規則に従ったgetter/setterを持つ  
  
厳密にいうとJavaBeansのルールはこれだけではありませんが、  
スコープに保存するJavaBeansとしては、これだけで十分です  
  
仕様を満たしたクラスをJavaBeansってあだ名で呼ぶような感じ  
  
```Serializable```(シリアライズ)  
シリアル化  
直列化  
インスタンスをファイルに書き込めるようにするやつ  
クラスの状態を文字にして保存できるイメージ  
通常のインターフェースは抽象メソッドをオーバーライドしないといけないけど、 
```implements```してもオーバーライドする必要ない  
抽象メソッドがない  
ただお知らせしてるだけ  
  
わけかわらなくてもお約束としてJavaBeansの仕様満たすために  
```implements Serializable```を書けばいい  
  
今回はJavaBeansのファイルは値を保持する  
もうひとつ計算をするクラスを作って、完全に分業してる  
  
packageは全部小文字  
  
doGetのあとはdoPostの前にビュー(JSP)を先に作る  
  
```<form action="bmiapp/HealthCheck" method="post">```
  
# リダイレクト

## リダイレクトの構文
**response.sendRedirect(""リダイレクト先のURL");**  
※リダイレクト先は、ブラウザがリクエストできる先であればどこでも可  
  
## リダイレクト先の記述方法(同じアプリケーションサーバにある場合)
・サーブレットクラスの場合→　/アプリケーション名/URLパターン  
・JSPファイルの場合→　/アプリケーション名/WebContentからのパス  

---
  

### ・リダイレクト先をURLで指定する例
**responce.sendRedirect("http://www.example.com/example/SampleServlet");**  
  
### ・リダイレクト先が同じサーバである例(サーブレットクラスの場合)
**response.sendRedirect("/example/SampleServlet");**  

---
  
```
BufferedReader br=null;
FileInputStream fis=new FileInputStream(path);
InputStreamReader isr=new InputStreamReader(fis,"UTF-8");
br=new BufferedReader(isr);
```
  
