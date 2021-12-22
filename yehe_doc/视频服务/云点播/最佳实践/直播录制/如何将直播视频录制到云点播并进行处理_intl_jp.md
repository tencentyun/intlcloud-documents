CSSレコーディングのソリューションは、ライブストリーミングのオリジナルストリームをオーディオ・ビデオパッケージングに変換（音声、ビデオデータおよび対応するタイムスタンプなどの情報は変更しない）することで得られるファイルをTencent Cloud VODプラットフォームに保存し、さらにレコーディングファイルに対する二次制作、配信、再生を行なうスタンダードソリューションです。詳細については、[CSSレコーディングソリューション](https://intl.cloud.tencent.com/document/product/1082)をご参照ください。

## 製品の特性
- Tencent Cloud CSSの機能をベースとして、CSSストリームのコンテンツを素早くレコーディングしてクラウドプラットフォームに保存し、さらに二次制作および配信を行うことができます。
- Tencent Cloudの最先端のオーディオビデオAI技術と全世界の膨大なライブストリーミングアクセラレーションノードをベースとして、専門的で安定性の高いCSSプッシュ、トランスコーディング、配信および再生サービスを提供します。超低遅延、超高画質、大規模並列処理（同時アクセス）のニーズに全面的に対応します。
- CSSレコーディングサービスをベースとして、お客様のライブストリーミングイベントを各種のユースケースやAppの中でスピーディーに伝播させることができます。
- 企業のライブストリーミング、eコマース、eラーニングのライブストリーミングなど多様な業界のシナリオに適用できます。またTencent Videoなど、多様な配信方式にも適用できます。

## 前提条件
-Tencent Cloudアカウントを[登録](https://intl.cloud.tencent.com/register)して[ログイン](https://intl.cloud.tencent.com/login)し、アカウントの実名認証を完了していること。実名認証を完了していないユーザーは、中国大陸のCSSレコーディングのVODへの変換インスタンスを購入できません。
- Tencent CloudのCSSとVODのサービスをアクティブ化します。まだアクティブになっていない場合は、 [CSSサービス](https://console.cloud.tencent.com/live/livestat) と [VODサービス](https://console.cloud.tencent.com/vod/overview) をアクティブ化してください。

## 実践手順
### 手順1：レコーディングテンプレートの作成
レコーディング機能を使用するには、まずレコーディングテンプレートを作成する必要があり、CSSレコーディング機能の設定はいずれもレコーディングテンプレートの中に保存します。様々な設定のレコーディングテンプレートを作成することで、様々な形式、様々な長さでのレコーディングファイルなどを実現できます。
- **コンソールから作成する方法**：
   1. [CSSコンソール](https://console.cloud.tencent.com/live/config/record)に入り、**機能設定**>[**CSSレコーディング**](https://console.cloud.tencent.com/live/config/record)を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/2e5d358a74f16e96a3e22fd1eb90da2b.png)

   2. **レコーディングテンプレート作成**をクリックし、必要なレコーディングファイルタイプを選択します（少なくとも1種類の形式を選択）。その他の設定項目の説明については、[レコーディングテンプレートの作成](https://intl.cloud.tencent.com/document/product/267/34223)をご参照ください。
		![](https://qcloudimg.tencent-cloud.cn/raw/10f22f9bd8bc59769ae8afb0f45aabc5.png)
		
   3. **保存**をクリックすれば、テンプレートの作成が完了します。
- **APIによる作成**：
[CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845) インターフェースを呼び出してレコーディングテンプレートを作成します。テンプレートの作成に成功すると対応するテンプレートIDが返ってきます。

### 手順2：レコーディング方法の選択
CSSでは様々なシナリオにもとづき、以下の種類のCSSレコーディング機能を呼び出す方法を提供しています。

#### 方法1：ドメイン名指定によるグローバルレコーディング
[CSSコンソール](https://console.cloud.tencent.com/live/config/record)またはAPIを呼び出して、CSSレコーディングテンプレートをプッシュドメイン名にバインドします。このドメイン名経由でプッシュした場合のみ自動レコーディングが行なわれます。

- **適用ケース**：ショーのライブストリーミング、eコマースライブストリーミング、オンライン講座、ビデオ監視などのフルレコーディングシナリオ。
- **操作フロー**：
	1. レコーディングテンプレートの作成に成功すると、[ドメイン名のバインド](https://console.cloud.tencent.com/live/config/record)を促すポップアップボックスが表示されますので、**ドメイン名のバインドに進む**をクリックしてプッシュドメイン名を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/0470af86e47f87158773ef09558afbcf.png)

   2. [**ドメイン名管理**](https://console.cloud.tencent.com/live/domainmanage)の中で、お客様の[CSSプッシュドメイン名](https://console.cloud.tencent.com/live/domainmanage)をクリックすると、プッシュ詳細ページに移動します。その後、**テンプレート設定**>**レコーディング設定**と選択し、**編集**をクリックすれば、プッシュドメイン名をバインドできます。詳細については、[レコーディングテンプレートの関連付け](https://intl.cloud.tencent.com/document/product/267/34224)をご参照ください。
![](https://qcloudimg.tencent-cloud.cn/raw/cb47ae54e0d17121fb0956886edbf5d5.png)

   3. [CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846)インターフェースを介してレコーディングテンプレートのテンプレートIDとプッシュドメイン名を渡せば、レコーディングテンプレートとプッシュドメイン名のバインドが完了します。

#### 方法2：単独ストリームの指定によるレコーディング
APIを介してCSSレコーディングテンプレートを特定のCSSストリームにバインドし、これによりその特定のCSSストリームのレコーディングを実現します。

- **適用ケース**：イベント・展示会・試合のライブストリーミングやマイク接続によるコラボライブなど、単独のイベントのための特殊なレコーディングシナリオ。
- **操作フロー**：[CreateLiveRecordRule](https://intl.cloud.tencent.com/document/product/267/30846)インターフェースを介してレコーディングルールを作成し、レコーディングテンプレートのテンプレートIDとバインドしたいドメイン名、パス、ストリーム名StreamName（必ず正確にマッチさせること）を渡せば、レコーディングテンプレートと指定CSSストリームのバインドが完了します。

#### 方法3：指定時間帯によるレコーディング
APIを呼び出すことでレコーディングの開始時間と終了時間を制御でき、指定した時間内にレコーディングタスクをトリガーしてレコーディングを行います。

- **適用ケース**：ニュースやイベントのライブストリーミングなど、ライブストリーミングのフローが比較的明確なレコーディングシナリオ。
- **操作フロー**：[CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)インターフェースを介してレコーディングタスクを作成し、レコーディングテンプレートのテンプレートIDとバインドしたいドメイン名、パス、ストリーム名StreamName（必ず正確にマッチさせること）を指定します。設定ではレコーディングの開始時間および終了時間を設定する必要があり、これにより開始時間にレコーディングがスタートします。
- **レコーディング例**：
 1. 最もシンプルなケースでは、指定されたStreamName、DomainName、AppNameとEndTimeパラメータを入力するだけです。
例：2020年08月10日午前08時から10時までのレコーディングタスクを作成、FLV形式、ビデオレコーディング、セグメント30分、永久保存。
入力例：
```
https://live.tencentcloudapi.com/?Action=CreateRecordTask&AppName=live&DomainName=mytest.live.push.com&StreamName=livetest&StartTime=1597017600&EndTime=1597024800&TemplateId=0&<パブリックリクエストパラメータ>
```
 2. さらに具体的なレコーディング形式、レコーディングタイプ、ストレージパラメータなどを指定できます。
例：2020年08月10日午前08時から10時までのレコーディングタスクを作成、MP4形式、セグメント1時間、永久保存。
 3. [CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845)を呼び出して、始めにレコーディングテンプレートを作成します。
 入力例：
 ```
 https://live.tencentcloudapi.com/?Action=CreateLiveRecordTemplate&TemplateName=templat&Description=test&Mp4Param.Enable=1&Mp4Param.RecordInterval=3600&Mp4Param.StorageTime=0&<パブリックリクエストパラメータ>
 ```
 出力例：
 ```
 {"Response": {"RequestId": "839d12da-95a9-43b2-a9a0-03366d01b532","TemplateId": 17016}}
 ```
 4. [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)を呼び出してレコーディングタスクを作成します。
 入力例：
 ```
 https://live.tencentcloudapi.com/?Action=CreateRecordTask&StreamName=livetest&AppName=live&DomainName=mytest.live.push.com&StartTime=1597017600&EndTime=1597024800&TemplateId=17016&<パブリックリクエストパラメータ>
 ```

#### 方法4：ハイライトレコーディング（ミクスストリーミングのレコーディングに対応）
ライブストリーミングの最中に素晴らしい場面に遭遇したときに、APIを呼び出してリアルタイムにCSSレコーディングを行なうことができます。

- **適用ケース**：試合やゲームのライブストリーミングなど、部分的な場面のレコーディングのみが必要なシナリオ（またはグローバルレコーディング後にトリミングを行なう場合）。
- **操作フロー**：[CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)インターフェースを介してレコーディングタスクを作成し、レコーディングテンプレートのテンプレートIDとバインドしたいドメイン名、パス、ストリーム名StreamName（必ず正確にマッチさせること）を指定します。設定ではレコーディングの終了時間を設定する必要があり、作成が完了するとレコーディングタスクがスタートします。
- **レコーディング例**：
 ```
 https://live.tencentcloudapi.com/?Action=CreateRecordTask&StreamName=test&AppName=live&DomainName=mytest.live.push.com&EndTime=1597024800&<パブリックリクエストパラメータ>
 ```

#### 方法5：純音声のレコーディング
純粋に音声のみのプッシュの場合は、AACの純音声レコーディングを設定することができます。

- **適用ケース**：音声ライブストリーミング、音声マイク接続などのシナリオ。
- **操作フロー**：レコーディングテンプレートの作成時、レコーディングファイルタイプにACC純音声レコーディングを選択し、対応するプッシュアドレスとの関連付けを行います。
>!バインディングルールは作成後約5～10分経ってから有効となります。バインディングルールの修正はプッシュ中のライブストリーミングには影響しません。新しくプッシュするCSSストリームに対してのみ有効となります。

### 手順3：CSSプッシュの開始
[手順2](#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E9.80.89.E6.8B.A9.E5.BD.95.E5.88.B6.E6.96.B9.E6.A1.88)にしたがってレコーディングテンプレートをプッシュドメイン名にバインドすると、そのプッシュアドレスによって対応するプッシュドメイン名が生成され、[CSSプッシュ](https://intl.cloud.tencent.com/document/product/267/31558)が行なわれます。

ライブストリーミングの終了後、レコーディングによって生成されたファイルは[VOD](https://console.cloud.tencent.com/vod/overview) プラットフォームに保存されます。

>?
>- レコーディングテンプレートの中でレコーディング先にサブアプリケーションを選択すると、対応するサブアプリケーションの下に保存されます。
>- レコーディングファイルのアドレス情報をコールバックしたい場合は、プッシュ前にコールバックテンプレートを作成して、レコーディングコールバックアドレスを入力してから保存し、さらにコールバックしたいプッシュドメイン名をバインドする必要があります。詳細については、[レコーディングイベント通知](https://intl.cloud.tencent.com/document/product/267/38082)をご参照ください。

### 手順4：レコーディングファイルの取得
次の方式によるレコーディングファイルのクエリーと取得をサポートしています。
- **レコーディングコールバックによる取得**：CSSプッシュの前にコールバックテンプレートを設定し（テンプレートには[レコーディングコールバックアドレスの設定](https://console.cloud.tencent.com/live/config/callback)が必要です）、レコーディングファイル生成時にコールバックによってファイルをコールバックサーバーに送信します。詳細については、[レコーディングイベント通知](https://intl.cloud.tencent.com/document/product/267/38082)をご参照ください。
![](https://qcloudimg.tencent-cloud.cn/raw/b45fc96295f66ee31506adb89724be10.png)
- **VODコンソールによる取得**：[VODコンソール](https://console.cloud.tencent.com/vod/media)でクエリーを行います、具体的な内容は、[ビデオの確認](https://intl.cloud.tencent.com/document/product/266/33895)をご参照ください。
- **VOD APIによる取得**：[SearchMedia](https://intl.cloud.tencent.com/document/product/266/34179)インターフェースを呼び出してファイルのクエリーを行います。

### 手順5：レコーディングファイルの処理
#### 方法1：CSSレコーディング + 自動トランスコーディング + ビデオアクセラレーション再生
- **適用ケース**：CSSレコーディング後にレコーディングファイルに対する自動トランスコーディングとビデオアクセラレーションを素早く行い、ユーザーがVODを再生できるようにします。ビデオ二次加工が不要なほとんどのライブストリーミングシナリオに適用できます。
- **操作フロー**：
	1. CSSプッシュのレコーディング前にレコーディングテンプレートを作成し、**高度な設定**をクリックしてタスクフローを設定します。
	![](https://qcloudimg.tencent-cloud.cn/raw/7fde65073d08b85a920f7466752ebbb7.png)
	2. VODコンソールで事前に作成したタスクフローテンプレートをバインドします。
	![](https://qcloudimg.tencent-cloud.cn/raw/5165daf69f81f1e22691985c90a169b5.png)
	3.お客様がCSSプッシュを行う場合は、[CSSプッシュ](https://intl.cloud.tencent.com/document/product/267/31558)をご参照ください。
	4. CSSレコーディングが完了したら、オンデマンドのFileIdを取得します。
	![](https://qcloudimg.tencent-cloud.cn/raw/364e3d8ed23147c6f65f1aafc3029355.png)
	5. 再生アドレスを取得し再生します。

#### 方法2：CSSレコーディング + 手動トランスコーディング + ビデオアクセラレーション再生
- **適用ケース**：一部のユーザーは、CSSレコーディングのビデオを先にVODに保存だけして、その後のトランスコーディングの操作は行わないことを希望することがあります。この場合は新規作成したレコーディングをVODに保存する時に、その他の操作を追加しないことができます。後からビデオに対してトランスコーディングを行いたい場合は、手動でトランスコーディング操作を起動することができます。また、VODのクラウドトリミング機能と連携させて使用すれば、より素晴らしい効果が得られます。

- **操作フロー**：
	1.お客様がCSSプッシュを行う場合は、[CSSプッシュ](https://intl.cloud.tencent.com/document/product/267/31558)をご参照ください。
	2. ファイルが自動的にレコーディングされ、VODに保存されます。
	3. VOD FileIdを取得します。
	4. トランスコードテンプレートを設定するか、タスクフローを手動でトランスコードします。詳細については、[テンプレート設定](https://intl.cloud.tencent.com/document/product/266/14059)をご参照ください。
	![](https://qcloudimg.tencent-cloud.cn/raw/e3c28f4fdb86ee215b12b17c1e06d4d5.png)
	5. お客様は、ビデオの二次編集を選択することができます。
	6. トランスコーディングおよび処理の完了後、ビデオアドレスを取得してその後の再生を行います。

#### 方法3：CSSレコーディング + アダプティブビットレートストリーミング + ビデオアクセラレーション + Super Player

- **適用ケース**：一部のユーザーは、ビデオのセキュリティに対して極めて高い要求があり、一般的なHLS 暗号化ではその暗号化に対するニーズを満たすことができませんが、ABSおよびSuper Playerを組み合わせて使用すれば、ビデオのセキュリティレベルを効果的に高めることができます。eラーニング、企業のトレーニングのような顧客シナリオに非常に適しています。

- **操作フロー**：
	1.お客様がCSSプッシュを行う場合は、[CSSプッシュ](https://intl.cloud.tencent.com/document/product/267/31558)をご参照ください。
	2. ファイルが自動的にレコーディングされ、VODに保存されます。
	3. VOD FileIdを取得します。
	4. ABSに変換するタスクフローを設定します。詳細については、[タスクフロー設定](https://intl.cloud.tencent.com/document/product/266/14058)をご参照ください。
	![](https://qcloudimg.tencent-cloud.cn/raw/7092c5503c4e0a50ec8214bf04159c46.png)
	5. スーパー再生の構成を設定し、作成したABSを選択して再生します。
		![](https://qcloudimg.tencent-cloud.cn/raw/cd16bb39eefc97e1d266f18402e2aaee.png)
	6. FileIdを使用してビデオを再生します。

