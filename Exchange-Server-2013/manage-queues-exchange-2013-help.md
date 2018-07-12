---
title: '管理队列: Exchange 2013 Help'
TOCTitle: 管理队列
ms:assetid: 37f11378-a884-4aff-ab55-689f40a46321
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997263(v=EXCHG.150)
ms:contentKeyID: 51408214
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理队列

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-01-31_

在 Microsoft Exchange Server 2013 中，您可以使用 Exchange 工具箱中的队列查看器或 Exchange 命令行管理程序来管理队列。有关在 Exchange 命令行管理程序中使用队列管理 cmdlet 的详细信息，请参阅[使用 Exchange 命令行管理程序管理队列](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的\&quot;队列\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 查看队列

## 使用 Exchange 工具箱中的队列查看器查看队列

1.  单击\&quot;开始\&quot;\>\&quot;所有程序\&quot;\>\&quot;Microsoft Exchange 2013\&quot;\>\&quot;Exchange 工具箱\&quot;。

2.  在\&quot;邮件流工具\&quot;部分，双击\&quot;队列查看器\&quot;，可以在新窗口中打开该工具。

3.  在队列查看器中，单击\&quot;队列\&quot;选项卡。此时将显示您所连接的服务器上所有队列的列表。

4.  可以使用操作窗格中的\&quot;导出列表\&quot;链接导出队列的列表。有关详细信息，请参阅[从队列查看器中导出列表](export-lists-from-queue-viewer-exchange-2013-help.md)。

## 使用命令行管理程序查看队列

若要查看队列，请使用以下语法。

    Get-Queue [-Filter <Filter> -Server <ServerIdentity> -Include <Internal | External | Empty | DeliveryType> -Exclude <Internal | External | Empty | DeliveryType>]

此示例显示了位于 Mailbox01 Exchange 2013 邮箱服务器上的所有非空队列的基本信息。

    Get-Queue -Server Mailbox01 -Exclude Empty

此示例显示了运行该命令的邮箱服务器上所含邮件超过 100 封的所有队列的详细信息。

    Get-Queue -Filter {MessageCount -gt 100} | Format-List

## 使用命令行管理程序查看多个 Exchange 服务器上的队列摘要信息

**Get-QueueDigest** cmdlet 提供特定作用域（例如，DAG、Active Directory 站点、服务器列表或整个 Active Directory 林）内所有服务器上队列状态的简略聚合视图。请注意，外围网络中已订阅的边缘传输服务器上的队列不包括在结果中。此外，**Get-QueueDigest** 在边缘传输服务器中可用，但结果仅限于边缘传输服务器上的队列。

> [!NOTE]  
> 默认情况下，<strong>Get-QueueDigest</strong> cmdlet 显示包含 10 封或更多邮件的传递队列，而且结果每一到两分钟更新一次。有关如何更改这些默认值的说明，请参阅 <a href="configure-get-queuedigest-exchange-2013-help.md">配置 Get-QueueDigest</a>。


若要查看多个 Exchange 服务器上的队列摘要信息，请运行以下命令：

    Get-QueueDigest <-Server <ServerIdentity1,ServerIdentity2,..> | -Dag <DagIdentity1,DagIdentity2...> | -Site <ADSiteIdentity1,ADSiteIdentity2...> | -Forest> [-Filter <Filter>]

这个示例显示了名为 FirstSite（邮件数量大于 100）的 Active Directory 站点上所有 Exchange 2013 邮箱服务器上的队列的摘要信息。

    Get-QueueDigest -Site FirstSite -Filter {MessageCount -gt 100}

这个示例显示了名为 DAG01 的数据库可用性组 (DAG)（队列状态有 **Retry** 值）上所有 Exchange 2013 邮箱服务器上的队列的摘要信息。

    Get-QueueDigest -Dag DAG01 -Filter {Status -eq "Retry"}

## 恢复队列

通过恢复队列，可以重新启动处于\&quot;已挂起\&quot;状态的队列中的传出活动。队列必须处于\&quot;已挂起\&quot;状态才能使此操作生效。恢复队列时，队列中邮件的状态不会更改。处于\&quot;已挂起\&quot;状态的邮件仍保持挂起，不会离开队列。

## 使用 Exchange 工具箱中的队列查看器恢复队列

1.  单击\&quot;开始\&quot;\>\&quot;所有程序\&quot;\>\&quot;Microsoft Exchange 2013\&quot;\>\&quot;Exchange 工具箱\&quot;。

2.  在\&quot;邮件流工具\&quot;部分，双击\&quot;队列查看器\&quot;，可以在新窗口中打开该工具。

3.  在队列查看器中，单击\&quot;队列\&quot;选项卡。此时将显示您所连接的服务器上所有队列的列表。

4.  单击\&quot;创建筛选器\&quot;，然后按如下方式输入筛选器表达式：
    
    1.  从队列属性下拉列表中选择\&quot;状态\&quot;。
    
    2.  从比较运算符下拉列表中选择\&quot;等于\&quot;。
    
    3.  从值下拉列表中选择\&quot;已挂起\&quot;。

5.  单击\&quot;应用筛选器\&quot;。将显示服务器上当前已挂起的所有队列。

6.  从列表中选择一个或多个队列，单击鼠标右键，然后选择\&quot;恢复\&quot;。

## 使用命令行管理程序恢复队列

若要恢复队列，请使用以下语法。

    Resume-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

本示例恢复本地服务器上状态为\&quot;已挂起\&quot;的所有队列。

    Resume-Queue -Filter {Status -eq "Suspended"}

本示例恢复位于 Mailbox01 服务器上的名为 contoso.com 的\&quot;已挂起\&quot;传递队列。

    Resume-Queue -Identity Mailbox01\contoso.com

## 您如何知道操作成功？

若要验证是否已成功恢复了队列，请执行以下操作：

1.  使用队列查看器或 **Get-Queue** cmdlet 查找尝试恢复的队列。

2.  验证队列 **Status** 属性是否有 `Suspended` 值。

## 重试队列

传输服务器无法连接到下一个跃点时，传递队列的状态将变为\&quot;重试\&quot;。当使用队列查看器或命令行管理程序重试传递队列时，将强制立即尝试连接并覆盖计划的下一次重试时间。如果连接未成功，则重置重试间隔计时器。传递队列必须处于\&quot;重试\&quot;状态，此操作才能生效。

## 使用 Exchange 工具箱中的队列查看器重试队列

1.  单击\&quot;开始\&quot;\>\&quot;所有程序\&quot;\>\&quot;Microsoft Exchange 2013\&quot;\>\&quot;Exchange 工具箱\&quot;。

2.  在\&quot;邮件流工具\&quot;部分，双击\&quot;队列查看器\&quot;，可以在新窗口中打开该工具。

3.  在队列查看器中，单击\&quot;队列\&quot;选项卡。此时将显示您所连接的服务器上所有队列的列表。

4.  单击\&quot;创建筛选器\&quot;，然后按如下方式输入筛选器表达式：
    
    1.  从队列属性下拉列表中选择\&quot;状态\&quot;。
    
    2.  从比较运算符下拉列表中选择\&quot;等于\&quot;。
    
    3.  从值下拉列表中选择\&quot;重试\&quot;。

5.  单击\&quot;应用筛选器\&quot;。此时显示当前状态为\&quot;重试\&quot;的所有队列。

6.  从列表中选择一个或多个队列。单击鼠标右键，然后选择\&quot;重试队列\&quot;。如果连接尝试成功，队列状态将更改为\&quot;活动\&quot;。如果无法建立任何连接，则队列将保持\&quot;重试\&quot;状态，并更新下一次重试时间。

## 使用命令行管理程序重试队列

若要重试队列，请使用以下语法。

    Retry-Queue <-Identity QueueIdentity | -Filter QueueFilter [-Server ServerIdentity]>

此示例重试本地服务器上状态为\&quot;重试\&quot;的所有队列。

    Retry-Queue -Filter {status -eq "retry"}

本示例重试了位于 Mailbox01 服务器上 `Retry` 状态下的名为 contoso.com 的队列。

    Retry-Queue -Identity Mailbox01\contoso.com

## 您如何知道操作成功？

若要验证是否已成功重试了队列，请执行以下操作：

1.  使用队列查看器或 **Get-Queue** cmdlet 查找尝试重试的队列。

2.  验证队列 **LastRetryTime** 属性是否与尝试重试队列的时间相匹配。

## 重新提交队列中的邮件

重新提交队列与重试队列相似，除了邮件会被发回提交队列以供分类程序重新处理。您可以重新提交具有以下状态的邮件：

  - 处于重试状态的传递队列。队列中的邮件不得处于\&quot;挂起\&quot;状态。

  - 在\&quot;无法到达\&quot;队列中但状态不是\&quot;已挂起\&quot;的邮件。

  - 病毒邮件队列中的邮件。

## 使用命令行管理程序重新提交邮件

若要重新提交邮件，请使用以下语法。

    Retry-Queue <-Identity QueueIdentity | -Filter {Status -eq "Retry"} -Server ServerIdentity> -Resubmit $true

此示例将重新提交位于 Mailbox01 服务器上任何传递队列中状态为\&quot;重试\&quot;的所有邮件。

    Retry-Queue -Filter {Status -eq "Retry"} -Server Mailbox01 -Resubmit $true

此示例将重新提交位于 Mailbox01 服务器上无法到达队列中的所有邮件。

    Retry-Queue -Identity Mailbox01\Unreachable -Resubmit $true

## 重新提交位于病毒邮件队列中的邮件

通过回复邮件提交病毒邮件队列中的邮件。您可以使用队列查看器或命令行管理程序重新提交病毒邮件队列中的邮件。请注意，当病毒邮件队列中有邮件时，病毒邮件队列仅在队列查看器中可见。

> [!NOTE]  
> 病毒邮件队列包含确定在服务器出现故障后对 Exchange 系统有害的邮件。可能这些邮件的内容或格式确实存在问题。或者，由于代理的编写不严谨，导致 Exchange 服务器在处理可能有害的邮件时出现故障。如果您不能确定病毒邮件队列中邮件的安全，则将邮件导出到文件以便对其进行检查。有关详细信息，请参阅<a href="export-messages-from-queues-exchange-2013-help.md">从队列导出邮件</a>。


## 使用 Exchange 工具箱中的队列查看器或重新提交病毒邮件队列中的邮件

1.  单击\&quot;开始\&quot;\>\&quot;所有程序\&quot;\>\&quot;Microsoft Exchange 2013\&quot;\>\&quot;Exchange 工具箱\&quot;。

2.  在\&quot;邮件流工具\&quot;部分，双击\&quot;队列查看器\&quot;，可以在新窗口中打开该工具。

3.  在队列查看器中，单击\&quot;队列\&quot;选项卡。此时将显示您所连接的服务器上所有队列的列表。

4.  单击病毒邮件队列。在操作窗格中，选择\&quot;查看邮件\&quot;。

5.  从列表中选择一个或多个邮件，单击鼠标右键，然后选择\&quot;恢复\&quot;。

## 使用命令行管理程序重新提交病毒邮件队列中的邮件

若要重新提交病毒邮件队列中的邮件，请执行以下步骤。

1.  通过运行以下命令查找邮件的标识。
    
        Get-Message -Queue Poison | Format-Table Identity

2.  在以下命令中使用在上一步中获得的邮件标识。
    
        Resume-Message <PoisonMessageIdentity>
    
    此示例将恢复病毒邮件队列中邮件标识值为 222 的邮件。
    
        Resume-Message 222

## 您如何知道操作成功？

若要验证您是否成功地重新提交了病毒邮件队列中的邮件，请执行以下操作：

1.  使用队列查看器或 **Get-Queue** cmdlet 查看尝试重新提交邮件的病毒邮件队列。

2.  验证邮件是否不在病毒邮件队列中了。请注意，空的病毒邮件队列不会在队列查看器或 **Get-Queue** cmdlet 中显现。因此，如果您重新提交的邮件是病毒邮件队列中的唯一邮件，并且病毒邮件队列不再可见，则说明成功重新提交了邮件。

## 挂起队列

挂起队列可以避免邮件离开队列，但是不会更改队列中邮件的状态。通过 SMTP 发送功能传递的邮件将完成操作。可以通过挂起队列来停止邮件流，然后挂起队列中的一封或多封邮件。恢复队列时，挂起的邮件不会离开队列。

可以挂起状态为\&quot;活动\&quot;或\&quot;重试\&quot;的队列。也可以挂起\&quot;无法到达\&quot;队列和\&quot;提交\&quot;队列。

如果挂起\&quot;无法到达\&quot;队列，则在恢复队列之前，传输服务器收到配置更新时，不会将邮件重新提交给分类程序。如果挂起\&quot;提交\&quot;队列，则在恢复队列之前，分类程序不会选取邮件。

## 使用 Exchange 工具箱中的队列查看器挂起队列

1.  单击\&quot;开始\&quot;\>\&quot;所有程序\&quot;\>\&quot;Microsoft Exchange 2013\&quot;\>\&quot;Exchange 工具箱\&quot;。

2.  在\&quot;邮件流工具\&quot;部分，双击\&quot;队列查看器\&quot;，可以在新窗口中打开该工具。

3.  在队列查看器中，单击\&quot;队列\&quot;选项卡。此时将显示您所连接的服务器上所有队列的列表。可以创建筛选器，以便仅显示符合特定条件的队列。

4.  选择一个或多个队列，再单击鼠标右键，然后选择\&quot;挂起\&quot;。

## 使用命令行管理程序挂起队列

若要挂起队列，请使用以下语法。

    Suspend-Queue <-Identity QueueIdentity | -Filter {QueueFilter} [-Server ServerIdentity]>

此示例将挂起本地服务器上邮件计数等于或大于 1,000 且状态为\&quot;重试\&quot;的所有队列。

    Suspend-Queue -Filter {MessageCount -ge 1000 -and Status -eq "Retry"}

本示例挂起位于 Mailbox01 服务器上的名为 contoso.com 的队列。

    Suspend-Queue -Identity Mailbox01\contoso.com

## 您如何知道操作成功？

若要验证是否已成功挂起了队列，请执行以下操作：

1.  使用队列查看器或 **Get-Queue** cmdlet 查找尝试挂起的队列。

2.  验证队列 **Status** 属性是否有 `Suspended` 值。

