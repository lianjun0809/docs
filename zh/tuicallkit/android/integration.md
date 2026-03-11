> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本文将介绍如何快速接入 TUICallKit 组件。您可以在 10 分钟内完成以下关键步骤，最终获得一个功能完备的音视频通话界面。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032357901/fc89fc8aafd711f0943c5254007c27c5.png)


## 准备工作

### **环境要求**
- **Android 版本要求**：Android 5.0（SDK API Level 21）及以上版本。

- **Gradle 版本要求：**Gradle 4.2.1 及以上的版本。

- **设备需满足**：Android 5.0 及以上的手机设备。


### **开通服务**

在使用腾讯云提供的音视频服务前，您需要前往控制台，为应用开通音视频服务。具体步骤参见 [开通服务](https://write.woa.com/document/139743928960860160)。开通服务后，请记录`SDKAppID` 和`SDKSecretKey`，在后续的步骤（[登录](https://write.woa.com/#step4)）中会用到。

## 快速接入

### 步骤1：导入组件

在 [GitHub](https://github.com/Tencent-RTC/TUIKit_Android) 中克隆或下载代码，然后将 `TUIKit_Android` 目录下的 `atomic_x` 和 `call` 目录下的 `tuicallkit-kt` 子目录复制到您当前工程的 app 同级目录中，如下图所示。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032357901/c1c072c9f02c11f0bfd65254001d6acc.png)


### 步骤2：工程配置
1. 在工程根目录下找到`settings.gradle.kts`（或 `settings.gradle )`文件，增加如下代码，导入`tuicallkit-kt`、`atomic_x` 组件到项目中。


   


【setting.gradle.kts】
``` java
include(":tuicallkit-kt")
include(":atomic_x")
```


【settings.gradle】
``` java
include ':tuicallkit-kt'
include ':atomic_x'
```

2. 在 app 目录下找到 `build.gradle.kts(或build.gradle)` 文件，在`dependencies` 中增加如下代码，声明当前 app 对组件的依赖。


   


【build.gradle.kts】
``` java
dependencies {
    api(project(":tuicallkit-kt"))
}
```


【build.gradle】
``` java
dependencies {
    api project(':tuicallkit-kt')
}
```
   

   > **说明：**
   > 

   > TUICallKit 工程内部已经默认依赖：`TRTC SDK`、`IM SDK`、`tuicallengine` 以及公共库 `tuicore`，不需要开发者单独配置。如需进行版本升级，则修改`tuicallkit-kt/build.gradle`文件中的版本号即可。
   > 

3. 由于 SDK 内部使用了 Java 反射特性，需要将部分类加入不混淆名单。请在 app 目录下的 `proguard-rules.pro` 文件末尾添加如下代码。添加完后，点击右上角的 **Sync Now**，同步代码。

   ``` java
   -keep class com.tencent.** { *; }
   ```
4. 在 app 目录下找到`AndroidManifest.xml` 文件，在 application 节点中添加 `tools:replace="android:allowBackup"`，覆盖组件内的设置，使用自己的设置。

   ``` java
     // app/src/main/AndroidManifest.xml
      <application
       android:name=".BaseApplication"
       android:allowBackup="false"
       android:icon="@drawable/app_ic_launcher"
       android:label="@string/app_name"
       android:largeHeap="true"
       android:theme="@style/AppTheme"
       tools:replace="android:allowBackup">
   ```   

   > **说明：**
   > 

   > 如果您集成 tuicallkit-kt 后报如下错误：
   > 
   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032357901/650a5745eb9611f0bfd65254001d6acc.png)


   > 原因是 AGP 8.0+ 要求 Gradle 运行时使用 Java 17 或更高版本。您可以在 Android Studio 中点击 Tools -> SDK Manager -> Build, Execution,Deployment -> Build Tools -> Gradle 配置 Gradle JDK 版本为 17 解决该问题
   > 
   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032357901/75d5fcddeb9711f09965525400370dda.png)



### 步骤3：登录

