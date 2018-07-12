---
title: '通过 Outlook 2016 for Mac 访问公用文件夹: Exchange Online Help'
TOCTitle: 通过 Outlook 2016 for Mac 访问公用文件夹
ms:assetid: bc9b8226-bd8b-4edc-882b-4f19cfe118eb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt788631(v=EXCHG.150)
ms:contentKeyID: 74115500
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 通过 Outlook 2016 for Mac 访问公用文件夹

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016, Office 365_

_**上一次修改主题：** 2017-05-19_

**摘要：** 最新版本的受支持的 Exchange 拓扑，允许用户使用 Outlook 2016 for Mac 访问公用文件夹。

与 Outlook 2016 年[4 月 2016年更新](https://go.microsoft.com/fwlink/?linkid=829202)的 Mac 客户端版本，[累积更新 14 (CU14)](https://go.microsoft.com/fwlink/p/?linkid=849432)的交换 2013年和[累积更新 2 (CU 2)](https://go.microsoft.com/fwlink/p/?linkid=849793)交换 2016 年，Outlook 2016 的 Mac 的用户现在可以访问更多类型的拓扑中的公用文件夹之前比。

## Outlook for Mac 限制

所有版本的 Outlook for Mac 均可访问 Exchange 公用文件夹，但直到最近，这些客户端才能在以下部署方案中访问公用文件夹：

  - **传统的公用文件夹与共存。**在 Exchange 2013 或交换 2016年服务器上用户的邮箱时，用户无法使用 Mac 的 Outlook 来访问部署在服务器运行 Exchange 2010 SP3 或更高版本的公用文件夹。其他客户端可以访问这些旧式的公用文件夹，在该方案中。

  - **混合拓扑。**基于联机 Exchange 中的邮箱与内部用户无法使用 Outlook，Mac 访问内部现代化公用文件夹。同样，Exchange 2013 或交换 2016年邮箱内部的用户不能使用 Outlook 的 Mac 访问公用文件夹在 Exchange 部署联机。

## Outlook 2016 for Mac

与 Mac，以及 Exchange 2013 的 CU14 和 CU2 交换 2016 年的 4 月 2016年更新 Outlook 2016 年，上述方案将现在用于 Outlook 2016 年 Mac 客户端。

下表总结了用户通过 Outlook 2016 for Mac 客户端尝试访问 Exchange 2013、Exchange 2016 和 Exchange Online 中公用文件夹时所支持的拓扑。

> [!NOTE]  
> 下表中显示的方案假设 Outlook 2016 for Mac 的 2016 年 4 月更新已应用于所有客户端。



<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>公用文件夹部署位置...</th>
<th>用户邮箱位于 Exchange 2010 SP3 或更高版本上</th>
<th>用户邮箱位于 Exchange 2013 CU13 或更高版本上</th>
<th>用户邮箱位于 Exchange 2016 CU2 或更高版本上</th>
<th>用户邮箱位于 Office 365/Exchange Online 上</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2010 SP3 或更高版本</p></td>
<td><p>支持</p></td>
<td><p>支持</p></td>
<td><p>支持</p></td>
<td><p>不支持</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server 2013 CU13 或更高版本</p></td>
<td><p>不支持</p></td>
<td><p>支持</p></td>
<td><p>支持</p></td>
<td><p>支持</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server 2016 CU2 或更高版本</p></td>
<td><p>不支持</p></td>
<td><p>支持</p></td>
<td><p>支持</p></td>
<td><p>支持</p></td>
</tr>
<tr class="even">
<td><p>Office 365/Exchange Online</p></td>
<td><p>不支持</p></td>
<td><p>支持</p></td>
<td><p>支持</p></td>
<td><p>支持</p></td>
</tr>
</tbody>
</table>


以下文章介绍如何通过共存或混合拓扑在 Exchange 组织中部署公用文件夹。只要 Outlook 2016 for Mac 客户端已安装 2016 年 4 月更新，就能够访问这些文章中详述的配置中的公共文件夹：

  - [配置用户邮箱位于 Exchange 2013 服务器上的旧版公用文件夹](configure-legacy-public-folders-where-user-mailboxes-are-on-exchange-2013-servers-exchange-2013-help.md)

  - [针对混合部署配置 Exchange 2013 公用文件夹](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

  - [配置 Exchange Online 公用文件夹以实现混合部署](configure-exchange-online-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)

