

[Hexo](http://zespia.tw/Hexo/) 是一个基于 `Node.js` 的静态博客程序, 可以方便的生成静态网页托管在 `github` 和 `Heroku` 上。

### 为什么要用静态博客？
- 跨平台同步文件
- 系统简单易懂, 毫不臃肿, 方便改版
- 众多第三方应用, 容易做自定义功能扩展
- 纯静态, 极低的服务器压力
- 最重要使用 `Markdown` 标记语法, 迁移什么的都非常方便
- 能够托管在 `Github` 上

下面简单用本博客介绍一下 `Hexo` 的简单使用扩展等

利用 `Hexo` 简单几步就能静态博客了

<!-- more -->

### Hexo 轻松搭建
- 安装 [nodejs](http://nodejs.org/) 和 [npm](https://npmjs.org/)
- npm install Hexo -g
- Hexo init blog -- 创建博客
- cd blog
- Hexo server -- 本地 Server
- Hexo generate -- 生成发布
- 修改 `blog/_config.yml` 中的的参数 `url` 在2.0+某版本中不为空立刻报错请保证不为空

具体细节请上 [http://zespia.tw/Hexo/](http://zespia.tw/Hexo/)


### 写作
在 `Hexo init blog` 生成的目录中, 将写好的 `md` 文件, 放入 `blog/source/_posts` 目录下即可
启动 `Hexo server` 可以边写边看效果, 注意备份好 `md` 文件方便以后更换系统主题迁移等操作。

长度控制可以编写 `md` 时, 添加 `<!-- more -->` 标签进行分割

官方默认属性, 通过编写 `title`, `date`, `author`, `categories`, `tags` 定义文章和从属分类等,
注意 `date` 必须填写, 否则在更换或迁移平台的时候, 生成的目录会发生变化,
因为根据生成当时的日期进行划分目录。(若没有更改 `_config.yml` 下的 `permalink` 属性情况下)

``` yml
layout: post
title: 用Hexo快速打造静态博客
date: 2013-09-15 12:00:00
categories: [前端]
tags: [Hexo, 静态博客, 自定义, 博客, 前端, github]
```

### 自定义主题
在生成的 `blog/themes/` 目录下就是所有主题, 可以通过配置 `blog/_config.yml` 文件中的 `theme` 进行主题更换, 注意的是修改完配置文件都要重启一下 `server` 或者 `generate` 重新生成一下。

若自行编写主题可能还是使用官方推荐的 `ejs` 可能会更好, 逻辑比较直观。

如果想做团队博客要注意 `Hexo` 环境必须相同, 所以建议将整个 `blog` 项目共享同步, 否则容易在版本更新时容易出现冲突。


### ishgo主题
`github` 项目地址 [https://github.com/ishgo-team/Hexo.ishgo](https://github.com/ishgo-team/Hexo.ishgo)


### Informations - 介绍
此主题主要用于团队技术博客而非其他个人博客, 因为主要优化在 `Markdown` 的代码着色, 着色主要参考 `submit Text2` 的 `monokai colors scheme`。

支持自适应, 采用 `bootstapr v3.0` , 已经兼容 `ie7+` 的手脚架, 主要考虑以后 `bootstap` 有比较好的扩展性和代码规范。

与官方默认主题不同的是使用 `jade` 和 `less` 来打造前端, 而非 `ejs` 和 `styl`, 所以安装有点儿麻烦

如果用于团队请将博客整个共享, 保证代码版本统一。否则在版本更新阶段容易造成代码冲突。

本主题不支持 `ie6`, `ie7` 以下版本, 支持 [ie6nomore](http://www.ie6nomore.com/) 行动。`ie6`, `ie7` 观看会跳到拒绝访问页面。

评论采用 `多说`, 侧栏的项目和评论数均由多说技术提供，已配置成本地与真实环境多说同步

可以添加新的文章属性

- `author` 作者, 根据 `ishgo/config.yml` 下的 `author` 进行查找, 如果显示相关信息。
- `hidden` 隐藏用于关于我们之类的文章, 在归档或目录下不会显示, 文章确实存在, 可直接不写。

实例:

``` yml
author: David
hidden: false
```

### Install - 安装

打开 `Hexo/_config.yml` 文件,
修改 `url` 成自己的博客地址, 不能为空,
修改 `plugins` 改成 `Hexo-renderer-jade` 和 `Hexo-renderer-less`,
修改 `theme` 属性改成 `ishgo`

``` yml
url: http://blog.ishgo.cn 
  
plugins:
  - hexo-renderer-jade
  - hexo-renderer-less
  
theme: ishgo
```

修改 `Hexo/package.json` 的 `dependencies` 添加 `Hexo-renderer-less` 和 `Hexo-renderer-jade` 两项

``` js
{
  "dependencies": {
    "Hexo-renderer-less": "*",
    "Hexo-renderer-jade": "*"
  }
}
```

~~其中 `Hexo-renderer-less` 插件, 貌似没有添加压缩选项, 里面的 `options` 不知道那里设置, 官方文档又神马都没写, 可以将 `node_modules/Hexo-renderer-less/index.js` 改写 `callback` 一行改成 `callback(null, tree.toCSS({compress: true}));`, 这样生成的 `css` 就会压缩了, 而 `jade` 默认压缩, 如果没有, 服务器基本上都做了 `gzip` 压缩, 这个可以忽视。~~

** [hexo-minifer](https://github.com/ChrisYip/hexo-minifier) plugin 可以完成以上任务鸟 **

``` js
var less = require('less'),
path = require('path');

hexo.extend.renderer.register('less', 'css', function(data, options, callback) {
  var parser = new(less.Parser)({
    paths: path.dirname(data.path),
    filename: path.basename(data.path)
  });

  parser.parse(data.text, function(err, tree) {
    if (err) return callback(err);
    callback(null, tree.toCSS({compress: true}));
  });
});
```

安装 `jade` 和 `less`

``` bash
cd Hexo/
npm install
```

### Config - 配置
通过修改 `theme/ishgo/_config.yml` 可以自定义博客
详细选项说明 [_config.yml](https://github.com/ishgo-team/hexo.ishgo/blob/master/_config.yml)

- site 网站相关设定
- menu 导航菜单
- sidebar 侧栏
- links 友情链接
- author 作者
- 其他选项


### 技术支持
最后感谢一些开源项目提供技术支持或服务托管等

- [Hexo](http://zespia.tw/Hexo/)
- [Bootstrap](http://getbootstrap.com/)
- [Font-Awesome](http://fortawesome.github.io/Font-Awesome/)
- [Nodejs](http://nodejs.org/)
- [Github](github.com)
- [jQuery](http://jquery.com/)
- [多说](http://www.duoshuo.com/)
- [jiathis](http://www.jiathis.com/)

### Update 2014-02-04
- 升级 bootstrap 3.0.0 至 3.1.0
- 升级 awesome-font 3.2.3 至 4.0.3
- 去除 jquery 和 juqery.prettify plugin
- 去除 hexo.ishgo/_config.yml 中某些选项
- 不再支持 ie7 和以下版本浏览器
- 添加 英文和繁体语言
- 网站样式总体进行修改
- 迁移 项目至 ishgo.team 下
- 修复 jade 版本升级带来某些编译失败
- 删除 ie7 版本下得所有样式
