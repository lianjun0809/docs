> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

TUIKit Compose 是基于腾讯云 IM SDK 的一套 Jetpack Compose 组件库，提供了聊天、会话列表、联系人管理等即时通信功能的完整解决方案。本文介绍如何手动集成该组件并实现核心功能。

## 关键概念

TUIKit Compose 提供了一套完整的即时通信 UI 组件，向下依赖 AtomicXCore 数据层，向上可构建各种功能性 Page。
- Page 层：基于 TUIKit Compose 组件封装的完整功能页面：ChatPage、ContactsPage、ConversationsPage，您可以直接使用。

- TUIKit Compose（UI 组件层）：基于 AtomicXCore 构建的 Jetpack Compose 组件，您可将其嵌套到自己已有的 App 页面中。

- AtomicXCore（数据层）：提供数据管理和业务逻辑，包含各种 Store 和 Manager。


## 前提条件
- Android Studio Ladybug | 2024.2.1 及以上版本

- Android 5.0 及以上系统版本

- Gradle 8.9 及以上版本

- Android Gradle Plugin 8.6 及以上版本

- JDK 17 及以上版本

- Kotlin 1.9.0 及以上版本

- 一个有效的腾讯云账号及 Chat 应用。可参考 [开通服务](https://write.woa.com/document/107052220771086336) 从控制台获取以下信息：

  - SDKAppID：App 在控制台获取的 Chat 应用的 ID，为应用的唯一标识

  - SDKSecretKey：应用的密钥
      

      > **说明：**
      > 
>     - 本项目目前仅支持手动集成，暂不支持通过 Maven 等包管理器集成。
>     - 为确保构建环境稳定，请严格遵循官方兼容性要求进行配置：
>     - Gradle、Android Gradle Plugin、JDK 与 Android Studio 的兼容性，请参阅 Android 官方文档：[版本说明](https://developer.android.com/build/releases/gradle-plugin#updating-gradle)﻿。
>     - Kotlin、Android Gradle Plugin 与 Gradle 的版本对应关系，请参阅 Kotlin 官方文档：[Kotlin-Gradle 插件兼容性](https://kotlinlang.org/docs/gradle-configure-project.html#apply-the-plugin)。

      > 我们建议您根据上述指南，选择与项目要求完全匹配的版本组合。
      > 


## 集成并引入组件

### 下载源码
1. 从 GitHub 下载 [TUIKit Compose](https://github.com/Tencent-RTC/TUIKit_android_compose) 源码：

   ``` bash
   git clone https://github.com/Tencent-RTC/TUIKit_Android_Compose.git
   ```

   项目目录结构说明：

   ``` bash
   atomic-x/
   ├── src/main/
   │   ├── java/io/trtc/tuikit/atomicx/     # UI 组件源码（必需集成）
   │       ├── messagelist/      # 消息列表组件
   │       ├── messageinput/     # 消息输入组件
   │       ├── conversationlist/ # 会话列表组件
   │       ├── contactlist/      # 联系人列表组件
   │       ├── basecomponent/    # 基础组件
   │       └── ...               # 其他 UI 组件
   │   # 资源文件（必需集成）
   │   ├── res/                    # 公共资源
   │   ├── res-message-list/       # 消息列表组件资源
   │   ├── res-message-input/      # 消息输入组件资源
   │   ├── res-conversation-list/  # 会话列表组件资源
   │   └── ...                     # 其他组件资源
   chat/
   ├── uikit/src/main/java/io/trtc/tuikit/chat/pages    # Page 组件（参考实现）
   │   ├── ChatPage.kt
   │   ├── ContactsPage.kt
   │   └── ConversationsPage.kt
   └── demo/                 # 示例应用（可选参考）
   ```

### 集成组件
1. 将组件目录完整复制到您的 Android 项目中，如下图所示，其中 ComposeDemo 是示例项目，TUIKit_Android_Compose 是从 GitHub 上下载的组件源码：

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/b784e12db56a11f0b0cf525400e889b2.png)

2. 在您的 settings.gradle.kts/settings.gradle 文件中添加 TUIKit Compose 组件：
   

   > **说明：**
   > 

   > TUIKit_Android_Compose 可以放在任何位置，只要在 settings.gradle 中正确设置相对路径即可。
   > 


   


【Kotlin DSL (推荐)】
``` java
// settings.gradle.kts
include(":atomicx")
project(":atomicx").projectDir = file("../TUIKit_Android_Compose/atomic-x")
```


【Groovy DSL】
``` java
// settings.gradle
include ':atomicx'
project(':atomicx').projectDir = new File(settingsDir, '../TUIKit_Android_Compose/atomic-x')
```

3. 在 app 模块的 build.gradle.kts/build.gradle 中添加下列依赖：


   


【Kotlin DSL (推荐)】
``` java
// app/build.gradle.kts
dependencies {
    implementation(project(":atomicx"))
}
```


【Groovy DSL】
``` java
// app/build.gradle
dependencies {
    api project(':atomicx')
}
```
   

   > **注意：**
   > 
>   - 使用本地集成方案时，如需升级时需要从 GitHub 获取最新的组件代码，覆盖您本地项目的 TUIKit Compose 目录。
>   - 当私有化修改和远端有冲突时，需要手动合并，处理冲突。


### 配置项目
1. 在 app 目录下找到 AndroidManifest.xml 文件，在 `application` 节点中添加 `tools:replace="android:allowBackup"`，覆盖组件内的设置，使用自己的设置。

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
2. 配置依赖项。


   在您的项目工程的 gradle/libs.versions.toml 文件中添加如下依赖项：

   ``` python
   # gradle/libs.versions.toml
   [versions]
   agp = "8.13.0"
   kotlin = "2.0.21"
   coreKtx = "1.10.1"
   junit = "4.13.2"
   junitVersion = "1.1.5"
   espressoCore = "3.5.1"
   appcompat = "1.7.1"
   material = "1.13.0"
   runner = "1.0.2"
   espressoCoreVersion = "3.0.2"
   appcompatV7 = "28.0.0"
   
   tuicore = "8.6.7021"
   lifecycleRuntimeKtx = "2.8.7"
   ui = "1.8.0"
   foundation = "1.8.0"
   composeBom = "2024.09.00"
   activityCompose = "1.10.1"
   activity = "1.8.0"
   constraintlayout = "2.2.1"
   
   [libraries]
   androidx-core-ktx = { group = "androidx.core", name = "core-ktx", version.ref = "coreKtx" }
   junit = { group = "junit", name = "junit", version.ref = "junit" }
   androidx-junit = { group = "androidx.test.ext", name = "junit", version.ref = "junitVersion" }
   androidx-espresso-core = { group = "androidx.test.espresso", name = "espresso-core", version.ref = "espressoCore" }
   androidx-appcompat = { group = "androidx.appcompat", name = "appcompat", version.ref = "appcompat" }
   material = { group = "com.google.android.material", name = "material", version.ref = "material" }
   runner = { group = "com.android.support.test", name = "runner", version.ref = "runner" }
   espresso-core = { group = "com.android.support.test.espresso", name = "espresso-core", version.ref = "espressoCoreVersion" }
   appcompat-v7 = { group = "com.android.support", name = "appcompat-v7", version.ref = "appcompatV7" }
   
   androidx-lifecycle-viewmodel-compose = { module = "androidx.lifecycle:lifecycle-viewmodel-compose", version.ref = "lifecycleRuntimeKtx" }
   androidx-compose-bom = { group = "androidx.compose", name = "compose-bom", version.ref = "composeBom" }
   androidx-compose-foundation = { group = "androidx.compose.foundation", name = "foundation", version.ref = "foundation" }
   androidx-compose-ui = { group = "androidx.compose.ui", name = "ui", version.ref = "ui" }
   androidx-compose-ui-graphics = { group = "androidx.compose.ui", name = "ui-graphics" }
   androidx-ui-tooling = { group = "androidx.compose.ui", name = "ui-tooling" }
   androidx-compose-material3 = { group = "androidx.compose.material3", name = "material3" }
   androidx-activity-compose = { group = "androidx.activity", name = "activity-compose", version.ref = "activityCompose" }
   androidx-lifecycle-runtime-ktx = { group = "androidx.lifecycle", name = "lifecycle-runtime-ktx", version.ref = "lifecycleRuntimeKtx" }
   androidx-ui-tooling-preview = { group = "androidx.compose.ui", name = "ui-tooling-preview" }
   androidx-ui-test-manifest = { group = "androidx.compose.ui", name = "ui-test-manifest" }
   tuicore = { module = "com.tencent.liteav.tuikit:tuicore", version.ref = "tuicore" }
   com-tencent-mmkv = { group = "com.tencent", name = "mmkv", version = "1.3.14" }
   
   [plugins]
   android-application = { id = "com.android.application", version.ref = "agp" }
   kotlin-android = { id = "org.jetbrains.kotlin.android", version.ref = "kotlin" }
   android-library = { id = "com.android.library", version.ref = "agp" }
   
   kotlin-compose = { id = "org.jetbrains.kotlin.plugin.compose", version.ref = "kotlin" }
   ```
3. 开启 Compose 支持。


   在 app 模块的 build.gradle.kts/build.gradle 中添加下列配置：


   


【Kotlin DSL (推荐)】
``` java
// app/build.gradle.kts
plugins {
    // 添加 Compose 插件
    alias(libs.plugins.kotlin.compose)
}
android {
    // 开启 Compose 
    buildFeatures {
        compose = true
    }
}
```


【Groovy DSL】
``` java
// app/build.gradle
plugins {
    // 添加 Compose 插件
    id libs.plugins.kotlin.compose.get().pluginId
}
android {
    // 开启 Compose 
    buildFeatures {
        compose true
    }
}
```

4. 配置混淆规则。


   在您的 app/proguard-rules.pro 文件中添加以下混淆规则：

   ``` java
   -keep class com.tencent.** { *; }
   ```
5. Android Studio 中点击 **File > Sync Project with Gradle Files** 集成组件。


## 接入步骤

### 步骤1：配置用户鉴权

在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im/tool-usersig) 根据 UserID 获取 UserSig 用于后续登录时的用户鉴权。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/ee78464abee111f09a6b525400454e06.png)


### 步骤2：用户登录

登录鉴权后才能正常使用组件的功能。您可以调用 login 接口，传入上文获取的 SDKAPPID、userSig 用于登录鉴权:
``` swift
// 用户登录
LoginStore.shared.login(context, SDKAPPID, userID, userSig,
    object : CompletionHandler {
        override fun onSuccess() {
              // 登录成功，可跳转聊天或会话页
        }
        override fun onFailure(code: Int, desc: String) {
              // 登录失败，可弹框报错
        }
    })
```

> **注意：**
> 

> 在正式的生产环境中，建议在您的服务端生成 UserSig，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig 来进行鉴权。详见 [服务端生成 UserSig](https://cloud.tencent.com/document/product/269/32688)。
> 


### 步骤3： 构建会话列表界面

您可以基于 TUIKit Compose 中的 ConversationList 组件，构建一个会话列表页面。ConversationList 内建的功能是：
- 展示用户的会话列表，包含单聊和群聊会话

- 支持用户操作单个会话：置顶、删除、清空会话消息等


   您可以将 ConversationList 直接集成到现有的 App 页面中，也可以新构建一个完整的会话列表页，组装后的一种 UI 效果如下图所示：

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/29853c55b56711f0a5e052540099c741.png)


   将 ConversationList 封装为会话列表页，可参考 `chat/uikit/src/main/java/io/trtc/tuikit/chat/pages/ConversationsPage.kt` 文件里的实现，`ConversationsPage` 主要做了以下工作：

1. 在 ConversationList 上方添加了 headerView。

2. 传递点击会话列表 cell 事件。


   核心示例代码如下所示：

   ``` swift
   @Composable
   fun ConversationsPage(
       onConversationClick: (ConversationInfo) -> Unit = {},
       editContent: @Composable () -> Unit = {},
   ) {
       val colors = LocalTheme.current.colors
       Column(
           modifier = Modifier
               .fillMaxSize()
               .background(Colors.Transparent)
       ) {
   
           PageHeader(stringResource(R.string.chat_uikit_chat)) {
               editContent()
           }
   
           Box(modifier = Modifier.fillMaxSize(), contentAlignment = Alignment.Center) {
               ConversationList(modifier = Modifier.navigationBarsPadding(), onConversationClick = onConversationClick)
           }
       }
   }
   ```

### 步骤4：构建聊天界面

您可以基于 TUIKit Compose 中的 MessageList、MessageInput  组件，构建一个聊天页面。

MessageList 内建的功能是：
- 展示单聊或群聊消息列表。

- 支持对单条消息操作：查看图片消息大图、播放视频或语音消息、复制文本消息、撤回消息、删除消息等。


   MessageInput 内建的功能是：

- 支持用户组建并发送多种类型的消息：文本、表情、图片、语音、视频、文件等。


   您可以将 MessageList 和  MessageInput 直接集成到现有的 App 页面中，也可以新构建一个完整的聊天页，组装后的一种 UI 效果如下图所示：

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/4f5f8481b56711f0a6c652540044a08e.png)


   将 MessageList 和 MessageInput 组装为聊天页，可参考  `chat/uikit/src/main/java/io/trtc/tuikit/chat/pages/ChatPage.kt` 文件里的实现，`ChatPage` 主要做了以下工作：

