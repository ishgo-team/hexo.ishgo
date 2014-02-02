# ishgo - 团队技术博客主题

Theme for [Hexo](http://zespia.tw/hexo/)

Demo: [http://blog.ishgo.cn/](http://blog.ishgo.cn/)

## Informations
此主题主要用于团队技术博客而非其他个人博客, 因为主要优化在 `Markdown` 的代码着色, 着色主要参考 `submit Text2` 的 `monokai colors scheme`。

支持自适应, 采用 `bootstapr 3.0` 版本, 以兼容 `ie7+` 的手脚架, 主要考虑以后 `bootstap` 有比较好的扩展性和代码规范。

与官方默认主题不同的是使用 `jade` 和 `less` 来打造前端, 而非 `ejs` 和 `styl`, 所以安装有点儿麻烦

如果用于团队请将博客整个共享, 保证代码版本统一。否则在版本更新阶段容易造成代码冲突。

本主题不支持 `ie6` 以下版本, 支持 [ie6nomore](http://www.ie6nomore.com/) 行动。IE6观看会跳到拒绝访问页面。

评论采用 `多说`, 侧栏的项目和评论数均由多说技术提供，已配置成本地与真实环境多说同步

可以添加新的文章属性
- `author` 作者, 根据 `ishgo/config.yml` 下的 `author` 进行查找, 如果显示相关信息。
- `hidden` 隐藏用于关于我们之类的文章, 在归档或目录下不会显示, 文章确实存在, 可直接不写。

    author: David
    hidden: false


## Install

打开 `hexo/_config.yml` 文件,
修改 `url` 成自己的博客地址, 不能为空,
修改 `plugins` 改成 `hexo-renderer-jade` 和 `hexo-renderer-less`,
修改 `theme` 属性改成 `ishgo`

    url: http://blog.ishgo.cn 
    
    plugins:
    - hexo-renderer-jade
    - hexo-renderer-less
    
    theme: ishgo
    
修改 `hexo/package.json` 的 `dependencies` 添加 `hexo-renderer-less` 和 `hexo-renderer-jade` 两项

    "dependencies": {
        "hexo-renderer-less": "*",
        "hexo-renderer-jade": "*"
    }

安装 `jade` 和 `less`

    cd hexo/
    npm install


## Config
通过修改 `theme/ishgo/_config.yml` 可以自定义博客
详细选项说明 [https://github.com/DavidKk/hexo.ishgo/blob/master/_config.yml](https://github.com/DavidKk/hexo.ishgo/blob/master/_config.yml)

- site 网站相关设定
- menu 导航菜单
- sidebar 侧栏
- links 友情链接
- author 作者
- 其他选项

```bash
    # 网站定义, 优先这里的定义, 如果没有会倒 hexo 根目录的 _config.yml 里面提取
    site:
        title: iShgo 团队博客
        subtitle: iShgo 团队博客
        description: iShgo 技术交流博客
        ico:
            ico/apple-touch-icon-144-precomposed.png:
                size: 144x144
                rel: apple-touch-icon-precomposed
            ico/apple-touch-icon-114-precomposed.png:
                size: 114x114
                rel: apple-touch-icon-precomposed
            ico/apple-touch-icon-72-precomposed.png:
                size: 72x72
                rel: apple-touch-icon-precomposed
            ico/apple-touch-icon-57-precomposed.png:
                rel: apple-touch-icon-precomposed
            ico/favicon.png:
                rel: shortcut icon
    
    # 导航菜单
    ## 导航栏名字在 languages 里面设置
    menu:
        home: /
        archives: /archives
        about: /about
    
    # 侧栏
    ## 侧栏项目是否开启
    ## author 作者信息
    ## 以下均是使用 `duosuo` 技术提供
    ## categories 文章分类
    ## dynamic 热门文章
    ## lively 最新动态
    ## visitors 最近访客
    sidebar:
        author: true
        categories: true
        dynamic: true
        lively: true
        visitors: true
    
    # 友情链接
    links:
        github:
            icon: icon-github
            url: https://github.com
            descript: github
    
        twitter:
            icon: icon-twitter
            url: https://twitter.com/twbootstrap
            descript: Twitter
    
        google_plus:
            icon: icon-google-plus
            url: https://plus.google.com/
            descript: Google+
    
    # 作者
    ## face         头像
    ## name         名字
    ## signature    个人签名
    ## profile      个人主页
    ## other        其他主页 必须对应下面 ico
    author:
        David:
            face: http://s.gravatar.com/avatar/53d03c1304a6ec5a3a92cdcdf5c7e7e3?s=200
            name: David
            signature: 不怕神一样的对手只怕猪一样的队友
            profile: https://github.com/DavidKk
            weibo: http://weibo.com/307853201
            twitter: https://twitter.com/Mr_DavidJones
            facebook: https://www.facebook.com/kk.cc.david
            google_plus: https://plus.google.com/111899862347999076942?rel=author
            github: https://github.com/DavidKk
    
        Barbery:
            face: http://tp1.sinaimg.cn/1763035100/180/1293205008/1
            name: Barbery
            signature: 加油!骚年~ 你的问题主要是读书不多,而想得太多(T_T)...
            profile: http://www.stutostu.com/?page_id=5
            weibo: http://weibo.com/stutostu
            github: https://github.com/Barbery
            google_plus: https://plus.google.com/111756747266879940955
    
    
    # 图标定义
    ## 使用 `Font-Awesome` icons
    ## 对应上面的其他主页必须定义才能显示, 否则不能显示
    ## 若要添加, 请自行添加特殊的 icons
    ico:
        weibo: icon-weibo
        twitter: icon-twitter
        facebook: icon-facebook
        google_plus: icon-google-plus
        github: icon-github
        bitbucket: icon-bitbucket
    
    #CDN
    cdn:
        jQuery: http://code.jquery.com/jquery.min.js
    
    # 代码着色
    prettify:
        enable: false
    
    # 多说评论
    duoshuo:
        enable: true
        id: blogishgo
    
    # jiathis分享
    jiathis:
        enable: true
        shareUID: 1832206
        uid: 1374060136495255
````
