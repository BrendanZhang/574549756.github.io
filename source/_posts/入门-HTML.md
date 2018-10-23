---
title: 入门-HTML
date: 2018-03-22 16:13:21
tags: HTML
categories: HTML
---
## 1.什么是HTML

### I. HTML
是超文本标记语言（**H**yper**T**ext**M**arkup **L**anguage，简称：**HTML**）是一种用于创建网页的标准标记语言。
### II. HTML版本(W3C组织制定规范)：
  i. HTML 4.01
  ii.XHTML
  iii. HTML 5
  iv. HTML 5.1
### III. 规范文档(Specification)
  i. 由W3C写文档（Sir Timothy John Berners-Lee）
  ii. W3C根据浏览器的实际情况总结文档，并不是凭空想象。
### IV. DOCTYPE
  i. 用来选择文档类型
  ii. DOCTYPE
  
  |版本|DOCTYPE|
  |:---:|:---:|
  |HTML 5及以上|<!DOCTYPE HTML>|
  |HTML 4.01 Strict|<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN""http://www.w3.org/TR/html4/strict.dtd"|
   |HTML 4.01 Transitional|<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN""http://www.w3.org/TR/html4/loose.dtd">|
   |HTML 4.01 Frameset|<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN""http://www.w3.org/TR/html4/frameset.dtd">|
   |XHTML 1.0 Strict|<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN""http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">|
   |XHTML 1.0 Transitional|<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN""http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">|
   |XHTML 1.0 Frameset|<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN""http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">|
   |XHTML 1.1 DTD|<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">|
   |XHTML Basic 1.1 (quick reference)|<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML Basic 1.1//EN""http://www.w3.org/TR/xhtml-basic/xhtml-basic11.dtd">|
   如果不写，就是个GG
   
## 2.W3C
I. 万维网联盟（World Wide Web Consortium，W3C），又称W3C理事会，是万维网的主要国际标准组织。李爵士创立。
II. 该组织试图通过W3C制定的新标准来促进业界成员间的兼容性和协议。不兼容的HTML版本由不同的供应商提供，导致网页显示方式不一致。联盟试图让所有的供应商实施一套由联盟选择的核心原则和组件。
III. 总结一下，制定规范的组织。

## 3.MDN
I. MDN Web Docs（旧称Mozilla Developer Network、Mozilla Developer Center，简称MDN）是一个汇集众多Mozilla基金会产品和网路技术开发文档的免费网站。
II. 就是查文档的。

