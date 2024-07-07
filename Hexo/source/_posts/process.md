---
title: 博客搭建过程
categories: 记录
description: 持续更新Hexo博客搭建全过程
---
## 搭建记录
这篇文章的内容为本站的搭建过程，省略一些修改图片路径等简易操作
### 1.初始化Hexo项目
在新的文件夹中打开终端，输入以下
``` shell
hexo init
```
### 2.安装初始依赖库
接着输入
``` shell
npm i
```
通过这个使博客内容可以正常显示
### 3.将博客挂载到github pages
随后安装hexo-deployer-git使博客能够上传到github
```shell
npm install hexo-deployer-git --save
```
（在此之后，在_config.yml中修改deploy内容，这里省略）
### 4.安装butterfly主题
```shell
npm i hexo-theme-butterfly
```
随后安装渲染器
```shell
npm install hexo-renderer-pug hexo-renderer-stylus --save
```
在此之后将_config.yml中的theme改为butterfly
并且将language改为zh-CN
### 5.文章显示
修改主题配置文件_config.butterfly.yml中的post_meta
date_type均改为both
date_format均改为relative
### 6.本地搜索
安装以下依赖
```shell
npm install hexo-generator-search --save
```
_config.yml中加入
```shell
search:
  path: search.xml
  field: post
  content: true
```
_config.butterfly.yml中local_search的enable改为true
### 7.字数统计
安装以下依赖
```shell
npm install hexo-wordcount --save
```
_config.butterfly.yml中wordcount的enable改为true
### 8.鼠标点击效果
_config.butterfly.yml中fireworks或者Heart symbol或者words的enable改为true
### 9.修改为一图流
首先在source文件夹内新建css文件夹，并新建custom.css写入以下代码
```shell
/* 页脚与头图透明 */
#footer {
  background: transparent !important;
}
#page-header {
  background: transparent !important;
}

/* 白天模式遮罩透明 */
#footer::before {
  background: transparent !important;
}
#page-header::before {
  background: transparent !important;
}

/* 夜间模式遮罩透明 */
[data-theme="dark"] #footer::before {
  background: transparent !important;
}
[data-theme="dark"] #page-header::before {
  background: transparent !important;
}
```
随后在_config.butterfly.yml文件中的inject配置项的head子项加入以下代码
```shell
inject:
  head:
    - <link rel="stylesheet" href="/css/custom.css" media="defer" onload="this.media='all'">
```
### 10.页脚徽标
安装以下依赖
```shell
npm install hexo-butterfly-footer-beautify --save
```
在站点配置文件_config.yml或者主题配置文件_config.butterfly.yml中添加（这是我的配置）
```shell
# footer_beautify
# 页脚计时器：[Native JS Timer](https://akilar.top/posts/b941af/)
# 页脚徽标：[Add Github Badge](https://akilar.top/posts/e87ad7f8/)
footer_beautify:
  enable:
    timer: true # 计时器开关
    bdage: true # 徽标开关
  priority: 5 #过滤器优先权
  enable_page: all # 应用页面
  exclude: #屏蔽页面
    # - /posts/
    # - /about/
  layout: # 挂载容器类型
    type: id
    name: footer-wrap
    index: 0
  # 计时器部分配置项
  runtime_js: /js/runtime.js
  runtime_css: /css/runtime.css
  # 徽标部分配置项
  swiperpara: 0 #若非0，则开启轮播功能，每行徽标个数
  bdageitem:
    - link: https://hexo.io/ #徽标指向网站链接
      shields: https://img.shields.io/badge/Frame-Hexo-blue?style=flat&logo=hexo #徽标API
      message: 博客框架为Hexo #徽标提示语
    - link: https://butterfly.js.org/
      shields: https://img.shields.io/badge/Theme-Butterfly-6513df?style=flat&logo=bitdefender
      message: 本站主题为Butterfly
    - link: https://vercel.com/
      shields: https://img.shields.io/badge/Hosted-Vercel-brightgreen?style=flat&logo=Vercel
      message: 本站采用Vercel部署
    - link: https://github.com/
      shields: https://img.shields.io/badge/Source-Github-d021d6?style=flat&logo=GitHub
      message: 本站项目由Github托管
  swiper_css: https://npm.elemecdn.com/hexo-butterfly-swiper/lib/swiper.min.css
  swiper_js: https://npm.elemecdn.com/hexo-butterfly-swiper/lib/swiper.min.js
  swiperbdage_init_js: https://npm.elemecdn.com/hexo-butterfly-footer-beautify/lib/swiperbdage_init.min.js
```
其中我的css配置为
```shell
/*电子钟字体*/
@font-face {
  font-family: 'UnidreamLED';
  src: url("https://cdn.jsdelivr.net/npm/akilar-candyassets/fonts/UnidreamLED.ttf");
  font-display: swap;
}
div#runtime {
  width: 280px;
  margin: auto;
  color: #fff;
  padding-inline: 5px;
  border-radius: 10px;
  background-color: rgba(0,0,0,0.7);
  font-family: 'UnidreamLED';
}
[data-theme="dark"] div#runtime {
  color: #28b4c8;
  box-shadow: 0 0 5px rgba(28,69,218,0.71);
  animation: flashlight 1s linear infinite alternate;
}
/*悬停显示徽标提示语*/
a.github-badge:hover:before {
  position: fixed;
  width: fit-content;
  margin: auto;
  left: 0;
  right: 0;
  top: 10%;
  border-radius: 10px;
  text-align: center;
  z-index: 100;
  content: attr(data-title);
  font-size: 20px;
  color: #fff;
  padding: 10px;
  background-color: var(--text-bg-hover);
}
[data-theme=dark] a.github-badge:hover:before {
  background-color: rgba(18,18,18,0.8);
}
@-moz-keyframes flashlight {
  from {
    box-shadow: 0 0 5px #1478d2;
  }
  to {
    box-shadow: 0 0 2px #1478d2;
  }
}
@-webkit-keyframes flashlight {
  from {
    box-shadow: 0 0 5px #1478d2;
  }
  to {
    box-shadow: 0 0 2px #1478d2;
  }
}
@-o-keyframes flashlight {
  from {
    box-shadow: 0 0 5px #1478d2;
  }
  to {
    box-shadow: 0 0 2px #1478d2;
  }
}
@keyframes flashlight {
  from {
    box-shadow: 0 0 5px #1478d2;
  }
  to {
    box-shadow: 0 0 2px #1478d2;
  }
}
```
我的js配置为
```shell
setInterval(() => {
    let create_time = Math.round(new Date('2024-07-06 22:00:00').getTime() / 1000); //在此行修改建站时间
    let timestamp = Math.round((new Date().getTime()) / 1000);
    let second = timestamp - create_time;
    let time = new Array(0, 0, 0, 0, 0);

    var nol = function(h){
      return h>9?h:'0'+h;
    }
    if (second >= 24 * 3600) {
      time[1] = parseInt(second / (24 * 3600));
      second %= 24 * 3600;
    }
    if (second >= 3600) {
      time[2] = nol(parseInt(second / 3600));
      second %= 3600;
    }
    if (second >= 60) {
      time[3] = nol(parseInt(second / 60));
      second %= 60;
    }
    if (second > 0) {
      time[4] = nol(second);
    }
     currentTimeHtml ="<div id='runtime'>" + '本站距今已运行了 ' + time[1] + ' 天 ' + time[2] + ' 时 ' + time[3] + ' 分 ' + time[4] + ' 秒' + '</div>';
    document.getElementById("workboard").innerHTML = currentTimeHtml;
  }, 1000);
```
### 11.修改字体
这个我有心理阴影，不再赘述，有需求自行查阅
### 12.