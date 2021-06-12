
# 波尔克

（谐音“博儿客”）

# 介绍
个人网站用了有四年了，期间一直都是用PHP+MySql的方式部署在阿里云，从备案域名折腾服务器，到调试各种插件，从制定学习计划，到学课程，又是边写文章边研究Markdown排版，种种事情花了很大功夫。今年1月份发生了一件事情——服务器到期，那会儿工作忙一直拖着续费的事情。阿里清空了磁盘，我也是事后才注意到通知短信，发现网站的文章数据全丢的那一刻，整个人浑身感觉都不好了。

痛定思痛，决定文章还是要继续写，写哪里呢CSDN、博客园、简书、掘金都只适合当存档的地方，毕竟没有个人网站用起来有感情。想起来之前工作的时候，为了写音视频直播学了Node，注意过Hexo框架，这个框架可以快速搭个人网站。哎哟不错哦，一拍大腿说干就干。谁让咱是行动派！

最终我花了一天时间，使用码云仓库+Hexo搭一个小型静态网站。优点是：免费，简单，便捷，最大优点是动静分离，静态资源放国内仓库，占磁盘空间的图片资源放CDN服务器，通过域名转发访问，加载效率杠杠滴。

这篇文章主要包含了个人网站的技术架构和常见问题。包括使用的oss管理平台、域名管理、评论管理、文章编辑与发布、网站编辑管理等功能的设计与实现。

<!-- more -->

# 网站架构

