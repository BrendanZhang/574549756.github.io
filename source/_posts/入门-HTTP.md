---
title: '入门-HTTP'
date: 2018-03-19 20:11:03
tags: HTTP
categories: HTTP
---
## 1.何为HTTP（HyperText Transfer Protocol）
I. 是一种用于分布式、协作式和超媒体信息系统的应用层协议。HTTP是万维网的数据通信的基础。
II.HTTP的发展是由蒂姆·伯纳斯-李(Sir Timothy John Berners-Lee)于1989年在欧洲核子研究组织（CERN）所发起。
## 2.什么？上面太多不想看？好吧：
 **a.HTTP**
 是一种规定客户端(浏览器)如何发出请求，服务器如何响应请求的协议
 **b.服务器端口**
 
 |端口|用途|
 |:----:|:----:|
 |21|FTP服务|
 |443|HTTPS服务（提供加密和安全端口传输）|
 |1080|代理服务器端口（SS的时候它是不是很眼熟？）|
 |3306|MySQL的默认端口|
 |80|HTTP服务的默认端口|
 
 **c.URI（Uniform Resource Identifier）**
   统一资源标识符：用于标识某一互联网资源名称的字符串。（包括下面两位）
 **d.URL（Uniform Resource Locator）**
   统一资源定位符（就是我们所说的网址）
 **e.URN（Uniform Resource Name）**
   统一资源名称（可以把它理解成名字）
 **f.DNS（Domain Name System）**
   域名系统：输入域名;输出IP。（输入baidu.com，电信~~运营商~~告诉你IP）

---
## 3.请求与响应
<font color=gray size=2>前言：环境Deepin15.5（debian）
终端运行`sudo apt-get install curl`安装curl命令（已安装请忽略前言）</font>

Curl命令：利用URL语法在命令行方式下工作的开源文件传输工具。
`curl xxx.com`=读取xxx.com网页信息

|参数|全称|作用|
|:---:|:---:|:---:|
|-s|--silent|静默模式（不显示进度和错误）|
|-S|--show-error|显示错误|
|-h|--help|帮助|
|-H|--header|自定义头部信息传递给服务器|
|-x|--proxy|在指定端口上使用HTTP代理（后面跟host）|
|-X|--request|后面跟动作指定命令|
|-d|--data|HTTP POST方式传输数据 `--data 'data=xxx'`|
|-D|--dump-header <文件名>|把header信息写入该文件|
|-v|--verbose|显示更多信息|
|-V|--version|显示版本信息|
|-I|--head|仅显示请求头部信息|

突出一个大小写很重要


#### I.请求
  **a.在终端运行**
  `curl -s -v -H "Protoss: Oracle" -- "https://www.baidu.com"`
  **b.得到Get请求**
	`> GET / HTTP/1.1`
	`> Host: www.baidu.com`
	`> User-Agent: curl/7.59.0`
	`> Accept: */*`
	`> Protoss: Oracle`
	`> `
  **c.那么如何使用POST请求？**
    `curl -X POST -s -v -H "Protoss: Oracle" -- "https://www.baidu.com"`
  **d.得到POST请求内容**
	`> POST / HTTP/1.1`
	`> Host: www.baidu.com`
	`> User-Agent: curl/7.59.0`
	`> Accept: */*`
	`> Protoss: Oracle`
	`> `
  **e.总结请求格式**
    `1 动词 路径 协议/版本`
    `2 Key1: value1`
    `2 Key2: value2`
    `2 Key3: value3`
    `2 Content-Type: application/x-www-form-urlencoded`
    `2 Host: www.baidu.com`
    `2 User-Agent: curl/7.54.0`
    `3 （第三部分永远都是一个回车,表达了请求头的结束和请求正文的开始）`
    `4 要上传的数据`
<font color=gray size=2>1.请求最多包含**四**部分，最少包含**三**部分
2.第**一**部分中动词有：**GET POST PUT PATCH DELETE** HEAD OPTIONS 等
3.路径包括「查询参数」，但不包括「锚点」，没写路径的话，默认为/
4.第**二**部分中Content-Type标注了第**四**部分的格式</font>

#### II.响应
<font color=gray size=2>前言：Get和Post的响应实例过长...请参照请求代码自行尝试。</font>

  **a.响应格式**
	`1 协议/版本号 状态码 状态解释`
	`2 Key1: value1`
	`2 Key2: value2`
	`2 Content-Length: 17931`
	`2 Content-Type: text/html`
	`3`
	`4 要下载的内容`
    注：<font color=gray size=2>第二部分中的Content-Type 标注了第 4 部分的格式且遵循MIME(多用途互联网邮件扩展)</font>
  **b.HTTP状态码**
  浏览器给服务器发请求有格式，服务器发现问题返回给浏览器用状态码呈现。
    
|状态码|意义|
|:----:|:----:|
|1xx|**不常用**|
|2xx|**表示成功**|
|201|**Created**请求已经被实现，而且有一个新的资源已经依据请求的需要而创建，且其URI已经随Location头信息返回。|
|202|**Accepted**服务器已接受请求，但尚未处理。最终该请求可能会也可能不会被执行，并且可能在处理发生时被禁止。|
|203|**Non-Authoritative Information**服务器是一个转换代理服务器（transforming proxy，例如网络加速器），以200 OK状态码为起源，但回应了原始响应的修改版本。|
|204|**No Content**服务器成功处理了请求，没有返回任何内容。|
|205|**Reset Content**服务器成功处理了请求，但没有返回任何内容。与204响应不同，此响应要求请求者重置文档视图。|
|3xx|**溜了呀，这没你要的**|
|301|**Moved Permanently**被请求的资源已永久移动到新位置，并且将来任何对此资源的引用都应该使用本响应返回的若干个URI之一。|
|302|**Found**要求客户端执行临时重定向（原始描述短语为“Moved Temporarily”）。|
|303|**See Other**对应当前请求的响应可以在另一个URI上被找到，当响应于POST（或PUT / DELETE）接收到响应时，客户端应该假定服务器已经收到数据，并且应该使用单独的GET消息发出重定向。|
|305|**Use Proxy**被请求的资源必须通过指定的代理才能被访问。|
|4xx|**你（客户端）背锅**|
|403|**Forbidden**服务器已经理解请求，但是拒绝执行它。|
|404|**Not Found**请求失败，请求所希望得到的资源未被在服务器上发现，但允许用户的后续请求。|
|5xx|**我（服务器）背锅**|
|503|**Service Unavailable**由于临时的服务器维护或者过载，服务器当前无法处理请求。|

## 4.如何使用Google Chrome发送请求与查看响应
#### I.发送请求
  a.F12打开开发者工具点击Network选项卡
  b.地址栏键入网址打开
  c.点击查看request，点击**View source**可以查看请求的前三部分
  d.如果有第四部分请求，则可以在 FormData 或 Payload 里面可以看到。（右键表头标签打开Method标签可查看Post Or Get）
#### II.查看响应
  a.F12打开开发者工具点击Network选项卡
  b.地址栏键入网址打开
  c.选中第一个响应
  d.查看Response Headers，点击**view source**可以查看响应的前两部分
  e.查看Response或Preview，可以查看响应的第四部分