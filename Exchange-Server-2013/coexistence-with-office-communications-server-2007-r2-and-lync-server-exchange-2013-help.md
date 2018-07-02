---
title: '与 Office Communications Server 2007 R2 和 Lync Server 共存: Exchange 2013 Help'
TOCTitle: 与 Office Communications Server 2007 R2 和 Lync Server 共存
ms:assetid: f12d65c7-0b2c-46a1-a14a-802a76296fa1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ851069(v=EXCHG.150)
ms:contentKeyID: 50556684
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 与 Office Communications Server 2007 R2 和 Lync Server 共存

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2015-03-09_

Communications Server 2007 R2 和 Lync Server 提供了许多最终用户功能，其中包括即时消息 (IM)、状态和 多方 IM；它们的语音邮件功能可以与 Exchange 统一消息 (UM) 集成。对于集成 Lync Server 2010 或 2013 的部署，可以为用户启用 Enterprise Voice，使启用了语音邮件的用户可以通过使用 Lync Server 组件访问其语音邮件。

将 UM 与更早版本的 Office Communications Server 或 Lync Server 集成时，并非所有功能都可用。对于充分利用新增的最终用户增强功能（如高分辨率照片、统一的联系人存储库和 Lync Archiving Integration 等）的用户，他们必须在 Lync Server 2013 和 Exchange Server 2013 有用户帐户，并且必须使用最新版本的 Lync 2013 客户端软件。例如，已在 Lync Server 2010 上启用企业语音的用户无法使用统一联系人存储。此外，Lync 2010 中也无法显示高分辨率照片。

在将 Exchange UM 与 Office Communications Server 2007 R2 或 Lync Server 2010 集成时，可能需要在组织中已部署的 Office Communications Server 2007 R2 或 Lync 2010 服务器上安装额外的修补程序、修补程序汇总、累积更新和 Service Pack。需要安装的内容取决于您的部署拓扑以及要与 Exchange UM 集成的产品版本。

## 需要的修补程序、修补程序汇总、累积更新和 Service Pack

下表展示了与 UM 集成的每个产品版本所需的修补程序。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>Office Communications Server 2007 R2 累积更新 10 或更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2010</p></td>
<td><p>Lync Server 2010 累积更新 3 或更高版本。</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p>不需要更新。</p></td>
</tr>
</tbody>
</table>

