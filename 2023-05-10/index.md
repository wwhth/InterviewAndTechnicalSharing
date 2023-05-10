## css盒模型
  1. 标准盒模型：box-sizing: content-box;
  > 元素宽度为 content width
  2. IE盒模型：box-sizing: border-box;
  > 元素宽度为：content + padding + border

## BFC块级格式化上下文
  1. 触发条件 
  float不为none， 
  overflow不为visible， 
  display为inline-block、table-caption、table-cell  
  2. 应用 
    - 阻止margin重叠
    - 阻止元素被浮动元素覆盖
    - 清除内部浮动（父元素高度塌陷问题）
## 回流和重绘
  1. 回流必会引起重绘，回流的性能开销更大
  2. 触发回流的情况：
    - 页面首次渲染
    - 浏览器窗口变化
    - 元素尺寸或者位置发生变化
    - 元素内容发生变化（文字大小、数量、图片）
    - 添加或者删除dom节点
    - css伪类激活（active、hover）
    - 查询某些属性或者调用某些方法（浏览器回流保证数据的准确性）
  3. visibility是重绘、opacity不会回流也不会重绘（GPU渲染 css硬件加速，transform、opacity、filter）
  4. 如何减少回流重绘
    - 避免使用table布局
    - 在dom树末端改变class
    - 减少使用css表达式（calc）
    - 避免多层内联样式
    - 将复杂动效应用在脱离文档流的布局上（position：fixed、absolute）
    - 避免在js中多次操作样式
## 事件流和事件委托

## DOM和BOM的区别
DOM： window.document
BOM: window

## AJAX
```
function myAjax() {
    var xhr = new XMLHttpRequest()
    // 1. 处理响应回调
    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4) {
            if (xhr.status === 200) {
                ...
            }
        }
    }
    // 2. 初始化一个请求
    xhr.open('post', '/xxx', true)
    // 3. 设置请求头信息
    xhr.setRequestHeader('Content-type', 'application/json;charset=UTF-8')
    // 4. 发送请求
    var params = { ... }
    xhr.send(params)
}
```
> fetch
```
fetch(url)
  .then(response => response.json())
  .then(data => console.log(data))
```
## 浏览器输入url回车后发生了什么
  - 解析url，是否命中缓存
  - 访问dns服务器，域名解析获取ip地址
  - 三次握手建立TCP连接
  - 发送HTTP请求
  - 服务器处理请求并返回HTTP报文
  - 浏览器解析渲染页面
  - 断开连接：TCP四次挥手

## 跨域
 1. JSONP，使用script标签，定义回调函数接收数据，浏览器兼容性好，只能发送get请求
 2. CORS 服务器配置相关
 3. img标签
 4. NGINX反向代理配置
 5. webSocket、PostMessage
 > 本地工程化配置proxy来代理跨域请求后端（webpack、vite）

## 移动端屏幕适配
 1. mate标签 viewprot
 2. postcss（转化）
 3. rem、%、vh、vm弹性单位
 4. 媒体查询，响应式布局

## 数据存储
1. cookie：有过期时间，长度限制4kb，且每次都会携带在请求头中，不推荐使用
2. SessionStorage：无过期时间，容量大，但窗口关闭自动删除
3. LocalStorage：无过期时间，容量大，应用场景很广
4. IndexedDB：存储更大量的结构化数据，浏览器本身不限制其容量

## 浏览器缓存
> 浏览器缓存状态都是通过设置http header来实现的
1. 强缓存
  - 由浏览器决定的，若命中缓存，资源是否更新都不会请求接口，状态码为200
  - 请求头expires（设置具体的过期时间），cache-control（设置多久之后过期），若同时存在cache-control优先级更高
2. 协商缓存
  - 是服务器收到请求后进行更新判断，如果资源没有修改就返回 Not Modified（状态码：304）
  - 请求头last-momodified（最后一次更改时间），ETag：优先级更高，资源的唯一标识。

## JavaScript异步加载async、defer

## 路由（hash、history）

## 垃圾回收
