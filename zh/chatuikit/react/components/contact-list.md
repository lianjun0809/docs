> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/zh/llms.txt
> Use this file to discover all available pages before exploring further.

## 概述

ContactList 是一个高度可配置的联系人列表组件。该组件支持好友列表、群组列表、黑名单和申请管理，提供分组折叠、搜索过滤、自定义渲染等核心功能，适用于即时通讯、社交应用等场景的联系人管理界面。



![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/1301c6bb66dd11f09a9d52540044a08e.png)


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

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >当前激活的联系人项</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableSearch</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >`true`</td>

<td rowspan="1" colSpan="1" >是否启用搜索功能</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >groupConfig</td>

<td rowspan="1" colSpan="1" >Partial<Record<ContactItemType, CustomGroupConfig>></td>

<td rowspan="1" colSpan="1" >`{}`</td>

<td rowspan="1" colSpan="1" >自定义分组配置</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >自定义 CSS 类名</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >React.CSSProperties</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >自定义内联样式</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >searchPlaceholder</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`'Search contacts'`</td>

<td rowspan="1" colSpan="1" >搜索框占位符文本</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >emptyText</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`'No contacts'`</td>

<td rowspan="1" colSpan="1" >空状态提示文本</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ContactItem</td>

<td rowspan="1" colSpan="1" >React.ComponentType<ContactListItemProps> \| undefined</td>

<td rowspan="1" colSpan="1" >`ContactListItem`</td>

<td rowspan="1" colSpan="1" >自定义联系人项组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ContactSearchComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<ContactSearchProps> \| undefined</td>

<td rowspan="1" colSpan="1" >`ContactSearch`</td>

<td rowspan="1" colSpan="1" >自定义搜索组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GroupHeader</td>

<td rowspan="1" colSpan="1" >React.ComponentType<{ data: ContactGroup }> \| undefined</td>

<td rowspan="1" colSpan="1" >默认分组头</td>

<td rowspan="1" colSpan="1" >自定义分组头部组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderEmptyList</td>

<td rowspan="1" colSpan="1" >React.ReactNode \| undefined</td>

<td rowspan="1" colSpan="1" >默认空状态</td>

<td rowspan="1" colSpan="1" >自定义空状态组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onContactItemClick</td>

<td rowspan="1" colSpan="1" >(item: ContactGroupItem) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >联系人项点击事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onFriendApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: FriendApplication) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >好友申请操作事件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onGroupApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: GroupApplication) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >群组申请操作事件</td>
</tr>
</table>


## ContactInfo props
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

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >当前显示的联系人项</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >showActions</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >`true`</td>

<td rowspan="1" colSpan="1" >是否显示操作按钮</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderEmpty</td>

<td rowspan="1" colSpan="1" >React.ReactNode \| undefined</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >空状态占位组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >FriendInfoComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<FriendInfoProps></td>

<td rowspan="1" colSpan="1" >`FriendInfo`</td>

<td rowspan="1" colSpan="1" >好友信息组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GroupInfoComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<GroupInfoProps></td>

<td rowspan="1" colSpan="1" >`GroupInfo`</td>

<td rowspan="1" colSpan="1" >群组信息组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >BlacklistInfoComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<BlacklistInfoProps></td>

<td rowspan="1" colSpan="1" >`BlacklistInfo`</td>

<td rowspan="1" colSpan="1" >黑名单信息组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >FriendApplicationInfoComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<FriendApplicationInfoProps></td>

<td rowspan="1" colSpan="1" >`FriendApplicationInfo`</td>

<td rowspan="1" colSpan="1" >好友申请信息组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GroupApplicationInfoComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<GroupApplicationInfoProps></td>

<td rowspan="1" colSpan="1" >`GroupApplicationInfo`</td>

<td rowspan="1" colSpan="1" >群组申请信息组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchGroupInfoComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<SearchGroupInfoProps></td>

<td rowspan="1" colSpan="1" >`SearchGroupInfo`</td>

