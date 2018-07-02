---
title: '设置传真服务器 URI 以允许发送传真的伙伴: Exchange Online Help'
TOCTitle: 设置传真服务器 URI 以允许发送传真的伙伴
ms:assetid: 77a9013b-d76b-4af2-8b2c-cef435cf67af
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ650873(v=EXCHG.150)
ms:contentKeyID: 52061387
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 设置传真服务器 URI 以允许发送传真的伙伴

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

您可以启用和禁用入站的传真与统一消息 (UM) 邮箱策略相关联的用户。默认情况下，当用户启用了 UM，用户不能接收传真邮件，除非您启用 UM 邮箱策略上的入站传真并指定合作伙伴传真服务器的 URI。如果 Uri 在 UM 邮箱策略上配置，但在 UM 拨号计划或为单个用户禁用允许传入传真的选项，已启用 UM 的用户链接到 UM 邮箱策略仍将无法接收传真。

有关传真合作伙伴的详细信息，请参阅[Microsoft 查明其传真合作伙伴](https://go.microsoft.com/fwlink/?linkid=190238)。

有关与传真相关的更多管理任务，请参阅[传真的步骤](faxing-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

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

## 使用 EAC 设置传真合作伙伴 URI

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要修改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要修改的策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在**UM 邮箱策略**页 \>**常规**，**合作伙伴传真服务器 URI**框中，输入 TCP 或 TLS URI。例如︰ *sip:faxserver1.contoso.com:5060;transport=tcp*或*sip:faxserver2.contoso.com:5061;transport=tls*
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>虽然框中可以包含多个传真服务器 URI，将使用只有一个。如果输入两个 Uri，则将使用第一个。</td>
    </tr>
    </tbody>
    </table>


4.  单击\&quot;保存\&quot;保存更改。

## 使用命令行管理程序设置传真合作伙伴 URI

此示例允许链接到 UM 邮箱策略 `UMDialPlan Default Policy` 的用户将具有端口 5060 的 TCP 用于合作伙伴传真服务器 `faxserver1`。

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver1.contoso.com:5060;transport=tcp

此示例允许链接到 UM 邮箱策略 `UMDialPlan Default Policy` 的用户将具有端口 5061 的 TLS 用于合作伙伴传真服务器 `faxserver2`。

    Set-UMMailboxPolicy "UMDialPlan Default Policy" -FaxServerURI sip:faxserver2.contoso.com:5061;transport=tls

