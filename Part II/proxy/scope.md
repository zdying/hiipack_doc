# 作用域 {#scope}

作用域主要使用于**变量查找**和**指令执行**。

### 作用域

hiipack 配置文件中涉及到的作用域有三种：

* _全局作用域_：这里的变量可以在任何地方访问到
* _domain作用域_：位于全局作用域下一级
* _location作用域_：位于domain作用域下一级

### 作用域层级关系

```
global
    |- domain
    |   |- location
    |   |- location
    |   |- ...
    |- domain
    |   |- location
    |   |- location
    |   |- ...
```

### 变量查找

当前作用域中查找变量的规则为：

1. 如果当前作用域有这个变量，_返回_ 这个变量的值
2. 查找上一级作用域，如果上一级作用域中有这个变量，_返回_ 这个变量的值。
3. 否则，如果上一级作用域是全局作用域，_返回_ 变量名称（包括`$`符号\)。
4. _重复步骤__**\[**__**2-3\]**_

### 指令执行

下一级作用域中的指令在对应的时机（request／response）会自动执行，此外，还会执行上一级作用域中的指令，比如：

```
www1.test.com => {
    # 1    
    proxy_set_header Host www.test.com;

    location / {
        # 2
        proxy_pass http://52.88.88.88/;
    }

    location /index.html {
        # 3
        proxy_pass http://127.0.0.1:8800/opgirl_global/view/index.html;
    }

    location ~ /\/(native|gallery|picture|font|6cn)\/(.*)/ {
        # 4
        proxy_pass http://88.88.88.88/$1/$2;
    }
}
```

上面的配置中，\#2、\#3和\#4处，都会执行配置在\#1处的指令，也就是说: `/`、`/index.html`和`/\/(native|gallery|picture|font|6cn)\/(.*)/`对应的请求，都会加上请求头部`Host`，值为`www.test.com`

