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
610                 支付密码已存在异常
620                 支付密码不存在异常
630                 提现方式支付宝未绑定异常
```
</details>

## 更新日志

<details>
<summary>2019</summary>

### 2019.8.2 以前
> * 完成基本接口

### 2019.8.13
> * [用户导航](#用户导航) [用户信息](#用户信息) [客服信息](#客服信息) [登录后获取验证码](#登录后获取验证码) [重置密码](#重置密码)

### 2019.8.14
> * [关于我们列表](#关于我们列表) [关于我们](#关于我们) [设置支付密码](#设置支付密码) [重置支付密码](#重置支付密码) 

### 2019.8.19
> * [修改logo](#修改logo) [登出](#登出) [检测支付密码](#检测支付密码)

### 2019.8.20
> * [钱包](#钱包) [钱包流水列表](#钱包流水列表)

### 2019.8.20
> * [支付宝信息](#支付宝信息) [绑定支付宝](#绑定支付宝) [解绑支付宝](#解绑支付宝) [提现请求信息](#提现请求信息)
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

[用户导航](#用户导航)

### 订单相关

[订单详情](#订单详情)

[确认订单](#确认订单)

[修改订单](#修改订单)

### 用户相关

[登出](#登出)

[用户信息](#用户信息)

[修改logo](#修改logo)

[客服信息](#客服信息)

[登录后获取验证码](#登录后获取验证码)

[重置密码](#重置密码)

[关于我们列表](#关于我们列表)

[关于我们](#关于我们)

[设置支付密码](#设置支付密码) 

[重置支付密码](#重置支付密码) 

[检测支付密码](#检测支付密码) 

### 支付相关

[钱包](#钱包) 

[钱包流水列表](#钱包流水列表) 

[支付宝信息](#支付宝信息) 

[绑定支付宝](#绑定支付宝) 

[解绑支付宝](#解绑支付宝) 

[提现请求信息](#提现请求信息) 

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
string      verify_code         【验证码】
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
        // 今日营业额
        "today_order_amount": 0,
        // 最新订单
        "newest_order": {
            // 订单号
            "order_sn": "S201907251029519267",
            // 下单时间
            "create_time": "2019-07-25 10:29:51",
            // 订单金额
            "total_amount": "0.06",
            // 下单时间显示
            "create_time_string": "15天前 10:29"
        },
        // 通知列表
        "notice_list": [
            {
                // 通知名
                "title": "lei了lei了，那个男人他lei了\t",
                // 通知时间
                "create_time": "2019-08-09 17:57:26"
            },
            {
                "title": "牌局竞技明天12点停服更新！",
                "create_time": "2019-08-09 17:55:54"
            },
            {
                "title": "欢迎来到美厨香！",
                "create_time": "2019-08-09 17:55:33"
            }
        ],
        // 用户信息
        "user_info": {
            // 企业名称
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
                    "order_sn": "S201908151454018522",
                    // 下单时间
                    "create_time": "2019-08-15 14:54:01",
                    // 规格总数
                    "total_number": 11,
                    // 订单金额
                    "total_amount": "915.00",
                    // 订单状态
                    "status": 4,
                    // 规格列表
                    "spec_list": [
                        {
                            // 商品ID
                            "good_id": 26,
                            // 商品名
                            "good_title": "虹陈香10kg红油豆瓣",
                            // 商品图片
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/213a5cee0d0bd8ea55ee78235191397e.jpg",
                            // 愿订单的购买数量
                            "buy_number": 3,
                            // 单位
                            "spec_name": "10kg",
                            // 单价
                            "price": "65.00",
                            // 补款订单购买数量
                            "advance_son_buy_number": 0.44,
                            // 最后的购买数量
                            "final_buy_number": 3.44
                        },
                        {
                            "good_id": 27,
                            "good_title": "扬名12kg精制红油豆瓣",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                            "buy_number": 8,
                            "spec_name": "12kg",
                            "price": "90.00",
                            "advance_son_buy_number": 1.16,
                            "final_buy_number": 9.16
                        }
                    ],
                    // 规格总数
                    "all_spec_number": 2,
                    // 补款的订单金额
                    "advance_son_total_amount": 133.09,
                    // 补款的订单规格数量
                    "advance_son_total_number": 1.6,
                    // 最终的订单金额
                    "final_total_amount": 1048.09,
                    // 最终的订单规格数量
                    "final_total_number": 12.6,
                    // 订单状态显示
                    "status_string": "已修改订单",
                    // 下单时间显示
                    "create_time_string": "2小时前"
                },
                {
                    "order_sn": "S201908151407006811",
                    "create_time": "2019-08-15 14:07:00",
                    "total_number": 11,
                    "total_amount": "915.00",
                    "status": 11,
                    "spec_list": [
                        {
                            "good_id": 26,
                            "good_title": "虹陈香10kg红油豆瓣",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/213a5cee0d0bd8ea55ee78235191397e.jpg",
                            "buy_number": 3,
                            "spec_name": "10kg",
                            "price": "65.00",
                            "advance_son_buy_number": 0.38,
                            "final_buy_number": 3.38
                        },
                        {
                            "good_id": 27,
                            "good_title": "扬名12kg精制红油豆瓣",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                            "buy_number": 8,
                            "spec_name": "12kg",
                            "price": "90.00",
                            "advance_son_buy_number": 1.02,
                            "final_buy_number": 9.02
                        }
                    ],
                    "all_spec_number": 2,
                    "advance_son_total_amount": 116.45,
                    "advance_son_total_number": 1.4,
                    "final_total_amount": 1031.45,
                    "final_total_number": 12.4,
                    "status_string": "拣货完成",
                    "create_time_string": "昨天 14:07"
                },
                {
                    "order_sn": "S201908151401316061",
                    "create_time": "2019-08-15 14:01:31",
                    "total_number": 8,
                    "total_amount": "720.00",
                    "status": 11,
                    "spec_list": [
                        {
                            "good_id": 27,
                            "good_title": "扬名12kg精制红油豆瓣",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                            "buy_number": 8,
                            "spec_name": "12kg",
                            "price": "90.00",
                            "advance_son_buy_number": 1.5,
                            "final_buy_number": 9.5
                        }
                    ],
                    "all_spec_number": 1,
                    "advance_son_total_amount": 135,
                    "advance_son_total_number": 1.5,
                    "final_total_amount": 855,
                    "final_total_number": 9.5,
                    "status_string": "拣货完成",
                    "create_time_string": "昨天 14:01"
                },
                {
                    "order_sn": "S201908151354363399",
                    "create_time": "2019-08-15 13:54:36",
                    "total_number": 8,
                    "total_amount": "720.00",
                    "status": 11,
                    "spec_list": [
                        {
                            "good_id": 27,
                            "good_title": "扬名12kg精制红油豆瓣",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                            "buy_number": 8,
                            "spec_name": "12kg",
                            "price": "90.00",
                            "advance_son_buy_number": 0,
                            "final_buy_number": 8
                        }
                    ],
                    "all_spec_number": 1,
                    "advance_son_total_amount": 0,
                    "advance_son_total_number": 0,
                    "final_total_amount": 720,
                    "final_total_number": 8,
                    "status_string": "拣货完成",
                    "create_time_string": "昨天 13:54"
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
                            "price": "0.01",
                            "advance_son_buy_number": 0,
                            "final_buy_number": 6
                        }
                    ],
                    "all_spec_number": 1,
                    "advance_son_total_amount": 0,
                    "advance_son_total_number": 0,
                    "final_total_amount": 0.06,
                    "final_total_number": 6,
                    "status_string": "拣货完成",
                    "create_time_string": "07-25 10:29"
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
                            "price": "0.01",
                            "advance_son_buy_number": 6,
                            "final_buy_number": 12
                        }
                    ],
                    "all_spec_number": 1,
                    "advance_son_total_amount": 0.14,
                    "advance_son_total_number": 6,
                    "final_total_amount": 0.2,
                    "final_total_number": 12,
                    "status_string": "拣货完成",
                    "create_time_string": "07-25 10:27"
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
                            "price": "0.01",
                            "advance_son_buy_number": 6,
                            "final_buy_number": 12
                        }
                    ],
                    "all_spec_number": 1,
                    "advance_son_total_amount": -0.04,
                    "advance_son_total_number": 6,
                    "final_total_amount": 0.02,
                    "final_total_number": 12,
                    "status_string": "拣货完成",
                    "create_time_string": "07-25 10:24"
                },
                {
                    "order_sn": "S201907171629229317",
                    "create_time": "2019-07-17 16:29:22",
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
                            "price": "0.01",
                            "advance_son_buy_number": 1.2,
                            "final_buy_number": 7.2
                        }
                    ],
                    "all_spec_number": 1,
                    "advance_son_total_amount": 0.01,
                    "advance_son_total_number": 1.2,
                    "final_total_amount": 0.07,
                    "final_total_number": 7.2,
                    "status_string": "拣货完成",
                    "create_time_string": "07-17 16:29"
                },
                {
                    "order_sn": "S201907171628071447",
                    "create_time": "2019-07-17 16:28:07",
                    "total_number": 1,
                    "total_amount": "0.01",
                    "status": 11,
                    "spec_list": [
                        {
                            "good_id": 27,
                            "good_title": "扬名12kg精制红油豆瓣",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                            "buy_number": 1,
                            "spec_name": "12kg",
                            "price": "0.01",
                            "advance_son_buy_number": 1,
                            "final_buy_number": 2
                        },
                        {
                            "good_id": 24,
                            "good_title": "红花椒特麻",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                            "buy_number": 1,
                            "spec_name": "500g",
                            "price": "90.00",
                            "advance_son_buy_number": 1,
                            "final_buy_number": 2
                        },
                        {
                            "good_id": 26,
                            "good_title": "虹陈香10kg红油豆瓣",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                            "buy_number": 1,
                            "spec_name": "10kg",
                            "price": "65.00",
                            "advance_son_buy_number": 1,
                            "final_buy_number": 2
                        }
                    ],
                    "all_spec_number": 3,
                    "advance_son_total_amount": 10.99,
                    "advance_son_total_number": 1,
                    "final_total_amount": 11,
                    "final_total_number": 2,
                    "status_string": "拣货完成",
                    "create_time_string": "07-17 16:28"
                }
            ],
            "count": 9,
            "total_page": 1,
            "current_page": 1,
            "pagesize": 10
        },
        "count_order_all": 9
    }
}
```  
</details>

