> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

TUIKit Flutter 是基于腾讯云 IM SDK 的一套 Flutter UI 组件库，提供了聊天、会话列表、联系人管理等即时通信功能的完整解决方案。本文介绍如何手动集成该组件并实现核心功能。

## 关键概念

TUIKit 提供了一套完整的即时通信 UI 组件，向下依赖 AtomicXCore 数据层，向上可构建各种功能性 Page。
- Page 层：基于 TUIKit 组件封装的完整功能页面：ChatPage、ContactsPage、ConversationsPage，您可以直接使用。

- TUIKit Flutter（UI 组件层）：基于 AtomicXCore 构建的 Flutter 组件，您可将其嵌套到自己已有的 App 页面中。

- AtomicXCore（数据层）：提供数据管理和业务逻辑，包含各种 Store 和 Manager。


## 前提条件
- Flutter >= 3.29.0 版本，Dart >= 3.7.0 版本，Kotlin >= 1.9版本。

- Android Studio Ladybug | 2024.2.1 及以上版本，Android Gradle plugin 7.3.1 以上版本，JDK 17 版本。

- Xcode 12.0 及以上版本。

- 一个有效的腾讯云账号及 Chat 应用。可参考 [开通服务](https://write.woa.com/document/107052220771086336#step1) 从控制台获取以下信息：

  - SDKAppID：App 在控制台获取的 Chat 应用的 ID，为应用的唯一标识。

  - SDKSecretKey：应用的密钥。
      

      > **说明：**
      > 
>     - 本项目目前仅支持手动集成，暂不支持通过 pub.dev 集成。
>     - 为确保构建环境稳定，请严格遵循官方兼容性要求进行配置：
>     - Gradle、Android Gradle Plugin、JDK 与 Android Studio 的兼容性，请参阅 Android 官方文档：[版本说明](https://developer.android.com/build/releases/gradle-plugin#updating-gradle)﻿。
>     - Kotlin、Android Gradle Plugin 与 Gradle 的版本对应关系，请参阅 Kotlin 官方文档：[Kotlin-Gradle 插件兼容性](https://kotlinlang.org/docs/gradle-configure-project.html#apply-the-plugin)。
>     - 使用 JDK 17 版本，其他版本可能导致编译失败，请参阅：[Java 版本切换](https://developer.android.com/build/jdks#kts)。

      > 我们建议您根据上述指南，选择与项目要求完全匹配的版本组合。
      > 


## 集成并引入组件

### 下载源码

1. 从 GitHub 下载 [TUIKit Flutter](https://github.com/Tencent-RTC/TUIKit_Flutter) 源码：
``` xml
git clone https://github.com/Tencent-RTC/TUIKit_Flutter.git
```

项目目录结构说明：
``` bash
atomic-x/
├── lib/                  # UI 组件源码（必需集成）
│   ├── messagelist/      # 消息列表组件
│   ├── messageinput/     # 消息输入组件
│   ├── conversationlist/ # 会话列表组件
│   ├── contactlist/      # 联系人列表组件
│   ├── basecomponent/    # 基础组件
│   └── ...               # 其他 UI 组件
├── call_assets/          # call 资源文件（必需集成）
├── chat_assets/          # chat 资源文件（必需集成）
chat/
├── uikit/                # Page 组件（参考实现）
│   ├── lib/
│      ├── chat_page.dart
│      ├── contacts_page.dart
│      └── conversations_page.dart
└── demo/                 # 示例应用（可选参考）
```

### 集成组件
1. 将组件目录完整复制到您的 Flutter 项目中，如下图所示，其中 flutter_demo 是示例项目，TUIKit_Flutter 是从 GitHub 上下载的组件源码：

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027325838/b47217aac39011f0a6dd5254005ef0f7.png)

2. 在您的 pubspec.yaml 文件中添加 TUIKit Flutter 组件。注意，TUIKit_Flutter 可以放在任何位置，只要在 pubspec.yaml 中正确设置相对路径即可：

   ``` bash
     tuikit_atomic_x:
       path: ../TUIKit_Flutter/atomic-x
   ```   

   > **注意：**
   > 
>   - 使用本地集成方案时，如需升级，您需要从 GitHub 获取最新的组件代码，覆盖您本地项目的 TUIKit_Flutter 目录。
>   - 当私有化修改和远端有冲突时，需要手动合并，处理冲突。


### 配置项目

在 iOS 端添加必要的权限配置。请打开 ios/Podfile ，在文件末尾新增如下权限代码：
``` objectivec
post_install do |installer|
  installer.pods_project.targets.each do |target|
    flutter_additional_ios_build_settings(target)
    target.build_configurations.each do |config|        
          config.build_settings['EXCLUDED_ARCHS[sdk=iphonesimulator*]'] = 'arm64'               
          config.build_settings['ENABLE_BITCODE'] = 'NO'        
          config.build_settings["ONLY_ACTIVE_ARCH"] = "NO"    
        end
    target.build_configurations.each do |config|
          config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] ||= [
            '$(inherited)',
            'PERMISSION_MICROPHONE=1',
            'PERMISSION_CAMERA=1',
            'PERMISSION_PHOTOS=1',
          ]
        end
  end
end

```

## 接入步骤

### 步骤1：配置用户鉴权

在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im/tool-usersig) 根据 UserID 获取 UserSig 用于后续登录时的用户鉴权。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027325838/10e98dafc3a611f09c26525400bf7822.png)


### 步骤2：用户登录

登录鉴权后才能正常使用组件的功能。您可以调用 login 接口，传入上文获取的 SDKAPPID、userID、userSig 用于登录鉴权：
``` java
final result = await LoginStore.shared.login(
      sdkAppID: SDKAPPID,
      userID: userID,
      userSig: userSig,
    );
if (result.errorCode == 0) {
    // 登录成功，可跳转聊天或会话页
} else {
    // 登录失败，可弹框报错
}
```

> **注意：**
> 

> 在正式的生产环境中，建议在您的服务端生成 UserSig，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig 来进行鉴权。详见 [服务端生成 UserSig](https://cloud.tencent.com/document/product/269/32688)。
> 


### 步骤3：构建会话列表界面

您可以基于 TUIKit Flutter 中的 ConversationList 组件，构建一个会话列表页面。ConversationList 内建的功能是：
- 展示用户的会话列表，包含单聊和群聊会话

- 支持用户操作单个会话：置顶、删除、清空会话消息等


   您可以将 ConversationList 直接集成到现有的 App 页面中，也可以新构建一个完整的会话列表页，组装后的一种 UI 效果如下图所示：

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027325838/acbda867c3a611f08c0e52540044a08e.png)


   将 ConversationList 封装为会话列表页，可参考 `chat/uikit/lib/conversations_page.dart` 文件里的实现，`ConversationsPage` 主要做了以下工作：

1. 在 ConversationList 上方添加了 AppBar。

2. 实现点击会话列表 cell 事件。

3. 支持创建会话和群组功能：

  1. 点击右上角按钮可以创建新会话或群组

  2. 支持从联系人列表选择好友创建单聊

  3. 支持选择多个好友创建群聊


      核心示例代码如下所示：

      ``` java
        @override
        Widget build(BuildContext context) {
          return Scaffold(
            appBar: AppBar(
              backgroundColor: colorsTheme.bgColorOperate,
              title: Text(atomicLocale.chat, style: TextStyle(fontSize: 34, fontWeight: FontWeight.w600)),
              centerTitle: false,
              scrolledUnderElevation: 0,
              actions: [],
            ),
            body: Column(
              children: [
                Expanded(
                  child: ConversationList(
                    onConversationClick: (conversation) {
                      Navigator.push(
                        context,
                        MaterialPageRoute(
                          builder: (context) => ChatPage(
                            conversation: conversation,
                          ),
                        ),
                      );
                    },
                  ),
                ),
              ],
            ),
          );
        }
      ```

### 步骤4：构建聊天界面

您可以基于 TUIKit Flutter 中的 MessageList、MessageInput  组件，构建一个聊天页面。

MessageList 内建的功能是：
- 展示单聊或群聊消息列表。

- 支持对单条消息操作：查看图片消息的大图、播放视频或语音消息、复制文本消息、撤回消息、删除消息等。


   MessageInput 内建的功能是：

- 支持用户组建并发送多种类型的消息：文本、表情、图片、语音、视频、文件等。


   您可以将 MessageList 和  MessageInput 直接集成到现有的 App 页面中，也可以新构建一个完整的聊天页，组装后的一种 UI 效果如下图所示：

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027325838/a2c04843c3a811f0a6dd5254005ef0f7.png)


   将 MessageList 和 MessageInput 组装为聊天页，可参考  `chat/uikit/lib/chat_page.dart` 文件里的实现，`ChatPage` 主要做了以下工作：

1. 在最上方添加了 AppBar，展示会话的名称。

2. 按照移动端用户使用习惯，上下拼接 MessageList 和 MessageInput。


   核心示例代码如下所示：

   ``` java
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(
             backgroundColor: colorsTheme.bgColorOperate,
             titleSpacing: 4.0,
             centerTitle: false,
             title: GestureDetector(
               onTap: _onTitleTap,
               child: Row(
                 mainAxisSize: MainAxisSize.min,
                 children: [
                   Padding(
                     padding: const EdgeInsets.only(right: 8.0),
                     child: Avatar.image(
                       name: widget.conversation.title,
                       url: widget.conversation.avatarURL,
                     ),
                   ),
                   Expanded(
                     child: Text(
                       widget.conversation.title ?? atomicLocale.chat,
                       style: TextStyle(fontSize: 14, fontWeight: FontWeight.w600),
                       overflow: TextOverflow.ellipsis,
                       maxLines: 1,
                     ),
                   ),
                 ],
               ),
             ),
             scrolledUnderElevation: 0.0,
             leading: IconButton.buttonContent(
               content: IconOnlyContent(Icon(Icons.arrow_back_ios, color: colorsTheme.buttonColorPrimaryDefault)),
               type: ButtonType.noBorder,
               size: ButtonSize.l,
               onClick: () => Navigator.of(context).pop(),
             ),
             actions: []),
         body: Column(
           children: [
             MessageList(
               conversationID: widget.conversation.conversationID,
               locateMessage: widget.message,
               onUserClick: (String userID) => _onUserClick(userID),
             ),
             MessageInput(
               conversationID: widget.conversation.conversationID,
             ),
           ],
         ),
       );
     }
   ```

### 步骤5：构建联系人界面

您可以基于 TUIKit Flutter 中的 ContactList 组件，构建一个联系人页面。ContactList 内建的功能是：
- 查看好友申请列表。

- 查看已加入的群列表。

- 处理群组邀请和申请。

- 管理黑名单列表。

- 查看好友。


   您可以将 ContactList 直接集成到现有的 App 中，也可以新构建一个完整的联系人列表页，组装后的一种 UI 效果如下图所示：

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027325838/4bf1d883c3a911f0b35752540099c741.png)


   将 ContactList 封装为联系人列表页，可参考 `chat/uikit/lib/contacts_page.dart `文件里的实现，`ContactsPage` 主要做了以下工作：

