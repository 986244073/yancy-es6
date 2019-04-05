# 一、介绍 #

## 1.历史 ##

1. ECMAScript和JavaScript
	- ECMA是标准，JS是实现
		- 类似于HTML5是标准，IE10、Chrome、FF都是实现
		- 换句话说，将来也能有其他XXXScript来实现ECMA
	- ECMAScript简称**ECMA或ES**
	- 目前版本
		- 低级浏览器主要支持ES 3.1
		- 高级浏览器正在从ES 5过渡到ES 6
2. 历史版本

|时间|ECMA|JS|解释|
|---|---|---|---|
|1996.11|ES 1.0|JS稳定|Netscape将JS提交给ECMA组织，ES正式出现|
|1998.06|ES 2.0||ES2正式发布|
|1999.12|ES 3.0||ES3被广泛支持|
|2007.10|ES 4.0||ES4过于激进，被废了|
|2008.07|ES 3.1||4.0退化为严重缩水版的3.1<br/>因为吵得太厉害，所以ES 3.1代号为Harmony(和谐)|
|2009.12|ES 5.0||ES 5.0正式发布<br/>同时公布了JavaScript.next也就是后来的ES 6.0|
|2011.06|ES 5.1||ES 5.1成为了ISO国际标准|
|2013.03|ES 6.0||ES 6.0草案定稿|
|2013.12|ES 6.0||ES 6.0草案发布|
|2015.06|ES 6.0||ES 6.0预计发布正式版<br/>JavaScript.next开始指向ES 7.0|

# 二丶兼容性

> http://kangax.github.io/compat-table/es5/
> http://kangax.github.io/compat-table/es6/

ES6(ES2015)支持IE10+、Chrome、FireFox、移动端、NodeJS

不支持可以:1.在线转换2.提前编译

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script src="browser.js" charset="utf-8"></script>
    <script type="text/babel">
    let a=12;
    let b=5;

    alert(a+b);
    </script>
  </head>
  <body>
  </body>
</html>

```



# 三丶变量

## var

1.可以重复声明

2.无法限制修改

3.没有块级作用域

```javascript
if (true) {
var a = 12;
}
alert(a)
```

## let (声明变量)

不能重复声明,可以修改,支持块级作用域

```javascript
let a=12;
let a=123;
alert(a);//SyntaxError: redeclaration of let a
```

```javascript
if (true) {
let a = 12;
}
alert(a);//ReferenceError: a is not defined
```

## const(声明常量)

不能重复声明,不能修改,支持块级作用域

```javascript
const a = 12;
a = 123;
alert(a);//TypeError: invalid assignment to const `a'
```

## 作用域

1.传统函数级

2.ES6块级



## 语法块

```
{}

if(){

}

for(){

}

{

}

```



# 四丶函数

## 箭头函数(可以修复this)

只是简写

```javascript
function 名字(参数){

}
(参数)=>{

}
```

1.如果，有且仅有1个参数，()也可以省

2.如果，有且仅有1条语句-return，{}可以省(json一般不简写)

```javascript   
    let show=a=>a*2;
    alert(show(12));
```

## 函数的参数



### 1.函数的扩展

>   function show(a, b, ...args){}

```javascript
function show(a, b, ...args, c){
alert(args);
}

show(12, 15, 8, 9, 20, 21, 90);//Uncaught SyntaxError: Rest parameter must be last formal parameter
```

*Rest Parameter必须是最后一个*

### 2.数组展开

```javascript
  let arr = [1, 2, 3];
      show(...arr);
      //...arr
      //1,2,3
      //show(1,2,3);
      function show(a, b, c) {
        alert(a);
        alert(b);
        alert(c);
      }
```

```javascript
    let arr1=[1,2,3];
    let arr2=[5,6,7];

    let arr=[...arr1, ...arr2];

    alert(arr);
```

  *展开后的效果，跟直接把数组的内容写在这儿一样*

```javascript
    let a;
    let arr=[1,2,3];

    a=...arr;//Uncaught SyntaxError: Unexpected token ...

    alert(a);
```

### 3.默认参数

```javascript
function show(a, b = 5, c = 12) {
    console.log(a, b, c);
  }

  show(99, 19, 88);
