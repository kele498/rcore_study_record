# rcore 训练营学习记录

## 背景链接

- 第二阶段: <https://github.com/LearningOS/rust-based-os-comp2023/blob/main/2023-autumn-scheduling-2.md>
- 官方文档：<https://learningos.cn/rCore-Tutorial-Guide-2023A/0setup-devel-env.html>

## 2023-10-24

### 搭建环境

- 使用 Windows WSL2 开发环境
- 检查 windows 中 wsl 版本：`wsl -l -v`  
- wsl 设置代理：开启 Clash for Windows 中的 tun mode 即可

### 安装 rustc

- 设置镜像

    ``` sh
    export RUSTUP_DIST_SERVER=https://mirrors.ustc.edu.cn/rust-static
    export RUSTUP_UPDATE_ROOT=https://mirrors.ustc.edu.cn/rust-static/rustup
    ```

- 使用官方安装脚本 `curl https://sh.rustup.rs -sSf | sh`
- 手动更新环境变量  `source "$HOME/.cargo/env"`
- 检查 rustc 版本  `rustc --version`

### 安装 Qemu 模拟器

- 安装命令：

    ``` sh
    # 需要先执行 update，要不会有很多依赖装不上
    sudo apt update
    # 安装编译所需的依赖包
    sudo apt install autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev \
                gawk build-essential bison flex texinfo gperf libtool patchutils bc \
                zlib1g-dev libexpat-dev pkg-config  libglib2.0-dev libpixman-1-dev git tmux python3
    # 下载源码包
    # 如果下载速度过慢可以使用我们提供的百度网盘链接：https://pan.baidu.com/s/1z-iWIPjxjxbdFS2Qf-NKxQ
    # 提取码 8woe
    wget https://download.qemu.org/qemu-7.0.0.tar.xz
    # 解压
    tar xvJf qemu-7.0.0.tar.xz
    # 编译安装并配置 RISC-V 支持
    cd qemu-7.0.0
    # 需要安装 ninja-build
    sudo apt install ninja-build
    ./configure --target-list=riscv64-softmmu,riscv64-linux-user
    make -j$(nproc)
    ```

- 设置环境变量

    ``` sh
    export PATH="$HOME/os-env/qemu-7.0.0/build/:$PATH"
    export PATH="$HOME/os-env/qemu-7.0.0/build/riscv64-softmmu:$PATH"
    export PATH="$HOME/os-env/qemu-7.0.0/build/riscv64-linux-user:$PATH"
    ```

- 检查 qemu 版本

    ``` sh
    qemu-system-riscv64 --version
    qemu-riscv64 --version  
    ```
