---
title: '启用信息通知: Exchange Online Help'
TOCTitle: 启用信息通知
ms:assetid: 07f6c13e-3781-4127-9321-f0f85f054259
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb266918(v=EXCHG.150)
ms:contentKeyID: 50556519
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用信息通知

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-19_

可以对统一消息 (UM) 自动助理启用信息通知。如果启用了信息通知，它会在营业时间或非营业时间问候语之后立即播放。默认情况下，没有配置信息通知。若要启用信息通知，请创建一个 .wav 或 .wma 文件作为信息通知，然后配置自动助理使用该声音文件。

关于 UM 自动助理的更多管理任务，请参阅[UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 创建一个要用于信息通知的 .wav 或 .wma 文件。

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

## 使用 EAC 启用信息通知

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择要为其启用信息通知的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 自动助理\&quot;页面\>\&quot;问候语\&quot;的\&quot;信息通知\&quot;下，单击\&quot;更改\&quot;，然后单击\&quot;浏览\&quot;，找到在启动此过程之前创建的信息通知文件。
    
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

## 使用命令行管理程序启用信息通知

本示例为名为 `MyUMAutoAttendant` 的 UM 自动助理启用使用 `MyInfoAnnouncement.wav` 文件的信息通知。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -InfoAnnouncementEnabled $true -InfoAnnouncementFilename MyInfoAnnouncement.wav

