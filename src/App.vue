<template>
  <div class="app">
    <!-- 首页第一屏内容容器，通过flex布局实现垂直水平居中 -->
    <div class="homepage">
      <!-- 名字标题，通过v-for将文字拆分为单个字母span，便于后续动画操作 -->
      <h1 class="name" ref="nameRef">
        <span
          class="letter"
          v-for="(letter, index) in text"
          :key="index"
          :ref="(el) => letterRefs[index] = el"
        >
          {{ letter }}
        </span>
      </h1>

      <!-- 个人简介文本区域 -->
      <div class="intro">
        <p>I am a Media Informatics Student and a self-motivated designer.</p>
        <p>I love asking questions and exploring new topics.</p>
        <p>I would like to create efficient and intuitive experiences through my work.</p>
      </div>
    </div>

    <!-- 向下滚动指示器，带有弹跳动画 -->
    <div class="animate-bounce">
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#FFA1A2" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="M19 14l-7 7-7-7"/>
      </svg>
    </div>
  </div>
</template>

<script setup lang="ts">
// 从vue中引入响应式相关的ref、生命周期钩子onMounted、nextTick等
import { ref, onMounted, Ref, nextTick } from 'vue';
// 从gsap中引入动画核心方法
import { gsap } from 'gsap';

// 定义要显示的名字文本
const text = 'QIYE WANG';
// 用于获取h1标题DOM元素的ref
const nameRef: Ref<HTMLElement | null> = ref(null);
// 用于存储每个字母span DOM元素的ref数组
const letterRefs: Ref<(HTMLElement | null)[]> = ref([]);

onMounted(() => {
  // 确保DOM完全渲染后再执行后续操作，避免获取不到元素
  nextTick(() => {
    // 初始化letterRefs数组长度，与text长度一致
    letterRefs.value = new Array(text.length).fill(null);
    
    // 调试日志：在浏览器控制台打印字母数量，用于验证
    console.log('字母数量:', text.length);
    // 打印获取到的有效字母元素数量，用于验证
    console.log('获取到的字母元素:', letterRefs.value.filter(el => el));
    // 打印标题元素是否成功获取，用于验证
    console.log('标题元素是否存在:', !!nameRef.value);

    // 为标题元素添加鼠标进入事件监听器，触发字母散开动画
    nameRef.value?.addEventListener('mouseenter', () => {
      // 遍历每个字母元素
      letterRefs.value.forEach((letter, index) => {
        if (letter) {
          // 使用GSAP的to方法，为字母添加随机偏移、缩放等动画效果
          gsap.to(letter, {
            x: Math.random() * 80 - 40, // 随机X方向偏移，范围-40到40
            y: Math.random() * 80 - 40, // 随机Y方向偏移，范围-40到40
            scale: 1.15, // 轻微放大1.15倍
            duration: 0.6, // 动画持续时间0.6秒
            delay: index * 0.05, // 每个字母按顺序延迟，营造逐个动画的效果
            ease: 'power2.out' // 动画缓动曲线，power2.out表示先快后慢
          });
        }
      });
    });

    // 为标题元素添加鼠标离开事件监听器，触发字母恢复动画
    nameRef.value?.addEventListener('mouseleave', () => {
      // 遍历每个字母元素
      letterRefs.value.forEach((letter, index) => {
        if (letter) {
          // 使用GSAP的to方法，让字母恢复到原始位置和大小
          gsap.to(letter, {
            x: 0, // X方向恢复到0
            y: 0, // Y方向恢复到0
            scale: 1, // 缩放恢复到1倍
            duration: 0.3, // 动画持续时间0.5秒
            delay: index * 0.01, // 每个字母按顺序延迟恢复
            ease: 'power2.in' // 动画缓动曲线，power2.in表示先慢后快
          });
        }
      });
    });
  });
});
</script>

<style scoped>
/* 引入Jaldi字体，用于页面文字显示 */
@import url('https://fonts.googleapis.com/css2?family=Jaldi:wght@400;700&display=swap');

/* 首页内容容器样式，实现全屏且内容居中 */
.homepage {
  min-height: 100vh; /* 容器最小高度为视口高度，占满屏幕 */
  display: flex; /* 使用flex布局 */
  flex-direction: column; /* 子元素垂直排列 */
  align-items: center; /* 水平居中 */
  justify-content: center; /* 垂直居中 */
  padding: 0 20px; /* 左右内边距，避免内容贴边 */
  background-color: #FFFFFF; /* 背景色为白色 */
  position: relative; /* 为绝对定位的滚动指示器提供参考 */
  margin: 0; /* 移除默认外边距 */
}

/* 名字标题样式 */
.name {
  color: #FFA1A2; /* 文字颜色为粉色 */
  font-family: 'Jaldi', sans-serif; /* 使用Jaldi字体， fallback为无衬线字体 */
  font-size: 96px; /* 字体大小 */
  font-weight: 400; /* 字体粗细，正常粗细 */
  margin: 0 0 30px 0; /* 底部外边距，与简介区域分隔 */
  display: flex; /* 使用flex布局，让字母span横向排列 */
  gap: 4px; /* 字母之间的间距 */
}

/* 单个字母样式，确保能被GSAP动画操作 */
.letter {
  display: inline-block; /* 行内块级元素，可设置宽高和定位 */
  text-shadow: 0 0 5px rgba(255, 161, 162, 0.3); /* 文字阴影，增加层次感 */
  position: relative; /* 相对定位，为绝对定位的动画做准备 */
}

/* 简介文本样式 */
.intro {
  color: #848484; /* 文字颜色为灰色 */
  font-size: 18px; /* 字体大小 */
  font-family: 'Jaldi', sans-serif; /* 使用Jaldi字体 */
  max-width: 600px; /* 最大宽度，避免文字过长 */
  line-height: 1.6; /* 行高，提升可读性 */
  text-align: center; /* 文字居中 */
  margin: 0; /* 移除默认外边距 */
}

/* 向下滚动指示器样式，带有弹跳动画 */
.animate-bounce{
  position: absolute; /* 绝对定位，固定在屏幕底部 */
  bottom: 40px; /* 距离底部的距离 */
  left: 50%; /* 水平方向居中的第一步，左移50% */
  transform: translateX(-50%); /* 水平方向居中的第二步，左移自身50%宽度 */
  animation: bounce 2s infinite; /* 应用bounce动画，持续2秒，无限循环 */
}

/* 定义弹跳动画关键帧 */
@keyframes bounce {
  0%, 100%{
    /* 初始和结束状态，水平居中，垂直不偏移 */
    transform: translateX(-50%) translateY(0);
  }
  50% {
    /* 中间状态，水平居中，垂直向下偏移10px */
    transform: translateX(-50%) translateY(10px);
  }
}

/* 响应式适配，手机端调整文字大小 */
@media (max-width: 768px) {
  .name {
    font-size: 64px; /* 手机端标题字体缩小 */
  }

  .intro{
    font-size: 16px; /* 手机端简介字体缩小 */
  }
}
</style>