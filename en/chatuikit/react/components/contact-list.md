> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/en/llms.txt
> Use this file to discover all available pages before exploring further.

## Overview

ContactList is a highly configurable contact list component. It supports friend list, group list, blocklist, and application management, offering core features such as group collapsing, search filtering, and custom rendering. It is suitable for contact management interfaces in instant messaging and social applications.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/41360ab1679511f0837f525400454e06.png)


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

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Currently active contact item</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >enableSearch</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >`true`</td>

<td rowspan="1" colSpan="1" >Whether to enable the search feature</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >groupConfig</td>

<td rowspan="1" colSpan="1" >Partial<Record<ContactItemType, CustomGroupConfig>></td>

<td rowspan="1" colSpan="1" >`{}`</td>

<td rowspan="1" colSpan="1" >Custom group configuration</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >className</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Custom CSS class name</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >style</td>

<td rowspan="1" colSpan="1" >React.CSSProperties</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Custom inline style</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >searchPlaceholder</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`'Search contacts'`</td>

<td rowspan="1" colSpan="1" >search box placeholder text</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >emptyText</td>

<td rowspan="1" colSpan="1" >string</td>

<td rowspan="1" colSpan="1" >`'No contacts'`</td>

<td rowspan="1" colSpan="1" >Empty status prompt text</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ContactItem</td>

<td rowspan="1" colSpan="1" >React.ComponentType<ContactListItemProps> \| undefined</td>

<td rowspan="1" colSpan="1" >`ContactListItem`</td>

<td rowspan="1" colSpan="1" >Custom contact person component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >ContactSearchComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<ContactSearchProps> \| undefined</td>

<td rowspan="1" colSpan="1" >`ContactSearch`</td>

<td rowspan="1" colSpan="1" >Custom search component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GroupHeader</td>

<td rowspan="1" colSpan="1" >React.ComponentType<{ data: ContactGroup }> \| undefined</td>

<td rowspan="1" colSpan="1" >Default group header</td>

<td rowspan="1" colSpan="1" >Custom group header component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderEmptyList</td>

<td rowspan="1" colSpan="1" >React.ReactNode \| undefined</td>

<td rowspan="1" colSpan="1" >Default empty status</td>

<td rowspan="1" colSpan="1" >Custom empty status component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onContactItemClick</td>

<td rowspan="1" colSpan="1" >(item: ContactGroupItem) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Contact person item click event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onFriendApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: FriendApplication) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Friend request operation event</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onGroupApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: GroupApplication) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Group request operation event</td>
</tr>
</table>


## ContactInfo props
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

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Currently showing contact item</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >showActions</td>

<td rowspan="1" colSpan="1" >boolean</td>

<td rowspan="1" colSpan="1" >`true`</td>

<td rowspan="1" colSpan="1" >whether to display the action button</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >PlaceholderEmpty</td>

<td rowspan="1" colSpan="1" >React.ReactNode \| undefined</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Empty status placeholder component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >FriendInfoComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<FriendInfoProps></td>

<td rowspan="1" colSpan="1" >`FriendInfo`</td>

<td rowspan="1" colSpan="1" >Friend information component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GroupInfoComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<GroupInfoProps></td>

<td rowspan="1" colSpan="1" >`GroupInfo`</td>

<td rowspan="1" colSpan="1" >Group information component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >BlacklistInfoComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<BlacklistInfoProps></td>

<td rowspan="1" colSpan="1" >`BlacklistInfo`</td>

<td rowspan="1" colSpan="1" >Blocklist information component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >FriendApplicationInfoComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<FriendApplicationInfoProps></td>

<td rowspan="1" colSpan="1" >`FriendApplicationInfo`</td>

<td rowspan="1" colSpan="1" >Friend request information component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >GroupApplicationInfoComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<GroupApplicationInfoProps></td>

<td rowspan="1" colSpan="1" >`GroupApplicationInfo`</td>

<td rowspan="1" colSpan="1" >Group application information component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchGroupInfoComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<SearchGroupInfoProps></td>

<td rowspan="1" colSpan="1" >`SearchGroupInfo`</td>

