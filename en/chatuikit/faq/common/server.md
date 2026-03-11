> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

---
product: 'Chat'
tech_stack: 'server'
framework: 'common'
title: 'Common Issues Knowledge Base'
keywords: ['console', 'server-side userSig generation', 'restapi', 'pre-callback', 'post-callback', 'nodejs/go/java/python and other server-side language userSig generation example code']
---

# Common Issues Knowledge Base

## UserSig Solutions

### Q: How to generate userSig on the server side?
**A:** For specific methods of generating userSig on the server side, please refer to: https://trtc.io/document/34385?product=chat&menulabel=uikit&platform=react. The documentation provides solutions for multiple server-side languages.

### Q: What's the difference in message format between pre-send and post-send callbacks in Chat? How to distinguish system messages from user messages?
**A:** 
1. Group message pre-send callback content does not include MsgSeq, MsgTime and other information. For details, please refer to the following documentation:
- One-to-one pre-send callback: https://trtc.io/document/34364?product=chat&menulabel=uikit&platform=react
- One-to-one post-send callback: https://trtc.io/document/34365?product=chat&menulabel=uikit&platform=react
- Group pre-send callback: https://trtc.io/document/34374?product=chat&menulabel=uikit&platform=react
- Group post-send callback: https://trtc.io/document/34375?product=chat&menulabel=uikit&platform=react
2. Normal message format: https://trtc.io/document/33527?product=chat&menulabel=uikit&platform=react

### Q: What are group message priorities and group message frequency controls?
**A:** Group messages are divided into 3 priorities (`High`, `Normal`, `Low`). If messages in a group exceed the frequency limit, the backend will prioritize delivering high-priority messages. Therefore, users should choose an appropriate priority based on the importance of the message. Total message frequency control refers to the limit on the maximum number of messages that can be sent per second across all endpoints for a single group. The default value is 40 messages/second, using average frequency limiting per second. When the number of messages exceeds the limit, the backend prioritizes delivering messages with relatively higher priority, and messages with the same priority are randomly ordered.

### Q: How to intercept messages sent by users?
**A:** Business servers can intercept through pre-send callbacks. For specific documentation, please refer to:
- One-to-one pre-send callback: https://trtc.io/document/34364?product=chat&menulabel=uikit&platform=react
- Group pre-send callback: https://trtc.io/document/34375?product=chat&menulabel=uikit&platform=react

### Q: How to delete and manage accounts?
**A:** REST API can be used to delete, import, and query accounts. For specific documentation, please refer to:
- Delete account: https://trtc.io/document/34955?product=chat&menulabel=uikit&platform=react
- Import single account: https://trtc.io/document/34953?product=chat&menulabel=uikit&platform=react
- Import multiple accounts: https://trtc.io/document/34954?product=chat&menulabel=uikit&platform=react
- Query account: https://trtc.io/document/34956?product=chat&menulabel=uikit&platform=react

### Q: How to handle when the number of accounts exceeds the limit?
**A:** When importing accounts, if the number of accounts exceeds the limit and you need to create more than 100 accounts, you need to upgrade your application to the Professional Edition. For specific operation instructions, please refer to: https://trtc.io/document/55096.

### Q: How to delete conversations on the server side?
**A:** Server-side conversation deletion can be done using REST API. For specific documentation, please refer to: https://trtc.io/document/34348?product=chat&menulabel=uikit&platform=react.
