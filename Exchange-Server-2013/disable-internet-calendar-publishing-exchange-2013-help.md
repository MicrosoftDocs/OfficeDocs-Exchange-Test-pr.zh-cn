---
title: '禁用 Internet 日历发布: Exchange 2013 Help'
TOCTitle: 禁用 Internet 日历发布
ms:assetid: f26dbf04-9dae-460f-a987-2ad3dfbc7b7e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ853047(v=EXCHG.150)
ms:contentKeyID: 50556698
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 禁用 Internet 日历发布

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-02-15_

Internet 日历发布的禁用方式取决于其启用方式。如果创建了专用于 Internet 日历发布的共享策略，则可将策略一起禁用或删除。如果已将 Internet 日历发布配置为默认共享策略中的一个共享规则，则只能删除\&quot;匿名\&quot;域的共享规则。

如果禁用 Internet 日历发布，则被配置为使用共享策略的用户将无法与策略中指定的\&quot;匿名\&quot;Internet 域共享日历信息。但是，在配置为使用专用于 Internet 日历发布的共享策略的所有用户将策略设置从其邮箱中删除之前，无法删除或禁用该共享策略。有关更改用户的共享策略设置的详细信息，请参阅[管理用户邮箱](manage-user-mailboxes-exchange-2013-help.md)。

> [!NOTE]  
> 如果禁用或删除共享策略，则被指定使用该策略的用户将继续共享信息，直到共享策略助理开始运行。要指定共享策略助理的运行频率，请使用带有 <em>SharingPolicySchedule</em> 参数的 <a href="https://technet.microsoft.com/zh-cn/library/aa998651(v=exchg.150)">Set-MailboxServer</a> cmdlet。


若要完全禁用 Internet 日历发布，还应禁用用于日历发布的 Outlook Web App 虚拟目录。执行此操作后，将无法访问先前由 Exchange 组织用户与外部 Internet 用户共享的发布日历链接。本主题后面将详细说明该步骤。

要了解有关 Internet Calendar Publishing 和共享策略的详细信息，请参阅[共享](sharing-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：15 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;日历和共享权限\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您该如何做？

## 步骤 1：使用 EAC 或命令行管理程序禁用或删除 Internet 日历发布的共享策略

## 使用 EAC

1.  导航到\&quot;组织\&quot; \>\&quot;分享\&quot;。

2.  在列表视图中的\&quot;单个共享\&quot;下，执行以下步骤之一：
    
      - 如果创建了一个专用于 Internet 日历发布的共享策略，请选择该策略，然后清除\&quot;开启\&quot;列中的复选框以禁用共享策略，或者单击\&quot;删除\&quot;![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标") 将其删除。
    
      - 如果已将 Internet 日历发布配置为默认共享策略中的共享规则，请执行以下步骤：
        
        1.  选择默认共享策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。
        
        2.  在\&quot;共享策略\&quot;中，选择\&quot;匿名\&quot;共享规则，然后单击\&quot;删除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标") 以删除该共享规则。
        
        3.  单击\&quot;保存\&quot;。

## 使用命令行管理程序

此示例禁用专用的 Internet 日历发布共享策略\&quot;Internet\&quot;。

    Set-SharingPolicy -Identity "Internet" -Enabled $false

此示例删除专用的 Internet 日历发布共享策略\&quot;Internet\&quot;。

    Remove-SharingPolicy -Identity "Internet"

有关语法和参数的详细信息，请参阅 [Set-SharingPolicy](https://technet.microsoft.com/zh-cn/library/dd297931\(v=exchg.150\))。

## 您如何知道此步骤有效？

若要验证是否已经成功删除或更新了共享策略，可运行以下命令行管理程序命令验证共享策略信息。

    Get-SharingPolicy <policy name> | format-list

如果删除了专用的 Internet 日历发布共享策略，则不会在 cmdlet 结果中看到该策略。

如果更新了默认的共享策略，请验证是否已从 *Domains* 参数中删除了 `Anonymous` 域。

有关语法和参数的详细信息，请参阅 [Get-SharingPolicy](https://technet.microsoft.com/zh-cn/library/dd335081\(v=exchg.150\))。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 步骤 2：使用命令行管理程序禁用 Outlook Web App 虚拟目录\&quot;匿名\&quot;功能

> [!NOTE]  
> 不能使用 EAC 禁用 Outlook Web App 虚拟目录的&amp;quot;匿名&amp;quot;功能。


此示例在客户端访问服务器 CAS01 上禁用 Outlook Web App 虚拟目录的\&quot;匿名\&quot;功能。

    Set-OwaVirtualDirectory -Identity "CAS01" - AnonymousFeaturesEnabled -$false

有关语法和参数的详细信息，请参阅 [Set-OwaVirtualDirectory](https://technet.microsoft.com/zh-cn/library/bb123515\(v=exchg.150\))。

## 您如何知道此步骤有效？

若要验证是否在客户端访问服务器上成功地禁用了 Outlook Web App 虚拟目录的\&quot;匿名\&quot;功能，请运行以下命令行管理程序命令以验证 *AnonymousFeaturesEnabled* 参数值是否为 `$false`。

    Get-OwaVirtualDirectory | format-list

有关语法和参数的详细信息，请参阅 [Get-OwaVirtualDirectory](https://technet.microsoft.com/zh-cn/library/aa998588\(v=exchg.150\))。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

