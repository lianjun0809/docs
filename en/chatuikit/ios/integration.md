> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

This article introduces how to integrate `TUIKit` components. 

> **Note:**
> 
> - Starting from version 5.7.1435, TUIKit supports modular integration and the classic UI. You can integrate the necessary modules according to your needs.
> - Starting from version 6.9.3557, TUIKit introduces a brand new minimalist UI.
> - To respect the copyright of emoji designs, the Chat Demo/TUIKit project does not include cutouts of large emoji elements. Please replace them with your own designs or other emoji packs for which you hold the copyright before officially launching for commercial use. **The default smiley face emoji pack shown below is copyrighted by Tencent RTC** and is available for licensed use for a fee. If you need to obtain a license, please [contact us](https://trtc.io/contact).

> ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027202808/500eefe097f711efaaca525400fdb830.png)
> 


You can freely choose between the classic or minimalist UI components according to your needs. If you are not familiar with the effects of the interface libraries, you can refer to the document [TUIKit Overview](https://www.tencentcloud.com/document/product/1047/50062).

## Environment Requirements
- Xcode 10 or later

- iOS 9.0 or later


## CocoaPods Integration
1. Install CocoaPods
Enter the following command in a terminal (you need to install Ruby on your Mac first):

   ``` bash
   sudo gem install cocoapods
   ```
2. Create a Podfile
Go to the path where the project is located and run the following command. Then, a Podfile will appear under the project path.

   ``` bash
   pod init
   ```
3. Add the corresponding TUIKit components to your Podfile according to your needs. Components are independent of each other, and adding or removing them will not affect project compilation. You can choose different Podfile integration methods as needed:

  - Remote CocoaPods Integration

  - Local Integration of DevelopmentPods


      The pros and cons of the above two integration methods are shown in the following table:

<table>
<tr>
<td rowspan="1" colSpan="1" >Integration methods</td>

<td rowspan="1" colSpan="1" >Suitable Scenarios</td>

<td rowspan="1" colSpan="1" >Advantage</td>

<td rowspan="1" colSpan="1" >Disadvantage</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Remote CocoaPods Integration</td>

<td rowspan="1" colSpan="1" >Suitable for integration without source code modifications.</td>

<td rowspan="1" colSpan="1" >When there is a version update of TUIKit, you only need to `Pod update` again to complete the update.</td>

<td rowspan="1" colSpan="1" >When you have modifications to the source code, using `Pod update` to update will overwrite your modifications with the new version of TUIKit.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >Local DevelopmentPods Integration</td>

<td rowspan="1" colSpan="1" >Suitable for customers who have custom modifications to the source code</td>

<td rowspan="1" colSpan="1" >When you have your own git repository, you can track changes. After modifying the source code, using `Pod update` to update other remote Pod libraries will not overwrite your modifications.</td>

<td rowspan="1" colSpan="1" >You need to manually overwrite your local TUIKit folder with the TUIKit source code to update.</td>
</tr>
</table>


### Remote CocoaPods

> **Note:**
> 

> Swift language component support was introduced in TUIKit version 8.5.6870.
> 


You can add components as needed in your Podfile:



【Minimalist version】




【Swift】
``` bash
# Uncomment the next line to define a global platform for your project
# ...
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '13.0'
# Prevent `*.xcassets` in TUIKit from conflicting with your project
install! 'cocoapods', :disable_input_output_paths => true

# Replace `your_project_name` with your actual project name
target 'your_project_name' do
  use_frameworks!
  use_modular_headers!

  # Integrate the chat feature
  pod 'TUIChat_Swift/UI_Minimalist' 
  # Integrate the conversation list feature
  pod 'TUIConversation_Swift/UI_Minimalist'
  # Integrate the relationship chain feature
  pod 'TUIContact_Swift/UI_Minimalist'
  # Integrate the search feature (To use this feature, you need to purchase the  Pro edition 、Pro Plus edition or Enterprise edition)
  pod 'TUISearch_Swift/UI_Minimalist' 
  # Integrate the audio/video call feature
  pod 'TUICallKit_Swift'
  # Integrate Translation Plugin(Value-added feature activation required, please contact Tencent Cloud Business to activate)
  pod 'TUITranslationPlugin_Swift'  
  # Integrate Session Tagging Plugin
  pod 'TUIConversationMarkPlugin_Swift'
  # Integrate Speech-to-Text Plugin
  pod 'TUIVoiceToTextPlugin_Swift'
end

#Pods config
post_install do |installer|
    installer.pods_project.targets.each do |target|
        target.build_configurations.each do |config|                
            #Fix Xcode14 Bundle target error
            config.build_settings['EXPANDED_CODE_SIGN_IDENTITY'] = ""
            config.build_settings['CODE_SIGNING_REQUIRED'] = "NO"
            config.build_settings['CODE_SIGNING_ALLOWED'] = "NO"
            config.build_settings['ENABLE_BITCODE'] = "NO"
            config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = "13.0"
            #Fix Xcode15 other links  flag  -ld64
            xcode_version = `xcrun xcodebuild -version | grep Xcode | cut -d' ' -f2`.to_f
            if xcode_version >= 15
              xcconfig_path = config.base_configuration_reference.real_path
              xcconfig = File.read(xcconfig_path)
              if xcconfig.include?("OTHER_LDFLAGS") == false
                xcconfig = xcconfig + "\n" + 'OTHER_LDFLAGS = $(inherited) "-ld64"'
              else
                if xcconfig.include?("OTHER_LDFLAGS = $(inherited)") == false
                  xcconfig = xcconfig.sub("OTHER_LDFLAGS", "OTHER_LDFLAGS = $(inherited)")
                end
                if xcconfig.include?("-ld64") == false
                  xcconfig = xcconfig.sub("OTHER_LDFLAGS = $(inherited)", 'OTHER_LDFLAGS = $(inherited) "-ld64"')
                end
              end
              File.open(xcconfig_path, "w") { |file| file << xcconfig }
            end
        end
    end
end
```


【Objective-C】
``` bash
# Uncomment the next line to define a global platform for your project
# ...
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '13.0'
# Prevent `*.xcassets` in TUIKit from conflicting with your project
install! 'cocoapods', :disable_input_output_paths => true

# Replace `your_project_name` with your actual project name
target 'your_project_name' do
  # Comment the next line if you don't want to use dynamic frameworks
  # TUIKit components are dependent on static libraries. Therefore, you need to mask the configuration.
  # use_frameworks!

  # Enable modular headers as needed. Only after you enable modular headers, the Pod module can be imported using @import.
  # use_modular_headers!

  # Integrate the chat feature
  pod 'TUIChat/UI_Minimalist' 
  # Integrate the conversation list feature
  pod 'TUIConversation/UI_Minimalist'
  # Integrate the relationship chain feature
  pod 'TUIContact/UI_Minimalist'
  # Integrate the search feature (To use this feature, you need to purchase the  Pro edition 、Pro Plus edition or Enterprise edition)
  pod 'TUISearch/UI_Minimalist' 
  # Integrate the audio/video call feature
  pod 'TUICallKit_Swift'
  # Integrate Translation Plugin, supported starting from version 7.2 (Value-added feature activation required, please contact Tencent Cloud Business to activate)
  pod 'TUITranslationPlugin'  
  # Integrate Session Tagging Plugin, supported starting from version 7.3
  pod 'TUIConversationMarkPlugin'
  # Integrate Speech-to-Text Plugin, supported starting from version 7.5
  pod 'TUIVoiceToTextPlugin'
  # Integrate message push plugin, supported starting from version 7.6
  pod 'TIMPush'
end

#Pods config
post_install do |installer|
    installer.pods_project.targets.each do |target|
        target.build_configurations.each do |config|                
            #Fix Xcode14 Bundle target error
            config.build_settings['EXPANDED_CODE_SIGN_IDENTITY'] = ""
            config.build_settings['CODE_SIGNING_REQUIRED'] = "NO"
            config.build_settings['CODE_SIGNING_ALLOWED'] = "NO"
            config.build_settings['ENABLE_BITCODE'] = "NO"
            config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = "13.0"
            #Fix Xcode15 other links  flag  -ld64
            xcode_version = `xcrun xcodebuild -version | grep Xcode | cut -d' ' -f2`.to_f
            if xcode_version >= 15
              xcconfig_path = config.base_configuration_reference.real_path
              xcconfig = File.read(xcconfig_path)
              if xcconfig.include?("OTHER_LDFLAGS") == false
                xcconfig = xcconfig + "\n" + 'OTHER_LDFLAGS = $(inherited) "-ld64"'
              else
                if xcconfig.include?("OTHER_LDFLAGS = $(inherited)") == false
                  xcconfig = xcconfig.sub("OTHER_LDFLAGS", "OTHER_LDFLAGS = $(inherited)")
                end
                if xcconfig.include?("-ld64") == false
                  xcconfig = xcconfig.sub("OTHER_LDFLAGS = $(inherited)", 'OTHER_LDFLAGS = $(inherited) "-ld64"')
                end
              end
              File.open(xcconfig_path, "w") { |file| file << xcconfig }
            end
        end
    end
end
```

【Classic version】




【Swift】
``` bash
# Uncomment the next line to define a global platform for your project
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '13.0'
# Prevent `*.xcassets` in TUIKit from conflicting with your project
install! 'cocoapods', :disable_input_output_paths => true

# Replace `your_project_name` with your actual project name
target 'your_project_name' do
  # Comment the next line if you don't want to use dynamic frameworks
  use_frameworks!
  use_modular_headers!

  # Integrate the chat feature
  pod 'TUIChat_Swift/UI_Classic' 
  # Integrate the conversation list feature
  pod 'TUIConversation_Swift/UI_Classic'
  # Integrate the relationship chain feature
  pod 'TUIContact_Swift/UI_Classic'
  # Integrate the search feature (To use this feature, you need to purchase the  Pro edition 、Pro Plus edition or Enterprise edition)
  pod 'TUISearch_Swift/UI_Classic' 
  # Integrate the audio/video call feature
  pod 'TUICallKit_Swift'
  # Integrate Voting Plugin
  pod 'TUIPollPlugin_Swift'
  # Integrate Group Chain Plugin
  pod 'TUIGroupNotePlugin_Swift'
  # Integrate Translation Plugin (Value-added feature activation required, please contact Tencent Cloud Business to activate)
  pod 'TUITranslationPlugin_Swift'  
  # Integrate Session Grouping Plugin
  pod 'TUIConversationGroupPlugin_Swift'
  # Integrate Session Tagging Plugin
  pod 'TUIConversationMarkPlugin_Swift'
  # Integrate Speech-to-Text Plugin
  pod 'TUIVoiceToTextPlugin_Swift'
  # Integrate Customer Service Plugin
  pod 'TUICustomerServicePlugin_Swift'

end

#Pods config
post_install do |installer|
    installer.pods_project.targets.each do |target|
        target.build_configurations.each do |config|                
            #Fix Xcode14 Bundle target error
            config.build_settings['EXPANDED_CODE_SIGN_IDENTITY'] = ""
            config.build_settings['CODE_SIGNING_REQUIRED'] = "NO"
            config.build_settings['CODE_SIGNING_ALLOWED'] = "NO"
            config.build_settings['ENABLE_BITCODE'] = "NO"
            config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = "13.0"
            #Fix Xcode15 other links  flag  -ld64
            xcode_version = `xcrun xcodebuild -version | grep Xcode | cut -d' ' -f2`.to_f
            if xcode_version >= 15
              xcconfig_path = config.base_configuration_reference.real_path
              xcconfig = File.read(xcconfig_path)
              if xcconfig.include?("OTHER_LDFLAGS") == false
                xcconfig = xcconfig + "\n" + 'OTHER_LDFLAGS = $(inherited) "-ld64"'
              else
                if xcconfig.include?("OTHER_LDFLAGS = $(inherited)") == false
                  xcconfig = xcconfig.sub("OTHER_LDFLAGS", "OTHER_LDFLAGS = $(inherited)")
                end
                if xcconfig.include?("-ld64") == false
                  xcconfig = xcconfig.sub("OTHER_LDFLAGS = $(inherited)", 'OTHER_LDFLAGS = $(inherited) "-ld64"')
                end
              end
              File.open(xcconfig_path, "w") { |file| file << xcconfig }
            end
        end
    end
end
```


【Objective-C】
``` bash
# Uncomment the next line to define a global platform for your project
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '13.0'
# Prevent `*.xcassets` in TUIKit from conflicting with your project
install! 'cocoapods', :disable_input_output_paths => true

# Replace `your_project_name` with your actual project name
target 'your_project_name' do
  # Comment the next line if you don't want to use dynamic frameworks
  # TUIKit components are dependent on static libraries. Therefore, you need to mask the configuration.
  # use_frameworks!

  # Enable modular headers as needed. Only after you enable modular headers, the Pod module can be imported using @import.
  # use_modular_headers!

  # Integrate the chat feature
  pod 'TUIChat/UI_Classic' 
  # Integrate the conversation list feature
  pod 'TUIConversation/UI_Classic'
  # Integrate the relationship chain feature
  pod 'TUIContact/UI_Classic'
  # Integrate the search feature (To use this feature, you need to purchase the  Pro edition 、Pro Plus edition or Enterprise edition)
  pod 'TUISearch/UI_Classic' 
  # Integrate the audio/video call feature
  pod 'TUICallKit_Swift'
  # Integrate Voting Plugin, supported starting from version 7.1
  pod 'TUIPollPlugin'
  # Integrate Group Chain Plugin, supported starting from version 7.1
  pod 'TUIGroupNotePlugin'
  # Integrate Translation Plugin, supported starting from version 7.2 (Value-added feature activation required, please contact Tencent Cloud Business to activate)
  pod 'TUITranslationPlugin'  
  # Integrate Session Grouping Plugin, supported starting from version 7.3
  pod 'TUIConversationGroupPlugin'
  # Integrate Session Tagging Plugin, supported starting from version 7.3
  pod 'TUIConversationMarkPlugin'
  # Integrate Speech-to-Text Plugin, supported starting from version 7.5
  pod 'TUIVoiceToTextPlugin'
  # Integrate Customer Service Plugin, supported starting from version 7.6
  pod 'TUICustomerServicePlugin'
  # Integrate message push plugin, supported starting from version 7.6
  pod 'TIMPush'

end

#Pods config
post_install do |installer|
    installer.pods_project.targets.each do |target|
        target.build_configurations.each do |config|                
            #Fix Xcode14 Bundle target error
            config.build_settings['EXPANDED_CODE_SIGN_IDENTITY'] = ""
            config.build_settings['CODE_SIGNING_REQUIRED'] = "NO"
            config.build_settings['CODE_SIGNING_ALLOWED'] = "NO"
            config.build_settings['ENABLE_BITCODE'] = "NO"
            config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = "13.0"
            #Fix Xcode15 other links  flag  -ld64
            xcode_version = `xcrun xcodebuild -version | grep Xcode | cut -d' ' -f2`.to_f
            if xcode_version >= 15
              xcconfig_path = config.base_configuration_reference.real_path
              xcconfig = File.read(xcconfig_path)
              if xcconfig.include?("OTHER_LDFLAGS") == false
                xcconfig = xcconfig + "\n" + 'OTHER_LDFLAGS = $(inherited) "-ld64"'
              else
                if xcconfig.include?("OTHER_LDFLAGS = $(inherited)") == false
                  xcconfig = xcconfig.sub("OTHER_LDFLAGS", "OTHER_LDFLAGS = $(inherited)")
                end
                if xcconfig.include?("-ld64") == false
                  xcconfig = xcconfig.sub("OTHER_LDFLAGS = $(inherited)", 'OTHER_LDFLAGS = $(inherited) "-ld64"')
                end
              end
              File.open(xcconfig_path, "w") { |file| file << xcconfig }
            end
        end
    end
end
```



> **Indication**
> 
> 1. If you directly use `pod 'TUIChat'` without specifying classic or minimalist, it will integrate both UI component versions by default. 
> 2. The Classic and Minimalist UI cannot be mixed. When integrating multiple components, you must choose classic UI or minimalist UI at the same time. For instance, the Classic TUIChat component must be used with the Classic versions of the TUIConversation, TUIContact, and TUIGroup. Similarly, the Minimalist version of the TUIChat component must be paired with the Minimalist versions of the TUIConversation, TUIContact.
> 3. If you are using Swift, please enable `use_modular_headers!`, and change the header file reference to @import reference.


After modifying the Podfile, run the following command to install TUIKit.
``` bash
pod install
```

If you cannot install the latest version of TUIKit, run the following command to update the local CocoaPods repository.
``` bash
pod repo update
```

Then run the following command to update the Pod version of the component.
``` bash
pod update
```

After all TUIKit components are integrated, the project structure is as follows:

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/f5fc0f6f12a211efa09b525400762795.png)