<td rowspan="1" colSpan="1" >搜索群组信息组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchUserInfoComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<SearchUserInfoProps></td>

<td rowspan="1" colSpan="1" >`SearchUserInfo`</td>

<td rowspan="1" colSpan="1" >搜索用户信息组件</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClose</td>

<td rowspan="1" colSpan="1" >() => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >关闭信息面板回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onSendMessage</td>

<td rowspan="1" colSpan="1" >(friend: Friend) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >发送消息回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onDeleteFriend</td>

<td rowspan="1" colSpan="1" >(friend: Friend) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >删除好友回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onUpdateFriendRemark</td>

<td rowspan="1" colSpan="1" >(friend: Friend, remark: string) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >更新好友备注回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onAddToBlacklist</td>

<td rowspan="1" colSpan="1" >(friend: Friend) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >添加到黑名单回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onRemoveFromBlacklist</td>

<td rowspan="1" colSpan="1" >(profile: UserProfile) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >从黑名单移除回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onEnterGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >进入群组回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onLeaveGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >退出群组回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onDismissGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >解散群组回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onFriendApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: FriendApplication) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >好友申请操作回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onGroupApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: GroupApplication) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >群组申请操作回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onAddFriend</td>

<td rowspan="1" colSpan="1" >(user: UserProfile, wording: string) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >添加好友回调</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onJoinGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel, note: string) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >加入群组回调</td>
</tr>
</table>


## 基础使用
``` tsx
import { ContactList, ContactInfo } from '@tencentcloud/chat-uikit-react';

function App() {
  return (
    <div>
      <ContactList />
      <ContactInfo />
    </div>
  );
}
```

## 自定义能力

### 自定义联系列表搜索功能开关

通过设置 `enableSearch` 参数，您可以灵活地控制 ContactList 中的搜索好友群组功能的显示。
``` typescript
<ContactList enableSearch={false} />
```

效果如下图所示：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/2147e4f366de11f09b85525400bf7822.png)

### 自定义联系列表联系人分组配置

`groupConfig` 用于自定义分组配置，包括标题、显示顺序、隐藏状态等，默认值为 `{}`。



【自定义分组标题】
``` typescript
import React from 'react';
import { ContactList } from '@tencentcloud/chat-uikit-react';
import { ContactItemType } from '@tencentcloud/chat-uikit-react';

function CustomGroupTitlesContactList() {
  const groupConfig = {
    [ContactItemType.FRIEND]: {
      title: '我的好友',
      order: 1
    },
    [ContactItemType.GROUP]: {
      title: '我的群组',
      order: 2
    },
    [ContactItemType.FRIEND_REQUEST]: {
      title: '好友申请',
      order: 0
    }
  };

  return (
    <ContactList
      groupConfig={groupConfig}
      onContactItemClick={(item) => {
        console.log('联系人点击:', item);
      }}
    />
  );
}
```

效果如下图所示：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/1c780045676711f09b85525400bf7822.png)

【隐藏特定分组】
``` tsx
import React from 'react';
import { ContactList } from '@tencentcloud/chat-uikit-react';
import { ContactItemType } from '@tencentcloud/chat-uikit-react';

function HiddenGroupsContactList() {
  const groupConfig = {
    [ContactItemType.BLACK]: {
      title: '黑名单',
      hidden: true // 隐藏黑名单分组
    },
    [ContactItemType.GROUP_REQUEST]: {
      title: '群组申请',
      hidden: true // 隐藏群组申请分组
    }
  };

  return (
    <ContactList
      groupConfig={groupConfig}
      onContactItemClick={(item) => {
        console.log('联系人点击:', item);
      }}
    />
  );
}
```

效果如下图所示：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/0b5061fa676711f0bd33525400e889b2.png)

### 自定义联系列表子项

