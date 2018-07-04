---
title: '为拥有相似姓名的用户配置拨号计划: Exchange Online Help'
TOCTitle: 为拥有相似姓名的用户配置拨号计划
ms:assetid: 14783f45-95f5-49de-8215-0a3aef7dc034
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb266943(v=EXCHG.150)
ms:contentKeyID: 51408197
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 为拥有相似姓名的用户配置拨号计划

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-21_

您可以配置统一消息 (UM) 拨号计划，以指定当用户拥有相同或相似姓名时为呼叫者提供的信息。UM 使用此设置区分拥有相同或相似姓名的用户，并将此信息提供给呼叫者。当系统提示呼叫者或 Outlook Voice Access 用户输入字母以查找特定用户时，有时会有多个名称与呼叫者的输入匹配。可以使用一种可用的选项向呼叫者提供详细信息，以帮助呼叫者找到其尝试联系的用户。

您可以在 UM 拨号计划和 UM 自动助理上设置此设置。当创建 UM 自动助理时，它将继承与自动助理关联的拨号计划的设置。默认情况下，不会为拨号计划配置此设置，所以不会为呼叫者提供其他信息以帮助他们找到正确的用户。

> [!NOTE]
> 对于为了让拥有相似姓名的用户能正常工作而包含的信息，您必须为您 Microsoft Exchange 组织中的收件人提供职务、部门和位置信息。


有关与 UM 拨号计划相关的其他管理任务，请参阅 [UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 为姓名相似的用户配置 UM 拨号计划

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面中，单击\&quot;配置\&quot;\>\&quot;传输和搜索\&quot;，在\&quot;为姓名相同的用户包含的信息\&quot;，选择以下选项之一：
    
      - **职务**   当找到两个或更多姓名相似的用户时，拨号计划会包含每个用户的职务。
    
      - **部门**   当找到两个或更多姓名相似的用户时，拨号计划会包含每个用户的部门。
    
      - **位置**   当找到两个或更多姓名相似的用户时，拨号计划会包含每个用户的位置。
    
      - **无**   当用户拥有相似姓名时，拨号计划不会包含任何其他信息。尽管这是默认设置，我们建议您为呼叫者包含可用选项之一。如果不这样做，呼叫者将无法区分两个或更多姓名相似用户之间的区别。
    
      - **提示输入别名**   拨号计划将提示呼叫者输入用户的别名。别名是用户电子邮件或 SMTP 地址中在 (@) 符号之前的部分。

3.  单击\&quot;保存\&quot;。

## 使用命令行管理程序为姓名相似的用户配置 UM 拨号计划

本示例在名为 `MyDialPlan` 的 UM 拨号计划上将为姓名相似用户包含的信息设置为\&quot;提示输入用户别名\&quot;。

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod PromptForAlias

本示例在名为 `MyDialPlan` 的 UM 拨号计划上将为姓名相似用户包含的信息设置为\&quot;部门\&quot;。

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod Department

本示例在名为 `MyDialPlan` 的 UM 拨号计划上将为姓名相似用户包含的信息设置为\&quot;位置\&quot;。

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod Location

