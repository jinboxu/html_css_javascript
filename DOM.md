#### DOM

**参考文档： https://www.cnblogs.com/wupeiqi/articles/5643298.html**

文档对象模型（Document Object Model，DOM）是一种用于HTML和XML文档的编程接口。它给文档提供了一种结构化的表示方法，可以改变文档的内容和呈现方式。我们最为关心的是，DOM把网页和脚本以及其他的编程语言联系了起来。DOM属于浏览器，而不是JavaScript语言规范里的规定的核心内容。 



#### 1. 找到标签

**a. 直接找**

>document.getElementById             根据ID获取一个标签
>
>document.getElementsByName          根据name属性获取标签集合
>
>document.getElementsByClassName     根据class属性获取标签集合
>
>document.getElementsByTagName       根据标签名获取标签集合

```
# 获取单个元素
document.getElementById('i1')

# 获取多个元素（列表）
document.getElementsByTagName('div')
document.getElementsByClassName('c1')
```



**b. 间接找**

>parentElement             // 父节点标签元素
>children                         // 所有子标签
>firstElementChild         // 第一个子标签元素
>lastElementChild          // 最后一个子标签元素
>nextElementtSibling     // 下一个兄弟标签元素
>previousElementSibling  // 上一个兄弟标签元素



#### 2. 操作

**a.  innerText**

> - 获取标签中的文本内容 :  ```标签.innerText```
>
> - 对标签内部文本重新赋值 : ```标签.innerText="..."```



**b. class操作**

> className                   //获取所有类名
>
> classList.remove(cls)   //删除指定类
>
> classList.add(cls)         //添加类



**c.  checkbox**

>获取值(true/false)
>
>checkbox对象.checked
>
>设置值
>
>checkbox对象.checked = true



---

**示例讲解**

#### 3.模态对话框 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .hide{
            display: none;
        }
        .c1{
            position: fixed;
            left: 0;
            top: 0;
            right: 0;
            bottom: 0;
            background-color: black;
            opacity: 0.6;
            z-index: 9;
        }
        .c2{
            width: 500px;
            height: 400px;
            background-color: white;
            position: fixed;
            left: 50%;
            top: 50%;
            margin-left: -250px;
            margin-top: -200px;
            z-index: 10;
        }
    </style>
</head>
<body style="margin: 0;">

    <div>
        <input type="button" value="添加" onclick="ShowModel();" />
        <input type="button" value="全选" onclick="ChooseAll();" />
        <input type="button" value="取消" onclick="CancleAll();" />
        <input type="button" value="反选" onclick="ReverseAll();" />

        <table>
            <thead>
                <tr>
                    <th>选择</th>
                    <th>主机名</th>
                    <th>端口</th>
                </tr>
            </thead>
            <tbody id="tb">

                <tr>
                    <td>
                        <input type="checkbox" />
                    </td>
                    <td>1.1.1.1</td>
                    <td>190</td>
                </tr>
                <tr>
                    <td><input type="checkbox"f id="test" /></td>
                    <td>1.1.1.2</td>
                    <td>192</td>
                </tr>
                <tr>
                    <td><input type="checkbox" /></td>
                    <td>1.1.1.3</td>
                    <td>193</td>
                </tr>
            </tbody>
        </table>
    </div>

    <!-- 遮罩层开始 -->
    <div id="i1" class="c1 hide"></div>
    <!-- 遮罩层结束 -->

    <!-- 弹出框开始 -->
    <div id="i2" class="c2 hide">
        <p><input type="text" /></p>
        <p><input type="text" /></p>
        <p>
            <input type="button" value="取消" onclick="HideModel();"/>
            <input type="button" value="确定"/>

        </p>

    </div>
    <!-- 弹出框结束 -->

    <script>
        function ShowModel(){
            document.getElementById('i1').classList.remove('hide');
            document.getElementById('i2').classList.remove('hide');
        }
        function HideModel(){
            document.getElementById('i1').classList.add('hide');
            document.getElementById('i2').classList.add('hide');
        }

        function ChooseAll(){
            var tbody = document.getElementById('tb');
            // 获取所有的tr
            var tr_list = tbody.children;
            for(var i=0;i<tr_list.length;i++){
                // 循环所有的tr，current_tr
                var current_tr = tr_list[i];
                var checkbox = current_tr.children[0].children[0];
                checkbox.checked = true;

            }
        }

        function CancleAll(){
            var tbody = document.getElementById('tb');
            // 获取所有的tr
            var tr_list = tbody.children;
            for(var i=0;i<tr_list.length;i++){
                // 循环所有的tr，current_tr
                var current_tr = tr_list[i];
                var checkbox = current_tr.children[0].children[0];
                checkbox.checked = false;

            }
        }

        function ReverseAll(){
            var tbody = document.getElementById('tb');
            // 获取所有的tr
            var tr_list = tbody.children;
            for(var i=0;i<tr_list.length;i++){
                // 循环所有的tr，current_tr
                var current_tr = tr_list[i];
                var checkbox = current_tr.children[0].children[0];
                if(checkbox.checked){checkbox.checked = false;}else{checkbox.checked = true;}}}

    </script>
</body>
</html>
```



![DOM1](pictures\DOM1.png)

>- .hide : 默认使遮罩和弹出框隐藏
>- ShowModel()  , HideModel()函数 :  点击"添加" 和"取消"hide属性
>- ChooseAll() , CancelAll()函数 : 找到tbody标签下的所有的checkbox对象并设置值
>- ReverseAll()函数 : 在上面两个函数的基础上加个判断



#### 4. 左侧管理菜单

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .hide{
            display: none;
        }
        .item .header{
            height: 35px;
            background-color: #2459a2;
            color: white;
            line-height: 35px;
        }
    </style>
</head>
<body>
    <div style="height: 48px"></div>

    <div style="width: 300px">

        <div class="item">
            <div id='i1' class="header" onclick="ChangeMenu('i1');">菜单1</div>
            <div class="content">
                <div>内容1</div>
                <div>内容1</div>
                <div>内容1</div>
            </div>
        </div>
        <div class="item">
            <div id='i2' class="header" onclick="ChangeMenu('i2');">菜单2</div>
            <div class="content hide">
                <div>内容2</div>
                <div>内容2</div>
                <div>内容2</div>
            </div>
        </div>
        <div class="item">
            <div id='i3' class="header" onclick="ChangeMenu('i3');">菜单3</div>
            <div class="content hide">
                <div>内容3</div>
                <div>内容3</div>
                <div>内容3</div>
            </div>
        </div>
        <div class="item">
            <div id='i4' class="header" onclick="ChangeMenu('i4');">菜单4</div>
            <div class="content hide">
                <div>内容4</div>
                <div>内容4</div>
                <div>内容4</div>
            </div>
        </div>



    </div>

    <script>
        function ChangeMenu(nid){
            var current_header = document.getElementById(nid);

            var item_list = current_header.parentElement.parentElement.children;

            for(var i=0;i<item_list.length;i++){
                var current_item = item_list[i];
                current_item.children[1].classList.add('hide');
            }

            current_header.nextElementSibling.classList.remove('hide');
        }
    </script>
</body>
</html>
```

> ChangeMenu(nid)函数 :  将当前的id通过参数传给函数，首先通过循环将所有的"内容"隐藏，最后将该id的"内容"显示出来

