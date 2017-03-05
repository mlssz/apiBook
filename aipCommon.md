aipCommon
# MLSSZ API
通用api

# Group Socket

## 更新位置信息 [/url]

建立websocket链接，实时更新自身的位置信息，即经纬度，并返回自身信息

+ Parameters
    + uid (number, required) - 用户id
    + token (string, required) - 用户token
    + positionx (number, required) - 用户经度值
    + positiony (number, required) - 用户维度值

+ Response 200 (application/json)

      {
        "user": {
          "id":1,
          "account":"17764591386",
          "name":"无名",
          "signup_time":"1487858596000",
          "pre_login_time":"1487858596000",
          "token":"c671e0a32b42419e84f8023a4d0ca5dd8e4d7312cdd5449a857da7e269398d38",
          "type":2,
        },
        "positionX":128.6846866,
        "positionY":12.6146,
        "score":"0"
      }

+ Response 403 (application/json)

        // 没有权限
        {
            "detail":"身份认证信息未提供。"
        }

# Group Order

## 获取订单列表 [/url]

用户获取自己的订单列表

+ Parameters
    + uid (number, required) - 用户id
    + token (string, required) - 用户token

+ Response 200 (application/json)

	订单具体格式见数据库设计
	[{
		Order
	}]

+ Response 403 (application/json)

    // 没有权限
    {
        "detail":"身份认证信息未提供。"
    }

## 完成订单状态 [/url]

用于完成订单等

+ Parameters
    + uid (number, required) - 用户id
    + token (string, required) - 用户token
	+ orderid (number,required) - 订单id


+ Response 200 (application/json)

	订单具体格式见数据库设计
	{
		Order
	}

+ Response 403 (application/json)

    // 没有权限
    {
        "detail":"身份认证信息未提供。"
    }
	//完成订单失败
	{
		"detail": "订单完成失败，订单(已完成、未接单)"
	}

## 取消订单 [/url]

用于取消订单

+ Parameters
    + uid (number, required) - 用户id
    + token (string, required) - 用户token
	+ orderid (number,required) - 订单id


+ Response 200 (application/json)

	订单具体格式见数据库设计
	{
		Order
	}

+ Response 403 (application/json)

    // 没有权限
    {
        "detail":"身份认证信息未提供。"
    }
	//完成订单失败
	{
		"detail": "订单取消失败，订单(已完成、已接单、司机未同意等)"
	}