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

测试地址：http://distributionapi.marketing.ypvpa.com          

正式地址：http://distributionapi.marketing.yuqg.com                
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

### 第一步请求 mobile_id

> 接口地址 /kitchen_api/plugin/get_mobile_id 

> 请求方式 POST

> **传递参数 Request Data : **
```
platform  【ios，android】
device_id  【设备号】
reqTime     
checksum 
```

>**返回参数 Response Data :**
```
{
    "responseCode": 0,
    "responseMessage": "ok成功",
    "data": {
        "mobile_id": "ios_V3ERydy5Kqcv"
    }
}

```
