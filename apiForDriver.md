FORMAT: 1A

# MLSSZ API

货车司机API说明文档

- 服务器地址 http://www.oeli.pub/s

# 货车司机用户组

## 注册 [/lessee/regist]

### 请求注册 [POST]

+ Request <success> (text/html)

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

## 完成个人信息 [/lessee/finishmyinfo]

### 请求完成个人信息 [POST]

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

## 登陆 [/lessee/regist]

### 请求登陆 [POST]

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

## 货车 [/lessee/addatruck]

### 添加一个货车 [POST]

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


## 货车 [/lessee/findmytrucks]

### 查看自己的货车列表 [POST]

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