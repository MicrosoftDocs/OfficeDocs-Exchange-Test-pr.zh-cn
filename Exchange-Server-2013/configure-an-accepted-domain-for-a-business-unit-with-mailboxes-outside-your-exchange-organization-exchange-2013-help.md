---
title: '为在贵 Exchange 组织之外具有邮箱的业务单位配置接受域: Exchange 2013 Help'
TOCTitle: 为在贵 Exchange 组织之外具有邮箱的业务单位配置接受域
ms:assetid: ff46310b-5392-4eac-97bc-d39d397e1ce1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657737(v=EXCHG.150)
ms:contentKeyID: 50492061
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为在贵 Exchange 组织之外具有邮箱的业务单位配置接受域

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2014-08-06_

在一些实例中，您可能希望为业务单元配置接受域，其中域中的许多或全部收件人在 Exchange 组织中没有邮箱。例如，这会在组织在两个或更多不同的电子邮件系统之间共享相同 SMTP 地址空间时出现。对于此类情况，您可以配置接受域为内部中继域。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“接受域”条目。

  - 如果您已在外围网络中订阅了边缘传输服务器，请在 Exchange 组织中的邮箱服务器上配置接受的域。在 EdgeSync 同步期间，接受的域配置会复制到边缘传输服务器。有关详细信息，请参阅[边缘订阅](edge-subscriptions-exchange-2013-help.md)。

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


## 使用 EAC 配置接受域为内部中继域

1.  在 EAC 中，导航到“邮件流”\> “接受域”，选择您要配置的域，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在“名称”字段中，输入接受域的显示名称。贵组织的每个接受域必须具有唯一显示名称。这可能与接受域不同。例如，域 Contoso.com 可以拥有 Contoso Local Accepted Domain 的显示名称。

3.  选择“内部中继域”。

4.  单击“保存”。

## 您如何知道这有效？

要验证您成功配置接受域为内部中继域，从内部中继域发送邮件到您的 Exchange 组织的邮箱，并验证收到邮件。

