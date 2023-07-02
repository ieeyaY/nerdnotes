# Linux

[TOC]

## User and Group

### User and Group Files

`/etc/passwd`: Account infomation, except password

```
<account>:<password>:<userid>:<groupid>:<discription>:<homedir>:<shell>
root     :x         :0       :0        :             :/root    :/bin/bash
```

`/etc/shadow`: Passwords
`/etc/group`: Group info

```
<group>:<password>:<groupid>:
```

## sudo

Allow sudo

1. add user to group `root`
2. uncomment or add line `%<group> ALL=(ALL:ALL) [NOPASSWD] ALL`
   > Note: line start without `%` indicates a user, e.g. `root ALL=(ALL:ALL) ALL`

## Archlinux install Gnome

安装显卡图形驱动
```bash
# 窗口管理系统
pacman -S xorg
# 桌面
pacman -S gnome gnome-extra gdm
# 字体
pacman -S ttf-hack
```

## Archlinux install Plasma
```bash
# minimal
pacman -S plasma-desktop
# general
pacman -S plasma
    # or
pacman -S plasma-meta
```

## [Arch Build System](https://wiki.archlinuxcn.org/wiki/Arch_%E6%9E%84%E5%BB%BA%E7%B3%BB%E7%BB%9F)

使用 $\textsf{asp}^\textsf{包}$ 通过 Git 获取 PKGBUILD 源码

## Essential Packages

```bash
pacman -S --needed git base-devel
# ArchWSL substitutes fakeroot by fakeroot-tcp
```

## Relative tools

### sed

#### sed command

```bash
sed OPTIONS... [SCRIPT] [INPUTFILE...]
sed OPTIONS... -f [script.sed] [INPUTFILE...]
```

#### sed script

```sed
[addr]X[options][;[addr]X[options][;...]]
```

`[addr]`:

  - regular expressions: `/<regex>/`
  - ranges: `<start>,<end>`

### MinGW

- MinGW
- [Msys2](https://www.msys2.org/)
- [Cygwin](https://www.cygwin.com/)

### Vim

Vim macro:
  - `$VIM` install dir (`C:\Program Files\Vim`, `/usr/share/vim`)
  - `$VIMRUNTIME` runtime dir (`$VIM/vim90`)
    `:set runtimepath+=...` `:set rtp+=`
  - `$HOME`
      
[ vim runtime path ](https://yyq123.github.io/learn-vim/learn-vi-204-vimfiles.html):
| Direction | Describe                                                             |
| ---       | ---                                                                  |
| autoload  | 自动载入脚本（autoload scripts）                                     |
| colors    | 配色方案                                                             |
| compiler  | 编译命令:compiler使用的脚本文件                                      |
| doc       | 文档                                                                 |
| ftplugin  | 针对特定类型文件的插件（需要配合:filetype plugin命令使用）           |
| indent    | 自动缩进定义文件                                                     |
| keymap    | 命名格式为 {language}[-{layout}][_{encoding}].vim 的Keymap文件       |
| lang      | 界面显示语言文件（英文、中文等）                                     |
| macros    | 宏示例（hanoi、maze、urm等），小工具（justify、matchit、swapmous等） |
| plugin    | 插件                                                                 |
| syntax    | 语法高亮度文件                                                       |
| tools     | 工具（unicode、vimspell等）                                          |
| tutor     | 入门教程                                                             |

## Wildcards

For bash and find

1. `*`：匹配零个或多个字符。
   例如，`ls /path/to/directory/*` 将匹配指定目录下的所有文件和子目录。
2. `?`：匹配单个字符。
   例如，`ls /path/to/directory/file?.txt` 将匹配 `file1.txt`、`file2.txt` 等文件。
3. `[]`：匹配指定范围内的字符。
   例如，`ls /path/to/directory/[abc]*` 将匹配以字母 "a"、"b" 或 "c" 开头的文件或目录。
4. `**`：(expanded wildcards)匹配任意级别的目录。
   例如，`ls /path/to/directory/**/*.txt` 将匹配指定目录及其子目录中的所有 `txt` 文件。

## CLI Pipeline

问题出在管道传参或bash脚本中参数常被空格分开

### `xargs`

> (https://www.cnblogs.com/chyingp/p/linux-command-xargs.html)

```
ls *.js | xargs -t -n2 ls -al
```
列出所有js文件传给 `xargs`, 先打印, 再2个为一组执行ls命令
```
find . -name '*.css' -print0 | xargs -0 -t ls -al
```
`find -print0` 让每个输出以 `NULL` 结尾而不是 `\n`, `xargs -0` 以 `NULL` 为分隔符识别

### `read`

> (https://www.cnblogs.com/klb561/p/9245696.html)

`read` 命令读入stdIO, 并赋给shell变量, ( 可用重定向改为从文件等地方读入 )