---
title: '配置在 Outlook Voice Access 用户断开连接之前登录失败的次数: Exchange Online Help'
TOCTitle: 配置在 Outlook Voice Access 用户断开连接之前登录失败的次数
ms:assetid: 02f93888-168c-44bb-8cf6-17f5fcc3d733
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423537(v=EXCHG.150)
ms:contentKeyID: 50489840
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置在 Outlook Voice Access 用户断开连接之前登录失败的次数

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-09_

可以指定断开呼叫者之前允许登录尝试连续不成功的次数。此设置的值可以介于 1 到 20 之间。此值设置得太低可能会给用户带来麻烦。对于大多数组织来说，应当将此值设置为默认的 3 次尝试。

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

## 使用 EAC 配置用户断开连接之前的登录失败次数

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在此列表视图中，选择您要修改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。

4.  在\&quot;设置\&quot;中的\&quot;断开连接前的登录失败的次数\&quot;下，输入登录失败次数。

5.  单击\&quot;保存\&quot;。

## 使用命令行配置断开用户之前登录失败的次数

此示例将一个名为 `MyUMDialPlan` 的 UM 拨号计划在断开用户之前登录失败的次数设置为 5。

    Set-UMDialPlan -identity MyUMDialPlan -LogonFailuresBeforeDisconnect 5

