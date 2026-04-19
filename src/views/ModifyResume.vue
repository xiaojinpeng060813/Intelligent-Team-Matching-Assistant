<template>
  <!-- 核心：用isActive控制显示，和其他页面逻辑一致 -->
  <div class="modify-resume-page" v-show="isActive">
    <!-- 页面头部 -->
    <div class="page-header">
      <div class="back-icon" @click="handleBack">←</div>
      <div class="header-title">编辑简历</div>
    </div>

    <!-- 主体内容容器 -->
    <div class="content-container">
      <!-- 基本信息区域 -->
      <div class="section">
        <div class="section-title">基本信息</div>
        <div class="form-list">
          <div class="form-item">
            <label class="label-text">姓名</label>
            <input class="input-box" v-model="resumeInfo.name" placeholder="请输入姓名" />
          </div>
          <div class="form-item">
            <label class="label-text">专业</label>
            <input class="input-box" v-model="resumeInfo.major" placeholder="请输入专业" />
          </div>
          <div class="form-item">
            <label class="label-text">学院</label>
            <input class="input-box" v-model="resumeInfo.college" placeholder="请输入学院" />
          </div>
          <div class="form-item">
            <label class="label-text">年级</label>
            <input class="input-box" v-model="resumeInfo.grade" placeholder="请输入年级" />
          </div>
          <div class="form-item">
            <label class="label-text">学号</label>
            <input class="input-box" v-model="resumeInfo.studentId" placeholder="请输入学号" />
          </div>
        </div>
      </div>

      <!-- 成绩信息区域 -->
      <div class="section">
        <div class="section-title">成绩信息</div>
        <div class="form-list">
          <div class="form-item">
            <label class="label-text">GPA</label>
            <input class="input-box" v-model="resumeInfo.gpa" placeholder="请输入GPA" />
          </div>
          <div class="form-item">
            <label class="label-text">成绩排名</label>
            <input class="input-box" v-model="resumeInfo.scoreRank" placeholder="请输入成绩排名" />
          </div>
          <div class="form-item">
            <label class="label-text">综测排名</label>
            <input class="input-box" v-model="resumeInfo.comprehensiveRank" placeholder="请输入综测排名" />
          </div>
        </div>
      </div>

      <!-- 技能标签区域 -->
      <div class="section">
        <div class="section-title">技能标签</div>
        <div class="tag-container">
          <div class="tag-item" v-for="tag in tagList" :key="tag">{{ tag }}</div>
        </div>
        <div class="add-tag-row">
          <input class="tag-input" placeholder="添加新的技能标签" v-model="newTag" />
          <button class="add-btn" @click="addTag">添加</button>
        </div>
      </div>

      <!-- 获奖经历区域 -->
      <div class="section">
        <div class="section-title-row">
          <div class="section-title">获奖经历</div>
          <button class="add-award-btn" @click="addAward">+添加</button>
        </div>
        <!-- 获奖经历列表 -->
        <div class="award-item" v-for="(award, index) in resumeInfo.awards" :key="index">
          <input class="award-input" placeholder="获奖名称" v-model="award.name" />
          <input class="award-input" placeholder="获奖级别及等级" v-model="award.level" />
          <input class="award-input" placeholder="第几作者" v-model="award.author" />
          <input class="award-input" placeholder="获奖年份" v-model="award.year" />
        </div>
      </div>

      <!-- AI总结提示 -->
      <div class="ai-tip">
        <div class="tip-title">关于AI总结</div>
        <div class="tip-content">
          保存后，AI将根据您填写的信息自动生成个人总结。AI生成的内容不可手动修改，以确保真实性。
        </div>
      </div>

      <!-- 保存按钮 -->
      <button class="save-btn" @click="handleSave">保存</button>
    </div>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue';

// 接收App.vue传递的激活状态（必须保留，解决白屏核心）
const props = defineProps({
  isActive: {
    type: Boolean,
    default: false
  }
});

// 定义事件：通知App.vue切换页面（返回个人中心）
const emit = defineEmits(['change-page']);

// 简历初始化数据（和UI截图1:1匹配）
const resumeInfo = ref({
  name: '刘同学（可编辑）',
  major: '计算机科学与技术',
  college: '计算机科学与工程学院',
  grade: '大二',
  studentId: '2414020121',
  gpa: '3.92',
  scoreRank: '1/124',
  comprehensiveRank: '1/124',
  awards: [
    { name: '全国大学生数学建模大赛', level: '省级一等奖', author: '第二作者', year: '2025' },
    { name: '国家奖学金', level: '', author: '', year: '2025' },
    { name: '', level: '', author: '', year: '' }
  ]
});

