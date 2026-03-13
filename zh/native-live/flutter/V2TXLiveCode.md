> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLiveCode 错误码文档

## 概述

`V2TXLiveCode` 是腾讯云直播SDK Flutter平台的错误码和警告码定义文件，包含了推流器、播放器、混流、录制等功能的错误码分类和详细说明。

**文件路径**: `v2_tx_live_code.dart`  
**平台支持**: Flutter  
**错误码总数**: 20个核心错误码和警告码

## 📋 目录结构

### 1. [错误码分类](#错误码分类)
### 2. [通用错误码](#通用错误码)
### 3. [网络相关警告码](#网络相关警告码)
### 4. [摄像头相关警告码](#摄像头相关警告码)
### 5. [麦克风相关警告码](#麦克风相关警告码)
### 6. [屏幕分享相关警告码](#屏幕分享相关警告码)
### 7. [编解码相关警告码](#编解码相关警告码)

## 1. 错误码分类

### 🎯 错误码统计

| 类别 | 错误码数量 | 主要功能 |
|------|----------|----------|
| 通用错误码 | 9个 | API调用、参数验证、权限检查等 |
| 网络相关警告码 | 2个 | 网络状况、视频卡顿监控 |
| 摄像头相关警告码 | 3个 | 摄像头设备状态监控 |
| 麦克风相关警告码 | 3个 | 麦克风设备状态监控 |
| 屏幕分享相关警告码 | 3个 | 屏幕分享功能状态监控 |
| 编解码相关警告码 | 2个 | 音视频编解码器状态监控 |

### 🔧 技术特点

- **层次化分类**: 按功能模块进行错误码分组
- **详细描述**: 每个错误码都有明确的说明和使用场景
- **平台适配**: 针对Flutter平台的特定错误码
- **调试友好**: 提供错误码的详细解释和处理建议

## 类型定义

```dart
typedef V2TXLiveCode = int;
```

`V2TXLiveCode` 是 `int` 类型的别名，用于表示各种错误和警告代码。

## 成功代码

| 代码 | 值 | 描述 |
|------|----|------|
| `V2TXLIVE_OK` | 0 | 操作成功 |

## 2. 通用错误码

### ✅ V2TXLIVE_OK - 操作成功

```dart
static const int V2TXLIVE_OK = 0;
```

**含义**: 没有错误，操作成功完成

**使用场景**:
- API调用成功返回
- 操作执行成功确认
- 状态检查正常

### ❌ V2TXLIVE_ERROR_FAILED - 通用错误

```dart
static const int V2TXLIVE_ERROR_FAILED = -1;
```

**含义**: 暂未归类的通用错误

**触发场景**:
- 内部处理异常

### ❌ V2TXLIVE_ERROR_INVALID_PARAMETER - 参数不合法

```dart
static const int V2TXLIVE_ERROR_INVALID_PARAMETER = -2;
```

**含义**: 调用API时传入的参数不合法

**常见场景**:
- 推流地址格式错误
- 设置的参数不支持

### ❌ V2TXLIVE_ERROR_REFUSED - API调用被拒绝

```dart
static const int V2TXLIVE_ERROR_REFUSED = -3;
```

**含义**: API调用被拒绝

**触发场景**:
- 调用时机不正确

### ❌ V2TXLIVE_ERROR_NOT_SUPPORTED - API不支持

```dart
static const int V2TXLIVE_ERROR_NOT_SUPPORTED = -4;
```

**含义**: 当前API不支持调用

**常见场景**:
- 平台不支持的功能
- SDK版本过低
- 硬件不支持的特性

### ❌ V2TXLIVE_ERROR_INVALID_LICENSE - License无效

```dart
static const int V2TXLIVE_ERROR_INVALID_LICENSE = -5;
```

**含义**: License不合法，调用失败

**触发场景**:
- License文件未设置
- License已过期
- License与包名不匹配

### ❌ V2TXLIVE_ERROR_REQUEST_TIMEOUT - 请求超时

```dart
static const int V2TXLIVE_ERROR_REQUEST_TIMEOUT = -6;
```

**含义**: 请求服务器超时

**常见场景**:
- 网络连接不稳定
- 服务器响应缓慢

### ❌ V2TXLIVE_ERROR_SERVER_PROCESS_FAILED - 服务器处理失败