| 名称                           | 用途                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| typora                         | markdown编辑器                                               |
| hexo                           | 博客服务                                                     |
| nodejs                         | hexo编译环境                                                 |
| gitee                          | 码云代码仓库                                                 |
| next                           | hexo主题                                                     |
| 七牛云                         | oss图片文件仓库                                              |
| 阿里云域名                     | 域名转发、cdn转发                                            |
| hexo-toc                       | 文档插件显示二级目录，响应点击事件                           |
| hexo-admin                     | 管理后台                                                     |
| hexo-wordcount                 | 统计字数                                                     |
| hexo-renderer-markdown-it-plus | markdown解析插件                                             |
| leanclound                     | 阅读量统计插件，如何配置[参考文章](https://blog.csdn.net/lijing742180/article/details/87928554) |
| gitment                        | git评论云                                                    |
| haoyuePlayer                   | 音乐播放                                                     |
| aplayer                        | 音乐播放                                                     |
| baidu_push                     | 文章推送                                                     |
| rating                         | 评分                                                         |
| calendar                       | 日历                                                         |
| live2d                         | 看板娘                                                       |
| Mpic                           | 图床发布工具，自动发布七牛                                   |
| Carouscl                   | [轮播图功能使用了Boostarp-Carouscl](https://getbootstrap.com/docs/4.0/components/carousel/) |
| valine-admin               | 评论云                                                       |
| hexo-related-popular-posts | 文章推荐                                                     |
| widgetpack                 | [文章评分](https://widgetpack.com/)                          |
| firestore                  | [top排行](https://www.liaofuzhan.com/posts/781439527.html)   |
| hexo-generator-index       | 分页                                                         |
| hexo-generator-archive     | 分页                                                         |
| hexo-generator-category    | 分页                                                         |
| hexo-generator-tag         | 分页                                                         |
| hexo-wordcount             | 字数与阅读时间                                               |
| gulp                       | 压缩代码                                                     |
| hexo-theme-Wikitten        | 文件树预览                                                   |
| hexo-directory-category    | 自定义分类页 |
| hexo-statistics-charts     | 静态图表统计post、tags                                       |
| hexo-online-server         | 在线编辑文章、页面、发布                                     |
| hexo-photoswipe            | [滑动轮播点击图片展示器](https://github.com/HarborZeng/hexo-photoswipe/blob/master/README_CN.md) |
| giteement | 评论云 |

# 模板架构

| 模板名称        | 用途                |
| --------------- | ------------------- |
| android-xx-Tips | Android百问百答模板 |
| book-note-model | 读书笔记模板        |
| draft           | 草稿模板            |
| page            | 页面模板            |
| post            | 文章模板            |



# 安装教程



## nodejs安装教程

步骤太简单了，难点就是找到合适版本、合适渠道的安装包，推荐国内使用方式2node中文网的方式下载安装

| 方式                                                         | 缺点                    | 优点             |
| ------------------------------------------------------------ | ----------------------- | ---------------- |
| [node官网](https://nodejs.org/zh-cn/)，点击链接下载，一路next同意协议安装 | 国外服务器下载慢        | 最新安装包       |
| [node中文网](http://nodejs.cn/)，点击链接下载，一路next同意协议安装 | 安装包版本落后1-2个版本 | 国内服务器下载快 |

## 码云配置网站教程



## git使用教程



## hexo使用教程



hexo官网有详细步骤，小白可以参考百度上的安装教程博客

| 方式                                                      | 步骤                                                         | 缺点                           | 优点               |
| --------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------ | ------------------ |
| [hexo官网](https://hexo.io/zh-cn/docs/)，权威hexo安装步骤 | npm install -g hexo-cli；                                    | 不适合小白用户，命令行操作居多 | 简洁，明了，歧义少 |
| 搜索引擎“hexo安装步骤”                                    | [《参考》](https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html) | 遇到问题较难解答               | 傻瓜式，上手快     |

# hexo常见指令

| 指令                       | 用途                                                         |
| -------------------------- | ------------------------------------------------------------ |
| hexo init                  | 在当前目录下创建工程                                         |
| _config.yml                | deploy:   type: git   repository: git@github.com:liuxianan/liuxianan.github.io.git   branch: master |
| hexo clean                 | 清除缓存                                                     |
| hexo g                     | 生成web                                                      |
| hexo s                     | 启动web服务并预览，在浏览器输入 <http://localhost:4000>      |
| hexo d                     | 发布pulic 目录下的静态页面至github                           |
| git clone url themes/yilia | 下载指定主题到根目录/thems/yilia/ 下                         |
| hexo new "postName"        | 新建文章，hexo n                                             |
| hexo new page "pageName"   | #新建页面                                                    |
| hexo generate              | 生成静态页面至public目录，hexo g                             |
| hexo server                | 开启预览访问端口（默认端口4000，'ctrl + c'关闭server）       |
| hexo deploy                | hexo d                                                       |
| hexo s -g                  | 生成并本地预览                                               |

# markdwon使用技巧

更多markdwon技巧可以移步至我的[Typora知识Wiki](https://shaunsheep.github.io/quickshortkey/#/typora)

## 缩放图片四种种技巧

```shell
<img src="" width="50%" height="50%">
![test image size](url){:class="img-responsive"}
![test image size](url){:height="50%" width="50%"}
![test image size](url){:height="100px" width="400px"}
```

## 设置字体颜色

```html
<label style="color:green">**数学日记**</label>
```

## 使用数学公式

| 文档名称                                                     | 优点                                     |      |
| ------------------------------------------------------------ | ---------------------------------------- | ---- |
| [KaTeX公式文档](https://katex.org/docs/supported.html#accents) | 网站清新，简洁，数学公式非常全，导航详细 |      |
| CTEX公式文档                                                 | 导航较为隐晦，除了数学公式外还有其他公式 |      |
|                                                              |                                          |      |

## markdown设置表格宽度

```css
| a | b | d |
|---|---|---|
| 1 | <div style="width: 150pt">very very very very very lonng long long long long text</div>| 3 |

```

```css
<div style="width: 150pt">  <div style="width: 50%">  ..
```



## markdown如何换行

markdown表格内换行需要使用`<br>`

## markdown如何开启数学公式

[1.开启行内公式模块，默认是关闭的。](https://www.dazhuanlan.com/2020/02/29/5e59eaf910c97/)

文件—>偏好设置—>Markdown,勾选内联公式，重启typora。

使用方式参考latext文档

## markdown设置字体颜色

**HTML方式：**

```css
　<font color='red'> text </font>
```

效果：　<font color='red'> text </font>

**KaTex/MathJax方式:**

```css
$\color{red}{红色字}$
```

效果：$\color{red}{红色字}$

## markdown如何等比缩放图片

在img标签里面只设置宽，不设置高，图片就会等比例缩放。

# 常见问题

## 如何搭建一个wiki页面

参考我的[如何做一篇wiki](https://shaunsheep.github.io/quickshortkey/#/)

## **码云部署hexo站点 css样式不显示？**

原因：仓库地址与个性地址url不一致
解决：修改_config.yml  
    ```xml
    url: https://ipvb.gitee.io/blog
    root: /blog
    ​```

其他码云部署的问题参考[这里](https://gitee.com/help/articles/4136#article-header3)

## hexo如何缩放图片

`<img src="" width="50%" height="50%">`

## hexo如何安装主题

1. 找到合适的主题列表，推荐以下2个：

   [有哪些好看的 Hexo 主题？](https://www.zhihu.com/question/24422335)

   [hexo.thems](https://hexo.io/themes/)

2. 安装主题至根目录，例如找到next主题，将其克隆岛根目录/thesms/next下

    ```js
     git clone https://github.com/iissnan/hexo-theme-next themes/next
    ```

3. 阅读[next文档](https://github.com/iissnan/hexo-theme-next)

    1. 引用主题：在config.yml中修改主题名称：`theme: next`
    2. 发布时遇到 bug`{% extends '_layout.swig' %}`；输入指令解决：`npm i hexo-renderer-swig`

## hexo不显示二级目录？

原因：hexo解析目录是按照1级，1级下面找2级，2级下面找3级的顺序查找目录的，如果只有2级，没有1级，是会显示错误的。

解决：先写1级标题，再写2级标题，先写大标题，再写小标题。

原因：markdown解析问题

解决：参考[渲染错误解决和超链接乱码解决方案](https://www.cnblogs.com/Createsequence/p/14150758.html)、参考[markdown-it的bug](https://convivae.top/posts/hexo-bo-ke-cai-keng/#%E6%96%B9%E6%B3%95-2)

## hexo点击二级目录不跳转?

原因：markdown解析问题

解决：参考[渲染错误解决和超链接乱码解决方案](https://www.cnblogs.com/Createsequence/p/14150758.html)、参考[markdown-it的bug](https://convivae.top/posts/hexo-bo-ke-cai-keng/#%E6%96%B9%E6%B3%95-2)

## hexo自动发布图片至七牛云？

阿里云-域名管理-解析设置-添加记录-设置以下参数

| 键       | 值               |
| -------- | ---------------- |
| 记录类型 | CNAME            |
| 主机记录 | 如cdn            |
| 记录值   | 从七牛云后台获取 |

七牛云-域名管理-加速域名设置值如cdn.yangchaofan.cn；cdn就是主机记录值；创建完毕后，获得一个CNAME值，记住该值，填写至阿里云域名记录值中。

[](https://portal.qiniu.com/kodo/overview)

## next如何打开百度分享？

主题文件中插入以下代码

```js
baidushare:
  type: button
  baidushare: true
```

## next如何添加搜索功能？

安装插件

```shell
npm install hexo-generator-searchdb --save
```

编辑全局配置

```javascript
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

编辑主题配置

```javascript
local_search:
  enable: true
```

## next如何添加评论功能？

翻墙打开[来比力官网](https://livere.com)，注册填写域名，copy代码块中的data-uid

```js
<!-- 来必力City版安装代码 -->
<div id="lv-container" data-id="city" data-uid="这里是id">
	<script type="text/javascript">
   (function(d, s) {
       var j, e = d.getElementsByTagName(s)[0];

       if (typeof LivereTower === 'function') { return; }

       j = d.createElement(s);
       j.src = 'https://cdn-city.livere.com/js/embed.dist.js';
       j.async = true;

       e.parentNode.insertBefore(j, e);
   })(document, 'script');
	</script>
<noscript> 为正常使用来必力评论功能请激活JavaScript</noscript>
</div>
<!-- City版安装代码已完成 -->
```
配置完成后可以在评论[后台](https://livere.com/insight/communite)管理评论内容。

## next如何安装valine

```shell
npm install valine --save
```

## next配置gitment

[Hexo 博客接入 Gitment 评论系统踩坑](https://www.jianshu.com/p/d3ce2dd7900f?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)

[认证重定向错误](https://github.com/imsun/gitment/issues/16#)

## next如何添加置顶功能？

```shell
$ npm uninstall hexo-generator-index --save
$ npm install hexo-generator-index-pin-top --save
```

文章插入top属性，top数值按大小倒序排序

```shell
title: 置顶
date: 2019-09-09 09:09:09
top: true
top: 1
```

设置置顶样式：

打开：`/blog/themes/next/layout/_macro`目录下的`post.swig`文件，定位到`<div class="post-meta">`标签下，插入如下代码：

```html
<div class="post-meta">
          <span class="post-time">
在此之下插入代码，包含在 span块内        
          {% if post.top %}
            <i class="fa fa-thumb-tack"></i>
            <font color=7D26CD>置顶</font>
            <span class="post-meta-divider">|</span>
          {% endif %}
```

## next如何跳转至站内相对路径？

## hexo如何创建模板？

**模板有什么用？**

模板可以当做一类文章的格式，按照指定格式批量创建文章，减少重复内容的编写工作。如创建读书笔记模板、创建一类任务计划模板。

**创建模板步骤？**

- 新建md文件，文件头插入以下内容，并将文件移动至`根目录/scaffolds` 下

```javascript
title: 《超效学习方法解码》心得
date: 2021-02-17 11:37:23
entitle:
tags:
categories:
```

- 使用指令读取模板创建文章

```shell
# hexo new 模板名称 "title"
hexo new book-note-model "《超效学习方法解码》心得"
```

## hexo如何创建草稿？

**草稿的用途？**

文章写到一半，未完成，并不想发布。可以向存到指定位置。hexo提供了_drafts目录存放草稿。

**创建草稿的步骤？**

- ​创建草稿

```shell
	# hexo new draft "title"
	hexo new draft "Android性能优化百问百答"
	INFO  Validating config
	INFO  Created: 
	D:\workspace\gitblog\hexoblogcode\source\_drafts\Android性能优化百问百答.md

```

- 发布草稿

```shell
# hexo publish 布局类型 "title"
hexo publish draft "Android性能优化百问百答"
INFO  Validating config
INFO  Published: D:\workspace\gitblog\hexoblogcode\source\_posts\Android性能优化百问百答.md

```

##   next文章自适应屏幕宽度

`\themes\next\source/css/_schemes/Picses/_layout.styl`在文件末尾添加代码

```css
// 以下为新增代码！！修改post宽度
header{ width: 80% !important; }
header.post-header {
  width: auto !important;
}
.container .main-inner { width: 80%; }
.content-wrap { width: calc(100% - 260px); }

.header {
  +tablet() {
    width: auto !important;
  }
  +mobile() {
    width: auto !important;
  }
}

.container .main-inner {
  +tablet() {
    width: auto !important;
  }
  +mobile() {
    width: auto !important;
  }
}

.content-wrap {
  +tablet() {
    width: 100% !important;
  }
  +mobile() {
    width: 100% !important;
  }
}

```

## next添加头像

打开themes/next/_config.yml

打开并放入头像/themes/next/source/images/

```css
avatar: /images/avatar_2.gif
```

## next统计字数

```
pm i --save hexo-wordcount
```

在站点配置文件添加如下配置

    # Dependencies: https://github.com/willin/hexo-wordcount
    post_wordcount:
      item_text: true
      wordcount: true         #文章字数统计
      min2read: true          #文阅读时长
      totalcount: false       
      separated_meta: true
在NexT主题配置文件添加如下配置（NexT主题已支持该插件，有的话无需再添加）

    # Dependencies: https://github.com/willin/hexo-wordcount
    post_wordcount:
      item_text: true
      wordcount: true         #文章字数统计
      min2read: true          #文阅读时长
      totalcount: false       
      separated_meta: true
## next不蒜子失效问题

hexo-theme-next主题中使用了dn-lbstatics.qbox.me域名的文件位置为：

```js
 themes\next\layout\_third-party\analytics\busuanzi-counter.swi
```

找到如下代码：

```js
<script async src="https://dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```


修改为：

```js
<script async src="https://busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```



# 使用说明

1.  定时使用typora编写markdown文章：编写markdown文件
2.  导出成html，发布在hexo：使用hexo s
3.  hexo推送到码云指定仓库地址：hexo d
4.  将阿里云的域名解析至码云仓库地址：配置域名解析
5.  通过公网域名访问我的网站

# 支持

1.  [typora使用手册](https://support.typora.io/Resize-Image/)
2.  [Gitee 官方提供的使用手册]( https://gitee.com/help)
2.  [七牛云](https://portal.qiniu.com/kodo/overview) 
3.  [阿里云](https://homenew.console.aliyun.com/home/dashboard/ProductAndService) 
4.  [hexo中文文档](https://hexo.io/zh-cn/docs)
6.  [next中文文档](http://theme-next.iissnan.com/third-party-services.html#comment-system)
7.  [leanclound统计云](https://console.leancloud.cn/apps)
8.  [来比力评论云](https://livere.com/insight/communite)
9.  [快站畅言](https://www.kuaizhan.com/)
