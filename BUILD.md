## 源码下载

```plain
$ git clone https://github.com/Project-LemonLime/Project_LemonLime.git --recursive
```

### 下载的东西太大了？

`git clone` 的时候，使用 `--depth=1` 可以使下载下来的文件大小减少很多（因为默认情况下它会把所有历史记录全部下载下来）。

### 如果 Github 还是太慢…

你也许可以到 `码云（Gitee）` 去下载。

在很多地区，从 `码云` 下载的速度是从 `Github` 下载的速度的 100 倍。

[这个仓库在码云下的镜像](https://gitee.com/iotang/Project_LemonLime)

## Windows

去 `Releases` 下载就可以了。

### Scoop 用户

添加[第三方 bucket](https://github.com/ChungZH/peach) 即可快速安装与更新

```powershell
scoop bucket add peach https://github.com/ChungZH/peach
scoop install peach/lemon
```

当然如果你装有 Qt 5/6，也可以下载源码编译。

NOTE: XLS 导出是默认关闭的，如需使用，请编译时附加 `-DENABLE_XLS_EXPORT` 启用。

### 非常严重的提示

由于 Windows 的特殊性，请在下载 `Releases` 后检查 LemonLime 的功能的完整性，比如是否能探测程序的运行时间和使用内存。不过如果使用源码构建 LemonLime 的话将不会出现这种问题，所以仍然推荐使用源码构建 LemonLime。

> 在很多地方，下载 Qt 的时间 + 安装 Qt 的时间 + 下载 LemonLime 源代码的时间 + 编译的时间 &lt; 从 Github 上下载可执行文件的时间。
>
> 下载 Qt 请考虑一个快速的国内镜像。

## Linux

### Arch Linux 系

```bash
## 迅速安装 ##
yay -S lemon-lime # 稳定版本
yay -S lemon-lime-git # 开发版本（提前使用许多新功能！）
# 感谢 @ayalhw 的支持。

## 使用 CMake ##
sudo pacman -S gcc cmake qt5-base ninja make # 依赖环境(ninja 和 make 二选一)
cd 源代码的目录
cmake . -DCMAKE_BUILD_TYPE=Release -GNinja # 如使用 make 请删去 -GNinja
cmake --build . --parallel $(nproc)  # 获得可执行文件 lemon

## 使用 QtCreator ##
sudo pacman -S qtcreator
```

### Debian | Ubuntu 系

```bash
## 使用 CMake ##
sudo apt install qt5-default build-essential ninja-build qtbase5-dev qttools5-dev cmake # 依赖环境, ninja 可选
cd 源代码的目录
cmake . -DCMAKE_BUILD_TYPE=Release -GNinja # 如使用 make 请删去 -GNinja
cmake --build . --parallel $(nproc)  # 获得可执行文件 lemon

cmake --install . # 将其安装到系统中，默认安装位置位于 /usr/local
# 或者直接生成 DEB 包
cmake . -DCMAKE_BUILD_TYPE=Release -GNinja -DBUILD_DEB=ON
cmake --build . --parallel $(nproc)

## 使用 QtCreator ##
sudo apt install qtcreator
```

#### \* Ubuntu 18 及更老 (包括 NOI Linux 这种毒瘤

Ubuntu 18 用 apt 安装的 Qt 版本只能到 5.9。

Ubuntu 16 用 apt 安装的 Qt 版本只能到 5.5。
GCC 不支持 C++17, 可以自己去 CMakeLists.txt 把标准改成 11, 能不能编译听天由命（目前还是可以的，等到迁移 Qt6 估计就不行了

NOI Linux 是 Ubuntu 14.04 的换皮，所以用 apt 安装的 Qt 版本只能到 5.2。

_arbiter 退出了群聊。_

### Fedora 系

```bash
## 使用 CMake ##
sudo dnf install cmake qt5-qtbase-devel qt5-linguist qt5-qtsvg-devel desktop-file-utils ninja-build make # 依赖环境(ninja 和 make 二选一)
cd 源代码的目录
cmake . -DCMAKE_BUILD_TYPE=Release -GNinja # 如使用 make 请删去 -GNinja
cmake --build . --parallel $(nproc) # 获得可执行文件 lemon

cmake --install . # 将其安装到系统中，默认安装位置位于 /usr/local

# 或者直接生成 RPM 包
sudo dnf install cmake qt5-qtbase-devel qt5-linguist qt5-qtsvg-devel desktop-file-utils ninja-build redhat-lsb-core fedora-packager rpmdevtools
cmake . -DCMAKE_BUILD_TYPE=Release -GNinja -DBUILD_RPM=ON
cmake --build . --parallel $(nproc)
```

### openSUSE 系

```bash
## 使用 CMake ##
sudo zypper in cmake libqt5-qtbase-common-devel libQt5Core-devel libQt5Gui-devel libQt5Network-devel libQt5Widgets-devel libQt5Concurrent-devel libqt5-linguist-devel libqt5-qtsvg-devel update-desktop-files ninja # 依赖环境(ninja 和 make 二选一)
cd 源代码的目录
cmake . -DCMAKE_BUILD_TYPE=Release -GNinja # 如使用 make 请删去 -GNinja
cmake --build . --parallel $(nproc) # 获得可执行文件 lemon

cmake --install . # 将其安装到系统中，默认安装位置位于 /usr/local

# 或者直接生成 RPM 包
sudo zypper in cmake libqt5-qtbase-common-devel libQt5Core-devel libQt5Gui-devel libQt5Network-devel libQt5Widgets-devel libQt5Concurrent-devel libqt5-linguist-devel libqt5-qtsvg-devel update-desktop-files ninja lsb-release rpm-build
cmake . -DCMAKE_BUILD_TYPE=Release -GNinja -DBUILD_RPM=ON
cmake --build . --parallel $(nproc)
```

## etc.

有 AppImage 可用（虽然丑了点

前往 Actions 或者 Release 界面下载，
`chmod +x xxxx.AppImage` 再执行即可（注意从 Actions 下载到的是一个压缩包

PS：有可能会提示缺少 fuse, 请安装

## macOS

在没有 macOS 机子的情况下写 macOS 支持是一件非常滑稽的事。

请使用 `watcher_macos.cpp` 编译 `watcher_unix`，否则内存限制会出问题。

```bash
cmake -DCMAKE_BUILD_TYPE=Release -GNinja .
cmake --build .
```