[接口目录](#接口目录)

### 用户导航

> 接口地址 /navigation/user

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token           【口令】     
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "获取成功",
    "data": {
        // 订单总数
        "count_order_all": 5,
        // 用户信息
        "user_info": {
            // 企业ID
            "id": 1,
            // 企业名称
            "title": "测试供应商001",
            // LOGO
            "logo": "http://www.ypvpa.localhost/uploads/images/201906/f24f73d171.jpg"
        }
    }
}
{
    "code": 600,
    "msg": "程序罢工，无效token或过期token",
    "data": {}
}
```  
</details>

[接口目录](#接口目录)

### 订单详情

> 接口地址 /order/order

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token           【口令】     
string              order_sn        【订单号】
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
        // 订单信息
        "order": {
            // 订单号
            "order_sn": "S201908151454018522",
            // 订单状态
            "status": 4,
            // 时间->下单时间
            "create_time": "2019-08-15 14:54:01",
            // 收货人（商户名)
            "extension_title": "苏杰的商户",
            // 收货电话（商户电话）
            "extension_tel": "18381082760",
            // 收取地址-详细地址（商户地址）
            "extension_address": "四川省成都市武侯区四川成都",
            // 订单金额
            "total_amount": "915.00",
            // 规格总数
            "total_number": 11,
            // 订单备注
            "remarks": null,
            // 时间->订单付款时间
            "pay_time": "2019-08-15 14:54:58",
            // 时间->送达时间
            "arrive_time": "2019年06月29日 后天 [营业即送 08:00-09:00",
            // 规格列表
            "spec_list": {
                "list": [
                    {
                        // 规格售价
                        "price": "65.00",
                        // 商品名
                        "good_title": "虹陈香10kg红油豆瓣",
                        // 商品图片
                        "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/213a5cee0d0bd8ea55ee78235191397e.jpg",
                        // 购买数量
                        "buy_number": 3,
                        // 规格总价
                        "all_spec_price": 195,
                        // 补款订单购买数量
                        "advance_son_buy_number": 0.44,
                        // 最后的购买数量
                        "final_buy_number": 3.44
                    },
                    {
                        "price": "90.00",
                        "good_title": "扬名12kg精制红油豆瓣",
                        "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                        "buy_number": 8,
                        "all_spec_price": 720,
                        "advance_son_buy_number": 1.16,
                        "final_buy_number": 9.16
                    }
                ],
                // 总规格数
                "all_spec_number": 2,
                // 总规格购买数量和
                "all_buy_number": 11,
                // 总金额
                "all_price": 915,
                // 总优惠价
                "all_diff_price": 0,
                // 运费
                "distribution_price": "0.00"
            },
            // 时间->取消订单时间
            "cancel_time": null,
             // 时间->订单拣货时间
            "distribution_get_order_time": "2019-08-15 14:59:10",
            // 时间->配送员接单时间
            "distribution_arriving_time": null,
            // 时间->配送员取货时间
            "distribution_sending_time": null,
            // 时间->订单完成时间
            "finish_time": null,
            // 时间->订单评论时间
            "evaluation_time": null,
            // 补款总金额
            "advance_son_total_amount": 133.09,
            // 补款规格总数
            "advance_son_total_number": 1.6,
            // 实际最后的总金额
            "final_total_amount": 1048.09,
            // 最终的订单规格数量
            "final_total_number": 12.6,
            // 订单状态显示
            "status_string": "已修改订单",
            // 订单状态显示的解释
            "status_string_description": "订单支付成功，等待商家接单",
            // 支付方式
            "pay_type_string": "微信支付",
            // 物流方式
            "distribution_type": "大神物流"
        },
        // 配送信息
        "distribution_order": {
            // 配送员全名
            "distribution_user_full_name": "罗宝银",
            // 配送员头像
            "distribution_user_face": "http://www.ypvpa.localhost/uploads/distribution_user/face/201905/a4acf3ef8c.jpg",
            // 配送员电话
            "distribution_user_mobile": "13900000053",
            // 配送状态
            "status_string": "已分配",
            // 坐标信息
            "coordinate_info": {
                // 确认接单坐标 到 取货坐标列表
                "receive_to_pick_goods": {
                    // 坐标纬度
                    "coordinate_x": "23.5555556",
                    // 坐标经度
                    "coordinate_y": "113.2222222", 
                    // 接单时间
                    "create_time": "1970-01-01 08:33:39"
                },
                // 取货坐标 到 完成坐标列表
                "pick_goods_to_merchant": {
                    // 坐标纬度
                    "coordinate_x": "23.5555556",
                    // 坐标经度
                    "coordinate_y": "113.2222222",
                    // 取货时间
                    "create_time": "1970-01-01 08:33:39" 
                }
            }
        }
    }
}
{
    "code": 200,
    "msg": "获取成功",
    "data": {
        // 订单信息
        "order": {
            // 订单号
            "order_sn": "S201907251024245837",
            // 订单状态
            "status": 11,
            // 时间->下单时间
            "create_time": "2019-07-25 10:24:24",
            // 收货人（商户名)
            "extension_title": "苏杰的商户",
            // 收货电话（商户电话）
            "extension_tel": "18381082760",
            // 收取地址-详细地址（商户地址）
            "extension_address": "四川省成都市武侯区四川成都",
            // 预付总金额
            "total_amount": "0.06",
            "total_number": 11,
            // 订单备注
            "remarks": null,
            // 时间->订单付款时间
            "pay_time": "2019-07-25 10:25:23",
            // 时间->送达时间
            "arrive_time": "2019年06月29日 后天 [营业即送 08:00-09:00]",
            // 规格列表信息
            "spec_list": {
                // 列表
                "list": [
                    {
                        // 规格售价
                        "price": "0.01",
                        // 商品名
                        "good_title": "扬名12kg精制红油豆瓣",
                        // 商品图片
                        "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                        // 购买数量
                        "buy_number": 6,
                        // 规格总价
                        "all_spec_price": 0.06
                    }
                ],
                // 总规格数
                "all_spec_number": 1,
                // 总规格购买数量和
                "all_buy_number": 6,
                // 总金额
                "all_price": 0.06,
                // 总优惠价
                "all_diff_price": 0,
                // 运费
                "distribution_price": "0.00",
            },
            // 时间->取消订单时间
            "cancel_time": null,
            // 时间->订单拣货时间
            "distribution_get_order_time": "2019-08-08 10:51:22",
            // 时间->配送员接单时间
            "distribution_arriving_time": null,
            // 时间->配送员取货时间
            "distribution_sending_time": null,
            // 时间->订单完成时间
            "finish_time": null,
            // 时间->订单评论时间
            "evaluation_time": null,
            // 补款总金额
            "advance_son_total_amount": -0.04,
            // 实际最后的总金额
            "final_total_amount": 0.02,
            // 订单状态显示
            "status_string": "拣货完成",
            // 订单状态显示的解释
            "status_string_description": "商家已完成拣货，等待配送",
            // 支付方式
            "pay_type_string": "微信支付",
            // 物流方式
            "distribution_type": "大神物流"
        },
        
    }
}

{
    "code": 200,
    "msg": "获取成功",
    "data": {
        "order": {
            "order_sn": "S201907171629229317",
            "status": 1,
            "create_time": "2019-07-17 16:29:22",
            "extension_title": "苏杰的商户",
            "extension_tel": "18381082760",
            "extension_address": "四川省成都市武侯区四川成都",
            "total_amount": "0.06",
            "remarks": null,
            "pay_time": "2019-07-17 16:29:45",
            "arrive_time": "2019年06月29日 后天 [营业即送 08:00-09:00]",
            "spec_list": {
                "list": [
                    {
                        "price": "0.01",
                        "good_title": "扬名12kg精制红油豆瓣",
                        "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/ef095c8bf7b0e252d79a7c9c2e6f248b.jpg",
                        "buy_number": 6,
                        "all_spec_price": 0.06
                    }
                ],
                "all_spec_number": 1,
                "all_buy_number": 6,
                "all_price": 0.06,
                "all_diff_price": 0,
                "distribution_price": "0.00"
            },
            "cancel_time": null,
            "distribution_get_order_time": null,
            "distribution_arriving_time": null,
            "distribution_sending_time": null,
            "finish_time": null,
            "evaluation_time": null,
            "advance_son_total_amount": 0,
            "final_total_amount": 0.06,
            "status_string": "已支付",
            "status_string_description": "订单支付成功，等待商家接单",
            "pay_type_string": "微信支付",
            "distribution_type": "大神物流"
        },
        "distribution_order": {}
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
float               total_number    【修改后的订单规格数】
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "请求成功",
    "data": {
        // 订单金额
        "total_amount": "915.00",
        // 补款金额
        "advance_son_total_amount": 133.09,
        // 订单规格总数
        "total_number": 11,
        // 补款规格总数
        "advance_son_total_number": 1.6,
        // 规格列表
        "spec_list": [
            {
                // 购买数量
                "buy_number": 3.44
            },
            {
                "buy_number": 9.16
            }
        ],
        // 最终的订单金额
        "final_total_amount": 1048.09,
        // 最终的订单规格总数
        "final_total_number": 12.6
    }
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

### 登出

> 接口地址 /user/logout

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token           【口令】     
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "请求成功",
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

### 用户信息

> 接口地址 /user/user

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token           【口令】     
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "获取成功",
    "data": {
        // LOGO
        "logo": "http://www.ypvpa.localhost/uploads/images/201906/f24f73d171.jpg",
        // 负责人
        "full_name": "苏苏",
        // 手机号
        "mobile": "18381082760",
        // 企业名称
        "title": "测试供应商001",
        // 企业ID
        "id": 1,
        // 经营地址 区
        "area_name": "武侯区",
        // 经营地址 市
        "city_name": "成都市",
        // 经营地址 省
        "province_name": "四川省",
        //  详细地址
        "address": "天府大道"
    }
}
{
    "code": 600,
    "msg": "程序罢工，无效token或过期token",
    "data": {}
}
```  
</details>

