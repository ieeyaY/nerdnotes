# Linux

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