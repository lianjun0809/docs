> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

TUIKit Compose is a Jetpack Compose component library based on Tencent Cloud IM SDK, providing complete solutions for instant messaging features such as chat, conversation list, and contact management. This document describes how to manually integrate these components and implement core functionality.

## Key Concepts

TUIKit Compose provides a complete set of instant messaging UI components, depending on the AtomicXCore data layer below and capable of building various functional Pages above.
- Page Layer: Complete functional pages encapsulated based on TUIKit Compose components: ChatPage, ContactsPage, ConversationsPage, which you can use directly.

- TUIKit Compose (UI Component Layer): Jetpack Compose components built on AtomicXCore, which you can embed into your existing App pages.

- AtomicXCore (Data Layer): Provides data management and business logic, including various Stores and Managers.


## Prerequisites
- Android Studio Ladybug | 2024.2.1 and above

- Android 5.0 and above system version

- Gradle 8.9 and above

- Android Gradle Plugin 8.6 and above

- JDK 17 and above

- Kotlin 1.9.0 and above

- A valid Tencent Cloud account and Chat application. You can refer to [Enable Service](https://trtc.io/document/45907?product=chat&menulabel=uikit&platform=android) to get the following information from the console:

  - SDKAppID: The ID of the Chat application obtained from the console, which is the unique identifier of the application

  - SDKSecretKey: The secret key of the application
      

      > **Note:**
      > 
>     - This project currently only supports manual integration and does not support integration through package managers like Maven.
>     - To ensure a stable build environment, please strictly follow the official compatibility requirements for configuration:
>     - For compatibility between Gradle, Android Gradle Plugin, JDK and Android Studio, please refer to the Android official documentation: [Version Notes](https://developer.android.com/build/releases/gradle-plugin#updating-gradle).
>     - For version correspondence between Kotlin, Android Gradle Plugin and Gradle, please refer to the Kotlin official documentation: [Kotlin-Gradle Plugin Compatibility](https://kotlinlang.org/docs/gradle-configure-project.html#apply-the-plugin).

      > We recommend that you choose a version combination that fully matches your project requirements according to the above guidelines.
      > 


## Integrate and Import Components

### Download Source Code
1. Download [TUIKit Compose](https://github.com/Tencent-RTC/TUIKit_android_compose) source code from GitHub:

   ``` bash
   git clone https://github.com/Tencent-RTC/TUIKit_Android_Compose.git
   ```

   Project directory structure description:

   ``` bash
   atomic-x/
   ├── src/main/
   │   ├── java/io/trtc/tuikit/atomicx/     # UI component source code (required integration)
   │       ├── messagelist/      # Message list component
   │       ├── messageinput/     # Message input component
   │       ├── conversationlist/ # Conversation list component
   │       ├── contactlist/      # Contact list component
   │       ├── basecomponent/    # Base components
   │       └── ...               # Other UI components
   │   # Resource files (required integration)
   │   ├── res/                    # Common resources
   │   ├── res-message-list/       # Message list component resources
   │   ├── res-message-input/      # Message input component resources
   │   ├── res-conversation-list/  # Conversation list component resources
   │   └── ...                     # Other component resources
   chat/
   ├── uikit/src/main/java/io/trtc/tuikit/chat/pages    # Page components (reference implementation)
   │   ├── ChatPage.kt
   │   ├── ContactsPage.kt
   │   └── ConversationsPage.kt
   └── demo/                 # Sample application (optional reference)
   ```

### Integrate Components
1. Copy the component directory completely to your Android project, as shown in the figure below, where ComposeDemo is the sample project and TUIKit_Android_Compose is the component source code downloaded from GitHub:

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/b784e12db56a11f0b0cf525400e889b2.png)

2. Add TUIKit Compose components in your settings.gradle.kts/settings.gradle file:
   

   > **Note:**
   > 

   > TUIKit_Android_Compose can be placed anywhere, as long as the relative path is correctly set in settings.gradle.
   > 


   


【Kotlin DSL (Recommended)】
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

3. Add the following dependencies in the build.gradle.kts/build.gradle of the app module:


   


【Kotlin DSL (Recommended)】
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
   

   > **Note:**
   > 
>   - When using the local integration solution, if you need to upgrade, you need to get the latest component code from GitHub and overwrite the TUIKit Compose directory in your local project.
>   - When there are conflicts between private modifications and remote changes, manual merging and conflict resolution are required.


### Configure Project
1. Find the AndroidManifest.xml file in the app directory, add `tools:replace="android:allowBackup"` in the `application` node to override the settings in the component and use your own settings.

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
2. Configure dependencies.


   Add the following dependencies in your project's gradle/libs.versions.toml file:

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
3. Enable Compose support.


   Add the following configuration in the build.gradle.kts/build.gradle of the app module:


   


【Kotlin DSL (Recommended)】
``` java
// app/build.gradle.kts
plugins {
    // Add Compose plugin
    alias(libs.plugins.kotlin.compose)
}
android {
    // Enable Compose 
    buildFeatures {
        compose = true
    }
}
```


【Groovy DSL】
``` java
// app/build.gradle
plugins {
    // Add Compose plugin
    id libs.plugins.kotlin.compose.get().pluginId
}
android {
    // Enable Compose 
    buildFeatures {
        compose true
    }
}
```

4. Configure obfuscation rules.


   Add the following obfuscation rules to your app/proguard-rules.pro file:

   ``` java
   -keep class com.tencent.** { *; }
   ```
5. Click **File > Sync Project with Gradle Files** in Android Studio to integrate components.


## Integration Steps

### Step 1: Configure User Authentication

Get UserSig based on UserID in [Chat Console](https://console.trtc.io/usersig) for subsequent user authentication during login.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/ee78464abee111f09a6b525400454e06.png)


### Step 2: User Login

You can only use the component functions normally after login authentication. You can call the login interface and pass in the SDKAPPID and userSig obtained above for login authentication:
``` swift
// User login
LoginStore.shared.login(context, SDKAPPID, userID, userSig,
    object : CompletionHandler {
        override fun onSuccess() {
              // Login successful, can navigate to chat or conversation page
        }
        override fun onFailure(code: Int, desc: String) {
              // Login failed, can show error dialog
        }
    })
```

> **Note:**
> 

> In a formal production environment, it is recommended to generate UserSig on your server side. When UserSig is needed, your App should send a request to the business server to get dynamic UserSig for authentication. For details, see [Server-side UserSig Generation](https://console.trtc.io/usersig).
> 


### Step 3: Build Conversation List Interface

You can build a conversation list page based on the ConversationList component in TUIKit Compose. The built-in functions of ConversationList are:
- Display user's conversation list, including single chat and group chat conversations

- Support user operations on individual conversations: pin, delete, clear conversation messages, etc.


   You can integrate ConversationList directly into existing App pages, or build a complete new conversation list page. One assembled UI effect is shown in the figure below:

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/29853c55b56711f0a5e052540099c741.png)


   To encapsulate ConversationList as a conversation list page, you can refer to the implementation in the `chat/uikit/src/main/java/io/trtc/tuikit/chat/pages/ConversationsPage.kt` file. `ConversationsPage` mainly does the following:

1. Added headerView above ConversationList.

2. Pass click conversation list cell events.


   The core sample code is shown below:

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

### Step 4: Build Chat Interface

You can build a chat page based on the MessageList and MessageInput components in TUIKit Compose.

The built-in functions of MessageList are:
- Display single chat or group chat message lists.

- Support operations on individual messages: view large images of image messages, play video or voice messages, copy text messages, recall messages, delete messages, etc.


   The built-in functions of MessageInput are:

- Support users to compose and send various types of messages: text, emoji, images, voice, video, files, etc.


   You can integrate MessageList and MessageInput directly into existing App pages, or build a complete new chat page. One assembled UI effect is shown in the figure below:

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/4f5f8481b56711f0a6c652540044a08e.png)


   To assemble MessageList and MessageInput into a chat page, you can refer to the implementation in the `chat/uikit/src/main/java/io/trtc/tuikit/chat/pages/ChatPage.kt` file. `ChatPage` mainly does the following:

1. Added headerView at the top to display the conversation name.

2. Vertically concatenated MessageList and MessageInput according to mobile user habits.


   The core sample code is shown below:

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

### Step 5: Build Contact Interface

You can build a contact page based on the ContactList component in TUIKit Compose. The built-in functions of ContactList are:
- View friend request list.

- View joined group list.

- Handle group invitations and applications.

- Manage blacklist.

- View friends.


   You can integrate ContactList directly into existing Apps, or build a complete new contact list page. One assembled UI effect is shown in the figure below:

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/6810fe9db56711f09a6b525400454e06.png)


   To encapsulate ContactList as a contact list page, you can refer to the implementation in the `chat/uikit/src/main/java/io/trtc/tuikit/chat/pages/ContactsPage.kt` file. `ContactsPage` mainly does the following:

1. Added headerView above ContactList.

2. Pass click contact list cell events.


   The core sample code is shown below:

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

### Step 6: Improve Navigation Logic Between Interfaces

ConversationsPage, ChatPage, and ContactsPage expose some user click events. You can customize events to implement interactions between pages:
<table>
<tr>
<td rowspan="1" colSpan="1" >Page</td>

<td rowspan="1" colSpan="1" >Callback</td>

<td rowspan="1" colSpan="1" >Suggested Navigation Logic</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >**ConversationsPage**</td>

<td rowspan="1" colSpan="1" >`onConversationClick: (ConversationInfo) -> Unit`</td>

<td rowspan="1" colSpan="1" >Triggered when clicking a conversation in the conversation list, suggest navigating to chat page (ChatPage).</td>
</tr>

<tr>
<td rowspan="2" colSpan="1" >**ContactsPage**</td>

<td rowspan="1" colSpan="1" >`onContactClick: (ContactInfo) -> Unit`</td>

<td rowspan="1" colSpan="1" >Triggered when clicking a contact cell, suggest navigating to user info page (C2CChatSetting).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`onGroupClick: (ContactInfo) -> Unit`</td>

<td rowspan="1" colSpan="1" >Triggered when clicking a group cell, suggest navigating to group chat page (ChatPage).</td>
</tr>

<tr>
<td rowspan="3" colSpan="1" >**ChatPage**</td>

<td rowspan="1" colSpan="1" >`onUserClick: (String) -> Unit`</td>

<td rowspan="1" colSpan="1" >Triggered when clicking user avatar or nickname in messages, suggest navigating to user info page (C2CChatSetting).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`onChatHeaderClick: (String) -> Unit`</td>

<td rowspan="1" colSpan="1" >Triggered when clicking avatar in navigation bar, suggest navigating to user info page (C2CChatSetting) or group chat info page (GroupChatSetting)</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`onBackClick: () -> Unit`</td>

<td rowspan="1" colSpan="1" >Triggered when clicking back button, suggest returning to previous page.</td>
</tr>
</table>


**chat/demo/app/src/main/java/io/trtc/tuikit/chat/MainActivity.kt** and **chat/demo/app/src/main/java/io/trtc/tuikit/chat/chat/ChatActivity.kt** serve as the glue layer for the above Pages, implementing callback events for each Page. The core sample code is as follows:
``` java
// chat/demo/app/src/main/java/io/trtc/tuikit/chat/MainActivity.kt

// Click conversation list cell to navigate
ConversationsPage(onConversationClick = {
    activity?.startActivity(
        Intent(activity, ChatActivity::class.java).apply {
            putExtra("conversationID", it.conversationID)
        }
    )
})

// Click contact page to navigate
ContactsPage(onGroupClick = {
    ChatSettingActivity.start(context, "", it.contactID, true)
}, onContactClick = {
    ChatSettingActivity.start(context, it.contactID, "", true)
})
```
``` java
// chat/demo/app/src/main/java/io/trtc/tuikit/chat/chat/ChatActivity.kt

// Click chat page to navigate
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

You can refer to the above callback descriptions and reference code to implement interaction logic between Pages.


