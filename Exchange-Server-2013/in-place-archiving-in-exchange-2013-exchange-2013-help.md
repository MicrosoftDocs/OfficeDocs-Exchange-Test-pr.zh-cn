---
title: 'Exchange 2013 中的就地存档: Exchange 2013 Help'
TOCTitle: Exchange 2013 中的就地存档
ms:assetid: b5e4c0e9-0558-4b90-bc12-f67adbfb59ac
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd979800(v=EXCHG.150)
ms:contentKeyID: 50491402
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 中的就地存档

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

*就地存档*有助于重新获得对组织邮件数据的控制，而无需个人存储 (.pst) 文件，并且允许用户在可通过 MicrosoftOutlook 2010 及更高版本和 Microsoft OfficeOutlook Web App 访问的“存档邮箱”中存储邮件。

在 Microsoft Exchange Server 2013 中，就地存档向用户提供了一个存储历史邮件数据的备用存储位置。就位存档是对邮箱用户启用的其他邮箱（称为存档邮箱）。Outlook 2007 及更高版本和 Outlook Web App 用户可以无缝访问其存档邮箱。通过使用其中任意一个客户端应用程序，用户可以查看存档邮箱，并在其主邮箱和存档邮箱之间移动或复制邮件。就地存档向用户提供一致的邮件数据视图，省去了管理 .pst 文件所需的用户开销。

可以在用户的主邮箱所处的相同邮箱数据库、相同邮箱服务器上的其他邮箱数据库或相同 Active Directory 站点的其他邮箱服务器上的邮箱数据库上设置该用户的存档。在 Exchange 2010 和更高版本的混合部署中，还可以为位于本地邮箱服务器上的邮箱设置基于云的存档。

**目录**

邮件数据和 .pst 文件

对存档邮箱进行客户端访问

委派访问

将邮件移动到存档邮箱

存档和保留策略

默认 MRM 策略

存档配额

就地档案和其他 Exchange 功能

管理存档邮箱

## 邮件数据和 .pst 文件

Outlook 使用 .pst 文件将数据存储在用户计算机本地或网络共享中。与脱机存储 (.ost) 文件（由处于缓存 Exchange 模式的 Outlook 用来存储邮箱副本以便脱机访问）不同，.pst 文件与用户的 Exchange 邮箱不同步。如果用户将邮件移动到 .pst 文件，这些邮件将从邮箱中删除。

使用 .pst 文件管理邮件数据可能会导致以下问题：

  - **非托管文件**   通常 .pst 文件由用户创建，并驻留在用户计算机或网络共享中。它们不由组织管理。因此，用户可以创建若干包含相同或不同邮件的 .pst 文件，并将其存储在不同位置，而不受组织控制。

  - **发现成本增加**   诉讼以及某些业务或法规要求有时会产生发现请求。查找驻留在用户计算机上的 .pst 文件中的邮件数据可能会非常消耗人力。因为跟踪非托管 .pst 文件可能很困难，所以在很多情况下可能无法发现 .pst 数据。这可能会使组织面临法律和财务风险。

  - **无法应用邮件保留策略**   邮件保留策略无法应用于 .pst 文件中的邮件。因此，组织可能不符合业务规定或适用法规。

  - **数据失窃风险**   存储在 .pst 文件中的邮件数据容易受到数据窃贼的攻击。例如，.pst 文件通常存储在便携式设备（例如便携式计算机、可移动硬盘驱动器）和便携式媒体（例如 USB 驱动器、CD 和 DVD）中。

  - **邮件数据的分段视图**   将信息存储在 .pst 文件中的用户不会获得其数据的统一视图。存储在 .pst 文件中的邮件通常仅在 .pst 文件所在的计算机上可用。因此，如果用户使用其他计算机上的 Outlook Web App 或 Outlook 访问其邮箱，则无法访问存储在其 .pst 文件中的邮件。

## 对存档邮箱进行客户端访问

下表列出了可用于访问存档邮箱的客户端应用程序。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端</th>
<th>访问存档邮箱</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013、Outlook 2010、Outlook 2007 和 Outlook Web App</p></td>
<td><p>是。Outlook 2013、Outlook 2010、Outlook 2007 和 Outlook Web App 用户可以将其主邮箱中的项目复制或移动到其存档邮箱，还可以使用保留策略将项目移动到存档。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Outlook 2010 及更高版本和 Outlook 2007 用户还可以将 .pst 文件中的项目复制或移动到其存档邮箱。Outlook 2007 用户需要 2011 年 2 月的 Office 2007 累计更新。Outlook 2010 及更高版本和 Outlook 2007 对存档支持存在一些差异。有关详细信息，请参阅 Exchange 工作组日志文章，<a href="https://blogs.technet.com/b/exchange/archive/2010/12/20/3411710.aspx">是的，在弗吉尼亚，Outlook 2007 中存在 Exchange 2010 存档支持</a>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>就地存档是一项高级功能，要求使用 Exchange 企业客户端访问许可证 (CAL)。有关如何对 Exchange 进行许可的详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/?linkid=237292">Exchange Server 许可</a>。有关访问存档邮箱所需的 Outlook 版本的详细信息，请参阅<a href="https://go.microsoft.com/fwlink/?linkid=237276">个人存档和保留策略的许可要求</a>。</td>
</tr>
</tbody>
</table>


