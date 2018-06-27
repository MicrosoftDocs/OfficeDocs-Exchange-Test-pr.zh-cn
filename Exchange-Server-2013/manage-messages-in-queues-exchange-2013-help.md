---
title: '管理队列中的邮件: Exchange 2013 Help'
TOCTitle: 管理队列中的邮件
ms:assetid: 83358884-6036-4e91-87a8-35200541874d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123535(v=EXCHG.150)
ms:contentKeyID: 51408246
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理队列中的邮件

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2014-05-07_

在 Microsoft Exchange Server 2013 中，可以使用 Exchange 工具箱中的队列查看器或 Exchange 命令行管理程序来管理队列中的邮件。有关在 Exchange 命令行管理程序中使用邮件管理 cmdlet 的详细信息，请参阅[使用 Exchange 命令行管理程序管理队列](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的\&quot;队列\&quot;条目。

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

## 从队列中删除邮件

发送给多个收件人的邮件可能位于多个队列中。若要通过一个操作从多个队列中删除邮件，需要使用筛选器。从队列中删除邮件时，可以选择是否发送未送达报告 (NDR)。不能从提交队列中删除邮件。

## 使用 Exchange 工具箱中的队列查看器删除邮件

1.  单击\&quot;开始\&quot;\>\&quot;所有程序\&quot;\>\&quot;Microsoft Exchange 2013\&quot;\>\&quot;Exchange 工具箱\&quot;。

2.  在\&quot;邮件流工具\&quot;部分，双击\&quot;队列查看器\&quot;，可以在新窗口中打开该工具。

3.  在队列查看器中，单击\&quot;邮件\&quot;选项卡。此时将显示您所连接的服务器上所有邮件的列表。若要将操作调整为针对单个队列执行，请单击\&quot;队列\&quot;选项卡，双击队列名，然后单击所显示的 *Server\\Queue* 选项卡。

4.  从列表中选择一个或多个邮件，单击鼠标右键，然后选择\&quot;删除邮件(发送 NDR)\&quot;或\&quot;删除邮件(不发送 NDR)\&quot;。此时将出现一个对话框，确认所选操作并显示\&quot;是否要继续?\&quot;。单击\&quot;是\&quot;。

5.  若要删除特定队列中的所有邮件，请单击\&quot;队列\&quot;选项卡。选择一个队列，单击鼠标右键，然后选择\&quot;删除邮件(发送 NDR)\&quot;或\&quot;删除邮件(不发送 NDR)\&quot;。此时将出现一个对话框，确认所选操作并显示\&quot;是否要继续?\&quot;。单击\&quot;是\&quot;。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果使用已筛选的列表，则显示的页可能不包含筛选器中的所有项目。在这种情况下，将出现一个显示以下内容的提示：<strong>此操作将影响此页上的所有项目。若要扩展此操作的作用域以包含此筛选器中的所有项目，请选中以下复选框，然后单击&amp;quot;确定&amp;quot;。</strong></td>
    </tr>
    </tbody>
    </table>


## 使用命令行管理程序删除邮件

若要删除邮件，请使用以下语法。

    Remove-Message <-Identity MessageIdentity | -Filter {MessageFilter}> -WithNDR <$true | $false>

此示例删除队列中主题为\&quot;Win Big\&quot;的邮件且不发送 NDR。

    Remove-Message -Filter {Subject -eq "Win Big"} -WithNDR $false

此示例从名为 Mailbox01 的服务器上无法访问的队列中删除邮件 ID 为 3 的邮件，并发送 NDR。

    Remove-Message -Identity Mailbox01\Unreachable\3 -WithNDR $true

## 您如何知道操作成功？

要验证是否已从队列中成功删除了邮件，请执行以下操作之一：

  - 在队列查看器中，选择队列，或者创建筛选器以验证邮件不再存在。

  - 使用带有 *Queue* 或 *Filter* 参数的 **Get-Message** cmdlet 验证邮件不再存在。有关详细信息，请参阅 [Get-Message](https://technet.microsoft.com/zh-cn/library/bb124738\(v=exchg.150\))。

## 在队列中恢复邮件

可以恢复当前处于\&quot;已挂起\&quot;状态的邮件。恢复邮件之后，便可传递邮件。如果恢复位于病毒邮件队列中的邮件，则会将邮件发送到分类程序以进行处理。发送给多个收件人的邮件可位于多个队列中。若要在一次操作中恢复多个队列中的邮件，必须使用筛选器。

## 使用 Exchange 工具箱中的队列查看器恢复邮件

1.  单击\&quot;开始\&quot;\>\&quot;所有程序\&quot;\>\&quot;Microsoft Exchange 2013\&quot;\>\&quot;Exchange 工具箱\&quot;。

2.  在\&quot;邮件流工具\&quot;部分，双击\&quot;队列查看器\&quot;，可以在新窗口中打开该工具。

3.  在队列查看器中，单击\&quot;邮件\&quot;选项卡。此时将显示您所连接的服务器上所有邮件的列表。若要将操作调整为针对单个队列执行，请单击\&quot;队列\&quot;选项卡，双击队列名，然后单击所显示的 *Server\\Queue* 选项卡。

4.  单击\&quot;创建筛选器\&quot;，然后按如下方式输入筛选器表达式：
    
    1.  从邮件属性下拉列表中选择\&quot;状态\&quot;。
    
    2.  从比较运算符下拉列表中选择\&quot;等于\&quot;。
    
    3.  从值下拉列表中选择\&quot;已挂起\&quot;。

5.  单击\&quot;应用筛选器\&quot;。将显示所有处于\&quot;已挂起\&quot;状态的邮件。

6.  从列表中选择一个或多个邮件，单击鼠标右键，然后选择\&quot;恢复\&quot;。

## 使用命令行管理程序恢复邮件

若要恢复邮件，请使用以下语法：

    Resume-Message <-Identity MessageIdentity | -Filter {MessageFilter}>

本示例将恢复 Contoso.com 域中从任意发件人发送的所有邮件。

    Resume-Message -Filter {FromAddress -eq "*contoso.com"}

本示例将恢复服务器 Hub01 上无法访问的队列中邮件 ID 为 3 的邮件。

    Resume-Message -Identity Hub01\Unreachable\3

要从带毒邮件队列重新提交邮件，请执行下列步骤：

## 您如何知道操作成功？

要验证是否已在队列中成功恢复邮件，请执行以下操作之一：

  - 在队列查看器中，选择队列，或者创建筛选器以验证邮件不再挂起。

  - 使用带有 *Queue* 或 *Filter* 参数的 **Get-Message** cmdlet 验证邮件不再挂起。有关详细信息，请参阅 [Get-Message](https://technet.microsoft.com/zh-cn/library/bb124738\(v=exchg.150\))。

请注意，如果在服务器上的任何队列中找不到该邮件，则可能表明该邮件已成功传递到下一个跃点。

## 在队列中挂起邮件

当挂起邮件时，将阻止邮件的传递。出现在队列中但已经处于传递过程中的邮件不会被挂起。传递将继续，并且邮件状态将是 **PendingSuspend**。如果传递失败，则邮件会重新进入队列，然后该邮件将被挂起。无法挂起\&quot;提交\&quot;队列或\&quot;带毒邮件\&quot;队列中的邮件。

发送给多个收件人的邮件可位于多个队列中。若要通过一个操作挂起多个队列中的邮件，需要使用筛选器。

## 使用 Exchange 工具箱中的队列查看器挂起邮件

1.  单击\&quot;开始\&quot;\>\&quot;所有程序\&quot;\>\&quot;Microsoft Exchange 2013\&quot;\>\&quot;Exchange 工具箱\&quot;。

2.  在\&quot;邮件流工具\&quot;部分，双击\&quot;队列查看器\&quot;，可以在新窗口中打开该工具。

3.  在队列查看器中，单击\&quot;邮件\&quot;选项卡。此时将显示您所连接的服务器上所有邮件的列表。若要限制单个队列的视图，请单击\&quot;队列\&quot;选项卡，双击队列名称，再单击出现的*\&quot;服务器\\队列\&quot;*选项卡。

4.  选择一个或多个邮件，右键单击，然后选择\&quot;挂起\&quot;。

## 使用命令行管理程序挂起邮件

若要挂起邮件，请使用以下语法：

    Suspend-Message <-Identity MessageIdentity | -Filter {MessageFilter}>

此示例挂起队列中所有来自域 contoso.com 中所有发件人的邮件。

    Suspend-Message -Filter {FromAddress -eq "*contoso.com"}

此示例挂起名为 Mailbox01 的服务器上无法访问的队列中邮件 ID 为 3 的邮件：

    Suspend-Message -Identity Mailbox01\Unreachable\3

## 您如何知道操作成功？

要验证是否已在队列中成功挂起邮件，请执行以下操作之一：

  - 在队列查看器中，选择队列，或者创建筛选器以验证邮件已挂起。

  - 使用带有 *Queue* 或 *Filter* 参数的 **Get-Message** cmdlet 验证邮件已挂起。有关详细信息，请参阅 [Get-Message](https://technet.microsoft.com/zh-cn/library/bb124738\(v=exchg.150\))。

