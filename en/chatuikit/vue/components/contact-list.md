> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/en/llms.txt
> Use this file to discover all available pages before exploring further.

## Overview

ContactList is a highly configurable contact list component. This component supports friend lists, group lists, blacklists, and application management, providing core features such as group collapsing, search filtering, and custom rendering. It's suitable for contact management interfaces in instant messaging and social applications.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/e81dc6d883b511f0b6b0525400bf7822.png)


## ContactList Props
<table>
<tr>
<td rowspan="1" colSpan="1" >Field</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >activeContactItem</td>

<td rowspan="1" colSpan="1" >ContactGroupItem \| undefined</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >Currently active contact item</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableSearch</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Whether to enable search functionality</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >groupConfig</td>

<td rowspan="1" colSpan="1" >Partial<Record<ContactItemType, CustomGroupConfig>></td>

<td rowspan="1" colSpan="1" >{}</td>

<td rowspan="1" colSpan="1" >Custom group configuration</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >searchPlaceholder</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >'Search contacts'</td>

<td rowspan="1" colSpan="1" >Search box placeholder text</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >emptyText</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >'No contacts'</td>

<td rowspan="1" colSpan="1" >Empty state message text</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ContactItem</td>

<td rowspan="1" colSpan="1" >Component \| undefined</td>

<td rowspan="1" colSpan="1" >ContactListItem</td>

<td rowspan="1" colSpan="1" >Custom contact item component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ContactSearchComponent</td>

<td rowspan="1" colSpan="1" >Component \| undefined</td>

<td rowspan="1" colSpan="1" >ContactSearch</td>

<td rowspan="1" colSpan="1" >Custom search component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GroupHeader</td>

<td rowspan="1" colSpan="1" >Component \| undefined</td>

<td rowspan="1" colSpan="1" >Default group header</td>

<td rowspan="1" colSpan="1" >Custom group header component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderEmptyList</td>

<td rowspan="1" colSpan="1" >Component \| undefined</td>

<td rowspan="1" colSpan="1" >Default empty state</td>

<td rowspan="1" colSpan="1" >Custom empty state component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onContactItemClick</td>

<td rowspan="1" colSpan="1" >(item: ContactGroupItem) => void</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >Contact item click event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onFriendApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: FriendApplication) => void</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >Friend application action event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onGroupApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: GroupApplication) => void</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >Group application action event</td>
</tr>
</table>


## ContactList Events
<table>
<tr>
<td rowspan="1" colSpan="1" >Event Name</td>

<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >contact-item-click</td>

<td rowspan="1" colSpan="1" >(item: ContactGroupItem)</td>

<td rowspan="1" colSpan="1" >Contact item click event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >friend-application-action</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: FriendApplication)</td>

<td rowspan="1" colSpan="1" >Friend application action event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >group-application-action</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: GroupApplication)</td>

<td rowspan="1" colSpan="1" >Group application action event</td>
</tr>
</table>


## ContactInfo Props
<table>
<tr>
<td rowspan="1" colSpan="1" >Field</td>

<td rowspan="1" colSpan="1" >Type</td>

<td rowspan="1" colSpan="1" >Default Value</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >contactItem</td>

<td rowspan="1" colSpan="1" >ContactGroupItem \| undefined</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >Currently displayed contact item</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >showActions</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >true</td>

<td rowspan="1" colSpan="1" >Whether to show action buttons</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderEmpty</td>

<td rowspan="1" colSpan="1" >Component \| undefined</td>

<td rowspan="1" colSpan="1" >undefined</td>

<td rowspan="1" colSpan="1" >Empty state placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >FriendInfoComponent</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >FriendInfo</td>

<td rowspan="1" colSpan="1" >Friend info component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GroupInfoComponent</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >GroupInfo</td>

<td rowspan="1" colSpan="1" >Group info component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >BlacklistInfoComponent</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >BlacklistInfo</td>

<td rowspan="1" colSpan="1" >Blacklist info component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >FriendApplicationInfoComponent</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >FriendApplicationInfo</td>

<td rowspan="1" colSpan="1" >Friend application info component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GroupApplicationInfoComponent</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >GroupApplicationInfo</td>

<td rowspan="1" colSpan="1" >Group application info component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchGroupInfoComponent</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >SearchGroupInfo</td>

<td rowspan="1" colSpan="1" >Search group info component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchUserInfoComponent</td>

<td rowspan="1" colSpan="1" >Component</td>

<td rowspan="1" colSpan="1" >SearchUserInfo</td>

<td rowspan="1" colSpan="1" >Search user info component</td>
</tr>
</table>


## ContactInfo Events
<table>
<tr>
<td rowspan="1" colSpan="1" >Event Name</td>