## 4.HTML标签
### I.标签
|类型|元素|描述|备注|
|:---:|:---:|:---:|:---:|
|根元素|`<html>`|代表 HTML 或 XHTML 文档的根。其他所有元素必须是这个元素的子节点。|包含全局属性|
|文档元数据|`<head>`|代表关于文档元数据的一个集合，包括脚本或样式表的链接或内容。|该元素包含全局属性。可用于`<head>`元素内的元素有: `<title>, <base>, <link>, <style>, <meta>, <script>, <noscript>, <command>`|
||`<title>`|定义文档的标题，将显示在浏览器的标题栏或标签页上。该元素只能包含文本，包含的标签不会被解释。|仅拥有全局属性，允许内容为非空字符或特殊字符（inter-element whitespace）的文本。	一个 `<head>` 元素只能包含一个 `<title>`元素|
||`<base>`|定义页面上相对 URL 的基准 URL。|允许空标签，不可以有结束标签。|
||`<link>`|用于链接外部的 CSS 到该文档。|这是一个空标签，鉴于他也是空元素，所以也不可有结束标签|
||`<meta>`|定义其他 HTML 元素无法描述的元数据。|也是个空标签，所以有始不能有终|
||`<style>`|用于内联 CSS。|内容为匹配type属性指定的语言的样式信息。标签始终都不能省略|
|脚本|`<script>`|定义一个内联脚本或链接到外部脚本。脚本语言是 JavaScript。|内容为动态脚本。包含全局属性而且拥有以下类别：`<async><defer> <integrity><src><type><text><crossorigin>`|
||`<noscript>`|定义当浏览器不支持脚本时显示的替代文字。|仅拥有全局元素|
||`<template>`|通过 JavaScript 在运行时实例化内容的容器。|是一种用于保存客户端内容的机制，该内容在页面加载时不被渲染，但可以在运行时使用JavaScript进行实例化。，加载页面的同时,解析器确实处理 `<template>`元素的内容，这样做只是确保这些内容是有效的; 然而,元素的内容不会被渲染|
|章节|`<body>`|代表 HTML 文档的内容。在文档中只能有一个 <body> 元素。|它必须是 `<html>` 元素的直接子元素。|
||`<section>`|定义文档中的一个章节。|内容中的一个专题组，一般来说会有包含一个标题（heading）。一般通过是否包含一个标题` (<h1>-<h6> element)` 作为子节点 来 辨识每一个`<section>`。允许内容：流式元素|
||`<nav>`|定义只包含导航链接的章节。|用于描述一个含有多个超链接的区域，这个区域包含转到其他页面，或者页面内部其他部分的链接列表。允许内容：流式元素|
||<article>|定义可以独立于内容其余部分的完整独立内容块。|表示文档、页面、应用或网站中的独立结构，其意在成为可独立分配的或可复用的结构，如在发布中，它可能是论坛帖子、杂志或新闻文章、博客、用户提交的评论、交互式组件，或者其他独立的内容项目。允许元素：流式元素|
||`<h1>,<h2>,<h3>,<h4>,<h5>,<h6>`|标题元素实现了六层文档标题，`<h1>` 是最大的标题，`<h6>` 是最小的标题。标题元素简要地描述章节的主题。|标题顺序从1到6顺序排列，不要为了改变字体大小跳过顺序使用标题，应该用CSS样式改变字体。允许内容：短语元素|
||`<header>`|定义页面或章节的头部。它经常包含 logo、页面标题、搜索表单和导航性的目录。|允许内容：流式元素|
||`<footer>`|定义页面或章节的尾部。它经常包含版权信息、法律信息链接和反馈建议用的地址。|允许内容：流式元素，但是不能包含`<footer>`或者`<header>`。|
||`<address>`|定义包含联系信息的一个章节。|允许内容：流式元素但是不能是内嵌的`<address>`元素、标题元素、章节元素|
||`<main>`|定义文档中主要或重要的内容。|允许内容：流式元素|
|组织内容|`<p>`|定义一个段落。|表示文本的一个段落。该元素通常表现为一整块与相邻文本分离的文本，或以垂直的空白隔离或以首行缩进。另外，`<p>`是块级元素。允许元素：短语元素|
||`<hr>`|代表章节、文章或其他长内容中段落之间的分隔符。|允许内容：无，这是一个空元素。所以有始无终。|
||`<pre>`|代表其内容已经预先排版过，格式应当保留 。|允许内容：短语元素|
||`<blockquote>`|代表引用自其他来源的内容。（块级引用）|代表其中的文字是引用内容。通常在渲染时，这部分的内容会有一定的缩进（注 中说明了如何更改）。若引文来源于网络，则可以将原内容的出处 URL 地址设置到 cite 特性上，若要以文本的形式告知读者引文的出处时，可以通过 `<cite>` 元素。允许内容：流式元素|
||`<ol>`|定义一个有序列表。|表示多个有序列表项，通常渲染为有带编号的列表。允许内容：一个或多个`<li>`元素。这些`<li>`元素可以再包含嵌套的`<ol>`或`<ul>`元素。|
||`<ul>`|定义一个无序列表。|代表多项的无序列表，即无数值排序项的集合，且它们在列表中的顺序是没有意义的。通常情况下，无序列表项的头部可以是几种形式，如一个点，一个圆形或方形。头部的风格并不是在页面的HTML描述定义, 但在其相关的CSS 可以用 list-style-type 属性。允许内容：一个或多个`<li>`元素。这些`<li>`元素可以再包含嵌套的`<ol>`或`<ul>`元素。|
||`<li>`|定义列表中的一个列表项。|用于表示列表里的条目。它必须被包含在一个父元素里：一个有顺序的列表(`<ol>`)，一个无顺序的列表(`<ul>`)，或者一个菜单 (`<menu>`)。在菜单或者无顺序的列表里，列表条目通常用点排列显示。在有顺序的列表里，列表条目通常是在左边有按升序排列计数的显示，例如数字或者字母。元素类型：块级 允许内容：流式内容|
||`<dl>`|HTML `<dl> `元素 （或 HTML 描述列表元素）是一个包含术语定义以及描述的列表，通常用于展示词汇表或者元数据 。|允许内容：一个或者多个`<dt>`元素。这些`<dt>`元素可以再包含嵌套的`<dd>`元素|
||`<dt>`|HTML `<dt>` 元素 （或 HTML 术语定义元素）用于在一个定义列表中声明一个术语。该元素仅能作为 `<dl>` 的子元素出现。通常在该元素后面会跟着 `<dd>` 元素， 然而，多个连续出现的 `<dt>` 元素都将由出现在它们后面的第一个 `<dd>` 元素定义。 |允许的内容：流式内容 但是不能包含 `<header>` 元素、`<footer>` 元素或者其他章节、标题内容。|
||`<dd>`|HTML `<dd>` 元素（HTML 描述元素）用来指明一个描述列表  (`<dl>`) 元素中一个术语的描述。这个元素只能作为描述列表元素的子元素出现，并且必须跟着一个 `<dt>` 元素。|允许的内容：流式元素|
||`<figure>`|代表一个和文档有关的图例。|`<figure>` 元素代表一段独立的内容, 经常与说明(caption) `<figcaption>` 配合使用, 并且作为一个独立的引用单元。当它属于主体(main flow)时，它的位置独立于主体。这个标签经常是在主文中引用的图片，插图，表格，代码段等等，当这部分转移到附录中或者其他页面时不会影响到主体。允许的内容：flow content中的`<figcaption>` 元素; 或者`<figcaption>` 元素中的flow content ; 或者 flow content.|
||`<figcaption>`|代表一个图例的说明。|`<figcaption>` 元素 是与其相关联的图片的说明/标题，用?于描述其父节点 `<figure>` 元素里的其他数据。这意味着 <figcaption> 在<figure> 块里是第一个或最后一个。同时 HTML Figcaption 元素是可选的；如果没有该元素，这个父节点的图片只是会没有说明/标题。允许的内容：流式元素|
||`<div>`|代表一个通用的容器，没有特殊含义。|`<div>`元素 (或 HTML 文档分区元素) 是一个通用型的流内容容器，它在语义上不代表任何特定类型的内容，它可以被用来对其它元素进行分组，一般用于样式化相关的需求（使用 class 或 id 特性) 或者对具有相同特性的一组元素进行分组 (比如 lang)，它应该在没有任何其它语义元素可用时才使用 (比如 `<article>` 或 `<nav>`) 。**没有默认样式!!!**允许的内容：流式元素|
|文字形式|`<a>`|代表一个链接到其他资源的超链接 。|`<a>` 元素  (或锚元素) 可以创建一个到其他网页、文件、同一页面内的位置、电子邮件地址或任何其他URL的超链接。允许内容：透明内容模型、流式元素、短语元素|
||`<em>`|代表强调的文字。|着重元素 (`<em>`) 标记出需要用户着重阅读的内容， <em> 元素是可以嵌套的，嵌套层次越深，则其包含的内容被认定为越需要着重阅读。通常展现为斜体。允许内容：短语元素|
||`<strong>`|代表特别重要的文字。|Strong 元素 (`<strong>`)表示文本十分重要，一般用粗体显示。允许内容：短语元素|
||`<small>`|代表注释 ，如免责声明、版权声明等，对理解文档不重要。|`<small>`元素將使文本的字体变小一号。(例如从大变成中等，从中等变成小，从小变成超小)。在HTML5中，除了它的样式含义，这个元素被重新定义为表示边注释和附属细则，包括版权和法律文本。允许内容：短语元素|
||`<s>`|代表不准确或不相关 的内容。|`<s>` 元素 使用删除线来渲染文本。使用 <s> 元素来表示不再相关，或者不再准确的事情。但是当表示文档编辑时，不提倡使用 <s> ；为此，提倡使用 `<del>` 和 `<ins>` 元素。允许的内容：短语元素|
||`<cite>`|代表作品标题。|HTML引用（Citation）标签 (<cite>) 表示一个作品的引用。它必须包含引用作品的符合简写格式的标题或者URL，它可能是一个根据添加引用元数据的约定的简写形式。允许内容：流式元素、短语元素|
||`<q>`|代表内联的引用 。|引用标签 (`<q>`)表示一个封闭的并且是短的行内引用的文本. 这个标签是用来引用短的文本，所以请不要引入换行符; 对于长的文本的引用请使用 `<blockquote>` 替代。|
||`<dfn>`|代表一个术语包含在其最近祖先内容中的定义 。|定义元素 (`<dfn>`) 表示术语的一个定义。`<dfn>` 元素标记了被定义的术语；术语定义应当在 `<p>`, `<section>`或定义列表 (通常是`<dt>`, `<dd>` 对)中给出。被定义术语的值由下列规则确定：如果 `<dfn>` 元素有一个 title 属性，那么该术语的值就是该属性的值。否则，如果它仅包含一个 `<abbr>` 元素，该元素拥有 title 属性，那么该术语的值就是该属性的值。否则，`<dfn>` 元素的文本内容就是该术语的值。|
||`<abbr>`|代表省略或缩写，其完整内容在 title 属性中。|允许内容：短语元素|
||`<data>`|关联一个内容的机器可读的等价形式 （该元素只在 WHATWG 版本的 HTML 标准中，不在 W3C 版本的 HTML5 标准中）。|<data> 元素 将一个指定内容和机器可读的翻译联系在一起。但如果内容是与 time 或者 date 相关的，一定要使用 `<time>`。允许内容：短语元素|
||`<time>`|代表日期 和时间 值；机器可读的等价形式通过 datetime 属性指定。|time 标签(`<time>`) 用来表示24小时制时间或者公历日期，若表示日期则也可包含时间和时区。此元素意在以机器可读的格式表示日期和时间。 有安排日程表功能的应用可以利用这一点。允许内容：短语元素，但不能包含time元素|
||`<code>`|	代表计算机代码 。|<code> 元素呈现一段计算机代码. 默认情况下, 它以浏览器的默认等宽字体显示。允许元素：短语元素|
||`<var>`|代表代码中的变量 。|<var> 标签表示变量的名称，或者由用户提供的值。允许元素：短语元素|
||`<samp>`|代表程序或电脑的输出 。|`<samp>` 元素用于标识计算机程序输出，通常使用浏览器默认的 monotype 字体。允许内容：短语元素|
||`<kbd>`|代表用户输入 ，一般从键盘输出，但也可以代表其他输入，如语音输入。|键盘输入元素(`<kbd>`) 用于表示用户输入，它将产生一个行内元素，以浏览器的默认monospace字体显示。允许内容：短语元素|
||`<sub>,<sup>`|分别代表下标 和上标 。|`<sub>` 元素定义了一个文本区域，出于排版的原因，与主要的文本相比，应该展示得更低并且更小。`<sup>` 元素定义了一个文本区域，出于排版的原因，与主要的文本相比，应该展示得更高并且更小。允许内容：短语元素。|
||`<i>`|代表一段不同性质 的文字，如技术术语、外文短语等。|<i> 用于表现因某些原因需要区分普通文本的一系列文本。例如技术术语、外文短语或是小说中人物的思想活动等，它的内容通常以斜体显示。允许内容：短语元素|
||`<b>`|代表一段需要被关注 的文字。|提醒注意（Bring Attention To）元素（`<b>`）用于吸引读者的注意到该元素的内容上（如果没有另加特别强调）。这个元素过去被认为是粗体（Boldface）元素，并且大多数浏览器仍然将文字显示为粗体。尽管如此，你不应将 `<b>` 元素用于显示粗体文字；替代方案是使用 CSS font-weight 属性来创建粗体文字。允许内容：短语元素|
||`<u>`|代表一段需要下划线呈现的文本注释，如标记出拼写错误的文字等。|`<u>` 元素使文本在其内容的基线下的一行呈现下划线。在HTML5中, 此元素表示具有未标注的文本跨度，显示渲染，非文本注释，例如将文本标记为中文文本中的专有名称(一个正确的中文标记), 或 将文本标记为拼写错误。允许内容：短语元素|
||`<mark>`|代表一段需要被高亮的引用的文字。|可以用来显示搜索引擎的关键词，允许的内容：短语元素|
||`<ruby>`|代表被ruby 注释 标记的文本，如中文汉字和它的拼音。|<ruby> 元素 被用来展示东亚文字注音或字符注释。允许内容：短语元素|
||`<rt>`|代表ruby 注释 ，如中文拼音。|Ruby 文本 (<rt>) 元素包含字符的发音，字符在 ruby 注解中出现，它用于描述东亚字符的发音。这个元素始终在 <ruby> 元素中使用。允许内容：短语元素|
||`<rp>`|代表 ruby 注释两边的额外插入文本 ，用于在不支持 ruby 注释显示的浏览器中提供友好的注释显示。|<rp> 元素用于为那些不能使用 <ruby> 元素展示 ruby 注解的浏览器，提供随后的圆括号。允许的内容：短语元素|
||`<bdi>`|代表需要脱离 父元素文本方向的一段文本。它允许嵌入一段不同或未知文本方向格式的文本。|`<bdi>` 元素 (双向隔离元素) 会隔离可能以不同方向进行格式化的外部文本。当不知道是从什么方向嵌入文本，如来自于数据库的文本（有起数据库的文本方向）的时候，该元素是十分有用的。允许内容：短语元素|
||`<span>`|代表一段没有特殊含义的文本，当其他语义元素都不适合文本时候可以使用该元素。|`<span>` 元素是短语内容的通用行内容器，并没有任何特殊语义。可以使用它来编组元素以达到某种样式意图（通过使用类或者Id属性），或者这些元素有着共同的属性，比如lang。应该在没有其他合适的语义元素时才使用它。`<span>` 与 `<div>` 元素很相似，但 `<div>` 是一个 块元素 而 `<span>` 则是 行内元素。**没有默认样式没有默认样式！！！**允许内容：短语元素|
||`<br>`|代表换行。|`<br>` 元素在文本中生成一个换行（回车）符号。此元素在写诗和地址时很有用，这些地方的换行都非常重要。允许内容：无，这是一个空元素|
||`<wbr>`|代表建议换行 (Word Break Opportunity) ，当文本太长需要换行时将会在此处添加换行符。|<wbr> 元素  — 一个文本中的位置，其中浏览器可以选择来换行，虽然它的换行规则可能不会在这里换行。允许内容：无，这是一个空元素|
|编辑|`<ins>`|定义增加到文档的内容。|`<ins>` 元素定义已经被插入文档中的文本。允许内容：透明内容模型|
||`<del>`|定义从文档移除 的内容。|`<del>`标签表示一些被从文档中删除的文字内容。比如可以在需要显示修改记录或者源代码差异的情况使用这个标签。`<ins>`标签的作用恰恰于此相反：表示文档中添加的内容。这个标签通常（但不一定要）在文字上显示删除线。允许内容：透明内容模型|
|嵌入内容|`<img>`|代表一张图片 。|允许内容：无 这是一个空元素 有始无终 父元素：接受嵌入式内容的任意元素|
||`<iframe>`|代表一个内联的框架 。|内联框架元素 `<iframe>` 表示嵌套的浏览上下文，有效地将另一个HTML页面嵌入到当前页面中。在HTML 4.01中，文档可能包含头部和正文，或头部和框架集，但不能包含正文和框架集。但是，`<iframe>`可以在正常的文档主体中使用。每个浏览上下文都有自己的会话历史记录和活动文档。包含嵌入内容的浏览上下文称为父浏览上下文。顶级浏览上下文（没有父级）通常是浏览器窗口。允许元素：流式元素、短语元素、嵌入元素、。|
||`<embed>`|代表一个嵌入 的外部资源，如应用程序或交互内容。|`<embed>`元素将外部内容嵌入文档中的指定位置。此内容由外部应用程序或其他交互式内容源（如浏览器插件）提供。允许内容：流式元素、短语元素、嵌入元素|
||`<object>`|代表一个外部资源 ，如图片、HTML 子文档、插件等。|`<object>` 元素（或者称作 HTML 嵌入对象元素）表示引入一个外部资源，这个资源可能是一张图片，一个嵌入的浏览上下文，亦或是一个插件所使用的资源。允许内容：流式元素、短语元素、嵌入元素|
||`<param>`|`<param> `元素(或 HTML Parameter 元素) 定义了 `<object>`的参数|允许内容：空元素 有始无终|
||`<video>`|代表一段视频 及其视频文件和字幕，并提供了播放视频的用户界面。|`<video>` 元素 用于在HTML或者XHTML文档中嵌入视频内容。允许内容：流式元素，包含任一 src 属性或是一个或多个 `<source>` 元素，其后紧跟流式元素 或 短语元素 ， 不包括`<video>` 或者 `<audio>` 元素。|
||`<audio>`|代表一段声音 ，或音频流 。|`<audio>` 元素用于在文档中表示音频内容。 `<audio>` 元素可以包含多个音频资源， 这些音频资源可以使用 src 属性或者`<source>` 元素来进行描述； 浏览器将会选择最合适的一个来使用。对于不支持`<audio>`元素的浏览器，`<audio>`元素也可以作为浏览器不识别的内容加入到文档中。允许内容：如果元素包含 src 属性：零个或多个 `<track>` 元素，其后紧跟不包含 `<audio>` 或者 `<video>`媒体元素的透明内容。或者：零个或多个 `<source>` 元素，其后紧跟零个或多个 `<track>` 元素，其后紧跟不包含 `<audio>` 或者 `<video>`媒体元素的透明内容。|
||`<source>`|为 `<video>` 或 `<audio>` 这类媒体元素指定媒体源 。|允许内容：一个 `<picture>` 元素, 且在`<img>`元素之前|
||`<track> `|为 `<video>` 或 `<audio>` 这类媒体元素指定文本轨道（字幕） 。|`<track>` 元素 被当作媒体元素—`<audio>` 和 `<video>`的子元素来使用。它允许指定计时字幕（或者基于事件的数据），例如自动处理字幕。track 给媒体元素添加的数据的类型在 kind 属性中设置，属性值可以是`subtitles`, `captions`, `descriptions`, `chapters` 或 `metadata`。该元素指向当用户请求额外的数据时浏览器公开的包含定时文本的源文件。一个`media` 元素的任意两个 `track` 子元素不能有相同的 `kind`, `srclang`, 和 `label`属性。允许内容：空，这是一个空元素|
||`<canvas>`|代表位图区域 ，可以通过脚本在它上面实时呈现图形，如图表、游戏绘图等。|`<canvas>`元素可被用来通过脚本（通常是JavaScript）绘制图形。比如,它可以被用来绘制图形,制作图片集合,甚至用来实现动画效果。你可以(也应该)在元素标签内写入可提供替代的的代码内容，这些内容将会在在旧的、不支持`<canvas>`元素的浏览器或是禁用了JavaScript的浏览器内渲染并展现。|
||`<map>`|与 `<area>` 元素共同定义图像映射 区域。|<map> 属性 与 <area> 属性一起使用来定义一个图像映射(一个可点击的链接区域).允许内容：任何透明元素模型|
||`<area>`|与 <map> 元素共同定义图像映射 区域。|<area> 元素 在图片上定义一个热点区域，可以关联一个超链接。<area>元素仅在<map>元素内部使用。允许内容：空，这是一个空元素 有始无终|
||`<svg>`|定义一个嵌入式矢量图 。|如果svg不是根元素，svg 元素可以用于在当前文档（比如说，一个HTML文档）内嵌套一个独立的svg片段。这个独立片段拥有独立的视口和坐标系统。允许内容：任意数量、任意排序的下列元素：动画元素；描述性元素；形状元素；结构化元素；渐变元素；`<a>, <altGlyphDef>, <clipPath>, <color-profile>, <cursor>, <filter>, <font>, <font-face>, <foreignObject>, <image>, <marker>, <mask>, <pattern>, <script>, <style>, <switch>, <text>, <view>`|
||`<math>`|定义一段数学公式 。|MathML的顶级元素是`<math>`。所有有效的MathML实例必须被包括在 `<math>` 标记中。另外不可以在一个 `<math>` 元素中嵌套第二个` <math>` 元素，但是 `<math>` 元素中可以有任意多的子元素 。|
|表格|`<table>`|定义多维数据 。|在 CSS 创建之前， HTML `<table>` 元素常常被用于布局页面。 这种用法在 HTML 4之后不被推荐使用，并且 `<table>`元素 不应该 被用于此目的。允许内容：按照这个顺序：一个可选的 `<caption>` 元素；零个或多个的 `<colgroup>` 元素；一个可选的 `<thead>` 元素；一个可选的 `<tfoot>` 元素（tfoot元素出现在tbody或tr元素前后都可以。在HTML4中，它只能出现在这些元素之前）；零个或多个 `<tbody>` 元素；一个或多个 `<tr>` 元素；|
||`<caption>`|代表表格的标题。|`<caption>` 元素 (or HTML 表格标题元素) 展示一个表格的标题， 它常常作为 `<table>` 的第一个子元素出现，同时显示在表格内容的最前面，但是，它同样可以被CSS样式化，所以，它同样可以出现在任何一个一个相对于表格的做任意位置。允许内容：流式元素|
||`<colgroup>`|代表表格中一组单列或多列。|表格列组（Column Group `<colgroup>`） 标签用来定义表中的一组列表。若`span`属性为`present`: 那它就是一个空属性。如果属性不是`present`内容为：零或多个`<col>`属性|
||`<col>`|代表表格中的列。|`<col>` 元素 定义表格中的列，并用于定义所有公共单元格上的公共语义。它通常位于<colgroup>元素内。允许内容：这是一个空元素有始无终|
||`<tbody>`|代表表格中一块具体数据 （表格主体）。|允许内容：零或多个`<tr>`元素|
||`<thead>`|代表表格中一块列标签（表头）。|允许内容：零或多个`<tr>`元素|
||`<tfoot>`|代表表格中一块列摘要（表尾）|允许内容：零或多个`<tr>`元素|
||`<tr>`|代表表格中的行 。|允许内容：零或多个`<td>`或`<th>`元素|
||`<td>`|代表表格中的单元格 。|允许内容：流式元素|
||`<th>`|代表表格中的头部单元格 。|允许内容：流内容（除header、footer、sectioning content或heading content的继承。）|
|表单|`<form>`|代表一个表单 ，由控件组成。|<form> 元素 表示了文档中的一个区域，这个区域包含有交互控制元件，用来向web服务器提交信息。可以用 `:valid `和`:invalid` CSS 伪类 来给一个元素指定样式。允许内容：流式元素|
||`<fieldset>`|代表控件组 。|`fieldset`元素通常用来对表单中的控制元素进行分组(也包括 label 元素)允许内容：一个可选的` <legend> `元素，后面跟流式元素|
||`<legend>`|代表 `<fieldset>` 控件组的标题。|`<legend>`元素（也称为HTML的域说明元素（or HMTL Legend Field Element））代表一个用于表示它的父元素`<fieldset>`的内容的标题。允许内容：短语元素|
||`<label>`|代表表单控件的标题。## II.元素|它通常关联一个控件，或者是将控件放置在label元素内，或者是用作其属性。这样的控制称作label元素的labeled control。允许内容：没有后代`label`元素的短语元素。除了标记控制之外，不允许使用其他可标记的元素。|
||`<button>	`|代表按钮。|`<button>` 元素表示一个可点击的按钮，可以用在表单或文档其它需要使用简单标准按钮的地方。 默认情况下，HTML按钮的显示样式接近于 user agent 所在的宿主系统平台（用户操作系统）的按钮， 但你可以使用 CSS 来改变按钮的样貌。允许内容：短语元素|
||`<select>`|代表下拉框。|`<select>` 元素是一种表单控件，可创建选项菜单。菜单内的选项为`<option>` , 可以由 `<optgroup>` 元素分组。选项可以被用户预先选择。允许内容：0个或多个 `<option>` 或者 `<optgroup>` 元素|
||`<datalist>`|代表提供给其他控件的一组预定义选项 。|Datalist 元素 (`<datalist>`) 包含了一组<option>元素,这些元素表示其它表单控件可选值。允许内容：要么短语元素 要么 0个或多个 `<option>`元素.|
||`<optgroup>`|代表一个选项分组。|在一个web表单中, HTML元素` <optgroup> `会创建包含在一个 `<select>` 元素中的一组选项。允许内容：0或多个 `<option>` 元素|
||`<option>`|代表一个 `<select>` 元素或 `<datalist>` 元素中的一个选项| HTML元素 `<option>`  用于定义在`<select>`,  `<optgroup>` 或`<datalist>` 元素中包含的项。`<option>` 可以在弹出窗口和 html 文档中的其他项目列表中表示菜单项。允许内容：带有最终转义字符（例如 `&eacute;`）的文本|
||`<textarea>`|代表多行文本框 。|`<textarea>` 元素表示一个多行纯文本编辑控件。 允许内容：文字|
||`<keygen>`|代表一个密钥对生成器。|尽量不要使用了，该特性已从Web标准中删除。|
||`<output>`|代表计算值。|`<output>` 标签表示计算或用户操作的结果。允许内容：短语元素|
||`<progress>`|代表进度条 。|progress (`<progress>`) 元素用来显示一项任务的完成进度.虽然规范中没有规定该元素具体如何显示,浏览器开发商可以自己决定,但通常情况下,该元素都显示为一个进度条形式。允许内容：流式元素|
||`<meter>`|代表滑动条。| `<meter>`元素用来显示已知范围的标量值或者分数值。允许内容：短语元素，但不允许有<meter>元素作为其子元素。|
|交互元素|`<details>`|代表一个用户可以(点击)获取额外信息或控件的小部件。|`<details>` 元素被用作发现小部件，用户可以从其中检索附加信息。允许内容：`<summary>`后紧跟流式元素|
||`<summary>`|代表 `<details>` 元素的综述或标题。|<summary> 元素 用作 一个`<details>`元素的一个内容的摘要，标题或图例。如果 `<summary>` 元素在浏览器内不能被正确解析和渲染,，则会展示`<details>`标签内的其他内容。|
||`<menuitem>`|代表一个用户可以点击的菜单项。|用户可以通过HTML的 `<menuitem>` 标签生成一个弹出式菜单。这包括上下文菜单，以及按钮可能附带的菜单。这个标签可以被显式定义，带有文本标签和可选图标来描述其外观，或者作为一个间接命令，其行为由一个单独的元素定义。命令还可以选择包含复选框或分组共享单选按钮。（`<input type="checkbox">` 和 `<input type="radio">`.)|
||`<menu>`|代表菜单。|HTML <menu> 元素 呈现了一组用户可执行或激活的命令。这既包含了可能出现在屏幕顶端的列表菜单，也包含了那些隐藏在按钮之下、当点击按钮后显示出来的文本菜单。使用说明:  `<menu>` 和 `<ul>` 元素都呈现了无序列表元素。最主要的区别是 `<ul>` 主要是为了展示选项，而 `<menu>` 则是为了交互。允许内容：如果元素位于列表菜单内：流式元素；或者零个或多个活动的 `<li>`, `<script>`和`<template>`二选一。如果元素位于右键菜单（上下文菜单）：零个或多个事件，任何顺序中，`<menu>`(仅上下文菜单) `<menuitem>`、`<hr>`、`<script>`、`<template>`。|

