> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## 概述

ContactList 是一个高度可配置的联系人列表组件。该组件支持好友列表、群组列表、黑名单和申请管理，提供分组折叠、搜索过滤、自定义渲染等核心功能，适用于即时通讯、社交应用等场景的联系人管理界面。

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/e81dc6d883b511f0b6b0525400bf7822.png)


## ContactList Props
<table>
<tr>
<td rowspan="1" colSpan="1" >字段</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >activeContactItem</td>

<td rowspan="1" colSpan="1" >ContactGroupItem \| undefined</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >当前激活的联系人项</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableSearch</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >是否启用搜索功能</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >groupConfig</td>

<td rowspan="1" colSpan="1" >Partial<Record<ContactItemType, CustomGroupConfig>></td>

<td rowspan="1" colSpan="1" >{}</td>

<td rowspan="1" colSpan="1" >自定义分组配置</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >searchPlaceholder</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >'Search contacts'</td>

<td rowspan="1" colSpan="1" >搜索框占位符文本</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >emptyText</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >'No contacts'</td>

<td rowspan="1" colSpan="1" >空状态提示文本</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ContactItem</td>

<td rowspan="1" colSpan="1" >Component \| undefined</td>

<td rowspan="1" colSpan="1" >ContactListItem</td>

<td rowspan="1" colSpan="1" >自定义联系人项组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ContactSearchComponent</td>

<td rowspan="1" colSpan="1" >Component \| undefined</td>

<td rowspan="1" colSpan="1" >ContactSearch</td>

<td rowspan="1" colSpan="1" >自定义搜索组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GroupHeader</td>

<td rowspan="1" colSpan="1" >Component \| undefined</td>

<td rowspan="1" colSpan="1" >默认分组头</td>

<td rowspan="1" colSpan="1" >自定义分组头部组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderEmptyList</td>

<td rowspan="1" colSpan="1" >Component \| undefined</td>

<td rowspan="1" colSpan="1" >默认空状态</td>

<td rowspan="1" colSpan="1" >自定义空状态组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onContactItemClick</td>

<td rowspan="1" colSpan="1" >(item: ContactGroupItem) => void</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >联系人项点击事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onFriendApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: FriendApplication) => void</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >好友申请操作事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onGroupApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: GroupApplication) => void</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >群组申请操作事件</td>
</tr>
</table>


## ContactList Events
<table>
<tr>
<td rowspan="1" colSpan="1" >事件名</td>

<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >contact-item-click</td>

<td rowspan="1" colSpan="1" >(item: ContactGroupItem)</td>

<td rowspan="1" colSpan="1" >联系人项点击事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >friend-application-action</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: FriendApplication)</td>

<td rowspan="1" colSpan="1" >好友申请操作事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >group-application-action</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: GroupApplication)</td>

<td rowspan="1" colSpan="1" >群组申请操作事件</td>
</tr>
</table>


## ContactInfo Props
<table>
<tr>
<td rowspan="1" colSpan="1" >字段</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >默认值</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >contactItem</td>

<td rowspan="1" colSpan="1" >ContactGroupItem \| undefined</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >当前显示的联系人项</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >showActions</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >是否显示操作按钮</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderEmpty</td>

<td rowspan="1" colSpan="1" >Component \| undefined</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >空状态占位组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >FriendInfoComponent</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >FriendInfo</td>

<td rowspan="1" colSpan="1" >好友信息组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GroupInfoComponent</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >GroupInfo</td>

<td rowspan="1" colSpan="1" >群组信息组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >BlacklistInfoComponent</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >BlacklistInfo</td>

<td rowspan="1" colSpan="1" >黑名单信息组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >FriendApplicationInfoComponent</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >FriendApplicationInfo</td>

<td rowspan="1" colSpan="1" >好友申请信息组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GroupApplicationInfoComponent</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >GroupApplicationInfo</td>

<td rowspan="1" colSpan="1" >群组申请信息组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchGroupInfoComponent</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >SearchGroupInfo</td>

