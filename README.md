1.new的时候发生了什么？js实现面向对象

（1）创建一个新对象；

（2）将构造函数的作用域赋给新对象（因此this就指向了这个新对象）；

（3）执行构造函数中的代码（为这个新对象添加属性）；

（4）返回新对象。

2.vue2 diff

diff 是对比更新前后的vDom  比较之后拿到索引在进行索引的比较，之后再将vnode进行移动新增或者删除
	OldStartIndex   OldLastIndex  newStartIndex newLastIndex  首首比较 尾尾比较 首尾比较    核心  首尾+索引对比
v3 diff

3.js值类型和引用类型的区别？怎么判断

存储地址  值类型数据是存在栈  引用类型是存在堆里面的     

typeof、instanceof、constructor、Object.prototype.toString.call()

4.除了new之外，还有什么方法可以实例化一个对象



5.闭包

能够读取其它函数内部变量的函数

函数返回一个函数   或者作为参数被其它函数调用

闭包的缺点：不能被垃圾回收机制回收（性能问题）  内存泄漏 


自由变量:当前作用域没有定义变量的值，他会沿着定义的位置向上查找，不会再调用的位置查找

产生闭包的三种情况：
1.函数返回函数
2.函数作为参数
3.自执行匿名函数


6.slot的用法

具名 匿名

slot（vue3废弃）   slot-scoped（vue3废弃）  v-slot    el-table中有用到


7.输入url到显示

1.根据URL进行DNS解析获取到真实IP，请求服务器，
2.服务器将后台返回的数据（HTML+CSS+JS+图片。。）返回给浏览器，
3.浏览器逐步解析后台返回的数据，DOM树，CSSom树渲染，js操作DOM树
4.数据渲染到页面上。


8.BFC(块级格式化上下文)
如何产生BFC
display属性不为none
position为absolute或fixed
display为 inline-block, table-cell, table-caption, flex, inline-flex
overflow不为visible

主要用途

清除内部元素浮动
防止margin合并（添加BFC在另一个元素）
右侧自适应不会和浮动产生交集

BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。包括浮动，和外边距合并等等，因此，有了这个特性，我们布局的时候就不会出现意外情况了。
9.原型链

10.深浅拷贝

浅拷贝：改变内存中的指针指向，修改新的内容会影响别的内容
深拷贝：重新开辟新空间，跟原先的没有任何关系

如何实现深拷贝：
1.JSON.parse(JSON.stringfy(xxx))
缺点：不能复制函数
2.递归
3.函数库lodash的_.cloneDeep方法

```
//递归
function deepClone(obj){
    let objClone = Array.isArray(obj)?[]:{};
    if(obj && typeof obj==="object"){
        for(key in obj){
            if(obj.hasOwnProperty(key)){
                //判断obj子元素是否为对象，如果是，递归复制
                if(obj[key]&&typeof obj[key] ==="object"){
                    objClone[key] = deepClone(obj[key]);
                }else{
                    //如果不是，简单复制
                    objClone[key] = obj[key];
                }
            }
        }
    }
    return objClone;
}
```
11.MVC与MVVM

MVC类似于闭环，M2V，V2C，C2M

MVVM则是VM作为桥梁，两边交互都需要通过VM，所以两边和VM的关系都是双向的

MVVM的优点：
低耦合
可重用性
独立开发
可测试


12.手写Promise

内置state变量
接受参数（resolve，reject）
then方法（race,all，allsetle）


13.Map和Set类型的区别

map是键值对
set  key和value值相等

注意set在不同浏览器格式不同
谷歌  {}
火狐[]


14.grid布局
grid-template-row
grid-template-column
grid-template-area


15.webpack
  tree-shaking


	tree-shaking主要指的是按需加载结合es6的import
	plugin loader 执行时机
	loader在打包之前执行，进行文件转换，plugin贯穿整个打包过程，优化打包过程
	css-loader作用
	解析url()和@import

16.雪碧图  首屏加载

雪碧图：一张大图，通过移动大图来显示不同的部分(backgroun-position:左右,上下)

