---
title: npm使用
date: 2015-09-19 23:00:56
tags: npm
---

## 1. 它是什么?
全称为`Node Package Manager`，大大简化了共享、重构代码的痛点
[官方介绍](https://docs.npmjs.com/getting-started/what-is-npm)

## 2. package.json
用来管理本地安装Package的最好方式，可以使用`npm init`来创建, 它有以下作用：
* 展示你的项目依赖哪些PKG
* 可以指定PKG的版本
* 便于稳定地构建


最简单的格式:
```
{
    # name的值是`小写的`、`一个词语，不能有空格`、`可以用 . 和 _ `
    "name": "my-awesome-pkg",
    # 格式为`x.x.x`
    "version": "1.0.0"
}
```

**定义依赖:**
包含`两种`类型的依赖:
* dependencies: 用在生产环境的依赖
* devDependencies: 用在开发环境的依赖

如下所示
```
{
    "name": "my_package",
    "version": "1.0.0",
    "dependencies": {
        "my_dep": "^1.0.0"
    },
    "devDependencies" : {
        "my_test_framework": "^3.1.0"
    }
}
```

## 3. 安装/卸载本地模块
默认安装方式就是本地安装
```
# 1. 默认安装
npm install PKG_NAME
## 1.1. 安装prod环境的依赖
npm install PKG_NAME --save
## 1.2. 安装dev环境的依赖
npm install PKG_NAME --save-dev

# 2. 卸载
npm uninstall PKG_NAME
## 2.1 卸载prod环境的依赖
npm uninstall --save PKG_NAME
## 2.2 卸载dev环境的依赖
npm uninstall --save-dev PKG_NAME
```
一旦输入这个命令后，那么，在当前目录下就会创建`node_modules`文件夹，并下载指定模块到这个目录


## 4. 安装/卸载全局模块
参照本地安装的格式，加入`-g`选项即可，如:
```
npm install -g PKG_NAME
```

## 5. 更新依赖
进入`package.json`所在目录，输入以下命令即可:
```
# 1. 执行更新
npm update
# 2. 测试是否有延迟的信息
npm outdated
```

## 6. 发布Package
参考 [这里](https://docs.npmjs.com/getting-started/publishing-npm-packages)

## 7. npm配置信息
npm可以从`命令行`、`环境变量`以及`npmrc文件`获取配置信息

可以通过以下命令查看配置信息:
```
# 1. 列出所有配置信息
npm config ls -l
```

### 7.1 npmrc文件
有`4`个地方可以包含此文件，优先级`逐渐降低`:
* 项目内的.npmrc文件
* 用户级别的.npmrc文件，$HOME/.npmrc
* 全局.npmrc文件，$PREFIX/etc/.npmrc
* npm内置.npmrc文件，/path/to/npm/.npmrc

**NOTE:**内容格式都是`KEY = VALUE`形式

配置示例（$HOME/.npmrc）:
```
# 1. 配置淘宝npm镜像
registry = "https://registry.npm.taobao.org/"
```
或
```
npm config set registry https://registry.npm.taobao.org
```