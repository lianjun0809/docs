> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

# Tencent Cloud Live Streaming SDK V2TXLivePremier API Documentation

## Feature Overview

`V2TXLivePremier` is the advanced interface for the Tencent Cloud Live Streaming (CSS) SDK. It provides global configuration and management for the SDK.

**File Path**: `v2_tx_live_premier.dart`  
**Platform Support**: Flutter  
**Feature Scope**: SDK initialization, license management, environment configuration

## 📋 Table of Contents

### 1. [V2TXLivePremier API](#v2txlivepremier接口)
### 2. [V2TXLivePremierObserver Callback Interface](#v2txlivepremierobserver回调接口)

## 1. V2TXLivePremier API

### Get SDK Version
```dart
static Future<String> getSDKVersionStr() async
```

**Return Value**: SDK version string, e.g., "10.7.0.12345"

**When to Use**: No restrictions

**Typical Use Cases**:
- Checking version compatibility
- Providing version details for troubleshooting
- Reporting and monitoring

**Example**:
```dart
String version = await V2TXLivePremier.getSDKVersionStr();
print('Current SDK version: $version');
```

### Set Observer Callback
```dart
static Future<void> setObserver(V2TXLivePremierObserver? observer) async
```

**Parameter**:
- `observer`: An object that implements the V2TXLivePremierObserver protocol

**When to Use**: Set at app startup for global effect

**Notes**:
- Set the observer once during app startup
- The observer object must remain valid for the entire app lifecycle

**Example**:
```dart
await V2TXLivePremier.setObserver((type, params) {
  switch (type) {
    case V2TXLivePremierObserverType.onLog:
      print('Log output: ${params['log']}');
      break;
    case V2TXLivePremierObserverType.onLicenceLoaded:
      print('Licence load result: ${params['result']}');
      break;
  }
});
```

### Configure SDK Environment
```dart
static Future<V2TXLiveCode> setEnvironment(String env) async
```

**Parameter**:
- `env`: Environment identifier. Options:
  - `"default"`: Default environment; SDK automatically selects the optimal access point
  - `"GDPR"`: GDPR-compliant environment; audio/video data does not pass through Mainland China servers

**Note**: Only call this API if you have specific requirements.

**Example**:
```dart
// Call only if GDPR compliance is required
await V2TXLivePremier.setEnvironment("GDPR");
```

### Set License Authorization
```dart
static Future<void> setLicence(String url, String key) async
```

**Parameters**:
- `url`: License URL
- `key`: License key

**When to Use**: Call at app startup, before any streaming or playback

**Documentation**: https://cloud.tencent.com/document/product/454/34750

**Example**:
```dart
class MyApplication extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Set license during app startup
    WidgetsBinding.instance.addPostFrameCallback((_) async {
      await V2TXLivePremier.setObserver((type, params) {
        if (type == V2TXLivePremierObserverType.onLicenceLoaded) {
          int result = params?['result'] ?? -1;
          String reason = params?['reason'] ?? '';
          
          if (result == 0) {
            print('Licence loaded successfully, $reason');
          } else if (result == -4) {
            print('Licence package name mismatch, $reason');
          } else if (result == -11) {
            print('Licence expired, $reason');
          } else {
            print('Licence other error, $reason');
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

### Call Experimental API
```dart
static Future<V2TXLiveCode> callExperimentalAPI(String jsonStr) async
```

**Parameter**:
- `jsonStr`: JSON string describing the API and its parameters

**Return Value**:
- `V2TXLIVE_OK`: Success
- `V2TXLIVE_ERROR_INVALID_PARAMETER`: Invalid parameter

**Example**:
```dart
String jsonParams = '{"api": "test", "param": "value"}';
V2TXLiveCode result = await V2TXLivePremier.callExperimentalAPI(jsonParams);
if (result == V2TXLiveCode.V2TXLIVE_OK) {
  print('Experimental API call succeeded');
}
```

## 2. V2TXLivePremierObserver Callback Interface

### Log Output Callback
```dart
void Function(V2TXLivePremierObserverType type, Map<String, dynamic>? params)
```

**Parameters**:
- `type`: Callback type, should be `V2TXLivePremierObserverType.onLog`
- `params`: Contains `level` and `log`

**Use Cases**:
- Custom log processing
- Redirect logs to external systems
- Log filtering and formatting

**Example**:
```dart
V2TXLivePremier.setObserver((type, params) {
  if (type == V2TXLivePremierObserverType.onLog) {
    int level = params?['level'] ?? 0;
    String log = params?['log'] ?? '';
    
    // Custom log handling
    if (level >= V2TXLiveLogLevel.V2TXLiveLogLevelWarning) {
      print('Warning log: $log');
    } else {
      print('Normal log: $log');
    }
  }
});
```

### License Load Callback
```dart
void Function(V2TXLivePremierObserverType type, Map<String, dynamic>? params)
```

**Parameters**:
- `type`: Callback type, should be `V2TXLivePremierObserverType.onLicenceLoaded`
- `params`: Contains `result` and `reason`

**Example**:
```dart
V2TXLivePremier.setObserver((type, params) {
  if (type == V2TXLivePremierObserverType.onLicenceLoaded) {
    int result = params?['result'] ?? -1;
    String reason = params?['reason'] ?? '';
    
    if (result == 0) {
      print('Licence loaded successfully: $reason');
    } else {
      print('Licence load failed ($result): $reason');
    }
  }
});
```

## Code Examples

### SDK Initialization Example
```dart
import 'package:flutter/material.dart';
import 'package:tencent_trtc/v2_tx_live_premier.dart';
import 'package:tencent_trtc/v2_tx_live_def.dart';

