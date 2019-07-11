# 美香厨APP接口文档
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
11000,              还有未支付的预购差价


10007,              登录错误

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

## 更新日志

### 2015.5.8 以前
> * 完成基本接口

### 2019.5.9
> * [评论订单](#评论订单)、[商品评论列表](#商品评论列表)
> * [商品详情](#商品详情) 添加关于评论的信息

### 2019.5.10
> * 更新 [取消订单](#取消订单) 参数变化：status_cancel_choice直接用 [订单取消原因列表](#订单取消原因列表) 取得的数据的ID
> * 添加 [订单取消原因列表](#订单取消原因列表)  
> * [商品列表](#商品列表)  [查询商品列表](#查询商品列表) [首页](#首页) [分类页面](#分类页面) 把规格库存为0的商品也全部显示出来

### 2019.5.13
> * [订单详情](#订单详情) [订单列表](#订单列表) status 10 已发货（待收货）分解为三个子状态：  
status 11 已发货（待收货）已分配订单 商家拣货完成状态  
status 12 已发货（待收货）已分配订单 配送员接单状态  
status 13 已发货（待收货）已分配订单 配送员取货状态

### 2019.5.16
> * [订单详情](#订单详情) 增加 送达时间、付款时间、拣货时间、接单时间、取货时间、完成时间、评论时间 默认为null
> * [订单详情](#订单详情) 增加 取消时间 默认为null

### 2019.5.23
> * [订单详情](#订单详情) [订单列表](#订单列表) status 20 已完成 分解为两个状态：  
status 21 已完成 未评论 状态  
status 22 已完成 已评论 状态  

### 2019.5.24
> * 添加 [H5首页3U](#H5首页3U) 
> * 更新 [首页](#首页) 添加 h5_url 字段
> * [系统消息列表](#系统消息列表) [系统消息详情](#系统消息详情) 添加 is_read 字段：unread 未读,read 已读 
> * 添加 [消息中心列表](#消息中心列表)  

### 2019.5.29
> * [首页](#首页) [购物车列表](#购物车列表) [用户详情](#用户详情) 添加 un_read_number 消息未读数           
> * 增加 [消息详情](#消息详情)

### 2019.6.4
> * 增加 [协议列表](#协议列表) [协议详情](#协议详情)

### 2019.6.12
> * [商品详情](#商品详情) [购物车列表](#购物车列表) 添加 起售数

### 2019.6.14
> * [首页](#首页) [专题详情](#专题详情) [查询商品列表](#查询商品列表) [商品列表](#商品列表) 添加 起售数、第一个规格起售数

### 2019.6.27
> * [首页](#首页) [分类页面](#分类页面) [商品列表](#商品列表) [查询商品列表](#查询商品列表) [商品详情](#商品详情) [订单确认页面](#订单确认页面) 添加 规格类型：标准的-std，预订的-advance
> * [订单确认页面](#订单确认页面) 添加 配送时间列表 arrive_time_list
> * [下单](#下单) 添加 输入参数 (配送时间 arrive_time) (开始配送时间 start_arrive_time) (结束配送时间 end_arrive_time)
> * [订单列表](#订单列表) [订单详情](#订单详情) 添加 (订单类型：标准的-std，预订-advance，预订补款-advance_son) (还未支付的尾款订单 wait_pay_order)

### 2019.6.28
>* [购物车列表](#购物车列表) 添加 购物车状态：normal 正常 lacked 失效
>* [支付订单](#支付订单) 添加 异常状态码 11000 还有未支付的预购差价,当出现异常状态时会附带需要支付的订单数据 wait_pay_order

###2019.7.11
>* [商品详情](#商品详情) 添加 是否已加入常购清单状态：是-joined 否-not_joined
>* 增加 [加入常购清单](#加入常购清单) [已加入的常购清单列表](#已加入的常购清单列表)  

## 接口目录

### 登录相关

[请求 mobile_id](#请求mobile_id)  

[发送验证码](#发送验证码)  
   
[密码登录](#密码登录)  

[验证码登录](#验证码登录) 

[找回密码](#找回密码) 

### 用户相关

[用户详情](#用户详情)  

### 商品相关

[首页](#首页)

[分类页面](#分类页面)  

[分类页面V2](#分类页面V2)  

[二级分类](#二级分类)  

[商品列表](#商品列表)  

[查询商品列表](#查询商品列表)  

[热门查询词列表](#热门查询词列表)  

[商品详情](#商品详情)  

[加入常购清单](#加入常购清单)  

[已加入的常购清单列表](#已加入的常购清单列表)  

[商品评论列表](#商品评论列表)  

### 专题相关

[专题详情](#专题详情)

[关于详情](#关于详情)

### 收藏相关

[收藏商品](#收藏商品)

[已收藏的商品列表](#已收藏的商品列表)
  
[清空商品收藏](#清空商品收藏)  

### 购物车相关

[购物车列表](#购物车列表)  

[计算购物车](#计算购物车)  

[批量删除购物车](#批量删除购物车)  

### 订单相关

[订单确认页面](#订单确认页面)  

[检测规格库存](#检测规格库存) 

[下单](#下单)  

[支付订单](#支付订单)  

[订单列表](#订单列表)  

[订单详情](#订单详情)  

[订单取消原因列表](#订单取消原因列表)  

[取消订单](#取消订单)  

[删除订单](#删除订单)  

[订单日志列表](#订单日志列表)  

[订单追踪列表](#订单追踪列表)  

[评论订单](#评论订单) 

### 消息相关

[消息详情](消息详情)

[消息中心列表](#消息中心列表)  

[系统消息列表](#系统消息列表)  

[系统消息详情](#系统消息详情)  

[常见问题列表](#常见问题列表)  

[常见问题详情](#常见问题详情)  

### 留言相关

[写留言](#写留言)  

### 版本相关

[ios版本](#ios版本)  

[android版本](#android版本)  

### 我的相关

[资质条款](#资质条款)  

### H5

[H5首页3U](#H5首页3U)

## 接口

### 请求mobile_id

> 接口地址 /plugin/get_mobile_id 

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      platform            【ios，android】
string      device_id           【设备号】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": 0,
    "responseMessage": "ok",
    "data": {
        "mobile_id": "ios_V3ERydy5Kqcv"
    }
}

```  
[接口目录](#接口目录)

### 发送验证码

> 接口地址 /plugin/verify_code

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile          【用户手机号】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": 0,
    "responseMessage": "发送成功",
    "data": {}
}
{
    "responseCode": 30001,
    "responseMessage": "短信发送失败",
    "data": {}
}
```  
[接口目录](#接口目录)

### 密码登录

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

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "mobile_id": "ios_ygPVpZKqO8TK",
        "session_id": "81e0712eb61ad88da7a2e47f8e550e15",
        "session_security": "VTJGc2RHVmtYMStyKzZvQVFpTjVoSE1RZVFlZGd6S0ZYcnNXYkRUemJnMzR3OTAvVWxJM1k3Q09XUlBYUEFobmVTZGZJUkprMzdUVDVGekVjWW5GWVB4amFNd3NuOTBvakNxcU9QRHcxVXowTzJkd1BkMEtZdTYxUlpDY3F0MHhQSnpEUHdXSzEwUEJzK1NyOE9KUGpBPT0",
        "user_info": {                          【用户信息】
            "id": 1185,                           【用户编号】
            "nickname": null,                       【用户昵称】
            "mobile": "18381082760",                   【用户手机（登录用的手机）】
            "extension_title": "通江店",               【商户名】
            "extension_tel": "18381082766",             【商户电话】
            "extension_logo": "\/uploads\/images\/20190402\/55e104138963bf0d4dc63c8821cc1b56.jpg",          【商户logo】
            "extension_province_name": "天津市",               【商户省名】
            "extension_city_name": "天津市",                   【商户市名】
            "extension_area_name": "河东区",                   【商户区名】
            "extension_address": "红星路四段"                    【商户地址】
        }
    }
}
```  
[接口目录](#接口目录)

### 验证码登录

> 接口地址 /user/login_via_sms

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      mobile          【用户手机号】
string      verify_code        【验证码】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "mobile_id": "ios_ygPVpZKqO8TK",
        "session_id": "81e0712eb61ad88da7a2e47f8e550e15",
        "session_security": "VTJGc2RHVmtYMStyKzZvQVFpTjVoSE1RZVFlZGd6S0ZYcnNXYkRUemJnMzR3OTAvVWxJM1k3Q09XUlBYUEFobmVTZGZJUkprMzdUVDVGekVjWW5GWVB4amFNd3NuOTBvakNxcU9QRHcxVXowTzJkd1BkMEtZdTYxUlpDY3F0MHhQSnpEUHdXSzEwUEJzK1NyOE9KUGpBPT0",
        "user_info": {                          【用户信息】
            "id": 1185,                           【用户编号】
            "nickname": null,                       【用户昵称】
            "mobile": "18381082760",                   【用户手机（登录用的手机）】
            "extension_title": "通江店",               【商户名】
            "extension_tel": "18381082766",             【商户电话】
            "extension_logo": "\/uploads\/images\/20190402\/55e104138963bf0d4dc63c8821cc1b56.jpg",          【商户logo】
            "extension_province_name": "天津市",               【商户省名】
            "extension_city_name": "天津市",                   【商户市名】
            "extension_area_name": "河东区",                   【商户区名】
            "extension_address": "红星路四段"                    【商户地址】
        }
    }
}
{
    "responseCode": 30001,
    "responseMessage": "验证码未获取或者超时!",
    "data": ""
}
```  
[接口目录](#接口目录)

### 找回密码

> 接口地址 /user/find_password

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      mobile          【用户手机号】
string      password            【新密码】
string      conn_password       【重复密码】
string      verify_code        【验证码】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": 0,
    "responseMessage": "找回密码成功",
    "data": {}
}
{
    "responseCode": 30001,
    "responseMessage": "验证码错误, 请重新发送!",
    "data": {}
}
{
    "responseCode": 30001,
    "responseMessage": "两次密码不一致",
    "data": {}
}
```  
[接口目录](#接口目录)

### 用户详情
 
> 接口地址 /user/user

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
         "user_info": {                          【用户信息】
            "id": 1185,                           【用户编号】
            "nickname": null,                       【用户昵称】
            "mobile": "18381082760",                   【用户手机（登录用的手机）】
            "extension_title": "通江店",               【商户名】
            "extension_tel": "18381082766",             【商户电话】
            "extension_logo": "\/uploads\/images\/20190402\/55e104138963bf0d4dc63c8821cc1b56.jpg",          【商户logo】
            "extension_province_name": "天津市",               【商户省名】
            "extension_city_name": "天津市",                   【商户市名】
            "extension_area_name": "河东区",                   【商户区名】
            "extension_address": "红星路四段"                    【商户地址】
        },
        "un_read_number": 2             【消息未读数】          
    }
}
```  
[接口目录](#接口目录)

### 首页

> 接口地址 /navigation/index

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int/null    random_number                 【获取随机商品列表个数（默认后台配置）】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "area_name": "河东区",                 【地区名称】
        "top_object_list": [                 【上部专题列表】
            {
                "id": 1,                    【专题ID】
                "litpic": "\/uploads\/goods\/cover\/20190404\/d94ccbd5f7e678c3a21c2c473a8dd4cf.jpg"             【专题图片】
            },
            {
                "id": 2,
                "litpic": "\/uploads\/goods\/cover\/20190404\/d94ccbd5f7e678c3a21c2c473a8dd4cf.jpg"
            },
            {
                "id": 3,
                "litpic": "\/uploads\/goods\/cover\/20190404\/d94ccbd5f7e678c3a21c2c473a8dd4cf.jpg"
            }
        ],
        "ad_object": {                      【广告专题】
            "id": 4,
            "litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190404\/d94ccbd5f7e678c3a21c2c473a8dd4cf.jpg",
            "h5_url": "http://www.ypvpa.localhost/index.php/kitchen_api/h5/index_3u.html"                               【专题url】
        },
        "mid_object_list": [                【中部专题列表】
            {
                "id": 5,                            【专题ID】
                "litpic": "\/uploads\/goods\/cover\/20190404\/d94ccbd5f7e678c3a21c2c473a8dd4cf.jpg"             【专题图片】
            },
            {
                "id": 6,
                "litpic": "\/uploads\/goods\/cover\/20190404\/d94ccbd5f7e678c3a21c2c473a8dd4cf.jpg"
            },
            {
                "id": 7,
                "litpic": "\/uploads\/goods\/cover\/20190404\/d94ccbd5f7e678c3a21c2c473a8dd4cf.jpg"
            }
        ],
        "good_cate_list": [                                 【一级分类列表】
            {
                "id": 1,                                    【分类ID】                                  
                "cate_name": "川菜",                        【分类名】
                "icon": "http://www.ypvpa.localhost/uploads/goods/cate_icon/20190326/df2701805309a17cd2bc47a3ac4d1b92.png"          【分类图标】
            },
            {
                "id": 4,
                "cate_name": "快乐水",
                "icon": ""
            },
            {
                "id": 6,
                "cate_name": "面包",
                "icon": ""
            },
            {
                "id": 10,
                "cate_name": "硬件",
                "icon": "http://www.ypvpa.localhost/uploads/goods/cate_icon/20190407/c5df1368a9ad6fe4c3057e711c0a4992.jpg"
            },
            {
                "id": 1,
                "cate_name": "更多",
                "icon": "http:\/\/www.ypvpa.localhost\/statics\/kitchen_api\/images\/default_all_goods_cate.png"
            }
        ],
        "good_list": [
            {
                "id": 11,           【商品ID】
                "litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190329\/fa407a4bfb5bcb15700f8fa44dd32a60.png",        【商品封面图】
                "title": "炒土豆丝",        【商品名】
                "first_spec_id": 5,         【第一个规格ID】
                "first_spec_name": "2斤",    【第一个规格单位】
                "first_spec_unit": "kg",    【第一个规格单位注释】
                "first_spec_price": "0.01", 【第一个规格售价】
                "first_spec_source_price": "20.00",     【第一个规格原始标价】
                "first_spec_min_buy_number": 1,         【第一个规格起售数】
                "spec_list": [              【规格列表】
                    {
                        "id": 5,            【规格ID】
                        "price": "0.01",    【规格售价】
                        "source_price": "20.00",    【规格原始标价】
                        "name": "2斤",       【规格单位】
                        "unit": "kg",        【规格单位注释】
                        "stock_number": 222,                【规格库存】
                        "min_buy_number": 1,                【起售数】
                        "type": "std",                      【规格类型：标准的-std，预订的-advance】
                        "cart_buy_number": 0    【此规格的购物车购买数量】
                    },
                    {
                        "id": 6,
                        "price": "0.01",
                        "source_price": "38.00",
                        "name": "半斤",
                        "unit": "500g",
                        "stock_number": 222,                
                        "min_buy_number": 1,
                        "type": "std", 
                        "cart_buy_number": 0
                    }
                ],
                "spec_count": 2,                        【规格数量】
                "first_spec_car_buy_number": 0          【第一个规格购买数量】
            },
            {
                "id": 12,
                "litpic": "\/uploads\/goods\/cover\/20190404\/d94ccbd5f7e678c3a21c2c473a8dd4cf.jpg",
                "title": "百事可乐",
                "first_spec_id": 9,
                "first_spec_name": "杯",
                "first_spec_unit": "1杯",
                "first_spec_price": "5.00",
                "first_spec_source_price": "20.00",
                "first_spec_min_buy_number": 1, 
                "spec_list": [
                    {
                        "id": 9,
                        "price": "5.00",
                        "source_price": "20.00",
                        "name": "杯",
                        "unit": "1杯",
                        "stock_number": 2,
                        "min_buy_number": 1,
                        "type": "advance", 
                        "cart_buy_number": 1
                    },
                    {
                        "id": 11,
                        "price": "2.00",
                        "source_price": "1.00",
                        "name": "1",
                        "unit": "1",
                        "stock_number": 2,
                        "min_buy_number": 1,
                        "type": "advance", 
                        "cart_buy_number": 1
                    }
                ],
                "spec_count": 2,
                "first_spec_car_buy_number": 1
            }
        ],
        "cart_all_spec_number": 4,      【购物车的规格数量和】
        "cart_all_buy_number": 5,      【购物车的规格购买数量和】
        "cart_all_price": "7.03",      【购物车的购物车总金额】
        "un_read_number": 2             【消息未读数】          
    }
}

{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "area_name": "河东区",
        "top_object_list": [],
        "ad_object": {},
        "mid_object_list": [],
        "good_cate_list": [
            {
                "id": 1,
                "cate_name": "川菜",
                "icon": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cate_icon\/20190326\/df2701805309a17cd2bc47a3ac4d1b92.png"
            },
            {
                "id": 4,
                "cate_name": "快乐水",
                "icon": ""
            },
            {
                "id": 6,
                "cate_name": "面包",
                "icon": ""
            },
            {
                "id": 10,
                "cate_name": "硬件",
                "icon": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cate_icon\/20190407\/c5df1368a9ad6fe4c3057e711c0a4992.jpg"
            }
        ],
        "good_list": [],
        "cart_all_spec_number": 4,
        "cart_all_buy_number": 5,
        "cart_all_price": "7.03"
    }
}
```  
[接口目录](#接口目录)

### 分类页面

> 接口地址 /navigation/sort

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int/null    limit                   【分页数(默认后台配置)】        
int/null    page                    【页数(默认1)】
int/null    cate_id                 【分类ID(默认选择第一个)】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "good_cate_list": [                                 【一级分类列表】
            {
                "id": 1,                                    【分类ID】                                  
                "cate_name": "川菜",                        【分类名】
                "icon": "http://www.ypvpa.localhost/uploads/goods/cate_icon/20190326/df2701805309a17cd2bc47a3ac4d1b92.png"          【分类图标】
            },
            {
                "id": 4,
                "cate_name": "快乐水",
                "icon": ""
            },
            {
                "id": 6,
                "cate_name": "面包",
                "icon": ""
            },
            {
                "id": 10,
                "cate_name": "硬件",
                "icon": "http://www.ypvpa.localhost/uploads/goods/cate_icon/20190407/c5df1368a9ad6fe4c3057e711c0a4992.jpg"
            }
        ],
        "default_cate_id": 1,                       【一级分类默认ID】
        "son_good_cate_list": [                     【二级分类列表】
            {
                "id": 2,                            【分类ID】
                "cate_name": "炒菜",                  【分类名】
                "icon": "http://www.ypvpa.localhost/uploads/goods/cate_icon/20190326/2178d9098ee0fbdb635e2f173b4065f1.png"          【分类图标】
            },
            {
                "id": 3,
                "cate_name": "烧菜",
                "icon": ""
            }
        ],
        "default_son_cate_id": 2,                   【二级分类默认ID】
        "good_list": {                  【商品分类列表】
            "list": [                   【分页列表】
                {
                    "id": 11,           【商品ID】
                    "litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190329\/fa407a4bfb5bcb15700f8fa44dd32a60.png",        【商品封面图】
                    "title": "炒土豆丝",        【商品名】
                    "first_spec_id": 5,         【第一个规格ID】
                    "first_spec_name": "2斤",    【第一个规格单位】
                    "first_spec_unit": "kg",    【第一个规格单位注释】
                    "first_spec_price": "0.01", 【第一个规格售价】
                    "first_spec_source_price": "20.00",     【第一个规格原始标价】
                    "first_spec_min_buy_number": 1,         【第一个规格起售数】
                    "spec_count": 2,                【包含的规格数量】
                    "spec_list": [              【规格列表】
                        {
                            "id": 5,            【规格ID】
                            "price": "0.01",    【规格售价】
                            "source_price": "20.00",    【规格原始标价】
                            "name": "2斤",       【规格单位】
                            "unit": "kg",        【规格单位注释】
                            "stock_number": 222,                【规格库存】
                            "min_buy_number": 1,            【起售数】
                            "type": "std",                      【规格类型：标准的-std，预订的-advance】
                            "cart_buy_number": 0    【此规格的购物车购买数量】
                        },
                        {
                            "id": 6,
                            "price": "0.01",
                            "source_price": "38.00",
                            "name": "半斤",
                            "unit": "500g",
                            "stock_number": 222,                
                            "min_buy_number": 1, 
                            "type": "std", 
                            "cart_buy_number": 0
                        }
                    ],
                    "spec_count": 2,                        【规格数量】
                    "first_spec_car_buy_number": 0          【第一个规格购买数量】
                },
                {
                    "id": 14,
                    "litpic": "",
                    "title": "回锅肉",
                    "first_spec_id": 14,
                    "first_spec_name": "3213",
                    "first_spec_unit": "3213",
                    "first_spec_price": "213.00",
                    "first_spec_source_price": "2131.00",
                    "first_spec_min_buy_number": 1,  
                    "spec_count": 3,
                    "spec_list": [
                        {
                            "id": 13,
                            "price": "11.00",
                            "source_price": "22.00",
                            "name": "22",
                            "unit": "22",
                            "stock_number": 222,                
                            "min_buy_number": 1, 
                            "type": "std", 
                            "cart_buy_number": 0
                        },
                        {
                            "id": 14,
                            "price": "213.00",
                            "source_price": "2131.00",
                            "name": "3213",
                            "unit": "3213",
                            "stock_number": 222,                
                            "min_buy_number": 1, 
                            "type": "std", 
                            "cart_buy_number": 0
                        },
                        {
                            "id": 15,
                            "price": "3123.00",
                            "source_price": "131.00",
                            "name": "3123",
                            "unit": "3123",
                            "stock_number": 222,                
                            "min_buy_number": 1, 
                            "type": "std", 
                            "cart_buy_number": 0
                        }
                    ],
                    "spec_count": 2,                        
                    "first_spec_car_buy_number": 0
                }
            ],
            "count": 2,         【列表总数】
            "total_page": 1,    【分页总数】
            "current_page": 1,  【当前页】
            "pagesize": 2       【每页数量，与limit一致】
        },
        "cart_all_spec_number": 7,      【购物车的规格数量和】
        "cart_all_buy_number": 77,      【购物车的规格购买数量和】
        "cart_all_price": "248.03",      【购物车的购物车总金额】
        "un_read_number": 2             【消息未读数】          
    }
}
```  
[接口目录](#接口目录)

### 分类页面V2

> 接口地址 /navigation/sort_v2

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "good_cate_list": [                 【一级分类列表】
            {
                "id": 1,                    【分类ID】
                "cate_name": "川菜",          【分类名】
                "icon": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cate_icon\/20190326\/df2701805309a17cd2bc47a3ac4d1b92.png",      【分类图标】
                "son_good_cate_list": [         【二级分类列表】
                    {
                        "id": 2,                【分类ID】
                        "cate_name": "炒菜",      【分类名】
                        "icon": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cate_icon\/20190326\/2178d9098ee0fbdb635e2f173b4065f1.png"   【分类图标】
                    },
                    {
                        "id": 3,
                        "cate_name": "烧菜",
                        "icon": ""
                    }
                ]
            },
            {
                "id": 4,
                "cate_name": "快乐水",
                "icon": "",
                "son_good_cate_list": [
                    {
                        "id": 5,
                        "cate_name": "可乐",
                        "icon": ""
                    }
                ]
            },
            {
                "id": 6,
                "cate_name": "面包",
                "icon": "",
                "son_good_cate_list": [
                    {
                        "id": 7,
                        "cate_name": "牛角",
                        "icon": ""
                    },
                    {
                        "id": 8,
                        "cate_name": "甜甜圈",
                        "icon": ""
                    },
                    {
                        "id": 9,
                        "cate_name": "泡芙",
                        "icon": ""
                    }
                ]
            },
            {
                "id": 10,
                "cate_name": "硬件",
                "icon": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cate_icon\/20190407\/c5df1368a9ad6fe4c3057e711c0a4992.jpg",
                "son_good_cate_list": []
            }
        ]
    }
}

{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "good_cate_list": [
            {
                "id": 1,
                "cate_name": "川菜",
                "icon": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cate_icon\/20190326\/df2701805309a17cd2bc47a3ac4d1b92.png",
                "son_good_cate_list": []
            },
            {
                "id": 4,
                "cate_name": "快乐水",
                "icon": "",
                "son_good_cate_list": []
            },
            {
                "id": 6,
                "cate_name": "面包",
                "icon": "",
                "son_good_cate_list": []
            },
            {
                "id": 10,
                "cate_name": "硬件",
                "icon": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cate_icon\/20190407\/c5df1368a9ad6fe4c3057e711c0a4992.jpg",
                "son_good_cate_list": []
            }
        ]
    }
}
```  
[接口目录](#接口目录)

### 二级分类

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

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "son_good_cate_list": [
            {
                "id": 2,                        【分类ID】
                "cate_name": "炒菜",              【分类名】
                "icon": "http://www.ypvpa.localhost/uploads/goods/cate_icon/20190326/2178d9098ee0fbdb635e2f173b4065f1.png"          【分类图标】
            },
            {
                "id": 3,
                "cate_name": "烧菜",
                "icon": ""
            }
        ]
    }
}

{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "son_good_cate_list": []
    }
}
```  
[接口目录](#接口目录)

### 商品列表

> 接口地址 /good/good_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int/null    cate_id                 【分类ID(默认0 表示所有分类ID)】
int/null    limit                   【分页数(默认后台配置)】        
int/null    page                    【页数(默认1)】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "good_list": {                  【商品分类列表】
            "list": [                   【分页列表】
                {
                    "id": 11,           【商品ID】
                    "litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190329\/fa407a4bfb5bcb15700f8fa44dd32a60.png",        【商品封面图】
                    "title": "炒土豆丝",        【商品名】
                    "first_spec_id": 5,         【第一个规格ID】
                    "first_spec_name": "2斤",    【第一个规格单位】
                    "first_spec_unit": "kg",    【第一个规格单位注释】
                    "first_spec_price": "0.01", 【第一个规格售价】
                    "first_spec_source_price": "20.00",     【第一个规格原始标价】
                    "first_spec_min_buy_number": 1,         【第一个规格起售数】
                    "spec_count": 2,                【包含的规格数量】
                    "spec_list": [              【规格列表】
                        {
                            "id": 5,            【规格ID】
                            "price": "0.01",    【规格售价】
                            "source_price": "20.00",    【规格原始标价】
                            "name": "2斤",       【规格单位】
                            "unit": "kg",        【规格单位注释】
                            "stock_number": 0,      【规格库存】
                            "min_buy_number": 1,    【起售数】
                            "type": "std",                      【规格类型：标准的-std，预订的-advance】
                            "cart_buy_number": 15   【此规格的购物车购买数量】       
                        },
                        {
                            "id": 6,
                            "price": "0.01",
                            "source_price": "38.00",
                            "name": "半斤",
                            "unit": "500g",
                            "stock_number": 0,    
                            "min_buy_number": 1,
                            "type": "std", 
                            "cart_buy_number": 0
                        }
                    ],
                    "first_spec_car_buy_number": 0         【第一个规格购买数量】
                },
                {
                    "id": 14,
                    "litpic": "",
                    "title": "回锅肉",
                    "first_spec_id": 14,
                    "first_spec_name": "3213",
                    "first_spec_unit": "3213",
                    "first_spec_price": "213.00",
                    "first_spec_source_price": "2131.00",
                    "first_spec_min_buy_number": 1,
                    "spec_count": 3,
                    "spec_list": [
                        {
                            "id": 13,
                            "price": "11.00",
                            "source_price": "22.00",
                            "name": "22",
                            "unit": "22",
                            "stock_number": 0,    
                            "min_buy_number": 1,
                            "type": "advance", 
                            "cart_buy_number": 0
                        },
                        {
                            "id": 14,
                            "price": "213.00",
                            "source_price": "2131.00",
                            "name": "3213",
                            "unit": "3213",
                            "stock_number": 0,    
                            "min_buy_number": 1,
                            "type": "advance", 
                            "cart_buy_number": 0
                        },
                        {
                            "id": 15,
                            "price": "3123.00",
                            "source_price": "131.00",
                            "name": "3123",
                            "unit": "3123",
                            "stock_number": 0,    
                            "min_buy_number": 1,
                            "type": "advance", 
                            "cart_buy_number": 0
                        }
                    ],
                }
            ],
            "count": 2,         【列表总数】
            "total_page": 1,    【分页总数】
            "current_page": 1,  【当前页】
            "pagesize": 2       【每页数量，与limit一致】
        },
        "cart_all_spec_number": 6,      【购物车的规格数量和】
        "cart_all_buy_number": 45,      【购物车的规格购买数量和】
        "cart_all_price": "109.00",      【购物车的购物车总金额】
    }
}

{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "good_list": {
            "list": [],
            "count": 0,
            "total_page": 0,
            "current_page": 1,
            "pagesize": 2
        }
    }
}
```  
[接口目录](#接口目录)

### 查询商品列表
 
> 接口地址 /good/search_good_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int/null    limit                   【分页数(默认后台配置)】        
int/null    page                    【页数(默认1)】
string      search                  【查询字符串】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "good_list": {                  【商品分类列表】
            "list": [                   【分页列表】
                {
                    "id": 11,           【商品ID】
                    "litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190329\/fa407a4bfb5bcb15700f8fa44dd32a60.png",        【商品封面图】
                    "title": "炒土豆丝",        【商品名】
                    "first_spec_id": 5,         【第一个规格ID】
                    "first_spec_name": "2斤",    【第一个规格单位】
                    "first_spec_unit": "kg",    【第一个规格单位注释】
                    "first_spec_price": "0.01", 【第一个规格售价】
                    "first_spec_source_price": "20.00",     【第一个规格原始标价】
                    "first_spec_min_buy_number": 1,         【第一个规格起售数】
                    "spec_count": 2,                【包含的规格数量】
                    "spec_list": [              【规格列表】
                        {
                            "id": 5,            【规格ID】
                            "price": "0.01",    【规格售价】
                            "source_price": "20.00",    【规格原始标价】
                            "name": "2斤",       【规格单位】
                            "unit": "kg",        【规格单位注释】
                            "stock_number": 0,      【规格库存】
                            "min_buy_number": 1,    【起售数】
                            "type": "std",                      【规格类型：标准的-std，预订的-advance】
                            "cart_buy_number": 15   【此规格的购物车购买数量】       
                        },
                        {
                            "id": 6,
                            "price": "0.01",
                            "source_price": "38.00",
                            "name": "半斤",
                            "unit": "500g",
                            "min_buy_number": 1, 
                            "type": "std",                
                            "cart_buy_number": 0
                        }
                    ],
                    "first_spec_car_buy_number": 0         【第一个规格购买数量】
                },
                {
                    "id": 14,
                    "litpic": "",
                    "title": "回锅肉",
                    "first_spec_id": 14,
                    "first_spec_name": "3213",
                    "first_spec_unit": "3213",
                    "first_spec_price": "213.00",
                    "first_spec_source_price": "2131.00",
                    "first_spec_min_buy_number": 1,
                    "spec_count": 3,
                    "spec_list": [
                        {
                            "id": 13,
                            "price": "11.00",
                            "source_price": "22.00",
                            "name": "22",
                            "unit": "22",
                            "min_buy_number": 1, 
                            "type": "std",                
                            "cart_buy_number": 0
                        },
                        {
                            "id": 14,
                            "price": "213.00",
                            "source_price": "2131.00",
                            "name": "3213",
                            "unit": "3213",
                            "min_buy_number": 1, 
                            "type": "std",                
                            "cart_buy_number": 0
                        },
                        {
                            "id": 15,
                            "price": "3123.00",
                            "source_price": "131.00",
                            "name": "3123",
                            "unit": "3123",
                            min_buy_number": 1, 
                            "type": "std",                
                            "cart_buy_number": 0
                        }
                    ],
                }
            ],
            "count": 2,         【列表总数】
            "total_page": 1,    【分页总数】
            "current_page": 1,  【当前页】
            "pagesize": 2       【每页数量，与limit一致】
        },
        "cart_all_spec_number": 6,      【购物车的规格数量和】
        "cart_all_buy_number": 45,      【购物车的规格购买数量和】
        "cart_all_price": "109.00",      【购物车的购物车总金额】
    }
}

{
    "responseCode": "0",
    "responseMessage": "查询成功",
    "data": {
        "good_list": {
            "list": [],
            "count": 0,
            "total_page": 0,
            "current_page": 1,
            "pagesize": 2
        },
        "cart_all_spec_number": 4,
        "cart_all_buy_number": 5,
        "cart_all_price": "7.03"
    }
}
```  
[接口目录](#接口目录)

### 热门查询词列表
 
> 接口地址 /good/hot_search_word_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int/null    number              【列表显示数量(默认后台配置)】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
       "hot_search_word_list": [        【热词列表】
            {
               "search_count": 2,      【查询次数】            
               "content": "海尔"         【查询内容】
            },
            {
                "search_count": 1,
                "content": "花椒"
            },
            {
                "search_count": 1,
                "content": "冰箱"
            }
        ]
    }
}
```  
[接口目录](#接口目录)

### 商品详情

> 接口地址 /good/good

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int         id              【商品ID】          
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "good": {                           【商品信息】
            "id": 12,                       【商品ID】
            "title": "百事可乐",            【商品标题】
            "description": "百事可乐",      【商品说明】
            "body": "<p>\r\n\t百事可乐fdsafa\r\n<\/p>",     【图文详情】
            "pic_list": [                   【轮播展示图】
                "http:\/\/www.ypvpa.localhost\/uploads\/goods\/album\/20190404\/e8003f338aa604704117dcc2ea1f0f8d.jpg",
                "http:\/\/www.ypvpa.localhost\/uploads\/goods\/album\/20190404\/5e323f178d3e77194d0be265dd6985a2.jpg"
            ],
            "spec_list": [                  【规格列表】
                {
                    "id": 9,                【规格ID】
                    "price": "5.00",        【规格售价】
                    "source_price": "20.00",        【规格原始标价】
                    "name": "杯",            【规格单位】
                    "unit": "1杯",            【规格单位注释】
                    "stock_number": 50,          【规格库存】
                    "type": "std",                      【规格类型：标准的-std，预订的-advance】
                    "min_buy_number": 1,         【起售数】
                    "join_status": "joined"         【是否已加入常购清单状态：是-joined 否-not_joined】
                },
                {
                    "id": 11,
                    "price": "2.00",
                    "source_price": "1.00",
                    "name": "1",
                    "unit": "1",
                    "stock_number": 20,
                    "type": "std", 
                    "min_buy_number": 1,
                    "join_status": "not_joined"
                }
            ],
            "distribution_price": 0,            【运费】
            "monthly_order_number": 0,           【月销量】
            "love_status": "loved"              【收藏状态：loved 已收藏 unloved 未收藏】
        },
        "good_evaluation_count": 1,             【商品评论总数】
        "good_evaluation_list": [
            {
                "evaluation": "66662323",           【评论】
                "good_star_number": 5,              【评论商品星数】
                "create_time": "2019-05-09 16:14:55",           【评论时间】
                "good_title": "百事可乐",               【商品标题】
                "spec_name": "1",                       【商品规格】
                "extension_title": "通江店2",              【商户名】
                "extension_logo": ""                        【商户图标】
            },
            {
                "evaluation": "66662323",
                "good_star_number": 5,
                "create_time": "2019-05-09 15:11:23",
                "good_title": "百事可乐",
                "spec_name": "1",
                "extension_title": "18381082766",
                "extension_logo": ""
            }
        ],
        "cart_all_spec_number": 4,      【购物车的规格数量和】
        "cart_all_buy_number": 18,      【购物车的规格购买数量和】
        "cart_all_price": "22.00",      【购物车的购物车总金额】
        "user_agent": {                 【代理信息】
            "tel": "18381082766"            【代理联系方式】
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "good": {},
        "cart_all_spec_number": 4,
        "cart_all_buy_number": 18,
        "cart_all_price": "22.00",
        "user_agent": {
            "tel": "18381082766"
        }
    }
}
```  
[接口目录](#接口目录)

### 加入常购清单
 
> 接口地址 /good/join_buy_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int         spec_id                        【规格ID】                         
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "加入常购清单成功",
    "data": {
        "spec_id": 64,
        "join_status": "joined"
    }
}
{
    "responseCode": "0",
    "responseMessage": "取消常购清单成功",
    "data": {
        "spec_id": 64,
        "join_status": "not_joined"
    }
}
{
    "responseCode": "10001",
    "responseMessage": "规格不存在",
    "data": {}
}
```  
[接口目录](#接口目录)

### 已加入的常购清单列表

> 接口地址 /good/joined_buy_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "buy_list": [                           【清单列表】
            {
                "spec_id": 171,                 【规格ID】       
                "buy_number": 1,                【购买数量增量】
                "good_id": 12,                      【商品ID】
                "good_title": "回锅肉",             【商品名】
                "good_litpic": "http:\/\/www.ypvpa.localhost",      【商品图片】
                "name": "2斤",                   【规格单位】
                "unit": "kg"                    【规格单位注释】
                "source_price": "22.00",            【规格原始标价】
                "price": "11.00",                    【规格售价】
                "stock_number": 100,                   【规格库存】
                "min_buy_number": 2,                      【起售数】 
                "status": "normal"                      【状态：normal 正常 lacked 失效】
            },
            {
                "spec_id": 64,
                "buy_number": 8,
                "good_id": 3,
                "good_title": "中粮米川府藏香",
                "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/30a47f62e9bd49a1101592f4f95f493a.jpg",
                "name": "50斤",
                "unit": "袋",
                "price": "115.00",
                "source_price": "115.00",
                "stock_number": 85,
                "min_buy_number": 1,
                "status": "normal"
            },
            {
                "spec_id": 62,
                "buy_number": 2,
                "good_id": 7,
                "good_title": "福掌柜超香菜籽油20L",
                "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190407/d9d29b632018464aad8e2828fbd42e25.jpg",
                "name": "20L",
                "unit": "件",
                "price": "170.00",
                "source_price": "180.00",
                "stock_number": 42,
                "min_buy_number": 1,
                "status": "normal"
            }
        ]
    }
}
```  
[接口目录](#接口目录)

### 商品评论列表

> 接口地址 /good/good_evaluation_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int         goods_id              【商品ID】          
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "list": [                                   【评论列表】
            {
                "evaluation": "66662323",           【评论】
                "good_star_number": 5,              【评论商品星数】
                "create_time": "2019-05-09 16:14:55",           【评论时间】
                "good_title": "百事可乐",               【商品标题】
                "spec_name": "1",                       【商品规格】
                "extension_title": "通江店2",              【商户名】
                "extension_logo": ""                        【商户图标】
            },
            {
                "evaluation": "66662323",
                "good_star_number": 5,
                "create_time": "2019-05-09 15:11:23",
                "good_title": "百事可乐",
                "spec_name": "1",
                "extension_title": "通江店2",
                "extension_logo": ""
            },
            {
                "evaluation": "此用户没有填写评价。",
                "good_star_number": 5,
                "create_time": "2019-05-09 12:52:12",
                "good_title": "百事可乐",
                "spec_name": "1",
                "extension_title": "通江店",
                "extension_logo": "http:\/\/www.ypvpa.localhost\/uploads\/images\/20190402\/55e104138963bf0d4dc63c8821cc1b56.jpg"
            },
            {
                "evaluation": "商品非常好！\nfdasf",
                "good_star_number": 5,
                "create_time": "2019-05-08 17:58:04",
                "good_title": "百事可乐",
                "spec_name": "1",
                "extension_title": "通江店",
                "extension_logo": "http:\/\/www.ypvpa.localhost\/uploads\/images\/20190402\/55e104138963bf0d4dc63c8821cc1b56.jpg"
            }
        ],
        "count": 4,                【列表总数】
        "total_page": 1,           【分页总数】
        "current_page": 1,          【当前页】    
        "pagesize": 5               【每页数量，与limit一致】
    }
}

{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "list": [],
        "count": 0,
        "total_page": 0,
        "current_page": 1,
        "pagesize": 5
    }
}
```  
[接口目录](#接口目录)

### 专题详情

> 接口地址 /object/object

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int         id                      【专题ID】
int/null    limit                   【商品列表分页数(默认后台配置)】        
int/null    page                    【商品列表页数(默认1)】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "object": {                                     【专题信息】
            "id": 1,                                    【专题ID】
            "title": "111",                             【专题名称】
            "banner_pic": "\/uploads\/goods\/cover\/20190404\/d94ccbd5f7e678c3a21c2c473a8dd4cf.jpg",    【专题横幅图】
            "good_list": {                  【商品分类列表】
                "list": [                   【分页列表】
                    {
                        "id": 11,           【商品ID】
                        "litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190329\/fa407a4bfb5bcb15700f8fa44dd32a60.png",        【商品封面图】
                        "title": "炒土豆丝",        【商品名】
                        "first_spec_id": 5,         【第一个规格ID】
                        "first_spec_name": "2斤",    【第一个规格单位】
                        "first_spec_unit": "kg",    【第一个规格单位注释】
                        "first_spec_price": "0.01", 【第一个规格售价】
                        "first_spec_source_price": "20.00",     【第一个规格原始标价】
                        "first_spec_min_buy_number": 1,         【第一个规格起售数】
                        "spec_count": 2,                【包含的规格数量】
                        "spec_list": [              【规格列表】
                            {
                                "id": 5,            【规格ID】
                                "price": "0.01",    【规格售价】
                                "source_price": "20.00",    【规格原始标价】
                                "name": "2斤",       【规格单位】
                                "unit": "kg",        【规格单位注释】
                                "min_buy_number": 1,    【起售数】
                                "cart_buy_number": 15   【此规格的购物车购买数量】       
                            },
                            {
                                "id": 6,
                                "price": "0.01",
                                "source_price": "38.00",
                                "name": "半斤",
                                "unit": "500g",
                                "min_buy_number": 1,    
                                "cart_buy_number": 0
                            }
                        ],
                        "first_spec_car_buy_number": 0         【第一个规格购买数量】
                    },
                    {
                        "id": 14,
                        "litpic": "",
                        "title": "回锅肉",
                        "first_spec_id": 14,
                        "first_spec_name": "3213",
                        "first_spec_unit": "3213",
                        "first_spec_price": "213.00",
                        "first_spec_source_price": "2131.00",
                        "first_spec_min_buy_number": 1,
                        "spec_count": 3,
                        "spec_list": [
                            {
                                "id": 13,
                                "price": "11.00",
                                "source_price": "22.00",
                                "name": "22",
                                "unit": "22",
                                "min_buy_number": 1,    
                                "cart_buy_number": 0
                            },
                            {
                                "id": 14,
                                "price": "213.00",
                                "source_price": "2131.00",
                                "name": "3213",
                                "unit": "3213",
                                "min_buy_number": 1,    
                                "cart_buy_number": 0
                            },
                            {
                                "id": 15,
                                "price": "3123.00",
                                "source_price": "131.00",
                                "name": "3123",
                                "unit": "3123",
                                "min_buy_number": 1,    
                                "cart_buy_number": 0
                            }
                        ],
                    }
                ],
                "count": 2,         【列表总数】
                "total_page": 1,    【分页总数】
                "current_page": 1,  【当前页】
                "pagesize": 2       【每页数量，与limit一致】
            },
        },
        "cart_all_spec_number": 4,          【购物车的规格数量和】
        "cart_all_buy_number": 5,          【购物车的规格购买数量和】
        "cart_all_price": "7.03"           【购物车的购物车总金额】
    }
}
```  
[接口目录](#接口目录)

### 关于详情

> 接口地址 /about/about

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
int         id                      【关于ID】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "about": {                  【关于信息】
            "id": 37,                   【关于ID】
            "title": "3U商户",            【关于题目】
            "create_time": "2019-04-28 11:31:50",       【关于创建时间】
            "body": "3U商户",                             【关于内容】
            "create_time_string": "2019-04-28"              【关于创建时间显示】
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "about": {}
    }
}
```  
[接口目录](#接口目录)

### 收藏商品
 
> 接口地址 /good/love_good

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int      goods_id                                【商品ID】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "收藏成功",
    "data": {
        "goods_id": 11,
        "love_status": "loved"
    }
}
{
    "responseCode": "0",
    "responseMessage": "取消收藏成功",
    "data": {
        "goods_id": 11,
        "love_status": "unloved"
    }
}
```  
[接口目录](#接口目录)

### 已收藏的商品列表
 
> 接口地址 /good/loved_good_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int/null        cate_id                 【分类ID(默认0 表示所有分类ID)】
string/null     loved_good_status       【收藏的商品状态：lacked 失效 其余状态或空都是查询所有】
int/null        limit                   【分页数(默认后台配置)】        
int/null        page                    【页数(默认1)】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "good_list": {
            "list": [
                {
                    "id": 11,           【商品ID】
                    "litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190329\/fa407a4bfb5bcb15700f8fa44dd32a60.png",        【商品封面图】
                    "title": "炒土豆丝",        【商品名】
                    "first_spec_id": 5,         【第一个规格ID】
                    "first_spec_name": "2斤",    【第一个规格单位】
                    "first_spec_unit": "kg",    【第一个规格单位注释】
                    "first_spec_price": "0.01", 【第一个规格售价】
                    "first_spec_source_price": "20.00",     【第一个规格原始标价】
                    "spec_count": 2,                【包含的规格数量】
                    "spec_list": [              【规格列表】
                        {
                            "id": 5,            【规格ID】
                            "price": "0.01",    【规格售价】
                            "source_price": "20.00",    【规格原始标价】
                            "name": "2斤",       【规格单位】
                            "unit": "kg",        【规格单位注释】
                            "stock_number": 0          【规格库存】
                        },
                        {
                            "id": 6,
                            "price": "0.01",
                            "source_price": "38.00",
                            "name": "半斤",
                            "unit": "500g",
                            "stock_number": 1          
                        }
                    ],
                    "spec_count": 2,                   【规格数量】
                    "love_good_status": "lowed_stock_number"                【收藏的商品状态：normal 正常 lacked 失效 lowed_stock_number 低库存】
                },
                {
                    "id": 12,
                    "litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190404\/d94ccbd5f7e678c3a21c2c473a8dd4cf.jpg",
                    "title": "百事可乐",
                    "first_spec_id": 9,
                    "first_spec_name": "杯",
                    "first_spec_unit": "1杯",
                    "first_spec_price": "5.00",
                    "first_spec_source_price": "20.00",
                    "spec_list": [
                        {
                            "id": 9,
                            "price": "5.00",
                            "source_price": "20.00",
                            "name": "杯",
                            "unit": "1杯",
                            "stock_number": 1
                        },
                        {
                            "id": 11,
                            "price": "2.00",
                            "source_price": "1.00",
                            "name": "1",
                            "unit": "1",
                            "stock_number": 0
                        }
                    ],
                    "spec_count": 2,
                    "love_good_status": "lowed_stock_number"
                },
                {
                    "id": 13,
                    "litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190404\/fe2cc5b880865c84195ad155f2aae2d3.jpg",
                    "title": "甜面包111",
                    "first_spec_id": 7,
                    "first_spec_name": "个数",
                    "first_spec_unit": "1个",
                    "first_spec_price": "2.00",
                    "first_spec_source_price": "20.00",
                    "spec_list": [
                        {
                            "id": 7,
                            "price": "2.00",
                            "source_price": "20.00",
                            "name": "个数",
                            "unit": "1个",
                            "stock_number": 20
                        },
                        {
                            "id": 12,
                            "price": "1.00",
                            "source_price": "1.00",
                            "name": "1",
                            "unit": "1",
                            "stock_number": 20
                        }
                    ],
                    "spec_count": 2,
                    "love_good_status": "lacked"
                },
                {
                    "id": 14,
                    "litpic": "",
                    "title": "回锅肉",
                    "first_spec_id": 13,
                    "first_spec_name": "22",
                    "first_spec_unit": "22",
                    "first_spec_price": "11.00",
                    "first_spec_source_price": "22.00",
                    "spec_list": [
                        {
                            "id": 13,
                            "price": "11.00",
                            "source_price": "22.00",
                            "name": "22",
                            "unit": "22",
                            "stock_number": 20
                        },
                        {
                            "id": 14,
                            "price": "213.00",
                            "source_price": "2131.00",
                            "name": "3213",
                            "unit": "3213",
                            "stock_number": 123
                        },
                        {
                            "id": 15,
                            "price": "3123.00",
                            "source_price": "131.00",
                            "name": "3123",
                            "unit": "3123",
                            "stock_number": 212
                        }
                    ],
                    "spec_count": 3,
                    "love_good_status": "normal"
                }
            ],
            "count": 4,                【列表总数】
            "total_page": 1,           【分页总数】
            "current_page": 1,          【当前页】    
            "pagesize": 5               【每页数量，与limit一致】
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "good_list": {
            "list": [],
            "count": 0,
            "total_page": 0,
            "current_page": 1,
            "pagesize": 5
        }
    }
}
```  
[接口目录](#接口目录)

### 清空商品收藏
 
> 接口地址 /good/empty_good_love

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "清空商品收藏成功",
    "data": {}
}
{
    "responseCode": "10001",
    "responseMessage": "商品收藏已经为空",
    "data": {}
}
```  
[接口目录](#接口目录)

### 购物车列表

> 接口地址 /navigation/cart_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "cart_list": [                          【购物车列表】
            {
                "spec_id": 171,                 【规格ID】       
                "buy_number": 1,                【购买数量增量】
                "good_id": 12,                      【商品ID】
                "good_title": "回锅肉",             【商品名】
                "good_litpic": "http:\/\/www.ypvpa.localhost",      【商品图片】
                "name": "2斤",                   【规格单位】
                "unit": "kg"                    【规格单位注释】
                "source_price": "22.00",            【规格原始标价】
                "price": "11.00",                    【规格售价】
                "stock_number": 100,                   【规格库存】
                "min_buy_number": 2,                      【起售数】 
                "status": "normal"                      【购物车状态：normal 正常 lacked 失效】
            },
            {
                "spec_id": 13,
                "buy_number": 2,
                "good_title": "回锅肉",
                "good_litpic": "http:\/\/www.ypvpa.localhost",
                "name": "22",
                "unit": "22",
                "source_price": "22.00",
                "price": "11.00",
                "stock_number": 100,
                "min_buy_number": 3,
                "status": "lacked"
            },
            {
                "spec_id": 12,
                "buy_number": 8,
                "good_title": "甜面包",
                "good_litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190404\/fe2cc5b880865c84195ad155f2aae2d3.jpg",
                "name": "1",
                "unit": "1",
                "source_price": "1.00",
                "price": "1.00",
                stock_number": 50,
                "min_buy_number": 1,
                "status": "lacked"
            }
        ],
        "cart_all_spec_number": 3,          【购物车的规格数量和】
        "cart_all_buy_number": 11,          【购物车的规格购买数量和】
        "cart_all_price": "30.00"           【购物车的购物车总金额】
    }
}

{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "cart_list": [],
        "cart_all_spec_number": 0,
        "cart_all_buy_number": 0,
        "cart_all_price": "0.00"
    }
}
```  
[接口目录](#接口目录)

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
 int         buy_number_string       【购买数量增量 比如+1 -1 0等，+1 -1表示在原有基础上+1 -1,0 表示直接定义此规格的购物车数量为0】【为了解决请求接收先后问题，现在只能传带符号的数量增量 如+1 -1】
 ```
 
 > ** 返回参数 Response Data : **
 ```
 {
     "responseCode": "0",
     "responseMessage": "执行成功",
     "data": {
         "buy_number_string": "+1",            【购物车购买数量增量】
         "price_string": "+5",                  【购物车价格增量】
         "cart_buy_number": 23,               【此规格的购物车购买数量】
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
 {
     "responseCode": "10001",
     "responseMessage": "购买数量信息必须带符号 buy_number_string(+1 -1等)",
     "data": {}
 }
```  
[接口目录](#接口目录)

### 批量删除购物车
 
> 接口地址 /cart/delete_carts

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
string      spec_ids                 【批量规格ID,ID之间以英文半角逗号隔开 比如2 或者 1,2,3】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "执行成功",
    "data": {
        "cart_all_spec_number": 6,          【购物车的规格数量和】  
        "cart_all_buy_number": 65,          【购物车的规格购买数量和】
        "cart_all_price": "236.03"          【购物车的购物车总金额】
    }
}
```  
[接口目录](#接口目录)

### 订单确认页面
 
> 接口地址 /order/order_ok

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
string/null         order_from                       【订单来源 good商品/cart购物车 默认good】
string/null         spec_ids_numbers                 【批量规格ID与数量对应,每个规格的ID与数量以英文半角下划线分隔，数量默认为1，ID之间以英文半角逗号隔开，比如 5 代表规格ID为5 数量为1，比如 5_2,9_3 代表规格ID为5、数量为2，规格ID为9、数量为3】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "spec_list": {                              【规格列表】
            "list": [
                {
                    "id": 5,                            【规格ID】
                    "name": "2斤",                       【规格单位】
                    "unit": "kg",                       【规格单位注释】
                    "price": "0.01",                    【规格售价】
                    "source_price": "20.00",            【规格原始标价】
                    "stock_number": 30,                 【规格库存】
                    "good_id": 14,                      【商品ID】
                    "good_title": "炒土豆丝",           【商品名】
                    "good_litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190329\/fa407a4bfb5bcb15700f8fa44dd32a60.png",       【商品图片】
                    "buy_number": 7,                     【购买数量】
                    "type": "std",                      【规格类型：标准的-std，预订的-advance】
                    "min_buy_number": 1                【起售数】

                },
                {
                    "id": 9,
                    "name": "杯",
                    "unit": "1杯",
                    "price": "5.00",
                    "source_price": "20.00",
                    "stock_number": 50,
                    "good_title": "百事可乐",
                    "good_litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190404\/d94ccbd5f7e678c3a21c2c473a8dd4cf.jpg",
                    "buy_number": 76
                    "type": "std", 
                    "min_buy_number": 1
                }
            ],
            "all_spec_number": 2,                   【规格数量和】
            "all_buy_number": 83,                   【规格购买数量和】
            "all_price": 380.07,                    【总金额】
            "all_source_price": 1660,               【总标价】
            "all_diff_price": 1279.93,              【总优惠价】
            "distribution_price": 0,                【运费】
            "pay_price": 380.07                     【订单实付金额】
        },
         "arrive_time_list": [                              【配送时间列表】
                    {
                        "day_select": "06-28(明天)",              【日期选择显示】
                        "hour_list": [
                            {
                                "start_arrive_time": "2019-06-28 08:00",            【开始配送时间 需要传给下单接口】
                                "end_arrive_time": "2019-06-28 09:00",              【结束配送时间 需要传给下单接口】
                                "section_select": "08:00-09:00",                    【时间段选择显示】
                                "arrive_time": "明天 [营业即送 08:00-09:00]"          【配送时间 需要传给下单接口】
                            },
                            {
                                "start_arrive_time": "2019-06-28 09:00",
                                "end_arrive_time": "2019-06-28 10:00",
                                "section_select": "09:00-10:00",
                                "arrive_time": "明天 [09:00-10:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-28 10:00",
                                "end_arrive_time": "2019-06-28 11:00",
                                "section_select": "10:00-11:00",
                                "arrive_time": "明天 [10:00-11:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-28 11:00",
                                "end_arrive_time": "2019-06-28 12:00",
                                "section_select": "11:00-12:00",
                                "arrive_time": "明天 [11:00-12:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-28 12:00",
                                "end_arrive_time": "2019-06-28 13:00",
                                "section_select": "12:00-13:00",
                                "arrive_time": "明天 [12:00-13:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-28 13:00",
                                "end_arrive_time": "2019-06-28 14:00",
                                "section_select": "13:00-14:00",
                                "arrive_time": "明天 [13:00-14:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-28 14:00",
                                "end_arrive_time": "2019-06-28 15:00",
                                "section_select": "14:00-15:00",
                                "arrive_time": "明天 [14:00-15:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-28 15:00",
                                "end_arrive_time": "2019-06-28 16:00",
                                "section_select": "15:00-16:00",
                                "arrive_time": "明天 [15:00-16:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-28 16:00",
                                "end_arrive_time": "2019-06-28 17:00",
                                "section_select": "16:00-17:00",
                                "arrive_time": "明天 [16:00-17:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-28 17:00",
                                "end_arrive_time": "2019-06-28 18:00",
                                "section_select": "17:00-18:00",
                                "arrive_time": "明天 [17:00-18:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-28 18:00",
                                "end_arrive_time": "2019-06-28 19:00",
                                "section_select": "18:00-19:00",
                                "arrive_time": "明天 [18:00-19:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-28 19:00",
                                "end_arrive_time": "2019-06-28 20:00",
                                "section_select": "19:00-20:00",
                                "arrive_time": "明天 [19:00-20:00]"
                            }
                        ]
                    },
                    {
                        "day_select": "06-29(后天)",
                        "hour_list": [
                            {
                                "start_arrive_time": "2019-06-29 08:00",
                                "end_arrive_time": "2019-06-29 09:00",
                                "section_select": "08:00-09:00",
                                "arrive_time": "后天 [营业即送 08:00-09:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-29 09:00",
                                "end_arrive_time": "2019-06-29 10:00",
                                "section_select": "09:00-10:00",
                                "arrive_time": "后天 [09:00-10:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-29 10:00",
                                "end_arrive_time": "2019-06-29 11:00",
                                "section_select": "10:00-11:00",
                                "arrive_time": "后天 [10:00-11:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-29 11:00",
                                "end_arrive_time": "2019-06-29 12:00",
                                "section_select": "11:00-12:00",
                                "arrive_time": "后天 [11:00-12:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-29 12:00",
                                "end_arrive_time": "2019-06-29 13:00",
                                "section_select": "12:00-13:00",
                                "arrive_time": "后天 [12:00-13:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-29 13:00",
                                "end_arrive_time": "2019-06-29 14:00",
                                "section_select": "13:00-14:00",
                                "arrive_time": "后天 [13:00-14:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-29 14:00",
                                "end_arrive_time": "2019-06-29 15:00",
                                "section_select": "14:00-15:00",
                                "arrive_time": "后天 [14:00-15:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-29 15:00",
                                "end_arrive_time": "2019-06-29 16:00",
                                "section_select": "15:00-16:00",
                                "arrive_time": "后天 [15:00-16:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-29 16:00",
                                "end_arrive_time": "2019-06-29 17:00",
                                "section_select": "16:00-17:00",
                                "arrive_time": "后天 [16:00-17:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-29 17:00",
                                "end_arrive_time": "2019-06-29 18:00",
                                "section_select": "17:00-18:00",
                                "arrive_time": "后天 [17:00-18:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-29 18:00",
                                "end_arrive_time": "2019-06-29 19:00",
                                "section_select": "18:00-19:00",
                                "arrive_time": "后天 [18:00-19:00]"
                            },
                            {
                                "start_arrive_time": "2019-06-29 19:00",
                                "end_arrive_time": "2019-06-29 20:00",
                                "section_select": "19:00-20:00",
                                "arrive_time": "后天 [19:00-20:00]"
                            }
                        ]
                    }
                ],
        "user_info": {                          【用户信息】
            "id": 1185,                           【用户编号】
            "nickname": null,                       【用户昵称】
            "mobile": "18381082760",                   【用户手机（登录用的手机）】
            "extension_title": "通江店",               【商户名】
            "extension_tel": "18381082766",             【商户电话】
            "extension_logo": "\/uploads\/images\/20190402\/55e104138963bf0d4dc63c8821cc1b56.jpg",          【商户logo】
            "extension_province_name": "天津市",               【商户省名】
            "extension_city_name": "天津市",                   【商户市名】
            "extension_area_name": "河东区",                   【商户区名】
            "extension_address": "红星路四段"                    【商户地址】
        }
    }
}
{
    "responseCode": "10001",
    "responseMessage": "库存不足 规格ID为5的购买量10000超过库存30",
    "data": {}
}
{
    "responseCode": "10001",
    "responseMessage": "库存不足 规格ID为5的购买量1000超过库存30,规格ID为9的购买量1001超过库存1000",
    "data": {}
}
```  
[接口目录](#接口目录)

### 检测规格库存
 
> 接口地址 /order/check_spec_stock

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
string/null         spec_ids_numbers                 【批量规格ID与数量对应,每个规格的ID与数量以英文半角下划线分隔，数量默认为1，ID之间以英文半角逗号隔开，比如 5 代表规格ID为5 数量为1，比如 5_2,9_3 代表规格ID为5、数量为2，规格ID为9、数量为3】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "库存充足",
    "data": {}
}
{
    "responseCode": "10001",
    "responseMessage": "库存不足 规格ID为5的购买量10000超过库存30",
    "data": {}
}
{
    "responseCode": "10001",
    "responseMessage": "库存不足 规格ID为5的购买量1000超过库存30,规格ID为9的购买量1001超过库存1000",
    "data": {}
}
```  
[接口目录](#接口目录)

### 下单
 
> 接口地址 /order/generate_order

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
string/null         order_from                       【订单来源 good商品/cart购物车 默认good】
string         spec_ids_numbers                 【批量规格ID与数量对应,每个规格的ID与数量以英文半角下划线分隔，数量默认为1，ID之间以英文半角逗号隔开，比如 5 代表规格ID为5 数量为1，比如 5_2,9_3 代表规格ID为5、数量为2，规格ID为9、数量为3】
string/null         remarks                         【订单备注】
string/null         arrive_time                         【配送时间 比如：后天 [营业即送 08:00-09:00]】
string/null         start_arrive_time                  【配送开始时间 比如：2019-06-29 08:00】
string/null         end_arrive_time                    【配送结束时间 比如：2019-06-29 09:00】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "成功下单",
    "data": {
        "order_sn": "S201904201623342595"               【订单序列号】
    }
}
{
    "responseCode": "30001",
    "responseMessage": "下单失败:购物车购买数量同步减少失败",
    "data": {}
}
```  
[接口目录](#接口目录)

### 支付订单
 
> 接口地址 /order/pay_order

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
string      order_sn                【订单号】
string      pay_type                【支付方式：微信 weixin  支付宝 alipay】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "获取支付订单数据成功",
    "data": {
        "appid": "wx14069c8d65f602ff",
        "partnerid": "1500740191",
        "prepayid": "wx261140006902492126b16dc13281889491",
        "noncestr": "5zxm1anUyuXkC6Be",
        "timestamp": 1556250000,
        "package": "Sign=WXPay",
        "sign": "38D2AD53A6128188DAA31596679DFBDC",
        "system_package": "Sign=WXPay"
    }
}
{
    "responseCode": "0",
    "responseMessage": "获取支付订单数据成功",
    "data": {
        "scalar": "alipay_sdk=alipay-sdk-php-20161101&app_id=2019042364291313&biz_content=%7B%22body%22%3A%22%E3%80%90%E5%A4%A7%E7%A5%9E%E5%8E%A8%E6%88%BF%E8%AE%A2%E5%8D%95%E3%80%91S201904261111479305%22%2C%22subject%22%3A%22%E3%80%90%E5%A4%A7%E7%A5%9E%E5%8E%A8%E6%88%BF%E8%AE%A2%E5%8D%95%E3%80%91S201904261111479305%22%2C%22out_trade_no%22%3A%22S201904261140224360%22%2C%22timeout_express%22%3A%221m%22%2C%22total_amount%22%3A%225.00%22%7D&charset=UTF-8&format=json&method=alipay.trade.app.pay&notify_url=http%3A%2F%2Fwww.ypvpa.localhost%2Findex.php%2Fkitchen_api%2Falipay_comm%2Fnotify.html&sign_type=RSA2&timestamp=2019-04-26+11%3A40%3A27&version=1.0&sign=0FF1Wr9F8CxIs4H2%2FFbEdConp8VCc5gGwUrKtvTAZ9yd0l4hgcrszjCSK%2FeHfTUiXOifdwa1f1u21VBcn2krSUxOf9c6vfrqpyEGVHVS3PPu3jvpTRZgphgAm0ESfbMzVFYXrkpTnIbk142MCS%2B4VW1ItcDNVsSUd0KcxFnL1PRyisdaDujsUWoWrjqih%2Fpficjur14Zu7JPaf6A%2FNpUO6gIa35vDulZmQx3Xk1jOTn9arLd1ioT%2FwTZ2fGeR%2BXIbQpn7y0N5xFyWq0Bpot%2Fh3JRZkAvSKYKjwKW%2BFMcpY1ikHNV3kw1tGgaN6Qfgko8mftvqGZSNkYDOgKKAO4h7Q%3D%3D"
    }
}
{
    "responseCode": "10001",
    "responseMessage": "订单不存在",
    "data": {}
}
{
    "responseCode": "11000",
    "responseMessage": "您还有未支付的预购差价，请先付清差价",
    "data": {
        "wait_pay_order": {                            【还未支付的尾款订单】
            "order_sn": "S201906271712571326",          【未支付订单号】
            "total_amount": "10.00",                    【未支付的总价格】
            "title": "福之泉大豆油25L",                   【规格名】
            "buy_number": 2,                             【规格购买数量】
            "advance_parent_order_sn": "S201906271712571321",   【父订单号】
            "advance_parent_status": 1,                         【父订单状态】
            "advance_parent_total_amount": "0.04",              【父订单总价格】
            "actual_total_amount": 10.04                        【实际的总价格】
        }
    }
}
```  
[接口目录](#接口目录)

### 订单列表
 
> 接口地址 /order/order_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int/null    limit                   【分页数(默认后台配置)】        
int/null    page                    【页数(默认1)】
string/null    status_choice                     【订单状态选择：no_pay 未付款（待付款） pay_success 已付款（待发货） send_success 已发货（待收货） finish 完成（待评价），其余状态或空都是显示所有订单】
```
> * status 0 未付款（待付款） 可以 取消订单、去付款
> * status 1 已付款（待发货） 可以 申请退款、提醒发货
> * status 10 已发货（待收货） 可以 催单(废除 分解为11 12 13)
> * status 11 已发货（待收货）已分配订单 商家拣货完成状态 
> * status 12 已发货（待收货）已分配订单 配送员接单状态
> * status 13 已发货（待收货）已分配订单 配送员取货状态
> * status 20 完成 可以 删除订单、申请售后、去评价（废除 分解为21 22）
> * status 21 完成（待评价） 可以 删除订单、申请售后、去评价
> * status 22 完成（已评价） 可以 删除订单、申请售后
> * status 30 订单取消（交易关闭） 可以 删除订单

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order_list": {                         【订单分页】
            "list": [                           【列表】
                {
                    "order_sn": "S201904201727304308",          【订单序列号】
                    "status": 0,                               【订单状态 现有5个状态分别对应5个详情页：状态 0 未支付（待付款） 1 支付成功（待发货） 10 已发货（待收货） 20 完成（待评价） 30 取消订单（交易关闭）】
                    "all_buy_number": 1,                        【购买规格数量和】
                    "pay_price": "5.00",                        【订单实付金额】
                    "create_time": "2019-04-20 17:27:30",           【订单创建时间】
                    "type": "advance",                              【订单类型（标准的-std，预订-advance，预订补款-advance_son）】
                    "wait_pay_order": {                            【还未支付的尾款订单】
                        "order_sn": "S201906271712571326",          【未支付订单号】
                        "total_amount": "10.00",                    【未支付价格】
                        "title": "福之泉大豆油25L",                   【规格名】
                        "buy_number": 2,                             【规格购买数量】
                        "advance_parent_order_sn": "S201904201727304308",   【父订单号】
                        "advance_parent_status": 1,                         【父订单状态】
                        "advance_parent_total_amount": "0.04",              【父订单总价格】
                        "actual_total_amount": 10.04                        【实际的总价格】
                    },
                    "spec_list": [                        【订单规格列表】
                        {
                            "good_id": 12,                      【商品ID】
                            "good_title": "百事可乐",               【商品名】
                            "good_litpic": "\/uploads\/goods\/cover\/20190404\/d94ccbd5f7e678c3a21c2c473a8dd4cf.jpg",           【商品图片】
                            "buy_number": 1,                    【商品规格购买数量】
                            "price": "5.00"                     【商品规格售价】
                        }
                    ],
                    "distribution_order": {                 【配送信息】
                        "distribution_user_full_name": "红星",            【配送员全名】
                        "distribution_user_face": "",                       【配送员头像】
                        "distribution_user_mobile": "18381082701",           【配送员电话】
                        "status_string": "赶往仓库",                    【配送状态】
                        "coordinate_info": {                        【坐标信息】
                            "receive_to_pick_goods": {          【确认接单坐标 到 取货坐标列表】
                                "coordinate_x": "23.5555556",                   【坐标X轴】
                                "coordinate_y": "113.2222222",                  【坐标Y轴】
                                "create_time": "1970-01-01 08:33:39"            【接单时间】
                            },
                            "pick_goods_to_merchant": {             【取货坐标 到 完成坐标列表】
                                "coordinate_x": "23.5555556",
                                "coordinate_y": "113.2222222",
                                "create_time": "1970-01-01 08:33:39"            【取货时间】
                            }
                        }
                    },
                    "user_agent": {                 【代理信息】
                      "tel": "18381082766"            【代理联系方式】
                    },
                    "status_string": "待付款",                     【订单状态显示】
                    "create_time_string": "昨天 17:27"                【订单创建时间显示】
                },
                {
                    "order_sn": "S201906271711395705",
                    "status": 0,
                    "all_buy_number": 1,
                    "pay_price": "0.02",
                    "create_time": "2019-06-27 17:11:39",
                    "type": "advance",
                    "wait_pay_order": {},
                    "spec_list": [
                        {
                            "good_id": 35,
                            "good_title": "福之泉大豆油25L",
                            "good_litpic": "http://www.ypvpa.localhost/uploads/goods/cover/20190505/2a2f1d293a5e11dfd316f8ad5634d8ae.jpg",
                            "buy_number": 1,
                            "price": "0.02"
                        }
                    ],
                    "distribution_order": {},
                    "user_agent": {
                        "tel": "4001-898-116"
                    },
                    "status_string": "待付款",
                    "create_time_string": "3小时前"
                }
            ],
            "count": 70,                【列表总数】
            "total_page": 35,           【分页总数】
            "current_page": 1,          【当前页】    
            "pagesize": 2               【每页数量，与limit一致】
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order_list": {
            "list": [],
            "count": 0,
            "total_page": 0,
            "current_page": 1,
            "pagesize": 6
        }
    }
}
```  
[接口目录](#接口目录)

### 订单详情
 
> 接口地址 /order/order

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
string      order_sn                                【订单号】
```
> * status 0 未付款（待付款） 可以 取消订单、去付款
> * status 1 已付款（待发货） 可以 申请退款、提醒发货
> * status 10 已发货（待收货） 可以 催单(废除 分解为11 12 13)
> * status 11 已发货（待收货）已分配订单 商家拣货完成状态 
> * status 12 已发货（待收货）已分配订单 配送员接单状态
> * status 13 已发货（待收货）已分配订单 配送员取货状态
> * status 20 完成 可以 删除订单、申请售后、去评价（废除 分解为21 22）
> * status 21 完成（待评价） 可以 删除订单、申请售后、去评价
> * status 22 完成（已评价） 可以 删除订单、申请售后
> * status 30 订单取消（交易关闭） 可以 删除订单

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order": {
            "order_sn": "S201904220039186777",                  【订单号】
            "status": 30,                                       【订单状态 现有5个状态分别对应5个详情页：状态 0 未支付（待付款） 1 支付成功（待发货） 10 已发货（待收货） 20 完成（待评价） 30 取消订单（交易关闭）】
            "create_time": "2019-04-22 00:39:18",               【时间->下单时间】
            "extension_title": "通江店",                       【收货人（商户名）】
            "extension_tel": "18381082766",                   【收货电话（商户电话）】
            "extension_province_name": "天津市",               【收货地址-省（商户省名）】
            "extension_city_name": "天津市",                   【收货地址-市（商户市名）】
            "extension_area_name": "河东区",                   【收货地址-区（商户区名）】
            "extension_address": "红星路四段"                    【收取地址-详细地址（商户地址）】
            "remarks": "555555",                        【订单备注】
            "pay_time": null,                           【时间->订单付款时间】
            "type": "advance",                              【订单类型（标准的-std，预订-advance，预订补款-advance_son）】
            "wait_pay_order": {                            【还未支付的尾款订单】
                "order_sn": "S201906271712571323",          【未支付订单号】
                "total_amount": "10.00",                    【未支付价格】
                "title": "福之泉大豆油25L",                   【规格名】
                "buy_number": 2,                             【规格购买数量】
                "advance_parent_order_sn": "S201904201727304308",   【父订单号】
                "advance_parent_status": 1,                         【父订单状态】
                "advance_parent_total_amount": "0.04",              【父订单总价格】
                "actual_total_amount": 10.04                        【实际的总价格】
            },
            "spec_list": {                          【规格列表信息】
                "list": [                           【列表】
                    {
                        "id": 9,                    【规格ID】
                        "price": "5.00",            【规格售价】
                        "source_price": "20.00",    【规格原始标价】
                        "name": "杯",                【规格单位】
                        "good_id": 12,              【商品ID】
                        "good_title": "百事可乐",       【商品名】
                        "good_litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190404\/d94ccbd5f7e678c3a21c2c473a8dd4cf.jpg",    【商品图片】
                        "buy_number": 1,            【购买数量】
                    }
                ],
                "all_spec_number": 1,               【规格数量和】
                "all_buy_number": 1,                【规格购买数量和】
                "all_price": 5,                     【总金额】
                "all_source_price": 20,             【总标价】
                "all_diff_price": 15,               【总优惠价】
                "distribution_price": "0.00",       【运费】
                "pay_price": 5                      【订单实付金额】
            },
            "status_string": "交易关闭",            【订单状态显示】
            "status_string_description": "其他原因",            【订单状态显示的解释】
            "status_cancel_string": "其他原因",     【订单取消（交易关闭）的原因】
            "create_time_string": "17分钟前",       【创建时间显示】
            "pay_type_string": "微信支付",           【支付方式】
            "cancel_time": "2019-04-29 20:49:58",   【取消时间】
            "arrive_time": "立即配送",              【时间->送达时间】
            "distribution_get_order_time": null,    【时间->订单拣货时间】
            "distribution_arriving_time": null,     【时间->配送员接单时间】
            "distribution_sending_time": null,      【时间->配送员取货时间】
            "finish_time": null,                    【时间->订单完成时间】
            "evaluation_time": null                 【时间->订单评论时间】
        },
        "distribution_order": {                 【配送信息】
            "distribution_user_full_name": "红星",            【配送员全名】
            "distribution_user_face": "",                       【配送员头像】
            "distribution_user_mobile": "18381082701",           【配送员电话】
            "status_string": "赶往仓库",                    【配送状态】
            "coordinate_info": {                        【坐标信息】
                "receive_to_pick_goods": {          【确认接单坐标 到 取货坐标列表】
                    "coordinate_x": "23.5555556",                   【坐标X轴】
                    "coordinate_y": "113.2222222",                  【坐标Y轴】
                    "create_time": "1970-01-01 08:33:39"            【接单时间】
                },
                "pick_goods_to_merchant": {             【取货坐标 到 完成坐标列表】
                    "coordinate_x": "23.5555556",
                    "coordinate_y": "113.2222222",
                    "create_time": "1970-01-01 08:33:39"            【取货时间】
                }
            }
        },
        "user_agent": {                 【代理信息】
            "tel": "18381082766"            【代理联系方式】
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order": {
            "order_sn": "S201906271712399263",
            "status": 1,
            "status_cancel_string": null,
            "create_time": "2019-06-27 17:12:39",
            "extension_title": "苏杰的商户",
            "extension_tel": "18381082760",
            "extension_province_name": "四川省",
            "extension_city_name": "成都市",
            "extension_area_name": "武侯区",
            "extension_address": "四川成都",
            "remarks": null,
            "pay_time": "2019-06-27 17:21:13",
            "type": "advance",
            "wait_pay_order": {},
            "spec_list": {
                "list": [
                    {
                        "id": 77,
                        "price": "0.02",
                        "source_price": "2.00",
                        "name": "瓶",
                        "good_id": 35,
                        "good_title": "福之泉大豆油25L",
                        "good_litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190505\/2a2f1d293a5e11dfd316f8ad5634d8ae.jpg",
                        "buy_number": 1
                    },
                    {
                        "id": 78,
                        "price": "0.02",
                        "source_price": "19.80",
                        "name": "900克",
                        "good_id": 34,
                        "good_title": "伊品鸡精",
                        "good_litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190407\/a8b30305190cb9113c039c2dee8587d9.jpg",
                        "buy_number": 2
                    }
                ],
                "all_spec_number": 2,
                "all_buy_number": 3,
                "all_price": 0.06,
                "all_source_price": 41.6,
                "all_diff_price": 41.54,
                "distribution_price": "0.00",
                "pay_price": 0.06
            },
            "cancel_time": null,
            "arrive_time": "立即配送",
            "distribution_get_order_time": null,
            "distribution_arriving_time": null,
            "distribution_sending_time": null,
            "finish_time": null,
            "evaluation_time": null,
            "status_string": "已支付",
            "status_string_description": "订单支付成功，等待商家接单",
            "create_time_string": "4小时前",
            "pay_type_string": "微信支付"
        },
        "distribution_order": {},
        "user_agent": {
            "tel": "4001-898-116"
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order": {},
        "distribution_order": {},
        "user_agent": {
            "tel": "4001-898-116"
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order": {
            "order_sn": "S201905131759149482",
            "status": 0,
            "status_cancel_string": null,
            "create_time": "2019-05-13 18:05:03",
            "extension_title": "苏杰的商户",
            "extension_tel": "18381082760",
            "extension_province_name": "四川省",
            "extension_city_name": "成都市",
            "extension_area_name": "武侯区",
            "extension_address": "四川成都",
            "remarks": "",
            "spec_list": {
                "list": [
                    {
                        "id": 66,
                        "price": "0.01",
                        "source_price": "9.40",
                        "name": "450g",
                        "good_id": 34,
                        "good_title": "伊品鸡精",
                        "good_litpic": "http:\/\/kitchenapi.marketing.yuqg.com\/uploads\/goods\/cover\/20190407\/a8b30305190cb9113c039c2dee8587d9.jpg",
                        "buy_number": 1
                    }
                ],
                "all_spec_number": 1,
                "all_buy_number": 1,
                "all_price": 0.01,
                "all_source_price": 9.4,
                "all_diff_price": 9.39,
                "distribution_price": "0.00",
                "pay_price": 0.01
            },
            "status_string": "等待买家付款",
            "status_string_description": "剩余23小时59分钟自动关闭",
            "create_time_string": "刚刚"
        },
        "distribution_order": {},
        "user_agent": {
            "tel": "4001-898-116"
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order": {
            "order_sn": "S201905161512346685",
            "status": 1,
            "status_cancel_string": null,
            "create_time": "2019-05-16 15:12:34",
            "extension_title": "苏杰的商户",
            "extension_tel": "18381082760",
            "extension_province_name": "四川省",
            "extension_city_name": "成都市",
            "extension_area_name": "武侯区",
            "extension_address": "四川成都",
            "remarks": "",
            "pay_time": "2019-05-16 15:13:14",
            "spec_list": {
                "list": [
                    {
                        "id": 66,
                        "price": "0.01",
                        "source_price": "9.40",
                        "name": "450g",
                        "good_id": 34,
                        "good_title": "伊品鸡精",
                        "good_litpic": "http://kitchenapi.marketing.yuqg.com/uploads/goods/cover/20190407/a8b30305190cb9113c039c2dee8587d9.jpg",
                        "buy_number": 1
                    }
                ],
                "all_spec_number": 1,
                "all_buy_number": 1,
                "all_price": 0.01,
                "all_source_price": 9.4,
                "all_diff_price": 9.39,
                "distribution_price": "0.00",
                "pay_price": 0.01
            },
            "status_string": "已支付",
            "status_string_description": "订单支付成功，等待商家接单",
            "create_time_string": "刚刚",
            "pay_type_string": "微信支付",
            "distribution_get_order_time": null,
            "distribution_arriving_time": null,
            "distribution_sending_time": null,
            "finish_time": null,
            "evaluation_time": null
        },
        "distribution_order": {},
        "user_agent": {
            "tel": "4001-898-116"
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order": {
            "order_sn": "S201905161512346685",
            "status": 11,
            "status_cancel_string": null,
            "create_time": "2019-05-16 15:12:34",
            "extension_title": "苏杰的商户",
            "extension_tel": "18381082760",
            "extension_province_name": "四川省",
            "extension_city_name": "成都市",
            "extension_area_name": "武侯区",
            "extension_address": "四川成都",
            "remarks": "",
            "pay_time": "2019-05-16 15:13:14",
            "spec_list": {
                "list": [
                    {
                        "id": 66,
                        "price": "0.01",
                        "source_price": "9.40",
                        "name": "450g",
                        "good_id": 34,
                        "good_title": "伊品鸡精",
                        "good_litpic": "http://kitchenapi.marketing.yuqg.com/uploads/goods/cover/20190407/a8b30305190cb9113c039c2dee8587d9.jpg",
                        "buy_number": 1
                    }
                ],
                "all_spec_number": 1,
                "all_buy_number": 1,
                "all_price": 0.01,
                "all_source_price": 9.4,
                "all_diff_price": 9.39,
                "distribution_price": "0.00",
                "pay_price": 0.01
            },
            "status_string": "拣货完成",
            "status_string_description": "商家已完成拣货，等待配送",
            "create_time_string": "4分钟前",
            "pay_type_string": "微信支付",
            "distribution_get_order_time": "2019-05-16 15:15:18",
            "distribution_arriving_time": null,
            "distribution_sending_time": null,
            "finish_time": null,
            "evaluation_time": null
        },
        "distribution_order": {
            "distribution_user_full_name": "苏杰",
            "distribution_user_face": "http://img.marketing.yuqg.com/uploads/distribution_user/face/201905/a4acf3ef8c.jpg",
            "distribution_user_mobile": "18381082760",
            "status_string": "已分配",
            "coordinate_info": {
                "receive_to_pick_goods": {},
                "pick_goods_to_merchant": {}
            }
        },
        "user_agent": {
            "tel": "4001-898-116"
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order": {
            "order_sn": "S201905161512346685",
            "status": 12,
            "status_cancel_string": null,
            "create_time": "2019-05-16 15:12:34",
            "extension_title": "苏杰的商户",
            "extension_tel": "18381082760",
            "extension_province_name": "四川省",
            "extension_city_name": "成都市",
            "extension_area_name": "武侯区",
            "extension_address": "四川成都",
            "remarks": "",
            "pay_time": "2019-05-16 15:13:14",
            "spec_list": {
                "list": [
                    {
                        "id": 66,
                        "price": "0.01",
                        "source_price": "9.40",
                        "name": "450g",
                        "good_id": 34,
                        "good_title": "伊品鸡精",
                        "good_litpic": "http://kitchenapi.marketing.yuqg.com/uploads/goods/cover/20190407/a8b30305190cb9113c039c2dee8587d9.jpg",
                        "buy_number": 1
                    }
                ],
                "all_spec_number": 1,
                "all_buy_number": 1,
                "all_price": 0.01,
                "all_source_price": 9.4,
                "all_diff_price": 9.39,
                "distribution_price": "0.00",
                "pay_price": 0.01
            },
            "status_string": "配送员已接单",
            "status_string_description": "配送员正在前往仓库，配送员:苏杰",
            "create_time_string": "6分钟前",
            "pay_type_string": "微信支付",
            "distribution_get_order_time": "2019-05-16 15:15:18",
            "distribution_arriving_time": "2019-05-16 15:17:41",
            "distribution_sending_time": null,
            "finish_time": null,
            "evaluation_time": null
        },
        "distribution_order": {
            "distribution_user_full_name": "苏杰",
            "distribution_user_face": "http://img.marketing.yuqg.com/uploads/distribution_user/face/201905/a4acf3ef8c.jpg",
            "distribution_user_mobile": "18381082760",
            "status_string": "赶往仓库",
            "coordinate_info": {
                "receive_to_pick_goods": {
                    "coordinate_x": "0.0000000",
                    "coordinate_y": "0.0000000",
                    "create_time": "2019-05-16 15:17:41"
                },
                "pick_goods_to_merchant": {}
            }
        },
        "user_agent": {
            "tel": "4001-898-116"
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order": {
            "order_sn": "S201905161512346685",
            "status": 13,
            "status_cancel_string": null,
            "create_time": "2019-05-16 15:12:34",
            "extension_title": "苏杰的商户",
            "extension_tel": "18381082760",
            "extension_province_name": "四川省",
            "extension_city_name": "成都市",
            "extension_area_name": "武侯区",
            "extension_address": "四川成都",
            "remarks": "",
            "pay_time": "2019-05-16 15:13:14",
            "spec_list": {
                "list": [
                    {
                        "id": 66,
                        "price": "0.01",
                        "source_price": "9.40",
                        "name": "450g",
                        "good_id": 34,
                        "good_title": "伊品鸡精",
                        "good_litpic": "http://kitchenapi.marketing.yuqg.com/uploads/goods/cover/20190407/a8b30305190cb9113c039c2dee8587d9.jpg",
                        "buy_number": 1
                    }
                ],
                "all_spec_number": 1,
                "all_buy_number": 1,
                "all_price": 0.01,
                "all_source_price": 9.4,
                "all_diff_price": 9.39,
                "distribution_price": "0.00",
                "pay_price": 0.01
            },
            "status_string": "配送员已取货",
            "status_string_description": "开始为您配送，配送员:苏杰",
            "create_time_string": "6分钟前",
            "pay_type_string": "微信支付",
            "distribution_get_order_time": "2019-05-16 15:15:18",
            "distribution_arriving_time": "2019-05-16 15:17:41",
            "distribution_sending_time": "2019-05-16 15:18:20",
            "finish_time": null,
            "evaluation_time": null
        },
        "distribution_order": {
            "distribution_user_full_name": "苏杰",
            "distribution_user_face": "http://img.marketing.yuqg.com/uploads/distribution_user/face/201905/a4acf3ef8c.jpg",
            "distribution_user_mobile": "18381082760",
            "status_string": "配送中",
            "coordinate_info": {
                "receive_to_pick_goods": {
                    "coordinate_x": "0.0000000",
                    "coordinate_y": "0.0000000",
                    "create_time": "2019-05-16 15:17:41"
                },
                "pick_goods_to_merchant": {
                    "coordinate_x": "0.0000000",
                    "coordinate_y": "0.0000000",
                    "create_time": "2019-05-16 15:18:20"
                }
            }
        },
        "user_agent": {
            "tel": "4001-898-116"
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order": {
            "order_sn": "S201905161512346685",
            "status": 20,
            "status_cancel_string": null,
            "create_time": "2019-05-16 15:12:34",
            "extension_title": "苏杰的商户",
            "extension_tel": "18381082760",
            "extension_province_name": "四川省",
            "extension_city_name": "成都市",
            "extension_area_name": "武侯区",
            "extension_address": "四川成都",
            "remarks": "",
            "pay_time": "2019-05-16 15:13:14",
            "spec_list": {
                "list": [
                    {
                        "id": 66,
                        "price": "0.01",
                        "source_price": "9.40",
                        "name": "450g",
                        "good_id": 34,
                        "good_title": "伊品鸡精",
                        "good_litpic": "http://kitchenapi.marketing.yuqg.com/uploads/goods/cover/20190407/a8b30305190cb9113c039c2dee8587d9.jpg",
                        "buy_number": 1
                    }
                ],
                "all_spec_number": 1,
                "all_buy_number": 1,
                "all_price": 0.01,
                "all_source_price": 9.4,
                "all_diff_price": 9.39,
                "distribution_price": "0.00",
                "pay_price": 0.01
            },
            "status_string": "订单已完成",
            "status_string_description": "感谢您使用美香厨",
            "create_time_string": "7分钟前",
            "pay_type_string": "微信支付",
            "distribution_get_order_time": "2019-05-16 15:15:18",
            "distribution_arriving_time": "2019-05-16 15:17:41",
            "distribution_sending_time": "2019-05-16 15:18:20",
            "finish_time": "2019-05-16 15:18:40",
            "evaluation_time": null
        },
        "distribution_order": {
            "distribution_user_full_name": "苏杰",
            "distribution_user_face": "http://img.marketing.yuqg.com/uploads/distribution_user/face/201905/a4acf3ef8c.jpg",
            "distribution_user_mobile": "18381082760",
            "status_string": "完成配送",
            "coordinate_info": {
                "receive_to_pick_goods": {
                    "coordinate_x": "0.0000000",
                    "coordinate_y": "0.0000000",
                    "create_time": "2019-05-16 15:17:41"
                },
                "pick_goods_to_merchant": {
                    "coordinate_x": "0.0000000",
                    "coordinate_y": "0.0000000",
                    "create_time": "2019-05-16 15:18:20"
                }
            }
        },
        "user_agent": {
            "tel": "4001-898-116"
        }
    }
}
```  
[接口目录](#接口目录)

### 订单取消原因列表
 
> 接口地址 /order/order_cancel_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order_cancel_list": [                  【订单取消原因列表】
            {
                "id": 1,                                        【订单取消原因ID】
                "status_cancel_string": "误购或不想买了"           【订单取消原因】
            },
            {
                "id": 2,
                "status_cancel_string": "信息填写有误，重新购买"
            },
            {
                "id": 3,
                "status_cancel_string": "在线支付遇到问题"
            },
            {
                "id": 4,
                "status_cancel_string": "其他原因"
            }
        ]
    }
}
```  
[接口目录](#接口目录)

### 取消订单
 
> 接口地址 /order/cancel_order

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
string      order_sn                                【订单号】
string/null    status_cancel_choice                 【订单状态取消原因:直接用/order/order_cancel_list获取的数据的ID】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "订单取消成功",
    "data": {}
}
{
    "responseCode": "10001",
    "responseMessage": "只有未购买的订单才能取消",
    "data": {}
}
{
    "responseCode": "10001",
    "responseMessage": "订单不存在",
    "data": {}
}
```  
[接口目录](#接口目录)

### 删除订单
 
> 接口地址 /order/delete_order

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
string      order_sn                                【订单号】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "订单删除成功",
    "data": {}
}
{
    "responseCode": "10001",
    "responseMessage": "只有购买完成或关闭的订单才能删除",
    "data": {}
}
{
    "responseCode": "10001",
    "responseMessage": "订单不存在",
    "data": {}
}
```  
[接口目录](#接口目录)

### 订单日志列表
 
> 接口地址 /order/order_log_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
int/null    limit                   【分页数(默认后台配置)】        
int/null    page                    【页数(默认1)】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order_log_list": {                 【订单日志列表信息】
            "list": [                       【列表】
                {
                    "order_sn": "S201904231038438763",              【订单号】
                    "create_time": "2019-04-23 11:03:27",           【创建时间】
                    "create_timestamp": 1555988607,                 【创建时间戳】
                    "status_string": "删除订单",                        【订单状态显示】
                    "status_string_description": "您的订单已删除"                    【订单状态说明】
                },
                {
                    "order_sn": "S201904231038438763",
                    "create_time": "2019-04-23 10:45:38",
                    "create_timestamp": 1555987538,
                    "status_string": "取消订单",
                    "status_string_description": "您的订单已取消"
                },
                {
                    "order_sn": "S201904231038438763",
                    "create_time": "2019-04-23 10:38:43",
                    "create_timestamp": 1555987123,
                    "status_string": "未支付",
                    "status_string_description": "您的订单还未付款，赶快去支付"
                },
                {
                    "order_sn": "S201904231038424658",
                    "create_time": "2019-04-23 10:38:42",
                    "create_timestamp": 1555987122,
                    "status_string": "未支付",
                    "status_string_description": "您的订单还未付款，赶快去支付"
                },
                {
                    "order_sn": "S201904231038127333",
                    "create_time": "2019-04-23 10:38:12",
                    "create_timestamp": 1555987092,
                    "status_string": "未支付",
                    "status_string_description": "您的订单还未付款，赶快去支付"
                }
            ],
            "count": 12,         【列表总数】
            "total_page": 3,    【分页总数】
            "current_page": 1,  【当前页】
            "pagesize": 5       【每页数量，与limit一致】
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order_log_list": {
            "list": [],
            "count": 12,
            "total_page": 3,
            "current_page": 3,
            "pagesize": 5
        }
    }
}
```  
[接口目录](#接口目录)

### 订单追踪列表
 
> 接口地址 /order/order_trace_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
string      order_sn                                【订单号】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order_trace_list": [                       【订单追踪列表】
            {
                "create_time": "2019-04-26 19:30:57",               【创建时间】
                "status_string": "配送员已取货",                          【状态显示】
                "status_string_description": "开始为您配送，配送员:红星",               【状态显示说明】
                "log": "http:\/\/www.ypvpa.localhost\/statics\/kitchen_api\/images\/order\/distribution.png",           【前方小log】
                "create_time_string": "2019-04-26 19:30"                【创建时间显示】
            },
            {
                "create_time": "2019-04-26 15:30:57",
                "status_string": "配送员已接单",
                "status_string_description": "正在前往商家，配送员:红星",
                "log": "http:\/\/www.ypvpa.localhost\/statics\/kitchen_api\/images\/order\/distribution.png",
                "create_time_string": "2019-04-26 15:30"
            },
            {
                "create_time": "2019-04-25 09:09:45",
                "status_string": "已支付",
                "status_string_description": "订单支付成功",
                "log": "http:\/\/www.ypvpa.localhost\/statics\/kitchen_api\/images\/order\/order_payed.png",
                "create_time_string": "2019-04-25 09:09"
            },
            {
                "create_time": "2019-04-23 10:38:09",
                "status_string": "订单提交成功",
                "status_string_description": "订单号:S201904231038093789",
                "log": "http:\/\/www.ypvpa.localhost\/statics\/kitchen_api\/images\/order\/order_unpay.png",
                "create_time_string": "2019-04-23 10:38"
            }
        ]
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "order_trace_list": [
            {
                "create_time": "2019-04-25 21:00:47",
                "status_string": "订单提交成功",
                "status_string_description": "订单号:S201904252100474389",
                "log": "http:\/\/www.ypvpa.localhost\/statics\/kitchen_api\/images\/order\/order_unpay.png",
                "create_time_string": "2019-04-25 21:00"
            }
        ]
    }
}
```  
[接口目录](#接口目录)

### 评论订单
 
> 接口地址 /order/evaluate_order

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
string      order_sn                                【订单号】
string      good_star_number                        【评价商品星数】
string      distribution_star_number                【评价配送星数】
string      evaluation                              【评论】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "评论成功",
    "data": {}
}
{
    "responseCode": "10001",
    "responseMessage": "已经评论",
    "data": {}
}
{
    "responseCode": "10001",
    "responseMessage": "订单只有完成交易后才能评论",
    "data": {}
}
```  
[接口目录](#接口目录)

### 消息详情

> 接口地址 /plugin/message

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "un_read_number": 2                 【未读数量】
    }
}
```
[接口目录](#接口目录)

### 消息中心列表
 
> 接口地址 /plugin/message_center_function_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "list": [
            {
                "message_type_title": "系统通知",               【消息类型题目】
                "logo": "http://www.ypvpa.localhost/statics/kitchen_api/images/message_center/system.png",      【消息类型logo】
                "last_message_description": "暂无更多内容",           【消息描述】
                "un_read_number": 1,                        【未读数量】
                "message_type": "system"                    【消息类型】
            },
            {
                "message_type_title": "订单通知",
                "logo": "http://www.ypvpa.localhost/statics/kitchen_api/images/message_center/order_log_list.png",
                "last_message_description": "暂无更多内容",
                "un_read_number": 0,
                "message_type": "order_log_list"
            }
        ]
    }
}
```  
[接口目录](#接口目录)

### 系统消息列表
 
> 接口地址 /plugin/system_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
int/null    limit                   【分页数(默认后台配置)】        
int/null    page                    【页数(默认1)】
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "system_list": {            【系统消息列表信息】
            "list": [               【列表】
                {
                    "id": 1,            【消息ID】
                    "title": "欢迎来到美香厨",        【消息题目】
                    "description": "666",               【消息摘要】
                    "create_time": "1970-01-01 08:33:39",       【消息创建时间】
                    "is_read": "unread",                        【是否已读:unread 未读,read 已读】
                    "create_time_string": "1970年01月01日 08:00"           【消息创建时间显示】
                }
            ],
            "count": 1,         【列表总数】
            "total_page": 1,    【分页总数】
            "current_page": 1,  【当前页】
            "pagesize": 2       【每页数量，与limit一致】
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "system_list": {
            "list": [],
            "count": 1,
            "total_page": 1,
            "current_page": 1,
            "pagesize": 2
        }
    }
}
```  
[接口目录](#接口目录)

### 系统消息详情
 
> 接口地址 /plugin/system

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
int         id                  【系统消息ID】          
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "system": {                     【系统消息信息】
            "id": 1,                        【消息ID】
            "title": "欢迎来到美香厨",        【消息题目】
            "description": "666",               【消息摘要】
            "body": "B站源码被公开 6啊",           【消息内容】
            "create_time": "1970-01-01 08:33:39",       【消息创建时间】
            "is_read": "unread",                        【是否已读:unread 未读,read 已读】
            "create_time_string": "1970-01-01"              【消息创建时间显示】
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "system": {}
    }
}
```  
[接口目录](#接口目录)

### 常见问题列表
 
> 接口地址 /plugin/question_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "question_list": [              【常见问题列表】
            {
                "id": 2,                    【常见问题ID】
                "question": "快递如何收费",           【问题】
                "answer": "快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。",           【回答】
                "answer_description": "快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过..."           【回答摘要】
            },
            {
                "id": 1,
                "question": "快递如何收费",
                "answer": "快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。",
                "answer_description": "快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过..."
            }
        ]
    }
}
```  
[接口目录](#接口目录)

### 常见问题详情
 
> 接口地址 /plugin/question

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
int         id                  【常见问题ID】          
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "question": {               【常见问题信息】
            "id": 1,                【常见问题ID】
            "question": "快递如何收费",               【问题】
            "answer": "快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。快递按公斤计算，超过1公斤算2公斤计算。",               【回答】
            "create_time": "2019-04-28 12:06:55",           【创建时间】
            "create_time_string": "2019-04-28"              【创建时间显示】
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "question": {}
    }
}
```  
[接口目录](#接口目录)

### 协议列表
 
> 接口地址 /plugin/agreement_list

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "agreement_list": [
            {
                "id": 2,                            【协议ID】
                "title": "协议2",                     【标题】
                "create_time": "2019-06-04 08:30:01",           【创建时间】
                "create_time_string": "2019年06月04日 08:30"       【创建时间显示】
            },
            {
                "id": 1,
                "title": "协议1",
                "create_time": "2019-06-04 08:29:58",
                "create_time_string": "2019年06月04日 08:29"
            }
        ]
    }
}
```  
[接口目录](#接口目录)

### 协议详情
 
> 接口地址 /plugin/agreement

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
int         id                  【协议ID】          
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "agreement": {
            "id": 1,
            "title": "协议1",                 【标题】
            "body": "协议1内容",                【内容】
            "create_time": "2019-06-04 08:29:58",           【创建时间】
            "create_time_string": "2019-06-04"              【创建时间显示】
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "agreement": {}
    }
}
```  
[接口目录](#接口目录)

### 写留言
 
> 接口地址 /mes_book/write_mes_book

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
string      mobile_id
string      session_id        
string      session_security
string      name                        【姓名】                         
string      mobile                      【电话】     
string      body                        【内容】   
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "订单删除成功",
    "data": {}
}
{
    "responseCode": "10001",
    "responseMessage": "只有购买完成或关闭的订单才能删除",
    "data": {}
}
{
    "responseCode": "10001",
    "responseMessage": "订单不存在",
    "data": {}
}
```  
[接口目录](#接口目录)

### ios版本
 
> 接口地址 /plugin/ios_version

> 请求方式 POST

> ** 传递参数 Request Data : **
```
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "version": {
            "code": "0",
            "msg": "获取版本信息成功",
            "data": {
                "module_type": "ios",
                "version_id": "2019-4-28",
                "log_information": "首次版本"
            }
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "version": {}
    }
}
```  
[接口目录](#接口目录)

### android版本
 
> 接口地址 /plugin/android_version

> 请求方式 POST

> ** 传递参数 Request Data : **
```
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "version": {
            "code": "0",
            "msg": "获取版本信息成功",
            "data": {
                "module_type": "android",
                "update_url": "http:\/\/jm.game.ypvpa.com\/kitchen_api\/alipay_comm\/weixin_data",
                "version_id": "2019-4-28",
                "force_version_id": "2019-4-28",
                "log_information": "首次版本"
            }
        }
    }
}
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "version": {}
    }
}
```  
[接口目录](#接口目录)

### 资质条款

> 接口地址 /about/mine_clause

> 请求方式 POST

> ** 传递参数 Request Data : **
```
int         reqTime     
string      checksum 
```

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "ok",
    "data": {
        "about": {
            "id": 38,               【关于ID】
            "title": "平台业务主体",      【题目】
            "create_time": "2019-04-29 19:05:25",       【创建时间】
            "body": "平台业务主体<br />",             【内容】
            "create_time_string": "2019-04-29"          【创建时间显示】
        }
    }
}
```  
[接口目录](#接口目录)

### H5首页3U
 
 > 接口地址 /h5/index_3u
 
 > 请求方式 GET
 
 > ** 传递参数 Request Data : **
 ```
 int         reqTime     
 string      checksum 
 string      mobile_id
 string      session_id        
 string      session_security
 ```
 
 > ** 返回参数 Response Data : **
 ```
 H5 页面
 
 {
     "responseCode": "10007",
     "responseMessage": "token失效，请重新登录",
     "data": {}
 }
```  
[接口目录](#接口目录)