---

### II.元素内容类型

每一个HTML元素都必须遵循定义了它可以包含哪一类内容的规则。 这些规则被归类为几个常见的元素内容模型（content model）。每个HTML元素都属于0个、1 个或多个内容模型，每个模型都有一些规则使得元素中的内容必须遵循一个HTML规范文档( HTML-conformant document)。

以下是三种类型的内容分类：

主内容类，描述了很多元素共享的内容规范；
表单相关的内容类，描述了表单相关元素共有的内容规范；
特殊内容类，描述了仅仅在某些特殊元素上才需要遵守的内容规范，通常这些元素都有特殊的上下文关系。

#### i.元数据内容（Metadata content）
此类元素 修改文档其余部分的陈述或者行为，建立与其他文档的链接，或者传达其他外带信息。
属于这一类的元素有：`<base>, <command>, <link>, <meta>, <noscript>, <script>, <style> and <title>.`
#### ii.流式元素（Flow content）
此类元素通常包含 文本或植入的内容。此类元素有：` <a>, <abbr>, <address>, <article>, <aside>, <audio>, <b>,<bdo>, <bdi>, <blockquote>, <br>, <button>, <canvas>, <cite>, <code>, <command>, <data>, <datalist>, <del>, <details>, <dfn>, <div>, <dl>, <em>, <embed>, <fieldset>, <figure>, <footer>, <form>, <h1>, <h2>, <h3>, <h4>, <h5>, <h6>, <header>, <hgroup>, <hr>, <i>, <iframe>, <img>, <input>, <ins>, <kbd>, <keygen>, <label>, <main>, <map>, <mark>, <math>, <menu>, <meter>, <nav>, <noscript>, <object>, <ol>, <output>, <p>, <pre>, <progress>, <q>, <ruby>, <s>, <samp>, <script>, <section>, <select>, <small>, <span>, <strong>, <sub>, <sup>, <svg>, <table>, <template>, <textarea>, <time>, <ul>, <var>, <video>, <wbr>` 以及 Text.

