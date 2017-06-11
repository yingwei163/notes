##安装

环境要求：PHP >= 5.3.0

使用 composer

composer require "stoneworld/wechat"

手动安装

下载 本安装包

然后引入根目录的autoload.php即可：

把wechat/autoload.php导入laravel的autoload

require "wechat/autoload.php"; 
##使用
use 写好的类 传入对应调用参数

	$options = array(
            'token'=>'stoneworld1992',   //填写应用接口的Token
            'encodingaeskey'=>'o1wze3492xoUVIc9ccTLJczO3BQ5pLfiHcKwtDEdqM9',//填写加密用的EncodingAESKey
            'appid'=>'wx8ac123b21f5347',  //填写高级调用功能的appid
            'appsecret'=>'4ZDHIETJ6e0oENlEkRhYwzWPTdKcPcRjCkgQkuHtQTJ12ZhWHESowrJqS9', //填写高级调用功能的密钥
            'agentid'=>'5', //应用的id
        );

##服务器端给客户端发送消息为例

	<?php

	use Stoneowrld\Wechat\Server;

	$options = array(
            'token'=>'stoneworld1992',   //填写应用接口的Token
            'encodingaeskey'=>'o1wze3492xoUVIc9ccTLJczO3BQ5pLfiHcKwtDEdqM9',//填写加密用的EncodingAESKey
            'appid'=>'wx8ac123b21f5347',  //填写高级调用功能的appid
            'appsecret'=>'4ZDHIETJ6e0oENlEkRhYwzWPTdKcPcRjCkgQkuHtQTJ12ZhWHESowrJqS9', //填写高级调用功能的密钥
            'agentid'=>'5', //应用的id
        );

	$server = new Server($options);
	//选择监听消息 根据用户发来的消息进行判断
	$server->on('message', function($message){
	//给出返回值
    return "您好!";
	});
	//用法
	// 监听所有类型
	$server->on('message', function($message) {
    return Message::make('text')->content('您好！');
	});

	// 监听指定类型
	$server->on('message', 'image', function($message) {
    return Message::make('text')->content('我们已经收到您发送的图片！');
	});

	$result = $server->server();
	echo $result;
	
	// 您可以直接echo 或者返回给框架 直接echo给用户
	echo $server->serve();
##1.AccessToken.php获取并缓存TOken
	
	
	    public function __construct($appId, $appSecret)
    {
        $this->appId     = $appId;
        $this->appSecret = $appSecret;
        $this->cacheKey = $this->cacheKey.'.'.$appId;
        $this->cache     = new Cache($appId);
    }
	使用Token时传入企业ID应用secret
	然后调用方法 获取Token
	$new->getToken()就可以返回access_token 如果有缓存就返回缓存里的access_token
##Agent.php应用相当于开发文档应用一块

	传入企业ID和应用appsecret
	    public function __construct($appId, $appSecret)
    {
        $this->http = new Http(new AccessToken($appId, $appSecret));
    }
	get传入应用iD可以直接调用
	set传入要设置应用就要传入设置的属性 在开发者文档中看
	lists查看应用列表什么都不用传入
##Auth.php网页授权获取用户信息

	使用对象先传入，企业ID，应用secret
	第一个方法生成Url根据给入的信息获取登陆用户的code
	第二个方法直接跳转不获取用户参数
	第三个方法根据code获取用户的openid|userid
	第四个方法根据用户的openid|userid获取用户信息 然后跳转页面
	第五个方法userid转换成openid接口
##Authorize.php成员登录授权获取用户信息

	与Auth差不多使用
	传入企业ID应用secret
	直接调用authorize方法 可以跳转和获取用户信息
##Broadcast.php群发消息

	传企业ID应用secret
	1群发来源应用
	2准备消息 放入要发送的消息
	3消息群发 选择参数为发送的范围 传入3个参数全部 部门 标签
##Menu.php菜单设置

	构造 传企业ID应用secret获取access_token
	1set传入 应用ID 文档类似的菜单设置
	2get传入 应用ID
	3delete传入 应用ID
	server的event方法可以获得菜单点击的键通过监听来回送消息
##Media.php上传素材 
	