# how_to_use_git

How to use git?

---

## Git Version

```
git version 2.43.0
```

---

## Remote 

- 查看当前远程仓库列表：

    ```bash
    git remote -v
    ```

- 重命名远程仓库

    `<old name>` 一般为 `origin`；

    `<new name>` 一般为 `github` / `gitee` 等；

    ```bash
    git remote rename <old name> <new name>
    ```

- 添加远程仓库

    ```bash
    git remote add <name> <URL>
    ```

- 示例：

    ```bash
    $ git remote -v
    origin  https://github.com/mico845/puzzle15.git (fetch)
    origin  https://github.com/mico845/puzzle15.git (push)
    $ git remote rename origin github
    $ git remote add gitee https://gitee.com/kemi741213/puzzle15.git
    $ git remote -v
    gitee   https://gitee.com/kemi741213/puzzle15.git (fetch)
    gitee   https://gitee.com/kemi741213/puzzle15.git (push)
    github  https://github.com/mico845/puzzle15.git (fetch)
    github  https://github.com/mico845/puzzle15.git (push)
    ```

    - 推送到指定远程仓库

        ```bash
        git push github main
        ```

        ```bash
        git push gitee main
        ```

--- 

## 3rd Party

使用 `git submodule` 管理第三方库

第三方库通常不建议直接在当前项目中修改，只在主仓库中记录其固定版本


- 添加 submodule

    ```bash
    git submodule add <URL> <submodule path>
    ```

- 示例： GoogleTest

    ```bash
    mkdir -p extern
    git submodule add https://github.com/google/googletest.git extern/googletest
    ```

---

## 个人 submodule

使用 git submodule 管理个人的其他仓库

与第三方库的区别：

第三方库会固定某个版本，不建议修改；

个人 submodule 可能会在其他电脑或其他项目中更新


- 添加 submodule

    ```bash
    git submodule add <URL> <submodule path>
    ```

- 指定 submodule 跟随分支

    ```bash
    git config -f .gitmodules submodule.<submodule path>.branch <branch>
    ```

- 同步 submodule 配置（把 `.gitmodules` 里的配置同步到本地 `.git/config`）

    ```bash
    git submodule sync -- <submodule path>
    ```

- 更新 submodule

    ```bash
    git submodule update --remote <submodule path>
    ```

- 示例：添加一个 `code-style-cpp-guide` SKILL

    ```bash
    git submodule add https://github.com/mico845/code-style-cpp-guide skills/code-style-cpp-guide
    git config -f .gitmodules submodule.skills/code-style-cpp-guide.branch main
    git submodule sync -- skills/code-style-cpp-guide
    git submodule update --remote skills/code-style-cpp-guide
    ```

---