<td rowspan="1" colSpan="1" >搜索群组信息组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchUserInfoComponent</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >SearchUserInfo</td>

<td rowspan="1" colSpan="1" >搜索用户信息组件</td>
</tr>
</table>


## ContactInfo Events
<table>
<tr>
<td rowspan="1" colSpan="1" >事件名</td>

<td rowspan="1" colSpan="1" >参数</td>

<td rowspan="1" colSpan="1" >描述</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >close</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >关闭信息面板事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sendMessage</td>

<td rowspan="1" colSpan="1" >(friend: Friend)</td>

<td rowspan="1" colSpan="1" >发送消息事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >deleteFriend</td>

<td rowspan="1" colSpan="1" >(friend: Friend)</td>

<td rowspan="1" colSpan="1" >删除好友事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >addToBlacklist</td>

<td rowspan="1" colSpan="1" >(friend: Friend)</td>

<td rowspan="1" colSpan="1" >添加到黑名单事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >removeFromBlacklist</td>

<td rowspan="1" colSpan="1" >(profile: UserProfile)</td>

<td rowspan="1" colSpan="1" >从黑名单移除事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >updateFriendRemark</td>

<td rowspan="1" colSpan="1" >(friend: Friend)</td>

<td rowspan="1" colSpan="1" >更新好友备注事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enterGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel)</td>

<td rowspan="1" colSpan="1" >进入群组事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >leaveGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel)</td>

<td rowspan="1" colSpan="1" >退出群组事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >dismissGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel)</td>

<td rowspan="1" colSpan="1" >解散群组事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >friendApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: FriendApplication)</td>

<td rowspan="1" colSpan="1" >好友申请操作事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >groupApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: GroupApplication)</td>

<td rowspan="1" colSpan="1" >群组申请操作事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >addFriend</td>

<td rowspan="1" colSpan="1" >(user: UserProfile, wording: string)</td>

<td rowspan="1" colSpan="1" >添加好友事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >joinGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel, note: string)</td>

<td rowspan="1" colSpan="1" >加入群组事件</td>
</tr>
</table>


## 基础用法
``` typescript
<template>
  <div class="contact-container">
    <ContactList />
    <ContactInfo />
  </div>
</template>

<script setup lang="ts">
import { ContactList, ContactInfo } from '@tencentcloud/chat-uikit-vue3';
</script>

<style scoped>
.contact-container {
  display: flex;
  height: 100vh;
}
</style>
```

## 自定义

### 自定义联系列表搜索功能开关

通过设置 `enableSearch` 参数，您可以灵活地控制 ContactList 中的搜索好友群组功能的显示。
``` typescript
<template>
  <ContactList :enableSearch="false" />
</template>
```
<table>
<tr>
<td rowspan="1" colSpan="1" >enableSearch="true"</td>

<td rowspan="1" colSpan="1" >enableSearch="false"</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/0f52214383ad11f0b321525400e889b2.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/ed273b0683ac11f0818a52540099c741.png)</td>
</tr>
</table>


### 自定义联系列表联系人分组配置

`groupConfig` 用于自定义分组配置，包括标题、显示顺序、隐藏分组等。
``` typescript
<template>
  <ContactList :groupConfig="customGroupConfig" />
</template>

<script setup lang="ts">
import { ContactList } from '@tencentcloud/chat-uikit-vue3';
import { ContactItemType } from '@tencentcloud/chat-uikit-vue3';

const customGroupConfig = {
  [ContactItemType.FRIEND]: {
    title: '我的朋友们',
    order: 1,
  },
  [ContactItemType.GROUP]: {
    title: '群聊列表',
    order: 2,
  },
  [ContactItemType.BLACK]: {
    hidden: true,
  },
  [ContactItemType.FRIEND_REQUEST]: {
    title: '好友请求',
    order: 0,
  }
};
</script>
```
<table>
<tr>
<td rowspan="1" colSpan="1" >修改前</td>

<td rowspan="1" colSpan="1" >修改后</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/0f52214383ad11f0b321525400e889b2.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/c127e97583ad11f0818a52540099c741.png)</td>
</tr>
</table>


