---
title: '禁用或启用 Exchange 搜索: Exchange 2013 Help'
TOCTitle: 禁用或启用 Exchange 搜索
ms:assetid: 195b25be-53fb-4215-90a5-04340d640bcc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996416(v=EXCHG.150)
ms:contentKeyID: 52061484
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 禁用或启用 Exchange 搜索

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-05-07_

默认情况下，对所有新邮箱数据库启用 Exchange 搜索，不要求附加配置。但是，如果要使 Exchange 搜索停止为邮箱内容编制索引，可以对单个邮箱数据库或整个邮箱服务器禁用 Exchange 搜索。

> [!CAUTION]  
> 禁用 Exchange 搜索会影响用户以联机模式使用 Outlook 或在 Windows Mobile 设备上所执行全文搜索的功能和性能。
> <a href="in-place-ediscovery-exchange-2013-help.md">就地电子数据展示</a> 也依赖于 Exchange 搜索。如果对某个邮箱数据库或邮箱服务器禁用 Exchange 搜索，则就地电子数据展示搜索将不会从该数据库或服务器返回任何邮件。


有关与 Exchange 搜索相关的其他管理任务，请参阅 [Exchange 搜索过程](exchange-search-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：1 分钟

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 可以对服务器或邮箱数据库启用或禁用 Exchange 搜索，但不能对单个邮箱用户启用或禁用该搜索。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 您想执行什么操作？

## 对邮箱数据库禁用或启用 Exchange 搜索

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“Exchange 搜索”条目。

> [!NOTE]  
> 不能使用 EAC 为邮箱数据库禁用或启用 Exchange 搜索。


此命令对名为 EXCH01 的邮箱数据库禁用 Exchange 搜索。

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $false

此命令对名为 EXCH01 的邮箱数据库启用 Exchange 搜索。

    Set-MailboxDatabase "Mailbox Database (EXCH01)" -IndexEnabled $true

有关语法和参数的详细信息，请参阅[Set-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb123971\(v=exchg.150\))。

## 对邮箱服务器禁用或启用 Exchange 搜索

要对邮箱服务器禁用 Exchange 搜索，您必须禁用和停止 Microsoft Exchange 搜索服务。同样，要对邮箱服务器启用 Exchange 搜索，您必须启用和启动 Microsoft Exchange 搜索服务。可以使用服务控制台或命令行管理程序执行该操作。

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“管理邮箱服务器上的 Exchange 搜索服务”条目。

**使用服务控制台**

1.  转到“开始”\>“管理工具”\>“服务”。

2.  在“服务”详细信息窗格中，右键单击“Microsoft Exchange 搜索”服务，然后选择“属性”。

3.  在“<strong>常规”</strong>选项卡上的<strong>“启动类型”</strong>列表中，选择<strong>“已禁用”</strong>以禁用该服务，或选择<strong>“自动”</strong>以自动启动它。
    
    > [!NOTE]  
    > 启动类型会在下次重新启动服务器后尝试启动服务时或手动启动服务时影响服务。在下一步中，服务将手动停止或启动。


4.  单击<strong>“停止”</strong>以停止该服务，或单击<strong>“启动”</strong>以启动该服务。

5.  单击“确定”保存更改。

**使用命令行管理程序**

运行下列命令停止并禁用 Microsoft Exchange 搜索服务。

```
    Stop-Service MSExchangeFastSearch
```
```
    Set-Service MSExchangeFastSearch -StartupType Disabled
```

运行下列命令将 Exchange 搜索服务配置为自动启动，然后启动该服务。

```
    Set-Service MSExchangeFastSearch -StartupType Automatic
```
```
    Start-Service MSExchangeFastSearch
```
