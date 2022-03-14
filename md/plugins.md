
## 主题

```html
<!-- 主题切换器 -->
<link 
	rel="stylesheet" 
	href="//cdn.jsdelivr.net/npm/docsify-darklight-theme@3/dist/docsify-themeable/style.min.css"
	type="text/css">
<!-- Theme: light -->
<link 
	rel="stylesheet" 
	href="https://cdn.jsdelivr.net/npm/docsify-themeable@latest/dist/css/theme-simple.css"
	title="light">
<!-- Theme: Dark -->
<link 
	rel="stylesheet alternative" 
	href="https://cdn.jsdelivr.net/npm/docsify-themeable@latest/dist/css/theme-simple-dark.css"
	title="dark">
<style>
	/* 主题切换器按钮自定义 */
	#docsify-darklight-theme {
		position: fixed;
		right: 20px;
		top: 50px;
		width: 25px;
		height: 25px;
	}

	/*滚动条样式 start*/
    /* 滚动条宽度 */
    ::-webkit-scrollbar {
        width: 4px;
        height: 4px;
    }
    /* 滚动条颜色 */
    ::-webkit-scrollbar-thumb {
        background: #33a9dc;
        background-image: linear-gradient(#6ecd56, #33a9dc, #cb6196, #c16290);
        border-radius: 2em;
    }

	/* 主题自定义样式 */
	:root {
		--base-font-size: 17px;
		/* 正文文字大小 */
		/* --theme-color: rgb(114, 240, 156); 主题颜色 */

		/* Emoji大小 */
		--emoji-size: calc(var(--base-line-height) * 0.6em);

		/* 链接文本样式 */
		--link-border-bottom: ;
		--link-border-bottom--hover: ;
		--link-color: #2694ab;
		--link-color--hover: #e59572;
		--link-text-decoration: underline;
		--link-text-decoration--hover: ;
		--link-text-decoration-color: ;
		--link-text-decoration-color--hover: ;

		/* 图片缩放时的背景颜色 */
		--zoomimage-overlay-background: rgba(3, 3, 3, 0.363);

		/* 分页页脚 */
		--pagination-border-top: ;
		--pagination-chevron-height: 0.8em;
		--pagination-chevron-stroke: currentColor;
		--pagination-chevron-stroke-linecap: round;
		--pagination-chevron-stroke-width: ;
		--pagination-label-color: ;
		--pagination-label-font-size: var(--font-size-s);
		--pagination-title-color: ;
		--pagination-title-font-size: var(--font-size-l);
	}
</style>
<script>
	window.$docsify = {
		themeable: {
          	readyTransition : true, //在等待网站初始化时是否显示一个加载指示器，在初始化完成后再进行淡化过渡(默认为true)
          	responsiveTables: true  // 表格水平翻滚(默认为true)
      	},
	}
</script>
<!-- 主题切换器 -->
<script 
	src="//cdn.jsdelivr.net/npm/docsify-darklight-theme@3/dist/docsify-themeable/main.min.js"
	type="text/javascript">
</script>
<script 
	src="//cdn.jsdelivr.net/npm/docsify-darklight-theme@3/dist/docsify-themeable/index.min.js"
	type="text/javascript">
</script>
```

## mermaid

```html
<script>
    window.$docsify = {
		plugins: [
			function (hook, vm) {
				hook.ready(function () {
					// 类似 jQuery.ready 初始化 mermaid, 禁用自动渲染
					mermaid.initialize({
						startOnLoad: false
					});
				});
				hook.doneEach(function () {
					// 每个页面渲染完成后手动渲染 mermaid 图表
					mermaid.init(undefined, '.mermaid');
				});
			}
		],

        markdown: {
            renderer: {
                code: function (code, lang) {
                    var html = '';
                    // 搜索 mermaid 代码
                    if (code.match(/^sequenceDiagram/) || code.match(/^graph/) || code.match(/^gantt/)) {
                        // 生成一个 mermaid 图表的容器
                        html = '<div class="mermaid">' + code + '</div>';
                    }
                    // 源码自带的 Prism 高亮插件
                    var hl = Prism.highlight(code, Prism.languages[lang] || Prism.languages.markup);
                    // 将图表的容器添加到代码之前
                    return html + '<pre v-pre data-lang="' + lang + '"><code class="lang-' + lang + '">' + hl + '</code></pre>';
                }
            }
        },
    }
</script>
```

