<template>
    <nav class="fixed top-0  
                left-0 
                w-full 
                z-50 
                py-6 
                transition-all 
                duration-300">
                <!-- fixed 固定定位：导航栏会固定在浏览器视口顶部，滚动页面时不会消失-->
                <!-- top-0 left-0	定位到视口的左上角（top: 0; left: 0;）-->
                <!--w-full	宽度 100%（width: 100%;），让导航栏撑满整个页面宽度-->
                <!-- z-50	层级为 50（z-index: 50;），确保导航栏在其他元素上方（不被遮挡）-->
                <!-- py-6	上下内边距为 1.5rem（padding-top: 1.5rem; padding-bottom: 1.5rem;）-->
                <!--transition-all	开启所有 CSS 属性的过渡动画（如背景色、内边距变化时会平滑过渡）-->
                <!--duration-300	过渡动画时长为 300 毫秒，让样式变化更丝滑-->


        <div class="container mx-auto px-6 flex justify-between items-center">
            <a hef="#home" class="text-2xl font-bold text-dark hover:text-primary transition-colors">
                QIYE 
            </a>

            <div class="hidden md:flex space-x-8">
                <a href="#projects" class="text-secondary hover:text-primary transition-colors">project</a>
                <a href="#projects" class="text-secondary hover:text-primary transition-colors">about</a>
                <a href="#projects" class="text-secondary hover:text-primary transition-colors">resume</a>
                <a href="#projects" class="text-secondary hover:text-primary transition-colors">contacr</a>
            </div>
        </div>
    </nav>
</template>

<style>
/* 导航栏样式 */
</style>