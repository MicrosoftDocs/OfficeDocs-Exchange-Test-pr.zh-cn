---
title: '还原到默认配置的详细信息模板: Exchange 2013 Help'
TOCTitle: 还原到默认配置的详细信息模板
ms:assetid: 84c5f49b-614d-4f0e-8701-0979a2eb90bf
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232102(v=EXCHG.150)
ms:contentKeyID: 50490964
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 还原到默认配置的详细信息模板

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-12_

详细信息模板编辑器不包含\&quot;撤消\&quot;按钮，您也不能使用键盘快捷方式撤消某个操作。若要撤消对模板进行的添加操作，您必须使用 DELETE 键。若要撤消删除操作，您必须重新应用设置。您还可以在退出详细信息模板编辑器时不保存所做更改，从而还原到初始设置。若要撤消已保存的更改，您可以还原模板。如果您还原模板，则会丢失所有自定义设置，且模板会还原至原始配置。

本主题介绍如何使用 Exchange 2013 工具箱或 Exchange 命令行管理程序将详细信息模板还原为默认配置。

要了解有关详细信息模板的详细信息，请参阅[详细信息模板](details-templates-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的\&quot;详细信息模板\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用 Exchange 工具箱将详细信息模板还原为默认配置

1.  单击\&quot;开始\&quot;\>\&quot;所有程序\&quot;\>\&quot;Microsoft Exchange Server 2013\&quot;\>\&quot;Exchange 工具箱\&quot;。

2.  在\&quot;Exchange 工具箱\&quot;中，单击\&quot;详细信息模板编辑器\&quot;，然后在操作窗格中单击\&quot;打开工具\&quot;。

3.  在\&quot;详细信息模板编辑器\&quot;的详细信息窗格中，选择要还原的模板，然后在操作窗格中单击\&quot;还原\&quot;。

4.  单击**是**以确认您要还原到其原始状态的模板。所有自定义都将丢失。

## 使用命令行管理程序将详细信息模板还原为默认配置

此示例将还原美国英语联系人详细信息模板。

```powershell
Restore-DetailsTemplate -Identity "en-US\Contact"
```

有关语法和参数的详细信息，请参阅 [Restore-DetailsTemplate](https://technet.microsoft.com/zh-cn/library/bb125188\(v=exchg.150\))。

