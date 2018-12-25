# 提升效率 提高个人形象

简洁，高效，装逼

## 效率

### 基础PC快捷键

- 逐词移动光
    + Ctrl + → 快速词语移动
    + ctrl + shift + →  = 逐词选中
- 将光标移到开头/结尾
    + Home
    + End
        + 好是好就是距离有点远
    + shift + Home = 选中
    + shift + End = 选中
- 选中当前行
    + Ctrl + L
- 缩进
    + Ctrl + [ / ]
- 向上移动一整行
    + ctrl shift + 上/下 
- 复制当前行到下一行
    + ctrl+shift+d

### sublime

- 切换标签
    + alt + 数字(代表第几个标签)
- 加光标
    + ctrl + 点击
- 选择相同的词
    + ctrl + d
- 向下插行
    + ctrl + enter
- 向上插行
    + ctrl + shift + enter
- 创建5个div类名为box、内容为1-5
    + 输入：div.box{$}5

### HBuilder X

- 光标向左
    + alt + j (左)
    + alt + h (右)
    + atl + k (上)
    + atl + j (下)
- 切换标签
    + alt + 数字(代表第几个标签)
- 整理代码
    + crtl + k
- 找到定义(变量的出处)
    + alt + 鼠标点击
- 加光标
    + ctrl + 点击
- 选择相同的词语
    + crti + e
- 选择首行光标
    + ctrl + shift + /
- 快速创建包围(标签)<></>
    + ctrl + ]
- 扩大包围
    + ctrl + =
- 新建标签卡
    + ctrl + t
- 关闭标签卡
    + ctrl + w
- 向下插行
    + ctrl + enter
- 向上插行
    + ctrl + shift + enter
- 上移一行
    + ctrl + up / down
- 删除整行
    + ctrl + d
- 变成大写
    + alt + shift + u
- 变成小写
    + alt + shift + l
- 光标到上个段落
    + ctlr + alt + PageUp
- 光标到下个段落
    + ctrl + alt + PageDown
- 设置标签/取消
    + ctrl + f2
- 下一个书签
    + f2
- 垂直滚动一屏
    + shift + 滚轮
- 交换选区内容
    + Ctrl+Shift+x
        * 双击第1个style属性后的引号内侧，可选中引号内容。
        * 按下Ctrl后继续双击第2个style属性后的引号内侧，可选中2个引号内的选区。
        * 按下Ctrl+Shift+x，交换style属性的内容。



## 代码风格指南

- 异步请求,如成功码为 0 ;
```js
    const ScuucessCode = 0; 
    $.ajax({
        type:"GET",
        url:"",
        dataType:"json",
        success:function(data){
           if(data.code == ScuucessCode){

           }else{
            
           }
        }
    });

```