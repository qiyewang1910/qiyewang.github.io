<template>
  <div class="app">
    <!-- 首页第一屏内容容器，通过flex布局实现垂直水平居中 -->
    <div class="homepage">
      <!-- 名字标题，通过v-for将文字拆分为单个字母span，便于后续动画操作 -->
      <h1 
        class="name" 
        ref="nameRef"
        @mouseenter= "handleMouseEnter" 
        @mouseleave= "handleMouseLeave" 
      >

        <!--遍历当前文字，每个字母生成一个span元素-->
        <span
          class="letter"
          v-for="(letter, index) in currentText"  
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

// 固定显示的文字，鼠标悬停时
const staticText = 'QIYE WANG';

//动态变化的文字列表，鼠标离开时
//设计思路：从单个字母逐个过渡到完整名字，营造动态感
const dynamicTexts =[
  'Q','QI','QIY','QIYE',  // 逐步显示"QIYE"
  'W','WA','WAN','WANG',  // 逐步显示"WANG"
  'Q WANG','QI WANG','QIY WANG',   // 逐步显示完整名字
  'QIYE W','QIYE WA','QIYE WAN','QIYE WANG',
];

//当前显示的文字（响应式变量）
const currentText = ref(dynamicTexts[0]);

//用于获取h1标题DOM元素的ref引用
const nameRef: Ref<HTMLElement | null> = ref(null);

// 用于存储每个字母span元素的ref数组
const letterRefs: Ref<(HTMLElement | null)[]> = ref([]);

// 控制是否处于悬停状态的响应式变量
let isHovered = ref(false);

// 存储动态切换文字的定时器ID
let animationInterval: number | null = null;

/** 鼠标进入事件处理函数， 功能：切换到固定文字显示清晰灰色效果 */

const handleMouseEnter = () => {
  //更新状态为悬停中
  isHovered.value =true;

  //清除动态切换定时器，停止文字变化
  if (animationInterval){
    clearInterval(animationInterval);
    animationInterval = null;
  }

  //使用GSAP实现淡出动画，为文字切换做准备
  gsap.to(letterRefs.value.filter(el => el), {
    opacity: 0,   //透明度变为0（淡出）
    duration: 0.3,  //动画持续0.3s
    onComplete: () => {  //淡出完成后执行
      //更新当前显示的文字为固定文字
      currentText.value = staticText;

      //等待DOM更新完成（确保新文字已渲染）
      nextTick(() => {
        //初始化新的字母数组长度
        letterRefs.value = new Array(currentText.value.length).fill(null);
        //为每个字母添加 清晰灰色 样式，移除 橙色模糊 样式
        letterRefs.value.forEach(letter => {
          if(letter) {
            letter.classList.remove('orange-blur');
            letter.classList.add('gray-sharp');
          }
        });

        //执行淡入动画，显示固定文字
        gsap.to(letterRefs.value.filter(el =>el),{
          opacity: 1,         //透明度变为1（淡入）
          duration: 0.3,      //动画持续0.3s
          ease: 'power2.out'  //缓动函数，使动画更自然
        });
      })
    }
  });
};

/** 鼠标离开事件处理函数，功能：恢复动态文字，显示橙色模糊效果 */
const handleMouseLeave = () => {
  //更新状态为非悬停
  isHovered.value = false;

  //执行淡出动画，为切换回动态文字做准备
  gsap.to(letterRefs.value.filter(el => el), {
    opacity: 0,
    duration: 0.3,
    onComplete:() => {
      //移除“清晰灰色”样式，添加“橙色模糊”样式
      letterRefs.value.forEach(letter => {
        if(letter) {
          letter.classList.remove('gray-sharp');
          letter.classList.add('orange-blur');
        }
      });

      //开始动态切换文字
      startDynamicAnimation();
    }
  });
};

/**
 * 生成下一个文字的索引（避免与当前索引相同）
 * @param currentIndex 当前显示文字的索引
 * @returns 下一个要显示的文字索引
 */
function getNextIndex(currentIndex: number){
  let nextIndex;
  //确保下一个索引与当前不同，避免连续显示相同的文字
  do {
    nextIndex = Math.floor(Math.random() * dynamicTexts.length);
  } while (nextIndex === currentIndex)
  return nextIndex;
}

/**
 * 启动动态文字切换动画
 */
function startDynamicAnimation(){
  let currentIndex = 0;

  //立即显示第一个动态文字
  currentText.value = dynamicTexts[currentIndex];
  nextTick(() => {
    // 初始化字母数组长度
    letterRefs.value = new Array(currentText.value.length).fill(null);
    //淡入显示第一个文字
    gsap.to(letterRefs.value.filter(el => el), {
      opacity: 1,
      duration : 0.3,
      ease: 'power2.out'
    });
  });

  //设定定时器，定时切换文字（每500ms一次）
  animationInterval = window.setInterval(() => {
    // 如果处于悬停状态，不执行切换
    if (isHovered.value) return;

    //获取下一个要显示的文字索引和内容
    const nextIndex = getNextIndex(currentIndex);
    const nextText = dynamicTexts[nextIndex];

    //淡出当前文字
    gsap.to(letterRefs.value.filter(el => el), {
      opacity: 0,
      duration: 0.3,
      onComplete: () => {
        //更新当前文字为下一个文字
        currentText.value = nextText;
        //等待DOM更新
        nextTick(() => {
          //淡入显示新文字
          gsap.to(letterRefs.value.filter(el => el), {
            opacity: 1,
            duration: 0.3,
            ease: 'power2.out'
          });
        });
      }
    });

    //更新当前索引
    currentIndex = nextIndex;
  }, 500);
}

// 组件挂载完成后执行
onMounted (() => {
  //等待DOM完全渲染后执行
  nextTick(() => {
    //初始化字母ref数组
    letterRefs.value = new Array(currentText.value.length).fill(null);

    // 为字母添加初始样式（橙色模糊）
    letterRefs.value.forEach(letter => {
      if (letter){
        letter.classList.add('orange-blur');
      }
    });

    //启动动态文字动画
    startDynamicAnimation();
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
  
  font-family: 'Jaldi', sans-serif; /* 使用Jaldi字体， fallback为无衬线字体 */
  font-size: 96px; /* 字体大小 */
  font-weight: 400; /* 字体粗细，正常粗细 */
  margin: 0 0 30px 0; /* 底部外边距，与简介区域分隔 */
  display: flex; /* 使用flex布局，让字母span横向排列 */
  gap: 4px; /* 字母之间的间距 */
  cursor: pointer; /* 鼠标悬停时显示手形光标 */
}

/* 单个字母样式，确保能被GSAP动画操作 */
.letter {
  display: inline-block; /* 行内块级元素，可设置宽高和定位 */
  position: relative; /* 相对定位，为绝对定位的动画做准备 */
  transition: all 0.3s ease; /* 所有属性变化都有过渡效果 */
}

/* 橙色模糊样式（鼠标离开时） */
.orange-blur {
  color:#FFA1A2;    /* 文字颜色为粉色 */
  filter: blur(4px);     /* 模糊效果（核心） */
  transition: filter 0.5s ease-in-out, color 0.5s ease-in-out;  /* 平滑过渡 */
}

/* 灰色清晰样式（鼠标悬停时） */
.gray-sharp{
  color: #848484;
  filter: blur(0);     /* 模糊效果（清晰显示） */
  transition: filter 0.5s ease-in-out, color 0.5s ease-in-out;  /* 平滑过渡 */
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

  .orange-blur{
    filter: blur(2px); /* 减弱模糊效果，提升小屏幕可读性 */
  }
}
</style>