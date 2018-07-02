---
title: '创建公用文件夹邮箱: Exchange 2013 Help'
TOCTitle: 创建公用文件夹邮箱
ms:assetid: 64437ffd-231b-4c10-84df-232ccbe9538f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ552410(v=EXCHG.150)
ms:contentKeyID: 50490744
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建公用文件夹邮箱

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2014-10-23_

必须先创建公用文件夹邮箱，然后才能创建公用文件夹。公用文件夹邮箱包含公用文件夹的层次结构信息和内容。您创建的首个公用文件夹邮箱是主层次结构邮箱，包含层次结构的只写拷贝。您创建的其他所有公用文件夹邮箱都是辅邮箱，包含层次结构的只读拷贝。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有关存储配额和公用文件夹的限制的详细信息，请参阅以下主题：
<ul>
<li><p>若要了解 Office 365 中的公用文件夹，请参阅 <a href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online 限制</a>。</p></li>
<li><p>有关本地 Exchange Server 2013 中的公用文件夹的信息，请参阅<a href="limits-for-public-folders-exchange-2013-help.md">公用文件夹的限制</a>。</p></li>
</ul></td>
</tr>
</tbody>
</table>


有关 Exchange 2013 中与公用文件夹相关的其他管理任务，请参阅[公用文件夹程序](public-folder-procedures-exchange-2013-help.md)。

有关 Exchange Online 中与公用文件夹相关的其他管理任务，请参阅 [Office 365 和 Exchange Online 中的公用文件夹程序](https://technet.microsoft.com/zh-cn/library/jj966272\(v=exchg.150\))。

## 在开始之前，您需要知道什么？

  - 估计完成时间：不超过 5 分钟。

  - Exchange 2013 公用文件夹和旧版 Exchange 服务器上的公用文件夹不会存在于同一组织中。当您仍具有旧版公用文件夹时，如果您尝试创建公用文件夹，则将收到错误“检测到已部署现有公用文件夹”**。要迁移现有的公用文件夹数据，则 使用 -HoldForMigration 开关来新建公用文件夹。**
    
    要在 Exchange 2013 中创建公用文件夹，您需要将旧版公用文件夹迁移到 Exchange 2013。为此，请遵循[使用串行迁移将公用文件夹从以前版本迁移到 Exchange 2013](https://technet.microsoft.com/zh-cn/library/jj150486\(v=exchg.150\))中的步骤。这些步骤将向您介绍如何创建可用于存储您迁移的公用文件夹的公用文件夹邮箱。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[共享和协作权限](sharing-and-collaboration-permissions-exchange-2013-help.md)主题中的“公用文件夹”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您想执行什么操作？

## 使用 EAC 创建公用文件夹邮箱

1.  导航到“公用文件夹”\>“公用文件夹邮箱”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“公用文件夹邮箱”中，为此公用文件夹邮箱提供名称。

3.  单击“保存”。

## 使用命令行管理程序创建公用文件夹邮箱

此示例将创建主公用文件夹邮箱。

    New-Mailbox -PublicFolder -Name MasterHierarchy

此示例将创建辅助公用文件夹邮箱。创建主层次结构邮箱与辅助层次结构邮箱之间的唯一差异在于，主邮箱是组织中创建的第一个邮箱。可以创建其他公用文件夹邮箱来实现负载平衡。

    New-Mailbox -PublicFolder -Name Istanbul 

有关语法和参数的详细信息，请参阅 [New-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997663\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否成功创建了主公用文件夹邮箱，可运行以下命令行管理程序命令：

    Get-OrganizationConfig | Format-List RootPublicFolderMailbox

有关语法和参数的详细信息，请参阅 [Get-OrganizationConfig](https://technet.microsoft.com/zh-cn/library/aa997571\(v=exchg.150\))。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

