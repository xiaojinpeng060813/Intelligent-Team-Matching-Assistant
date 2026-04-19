<template>
  <div class="page bg-gray-50" :class="{ active: isActive }">
    <!-- 顶部导航栏 -->
    <div class="top-nav">
      <i class="fa fa-arrow-left back-icon" @click="handleBack"></i>
      <h2 class="nav-title">我的发布</h2>
    </div>

    <!-- 发布卡片列表 -->
    <div class="content-wrapper">
      <!-- 单个发布卡片 -->
      <div class="publish-card" v-for="item in publishList" :key="item.id">
        <div class="card-header">
          <div class="header-left">
            <!-- 替换为参考图的奖杯样式，更贴近视觉效果 -->
            <div class="trophy-box">
              <i class="fa fa-trophy trophy-icon"></i>
            </div>
            <div class="title-wrap">
              <h3 class="card-title">{{ item.title }}</h3>
              <p class="card-time">{{ item.time }}</p>
            </div>
          </div>
          <div class="header-right">
            <span class="tag-competition">{{ item.tag }}</span>
            <span class="tag-count">{{ item.count }}</span>
          </div>
        </div>
        <div class="card-content">
          <p class="content-text">{{ item.desc }}</p>
          <i class="fa fa-angle-right content-arrow"></i>
        </div>
        <div class="card-footer">
          <div class="user-info">
            <!-- 参考图的圆形头像样式 -->
            <div class="avatar">{{ item.userName.charAt(0) }}</div>
            <div class="user-detail">
              <p class="user-name">{{ item.userName }}</p>
              <p class="user-major">{{ item.userMajor }}</p>
            </div>
          </div>
          <button class="delete-btn" @click="handleDelete(item.id)">
            <i class="fa fa-trash-o"></i>删除
          </button>
        </div>
      </div>

      <!-- 空状态 -->
      <div class="empty-state" v-if="publishList.length === 0">
        <i class="fa fa-paper-plane-o empty-icon"></i>
        <p class="empty-text">暂无发布的招募信息</p>
        <button class="empty-btn" @click="handleAddPublish">去发布</button>
      </div>
    </div>

    <!-- 右下角发布按钮 -->
    <div class="publish-btn" @click="handleAddPublish">
      <i class="fa fa-paper-plane publish-icon"></i>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  isActive: {
    type: Boolean,
    default: false
  }
});

const emit = defineEmits(['change-page']);

// 模拟数据
const publishList = ref([
  {
    id: 1,
    title: '全国大学生数学建模大赛',
    time: '2小时前',
    tag: '竞赛',
    count: '1/3',
    desc: '组建团队参加2026年全国大学生数学建模竞赛...',
    userName: '张同学',
    userMajor: '计算机科学与技术 · 大三'
  }
]);

// 返回个人中心
const handleBack = () => {
  console.log('点击返回，切回个人中心');
  emit('change-page', 3);
};

// 新增发布
const handleAddPublish = () => {
  alert('即将跳转到发布招募信息页面～');
};

// 删除发布
const handleDelete = (id) => {
  if (confirm('确定要删除这条发布吗？')) {
    publishList.value = publishList.value.filter(item => item.id !== id);
  }
};
</script>

<style scoped>
/* 核心样式：仅优化卡片视觉，其他全保留 */
.page {
  display: none;
  min-height: 100vh;
  background-color: #f9fafb;
  font-family: "PingFang SC", "Microsoft YaHei", sans-serif;
}
.page.active {
  display: block;
  width: 100%;
}

/* 顶部导航 */
.top-nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 50px;
  background-color: #9333ea;
  color: #fff;
  display: flex;
  align-items: center;
  padding: 0 16px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.03);
  z-index: 99;
}
.back-icon {
  font-size: 20px;
  cursor: pointer;
  margin-right: 15px;
}
.nav-title {
  font-size: 19px;
  font-weight: 600;
}

/* 内容区 */
.content-wrapper {
  padding: 70px 16px 80px;
  box-sizing: border-box;
}

