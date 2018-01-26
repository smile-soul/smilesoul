---
title: Web最佳实践阅读总结(2)
tags: JavaScript
categories: 编程语言
date: 2017-10-09 08:28:41
---
##### 代码符合标准
* 标准的页面会保证正确的渲染
* 页面容易被搜索引擎搜索，提高搜索排名(SEO)
* 提高网站的易用性
* 网页更好维护和扩展（Validator，HTML Validator 属于Firefox插件)

##### 停止使用不标准的标签和属性，简化HTML代码
* 标签没有实际意义，仅设置样式（不推荐使用）
* 不推荐使用blink，marquee
* 让HTML拥有更好的语义
* 移除不常用的HTML标签

##### 样式和结构分离
* HTML页面链接一个CSS（最优），提高加载速度
* HTML内嵌CSS（单一页面最佳，减少加载CSS样式文件的请求数目，加快加载速度
* 内联CSS样式，可以使用JS动态来统一修改，很少使用，JQ中使用其实现动画效果
* 在CSS样式文件中引用CSS文件，避免使用

##### 添加JS禁用提示信息
* 使用noscrpt，HTML4只在body中起作用，HTML5中可以出现在head中，支持HTML，不支持XHTML
* 最好使用noscript，采用渐进增强的模式，平稳降级

##### 添加必要的meta的标签
* meta的属性：name，http-equiv，content，charset
* name和content属性组合，构成名称/值对
* name中keywords，description最常用
* http-equiv和content属性结合，构成http命令
* 其中content-type，default-style，refresh已经确定，content-language，set-cookie 未正式确定
* charset设置编码

##### 常用的meta方法
* 设置IE浏览器的兼容性
* 设置页面在移动设备中的显示
* 设置IE浏览器的固定网站功能

##### HTML语义化
* 语义化使搜索引擎和第三方抓取工具更容易读懂代码
* 去掉CSS也可以保持良好的外观
* div，span尽量少使用
* 把无关的元素重HTML中删除
* 添加一些隐藏文字
* 要求：
	* 熟悉所有规范中的HTML标签，理解各标签的语义
	* 熟悉各标签上规范的属性，给HTML标签设置必要的属性
	* 样式和结构的分离
* 构建页面标题的最佳实践：
	* 使用hx标签
	* 页面只是使用一个h1
	* hx使用过程中不要跳级
	* 不要使用hx设置样式
* 设计表单：
	* 使用label标签，并设置label标签的for属性
	* 给输入控件设置合适的水印提示
	* 输入控件设置tab顺序
	* 使用HTML5中引入的表单控件
	
##### HTML5新特性使用
* async和defer属性
	* 不使用在内联里面
	* defer：以并行的方式下载脚本，而不是阻塞的方式下载，在脚本加载完成后，浏览器会在DOM触发之前按照引用顺序运行JS
	* async：以异步的方式下载脚本，在下载结束后立即执行代码，而不会等待页面解析结束
	* 在设置async时候，推荐同时设置defer属性，提高脚本加载执行的性能
* 标签上的自定义属性data-\*
* script可以编写HTML模板和XML数据
    
##### 选择器注意
* 尽量不使用ID选择器
* 减少子选择器的层级（less和Sass的滥用）
* 使用组合CSS类选择器
	
##### 兼容IE浏览器
* 兼容旧浏览器的代码，被称为hack代码
* 熟悉IE浏览器中常见的兼容样式
* 分离样式兼容代码

	```
            .color{ _color:green;}  ( IE6 (含 IE6 ) 以下)
                    
            .color{ *color:gray; }  ( IE7 ( 含 IE7 )以下)
                    
            .color { color:green \0; } ( IE8 + )
                
            .color { color:green \ ; }   ( IE8 . IE9 )
                    
            :root .color { color:green \0; } ( IE9 + )
                    
            .color { color:green \9\0; }   ( IE9+ )
                    
            .color { color:green \9; }   ( IE10 ( 含 IE10 ) 以下 )
                    
            *::-ms-backdrop, .color{ color:red; }   ( IE11 )
                    
            * html .color { color: red; } (IE6 ONLY )
                    
            *+html .color { color: red; } ( IE7 ONLY )
                    
            @media screen\9 { 
                    .color { color: black; } 
                    }  ( IE6 . IE7 )      
            @media \0screen {
                     .color { color: black; } 
                    }  ( IE8 ONLY )      
            @media \0screen, screen\9 {
                     .color { color: black; } 
                    } ( IE6 . IE7 . IE8 ) 
            @media screen\0 {
                     .color { color: black; } 
                    }  ( IE8 . IE9 . IE10 )
                    @media screen and (min-width: 0\0) {
                     .color { color: black; }
                    }  ( IE9 . IE10 )
                    
            
            @media screen and (-ms-high-contrast: active), (-ms-high-contrast: none) { 
            .color { color: black; }
            }   ( IE10 ONLY )
            
            @media all and (-ms-high-contrast:none){
            .color { color:greeny \0; }
            } ( IE10 + )
            
            @media all and (-ms-high-contrast:none){ 
            *::-ms-backdrop, .color { color:green \0; }
             } ( IE11 + )
```

##### em，px，%
* px：绝对尺寸，em：应用元素上字体大小的两倍，%：相对于父元素的百分比
* 尽量设置相对尺寸
* 只有在可预知元素尺寸的情况下才使用绝对尺寸
* 使用em设置字体的大小

----
* [常用的meta方法](http://www.haorooms.com/post/html_meta_ds) 
* [CSS: em, rem区别](https://webdesign.tutsplus.com/zh-hans/tutorials/comprehensive-guide-when-to-use-em-vs-rem--cms-23984)
* [script的defer和async](http://ued.ctrip.com/blog/script-defer-and-async.html)