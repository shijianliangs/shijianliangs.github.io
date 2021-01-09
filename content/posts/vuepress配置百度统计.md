---
title: "vuepress配置百度统计"
date: 2018-01-05
categories: ["other"]
tags: ["vuepress","baidu-tongji"]
draft: false 
---
## config.js

```javascript
module.exports = {
    ......
    head: [
        ['script', {}, `
            var _hmt = _hmt || [];
            (function() {
            var hm = document.createElement("script");
            hm.src = "https://hm.baidu.com/hm.js?xxxxxxxxxx";
            var s = document.getElementsByTagName("script")[0];
            s.parentNode.insertBefore(hm, s);
        })();
        `]
    ]
}
```

## 参考

[https://www.codeleading.com/article/94892317519/](https://www.codeleading.com/article/94892317519/)