<td rowspan="1" colSpan="1" >Group information search component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >SearchUserInfoComponent</td>

<td rowspan="1" colSpan="1" >React.ComponentType<SearchUserInfoProps></td>

<td rowspan="1" colSpan="1" >`SearchUserInfo`</td>

<td rowspan="1" colSpan="1" >User information search component</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onClose</td>

<td rowspan="1" colSpan="1" >() => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Close message panel callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onSendMessage</td>

<td rowspan="1" colSpan="1" >(friend: Friend) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Message send callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onDeleteFriend</td>

<td rowspan="1" colSpan="1" >(friend: Friend) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Remove friend callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onUpdateFriendRemark</td>

<td rowspan="1" colSpan="1" >(friend: Friend, remark: string) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Update friend remark callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onAddToBlacklist</td>

<td rowspan="1" colSpan="1" >(friend: Friend) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Add to blocklist callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onRemoveFromBlacklist</td>

<td rowspan="1" colSpan="1" >(profile: UserProfile) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Remove from blocklist callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onEnterGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Group entry callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onLeaveGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Group exit callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onDismissGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Group dismissed callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onFriendApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: FriendApplication) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Friend request operation callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onGroupApplicationAction</td>

<td rowspan="1" colSpan="1" >(action: 'accept' \| 'refuse', application: GroupApplication) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Group application operation callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onAddFriend</td>

<td rowspan="1" colSpan="1" >(user: UserProfile, wording: string) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Friend request callback</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >onJoinGroup</td>

<td rowspan="1" colSpan="1" >(group: GroupModel, note: string) => void</td>

<td rowspan="1" colSpan="1" >`undefined`</td>

<td rowspan="1" colSpan="1" >Group join callback</td>
</tr>
</table>


## Basic Usage
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

## Custom Capabilities

### Custom Contact List Search Feature Switch

By setting the `enableSearch` parameter, you can flexibly control the display of the friend search group feature in ContactList.
``` typescript
<ContactList enableSearch={false} />
```

The effect is as shown below.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/3d1879db679511f09b85525400bf7822.png)


### Custom Contact List Contact Group Configuration

`groupConfig` is used for custom group configuration, including title, display sequence, hidden state, etc. The default value is `{}`.



【Custom Group Heading】
``` typescript
import React from 'react';
import { ContactList } from '@tencentcloud/chat-uikit-react';
import { ContactItemType } from '@tencentcloud/chat-uikit-react';

function CustomGroupTitlesContactList() {
  const groupConfig = {
    [ContactItemType.FRIEND]: {
      title: 'My friend',
      order: 1
    },
    [ContactItemType.GROUP]: {
      title: 'My Groups',
      order: 2
    },
    [ContactItemType.FRIEND_REQUEST]: {
      title: 'Friend request',
      order: 0
    }
  };

  return (
    <ContactList
      groupConfig={groupConfig}
      onContactItemClick={(item) => {
        console.log('contact person click:', item);
      }}
    />
  );
}
```

The effect is as shown below.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/3d333139679511f09a9d52540044a08e.png)

【Hide Specific Group】
``` typescript
import React from 'react';
import { ContactList } from '@tencentcloud/chat-uikit-react';
import { ContactItemType } from '@tencentcloud/chat-uikit-react';

function HiddenGroupsContactList() {
  const groupConfig = {
    [ContactItemType.BLACK]: {
      title: 'blocklist',
      hidden: true // hide blocklist grouping
    },
    [ContactItemType.GROUP_REQUEST]: {
      title: 'Group Application',
      hidden: true // hide group application grouping
    }
  };

  return (
    <ContactList
      groupConfig={groupConfig}
      onContactItemClick={(item) => {
        console.log('contact person click:', item);
      }}
    />
  );
}
```

The effect is as shown below.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/3d119649679511f09b85525400bf7822.png)


### Custom Contact List Sub-Item

ContactItem is used for custom rendering component of contact person, with default value as built-in `ContactListItem` component.
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
        console.log('contact person click:', item);
      }}
    />
  );
}
```

The effect is as shown below.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/410ebb3d679511f08e915254007c27c5.png)


### Custom Contact Person Detail Action Button Switch

`showActions` specifies whether to display action buttons. The default value is `true`.
``` typescript
import React from 'react';
import { ContactInfo } from '@tencentcloud/chat-uikit-react';

