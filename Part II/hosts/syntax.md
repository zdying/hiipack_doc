# 语法

语法跟系统`hosts`语法基本一致，唯一不一样的地方就是，hiipack的`hosts`支持**IP+端口**，语法如下:

```
IP[:端口] 域名1 域名2 域名3 ... 域名N
```

```
# custom hosts with port :)

# comment
# 127.0.0.1 hiipack.com
# 127.0.0.1:8800 hiipack.com
# 127.0.0.1:8800 hiipack.com hii.com

127.0.0.1:8800 hiipack.com hii.com

127.0.0.1 example.com example.com.cn

```