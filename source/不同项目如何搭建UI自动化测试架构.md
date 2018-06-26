---
title: 不同项目搭建UI自动化测试架构的痛点
date: 2017-11-27 13:15:19
tags: 测试
---
	
连续两个不同项目的自动化测试选择，每个项目也应都有适合自己项目的敏捷实践，发现项目存在的问题，持续改进才是最佳实践。
	
## 背景介绍
	
团队中自动化测试的优点和必要性此时就不再赘述，回归测试
		
## 测试用例管理

## 测试数据管理
csv
yml
js
## 测试运行
框架选择：
Nightwatch是一套新近问世的基于Node.js的验收测试框架，使用Selenium WebDriver API以将Web应用测试自动化。它提供了简单的语法，支持使用JavaScript和CSS选择器，来编写运行在Selenium服务器上的端到端测试。
自定义断言
易于扩展
Typescript

Protractor:使用Jasmine测试框架测试接口,针对AngularJS的应用程序
针对AngularJS中的Element不需要做特殊的处理，普通HTML元素也同样支持
智能等待，不需要为页面中的加载和同步显示做特殊的等待时间处理
1,不需要基于id，css选择器，xpath等查询元素，你可以基于绑定，模型，迭代器等等进行测试。

2,避免回调地狱。对比下面的代码就知道了。

复制代码
//没有protractor
driver.getTitle().then(function(title){
    expect(title).toBe('Baidu');
});

//使用protractor
expect(browser.getTitle()).toEqual('Baidu');
复制代码

protractor 
cucumber
nightwatch framework 
mocha test runner


Page Object

配置文件

## 测试报告

## 测试框架

## 驱动层 Selenium

## 丢掉UI自动化测试
SEO标签，组件测试，SEO redirection

## 视觉测试
speedcurve
spectre 


