---
title: '启用自定义的工作时间内菜单提示: Exchange Online Help'
TOCTitle: 启用自定义的工作时间内菜单提示
ms:assetid: 89053e84-3490-4dc6-ade3-9b6c5dbf4020
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232116(v=EXCHG.150)
ms:contentKeyID: 50556612
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用自定义的工作时间内菜单提示

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-19_

您可以自定义菜单提示，在工作时间内由统一消息 (UM) 自动助理。创建 UM 自动助理后，默认的系统提示 （"欢迎到统一消息"） 用作后营业时间播放欢迎问候语是呼叫者将听到菜单提示。虽然系统提示不能替换或更改，可以自定义问候语和菜单提示使用的 UM 自动助理。创建自定义的工作时间内菜单提示音频文件后，必须启用 UM 自动助理的菜单导航项的营业时间。

如果只希望将组织或公司的名称包括在默认系统提示中，则可在 UM 自动助理上的\&quot;公司名称\&quot;框中输入该名称。有关详细信息，请参阅[输入公司名称](enter-a-business-name-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您必须配置自动助理的营业时间。有关详细信息，请参阅<a href="configure-business-hours-exchange-2013-help.md">配置工作时间</a>。</td>
</tr>
</tbody>
</table>


关于 UM 自动助理的更多管理任务，请参阅[UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 创建要用于菜单提示的 .wav 或 .wma 文件。

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

## 使用 EAC 启用自定义的营业时间菜单提示

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择要为其启用自定义营业时间菜单提示的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 自动助理\&quot;页面 \>\&quot;菜单导航\&quot;上的\&quot;营业时间菜单导航\&quot;下，单击\&quot;更改\&quot;，然后单击\&quot;浏览\&quot;找到自定义的营业时间菜单提示文件。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>用于菜单提示的文件必须是 .wav 文件或 .wma 文件。</td>
    </tr>
    </tbody>
    </table>


4.  在找到该文件后，单击\&quot;打开\&quot;，然后再单击\&quot;保存\&quot;。

## 使用命令行管理程序启用自定义的营业时间菜单提示

此示例在 UM 自动助理 `businesshoursprompts.wav` 上启用营业时间主菜单提示并使用名为 `MyUMAutoAttendant` 的自定义提示。

    Command Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursMainMenuCustomPromptEnabled $true -BusinessHoursMainMenuCustomPromptFilename BusinessHoursPrompts.wav

此示例将配置名为 `MyUMAutoAttendant` 的 UM 自动助理，其营业时间配置为 10:45 到 13:15（星期日）、09:00 到 17:00（星期一）、09:00 到 16:30（星期六）和假日时间，而其关联问候语配置为\&quot;`New Year`\&quot;（2013 年 1 月 2 日）和\&quot;`Building Closed for Construction`\&quot;（从 2013 年 4 月 24 日到 2013 年 4 月 28日）。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

本示例配置 UM 自动助理，名为`MyAutoAttendant` ，使营业时间导航菜单，以便调用方按 1，它们正在转发到另一个名为`SalesAutoAttendant`的 UM 自动助理。当他们请按 2 时，它们正在转发到的`Support`，分机号 12345，当他们请按 3，它们被发送到另一个播放音频文件的自动助理。

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

