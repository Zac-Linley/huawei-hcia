## 开启侧边栏功能

- 手动创建`_sidebar.md`

```text
.
├── README.md
├── index.html
├── .nojekyll
└── _sidebar.md
```

- 添加配置项到`index.html`

```html
<script>
  window.$docsify = {
    loadSidebar: true, //开启侧边栏
  }
</script>
```

### 编辑侧边栏

根据需求自定义修改，支持基本Markdown语法。

```markdown
- [首页](README) 
- [指南](zh-cn/guide)
- **docsify配置**
	- [sidebar配置](docsifyconfig/sidebar.md)
```

## 自动添加文章标题

使用`_sidebar.md`中的链接名称作为对应链接文档的首行标题，也可以指定。

```markdown
- [首页](README) 
- [指南](zh-cn/guide "指定标题")
```

添加配置项到`index.html`

```html
<script>
    window.$docsify = {
		autoHeader: true, //自动添加文章标题
    }
</script>
```

## 在侧边栏显示的最大标题级别

添加配置项到`index.html`

```html
<script>
    window.$docsify = {
		subMaxLevel: 3, //在侧边栏显示的最大标题级别
    }
</script>
```

## 嵌套的侧边栏

- 浏览到一个目录时只显示这个目录自己的侧边栏，可以在每个文件夹中添加一个`_sidebar.md`文件来实现。

```text
.
├── README.md
├── index.html
├── .nojekyll
├── _sidebar.md
└── zh-cn
    ├── README.md
    └── _sidebar.md
```

- `_sidebar.md`的加载逻辑是从每层目录下获取文件，如果当前目录不存在该文件则回退到上一级目录
- 配置 `alias` 避免不必要的回退过程

添加配置项到`index.html`

```html
<script>
    window.$docsify = {
		alias: {
			'/.*/_sidebar.md': '/_sidebar.md' //避免不必要的退回
		},
    }
</script>
```

## 侧边栏中的logo

在侧边栏顶部显示的logo，将`.png`、`.svg`等格式的图片存储到项目内的文件夹中，在`logo`配置项中指定图片路径。

`name`是显示在侧边栏顶部的文字，设置`logo`后会被logo图片覆盖，不设置`name`logo图片无法显示。

添加配置项到`index.html`

```html
<script>
    window.$docsify = {
        name: 'text',
		logo: 'media/logo.svg', //侧边栏中出现的网站图标，点击时会返回README
    }
</script>
```

## 完全隐藏侧边栏

如果你不想使用侧边栏

添加配置项到`index.html`

```html
<script>
  window.$docsify = {
    hideSidebar: true, //完全隐藏侧边栏
  };
</script>
```