ContactItem 用于自定义联系人项的渲染组件，默认值为内置的 `ContactListItem` 组件。
``` typescript
import React from 'react';
import { ContactList, Avatar } from '@tencentcloud/chat-uikit-react';
import type { ContactListItemProps } from '@tencentcloud/chat-uikit-react';

const SimpleContactItem: React.FC<ContactListItemProps> = ({ 
  contactItem, 
  onClick, 
  activeContactItem 
}) => {
  const isActive = activeContactItem?.data.userID === contactItem.data.userID;

  return (
    <div
      className={`simple-contact-item ${isActive ? 'active' : ''}`}
      onClick={() => onClick?.(contactItem.type, contactItem.data)}
      style={{
        padding: '8px 12px',
        borderBottom: '1px solid #f0f0f0',
        cursor: 'pointer',
        backgroundColor: isActive ? '#e6f7ff' : 'transparent'
      }}
    >
      <div style={{ display: 'flex', alignItems: 'center', gap: '10px' }}>
        <Avatar src={contactItem.data.avatar}  alt="avatar" />
        <span>{contactItem.data.nick || contactItem.data.name}</span>
      </div>
    </div>
  );
};

function ContactListWithSimpleItems() {
  return (
    <ContactList
      ContactItem={SimpleContactItem}
      onContactItemClick={(item) => {
        console.log('联系人点击:', item);
      }}
    />
  );
}
```

效果如下图所示：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/849d4e5e66e111f0bd33525400e889b2.png)

### 自定义联系人详情操作按钮开关

`showActions` 用于控制是否显示操作按钮，默认值为 `true`。
``` typescript
import React from 'react';
import { ContactInfo } from '@tencentcloud/chat-uikit-react';

function ReadOnlyContactInfo() {
  const friendData = {
    type: ContactItemType.FRIEND,
    data: {
      userID: 'user123',
      nick: '张三',
      avatar: 'https://example.com/avatar.jpg',
      remark: '同事',
      // ... 其他好友属性
    },
  };

  return (
    <ContactInfo 
      contactItem={friendData}
      showActions={false} // 隐藏所有操作按钮，只显示信息
    />
  );
}
```

效果如下图所示：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/0a5c7141676911f0b5365254001c06ec.png)


### 自定义联系人详情空状态

`PlaceholderEmpty` 用于自定义空状态显示内容，默认值为 `undefined`。
``` typescript
import React from 'react';
import { ContactInfo } from '@tencentcloud/chat-uikit-react';

function CustomEmptyState() {
  const EmptyPlaceholder = () => (
    <div style={{ 
      width: '100%',
      textAlign: 'center', 
      padding: '40px 20px',
      color: '#999',
      fontSize: '14px',
      background: '#fff',
    }}>
      <div style={{ fontSize: '48px', marginBottom: '16px' }}>👤</div>
      <div>请选择一个联系人查看详细信息</div>
      <div style={{ marginTop: '8px', fontSize: '12px' }}>
        点击左侧联系人列表中的任意项目
      </div>
    </div>
  );

  return (
    <ContactInfo 
      contactItem={undefined}
      PlaceholderEmpty={<EmptyPlaceholder />}
    />
  );
}
```

效果如下图所示：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/4a270500676911f0924f5254005ef0f7.png)


### 自定义联系人详情组件

> **说明：**
> 
> - `FriendInfoComponent` 用于自定义好友信息组件，默认值为内置的 `FriendInfo` 组件。
> - `GroupInfoComponent` 用于自定义群组信息组件，默认值为内置的 `GroupInfo` 组件。
> - `BlacklistInfoComponent` 用于自定义黑名单信息组件，默认值为内置的 `BlacklistInfo` 组件。
> - `FriendApplicationInfoComponent` 用于自定义好友申请信息组件，默认值为内置的 `FriendApplicationInfo` 组件。
> - `GroupApplicationInfoComponent` 用于自定义群组申请信息组件，默认值为内置的 `GroupApplicationInfo` 组件。




