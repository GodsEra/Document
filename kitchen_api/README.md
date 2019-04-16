# Document
大神时代接口文档


# Demo

> **API 接口返回说明文档**

> **导航: 用户信息**

> 接口地址 /user 请求方式 GET

> **传递参数 Request Data : **
```
formdata 格式

id=1
keyword=123
```

>**返回参数 Response Data :**
```
// 20170912101719
// http://www.xxx.com/user

{
  "code": 200,
  "msg": "查询成功",
  "data": {
  }
}

```

> **状态码说明**
```
code 响应状态 100 未登录 200 操作成功 400 操作失败 500异常输出信息
msg  响应信息
data 响应数据 具体参考其接口文档
```