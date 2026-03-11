> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLivePremier 接口文档

## 概述

`V2TXLivePremier` 是腾讯云直播 SDK 的高级接口类，提供 SDK 全局配置和管理功能。

**文件路径**: `v2_tx_live_premier.dart`
**平台支持**: Flutter
**功能范围**: SDK初始化、Licence管理、环境配置

## 📋 目录结构

### 1. [V2TXLivePremier接口](#v2txlivepremier接口)
### 2. [V2TXLivePremierObserver回调接口](#v2txlivepremierobserver回调接口)

## 1. V2TXLivePremier接口

### getSDKVersionStr() - 获取 SDK 版本号
```dart
static Future<String> getSDKVersionStr() async
```

**返回值**: SDK 版本字符串，格式如 "10.7.0.12345"

**使用时机**: 无限制

**使用场景**:
- 版本兼容性检查
- 问题排查时提供版本信息
- 统计和监控

**示例**:
```dart
String version = await V2TXLivePremier.getSDKVersionStr();
print('当前SDK版本：$version');
```

### setObserver() - 设置 V2TXLivePremier 回调接口
```dart
static Future<void> setObserver(V2TXLivePremierObserver? observer) async
```

**参数**:
- `observer`: 实现V2TXLivePremierObserver协议的对象

**使用时机**: 在应用启动时设置，全局生效

**注意事项**:
- 建议在应用启动时设置一次即可
- 观察者对象需要在整个应用生命周期内保持有效

**示例**:
```dart
await V2TXLivePremier.setObserver((type, params) {
  switch (type) {
    case V2TXLivePremierObserverType.onLog:
      print('日志输出: ${params['log']}');
      break;
    case V2TXLivePremierObserverType.onLicenceLoaded:
      print('Licence加载结果: ${params['result']}');
      break;
  }
});
```



### setEnvironment() - 设置 SDK 接入环境
```dart
static Future<V2TXLiveCode> setEnvironment(String env) async
```

**参数**:
- `env`: 环境标识，支持：
  - `"default"`: 默认环境，SDK 在全球寻找最佳接入点
  - `"GDPR"`: GDPR 环境，音视频数据不经过中国大陆服务器

**注意**: 如无特殊需求，请不要调用此接口

**示例**:
```dart
// 仅在需要GDPR合规时调用
await V2TXLivePremier.setEnvironment("GDPR");
```

### setLicence() - 设置 SDK 的授权 License
```dart
static Future<void> setLicence(String url, String key) async
```

**参数**:
- `url`: licence 地址
- `key`: licence 秘钥

**使用时机**: 应用启动时调用，必须在推流/播放前设置

**文档地址**: https://cloud.tencent.com/document/product/454/34750

**示例**:
```dart
class MyApplication extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // 在应用启动时设置Licence
    WidgetsBinding.instance.addPostFrameCallback((_) async {
      await V2TXLivePremier.setObserver((type, params) {
        if (type == V2TXLivePremierObserverType.onLicenceLoaded) {
          int result = params?['result'] ?? -1;
          String reason = params?['reason'] ?? '';
          
          if (result == 0) {
            print('licence 加载成功, $reason');
          } else if (result == -4) {
            print('licence 包名不匹配，$reason');
          } else if (result == -11) {
            print('licence 过期，$reason');
          } else {
            print('licence 其它错误，$reason');
          }
        }
      });
      await V2TXLivePremier.setLicence("your_licence_url", "your_licence_key");
    });
    
    return MaterialApp(
      home: MyHomePage(),
    );
  }
}
```


### callExperimentalAPI() - 调用实验性 API 接口
```dart
static Future<V2TXLiveCode> callExperimentalAPI(String jsonStr) async
```

**参数**:
- `jsonStr`: 接口及参数描述的 JSON 字符串

**返回值**:
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: 参数非法

**示例**:
```dart
String jsonParams = '{"api": "test", "param": "value"}';
V2TXLiveCode result = await V2TXLivePremier.callExperimentalAPI(jsonParams);
if (result == V2TXLiveCode.V2TXLIVE_OK) {
  print('实验性API调用成功');
}
```

