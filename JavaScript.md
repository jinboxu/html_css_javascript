## JavaScript

**参考文档： https://www.cnblogs.com/wupeiqi/articles/5602773.html**

**JS代码块需要放置在\<body\>标签内部的最下方**

#### 1. 注释

> 1. 注释
>
> 当行注释   //
>
> 多行注释   /*          */



> 2. 全局变量和局部变量
>
> name = 'alex';       全局变量
>
> var name='eric';        局部变量



> 3. 定时器
>
> setInterval('执行的代码', 间隔时间 )



欢迎滚动条:

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>欢迎滚动条</title>
</head>
<body>
	<div id="l1">欢迎老男孩莅临指导&nbsp;&nbsp;&nbsp;</div>

	<script type="text/javascript">
		function func() {
			//根据id获取指定标签的内容
			var tag = document.getElementById('l1');
			//获取标签内部的内容
			var content = tag.innerText;

			var f = content.charAt(0);
			var l = content.substring(1, content.length);

			var net_content = l + f;

			//重新赋值
			tag.innerText = net_content;
		}

		setInterval('func()', 500);
	</script>
</body>
</html>
```

