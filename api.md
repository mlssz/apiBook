FORMAT: 1A

# MLSSZ API

此api仅用于乘客端，api调用的接口地址(url)请@oeil补充完整

- 用户服务器地址：http://www.oeli.pub:80/haoyun/s/
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
            "code": "" //验证码
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
            "code": "1484635014000"
        }
    
+ Response 200 (application/json)

        {
            "status": "0",//0为登录失败，1为登录成功
            "msg": "失败的原因"//格式由@oeil确认
        }
        
## 上传客户相关信息 [POST /rent/upload]

文件大小不得超过1M，编码为UTF-8

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

## 下载证件照片 [GET /rent/download]

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


# Group 地图模块

用于位置操作的api

## 显示租车人附近的汽车 [GET /rent/{uid}/near_lessees{?token, positionx, positiony, limit, cartype}]

根据租车人与货车主的经纬度，获取租车人附近的货车主们。

+ Parameters
    + uid (number, required) - 用户id
    + token (string, required) - 用户token
    + positionx (number, required) - 用户经度值
    + positiony (number, required) - 用户维度值
    + cartype: `2` (number, required) - 车辆类型
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
            "order_count": 23,
            "truck": "浙A00000", // 车牌号
            "distance": 200,   // 实际距离 200 （单位：米）
            "score":"0"
          },
        ]

+ Response 403 (application/json)

        // 没有权限
        {
            "detail":"身份认证信息未提供。"
        }
        
# Group 常用线路管理

## 获得一个用户所有的线路 [GET /line/getAllByUserId]

+ Request <success> (text/html)

        {
                "uid":0,
                "token":""
        }

+ Response 200 (application/json)

        //成功

        {
                "status":1,
                "lines":[]
        }

        //失败

        {
                "status":0,
                "msg":""
        }

## 获得该用户的一个线路详情 [GET /line/getOneById]

+ Request <success> (text/html)

        {
                "uid":0,
                "token":"",
                "id":0  //线路ID
        }

+ Response 200 (application/json)

        //成功

        {
                "status":1,
                "line":{}
        }

        //失败

        {
                "status":0,
                "msg":""
        }

## 删除一个线路 [GET /line/deleteOneById]

+ Request <success> (text/html)

        {
                "uid":0,
                "token":"",
                "id":0  //线路ID
        }

+ Response 200 (application/json)

        //成功

        {
                "status":1
        }

        //失败

        {
                "status":0,
                "msg":""
        }

## 更新用户的一个线路详情 [GET /line/updateOneById]

+ Request <success> (text/html)

        {
                "uid":0,
                "token":"",
                "id":0，
                "rental":0,
                "lessee":0,
                "startplace":"",
                "endplace":"",
                "center":"",
                "remark":""
        }

+ Response 200 (application/json)

        //成功

        {
                "status":1
        }

        //失败

        {
                "status":0,
                "msg":""
        }


# Group 订单管理
 
| state | verbose        |
|  :--- | ----:          |
|     0 | 系统选车订单   |
|     1 | 自主选车订单   |
|     2 | 长期订单       |
|     3 | 订单被接受     |
|     4 | 完成订单       |
|     5 | 订单未完成结束 |
|     6 | 预约订单       |

## 通过ID获得一个订单详情 [GET /order/getOneById]

+ Request <success> (text/html)

        {
                "uid":0,
                "token":"",
                "id":0
        }

+ Response 200 (application/json)

        //成功

        {
                "status":1,
                "order":{}
        }

        //失败

        {
                "status":0,
                "msg":""
        }

## 租车人获得自己所有订单详情 [GET /order/getRentalAll]

+ Request <success> (text/html)

        {
                "uid":0,
                "token":""
        }

+ Response 200 (application/json)

        //成功

        {
                "status":1,
                "orders":[]
        }

        //失败

        {
                "status":0,
                "msg":""
        }


## 司机获得自己所有订单详情 [GET /order/getLesseeAll]

