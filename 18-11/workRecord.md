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
