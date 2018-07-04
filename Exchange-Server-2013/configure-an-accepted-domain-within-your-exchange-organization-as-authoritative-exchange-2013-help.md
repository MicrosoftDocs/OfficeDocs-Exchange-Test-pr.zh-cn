---
title: '配置贵 Exchange 组织内的接受域为权威: Exchange 2013 Help'
TOCTitle: 配置贵 Exchange 组织内的接受域为权威
ms:assetid: e182d54f-e58a-47ba-a5c1-28c0dfa86eed
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657734(v=EXCHG.150)
ms:contentKeyID: 50491824
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置贵 Exchange 组织内的接受域为权威

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-02-17_

如果属于您组织的某个域托管 SMTP 命名空间中所有收件人的邮箱，将把该域视为权威域。默认情况下，配置一个接受域为 Exchange 组织的权威域。如果您的组织有多个 SMTP 命名空间，可配置多个接受域为权威域。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“接受域”条目。

  - 如果您已在外围网络中订阅了边缘传输服务器，请在 Exchange 组织中的邮箱服务器上配置接受的域。在 EdgeSync 同步期间，接受的域配置会复制到边缘传输服务器。有关详细信息，请参阅[边缘订阅](edge-subscriptions-exchange-2013-help.md)。

  - 要创建的接受域的名称不能与已配置的远程域的名称相同。例如，如果已将 fabrikam.com 配置为远程域，则不能创建名称为 fabrikam.com 的接受域。

  - 配置接受域之前，必须验证该 SMTP 命名空间的公用域名系统 (DNS) MX 资源记录存在，并且该 MX 资源记录引用了与 Exchange 组织关联的服务器名称和 IP 地址。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用 EAC 将接受域配置为权威域

如果您 Exchange 组织的接受域托管该域 SMTP 命名空间内所有收件人的邮箱，则可能需要将其配置为权威域。

1.  在 EAC 中，导航到“邮件流”\>“接受域”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“名称”字段中，输入接受域的显示名称。您组织的每个接受域都必须有一个唯一的显示名称，该名称可能与接受域不同。例如，域 contoso.com 可以拥有 Contoso Local Accepted Domain 的显示名称。

3.  在“接受域”字段中，输入接受域。指定您的组织为其接受电子邮件的 SMTP 命名空间。（例如，Contoso.com）。

4.  选择“权威域”。该选项用于为接受域在您的 Exchange 组织中中继到服务器的电子邮件，该接受域托管 SMTP 命名空间中所有收件人的邮箱。

5.  单击“保存”。

> [!tip]
> 要配置已创建的接受域，从接受域列表中选择域，并单击“编辑”<img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="编辑图标" alt="编辑图标" />。您可以将多个域配置为权威域。


## 您如何知道这有效？

您的新接受域将出现在 EAC 中的接受域列表中。要验证是否已成功将接受域配置为权威域，可发送电子邮件至域并验证是否收到电子邮件。

