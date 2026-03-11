> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本文将介绍如何集成 `TUIKit` 组件。 

> **说明：**
> 
> 1. 从 5.7.1435 版本开始，TUIKit 支持模块化集成，支持了经典版 UI，您可以根据自己的需求集成所需模块。
> 2. 从 6.9.3557 版本开始，TUIKit 新增了全新的简约版 UI。
> 3. 为了尊重版权，IM Demo/TUIKit 工程中默认不包含大表情元素切图。正式上线商用前请您替换为自己设计或拥有版权的其他表情包。下图所示默认的**小黄脸表情包版权归腾讯云所有**，可有偿授权使用，如需获得授权可您可以通过升级至 [IM 企业版套餐](https://buy.cloud.tencent.com/avc) 免费使用该表情包。

> ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027937867/00f495e4391911efbec9525400a9236a.png)
> 


您可以根据需求自由选择经典版或简约版 UI 组件。如果您还不了解各个界面库的功能，可以查阅文档 [TUIKit 界面库介绍](https://cloud.tencent.com/document/product/269/37190)。

## 开发环境要求
- Xcode 10 及以上

- iOS 9.0 及以上


## CocoaPods 集成
1. 安装 CocoaPods。
在终端窗口中输入如下命令（需要提前在 Mac 中安装 Ruby 环境）：

   ``` bash
   sudo gem install cocoapods
   ```
2. 创建 Podfile 文件。
进入项目所在路径输入以下命令行，之后项目路径下会出现一个 Podfile 文件。

   ``` bash
   pod init
   ```
3. 根据业务需求在 Podfile 中添加对应的 TUIKit 组件。组件之间相互独立，添加或删除均不影响工程编译。您可以按需选择不同的 Podfile 集成方式：

  - 远程 CocoaPods 集成。

  - DevelopmentPods 本地集成。


      以上两种集成方式的优缺点如下表所示：

<table>
<tr>
<td rowspan="1" colSpan="1" >集成方式</td>

<td rowspan="1" colSpan="1" >适合场景</td>

<td rowspan="1" colSpan="1" >优点</td>

<td rowspan="1" colSpan="1" >缺点</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >远程 CocoaPods 集成</td>

<td rowspan="1" colSpan="1" >适合无源码修改时的集成。</td>

<td rowspan="1" colSpan="1" >当 TUIKit 有版本更新时，您只需再次` Pod update `即可完成更新。</td>

<td rowspan="1" colSpan="1" >当您有源码修改，使用 `Pod update` 更新时，新版本的 TUIKit 会覆盖您的修改。</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >本地 DevelopmentPods 集成</td>

<td rowspan="1" colSpan="1" >适合有涉及源码自定义修改的客户。</td>

<td rowspan="1" colSpan="1" >当您有自己的 git 仓库时，可以跟踪修改。修改源码后，使用 `Pod update` 更新其他远程 Pod 库时，不会覆盖您的修改。</td>

<td rowspan="1" colSpan="1" >您需要手动将 TUIKit 源码覆盖您本地 TUIKit 文件夹进行更新。</td>
</tr>
</table>


### 远程 CocoaPods 集成

您可以在 Podfile 中按需添加组件库：

> **注意：**
> 

> 从 8.5.6870 版本开始，TUIKit 支持 Swift 语言组件。
> 




【经典版】




【Swift 组件】
``` bash
# Uncomment the next line to define a global platform for your project
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '13.0'
# 防止 TUIKit 组件里的 *.xcassets 与您项目里面冲突。
install! 'cocoapods', :disable_input_output_paths => true

# 请使用您的真实项目名称替换 your_project_name
target 'your_project_name' do
  use_frameworks!
  use_modular_headers!

  # 集成聊天功能
  pod 'TUIChat_Swift/UI_Classic' 
  # 集成会话功能
  pod 'TUIConversation_Swift/UI_Classic'
  # 集成关系链功能
  pod 'TUIContact_Swift/UI_Classic'
  # 集成搜索功能（需要购买旗舰版或企业版套餐）
  pod 'TUISearch_Swift/UI_Classic' 
  # 集成音视频通话功能
  pod 'TUICallKit_Swift'
  # 集成投票插件
  pod 'TUIPollPlugin_Swift'
  # 集成群接龙插件
  pod 'TUIGroupNotePlugin_Swift'
  # 集成翻译插件（需开通增值功能，请联系腾讯云商务开通）
  pod 'TUITranslationPlugin_Swift'  
  # 集成会话分组插件
  pod 'TUIConversationGroupPlugin_Swift'
  # 集成会话标记插件
  pod 'TUIConversationMarkPlugin_Swift'
  # 集成语音转文字插件
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

```


【Objective-C 组件】
``` bash
# Uncomment the next line to define a global platform for your project
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '13.0'
# 防止 TUIKit 组件里的 *.xcassets 与您项目里面冲突。
install! 'cocoapods', :disable_input_output_paths => true

# 请使用您的真实项目名称替换 your_project_name
target 'your_project_name' do
  # 从 7.1 版本开始，新增了 TUIKit 插件（TUIXXXPlugin），TUIKit 插件是动态库依赖，需要开启此设置。
  # 如果您不依赖 TUIKit 插件，该设置可以保持关闭。
  use_frameworks!
  # 请按需开启 modular headers，开启后 Pod 模块才能使用 @import 导入，简化 Swift 引用 OC 的方式。
  # use_modular_headers!

  # 集成聊天功能
  pod 'TUIChat/UI_Classic' 
  # 集成会话功能
  pod 'TUIConversation/UI_Classic'
  # 集成关系链功能
  pod 'TUIContact/UI_Classic'
  # 集成搜索功能（需要购买旗舰版或企业版套餐）
  pod 'TUISearch/UI_Classic' 
  # 集成音视频通话功能
  pod 'TUICallKit_Swift'
  # 集成快速会议
  pod 'TUIRoomKit'
  # 集成投票插件，从 7.1 版本开始支持
  pod 'TUIPollPlugin'
  # 集成群接龙插件，从 7.1 版本开始支持
  pod 'TUIGroupNotePlugin'
  # 集成翻译插件，从 7.2 版本开始支持（需开通增值功能，请联系腾讯云商务开通）
  pod 'TUITranslationPlugin'  
  # 集成会话分组插件，从 7.3 版本开始支持
  pod 'TUIConversationGroupPlugin'
  # 集成会话标记插件，从 7.3 版本开始支持
  pod 'TUIConversationMarkPlugin'
  # 集成语音转文字插件，从 7.5 版本开始支持
  pod 'TUIVoiceToTextPlugin'
  # 集成消息推送插件，从 7.6 版本开始支持
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

```

【简约版】




【Swift 组件】
``` bash
# Uncomment the next line to define a global platform for your project
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '13.0'
# 防止 TUIKit 组件里的 *.xcassets 与您项目里面冲突。
install! 'cocoapods', :disable_input_output_paths => true

# 请使用您的真实项目名称替换 your_project_name
target 'your_project_name' do
  use_frameworks!
  use_modular_headers!

  # 集成聊天功能
  pod 'TUIChat_Swift/UI_Minimalist' 
  # 集成会话功能
  pod 'TUIConversation_Swift/UI_Minimalist'
  # 集成关系链功能
  pod 'TUIContact_Swift/UI_Minimalist'
  # 集成搜索功能（需要购买旗舰版或企业版、套餐）
  pod 'TUISearch_Swift/UI_Minimalist' 
  # 集成音视频通话功能
  pod 'TUICallKit_Swift'
  # 集成翻译插件（需单独购买翻译插件）
  pod 'TUITranslationPlugin_Swift'  
  # 集成语音转文字插件
  pod 'TUIVoiceToTextPlugin_Swift'
  # 集成表情回应插件 
  pod 'TUIEmojiPlugin_Swift'
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
```


【Objective-C 组件】
``` bash
# Uncomment the next line to define a global platform for your project
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '13.0'
# 防止 TUIKit 组件里的 *.xcassets 与您项目里面冲突。
install! 'cocoapods', :disable_input_output_paths => true

# 请使用您的真实项目名称替换 your_project_name
target 'your_project_name' do
  # 从 7.1 版本开始，新增了 TUIKit 插件（TUIXXXPlugin），TUIKit 插件是动态库依赖，需要开启此设置。
  # 如果您不依赖 TUIKit 插件，该设置可以保持关闭。
  use_frameworks!
  # 请按需开启 modular headers，开启后 Pod 模块才能使用 @import 导入，简化 Swift 引用 OC 的方式。
  # use_modular_headers!

  # 集成聊天功能
  pod 'TUIChat/UI_Minimalist' 
  # 集成会话功能
  pod 'TUIConversation/UI_Minimalist'
  # 集成关系链功能
  pod 'TUIContact/UI_Minimalist'
  # 集成搜索功能（需要购买旗舰版或企业版、套餐）
  pod 'TUISearch/UI_Minimalist' 
  # 集成音视频通话功能
  pod 'TUICallKit_Swift'
  # 集成翻译插件，从 7.2 版本开始支持（需单独购买翻译插件）
  pod 'TUITranslationPlugin'  
  # 集成语音转文字插件，从 7.5 版本开始支持
  pod 'TUIVoiceToTextPlugin'
  # 集成消息推送插件，从 7.6 版本开始支持
  pod 'TIMPush'
  # 集成表情回应插件，从 7.8 版本开始支持  
  pod 'TUIEmojiPlugin'
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
```

> **说明：**
> 
> 1. 如果您直接 `pod 'TUIChat'`，不指定经典版或简约版，默认会集成两套版本 UI 组件。 
> 2. 经典版和简约版 UI 不能混用，集成多个组件时，您必须同时全部选择经典版 UI 或简约版 UI。例如，经典版 `TUIChat` 组件必须与经典版 `TUIConversation`、`TUIContact` 组件搭配使用。同理，简约版 `TUIChat` 组件必须与简约版 `TUIConversation`、`TUIContact` 组件搭配使用。
> 3. 如果您使用的是 Swift，请开启 `use_modular_headers!` ，并将头文件引用改成 @import 模块名形式引用。


Podfile 修改完毕后，执行以下命令，安装 TUIKit 组件。
``` bash
pod install
```

如果无法安装 TUIKit 最新版本，执行以下命令更新本地的 CocoaPods 仓库列表。
``` bash
pod repo update
```

之后执行以下命令，更新组件库的Pod版本。
``` bash
pod update
```

集成全部的 TUIKit 组件后的项目结构：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100031390357/0ae0e5c8eb4411eeb5dc525400aa857d.png)


