---
title: '配置工作时间: Exchange Online Help'
TOCTitle: 配置工作时间
ms:assetid: 96b4be99-af94-4fa4-959a-48413387a044
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232133(v=EXCHG.150)
ms:contentKeyID: 50491088
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置工作时间

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-19_

在营业时间配置统一邮件 (UM) 自动助理时，处于打开状态，您的组织的日期和营业时间问候语的小时数并定义菜单提示呼叫者将听到时它们调用配置自动助理是分机号。如果呼叫者是您定义工作时间之外的时间内达到自动助理，呼叫者将听到非营业时间提示和问候。

EAC 有多个默认日程安排选项。例如，大多数公司都是从上午 8:00 到下午 5:00，星期一至星期五开放。有时的默认选项不适合您的需求，您需要自定义日程安排。如果您的营业时间与由系统定义的日程安排不同，您可以定义自定义的时间表自动助理。

默认情况下，不论呼叫者每天何时呼叫 UM 自动助理，自动助理将会播放营业时间提示和问候语。

> [!NOTE]
> 设置 UM 自动助理的营业时间和非营业时间的日程安排时，请确保时区配置正确。


有关与 UM 自动助理相关的更多管理任务，请参阅 [UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 指定 UM 自动助理的营业时间

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择要为其设置的营业时间的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 自动助理\&quot;页面\>\&quot;营业时间\&quot;的\&quot;营业时间\&quot;下单击\&quot;配置营业时间\&quot;。

4.  在\&quot;配置营业时间\&quot;页上，选择要用作一周中每一天的营业时间的时间。

5.  单击\&quot;确定\&quot;，然后单击\&quot;保存\&quot;。

## 使用命令行管理程序指定 UM 自动助理的营业时间

本示例将设置名为 `MyUMAutoAttendant` 的 UM 自动助理的营业时间。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30

