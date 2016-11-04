# 配置命令

全局配置，可以采用`hii config [operation] [args...]`或者`hiipack config [operation] [args...]`。

其中`operation`可以是下面中的一个:

## list

> 列出现在所有的配置字段

比如：
```bash
$ hiipack config list

registry=http://registry.npm.corp.qunar.com/
system_proxy=myproxy.com:25
```


## set

> 设置某个字段

比如: 

```bash
hii config set config_field config_value
```


## delete

> 删除某个配置字段

比如：

```bash
hiipack config delete config_field
```