class MyApplication extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Initialize SDK at app startup
    WidgetsBinding.instance.addPostFrameCallback((_) async {
      await SDKManager.initializeSDK();
    });
    
    return MaterialApp(
      title: 'Tencent Cloud Live Streaming SDK Example',
      home: MyHomePage(),
    );
  }
}

class SDKManager {
  static Future<void> initializeSDK() async {
    try {
      // 1. Register observer callback
      await V2TXLivePremier.setObserver((type, params) {
        switch (type) {
          case V2TXLivePremierObserverType.onLog:
            int level = params?['level'] ?? 0;
            String log = params?['log'] ?? '';
            
            // Handle logs by level
            if (level >= V2TXLiveLogLevel.V2TXLiveLogLevelWarning) {
              print('⚠️ Warning log: $log');
            } else if (level >= V2TXLiveLogLevel.V2TXLiveLogLevelInfo) {
              print('ℹ️ Info log: $log');
            } else {
              print('🔍 Debug log: $log');
            }
            break;
            
          case V2TXLivePremierObserverType.onLicenceLoaded:
            int result = params?['result'] ?? -1;
            String reason = params?['reason'] ?? '';
            
            if (result == 0) {
              print('✅ Licence loaded successfully: $reason');
            } else if (result == -4) {
              print('❌ Licence package name mismatch: $reason');
            } else if (result == -11) {
              print('❌ Licence expired: $reason');
            } else {
              print('❌ Licence load failed ($result): $reason');
            }
            break;
        }
      });
      
      // 2. Set license (required)
      await V2TXLivePremier.setLicence("your_licence_url", "your_licence_key");
      
      // 3. Get SDK version
      String version = await V2TXLivePremier.getSDKVersionStr();
      print('📦 SDK version: $version');
      
      print('🎉 SDK initialization complete');
      
    } catch (e) {
      print('❌ SDK initialization exception: $e');
    }
  }
}
```

#### Experimental API Example
```dart
class ExperimentalAPI {
  static Future<void> testExperimentalAPI() async {
    try {
      // Call experimental API
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
        print('✅ Experimental API call succeeded');
      } else if (result == V2TXLiveCode.V2TXLIVE_ERROR_INVALID_PARAMETER) {
        print('❌ Experimental API parameter error');
      } else {
        print('❌ Experimental API call failed: $result');
      }
      
    } catch (e) {
      print('❌ Experimental API call exception: $e');
    }
  }
}
```

## Notes

### License Authorization Management
- **Required**: Call `setLicence()` before using the SDK; otherwise, features will be restricted
- **Timing**: Set during app startup, before any streaming or playback
- **Error Handling**: Monitor authorization status with the `onLicenceLoaded` callback

### Callback Registration Timing
- **Early Registration**: Register observer callbacks before SDK initialization
- **Single Registration**: Set only once at app startup
- **Lifecycle**: The observer object must remain valid throughout the app lifecycle

### Thread Safety
- **Main Thread Execution**: All callbacks in Flutter run on the UI main thread
- **No Thread Handling Required**: No extra thread synchronization needed
- **Async Safety**: Ensure asynchronous operations are handled correctly

### Memory Management
- **Timely Removal**: Remove observers when no longer needed
- **Avoid Cyclic References**: Do not hold strong references to the SDK in callbacks
- **Resource Release**: Release all resources when the app exits

### Log Configuration
- **Debug Phase**: Enable detailed logs for troubleshooting
- **Production Environment**: Reduce log output for better performance
- **Custom Handling**: Use the `onLog` callback for custom log processing

### Environment Configuration
- **Default Environment**: Use unless you have special requirements
- **GDPR Environment**: Use only if GDPR compliance is required
- **Proxy Settings**: Configure only if proxy access is needed

## Best Practices

### License Setup Best Practices
```dart
class LicenceManager {
  static Future<bool> setupLicence() async {
    try {
      // Register license callback
      await V2TXLivePremier.setObserver((type, params) {
        if (type == V2TXLivePremierObserverType.onLicenceLoaded) {
          int result = params?['result'] ?? -1;
          String reason = params?['reason'] ?? '';
          
          if (result == 0) {
            print('✅ License authorized successfully');
          } else {
            print('❌ License authorization failed ($result): $reason');
            // Show user-friendly error messages based on error code
            showLicenceErrorDialog(result, reason);
          }
        }
      });
      
      // Set license
      await V2TXLivePremier.setLicence("your_licence_url", "your_licence_key");
      return true;
      
    } catch (e) {
      print('❌ License setup exception: $e');
      return false;
    }
  }
  
  static void showLicenceErrorDialog(int result, String reason) {
    // Show error message based on error code
    String message = '';
    switch (result) {
      case -4:
        message = 'App package name mismatch. Please check your license configuration.';
        break;
      case -11:
        message = 'License expired. Please renew your license.';
        break;
      default:
        message = 'License configuration error: $reason';
        break;
    }
    
    // Display error dialog
    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: Text('License Error'),
        content: Text(message),
        actions: [
          TextButton(
            onPressed: () => Navigator.pop(context),
            child: Text('OK'),
          ),
        ],
      ),
    );
  }
}
```

## FAQs

### Q: How do I troubleshoot license setup failures?
A: Check the following:
1. Is the license URL and key correct?
2. Does the app package name match the license configuration?
3. Is the license still valid?
4. Is the network connection working?

### Q: What if the log file becomes too large?
A: Recommendations:
1. Use a higher log level in production
2. Clean up log files regularly
3. Use custom log callbacks to filter logs

### Q: How do I test experimental APIs?
A: Recommendations:
1. Use in a test environment
2. Review API documentation carefully
3. Handle exceptions appropriately
4. Provide feedback on your experience