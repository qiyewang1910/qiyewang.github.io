<template>
  <div class = "app">

    <!-- 页面内容 HTML结构 -->

    <!--顶部导航-->
    <header class="header">
      <h1>我的个人主页</h1>
      <nav>
        <a href= "#about">关于我</a>
        <a href= "#projects">项目</a>
        <a href= "#contact">联系</a>
      </nav>
    </header>

    <!--主题内容-->
    <main class ="main">
      <section id="about"> 
        <h2> 关于我 </h2>
        <p>I am a Media Informatics Student and a self-motivated designer.</p>
        <p>l love asking questions and exploring new topics.</p>
        <p>l would like to create efficient and intuitive experiences through my work.</p>
      </section>

      <section class="projects">
        <h2> 我的项目 </h2>
        <ul>
          <li> <a href="#"> 项目 A </a> 一个有趣的前端作品 </li>
          <li> <a href="#"> 项目 B </a> 练习Vue3的Demo </li>
        </ul>
      </section> 

      <section class="contact">
        <h2> 联系我 </h2>
          <p>LinkedIn： </p>
          <p>GitHub： </p>
          <p>Email： </p>
      </section> 

    </main>

    <footer class="footer">
      <p>designed & coded by Qiye WANG © 2025</p>
    </footer>

  </div>  
</template>


<script setup lang="ts">
//暂时不引用其他组件。 页面逻辑（typscript）
</script>


<style scoped>
/* 全局布置   页面样式（CSS） */
body {
  margin: 0;
  font-family: system-ui, Arial, sans-serif;
  line-height: 1.6;
  background: #fafafa;
  color: #333;
}
/* 顶部导航 */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #333;
  color: white;
  padding: 1rem 2rem;
  flex-wrap: wrap;
}

.logo {
  marigin: 0;
}

.nav {
  display: flex;
  gap: 1rem;
}

.nav a {
  color: white;
  text-decoration: none;
  font-weight: bold;
}

.nav a:hover {
  text-decoration: underline;
}

/* 主体内容 */
.main {
  padding: 2rem;
}

section {
  margin-bottom: 3rem;
}

/* 卡片布局 */
.projects{
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
}

.card {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.card h3 {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.card h3{
  margin-top: 0;
}

/* 页脚 */
.footer {
  background: #f1f1f1;
  text-align: center;
  padding: 1rem; 
}

/* 响应式 小屏幕 */
@media (max-width: 600px) {
  .header {
    flex-direction: column;
    text-align: center;
  }

  .nav {
    margin-top: 0.5rem;
    flex-wrap: wrap;
    justify-content: center;
  }
}

</style>
