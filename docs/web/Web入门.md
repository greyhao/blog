## Web 入门

### HTML

**HyperText Markup Language，超文本标记语言**，不是编程语言，是告知浏览器如何组织页面的标记语言，由 一系列*元素（elements）*组成，使用*标签（tag）*来创建元素（标签来识别元素的开始或结束，元素是 DOM 中的一部分）。典型的元素包括：具有一些属性的开始标签，中间的文本内容和一个结束标签。



####元素的结构

![HTML 元素](https://tva1.sinaimg.cn/large/e6c9d24ely1h2zv1m3e7vj20g8073mxg.jpg)



元素的主要部分：

* 开始标签（Opening tag）：包含元素的名称，被左、右角括号包围
* 结束标签（Closing tag）：与开始标签相似，但是在元素名之前包含一个斜杠
* 内容（Content）：元素的内容
* 属性：位于开始标签中
  * 一般属性包含：属性名等号属性值，例如：`<a herf = "httsp://xx.xx.com">xx</a>`
  * 布尔属性：没有值的属性，这些属性只有跟属性名相同的属性值，例如：`<input type="text" disabled>`
* 元素（Element）：开始标签、结束标签与内容相结合



**不同的标签有不同的语义，语义很重要。**



#### 块级元素、内联元素、空元素

* 块级元素在页面中以块的形式展现 --- 相对于其前面的内容会出现在新的一行，其后面的内容也会被挤到下一行。通常用于展示页面上结构化的内容，例如段落、列表、导航菜单、页脚等。以 block 形式展现的块级元素不会被嵌套进内联元素，但是可以嵌套在其他块级元素中。
* 内联元素通常出现在块级元素中并环绕文档内容中的一小部分，而不是一整个段落或一组内容。内联元素不会导致文本换行：它通常出现在一堆文件之间例如超链接元素 `<a>` 或强调元素 `<em>` 和 `<strong>`。
* 不包含任何内容的元素或只有一个标签的元素称为空元素（void elements），比如 `img` 标签。



#### 特殊字符

| 原义字符 | 等价字符引用 |
| -------- | ------------ |
| <        | `&lt;`       |
| >        | `&gt;`       |
| "        | `&quot;`     |
| '        | `&apos;`     |
| &        | `&amp;`      |



#### head 标签

header 标签中的内容不会在页面中显示出来，包含：

* title：在浏览器标签中显示；保存书签时的默认书签名

* CSS 的链接、JavaScript 脚本

  添加方式

  ```html
  <!-- CSS -->
  <link rel="stylesheet" href="my-css-file.css">
  
  <!-- JavaScript -->
  <!-- 非必须放在 head 中；defer 解析所有 HTML 内容之后再加载 js 文件 -->
  <script src="my-js-file.js" defer></script>
  ```

  

* 自定义图标的链接：网站添加自定义图标（favicon），在浏览器收藏或书签中显示

  添加方式：将图片放到项目中或使用图片链接，添加如下代码，href 的值为图片路径

  ```html
  <head>
    ...
    <link type="image/x-icon" rel="icon" href="./favicon.ico">
    ...
  </head>
  ```



* 其它的元数据（描述 HTML 的数据，比如：作者和描述文档的关键词）等信息

* meta：元数据

  * charset：设置文档的字符编码

  * 包含 name，content 属性

    * name：指定 meta 元素的类型：authon 作者、description 描述：用来搜索引擎优化
    * content：指定了实际的元数据内容

  * 其他元数据

    * FaceBook 元数据协议：Open Graph data，当在 FaceBook 链接到网址时，显示设置的内容

      ```html
      <meta property="og:image" content="想要显示的图片的链接地址">
      <meta property="og:description" content="想要显示的描述">
      <meta property="og:title" content="想要显示的标题">
      ```

      

    * Twitter 元数据协议： Twitter Cards，当网站的 URL 显示在 twitter.com 上时，具有类似的效果

      ```html
      <meta name="twitter:title" content="想要显示的标题">
      ```





```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="author" content="grey">
    <meta name="description" content="grey wrote this page.">
    <link rel="icon" href="./favicon.ico" type="image/x-icon">
    <link type="stylesheet" href="../styles/style.css" />
    <script src="../scripts/element.js" defer></script>
    <title>我是Title</title>
  </head>
  <body>
  </body>
</html>
```



#### 为文档设置主语言

```html
<!-- 设置文档主语言 -->
<html lang="zh-CN">
  ...
</html>

<!-- 设置局部语言 -->
<p>
  Japennes example: <span lang="ja">ご飯が熱い。</span>.
</p>
```





####常用标签

内联元素：

​	

| 标签   | 功能                           | 常用属性                                                     | 使用场景                                                 |
| ------ | ------------------------------ | ------------------------------------------------------------ | -------------------------------------------------------- |
| em     | 斜体文字                       |                                                              |                                                          |
| i      | 斜体文字                       |                                                              | 外国文字、<br />分类名称、<br />技术术语、<br />一种思想 |
| strong | 文字加粗                       |                                                              |                                                          |
| b      | 文字加粗                       |                                                              | 关键字、<br />产品名称、<br />引导句                     |
| u      | 文字加下划线                   |                                                              | 专有名词、<br />拼写错误                                 |
| a      | 超链接                         | href：超链接的地址<br />traget：指定链接如何呈现出来，<br />值为 _blank 时在新标签中显示链接，默认在当前页打开<br />title：鼠标悬停时提示<br />download：给下载资源指定默认的保存文件名<br />href="mailto:xx"： 发送邮件（打开邮箱客户端，xx 邮件地址非必须项） | 链接 url、<br />块级链接、<br />文档片段、               |
| sub    | 下标                           |                                                              |                                                          |
| sup    | 上标                           |                                                              |                                                          |
| code   | 代码（计算机语言）             |                                                              |                                                          |
| pre    | 保留空白字符（通常用户代码块） |                                                              |                                                          |
| var    | 标记具体变量名                 |                                                              |                                                          |
| kbd    | 标记输入电脑的键盘输入         |                                                              |                                                          |
| samp   | 标记计算机程序的输出           |                                                              |                                                          |
|        |                                |                                                              |                                                          |

​	em： 斜体

​	strong：粗体

​	a：超链接，属性

块级元素：

| 标签                   | 功能     | 常用属性                         |
| ---------------------- | -------- | -------------------------------- |
| p                      | 段落     |                                  |
| h1、h2、h3、h4、h5、h6 | 标题     |                                  |
| ul                     | 无序列表 | 每一项都是 li                    |
| ol                     | 有序列表 | 每一项都是 li                    |
| dl                     | 描述列表 | 每一项是 dt<br />每一个描述是 dd |
|                        |          |                                  |
|                        |          |                                  |



#### 超链接

`<a>` 实现超链接

```html
<!-- 基本用法 -->
<a href="https://google.com" title="Google 搜索">打开 Google</a>

<!-- 块级链接 -->
<a href="https://google.com">
  <img src="./google.png" alt="open google">
</a>

<!-- 文档片段(当前页面，其他页面都可以)  1，设置 id 属性；2，链接到 id -->
<h2 id="name">标题</h2>
<!-- 当前页面 -->
<p>点击<a herf="#name">回到标题</a></p>
<!-- 其他页面 -->
<p>查看<a herf="../content.html#name">回到标题</a></p>

<!-- 发送邮件 -->
<a href="mailto:h@1.com">发送邮件</a>
<!-- 发送邮件 设置抄送人、主题-->
<a href="mailto:h@1.com?cc=n@2.com&subject=This%20is%20the%20subject">发送邮件</a>

```



#### 引用

* 块级引用

  使用 `blockquote` 标签，渲染块引用时默认会增加缩紧

  ```html
  <blockquote cite="引用资源链接">
    具体引用内容
  </blockquote>
  ```

* 行内引用

  使用 `q` 标签，引用内容会放入引号内

  ```html
  <p>
    <code>&lt;q&gt;</code> - is <q cite="引用资料链接">具体引用内容</q>
  </p>
  ```

cite 属性不展示，使用 a + cite 标签显示引文，引文默认的字体样式是斜体。

```html
<p>
	mdn p 标签介绍
	<q cite="https://baidu.com">p is axxxxxx</q>
	<a href=""><cite>MDN page</cite></a>
</p>
```



#### 缩略语

标签 `abbr`， title 属性的值是缩写的解释，鼠标在标签内容上时显示解释。

```html
<p>
  使用 <abbr title="超文本标记语言">HTML</abbr> 来组织网页文档。
</p>
```



#### 标记联系方式

标签 `address`，为了标记编写 HTML 文档的人的联系方式。



#### 文档常用元素

#####有语义元素

* `main ` ：位于 body 中，用来存放每个页面独有的内容，每个页面只能有一个
* `article`：文章，经常嵌套到 main 中
* `section`：将页面用来按功能分块
* `aside`：包含间接信息，例如：外链，经常嵌套在 main 中
* `header`：页眉，在 body 中则是全局页眉，在 article 或 section 中，则为该部分的页眉
* `nav`：包含页面的主导航栏，可以放在 header 中
* `footer`：页脚

##### 无语义元素

*注意：无法找到更好的语义元素时使用无语义元素*

* `div`：块级元素
* `span`：内联元素

##### 换行和水平分割线

* `br`：换行
* `hr`：水平分割线，一条水平的直线



####多媒体

#####img

`img`： 图片， 属性：alt：图片无法显示时显示的描述，图片大小建议在 CSS 中设置

```html
<img src="./a.png" alt="示例图片" title="鼠标悬停在图片时显示的信息">
```

#####video

`video`：视频，

* src：视频源
* controles： 控制播放的按钮，
* 标签内的内容：后备内容，浏览器不支持 vidoe 标签的时候会显示
* poster：视频封面图片
* width、height：支持宽高设置，不会改变视频比例，视频仍按自己的比例播放，比例不一致会留白

```html
<video src="./aa.webm" controls poster="../../images/monkey.jpg">
  <p>不支持 HTML5 视频，点击<a href="./aa.mp4"></a>观看</p>
</video>


<!-- 另一个种写法，提供多个source，自动匹配第一个支持的格式  -->
<video controls>
  <source src="./a.webm" type="video/webm">
  <source src="./a.mp4" type="video/mp4">
  <p>不支持 HTML5 视频，点击</p><a href="./aa.mp4"></a>观看</p>
</video>
```



#####audio

`audio`：音频

* controles：  播放控制
* src：音频源
* 同 video 的不同： 不支持设置宽/高、poster，其他属性一致



WebVTT 格式文件后缀为 .vtt ，包含元数据，用来给视频/音频显示字幕。

kind 属性值包括：

​		subtitles ：不同语言的字幕

​		captions：同步翻译对白，描述重要信息的声音，帮助不能听音频的人处理音频中的内容

​		descriptions：文字转为音频，服务视觉障碍的人

```html
<video controls>
	<source src="xx.mp4" type="video/mp4">
  <srouce src="xx.webm" type="video/webm">
  <track kind="subtitles" src="xx_en.vtt" srclang="en">
</video>
```



js 中，通过 load() 方法重新加载媒体文件。



#####figure

`figure`，`figcaption`  语义容器，使用 `figcaption`  的内容描述说明 figure 元素的内容。

figure 中可以是图片、代码、音视频等内容。

```html
<figure>
	<img src="../../images/monkey.jpg" alt="monkey image" />
  <figcaption>图片描述</figcaption>
</figure>
```



#####iframe

`iframe` 嵌入其他网页

​	src：需要嵌入的 url 路径

​	widht、height：设置宽高

​	frameborder：边框，1 的时候有边框， 0 的时候没有边框

​	allowfullscreen：如果设置，可以通过全屏 API 设置为全屏模式

​	支持 后备内容

​	sandbox：提高安全性设置

```html
<iframe src="嵌入的 url" width="100%" height="500" frameborder="0" allowfullscreen sandbox>
  <p>不支持 iframe 标签</p>
</iframe>
```

`embed` 、`object` 嵌入pdf、svg  淘汰中，不常用



#####矢量图形

图片类型：

* 位图：使用像素网格定义，精确包含了每个像素的位置和它的色彩信息，常见的位图格式：bitmap（.bmp）、png，jpeg，gif
* 矢量图：使用算法来定义，包含了图形和路径的定义，svg 用来描述矢量图像的 XML 语言

```html
<!-- 显示 svg  -->
<!-- 使用 img 标签  
优点：同图片语法相同；a 标签嵌套变为超链接图片；
缺点：无法使用 js 操作图像；无法使用 css 控制 svg 内容；不能用 css 伪类重设图像样式；
-->
<img src="./circle.svg" alt="circle" />

<!-- 直接在 html 代码中使用 svg 代码 
优点：减少http请求，减少加载时间；
		 分配 id，可以css修改样式； 
		 使用 css 交互和 css 动画；

缺点：多处使用资源不好维护；
		 增加 html 文件大小；
		 浏览器不能缓存；
		 
-->
<body>
	<svg width="300" height="200">
		<rect width="100%" height="100%" fill="green" />
	</svg>
</body>

<!-- 使用 iframe 标签 
缺点：浏览器可能不支持 iframe；svg 和当前网页需要同源，否则不能使用 js 操作svg；
-->
<iframe src="./circle.svg" width="500"
height="500" frameborder="0" sandbox>
	<img src="./circle.png">
</iframe>
```



#####响应式图片

响应式图片：在不同的屏幕尺寸和分辨率的设备上都能良好工作

* 分辨率切换：不同的尺寸

  ```html
  <img srcset="elva-fairy-320w.jpg 320w,
               elva-fairy-480w.jpg 480w,
               elva-fairy-800w.jpg 800w"
       sizes="(max-width: 320px) 280px, // 宽度小于等于320设置值为 280px
              (max-width: 480px) 440px,
              800px"
       src="elva-fairy-800w.jpg" alt="Elva dressed as a fairy">
  ```

浏览器执行过程：

1. 查看设备宽度
2. 检测 sizes 列表中哪儿个条件为真
3. 查看设置的大小
4. 加载 srcset 列表中引用的最接近所选的大小的图像



* 分辨率切换：相同的尺寸，不同的分辨率

  ```html
  <img srcset="elva-fairy-320w.jpg,
               elva-fairy-480w.jpg 1.5x,
               elva-fairy-640w.jpg 2x"
       src="elva-fairy-640w.jpg" alt="Elva dressed as a fairy">
  
  ```

  浏览器计算当前显示器的分辨率，然后显示最合适的图像。



* 图片切换：根据浏览器的大小显示不同的图片

  ```html
  <picture>
    <source media="(max-width: 799px)" srcset="elva-480w-close-portrait.jpg">
    <source media="(min-width: 800px)" srcset="elva-800w.jpg">
    <img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva">
  </picture>
  
  ```

  当 media 的属性值为真时，显示对应 srcset 的值；按顺序执行找最符合的。

  

  设置 type，浏览器对不支持的类型会直接跳过

  ```html
  <picture>
    <source type="image/svg+xml" srcset="pyramid.svg">
    <source type="image/webp" srcset="pyramid.webp">
    <img src="pyramid.png" alt="regular pyramid built from four equilateral triangles">
  </picture>
  
  ```

  

####表格

table：表格

tr：表格中的行

thead：标题行 -- 用来嵌套 tr

tbody：单元格的行 -- 用来嵌套 tr

tfoot：表格底部行 -- 用来嵌套 tr

td：单元格

th：表格中的标题（单元格）

​		scpoe 属性：表示是行标题还是列标题，可选值：col、row、colgroup、rowgroup（多列、多行）

colspan：宽度是几个单元格

rowspan：高度是几个单元格

col：给列设置统一样式

colgroup：包含 col

caption：表格标题



```html
<table>
  <caption>表格标题</caption>
  <colgroup>
    <col >
    <col style="backgroud-color:red">
    <col span="2">
  </colgroup>
  <thead>
    <tr>
      <th>name</th>
    	<th>age</th>
    	<th>address</th>
    	<th>tel</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>A</td>
    	<td>5</td>
    	<td>---</td>
    	<td>001</td>
    </tr>
    <tr>
      <td>B</td>
    	<td>5</td>
    	<td colspan="2">---</td>
    </tr>
    <tr>
      <td>D</td>
    	<td>5</td>
    	<td>---</td>
    	<td rowspan="2">001</td>
    </tr>
    <tr>
      <td>C</td>
    	<td>5</td>
    	<td>---</td>
    </tr>
  </tbody>
</table>
```







### CSS

层叠样式表，用于设置和布置网页。

####如何使用

##### 外部样式表

最常用的方式；

定义 .CSS 文件，在改文件中定义样式；

在 html 文件 `head` 标签中引用：

`<link rel="stylesheet" href="styles/style.css">`



#####内部样式表

后期维护成本高；

将 CSS 放在 HTML 文件 head 标签里的 style 中

```html
<head>
  ...
	<style>
    h1 {
      color:blud;
    }
  </style>
  ...
</head>
```



##### 内联样式

位于 HTML 元素的 style 属性中，优点：只影响一个元素；缺点：难维护；代码可读性低；

```html
<body>
  <h1 style="color: red;">hello!</h1>
</body>
```



####选择器的结构

![图解CSS声明](https://tva1.sinaimg.cn/large/e6c9d24ely1h2zv19z7lzj20nm0dc74r.jpg)



####属性

#####属性的值可以是函数：

格式：函数名()

* cale()：计算
* rotate()：旋转



##### @ rules

导入 CSS 样式表： @import 'style2.css';

@media：使用媒体查询，当满足某些条件成立时。

```css
@import 'styles-2.css';

/* body 背景为 pink，当宽度大于等于 30em 时，背景为 blue*/
body {
  background-color: pink;
}

@media(min-width: 30em) {
  body {
    background-color: blue;
  }
}
```



##### 速记属性

允许在一行中设置多个属性值的属性为速记属性。

* font
* background
* padding 
  * 值为四个值代表：上右下左
* border
* margin
  * 值为四个值代表：上右下左



#### CSS 加载流程

![img](https://tva1.sinaimg.cn/large/e6c9d24ely1h3a78xydjij208c038a9z.jpg)

* 加载 HTML 文件
* HTML 转为 DOM
* 加载 HTML 中的资源：图片、视频、CSS
* 解析 CSS，添加样式到对应的元素中
* 显示最终的页面



#### 层叠

顺序规则：

* 当应用两条同级别的规则到一个元素的时候，写在后面的就是实际使用的规则
* 类选择器的优先级高于元素选择器

**只会覆盖相同属性的值**



#### 继承

一些设置在父元素上的 CSS 属性可以被子元素继承，有些则不能。

常见可继承属性：color

不可继承属性：padding、margin、border

##### 控制基础

* inherit

  设置该属性使子元素和父元素相同，也就是开启基础

* initial

  设置属性值和浏览器默认样式相同。如果浏览器默认样式未设置且该属性是自然基础的，那会等同于 inherit

* unset

  属性重置为自然值，也就是如果属性是自然继承那么就是 inherit，否则和 initial 一样

```css
body {
	color: red;
}

h1 {
  color: initial;
}
```

##### 重设属性值

使用 all 属性。

```css
body {
	color: red;
}

h1 {
  all: unset;
}
```



#### 选择器的优先级

优先级由四个部分（4位数）的分数相加；

* 千位：声明在 style 属性（内联样式）则该位得一分。这样的声明没有选择器，所以总是 1000 分；
* 百位：选择器中包含 ID 选择器则该位得一分；
* 十位：选择器中包含类选择器、属性选择器或者伪类选择器；
* 个位：选择器中包含元素、伪元素选择器则该位得一分；

**通用选择器（*），组合符（+、>、～、''），和否定伪类（:not） 不会影响优先级**

**计算时不允许进位，也就是无论多少个类选择器的权重叠加都不会超过一个 ID 选择器**



`!important` ：可以覆盖上面所有的优先级计算。**非必要不使用**，使用情况：不能修改核心的 CSS 模块，又想覆盖样式时。

```css
#winning {
    background-color: red;
    border: 1px solid black;
}
    
.better {
    background-color: gray;
		/* border 属性最终会使用这里的属性值 */  
    border: none !important;
}
```



#### 样式覆盖顺序

优先级从小到大的顺序

1. 浏览器默认样式
2. 用户样式表（用户设置的自定义样式）
3. 开发人员设置的样式
4. 开发人员设置的样式表中的 !improtant 声明
5. 用户样式表中的 !important 声明



#### 选择器列表

多个相同样式的 css 选择器可以混编为一个选择器列表。使用逗号分隔选择器。

**注意：使用选择器列表时，当任一选择器无效（存在语法错误），整条规则都会被忽略。**

```css
p, li, h1, .name {
	color: red;
}
```



#### 选择器类型

| 选择器名称                           | 选择的内容                                          | 示例                                     |
| ------------------------------------ | --------------------------------------------------- | ---------------------------------------- |
| 元素选择器（也称：标签或类型选择器） | 所有指定类型的 HTML 标签                            | p 选择 `<p>`                             |
| ID 选择器                            | 具有指定 ID 的元素（单一页面中，id 和元素一一对应） | #my-id 选择 `<p id="my-id"> `            |
| 类选择器                             | 具有特定类的元素（一个类可以有多个实现）            | .my-class 选择 `<p class="my-class">`    |
| 属性选择器                           | 拥有特定属性的元素                                  | img[src] 选择 `<img src="my.img">`       |
| 伪类选择器                           | 特定状态下的特定元素（比如鼠标悬停）                | a:hover 仅在鼠标悬停在链接上时选择 `<a>` |
| 全局选择器                           | 选中了文档中的所有内容                              | 使用 * 符号                              |



```css
/* 元素选择器 */
p {
  ...
}

/* 类选择器 */
.name {
  ...
}

/* id 选择器 */
#id {
  ...
}

/* 标签属性选择器 */
/* 属性存在时选择该元素 */
a[title] {
  ...
}
/* 有特定值的标签属性存在时选择该元素 */
a[href="https://xx.xx.xx"] {
  ...
}

/* 伪类选择器 */
a:hover {
  ...
}

/* 伪元素选择器 */
p::first-line {
  ...
}

/* 运算符 */

/* 后代选择器 */
/* 所有后代 */
article p {
  ...
}

/* 子代选择器 */
/* 直接后代 */
article > p {
  ...
}

/* 相邻兄弟选择器 */
/* 第二个元素紧跟在第一个元素之后，并且两个元素属于同一个父元素的子元素。 */
h1 + p {
  ...
}

/* 通用兄弟选择器 */
/* 选择 h1 元素之后所有同级 p 元素 */
h1 ～ p {
  ...
}


```



##### 属性选择器

######存否和值选择器

基于一个元素自身是否存在或基于不同的按属性值的匹配，来选取元素。

* [attr] ：匹配带有一个属性名为 attr 的元素
* [attr="xx"] ： 匹配带有一个属性名为 attr，值为 xx 的元素
* [attr~="a b c"] ：匹配带有一个属性名为 attr，其值为 “a b c” 或其值至少有一个和 "a b c" 中的一个匹配
* [attr|="ac"]：匹配带有一个属性名为 attr，其值为 "ac" 或者值以 "ac" 为开始字符后面紧跟连字符 "-"



###### 子字符串匹配选择器

* [attr^= value] ：匹配带有一个名为 attr 的属性的元素，其值开头为 value 
* [attr$=value] ：匹配带有一个名为 attr 的属性的元素，其值结尾为 value 
* [attr*=value] ：匹配带有一个名为 attr 的属性的元素，其值的字符串中的任何地方，至少出现了一次 value 



###### 大小写敏感

属性值是大小写敏感的，如果想不区分大小写在闭合括号前使用 `i`

```css
/* 匹配含有 class 属性并且属性值以 a 或 A 开始的 li 元素*/
li[class^=a i] {
	...
}
```



#####伪类选择器

用于选择处于特定状态的元素，如是第一个元素时，或者当鼠标指针悬浮在元素上时。

格式：`:伪类名`

* :first-child  匹配一组兄弟元素中的第一个子元素
* :last-child  匹配父元素的最后一个子元素
* :only-chid  匹配没有任何兄弟元素的元素
* :nth-child(x)   首先找到当前元素的所有兄弟元素，安装位置从 1 开始排序，选择的结果由括号中 x 决定，举例：
  * x 为 0n + 3  匹配第三个元素
  * x 为 1n+ 0 匹配所有元素
  * 2n + 0 匹配位置为偶数的元素
  * 2n + 1 匹配位置为奇数的元素
  * 3n+4 位置为：4、7、10... 的元素
* :invalid  匹配任意内容未通过验证的 `<input>` 或其他 `<form>` 元素

```css
/* 选中 article 中第一个 p 元素 */
article p:first-child {
	...
}
```

用户行为伪类也叫动态伪类

* :hover  鼠标悬浮在元素上时
* :focus  选定获取到焦点的元素



#####伪元素选择器

格式：`::伪元素名`

* ::first-line  元素中的第一行
* ::before  同 content 属性一同使用，在元素开头添加内容，来添加图标、空字符串
* ::after  同 content 属性一同使用，在元素结尾添加内容，来添加图标、空字符串



```css
/* 在类为 box 的元素开头添加内容  */
.box::before {
	content: "在开头添加内容"
}

/* 在文本前添加一个大小为：100*100 背景为红色 宽度为1颜色为黑色实线描边 的方块 */
.box::before {
  content: '';
  display: block;
  widht: 100px;
  height: 100px;
  background-color: red;
  border: 1px solid black;
}
```



伪类和伪元素结合

```css
/* 匹配第一段中的第一行 */
article p:first-child::first-line {
  ...
}
```



##### 关系选择器

* 后代选择器  

   空格 ` `  组合两个选择器，匹配所有后代元素

* 子代选择器 

  大于号 `>` ，只会匹配直接子元素

* 邻接兄弟选择器

  加号 `+` ，选中恰好处于另一个处于同级的元素紧挨的元素

* 通用兄弟选择器

  `~` ，选中指定元素的兄弟元素

  



####盒模型

所有元素都被一个个的盒子（box）包围着。



#####块级盒子（Block box）

表现行为：

* 盒子会在内联的方向上扩展并占据父容器在该方向上的所有空间，在绝大数情况下意味着盒子会和父容器一样宽
* 每个盒子都会换行
* width 和 height 属性可以发挥作用
* 内边距、外边距和边框会将其他元素从当前盒子周围推开

例如：`h1` 、`p`



#####内联盒子（Inline box）

表现行为：

* 盒子不会换行
* widht 和 height 属性不起作用
* 垂直方向的内边距、外边距以及边框会被应用但是不会把其他处于 inline 状态的盒子推开
* 水平方向的内边距、外边距以及边框会被应用且会把其他处于 inline 状态的盒子推开
* 使用 `display:inline-block` 可以使内联盒子的 widht 和 height 属性起作用，不会跳转到新行，在内联和块之间提供了一个中间状态

例如：`a ` 、` span` 、`em` 、 `strong`



通过 `display` 属性的设置，控制盒子的外部显示状态。



#####内部和外部显示状态

外部显示状态决定盒子是块级还是内联；

内部显示状态决定盒子内部元素是如何布局的，默认是安装正常文档流布局（块级和内联布局）。可以通过类似使用 flex 的 display 值来更改内部显示状态。一个元素设置 `display: flex` ，外部显示状态为 block，内部显示状态修改为 flex，会根据弹性盒子（Flexbox）规则进行布局。



##### 盒模型结构

结构图：

![Diagram of the box model](https://tva1.sinaimg.cn/large/e6c9d24ely1h3ekuhcxbzj20f408caa5.jpg)

* Content box：显示内容，大小通过 widht 和 height 设置
* Padding box：包围在内容区域外部的空白区域，大小通过 padding 相关属性设置
* Border box：边框盒包裹内容和内边距，大小通过 border 相关属性设置
* Margin box：最外面的区域，是盒子和其他元素之间的空白区域，不计入实际大小，大小通过 margin 相关属性设置



**实际大小**

* 标准盒模型（默认情况） 

  盒子实际大小 = content + padding + border

* 替代盒模型

  通过设置： box-sizing: border-box;

  盒子实际大小 = content 大小（也就是 widht 、height）

  

##### 外边距

* 四个值可以单独设置也可以同时设置
* 值为正时推开周边元素，值为负时，收缩空间
* 外边距折叠，如果有两个外边距相接的元素，这些外边距将合并为一个外边距，即最大的单个外边距的大小



##### 内边距

* 内边距的值大于等于 0 
* 四个值可以单独设置也可以同时设置



##### 边框

* 四个边框均包含：样式、宽度和颜色，可以单独设置也可以同时设置
* 圆角 border-radius ：两个值 第一个为水平半径，第二个为垂直半径，相同时只需写一个值



##### 背景

* background-color 背景颜色，值为任何有效的 color 值，背景颜色扩展到元素的内容和内边距下面

* background-image 背景图片，渐变背景（制作：https://cssgradient.io/），大图不会缩小所以只能看到图片的一部分，小图平铺填充元素。图片背景显示在颜色背景之上

  * 可以设置多个图片（使用逗号隔开），先设置的在顶部，对应图片的数量：以下属性值也可以设置多个值，控制对应位置的图片，属性值个数小于图片个数时进行较小数量的值会循环

  * 控制背景平铺的属性 background-repeat 

    * no-repeat  不重复
    * repeat-x  水平重复
    * repeat-y  垂直重复
    * repeat 两个方向重复

  * 调整背景图像大小的属性 background-size 

    * cover  放大图片以完全覆盖元素，会保持图片的宽高比，图片会超出元素之外
    * contain  将图像的大小适合元素（图片在元素内），图像和元素宽高比不同时，会出现间隙
    * 数值  指定确切大小

  * 背景图像定位属性 background-position

    设置图片在元素中显示的位置，使用的坐标系中框的左上角是  (0, 0)，框沿着水平 (x) 和垂直 (y) 轴定位

    * 使用关键字 top、center
    * 使用数值：长度值或百分比 ：10px 20%
    * 混合使用关键字和数值: top 20px
    * 设置 4 个值来指到盒子的某些边的距离    `background-position: top 20px right 10px; `从顶部调整 20px，从右侧调整 10px

  * 背景如何滚动 background-attachment 

    * scroll：元素的背景在页面滚动时滚动，元素内容滚动，背景不会移动。被固定在页面的相同位置，所以会随页面进行滚动
    * fixed：元素的背景固定在视图端口上，页面或内容滚动时，均不滚动。始终在屏幕上的相同位置
    * local：滚动元素时背景跟着滚动，固定在设置的元素上，所以滚动元素时背景也随之滚动

* 使用简写

  * 背景之间使用逗号隔开
  * 第一个背景指定所有普遍属性
  * background-color 只能在逗号之后指定
  * background-size 只能包含在背景位置之后，用 "/" 分隔，例如：center/80%



##### 书写模式

CSS 中的书写模式是指文本的排列方向是横行还是纵向的。

属性  writing-mode 用来改变书写模式，包含值：

* horizontal-tb 块流向从上至下，对应文本方向是横向
* verticla-rl 块流向从右向左，对应的文本方向是纵向
* vertical-lr 块流向从左向右，对应的文本方向是纵向



横向书写模式下，影射到 width 的属性被称作内联尺寸（inline-size）--- 内联纬度的尺寸；影射 height 的属性被称为块级尺寸（block-size），这是块级维度的尺寸。

| 物理属性      | 对应逻辑属性         |
| ------------- | -------------------- |
| widht         | inline-size          |
| height        | block-size           |
| margin-top    | margin-block-start   |
| padding-left  | padding-inline-start |
| border-bottom | border-block-end     |

*对应属性：上下（top、bottom） 是 block-start/end , 左右（left、right）是 inline-start/end*

​	

##### 溢出

溢出是在盒子无法容纳下太多的内容的时候发生的。

使用  overflow 属性控制溢出时候的处理

* visiable  显示溢出的内容，默认值
* hidden 隐藏溢出的内容
* scroll  显示滚动条，同时设置了水平、垂直方向，设置单一方向的滚动：`overflow-y: scroll`
* auto 当内容溢出的时候显示滚动条



*块级排版上下文（Block Formatting Context, BFC）*，当设置为 auto 或 scroll 时就建立了一个块级排版上下文。



##### CSS 的值与单位

数值类型：

* integer ：整数
* number ：小数，可能有小数部分也可能没有
  * 无须单位的数值属性：透明度 `opacity: 0`  0 完全透明 1 完全不透明
* dimension ：带有附加单位的 number，包含：length、angle、time、resolution 类型
  * length 长度
    * 相对长度，包含单位
      * cm 厘米  等价值  1cm = 96px/2.54
      * mm 毫米 等价值  1mm = 1/10th of 1cm
      * Q 四分之一毫米  等价值  1Q = 1/40th of 1cm
      * in 英寸  等价值  1in = 2.54cm = 96px
      * pc 十二点活字  等价值  1pc = 1/6th of 1in
      * pt 点  等价值  1pt = 1/72th of 1in
      * px 像素  等价值  1px = 1/96th of 1in
    * 绝对长度，包含单位
      * em  在 font-size 中使用时是相对于父元素的字体大小的倍数，在其他属性使用时是相对于自身的字体大小
      * ex 字符 “x”  的高度
      * ch  数字 "0" 的宽度
      * rem 根元素的字体大小的倍数
      * lh  元素的 line-height
      * vw 视窗宽度的百分比
      * vh 视窗高度的百分比
      * vmin 视窗较小尺寸的百分比
      * vmax  视窗大尺寸的百分比
* percentage ：百分比的值，百分比的值总是相对于另一个量
  * 元素字体设置为百分比，那么它将是元素父元素字体大小的百分比
  * 元素宽度设置为百分比，那么它将是父元素宽度的百分比
  * margin、padding 设置为百分比，均是对应元素的**宽**进行计算（也就是块的内联尺寸）



######颜色

颜色属性的值有以下表示方式

* 颜色关键字
* 十六进制颜色值  例如 `#ff00ff`
* RGB 的值 `rgb(2, 121, 139)`   3 个 0～255 的数表示
* RGBA 的值  `rgba(2, 121, 139, 0.5)`   前  3 位是 0～255 的数， 最后一位是 0～ 1 代表颜色的透明度，1 表示完全不透明
* HSL 的值  接受色调、饱和度和亮度的值为参数，格式 `hsl(188, 97%, 28%)`
  * 色调： 颜色的底色，这个值在 0 和 360 之间，表示色轮周围的角度
  * 饱和度：它的值在 0～100%，其中 0 为无颜色，100% 为全色饱和度
  * 亮度：它的值在 0～100%，其中 0 为没有光（显示为黑色），100% 表示完全亮（显示为白色）
* HSLA 的值，对比 HSL 多了一位（范围：0～1），指定透明度 `hsla(188, 97%, 28%, .3)`



##### 图像、视频、音频

图像和视频被描述为**替换元素**，意味着 CSS 不能影响这些元素的内部布局仅影响它们在页面上与其他元素中的位置。

######调整大小

* 给元素设置 ` max-width: 100%;`  将允许图片（视频、音频）尺寸上小于但不大于盒子

* 属性 object-fit 设置
  * cover 缩小/放大图像，维持图像的比例，充满整个盒子
  * contain 图像将会缩放到足以放到盒子里面的大小，如果图像和盒子比例不一致则会导致“开天窗”的结果
  * fill  图像充满整个盒子，不维持比例

**当替换元素在成为网格或者弹性布局的一部分时，有不同的默认行为（显示在容器的起始处），这避免它们被布局奇怪拉伸。**



##### 表单

样式统一代码

```css
button,
input,
slect,
textarea {
  font-family: inherit;
  font-size: 100%;
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

textarea {
  overflow: auto;
}
```



##### 样式化表格

* 使用 ` table-layout: fixed` 创建可控的表布局，通过设置标题的宽设置列的宽度
* 使用 `border-collapse: collapse` 使表元素边框合并



CSS 布局主要就是基于盒模型，常用属性：

* padding：内边距，围绕着内容的空间
* border：边距，紧接着内边距的线
* margin：外边距，围绕着元素外部的空间
* width：元素的宽度
* background-color：元素内容和内边距底下的颜色
* color：元素内容（通常是文本）的颜色
* text-shadow：为元素内的文本设置阴影
* display：设置元素的显示模式

![From outside to in they are labelled margin, border and padding](https://tva1.sinaimg.cn/large/e6c9d24ely1h30n02lma9j20fy0ci753.jpg)

#####属性及属性值

* `margin:  0 auto; ` 为 margin 或 padding 等属性设置两个值时，第一个值代表元素的上方和下方，第二个值代表左边和右边，auto 是特殊值，意思是水平方向上左右对称。

* `padding: 0 10px 10px 10px;` 四个值的顺序：上、右、下、左。
* `border: 5px solid black;` 5 像素的黑色实线边框。
* `text-shadow: 3px 3px 1px black;` 
  * 第一个值设置水平偏移量 -- 阴影右移的像素数（负值左移）
  * 第二个值设置垂直偏移量 -- 阴影下移的像素数（负值上移）
  * 第三个值设置阴影的模糊半径 -- 值越大产生的阴影越模糊
  * 第四个值设置阴影的基色
* `display: block;`  给予内联元素块级行为（占据页面的空间并且能够赋予外边距和其他改变间距的值）



##### 文本样式

* 字体样式：作用于字体的属性，会直接应用到文本中，比如使用哪儿种字体，字体的大小是怎样的，字体是粗体、斜体等

  * **文档根元素 html 中的文本字体大小为：16px，浏览器 font-size 标准设置的值为： 16 px**

  * font-family 字体

    ```css
    p {
      font-family:"Trebuchet MS", Verdana, sans-serif; /*设置字体栈，从第一个开始查看当前机器中，该字体是否可用，可用就应用到元素中，不可用就移动列表的下一个，名字为多个单词的字体使用引号包裹 */
    }
    ```

    

  * font-style 打开和关闭文本斜体

    * normal 普通字体
    * italic 斜体
    * oblique 斜体的模拟版本

  * font-weight 设置文字的粗体大小

    * normal 普通字体
    * bold 加粗字体
    * lighter 粗体设置为比其父元素粗体更细
    * bolder 粗体设置为比其父元素粗体更粗
    * 100 - 900 数值粗体值

  * text-transform   设置要转换的字体

    * none 防止任何转型
    * uppercase 转为大写
    * lowercase 转为小写
    * capitalize  所有单词的首字母为大写
    * full-width  转为全角

  * text-decoration  文本的装饰（链接 a 元素取消设置默认下划线），值可以为多个装饰；可设置颜色和样式

    * none 取消任何装饰

    * underline 文本下划线

    * overline 文本上划线

    * line-through 穿过文本的线

      ```css
      p {
        /* 设置了两种线 */
        text-decoration: underline overline;
        /* 设置了线、线颜色、线的粗细、线样式 */
        text-decoration: line-through red 2px wavy;
      }
      ```

      

  * text-shadow 文本阴影 可以同时设置多种阴影，用逗号分隔

    ```css
    p {
      text-shadow: 4px 4px 5px red; /* 1: 阴影和原始文本的水平偏移；2:阴影和原始文本的垂直便宜；第三个值模糊半径，默认为0；4：阴影的基础颜色，默认 black */
    }
    ```

    

* 文本布局风格：作用于文本的间距以及其他布局功能的属性，比如，允许操作行与字之间的空间，以及内容框中，文本如何对齐

  * text-align 文本对齐方式
    * left 左对齐
    * right 右对齐
    * center 居中
    * justify 展开，改变单词间的差距，使所有文本行的宽度相同
  * line-height  行高，文本每行之间的高
    * 值为无单位的数值 （推荐值 1.5-2）   实际结果为：字号乘以 font-size
    * 带单位的数值  
  * word-spacing 单词间距  
    * 带单位的数值
  * letter-spacing 字母间距
    * 带单位的数值
  * text-indent  文本的第一行预留水平空间
  * text-overflow 文本溢出的处理

**Font 简写**

顺序：font-style, font-variant, font-weight, font-stretch, font-size, line-height, font-family

必须指定的属性：font-size, font-family 

font-size 和 line-height 中间必须放一个斜杠 `/`



##### 列表特定样式

* list-style-type 设置项目符号点的类型 none
* list-style-position  项目符号点的位置，inside  outside（默认值）
* list-style-image 项目符号图片

以上属性简写，属性可以任意排列，可以设置任意个数，默认值：disc、none、outside

```css
ul {
  list-style: square url(example.png) inside;
}
```

* start 列表计数起始值
* reversed 列表倒计数
* value （li） 指定数值

```html
<ol start="5" reversed>
   <li> 1-AAA</li>
   <li> 2-AAA</li>
   <li> 3-AAA</li>
   <li> 4-AAA</li>
   <li> 5-AAA</li>
</ol>

<ol>
  <li value="3">c</li>
  <li value="1">a</li>
  <li value="2">b</li>
</ol>
```



##### 链接样式

* outline 边框，不占用盒子的空间

链接状态对应的伪类

* :link 默认状态
* :visited 已经访问过的
* :hover 鼠标光标悬浮在链接时
* :focus  被选中时，键盘 tab 键
* :active 被激活时（被点击时）



#### CSS 布局

#####正常流布局（normal flow）

指不对页面进行任何布局控制，浏览器默认的 HTML 布局方式

默认的，块级元素的内容宽度是其父元素的 100%，其高度与其内容高度一致；内联元素的宽、高同内容一致。如果想控制内联元素的宽和高，需要为元素设置 display:  block 或 display: inline-block



两个相邻的元素都设置了 margin 并且两个 margin 有重叠，那么更大的值会被保留，这杯成为**外边距叠加**



##### display 属性

正常流中的所有内容都有 display 属性值，块元素的值为 display:block，内联元素的值为 display:inline。

通过更改元素的 display 值，改变元素的默认表现形式。



##### 弹性盒子（Flexbox）

专门设计出来用于创建横向或是纵向的一维页面布局，元素可以膨胀以填充额外的空间，收缩以适应更小的空间

**通过设置 display: flex 是其按弹性盒子进行布局**

flex 盒子模型

![flex_terms.png](https://tva1.sinaimg.cn/large/e6c9d24ely1h3jhijug7wj20fn099wey.jpg)

* 主轴（main axis） 沿着 flex 元素放置的方向延伸的轴，轴的开始和结束被称为 main start 和 main end
* 交叉轴 （cross axis）垂直于 flex 元素放置方向的轴，轴的开始和借宿被称为 cross start 和 cross end
* 设置了 display: flex 的元素被称为 flex 容器
* 在 flex 容器中的盒子被称为 flex 项（flex item）



flex 容器 属性及值：

* flex-direction 排列方向

  * row   水平排列（默认值）
  * row-reverse  反向水平排列
  * column 垂直排列
  * column-reverse 反向垂直排列

* flwx-wrap

  * wrap 将溢出的内容移到下一行

* align-items 控制在交叉轴上的位置

  * stretch   拉伸 item 的高度（交叉轴方向拉伸）同父元素一样（默认值）

  * center  保持元素原有高度，在交叉轴居中
  * flex-start 在交叉轴开始处对齐
  * flex-end 在交叉轴结束处对齐

* justify-content 控制元素在主轴上的位置

  * flex-start  位于主轴的开始处，默认值
  * flex-end 在结尾处
  * center 主轴居中
  * space-around  沿着主轴均匀分布，在任意一端都会留有空间
  * space-between 同 space-around 相似，只是不会在两端留下任何空间

flex item 属性及值：

* flex

  * flex: 100px; 设置 元素的最小宽至少为 100px

  * flex: 1; 设置元素在主轴方向上的占比，占用的空间是在设置 padding 和 margin 之后剩余的空间

  * flex: 1 200px;  元素先获得 200px 的可用空间，剩余空间根据比例分配

* align-self  覆盖  align-items 的行为，值同  align-items

* order 改变位置，不影响在源顺序（dom 树里元素的顺序）

  * 数值  默认值为 0；orfer 值大的元素排在值小的元素后面；相同 order 的元素按源顺序显示；可以设置 - 1 会排在 0 前面；



简写方式

```css
flex-direction: row;
flex-wrap: wrap;

/* 上面两句可缩写为 */
flex-flow: row warp;

```





##### 网格（Grid） 布局

用于同时在两个维度上把元素按行和列排列

设置 display: grid，同时需要设置行、列的属性

* grid-template-columns:

  	* 1fr 2fr 1fr 2fr; 设置等宽的 4 列，fr 将可用空间按比例分配

  	* repeat(2, 1fr 2fr); 重复构建列/行，第一个参数是重复次数，第二个参数是重复构建的配置，此处配置等同于上面的写法

* grid-template-rows: 100px 100px; 设置每行的行高

* row-gap: 5px;  设置行间距

* column-gap: 10px; 设置列间距

* gap: 10px; 设置行、列间距
* grid-auto-rows  隐式网格（当内容放到网格外时生成的网格）的行高，只设置一个值
  * 100px  数值 具体值
  * minmax(100px, auto)   尺寸最小为 100px，当内容尺寸大于 100 像素时会根据内容自动调整
* grid-auto-columns 隐式网格的列宽

######放置元素

* 基于线的元素放置（指定行列分割线）
  * grid-column、grid-row
    * 1   占第1个格
    * 1/3  占第一条分割线到第三条分割线中间（第一、第二个格 ）
* 使用 grid-template-areas 属性放置元素
  * 在父元素中定义属性   grid-template-areas ，按表格每个格子进行命名
  * 在子元素中定义属性 grid-area: xx 值为定义的格子的名称





##### 浮动（float）

把一个元素 浮动起来，会改变元素本身和在正常布局流中跟随它的其他元素的行为。元素会浮动在左侧或右侧，并且从**正常布局流中移除**，周围内容会在这个被设置浮动的元素周围环绕。

属性 float 可能的值：

* left  浮动到左侧
* right  浮动到右侧
* none  默认值，不浮动
* inherit  继承父元素的浮动属性



所有在浮动下面的自身不浮动的内容都将围绕浮动元素进行包装，此时需要给这些不浮动的元素设置 `clear: both` 用来告知浏览器这个元素和源码后面的元素将不浮动。

* clear
  * left 停止任何活动的左浮动
  * right 停止任何活动的右浮动
  * both 停止任何活动的左右浮动



*同层级元素同时设置了 float:right ，那么**先声明**的会再最右侧，因为先声明的元素在源代码顺序上比后声明的元素等级要高，所以在浮动顺序上也会比后声明的元素等级要高，又同时向右浮动，所以先声明的更靠右。*



非浮动元素的外边距不能用于它们和浮动元素之间来创建空间，所有需要添加一个额外的 div 进行，此 div 不需设置高度，设置属性 `clear: both`



设置 浮动 最好设置 样式`box-sizing: border-box;`，避免增加内边距或边界的宽度时，超出父布局的大小而导致页面布局显示异常。





##### 定位（positioning）

属性：positon

能够让一个元素从它原本在正常布局流中应该在的位置移动到另一个位置。用来管理和微调页面中的一个特色项的位置。

定位类型：

* static  静态定位 （Static positioning） 元素默认的属性，表示放在文档布局流的默认位置
* relative  相对定位 （Relative positioning）相对于元素在正常的文档流中的位置移动它，可以将两个元素叠放在页面上
  * 需要设置 top、bottom、left、right 后位置才会发生改变  在源位置上偏移
* absolute   绝对定位 （Absolute positioning）将元素完全**从页面的正常布局流中移除**，类似将它单独放在一个图层中。可以设置相对于指定元素进行定位
  * 设置 top、bottom、left、right 指定元素应距离包含元素的每个边的距离
  * 绝对定位元素的包含元素：取决于绝对定位元素父元素的 position 属性，如果所有的父元素都没有显式地定义 position 属性，那么绝对定位元素会被包含在**初始块容器**中，初始块容器同浏览器视口一样大，html 标签也位于这个容器中。**绝对定位元素会被放在 html 元素的外面，并且根据浏览器视口来定位。通过设置绝对定位元素其中一个父元素的定位属性来改变绝对定位元素的相对位置元素。** 
  * 同层级的两个元素同时设置了绝对定位，在源顺序中**后定位**的元素将覆盖在先定位的元素
  * 设置 z-index 属性来改变层叠，默认值为 auto 实际上为 0。值大的元素会移动到堆栈上方。
* fixed   固定定位 （Fixed positioning） 与绝对定位类似，但是是将一个元素**相对于浏览器视口固定**，创建类似在整个页面滚动过程中总是处于屏幕的某个位置的导航菜单非常有用
* sticky   粘性定位 （Sticky positioning）让元素先保持和 static 一样的定位，当它的相对视口位置达到某一个预设值时，就会想 fixed 一样定位





#####表格布局

display: table-row; 设置为表格行

display:table-cell; 设置为表格的最小单元

display: table-caption;  设置为表格标题





##### 多列布局

把内容按列排序的方式

设置多列布局

* 通过设置 column-width: 具体数值 

* column-count: 具体数值 将块转为多列容器， 浏览器根据指定的值去创建列，任何剩余的空间之后都会被现有的列平分，所以列元素实际宽度不一定就是设置的值

其他属性

* column-gap: 20px 设置列间隙的宽
* column-rule 设置间隔的样式，同 border 用法类似，放置于 column-gap 中，不占用宽度
* break-inside: avoid;  避免拆分列中的元素





#####其他属性

`cursor: pointer;`  设置鼠标悬浮在元素上时显示为小手图标

`transition: 0.6s all;` 状态改变时平滑的过度



#### 响应式设计（RWD）

响应式网页设计：RWD（responsive web design）

媒体查询以及样式改变时的点，被叫做**断点（breakpoints）**。

实现响应式设计，用到的 web 平台的功能

* 媒介查询   允许一系列测试，如屏幕是否大于某个宽度或者某个分辨率，并将 CSS 选择性地适应用户地适应用户的需要应用在样式化页面上

  * media-type （媒体类型）：all、print、screen、speech

  * media-feature-rule（媒体特征规则）

    * 宽、高  
      * width: 600px
      * max-width: 600px
      * min-width: 200px
    * 朝向
      * orientation: landscape 横放模式
      * orientation: portrait 竖放模式
    * 使用指点设备（触摸屏无法实现悬浮）
      * hover: hover

  * 媒体查询可以组合使用

    * 与逻辑  

      ```css
      @media screen and (min-width: 400px) and (orientation: landscape){ ... }
      ```

    * 或逻辑

      ```css
      @media screen and (min-width: 400px), screen and (orientation: landscape) {..}
      ```

    * 非逻辑

      ```css
      @media not all and (orientation: landscape) {...}
      ```

  

  

  

  ```css
  /* 格式 */
  @media media-type and (media-feature-rule) {
    /* CSS rules go here */
  }
  
  
  /* 查询测试，当前的 Web 页面是否为屏幕媒体并且宽度至少为 800px 时包含的样式才会被应用 */
  @media screen and (min-width: 800px) {
    .container {
      ...
    }
  }
  ```

  

* 使用 视口单位 vw 实现响应式排版：font-size: calc(1.5rem + 3vw)

* 视口元标签在 head 标签中 `<meat name="viewport" content="width=device-width,initial-scale=1">`    // 这个元标签告诉移动端浏览器，应该将视口宽度设定为设备的宽度。原因：手机浏览器会将宽度设为 960px，显示的是桌面布局的缩放版本。





### JavaScript

#### 如何使用

* 内部 JavaScript

  在 head 或 body 中添加 `<script> // js 代码  </script>`

* 外部 javaScript

  定义 scriptts/x.js 文件

​		然后在 html 文件 `head` 标签中添加引用：

​		`<script src="scriptts/x.js" defer></script>`



脚本阻塞问题的两种解决方案

* async  不会阻塞页面渲染，直接下载然后运行，无法控制运行次序，只是脚步不会阻止剩余页面的显示。适用于：页面的脚本之间彼此独立，且不依赖于本页面的其它任何脚本。
* defer  按照在页面中出现的顺序加载和运行



####同 HTML 交互

常用对象及代码

```javascript
// 带提示信息和输入框的弹窗，并将输入的内容赋值给 info
let info = prompt("input info"); 

// 查询元素 参数可以为：标签名、类名
let pInfo = document.querySelector('p');
// 查询所有元素
document.querySelectorAll('p');
// 修改元素文本
pInfo.textContent = "new content";
// 修改 input 内容
input.value = "new value";
// 修改元素样式 xx 为属性名
pInfo.style.xx = "";

// 添加节点
h1.appendChild(pInfo);
// 移除节点
h1.removeChild(pInfo);
// 移除节点 自己不能移除自己
pInfo.parentNode.removeChild(pInfo);

// 窗口大小改变监听事件
window.onresize = function() {
  ... 
  var w = window.innerWidth;
  var h = window.innerHeight;
}

// 给元素设置点击事件  clickM 为一个 function 
// 方式一 设置多个方法前面设置的会覆盖后面设置的
info.onclikc = clickM;
// 方式二 优点：可以移除事件; 可以设置多个点击时的方法
info.addEventListener('click', clickM);
// 移除事件
info.removeEventListener('click', clickM);

// 事件对象 event 被自动传递给处理方法 
info.onclick = function(event) {
  // event.target 为发送事件的对象本身（也就是被点击的元素）
  event.target.style.backgroundColor = "#ff0000";
}

// 阻止默认行为
// 表单输入检验-- 为空提示信息，不提交表单
form.addEventListener("submit", (e) => {
	if (fname.value === "" || lname.value === "") {
		e.preventDefault(); // 阻止默认行为
		para.textContent = "You need to fill in both names!";
	}
});

                           
// 随机数 
// 0 和 1 之间的随机数
Math.random();
// 随机数 1~100
Math.floor(Math.random() * 100) + 1;

// 截取字符串  [start， end) 含前不含后
"abcde".slice(0, 2); // 结果：ab
"abcde".slice(2); // 结果：cde

// 是否包含指点字符串
"abceEgG".indexOf("bdc"); // 返回所在位置，不存在返回 -1

// 转换大小写
"aBd".toLowerCase(); // 均转为小写
"aBd".toUpperCase(); // 均转为大写

// 字符串转为数组
"ab,123,cd,ef".split(",");
// 数组转为字符串
// 方式一 可以指定分隔符
["ab", "cd"].join(",");
// 方式二 分隔符为 逗号
["ab", "cd"].toString();


// 数组操作
// 在尾部添加一项，方法执行完返回新数组的长度
var length = array.push("xx"); 
// 在尾部添加多项
array.push("xx", "bb");
// 删除数组最后一个元素，返回被删除项的内容
var item = array.pop(); 
// 在数组起始位置添加一项
array.unshift("new");
// 删除数组中第一项
array.shift();





```



####事件冒泡和捕捉

当事件发生在具有父元素的元素上时，浏览器运行两个不同的阶段：捕获阶段和冒泡阶段。

捕获阶段

* 从 html 元素到点击的元素检测是否注册了 onclick 事件，如果有就执行

冒泡阶段（默认情况下，按此注册）

* 从点击元素到 html 标签元素检测是否注册了 onclick 事件，如果有就运行
* 只想执行点击元素的点击事件，在元素点击方法中添加代码：event.stopPropagation();，则不会执行父元素们的点击事件



#### 原型

JavaScript 是一种基于原型的语言（prototype-based language） --- 每个对象拥有一个原型对象，对象以其原型为模版、从原型继承方法和属性。原型对象也可能拥有原型，并从中继承方法和属性，一层一层，以此类推。这种关系常被称为**原型链（prototype chain）**。

**上游对象的方法不会复制到下游的对象实例中，下游对象本身虽然没有定义这些方法，但是浏览器会通过上溯原型链、从上游对象中找到它们。当上游对象发生变化（新增函数），下游对象会自动更新。**



```js
// 对象定义模式
function Test(a, b, c) {
  // 属性定义
}

// 定义方法 x
Test.prototype.x = function() {...}

// 定义方法 y
Test.prototype.y = function() {...}
```



####继承

JavaScript 继承的对象函数不是通过复制而来，而是通过原型链继承（通常被称为**原型链继承 -- prototype inheritance**）。

```js
// Person 对象
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// 定义 Person 对象的方法
Person.prototype.sayHello() {
  console.log("hello, this is Person, name = " + this.name);
}

// Teacher 对象，继承自 Person 对象
function Teacher(name, age, address） {
  Person.call(this, name, age); // 注意：调用 call 方法
	this.address = address;
}
// 设置 prototype
Teacher.prototype = Object.create(Person.prototype);
// 设置 构造方法
Object.defineProperty(Teacher.prototype, "constructor", {
	value: Teacher,
	enumerable: false,
	writable: true,
});

// Teacher 实现自己的 sayHello 方法
Teacher.prototype.sayHello = function() {
  console.log("hello, this is Teacher, name = " + this.name);
}


// ECMAScript 2015 (ES6) 实现上述代码
class Person() {
  constructor(name, age){
    this.name = name;
    this.age = age;
  }
  
  sayHellow() {
    console.log(`hello, this is Person, name = " + ${this.name}`);
  }
}

class Teacher extends Person {
  constructor(name, age, address) {
    super(name, age);
    this._address = address;
  }
  
  get address() {
    return this._address;
  }
  
  set address(newAddress) {
    this._address = newAddress;
  }
}


```





#### XMLHttpRequest

用来向服务器请求资源文件（图片、文本、json、html 代码等）

```js
// 请求链接
var requestUrl = "https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json"; 
var request = new XMLHttpRequest();
request.open("GET", requestUrl);
request.responseType = "json";
request.send();
request.onload = function() {
  const superheroes = request.response;
  // 解析拿到的 json 数据
  ...
}
```



#### Fetch

fetch 是 XMLHttpRequest 的一个现代替代品。使异步 HTTP 请求更容易实现

```js
fetch(url).then(function(response) {
	response.json()
}).then(json => {
  conslog.log("success");
  ...
}).catch(e => {
  console.log(e);
});
```





#### JSON 对象解析和转换

`JSON.parse("")`; // 字符串转为 JSON 对象

`JSON.stringify(jsonObj);`  // JSON 对象转为 JSON 字符串



#### 异步

##### Promise 

Promise 是 JavaScript 中异步编程的基础，是一个由异步函数返回的可以向我们指示当前操作所处的状态的对象。

Promise 的三种状态

* 待定（pending）： 初始状态，即没有被兑现也没有被拒绝。调用 fetch() 返回 Promise 的状态，此时请求还在进行中
* 已兑现（fulfilled）：意味着操作成功完成。当 Promise 完成时，它的 then() 函数被调用
* 已拒绝（rejected）：意味着操作失败，此时 catch() 函数被调用

*可以使用 已敲定（settled）同时表示已兑现和已拒绝。*



Promise.all([]) 合并执行多个互不依赖的 Promise，由 Promise.all 返回的 Promise：

* 当且仅当数组中所有的 Promise 都被兑现时，才会通知 then 函数并提供一个包含所有响应的数组，数组中响应的顺序与被传入 all 的 Promise 顺序相同
* 会被拒绝，如果数组中有任何一个 Promise 被拒绝，此时，catch 处理函数被调用，并提供被拒绝的 Promise 所抛出的错误



Promise.any([])  当数组中的任何一个被兑现时就会被兑现，如果所有的都被拒绝，会被拒绝。无法预测哪儿个请求会先被兑现。

 

```js
// promis 使用例子
const fetchPromise = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');

// 异步
fetchPromise
  .then( response => {
      if(!response.ok){
          throw new Errow(`HTTP error code: ${response.status}`);
      }
    return response.json();
  })
  .then( json => {
    console.log(json[0].name);
  }).catch(error => {
      console.log(`eror ${error}`);
  });


// 合并多个 Promise
const fetchPromise1 = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
const fetchPromise2 = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/not-found');
const fetchPromise3 = fetch('https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json');

// 将所有 Promise 传入，当都被兑现时通知 then() 函数处理，响应结果数组的顺序就是传入的顺序
Promise.all([fetchPromise1, fetchPromise2, fetchPromise3])
  .then(responses => {
  	for(const response of responses) {
      console.log(`${response.url}: ${response.status}`);
    }
  }).catch(error => {
	  console.log(`eror ${error}`);
  });


// Promise.any 
Promise.any([fetchPromise1, fetchPromise2, fetchPromise3])
  .then( response => {
    console.log(`${response.url}：${response.status}`);
  })
  .catch( error => {
    console.error(`获取失败：${error}`)
  });
```



##### async 和 await

async 关键字提供了一种更简单的方法来处理基于异步 Promise 的代码。

在函数开头添加 async ，使其成为一个异步函数

```js
// 定义异步函数
async function test() {
  ...
}


// async 结合 fetch 的使用例子
async function fetchProducts() {
  try {
    const response = await fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
    if (!response.ok) {
      throw new Error(`HTTP 请求错误：${response.status}`);
    }
    const json = await response.json();
    return json;
  }
  catch(error) {
    console.error(`无法获取产品列表：${error}`);
  }
}

const jsonPromise = fetchProducts();
jsonPromise.then((json) => console.log(json[0].name));
  

// 实现返回 Promise 的方法
function alarm(person, delay) {
  return new Promise((resolve, reject) => {
    if (delay < 0) {
      throw new Error('Alarm delay must not be negative');
    }
    window.setTimeout(() => {
      resolve(`Wake up, ${person}!`);
    }, delay);
  });
}

// 调用
alarm("name", 2000)
    .then(message => output.textContent = message)
    .catch(error => output.textContent = `Couldn't set alarm: ${error}`);

// 调用 使用await
try {
	const message = await alarm("name", 2000);
  output.textContent = message;
} catch (error) {
	output.textContent = `Couldn't set alarm: ${error}`;
}

```



##### workers

实现在不同线程中运行某些任务的能力。

主代码和 worker 代码永远不能直接访问彼此的变量。 workers 和主代码运行在完全分离的环境中中，只有通过互相发送消息来交互。workers 不能访问 DOM。

workers 类型：

* dedicated workers
* shared workers  可以由运行在不同窗口中的多个不同脚本共享
* service workers  行为像代理服务器，缓存资源以便 web 应用程序可以在用户离线时工作，是渐进式 web 应用的关键组件



```js
// 交互的例子
// main.js 
// 被添加到 html 中
// 创建 worker 对象
const worker = new Worker("./generate.js");

// 发送消息
worker.postMessge({command: "generate", quota: quota});

// 监听来自 workder 的消息
worker.addEventListener("message", message => {
  console.log("msg = " +  message.data);
});


// generate.js
// 监听来自主线程的消息
addEventListener("message", message => {
  if(message.data.command === "generate") {
    // 接收到消息 逻辑处理代码
    // 取出参数
    console.log(message.data.quota);
    ... 
    // 完成后给主线程发送消息
    postMessage();
  }
});
```



#### 客户端 Web API

web 页面视图中的浏览器的主要部分

* window 是载入浏览器的标签，在 js 中用 Window 对象来表示，使用这个对象可以拿到窗口的大小（window.width 和 window.height），操作载入窗口的文档、存储客户端上文档的特殊数据、为当前窗口绑定 event handler 等
* navigator 表示浏览器存在于 web 上的状态和标识（即用户代理），在 js 中使用 Navigator 表示，可以获取地理信息、偏爱语言、多媒体流等
* document 是载入窗口的实际页面，在 js 中使用 Document 对象表示，使用改对象返回和操作文档中的 HTML 和 CSS



#### 客户端存储

* cookies  旧方式

* Web Storageg   存储和检索较小的、键值对形式的数据

  * sessionStorage 关闭浏览器丢失

  * localStorage 重启浏览器也不会丢失

    ```js
    // 存储数据
    localStorage.setItem(key, value);
    // 获取数据
    localstorage.getItem(key);
    // 删除数据
    localstorage.removeItem(key);
    ```

    

* indexedDB，简称 IDB   在浏览器中的数据库系统，复杂数据

  ```js
  // 初始化
  let db;
  window.onload = function() {
    // 数据库名字： notes，版本号：1
    let request = window.indexedDB.open("notes", 1);
    request.onerror = function () {
      console.log("Database failed to open");
    };
    request.onsuccess = function () {
      console.log("Database opened successfully");
      db = request.result;
      displayData();
    };
  
    // 版本升级时逻辑
    request.onupgradeneeded = function (e) {
      let db = e.target.result;
      // 新建表 notes
      let objectStore = db.createObjectStore("notes", {
        keyPath: "id",
        autoIncrement: true,
      });
      objectStore.createIndex("title", "title", { unique: false });
      objectStore.createIndex("body", "body", { unique: false });
      console.log("Database setup complete.");
    };
  }
  
  // 添加记录
  function addData() {
    let newItem = { title: titleInput.value, body: bodyInput.value };
    let transaction = db.transaction(["notes"], "readwrite");
    let objectStore = transaction.objectStore("notes");
    // 添加
    var request = objectStore.add(newItem);
    // 成功监听事件
    request.onsuccess = function () {
      titleInput.value = "";
      bodyInput.value = "";
    };
    // 完成监听事件
    transaction.oncomplete = function () {
      console.log("Transaction completed");
      displayData();
    };
    // 错误监听事件
    transaction.onerror = function () {
      console.log("Transaction failed");
    };
  }
  
  // 查询记录
  function show() {
    let objectStore = db.transaction("notes").objectStore("notes");
    objectStore.openCursor().onsuccess = function (e) {
      let cursor = e.target.result;
      if (cursor) {
        var title = cursor.value.title;
        var body = cursor.value.body;
      }
    }
  }
  
  // 删除记录
  function deleteItem(e) {
    let noteId = Number(e.target.parentNode.getAttribute("data-note-id"));
    let transaction = db.transaction(["notes"], "readwrite");
    let objectStore = transaction.objectStore("notes");
    // 根据 id 删除
    let request = objectStore.delete(noteId);
    // 删除成功监听
    transaction.oncomplete = function () {
      
    };
  }
  
  ```



* Cache API  同 service worker 结合实现离线访问



### 表单

form 元素，属性介绍

* action 定义了在线提交表单时，应该把所收集的数据给谁（URL 接口）
* method 发送数据的 HTTP 方法

包含的元素

* label  
  * 为表单小部件定义标签（介绍文本）
  * 定义 for 属性，将标签链接到表单的方式
* input 
  * type 定义输入类型，值包含：text（默认值）、email、radio、file、checkbox、hidden、image、password、reset、submit、button
  * 定义 id 属性，同 label 的 for 属性值相同
  * name 属性，属性值为传入接口的参数名
  * 设置默认值设置 value="--"
* textarea  
  * 定义 id 属性，同 label 的 for 属性值相同 
  * 设置默认值在标签中： ---
  * name 属性，属性值为传入接口的参数名
* button
  * 表单中的按钮
  * type 属性的取值
    * submit 默认值，发送表单的数据到 action 所定义的网页
    * reset  将表单所有小部件的值恢复为默认值
    * button  不会发生任何事，用 JS 构建定制按钮时用
* 元素：fieldset 、legend
  * fieldset 创建相同目的的小部件，例如一组单选按钮
  * legend 为 fieldset 的标签，内容描述部件的用途





```js
// 常见表单部件
<form>
  
  // 单行文本框  约束：如果您输入带有换行符的文本，浏览器会在发送数据之前删除这些换行符。
  <input type="text" id="comment" name="comment" value="I'm a text field">
  
  // 隐藏内容 界面上不显示，传入时间戳用
  <input type="hidden" id="timestamp" name="timestamp" value="1286705410">
  
  // 单选框
  <fieldset>
  	<legend>What is your favorite meal?</legend>
  	<ul>
    	<li>
      	<label for="soup">Soup</label>
      	<input type="radio" id="soup" name="meal" value="soup" checked>
    	</li>
    	<li>
      	<label for="curry">Curry</label>
      	<input type="radio" id="curry" name="meal" value="curry">
    	</li>
    	<li>
      	<label for="pizza">Pizza</label>
      	<input type="radio" id="pizza" name="meal" value="pizza">
    	</li>
  	</ul>
	</fieldset>
    
    
  // 复选框
	<fieldset>
  	<legend>Choose all the vegetables you like to eat</legend>
  	<ul>
    	<li>
      	<label for="carrots">Carrots</label>
      	<input type="checkbox" id="carrots" name="vegetable" value="carrots" checked>
    	</li>
    	<li>
      	<label for="peas">Peas</label>
      	<input type="checkbox" id="peas" name="vegetable" value="peas">
    	</li>
    	<li>
      	<label for="cabbage">Cabbage</label>
      	<input type="checkbox" id="cabbage" name="vegetable" value="cabbage">
    	</li>
  	</ul>
	</fieldset>


  
  // 文件选择 
  // 图片 多张
  <input type="file" name="file" id="file" accept="image/*" multiple>
  // 相机图片
  <input type="file" accept="image/*;capture=camera">
  // 视频
  <input type="file" accept="video/*;capture=camcorder">
  // 音频
	<input type="file" accept="audio/*;capture=microphone">

</form>
```







### 发布网站

#### 使用 GitHub pages 发布

要求：

* 项目名：xxx.github.io // xxx 为当前 github 账号的用户名
* 项目中包含一个 `index.html` 文件

项目代码提交之后，就可以看通过 https://xxx.github.io/ 访问到。



### 万维网如何工作的

#### 客户端和服务器

连接到互联网的计算机称作客户端和服务器。

* 客户端是典型的 Web 用户入网设备（连接了网络的电脑和手机）和设备上可联网的软件（chrome 浏览器）
* 服务器是存储网页，站点和应用的计算机

#### 其他部分

* 网络连接：允许在互联网上发送和接收数据
* TPC/IP：传输控制协议和因特网互连协议是定义数据如何传输的通信协议
* DNS：域名系统服务器是网站通讯录，浏览器内输入网址，获取网页之前会查看域名系统
* HTTP：超文本传输协议是一个定义客户端和服务器间交流的语言和协议
* 组成文件：一个网页有许多文件组成，这些文件分为：
  * 代码：HTML、CSS、JavaScript
  * 资源：图像、音乐、视频、word 文档、pdf 文件

#### 输入网址后发生了什么

1. DNS 查询存放网页的服务器的实际地址
2. 浏览器发送 HTTP 请求到服务器，拷贝一份网页到客户端
3. 服务器同意请求后，返回“200 OK”信息，然后将网页文件以数据包的形式传输给浏览器
4. 浏览器将数据包聚集成完整的网页呈现出来

#### HTML 文件被浏览器解析的顺序

* 首先解析 HTML 文件，识别所有 link 和 script 元素，获取它们指向的外部文件的链接
* 继续解析 HTML 的同时，根据外部文件的链接向服务器发送请求，获取并解析 CSS 文件和 JavaScrite 文件
* 将解析后的 HTML 文件生成一个 DOM 树（在内存中），给解析后的 CSS 文件生成一个 CSSOM 树（在内存中），并且会编译和执行解析后的 JavaScript 文件
* 构建 DOM 树、CSSOM 树，执行 JavaScript 文件的同时，在屏幕上绘制出网页的界面；用户看到网页界面就可以跟网页进行交互了



