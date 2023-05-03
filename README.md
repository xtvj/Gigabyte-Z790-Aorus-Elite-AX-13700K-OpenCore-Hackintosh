# Gigabyte-Z790-Aorus-Elite-AX-13700K-OpenCore-Hackintosh

### 我的硬件

- Motherboard：Gigabyte Z790 Aorus Elite ax DDR5 Ver1.0
- CPU：I7 13700K （对CPU没特别要求，别的CPU只需在config.plist中更改显示名就可以）
- GPU：Gigabyte RX6600 EAGLE 8G (只要是免驱的显卡都应该适用)
- macOS：Ventura 13.3.1（Ventura所有版本都适用，Monterey、Big Sur没测试过）
- OpenCore ： 0.9.1
- Bios：F6a [官方地址](https://www.aorus.com/motherboards/Z790-AORUS-ELITE-AX-rev-10/Support)



# ~~警告！！！~~

 **~~目前增量更新时卡进度条，不知道怎么解决。不建议用此EFI进行更新系统。~~**



# 关于增量更新

禁用BlueToolFixup.kext 再更新即可增量更新

我是把蓝牙相关的三个kext（BlueToolFixup.kext、IntelBluetoothFirmware.kext、IntelBTPatcher.kext）都禁用增量更新成功了。




# 请生成自己的SMBIOS

使用[OCAT](https://github.com/ic005k/OCAuxiliaryTools/releases)随机生成自己的UUID等再使用。



# 关于制作EFI启动盘

按照官方教程[OpenCore-Install-Guide/](https://dortania.github.io/OpenCore-Install-Guide/)操作就行。

大致可分为

<img src="https://xtvj.github.io/images/黑苹果EFI制作流程.svg" alt="黑苹果EFI制作流程" style="zoom:75%;" />

#### [制作ACPI](https://dortania.github.io/Getting-Started-With-ACPI/ssdt-methods/ssdt-easy.html#running-ssdttime)

我是使用[SSDTTime](https://github.com/corpnewt/SSDTTime)工具在Windows下生成的，操作很简单，只是当初看英文文档的时候先看的手动制作，以为很难，其实用工具在Windows下选择几个选项就自动生成了。

#### U盘启动盘

~~之前是下载完整的MacOS镜像，再使用[etcher](https://github.com/balena-io/etcher)刷入U盘，之后把EFI放入U盘的EFI分区中，这样启动时总是找不到MacOS的选项。原因大概是etcher把EFI分区没有标记，用分区工具将放EFI的分区改为引导分区应该就行，自己没有测试过。~~

之前制作U盘启动盘我是用官方建议的方式：[rufus-method](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/windows-install.html#rufus-method)




现在的启动U盘制作过程（macOS系统、参考了：https://post.smzdm.com/p/a785e48l/ )

1. 使用[macadmin-scripts](https://github.com/munki/macadmin-scripts)下载相应的离线安装镜像，下载后会自动换成DMG的文件。

2. 加载DMG镜像文件到系统
3. sudo /Volumes/下载的镜像名/Contents/Resources/createinstallmedia --volume /Volumes/新建的空白镜像名/
4. 再挂载新建的镜像文件，并挂载其EFI文件夹，把EFI复制进去
5. 使用[etcher](https://github.com/balena-io/etcher)写入U盘



或使用[gibMacOS](https://github.com/corpnewt/gibMacOS)下载PKG文件安装到系统，再用[官方的方法](https://support.apple.com/en-us/HT201372)制作U盘也很方便



# 关于安装

安装过程中**启动Apple Logo后会有一段较长时间的屏幕熄灭**，我第一次安装的时候有好几分钟的黑屏时间，目前使用有十几秒的黑屏时间，黑屏时间过后才会出现设置界面或登录界面。



# 关于EFI

EFI会长期更新

机型改为iMac pro1,1可以提高单核性能



# 关于BIOS

并不是非要按我的设置来做，你能启动并成功安装使用的话就不用动它了。

- **Secure Boot : Disabled**

- **Internal Graphics : Disabled**

- Above 4G Decoding : Enabled

- Above 4GB MMIO BIOS assignment : Enabled

- Re-Size BAR Support : Disabled

- **Intel Platform Trust Technology(PTT): Disabled**

- **Hyper-Threading : Enabled**

- **CFG Lock : Disabled**

![image info](./img/IMG_0390.avif)

![image info](./img/IMG_0391.avif)

![image info](./img/IMG_0392.avif)

![image info](./img/IMG_0393.avif)

![image info](./img/IMG_0394.avif)

![image info](./img/IMG_0395.avif)

![image info](./img/IMG_0396.avif)

![image info](./img/IMG_0397.avif)



# 关于功能

- 能正常开机使用
- 能登录AppStore下载软件
- 睡眠未测试，我都是直接关机后断电
- iCloud、Message等未测试，这些功能我没用到。



# 推荐的软件

- [MonitorControl](https://github.com/MonitorControl/MonitorControl) ：用来调整屏幕亮度。

- [OCAT](https://github.com/ic005k/OCAuxiliaryTools/releases) ：用来修改EFI文件

- [Stats](https://github.com/exelban/stats)：状态栏的系统监测工具



# EFI文件分享

[Gigabyte-Z790-Aorus-Elite-AX-13700K-OpenCore-Hackintosh](https://github.com/xtvj/Gigabyte-Z790-Aorus-Elite-AX-13700K-OpenCore-Hackintosh)



# 更新记录

2023.05.03 ：

1. 添加CleanNvram工具，并在启动时显示系统外的工具类选项，如需隐藏可**勾选**Misc→Boot→HideAuxiliary
2. 更新自己的Bios为F6a，并更新Bios设置截图

