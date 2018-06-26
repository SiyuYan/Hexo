---
title: 安全
categories: 安全

---
# 客户端安全
## 浏览器安全
### 基础概念
* **同源策略**(Same Origin Policy)-->浏览器最基本的安全功能。
 * 限制来自不同源的document和脚本，host(Domains/IP), protocols and ports
* sandbox  --资源隔离类模块
 * ‘挂马’：**利用浏览器漏洞执行任意代码的攻击方式-**->多进程架构 
chrome（浏览器进程、渲染进程、插件进程、扩展进程）  sandbox隔离，网页代码通过IPC channel和浏览器内核通信，和OS通信。每个Tab是一个进程
* 恶意网址拦截，恶意网址黑名单：挂马网站（恶意脚本，运行后植入木马），钓鱼网站（模仿知名网站相似页面欺骗用户）
 * EV SSL证书（Extended Validation SSL Certificate）
* XSS -->XSS Filter(微软 IE)
-->CSP(Content Security Policy -->Firefox):服务器端返回一个http头，在其中描述页面应该遵守的安全策略，xss在没有第三方插件帮助下无法控制HTTP头。  
		
		#Summary: 同源策略，恶意网址检测，插件安全
	
### 注入

**注入漏洞**：应⽤程序忽略了对输⼊数据的检查，这些夹杂了恶意代码的数据被应⽤程序误认为是正常的指令⽽运⾏，从⽽使系统受到攻击。

恶意输⼊数据被当做代码执⾏。

测试SQL注⼊漏洞的技巧：

* 基于报错的测试
* 基于“真/假”的测试
* 延迟测试
SQLMAP
OWASP ZAP
BURTP