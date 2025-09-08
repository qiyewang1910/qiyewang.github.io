<template>
  <div class = "app">
    <!-- 页面内容 HTML结构 -->

    <!-- 首页第一屏内容 -->
    <div class="homepage">
      <h1 class= "name">QIYE WANG</h1>
      <div class="intro">
        <p>I am a Media Informatics Student and a self-motivated designer.</p>
        <p>l love asking questions and exploring new topics.</p>
        <p>l would like to create efficient and intuitive experiences through my work.</p>
      </div>
    </div>

    <!-- 向下滚动指示器 -->
    <div class="animate-bounce">
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#FFA1A2" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="M19 14l-7 7-7-7"/>
      </svg>
    </div>
  </div>
</template>


<script setup lang="ts">
// 暂时不引用其他组件。 页面逻辑（typscript）
// 交互逻辑（当前简单需求暂时用不到，留空即可）
// 后续如果要加功能（如点击事件、加载数据），再在这里写
</script>


<style scoped>
/* 3. <style> 部分：调格式（对应 CSS 的角色，scoped 表示样式只作用于当前组件） */
/* 先引入 Jaldi 字体（通过 Google Fonts，确保字体生效） */
@import url('https://fonts.googleapis.com/css2?family=Jaldi:wght@400;700&display=swap');

/* 容器：让内容居中显示（占满整个屏幕高度） */
  .homepage{
    min-height: 100vh;  /* 让容器高度等于屏幕高度，内容居中垂直*/
    display: flex;
    flex-direction: column;  /* 内容垂直排列（标题在上，简介在下） */
    align-items: center;   /* 水平居中 */
    justify-content: center; /* 垂直居中 */
    padding: 0 20px; /* 左右留一点边距，避免手机端内容贴边 */
    background-color: #FFFFFF; /* 背景白色 */
  }

  /* QIYE WANG */
  .name{
    color: #FFA1A2; /* 文字颜色：粉 */
    font-family: 'Jaldi', sans-serif;  /* 字体Jaldi （如果加载失败，用默认无衬线字体） */
    font-size: 96px;
    font-style: normal;    /* 字体样式：正常（非斜体） */
    font-weight: 400;     /* 字重：正常（400是默认正常字重） */
    line-height: normal;   /* 行高：正常 */
    width: 437px;   /* 宽度427 */
    height: 110px;   /* 高度110px */
    margin: 0 0 30px 0;   /* 底部留30px 间距，和间接分开 */
    text-align: center;   /* 文字居中（避免宽度固定后文字偏左）*/
  }

  /* 简介文字样式（补充适配，让整体协调） */
  .intro {
    color: #848484;      /* 文字颜色：灰色 */
    font-size: 18px;      /* 字体大小18px */
    font-family: 'Jaldi', sans-serif;  /* 字体Jaldi （如果加载失败，用默认无衬线字体） */
    max-width: 600px;    /* 最大宽度：避免文字太长，换行更美观 */
    line-height: 1.6;    /* 行高1.6 阅读更舒适 */
    text-align: center;   /* 文字居中 */
  }

  /* 向下滚动指示器样式（简单动画，提示用户可滚动） */
  .animate-bounce{
    position: absolute;  /* 固定在屏幕底部 */
    bottom: 40px;  /* 距离底部40 */
    left: 50%;     /* 左侧对齐容器的50%位置 */
    transform: translateX(-50%);   /* 向左移动自身宽度的50%，实现完全居中 */
    animation: bounce 2s infinite; /* 弹跳动画，持续2秒，无限循环 */
  }

  @keyframes bounce {
    0%, 100%{
      transform: translateY(0); /* 初始和结束位置：不移动 */
    }
    50% {
      transform: translateY(10px); /* 中间位置：向下移动10px */
    }
  }

  /* 响应式适配： 手机端调整标题大小（避免96px在手机上太大） */
  @media (max-width: 768px) {
    .name {
      font-size: 64px; /* 手机端标题缩小到64px */
      width: auto; /* 宽度自动，避免手机端超出屏幕 */
      height: auto; /* 高度自动 */
    }

    .intro{
      font-size: 16px; /* 手机端简介文字缩小到16px */
    }
  }
</style>
