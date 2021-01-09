---
title: "TCP的3次握手"
date: 2019-01-18
categories: ["other"]
tags: ["tvp"]
draft: false 
---
## 3次握手
<div class="mermaid">
sequenceDiagram
A->>B: 1
B-->>A: 2
A->>B: 3
</div>

```
第1次代表A向B请求
第2次代表B确认收到A的请求，并向A发送请求
第3次代表A确认收到B的请求
```
## 4次挥手
<div class="mermaid">
sequenceDiagram
A->>B: 1
B-->>A: 2
B-->>A: 3
A->>B: 4
</div>

```
第1次代表A告诉B，要关闭连接
第2次代表B收到A关闭连接的请求，并确认
第3次代表B关闭与A的连接
第4次代表A确认B的关闭连接
```
## 6种标志位
```
SYN：同步标志
ACK：确认标志
RST：复位标志
URG：紧急标志
PSH：推标志
FIN：结束标志
```
