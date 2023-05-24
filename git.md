# Git

```
#查看所有配置 (--list) 及其所在文件 (--show-origin)
git config --list --show-origin
```

## 常用

```
git init [<directory>]
git clone <repository> <directory>
git clone <repository> [-b <branch>] <directory>
git clone --bare <repo-name> <repo-name>.git     # 导出为裸仓库
git pull                                         # git fetch --all; git merge ?
```

## branches

```
git branch [-av]                                  # 列出
git checkout <branch>
git checkout -b <new-branch>
git checkout -b <new-branch> origin/<branch-name> # 新建分支并与远程连接
git branch -d <branch-to-delete>
git tag <tagname> [<commit> | <object>]           # 在当前或<commit>标记
```

## changes

```
git status
git add <path>
git commit -m "<message>"
git reset [<file>]        # = git reset --mixed HEAD [<file>]
git checkout [commit]
```

|                            | HEAD | Index | Workdir | WD safe |
|             ---            |  --- |  ---  |   ---   |   ---   |
|        Commit Level        |      |       |         |         |
|   `reset --sort [commit]`  |  REF |   NO  |    NO   |    Y    |
|      `reset [commit]`      |  REF |  YES  |    NO   |    Y    |
|   `reset --hard [commit]`  |  REF |  YES  |   YES   |    Y    |
|     `checkout [commit]`    | HEAD |  YES  |   YES   |    N    |
|         File Level         |      |       |         |         |
|   `reset [commit] <path>`  |  NO  |  YES  |    NO   |    Y    |
| `checkout [commit] <path>` |  NO  |  YES  |   YES   |    N    |

## rebase

```
git merge <branch>                               # 合并并前进
git rebase <branch>                              # 取出当前分支移到目标支上
git fetch <alias>                                # 从远程别名上下载 (不合并)
git merge [--no-ff] [--ff-only] <alias>/<branch> # 合并 (不快进/仅快进)
```

## diff

```
git diff <branchA>...<branchB>
git difftool
```

## `git config`

```
git config --global format.pretty=short
```