【自定义好友信息组件】
``` typescript
import React from 'react';
import { ContactInfo } from '@tencentcloud/chat-uikit-react';
import type { FriendInfoProps, Friend } from '@tencentcloud/chat-uikit-react';
import { Button } from '@tencentcloud/uikit-base-component-react';

// 自定义好友信息组件
const CustomFriendInfo: React.FC<FriendInfoProps> = ({ 
  friend, 
  showActions, 
  onClose, 
  onSendMessage,
  onDeleteFriend 
}) => {
  return (
    <div style={{ padding: '20px', border: '1px solid #e0e0e0', borderRadius: '8px' }}>
      <div style={{ display: 'flex', alignItems: 'center', marginBottom: '16px' }}>
        <img 
          src={friend.avatar} 
          alt="avatar" 
          style={{ width: '60px', height: '60px', borderRadius: '50%', marginRight: '16px' }}
        />
        <div>
          <h3 style={{ margin: '0 0 4px 0' }}>{friend.nick}</h3>
          <p style={{ margin: '0', color: '#666' }}>备注: {friend.remark}</p>
        </div>
      </div>
      
      <div style={{ display: 'flex', flexDirection: 'column', gap: '10px',  marginBottom: '16px' }}>
        <p><strong>用户ID:</strong> {friend.userID}</p>
        <p><strong>个性签名:</strong> {friend.selfSignature}</p>
        <p><strong>位置:</strong> {friend.location}</p>
      </div>


      {showActions && (
        <div style={{ display: 'flex', gap: '8px' }}>
          <Button onClick={() => onSendMessage?.(friend)}>发送消息</Button>
          <Button onClick={() => onDeleteFriend?.(friend)}>删除好友</Button>
          <Button onClick={onClose}>关闭</Button>
        </div>
      )}
    </div>
  );
};

function CustomFriendInfoDemo() {
  const friendData = {
    type: ContactItemType.FRIEND,
    data: {
      userID: 'user123',
      nick: '张三',
      avatar: 'https://example.com/avatar.jpg',
      remark: '同事',
      selfSignature: '热爱技术，热爱生活',
      location: '北京',
      // ... 其他属性
    },
  };

  return (
    <ContactInfo 
      contactItem={friendData}
      FriendInfoComponent={CustomFriendInfo}
      onSendMessage={(friend) => console.log('发送消息给:', friend.nick)}
      onDeleteFriend={(friend) => console.log('删除好友:', friend.nick)}
    />
  );
}
```

效果如下图所示：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/56337044676a11f0b5365254001c06ec.png)

【自定义群组信息组件】
``` typescript
import React from 'react';
import { ContactInfo, GroupMemberRole } from '@tencentcloud/uikit-component-react';
import type { GroupInfoProps, GroupModel } from '@tencentcloud/uikit-component-react';
import { Button } from '@tencentcloud/uikit-base-component-react';

// 自定义群组信息组件
const CustomGroupInfo: React.FC<GroupInfoProps> = ({ 
  group, 
  showActions, 
  onClose, 
  onEnterGroup,
  onLeaveGroup,
  onDismissGroup 
}) => {
  const isOwner = group.selfInfo?.role === GroupMemberRole.OWNER; // 群主
  const isAdmin = group.selfInfo?.role === GroupMemberRole.ADMIN; // 管理员

  return (
    <div style={{ padding: '20px', border: '1px solid #e0e0e0', borderRadius: '8px' }}>
      <div style={{ display: 'flex', alignItems: 'center', marginBottom: '16px' }}>
        <img 
          src={group.avatar} 
          alt="group avatar" 
          style={{ width: '60px', height: '60px', borderRadius: '8px', marginRight: '16px' }}
        />
        <div>
          <h3 style={{ margin: '0 0 4px 0' }}>{group.name}</h3>
          <p style={{ margin: '0', color: '#666' }}>
            群组ID: {group.groupID}
          </p>
        </div>
      </div>
      
      <div style={{ display: 'flex', flexDirection: 'column', gap: '10px',  marginBottom: '16px' }}>
        <p><strong>群组介绍:</strong> {group.introduction}</p>
        <p><strong>群组公告:</strong> {group.notification}</p>
        <p><strong>成员数量:</strong> {group.memberCount}/{group.maxMemberCount}</p>
        <p><strong>我的角色:</strong> {
          isOwner ? '群主' : isAdmin ? '管理员' : '普通成员'
        }</p>
      </div>

      {showActions && (
        <div style={{ display: 'flex', gap: '8px' }}>
          <Button onClick={() => onEnterGroup?.(group)}>进入群组</Button>
          <Button onClick={() => onLeaveGroup?.(group)}>退出群组</Button>
          {isOwner && (
            <Button onClick={() => onDismissGroup?.(group)}>解散群组</Button>
          )}
          <Button onClick={onClose}>关闭</Button>
        </div>
      )}
    </div>
  );
};

function CustomGroupInfoDemo() {
  const groupData = {
    type: ContactItemType.GROUP,
    data: {
      groupID: 'group123',
      name: '技术交流群',
      avatar: 'https://example.com/group-avatar.jpg',
      type: 'Public',
      introduction: '技术交流与分享',
      notification: '欢迎加入技术交流群',
      ownerID: 'owner123',
      memberCount: 100,
      maxMemberCount: 200,
      selfInfo: {
        userID: 'currentUser',
        role: GroupMemberRole.OWNER, // 群主
        nameCard: '群主',
        joinTime: Date.now(),
      },
    },
  };

  return (
    <ContactInfo 
      contactItem={groupData}
      GroupInfoComponent={CustomGroupInfo}
      onEnterGroup={(group) => console.log('进入群组:', group.name)}
      onLeaveGroup={(group) => console.log('退出群组:', group.name)}
      onDismissGroup={(group) => console.log('解散群组:', group.name)}
    />
  );
}
```

