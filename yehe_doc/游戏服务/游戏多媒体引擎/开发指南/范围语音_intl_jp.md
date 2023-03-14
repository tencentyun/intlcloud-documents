## 機能の説明
音声ルーム内では、ユーザー－はある距離内にいる他のユーザーとリアルタイムで音声通話を行うことができます。この機能は、ビジネス層でGMEクライアントインターフェースを呼び出して音源の方位を更新します。サーバーに自端の位置を通知することを目的とします。**自端の世界座標+自端が受信した音声の範囲**、**他端の世界座標+他端が受信した音声の範囲**によって判断した後、サーバーでプレイヤーの範囲内の音声ストリームを転送し、デフォルトでは、プレイヤーから最も近い20本の音声ストリームに転送します。

音源方位の更新はサーバーに自端の位置を通知することを目的とします。自端の世界座標+自端が受信した音声の範囲と、他端の世界座標+他端が受信した音声の範囲で判断し、レンジボイス効果を達成します。

## ユースケース

###　 PUBGゲーム
**PUBGゲーム、生存射撃モバイルゲーム**特有の「チームのみ」または「全員」のボイスモードを提供します。ゲームの設定で、プレイヤーが次の項目を選択できます：
- 「チームのみ」モードを使用すると、チーム内のチームメイトが話している声だけが聞こえます。
- 「全員」モードを使用すると、チーム内のチームメイトの声や、ある範囲内で他の対局者が話している声を聞くことができます。

###　没入型バーチャルシーン
例えば**ゲームのコンサート**などのバーチャルシーンでは、レンジボイスを使ってボーカリストがバーチャルルーム内で歌い、聴衆全員が歌声を聞きながら、自分の一定範囲内の他の聴衆とコミュニケーションをとるようになっています。最高で同ルーム内の1万人以上が同時にマイクをオンにすることができます。

## 体験効果

