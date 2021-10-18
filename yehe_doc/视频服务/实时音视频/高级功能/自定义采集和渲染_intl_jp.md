## 内容紹介

- **ビデオキャプチャのカスタマイズ**
  美顔や特殊効果処理モジュールを自社開発（またはサードパーティから購入）する場合は、カメラで撮影した画面を自身でキャプチャし処理する必要があります。この場合はTRTCCloudの`enableCustomVideoCapture`インターフェースを介してTRTC SDK自体のカメラキャプチャと画像処理ロジックをオフにすることが可能です。その後 `sendCustomVideoData` インターフェースを使用し TRTC SDKに自身のビデオデータを入力することができます。
- **ビデオレンダリングのカスタマイズ**
  TRTC SDKは、OpenGLを使用してビデオ画面のレンダリングを行います。ゲーム開発に使用する場合、または自身のインターフェースエンジンにTRTC SDKを埋め込む場合は、自身でビデオ画面をレンダリングする必要があります。
- **オーディオキャプチャのカスタマイズ**
  特殊なハードウェアデバイスでTRTC SDKを使用し、外部の音声キャプチャデバイスに接続して自身で音声データをキャプチャする必要がある場合はTRTCCloudの`enableCustomAudioCapture`インターフェースを介してTRTC SDKデフォルトのサウンドキャプチャプロセスをオフにする必要があります。その後、`sendCustomAudioData`インターフェースを使用してTRTC SDKに自身の声音データを入力することができます。
>!オーディオキャプチャのカスタマイズを有効にすると、エコーキャンセル（AEC）機能が無効になる場合があります。
- **オーディオ生データの取得**
  音声モジュールは非常に複雑で、SDKは音声デバイスのキャプチャおよび再生ロジックを厳密に制御する必要があります。一部シーンにおいて、リモートユーザーのオーディオデータまたはローカルマイクによってキャプチャされたオーディオデータを取得する必要がある場合は、TRTC SDKによって提供される対応するコールバックインターフェースを介して取得することができます。

## サポートするプラットフォーム

|   iOS    | Android  |  Mac OS  | Windows  | web         |  Flutter  |
| :------: | :------: | :------: | :------: | :-----------: |:--------: |
| &#10003; | &#10003; | &#10003; | &#10003; | &#10003;（[Web](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-20-advanced-customized-capture-rendering.html)）     |     ×    |

## ビデオキャプチャのカスタマイズ

TRTCCloudの`enableCustomVideoCapture`インターフェースを介してTRTC SDK自体のカメラキャプチャと画像処理ロジックをオフにします。その後、`sendCustomVideoData`インターフェースを使用してTRTC SDKに自身のビデオデータを入力することができます。

`sendCustomVideoData`インターフェースに`TRTCVideoFrame`と呼ばれるビデオ画像のフレームを表すパラメータがあります。不要なパフォーマンスロスを回避するため、TRTC SDKに入力されるビデオデータには、プラットフォームごとに異なるフォーマット要件があります。具体的な要件は次のとおりです。

<dx-tabs>
::: iOS\sプラットフォーム
TRTC SDKはNV12とi420という2種類のiOSバージョンのYUVデータ形式をサポートします。iOSプラットフォームにおいて、より高性能な画像転送方法はCVPixelBufferRefであるため、次のパラメータ形式を推奨します。

