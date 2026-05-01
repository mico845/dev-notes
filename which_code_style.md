# which_code_style

**Which code style?**

---

## Skills

使用 `code-style-cpp-guide` 作为 C++ Code Style 的参考 SKILL

关于 Code Style 的内容我做成了网页 [Code Style Guide](https://mico845.github.io/code-style-cpp-guide/) 👈

- clone 到本地并设置 gitignore

  ```bash
  git clone https://github.com/mico845/code-style-cpp-guide skills/code-style-cpp-guide
  echo skills/code-style-cpp-guide/ >> .gitignore
  ```


- 以 git submodule 方式添加到项目

  ```bash
  git submodule add https://github.com/mico845/code-style-cpp-guide skills/code-style-cpp-guide
  ```

---

## clang-format

```yaml
# .clang-format
# Ubuntu clang-format version 20.1.8
# Clang-Format Style Options: https://clang.llvm.org/docs/ClangFormatStyleOptions.html
---
BasedOnStyle: Google 

Standard: Latest 

ColumnLimit: 120

AllowShortIfStatementsOnASingleLine: Never
```

含义：

- clang-format 基于 Google 风格

  ```yaml
  BasedOnStyle: Google 
  ```

- 语言标准设置为最新

  ```yaml
  Standard: Latest 
  ```

- 行的限制设置为 `120`
  
  ```yaml
  ColumnLimit: 120
  ```
  
  设置为 `0` 意味着不设限制
  
- 通过不同的值判断 `if (a) return;` 是否可以放在单行上

  ```yaml
  AllowShortIfStatementsOnASingleLine: Never
  ```

  `Never` 从不把短 if 放在同一行上
---

## clang-tidy

```yaml
# .clang-tidy
# Ubuntu LLVM version 20.1.8
# Clang-Tidy Checks: https://clang.llvm.org/extra/clang-tidy/checks/list.html
---
Checks: >
  -*,
  clang-analyzer-*,
  bugprone-*,
  modernize-*,
  performance-*,
  portability-*,
  misc-*,
  readability-*,
  cppcoreguidelines-*,
  google-*,
  -google-readability-braces-around-statements,
  -readability-braces-around-statements,
  -modernize-use-trailing-return-type,
  -readability-identifier-length
```

含义：

- 先关闭所有检查

  ```yaml
  -*
  ```

- 常见选项：

  | Name prefix          | Description                                      |
  | :------------------- | :----------------------------------------------- |
  | `abseil-`            | 与 Abseil 库相关的检查                           |
  | `altera-`            | 与 FPGA 的 OpenCL 编程相关的检查                 |
  | `android-`           | 与 Android 相关的检查                            |
  | `boost-`             | 与 Boost 库相关的检查                            |
  | `bugprone-`          | 针对易出 BUG 的代码结构的检查                    |
  | `cert-`              | 与 CERT 安全编码指南相关的检查                   |
  | `clang-analyzer-`    | Clang 静态分析器检查                             |
  | `concurrency-`       | 与并发编程相关的检查，包括线程、纤程、协程等     |
  | `cppcoreguidelines-` | 与 C++ 核心指南相关的检查                        |
  | `darwin-`            | 与 Darwin 编码约定相关的检查                     |
  | `fuchsia-`           | 与 Fuchsia 编码约定相关的检查                    |
  | `google-`            | 与 Google 编码约定相关的检查                     |
  | `hicpp-`             | 与高完整性 C++ 编码标准相关的检查                |
  | `linuxkernel-`       | 与 Linux 内核编码约定相关的检查                  |
  | `llvm-`              | 与 LLVM 编码约定相关的检查                       |
  | `llvmlibc-`          | 与 LLVM-libc 编码标准相关的检查                  |
  | `misc-`              | 无法归入更合适类别的检查                         |
  | `modernize-`         | 提倡使用现代语言结构的检查；当前“现代”指 C++11   |
  | `mpi-`               | 与 MPI（消息传递接口）相关的检查                 |
  | `objc-`              | 与 Objective-C 编码约定相关的检查                |
  | `openmp-`            | 与 OpenMP API 相关的检查                         |
  | `performance-`       | 针对性能相关问题的检查                           |
  | `portability-`       | 针对可移植性相关问题的检查，且不涉及特定编码风格 |
  | `readability-`       | 针对可读性相关问题的检查，且不涉及特定编码风格   |
  | `zircon-`            | 与 Zircon 内核编码约定相关的检查                 |

---

## clangd 

使用本地的 clangd 
搭配 VS Code 的 LLVM 官方插件 `clangd`

关于 clangd 的参数配置：
```json
{
    "clangd.arguments": [
        "--compile-commands-dir=${workspaceFolder}",
        "--query-driver=clang,clang++",
        
        "--clang-tidy",
        "--background-index",
        "--completion-style=detailed",
        "--header-insertion=iwyu",
        "--function-arg-placeholders=false",
        "--log=error",        
    ]
}
```


---

## Ref
- [Google Code Style](https://github.com/google/styleguide)
- [Google 开源项目风格指南——中文版¶](https://zh-google-styleguide.readthedocs.io/en/latest/index.html)
- [Clang-Format Style Options](https://clang.llvm.org/docs/ClangFormatStyleOptions.html)
- [Clang-Tidy Checks](https://clang.llvm.org/extra/clang-tidy/checks/list.html)

---