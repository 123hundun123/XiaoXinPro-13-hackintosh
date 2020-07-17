## XiaoXinPro-13-hackintosh EFI Changelog

- # 0717-2020: Clover + OC
  - ### CLOVER_7-17-2020小兵自用版，支持BS.zip(@daliansky):
    - 更新`DVMT补丁`至`10.15.6`等

  - ### EFI-OC06-PRO13(@宪武):
    - 更新 `SMC*.kext` 感应器驱动支持 11 (`Big Sur`)
    - 更新 `RTCMemoryFixup.kext`

  - ###  附加 `EFI-OC06-PRO13`更新：
    - AX200
    - DW1820A
    - i7或部分i5 (内置DVMT补丁支持到15.6+仿冒CPUID+DW1820A+声卡id11)

- # 0713-2020-OC:

  - `OC` 和 `BOOT` 这两个文件夹 来自 `宪武`发群里的 `EFI-OC06-PRO13for11.zip`

  - `AX200` 文件夹：集成 AX200 网卡驱动，包括 Wi-Fi和 蓝牙 驱动，手动开启【`以太网`】才行使用；

  - `DW1820A` 文件夹：基成 DW1820A 网卡驱动，具体细节看文件夹里面的说明

  - ### EFI-OC06-PRO13for11.zip(`@宪武`):
    - 支持 [Big Sur(11) 安装](https://blog.daliansky.net/WeChat-First-macOS-Big-Sur-Beta-2-Installer-for-OpenCore-and-PE-dual-EFI-partition-original-image.html)
    - `SMCBatteryManager.kext`现在无法驱动 `MAC11`，暂时改为 `ACPIBatteryManager.kext`
    - `SSDT-OCPublic-Merge.aml`去掉了`RTC部分`，而小新PRO仍然用`SSDT-RTC_Y-AWAC_N.aml`为`RTC`打补丁(`RTC很特殊，依赖于机器本身，可能不同的机器RTC形式不同`)

    - 强烈建议把11安装到新分区
    - 老的MAC系统下载APP，安装时选择新分区，安装过程重启4-5次
    - 先用磁盘工具给MAC11分区，然后安装下载的APP，安装过程提示安装位置，选择刚才的MAC11

    -  ### BIOS 设置：EFI-OC-PRO13使用说明.pdf

- # 06-03-2020-Clover

  - 添加 引导参数: `rtcfx_exclude=80-AB,B0-B4`, 以及其驱动 `RTCMemoryFixup.kext` 详情看[CMOS相关](https://github.com/daliansky/OC-little/tree/master/15-CMOS%E7%9B%B8%E5%85%B3)
  - 删除 `SSDT-XSPI.aml`
  - 删除 `NVMeFix.kext`
  - 删除 `VoodooInput.kext`
  - 更新 `kexts` 到最新版本
  - 更新 `DVMT` 补丁匹配系统说明 for (@daliansky)
  - ## 注意
  - 以上部分同步 `OC`  for (@宪武)，但保留 `DVMT`补丁 和 `DW1820A` 网卡相关驱动

 - # 06-02-2020-OC(`@宪武`):
    - 添加 `boot-args`: `rtcfx_exclude=80-AB,B0-B4`, 以及对应的驱动 `RTCMemoryFixup.kext`
    - 屏蔽仿冒 `Emulate`，即屏蔽 `Cpuid1Data`、`Cpuid1Mask`
    - 删除 `SSDT-XSPI.aml`
    - 删除 `NVMeFix.kext`
    - 删除 `DVMT` 补丁: 1. `Kernel -> Patch` 的两个 `DVMT` 补丁, 2. `DeviceProperties` 下的 `framebuffer-fbmem`、`framebuffer-stolenmem`
    - 删除 `DW1820A` 相关驱动：`AirportBrcmFixup.kext、BrcmBluetoothInjector.kext、BrcmFirmwareData.kext、BrcmPatchRAM3.kext`
    - 更新：`OC 0.5.9`， `kexts` 日常更新(`PS：触摸板驱动自行更新`) 

    - ### 注意：
    - 1.因删除了 `DVMT` 相关补丁，可能需要 `CLCN32WW.DPC10.rar` 或使用 `解锁DVMT工具` 解除`DVMT`限制，刷`BIOS`有风险，后果自负
    - 2.`i7或部分i5机型`需要去除屏蔽仿冒 `Emulate`，即 `Cpuid1Data`、`Cpuid1Mask`

    - 更多细节请看 《EFI-OC-PRO13使用说明.pdf》或 《[OC-little](https://github.com/daliansky/OC-little)》

 - # 05-04-2020: 
   ### OC(`@宪武`)
    - `SSDT-OCPublic-Merge.aml` 合并 `SSDT-EC.aml`、`SSDT-RTC0.aml`、`SSDT-USBX.aml`、`SSDT-ALS0.aml`、`SSDT-MCHC.aml`
    - `AllowNvramReset` 设置 `true`，允许 `reset Nvram`
    - 外置引用 `VoodooInput` 改为内置 `VoodooI2C.kext/Contents/PlugIns/VoodooInput.kext`
    - 添加 `NVMeFix.kext`
    - 日常更新 `kexts`
    - 更新 [OC releases v0.5.8](https://github.com/acidanthera/OpenCorePkg/releases/tag/0.5.8)

   ### MOD OC(`基于OC`)
    - 去除 `-v`
    - 禁用`Entries`, 改为通用设置，双系统引导(引导Windows)：`\EFI\Microsoft\Boot\bootmgfw.efi`
    - 此版本比原版多了 `ACPI-> Quirks-> EnableForAll,Booter-> Quirks-> EnableForAll,Misc->boot->SkipCustomEntryCheck` 三个选项
    - 安装系统或进Recovery模式可以选：`config-安装系统或进Recovery模式.plist`
    - 更新 [OC releases N-d-k-0.5.8](https://github.com/n-d-k/OpenCorePkg/releases/tag/N-d-k-0.5.8)
    - 更多请看： [n-d-k / OpenCorePkg](https://github.com/n-d-k/OpenCorePkg) 或 [教程](http://bbs.pcbeta.com/viewthread-1838814-1-1.html)

   ### CLOVER(`移植OC更新`)
    - 去除 `-v`
    - 日常更新 `kexts`
    - 添加 `NVMeFix.kext`
    - 设置机型为 `MacBookAir9,1`
    - 去除`CPU，Type`: `0x0705`,已自动识别 `i7`
    - 移除 `config_Install.plist`,下面说明 `CLOVER 安装(12-4-2019) 或 Recovery 模式`
    - `SSDT-OCPublic-Merge.aml` 合并 `SSDT-EC.aml`、`SSDT-RTC0.aml`、`SSDT-USBX.aml`、`SSDT-ALS0.aml`、`SSDT-MCHC.aml`
    - 更新 [Clover_r5115](https://github.com/CloverHackyColor/CloverBootloader/releases/tag/5115)

   ### CLOVER 安装(`12-4-2019`) 或 Recovery 模式
   安装请使用：`Pro13_I7_Installer_DW1820A_and_UMIS_12-4-2019_by_黑果小兵.zip`
   - `安装系统` 或 `进Reocery模式` 请使用Clover下的：`config_Installer.plist`，[安装教程](https://blog.daliansky.net/Lenovo-Xiaoxin-PRO-13-2019-and-macOS-Catalina-Installation-Tutorial.html)
   - 安装系统后进系统请`一定要执行` `重建缓存`：软件或 命令： `sudo kextcache -i /`


- # 04-26-2020:  
  ### OC / Clover
  - 加回 `SSDT-GPRW.aml`
  - 禁用 `SSDT-USBX.aml`
  - `SSDT-PCI.LPCB-Wake-AOAC.aml` 重命名为 `SSDT-PCI0.LPCB-Wake-AOAC.aml`
  - 默认内置 `DW1820A` 网卡驱动，根据网卡类型去或留
  - 默认声卡 `layout-id` 为 `100`，根据需要可设置 `11`, `99`
  - 去除 `CPUFriend.kext`、`CPUFriendDataProvider.kext`
  - 机型由 `MacBookPro15,4` 更新为 `MacBookAir9,1`，需要重新设置三码，不然关于本机还是显示 `MacBook Pro`
  - `kexts` 日常驱动更新
  - `OC`更新为`0.5.8`
  - `Clover` 版本无更新

- # 04-18-2020:  
  ### OC / Clover 关于声卡ID 使用情况
  - `layout-id` 暂时改为 `11` 正常；
  - 目前使用 `99` `可能` 出现耳机无人声;
  - 有特殊用途( `mic 暂不可用，使用外接麦克风，但又想设置内置扬声器`)：`100`; 
  - - 使用 `100` 下默认:
  - - 输出：1.内置扬声器，2.耳机(即使没接入耳机)；
  - - 输入：1.内置麦克风，2.线路输入(即使没接入外接设备)；



- # 04-08-2020-OC(@宪武):
  - `AppleXcpmCfgLock`、`AppleXcpmExtraMsrs`设置`false`
  - 添加`VoodooInput.kext`驱动
  - 移除`disable-external-gpu`属性
  - 更新并重命名`SSDT-PCIWake-AOAC.aml`为`SSDT-PCI.LPCB-Wake-AOAC.aml`
  - `SSDT-RMCF-Fn-disable.aml`重命名为`SSDT-RMCF-PS2Map-LenovoPRO13.aml`
  - 更新`SSDT-RTC_Y-AWAC_N.aml`
  - 更新：`OC(0.5.8)`、`kexts`驱动日常更新

- # 3-24-2020  
  Clover/OC （@宪武）
  - 优化触控板驱动增加延迟、减少误触。使用`AOAC-PRW`全局更名（[详见OC-little](https://github.com/daliansky/OC-little/tree/master/01-关于AOAC/01-5-AOAC-PRW全局更名)）
  - ### ACPI-Add下
  - 更新`SSDT-OCI2C-TPXX-lenovoPRO13.aml`补丁
  - 删除`SSDT-GPRW.aml`补丁

  - ### ACPI-Patch下
  - 删除`GPRW to XPRW` 替换成`_PRW to XPRW`: 
  - `Find: 5F505257`
  - `Replace: 58505257`

- # 3-18-2020  
  - Clover/OC:
  - 触摸板：优化三指和四肢

- # 3-11-2020(@宪武)

  - OC 分支更新
  - 更新OC版本；
  - 更新DVMT支持15.4;
  - 屏蔽*S键，Fn+C/P亮度调节，开机键亮屏

- # 3-8-2020(@daliansky)

  - CLOVER 分支更新
  - 声卡：新增`layout-id:100`，手动切换输入与输出节点，以解决无法驱动`Intel SST` DMIC内麦所带来的一系列问题
  - 新增：`DVMT` for 10.15.4 patch

  

- # 02-28-2020
  
  #### OC(@宪武大佬)
   - 更新OC，为下次更新OC声音(指OC的一个功能)准备；
   - 修复掉声卡问题；
   - 只显示引导菜单，其它菜单内容隐藏；
   - i5/i7合二为一；
   - USB供电(快充？需要手机设备支持)
   - Fn+Q 唤醒
  - [具体详情](/EFI/EFI-OC-PRO13-AOAC/EFI-OC.md)
  
- # 02-18-2020
  #### OC(@宪武大佬)
    - 触摸板驱动(`02-17`)；
    - 关闭触摸板方法 `FN+F6` 
    - 唤醒方法:`电源键唤醒`
    - 优化：`SSDT-I2CxConf.aml`做了较大修改，添加了保护，适用于所有机器

- # 02-17-2020
  #### Clover(@小兵大佬)
    - 添加触摸板驱动及相关信息；

- # 01-29-2020
  #### OC
    - 更新OC；
    - ALC声卡；
  
- # 01-16-2020
  #### Clover
    - 去除-v；
    - 修改因删除主题后开机显示白色背景+logo：改为开机显示为黑色+白色logo；
    - 修改开机第一阶段logo大小；
    - 显示【关于本机 - 内存 】

- # 01-08-2020
  #### OC （宪武大佬更新）
    - 删除VirtualSmc.efi以及config中列表;
    - config新增-OSInfo;
    - config新增-SignalAppleOS;
    - config新增-SupportsCsm;
    - config新增-WriteFlash;
    - config新增2-AppleSmcIo;
    - config新增2-AuthRestart;
    - 更新DW1820A蓝牙、Wi-Fi驱动;
    - 删除SSDT-Q0CQ0D-Energy.aml;
    - SSDT-S1-S3-disable.aml撤回SSDT-S3-disable.aml;
    - 删除CPUFriend.kext、CPUFriendDataProvider.kext;
    - 添加NVMeFix.kext;
    - 更新版本OpenCore.efi版本(https://github.com/n-d-k/OpenCorePkg);
    - 删除RU.efi;
    - 添加grubwithsetup_var.efi;
    - 日常更新Lilu.kext、VirtualSMC.kext等驱动
    - 删除modGRUBShell.efi
    - config-i5.plist为i5机型使用;
    - config-i7.plist为i7机型使用，与i5区别在于DVMT;
    - config-识别i7.plist为i7机型使用，在config-i7.plist基础上补充完整信息，取消自动补充参数，识别i7（关于本机）

- # 01-06-2020  
  #### CLOVER(@daliansky)
  - 添加对 `DW1820A` 注入 `pci-aspm-default`(请根据 `DW1820A` 的 `PCI`地址不同更改，请勿直接套搬，参考 [教程](https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html) )
  - `去掉`启动参数 `-alcbeta` (与 `AppleALC` 有关)
  - 暂时`注释`声卡 `PCI` 注入(暂时使用万能声卡 `VoodooHDA` 驱动)

- # 01-01-2020  
  - `OC` 暂时不支持引导安装，只驱动集显；
  - `CLOVER` 可以安装引导 和 驱动集显；
  - `CLOVER`、`OC` 内置 `DW1820A` 蓝牙、Wi-Fi 驱动;
  - `Clover`、`OC` 理论上通用 `i5`、`i7` (`i7-10710U` 仿冒 `i5 - 10210U` 的 `CPUID`: `0x0806EC`);
  - `Clover`、`OC` 都内置 `DW1820A` `Wi-Fi`、`蓝牙`驱动；
  - `Clover`、`OC` 仅添加 `10.15.* `的 `DVMT` 补丁；
  - `Clover` 已支持外接显示设备；
  - `App Store`、视频软件(`腾讯视频`)出现`鼠标卡断问题`的暂时解决方法：
   App Store 左上角，`偏好设置`，`视频自动播放`，去除打勾☑️。
  #### 未解决：
  - 0、某个机型不能驱动集显，未找到原因；
  - 1、如果使用 `10.15.x` 以下版本系统，可能出现进不了系统，自行添加对应的DVMT；
  - 2、触摸板、睡眠、声卡(`暂时用万能驱动，手动切换Speaker，不支持内置麦克风`)；
  - 3、`OC`  `i7-10710U` 目前 识别为 `i5`，不影响使用；
  - 4、`OC` 不支持外接显示设备；
  - 5、`OC` 不支持引导安装。