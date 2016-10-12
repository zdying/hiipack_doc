# 安装

## 从 NPM 安装

Hiipack 已经发布到 [npmjs.com](https://www.npmjs.com/) , 可以通过npm安装：

```bash
npm install -g hiipack
```

如果要安装 DEV 或者 BETA 版本（不稳定），可以使用：

```bash
npm install -g hiipack@dev  # dev版本
npm install -g hiipack@beta # beta版本
```

> 提示：
> 
> 1. 国内用户推荐使用淘宝的NPM源，安装速度比较快
> 
> 2. hiipack 默认支持css/less/sass，所以依赖 node-sass, 安装 node-sass 需要从 github 下载文件，所以比较慢，推荐使用淘宝 node-sass 镜像
> 
> 3. 为了解决以上两个问题，可以使用下面的代码安装

```bash
# node-sass二进制文件镜像 
export SASS_BINARY_SITE="https://npm.taobao.org/mirrors/node-sass" 

# 安装 
npm install hiipack -g --registry=https://registry.npm.taobao.org
```

## 从 Github 安装

也可以从 Github 源码安装：

```bash
# 从master分支安装
npm install -g zdying/hiipack

# 从特定分支安装
npm install -g https://github.com/zdying/hiipack#branch-name
```

## 检查是否安装成功

hiipack 安装完成后，系统中会增加 `hiipack`命令和 `hii` 命令，两个一样，后者更简短。可以执行 `hiipack` 或者 `hii`, 如果能看到版本信息，表示安装成功。

使用 `hii -h` 或者 `hii --help`可以查看帮助信息。

