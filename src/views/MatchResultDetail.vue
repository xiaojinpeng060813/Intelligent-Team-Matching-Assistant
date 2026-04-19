<template>
  <!-- ✅ 新增：全屏固定定位，覆盖整个屏幕，高z-index，绝对不会和其他页面叠加 -->
  <div class="match-result-detail-page" style="position: fixed; top: 0; left: 0; z-index: 9999;">
    <!-- 详情页头部（带返回按钮） -->
    <div class="detail-header">
      <div class="back-icon" @click="goBack">←</div>
      <div class="header-content">
        <span class="header-title">智能匹配</span>
        <span class="header-subtitle">基于AI算法，为您推荐最适合的队友</span>
      </div>
    </div>

    <!-- 匹配结果列表（1:1复刻截图） -->
    <div class="match-result-list">
      <div class="match-card" v-for="(item, index) in matchList" :key="index">
        <div class="student-header">
          <div class="avatar">
            <span class="avatar-text">{{ item.name.charAt(0) }}</span>
          </div>
          <div class="student-info">
            <div class="student-name">{{ item.name }}</div>
            <div class="student-desc">{{ item.major }} | {{ item.major }}学院 | {{ item.grade }}</div>
          </div>
        </div>

        <div class="skill-tags">
          <span class="tag" v-for="skill in item.skills" :key="skill">{{ skill }}</span>
        </div>

        <div class="awards-section">
          <div class="section-title">获奖成果</div>
          <div class="award-item" v-for="award in item.awards" :key="award">
            <i class="award-icon">🏆</i>
            <span class="award-text">{{ award }}</span>
          </div>
        </div>

        <div class="reason-section">
          <div class="section-title reason-title">
            <i class="reason-icon">🔍</i>
            AI推荐理由
          </div>
          <div class="reason-text">{{ item.reason }}</div>
        </div>

        <!-- 点击打开二维码弹窗 -->
        <button class="contact-btn" @click="openQrCode(item)">联系</button>
      </div>
    </div>

    <!-- ✅ 新增：二维码弹窗（蒙层 + 弹窗内容） -->
    <div class="qr-modal" v-if="showQrModal" @click="closeQrCode">
      <div class="qr-modal-content" @click.stop>
        <div class="qr-title">扫码添加 {{ currentStudent.name }} 企业微信</div>
        <img class="qr-image" src="https://picsum.photos/300/300" alt="微信二维码">
        <div class="qr-tip">企业微信扫码添加</div>
        <button class="qr-close-btn" @click="closeQrCode">关闭</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const emit = defineEmits(['close-detail']);
const goBack = () => {
  emit('close-detail');
};

// 假数据（匹配截图内容，完全保留）
const matchList = ref([
  {
    name: "刘同学",
    major: "计算机科学与技术",
    grade: "大二",
    skills: ["Python", "C语言", "C++", "数据分析", "JavaScript"],
    awards: [
      "全国大学生数学竞赛国家级二等奖",
      "全国大学生数学建模大赛省级一等奖",
      "湖南省大学生程序设计大赛省级二等奖"
    ],
    reason: "他熟练掌握多种编程语言与数据分析技能，在全国大学生数学竞赛、数学建模竞赛、ACM-ICPC等高水平赛事中多次斩获国家级、省部级奖项，兼具出色的学习能力与实践竞赛能力。"
  },
  {
    name: "刘同学",
    major: "计算机科学与技术",
    grade: "大二",
    skills: ["Python", "C++", "数据分析", "JavaScript"],
    awards: [
      "全国大学生数学竞赛国家级二等奖",
      "全国大学生数学建模大赛省级一等奖",
      "湖南省大学生程序设计大赛省级二等奖"
    ],
    reason: "他熟练掌握多种编程语言与数据分析技能，在全国大学生数学竞赛、数学建模竞赛、ACM-ICPC等高水平赛事中多次斩获国家级、省部级奖项，兼具出色的学习能力与实践竞赛能力。"
  }
]);

// ✅ 新增：二维码弹窗相关数据
const showQrModal = ref(false);
const currentStudent = ref({ name: '' });

// 打开二维码弹窗
const openQrCode = (item) => {
  currentStudent.value = item;
  showQrModal.value = true;
};

// 关闭二维码弹窗
const closeQrCode = () => {
  showQrModal.value = false;
};
</script>

<style scoped>
/* 恢复全局默认字体，仅AI推荐理由区域使用阿里巴巴普惠体 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "PingFang SC", "Microsoft YaHei", sans-serif; /* 还原全局默认字体 */
}

.match-result-detail-page {
  width: 100%;
  height: 100vh;
  overflow-x: hidden;
  overflow-y: auto; /* ✅ 新增：详情页内容过长时可以滚动 */
  background-color: #F5F7FA; /* ✅ 新增：统一背景色，避免透底 */
}

