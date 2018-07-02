---
title: '选择的语言的自动助理: Exchange Online Help'
TOCTitle: 选择的语言的自动助理
ms:assetid: 3a1c1ec0-c726-41fb-a294-59faab205609
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997306(v=EXCHG.150)
ms:contentKeyID: 50556565
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 选择的语言的自动助理

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2016-12-09_

您可以配置默认提示语言设置统一邮件 (UM) 自动助理。在 UM 自动助理设置可用的语言使您能够配置默认提示语言上的自动助理。当您使用默认系统提示的自动助理时，这是调用方时自动助理应答传入的呼叫会听到的语言。这个语言设置影响仅在安装了邮箱服务器运行 Microsoft Exchange 统一消息服务之后提供了默认系统提示。此设置不会影响自动助理配置的自定义提示。可用的语言基于邮箱服务器安装了统一消息语言包。

您创建的每个自动助理最初将为默认语言使用英语 (EN-US)。英语 (EN-US) 语言包安装默认情况下，所有版本的Microsoft交换 2013年上，不能删除。如果您想要选择其他语言，例如，德语 (DE-DE)，您必须首先下载从[Exchange Server 2013 UM 语言包](https://go.microsoft.com/fwlink/?linkid=266542) UM 德语语言包.exe 文件并使用 UMLanguagePack.de de.exe 安装文件在邮箱服务器上安装 UM 语言包。已安装 UM 语言包后，您可以设置默认语言为 UM 自动助理的语言不是英语 (EN-US)。

有关与 UM 语言相关的其他任务，请参阅 [UM 语言、 提示和问候过程](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用 EAC 配置默认语言设置

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在列表视图中，选择要修改 UM 拨号计划，然后在工具栏上单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择要更改的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  在\&quot;常规\&quot;页面的\&quot;自动语音界面的语言\&quot;下，从下拉列表中选择所需的语言。

5.  单击\&quot;保存\&quot;接受更改。

## 使用命令行管理程序配置默认语言设置

此示例将 UM 自动助理 `MyUMAutoAttendant` 的默认语言设置为英语（英国）。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language en-GB

此示例将 UM 自动助理 `MyUMAutoAttendant` 的默认语言设置为德语。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language de-DE

