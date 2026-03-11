> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本文将介绍如何快速接入 TUICallKit 组件。您可以在 10 分钟内完成以下关键步骤，最终获得一个功能完备的音视频通话界面。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182394/6dcf7117b60011f0a808525400bf7822.png)


## 准备工作

### 环境要求

Flutter 3.24.0、Dart 3.5.0 及以上版本。

### 开通服务

在使用腾讯云提供的音视频服务前，您需要前往控制台，为应用开通音视频服务。具体步骤详细参见 [开通服务](https://write.woa.com/document/139743928960860160)。开通服务后，请记录`SDKAppID` 和`SDKSecretKey`，在后续的步骤（[登录](https://write.woa.com/#8495693e-91ce-41ac-92ee-728b33a7714b)）中会用到。

## 快速接入

### 步骤1：导入插件

在工程的根目录下，通过命令行执行以下命令安装 [tencent_calls_uikit](https://pub.dev/packages/tencent_calls_uikit) 插件。
``` bash
flutter pub add tencent_calls_uikit
```

### 步骤2：工程配置
- 原生工程配置：


   

【Android】
1. 由于 SDK 内部使用了 Java 反射机制（或特性），需要将部分 SDK 类加入不进行混淆处理的名单。

  - 请在工程的`android/app/build.gradle` 文件中配置并开启混淆规则：

``` java
  android {
    ......
    buildTypes {  
        release {  
            ......
            isMinifyEnabled = true  
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'  
        } 
    }
}
```
  - 在工程的 `android/app` 目录下创建 `proguard-rules.pro` 文件，并在其中添加如下代码：

``` java
-keep class com.tencent.** { *; }
```
2. 在工程的 `android/app/build.gradle `文件中配置开启 Multidex 支持。

``` java
  android {  
    ......
    defaultConfig {
      ......
      multiDexEnabled true
    } 
}
```

【iOS】

因为 TUICallKit 需要使用音视频功能，您必须获取麦克风和摄像头的授权。

授权操作方法：在您的 iOS 工程的 `Info.plist` 文件中，在顶级 `<dict>` 元素下添加以下两项。
``` java
<key>NSCameraUsageDescription</key>
<string>CallingApp需要访问您的相机权限，开启后录制的视频才会有画面</string>
<key>NSMicrophoneUsageDescription</key>
<string>CallingApp需要访问您的麦克风权限，开启后录制的视频才会有声音</string>
```

- Flutter 工程配置


   在 Flutter 应用框架的 navigatorObservers 中添加 TUICallKit.navigatorObserver，以下是使用 MaterialApp 框架的示例代码：

   ``` java
   import 'package:tencent_calls_uikit/tencent_calls_uikit.dart';
   
    ......
   
   class XXX extends StatelessWidget {
     const XXX({super.key});
   
    @override
     Widget build(BuildContext context) {
       return MaterialApp(
         navigatorObservers: [TUICallKit.navigatorObserver],
         ......
       );
     }
   }
   ```

### 步骤3：登录

在您的项目中添加如下代码，调用 `login` 接口完成插件的登录。此步骤至关重要：只有成功登录后，您才能正常使用 TUICallKit 提供的各项功能。


``` java
import 'package:tencent_calls_uikit/tencent_calls_uikit.dart';
import 'package:tencent_calls_uikit/debug/generate_test_user_sig.dart';
......

final String userId    = 'xxxxx';  // 请替换为您的 UserId
final int    sdkAppId  = 0;        // 请替换为第一步在控制台得到的 SDKAppID
final String secretKey = 'xxxx';   // 请替换为第一步在控制台得到的 SecretKey

void login() async {
    String userSig  = GenerateTestUserSig.genTestSig(userID, sdkAppID, secretKey);
    CompletionHandler result = await TUICallKit.instance.login(sdkAppID, userID, userSig);
    if (result.errorCode == 0) {
      print('Login success');
    } else {
      print('Login failed: ${result.errorCode} ${result.errorMessage}');
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

<td rowspan="1" colSpan="1" >客户根据自己的业务自定义用户 ID，只允许包含大小写英文字母(a-z A-Z)、数字(0-9)及下划线和连词符。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sdkAppId</td>

<td rowspan="1" colSpan="1" >int</td>

<td rowspan="1" colSpan="1" >在 [实时音视频 TRTC 控制台](https://console.cloud.tencent.com/trtc) 创建的音视频应用的唯一标识。</td>
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
> - **开发环境**：如果您在本地开发调试阶段，可以采用本地 `GenerateTestUserSig.genTestSig`函数生成 userSig。该方法中 secretKey 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量。
> - **生产环境**：如果您的项目要发布上线，请采用 [服务端生成 UserSig](https://write.woa.com/document/86735811695435776) 的方式。


### 步骤4：设置昵称和头像 [可选]

首次登录的用户没有头像和昵称信息，您可以通过 [setSelfInfo](https://write.woa.com/document/94733520019521536) 接口设置头像和昵称：






【Flutter（Dart）】
``` swift
import 'package:tencent_calls_uikit/tencent_calls_uikit.dart';

void _setSelfInfo() {
    String nickname = "jack"
    String avatar = "https:/****/user_avatar.png"
    CompletionHandler result = TUICallKit.instance.setSelfInfo(nickname, avatar);
}
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
</table>


### 步骤5：发起通话

拨打方可以通过调用 `calls` 函数，并指定媒体类型和被叫方用户 ID 列表，来发起语音或视频通话。`calls` 接口同时支持一对一通话和多人通话。当 userIdList 中包含一个 userId 时，为一对一通话；当 userIdList 包含多个 userId 时，则为多人通话。


``` java
import 'package:tencent_calls_uikit/tencent_calls_uikit.dart';
......

void _call() {
    List<String> participantIds = ['vince'];
    CallMediaType mediaType = CallMediaType.audio;
    CallParams callParams = CallParams();    
    TUICallKit.instance.calls(participantIds, mediaType, callParams);
}
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

<td rowspan="1" colSpan="1" >CallMediaType</td>

<td rowspan="1" colSpan="1" >通话的媒体类型，例如视频通话、语音通话。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >CallParams</td>

<td rowspan="1" colSpan="1" >通话扩展参数，例如房间号、通话邀请超时时间等。</td>
</tr>
</table>


### 步骤6：接听通话

接听端完成登录后，拨打端发起通话，接收端就可以收到通话邀请，同时伴随铃声和振动。

## 更多功能

### 开启悬浮窗功能

您可以通过调用 [enableFloatWindow](https://write.woa.com/document/94733520019521536) 开启/关闭悬浮窗功能，在初始化 TUICallKit 组件时启用该功能，默认状态为关闭（false）。可通过点击通话界面左上角的悬浮窗按钮，将通话界面缩小为悬浮窗形式。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182394/f303e819b62311f0a6c652540044a08e.png)



``` java
import 'package:tencent_calls_uikit/tencent_calls_uikit.dart';
......

void _enableFloatWindow() {
    TUICallKit.instance.enableFloatWindow(true);
}
```

**详情：**默认为 false，通话界面左上角的悬浮窗按钮隐藏，设置为 true 后显示。

### 开启来电横幅

您可以通过调用 `enableIncomingBanner` 开启/关闭来电横幅显示，该功能默认为关闭状态（false）。当被叫端收到来电时，默认展示全屏通话等待界面。启用此功能后，将首先显示一个横幅通知，然后根据需要切换到全屏通话界面。请注意，显示来电横幅需要授予悬浮窗权限，具体的显示策略将根据权限设置及应用当前是否在前台或后台运行来决定。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182394/5fd105fdb62d11f0a808525400bf7822.png)



``` java
import 'package:tencent_calls_uikit/tencent_calls_uikit.dart';
......

void _enableFloatWindow() {
    TUICallKit.instance.enableIncomingBanner(true);
}
```

**详情：**默认为 false，被叫端收到邀请后默认弹出全屏通话等待界面。开启后先展示一个横幅，然后根据需要拉起全屏通话界面。

### 多人通话

主叫方使用 `calls` 方法发起通话时，若被叫用户列表超过一人，则自动视为群组通话。其他成员可通过 `join` 方法加入该多人通话。

**发起多人通话：**使用 `calls` 方法发起通话时，若被叫用户列表（`userIdList`）超过一人，则自动视为群组通话。


``` java

import 'package:tencent_calls_uikit/tencent_calls_uikit.dart';
......

void _call() {
    List<String> participantIds = ['vince','mike'];
    CallMediaType mediaType = CallMediaType.audio;
    CallParams callParams = CallParams();    
    TUICallKit.instance.calls(participantIds, mediaType, callParams);
}
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

<td rowspan="1" colSpan="1" >CallMediaType</td>

<td rowspan="1" colSpan="1" >通话的媒体类型，例如视频通话、语音通话。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >params</td>

<td rowspan="1" colSpan="1" >CallParams</td>

<td rowspan="1" colSpan="1" >通话扩展参数，例如房间号、通话邀请超时时间，离线推送自定义内容等。</td>
</tr>
</table>


**加入多人通话：**可使用 `join` 方法加入指定的群组通话。


``` java
import 'package:tencent_calls_uikit/tencent_calls_uikit.dart';

void join() {
    String callId = "123456";
    TUICallKit.instance.join(callId);
}
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
</table>


### 语言设置
- **支持的语言：**目前支持**简体中文、英文和日文，**默认语言为**英文 。**

- **切换语言：**TUICallKit 不提供单独的语言切换接口。其界面语言将自动跟随当前应用程序根组件（如 MaterialApp 或 CupertinoApp）所使用的语言设置而切换。 您只需更改应用根组件的语言配置即可实现通话界面的语言切换。
   

   > **说明：**
   > 

   > 如需设置其他语言，请[联系我们](https://cloud.tencent.com/document/product/647/19906)获取协助。
   > 


### 铃声设置

您可通过以下方式设置默认铃声、来电静音模式：
- **设置默认铃声：**如果您通过源码依赖 TUICallKit 组件，您可以替换铃声资源文件（[发起呼叫时的铃音](https://github.com/Tencent-RTC/TUICallKit/blob/main/Flutter/assets/audios/phone_dialing.mp3)、[接到呼叫时的铃音](https://github.com/Tencent-RTC/TUICallKit/blob/main/Flutter/assets/audios/phone_ringing.mp3)）设置默认铃声。

- **来电静音模式：**您可以通过 [enableMuteMode](https://write.woa.com/document/94733520019521536) 设置静音模式。


   
``` java
import 'package:tencent_calls_uikit/tencent_calls_uikit.dart';
......

void _setCallingBell() {
    TUICallKit.instance.enableMuteMode(true);
}
```

**详情：**开启后，收到通话请求，不会播放来电铃声。


## 自定义您的 UI 

### 替换图标按钮

您可以直接替换 [assets/images](https://github.com/Tencent-RTC/TUICallKit/tree/main/Flutter/assets/images) 文件夹下的图标，以确保整个 App 中的图标色调风格保持一致。以下列出了基本的功能按钮，您可以替换对应的图标以适配自己的业务场景。







常用图标文件名列表
<table>
<tr>
<td rowspan="1" colSpan="1" >图标</td>

<td rowspan="1" colSpan="1" >文件名称</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182394/87b3fd48b63411f0b4c35254001c06ec.png)</td>

<td rowspan="1" colSpan="1" >dialing.png</td>

<td rowspan="1" colSpan="1" >接听来电图标</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182394/87bc58a9b63411f0a808525400bf7822.png)</td>

<td rowspan="1" colSpan="1" >hangup.png</td>

<td rowspan="1" colSpan="1" >挂断通话图标</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182394/87b50a49b63411f0b9945254005ef0f7.png)</td>

<td rowspan="1" colSpan="1" >mute_on.png</td>

<td rowspan="1" colSpan="1" >关闭麦克风图标</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182394/87b948a1b63411f0a808525400bf7822.png)</td>

<td rowspan="1" colSpan="1" >handsfree.png</td>

<td rowspan="1" colSpan="1" >关闭扬声器图标</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182394/87b904d4b63411f0a808525400bf7822.png)</td>

<td rowspan="1" colSpan="1" >camera_off.png</td>

<td rowspan="1" colSpan="1" >关闭摄像头图标</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027182394/87ae00adb63411f0b0cf525400e889b2.png)</td>

<td rowspan="1" colSpan="1" >add_user.png</td>

<td rowspan="1" colSpan="1" >通话过程中邀请用户图标</td>
</tr>
</table>


## 常见问题

如果您在接入和使用中遇到问题，请参见 [常见问题](https://write.woa.com/document/98788861869330432)。

## 交流与反馈

如果您在使用过程中，有任何意见或建议，请[联系我们](https://cloud.tencent.com/document/product/647/19906)。