效果如下图所示：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/c93c8710676b11f0bd33525400e889b2.png)

【自定义黑名单信息组件】
``` typescript
import React from 'react';
import { ContactInfo } from '@tencentcloud/uikit-component-react';
import type { BlacklistInfoProps, UserProfile } from '@tencentcloud/uikit-component-react';
import { Button } from '@tencentcloud/uikit-base-component-react';

// 自定义黑名单信息组件
const CustomBlacklistInfo: React.FC<BlacklistInfoProps> = ({ 
  profile, 
  showActions, 
  onClose, 
  onRemoveFromBlacklist 
}) => {
  return (
    <div style={{ padding: '20px', border: '1px solid #e0e0e0', borderRadius: '8px' }}>
      <div style={{ display: 'flex', alignItems: 'center', marginBottom: '16px' }}>
        <img 
          src={profile.src} 
          alt="avatar" 
          style={{ width: '60px', height: '60px', borderRadius: '50%', marginRight: '16px' }}
        />
        <div>
          <h3 style={{ margin: '0 0 4px 0', color: '#ff4d4f' }}>{profile.nick}</h3>
          <p style={{ margin: '0', color: '#666' }}>用户ID: {profile.userID}</p>
        </div>
      </div>
      
      <div style={{ display: 'flex', flexDirection: 'column', gap: '10px',  marginBottom: '16px' }}>
        <p><strong>个性签名:</strong> {profile.selfSignature}</p>
        <p><strong>位置:</strong> {profile.location}</p>
        <p style={{ color: '#ff4d4f', fontWeight: 'bold' }}>
          ⚠️ 此用户已被加入黑名单
        </p>
      </div>

      {showActions && (
        <div style={{ display: 'flex', gap: '8px' }}>
          <Button 
            onClick={() => onRemoveFromBlacklist?.(profile)}
            style={{ backgroundColor: '#52c41a', color: 'white', border: 'none' }}
          >
            移出黑名单
          </Button>
          <Button onClick={onClose}>关闭</Button>
        </div>
      )}
    </div>
  );
};

function CustomBlacklistInfoDemo() {
  const blacklistData = {
    type: ContactItemType.BLACK,
    data: {
      userID: 'user456',
      nick: '李四',
      src: 'https://example.com/avatar2.jpg',
      gender: 1,
      birthday: 19920101,
      location: '深圳',
      selfSignature: '被拉黑用户',
      allowType: 1,
      adminForbidType: 0,
    },
  };

  return (
    <ContactInfo 
      contactItem={blacklistData}
      BlacklistInfoComponent={CustomBlacklistInfo}
      onRemoveFromBlacklist={(profile) => console.log('移出黑名单:', profile.nick)}
    />
  );
}
```

