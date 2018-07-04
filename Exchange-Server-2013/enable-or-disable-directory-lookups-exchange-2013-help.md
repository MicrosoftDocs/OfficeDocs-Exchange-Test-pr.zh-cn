---
title: '启用或禁用目录查找: Exchange Online Help'
TOCTitle: 启用或禁用目录查找
ms:assetid: c0768815-8578-4385-8d4c-7d1e40304cec
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423557(v=EXCHG.150)
ms:contentKeyID: 52061452
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁用目录查找

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-05-10_

您可以启用目录查找，以便呼叫者连接到统一消息 (UM) 自动助理可以查找中使用其电话键盘的目录的名称，但不是能使用语音输入目录中搜索。默认情况下启用此设置。如果禁用此设置，则调用方不能在目录中搜索特定人员使用按键或语音命令。

有关与 UM 自动助理相关的更多管理任务，请参阅 [UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

> [!NOTE]
> 用户不能使用自动语音识别 (ASR) 或语音输入的目录中查找用户的 Outlook Voice Access，他们只能使用 DTMF 或按键输入。


## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 启用或禁用目录查找

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择要启用或禁用目录查找的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在**UM 自动助理**页 \>**访问通讯簿和运算符**，请在**搜索通讯簿选项**中选择**允许调用方要搜索的用户的名称或别名，**以使调用方可以搜索用户旁边的复选框。若要禁用搜索用户的调用方，请清除此复选框。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序启用或禁用目录查找

此示例对名为 `MyUMAutoAttendant` 的 UM 自动助理禁用目录查找。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -NameLookupEnabled $false