> **注意：**
> 

> 若您操作遇到错误，可查阅文末的常见问题。
> 


### 本地 DevelopmentPods 源码集成
1. 从 GitHub 下载 TUIKit 源码，将 TUIKit 目录直接拖入您的工程目录下:

  - [Swift TUIKit 源码 Github 地址](https://github.com/Tencent-RTC/Chat_UIKit/tree/main/Swift/TUIKit)：

      ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027639409/69fbca623b9411f0912c52540044a08e.png)

  - [Objective-C TUIKit 源码 Github 地址](https://github.com/TencentCloud/TIMSDK/tree/master/iOS/TUIKit)：

      ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/d51053be4e1011ee84f2525400494e51.png)

2. 修改您 Podfile 中每个组件的本地路径。path 是 TUIKit 文件夹相对于您工程 Podfile 文件的位置，常见的有：

  - TUIKit 文件夹位于您工程 Podfile 文件**父目录**： `pod 'TUICore', :path => "../TUIKit/TUICore"`

  - TUIKit 文件夹位于您工程 Podfile 文件**当前目录**： `pod 'TUICore', :path => "./TUIKit/TUICore"`

  - TUIKit 文件夹位于您工程 Podfile 文件**子目录**： ` pod 'TUICore', :path => "/TUIKit/TUICore"`


      以 TUIKit 文件夹位于您工程 Podfile 文件父目录为例：


      