> **Note:**
> 

> If you encounter any errors in the process, you can refer to the FAQs at the end of the document.
> 


### Local DevelopmentPods
1. Download TUIKit source code from GitHub. Drag it directly into your project directory: 

  1. [Swift TUIKit in Github](https://github.com/Tencent-RTC/Chat_UIKit/tree/main/Swift/TUIKit):

      ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027639409/aeb85ab63b9d11f0b0ce5254007c27c5.png)

  2. [Objective-C TUIKit in Github](https://github.com/TencentCloud/chat-uikit-ios/tree/main/TUIKit):

      ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/548ce77e129d11efa2935254005ac0ca.png)

2. Modify the local path of each component in your Podfile. The path is the location of the TUIKit folder relative to your project's Podfile, commonly including:

  - The TUIKit folder is located in the **parent directory** of your project's Podfile: `pod 'TUICore', :path => "../TUIKit/TUICore"`

  - The TUIKit folder is located in the **current directory** of your project's Podfile: `pod 'TUICore', :path => "./TUIKit/TUICore"`

  - The TUIKit folder is located in the **subdirectory** of your project's Podfile: ` pod 'TUICore', :path => "/TUIKit/TUICore"`


      Taking the TUIKit folder located in the parent directory of your project's Podfile as an example:


      

【DevelopmentPodfile】




