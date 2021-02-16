# 网站波尔克

#### 介绍
阿里云服务器用了三年了，到期忘了续费。网站文章资料忘了及时导出，也被清空了。于是打算使用免费仓库搭一个个人网站，简单，使用，空间够用。

#### 网站架构
软件架构：

hexo

nodejs

npm

gitee


#### 安装教程

1. nodejs安装教程

   步骤太简单了，难点就是找到合适版本、合适渠道的安装包，推荐国内使用方式2node中文网的方式下载安装

   | 方式                                                         | 缺点                    | 优点             |
   | ------------------------------------------------------------ | ----------------------- | ---------------- |
   | [node官网](https://nodejs.org/zh-cn/)，点击链接下载，一路next同意协议安装 | 国外服务器下载慢        | 最新安装包       |
   | [node中文网](http://nodejs.cn/)，点击链接下载，一路next同意协议安装 | 安装包版本落后1-2个版本 | 国内服务器下载快 |
   |                                                              |                         |                  |

2. 码云配置网站教程

3. git使用教程

4. hexo使用教程

   hexo官网有详细步骤，小白可以参考百度上的安装教程博客

   | 方式                                                      | 步骤                                                         | 缺点                           | 优点               |
   | --------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------ | ------------------ |
   | [hexo官网](https://hexo.io/zh-cn/docs/)，权威hexo安装步骤 | npm install -g hexo-cli；                                    | 不适合小白用户，命令行操作居多 | 简洁，明了，歧义少 |
   | 搜索引擎“hexo安装步骤”                                    | [《参考》](https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html) | 遇到问题较难解答               | 傻瓜式，上手快     |
   |                                                           |                                                              |                                |                    |

   hexo常见指令

   | 指令                       | 用途                                                         |
   | -------------------------- | ------------------------------------------------------------ |
   | hexo init                  | 在当前目录下创建工程                                         |
   | _config.yml                | deploy:   type: git   repository: git@github.com:liuxianan/liuxianan.github.io.git   branch: master |
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
   |                            |                                                              |

   ​

#### 使用说明

1.  定时使用typora编写markdown文章
2.  导出成html，发布在hexo
3.  hexo推送到码云指定仓库地址
4.  将阿里云的域名解析至码云仓库地址
5.  通过公网域名访问我的波尔克

#### 特技

1.  使用 Readme\_XXX.md 来支持不同的语言，例如 Readme\_en.md, Readme\_zh.md
2.  Gitee 官方博客 [blog.gitee.com](https://blog.gitee.com)
3.  你可以 [https://gitee.com/explore](https://gitee.com/explore) 这个地址来了解 Gitee 上的优秀开源项目
4.  [GVP](https://gitee.com/gvp) 全称是 Gitee 最有价值开源项目，是综合评定出的优秀开源项目
5.  Gitee 官方提供的使用手册 [https://gitee.com/help](https://gitee.com/help)
6.  Gitee 封面人物是一档用来展示 Gitee 会员风采的栏目 [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)
