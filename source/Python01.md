# Python

```演算子
print(3**3) # 3の3乗
print(10 / 3) # int割るintもちゃんと計算(jsも同じ)
print(10 // 3) # 商を求める->3
print(10 % 3) #余り->1
print('Hello'*3) # HelloHelloHello
print(123**300)
```
  
```入力と型変換
m=input('何メートル?')
cm=float(m)*100
print(type(cm))
print('答えは'+str(cm)+'です')
```
  
```if文
print("これから無人島でしばらく一人で生活しなくてはなりません。")
print("好きなものを一つだけ持って行くとしたら何を持って行く？")
print("1: ナイフ")
print("2: 携帯電話")
print("3: 漫画")
i=int(input())

if i<1 or i>3 :
    print('範囲外')
    quit()

print("\n----\n")
print("無人島生活から、将来の恋人について分かります。")

if i==1:
    print("現実的な道具を選んだあなたは..")
    print("現実的な身の丈にあった相手を選ぶでしょう。")
elif i==2:
    print("誰かとつながる道具を選んだあなたは..")
    print("話し好きな賑やかな相手が相応しいでしょう。")
else:
    print("実用よりも娯楽アイテムを選んだあなたは..")
    print("夢見がちなので、理想がとても高いでしょう。")
```
  
```for文
n=int(input('正の整数>'))
# print(sum(range(1,n+1)))
total=0
for i in range(1,n+1):
    total+=i
print(total)
```
  
```random
import random
print(random.randint(1,6))
import time
time.sleep(3)
print('Hello')
```
  
```競争アプリ
import random
import time

# 変数の初期化
a=b=0
goal=20

# ユーザーからの入力を得る
user=input('aとbのどちらのカメが勝つか?')

# 競争開始
print('競争開始!')

# aとbのどちらもゴールしていない間繰り返す
while a < goal and b<goal:
    print('---')
    a+=random.randint(1,6)
    b+=random.randint(1,6)
    print('a:'+'>'*a +'@')
    print('b:'+'>'*b +'@')
    time.sleep(1)

# 判定
winner='同時' if a == b else 'a' if a > b else 'b'
"""
if a == b:
    winner='同時'
elif a > b:
    winner='a'
else:
    winner='b'
"""

# 予想は当たった?
print('当たり' if winner==user else 'はずれ')
"""
if winner == user:
    print('当たり')
else:
    print('はずれ')
"""
```
  
```じゃんけんアプリ
import random
n=3
win=lose=draw=0
for i in range(1,n+1):
    print(f'じゃんけん{i}回目')
    print('あなたの手は?')
    user=int(input('0:グー、1:チョキ、2:パー>'))
    pc=random.randint(0,2)
    print(f'pcの手は{pc}')
    diff=(user-pc + 3)%3
    if diff == 0:
        print('あいこ')
        draw+=1
    elif diff == 2:
        print('勝ち')
        win+=1
    else:
        print('負け')
        lose+=1
print(f'結果({n}戦) win:{win} lose:{lose} draw:{draw}')
```
  
```list
a_list=[20,35,82,50,33]
print(a_list[0]) # ->20
print(a_list[-1]) # 33

# for文
for i in a_list:
    print(i)

# 要素数
print(len(a_list)) # ->5
```
  
```listの操作
points = [62, 58, 72, 60, 47, 81, 74, 65, 59, 38]
print(f'平均点{sum(points)/len(points)}')
print(max(points)) # 81
print(min(points)) # 38

ls=sorted(points) # 昇順に並べたものを返す
ls=sorted(points,reverse=True) # 降順

print(ls)

ls2=points[0:3]
print(ls2) # [62,58,72]
ls3=points[3:5]
print(ls3) # [60,47]
ls4=points[-2:] 
print(ls4) #[59,38]
```
  
```二次元リスト
a=[
    ['田中',30,50,80],
    ['井上',80,20,40],
    ['鈴木',80,30,40],
]
print(a[0]) #['田中',30,50,80]
print(a[2][1]) # 80
a[2][-1]=60
print(a[2]) #['鈴木',80,30,60]

print(len(a)) # 3
```
  
```クイズアプリ
# 三択クイズ
# クイズデータを二次元のリストで表現 --- (*1)
quiz_list = [
    # [問題, 選択肢1, 選択肢2, 選択肢3, 答え]
    ["夏目漱石の本名は？", "石男", "浩介", "金之助", 3],
    ["野口英世が亡くなった場所は？", "福島", "ガーナ", "パリ", 2],
    ["福澤諭吉が広めたものは？", "カレー", "電灯", "天ぷら", 1],
    ["樋口一葉が書いた小説は？", "双葉", "十三夜", "歌世界", 2]
]

import random
# シャッフル
random.shuffle(quiz_list)

# 繰り返し出題する
for quiz in quiz_list:
    print('[問題]')
    print(quiz[0])
    # 選択肢を表示
    for i in range(1,4):
        print(str(i)+':'+quiz[i])
    user=int(input('答えは?'))
    if user==quiz[4]:
        print('正解!')
    else:
        print('ハズレ...答えは',quiz[quiz[4]],'です')
    print('---')
```
  
```dictionary
a_dict={'田中':48,'佐藤':78,'井上':49}
print(a_dict['佐藤']) # 78
a_dict['佐藤']=79

# for
for key in a_dict:
    print(f'{key}は{a_dict[key}才')
```

```dictionaryを使ったアプリ
import math
# レストランのメニュー
menu_dict = {
    "洋風カレー": 900,
    "オムライス": 870,
    "ラザニア": 790,
    "ハンバーグ定食": 920,
    "トマトパスタ": 720
}
"""
for key in menu_dict:
    price=math.ceil(menu_dict[key]*1.3)
    print(f'{key}:{menu_dict[key]}->{price}円')
"""
# items()を使ってタプルに変換
# [('洋風かれー',900),('オムライス',800)....]
# a,b=10,20
for name,price in menu_dict.items():
    new_price=math.ceil(price*1.3)
    print(f'{name}:{price}->{new_price}円')
```
  
```deictionaryを使ったアプリ２
# 今回集計するデータ --- (*1)
s = """
サンマ,カツオ,サンマ,サンマ,マグロ,フグ,マグロ,マグロ,マグロ,サンマ,ニシン,イワシ,サンマ,サンマ,カツオ,サンマ,カツオ,サンマ,カツオ,サンマ,マグロ,マグロ,マグロ,ニシン
"""
# データの前後にある空白を除去 --- (*2)
s = s.strip()
# カンマでデータを区切る --- (*3)
s_list = s.split(",")

# 空のdictを作成
dic=dict()

# forでリストを回しながらdictを更新していく

for fish in s_list:
    if fish in dic:
        dic[fish]+=1
    else:
        dic[fish]=1

# 結果を出力

for name,count in dic.items():
    print(f'{name}={count}')
```
  
```文字列のスライス
import math
# abcd.....zの文字列生成
data=''.join([chr(i) for i in range(97,97+26)])
w=int(input('幅>'))
for i in range(math.ceil(len(data)/w)):
    print(data[i*w:(i+1)*w])
```
