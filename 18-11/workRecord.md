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