[接口目录](#接口目录)

### 修改logo

> 接口地址 /user/edit_logo

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token           【口令】     
string              logo_base64     【logo图片的base64值】     
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "请求成功",
    "data": {
        // 新logo地址
        "logo": "http://www.ypvpa.localhost/uploads/supplier/logo/201908/6f79f945ec.png"
    }
}
{
    "code": 400,
    "msg": "请求失败，上传logo失败~",
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

### 客服信息

> 接口地址 /user/client

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token           【口令】     
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "获取成功",
    "data": {
        // 电话
        "tel": "4001-898-116",
        // 题目
        "title": "24小时在线客服",
        // 摘要
        "description": "有问题？联系上方客服电话服务您！"
    }
}
{
    "code": 600,
    "msg": "程序罢工，无效token或过期token",
    "data": {}
}
```  
</details>

[接口目录](#接口目录)

### 登录后获取验证码

> 接口地址 /user/verify_code

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token           【口令】     
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "请求成功~",
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

### 重置密码

> 接口地址 /user/reset_password

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token                   【口令】 
string              original_password       【原始的密码】
string              password                【重置的密码】
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
    "msg": "请求失败，原始密码错误",
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

### 关于我们列表

> 接口地址 /user/about_us_list

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token           【口令】 
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "获取成功",
    "data": {
        "0": {
            "id": 1,
            "title": "美厨香客户协议"
        },
        "1": {
            "id": 2,
            "title": "美厨香用户协议"
        }
    }
}
{
    "code": 600,
    "msg": "程序罢工，无效token或过期token",
    "data": {}
}
```  
</details>