【Swift】
``` bash
ment# Uncomment the next line to define a global platform for your project
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '13.0'
install! 'cocoapods', :disable_input_output_paths => true

# Replace `your_project_name` with your actual project name
target 'your_project_name' do
  # Uncomment the next line if you're using Swift or would like to use dynamic frameworks
  use_frameworks!
  use_modular_headers!

  # Integrate the basic library (required)
  pod 'TUICore', :path => "../TUIKit/TUICore"
  pod 'TIMCommon_Swift', :path => "../TUIKit/TIMCommon"
  
  # Integrate TUIKit components (optional)
  # Integrate the chat feature
  pod 'TUIChat_Swift', :path => "../TUIKit/TUIChat"
  # Integrate the conversation list feature
  pod 'TUIConversation_Swift', :path => "../TUIKit/TUIConversation"
  # Integrate the relationship chain feature
  pod 'TUIContact_Swift', :path => "../TUIKit/TUIContact"
  # Integrate the search feature (To use this feature, you need to purchase the Ultimate edition)
  pod 'TUISearch_Swift', :path => "../TUIKit/TUISearch"
  # Integrate the audio/video call feature
  pod 'TUICallKit_Swift'
  
  # Integrate the TUIKitPlugin plugin (optional)
  # Integrate translation plugin (Value-added feature activation is required. Please contact Tencent Cloud sales)
  pod 'TUITranslationPlugin_Swift'
  
  # Other Pods
  pod 'MJRefresh'
  pod 'SnapKit'
end
#Pods config
post_install do |installer|
    installer.pods_project.targets.each do |target|
        target.build_configurations.each do |config|                
            #Fix Xcode14 Bundle target error
            config.build_settings['EXPANDED_CODE_SIGN_IDENTITY'] = ""
            config.build_settings['CODE_SIGNING_REQUIRED'] = "NO"
            config.build_settings['CODE_SIGNING_ALLOWED'] = "NO"
            config.build_settings['ENABLE_BITCODE'] = "NO"
            config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = "13.0"
            #Fix Xcode15 other links  flag  -ld64
            xcode_version = `xcrun xcodebuild -version | grep Xcode | cut -d' ' -f2`.to_f
            if xcode_version >= 15
              xcconfig_path = config.base_configuration_reference.real_path
              xcconfig = File.read(xcconfig_path)
              if xcconfig.include?("OTHER_LDFLAGS") == false
                xcconfig = xcconfig + "\n" + 'OTHER_LDFLAGS = $(inherited) "-ld64"'
              else
                if xcconfig.include?("OTHER_LDFLAGS = $(inherited)") == false
                  xcconfig = xcconfig.sub("OTHER_LDFLAGS", "OTHER_LDFLAGS = $(inherited)")
                end
                if xcconfig.include?("-ld64") == false
                  xcconfig = xcconfig.sub("OTHER_LDFLAGS = $(inherited)", 'OTHER_LDFLAGS = $(inherited) "-ld64"')
                end
              end
              File.open(xcconfig_path, "w") { |file| file << xcconfig }
            end
        end
    end
end
```


