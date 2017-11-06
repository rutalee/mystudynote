# 服务器与Ajax

## 1.Ajax简介

Ajax是Asynchronous Javascript And XML(异步JavaScript和XML)的缩写，实际上XML已经过时，现在的公司，几乎全都在使用JSON代替XML。所以理论上讲，应该称呼为Ajaj，但这个词很难看也很难念，所以依旧将该技术成为Ajax

Ajax能在不刷新页面的情况下，让浏览器悄悄地、异步地向服务器发出HTTP请求。服务器收到请求后，传回新的格式化数据回来（通常是JSON）。浏览器解析JSON，通过DOM将新数据呈递显示，页面仅局部刷新，这样用户体验会很好

## 2.服务器与客户端

### 2.1 服务器

是提供计算服务的设备。由于服务器需要响应服务请求，并进行
处理，因此一般来说服务器应具备承担服务并且保障服务的能力

服务器和通用的计算机架构类似，但是由于需要提供高可靠的服务，因此在处理能力、稳定性、可靠性、安全性、可扩展性、可管理性等方面要求较高

按服务类型可分为：文件服务器、数据库服务器、邮件服务器、Web 服务器等

按操作系统可分为：Linux服务器、Windows服务器等

按应用软件可分为 Apache服务器、Nginx 服务器、IIS服务器、Tomcat服务器、Node服务器等

**服务器软件**是指使计算机具备提供某种服务能力的应用软件，
通过安装相应的服务软件，然后进行配置后就可以使计算具备了提供某种服务的能力。

### 2.2 客户端

具有向服务器索取服务能力的终端，一般指通用的计算机和在其上运行的浏览器、应用程序的软件

## 3.网络相关概念

### 3.1 IP地址

所谓IP地址就是给每个连接在互联网上的主机分配的一个32位地址

windows操作系统下

查看本机的IP： ipconfig 或者ipconfig -all

查看域名的IP： ping

### 3.2 域名

由于IP地址是基于数字，不方便记忆，于是便用域名来代替IP地址。域名就是方便IP的的别名，替代品

### 3.3 DNS以及查找的规则

记录了 IP 地址和域名的映射（对应）关系。

查找优先级 本机hosts文件、DNS服务器

### 3.4 端口

端口是计算机与外界通讯交流的出口，每个端口对应不同的服务

## 4.通信协议

### 4.1 常见的通信协议

1. HTTP、HTTPS 超文本传输协议   ----  默认http是80端口,https是443端口
2. FTP 文件传输协议    ---- 默认是 21 端口
3. SMTP 简单邮件传输协议  ---- 默认是 25 端口

### 4.2 HTTP协议

即超文本传输协议，网站是基于HTTP协议的。

HTTP协议是由从客户机到服务器的请求(Request)和从服务器到客户机的响应(Response)进行了约束和规范。

即HTTP协议主要由请求和响应构成。

报文格式：

请求报文格式如下：

    请求行 － 通用信息头 － 请求头 － 实体头 － 报文主体

响应报文格式如下：

    状态行 － 通用信息头 － 响应头 － 实体头 － 报文主体

### 4.3 HTTPS协议

以安全为目标的HTTP通道，简单讲是HTTP的安全版。

即HTTP下加入SSL层，HTTPS的安全基础是SSL，因此加密的详细内容就需要SSL。

SSL即安全套接层，是为网络通信提供安全及数据完整性的一种安全协议。

### 4.4 C/S 和 B/S

C/S --- 客户机和服务器模式 --- 例如QQ、迅雷

B/S --- 浏览器和服务器模式 --- 例如OA、网页版QQ、网页版263邮箱

但要注意：

    B/S是基于特定通信协议(HTTP)的C/S架构，也就是说B/S包含在C/S中，是特殊的C/S架构。

    B/S属于C/S，浏览器只是特殊的客户端，本质上开发浏览器，还是实现一个C/S系统。

## 5.原生Ajax请求

### 5.1 创建XHR对象