+ Request <success> (text/html)

        {
                "uid":0,
                "token":""
        }

+ Response 200 (application/json)

        //成功

        {
                "status":1,
                "orders":[]
        }

        //失败

        {
                "status":0,
                "msg":""
        }


## 租车人新建一个订单 [GET /order/createOne]

+ Request <success> (text/html)

        {
                "uid":0,
                "token":"",
                "startplace":"",
                "startplacex":0,
                "startplacey":0,
                "endplace":"",
                "starttime":0,
                "status":0,
                "trucktype":0,
                "fee":0.0
        }

+ Response 200 (application/json)

        //成功

        {
                "status":1,
                "order":{}
        }

        //失败

        {
                "status":0,
                "msg":""
        }

## 司机查询附近的订单 [GET /order/getNearAll]

+ Request <success> (text/html)

        {
                "uid":0,
                "token":"",
                "placex":0.0,
                "placey":0.0,
                "radius":0.0  //范围多大的园半径，单位：米（m）
        }

+ Response 200 (application/json)

        //成功

        {
                "status":1,
                "orders":[]
        }

        //失败

        {
                "status":0,
                "msg":""
        }

## 系统接单中的司机抢单 [POST /order/lesseechoose]

+ Request (text/html)

        {
                "uid":0,
                "token":"",
                "orderid":0
        }

+ Response 200 (application/json)

        //成功

        {
                "status":1
        }

        //失败

        {
                "status":0,
                "msg":""
        }

## 自主接单中的司机抢单 [POST /order/rentchoose]

+ Request (text/html)

        {
                "uid":0,
                "token":"",
                "orderid":0
        }

+ Response 200 (application/json)

        //成功

        {
                "status":1
        }

        //失败

        {
                "status":0,
                "msg":""
        }

## 自主接单中的租车人查看订单状态 [POST /order/rentchoosestatus]

+ Request (text/html)

        {
                "uid":0,
                "token":"",
                "orderid":0
        }

+ Response 200 (application/json)

        //成功

        {
                "status":1,
                "lessees":[]
        }

        //失败

        {
                "status":0,
                "msg":""
        }

## 自主接单中的租车人选择司机 [POST /order/rentchoosealessee]

+ Request (text/html)

        {
                "uid":0,
                "token":"",
                "orderid":0,
                "lessee":0
        }

+ Response 200 (application/json)

        //成功

        {
                "status":1
        }

        //失败

        {
                "status":0,
                "msg":""
        }

## 租车人确认货物到达目的地 [GET /order/confirmOne]

+ Request <success> (text/html)

        {
                "uid":0,
                "token":"",
                "orderid":0,
                "score":0,
                "remark":""
        }

+ Response 200 (application/json)

        //成功

        {
                "status":1,
                "orders":[]
        }

        //失败

        {
                "status":0,
                "msg":""
        }


# Group 货车司机用户组

## 请求注册 [POST /lessee/regist]

+ Request <success> (text/html)

        {
                "phone":12345678910,
                "password":"sdafsad",
                "positionx":0,
                "positiony":0,
                "code":"" //验证码
        }

+ Response 200 (application/json)

    //成功
    
        {
            "lessee": {
                "id": 23, 
                "account": "17764591382", 
                "name": "无名", 
                "registTime": 1488425454000, 
                "lastlogin": 1488425454000, 
                "token": "9c37255a9beb420893125c54d1269dc03e09d4663d2c4b6085f83503b840f8cc", 
                "type": 4, 
                "positionX": 21.23443, 
                "positionY": 32.56, 
                "score": 0, 
                "realName": "", 
                "ci": "", 
               "password": ""
            }, 
            "status": 1
        }
    
    //失败
    
    {
        "status":0,
        "msg":""
    }


## 请求完成个人信息 [POST /lessee/finishmyinfo]