【DevelopmentPodfile】




【Swift 组件】
``` bash
# Uncomment the next line to define a global platform for your project
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '13.0'
install! 'cocoapods', :disable_input_output_paths => true

# 请使用您的真实项目名称替换 your_project_name
target 'your_project_name' do
  # Uncomment the next line if you're using Swift or would like to use dynamic frameworks
  use_frameworks!
  use_modular_headers!
  
  # 集成基础库（必选）
  pod 'TUICore', :path => "../TUIKit/TUICore"
  pod 'TIMCommon_Swift', :path => "../TUIKit/TIMCommon"
  # 集成TUIKit组件（可选）
  # 集成聊天功能
  pod 'TUIChat_Swift', :path => "../TUIKit/TUIChat"
  # 集成会话功能
  pod 'TUIConversation_Swift', :path => "../TUIKit/TUIConversation"
  # 集成关系链功能
  pod 'TUIContact_Swift', :path => "../TUIKit/TUIContact"
  # 集成搜索功能（需要购买旗舰版或企业版套餐）
  pod 'TUISearch_Swift', :path => "../TUIKit/TUISearch"
  
  # 集成音视频通话功能
  pod 'TUICallKit_Swift'
  
  # 集成 TUIKitPlugin 插件 （可选）
  # 集成翻译插件（需单独购买插件）
  pod 'TUITranslationPlugin_Swift'
  # 集成语音转文字插件（需单独购买插件）
  pod 'TUIVoiceToTextPlugin_Swift'

  # 其他 Pod
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
en
```


【Objective-C 组件】
``` bash
# Uncomment the next line to define a global platform for your project
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '13.0'
install! 'cocoapods', :disable_input_output_paths => true

# 请使用您的真实项目名称替换 your_project_name
target 'your_project_name' do
  # Uncomment the next line if you're using Swift or would like to use dynamic frameworks
  use_frameworks!
  use_modular_headers!
  
  # 集成基础库（必选）
  pod 'TUICore', :path => "../TUIKit/TUICore"
  pod 'TIMCommon', :path => "../TUIKit/TIMCommon"
  # 集成TUIKit组件（可选）
  # 集成聊天功能
  pod 'TUIChat', :path => "../TUIKit/TUIChat"
  # 集成会话功能
  pod 'TUIConversation', :path => "../TUIKit/TUIConversation"
  # 集成关系链功能
  pod 'TUIContact', :path => "../TUIKit/TUIContact"
  # 集成搜索功能（需要购买旗舰版或企业版套餐）
  pod 'TUISearch', :path => "../TUIKit/TUISearch"
  
  # 集成音视频通话功能
  pod 'TUICallKit_Swift'
  # 集成快速会议
  pod 'TUIRoomKit'
  
  # 集成TUIKitPlugin插件 （可选）
  # 集成翻译插件，从 7.2 版本开始支持（需单独购买翻译插件）
  pod 'TUITranslationPlugin'
  # 集成推送插件
  pod 'TIMPush'

  # 其他 Pod
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
en
```

3. Podfile 修改完毕后，执行以下命令，安装本地 TUIKit 组件。示例：

   ``` bash
   pod install
   ```   

   > **注意：**
   > 
>   1. 使用本地集成方案时，如需升级时需要从 Github 获取最新的组件代码，覆盖您本地项目的 TUIKit 目录。
>   2. 当私有化修改和远端有冲突时，需要手动合并，处理冲突。
>   3. TUIKit 插件需要依赖 TUICore 的版本，请确保插件版本和 "../TUIKit/TUICore/TUICore.spec" 中的 spec.version 一致。


## 第三方库依赖

TUIKit 依赖的第三方库的最低版本如下，如果您的版本较低，请升级到最新版本。




【Swift 组件】
``` plaintext
- MJExtension (3.4.1)
- MJRefresh (3.7.5)
- SnapKit (5.7.1)
- SSZipArchive (2.4.3)
- SDWebImage (5.18.11)
```


【Objective-C 组件】
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

## 快速搭建