<td rowspan="1" colSpan="1" >Parameters</td>

<td rowspan="1" colSpan="1" >Description</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >close</td>

<td rowspan="1" colSpan="1" >-</td>

<td rowspan="1" colSpan="1" >Close info panel event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sendMessage</td>

<td rowspan="1" colSpan="1" >(friend: Friend)</td>

<td rowspan="1" colSpan="1" >Send message event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >deleteFriend</td>

<td rowspan="1" colSpan="1" >(friend: Friend)</td>

<td rowspan="1" colSpan="1" >Delete friend event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >addToBlacklist</td>

<td rowspan="1" colSpan="1" >(friend: Friend)</td>

<td rowspan="1" colSpan="1" >Add to blacklist event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >removeFromBlacklist</td>

<td rowspan="1" colSpan="1" >(profile: UserProfile)</td>

<td rowspan="1" colSpan="1" >Remove from blacklist event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >updateFriendRemark</td>

<td rowspan="1" colSpan="1" >(friend: Friend)</td>

<td rowspan="1" colSpan="1" >Update friend remark event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enterGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel)</td>

<td rowspan="1" colSpan="1" >Enter group event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >leaveGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel)</td>

<td rowspan="1" colSpan="1" >Leave group event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >dismissGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel)</td>

<td rowspan="1" colSpan="1" >Dismiss group event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >friendApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: FriendApplication)</td>

<td rowspan="1" colSpan="1" >Friend application action event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >groupApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: GroupApplication)</td>

<td rowspan="1" colSpan="1" >Group application action event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >addFriend</td>

<td rowspan="1" colSpan="1" >(user: UserProfile, wording: string)</td>

<td rowspan="1" colSpan="1" >Add friend event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >joinGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel, note: string)</td>

<td rowspan="1" colSpan="1" >Join group event</td>
</tr>
</table>


## Basic Usage
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

## Customization

### Customize Contact List Search Toggle

By setting the `enableSearch` parameter, you can flexibly control the display of the friend/group search functionality in ContactList.
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


### Customize Contact List Group Configuration

`groupConfig` is used to customize group configuration, including title, display order, hiding groups, etc.
``` typescript
<template>
  <ContactList :groupConfig="customGroupConfig" />
</template>

<script setup lang="ts">
import { ContactList } from '@tencentcloud/chat-uikit-vue3';
import { ContactItemType } from '@tencentcloud/chat-uikit-vue3';

const customGroupConfig = {
  [ContactItemType.FRIEND]: {
    title: 'My Friends',
    order: 1,
  },
  [ContactItemType.GROUP]: {
    title: 'Group Chats',
    order: 2,
  },
  [ContactItemType.BLACK]: {
    hidden: true,
  },
  [ContactItemType.FRIEND_REQUEST]: {
    title: 'Friend Requests',
    order: 0,
  }
};
</script>
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Before</td>

<td rowspan="1" colSpan="1" >After</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/0f52214383ad11f0b321525400e889b2.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/c127e97583ad11f0818a52540099c741.png)</td>
</tr>
</table>


### Customize Contact List Items

You can fully control the rendering of contact list items by passing in a custom `ContactItem` component.
``` typescript
<template>
  <div class="custom-contact-item" @click="handleClick">
    <label>Custom Contact</label>
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
<td rowspan="1" colSpan="1" >Before</td>

<td rowspan="1" colSpan="1" >After</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/fc596af883af11f093f45254005ef0f7.png)</td>

<td rowspan="1" colSpan="1" >![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/e990a2d983af11f0ae9d5254001c06ec.png)</td>
</tr>
</table>


### Customize Contact Details Action Button Toggle

By setting the `showActions` parameter, you can control the display of action buttons on the contact details page.
``` typescript
<template>
  <ContactInfo 
    :showActions="false"
  />
</template>
```
<table>
<tr>
<td rowspan="1" colSpan="1" >Before</td>

<td rowspan="1" colSpan="1" >After</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/26c5a53f83b011f0818a52540099c741.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/4f25ef6b83b011f0b6b0525400bf7822.png)</td>
</tr>
</table>


### Customize Contact Details Empty State

When no contact is selected, you can customize the empty state component to display.
``` typescript
<template>
  <div>
    Custom Empty State
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

### Customize Friend Details Component

You can customize the detail display component for different types of contacts.
``` typescript
<template>
  <div class="custom-contact-info">
    <label>Custom Friend Details</label>
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
<td rowspan="1" colSpan="1" >Before</td>

<td rowspan="1" colSpan="1" >After</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/d853594483b211f0818a52540099c741.png)</td>

<td rowspan="1" colSpan="1" ><br>![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/c084ae7b83b211f0992e52540044a08e.png)</td>
</tr>
</table>

