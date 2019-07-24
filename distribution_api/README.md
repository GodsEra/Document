# 大神物流APP接口文档

## 注意事项
```
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

6、所有接口返回
{
    "reqCode": 接口请求码,
    "responseCode": 错误码,
    "responseMessage": "错误提示",
    "data": 返回的数据
}
```

## 请求地址
```
测试地址：http://distributionapi.marketing.ypvpa.com
```

## 状态码
<details>
<summary>状态码说明</summary>

```
responseCode        响应状态 
responseMessage     响应信息
data                响应数据 具体参考其接口文档
```
</details>

<details>
<summary>状态码列表</summary>

```
0                   成功
30001,              错误

客户端错误
10001,              参数错误
10002,              签名错误
10003,              重复请求
10004,              请求代码错误
10005,              请求过于频繁
10006,              设备ID不能为空
10009,              风控校验失败
10099,              API 已弃用
10098,              处理失败

服务端错误
20001,              数据库执行错误
20002,              接口仅限app调用
20003,              des3 key过期
20005,              解密失败
20004,              参数没加密
20006,              系统繁忙请稍后重试

security相关错误
20401,              获取des3 key失败

验证码相关错误
20601,              生成验证码失败
20602,              验证码不正确或验证码已过期

session相关错误
20701,              session id检测操作失败
```
</details>

## 更新日志

<details>
<summary>2019</summary>

### 2019.5.8 以前
> * 完成基本接口