|  パラメータ名   |       パラメータタイプ       |                      推奨値                       |                           付注                           |
| :---------: | :------------------: | :-------------------------------------------------: | :----------------------------------------------------------: |
| pixelFormat | TRTCVideoPixelFormat |              TRTCVideoPixelFormat_NV12              |       iOSプラットフォーム上でカメラでキャプチャされるネイティブのビデオ形式はNV12です。        |
| bufferType  | TRTCVideoBufferType  |                     PixelBuffer                     |            iOSでネイティブにサポートされているビデオフレーム形式。最も高いパフォーマンスを発揮します。            |
| pixelBuffer |   CVPixelBufferRef   | TRTCVideoBufferTypeがPixelBufferの場合は入力する必要があります。 |     iPhoneのカメラでキャプチャされるデータはNV12形式のPixelBufferです。      |
|    data     |       NSData\*       |   TRTCVideoBufferTypeがNSDataの場合は入力する必要があります。    |                    性能はPixelBufferほど高くありません。                    |
|  timestamp  |       uint64_t       |                          0                          | 0を入力できます。SDKはこのようにtimestampフィールドへの入力をカスタマイズできますが、sendCustomVideoDataの呼び出し間隔を**均等**に制御してください。 |
|    width    |       uint64_t       |                   ビデオ画面の幅                    |                渡される画面のピクセル幅を正確に入力してください。                |
|   height    |       uint32_t       |                   ビデオ画面の高さ                    |                渡される画面のピクセル高さを正確に入力してください。                |
|  rotation   |  TRTCVideoRotation   |                       未入力                        | <ul style="margin:0"><li/>デフォルトは未入力。 <li/>画面を回転させたい場合は、`TRTCVideoRotation_0`、`TRTCVideoRotation_90`、`TRTCVideoRotation_180`、`TRTCVideoRotation_270`と入力します。SDKがその値に応じて対応する角度にビデオを時計回りに回転させます。例えば、縦画面の場合、`TRTCVideoRotation_90`と入力すると、SDKが画面を回転させて横表示にします。</ul> |

#### サンプルコード
[Demo]フォルダの中に`TestSendCustomVideoData.m`という名のファイルがあり、これにはローカルビデオファイルの中からNV12形式のPixelBufferを読み取り、SDKを介して後続の処理を行う方法が示されています。

```objectiveC
//TRTCVideoFrameをアセンブルし、trtcCloudオブジェクトに送信します
TRTCVideoFrame* videoFrame = [TRTCVideoFrame new];
videoFrame.bufferType = TRTCVideoBufferType_PixelBuffer;
videoFrame.pixelFormat = TRTCVideoPixelFormat_NV12;
videoFrame.pixelBuffer = CMSampleBufferGetImageBuffer(sampleBuffer);
        
[trtcCloud sendCustomVideoData:videoFrame];      
```
:::
::: Android\sプラットフォーム
Androidプラットフォームには、次の2種類のスキームがあります。
- **bufferスキーム**：ドッキングは比較的簡単ですが、性能が劣ります。高解像度のシナリオには適しません。
bufferでは、byte[]型の配列をTRTCSDKに直接挿入することが要求され、i420およびNV21のYUVフォーマットをサポートします。
<table>
<thead><tr><th>パラメータ名</th><th>パラメータタイプ</th><th>推奨値</th><th>付注</th></tr></thead>
<tbody><tr>
  <td>pixelFormat</td>
  <td>int</td>
  <td>TRTC_VIDEO_PIXEL_FORMAT_I420または<br> TRTC_VIDEO_PIXEL_FORMAT_NV21</td>
  <td>i420とNV21は、異なる2種類のYUVデータ形式です。</td>
</tr><tr>
  <td>bufferType</td>
  <td>int</td>
  <td>TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY</td>
  <td>dataを使用する方式にYUVデータの転送を指定。</td>
</tr><tr>
  <td>texture</td>
  <td>TRTCTexture</td>
  <td>bufferスキームの場合は入力しません</td>
  <td>i420またはNV21の2種類の形式を選択する場合、このパラメータは入力しません。</td>
</tr><tr>
  <td>data</td>
  <td>byte[]</td>
  <td>YUV形式のデータbuffer</td>
  <td>パッケージングされているのは、Javaタイプのメモリです。Javaレイヤーでの使用に適しています。</td>
</tr><tr>
  <td>buffer</td>
  <td>ByteBuffer</td>
  <td>bufferスキームの場合は入力しません</td>
  <td>パッケージングされているのは、C/C++ タイプのメモリです。JNIレイヤーでの使用に適しています。</td>
