## 概要
Tencentは中国で最も早くに最大のインスタントメッセージを開発したデペロッパーです。産業界のデジタルトランスフォーメーショントレンドに対応し、Tencent Cloudは、SDKおよびREST APIの形式で並行性と信頼性の高いインスタントメッセージ機能を実装し、IM製品としてリリースしました。簡易な方法でTencent Cloudが提供するIM SDKをご自身のアプリケーションに統合し、サーバー側のREST APIと連携することで、インスタントメッセージ機能を容易に利用できます。IMサービスとアプリケーション間のインタラクションは下図に示すとおりです：
![](https://qcloudimg.tencent-cloud.cn/raw/2e57bf9cbb3a1855efe7abdfd7d8beab.png)
開発者の各段階におけるニーズおよび各シーンに合わせて、IMチームは一連のソリューションを提供します。それには、Android、iOS、Windows、WebのSDKコンポーネント、サーバーに統合する[REST APIインターフェース](https://intl.cloud.tencent.com/document/product/1047/34620)、[サードパーティコールバックインターフェース](https://intl.cloud.tencent.com/document/product/1047/34354) などが含まれます。開発者はこれらのコンポーネントおよび機能を利用して、信頼性が高く、かつ安定したインスタントメッセージ製品を簡単かつスピーディーに構築し、思いのままに世界中に届けることができます。

## アーキテクチャの紹介
IMはグローバルアクセス、シングルチャット、グループチャット、メッセージプッシュ、マネージドリレーションシップチェーン、アカウント認証などの全方位ソリューションを提供します。また、完全なAppアクセス、バックエンド管理インターフェースを提供します。
![](https://main.qcloudimg.com/raw/6537f6e705289419963ee647ae851c94.png)

## 業務の紹介
### アクセスサービス
アクセスサービスはIMに、全世界をカバーし、コネクティビティと信頼性が高く、強力なセキュリティを備えたネットワーク接続チャネルを提供します。自社開発した最適な多重アドレッシングアルゴリズムにより、ネットワーク全体のスケジューリング機能も有し、スマート互換技術を使用した透過ゲートウェイポリシー、長時間接続における多重化、トランスポート層のプロトコル最適化、チャネルの暗号化などにより、業務上でネットワークの細部に頭を悩ませる必要はなくなり、業務バックエンドとの間で簡単かつ信頼性の高い通信を安全に実現することができます。
端末からログインすると、IM SDKが最寄りのアクセスポイントまたはアクセラレーションポイントにアクセスします。グローバルアクセス・アクセラレーションポイントの分布は以下のとおりです：

- 中国：華南、華北、華東、中国香港、中国台湾など。
- その他の国（または地域）：
 - アジア：シンガポール、インドネシア、アラブ首長国連邦、タイ、マレーシア、日本、ベトナム、インド、韓国、フィリピンなど。
 - ヨーロッパ：イギリス、オランダ、フランス、ドイツ、イタリア、ノルウェー、フランス、ロシア、スペインなど。
 - 南アメリカ：ブラジルなど。
 - 北アメリカ：アメリカ、カナダ、メキシコなど。
 - オセアニア：オーストラリアなど。
 - アフリカ：南アフリカ共和国、ナイジェリアなど。

### データストレージセンター
IMは、中国、南アジア(インド)、東南アジア(シンガポール)、北東アジア(韓国ソウル)、ヨーロッパ(ドイツフランクフルト)、北米(米国シリコンバレー)のデータストレージセンターを提供します。ご利用の業務データはアプリケーションを作成する時に選択したデータセンターに保存されます。すべてのデータセンターは世界中のどこでもアクセスできます。

### シングルチャット
シングルチャットとは1V1のチャットのことであり、 テキスト、顔絵文字、位置情報、画像、音声、ショートビデオおよびカスタムメッセージなどを含む機能を提供します。Red Packet、チャットボット、メッセージ開封確認、メッセージ取り消しなどの特殊な機能を備えるほか、オフラインメッセージ、ローミングメッセージなどのサービスも提供します。詳細については[シングルチャットメッセージ](https://intl.cloud.tencent.com/document/product/1047/33523)ドキュメントをご参照ください。

### グループチャット
複数人によるチャットサービスです。グループの追加方法および組織管理形式の部分の違いにより、次の5種類のグループタイプを設けており、様々なグループチャットシーンのニーズに対応できます。

- **友達ワークグループ(Work)**：作成後はすでにグループ内にいるフレンドのみを招待して参加させることができ、かつ被招待者側の同意またはグループマスターの承認は不要です。
- **知らない人とのソーシャルグループ(Public)**：作成後はグループマスターがグループ管理者を指定できます。ユーザーはグループIDを検索してグループ参加申請を送信した後、グループマスターまたは管理者が申請を承認してからでないとグループに参加できません。
- **臨時ミーティンググループ（Meeting）**：作成後は自由に参加・退出でき、かつグループ参加前のメッセージを確認する機能をサポートしています。音声/ビデオ会議のシナリオ、eラーニングのシナリオなどのTRTC製品と連携させたシナリオに適しています。
- **ライブストリーミンググループ（AVChatRoom）**：作成後は自由に参加・退出ができ、グループ参加者数の上限はありませんが、メッセージ履歴の保存はサポートしていません。CSS製品との連携に適しており、弾幕チャットのシナリオに使用します。
- **コミュニティ（Community）**：作成後は、自由に出入りでき、知識の共有やゲームの交流など、大規模なコミュニティのグループチャットシーンに適しています。
>?コミュニティ（Community）機能は端末向けSDK 5.8.1668エンハンス以降、Web向けSDK 2.17.0以降をサポートします。この機能を使用するには、Ultimate版を購入し、[**コンソール**](https://console.cloud.tencent.com/im/qun-setting) > **グループ機能設定** > **コミュニティグループ** スイッチをオンにする必要があります。

グループは、カスタムグループタイプ、カスタムグループフィールド、カスタムグループメンバーフィールド、カスタムグループID、カスタムイベントコールバックなどを含む、高度なカスタマイズ性を有しています。Appはそれぞれのニーズに応じて細部までのカスタマイズを行うことができます。詳細については[グループシステム](https://intl.cloud.tencent.com/document/product/1047/33529)ドキュメントをご参照ください。
>!ライブストリーミンググループ（AVChatRoom）には参加者数の上限を設定していないが、短時間でグループ参加者の激増がありうる運用シーン（例えば、大規模オンラインイベントの開催により、単一グループの参加者が5万人以上に達する見込みの場合など）の場合、サービスリソースを調達するように、事前に[Tencent Cloudカスタマサービス](https://www.tencentcloud.com/contact-us)または営業担当者に連絡し、SDKAppIDとイベント予定開催時間を伝えてください。



### プロファイルマネージドリレーションシップチェーン
プロファイル、マネージドリレーションシップチェーンの一体型ソリューションを提供し、ユーザーのプロファイル（ニックネーム、プロフィール画像、カスタムプロファイルフィールドなど）、フレンドリスト、ブラックリストなどを保存できます。IMのプロファイルマネージドリレーションシップチェーンホスティングサービスは最大12セットのバックアップサービスを提供し、複数のデータセンターでのクロスリージョンデプロイにより、サービス品質と障害復旧効果を向上させます。詳細については[プロファイル管理](https://intl.cloud.tencent.com/document/product/1047/33520)、[リレーションシップチェーン管理](https://intl.cloud.tencent.com/document/product/1047/33521)ドキュメントをご参照ください。

### アカウント認証
安全な非対称暗号化ECDSA-SHA256およびハッシュ化HMAC-SHA256（HMAC-SHA256の使用を推奨）を提供します。開発者が直接Appを使用して、自分のアカウントへのIMサービスのクイックインテグレーションを行うことができ、煩雑なアカウントマッピングの作業を行わずにすみます。簡単なSDKインテグレーション、便利なインターフェースコールによって、ユーザーアカウント（UserID）とパスワード（UserSig）の認証が完了します。詳細については、[ログイン認証](https://intl.cloud.tencent.com/document/product/1047/33517)ドキュメントをご参照ください。

## 管理と監視
基本的なインスタントメッセージ機能のほかに、IMは便利で使いやすい管理コンソールも提供しています。このコンソールで、アプリケーションの作成、IM SDKのダウンロード、アプリケーション設定情報を照会してアプリケーションの調整、インスタントメッセージ機能の統合を行うことができます。また、コンソールではバックエンドメッセージの送信、グループ管理およびデータ統計などの機能も提供します。詳細については、[コンソールガイド](https://intl.cloud.tencent.com/document/product/1047/34577)ドキュメントをご参照ください。

## 高度な機能
### REST API
REST APIはHTTP管理用インターフェースであり、主な機能はAppバックエンドにバックエンド管理ポータルを提供することです。現時点でIMがサポートしているREST APIについては、[REST APIインターフェースの紹介](https://intl.cloud.tencent.com/document/product/1047/34620)ドキュメントをご参照ください。

REST API以外に、IMコンソールでも簡単なデータ管理、シングル/グループメッセージなどの機能を実現でき、開発者はIMコンソールでデータの管理、確認およびテストを行うことができます。比較すると、REST APIインターフェースの方が比較的ベーシックですが、より強力な管理機能を提供できます。


### サードパーティのコールバック
いわゆる[サードパーティのコールバック](https://intl.cloud.tencent.com/document/product/1047/34354)とは、あるイベントの発生前または発生後に、IMがAppのバックエンドサーバーにリクエストを送信し、Appバックエンドがこれに基づいて必要なデータを同期するか、またはイベントに介入してその後の処理プロセスを行うことを言います。
IMは豊富な種類のコールバックインターフェースを提供しており、現時点ではコールバック機能はすべて無料です。詳細については、[コールバックコマンドリスト](https://intl.cloud.tencent.com/document/product/1047/34355)ドキュメントをご参照ください。

## プライベートサービスのサポート
プライベートデプロイにより、企業はシステムを自社のサーバーに直接デプロイすることができ、データはローカルにそのまま保存されます。IMは、プライベートデプロイ機能をサポートしており、企業によるプライベートバージョンのデプロイ・実施・運用・保守を支援することができます。
>?申請するときは、Tencent Cloudルートアカウントにログインする必要があります。

## セキュリティコンプライアンス
コンプライアンスはTencent Cloud IMの発展の基本です。Tencent Cloud IMは各国および業界のコンプライアンス要件を遵守し、提供するサービスの**セキュリティ、コンプライアンス、可用性、機密保持およびプライバシー**を保証するほか、IMを使用するお客様に関連のサポートを提供することで、**企業とその顧客の様々なコンプライアンス監督管理のニーズを満たし、会社と顧客による監査業務への重複投資を削減し、監査と管理の効率を向上させます。**

<b>IMは一連のSOC報告書（SOC 1、SOC 2、SOC 3を含む）、サイバーセキュリティ等級保護2.0（3級）、ISOシリーズ認証（ISO 9001、ISO 20000、ISO 27001、ISO 27017、ISO 27018、ISO 27701、ISO 29151を含む）、CSA STAR、NIST CSF、BS10012およびKISMS等の認証を取得済みです。</b>

<style>
    .card-container {
        width: 380px;
				height:
        display: block;
        float: left;
        padding-left: 15px;
        padding-right: 15px;
        box-sizing: border-box;
    }

    .card {
        border-radius: 10px;
        padding-top: 10px;
        padding-left: 10px;
        padding-right: 10px;
        padding-bottom: 10px;
        margin-top: 30px;
        border: 1px solid #ebeef5;
        background-color: #fff;
        overflow: hidden;
        box-shadow: 0 2px 12px 0 rgb(0 0 0 / 10%);
        text-align: left;
    			height:260px;
    }
    
    .markdown-text-box img {
        box-shadow: none;
    }


    .titlename {
                color:#191919;f
        position: relative;
        top: -2px;
                font-weight: bolder;
                font-size: larger;
    }
        
        @media (max-width: 768px){
                .card-container,
                .scene-card-container{
                        width: 100%;
                }
                .scene-card > div{
                        width: 100%!important;
                        margin-left: 0!important;
                }
                img {
        box-shadow: none;
    }
        }
</style>

<div style="position: relative; box-sizing: border-box;  padding-bottom: 10px; margin-bottom: 10px; overflow:hidden">
    <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/7c288e0b31526692c16a8e4fe641d6db.jpg" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/11543">SOC 1 Type Ⅱレポート</a> </p>
																<p style="color:#586376;">AICPA監査基準SSAE No. 18のうちAT-C section 320を参照し、Tencent Cloudサービスシステムの制御環境について発行するレポートです</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/7c288e0b31526692c16a8e4fe641d6db.jpg" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/11543">SOC 2 Type Ⅱレポート</a> </p>
                                <p style="color:#586376;">AICPA監査基準SSAE No. 18のうちAT-C section 205およびTSP section 100 2017版を参照し、Tencent Cloudサービスシステムの安全性、可用性、機密性について発行するレポートです</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/7c288e0b31526692c16a8e4fe641d6db.jpg" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/11543">SOC 3 Type Ⅱレポート</a></p>
																<p style="color:#586376;">AICPA監査基準SSAE No. 18のうちAT-C section 205およびTSP section 100 2017版を参照し、Tencent Cloudサービスシステムの安全性、可用性、機密性報告について発行する一般制御レポートです</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/7e62e559319afa51562101026009f0e3.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://www.tencentcloud.com/document/product/363/2487">サイバーセキュリティ等級保護2.0 </a></p>
																<p style="color:#586376;">Tencent金融クラウドは等級保護レベル4の届出と評価に合格しており、パブリッククラウドは等級保護レベル3の届出と評価に合格しています</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/be5a02d7027805cec66391d24d5382d6.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/2410">ISO 9001品質管理システム認証</a>
																<p style="color:#586376;">Tencent Cloudは中国国内で初めてクラウドコンピューティング分野でISO 9001 CNASおよびANABのダブル認証を取得したクラウドコンピューティングプロバイダであり、効果の高い品質管理フローの実施により、優れたクラウドサービスを提供します</p></p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/0f2f62361c7420c58bfeab74c42373da.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/2409">ISO 20000 ITサービス管理システム認証</a> </p><p style="color:#586376;">Tencent Cloudは中国国内で初めてISO 20000-1:2018新版基準の認証を取得したクラウドコンピューティングプロバイダであり、標準のITサービス管理フローを構築して厳密に実施します</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/b3b88a42e294d602d7af7d42aa343b4d.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/2408">ISO 27001情報セキュリティマネジメントシステム認証</a></p><p style="color:#586376;">ISO/IEC 27001:2015は、ISO/IEC 27002:2013を補足するものです。Tencent CloudはISO 27001指導証書を取得済みであり、クラウドコンピューティングの情報セキュリティコントロールを有効に設計し、実施していることが証明されています</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/4934c5489f0cb35f8e1e16614fc07593.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/33541">ISO 27017クラウドサービス情報セキュリティコントロール実施ガイドライン</a></p><p style="color:#586376;">ISO/IEC 27017:2015は、ISO/IEC 27002:2013を補足するものです。Tencent CloudはISO 27017指導証書を取得済みであり、クラウドコンピューティングの情報セキュリティコントロールを有効に設計し、実施していることが証明されています</p>
            </div>
 </div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/c5b246657205e0023ea89b19d95b6753.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/14031">ISO 27018パブリッククラウド個人情報保護認証</a></p><p style="color:#586376;">Tencent Cloudは、個々のお客様の個人情報の保護に力を入れており、整った個人情報管理システムを構築し、さまざまな技術的手段によりユーザーの個人情報を保護しています</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/0b37fbf8d1bfa04031db30ed15d76f9b.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/33540">ISO 27701個人情報マネジメントシステム国際基準</a> <p style="color:#586376;">Tencent Cloudは世界で初めてISO/IEC 27701認証を取得したクラウドサービスプロバイダであり、プライバシー情報マネジメントシステムを構築、実施しており、継続的に改善する能力を持っています</p></p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/f652574979d9db78c8a991ca4b8a78fc.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://www.tencentcloud.com/document/product/363/39609">ISO 29151個人識別可能情報保護実施ガイドライン</a> </p><p style="color:#586376;">Tencent Cloudは、個人識別可能情報の保護のために適切な情報セキュリティリスクマネジメント環境を提供しており、同時に業界のベストプラクティスを達成し、継続的に改善する能力を持っています</p>
            </div>
        </div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/32d85d30e2129e5f22259918ff1d6619.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/7249">CSA STARクラウドセキュリティマネジメントシステム認証</a> </p><p style="color:#586376;">CSA STARはクラウドセキュリティに特化した国際的な認証であり、Tencent CloudはゴールドレベルのSTAR認証を取得しており、クラウドセキュリティ技術の統制を強化しています</p>
            </div>
</div>
 <div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;" src="https://qcloudimg.tencent-cloud.cn/raw/a18be30e18d5f87d324094f9353083d0.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/45469">NISTサイバーセキュリティフレームワーク</a> </p><p style="color:#586376;">NIST CSFは、アメリカ国立標準技術研究所が大統領令（E0）13636の「重要インフラのサイバーセキュリティ強化」に基づいて開発されたもので、このフレームワークは業務の駆動要因を用いてサイバーセキュリティ活動を指導することに重きを置いています</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"src="https://qcloudimg.tencent-cloud.cn/raw/23115be55af090caf230525be53b883d.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://intl.cloud.tencent.com/document/product/363/34542">KISMS認証</a> </p><p style="color:#586376;">Tencent Cloudは、中国で初めてKISMS認証を取得したクラウドコンピューティングプロバイダであり、Tencent Cloudが構築している情報セキュリティマネジメントシステムと機能が、関連する韓国の法律と標準のコンプライアンス要件を満たしていることを証明しています</p>
            </div>
</div>
<div class="card-container">
            <div class="card">
                           <img style="width:100px; max-width: inherit;"  src="https://qcloudimg.tencent-cloud.cn/raw/eac6c9f40236f5ad1028ddbb34a2c5cb.png" data-nonescope="true">
                                <p class="titlename">  <a href="https://www.tencentcloud.com/document/product/363/45470">BS 10012 </a></p><p style="color:#586376;">英国規格協会が公布した個人情報マネジメントシステム規格</p>
            </div>
</div>
</div>



