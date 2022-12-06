開発者がTencent Cloud GME製品のAPIを容易にデバッグして導入するために、このドキュメントではGMEのコマンダーモードの導入手順を紹介します。

## ユースケース

ウォーゲームのシーンで、GMEはキャスターとオーディエンスの2種類のロールを提供します。ルームに参加する前にキャスターを設定した場合、ルームに参加した後マイクをオンにして発言したり、スピーカーをオンにしてルーム内のコミュニケーション音声を聞くことができます。オーディエンスとしてルームに参加した場合、ルームに参加した後マイクをオンにしてもルーム内で発言することができません。

## 前提条件

- GMEアプリケーションの作成が完了し、SDK AppIDとKeyを取得しました。[サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
- **GMEリアルタイムボイスサービス**が既に有効にされました。[サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/10782)をご参照ください。
- **GME SDKの導入**が完了しました。[SDKの快速導入](https://intl.cloud.tencent.com/document/product/607/40858)をご参照ください。

## 統合の手順

ウォーゲーム音声モードを導入する手順は次の通りです：

<dx-steps>
-<dx-tag-link link="#enable" tag="控制台">GMEサービスの利用</dx-tag-link>
-<dx-tag-link link="#config" tag="控制台">ロールの設定</dx-tag-link>
-<dx-tag-link link="#access" tag="业务侧">リアルタイム音声サービスの利用</dx-tag-link>
-<dx-tag-link link="#callback" tag="业务侧">マイクをオンにする</dx-tag-link> 
-<dx-tag-link link="#result" tag="控制台">ロールの切り替え </dx-tag-link>
-<dx-tag-link link="#usage" tag="控制台">ルーム退出</dx-tag-link>
</dx-steps>

 [](id:enable)
### ステップ1：GMEサービスの利用

GME SDKの呼び出しと導入については、[Native SDKのクイック導入](https://intl.cloud.tencent.com/document/product/607/40858)、[Unity SDKのクイック導入](https://intl.cloud.tencent.com/document/product/607/44544)、[Unreal SDKのクイック導入](https://intl.cloud.tencent.com/document/product/607/44545)をご参照ください。

[](id:config)
### ステップ2：ロールの設定

EnterRoomインターフェースを呼び出す前に、ロール設定インターフェースを呼び出して、コマンダーモードでローカル側のロールを設定してください。

####  関数のプロトタイプ
```
public abstract int SetAudioRole(ITMG_AUDIO_MEMBER_ROLE role); 
```

| パラメータ | タイプ                   | 意味                                                         |
| ---- | ---------------------- | ------------------------------------------------------------ |
| role | ITMG_AUDIO_MEMBER_ROLE | <li>ITMG_AUDIO_MEMBER_ROLE_ANCHORはキャスターを意味し、ルーム内のマイクとスピーカーをオンにすることができます </li><li>ITMG_AUDIO_MEMBER_ROLE_AUDIENCEはオーディエンスを意味し、視聴するため、ルーム内のスピーカーのみをオンにすることができます</li> |

#### サンプルコード
```
ITMGContext.GetInstance().SetAudioRole(ITMG_AUDIO_MEMBER_ROLE.ITMG_AUDIO_MEMBER_ROLE_AUDIENCE);
```

[](id:access)
### ステップ3：リアルタイム音声サービスの利用 

EnterRoomインターフェースを呼び出して、リアルタイム音声ルームに入ります。

[](id:callback)
### ステップ4： マイクをオンにする 

- ロールがキャスターの場合は、EnableMicインターフェースとEnableSpeakerインターフェースを正常に呼び出してマイクとスピーカーをオンにできます。
- ロールがオーディエンスの場合、EnableSpeakerインターフェースを使用してスピーカーをオンにできますが、EnableMicインターフェースを呼び出すとAV_ERR_INVALID_ARGUMENT (1004)エラーコードが返され、この時点ではオーディエンスモードであり、マイクのオンは無効であることが表示されます。

[](id:result)
### ステップ5：ロールの切り替え

ルーム内でSetAudioRoleを呼び出してロールを変更することができます。
- ロールが設定されていない場合、新しく設定されたロールに切り替えます。
- ロールが設定された場合は、新しく設定されたロールに切り替えます。
- この時点でロールが設定されていない場合、またはキャスターである場合、通常の通話が行われるようマイクがオンの状態で、オーディエンスに切り替えると、マイクがオンのままです。この場合、業務レベルではEnableMicインターフェースを呼び出してマイクの状態とマイクUIの状態を変更することをお勧めします。

[](id:usage)
### 手順6：ルーム退出 

ExitRoomインターフェースを呼び出してリアルタイム音声ルームを終了すると、ロール状態が無効になり、ロールを再設定してください。
