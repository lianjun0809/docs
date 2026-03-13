> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLivePremier API Documentation

## Feature Overview

`V2TXLivePremier` is the advanced API class in the Tencent Cloud Live Streaming (CSS) SDK. It provides global configuration and management for the SDK, including initialization, license management, environment setup, audio data callbacks, and experimental API access.

**Platform Support**: iOS, macOS  
**Feature Scope**: SDK initialization, license management, environment configuration, audio data callbacks, experimental APIs

## 📋 Table of Contents

### 1. [V2TXLivePremier APIs](#v2txlivepremier接口)
### 2. [V2TXLivePremierObserver Callback Interfaces](#v2txlivepremierobserver回调接口)

## 1. V2TXLivePremier APIs

### 🔧 getSDKVersionStr - Retrieve SDK Version

```objc
+ (NSString *)getSDKVersionStr;
```

**Description**: Returns the current SDK version as a string.

**Return Value**: 
- `NSString*`: SDK version string, for example: "10.7.0.12345"

**Typical Use Cases**:
- Checking version compatibility
- Providing version details for troubleshooting
- Reporting and monitoring

**Example**:
```objc
NSString *version = [V2TXLivePremier getSDKVersionStr];
NSLog(@"Current SDK version: %@", version);
```

### setObserver - Set Global Callback Interface

```objc
+ (void)setObserver:(id<V2TXLivePremierObserver>)observer;
```

**Parameters**:
- `observer`: Object conforming to the V2TXLivePremierObserver protocol

**Usage Recommendation**: Set the observer once during app startup. The observer remains active throughout the app lifecycle.

**Notes**:
- Set the observer only once at startup.
- Ensure the observer object is valid for the entire app lifecycle.

### setLogConfig - Configure Logging

```objc
+ (V2TXLiveCode)setLogConfig:(V2TXLiveLogConfig *)config;
```

**Parameters**:
- `config`: Log configuration object (log level, storage path, etc.)

**Usage Recommendation**: Configure logging at app startup for global effect.

**Typical Use Cases**:
- Enable detailed logging for debugging
- Minimize log output in production
- Customize log storage location

**Example**:
```objc
V2TXLiveLogConfig *logConfig = [[V2TXLiveLogConfig alloc] init];
logConfig.enableConsole = YES;
logConfig.enableLogFile = YES;
logConfig.enableObserver = YES;
logConfig.logLevel = V2TXLiveLogLevelAll;
[V2TXLivePremier setObserver:self];
[V2TXLivePremier setLogConfig:logConfig];
```

### setEnvironment - Select SDK Access Environment

```objc
+ (V2TXLiveCode)setEnvironment:(const char *)env;
```

**Parameters**:
- `env`: Environment identifier. Options:
  - `"default"`: Default environment; SDK automatically selects the best global access point
  - `"GDPR"`: GDPR-compliant environment; audio/video data does not route through servers in mainland China

**Note**: Only use this API if you have specific environment requirements.

### setLicence - Set SDK License

```objc
+ (void)setLicence:(NSString *)url key:(NSString *)key;
```

**Parameters**:
- `url`: License URL
- `key`: License key

**Usage Recommendation**: Set the license during app startup. You must configure the license before starting stream publishing or playback.

**Reference Documentation**: https://cloud.tencent.com/document/product/454/34750

**Example**:
```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [V2TXLivePremier setObserver:self];
    [V2TXLivePremier setLicence:@"your_licence_url" key:@"your_licence_key"];
    return YES;
}

#pragma mark - V2TXLivePremierObserver
- (void)onLicenceLoaded:(int)result Reason:(NSString *)reason {
    if (result == 0) {
        NSLog(@"Licence loaded successfully, %@", reason);
    } else if (result == -4) {
        NSLog(@"Licence package name mismatch, %@", reason);
    } else if (result == -11) {
        NSLog(@"Licence expired, %@", reason);
    } else {
        NSLog(@"Licence other error, %@", reason);
    }
}
```

### setSocks5Proxy - Configure SOCKS5 Proxy

