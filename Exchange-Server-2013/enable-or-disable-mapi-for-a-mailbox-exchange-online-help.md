---
title: '启用或禁用邮箱的 MAPI: Exchange Online Help'
TOCTitle: 启用或禁用邮箱的 MAPI
ms:assetid: c2c6718c-a2c0-4ed2-b4ed-364c3cb1f592
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124497(v=EXCHG.150)
ms:contentKeyID: 50556668
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁用邮箱的 MAPI

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2017-12-31_

您可以使用Exchange 管理中心或Exchange 命令行管理程序来启用或禁用对用户邮箱的 MAPI。当启用 MAPI 时，可以通过Outlook或其他 MAPI 的电子邮件客户端访问用户的邮箱。当禁用 MAPI 时，它无法访问Outlook或其他 MAPI 客户端。但是，邮箱将继续接收电子邮件，并假设已启用邮箱访问的那些客户端，用户可以访问该邮箱发送和接收电子邮件，使用Outlook Web App、 POP 电子邮件客户端或 IMAP 客户端。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>默认情况下，在创建用户邮箱时会启用对 Outlook Web App 以及 MAPI、POP3 和 IMAP4 电子邮件客户端的支持。</td>
</tr>
</tbody>
</table>


有关与电子邮件客户端访问邮箱相关的其他管理任务，请参阅下列主题：

  - [启用或禁用邮箱的 Outlook Web App](enable-or-disable-outlook-web-app-for-a-mailbox-exchange-2013-help.md)

  - [对用户启用或禁用 IMAP4 访问](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [对用户启用或禁用 POP3 访问](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的\&quot;客户端访问用户设置\&quot;条目。

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


## 您想执行什么操作？

## 使用 EAC 启用或禁用 MAPI

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在用户邮箱列表中，单击要启用或禁用 MAPI 的邮箱，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在邮箱属性页上，单击\&quot;邮箱功能\&quot;。

4.  在\&quot;电子邮件连接\&quot;下，执行下列操作之一。
    
      - 若要禁用 MAPI 下, **MAPI： 启用**，单击**禁用**。
        
        出现警告，询问您不确定您想要禁用 MAPI。单击**是**。
    
      - 若要在启用 MAPI， **MAPI： 禁用**，单击**启用**。

5.  单击\&quot;保存\&quot;以保存您所做的更改。

## 使用 Exchange 管理外壳程序启用或禁用 MAPI

此示例为 Ken Sanchez 的邮箱禁用 MAPI。

    Set-CASMailbox -Identity "Ken Sanchez" -MAPIEnabled $false

此示例为 Esther Valle 的邮箱启用 MAPI。

    Set-CASMailbox -Identity "Esther Valle" -MAPIEnabled $true

有关语法和参数的详细信息，请参阅 [Set-CASMailbox](https://technet.microsoft.com/zh-cn/library/bb125264\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否为用户邮箱成功启用或禁用了 MAPI，请执行下列操作之一：

  - 在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;，单击相应的邮箱，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

  - 在邮箱属性页上，单击\&quot;邮箱功能\&quot;。

  - 在\&quot;电子邮件连接\&quot;下，验证 MAPI 是处于启用状态还是禁用状态。

或

  - 在 Exchange 命令行管理程序 中运行以下命令。
    
        Get-CASMailbox <identity>
    
    如果启用 MAPI，则*MapiEnabled*属性的值是`True`。如果禁用 MAPI，则值为`False`。