【Objective-C】
``` bash
ment# Uncomment the next line to define a global platform for your project
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '13.0'
install! 'cocoapods', :disable_input_output_paths => true

# Replace `your_project_name` with your actual project name
target 'your_project_name' do
  # Uncomment the next line if you're using Swift or would like to use dynamic frameworks
  use_frameworks!
  use_modular_headers!

  # Integrate the basic library (required)
  pod 'TUICore', :path => "../TUIKit/TUICore"
  pod 'TIMCommon', :path => "../TUIKit/TIMCommon"
  
  # Integrate TUIKit components (optional)
  # Integrate the chat feature
  pod 'TUIChat', :path => "../TUIKit/TUIChat"
  # Integrate the conversation list feature
  pod 'TUIConversation', :path => "../TUIKit/TUIConversation"
  # Integrate the relationship chain feature
  pod 'TUIContact', :path => "../TUIKit/TUIContact"
  # Integrate the search feature (To use this feature, you need to purchase the Ultimate edition)
  pod 'TUISearch', :path => "../TUIKit/TUISearch"
  # Integrate the audio/video call feature
  pod 'TUICallKit_Swift'
  # Integrate the video conference feature
  pod 'TUIRoomKit'
  
  # Integrate the TUIKitPlugin plugin (optional)
  # Note: The TUIKitPlugin plugin version must be the same as the TUICore version.
  # Ensure that the plugin version matches spec.version in "../TUIKit/TUICore/TUICore.spec".
  
  # Integrate the voting plugin, supported from version 7.1
  pod 'TUIPollPlugin'
  # Integrate the group chain plugin, supported from version 7.1
  pod 'TUIGroupNotePlugin'
  # Integrate translation plugin, supported from version 7.2 (Value-added feature activation is required. Please contact Tencent Cloud sales)
  pod 'TUITranslationPlugin'
  # Integrate the session grouping plugin, supported from version 7.3
  pod 'TUIConversationGroupPlugin'
  # Integrate the session tagging plugin, supported from version 7.3
  pod 'TUIConversationMarkPlugin'
  # Integrate the offline push feature
  pod 'TIMPush'
  
  # Other Pods
  pod 'MJRefresh'
  pod 'Masonry'
end
#Pods config
post_install do |installer|
    installer.pods_project.targets.each do |target|
        target.build_configurations.each do |config|                
            #Fix Xcode14 Bundle target error
            config.build_settings['EXPANDED_CODE_SIGN_IDENTITY'] = ""
            config.build_settings['CODE_SIGNING_REQUIRED'] = "NO"
            config.build_settings['CODE_SIGNING_ALLOWED'] = "NO"
            config.build_settings['ENABLE_BITCODE'] = "NO"
            config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = "13.0"
            #Fix Xcode15 other links  flag  -ld64
            xcode_version = `xcrun xcodebuild -version | grep Xcode | cut -d' ' -f2`.to_f
            if xcode_version >= 15
              xcconfig_path = config.base_configuration_reference.real_path
              xcconfig = File.read(xcconfig_path)
              if xcconfig.include?("OTHER_LDFLAGS") == false
                xcconfig = xcconfig + "\n" + 'OTHER_LDFLAGS = $(inherited) "-ld64"'
              else
                if xcconfig.include?("OTHER_LDFLAGS = $(inherited)") == false
                  xcconfig = xcconfig.sub("OTHER_LDFLAGS", "OTHER_LDFLAGS = $(inherited)")
                end
                if xcconfig.include?("-ld64") == false
                  xcconfig = xcconfig.sub("OTHER_LDFLAGS = $(inherited)", 'OTHER_LDFLAGS = $(inherited) "-ld64"')
                end
              end
              File.open(xcconfig_path, "w") { |file| file << xcconfig }
            end
        end
    end
end
```

