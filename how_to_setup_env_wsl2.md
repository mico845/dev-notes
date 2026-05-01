# how_to_setup_env_wsl2

**How to set up a C++ development environment on Windows 11 with WSL 2?**

---

## WSL2

这里以创建一个名为 `Ubuntu2404` 的 Ubuntu 24.04 发行版为例：

- WSL2 更新

  ```bash
  wsl --update
  ```

- 下载获取 Ubuntu-24.04 镜像到 `<Image Path>` （举例：`E:\wsl2\ubuntu2404_backup.tar`）

  ```bash
  wsl --list --online
  wsl --install Ubuntu-24.04
  wsl --export Ubuntu-24.04 <Image Path>
  ```

- 安装到自定义位置 `<Install Path>` （举例：`E:\wsl2\ubuntu2404`）

  ```bash
  wsl --unregister Ubuntu-24.04
  wsl --import Ubuntu2404 <Install Path> <Image Path>
  ```

- 修改默认用户 `<User Name>` （举例：`ricky`）

  ```bash
  wsl --manage Ubuntu2404 --set-default-user <User Name>
  ```

- 启动 WSL2

  ```bash
  wsl -d Ubuntu2404
  ```

- 修改 WSL2 配置

  ```bash
  sudo vi /etc/wsl.conf
  ```

  ```
  [boot]
  systemd=true
  
  [user]
  default=ricky
  
  [interop]
  enabled = true
  appendWindowsPath = false
  ```

  其中：

  - `enabled = true` 是允许从 WSL2 启动 Windows 程序
  - `appendWindowsPath = false` 是不把 Windows 的 PATH 追加进 WSL2 的 `$PATH`

- 重启 WSL2

  ```bash
  wsl --shutdown
  ```

- Ubuntu 更新

  ```bash
  sudo apt update
  sudo apt upgrade
  ```

---

## LLVM

- 使用 LLVM 官方安装脚本（笔者安装的是 *LLVM 20*）

    ```bash
    wget https://apt.llvm.org/llvm.sh -O /tmp/llvm.sh
    chmod +x /tmp/llvm.sh
    sudo /tmp/llvm.sh 20 all
    ```
- 管理和配置系统中的软件版本

    ```bash
    sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-20 100
    sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-20 100
    sudo update-alternatives --install /usr/bin/clangd clangd /usr/bin/clangd-20 100
    sudo update-alternatives --install /usr/bin/clang-tidy clang-tidy /usr/bin/clang-tidy-20 100
    sudo update-alternatives --install /usr/bin/clang-format clang-format /usr/bin/clang-format-20 100
    ```



Ref:
- [LLVM Debian/Ubuntu packages](https://apt.llvm.org/)

---

## CMake

- 导入 key

    ```bash
    test -f /usr/share/doc/kitware-archive-keyring/copyright ||
    wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | gpg --dearmor - | sudo tee /usr/share/keyrings/kitware-archive-keyring.gpg >/dev/null  
    ```

- For Ubuntu Noble Numbat (24.04):

    ```bash
    echo 'deb [signed-by=/usr/share/keyrings/kitware-archive-keyring.gpg] https://apt.kitware.com/ubuntu/ noble main' | sudo tee /etc/apt/sources.list.d/kitware.list >/dev/null
    sudo apt-get update
    ```

- 删除临时 key，用 keyring 管理

    ```bash
    test -f /usr/share/doc/kitware-archive-keyring/copyright ||
    sudo rm /usr/share/keyrings/kitware-archive-keyring.gpg
    sudo apt-get install kitware-archive-keyring
    ```

- 安装 cmake

    ```bash
    sudo apt-get install cmake
    ```



Ref:
- [Kitware APT 仓库 --- Kitware APT Repository](https://apt.kitware.com/)

---

## Ninja

```bash
sudo apt install -y ninja-build
```

---

## VS Code Extensions

- `ms-vscode-remote.remote-wsl` — WSL
-  `llvm-vs-code-extensions.vscode-clangd` — clangd
-  `xaver.clang-format` — Clang-Format
- `usernamehw.errorlens` — Error Lens
-  `KylinIdeTeam.cmake-intellisence` — CMake IntelliSence

---

## Current Environment

```bash
$ clang++ -v
Ubuntu clang version 20.1.8 (++20250804090239+87f0227cb601-1~exp1~20250804210352.139)
Target: x86_64-pc-linux-gnu
Thread model: posix
InstalledDir: /usr/lib/llvm-20/bin
Found candidate GCC installation: /usr/lib/gcc/x86_64-linux-gnu/13
Selected GCC installation: /usr/lib/gcc/x86_64-linux-gnu/13
Candidate multilib: .;@m64
Selected multilib: .;@m64
$ cmake --version
cmake version 4.3.2

CMake suite maintained and supported by Kitware (kitware.com/cmake).
$ ninja --version
1.11.1
```

---