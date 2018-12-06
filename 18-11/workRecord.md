# 每天难点

## 2018-11-22 

- html 页面内锚点定位及跳转方法总结
    + https://blog.csdn.net/this_itboy/article/details/76020658
- localStorage使用总结
    + https://www.cnblogs.com/st-leslie/p/5617130.html
- 跨域影响 , 如果你在 jsonp 里嵌套 ajax 默认为 get请求
    + https://www.cnblogs.com/nullman/p/6185676.html
- layui 自带 ajax 可以解决 跨域 在 suceess 只能 get请求
    + 跨域后 回调 再一次 ajax 请求 发现 只能get 不能post
    + 不知道怎么解决 .. 发现 用 layui jq 可以解决
- promise 
```javascript
    // Promise
    var p_city = new Promise(function(resolve,reject){
        $.ajax({
            url: '',
            type: "GET",
            dataType: "jsonp",
            jsonp: "callback",
            success: function (data) {
                var city = data.result.addressComponent.city;
                resolve(city);
            }
        })
    })     

    function runAsync(value){

        var getCityId = new Promise(function(resolve,reject){
            $.ajax({
                url:'/wap.php/api/getCityId',
                method:'POST',
                data:{
                    city_name:value
                },
                success:function(data){
                    var data = $.parseJSON(data);
                    resolve(data);
                    var status = data.statusCode;

                    if(status == '200') {

                        var city_name = data.data.region_name;
                        var city_id = data.data.region_id;
                        $('.location').text(city_name);
                        $('.location').attr('data-region_id',city_id);
                    }
                }
            })
        })

        return getCityId;

    }


    p_city.then(function(value){
        console.log(value);

        return runAsync(value);
    }).then(function(data){
        console.log(data);
    })

```

## 2018-11-27

- &#65279导致页面顶部空白一行解决方法
    + https://jingyan.baidu.com/article/1709ad80693cbe4635c4f066.html
- 微信小程序】——wxss引用外部CSS文件及iconfont，图文教程
    + https://blog.csdn.net/weixin_42661321/article/details/82379930
- 类似小说 章节数据库设计
    + https://bbs.csdn.net/wap/topics/340187185
- 小程序图书管理设计
    + 图书
        * 是否免费
            - 是: 标签 为免费
            - 否:跳转到购买页面
                + 购买了是在个人表中 , 新建一个购买图书字段 , 并把图书id加入进去?
                + 如果图书删除了还能看吗
    + 图书标签
        * 免费标签
        * 自定义的标签?
    + 购买
        * 是否会员
            - 是:会员价打折购买
            - 否:购买图书(实际上购买会员?)
            - 疑问:购买了会员 .. 还要买图书吗?
    + 章节设计
        * 是否有免费试读章节
        * 付费章节(需要购买)
- 前端基础算法 
    + https://juejin.im/entry/5acf784a5188255caf069a93
```javascript
function isPalindrome1(val){
            // 允许输入字符串和数字和布尔值
            if (typeof val !== 'string') val = val.toString();

            // split()
            // 拆分字符串 , 把字符串转换成数组 split('') 每个字符串 , 隔开\
            
            // reverse()
            // 数组倒叙
            
            // join()
            // split()逆向方法, 将数组合并成字符串 返回一个新字符串
             
            let newVal = val.split('').reverse().join('');
            
            return val === newVal;
        }
        isPalindrome1(121) // true
        isPalindrome1('yuzuy') // true

        /*
        * 判断文字是否为回文
        * @param {string|number} val 需要判断的文字
        * @return {boolean} bool 是否为回文 
        */
        function isPalindrome2(val){
            val = val + ''; // 非字符串转化为字符串

            // charAt() 方法可返回指定位置的字符。
            // var str="Hello world!"
            // str.charAt(0) -> H
            // str.charAt(1) -> e
            // str.charAt(2) -> l
            
            // 这里为什么 i <= j 呢？如果中间只有一个字符，是不需要比较的，它肯定等于它本身！！！
            for(let i = 0, j = val.length - 1; i < j; i++, j--){

                // 最前面和最后面比较
                // 如果中间只有一个字符，是不需要比较的
                if(val.charAt(i) !== val.charAt(j)){
                    return false;
                }
            }
            
            return true;
        }
        isPalindrome2(12321) // true
        // isPalindrome2('yuzuy') // true
        

        // 反转字符串
        function reverseVal1(val){
            val = val+'';
            
            return val.split('').reverse().join('');
        }

        var bin =  reverseVal1('bin');


        /*
        * 反转字符串
        * @param {string} val 需要反转的字符串
        * @return {string} str 反转后的字符串
        */
        function reverseVal2(val){
            val = val+'';
            
            let str = '',
                i = 0,
                len = val.length;
            while(i < len){

                str += val.charAt(len - 1 - i);

                i++; 
            }
            
            return str;
        }
        var bin =  reverseVal2('bin');
        // console.log(bin)
    
        function my_reverseVal(val){
            val = val+'';
            let str = '';
            for(var i = 0,j = val.length-1;i <= j;i++){
                str += val.charAt(j - i);
            }
            return str;
        }   
        var bin = my_reverseVal('bin');
```
- 前端工程基础
    + https://juejin.im/entry/55de6f5f60b271314aed0917