3. After modifying the Podfile, run the following command to install the local TUIKit components. Example:

   ``` bash
   pod install
   ```   

   > **Note:**
   > 
>   4. When using the local integration solution, if you need to upgrade, you must obtain the latest souce code from Github and overwrite the TUIKit directory in your local project.
>   5. When private modifications conflict with the remote version, manual merging is required to resolve conflicts.
>   6. The TUIKit plugin relies on the version of TUICore, so please ensure that the plugin version matches the spec.version in "../TUIKit/TUICore/TUICore.spec".


## Third-party Library Dependencies

The minimum version requirements for third-party libraries depended on by TUIKit are as follows. If your version is lower, please upgrade to the latest version.




【Swift】
``` plaintext
- MJExtension (3.4.1)
- MJRefresh (3.7.5)
- SnapKit (5.7.1)
- SSZipArchive (2.4.3)
- SDWebImage (5.18.11)
```


【Objective-C】
``` plaintext
- Masonry (1.1.0)
- MJExtension (3.4.1)
- MJRefresh (3.7.5)
- ReactiveObjC (3.1.1)
- SDWebImage (5.18.11):
  - SDWebImage/Core (= 5.18.11)
- SDWebImage/Core (5.18.11)
- SnapKit (5.6.0)
- SSZipArchive (2.4.3)
```

