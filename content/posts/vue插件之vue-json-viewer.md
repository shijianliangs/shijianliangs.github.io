---
title: "vue插件之vue-json-viewer"
date: 2017-10-11
categories: ["other"]
tags: ["vue","vue-json-viewer"]
draft: false 
---
## 安装
```bash
npm install vue-json-viewer --save
```

## 使用
```xml
<!-- 默认不展开 -->
<json-viewer :value="jsonData"></json-viewer>
<!-- 默认展开 -->
<json-viewer  :value="jsonData"  :expand-depth=5 copyable  boxed  sort></json-viewer>
```
```js
import Vue from 'vue'
import JsonViewer from '../../node_modules/vue-json-viewer'

Vue.use(JsonViewer)

data() {
    return {
        jsonData: {"a":[{"b":"v"},{"c":5}],"M":"n"}
    }
 }
```

## 效果

![image-20191016082647005](https://typora-1258677967.cos.ap-chengdu.myqcloud.com/image-20191016082647005.png)

## 参考
[https://blog.csdn.net/sanlingwu/article/details/84141673](https://blog.csdn.net/sanlingwu/article/details/84141673)