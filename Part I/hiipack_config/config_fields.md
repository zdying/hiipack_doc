# 支持的配置字段

### system_proxy

系统代理地址，启动hiipack时，如果添加参数`-xo`，会启动代理服务，同时打开浏览器窗口。这时候，用户`rewrite`或者`hosts`中配置的域名，会自动代理到`127.0.0.1:4936`，如果不在配置的域名列表中，就不会走任何代理。

设置了`system_proxy`后，没有在配置的域名中的其他域名，会走`system_proxy`对应的代理。

`system_proxy`的格式为:

```
domain:prot
```

比如：

```
proxy.my-domain.com:3456
```

### registry

配置`npm`源。

比如:

```
http://registry.npm.corp.qunar.com/
```

> **注意：** 启动服务时，也可以传入参数`--registry <url>`来指定


### sslKey

ssl 证书私钥文件路径

> **注意：** 启动服务时，也可以传入参数`--ssl-key <key-file-path>`来指定

### sslCert

ssl 证书文件路径

> **注意：** 启动服务时，也可以传入参数`--ssl-cert <cert-file-path>`来指定