1. 在最上方添加了 headerView，展示会话的名称。

2. 按照移动端用户使用习惯，上下拼接 MessageList 和 MessageInput。


   核心示例代码如下所示：

   ``` swift
   @Composable
   fun ChatPage(
       conversationID: String,
       locateMessage: MessageInfo? = null,
       onUserClick: (String) -> Unit,
       onChatHeaderClick: (String) -> Unit,
       onBackClick: () -> Unit,
   ) {
       ...
   
       val avatarUrl = conversationState.value?.avatarURL
       val displayName = conversationState.value?.title
       val colors = LocalTheme.current.colors
       Scaffold(
           modifier = Modifier
               .background(color = colors.bgColorOperate)
               .fillMaxSize()
               .wrapContentHeight(), topBar = {
               Box(
                   modifier = Modifier
                       .background(color = colors.bgColorOperate)
                       .fillMaxWidth()
                       .statusBarsPadding()
               ) {
                   ChatHeader(
                       avatarUrl = avatarUrl,
                       name = displayName ?: "",
                       onBackClick = onBackClick,
                       onAvatarClick = {
                           onChatHeaderClick(conversationID)
                       }
                   )
               }
           },
           bottomBar = {
               Box(
                   modifier = Modifier
                       .fillMaxWidth()
                       .background(color = colors.bgColorOperate)
               ) {
                   MessageInput(modifier = Modifier.navigationBarsPadding(), conversationID = conversationID)
               }
   
           }) { padding ->
           Box(
               modifier = Modifier
                   .padding(padding)
           ) {
               MessageList(conversationID = conversationID, locateMessage = locateMessage) {
                   onUserClick(it)
               }
           }
       }
   }
   ```

