---
title: '将移动电话配置为访问电子邮件: Exchange 2013 Help'
TOCTitle: 将移动电话配置为访问电子邮件
ms:assetid: 8d6e2cea-265a-43d9-a074-076f35658436
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123704(v=EXCHG.150)
ms:contentKeyID: 52061371
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 将移动电话配置为访问电子邮件

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-03-12_

可以配置移动电话（如 Windows 电话）以使用 MicrosoftExchange ActiveSync。您应该对组织中的每部移动电话执行此过程。

## 先决条件

  - 您已查阅要配置的移动电话的制造商文档。

  - 在组织中已启用 Exchange ActiveSync。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有关在移动电话或平板电脑上设置基于 Microsoft Exchange 的电子邮件的设备专用信息，请参阅<a href="https://support.office.com/zh-cn/article/set-up-a-mobile-device-using-office-365-for-business-7dabb6cb-0046-40b6-81fe-767e0b1f014f">使用 Office 365 商业版设置移动设备</a>。</td>
</tr>
</tbody>
</table>


## 配置移动电话以使用 Exchange ActiveSync

大多数移动电话和设备能够使用 Autodiscover 配置移动电子邮件客户端以使用 Exchange ActiveSync。若要在大多数移动电话上配置电子邮件帐户，需要两类信息。

  - 用户的电子邮件地址

  - 用户密码

如果移动电话无法通过自动发现自动与 Exchange 服务器联系，则您必须手动设置移动电话。若要进行手动设置，则需要提供用户的电子邮件地址和密码以及 Exchange ActiveSync 服务器名称。在大多数组织中，Exchange ActiveSync 服务器名称与不带 /owa 的 Outlook Web App 服务器名称相同，例如 mail.contoso.com。

## Windows Phone 同步

如果您配置 Windows Phone 移动电话以使用 Exchange 与 Exchange ActiveSync 同步，则仅支持移动设备邮箱策略设置的子集。[Windows Phone 和设备支持的移动设备邮箱策略](supported-mobile-device-mailbox-policies-for-windows-phones-and-devices-exchange-2013-help.md)中详述了这些策略设置。

如果您对所使用的 Windows Phone 版本不支持的移动设备邮箱策略设置进行配置，则还必须将 **AllowNonProvisionableDevices** 策略设置设置为 true 或者为 Windows Phone 移动电话创建单独的移动设备邮箱策略。

