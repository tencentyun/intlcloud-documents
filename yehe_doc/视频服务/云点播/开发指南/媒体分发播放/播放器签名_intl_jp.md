プレーヤー署名は、App再生サービスが端末の再生権限を承認するために使用されます。下図の手順6に示すとおり、 App再生サービスが端末での再生を承認すると、有効な署名が配布されます。端末では、署名の有効時間内にビデオコンテンツを再生することができます。
<img src="https://main.qcloudimg.com/raw/e5ae52f1b5f15f289b6f54aa28917da4.png" width="700" />

以下で、プレーヤー署名のパラメータと生成規則について説明します。

## 署名パラメータ[](id:p0)

| パラメータ名         | 入力必須 | タイプ    | 説明                                                         |
| ---------------- | ---- | ------- | ------------------------------------------------------------ |
| appId            | はい   | Integer | VODアプリケーションのappId。                                             |
| fileId           | はい   | String  | VODファイルID。                                                |
| contentInfo      | はい   | Object  | VODファイルIDで再生する具体的なコンテンツ。[ContentInfoタイプ](#p1)です。下記の3種類のうち1種類を再生できます。<li> [アダプティブビットレートストリーミングへのトランスコード](https://intl.cloud.tencent.com/document/product/266/33942)で出力されたオーディオビデオ。暗号化は行っても行わなくても構いません。</li><li>[トランスコード](https://intl.cloud.tencent.com/document/product/266/33938)で出力されたオーディオビデオ。</li><li>[アップロード](https://intl.cloud.tencent.com/document/product/266/9760)されたオリジナルオーディオビデオ。</li> |
| currentTimeStamp |はい   | Integer | 配布された署名の現在のUnixタイムスタンプ。                                   |
| expireTimeStamp  | いいえ   | Integer | 配布された署名の有効期限のUnixタイムスタンプ。空のままは有効期限内であることを表します。                   |
| urlAccessInfo    | いいえ   | Object | 再生リンクアクセス設定パラメータ。[Keyリンク不正アクセス防止](https://intl.cloud.tencent.com/document/product/266/33986)設定、再生ドメイン名およびプロトコルパラメータが含まれます。[UrlAccessInfoタイプ](#p4)です。 |
| drmLicenseInfo   | いいえ   | Object | DRM Licenseの設定パラメータ。[DrmLicenseInfo タイプ](#p5)です。       |

#### ContentInfoタイプ[](id:p1)

| パラメータ名              | 入力必須 | タイプ            | 説明                                                         |
| --------------------- | ---- | --------------- | ------------------------------------------------------------ |
| audioVideoType        | はい   | String          | 再生するオーディオビデオのタイプ。オプション値：<li>RawAdaptive：暗号化されていない[アダプティブビットレートストリーミングへのトランスコード](https://intl.cloud.tencent.com/document/product/266/33942)による出力。</li><li>ProtectedAdaptive：プライベート暗号化またはDRMで保護された[アダプティブビットレートストリーミングへのトランスコード](https://intl.cloud.tencent.com/document/product/266/33942)による出力。<li>Transcode：[トランスコード](https://intl.cloud.tencent.com/document/product/266/33938)後の出力。</li><li>Original：[アップロード](https://intl.cloud.tencent.com/document/product/266/9760)されたオリジナルオーディオビデオ。</li> |
| rawAdaptiveDefinition | いいえ   | Integer         | 出力が許可される、暗号化されていない[ABS生成テンプレート](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF)のID。audioVideoTypeがRawAdaptiveの場合のみ、このパラメータが入力必須かつ有効になります。 |
| drmAdaptiveInfo       | いいえ   | Object          | 出力が許可される、暗号化によって保護された[ABS生成テンプレート](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF)のID。audioVideoTypeがProtectedAdaptiveの場合のみ、このパラメータが入力必須かつ有効になります。[DRMAdaptiveInfoタイプ](#p2)です。 |
| transcodeDefinition   | いいえ   | Integer         | 出力が許可される[トランスコードテンプレート](https://intl.cloud.tencent.com/document/product/266/33938#.3Ca-id.3D.22zm.22.3E.3C.2Fa.3E.E8.BD.AC.E7.A0.81.E6.A8.A1.E6.9D.BF)のID。audioVideoTypeがTranscodeの場合のみ、このパラメータが入力必須かつ有効になります。 |
| imageSpriteDefinition | いいえ   | Integer         | プログレスバープレビュー用の[スプライトイメージテンプレート](https://intl.cloud.tencent.com/document/product/266/33940)のID。 |
| resolutionNames       | いいえ   | Array of Object | プレーヤーが解像度のそれぞれ異なるサブストリームに表示する名前であり、[ResolutionNameInfoタイプ](#p3)の配列です。入力しない場合またはnull配列を入力した場合はデフォルトの設定を使用します。</br>MinEdgeLength：240，Name：240P。</br>MinEdgeLength：480，Name：480P。</br>MinEdgeLength：720，Name：720P。</br>MinEdgeLength：1080，Name：1080P。</br>MinEdgeLength：1440，Name：2K。</br>MinEdgeLength：2160，Name：4K。</br>MinEdgeLength：4320，Name：8K。 |


#### DRMAdaptiveInfoタイプ[](id:p2)

| パラメータ名                    | 入力必須 | タイプ    | 説明                                                         |
| --------------------------- | ---- | ------- | ------------------------------------------------------------ |
| privateEncryptionDefinition | いいえ   | Integer | [保護タイプDrmType](https://www.tencentcloud.com/document/product/266/34187#AdaptiveDynamicStreamingTemplate)がSimpleAESである[ABS生成テンプレート](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF)のID。 |
| widevineDefinition          | いいえ   | Integer | [保護タイプDrmType](https://www.tencentcloud.com/document/product/266/34187#AdaptiveDynamicStreamingTemplate)がWidevineである[ABS生成テンプレート](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF)のID。 |
| fairPlayDefinition          | いいえ   | Integer | [保護タイプDrmType](https://www.tencentcloud.com/document/product/266/34187#AdaptiveDynamicStreamingTemplate)がFairPlayである[ABS生成テンプレート](https://intl.cloud.tencent.com/document/product/266/33942#.3Ca-id.3D.22zsy.22.3E.3C.2Fa.3E.E8.BD.AC.E8.87.AA.E9.80.82.E5.BA.94.E7.A0.81.E6.B5.81.E6.A8.A1.E6.9D.BF)のID。 |

#### ResolutionNameInfoタイプ[](id:p3)

| パラメータ名      | 入力必須 | タイプ    | 説明                       |
| ------------- | ---- | ------- | -------------------------- |
| MinEdgeLength | はい   | Integer | ビデオ短辺の長さ。単位：ピクセル。 |
| Name          | はい   | String  | 表示名。                 |

#### UrlAccessInfoタイプ[](id:p4)

| パラメータ名 | 入力必須 | タイプ    | 説明                                                         |
| -------- | ---- | ------- | ------------------------------------------------------------ |
| t        | いいえ   | String  | <ul style="margin:0;"><li>16進文字列で、リンクの有効期限を表します。</li><li>具体的な意味と値については [リンク不正アクセス防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F) のtパラメータをご参照ください。</li><li>入力しない場合は有効期間内であることを表します。</li></ul> |
| exper    | いいえ   | Integer | <ul style="margin:0;"> <li>プレビュー時間。単位は秒で、10進法で表示します。</li><li>プレビュー時間を指定する場合、時間は30秒以上とする必要があります。</li><li>具体的な意味と値については、 [リンク不正アクセス防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F) のexperパラメータをご参照ください。</li></ul> |
| rlimit   | いいえ   | Integer | <ul style="margin:0;"><li>異なるIPの端末で許可される最大再生数。10進法で表示します。</li><li>具体的な意味と値については、 [リンク不正アクセス防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F) のrlimitパラメータをご参照ください。</li></ul> |
| us       | いいえ   | String  | <ul style="margin:0;"><li>リンクを一意に識別できるリンクID。</li><li>具体的な意味と値については、 [リンク不正アクセス防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F) のusパラメータをご参照ください。</li></ul> |
| domain   | いいえ   | String  | 再生時に使用するドメイン名。入力しない場合またはDefaultを入力した場合は、[デフォルト配信設定](https://intl.cloud.tencent.com/document/product/266/35768)のドメイン名を使用することを表します。 |
| scheme   | いいえ   | String  | 再生時に使用するScheme。入力しない場合またはDefaultを入力した場合は、[デフォルト配信設定](https://intl.cloud.tencent.com/document/product/266/35768)のSchemeを使用することを表します。その他のオプション値：<ul style="margin:0;"><li>HTTP。</li><li>HTTPS。</li></ul> |

#### DrmLicenseInfoタイプ[](id:p5)

| パラメータ名          | 入力必須 | タイプ            | 説明                                                         |
| ----------------- | ---- | --------------- | ------------------------------------------------------------ |
| persistent        | いいえ   | String          | 端末に商用DRM再生ライセンスの永続的な保存を許可するかどうか。値の範囲：<ul style="margin:0;"><li>ON: 永続的な保存を許可します。</li><li>OFF: 永続的な保存を許可しません。</li></ul>デフォルトの値はOFFになっています。 |
| rentalDuration    | いいえ   | Integer         | persistentがONの場合に、商用DRM再生ライセンスによって許可される永続的な保存時間。単位は秒で、入力しない場合は時間制限がないことを表します。 |
| forceL1TrackTypes | いいえ   | Array of String | Widevineを使用する際に、端末に必ずL1セキュリティレベルを使用して処理するよう要求するTrackタイプ。このうち、未指定のTrackタイプはデフォルトでL3セキュリティレベルを使用して処理します。値の範囲は次のとおりです。<ul style="margin:0;"><li>AUDIO: オーディオサブストリーム。</li><li>SD: 短辺が720未満のサブストリーム。</li><li>HD: 短辺が720以上かつ2160未満のサブストリーム。</li><li>UHD1: 短辺が2160以上かつ4320未満のサブストリーム。</li><li>UHD2: 短辺が4320以上のサブストリーム。</li></ul> |

>?
>- [サブアプリケーション](https://intl.cloud.tencent.com/document/product/266/33987) を使用する場合、appIdパラメータとしてサブアプリケーションAppIdを設定する必要があります。
>- 署名パラメータの`t`、`exper`、`rlimit`、`us`の説明と値は、 [リンク不正アクセス防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F) の同名パラメータと完全に一致します。

## 署名計算

VODプレーヤーの署名には、Header、PayLoad、Key によって計算され組み合わせられたデジタルトークンである [JWT](https://tools.ietf.org/html/rfc7519)（JSON Web Token）を採用します。

### Header

HeaderはJSON形式であり、JWTで使用されるアルゴリズム情報を表し、その内容は次のとおり固定的 に使用されます：

```
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### PayLoad

Payload はJSON形式であり、次に例示するようにプレーヤーの署名パラメータのコンテンツです。

```
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "contentInfo": {
    "audioVideoType": "RawAdaptive",
    "rawAdaptiveDefinition": 10,
    "imageSpriteDefinition": 10
  },
  "currentTimeStamp": 1663064276,
  "expireTimeStamp": 1663294210,
  "urlAccessInfo": {
    "t": "6323e6b0",
    "rlimit": 3,
    "us": "72d4cd1101"
  }
}
```

### Key[](id:p6)

Keyは署名の計算時に使用するキーです。ここでは[デフォルト配信設定](https://intl.cloud.tencent.com/document/product/266/35768)の`再生キー`を使用します。

### 計算式

1.  Signatureの計算：
   `Signature = HMACSHA256(base64UrlEncode(Header) + "." + base64UrlEncode(Payload), Key)`
2.  Tokenの計算：
   `Token = base64UrlEncode(Header) + '.' + base64UrlEncode(Payload) + '.' + base64UrlEncode(Signature)`
   最終的に得られたTokenが、VODプレーヤー署名となります。

>?HMACSHA256については  [RFC - HMACSHA256](https://tools.ietf.org/html/rfc4868#page-3) をご参照ください。base64UrlEncodeについては [RFC - base64UrlEncode](https://tools.ietf.org/html/rfc4648#page-7) をご参照ください。

署名の計算および署名の検証を容易にするため、VODコンソールでは署名発行ツールおよび検証ツールを提供しています。

* [プレーヤー署名ツール](https://console.cloud.tencent.com/vod/distribute-play/signature) 。

### 計算例

例えばあるユーザーの、appIdが`1255566655`、fileIdが`4564972818519602447`のビデオについてプレーヤー署名を生成する場合で、かつ以下のようであったとします。

* 再生キーが`TxtyhLlgo7J3iOADIron`。
* プレーヤー署名の配布時間が2022-09-13 18:17:56、対応するUnix時間が`1663064276`。
* プレーヤー署名の有効期限が2022-09-16 10:10:10、対応するUnix時間が`1663294210`。
* リンク不正アクセス防止の有効期限が2022-09-16 11:00:00、対応するUnix時間が`6323e6b0`。
* URLでの再生を最大3つの異なるIPで許可。
* 生成されたランダムな文字列が`72d4cd1101`。

この場合の署名手順は、次のとおりです.

1. Headerのコンテンツ：

```
{
  "alg": "HS256",
  "typ": "JWT"
}
```

base64UrlEncode で処理した後の結果：
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`。

2. Payloadのコンテンツ：

```
{
  "appId": 1255566655,
  "fileId": "4564972818519602447",
  "contentInfo": {
    "audioVideoType": "RawAdaptive",
    "rawAdaptiveDefinition": 10,
    "imageSpriteDefinition": 10
  },
  "currentTimeStamp": 1663064276,
  "expireTimeStamp": 1663294210,
  "urlAccessInfo": {
    "t": "6323e6b0",
    "rlimit": 3,
    "us": "72d4cd1101"
  }
}
```

base64UrlEncode で処理した後の結果：
`eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImNvbnRlbnRJbmZvMSI6eyJhdWRpb1ZpZGVvVHlwZSI6IlJhd0FkYXB0aXZlIiwicmF3QWRhcHRpdmVEZWZpbml0aW9uIjoxMCwiaW1hZ2VTcHJpdGVEZWZpbml0aW9uIjoxMH0sImN1cnJlbnRUaW1lU3RhbXAiOjE2NjMwNjQyNzYsImV4cGlyZVRpbWVTdGFtcCI6MTY2MzI5NDIxMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNjMyM2U2YjAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSJ9fQ`。

3.  再生キーをKey（`TxtyhLlgo7J3iOADIron`）としてHMAC計算を実行した場合、Signature は次のようになります。
    `QFcBX9830ysTzJIyZxoOlRmNb2Gqy2fns9yOfriaDI8`。
4.  最終的に Token はこのようになります。
    `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTI1NTU2NjY1NSwiZmlsZUlkIjoiNDU2NDk3MjgxODUxOTYwMjQ0NyIsImNvbnRlbnRJbmZvMSI6eyJhdWRpb1ZpZGVvVHlwZSI6IlJhd0FkYXB0aXZlIiwicmF3QWRhcHRpdmVEZWZpbml0aW9uIjoxMCwiaW1hZ2VTcHJpdGVEZWZpbml0aW9uIjoxMH0sImN1cnJlbnRUaW1lU3RhbXAiOjE2NjMwNjQyNzYsImV4cGlyZVRpbWVTdGFtcCI6MTY2MzI5NDIxMCwidXJsQWNjZXNzSW5mbyI6eyJ0IjoiNjMyM2U2YjAiLCJybGltaXQiOjMsInVzIjoiNzJkNGNkMTEwMSJ9fQ.QFcBX9830ysTzJIyZxoOlRmNb2Gqy2fns9yOfriaDI8`。

## サンプルコード

VODはPython、Java、Go、C#、PHPおよびNode.jsなどの言語用に複数のプレーヤーのサンプルコードを提供しています。詳細については[プレーヤー署名 - 署名の例](https://intl.cloud.tencent.com/document/product/266/38096)をご参照ください。

## よくあるエラー

プレーヤー署名を使用した際、Player SDKがエラーコードを返した場合、よくある原因は次のとおりです。

- **署名の計算 [KEY](#p6) が間違っている**。 [デフォルト配信設定](https://intl.cloud.tencent.com/document/product/266/35768) 内の`再生キー`を使用する必要があります。KEY[リンク不正アクセス防止パラメータ](https://intl.cloud.tencent.com/document/product/266/33986#.E9.98.B2.E7.9B.97.E9.93.BE-url-.E7.94.9F.E6.88.90.E6.96.B9.E5.BC.8F) 内の`KEY`パラメータを誤って使用しているかどうかをチェックすることができます。
- **[署名パラメータ](#p0) 入力ミス**。例：
   - **パラメータタイプのエラー** 例えばappIdが整数で、誤って `appId:"125000123"`（文字列型）と入力している。または`contentInfo`内のトランスコードテンプレートパラメータが整数で、誤って`transcodeDefinition: "14011"`（文字列型）と入力している
   - **パラメータ値が有効範囲を超えている** 例えば`contentInfo`内の再生するオーディオビデオタイプのパラメータを、誤って`audioVideoType: "Transocde"`（スペルミス、有効な列挙値ではない）と入力している
