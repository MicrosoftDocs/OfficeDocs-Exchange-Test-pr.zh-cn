---
title: '启用自定义非营业时间菜单提示: Exchange Online Help'
TOCTitle: 启用自定义非营业时间菜单提示
ms:assetid: 094c50b2-072b-4929-aaf8-f7db5b19e9b6
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb266919(v=EXCHG.150)
ms:contentKeyID: 50556520
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用自定义非营业时间菜单提示

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-03-22_

您可以自定义统一消息 (UM) 自动助理在营业时间之外要使用的菜单提示。创建 UM 自动助理之后，系统将使用默认系统提示（\&quot;欢迎使用统一消息\&quot;）作为呼叫者在播放非营业时间欢迎问候语之后听到的菜单提示。尽管不得替换或更改系统提示语，但您可以自定义用于 UM 自动助理的问候语和菜单提示。创建自定义的非营业时间菜单提示音频文件之后，必须在 UM 自动助理中为非营业时间启用菜单导航条目。

如果只希望将组织或公司的名称包括在默认系统提示中，则可在 UM 自动助理上的\&quot;公司名称\&quot;框中输入该名称。有关详细信息，请参阅[输入公司名称](enter-a-business-name-exchange-2013-help.md)。

> [!important]
> 必须在自动助理中配置营业时间。配置营业时间之后，系统将自动设置非营业时间。有关详细信息，请参阅<a href="configure-business-hours-exchange-2013-help.md">配置工作时间</a>。


关于 UM 自动助理的更多管理任务，请参阅[UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 创建一个要用于菜单提示的 .wav 或 .wma 文件。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 启用自定义的非营业时间菜单提示

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择要为其启用自定义非营业时间菜单提示的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 自动助理\&quot;页面 \>\&quot;菜单导航\&quot;的\&quot;非营业时间菜单导航\&quot;下，单击\&quot;更改\&quot;，然后单击\&quot;浏览\&quot;，以找到自定义的非营业时间菜单提示文件。
    
    > [!important]
    > 用于菜单提示的文件必须是 .wav 或 .wma 文件。


4.  在找到该文件后，请单击\&quot;打开\&quot;，然后再单击\&quot;保存\&quot;。

## 使用命令行管理程序启用自定义的非营业时间菜单提示

本示例将启用名为 `MyUMAutoAttendant` 的 UM 自动助理，其营业时间配置为 10:45 到 13:15（星期日）、09:00 到 17:00（星期一）、09:00 到 16:30（星期六）和假日时间，而其关联问候语配置为\&quot;`New Year`\&quot;（2013 年 1 月 1 日）和\&quot;`Building Closed for Construction`\&quot;（从 2013 年 4 月 24 日 到 2013 年 4 月 28日）。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

本示例将配置名为 `MyAutoAttendant` 的 UM 自动助理，并启用非营业时间导航菜单，以便在呼叫者按 1 时，他们会转到另一个名为 `SalesAutoAttendant` 的 UM 自动助理。当呼叫者按 2 时，他们会转到分机号码 12345 以获得 `Support`，在按 3 时，他们会发送到另一个播放音频文件的 UM 自动助理。

    Set-UMAutoAttendant -Identity MyAutoAttendant - 
    AfterHoursKeyMappingEnabled $true -
    AfterHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

