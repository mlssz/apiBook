FORMAT: 1A

# MLSSZ API

此api仅用于乘客端，api调用的接口地址(url)请@oeil补充完整

- 用户服务器地址：https://www.oeli.pub:80/haoyun/s/
- 地图服务器地址：http://115.159.155.229:8123/

# Group Rental用户模块

用于用户登录的api

## Rental登录 [/rent/login.json]

用户发送登录请求，登录系统

### 请求登录 [POST]

+ Request <Success> (application/json)

        {
            "account": "12345678901",
            "position": "x,y",
            "timestamp": 1484635014000
        }

+ Response 200 (application/json)

    {
        "status": 1,//0为登录失败，1为登录成功
        "rental": {
            "id": 1,
            "account": "17764591386",
            "name": "无名",
            "registTime": "1487858596000",
            "lastlogin": "1487858596000",
            "token": "c671e0a32b42419e84f8023a4d0ca5dd8e4d7312cdd5449a857da7e269398d38",
            "type": 1,
            "positionX": 128.6846866,
            "positionY": 12.6146,
            "score": "0"
        }
    }

+ Request <Failed> (application/json)

        {
            "account": "12345678901",
            "position": "x,y",
            "timestamp": "1484635014000"
        }
    
+ Response 200 (application/json)

        {
            "status": "0",//0为登录失败，1为登录成功
            "msg": "失败的原因"//格式由@oeil确认
        }



# Group 地图模块

用于位置操作的api

## 显示租车人附近的汽车 [GET /rent/{uid}/near_lessees{?token, positionx, positiony, limit}]

根据租车人与货车主的经纬度，获取租车人附近的货车主们。

+ Parameters
    + uid (number, required) - 用户id
    + token (string, required) - 用户token
    + positionx (number, required) - 用户经度值
    + positiony (number, required) - 用户维度值
    + limit: `20` (number, required) - 范围，单位米(M)

+ Response 200 (application/json)

        [
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
          },
        ]

+ Response 403 (application/json)

        // 没有权限
        {
            "detail":"身份认证信息未提供。"
        }

## 上传客户相关信息 [/rent/upload]

文件大小不得超过1M，编码为UTF-8

### 上传 [POST]

+ Request <success> (text/html)

    //type 有 身份证(sfz)、车牌(cp)、车辆登记证书(djz)、驾驶证(jsz)、车辆正面照(zmz)、头像(head)
    {
        "uid":0,
        "token":"",
        "type":""，
        "file":file //enctype="multipart/form-data"
    }

+ Response 200 (application/json)

    //成功
    { 
        "status": 1
    }
    //失败
    {
        "status":0,
        "msg":""
    }

## 下载证件照片 [/rent/download]

### 下载 [GET]

+ Request <success> (text/html)

    //type 有 身份证(sfz)、车牌(cp)、车辆登记证书(djz)、驾驶证(jsz)、车辆正面照(zmz)、头像(head)
    {
        "uid":0,
        "token":"",
        "type":""
    }

+ Response 200 (file)

    //成功
    文件流
    //失败
    错误信息
