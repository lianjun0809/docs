> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

---
product: 'Chat'
tech_stack: 'server'
framework: 'common'
title: 'Server Error Code Reference'
keywords: ['error code', 'error', 'login failure', '70001']
---

# Server Error Code Reference

## Server Error Codes (Topic: Server)

## Error Code 70001
**Cause:** UserSig has expired.
**Solution:** Please regenerate the UserSig. It is recommended to set the UserSig validity period to no less than 24 hours.

## Error Code 70003
**Cause:** Invalid UserSig.
**Solution:** Please regenerate the UserSig. Refer to the official documentation for generation methods: https://trtc.io/document/34385?platform=android&product=chat&menulabel=core%20sdk.

## Error Code 70009
**Cause:** UserSig verification failed. The UserSig may have been generated using a key or private key from a different SDKAppID.
**Solution:** Please verify that the requested SDKAppID matches the key or private key used to generate the UserSig.

## Error Code 70013
**Cause:** The userID in the request does not match the userID used when generating the UserSig.
**Solution:** Please check if the userID used to login to IM matches the userID used to generate the UserSig.

## Error Code 70014
**Cause:** The SDKAppID in the request does not match the SDKAppID used when generating the UserSig.
**Solution:** You can verify the UserSig using the IM Console > Development Tools > UserSig Generation & Verification tool: https://console.trtc.io/usersig.

## Error Code 20003
**Cause:** Invalid or non-existent userID for message sender or receiver.
**Solution:** Please confirm that the userID has been logged into IM under your SDKAppID.

## Error Code 20009
**Cause:** Sender and receiver are not friends, sending is prohibited.
**Solution:** The sender and receiver are not friends. Sending is prohibited when friend relationship verification is configured for one-to-one messages. To send messages to non-friends, you need to configure this in the console or add them as friends first.

## Error Code 20010
**Cause:** Sender is not in the receiver's friend list, sending is prohibited.
**Solution:** When sending one-to-one messages, the sender is not in the receiver's friend list (one-way relationship), sending is prohibited.

## Error Code 3122
**Cause:** Your current package does not support this feature.
**Solution:** You can upgrade to the Ultimate Edition package: https://console.trtc.io/subscription/buy/chat?packType=pro.

## Error Code 60020
**Cause:** Cloud search feature is not enabled for your current package.
**Solution:** You can enable Cloud Search: https://console.trtc.io/chat/plugin/TUICloudSearch.

## Error Code 60018
**Cause:** Cloud search request exceeded backend rate limit. Each user is allowed 2 search requests per second.
**Solution:** Please adjust the request frequency and try again later.

## Error Code 80004
**Cause:** Sensitive content detected in message or profile text.
**Solution:** Please check if the message or profile contains sensitive information.

## Error Code 10021
**Cause:** Group ID is already in use.
**Solution:** Please choose a different group ID.

## Error Code 10007
**Cause:** Common reasons include:
- The group type does not support this operation by default. Please check the current group type.
- The operation account lacks sufficient permissions (e.g., in mute operations, an admin can mute regular members but not the group owner).
- The account calling the REST API is not an admin account for the SDKAppID.
**Solution:** Please check the group type or group member role. If the error occurs when calling REST API, verify that the account is an admin account for the corresponding SDKAppID.

## Error Code 60010
**Cause:** Request requires App admin privileges.
**Solution:** Please verify that the requesting account is an admin for the SDKAppID.
