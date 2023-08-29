---
title: Hexo 博客搭建和使用教程
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

<img src="/images/Git.png" />

* 安装后验证: 在 cmd 中输入命令 git --version, 查看 Git 版本

#### 1.3 安装 Node.js

* 官方下载地址: <u>[Node.js (nodejs.org)](https://nodejs.org/en)</u>
* 注意事项: 使用 Node.js 官方安装程序时，请确保勾选 Add to PATH 选项（默认已勾选）

<img src="/images/Node.png" />

* 安装后验证: 在 cmd 中输入命令 node -v, 查看 Node 版本
  
---

至此，您已经完成了安装 Hexo 所需的所有额外环境，接下来就可以安装 Hexo 了

### 第二章 安装 Hexo
#### 2.1 安装 Hexo

* 命令: npm install -g hexo-cli
  说明: -g 表示全局安装，hexo-cli 为所安装的包
* 安装后验证: 在 cmd 中输入命令 hexo -v, 可查看 hexo 版本
  
<img src="/images/hexo.png" />

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
  
<img style="display: flex;width:80%;margin: 0 auto;" src="/images/github.png"/>

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
   
<img src="/images/github-ssh.png" />

3. 生成了一个新的 C:\Users\您的用户名\ .ssh文件夹，打开这个文件夹，找到 .ssh\id_rsa.pub 文件，记事本打开并复制里面的内容
   
4. 打开您的 github 主页，进入个人设置 -> SSH and GPG keys -> New SSH key，把复制的内容粘贴进去，title 随便填，保存即可，我们的公钥就添加成功了，设置好如下图:

<img src="/images/github-key.png" />

5. 检测是否设置成功:

输入命令: ssh -T git@github.com

<img src="/images/github-success.png" />

看到以上信息说明 SSH 已配置成功!

6. 此外您还需要如下配置:
   
命令: git config --global user.name "您的 Github username" // 注意是 username, 而非昵称

命令: git config --global user.email "xxx@qq.com" // 填写您的 github 注册邮箱

---

至此，您已经成功配置好了 Github，接下来开始搭建个人博客吧!

### 第四章 使用 Hexo 搭建博客