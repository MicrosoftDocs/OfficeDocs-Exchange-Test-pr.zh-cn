---
title: '为独立的业务单位配置接受域: Exchange 2013 Help'
TOCTitle: 为独立的业务单位配置接受域
ms:assetid: bc95dbdc-3669-4c06-ab94-90093bc0dbfd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657491(v=EXCHG.150)
ms:contentKeyID: 50491438
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为独立的业务单位配置接受域

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-02-17_

在某些情况下，您可能希望为电子邮件服务器位于 Exchange 组织外部的独立业务单元配置接受域。在此情况中，您可以将接受域配置为外部中继域。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“接受域”条目。

  - 如果您已在外围网络中订阅了边缘传输服务器，请在 Exchange 组织中的邮箱服务器上配置接受的域。在 EdgeSync 同步期间，接受的域配置会复制到边缘传输服务器。有关详细信息，请参阅[边缘订阅](edge-subscriptions-exchange-2013-help.md)。

  - 要创建的接受域的名称不能与已配置的远程域的名称相同。例如，如果已将 fabrikam.com 配置为远程域，则不能创建名称为 fabrikam.com 的接受域。

  - 配置接受域之前，必须验证该 SMTP 命名空间的公用域名系统 (DNS) MX 资源记录存在，并且该 MX 资源记录引用了与 Exchange 组织关联的服务器名称和 IP 地址。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用 EAC 将接受域配置为外部中继域

您可能希望为电子邮件服务器位于 Exchange 组织外部的独立业务单元配置接受域。

1.  在 EAC 中，导航到“邮件流”\>“接受域”，选择您要配置的域，单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在“名称”字段中，输入接受域的显示名称。贵组织的每个接受域必须具有唯一显示名称。这可能与接受域不同。例如，域 Contoso.com 可以拥有 Contoso Local Accepted Domain 的显示名称。

3.  选择“外部中继域”。该选项用于中继到 Exchange 组织外部的服务器的电子邮件。

4.  单击“保存”。

## 您如何知道这有效？

要验证您是否已成功将接受域配置为外部中继域，请从您已配置为外部中继域的接受域发送一封邮件，并验证该邮件是否收到。

