# 升级 BIOS 和增强性能

[English](README.md) | **中文**

## 目录

- [简介](#简介)
- [TM1701](#tm1701)
  - [更新历史](#更新历史)
  - [怎么升级](#怎么升级)
  - [怎么提升性能](#怎么提升性能)
- [TM1707](#tm1707)
  - [更新历史](#更新历史-1)
  - [怎么升级](#怎么升级-1)
  - [怎么提升性能](#怎么提升性能-1)
- [TM1905](#tm1905)
  - [更新历史](#更新历史-2)
  - [怎么升级](#怎么升级-2)
  - [怎么提升性能](#怎么提升性能-2)
- [TM1963](#tm1963)
  - [更新历史](#更新历史-3)
  - [怎么升级](#怎么升级-3)
- [鸣谢](#鸣谢)


## 简介

| 机型 | 提供的 BIOS 版本 |
| ------ | ---------- |
| TM1701 | [XMAKB5R0P0603](TM1701/XMAKB5R0P0603)，[XMAKB5R0P0906](TM1701/XMAKB5R0P0906)，[XMAKB5R0P0A07](TM1701/XMAKB5R0P0A07.exe)，[XMAKB5R0P0E07](TM1701/XMAKB5R0P0E07.exe) |
| TM1707 | [XMAKB5RRP0C05](TM1707/XMAKB5RRP0C05.exe) |
| TM1905 | [XMACM500P0401](TM1905/XMACM500P0401.exe) |
| TM1963 | [XMACM5B1P0201](TM1963/XMACM5B1P0201.exe) |

这些 BIOS 包来自小米官方或加盟售后。

~文件夹 [ME](ME) 的 ME 固件来自于 [Fernando's Win-RAID 论坛](https://www.win-raid.com/t596f39-Intel-Management-Engine-Drivers-Firmware-amp-System-Tools.html)。更新最新的 ME 固件有助于抵御潜在的恶意攻击。上述文件夹里的 ME 固件版本是 `Intel CSME 11.8 Consumer PCH-LP Firmware v11.8.55.3510`，`Intel (CS)ME System Tools` 的版本是 `Intel CSME System Tools v11 r14 - (2018-08-09)`。~

**警告：因为操作涉及到 BIOS 等底层代码，如果在升级过程中出现错误（比如升级程序强制退出，或不正确地运行[#8](https://github.com/stevezhengshiqi/XiaoMi-Pro/issues/8)里的脚本)，电脑可能无法启动。**

如果很不幸这些悲惨的事情发生在你身上，建议你去咨询小米售后进行维修。如果你使用了本仓库的任意脚本或固件包，你需要承担所有后果，作者只是提供固件和途径，请大家谨慎斟酌。


## TM1701

### 更新历史

#### XMAKB5R0P0906

- BIOS 面板里新增 `KB Backlight Mode` 选项，可选择 `Power Saving` （默认，键盘灯空闲15秒后自动熄灭）或 `Standard` （键盘灯在系统非睡眠时常亮）
- 减少低负载下的风扇噪声

#### XMAKB5R0P0A07 和 XMAKB5R0P0E07

- 我对这些版本的新特性完全不知情。提供者们没有给予很多的信息。
- 在我的电脑上 XMAKB5R0P0A07 的 `KB Backlight Mode` - `Standard` 不工作。
- 升级到这些 BIOS 版本十分简单，下载并运行 exe 文件即可。


### 怎么升级

#### XMAKB5R0P0603

**降级到这个版本是被允许的**

1. 准备一个 FAT32 U盘，下载 [XMAKB5R0P0603](TM1701/XMAKB5R0P0603) 文件夹里的所有文件并把它们放入U盘的根目录。

2. 插上电源并重启电脑，按 `F12`，并选择U盘启动项。

3. 在 shell 界面，输入 `unlockme.nsh`，然后电脑可能会自动重启。然后重复第 2 步并输入 `flash.nsh`。

4. 等待安装过程结束。

#### XMAKB5R0P0906

有句老话说得好，“不打无准备之仗”。**备份重要资料永远不会错。** 有用户反映运行程序后会遇到蓝屏问题。

1. 下载 [XMAKB5R0P0906](TM1701/XMAKB5R0P0906) 文件夹里的所有文件。

2. 用管理员权限运行 `H2OFFT-Wx64.exe`。
  - 注意：从这一步开始，你的电脑最好接上电源，直到整个安装进程结束。

3. 一个警告可能会出现，忽视它并继续更新。

4. 电脑会自动重启，等待，直到安装过程结束。

#### XMAKB5R0P0A07 或更新版本

直接运行 exe 文件即可。保证电脑在升级时一直接上电源。


### 怎么提升性能

[FallenChromium](https://github.com/FallenChromium) 和 [Cyb](http://4pda.ru/forum/index.php?showuser=914121) 制作了脚本用来扩大动态显存大小（从32mb扩大到64mb），解锁 MSR 0xE2 寄位器，和修改 EC 固件来减少风扇噪声。脚本位于 [DVMT_and_0xE2_fix](TM1701/DVMT_and_0xE2_fix)。如果想获取更多的信息，你可以访问 [#8](https://github.com/stevezhengshiqi/XiaoMi-Pro/issues/8) 和 [cybsuai的仓库](https://github.com/cybsuai/Mi-Notebook-Pro-tweaks)。

运行完脚本后，你需要在 `config.plist` 里删除 `framebuffer-fbmem` 和 `framebuffer-stolenmem`，修改 `framebuffer-flags` 并禁用 MSR 0xE2 补丁。
- 打开 `/EFI/CLOVER (或者 OC)/config.plist`，删除以下代码：
```xml
  <key>framebuffer-fbmem</key>
  <data>AACQAA==</data>
  <key>framebuffer-stolenmem</key>
  <data>AAAwAQ==</data>
```
- 然后修改 `framebuffer-flags` 来开启 `FBEnableDynamicCDCLK`
```diff
  <key>framebuffer-flags</key>
-   <data>CwfDAA==</data>
+   <data>CwfjAA==</data>
```
- 如果是 Clover 用户，更改以下代码来禁用 MSR 0xE2 补丁：
```diff
    <key>KernelPm</key>
-   <true/>
+   <false/>
```
- 如果是 OC 用户，更改以下代码来禁用 MSR 0xE2 补丁：
```diff
    <key>AppleXcpmCfgLock</key>
-   <true/>
+   <false/>
```


## TM1707

### 更新历史

#### XMAKB5RRP0C05

- BIOS 提供商没有提供更多信息


### 怎么升级

#### XMAKB5RRP0C05

直接运行 exe 文件即可。保证电脑在升级时一直接上电源。


### 怎么提升性能

下面这张表是关于 BIOS 的一些高级配置，感谢 [goodyttoor](https://github.com/goodyttoor)。

| 项目 | 地址 | 选项 |
| ----- | ----- | ----- |
| DVMT Pre-Allocated | 0xDF | 0x1: 32M (默认), 0x2: 64M (推荐) |
| DVMT Total Gfx Mem | 0xE0 | 0x1: 128M, 0x2: 256M (默认), 0x3: MAX (推荐) |
| CFG Lock | 0x3C | 0x0: Disabled (推荐), 0x1: Enabled (默认) |
| BIOS Lock | 0x17 | 0x0: Disabled (推荐), 0x1: Enabled (默认) |


## TM1905

### 更新历史

#### XMACM500P0401

- BIOS 提供商没有提供更多信息


### 怎么升级

#### XMACM500P0401

直接运行 exe 文件即可。保证电脑在升级时一直接上电源。


### 怎么提升性能

下面这张表是关于 BIOS 的一些高级配置，感谢 [htmambo](https://github.com/htmambo)。

| 项目 | 地址 | 配置项 | 选项 | 默认 | 推荐 |
| ----- | ----- | ----- | ----- | ----- | ----- |
| RTC | 0x54A | SETUP | 0x0:ACPI Time and Alarm Device; 0x1:Legacy RTC | 0x0 | 0x1 |
| DVMT | 0x107 | SaSETUP | 0x0:0M, 0x1:32M, 0x2:64M | 0x1 | 0x2 |
| DVMT Total Gfx Mem | 0x108 | SaSETUP | 0x1:128M, 0x2:256M, 0x3:Max | 0x3 | 0x3 |
| CFG LOCK | 0x3E | CpuSetup | 0x0:Disabled, 0x1:Enabled | 0x1 | 0x0 |
| MSR LOCK | 0x2B | SETUP | 0x0:Disabled, 0x1:Enabled | 0x0 | 0x0 |
| BIOS Lock | 0x17 | SETUP | 0x0:Disabled, 0x1:Enabled | 0x1| 0x0 |

修改完配置后，你需要在 `config.plist` 里删除 `framebuffer-stolenmem` 并禁用 MSR 0xE2 补丁。
- 打开 `/EFI/CLOVER (或者 OC)/config.plist`，删除以下代码：
```xml
  <key>framebuffer-stolenmem</key>
  <data>AADgAQ==</data>
```
- 如果是 Clover 用户，更改以下代码来禁用 MSR 0xE2 补丁：
```diff
    <key>KernelPm</key>
-   <true/>
+   <false/>
```
- 如果是 OC 用户，更改以下代码来禁用 MSR 0xE2 补丁：
```diff
    <key>AppleXcpmCfgLock</key>
-   <true/>
+   <false/>
```


## TM1963

### 更新历史

#### XMACM5B1P0201

- BIOS 提供商没有提供更多信息


### 怎么升级

#### XMACM5B1P0201

直接运行 exe 文件即可。保证电脑在升级时一直接上电源。


## 鸣谢

- 感谢一个热心的朋友提供 `XMAKB5R0P0A07` BIOS 包。他不想惹上麻烦，所以还请大家不要随意流传 `XMAKB5R0P0A07` BIOS 包。**不建议QQ群友讨论并上传此包，会给上传者带来很大的麻烦。**
- 感谢 [Cyb](http://4pda.ru/forum/index.php?showuser=914121) 和 [FallenChromium](https://github.com/FallenChromium) 提供优秀的脚本来增强性能。
- 感谢 [goodyttoor](https://github.com/goodyttoor) 提供 TM1707 BIOS 高级配置。
- 感谢 [htmambo](https://github.com/htmambo) 提供 TM1905 BIOS 高级配置。
- 感谢 小米加盟售后 和 [一土木水先生](http://bbs.xiaomi.cn/u-detail-1242799508) 提供 `XMAKB5R0P0603` 和 `XMAKB5R0P0906` BIOS 包。原出处在[这里](http://bbs.xiaomi.cn/t-36660609-1)。
- 感谢 [小米官方](https://www.mi.com/service/bijiben/drivers/15) 提供 `XMAKB5R0P0E07` BIOS 包。
- 感谢 [小米官方](https://www.mi.com/service/bijiben/drivers/15-game-gtx) 提供 `XMAKB5RRP0C05` BIOS 包。
- 感谢 [小米官方](https://www.mi.com/service/bijiben/drivers/A10) 提供 `XMACM500P0401` BIOS 包。
- 感谢 [小米官方](https://www.mi.com/service/bijiben/drivers/A10G5) 提供 `XMACM5B1P0201` BIOS 包。
