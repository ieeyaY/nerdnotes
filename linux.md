# Linux

[TOC]

## device info

`lscpu`
`lspci`
`lshw`
`lsscsi`
`lsusb`
`lnxi`
`df`
`free`
`dmidecode`
`hdparm`
[ref](https://linux.cn/article-6928-1.html)

## benchmark 性能测试
`unixbench` 等
[几款优秀的Linux基准测试工具](https://www.cnblogs.com/sophiascpn/p/13796683.html)

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

## tty Fonts

`setfont` 命令, 或
`/etc/vconsole.conf` 配置文件, 支持`/usr/share/kbd/consolefonts`中的字体
```conf
KEYMAP=us
FONT=ter-????
XKBLAYOUT=us
XKBMODEL=pc105+inet
XKBOPTIONS=terminate:ctrl_alt_kbsp
```

## Xorg

Xorg.conf格式
BusID(`0:2:0`) --> Device(`Card0`) --> Screen, Monitor, ...

### tigervnc

1. vncpasswd
```bash
vncpasswd $XDG_CONFIG_HOME/tigervnc/passwd
chmod 600 $XDG_CONFIG_HOME/tigervnc/passwd
```
2. edit `/etc/tigervnc/vncserver.users`
3. `$XDG_CONFIG_HOME/tigervnc/config`
4. 启动:
   - 无头: `systemctl start vncserver@:N`
   - 转发本地: `/etc/X11/xorg.conf.d/10-vnc.conf`
5. vncviewer: 
   - 无头 vncviewer host:N
   - 转发本地 vncviewer host:0 (本地$DISPLAY)
> [任何操作都正常，就是vnc的远程窗口画面不更新](https://forum.ubuntu.com.cn/viewtopic.php?t=219256):
>   把桌面 效果 选成无就行了 也就是要 不要选扩展模式 不能开3D桌面。


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
> Wayland 无法进入桌面而 X11 没问题; 显示器接到核显上则二者都没问题
> 检查GPU型号和架构: [AMD驱动](https://wiki.archlinux.org/title/Xorg#AMD) 和 [NVIDIA驱动](https://wiki.archlinux.org/title/Xorg#Driver_installation)

## Archlinux install remote desktop

```
yay -S sunloginclient
```
aur构建过程中如果失败注意查看其信赖失败的解决方案.<br/>向日葵依赖 `gconf`^aur^, 其在构建时缺少 `glib2-devel` 依赖而报错
被控和控制都要 `start runsunloginclien.service` 才能运行
同时, 向日葵目前不支持 `gdm`, `sddm` 等显示管理以及 wayland

## [Arch Build System](https://wiki.archlinuxcn.org/wiki/Arch_%E6%9E%84%E5%BB%BA%E7%B3%BB%E7%BB%9F)

使用 $\textsf{asp}^\textsf{包}$ 通过 Git 获取 PKGBUILD 源码

## Essential Packages

```bash
pacman -S --needed git base-devel
# ArchWSL substitutes fakeroot by fakeroot-tcp
yay -S mkinitcpio-firmware
```

## Useful tools

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

#### Vimspector

C/C++调试使用vscode-cpptools
- 使用watches debug:
   - <pvar>, <prtlen>
   - <pvar>[0]@<prtlen>
   - *<pvar>@<prtlen>
- 使用Console debug:
   - <pvar>[0]@<prtlen>
   - *<pvar>@<prtlen>

### 7-Zip

#### Switches
-m\<Parameters\>
| Parameter            | Default  | Description                                               |
|----------------------|----------|-----------------------------------------------------------|
| x=[0 \| 1 \| 3 \| 5 \| 7 \| 9 ] | 5        | Sets level of compression.                                |
| m={MethodID}         | Deflate  | Sets a method: Copy, Deflate, Deflate64, BZip2, LZMA, PPMd.|
| fb={NumFastBytes}    | 32       | Sets number of Fast Bytes for Deflate encoder.            |
| pass={NumPasses}     | 1        | Sets number of Passes for Deflate encoder.                |
| d={Size}[b\|k\|m]    | 900000   | Sets Dictionary size for BZip2                            |
| mem={Size}[b\|k\|m]  | 24       | Sets size of used memory for PPMd.                        |
| o={Size}             | 8        | Sets model order for PPMd.                                |
| mt=[off \| on \| {N}]| on       | Sets multithreading mode.                                 |
| em={EncryptionMethodID} | ZipCrypto | Sets a encryption method: ZipCrypto, AES128, AES192, AES256 |
| cl=[off \| on]       | off      | 7-Zip always uses local code page for file names.         |
| cu=[off \| on]       | off      | 7-Zip uses UTF-8 for file names that contain non-ASCII symbols.|
| cp={CodePage}        | off      | Sets code page                                            |
| tm=[off \| on]       | on       | Stores last Modified timestamps for files.                |
| tc=[off \| on]       | off      | Stores Creation timestamps for files.                     |
| ta=[off \| on]       | off      | Stores last Access timestamps for files.                  |
| tp={N}               | 0        | Sets timestamp precision: 0 - Windows (100 ns), 1 - Unix (1 sec), 2 - DOS (2 sec). 3 - Windows (100 ns). |

指定GBK:
```
7z x <archievement> -mcp=936
```
#### 匹量解压

```bash
find -name "expr" -exec unzip -j {} "**/*.tif" -d outdir
```
`-j` 直接输出文件
文件内成员通配符加`""`

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

默认将标准输入按\s拆分成多个参数
`xargs -n max-args` 1 次命令最多传递的参数个数, 超过则执行多次
`xargs -L max-lines` 1 次命令最多传递的参数行数, 超过则执行多次
`xargs -d delim` 以 delim 为分隔符 (会使 \s 识别为参数)
    可以以NULL为分隔符`find . -print0 | xargs -0`
`xargs -p` (prompt)提示命令, 并确认 `xargs -t` (type)提示命令, 不确认
`xargs -r` 空参数则不执行命令
`xargs -I {} <command> {} <args>` 占位符
标准输入中有\则xargs不识别, 用"\" '\'

#### 一些用法
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

## 指定大小生成文件 - `dd`

## apt
添加32位库
```
dpkg --add-architecture i386
```