效果如下图所示：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/e8aea7e0676c11f09b85525400bf7822.png)

【自定义好友申请信息组件】
``` typescript
import React from 'react';
import { ContactInfo } from '@tencentcloud/uikit-component-react';
import type { FriendApplicationInfoProps, FriendApplication } from '@tencentcloud/uikit-component-react';
import { Button } from '@tencentcloud/uikit-base-component-react';

// 自定义好友申请信息组件
const CustomFriendApplicationInfo: React.FC<FriendApplicationInfoProps> = ({ 
  application, 
  showActions, 
  onClose, 
  onAccept,
  onRefuse 
}) => {
  const formatTime = (timestamp: number) => {
    return new Date(timestamp).toLocaleString();
  };

  return (
    <div style={{ padding: '20px', border: '1px solid #e0e0e0', borderRadius: '8px' }}>
      <div style={{ display: 'flex', alignItems: 'center', marginBottom: '16px' }}>
        <img 
          src={application.src} 
          alt="avatar" 
          style={{ width: '60px', height: '60px', borderRadius: '50%', marginRight: '16px' }}
        />
        <div>
          <h3 style={{ margin: '0 0 4px 0' }}>{application.nick}</h3>
          <p style={{ margin: '0', color: '#666' }}>申请时间: {formatTime(application.time)}</p>
        </div>
      </div>
      
      <div style={{ display: 'flex', flexDirection: 'column', gap: '10px',  marginBottom: '16px' }}>
        <p><strong>申请来源:</strong> {application.source}</p>
        <p><strong>申请附言:</strong> {application.wording}</p>
        <p style={{ color: '#1890ff', fontWeight: 'bold' }}>
          📝 新的好友申请
        </p>
      </div>

      {showActions && (
        <div style={{ display: 'flex', gap: '8px' }}>
          <Button 
            onClick={() => onAccept?.(application)}
            style={{ backgroundColor: '#52c41a', color: 'white', border: 'none' }}
          >
            接受申请
          </Button>
          <Button 
            onClick={() => onRefuse?.(application)}
            style={{ backgroundColor: '#ff4d4f', color: 'white', border: 'none' }}
          >
            拒绝申请
          </Button>
          <Button onClick={onClose}>关闭</Button>
        </div>
      )}
    </div>
  );
};

function CustomFriendApplicationInfoDemo() {
  const applicationData = {
    type: ContactItemType.FRIEND_REQUEST,
    data: {
      userID: 'user789',
      nick: '王五',
      src: 'https://example.com/avatar3.jpg',
      time: Date.now(),
      source: '搜索添加',
      wording: '你好，我想加你为好友，一起交流技术',
      type: 1,
    },
  };

  return (
    <ContactInfo 
      contactItem={applicationData}
      FriendApplicationInfoComponent={CustomFriendApplicationInfo}
      onFriendApplicationAction={(action, application) => {
        if (action === 'accept') {
          console.log('接受好友申请:', application.nick);
        } else {
          console.log('拒绝好友申请:', application.nick);
        }
      }}
    />
  );
}
```

效果如下图所示：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/42ea5e27676e11f0924f5254005ef0f7.png)