function ReadOnlyContactInfo() {
  const friendData = {
    type: ContactItemType.FRIEND,
    data: {
      userID: 'user123',
      nick: 'Zhang San',
      avatar: 'https://example.com/avatar.jpg',
      remark: 'colleague',
      // ... other friend properties
    },
  };

  return (
    <ContactInfo 
      contactItem={friendData}
      showActions={false} // Hide ALL action buttons and display information only
    />
  );
}
```

The effect is as shown below.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/3d38fc0c679511f0924f5254005ef0f7.png)


### Custom Contact Person Detail Empty Status

`PlaceholderEmpty` is used for custom empty status display content, default value is `undefined`.
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
      <div>Select one contact person to view detailed information</div>
      <div style={{ marginTop: '8px', fontSize: '12px' }}>
        click any item in the left-side contact list
      </div>
    </div>
  );

  return (
    <ContactInfo 
      PlaceholderEmpty={<EmptyPlaceholder />}
    />
  );
}
```

The effect is as shown below.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/410e35cf679511f0837f525400454e06.png)


### Custom Contact Person Detail Component

> **Note:**
> 
> - `FriendInfoComponent` for custom friend information component, default value is built-in `FriendInfo` component.
> - `GroupInfoComponent` for custom group information component, default value is built-in `GroupInfo` component.
> - `BlacklistInfoComponent` for custom blocklist information component, default value is built-in `BlacklistInfo` component.
> - `FriendApplicationInfoComponent` for custom Friend request information component, default value is built-in `FriendApplicationInfo` component.
> - `GroupApplicationInfoComponent` for custom group application information component, default value is built-in `GroupApplicationInfo` component.




【Custom Friend Information Component】
``` typescript
import React from 'react';
import { ContactInfo } from '@tencentcloud/chat-uikit-react';
import type { FriendInfoProps, Friend } from '@tencentcloud/chat-uikit-react';
import { Button } from '@tencentcloud/uikit-base-component-react';

// Custom Friend Information Component
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
          <p style={{ margin: '0', color: '#666' }}>Remark: {friend.remark}</p>
        </div>
      </div>
      
      <div style={{ display: 'flex', flexDirection: 'column', gap: '10px',  marginBottom: '16px' }}>
        <p><strong>uid:</strong> {friend.userID}</p>
        <p><strong>Personal signature:</strong> {friend.selfSignature}</p>
        <p><strong>Location:</strong> {friend.location}</p>
      </div>


      {showActions && (
        <div style={{ display: 'flex', gap: '8px' }}>
          <Button onClick={() => onSendMessage?.(friend)}>Send Message</Button>
          <Button onClick={() => onDeleteFriend?.(friend)}>Remove Friend</Button>
          <Button onClick={onClose}>Close</Button>
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
      nick: 'Zhang San',
      avatar: 'https://example.com/avatar.jpg',
      remark: 'colleague',
      selfSignature: 'Love technology, love life',
      location: 'Beijing',
      // ... other attributes
    },
  };

  return (
    <ContactInfo 
      contactItem={friendData}
      FriendInfoComponent={CustomFriendInfo}
      onSendMessage={(friend) => console.log('Send message to:', friend.nick)}
      onDeleteFriend={(friend) => console.log('Remove friend:', friend.nick)}
    />
  );
}
```

The effect is as shown below.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/3d11e473679511f0924f5254005ef0f7.png)


