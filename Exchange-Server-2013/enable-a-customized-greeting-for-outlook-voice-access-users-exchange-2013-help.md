---
title: '启用 Outlook Voice Access 用户自定义的问候语: Exchange Online Help'
TOCTitle: 启用 Outlook Voice Access 用户自定义的问候语
ms:assetid: abd418ec-2c65-4720-859d-c11a2698dc06
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124125(v=EXCHG.150)
ms:contentKeyID: 50556635
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用 Outlook Voice Access 用户自定义的问候语

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

默认情况下，每个统一邮件 (UM) 拨号计划欢迎问候语，它已向呼叫者播放，包括Outlook拨入到已配置一个 Outlook Voice Access 数字语音访问用户使用标准的.wav 文件。但是，您可以创建的欢迎问候语的.wav 或.wma 文件，然后在 UM 拨号计划上启用它。

例如，您可能需要更改默认欢迎问候语，改为提供特定于您的公司，如"欢迎Outlook Woodgrove Bank 语音访问。"欢迎问候语若要执行此操作，您记录的自定义欢迎问候语，并将其保存为.wav 或.wma 文件。然后您可以配置拨号计划，可以自定义欢迎问候语。

有关可用的Outlook语音访问用户菜单选项的详细信息，请参阅Outlook语音访问快速参考指南可从[Microsoft 下载中心获取](https://go.microsoft.com/fwlink/p/?linkid=272767)。

有关与 UM 拨号计划相关的其他管理任务，请参阅[UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

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

## 使用 EAC 启用自定义欢迎问候语

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在此列表视图中，选择您要修改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。

4.  在\&quot;Outlook Voice Access\&quot;中的\&quot;欢迎问候语\&quot;下，单击\&quot;更改\&quot;，然后单击\&quot;浏览\&quot;查找问候语文件。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>用于欢迎问候语的文件必须是 .wav 文件或 .wma 文件。</td>
    </tr>
    </tbody>
    </table>


5.  在找到该文件后，单击\&quot;打开\&quot;，然后再单击\&quot;保存\&quot;。

## 使用命令行管理程序启用自定义欢迎问候语

此示例在名为 `MyUMDialPlan` 的 UM 拨号计划中启用使用 C:\\UMPrompts\\welcome.wav 文件的欢迎问候语。

    Set-UMDialPlan -Identity MyUMDialPlan -WelcomeGreetingEnabled $true -WelcomeGreetingFilename c:\UMPrompts\welcome.wav

