
# 趣儿养后台工功能开发

## 购买会员赠送指定商品

### 概述

后台-会员设置的时候选择赠送商品(商品模块已经写好).
用户在小程序里购买,支付.

### 思路

1. 后台要可以选择已创建商品
2. 可以添加删除
3. 用表格形式更直观
4. 小程序购买的时候模仿商城购买车,等于捆绑销售,买套餐
5. 调用商城购物车接口,完成下单
6. 支付完成后更新会员订单表,商品订单表

### 后台

服务器语言只会PHP , 所以继续使用PHP完成二次开发。
这次遇到的挑战是框架使用的是 `Yii` 很高兴，出了ThinkPHP 还能尝试其他框架。
PHP只会半桶水，又使用一个新的框架，试错，总是要的。
坑还是要踩的。

#### 基本使用

**MVC**

> - 和其他 PHP 框架类似，Yii 实现了 MVC（Model-View-Controller） 设计模式并基于该模式组织代码。

Yii 的 MVC 模式令我印象深刻，以前用 ThinkPHP 的时候 常常在 Controllers 里写代码，这是很不严谨（自我检讨）。

而 Yii 在这方面相对严格。让我学会使用 Models 。

View 使用的是 PHP 后缀的文件，一开始以为 html 找了挺久，最终还是求助于后端大神。

**路由**

> - 请求被解析成一个路由和关联的参数；
> - 路由相关的一个控制器动作被创建出来处理这个请求。

项目使用了美化路由，还没使用过基础，还是贴出来学习下。

```php
use yii\helpers\Url;

// 创建一个普通的路由URL：/index.php?r=post%2Findex
echo Url::to(['post/index']);

// 创建一个带路由参数的URL：/index.php?r=post%2Fview&id=100
echo Url::to(['post/view', 'id' => 100]);

// 创建一个带锚定的URL：/index.php?r=post%2Fview&id=100#content
echo Url::to(['post/view', 'id' => 100, '#' => 'content']);

// 创建一个绝对路径URL：http://www.example.com/index.php?r=post%2Findex
echo Url::to(['post/index'], true);

// 创建一个带https协议的绝对路径URL：https://www.example.com/index.php?r=post%2Findex
echo Url::to(['post/index'], 'https');
```

**CURD**

查询

```
Customer::find()->one();    此方法返回一条数据；

Customer::find()->all();    此方法返回所有数据；

Customer::find()->count();    此方法返回记录的数量；

Customer::find()->asArray()->one();    以数组形式返回一条数据；

Customer::find()->asArray()->all();    以数组形式返回所有数据；

Customer::find()->where($condition)->asArray()->orderBy('id DESC')->all();
```

更新

```
//update();
//runValidation boolen 是否通过validate()校验字段 默认为true 
//attributeNames array 需要更新的字段 
$model->update($runValidation , $attributeNames);  

//updateAll();
//update customer set status = 1 where status = 2
Customer::updateAll(['status' => 1], 'status = 2'); 

//update customer set status = 1 where status = 2 and uid = 1;
Customer::updateAll(['status' => 1], ['status'=> '2','uid'=>'1']);
```

删除

```
$model = Customer::findOne($id);
$model->delete();

$model->deleteAll(['id'=>1]);
```


批量插入

```
Yii::$app->db->createCommand()->batchInsert(UserModel::tableName(), ['user_id','username'], [
    ['1','test1'],
    ['2','test2'],
    ['3','test3'],   
])->execute();
```

查看执行

```
//UserModel 
$query = UserModel::find()->where(['status'=>1]); 
echo $query->createCommand()->getRawSql();
```

#### 还需提升

在这次项目中，感觉自己专注度不够集中，有点容易走神。效率偏低。

提高效率方法 

- 抛弃鼠标，用快捷键
- 对键盘了如指掌
- 打字速度够快
- 拥有快速debug能力
    + 优秀的程序员总能快速对程序进行debug，比新手快上一百倍可能并不是夸张的说法。这不仅仅是因为他们懂得的知识比新人们多，更是因为经过千锤百炼、千劫万难之后，他们找到了严格而有逻辑的方式进行debug、进行错误源头的寻找。所以，如果你还是个只能慢慢debug的新人，那么你接下来的任务就是不断写代码、解决错误，把经验积累到一定的量，然后期待debug速度质的飞跃。
- 先思考，再编程
- 使用好的编程风格
- 使用合适编辑器
- 对语言深入度

---

阅读别人代码还需要掌握方法。

- 代码只是软件工程中不大不小的一部分
    + 对于开发人员来说，更重要的是《需求分析》和《详细设计》。因此在阅读他人代码之前，首先理解此代码是满足什么需求、解决什么问题，使用了什么关键技术、选择了什么样的实现方式等。    有此基础，看代码时，布局了然于胸，有的放矢。    反之直接深入（特别是复杂的）代码，枝繁交错、伏线千里，很容易所谓"出不来了"，事倍功半。
- (如果有可能)拒绝阅读烂代码
    + 好的代码，思路清晰、（同样的复杂度下）更易厘清；健壮性好、受益匪浅；风格良好（如注释、排版）、赏心悦目；技巧丰富、常有拾缀。反之亦然..
- 流程、功能、细节
    + 先理解函数功能，组织起整个流程；再阅读函数内部的逻辑；如有强烈的需求，才去深入每一条语句。
- 画图
    + 无论是随手草图，还是漂亮的思维导图，对于理解流程都非常有益。人的内存有限，若不画图，易出现刚理解函数D、已忘了函数A的情况。
- 严待自己代码
    + 为后来的维护者留下优良的代码，是行善、更是树立个人形象。
    + 为半年后的自己留下优良的代码，以前挖的坑最后往往还是自己跳、且代价更大。

--- 

代码风格，我以前没注意过，开发时间都不不够用，代码风格我真的没思考过。
俗话说磨刀不误砍柴工，代码风格，一定要掌握。
良好代码风格是行善。。更是树立个人形象。

### 小程序

个人感觉小程序的适配做的很好，相比webApp，好的太多了。

客户第一个感觉是前端，展示。在样式上，在细节上，如果做的细致，完美一点，客户接纳程度会更高，也更好沟通。

作为第一批小程序的开发者，感觉连开发工具也没有琢磨透，有点不应该。

高效的使用调试工具开发效率会更高一点。

