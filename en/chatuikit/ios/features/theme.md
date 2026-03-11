> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

TUIKit SwiftUI provides powerful appearance customization capabilities, supporting custom theme modes (Light/Dark/Follow System) and theme colors for your application. Through simple configuration, developers can easily implement app-level theme switching and brand color customization.

Taking the message list as an example, the effects of custom theme modes and theme colors are shown below:
<table>
<tr>
<td rowspan="1" colSpan="1" >**Light + Default Color**</td>

<td rowspan="1" colSpan="1" >**Light + Orange**</td>

<td rowspan="1" colSpan="1" >**Dark + Default Color**</td>

<td rowspan="1" colSpan="1" >**Dark + Green Theme**</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027639409/6c3b7f7ab2e511f0b96752540044a08e.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027639409/fb4a9542b30c11f097b152540099c741.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027639409/6c3aca9bb2e511f0bd1d5254001c06ec.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027639409/6c3d7e74b2e511f0b96752540044a08e.png)</td>
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
<td rowspan="1" colSpan="1" >`setThemeMode(_:)`</td>

<td rowspan="1" colSpan="1" >`ThemeMode`</td>

<td rowspan="1" colSpan="1" >`Void`</td>

<td rowspan="1" colSpan="1" >Sets the display mode, automatically saves and refreshes.<br>• `.system`: Follow system appearance.<br>• `.light`: Force light mode.<br>• `.dark`: Force dark mode.</td>
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
<td rowspan="1" colSpan="1" >`setPrimaryColor(_:)`</td>

<td rowspan="1" colSpan="1" >`String`</td>

<td rowspan="1" colSpan="1" >`Void`</td>

<td rowspan="1" colSpan="1" >Sets the theme color, requires Hex format (e.g., "#1C66E5").</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`clearPrimaryColor()`</td>

<td rowspan="1" colSpan="1" >None</td>

<td rowspan="1" colSpan="1" >`Void`</td>

<td rowspan="1" colSpan="1" >Clears custom theme color and restores default blue.</td>
</tr>
</table>


> **Note:**
> 
> 1. After calling `setThemeMode` or `setPrimaryColor`, the configuration is automatically saved to `UserDefaults` without manual saving. It will automatically load on next app launch.
> 2. Cache is automatically cleared when modifying theme configuration, ensuring the color scheme updates in real-time. Developers don't need to manage cache.
> 3. Avoid frequently switching themes when using settings APIs (e.g., calling in a loop).


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

<td rowspan="1" colSpan="1" >`Bool`</td>

<td rowspan="1" colSpan="1" >Whether a custom theme color is set.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`isDarkMode`</td>

<td rowspan="1" colSpan="1" >`Bool`</td>

<td rowspan="1" colSpan="1" >Whether currently in dark mode.</td>
</tr>
</table>


## Usage

This section introduces how to integrate and use theme and theme color customization features in your application, providing three approaches from simple to complex.

### Approach 1: Using AppBuilder Configuration (Recommended)

AppBuilder is a convenient feature and UI customization configuration tool, managed through JSON configuration files, suitable for scenarios where Web + Native dual-platform applications need to maintain a unified appearance.

You can experience the AppBuilder feature at [Chat Web Demo](https://trtc.io/demo/homepage/#/detail?scene=messenger), experience entry:

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027639409/ab6c76ddb30111f09e195254007c27c5.png)


Although the Chat Web Demo currently cannot preview mobile configuration effects in real-time, mobile platforms already support AppBuilder's configuration capabilities.

Next, we'll introduce how to apply custom configurations to mobile projects after setting up AppBuilder in the Web demo. The process is quite simple, with only 3 steps:
1. Download the configuration file.

2. Drag the configuration file appConfig.json into your iOS project.

3. Load the configuration file at app launch.


#### Step 1: Download Configuration File

Visit [Chat Web Demo](https://trtc.io/demo/homepage/#/detail?scene=messenger) and download the appConfig.json configuration file. The download path is:

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027639409/722a624ab30011f0bb7b525400bf7822.png)


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

<td rowspan="1" colSpan="1" >Theme mode.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >`primaryColor`</td>

<td rowspan="1" colSpan="1" >String</td>

<td rowspan="1" colSpan="1" >Hex color value, e.g., `"#0ABF77"`</td>

<td rowspan="1" colSpan="1" >Theme color.</td>
</tr>
</table>


#### Step 2: Add Configuration File to Project

Drag appConfig.json into your project, ensuring the correct Target is selected and Copy Bundle Resources is properly checked.