【自定义群组申请信息组件】
``` typescript
import React from 'react';
import { ContactInfo } from '@tencentcloud/uikit-component-react';
import type { GroupApplicationInfoProps, GroupApplication } from '@tencentcloud/uikit-component-react';
import { Button } from '@tencentcloud/uikit-base-component-react';

// 自定义群组申请信息组件
const CustomGroupApplicationInfo: React.FC<GroupApplicationInfoProps> = ({ 
  application, 
  showActions, 
  onClose, 
  onAccept,
  onRefuse 
}) => {
  const getApplicationTypeText = (type: number) => {
    return type === 0 ? '用户申请加入' : '邀请用户加入';
  };

  return (
    <div style={{ padding: '20px', border: '1px solid #e0e0e0', borderRadius: '8px' }}>
      <div style={{ display: 'flex', alignItems: 'center', marginBottom: '16px' }}>
        <div style={{ width: '60px', height: '60px', borderRadius: '8px', marginRight: '16px', backgroundColor: '#f0f0f0', display: 'flex', alignItems: 'center', justifyContent: 'center' }}>
          👥
        </div>
        <div>
          <h3 style={{ margin: '0 0 4px 0' }}>{application.groupName}</h3>
          <p style={{ margin: '0', color: '#666' }}>
            {getApplicationTypeText(application.applicationType)}
          </p>
        </div>
      </div>
      
       <div style={{ display: 'flex', flexDirection: 'column', gap: '10px',  marginBottom: '16px' }}>
        <p><strong>申请人:</strong> {application.applicantNick}</p>
        <p><strong>群组ID:</strong> {application.groupID}</p>
        <p><strong>申请备注:</strong> {application.note}</p>
        <p style={{ color: '#1890ff', fontWeight: 'bold' }}>
          📋 群组申请待处理
        </p>
      </div>

      {showActions && (
        <div style={{ display: 'flex', gap: '8px' }}>
          <Button 
            onClick={() => onAccept?.(application)}
            style={{ backgroundColor: '#52c41a', color: 'white', border: 'none' }}
          >
            同意申请
          </Button>
          <Button 
            onClick={() => onRefuse?.(application)}
            style={{ backgroundColor: '#ff4d4f', color: 'white', border: 'none' }}
          >
            拒绝申请
          </Button>
          <Button onClick={onClose}>关闭</Button>
        </div>
      )}
    </div>
  );
};

function CustomGroupApplicationInfoDemo() {
  const applicationData = {
    type: ContactItemType.GROUP_REQUEST,
    data: {
      applicant: 'user999',
      applicantNick: '赵六',
      groupID: 'group456',
      groupName: '产品经理交流群',
      applicationType: 0,
      userID: 'user999',
      note: '我想加入产品经理交流群，学习产品设计经验',
    },
  };

  return (
    <ContactInfo 
      contactItem={applicationData}
      GroupApplicationInfoComponent={CustomGroupApplicationInfo}
      onGroupApplicationAction={(action, application) => {
        if (action === 'accept') {
          console.log('同意群组申请:', application.groupName);
        } else {
          console.log('拒绝群组申请:', application.groupName);
        }
      }}
    />
  );
}
```

效果如下图所示：

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/44424b79676f11f09a9d52540044a08e.png)

## useContactListState

ContactListState 是基于 Zustand 的关系链管理钩子，为 ContactLis 组件提供完整的数据管理能力。它支持好友列表、群组列表、黑名单和申请管理等功能关了。如果自定义组件能力不能支持您的业务，可以使用 ContactListState 实现您的需求。

### 数据
<table>
<tr>
<td rowspan="1" colSpan="1" >属性名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >friendList</td>

<td rowspan="1" colSpan="1" >Friend[]</td>

<td rowspan="1" colSpan="1" >好友列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >groupList</td>

<td rowspan="1" colSpan="1" >Group[]</td>

<td rowspan="1" colSpan="1" >群组列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >blackList</td>

<td rowspan="1" colSpan="1" >UserProfile[]</td>

<td rowspan="1" colSpan="1" >黑名单列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >friendApplicationUnreadCount</td>

<td rowspan="1" colSpan="1" >number</td>

<td rowspan="1" colSpan="1" >未读好友申请数量</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >friendGroupList</td>

<td rowspan="1" colSpan="1" >FriendGroup[]</td>

<td rowspan="1" colSpan="1" >好友分组列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >friendApplicationList</td>

<td rowspan="1" colSpan="1" >FriendApplication[]</td>

<td rowspan="1" colSpan="1" >好友申请列表</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >groupApplicationList</td>

<td rowspan="1" colSpan="1" >GroupApplication[]</td>

