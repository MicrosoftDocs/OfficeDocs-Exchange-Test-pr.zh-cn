---
title: '配置就地存档（内部部署）的存档配额: Exchange 2013 Help'
TOCTitle: 配置就地存档（内部部署）的存档配额
ms:assetid: f10e77c7-e1d4-415a-bef9-cb3f00e74c34
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee633489(v=EXCHG.150)
ms:contentKeyID: 50556697
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置就地存档（内部部署）的存档配额

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-12-04_

在内部部署中，默认情况下使用无限存储配额创建就地存档。 因此，需要编辑邮箱的属性以设置存档的存储配额。可以设置以下存档配额：

  - **存档警告配额**   当就地存档超出指定的存档警告配额时，系统会记录一个事件供 Exchange 管理员使用，并向邮箱用户发送警告消息。

  - **存档配额**   当就地存档超出指定的存档配额时，不会再将邮件移动到存档，并向邮箱用户发送警告消息。

有关就地存档的详细信息，请参阅[Exchange 2013 中的就地存档](in-place-archiving-in-exchange-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 在 Exchange 管理中心 (EAC) 中，可以使用包含固定值的下拉列表配置存档配额和存档警告配额。 如果要将配额设置为未在 EAC 中列出的值，请使用命令行管理程序。

  - 将存档警告配额设置为一个小于存档配额的值。 根据用户的存档增长速度，存档警告配额与存档配额之间的差异应留出足够的时间让用户采用恰当的措施，例如从存档中删除项目或者请求管理员或 IT 技术支持人员提高存档配额。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 为邮箱配置存档配额和存档警告配额

1.  导航到“收件人”\>“邮箱”

2.  在列表视图中，选择一个邮箱。

3.  在详细信息窗格中的“就地存档”下，单击“查看详情”。

4.  在“存档邮箱”中，使用“配额值(GB)”和“达到该限度时发出警告(GB)”列表选择所需的值。

5.  单击“确定”。

## 使用命令行管理程序为邮箱配置存档配额和存档警告配额

此示例将 Chris Ashton 的邮箱存档配额设置为 10 GB；达到该大小时，用户会收到指示就地存档已满的警告消息，并且无法再将邮件移到该存档。 此示例还将存档警告配额设置为 9.5 GB，达到该大小时，用户会收到就地存档将满的警告消息。

```powershell
Set-Mailbox -Identity "Chris Ashton" -ArchiveQuota 10GB -ArchiveWarningQuota 9.5GB
```

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否对现有邮箱成功启用了内部部署，可执行以下操作之一：

  - 在 EAC 中，导航到“收件人”\>“邮箱”，然后选择所需的邮箱。 在详细信息窗格中的“就地存档”下，单击“查看详情”，然后验证存档的配额设置。

  - 在命令行管理程序中，运行以下命令可显示有关存档的配额信息。
    
        Get-Mailbox <Name> | FL Name,Archive*Quota