Outlook 不会在用户的计算机上创建存档邮箱的本地副本，即使其被配置为使用缓存 Exchange 模式也是如此。用户只能在联机模式下访问存档邮箱。

## 委派访问

“委派访问”是指用户或用户组被赋予对其他用户的邮箱的访问权时所进行的访问。有几种提供委派访问的情况，其中包括：

  - 为一个或多个用户提供对已不再受组织雇佣用户的邮箱的访问权。在这种情况下，可能会被赋予委派访问权的用户包括离职用户的经理或主管，或者将承担离职用户职责的另一位用户。

  - 为一个或多个用户提供对共享邮箱的访问权。

  - 为行政助理提供对其所协助的高级管理人员的邮箱的访问权。

在 Exchange 2013 中，为邮箱分配“完全访问”权限后，您向其分配此权限的代理人还可以访问该用户的存档。代理人必须使用 Outlook 来访问邮箱，而且他们必须连接到 Exchange 2010 SP1 或更高版本的客户端访问服务器才能实现自动发现目的。自动发现是一项 Exchange 服务，提供用于自动配置 Outlook 客户端的配置设置。当代理人使用 Outlook 访问 Exchange 2013 邮箱时，可以在 Outlook 中看到其有权访问的主邮箱和存档。

## 将邮件移动到存档邮箱