在您的项目中添加如下代码，调用 `login` 方法实现 TUI 组件的登录。这一步骤至关重要，只有在成功登录之后，您才能正常使用 TUICallKit 提供的各项功能。






【Android（Kotlin）】
``` java
import com.tencent.qcloud.tuicore.TUILogin
import com.tencent.qcloud.tuicore.interfaces.TUICallback
import com.tencent.qcloud.tuikit.tuicallkit.debug.GenerateTestUserSig

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        
        val userId = "denny"         // 请替换为您的UserId
        val sdkAppId = 0             // 请替换为在控制台得到的SDKAppID
        val secretKey = "****"       // 请替换为在控制台得到的SecretKey
        val userSig = GenerateTestUserSig.genTestUserSig(userId, sdkAppId, secretKey) 
        TUILogin.login(this, sdkAppId, userId, userSig, object : TUICallback() {
            override fun onSuccess() {
            }
            override fun onError(errorCode: Int, errorMessage: String) {
            }
         }) 
    }
}
```


【Android（Java）】
``` java
import com.tencent.qcloud.tuicore.TUILogin;
import com.tencent.qcloud.tuicore.interfaces.TUICallback;
import com.tencent.qcloud.tuikit.tuicallkit.debug.GenerateTestUserSig;

public class MainActivity extends AppCompatActivity {
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        
        String userId = "denny";     // 请替换为您的UserId
        int sdkAppId = 0;            // 请替换为第一步在控制台得到的SDKAppID
        String secretKey = "****";   // 请替换为第一步在控制台得到的SecretKey
        String userSig = GenerateTestUserSig.genTestUserSig(userId, sdkAppId, secretKey);
        TUILogin.login(this, sdkAppId, userId, userSig, new TUICallback() {
            @Override
            public void onSuccess() {
            }
            
            @Override
            public void onError(int errorCode, String errorMessage) {
            }
        });
    }
}

```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userId</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >只允许包含大小写英文字母(a-z A-Z)、数字(0-9)及下划线和连词符。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sdkAppId</td>

<td rowspan="1" colSpan="1" >int</td>

