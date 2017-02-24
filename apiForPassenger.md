FORMAT: 0.0.1

# tips
此api仅用于乘客端，api调用的接口地址(url)请@oeil补充完整

# 用户登录模块
用于用户登录的api

## 请求验证码[/url]
将验证码以短信的形式发送到用户的手机，用于用户登录系统

+Request (json)

	{
		"phone" : 12345678901,			//phone为11位数字
		"timestamp"	: 1484635014000,	//timestamp精确到毫秒
	}

+Response (json)
	
	{
		"status" :0\1,	//0为发送失败，1为发送成功
	}

## 请求登录[/haoyun/s/rent/login.json]
用户发送登录请求，登录系统

+Request (json)

	{
		"account" : 12345678901,
		"position"	: x,y,
		"timestamp"	: 1484635014000
	}

+Response (json)
成功：
	{
		"status" 	: 1,	//0为登录失败，1为登录成功
		"rental"	:{"id":1,"account":"17764591386","name":"无名","registTime":1487858596000,"lastlogin":1487858596000,"token":"c671e0a32b42419e84f8023a4d0ca5dd8e4d7312cdd5449a857da7e269398d38","type":1,"position":"128,123","score":0}
	}
失败:
	{
		"status" 	: 0,	   //0为登录失败，1为登录成功
		"msg"		: 失败的原因	//格式由@oeil确认
	}