### 步骤5：构建联系人界面

您可以基于 TUIKit Compose 中的 ContactList 组件，构建一个联系人页面。ContactList 内建的功能是：
- 查看好友申请列表。

- 查看已加入的群列表。

- 处理群组邀请和申请。

- 管理黑名单列表。

- 查看好友。


   您可以将 ContactList 直接集成到现有的 App 中，也可以新构建一个完整的联系人列表页，组装后的一种 UI 效果如下图所示：

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/6810fe9db56711f09a6b525400454e06.png)


   将 ContactList 封装为联系人列表页，可参考 `chat/uikit/src/main/java/io/trtc/tuikit/chat/pages/ContactsPage.kt `文件里的实现，`ContactsPage` 主要做了以下工作：

1. 在 ContactList 上方添加了 headerView。

2. 传递点击联系人列表 cell 事件。


   核心示例代码如下所示：

   ``` swift
   @Composable
   fun ContactsPage(
       onContactClick: (ContactInfo) -> Unit = {},
       onGroupClick: (ContactInfo) -> Unit = {},
       editContent: @Composable () -> Unit = {},
   ) {
   
       val colors = LocalTheme.current.colors
       Column(
           modifier = Modifier
               .fillMaxSize()
               .background(Colors.Transparent)
       ) {
           PageHeader(stringResource(R.string.chat_uikit_contacts)) {
               editContent()
           }
   
           Box(
               modifier = Modifier
                   .fillMaxSize()
                   .navigationBarsPadding(), contentAlignment = Alignment.Center
           ) {
               ContactList(onGroupClick = onGroupClick, onContactClick = onContactClick)
           }
       }
   }
   ```

