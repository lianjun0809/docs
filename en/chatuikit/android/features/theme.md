> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

TUIKit Compose provides powerful appearance customization capabilities, supporting custom theme modes (Light/Dark/Follow System) and theme colors for your application. Through simple configuration, developers can easily implement app-level theme switching and brand color customization.

Taking the message list as an example, the effects of custom theme modes and theme colors are shown below:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Light + Default Color**</td>

<td rowspan="1" colSpan="1" >**Light + Orange**</td>

<td rowspan="1" colSpan="1" >**Dark + Default Color**</td>

<td rowspan="1" colSpan="1" >**Dark + Green Theme**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/1dcc10b9bee511f08863525400e889b2.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/34013fd4bee511f0a808525400bf7822.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/4d036798bee511f0b4c35254001c06ec.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/61fff637bee511f08863525400e889b2.png)</td>
</tr>
</table>


## Core Capabilities

**Mode Switching**
- Light Mode: Bright interface suitable for daytime use.

- Dark Mode: Dark interface suitable for nighttime use.

- Follow System: Automatically follows system appearance settings.


   **Theme Color Customization**

- Preset Theme Colors: Provides standard colors like blue, green, red, orange, etc.

- Custom Theme Colors: Supports any Hex format color.

- Smart Palette Generation: Automatically generates a complete palette of 10 color shades.

- Clear Customization: One-click restore to default theme color.


## API Reference

The above functionalities are based on a set of concise APIs provided by `ThemeState` for theme configuration and information queries.

### Set Theme Mode
<table>
<tr>
<td rowspan="1" colSpan="1" >Method</td>

<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Return Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`setThemeMode`</td>

<td rowspan="1" colSpan="1" >`ThemeMode`</td>

<td rowspan="1" colSpan="1" >`Unit`</td>

<td rowspan="1" colSpan="1" >Sets the display mode, automatically saves and refreshes.<br>• `ThemeMode.SYSTEM`: Follow system appearance.<br>• `ThemeMode.LIGHT`: Force light mode.<br>• `ThemeMode.DARK`: Force dark mode.</td>
</tr>
</table>


### Set Theme Color
<table>
<tr>
<td rowspan="1" colSpan="1" >Method</td>

<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Return Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`setPrimaryColor`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >`Unit`</td>

<td rowspan="1" colSpan="1" >Sets the theme color, requires Hex format (e.g., "#1C66E5").</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`clearPrimaryColor`</td>

<td rowspan="1" colSpan="1" >None</td>

<td rowspan="1" colSpan="1" >`Unit`</td>

<td rowspan="1" colSpan="1" >Clears custom theme color and restores default blue.</td>
</tr>
</table>


> **Note:**
> 
> - After calling `setThemeMode` or `setPrimaryColor`, the configuration is automatically saved to persistent storage without manual saving. It will automatically load on next app launch.
> - Cache is automatically cleared when modifying theme configuration, ensuring the color scheme updates in real-time. Developers don't need to manage cache.
> - Avoid frequently switching themes when using settings APIs (e.g., calling in a loop).


### Query ThemeState Information

The following read-only properties can be used to query the current theme configuration status and information:
<table>
<tr>
<td rowspan="1" colSpan="1" >Property</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`currentMode`</td>

<td rowspan="1" colSpan="1" >`ThemeMode`</td>

<td rowspan="1" colSpan="1" >Current theme mode.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`currentPrimaryColor`</td>

<td rowspan="1" colSpan="1" >`String?`</td>

