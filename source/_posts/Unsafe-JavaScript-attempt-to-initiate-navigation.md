---
title: Unsafe JavaScript attempt to initiate navigation for frame...
date: 2019-8-22 17:01:00
tags: iframe sandbox
source: https://www.jianshu.com/p/df102bbe94b9
---
页面 <code>https://www.aaa.com/a.html</code>引入一个iframe<code>https://www.bbb.com/b.html</code>，<code>b.html</code>在代码中尝试修改父级页面的url，由于同源策略会出现以下报错


![出现以上报错信息](/images/unsafe-JavaScript-attempt-img1.png)
```
Unsafe JavaScript attempt to initiate navigation for frame with origin 'https://www.aaa.com/a.html' from frame with URL 'https://www.bbb.com/b.html'. The frame attempting navigation is targeting its top-level window, but is neither same-origin with its target nor has it received a user gesture. See https://www.chromestatus.com/features/5851021045661696.
```
大概意思是：浏览器监测到了iframe中存在不安全的链接正在尝试进行导航。
iframe默认情况下
```
在html5页面中，可以使用iframe的sandbox属性，<iframe src="https://www.bbb.com/b.html"></iframe>如果未添加sandbox属性，或者添加了sandbox但是后面不加任何值，就代表采用默认的安全策略，即：iframe的页面将会被当做一个独自的源，同时不能提交表单，以及执行javascript脚本，也不能让包含iframe的父页面导航到其他地方，所有的插件，如flash,applet等也全部不能起作用。简单说iframe就只剩下一个展示的功能，正如他的名字一样，所有的内容都被放入了一个单独的沙盒。
```

sandbox包含的属性及作用：
```
allow-forms 允许进行提交表单
allow-scripts 运行执行脚本
allow-same-origin 允许同域请求,比如ajax,storage
allow-top-navigation 允许iframe能够主导window.top进行页面跳转
allow-popups 允许iframe中弹出新窗口,比如,window.open,target=”_blank”
allow-pointer-lock 在iframe中可以锁定鼠标，主要和鼠标锁定有关
```

在iframe加上这个代码之后 sandbox="allow-scripts allow-top-navigation allow-same-origin" ，刷新页面再测，就可以正常跳转了


```
turntable.js?v=48149109fd63d82fe8c816eafa1d7a6a:44 Uncaught DOMException: Failed to set the 'href' property on 'Location': The current window does not have permission to navigate the target frame to 'https://luckydraw.wenjuan.com/draw/info/5d5cdb262ee1305873576887/?mid=5d5cdc02f27e69739bbb70b5&short_id=&title=&begin_desc=##/5d5cda1f3631f2edd45f4f90/7Fj67v/%E6%B5%8B%E8%AF%84-%E6%B5%8B%E8%AF%84%E5%88%86%E5%80%BC+%E8%87%AA%E5%AE%9A%E4%B9%89%E6%8A%BD%E5%A5%96/assess'.
    at HTMLCanvasElement.callback (https://luckydraw.wenjuan.com/static/js/draw/turntable.js?v=48149109fd63d82fe8c816eafa1d7a6a:44:50)
    at Wilq32.PhotoEffect._setupParameters._animate (https://luckydraw.wenjuan.com/static/js/draw/awardRotate.js?v=9ddbfcbcea64ded76311975f2c2eea07:238:43)
    at https://luckydraw.wenjuan.com/static/js/draw/awardRotate.js?v=9ddbfcbcea64ded76311975f2c2eea07:230:35
```
![出现以上报错信息](/images/unsafe-JavaScript-attempt-img2.png)