### 步骤6：完善界面间的跳转逻辑

ConversationsPage、ChatPage、ContactsPage 中暴露了一些用户点击事件，您可以自定义事件来实现页面间的交互：
<table>
<tr>
<td rowspan="1" colSpan="1" >Page</td>

<td rowspan="1" colSpan="1" >回调</td>

<td rowspan="1" colSpan="1" >建议跳转逻辑</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**ConversationsPage**</td>

<td rowspan="1" colSpan="1" >`onConversationClick: (ConversationInfo) -> Unit`</td>

<td rowspan="1" colSpan="1" >点击会话列表中的会话时触发，建议跳转到聊天页面（ChatPage）。</td>
</tr>

<tr>
<td rowspan="2" colSpan="1" >**ContactsPage**</td>

<td rowspan="1" colSpan="1" >`onContactClick: (ContactInfo) -> Unit`</td>

<td rowspan="1" colSpan="1" >点击联系人 cell 时触发，建议跳转用户信息页（C2CChatSetting）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`onGroupClick: (ContactInfo) -> Unit`</td>

<td rowspan="1" colSpan="1" >点击群组 cell 时触发，建议跳转群聊页面（ChatPage）。</td>
</tr>

<tr>
<td rowspan="3" colSpan="1" >**ChatPage**</td>

