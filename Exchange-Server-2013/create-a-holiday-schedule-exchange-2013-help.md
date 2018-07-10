---
title: '创建假日日程安排: Exchange Online Help'
TOCTitle: 创建假日日程安排
ms:assetid: 0c5c51e4-5b51-451b-ab93-2cebf644dc96
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb266921(v=EXCHG.150)
ms:contentKeyID: 50489979
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 创建假日日程安排

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-19_

可以定义在假日以及其他情况下，您的组织停止营业的日期和时间。在指定的开始日期与结束日期之间，接通统一消息 (UM) 自动助理的呼叫者将听到您在配置假日日程安排时指定的假日问候语。呼叫者听到您指定的假日问候语之后，系统将向呼叫者播放非营业时间问候语和菜单提示。

您还可以在现有假日日程安排内创建假日日程安排。创建多个假日日程安排时，统一消息将允许您重叠所安排的假日时间。例如，可以在组织由于施工而停止营业时，定义一个自 12 月 15 日到 12 月 31 日的假日日程安排，同时可以定义另一个自 12 月 24 日到 12 月 26 日的假日日程安排。如果呼叫者在 12 月 15 日到 12 月 23 日以及 12 月 27 日到 12 月 31 日之间呼叫自动助理，系统将为呼叫者播放您为此日程安排指定的假日问候语。例如：\&quot;我们目前由于施工而停止营业\&quot;。如果呼叫者在 12 月 24 日到 12 月 26 日之间呼叫自动助理，系统将为呼叫者播放另一条假日问候语，例如\&quot;我们目前停止营业，使员工可以与家人共度假日\&quot;。

有关与 UM 自动助理相关的更多管理任务，请参阅 [UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 为 UM 自动助理指定假日日程安排

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在列表视图中，选择要更改的 UM 拨号计划，然后在工具栏上单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面上，在\&quot;UM 自动助理\&quot;下，选择要为其设置假日日程安排的 UM 自动助理。在工具栏上，单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 自动助理\&quot;页面 \>\&quot;营业时间\&quot;中的\&quot;假日日程安排\&quot;下，单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在\&quot;新建假日\&quot;页面上配置以下属性：
    
      - **名称**   输入假日日程安排的名称。
    
      - **假日问候语**   浏览到用作问候语的 .wav 文件。这是必填字段。
    
      - **开始日期**   使用此列表可以选择假日开始的日期。假日日程安排将在此列表指定日期的午夜开始。
    
      - **结束日期**   使用此列表可以选择假日结束的日期。假日日程安排将在此列表指定日期的晚上 11:59 结束。

5.  在配置了假日日程安排之后，单击\&quot;确定\&quot;，然后单击\&quot;保存\&quot;。

## 使用命令行管理程序为 UM 自动助理指定假日日程安排

本示例将配置名为 `MyUMAutoAttendant` 的 UM 自动助理，其营业时间配置为 10:45 到 13:15（星期日）、09:00 到 17:00（星期一）、09:00 到 16:30（星期六）和假日时间，而其关联问候语配置为\&quot;New Year\&quot;（2013 年 1 月 2 日）和\&quot;Building Closed for Construction\&quot;（从 2013 年 4 月 24 日到 2013 年 4 月 28 日）。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

