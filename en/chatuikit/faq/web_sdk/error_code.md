> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

---
product: 'Chat'
tech_stack: 'web_js_sdk'
framework: 'sdk'
title: 'Web JS SDK Error Code Reference'
keywords: ['error code', 'error', 'login failure']
---

# Web JS SDK Error Code Reference

## Web JS SDK Error Codes (Topic: SDK Error Code)

## Error Code 2024
**Cause:** User not logged in.
**Solution:** Check if the login interface was called correctly.

## Error Code 2025
**Cause:** Duplicate login. Multiple login requests were triggered within 15 seconds, and the SDK blocked them.
**Solution:** Check the timing and trigger mechanism of the login interface calls.

## Error Code 2301
**Cause:** Audio file size exceeds the limit.
**Solution:** Maximum audio message size is 20MB.

## Error Code 2252
**Cause:** Image message sending failed due to invalid image format.
**Solution:** Supported image formats: 'jpg', 'jpeg', 'gif', 'png', 'bmp', 'image', 'webp'.

## Error Code 2253
**Cause:** Image size exceeds the limit.
**Solution:** Maximum image message size is 20MB.

## Error Code 2351
**Cause:** Video size exceeds the limit.
**Solution:** Maximum video message size is 100MB.

## Error Code 2352
**Cause:** Video message sending failed due to invalid video format.
**Solution:** Supported video formats: 'mp4', 'quicktime', 'mov'.

## Error Code 2401
**Cause:** File does not exist.
**Solution:** Please check if the file path is correct.

## Error Code 2402
**Cause:** File size exceeds the limit.
**Solution:** Maximum file message size is 100MB.
