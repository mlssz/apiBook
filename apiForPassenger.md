FORMAT: 0.0.1

# tips
此api仅用于乘客端，api调用的接口地址(url)请@oeil补充完整

用户服务器地址：https://www.oeli.pub:80

# 用户登录模块
用于用户登录的api

## 请求登录[/haoyun/s/rent/login.json]
用户发送登录请求，登录系统

+Request (json)

	{
		"account" : "12345678901",
		"position"	: "x,y",
		"timestamp"	: "1484635014000",
	}

+Response (json)

成功：

	{
		"status" 	: 1,	//0为登录失败，1为登录成功
		"rental"	:{
			"id":1,"account":"17764591386",
			"name":"无名",
			"registTime":"1487858596000",
			"lastlogin":"1487858596000",
			"token":"c671e0a32b42419e84f8023a4d0ca5dd8e4d7312cdd5449a857da7e269398d38",
			"type":1,
			"position":"128,123",
			"score":"0"
		}
	}

失败:

	{
		"status" 	: "0",	   //0为登录失败，1为登录成功
		"msg"		: "失败的原因"	//格式由@oeil确认
	}

# 地图模块
用于位置操作的api

##模糊查询位置[/url]

+Request (json)

	{
		"place" : "",		//输入的地点名称，如：杭州电子
		"token" : "token",
		timestramp : "1484635014000",
	}

+Response (array)

	[{
		"placeName":"",		//返回的地点名称，如：杭州电子科技大学生活区东门
		"position" :"X,Y" 	//返回的地点的经纬度
	},
	{
		"placeName":"",
		"position" :"X,Y"
	},
	...
	{
		"placeName":"",
		"position" :"X,Y"
	}]
