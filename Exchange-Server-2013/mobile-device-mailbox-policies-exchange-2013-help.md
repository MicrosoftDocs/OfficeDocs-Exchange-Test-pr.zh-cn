---
title: '移动设备邮箱策略: Exchange 2013 Help'
TOCTitle: 移动设备邮箱策略
ms:assetid: 9317b3bc-44a1-4e54-bc51-4f0b194b6a55
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123783(v=EXCHG.150)
ms:contentKeyID: 50491045
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 移动设备邮箱策略

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-06-16_

在 MicrosoftExchange Server 2013 中，您可以创建移动设备邮箱策略，将常用的策略集或安全设置应用于一组用户。在 Exchange 2013 组织中部署 Exchange ActiveSync 之后，可以新建移动设备邮箱策略，也可以修改现有策略。安装 Exchange 2013 时，会创建一条默认的移动设备邮箱策略。这条默认的移动设备邮箱策略将自动分配给所有用户。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Windows Phone 7 移动手机仅支持所有 Exchange ActiveSync 邮箱策略设置的子集。有关完整列表，请参阅 Windows Phone 7 同步。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>iOS7 指纹读取器不支持作为设备密码。如果启用指纹读取器来保护您的 iOS7 设备，当您的移动设备邮箱策略需要密码时，将仍需要创建和输入密码。</td>
</tr>
</tbody>
</table>


## 移动设备邮箱策略概述

您可以使用移动设备邮箱策略管理许多不同的设置。其中包括：

  - 要求使用密码

  - 指定最小密码长度

  - 要求在密码中使用数字或特殊字符

  - 指定在要求用户重新输入密码之前设备可以保持非活动状态的时间

  - 指定密码尝试失败多少次后擦除设备

有关所有可配置的设置的详细信息，请参阅移动设备策略设置。

## 管理 Exchange ActiveSync 邮箱策略

移动设备邮箱策略可在 Exchange 管理中心 (EAC) 或 Exchange 命令行管理程序中创建。如果在 EAC 中创建策略，只能配置可用设置的子集。可以使用命令行管理程序配置其余的设置。

## Windows Phone 7 同步

如果在组织中拥有 Windows Phone 7 移动电话，则在配置某些 Exchange ActiveSync 邮箱策略属性时，这些电话会遇到同步问题。若要使 Windows Phone 7 移动电话可以与 Exchange 邮箱同步，请将 **AllowNonProvisionableDevices** 属性设置为 True，或仅配置以下 Exchange ActiveSync 邮箱策略属性：

  - AllowSimplePassword

  - BlockInternetSharing

  - BlockRemoteDesktop

  - DisableDesktopSync

  - DisableIrDA

  - DisableRemovableStorage

  - DeviceWipeThreshold

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - PasswordExpiration

  - PasswordHistory

  - PasswordRequired

## 移动设备邮箱策略设置

下表总结了可以使用移动设备邮箱策略指定的设置。

