> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLivePremier API Documentation

## Feature Overview

`V2TXLivePremier` is the advanced interface for the Tencent Cloud Live Streaming (CSS) SDK, offering global configuration and management for the SDK.

**File Path**: `com/tencent/live2/V2TXLivePremier.java`  
**Platform Support**: Android  
**Feature Scope**: SDK initialization, license management, environment configuration

## 📋 Table of Contents

### 1. [V2TXLivePremier APIs](#v2txlivepremier接口)
### 2. [V2TXLivePremierObserver Callback Interface](#v2txlivepremierobserver回调接口)

## 1. V2TXLivePremier APIs

### getSDKVersionStr() - Retrieve SDK Version
```java
public static String getSDKVersionStr()
```

**Return Value**: Returns the SDK version as a string, for example: "10.7.0.12345"

**When to Call**: Can be called at any time

**Typical Use Cases**:
- Checking version compatibility
- Providing version information for troubleshooting
- Collecting statistics and monitoring

**Example**:
```java
String version = V2TXLivePremier.getSDKVersionStr();
Log.i(TAG, "Current SDK version: " + version);
```

### setObserver() - Set Global Callback Interface
```java
public static void setObserver(V2TXLivePremierObserver observer)
```

**Parameters**:
- `observer`: An object that implements the V2TXLivePremierObserver interface

**When to Call**: Set this during app startup; applies globally

**Notes**:
- Set the observer once at app startup
- The observer instance must remain valid for the entire app lifecycle

### setLogConfig() - Configure Logging
```java
public static void setLogConfig(V2TXLiveDef.V2TXLiveLogConfig config)
```

**Parameters**:
- `config`: Log configuration object, including log level, storage path, and other settings

**When to Call**: Set during app startup; applies globally

**Typical Use Cases**:
- Enable detailed logs for debugging
- Reduce log output in production
- Customize the log storage path

**Example**:
```java
V2TXLiveLogConfig logConfig = new V2TXLiveDef.V2TXLiveLogConfig();
logConfig.enableConsole = true;
logConfig.enableLogFile = true;
logConfig.enableObserver = true;
logConfig.logLevel = V2TXLiveLogLevel.V2TXLiveLogLevelAll;
V2TXLivePremier.setObserver(new V2TXLivePremier.V2TXLivePremierObserver() {
    @Override
    public void onLog(int level, String log) {
        // doSomething
    }
});
```

### setEnvironment() - Set SDK Access Environment
```java
public static void setEnvironment(String env)
```

**Parameters**:
- `env`: Environment identifier. Supported values:
  - `"default"`: Default environment; the SDK automatically selects the optimal global access point
  - `"GDPR"`: GDPR environment; audio and video data will not pass through servers in Mainland China

**Note**: Only use this API if you have specific requirements

### setLicence() - Set SDK License

```java
public static void setLicence(Context context, String url, String key)
```

**Parameters**:
- `context`: Android context
- `url`: License URL
- `key`: License key

**When to Call**: Must be called during app startup and before starting any streaming or publishing

**Documentation**: https://cloud.tencent.com/document/product/454/34750

**Example**:
```java
public class MyApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        V2TXLivePremier.setObserver(new V2TXLivePremierObserver() {
            @Override
            public void onLicenceLoaded(int result, String reason) {
                if (result == 0) {
                    Log.i(TAG, "License loaded successfully, " + reason);
                } else if (result == -4) {
                    Log.e(TAG, "License package name mismatch, " + reason);
                } else if (result == -11) {
                    Log.e(TAG, "License expired, " + reason);
                } else {
                    Log.e(TAG, "Other license error, " + reason);
                }
            }
        });
        V2TXLivePremier.setLicence(this, "url", "key");
    }
}
```

### setSocks5Proxy() - Configure Socks5 Proxy

```java
public static void setSocks5Proxy(String host, int port, String username, String password, V2TXLiveDef.V2TXLiveSocks5ProxyConfig config)
```

**Parameters**:
- `host`: Socks5 proxy server address
- `port`: Socks5 proxy server port
- `username`: Proxy server username
- `password`: Proxy server password
- `config`: Socks5 proxy configuration

**When to Call**: Set during app startup

### enableAudioCaptureObserver() - Enable or Disable Audio Capture Callback
```java
public static void enableAudioCaptureObserver(boolean enable, V2TXLiveDef.V2TXLiveAudioFrameObserverFormat format)
```

**Parameters**:
- `enable`: Enable or disable the callback (default: false)
- `format`: Audio frame callback format

**When to Call**: Must be called before `V2TXLivePusher#startPush`

---

### enableAudioPlayoutObserver() - Enable or Disable Final Audio Playback Callback
```java
public static void enableAudioPlayoutObserver(boolean enable, V2TXLiveDef.V2TXLiveAudioFrameObserverFormat format)
```

**Parameters**:
- `enable`: Enable or disable the callback (default: false)
- `format`: Audio frame callback format

**Technical Details**:
- Audio frame duration is fixed at 0.02s
- PCM format audio data
- Callback provides mixed audio data for playback

### enableVoiceEarMonitorObserver() - Enable or Disable Ear Monitor Audio Callback
```java
public static void enableVoiceEarMonitorObserver(boolean enable)
```

**Parameters**:
- `enable`: Enable or disable the callback (default: false)

### setUserId() - Set User ID
```java
public static void setUserId(String userId)
```

**Parameters**:
- `userId`: User or device ID managed by your application logic

**When to Call**: Set during app startup

### callExperimentalAPI() - Invoke Experimental API
```java
public static int callExperimentalAPI(String jsonStr)
```

**Parameters**:
- `jsonStr`: JSON string describing the API and its parameters

**Return Values**:
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Invalid parameter

## 2. V2TXLivePremierObserver Callback Interface

### onLog() - Custom Log Callback
```java
public void onLog(int level, String log)
```

**Parameters**:
- `level`: Log level
- `log`: Log message

**Typical Use Cases**:
- Custom log processing
- Redirect logs to your own logging system
- Log filtering and formatting

### onLicenceLoaded() - License Load Callback
```java
public void onLicenceLoaded(int result, String reason)
```

**Parameters**:
- `result`: Result code (0 for success, negative values indicate failure)
- `reason`: Reason for failure

### onCaptureAudioFrame() - Local Microphone Audio Callback
```java
public void onCaptureAudioFrame(V2TXLiveDef.V2TXLiveAudioFrame frame)
```

**Parameters**:
- `frame`: Audio data frame

**Important Notes**:
- Avoid time-consuming operations in this callback
- Audio data can be modified
- Frame duration is fixed at 0.02s
- Does not include background music, sound effects, or other pre-processing
- Ultra-low latency

### onPlayoutAudioFrame() - Mixed Audio Playback Callback
```java
public void onPlayoutAudioFrame(V2TXLiveDef.V2TXLiveAudioFrame frame)
```

**Parameters**:
- `frame`: PCM format audio data frame

**Important Notes**:
- Frame duration is fixed at 0.02s
- Data is readable and writable; ensure timely processing
- Does not include ear monitor audio data

### onVoiceEarMonitorAudioFrame() - Ear Monitor Audio Callback

```java
public void onVoiceEarMonitorAudioFrame(V2TXLiveDef.V2TXLiveAudioFrame frame)
```

**Parameters**:
- `frame`: PCM format audio data frame

**Important Notes**:
- Frame duration may vary
- Data is readable and writable; ensure timely processing