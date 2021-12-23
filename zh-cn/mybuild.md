
### 初始化后出现的三个文件
index.html 入口文件
README.md 会做为主页内容渲染
.nojekyll ./docs 目录下创建一个 .nojekyll 文件，以防止 GitHub Pages 忽略下划线开头的文件。




### 搭建过程  过程中存在的报错也一并记录

 
最近公司一直网络错误
删除掉删除用户目录下的.npmrc  又可以了
npm i docsify-cli -g
然后我在Git clone 已经创建在gitee上的docs空仓库，在控制台输入 
docsify init ./
不行  cli安装成功后，init 初始化，报：
'docsify' 不是内部或外部命令，也不是可运行的程序 或批处理文件
设置了环境变量，在idea控制台依然显示docsify不是内部和外部的命令
然后我在下面位置输入cmd，弹出当前目录的cmd窗口
成功创建docs文件夹和里面的文件，因为前面我已经clone下来，文件夹已存在，所以我选择覆盖
根据命令提示我输入
docsify serve docs
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

### 插件

官方还提供了非常多实用的插件，比如说全文搜索、解析emoji表情、一键复制代码等等，完整版请参考官方插件列表。https://links.jianshu.com/go?to=https%3A%2F%2Fdocsify.js.org%2F%23%2Fzh-cn%2Fplugins