## 2018-11-28

- 算法
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title></title>
    <link rel="stylesheet" href="">
</head>
<body>
    <script>
        function isPalindrome1(val){
            // 允许输入字符串和数字和布尔值
            if (typeof val !== 'string') val = val.toString();

            // split()
            // 拆分字符串 , 把字符串转换成数组 split('') 每个字符串 , 隔开\
            
            // reverse()
            // 数组倒叙
            
            // join()
            // split()逆向方法, 将数组合并成字符串 返回一个新字符串
             
            let newVal = val.split('').reverse().join('');
            
            return val === newVal;
        }
        isPalindrome1(121) // true
        isPalindrome1('yuzuy') // true

        /*
        * 判断文字是否为回文
        * @param {string|number} val 需要判断的文字
        * @return {boolean} bool 是否为回文 
        */
        function isPalindrome2(val){
            val = val + ''; // 非字符串转化为字符串

            // charAt() 方法可返回指定位置的字符。
            // var str="Hello world!"
            // str.charAt(0) -> H
            // str.charAt(1) -> e
            // str.charAt(2) -> l
            
            // 这里为什么 i <= j 呢？如果中间只有一个字符，是不需要比较的，它肯定等于它本身！！！
            for(let i = 0, j = val.length - 1; i < j; i++, j--){

                // 最前面和最后面比较
                // 如果中间只有一个字符，是不需要比较的
                if(val.charAt(i) !== val.charAt(j)){
                    return false;
                }
            }
            
            return true;
        }
        isPalindrome2(12321) // true
        // isPalindrome2('yuzuy') // true
        

        // 反转字符串
        function reverseVal1(val){
            val = val+'';
            
            return val.split('').reverse().join('');
        }

        var bin =  reverseVal1('bin');


        /*
        * 反转字符串
        * @param {string} val 需要反转的字符串
        * @return {string} str 反转后的字符串
        */
        function reverseVal2(val){
            val = val+'';
            
            let str = '',
                i = 0,
                len = val.length;
            while(i < len){

                str += val.charAt(len - 1 - i);

                i++; 
            }
            
            return str;
        }
        var bin =  reverseVal2('bin');
        // console.log(bin)
    
        function my_reverseVal(val){
            val = val+'';
            let str = '';
            for(var i = 0,j = val.length-1;i <= j;i++){
                str += val.charAt(j - i);
            }
            return str;
        }   
        var bin = my_reverseVal('bin');

        // 循环 倍数
        function factorialize3(n){
            if(typeof n !== 'number') throw new Error('参数必须为整整')
            if(n === 1) return 1;   
            let total = 1;
            while(n>1){
                total = n * total;

                n--;
            }
            return total;
        }

        var result = factorialize3(4);

        function my_factorialize(n){
            if(typeof n !== 'number') throw new Error('必须是整数');

            if(n == 1) return 1;

            for(var total = 1;n>1;n--){
                total = n * total;
            }
            return total;
        }
        // console.log(my_factorialize(4));
        
        /*
        * 生成指定长度的随机字符串
        * @param {number} n 生成字符串个数
        * @return {string} str 反转后的字符串
        * Math.round(Math.random() (str.length - 1))
            Math.ceil(Math.random() (str.length - 1))
            Math.floor(Math.random() * str.length)
            这三种方式等价，都能生成[0, str.length-1]随机数
        */
        // Math.random() 方法可返回介于 0 ~ 1 之间的一个随机数。
        // Math.round() 方法可把一个数字舍入为最接近的整数。(四舍五入)
        // Math.ceil() 方法执行的是向上取整计算
        // Maht.floor() 方法可对一个数进行下舍入。
        function randomString1(n){
            let str = 'abcdefghijklmnopqrstuvwxyz0123456789';
            let tem = '',
                i = 0;
            
            // Math.random 函数产生值的范围[0,1)
            while(i<n){
                tem += str.charAt(Math.round(Math.random() * str.length))
                i++;
            }
            
            return tem;
        }
        // console.log(randomString1(10));
        // 
        /*
        * 生成指定长度的随机字符串
        * @param {number} n 生成字符串个数
        * @return {string} 反转后的字符串
        */
        // Math.random() 生成 0 - 1 的数
        // toString() 转换为字符串
        // substr() 方法可在字符串中抽取从 start 下标开始的指定数目的字符。返回从下标x开始的书
        // slice() 方法可从已有的数组中返回选定的元素。 0-10 返回下标为0 - 10 的字符串 
        function randomString2(n){
            console.log(Math.random().toString(36));
            return Math.random().toString(36).substr(2).slice(0, n)
        }
        // console.log(randomString2(15))


        // 数组去重
        /*
        * 数组去重
        * @param {array} ary 需要去重的数组
        * @return {array} 去重后的数组
        */
        // ES6提供了数据结构Set。类似于数组，但是没有重复值。
        // Set本身是一个构造函数，用来生成Set数据结构
        // Set可以接受一个数组（或者类数组对象）作为参数，用来初始化
        // var set = new Set([1, 2, 3, 4, 4]);
        // console.log([...set])    // [1,2,3,4]
        // Array.from()方法可以将Set结构转换为数组Array.from(new Set(array))
        // var newArr = Array.from(new Set([1,2,3,4,5,6,7,8,9,9,8,7,5]))
        // console.log(newArr)
        function unique1(ary){
            return [...new Set(ary)];
        }
        // console.log(unique1([1,2,3,4,5,6,7,8,9,9,8,7,5]))
        
        // 方法三（临时数组判断插入）
        /*
        * 数组去重
        * @param {array} ary 需要去重的数组
        * @return {array} 去重后的数组
        */
        // ES6 includes() 方法
        // includes() 方法用来判断一个数组是否包含一个指定的值，如果是返回 true，否则false。
        // let site = ['runoob', 'google', 'taobao'];
        // site.includes('runoob');  // true
        // site.includes('baidu');  // fasle 
        function unique3(ary){
            let tem = [],
                i = 0,
                // 设定一个新数组
                len = ary.length;
            
            while(i < len){
                // tem.indexOf() === -1 同理
                // 判断新数组是否有 指定值 
                if(!tem.includes(ary[i])){
                    // 没有那么值推进去 新数组
                    tem.push(ary[i])
                }
                i++;
            }
            
            return tem;
        }
        // console.log(unique3([1,2,3,4,5,6,7,8,9,9,8,7,5]))
        

        /*
        * 数组去重
        * @param {array} ary 需要去重的数组
        * @return {array} 去重后的数组
        */
        // indexOf() 方法可返回某个指定的字符串值在字符串中首次出现的位置。
        // 如果要检索的字符串值没有出现，则该方法返回 -1。
        function unique4(ary){
            let tem = [],
                len = ary.length;
            
            for(let i = 0; i < len; i++ ){
                // 核心，首次的索引出现是否为当前的索引
                // 如果当前数组的第i项在当前数组中第一次出现的位置不是i，那么表示第i项是重复的，忽略掉。否则存入结果数组。
                if(ary.indexOf(ary[i]) === i) tem.push(ary[i]);
                // console.log(ary.indexOf(ary[i]),i);
            }
            
            return tem;
        }
