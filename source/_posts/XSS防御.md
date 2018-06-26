---
title: XSS
categories: 安全

---

# XSS		
* XSS(Cross Site Script)黑客通过HTML注入篡改了网页，插入了恶意的脚本，从而在用户浏览网页时，控制用户浏览器的一种攻击。
 * 反射型：非持久性型，点击后攻击成功，**一般会修改正常URL，一般要求攻击者将XSS URL发送给用户点击**
 因为这种攻击方式的注入代码是从目标服务器通过错误信息、搜索结果等等方式“反射”回来的。而称为非持久型XSS，则是因为这种攻击方式具有一次性。攻击者通过电子邮件等方式将包含注入脚本的恶意链接发送给受害者，当受害者点击该链接时，注入脚本被传输到目标服务器上，然后服务器将注入脚本“反射”到受害者的浏览器上，从而在该浏览器上执行了这段脚本。
 * 存储型：会把用户输入的数据存储在**服务器端,在用户访问正常的URL会自动触发。**
 攻击脚本将被永久地存放在目标服务器的数据库和文件中。这种攻击多见于论坛，攻击者在发帖的过程中，将恶意脚本连同正常信息一起注入到帖子的内容之中。随着帖子被论坛服务器存储下来，恶意脚本也永久地被存放在论坛服务器的后端存储器中。当其它用户浏览这个被注入了恶意脚本的帖子的时候，恶意脚本则会在他们的浏览器中得到执行，从而受到了攻击。
 * DOM Based XSS(也是反射型) 通过修改页面的DOM节点
 
 XSS危害：跨站脚本漏洞带来的危害⾮常多，最常⻅的是被⽤来**盗取⽤户账户信息**，**进⾏钓⻥欺诈，网⻚挂⻢**，更甚⾄可以被⽤来刷流量、实施DDoS攻击等。

* XSS Payload（js代码）:

1. 窃取cookie: 通过读取浏览器的Cookie对象，把document.cookie对象作为参数发送到远程服务器，登录凭证。如果cookie中没有绑定客户端信息(如和IP绑定)，窃取cookie就可以直接登录
解决办法：**HttpOnly** 
2. 模拟GET，POST请求操作用户的浏览器
3. XSS钓鱼：有和用户交互（输入验证码、Old password）-->读取页面内容，将验证码发送到远程服务器；用JS在当前页面划出一个伪造的登陆框，发送到黑客服务器上
4. 识别用户浏览器，操作系统-->浏览器内存攻击，植入木马。方法：1，userAgent 2,根据不同浏览器实现的独特功能
5. 识别用户安装的软件：判断ActiveX控件的classid是否存在来判断是否安装某软件。（Flash的ActionScript中读取system.capabilities对象后，将结果通过ExternallIterface传给页面的JS）
6. CSS History Hack 通过CSS，来发现一个用户曾经访问过的网站，style的visited属性，访问过后颜色变得不同
7. 获取用户真实本地IP:借助第三方软件， Attack API java..

* XSS 攻击平台	
 * Attack API
 * BeFF
 * XSS-Proxy：嵌套iframe方式实时地远程控制被XSS攻击的浏览器
 

蠕虫：蠕虫病毒是一种能够利用系统漏洞通过网络进行自我传播的恶意程序。它不需要附着在其他程序上，而是独立存在的。当形成规模、传播速度过快时会极大地消耗网络资源导致大面积网络拥塞甚至瘫痪。是一种能够自我复制的计算机程序。
8. XSS Worm ：**扩大传播**。用户之间发生交互行为的页面，如果存在存储型XSS，容易发生攻击（因为需要传播）

不干扰用户使用，窃取用户数据最可怕。

## XSS构造技巧

* 利用字符编码 \
* 绕过长度限制：
  * 利用事件 "onclick=alert(1)
  * 把XSS Payload写到别处，再通过尖端带马甲在这段XSS Payload。（such as:location.hash 内容不会再http包中发送，所以服务期端的Web日志中并不会记录下其内容，隐藏了意图)
  * 利用注释绕过长度限制
* 使用<base>标签：定义页面上所有使用相对路径标签hosting地址。通过远程服务器上伪造图片、链接或脚本，劫持当前页面上所有使用相对路径的标签。一定要过滤这个标签！
* windows.name：windows对象是浏览器的窗体，而并非document对象，不受同源策略的限制。windows.name=“alert(document.cookie)” ,eval(name)

          #随着技术发展，难以利用的漏洞也许以后不再是难题

## Flash XSS 
* 嵌入ActionScript脚本，实施脚本攻击
  * \<embed> 
  * \<object> 加载ActiveX控件
  * 解决办法：
      * 视频文件转成flv(静态文件)
      * 对动态脚本的Flash配置参数进行限制。
         * allowScriptAccess：定义了Flash能否和HTML进行通信：
         * allowNetworking：控制了Flash与外部网络进行通信
 * XSS漏洞：缺乏输入验证
 
          #注入Flash变量的XSS，因为问题出现在编译后的Flash文件中，一半的扫描工具或者代码审计工具难以检查。 

## 使用框架的安全性漏洞
## XSS防御 
### HTTPOnly
* XSS带来cookie劫持，窃取用户信息，模拟用户身份执行操作等。
* HTTPOnly解决XSS后的cookie劫持。 

   cookie使用过程：
   * 浏览器发送请求，没有cookie；
   * 服务器返回时候发送set-cookie头，向客户端浏览器写入cookie；
   * 在该cookie到期前，浏览器访问该域的所有页面，都将发送cookie
   
            # 设置httponly后javascript不能读取到
 然而，还有绕过httponly的攻击方法。such as aphche支持的一个header是TRACE。
   
### 输入检查
一定要在服务器端实现，前端容易绕过   
### 输出检查
* javascriptEncode,HTMLEncode 
* **在正确的地方选择用这个正确的编码方式** 
* XSS本质是HTML注入，用户的数据被当做HTML代码一部分来执行，混淆了原本的语义，产生了新的语义，View层在应用拼接变量到HTML页面时产生。

### 防御措施
* HTML标签中输出变量 eg:构造一个\<script>、\<img src='' onerror=''> -->使用HtmlEncode
* HTML属性中输出变量 eg:\<div name=“**">\<script>"alert''\</script>**<"">\</div> -->使用HtmlEncode
* 在script标签中输出  -->使用javascriptEncode
* 在事件中输出  -->使用javascriptEncode
* 在CSS中输出：尽可能禁止用户可控制的变量在style标签，HTML标签的style属性以及CSS文件中输出 -->使用OWASP ESAPI中的encodeForCSS（）函数
* 在地址中输出
  * 控制部分URL：在url的path或者search参数中输出  -->使用URLEncode
  * 控制全部URL：首先检查是否http开头（不是自动添加）确保不会出现伪协议类的XSS攻击；而后URLEncode;最后OWASP ESAPI有一个URLEncode严格实现 
### 处理富文本
* 禁止事件
* 输入检查
* 过滤标签，使用**白名单**（\<a>\<img>\<div>等），避免使用黑名单。同样方法处理属性事件
* 尽可能禁止用户自定义CSS和Style
### 防御DOM Based XSS 

 
 
 防御方法：
 * HTTPOnly（是Cookie扩展功能，使JS无法获得Cookie）
 * X-Frame-Options属于HTTP响应首部，用于控制网站内容器在其他web网站内的Frame标签内的显示问题。为了防止点击挟持。X-Frame-Options：DENY
 * X-XSS-Protection:1属于HTTP响应首部，用于控制浏览器XSS防护机制的开关。