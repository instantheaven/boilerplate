# ２値の入れ替え
### 実例

```2値の入れ替えの基本形
int a=3;
int b=5;
int temp=0;

temp=a;
a=b;
b=temp;

```

 
```小さい順に並び替える
int a=10;
int b=5;
int temp=0;

if(a>b){
    temp=a;
    a=b;
    b=temp;
}
```
 
```大きい順に並び替える
int a=10;
int b=5;
int temp=0;

if(a<b){
    temp=a;
    a=b;
    b=temp;
}
```
 
```
int[] nums={1,2,3,4};
int temp=0;
```
  
---
  
# リバースのアルゴリズム
[2020/01/14のメモより](https://96neko.notepm.jp/draft/7353b0688b)**　Q4**

# リバースのアルゴリズム
## reversの考え方の基本



**アルゴリズムを使う
リバースのアルゴリズム**

---

3 6 7 2 5
**先頭と最後を入れ替えて、二番目と三番目を入れ替える**
5 2 7 6 3

40回の時は20回入れ替える
1000回の時は？
**2で割った商で出せる(i<nums.length/2)**

**ループ回数がわかったら入れ替えたらいい
そういうアルゴリズム**

nums[nums.length-1-i]
何でiを入れると最後の要素を取り出せるのか
i=0;

最後の要素はnums.length-1

**基本的には2値の入れ替えのロジック**
　

### 実例
```リバースのアルゴリズム
import java.util.*;
public class Q4{
	public static void main(String[] args){
		int[] nums={3,8,10,5,4};
		for(int i=0;i<nums.length/2;i++){
			int temp=nums[i];
			nums[i]=nums[nums.length-1-i];
			nums[nums.length-1-i]=temp;
		}
	}
}
```
  
---
  
# 2重for文(考え方)
ひとつめが基準点
ふたつめが比較
  
---
  
# char型
```
char c=str.charAt(0);
String str="Hello"
char c1=str.charAt(0);//H
char c2=str.charAt(1);//e
```
  
**char型の状態で取り出す**  

  

String型はchar型が連続したもの  
  
"a"+"b"+"c"+"d"+"e" ←char型のイメージ  
"abcde" ←String型のイメージ  

##  逆さ文字
**文字列連結を利用する方法**  
空文字  
String型とchar型を文字列連結させている  
文字列と結合すると新しい文字列を作る  
  

**toCharArray**  
変数.toCharArray(); は文字列をchar型に変換  
  
String.valueOf(cArray)  
String.valueOfは最終的に文字列にする  
(Integer.parsIntの反対)  
  
---
  
# 二進数
### 使える数字が０か１しかない

```
十進数　　　　　二進数
1                 1
2                10
3                11
4               100
5               101
```
  
２の０乗は１  
２の１乗は１  
２の２乗は４  
２の３乗は８  
  
---
  
# 配列①

** [配列の扱い方](https://96neko.notepm.jp/page/3adf050af5)**

---


## 配列(array)
同一種類の複数データを並び順で格納するデータ構造  
int[]; []がついてると配列  
## 配列変数
配列につけられた名前  
int[] nums; numsの部分  
## 要素(element)
通常の変数のように型を持ち、1つのデータを格納できる  
nums[0]=5; 5の部分  
## 添え字(index)
配列内の各要素には、0番、1番、2番という番号がついている。  
この番号を添え字といい、0から始まる決まり  
nums[0]; 0の部分  
  
Java
```java
//配列を使うには配列の宣言をする
//書き方

//配列の宣言
//型名[] 配列変数名;
int[] nums;

//配列の要素数を指定する場合
//型名 配列変数名[]=new 型名[要素数];
int[] new nums=[10];

//配列の要素への値の代入

//書き方
//配列変数名[インデックス]
nums[0]

//配列の要素へ値を代入するには
//配列変数名[インデックス]=値;
nums[0]=10;

//宣言と同時に値を代入して初期化
//型名 配列変数名[]={値1,値2,...};
int[] nums={10,20,30,40};


public class Main{
	publicstatic void main(String[] args) throws Expetion{
		
		//変数の宣言と初期化
		int score[]={50,70,40,80,55};

		//値を出力
		for(int i=0;i<5;i++){
			System.out.println(score[i]):
			//このiはインデックス(添え字)の数字を指してる
			//だからscore[i]は1回目のfor文だと、
			//score[0]と同じで
			//インデックス0に入ってる要素の50を出力する
		}
	}
}

//要素数=配列変数名.length
//score.length の部分
int score[]={50,70,40,80,55};
System.out.println(score.length);
//実行結果は5

//要素数分の繰り返し処理
//score.lengthで要素数分繰り返す
//iはi++で1ずつ増えていくので、
//score[i]のi部分はインデックスと同じ数字で回る
for(int i=0;i<score.length;i++){
	System.out.println(score[i]);
}

```
  
  
---
  
# 配列扱い方
```java
public class ArrayLesson01{
	public static void main(String[] args){
		int[] nums;//配列の宣言
		int[] nums=new int[3];//配列の要素数を３つにする
		int[] nums={10.20.30};//配列の要素に10,20,30の値を入れる
		for(int i=0;i<nums.length;i++){
			nums[i]=i;//iの値を配列に格納する(0,1,2)
			nums[i]=i+1;//iの値に+1したものを配列に格納する(1,2,3)
		}
		int a=nums[0];//配列の一番最初
		int a=nums[nums.length-1];//配列の一番最後(インデックスは要素数より1少ないため)
		System.out.println(nums[]);//数字が入ってないのでエラー
		System.out.println(nums[nums.length]);//この要素数はないためエラー
		System.out.println(nums.length);//要素数を表示

		int data=0;
		nums[data];//dataはインデックスの数字
		nums[]=data;//dataは要素に入るからこのままだとエラー
		nums[0]=data;//インデックスを指定すればOK
	}
}
```
  
---
  