1. 在 ContactList 上方添加了 AppBar。

2. 实现点击联系人列表 cell 事件。

3. 支持添加联系人和添加群组：

  1. 点击右上角 "+" 按钮可以添加联系人或群组

  2. 支持根据 UserID 搜索目标联系人

  3. 支持根据 GroupID 搜索目标群组


      核心示例代码如下所示：

      ``` java
        @override
        Widget build(BuildContext context) {
          AtomicLocalizations atomicLocale = AtomicLocalizations.of(context);
          SemanticColorScheme colorsScheme = BaseThemeProvider.colorsOf(context);
          return Scaffold(
            appBar: AppBar(
              backgroundColor: colorsScheme.bgColorOperate,
              title: Text(atomicLocale.contact, style: TextStyle(fontSize: 34, fontWeight: FontWeight.w600),),
              centerTitle: false,
              scrolledUnderElevation: 0,
              actions: [],
            ),
            body: ContactList(
              onGroupClick: (ContactInfo contactInfo) {
                _onGroupClick(context, contactInfo);
              },
              onContactClick: (ContactInfo contactInfo) {
                _onContactClick(context, contactInfo);
              },
            ),
          );
        }
      ```

### 步骤6：完善界面间的跳转逻辑

ConversationsPage、ChatPage、ContactsPage 中实现了默认的用户点击事件，您可以自定义事件来实现页面间的交互：
<table>
<tr>
<td rowspan="1" colSpan="1" >Page</td>

