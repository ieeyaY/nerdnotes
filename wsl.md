# WSL notes

## About Various Distribute

### Arch WSL

[ArchWSL](https://github.com/yuk7/ArchWSL.git)
[ArchWSL Doc](https://wsldl-pg.github.io/ArchW-docs/)

> Note: For appx install
> Install cer file to Local Machine>Trusted People
> Then install appx file
> [Initialize keyring](https://wsldl-pg.github.io/ArchW-docs/How-to-Setup/#initialize-keyring) for the pacman.

> Note: Update
> Download and install zip or installer to overwrite existing one.

install desktop first then gvim, etc.
```
man-db man-page base-devel plasma-desktop gvim neofetch ctags 
git perl-rename bash-completion openssh tree cmake python-pip pyright python-debugpy python-virtualenv autopep8 flake8(vim-syntastic) zip unzip
python-json5 (fortls dep)
vim-language-server fortls cmake-language-server(aur)
man-page-zh_cn adobe-source-han-serif-cn-fonts expac (optional) 
```

### wsl2 rime

#### ibus-rime

```
pacman -S ibus-rime rime-wubi
yay -S ibus-qt # 可选
```

bashrc加入
```
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus
ibus-daemon -d -x
```

#### fcitx5-rime

```
pacman -S fcitx5-im fcitx-rime rime-wubi
yay -S fcitx5-input-support
```

不要用shift切换中英, linux下输入法切换, 候选词切换等按键由fcitx和ibus等控制, 方案切换最好用F4, 加入control+F4等可能被拦截[TODO]

## About WSLg

### WSLg configuration

[wslconfig](https://github.com/microsoft/wslg/wiki/WSLg-Configuration-Options-for-Debugging)

> [翻译](./wslconfig-tran.md)

### others

显示器: `export DISPLAY=[ip]:0`

## Hyper-V

[Enable Hyper-V](https://github.com/littletaoishere/WindowsHomeHyperV.git)

### Hyper-V winnat 占用v2ray端口

> 重启一下winnat即可恢复。 
> ```
> > net stop winnat Windows NAT Driver
> 服务已成功停止
> > net start winnat Windows NAT Driver
> 服务已经启动成功
> ```

参考: [解决V2rayN测速时提示运行Core失败，请看日志的问题 - 邮莓生活](https://mailberry.com.cn/2023/08/solve-v2rayn-core-fail-issues/)

## Optimize Disk

To compress disk and reclaim disk space
```powershell
Optimize-VHD -Path "C:\path\to\your.vhdx" -Mode Full
```
vhdx path:
`%LOCALAPPDATA%\Packages\<wslpackage>\LocalState\<distro>.vhdx`