【Custom Group Information Component】
``` typescript
import React from 'react';
import { ContactInfo, GroupMemberRole } from '@tencentcloud/uikit-component-react';
import type { GroupInfoProps, GroupModel } from '@tencentcloud/uikit-component-react';
import { Button } from '@tencentcloud/uikit-base-component-react';

// Custom Group Information Component
const CustomGroupInfo: React.FC<GroupInfoProps> = ({ 
  group, 
  showActions, 
  onClose, 
  onEnterGroup,
  onLeaveGroup,
  onDismissGroup 
}) => {
  const isOwner = group.selfInfo?.role === GroupMemberRole.OWNER; // group owner
  const isAdmin = group.selfInfo?.role === GroupMemberRole.ADMIN; // admin

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
            Group ID: {group.groupID}
          </p>
        </div>
      </div>
      
      <div style={{ display: 'flex', flexDirection: 'column', gap: '10px',  marginBottom: '16px' }}>
        <p><strong>Group introduction:</strong> {group.introduction}</p>
        <p><strong>Group notice:</strong> {group.notification}</p>
        <p><strong>Member count:</strong> {group.memberCount}/{group.maxMemberCount}</p>
        <p><strong>My role:</strong> {
          isOwner ? 'group owner' : isAdmin ? 'admin' : 'ordinary member'
        }</p>
      </div>

      {showActions && (
        <div style={{ display: 'flex', gap: '8px' }}>
          <Button onClick={() => onEnterGroup?.(group)}>Enter group</Button>
          <Button onClick={() => onLeaveGroup?.(group)}>Exit group</Button>
          {isOwner && (
            <Button onClick={() => onDismissGroup?.(group)}>Dissolve group</Button>
          )}
          <Button onClick={onClose}>Close</Button>
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
      name: 'technical exchange group',
      avatar: 'https://example.com/group-avatar.jpg',
      type: 'Public',
      introduction: 'technical exchange and sharing',
      notification: 'Welcome to join the technical exchange group',
      ownerID: 'owner123',
      memberCount: 100,
      maxMemberCount: 200,
      selfInfo: {
        userID: 'currentUser',
        role: GroupMemberRole.OWNER, // group owner
        nameCard: 'group owner',
        joinTime: Date.now(),
      },
    },
  };

  return (
    <ContactInfo 
      contactItem={groupData}
      GroupInfoComponent={CustomGroupInfo}
      onEnterGroup={(group) => console.log('Enter group:', group.name)}
      onLeaveGroup={(group) => console.log('Exit group:', group.name)}
      onDismissGroup={(group) => console.log('Dissolve group:', group.name)}
    />
  );
}
```

The effect is as shown below.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/3d17ba45679511f0b5365254001c06ec.png)

【Custom Blocklist Information Component】
``` typescript
import React from 'react';
import { ContactInfo } from '@tencentcloud/uikit-component-react';
import type { BlacklistInfoProps, UserProfile } from '@tencentcloud/uikit-component-react';
import { Button } from '@tencentcloud/uikit-base-component-react';

// Custom Blocklist Information Component
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
          <p style={{ margin: '0', color: '#666' }}>uid: {profile.userID}</p>
        </div>
      </div>
      
      <div style={{ display: 'flex', flexDirection: 'column', gap: '10px',  marginBottom: '16px' }}>
        <p><strong>Personal signature:</strong> {profile.selfSignature}</p>
        <p><strong>Location:</strong> {profile.location}</p>
        <p style={{ color: '#ff4d4f', fontWeight: 'bold' }}>
          This user has been added to the blocklist
        </p>
      </div>

      {showActions && (
        <div style={{ display: 'flex', gap: '8px' }}>
          <Button 
            onClick={() => onRemoveFromBlacklist?.(profile)}
            style={{ backgroundColor: '#52c41a', color: 'white', border: 'none' }}
          >
            Move from blocklist
          </Button>
          <Button onClick={onClose}>Close</Button>
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
      nick: 'Li Si',
      src: 'https://example.com/avatar2.jpg',
      gender: 1,
      birthday: 19920101,
      location: 'Shenzhen',
      selfSignature: 'blocklisted user',
      allowType: 1,
      adminForbidType: 0,
    },
  };

  return (
    <ContactInfo 
      contactItem={blacklistData}
      BlacklistInfoComponent={CustomBlacklistInfo}
      onRemoveFromBlacklist={(profile) => console.log('Removing from blocklist:', profile.nick)}
    />
  );
}
```

The effect is as shown below.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/410ce2c7679511f0837f525400454e06.png)

