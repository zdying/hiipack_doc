# 如何开始



## 初始化工程

```
hii init <project-name>
```

`hii init project-name` 会默认初始化一个项目，可以通过参数`-t`或者`--type`指定项目类型，参数可选值：

* `empty`: 空项目 
* `es6`: 使用ECMAScript 2015的项目
* `react`: 使用`react`的项目
* `react-redux`: 使用`react`和`redux`的项目
* `normal`: 普通项目， **默认为**`normal`**\*** 
* `vue`: Vue.js项目\(**hiipack本身不支持vue模板编译，但是简单配置就可以了**\)



## 启动本地服务

```
hii start
```

假设项目目录为`/Users/user-name/workspace/todo`, 初始化`todo`后，进入到**上一级目录**`/Users/user-name/workspace/`, 执行：`hii start`

默认端口是**`8800`**, 如果要自己指定端口，可以使用参数`-p <port>`或者`--port <port>`:

```
hii start -p 9876
```

如果要打开浏览器，可以使用参数`-o`或者`--open`:

```
hii start -p 9876 -o
#或者
hii start --port 9876 --open
```

默认情况下只显示`access`和`info`日志，**不会显示调试信息**，如果要显示可以使用参数`-d`或者`--debug`:

```
hii start -p 9876 -o -d
```



## 打包代码

```
hii pack
```

打包的代码，会根据配置文件，把文件打包到一起，但是不压缩混淆代码，打包的文件会添加版本号`@dev`。

打包后的代码位于`project/dev/`中。



## 打包压缩代码

```
hii min
```

构建线上环境的代码，代码会被打包到一起并且压缩，添加版本号`@[file_md5_hash]`。

打包后的代码位于`project/prd/`中。



## 上传代码到远程服务器

```
hii sync
```

把当前目录的代码上传到服务器，要上传的内容和服务器用户、IP、目录等配置，在项目根目录的`dev.json`中, 配置例子:

```json
{ 
    "source": "./", 
    "server": "192.168.100.200", 
    "path": "/path/to/your/project/", 
    "exclude": [
        ".git", ".DS_Store", "node_modules", "prd", "loc", "dll"
    ]
}
```




## 启动代理服务

如果要使用代理服务功能， 启动时添加参数`-x`或者`--proxy`, 默认端口为`4936`\(4 \* 9 = 36\) :\)。

启动代理服务后，hiipack会去解析工程根目录下面的`rewrite`文件，根据里面的配置规则转发请求。

启动代理服务后，可以省略本地配置`hosts`和启动`Nginx`服务。

> 提示：启动代理服务器后，建议同时打开浏览器窗口（添加参数: `-o`或者`--open`), 打开的浏览器窗口回自动配置好代理。