</tr><tr>
  <td>width</td>
  <td>uint64_t</td>
  <td>ビデオ画面の幅</td>
  <td>渡される画面のピクセル幅を正確に入力してください。</td>
</tr><tr>
  <td>height</td>
  <td>uint32_t</td>
  <td>ビデオ画面の高さ</td>
  <td>渡される画面のピクセル高さを正確に入力してください。</td>
</tr><tr>
  <td>timestamp</td>
  <td>long</td>
  <td>ビデオフレームのキャプチャ時間</td>
  <td>0を入力できます。この場合SDKがtimestampフィールドを自動入力します。ただしsendCustomVideoDataの呼び出し間隔が<strong>均等</strong>になるように制御してください。</td>
</tr><tr>
  <td>rotation</td>
  <td>int</td>
  <td>未入力</td>
  <td><li>デフォルトでは未入力。 </li><li>画面を回転させたい場合は、0、90、180、270と入力します。SDKがその値に応じてビデオを対応する角度まで時計回りに回転させます。例えば、縦画面の場合、90と入力すると、SDKが画面を回転させて横表示にします。</li></td>
</tr></tbody></table>

- **textureスキーム**：ドッキングにはある程度のOpenGLの基礎が必要です。ただし性能は良く、とりわけ画面解像度が高いときに良好です。
textureはTRTC SDKにOpenGLテクスチャを渡す必要があります。この方法の正常な動作を保証するには、事前にOpenGL環境を設定しておく必要があるため、この方法のドッキング難度は極めて高いものとなっています。OpenGLを学んだことがない場合は、当社が提供するサンプルコードを直接使用することを推奨します。サンプルコードは[Demo]の `customCapture` フォルダにあり、次のファイルが含まれています。
<table><thead><tr><th>ファイル名</th><th>ソースコードロジック</th></tr></thead>
<tbody>
<tr><td>TestSendCustomData.java</td>
<td>TRTCCloudのsendCustomVideoData関数を介して、SDKにビデオテクスチャをフィードする方法を示します。</td>
</tr><tr>
<td>TestRenderVideoFrame.java</td>
<td>TRTCCloudのオリジナルのレンダリングロジックをスキップして、自身でOpenGLを使用して画面をレンダリングする方法を示します。</td>
</tr><tr>
<td>VideoFrameReader.java</td>
<td>ローカルのビデオファイルから、1フレームずつ画面を読み取ります。</td>
</tr><tr>
<td>decoderフォルダ</td>
<td>デコードモジュール|</td>
</tr><tr>
<td>openglフォルダ</td>
<td>OpenGLの基本関数をカプセル化し、より使いやすくしています。</td>
</tr><tr>
<td>renderフォルダ</td>
<td>Eglの基本関数をカプセル化し、より使いやすくしています。</td></tr>
</tbody></table>

>! CPU使用率が過度に高くなるのを避けるため、640 x 360以上の解像度に対して、textureを使用することを推奨します。


#### サンプルコード
`TestSendCustomVideoData.java`のコード原理はより複雑です。
1. コードはまずGLThreadスレッドを開始します。このスレッドは、関連する「サーフェース（SurfaceTexture）」にコンテンツが描画されるまで、ほとんどの場合、待機状態にあります。
2. コードは次にローカルビデオファイルからフレームごとにビデオ画面を読み取り、前述の手順で作成した「サーフェース」上にフレームごとに画面を描画するためのMovieVideoFrameReaderと呼ばれるモジュールを使用します。
3. フレームが描画されるたびに、手順1で作成したGLThreadスレッドがウェイクアップされ、次の`onTextureProcess`コールバックがあり、このコールバック関数で取得したtextureがsendCustomVideoData関数を介してSDKに渡されます。

