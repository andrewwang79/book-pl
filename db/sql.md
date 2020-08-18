# SQL

## 常用
1. 变量定义
```
DECLARE @xyz varchar(50)
SET @xyz='hi'
```

1. 时间调整
```
pay_time = DATEADD(HH, 1, pay_time) // 增加1小时
```

1. null判断
```
xyz is null
xyz is not null
```

## 字符串
1. 前加字符串：xyz=CONCAT('hi', xyz) // 'hi' + xyz
1. 匹配：locate('http', xyz)=0 // 含有字符串'http'
1. 替换：xyz=REPLACE(xyz, 'hi', 'hello') // 'hi'替换成'hello'
