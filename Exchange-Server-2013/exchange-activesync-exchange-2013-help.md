---
title: 'Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync
ms:assetid: 5fafaff3-eb37-4fdb-95f0-e56c45ea5884
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998357(v=EXCHG.150)
ms:contentKeyID: 50490683
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ActiveSync

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

了解 Exchange Server 2013 的 Exchange ActiveSync 客户端协议。您将了解 Exchange ActiveSync 功能，包括安全功能、您可以管理的项目、如何确保其安全，以及如何避免同步到 Windows Phone 7 出现问题。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主题适用于管理员。想要设置您的 Windows Phone、iOS 或 Android 设备以访问您的 Office 365 或 Exchange Server 邮箱？请查看下列主题。
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=615415">Set up email on Windows Phone</a>（在 Windows Phone 上设置电子邮件）</p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=615414">在 iPhone、iPad 或 iPod Touch 上设置电子邮件</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/?linkid=615417">在 Android 手机或平板电脑上设置电子邮件</a></p></li>
</ul></td>
</tr>
</tbody>
</table>


Exchange ActiveSync 是使您可以将移动设备与 Exchange 邮箱同步的客户端协议。安装 Microsoft Exchange 2013 时，默认情况下会启用 Exchange ActiveSync。

**目录**

Exchange ActiveSync 概述

Exchange ActiveSync 中的功能

管理 Exchange ActiveSync

Windows Phone 7 同步

## Exchange ActiveSync 概述

Exchange ActiveSync 是一种 Microsoft Exchange 同步协议，该协议经过优化，以适用于高延迟和低带宽网络。基于 HTTP 和 XML 的协议使移动电话可以访问运行 Microsoft Exchange 的服务器上的组织信息。Exchange ActiveSync 使移动电话用户可以访问其电子邮件、日历、联系人和任务，并且在脱机工作时仍可以继续访问这些信息。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange ActiveSync 不支持共享邮箱或代理访问。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Windows Phone 7 移动电话仅支持所有 Exchange ActiveSync 邮箱策略设置的子集。有关完整列表，请参阅 Windows Phone 7 同步。</td>
</tr>
</tbody>
</table>


## Exchange ActiveSync 中的功能

Exchange ActiveSync 具有以下功能：

  - 支持 HTML 邮件

  - 支持后续标志

  - 电子邮件的会话分组

  - 能够同步或不同步整个会话

  - 可将短信服务 (SMS) 消息与用户的 Exchange 邮箱同步

  - 支持查看邮件答复状态

  - 支持快速邮件检索

  - 会议与会者信息

  - 增强的 Exchange 搜索

  - PIN 重置

  - 通过密码策略增强的设备安全性

  - 用于无线设置的自动发现

  - 支持设置用户离开、度假或外出时的自动答复

  - 支持任务同步

  - 直推技术

  - 支持联系人的可用性信息

## 管理 Exchange ActiveSync

默认情况下，已启用 Exchange ActiveSync。拥有 Exchange 邮箱的所有用户都可以将其移动设备与 Microsoft Exchange 服务器进行同步。

可以执行下列 Exchange ActiveSync 任务：

  - 启用和禁用用户的 Exchange ActiveSync

  - 设置诸如最小密码长度、设备锁定和最大密码尝试失败次数等策略

  - 启动远程擦除，从丢失或被盗的移动电话中清除所有数据

  - 运行多种报告，以便查看或导出为各种格式

  - 控制可以通过设备访问规则与组织同步的移动设备类型

## Exchange ActiveSync 中的安全性

可以配置 Exchange ActiveSync，对 Exchange 服务器和移动设备之间的通信使用安全套接字层 (SSL) 加密。

## 在 Exchange ActiveSync 中管理移动设备访问

可以控制能够同步的移动设备。可以通过在新移动设备连接到组织时监视它们或通过设置确定允许连接的移动设备类型的规则，来执行此操作。无论选择何种方式来指定可以同步的移动设备，都可以随时为特定用户批准或拒绝对任何特定移动设备的访问

## Exchange ActiveSync 中的设备安全功能

除了能够为 Exchange 服务器和移动设备之间的通信配置安全选项以外，Exchange ActiveSync 还提供了下列功能，以增强移动设备的安全性：

  - **远程擦除**   如果您的移动设备丢失、被盗或存在其他安全风险，则可通过使用 Outlook Web App 从 Exchange Server 计算机或从任何 Web 浏览器发出远程擦除命令。该命令将从移动设备上清除所有数据。

  - **设备密码策略**   Exchange ActiveSync 允许为设备密码配置几个选项。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>iOS7 指纹读取器技术不能用作设备密码。如果您选择使用 iOS7 指纹读取器，而组织的移动设备邮箱策略要求设备密码，则您仍需要创建和输入设备密码。</td>
    </tr>
    </tbody>
    </table>
    
    设备密码选项包括：
    
      - **最小密码长度(字符)**   此选项可以为移动设备指定密码长度。默认长度是 4 个字符，但最多可以包括 18 个字符。
    
      - **最小字符集数目**   使用此文本框可以指定字母数字密码的复杂性，并强制用户使用以下字符集中的若干不同字符集：小写字母、大写字母、符号和数字。
    
      - **需要字母数字密码**   此选项确定密码强度。可以强制在密码中使用除数字以外的字符或符号。
    
      - **不活动时间(秒)**   此选项确定在系统提示用户输入密码以解除移动设备锁定之前该移动设备必须处于不活动状态的时间长度。
    
      - **强制密码历史**   选中此复选框可以强制移动电话阻止用户重复使用其以前的密码。您设置的数字可确定不允许用户重复使用的过去密码的数目。
    
      - **启用密码恢复**   选中此复选框可以对移动设备启用密码恢复。管理员可以使用 **Get-ActiveSyncDeviceStatistics** cmdlet 来查找用户的恢复密码。
    
      - **擦除设备之前允许的尝试失败次数**   此选项用于指定是否要在发生多次密码尝试失败后擦除电话内存。

  - **设备加密策略**   您可以对一组用户强制执行一些移动设备加密策略。这些策略包括：
    
      - **要求在设备上进行加密**   选中此复选框可以要求在移动设备上进行加密。这样可通过对移动设备中的所有信息加密来增强安全性。
    
      - **要求对存储卡加密**   选中此复选框可以要求对移动设备的可移动存储卡加密。这样可通过对移动设备存储卡上的所有信息进行加密来增强安全性。

## Windows Phone 7 同步

如果在组织中拥有 Windows Phone 7 移动设备，则在配置某些移动设备邮箱策略属性时，这些设备会遇到同步问题。若要使 Windows Phone 7 移动电话可以与 Exchange 邮箱同步，请将 **AllowNonProvisionableDevices** 属性设置为 true，或仅配置以下移动设备邮箱策略属性：

  - PasswordRequired

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - DeviceWipeThreshold

  - AllowSimplePassword

  - PasswordExpiration

  - PasswordHistory

  - DisableRemovableStorage

  - DisableIrDA

  - DisableDesktopSync

  - BlockRemoteDesktop

  - BlockInternetSharing