<td rowspan="1" colSpan="1" >Current theme color (Hex format).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`hasCustomPrimaryColor`</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >Whether a custom theme color is set.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isDarkMode`</td>

<td rowspan="1" colSpan="1" >`Boolean`</td>

<td rowspan="1" colSpan="1" >Whether currently in dark mode.</td>
</tr>
</table>


## Usage

This section introduces how to integrate and use theme and theme color customization features in your application, providing three approaches from simple to complex.

### Approach 1: Using AppBuilder Configuration (Recommended)

AppBuilder is a convenient feature and UI customization configuration tool, managed through JSON configuration files, suitable for scenarios where Web + Native dual-platform applications need to maintain a unified appearance.

You can experience the AppBuilder feature at [Chat Web Demo](https://trtc.io/demo/homepage/#/detail?scene=messenger), experience entry:

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/321d5873b88211f09a6b525400454e06.png)


Although the Chat Web Demo currently cannot preview mobile configuration effects in real-time, mobile platforms already support AppBuilder's configuration capabilities.

Next, we'll introduce how to apply custom configurations to mobile projects after setting up AppBuilder in the Web demo. The process is quite simple, with only 2 steps:
1. Download the configuration file.

2. Drag the configuration file appConfig.json into your Android project.


####  1. Download Configuration File

Visit [Chat Web Demo](https://trtc.io/demo/homepage/#/detail?scene=messenger) and download the appConfig.json configuration file. The download path is:

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/3205aa68b88211f0a808525400bf7822.png)


The `appConfig.json` file content is shown below, corresponding one-to-one with the configuration items on the AppBuilder page. The appearance-related configurations are `theme` and its subfields:
``` json
{
  "theme": {
    "mode": "light", // Theme mode: light-Light mode, dark-Dark mode, system-Follow system
    "primaryColor": "#E65100" // Primary color, hex color value
  },
  "messageList": {
    "alignment": "two-sided",
    "enableReadReceipt": false,
    "messageActionList": [
        "copy",
        "recall",
        "quote",
        "forward",
        "delete"
    ]
  },
  "conversationList": {
    "enableCreateConversation": true,
    "conversationActionList": [
      "delete",
      "mute",
      "pin",
      "markUnread"
    ]
  },
  "messageInput": {
    "hideSendButton": false,
    "attachmentPickerMode": "collapsed"
  },
  "search": {
    "hideSearch": false
  },
  "avatar": {
    "shape": "circular"
  }
}
```

**Configuration Options**
<table>
<tr>
<td rowspan="1" colSpan="1" >Parameter</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Options</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`mode`</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >`"system"`, `"light"`, `"dark"`</td>

<td rowspan="1" colSpan="1" >Theme mode</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`primaryColor`</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >Hex color value, e.g., `"#0ABF77"`</td>

<td rowspan="1" colSpan="1" >Theme color</td>
</tr>
</table>


#### 2. Add Configuration File to Project

Drag appConfig.json into your project. Taking the GitHub open source Demo [TUIKit Android Compose](https://github.com/Tencent-RTC/TUIKit_Android_Compose/blob/main/chat/demo/app/src/main/assets/appConfig.json) project as an example, appConfig.json is located in the demo/app's assets folder:

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027983637/ce0dba6fb88a11f0a808525400bf7822.png)


After this, without writing additional code, when you launch the app, the mode and theme color of TUIKit Compose components will automatically display the values you set in appConfig.json.

### Approach 2: Set Theme Mode via Code

You can directly set the theme mode through the API `setThemeMode`. Example code:
``` swift
val themeState = ThemeState.shared
Column {
    Button(onClick = {
        themeState.setThemeMode(ThemeMode.SYSTEM)
    }) { Text(text = "Follow System") }
    Button(onClick = {
        themeState.setThemeMode(ThemeMode.LIGHT)
    }) { Text(text = "Light Mode") }
    Button(onClick = {
        themeState.setThemeMode(ThemeMode.DARK)
    }) { Text(text = "Dark Mode") }
}
```

### Approach 3: Set Theme Color via Code

You can set the theme color through the API `setPrimaryColor` by passing a primary color value. The entire TUIKit Compose component will automatically adapt a set of similar color values in the same color scheme based on this primary color value to render the interface, without the need for manual UI adaptation. Example code:
``` swift
Column {
    var text: String by remember { mutableStateOf("#1C66E5") }

    fun isValidHexColor(): Boolean {
        return text.matches(Regex("^#[0-9A-Fa-f]{6}$"))
    }
    BasicTextField(
        value = text,
        onValueChange = { text = it },
        modifier = Modifier
            .fillMaxWidth()
            .padding(16.dp)
    )
    Button(
        enabled = isValidHexColor(),
        onClick = {
            themeState.setPrimaryColor(text)
        }) {
        Text("Apply Theme Color")
    }
}
```

> **Usage Recommendations:**
> 
> - For most applications, it's recommended to use the JSON configuration file approach, which is simple, reliable, and supports multi-platform uniformity.
> - Consistently use colors from `themeState.colors` throughout the application to ensure interface consistency when switching themes.


## FAQ

### **How to determine if currently in dark mode?**
``` java
if themeState.isDarkMode {
    // Currently in dark mode
} else {
    // Currently in light mode
}
```

### **Can I set transparency?**

Not supported. Theme colors only support 6-digit Hex format (RGB), not 8-digit format (RGBA).

### **How to restore default theme?**
``` swift
themeState.clearPrimaryColor()  // Clear custom theme color
themeState.setThemeMode(ThemeMode.SYSTEM)  // Restore follow system
```

### **Where is theme configuration stored?**

Stored in the app's persistent storage. It will be lost after uninstalling the app and will restore to default configuration after reinstalling.

### **How to get the complete current theme configuration?**
``` swift
val config = themeState.currentTheme
print("Mode: ${config.mode}")
print("Theme Color: ${config.primaryColor ?: "Default"}")
```

### **Can I set mode and theme color simultaneously?**

Yes, you can call both methods separately, and the system will automatically merge the configurations:
``` swift
themeState.setThemeMode(ThemeMode.DARK)
themeState.setPrimaryColor("#0ABF77")
```
