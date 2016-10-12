# 指令

`指令`（也称：`命令`）用于设置变量，或者对`request`\/`response`做一些操作。

## hiipack 支持的指令

### 代理请求相关

代理请求相关的指令，用于操作代理服务向目标服务器发送请求的`Request`对象。

#### proxy\_set\_header

作用：设置请求头部字段

参数：

```
key：字段名称
value：字段值
```

例子：

```bash
proxy_set_header Host some.example.com
```

#### proxy\_hide\_header

作用：删除请求头部字段

参数：

```bash
key: 要删除的字段名称
```

例子：

```bash
proxy_set_header Host some.example.com
```

#### proxy\_set\_cookie

作用：设置请求Cookie

参数：

```bash
key：Cookie名称
value：Cookie值
```

例子：

```bash
proxy_set_cookie from hiipack;
```

#### proxy\_hide\_cookie

作用：删除请求Cookie字段

参数：

```bash
key：Cookie名称
```

例子：

```bash
proxy_hide_cookie from;
```

### 代理响应相关

代理响应相关的指令用于配置代理服务器响应浏览器的`Response`对象。

#### set\_header

作用：添加Header字段

参数：

```bash
key：Header字段名称
value：Header字段的值
```

例子：

```bash
hide_header Server;
```




#### hide\_header

作用：删除Header字段

参数：

```bash
key：Header字段名称
```

例子：

```bash
hide_header Server;
```





#### hide\_cookie

作用：删除Cookie字段

参数：

```bash
key：Cookie名称
```

例子：

```bash
hide_cookie Access-Control-Allow-Origin;
```

'set\_header': function\(key, value\){ log.debug\('set\_header -', this, key, value\); this.response.headers\[key\] = value; }, 'set\_cookie': function\(key, value\){ log.debug\('set\_cookie -', this, key, value\); this.response.headers\['Set-Cookie'\] = key + '=' + value; }, proxy\_pass: function\(value\){ this.props.proxy = value; }, \/\/ global commands 'set': function\(key, value\){ this.props\[key\] = value; }};

