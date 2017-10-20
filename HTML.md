# 1.常见浏览器及其内核

## 1.1 浏览器内核

浏览器内核又可以分成两部分：渲染引擎(Rendering Engine)和JavaScript引擎

**渲染引擎**：它负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入 CSS 等），以及计算网页的显示方式，然后输出到显示设备上

**JavaScript引擎**：负责解析并执行 JavaScript 语言来实现网页的动态效果

## 1.2 主流浏览器及其内核分类

**Trident**：IE内核

**Gecko**：FireFox内核

**Presto**：Opera原内核(现为Blink)

**Webkit**：Safari、Chrome内核(现在Chrome是Blink内核，是Webkit的分支)

**EdgeHTML**：Edge浏览器内核

> 浏览器的内核不同，他们工作原理、解析也就不同，显示就会有差别

# 2.Web标准

## 2.1 Web标准的概念

Web标准不是某一个标准，而是由W3C和其他标准化组织制定的一系列标准的集合。主要包括结构（Structure）、表现（Presentation）和行为（Behavior）三个方面

1. **结构标准**：结构用于对网页元素进行整理和分类，主要包括XML和XHTML两个部分

2. **样式标准**：表现用于设置网页元素的版式、颜色、大小等外观样式，主要指的是CSS

3. **行为标准**：行为是指网页模型的定义及交互的编写，主要包括DOM和ECMAScript两个部分

> **主要体现在**：HTML标签闭合、标签小写、不乱嵌套、页面结构编写符合语义化、使用外链 css 和 js 脚本、结构行为表现的分离等

## 2.2 Web标准的好处

1. 让Web的发展前景更广阔
2. 内容能被更广泛的设备访问
3. 更容易被搜寻引擎搜索
4. 降低网站流量费用
5. 使网站更易于维护
6. 提高页面浏览速度

# 3.文档类型<!DOCTYPE>

## 3.1 定义

<!DOCTYPE> 标签位于文档的最前面，用于向浏览器说明当前文档使用哪种 HTML 或 XHTML 标准规范，必需在开头处使用

<!DOCTYPE>标签为所有的XHTML文档指定XHTML版本和类型，只有这样浏览器才能将该网页作为有效的XHTML文档，并按指定的文档类型进行解析

## 3.2 HTML5的DOCTYPE

HTML5只需要写 <!DOCTYPE HTML>即可，因为HTML5 不基于 SGML(标准通用标记语言)，因此不需要对 DTD 进行引用，但是需要 DOCTYPE 来规范浏览器的行为（让浏览器按照它们应该的方式来运行）

# 4.字符集

GB2312 简单中文 包括6763个汉字

BIG5 繁体中文 港澳台等用

GBK包含全部中文字符 是GB2312的扩展，加入对繁体字的支持，兼容GB2312

UTF-8则包含全世界所有国家需要用到的字符

# 5.HTML骨架结构(以HTML5为例)

~~~html
<!DOCTYPE html>
<!-- 定义DOCTYPE文档类型 -->
<html lang="zh">
<!-- lang属性规定元素内容的语言代码 -->

<head>
    <!-- 定义文档的头部，它是所有头部元素的容器。<head> 中的元素可以引用脚本、指示浏览器在哪里找到样式表、提供元信息等等 -->
    <meta charset="UTF-8"><!-- 定义网页字符集信息，charset属性值是当前网页字符集编码 -->
    <title>页面标题</title><!-- 定义页面的标题 -->
</head>

<body>
<!-- 网页的主体部分 -->
</body>

</html>
~~~

# 6.HTML常用标签

## 6.1 常用的语义化标签

1. 标题标签
~~~html
<h1>、<h2>、<h3>、<h4>、<h5>和<h6>
~~~

2. 段落标签
~~~html
<p>  文本内容  </p>
~~~

3. 文本格式化标签
~~~html
<strong>加粗强调 <em>斜体强调 <del>删除 <ins>插入
~~~

4. 列表
~~~html
<ul>无序列表 <ol>有序列表 以上二者中的每一项都是<li>
<dl>自定义列表 <dt>是每一项的标题 <dd>是每一项的内容
~~~

## 6.2 常用的功能性标签

1. 图像标签
~~~html
<img src="图片路径" alt="图像不能显示时的文本" title="鼠标悬停时的文本">
~~~