Taking the GitHub open source Demo [TUIKit iOS SwiftUI](https://github.com/Tencent-RTC/TUIKit_iOS_SwiftUI/blob/main/chat/demo/ChatDemo/appConfig.json) project as an example, appConfig.json is located in the main bundle of demo/ChatDemo:

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027639409/06269308b30611f099275254005ef0f7.png)


#### Step 3: Load Configuration File

Set the JSON file path at app launch to load the configuration file. If you also place appConfig.json in the app's main bundle, you can obtain the JSON file like this:
``` swift
import AtomicX

@main
struct MyApp: App {
    init() {
        // Load theme configuration file
        if let path = Bundle.main.path(forResource: "appConfig", ofType: "json") {
            AppBuilderHelper.setJsonPath(path: path)
        }
    }
    
    var body: some Scene {
        WindowGroup {
            ContentView()
                // Inject ThemeState.shared into the app's root view
                .environmentObject(ThemeState.shared)
        }
    }
}
```

After this, without writing additional code, when you launch the app, the mode and theme color of TUIKit SwiftUI components will automatically display the values you set in appConfig.json.

### Approach 2: Set Theme Mode via Code

You can directly set the theme mode through the API `setThemeMode`, where themeState is the ThemeState.shared singleton object obtained from the environment. Example code:
``` swift
import SwiftUI
import AtomicX

struct SettingsView: View {
    @EnvironmentObject var themeState: ThemeState
    
    var body: some View {
        List {
            Section("Appearance Mode") {
                Button("Follow System") {
                    themeState.setThemeMode(.system)
                }
                Button("Light Mode") {
                    themeState.setThemeMode(.light)
                }
                Button("Dark Mode") {
                    themeState.setThemeMode(.dark)
                }
            }
        }
        .navigationTitle("Settings")
    }
}
```

### Approach 3: Set Theme Color via Code

You can set the theme color through the API `setPrimaryColor` by passing a primary color value. The entire TUIKit SwiftUI component will automatically adapt a set of similar color values in the same color scheme based on this primary color value to render the interface, without the need for manual UI adaptation. Example code:
``` swift
struct CustomColorPicker: View {
    @EnvironmentObject var themeState: ThemeState
    @State private var customColor = "#1C66E5"
    
    var body: some View {
        VStack(spacing: 20) {
            TextField("Enter color value", text: $customColor)
                .textFieldStyle(RoundedBorderTextFieldStyle())
                .placeholder(when: customColor.isEmpty) {
                    Text("#1C66E5").foregroundColor(.gray)
                }
            
            Button("Apply Theme Color") {
                themeState.setPrimaryColor(customColor)
            }
            .disabled(!isValidHexColor(customColor))
        }
        .padding()
    }
    
    private func isValidHexColor(_ hex: String) -> Bool {
        let pattern = "^#[0-9A-Fa-f]{6}$"
        return hex.range(of: pattern, options: .regularExpression) != nil
    }
}
```

> **Usage Recommendations:**
> 
> - For most applications, it's recommended to use the JSON configuration file approach, which is simple, reliable, and supports multi-platform uniformity.
> - Consistently use colors from `themeState.colors` throughout the application to ensure interface consistency when switching themes.


## FAQ
- **How to determine if currently in dark mode?**

   ``` swift
   if themeState.isDarkMode {
       // Currently in dark mode
   } else {
       // Currently in light mode
   }
   ```
- **How to see effects immediately after setting theme color?**


   The UI will automatically refresh after setting the theme color because `ThemeState` is an `ObservableObject`. Ensure your views use `@EnvironmentObject` or `@ObservedObject` to observe state changes.

- **Can I set transparency?**


   Not supported. Theme colors only support 6-digit Hex format (RGB), not 8-digit format (RGBA). If you need transparency effects, add the `.opacity()` modifier when using colors.

- **How to restore default theme?**

   ``` swift
   themeState.clearPrimaryColor()  // Clear custom theme color
   themeState.setThemeMode(.system) // Restore follow system
   ```
- **Where is theme configuration stored?**


   Stored in `UserDefaults` with key `"BaseComponentThemeKey"`. It will be lost after uninstalling the app and will restore to default configuration after reinstalling.

- **How to get the complete current theme configuration?**

   ``` swift
   let config = themeState.currentTheme
   print("Mode: \(config.mode)")
   print("Theme Color: \(config.primaryColor ?? "Default")")
   ```
- **Can I set mode and theme color simultaneously?**


   Yes, you can call both methods separately, and the system will automatically merge the configurations:

   ``` swift
   themeState.setThemeMode(.dark)
   themeState.setPrimaryColor("#0ABF77")
   ```
   