## 侧边栏折叠

```html
<head>
    <!-- docsify-sidebar-collapse -->
    <!-- arrow style -->
    <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/sidebar.min.css" />
    <!-- folder style -->
    <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/sidebar-folder.min.css" />
</head>
<body>
	<div id="app"></div>
	<script>
        window.$docsify = {
		sidebarDisplayLevel: 1, //侧边栏显示的标题级别 	
	}
	</script>
	<!-- docsify-sidebar-collapse -->
	<script src="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/docsify-sidebar-collapse.min.js"></script>
</body>
```

- 默认情况下，侧边栏是会一直展开出文档标题外的所有目录
- 你可以添加插件[docsify-sidebar-collapse](https://github.com/iPeng6/docsify-sidebar-collapse)来使他们自动折叠起来

- `sidebarDisplayLevel: 1`用来设置你想显示的标题级别，其他的会自动折叠

- 作者提供了两种风格**箭头**和**文件夹**，如图

![img](https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/202201271801779.gif)

![img](https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/202201271801194.jpeg)

## 全文搜索

```html
<script>
	window.$docsify = {
		search: {
        	maxAge: 86400000, //过期时间，单位ms
			paths: 'auto', //或填写路径[]
        	placeholder: '输入搜索内容', //默认为'Type to search'
        	noData: '⛔没有找到搜索结果', //默认为'No Results!'
        	depth: 6,// 搜索标题的最大层级, 1 - 6
        	hideOtherSidebarContent: true, // 是否隐藏其他侧边栏内容
        	namespace: 'website-1' // 避免搜索索引冲突(同一域下的多个网站之间) ,使用不同的索引作为路径前缀（namespaces）注意：仅适用于 paths: 'auto' 模式
      	},
	}
</script>
<!-- plugin-search -->
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
```

## [sidebar-footer](https://markbattistella.github.io/docsify-sidebarFooter-docs/#/)

> 此插件可以在侧边栏（或页面）的底部创建一个页脚区域，可以显示版权年份、公司名称、网站链接、隐私政策、cookies等

```html
<script>
	window.$docsify = {
		autoFooter: {
			name: linley, //String 公司显示名称（必填）
			copyYear: 2022, //Int 开始版权年（必填）
			url: 'docs.lzxblog.top', //String 公司网址（可选）
			policy:, //Bool | String 显示隐私政策（可选）
			terms:, //Bool | String 显示服务条款（可选）
			cookies:, //Bool | String 显示Cookies政策（可选）
			onBody: false //Bool 如果是'true'，就在主界面下方显示
  		},
	}
</script>
<!-- plugin-sidebar-footer -->
<script src="https://cdn.jsdelivr.net/npm/@markbattistella/docsify-sidebarfooter@latest"></script>
```

- 当你配置好之后发现并没有显示在侧边栏
- 需要在`_sidebar.md`中添加如下代码来启用

```markdown
<footer id="mb-footer"></footer>
```

## External Script

如果文档里的`<script>`是内联脚本，可以直接执行；而如果是外链脚本（即 js 文件内容由 `src` 属性引入），则需要使用此插件。

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/external-script.min.js"></script>
```

## emoji :id=emoji

默认设置是支持解析表情符号。能将类似`:100:`解析为:100:。但它并不精确，因为没有处理非 emoji 的字符串。如果你需要正确解析emoji字符串，你可以引入这个插件。

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/emoji.min.js"></script>
```

> 如果您不想解析为表情符号，可以使用`__colon__`或 `&#58;`，如果需要在标题中使用，我们建议您使用`&#58;`。例如`&#58;100:`

## 按钮样式 :id=button1

- docsify是支持`<button></button>`来创建一个<button class=button>按钮</button>的，但是官方主题的按钮确实不是很好看
- 添加这段代码到`index.html`中，你会得到一个和我这个一样的按钮
- 如果你会`css`自定义主题，请跳过

```html
<head>	
	<style>
		.button {
			-webkit-transition-duration: 0.4s;
			transition-duration: 0.4s;
			padding: 1.5px 10px;
			text-align: center;
			background-color: #f2f4f6;
			color: black;
			border: 2px solid #4CAF50;
			border-radius:5px;
		}
		.button:hover {
			background-color: #4CAF50;
			color: white;
		}
	</style>
</head>
```

> 方法来自知乎《[如何用HTML实现简单按钮样式](https://zhuanlan.zhihu.com/p/145914159)》

## 代码高亮

docsify内置的代码高亮工具是Prism，默认支持的语言如下：

- Markup - `markup`, `html`, `xml`, `svg`, `mathml`, `ssml`, `atom`, `rss`
- CSS - `css`
- C-like - `clike`
- JavaScript - `javascript`, `js`

[添加额外的语法支持](https://prismjs.com/#supported-languages)需要通过CDN添加相应的[语法文件](https://cdn.jsdelivr.net/npm/prismjs@1/components/)

```html
<!-- powershell代码高亮 -->
<script src="//cdn.jsdelivr.net/npm/prismjs/components/prism-powershell.min.js"></script>
```

## 复制到剪贴板

在所有的代码块上添加一个简单的`Click to copy`按钮来允许用户从你的文档中轻易地复制代码。由[@jperasmus](https://github.com/jperasmus)提供。

```html
window.$docsify = {
	// 复制代码到剪贴板
	copyCode: {
		buttonText: '复制到剪切板',
		errorText: '错误',
		successText: '已复制'
	}
}
<script src="//cdn.jsdelivr.net/npm/docsify-copy-code/dist/docsify-copy-code.min.js"></script>
```

## 顶部横幅-[topbanner](https://github.com/Plugin-contrib/docsify-plugin/tree/master/packages/docsify-top-banner-plugin)

![img](https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/202201281001846.png ':size=35%')

在`index.html`中添加如下：

```html
<head>
    <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify-top-banner-plugin@latest/dist/style.css" />  
</head>
<boday>
    <div id="app">Loading</div>
    <script>
    	window.$docsify = {
        	topBanner: {
        		position: 'relative',//String 'relative' 'fixed'
        		textAlign: 'center', //对齐方式'right' 'left' 'center'
        		linkColor: '#3b8686', //链接字体颜色
        		textColor: '#fe5f55', //文本字体颜色
        		backgroundColor: '#FFF5C3', //背景颜色
        		zIndex: '-1', //元素覆盖优先级
        		content: 'bala bala' //横幅内容
        	},
		}
	</script>
	<script src="https://cdn.jsdelivr.net/npm/docsify-top-banner-plugin@latest/dist/index.js"></script>
</boday>
```

## 分页页脚-[pagination](https://github.com/imyelo/docsify-pagination)

```html
<script>
    window.$docsify = {
		pagination: {
			previousText: '上一章节', //String 默认'PREVIOUS'跳转到上一页的标签文本
			nextText: '下一章节', //String 默认'NEXT'跳转到下一页的标签文本
			crossChapter: true, //Boolean 默认false 允许导航到上一章/下一章
			crossChapterText: true, //Boolean 默认false 显示章节名称
		}, 
	}
</script>
<script src="//unpkg.com/docsify-pagination/dist/docsify-pagination.min.js"></script>
```

## 文本分栏-[slides](https://github.com/shawntabrizi/docsify-slides) :id=slides-plugin

```html
<script src="//unpkg.com/docsify-slides/dist/docsify-slides.min.js"></script>
```

> **注意：**此插件与[`docsify-pagination`](https://github.com/imyelo/docsify-pagination)插件结合使用效果最佳。请务必在您的 docsify 网站上启用此插件，以获得完整的体验。

如何使用请参考[文档助手](md/helper.md#slides-ed)

## [Charty图表](https://markbattistella.github.io/docsify-charty-docs/#/?id=pie) :id=charty-plugin

```charty
{
  "title":   "Area chart",
  "caption": "With a caption",
  "type":    "area",
  "options": {
    "legend":  true,
    "labels":  true,
    "numbers": true
  },
  "data": [
    {
        "label": "2010",
        "value": [120, 23, 45, 34, 52, 43, 59, 40]
     }
  ]
}
```

包含了多种类型图表的插件，具体使用方法参考[文档助手](md/helper.md#charty-ed)

```html
<head>
    <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/@markbattistella/docsify-charty@latest/dist/docsify-charty.min.css">
</head>    
<boday>
    <script>
		window.$docsify = {
            charty: {
            theme: '#348498',//String 全局主题颜色，支持HEX
            mode:  'light',//String 主题模式，'light' 或 'dark'
            debug: 'false'//如果图表没有加载，控制台的日志就会出现
        	},
		}
    </script>
    <script src="//cdn.jsdelivr.net/npm/@markbattistella/docsify-charty@latest"></script>
</boday>
```

## 字数统计

![image-20220128135341695](https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/202201281353727.png)

在页面右上角显示文档的字数统计和阅读时间，可以修改字体大小或颜色等

```html
<script>
    window.$docsify = {
		count:{
			countable:true,
			fontsize:'0.9em',
			color:'rgb(90,90,90)',
			language:'chinese'
		},
	}
</script>
<script src="//unpkg.com/docsify-count/dist/countable.js"></script>
```

## 公式-[katex](https://github.com/upupming/docsify-katex) :id=katex-plugin

可以在docsify中插入katex公式的插件，查看[支持的符号和公式的列表](https://katex.org/docs/support_table.html)，使用方法参考[文档助手](md/helper.md#katex-ed)

```html
<!-- CDN files for docsify-katex -->
<script src="//cdn.jsdelivr.net/npm/docsify-katex@latest/dist/docsify-katex.js"></script>
<!-- or <script src="//cdn.jsdelivr.net/gh/upupming/docsify-katex@latest/dist/docsify-katex.js"></script> -->
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/katex@latest/dist/katex.min.css"/>
```

## 拓展提示文本块-[Flexible Alerts](https://github.com/fzankl/docsify-plugin-flexible-alerts) :id=flexible-a-plguin

![img](https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/202201281445993.jpeg)

拓展了4种类型的提示文本块，你也可以按照规则自定义多种风格，使用规则参考[文档助手](md/helper.md#flexible-a-ed)

```html
<script>
	window.$docsify = {
        'flexible-alerts': {
			style: 'flat', //风格样式 'callout'(图片左) or 'flat'(图片右)
			note: {
				label: "Hinweis"
			},
			tip: {
				label: "Tipp"
			},
			warning: {
				label: "Warnung"
			},
			attention: {
				label: "Achtung"
			}
		},
	}
</script>
<!-- Flexible Alerts -->
<script src="//unpkg.com/docsify-plugin-flexible-alerts"></script>
```

## Gitalk评论系统

[Gitalk](https://github.com/gitalk/gitalk)，一个现代化的，基于Preact和Github Issue的评论系统。

```html
<link rel="stylesheet" href="//cdn.jsdelivr.net/npm/gitalk/dist/gitalk.css">

<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/gitalk.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/gitalk/dist/gitalk.min.js"></script>
<script>
  const gitalk = new Gitalk({
    clientID: 'Github Application Client ID',
    clientSecret: 'Github Application Client Secret',
    repo: 'Github repo', //Github仓库名称
    owner: 'Github repo owner', //Github名称
    admin: ['Github repo collaborators, only these guys can initialize github issues'], //不知道的填自己的Github名称就好
    // facebook-like distraction free mode
    distractionFreeMode: false
  })
</script>
```

### 申请 GitHub OAuth application

打开[GutHub](https://github.com/)，点击右上角**头像**，先择**Setting**，找到最下面的**Developer settings**选项，选择**OAuth Apps**, 然后会在页面右边有一个**New OAuth App** 按钮，点击这个按钮就进入到新建OAuth application页面。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/202201281713195.jpeg" width=500>

完成之后就可以找到你自己的`Client ID`与`Client Secret`了

### 问题

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/202201281719774.png" width= 500>

> [!NOTE]
>
> 如果出现这样的提示，使用自己的GitHub账号登陆一下就可以了

## 返回顶部按钮

```html
<script>
	window.$docsify = {
		// ...
		scrollToTop: {
			auto: true,
			text: 'Top',
			right: 15,
			bottom: 15,
			offset: 500
		}
	};
</script>
<!-- 回到顶部功能 -->
<script src="//unpkg.com/docsify-scroll-to-top/dist/docsify-scroll-to-top.min.js"></script>
```

## 为每个文档化标记添加更新时间

```html
<script>
	timeUpdater: {
		text: "🕒<font color='#a39e9e'>最后修改: {docsify-updated}</font>",
		formatUpdated: "{YYYY}-{MM}-{DD} {HH}:{mm}",
	},
</script>
<!-- 为每个文档化标记添加更新时间 -->
<script src="https://cdn.jsdelivr.net/npm/docsify-updated@1/src/time-updater.min.js"></script>
```

## 右侧二维码

```html
<style>
	/* 右侧二维码 */

	.advertisement {
		position: fixed;
		right: 20px;
		top: 100px;
		width: 110px;
		box-shadow: -1px 0 2px 0px #c5ebda;
		padding: 10px;
		z-index: 99;
		background-color: #fff;
		text-align: center;
	}

	.advertisement p,
	h4 {
		margin: 0;
		padding: 0;
	}

	.advertisement .Tencent_code h4 {
		font-size: 15px;
		color: #25a46a;
		margin-bottom: 10px;
	}
</style>
<body>
	<!-- 右侧二维码 -->
	<div class="advertisement">
	<div class="Tencent_code">
	<h4>关注作者公众号</h4>
	<p style="font-size: 12px;">万千小伙伴陪你一起学</p>
	<img src="https://cdn.jsdelivr.net/gh/wugenqiang/PictureBed/images01/20200808182633.jpg" alt="EnjoyToShare" />
	</div>
	</div>
<body>
```

## 其他自定义样式

```html
<!-- 自定义样式 -->
    <style>
        /* 按钮样式 */

        .button1 {
            -webkit-transition-duration: 0.4s;
            transition-duration: 0.4s;
            padding: 2px 10px;
            text-align: center;
            background-color: white;
            color: black;
            border: 2px solid #4CAF50;
            border-radius: 5px;
        }

        .button1:hover {
            background-color: #4CAF50;
            color: white;
        }

        nav.app-nav li ul {
            min-width: 100px;
        }

        /*滚动条样式 start*/
        /* 滚动条宽度 */

        ::-webkit-scrollbar {
            width: 4px;
            height: 4px;
        }

        /* 滚动条颜色 */

        ::-webkit-scrollbar-thumb {
            background: #33a9dc;
            background-image: linear-gradient(#6ecd56, #33a9dc, #cb6196, #c16290);
            border-radius: 2em;
        }

        /* ali图标样式-用于navbar */
        .icon {
            width: 1em;
            height: 1em;
            vertical-align: -0.15em;
            fill: currentColor;
            overflow: hidden;
        }

        /* ali图标样式1-用于正文 */
        .icon1 {
            width: 2em;
            height: 2em;
            vertical-align: -0.15em;
            fill: currentColor;
            overflow: hidden;
        }

        /* ali图标样式2-用于标题 */
        .icon2{
            width: 1.4em;
            height: 1.4em;
            vertical-align: -0.34em;
            fill: currentColor;
            overflow: hidden;
        }
    </style>
```

## 术语表

在`index.html`中添加脚本

```html
<script src="//unpkg.com/docsify-glossary/dist/docsify-glossary.min.js"></script>
```

在根目录中创建`_glossary.md`文档，编辑内容如下：

```md
##### glossary
glossary是一个docsify插件，用于自定义术语。
```

- 每一条术语都要使用5级标题`#####`开头
- 下一行为术语的解释内容
- 在文档中引用时术语的前后需追加**空格**` glossary `

## 图片缩放

```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/zoom-image.min.js"></script>
```

个别图片不适用缩放

```md
![](image.png ":no-zoom")
```