```

# 五丶解构赋值

1.左右两边结构必须一样
2.右边必须是个东西
3.声明和赋值不能分开(必须在一句话里完成)

数组:

```javascript
    let [a,b,c]=[1,2,3];
    console.log(a, b, c);
```

json:

```javascript
    let {a, c, d}={a: 12, c: 5, d: 6};
    console.log(a, c, d);
```

```javascript
    let [{a, b}, [n1, n2, n3], num, str]=[{a: 12, b: 5}, [12,5,8], 8, 'cxzcv'];

    console.log(a,b,n1,n2,n3,num,str);
```
注意
```javascript
    let [a,b]={a: 12, b: 45};

    console.log(a,b);//Uncaught TypeError: {(intermediate value)(intermediate value)} is not iterable

```

```javascript
    let {a,b}={12,5};

    console.log(a,b);//Uncaught SyntaxError: Unexpected token ,
```

```javascript
    let [a,b];
    [a,b]=[12,5];
    console.log(a,b);//Uncaught SyntaxError: Missing initializer in destructuring declaration
```

# 六丶系统对象

## map       映射          

一个对一个
  [12, 58, 99, 86, 45, 91]
  [不及格, 不及格, 及格, 及格, 不及格, 及格]

```javascript
let arr=[19, 85, 99, 25, 90];
//用item分别存储
let result=arr.map(item=>item>=60?'及格':'不及格');

alert(score);
alert(result);
```

  [45, 57, 135, 28]
  [
    {name: 'blue', level: 0, role: 0},
    {name: 'zhangsan', level: 99, role: 3},
    {name: 'aaa', level: 0, role: 0},
    {name: 'blue', level: 0, role: 0},
  ]

## reduce      汇总          

一堆出来一个
  算个总数 
    [12, 8000000, 599999] =>  80060011

```javascript
 let arr=[12,69,180,8763];
//tmp为前面的和 12+69  item=180
let result=arr.reduce( (tmp, item, index){
      //alert(tmp+','+item+','+index);
      return tmp+item; //tmp为前面的和 12+69  item=180
});

alert(result);
```

算个平均数
    [12, 59, 99]          =>  56.67

```javascript
  let arr=[12,69,180,8763];

    let result=arr.reduce(function (tmp, item, index){
      if(index!=arr.length-1){ //不是最后一次
        return tmp+item;
      }else{                    //最后一次
        return (tmp+item)/arr.length;
      }
    });

    alert(result);
```

## filter      过滤器

```javascript
    let arr=[12,5,8,99,27,36,75,11];

    let result=arr.filter(item=>item%3==0);

    alert(result);
```

```javascript
    let arr=[
      {title: '男士衬衫', price: 75},
      {title: '女士包', price: 57842},
      {title: '男士包', price: 65},
      {title: '女士鞋', price: 27531}
    ];

    let result=arr.filter(item=>item.price>=10000);

    console.log(result);
```



## forEach     循环(迭代)

```javascript
let arr=[12,5,8,9];

arr.forEach((item,index)=>{
alert(index+': '+item);
    });
```

# 七丶字符串

## 1.多了两个新方法

  startsWith

```javascript
let str='git://www.baidu.com/2123123';

    if(str.startsWith('http://')){
      alert('普通网址');
    }else if(str.startsWith('https://')){
      alert('加密网址');
    }else if(str.startsWith('git://')){
      alert('git地址');
    }else if(str.startsWith('svn://')){
      alert('svn地址');
    }else{
      alert('其他');
    }
```



  endsWith

```javascript
    let str='1.png';

    if(str.endsWith('.txt')){
      alert('文本文件');
    }else if(str.endsWith('.jpg')){
      alert('JPG图片');
    }else{
      alert('其他');
    }
```



## 2.字符串模板

  字符串连接

```javascript
let title='标题';
let content='内容';
let str='<div>\
  <h1>'+title+'</h1>\
  <p>'+content+'</p>\
</div>';