可以通过多种方式将邮件移动到存档邮箱：

  - **手动移动或复制邮件**   邮箱用户可以手动将邮件从其主邮箱或 .pst 文件移动或复制到其存档邮箱。存档邮箱在 Outlook 和 Outlook Web App 中显示为其他邮箱或 .pst 文件。

  - **使用收件箱规则移动或复制邮件**   邮箱用户可以在 Outlook 或 Outlook Web App 中创建收件箱规则，以便将邮件自动移动到其存档邮箱中的文件夹。若要了解更多信息，请参阅[了解收件规则](http://help.outlook.com/zh-cn/140/bb899620.aspx)。

  - **使用保留策略移动邮件**   可以使用保留策略自动将邮件移动到存档。用户还可以应用个人标记来将邮件移动到存档。有关存档和保留策略的详细信息，请参阅本主题后面的存档和保留策略。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>个人标记仅可用于 Outlook Web App 以及 Outlook 2010 和更高版本。</td>
    </tr>
    </tbody>
    </table>


  - **从 .pst 文件导入邮件**   在 Exchange 2013 中，可以使用邮箱导入请求将邮件从 .pst 文件导入用户的存档或主邮箱。有关详细信息，请参阅[邮箱导入和导出请求](mailbox-import-and-export-requests-exchange-2013-help.md)。还可以使用 PST 捕获工具在组织的计算机上搜索 .pst 文件，并将 .pst 文件数据导入用户的存档。

## 存档和保留策略

在 Exchange 2013 中，您可以对邮箱应用存档策略，以便在指定期限后自动将邮件从用户的主邮箱移动到存档邮箱。存档策略是通过创建使用“移动到存档”保留操作的保留标记而实现的。

邮件将移动到存档邮箱中与主邮箱的源文件夹同名的文件夹中。如果存档邮箱中不存在同名的文件夹，将在“托管文件夹助理”移动邮件时创建该文件夹。通过在存档邮箱中重新创建相同的文件夹层次结构，用户可以轻松地找到邮件。

有关保留策略、保留标记和“移动到存档”保留操作的详细信息，请参阅[保留标记和保留策略](retention-tags-and-retention-policies-exchange-2013-help.md)。

## 默认 MRM 策略

Exchange 2013 安装程序会创建默认存档和保留策略，即“默认 MRM 策略”。该策略包含具有“移动到存档”操作的保留标记，如下表所示。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2010 中，Exchange 安装程序所创建的默认存档和保留策略名为“默认存档和保留策略”。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>保留标记名称</th>
<th>标记类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>默认 2 年后移动到存档</strong></p></td>
<td><p>默认 (DPT)</p></td>
<td><p>两年后邮件将自动移动到存档邮箱。应用于整个邮箱中未从文件夹继承或显式应用保留标记的邮件。</p></td>
</tr>
<tr class="even">
<td><p><strong>个人 1 年后移动到存档</strong></p></td>
<td><p>个人</p></td>
<td><p>一年后邮件将自动移动到存档邮箱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>个人 5 年后移动到存档</strong></p></td>
<td><p>个人</p></td>
<td><p>5 年后邮件将自动移动到存档邮箱。</p></td>
</tr>
<tr class="even">
<td><p><strong>个人永远不会移动到存档</strong></p></td>
<td><p>个人</p></td>
<td><p>邮件永远不会移动到存档邮箱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>可恢复邮件 14 天后移动到存档</strong></p></td>
<td><p>“可恢复的项目”文件夹</p></td>
<td><p>邮件将从用户主邮箱的“可恢复的项目”文件夹移动到存档邮箱的“可恢复的项目”文件夹。尝试恢复存档中已删除项目的用户必须使用存档邮箱的“恢复已删除邮件”功能。</p></td>
</tr>
</tbody>
</table>


如果为邮箱用户启用了就地存档，而且尚没有为邮箱分配保留策略，将自动分配默认存档和保留策略。在“托管文件夹助理”对邮箱进行处理后，用户即可使用这些标记，然后可以标记要移动到存档邮箱的文件夹或邮件。默认情况下，2 年后将移动整个邮箱中的电子邮件。

在为用户设置存档邮箱之前，建议先通知用户将对其邮箱应用的存档策略，并根据其需求提供后续培训或文档。其中应包括如下相关详细信息：

  - 存档、默认存档和保留策略中的可用功能。

  - 有关邮件可能会在何时自动移动到存档的信息。

  - 有关在存档邮箱中创建的文件夹层次结构的信息。

  - 如何应用个人标记（显示在 Outlook 和 Outlook Web App 的“存档策略”菜单中）。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果将保留策略应用于具有存档邮箱的用户，该保留策略将替换默认 MRM 策略。可以通过“移动到存档”操作创建一个或多个保留标记，然后将这些标记链接到保留策略。还可以将默认“移动到存档”标记（由安装程序创建并链接到“默认 MRM 策略”）添加到您创建的任何保留策略。</td>
</tr>
</tbody>
</table>


有关 Outlook 2010 及更高版本中遵从性和存档的信息，请参阅[规划 Outlook 2010 中的遵从性和存档](https://go.microsoft.com/fwlink/?linkid=210902)。

## 存档配额

存档邮箱旨在使用户可以在其主邮箱外部存储历史邮件数据。通常，邮箱存储配额较低，并且超出这些配额时会受到很多限制，因此用户会使用 .pst 文件。例如，当用户的邮箱大小超过了“禁止发送”配额时，可以阻止用户发送邮件。同样，当用户的邮箱大小超过了“禁止发送和接收”配额时，可以阻止用户发送和接收邮件。

为了不再使用 .pst 文件，可向存档邮箱提供满足用户要求的存储限制。但是，您可能仍希望保留对存储配额和存档邮箱增长的控制，以帮助监视成本和扩展。

为了帮助进行此项控制，可以使用“存档警告配额”和“存档配额”配置存档邮箱。存档邮箱超过了指定的存档警告配额时，将在应用程序事件日志中记录一个警告事件。当存档邮箱超过了指定的存档配额时，不会再将邮件移动到存档，将在应用程序事件日志中记录一个警告事件，并会向邮箱用户发送配额邮件。默认情况下，在 Exchange 2013 中，存档警告配额和存档配额将分别设置为 45 GB 和 50 GB。

下表列出了在符合存档警告配额和存档配额时，所记录的事件及发送的警告邮件。


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>配额</th>
<th>事件 ID</th>
<th>类型</th>
<th>来源</th>
<th>类别</th>
<th>邮件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>存档警告配额</p></td>
<td><p>10022</p></td>
<td><p>警告</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>托管文件夹助理</p></td>
<td><p>存档邮箱 '&lt;显示名称&gt;:&lt;GUID&gt;:&lt;邮箱数据库&gt;:&lt;服务器 FQDN&gt;' 已超出存档警告配额 '&lt;存档警告配额&gt;'。存档邮箱大小为 '&lt;大小&gt;' 个字节。</p></td>
</tr>
<tr class="even">
<td><p>存档配额</p></td>
<td><p>8537</p></td>
<td><p>警告</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>常规</p></td>
<td><p>&lt;旧 DN&gt; 的存档邮箱已超出存档邮箱大小的上限。您无法将邮件复制或移入存档邮箱。所有将邮件移至存档邮箱的邮件保留操作都会失败，且主邮箱中可能会有附带逾期保留标记的邮件，直到存档邮箱的大小缩回到最大限制范围内。有关存档邮箱的情况，需通知邮箱所有者。</p></td>
</tr>
</tbody>
</table>


## 就地档案和其他 Exchange 功能

本部分介绍就地存档之间的功能和各种 Exchange 功能：

  - **Exchange 搜索**   快速搜索邮件的能力对于存档邮箱变得更加重要。对于 Exchange 搜索，主邮箱与存档邮箱之间没有差异。两个邮箱的内容均编制了索引。因为存档邮箱未在用户的计算机上缓存（即使使用处于缓存 Exchange 模式的 Outlook 也是如此），所以存档的搜索结果始终由 Exchange 搜索提供。在 Outlook 2010 及更高版本和 Outlook Web App 中搜索整个邮箱时，搜索结果包括用户的主邮箱和存档邮箱。

  - **就地电子数据展示**   当发现管理员执行就地电子数据展示搜索时，同时也会搜索用户的存档邮箱。当从 Exchange 管理中心 (EAC) 创建发现搜索时，没有排除存档邮箱的选项。使用 Exchange 命令行管理程序创建发现搜索时，可以通过使用 *DoNotIncludeArchive* 开关排除存档。有关详细信息，请参阅[New-MailboxSearch](https://technet.microsoft.com/zh-cn/library/dd298064\(v=exchg.150\))。若要了解详细信息，请参阅[就地电子数据展示](in-place-ediscovery-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您不能使用就地电子数据展示搜索断开连接的邮箱。</td>
    </tr>
    </tbody>
    </table>


  - **就地保留和诉讼保留**   如果将邮箱置于就地保留或诉讼保留，保留将同时置于主邮箱和存档邮箱。若要了解有关就地保留和诉讼保留的更多信息，请参阅[就地保留和诉讼保留](in-place-hold-and-litigation-hold-exchange-2013-help.md)。

  - **可恢复的项目文件夹**   存档邮箱包含自己的“可恢复的项目”文件夹，而且其“可恢复的项目”文件夹配额需与主邮箱的“可恢复的项目”文件夹配额相同。有关可恢复邮件的详细信息，请参阅[“可恢复的项目”文件夹](recoverable-items-folder-exchange-2013-help.md)。

  - **Exchange 中的 Lync 内容存档**   可以将用户的主邮箱中的即时消息对话以及共享的在线会议文档存档。邮箱必须驻留于 Exchange 2013 邮箱服务器，并且还必须在组织中部署 Microsoft Lync 2013。有关详细信息，请参阅[与 SharePoint 和 Lync 的集成](integration-with-sharepoint-and-lync-exchange-2013-help.md)。

## 管理存档邮箱

在 Exchange 2013 中，创建和管理存档邮箱与常见邮箱管理任务集成在一起，其中包括：

  - **创建存档邮箱**   可以在创建邮箱时创建存档邮箱，也可以为现有邮箱启用存档邮箱。有关详细信息，请参阅[在 Exchange 2013 中管理就地存档](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)。

  - **移动存档邮箱**   可将用户的存档邮箱移动到相同邮箱服务器的其他邮箱数据库，也可以移动到其他服务器，而与主邮箱无关。要移动用户的存档邮箱，必须创建邮箱移动请求。有关详细信息，请参阅[管理内部部署移动](manage-on-premises-moves-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>不支持在 Exchange Server 的不同版本上查找用户的邮箱和存档。</td>
    </tr>
    </tbody>
    </table>


  - **禁用存档邮箱**   您可能希望禁用用户的存档邮箱以进行故障排除，或者要将主邮箱移动到不支持就地存档的 Exchange 版本。禁用存档与禁用主邮箱类似。有关详细信息，请参阅[在 Exchange 2013 中管理就地存档](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)。在内部部署中，禁用的存档邮箱将保留在邮箱数据库中，直到达到了该数据库的已删除邮箱保留期。在此期间，用户可以重新将该存档连接到邮箱用户。达到了已删除邮箱保留期时，已断开连接的存档邮箱将从邮箱数据库中清除。

  - **检索邮箱统计信息和文件夹统计信息**   可以将 *Archive* 开关与 [Get-MailboxStatistics](https://technet.microsoft.com/zh-cn/library/bb124612\(v=exchg.150\)) cmdlet 和 [Get-MailboxFolderStatistics](https://technet.microsoft.com/zh-cn/library/aa996762\(v=exchg.150\)) cmdlet 结合使用，来检索用户存档邮箱的邮箱统计信息和邮箱文件夹统计信息。

  - **测试存档连接性**   在 Exchange 2013 中，可以使用 [Test-ArchiveConnectivity](https://technet.microsoft.com/zh-cn/library/hh529914\(v=exchg.150\)) cmdlet 来测试指定用户的内部部署或基于云的存档连接性。