[接口目录](#接口目录)

### 关于我们

> 接口地址 /user/about_us

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token           【口令】 
int                 id              【关于我们ID】
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "获取成功",
    "data": {
        "title": "美厨香客户协议",
        "content": "666666",
        "create_time": "2019-08-14 02:25:42"
    }
}
{
    "code": 400,
    "msg": "请求失败，信息不存在",
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

### 设置支付密码

> 接口地址 /user/set_pay_password

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token                   【口令】 
string              pay_password            【支付密码】 
string              confirm_pay_password    【确认支付密码】 
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "请求成功",
    "data": {}
}
{
    "code": 610,
    "msg": "请求失败，已存在支付密码",
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

### 重置支付密码

> 接口地址 /user/reset_pay_password

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token                   【口令】 
string              verify_code             【验证码】
string              pay_password            【重置的支付密码】 
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "请求成功",
    "data": {}
}
{
    "code": 620,
    "msg": "请求失败，不存在支付密码",
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

### 检测支付密码

> 接口地址 /user/check_has_pay_password

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token                   【口令】 
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "请求成功",
    "data": {
        // 状态 1-已设置支付密码 0-没有设置支付密码
        "status": 1
    }
}
{
    "code": 200,
    "msg": "请求成功",
    "data": {
        "status": 0
    }
}
{
    "code": 600,
    "msg": "程序罢工，无效token或过期token",
    "data": {}
}
```  
</details>

[接口目录](#接口目录)

### 钱包

> 接口地址 /user/wallet

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token                   【口令】 
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "获取成功",
    "data": {
        // 钱包余额
        "balance": "0.00"
    }
}
{
    "code": 600,
    "msg": "程序罢工，无效token或过期token",
    "data": {}
}
```  
</details>

