> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

TUIKit Flutter is a set of Flutter UI component libraries based on Tencent Cloud IM SDK, providing complete solutions for instant messaging features such as chat, conversation list, and contact management. This document introduces how to manually integrate these components and implement core features.

## Key Concepts

TUIKit provides a complete set of instant messaging UI components, relying on the AtomicXCore data layer at the bottom and allowing construction of various functional Pages at the top.
- Page Layer: Complete functional pages encapsulated based on TUIKit components: ChatPage, ContactsPage, ConversationsPage, which you can use directly.

- TUIKit Flutter (UI Component Layer): Flutter components built on AtomicXCore, which you can embed into your existing App pages.

- AtomicXCore (Data Layer): Provides data management and business logic, including various Stores and Managers.


## Prerequisites
- Flutter >= 3.29.0, Dart >= 3.7.0, Kotlin >= 1.9.

- Android Studio Ladybug | 2024.2.1 or higher, Android Gradle plugin 7.3.1 or higher, JDK 17.

- Xcode 12.0 or higher.

- A valid Tencent Cloud account and Chat application. Refer to [Activate Service](https://trtc.io/document/45907?product=chat&menulabel=uikit&platform=flutter) to obtain the following information from the console:

  - SDKAppID: The ID of the Chat application obtained from the console, serving as the unique identifier for the application.

  - SDKSecretKey: The application's secret key.
      

      > **Note:**
      > 
>     - This project currently only supports manual integration and does not support integration via pub.dev.
>     - To ensure a stable build environment, please strictly follow the official compatibility requirements for configuration:
>     - For compatibility between Gradle, Android Gradle Plugin, JDK, and Android Studio, please refer to the Android official documentation: [Version Notes](https://developer.android.com/build/releases/gradle-plugin#updating-gradle).
>     - For version correspondence between Kotlin, Android Gradle Plugin, and Gradle, please refer to the Kotlin official documentation: [Kotlin-Gradle Plugin Compatibility](https://kotlinlang.org/docs/gradle-configure-project.html#apply-the-plugin).
>     - Use JDK 17, as other versions may cause compilation failures. Refer to: [Java Version Switching](https://developer.android.com/build/jdks#kts).

      > We recommend that you choose a version combination that fully matches the project requirements according to the above guidelines.
      > 


## Integration and Import Components

### Download Source Code

1. Download [TUIKit Flutter](https://github.com/Tencent-RTC/TUIKit_Flutter) source code from GitHub:
``` xml
git clone https://github.com/Tencent-RTC/TUIKit_Flutter.git
```

Project directory structure explanation:
``` bash
atomic-x/
├── lib/                  # UI component source code (required integration)
│   ├── messagelist/      # Message list component
│   ├── messageinput/     # Message input component
│   ├── conversationlist/ # Conversation list component
│   ├── contactlist/      # Contact list component
│   ├── basecomponent/    # Base components
│   └── ...               # Other UI components
├── call_assets/          # Call resource files (required integration)
├── chat_assets/          # Chat resource files (required integration)
chat/
├── uikit/                # Page components (reference implementation)
│   ├── lib/
│      ├── chat_page.dart
│      ├── contacts_page.dart
│      └── conversations_page.dart
└── demo/                 # Example application (optional reference)
```

### Integrate Components
1. Copy the complete component directory to your Flutter project, as shown below. Here flutter_demo is the example project, and TUIKit_Flutter is the component source code downloaded from GitHub:

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027325838/b47217aac39011f0a6dd5254005ef0f7.png)

2. Add TUIKit Flutter components to your pubspec.yaml file. Note that TUIKit_Flutter can be placed anywhere, as long as the relative path is correctly set in pubspec.yaml:

   ``` bash
     tuikit_atomic_x:
       path: ../TUIKit_Flutter/atomic-x
   ```   

   > **Note:**
   > 
>   - When using the local integration solution, if you need to upgrade, you need to obtain the latest component code from GitHub and overwrite the TUIKit_Flutter directory in your local project.
>   - When there are conflicts between private modifications and remote changes, you need to manually merge and resolve conflicts.


### Configure Project

Add necessary permission configurations on the iOS side. Open ios/Podfile and add the following permission code at the end of the file:
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

## Integration Steps

### Step 1: Configure User Authentication

Obtain UserSig according to UserID in the [Chat Console](https://console.trtc.io/usersig) for subsequent user authentication during login.


### Step 2: User Login

After login authentication, you can use the component features normally. You can call the login interface and pass the SDKAPPID, userID, and userSig obtained above for login authentication:
``` java
final result = await LoginStore.shared.login(
      sdkAppID: SDKAPPID,
      userID: userID,
      userSig: userSig,
    );
if (result.errorCode == 0) {
    // Login successful, can navigate to chat or conversation page
} else {
    // Login failed, can display error popup
}
```

> **Note:**
> 

> In a formal production environment, it is recommended to generate UserSig on your server. When UserSig is needed, your App should send a request to your business server to obtain dynamic UserSig for authentication. See [Generate UserSig on Server](https://trtc.io/document/34385).
> 


### Step 3: Build Conversation List Interface

You can build a conversation list page based on the ConversationList component in TUIKit Flutter. Built-in features of ConversationList include:
- Display the user's conversation list, including one-on-one and group conversations

- Support user operations on individual conversations: pin, delete, clear conversation messages, etc.


   You can integrate ConversationList directly into your existing App page, or build a complete new conversation list page. One assembled UI effect is shown below:

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027325838/acbda867c3a611f08c0e52540044a08e.png)


   To encapsulate ConversationList as a conversation list page, refer to the implementation in the `chat/uikit/lib/conversations_page.dart` file. `ConversationsPage` mainly does the following:

1. Adds AppBar above ConversationList.

2. Implements click events for conversation list cells.

3. Supports creating conversations and groups:

  1. Click the button in the upper right corner to create new conversations or groups

  2. Supports selecting friends from the contact list to create one-on-one chats

  3. Supports selecting multiple friends to create group chats


      Core example code is as follows:

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

### Step 4: Build Chat Interface

You can build a chat page based on the MessageList and MessageInput components in TUIKit Flutter.

Built-in features of MessageList include:
- Display one-on-one or group message lists.

- Support operations on individual messages: view large images for image messages, play video or voice messages, copy text messages, recall messages, delete messages, etc.


   Built-in features of MessageInput include:

- Support users in composing and sending various types of messages: text, emoji, image, voice, video, file, etc.


   You can integrate MessageList and MessageInput directly into your existing App page, or build a complete new chat page. One assembled UI effect is shown below:

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027325838/a2c04843c3a811f0a6dd5254005ef0f7.png)


   To assemble MessageList and MessageInput as a chat page, refer to the implementation in the `chat/uikit/lib/chat_page.dart` file. `ChatPage` mainly does the following:

1. Adds AppBar at the top to display the conversation name.

2. Vertically combines MessageList and MessageInput according to mobile user habits.


   Core example code is as follows:

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

### Step 5: Build Contact Interface

You can build a contact page based on the ContactList component in TUIKit Flutter. Built-in features of ContactList include:
- View friend request list.

- View list of joined groups.

- Handle group invitations and applications.

- Manage blocklist.

- View friends.


   You can integrate ContactList directly into your existing App, or build a complete new contact list page. One assembled UI effect is shown below:

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027325838/4bf1d883c3a911f0b35752540099c741.png)


   To encapsulate ContactList as a contact list page, refer to the implementation in the `chat/uikit/lib/contacts_page.dart` file. `ContactsPage` mainly does the following:

1. Adds AppBar above ContactList.

2. Implements click events for contact list cells.

3. Supports adding contacts and groups:

  1. Click the "+" button in the upper right corner to add contacts or groups

  2. Supports searching for target contacts by UserID

  3. Supports searching for target groups by GroupID


      Core example code is as follows:

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

### Step 6: Complete Navigation Logic Between Interfaces

ConversationsPage, ChatPage, and ContactsPage implement default user click events. You can customize events to implement interactions between pages:
<table>
<tr>
<td rowspan="1" colSpan="1" >Page</td>

<td rowspan="1" colSpan="1" >Callback</td>

<td rowspan="1" colSpan="1" >Suggested Navigation Logic</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**ConversationsPage**</td>

<td rowspan="1" colSpan="1" >`onConversationClick: (conversation) {}`</td>

<td rowspan="1" colSpan="1" >Triggered when clicking a conversation in the conversation list, recommended to navigate to the chat page (ChatPage).</td>
</tr>

<tr>
<td rowspan="2" colSpan="1" >**ContactsPage**</td>

<td rowspan="1" colSpan="1" >`onContactClick: (ContactInfo contactInfo) {}`</td>

<td rowspan="1" colSpan="1" >Triggered when clicking a contact cell, recommended to navigate to the user info page (C2CChatSetting).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`onGroupClick: (ContactInfo contactInfo) {}`</td>

<td rowspan="1" colSpan="1" >Triggered when clicking a group cell, recommended to navigate to the group chat page (ChatPage).</td>
</tr>

<tr>
<td rowspan="3" colSpan="1" >**ChatPage**</td>

<td rowspan="1" colSpan="1" >`onUserClick: (String userID) {}`</td>

<td rowspan="1" colSpan="1" >Triggered when clicking a user avatar or nickname in a message, recommended to navigate to the user info page (C2CChatSetting).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`onChatHeaderClick: () {}`</td>

<td rowspan="1" colSpan="1" >Triggered when clicking the avatar in the navigation bar, recommended to navigate to the user info page (C2CChatSetting) or group chat info page (GroupChatSetting)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`onBackClick: () {}`</td>

<td rowspan="1" colSpan="1" >Triggered when clicking the back button, recommended to return to the previous page.</td>
</tr>
</table>


You can refer to the above callback descriptions and reference code to implement interaction logic between Pages.

## FAQ

### **After integrating the tuikit_atomic_x component, what should I do about errors related to **`theme_state`** and **`atomic_localizations`**?**

The component supports theme color and internationalized string switching. You need to use `ComponentTheme` to wrap the root `widget` in the `main.dart` file in the project root directory, and add the `AtomicLocalizations.delegate` configuration to the `localizationsDelegates` of `MaterialApp`. You can refer to the `main.dart` file in the source code Demo for usage.