常用的聊天软件都是由会话列表、聊天窗口、好友列表、音视频通话等几个基本的界面组成，参考下面步骤，您仅需几行代码即可在项目中快速搭建这些 UI 界面。

> **说明：**
> 

>  关于 TUIKit 组件模块功能：
> 
> - 实操教学（Objective-C 组件版本）视频请参见：[极速集成 TUIKit（iOS）](https://cloud.tencent.com/edu/learning/course-3130-56699)。
> - 如果想了解更多，您还可以 [下载并运行 TUIKitDemo 源码](https://cloud.tencent.com/document/product/269/68228)，内含常见功能示例。


### 步骤1：组件登录

登录组件后才能正常使用组件的功能。用户在 App 上点击登录时，您可以登录 TUIKit 组件。
SDKAppID 需要在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 创建并获取，userSig 需要按规则计算，详细步骤请参考文档 [快速入门](https://cloud.tencent.com/document/product/269/68228#.E6.93.8D.E4.BD.9C.E6.AD.A5.E9.AA.A4)。

示例代码如下所示：




【Swift】
``` swift
@objc func loginSDK(_ userID: String, userSig: String, succ: TSucc?, fail: TFail?) {
    TUILogin.login(Int32(SDKAPPID), userID: userID, userSig: userSig, config: loginConfig, succ: {
        // update UI
        succ?()
    }, fail: { code, msg in
        // update UI
        fail?(code, msg)
    })
}
```


【Objective-C】
``` objectivec
#import "TUILogin.h"

- (void)loginSDK:(NSString *)userID userSig:(NSString *)sig succ:(TSucc)succ fail:(TFail)fail {
    [TUILogin login:SDKAppID userID:userID userSig:sig succ:^{
        NSLog(@"登录成功");
    } fail:^(int code, NSString *msg) {
        NSLog(@"登录失败");
    }];
}
```

### 步骤2：构建会话列表

会话列表只需要创建 `TUIConversationListController` 对象即可。会话列表会从数据库中读取最近联系人，当用户点击联系人时，`TUIConversationListController` 将事件 `didSelectConversation` 回调给上层。

示例代码如下所示：



【经典版】




【Swift】
``` swift
// ConversationController 为您自己的 ViewController
public class ConversationController: UIViewController, V2TIMSDKListener, TUIPopViewDelegate {
    override public func viewDidLoad() {
        super.viewDidLoad()
        setupNavigation()

        conv = TUIConversationListController()
        if let conv = conv {
            addChild(conv)
            view.addSubview(conv.view)
        }
    }
}
// 会话列表点击事件，可自定义，通常是打开聊天界面
public protocol TUIConversationListControllerListener: AnyObject {
    func conversationListController(_ conversationController: UIViewController, didSelectConversation conversation: TUIConversationCellData) -> Bool
}
```


【Objective-C】
``` objectivec
#import "TUIConversationListController.h"

// ConversationController 为您自己的 ViewController
@implementation ConversationController 
- (void)viewDidLoad {
    [super viewDidLoad];
    // TUIConversationListController
    TUIConversationListController *vc = [[TUIConversationListController alloc] init];
    vc.delegate = self;
    // 把 TUIConversationListController 添加到自己的 ViewController
    [self addChildViewController:vc];
    [self.view addSubview:vc.view];
}

- (void)conversationListController:(UIViewController *)conversationController 
             didSelectConversation:(TUIConversationCellData *)conversation {
    // 会话列表点击事件，可自定义，通常是打开聊天界面
}
@end
```

【简约版】




【Swift】
``` swift
// ConversationController 为您自己的 ViewController
public class ConversationController: UIViewController, V2TIMSDKListener, TUIPopViewDelegate {
    override public func viewDidLoad() {
        super.viewDidLoad()
        setupNavigation()

        conv = TUIConversationListController_Minimalist()
        if let conv = conv {
            addChild(conv)
            view.addSubview(conv.view)
        }
    }
}
// 会话列表点击事件，可自定义，通常是打开聊天界面
public protocol TUIConversationListControllerListener: AnyObject {
    func conversationListController(_ conversationController: UIViewController, didSelectConversation conversation: TUIConversationCellData) -> Bool
}
```


【Objective-C】
``` objectivec
#import "TUIConversationListController_Minimalist.h"

// ConversationController 为您自己的 ViewController
@implementation ConversationController
- (void)viewDidLoad {
    [super viewDidLoad];
    // TUIConversationListController_Minimalist
    TUIConversationListController_Minimalist *vc = [[TUIConversationListController_Minimalist alloc] init];
    vc.delegate = self;
    // 把 TUIConversationListController_Minimalist 添加到自己的 ViewController
    [self addChildViewController:vc];
    [self.view addSubview:vc.view];
}

- (void)conversationListController:(TUIConversationListController_Minimalist *)conversationController 
            didSelectConversation:(TUIConversationCell *)conversation
{
    // 会话列表点击事件，通常是打开聊天界面
}
@end
```

### 步骤3：构建聊天窗口

初始化聊天界面时，需要上层传入当前聊天界面对应的会话信息。

示例代码如下所示：



【经典版】




【Swift】
``` swift
let conversationData = TUIChatConversationModel()
conversationData.userID = userID ?? ""
conversationData.groupID = groupID ?? ""
if let chatVC = getChatViewController(conversationData) {
    navigationController?.pushViewController(chatVC, animated: true)
}

private func getChatViewController(_ model: TUIChatConversationModel) -> TUIBaseChatViewController? {
    var chat: TUIBaseChatViewController?
    if let userID = model.userID, !userID.isEmpty {
        chat = TUIC2CChatViewController()
    } else if let groupID = model.groupID, !groupID.isEmpty {
        chat = TUIGroupChatViewController()
    }
    chat?.conversationData = model
    return chat
}
```


【Objective-C】
``` objectivec
#import "TUIC2CChatViewController.h"

// ChatViewController 为您自己的 ViewController
@implementation ChatViewController
- (void)viewDidLoad {
  // 创建会话信息
  TUIChatConversationModel *data = [[TUIChatConversationModel alloc] init];
  data.userID = @"userID";    
  // TUIC2CChatViewController
  TUIC2CChatViewController *vc = [[TUIC2CChatViewController alloc] init];  
  [vc setConversationData:data];
  // 把 TUIC2CChatViewController 添加到自己的 ViewController
  [self addChildViewController:vc];
  [self.view addSubview:vc.view];
}
@end
```

> **说明：**
> 

> `TUIC2CChatViewController` 会自动拉取该用户的历史消息并展示出来。
> 


【简约版】




【Swift】
``` swift
let conversationData = TUIChatConversationModel()
conversationData.userID = userID ?? ""
conversationData.groupID = groupID ?? ""
if let chatVC = getChatViewController(conversationData) {
    navigationController?.pushViewController(chatVC, animated: true)
}

private func getChatViewController(_ model: TUIChatConversationModel) -> TUIBaseChatViewController_Minimalist? {
    var chat: TUIBaseChatViewController_Minimalist?
    if let userID = model.userID, !userID.isEmpty {
        chat = TUIC2CChatViewController_Minimalist()
    } else if let groupID = model.groupID, !groupID.isEmpty {
        chat = TUIGroupChatViewController_Minimalist()
    }
    chat?.conversationData = model
    return chat
}
```


【Objective-C】
``` objectivec
#import "TUIC2CChatViewController_Minimalist.h"

// ChatViewController 为您自己的 ViewController
@implementation ChatViewController
- (void)viewDidLoad {
  // 创建会话信息
  TUIChatConversationModel *data = [[TUIChatConversationModel alloc] init];
  data.userID = @"userID";    
  // 创建 TUIC2CChatViewController_Minimalist
  TUIC2CChatViewController_Minimalist *vc = [[TUIC2CChatViewController_Minimalist alloc] init];  
  [vc setConversationData:data];
  // 把 TUIC2CChatViewController 添加到自己的 ViewController
  [self addChildViewController:vc];
  [self.view addSubview:vc.view];
}
@end
```

> **说明**
> 

> `TUIC2CChatViewController_Minimalist` 会自动拉取该用户的历史消息并展示出来。
> 


### 步骤4：构建通讯录界面

通讯录界面不需要其它依赖，只需创建对象并显示出来即可。



【经典版】




【Swift】
``` swift
// ContactController 为您自己的 ViewController
public class ContactsController: UIViewController, TUIPopViewDelegate {
    override public func viewDidLoad() {
        super.viewDidLoad()

        contactVC = TUIContactController()
        if let contactVC = contactVC {
            addChild(contactVC)
            view.addSubview(contactVC.view)
        }
    }
}
```


【Objective-C】
``` objectivec
#import "TUIContactController.h"

// ContactController 为您自己的 ViewController
@implementation ContactController
- (void)viewDidLoad {    
  // 创建 TUIContactController
  TUIContactController *vc = [[TUIContactController alloc] init];
  // 把 TUIContactController 添加到自己的 ViewController
  [self addChildViewController:vc];
  [self.view addSubview:vc.view];
}
@end
```

注意，上面代码只能将 `TUIContactController` 初始化并展示出来，其中的点击行为（例如点击好友、添加好友等），TUIKit 会通过 `TUIContactControllerListener` 抛给上层处理：




【Swift】
``` swift
protocol TUIContactControllerListener: NSObjectProtocol {
    func onSelectFriend(_ cell: TUICommonContactCell) -> Bool
    func onAddNewFriend(_ cell: TUICommonTableViewCell) -> Bool
    func onGroupConversation(_ cell: TUICommonTableViewCell) -> Bool
}

```


【Objective-C】
``` objectivec
@protocol TUIContactControllerListener <NSObject>
@optional
- (void)onSelectFriend:(TUICommonContactCell *)cell;
- (void)onAddNewFriend:(TUICommonTableViewCell *)cell;
- (void)onGroupConversation:(TUICommonTableViewCell *)cell;
@end
```

【简约版】




【Swift】
``` swift
// ContactController 为您自己的 ViewController
public class ContactsController: UIViewController, TUIPopViewDelegate {
    override public func viewDidLoad() {
        super.viewDidLoad()

        contactVC = TUIContactController_Minimalist()
        if let contactVC = contactVC {
            addChild(contactVC)
            view.addSubview(contactVC.view)
        }
    }
}
```


【Objective-C】
``` objectivec
#import "TUIContactController_Minimalist.h"

// ContactController 为您自己的 ViewController
@implementation ContactController
- (void)viewDidLoad {    
  // 创建 TUIContactController_Minimalist
  TUIContactController_Minimalist *vc = [[TUIContactController_Minimalist alloc] init];
  // 把 TUIContactController_Minimalist 添加到自己的 ViewController
  [self addChildViewController:vc];
  [self.view addSubview:vc.view];
}
@end
```

注意，上面代码只能将 `TUIContactController_Minimalist` 初始化并展示出来，其中的点击行为（例如点击好友、添加好友等），TUIKit 会通过 `TUIContactControllerListener_Minimalist` 抛给上层处理：




【Swift】
``` swift
protocol TUIContactControllerListener_Minimalist: AnyObject {
    func onSelectFriend(_ cell: TUICommonContactCell_Minimalist) -> Bool
    func onAddNewFriend(_ cell: TUICommonTableViewCell) -> Bool
    func onGroupConversation(_ cell: TUICommonTableViewCell) -> Bool
}
```


【Objective-C】
``` objectivec
@protocol TUIContactControllerListener_Minimalist <NSObject>
@optional
- (void)onSelectFriend:(TUICommonContactCell *)cell;
- (void)onAddNewFriend:(TUICommonTableViewCell *)cell;
- (void)onGroupConversation:(TUICommonTableViewCell *)cell;
@end
```

例如，单击好友后，您可以将好友信息页展示出来：



【经典版】




【Swift】
``` swift
@objc private func onSelectFriend(_ cell: TUICommonContactCell) {
    if let delegate = delegate {
        if delegate.onSelectFriend(cell) { return }
    }
    let data = cell.contactData
    let vc = TUIFriendProfileController(style: .grouped)
    vc.friendProfile = data?.friendProfile
    navigationController?.pushViewController(vc, animated: true)
}
```


【Objective-C】
``` objectivec
#import "TUIFriendProfileController.h"

- (void)onSelectFriend:(TUICommonContactCell *)cell
{
    TUICommonContactCellData *data = cell.contactData;
    // 创建好友资料 vc
    TUIFriendProfileController *vc = [[TUIFriendProfileController alloc] init];
    vc.friendProfile = data.friendProfile;
    // 展示好友资料 vc
    [self.navigationController pushViewController:(UIViewController *)vc animated:YES];
}
```

【简约版】




【Swift】
``` swift
@objc func onSelectFriend(_ cell: TUICommonContactCell_Minimalist) {
    if let delegate = delegate {
        if delegate.onSelectFriend(cell) { return }
    }
    let data = cell.contactData
    let vc = TUIFriendProfileController_Minimalist()
    vc.friendProfile = data?.friendProfile
    navigationController?.pushViewController(vc, animated: true)
}
```


【Objective-C】
``` objectivec
#import "TUIFriendProfileController_Minimalist.h"

- (void)onSelectFriend:(TUICommonContactCell *)cell
{
    TUICommonContactCellData *data = cell.contactData;
    // 创建好友资料 vc
    TUIFriendProfileController_Minimalist *vc = [[TUIFriendProfileController_Minimalist alloc] init];
    vc.friendProfile = data.friendProfile;
    // 展示好友资料 vc
    [self.navigationController pushViewController:(UIViewController *)vc animated:YES];
}
```

### 步骤5：构建音视频通话功能

TUI 组件支持在聊天界面对用户发起音视频通话，仅需要简单几步就可以快速集成：
<table>
<tr>
<td rowspan="1" colSpan="1" >视频通话</td>

<td rowspan="1" colSpan="1" >语音通话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100022348635/7b737757cc6e11edb580525400088f3a.jpg)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100022348635/7b91a71acc6e11edb580525400088f3a.png)</td>
</tr>
</table>

1. 开通音视频服务。

2. 登录 即时通信 IM 控制台 ，单击目标应用卡片，进入应用的基础配置页面。

3. 在开通腾讯实时音视频服务功能区，单击**免费体验**即可开通 TUICallKit 的 7 天免费试用服务。

4. 在弹出的开通实时音视频 TRTC 服务对话框中，单击确认，系统将为您在 [实时音视频控制台](https://console.cloud.tencent.com/trtc) 创建一个与当前 IM 应用相同 SDKAppID 的实时音视频应用，二者账号与鉴权可复用。

5. 集成 TUICallKit 组件。
在 podfile 文件中添加以下内容。

   ``` objectivec
   // 集成音视频通话组件
   pod 'TUICallKit_Swift'                  
   ```
6. 发起和接收视频或语音通话。

<table>
<tr>
<td rowspan="1" colSpan="1" >消息页发起通话</td>

<td rowspan="1" colSpan="1" >联系人页发起通话</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100022348635/7ba6705ccc6e11edb580525400088f3a.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100022348635/7bbfa40bcc6e11edb580525400088f3a.png)</td>
</tr>
</table>


   集成 TUICallKit 组件后，聊天界面和联系人资料界面默认会出现 “视频通话” 和 “语音通话” 两个按钮，当用户点击按钮时，TUIKit 会自动展示通话邀请 UI，并给对方发起通话邀请请求。

  - 当用户在线收到通话邀请时，TUIKit 会自动展示通话接收 UI，用户可以选择同意或者拒绝通话。

  - 当用户离线收到通话邀请时，如需唤起 App 通话，就要使用到离线推送能力，离线推送的实现请参见 [添加离线推送](https://cloud.tencent.com/document/product/269/109894)。

7. 添加离线推送。
在使用离线推送之前，您需要开通 [IM 离线推送](https://cloud.tencent.com/document/product/269/75429) 服务。

8. 关于 App 的配置，您可以参见文档：[集成 TUIOfflinePush 跑通离线推送功能](https://cloud.tencent.com/document/product/269/109894)。
   

   > **说明：**
   > 

   > 配置完成后，当单击接收到的**音视频通话离线推送通知**时， TUICallKit 会自动拉起**音视频通话邀请界面**。
   > 

9. 附加增值能力
集成 TUIChat 和 TUICallkit 的组件后，在聊天界面发送语音消息时，即可**录制带 AI 降噪和自动增益的语音消息**。该功能需要购买 [音视频通话能力](https://cloud.tencent.com/document/product/1640/79968) 进阶版及以上套餐，仅 IMSDK 7.0 及以上版本支持。当套餐过期后，录制语音消息会切换到系统 API 进行录音。
下面是使用两台华为 P10同时录制的语音消息对比：

<link rel="stylesheet" href="//cloudcache.tencentcs.com/open_proj/proj_qcloud_v2/gateway/portal/css/global-20209142343.css?max_age=31536000&amp;t=20191128" />
<link rel="stylesheet" href="//cloudcache.tencentcs.com/open_proj/proj_qcloud_v2/gateway/portal/css/global-components.css?max_age=31536000&amp;t=20180817" />
<link rel="stylesheet" href="//cloudcache.tencentcs.com/open_proj/proj_qcloud_v2/gateway/documentation/documentation-v4/css/pandect-20219091610.css" />
<link rel="stylesheet" href="//cloudcache.tencentcs.com/open_proj/proj_qcloud_v2/gateway/documentation/documentation-v4/css/import-2-markdown-20219091610.css" />
<link rel="stylesheet" href="//cloudcache.tencentcs.com/open_proj/proj_qcloud_v2/platform/documents/css/documents-202205161915.css" />
<link rel="stylesheet" href="//cloudcache.tencentcs.com/open_proj/proj_qcloud_v2/gateway/documentation/documentation-v4/css/pandect-202012171130.css" />
<link rel="stylesheet" href="//qcloudimg.tencent-cloud.cn/static/document/qcloud-document-sdk.v0.0.17.css" />
<link rel="stylesheet" href="//cloudcache.tencentcs.com/qcloud/main/components/document-feedback/document-feedback.944df9c907.css" />
<style>
* {
  font-family: 'pingfang SC','helvetica neue',arial,'hiragino sans gb','microsoft yahei ui','microsoft yahei',simsun,sans-serif;
}
</style>
 
<div class="markdown-text-box">
<table style="text-align:center;vertical-align:middle;width:800px">
  <tr>
    <th style="text-align:center"><b>系统录制的语音消息<br /></b></th>
    <th style="text-align:center"><b>TUICallkit 录制的带 AI 降噪和自动增益的语音消息<br /></b></th>
  </tr>
  <tr>
    <td>
      <audio id="audio" controls preload="none">
	<source id="m4a" src="https://im.sdk.cloudcachetci.com/tools/resource/rain_system_record.m4a"></source>
      </audio>
    </td>
		
    <td>
      <audio id="audio" controls preload="none">
	<source id="m4a" src="https://im.sdk.cloudcachetci.com/tools/resource/rain_tuicallkit_record_with_agc_aidenoise.m4a"></source>
      </audio>
    </td>
  </tr>
</table>

</div>





### 步骤6：构建多人音视频功能

TUI 组件支持在聊天界面对用户发起多人音视频，仅需要简单几步就可以快速集成：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027269567/c5fbe907b0f711ee9fd6525400bb593a.png)

1. 开通音视频服务。

2. 登录 [即时通信 IM 控制台](https://console.cloud.tencent.com/im)，单击目标应用卡片，进入应用的基础配置页面。

3. 找到含 UI 低代码场景方案功能区，单击卡片下方的多人音视频（TUIRoomKit） > 免费体验。

4. 在弹窗中单击免费试用7天，即可成功开通多人音视频免费体验版。开通完成后即可参见 [集成指引](https://cloud.tencent.com/document/product/269/84296) 进行集成。

5. 集成 TUIRoomKit 组件。在 podfile 文件中添加以下内容。

   ``` ruby
   // 集成多人音视频组件
   pod 'TUIRoomKit'
   ```
6. 发起多人音视频会议


   集成 TUIRoomKit 组件后，聊天界面默认会出现 “快速会议” 按钮，当用户点击按钮时，TUIKit 会自动发起会议，并在聊天记录中展示一条会议邀请卡片。

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027269567/a2bf4380b0fa11eeae9a525400c26da5.jpg)


## 常见问题

#### 1. TUICallKit 和自己集成的音视频库冲突了？

腾讯云的音视频库不能同时集成，可能存在符号冲突，可以按照下面的场景处理。
1. 如果您使用了 `TXLiteAVSDK_TRTC` 库，不会发生符号冲突。可直接在 Podfile 文件中添加依赖，

   ``` ruby
   pod 'TUICallKit_Swift'  
   ```
2. 如果您使用了 `TXLiteAVSDK_Professional` 库，会产生符号冲突。您可在 Podfile 文件中添加依赖，

   ``` ruby
   pod 'TUICallKit_Swift/Professional'
   ```
3. 如果您使用了 `TXLiteAVSDK_Enterprise` 库，会产生符号冲突。建议升级到 `TXLiteAVSDK_Professional` 后使用 TUICallKit_Swift/Professional。


#### 2. 通话邀请的超时时间默认是多久？

通话邀请的默认超时时间是 30 秒。

#### 3. 在邀请超时时间内，被邀请者如果离线再上线，能否立即收到邀请？
- 如果是单聊通话邀请，被邀请者离线再上线可以收到通话邀请，TUIKit 内部会自动唤起通话邀请界面。

- 如果是群聊通话邀请，被邀请者离线再上线后会自动拉取最近 30 秒内的邀请，TUIKit 会自动唤起群通话界面。


#### 4. 上架 Appstore 时打包失败，提示 Unsupported Architectures。

问题现象如下图，打包时提示 ImSDK_Plus.framework 中包含了 Appstore 不支持的 x86_64 模拟器版本。该问题是由于 IMSDK 为了方便开发者调试，发布时会默认带上模拟器版本。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027269567/3ee0a085ec0411eeb5dc525400aa857d.png)

您可以按照下面的步骤，在打包时去掉模拟器版本：
1. 选中您工程的 Target，并点击 Build Phases 选项，在当前面板中添加 Run Script；

   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027269567/4b1b2ce5ec0411eea93552540076ba55.png)

2. 在新增的 Run Script 中，添加如下脚本：

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
   ![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027269567/6ad039a0ec0411ee94705254001a1c03.png)


## Xcode 集成常见问题

#### 1.  [Xcodeproj] Unknown object version (60). (RuntimeError)

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/e59d1a43dd2e11eeb419525400ea3514.png)


使用 Xcode15 创建新工程来集成 TUIKit 时，输入**pod install** 后，可能会遇到此问题，原因是使用了较旧版本的 CocoaPods ，此时有两种解决办法：

解决方式一： 修改 Xcode 工程的 **Project Format **版本。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/2d589afadd2611eeb419525400ea3514.png)


解决方式二： 升级本地的 CocoaPods 版本，升级方式本文不再赘述。

您可以在终端输入 **pod --version** 查看当前的 Pods 版本。

#### 2. -ld64链接器问题

Assertion failed: (false && "compact unwind compressed function offset doesn't fit in 24 bits"), function operator(), file Layout.cpp,

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/5fdb1ededd1811eea20f525400b5f95f.png)