[接口目录](#接口目录)

### 钱包流水列表

> 接口地址 /user/wallet_log_list

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token                   【口令】 
int/null            page            【默认第1页】     
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "获取成功",
    "data": {
        // 流水分页
        "log_paginate": {
            // 流水列表
            "list": [
                {
                    // 流水金额
                    "amount": "99.00",
                    // 流水时间
                    "create_time": "2019-08-20 14:36:00",
                    // 流水标题
                    "title": "预售：虹陈香10kg红油豆瓣",
                    // 流水时间显示
                    "create_time_string": "52分钟前"
                },
                {
                    "amount": "99.00",
                    "create_time": "2019-08-20 14:29:41",
                    "title": "预售：虹陈香10kg红油豆瓣",
                    "create_time_string": "59分钟前"
                },
                {
                    "amount": "99.00",
                    "create_time": "2019-08-20 11:41:46",
                    "title": "预售：虹陈香10kg红油豆瓣",
                    "create_time_string": "4小时前"
                },
                {
                    "amount": "195.00",
                    "create_time": "2019-08-20 11:30:59",
                    "title": "预售：虹陈香10kg红油豆瓣",
                    "create_time_string": "4小时前"
                },
                {
                    "amount": "195.00",
                    "create_time": "2019-08-20 11:27:40",
                    "title": "预售：虹陈香10kg红油豆瓣",
                    "create_time_string": "5小时前"
                },
                {
                    "amount": "195.00",
                    "create_time": "2019-08-20 11:10:53",
                    "title": "预售：虹陈香10kg红油豆瓣",
                    "create_time_string": "5小时前"
                }
            ],
            // 列表总数
            "count": 7,
            // 分页总数
            "total_page": 2,
            // 当前页
            "current_page": 1,
            // 每页数量
            "pagesize": 6,
            // 收入总金额
            "income_amount": 882,
            // 支出总金额
            "outlay_amount": 0
        }
    }
}
{
    "code": 600,
    "msg": "程序罢工，无效token或过期token",
    "data": {}
}
```  
</details>

[接口目录](#接口目录)

### 支付宝信息

> 接口地址 /user/withdrawals_type_alipay_info

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token                           【口令】 
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "获取成功",
    "data": {
        // 支付宝账户姓名
        "alipay_account_number": "18381082760",
        // 支付宝账户
        "alipay_full_name": "马化腾",
        // 是否绑定支付宝(0-未绑定 1-已绑定)
        "status": 1
    }
}
{
    "code": 600,
    "msg": "程序罢工，无效token或过期token",
    "data": {}
}
```  
</details>