// console.log(unique4([1,2,3,4,5,6,7,8,9,9,8,7,5]))


        /*
        * 数组去重
        * @param {array} ary 需要去重的数组
        * @return {array} 去重后的数组
        */
        function unique5(array){
            var temp = []; //一个新的临时数组
            for(var i = 0; i < array.length; i++){
                if(temp.indexOf(array[i]) == -1){
                    temp.push(array[i]);
                }
            }
            return temp;
        }


        // 出现次数最多的字符
        // 方法一（对象key的唯一性进行累加）
        // Math.max() 方法可返回两个指定的数中带有较大的值的那个数
        // Math.max(5,7) , 但是不支持数组
        // Math.max.apply(obj,parms);//这个obj对象将代替Function类里this对象，第二个传进来的是参数
        // 用 apply 调用
        // console.log(Math.max.apply(null, [1,23,4,5,6,7,8,77]))
        
        // ES6 Object.values()
        // Object.values方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（ enumerable ）属性的键值。
        // var obj = { foo: "bar", baz: 42 };
        // Object.values(obj)
        // ["bar", 42]

        // ES6 Object.keys()
        // ES5 引入了Object.keys方法，返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键名。
        // var obj = { foo: 'bar', baz: 42 };
        // Object.keys(obj)
        // ["foo", "baz"]
        
        // Object.entries()
        // Object.entries()方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对数组。
        // const obj = { foo: 'bar', baz: 42 };
        // Object.entries(obj)
        // [ ["foo", "bar"], ["baz", 42] ]
        function maxNum1(str){
            // 转字符串
            if(typeof(str) !== 'string') str = str.toString();
            // 定义 obj
            let obj = {},
                maxChar = []; // 使用数组保存出现最多次的某些字符

            // 将字符串转成数组 , 进行遍历
            str.split('').forEach( (val) => {
                // 判断 obj 中 , 是否有当前的值
                if(!obj[val]){
                    // 没有就将值 当 key , 值为1 新增进去 {a:1} 
                    obj[val] = 1;
                }else{
                    // 否则就++ {a:2}
                    obj[val]++;
                }
            })  

            // 选取数组最大的值(this, Object.values(obj))
            let maxCount =  Math.max.apply(null, Object.values(obj))
            // forEach方法总是返回 undefined 且 没有办法中止或者跳出 forEach 循环。
            // console.log(Object.entries(obj));
            Object.entries(obj).forEach( item => {
                // console.log(item)
                if(item[1] == maxCount){
                    maxChar.push(item[0])
                }
            })
            return maxChar;
        }
        // console.log(maxNum1('asdfghjklsdflkjsalkfjsaldjfsdfjasfjsadflksajflaslkdfjasdkfssfsdfsdfsdfsdf'));
        
        function myMaxNum(str){
            str = str + '';
            var newArr = str.split('');

            var json = [];

            for(var i=0;i<newArr.length;i++){
                if(json[newArr[i]]){
                    json[newArr[i]]+=1;
                }else {
                    json[newArr[i]] = 1;
                }
            }

            var num = 0;
            var number = "";

            for(var k in json){

                // json[k] => value
                // {a:18}  => 18
                if(json[k]>num){
                    // 做比较 获取最大 value
                    num = json[k];
                    // 得出 key
                    number = k;
                }
            }

            return number

        }
        // var result = myMaxNum('qwerq');
        

        // 数组扁平化
        // 数组的扁平化，就是将一个嵌套多层的数组 array (嵌套可以是任何层数)转换为只有一层的数组。
        // 实现方法：Array.prototype.flatten(depth)，参数depth表示需要扁平化的层数，返回一个新的数组。
        function flatten1(ary){
            let tem = [],
                i = 0,
                len = ary.length;
            while(i < len){
                if(Array.isArray(ary[i])){
                    // 递归进行上面步骤
                    // [].concat(...ary)，它的参数可以为数组或值，作用为将数组或值连接成新数组。
                    tem = tem.concat(flatten1(ary[i]))
                }else{
                    tem.push(ary[i]);
                }
                i++;
            }
            return tem;
        }

        // console.log(flatten1([1,2,3,[4,5,6,[7,8,9,[10]]]]));
        
        var num = [1,2,3,4,5];
        var res = num.reduce(function(total,num){
            // console.log(num) 
            return total+num;
            //return total + Math.round(num);//对数组元素四舍五入并计算总和
        },0);
        // console.log(res);

        function flatten2(ary){
            return ary.reduce((pre, cur) => {
                // console.log(cur);
                return pre.concat(Array.isArray(cur) ? flatten2(cur) : cur)
            }, [])
            
        }

        // console.log(flatten2([1,2,3,[4,5,6,[7,8,9,[10]]]]));
        
        // 方法三（转化为字符串）
        function flatten3(ary){
            return ary.toString().split(',')
        }
        // console.log(flatten3([1,2,3,[4,5,6,[7,8,9,[10]]]]));
        

        // 数组中最大差值
        function getMaxProfit1(ary){
            return Math.max.apply(null, ary) - Math.min.apply(null, ary);
        }
        // console.log(getMaxProfit1([1,2,3,4,5,6,78,9]));
        

        // 判断是否为质数（prime number）素数
        // 质数：只能被1和自己整除且大于1的数。
        function isPrimeNumber1(n){
            if(n < 2) return false;
            if(n === 2) return true; // 最小的质数
            for(let i = 2; i < n; i++){
                if(n % i === 0){
                    return false;
                }
            }
            return true;
        }
        // console.log(isPrimeNumber1(11));

        // 金额转大写
        function money2Chinese(num) {
          if(!typeof num) throw new Error('参数为数字')
          let strOutput = ""
          let strUnit = '仟佰拾亿仟佰拾万仟佰拾元角分'
          num += "00"
          const intPos = num.indexOf('.')
          if (intPos >= 0) {
            num = num.substring(0, intPos) + num.substr(intPos + 1, 2)
          }
          strUnit = strUnit.substr(strUnit.length - num.length)
          for (let i = 0; i < num.length; i++) {
            strOutput += '零壹贰叁肆伍陆柒捌玖'.substr(num.substr(i, 1), 1) + strUnit.substr(i, 1)
          }
          
          return strOutput.replace(/零角零分$/, '整').replace(/零[仟佰拾]/g, '零').replace(/零{2,}/g, '零').replace(/零([亿|万])/g, '$1').replace(/零+元/, '元').replace(/亿零{0,3}万/, '亿').replace(/^元/, "零元");
        }
        // money2Chinese(1)
        console.log(money2Chinese(1990))
    </script>
