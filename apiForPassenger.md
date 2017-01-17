FORMAT: 0.0.1

# tips
此api仅用于乘客端，api调用的接口地址(url)请@oeil补充完整

# 用户登陆模块
用于用户登陆的api

## 请求验证码[/url]
将验证码以短信的形式发送到用户的手机，用于用户登陆系统

+Request (json)

	{
		"phone" : 12345678901		//phone为11位数字
		"timestamp"	: 1484635014000	//timestamp精确到毫秒
	}

+Response (json)
	
	{
		"status" :0/1	//0为发送失败，1为发送成功
	}

## 请求登陆[/url]
用户发送登陆请求，登陆系统

+Request (json)

	{
		"phone" : 12345678901
		"code"	: 123456		//验证码为6位数字
	}

+Response (json)

	{
		"status" 	: 0/1	//0为登陆失败，1为登陆成功
		"token"		:	格式由@oeil确认
	}