<template>
    <div class="project-card group cursor-pointer overflow-hidden rounded-lg shadow-md transition-all duration-300 hover:shadow-xl">
      <!-- 项目图片（带悬停放大效果） -->
      <div class="relative overflow-hidden h-64">
        <img 
          :src="imageUrl" 
          alt="Project preview" 
          class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110"
        >
        <!-- 悬停时显示的背景遮罩 -->
        <div class="absolute inset-0 bg-rose-500/20 opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
      </div>
  
      <!-- 项目信息 -->
      <div class="p-6">
        <h3 class="text-xl font-medium text-gray-800 mb-2 group-hover:text-rose-500 transition-colors">
          {{ title }}
        </h3>
        <p class="text-gray-600 mb-4 line-clamp-2">
          {{ description }}
        </p>
        <div class="text-sm text-gray-400">
          {{ tags }}
        </div>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  // 定义组件属性
  defineProps<{
    title: string;
    description: string;
    imageUrl: string;
    tags: string;
  }>();
  </script>
  
  <style scoped>
  .project-card {
    background-color: #fff;
  }
  
  /* 图片加载过渡效果 */
  img {
    opacity: 0;
    animation: fadeIn 0.5s ease-in-out forwards;
  }
  
  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }
  </style>