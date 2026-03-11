> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLivePremier 接口文档

## 概述

`V2TXLivePremier` 是腾讯云直播 SDK 的高级接口类，提供 SDK 全局配置和管理功能。

**平台支持**: iOS, macOS  
**功能范围**: SDK初始化、Licence管理、环境配置、音频数据回调、实验性API

## 📋 目录结构

### 1. [V2TXLivePremier接口](#v2txlivepremier接口)
### 2. [V2TXLivePremierObserver回调接口](#v2txlivepremierobserver回调接口)

## 1. V2TXLivePremier接口

### 🔧 getSDKVersionStr - 获取SDK版本号

```objc
+ (NSString *)getSDKVersionStr;
```

**功能**: 获取当前SDK的版本号字符串

**返回值**: 
- `NSString*`: SDK版本号字符串，格式如 "10.7.0.12345"

**使用场景**:
- 版本兼容性检查
- 问题排查时提供版本信息
- 统计和监控

**示例**:
```objc
NSString *version = [V2TXLivePremier getSDKVersionStr];
NSLog(@"当前SDK版本: %@", version);
```

### setObserver() - 设置 V2TXLivePremier 回调接口

```objc
+ (void)setObserver:(id<V2TXLivePremierObserver>)observer;
```

**参数**:
- `observer`: 实现V2TXLivePremierObserver协议的对象

**使用时机**: 在应用启动时设置，全局生效

**注意事项**:
- 建议在应用启动时设置一次即可
- 观察者对象需要在整个应用生命周期内保持有效

### setLogConfig() - 设置 Log 的配置信息

```objc
+ (V2TXLiveCode)setLogConfig:(V2TXLiveLogConfig *)config;
```

**参数**:
- `config`: 日志配置对象，包含日志级别、存储路径等

**使用时机**: 在应用启动时设置，全局生效

**使用场景**:
- 调试阶段开启详细日志
- 生产环境减少日志输出
- 自定义日志存储路径

**示例**:
```objc
V2TXLiveLogConfig *logConfig = [[V2TXLiveLogConfig alloc] init];
logConfig.enableConsole = YES;
logConfig.enableLogFile = YES;
logConfig.enableObserver = YES;
logConfig.logLevel = V2TXLiveLogLevelAll;
[V2TXLivePremier setObserver:self];
[V2TXLivePremier setLogConfig:logConfig];
```

### setEnvironment() - 设置 SDK 接入环境

```objc
+ (V2TXLiveCode)setEnvironment:(const char *)env;
```

**参数**:
- `env`: 环境标识，支持：
  - `"default"`: 默认环境，SDK 在全球寻找最佳接入点
  - `"GDPR"`: GDPR 环境，音视频数据不经过中国大陆服务器

**注意**: 如无特殊需求，请不要调用此接口

### setLicence() - 设置 SDK 的授权 License

```objc
+ (void)setLicence:(NSString *)url key:(NSString *)key;
```

**参数**:
- `url`: licence 地址
- `key`: licence 秘钥

**使用时机**: 应用启动时调用，必须在推流/播放前设置

**文档地址**: https://cloud.tencent.com/document/product/454/34750

**示例**:
```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [V2TXLivePremier setObserver:self];
    [V2TXLivePremier setLicence:@"your_licence_url" key:@"your_licence_key"];
    return YES;
}

#pragma mark - V2TXLivePremierObserver
- (void)onLicenceLoaded:(int)result Reason:(NSString *)reason {
    if (result == 0) {
        NSLog(@"licence 加载成功, %@", reason);
    } else if (result == -4) {
        NSLog(@"licence 包名不匹配，%@", reason);
    } else if (result == -11) {
        NSLog(@"licence 过期，%@", reason);
    } else {
        NSLog(@"licence 其它错误，%@", reason);
    }
}
```

### setSocks5Proxy() - 设置 SDK socks5 代理配置

```objc
+ (V2TXLiveCode)setSocks5Proxy:(NSString *)host 
                          port:(NSInteger)port 
                      username:(NSString *)username 
                      password:(NSString *)password 
                        config:(V2TXLiveSocks5ProxyConfig *)config;
```

