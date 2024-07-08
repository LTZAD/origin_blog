---
title: Hexo博客网站搭建过程
categories: 记录
description: 这里将持续更新本站搭建全过程
swiper_index: 2
cover: /pictures/cover_1.jpg
---
# 搭建记录
这篇文章的内容为本站的搭建过程，省略一些修改图片路径等简易操作
## 1.初始化Hexo项目
在新的文件夹中打开终端，输入以下
``` shell
hexo init
```
## 2.安装初始依赖库
接着输入
``` shell
npm i
```
通过这个使博客内容可以正常显示
## 3.将博客挂载到github pages
随后安装hexo-deployer-git使博客能够上传到github
```shell
npm install hexo-deployer-git --save
```
（在此之后，在_config.yml中修改deploy内容，这里省略）
## 4.安装butterfly主题
```shell
npm i hexo-theme-butterfly
```
随后安装渲染器
```shell
npm install hexo-renderer-pug hexo-renderer-stylus --save
```
在此之后将_config.yml中的theme改为butterfly
并且将language改为zh-CN
## 5.文章显示
修改主题配置文件_config.butterfly.yml中的post_meta
date_type均改为both
date_format均改为relative
## 6.本地搜索
安装以下依赖
```shell
npm install hexo-generator-search --save
```
_config.yml中加入
```yml
search:
  path: search.xml
  field: post
  content: true
```
_config.butterfly.yml中local_search的enable改为true
## 7.字数统计
安装以下依赖
```shell
npm install hexo-wordcount --save
```
_config.butterfly.yml中wordcount的enable改为true
## 8.鼠标点击效果
_config.butterfly.yml中fireworks或者Heart symbol或者words的enable改为true
## 9.修改为一图流
首先在source文件夹内新建css文件夹，并新建custom.css写入以下代码
```css
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
```yml
inject:
  head:
    - <link rel="stylesheet" href="/css/custom.css" media="defer" onload="this.media='all'">