<td rowspan="1" colSpan="1" >群组申请列表</td>
</tr>
</table>


### 操作方法
<table>
<tr>
<td rowspan="1" colSpan="1" >属性名</td>

<td rowspan="1" colSpan="1" >类型</td>

<td rowspan="1" colSpan="1" >说明</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >addFriend</td>

<td rowspan="1" colSpan="1" >(options: AddFriendParams) => Promise</td>

<td rowspan="1" colSpan="1" >添加好友</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >deleteFriend</td>

<td rowspan="1" colSpan="1" >(options: DeleteFriendParams) => Promise</td>

<td rowspan="1" colSpan="1" >删除好友</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >setFriendRemark</td>

<td rowspan="1" colSpan="1" >(options: FriendRemarkParams) => Promise</td>

<td rowspan="1" colSpan="1" >设置好友备注</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >markFriendApplicationAsRead</td>

<td rowspan="1" colSpan="1" >() => Promise</td>

<td rowspan="1" colSpan="1" >标记好友申请为已读</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >acceptFriendApplication</td>

<td rowspan="1" colSpan="1" >(options: FriendApplicationParams) => Promise</td>

<td rowspan="1" colSpan="1" >接受好友申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >refuseFriendApplication</td>

<td rowspan="1" colSpan="1" >(userID: string) => Promise</td>

<td rowspan="1" colSpan="1" >拒绝好友申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >addToBlacklist</td>

<td rowspan="1" colSpan="1" >(userIDList: string[]) => Promise</td>

<td rowspan="1" colSpan="1" >添加到黑名单</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >removeFromBlacklist</td>

<td rowspan="1" colSpan="1" >(userIDList: string[]) => Promise</td>

<td rowspan="1" colSpan="1" >从黑名单移除</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >createFriendGroup</td>

<td rowspan="1" colSpan="1" >(options: FriendGroupParams) => Promise</td>

<td rowspan="1" colSpan="1" >创建好友分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >deleteFriendGroup</td>

<td rowspan="1" colSpan="1" >(name: string) => Promise</td>

<td rowspan="1" colSpan="1" >删除好友分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >addToFriendGroup</td>

<td rowspan="1" colSpan="1" >(options: FriendGroupParams) => Promise</td>

<td rowspan="1" colSpan="1" >添加好友到分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >removeFromFriendGroup</td>

<td rowspan="1" colSpan="1" >(options: FriendGroupParams) => Promise</td>

<td rowspan="1" colSpan="1" >从分组移除好友</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >renameFriendGroup</td>

<td rowspan="1" colSpan="1" >(options: RenameFriendGroupParams) => Promise</td>

<td rowspan="1" colSpan="1" >重命名好友分组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >joinGroup</td>

<td rowspan="1" colSpan="1" >(options: JoinGroupParams) => Promise</td>

<td rowspan="1" colSpan="1" >申请加入群组</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >acceptGroupApplication</td>

<td rowspan="1" colSpan="1" >(options: GroupApplicationParams) => Promise</td>

<td rowspan="1" colSpan="1" >接受群组申请</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >refuseGroupApplication</td>

<td rowspan="1" colSpan="1" >(options: GroupApplicationParams) => Promise</td>

<td rowspan="1" colSpan="1" >拒绝群组申请</td>
</tr>
</table>


## 使用示例
``` typescript
import { useContactListState } from '@tencentcloud/chat-uikit-react';
const {
    friendList,
    groupList,
    blackList,
    friendApplicationUnreadCount,
    friendGroupList,
    friendApplicationList,
    groupApplicationList,
    addFriend,
    deleteFriend,
    setFriendRemark,
    markFriendApplicationAsRead,
    acceptFriendApplication,
    refuseFriendApplication,
    addToBlacklist,
    removeFromBlacklist,
    createFriendGroup,
    deleteFriendGroup,
    addToFriendGroup,
    removeFromFriendGroup,
    joinGroup,
    acceptGroupApplication,
    refuseGroupApplication,
  } = useContactListState();
```
