## 开启导航栏

- 手动创建`_sidebar.md`

```text
.
├── README.md
├── index.html
├── .nojekyll
├── _sidebar.md
└── _navbar.md
```

- 添加配置项到`index.html`

```html
<script>
  window.$docsify = {
    loadNavbar: true, //定制导航栏 (加载 _navbar.md)
  }
</script>
```

### 编辑侧边栏

根据需求自定义修改，支持基本Markdown语法。

```markdown
- 入门

  - [快速开始](zh-cn/quickstart.md)
  - [多页文档](zh-cn/more-pages.md)
  - [定制导航栏](zh-cn/custom-navbar.md)
  - [封面](zh-cn/cover.md)


- 配置
  - [配置项](zh-cn/configuration.md)
  - [主题](zh-cn/themes.md)
  - [使用插件](zh-cn/plugins.md)
  - [Markdown 配置](zh-cn/markdown.md)
  - [代码高亮](zh-cn/language-highlight.md)
```

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/202201272130171.png" alt="嵌套导航栏" style="zoom:50%;" />

## 在`index.html`中创建导航按钮

```html
<body>
  <nav>
    <a href="#/">EN</a>
    <a href="#/zh-cn/">中文</a>
  </nav>
  <div id="app"></div>
</body>
```

!> 注意：文档的链接都要以`#/`开头。

## 小屏设备下导航栏自动合并到侧边栏

```html
<script>
  window.$docsify = {
    mergeNavbar: true, //小屏设备下导航栏自动合并到侧边栏
  }
</script>
```

## 在导航栏中使用emoji

需要[安装emoji插件](md/plugins.md#emoji)

添加脚本到`index.htmml`

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/emoji.min.js"></script>
```