【Custom Friend Request Information Component】
``` typescript
import React from 'react';
import { ContactInfo } from '@tencentcloud/uikit-component-react';
import type { FriendApplicationInfoProps, FriendApplication } from '@tencentcloud/uikit-component-react';
import { Button } from '@tencentcloud/uikit-base-component-react';

// Custom Friend Request Information Component
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
          <p style={{ margin: '0', color: '#666' }}>Application time: {formatTime(application.time)}</p>
        </div>
      </div>
      
      <div style={{ display: 'flex', flexDirection: 'column', gap: '10px',  marginBottom: '16px' }}>
        <p><strong>Application source:</strong> {application.source}</p>
        <p><strong>Remarks:</strong> {application.wording}</p>
        <p style={{ color: '#1890ff', fontWeight: 'bold' }}>
          Friend request
        </p>
      </div>

      {showActions && (
        <div style={{ display: 'flex', gap: '8px' }}>
          <Button 
            onClick={() => onAccept?.(application)}
            style={{ backgroundColor: '#52c41a', color: 'white', border: 'none' }}
          >
            accept application
          </Button>
          <Button 
            onClick={() => onRefuse?.(application)}
            style={{ backgroundColor: '#ff4d4f', color: 'white', border: 'none' }}
          >
            reject application
          </Button>
          <Button onClick={onClose}>Close</Button>
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
      nick: 'Wang Wu',
      src: 'https://example.com/avatar3.jpg',
      time: Date.now(),
      source: 'search add',
      wording: 'hello, i want to add you as a friend to discuss technology together',
      type: 1,
    },
  };

  return (
    <ContactInfo 
      contactItem={applicationData}
      FriendApplicationInfoComponent={CustomFriendApplicationInfo}
      onFriendApplicationAction={(action, application) => {
        if (action === 'accept') {
          console.log('Accept friend request:', application.nick);
        } else {
          console.log('Refuse friend application:', application.nick);
        }
      }}
    />
  );
}
```

The effect is as shown below.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/3d12304b679511f0bd33525400e889b2.png)

【Custom Group Application Information Component】
``` typescript
import React from 'react';
import { ContactInfo } from '@tencentcloud/uikit-component-react';
import type { GroupApplicationInfoProps, GroupApplication } from '@tencentcloud/uikit-component-react';
import { Button } from '@tencentcloud/uikit-base-component-react';

// Custom Group Application Information Component
const CustomGroupApplicationInfo: React.FC<GroupApplicationInfoProps> = ({ 
  application, 
  showActions, 
  onClose, 
  onAccept,
  onRefuse 
}) => {
  const getApplicationTypeText = (type: number) => {
    return type === 0 ? 'user application to join' : 'invite user joined';
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
        <p><strong>Applicant:</strong> {application.applicantNick}</p>
        <p><strong>Group ID:</strong> {application.groupID}</p>
        <p><strong>Application remarks:</strong> {application.note}</p>
        <p style={{ color: '#1890ff', fontWeight: 'bold' }}>
          Group request pending
        </p>
      </div>

      {showActions && (
        <div style={{ display: 'flex', gap: '8px' }}>
          <Button 
            onClick={() => onAccept?.(application)}
            style={{ backgroundColor: '#52c41a', color: 'white', border: 'none' }}
          >
            Approving Applications
          </Button>
          <Button 
            onClick={() => onRefuse?.(application)}
            style={{ backgroundColor: '#ff4d4f', color: 'white', border: 'none' }}
          >
            reject application
          </Button>
          <Button onClick={onClose}>Close</Button>
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
      applicantNick: 'Zhao Liu',
      groupID: 'group456',
      groupName: 'product manager communication group',
      applicationType: 0,
      userID: 'user999',
      note: 'I want to join the product manager communication group to learn product design experience',
    },
  };

  return (
    <ContactInfo 
      contactItem={applicationData}
      GroupApplicationInfoComponent={CustomGroupApplicationInfo}
      onGroupApplicationAction={(action, application) => {
        if (action === 'accept') {
          console.log('Approve group request:', application.groupName);
        } else {
          console.log('Reject group request:', application.groupName);
        }
      }}
    />
  );
}
```

The effect is as shown below.

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027116646/3d42e3cb679511f08e915254007c27c5.png)

## 