+ Request <success> (text/html)

        {
            "uid":0,
            "token":"",
            "nickname":"",
            "realname":"",
            "ci":""
        }

+ Response 200 (application/json)

    //成功
    
        {
            "lessee": {
                "id": 23, 
                "account": "17764591382", 
                "name": "oeli", 
                "registTime": 1488425454000, 
                "lastlogin": 1488425454000, 
                "token": "9c37255a9beb420893125c54d1269dc03e09d4663d2c4b6085f83503b840f8cc", 
                "type": 4, 
                "positionX": 21.23443, 
                "positionY": 32.56, 
                "score": 0, 
                "realName": "事物", 
                "ci": "511622199608324566", 
                "password": ""
        }, 
        "status": 1
    }

    //失败
    
        {
            "status":0,
            "msg":""
        }

## 请求登陆 [POST /lessee/login]

+ Request <success> (text/json)

        {
            "phone":12345678910,
            "password":"sdafsad",
            "positionx":0,
            "positiony":0,
            "code":""
        }

+ Response 200 (application/json)

    //成功
    
        {
            "lessee": {
                "id": 16, 
                "account": "17764591381", 
                "name": "无名", 
                "registTime": 1488379162000, 
                "lastlogin": 1488379162000, 
                "token": "f520338fb5b64f05b3baf86a200cdd91d8c595e75f22461dbf2fd46761b558cc", 
                "type": 4, 
                "positionX": 232, 
                "positionY": 324, 
                "score": 0, 
                "realName": "", 
                "ci": "", 
                "password": ""
            }, 
            "status": 1
        }
    
    //失败
    
        {
            "status":0,
            "msg":""
        }


## 添加一个货车 [POST /lessee/addatruck]

货车类型：

| car tpye | comment  |
|   :----- | :------: |
|        0 | 小型货车 |
|        1 | 大型货车 |
|        2 | 小型平板 |
|        3 | 中型平板 |
|        4 | 大型平板 |

+ Request <success> (text/html)

        {
            "uid":0,
            "token":"",
            "no":"",
            "load":0,
            "width":0,
            "height":0,
            "length":0,
            "type":0,
            "moreinfo":"",
            "remark":""
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


## 查看自己的货车列表 [POST /lessee/findmytrucks]

+ Request <success> (text/html)

        {
            "uid":0,
            "token":""
        }

+ Response 200 (application/json)

    //成功
    
        {
            "trucks": [
                {
                    "id": 2, 
                    "lessee": 1, 
                    "no": "asuifia", 
                    "loads": 556, 
                    "width": 1232.234, 
                    "height": 0, 
                    "length": 213, 
                    "type": 4, 
                    "moreinfo": "sadasd", 
                    "remark": "sdfdsf"
                }, 
                {
                    "id": 3, 
                    "lessee": 1, 
                    "no": "asuifia", 
                    "loads": 556, 
                    "width": 1232.234, 
                    "height": 0, 
                    "length": 213, 
                    "type": 4, 
                    "moreinfo": "sadasd", 
                    "remark": "sdfdsf"
                }
            ], 
            "status": 1
        }
    
    //失败
    
        {
            "status":0,
            "msg":""
        }


## 上传货车相关信息 [POST /lessee/upload]

文件大小不得超过1M，编码为UTF-8

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

## 下载证件照片 [GET /lessee/download{?uid, token, type}]

+ Parameters
    + uid (number, required) - 用户id
    + token (string, required) - 用户token
    + type (string, required) - 身份证(sfz)、车牌(cp)、车辆登记证书(djz)、驾驶证(jsz)、车辆正面照(zmz)、头像(head)

+ Response 200 (file)

    //成功
    文件流
    //失败
    错误信息

## 语音验证码 [POST /yzm/yuyin/{type}]

{type}是一个自定义字符，依据调用api的名字来输入，如果是登陆会用到/lessee/regist，那么{type}用regist替换

+ Request <success> (text/html)

        {
            "phone":0 //电话号码
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