</body>
</html>
```
- 图像优化原理
    + https://juejin.im/post/5bfe00e7e51d456f4f2c8860
- 前端工程基础
    + https://juejin.im/entry/55de6f5f60b271314aed0917
- vue3-cli
    + https://juejin.im/post/5bfb3da25188251a82660fed

## 2018-11-29

- waiper 实现商品滚动
    + http://bbs.swiper.com.cn/forum.php?mod=viewthread&tid=1284
```javascript
$(function(){

                // 无缝滚动
                var swiper = new Swiper('.swiper-container', {
                    speed:6000,
                    autoplay:{
                         delay: 1,
                    },
                    slidesPerView: 5, // 显示个数
                    spaceBetween: 50, // 间隔
                    grabCursor : true,    // 是否为手装
                    loop : true,  // 无线循环
                    freeMode:true,
                });

                // 鼠标滑过悬停  离开开启
                $(".swiper-container").mouseenter(function () {
                    swiper.autoplay.stop();
                }).mouseleave(function(){
                    swiper.autoplay.start();
                });



                // 实力展示轮播 公司简介 店铺公告 经销商说明
                var swiper_company_profile = new Swiper('.swiper-company-profile', {
                    simulateTouch : false, // 禁止鼠标触摸
                });

                $('.nav-btn').mouseenter(function(){
                    var that = this;
                    // 获取id
                    var id = this.dataset.id;

                    // 跳转指定
                    swiper_company_profile.slideTo(id, 1000,show());//切换到第一个slide，速度为1秒

                    // 回调函数不能直接写在 后面 , 只能
                    function show(){
                        $('.nav-btn').removeClass('right-nav-active');
                        $(that).addClass('right-nav-active');
                    }

                })


                // 实力展示轮播 无缝滚动
                var swiper_company_footer = new Swiper('.swiper-company-footer', {
                    speed:1000,
                    autoplay:{
                         delay: 1000,
                    },
                    slidesPerView: 4, // 显示个数
                    spaceBetween: 50, // 间隔
                    grabCursor : true,    // 是否为手装
                    loop : true,  // 无线循环
                    navigation: {
                      nextEl: '.swiper-button-next',
                      prevEl: '.swiper-button-prev',
                    },
                });

                 // 鼠标滑过悬停  离开开启
                $(".swiper-company-footer").mouseenter(function () {
                    swiper_company_footer.autoplay.stop();
                }).mouseleave(function(){
                    swiper_company_footer.autoplay.start();
                });

  
            })