首屏加载：图片懒加载  data-image   用src替换
减少请求  


17.虚拟DOM 虚拟DOM是如何合并patch的


18.vuex为什么要设计mutation和action ，一个不行吗



19.vue挂载和卸载 父子组件生命周期钩子执行顺序

父 beforecreate 父 created 父beforeMount  子 beforeCreate 子 created 子 beforeMount 子 mounted
 父 mounted

父 beforeDestroy 子beforeDestroy 子 destroyed  父 destroyed


20.强缓存和协商缓存

304

200

21.如何理解script标签是个宏任务

queue1(宏):[
    
    
    time1
    tiem2
     ]
queue2(微):[

]

steTime(宏):[
        start1 , p1 ,end1
    ],
    setTime2(宏):[

    ]


start1 -> p1 ->  end1-> then1-> start2->p2->end2 ->then2 ->time1 -> time2

22.https的加密方式

对称加密 非对称加密 证书

23.Object.is和===的区别
Object.is
NaN = NaN  -0 != +0
===  相反

24.事件委托

25.use strict



26.url和uri的区别
URL属于URI的一种

27.为什么不能同时使用v-if和v-for，:key

性能问题

28.element二次封装属性太多怎么办

$attrs,会排除掉props


29.echart中数据太多，渲染慢怎么办

beforeDestroy(){
    this.$refs.myChart && this.$refs.myChart.clear();
};

30.请求头中connect=keep-alive代表什么意思

tcp连接一直开启

31.对象冻结的方法和场景

Object.preventExtensions   不能增加方法和属性
Object.seal()：不能增删
Object.freeze() 不能增删改 只能冻结本身对象  如果内部还有引用类型的，不会被冻结
手动实现  使用Object.freeze()递归将内部也冻结
32.原型链和继承

instanceof 方法就是利用原型链来判断的

实例=》构造参数（=》父类）=》Object=>null

33.vue2源码

v-if v-show区别

v-if v-for优先级

双向绑定原理

v-model

computed和watch区别

nextTick


34.什么是单点登录？如何实现？

token 鉴权

35.web常见的攻击方式有哪些？如何防御？
XSS CSRF

36.this的指向
window或者setTimeout下指向window
构造函数内部this指向实例对象
箭头函数的this指向上层，没有就是window

36.weakMap weakSet
一种弱类型
主要是可以用垃圾回收机制回收
weakMap的key必须是引用类型
不可迭代

37.call apply bind 

bind返回的是函数本身 也是每个参数放在后面
apply的参数用数组包裹
call是每个参数放在后面

38.ajax，fetch，axios区别？


39.css画三角形？还有别的方法吗？


40.重绘  重排



首先这个涉及到了浏览器差的运行机制
1. 构建Dom树，生成内容树  HTML和js做的
2. 构建渲染树CSSom树 CSS做的
3. 布局渲染树  计算大小和位置
4. 绘制渲染树  根据UI来绘制

#### 重绘指的是元素的外观属性发生了变化，比如color，background-color等，重排（回流）指的是元素的尺寸，布局，隐藏等改变需要重新构建。在回流的时候，浏览器会使渲染树中受影响的部分失效，并重新构造这部分渲染树，完成回流后，浏览器会发生重绘，所以回流必定会触发重绘，重绘不一定会触发回流。

41.类数组转换为数组
Array.from()

42.indexOf和includes的区别

NaN indexOf 返回-1，includes返回true

43.拍平数组（flat）

1.Array.prototype.concat.apply([],arr)
直接使用可以拍平二维数组

const flat=(arr)=>{
    const hasDeeper=arr.some(item=>item instanceof Array)
    if(!hasDeeper){
        return arr
    }
    const res =Array.prototype.cancat.apply([],arr)
    return flat(res)
}

44.css垂直水平居中

1.position+margin负值 （宽高固定）

2.position+margin：auto （固定宽高）

3.display:table-ceil +vertical-align:middle （固定宽度）

4.postition+transform(不需要固定宽高)

5.flex(不需要固定宽高)

45.函数柯里化

46.innerHeight offsetHeight

