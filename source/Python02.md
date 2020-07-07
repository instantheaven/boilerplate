# Python02

listのソート  
```listのソート
a_list=[33,98,74,74,88,85]
a.list.sort() # 自分自身を並べ替え
print(a_list)

b_list=sorted(a_list,reverse=True)
print(b_list)

f_dict={'Orange':300,'Banana':200,'Apple':500}
sorted_list=sorted(f_dict)
print(sorted_list)
for key in sorted_list:
    print(f'{key}:{f_dict[key]}')

sorted_list2=sorted(f_dict.items()
        ,key=lambda x:x[1]
        )
print(sorted_list2)
for name,price in sorted_list2:
    print(f'{name}:{price}')
```
  
listとdictと並べ替え
```listとdictと並べ替え
# あるクラスのテスト結果
test_list = [
  { "名前": "田中", "国語": 80, "算数": 45, "社会": 90 },
  { "名前": "鈴川", "国語": 62, "算数": 70, "社会": 58 },
  { "名前": "早川", "国語": 77, "算数": 69, "社会": 74 }
]
person=test_list[0]
print(person['名前'])

print(test_list[0]['名前'])

total=0
for p in test_list:
    total+=p['国語']
print(total/len(test_list))

# 合計の項目を作る
for p in test_list:
    p['合計']=p['国語']+p['算数']+p['社会']
    
# 合計でlistを並べ替え
sorted_list3=sorted(test_list,
        key=lambda p:p['合計'],
        reverse=True
        )

# 出力
for p in sorted_list3:
    print(f'{p["名前"]}:{p["合計"]}')
```
  
タプル
```タプル
a=(1,2,3)
print(a[0]) # 1

b=a+(4,)
print(b) # (1,2,3,4)

# a[0]=10 

n1,n2,n3=a # アンパック代入
print(n1) # 1

a1,*ls=a
print(a1) # 1
print(ls) #[2,3]
```
  
関数
```関数
# 関数の定義
def tasu(a:int,b:int)->int:
    return a+b

# 関数を使う
print(tasu(2,3))
print(tasu(10,20))
```
  
水族館app
```水族館app
def calc_fee(age:int,is_mon:bool)->int:
    fee=2000
    if age < 3:
        fee=0
    elif age < 6:
        fee=500
    elif age >=60:
        fee=1500
    if is_mon :
        fee=int(fee*0.8)
    return fee

print(calc_fee(18,False))
print(calc_fee(20,True))
print(calc_fee(2,False))
print(calc_fee(70,True))
```
  
次のオリンピックまで何年？
```次のオリンピックまで何年？
def show_next_olympic(year:int)->None:
    diff=4-year%4
    print(f'{year}年の次のオリンピックは{year+diff}年')
show_next_olympic(2016)
show_next_olympic(2018)
show_next_olympic(2020)
```
  
次のオリンピックまで何日？
```次のオリンピックまで何日？
import datetime

# 特定の日付からオリンピックまでの調べる関数
def calc_days(y,m,d):
    olympic=datetime.datetime(2021,7,23).timestamp()
    target=datetime.datetime(y,m,d).timestamp()

    # 1日当たりの秒
    perday=24*60*60
    days=int((olympic-target)//perday)

    s=f'{y}/{m}/{d}から{days}日後'
    print(s)

calc_days(2018,12,1)

t=datetime.date.today()
calc_days(t.year,t.month,t.day)
```
  
関数を定義する場所
```関数を定義する場所
def main():
    print(tasu(3,5))
    sub1()
    sub2()

def tasu(a,b):
    return a+b

def sub1():
    print('sub1')

def sub2():
    print('sub2')

main()
```
  
ラムダ式
```ラムダ式
tasu=lambda x,y:x+y
print(tasu(2,3))
add=tasu
print(add(3,5))

"""
jsだったら
tasu=(x,y)=>{x+y}
console.log(tasu(2,3))
```
  
### モジュール
モジュールの作成(今回はkeisan.pyを以下のように作成した）
```keisan.py
def tasu(a,b):
    return a+b

def hiku(a,b):
    return a-b

def kakeru(a,b):
    return a*b
```
  
モジュールの呼び出し
```モジュールの呼び出し
import keisan

print(keisan.tasu(3,5))
print(keisan.kakeru(2,3))

import random as r
print(r.randint(1,6))
```
  
モジュールないの特定の関数の呼び出し
```モジュールないの特定の関数の呼び出し
from keisan import tasu

print(tasu(2,3))
```
  
モジュール内のすべての関数を関数名だけで呼び出せるようにする
```モジュール内のすべての関数を関数名だけで呼び出せるようにする
from keisan import *
print(tasu(3,3))
print(hiku(100,11))
print(kakeru(3,4))
```
  
関数に別名をつける
```関数に別名をつける
from keisan import tasu as add
from keisan import kakeru as mul
print(add(3,8))
print(mul(2,4))

from random import randint as rnd
print(rnd(1,6))
```
  
お天気アプリ(Jsonパース)
```お天気アプリ(Jsonパース)
# 天気予報を取得するモジュール
# URLからJSONデータをダウンロードする関数
def get_json(url):
    import urllib.request as req
    import json
    # データをダウンロード
    res=req.urlopen(url)
    json_data=res.read()
    # JSONデータをPythonで使えるように読み込む
    return json.loads(json_data)

# 都市IDを取得することで天気情報を取得する関数
def get_weather(city_id):
    url = "http://weather.livedoor.com/forecast/webservice/json/v1"
    url += "?city=" + str(city_id)
    data=get_json(url)

    s=''
    s+=data['title']+"\n"
    for row in data['forecasts']:
        label=row['dateLabel']
        telop=row['telop']
        s+=label+":"+telop+"\n"
    return s

# モジュールとして利用されるかどうかの判定
if __name__ == '__main__':
    res=get_weather(130010) # 東京の天気を取得
    print(res)
```
  
モジュールとして読み込み実行
```モジュールとして読み込み実行
import l29
print(l29.get_weather(260010))
```
  
変数のスコープの確認
```変数のスコープの確認
value=30

def hoge1():
    print(value)

def hoge2():
    global value
    value=999
    print(value)

hoge1()
hoge2()
print(value)
# print(fuga)
```
  
郵便番号アプリ(Jsonパース)
```郵便番号アプリ(Jsonパース)
def get_json(url):
    import urllib.request as req
    import json
    res=req.urlopen(url)
    json_data=res.read()
    return json.loads(json_data)

def get_addr(zip_code):
    url=f'https://api.aoikujira.com/zip/zip.php?zn={zip_code}&fmt=json'
    data=get_json(url)
    return data['result']

if __name__ =='__main__':
    print(get_addr('110-0006'))
```
  
zip_addrをモジュールとして呼び出し実行する。
```zip_addrをモジュールとして呼び出し実行する。
import zip_addr
print(zip_addr.get_addr('144-0054'))
```
