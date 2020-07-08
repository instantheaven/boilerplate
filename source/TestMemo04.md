# テスト前に確認しておきたいメモ④
**[1回目のテスト用の確認まとめ](https://github.com/instantheaven/boilerplate/blob/master/source/TestMemo01.md)**  
**[2回目のテスト用の確認まとめ](https://github.com/instantheaven/boilerplate/blob/master/source/TestMemo01.md)**  
**[3回目のテスト用の確認まとめ](https://github.com/instantheaven/boilerplate/blob/master/source/TestMemo03.md)**  
  
Unityの基礎

---

**CreateEmptyするときは最初に0,0,0でリセットしてから使うこと**  
  
```void Start```は一回だけ走る  
スクリプトが画面に登場したときにだけ  
```transform```は全てのオブジェクトが持っているコンポーネント  
```transform.```って書くとコンポーネントにアタッチできる  
```localposition```なのは```Stage```の子要素になってるから  
直下か何かに子要素かでインセプターの```Transform```の意味が違う  
ダイレクトに置いてあると```Transform```は  
グローバル空間(この世界の座標)に置いてある```position```  
子要素の場合は  
親からのずれを保持している  
  
```Rigidbody```コンポーネントを追加し、```Is Kinematic```(イズキネマティック)にチェックを入れる  
擦り抜けを防げる  
  
**重要なチェックボックス**  
* **Is Trigger**  
* **Is Kinematic**  
* **Has Exit Time**  
  
```Is Trigger```のチェックを入れなければ当たり判定があるけど、入れるとセンサーになる  
```Is Kinematic```のチェックを入れると外からの影響を受けない  
重力をつけても落ちない  
```HasExitTime```も重要なチェックボックス  
出る時間をセット  
終了時間をもって遷移する  
チェックをつけると終了しないと遷移しない  
終了時間は```ExitTime```  
```HasExitTime```がついてるのとついてないので挙動が全然違う  
  
```isTrigger```が空間から出たときは  
```OnTriggerExit```  
  
```isTrigger```が空間に入ってきたときは  
```OnTriggerEnter```  
  
```isTrigger```がずっと空間にいる間中は  
```OnTriggerStay```  
  
```OnCollision```でも一緒  

  
sphereは地球換算で1mだからもっさりするから重力を変える  
  
```mass```は軽い方が吹っ飛ぶ  
  
BallGeneratorはコルーチンを使ってる  
1.5秒ごとにボールが飛び出す  
```Update```でやると1秒で60個出てしまう  
1.5秒ごとにやる```Update```みたいなもの  
間引いても良いけど、最初から設定しておこうよということ  
```transform.positon```はBallGenerator  
```transform.rotation```はその前に設定した向き(インスペクターの```Rotation```)  
ボールだから今回の場合ボールの向きは関係ない  
```transform.forward```は```x軸```(青い矢印)の向きで力を与えてる  
```AddForce```と```velocity```の違い  
動いてるものに対しては違いが出る  
動いてるものに対して初速が出てしまうのが```AddForce```(力を加える)  
この場合上にカクカクって移動してしまう  
```velocity```は強制的に動きを変える？  
  
```isGrounde```が```true```は接地してる時  
  
```isGrounded```って言うプロパティを見ることで接地してるのかが判定できる  
少し凸凹の地面だと接地しててもしてないと判断されたりする  
  
接地してるときに何ができるかと言うと、  
```Vertical```だから上下  
```Vertical```が0.0f以上だから上方向だけ  
上を押すと```moveDirection```を1  
  
  

```OnCollisionEnter```は何かにぶつかった時  
  
  
```public int Count{ get; set;}=0;```  
JavaにはないC#のプロパティという仕組み  
  
プロパティ名は一文字目を大文字にする  
  
```person.Name```で値を入れられる  
Javaならゲッターとセッターを使わなきゃいけない  
  
プロパティは  
```privateフィールド```に対して```publicフィールド```みたいにアクセスできる  
  
初期化子(しょきかし)  
  
```private set```にすると```get```のみできるようにできる  
  
```setter,getter```で特にやる処理がない場合は自動プロパティが便利  
  
```
using System;
namespace ClassLesson
{
    public class Person
    {
        //自動プロパティ
        public string Name { get; set; }
        //初期値も指定できる
        //public string Name { get; set; } = "ごんべ";
        public int Age { get; set; }
        public void ShowInfo()
        {
            Console.WriteLine($"名前:{this.Name},年齢:{this.Age}");
        }

    }
}
```
  
Javaの```publicフィールド```に挙動は近い  
厳密には違う  
  
一文字目が大きくて丸括弧がついてたら関数でついてなかったらプロパティ  
```List```の```Count```とかはプロパティ  
  
C#のメソッドは一文字目が大文字  
  
  

```Interpolate(インターポレイト)```  
補間する  
  
```var```  
右辺見たら型が明らかな場合は、左辺書く必要がなく使える  
Pythonとかみたいに後から他の型を入れられない  
宣言の時だけ使える  
2行に分けたら使えない  
  
Javaの拡張for文  
```for(String s:names){}```  
  
C#は  
```foreach(string s in names){}```  
  
ポイントはJavaとC#でのクラスの書き方、var、拡張for文  

  
  

**サインはy座標、コサインはx座標**を覚えておけばOK  
特徴としては1から−1まで連続して動くこと(サイン)  
  
```Mathf.sin```  
Unityでは```Mathf```  
```Time```クラス  
Unityの時間関係のことを管理しているクラス  
```Input```クラスは入力関係を全部やってるクラス  
```Time.time```ゲームが始まってからの時間、どんどん増えていく  
```Mathf```は何の単位を返すか  
1から−1までの値を返す  
  
```MonoBehavior```(モノビヘイヴィア)のインスタンス化  
```MonoBehavior```を継承したクラスはnewを直接呼び出すことができません  
```Instantiate```(インスタンシエイト)関数によりプレファブからオブジェクトを生成するか、  
何かしらの```GameObject```に対して```AddComponent```関数を用い、コンポーネントとして追加する必要があります  
  
インスタンシエイト  
何をどこにどの向きで  
  
```UpDate```の次に  
```Instantiate```は重要  
  
GameObject型  
```Torque```(トルク)は回転で発生する力  
  
```Input.GetButtonDown```  
クリックしたとき、ボタンを押したとき(押し下げ時)  
```Input.GetButtonDown("Fire1")```  
```Input```に```Fire1```が定義されている  
要注意ポイント  
ダブルクォーテーションで囲まれてる文字列だから間違えててもエラーが出ない  
ダブルクォーテーションの中を書くときはより一層気をつけて書くこと  
  
```Input.GetMouseButtonDown(0)```  
０がクリック、１が右クリック  
  
```GetMouseButtonDown(0)```  
マウスの左クリック(通常)を押し込んだとき  
```GetMouseButtonUp(0)```  
マウスの左クリック(通常)を離したとき  
```InputMousePosition```には二次元で値が入る  
  
  

```GetButtonUp```は離したとき  
  
```x軸```方向に回して、```y軸```方向に回してだと、特定の条件で回転制御不能になる(ジンバルロック)  
  
  
Rigidbody型  
```Rigidbody candyRigidBody = candy.getComponent<Rigidbody>();```  
今、生成した```candy```の```Rigidbody```を取得  
```candyRigidBody.AddForce(transform.forward * shotSpeed)```  
```AddForce```はベクトルを与える  
```transform.forward```　は、z軸が向いている方向(前を向いてくれる)  
この場合の```transform```は```Shooter```を指している  
```transform.forward```もUnity用語ベスト30に入るぐらい大事、よく使う  
  
Unityのオブジェクトには前という概念があって、```z軸```が前になる  
```z軸```の位置を考慮しないといけない  
変な方向向いてたら入れ子にして```z軸```を設定し直す  
  
```AddTorque```は回転力  
  
```transform.Translate``` で移動させてる  
```(Vector3.forward)```  
```Vector3```クラスに書いてある定数だから```Vector3.forward```は001  
```new Vector3(0,0,1f)``` と同じ  
自分自身の軸に従って飛んでいく  
もし第二引数に```speace.World```ってするとワールド空間の```z軸```に向かって進んでいく  
  
```ShipScript.cs(C#)
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ShipScript : MonoBehaviour
{
    public GameObject prefab;
    Vector3 vec; //出荷しただけでnullではなく0,0,0が入ってる(構造体) クラスやフィールドに似てるけど構造体は参照型じゃない
    public float speed;

    // Update is called once per frame
    void Update()
    {
        vec.x = Input.GetAxis("Horizontal"); //左右の移動
        transform.Rotate(Input.GetAxis("Vertical"), 0, 0); //上下を押したときの回転(x回転) 上を押すと前に倒れる
        transform.Translate(vec * speed); //x軸方向に動く
        if(Input.GetButtonDown("Jump")){　//スペースボタンを押したときに
            GameObject bullet = Instantiate(
                prefab, //何を
                transform.position, //どこに
                Quaternion.LookRotation(Quaternion.Euler(-90f, 0, 0) * transform.forward) //どの角度で
                //Quaternionを掛け算で更に回せる オイラー角を使う
                //LookRotationは引数にベクトルを与えることでそのベクトルを向くQuaternion(回転)を作ってくれる
                //transform.forward はこの物体がアタッチされているz軸の向き(この場合Ship)
                //transform.rotation にすると腹から出る(だから90度ずらしてる)
            );
        }
    }
}
```
　
   
```Debug.Log();```と```Debug.Break();```は大事  
検証することばかり  
```Debug.Break()```はそこで一時停止  
  
アクシス【```axis```】 の解説  
機軸。 変化・運動などの軸となる主な方向。  
  
```sampleCandyCount % SphereCandyFrequency ==0```  
%はあまり  
```SphereCandyFrequency ```で ```sampleCandyCount``` を割ったあまりが０かどうか  
  
```Random.Range()```  
は端を含まない(未満)  
intとintのときは含まない、小数点と小数点のときは含む  
  
```candy.transform.parent = candyHolder.transform```  
```candy.transform.parent```は親をどうしますか  
```parent```(ペアレント)は親子関係  
```transform```はつける決まり、なしだとできない  
親子関係を埋めよっていう**テスト**が出たら難しいよな  
```transform```に位置とか維持してるし必要  
親をどうしますか　だから、右辺に親  
  
カメラ  
```SkyBox```(空)じゃなくて```SolidColor(```色)にできたりする  
```Orthographic```(オルトグラフィック)で遠近感をなくす  
  
```Sensitivity```(感度)を下げるとゆっくりに1000だと速い  
  
```Rigidbody```の```Collision Detection```を```Continuous Dynamic```に設定する(一番重く一番監視してるやつ)  
弾丸とかが速いとすり抜けが起きることがある  
処理が重くならないように0.05秒休んでたりする  
  
```OnBecameInvisible()```  
オンビケイムインビジブル  
カメラのレンダリングの範囲から外れたら消してくれる(```Destroy(gameObject)```  
  
  
```Ray```は光線  
Unityでもよく使う  
見えない光線  
```Ray```は基本的にまっすぐ  
```Ray飛ばす```　って言葉をよく使う  
１メートルの```Ray```を飛ばして接触判定したり、いろんな使い方がある  
センサーみたいな  

  
```normalized```は1にする  
```normalized```しないと斜めをクリックしたときに速くなっちゃう、遠いから(距離があるから)  
長さを1にしておこうと言うこと  
  
```velocity```の数字を変えると速さが変わる  
  
```OnGUI```  
```public```で```GUIStyle```を用意して  
第三引数で```Style```を渡すとインスペクターで細かい設定ができるようになる  
どこにどの文字列をが第一引数、第二引数  
  
```if(msg == "GameOver")```  
Javaなら```文字列.Equals(文字列)```じゃないとできなかったけど、  
C#なら上のでできる  
  
```Time.timeScale = 0f;```  
ゲーム内の時間が止まる  
ゲームが完全に止まるわけじゃない  
画面が止まってるけど、クリックすると```Instantiate```ができて作られる  
時間が止まってるから物が動けないだけ  
```Update```は止まらない  
生成もしたくない場合は、```timeScale```が0以上の条件もつけておくとか  
  
プレファブ状態のものにはスクリプトを登録できない  
登場してきた後にファインド(探しに行く)するとか(重い)  
```GameManager```をフィールドで用意しておく  
```OnCollisionEnter```は衝突が発生したら  
コライダー同士の衝突  
今回はコリジョン(```Collision```)  
```OnTriggerEnter```は```コライダー()```  
覚えておくといい(**テスト**に出るかも？な雰囲気。明言はしてないけど)  
  

Nejikoの3メートル後ろからNejikoの向きにカメラを向けよう  
  
```target.forward(Nejikoが向いてる向き) * 3(3倍) + Vector3.up(上方向から)```を```target.positon```から引く  
  
Nejikoの向いてる向きを(回転)を少し遅れて追いかけたい場合は  
```Lerp```じゃなく```Quaternion.Slerp```  
  
１フレーム、最初は0.168が入るけど、```deltaTime```かけてるから１秒間に10m走ることになる  
そのままだと加速して行ってしまうから  
第一引数と第三引数で挟み込んでる(クランプ 工作とかで挟むやつ)  
```moveDirection.z=Mathf.Clamp(acceleratedZ,0,sppedZ);```  
5に到達したら終わり  
10mにはならない  
上方と下方を設定した変数を用意したときは良い(Clamp)  
  
 キャラクターコントローラーを動かしたい場合  
 重力も設定したい場合は  
 ```controller.Move```  
 **テスト**出すなら**Move**  
  
カメラ  
```player.positon```だとUnityちゃんの腰の辺りを見ちゃうから、プラス```Vector3.up```で1m上を見てる  
  

**テスト**問題として  
```isTrigger```を持つ物体が来たとして、そこで処理を走らせたい場合、メソッドはどう書くか  
```OnTriggerEnter```  
これは大事  
  
```if(Physics.Raycast(ray,out hit,100.0f)){```  
out  
  
Javaでは厳密な意味の参照渡しができないけど、  
C#はできる  
それが```out```  
```out```は参照渡し  
  
クラスが参照型  
構造体は値型  
でもほぼほぼ同じ  
  
```RaycastHit```  
  
覚えることは  
C#は厳密な意味の参照渡しができることと  
```RaycastHit hit;```でやれること  
  
```Ray```でクリックしたところに当てて、キャラをそこに動かすとかよくある  
  
```RaycastAll```で貫通  
  
Unityのインスペクターでできることはスクリプトでできる  
```Rigidbody```をつけたりとか  
  
```magnitude```はベクトルの大きさ  
```LookAt```は便利なメソッド  
```LookAt場所```って指定するとそっち方向にむけてくれる  
  
クラスの前にオプションをつける  
Javaでいうアノテーション  
```@WebServlet("/Login")```  
  
C#の場合、直かっこで付与できる  
  

```Button```で大事な属性は```OnClick属性```  
  
シーンの名前でもシーン番号でも指定できる  
  
```enabled```(イネイブルド)  
今回はコンポーネント単位  
GameControllerコンポーネント  
名前の左横のチェックボックスをやるのが```enabled```  
昨日は```setActive```でやった  
  
コルーチンは```deltaタイム```を蓄積させて時間を操る  
  
```Invoke関数```  
第一引数で指定した関数を、第二引数で指定した秒数だけ遅らせて実行する  
まぁまぁ使うことがある  
  
```Quaternion.Euler(0, 90f, 0)```  
は縦方向のプレハブだから、90度回転させてあげる  
  
```Rigidbody```の中の  
```Constraints```(コンストレインツ)  
```Freez```できる  
回転しないとか、その移動はしないとか  
x方向の移動はしないとか  
すごく使う  
物理演算したいけど特定の動きや特定の回転の制限ができる  
  
```RectTransform```  
```Transform```を継承している  
中心の概念がある  
  
```SetActive(true)```  
何をやってるかというと、メインカメラとか何にでも名前の横にチェックボックスがある、それを  
有効にしたり無効にしたりしてる(表示・非表示)  
めちゃくちゃよく使う  
  
NejikoController型はスクリプト  
TextはTextコンポーネント型  
LifePanel型はスクリプト  
  
scoreLabel.text  
はテキストコンポーネントの中のテキストを指してる  
Textがテキストコンポーネント型だから  
今までのコンポーネントの取得と違う  
  
GameObject型のtextとかでGetCompornentで取得して  
.textでセットできるのと同じ  
  
```SlopeLimit``` 45度の傾斜まで登れる  
```StepOffset``` 30cmの段差なら問題ない  
  
使いたい部品があったら、フィールドで宣言して  
```Start```でコンポーネントを取得するのがUnityのセオリー  
```Update```でやっちゃうと1回でいいことが、1分間で3600回呼び出してしまう  
  
```transform.Rotate```で諸々関係なく回転させてる(左)  
  
Timeで一番重要なのは```Time.deltaTime;```  
1フレームに要する時間  
1秒間に60回だとすると、0.016ぐらいと言うのを覚えておく  
  
デルタタイムを考慮した値を加算した場合  
フレームレートにかかった時間に応じて値が伸縮し同じ合計値になる  
  
```LateUpdate```は普通の```Update```より実行がワンテンポ遅い  
何に使われるか、主にカメラの追従  
  
```Lerp```(ラープ)はよく出てくる  
50%の場所までしか行かない  
ちょっと遅れる  