let str2=`<div>
  <h1>${title}</h1>
  <p>${content}</p>
</div>`;
```



  i.直接把东西塞到字符串里面      ${东西}
  ii.可以折行

# 八丶ES6的面向对象

## 1.类,继承

```javascript
//原来的
function User(name, pass){
this.name=name;
this.pass=pass;
}
//外挂方法
User.prototype.showName=function (){
alert(this.name);
};
User.prototype.showPass=function (){
alert(this.pass);
};
//继承
function VipUser(name, pass, level){
      User.call(this, name, pass);//继承属性
      this.level=level;
    }

    VipUser.prototype=new User();
    VipUser.prototype.constructor=VipUser;
    VipUser.prototype.showLevel=function (){
      alert(this.level);
    };

    var v1=new VipUser('blue', '123456', 3);

    v1.showName();
    v1.showPass();
    v1.showLevel();
```

```javascript
//现在的
class User{
constructor(name, pass){
this.name=name;
this.pass=pass;
}

showName(){
alert(this.name);
}
showPass(){
alert(this.pass);
}
}
//继承
class VipUser extends User{
constructor(name, pass, level){
super(name, pass);
this.level=level;
}

showLevel(){
alert(this.level);
}
}

var v1=new VipUser('blue', '123456', 3);

v1.showName();
v1.showPass();
v1.showLevel();
```

1.class关键字、构造器和类分开了
2.class里面直接加方法

继承：

super=超类==父类

## 2.应用--react

React：
1.组件化——class
2.JSX=babel==browser.js

基础的东西

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script src="react.js" charset="utf-8"></script>
    <script src="react-dom.js" charset="utf-8"></script>
    <script src="browser.js" charset="utf-8"></script>
    <script type="text/babel">
    window.onload=function (){
      let oDiv=document.getElementById('div1');

      ReactDOM.render(
        <span>123</span>,
        oDiv
      );
    };
    </script>
  </head>
  <body>
    <div id="div1">

    </div>
  </body>
</html>

```

组件

```javascript
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <script src="react.js" charset="utf-8"></script>
    <script src="react-dom.js" charset="utf-8"></script>
    <script src="browser.js" charset="utf-8"></script>
    <script type="text/babel">
    class Item extends React.Component{
      constructor(...args){
        super(...args);
      }

      render(){
        return <li>{this.props.str}</li>;
      }
    }

    class List extends React.Component{
      constructor(...args){
        super(...args);
      }

      render(){
        return <ul>
          {this.props.arr.map(a=><Item str={a}></Item>)}
        </ul>;
      }
    }

    window.onload=function (){
      let oDiv=document.getElementById('div1');

      ReactDOM.render(
        <List arr={['abc', 'erw', 'sdfasdf', 'dfasdfsdfds']}></List>,
        oDiv
      );
    };
    </script>
  </head>
  <body>
    <div id="div1">

    </div>
  </body>
</html>

```

# 九丶json

## 1.标准写法

```json
{"key": "aaa", "key2": 12} 
```

## 2.JSON对象

stringify 把json转换成字符串
parse   字符串转换json

# 十丶异步处理

## 异步——多个操作可以一起进行，互不干扰 √





```javascript
$.ajax({
  url: 'data/1.json',
  dataType: 'json',
  success(data1){
    $.ajax({
      url: 'data/2.json',
      dataType: 'json',
      success(data2){
        $.ajax({
          url: 'data/3.json',
          dataType: 'json',
          success(data3){
            console.log(data1, data2, data3);
          }
        });
      }
    });
  }
});
```

## 同步——操作一个个进行

```javascript
let data1=$.ajax('data/1.json');
let data2=$.ajax('data/2.json');
let data3=$.ajax('data/3.json');
```

## Promise

```javascript
  Promise.all([
      $.ajax({url: 'data/1.json', dataType: 'json'}),
      $.ajax({url: 'data/2.json', dataType: 'json'}),
      $.ajax({url: 'data/3.json', dataType: 'json'}),
    ]).then(([data1, data2, data3])=>{
      console.log(data1, data2, data3);
    }, (res)=>{
      alert('错了');
    });
```

# async/await

```javascript
 async function show(){
      let data1=await $.ajax({url: 'data/1.json', dataType: 'json'});
      if(data1.a<10){
        let data2=await $.ajax({url: 'data/2.json', dataType: 'json'});
        alert('a');
      }else{
        let data3=await $.ajax({url: 'data/3.json', dataType: 'json'});
        alert('b');
      }
    }
```