### 自定义联系列表子项

您可以通过传入自定义的 `ContactItem` 组件来完全控制联系人列表项的渲染。
``` typescript
<template>
  <div class="custom-contact-item" @click="handleClick">
    <label>自定义联系人</label>
    <span v-if="props.contactItem.type === ContactItemType.FRIEND">{{ props.contactItem.data.nick }}</span>
    <span v-if="props.contactItem.type === ContactItemType.GROUP">{{ props.contactItem.data.name }}</span>
  </div>
</template>
<script setup lang="ts">
import { ContactItemType } from '@tencentcloud/chat-uikit-vue3';

const props = defineProps<{
  contactItem: any;
}>();
const emit = defineEmits<{
  click: [type: ContactItemType, item: any];
}>();
const handleClick = () => {
  emit('click', props.contactItem.type, props.contactItem.data);
};
</script>
<style scoped>
.custom-contact-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px 20px;
  border-bottom: 1px solid #eee;
}
</style>

```
``` typescript
<template>
  <ContactList :ContactItem="CustomContactItem" />
</template>

<script setup lang="ts">
import { ContactList } from '@tencentcloud/chat-uikit-vue3';
import CustomContactItem from './CustomContactItem.vue';
</script>
```
<table>
<tr>
<td rowspan="1" colSpan="1" >修改前</td>

<td rowspan="1" colSpan="1" >修改后</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/fc596af883af11f093f45254005ef0f7.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/e990a2d983af11f0ae9d5254001c06ec.png)</td>
</tr>
</table>


### 自定义联系人详情操作按钮开关

通过设置 `showActions` 参数，您可以控制联系人详情页面中操作按钮的显示。
``` typescript
<template>
  <ContactInfo 
    :showActions="false"
  />
</template>
```
<table>
<tr>
<td rowspan="1" colSpan="1" >修改前</td>

<td rowspan="1" colSpan="1" >修改后</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/26c5a53f83b011f0818a52540099c741.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/4f25ef6b83b011f0b6b0525400bf7822.png)</td>
</tr>
</table>


### 自定义联系人详情空状态

当没有选中任何联系人时，您可以自定义显示的空状态组件。
``` typescript
<template>
  <div>
    自定义空状态
  </div>
</template>
```
``` typescript
<template>
  <ContactInfo 
    :PlaceholderEmpty="CustomEmpty"
  />
</template>

<script setup lang="ts">
import { ContactList } from '@tencentcloud/chat-uikit-vue3';
import CustomEmpty from './CustomEmpty.vue';
</script>
```

### 自定义好友详情组件

您可以为不同类型的联系人自定义详情显示组件。
``` typescript
<template>
  <div class="custom-contact-info">
    <label>自定义好友详情</label>
    <div class="friend-info">
      <img
        class="avatar"
        :src="friend.avatar"
        alt=""
      >
      <span>{{ friend.nick }}</span>
    </div>
  </div>
</template>
<script setup lang="ts">
import type { Friend } from '@tencentcloud/chat-uikit-vue3';

defineProps<{
  friend: Friend;
}>();
</script>
<style scoped>
.custom-contact-info {
  display: flex;
  flex-direction: column;
  gap: 10px;
  padding: 20px;
}
.friend-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
}
.avatar {
  width: 60px;
  height: 60px;
  border-radius: 50%
}
</style>

```
``` typescript
<template>
  <ContactInfo
    :FriendInfoComponent="CustomFriendInfo"
  />
</template>

<script setup lang="ts">
import { defineComponent, h } from 'vue';
import type { FriendInfoProps, GroupInfoProps } from '@tencentcloud/chat-uikit-vue3';
import CustomFriendInfo from './CustomFriendInfo.vue';
</script>
```
<table>
<tr>
<td rowspan="1" colSpan="1" >修改前</td>

<td rowspan="1" colSpan="1" >修改后</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/d853594483b211f0818a52540099c741.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/c084ae7b83b211f0992e52540044a08e.png)</td>
</tr>
</table>

