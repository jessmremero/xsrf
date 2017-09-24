# xsrf
cross-site request forgery   跨站请求伪造
是一种挟制用户已登录web应用程序执行非本意的操作，利用的是网站对用户网页浏览器的信任
要点：
1、已登录的web应用
2、伪造请求（get post）
示例：
 addfriend.onclick = function(){
        $.get('./addfriend.json?userId=jack)
    }
标准文件请求好友如上，伪造请求如下：
&lt;img src="http://192.168.1.113:8860/addfriend.json?userId=daliwan" alt=""&gt;
这样你在访问图片时，实际上就是添加了好友（<!--img的src等于一个API的地址-->）
组织方法：利用cookie
原理：
1、cookie只要域名、端口号一致就都会有
2、伪造方是读不到cookie的值的
所以利用上面的这一点，在请求时同时带上cookie的值，如：
 addfriend.onclick = function(){
        $.get('./addfriend.json?userId=jack&xsrfietoken=${user}')
    }
