---
title: nvm使用
date: 2015-09-13 23:12:06
tags: node.js
---

# 1. 安装脚本

```

# 这里的 v0.31.1 是版本号，应该以最新版本号为主, 参考 https://github.com/creationix/nvm
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.1/install.sh | bash
```

执行完这个步骤之后，有以下改变：

+ 在$HOME目录下包含`.nvm`，这是一个使用 `git` 管理的项目，也就是说，当我们要更新 `nvm版本`，可以基于 `git` 来更新

+ 在$HOME/.bash_profile里，包含了以下内容：

    ```

export NVM_DIR="/Users/dxlau/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm
    ```

`nvm.sh` 脚本导出了一些便于操作的环境变量 （env | grep NVM）:

```

NVM_CD_FLAGS=

NVM_PATH=$HOME/.nvm/versions/node/v6.2.2/lib/node

NVM_DIR=$HOME/.nvm

NVM_NODEJS_ORG_MIRROR=https://nodejs.org/dist

NVM_BIN=$HOME/.nvm/versions/node/v6.2.2/bin

NVM_IOJS_ORG_MIRROR=https://iojs.org/dist

```

当我们需要针对 `nodejs` 或 `iojs` 设置国内镜像时，就可以通过修改对应的环境变量来达到目的

# 2. 测试安装是否成功

```

command -v nvm

只要输出`nvm`就可以了

```

# 3.使用

常用的命令在 `$NVM_DIR/README.markdown` 文件里都有示例

## 3.0 查看nvm支持哪些命令

```

nvm --help

```

## 3.1 查看本地安装了哪些版本

```

nvm ls

```

## 3.2 查看远程有哪些版本可用

```

nvm ls-remote

```

## 3.3 安装指定版本

```

nvm install NODE_AVAILABEL_VERSION

如：nvm install v6.9.1

```

**NOTE: **安装成功后，需要新开一个窗口执行 `nvm use NODE_VERSION` 进行切换

## 3.4 查看指定版本安装位置

```

nvm which NODE_AVAILABEL_VERSION

```

## 3.5 使用特定版本

```

nvm use NODE_INSTALLED_VERSION

```

再次输入 `nvm ls` 可以看到箭头指向特定版本


## 3.6 使用国内的nodejs镜像

如果不使用国内镜像的话，每次使用 `nvm install NODE_VERSION` 时，默认都会从 `https://nodejs.org/dist` 下载安装包，下载速度会比较慢。

阿里提供的镜像地址挺好用的，[淘宝NPM镜像](https://npm.taobao.org/)

```

// 如下命令导出的 NVM_NODEJS_ORG_MIRROR 环境变量只在当前shell窗口有用，可考虑在 .bash_profile 中导出

export NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node

nvm install NODE_VERSION

```

# 4.资源

[NVM in github](https://github.com/creationix/nvm)