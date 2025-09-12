<template>
  <div class="app">
    <!--引入导航栏-->
    <Navbar />

    <!--引入首页-->
    <Homepage />

    <!--引入项目页-->
    <ProjectsPage />

  </div>
</template>

<script setup lang="ts">
// 导入拆分后的组件
import Navbar from './components/Navbar.vue';
import Homepage from './components/HomePage.vue';
import ProjectsPage from './components/ProjectsPage.vue';
</script>



<style scoped>
/* 引入Jaldi字体，用于页面文字显示 */
@import url('https://fonts.googleapis.com/css2?family=Jaldi:wght@400;700&display=swap');

</style>