IE7+、Firefox、Opera、Chrome 和 Safari 都支持原生的 XHR 对象，在这些浏览器中创建 XHR 对象可以直接实例化 XMLHttpRequest 即可

```js
var xhr = new XMLHttpRequest();
```

如果是 IE6 及以下，那么我们必须还需要使用 ActiveX 对象通过 MSXML 库来实现

```js
var xhr = new ActiveXObject('Microsoft.XMLHTTP');
```

### 5.2 XHR的open方法和send方法

创建完XHR对象后，想要发送Ajax请求，必须先使用open方法确定请求的类型，请求的url地址，是同步还是异步请求

```js
xhr.open(`method`,`url`,`async`)
// method：请求的类型；GET 或 POST
// url：文件在服务器上的位置
// async：true（异步）或 false（同步）
```

#### GET 还是 POST？

与 POST 相比，GET 更简单也更快，并且在大部分情况下都能用。

然而，在以下情况中，请使用 POST 请求：

- 无法使用缓存文件（更新服务器上的文件或数据库）
- 向服务器发送大量数据（POST 没有数据量限制）
- 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠

如果需要像 HTML 表单那样 POST 数据，请使用 setRequestHeader() 来添加 HTTP 头。然后在 send() 方法中规定您希望发送的数据

```js
xhr.open('post','url',true);
xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xhr.send('name=lee&id=5');
// setRequestHeader(header,value)
// 向请求添加 HTTP 头。
// header: 规定头的名称
// value: 规定头的值
```

如果是 GET 请求，参数直接写在url中，且不需要设置请求头

### 5.3 onreadystatechange 事件

当请求被发送到服务器时，我们需要执行一些基于响应的任务。

每当 readyState 改变时，就会触发 onreadystatechange 事件。

readyState 属性存有 XMLHttpRequest 的状态信息。
下面是 XMLHttpRequest 对象的三个重要的属性：

**onreadystatechange** 存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。

**readyState** 存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。

- 0: 请求未初始化
- 1: 服务器连接已建立
- 2: 请求已接收
- 3: 请求处理中
- 4: 请求已完成，且响应已就绪

**status**
200: "OK"
404: 未找到页面

### 5.4 接收响应

如需获得来自服务器的响应，需使用 XMLHttpRequest 对象的 responseText 或 responseXML 属性

```js
xhr.responseText
xhr.responseXML
```

由于现在XML已不是数据交互时数据的主流格式，现在一般都是返回JSON格式的文本，所以只要使用responseText接收到JSON格式的文本信息，再使用JSON.parse()将其转换成对象来进行操作

### 5.5 一个完整原生Ajax请求过程的代码

```js
var xhr = new XMLHttpRequest();
xhr.open('get', 'http://localhost:16688/categories/1/shops?_page=1&_limit=10', true);
// 如果是POST请求，且要发送类似的表单数据，需要加如下请求头
// xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xhr.send();
xhr.onreadystatechange = function () {
    if (xhr.readyState == 4 && xhr.status == 200) {
        var data = xhr.responseText;
        // 后续操作
    }
}
```

## 6.同步与异步底层原理分析

### 6.1 为什么JavaScript是单线程的却能让AJAX异步发送和回调请求

JS运行在浏览器中，是单线程的，每个window一个JS线程，既然是单线程的，在某个特定的时刻只有特定的代码能够被执行，并阻塞其它的代码。而浏览器是事件驱动的（Event driven），浏览器中很多行为是异步（Asynchronized）的，会创建事件并放入执行队列中。javascript引擎是单线程处理它的任务队列，你可以理解成就是普通函数和回调函数构成的队列。当异步事件发生时，如mouse click, a timer firing, or an XMLHttpRequest completing（鼠标点击事件发生、定时器触发事件发生、XMLHttpRequest完成回调触发等），将他们放入执行队列，等待当前代码执行完成。

### 6.2 异步事件驱动

