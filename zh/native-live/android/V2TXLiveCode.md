> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

# 腾讯云直播SDK V2TXLiveCode 错误码文档

## 概述

`V2TXLiveCode.java` 是腾讯云直播SDK Android平台的错误码和警告码定义文件，包含了推流器、播放器、混流、录制等功能的错误码分类和详细说明。

**文件路径**: `com/tencent/live2/V2TXLiveCode.java`  
**平台支持**: Android  
**错误码总数**: 20个核心错误码和警告码

## 📋 目录结构

### 1. [错误码分类](#错误码分类)
### 2. [通用错误码](#通用错误码)
### 3. [网络相关警告码](#网络相关警告码)
### 4. [摄像头相关警告码](#摄像头相关警告码)
### 5. [麦克风相关警告码](#麦克风相关警告码)
### 6. [屏幕分享相关警告码](#屏幕分享相关警告码)
### 7. [编解码相关警告码](#编解码相关警告码)
### 8. [错误码使用指南](#错误码使用指南)
### 9. [错误处理最佳实践](#错误处理最佳实践)

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
- **平台适配**: 针对Android平台的特定错误码
- **调试友好**: 提供错误码的详细解释和处理建议

## 2. 通用错误码

### ✅ V2TXLIVE_OK - 操作成功

```java
public static final int V2TXLIVE_OK = 0;
```

**含义**: 没有错误，操作成功完成

**使用场景**:
- API调用成功返回
- 操作执行成功确认
- 状态检查正常


### ❌ V2TXLIVE_ERROR_FAILED - 通用错误

```java
public static final int V2TXLIVE_ERROR_FAILED = -1;
```

**含义**: 暂未归类的通用错误

**触发场景**:
- 内部处理异常


### ❌ V2TXLIVE_ERROR_INVALID_PARAMETER - 参数不合法

```java
public static final int V2TXLIVE_ERROR_INVALID_PARAMETER = -2;
```

**含义**: 调用API时传入的参数不合法

**常见场景**:
- 推流地址格式错误
- 设置的参数不支持


### ❌ V2TXLIVE_ERROR_REFUSED - API调用被拒绝

```java
public static final int V2TXLIVE_ERROR_REFUSED = -3;
```

**含义**: API调用被拒绝

**触发场景**:
- 调用时机不正确


### ❌ V2TXLIVE_ERROR_NOT_SUPPORTED - API不支持

```java
public static final int V2TXLIVE_ERROR_NOT_SUPPORTED = -4;
```

**含义**: 当前API不支持调用

**常见场景**:
- 平台不支持的功能
- SDK版本过低
- 硬件不支持的特性


### ❌ V2TXLIVE_ERROR_INVALID_LICENSE - License无效

```java
public static final int V2TXLIVE_ERROR_INVALID_LICENSE = -5;
```

**含义**: License不合法，调用失败

**触发场景**:
- License文件未设置
- License已过期
- License与包名不匹配


### ❌ V2TXLIVE_ERROR_REQUEST_TIMEOUT - 请求超时

```java
public static final int V2TXLIVE_ERROR_REQUEST_TIMEOUT = -6;
```

**含义**: 请求服务器超时

**常见场景**:
- 网络连接不稳定
- 服务器响应缓慢


### ❌ V2TXLIVE_ERROR_SERVER_PROCESS_FAILED - 服务器处理失败

```java
public static final int V2TXLIVE_ERROR_SERVER_PROCESS_FAILED = -7;
```

**含义**: 服务器无法处理您的请求

**触发场景**:
- 服务器内部错误
- 请求格式不正确
- 服务器资源不足


### ❌ V2TXLIVE_ERROR_DISCONNECTED - 连接断开

```java
public static final int V2TXLIVE_ERROR_DISCONNECTED = -8;
```

**含义**: 网络连接断开

**常见场景**:
- 推流网络断开
- 拉流网络断开


### ❌ V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS - 无可用HEVC解码器

```java
public static final int V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS = -2304;
```

**含义**: 找不到可用的HEVC解码器

**触发场景**:
- 设备不支持HEVC硬解
- HEVC解码器初始化失败
- 系统版本过低


## 3. 网络相关警告码