属于此类的少数其他元素（仅限于某种特殊情形，这些元素才会属于此类）：
`<area>`, 仅限于它作为<map>的子节点的情形
`<link>`, 仅限于itemprop属性存在的情形
`<meta>`, 仅限于itemprop属性存在的情形
`<style>`, 仅限于 scoped属性存在的情形
#### iii.章节元素（Sectioning content）
隶属于分节内容模型的元素 在当前的大纲中创建一个分节，此分节将定义`<header>`元素、`<footer> `元素和标题元素（heading content）的范围。
属于此类的元素有： `<article>, <aside>, <nav> and <section>`. 
#### iv.标题元素（Heading content）
标题内容 定义了分节的标题，而这个分节可能由一个明确的分节内容元素直接标记，也可能由标题本身隐式地定义。
属于此分类的元素有： `<h1>, <h2>, <h3>, <h4>, <h5>, <h6>` and `<hgroup>`.
#### v.短语元素（Phrasing content）
短语元素（Phrasing content） 规定文本和它包含的标记。 一些Phrasing content就构成了段落.
属于此类的元素有： `<abbr>, <audio>, <b>, <bdo>, <br>, <button>, <canvas>, <cite>, <code>, <command>, <datalist>, <dfn>, <em>, <embed>, <i>, <iframe>, <img>, <input>, <kbd>, <keygen>, <label>, <mark>, <math>, <meter>, <noscript>, <object>, <output>, <progress>, <q>, <ruby>, <samp>, <script>, <select>, <small>, <span>, <strong>, <sub>, <sup>, <svg>, <textarea>, <time>, <var>, <video>, <wbr>` 和 plain text (仅当所包含的内容不完全为空字符的时候).
一些其他的元素也属于这个分类，但是只有当如下特殊情况时才会实现:
`<a>`, 当它仅包含 phrasing content 时
`<area>`, 当它为`<map>` 元素的子元素时
`<del>`, 当它仅包含 phrasing content 时
`<ins>`, 当它仅包含 phrasing content 时
`<link>`, 如果itemprop属性存在的情形
`<map>`, 当它仅包含 phrasing content 时
`<meta>`,如果itemprop属性存在的情形
#### vi.嵌入元素（Embedded content）
Embedded content输入另一个资源或者将来自另一种标记语言或命名空间的内容插入到文档中。
属于此类的元素有：`<audio>, <canvas>, <embed>, <iframe>, <img>, <math>, <object>, <svg>, <video>`.
#### vii.交互元素（Interactive content）
交互式内容包含为用户交互而特别设计的元素。 
属于此类的元素有：`<a>，<button>，<details>，<embed>，<iframe>，<keygen>，<label>，<select>` 和 `<textarea>`。
仅在特殊情形下才会属于此类的元素有:
`<audio>`, 若controls属性存在
`<img>`, 若usemap属性存在
`<input>`, 若type属性不处于隐藏（hidden）状态
`<menu>`, 若type属性处于工具栏（toolbar）状态
`<object>`, 若usemap属性存在
`<video>`, 若controls属性存在
#### viii.表单相关内容（Form-associated content）
表单相关的内容 包含 拥有表单父节点（exposed by a form attribute）的元素，一个表单父节点可以是`<form>`元素，也可以是其id在表单属性中被指定了的元素。（Form-associated content comprises elements that have a form owner, exposed by a form attribute. A form owner is either the containing `<form>` element or the element whose id is specified in the form attribute.）
`<button>`
`<fieldset>`
`<input>`
`<keygen>`
`<label>`
`<meter>`
`<object>`
`<output>`
`<progress>`
`<select>`
`<textarea>`
 此类包含了几个子类：
