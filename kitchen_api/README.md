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

## 接口目录

[请求 mobile_id](#请求mobile_id)  
   
[登录](#登录)  

[分类页面](#分类页面)  

[分类页面V2](#分类页面V2)  

[获取二级分类](#获取二级分类)  

[获取商品列表](#获取商品列表)  

[计算购物车](#计算购物车)  

[商品详情页面](#商品详情页面)  

## 请求接口

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

> ** 返回参数 Response Data : **
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
                    "spec_count": 2,                【包含的规格数量】
                    "spec_list": [              【规格列表】
                        {
                            "id": 5,            【规格ID】
                            "price": "0.01",    【规格售价】
                            "source_price": "20.00",    【规格原始标价】
                            "name": "2斤",       【规格单位】
                            "unit": "kg"        【规格单位注释】
                        },
                        {
                            "id": 6,
                            "price": "0.01",
                            "source_price": "38.00",
                            "name": "半斤",
                            "unit": "500g"
                        }
                    ],
                    "status_name": null
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
                    "spec_count": 3,
                    "spec_list": [
                        {
                            "id": 13,
                            "price": "11.00",
                            "source_price": "22.00",
                            "name": "22",
                            "unit": "22"
                        },
                        {
                            "id": 14,
                            "price": "213.00",
                            "source_price": "2131.00",
                            "name": "3213",
                            "unit": "3213"
                        },
                        {
                            "id": 15,
                            "price": "3123.00",
                            "source_price": "131.00",
                            "name": "3123",
                            "unit": "3123"
                        }
                    ],
                    "status_name": null
                }
            ],
            "count": 2,         【列表总数】
            "total_page": 1,    【分页总数】
            "current_page": 1,  【当前页】
            "pagesize": 2       【每页数量，与limit一致】
        }
        
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

### 获取商品列表

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
                    "spec_count": 2,                【包含的规格数量】
                    "spec_list": [              【规格列表】
                        {
                            "id": 5,            【规格ID】
                            "price": "0.01",    【规格售价】
                            "source_price": "20.00",    【规格原始标价】
                            "name": "2斤",       【规格单位】
                            "unit": "kg",        【规格单位注释】
                            "cart_buy_number": 15
                        },
                        {
                            "id": 6,
                            "price": "0.01",
                            "source_price": "38.00",
                            "name": "半斤",
                            "unit": "500g",
                            "cart_buy_number": 0
                        }
                    ],
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
                    "spec_count": 3,
                    "spec_list": [
                        {
                            "id": 13,
                            "price": "11.00",
                            "source_price": "22.00",
                            "name": "22",
                            "unit": "22",
                            "cart_buy_number": 0
                        },
                        {
                            "id": 14,
                            "price": "213.00",
                            "source_price": "2131.00",
                            "name": "3213",
                            "unit": "3213",
                            "cart_buy_number": 0
                        },
                        {
                            "id": 15,
                            "price": "3123.00",
                            "source_price": "131.00",
                            "name": "3123",
                            "unit": "3123",
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

> ** 返回参数 Response Data : **
```
{
    "responseCode": "0",
    "responseMessage": "执行成功",
    "data": {
        "cart_buy_numer": 23,               【此规格的购物车购买数量】
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
[接口目录](#接口目录)

### 商品详情页面

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
                    "unit": "1杯"            【规格单位注释】
                },
                {
                    "id": 11,
                    "price": "2.00",
                    "source_price": "1.00",
                    "name": "1",
                    "unit": "1"
                }
            ],
            "distribution_price": 0,            【运费】
            "monthly_order_number": 0           【月销量】
        },
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

### 购物车信息

> 接口地址 /cart/cart_list

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
                "good_title": "回锅肉",             【商品名】
                "good_litpic": "http:\/\/www.ypvpa.localhost",      【商品图片】
                "name": "2斤",                   【规格单位】
                "unit": "kg"                    【规格单位注释】
                "source_price": "22.00",            【规格原始标价】
                "price": "11.00"                    【规格售价】
            },
            {
                "spec_id": 13,
                "buy_number": 2,
                "good_title": "回锅肉",
                "good_litpic": "http:\/\/www.ypvpa.localhost",
                "name": "22",
                "unit": "22",
                "source_price": "22.00",
                "price": "11.00"
            },
            {
                "spec_id": 12,
                "buy_number": 8,
                "good_title": "甜面包",
                "good_litpic": "http:\/\/www.ypvpa.localhost\/uploads\/goods\/cover\/20190404\/fe2cc5b880865c84195ad155f2aae2d3.jpg",
                "name": "1",
                "unit": "1",
                "source_price": "1.00",
                "price": "1.00"
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