```

# 2018-11-30

- PHP 上传视频
    + 原生 input 上传
 ```html
 <!-- enctype="multipart/form-data" -->
 <form action="" method="post" id="edit_from" enctype="multipart/form-data">
 <!-- type="file"  accept="video/*" -->
    <input name="video" id="video" type="file"  accept="video/*" />
 </form>
 ```
         * 上传失败提示码
             - PHP $_FILES error码对应错误信息
             - 0： 上传成功
             - 1：  上传文件超出php配置max_upload_filesize限制
             - 2： 上传文件超出html表单限制
             - 3： 文件只有部分被上传 
             - 4： 没有上传文件
             - 6： 没有找不到临时文件夹 
             - 7： 文件写入失败（可能是文件权限不足）
             - 8： php文件上传扩展file没有打开 
         * 解决错误代码 1
             - php 上传大文件——配置upload_max_filesize和post_max_size 
             - http://blog.sina.com.cn/s/blog_16698a9a40102yai4.html
             - 在查看程序中有没有限定 上传文件大小的配置
             - 有就修改
 - PHP 模糊查询
     + https://www.cnblogs.com/jpfss/p/6944245.html
 - PHP 左链接
     + https://blog.csdn.net/plg17/article/details/78758593
     + https://blog.csdn.net/plg17/article/details/78758593
     ```php