浏览器是事件驱动的（Event driven），浏览器中很多行为是异步（Asynchronized）的，例如：鼠标点击事件、窗口大小拖拉事件、定时器触发事件、XMLHttpRequest完成回调等。当一个异步事件发生的时候，它就进入事件队列。浏览器有一个内部大消息循环，Event Loop（事件循环），会轮询大的事件队列并处理事件。例如，浏览器当前正在忙于处理onclick事件，这时另外一个事件发生了（如：window onSize），这个异步事件就被放入事件队列等待处理，只有前面的处理完毕了，空闲了才会执行这个事件。setTimeout也是一样，当调用的时候，js引擎会启动定时器timer，大约xxms以后执行xxx，当定时器时间到，就把该事件放到主事件队列等待处理（浏览器不忙的时候才会真正执行）

### 6.3 浏览器不是单线程的

JS运行在浏览器中，是单线程的，每个window一个JS线程，但浏览器不是单线程的，例如Webkit或是Gecko引擎，都可能有如下线程：

- javascript引擎线程
- 界面渲染线程
- 浏览器事件触发线程
- Http请求线程 如果js是单线程的，那么谁去轮询大的Event loop事件队列？答案是浏览器会有单独的线程去处理这个队列。

### 6.4 Ajax异步请求是否真的异步

既然说JavaScript是单线程运行的，那么XMLHttpRequest在连接后是否真的异步? 其实请求确实是异步的，这请求是由浏览器新开一个线程请求（见前面的浏览器多线程）。当请求的状态变更时，如果先前已设置回调，这异步线程就产生状态变更事件放到 JavaScript引擎的事件处理队列中等待处理。当浏览器空闲的时候出队列任务被处理，JavaScript引擎始终是单线程运行回调函数。javascript引擎确实是单线程处理它的任务队列，能理解成就是普通函数和回调函数构成的队列。 总结一下，Ajax请求确实是异步的，这请求是由浏览器新开一个线程请求，事件回调的时候是放入Event loop单线程事件队列等候处理。

### 6.5 setTimeout(func, 0)为什么有时候有用

有时候加一个setTimeout(func, 0)非常有用，为什么？难道是模拟多线程吗？错！前面已经说过了，javascript是JS运行在浏览器中，是单线程的，每个window一个JS线程，既然是单线程的，setTimeout(func, 0)神奇在哪儿？那就是告诉js引擎，在0ms以后把func放到主事件队列中，等待当前的代码执行完毕再执行，注意：重点是改变了代码流程，把func的执行放到了等待当前的代码执行完毕再执行。这就是它的神奇之处了。它的用处有三个：

- 让浏览器渲染当前的变化（很多浏览器UI render和js执行是放在一个线程中，线程阻塞会导致界面无法更新渲染）
- 重新评估”script is running too long”警告
- 改变执行顺序

## 7 跨域

### 7.1 同源策略

同源策略是浏览器的一种安全策略，所谓同源指的是请求URL地址中的协议、域名和端口号都相同，只要其中之一不相同就是跨域

同源策略主要是为了保证浏览器的安全性

在同源策略下，浏览器不允许Ajax跨域获取服务器数据

### 7.2 跨域的主流解决方案

1. jsonp

2. 服务器代理

3. CORS

### 7.3 JSONP的原理

HTML中，script标签对资源的请求是可以跨域的，src属性里的url地址可以是一个跨域的地址

这样的话，动态创建script标签，然后通过它src属性发送跨域请求就可以请求到响应数据

但请求到相应的过程是异步的，我们不知道什么时候会获得数据，javascript本身又是单线程的，直接去调用相应的数据有极大几率调取不到

这时，便要求响应返回的是一个函数调用形式的字符串，函数的参数就是此次请求所需要的数据

这样我们可以在浏览器JS的全局作用域中定义一个函数，这个函数就是用来处理跨域响应数据的，函数名与响应返回的函数调用的函数名一致

由于script标签请求到的数据会将其当成JS代码解析，这样就会在响应数据返回至浏览器时发生函数调用，从而可以处理响应中的数据

>注意：ajax和jsonp其实本质上是不同的东西，ajax的核心是通过XmlHttpRequest获取非本页内容,而jsonp的核心则是动态添加```<script>```标签来调用服务器提供的js脚本，且jsonp只支持get请求