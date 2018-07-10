---
title: '更改音频编解码器: Exchange Online Help'
TOCTitle: 更改音频编解码器
ms:assetid: 139b2ccd-28c5-46c0-9050-777f4f59aade
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996342(v=EXCHG.150)
ms:contentKeyID: 50490051
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更改音频编解码器

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

统一消息可以使用四个编解码器其中之一来创建语音邮件：MP3、Windows Media Audio (WMA)、Group System Mobile (GSM) 06.10 和 G.711 Pulse Code Modulation (PCM) Linear。默认情况下，在创建统一消息 (UM) 拨号计划时，UM 拨号计划使用 MP3 音频编解码器录制语音邮件。MP3 音频格式是跨多个操作系统、电子邮件客户端和 MP3 播放器使用的常用音频格式。在创建 UM 拨号计划之后，可以将 UM 拨号计划配置为使用其他音频格式之一（包括 WMA、GSM 06.10 或 G.711 PCM Linear 音频编解码器）。若要收听语音邮件，移动电话或计算机必须安装兼容的音频软件应用程序。

有关与 UM 拨号计划相关的其他任务，请参阅[UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 可以在统一消息拨号计划上更改音频编解码器

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在此列表视图中，选择您要修改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。

4.  在\&quot;设置\&quot;中的\&quot;音频编解码器\&quot;下，使用下拉列表选择以下项目之一：
    
      - MP3
    
      - WMA
    
      - GSM
    
      - G711

5.  单击\&quot;保存\&quot;。

## 使用命令行管理程序可以在统一消息拨号计划上更改音频编码解码器

此示例在名为 `MyUMDialPlan` 的 UM 拨号计划上将音频编码解码器设置为 G.711。

    Set-UMDialPlan -Identity MyUMDialPlan -AudioCodec G711

此示例在名为 `MyUMDialPlan` 的 UM 拨号计划上将音频编码解码器设置为 WMA。

    Set-UMDialPlan -Identity MyUMDialPlan -AudioCodec Wma