```java
public int onTextureProcess(int textureId, EGLContext eglContext) {
        if (!mIsSending) return textureId;

        //テクスチャ方式を介してビデオフレームをSDKに入力します
        TRTCCloudDef.TRTCVideoFrame videoFrame = new TRTCCloudDef.TRTCVideoFrame();
        videoFrame.texture = new TRTCCloudDef.TRTCTexture();
        videoFrame.texture.textureId = textureId;
        videoFrame.texture.eglContext14 = eglContext;
        videoFrame.width = mPlayThread.getVideoWidth();
        videoFrame.height = mPlayThread.getVideoHeight();
        videoFrame.pixelFormat = TRTCCloudDef.TRTC_VIDEO_PIXEL_FORMAT_Texture_2D;
        videoFrame.bufferType = TRTCCloudDef.TRTC_VIDEO_BUFFER_TYPE_TEXTURE;
        mTRTCCloud.sendCustomVideoData(videoFrame);
        return textureId;
    }
```
:::
::: Windows\sプラットフォーム
Windowsプラットフォームでは、TRTCVideoPixelFormat_I420のみをサポートしています。次のパラメータ形式を推奨します。
<table>
<thead><tr><th>パラメータ名</th><th>パラメータタイプ</th><th>推奨値</th><th>付注</th>
</tr></thead><tbody>
<tr>
  <td>videoFormat</td>
  <td>TRTCVideoPixelFormat</td>
  <td>TRTCVideoPixelFormat_I420</td>
  <td>TRTCVideoPixelFormat_I420のみサポートしています。</td>
</tr><tr>
  <td>bufferType</td>
  <td>TRTCVideoBufferType</td>
  <td>TRTCVideoBufferType_Buffer</td>
  <td>TRTCVideoBufferType_Bufferのみサポートしています。</td>
</tr><tr>
  <td>textureId</td>
  <td>int</td>
  <td>入力不要</td>
  <td>Windowsプラットフォームはテクスチャをサポートしていません</td>
</tr><tr>
  <td>data</td>
  <td>char *</td>
  <td>ビデオフレームbuffer</td>
  <td>I420データフレーム。</td>
</tr><tr>
  <td>timestamp</td>
  <td>uint64_t</td>
  <td>0</td>
  <td>0を入力できます。この場合SDKがtimestampフィールドを自動入力します。ただしsendCustomVideoDataの呼び出し間隔が<strong>均等</strong>になるように制御してください。</td>
</tr><tr>
  <td>width</td>
  <td>uint64_t</td>
  <td>ビデオ画面の幅</td>
  <td>渡される画面のピクセル幅を正確に入力してください。</td>
</tr><tr>
  <td>height</td>
  <td>uint32_t</td>
  <td>ビデオ画面の高さ</td>
  <td>渡される画面のピクセル高さを正確に入力してください。</td>
</tr><tr>
  <td>rotation</td>
  <td>TRTCVideoRotation</td>
  <td>画面の回転角度</td>
  <td><li>デフォルトは未入力。 </li><li>画面を回転させたい場合は、<code>TRTCVideoRotation_0</code>、<code>TRTCVideoRotation_90</code>、<code>TRTCVideoRotation_180</code>、<code>TRTCVideoRotation_270</code>と入力します。SDKはその値に応じてビデオを対応する角度まで時計回りに回転させます。例えば、縦画面の場合、<code>TRTCVideoRotation_90</code>と入力すると、SDKが画面を回転させて横表示にします。</li></td>
</tr></tbody></table>

