# Gigabyte-Z790-Aorus-Elite-AX-13700K-OpenCore-Hackintosh

- Motherboard :Gigabyte Z790 Aorus Elite ax DDR5
- CPU : I7 13700K
- GPU : Gigabyte RX6600 EAGLE 8G
- OpenCore : 0.9.0
- MacOS : Ventura 13.3

# 警告！！！

## 目前增量更新时卡进度条，不知道怎么解决。不建议用此EFI进行更新系统。

## 增量更新重启进macos Installers选项，但是进度条不动，进—V看LOG好像没输出。。。

---


# 关于安装

之前是下载完整的MacOS镜像，再使用[etcher](https://github.com/balena-io/etcher)刷入U盘，之后把EFI放入U盘的EFI分区中，这样启动时总是找不到MacOS的选项。

制作U盘启动盘我是用官方建议的方式：[rufus-method](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/windows-install.html#rufus-method)

安装过程中**启动Apple Logo后会有一段较长时间的屏幕熄灭**，我第一次安装的时候有好几分钟的黑屏时间，目前使用有十几秒的黑屏时间，黑屏时间过后才会出现设置界面或登录界面。

# 关于EFI

EFI会长期更新，但目前很很不完善，不是必须还不建议用。

机型改为iMac pro1,1可以提高单核性能

# 关于增量更新

禁用BlueToolFixup.kext 重启再更新即可增量更新

# 关于BIOS

- **Secure Boot : Disabled**

- Internal Graphics : Disabled

- **Above 4G Decoding : Enabled**

- **Above 4GB MMIO BIOS assignment : Enabled**

- Re-Size BAR Support : Disabled

- **Hyper-Threading : Enabled**

- **CFG Lock : Disabled**

![image info](./1.png)

![image info](./2.png)

![image info](./3.png)



---

推荐的软件

- [MonitorControl](https://github.com/MonitorControl/MonitorControl) ：用来调整屏幕亮度。

- [OCAT](https://github.com/ic005k/OCAuxiliaryTools/releases) ：用来修改EFI文件

目前推荐[nakquada](https://github.com/nakquada/Z790-Hackintosh)的EFI，他的EFI好像跑分比较正常。
