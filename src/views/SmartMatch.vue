<template>
  <div class="page" :class="{ active: isActive }">
    <!-- 顶部标题栏（原生CSS，无依赖） -->
    <div class="match-header">
      <div class="header-content">
        <!-- 图标 -->
        <i class="fa fa-exchange text-white" style="font-size: 32px;"></i>
        <!-- 标题文字容器 -->
        <div class="title-text">
          <h2 class="text-white text-xl font-bold">智能匹配</h2>
          <p class="text-white/80 text-sm">基于AI算法，为您推荐最适合的队友</p>
        </div>
      </div>
    </div>

    <!-- 表单区域 -->
    <div class="form-wrapper">
      <div class="form-container">
        <h3 class="form-title">选择您所要匹配的类型</h3>
        
        <!-- 类别 -->
        <div class="form-item">
          <label class="form-label">类别</label>
          <select class="form-input">
            <option>不限</option>
            <option>竞赛</option>
            <option>考研</option>
            <option>运动</option>
          </select>
        </div>

        <!-- 年级 -->
        <div class="form-item">
          <label class="form-label">年级</label>
          <select class="form-input">
            <option>不限</option>
            <option>大一</option>
            <option>大二</option>
            <option>大三</option>
            <option>大四</option>
          </select>
        </div>

        <!-- 学院 -->
        <div class="form-item">
          <label class="form-label">学院</label>
          <input 
            type="text" 
            placeholder="请输入您的学院" 
            class="form-input"
          >
        </div>

        <!-- 专业 -->
        <div class="form-item">
          <label class="form-label">专业</label>
          <input 
            type="text" 
            placeholder="请输入您的专业" 
            class="form-input"
          >
        </div>

        <!-- 主题 -->
        <div class="form-item">
          <label class="form-label">主题</label>
          <input 
            type="text" 
            placeholder="如数学建模大赛、程序设计大赛" 
            class="form-input"
          >
        </div>

        <!-- 其他 -->
        <div class="form-item">
          <label class="form-label">其他</label>
          <textarea 
            placeholder="请输入额外的匹配要求 (如技能、时间等)" 
            class="form-textarea"
          ></textarea>
        </div>

        <!-- 匹配按钮（原生交互，无依赖） -->
        <button 
          @click="openDetailPage" 
          class="match-btn"
        >
          匹配
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  isActive: {
    type: Boolean,
    default: false
  }
});

const emit = defineEmits(['open-detail']);
const openDetailPage = () => {
  emit('open-detail');
};
</script>

<style scoped>
/* 核心修改：完全对齐参考代码的page样式，去掉多余属性，保留核心铺满逻辑 */
.page {
  display: none;
  min-height: 100vh; /* 和参考代码一致，占满视口高度 */
  background-color: #f9f9f9; /* 灰色背景 */
  margin: 0 !important; /* 强制清除外边距 */
  padding: 0 !important; /* 强制清除内边距 */
  width: 100% !important; /* 宽度100%，绑定父容器（视口） */
}

.page.active {
  display: block;
  width: 100% !important; /* 和参考代码一致，仅用100%，不用vw避免滚动 */
}

/* 核心修改：参考fixed-header的写法，用left/right:0替代width，强制全屏 */
.match-header {
  background-color: #1E88E5;
  position: fixed !important;
  top: 0 !important;
  left: 0 !important; /* 强制左对齐 */
  right: 0 !important; /* 强制右对齐 → 自动铺满宽度 */
  z-index: 9999;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.03); /* 可选：和参考代码保持视觉一致 */
}

/* 内容区内边距保留，仅去掉多余的margin */
.header-content {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 16px; /* 仅内部padding，不影响整体宽度 */
  box-sizing: border-box;
}

.title-text {
  display: flex;
  flex-direction: column;
  justify-content: center;
  line-height: 1.4;
}

.title-text h2 {
  font-size: 20px;
  margin: 0;
  color: white;
  font-weight: bold;
}

.title-text p {
  font-size: 14px;
  margin: 0;
  color: rgba(255, 255, 255, 0.8);
}

/* 核心：表单容器仅内部padding，不设置左右margin，宽度100% */
.form-wrapper {
  padding: 0 16px; /* 仅内部左右内边距，不影响灰色背景铺满 */
  box-sizing: border-box;
  margin-top: 88px; /* 给固定头部留空间 */
  width: 100%;
}

.form-container {
  background-color: white;
  border-radius: 8px;
  padding: 20px;
  margin-top: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
  box-sizing: border-box;
  margin-bottom: 100px;
  width: 100%;
}

.form-title {
  font-size: 18px;
  font-weight: 600;
  margin: 0 0 16px 0;
  color: #333;
}

.form-item {
  margin-bottom: 16px;
}

.form-label {
  display: block;
  color: #333;
  font-size: 14px;
  font-weight: 500;
  margin-bottom: 8px;
}

.form-input {
  width: 100%;
  padding: 12px 16px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  font-size: 14px;
  box-sizing: border-box;
  outline: none;
}

.form-input:focus {
  border-color: #1E88E5;
  box-shadow: 0 0 0 2px rgba(30, 136, 229, 0.1);
}

.form-textarea {
  width: 100%;
  padding: 12px 16px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  font-size: 14px;
  min-height: 80px;
  box-sizing: border-box;
  outline: none;
  resize: vertical;
}

.form-textarea:focus {
  border-color: #1E88E5;
  box-shadow: 0 0 0 2px rgba(30, 136, 229, 0.1);
}

.match-btn {
  width: 100%;
  padding: 12px;
  background-color: #1E88E5;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 18px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s ease;
  box-sizing: border-box;
}

.match-btn:hover {
  background-color: #1976D2;
}

.match-btn:active {
  background-color: #1565C0;
}
</style>