## Build Basic Interfaces

After integrating TUIKit, if you want to continue building basic interfaces for chat, conversation list, etc., please refer to the document: [Build Chat](https://www.tencentcloud.com/document/product/1047/61215), [Build Conversation List.](https://www.tencentcloud.com/document/product/1047/61217)

## FAQs

### Xcode Issues
- **Integration error: [Xcodeproj] Unknown object version (60). (RuntimeError)**

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/8c79531de10611eeb1eb525400b5f95f.png)


   When integrating TUIKit in a new project created with Xcode15 and entering `pod install`, you may encounter this issue due to using an older version of CocoaPods. There are two solutions:


   Solution 1: Change the Xcode project's `Project Format` version to Xcode13.0.

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/391e61fb12a211efa2935254005ac0ca.png)


   Solution 2: Upgrade your local version of CocoaPods. The upgrade method will not be elaborated here.

- **Assertion failed: (false && "compact unwind compressed function offset doesn't fit in 24 bits"), function operator(), file Layout.cpp.**

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/8c7cc874e10611ee9f745254008eb8a8.png)


   Or, when integrating TUIRoom with XCode15, the latest linker causes symbol conflicts in TUIRoomEngine, which is also part of this issue.

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/8c7853f5e10611eeb1eb525400b5f95f.png)


   Solution: Modify the linker configuration. In `Build Settings`, add `-ld64` to `Other Linker Flags`.


   Official Documentation: [https://developer.apple.com/forums/thread/735426](https://links.jianshu.com/go?to=https%3A%2F%2Fdeveloper.apple.com%2Fforums%2Fthread%2F735426)

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/8c6dc1f8e10611eeb419525400ea3514.png)

