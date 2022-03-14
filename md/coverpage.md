## 启用封面
- 创建`_coverpage.md`

```text
.
├── README.md
├── index.html
├── .nojekyll
├── _sidebar.md
├── _navbar.md
└── _coverpage.md
```

- 添加配置项到`index.html`

```html
<script>
  window.$docsify = {
    coverpage: true, //开启封面
  }
</script>
```

### 编辑封面内容

```markdown
![logo](_media/icon.svg)

# docsify <small>3.5</small>

> 一个神奇的文档网站生成器。

- 简单、轻便 (压缩后 ~21kB)
- 无需生成 html 文件
- 众多主题

[GitHub](https://github.com/docsifyjs/docsify/)
[Get Started](#docsify)

<!-- 背景图片 -->

![](_media/bg.png)

<!-- 背景色 -->

![color](#f0f0f0)
```

## 只在访问主页时加载封面

- 默认情况下，封面和你的首页连在一起，可以通过鼠标上下滑动
- 如果你想分开访问，在`index.html`中添加如下配置

```html
<script>
	window.$docsify = {
        onlyCover: true, // 只在访问主页时加载封面
	};
</script>
```

## 多个封面

像侧边栏一样支持嵌套

```text
.
├── README.md
├── index.html
├── .nojekyll
├── _sidebar.md
├── _navbar.md
├── _coverpage.md
└── zh-cn
    ├── README.md
    ├── _sidebar.md
    ├── _navbar.md
    └──_coverpage.md
```