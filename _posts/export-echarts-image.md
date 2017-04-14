---
title: 导出echarts中的图片
date: 2017-04-14 22:55:31
tags: echarts,image
---

> echarts提供了很多精美图表插件，通过浏览器来渲染后，用户可以保存图表为图片。但是有些应用场景，需要在用户不打开浏览器的情况下，能把图表保存下来，比如把echarts图表插入到word文档中。这种需求下，我开发了echarts图片导出服务，并提供了相关接口。

### 提供了两种类型的接口：

- ###### 把定制页面的echarts图表保存为图片
请求实例：
```
curl http://115.29.188.241:3100/ -d '{"url":"http://115.29.188.241/public/echarts/default.html","funcs":"salesChart,bubbleChart","delay":1000}'
```
参数解释：
- 请求接口：http://115.29.188.241:3100/
- 请求方法：POST
- 请求参数：
	- 参数格式：JSON
	- url:定制的echarts图表页面，如：http://115.29.188.241/public/echarts/default.html
	- funcs：上面指定的URL页面上暴露的echarts实例全局变量，多个实例用半角逗号隔开，如：salesChart,bubbleChart。
	![sales](http://ogcxhul17.bkt.clouddn.com/demo-sales.png)
	![bubble](http://ogcxhul17.bkt.clouddn.com/demo-bubble.png)
	- delay：可选项，单位ms，默认100，最大值5000。延时执行时间，有的echarts图表带有动画，需要等待动画执行完，delay时间越长，等待接口返回时间越长，建议关闭动画。

返回结果：
```
{"err":0,"msg":"success","imgs":{"bubbleChart":"http://saas-pubsentiment-img1.oss-cn-hangzhou.aliyuncs.com/2017/04/14/1492182803618.png","salesChart":"http://saas-pubsentiment-img1.oss-cn-hangzhou.aliyuncs.com/2017/04/14/1492183306861.png"}}
```

出参解释：
- err： 0 或者 1 ， 0 表示没有错误，1表示发生错误。
- msg： 成功返回success，失败返回错误的信息。
- imgs：json对象，key为请求参数funcs中指定的全局变量名，比如这里的salesChart对应的图片为http://saas-pubsentiment-img1.oss-cn-hangzhou.aliyuncs.com/2017/04/14/1492183306861.png，bubbleChart对应的图片为http://saas-pubsentiment-img1.oss-cn-hangzhou.aliyuncs.com/2017/04/14/1492182803618.png
![salesChart](http://saas-pubsentiment-img1.oss-cn-hangzhou.aliyuncs.com/2017/04/14/1492183306861.png)	
![bubbleChart](http://saas-pubsentiment-img1.oss-cn-hangzhou.aliyuncs.com/2017/04/14/1492182803618.png)


- ###### 根据echarts option参数来生成图片，这里echarts的版本为3.5.3
请求实例：
```
curl http://115.29.188.241:3100/ -d '{"echartsOption":{"tooltip":{"trigger":"item","formatter":"{a} <br/>{b}: {c} ({d}%)"},"legend":{"orient":"vertical","x":"left","data":["直接访问","邮件营销","联盟广告","视频广告","搜索引擎"]},"series":[{"name":"访问来源","type":"pie","radius":["50%","70%"],"avoidLabelOverlap":false,"label":{"normal":{"show":false,"position":"center"},"emphasis":{"show":true,"textStyle":{"fontSize":"30","fontWeight":"bold"}}},"labelLine":{"normal":{"show":false}},"data":[{"value":335,"name":"直接访问"},{"value":310,"name":"邮件营销"},{"value":234,"name":"联盟广告"},{"value":135,"name":"视频广告"},{"value":1548,"name":"搜索引擎"}]}]},"width":600,"height":400}'
```
参数解释：
- 请求接口：http://115.29.188.241:3100/
- 请求方法：POST
- 请求参数：
	- 参数格式：JSON
	- echartsOption：echarts的配置信息
	![demo-pie](http://ogcxhul17.bkt.clouddn.com/demo-pie.png)
	- width：可选项，生成图片的宽度，单位px，最大值：2000，默认值：600
	- height：可选项，生成图片的高度，单位px，最大值：2000，默认值：400
```
{"err":0,"msg":"success","imgs":{"myChart":"http://saas-pubsentiment-img1.oss-cn-hangzhou.aliyuncs.com/2017/04/14/1492184722716.png"}}
```

出参解释：

- err： 0 或者 1 ， 0 表示没有错误，1表示发生错误。
- msg： 成功返回success，失败返回错误的信息。
- imgs：这里的key固定为myChart
![demo-pie](http://saas-pubsentiment-img1.oss-cn-hangzhou.aliyuncs.com/2017/04/14/1492184722716.png)