**参数**:
- `host`: socks5 代理服务器地址
- `port`: socks5 代理服务器端口
- `username`: 代理服务器用户名
- `password`: 代理服务器密码
- `config`: socks5 代理配置

**使用时机**: 应用启动时调用

### enableAudioCaptureObserver() - 开启/关闭对音频采集数据的监听回调

```objc
+ (V2TXLiveCode)enableAudioCaptureObserver:(BOOL)enable 
                                   format:(V2TXLiveAudioFrameObserverFormat *)format;
```

**参数**:
- `enable`: 是否开启（默认 false）
- `format`: 音频帧回调格式

**使用时机**: 需要在 `V2TXLivePusher#startPush` 之前调用

### enableAudioPlayoutObserver() - 开启/关闭对最终系统要播放出的音频数据的监听回调

```objc
+ (V2TXLiveCode)enableAudioPlayoutObserver:(BOOL)enable 
                                  format:(V2TXLiveAudioFrameObserverFormat *)format;
```

**参数**:
- `enable`: 是否开启（默认 false）
- `format`: 音频帧回调格式

**技术规格**:
- 音频时间帧长固定为0.02s
- PCM格式音频数据
- 混合各路待播放音频后的数据

### enableVoiceEarMonitorObserver() - 开启/关闭对耳返音频数据的监听回调

```objc
+ (V2TXLiveCode)enableVoiceEarMonitorObserver:(BOOL)enable;
```

**参数**:
- `enable`: 是否开启（默认 false）

**技术规格**:
- 音频时间帧长不固定
- PCM格式音频数据
- 耳返专用音频流

### setUserId() - 设置 userId

```objc
+ (void)setUserId:(NSString *)userId;
```

**参数**:
- `userId`: 业务侧维护的用户/设备 ID

**使用时机**: 应用启动时调用

### callExperimentalAPI() - 调用实验性 API 接口

```objc
+ (V2TXLiveCode)callExperimentalAPI:(NSString *)jsonStr;
```

**参数**:
- `jsonStr`: 接口及参数描述的 JSON 字符串

**返回值**:
- `V2TXLIVE_OK`: 成功
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: 参数非法

## 2. V2TXLivePremierObserver回调接口

### onLog() - 自定义 Log 输出回调

```objc
- (void)onLog:(V2TXLiveLogLevel)level log:(NSString *)log;
```

**参数**:
- `level`: 日志级别
- `log`: 日志内容

**使用场景**:
- 自定义日志处理
- 日志重定向到自有系统
- 日志过滤和格式化

### onLicenceLoaded() - License加载回调

```objc
- (void)onLicenceLoaded:(int)result Reason:(NSString *)reason;
```

**参数**:
- `result`: 设置结果（0 成功，负数失败）
- `reason`: 失败原因

### onCaptureAudioFrame() - 本地麦克风采集到的音频数据回调

```objc
- (void)onCaptureAudioFrame:(V2TXLiveAudioFrame *)frame;
```

**参数**:
- `frame`: 音频数据帧

**重要说明**:
- 不要在此回调中做耗时操作
- 音频数据支持修改
- 时间帧长固定为 0.02s
- 不包含背景音、音效等前处理效果
- 延迟极低

### onPlayoutAudioFrame() - 混合后播放音频数据回调

```objc
- (void)onPlayoutAudioFrame:(V2TXLiveAudioFrame *)frame;
```

**参数**:
- `frame`: PCM 格式音频数据帧

**重要说明**:
- 时间帧长固定为 0.02s
- 数据可读写，但需保证处理耗时
- 不包含耳返音频数据

### onVoiceEarMonitorAudioFrame() - 耳返音频数据回调

```objc
- (void)onVoiceEarMonitorAudioFrame:(V2TXLiveAudioFrame *)frame;
```

**参数**:
- `frame`: PCM 格式音频数据帧

**重要说明**:
- 时间帧长不固定
- 数据可读写，但需保证处理耗时
