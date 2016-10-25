# 自定义插件\/loader

### 自动安装依赖 {#auto-install}

项目中，肯定会用到许多`插件`和`loader`，以前我们会将这些第三方的依赖，安装到项目里面，也就是会添加到`package.json`中的`devDependencies`字段中，这样其他人 clone 下这个项目后，执行`npm install`后就可以运行工程了。

Hiipack 支持自定义`插件`和`loader`自动安装，用户可以不需要手动安装到项目并设置`devDependencies`字段。当 Hiipack 解析配置文件时，发现自定义`插件`或者`loader`的不存在的时候会自动安装所需的依赖到临时目录中。

#### 自动安装的好处 {#benefit}

1. 用户可以不用关心这些第三方依赖的管理，不需要安装到项目中，这样可以保持项目中`package.json`和`node_modules`的清洁，用户安装的依赖，就是最终需要打包的代码，不需要关心开发环境相关的代码。

2. 安装到临时目录的第三方依赖，可以在多个项目中共享，不用重复安装。

3. 可以充分共享 Hiipack _**默认已经安装的一些模块**_ 和 _**全局的模块**_，比如 Hiipack 依赖了`less`, 用户如果也需要`less`，可以直接使用 Hiipack 已经安装好的。


当然，自动依赖也有一些不足之处。需要我们自己去克服。

#### 自动安装的不足 {#insufficient}

1. 版本号问题，如果某个项目需要依赖特定版本的某个第三方插件或者loader，而其他项目不兼容这个版本，需要其他的版本。这时候，Hiipack 也不知道怎么办了。

2. 临时目录，可能会被定期清除，这样就会导致，可能多次安装，因为 Hiipack 解析到某个插件或者loader的时候，临时目录没有了，就会自动安装。


#### 怎么解决上面的不足？ {#how-to-solve}

在`require`一个模块的时候，可以使用绝对路径。要获取模块的绝对路径，可以使用`require.resolve(module_name)`。

Hiipack 也提供了一个全局的方法`__hiipack__.resolve(module_name)`或者`__hii__.resolve(module_name)`，调用这个方法，Hiipack 会按照如下顺序查找已经安装的模块：

1. Hiipack 根目录的`node_modules`

2. Node.js 全局模块目录（`npm root -g`）

3. Hiipack 临时目录


如果找到，返回模块的绝对路径，如果找不到，返回空。

这样，解决上面的_**问题1**_，就有了思路:

以`vue-loader`为例子，假如我们需要特定的版本`8.5.4`，我们可以把这个版本的`vue-loader`安装到项目中，然后使用`require.resolve("vue-loader")`获取到绝对路径，然后配置：

```javascript
{ 
    test: /\.vue$/, 
    loader: require.resolve('vue-loader') 
}
```

那 _**问题2**_ 呢？

Hiipack 目前还没有去处理，如果被清除了，下次重新安装，保证代码正常运行，以后的版本中，Hiipack 会开辟其他的地方（比如：用户目录）去存储以避免这样的问题。

