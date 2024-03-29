hexo-theme-aria
===============

A Hexo theme inspired by Kalafina's song ARIA.
----------------------------------------------

[English README](README.md)

主题预览：[喵's StackHarbor](http://aria.ismyonly.one/)

![屏幕截图](ARIA.png)

# 捐助

作为一个学生，我没有能带来稳定收入的工作，我只是出于热爱占用我的空闲时间编写了这个主题。如果你喜欢它或者它和它的代码帮助到了你，你可以通过微信支付或者支付宝或者 PayPal 捐助我来支持我的开发，下面是我的二维码和链接：

- 微信支付

	![WeChatPay](https://sh.alynx.xyz/images/WeChatPay.png)

- 支付宝

	![AliPay](https://sh.alynx.xyz/images/AliPay.png)

- PayPal

	[点击这里](http://paypal.me/AlynxZhou)


# 主题特色

- 优雅的响应式双栏设计和 CSS 动画。

- 内置评论系统（目前支持 [Disqus](https://disqus.com/)、[commenjs](https://github.com/wzpan/comment.js) 以及 [Valine](https://valine.js.org/)）。（由于 HyperComments 转为必须付费，已经移除。）

- 不蒜子访问量计数。

- Hexo 搜索支持（通过安装 `hexo-generator-search` 并参照其 [说明文件](https://github.com/wzpan/hexo-generator-search) 进行配置来生成搜索索引）。

- 多语言支持（目前支持简体中文，繁体中文和英文，欢迎添加翻译）。

- [Lightgallery](https://sachinchoolur.github.io/lightgallery.js/) 实现的图片浏览。

- RSS 支持（安装 `hexo-generator-feed` 并参照其 [说明文件](https://github.com/hexojs/hexo-generator-feed) 进行配置来生成所需文件）。

- 自动转换 Markdown 格式的资源文件夹链接到绝对路径。（无需 `hexo-asset-image` 插件。）

# 使用前须知

- 使用静态网站生成器需要有一定的相关知识，如果您对这方面毫无了解，不建议使用 Hexo 和 ARIA 建站。请您确定您有基础的 Hexo、YAML、git、Markdown 和 Web 知识再继续。

- ARIA 使用了 [FlexBox 布局](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex) 来放置页面上的元素，但是 Internet Explorer 9 和更低的版本没有办法支持这个布局。所以如果你用 IE，请升级到 IE 11 或者更高的版本，或者使用诸如 [Google Chrome](https://www.google.com/intl/zh-CN_ALL/chrome/) 或者 [Mozilla Firefox](https://www.mozilla.org/zh-CN/firefox/) 这样的现代浏览器。如果你知道怎么在旧版 IE 里面回退 FlexBox 到替代的其它布局，请提交 PR，十分感谢。

# 使用说明

## 安装插件

首先进入你的 Hexo 站点目录。使用 `hexo-renderer-njucks` 而不是 `hexo-renderer-nunjucks`、`hexo-renderer-njk`、`hexo-renderer-njks`，后面三个已经无人维护，并且也不支持 Nunjucks 3。

```
$ npm install --save hexo-renderer-njucks hexo-renderer-stylus hexo-generator-search hexo-generator-feed
```

## 克隆仓库

把它克隆到 Hexo 站点下的 `themes/aria` 目录：

```
$ git clone https://github.com/AlynxZhou/hexo-theme-aria themes/aria
```

## 修改站点配置

下面的配置需要修改你 **站点的** `_config.yml`。

### 把主题修改为 `aria`

```yaml
theme: aria
```

### 语言设置

可以设置的值为 `zh_CN`、`zh_HK`、`zh_TW` 或 `en`。如果你从别的主题转移过来比如旧版本 NexT，请注意这里不是 `zh-Hans` 而是 `zh_CN`。`default` 是 `en` 的别名。

```yaml
language: zh_CN
```

### Hexo 搜索插件的配置

```yaml
# Hexo local search
search:
  path: search.xml
  field: all
```

### Hexo RSS 插件的配置

```yaml
# Hexo feed
feed:
  type: atom
  path: atom.xml
  limit: 20
  hub:
  content:
  content_limit: 140
  content_limit_delim: ' '
```

### 高亮设置

Hexo 内置的语法高亮功能使用了 highlight.js，但默认却没有给高亮的类名添加 `hljs-` 的前缀，而 highlight.js 项目提供的 CSS 文件却使用了这个前缀。为了保持和 highlight.js 项目 CSS 文件的兼容性，你需要像下面一样添加 `hljs: true` 到对应的配置里：

```yaml
highlight:
  enable: true
  hljs: true # 添加这一行！
  line_number: true
  auto_detect: true
  tab_replace:
```

## 复制 ARIA 配置

把 `_config.yml.example` 复制为 `_config.yml`：

```
$ cp themes/aria/_config.yml.example themes/aria/_config.yml
```

## 修改主题配置

下面的配置需要修改 ARIA 目录下的 **主题的** `_config.yml`，不需要修改所有的配置项，只要修改你需要的部分就可以了：

### 菜单设置

如果你想要启用“分类”和“标签”页面，取消注释 `categories` 和 `tags`，然后运行 `hexo new page categories` 和 `hexo new page tags` 生成这两个页面，最后分别把 `layout: categories` 和 `layout: tags` 添加到对应文件的文件头里。如果你想要启用“关于”页面，运行 `hexo new page about` 并取消注释即可：

```yaml
menu:
  - name: home
    link: /
    icon: <i class="fas fa-home"></i>
  - name: archives
    link: archives/
    icon: <i class="fas fa-archive"></i>
  - name: categories
    link: categories/
    icon: <i class="fas fa-th-list"></i>
  - name: tags
    link: tags/
    icon: <i class="fas fa-tags"></i>
  - name: about
    link: about/
    icon: <i class="fas fa-user-edit"></i>
```

### 生成 Favicon

首先准备好一张图片作为你想要的 favicon 的原图，然后访问 <https://realfavicongenerator.net/> 生成各种不同浏览器的 favicon，然后下载压缩包，解压到你站点目录下 `source/favicons` 目录里（没有则创建一个）。ARIA 会自动加载这些图标。

### 网站关键词

将 `keywords` 项设置为关键词列表。

### CreativeCommons 许可证

设置 `creative_commons` 项。为了保证美观，ARIA 会将链接显示在网站底部。可选的许可证有 `by`、`by-sa`、`by-nd`、`by-nc`、`by-nc-sa`、`by-nc-nd`，有关它们的区别参见 <https://creativecommons.org/licenses/>。

### 代码高亮主题

ARIA 内置了四种常见代码高亮主题，设置 `highlight` 项为 `atom-one-dark`、`atom-one-light`、`solarized-dark`、`solarized-light` 中的一个。ARIA 使用了 Hexo 内置的 highlight.js，因此如果你想添加更多的高亮主题，直接访问 [highlight.js 的样式仓库](https://github.com/isagalaev/highlight.js/tree/master/src/styles)，下载你需要的 CSS 文件到你站点的 `source/css/` 目录（也即在你存放 Markdown 文件的 `source/` 目录下面创建一个 `css/` 目录，你也可以把它放到主题的 `source/css/` 目录，但是这样会污染 git 工作区），然后设置这里的值为你下载的文件名（**不要** 添加`.css` 后缀，这个是自动添加的）。

### 自定义信息

`custom_info` 项的值会显示在网站底部，出于格式考虑请不要设置过长的字符串。

### 头像

设置 `avatar` 项为你头像的链接，例如设置 `avatar: images/myavatar.png`，则你需要把自己的头像放置到站点根目录下的 `source/images/myavatar.png`。

### 自定义 Logo

设置方法类似于头像，`logo` 项的值将会被显示在默认顶部 `ARIA` 的位置，或者如果你想隐藏 logo，把这一项留空。

### 自定义主题色

主题色 `color` 会被用于页眉和页脚的背景上，一些浏览器也会使用它来辅助变色，例如 Android 版 Chrome 的标题栏颜色，默认为网站的深色。由于颜色以 `#` 开头，需要加双引号以防止被作为 YAML 的注释。如果你没有特殊需求，最好不要修改这里的颜色。

### Google 页面验证

如果想把你的网站提交给 Google，需要证明你是此网站的所有者，当 Google 要求你验证时，选择“使用 <meta> 元标签”，复制 `content` 属性的值，填写到 `google_verification` 项，然后重新生成发布网站。

### 网站创建年份

将 `since` 值设为你网站的创建年份，如果留空或者填写年份与当前年份一致，网站底部只会显示当前年份，否则显示 `创建年份 - 当前年份`。

### 搜索设置

如果需要启用搜索，首先确保第一步中安装了 `hexo-generator-search`，并且按照第二步配置过了，然后将 `search` 设置为 `true`，搜索框会显示在侧边栏的上部。

### 侧边栏设置

有 `left`、`right` 和 `false` 三种选择，设置为 `false` 则不会显示侧边栏。

### 动画

将 `animate` 设置为 `true` 则会启用卡片的翻转动画效果（不建议启用，在某些浏览器和较低配置电脑上可能会导致卡顿）。

### 不蒜子计数

如果需要关闭不蒜子计数，将 `busuanzi` 设置为 `false`，否则在页面底部会显示 `站点访问次数`、`站点访问人数`、`页面访问次数`。

### MathJax 设置

[MathJax](https://www.mathjax.org/) 是一套用于在网页上显示数学公式和符号的 JavaScript 排版库，由于其体积较大，ARIA 没有内置，如果你有数学写作需要，首先设置 `mathjax` 下的 `enable` 为 `true`，然后将 `cdn` 项设置为你要使用的 MathJax CDN，然后在需要使用的页面添加文件头 `mathjax: true`。设置 `global` 为 `true` 可以在全部页面启用 MathJax，但可能会拖慢非数学页面的显示速度。

### 常用库 CDN

可以对 ARIA 内置的库使用 CDN 加速，首先将 `lib_cdn` 下的 `enable` 设置为 `true`，然后将 CDN 地址添加到配置中即可，如果你不了解自己在做什么，请直接跳过这部份。

### 社交链接

先将 `social` 下面 `enable` 设置为 `true`，然后在 `links` 下添加你的个人社交链接，格式如下：

```yaml
social:
  enable: true
  links:
    - name: 显示名称
      link: 网页地址
      icon: 你所使用的 Font Awesome 图标的 HTML 标签
    - name: 显示名称
      link: 网页地址
      icon: 你所使用的 Font Awesome 图标的 HTML 标签
```

前往 [Font Awesome](https://fontawesome.com/) 获取你想要的图标。

### 友情链接

先将 `blogroll` 下面的 `enable` 设置为 `true`，然后在 `links` 下添加友情链接，格式如下：

```yaml
blogroll:
  enable: true
  links:
    - name: 显示名称
      link: 网页地址
      icon: 你所使用的 Font Awesome 图标的 HTML 标签
    - name: 显示名称
      link: 网页地址
      icon: 你所使用的 Font Awesome 图标的 HTML 标签
```

前往 [Font Awesome](https://fontawesome.com/) 获取你想要的图标。

### 评论系统

首先将 `comment` 下 `enable` 设成 `true` 以全局启用评论（首页、归档、分类、标签页面除外），然后填入你的 Disqus Shortname。如果你有哪个页面想单独关闭评论，添加文件头 `comment: false` （`comment` 不是 `comments`！）。

如果你使用 commentjs，首先将它的 `enable` 设置成 `true`，然后根据你的网站页面存放位置设置 `type`，支持 `github` 和 `oschina`，`user` 是你在这些网站的用户名，`repo` 是你这个仓库的名字，`client_id` 和 `client_secret` 需要你去 [github](https://github.com/settings/applications/new) 或者 [oschina](https://git.oschina.net/oauth/applications/new) 生成一个应用，然后复制 Token。

如果你使用 Valine，首先设置 `api_id` 与 `api_key`，并将 `enable` 设置为 `true`，其它配置项参照 Valine 文档设置。

如果启用多个评论系统，默认只会显示顺序靠前的（顺序：Disqus，commentjs，Valine）。

Tips：如果想批量更改新生成的文件的文件头，编辑站点目录下 `scaffolds` 目录里的文件，Hexo 会把这个目录内的文件作为生成新文件时的模板。

### 打赏

将 `reward` 下 `enable` 设置为 `true` 启用打赏，然后在 `comment` 项设置你的打赏提示语，然后按需设置三种打赏方式的二维码（微信支付，支付宝，比特币），设置方式同头像，如果想关闭某一项留空即可。

### 自动截断摘要

如果你想自动生成首页的文章摘要，你可以使用这个选项。例如设置 `auto_excerpt: 200` 就会让主题截取文章的前 200 个字符（不含 HTML 标签）作为摘要。但是如果你想要更好的显示效果，建议你 **在想要的地方放置一个 `<!--more-->` 标签，在这个标签之前的文章内容会被作为文章的摘要**。

### 自定义字体

首先将 `custom_font` 下面的 `enable` 为 `true`，然后去提供网页字体服务的网站比如 [Google Fonts](https://fonts.google.com/)（如果你不能访问，找个替代品），然后选择所有你需要的字体，把生成的 `<link>` 标签里面的 `href` 属性网址复制出来粘贴到 `link` 选项下面。然后给不同的部分设置不同的字体。

示例如下：

```yaml
custom_font:
  enable: true
  link: //fonts.googleapis.com/css?family=Lato|Roboto+Condensed|Skranji|Ubuntu|Ubuntu+Mono
  all: Ubuntu # <body> 的字体。
  title: Roboto Condensed # 标题字体。
  subtitle: Roboto Condensed # 副标题字体。
  main: Ubuntu # 主要部份字体（菜单以下页脚以上）。
  code: Ubuntu Mono # 代码字体。
```

## 内置写作样式

Markdown 会被编译成 HTML，所以你可以直接在有效的 Markdown 文件里面写 HTML 代码。为了能更好地组织文章结构，主题内置了一些自定义样式类，可以在写作时使用。

### 居中引用

只要给你的 HTML 代码添加 `.centerquote` 这个类，你就能得到一个有上下边框的居中引用。推荐给 `<blockquote></blockquote>` 标签使用这个类：

```HTML
<blockquote class="centerquote">居中引用样例</blockquote>
```

看起来像这样：

![居中引用样例][centerquote-example]

### 彩色警告块

只要给你的 HTML 代码添加 `.alert-red`, `.alert-green` 或 `.alert-blue`：

```HTML
<div class="alert-red">红色警告块样例</div>
<div class="alert-green">绿色警告块样例</div>
<div class="alert-blue">蓝色警告块样例</div>
```

看起来像这样：

![警告块样例][alert-example]

## 自定义 CSS 和 JavaScript

如果你需要用自定义的 CSS 覆盖 ARIA 内置的 CSS 样式，可以编辑 `themes/aria/source/css/custom.styl`，这个文件会被最后加载。

如果你需要使用自定义的 JavaScript，可以编辑 `themes/aria/source/js/custom.js`，这个文件会被最后加载。

## 更新主题

如果你使用了自定义的 CSS 或 JavaScript，更新之前请先用 Git 把它们提交。只有工作区干净的时候才能进行拉取

然后使用 `git pull` 拉取最新的更新，如果有冲突请手动合并提交。

每次更新完了不要忘记对比 `_config.yml` 和 `_config.yml.example`，并手动将 example 中的更改应用到你自己的配置中。

# 开源许可证

Apache-2.0

# 特别注意

我给这个主题定下的目标是精简的配置和优雅的样式。如果你需要某种功能的话你可以修改它然后提一个 Pull Request，如果这些功能很有用我会很快合并。然而有些主题走了极端，它们要么号称自己“简洁/更简洁/最简洁”但实际上是简陋，要么是给自己塞了一大堆功能和乱七八糟的配置，其中有些是大部分用户不会用到或者使用默认值的，我不想要这样的功能。

例如说我只打算给这个主题添加 Hexo 本地搜索（这个插件生成一个索引文件然后用主题内部的 JavaScript 就可以查询而不需要购买数据库服务）因为它很容易就能工作。真的有人会去付费使用 Swift 搜索或者 Algolia 嘛？所以最好不要给我提比如 *我添加了 Swift 搜索然后就让一些新来的用这个然后去掏钱吧反正他们什么都不懂！* 因为我还觉得本地搜索更容易用呢！如果你不喜欢本地搜索关了它就得了（你就这么痛恨一个不需要额外代价的网页上的搜索框？）。

哦对了也别给我提类似 *我添加了一个配置项让用户选择他们的头像显示成方形而不是圆形！*，就算我们能把头像设置成从 **三角形** 到 **正十七边形** 又能有什么用？我们真的需要在一个主题里塞进去六个或者更多个不同的方案？如果你想，你可以 fork 一个你自己的，但我更愿意把他们拆成六个单独的主题。这能让开发者更容易知道该在哪修改代码而不是在一堆毫无关系的方案代码比如说 `{% if schemeA %}{{ xxxxxxxxxblockxxxxxXXXXXxxxxx }}{% elif schemeB %}{{ xxxxxxxspanxxxxximgxxxxx }}{% endif %}` 或 `if (hexo-config(schemeA)) { .cls { a { &:hover { background: #333; } } } }` 中寻找 bug，我曾经在这里面找过所以我知道这玩意有多么辣眼睛……

最后，如果你想添加评论系统，尽量选用户多的比如 Gitment 或者 Valine 或 LiveRe，别再添加 多说 或者 畅言 或者 网易云跟帖 之类的因为它们有的已经倒闭了有的配置起来能迷倒一头大象或者要你把你的隐私备案到某些“其他国家”的政府。我想让 ARIA 变的很容易使用，而不是成为一堆没必要的选择的组合体。如果 85% 以上的用户都不需要一个自定义设置，那就把它写进代码里而不是配置文件里。

[centerquote-example]: data:image/png;base64,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AA7SkiVL+mTd2bNn57zzzutyzHvvvVfupPzJT36S2traLsc/+uijeffdd7tdu6mpab/th7tSKpUKjfuia9vqt83nn3+eV199NUly5plnlreJPuWUUzJixIhcfPHFHc7T0tKSp59+unxfZ0HqlClTOnz/rbfeKm8pXFFRccD1hoaGcoezgBUAAODwEbACAAAcpKlTp6Zfv+7/rNq0aVMaGhpSW1ubcePGdTm2f//+3c5XW1vbaQjXpn0IOmnSpIwdO7bL8UOGDOl23SR5/vnnc//99xcae7jt2rUrH330UYfXmpubC41L9oXGXampqckPf/jD8s8rV64sB6zz58/PV77ylf3Gd3aeanNzczlgnTt3bk4//fQu122vVCrloYce6nLM6tWry2f0/u53v9svhG1pacmpp55aPpcWAACAgydgBQAAOEhXXXVVuXuxK7fcckvWrVuX6dOn54orrjgClR0+//nPf/q6hLK//OUvhcbde++9+52heqjeeeed8usXXnhhv/D1cPn73/+ezZs3dzlm1apV5dcdhca7d+/u9boAAAC+jASsAAAAPdDWIZh0vE3rsa4tYK2vr8/3vve9QvcU7Y49Wvzzn/8sv37++edTX1+fqVOnHrb1tm7dmgcffDBJUl1dncbGxgPGNDY2Zu3atUmS73//+/t11b744ov5xz/+kdGjRx+2GgEAAL5MBKwAAAA90H7r2crKyj6s5Mhrbm7Oli1bkiSTJ0/OyJEj+7SeRYsW5bTTTuvwWnNzc2688cYkyQ9+8INMnz6903mampqyePHiQmtu2bIlW7du3e+9P//5z7nxxhvL2zu3tLRk165dB9y7d+/e8uvdu3dnx44dB4yprq7OwIED93vvgQceSFNTUwYPHpxvfvObHW4V/PLLL6exsTHDhg3LN77xjf1+N5cuXZoknZ75CgAAQM8IWAEAAHqgpaWl/Pq2224rFLL+97//TbJvC9e2gLIrAwcOzNVXX33wRR4m77//fvn5x48f38fV7OuM7SzkbR+EdzUuSYcdoZ15/fXX9/v5jDPOyMqVK/Pwww/nsssuS7Lv+77pppu6nOfOO+/s8P1vfetb5XnazJw5M2+++WYWLVqUPXv2HHBPqVTKsmXLkiTnnHPOAb+T//73v5N8Mb4zAACAY4GAFQAAoAfaB3fr1q3r0b07duzosGvxfxU517UvtD9/9YQTTuiTGtpv0dwXHcSvvfZaKioqUiqVkiTz5s3LunXr8swzz2TWrFmZPHlyr685Z86cbN26NbNmzcry5csPuL5mzZpycH/uuefud23Pnj356KOPkuSw1AYAAPBlJGAFAADogaampiT7tnItegbps88+m23btuWUU05JfX19t+P79fti/qnWFrAOHjw4w4YN65Ma2m+z27Yl75GyadOmbNmyJdOmTSufwzpw4MB8+9vfzpIlS3Lffffll7/8ZSZMmJCbb775gPv37t2bX/3qV0mSn/70p6mrqztgTEfPVFVVlYULF3ZYU3Nzc+67774k+zpd/7dTd/369UmS4cOHZ/jw4T14WgAAADrzxfyrHQAA4AuqrQO1trY2X//61wvds2LFimzbti3jx48vfE9Xtm/fXg74OtO2LXGSbNy4sdvO2U8//bTbddsC1t27d+faa68tUOk+CxYsyPz58wuP70pfBqzPPvtskuTss8/e7/O/8MILs3Tp0ixYsCDJvkB06NChB9zfvvu5pqamwzE99fjjj2fbtm2pqqrKpZdemkcffTSjR4/OnDlzkiRvvvlmkuTkk08+5LUAAADYR8AKAADQAzt37kySXgnHDtbrr79+wFmgXbnrrrsOec1SqbRfaNs+LOxOb2553NZBnCTLli3LG2+80eG49mflvvTSS9m4cWOncxZ5lk8++SQrVqzIkCFDcuqpp+53rbq6OjfccENGjBjR7Ty9re3zmDdvXnbu3JlHHnkkyb5u28suuyyrV69OkkyfPv2I1wYAAHCsErACAAD0QFsnaF9tkdtXWltbc80116SysrLQ2ad79uzJrbfemmRft29vaTtPNEnhkHnt2rVZu3btIa375JNPprW1NXPmzOnw+fsiXE2SSy+9NOPHj8+MGTMyYMCAXHzxxXniiSeybNmyvPPOO9m5c2cqKipy2mmn9Ul9AAAAxyIBKwAAQA+0Baztz7p84YUX8swzz3R6z8cff5wkeeWVV7rc2nfu3Lm56KKLuq1h3rx5ueSSS7ocs3r16txxxx1JkhtuuCFjxozpcvxdd92VlStXdnq9qqoq06ZN67a2Nm3bCSe9Gz5u3749SVJZWZmvfvWrnY5rbW0th6oTJ07s8vzR9mM7snnz5jz33HOpqKjIueee2+m4Dz74IBs2bOj0evuu2rVr15a7oTsyc+bMwp2/X/va18qvFy5cmDFjxuTuu+/Oli1bkiR1dXUZNGhQobkAAADonoAVAACgoMbGxnJoNWHChPL7n332Wfn9ruzZsyd79uzp9PquXbsK1XHcccdl4MCBXY5pfz7pgAEDuh0/dOjQDB8+vNe2823fadqbAeuHH36YJBk3blx+9rOfdTquubm5fE7sxRdfnPr6+k7HNjY25rrrruv0+pIlS9La2prZs2dn3Lhx2b17d4fj3n333dxzzz1FHiPLli3r8vrEiRMP+ruYO3duampq8oc//CFJcv755x/UPAAAAHRMwAoAAFDQpk2b0tramiQZP378AddHjx6dK6+8ssfz3nPPPYUC2l/84hcplUqpqqrq8RrdWbRoURYtWtRr87UFrEXC3Z5o64zt6PM/XOrq6rJmzZpuu4YHDx68X/D+v0qlUjZv3pxkXwd0V59L+4D8YLz33ntJ9m1l3dH5qzNmzEipVMqAAQMOaR0AAIAvIwErAABAQevWrUuS9OvXL8cff/wB16urq3u0jW6bogHkoYZuR1JbwNqb3auff/55eYvlSZMm9dq83bngggvS1NTU4XfeXn19fZedsu27aq+44oqcfvrpvVpnm48//rjcITt//vwOA/mrr776sKwNAADwZVDZ1wUAAAAcLdq6AqdOnXpYukiPJW0Ba21tba/NuXr16jQ3NyfJYQsnO9KvX7/Mnz//iK13KEqlUu666640Nzdn1KhRtgcGAAA4DASsAAAABTQ0NGTDhg1JkpkzZ/ZxNV98bVvh9mYH68qVK5Mkxx9/fLfdpF9WzzzzTLnL9/LLL/cfAQAAAA4DASsAAEABL7/8crl7sqMzLfl/W7duzYcffpik97by3bp1azlgPe+883plzmPNihUr8sADDyRJzj333MyYMaOPKwIAADg2OYMVAACgGy0tLeUzLadOnZrhw4d3OG7btm25+eabezz/+++/f0j19YXW1tasX78+/fv3T//+/XPcccelf//++fzzz3PvvfeWx9XV1fXKen/961/T2tqagQMHHtK2ty0tLamsrExFRUX5vbYwOCl+Hu4Xzauvvpo777wzpVIpEydOzOWXX97l+IaGhjQ1NaWqqioVFRVpaWnJzp07kyQDBgw4EiUDAAActQSsAAAA3XjuuefKIdyCBQs6HdfU1FQ+p/VYV1lZmccee6y8HW1HTj/99IwaNeqQ11q2bFneeuutJMlFF110SAHgrbfemrfffjtJUlFRkcrKyrS0tJR/Hj9+/CHXe6Q98sgjefTRR5Ps2z755z//eaqrq7u8Z/Xq1fnTn/7U4bUTTjih12sEAAA4lghYAQAAulFVVZXq6upMnjw5U6ZM6XRcbW1tLr300h7P/9BDD+3XRXm0qK+v7zRgnTZtWn70ox/1yjo1NTWpqqrKpEmTctFFFx3SXGeddVY5YC2VSuVwdeDAgbnkkku6DSa/iKZPn54nn3wyEyZMyNVXX50hQ4YUuqdfv37lba+TZPjw4Zk9e3YmT558OMsFAAA46lWUSqVSXxcBAADwRbdjx47s2bMn48aNO+Daxo0bs27dugwdOjRz587t8dwrV67Mrl27MmHChJx00km9UW4+/PDDctfn2WefnZqaml6Zt72mpqZ88sknaW1tLf8rlUoZOXJkBg0aVGiOlpaWPP3000mSmTNnZuzYsR2OW79+fWprazNy5MhC85ZKpWzfvj1JMnTo0HJw2tTUlI0bN5a7V6uqqjJy5MgMGzas0LxJsnfv3jz//PNJkjlz5mTw4MGF7mttbS1vNT1jxoyD6u7dsmVL1q1bl5qamtTX15ff37BhQ0488cT061f8/1F/8MEHKZVK6devXwYNGlT4OwMAAPiyE7ACAAAAAAAAFFTZ1wUAAAAAAAAAHC0ErAAAAAAAAAAFCVgBAAAAAAAAChKwAgAAAAAAABQkYAUAAAAAAAAoSMAKAAAAAAAAUJCAFQAAAAAAAKAgASsAAAAAAABAQQJWAAAAAAAAgIIErAAAAAAAAAAFCVgBAAAAAAAAChKwAgAAAAAAABQkYAUAAAAAAAAoSMAKAAAAAAAAUJCAFQAAAAAAAKAgASsAAAAAAABAQQJWAAAAAAAAgIIErAAAAAAAAAAFCVgBAAAAAAAAChKwAgAAAAAAABQkYAUAAAAAAAAoSMAKAAAAAAAAUJCAFQAAAAAAAKCgfn2x6IoVK/piWQAAAAAAAOAYNGvWrCO2lg5WAAAAAAAAgIIErAAAAAAAAAAFCVgBAAAAAAAAChKwAgAAAAAAABQkYAUAAAAAAAAoqKJUKpX6uggAAAAAAACAo4EOVgAAAAAAAICCBKwAAAAAAAAABQlYAQAAAAAAAAoSsAIAAAAAAAAU9H84OpX3pHX8aAAAAABJRU5ErkJggg==

[alert-example]: data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAB1oAAAFUCAYAAACN7j5FAAAABHNCSVQICAgIfAhkiAAAABl0RVh0U29mdHdhcmUAZ25vbWUtc2NyZWVuc2hvdO8Dvz4AACAASURBVHic7N1nYFRVwsbxJ8mkTHolCb036SC9VysIVqwo6trL6mtZXRuuiu6irGJFRQUEpCMivdcASxcIPYEACSG9TH0/BIYMkwmZgETI//fp3tNv4pf4cM7xstvtdgEAAAAAAAAAAAAAysy7ohcAAAAAAAAAAAAAAFcaglYAAAAAAAAAAAAA8BBBKwAAAAAAAAAAAAB4iKAVAAAAAAAAAAAAADxE0AoAAAAAAAAAAAAAHiJoBQAAAAAAAAAAAAAPEbQCAAAAAAAAAAAAgIcIWgEAAAAAAAAAAADAQwStAAAAAAAAAAAAAOAhglYAAAAAAAAAAAAA8JChohdgy86R5WSarDm5suflV/RyAAAAAAAAAAAAAPxFeQca5R0cJEOVaHmHBFfoWrzsdru9Qma2WmU6eESW1FMVMj0AAAAAAAAAAACAK5chJkp+dWpKPj4VMn+FHR1ceICQFQAAAAAAAAAAAED5WFJPqfDgkQqbv0KODramZ8iadiZk9ZJ8jEbJ1yB5c2UsAAAAAAAAAAAAADdsNslskTU/X7JL1tRTskZGyCcy/LIvpUKSTfPxk+cWEGCU/P0IWQEAAAAAAAAAAACUzttb8veTtzHAUWQplj1e1qVUxKT2ggLHs5dfhWyqBQAAAAAAAAAAAHCF8vL1dTzbCgorZA0VE7QWmoqtgJ2sAAAAAAAAAAAAADxQLGO0F1aioBUAAAAAAAAAAAAArmQErQAAAAAAAAAAAADgIYJWAAAAAAAAAAAAAPAQQSsAAAAAAAAAAAAAeIigFQAAAAAAAAAAAAA8RNAKAAAAAAAAAAAAAB4iaAUAAAAAAAAAAAAADxG0AgAAAAAAAAAAAICHCFoBAAAAAAAAAAAAwEMErQAAAAAAAAAAAADgIYJWAAAAAAAAAAAAAPAQQSsAAAAAAAAAAAAAeIigFQAAAAAAAAAAAAA8RNAKAAAAAAAAAAAAAB4iaAUAAAAAAAAAAAAADxG0AgAAAAAAAAAAAICHCFoBAAAAAAAAAAAAwEMErQAAAAAAAAAAAADgIYJWAAAAAAAAAAAAAPAQQSsAAAAAAAAAAAAAeIigFQAAAAAAAAAAAAA85PPWW2+9dbknNScfczx7GwMu9/QAAAAAIElK2b9f62b9qqjq1RQQFFiha7GYzJrw9r+UnZ6uqOpV5ef/5/2ttGf9Bs35/EvlZWSqZtMmjvI5Y77QmpmzFV+3joIjIkrsO/vTMTq4bYfi69eRX8DFrdFUUKDty1fKPzBQxuBgl/oNv/6mOZ9+oS1LlqpN/74XNVdxJw8d0c5Vq3Xq6DHF1qldpj5pycn636IlOr7/gKo1bHBR8xfk5GrsC69o47z5qt2imQJDQ13aFObladuy5SrMy1N4bJVSx7OazZo44j3lZWYrPLaK/Mrwd/aJg4e1aup0eft4KyIurtzfUtzSiZO16fcF8gvwV2TV+EsyJgAAAACUxl5Q6Hj2rVH1ss9vuOwzAgAAAMBfxNIJk7Vj5SqtmDJV//fTdwqNjq6wtSyfPEV/rF2nPRsS1OjatgoKDbtkYxfk5GpvwkbHe+LmLUpM2CSryayQyEhH+e71CTqdclw1GjXSyUNHJEm+/v5q0rmjJOnk4SNaN3uuQqMi1f/B+y96XTuWr9TUf38sSXr6y08VX6+eU31mapqO7N4tvwDjRc9V3KEdOzRz9GeKqVFdLXr1KFOfY4n7NfeLrxUUGqr2N91wUfNbbRYd2b1bkmQuLCixzaz/jtGWxUsVHhurZ78eI/9A9/8QYMfK1dq1eq12rV6rkMhIXdOt8wXXsH3FSq2YMlWJGzfp6a/GlO9DzpOYkKBDO3Ypvl5d1W/b5pKMCQAAAAB/ZQStAAAAACqlk4eLdjVKUstePSo0ZE1LTtayn6dIkjoOvEkxNWu6bWu32WS1WGXw8y3z+JmpaZr03kiX8gNbt+nA1m0u5UvGT3Q8h0VHO4LWlVOnS5Kadeuq3KzsUucMDAmWj2/pa0z47XdJUq2mTVxC1squ/0PDtGv1WmWcOKH5343TwKeecNt2zYxZkqTqjRuWKWSVpF2r10qSWvbupTUzZum3r8aWqV/bAf00+PlnytQWAAAAAK52BK0AAAAAKqXlP0+R3W6Xj8GgPvff41S3acEibV6wqNxjR8TF6rYXny9TW4vJrKkjR8lqNksqCs3OBmfuRFaL112vvKTqjRuVaY7IqnF67L+jHO+7Vq3RiilT1aRTR/UYeoejfNpHo5SalKxBTz+h+Ab1JUkGQ1FYeixxvzbPX1i0xpmztWbm7FLnfPTjj1S72TVu64/uTdThXX9IkjoMvKlM31GZhFeJUa97h2r+2O+1fvZcdb5lkKKrV3Npd3DrdiXt3iNJGvDQsDKNfTolRccPHpQktejdUztXrpLNai1TX7vdLknKzcqUJBmDguXt41OmvgAAAABwtSFoBQAAAFDppB9N0ZalyyRJ1954ncsdlRknTuhgCTs9yyovs1aZ284YNdpxjGxZpR9N0cmkpDIHrb7+/qrZpLEkafe69dq2dJnqtGiuXnff6TTG9Y8OV25Wthq2a6uQyHN3tFoKTZr+n09kt9sVHhOtuq1bOY2fl5ml3es3yNtgUKtePSQvLwWHh5e6pkU/jJck+QUYFVOzhk4cPOzSJicjQ5Jks1tLrD+fX6BRERe4z/RK0mnQzVoxearys7O1bNKUEsP7+WO/lyTVb9Na9c77vbizaX7RPyKo07KFwmOi1ax7V8XXL9pRnJ12SpPf/1CSNPT1VxUU4fx7DD3z38X7d9wrm9Wq57/7SjE1apTvAwEAAADgCkfQCgAAAKDSWTppiuw2m/wCAtTr7qEu9dUaNnB7D2fy7j06tm+/JOnaG66Tl7e3S5vQqEiXspIsGf+z/rd4iSSp7wP3qVWvnm7bphw4qInvvie7zabWfXqrTb++ZZqjOKvJpF+//FoZqWkyhoZq1bQZJbZLPHOf6zXduqh5926aOfpTHdtf9M05mZnqffdQRVaLd7Sf9/VY7V6/Qa369CrTTt4jf+zWng0JkiRTQb7GPFH6UbSWQpNGP/r4Bcdt2qWj7n3rjQu2K01hXq52rFrrUp58Zteo2WTWplJ2O7fs0V0Gf7+LWsNZfgEB6nDjdVozc458/fxd6neuXOMI6fs/9ECZxrRZLEqYN1+S1Kp30f20YdHRCjtzdPb2FSslScER4Wreo9tFfwMAAAAAXM0IWgEAAABUKsl79mrz/AWSpB533eG0c9Nus8nL21uNO7RX4w7tS+y/8PsfHUHroGeeLPexqWtmztaiH36SJHUceKN63+sa+J5VkJOred9+K7vNppga1TXwGff3dZZm2eRflH40RWHR0fL19VPG8ZMltks/nqKcjExVrV9fM0aN1uaFixUSEaEWvXpq9fQZmvnpGD343jvy8vZWVlqa1s2eK0nqfvutF1yDzWLRrNGflWv9l0Pu6SxN+2iU23pTQX6p9Q3btVXIeUFrfla2fv38K8e72WRyPC/49gcFhoZKkuq1baUajRpq4bjx5/rmZKtGk8bKzcjQxHfecxr3yB9FRy/7BRi1YvJUR3mTLh3Vuk/vEte3a916Zaeny8dgULOuXV3qk84c51y7WTO33wgAAAAAKELQCgAAAKDSsFmtmvnJp7Lb7apar5563Hmboy559x5NGfkfDXzqcdVv2/pPXcfiHydo8U8TJElNu3TSzU+6361pNZk08d33lX40RSERERr23jvyDwz0eM7NCxdp8Y8T5OPrq8HPP6OwmBiXNlFV42Xw99PP776v7ctXysfXoNSkJBlDQvTgyHdVpWZNHdqxQ/s2bdavX3ylAcMf1Pi3RshcWKg2/fqoSq2aF1zH8slTlbL/gCTpnjde1zXdOrttu/D7H7V04iT5BRj11pxpHn/zWZZCk7LSTjnezx5JbLFYlH40xVEeFBEmL4OP027ds0x5+co5nSEvLy9FVHU+atpmtijjZKrb+U2mQsfO5fPtObN7WJL8gwMVGR+vHStXle3Dzo5fkO/UJ6pqVbdtV00u+jlGxMXJGBriUn9kZ9EO2VrNmnq0BgAAAACojAhaAQAAAFQaa2bO1rF9++VtMOjW/3tO3oaiP4lsVqtmfPKp0pKTNeHtd/XiT98qKKz0O0bLw2o269cvvtb6OUU7QGs2aaw7X32pxOOHpaLdnz+/N1L7Nm2Wv9GoB/71jst9smWxduYczRnzhWMN414r+XjdJ8eMVrWGDZSTflqSFFurpjoN/ECnT5xUVLWi8O6uf7ysL57+u9bOnKO9Gzbp1LFjiq9XVwOfefKC6ziwbbuWjJ8oqeiY39JC1kspOTFRXz//fy7lp1OO69/Dhjveb3/lRbXu01svjvvWpe22pcs16b2RCgwJcalPP5riNM75/PwDnI6iLszL09YlyyRJzbp1VWBY0Y7W2tdco7DoaPW4844Sx7HZLFr5y3RHP3eBap0WJe9G/WPtOsdRw15ervX5WdlKTkwsWkuza9x+DwAAAACgCEErAAAAgErh5OEjWjSu6KjeXnffqfh69Rx1q6fPcuyyvOmJv/0pIWtqUpKmvP+Rjibuc5Qd3bdf/7rtbrd9bHarLIVFx8yaCgv19d9fKnWO/g/dr86DB7mUN+ncUVsXL1XbG/prxqj/qk3/vupd7G7aJRN/1uZi945mnwlagyLC5W0wOEJWSYqqVlX9H7pfM0d/plPHjkmSBj//jPwCAkpdW2pSkia8NUJWi0XB4WEa+PSFg9mrhTEkWLc8+5TjfefKNY6gtefQO1W1QT2n9gMeHlbiOBaT2RG0thnQ1+3x1iWx2+1a+P1PpbbZnZAgm9UqSfrmhZclnUtjbTaL6rdpo/tHvFnmOQEAAADgakfQCgAAAOCql34sRePfelemggIFhoQqulo1rZ05R9npp5SVflo7lq+UVHSMb9vr+l/y+f9Ys06T3hspc2GhJMnfaFRhfr6sZrOsZnOZxrDbbDIV5JfaxmqxllgeXiVGj306SqlJSZIkY1Cw0/G4xqBgx7PNYlFmWpokKTg8wmmcrLQ0LfpxgjbNX+hU/u1L/1CPoXeo6+BbZDjvftKzAoKC1aRjB21ZulxDX/+HQqOiSv2WS6l6gwZOu1C3LF2qRT+MV0R8nIa//y9HeVBE2GVZz77/bXE8b/htnlMI+2dZN+tXHT94sNQ2f6xe53g2FRS41OdnZV3ydQEAAADAlYygFQAAAMBVb/6345SWnCxJysvO0uT3P3RpExIRocHPP/2nzB8ZHyeL2SwvLy/1vu9u2W12LRk/UZHV4jXk78+57Tfto1E6ffyErr3hOrXs08ttu8nvfqDs06fLvJ51v87VpoXnwlLzmV2zdrtdu9cnyFxYqIgqVRQSGSGryaSda9Zpy6Il2rtxk2xWq/wDA9XnvrvVrHs3zft6rLYvX6kF347T2hmz1aJHdzXr0VU1mzaRV7HzaUMiI3TbSy+o//BhlzVklSSDv59TsBwcXrRj2WAwlHgfa0lsNlvRQ0ln7npof/Gg9dff1KJnd9Vt2eKix3UnLTlZv4/9TtK5kP98pvx87U3YJEm64bFHVLVBfUfd5nnztXnREkXGl+1nBQAAAACVBUErAAAAgKte817dtX1F0a5VY0iIImKrKCIuVod37lLO6QxJ0pAXn/tTjgyWpNg6tdXzrttVu3kzNWjXVot/miBJ8g8wqm6L5m77nT2ON7JqXKntfPxK3kXqTp0WzdWyd0+nsl2r1+iLp5+X3W6XJF3TrbNyMzNktVi1auo0Je9JVEBwkNr07aMed92hkKhISdLQ119V67699fvY73Xy8BGtnjFTq2fM1J2vvuQ0xwdD71Oehzsiz+7QNRXk640bXY9ELs3rUyfJz2j0qE9pzKai3ci+bnbsllVqUpIj9D9r+sej9exXn8vX319S0T26OZmZLn2thed2P+dmZjl2HhfnH2BUQHCQU9m8b76TubBQQaGh6nzrYC38/geXfpsXLJapIF+hUZHqfMtAefv4OOrWzpglSWUOpQEAAACgsiBoBQAAAHDVa9y+ve575w3Vad7cEUL9b/ES7Vy1RpLU9bbBatT+2j91Df0efOBPHb8sIqrE6skxoxUUHq7wKjFOdVHxcTIGFx0hHBkfr/SUFP3rtrvVtEsn3fXqKzq4bZua9+pR4l2sjTt2UOOOHXR45y4lzJsvb29vlyDXajLLYirbMckluZi+l4Ipr2gXqMHP/6LG2bZshdN7s65dtGPVai0c96Nu+NsjkqTjBw9pzJPPljrOtI9GlVje7fYhuv7Rh53KmnbqqD/WrNPAZ55UYW6eSx+73a61s2ZLktoO6O8UskrSsX37JUlxteuUuiYAAAAAqGwIWgEAAABc9Qx+vmrSqaPjPWn3Hs0YNVqS1KRzR13/yPCKWtplY8rPl81qU1TVqpKkgpxcp/q4OnV00+N/c7wfTUzU5gWLtGv1WrW/4Xpd062rbBarS7/iYmvV0k2PPSpvg49L3d1vvCab1XKJvubCDB7u8pWK7sHNOJlaYl3WqVOSJG8fb50+fsKpLuPUuZ2lmampsphMCgoPKzGU3rZ0uby8vBw7hzsNHqQDW7dr9fRZat6ju2o0buTxui+kdd/eSks+puY9umnjb/Nd6vdsSFBqUtEu23bXO99RXJCT6/jeGk0aXvK1AQAAAMCVjKAVAAAAQKWSmZam8W+OkMVkVrWGDXTnqy/Jy9u7opf1p/vpzRFOd4N6Ytxrb3jUvkXP7rrrtVecyuq0dH/08V9FTkamPrrvwVLbnDx8pNQ2nz9VdOfuXf94WS169XCqS9q9R6lJyarXupXjdxEQZFTXO4ZowbfjNPfzr/TYf0cpvm4dvTp5gsvYFpPJMfftL7+o+m1au7TxC3ANmL0NBg14eFiJ67WYzJr7+deSpKZdOikiLs6p/uD27ZKksOhohUZHu/1uAAAAAKiMCFoBAAAAVBqm/HyNf3OEstPTFVGliu5/580Sdx1eLuZCk04cPOy+3mySJOWcyii1nc1y4WN1m3XtrLjatT1eY3nEN6h7Wea50qyZPlOS1LpfH6fQu/Ogm7V2xmz1ue8eSUXBaEhkhEv/4scnG0OCS2zjqeWTpujUsWPyMRh0/SPDtfinCYqsGq/WfXpLknavXS9JqtWs6UXPBQAAAABXG4JWAAAAAJWCKT9fP7z2po7uTZTB30/XPTpcRxMTlb7iuNKPpSg95bhOpaTIGBikxz4t+f7LSy0tOVmjH338gu1Wz5ip1TNmXtRcHQbe5PRemJcnu81+UWOe5eUt+QcGedRn1n8/l91uuyTzS1LHgTcqrk757xA15efLYjLpxXHfutRZrWaNefI5mQoKHGV9H7hXrXr1cjteUESY03tGapq2r1il4IhwNWjbxqnOz2jU4599ovCYy79j1FRY9E2dhwxS1ql0Lf6xaCdt8u49uuGR4dqzIUGS1Khj+8u+NgAAAAD4qyNoBQAAAHDVO7Jrt6aP+kQnDx+RJFkKTfr53fdLbBtTs8blXFqF+eG1N3Rox65LMlZktfgSA8rSJPw2Tzar9ZLML0mNO7YvV9CampSk9XN+0+YFC9Wmfz/d9MTfXNrs/98WR8jasH077d2wUbvXb1Dve+8u8zwrp/wim9WqVr17ytvgelR1RYSsknT9I8MVW7u2mnbuJP9Ao3redbuWTfpFa2fO0b7NW5R1Kl1e3t5qdG27ClkfAAAAAPyVEbQCAAAAuOplpqU6QtbifP39FVOjumJr1VJ0zRqKrVlDsXVqX7Z1ValVU8M/LDnw9cQXTz2rjNQ0j/r0umeocjIzL3puSfIPMJa7b+1mTRVdo3zhtrmwUFuXLCv33GlHj+njh84FqyX9NyJJO1etliRFxMfp5ice0382PKzk3Xt1NHGfqjWof8F5Thw8pPVzfpOXl5faXX+d23YnDx3RkV1/uK23Wi2O58SNm5Rz6rTbtk26dFBQWPgF1yZJbfr1cTz3H/6goqtX14xPPlXqkSRJUr3WrRQYGlqmsQAAAACgMiFoBQAAAHDVa9Kxo0KjoxRbp7bqtmyhuDq1VaVmDYXHxsrLy6vC1uXj5i5OT3W5bYgKcnNV85omZe7jZzTKeIl2lPr5+5e7b5t+/dTuhgHl6pudftqjoPX0iZPaPH+hEub9Lkmy24qOLo6vW0ddb79VLXp0c+mTm5WprUuXS5KadeuiqGpVVbdVSx3YslVrp8/UbS+/eMF5fx/7fdFu1j69VKVWTeVmlRxwH9i6VbM/+6JM37J25pxS65+sP7rMQev52gzop4CgII1/+11JUocbbyjXOAAAAABwtSNoBQAAAHDVM/j56uWJP1ZoqPpn6jLkFsfzqaPHFF4lRj6+vqX2mT/2uwo9Ovhy2r/5f1o1dYb2btwku/3cvbT127RWt9uHqEG7tm77Lhg7TvnZOfLy9labvkU7P9vfcJ0ObNmqzYuWqM2AfqrbqmWp89dv21p7N2664FHDgaGhiq9X12293WbX8YMHJUkRcbEKCHJ/L66vX/nDb0k6tHOnJCk0KlJNOrnez9qkUwfZ7Tb5Gcu/mxkAAAAArnQErQAAAAAqhas1ZD3f3C+/UfLu3eo77H61v/F6t+3ufvOfslrMl2ROby/XO0f/SpL2JmpPwkZJkrePj1r07K5utw9RfL16pfZL3r1HG39fIElqf+MNjmOlm/foplXTpit5T6KmjRqtZ7/+XH4BAW7H6XjTDTIVFCq6erVS52vRq4da9Orhtt5iMuuNGwdJkm5+6nE17uAagF4Kp0+c1NpZv0qSetx1p7wNrv/r4J43X/9T5gYAAACAKwlBKwAAAIBKy26369TRozq6d5+OJibqaOJ+RVerqsHPP1PRSyu39JQU5WRkKvNkqts2drtdCXPnXdJ5r73xegWHh13SMS+VNv36aOWUqWrbv686Dxms8CoxF+yTlpys8W+NkN1uV2BIqPoNu9dR5+XtrUHPPq3Pn3pOp1OOa86YLzXk78+6DfN9/PzU6+47L9n3/Jnsdrum/+cTWc1mRcTHqf2N7u+UBQAAAIDKjqAVAAAAQKVgt9mUlpys5MR9OrZ3v44lJurYvv0qzM8/r6G95AEuobPH+lrMl2ZH6Vm5WZlKO3pMkhy7L0tit9m0cNyPkiSDv5+8vXzKNZ/dbpO5sFCS1LRzp79s0BoaFaVXfx4vg79fmdqnJiVp7IuvKjs9XZJ089OPKzA01KlNtQb11WnQzVozY5Y2/b5AkpeGPP+0vLz/2rt7L2TV1Bna/78tkqSbHnv0gkdQAwAAAEBlRtAKAAAA4Kq37OfJWjZxskwFBSXW+xgMqla/vmo0aaz6bVvp3w8MV8aJkyW2tVmtjud/3jDI7S7G3vcOdXsnZ2RcnCTp9IkTysvKcgnxymvDr7/LZrFIkqrWd3/XZ3HD3huhui2al2u+1KQkffzQ38rV96wThw4rMWFTufrmZWeXuW1ZQ9YDW7dp8nsfOkLW/g89oJZujvMdMHyYUvYf0MFt27Xp9/mymk0a8vyzZZ7rr2b78pX6fex3kqR21w9Qk84dK3hFAAAAAPDXRtAKAAAA4KrnZzQ6hazhMdGq0aSJajRtrBpNGqta/foy+J3buTfr0y+cAlV37Dab3O1/tZeyMza2Vi1JkqXQpG9eeFlt+vdTVHyc/IwB8vZwB6HNbFFWevqZsK/oPtFqDRsounp1j8apKKtnzNTqGTMrehnKOZ2heV+N1f8WL3GU3fj4o+oy5Ba3fXz9/XX/iDf03cuvK2n3Hm1ZvFSHtu/QgOEPqkWvHlfUvcBbFi/V1H9/LLvNpqr16ummxx8ttX1+do7MhQXy9jHIy8dLVrNFWemnJUkBRuPlWDIAAAAAVDiCVgAAAABXvTrNr1HX2warZtMmqtGkscKio0ttf93wYTLll7z7tayqNqjvti62Ti1de/0AJcybrxOHDmve12Mvaq7iAoICdcuzT5W5/Y+vvSVvQ/mOu7VbbeXqV5yPr698fMr3p2nxo4svxq7VazX136NUkJMrSYqsGq/Bzz6lem1aX7Cvf2CQhv3rHf34xts6vHOXMk6mavL7H+rQjl0a9MwTF722y2HxjxO0+KcJkqSoqlU17P0R8rtAWLp7wwb98sG/S6yLqV3rkq8RAAAAAP6KCFoBAAAAXPXi69VTfL16ZW7fws1RsZfS4L8/q7bXDdDWpUuVsv+A8nNyVZiTI3OhyaNxvH18FBIZqZCoSMXVrq32N9+giLjYMvdv1r2LR+2Ly83M1LpZv5ar71mDnnpC7W4YUK6+2emn9f6d91zU/JJUrVED+QcYZSooVPfbBqv3vfd4dPyvMTREj476UGtn/6oF3/4gX38/9Rh6x0Wv63Jp1OFaLZ/yi+Lr1NE9b76m4IjwC/Zp0rGjfHx9ZS12z3BYdLRa9u6pmk0a/4mrBQAAAIC/DoJWAAAAAKggNZs2Vs2mlz+U8vL21o1njoZt1r3rBXf4upOfnaO42rUlSaFRkR71rdOimWw2u0KiIso1tyQZfH3VtEvRPaLB4RcOB90Ji47WsPdGyC6b4urUKdcYXt7e6nzLQDXp1FE5p08rPMb9z9Tf3+j4+YdGR5V5Dm+fc7+32Jo1yrXOWs2a6JZnn1JAUJCjrHqjhho+8j1Va9DA6Qjt0gQEBerpLz6V3WaXj69BgaEhl+yuYQAAAAC4UnjZS7s46E+St3aj49knIuxyTw8AAAAAAAAAAADgCmc9nel4DuzU7rLPX76LeAAAAAAAAAAAAACgEiNoBQAAAAAAAAAAAAAPEbQCAAAAAAAAAAAAgIcIWgEAAAAAAAAAAADAQwStAAAAAAAAAAAAAOAhglYAAAAAAAAAAAAA8BBBKwAAAAAAAAAAAAB4iKAVAAAAAAAAAAAAADxE0AoAAAAAAAAAAAAAHiJoBQAAAAAAAAAAAAAPEbQCAAAAAAAAAAAAgIcI1KHVXAAAIABJREFUWgEAAAAAAAAAAADAQwStAAAAAAAAAAAAAOAhglYAAAAAAAAAAAAA8BBBKwAAAAAAAAAAAAB4iKAVAAAAAAAAAAAAADxE0AoAAAAAAAAAAAAAHiJoBQAAAAAAAAAAAAAPEbQCAAAAAAAAAAAAgIcqJmj18qqQaQEAAAAAAAAAAABcZSooe6yQoNXbGHDuxWariCUAAAAAAAAAAAAAuFJZrI5Hp+zxMqqYoDUo0PFsKyysiCUAAAAAAAAAAAAAuELZCgocz95BQRWyhgoJWg1xsY5ne4FJtvwCdrYCAAAAAAAAAAAAKJXdapM1J092s8VRZoivUiFrMVTEpN7BgTLExshyIlWSZC8olLWAna0AAAAAAAAAAAAAys4QF+N0mu7lVCE7WiXJr1Z1+YSFVtT0AAAAAAAAAAAAAK5gPuFh8qtZo8Lm97Lb7fYKm12S+dhxWdPSZTOZpGJbfAEAAAAAAAAAAADAia9B3n5+MsREyRAfe+H2f6IKD1oBAAAAAAAAAAAA4EpTYUcHAwAAAAAAAAAAAMCViqAVAAAAAAAAAAAAADxE0AoAAAAAAAAAAAAAHiJoBQAAAAAAAAAAAAAPEbQCAAAAAAAAAAAAgIcIWgEAAAAAAAAAAADAQwStAAAAAAAAAAAAAOAhglYAAAAAAAAAAAAA8BBBKwAAAAAAAAAAAAB4iKAVAAAAAAAAAAAAADxE0AoAAAAAAAAAAAAAHiJoBQAAAAAAAAAAAAAPEbQCAAAAAAAAAAAAgIcIWgEAAAAAAAAAAADAQwStAAAAAAAAAAAAAOAhglYAAAAAAAAAAAAA8BBBKwAAAAAAAAAAAAB4iKAVAAAAAAAAAAAAADxE0AoAAAAAAAAAAAAAHiJoBQAAAAAAAAAAAAAPEbQCAAAAAAAAAAAAgIcIWgEAAAAAAAAAAADAQwStAAAAAAAAAAAAAOAhglYAAAAAAAAAAAAA8BBBKwAAAAAAAAAAAAB4iKAVAAAAAAAAAAAAADxE0AoAAAAAAAAAAAAAHiJoBQAAAAAAAAAAAAAPEbQCAAAAAAAAAAAAgIcIWgEAAAAAAAAAAADAQwStAAAAAAAAAAAAAOAhQ0UvIMuUoxN5aco25yrPkl/RywEAAAAAAAAAAADwFxVkMCrYL0ixxmiF+gVX6Fq87Ha7vSImttqt2p95RCfzT1XE9AAAAAAAAAAAAACuYFWMUaoXVlM+Xj4VMn+FHR28j5AVAAAAAAAAAAAAQDmdzD+l/ZlHKmz+Cjk6+FRBhlLPhKxekgIMRvn5GOTNlbEAAAAAAAAAAAAASuAlySqbTFaLCiz5sqsobI0KiFBUQPhlX0+FJJspeScdzwEGowJ8/AhZAQAAAAAAAAAAALhll+QtbwX4+CnAEOAoL549Xk4Vkm7mWwocz34+FbKpFgAAAAAAAAAAAMAVytfH1/FcYCmskDVUSNBaaDU5nn3YyQoAAAAAAAAAAADAA8UzxgJrJQpai7NX9AIAAAAAAAAAAAAAwEMVHrQCAAAAAAAAAAAAwJWGoBUAAAAAAAAAAAAAPETQCgAAAAAAAAAAAAAeImgFAAAAAAAAAAAAAA8RtAIAAAAAAAAAAACAhwhaAQAAAAAAAAAAAMBDBK0AAAAAAAAAAAAA4CGCVgAAAAAAAAAAAADwEEErAAAAAAAAAAAAAHiIoBUAAAAAAAAAAAAAPETQCgAAAAAAAAAAAAAeImgFAAAAAAAAAAAAAA8RtAIAAAAAAAAAAACAhwhaAQAAAAAAAAAAAMBDBK0AAAAAAAAAAAAA4CGCVgAAAAAAAAAAAADwEEErAAAAAAAAAAAAAHiIoBUAAAAAAAAAAAAAPETQCgAAAAAAAAAAAAAeImgFAAAAAAAAAAAAAA8RtAIAAAAAAAAAAACAh3zeeuutty73pEdyjjmejYaAyz09AAAAAOhoaop+WTxDtWKrKzAgsKKXI5PZrDe++ZfSM9NVvUpVBfj9eX8rrduxQZ9O+VKZOZlqWqeJo/zTyV9o+rLZqlutjiJDI0rsO3rSGG1N3KH6Nepc9BrzCwu0fPNKBQYEKjgw2KV+9srf9N/JX2hRwlJd17HvRc1V3KGUI1qxZbWOph5Tnaq1y9Qn6USyFiUs0b7kA2pUq8FFzZ+Tn6vnP35Fv62er5b1myk0ONSlTX5BnpZsXK78gjzFRlYpdTyz1ay3vnlPWbnZqhJZRUb/C/9eDh47rCmLpsvH21vx0XHl/pbixv8+WfPWLJC/n7+qxcRfkjEBAAAAoDQF1kLHc82Qqpd9fsNlnxEAAAAA/gJ+WzNfE+dP0aSFU/XziO8UHR7tVP/L4hnKLcgr83gFpgL5ePvo+o79VD22msfrmbhgitZsW6f1OxLUvmlbhQWHeTyGOzn5udqwc6PjfePuLdqwa5NMFrMiQyMd5Wt3Jigl7bga126kwylHJEn+vv7q0rKjJOnw8SOauWKuosIiNXzg/Re9rmWbV+rDnz6WJH3zj09Vv3o9p/rU02nadWi3jP7Gi56ruG37dujjnz9Tjdjq6t2uR5n6JCbt12e/fK2w4FAN7HbDRc1vtVq069BuSVKBuaDENqMmjdGiDUsVFxWr714bI2Mp/xhgxebVWrV1rVZtXavIsEh1b9X5gmtYtnmlJi2cqoQ/NmnsP8aU70POs2Fngrbv36X6Nerq2iZtLsmYAAAAAPBXRtAKAAAAoNKxWC36fe1CSVKrhi1cQlapKGhNzUjzeOzWjVp6HLQmnUjWxPlTJEmDetykWvE13ba12W2yWKzy8/Ut8/ipp9M04ruRLuVb9m7Tlr3bXMp//G2i4zkmPNoRtE5aOF2S1L11V2XmZpc6Z2hQsHx9Sl/j3NW/S5KuqdvEJWSt7B4eNEyrtq7V8VMn9M2scXrmzifctp22dJYkqXGthmUKWSVp1da1kqS+1/bStKWz9MW0sWXqd33nfnrh7mfK1BYAAAAArnYErQAAAAAqnTXb1ys967Qk6fY+g0tsM6BjX+Xm55RpPLvdrpkr5kqS/P38PVqLyWzWBz+MktliliRNXzpL088EZ+5Ui4nX6w++pMa1G5VpjvjoOI15aZTjfeX/1mjSwqnq3KKj7rnuDkf5Bz+MUtKJZD131xNqULO+JMnXuygsTTyyX/PXFYXTM5bN1oxls0ud878vfKTm9a5xW7/ncKJ2HvhDknRL95vK9B2VSWxEjO6/fqi+nvm9Zq6YqyE9B5UY4G9N3K4/Du2RJD0yaFiZxj6WlqIDRw9Kknq366mVW1bJarOWqa/NbpckZeZkSpKCA4Pl4+1Tpr4AAAAAcLUhaAUAAABQ6cxdVbSTsk7VWmrftG2JbTw5GtdsMTmCVqOHQeu/J4x2HCNbVkdTU3T4eFKZg9YAP381rd1YkrR2+3ot3rhMLRs0133X3ek0xuNDhiszN1vXNm2rqGJ3tBaaTfpwwiey2+2KiYhW20atnMbPyM3Suu0b5ONjUN92PeTl5aWI4PBS1/T93PGSJKO/UTXjaujgscMubTJyMiRJNpu1xPrzBQYYL3if6ZXklh436+cFU5Wdl62JC6bopfued2nz9YzvJUltG7dWm8atXOpL8vvaRZKklg1bqEpEtLq37qp61Yp2FJ/KPKV3v/9QkvTmw68q/LzfY1RY0X8Xt75yr6w2q3544yvVjKtRvg8EAAAAgCscQSsAAACASiXl1HEl/LFZkvvdrJ7KLzx3z6bRr+z3if4072ct3LBEkvTQzfepd7uebtvuP3pQb3/znmx2m/q1760BHft6vE6zxaQxU79W6uk0hQWFasqSGSW227Cr6D7X7q26qGebbvp44qfal7RfUtFOxnuvH6pqMfGO9l9MH6t12zeof/teJYaB59t1aLfW70iQJOUX5utvH5R+FG2h2aSH3n38guN2bdFRIx5744LtSpOXn6sVZ47VLe7srlGT2azf1y1y279X2+7y9/W7qDWcZfQP0MCu12na8jny83UN8FdsWeMI6R8e9ECZxrRYLZq7Zr4kqe+Z+2ljwqMVc+b47GWbV0qSIkLD1bNNt4v+BgAAAAC4mhG0AgAAAKhUxv8+WXa7XbGRVdSnXS+37ZJPHNXY2T+UacwCc6Hj2d+vbCHb9GWz9d2cnyRJt3S/UfddP9Rt25z8XH0941vZ7DbViK2u5+9yf19naSbM/0VHU1MUEx4tP4OfTqSdLLFdyqkUnc7OVMMa9fXvCaM1f/1iRYZGqHe7npq6ZIY+mTRGI596R95e3krLSNPsM7t57+x36wXXYLFa9PHEz8q1/svhdE6WRv44ym19fmF+qfXXNm3rErRm5WXrsylfOd5NZpPjeeysHxQaFCpJatu4lRrXaqjvfx3vqM/Oy9Y1tRsrIztDb33zntO4Z49eNvobNWnBVEd5l5Yd1a997xLXt2b7eqVnpsvgY1D3Nl1d6ncdLBqzRb1mbr8RAAAAAFCEoBUAAABApZF0Ilnzzxyb+vitD8vPt+j+0cUJy7Rq61o9NmS44+jZrPxsLf/fKo/nCPC/8I7Wcb9O0A+/TZAkdW3ZSU/f6X63ptli0ttj39fR1BRFhkZo5FPvyBgQ6PG65q9bpB/mTpCvwVcv3POMqkTEuLSpGhMvf18/vT32fS3bvFK+BoOOHE9SSGCIPnz6XdWOr6lt+3do4x+bNWbKV3r4lgf1+pcjVGAq1IAOfVQrruYF1zFp4VTtSz4gSXr70dfVvVVnt22/nf2jxv8+SUZ/o377eJrH33xWodmktIxTjveM7KIjiS1Wi46mpjjKI0PCZPDxcdqte1ZeYb5OZ2XIy8tLVaPjnOrMFotOnk51P7+p0LFz+Xzrd250PAcbA1U1Jt7j/+7yC/Od+lSrUtVt28kLin6O8dFxCg0Mcanfub9oh2zz+k09WgMAAAAAVEYErQAAAAAqje/m/CSrzarWjVqqR+ui3Xxmi0nfzv5BKadOyGaz6e1HX5Mk1YmrqTEvud+5WNyB5IP6z8RPJRXdh+qO2WrWZ7987dgBek2dxnrtwZfk7eVdYnuL1aJ3vh2pjX9sltHfqA+eeEfxUXElti3N9OVz9OnkL4rWYDHrlTElH6/75cuj1ahWA6VnnZYk1YyrqVHPfaATp046wrs3HnxZT3z0d01fPkfr/9ikoyePqX71unr2ricvuI4te7frh7kTJRUd81tayHop7T2SqGf+838u5Slpx3Xvm8Md7/8Y9qL6te+t8W9/69J2ycblGvHdSIUGhbjUH01NcRrnfAF+Abq52w2O97yCPC1OWCZJ6tG6q0KDi3a0Nqt3jWLCo3X3gDtKHMditWjKoumOfu4C1Rb1S96NumbbulLvA87Ky9aeI4lFa6l7jdt2AAAAAIAiBK0AAAAAKoVt+3Zo2eaV8vby1lO3/81RPnvlb0o5dUK+Bl89OvghR7kxIFBNazcu09g5ebmSJIOPQQafkv/MOnI8Sf8a95H2HtnnKNubtF9DXr7b7bg2m1WFZ46ZLTQV6tmPXyp1HcMH3q9bew1yKe/SoqMWr1+qG7r0178n/FfXdeyre4sdVTx+3s9O946mZxcFrREh4TL4GJwCvWpVqmr4wPv18c+f6ejJY5KkF+55Rkb/gFLXduR4kv759QhZrBZFhITpuTIEs1eLkMBg/X3oU473FVvWOILWewbcqQY16zm1f2TQsBLHMZnNjqB1QMe+6tS8fZnXYLfb9e2Zo6rdWb8jQVabVZL03Ccvy0tejjqrzaK2jdvovcffLPOcAAAAAHC1I2gFAAAAcNU7cTpVI3/6WJLUuUUHZedma3HCMqVmnNKkhb9Iku7se2uJR8aWRV5BniT3u1lXb12nd78fqQJT0V2uRn+j8gvzZbaYZbaYyzSHzW5TfmF+qW0sVmuJ5bERMRrz0igdOZ4kSQoyBjt9a5AxuNgYFqWdTpMkRYRGOI2TlpGm7+dO0O9rFjqVvzD6H7p7wB26rfctLveTOuYIDFaX5h20aONyvfnwPxQVHlXqt1xKDWs2cNqFujhhqb7/dbzio+P00dP/cpRHhoRdlvVs3r3F8Txn9Tz9veZTpbS+NGas+FUHjh4stc3qresczwWFBS71WblZl3xdAAAAAHAlI2gFAAAAcNUbO2ucjp25i3PV1rVatXWtU31MhPNxrf/8aoTSM0+XefyM3ExJUr6pUE9++HdJUtdWnTS0/+2SpPiYOJnMZnl5eemBG++WzWbXj79NVLWYeL14z3Nux/3wp1FKOXVCN3W9Tn3a9XLbbsR3HziO+y2L2Svnav66c2Hp2V2zdtm1bkeCCkyFio2soqjQCJktJq3auk4LNixRws5NstqsCgwI1AM33q0ebbrpy2ljtWzzSo2dNU7Tl81Wrzbd1aNtVzWr00ReXud2REaFRuiVB17QI4OGXdaQVZL8ff2cguXwkHBJRTuQyxqu22w2SXLa5Vlem/cUC1pX/qbebburVcMWFz2uO0knkvXNjO8knQv5z5dXmK8NuzZJkp649RE1qFHfUTdv7XwtWL9EVcv5DxEAAAAA4GpF0AoAAADgqte1ZSct2rBUkhQcGKxacTUku107DxbdV/nErY84HX27L/mAjp864fE8VqvFcQdmvRp1HeV1q9bW0AG3q2WDZrq2SVuNmztBUlHo1aphc7fjBZxZU3xUXKnt/NzsInWnZYPm6nNtT6eyVVvX6IkPn5fdbpckdW/dWRk5GbJarJq8cJr2HElUsDFI/Tr00b0D7lBkWKQk6c2HX1X/7b311Yzvdfj4EU1bOlPTls7U6w++5DTH7a/ep6w8z3ZEWixFO3TzC/M14FnXI5FLM+PDSQr0N3rUpzSF5qLdyJ7+rM935HiSkk4kO5X9e8JojX3tc8eOaLPVrIzsTJe+JvO53c+ZuVlKzUhzaWP0NyrYGORU9tXM71RgKlRYcKhu6z1Y387+waXfgnWLlV+Yr6iwSA3pNVA+3j6OuunLZkmSqkYTtAIAAABAcQStAAAAAK56Ha65Vq8N+z+1bthCUeFRKjAV6m8fPHOmrp16tunm1P6ZOx5TfglHp0rS0k0rtGrrWjWs1UB39hnids7zd/89PPCBi/yKixcbFasvXx6t8NBwxUbEONVVi45TyJkjhKvGxOtYaooGv3S3urbspH8Of0VbE7epV9seJd7F2ql5B3Vq3kHbD+zSvNXz5eXt7RLkmq1mp6DQUxfT91I4uwvU383x0GW1ZNMKp/furbpoxZbV+n7Oj3r81kckSQeSD+mxkc+WOs7IH0eVWH5H3yF6fMjDTmVdWnTU6q3r9NxdTyovP8+lj91u1/RlsyVJ13fq7xSyStK+pP2SpLrV6pS6JgAAAACobAhaAQAAAFz1Avz81bf9uaN3v5nxnY4cT1JkaIRevv8Fl/admndQXn6uvLy8ZAwIdKo7eOywVm1dqyphUerdrodL3+y8HIUEBruUV7S8wnzZbDZVq1JVkpSTn+tUX6daHT15+98c73sPJ+r3dYu0auta3dT1enVv3VVWm9Wln9MY8bX0xG2PugR1kvT2I6/JYrVcoq+5MHd3xZbGZrfpZHpqiXWpGackSd5e3i67nVNPpxV7TpXZbFJYcFiJofSSjcvl5eXl2Dl8a+9B2pK4XVOXzFLPtt3VpHYjj9d9If3a91byyWPq2aabfls936V+3Y4Exy7bG7r0d6rLyc9VypnvbVq74SVfGwAAAABcyQhaAQAAAFQqCX9s0vTlcyRJrzzwgiJCwlza7D2yT2+NfU8hQSF6//G3FRkaXqax569bpFE/f6rBPQdq2I33Oo6C/St448sR2lTsblBPvDLmDY/a92rXXW889IpTWcsG7o8+/qs4nZ2pof98sNQ2h48fKbXN4yOL7tz950MvuwTxfxzao6QTyWrbqJXjdxEYYNQdfYdo7KxxGvPLV/rs/0apXvU6mvrBBJexzWaTY+5XH3hRbZu0dmljLCFgNvgY9MigYSWu12Q2a8y0ryUVHbEdHxXnVL8tcbskKSY8WtHh0W6/GwAAAAAqI4JWAAAAAJVGVm6WRv74sSRpaP/bdW2TNiW2iw6LlNEvQHsPJ+qZ/7ygj575l0sAdb7ZK3/Txz9/JknKLyyQr+HCf24Vmk06eOyw23qT2SRJSs/KKLWd2XLhY3W7te6s2lVrX7DdpdCg2P20OGfqkpmSpH4d+jiF3oN73qzpy2br/hvvkVQUjEaFRrj0L358ckhgcIltPDVx/hQdPXlMBh+DHhs8XOPmTlC1mHj1a99bkrRm+3pJUrP6TS96LgAAAAC42hC0AgAAAKgUTGaz/vnVuzqVma761euqV5vuWpywTAeOHdL+5AM6cOyQ3nvsTdWvUU+RYZH6+O8j9cpnb+iPQ3v06pi3NOalUQoqdoxwdkHRXZd2u11jZ/+gifOnSJIeveVBDe1/e5nWlHQiWQ+9+/gF201bOlPTls4sx1efM6j7TU7v+QV5sp45vvZieUsKNAZ51OeTSZ/LZrddkvklaVD3G1XvIu4QzSvMl9ls0vi3v3Wps1jMeuzD51RQ7N7eB2+6V32u7eXS9qzI83ZKnzydpuWbVykiNFztmjoH/IH+Rn3x0ieqEnH5d4wWmIu+6dbeg3QqK10/zC3aSbv74B49dutwrduRIEnq1Kz9ZV8bAAAAAPzVEbQCAAAAuOqdSP//9u4yOsprbeP4NTNxV5JAgOBBi7tTvFBKhXqpngr19rSn9JxTe+tyCnX3QgVooUWLFHd3C0ESEogTkoy9HwIDaTLJPCElyP+3Vtd65tn3lgn5knV1752m1755Wxt2bZIk7TqwR3e9fH+pOrPl1N2iIQHBennMc7r3lYe0LzVZL3/5hp7/x79d7et3bNCqbWs1ZcFULV6/TIF+AfrnzQ+rZ+tuf/8XqgJPvPsfbdy9pUrGqhUdV2ZAWZ5pi6bL7rBXyfxScRBYmaA1OXW/fln4u2Yuna2BXfrr/tPuqT1pzbZ1rpC1U/P2Wr55lZZuXKGbh1zv8TwTZ/0ou8OuSzv0lpfZXKq9OkJWSbr7ittVLy5B3Vt3UYCvv24YcLW+nfWjJi2YqlXb1+lodobMJrM6NW9fLesDAAAAgHMZQSsAAACAC97WpO1avW1tiXd+vn5qXLuhmtZroqYJTZSY0EQx4dElakICgvXC3f/VC5+/oluGXK9jBfnavm+nq/3xcWMlSYl1G+vftz+hmlFxhtaVEFdHrz/4UiW/1Sn3vPKg0jOPGOpz05DrlJWbfcZzS5K/r3+l+7Zs0Ey1Y2tXqm9hUaH+WDm/0nMfTDukW547FazuS0kus27husWSpLioWN1/9d1avvkObdu3QzuSd6lxnYYVzrPnUJJ+Wfi7TCaThnYb5LYuKSVZW/Zsddtutdtcz6u2rFZmTqbb2q6XdFJYkGd3Cw/s3M/1fMeIW1UrJl5vfjdeyan7JUltE1srJDDEo7EAAAAA4GJC0AoAAADggte5RUeFBYWqWf2m6tKigxITmqhezbqymC0V9k2Iq6OP//WOFq5fqiff+6+OZmeUaK8ZHadxj74qby8fw+tydxenUaMuHanc/GNqXr+px338fP0VZKuaHaV+Pr6V7juoc38N6TawUn2P5mQaCloPZ6Rp+pLZ+m3xDElyHV3cIL6erul3pfq071GqT3ZetuasWiBJ6tmmm2rVqKk2TS7R2u3r9fO8KfrXLY9VOO9HUz4v3s3asY/qxtZRdl7ZAffa7es17of3PfoukxZMLbf9g/i3PQ5a/2pwl/4K8g/Ufz56QZI0rMeQSo0DAAAAABc6glYAAAAAFzw/H1/98NJX8rZ4G+6bnnVE4ya8p0UblkmSIkIjlJGdoUsat9KRzHQdTE/RJ798qXuuvLOql+2xK/uMcD0fTDukGpHRFX7Xjyd/Vq1HB59Nq7et1Y9/TNaKLavlPO1e2naJbTSq/0h1aNrObd+Pf/lCefl5MpvMGtCpeOfnZd0Gae329Zq1fK4Gde6vNk0uKXf+Dk3baOXm1bplcPlHDYcGhahhfH237Q6nU3sO7pUkxUXGKLCce3F9zyD8lqRNuzdLkiJDI9S1Zen7Wbu26iSnwyF/v8rvZgYAAACA8x1BKwAAAICLQnnBY97xY1qzfZ3aNmmtoBPhlcPp0K9//q6Pf/lC+QX5Cg0K0aPXP6Adybv0zYwJCvYL0Jg7x+r+1x/VD39M1vHCAj0w6h55War3z6x3f/5Y25K26dZhN2tY98Fu656969+y2a1VMqfFVPrO0XPJtn07tXzzKkmSxWxRn/Y9NerSkWoY36D8fknb9fuSWZKKd3XWr5kgSerdrod+mDNJ25N36rVv39anY9+Tv6+f23GG9xii44WFio+pVe58fdv3Ut/2vdy2F1mtGvjg5ZKk+6+5R13KCECrwuGMNE1eME2SdP2gUWX+Tj9319N/y9wAAAAAcD4haAUAAABw0XE4HdqRvEurtq7Ris2rtGXvdtkddr3xwItqm9haew4l6Y1vxmlL0jZJUqcWHfT4jQ8pMiRcO5J3ucZpGF9fL9z9H419/1lNXTRdSSn79NgND6pOJe8crQqH0lOUmZuttIx0tzVOp1O/LZ5epfMO7TZY4cGhVTpmVRnUqZ8mzP5Jg7tcqiv7XlHqLt6y7D98QE9/+LycTqdCAkN027AbXW1mk1mPXH+/7nnlIaUcSdW4Hz7QP298UCaTqcyxvL18dOOgUVX2ff5OTqdTr339P1ltVsVFxWpYd/d3ygIAAADAxY6gFQAAAMBFISM7Qyu3rtHKrWu0ausaZefllGivG1tHZrNFn0/7Rt/O/EF2u01+Pr66e+QdurznULfjtktso5fufVb//fhFbdy9RXe8OEaX97xMI/sMU1xkbJl9vL2Kd9cW2apmR+lJ2XnZOpB+SJJUv1aC2zqH06FPf/1KkuTr7SOzB3fVlsXpdKigqFCS1K1Vl3M2aI0Mi9RPL30jX2/P7tFNTt2vh9/+lzJO3Mf6P3unAAAgAElEQVT74Kh7FBIYUqKmcZ2GGtF7mCbN+0Uzls6SyWTSYzfcL/M5vru3Ij/8MVmrt6+TJN135V2VOm4bAAAAAC4WBK0AAAAALnhTFkzT2xPfK/W+WUKiurfuoh6XdHUd67ppzxbZ7TYl1m2ssaMfr/C4V0lq0+QSffzUeD3/6cvavHebfpo7WWkZaXr2rrFl1teMKg5gDx89rJxjOaVCvMqaumiG7HabJJV71+fpXr7vebVu3LJS8yWn7tctz/2jUn1P2nNon1ZsWV2pvrnHcj2u9TRkXbdjg57//FVXyHrH8FvcHud75+WjtfvAHq3fuVHTl8yU1Vakx2540OO5zjXz1yzUR5M/kyQN6TZQ3S7pXM0rAgAAAIBzG0ErAAAAgAte3RNH+VosXmrTuJW6X9JF3Vt1VmRYZKna6wdercjQcPXv2LfMuymdcpY5R0xEDY1/7A3NWTlP81Yv1JM3P+x2PQlxdSVJhdYiPfTWExrYub9qRsXKz9fP8A5Cm8Omo1kZWrdzo2YsLb5PtHHdRqodE29onOry87wp+nnelOpehjJysvTB5E80e/lc17sxV9+lK/uMcNvHz8dXL979Hz02/mltTdquOSvmacPOTbprxK3q276X26OEz0VzVszTy1+/JYfToYa1G+i+q+4qtz43P0+FRQUym71kMZtks9l0NCdTkuTv6382lgwAAAAA1Y6gFQAAAMAFLzGhicaOflydW3ZUkH9gubVmk1mDuwwo8W7cxPd0MD1FXl7e2r5vhyQpMiyqVF+TyaT+Hfuqf8e+5c5Rr2ZdDe02UL8tnqm9h/bpg0mfGPxG7gX6BeiRa8d4XP/U+8/IYq7ccbd2h6NS/U7n7eVdZqDtidOPLj4Ti9Yv1Stfvam848ckSTWj4/TIdWPULrFNhX0D/AP18pjnNPa9Z7VpzxalZabrhc9f1cbdW/TQtfee8drOhi+mfasvf/9WklSrRk29ct/zCqggLF22aYVe/OL1MtsSatat8jUCAAAAwLmIoBUAAADABc/f10+XduxT6f4RoRGavGCa63OgX4D6dyo/TK3IYzc8qMFdB2ruinnaeXCPjuUfU+7xPBVZiwyNYzFbFBEaocjQCNWvmaDhPYYoNjLG4/692nRTjIH60+XkZZf4uVTGQ6Pu1ZBuAyvV92hOpq568oYzml+SmtRtJH9ffx0vKtS1/a7QTUNvMHT8b0hAsN5+9FVNWTBNn/zypXy9fXT9wGvOeF1nS+eWHTRh9o+qX6uenrtrrCJCwirs07VVZ3l7ect62j3D0WFR6teht5olJP6dywUAAACAcwZBKwAAAABUYHDn/ooICZePl4+iwqJOBHN+Zzxu83qJal7v7IdSZpNZY64uPhq2Z5vuii5jd64ncvPzlFAzQZIUGRZhqO8ljVrI7nQqIjS8UnNLko+Xt7q3Kr5HNNyDcNCd6LAovTLmeTmcDjWoVa9SY5hNZo3sPVzdWnVWRk6maoS7/5n6+fq7fv5RZRxf7Y7FcurfrW5c7Uqts3n9pnr4ujEldnYn1m2s1x58UU1qN5KPt2dHVwf6Bejjp8bL4XDK2+KlkKDgKrtrGAAAAADOFyan01n2BUN/o0Upq1zP4b6hZ3t6AAAAAAAAAAAAAOe5zMJs13P3uPZnff7KXcQDAAAAAAAAAAAAABcxglYAAAAAAAAAAAAAMIigFQAAAAAAAAAAAAAMImgFAAAAAAAAAAAAAIMIWgEAAAAAAAAAAADAIIJWAAAAAAAAAAAAADCIoBUAAAAAAAAAAAAADCJoBQAAAAAAAAAAAACDCFoBAAAAAAAAAAAAwCCCVgAAAAAAAAAAAAAwiKAVAAAAAAAAAAAAAAwiaAUAAAAAAAAAAAAAgwhaAQAAAAAAAAAAAMAgglYAAAAAAAAAAAAAMIigFQAAAAAAAAAAAAAMImgFAAAAAAAAAAAAAIMIWgEAAAAAAAAAAADAIIJWAAAAAAAAAAAAADCIoBUAAAAAAAAAAAAADKqWoNUkU3VMCwAAAAAAAAAAAOACU13ZY7UErQFefq5nhxzVsQQAAAAAAAAAAAAA5ym70+56Pj17PJuqJWgN9A5wPRfYCqtjCQAAAAAAAAAAAADOU8etBa7nIO/AallDtQStNQNjXM+F9iLl2wrY2QoAAAAAAAAAAADALZMku9OhPGu+rE6b631cYI1qWY9XdUwa5B2g2IBopeanS5IK7YUqtLOzFQAAAAAAAAAAAIDn4gKiFXTaabpnU7XsaJWkeiHxCvMNqa7pAQAAAAAAAAAAAJzHwn1DlRBSu9rmNzmdTme1zS7p4LFUpeVnqMhRJKvDVnEHAAAAAAAAAAAAABclb7OXfMw+igmILHFdaXWo9qAVAAAAAAAAAAAAAM431XZ0MAAAAAAAAAAAAACcrwhaAQAAAAAAAAAAAMAgglYAAAAAAAAAAAAAMIigFQAAAAAAAAAAAAAMImgFAAAAAAAAAAAAAIMIWgEAAAAAAAAAAADAIIJWAAAAAAAAAAAAADCIoBUAAAAAAAAAAAAADCJoBQAAAAAAAAAAAACDCFoBAAAAAAAAAAAAwCCCVgAAAAAAAAAAAAAwiKAVAAAAAAAAAAAAAAwiaAUAAAAAAAAAAAAAgwhaAQAAAAAAAAAAAMAgglYAAAAAAAAAAAAAMIigFQAAAAAAAAAAAAAMImgFAAAAAAAAAAAAAIMIWgEAAAAAAAAAAADAIIJWAAAAAAAAAAAAADCIoBUAAAAAAAAAAAAADCJoBQAAAAAAAAAAAACDCFoBAAAAAAAAAAAAwCCCVgAAAAAAAAAAAAAwiKAVAAAAAAAAAAAAAAwiaAUAAAAAAAAAAAAAgwhaAQAAAAAAAAAAAMAgglYAAAAAAAAAAAAAMIigFQAAAAAAAAAAAAAMImgFAAAAAAAAAAAAAIMIWgEAAAAAAAAAAADAIIJWAAAAAAAAAAAAADDIq7oXkHlcOpgjZRdIeUXVvRoAAAAAAAAAAAAA5yKTpCAfKcRPqhUihftX83qcTqezOia2OaStadKh3OqYHQAAAAAAAAAAAMD5rFaIlBgteVXTGb7VdnTwFkJWAAAAAAAAAAAAAJV0MKd4Y2d1qZajg9OOSSknQ1aTFOgj+Voks6k6VgMAAAAAAAAAAADgfOBwSoV26ViRJGfxxs6YIKlG0NlfS7XsaE3OOvUc6CP5exGyAgAAAAAAAAAAACif2VScLQZ6n3qXnF1Na6mOSfOLTj37WKpjBQAAAAAAAAAAAADOV76nndubb62eNVRL0HrcdurZwk5WAAAAAAAAAAAAAAaYT0s5Cy6moBUAAAAAAAAAAAAAKs1Z5uNZRdAKAAAAAAAAAAAAAAYRtAIAAAAAAAAAAACAQQStAAAAAAAAAAAAAGAQQSsAAAAAAAAAAAAAGETQCgAAAAAAAAAAAAAGEbQCAAAAAAAAAAAAgEEErQAAAAAAAAAAAABgEEErAAAAAAAAAAAAABhE0AoAAAAAAAAAAAAABhG0AgAAAAAAAAAAAIBBBK0AAAAAAAAAAAAAYBBBKwAAAAAAAAAAAAAYRNAKAAAAAAAAAAAAAAYRtAIAAAAAAAAAAACAQQStAAAAAAAAAAAAAGAQQSsAAAAAAAAAAAAAGETQCgAAAAAAAAAAAAAGEbQCAAAAAAAAAAAAgEEErQAAAAAAAAAAAABgEEErAAAAAAAAAAAAABhkeeaZZ54525Puzjj1HOBztmcHAAAAgJLe/3GBPpmySOkZuWqTWMej2sNHc9S2afm1RhRZ7Xr8fz/rSNYx1YmLkJ+Pd5WN/VeL1+7S61/PUmZOvlo2quV6/9qXszRx1ko1ql1DEaGBZfZ99YuZWr01WU0SYuTne2ZrLCi0as7ybQoM8FVwgF+p9p//WKvXvpypGUs267Kerc5ortPtOXBEc1du14G0TDWIj/aoz76UDE1fvEk79qWpWf24M5o/L79Q/3jhG/0yf53aJtZRaLB/qZr8giLNWrJF+QVFio0KLXc8m82hJ97+Wdl5xxUXFSp/v4r/0N59IF3f/LZcFrNZNWuEVfq7nO6zKYv164IN8vf1VnxMeJWMCQAAAADlybeeem4Yefbn9zr7UwIAAADAuWX3gXSt3pKsmIgQj2sjQ4OqdA1fTF2iP9fs1OL1u9StdQOFBZUO3yorL79QSzbsdn1evnGvlqzfoyKrXVHhp77HonW7dDAtS83r19SeQ0ckSb7e3urVrpEkae/BI/ph9mpFhwfp3mt6n/G6Zi/fqmc/nCZJ+u7F29W4bkyJ9rSMHG3cdUgBflUbOq/dvl8vfTZdCTUjNaBzM4/6bN+Xqje+nq2wYH9d2a/NGc1vczi0cdchSVJBkbXMmpc+m67pizerZnSoJrx8pwLKCU//WLFV81bt0LxVOxQVFqQ+HZpUuIY5y7bqq2nLtGzDHn330h2V+yJ/sWTDbq3bfkCN68aoU8t6VTImAAAAAJzLCFoBAAAAXPBsNoe+nLbUbfu+Q0clSbuS0/TplMXljnWyds+B9HJrR/Zto/CQAI/Wty8lQ1/8ukSSdE3/9kqo6f5/w3U4nLLZHfLxtng0tiQdzsjRU+OnlHq/ass+rdqyr9T7jycvcj3HRAS7gtavf1suSerXMVHZecfLnTM00F9eXuXfVjNl7lpJ0iWNapUKWS92943qo/mrduhQerbemThP/7xloNva72eulCQ1bxDnUcgqSfNX75AkDerWQhNmrNRb383xqN/lvVrrqdsHe1QLAAAAABc6glYAAAAAFzyr3a73f1xQYd2O5DTtSE7zaMxd+9O1a7/7MXu3b+xR0FpkteuZD35VkdUuSfp+xkp9P2NluX1qx4brhXtHqHkDz46wrRUdri+eHe36PHflNn01bZl6tm2k2y7v5nr/zIdTlXToqJ68dZASE2IlyRWWbktK1bQ/10uSJsxcpQkzV5U75yf/vVmtG8e7bd+6N1Xrdx6UJF3dv71H3+NiEhsZojuu6K7xE+bpp9mrde2ADqoTF1Gqbs3WZG06sTt2zDV9PBr7YFqWdianySRpYJfmmrtym+x2p0d9Hc7iuqwTQXtwgJ8sZpNHfQEAAADgQkPQCgAAAOCC52U26/rBHdy2/7lmpw4czlKD+KgKjzw9WVs3NkLd2jRwWxfq4dG/L3zym+sYWU/tT81U0sEjHgetfr5eatGwpiRp4dpdmrlks9o1raPbR3QvMcaD1/dTdl6+urRqoMjT7mgtLLLp+Y9+k8NZvMO1Y4uSP6Os3HwtXLtLXhazBnVtLpPJpIjg8kPmD3/6U5IU4OethJqR2n0gvVRNZk6+JMlud5bZ/leBfr6Kjar4+OfzxagB7fXV1KXKPlagL35dov/847JSNeMnzJUkdWpRTx1aJHg07tQFGyRJbZvVUUxksPp1THTtKD6Smaux7/4iSXr5/isU/pe7eqPCio+aHnjv/2S3O/XT6/9QQlw1XIQEAAAAAOcAglYAAAAAFzxvb4seubG/2/ZD6dk6cDhLLRvFl1t3em2TerEV1lbk0ymL9PuiTZKke67uqYFdmrut3ZmcpifHTZLd4dSQ7i00tGdLw/NZrXa9+c1sHc7IVVhwgL6dvrzMuiXr90iS+nVIVL9OiXrps+navu+wJCkrL1+3j+im+JhwV/3b3/2hhWt3aUi3FmWGgX+1adchLVq3S5KUX2DVjU9/Vm59odWmUU98XOG4vds31usPX1VhXXmOHS/SvFXbSr3ftLM4DC+y2jRt4Qa3/ft3aiZfn6r5U9vP11sj+7XVhJkryxxz3srtrpD+vlG9PRrTZndoyvx1kqRBJ37fakQEq0ZEsCTpj+XF3z0yNFCXdm56pl8BAAAAAC5oBK0AAAAALnqDujRX03pxalLOPaGpR3Lk5WXWpR2bqkF8tBrWrnFGc06cuUof/Fi8q/Oa/u10+4jubmvz8gs1bsJc2R1OJdSM1JO3DqrUnJ9PXaL9qZmKiQiWj7dFKelZZdYdTMtSRk6+EhNi9X+f/K5pCzcqMixQAzs313czVujlz2do3D+vldlsUnpGnn6cvVomSTdd1rnCNdjsDr302fRKrf9syMw5pmc+mOa2Pb/AWm57l1YNSoWiOXkFev3rWa7PhVab6/ndH+a7dj93al5PzRvW1Ps/nTqSOjevQC0b1VJGbr6eGDepxLgbdx6QVLwr+PQ7iHu3a6zB3VqUub4/V+/Ukaw8eXuZ1a9j6SB1w4kxWyfWdvsdAQAAAADFCFoBAAAAXPQu7dxU706cr/mrd0iSurdpWKrmxc+ma8n63bqsR0s9c/ewM5rvo58X6qNJCyVJfdo31mM3D3Bba7Xa9eS4SdqfmqnIsECN++e1CvDzMTznb39u1Mc/L5SPt0Vj7xiimMjSR+zG1wiXr4+X/jVusmYv3ypvL4v2Hjqi0EA/vfvEdaoXH611O5K1bONevfH1bN1/bR899taPKiiy6bIeLVWvVlSF6/hy6lLX7tjXHrpSfTo0cVv7/o8L9OmUxQrw89afnz5u+DufVFhkU3pmrutzZs4xSZLVZteBw5mu9xGhgfKyWFQ7NrzUGPnHi3Q0+5jMJqlWTMl2q9Wu1KM5bucvKLK6di7/1eJ1u13PQQG+qhUb7tpV6qn8AmuJPrVjSq//pK9/Kw5ka0aHKSTIr1S7K2htTNAKAAAAABUhaAUAAABwUZk8d60OpmepY4t66tg8wfV+zoqt2p+aqbio0FJBa1ZuvpZvKj5Ot1Wj+ErPbbM59PpXs/TTH2uKx2pYS8/fO0Jms6nsertDT70zWcs27lWgn4/efnyUakaHGp534qxVev3L4h2VRVa7Hnh1Ypl1X79wm5rWi9XR7DxJUv1aUbp67I1KSc92hY//d98VGv3fLzRx1iotXb9byYcz1aRujEe7bFdvTdYnk4sD5t7tG5cbslalrUmpuuPZr0q9P5iWpRGPvO/6/Py9wzW4WwtNfuOeUrWzlm3RU+OnKCTIv1T7gcOZJcb5K39fb13Zr43r87HjRZqxZLMkqV+nRIWd2NHaukltxUQEa/TwLmWOY7c79PVvy1393AWqbRPrlPn+zzU7XUcNm0ylf+dy8gq0ZW+Kay0AAAAAgPIRtAIAAAC4qMxYulmrtyTLx9urRNBanjnLt8lud0qSDqRl6vsZK93WelnMurp/u1Lvk1KO6t/v/qKte1Nd77btS9WAe99yO5bd7nQdM1tQZNVdz39d7jrvvbq3rh3UodT7Xu0aa8biTbq8d2u98MnvGtazlW4f0c3V/umUxZr656l7R49mFe/4jAgJlJfFXGKHZ+3YcN17TW+99Nl0JR/OlEnS2DuGyM/Xu9y1JaUc1eNv/SSrzaGIkAA9Obpyxx+fj4ID/fSv2wa7Ps9bud0VtN46vKsSE2JL1I8Z1afMcYqsdlfQOqxHqzJ3XrvjdBbvEC7P4vW7XL/ndz3/tU7PYu0Ohzo1r6c3H7vG4zkBAAAA4EJH0AoAAAAAFZix5NSxr19NW1ZubYCfd6mgdcHqnRr7zmQVFBWHpoF+PjpWUKQiq11FVrtHa7A7nMovsJZbY3M4ynwfGxmiz58draSUo5Kk4EBfxZ+2GzI40PfUGHaHDmcUH4MbERZYYpz0jDx9OOlPTV2wXpJkkuSUdM+L3+rW4V113aCOpe4ndc0R4KeebRtpxpLNevmBkYoKDyr3u1SlpgmxmvLmqV2oM5Zs1gc//alaNcL07pPXud5HhAaW1b3Krdi01/U8ee7aEiHs3+WH2au0Mzmt3JqTR2dL0vHC0r9r2XnHq3xdAAAAAHA+I2gFAAAAgHIcOJyp9duL763s1a6RwkPKD+N8vCyl3tWqESarzS6zSbpzZA85HE59PHmRaseG6+k7hrod67kPp+pgerZG9m2jgV2bu6176p3Jrl2onvhpzpoSO1gLTwTATqdTi9ftUkGRTXFRIYoMDZTVatf81Tv0+6KNWrJht+x2pwL9fXTXyB7q16mp3v72D81evlXvTJyvCTNXaUCXpurXsalaNYovsSMyMjRQz9w9TGNG9TmrIask+fp4lQiWT/4bentZSrwvj+PETk+Tyj7m2YgVm5Ncz5P+WKsBnZupXbO6ZzyuO/tSMjT++7mSToX8f3W80Kql64vvi334hkuVWO/ULttf56/Xb4s2lrqbFgAAAAAudgStAAAAAFCOD3/+U05JdWMj9OpDV8lsMmnuim2aMn+dnrtnuMJDAioco2HtaN0yrKvaJtZW51b19dGk4ntKA3x91K5p2fdpSpKfn4+k4qC2vDpfb2N/2rVNrKNB3UoGt/NWbtfo/3wuR3GeqL4dEpWVmy+bzaFvflumzXtSFBzoq6HdW2r08K6KCisOS1964AoNWdtS47+fqz0Hj+i76Sv13fSV+r/7Li8RDg+5f5zhHZE2W/EO3fwCq7rd+oqhvnM+eET+FRxnbERBUfEOT3c7dj2VlHJU+1IySrx74dPf9f2Ld8rPt3hsm82hjJzSwXnRiWOkJSkrL19pGbmlagL8fBQU4Fvi3bjv/1BBkU1hwf66flBHvVfGEcLT/tyg/AKrosODdO2gDrKcdm/wxJnFR2V7GkoDAAAAwMWCoBUAAAAA3NiWlKoZi0/cpTmiqyxmk4qsdn06ZZF2JKdp7DtTNP7J60qEUu7ce02vv3u5FYqLDNXXL9ym8JAAxUaGlGiLrxGukED/4ueYMB04nKX+d/9Pvds31v+NGaHVW5M1sEuzMu9i7dGmoXq0aaj1Ow7ol3nrZLaYS+3ALbLaVVjk2THJZTmTvlUh/8Qu0DMNWmct3VLic5+OTTR3xXZ98NMCPXRDP0nSzv1puunpz8od55kPppX5/qahnfTg9f1KvOvVrrEWrN6pJ0cP0rGCwlJ9nE5p4qxVkqThvS4p9fu8Pan4XuFGtWuUuyYAAAAAuNgQtAIAAABAGQqLbPrvB1OLd7PGRWhQ1xaSJB9vi1584Ard/PRnWrE5SR/+tED3XtO7WtfqieOFVtntDtU+sSsxL79k4Nawdg09elN/1+ete1I09c8Nmrdqh67o20b9OibKZneU6ne6BvHReuSm/vKymEu1vfrglW7vkP07+Bjc5StJDofTdT/tX6VnFu8etZjNSjmSXaLt8Gk7Sw8fzVGR1abw4IAyQ+lZS7fIbJJr5/B1Aztq9ZZkfT9jhS7t1FQtGtY0vO6KDOneUsmpGbq0c1P9Mn9dqfbF63Yp6dBRmSRd3rt1iba8/EIdTC/+vi0a1KrytQEAAADA+YygFQAAAADKsHDNTu3Zny6L2aRn/jGsRHiYEBepJ0YP0n8/mKovpy5V/07N1Kjuub3b79E3f9SKTUmV6vvAqxMN1Q/o0kwvjhlR4l3bco4+Pldk5uZr2IPvlluz5+CRcmtu/vfnkqQX7x+hAZ2blWjbtOuQkg4dVccWCa5/i0B/H900tJPemThfb349W589e4sa1amhme89WGrsIqvNNfdz9wxXp5b1StX4+ZQOd70sZo0Z1afM9RZZ7Xrz69mSpN7tG6tmdGiJ9jXbkiVJMRHBio44u3frAgAAAMC5jqAVAAAAAMpwaeemCg70047kw2rZqPROvqE9WurXBeu1emuy3vp2jt576nrDcxQUWbX7QLrb9pN3ch7Nziu3zmqr+Fjdvh0S1bB2tOE1VkaTOrFnZZ7zzfczVkiShnZvWSL0HjWwgybMXKU7r+whqTgYjQwNLNW/yHrq3zkk0K/MGqO++HWJkg9nytvLrAeu66ePJi1U7ZhwDe5WvIN74ZqdkqRLmtQ+47kAAAAA4EJD0AoAAADgojKsZyu1a1pX7ZrWrbC2U8t6Ze4aPGnMqD669ZkvtXnPIR04nKX4mDBDa9mXkqFRT3xcYd1301fqu+krDY39V1dd2rbE5/yCIjlOnl97hkwmkwL9fQz1eeXzGXI4q2Z+Sbr60nZqWKfyu4qPF1pVZLVpypv3lGqz2R266enPdLzQ6np391U9Negv99CeLuIvIejho7mas2KrIkMD1blV/RJt/r7e+vK5WxUTGVzp9VdWwYnvdN3AjjqSlaePfl4oqXj37UPX99OidbskFd/DCwAAAAAoiaAVAAAAwEXlsh6tynw/9rYhKiiyqm5cpMdjtWxUS2NvH6ze7ZsoPCSgqpZ4Vjzw6gSt236gSsaqHRuuyW+UDijLM2neWtntVRe09mjTqFJBa1LKUf08Z42m/rlBw3q2KnFP7UkrNyW5QtaulzTQkvW7tXDtTt1xRXeP5/lq2lLZ7U4N6tpcljLusK2OkFWSHri+rxrUjlavdo0V6O+rW4d31ee/LtHEWau0YtNepWfmyWI2qWurBtWyPgAAAAA4lxG0AgAAALjojJ8wT9l5x6tsvM17UiRJD1zbVyFBfh73axAfpfeeuuGM57/56c90OCPXUJ87RnRXZm7+Gc8tSQF+xnaznq51k3gl1IyqVN+CQqtmLNlc6bn3p2bo6sc+1Mm4d8+BI2XWzVu1XZJUq0aYHr95gEY++r42707Rtr2pSqxX8THJu/an66c/Vstskkb0ae22bs+BI9q4y334bbM5XM9LN+zR0ew8t7W92jVWWLBn4f/QHi1dz/eN6q06cRF68dPftffQUUlSh+YJCg3292gsAAAAALiYELQCAAAAuOjMXrZFh9Kzq3zcu0b2UIg8D1q9LJYquWfzxqGdlZtfoFaN4j3u4+/nI5vdUXGhB/x8vCvdd1jPVrq8t/vwsTxHs48ZClpTj+To1wXrNWX+WkmS/cTRyY3r1NCNQztrQOdmpfpk5R13zdGvQ6Jqx4arfbO6Wrlln76fsVLP3jOswnnfmTBPdrtTg7s1V71aUcpyE/Kv2rpPr34x06PvMnHWqnLbG9eN9Tho/athPVspOMBPj731kyTpyn5tK+gBAAAAABcnglYAAAAAF63Rw7uodePars+79qfpnYnzFRsZoidvHVSidtz3c7Xn4BH94/HB7GYAAAlRSURBVMoealovzvU+OTVDb34z56ytuSzXDerget6fmqm4qFB5eZU+nvZ04yfMrdajg8+mFZuT9O3vy7V0/W6dfi1tpxb1dNPQTqXuTD3duxPmKedYgSxmk4ac2Pl5Rb82Wrlln35ftFHDerZS++bl3/fbqWU9Ld2wW3de0aPcurBgfzWpG+O23eF0amdymiSpVnSoggLch/q+3mf25/667fslSdHhQerRtlGp9l5tG8vhdCrAt/K7mQEAAADgfEfQCgAAAOCi1bRenLq3aej67H/iCNzAAN8S7yXpi6lLJEktGtZSl9OCua17U8/CSj331jeztWn3Id19VS+N7NfGbd1rD10lq81eJXOazaYqGefvsmX3IS1et1uSZLGYNKBzM900tLMalxNqStLm3Sn6Zf46SdLIvm3UsHa0JOnSjk31bf3l2rwnRc9/8psmvnyn/Hzd7+q9ql9bHS8oUp24iHLnG9C5WZm7ak8qstrVdfQrkqTHbxlY6ne0qqQeydEPs4t3zI4e3lVeZdwp++pDV/4tcwMAAADA+YSgFQAAAAAuIAfSspSRk6/DGTlua5xOadLctVU678i+bRQeUrmjav9ul/Vopa+mLdOwnq103eCOio0MqbDPvpQMPfbWj3I4pdAgf919VS9Xm9ls0r9uG6xb/vO5DqZl6dUvZ+nfdw6VyU3e7O1t0W0julXV1/lbOZ3Scx9PU5HVrlo1wnRlX44NBgAAAAB3CFoBAAAA4Czz8bJIkoqstiodNyvvuJJTMyRJDWvXcFvncDr1/o8LJBUfMWuxVG5HqsPhVEFR8Xfo3b7xORu0RoUHafo7D8jXx7M/gZNSjuruF77Vkaw8SdI/Rw9UaLB/iZrEerG6ZkB7fT9jpX5dsF4mkzT29iHn/O7einw7fblWbEqSJD1yY/8Kj6AGAAAAgIsZQSsAAAAAnGW1aoRLkg6lZys793ipEK+yJs1ZI5vdIUkVHot70rgnrlW7pnUqNV9SylFd9diHlep70u4D6Vq6YU+l+ubkHfe41tOQdfWWfRr77i+ukPW+a3prYJeyj/O975o+2rHvsFZvTdYv89eryGrT03cM9Xiuc82cZVs1/vu5kqQRfVqrV7vSd7MCAAAAAE45P//6AwAAAAADtu1N1eL1u12fc/MLJEl/rNimpENHXe8PpWdJkjKzj+nTKYtLjJF6pPgo3hmLN2vLnhTX+/SMXNfzhBkrFRjgK0lq36yuLmkcX+Z66sdHSZIKrTbd9X/faFjPVoqvES5/X295ndjt6imb3a4jmXlavTVZvy5YL0lqVj9WdSu4D/Rc8d30lfpu+srqXoYyso/pf9/9od8XbZIkmSQ9clN/XTeog9s+fr5eevPRa3Tfy99p065Dmr54s9Zu26/7r+2jAV2auz1K+Fw0Y/FmPfPhVNkdTjWpG6NHb+pfbn3usQIVFNpksZhktphls9pd4XTAibuOAQAAAOBCR9AKAAAA4IK3eU+K66jc081auqXM+oyc/DLrJem3RRvdzvPVb8tcz/df28dt0NogPlpX9GmtyfPWaff+dP3v2z/KW74hQQG++tdtQzyuf/j1ibJYKnc8rMPurFS/0/l4W+RV2flPO7r4TCxYvUPPfDhVuccKJUnxMWF66vYh6tg8ocK+gf4+Gvf4tXr4jR+0fscBpR7N0dh3f9G67fv1xK2DznhtZ8NHPy/UR5MWSpLqxIRr/BPXyt/Xu9w+i9bt0r/f+7XMtgbx0VW+RgAAAAA4FxG0AgAAALjg1a8VpSv7tTmrc1Z0dO/YO4ZoeK9LNGPJZu3Yd1i5+QXKPVagQoP3tlosZkWFBik6PFgNakfrqkvbKi4q1OP+/To2VVy05/Wny8rN1w+zVleq70lPjB6oy3u3rlTfo9nHNPDet89ofklqWi9OAb4+Ol5g1U1DO+uOK7obOv43JMhPH//7Jv04e7Xe/WGefL29NXp4tzNe19nSvU1DfTl1qRrVraHXHrxKEaGBFfbp0aaRfLwtKrLaXe9iIoI1sGtztWhY8+9cLgAAAACcM0xOp/PM/xdkg2buPPUcVfHfbwAAAACAKuR0ShNmFh/X269jompEBFdqnNxjBZq1bKskqX+npgoJ8vO4770vfie706Gbh3RWtzYNKz3/sx9NkyTddnk3NasfV6lxpOK7Yp0OpxrWqVHpMaTiI6aPZOWVGzYWFtk0ae5aSdLgbs0VFhzg0dh2h1M/zFolSerZtpFq1QgzvL6kQ0e1emuyggN9NaDzqbtn1+84oKb14uTj7fnR1XsPHpHD6ZS3xaLQIP8qu2sYAAAAADx15Nip54GNzv78BK0AAAAAAAAAAAAAzjvVHbRW7iIcAAAAAAAAAAAAALiIEbQCAAAAAAAAAAAAgEEErQAAAAAAAAAAAABgEEErAAAAAAAAAAAAABhE0AoAAAAAAAAAAAAABhG0AgAAAAAAAAAAAIBBBK0AAAAAAAAAAAAAYBBBKwAAAAAAAAAAAAAYRNAKAAAAAAAAAAAAAAYRtAIAAAAAAAAAAACAQQStAAAAAAAAAAAAAGAQQSsAAAAAAAAAAAAAGETQCgAAAAAAAAAAAAAGEbQCAAAAAAAAAAAAgEEErQAAAAAAAAAAAABgEEErAAAAAAAAAAAAABhE0AoAAAAAAAAAAAAABhG0AgAAAAAAAAAAAIBBBK0AAAAAAAAAAAAAYFC1BK2m6pgUAAAAAAAAAAAAwAWnurLHaglag3xOPTuc1bECAAAAAAAAAAAAAOcrm+PUc5Bv9ayhWoLW4NO+7PGi6lgBAAAAAAAAAAAAgPPVsdMyxpCLKWitG37q+bhNOlbIzlYAAAAAAAAAAAAA5bM5pZwCyWo/9a5OWPWsxas6Jg3xleJDpQPZxZ+P24r/AwAAAAAAAAAAAABP1Q69yHa0SlKTKCkyoLpmBwAAAAAAAAAAAHA+iw4szhyri8npdFbrob1JmdKhXKnQJhXZK64HAAAAAAAAAAAAcHHysUi+XlKtEKluNR0ZfFK1B60AAAAAAAAAAAAAcL6ptqODAQAAAAAAAAAAAOB8RdAKAAAAAAAAAAAAAAYRtAIAAAAAAAAAAACAQQStAAAAAAAAAAAAAGAQQSsAAAAAAAAAAAAAGETQCgAAAAAAAAAAAAAGEbQCAAAAAAAAAAAAgEEErQAAAAAAAAAAAABg0P8DYd99fBVDOPYAAAAASUVORK5CYII=
