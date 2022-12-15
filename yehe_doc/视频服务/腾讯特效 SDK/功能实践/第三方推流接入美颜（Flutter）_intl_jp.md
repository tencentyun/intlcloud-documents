Flutter端末のGL環境はネイティブ端末の環境から隔離されているため、Flutterに美顔を接続する際に直接バインド関係を確立することができません。下図のようにネイティブ端末で関係のバインドを行う必要があります。
<img src="https://qcloudimg.tencent-cloud.cn/raw/73bbc3c15e95db29a270fc4e1927a026.png" style="zoom:50%;" />

## 実現方式の全体フロー
1. 美顔側で1層のインターフェースを抽象化し、美顔側にインターフェースを実装します。
2. アプリケーションの起動時にこのインターフェースをサードパーティプッシュ端末に登録することで、サードパーティプッシュ端末がこのインターフェースによって美顔インスタンスを作成、使用、破棄できるようになります。
3. サードパーティプッシュ端末は美顔の作成および破棄機能を自身のFlutter端末に公開して、お客様が使用できるようにします。
4. 美顔属性の設定は美顔のFlutter SDK機能によって処理することができます。


### TRTCの例
美顔側が定義するインターフェース：
```java
public interface ITXCustomBeautyProcesserFactory {

    /**
     * 美顔インスタンスの作成
     * @return
     */
    ITXCustomBeautyProcesser createCustomBeautyProcesser();

    /**
     * 美顔インスタンスの破棄（GLスレッドで呼び出す必要があります）
     */
    void destroyCustomBeautyProcesser();
}
public interface ITXCustomBeautyProcesser {

   //美顔がサポートするビデオフレームのピクセル形式を取得します。美顔がサポートしているのはOpenGL 2Dテクスチャです。
    TXCustomBeautyPixelFormat getSupportedPixelFormat();
    //美顔がサポートするビデオデータパッケージ形式を取得します。美顔がサポートしているのはV2TXLiveBufferTypeTextureです。テクスチャIDを直接操作でき、パフォーマンスが最良で、画質ロスが最少です。
    TXCustomBeautyBufferType getSupportedBufferType();
   //GLスレッドで呼び出します（srcFrameにはRGBAテクスチャ、およびwidth、heightが含まれる必要があります）。美顔処理後に処理後のテクスチャオブジェクトをdstFrame内のtexture.textureId内に配置します。
    void onProcessVideoFrame(TXCustomBeautyVideoFrame srcFrame, TXCustomBeautyVideoFrame dstFrame);
}
```

1. TRTCで登録メソッドを提供しています。アプリケーションの起動時に、美顔側のITXCustomBeautyProcesserFactoryインターフェースの実装クラス`com.tencent.effect.tencent_effect_flutter.XmagicProcesserFactory`をTRTCに登録します（ネイティブ端末で行います）。
![](https://qcloudimg.tencent-cloud.cn/raw/9b21d439c06afcf3b01ef969931dd992.png)
2. `Flutter`層で、カスタム美顔インターフェースの有効化と無効化を行う`Future<V2TXLiveCode> enableCustomVideoProcess(bool enable)`インターフェースを提供します。
3. TRTCネイティブ端末に美顔オン/オフメソッドを実装します。
![](https://qcloudimg.tencent-cloud.cn/raw/5a8b502b3700bf853d13d9112536c4c8.png)
![](https://qcloudimg.tencent-cloud.cn/raw/a58a0f003061b067a503138b92571894.png)



## 付録
**美顔が提供する抽象化層の依存**
```groovy
///
implementation 'com.tencent.liteav:custom-video-processor:latest.release'
```
