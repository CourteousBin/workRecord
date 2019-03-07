# 3月工作

## map 使用

- 可以遍历数组对象
- 映射(返回)一个新值
- .map((index)=>{}) index 代表当前元素
- 可以定义过滤器 return 
- 新值 , 只保存你过滤后的值

```javascript
let dataList = [{id:1,name:'bin',age:'21'},{id:2,name:'hong',age:'31'}];
<!-- index 表示当前元素 -->
let dataList = dataList.map((index) => {
    <!-- 新值 , 只保存你过滤后的值 (return 里面的值) -->
  return {
    pictureUrl: util.index.name,
    levelName: index.age,
    typeId: index.id
  }
});
```

## async/awiat 使用

- 在里面有 promise 异步请求的函数 前面加关键字 async
- await promise 函数 代表 , 等待他执行

```javascript
function loadPromise () {
  return new Promise((resolve) => {
    util.request('secondSearch', 'POST', Parma, (e) => {
      resolve(e)
    })
  })
},
async function doing () {
    let result = await this.loadPromise()
    // doing...
} ;
```

## 三目运算符骚操作

if/else if/ else

```html
<view class=" {{ item == '123' ? '123' : item == '456' ? '456' : '789'}} "></view>
```

## inline-flex inline-block

`inline-flex` 和 `inline-block` 一样.

对内部元素来说是个 `display:flext` 的容器，对外部元素来说是个 `inline` 的块。

## box-sizing: border-box;

box-sizing 属性可以被用来调整这些表现:

content-box  是默认值。如果你设置一个元素的宽为100px，那么这个元素的内容区会有100px宽，并且任何边框和内边距的宽度都会被增加到最后绘制出来的元素宽度中。

border-box 告诉浏览器去理解你设置的边框和内边距的值是包含在width内的。

也就是说，如果你将一个元素的width设为100px,那么这100px会包含其它的border和padding，内容区的实际宽度会是width减去border + padding的计算值。

大多数情况下这使得我们更容易的去设定一个元素的宽高。

border-box  width 和 height 属性包括内容，内边距和边框，但不包括外边距

如果 width:50% , 你的padding border 是 px , 那么 . 这些值加起来 , 就会超出 50% 打乱布局

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title></title>
    <link rel="stylesheet" href="">
    <style>
    body {
        width: 100%;
    }

    .box {
        width: 100px;
        padding: 10px;
        height: 100px;
        background-color: green;
        box-sizing: border-box;
        margin: 10px;
        border: 10px solid blue;
    }

    .one {
        background-color: red;
        width: 100px;
        height: 100px;

    }

    .two {
        background-color: blue;
        width: 50%;
        height: 200px;
        box-sizing: border-box;
        padding: 20px;
    }

    .three {
        background-color: red;
        width: 100%;
        height: 100%;
    }
    </style>
</head>

<body>
    <div class="box"></div>
    <div class="one"></div>
    <div class="two">
        <div class="three"></div>
    </div>
</body>

</html>
```

## ...的使用

- 合并
- 解剖

## 更好的条件判断

```javascript
// 更好的条件判断
    let condition = {
        cat:function(){
            console.log('cat')
        },
        dog:function(){
            console.log('dog')
        },
        duck:[1,2,3,4,5]

    }

    function select(animal){
        return condition[animal]
    }

    let result = select('duck')
console.log(result);
    // result();
```