- **Rosetta Simulator Issue**


   When using Apple Silicon (M1, M2, etc. series chips), you'll encounter this type of popup. The reason is that some third-party libraries, including SDWebImage, do not support xcframework. However, Apple has still provided an adaptation method, which is to enable Rosetta settings on the emulator. Generally, the Rosetta option will automatically pop up during compilation.

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/8cd073eae10611eeb419525400ea3514.png)

- **Xcode 15 Developer Sandbox Option Error: Sandbox: bash(xxx) deny(1) file-write-create**

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/8c61b3dee10611ee9f745254008eb8a8.png)


   When you create a new project using Xcode 15, this option may cause compilation and execution failure. It is recommended that you turn off this option.

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/8c75e297e10611eeb419525400ea3514.png)

- **Xcode 16 does not support enabling bitcode for Frameworks**


   **Solution 1: Upgrade the SDK**


   If you are using an old version SDK with Bitcode (e.g., TXIMSDK_iOS), it is recommended to follow this document and upgrade the SDK to TXIMSDK_Plus_iOS_XCFramework.


   **Solution 2: Modify the Podfile**


   Add the following configuration to the end of your Podfile and run pod install again.

   ``` java
   post_install do |installer|
     bitcode_strip_path = 'xcrun --find bitcode_strip'.chop!
     def strip_bitcode_from_framework(bitcode_strip_path, framework_relative_path)
       framework_path = File.join(Dir.pwd, framework_relative_path)
       command = "#{bitcode_strip_path} #{framework_path} -r -o #{framework_path}"
       puts "Stripping bitcode: #{command}"
       system(command)
     end
     framework_paths = [
       "/Pods/TXIMSDK_iOS/ImSDK.framework/ImSDK",
     ]
     framework_paths.each do |framework_relative_path|
       strip_bitcode_from_framework(bitcode_strip_path, framework_relative_path)
      end
   end
   ```

### CocoaPods Issues
- **When using remote integration, issues with mismatched Pod dependency versions**


   If you encounter a mismatch between the Podfile.lock and the plugin dependency version of TUICore while using remote CocoaPods integration, 


   please delete the Podfile.lock file and use `pod repo update`to update your local repository, then use `pod update` to refresh the updates.

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/8c51cf32e10611eeb1eb525400b5f95f.png)

