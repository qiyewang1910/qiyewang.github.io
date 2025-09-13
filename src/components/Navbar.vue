<template>
    <nav 
      class="fixed top-0 left-0 w-full z-50 transition-all duration-300"
      :class="{ 'py-3 bg-white/90 backdrop-blur-sm shadow-sm': isScrolled, 'py-6 bg-transparent': !isScrolled }"
    >
      <div class="container mx-auto px-6 flex justify-between items-center">
        <a href="#home" class="text-2xl font-bold text-gray-800 hover:text-rose-500 transition-colors">
          QIYE
        </a>
  
        <div class="hidden md:flex space-x-8">
          <a 
            href="#home" 
            class="text-gray-600 hover:text-rose-500 transition-colors"
            :class="{ 'text-rose-500': activeSection === 'home' }"
          >
            home
          </a>
          <a 
            href="#project" 
            class="text-gray-600 hover:text-rose-500 transition-colors"
            :class="{ 'text-rose-500': activeSection === 'project' }"
          >
            projects
          </a>
          <a href="#about" class="text-gray-600 hover:text-rose-500 transition-colors">about</a>
          <a href="#contact" class="text-gray-600 hover:text-rose-500 transition-colors">contact</a>
        </div>
      </div>
    </nav>
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted, onUnmounted } from 'vue';
  
  // 滚动状态管理
  const isScrolled = ref(false);
  const activeSection = ref('home');
  
  // 监听滚动事件
  const handleScroll = () => {
    // 导航栏样式变化
    isScrolled.value = window.scrollY > 50;
  
    // 监听当前活跃区域（基于滚动位置）
    const sections = ['home', 'project', 'about', 'contact'];
    const currentPosition = window.scrollY + 100;
  
    for (const section of sections) {
      const element = document.getElementById(section);
      if (element) {
        const { offsetTop, offsetHeight } = element;
        if (currentPosition >= offsetTop && currentPosition < offsetTop + offsetHeight) {
          activeSection.value = section;
          break;
        }
      }
    }
  };
  
  // 平滑滚动到锚点
  document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function(e) {
      e.preventDefault();
      const targetId = this.getAttribute('href')?.substring(1);
      if (targetId) {
        const targetElement = document.getElementById(targetId);
        targetElement?.scrollIntoView({ behavior: 'smooth' });
      }
    });
  });
  
  onMounted(() => {
    window.addEventListener('scroll', handleScroll);
  });
  
  onUnmounted(() => {
    window.removeEventListener('scroll', handleScroll);
  });
  </script>