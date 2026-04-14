<template>
  <div class="bottom-nav rounded-t-nav py-4 px-6 shadow-md">
    <div class="flex justify-around items-center">
      <!-- 招聘广场 -->
      <div 
        class="nav-item flex flex-col items-center justify-center"
        :class="activePage === 1 ? 'nav-active' : 'nav-inactive'"
        @click="handleNavClick(1)"
      >
        <div class="icon-wrapper mb-1">
          <i class="fa fa-home text-2xl"></i>
        </div>
        <span class="text-sm font-medium">招聘广场</span>
      </div>
      <!-- 智能推荐 -->
      <div 
        class="nav-item flex flex-col items-center justify-center"
        :class="activePage === 2 ? 'nav-active' : 'nav-inactive'"
        @click="handleNavClick(2)"
      >
        <div class="icon-wrapper mb-1">
          <i class="fa fa-random text-2xl"></i>
        </div>
        <span class="text-sm font-medium">智能推荐</span>
      </div>
      <!-- 个人信息 -->
      <div 
        class="nav-item flex flex-col items-center justify-center"
        :class="activePage === 3 ? 'nav-active' : 'nav-inactive'"
        @click="handleNavClick(3)"
      >
        <div class="icon-wrapper mb-1">
          <i class="fa fa-user text-2xl"></i>
        </div>
        <span class="text-sm font-medium">个人信息</span>
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  activePage: {
    type: Number,
    default: 1
  }
});

const emit = defineEmits(['change-page']);

const handleNavClick = (pageNum) => {
  emit('change-page', pageNum);
};
</script>

<style scoped>
.bottom-nav {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background: white;
  z-index: 999;
  padding-bottom: env(safe-area-inset-bottom);
  border-top: 1px solid #f0f0f0;
}

.nav-item {
  cursor: pointer;
  transition: all 0.2s ease;
  padding: 6px 0;
  width: 80px;
  text-align: center;
}

/* 核心调整：图标容器宽度从30px加宽到36px，和文字更贴合 */
.icon-wrapper {
  width: 36px; /* 加宽后刚好比文字窄一点，视觉更协调 */
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.nav-active {
  color: #409eff;
  transform: scale(1.05);
}

.nav-inactive {
  color: #999;
}

.nav-item:hover {
  color: #409eff;
}

.text-2xl {
  font-size: 20px !important;
}

.text-sm {
  font-size: 14px !important;
}
</style>