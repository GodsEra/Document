# 美香厨 供应商 小程序 接口文档

## 请求地址
```
测试地址: http://kitchenminiapi.marketing.ypvpa.com
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
600                 token无效或过期异常
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

[获取验证码](#获取验证码)  

[验证码登录](#验证码登录)  

[找回密码](#找回密码)  

### 导航相关

[首页](#首页)

[订单列表](#订单列表)

### 订单相关

[确认订单](#确认订单)

[修改订单](#修改订单)

## 接口

### 密码登录

> 接口地址 /account/login_via_password

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string      access_token        【登录口令：具体询问开发者】     
string      code                【微信js code（暂时不用）】 
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
        "token": "ZXlKMGVYQWlPaUpLVjFRaUxDSmhiR2NpT2lKSVV6STFOaUo5LmV5SnZZbXBsWTNRaU9uc2liM0JsYm1sa0lqbzBMQ0p6WlhOemFXOXVYMnRsZVNJNk9YMTkuWVN1dUV5VTRSOFEwemRxWnNjUzU5a3IxMmNMRVk5NHMwQlpqMm1DOHEwTQ==",
        // 过期时间（单位：秒）
        "expire_time": 2592000
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

### 获取验证码

> 接口地址 /account/verify_code

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string      access_token        【登录口令：具体询问开发者】     
string      mobile              【手机号】
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "请求成功",
    "data": {}
}
{
    "code": 400,
    "msg": "短信发送失败",
    "data": {}
}
{
    "code": 400,
    "msg": "亲，缺少手机号~",
    "data": {}
}
{
    "code": 400,
    "msg": "亲，缺少登录令牌~",
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
string      code                【微信js code（暂时不用）】 
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
        "token": "ZXlKMGVYQWlPaUpLVjFRaUxDSmhiR2NpT2lKSVV6STFOaUo5LmV5SnZZbXBsWTNRaU9uc2liM0JsYm1sa0lqbzBMQ0p6WlhOemFXOXVYMnRsZVNJNk9YMTkuWVN1dUV5VTRSOFEwemRxWnNjUzU5a3IxMmNMRVk5NHMwQlpqMm1DOHEwTQ==",
         // 过期时间（单位：秒）
        "expire_time": 2592000
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

### 找回密码

> 接口地址 /account/find_password

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string      access_token        【登录口令：具体询问开发者】     
string      mobile              【手机号】
string      verify_code         【验证码】
string      password            【重置的密码】
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "请求成功~",
    "data": {}
}
{
    "code": 400,
    "msg": "亲，验证码已过期~",
    "data": {}
}
{
    "code": 400,
    "msg": "亲，缺少密码~",
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
string              token           【口令】     
int/null            page            【默认第1页】     
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "获取成功",
    "data": {
        // 规格分页
        "spec_paginate": {
            // 规格列表
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

### 订单列表

> 接口地址 /navigation/order_list

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token           【口令】     
int/null            page            【默认第1页】    
string/null         status_choice   【默认全部，pay_success 待发货，send_success 待收货，finish 已完成】    
```
> * status 0 未付款（待付款） 
> * status 1 已付款（待发货） (分解为2、3、4)
> * status 2 （预付款专属）待确认订单 => 可以 确认接单
> * status 3 （预付款专属）待修改订单 => 可以 修改订单
> * status 4 （预付款专属）已修改订单 
> * status 10 已发货（待收货）(分解为11 12 13)
> * status 11 已发货（待收货）已分配订单 商家拣货完成状态 
> * status 12 已发货（待收货）已分配订单 配送员接单状态
> * status 13 已发货（待收货）已分配订单 配送员取货状态
> * status 20 完成（分解为21 22）
> * status 21 完成（待评价） 
> * status 22 完成（已评价） 
> * status 30 订单取消（交易关闭）

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "获取成功",
    "data": {
        // 订单分页
        "order_paginate": {
            // 订单列表
            "list": [
                {
                    // 订单号
                    "order_sn": "S201907171628071447",
                    // 下单时间
                    "create_time": "2019-07-17 16:28:07",
                    // 规格总数
                    "total_number": 1,
                    // 订单金额
                    "total_amount": "0.01",
                    // 订单状态
                    "status": 11,
                    // 规格列表
                    "spec_list": [
                        {
                            // 商品ID
                            "good_id": 27,
                            // 商品名
                            "good_title": "扬名12kg精制红油豆瓣",
                            // 商品图片
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                            // 购买数量
                            "buy_number": 1,
                            // 单位
                            "spec_name": "12kg",
                            // 单价
                            "price": "0.01"
                        },
                        {
                            "good_id": 24,
                            "good_title": "红花椒特麻",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                            "buy_number": 1,
                            "spec_name": "500g",
                            "price": "90.00"
                        },
                        {
                            "good_id": 26,
                            "good_title": "虹陈香10kg红油豆瓣",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                            "buy_number": 1,
                            "spec_name": "10kg",
                            "price": "65.00"
                        }
                    ],
                    // 补款金额
                    "advance_son_total_amount": 10.99,
                    // 最终的订单金额（已这个金额为准来支付）
                    "final_total_amount": 11,
                    // 订单状态显示
                    "status_string": "拣货完成",
                    // 下单时间显示
                    "create_time_string": "07-17 16:28"
                },
                {
                    "order_sn": "S201907171629229317",
                    "create_time": "2019-07-17 16:29:22",
                    "total_number": 6,
                    "total_amount": "0.06",
                    "status": 2,
                    "spec_list": [
                        {
                            "good_id": 27,
                            "good_title": "扬名12kg精制红油豆瓣",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                            "buy_number": 6,
                            "spec_name": "12kg",
                            "price": "0.01"
                        }
                    ],
                    "advance_son_total_amount": 0,
                    "final_total_amount": 0.06,
                    "status_string": "待确认接单",
                    "create_time_string": "07-17 16:29"
                },
                {
                    "order_sn": "S201907251024245837",
                    "create_time": "2019-07-25 10:24:24",
                    "total_number": 6,
                    "total_amount": "0.06",
                    "status": 11,
                    "spec_list": [
                        {
                            "good_id": 27,
                            "good_title": "扬名12kg精制红油豆瓣",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                            "buy_number": 6,
                            "spec_name": "12kg",
                            "price": "0.01"
                        }
                    ],
                    "advance_son_total_amount": -0.04,
                    "final_total_amount": 0.02,
                    "status_string": "拣货完成",
                    "create_time_string": "14天前 10:24"
                },
                {
                    "order_sn": "S201907251027238953",
                    "create_time": "2019-07-25 10:27:23",
                    "total_number": 6,
                    "total_amount": "0.06",
                    "status": 11,
                    "spec_list": [
                        {
                            "good_id": 27,
                            "good_title": "扬名12kg精制红油豆瓣",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                            "buy_number": 6,
                            "spec_name": "12kg",
                            "price": "0.01"
                        }
                    ],
                    "advance_son_total_amount": 0.14,
                    "final_total_amount": 0.2,
                    "status_string": "拣货完成",
                    "create_time_string": "14天前 10:27"
                },
                {
                    "order_sn": "S201907251029519267",
                    "create_time": "2019-07-25 10:29:51",
                    "total_number": 6,
                    "total_amount": "0.06",
                    "status": 11,
                    "spec_list": [
                        {
                            "good_id": 27,
                            "good_title": "扬名12kg精制红油豆瓣",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                            "buy_number": 6,
                            "spec_name": "12kg",
                            "price": "0.01"
                        }
                    ],
                    "advance_son_total_amount": 0,
                    "final_total_amount": 0.06,
                    "status_string": "拣货完成",
                    "create_time_string": "14天前 10:29"
                }
            ],
             // 列表总数
            "count": 5,
             // 分页总数
            "total_page": 1,
            // 当前页
            "current_page": 1,
            // 每页数量
            "pagesize": 10
        },
        // 订单总数
        "count_order_all": 5
    }
}
```  
</details>

[接口目录](#接口目录)

### 确认订单

> 接口地址 /order/accept_order

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token           【口令】     
string              order_sn        【订单号】
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "请求成功",
    "data": {}
}
{
    "code": 400,
    "msg": "请求失败，只有待确认订单有权限~",
    "data": {}
}
{
    "code": 600,
    "msg": "程序罢工，无效token或过期token",
    "data": {}
}
```  
</details>

[接口目录](#接口目录)

### 修改订单

> 接口地址 /order/edit_order

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token           【口令】     
string              order_sn        【订单号】
float               total_amount    【修改后的订单金额】
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "请求成功",
    "data": {}
}
{
    "code": 400,
    "msg": "请求失败，只有待修改订单有权限~",
    "data": {}
}
{
    "code": 400,
    "msg": "程序罢工，缺少订单金额 total_amount~",
    "data": {}
}
{
    "code": 600,
    "msg": "程序罢工，无效token或过期token",
    "data": {}
}
```  
</details>

[接口目录](#接口目录)


