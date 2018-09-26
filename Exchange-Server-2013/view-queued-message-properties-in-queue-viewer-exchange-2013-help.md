---
title: '在队列查看器中查看排队邮件属性: Exchange 2013 Help'
TOCTitle: 在队列查看器中查看排队邮件属性
ms:assetid: 9d15d8b8-e061-4288-9354-df58e282fb6b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123934(v=EXCHG.150)
ms:contentKeyID: 50491152
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.Edge.SystemManager.MessagePropertyPage
ms.translationtype: MT
---

# 在队列查看器中查看排队邮件属性

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-01-17_

可以使用 Exchange 工具箱中的队列查看器来查看排队等待传递的邮件的属性。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的\&quot;队列\&quot;条目。

  - 还可以使用 Exchange 管理命令行中的 Get-Message cmdlet 查看队列查看器中不可见的其他邮件属性。有关详细信息，请参阅 [邮件筛选器](message-filters-exchange-2013-help.md) 和 [使用 Exchange 命令行管理程序管理队列](use-the-exchange-management-shell-to-manage-queues-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 Exchange 工具箱中的队列查看器查看邮件的属性

1.  单击\&quot;开始\&quot;\>\&quot;所有程序\&quot;\>\&quot;Microsoft Exchange 2013\&quot;\>\&quot;Exchange 工具箱\&quot;。

2.  在\&quot;邮件流工具\&quot;部分，双击\&quot;队列查看器\&quot;，可以在新窗口中打开该工具。

3.  在\&quot;队列查看器\&quot;中，选择\&quot;邮件\&quot;选项卡可以看见组织中当前正在排队等待传递的邮件的列表。

4.  右键单击要查看其属性的邮件，然后选择\&quot;属性\&quot;。

5.  \&quot;常规\&quot;选项卡显示有关邮件的以下详细信息：
    
      - **标识**   此字段显示表示特定邮件的整数。邮件被接收以待处理时，队列数据库将分配邮件标识。你可包括一个可选服务器和队列标识来标识该邮件的唯一实例。
    
      - **主题**   此字段显示以文本字符串形式表示的邮件主题。此值是从 `Subject:` 头字段获取的。
    
      - **Internet 邮件 ID**   此字段显示 `MessageID:` 标头字段的值。该属性值以 GUID 形式表示，后跟发送服务器的 SMTP 地址，如下例所示：67D754D6103DC4FB3BA6BC7205DACABA61231@exchange.contoso.com
    
      - **发件人地址**   此字段显示邮件发件人的 SMTP 地址。可从邮件信封中的 MAIL FROM: 获取此值。
    
      - **状态**：此字段显示当前邮件状态。邮件可以具有下列状态值之一：
        
          - **活动**   如果邮件在传递队列中，则此邮件正准备传递到目标。如果邮件在提交队列中，则此邮件正在由分类程序进行处理。
        
          - **暂停删除**   邮件虽被管理员删除，但已在传递中。如果邮件传递出现错误，从而导致此邮件重新进入队列，则该邮件将被删除。否则，邮件传递将继续进行。
        
          - **暂停挂起**   邮件虽被管理员挂起，但已在传递中。如果邮件传递出现错误，从而导致此邮件重新进入队列，则该邮件将被挂起。否则，邮件传递将继续进行。
        
          - **就绪**   邮件正在队列中等待进行处理。
        
          - **重试**   邮件所在队列进行的上一次连接尝试失败。邮件正在等待下一次队列重试。
        
          - **挂起**   邮件由管理员挂起。
    
      - **大小(KB)**：此字段显示舍入到最接近的 KB 的邮件大小。
    
      - **邮件源名称**：此字段显示将此邮件提交到队列的组件的名称。
    
      - **源 IP**：此字段显示将邮件提交到 Exchange 组织的外部服务器的 IP 地址。
    
      - **SCL**   此字段显示邮件的垃圾邮件可信度 (SCL) 分级。有效的 SCL 条目是从 0 到 9 的整数或 -1。空 SCL 条目表示邮件尚未经过内容筛选器代理处理。
    
      - **接收日期**：此字段显示存放邮件所在队列的服务器接收邮件时的日期时间。
    
      - **过期时间**：此字段显示当邮件无法传递而使邮件过期并将从队列中删除时的日期和时间。
    
      - **上一错误**：此字段显示为邮件记录的上一个错误。
    
      - **队列 ID**   此字段显示存放邮件的队列的标识。队列标识以 *Server\\destination* 的形式表示，其中 *destination* 是传递组、路由目标、永久队列名或列队数据库标识符。队列数据库标识符以整数形式表示，可通过查看邮件属性来确定。
    
      - **收件人**：此字段显示向其发送邮件的收件人的列表。
    
      - **重试次数**：此字段显示尝试将邮件传递到目标的次数。

6.  \&quot;收件人信息\&quot;选项卡显示有关邮件收件人的以下信息：
    
      - **地址**   此字段显示邮件收件人的 SMTP 地址。此值是从邮件信封中的 `RCPT TO:` 获取的。
    
      - **状态**：此字段显示当前邮件状态。邮件可以具有下列状态值之一：
        
          - **活动**   如果邮件在传递队列中，则此邮件正准备传递到目标。如果邮件在提交队列中，则此邮件正在由分类程序进行处理。
        
          - **暂停删除**   邮件虽已被管理员删除，但已在传递中。如果邮件传递出现错误，从而导致此邮件重新进入队列，则该邮件将被删除。否则，邮件传递将继续进行。
        
          - **暂停挂起**   邮件虽已被管理员挂起，但已在传递中。如果邮件传递出现错误，从而导致此邮件重新进入队列，则该邮件将被挂起。否则，邮件传递将继续进行。
        
          - **就绪**   邮件正在队列中等待进行处理。
        
          - **重试**   邮件所在队列进行的上一次连接尝试失败。邮件正在等待下一次队列重试。
        
          - **已搁置**   邮件已被管理员挂起。
    
      - **上一错误**：此字段显示为邮件记录的上一个错误。

## 使用命令行管理程序查看邮件的属性

可以使用 **Get-Message** cmdlet 查看当前正在排队等待传递的邮件的属性。以下示例将当前处于重试状态的所有邮件的发件人地址、收件人、主题和接收日期信息制成表格：

```powershell
    Get-Message -IncludeRecipientInfo -Filter {Status -eq "Retry"} | Format-Table FromAddress,Recipients,Subject,DateReceived
```

有关语法和参数的详细信息，请参阅[Get-Message](https://technet.microsoft.com/zh-cn/library/bb124738\(v=exchg.150\))。

