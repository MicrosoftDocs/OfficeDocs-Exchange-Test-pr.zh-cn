---
title: '保留标记和保留策略: Exchange 2013 Help'
TOCTitle: 保留标记和保留策略
ms:assetid: 48c13be5-3f01-4849-a089-766210e54f89
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd297955(v=EXCHG.150)
ms:contentKeyID: 50490475
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 保留标记和保留策略

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

在 Microsoft Exchange Server 2013 和 Exchange Online 中，邮件记录管理 (MRM) 有助于组织管理电子邮件生命周期，并降低与电子邮件和其他通信有关的法律风险。通过 MRM 可更方便地保留为符合公司策略、政府法规或法律要求而需要的邮件以及删除没有法律或商业价值的内容。

观看此[视频](http://go.microsoft.com/fwlink/?linkid=825854)，了解如何将保留标记和保留策略应用到 Exchange Online 中邮箱的快速概览。

正在查找管理 MRM 的分步说明？请参阅[邮件记录管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

**内容**

邮件记录管理策略

保留标记

保留策略

托管文件夹助理

保留挂起

## 邮件记录管理策略

在 Exchange 2013 和 Exchange Online 中，MRM 是通过使用“保留标记”和“保留策略”实现的。在讨论这些保留功能中每一项的详细信息之前，必须了解这些功能在整体 MRM 策略中的用法，这一点很重要。该策略基于以下几项功能：

  - 将“保留策略标记”(RPT) 分配到默认文件夹，如“收件箱”和“已删除邮件”。

  - 将“默认策略标记”(DPT) 应用于邮箱以管理所有无标记邮件的保留。

  - 允许用户将“个人标记”分配给自定义文件夹和单个项目。

  - 将 MRM 功能和用户的收件箱管理和存档习惯分开。不要求用户根据保留要求把邮件放入托管文件夹。各个邮件的保留标记可以和其所在文件夹所应用的保留标记不同。

下图说明了这一策略的实现过程中涉及到的任务。

![使用邮件保留的保留策略](images/Dd297955.429b51d5-51b8-4816-b8a4-221e0915d0c0(EXCHG.150).gif "使用邮件保留的保留策略")

返回顶部

## 保留标记

如上图所示，保留标记用于将保留设置应用于文件夹和各个项目（如电子邮件和语音邮件）。这些设置将指定邮件在邮箱中停留的时间，以及当邮件达到指定的保留时间时应采取的操作。当某封邮件达到其保留时间时，该邮件将被移至用户的就地存档或被删除。

![保留标记中的设置](images/Dd297955.936edd6a-8bc4-4c03-94a3-c240ffe7dd6a(EXCHG.150).png "保留标记中的设置")

保留标记允许用户标记自己的邮箱文件夹和要保留的单个项目。用户无需再根据邮件保留要求将项目存入管理员设置的托管文件夹中。

## 保留标记的类型

保留标记根据可以应用它们的人以及它们在邮箱中可以应用的位置，分为下面三类。


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
<th>保留标记的类型</th>
<th>已应用</th>
<th>应用者</th>
<th>可用操作</th>
<th>详细信息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>默认策略标记 (DPT)</p></td>
<td><p>自动应用于整个邮箱</p>
<p>DPT 适用于<em>未标记</em>项目，即没有直接或通过从文件夹继承而应用保留标记的项目。</p></td>
<td><p>管理员</p></td>
<td><ul>
<li><p>移动到存档</p></li>
<li><p>删除但允许恢复</p></li>
<li><p>永久删除</p></li>
</ul></td>
<td><p>用户无法更改应用于邮箱的 DPT。</p></td>
</tr>
<tr class="even">
<td><p>保留策略标记 (RPT)</p></td>
<td><p>自动应用于默认文件夹</p>
<p>默认文件夹是在所有邮箱中自动创建的文件夹，例如：“收件箱”、“已删除邮件”和“已发送邮件”。请参阅<a href="default-folders-that-support-retention-policy-tags-exchange-2013-help.md">支持保留策略标记的默认文件夹</a>中的受支持默认文件夹列表。</p></td>
<td><p>管理员</p></td>
<td><ul>
<li><p>删除但允许恢复</p></li>
<li><p>永久删除</p></li>
</ul></td>
<td><p>用户无法更改应用于默认文件夹的 RPT。</p></td>
</tr>
<tr class="odd">
<td><p>个人标记</p></td>
<td><p>手动应用于项目和文件夹</p>
<p>用户可以使用收件箱规则自动应用标记，以便将邮件移动到具有特定标记的文件夹，或者将个人标记应用于邮件。</p></td>
<td><p>用户</p></td>
<td><ul>
<li><p>移动到存档</p></li>
<li><p>删除但允许恢复</p></li>
<li><p>永久删除</p></li>
</ul></td>
<td><p>个人标记允许用户确定项目应保留多久。例如，邮箱可能具有在七年后删除项目的 DPT，但用户可以通过应用在三天内将其删除的个人标记，为新闻稿和自动通知等项目创建例外。</p></td>
</tr>
</tbody>
</table>


## 有关个人标记的详细信息

个人标记可作为 Outlook 2010 和 Outlook Web App 用户的保留策略的一部分，以供这些用户使用。在 Outlook 2010 和 Outlook Web App 中，具有“移动到存档”操作的个人标记显示为“存档策略”，具有“删除但允许恢复”或“永久删除”操作的个人标记显示为“保留策略”，如下图所示。

![Outlook 2010 和 Outlook Web App 中的个人标记](images/Dd297955.2dbaee13-fdd0-4c30-b821-e662ce2587bb(EXCHG.150).gif "Outlook 2010 和 Outlook Web App 中的个人标记")

用户可以将个人标记应用于他们创建的文件夹或单个项目。对于应用了个人标记的邮件，始终根据个人标记的设置进行处理。用户可将个人标记应用于邮件，以使其移动或删除时间早于或晚于应用于该用户邮箱的 DPT 或 RPT 中指定的设置。还可创建禁用了保留的个人标记。这样用户可对项目进行标记，以使其从不移至存档或永不到期。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>用户可将存档策略应用于默认文件夹、用户创建的文件夹或子文件夹以及个别项目。用户可将保留策略应用于用户创建的文件夹或子文件夹以及个别项目（包括默认文件夹中的子文件夹和项目），而不应用于默认文件夹。</td>
</tr>
</tbody>
</table>


此外，用户还可以使用 Exchange 管理中心 (EAC) 选择其他与自身保留策略不相关的个人标记。然后，所选标记在 Outlook 2010 和 Outlook Web App 中变为可用状态。要使用户可从 EAC 中选择其他标记，必须将 [MyRetentionPolicies 角色](myretentionpolicies-role-exchange-2013-help.md) 添加到用户的角色分配策略。要详细了解用户的角色分配策略，请参阅[了解管理角色分配策略](understanding-management-role-assignment-policies-exchange-2013-help.md)。如果允许用户选择其他个人标记，则 Exchange 组织中的所有个人标记均可供用户使用。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>个人标记是一项高级功能。策略中含有这些标记的的邮箱（即用户向其邮箱添加标记的结果）需要 Exchange Enterprise 客户端访问许可证 (CAL)。</td>
</tr>
</tbody>
</table>


返回顶部

## 保留时间

在启用某个保留标记时，必须为该标记指定保留时间。此时间指示在邮件到达用户邮箱中后，保留邮件的天数。

非定期项目（如电子邮件）与具有结束日期的项目或定期项目（如会议和任务）的保留时间的计算方式不同。若要了解如何为不同类型的项目计算保留时间，请参阅[如何计算保留时间](how-retention-age-is-calculated-exchange-2013-help.md)。

还可以创建禁用保留的保留标记，或在创建标记后禁用标记。因为具有已禁用标记的邮件不会进行处理，因此不会采取保留操作。因此，用户可以使用已禁用个人标记作为“从不移动”标记或“从不删除”标记，以覆盖本会应用于邮件的 DPT 或 RPT。

## 保留操作

创建或配置保留标记时，您可以选择当项目达到保留期限时采取下列保留操作之一：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>保留操作</th>
<th>执行的操作</th>
<th>除非…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>移动到存档</strong> 1</p></td>
<td><ul>
<li><p>将邮件移动到用户的存档邮箱</p></li>
<li><p>仅对 DPT 和个人标记可用</p></li>
</ul>
<p>有关存档的详细信息，请参阅：</p>
<ul>
<li><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的就地存档</a></p></li>
<li><p><a href="https://technet.microsoft.com/zh-cn/library/dn922147(v=exchg.150)">Exchange Online 中的存档邮箱</a></p></li>
</ul></td>
<td><ul>
<li><p>如果用户没有存档邮箱，则不会执行任何操作。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>删除但允许恢复</strong></p></td>
<td><ul>
<li><p>模拟用户清空“已删除邮件”文件夹时的行为。</p></li>
<li><p>邮件已移到邮箱中的<a href="recoverable-items-folder-exchange-2013-help.md">“可恢复的项目”文件夹</a>，并在<em>已删除项目保留</em>期内保留。</p></li>
<li><p>为用户提供另一次在 Outlook 或 Outlook Web App 中使用“恢复已删除项目”对话框恢复项目的机会。</p></li>
</ul></td>
<td><ul>
<li><p>如果您将已删除邮件的保留期限设置为零天，则项目将永久删除。有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/dn163584(v=exchg.150)">更改为 Exchange Online 邮箱保留永久删除的项目的时间</a>。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>永久删除</strong></p></td>
<td><ul>
<li><p>永久删除邮件。</p></li>
<li><p>邮件永久删除后则无法恢复。</p></li>
</ul></td>
<td><ul>
<li><p>如果邮箱处于<a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">就地保留和诉讼保留</a>或诉讼保留状态，则项目会根据保留参数保留在“可恢复的项目”文件夹中。<a href="in-place-ediscovery-exchange-2013-help.md">就地电子数据展示</a>仍会在搜索结果中返回这些项目。</p>
<p></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>标记为已过保留期限</strong></p></td>
<td><ul>
<li><p>将邮件标记为已过期。在 Outlook 2010 或更高版本以及 Outlook Web App 中，已到期项目会与通知“此项目已到期”和“此项目将在 0 天后到期”一起显示。在 Outlook 2007 中，使用带删除线的文本显示标为已过期的项目。</p></li>
</ul></td>
<td><p>不适用</p></td>
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
<td>1   在 Exchange 混合部署中，可以为本地主邮箱启用基于云的存储邮箱。如果向本地邮箱分配存档策略，项目将移动到基于云的存档。如果将某个项目移动到存档邮箱，不会在本地邮箱中保留它的副本。如果将本地邮箱置于保留状态，存档策略仍会将项目移动到基于云的存档邮箱，项目将在其中保存保留指定的时间。</td>
</tr>
</tbody>
</table>


有关如何创建保留标记的详细信息，请参阅[创建保留策略](create-a-retention-policy-exchange-2013-help.md)。

返回顶部

## 保留策略

若要将一个或多个保留标记应用于邮箱，必须将其添加到保留策略，然后将该策略应用于邮箱。一个邮箱不能有多个保留策略。保留标记可以随时链接到保留策略或断开与保留策略的链接，更改会自动对应用了策略的所有邮箱生效。

保留策略可以有以下保留标记：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>保留标记类型</th>
<th>策略中的标记</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>默认策略标记 (DPT)</p></td>
<td><ul>
<li><p>一个具有“移动到存档”操作的 DPT</p></li>
<li><p>一个具有“删除但允许恢复”或“永久删除”操作的 DPT</p></li>
<li><p>一个具有“删除但允许恢复”或“永久删除”操作的、适用于语音邮件的 DPT</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>保留策略标记 (RPT)</p></td>
<td><ul>
<li><p>每个受支持的默认文件夹所具有的一个 RPT</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不能将特定默认文件夹（如“已删除邮件”）的多个 RPT 链接到相同的保留策略。</td>
</tr>
</tbody>
</table>

</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>个人标记</p></td>
<td><ul>
<li><p>任意数量的个人标记</p></li>
</ul>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>策略中的个人标记太多会使用户感到混淆。我们建议添加到保留策略的个人标记不要超过 10 个。</td>
</tr>
</tbody>
</table>

</td>
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
<td>尽管保留策略不需要链接任何保留标记也可使用，但我们建议不要使用此方案。如果具有保留策略的邮箱未链接任何保留标记，则这可能会导致邮箱项目永不过期。</td>
</tr>
</tbody>
</table>


保留策略可以包含存档标记（将项目移动到个人存档邮箱的标记）和删除标记（删除项目的标记）。邮箱项目也可以同时应用这两种类型的标记。存档邮箱没有单独的保留策略。相同保留策略会应用于主邮箱和存档邮箱。

在规划创建保留策略时，必须考虑这些策略是否同时包含存档和删除标记。前面已提到，保留策略可以具有一个使用“移动到存档”操作的 DPT，以及一个使用“删除但允许恢复”或“永久删除”操作的 DPT。具有“移动到存档”操作的 DPT 的保留时间必须短于具有删除操作的 DPT 的保留时间。例如，可以使用具有“移动到存档”操作的 DPT 在两年后将项目移动到存档邮箱，并使用具有删除操作的 DPT 在七年后将项目从邮箱中删除。七年后主邮箱和存档邮箱中的项目都将被删除。

有关与保留策略相关的管理任务列表，请参阅[邮件记录管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 默认保留策略

Exchange 安装程序会创建保留策略“**默认 MRM 策略**”。默认 MRM 策略自动应用于 Exchange Online 中的新邮箱。在 Exchange Server 中，如果您为新用户创建存档，并且没有指定保留策略，则系统自动应用该策略

您可以修改默认 MRM 策略中包含的标记。例如，更改保留时间或保留操作、禁用标记或者通过添加或删除其中标记来修改该策略。更新后的策略将在下次托管文件夹助理对邮箱进行处理时应用于邮箱。

有关详细信息（包括链接到该策略的保留标记列表），请参阅[Exchange Online 和 Exchange Server 中的默认保留策略](default-retention-policy-in-exchange-online-and-exchange-server-exchange-2013-help.md)。

返回顶部

## 托管文件夹助理

托管文件夹助理是在邮箱服务器上运行的邮箱助理，可处理应用了保留策略的邮箱。

托管文件夹助理应用保留策略的方式是检查邮箱中的邮件，并确认是否需要保留这些邮件。然后将需要保留的项目用相应的保留标记进行标记，并对超过保留时间的项目执行指定的保留操作。

托管文件夹助理是基于限制的助理。基于限制的助理始终运行，无需进行计划。这些助理可以占用的系统资源会受到限制。可以将托管文件夹助理配置为在特定期间内（称为“工作周期”）处理邮箱服务器上的所有邮箱。此外，该助理会按指定间隔（称为“工作周期检查点”）刷新要处理的邮箱的列表。在刷新过程中，该助理会将新创建或移动的邮箱添加到队列中。它还会重新确定由于故障而未成功处理的现有邮箱的优先级，并将这些邮箱移动到队列中的较前位置，以便可以在相同工作周期中进行处理。

您还可以使用 [Start-ManagedFolderAssistant](https://technet.microsoft.com/zh-cn/library/aa998864\(v=exchg.150\)) cmdlet 手动触发该助理以处理指定邮箱。若要了解详细信息，请参阅[配置托管文件夹助理](configure-the-managed-folder-assistant-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>托管文件夹助理不会对不需要保留（通过禁用保留标记进行指定）的邮件执行任何操作。您还可以禁用某个保留标记，以临时挂起具有该标记的项目，使其不被处理。</td>
</tr>
</tbody>
</table>


## 在文件夹之间移动项目

从一个文件夹移动到其他文件夹的邮箱项目将继承其移入的文件夹所应用的任何标记。如果将某个项目移动到未分配标记的文件夹，则向该项目应用 DPT。如果为该邮件显式分配了一个标记，则该标记始终优先于任何文件夹级别的标记或默认标记。

## 对存档中的文件夹应用保留标签

当用户对存档中的某个文件夹应用个人标签时，如果在主邮箱中存在一个名称相同但是标签不同的文件夹，存档中该文件夹上的标签将变更以与主邮箱中的文件夹相匹配。这是设计使然，以免对与用户主邮箱中的相同文件夹有着不同到期行为的存档文件夹中的项目产生困惑。例如，用户在主邮箱中有一个带有 *Delete – 3 years* 标签、名为 Project Contoso 的文件夹，在存档邮箱中也有一个 Project Contoso 文件夹。如果用户应用 *Delete – 1 year* 个人标签以在 1 年后删除该文件夹中的项目。当再次处理该邮箱时，文件夹的标签将恢复为 Delete – 3 Years。

## 移除或删除保留策略中的保留标记

从邮箱所应用的保留策略中移除保留标记后，用户将不再能使用该标记，且该标记不能再应用于邮箱中的任何邮件。

已用该标记进行标记的现有项目将继续由托管文件夹助理根据之前设置进行处理，并且将对这些邮件应用标记中指定的任何保留操作。

但是，如果删除该标记，则会删除存储在 Active Directory 中的标记定义。这会使托管文件夹助理处理邮箱中的所有项目，并对应用了已删除标记的项目重新进行标记。根据邮箱数和邮件数，此过程可能会在所有包含使用保留策略（包括已删除标记）的邮箱的邮箱服务器上占用大量资源。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>从保留策略中移除保留标记后，根据该标记的设置，任何应用了该标记的现有邮箱项目将继续过期。为防止该标记的设置应用于任何邮件，应删除该标记。删除标记会将该标记从其所在的任何保留策略中删除。</td>
</tr>
</tbody>
</table>


## 禁用保留标记

如果禁用某个保留标记，则托管文件夹助理将忽略应用了该标记的项目。禁用了保留标记的项目将从不移动或从不删除，具体取决于指定的保留操作。因为这些项目仍被视为标记项目，所以不会对其应用 DPT。例如，如果要对保留标记设置进行故障排除，可以暂时禁用保留标记，以停止托管文件夹助理对具有该标记的邮件的处理。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>已禁用保留标记的保留期会向用户显示为“从不”。如果用户标记某个项目时认为将永不会删除该项目，则以后启用标记可能会导致意外删除用户不想删除的项目。对于具有“移动到存档”操作的标记，情况也是如此。</td>
</tr>
</tbody>
</table>


返回顶部

## 保留挂起

当用户暂时离开办公室且不能访问自己的电子邮件时，可在用户返回工作岗位或访问电子邮件之前将保留设置应用于新邮件。根据保留策略，可以删除邮件或将其移动到用户的个人存档。将邮箱放在保留挂起中可以使保留策略在指定的时间内暂停处理邮箱。在将邮箱放在保留挂起中之后，还可以指定保留注释以将通知邮箱用户（或其他授权访问邮箱的用户）有关保留挂起的信息，包括计划开始和结束挂起的时间。保留注释显示在支持的 Outlook 客户端中。还可以将保留挂起注释本地化为用户的首选语言。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>将邮箱放在保留挂起中不会影响对邮箱存储配额的处理。根据邮箱使用情况和适用的邮箱配额，当用户度假或长时间无法访问电子邮件时，可考虑暂时增加用户的邮箱存储配额。有关邮箱存储配额的详细信息，请参阅<a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">配置邮箱的存储配额</a>。</td>
</tr>
</tbody>
</table>


用户长期不工作时，可能会积累大量的电子邮件。根据电子邮件数量和离开的时间长度，这些用户可能需要几周时间将自己的邮件分类。在这些情况下，在将邮件从保留挂起中删除以前，要考虑到用户跟进邮件可能要花的额外时间。

如果您所在的组织从未实现 MRM，且您的用户还不熟悉它的功能，则也可以在 MRM 部署的初始“准备和培训”阶段使用保留挂起。您可以创建和部署保留策略并使用户了解这些策略，而不会有在用户可以标记项目之前便移动或删除项目的风险。在准备和培训期结束的前几天，您应提醒用户即将达到准备截止时间。过了截止时间后，您可以从用户邮箱中删除保留挂起，以允许托管文件夹助理处理邮箱项目并执行指定的保留操作。

有关如何将邮箱放在保留挂起中的详细信息，请参阅[放置的邮箱上保留挂起](place-a-mailbox-on-retention-hold-exchange-2013-help.md)。

返回顶部

