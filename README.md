# Gigabyte-Z790-Aorus-Elite-AX-13700K-OpenCore-Hackintosh

### 非常抱歉，停更了

非常抱歉，我离开了我的国家，并在离开前砸毁了我的所有硬件设备，来到了一个自由的国度后也不可能购买相同的硬件了，刚才看到还有人在fork这个仓库,就想说一声我不再更新了，实在抱歉。请选择其他人的或自行修改更新内容。抱歉，抱歉，抱歉。


### 我的软、硬件

- Motherboard：Gigabyte Z790 Aorus Elite ax DDR5 Ver1.0
- CPU：I7 13700K （对CPU没特别要求，别的CPU只需在config.plist中更改显示名就可以）
- GPU：Gigabyte RX6600 EAGLE 8G (只要是免驱的显卡都应该适用)
- macOS：Sequoia 15.0 （理论上Sonoma、Ventura所有版本都适用，Monterey、Big Sur没测试过）
- OpenCore ： 1.0.0
- Bios：F10 [官方地址](https://www.aorus.com/motherboards/Z790-AORUS-ELITE-AX-rev-10/Support)



# 警告！！！

**更新BIOS后，BIOS配置可能被重置，需要重新设置。**

**更新BIOS之后重启第一次进系统时有时候可能需要执行一次ResetNram，不然有时候进不去系统，原因未知，也不知道这操作起没起作用。**



# 关于增量更新

禁用BlueToolFixup.kext 再更新即可增量更新

我是把蓝牙相关的三个kext（BlueToolFixup.kext、IntelBluetoothFirmware.kext、IntelBTPatcher.kext）都禁用增量更新成功了。



# 请生成自己的SMBIOS

使用[OCAT](https://github.com/ic005k/OCAuxiliaryTools/releases)随机生成自己的UUID等再使用。

生成的SystemSerialNumber可以检查一下能否在官网查的到，如果提示不正常则是可用的，如果查到有保修期之类的信息，说明这个号码是苹果官方售卖的硬件使用的ID，不要用，使用后有封号风险。

一般随机生成的很大概率是查不到信息，可以使用的。



# 关于制作EFI启动盘

#### 1. [制作ACPI](https://dortania.github.io/Getting-Started-With-ACPI/ssdt-methods/ssdt-easy.html#running-ssdttime)

此操作不是必需，可直接使用我生成的ACPI

我是使用[SSDTTime](https://github.com/corpnewt/SSDTTime)工具在Windows下生成的，操作很简单，只是当初看英文文档的时候先看的手动制作，以为很难，其实用工具在Windows下选择几个选项就自动生成了。



#### 2. 定制自己机箱的USB驱动

此操作很有必要

使用[USBToolBox](https://github.com/USBToolBox/tool/releases)在Windows下制作驱动，替换EFI里的UTBMap.kext就可以。

如果不定制也可以使用主板上的USB接口，只是机箱上的可能识别不到。

而且我自己定制的USB驱动可能不太完善，接口速度不高。



#### 3. U盘启动盘

~~之前是下载完整的MacOS镜像，再使用[etcher](https://github.com/balena-io/etcher)刷入U盘，之后把EFI放入U盘的EFI分区中，这样启动时总是找不到MacOS的选项。原因大概是etcher把EFI分区没有标记，用分区工具将放EFI的分区改为引导分区应该就行，自己没有测试过。~~

之前制作U盘启动盘我是用官方建议的方式：[rufus-method](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/windows-install.html#rufus-method)




现在的启动U盘制作过程（macOS系统、参考了：https://post.smzdm.com/p/a785e48l/ )

1. 使用[macadmin-scripts](https://github.com/munki/macadmin-scripts)下载相应的离线安装镜像，下载后会自动换成DMG的文件。

   [scheblein/macadmin-scripts](https://github.com/scheblein/macadmin-scripts)分支修复了macos13上使用问题

2. 加载DMG镜像文件到系统

3. sudo /Volumes/下载的镜像名/Contents/Resources/createinstallmedia --volume /Volumes/新建的空白镜像名/

4. 再挂载新建的镜像文件，并挂载其EFI文件夹，把EFI复制进去

5. 使用[etcher](https://github.com/balena-io/etcher)写入U盘



或使用[gibMacOS](https://github.com/corpnewt/gibMacOS)下载PKG文件安装到系统，再用[官方的方法](https://support.apple.com/en-us/HT201372)制作U盘也很方便

#### 4. WiFi驱动

根据网友的测试使用[itlwm](https://github.com/OpenIntelWireless/itlwm/releases)+[HeliPort](https://github.com/OpenIntelWireless/HeliPort)的方式可以驱动，

使用[AirportItlwm](https://github.com/OpenIntelWireless/itlwm/releases)的方式可能驱动不成功。




# 关于安装

RX6600/XT显卡在安装过程中**启动Apple Logo后会有一段较长时间的屏幕熄灭**，我第一次安装的时候有好几分钟的黑屏时间，目前每次启动都会有十几秒的黑屏时间，黑屏时间过后才会出现设置界面或登录界面。其它免驱显卡可能没有这个问题。



# 关于EFI

EFI会长期更新

~~机型改为iMac pro1,1可以提高单核性能~~



# 关于BIOS

并不是非要按我的设置来做，你能启动并成功安装使用的话就不用动它了。

- **Secure Boot : Disabled**
- **Internal Graphics : Enabled**
- Above 4G Decoding : Enabled
- Above 4GB MMIO BIOS assignment : Enabled
- **Re-Size BAR Support : Enabled**
- **Aperture Size : 1024MB**
- **Intel Platform Trust Technology(PTT): Disabled**
- **CFG Lock : Disabled**



![image info](./img/1.avif)



![image info](./img/2.avif)



# 关于功能

- 能正常开机使用
- 能登录AppStore下载软件
- 睡眠已正常，感谢 **[mingweiarthurli](https://github.com/mingweiarthurli)** 和 **[jas0nxu](https://github.com/jas0nxu)**
- iCloud、Message等未测试，可能是正常的。这些功能我没用到。
- 安装系统后，推荐使用ResetNram清一下



# 关于跑分

R23跑分与Windows下的跑分几乎相同

如果你使用单条内存、或散热系统不行，Geekbench的跑分可能会低于预期



# 推荐的软件

- [MonitorControl](https://github.com/MonitorControl/MonitorControl) ：用来调整屏幕亮度。

- [OCAT](https://github.com/ic005k/OCAuxiliaryTools/releases) ：用来修改EFI文件

- [Stats](https://github.com/exelban/stats)：状态栏的系统监测工具



# EFI文件分享

[Gigabyte-Z790-Aorus-Elite-AX-13700K-OpenCore-Hackintosh](https://github.com/xtvj/Gigabyte-Z790-Aorus-Elite-AX-13700K-OpenCore-Hackintosh)



# 更新记录

- 2024.06.26

1. 重新添加CPUFriend等三个驱动。
2. 如果长时间未更新，可自行使用[OCAT](https://github.com/ic005k/OCAuxiliaryTools/releases)工具升级。

- 2024.06.24

1. 更新蓝牙驱动以适配macOS15
2. 更新其它驱动

- 2024.05.26

1. 更新OpenCore为1.0.0
2. 由于Bios更新后生成的ACPI文件有一点点区别（实例上代码里就两三处的判断条件改了一下），就更新了ACPI文件。
3. 目前我使用macOS和Windwos双系统，之前启动到macOS阶段偶尔会随机重启，现在不会了，不知道是更新了什么才修复的。
4. 此EFI更新不那么频繁了，有玩机高手的网友开个仓库分享下自己的EFI呗。

- 2024.03.10

1. 更新Bios为F10，Bios打开Re-Size BAR，Aperture Size 为1024MB
2. 打开OpenCore中的disableIoMapper和disableIoMapperMapping参数
3. 引导参数中添加-wegnoigpu
4. 参考[#4](https://github.com/xtvj/Gigabyte-Z790-Aorus-Elite-AX-13700K-OpenCore-Hackintosh/issues/4)

- 2024.02.21

1. 更新OpenCore 0.9.8
2. OC_ATTR_USE_GENERIC_LABEL_IMAGE[改为不勾选](https://bbs.pcbeta.com/forum.php?mod=redirect&goto=findpost&ptid=1993971&pid=54954198)、securebootmodel设置为禁用

- 2023.12.24

1. 修复增量更新14.2.1无法安装的问题（更新驱动为开发版最新的驱动，安装最新增量更新时不报错了。）
2. 修复14.2.1下蓝牙不能启用的问题（更新蓝牙驱动为开发版本。）
3. 如果更新OpenCore后启动不正常，或蓝牙未正常开启，可以启动时执行一次ResetNram

- 2023.12.16

1. 更新OpenCore 0.9.7
2. 添加启动参数`revpatch=auto,sbvmm,asset`以修复检测不到更新的BUG，可能下载增量更新后安装失败，可以重启后执行一次ResetNram，之后就可以正常增量更新了。
3. 以后只对EFI进行MacOS Sonoma的兼容性测试。

- 2023.09.13

1. 更新OpenCore 0.9.5

- 2023.08.08

1. 更新OpenCore 0.9.4

- 2023.07.29

1. 默认禁用CPUFriend驱动：原因是[每次升级系统可能要重新生成](https://github.com/stevezhengshiqi/one-key-cpufriend/blob/main/README_CN.md#:~:text=%E6%B3%A8%E6%84%8F%EF%BC%9A%E5%8D%87%E7%BA%A7%20macOS%20%E7%89%88%E6%9C%AC%E5%89%8D%E5%BB%BA%E8%AE%AE%E5%81%9C%E7%94%A8%20CPUFriend.kext%20%E5%92%8C%20CPUFriendDataProvider.kext%E3%80%82%E6%AF%8F%E6%AC%A1%E5%8D%87%E7%BA%A7%20macOS%20%E7%89%88%E6%9C%AC%E5%90%8E%EF%BC%8C%E4%BD%A0%E9%9C%80%E8%A6%81%E9%87%8D%E6%96%B0%E7%94%9F%E6%88%90%20CPUFriendDataProvider.kext%EF%BC%8C%E5%90%A6%E5%88%99%E7%94%B5%E6%BA%90%E7%AE%A1%E7%90%86%E4%BC%9A%E4%B8%8D%E6%AD%A3%E5%B8%B8%E6%88%96%E8%80%85%E5%AF%BC%E8%87%B4%E5%86%85%E6%A0%B8%E5%B4%A9%E6%BA%83%E3%80%82)CPUFriendDataProvider，我自己还不确定。

- 2023.07.29

1. 添加CPUFriend和CPUFriendDataProvider驱动，在MacPro机型下单核性能也正常
2. 其实不加这两个驱动CPU睿频也能正常，我的13700K也能达到5.4GHz，想要更高就只能通过更改Bios里的设置。

- 2023.07.12

1. 更新[BlueToolFixup.kext](https://github.com/acidanthera/BrcmPatchRAM/actions/runs/5283322833)文件到2.6.8版本以修复MacOS13.5beta中蓝牙能扫描到但不能连接的问题

- 2023.06.13

1. 更新OpenCore 0.9.3

- 2023.06.12

1. 更改UIScale值为1，以修复开机时随机的不显示或启动不起来的问题。参考远景一贴子，说是可以设置为-1或1
2. 目前EFI算是稳定了，暂时没有发现BUG，如有欢迎提Issues，虽说不一定能解决，但一起讨论还有可能帮到我自己呢。

- 2023.06.10

1. 升级部分kext，删除三个无用的ACPI文件
2. 未修复任何BUG，只是更新了点驱动

- 2023.06.05

1. 在13.4以上的系统下，蓝牙不能用，可以通过在NVRAM的7C436110-AB2A-4BBB-A880-FE41995C9F82下添加两个参数来修复

   ```
   bluetoothExternalDongleFailed Data 00
   
   bluetoothInternalControllerInfo Data 0000000000000000000000000000
   ```

- 2023.06.01

1. 添加[AirportItlwm.kext](https://github.com/OpenIntelWireless/itlwm)驱动，现在WiFi可以正常使用了。

- 2023.05.20

1. 禁用EnableVectorAcceleration，以修复显卡为Rx6600或Rx6600XT时，开机过程中的随机重启问题，参考地址：https://bbs.pcbeta.com/viewthread-1967636-1-2.html 。我已经开机二十来次，除第一次重启外都没重启。

- 2023.05.09

1. 更新到OpenCore0.9.2
2. 禁用了WiFi驱动，本来启用时WiFi也不能用。
3. 添加提示USB驱动制作

- 2023.05.03 ：

1. 添加ResetNram工具，并在启动时显示系统外的工具类选项，如需隐藏可**勾选**Misc→Boot→HideAuxiliary
2. 更新自己的Bios为F6a，并更新Bios设置截图