<td rowspan="1" colSpan="1" >`onUserClick: (String) -> Unit`</td>

<td rowspan="1" colSpan="1" >点击消息中的用户头像或昵称时触发，建议跳转用户信息页（C2CChatSetting）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`onChatHeaderClick: (String) -> Unit`</td>

<td rowspan="1" colSpan="1" >点击导航栏中的头像时触发，建议跳转用户信息页（C2CChatSetting）或群聊信息页（GroupChatSetting）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`onBackClick: () -> Unit`</td>

<td rowspan="1" colSpan="1" >点击返回按钮时触发，建议返回上一级页面。</td>
</tr>
</table>


**chat/demo/app/src/main/java/io/trtc/tuikit/chat/MainActivity.kt **和 **chat/demo/app/src/main/java/io/trtc/tuikit/chat/chat/ChatActivity.kt** 作为上述 Page 的粘合层，实现了各个 Page 的回调事件，核心示例代码如下：
``` java
// chat/demo/app/src/main/java/io/trtc/tuikit/chat/MainActivity.kt

// 点击会话列表 cell 跳转
ConversationsPage(onConversationClick = {
    activity?.startActivity(
        Intent(activity, ChatActivity::class.java).apply {
            putExtra("conversationID", it.conversationID)
        }
    )
})

// 点击联系人页面跳转
ContactsPage(onGroupClick = {
    ChatSettingActivity.start(context, "", it.contactID, true)
}, onContactClick = {
    ChatSettingActivity.start(context, it.contactID, "", true)
})
```
``` java
// chat/demo/app/src/main/java/io/trtc/tuikit/chat/chat/ChatActivity.kt

// 点击聊天页面跳转
ChatPage(
   conversationID = conversationID,
   locateMessage = message,
   onUserClick = {
       handleChatSettingNavigation(it)
   }, onChatHeaderClick = {
       val userID = getUserID(conversationID)
       val groupID = getGroupID(conversationID)
       handleChatSettingNavigation(userID, groupID)
   }, onBackClick = { finish() })
```

您可以参考上述回调说明及参考代码，实现 Page 之间交互逻辑。

## 常见问题

### 功能常见问题

**登录失败，提示签名错误**

请检查 SDKAppID 和 UserSig 是否正确，UserSig 是否已过期。可以参考上文 [配置用户鉴权](https://write.woa.com/#db72233d-96ad-4ea7-b9d1-b591996701b5) 重新生成 UserSig。

## 联系我们

如果您在接入或使用过程有任何疑问或者建议，欢迎 [联系我们](https://cloud.tencent.com/document/product/269/59590) 提交反馈。