2. 链接标签
~~~html
<a href="链接目标的url地址" target="链接页面的打开方式">文本或图像</a>
target属性取值有_self和_blank两种，其中_self为默认值，_blank为在新窗口中打开方式
~~~

3. 表格标签
~~~html
<table><!-- 定义表格 -->
    <caption></caption><!-- 表格标题 -->
    <thead><!-- 表格头部 -->
        <tr><!-- 表格一行 -->
            <th></th><!-- 表头项 -->
            <th></th>
            <th></th>
        </tr>
    </thead>
    <tbody><!-- 表格主体 -->
        <tr>
            <td></td><!-- 表格的一个单元格 -->
            <td></td>
        </tr>
    </tbody>
</table>
表格中<caption><thead><tbody>一般都可以忽略
可以使用colspan属性跨列合并 rowspan属性跨行合并
~~~

## 6.3 表单

1. input控件
~~~html
<input type="text">单行文本输入框
<input type="password">密码输入框
<input type="radio">单选框
<input type="checkbox">复选框
<input type="button">按钮
<input type="submit">提交按钮
<input type="reset">重置按钮
<input type="file">文件域
<!-- 
    name属性定义控件名称
    value属性定义控件值
    checked用于设定单选和复选框被默认选中的项
    maxlength设置输入字符的最大个数
-->
~~~

2. textarea控件
~~~html
<textarea cols="每行中的字符数" rows="显示的行数">
       文本内容
</textarea>
~~~

3. 下拉菜单
~~~html
<select>
        <option>选项1</option>
        <option>选项2</option>
        <option>选项3</option>
       ...
</select>
<!-- 
    1.<select></select>中至少应包含一对<option></option>。
    2.在option 中定义selected =" selected "时，当前项即为默认选中项。
 -->
~~~

4. 普通按钮button
~~~html
<button>按钮文字</button>
~~~

5. 表单域
~~~html
<form action="url地址" method="提交方式" name="表单名称">
       各种表单控件
</form>
<!-- 
    action 在表单收集到信息后，需要将信息传递给服务器进行处理，action属性用于指定接收并处理表单数据的服务器程序的url地址。
    method 用于设置表单数据的提交方式，其取值为get或post
    name 用于指定表单的名称，以区分同一个页面中的多个表单
 -->
~~~

# 7.HTML语义化的优势

（1）HTML 语义化让页面的内容结构化，结构更清晰，便于对浏览器、搜索引擎解析；

（2）即使在没有样式 CSS 的情况下也能以一种文档格式显示，并且是容易阅读的；

（3）搜索引擎的爬虫也依赖于 HTML 标记来确定上下文和各个关键字的权重，有利于 SEO；

（4）使阅读源代码的人更容易将网站分块，便于阅读、维护和理解。

# 8.网站优化三大标签

## 8.1 网页title标题

title具有不可替代性，是我们的内页第一个重要标签，是搜索引擎了解网页的入口，和对网页主题归属的最佳判断点

建议：

首页标题：网站名（产品名）- 网站的介绍

## 8.2 关键字Keywords

Keywords是页面关键词，是搜索引擎关注点之一。Keywords应该限制在6～8个关键词。 用英文逗号 关键词1,关键词2

```html
<meta name="Keywords" content="网上购物,网上商城,手机,笔记本,电脑,MP3,CD,VCD,DV,相机,数码,配件,手表,存储卡,京东" />

<meta name="keywords" content="小米,小米5s,红米Note4,小米MIX,小米商城" />
```

## 8.3 网站说明Description

简要说明我们网站的主要做什么的

Description作为网站的总体业务和主题概括，多采用“我们是…”“我们提供…”“×××网作为…”“电话：010…”之类语句

```html
<meta name="description" content="京东JD.COM-专业的综合网上购物商城,销售家电、数码通讯、电脑、家居百货、服装服饰、母婴、图书、食品等数万个品牌优质商品.便捷、诚信的服务，为您提供愉悦的网上购物体验!" />
```

1. 描述中出现关键词，与正文内容相关，这部分内容是给人看的，所以要写的很详细，让人感兴趣， 吸引用户点击。
2. 同样遵循简短原则，字符数含空格在内不要超过 120 个汉字。
3. 补充在 title 和 keywords 中未能充分表述的说明。