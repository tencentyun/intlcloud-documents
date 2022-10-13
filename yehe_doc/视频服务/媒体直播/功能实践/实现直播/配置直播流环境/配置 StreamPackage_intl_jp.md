このセクションでは、StreamPackageの設定方法についてご説明します。

1. [StreamPackageコンソールトップページ](https://console.tencentcloud.com/mdp/channel)に進み、初めに業務ニーズに応じて最寄りのリージョンを選択します。![](https://qcloudimg.tencent-cloud.cn/raw/9e2a246d5681ee392a1c8c70cd342de3.png)
2. **Create Channel**をクリックしてチャネルを作成し、設定に必要な情報を入力します。![](https://qcloudimg.tencent-cloud.cn/raw/beef79acbc0bb01fdc795adabd23cf83.png)
- **Input Protocol**： HLSおよびDASHをサポートしています。ここではHLSを例にします。
- **Max Segment Duration**：このチャネルにプッシュするHLSストリームのtsファイルの最大時間を表します。推奨設定は4秒です。
- **Max Playlist Duration**：このチャネルにプッシュするHLSストリームのm3u8再生リストファイルの最大時間を表します。推奨設定は12秒、すなわちm3u8に3つのセグメントが含まれることになります。

3. 必要な設定情報を送信すると、自動的にチャネルの高度な設定ページに進みます。設定情報は**Information**に表示され、その中のライブストリーミングプッシュアドレス**Input**、back-to-originプルストリーミングアドレス**Endpoints**および**CDN**アクセラレーションについて、さらに設定を行うことができます。

4. **Input**：システムは2つのInputプッシュノードアドレスを自動的に作成し、マスター/スレーブプッシュ操作を行いやすくすることで、可用性の高いライブストリーミングオリジンサーバーサービスを実現します。
![](https://qcloudimg.tencent-cloud.cn/raw/48526b3405cd4373f41f95aa254c4a37.png)
- このうち、各Inputには独立したアクセス認証情報を設定することができます。**Input Authentication**スイッチをオンにすると、システムは1組の**Username / Password**を自動的に作成します。ここに挿入![](https://qcloudimg.tencent-cloud.cn/raw/c32de384eda1fa084d50b13f243a9021.png)
- このとき、**Rotate credentials**をクリックすると、ただちに新しい認証情報が生成され、元の情報は復元できなくなります。
- 他のサードパーティサービスによってこのアドレスにライブストリームデータをプッシュしたい場合は、事前に**Input Url**および**Authentication**情報を記録しておいてください。

5. **Endpoint**：**Endpoint**タブに進み、**Create Endpoint**をクリックしてback-to-originプルノードアドレスを作成します。ここでは、IPブラックリスト/ホワイトリスト（IP Restriction）、認証キー（AuthKey）という2つのアクセス方法をサポートしています。Channel作成の際にHLSプロトコルを選択しているため、システムもHLSのback-to-originアドレスを生成します。このアドレスは実際にはmain.m3u8の完全なパスです。
![](https://qcloudimg.tencent-cloud.cn/raw/43f73db0ecaba6c72d7eb4677397caad.png)

6. これでStreamPackageチャネルの設定は完了しました。**Channel Management**トップページに戻り、チャネルリストで先ほど設定したチャネルを見つけ、チャネル**ID**および**Endpoint Url**を記録します。これらはこの後の設定操作の際に使用します。
![](https://qcloudimg.tencent-cloud.cn/raw/5eb1b481f758f89ec7a1279d7bd4d873.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3f7c30d33e17425a44dca05a701e8ad7.png)