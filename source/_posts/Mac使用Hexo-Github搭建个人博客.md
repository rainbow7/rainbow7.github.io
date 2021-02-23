---
title: Mac使用Hexo+Github搭建个人博客
date: 2021-02-12 21:14:51
tags:
---
我是怎么来的？还是简单记录下我的出生吧。我的爸爸是[Hexo](https://hexo.io/zh-cn/)，它的自我介绍非常清晰，我就不废话啦。我的妈妈是[Github Pages](https://pages.github.com/)，点击即可了解，看过之后发现，其实就算只有妈妈，也是可以有我的。不过有了爸爸，会让我更好的成长。感谢你们！
<!-- more -->
从上面也了解到，其实我是由“两部分组成的”。下面就分别介绍这两个部分。不会很详细的介绍，只会包括流程。因为在它们各自的官网首页已经有很详细的讲解了。本文大多也是摘抄自官网。

### Hexo静态博客工具的安装

##### 安装[Node.js](https://nodejs.org/zh-cn/)，使用以下命令检查是否安装成功

```
node -v // 正常情况下，会有版本号输出
npm -v // npm是nodejs的包管理器，安装Hexo需要使用
```
##### 安装[Hexo](https://hexo.io/zh-cn/)

完成第一步后，安装Hexo就很简单了， 终端中输入`npm install hexo-cli -g`。完成后输入以下命令生成本地页面

```
hexo init blog  // 初始化博客文件夹blog，可改为其他
cd blog  // 进入到 blog 文件夹
npm install  // 安装
hexo new 文件名 // 创建新的文章，文章会以markdown格式保存在blog/source/_post中
hexo server  // 启动本地服务，这步执行完成之后，就可以在本地预览页面了，链接会在终端中输出，按住ctrl就可以点击查看了
```

经过以上两个步骤就完成了Hexo的安装，已经可以在本地浏览生成的页面了。下面将介绍如何配置Github Pages，以便将我们的页面上传到Github。

### Github Pages的配置

Github当然是依赖Git的了，所以要先安装好Git工具。

##### 安装[Git](https://git-scm.com/)

安装完成后终端输入`git version`，有版本号输出表示安装成功。

##### 配置Github Pages

首先需要开通Github，然后是设置SSH key，如果没有的话。

##### 配置多个SSH Key

这里简单说下配置多个SSH Key。比如公司的Git Lab仓库与我们的自己的Github分别使用不同的配置。

   1.生成新的密钥  `ssh-keygen -t rsa -C email // 将email替换为你要使用的email，回车后输入保存的文件名，如id_rsa_github`

   2.进入.shh文件夹，创建config文件  `vi config // 生成同时编辑config文件`

   3.为不同的域配置不同的SSH key
       
```
Host xxx.com // 域名
User email // 所配置的邮件地址
PreferredAuthentications publickey // 密钥类型，固定公钥
IdentityFile ~/.ssh/id_rsa_xxx // key 文件
#-----------------------------------------------------
Host xxx.com
User email
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa_xxx
```

##### 创建博客仓库

需要注意的是Repository name，<font color=#ff0000> 必须为username.github.io。username为你的Github的用户名。</font>创建完成以后。点击此Repository的Setting，向下滚动，找到Github Pages，目前Github仓库主分支名称已经改了main，我是习惯性的在创建时将分支名改为了master。此时如果在项目下新建一个名为index.html的文件，就可以通过https://username.github.io/ 来访问了。

### 关联Hexo与Github Pages

我们已经分别准备好了Hexo与Github Pages。是时候将它们关联起来了。

##### 配置部署脚本

进入到已经使用Hexo初始化好的博客文件夹（假定叫blog），打开_config.yml文件，向下滚动，找到deploy，加入如下配置，<font color=#ff0000>要注意空格必须要有</font>

```yml
deploy:
  type: 'git'
  repo: 'git@github.com:username/username.github.io.git' // 也就是平时clone仓库时的地址
  branch: 'master' // 博客所在的分支，据说目前只支持主分支，这个没有做验证
```
##### 安装deploy插件

终端执行`npm install hexo-deployer-git -save`完成后就可以使用Hexo进行部署了。以下是几个常用的命令，更多的命令可以通过hexo help查看。

```
hexo clean  // 清除，如果新的改动没有变化，可以试下，通常不需要
hexo g(generate)  // 生成页面
hexo s(server)  // 开启本地服务，可以先在本地预览
hexo d(deploy)  // 发布，成功的话，过一会儿，通常10几秒，打开https://username.github.io/就能看到自己写的文章了
hexo g -d  // 组合命令，生成+发布
```

现在已经可以开始写一些东西，并且方便的发布了。如果你想自定义主题，自定义域名，可以接着往下看。

##### 更换主题

找到自己的喜欢的[主题](https://hexo.io/themes/)，clone到blog文件夹下的themes文件夹，并修改_config.yml中的theme配置。是不是很简单。

##### 配置个性域名

以阿里云为例，点击添加记录，按以下配置添加，把记录值改为你的地址。然后在Repository添加一个文件CNAME，文件的内容是你的域名。最后在Repository的Setting中，Github Pages那里添加你的域名，点击保存。现在已经可以使用你自己的域名来访问站点了。各配置如下图所示
![](/assets/blogImage/ali_domain_setting.png)

### 替换Markdown插件

hexo默认的markdown插件为`hexo-renderer-marked`不是很给力。所以将它换为更强力的[hexo-renderer-markdown-it](https://github.com/hexojs/hexo-renderer-markdown-it)，至于怎么个强力法，用了才知道。先安利一个非常简介好用的markdwon编辑器[typora](https://typora.io/)。下面简单记录下替换步骤。

```xml
$ npm un hexo-renderer-marked --save  # 卸载原来的
$ npm i hexo-renderer-markdown-it --save  #安装新的
```

配置，具体的含意可以自行学习

```yaml
# Markdown-it config
markdown:
  render:
    html: true
    xhtmlOut: false
    breaks: true
    linkify: true
    typographer: true
    quotes: '“”‘’'
  plugins:
    - markdown-it-abbr      #缩写插件
    - markdown-it-footnote  #脚注插件
    - markdown-it-ins       #插入插件（下划线插件）
    - markdown-it-sub       #下标插件
    - markdown-it-sup       #上标插件
    - markdown-it-emoji     #emoji插件
    - markdown-it-container #内容块
    - markdown-it-deflist   #Definition list (<dl>) tag
    - markdown-it-ins       #++inserted++ => <ins>inserted</ins>
    - markdown-it-mark      #<mark> tag
  anchors:                  #锚
    level: 2                #最小对哪一级标题生效，对应H1-H6
    collisionSuffix: 'v'
    permalink: false        #链接，如果设置为true，点击后，会将其滚动到页面的最上方，
    permalinkClass: header-anchor
    permalinkSymbol: ¶      #锚的标记，说的直白点儿，就是你点击这个东西，会发生上面所说的滚动
```

这里说一下`anchors`，锚，开始时没搞清楚，还给作者提了个[Issues](https://github.com/XPoet/hexo-theme-keep/issues/64)

### FAQ

> 记录使用hexo过程中遇到的一些问题，为了保持整个目录的整洁，就不新建文章了。

##### deploy后，域名失效

解决方法：当我们使用自定义域名后，其实是生成了一个文件CNAME，里面记录着我们的域名，当deploy后，会使用blog/source下的文件替换github仓库中的文件，会把CNAME文件给搞没。找到问题之后，对症下药就好了，在source文件夹下新建一个CNAME文件，把我们域名写上就好了。这样每次deploy后，这个文件还会有，域名就可以正常使用了。