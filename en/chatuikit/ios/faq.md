> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

### Does TUIKit source code support Androidx?

Yes.

### Why do I encounter a 6012 error or "TLSSDK exchange ticket fail" upon login?
- The initialization API and the login API must be called separately and cannot be called successively because there are asynchronous operations in the initialization method.

- If you are using Chat Free edition and upgrade to Chat Pro Edition, after the upgrade, you can configure your SDKAppID in the console to ensure proper login. For pricing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).


### Why do I encounter a 6013 "SDK Not Initialized" error?

If the 6013 "SDK Not Initialized" error occurs, try the following troubleshooting methods:
1. Check whether you performed other operations such as receiving and sending messages before logging in successfully.

2. Check whether you were forced offline when logging in by an account already logged in on another device. By default, the Chat SDK allows one account to log in on one device at a time. For more information, see [Multi-Device Login](https://intl.cloud.tencent.com/document/product/1047/33518).

3. For Android, verify that all library files have been loaded or repossessed by the system during use.


### Why do I encounter "code: 6205 desc: QALSERVICE not ready" error?

This error is caused by calling `stopQALService` after initialization. To fix it, refer to the [configuration method](https://blog.csdn.net/qq_16131393/article/details/54895733) shared by one of our customers.

### Why do not emojis appear or appear as gibberish in messages?

Chat does not provide emoji packs. You must align the actual parsing by yourself.

There are two ways to use emojis:
- Use index in TIMFaceElem to identify the index of the emojis. For example, an Android device and an iOS device have the same set of emojis and index 2 represents the smile emoji. When index=2, both devices send and receive the same indexed emoji.

- Use data in TIMFaceElem. For example, the names of emoji images are string-type. Use the word "smile" to represent the smile emoji, and store "smile" in data. Then, both iOS and Android devices use data as the key to retrieve and display the corresponding emoji.


   You can also use the two fields at the same time. For example, use data to specify the emoji set and index to indicate the specific index in this emoji set. This way, you can implement many different emoji effects as in QQ. It is possible to store more complex data structures in data as long as the devices follow the same parsing rules.


### Why do I encounter error 10002 during operations?

This status code is returned when a network exception, timeout, or ticket switching failure occurs during server-side authentication. If you see this status code, wait a moment and try again.

### Why do I encounter error 6200 or 6201 when receiving or sending messages?

This status code is returned when the client is offline, times out, or is disconnected. Error 6200 is defined as no network connection during request sending, whereas error 6201 is defined as no network connection during response sending. When you encounter this status code, check the network condition or wait for the network to restore and try again.

### Why do I encounter error 20003 when receiving and sending messages?

This error code is returned when UserID is invalid or UserID has not been imported to Chat. To fix it, check whether UserID has been imported to Tencent Cloud.

### Why do I encounter error 6010 when playing audio messages?

This error code is returned when audio messages that are no longer retained by the roaming server are requested. To fix it, you can [increase the message roaming duration](https://intl.cloud.tencent.com/document/product/1047/34419) or download audio files to local storage and play them. However, expired files cannot be restored. Different SDK versions allow you to increase the retention duration for different message types. For more information, see [Message Storage](https://intl.cloud.tencent.com/document/product/1047/33524).

### Why do I encounter errors 70001, 70003, 70009, and 70013 during account authentication?

These errors occur because UserID and UserSig do not match. To fix it, check the validity of UserID and UserSig. Among them, error 70001 means UserSig has expired, error 70003 means a verification failure due to a truncated UserSig, error 70009 means UserSig verification failed (possibly due to mixing the keys or private keys of other SDKAppIDs when generating UserSig), and error 70013 means UserID does not match.

### Why do I encounter the error code -2 or -5 when the web client app is using the Chat SDK?
- -2: Indicates that a web app request to the server failed, usually due to network problems. Web apps send requests to the server by using the HTTP Long Polling method, and this status code is returned when a network problem occurs. To fix it, check your network or try again.

- -5: When the login attempt is not completed and the SDK has not received the a2key and tinyID returned by the server, directly calling other APIs returns the "tinyid or a2 is empty" error message and -5 error code.


### What should I do when the SDK on the armeabi platform reports "java.lang.UnsatisfiedLinkError: No implementation found for"?

Copy jni/armeabi-v7a/libImSDK.so in the Chat SDK’s aar file to the src/main/jniLibs/armeabi directory in your source code project and load it in build.gradle.

### How can I resolve x86_64 and i386 architecture errors when the app has been launched in App Store?

This error occurs because App Store does not support the x86_64 and i386 architecture. The solution is as follows:
1. Clear the project compilation cache:
 Select **Product** > **clean**, press Alt until "clean build Folder..." appears and wait for the operation to complete.

2. Remove the x86_64 and i386 architecture not supported by App Store:
 a. Select **TARGETS** > **Build Phases**.
 b. Click the plus sign and select **New Run Script Phase**.
 c. Add the following code:

   ``` bash
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
   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100031390357/ac95ba51e28011eeb1eb525400b5f95f.png)

3. Package the app and upload it again.


### Can developers directly utilize the emoticon packs demonstrated in the Chat various client demos/TUIKit projects?

To respect the copyright of emoji designs, the Chat Demo/TUIKit project does not include cutouts of large emoji elements. Please replace them with your own designs or other emoji packs for which you hold the copyright before officially launching for commercial use. **The default smiley face emoji pack shown below is copyrighted by Tencent RTC** and is available for licensed use for a fee. If you need to obtain a license, please [contact us](https://trtc.io/contact).

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027202808/a44543c197f611ef820f525400d5f8ef.png)