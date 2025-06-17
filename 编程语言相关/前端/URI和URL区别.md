## **URL**

URL：（全称：Uniform Resource Locator）统一资源定位符。

它是对可以从互联网上得到的资源的位置和访问方法的一种简洁的表示，是互联网上标准资源的地址。

URL 的常见定义格式为：

`scheme://host[:port#]/path/…/[;url-params][?query-string][#anchor]`

```text
scheme //有我们很熟悉的http、https、ftp以及著名的ed2k，迅雷的thunder等。
host   //HTTP服务器的IP地址或者域名
port#  //HTTP服务器的默认端口是80，这种情况下端口号可以省略。如果使用了别的端口，必须指明，
例如tomcat的默认端口是8080  http://localhost:8080/
path   //访问资源的路径
url-params  //所带参数 
query-string    //发送给http服务器的数据
anchor //锚点定位
```

一般的URL为：

```text
URL:  http://127.0.0.1:8080/webProject/index.html 
```


## **URI**

URI：（全称：Uniform Resource Identifier）统一资源标识符，它是一个字符串**用来标示抽象或物理资源。**

Web上可用的每种资源（ HTML文档、图像、音频、视频片段、程序等）都由一个通用资源标识符（Uniform Resource Identifier, 简称”URI”）进行定位。

URI的格式也由三部分组成：

1. 访问资源的命名机制。
2. 存放资源的主机名。
3. 资源自身的名称，由路径表示。


## **联系与区别**

URI 属于 URL 更高层次的抽象，一种字符串文本标准。

就是说，URI 属于父类，而 URL 属于 URI 的子类。**URL 是 URI 的一个子集**


>URI ：Uniform Resource Identifier，统一资源标识符；
>URL：Uniform Resource Locator，统一资源定位符；
>URN：Uniform Resource Name，统一资源名称。


[http://www.baidu.com](https://link.zhihu.com/?target=http%3A//www.baidu.com)是URL.  
[http://www.baidu.com/index.html](https://link.zhihu.com/?target=http%3A//www.baidu.com/index.html) 是URL 同时也是URI。  
所以，URL 就是 URI 的 定位。

但 URI 不一定是 URL。  
因为 URI有一类子集是 URN，它是命名资源 但不指定如何定位资源。  
如： mailto 需要 加上 相应的结构参数，才能进行 统一资源定位。  
如： mailto: xxxxx@qq.com

因此，三者之间的关系是：  
URL 一定是 URI  
URN + URL 就是 URI