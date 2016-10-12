# hiipack代理使用方法

## 推荐方式 {#recommand}

要使用 hii 的代理功能，两个步骤即可：

1. **创建代理配置文件**
2. **启动本地服务时添加参数: **`--proxy --open`** 或者 **`-xo`

> 提示:
> 
> 1. `-x`或者`--proxy` ==&gt; 启动代理服务
> 
> 2. `-o`或者`--open` ==&gt; 打开浏览器窗口，默认Chrome

自动打开浏览器窗口的好处是：

* 自动配置代理，用户无需自己手动配置
* 没有hosts缓存问题
* 新打开的窗口独立于其他的浏览器窗口，互不影响

## 手动配置 {#config-yourself}

目前，hiipack 打开的 Chrome 浏览器窗口，不会加载用户以前的配置、插件，这样从某种意义上不是很方便。

如果不让 hiipack 打开浏览器窗口，代理服务启动后，需要自己手动设置浏览器代理或者系统代理。

代理地址：

```
127.0.0.1:4936
```

这样浏览器里面**所有的**请求就会经过 hiipack 的启动在`4936`的服务。

这样会有一个问题就是，那些原本不需要走代理的地址，其实是没有必要通过 hiipack 代理的，这样增加了 hiipack 的负担，也影响了响应的速度。

因此，hiipack 还提供了一种代理的方式：**_自动代理_**（有关自动代理的内容，可以参考：[Proxy-Auto-Conifg](https://en.wikipedia.org/wiki/Proxy_auto-config) 或者 [PAC（代理自动配置）](http://baike.baidu.com/item/PAC/16292100)）。

有了自动代理，**只有用户配置的**`hosts`**中的域名和**`rewrite`**中的域名才会通过代理服务器**。

要使用自动代理，可以在 hiipack 启动日志中找到代理文件的路径，比如下面最后一行中的地址：

```bash
# hiipack 启动日志
current workspace /Users/zdying/work/test
hiipack started at http://127.0.0.1:8800
hiipack proxyed at http://127.0.0.1:4936
hiipack proxy file file:///usr/local/lib/node_modules/hiipack/src/proxy/pac/hiipack.pac
```