/* 发布卡片：完全参照参考图重构样式 */
.publish-card {
  background-color: #fff;
  border-radius: 12px; /* 更圆润的圆角，贴近参考图 */
  padding: 20px 16px;
  margin-bottom: 16px;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.08); /* 更柔和的阴影 */
  border: 1px solid #f0f0f0; /* 浅边框增加层次感 */
}
.card-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 12px;
}
.header-left {
  display: flex;
  align-items: flex-start;
}
/* 参考图的奖杯背景盒，更醒目 */
.trophy-box {
  width: 36px;
  height: 36px;
  border-radius: 8px;
  background-color: #ecfdf3;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 12px;
}
.trophy-icon {
  font-size: 18px;
  color: #059669; /* 参考图的绿色调 */
  margin-top: 0;
}
.title-wrap .card-title {
  font-size: 17px;
  font-weight: 600;
  color: #1f2937; /* 更深的标题色，更醒目 */
  margin: 0 0 4px 0;
  line-height: 1.3;
}
.title-wrap .card-time {
  font-size: 13px;
  color: #6b7280;
  margin: 0;
}
.header-right {
  display: flex;
  align-items: center;
  gap: 8px; /* 更合理的间距 */
}
.tag-competition {
  font-size: 12px;
  background-color: #eff6ff; /* 参考图的竞赛标签蓝色调 */
  color: #2563eb;
  padding: 3px 10px;
  border-radius: 6px; /* 更圆润的标签 */
  font-weight: 500;
}
.tag-count {
  font-size: 13px;
  color: #6b7280;
  background-color: #f9fafb;
  padding: 2px 8px;
  border-radius: 4px;
}

/* 卡片内容：贴近参考图的简洁样式 */
.card-content {
  position: relative;
  margin: 12px 0;
  padding-right: 24px;
  border-bottom: 1px solid #f5f5f5; /* 分割线，参考图视觉层次 */
  padding-bottom: 16px;
}
.content-text {
  font-size: 14px;
  color: #4b5563;
  margin: 0;
  line-height: 1.5;
  color: #6b7280; /* 参考图的正文浅色调 */
}
.content-arrow {
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  font-size: 18px;
  color: #d1d5db; /* 更浅的箭头，不抢视觉 */
}

/* 卡片底部：参考图的用户信息样式 */
.card-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 12px;
}
.user-info {
  display: flex;
  align-items: center;
}
.avatar {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background-color: #2563eb; /* 参考图的蓝色头像 */
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 14px;
  font-weight: 600;
}
.user-detail {
  margin-left: 10px;
}
.user-name {
  font-size: 15px;
  color: #1f2937;
  margin: 0;
  font-weight: 500;
}
.user-major {
  font-size: 12px;
  color: #6b7280;
  margin: 2px 0 0 0;
}
.delete-btn {
  font-size: 12px;
  background-color: #fef2f2; /* 更柔和的删除按钮底色 */
  color: #dc2626;
  border: none;
  padding: 5px 10px;
  border-radius: 6px;
  display: flex;
  align-items: center;
  cursor: pointer;
}
.delete-btn:hover {
  background-color: #fee2e2;
}
.delete-btn .fa-trash-o {
  margin-right: 4px;
}

/* 空状态 */
.empty-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 80px 20px;
  color: #999;
}
.empty-icon {
  font-size: 64px;
  color: #e5e7eb;
}
.empty-text {
  font-size: 14px;
  color: #6b7280;
  margin-top: 8px;
}
.empty-btn {
  font-size: 14px;
  color: #409eff;
  border: none;
  background: none;
  margin-top: 16px;
  cursor: pointer;
}

/* 右下角发布按钮：保留所有位置/大小，仅新增居中强制样式 */
.publish-btn {
  position: fixed;
  bottom: 120px;
  right: 30px;
  width: 80px;
  height: 80px;
  border-radius: 50%;
  background-color: #409eff;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 12px rgba(64, 158, 255, 0.4);
  cursor: pointer;
  z-index: 98;
  transition: all 0.2s ease;
  padding: 0;
  border: none;
  box-sizing: border-box; /* 新增：强制盒模型消除干扰 */
  outline: none; /* 新增：消除轮廓干扰 */
}
.publish-btn:hover {
  transform: scale(1.05);
  box-shadow: 0 6px 16px rgba(64, 158, 255, 0.5);
}
.publish-btn:active {
  transform: scale(0.95);
}
.publish-icon {
  font-size: 30px;
  color: #fff;
  line-height: 0;
  margin: 0;
  display: block;
  transform: translate(-3px, 0); /* 仅修改这行：左移3px（3磅） */
}
</style>