**可列举的元素（listed）**
在 form.elements 和 fieldset.elements IDL collections中列举出的元素. 包括 `<button>，<fieldset>，<input>，<keygen>，<object>，<output>，<select>` 和 `<textarea>`。
**可标签的元素（labelable）**
和 `<label>` 相关联的元素。包括 `<button>，<input>，<keygen>，<meter>，<output>，<progress>，<select>` 和 `<textarea>`。
**可提交的元素（submittable）**
包括当表单提交时可以用来组成表单数据的元素。 包括 `<button>，<input>，<keygen>，<object>，<select>` 和 `<textarea>`.
**可重置的元素（resettable）**
当表单重置时会被重置的元素。包括 `<input>，<keygen>，<output>，<select>` 和 `<textarea>`.
#### ix.透明内容模型（Transparent content model）
如果一个元素拥有 transparent content mode， 即使将透明内容更换为子元素，其内容必须由合法的HTML5元素组成。
例如，`<del>` 和 `<ins>` 是透明的：
`<p>We hold these truths to be <del><em>sacred &amp; undeniable</em></del> <ins>self-evident</ins>.</p>`
如果这两个元素被移除，这个程序段依然是合法的。
`<p>We hold these truths to be <em>sacred &amp; undeniable</em> self-evident.</p>`