```dart
static const int V2TXLIVE_ERROR_SERVER_PROCESS_FAILED = -7;
```

**含义**: 服务器无法处理您的请求

**触发场景**:
- 服务器内部错误
- 请求格式不正确
- 服务器资源不足

### ❌ V2TXLIVE_ERROR_DISCONNECTED - 连接断开

```dart
static const int V2TXLIVE_ERROR_DISCONNECTED = -8;
```

**含义**: 网络连接断开

**常见场景**:
- 推流网络断开
- 拉流网络断开

### ❌ V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS - 无可用HEVC解码器

```dart
static const int V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS = -2304;
```

**含义**: 找不到可用的HEVC解码器

**触发场景**:
- 设备不支持HEVC硬解
- HEVC解码器初始化失败
- 系统版本过低

## 3. 网络相关警告码

### ⚠️ V2TXLIVE_WARNING_NETWORK_BUSY - 网络状况差

```dart
static const int V2TXLIVE_WARNING_NETWORK_BUSY = 1101;
```

**含义**: 网络状况差，上行带宽太小，上传数据被阻塞

**触发场景**:
- 上行带宽不足
- 网络抖动严重
- 数据包发送阻塞

**处理建议**:
- 检查网络连接状态
- 降低视频码率或分辨率
- 切换到更稳定的网络环境

### ⚠️ V2TXLIVE_WARNING_VIDEO_BLOCK - 视频播放卡顿

```dart
static const int V2TXLIVE_WARNING_VIDEO_BLOCK = 2105;
```

**含义**: 当前视频播放出现卡顿

**触发场景**:
- 网络下行带宽不足
- 视频解码器性能不足
- 设备CPU负载过高

**处理建议**:
- 检查网络连接质量
- 降低视频分辨率或帧率
- 优化播放器解码性能

## 4. 摄像头相关警告码

### ⚠️ V2TXLIVE_WARNING_CAMERA_START_FAILED - 摄像头启动失败

```dart
static const int V2TXLIVE_WARNING_CAMERA_START_FAILED = -1301;
```

**含义**: 摄像头启动失败

**触发场景**:
- 摄像头硬件故障
- 摄像头驱动异常
- 系统资源不足

**处理建议**:
- 检查摄像头硬件状态
- 重启应用或设备
- 检查系统权限设置

### ⚠️ V2TXLIVE_WARNING_CAMERA_OCCUPIED - 摄像头被占用

```dart
static const int V2TXLIVE_WARNING_CAMERA_OCCUPIED = -1316;
```

**含义**: 摄像头被占用，尝试开启其他摄像头

**触发场景**:
- 其他应用正在使用摄像头
- 系统相机应用正在运行
- 视频通话应用占用摄像头

**处理建议**:
- 关闭其他使用摄像头的应用
- 切换到其他可用摄像头
- 等待摄像头资源释放

### ⚠️ V2TXLIVE_WARNING_CAMERA_NO_PERMISSION - 摄像头权限未授权

```dart
static const int V2TXLIVE_WARNING_CAMERA_NO_PERMISSION = -1314;
```

**含义**: 摄像头设备未授权，通常在移动设备上，可能是用户拒绝了权限

**触发场景**:
- 用户拒绝了摄像头权限请求
- 应用未申请摄像头权限
- 权限被系统或用户撤销

**处理建议**:
- 检查并请求摄像头权限
- 引导用户开启权限设置
- 提供权限申请说明

## 5. 麦克风相关警告码

### ⚠️ V2TXLIVE_WARNING_MICROPHONE_START_FAILED - 麦克风启动失败

```dart
static const int V2TXLIVE_WARNING_MICROPHONE_START_FAILED = -1302;
```

**含义**: 麦克风启动失败

**触发场景**:
- 麦克风硬件故障
- 音频驱动异常
- 系统音频服务异常

**处理建议**:
- 检查麦克风硬件状态
- 重启音频服务或设备
- 检查音频权限设置

### ⚠️ V2TXLIVE_WARNING_MICROPHONE_OCCUPIED - 麦克风被占用

```dart
static const int V2TXLIVE_WARNING_MICROPHONE_OCCUPIED = -1319;
```

**含义**: 麦克风被占用，例如移动设备正在通话时，开启麦克风失败

**触发场景**:
- 正在进行电话通话
- 其他应用正在使用麦克风
- 语音助手正在运行

