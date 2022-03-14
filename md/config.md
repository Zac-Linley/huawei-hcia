## GitHub挂件

配置仓库地址或者 `username/repo` 的字符串，会在页面右上角渲染一个 [GitHub Corner](http://tholman.com/github-corners/) 挂件。

添加配置项到`index.html`

```html
<script>
    window.$docsify = {
        repo: 'docsifyjs/docsify', //GitHub挂件
        // or
        repo: 'https://github.com/docsifyjs/docsify/', //GitHub挂件
    };
</script>
```

## 切换页面后是否自动跳转到页面顶部

添加配置项到`index.html`

```html
<script>
    window.$docsify = {
        auto2top: true, //切换页面后是否自动跳转到页面顶部
    };
</script>
```

## 首页文件加载路径

不使用`README.md`作为首页

添加配置项到`index.html`

```html
<script>
    window.$docsify = {
        // 入口文件改为 /home.md
        homepage: 'home.md', //首页文件加载路径

        // 文档和仓库根目录下的 README.md 内容一致
        homepage: 'https://raw.githubusercontent.com/docsifyjs/docsify/master/README.md', //首页文件加载路径
    };
</script>
```

## 文档加载的根路径

```html
<script>
    window.$docsify = {
        basePath: '/path/', //文档加载的根路径

        // 直接渲染其他域名的文档
        basePath: 'https://docsify.js.org/', //文档加载的根路径

        // 甚至直接渲染其他仓库
        basePath: 'https://raw.githubusercontent.com/ryanmcdermott/clean-code-javascript/master/', //文档加载的根路径
    };
</script>
```

## 链接使用相对路径

```text
.
├── README.md
├── guide.md
└── zh-cn
    ├── README.md
    ├── guide.md
    └── config
        └── example.md
```

如果 **启用** 了相对路径，当前链接是 `http://domain.com/zh-cn/README` ，对应的链接会解析为：

```
guide.md              => http://domain.com/zh-cn/guide
config/example.md     => http://domain.com/zh-cn/config/example
../README.md          => http://domain.com/README
/README.md            => http://domain.com/README
```

```html
<script>
    window.$docsify = {
        relativePath: true, // 启用相对路径
  
        relativePath: false, // 禁用相对路径（默认值）
    };
</script>
```

## 文档标题跳转地址

```html
<script>
    window.$docsify = {
        nameLink: '/', //文档标题跳转地址

        // 按照路由切换
        nameLink: {
            '/zh-cn/': '/zh-cn/',
            '/': '/',
        }, //文档标题跳转地址
    };
</script>
```

## 替换主题色

```html
<script>
    window.$docsify = {
        themeColor: '#3F51B5', //替换主题色
    };
</script>
```

## 执行文档里的script标签里的脚本

- 类型：`Boolean`

执行第一个script([demo](https://docsify.js.org/#/zh-cn/themes))。如果Vue存在，则自动开启。

```html
<script>
    window.$docsify = {
        executeScript: true, //执行文档里的script标签里的脚本
    };
</script>
```

```
## This is test

<script>
  console.log(2333)
</script>
```

注意如果执行的是一个外链脚本，比如 jsfiddle 的内嵌 demo，请确保引入 [external-script](https://docsify.js.org/#/plugins?id=%e5%a4%96%e9%93%be%e8%84%9a%e6%9c%ac-external-script) 插件。

## 禁用emoji

```html
<script>
    window.$docsify = {
        noEmoji: true, //禁用emoji
    };
</script>
```

如果该选项设为 `false` ，但是你不想解析一些特别的表情符，[参考这里](https://github.com/docsifyjs/docsify/issues/742#issuecomment-586313143)

## 显示文档更新日期

```html
<script>
    window.$docsify = {
        formatUpdated: '{MM}/{DD} {HH}:{mm}', //显示文档更新日期

        formatUpdated: function(time) {
            // ...

            return time;
        },
    };
</script>
```

日期格式：

- `{YYYY}`: full year; eg: **2017**
- `{YY}`: short year; eg: **17**
- `{MM}`: month; eg: **04**
- `{DD}`: day; eg: **01**
- `{HH}`: hours; eg: **06** (24h)
- `{mm}`: minutes; eg: **59**
- `{ss}`: seconds; eg: **09**
- `{fff}`: milliseconds; eg: **555**

## 外部链接的打开方式

```html
<script>
    window.$docsify = {
        externalLinkTarget: '_self', //外部链接的打开方式，'_blank'在新窗口打开
    };
</script>
```

## 右上角链接的打开方式

```html
<script>
    window.$docsify = {
        cornerExternalLinkTarget: '_self', //右上角链接的打开方式，'_blank'在新窗口打开
    };
</script>
```

## 找不到指定页面时加载`_404.md`

```html
<script>
    window.$docsify = {
     notFoundPage: true, //找不到指定页面时加载`_404.md`,'my404.md'自定义路径
    };
</script>
```

## 浏览文档时保持页面顶部有一定空间

```html
<script>
    window.$docsify = {
        topMargin: 90, //浏览文档时保持页面顶部有一定空间 default: 0
    };
</script>
```

> 当你使用'固定页头'布局时这个选项很有用，可以让你的锚点对齐标题栏。