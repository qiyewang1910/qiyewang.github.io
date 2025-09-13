<template>
    <section id="projects" class="min-h-screen bg-light py-20">
      <!-- 页面标题 -->
      <div class="section-title mb-16">
        <h2 class="text-4xl font-light tracking-wider text-gray-800 text-center">
          selected work
        </h2>
        <div class="w-24 h-1 bg-rose-400 mx-auto mt-4"></div>
      </div>
  
      <!-- 项目卡片容器 -->
      <div class="project-container max-w-6xl mx-auto px-6 grid grid-cols-1 md:grid-cols-2 gap-12">
        <!-- 项目1（占位方框） -->
        <div class="project-card group cursor-pointer overflow-hidden rounded-lg shadow-md transition-all duration-300 hover:shadow-xl">
          <div class="bg-gray-200 h-64 animate-pulse"></div>
          <div class="p-6">
            <div class="h-6 bg-gray-200 rounded w-1/3 mb-4 animate-pulse"></div>
            <div class="h-4 bg-gray-200 rounded mb-2 w-full animate-pulse"></div>
            <div class="h-4 bg-gray-200 rounded w-2/3 animate-pulse"></div>
            <div class="h-4 bg-gray-200 rounded mt-4 w-1/2 animate-pulse"></div>
          </div>
        </div>
  
        <!-- 项目2（占位方框） -->
        <div class="project-card group cursor-pointer overflow-hidden rounded-lg shadow-md transition-all duration-300 hover:shadow-xl">
          <div class="bg-gray-200 h-64 animate-pulse"></div>
          <div class="p-6">
            <div class="h-6 bg-gray-200 rounded w-1/3 mb-4 animate-pulse"></div>
            <div class="h-4 bg-gray-200 rounded mb-2 w-full animate-pulse"></div>
            <div class="h-4 bg-gray-200 rounded w-2/3 animate-pulse"></div>
            <div class="h-4 bg-gray-200 rounded mt-4 w-1/2 animate-pulse"></div>
          </div>
        </div>
  
        <!-- 项目3（占位方框） -->
        <div class="project-card group cursor-pointer overflow-hidden rounded-lg shadow-md transition-all duration-300 hover:shadow-xl">
          <div class="bg-gray-200 h-64 animate-pulse"></div>
          <div class="p-6">
            <div class="h-6 bg-gray-200 rounded w-1/3 mb-4 animate-pulse"></div>
            <div class="h-4 bg-gray-200 rounded mb-2 w-full animate-pulse"></div>
            <div class="h-4 bg-gray-200 rounded w-2/3 animate-pulse"></div>
            <div class="h-4 bg-gray-200 rounded mt-4 w-1/2 animate-pulse"></div>
          </div>
        </div>
  
        <!-- 项目4（占位方框） -->
        <div class="project-card group cursor-pointer overflow-hidden rounded-lg shadow-md transition-all duration-300 hover:shadow-xl">
          <div class="bg-gray-200 h-64 animate-pulse"></div>
          <div class="p-6">
            <div class="h-6 bg-gray-200 rounded w-1/3 mb-4 animate-pulse"></div>
            <div class="h-4 bg-gray-200 rounded mb-2 w-full animate-pulse"></div>
            <div class="h-4 bg-gray-200 rounded w-2/3 animate-pulse"></div>
            <div class="h-4 bg-gray-200 rounded mt-4 w-1/2 animate-pulse"></div>
          </div>
        </div>
      </div>
    </section>
  </template>
  
  <script setup lang="ts">
  // 后续可在此处导入ProjectCard组件
  // import ProjectCard from './ProjectCard.vue';
  </script>
  
  <style scoped>
  /* 引入Jaldi字体保持风格统一 */
  @import url('https://fonts.googleapis.com/css2?family=Jaldi:wght@400;700&display=swap');
  
  .section-title {
    margin-top: 80px; /* 适配固定导航栏高度 */
    font-family: 'Jaldi', sans-serif;
  }
  
  .project-container {
    padding-bottom: 100px;
  }
  
  /* 占位卡片动画效果 */
  .animate-pulse {
    animation: pulse 1.5s cubic-bezier(0.4, 0, 0.6, 1) infinite;
  }
  
  @keyframes pulse {
    0%, 100% {
      opacity: 1;
    }
    50% {
      opacity: 0.5;
    }
  }
  
  /* 响应式调整 */
  @media (max-width: 768px) {
    .section-title h2 {
      font-size: 2.5rem;
    }
    
    .project-container {
      gap: 8px;
    }
  }
  </style>