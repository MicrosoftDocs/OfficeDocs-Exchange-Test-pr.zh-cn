---
title: '已定义 ExecutionPolicy GPO: Exchange 2013 Help'
TOCTitle: 已定义 ExecutionPolicy GPO
ms:assetid: 63de83e2-9a6b-4f57-85b9-df445bea18dd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.powershellexecutionpolicycheckset(v=EXCHG.150)
ms:contentKeyID: 61203676
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 已定义 ExecutionPolicy GPO

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-15_

无法继续 Microsoft Exchange Server 2013 安装程序，因为它检测到\&quot;ExecutionPolicy\&quot;组策略对象 (GPO) 定义了一个或两个以下策略：

  - **MachinePolicy**

  - **UserPolicy**

策略是如何定义的并不重要。重要的是已定义了策略。

运行 Exchange 2013 安装程序后，Exchange 将停止并禁用 Windows Management Instrumentation (WMI) 服务。如果定义了其中一个策略，则需要启用 WMI 服务以运行 Windows PowerShell 脚本。如果定义了策略并停止了 WMI 服务，则安装程序将失败，并且会将服务器置于不一致状态。

若要继续安装程序，需要暂时删除\&quot;ExecutionPolicy\&quot;GPO 中\&quot;MachinePolicy\&quot;或\&quot;UserPolicy\&quot;的所有定义。

有关如何在**ExecutionPolicy** GPO 中删除**MachinePolicy**或**UserPolicy**的任何定义的信息，请参阅[知识库文章 KB981474](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=981474)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>虽然此知识库文章是针对 Exchange 2010 撰写的，但也适用于 Exchange 2013 累积更新和 Service Pack。</td>
</tr>
</tbody>
</table>


遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

