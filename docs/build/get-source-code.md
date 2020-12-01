---
id: get-source-code
title: "获取源码"
sidebar_label: "获取源码"
---

注：该文档中均使用 `$AKMC_PATH` 来指代 MISA-AKMC 源码目录

## 1. 获取源码
你可以使用以下任意一种方式获取代码：git clone、下载源码包。
如果你已经拥有源代码，可以忽略此步骤，直接跳到[安装依赖](#2-安装依赖)小节。

### 1.1 git clone
如果你的系统中安装了 git 工具，可以使用 git clone 来拷贝仓库到本地。
这样的好处是，你可以随时切换使用其他任意版本的代码。
```bash
git clone https://git.hpcer.dev/HPCer/misa-akmc/kmc.git # https
```

或者，如果你配置了ssh key, 也可以使用 ssh 协议进行 clone:
```bash
git clone ssh://git@git.hpcer.dev:2222/HPCer/misa-akmc/kmc.git # ssh
```

上述 git clone 命令会创建一个名为 kmc 的目录。
克隆完成后，你可以选择通过调用以下命令来构建特定分支（如版本分支）
```bash
$ cd $MD_PATH # MISA-MD 源码目录
$ git checkout Branch_Or_Tag
# where ' Branch_Or_Tag' is the desired branch or tag.
```
例如，要使用 v0.1.0 版本而不是主分支，可使用以下命令进行切换 `git checkout v0.1.0`.

### 1.2 直接下载源码包
使用wget命令或者在浏览器中下载源代码压缩包。  
如，下载v0.4.0版本的源码包：
```bash
$ wget -O kmc-v0.1.0.tar.gz \
  https://git.hpcer.dev/HPCer/misa-akmc/kmc/-/archive/v0.1.0/kmc-v0.1.0.tar.gz
$ tar -zxvf MISA-MD-v0.4.0.tar.gz
```

## 2. 安装依赖

获取的源码中不包含该程序的依赖包，所以还需要额外的工作来安装依赖。

MISA-MD 依赖于一些开源库, 如[kiwi](https://git.hpcer.dev/genshen/kiwi),
googletest, [xoshiro](https://github.com/misa-kmc/xoshiro), [libcomm](https://git.hpcer.dev/HPCer/CrystalMD/libcomm)等。
可以使用[pkg](https://github.com/genshen/pkg)依赖管理工具下载依赖包或者直接将对应依赖包导入到 MISA-AKMC 源码`vendor`目录。

其中，`pkg` 工具的安装见 https://github.com/genshen/pkg/。

以下三种依赖安装方式选择其一即可：

### 2.1 使用 pkg 安装依赖
使用该方式安装依赖，需要你的系统能够连接到互联网，且有所有依赖仓库的 git 克隆权限。
可以通过设置 `PKG_AUTH` 环境变量的方式指定获取相关私有仓库的口令，
如 `PKG_AUTH=username?token@git.hpcer.dev` 指定了获取位于 git.hpcer.dev 上的私有依赖库的用户名和认证 token。

依赖安装：
```bash
cd $MD_PATH
PKG_AUTH=username?token@git.hpcer.dev pkg fetch
pkg install
```

### 2.2 使用 pkg 导入依赖包
假设依赖压缩包文件名为: vendor-20190725-003851.426644.tar, 可以通过以下 pkg 命令导入依赖包:
```bash
cd $MD_PATH
pkg import --input vendor-20190725-003851.426644.tar
pkg fetch
pkg install
```

### 2.3 直接解压依赖包

直接导入依赖是将已有的依赖压缩包解压解压 MISA-MD 的源码的 `vendor` 目录。

假设依赖压缩包文件名为：vendor-20190725-003851.426644.tar, 可以通过以下命令加入依赖包:
```bash
mkdir -p $MD_PATH/vendor
cd $MD_PATH/vendor
tar xvf path/of/vendor-20200725-003851.426644.tar # tar to direcooty.
```