### 2019.7.24
>* 增加 [设置坐标](#设置坐标)
</details>

## 接口目录

[请求 mobile_id](#请求mobile_id)  

[第二步用户登陆](#第二步用户登陆)  

[发送短信验证码](#发送短信验证码)  

[使用短信验证码进行登陆](#使用短信验证码进行登陆)  

[重置密码](#重置密码)  

[base64位上传图像](#base64位上传图像)  

[变更用户资料（目前只允许修改头像）](#变更用户资料（目前只允许修改头像）)  

[获取地区联动（所有地区）](#获取地区联动（所有地区）)  

[获取地区列表（可以进行联动查询）](#获取地区列表（可以进行联动查询）)  

[获取配送的订单列表](#获取配送的订单列表)  

[订单详情](#订单详情)  

[确认接单](#确认接单)  

[确认已经取货](#确认已经取货)  

[确认配送完成](#确认配送完成)  

[更新配送人员坐标](#更新配送人员坐标)  

[查找订单数量](#查找订单数量)  

[查找订单简易列表](#查找订单简易列表)  

[首页显示统计数据](#首页显示统计数据)  

[收益列表](#收益列表)  

[收益统计](#收益统计)  

[查询登陆用户详情](#查询登陆用户详情)  

[设置坐标](#设置坐标)  

## 接口

### 请求mobile_id

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110000
$params   platform  【ios，android】
$params   device_id  【设备号】
$params   reqTime     
$params   checksum 
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110000,
    "responseCode": 0,
    "responseMessage": "ok",
    "data": {
        "mobile_id": "ios_nWGrwy92TOez"   【mobile_id     全局使用】
    }
}

```  
</details>

[接口目录](#接口目录)

### 第二步用户登陆

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110201
$params   reqTime     
$params   checksum 
$params   mobile_id
$params   mobile  【用户手机号】
$params   password  【登陆密码】
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110201,
    "responseCode": 0,
    "responseMessage": "ok",
    "data": {
        "mobile_id": "ios_nWGrwy92TOez",   
        "session_id": "1671f90a744ccf30f33ab95bca4de6c5",  【全局】
        "session_security": "VTJGc2RHVmtYMS9VcGQ5QmkxNGZLbHFpbVpVQmpuRGNyM3Z2V3FXdFB0V1pOcktyYlJXS1IvSklINGxMaCtlbHN6NDVmSmI3UkJ0WGZGMGRxZWhSSk1FeXZ3Sk1pa3ZqR3FDZGdZN1RsZE15WkUvOGYrM1FBVXcrZjNLemgzR0JnUUg0eGwvSWt2WXV3L3lYZUlvSGp3PT0",【全局】
        "user": {     【用户详情】
            "id": 1,    【用户编号】
            "user_id": 0,
            "status": 1,     【工作状态，休假或者上班】
            "work_status": 5,【空闲还是忙碌】
            "full_name": "陈曦",   【姓名】
            "face": "http:\/\/img.marketing.dashen.com\/uploads\/face\/201901\/f17622f006.jpg",【头像】
            "mobile": "13438259723",  【手机号】
            "service_area_json": "{\"service_area\":\"2545\",\"service_city\":\"285\",\"service_province\":\"23\",\"service_str\":\"\\u56db\\u5ddd\\u7701-\\u5df4\\u4e2d\\u5e02-\\u901a\\u6c5f\\u53bf\"}",
            "service_province": null,    【省编号】
            "service_city": 285,【市编号】
            "service_area": 2545,【区县编号】
            "number": 0,
            "settlement_number": 0,
            "is_delete": 0,
            "create_time": "2019-01-15 09:34:51",
            "update_time": "2019-03-26 12:02:06",
            "status_name": "工作中",     【工作状态，休假或者上班】
            "work_status_name": "空闲中",【空闲还是忙碌】
            "service_area_json_array": {
                "service_area": "2545",        【区县编号】
                "service_city": "285",            【市编号】
                "service_province": "23",       【省编号】
                "service_str": "四川省-巴中市-通江县"    【联动信息】
            }
        }
    }
}
```  
</details>

[接口目录](#接口目录)

### 发送短信验证码

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110202
$params   reqTime     
$params   checksum 
$params   mobile_id
$params   mobile  【用户手机号】
$params   slug  【固定值：用户注册---get_verify_code_to_reg    用户登陆：get_verify_code_to_reg   找回密码：get_verify_code_to_reg】
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110202
    "responseCode": 0,
    "responseMessage": "ok",
    "data": [ ]
}
```  
</details>

[接口目录](#接口目录)

### 使用短信验证码进行登陆

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110203
$params   reqTime     
$params   checksum 
$params   mobile_id
$params   mobile  【用户手机号】
$params   verify_code  【短信验证码】
```

> ** 返回参数 Response Data : **
```
返回数据与用户登陆一样
```  
</details>

[接口目录](#接口目录)

### 重置密码

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110204
$params   reqTime     
$params   checksum 
$params   mobile_id
$params   mobile  【用户手机号】
$params   verify_code  【短信验证码】
$params   password  【新密码】
$params   conn_password  【确认密码】
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110202
    "responseCode": 0,
    "responseMessage": "ok",
    "data": [ ]
}
```  
</details>

[接口目录](#接口目录)

### base64位上传图像
 
> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110205
$params   reqTime     
$params   checksum 
$params   mobile_id
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】
$params   module  【上传模块固定值    头像-distributionUserFace】
$params   base64_img_body  【base64位图像内容  -------------改字段不需要进行签名】
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110205,
    "responseCode": 0,
    "responseMessage": "ok",
    "data": {
        "name": "a9b4dce522",    【图像名称】
        "save_name": "\/uploads\/images\/201903\/a9b4dce522.png",   【保存路径】  
        "extension": "png",    【后缀名】
        "pic_host": "http:\/\/img.marketing.dashen.com"     【图像保存的域名】
    }
}
```  
</details>

[接口目录](#接口目录)

### 变更用户资料（目前只允许修改头像）
 
> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110206
$params   reqTime     
$params   checksum 
$params   mobile_id
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】
$params   face  【上传图像返回的   路径----------对应save_name值】
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110206,
    "responseCode": 0,
    "responseMessage": "ok",
    "data":[]
}
```  
</details>

[接口目录](#接口目录)

### 获取地区联动（所有地区）

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110101
$params   mobile_id   全局  mobile_id   
$params   reqTime    
$params   checksum 
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110101，
    "responseCode": 0,
    "responseMessage": "ok",
    "data": [
        {
            "id": 1,
            "reid": 0,
            "cat_name": "北京市",    【省】
            "jianpin": "bjs",
            "quanpin": "beijingshi",
            "list": [
                {
                    "id": 35,
                    "reid": 1,
                    "cat_name": "北京市",   【市】
                    "jianpin": "bjs",
                    "quanpin": "beijingshi",
                    "list": [
                        {
                            "id": 380,
                            "reid": 35,
                            "cat_name": "东城区",  【区县】
                            "jianpin": "dcq",
                            "quanpin": "dongchengqu"
                        },
                    ]
                }
            ]
        },
    ]
}
```  
</details>

[接口目录](#接口目录)

### 获取地区列表（可以进行联动查询）

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110102
$params   reqTime    
$params   checksum 
$params   mobile_id   全局  mobile_id
$params   reid   【主键编号，0为顶级-省】 
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110102
    "responseCode": 0,
    "responseMessage": "ok",
    "data": [
       {
            "id": 1,    【主键编号】
            "reid": 0,   【上级编号   0为顶级】
            "cat_name": "四川省",   【地区名称】
            "quanpin": "scs",   【地区拼音首字母  - 备用】
            "jianpin": "sichuansheng",   【全拼音  - 备用】
 
        }
    ]
}
```  
</details>

[接口目录](#接口目录)

### 获取配送的订单列表

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110301
$params   reqTime    
$params   checksum 
$params   mobile_id   全局  mobile_id   
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】

$params   limit   每页读取多少条记录
$params   page   第几页数据  
$params   order_by   【为空为创建时间倒序       l.status desc 订单状态倒序     l.status desc 订单状态顺序    l.create_time desc 创建时间倒序    l.create_time asc 创建时间顺序         可以组合使用比如： l.status desc l.create_time desc   意思是：优先订单状态倒序 然后再时间倒序】
$params   status  状态  【为空为全部        1-等待接单     2-确认接单    5-已经取货   10--完成】   
$params  start_time    【时间查询     开始时间   如：2019-03-23 12:36:35】
$params  end_time      【时间查询    结束时间   如：2019-03-23 12:36:35】
$params  order_sn  【订单号】
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110301,
    "responseCode": 0,
    "responseMessage": "ok",
    "data": {
        "list": [
            {
                "id": 529,         【配送订单编号】
                "status": 10,     【配送状态】
                "user_id": 1,      【配送人员编号】
                "order_type": "kitchen",   【订单类型   kitchen表示大神厨房】
                "order_sn": "S201903301129547356",    【订单编号】
                "complete_time": "2019-03-30 15:52:25",【配送完成时间】
                "is_settlement": 0,
                "settlement_time": null,
                "create_time": "2019-03-30 15:05:12",【配送创建时间】
                "update_time": "2019-03-30 15:52:25",【更新时间】
                "full_name": "陈曦",                    【配送人员姓名】
                "mobile": "13438259723",            【配送人员电话】
                "order_info": {                                          【订单详情】
                    "merchant_name": "霸王牛肉分店",      【店铺名称】
                    "order_sn": "S201903301129547356",
                    "contact_province": null,                 【位置：省】
                    "contact_city": null,                          【位置：市】
                    "contact_dist": null,                          【位置：区县】
                    "contact_street": null,                       【详细位置】
                    "contact_name": null,                       【收货人】
                    "contact_mobile": null,                      【联系电话】
                    "pay_money": "0.00",                【付款总金额】
                    "total_amount": "100.00",         【订单总金额】
                    "remarks": null,                          【备注】
                    "create_time": "2019-03-30 11:29:54"      【创建时间】
                },
                "order_item_list": [                          【商品列表】
                    {
                        "title": "红烧肉",            【商品名称】
                        "buy_number": 1,         【商品数量】
                        "litpic": "http:\/\/distributionapi.marketing.dashen.com\/uploads\/goods\/cover\/20190330\/d2aba040f501729c477662e75710314c.png",     【商品封面图】
                        "price": "100.00",             【商品单价】
                        "spec_name": "10瓶装"    【商品规格名称】
                    }
                ],
                "status_name": "完成配送"     【配送状态说明】
            }
        ],
        "count": 4,     【总共有多少条】
        "total_page": 4,      【一共有多少页】
        "current_page": 1,     【当前页数的  位置】
        "pagesize": 1              【每页显示多少条记录】
    }
}
```  
</details>

[接口目录](#接口目录)

### 订单详情

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110305
$params   reqTime    
$params   checksum 
$params   mobile_id   全局  mobile_id   
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】
$params   order_id   【配送订单编号】
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110305,
    "responseCode": 0,
    "responseMessage": "ok",
    "data": {
        "id": 529,
        "status": 5,
        "user_id": 1,
        "order_type": "kitchen",
        "order_sn": "S201903301129547356",
        "complete_time": "2019-03-30 15:52:25",
        "is_settlement": 0,
        "settlement_time": null,
        "create_time": "2019-03-30 15:05:12",
        "update_time": "2019-04-01 15:50:23",
        "status_name": "配送中",
        "type_order_info": {
            "merchant_name": "霸王牛肉分店",
            "order_sn": "S201903301129547356",
            "contact_province": null,
            "contact_city": null,
            "contact_dist": null,
            "contact_street": null,
            "contact_name": null,
            "contact_mobile": null,
            "pay_money": "0.00",
            "total_amount": "100.00",
            "remarks": null,
            "create_time": "2019-03-30 11:29:54"
        },
        "type_order_item_list": [
            {
                "title": "红烧肉",
                "buy_number": 1,
                "litpic": "\/uploads\/goods\/cover\/20190330\/d2aba040f501729c477662e75710314c.png",
                "price": "100.00",
                "spec_name": "10瓶装"
            }
        ],
        "pick_goods_address": {    //【取货地址 和坐标】
            "id": 10,
            "type": 3,
            "user_id": 1166,
            "province_id": 23,
            "city_id": 285,
            "area_id": 2545,
            "address": null,
            "coordinate_x": null,
            "coordinate_y": null
        },
        "coordinate_list": {   //  【坐标列表】
            "receive_to_pick_goods": [    【确认接单坐标   到  取货坐标列表】
                {
                    "coordinate_x": "23.5555556",
                    "coordinate_y": "113.2222222",
                    "create_time": "2019-04-01 15:49:04"
                }
            ],
            "pick_goods_to_merchant": [  【取货坐标   到  完成坐标列表】
                {
                    "coordinate_x": "23.5555556",
                    "coordinate_y": "113.2222222",
                    "create_time": "2019-04-01 15:50:23"
                }
            ]
        }
    }
}
```  
</details>

[接口目录](#接口目录)

### 确认接单

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110302
$params   reqTime    
$params   checksum 
$params   mobile_id   全局  mobile_id   
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】
$params   order_id   【配送订单编号】
$params   coordinate_x   【坐标：X轴】
$params   coordinate_y   【坐标：Y轴】
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110302
    "responseCode": 0,
    "responseMessage": "ok",
    "data": [ ]
}
```  
</details>

[接口目录](#接口目录)

### 确认已经取货
 
> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110303
$params   reqTime    
$params   checksum 
$params   mobile_id   全局  mobile_id   
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】
$params   order_id   【配送订单编号】
$params   coordinate_x   【坐标：X轴】
$params   coordinate_y   【坐标：Y轴】
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110303
    "responseCode": 0,
    "responseMessage": "ok",
    "data": [ ]
}
```  
</details>

[接口目录](#接口目录)

### 确认配送完成
 
> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110304
$params   reqTime    
$params   checksum 
$params   mobile_id   全局  mobile_id   
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】
$params   order_id   【配送订单编号】
$params   coordinate_x   【坐标：X轴】
$params   coordinate_y   【坐标：Y轴】
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110304
    "responseCode": 0,
    "responseMessage": "ok",
    "data": [ ]
}
```  
</details>

[接口目录](#接口目录)

### 更新配送人员坐标

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110211
$params   reqTime    
$params   checksum 
$params   mobile_id   全局  mobile_id   
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】
$params   coordinate_x   【坐标：X轴】
$params   coordinate_y   【坐标：Y轴】         
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110304
    "responseCode": 0,
    "responseMessage": "ok",
    "data": [ ]
}
```  
</details>

[接口目录](#接口目录)

### 查找订单数量
 
> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110306
$params   reqTime    
$params   checksum 
$params   mobile_id   全局  mobile_id   
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】
$params   status   【订单状态】
$params   time_type   【时间类型固定值     today-今天    week- 本周,month-本月, year- 今年】
$params   start_time    【开始时间    和时间类型二选一】
$params   end_time  【结束时间  和时间类型二选一】                         
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110306
    "responseCode": 0,
    "responseMessage": "ok",
    "data": 100   【订单数量】
}
```  
</details>

[接口目录](#接口目录)

### 查找订单简易列表

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110307
$params   reqTime    
$params   checksum 
$params   mobile_id   全局  mobile_id   
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】
$params   page  【查询第几页】
$params   limit  【每页显示多少条记录】
$params   status   【订单状态】
$params   time_type   【时间类型固定值     today-今天    week- 本周,month-本月, year- 今年】
$params   start_time    【开始时间    和时间类型二选一】
$params   end_time  【结束时间  和时间类型二选一】
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110307,
    "responseCode": 0,
    "responseMessage": "ok",
    "data": {
        "list": [
            {
                "order_type": "kitchen",   【订单类型】
                "order_sn": "S201903301124445843"   【订单编号】
             【字段名称    ---  不够的可以叫开发加上】
            }
        ],
        "count": 3,  
        "total_page": 3,
        "current_page": 1,
        "pagesize": 1
    }
}
```  
</details>

[接口目录](#接口目录)

### 首页显示统计数据

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110308
$params   reqTime    
$params   checksum 
$params   mobile_id   全局  mobile_id   
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】         
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110308,
    "responseCode": 0,
    "responseMessage": "ok",
    "data": {
        "status_1_count": 3,    【待接收】
        "status_2_count": 0,【正在赶往取货地方】
        "status_5_count": 1,  【正在赶往商户】
        "status_10_count": 0,  【已经完成数】
        "today_income_money": 0  【今日收入】
    }
}
```  
</details>

[接口目录](#接口目录)

### 收益列表

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110309
$params   reqTime    
$params   checksum 
$params   mobile_id   全局  mobile_id   
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】
$params   time_type   【时间类型固定值     today-今天    week- 本周,month-本月, year- 今年】
$params   start_time    【开始时间    和时间类型二选一】
$params   end_time  【结束时间  和时间类型二选一】
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110309,
    "responseCode": 0,
    "responseMessage": "ok",
    "data": {
        "list": [
            {
                "id": 87,
                "user_id": 1,
                "module_type": "mall_order",   【订单类型】
                "used_type": 1,   【1-收入，-1（负一）-支出】
                "project_id": "MG201811020758293330",    【订单编号】
                "remark": "大神厨房【提成】",     【备注】
                "amount": "5.00",    【金额】
                "create_time": "2018-11-02 07:59:19",
                "full_name": "陈曦",
                "mobile": "13438259723",
                "module_type_name": null,        【订单类型名称】
                "used_type_name": "收入"       【类型名称】
            }
        ],
        "count": 1,
        "total_page": 1,
        "current_page": 1,
        "pagesize": 15,
        "income_money": 5    【总共收益】
    }
}
```  
</details>

[接口目录](#接口目录)

### 收益统计

> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110310
$params   reqTime    
$params   checksum 
$params   mobile_id   全局  mobile_id   
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】

$params   time_type   【时间类型固定值     today-今天    week- 本周,month-本月, year- 今年】
$params   start_time    【开始时间    和时间类型二选一】
$params   end_time  【结束时间  和时间类型二选一】
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110310,
    "responseCode": 0,
    "responseMessage": "ok",
    "data": 5    【总共收益】
}
```  
</details>

[接口目录](#接口目录)

### 查询登陆用户详情
 
> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110208
$params   reqTime    
$params   checksum 
$params   mobile_id   全局  mobile_id   
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110208,
    "responseCode": 0,
    "responseMessage": "ok",
    "data": {
        "id": 1,
        "user_id": 0,
        "status": 1,
        "work_status": 5,
        "full_name": "王超",
        "face": "\/uploads\/face\/201901\/f17622f006.jpg",
        "mobile": "13438259723",
        "service_area_json": "{\"service_area\":\"2545\",\"service_city\":\"285\",\"service_province\":\"23\",\"service_str\":\"\\u56db\\u5ddd\\u7701-\\u5df4\\u4e2d\\u5e02-\\u901a\\u6c5f\\u53bf\"}",
        "service_province": null,
        "service_city": 285,
        "service_area": 2545,
        "number": 0,
        "settlement_number": 0,
        "is_delete": 0,
        "create_time": "2019-01-15 09:34:51",
        "update_time": "2019-03-27 15:41:15",
        "status_name": "工作中",
        "work_status_name": "空闲中",
        "service_area_json_array": {
            "service_area": "2545",
            "service_city": "285",
            "service_province": "23",
            "service_str": "四川省-巴中市-通江县"
        }
    }
}
```  
</details>

[接口目录](#接口目录)

### 设置坐标
 
> 接口地址 /dispatch/index

> 请求方式 POST

<details>
<summary></summary>

> ** 传递参数 Request Data : **
```
$params   reqCode    110401
$params   reqTime    
$params   checksum 
$params   mobile_id   全局  mobile_id   
$params   session_id【登陆的时候 返回的值】
$params   session_security  【登陆的时候 返回的值】
$params   coordinate_x          纬度
$params   coordinate_y          经度
```

> ** 返回参数 Response Data : **
```
{
    "reqCode": 110401,
    "responseCode": 0,
    "responseMessage": "坐标设置成功",
    "data": ""
}
```  
</details>

[接口目录](#接口目录)