或是使用 XCode15 集成 TUIRoom 时，因最新链接器导致 TUIRoomEngine 的符号冲突，都属于该问题。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/0e8212c1dd1911ee9e38525400bb593a.png)


解决方式是：修改链接器配置

在 **Build Settings** 中的**Other Linker Flags** 种添加"**-ld64**"，即可解决。  参考资料： [https://developer.apple.com/forums/thread/735426](https://links.jianshu.com/go?to=https%3A%2F%2Fdeveloper.apple.com%2Fforums%2Fthread%2F735426)。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/c1cae388dd1911eea20f525400b5f95f.png)


#### 3. Rosetta 模拟器问题

使用苹果芯片（m1\m2等系列芯片）时会遇到， 原因是包括 SDWebImage 在内的三方库，并未支持 xcframework，不过苹果依旧给出了适配办法，就是在模拟器上开启 Rosetta 设置， 一般情况下编译时会自动弹出 Rosetta 选项。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/fd5287fadd1911ee9e38525400bb593a.png)


#### 4. Xcode 15 开发者沙盒选项问题

Sandbox: bash(xxx) deny(1) file-write-create

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/a35a6146e10311eeb419525400ea3514.png)


当您使用 Xcode 15 创建一个新工程时， 可能会因为此选项导致编译运行失败，建议您关闭此选项。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/e4e44368dd1c11eea941525400ea3514.png)


