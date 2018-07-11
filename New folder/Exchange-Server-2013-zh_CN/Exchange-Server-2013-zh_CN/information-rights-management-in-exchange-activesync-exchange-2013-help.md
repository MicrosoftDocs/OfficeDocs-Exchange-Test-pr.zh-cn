---
title: 'Exchange ActiveSync 中的信息权限管理: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync 中的信息权限管理
ms:assetid: ebf04460-4d61-4b00-86b9-85ec1dbbd6a1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff657743(v=EXCHG.150)
ms:contentKeyID: 50491910
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ActiveSync 中的信息权限管理

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

信息工作者经常会使用电子邮件交换敏感信息。为帮助保护此类信息的安全，组织可以使用信息权限管理 (IRM) 对邮件内容应用持久保护。由于越来越多地使用移动设备访问电子邮件，因此移动设备用户可创建和使用受 IRM 保护的内容，这一点很重要。

**目录**

Exchange 2013 中的移动 IRM 保护

要求

安全

启用 Exchange ActiveSync 中的 IRM

要了解与 IRM 相关的管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## Exchange 2013 中的移动 IRM 保护

在 Exchange 2013 中，用户通过 Microsoft Exchange ActiveSync 中的 IRM 可在任何受支持的 Exchange ActiveSync 设备上访问丰富 IRM 功能，而不必配置 AD RMS 权限或将设备连接到计算机并对其激活 IRM。此外，移动设备不需要运行 Windows。Microsoft 向移动设备制造商、原始设备制造商 (OEM) 和其他厂商颁发 Exchange ActiveSync 许可证。有关当前 Exchange ActiveSync 许可证持有人的列表，请展开 [Microsoft 技术许可](https://go.microsoft.com/fwlink/p/?linkid=198562) 页面上的“Exchange ActiveSync 协议”部分。

使用 Exchange ActiveSync 中的 IRM，移动设备用户可以：

  - 创建受 IRM 保护的邮件。

  - 阅读受 IRM 保护的邮件。

  - 回复和转发受 IRM 保护的邮件。

Exchange 2013 中的移动 IRM 保护

## 要求

适用下列要求：

  - 组织中的客户端访问服务器必须运行 Exchange 2010 SP1 或更高版本。

  - 必须在组织中部署 AD RMS 服务器。

  - 必须对内部邮件启用 IRM。这是 Exchange 2010 中所有 IRM 功能的先决条件。有关详细信息，请参阅[对内部邮件启用或禁用 IRM](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)。

  - 必须在 Exchange ActiveSync 邮箱策略中启用 IRM。可使用不同的 Exchange ActiveSync 邮箱策略对不同用户组启用或禁用 IRM。

  - 支持 Exchange ActiveSync 协议版本 14.1 的设备（包括 Windows 手机）可支持 Exchange ActiveSync 中的 IRM。设备的移动电子邮件应用程序必须支持 Exchange ActiveSync 版本 14.1 中定义的 RightsManagementInformation 标记。

Exchange 2013 中的移动 IRM 保护

## 安全

在 Exchange ActiveSync 中启用 IRM 时，客户端访问服务器将受 IRM 保护的邮件解密，然后再提供这些邮件供支持的移动设备访问。进行同步后，受 IRM 保护的邮件以不加密格式位于移动设备上。移动设备上具有 IRM 功能的电子邮件客户端应用程序实施 IRM 保护。

Exchange ActiveSync 中的 IRM 不会将客户端访问服务器上受 IRM 保护的附件解密。用于创建或查看文件的的应用程序强制访问受 IRM 保护的文件。例如，在 Windows 手机上，[Microsoft Office Mobile](https://go.microsoft.com/fwlink/p/?linkid=205121) 实施对 Microsoft Office 文件的 IRM 保护。要访问受 IRM 保护的 Office 文件，用户必须将设备连接到计算机，然后用 RMS 服务器激活 Office Mobile。

启用 Exchange ActiveSync 中的 IRM 时，建议使用下表中显示的 Exchange ActiveSync 策略设置帮助保护移动设备。

### Exchange ActiveSync 策略设置

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>设置</th>
<th>使用新 Exchange ActiveSync 邮箱策略向导进行配置</th>
<th>使用 New-ActiveSyncMailboxPolicy cmdlet 进行配置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>要求用户输入密码才能访问其移动设备上的信息。</p></td>
<td><p>选中“要求提供密码”复选框。</p></td>
<td><p>将 <em>DevicePasswordEnabled</em> 参数设置为 <code>$true</code>。</p></td>
</tr>
<tr class="even">
<td><p>对移动设备启用加密。</p></td>
<td><p>选中“要求提供密码”复选框，然后选中“要求对设备加密”复选框。</p></td>
<td><p>将 <em>RequireDeviceEncryption</em> 参数设置为 <code>$true</code>。</p>

> [!important]
> 将 <em>RequireDeviceEncryption</em> 参数设置为 <code>$true</code> 时，将无法连接不支持设备加密的移动设备。

</td>
</tr>
<tr class="odd">
<td><p>不允许不可设置的设备与 Exchange 服务器进行同步。</p></td>
<td><p>清除“允许不可设置的设备”复选框。</p></td>
<td><p>将 <em>AllowNonProvisionableDevices</em> 参数设置为 <code>$false</code>。</p></td>
</tr>
</tbody>
</table>


若要了解详细信息，请参阅[移动设备邮箱策略](mobile-device-mailbox-policies-exchange-2013-help.md)。

Exchange 2013 中的移动 IRM 保护

## 启用 Exchange ActiveSync 中的 IRM

要启用 Exchange ActiveSync 中的 IRM，请执行以下任务：

1.  将联合邮箱（Exchange 2013 和 Exchange 2010 安装程序创建的一个系统邮箱）添加到 AD RMS 中的超级用户组。这样，Exchange 2013 和 Exchange 2010 服务器便可以访问受 IRM 保护的邮件。有关详细信息，请参阅[将联合身份验证邮箱添加到 AD RMS 超级用户组](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

2.  使用 Exchange 命令行管理程序中的 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\)) cmdlet 在客户端访问服务器上启用 IRM。这样可为组织启用 Exchange ActiveSync 中的 IRM 和 Microsoft OfficeOutlook Web App 中的 IRM。有关详细信息，请参阅[启用或禁用客户端访问服务器上的信息权限管理](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md)。

Exchange 2013 中的移动 IRM 保护