// 技能标签列表
const tagList = ref(['Python', 'Java', 'MATLAB']);
// 新增标签输入框绑定
const newTag = ref('');

// 返回个人中心逻辑（和App.vue联动）
const handleBack = () => {
  emit('change-page', 3); // 切换回3号页面（个人中心）
};

// 添加技能标签
const addTag = () => {
  if (newTag.value.trim()) {
    tagList.value.push(newTag.value.trim());
    newTag.value = '';
  }
};

// 添加获奖经历
const addAward = () => {
  resumeInfo.value.awards.push({ name: '', level: '', author: '', year: '' });
};

// 保存简历逻辑
const handleSave = () => {
  console.log('保存的简历信息：', resumeInfo.value);
  alert('简历保存成功！');
};
</script>

<style scoped>
/* 页面整体样式（解决白屏+适配） */
.modify-resume-page {
  width: 100%;
  height: 100vh;
  box-sizing: border-box;
  background-color: #ffffff;
  overflow-y: auto;
  font-family: -apple-system, BlinkMacSystemFont, "PingFang SC", "Helvetica Neue", sans-serif;
}

/* 页面头部（1:1还原UI） */
.page-header {
  height: 44px;
  width: 100%;
  background-color: #ffffff;
  border-bottom: 1px solid #e5e5e5;
  display: flex;
  align-items: center;
  padding: 0 15px;
  box-sizing: border-box;
  position: sticky;
  top: 0;
  z-index: 10;
}

.back-icon {
  font-size: 18px;
  color: #000000;
  font-weight: 600;
  cursor: pointer;
  margin-right: 10px;
}

.header-title {
  font-size: 17px;
  color: #000000;
  font-weight: 600;
}

/* 主体内容容器 */
.content-container {
  padding: 15px;
  box-sizing: border-box;
}

/* 区域标题样式 */
.section {
  margin-bottom: 20px;
}

.section-title {
  font-size: 16px;
  color: #000000;
  font-weight: 600;
  margin-bottom: 10px;
  padding-bottom: 5px;
  border-bottom: 1px solid #e5e5e5;
}

.section-title-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  padding-bottom: 5px;
  border-bottom: 1px solid #e5e5e5;
}

/* 表单列表样式 */
.form-list {
  width: 100%;
}

.form-item {
  display: flex;
  align-items: center;
  margin-bottom: 12px;
}

.label-text {
  width: 80px;
  font-size: 15px;
  color: #333333;
  text-align: left;
}

.input-box {
  flex: 1;
  height: 35px;
  border: none;
  border-bottom: 1px solid #e5e5e5;
  font-size: 15px;
  color: #333333;
  padding: 0 5px;
  box-sizing: border-box;
  outline: none;
}

/* 技能标签区域 */
.tag-container {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 10px;
}

.tag-item {
  background-color: #e8f4f8;
  color: #1e88e5;
  padding: 5px 10px;
  border-radius: 15px;
  font-size: 14px;
}

.add-tag-row {
  display: flex;
  align-items: center;
  gap: 10px;
}

.tag-input {
  flex: 1;
  height: 35px;
  border: 1px solid #e5e5e5;
  border-radius: 5px;
  padding: 0 10px;
  font-size: 14px;
  outline: none;
  box-sizing: border-box;
}

.add-btn {
  background-color: #1e88e5;
  color: #ffffff;
  border: none;
  border-radius: 5px;
  padding: 8px 15px;
  font-size: 14px;
  cursor: pointer;
}

/* 获奖经历区域 */
.add-award-btn {
  font-size: 14px;
  color: #1e88e5;
  background: none;
  border: none;
  cursor: pointer;
}

.award-item {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 10px;
}

.award-input {
  flex: 1;
  min-width: 80px;
  height: 35px;
  border: none;
  border-bottom: 1px solid #e5e5e5;
  font-size: 14px;
  color: #333333;
  padding: 0 5px;
  outline: none;
  box-sizing: border-box;
}

/* AI总结提示 */
.ai-tip {
  background-color: #f5f5f5;
  padding: 10px 15px;
  border-radius: 5px;
  margin-bottom: 20px;
}

.tip-title {
  font-size: 14px;
  color: #000000;
  font-weight: 600;
  margin-bottom: 5px;
}

.tip-content {
  font-size: 13px;
  color: #666666;
  line-height: 1.5;
}

/* 保存按钮（1:1还原UI蓝色按钮） */
.save-btn {
  width: 100%;
  height: 45px;
  background-color: #1e88e5;
  color: #ffffff;
  border: none;
  border-radius: 5px;
  font-size: 17px;
  font-weight: 600;
  cursor: pointer;
}

.save-btn:active {
  background-color: #1976d2;
}
</style>
