# 2Dアクションゲーム

**ゲーム作成の方針**
今回はキャラクター自身を移動させるのではなく、背景オブジェクトを移動させ、相対的にキャラクターが進んでいるように見せることにします  
  
**2Dと3Dの違い**  
skybox、シーンギズモ、Directional Lightがない  
Orthographic  
並行投影(奥行きがない)  
  
**画像とスプライトの違い**  
スプライトには中心の概念がある  
自分の画像を使う場合は、変換する必要がある  
  
**スプライトアトラス**  
一枚の大きな画像を切り分けて並べて使う感じ  
メモリの節約  
今はそこまで必要じゃなくなってるかも  
  
**背景を動かす**  
こういった時に大事なのは実行しながらSceneを見ること  
positionの値を見たり  
検証したり好奇心も大事  
```Translate``` x軸が1秒間に3移動する  
-8より小さい時は```ScrollEnd()```を呼ぶ  
```transform.positon=new Vector3(8f,0,0);```これでやると何故か動きは同じなのに縦線が出る  
処理は早そうなのに  
```SendMessage```  
アタッチされている他のスクリプトにイベントが発生したとコールしてくれる  
他のスクリプトのメソッドを呼べる  
第二引数に設定されている```SendMessageOptions.DontRequireReceiver'''は、受け手がいなくてもエラーを出さないというもの  
  
**アニメーション**  
前の時はpositionを移動させたけど、  
今回は複数のスプライトを切り替えている  
羽ばたくものと静止状態のものを作る  
アニメーションクリップだけでは動かないし、アニメーターだけでも動かない  
アニメーションコンポーネントに登録してやっと動く  
Boolで判定するんだからHasExitTimeは外した方がいい  
HasExitTimeは時間で遷移するやつ  
  
**キャラクターのコントロール**  
コライダーを大きくすると難しく、小さくすると簡単に  
当たり判定が厳しいか、甘いか  
```GravityScale```とかはゲームの操作感や難易度や世界観に影響するところだから、実際は吟味するところ  
5にすると下に引っ張られて飛ぶのが大変  
重力の値で面白さが変わる  
```Awake()```  
Awake関数はStart関数よりも前に動く  
自分が持っているコンポーネントの取得とかなら問題ない(デメリットもない)  
ただ他のコンポーネントの取得はまだ登場していないからできない  
  
**キャラクターのアニメーション制御**  
z軸は奥  
z軸の値を動かすとキャラクターの向きが変わる  
キャラクターの角度によってアニメーションの状態を変えたい  
上にいる時は羽ばたいて、下にいる時は羽ばたかない  
今回x座標に動いていないけど、前に進んでいると考えて```relativeVelocityX```  
背景と同じ3にする  
計算するために必要  
```ApplyAngle()```  
この関数の中身は難しい  
```Atan2```はアークタンジェント  
サインコサインタンジェントに共通してるのは角度を指定すると値が出る  
アークがつくと逆になる  
逆三角関数  
値から角度を出す  
いきなり```transform.localRotation```に入れるとカクカクってなっちゃうから、```Lerp```で徐々に変えてる  
このゲームぐらいだと変わらない  
**覚えておくことは、アークは逆ということと、角度返すんだなということ**  
子要素はlocalRotation  
  
**死亡判定**  
```IsDead()```はgetter  
プロパティを作るのもあり  
```OnCollisionEnter2D```  
衝突判定  
  
キャラクターの角度を穏やかにしたい場合どうすればいいか  
角度を決定してるのは見かけの速度3(横の長さ)  
これを大きくすればいい  
```relativeVelocityX```を10とかにしてあげたらいい  
  
**Blockの作成**  
作成の際、全体図を頭に入れた方がいい  
```minHeight```はPivotの高さ(低い方)  
```maxHeight```はPivotの高さ(高い方)  
floatの場合、Randomは端含む  
もしここまででスクリプトが完成ならば、  
```pivot.transform.localPosition```  
```GameObject pivot``` GameObject型じゃなくTransform型でやれば  
```pivot.localPosition```で行けるしスッキリしてる  
ヒエラルキーの根元に置いてあるのはルート要素  
親要素は```position```(グローバル座標に対して)  
一度でも子要素になったものは```localPosition```(ローカル座標に対して)  
隙間をランダムにするにはどうしたらいいか(お題)  
上下両方動かすことはないな  
下を動かそう  
どのぐらい動かせばいいか？を実際に見ながらプランニングする  
```isRandom```でインスペクターのチェックボックスがオンなら隙間がランダムに、オフなら今まで通り  
  
---
　　
```Find関数```の利用と注意点  
  
| Find関数 | 機能 |
|  ---  |  ---  |
| Find(string name) | 名前でゲームオブジェクトを検索 |
| FindWithTag(string tag) | タグでゲームオブジェクトを検索 |
| FindGameObjectsWithTag(string tag) | タグでゲームオブジェクトを検索し、一致する全ての要素を配列で返す |
| FindObjectOfType<Type type>() | オブジェクトの型でコンポーネントを検索 |
| FindObjectsOfType<Type type>() | オブジェクトの型でコンポーネントを検索し、一致する全ての要素を配列で返す |
  
複数だと配列を返す  
  
便利な```Find関数```ですが、気軽に使うべきではありません。検索の処理は非常に重く、シーン中のオブジェクトが多くなると著しくパフォーマンスを低下させます。```Update関数```内で```Find関数```を使うと致命的です。  
  
```
  public void SetSteerActive(bool active){
		//Rigidbodyのオン、オフを切り替える
		rb2d.isKinematic = !active;
}
```
   
```isKinematic```がオンだと動けなくて、オフにしたら動ける  
そういう切り替え  
2DだとRigidbody2DのBodyTypeの中にプルダウンである  
 
**enum**  
列挙定数  
クラス作るときに```class ◯◯```って書くみたいな  
```enum ◯◯```  
定数を列挙するだけのクラスみたいな雰囲気  
 
** Java**  
  
 ```public static int PLAY=1,STOP=2;```  
 ```if(num==PLAY)```  
  
 ```void hoge(int mode){``` PLAYなのかSTOPなのか1か2かを判定したいメソッド  
```  switch(mode){``` でもint型の引数ならなんでもいいように思われる、100で入れるとか  
```  case PLAY:```  
```  }```  
 ```}```  
 これだと引数が制限できない  
   
 ```enum Mode{```  
 ```  PLAY,```  
 ``` STOP```  
``` }```  
  
``` void hoge(Mode mode){```  
 ```  switch(mode){```  
 ```  case PLAY:```  
 ```  }```  
 ```}```  
  
Mode型だとPLAYとSTOPの2つしかないから、引数を制限できる  
それ以外を突っ込むとコンパイルエラー  
  
状態を表したいから今回はState(State部分はクラス名みたいなものだから、その時々で名前をつける)  
  
使い方は```enum名.Ready```  
  
**Ready**  
キャラクターもブロックも動かないようにしてる  
背景だけ動いてる(雲と地面)  
  
**switch**  
stateで分岐  
最初はStartでやってるからReady  
  
**GameStart**  
キャラクターとブロックも動けるようにする  
  
** GameOver**  
```GameObject.FindObjectsOfType<ScrollObject>();```  
他のものが持ってるものでも探せば使えるからすごいけど、処理はめちゃくちゃ重くなる  
12個ScrollObjectを持ってるのがゲーム上にいる  
  
  
** Find**  
ObjectかObjectsか  
単数か複数かで戻り値が一つか配列か変わる  
こういうのはよくある  
  
```foreach(ScrollObject so in scrollObjects){```  
scrollObjectsはScrollObject型とわかりきってるから  
```foreach(var so in scrollObjects){```  
var の使い所  
  
Reload  
教科書のは古い書き方  
今のシーンの名前を取得して(説明変数)、それを読み込む  

```
        // 他のシーンを呼び出す
        Application.LoadLevel("Main"); // 非推奨
        SceneManager.LoadScene("Main"); // OK

        // 遷移前のシーンを残して、他のシーンを呼び出す
        Application.LoadLevelAdditive("Main"); // 非推奨
        SceneManager.LoadScene("Main", LoadSceneMode.Additive); // OK

        // 現在読み込んでいるシーンを再読込
        Application.LoadLevel(Application.loadedLevel); // 非推奨
        SceneManager.LoadScene(SceneManager.GetActiveScene().name); // OK
```
  

３、４、５種類ぐらいしかない時はenumの出番  
２種類ならboolでやりたい  

  
ClearTriggerはFindとSendMessageの練習  
GameController型の変数を用意したらいい  
それドットIncreaseScore()メソッドを呼べばいい  
  
SetActiveはチェックボックスのオンオフ  
  
```Mathf.Clamp```はよく使う  
  
アタッチしただけじゃなく中身を見にいく姿勢は大事  


x軸のスケールをマイナスにすると反対に向かせられる  
  
---
  
