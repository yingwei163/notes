#Laravel Elixir 扩展
****
##1.安装Node.js 

	https://nodejs.org/en/
	v6.10.3 LTS
	
##2.安装Gulp
	
	npm install --global gulp

##3.安装Laravel Elixir

	Laravel Elixir
	最后的步骤就是安装 Elixir！在每一份新安装的 Laravel 代码里，你会发现根目录有个名为 package.json 的文件。想像它就如同你的 composer.json 文件，只不过它定义的是 Node 的依赖扩展包，而不是 PHP 的。你可以使用以下的命令安装依赖扩展包：

	npm install
	如果你是在 Windows 系统上或在 Windows 主机系统上运行 VM 进行开发，你需要在运行 npm install 命令时将 --no-bin-links 开启：

	npm install --no-bin-links

	速度慢可以使用淘宝镜像
	npm install -g cnpm --registry=https://registry.npm.taobao.org
	安装完就可以使用cnpm

##SCSS
	
	文件扩展名不同：“.sass”和“.scss”；
	Sass是以严格缩进式语法规则来书写的，不带大括号和分号；而SCSS的语法和CSS书写语法类似。	
	安装介绍文档
	http://www.jianshu.com/p/fa379a309c8a
	方法一（通过命令安装sass）：打开命令终端，输入：gem install sass安装前需要先安装Ruby
	https://rubyinstaller.org/
	安装失败了不过laravel里的 resources/assets/sass自带

##最终使用


	用elixir调用Gulp对css进行压缩
	scss写完成后在laravel/gulpfile.js中编写
	elixir(function(mix) {
			//scss文件名
    mix.sass('app.scss');
	});
	这样可以吧sass文件编译成css文件 
	然后用gulp压缩成一个短CSS文件
##扩展在调用gulp watch 压缩的时候可以有一个回调函数
	如果你需要在 Elixir 调用一个既有的 Gulp 任务，你可以使用 task 方法。举个例子，假设你有一个 Gulp 任务，当你调用时会输出一些简单的文本：

	gulp.task('speak', function() {
    var message = 'Tea...Earl Grey...Hot';

    gulp.src('').pipe(shell('say ' + message));
	});
	如果你希望在 Elixir 中调用这个任务，使用 mix.task 方法并传递该任务的名称作为该方法唯一的参数：

	elixir(function(mix) {
    mix.task('speak');
	});