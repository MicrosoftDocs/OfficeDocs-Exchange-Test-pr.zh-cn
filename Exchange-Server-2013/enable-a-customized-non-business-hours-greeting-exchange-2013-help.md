---
title: '启用自定义非-营业时间问候语: Exchange Online Help'
TOCTitle: 启用自定义非-营业时间问候语
ms:assetid: d4743805-bab0-4735-a1e0-2cea4e088e8c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232183(v=EXCHG.150)
ms:contentKeyID: 50556678
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用自定义非-营业时间问候语

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-30_

您可以启用自定义非-营业时间问候语的统一邮件 (UM) 自动助理。非-营业时间问候语是第一件事呼叫者将听到时 UM 自动助理应答的呼叫在非业务时间。您可能需要自定义问候语。

统一的消息包括默认系统的提示使用在非业务时间。尽管默认的系统提示不能替换或更改，您可以提供自定义的问候。以.wav 或.wma 文件格式，用于呼叫连接到 UM 自动助理在非业务时间内，您可以创建自定义的问候。例如，"您已经达到 Woodgrove Bank 后小时。"

如果您想要包括的组织或作为默认问候语的一部分的企业名称，可以在**公司名称**框中输入名称，UM 自动助理。有关详细信息，请参阅[输入公司名称](enter-a-business-name-exchange-2013-help.md)。

有关与 UM 自动助理相关的更多管理任务，请参阅 [UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 创建要用于问候语的 .wav 或 .wma 文件。

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

## EAC 用于启用自定义非-营业时间问候语

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在**UM 拨号计划**页的**UM 自动助理**下,，选择为其您想要启用自定义非-营业时间问候语，并单击**编辑**![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")UM 自动助理。

3.  在**UM 自动助理**页面上，\>**问候**下**非营业时间问候语**，单击**更改**，然后单击**浏览**以查找自定义非工作时间问候语开始此过程之前创建的文件。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>用于问候语的文件必须是 .wav 或 .wma 文件。</td>
    </tr>
    </tbody>
    </table>


4.  在找到该文件后，请单击\&quot;打开\&quot;，然后再单击\&quot;保存\&quot;。

## 使用外壳程序启用自定义非-营业时间问候语

本示例启用非营业时间问候使用 UM 自动助理`MyUMAutoAttendant`名为`GreetingFile.wav`的自定义的问候语。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AfterHoursWelcomeGreetingEnabled $true -AfterHoursWelcomeGreetingFilename GreetingFile.wav

此示例将配置名为 `MyUMAutoAttendant` 的 UM 自动助理，其营业时间配置为 10:45 到 13:15（星期日）、09:00 到 17:00（星期一）、09:00 到 16:30（星期六）和假日时间，而其关联问候语配置为\&quot;`New Year`\&quot;（2013 年 1 月 2 日）和\&quot;`Building Closed for Construction`\&quot;（从 2013 年 4 月 24 日到 2013 年 4 月 28日）。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

本示例将名为`MyAutoAttendant` UM 自动助理配置和启用非营业时间键映射，以便调用方按 1，它们正在转发到另一个名为`SalesAutoAttendant`的 UM 自动助理。当他们请按 2 时，它们正在转发到的`Support`，分机号 12345，当他们请按 3，它们被发送到另一个播放音频文件的自动助理。

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

