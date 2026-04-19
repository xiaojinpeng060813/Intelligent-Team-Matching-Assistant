<template>
  <div class="page bg-gray-50" :class="{ active: isActive }">
    <!-- 顶部导航栏：完全保留你原代码样式，未做任何修改 -->
    <div class="detail-header flex items-center w-full fixed top-0 left-0 z-50 px-4 py-2">
      <i class="fa fa-angle-left text-3xl text-white mr-3 cursor-pointer" @click="handleBack"></i>
      <h2 class="text-xl font-bold text-white">招募详情</h2>
    </div>

    <!-- 核心内容区：仅修改 padding-top（从pt-18改为pt-20），增大基础留白 -->
    <div class="content-wrapper px-4 pt-20 pb-20">
      <!-- 1. 招募标题卡片：仅修改 mt-4 改为 mt-6（进一步增大顶部留白），其余原样 -->
      <div class="bg-white mt-6 p-4 rounded-lg">
        <div class="flex items-center mb-2">
          <span class="bg-purple-100 text-purple-600 text-xs px-2 py-0.5 rounded-full mr-2 flex items-center">
            <i class="fa fa-trophy text-xs mr-1"></i>竞赛
          </span>
          <h3 class="text-lg font-bold text-black flex-1">{{ detailInfo.title }}</h3>
        </div>
        <p class="text-gray-600 text-sm leading-relaxed mb-3">{{ detailInfo.desc }}</p>
        <div class="flex items-center text-xs text-gray-500">
          <i class="fa fa-clock-o mr-1"></i>
          <span>{{ detailInfo.time }}</span>
          <span class="mx-2">|</span>
          <i class="fa fa-users mr-1"></i>
          <span>{{ detailInfo.count }}</span>
        </div>
      </div>

      <!-- 2. 队友要求模块：完全保留你原代码样式，未做任何修改 -->
      <div class="bg-white mt-3 p-4 rounded-lg">
        <h4 class="text-base font-medium text-black mb-3">队友要求</h4>
        <ul class="text-sm text-gray-600 space-y-2">
          <li class="flex items-start">
            <i class="fa fa-check-circle text-green-500 mt-0.5 mr-2 text-xs"></i>
            <span>{{ detailInfo.requirement1 || '熟练掌握Python、C语言、Java等两种及以上编程语言' }}</span>
          </li>
          <li class="flex items-start">
            <i class="fa fa-check-circle text-green-500 mt-0.5 mr-2 text-xs"></i>
            <span>{{ detailInfo.requirement2 || '逻辑分析能力、数据分析能力好' }}</span>
          </li>
          <li class="flex items-start">
            <i class="fa fa-check-circle text-green-500 mt-0.5 mr-2 text-xs"></i>
            <span>{{ detailInfo.requirement3 || '具有良好的论文写作能力' }}</span>
          </li>
          <li class="flex items-start">
            <i class="fa fa-check-circle text-green-500 mt-0.5 mr-2 text-xs"></i>
            <span>{{ detailInfo.requirement4 || '时间充裕、能全程参与比赛（9月中上旬之前）、服从团队安排' }}</span>
          </li>
          <li class="flex items-start">
            <i class="fa fa-check-circle text-green-500 mt-0.5 mr-2 text-xs"></i>
            <span>{{ detailInfo.requirement5 || '数学专业、计算机专业、电子信息专业及其相关专业以及有相关竞赛经验者优先' }}</span>
          </li>
        </ul>
      </div>

      <!-- 3. 发布者信息模块：完全保留你原代码样式，未做任何修改 -->
      <div class="bg-white mt-3 p-4 rounded-lg">
        <h4 class="text-base font-medium text-black mb-3">发布者信息</h4>
        <div class="flex items-center">
          <div class="w-12 h-12 rounded-full bg-blue-500 text-white flex items-center justify-center font-bold text-xl mr-3">
            {{ (detailInfo.name || '张').charAt(0) }}
          </div>
          <div class="flex-1 text-left">
            <p class="text-base font-medium text-black">{{ detailInfo.name || '张同学' }}</p>
            <p class="text-xs text-gray-500">{{ detailInfo.major || '计算机科学与技术 · 大三' }}</p>
          </div>
        </div>
        <div class="mt-3 flex flex-wrap gap-2">
          <span v-for="(tag, idx) in (detailInfo.skills || ['Python', 'C语言', 'C++', '数据分析', 'JavaScript'])" :key="idx" 
                class="bg-blue-100 text-blue-600 text-xs px-2 py-1 rounded-full">
            {{ tag }}
          </span>
        </div>
      </div>

      <!-- 4. 群聊二维码模块：完全保留你原代码样式，未做任何修改 -->
      <div class="bg-white mt-3 p-4 rounded-lg mb-6">
        <h4 class="text-base font-medium text-black mb-3">群聊二维码</h4>
        <div class="qrcode-container bg-white border border-gray-200 rounded-lg p-3 w-48 mx-auto">
          <img :src="detailInfo.qrcode || 'https://via.placeholder.com/150/FFFFFF/000000?text=群聊二维码'" 
               alt="群聊二维码" class="w-full h-auto">
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue';

const props = defineProps({
  isActive: {
    type: Boolean,
    default: false
  },
  detailInfo: {
    type: Object,
    default: () => ({
      id: 0,
      title: '全国大学生数学建模大赛',
      tag: '竞赛',
      desc: '组建团队参加2026年全国大学生数学建模竞赛，团队已有一名指导老师，欢迎擅长编程和论文写作的伙伴加入！',
      time: '2小时前',
      count: '1/3',
      name: '张同学',
      major: '计算机科学与技术 · 大三',
      skills: ['Python', 'C语言', 'C++', '数据分析', 'JavaScript'],
      requirement1: '熟练掌握Python、C语言、Java等两种及以上编程语言',
      requirement2: '逻辑分析能力、数据分析能力好',
      requirement3: '具有良好的论文写作能力',
      requirement4: '时间充裕、能全程参与比赛（9月中上旬之前）、服从团队安排',
      requirement5: '数学专业、计算机专业、电子信息专业及其相关专业以及有相关竞赛经验者优先',
      qrcode: ''
    })
  }
});

const emit = defineEmits(['back']);
const handleBack = () => {
  emit('back');
};
</script>

<style scoped>
.page {
  display: none;
  min-height: 100vh;
  overflow-x: hidden;
  background-color: #f5f5f5 !important;
}

.page.active {
  display: block;
  width: 100%;
}

/* 顶部导航栏：完全保留你原代码样式，未做任何修改 */
.detail-header {
  height: 50px;
  box-sizing: border-box;
  background-color: #2595F6 !important;
}

/* 内容区：仅修改 padding-top（从52px改为60px），增大基础留白，其余原样 */
.content-wrapper {
  width: 100%;
  box-sizing: border-box;
  padding-top: 60px !important; 
  padding-bottom: 60px !important;
}

/* 统一样式：完全保留你原代码样式，未做任何修改 */
.qrcode-container {
  box-sizing: border-box;
}
.leading-relaxed {
  line-height: 1.5;
}
.rounded-lg {
  border-radius: 8px;
}
.rounded-full {
  border-radius: 9999px;
}
</style>