

[官网](https://docsify.js.org/)

### 初始化后出现的三个文件
index.html 入口文件
README.md 会做为主页内容渲染
.nojekyll ./docs 目录下创建一个 .nojekyll 文件，以防止 GitHub Pages 忽略下划线开头的文件。




### 搭建过程  过程中存在的报错也一并记录
>前提： 需安装node.js  主要是为了生成初始化文件  如果你拷贝了文件，当我这个前提没说
 
>最近公司一直网络错误
删除掉删除用户目录下的.npmrc  又可以了
```
npm i docsify-cli -g
```
然后我在Git clone 已经创建在gitee上的docs空仓库，在控制台输入 
```
docsify init ./
```
不行  cli安装成功后，init 初始化，报：
'docsify' 不是内部或外部命令，也不是可运行的程序 或批处理文件  
设置了环境变量，在idea控制台依然显示docsify不是内部和外部的命令  
然后我在下面位置输入cmd，弹出当前目录的cmd窗口
<img src="img/articles/clipboard.png">
成功创建docs文件夹和里面的文件，因为前面我已经clone下来，文件夹已存在，所以我选择覆盖  
根据命令提示我输入
```
docsify serve docs
```
在浏览器输入http://localhost:3000/#/  查看

你直接下载Github仓库的项目是没办法打开index.html
必须运行docsify服务


#### 配置Github Corner
https://www.jianshu.com/p/4883e95aa903

window.$docsify的 repo 参数配置仓库地址
```javascript
    window.$docsify = {
      name: 'yuyege',
      repo: 'https://gitee.com/hjh_698/docs.git',
      coverpage: true
    }
```
#### 开启渲染封面
coverpage 参数
```javascript
window.$docsify = {
        coverpage: true
}
```
封面的生成同样是从 markdown 文件渲染来的。开启渲染封面功能后在文档根目录创建 _coverpage.md 文件，在文档中编写需要展示在封面的内容。
```html
![logo](https://docsify.js.org/_media/icon.svg)

# 测试说明文档

> 使用Vue全家桶+Node.js搭建的小型全栈项目.

* 前端框架：vue-cli、vue-router、axios、vuex
* UI类库：Mint-UI、Vant
* 后端数据接口：Express、MongoDB

[GitHub](https://github.com/Hanxueqing/Douban-Movie.git)
[Get Started](#quick-start)
```


#### 封面主题
目前的背景是随机生成的渐变色，我们自定义背景色或者背景图。可以参考官网文档封面这一章节自行设置。
直接打开 index.html 修改替换 css 地址即可切换主题，官方目前提供五套主题可供选择，模仿 Vue 和 buble 官网订制的主题样式。还有 @liril-net 贡献的黑色风格的主题
```html
  <link rel="stylesheet" href="//unpkg.com/docsify/themes/vue.css">
  <link rel="stylesheet" href="//unpkg.com/docsify/themes/buble.css">
  <link rel="stylesheet" href="//unpkg.com/docsify/themes/dark.css">
  <link rel="stylesheet" href="//unpkg.com/docsify/themes/pure.css">
  <link rel="stylesheet" href="//unpkg.com/docsify/themes/dolphin.css">
 ```

https://jhildenbiddle.github.io/docsify-themeable/#/themes?id=simple
```html
<!-- Theme: Defaults  极简主题 -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify-themeable@0/dist/css/theme-defaults.css">
<!-- Theme: simple -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify-themeable@0/dist/css/theme-simple.css">
<!-- Theme: Simple Dark -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify-themeable@0/dist/css/theme-simple-dark.css">

```

#### 多页面

目前我创建的文档是单页面的，上下滚动即可浏览全部内容。如果想创建多个页面，即点击左侧侧边栏导航跳转到不同url，就需要配置多级路由，这一功能在docsify中也很容易实现，我们需要在index.html文件中的window.$docsify中开启loadSidebar选项：
```javascript
<script>
  window.$docsify = {
    loadSidebar: true
  }
</script>
<script src="//unpkg.com/docsify"></script>
```

然后在根目录创建自己的_sidebar.md文件，配置我们需要显示的页面。详细操作步骤参考官方多页文档教程。https://links.jianshu.com/go?to=https%3A%2F%2Fdocsify.js.org%2F%23%2Fzh-cn%2Fmore-pages
注：配置了loadSidebar后就不会生成默认的侧边栏了。
```html
* Introduction
    * [简介](README.md)


- 一级目录1
    - [总概](README.md)
    - <details><summary><b>二级目录1</b></summary>
      <p>

        - [实例1](/zh-cn/test1.md) 
        - [实例2](/zh-cn/test2.md)
        - [实例3](README.md)
        - [实例4](README.md)
        - [实例5](README.md)

      </p>
      </details>
    

* 一级目录2
    - [实例1](/zh-cn/test1.md)
    - [实例2](/zh-cn/test2.md)
```

#### 路径问题
以项目根目录为准, 不管md文档在根目录的哪个子目录里面，路径从根目录下开始
不是以自身文档所在目录为准
```javascript
<img src="img/xx/xx.JPG">
[实例2](/zh-cn/test2.md)
```

### 插件

官方还提供了非常多实用的插件，比如说全文搜索、解析emoji表情、一键复制代码等等，完整版请参考官方插件列表。https://links.jianshu.com/go?to=https%3A%2F%2Fdocsify.js.org%2F%23%2Fzh-cn%2Fplugins

### 似乎有bug  ： 页面导航有时候没有刷新
docsify为什么导航没有刷新？
最后发现是zh-cn文件夹里面的导航修改了，但是docs根目录下的_saber.md文件没有发生修改
解决： index.html添加一个如下配置，然后去掉zh-cn文件夹下的_sidebar.md，这样只维护一个目录就够了。
```javascript
window.$docsify = {
    alias: { // 定义路由别名，可以更自由的定义路由规则。 支持正则
        '/.*/_sidebar.md': '/_sidebar.md',//防止意外回退  避免编辑多个sidebar目录文件
        '/.*/_navbar.md': '/_navbar.md'
    },
}
```


### 部署前
创建仓库 提交仓库
```
git add .
git commit -m 'msg'
git push orgin master // 这个之前需要提供 gitHub 账号和密码
```

### 部署在码云
网友都说不行，虾米，我试试开启
Gitee Pages 服务（开源项目静态效果演示用途）
<img src="img/articles/article1.JPG">
这种没人审核的网页要实名防止做坏事在国内需要认证似乎很正常
等我实名认证后，出现下面页面，强制https打钩，然后直接点击启动
<img src="img/articles/mybuild/giteepage.JPG">

一年前我在Gitee网站上搭建过，果然链接404了，但我repo的图库还在，也是实名验证问题吗

### 部署在个人服务器
首先，docsify是静态的无后台的，它只要使用域名能访问到index.html,就是部署成功
服务器我有，把项目docs文件夹放在www.junhao.host域名所在的目录下
使用www.junhao.host/docs即可访问
但是保险一点，配置一下nginx
路由www.junhao.host/docs，后面是重定向的位置，这样位置就可以很随意
```bash
server{

    # docs文档网站  第一条配置失败，404
    # location /docs/ {
    #     root  /xxx/test/docsite;
    #     index index.html index.htm;
    # }
    # 别名 访问docs开头的资源代理到以下目录
	location ^~/docs {
    	alias  /xxx/test/docsite/;
	}

}
```
访问试一下：http://www.junhao.host/docs/
缺点： 更新必须手动更新，不推荐这种方式

### 部署在Github
https://github.com/bingganlen/docs
打开settings，有一个Github Pages 的设置（或者直接在左导航点击Page），点击 source 中的本来的 None ，使其变成 master 分支
<img src="img/articles/mybuild/MAKEGitHub1.JPG" />
<img src="img/articles/mybuild/MAKEGitHub2.JPG" />
<img src="img/articles/mybuild/MAKEGitHub3.JPG" />
点击 save后出现一个网址
Your site is ready to be published at https://bingganlen.github.io/docs/

其它： 一次提交到GitHub和Gitee
```bash
[core]
	repositoryformatversion = 0
	filemode = false
	bare = false
	logallrefupdates = true
	symlinks = false
	ignorecase = true
[submodule]
	active = .
[remote "origin"]
	url = https://gitee.com/xxxx/docs.git
	url = git@github.com:xxxx/docs.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master
```

代码推送过程中的小bug，GitHub需要SSH免登无认证的连接，才能clone和push，
新出的Github Token纯属误导（就是一坨屎），生成的token附在remote的url上也不能用。
个人网站文档更新必须手动更新，无趣；
码云gitee存在实名认证，似乎所有都不完美