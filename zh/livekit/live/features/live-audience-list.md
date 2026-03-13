> ## Documentation Index
> Fetch the complete documentation index at: https://raw.githubusercontent.com/lianjun0809/docs/main/zh/llms.txt
> Use this file to discover all available pages before exploring further.

本文对 TUILiveKit 组件中的**观众列表组件（LiveAudienceList）**进行了详细的介绍，您可以在已有项目中直接参考本文示例集成我们开发好的组件，也可以根据您的需求按照文档中的组件定制化部分对样式，布局进行深度的定制。

## 核心功能
| **功能分类** | **具体能力** |
| --- | --- |
| **实时观众展示** | 实时显示直播间在线观众列表，支持头像、昵称展示，提供清晰的观众信息视图，让主播能够直观了解观众构成 |
| **响应式设计** | 组件支持桌面端和移动端两套UI方案，自动适配不同设备屏幕尺寸，提供一致的用户体验，满足多平台直播需求 |
| **可定制化 UI** | 提供灵活的插槽机制，支持自定义观众标记、头像样式等元素，让您能够根据业务需求定制观众列表的展示效果，打造独特的视觉体验 |

## 组件接入

### 步骤1：环境配置及开通服务

在进行快速接入之前，您需要参见 准备工作，满足相关环境配置及开通对应服务。

### 步骤2: 安装依赖

【npm】
``` bash
npm install tuikit-atomicx-vue3@latest @tencentcloud/uikit-base-component-vue3 --save
```

【pnpm】
``` bash
pnpm add tuikit-atomicx-vue3@latest @tencentcloud/uikit-base-component-vue3
```

【yarn】
``` bash
yarn add tuikit-atomicx-vue3@latest @tencentcloud/uikit-base-component-vue3
```

### 步骤3：集成观众列表组件

在您的项目中引入并使用**观众列表组件**，可直接复制如下代码示例至您的项目中展示直播间观众列表。
``` typescript
<template>
  <UIKitProvider theme="dark" language="zh-CN">
    <div class="app">
        <div class="live-audience-container">
          <LiveAudienceList class="live-audience-list"/>
      </div>
    </div>
  </UIKitProvider>
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import { UIKitProvider } from '@tencentcloud/uikit-base-component-vue3';
import { LiveAudienceList, useLoginState, useLiveState } from 'tuikit-atomicx-vue3';

const { login } = useLoginState();
const { joinLive } = useLiveState();

async function initLogin() {
  try {
    await login({
      sdkAppId: 0,        // SDKAppID, 可以参考步骤 1 获取
      userId: '',         // UserID, 可以参考步骤 1 获取
      userSig: '',        // userSig, 可以参考步骤 1 获取
    });
  } catch (error) {
    console.error('登录失败:', error);
  }
}

onMounted(async () => {
  await initLogin();                    
  await joinLive({
    liveId: '输入对应直播间 LiveId',     // 进入直播间
  });
});
</script>

<style>.live-audience-container{display:flex;height:100%;width:300px;padding:20px}.live-audience-list{width:100%;height:100%}</style>
```

## 组件定制化

**观众列表组件**提供了灵活的组件自定义插槽，该插槽支持您根据自己需求调整观众标记、特殊身份标识等元素的样式与布局。下列分别给出插槽使用示例

### 组件插槽
| **名称** | **参数** | **说明** |
| --- | --- | --- |
| customAudienceInfo | audience: AudienceInfo | 自定义观众信息的显示 UI |

``` typescript
// customAudienceInfo 插槽使用示例
<LiveAudienceList>
   <CustomAudienceInfo #customAudienceInfo />
</LiveAudienceList>
```

`AudienceInfo` 定义了直播房间中每个观众的基本信息和状态：
| **参数** | **类型** | **说明** |
| --- | --- | --- |
| userId | string | 观众的唯一标识符，在整个系统中保持唯一性。 |
| userName | string | 观众在直播中显示的名称，支持中文、英文等字符，为空时显示 userId。 |
| avatarUrl | string | 观众头像的完整 URL 地址，支持 HTTPS 协议。 |
| isMessageDisabled | boolean | 观众是否被禁言，true 表示已被禁言，false 表示可以正常发言。 |
| joinTime | number | 观众进入直播间的时间戳，用于排序和统计。 |

``` typescript
interface AudienceInfo {
  userId: string;              // 观众唯一标识
  userName?: string;           // 观众显示名称（可选）
  avatarUrl?: string;          // 观众头像URL（可选）
  isMessageDisabled?: boolean; // 是否被禁言（可选）
  joinTime?: number;           // 进入时间戳（可选）
} 
```

### 组件属性
| **属性名** | **类型** | **默认值** | **说明** |
| --- | --- | --- | --- |
| height | string | '500px' | 组件高度，支持 CSS 单位（px、%、vh等）。 |
| style | CSSProperties | {} | 自定义样式对象，用于覆盖组件默认样式。 |

#### 自定义插槽示例

为了更好地让您体验及理解**观众列表组件** 组件的 **customAudienceInfo **插槽定制化能力，我们提供了**自定义个人信息**示例场景供您参考，您可以参考上述**步骤3**将如下代码增量复制至您的项目中实现类似场景的效果。
``` typescript
<template>
  <LiveAudienceList>
    <template #customAudienceInfo="{ audience }">
      <div class="custom-audience-info">
        <!-- 头像 -->
        <img 
          :src="audience.avatarUrl || defaultAvatar" 
          :alt="audience.userName || audience.userId"
          class="audience-avatar"
        />
        
        <!-- 观众信息 -->
        <div class="audience-details">
          <span class="audience-name">{{ audience.userName || audience.userId }}</span>
          <span class="join-time">{{ formatJoinTime(audience.joinTime) }}</span>
        </div>
        
        <!-- 状态指示器 -->
        <div v-if="audience.isMessageDisabled" class="muted-indicator">🔇</div>
      </div>
    </template>
  </LiveAudienceList>
</template>

<script setup lang="ts">
import { LiveAudienceList } from 'tuikit-atomicx-vue3';

const defaultAvatar = 'xxx'; // 输入默认头像 Url

const formatJoinTime = (timestamp?: number) => {  // 格式化加入时间
  if (!timestamp) return '刚刚加入';
  
  const now = Date.now();
  const diff = now - timestamp;
  const minutes = Math.floor(diff / (1000 * 60));
  const hours = Math.floor(diff / (1000 * 60 * 60));
  const days = Math.floor(diff / (1000 * 60 * 60 * 24));
  
  if (days > 0) return `${days}天前加入`;
  if (hours > 0) return `${hours}小时前加入`;
  if (minutes > 0) return `${minutes}分钟前加入`;
  return '刚刚加入';
};
</script>

<style scoped>.custom-audience-info{display:flex;align-items:center;gap:12px;padding:8px;border-radius:8px;transition:background-color .2s ease}.custom-audience-info:hover{background-color:var(--uikit-color-gray-1)}.audience-avatar{width:40px;height:40px;border-radius:50%;object-fit:cover;border:2px solid var(--uikit-color-gray-3)}.audience-details{flex:1;display:flex;flex-direction:column;gap:4px}.audience-name{font-size:14px;font-weight:500;color:var(--text-color-primary);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}.join-time{font-size:12px;color:var(--text-color-secondary)}.muted-indicator{font-size:16px;opacity:.6}</style>
```