### ⚠️ V2TXLIVE_WARNING_NETWORK_BUSY - 网络繁忙

```java
public static final int V2TXLIVE_WARNING_NETWORK_BUSY = 1101;
```

**含义**: 网络状况不佳，上行带宽太小，上传数据受阻

**监控指标**:
- 上行带宽限制
- 网络延迟增加
- 数据包丢失率升高


### ⚠️ V2TXLIVE_WARNING_VIDEO_BLOCK - 视频卡顿

```java
public static final int V2TXLIVE_WARNING_VIDEO_BLOCK = 2105;
```

**含义**: 当前视频播放出现卡顿

**卡顿原因分析**:
- 网络带宽不足
- 解码性能瓶颈
- 渲染性能问题


## 4. 摄像头相关警告码

### ⚠️ V2TXLIVE_WARNING_CAMERA_START_FAILED - 摄像头打开失败

```java
public static final int V2TXLIVE_WARNING_CAMERA_START_FAILED = -1301;
```

**含义**: 摄像头打开失败

**失败原因**:
- 硬件故障
- 驱动问题
- 资源冲突


### ⚠️ V2TXLIVE_WARNING_CAMERA_OCCUPIED - 摄像头被占用

```java
public static final int V2TXLIVE_WARNING_CAMERA_OCCUPIED = -1316;
```

**含义**: 摄像头正在被占用中

**占用场景**:
- 其他应用正在使用摄像头
- 系统相机应用运行中
- 视频通话进行中


### ⚠️ V2TXLIVE_WARNING_CAMERA_NO_PERMISSION - 摄像头未授权

```java
public static final int V2TXLIVE_WARNING_CAMERA_NO_PERMISSION = -1314;
```

**含义**: 摄像头设备未授权，通常在移动设备出现，可能是权限被用户拒绝了


## 5. 麦克风相关警告码

### ⚠️ V2TXLIVE_WARNING_MICROPHONE_START_FAILED - 麦克风打开失败

```java
public static final int V2TXLIVE_WARNING_MICROPHONE_START_FAILED = -1302;
```

**含义**: 麦克风打开失败

**故障原因**:
- 硬件连接问题
- 系统音频设置异常
- 音频会话初始化失败


### ⚠️ V2TXLIVE_WARNING_MICROPHONE_OCCUPIED - 麦克风被占用

```java
public static final int V2TXLIVE_WARNING_MICROPHONE_OCCUPIED = -1319;
```

**含义**: 麦克风正在被占用中，例如移动设备正在通话时，打开麦克风会失败

**占用场景**:
- 设备正在通话中
- 其他音频应用占用麦克风
- 音频会话冲突


### ⚠️ V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION - 麦克风未授权

```java
public static final int V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION = -1317;
```

**含义**: 麦克风设备未授权，通常在移动设备出现，可能是权限被用户拒绝了


## 6. 屏幕分享相关警告码

### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED - 系统不支持屏幕分享

```java
public static final int V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED = -1309;
```

**含义**: 当前系统不支持屏幕分享


### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED - 开始录屏失败

```java
public static final int V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED = -1308;
```

**含义**: 开始录屏失败，如果在移动设备出现，可能是权限被用户拒绝了


### ⚠️ V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED - 录屏被系统中断

```java
public static final int V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED = -7001;
```

**含义**: 录屏被系统中断


## 7. 编解码相关警告码

### ⚠️ V2TXLIVE_WARNING_CURRENT_ENCODE_TYPE_CHANGED - 编码器改变更

```java
public static final int V2TXLIVE_WARNING_CURRENT_ENCODE_TYPE_CHANGED = 1104;
```

**含义**: 表示编码器发生改变，可以通过onWarning函数的扩展信息中的codec_type字段来获取当前的编码格式


### ⚠️ V2TXLIVE_WARNING_CURRENT_DECODE_TYPE_CHANGED - 解码器变更

```java
public static final int V2TXLIVE_WARNING_CURRENT_DECODE_TYPE_CHANGED = 2008;
```

**含义**: 表示解码器发生改变，可以通过onWarning函数的扩展信息中的codec_type字段来获取当前的解码格式

**注意**: Windows端不支持此错误码的扩展信息
