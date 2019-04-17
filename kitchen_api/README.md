# 大神厨房APP接口文档
```
注意事项 
1、加密key ：8Klr!;tey#3{O/dT9>H)H_*qlt(G$LHq|zF{YlH@3M_6iSn    （生成签名所需）

2、每次发送请求   需生成  checksum  字段
         生成checksum（签名字段）要求：
         1、增加key字段进行签名    
         2、（所有字段）  按照键名对关联数组进行升序排序
         3、使用md5 加密
         4、把所有字符转换为小写

3、全部使用 post请求

4、全局参数
        reqCode   【请求码  110000-119999】
        checksum   【签名】
        reqTime   【请求时间，毫秒单位】
        mobile_id   【等同与  token】

5、用户安全参数
        session_id   【登陆标识】	
        session_security   【安全校验码】
```

## 请求地址
```
接口开始

测试地址: http://kitchenapi.marketing.ypvpa.com

线上地址：http://kitchenapi.marketing.yuqg.com          

```

## 状态码
> **状态码说明**
```
responseCode        响应状态 
responseMessage     响应信息
data                响应数据 具体参考其接口文档
```
> **responseCode返回状态码**
```
0                   成功
30001,              错误
//客户端错误
10001,              参数错误
10002,              签名错误
10003,              重复请求
10004,              请求代码错误
10005,              请求过于频繁
10006,              设备ID不能为空
10009,              风控校验失败
10099,              API 已弃用
10098,              处理失败
//服务端错误
20001,              数据库执行错误
20002,              接口仅限app调用
20003,              des3 key过期
20005,              解密失败
20004,              参数没加密
20006,              系统繁忙请稍后重试

//security相关错误
20401,           //获取des3 key失败
//验证码相关错误
20601,           //生成验证码失败
20602,           //验证码不正确或验证码已过期
//session相关错误
20701,           //session id检测操作失败
```

## 请求接口

### 请求 mobile_id

> 接口地址 /plugin/get_mobile_id 

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      platform            【ios，android】
string      device_id           【设备号】
```

> ** 返回参数 Request Data : **
```
{
    "responseCode": 0,
    "responseMessage": "ok",
    "data": {
        "mobile_id": "ios_V3ERydy5Kqcv"
    }
}

```

### 登录

> 接口地址 /user/login_via_password

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      mobile          【用户手机号】
string      password        【登陆密码】
```

> ** 返回参数 Request Data : **
```
{
    "responseCode": 0,
    "responseMessage": "ok",
    "data": {
        "mobile_id": "ios_ygPVpZKqO8TK",
        "session_id": "acd1fd29796be12f9b3313e022682578",
        "session_security": "VTJGc2RHVmtYMTlITU9vQXVkMmdBVU4xYU9mNlZmcGdMVEk2SU1TTlhIcndQTmhsWWdNN0t5Mjd4SEdlTmdmYmdLWUdaRzZXT0xiWk9pSDhLS3ZPdHNvdDQxaDI5ODRRQ1dRUE5nZVhPRTRvTXZXVWNRKzNieUdoczdGUzA0YjNBM05jSGRQRDk0ZC9sSFVGa0FwejdBPT0",
        "user": {
            "id": 1185,         【用户编号】
            "status": 1,
            "superior_id": 580,
            "group_id": 20,
            "username": "admin",
            "mobile": "18381082760",
            "email": null,
            "face": "http:\/\/www.ypvpa.localhost\/uploads\/images\/20190402\/3dad8d9e900ceaddf8f867487bd69167.jpg",
            "nickname": null,
            "is_real_name": 0,
            "full_name": null,
            "sex": 0,
            "id_type": 1,
            "idnumber": null,
            "id_zheng": null,
            "id_fan": null,
            "id_shouchi": null,
            "birthday": null,
            "is_delete": 0,
            "invite_code": "jpas122f",
            "create_time": "2019-04-02 03:49:02",
            "update_time": "2019-04-02 03:49:02",
            "sex_name": "保密",
            "status_name": "正常",
            "group_name": "商家"
        }
    }
}
```

### 获取二级分类

> 接口地址 /sort/son_good_cate_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int         parent_cate_id          【一级分类（上级分类）ID】
```

> ** 返回参数 Request Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "son_good_cate_list": [
            {
                "id": 2,
                "cate_name": "炒菜",
                "icon": "http://www.ypvpa.localhost/uploads/goods/cate_icon/20190326/2178d9098ee0fbdb635e2f173b4065f1.png"
            },
            {
                "id": 3,
                "cate_name": "烧菜",
                "icon": ""
            }
        ]
    }
}

```

### 计算购物车

> 接口地址 /cart/calculate_cart

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int         spec_id                 【规格ID】
int         buy_number_string       【购买数量增量 比如+1 -1 0等，+1 -1表示在原有基础上+1 -1,0 表示直接定义此规格的购物车数量为0】
```

> ** 返回参数 Request Data : **
```
{
    "responseCode": "0",
    "responseMessage": "执行成功",
    "data": {
        "cart_all_spec_number": 4,          【购物车的规格数量和】
        "cart_all_buy_number": 27,          【购物车的规格购买数量和】
        "cart_all_price": "121.00"          【购物车的购物车总金额】
    }
}
{
    "responseCode": "10001",
    "responseMessage": "购物车物品超过库存",
    "data": {}
}
```