- **When using local integration, issues with mismatched Pod dependency versions**


   When integrating local DevelopmentPods and the plugin dependency on TUICoreis newer, but the local Pod dependency version is 1.0.0,


   Please refer to [Podfile_local](https://github.com/TencentCloud/chat-uikit-ios/blob/main/Demo/Podfile_local) and [TUICore.spec](https://github.com/TencentCloud/chat-uikit-ios/blob/main/TUIKit/TUICore/TUICore.podspec) for modifications. The plugin needs to follow the version and match the one in TUICore.spec.


   When using local integration for the first time, we recommend you download our sample Demo project, replace the content of the Podfile with Podfile_local, and execute `Pod update` for cross-reference.

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/8c974171e10611ee9ca3525400bb593a.png)


### Submission Issues
- **Packaging failure when launching on the Appstore, with an 'Unsupported Architectures' error message.**


   The issue is illustrated below, where packaging indicates the ImSDK_Plus.framework includes an x86_64 simulator version not supported by the Appstore. This is because the SDK, to facilitate developer debugging, defaults to including the simulator version upon release.

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027639409/d51c312e249f11ef9bc3525400456a87.png)


   You can follow the steps below to remove the simulator version during packaging:

  1. Select your project's Target and click on the `Build Phases` option, then add a `Run Script` to the current panel;

      ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027639409/d522307f249f11efa45a5254008fe934.png)

  2. In the newly added Run Script, insert the following script:

      ``` bash
      #!/bin/sh
      
      # Strip invalid architectures
      strip_invalid_archs() {
          binary="$1"
          echo "current binary ${binary}"
          # Get architectures for current file
          archs="$(lipo -info "$binary" | rev | cut -d ':' -f1 | rev)"
          stripped=""
          for arch in $archs; do
              if ! [[ "${ARCHS}" == *"$arch"* ]]; then
                  if [ -f "$binary" ]; then
                      # Strip non-valid architectures in-place
                      lipo -remove "$arch" -output "$binary" "$binary" || exit 1
                      stripped="$stripped $arch"
                  fi
              fi
          done
          if [[ "$stripped" ]]; then
              echo "Stripped $binary of architectures:$stripped"
          fi
      }
      
      APP_PATH="${TARGET_BUILD_DIR}/${WRAPPER_NAME}"
      
      # This script loops through the frameworks embedded in the application and
      # removes unused architectures.
      find "$APP_PATH" -name '*.framework' -type d | while read -r FRAMEWORK
      do
          FRAMEWORK_EXECUTABLE_NAME=$(defaults read "$FRAMEWORK/Info.plist" CFBundleExecutable)
          FRAMEWORK_EXECUTABLE_PATH="$FRAMEWORK/$FRAMEWORK_EXECUTABLE_NAME"
          echo "Executable is $FRAMEWORK_EXECUTABLE_PATH"
          strip_invalid_archs "$FRAMEWORK_EXECUTABLE_PATH"
      done
      ```
      ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027639409/d538ac11249f11ef9dd5525400441de3.png)


### TUICallKit Issues
- **What should I do if TUICallKit conflicts with an audio/video library that I have integrated?**


   Tencent Cloud's audio and video libraries cannot be integrated simultaneously due to possible symbol conflicts. These can be addressed as follows.

  1. If you have integrated the `TXLiteAVSDK_TRTC` library, a symbol conflict will not occur. You can directly add the dependency in Podfile:

      ``` ruby
      pod 'TUICallKit_Swift'  
      ```
  2. If you have integrated the `TXLiteAVSDK_Professional` library, a symbol conflict will occur. You can add the dependency in Podfile:

      ``` ruby
        pod 'TUICallKit_Swift/Professional'
      ```
  3. If you have integrated the `TXLiteAVSDK_Enterprise` library, a symbol conflict will occur. It is recommended to upgrade to `TXLiteAVSDK_Professional` and then use TUICallKit_Swift/Professional.

- **How long is the default duration for call invitation timeouts?**


   The default timeout duration for a call invitation is 30 seconds.

- **During the invitation timeout period, can the invitee immediately receive the invitation if they go offline and then online?**


   1.If the call invitation is started in a one-to-one chat, the invitee can receive the call invitation, and the TUIKit will automatically open the call invitation UI internally.


   2.If the call invitation is for a group chat, the invitee will automatically fetch invitations from the last 30 seconds upon going online again, and the TUIKit will automatically trigger the group call interface.3.


## Contact Us

If you have any questions about this article, feel free to join the [Telegram Technical Group](https://t.me/+EPk6TMZEZMM5OGY1), where you will receive reliable technical support.