<td rowspan="1" colSpan="1" >在 [实时音视频 TRTC 控制台](https://console.cloud.tencent.com/trtc) 创建的音视频应用的唯一标识 SDKAppID。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >secretKey</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >在 [实时音视频 TRTC 控制台](https://console.cloud.tencent.com/trtc) 创建的音视频应用的 SDKSecretKey。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userSig</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >一种安全保护签名，用于对用户进行登录鉴权认证，确认用户是否真实，阻止恶意攻击者盗用您的云服务使用权。</td>
</tr>
</table>


> **说明：**
> 
> - **开发环境**：如果您在本地开发调试阶段，可以采用本地 [GenerateTestUserSig.genTestUserSig](https://github.com/Tencent-RTC/TUIKit_Android/blob/main/application/debug/src/main/java/com/tencent/qcloud/tuikit/debug/GenerateTestUserSig.java) 函数生成 userSig。该方法中 secretKey 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量。
> - **生产环境**：如果您的项目要发布上线，请采用 [服务端生成 UserSig](https://write.woa.com/document/86735811695435776) 的方式。


### 步骤4：设置昵称和头像[可选]

首次登录的用户没有头像和昵称信息，您可以通过 `setSelfInfo` 接口设置头像和昵称：






【Android（Kotlin）】
``` java
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit

val name = "mike" // 目标用户的昵称。
val avatar = "https:/****/user_avatar.png" // 目标用户的头像。
TUICallKit.createInstance(applicationContext).setSelfInfo(name, avatar, 
    object : CompletionHandler {
         override fun onSuccess() {
             // 设置成功
         }
         override fun onFailure(code: Int, desc: String) {
             // 设置失败
         }
     })
```


【Android（Java）】
``` java
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit;

String name = "mike"; // 目标用户的昵称。
String avatar = "https:/****/user_avatar.png"; // 目标用户的头像。
TUICallKit.createInstance(applicationContext).setSelfInfo(name, avatar, 
    new CompletionHandler() {
        @Override
        public void onSuccess() {
            // 设置成功
        }

        @Override
        public void onFailure(int code, String desc) {
            // 设置失败
        }
    });
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >nickname</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >目标用户的昵称。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >avatar</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >目标用户的头像。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >completion</td>

<td rowspan="1" colSpan="1" >CompletionHandler</td>

<td rowspan="1" colSpan="1" >异步操作的结果回调。</td>
</tr>
</table>


### 步骤5：发起通话

拨打方可以通过调用 `calls` 函数，并指定通话类型和被叫方的 userID，来发起语音或视频通话。`calls` 接口同时支持一对一通话和多人通话。当 userIDList 中包含一个 userID 时，为一对一通话；当 userIDList 包含多个 userID 时，则为多人通话。






【Kotlin】
``` java
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit
import io.trtc.tuikit.atomicxcore.api.call.CallMediaType
import io.trtc.tuikit.atomicxcore.api.call.CallParams

val userIdList = mutableListOf<String>()
userIdList.add("mike")
val mediaType = CallMediaType.Audio
val callParams = CallParams()
TUICallKit.createInstance(context).calls(userIdList, mediaType, params, object : CompletionHandler {
    override fun onFailure(code: Int, desc: String) {
       // 失败回调
    }
    override fun onSuccess() {
       // 成功回调
    }
})
```


【Java】
``` java
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit;
import io.trtc.tuikit.atomicxcore.api.call.CallMediaType;
import io.trtc.tuikit.atomicxcore.api.call.CallParams;

List<String> userIdList = new ArrayList<>();
userIdList.add("mike");
CallMediaType mediaType = CallMediaType.Audio;
CallParams params = new CallParams();
TUICallKit.createInstance(this).calls(userIdList, mediaType, params, new CompletionHandler() {
    @Override
    public void onFailure(int code, String desc) {
        // 失败回调
    }
    @Override
    public void onSuccess() {
        // 成功回调
    }
});

```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userIdList</td>

<td rowspan="1" colSpan="1" >List<String></td>

<td rowspan="1" colSpan="1" >目标用户的 userId 列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mediaType</td>

<td rowspan="1" colSpan="1" >[CallMediaType](https://liteav.sdk.cloudcachetci.com/doc/product/tuikit/atomic-x/android/zh/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.call/-call-media-type/index.html)</td>

<td rowspan="1" colSpan="1" >通话的媒体类型，例如视频通话、语音通话。<br>- Audio : 语音通话。<br>- Video : 视频通话。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >[CallParams](https://liteav.sdk.cloudcachetci.com/doc/product/tuikit/atomic-x/android/zh/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.call/-call-params/index.html)</td>

<td rowspan="1" colSpan="1" >通话扩展参数，例如房间号、通话邀请超时时间等。<br>- roomId : 此次通话的房间 ID。<br>- timeout : 发起通话等待的最长时间，超过该时间通话结束。<br>- userData : 发起通话时自定义扩展字段。<br>- chatGroupId : 与 chat 结合使用，Chat 群组的群 ID 。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >completion</td>

<td rowspan="1" colSpan="1" >CompletionHandler</td>

<td rowspan="1" colSpan="1" >异步操作的结果回调。</td>
</tr>
</table>


### 步骤6：接听通话

接听端完成登录后，拨打端发起通话，接收端就可以收到通话邀请，同时伴随铃声和振动。

## 更多功能

### AI 转录与翻译

您可以通过调用 `enableAITranscriber` 开启/关闭 AI 转录与翻译功能。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027194436/29fb5e7a00f411f198e252540097cba1.png)


> **注意：**
> 
> 1. 该功能默认为开启状态（enable = true）。如需关闭，请在发起通话前调用 `enableAITranscriber`(enable: false)。
> 2. AI 实时转录与翻译为增值服务。体验版赠送免费额度，可直接体验。如需开通正式版，请在 [实时音视频控制台](https://console.cloud.tencent.com/trtc) 开通套餐包，详见 [计费说明](https://cloud.tencent.com/document/product/647/111976)。







【Kotlin】
``` swift
TUICallKit.createInstance(context).enableAITranscriber(true)
```


【Java】
``` objectivec
TUICallKit.createInstance(context).enableAITranscriber(true);
```

**详情：**默认为 true，通话界面上显示 AI 翻译相关页面，设置为 false 后关闭。

### 开启悬浮窗功能

您可以通过调用 `enableFloatWindow` 开启/关闭悬浮窗功能，在初始化 TUICallKit 组件时启用该功能，默认状态为关闭（false）。可通过点击通话界面左上角的悬浮窗按钮，将通话界面缩小为悬浮窗形式。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032357901/1f41fc38b00011f0a6a2525400e889b2.png)







【Kotlin】
``` java
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit

TUICallKit.createInstance(this).enableFloatWindow(true)
```


【Java】
``` java
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit;

TUICallKit.createInstance(this).enableFloatWindow(true);
```

**详情：**默认为 false，通话界面左上角的悬浮窗按钮隐藏，设置为 true 后显示。

### 开启来电横幅

您可以通过调用 `enableIncomingBanner` 开启/关闭来电横幅显示，该功能默认为关闭状态（false）。当被叫端收到来电时，默认展示全屏通话等待界面。启用此功能后，将首先显示一个横幅通知，然后根据需要切换到全屏通话界面。请注意，显示来电横幅需要授予悬浮窗权限，具体的显示策略将根据权限设置及应用当前是否在前台或后台运行来决定，具体策略可参考：[被叫端来电显示策略](https://write.woa.com/document/86735803114926080)。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032357901/b8f92a1cafff11f0995e525400454e06.png)







【Android（Kotlin）】
``` java
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit

TUICallKit.createInstance(context).enableIncomingBanner(true)
```


【Android（Java）】
``` java
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit;

TUICallKit.createInstance(context).enableIncomingBanner(true);
```

**详情：**默认为 false，被叫端收到邀请后默认弹出全屏通话等待界面。开启后先展示一个横幅，然后根据需要拉起全屏通话界面。

### 实现多人通话

主叫方使用 `calls` 方法发起通话时，若被叫用户列表超过一人，则自动视为群组通话。其他成员可通过 `join` 方法加入该多人通话。
- **发起多人通话：**使用 `calls` 方法发起通话时，若被叫用户列表（`userIdList`）超过一人，则自动视为群组通话。


   




【Kotlin】
``` java
import com.tencent.cloud.tuikit.engine.call.TUICallDefine
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit
import io.trtc.tuikit.atomicxcore.api.call.CallMediaType
import io.trtc.tuikit.atomicxcore.api.call.CallParams

val userIdList = mutableListOf<String>()
userIdList.add("mike")
userIdList.add("tate")
val mediaType = CallMediaType.Audio
val params = CallParams()
TUICallKit.createInstance(context).calls(userIdList, mediaType, params, object : CompletionHandler {
    override fun onFailure(code: Int, desc: String) {
       // 失败回调
    }
    override fun onSuccess() {
       // 成功回调
    }
})
```


【Java】
``` java
import com.tencent.cloud.tuikit.engine.call.TUICallDefine;
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit;
import io.trtc.tuikit.atomicxcore.api.call.CallMediaType;
import io.trtc.tuikit.atomicxcore.api.call.CallParams;

List<String> userIdList = new ArrayList<>();
userIdList.add("mike");
userIdList.add("tate");
CallMediaType mediaType = CallMediaType.Audio;
CallParams params = new CallParams();
TUICallKit.createInstance(context).calls(userIdList, mediaType, params, new CompletionHandler() {
    @Override
    public void onFailure(int code, String desc) {
        // 失败回调
    }

    @Override
    public void onSuccess() {
        // 成功回调
    }
});
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >userIdList</td>

<td rowspan="1" colSpan="1" >List<String></td>

<td rowspan="1" colSpan="1" >目标用户的 userId 列表。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >mediaType</td>

<td rowspan="1" colSpan="1" >[CallMediaType](https://liteav.sdk.cloudcachetci.com/doc/product/tuikit/atomic-x/android/zh/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.call/-call-media-type/index.html)</td>

<td rowspan="1" colSpan="1" >通话的媒体类型，例如视频通话、语音通话。<br>- Audio : 语音通话。<br>- Video : 视频通话。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >[CallParams](https://liteav.sdk.cloudcachetci.com/doc/product/tuikit/atomic-x/android/zh/-atomic-x%20-core%20-a-p-i/io.trtc.tuikit.atomicxcore.api.call/-call-params/index.html)</td>

<td rowspan="1" colSpan="1" >通话扩展参数，例如房间号、通话邀请超时时间等。<br>- roomId : 此次通话的房间 ID。<br>- timeout : 发起通话等待的最长时间，超过该时间通话结束。<br>- userData : 发起通话时自定义扩展字段。<br>- chatGroupId : 与 chat 结合使用，Chat 群组的群 ID 。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >completion</td>

<td rowspan="1" colSpan="1" >CompletionHandler</td>

<td rowspan="1" colSpan="1" >异步操作的结果回调。</td>
</tr>
</table>


- **加入多人通话：**可使用 `join` 方法加入指定的群组通话。


   




【Kotlin】
``` java
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit

val callId = "123456" // 此次通话的 ID
TUICallKit.createInstance(this).join(callId, object : CompletionHandler {
    override fun onFailure(code: Int, desc: String) {
      // 失败回调
    }
    override fun onSuccess() {
      // 成功回调
    }
})
```


【Java】
``` java
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit;

String callId = "123456"; // 此次通话的 ID
TUICallKit.createInstance(this).join(callId, new CompletionHandler() {
    @Override
    public void onFailure(int code, String desc) {
        // 失败回调
    }

    @Override
    public void onSuccess() {
        // 成功回调
    }
});
```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >callId</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >此次通话的唯一标识。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >completion</td>

<td rowspan="1" colSpan="1" >CompletionHandler</td>

<td rowspan="1" colSpan="1" >异步操作的结果回调。</td>
</tr>
</table>



### 设置语言
- **支持的语言：**目前支持**简体中文、繁体中文、英文、日文和阿拉伯语。**

- **切换语言：**TUICallKit 默认语言与手机系统保持一致 。如果需要切换语言，可以使用 `TUIThemeManager.getInstance().changeLanguage `方法设置语言，以设置语言为英文的示例代码如下**。**


   




【Kotlin】
``` java
import com.tencent.qcloud.tuicore.TUIThemeManager;

public class MainActivity extends BaseActivity {
    @Override
  public void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState)
      
      val language = TUIThemeManager.LANGUAGE_ZH_CN // 设置的语言
      TUIThemeManager.getInstance().changeLanguage(applicationContext, language)
    }
}
```


【Java】
``` java

import com.tencent.qcloud.tuicore.TUIThemeManager;

public class MainActivity extends BaseActivity {
    @Override
  public void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      String language = TUIThemeManager.LANGUAGE_EN; // 设置的语言
      TUIThemeManager.getInstance().changeLanguage(getApplicationContext(), language);
    }
}

```
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >language</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >设置的语言：<br>- TUIThemeManager.LANGUAGE_EN：英文。<br>- TUIThemeManager.LANGUAGE_AR：阿拉伯语。<br>- TUIThemeManager.LANGUAGE_ZH_HK：中文繁体。<br>- TUIThemeManager.LANGUAGE_ZH_CN：中文简体。</td>
</tr>
</table>


> **说明：**
> 

> 如需设置其他语言，请[联系我们](https://cloud.tencent.com/document/product/647/19906)获取协助。
> 



### 设置铃声

您可通过以下方式设置默认铃声、来电静音模式、离线推送铃声：
- **设置默认铃声（方式1）：**如果您通过源码依赖 TUICallKit 组件，您可以替换铃声资源文件（[发起呼叫时的铃声](https://github.com/Tencent-RTC/TUIKit_Android/blob/main/call/tuicallkit-kt/src/main/res/raw/phone_dialing.mp3)、[接到呼叫时的铃声](https://github.com/Tencent-RTC/TUIKit_Android/blob/main/call/tuicallkit-kt/src/main/res/raw/phone_ringing.mp3)）设置默认铃声。

- **设置默认铃声（方式2）：**通过 [setCallingBell](https://cloud.tencent.com/document/product/647/78750#setCallingBell) 接口设置被叫端收到的来电铃声。


   




【Android（Kotlin）】
``` java
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit

val filePath = "***/callingBell.mp3"
TUICallKit.createInstance(context).setCallingBell(filePath)
```


【Android（Java）】
``` java
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit;

String filePath = "***/callingBell.mp3";
TUICallKit.createInstance(context).setCallingBell(filePath);
```

**详情：**这里仅限传入本地文件地址，需要确保该文件目录是应用可以访问的。铃声设置后与设备绑定，更换用户，铃声依旧会生效。如需恢复默认铃声，filePath传空即可。
<table>
<tr>
<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >filePath</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >铃声文件的路径。</td>
</tr>
</table>


- **来电静音模式：**您可以通过 [enableMuteMode](https://cloud.tencent.com/document/product/647/78750#enableMuteMode) 设置静音模式。


   




【Android（Kotlin）】
``` java
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit

TUICallKit.createInstance(context).enableMuteMode(true)
```


【Android（Java）】
``` java
import com.tencent.qcloud.tuikit.tuicallkit.TUICallKit;

TUICallKit.createInstance(context).enableMuteMode(true);
```

**详情：**开启后，收到通话请求，不会播放来电铃声。

- **自定义离线推送铃声**：离线推送默认铃声是由系统决定的，可以在 手机设置 中，进入应用详情，查看或更改应用的通知铃声。


## 自定义您的 UI

### 替换图标按钮

您可以直接替换 [res\drawable-xxhdpi](https://github.com/Tencent-RTC/TUIKit_Android/tree/main/atomic_x/src/main/res-callview/drawable-xxhdpi) 文件夹下的图标，以确保整个 App 中的图标色调风格保持一致。以下列出了基本的功能按钮，您可以替换对应的图标以适配自己的业务场景。







常用图标文件名列表
<table>
<tr>
<td rowspan="1" colSpan="1" >图标</td>

<td rowspan="1" colSpan="1" >文件名称</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032357901/ee93f5f6af1311f0b5345254005ef0f7.png)</td>

<td rowspan="1" colSpan="1" >callview_ic_dialing.png</td>

<td rowspan="1" colSpan="1" >接听来电图标</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032357901/eeb7bf23af1311f09710525400e889b2.png)</td>

<td rowspan="1" colSpan="1" >callview_ic_hangup.png</td>

<td rowspan="1" colSpan="1" >挂断通话图标</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032357901/eeb279f7af1311f09710525400e889b2.png)</td>

<td rowspan="1" colSpan="1" >callview_ic_mic_unmute.png</td>

<td rowspan="1" colSpan="1" >关闭麦克风图标</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032357901/eec4442baf1311f0b08552540044a08e.png)</td>

<td rowspan="1" colSpan="1" >callview_ic_handsfree_disable.png</td>

<td rowspan="1" colSpan="1" >关闭扬声器图标</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032357901/ee8f4bb6af1311f096c2525400454e06.png)</td>

<td rowspan="1" colSpan="1" >callview_ic_camera_disable.png</td>

<td rowspan="1" colSpan="1" >关闭摄像头图标</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100032357901/ee8ff7beaf1311f0a0a052540099c741.png)</td>

<td rowspan="1" colSpan="1" >callview_ic_add_user_black.png</td>

<td rowspan="1" colSpan="1" >通话过程中邀请用户图标</td>
</tr>
</table>


## 常见问题

如果您在接入和使用中遇到问题，请参见 [常见问题](https://write.woa.com/document/86735803114926080)。

## 交流与反馈

如果您在使用过程中，有什么建议或者意见，可以 [联系我们](https://cloud.tencent.com/document/product/647/19906)，感谢您的反馈。
