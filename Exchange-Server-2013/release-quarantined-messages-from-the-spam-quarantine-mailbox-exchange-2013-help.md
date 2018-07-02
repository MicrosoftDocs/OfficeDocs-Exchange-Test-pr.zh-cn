---
title: '从垃圾邮件隔离邮箱中释放隔离的邮件: Exchange 2013 Help'
TOCTitle: 从垃圾邮件隔离邮箱中释放隔离的邮件
ms:assetid: 7a86bfde-f868-4689-bdec-5f01e52b510d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998920(v=EXCHG.150)
ms:contentKeyID: 50490975
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 从垃圾邮件隔离邮箱中释放隔离的邮件

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

可以使用 Microsoft Outlook 从垃圾邮件隔离邮箱恢复隔离邮件。

垃圾邮件隔离是内容筛选器代理的一项功能，可以减小丢失合法邮件的风险。邮件达到垃圾邮件隔离阈值时，将封装在未送达报告 (NDR) 中并传递到垃圾邮件隔离邮箱。有关垃圾邮件隔离功能的详细信息，请参阅[垃圾邮件隔离](spam-quarantine-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的\&quot;邮箱访问\&quot;条目。

  - 此过程要求配置了反垃圾邮件隔离邮箱。有关详细信息，请参阅[配置垃圾邮件隔离邮箱](configure-a-spam-quarantine-mailbox-exchange-2013-help.md)。

  - 若要访问隔离邮箱，您需要配置该邮箱的 Outlook 配置文件，然后打开使用 Outlook 邮箱。有关配置和使用多个 Outlook 配置文件的详细信息，请参阅[概述的 Outlook 电子邮件配置文件](https://go.microsoft.com/fwlink/p/?linkid=178975)。

  - 为便于查找要恢复的邮件，可以创建一个自定义 Outlook 表单并修改默认视图以便在邮件列表中公开原始发件人地址。有关详细步骤，请参阅[将 Outlook 配置为显示隔离邮箱中的原始发件人](configure-outlook-to-show-the-original-sender-in-the-quarantine-mailbox-exchange-2013-help.md)。

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

## 使用 Outlook 2010 或 Outlook 2013 从垃圾邮件隔离邮箱中释放邮件

1.  在客户端计算机上使用 Outlook 2010 或 Outlook 2013 打开隔离邮箱。

2.  在\&quot;邮件\&quot;视图中，在\&quot;收件箱\&quot;中查找要恢复的邮件，然后双击该邮件将其打开。

3.  在功能区的\&quot;移动\&quot;部分，单击\&quot;操作\&quot;\>\&quot;重新发送此邮件\&quot;。

4.  邮件打开后，单击\&quot;发送\&quot;，将邮件重新发送给所需的收件人。

## 使用 Outlook 2007 从垃圾邮件隔离邮箱释放邮件

1.  在客户端计算机上使用 Outlook 2007 打开隔离邮箱。

2.  在\&quot;邮件文件夹\&quot;视图中，在\&quot;收件箱\&quot;中查找要恢复的邮件，然后双击该邮件将其打开。

3.  在\&quot;报告\&quot;选项卡的\&quot;答复\&quot;组中，单击\&quot;重新发送\&quot;。

4.  邮件打开后，单击\&quot;发送\&quot;，将邮件重新发送给所需的收件人。

## 您如何知道这有效？

要验证您是否已成功从垃圾邮件隔离邮箱中释放邮件，请与收件人联系并确认他们收到了邮件。