[Demo体験](https://intl.cloud.tencent.com/document/product/607/50220)で体験プログラムをダウンロードすると、3Dサウンドやレンジボイスの効果を体験することができます。


## 基本概念

レンジボイス機能を使用するには、**音声モード**、**音声受信範囲**、**TeamID**という3つの概念があります。

###　ボイスモード

レンジボイスルームに参加した時に、2種類の音声モードを選択することが可能です。

| 音声モード | パラメータの名称               | 機能                                        |
| -------- | ---------------------- | ------------------------------------------------------------ |
| 全員   | RANGE_AUDIO_MODE_WORLD | <li>設定されると、プレイヤーの近くにいる一定範囲の人がプレイヤーの話を聞くことができます。その範囲内にこのモードが設定されているプレイヤーがいれば、お互いに話をすることもできます。</li><li>チームメートはお互いに聞こえます。 |
| チームのみ   | RANGE_AUDIO_MODE_TEAM  | <li>チームメンバーのみが聞こえます                               |

>! チームメイト間の通話は、距離や音声モードに左右されません。

###　音声受信範囲

![](https://main.qcloudimg.com/raw/fccdd2f96b75e350adf9de934590b4f7.png)
音声モードが**すべての人（RANGE_AUDIO_MODE_WORLD）**に設定されている場合、この場合の音声受信範囲はUpdateAudioRecvRangeインターフェースの影響を受けます。

次の2人のプレイヤーAとBが異なるチームで、音声モードが**すべての人（RANGE_AUDIO_MODE_WORLD）**に設定されているとします。

| プレイヤー座標  | 音声受信範囲 | 他プレイヤとの音声到達状況                                   | チームメイトとの音声到達状況         |
| ---------- | ------------ | -------------------------------------------------------- | -------------------------- |
| A（0,0,0） | 10メートル         | プレイヤーAから10メートル内のBプレイヤーの声が聞こえます。    | 同じチームのメンバー同士の通話に影響を与えません。 |
| B（0,8,0） | 5メートル          | プレイヤーBから5メートル以上離れたプレイヤーAの声が聞こえません。    | 同じチームのメンバー同士の通話に影響を与えません |

<dx-alert infotype="explain" title="">
プレイヤー音声到達状況の詳細については[付録](https://intl.cloud.tencent.com/document/product/607/17972)をご参照ください。
</dx-alert>

###　TeamID

範囲ボイスを使用するには、SetRangeAudioTeamIDインターフェースを呼び出してチーム番号TeamIDを設定し、EnterRoomインターフェースを呼び出してボイスルームに入る必要があります。

- ルームに参加するときに指定されたTeamID != 0の場合、範囲ボイスルームモードに切り替えます。メンバーがTeamID=1を使用してボイスルームに入った場合、そのボイスモードがRANGE_AUDIO_MODE_TEAMに設定されると、TeamID=1のメンバーだけが彼の声を聞くことができます、設定された音声モードがRANGE_AUDIO_MODE_WORLDであれば、TeamID=1のメンバー以外の一定範囲のプレイヤーにもその音声を聞くことができます。
<table>
   <tr>
      <th>TeamIDの状況</th>
      <th>音声モード</th>
			<th>範囲</th>
      <th>音声到達状況</th>
   </tr>
   <tr>
      <td  rowspan="2">TeamID != 0、仮にTeamID=1とします</td>
      <td> RANGE_AUDIO_MODE_TEAM</td>
			  <td>10メートル</td>
      <td>TeamID=1のメンバーと通話できます</td>
   </tr>
   <tr>
      <td> RANGE_AUDIO_MODE_WORLD</td>
      <td>10メートル</td>
			 <td>TeamID=1のメンバーと、音声モードがRANGE_AUDIO_MODE_WORLDに設定されている同室10メートル以内のメンバーと通話できます</td>
   </tr>
</table>   
- チームID=0を使用して音声ルームに入室したメンバーは、レンジボイスのホストモードとなり、ルーム内の全員（音声モードがすべての人であるか、チームのみであるかにかかわらず）がそのメンバーの音声を聞くことができます。
<table>
   <tr>
      <th>TeamIDの状況</th>
      <th>TeamID変更のタイミング</th>
			<th>範囲</th>
      <th>音声到達状況</th>
   </tr>
   <tr>
      <td  rowspan="2">TeamID = 0 </td>
      <td>ルームに入る前にTeamID!=0、ルームに入ったらTeamID=0に変更します</td>
			  <td>10メートル</td>
      <td><li>発話音声はルーム内のすべてのメンバー（音声モードがすべての人かチームのみかを問わず）に聞こえます。<li>TeamID=0のメンバーと会話ができます。<li>RANGE_AUDIO_MODE_WORLDに設定されている同ルームの10メートル範囲のメンバーの声が聞こえます。</td>
   </tr>
   <tr>
      <td>ルームに入る前にTeamID=0であり、TeamID=0でルームに入ります</td>
      <td>10メートル</td>
			 <td><li>発話音声はルーム内のすべてのメンバー（音声モードがすべての人かチームのみかを問わず）に聞こえます。<li>TeamID=0のメンバーと会話ができます。<li>ルーム内の他の人の発話音声は聞こえません。</td>
   </tr>
</table>   



###　シナリオ例

- **PUBGゲーム**：例えばPUBGタイプのゲームでは、4人でチームを組む場合、この4人に同じチーム番号TeamIDを設定する必要があります。100人ごとに1つの対局ルーム、1つの対局に25チームがある場合、25チームは同じ音声ルームに入る必要があります。対局中、あるプレイヤーが10メートル範囲内の見知らぬ人とコミュニケーションを取りたい場合、音声距離範囲を10に設定し、音声モードをRANGE_AUDIO_MODE_WORLDに設定し、またマイクとスピーカーをオンにします。チーム以外のメンバーでなく、チームメンバーとコミュニケーションを取りたい場合は、音声モードをRANGE_AUDIO_MODE_TEAMに設定するだけでよい。
- **ゲームコンサート**：ゲーム中にコンサートを開催し、歌手とゲームプレイヤーが対話しない場合、ゲームプレイヤーがTeamID=OpenIDを使用してレンジボイスルームに入ることができます。また音声モードをRANGE_AUDIO_MODE_WORLDに設定し、ゲームのプレイ方法に応じて音声距離の範囲を設定します。これにより、ゲームプレイヤーは近くのプレイヤーとコミュニケーションを取ることができます。歌手がTeamIDを0に設定してルームに入ると、歌手の声はルームの人全体に聞こえるが、歌手には他の人の声は聞こえません。
- **ホストモード**：ゲーム中の仮想テーブルゲームのようなシーンでは、ホストの話し声はルーム内のすべての人に聞こえると同時に、範囲内のプレイヤーの話し声も聞こえるようにしなければなりません。ホストはまずTeamID!=0の形でルームに入り、ルームに入ってからTeamIDを0にすると、その時点でホストの話はルーム内のすべての人に聞こえ、ホストも範囲内のプレイヤーの声を聞くことができます。



##  前提条件

- **リアルタイムボイスサービスが既に有効にされました**：[音声サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
- **GME SDK導入済み**：コアインターフェースとリアルタイム音声インターフェースの導入を含みます。詳細については、[Native SDKクイックスタート](https://intl.cloud.tencent.com/document/product/607/40858)、[Unity SDKクイックスタート](https://intl.cloud.tencent.com/document/product/607/44544)、[Unreal SDKクイックスタート](https://intl.cloud.tencent.com/document/product/607/44545)をご参照ください。
- **万人レンジボイス**：同室でレンジボイスを使用する人数は1000人を超えた場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してGME開発者に連絡してください。

## 使用手順

<img src="https://qcloudimg.tencent-cloud.cn/raw/4f531ae31457f031b0034d8dc39eda3c.png"  width="40%"/></img>

> !
>
>- この手順に従ってインターフェースを呼び出してください。
>- フローチャットの青い部分は音声範囲に必要な手順です。
>- 通常のチーム音声ルームとは異なり、レンジボイス機能を使用しているは、**スムーズな音質でルームに入る必要があります**。
>- 入室が成功した後、UpdateAudioRecvRangeを1回以上呼び出し、フレームごとにUpdateSelfPositionを呼び出します。


[](id:step0)
### 1. TeamIDの設定

- ルームに入る前に、このインターフェースでチーム番号を設定すると、次回の入室に有効です。
- 入室後、このインターフェースを使用してチーム番号を変更できます。設定後すぐに有効になります。
- 退室後、TeamIDが自動的に0にリセットされないため、当該ボイスモードを呼び出すことを決めたら、毎回はEnterRoomの前にこのメソッドを呼び出しTeamIDを設定してください。
- 退室してからもう一度入室した場合、退室成功のコールバックを実行した後、チーム番号設定インターフェースを呼び出してください。

####  関数のプロトタイプ

```
ITMGContext SetRangeAudioTeamID(int teamID)
```

|パラメータ     | タイプ         |意味|
| ------------- |:-------------:|-------------|
| teamID		|　int 		 | チームナンバーであり、レンジボイスモードの利用中に使われています。TeamIDが0の場合は、通話モードは一般チームボイスで、デフォルトは０です。|

###　2.　音声モードの設定

- 入室前に、このインターフェースを呼び出して音声モードを変更します。次回の入室に有効です。
- 入室後、このインターフェースを呼び出して音声モードを変更すると、現在のユーザーの音声モードが直接変更されます。
- 退室後、このパラメータは自動的にMODE_WORLDにリセットされないため、このメソッドを呼び出すことを決めたら、毎回はEnterRoomの前にこの方法を呼び出し、audioModeを設定してください。

####  関数のプロトタイプ

```
ITMGRoom int SetRangeAudioMode(RANGE_AUDIO_MODE rangeAudioMode)
```

| パラメータ  | タイプ | 意味                                                         |
| -------------- | :--: | ----------------------------------------------------- |
| rangeAudioMode    |int   |　0(MODE_WORLD)が「全員」を表し、1(MODE_TEAM)が「チームのみ」を表す|

### 3. 音声ルームに参加します

EnterRoomを呼び出す前に、SetRangeAudioTeamIDとSetRangeAudioModeの2つのAPIを呼び出す必要があります。

####  関数のプロトタイプ

```
ITMGContext.GetInstance(this).EnterRoom(roomId,ITMG_ROOM_TYPE_FLUENCY, authBuffer); 
```

音声ルームに入るにはスムーズな音質を使用しなければなりません。その後、入室のコールバックを監視して処理します。

```
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM == type)
        {
           	//イベントから返されたデータの分析
            int nErrCode = data.getIntExtra("result" , -1);
            String strErrMsg = data.getStringExtra("error_info");

            if (nErrCode == AVError.AV_OK)
            {
                ///入室シグナリングを受信し、入室が成功し、機器を操作できます
                ScrollView_ShowLog("EnterRoom success");
                Log.i(TAG,"EnterRoom success!");
            }
            else
            {
                //入室に失敗し、返されたエラーメッセージを分析する必要があります
                ScrollView_ShowLog("EnterRoom fail :" + strErrMsg);
                Log.i(TAG,"EnterRoom fail!");
            }  
        }
	}
```

入室が成功すると、UpdateAudioRecvRangeを少なくとも1回呼び出し、フレームごとにUpdateSelfPositionを呼び出します。

### 4. ボイス受信距離範囲の設定

- このメソッドで設定された音声受信範囲（距離はゲームエンジンによって異なる）は、正常に入室した後に呼び出すことが可能です**。
- この方法はUpdateSelfPositionと連携し音源位置を更新することに使われています
- このメソッドは一度呼び出すだけで有効になり、変更が可能です。

####  関数のプロトタイプ 

```
ITMGRoom int UpdateAudioRecvRange(int range)
```

| パラメータ     | タイプ  | 意味                                           |
| ----- | ---- | ------------------------------------------ |
| range | int  | 音声を受信できる最大範囲（エンジン距離単位） |

####  サンプルコード  

```
ITMGContext.GetInstance().GetRoom().UpdateAudioRecvRange(300);
```

### 5. 音源方位の更新

音源方位の更新はサーバーに自端の位置を通知することを目的とします。**自端の世界座標+自端が受信した音声の範囲**と、**他端の世界座標+他端が受信した音声の範囲**で判断し、レンジボイス効果を達成します。

- この関数は音源方位の更新に使用されます。**入室が成功した後に呼び出すことができます**。また**フレームごとにを呼び出す**必要があります。Unityエンジンの場合、このインターフェースはUpdateで呼び出される必要があります。
- レンジボイスを使用して音源方位を更新する必要があります。範囲判断能力が不要な場合でも、**ルームに入ってから一度このインターフェースを呼び出す必要があります**。
- 3Dサウンド効果を同時に使用する場合、このインターフェースのパラメータaxisForward、axisRightおよびaxisUpは下文の[3Dボイスセクション](https://intl.cloud.tencent.com/document/product/607/17972)に従って設定する必要があります。

####  関数のプロトタイプ

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])
```

| パラメータ        | タイプ    | 意味                                       |
| ----------- | ------- | ------------------------------------------ |
| position    | int[]   | 世界座標での自己座標であり、順序は前、右、上です |
| axisForward   |float[]  |本製品では考慮する必要はありません|
| axisRight    |float[]  |本製品では考慮する必要はありません|
| axisUp    |float[]  |本製品では考慮する必要はありません|

##　レンジボイスと3D効果音

上文で紹介したレンジボイス機能は、距離によって音声の到達性を制御するもので、より没入感のある体験が必要な場合は、3D効果音と併用することをお勧めします。

## 使用手順

レンジボイスを使用すると同時に、3D効果音機能を使用する場合は、ルームに入ってから次のレンジボイスステップ1、2、3を完了した後、3Dエンジンを初期化し、3D効果音をオンにします。

<img src="https://qcloudimg.tencent-cloud.cn/raw/39fb54637b7957509d00ed440f7ae0a9.png"  width="40%"/></img>

>?　フローチャートの緑の部分は、3D音声に必要な手順です。

### 前提条件

[レンジボイス利用手順]（#STEP0）を参照してステップ1、2、3を完了します。

### 4.　3D効果音エンジンの初期化

この関数は、3Dサウンドエフェクトエンジンを初期化するために使用され、入室した後に呼び出します。このインターフェイスは、3Dサウンドエフェクトを使用する前に呼び出す必要があります、3Dサウンドエフェクトを送信せず受信するのみのユーザーでも、このインターフェイスを呼び出す必要があります。

####  関数のプロトタイプ 

```
public abstract int InitSpatializer(string modelPath)
```

| パラメータ      | タイプ   | 意味                      |
| --------- | ------ | ------------------------------------------------------------ |
| modelPath | string |　空を入力すればよい |

### 5.　3D効果音のオン/オフ

この関数は、3Dサウンドエフェクトをオン/オフにするために使用されます。オンにした後、3Dサウンドエフェクトが聞こえます。

####  関数のプロトタイプ

```
public abstract int EnableSpatializer(bool enable, bool applyToTeam)

```

| パラメータ        | タイプ | 意味                                              |
| ----------- | ---- | -------------------------------------------------- |
| enable      | bool | オンにすると3D効果音が聞こえる                          |
| applyToTeam  |bool    |3D音声はチーム内で機能するかどうかを示します、enbleがtrueである場合にのみ有効です|

IsEnableSpatializerインターフェースを使用して3Dサウンドの状態を取得します。

### 6. ボイス受信距離範囲（3D）の設定

- このメソッドで設定された音声受信範囲（距離はゲームエンジンによって異なる）は、正常に入室した後に呼び出すことが可能です**。
- この方法はUpdateSelfPositionと連携し音源位置を更新することに使われています
- このメソッドは一度呼び出すだけで有効になります。
-　3D効果音は、音源の音量の減衰は音源距離と一定の関係があります。単位距離がrangeを超えると、音量はほぼゼロになります。
- 距離と音声の減衰の関係については、ドキュメント付録をご参照ください。

####  関数のプロトタイプ 

```
ITMGRoom int UpdateAudioRecvRange(int range)

```

| パラメータ     | タイプ  | 意味                                           |
| ----- | ---- | ------------------------------------------ |
| range | int  | 音声を受信できる最大範囲（エンジン距離単位） |

####  サンプルコード  

```
ITMGContext.GetInstance().GetRoom().UpdateAudioRecvRange(300);

```

### 7. 音源方位（3D）の更新

音源方位の更新はサーバーに自端の位置を通知することを目的とします。**自端の世界座標+自端が受信した音声の範囲**と、**他端の世界座標+他端が受信した音声の範囲**で判断し、レンジボイス効果を達成します。


- この関数は音源方位の更新に使用されます。**入室が成功した後に呼び出すことができます**。また**フレームごとにを呼び出す**必要があります。Unityエンジンの場合、このインターフェースはUpdateで呼び出される必要があります。
- **この機能を使用するには、サンプルコードを直接コピーして呼び出してください**。

####  関数のプロトタイプ

```
public abstract int UpdateSelfPosition(int position[3], float axisForward[3], float axisRight[3], float axisUp[3])

```

| パラメータ        | タイプ    | 意味                                       |
| ----------- | ------- | ------------------------------------------ |
| position    | int[]   | 世界座標での自己座標であり、順序は前、右、上です |
| axisForward | float[] | ローカル座標系前軸の単位ベクトル|
| axisRight   | float[] | ローカル座標系右軸の単位ベクトル|
| axisUp      | float[] | ローカル座標系上軸の単位ベクトル|

####  サンプルコード

**Unreal**

```
FVector cameraLocation = UGameplayStatics::GetPlayerCameraManager(GetWorld(), 0)->GetCameraLocation();
FRotator cameraRotation = UGameplayStatics::GetPlayerCameraManager(GetWorld(), 0)->GetCameraRotation();
int position[] = { 
    (int)cameraLocation.X,
    (int)cameraLocation.Y,
    (int)cameraLocation.Z };
FMatrix matrix = ((FRotationMatrix)cameraRotation);
float forward[] = { 
    matrix.GetColumn(0).X,
    matrix.GetColumn(1).X,
    matrix.GetColumn(2).X };
float right[] = { 
    matrix.GetColumn(0).Y,
    matrix.GetColumn(1).Y,
    matrix.GetColumn(2).Y };
float up[] = { 
    matrix.GetColumn(0).Z,
    matrix.GetColumn(1).Z,
    matrix.GetColumn(2).Z};
ITMGContextGetInstance()->GetRoom()->UpdateSelfPosition(position, forward, right, up); 

```

**Unity**

```
Transform selftrans = currentPlayer.gameObject.transform;
Matrix4x4 matrix = Matrix4x4.TRS(Vector3.zero, selftrans.rotation, Vector3.one);
int[] position = new int[3] { 
    selftrans.position.z,
    selftrans.position.x,
    selftrans.position.y};
float[] axisForward = new float[3] { 
    matrix.m22,
    matrix.m02,
    matrix.m12 };
float[] axisRight = new float[3] { 
    matrix.m20,
    matrix.m00,
    matrix.m10 };
float[] axisUp = new float[3] { 
    matrix.m21,
    matrix.m01,
    matrix.m11 };
ITMGContext.GetInstance().GetRoom().UpdateSelfPosition(position, axisForward, axisRight, axisUp);

```


###　ホストに3D効果音を使用することを禁止する

もしシナリオの中でプレイヤーがレンジボイスのホストモードを使用する場合、つまり彼の声はルーム内のすべてのプレイヤーが聞くようにする場合、[3D音声ブラックリストインターフェース](https://intl.cloud.tencent.com/document/product/607/18218)を参照し、すべての聴取側でホストを聴取側の3D音声ブラックリストに追加する必要があります。これで、3D音声機能減衰効果がホストの音声到達性の影響を回避します。

各ロールのAPI呼び出しのタイミングは次のとおりです：

<table>
<tr>
<td rowspan="1" colSpan="1" >ホストAPIタイミング</td>
<td rowspan="1" colSpan="1" >視聴者APIタイミング</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" ><img src="https://qcloudimg.tencent-cloud.cn/raw/beeb060d2ed5ee1c6b2ac6a9085c3561.jpeg"  width="100%"/></img></td>
<td rowspan="1" colSpan="1" ><img src="https://qcloudimg.tencent-cloud.cn/raw/431d6a477c227002245730c20215405e.jpeg"  width="89%"/></img></td>
</tr>
</table>



## 付録

###　各音声モード

各音声モードでのプレイヤーの音声到達状況：

- 仮にAプレイヤーの状態を「全員」とすると、対応するBプレイヤーの異なる音声モードでの到達可能状況は下記の通りです：
<table>
<thead>
<tr>
<th >同じチームかどうか</th>
<th>範囲内かどうか</th>
<th>音声モード</th>
<th>AとBがお互いの声を聞いているかどうか</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="4">同じチーム</td>
<td rowspan="2">はい</td>
<td>MODE_WORLD</td>
<td>はい</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>はい</td>
</tr>
<tr>
<td rowspan="2">いいえ</td>
<td>MODE_WORLD</td>
<td>はい</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>はい</td>
</tr>
<tr>
<td rowspan="4">違うチーム</td>
<td rowspan="2">はい</td>
<td>MODE_WORLD</td>
<td>はい</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>いいえ</td>
</tr>
<tr>
<td rowspan="2">いいえ</td>
<td>MODE_WORLD</td>
<td>いいえ</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>いいえ</td>
</tr>
</tbody></table>
- 仮にAプレイヤーの状態を「チームのみ」とすると、対応するBプレイヤーの異なる音声モードでの到達可能状況は下記の通りです：
<table>
<thead>
<tr>
<th >同じチームかどうか</th>
<th>範囲内かどうか</th>
<th>音声状態</th>
<th>AとBがお互いの声を聞いているかどうか</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="4">同じチーム</td>
<td rowspan="2">はい</td>
<td>MODE_WORLD</td>
<td>はい</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>はい</td>
</tr>
<tr>
<td rowspan="2">いいえ</td>
<td>MODE_WORLD</td>
<td>はい</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>はい</td>
</tr>
<tr>
<td rowspan="4">違うチーム</td>
<td rowspan="2">はい</td>
<td>MODE_WORLD</td>
<td>いいえ</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>いいえ</td>
</tr>
<tr>
<td rowspan="2">いいえ</td>
<td>MODE_WORLD</td>
<td>いいえ</td>
</tr>
<tr>
<td>MODE_TEAM</td>
<td>いいえ</td>
</tr>
</tbody></table>



### 距離と音の減衰の関係

3Dサウンドエフェクトでは、音源のボリュームは音源の距離と減衰関係にあります。単位距離がrangeを超えた後、ボリュームはほぼゼロまで減衰します。

| 距離範囲（エンジン単位） | 減衰公式                     |
| -------------------- | ---------------------------- |
| 0 < N < range/10     | 減衰係数：1.0（ボリュームは減衰しない）です |
| N ≥ range/10         | 減衰係数：range/10/N         |

![](https://main.qcloudimg.com/raw/4a71a93f7c91ecd70f50968875f95087.png)