## 2. V2TXLivePremierObserver回调接口

### onLog() - 自定义 Log 输出回调
```dart
void Function(V2TXLivePremierObserverType type, Map<String, dynamic>? params)
```

**参数**:
- `type`: 回调类型，为 `V2TXLivePremierObserverType.onLog`
- `params`: 参数，包含 `level` 和 `log` 字段

**使用场景**:
- 自定义日志处理
- 日志重定向到自有系统
- 日志过滤和格式化

**示例**:
```dart
V2TXLivePremier.setObserver((type, params) {
  if (type == V2TXLivePremierObserverType.onLog) {
    int level = params?['level'] ?? 0;
    String log = params?['log'] ?? '';
    
    // 自定义日志处理
    if (level >= V2TXLiveLogLevel.V2TXLiveLogLevelWarning) {
      print('警告日志: $log');
    } else {
      print('普通日志: $log');
    }
  }
});
```

### onLicenceLoaded() - License加载回调
```dart
void Function(V2TXLivePremierObserverType type, Map<String, dynamic>? params)
```

**参数**:
- `type`: 回调类型，为 `V2TXLivePremierObserverType.onLicenceLoaded`
- `params`: 参数，包含 `result` 和 `reason` 字段

**示例**:
```dart
V2TXLivePremier.setObserver((type, params) {
  if (type == V2TXLivePremierObserverType.onLicenceLoaded) {
    int result = params?['result'] ?? -1;
    String reason = params?['reason'] ?? '';
    
    if (result == 0) {
      print('Licence加载成功: $reason');
    } else {
      print('Licence加载失败($result): $reason');
    }
  }
});
```



## 使用示例

### 完整初始化流程
```dart
import 'package:flutter/material.dart';
import 'package:tencent_trtc/v2_tx_live_premier.dart';
import 'package:tencent_trtc/v2_tx_live_def.dart';

class MyApplication extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // 在应用启动时初始化SDK
    WidgetsBinding.instance.addPostFrameCallback((_) async {
      await SDKManager.initializeSDK();
    });
    
    return MaterialApp(
      title: '腾讯云直播SDK示例',
      home: MyHomePage(),
    );
  }
}

class SDKManager {
  static Future<void> initializeSDK() async {
    try {
      // 1. 设置观察者回调
      await V2TXLivePremier.setObserver((type, params) {
        switch (type) {
          case V2TXLivePremierObserverType.onLog:
            int level = params?['level'] ?? 0;
            String log = params?['log'] ?? '';
            
            // 根据日志级别处理
            if (level >= V2TXLiveLogLevel.V2TXLiveLogLevelWarning) {
              print('⚠️ 警告日志: $log');
            } else if (level >= V2TXLiveLogLevel.V2TXLiveLogLevelInfo) {
              print('ℹ️ 信息日志: $log');
            } else {
              print('🔍 调试日志: $log');
            }
            break;
            
          case V2TXLivePremierObserverType.onLicenceLoaded:
            int result = params?['result'] ?? -1;
            String reason = params?['reason'] ?? '';
            
            if (result == 0) {
              print('✅ Licence加载成功: $reason');
            } else if (result == -4) {
              print('❌ Licence包名不匹配: $reason');
            } else if (result == -11) {
              print('❌ Licence过期: $reason');
            } else {
              print('❌ Licence加载失败($result): $reason');
            }
            break;
        }
      });
      
      // 2. 设置Licence（必须步骤）
      await V2TXLivePremier.setLicence("your_licence_url", "your_licence_key");
      
      // 3. 获取SDK版本信息
      String version = await V2TXLivePremier.getSDKVersionStr();
      print('📦 SDK版本: $version');
      

      

      
      print('🎉 SDK初始化完成');
      
    } catch (e) {
      print('❌ SDK初始化异常: $e');
    }
  }
}
```



