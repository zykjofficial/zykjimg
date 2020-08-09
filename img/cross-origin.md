```
title: 解决前端跨域问题(Cross-Origin Read Blocking (CORB) blocked cross-origin response)
description: 折腾了一天的跨域问题、终于得到了答案
tags:
  - 前端
  - 后端
  - 跨域
categories: 
  - Web教程
  - 跨域
keywords: 跨域
comments: false
cover: 'https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/cross-origin-cover.png'
top_img: 'https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/cross-origin-cover.png'
toc: true
toc_number: true
copyright: true
```

# 前提

本来像写一个请求B站API用户粉丝数的函数、结果遇到了跨域的问题

![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200530210036.png)

然而通过设置了`dataType: "jsonp"`又遇到了这个问题

![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200530210253.png)

同源策略，它是由Netscape提出的一个著名的安全策略。现在所有支持JavaScript 的浏览器都会使用这个策略。所谓同源是指，域名，协议，端口相同。当一个浏览器的两个tab页中分别打开来 百度和谷歌的页面。当浏览器的百度tab页执行一个脚本的时候会检查这个脚本是属于哪个页面的，即检查是否同源，只有和百度同源的脚本才会被执行。如果非同源，那么在请求数据时，浏览器会在控制台中报一个异常，提示拒绝访问。通常这个异常以上面的形式存在着。

折腾了一天的跨域问题、终于得到了答案。。。

# 跨域

## 什么是跨域

{% note info %}

跨域，是指浏览器不能执行其他网站的脚本。它是由浏览器的同源策略造成的，是浏览器对JavaScript实施的安全限制。

同源策略限制了一下行为：

- Cookie、LocalStorage 和 IndexDB 无法读取
- DOM 和 JS 对象无法获取
- Ajax请求发送不出去

{% endnote %}

当一个请求url的协议、域名、端口三者之间任意一个与当前页面url不同即为跨域

| 当前页面url               | 被请求页面url                   | 是否跨域 | 原因                           |
| ------------------------- | ------------------------------- | -------- | ------------------------------ |
| http://www.test.com/      | http://www.test.com/index.html  | 否       | 同源（协议、域名、端口号相同） |
| http://www.test.com/      | https://www.test.com/index.html | 跨域     | 协议不同（http/https）         |
| http://www.test.com/      | http://www.baidu.com/           | 跨域     | 主域名不同（test/baidu）       |
| http://www.test.com/      | http://blog.test.com/           | 跨域     | 子域名不同（www/blog）         |
| http://www.test.com:8080/ | http://www.test.com:7001/       | 跨域     | 端口号不同（8080/7001）        |



# Ajax接口数据类型		

## json格式

```json
{
    "message":"获取成功",
    "state":"1",
    "result":{"name":"zykj","id":1,"description":"zykjofficial"}
}
```

## jsonp格式：

```jsonp
callback({
	"message":"获取成功",
    "state":"1",
    "result":{"name":"zykj","id":1,"description":"zykjofficial"}
})
```

我们可以看到，在url中callback传到后台的参数是什么callback就是什么，jsonp比json外面有多了一层，callback()。这样就知道怎么处理它了。于是修改后台代码。

Jsonp(JSON with Padding) 是 json 的一种"使用模式"，可以让网页从别的域名（网站）那获取资料，即跨域读取数据。注意：Jsonp只支持get请求。

## 前端代码

```javascript
 setTimeout(() => {
     $.ajax({
         url: "https://api.bilibili.com/x/space/acc/info?mid=241230332",
         type: "get",
         dataType: "jsonp",
         jsonpCallback:"jsonp",
         jsonp:"json",
         success: function (data) {
             console.log(data);
         },
         error: function () {
             console.log("请求错误");
         }

     })
}, 1000)
```

## 后端代码

```java
@RequestMapping("/userinfo/{uid}")
public String getUserInfo(@PathVariable String uid){
        RestTemplate template = new RestTemplate();
        Object forObject = template.getForObject("https://api.bilibili.com/x/space/acc/info?mid="+uid, Object.class);
        return "jsonp("+JSON.toJSONString(forObject)+")";
}
```

自己的理解就是后台请求B站API返回的数据转换成JSON数据、套入`jsonp()`并且返回给请求者、相当于自己把数据封装了一下。

![](https://cdn.jsdelivr.net/gh/zykjofficial/zykjimg/img/20200530211708.png)

这样就可以请求到了。

