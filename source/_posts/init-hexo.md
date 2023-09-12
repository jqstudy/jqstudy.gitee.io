---
title: Hexo 博客搭建和使用教程
date: 2023-08-28 16:39:29
tags:
categories: web前端
---
从零搭建一个属于自己的静态博客网站，使用Hexo博客框架并部署到 Github，让您可以在不用购买云服务器的情况下拥有一个属于自己的博客网站。

### Hexo 介绍
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
官方地址: <u>[Hexo](https://hexo.io/zh-cn/index.html)</u>

### 第一章 前期准备
#### 1.1 安装前所需环境介绍

安装 Hexo 之前，需要确保您的 PC 中已经安装以下工具:
* Node.js <u>[地址: Node.js (nodejs.org)](https://nodejs.org/en)</u>
* Git <u>[地址: Git (git-scm.com)](https://git-scm.com/)</u>
  

如果您的电脑已经具备所需工具，那么您可以直接进入第二章开始安装 Hexo 了。

如果您还未安装这两款工具，那么请按照以下步骤进行安装。

#### 1.2 安装 Git

* 官方下载地址: <u>[Git - Downloading Package (git-scm.com)](https://git-scm.com/download/win)</u>
* 注意事项: 建议选择 64-bit Git for Windows Setup，并且安装时要勾选 Add to PATH 选项

<img src="/images/initHexo/Git.png" />

* 安装后验证: 在 cmd 中输入命令 git --version, 查看 Git 版本

#### 1.3 安装 Node.js

* 官方下载地址: <u>[Node.js (nodejs.org)](https://nodejs.org/en)</u>
* 注意事项: 使用 Node.js 官方安装程序时，请确保勾选 Add to PATH 选项（默认已勾选）

<img src="/images/initHexo/Node.png" />

* 安装后验证: 在 cmd 中输入命令 node -v, 查看 Node 版本
  
---

至此，您已经完成了安装 Hexo 所需的所有额外环境，接下来就可以安装 Hexo 了

### 第二章 安装 Hexo
#### 2.1 安装 Hexo

* 命令: npm install -g hexo-cli
  说明: -g 表示全局安装，hexo-cli 为所安装的包
* 安装后验证: 在 cmd 中输入命令 hexo -v, 可查看 hexo 版本
  
<img src="/images/initHexo/hexo.png" />

#### 2.2 注意事项

建议永远安装最新版本的 Hexo，以及 <u>[推荐的 Node.js 版本](https://hexo.io/zh-cn/docs/index.html#%E5%AE%89%E8%A3%85%E5%89%8D%E6%8F%90)</u>

| Hexo版本 | Node版本 |
|--- | --- |
| 6.0+ | 12.13.0 |
| 5.0+ | 10.13.0 |
| 4.1 - 4.2 | 8.10 |
| 4.0 | 8.6 |
| 3.3 - 3.9 | 6.9 |
| 3.2 - 3.3 | 0.12 |
| 3.0 - 3.1 | 0.10 or iojs |
| 0.01 - 2.8 | 0.10 |

---

至此，您已成成功安装了 Hexo，接下来进入 Github 的配置吧!

### 第三章 配置 Github

如果您还没有 Gihub 账户，请注册一个 Github 账户吧!

#### 3.1 在 Github 上创建仓库

* 新建一个名为: <u>[http://username.github.io](http://username.github.io)</u> 的仓库(username 为您的 Github 用户名)
* 比如，如果您的 github 用户名是 test，那么您就新建名为 <u>[http://test.github.io](http://test.github.io)</u> 的仓库（必须是您的用户名，其它名称无效），将来你的网站访问地址就是 <u>[https://test.github.io](https://test.github.io)</u> 了。由此可见，每一个 github 账户最多只能创建一个这样可以直接使用域名访问的仓库。
  
<img style="display: flex;width:80%;margin: 0 auto;" src="/images/initHexo/github.png"/>

* 注意事项:
注册的邮箱一定要验证，否则不会成功;
仓库名字必须是：<u>[http://username.github.io](http://username.github.io)</u>，其中 username 是你的用户名;
仓库创建成功不会立即生效，需要过一段时间，大概10-30分钟，或者更久

#### 3.2 配置 SSH 免密登录

为什么要配置这个呢？因为您提交代码肯定要拥有您的 github 权限才可以，但是直接使用用户名和密码太不安全了，所以我们使用 ssh key 来解决本地和服务器的连接问题。
注: 如果您已经配置过 SSH，可跳过此步骤

步骤:

1. 首先打开电脑文件夹，找到 C:\Users\您的用户名\ .ssh文件夹并删除(如果没有，则直接进入第二步)
   
2. 在 C:\Users\您的用户名 文件夹下右键打开 Git Bash Here 输入命令: ssh-keygen -t rsa -C "你的github登录邮箱" 生成.ssh秘钥，输入后连敲三次回车，出现下图情况代表成功
   
<img src="/images/initHexo/github-ssh.png" />

3. 生成了一个新的 C:\Users\您的用户名\ .ssh文件夹，打开这个文件夹，找到 .ssh\id_rsa.pub 文件，记事本打开并复制里面的内容
   
4. 打开您的 github 主页，进入个人设置 -> SSH and GPG keys -> New SSH key，把复制的内容粘贴进去，title 随便填，保存即可，我们的公钥就添加成功了，设置好如下图:

<img src="/images/initHexo/github-key.png" />

5. 检测是否设置成功:

输入命令: ssh -T git@github.com

<img src="/images/initHexo/github-success.png" />

看到以上信息说明 SSH 已配置成功!

6. 此外您还需要如下配置:
   
命令: git config --global user.name "您的 Github username" // 注意是 username, 而非昵称

命令: git config --global user.email "xxx@qq.com" // 填写您的 github 注册邮箱

---

至此，您已经成功配置好了 Github，接下来开始搭建个人博客吧!

### 第四章 使用 Hexo 搭建博客

#### 4.1 初始化

1. 在电脑的某个磁盘或路径新建一个名为 hexo 的文件夹(名字可以随便取)，比如我的是 D:\hexo，由于这个文件夹将来就作为您存放代码的地方，所以最好不要随便放
   
2. 在 D:\hexo 文件夹下右键打开 Git Bash Here(控制台)，输入命令: hexo init 进行初始化

<img src="/images/initHexo/hexo-init.png" />

- hexo 会自动下载一些文件到这个目录，包括 node_modules，目录结构如下图:

<img src="/images/initHexo/hexo-file.png" />

3. 执行命令: hexo g 会在 public 文件夹下生成相关的 html 文件，这些文件将来需要提交到 Github 上

4. 执行命令: hexo s 可以开启本地预览服务，打开浏览器访问 http://localhost:4000 即可看到博客内容

#### 4.2 将博客部署到 Github

1. 在 D:\hexo 目录下安装 hexo-deployer-git 插件

- 命令: `npm install hexo-deployer-git --save`

2. 编辑 D:\hexo 目录下的 _config.yml 文件，在文件末尾添加如下内容:

<img src="/images/initHexo/upload-git.png" />

- 注意: 其中 repository 中的内容即为 github 个人主页链接地址

3. 在 D:\hexo 目录下，输入命令: hexo d 将本地 blog 推送到 github 远程仓库，也可能需要输入 username & pwd

推送成功后，即可通过 https://jqstudy.gitee.io/ 访问个人博客了!

---

至此，您已经会使用 Hexo 搭建博客了，但是您会发现此时访问博客主页，页面很不美观，那么接下来就对您的博客进行美化吧!

### 第五章 更换主题

在 D:\hexo 目录下有一个 themes 文件夹，该文件夹下存放着 hexo 所使用的主题

#### 5.1 搜索主题

- hexo 官方提供了很多主题供我们使用，地址: [Themes | Hexo](https://hexo.io/themes/), 选择喜欢的主题并点击即可跳转至 github
- 笔者使用了 github 上面一个大佬制作的主题，地址: [JoeyBling/hexo-theme-yilia-plus: 一个简洁优雅的hexo主题 A simple and elegant theme for hexo. (github.com)](https://github.com/JoeyBling/hexo-theme-yilia-plus)
- 您可以在 github 中直接搜索 hexo 主题

#### 5.2 下载主题

1. 在 D:\hexo 目录下右键 Git Bash Here(控制台)

2. 执行命令: `git clone 主题http链接 themes/主题名称` 将主题下载至 themes 文件夹下

<img src="/images/initHexo/git-clone.png" />

- 可以在该文件夹下查看是否下载成功

<img src="/images/initHexo/git-clone-file.png" />

#### 5.3 使用主题

- 打开 D:\hexo 目录下的 _config.yml 文件，在里面找到 theme: landscape改为theme: yilia-plus(yilia-plus为我们要使用的主题名)，然后执行 `hexo clean` 先删除旧的 html 文件，再执行 `hexo g` 重新生成，再执行 `hexo d` 推送到远程仓库

<img src="/images/initHexo/theme.png" />

- 在浏览器输入相应域名，发现主题已更换
- 注意: 可能需要等一段时间刷新才更换 please be patient

#### 5.4 修改主题内容

您可以在 themes/fluid 文件夹中查看该主题的内容，并可编辑该文件夹中的 _config.yml 文件修改主题样式

<img src="/images/initHexo/update-theme.png" />

- 注意: 记得编辑根目录下的 _config.yml 文件，将信息修改为自己的

<img src="/images/initHexo/Site.png" />

### 第六章 使用 Typora 编写博客

#### 6.1 Typora 介绍

Typora 是一款轻便简洁的 Markdown 编辑器，支持即时渲染技术，这也是与其他 Markdown 编辑器最显著的区别。即时渲染使得你写Markdown 就像是写 Word 文档一样流畅自如，不像其他编辑器的有编辑栏和显示栏。

优点:
- 简洁美观
- 实时预览
- 扩展语法
- 跨平台

#### 6.2 安装 Typora

官网: [Typora 官方中文站 (typoraio.cn)](https://typoraio.cn/)

遗憾的是去年 Typora 还是免费的，今年的新版居然开始收费了。

为此，我为大家准备了旧版免费的安装包 [typora-setup-x64.exe](https://www.aliyundrive.com/s/7Mfocz2n4fc) 提取码: `ah61`

#### 6.3 写博客

1. 在 D:\hexo 目录下，通过输入命令: hexo new "文章 title" 会在 /source 文件夹下生成对应文章的 .md 文件，然后就可以通过 Typora 打开此文件编写文章并保存了

2. 当您写完该篇文章后，依次输入以下命令:

`hexo clean` 删除 public 文件夹，即删除旧的博客文章

`hexo g` 生成 public 文件夹，即生成新的博客文章相关 html 文件

`hexo d` 将博客推送到 github

#### 6.4 向 Hexo 博客中插入图片

Hexo 有多种图片插入方式，可以将图片存放在本地引用或者将图片放在 CDN 上引用。

1. 本地引用–绝对路径

当 Hexo 项目中只用到少量图片时，可以将图片统一放在 source/images 文件夹中，通过 markdown 语法访问它们。

`![可以写关于图片的描述](/images/image.jpg)`

图片既可以在首页内容中访问到，也可以在文章正文中访问到。

2. 本地引用–相对路径

图片除了可以放在统一的 images 文件夹中，还可以放在文章自己的目录中。文章的目录可以通过配置 _config.yml 来生成。

打开项目根目录中的 _config.yml 文件，将 _config.yml文件中的配置项 post_asset_folder 设为 true 后，执行命令 hexo new "post_name"，在 source/posts 中会生成文章 post_name.md 和同名文件夹 post_name。

<img src="/images/initHexo/post_name.png" />

将图片资源放在 post_name 文件夹中，文章就可以使用相对路径引用图片资源了。

`![](image.jpg)`

但是使用这种引用方式，图片只能在文章中显示，但无法在首页中正常显示。

如果希望图片在文章和首页中同时显示，可以使用标签插件语法(推荐使用这种引用方法)。

`{% asset_img image.jpg This is an image %}`

3. CDN 引用(不推荐)

除了在本地存储图片，还可以将图片上传到一些免费的 CDN 服务中。

比如Cloudinary （梯子访问）提供的图片CDN服务，在 Cloudinary 中上传图片后，会生成对应的 url 地址，将地址直接拿来引用即可。或者上传到路过图床（不用梯子）。

### 第七章 总结

以上就是本人搭建博客的过程以及遇到的一些问题和解决办法，按照本人搭建博客的步骤就可以搭建一个相当不错的静态博客网站了。

如果想要让 baidu 和 google 搜索引擎收录自己的网站地址，可自行必应搜索。

谢谢大家!

参考教程: [www.bilibili.com/video](https://www.bilibili.com/video/BV1Yb411a7ty/?share_source=copy_web&vd_source=d698f3adeb829e7ec38eaffd67915950)