#### サンプルコード
[Demo](https://github.com/tencentyun/TRTCSDK/blob/master/Windows/DuilibDemo/sdkinterface/TRTCCloudCore.cpp)ファイルの中に`sendCustomVideoFrame` という関数があり、それによって、ローカルビデオファイルの中からI420形式のbufferを読み取り、SDKを介して後続の処理を実行する方法を示しています。

```C++
//TRTCVideoFrameをアセンブルし、trtcCloudオブジェクトに送信します
TRTCVideoFrame frame;
frame.videoFormat = LiteAVVideoPixelFormat_I420;
frame.length = bufferSize;
frame.data = _video_buffer;
frame.width = _video_width;
frame.height = _video_height;
m_pCloud->sendCustomVideoData(TRTCVideoStreamTypeBig, & frame);      
```
:::
</dx-tabs>





## ビデオレンダリングのカスタマイズ

TRTC SDKは、OpenGLを使用してビデオ画面のレンダリングを行います。ゲーム開発に使用する場合、または自身のインターフェースエンジンにTRTC SDKを埋め込む場合は、自身でビデオ画面をレンダリングする必要があります。

<dx-tabs>
::: iOS\sプラットフォーム（\sMacを含む）
TRTCCloudの`setLocalVideoRenderDelegate`と`setRemoteVideoRenderDelegate`を介してローカルとリモート画面のカスタムレンダリングのコールバックを設定します。関連パラメータは次のとおりです。

|  パラメータ名   |       パラメータタイプ       |            推奨値             |                付注                |
| :---------: | :------------------: | :-----------------------------: | :------------------------------------: |
| pixelFormat | TRTCVideoPixelFormat |    TRTCVideoPixelFormat_NV12    |                   -                    |
| bufferType  | TRTCVideoBufferType  | TRTCVideoBufferType_PixelBuffer | iOSでネイティブにサポートされているビデオフレーム形式。最も高いパフォーマンスを発揮します。 |

[](id:example_ios)
#### サンプルコード
pixelFormatがTRTCVideoPixelFormat_NV12を選択し、bufferTypeがTRTCVideoBufferType_PixelBufferを選択する場合は、NV12形式のPixelBufferをビデオイメージに簡単に変換することができます。Demoフォルダに`TestRenderVideoFrame.m` と呼ばれるファイルがあり、その中に次のサンプルコードを使用したこの方法の使用法が示されています。

```objectiveC
- (void)onRenderVideoFrame:(TRTCVideoFrame *)frame 
                                userId:(NSString *)userId 
						        streamType:(TRTCVideoStreamType)streamType
{
    //userIdがnilの場合はローカル画面、nilでない場合はリモート画面です
    CFRetain(frame.pixelBuffer);
    __weak __typeof(self) weakSelf = self;
    dispatch_async(dispatch_get_main_queue(), ^{
        TestRenderVideoFrame* strongSelf = weakSelf;
        UIImageView* videoView = nil;
        if (userId) {
            videoView = [strongSelf.userVideoViews objectForKey:userId];
        }
        else {
            videoView = strongSelf.localVideoView;
        }
        videoView.image = [UIImage imageWithCIImage:[CIImage imageWithCVImageBuffer:frame.pixelBuffer]];
        videoView.contentMode = UIViewContentModeScaleAspectFit;
        CFRelease(frame.pixelBuffer);
    });
}
```
:::
::: Android\sプラットフォーム
TRTCCloudの`setLocalVideoRenderListener`と`setRemoteVideoRenderListener`を介してローカルとリモート画面のカスタムレンダリングのコールバックを設定します。関連パラメータは次のとおりです。

|  パラメータ名   |       パラメータタイプ       |                           推奨値                           |                           付注                           |
| :---------: | :------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| pixelFormat | TRTCVideoPixelFormat |                 TRTC_VIDEO_PIXEL_FORMAT_NV21                 |             カスタムレンダリングは現在textureスキームをサポートしていません。              |
| bufferType  | TRTCVideoBufferType  | TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY または<br> TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER | BYTE_BUFFERはjniレイヤーでの使用に適し、BYTE_ARRAYはJavaレイヤーでの直接的な操作に使用できます。 |

[](id:example_android)
#### サンプルコード
<dx-codeblock>
::: Android java
    public void onRenderVideoFrame(String userId, int streamType, final TRTCCloudDef.TRTCVideoFrame frame) {
        if (!userId.equals(mUserId) || mSteamType != streamType) {
            // レンダリングコールバックのidまたはsteamtypeが正しくない場合
            return;
        }
        if (frame.texture != null) {
            // frame.textureのテクスチャ描画が終了するまで待機します
            GLES20.glFinish();
        }
        Size mSurfaceSize; //ここでSurfaceの幅と高さを設定します
        GpuImageI420Filter mYUVFilter;
        GLES20.glViewport(0, 0, mSurfaceSize.width, mSurfaceSize.height);
        GLES20.glBindFramebuffer(GLES20.GL_FRAMEBUFFER, 0);
        GLES20.glClearColor(0, 0, 0, 1.0f);
        GLES20.glClear(GLES20.GL_DEPTH_BUFFER_BIT | GLES20.GL_COLOR_BUFFER_BIT);
        if (frame.data != null) {
            mYUVFilter.loadYuvDataToTexture(frame.data, frame.width, frame.height);
        } else {
            mYUVFilter.loadYuvDataToTexture(frame.buffer, frame.width, frame.height);
        }         
        mYUVFilter.onDraw(NO_TEXTURE, mGLCubeBuffer, mGLTextureBuffer);
        
    }
:::
</dx-codeblock>
:::
::: Windows\sプラットフォーム
TRTCCloudのsetLocalVideoRenderCallbackおよびsetRemoteVideoRenderCallbackを介してローカルとリモート画面のカスタムレンダリングコールバックを設定します。関連パラメータは次のとおりです。

|  パラメータ名   |         パラメータタイプ          |          推奨値           |                           付注                           |
| :---------: | :-----------------------: | :-------------------------: | :----------------------------------------------------------: |
| pixelFormat |   TRTCVideoPixelFormat    | TRTCVideoPixelFormat_BGRA32 | TRTCVideoPixelFormat_I420またはTRTCVideoPixelFormat_BGRA32ピクセル形式のビデオフレームのコールバックをサポートしています。 |
| bufferType  |    TRTCVideoBufferType    | TRTCVideoBufferType_Buffer  |           現在はTRTCVideoBufferType_Bufferのみサポートしています。            |
|  callback   | ITRTCVideoRenderCallback* |  ITRTCVideoRenderCallback*  |                       カスタムレンダリングコールバック。                       |

[](id:example_windows)
#### サンプルコード
pixelFormatにTRTCVideoPixelFormat_BGRA32を選択し、bufferTypeに TRTCVideoBufferType_Bufferを選択した場合は、非常に簡単に、BGRA32形式のPixelBufferをビデオ画面に変換できます。Demoの中に`TXLiveAvVideoView.cpp`というファイルがあり、その中に次のサンプルコードを使用したこの方法の使用法が示されています。

<dx-codeblock>
::: Window c++
void TXLiveAvVideoView::renderFitMode(HDC hDC, unsigned char * buffer, int width, int height, RECT& rcImage)
{
    Point origin;
    origin.X = m_rcItem.left, origin.Y = m_rcItem.top;
    int viewWith = m_rcItem.right - m_rcItem.left;
    int viewHeight = m_rcItem.bottom - m_rcItem.top;

    bool bReDrawBg = false;
    
    if (m_bmi.bmiHeader.biWidth != width || m_bmi.bmiHeader.biHeight != height)
    {
        memset(&m_bmi, 0, sizeof(m_bmi));
        m_bmi.bmiHeader.biSize = sizeof(BITMAPINFOHEADER);
        m_bmi.bmiHeader.biWidth = width;
        m_bmi.bmiHeader.biHeight = height;
        m_bmi.bmiHeader.biPlanes = 1;
        m_bmi.bmiHeader.biBitCount = 32;
        m_bmi.bmiHeader.biCompression = BI_RGB;
        bReDrawBg = true;
    }
    //レンダリング処理の開始
    ::SetStretchBltMode(hDC, COLORONCOLOR);
    if (bReDrawBg)
        ::PatBlt(hDC, 0 + origin.X, 0 + origin.Y, viewWith, viewHeight, BLACKNESS);
    ::StretchDIBits(hDC, x + origin.X, y + origin.Y, width, height, 0, 0, width, height, m_argbRenderFrame.frameBuf, &m_bmi, DIB_RGB_COLORS, SRCCOPY);
}
:::
</dx-codeblock>
:::
</dx-tabs>

## オーディオキャプチャのカスタマイズ

TRTCCloudの`enableCustomAudioCapture`インターフェースを介してTRTC SDKデフォルトのサウンドキャプチャプロセスをオフにする必要があります。その後、`sendCustomAudioData`インターフェースを使用してTRTC SDKに自身の声音データを入力することができます。

`sendCustomAudioData`インターフェースに1フレームが20msの長さのオーディオデータを表す`TRTCAudioFrame`と呼ばれるパラメータがあります。

-  `sendCustomAudioData` を介してSDKに送信されるデータは 、AACや他の圧縮形式ではなく、PCMフォーマットの非圧縮オーディオ生データでなければなりません。
- sampleRateとchannelsはそれぞれサウンドサンプルレートとサウンドチャンネル数を意味します。渡されるPCMデータと厳密に一致させてください。
- フレームごとのオーディオデータの推奨時間は20msであり、次のように計算することができます。sampleRateが48000、サウンドチャンネルが1（シングルサウンドチャンネル）である場合、sendCustomAudioDataの各呼び出しで渡されるbufferの長さは：48000 * 0.02s * 1 * 16bit = 15360bit = 1920バイトでなければなりません。
- timestampは0にすることができます。timestampが0である場合、SDKはオーディオタイムスタンプを自動的に入力します。以上より、オーディオタイムスタンプの安定性を確保するため、`sendCustomAudioData`を**均等**に呼び出し、20msに1度の頻度を確保してください。そうしなければ、声音が途切れるという結果を招くおそれがあります。

>! `sendCustomAudioData`を使用すると、エコーキャンセル（AEC）の機能が無効になる場合があります。

## オーディオ生データの取得

音声モジュールは非常に複雑で、SDKは音声デバイスのキャプチャおよび再生ロジックを厳密に制御する必要があります。一部シーンにおいて、リモートユーザーのオーディオデータまたはローカルマイクによってキャプチャされたオーディオデータを取得する必要がある場合は、TRTCCloudに対応する異なるプラットフォームのインターフェースを介して、3つのコールバック関数をSDKに統合できます。

<dx-alert infotype="explain" title="TRTCCloudの対応するプラットフォームごとのインターフェースはそれぞれ以下となります。">
<ul style="margin:0"><li/><b>iOS：</b>setAudioFrameDelegate。
<li/><b>Android：</b>setAudioFrameListener。
<li/><b>Windows：</b>setAudioFrameCallback。
</ul>
</dx-alert>

| インターフェース                  | 説明                                                         |
| --------------------- | ------------------------------------------------------------ |
| onCapturedAudioFrame  | ローカルマイクでキャプチャしたオーディオ生データを取得します。ユーザー定義キャプチャモードでないときは、SDKがマイクの音声のキャプチャを担当しますが、SDKがキャプチャしたオーディオ生データを取得したい場合には、このコールバック関数を介して取得することができます。 |
| onPlayAudioFrame      | この関数は各リモートユーザーのミキシング前の声音データをコールバックします。特定のチャネルの音声に対して音声認識を行いたい場合は、このコールバックを使用することができます。 |
| onMixedPlayAudioFrame | 各チャネルのオーディオデータをミキシングした後、再生のためにスピーカーに送信される前に、この関数を介してコールバックされます。 |

>!
- 上記のコールバック関数の中で何らかの時間のかかる操作を行わないでください。直接コピーし、別のスレッドで処理することを推奨しますが、そうしない場合、音声の途切れまたはエコーキャンセル（AEC）の無効化などの問題が生じる恐れがあります。
- 上記のコールバック関数の中でコールバックされるデータは読み取りとコピーのみが許され、修正することはできません。修正すると様々な不確定な影響が生じる恐れがあります。





