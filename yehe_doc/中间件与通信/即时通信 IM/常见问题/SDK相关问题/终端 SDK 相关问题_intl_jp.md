3. ### TUIKitソースコードはAndroidxに対応していますか。
   TUIKitの最新ソースコードはすでにAndroidxに対応しています。

   ### ログインにエラー6012が発生しましたか、またはTLSSDK exchange ticket fail。

   - 初期化インターフェースとログインインターフェースは、連続的に呼び出すことはできなく（初期化メソッドに非同期操作があるため）別々に呼び出す必要があります。
   - 現在IM体験版を使用している場合、Professional Editionにアップグレードする必要があります。アップグレード後は正常にログインできます。SDKAppIDをコンソールで構成することができます。価格の詳細については、[製品価格](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

   ### SDK未初期化エラーの6013が発生しましたが、どうしますか。

   SDK未初期化エラー6013が発生した場合、次の方法でトラブルシューティングすることができます。
   1. ログインにせずにメッセージの送受信などの他の操作を行っていないかどうかを確認します。
   2. ログイン中に他の端末によって強制オフラインさせられたかどうかを確認します。IM SDKはデフォルトで1つのアカウントが1つの端末にしかログインできません。処理方法については、[多端末同時ログイン](https://intl.cloud.tencent.com/document/product/1047/33518)ドキュメントをご参照ください。
   3. Androidの場合、ライブラリファイルがすべて読み込まれていないか、使用中にシステムによってリサイクルされたりしていないかどうかに注意してください。

   ### コード：6205 desc: QALSERVICE not ready？

   初期化後に`stopQALService`が呼び出されると、このエラーが発生します。お客様が共有している[構成方法](https://blog.csdn.net/qq_16131393/article/details/54895733)をご参照ください。

   ### 絵文字を送信すると、メッセージリストが空か、それとも文字化けしていますが、どうしますか。

   IMは絵文字を提供していません。具体的な解析には自分でアライメントする必要があります。
   絵文字は次の2つの使用方法があります。
   - 1つはTIMFaceElemのindexを使って絵文字のインデックスを識別します。例えばAndroidとiOSの両端末に同じ絵文字画像があり、インデックス2またはindex=2は笑顔を意味し、両端末の送受信に同じインデックス絵文字画像が表示されればよい。
   - もう1つはTIMFaceElemのdataを使用します。例えば絵文字画像は文字列で命名され、smileは笑顔を意味し、dataにsmileを保存することができ、iOSとAndroidの両端末でdataからkeyとして適切な絵文字画像を見つけて表示することができます。

   また、両方のフィールドを共に使用することもできます。例えば、dataはどの絵文字シリーズを表し、indexはその絵文字シリーズのどのインデックスを表すなど、QQのようなさまざまな絵文字効果を実現することができます。多端末解析ルールが一致すれば、dataにより複雑なデータ構造を保存することもできます。

   

   ### 操作時にエラーコード10002が返されることがありますが、どうしますか。

   サービス側の認証を必要とする操作時には、ネットワーク異常、タイムアウトまたはチケット切り替えに失敗した場合、このステータスコードが返されます。このステータスコードが検出された場合、後で再試行すればよい。

   ### メッセージの送受信中にエラーコード6200または6201を受信しましたが、どうしますか。

   このステータスコードが返された場合、クライアントがネットワークオフライン、タイムアウトまたはアクセス可能なネットワークなしである可能性があります。6200は、リクエスト時にネットワークがないと定義され、6201は、レスポンス時にネットワークがないと定義されています。このステータスコードが検出された場合、ネットワークを確認するか、ネットワーク回復を待ってから再試行してください。

   ### メッセージの送受信時にエラーコード20003が返されましたが、どうしますか。

   ユーザアカウント（UserID）がTencent Cloudにインポートされているかどうかをチェックしてください。UserIDが無効な場合、またはUserIDがTencent IMにインポートされていない場合には、このエラーコードが返されます。

   ### 音声メッセージの再生時にエラーコード6010が返されましたが、どうしますか。

   通常、音声メッセージがローミングデータの保存期間を過ぎて、リクエストに失敗した場合に発生します。[ローミングメッセージの時間を延長](https://intl.cloud.tencent.com/document/product/1047/34419)または音声ファイルをローカルに保存して再生を実行することができます（期限切れのファイルは復元できません）。ただし、履歴メッセージの保存時間の延長をサポートするメッセージタイプは、SDKのバージョンによって異なります。詳細については、[メッセージの保存](https://intl.cloud.tencent.com/document/product/1047/33524)をご参照ください。

   ### アカウント認証時にエラーコード70001または70003または70009または70013が返されましたが、どうしますか。

   これらのステータスコードは、UserIDとUserSigが一致しないときに発生します。UserIDとUserSigの有効性を確認してください。ここで、70001はUserSigの有効期限が切れたこと、70003はUserSigが切断されて検証に失敗したこと、70009はUserSigパブリックキー検証の不一致、70013はUserIDの不一致と定義されています。

   ### Web側でIM SDKを使用するとエラーコード-2または-5が返されましたが、どうしますか。

   - \-2：Web側がサーバーにリクエストを送信するときの失敗の原因は通常、ネットワークの不具合です。Web側はHTTP Long Pollingを使用してサービス側にリクエストを送信して、ネットワークに不具合がある場合、このステータスコードが返されます。この場合、ネットワークを確認するか、再試行してください。
   - \-5：ログイン操作が完了せず、SDKがサーバーから返されたa2keyとtinyIDを受信していないまま、他のインターフェースを直接呼び出すと、「tinyidまたはa2が空です」というエラーメッセージとエラーコード-5が表示されます。

   ### armeabiプラットフォームでSDKから「java.lang.UnsatisfiedLinkError: No implementation found for」エラーが表示された場合、どのすればいいですか。
   imsdkのaarのjni/armeabi-v7a/libImSDK.soをソースコードプロジェクトのsrc/main/jniLibs/armeabiディレクトリにコピーし、build.gradleで読み込めばよいです。

   ### App Storeにリリースする時に、x86_64、i386アーキテクチャーエラーが発生しましたが、どう解決しますか。
   この不具合は、App Storeがx86_64、i386アーキテクチャをサポートしていないためです。具体的な解決策は次のとおりです。
   1. プロジェクトのコンパイルキャッシュをクリアします。
    **Product**>**clean**を選択し、Altキーを押してclean build Folder...になり、操作が完了するまで待ちます。
   2. App Storeでサポートされていないx86_64とi386アーキテクチャを次のように削除します。
    a. **TARGETS**>**Build Phases**を選択します。
     b. プラス記号をクリックし、**New Run Script Phase**を選択します。
     c. 次のコードを追加します。

   ```
   APP_PATH="${TARGET_BUILD_DIR}/${WRAPPER_NAME}"  
   
   # This script loops through the frameworks embedded in the application and  
   
   # removes unused architectures.  
   
    find "$APP_PATH" -name '*.framework' -type d | while read -r FRAMEWORK  
    do  
    FRAMEWORK_EXECUTABLE_NAME=$(defaults read "$FRAMEWORK/Info.plist" CFBundleExecutable)  
    FRAMEWORK_EXECUTABLE_PATH="$FRAMEWORK/$FRAMEWORK_EXECUTABLE_NAME"  
    echo "Executable is $FRAMEWORK_EXECUTABLE_PATH"  
   
    EXTRACTED_ARCHS=()  
   
    for ARCH in $ARCHS  
    do  
    echo "Extracting $ARCH from $FRAMEWORK_EXECUTABLE_NAME"  
    lipo -extract "$ARCH" "$FRAMEWORK_EXECUTABLE_PATH" -o "$FRAMEWORK_EXECUTABLE_PATH-$ARCH"  
    EXTRACTED_ARCHS+=("$FRAMEWORK_EXECUTABLE_PATH-$ARCH")  
    done  
   
    echo "Merging extracted architectures: ${ARCHS}"  
    lipo -o "$FRAMEWORK_EXECUTABLE_PATH-merged" -create "${EXTRACTED_ARCHS[@]}"  
    rm "${EXTRACTED_ARCHS[@]}"  
   
    echo "Replacing original executable with thinned version"  
    rm "$FRAMEWORK_EXECUTABLE_PATH"  
    mv "$FRAMEWORK_EXECUTABLE_PATH-merged" "$FRAMEWORK_EXECUTABLE_PATH"  
   
    done
   ```

    ![](https://main.qcloudimg.com/raw/f343cb4d7674d58623dfa0097d2c6484.png)

   3. 再び圧縮してアップロードします。