[接口目录](#接口目录)

### 绑定支付宝

> 接口地址 /user/binding_alipay

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token                           【口令】 
string              verify_code                     【验证码】 
string              alipay_full_name                【支付宝账户姓名】 
string              alipay_account_number           【支付宝帐号】 
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
    "msg": "亲，缺少验证码~",
    "data": {}
}
{
    "code": 400,
    "msg": "请求失败，支付宝已经绑定",
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

### 解绑支付宝

> 接口地址 /user/untied_alipay

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token                           【口令】 
string              verify_code                     【验证码】 
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
    "msg": "亲，缺少验证码~",
    "data": {}
}
{
    "code": 630,
    "msg": "请求失败，支付宝还未绑定",
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

### 提现请求信息

> 接口地址 /user/withdrawals_request_info

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
string              token                           【口令】 
string              verify_code                     【验证码】 
```

> ** 返回参数 Response Data : **
```
{
    "code": 200,
    "msg": "获取成功",
    "data": {
        // 支付类型列表
        "withdrawals_type_list": [
            {
                // 类型（alipay-支付宝）
                "type": "alipay",
                // 标题
                "title": "18381082760"
            }
        ],
        // 钱包
        "wallet": {
            // 钱包余额
            "balance": "200.00"
        }
    }
}
{
    "code": 400,
    "msg": "亲，缺少验证码~",
    "data": {}
}
{
    "code": 630,
    "msg": "请求失败，支付宝还未绑定",
    "data": {}
}
{
    "code": 620,
    "msg": "请求失败，不存在支付密码",
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

