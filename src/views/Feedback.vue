<template>
  <!-- 反馈页面容器：参考榜样代码的布局逻辑，isActive控制显隐 -->
  <div class="page bg-gray-50" :style="{ display: isActive ? 'block' : 'none' }">
    <!-- 头部导航栏：吸顶+和榜样代码一致的视觉风格 -->
    <div class="fixed-header">
      <div class="feedback-header">
        <div class="back-icon" @click="handleBack">←</div>
        <div class="header-title">反馈</div>
      </div>
    </div>

    <!-- 核心内容区：参考榜样代码的content-wrapper逻辑，优化留白 -->
    <div class="content-wrapper">
      <div class="feedback-card">
        <div class="card-title">意见反馈</div>
        <textarea 
          class="feedback-textarea"
          placeholder="请输入内容"
          rows="10"
          v-model="feedbackContent"
        ></textarea>
        <button class="submit-btn" @click="handleSubmit">提 交</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// 接收父组件传递的显隐状态
const props = defineProps({
  isActive: {
    type: Boolean,
    default: false
  }
});

// 定义事件发射器，向App.vue发送页面切换指令
const emit = defineEmits(['change-page']);

// 反馈内容绑定
const feedbackContent = ref('');

// 返回个人中心（通过emit触发App.vue的页面切换）
const handleBack = () => {
  console.log('点击返回：回到个人中心');
  emit('change-page', 3); // 3 = 个人中心页面
};

// 提交反馈（提交后自动返回）
const handleSubmit = () => {
  if (!feedbackContent.value.trim()) {
    alert('请输入反馈内容！');
    return;
  }
  alert('反馈提交成功！感谢您的建议～');
  feedbackContent.value = ''; // 清空输入框
  handleBack(); // 提交后返回个人中心
};
</script>

<style scoped>
/* 核心：参考榜样代码的page样式，保证灰色底纹铺满 */
.page {
  display: none;
  min-height: 100vh; /* 强制占满视口高度 */
  width: 100%;
  box-sizing: border-box;
  margin: 0;
  padding: 0; /* 清除默认边距，确保底纹铺满 */
  font-family: "PingFang SC", "Microsoft YaHei", sans-serif;
}
.page.active {
  display: block;
}

/* 匹配榜样代码的自然灰色：bg-gray-50（#f9fafb），不刺眼 */
.bg-gray-50 {
  background-color: #f9fafb !important;
}

/* 头部吸顶：参考榜样代码的fixed-header逻辑 */
.fixed-header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background-color: #fff; /* 头部白色背景，和榜样代码一致 */
  z-index: 99;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.03); /* 轻微阴影，提升层次 */
}

/* 头部导航栏：适配移动端，高度舒适 */
.feedback-header {
  width: 100%;
  height: 50px;
  display: flex;
  align-items: center;
  padding: 0 1rem; /* 和榜样代码一致的左右内边距（16px） */
  box-sizing: border-box;
}

/* 返回箭头：大小适中，交互友好 */
.back-icon {
  font-size: 20px;
  color: #333;
  margin-right: 15px;
  cursor: pointer;
  font-weight: 600;
  transition: color 0.2s ease;
}
.back-icon:hover {
  color: #409eff; /* 匹配榜样代码的主色 */
}

/* 头部标题：字体大小适配 */
.header-title {
  font-size: 19px;
  color: #333;
  font-weight: 600;
}

/* 内容区：参考榜样代码的content-wrapper，优化顶部内边距+左右留白 */
.content-wrapper {
  padding: 70px 1rem 2rem; /* 顶部留头部空间，左右16px（舒适留白），底部2rem */
  box-sizing: border-box;
  width: 100%;
}

/* 反馈卡片：左右无额外留白（复用content-wrapper的1rem），视觉更舒展 */
.feedback-card {
  background-color: #fff;
  border-radius: 12px; /* 适度圆角，不夸张 */
  padding: 20px; /* 内部内边距，保证内容不拥挤 */
  box-sizing: border-box;
  width: 100%;
  box-shadow: 0 1px 3px rgba(0,0,0,0.05); /* 轻微阴影，和榜样代码一致 */
}

/* 卡片标题：字体大小舒适 */
.card-title {
  font-size: 18px;
  color: #333;
  font-weight: 600;
  margin-bottom: 15px;
}

/* 输入框：匹配整体风格，字体舒适 */
.feedback-textarea {
  width: 100%;
  height: auto;
  box-sizing: border-box;
  padding: 15px;
  border: 1px solid #e5e5e5;
  border-radius: 8px;
  resize: none;
  font-size: 16px;
  color: #333;
  outline: none;
  line-height: 1.6;
}
.feedback-textarea::placeholder {
  color: #999;
  font-size: 16px;
}

/* 提交按钮：圆角+加粗+主色，视觉舒适 */
.submit-btn {
  width: 100%;
  height: 50px;
  background-color: #409eff; /* 匹配榜样代码的主色 */
  color: #fff;
  border: none;
  border-radius: 8px; /* 适度圆角 */
  font-size: 18px;
  font-weight: 700; /* 文字加粗 */
  margin-top: 20px;
  cursor: pointer;
  transition: background-color 0.2s ease;
}
.submit-btn:active {
  background-color: #337ecc; /* 点击态加深，更友好 */
}
</style>