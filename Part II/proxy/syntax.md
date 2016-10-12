# 配置语法

```
### domain### location### 命令### 注释
```

## 变量

#### 语法

```bash
$变量名
```

#### 例子

```bash
# 使用变量
$var_name

# 定义变量
set $var_name value
```




## domain

`domain` 用来指定一个域名，这个域名的所有配置都在 `domain` 块中。

#### 语法：

```bash
[域名|变量] => {
    # ...
}
```

#### 例子

```bash
# 直接使用域名
some.example.com => {
    # ...
}

# 或者使用变量
$domain => {
    # ...
}
```





## location

`location` 用来指定域名中的一个具体的路径，这个路径的所有配置都在 `location` 块中。

注意:**`location`必须位于`domain`块中**。


#### 语法

```bash
location [目录|文件|正则表达式|变量] {
    # ...
}
```

#### 例子

```bash
# 目录
location /some/path/ {
    # ...
}

# 具体文件
location /some/file.htm {
    # ...
}

# 正则表达式

location ~ /^\/some\/(path|path1)\/.*/ {
    # ...
}

# 变量

location $some/$path {
    # ...
} 
```






## 命令

命令用于设置一些变量，或者对`request`/`response`做一些操作。

#### 语法

```bash
命令 参数1 参数2 ... 参数N
```

#### 例子

```bash
# 设置代理时的头部
proxy_set_header Host some.example.com;

# 设置response的cookie
set_cookie UserID some_user_id;
```




## 注释

用来注释某些不需要的内容，**只支持单行注释**。

#### 语法

```bash
# 注释内容
```

#### 例子

```bash
# 注释内容
set var value; # 设置变量
```



#### 简写语法

简写语法，可以用来定义一些基本的规则，不需要写`location`和其他的命令.

#### 语法

```bash
域名 ==> 域名|路径
```

#### 例子

```bash
json.example.com => 127.0.0.1:8800;
```





## 完整的例子

```bash
## url rewrite rules
# page.example.com => hii.com;
## json.example.com => 127.0.0.1:8800;

### rewrite folder

# api.example.com/user/ => {
#     proxy_pass other.example.com/user/;
#
#     ## proxy request config
#     proxy_set_header host api.example.com;
#     proxy_set_header other value;
#     proxy_hide_header key;
#
#     proxy_set_cookie userid 20150910121359;
#     proxy_hide_cookie sessionid;
#
#     ## response config
#     set_header Access-Control-Allow-Origin *; 
#
#     # allow CORS
#     set_cookie sessionID E3BF86A90ACDD6C5FF49ACB09;
#     hide_header key;
#     hide_cookie key;
# }

## regexp support
# ~ /\/(demo|example)\/([^\/]*\.(html|htm))$/ => {
#    proxy_pass http://127.0.0.1:9999/$1/src/$2;
#
#    set_header Access-Control-Allow-Origin *;
# }

## simple rewrite rule
usercenter.example.com => $domain/test;
flight.qunar.com/flight_qzz => 127.0.0.1:8800/flight_qzz;

set $domain api.example.com;
set $local 127.0.0.1:8800;
set $flight flight;
set $test $flight.example.com;
set $id 1234567;

## standard rewrite url
$domain => {
    proxy_pass http://127.0.0.1:8800/news/src/mock/;
    set $id 1234;
    set $mock_user user_$id;
    set_header Host $domain;
    set_header UserID $mock_user;
    set_header Access-Control-Allow-Origin *;
}

# api.example.com => {
#     proxy_pass http://$local/news/src/mock/list.json;
#     set_header Access-Control-Allow-Origin *;
# }

api.qunar.com => {
    set_header Access-Control-Allow-Origin *;
    set $node_server 127.0.0.1:3008;
    set $order order;
    set $cookie1 login=true;expires=20160909;
    location /$flight/$order/detail {
        proxy_pass http://$node_server/user/?domain=$domain;
        set_header Set-Cookie userID 200908204140;
    }

    location ~ /\/(usercenter|userinfo)/ {
        set $cookie login=true;expires=20180808;
        proxy_pass http://127.0.0.1:3008/info/;
        set_cookie userID 200908204140;
        set $id user_iddddd;
        set_cookie $flight zdy_$id;
    }
}
```

