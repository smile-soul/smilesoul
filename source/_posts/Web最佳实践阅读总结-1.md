---
title: Web最佳实践阅读总结(1)
tags: JavaScript
categories: 编程语言
date: 2017-10-05 23:11:42
---
![](https://badge.juejin.im/entry/59d9c9dcf265da06456da777/likes.svg?style=flat-square)
### 介绍
----
最近开始刷一些书和题,此系列是介绍在读`Web最佳实践`的一些收获和体会。
![](http://ou42j47mq.bkt.clouddn.com/2017-10-05-webbest.jpg)
---
##### web前端发展现状
 * 存在问题：
    * 代码组织混乱
    * 代码格式的问题突出
    * 页面布局随意
    * 网站整体性能差，没有意识到应用诸如缓存，动态加载，脚本压缩，图片压缩等提高性能技术
 * 推荐做法：
    * 压缩样式表和脚本文件
    * 减少HTTP请求次数
    * 简洁和符合W3C标准的HTML和CSS代码能减少浏览器解析的时间，加快渲染过程
    * 页面请求数量越少，相对页面的加载速度更快
    * 在JS代码中选择性能更好的实现方案，如延迟加载，动态加载等技术;
 * 延迟加载
    ```
    <script type=”text/javascript” src=”" id=”my”></script> 
    <script type=”text/javascript”> 
    setTimeout(“document.getElementById(‘my').src='include/php100.php'; “,3000);//延时3秒 
    </script> 

    ```
 * 最后加载
    * 引入外部js脚本文件时，如果放入html的head中,则页面加载前该js脚本就会被加载入页面，而放入body中，则会按照页面从上倒下的加载顺序来运行javascript的代码，所以可以把js外部引入的文件放到页面底部，来让js最后引入，从而加快页面加载速度
 * 动态加载
    ```
    
        <scrīpt src='' id="s1"></scrīpt> 
        <scrīpt language="javascrīpt"> 
        s1.src="test.js" 
        </scrīpt> 
    ```
##### 前端代码重构
 * 删除无用代码，精简代码（不起作用的CSS样式和废弃的JavaScript函数）
 * 前端代码规范化，把CSS代码放到独立的文件中，在JS定义局部变量，把部分全局变量改变成局部变量
 * 前端代码模块化，引入面向对象的思想来重构JavaScript代码，进一步明确公有接口和私有接口
 * 提高页面性能：
    * 将部分不影响首页展示的JS文件延迟到页面的加载后加载
    * 删除页面中初始隐藏的区域，改为通过JS按需动态生成
    * 页面中的部分图片延迟加载
    * 调整CSS和JS文件引用顺序，即CSS在前，JS在后
    * 给静态文件设置缓存，使用CSS Sprite，合并背景图
    * 合并和压缩发布后的CSS和JS代码模块
 * 前端重构最佳实践
    * 重构前一定要预测风险，最好先完善自动化测试代码
    * 重构的目的和范围要明确，提高代码的可维护性，可读性和性能
    * 最好先易后难，循序渐进。先修改诸如命名，格式等不涉及具体逻辑的内容
    * 重构过程中要持续测试，在多个浏览器测试，确保重构的部分功能正确。切记大量重构后再进行测试，因为大量重构后基本很难记得重构的逻辑，也可能遗漏部分测试用例
    * 性能提升，先进行检测网站的整体性能并量化，找出性能瓶颈。重构过程中要持续监控性能，并进行对比
##### 前端框架的使用
 * 项目需求
    * 调查项目是否需要AJAX操作
    * 是否需要模块化
    * 数据传输格式JSON或者XML
    * 需要支持的浏览器
    * 移动还是普通网站
    * 需要的UI模块（模态窗口，滑块控件，进度条，提示框，分割框，幻灯显示，自动填充）
 * 项目的特点
 * 框架的特点
##### 代码质量
 * 编写高质量，标准的HTML（标准校验工具，ESLint, Flow, JSDoc, ts）
 * 明确浏览器支持范围
    * Chrome和Safari  IE Tester（IE兼容测试工具
 * 避免浏览器兼容性的问题
    * 先考虑更改方案，使用没有兼容问题的代码
    * 考虑如何兼容的问题
    * 兼容IE，使用IE特有的条件表达式(hack)
    * 让兼容的代码独立，提高代码的可维护性
 * HTML5新特性
    * 新标签的兼容，CSS3的兼容，新增的API（使用html5shiv框架）
    * CSS3本身不支持，会直接忽略
    * 新增加的接口的使用，必须添加条件判断（Modernizr）
    * 多看Can I use
##### web性能分析
 * YSlow，pagespeed
    * 基于不同的规则评定网站整体性能评分
    * 给出提高网页性能的建议
    * 统计页面加载的组件
    * 页面的统计信息视图
    * 相关性能分析工具集：Smush.it
 * Chrome开发工具
    * Network中可以查看各资源请求和下载所用的时间
    * Timeline可以查看网页渲染和交互过程中个步骤所花费的时间，从资源到JS的解析执行，样式的应用和绘制
    * Profiles中可以查看网页的CPU及内存占有情况报告
    * Audits中提供了各种资源和配置优化的建议和未使用CSS规则的列表
 * 加快代码和资源文件传输的方式
    * CDN分发
    * 缓存(meta)
    * 压缩代码和资源文件（最优）
    * Gzip算法（压缩，header可以检查是否开启）
    * JS压缩（UglifyJS压缩和优化，YUI Compressor 仅压缩，Closure Compiler压缩和优化）
    * CSS(CSS Compressor,YUI Compressor)
    * HTML(HtmlCompressor使用时仔细调查和测试，避免压缩工具和破坏)
    * 图片资源压缩（TinyPNG，JPEGmini，ImageOptim)

---
* Airbnb规范: https://github.com/airbnb/javascript
* Eslint规范: https://eslint.org/docs/rules/
* Beachmark.js性能测试: https://benchmarkjs.com/docs#toc