### 5. Xcode 16 不支持 Framework 开启 bitcode 问题

**解决方案1：升级 SDK**
如果您使用的是包含 Bitcode 的旧版本 SDK（如 TXIMSDK_iOS），建议您按照本文档的指引，将 SDK 升级至 TXIMSDK_Plus_iOS_XCFramework。
**解决方式2: 修改 Podfile 配置**

在您的 Podfile 末尾新增如下配置，重新 Pod install。
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

## CocoaPods 集成常见问题

#### 1. 使用远端集成时，Pod依赖版本不匹配问题

若您[使用远端 Pods 集成时](https://write.woa.com/document/107052221686493184)，出现 **Podfile.lock** 和 插件依赖的 TUICore 版本不一致时， 

此时请删除 **Podfile.lock** 文件， 并使用 **pod repo update **更新本地代码仓库， 之后使用 **pod update** 重新更新即可。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/ad33aee1e10311ee9ca3525400bb593a.png)


#### 2. 使用本地集成时，Pod依赖版本不匹配问题

若您[使用DevelopPods集成时](https://write.woa.com/document/107052221686493184) 出现  插件依赖的 **TUICore **版本较新，但本地 Pod 依赖的版本号是 **1.0.0** ，

此时请您参见 [Podfile_local](https://github.com/TencentCloud/TIMSDK/blob/master/iOS/Demo/Podfile_local) 和 [TUICore.spec](https://github.com/TencentCloud/TIMSDK/blob/master/iOS/TUIKit/TUICore/TUICore.podspec) ， 插件需要跟随版本，需要和 TUICore.spec 中一致，正常情况下我们会帮您修改为一致。

第一次使用本地集成时，建议您下载我们的示例 Demo 工程，将 Podfile 文件内容替换为 Podfile_local 的内容，执行 **Pod update **后相互参照。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027870539/b364c1ebe10311ee9ca3525400bb593a.png)