```objc
+ (V2TXLiveCode)setSocks5Proxy:(NSString *)host 
                          port:(NSInteger)port 
                      username:(NSString *)username 
                      password:(NSString *)password 
                        config:(V2TXLiveSocks5ProxyConfig *)config;
```

**Parameters**:
- `host`: SOCKS5 proxy server address
- `port`: SOCKS5 proxy server port
- `username`: Proxy username
- `password`: Proxy password
- `config`: SOCKS5 proxy configuration object

**Usage Recommendation**: Configure the proxy during app startup.

### enableAudioCaptureObserver - Enable/Disable Audio Capture Callback

```objc
+ (V2TXLiveCode)enableAudioCaptureObserver:(BOOL)enable 
                                   format:(V2TXLiveAudioFrameObserverFormat *)format;
```

**Parameters**:
- `enable`: Enable or disable callback (default: NO)
- `format`: Audio frame callback format

**Usage Recommendation**: Call before invoking `V2TXLivePusher#startPush`.

### enableAudioPlayoutObserver - Enable/Disable Mixed Audio Playback Callback

```objc
+ (V2TXLiveCode)enableAudioPlayoutObserver:(BOOL)enable 
                                  format:(V2TXLiveAudioFrameObserverFormat *)format;
```

**Parameters**:
- `enable`: Enable or disable callback (default: NO)
- `format`: Audio frame callback format

**Technical Details**:
- Audio frame duration: 0.02s (fixed)
- PCM audio format
- Data includes all mixed playback audio streams

### enableVoiceEarMonitorObserver - Enable/Disable Ear Monitor Audio Callback

```objc
+ (V2TXLiveCode)enableVoiceEarMonitorObserver:(BOOL)enable;
```

**Parameters**:
- `enable`: Enable or disable callback (default: NO)

**Technical Details**:
- Audio frame duration: variable
- PCM audio format
- Dedicated ear monitor audio stream

### setUserId - Set User Identifier

```objc
+ (void)setUserId:(NSString *)userId;
```

**Parameters**:
- `userId`: User or device identifier managed by your business logic

**Usage Recommendation**: Set during app startup.

### callExperimentalAPI - Invoke Experimental API

```objc
+ (V2TXLiveCode)callExperimentalAPI:(NSString *)jsonStr;
```

**Parameters**:
- `jsonStr`: JSON string specifying the API and parameters

**Return Value**:
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Invalid parameter

## 2. V2TXLivePremierObserver Callback Interfaces

### onLog - Custom Log Output

```objc
- (void)onLog:(V2TXLiveLogLevel)level log:(NSString *)log;
```

**Parameters**:
- `level`: Log level
- `log`: Log message

**Typical Use Cases**:
- Custom log processing
- Redirect logs to external systems
- Filter and format log output

### onLicenceLoaded - License Load Result

```objc
- (void)onLicenceLoaded:(int)result Reason:(NSString *)reason;
```

**Parameters**:
- `result`: Result code (0 for success, negative values indicate failure)
- `reason`: Failure reason

### onCaptureAudioFrame - Microphone Audio Data Callback

```objc
- (void)onCaptureAudioFrame:(V2TXLiveAudioFrame *)frame;
```

**Parameters**:
- `frame`: Captured audio data frame

**Important Notes**:
- Avoid time-consuming operations in this callback
- You can modify the audio data
- Frame duration is 0.02s (fixed)
- Does not include background music, sound effects, or pre-processing
- Ultra-low latency

### onPlayoutAudioFrame - Mixed Playback Audio Data Callback

```objc
- (void)onPlayoutAudioFrame:(V2TXLiveAudioFrame *)frame;
```

**Parameters**:
- `frame`: PCM audio data frame

**Important Notes**:
- Frame duration is 0.02s (fixed)
- Data is readable and writable; ensure efficient processing
- Ear monitor audio is not included

### onVoiceEarMonitorAudioFrame - Ear Monitor Audio Data Callback

```objc
- (void)onVoiceEarMonitorAudioFrame:(V2TXLiveAudioFrame *)frame;
```

**Parameters**:
- `frame`: PCM audio data frame

**Important Notes**:
- Frame duration is variable
- Data is readable and writable; ensure efficient processing