**处理建议**:
- 结束当前通话或语音应用
- 等待麦克风资源释放
- 切换到其他音频输入设备

### ⚠️ V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION - 麦克风权限未授权

```dart
static const int V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION = -1317;
```

**含义**: 麦克风设备未授权，通常在移动设备上，可能是用户拒绝了权限

**触发场景**:
- 用户拒绝了麦克风权限请求
- 应用未申请麦克风权限
- 权限被系统或用户撤销

**处理建议**:
- 检查并请求麦克风权限
- 引导用户开启权限设置
- 提供权限申请说明

## 6. 屏幕分享相关警告码

### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED - 系统不支持屏幕共享

```dart
static const int V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED = -1309;
```

**含义**: 当前系统不支持屏幕共享

**触发场景**:
- 操作系统版本过低
- 设备硬件不支持
- 平台限制（如某些移动设备）

**处理建议**:
- 检查系统版本要求
- 确认设备是否支持屏幕录制
- 考虑使用其他分享方式

### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED - 屏幕录制启动失败

```dart
static const int V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED = -1308;
```

**含义**: 启动屏幕录制失败，如果在移动设备上出现，可能是用户拒绝了权限

**触发场景**:
- 用户拒绝了屏幕录制权限
- 系统安全策略限制
- 其他应用正在使用屏幕录制

**处理建议**:
- 检查并请求屏幕录制权限
- 引导用户开启权限设置
- 关闭其他屏幕录制应用

### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED - 屏幕录制被中断

```dart
static const int V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED = -7001;
```

**含义**: 屏幕录制被系统中断

**触发场景**:
- 系统弹出对话框或通知
- 用户切换到其他应用
- 系统资源紧张被强制中断

**处理建议**:
- 重新启动屏幕录制
- 避免在录制过程中进行其他操作
- 检查系统资源使用情况

## 7. 编解码相关警告码

### ⚠️ V2TXLIVE_WARNING_ENCODER_START_FAILED - 视频编码器启动失败

```dart
static const int V2TXLIVE_WARNING_ENCODER_START_FAILED = -1303;
```

**含义**: 视频编码器启动失败

**触发场景**:
- 编码器硬件资源不足
- 编码参数设置不当
- 系统编解码器异常

**处理建议**:
- 检查编码参数设置
- 降低视频分辨率或码率
- 重启编码器或应用

### ⚠️ V2TXLIVE_WARNING_DECODER_START_FAILED - 视频解码器启动失败

```dart
static const int V2TXLIVE_WARNING_DECODER_START_FAILED = -1304;
```

**含义**: 视频解码器启动失败

**触发场景**:
- 解码器硬件资源不足
- 视频格式不支持
- 系统解码器异常

**处理建议**:
- 检查视频格式兼容性
- 降低视频分辨率或帧率
- 重启解码器或应用

### ⚠️ V2TXLIVE_WARNING_CURRENT_ENCODE_TYPE_CHANGED - 编码器类型变更

```dart
static const int V2TXLIVE_WARNING_CURRENT_ENCODE_TYPE_CHANGED = 1104;
```

**含义**: 表示编码器发生改变，可以通过onWarning回调函数的扩展信息中的codec_type字段来获取当前的编码格式

**触发场景**:
- 编码器自动切换（如从硬件编码切换到软件编码）
- 编码参数动态调整
- 系统资源变化导致编码器变更

**处理建议**:
- 监听编码器变更事件，及时调整编码策略
- 根据编码器类型优化视频质量设置
- 记录编码器变更日志用于性能分析

### ⚠️ V2TXLIVE_WARNING_CURRENT_DECODE_TYPE_CHANGED - 解码器类型变更

```dart
static const int V2TXLIVE_WARNING_CURRENT_DECODE_TYPE_CHANGED = 2008;
```

**含义**: 表示解码器发生改变，可以通过onWarning回调函数的扩展信息中的codec_type字段来获取当前的解码格式

**触发场景**:
- 解码器自动切换（如从硬件解码切换到软件解码）
- 视频格式变化导致解码器变更
- 系统资源变化导致解码器变更

**处理建议**:
- 监听解码器变更事件，及时调整解码策略
- 根据解码器类型优化播放性能
- 记录解码器变更日志用于性能分析

**注意**: Flutter平台支持此错误码的扩展信息，可以通过回调参数获取详细的编解码器类型信息
