# js DOM BOM

- js通过访问BOM(DOM在各自浏览器上的实现)来访问、控制、修改客户端(浏览器)
- DOM(文档对象模型)是用于HTML和XML文档的API(应用程序编程接口),DOM就是接口对象，比如JDOM(java dom),XML DOM  
- BOM:浏览器对象， 是 各个浏览器厂商根据 DOM在各自浏览器上的实现。window是BOM而非js对象
  >*DOM描述了处理网页内容的方法和接口，BOM描述了与浏览器进行交互的方法和接口。*
- DOM举例，HTML DOM,
  1. 定义文档结构--节点对象树,  
  ![对象树](../picture/html_dom.jpg)

## js引用和书写

- `<script type="text/javascript" async src="example.js"></script>`加载外部js,页面会暂停处理，其中对于html来说：先加载`head`所以如果js太多会空白，放body后。加上type表示使用的是javascript可以换java等
- 可以加上async来进行立即下载，延迟执行，可以放`head`中了，(异步)如上确保两者之间互不依赖，
- "use strict";在标签内加上这个会严格模式，报错一些问题，在js中，如果某个变量没有var声明，会自动移到上一层作用域中找声明语句，有就是这个。没有就套娃到全局。

## 用法

1. typeof message用于查看是那种类型。var me=Boolean(message)这样转换可以判断字符串是否为空，因为字符串强制转换，""和（空串）都会是false,可以测数值0。可以直接if (me)。如果message='2'是对象的话很可能就改变了程序流程。
2. var num1 = parseInt("AF",16);解析指定数值类型。16不指定，就自动解析