#### 实验性API调用示例
```dart
class ExperimentalAPI {
  static Future<void> testExperimentalAPI() async {
    try {
      // 调用实验性API
      String jsonParams = '''
      {
        "api": "testFeature",
        "params": {
          "enable": true,
          "threshold": 0.5,
          "mode": "auto"
        }
      }
      ''';
      
      V2TXLiveCode result = await V2TXLivePremier.callExperimentalAPI(jsonParams);
      
      if (result == V2TXLiveCode.V2TXLIVE_OK) {
        print('✅ 实验性API调用成功');
      } else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
        print('❌ 实验性API参数错误');
      } else {
        print('❌ 实验性API调用失败: $result');
      }
      
    } catch (e) {
      print('❌ 实验性API调用异常: $e');
    }
  }
}
```

## 注意事项

### 1. Licence授权管理
- **必须设置**: 使用SDK前必须调用 `setLicence()` 进行授权，否则SDK功能受限
- **设置时机**: 在应用启动时调用，必须在推流/播放前完成
- **错误处理**: 通过 `onLicenceLoaded` 回调监控授权状态

### 2. 回调注册时机
- **提前注册**: 观察者回调需要在SDK初始化前设置
- **单次设置**: 建议在应用启动时设置一次即可
- **生命周期**: 观察者对象需要在整个应用生命周期内保持有效



### 4. 线程安全
- **主线程执行**: Flutter中所有回调都在UI主线程执行
- **无需线程处理**: 无需额外线程同步处理
- **异步安全**: 确保异步操作的正确性

### 5. 内存管理
- **及时移除**: 及时移除不再使用的观察者
- **避免循环引用**: 避免在回调中持有对SDK的强引用
- **资源释放**: 应用退出时确保释放所有资源

### 6. 日志配置
- **调试阶段**: 开启详细日志便于问题排查
- **生产环境**: 减少日志输出提高性能
- **自定义处理**: 可通过 `onLog` 回调实现自定义日志处理

### 7. 环境配置
- **默认环境**: 如无特殊需求，使用默认环境配置
- **GDPR环境**: 仅在需要GDPR合规时使用
- **代理设置**: 仅在需要代理访问时配置

## 最佳实践

### Licence设置最佳实践
```dart
class LicenceManager {
  static Future<bool> setupLicence() async {
    try {
      // 设置Licence回调
      await V2TXLivePremier.setObserver((type, params) {
        if (type == V2TXLivePremierObserverType.onLicenceLoaded) {
          int result = params?['result'] ?? -1;
          String reason = params?['reason'] ?? '';
          
          if (result == 0) {
            print('✅ Licence授权成功');
          } else {
            print('❌ Licence授权失败($result): $reason');
            // 可根据错误码提供用户友好的提示
            showLicenceErrorDialog(result, reason);
          }
        }
      });
      
      // 设置Licence
      await V2TXLivePremier.setLicence("your_licence_url", "your_licence_key");
      return true;
      
    } catch (e) {
      print('❌ Licence设置异常: $e');
      return false;
    }
  }
  
  static void showLicenceErrorDialog(int result, String reason) {
    // 根据错误码显示相应的错误提示
    String message = '';
    switch (result) {
      case -4:
        message = '应用包名不匹配，请检查Licence配置';
        break;
      case -11:
        message = 'Licence已过期，请续期';
        break;
      default:
        message = 'Licence配置错误: $reason';
        break;
    }
    
    // 显示错误对话框
    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: Text('Licence错误'),
        content: Text(message),
        actions: [
          TextButton(
            onPressed: () => Navigator.pop(context),
            child: Text('确定'),
          ),
        ],
      ),
    );
  }
}
```





## 常见问题解答

### Q: Licence设置失败如何处理？
A: 检查：
1. Licence URL和Key是否正确
2. 应用包名是否与Licence配置匹配
3. Licence是否在有效期内
4. 网络连接是否正常



### Q: 日志文件过大如何处理？
A: 建议：
1. 生产环境使用较高的日志级别
2. 定期清理日志文件
3. 使用自定义日志回调进行日志过滤

### Q: 如何测试实验性API？
A: 建议：
1. 在测试环境中使用
2. 仔细阅读API文档
3. 做好异常处理
4. 反馈使用体验