```
## 10.页脚徽标
安装以下依赖
```shell
npm install hexo-butterfly-footer-beautify --save
```
在站点配置文件_config.yml或者主题配置文件_config.butterfly.yml中添加（这是我的配置）
```yml
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
```css
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
```js
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
## 11.修改字体
这个我有心理阴影，不再赘述，有需求自行查阅
## 12.文章置顶滚动栏
安装以下依赖
```shell
npm install hexo-butterfly-swiper --save
```
在站点配置文件_config.yml或者主题配置文件_config.butterfly.yml中添加
```yml
# hexo-butterfly-swiper
# see https://akilar.top/posts/8e1264d1/
swiper:
  enable: true # 开关
  priority: 5 #过滤器优先权
  enable_page: all # 应用页面
  timemode: date #date/updated
  layout: # 挂载容器类型
    type: id
    name: recent-posts
    index: 0
  default_descr: 再怎么看我也不知道怎么描述它的啦！
  swiper_css: https://npm.elemecdn.com/hexo-butterfly-swiper/lib/swiper.min.css #swiper css依赖
  swiper_js: https://npm.elemecdn.com/hexo-butterfly-swiper/lib/swiper.min.js #swiper js依赖
  custom_css: https://npm.elemecdn.com/hexo-butterfly-swiper/lib/swiperstyle.css # 适配主题样式补丁
  custom_js: https://npm.elemecdn.com/hexo-butterfly-swiper/lib/swiper_init.js # swiper初始化方法
```
在博客中使用swiper_index，后边数字越大越优先展示
## 13.文章双侧栏显示及加载动画
本篇分为两个部分，首先实现双侧栏显示，随后是加载动画
### A.双侧栏显示
安装以下依赖
```shell
npm i hexo-butterfly-article-double-row --save
```
在网站配置文件_config.yml中新增以下项
```yml
butterfly_article_double_row:
  enable: true
```
在custom.css中新增以下使按钮居中
```css
#pagination {
  width: 100%;
  margin: auto;
}
```
### B.wowjs动画
安装以下依赖
```shell
npm install hexo-butterfly-wowjs --save
```
在站点配置文件_config.yml或者主题配置文件_config.butterfly.yml中添加（这是我的配置）
```yml
wowjs:
  enable: true #控制动画开关。true是打开，false是关闭
  priority: 10 #过滤器优先级
  mobile: false #移动端是否启用，默认移动端禁用
  animateitem:
    - class: recent-post-item #必填项，需要添加动画的元素的class
      style: animate__fadeInLeft #必填项，需要添加的动画
      duration: 1s #选填项，动画持续时间，单位可以是ms也可以是s。例如3s，700ms。
      delay: 0 #选填项，动画开始的延迟时间，单位可以是ms也可以是s。例如3s，700ms。
      offset: 100 #选填项，开始动画的距离（相对浏览器底部）
      iteration: 1 #选填项，动画重复的次数
    - class: card-widget
      style: animate__fadeInRight
      duration: 1s #选填项，动画持续时间，单位可以是ms也可以是s。例如3s，700ms。
      delay: 0 #选填项，动画开始的延迟时间，单位可以是ms也可以是s。例如3s，700ms。
  animate_css: https://npm.elemecdn.com/hexo-butterfly-wowjs/lib/animate.min.css
  wow_js: https://npm.elemecdn.com/hexo-butterfly-wowjs/lib/wow.min.js
  wow_init_js: https://npm.elemecdn.com/hexo-butterfly-wowjs/lib/wow_init.js
```
如需修改动画效果，参考[Animate.css](https://animate.style/)，复制并更改style后的内容
## 14.菜单栏居中
在custom.css文件中新增以下
```css
/* 一级菜单居中 */
#nav .menus_items {
  position: absolute !important;
  width: fit-content !important;
  left: 50% !important;
  transform: translateX(-50%) !important;
}
```
修改_config.butterfly.yml中menu的列表，后加hide
```yml
列表||fas fa-list || hide:
```
通过这个可以确保列表在手机端为折叠状态
## 15.黑夜模式下文字霓虹灯效果
在custom.css文件中新增以下
```css
/* 日间模式不生效 */
[data-theme="light"] #site-name,
[data-theme="light"] #site-title,
[data-theme="light"] #site-subtitle,
[data-theme="light"] #post-info {
  animation: none;
}
/* 夜间模式生效 */
[data-theme="dark"] #site-name,
[data-theme="dark"] #site-title {
  animation: light_15px 10s linear infinite;
}
[data-theme="dark"] #site-subtitle {
  animation: light_10px 10s linear infinite;
}
[data-theme="dark"] #post-info {
  animation: light_5px 10s linear infinite;
}
/* 关键帧描述 */
@keyframes light_15px {
  0% {
    text-shadow: #5636ed 0 0 15px;
  }
  12.5% {
    text-shadow: #11ee5e 0 0 15px;
  }
  25% {
    text-shadow: #f14747 0 0 15px;
  }
  37.5% {
    text-shadow: #f1a247 0 0 15px;
  }
  50% {
    text-shadow: #f1ee47 0 0 15px;
  }
  50% {
    text-shadow: #b347f1 0 0 15px;
  }
  62.5% {
    text-shadow: #002afa 0 0 15px;
  }
  75% {
    text-shadow: #ed709b 0 0 15px;
  }
  87.5% {
    text-shadow: #39c5bb 0 0 15px;
  }
  100% {
    text-shadow: #5636ed 0 0 15px;
  }
}

@keyframes light_10px {
  0% {
    text-shadow: #5636ed 0 0 10px;
  }
  12.5% {
    text-shadow: #11ee5e 0 0 10px;
  }
  25% {
    text-shadow: #f14747 0 0 10px;
  }
  37.5% {
    text-shadow: #f1a247 0 0 10px;
  }
  50% {
    text-shadow: #f1ee47 0 0 10px;
  }
  50% {
    text-shadow: #b347f1 0 0 10px;
  }
  62.5% {
    text-shadow: #002afa 0 0 10px;
  }
  75% {
    text-shadow: #ed709b 0 0 10px;
  }
  87.5% {
    text-shadow: #39c5bb 0 0 10px;
  }
  100% {
    text-shadow: #5636ed 0 0 10px;
  }
}

@keyframes light_5px {
  0% {
    text-shadow: #5636ed 0 0 5px;
  }
  12.5% {
    text-shadow: #11ee5e 0 0 5px;
  }
  25% {
    text-shadow: #f14747 0 0 5px;
  }
  37.5% {
    text-shadow: #f1a247 0 0 15px;
  }
  50% {
    text-shadow: #f1ee47 0 0 5px;
  }
  50% {
    text-shadow: #b347f1 0 0 5px;
  }
  62.5% {
    text-shadow: #002afa 0 0 5px;
  }
  75% {
    text-shadow: #ed709b 0 0 5px;
  }
  87.5% {
    text-shadow: #39c5bb 0 0 5px;
  }
  100% {
    text-shadow: #5636ed 0 0 5px;
  }
}
```
## 16.个人卡片渐变色
在custom.css中新增
```css
/* 侧边栏个人信息卡片动态渐变色 */
#aside-content > .card-widget.card-info {
  background: linear-gradient(
    -45deg,
    #e8d8b9,
    #eccec5,
    #a3e9eb,
    #bdbdf0,
    #eec1ea
  );
  box-shadow: 0 0 5px rgb(66, 68, 68);
  position: relative;
  background-size: 400% 400%;
  -webkit-animation: Gradient 10s ease infinite;
  -moz-animation: Gradient 10s ease infinite;
  animation: Gradient 10s ease infinite !important;
}
@-webkit-keyframes Gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
@-moz-keyframes Gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
@keyframes Gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

/* 黑夜模式适配 */
[data-theme="dark"] #aside-content > .card-widget.card-info {
  background: #191919ee;
}

/* 个人信息Follow me按钮 */
#aside-content > .card-widget.card-info > #card-info-btn {
  background-color: #3eb8be;
  border-radius: 8px;
}
```
颜色内容可以自行更改
## 17.页面样式调节
在css中添加
```css
:root {
  --trans-light: rgba(255, 255, 255, 0.88);
  --trans-dark: rgba(25, 25, 25, 0.88);
  --border-style: 1px solid rgb(169, 169, 169);
  --backdrop-filter: blur(5px) saturate(150%);
}

/* 首页文章卡片 */
#recent-posts > .recent-post-item {
  background: var(--trans-light);
  backdrop-filter: var(--backdrop-filter);
  border-radius: 25px;
  border: var(--border-style);
}

/* 首页侧栏卡片 */
#aside-content .card-widget {
  background: var(--trans-light);
  backdrop-filter: var(--backdrop-filter);
  border-radius: 18px;
  border: var(--border-style);
}

/* 文章页、归档页、普通页面 */
div#post,
div#page,
div#archive {
  background: var(--trans-light);
  backdrop-filter: var(--backdrop-filter);
  border: var(--border-style);
  border-radius: 20px;
}

/* 导航栏 */
#page-header.nav-fixed #nav {
  background: rgba(255, 255, 255, 0.75);
  backdrop-filter: var(--backdrop-filter);
}

[data-theme="dark"] #page-header.nav-fixed #nav {
  background: rgba(0, 0, 0, 0.7) !important;
}

/* 夜间模式遮罩 */
[data-theme="dark"] #recent-posts > .recent-post-item,
[data-theme="dark"] #aside-content .card-widget,
[data-theme="dark"] div#post,
[data-theme="dark"] div#archive,
[data-theme="dark"] div#page {
  background: var(--trans-dark);
}


/* 夜间模式页脚页头遮罩透明 */
[data-theme="dark"] #footer::before {
  background: transparent !important;
}
[data-theme="dark"] #page-header::before {
  background: transparent !important;
}

/* 阅读模式 */
.read-mode #aside-content .card-widget {
  background: rgba(158, 204, 171, 0.5) !important;
}
.read-mode div#post {
  background: rgba(158, 204, 171, 0.5) !important;
}

/* 夜间模式下的阅读模式 */
[data-theme="dark"] .read-mode #aside-content .card-widget {
  background: rgba(25, 25, 25, 0.9) !important;
  color: #ffffff;
}
[data-theme="dark"] .read-mode div#post {
  background: rgba(25, 25, 25, 0.9) !important;
  color: #ffffff;
}
```
## 18.音乐播放器
安装以下依赖
```shell
npm install hexo-tag-aplayer --save
```
在_config.yml中添加
```yml
# 音乐插件
aplayer: 
  meting: true
  asset_inject: false
```
并且在_config.butterfly.yml中修改aplayerInject
```yml
aplayerInject:
  enable: true
  per_page: true
```
其余用法等不再赘述，详情见[Butterfly添加全局吸底Aplayer教程](https://butterfly.js.org/posts/507c070f/)或者参考[APlayer官网档案](https://aplayer.js.org/#/zh-Hans/)
### 附：再在这里贴一个魔改音乐播放器教程
详情见[butterfly魔改aplayer音乐](https://blog.anheyu.com/posts/6c69.html)
## 19.