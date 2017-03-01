FORMAT: 0.0.1

# tips
此api仅用于乘客端，api调用的接口地址(url)请@oeil补充完整

用户服务器地址：https://www.oeli.pub:80/haoyun/s/

# 用户登录模块
用于用户登录的api

## 请求登录[/rent/login.json]
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
			"id":1,
			"account":"17764591386",
			"name":"无名",
			"registTime":"1487858596000",
			"lastlogin":"1487858596000",
			"token":"c671e0a32b42419e84f8023a4d0ca5dd8e4d7312cdd5449a857da7e269398d38",
			"type":1,
			"positionX":128.6846866,
			"positionY":12.6146,
			"score":"0"
		}
	}

失败:

	{
		"status" 	: "0",	   //0为登录失败，1为登录成功
		"msg"		: "失败的原因"	//格式由@oeil确认
	}

# Group 地图模块
用于位置操作的api

## 租车人附近的汽车 [/rent/near_lessees{?uid, token, positionx, positiony, limit}]

### 显示所有附近汽车 [GET]

    GET /rent/near_lessees
    
+ Parameters
    + uid (number, required) - 用户id
    + token (string, required) - 用户token
    + positionx (number, required) - 用户经度值
    + positiony (number, required) - 用户维度值
    + limit (number, required) - 范围，单位米(M)

+ Response 200 (application/json)

	[{
		"id":1,
		"account":"17764591386",
		"name":"无名",
		"registTime":"1487858596000",
		"lastlogin":"1487858596000",
		"token":"c671e0a32b42419e84f8023a4d0ca5dd8e4d7312cdd5449a857da7e269398d38",
		"type":2,
		"positionX":128.6846866,
		"positionY":12.6146,
		"score":"0"
	}]
