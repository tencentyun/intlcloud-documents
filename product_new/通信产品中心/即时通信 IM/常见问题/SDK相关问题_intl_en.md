### Does TUIKit source code support Androidx?
No, TUIKit source code does not support Androidx currently.

### Why do I encounter error 6012 or the "TLSSDK exchange ticket fail" message upon login?

- The initialization API and the login API must be called separately and cannot be called continuously (because asynchronous operations exist in the initialization method).
- If you are using IM Trial Edition, you must upgrade to IM Pro Edition for intended login. You can configure your SDKAppID on your console. For more information on pricing, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

### Why do I encounter error 6013 stating that the SDK has not been initialized?

If error 6013 occurs, try the following troubleshooting options:
1. Check whether you have performed other operations such as receiving and sending messages before logging in successfully.
2. Check whether you have been forced offline on another device. By default, the IM SDK allows one account to log in on a single device. For information on how to handle this situation, see [Multi-Device Login](https://intl.cloud.tencent.com/document/product/1047/33518#.E5.A4.9A.E7.AB.AF.E7.99.BB.E5.BD.95).
3. For Android, verify that all library files have been loaded or repossessed by the system during use.

### Why do I encounter error 6205 stating that "QALSERVICE not ready"?

This error is caused by calling `stopQALService` after initialization. To correct it, refer to the [configuration method](https://blog.csdn.net/qq_16131393/article/details/54895733) shared by one of our customers.

### Why do not emojis appear or they appear as gibberish in messages?

IM does not provide any emoji packs. You must troubleshoot based on the actual use case.
There are two ways to use emojis:
- Use the index parameter in TIMFaceElem to identify the indexes of the emojis. For example, an Android device and an iOS device share the same set of emojis, and index 2 represents the smiley emoji. When index=2, both devices send and receive the same indexed emoji.
- Use the data parameter in TIMFaceElem. For example, the names of emoji images are of the string type. Use the word "smile" to represent the smiley emoji, and store "smile" in the data parameter. Then, both iOS and Android devices use data as the key to locate and display the corresponding emoji.

You can also use the preceding two fields at the same time. For example, use data to specify the emoji set and index to indicate the specific index in this emoji set to achieve various emoji effects. It is possible to store more complex data structures in data as long as the devices follow the same parsing rules.

### Why does logging in to the iLive SDK sometimes return error 6015?

Subsequent `login` operations return this error code before the initial `login` operation is called back. We recommend that you call the initialization API during app initialization and the login API during login.

### Why do I occasionally encounter error 10002 during operations?

This status code is returned when a network exception, timeout, or ticket switching failure occurs during a server-side authentication operation. If you encounter this error code, try again later.

### Why do I encounter error 6200 or 6201 when receiving or sending messages?

This error code is returned when the client is offline, times out, or has no network connection. Error code 6200 is defined as no network connection during request sending, whereas error code 6201 is defined as no network connection during response sending. If you encounter this error code, check the network condition or wait for the network to restore and then try again.

### Why do I encounter error 116001 when receiving and sending short videos with IM SDK v3.x?

This error occurs when the VOD service has not been activated. To troubleshoot, do as follows:
1. Check the status of the UGSV service in the IM console and verify that it has been activated.
2. To store short videos for more than 7 days, additionally check that the VOD service has been activated in the VOD console.

### Why do I encounter error 20003 when receiving and sending messages?

This error code is returned when UserID is invalid or UserID has not been imported to IM. To correct it, check whether UserID has been imported to Tencent Cloud.

### Why do I encounter error 6010 when playing audio messages?

This error code is returned when you request audio messages that are no longer available on the roaming server. To correct it, [increase the message roaming period](https://intl.cloud.tencent.com/document/product/1047/34419#.E5.8E.86.E5.8F.B2.E6.B6.88.E6.81.AF.E5.AD.98.E5.82.A8.E6.97.B6.E9.95.BF.E9.85.8D.E7.BD.AE) or download audio files to local storage and play them locally (expired files cannot be restored.) Different SDK versions allow you to increase the storage period for different message types. For more information, see [Message Storage](https://intl.cloud.tencent.com/document/product/1047/33524#MsgType).

### What do the returned error codes 70001, 70003, 70009, and 70013 mean during account authentication?

These errors occur because UserID and UserSig do not match. To correct them, check whether UserID and UserSig are valid. Error code 70001 indicates that UserSig has expired, 70003 indicates a verification failure due to the truncated UserSig, 70009 indicates that UserSig failed public key verification, and 70013 indicates a UserID mismatch.

### Why do error codes -2 or -5 appear when the web app is using the IM SDK?

- \For error code -2: it indicates that a web app request to the server failed, which normally results from network problems. The web app sends requests to the server by using the HTTP Long Polling method, and this error code is returned when a network problem occurs. To correct it, check the network condition or try again.
- \For error code -5: when the login operation is not completed and the SDK has not received the a2key and tinyID returned by the server, directly calling other APIs returns the "tinyid or a2 is empty" error message and error code -5.

### How can I solve x86_64 and i386 architecture errors when the app has been launched in App Store?
This error occurs because App Store does not support the x86_64 and i386 architectures. To correct it, do as follows:
1. Clear the project compilation cache:
 Choose **Product** > **clean**, press Alt until "clean build Folder..." appears, and wait for the operation to finish.
2. Remove the x86_64 and i386 architectures that are not supported by App Store:
 a. Choose **TARGETS** > **Build Phases**.
 b. Click the plus sign and choose **New Run Script Phase**.
 c. Add the following code:

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

3. Package and upload again.
