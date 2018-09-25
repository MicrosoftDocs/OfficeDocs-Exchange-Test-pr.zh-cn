---
title: '将 Lync 对话和会议内容存档到 Exchange 中: Exchange 2013 Help'
TOCTitle: 将 Lync 对话和会议内容存档到 Exchange 中
ms:assetid: 3cff970e-e5ed-4a54-88e6-3665d84b5ed7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn508399(v=EXCHG.150)
ms:contentKeyID: 59678851
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 将 Lync 对话和会议内容存档到 Exchange 中

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

你可以将 Lync Online 内容（如 IM 对话）存档到 Exchange Online 中的用户邮箱。在本地部署中，可以将 Lync 2013 内容存档到 Exchange 2013 邮箱。在联机和本地环境中，此操作需要对用户邮箱设置诉讼保留或就地保留。当邮箱处于保留状态的的用户永久删除 Lync 内容时，已存档的 Lync 内容将保留在用户邮箱的“可恢复的项目”文件夹中。虽然这些内容对用户不可见，但会包含在电子数据展示搜索中。

将邮箱置于诉讼保留时，将保留所有内容类型（包括 Lync 项目）。默认情况下，创建就地保留时也是如此。但是，如果想使用就地保留来仅保留 Lync 项目，请使用“**就地电子数据展示和保留**”向导中的“**选择邮件类型**”选项，然后选择“**Lync 项目**”，如下面的屏幕截图所示。

![将 Lync 项目置于保留状态](images/Dn508399.691d2324-9fac-4689-8527-c78d387e0e3e(EXCHG.150).jpg "将 Lync 项目置于保留状态")

> [!NOTE]  
> 还可以配置就地保留以排除 Lync 项目。例如，相对于其他内容类型，组织可能更倾向于在短时间内保留即时消息和语音邮件项目。若要实施此类保留策略，可创建就地保留以长时间保留内容（例如 7 年），并将 Lync 项目从此保留中排除。然后，可创建保留时间更短且仅保留 Lync 项目的其他就地保留。用户还可以指定内容的保留时间。有关创建具有特定持续时间的保留的详细信息，请参阅<a href="https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/in-place-and-litigation-holds">就地保留和诉讼保留</a>。


有关将用户置于保留状态的分步说明，请参阅以下主题：

  - [创建或删除就地保留](https://technet.microsoft.com/zh-cn/library/dd979797(v=exchg.150))

  - [将邮箱放到诉讼保留中](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

有关与存档相关的其他管理任务，请参阅：

  - [在 Exchange Online 中启用或禁用存档邮箱](https://technet.microsoft.com/zh-cn/library/jj984357\(v=exchg.150\))

  - [在 Exchange 2013 中管理就地存档](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

## 更多信息

  - Lync 内容的存档发生在服务器上，无论用户是否将 Lync 客户端配置为[将 Lync IM 对话保存在“对话历史记录”文件夹中](https://go.microsoft.com/fwlink/p/?linkid=400589)。

  - 将用户置于诉讼保留或就地保留后开始存档 Lync 内容。若要确保从用户帐户创建后就开始存档用户的 Lync 通信内容，请在帐户创建成功之后立即将其置于保留状态。

此外，在本地 Exchange 2013 和 Lync 2013 部署中：

  - 您必须在 Lync 2013 和 Exchange 2013 之间配置 OAuth 身份验证。有关详细信息，请参阅[与 SharePoint 和 Lync 的集成](integration-with-sharepoint-and-lync-exchange-2013-help.md)。

  - 你还可以将 Lync 2013 内容存档到 Exchange 2013，无论是否将用户置于保留状态。为此，请配置用户的 Exchange 存档策略。使用 Lync 2013 服务器上的 `Set-CsUser` cmdlet 将 Lync 用户的 *ExchangeArchivingPolicy* 属性设置为 `ArchivingToExchange`。

  - 若要详细了解如何在本地部署中存档 Lync 内容，请参阅 Lync 2013 文档中的[规划存档](https://go.microsoft.com/fwlink/p/?linkid=400590)。

