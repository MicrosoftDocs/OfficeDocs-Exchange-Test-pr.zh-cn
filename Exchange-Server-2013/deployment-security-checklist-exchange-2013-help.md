---
title: '部署安全性核对清单: Exchange 2013 Help'
TOCTitle: 部署安全性核对清单
ms:assetid: 0cbfad59-f503-48a0-8184-6ca999d89e61
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996026(v=EXCHG.150)
ms:contentKeyID: 50489980
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 部署安全性核对清单

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

Microsoft Exchange Server 2013 功能旨在帮助提高您的邮件环境的安全性。通常，对于 Exchange 2013，以下条件成立：

  - Exchange 2013 所使用的帐户具有执行给定任务集所需的最低权限。

  - 默认情况下，仅当需要时才会启动服务。

  - Exchange 对象的访问控制列表 (ACL) 权限被最小化。

  - 管理权限是根据在对象上进行指定修改所需的更改范围进行设置的。

  - 默认情况下，所有内部默认邮件路径都会被加密。

本主题列出了一些步骤，建议您在安装 Microsoft Exchange 之前，执行这些步骤以强化邮件环境。建议您在每次安装新的 Exchange 服务器角色时参考此检查表。

在安装 Exchange 2013 之前，请执行下列步骤。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>步骤</th>
<th>完成？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>运行 <a href="https://go.microsoft.com/fwlink/p/?linkid=54836">Microsoft Update</a>。</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>运行 MicrosoftWindows 恶意软件删除工具。恶意软件删除工具包含在 Microsoft Update 中。有关该工具的详细信息，请参阅<a href="http://go.microsoft.com/fwlink/p/?linkid=73452">恶意软件删除工具</a>。</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>运行 <a href="https://go.microsoft.com/fwlink/p/?linkid=16526">Microsoft Baseline Security Analyzer</a>。</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

