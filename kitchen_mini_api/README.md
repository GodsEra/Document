# 美香厨 供应商 小程序 接口文档

## 请求地址
```
测试地址: http://www.marketing.ypvpa.com/kitchen_mini_api
```

## 状态码
<details>
<summary>状态码说明</summary>

```
code                响应状态 
msg                 响应信息
data                响应数据 具体参考其接口文档
```
</details>

<details>
<summary>状态码列表</summary>

```
100                 未登录
101                 未认证
200                 操作成功
400                 操作失败
500                 异常
```
</details>

## 更新日志

<details>
<summary>2019</summary>

### 2019.8.2 以前
> * 完成基本接口
</details>

## 接口目录

### 登录相关

[密码登录](#密码登录)  

[验证码登录](#验证码登录)  

### 导航相关
[首页](#首页)

## 接口

### 密码登录

> 接口地址 /account/login_via_password

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string      access_token        【登录口令：具体询问开发者】     
string      code                【微信js code】 
string      mobile              【手机号】
string      password            【密码】
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "亲，关联微信成功~",
    "data": {
        // 口令，相当于微信里的3rd_session，用于保持登录状态，登录后的接口都要带此参数
        "token": "ZXlKMGVYQWlPaUpLVjFRaUxDSmhiR2NpT2lKSVV6STFOaUo5LmV5SnZZbXBsWTNRaU9uc2liM0JsYm1sa0lqbzBMQ0p6WlhOemFXOXVYMnRsZVNJNk9YMTkuWVN1dUV5VTRSOFEwemRxWnNjUzU5a3IxMmNMRVk5NHMwQlpqMm1DOHEwTQ=="
    }
}
{
    "code": 400,
    "msg": "帐号或密码错误",
    "data": {}
}
{
    "code": 400,
    "msg": "invalid code, hints: [ req_id: xHAD0qLnRa-2Viq7a ]",
    "data": {}
}
```  
</details>

[接口目录](#接口目录)

### 验证码登录

> 接口地址 /account/login_via_sms

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string      access_token        【登录口令：具体询问开发者】     
string      code                【微信js code】 
string      mobile              【手机号】
string      verify_code            【验证码】
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "亲，关联微信成功~",
    "data": {
        // 口令，相当于微信里的3rd_session，用于保持登录状态，登录后的接口都要带此参数
        "token": "ZXlKMGVYQWlPaUpLVjFRaUxDSmhiR2NpT2lKSVV6STFOaUo5LmV5SnZZbXBsWTNRaU9uc2liM0JsYm1sa0lqbzBMQ0p6WlhOemFXOXVYMnRsZVNJNk9YMTkuWVN1dUV5VTRSOFEwemRxWnNjUzU5a3IxMmNMRVk5NHMwQlpqMm1DOHEwTQ=="
    }
}
{
    "code": 400,
    "msg": "亲，验证码已过期~",
    "data": {}
}
{
    "code": 400,
    "msg": "invalid code, hints: [ req_id: xHAD0qLnRa-2Viq7a ]",
    "data": {}
}
```  
</details>

[接口目录](#接口目录)

### 首页

> 接口地址 /navigation/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string      token           【口令】     
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "获取成功",
    "data": {
        // 商品分页
        "good_paginate": {
            // 商品列表
            "list": [
                {
                    // 商品ID
                    "id": 22,
                    // 商品名 
                    "good_title": "扬名12kg精制红油豆瓣",
                    // 商品图片
                    "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                    // 单位
                    "name": "12kg",
                    // 单价
                    "price": "0.01",
                    // 已售数
                    "payed_buy_number": 25,
                    // 好评率
                    "high_opinion_rate": "0%"
                }
            ],
            // 列表总数
            "count": 1,
            // 分页总数
            "total_page": 1,
            // 当前页
            "current_page": 1,
            // 每页数量
            "pagesize": 10
        },
        // 订单总数
        "count_order_all": 5,
        // 用户信息
        "user_info": {
            "title": "测试供应商001"
        }
    }
}
```  
</details>

[接口目录](#接口目录)