### 移动设备邮箱策略设置

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>设置</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>允许蓝牙</p></td>
<td><p>此设置指定移动设备是否允许建立 Bluetooth 连接。可用选项包括“禁用”、“仅免提”和“允许”。默认值为“允许”。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
<tr class="even">
<td><p>允许浏览器</p></td>
<td><p>此设置指定是否允许在移动设备上使用 Pocket Internet Explorer。此设置不会影响移动设备上安装的第三方浏览器。默认值为 <code>$true</code>。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
<tr class="odd">
<td><p>允许照相机</p></td>
<td><p>此设置指定是否可以使用移动设备上的照相机。默认值为 <code>$true</code>。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
<tr class="even">
<td><p>允许用户电子邮件</p></td>
<td><p>此设置指定移动设备用户是否可以在移动设备上配置个人电子邮件帐户（POP3 或 IMAP4）。默认值为 <code>$true</code>。此设置不控制使用第三方移动设备电子邮件程序对电子邮件帐户的访问。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
<tr class="odd">
<td><p>允许桌面同步</p></td>
<td><p>此设置指定移动设备是否可以通过电缆、Bluetooth 或 IrDA 连接与计算机进行同步。默认值为 <code>$true</code>。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
<tr class="even">
<td><p>允许外部设备管理</p></td>
<td><p>此设置指定是否允许使用外部设备管理程序来管理移动设备。</p></td>
</tr>
<tr class="odd">
<td><p>允许 HTML 电子邮件</p></td>
<td><p>此设置指定同步到移动设备的电子邮件是否可以采用 HTML 格式。如果此设置设为 <code>$false</code>，所有电子邮件将转换为纯文本。</p></td>
</tr>
<tr class="even">
<td><p>允许 Internet 共享</p></td>
<td><p>此设置指定是否可以使用移动设备作为台式机或便携式计算机的调制解调器。默认值为 <code>$true</code>。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
<tr class="odd">
<td><p>AllowIrDA</p></td>
<td><p>此设置指定移动设备是否允许建立红外连接。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
<tr class="even">
<td><p>允许移动 OTA 更新</p></td>
<td><p>此设置指定是否可以通过手机网络数据连接将移动设备邮箱策略设置发送到移动设备。默认值为 <code>$true</code>。</p></td>
</tr>
<tr class="odd">
<td><p>允许不可设置的设备</p></td>
<td><p>此设置指定是否允许可能不支持应用所有策略设置的移动设备使用 Exchange ActiveSync 连接到 Exchange 2013。允许不可设置的设备会产生安全隐患。例如，某些不可设置的设备可能无法实现组织的密码要求。</p></td>
</tr>
<tr class="even">
<td><p>允许 POP/IMAP 电子邮件</p></td>
<td><p>此设置指定用户是否可以在移动设备上配置 POP3 或 IMAP4 电子邮件帐户。默认值为 <code>$true</code>。此设置不控制第三方电子邮件程序的访问。</p></td>
</tr>
<tr class="odd">
<td><p>允许远程桌面</p></td>
<td><p>此设置指定移动设备是否可以启动远程桌面连接。默认值为 <code>$true</code>。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
<tr class="even">
<td><p>允许简单密码</p></td>
<td><p>此设置启用或禁用诸如 1111 或 1234 这样的简单密码。默认值为 <code>$true</code>。</p></td>
</tr>
<tr class="odd">
<td><p>允许 S/MIME 加密算法协商</p></td>
<td><p>此设置指定移动设备上的邮件应用程序是否可以在收件人的证书不支持指定的加密算法时协商加密算法。</p></td>
</tr>
<tr class="even">
<td><p>允许 S/MIME 软件证书</p></td>
<td><p>此设置指定移动设备上是否允许使用 S/MIME 软件证书。</p></td>
</tr>
<tr class="odd">
<td><p>允许存储卡</p></td>
<td><p>此设置指定移动设备是否可以访问存储卡中存储的信息。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
<tr class="even">
<td><p>允许短信服务</p></td>
<td><p>此设置指定是否可以在移动设备上使用短信服务。默认值为 <code>$true</code>。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
<tr class="odd">
<td><p>允许未签名应用程序</p></td>
<td><p>此设置指定是否可以在移动设备上安装未签名的应用程序。默认值为 <code>$true</code>。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
<tr class="even">
<td><p>允许未签名安装程序包</p></td>
<td><p>此设置指定是否可以在移动设备上运行未签名的安装程序包。默认值为 <code>$true</code>。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
<tr class="odd">
<td><p>允许 Wi-Fi</p></td>
<td><p>此设置指定是否允许在移动设备上进行无线 Internet 访问。默认值为 <code>$true</code>。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
<tr class="even">
<td><p>必须是字母数字密码</p></td>
<td><p>此设置要求密码包含数字和非数字字符。默认值为 <code>$true</code>。</p></td>
</tr>
<tr class="odd">
<td><p>已许可应用程序列表</p></td>
<td><p>此设置存储了可以在移动设备上运行的已许可应用程序的列表。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
<tr class="even">
<td><p>启用附件</p></td>
<td><p>此设置使附件可以下载到移动设备。默认值为 <code>$true</code>。</p></td>
</tr>
<tr class="odd">
<td><p>启用设备加密</p></td>
<td><p>此设置在移动设备上启用加密。并非所有移动设备都可以强制实行加密。有关详细信息，请参阅设备和移动操作系统文档。</p></td>
</tr>
<tr class="even">
<td><p>设备策略刷新间隔</p></td>
<td><p>此设置指定从服务器向移动设备发送移动设备邮箱策略的频率。</p></td>
</tr>
<tr class="odd">
<td><p>启用 IRM</p></td>
<td><p>此设置指定移动设备上是否启用了信息权限管理 (IRM)。</p></td>
</tr>
<tr class="even">
<td><p>最大附件大小</p></td>
<td><p>此设置控制可下载到移动设备的附件的最大大小。默认值为“Unlimited”。</p></td>
</tr>
<tr class="odd">
<td><p>最长日历期限筛选器</p></td>
<td><p>此设置指定可同步到移动设备的日历日的最大范围。接受以下值：</p>
<ol>
<li><p>All</p></li>
<li><p>OneDay</p></li>
<li><p>ThreeDays</p></li>
<li><p>OneWeek</p></li>
<li><p>TwoWeeks</p></li>
<li><p>OneMonth</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>最长电子邮件期限筛选器</p></td>
<td><p>此设置指定可同步到移动设备的电子邮件项的最大天数。接受以下值：</p>
<ol>
<li><p>All</p></li>
<li><p>OneDay</p></li>
<li><p>ThreeDays</p></li>
<li><p>OneWeek</p></li>
<li><p>TwoWeeks</p></li>
<li><p>OneMonth</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>最大电子邮件正文截断大小</p></td>
<td><p>此设置指定电子邮件在同步到移动设备的过程中被截断的最大大小。该值以千字节 (KB) 为单位。</p></td>
</tr>
<tr class="even">
<td><p>最大电子邮件 HTML 正文截断大小</p></td>
<td><p>此设置指定 HTML 电子邮件在同步到移动设备的过程中被截断的最大大小。该值以千字节 (KB) 为单位。</p></td>
</tr>
<tr class="odd">
<td><p>最大不活动时间锁定</p></td>
<td><p>此值指定移动设备在要求提供密码重新激活之前可处于非活动状态的时长。可以输入 30 秒和 1 小时之间的任何时间间隔。默认值为 15 分钟。</p></td>
</tr>
<tr class="even">
<td><p>最大密码失败尝试次数</p></td>
<td><p>此设置指定用户为移动设备输入正确密码之前可以尝试的次数。可以输入 4 到 16 之间的任意数字。默认值为 8。</p></td>
</tr>
<tr class="odd">
<td><p>最小密码复杂字符数</p></td>
<td><p>此设置指定移动设备密码要求的字符集数量。字符集有：</p>
<ul>
<li><p>小写字母。</p></li>
<li><p>大写字母。</p></li>
<li><p>数字（0 到 9）。</p></li>
<li><p>特殊字符（例如，感叹号）。</p></li>
</ul>
<p>您可以输入介于 1 到 4 之间的任意数字。默认值为 1。</p>
<p>对于 Windows Phone 8 设备，此设置指定密码要求的字符集数量。例如，值 3 至少需要任何三个字符集内的一个字符。</p>
<p>对于 Windows Phone 10 设备，此设置将指定以下密码复杂性要求：</p>
<ol>
<li><p>仅限数字。</p></li>
<li><p>数字和小写字母。</p></li>
<li><p>数字、小写字母和大写字母。</p></li>
<li><p>数字、小写字母、大写字母和特殊字符。</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>最短密码长度</p></td>
<td><p>此设置指定移动设备密码包含的最小字符数。可以输入 1 到 16 之间的任意数字。默认值为 4。</p></td>
</tr>
<tr class="odd">
<td><p>启用密码</p></td>
<td><p>此设置启用移动设备密码。</p></td>
</tr>
<tr class="even">
<td><p>密码有效期</p></td>
<td><p>此设置使管理员可以配置密码更改时长，经过此时长之后必须更改移动设备的密码。</p></td>
</tr>
<tr class="odd">
<td><p>密码历史记录</p></td>
<td><p>此设置指定可以存储在用户邮箱中的旧密码数。用户不能重复使用已存储的密码。</p></td>
</tr>
<tr class="even">
<td><p>启用密码恢复</p></td>
<td><p>启用此设置后，移动设备可以生成恢复密码并发送到服务器。如果用户忘记自己的移动设备密码，可使用恢复密码解除锁定移动设备，然后可以创建新的移动设备密码。</p></td>
</tr>
<tr class="odd">
<td><p>要求设备加密</p></td>
<td><p>此设置指定是否要求设备加密。如果设置为 <code>$true</code>，移动设备必须能够支持和实现加密，才能与服务器同步。</p></td>
</tr>
<tr class="even">
<td><p>要求加密 S/MIME 邮件</p></td>
<td><p>此设置指定是否必须加密 S/MIME 邮件。默认值为 <code>$false</code>。</p></td>
</tr>
<tr class="odd">
<td><p>要求加密 S/MIME 算法</p></td>
<td><p>此设置指定加密 S/MIME 邮件时必须使用哪种必需的算法。</p></td>
</tr>
<tr class="even">
<td><p>漫游时要求手动同步</p></td>
<td><p>此设置指定移动设备漫游时是否必须手动同步。如果允许在漫游时自动同步，将会经常使移动设备数据计划的数据费用超过预期。</p></td>
</tr>
<tr class="odd">
<td><p>要求签名 S/MIME 算法</p></td>
<td><p>此设置指定为邮件签名时必须使用哪种必需的算法。</p></td>
</tr>
<tr class="even">
<td><p>要求签名 S/MIME 邮件</p></td>
<td><p>此设置指定移动设备是否必须发送已签名的 S/MIME 邮件。</p></td>
</tr>
<tr class="odd">
<td><p>要求存储卡加密</p></td>
<td><p>此设置指定是否必须加密存储卡。并非所有移动设备操作系统均支持存储卡加密。有关详细信息，请参阅您的移动设备及移动操作系统的文档。</p></td>
</tr>
<tr class="even">
<td><p>未许可的 ROM 中应用程序列表</p></td>
<td><p>此设置指定不能在 ROM 中运行的应用程序列表。需要 Exchange Enterprise 客户端访问许可证才能更改此设置的值。</p></td>
</tr>
</tbody>
</table>