.detail-header {
  height: 72px;
  width: 100%;
  background-color: #1E88E5;
  padding: 0 16px;
  display: flex;
  align-items: center;
  color: #FFFFFF;
}

.back-icon {
  font-size: 28px; /* 原24px → 提升4px */
  font-weight: 700;
  cursor: pointer;
  margin-right: 12px;
}

.header-content {
  flex: 1;
}

.header-title {
  font-size: 26px; /* 原22px → 提升4px */
  font-weight: 700;
  display: block;
  margin-bottom: 4px;
}

.header-subtitle {
  font-size: 16px; /* 原12px → 提升4px */
  opacity: 0.9;
  display: block;
}

.match-result-list {
  padding: 16px;
  min-height: calc(100vh - 72px);
}

.match-card {
  background-color: #FFFFFF;
  border-radius: 12px;
  padding: 20px;
  margin-bottom: 16px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
}

.student-header {
  display: flex;
  align-items: center;
  margin-bottom: 16px;
}

.avatar {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background-color: #1E88E5;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 12px;
}

.avatar-text {
  color: #FFFFFF;
  font-size: 24px; /* 原20px → 提升4px */
  font-weight: 600;
}

.student-name {
  font-size: 22px; /* 原18px → 提升4px */
  font-weight: 600;
  color: #333333;
  margin-bottom: 4px;
}

.student-desc {
  font-size: 16px; /* 原12px → 提升4px */
  color: #666666;
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 16px;
}

.tag {
  background-color: #E8F3FF;
  color: #1E88E5;
  font-size: 16px; /* 原12px → 提升4px */
  padding: 6px 14px; /* 微调内边距适配字号 */
  border-radius: 16px;
}

.awards-section {
  margin-bottom: 16px;
}

.section-title {
  font-size: 18px; /* 原14px → 提升4px */
  font-weight: 600;
  color: #333333;
  margin-bottom: 8px;
}

/* ✅ 仅AI推荐理由标题使用阿里巴巴普惠体 + 亮蓝色 */
.reason-title {
  color: #0088FF !important; /* 亮蓝色 */
  font-family: "Alibaba PuHuiTi", sans-serif !important; /* 仅此处用普惠体 */
}

.award-item {
  display: flex;
  align-items: center;
  margin-bottom: 4px;
  font-size: 17px; /* 原13px → 提升4px */
  color: #666666;
}

.award-icon {
  margin-right: 8px;
  font-size: 18px; /* 原14px → 提升4px */
}

.reason-section {
  margin-bottom: 20px;
}

.reason-icon {
  margin-right: 6px;
}

/* ✅ 仅AI推荐理由正文：亮蓝色 + 阿里巴巴普惠体 + 首行缩进2字符 */
.reason-text {
  font-size: 17px; /* 原13px → 提升4px */
  color: #0088FF !important; /* 亮蓝色 */
  line-height: 1.6; /* 微调行高提升可读性 */
  text-align: justify;
  font-family: "Alibaba PuHuiTi", sans-serif !important; /* 仅此处用普惠体 */
  text-indent: 2em; /* 首行缩进2字符（em单位适配字体大小） */
}

.contact-btn {
  width: 100%;
  height: 48px; /* 微调高度适配字号 */
  background-color: #1E88E5;
  color: #FFFFFF;
  border: none;
  border-radius: 8px;
  font-size: 20px; /* 原16px → 提升4px */
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.contact-btn:active {
  background-color: #1976D2;
}

/* 网页端适配 */
@media (min-width: 768px) {
  .match-result-list {
    max-width: 600px;
    margin: 0 auto;
  }
  .match-card {
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  }
}

/* ===================== ✅ 修复：二维码完美居中 ===================== */
.qr-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10000;
}

.qr-modal-content {
  background: #fff;
  width: 320px;
  padding: 30px 20px;
  border-radius: 16px;
  text-align: center;
  box-shadow: 0 4px 20px rgba(0,0,0,0.2);
  display: flex;
  flex-direction: column;
  align-items: center; /* 核心：水平居中 */
}

.qr-title {
  font-size: 18px;
  font-weight: 600;
  color: #333;
  margin-bottom: 20px;
  text-align: center;
}

.qr-image {
  width: 260px;
  height: 260px;
  object-fit: cover;
  border-radius: 8px;
  margin-bottom: 16px;
  display: block;
}

.qr-tip {
  font-size: 14px;
  color: #666;
  margin-bottom: 20px;
  text-align: center;
}

.qr-close-btn {
  width: 100%;
  height: 44px;
  background: #1E88E5;
  color: #fff;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  cursor: pointer;
}
</style>