### III. 空元素
**一个空元素（empty element）**可能是 HTML，SVG，或者 MathML 里的一个不可能存在子节点（例如内嵌的元素或者元素内的文本）的element。
HTML，SVG 和 MathML 的规范都详细定义了每个元素能包含的具体内容（define very precisely what each element can contain）。许多组合是没有任何语义含义的，比如一个 `<audio>` 元素嵌套在一个 `<hr>` 元素里。
在 HTML 中，通常在一个空元素上使用一个闭标签是无效的。例如， `<input type="text"></input>` 的闭标签是无效的 HTML。
在 HTML 中有以下这些空元素：
`<area>`
`<base>`
`<br>`
`<col>`
`<colgroup>` when the span is present
`<command>`
`<embed>`
`<hr>`
`<img>`
`<input>`
`<keygen>`
`<link>`
`<meta>`
`<param>`
`<source>`
`<track>`
`<wbr>`
**在极少数情况下，空元素被错误地称为“无效元素”(void elements)。**
<font color=gray>有始无终的诸位，不加闭标签</font>

### IV.可替换元素
CSS 里，可替换元素（replaced element）的展现不是由CSS来控制的。这些元素是一类 外观渲染独立于CSS的 外部对象。 典型的可替换元素有 `<img>`、 `<object>`、 `<video>` 和 表单元素，如`<textarea>`、 `<input>` 。 某些元素只在一些特殊情况下表现为可替换元素，例如 `<audio>` 和 `<canvas>` 。 通过 CSS content 属性来插入的对象 被称作 匿名可替换元素（anonymous replaced elements）。

**自己决定自己宽高的元素**

CSS在某些情况下会对可替换元素做特殊处理，比如计算外边距和一些auto值。

需要注意的是，一部分（并非全部）可替换元素，本身具有尺寸和基线（baseline），会被像vertical-align之类的一些 CSS 属性用到。

### V.标签的属性
**HTML标签没有块级元素和内联元素的区别，仅仅仅仅仅仅在CSS里有这种区别**
`<div>`是块级元素？？？naive！
`<style>
  div{
    display: inline;
 }
</style>`
你曾经是个块级元素(默认)，但看看你现在的样子。
<br>
**HTML只做一件事情：定义他是什么，而他长什么样子和HTML没关系。**~~这种问题请交给CSS~~