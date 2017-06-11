#acss使用记录
	
	//选择的文档资料
	http://www.ruanyifeng.com/blog/2012/06/sass.html

##无
	css预处理器 用一种专门的编程语言，进行网页样式设计，
	然后再编译成正常的CSS文件。
##有

	SASS是一种CSS的开发工具，提供了许多便利的写法，
	大大节省了设计者的时间，使得CSS的开发，变得简单和可维护。

	SASS提供四个编译风格的选项：
	nested：嵌套缩进的css代码，它是默认值。
	expanded：没有缩进的、扩展的css代码。
	compact：简洁格式的css代码。
	compressed：压缩后的css代码。

##基本用法

#####SASS允许使用变量，所有变量以$开头。
	　　$blue : #1875e7;　
	div {
	color : $blue;
	}
#####如果变量需要镶嵌在字符串之中，就必须需要写在#{}中
	$sude : left
	.bl{
		border-#{$side}-radius:5px;
	}
#####sass允许在代码中使用算式
	
	body{margin:(14px/2);top:50px + 100px; right:$var *10%}
#####sass允许选择器嵌套
	
	普通css里的
	div h1{}
	sass里的
	div{
		//可以嵌套很多
		h1{
		color:red;
		}
	}
#####属性嵌套

	写嵌套的时候就要写:号
	p{
		border:{
		color:red;
		}
	}
#####在嵌套的代码块里使用父元素可以写成

	a{
		&:hover{color:#ffb3ff;}
	}
##注释

	/**/标准注释 保留到编译后 压缩不保留
	//单行 只保留在sass源文件
	/*！*/重要注释 压缩也保留 
##继承性

	允许一个选择器，继承另一个选择器
	.class1{border:1px solid #ddd;}
	继承使用@extend
	.class2{
		@extend.class1;
		font-size:120%;
	}
##可以跟模板一样调用Mixin

	@mixin left{color:red;}
	使用@include命令调用mixin
	div{@include left;}
	//要点可以指定参数和缺省值（如函数的形参和实参）
	//形参
	@mimin left($value:10px){
		color:red;		
	}

	div{
		//实参
		@include left(20px);
	}
##颜色函数

	// lighten(#cc3, 10%) #d6d65c
	// d6d65cdarken(#cc3, 10%)  #a3a329
	// a3a329	grayscale(#cc3) #808080
	// 808080complement(#cc3) #33c
##插入文件

	插入一个外部文件
	@import 'path/filename.scss';
	
##条件语句

	if else 
	P{@if 1+1==2 {color:red}@else{color:blue}}
##循环语句

	for 语句支持
	　　@for $i from 1 to 10 {
	.border-#{$i} {
		border: #{$i}px solid blue;
	}
	}
	while 支持

	each 支持
	　　@each $member in a, b, c, d {
	.#{$member} {
	background-image: url("/image/#{$member}.jpg");
		}
	}
##自定义函数

	@function two($n){
	@return $n*2;
	}
	.sidebar{
	width:two(5px);
	}