$re_count = $db->getOne("SELECT COUNT(*) FROM {$config->db_prefix}article_info as a LEFT JOIN {$config->db_prefix}article_cat as c ON a.cat_id=c.cat_id WHERE parent_id in(SELECT cat_id FROM {$config->db_prefix}article_cat WHERE cat_name='案例视频') and 1  {$where}");
     ```

 # 2018-12-6

- 效率
    + 增加专注力
    + 快速编写代码
    + 以免加班
- 小程序音频组件
    + 第一种
        + https://developers.weixin.qq.com/miniprogram/dev/component/audio.html
        + auido 不支持 iphone 
        + 如果坚持要用 audio , 自己写两个按钮,对应播放/暂停事件
    - 第二种
        + https://developers.weixin.qq.com/miniprogram/dev/api/wx.createInnerAudioContext.html
        + 自己创建按钮来控制事件播放
    
```html
<block wx:if="{{audio_path}}">
    <audio name="{{title}}" author="趣儿养" src="{{audio_path}}" id="myAudio" controls="{{true}}"></audio>
    <view class="audio_btn">
        <view>
            <van-button size="small" plain type="danger" bind:click="audioPause" custom-class="audio_pause">暂停</van-button>
        </view>
        <view>
            <van-button size="small" plain type="primary" bind:click="audioPlay" custom-class="audio_play">播放</van-button>
        </view>
        
    </view>
    
</block>

<script>
    onLoad:function(){
        // audio id
        o.audioCtx = wx.createAudioContext('myAudio');
    },
    audioPlay: function (e) {
        // 开始播放
        this.audioCtx.play()
    },
    audioPause: function (e) {
        // 暂停播放
        this.audioCtx.pause()
    },
    // 第二种方法,创建开始/暂停按钮
    const test = wx.createInnerAudioContext();

    // url
    test.src = t.data.audio_path;
    // 自动播放
    test.autoplay = true;
    
</script>
```