<td rowspan="1" colSpan="1" >回调</td>

<td rowspan="1" colSpan="1" >建议跳转逻辑</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**ConversationsPage**</td>

<td rowspan="1" colSpan="1" >`onConversationClick: (conversation) {}`</td>

<td rowspan="1" colSpan="1" >点击会话列表中的会话时触发，建议跳转到聊天页面（ChatPage）。</td>
</tr>

<tr>
<td rowspan="2" colSpan="1" >**ContactsPage**</td>

<td rowspan="1" colSpan="1" >`onContactClick: (ContactInfo contactInfo) {}`</td>

<td rowspan="1" colSpan="1" >点击联系人 cell 时触发，建议跳转到用户信息页（C2CChatSetting）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`onGroupClick: (ContactInfo contactInfo) {}`</td>

<td rowspan="1" colSpan="1" >点击群组 cell 时触发，建议跳转群聊页面（ChatPage）。</td>
</tr>

<tr>
<td rowspan="3" colSpan="1" >**ChatPage**</td>

<td rowspan="1" colSpan="1" >`onUserClick: (String userID) {}`</td>

<td rowspan="1" colSpan="1" >点击消息中的用户头像或昵称时触发，建议跳转用户信息页（C2CChatSetting）。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`onChatHeaderClick: () {}`</td>

<td rowspan="1" colSpan="1" >点击导航栏中的头像时触发，建议跳转用户信息页（C2CChatSetting）或群聊信息页（GroupChatSetting）</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`onBackClick: () {}`</td>

<td rowspan="1" colSpan="1" >点击返回按钮时触发，建议返回上一级页面。</td>
</tr>
</table>


您可以参考上述回调说明及参考代码，实现 Page 之间交互逻辑。

## 常见问题

### **集成 tuikit_atomic_x 组件后，有 **`theme_state`** 和 **`atomic_localizations`** 的报错怎么办？**

组件支持主题颜色和国际化字符串切换，需要在项目根目录的 `main.dart` 文件中使用 `ComponentTheme` 来包装根 `widget`，并且需要在 `MaterialApp` 的 `localizationsDelegates` 中增加 `AtomicLocalizations.delegate` 的配置，可参考源码 Demo 中的 `main.dart` 文件的使用。

### **登录失败，提示签名错误怎么办？**

请检查 SDKAppID 和 UserSig 是否正确，UserSig 是否已过期。可以参考上文 [配置用户鉴权](https://write.woa.com/document/193282372365111296) 重新生成 UserSig。

## 联系我们

如果您在接入或使用过程中有任何疑问或者建议，欢迎 [联系我们](https://cloud.tencent.com/document/product/269/59590) 提交反馈。

