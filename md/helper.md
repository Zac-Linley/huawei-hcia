## 一般引用

```md
> 一般引用文本
```

> 一般引用文本

## 重要提示

适合显示重要的提示信息，语法为 `!> 内容`。

```markdown
!> 一段重要的内容，可以和其他 **Markdown** 语法混用。
```

!> 一段重要的内容，可以和其他 **Markdown** 语法混用。

## 普通提示

普通的提示信息，比如写 TODO 或者参考内容等。

```markdown
?> _TODO_ 完善示例
```

?> _TODO_ 完善示例

## 提示拓展 :id=flexible-a-ed

!> 使用此功能的前提是[安装Flexible-Alerts插件](md/plugins.md#flexible-a-plguin)

```mark
> [!NOTE]
> An alert of type 'note' using global style 'callout'.

> [!TIP]
> An alert of type 'tip' using global style 'callout'.

> [!WARNING]
> An alert of type 'warning' using global style 'callout'.

> [!ATTENTION]
> An alert of type 'attention' using global style 'callout'.

> [!NOTE|style:flat]
> An alert of type 'note' using alert specific style 'flat' which overrides global style 'callout'.
```

> [!NOTE]
> An alert of type 'note' using global style 'callout'.

> [!TIP]
> An alert of type 'tip' using global style 'callout'.

> [!WARNING]
> An alert of type 'warning' using global style 'callout'.

> [!ATTENTION]
> An alert of type 'attention' using global style 'callout'.

> [!NOTE|style:flat]
> An alert of type 'note' using alert specific style 'flat' which overrides global style 'callout'.

## 忽略编译链接

有时候我们会把其他一些相对路径放到链接上，你必须告诉 docsify 你不需要编译这个链接。 例如：

```md
[link](/demo/)
```

它将被编译为 `<a href="/#/demo/">link</a>` 并将加载 `/demo/README.md`. 可能你想跳转到 `/demo/index.html`。

现在你可以做到这一点

```md
[link](/demo/ ':ignore')
```

即将会得到 `<a href="/demo/">link</a>` html 代码。不要担心，你仍然可以为链接设置标题。

```md
[link](/demo/ ':ignore title')

<a href="/demo/" title="title">link</a>
```

## 设置链接的 target 属性

```md
[link](/demo ':target=_blank')
[link](/demo2 ':target=_self')
```

## 禁用链接

```md
[link](/demo ':disabled')
```

## 跨域链接

只有当你同时设置了 `routerMode: 'history'` 和 `externalLinkTarget: '_self'` 时，你需要为这些跨域链接添加这个配置。

```md
[example.com](https://example.com/ ':crossorgin')
```

## 忽略副标题

- 侧边栏中是自动忽略markdown文档中的一级标题的
- 如果你需要忽略其他级别的标题，在markdown的标题后添加`<!-- {docsify-ignore} -->`

```markdown
## Header 2 <!-- {docsify-ignore} -->
```

## 列表

```md
**有序列表**

1. Ordered 1
1. Ordered 2
   1. Ordered 2a
   1. Ordered 2b
   1. Ordered 2c
1. Ordered 3

**无序列表**

- Unordered 1
- Unordered 2
  - Unordered 2a
  - Unordered 2b
  - Unordered 2c
- Unordered 3

**任务列表**

- [x] Task 1
- [ ] Task 2
  - [x] Subtask A
  - [ ] Subtask B
- [ ] Task 3

```

**有序列表**

1. Ordered 1
1. Ordered 2
   1. Ordered 2a
   1. Ordered 2b
   1. Ordered 2c
1. Ordered 3

**无序列表**

- Unordered 1
- Unordered 2
  - Unordered 2a
  - Unordered 2b
  - Unordered 2c
- Unordered 3

**任务列表**

- [x] Task 1
- [ ] Task 2
  - [x] Subtask A
  - [ ] Subtask B
- [ ] Task 3

## 图片处理

### 缩放

```md
![logo](https://docsify.js.org/_media/icon.svg ':size=WIDTHxHEIGHT')
![logo](https://docsify.js.org/_media/icon.svg ':size=50x100')
![logo](https://docsify.js.org/_media/icon.svg ':size=100')

<!-- 支持按百分比缩放 -->

![logo](https://docsify.js.org/_media/icon.svg ':size=10%')
```

![logo](https://docsify.js.org/_media/icon.svg ':size=50x100')
![logo](https://docsify.js.org/_media/icon.svg ':size=100')
![logo](https://docsify.js.org/_media/icon.svg ':size=10%')

### 设置图片的 Class

```md
![logo](https://docsify.js.org/_media/icon.svg ':class=someCssClass')
```

### 设置图片的 ID

```md
![logo](https://docsify.js.org/_media/icon.svg ':id=someCssId')
```

## 设置标题的 id 属性

```md
### 你好，世界！ :id=hello-world
```

引用标题id链接

```markdown
[你好](example/helpers.md#hello-world)
```

## html 标签中的 Markdown

你需要在 html 和 Markdown 内容中插入空行。
当你需要在 details 元素中渲染 Markdown 时很有用。

```markdown
<details>
<summary>自我评价（点击展开）</summary>

- Abc
- Abc

</details>
```

<details>
<summary>自我评价（点击展开）</summary>

- Abc
- Abc

</details>

Markdown 内容也可以被 html 标签包裹。

```markdown
<div style='color: red'>

- listitem
- listitem
- listitem

</div>
```

<div style='color: red'>

- Abc
- Abc

</div>

## 角标

```md
这是<sub>下标</sub>

这是<sup>上标</sup>
```

这是<sub>下标</sub>

这是<sup>上标</sup>

## 按钮

可以使用`<button class='button1'></button>`来创建一个<button class= "button1">按钮</button>，设置`class='button1'`的原因是在`index.html`中添加了`.button1`的[自定义按钮样式](#button1)，如果你需要让按钮指向一个链接，请使用`<a></a>`来实现

```html
<a href="https://docsify.js.org/"><button class= 'button1'>docsify官网</button></a>
```

<a href="https://docsify.js.org/"><button class= 'button1'>docsify官网</button></a>

## 文本分栏 :id=slides-ed

!> 使用此功能的前提是[安装slides插件](md/plugins.md#slides-plugin)

```md
民十北美设合低现华无，见阶音将己办究过，你少弦加于求王伸。 万最过指事美车面回把由京，却公计进孤气属详奔。 系至就型可统所酸住相，放因段何F抓江十。 用多表干维条严习，江完F华重。 确查无感部小里音眼，周把图发查生亲任，经消材入秧引写处。
<!-- slide:break -->
美把难省向开今场，度水准特格务你历，长Y询度半件。 你引技么我大度情证改回之，八统接思8步按表盛。 装住阶知全放走结复实阶，义关军决承地示号。
```

![image-20220125223058608](https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/202201281048813.png)

### 也可也设置左右占比

```md
民十北美设合低现华无，见阶音将己办究过，你少弦加于求王伸。 万最过指事美车面回把由京，却公计进孤气属详奔。 系至就型可统所酸住相，放因段何F抓江十。 用多表干维条严习，江完F华重。 确查无感部小里音眼，周把图发查生亲任，经消材入秧引写处。
<!-- slide:break-30 -->
美把难省向开今场，度水准特格务你历，长Y询度半件。 你引技么我大度情证改回之，八统接思8步按表盛。 装住阶知全放走结复实阶，义关军决承地示号。
```

![image-20220125223559044](https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/202201281048940.png)

## 插入图表 :id=charty-ed

!> 使用此功能的前提是[安装charty插件](md/plugins.md#charty-plugin)

````markdown
```charty
{
  "title":   '',  #String 图表的标题，显示在顶部。如果你想隐藏它，请留空
  "caption": '',  #String 图表的子文本，显示在标题下。如果你想隐藏它，请留空
  "type":    '',  #String 你想显示的图表类型 
  "options": {
    "theme":   '',  #String 为这个图表设置一个单独的主题。它将覆盖全局主题
    "legend":  '',  #Boolean 显示图表说明，默认为 'true'
    "labels":  '',  #Boolean 显示图表标签，默认为 'true'
    "numbers": ''  #Boolean 鼠标悬停时显示折点数字，默认为 'true'
  },
  "data": [
    {
      "label": '',  #String 图形化的数据点标签
      "value": '',  #Int / Array 数值
      "colour": ''  #String 用一个特定的颜色覆盖全局主题和选项中的主题
    }
  ]
}
```
````

```charty
{
  "title":   "Radar chart",
  "caption": "With a caption",
  "type":    "radar",
  "options": {
    "legend":  true,
    "labels":  true,
    "numbers": true
  },
  "data": [
    {
        "label": "iPhone",
        "value": [64, 23, 45, 34, 52, 43, 59, 40],
        "points": [
            "Features",
            "Style",
            "Usability",
            "Ratings",
            "Apps",
            "Softness",
            "Ruggedness",
            "Appeal"
        ]
    },
    {
        "label": "Android",
        "value": [86, 53, 55, 66, 80, 46, 49, 40]
    },
    {
        "label": "Chrome",
        "value": [100, 35, 76, 90, 36, 9, 0, 90]
    }
  ]
}
```

### charty提供的图表类型

- area
- radar
- doughnut
- section
- rings
- plot
  - scatter
  - bubble
- line
- bar
  - bar
  - colum
  - bar-stacked
  - colum-stacked
- Rating
  - review

## 插入公式 :id=katex-ed

!> 使用此功能的前提是[安装katex插件](md/plugins.md#katex-plugin)

```markdown
$E=mc^2$
```

$ E=mc^2 $

katex支持的公式列表和书写规则，查看[官方文档](https://katex.org/docs/support_table.html)

## 标记文本

```md
<mark>Marked text</mark>
```
<mark>Marked text</mark>

## 键盘按键

```md
<kbd>&uarr;</kbd> 上箭头

<kbd>&darr;</kbd> 下箭头

<kbd>&larr;</kbd> 左箭头

<kbd>&rarr;</kbd> 右箭头

<kbd>&#8682;</kbd> 大写锁定

<kbd>&#8984;</kbd> Command

<kbd>&#8963;</kbd> Control

<kbd>&#9003;</kbd> Delete

<kbd>&#8998;</kbd> Delete (Forward)

<kbd>&#8600;</kbd> End

<kbd>&#8996;</kbd> Enter

<kbd>&#9099;</kbd> Escape

<kbd>&#8598;</kbd> Home

<kbd>&#8670;</kbd> Page Up

<kbd>&#8671;</kbd> Page Down

<kbd>&#8997;</kbd> Option, Alt

<kbd>&#8629;</kbd> Return

<kbd>&#8679;</kbd> Shift

<kbd>&#9251;</kbd> Space

<kbd>&#8677;</kbd> Tab

<kbd>&#8676;</kbd> Tab + Shift
```

<kbd>&uarr;</kbd> 上箭头

<kbd>&darr;</kbd> 下箭头

<kbd>&larr;</kbd> 左箭头

<kbd>&rarr;</kbd> 右箭头

<kbd>&#8682;</kbd> 大写锁定

<kbd>&#8984;</kbd> Command

<kbd>&#8963;</kbd> Control

<kbd>&#9003;</kbd> Delete

<kbd>&#8998;</kbd> Delete (Forward)

<kbd>&#8600;</kbd> End

<kbd>&#8996;</kbd> Enter

<kbd>&#9099;</kbd> Escape

<kbd>&#8598;</kbd> Home

<kbd>&#8670;</kbd> Page Up

<kbd>&#8671;</kbd> Page Down

<kbd>&#8997;</kbd> Option, Alt

<kbd>&#8629;</kbd> Return

<kbd>&#8679;</kbd> Shift

<kbd>&#9251;</kbd> Space

<kbd>&#8677;</kbd> Tab

<kbd>&#8676;</kbd> Tab + Shift

## 水平分割线

```md
---
```

---
