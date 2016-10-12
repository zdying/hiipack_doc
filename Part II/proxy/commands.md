# 指令

`指令`（也称：`命令`）用于设置变量，或者对`request`/`response`做一些操作。

## hiipack 支持的指令


### 代理请求相关

代理请求相关的指令，用于操作代理服务向目标服务器发送请求的`Request`对象。


#### proxy_set_header

作用：设置请求头部字段

参数：
    
    key：字段名称
    value：字段值

例子：

```bash
proxy_set_header Host some.example.com
```




#### proxy_hide_header

作用：删除请求头部字段

参数：

    key: 要删除的字段名称

例子：

```bash
proxy_set_header Host some.example.com
```




#### proxy_set_cookie

作用：设置请求Cookie

参数：

    key：Cookie名称
    value：Cookie值


例子：

```bash
proxy_set_cookie from hiipack;

```



#### proxy_hide_cookie

作用：删除请求Cookie字段

参数：
    
    key：Cookie名称


例子：

```bash
proxy_hide_cookie from;
```


### 代理响应相关

代理响应相关的指令用于配置代理服务器响应浏览器的`Response`对象。



#### hide_cookie

作用：删除Cookie字段

参数：

 key：Cookie名称

例子：

```bash
hide_cookie Access-Control-Allow-Origin;
```



#### hide_header

作用：删除Header字段

参数：

 key：Header字段名称

例子：

```bash

hide_header Server;

```

'hide_header': function(key, value){ log.debug('hide_header -', this, key, value); delete this.response.headers[key]; }, 'set_header': function(key, value){ log.debug('set_header -', this, key, value); this.response.headers[key] = value; }, 'set_cookie': function(key, value){ log.debug('set_cookie -', this, key, value); this.response.headers['Set-Cookie'] = key + '=' + value; }, proxy_pass: function(value){ this.props.proxy = value; }, // global commands 'set': function(key, value){ this.props[key] = value; }};
