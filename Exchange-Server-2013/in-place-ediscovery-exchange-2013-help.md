---
title: '就地电子数据展示: Exchange Online Help'
TOCTitle: 就地电子数据展示
ms:assetid: 6377cb7a-3416-4e15-8571-c45d2160fc6f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298021(v=EXCHG.150)
ms:contentKeyID: 50490713
ms.date: 01/19/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 就地电子数据展示

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2017-01-17_

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange Online（Office 365 和 Exchange Online 独立计划）中新建就地电子数据展示搜索的截止时间为 2017 年 7 月 1 日，我们已推迟了这一最后期限。不过，今年晚些时候或明年初，将无法在 Exchange Online 中新建就地电子数据展示搜索。若要创建电子数据展示搜索，请开始在 Office 365 安全与合规中心使用<a href="https://go.microsoft.com/fwlink/?linkid=847843">内容搜索</a>。在我们取消新建就地电子数据展示搜索后，仍可以修改现有就地电子数据展示搜索，并且在 Exchange Server 2013 和 Exchange 混合部署中新建就地电子数据展示搜索也仍将受支持。</td>
</tr>
</tbody>
</table>


如果您的组织遵循法定发现要求（与组织策略、合规性或诉讼相关），Microsoft Exchange Server 2013 和 Exchange Online 中的就地电子数据展示可以帮助您对邮箱内的相关内容执行发现搜索。Exchange 2013 和 Exchange Online 还提供联合搜索功能以及与 Microsoft SharePoint 2013 和 Microsoft SharePoint Online 的集成。您可以使用 SharePoint 中的电子数据展示中心搜索并保留与某个案例相关的所有内容，包括 SharePoint 2013 和 SharePoint Online 网站、文档、SharePoint（仅限 SharePoint 2013）编入索引的文件共享、Exchange 中的邮箱内容以及存档的 Lync 2013 内容。您还可以在 Exchange 混合环境中使用就地电子数据展示，在同一搜索中搜索内部部署邮箱和基于云的邮箱。

**目录**

就地电子数据展示的工作原理

Exchange 搜索

发现管理角色组和管理角色

就地电子数据展示的自定义管理作用域

与 SharePoint Server 2013 和 SharePoint Online 的集成

Exchange 混合部署中的电子数据展示

发现邮箱

使用就地电子数据展示

估计、预览和复制搜索结果

将搜索结果导出到 PST 文件

不同的搜索结果

就地电子数据展示搜索的日志记录

就地电子数据展示和就地保留

保留邮箱以用于就地电子数据展示

就地电子数据展示限制和限制策略

就地电子数据展示文档

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>就地电子数据展示是一项强大的功能，利用它，具有正确权限的用户可能可以访问存储在 Exchange 2013 或 Exchange Online 组织中的所有邮件记录。控制和监视发现活动是很重要的，这些活动包括将成员添加至 Discovery Management 角色组、分配 Mailbox Search 管理角色以及分配对发现邮箱的邮箱访问权限。</td>
</tr>
</tbody>
</table>


## 就地电子数据展示的工作原理

就地电子数据展示使用的是由 Exchange 搜索创建的内容索引。基于角色的访问控制 (RBAC) 提供了 [发现管理](discovery-management-exchange-2013-help.md) 角色组，以便将发现任务委派给非技术人员，而无需提供提升的权限，提升的权限可能会允许用户对 Exchange 配置进行任何操作性的更改。Exchange 管理中心 (EAC) 为非技术人员（如法律和合规事务主管、记录管理员和人力资源 (HR) 专家等）提供易于使用的搜索界面。

授权用户可以执行就地电子数据展示搜索，方法是选择邮箱，然后指定搜索条件，例如关键字、开始日期和结束日期、发件人地址和收件人地址以及邮件类型。搜索完成后，授权用户可以选择下列操作之一：

  - **估计搜索结果**   此选项将返回预计的项目总大小和数量，搜索将基于您指定的条件返回。

  - **预览搜索结果**   此选项提供结果预览。将显示从每个搜索的邮箱返回的邮件。

  - **复制搜索结果**   此选项允许您将邮件复制到发现邮箱。

  - **导出搜索结果**   将搜索结果复制到发现邮箱后，可以将其导出到 PST 文件中。

![估计、预览、复制和导出搜索结果](images/Dd298021.6356971a-34ed-4586-8229-030448d4fe2d(EXCHG.150).gif "估计、预览、复制和导出搜索结果")

## Exchange 搜索

就地电子数据展示使用的是由 Exchange 搜索创建的内容索引。Exchange 搜索经过重新设计，可使用 Microsoft Search Foundation，这是一个丰富的搜索平台，具有更高的索引和查询性能以及改进搜索功能。因为 Microsoft Search Foundation 也由其他 Office 产品（包括 SharePoint 2013）使用，所以它可在这些产品间提供更好的互操作性和相似的查询语法。

使用单一内容索引引擎，当 IT 部门收到电子数据展示请求时，无需使用其他资源便可针对就地电子数据展示进行爬网和索引邮箱数据库。

就地电子数据展示使用关键字查询语言 (KQL)，这是一种查询语法，类似于 Microsoft Outlook 和 Outlook Web App 中的即时搜索使用的高级查询语法 (AQS)。熟悉 KQL 的用户可以轻松构建强大的搜索查询以搜索内容索引。

有关通过 Exchange 搜索编制索引的文件格式的详细信息，请参阅[由 Exchange 搜索编制索引的文件格式](file-formats-indexed-by-exchange-search-exchange-2013-help.md)。

## 发现管理角色组和管理角色

对于执行就地电子数据展示搜索的授权用户，您必须将其添加到 [发现管理](discovery-management-exchange-2013-help.md) 角色组。此角色组由下面两个管理角色构成：[邮箱搜索角色](mailbox-search-role-exchange-2013-help.md)（使用户可执行就地电子数据展示搜索）和 [法定保留角色](legal-hold-role-exchange-2013-help.md)（使用户可将邮箱置于就地保留或诉讼保留状态）。

默认情况下，不会向任何用户或 Exchange 管理员分配执行与就地电子数据展示相关的任务所需的权限。作为组织管理角色组成员的 Exchange 管理员可向发现管理角色组添加用户，并可创建自定义角色组，将发现管理员的作用域限制为用户的子集。有关将用户添加到 Discovery Management 角色组的详细信息，请参阅[在 Exchange 中分配电子数据展示权限](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果用户未添加到 Discovery Management 角色组或未分配 Mailbox Search 角色，则不会在 EAC 中显示“就地电子数据展示和保留”用户界面，且就地电子数据展示 cmdlet 在 Exchange 命令行管理程序中不可用。</td>
</tr>
</tbody>
</table>


RBAC 角色更改的审核（默认情况下会启用）可确保保留了适当的记录，以便跟踪发现管理角色组的分配。您可以使用管理员角色组报告搜索对管理员角色组所做的更改。有关详细信息，请参阅[搜索角色组更改或管理员审核日志](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)。

返回顶部

## 就地电子数据展示的自定义管理作用域

您可以使用自定义管理范围，允许特定用户或组使用就地电子数据展示来搜索 Exchange 2013 或 Exchange Online 组织中的部分邮箱。例如，您可能希望发现管理员仅搜索特定位置或部门的用户邮箱。您可以通过创建使用自定义收件人筛选器控制可以搜索哪些邮箱的自定义管理作用域来执行此操作。收件人筛选器作用域根据收件人类型或其他收件人属性，使用筛选器指向特定收件人。

对于就地电子数据展示，用户邮箱上可以用于为自定义作用域创建收件人筛选器的唯一属性是通讯组成员身份。如果您使用其他属性（如 *CustomAttributeN*、*Department* 或 *PostalCode*），由分配了自定义作用域的角色组成员运行的搜索将失败。有关详细信息，请参阅[为就地电子数据展示搜索创建自定义管理范围](create-a-custom-management-scope-for-in-place-ediscovery-searches-exchange-2013-help.md)。

## 与 SharePoint Server 2013 和 SharePoint Online 的集成

Exchange 2013 和 Exchange Online 提供与 SharePoint 2013 和 SharePoint Online 的集成，从而使发现管理员可以在 SharePoint 中使用电子数据展示中心来执行以下任务：

  - **从单个位置搜索和保留内容** 授权发现管理员可以跨 SharePoint 和 Exchange 搜索和保留内容，包括 Lync 内容（如 Exchange 邮箱中存档的即时消息对话和共享会议文档）。

  - **案例管理** 电子数据展示中心使用案例管理方法进行电子数据展示，从而使您可以创建案例并针对每个案例跨不同内容库保留内容。

  - **导出搜索结果** 发现管理员可以使用电子数据展示中心导出搜索结果。包含在搜索结果中的邮箱内容会导出到 PST 文件中。

SharePoint 还使用 Microsoft Search Foundation 进行内容索引和查询。无论发现管理员是使用 EAC 还是电子数据展示中心搜索 Exchange 内容，都会返回相同邮箱内容。

在内部部署中，在使用 SharePoint 中的电子数据展示中心搜索 Exchange 邮箱之前，必须在两个应用程序之间建立信任。在 Exchange 2013 和 SharePoint 2013 中，这使用 OAuth 身份验证来完成。有关详细信息，请参阅[针对 SharePoint eDiscovery 中心配置 Exchange](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)。从 SharePoint 执行的电子数据展示搜索通过 Exchange 使用 RBAC 进行授权。若要 SharePoint 用户能够执行 Exchange 邮箱的电子数据展示搜索，必须在 Exchange 中向他们分配委派发现管理权限。若要能够预览使用 SharePoint 电子数据展示中心执行的电子数据展示搜索中返回的邮箱内容，发现管理员必须在相同 Exchange 组织中拥有邮箱。

有关如何在 Office 365 组织中设置电子数据展示中心的分步说明，请参阅[在 SharePoint Online 中设置电子数据展示中心](https://go.microsoft.com/fwlink/p/?linkid=331600)。

## Exchange 混合部署中的电子数据展示

若要在 Exchange 2013 混合组织中成功执行跨界电子数据展示搜索，必须在 Exchange 本地组织和 Exchange Online 组织之间配置 OAuth（开放授权）身份验证，以便能够使用就地电子数据展示搜索本地和基于云的邮箱。OAuth 身份验证是允许应用程序互相进行身份验证的服务器间身份验证协议。

OAuth 身份验证支持 Exchange 混合部署中的以下电子数据展示方案：

  - 在使用 Exchange Online Archiving 的本地邮箱中搜索基于云的存档邮箱。

  - 在同一个电子数据展示搜索中搜索本地和基于云的邮箱。

  - 通过使用 SharePoint Online 中的电子数据展示中心搜索本地邮箱。

有关需要在 Exchange 混合部署中配置 OAuth 身份验证的电子数据展示方案的详细信息，请参阅[使用 OAuth 身份验证支持 Exchange 混合部署中的电子数据展示](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md)。有关配置 OAuth 身份验证以支持电子数据展示的分步说明，请参阅[配置 Exchange 和 Exchange Online 组织之间的 OAuth 身份验证](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)。

## 发现邮箱

创建就地电子数据展示搜索之后，您可以将搜索结果复制到目标邮箱。通过 EAC，您可以选择发现邮箱作为目标邮箱。发现邮箱是一种特殊类型的邮箱，它具有以下功能：

  - **更加轻松安全的目标邮箱选择**   当您使用 EAC 复制就地电子数据展示搜索结果时，只有发现邮箱可作为存储搜索结果的存储库。无需在可能很长的组织可用邮箱列表中费心挑选。这也消除了发现管理员出现以下错误的可能性：即不小心选择了其他用户的邮箱或可能存储了敏感邮件的不安全邮箱。

  - **大型邮箱存储配额**   目标邮箱应能够存储就地电子数据展示搜索可能返回的大量邮件数据。默认情况下，发现邮箱的邮箱存储配额为 50 千兆字节 (GB)。不能增加此存储配额。

  - **默认情况下更加安全**   与所有邮箱类型一样，发现邮箱具有关联的 Active Directory 用户帐户。但是默认情况下，此帐户为禁用状态。只有被显式授权访问发现邮箱的用户可以访问。发现管理角色组的成员具有对默认发现邮箱的完全访问权限。对于您创建的任何其他发现邮箱，未将邮箱访问权限分配给任何用户。

  - **电子邮件传递已禁用**   虽然电子邮件在 Exchange 地址列表中可见，但用户不能将其发送至发现邮箱。使用传递限制来禁止对发现邮箱进行电子邮件传递。这可保持复制到发现邮箱的搜索结果的完整性。

Exchange 2013 安装程序会创建一个显示名为“发现搜索邮箱”的发现邮箱。可以使用命令行管理程序创建其他发现邮箱。默认情况下，创建的发现邮箱不会分配任何邮箱访问权限。可以为发现管理员分配完全访问权限以访问复制到发现邮箱的邮件。有关详细信息，请参阅[创建发现邮箱](create-a-discovery-mailbox-exchange-2013-help.md)。

就地电子数据展示还使用显示名为“SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}”的系统邮箱来保留就地电子数据展示元数据。系统邮箱在 EAC 或 Exchange 地址列表中不可见。在内部部署组织中，在删除就地电子数据展示系统邮箱所在的邮箱数据库之前，必须将该邮箱移动到其他邮箱数据库。如果删除或损坏了该邮箱，则发现管理员无法执行电子数据展示搜索，直到重新创建该邮箱。有关详细信息，请参阅[Re-create the Discovery system mailbox](re-create-the-discovery-system-mailbox-exchange-2013-help.md)。

返回顶部

## 使用就地电子数据展示

已添加至发现管理角色组的用户可以执行就地电子数据展示搜索。可以在 EAC 中使用基于 Web 的界面执行搜索。这可以使非技术人员（如记录管理员、合规事务主管或是法律和 HR 专家）可以更加轻松地使用就地电子数据展示。还可以使用命令行管理程序执行搜索。有关详细信息，请参阅[创建就地电子数据展示搜索](create-an-in-place-ediscovery-search-exchange-2013-help.md)

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在内部部署组织中，可以使用就地电子数据展示搜索位于 Exchange 2013 邮箱服务器上的邮箱。若要搜索位于 Exchange 2010 邮箱服务器上的邮箱，请对 Exchange 2010 服务器使用多邮箱搜索。<br />
在混合部署（即有些邮箱存在于内部部署邮箱服务器，有些邮箱存在于基于云的组织中的环境）中，可以在内部部署组织中使用 EAC 对基于云的邮箱执行就地电子数据展示搜索。如果要将邮件复制到发现邮箱，则必须选择一个内部部署发现邮箱。来自搜索结果中返回的基于云的邮箱的邮件会被复制到指定的内部部署发现邮箱。有关混合部署的详细信息，请参阅 <a href="https://technet.microsoft.com/zh-cn/library/jj200581(v=exchg.150)">Exchange Server 混合部署</a>。</td>
</tr>
</tbody>
</table>


EAC 中的“就地电子数据展示和保留”向导使您可以创建就地电子数据展示搜索，还可使用就地保留将搜索结果置于保留状态。在创建就地电子数据展示搜索时，会在就地电子数据展示系统邮箱中创建搜索对象。可以通过操纵该对象来启动、停止、修改或删除搜索。在创建搜索之后，可以选择获取搜索结果的估计，这包括可帮助确定查询有效性的关键字统计信息。还可以对搜索中返回的项目进行实时预览，从而使您可以查看邮件内容、从每个源邮箱返回的邮件数以及邮件总数。可以使用此信息在需要时进一步微调查询。

当对搜索结果满意时，可以将结果复制到发现邮箱。还可以使用 EAC 或 Outlook 将发现邮箱或其中部分内容导出到 PST 文件。

当创建就地电子数据展示搜索时，必须指定以下参数：

  - **名称**   搜索名称用于标识搜索。当将搜索结果复制到发现邮箱时，会通过使用以唯一方式标识发现邮箱中的搜索结果的搜索名称和时间戳，在发现邮箱中创建文件夹。

  - **邮箱**   可以选择搜索 Exchange 2013 或 Exchange Online 组织中的所有邮箱或指定要搜索的邮箱。用户的主邮箱和存档邮箱包含在搜索中。如果还要使用相同搜索将项目置于保留状态，则必须指定邮箱。可以指定一个通讯组，以包含作为该组成员的邮箱用户。组的成员资格会在创建搜索时一次性进行计算，对组成员资格的后续更改不会自动反映在搜索中。
    
    在 Exchange Online 中，您还可以指定 Office 365 组作为内容源，以便系统搜索组邮箱（或将其置于保留状态）。当您将 Office 365 组添加到就地电子数据展示搜索时，系统只会搜索组邮箱，不搜索组成员的邮箱。

  - **搜索查询**   可以包含指定邮箱中的所有邮箱内容，或使用搜索查询返回与案例或调查更加相关的项目。可以在搜索查询中指定以下参数：
    
      - **关键字**   可以指定关键字和短语来搜索邮件内容。还可以使用逻辑运算符 **AND**、**OR** 和 **NOT**。此外，Exchange 2013 还支持 **NEAR** 运算符，从而使您可以搜索与另一个单词或短语接近的单词或短语。
        
        若要搜索包含多个单词的短语的完全匹配项，必须在该短语前后加上引号。例如，搜索短语“plan and competition”将返回包含该短语的完全匹配项的邮件，而指定 **plan AND competition** 则将返回在邮件中任何位置包含单词 **plan** 和 **competition** 的邮件。
        
        Exchange 2013 还支持将关键字查询语言 (KQL) 语法用于就地电子数据展示搜索。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>就地电子数据展示不支持正则表达式。</td>
        </tr>
        </tbody>
        </table>
        
        逻辑运算符必须使用大写，以将其作为运算符而非关键字处理，例如 **AND** 和 **OR**。我们建议对任何混用多个逻辑运算符的查询使用显式圆括号，以避免出现错误或误解。例如，如果要搜索包含 WordA 或 WordB 以及 WordC 或 WordD 的邮件，则必须使用 **(WordA OR WordB) AND (WordC OR WordD)**。
    
      - **开始日期和结束日期**   默认情况下，就地电子数据展示不按日期范围限制搜索。若要搜索特定日期范围内发送的邮件，可以通过指定开始和结束日期来缩小搜索范围。如果不指定结束日期，则每次重新启动搜索时将返回最新结果。
    
      - **发件人和收件人**   若要缩小搜索范围，可以指定邮件的发件人或收件人。可以使用电子邮件地址、显示名称或域名来搜索发送到或发送自域中每个用户的项目。例如，若要查找由任何用户发送到或发送自 Contoso, Ltd. 的电子邮件，请在 EAC 的“发件人”或“收件人/抄送”字段中指定“@contoso.com”。还可以在命令行管理程序的 *Senders* 或 *Recipients* 参数中指定“@contoso.com”。
    
      - **邮件类型**   默认情况下，搜索所有邮件类型。可以通过选择特定的邮件类型（如电子邮件、联系人、文档、日记、会议、便笺和 Lync 内容）来限制搜索。

下面的屏幕快照显示了 EAC 中的搜索查询的一个示例。

![配置电子数据展示搜索查询](images/Dd298021.a3626569-8700-421e-8b4e-7ec520b28272(EXCHG.150).png "配置电子数据展示搜索查询")

使用就地电子数据展示时，还需考虑以下事项：

  - **附件**   就地电子数据展示会搜索 Exchange 搜索支持的附件。有关详细信息，请参阅 [由 Exchange 搜索编制索引的文件格式](file-formats-indexed-by-exchange-search-exchange-2013-help.md)。在内部部署中，通过针对邮箱服务器上的文件类型安装搜索筛选器（也称为 iFilter），可以添加对其他文件类型的支持。

  - **不可搜索的项目**   不可搜索的项目是指 Exchange 搜索无法编入索引的邮箱项目。无法编入索引的原因包括未对附加文件安装搜索筛选器、筛选器错误和加密邮件。若要实现成功的电子数据展示搜索，组织可能需要包含这类项目以进行审阅。将搜索结果复制到发现邮箱或将搜索结果导出到 PST 文件中时，您可以将不可搜索的项目包括在内。有关详细信息，请参阅 [Exchange 电子数据展示中不可搜索的项目](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)。

  - **加密项目**   因为 Exchange 搜索不会将使用 S/MIME 加密的邮件编入索引，所以就地电子数据展示不会搜索这些邮件。如果选择了用于在搜索结果中包括不可搜索的项目的选项，则这些使用 S/MIME 加密的邮件将复制到发现邮箱。

  - **受 IRM 保护的项目**   使用信息权限管理 (IRM) 保护的邮件会由 Exchange 搜索编入索引，因此在匹配查询参数时会包括在搜索结果中。必须使用 Active Directory 权限管理服务 (AD RMS) 群集保护邮件，此群集应与邮箱服务器处于同一 Active Directory 林中。有关详细信息，请参阅[信息权限管理](information-rights-management-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>当由于解密失败或 IRM 被禁用，Exchange 搜索无法将受 IRM 保护的邮件编入索引时，不会将受保护的邮件添加到失败项目的列表。如果选择了用于在搜索结果中包括不可搜索的项目的选项，则结果中可能不包括无法解密的受 IRM 保护的邮件。<br />
    若要在搜索中包括受 IRM 保护的邮件，可以创建其他搜索以包括具有 .rpmsg 附件的邮件。可以使用查询字符串 <code>attachment:rpmsg</code> 在指定邮箱中搜索所有受 IRM 保护的邮件（无论是否成功编入了索引）。当某个搜索返回与搜索条件匹配的邮件（包括成功编入索引的受 IRM 保护的邮件）时，这可能会导致部分搜索结果重复。该搜索不会返回无法编入索引的受 IRM 保护的邮件。<br />
    对所有受 IRM 保护的邮件执行的第二次搜索还包括在第一次搜索返回且成功编入索引的受 IRM 保护的邮件。此外，第二次搜索返回的受 IRM 保护的邮件可能与用于第一次搜索的搜索条件（如关键字）不匹配。</td>
    </tr>
    </tbody>
    </table>


  - **重复数据删除**   在将搜索结果复制到发现邮箱时，可以对搜索结果启用“重复数据删除”功能以便仅将特定邮件的一个实例复制到发现邮箱。重复数据删除具有以下好处：
    
      - 由于减少了复制的邮件数，因此降低了存储要求并缩小了发现邮箱的大小。
    
      - 减轻了发现管理员、法律顾问或参与审阅搜索结果的其他人员的工作负荷。
    
      - 降低了电子数据展示成本，具体取决于从搜索结果中排除的重复项目数。

返回顶部

## 估计、预览和复制搜索结果

在完成就地电子数据展示搜索之后，可以在 EAC 的详细信息窗格中查看搜索结果估计。估计包括返回的项目数和这些项目的总大小。还可以查看关键字统计信息，这些统计信息可返回有关针对搜索查询中使用的每个关键字返回的项目数的详细信息。此类信息可用于确定查询有效性。如果查询范围太广，则可能返回大得多的数据集，这可能需要更多资源用于审阅并会提高电子数据展示成本。如果查询范围太窄，则可能会显著减少返回的记录数，或是完全不返回任何记录。可以使用估计和关键字统计信息来微调查询，以满足要求。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2013 中，关键字统计信息还包括非关键字属性（如搜索查询中指定的日期、邮件类型和发件人/收件人）的统计信息。</td>
</tr>
</tbody>
</table>


还可以预览搜索结果，以便进一步确保返回的邮件包含所搜索的内容并在需要时进一步微调查询。电子数据展示搜索预览会显示从搜索的每个邮箱中返回的邮件数以及搜索返回的邮件总数。预览会快速生成，而无需将邮件复制到发现邮箱。

在对搜索结果的数量和质量满意之后，可以将它们复制到发现邮箱。当复制邮件时，可以选择以下选项：

  - **包括不可搜索的项目**   有关被视为不可搜索的项目类型的详细信息，请参阅上一节中的电子数据展示搜索注意事项。

  - **启用重复数据删除**   在搜索的一个或多个邮箱中找到多个实例时，重复数据删除可仅包括特定记录的单个实例，从而减小数据集。

  - **启用完整日志记录**   默认情况下，仅当复制项目时才启用基本日志记录。可以选择完整日志记录以包含搜索返回的所有记录的有关信息。

  - **在复制完成时向我发送邮件**   就地电子数据展示搜索可能可返回大量记录。将返回的邮件复制到发现邮箱可能需要较长时间。使用此选项可在复制过程完成时收到电子邮件通知。为了更方便地使用 Outlook Web App 进行访问，通知包含一个链接，该链接指向将邮件复制到的发现邮箱中的位置。

有关详细信息，请参阅[将电子数据展示搜索结果复制到发现邮箱](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)。

返回顶部

## 将搜索结果导出到 PST 文件

将搜索结果复制到发现邮箱后，可以将搜索结果导出到 PST 文件中。

![将电子数据展示搜索结果导出到 PST 文件](images/Dd298021.4ddca8af-1af5-4cb2-852c-e3a292099a58(EXCHG.150).gif "将电子数据展示搜索结果导出到 PST 文件")

在将搜索结果导出到 PST 文件之后，您或其他用户可以在 Outlook 中打开这些结果，以查看或打印在搜索结果中返回的邮件。有关详细信息，请参阅[将电子数据展示搜索结果导出到 PST 文件](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)。

## 不同的搜索结果

由于就地电子数据展示对实时数据进行搜索，因此对同一内容源进行的两次搜索以及使用同一搜索查询可能会返回不同的结果。估计的搜索结果也可能不同于复制到发现邮箱中的实际搜索结果。即使在短时间内重新运行相同的搜索，搜索结果也可能不同。有几个因素可能会影响搜索结果的一致性：

  - 对传入电子邮件的连续索引，这是因为 Exchange 搜索不断地对您组织的邮箱数据库和传输管道进行爬网并将它们编入索引。

  - 用户或自动进程删除电子邮件。

  - 批量导入大量电子邮件，需要花费时间来编入索引。

如果您遇到相同搜索产生不同结果的情况，可以考虑将邮箱置于保留状态以保存内容，在非高峰时段运行搜索，并在导入大量电子邮件后留出些索引时间。

## 就地电子数据展示搜索的日志记录

有两种类型的日志记录可用于就地电子数据展示搜索：

  - **基本日志记录**   默认情况下将为所有就地电子数据展示搜索启用基本日志记录。基本日志记录包含有关搜索和搜索执行人员的信息。使用基本日志记录捕获的信息会显示在发送到存储搜索结果的邮箱的电子邮件正文中。邮件位于为存储搜索结果而创建的文件夹中。

  - **完整日志记录**   完整日志记录包含搜索返回的所有邮件的信息。此信息以逗号分隔值 (.csv) 文件的形式提供，该文件会附加到包含基本日志记录信息的电子邮件中。搜索的名称将用作 .csv 文件的名称。出于遵从性或保留记录的目的，可能需要此信息。若要启用完整日志记录，必须在 EAC 中将搜索结果复制到发现邮箱时选择**启用完整日志记录**选项。如果使用命令行管理程序，则使用 *LogLevel* 参数指定完整日志记录选项。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>还可以在使用命令行管理程序创建或修改就地电子数据展示搜索时禁用日志记录。</td>
</tr>
</tbody>
</table>


除了在将搜索结果复制到发现邮箱时包含的搜索日志之外，Exchange 还记录 EAC 或命令行管理程序用于创建、修改或删除就地电子数据展示搜索的 cmdlet。此信息记录在管理员审核日志条目中。有关详细信息，请参阅[管理员审核日志记录](administrator-audit-logging-exchange-2013-help.md)。

返回顶部

## 就地电子数据展示和就地保留

作为电子数据展示请求的一部分，您可能需要将邮箱内容保留至处理诉讼或调查之后。还必须保留邮箱用户或任何过程已删除或更改的邮件。在 Exchange 2013 中，这是通过使用就地保留来完成的。有关详细信息，请参阅[就地保留和诉讼保留](in-place-hold-and-litigation-hold-exchange-2013-help.md)。

在 Exchange 2013 中，可以使用新的“就地电子数据展示和保留”向导来搜索项目并将它们保留进行电子数据展示或满足其他业务要求所需的时间长度。将相同搜索用于就地电子数据展示和就地保留时，请注意以下事项：

  - 不能使用搜索所有邮箱的选项。必须选择邮箱或通讯组。

  - 如果某个就地电子数据展示搜索还用于就地保留，则不能删除该搜索。必须先在搜索中禁用就地保留选项，然后才能删除该搜索。

## 保留邮箱以用于就地电子数据展示

员工离开组织时，一般会禁用或删除其邮箱。在禁用了邮箱后，会将其从用户帐户断开连接，但仍会将其保留在邮箱中一段时间（默认为 30 天）。托管文件夹助理不会处理断开连接的邮箱，并且在此期间不会应用任何保留策略。您将无法搜索断开的邮箱的内容。达到了为邮箱数据库配置的已删除邮箱保留期时，会将该邮箱从邮箱数据库中清除。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange Online 中，就地电子数据展示可以搜索非活动邮箱的内容。非活动邮箱是指置于就地保留或诉讼保留然后被删除的邮箱。只要非活动邮箱置于保留状态，就能被保留。非活动邮箱从就地保留状态移除或诉讼保留被禁用时，就会永久删除。有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/dn144876(v=exchg.150)">在 Exchange Online 中管理非活动邮箱</a>。</td>
</tr>
</tbody>
</table>


在内部部署中，如果组织要求对已离开组织的员工的邮件应用保留设置，或者需要保留前员工的邮箱供当前或未来电子数据展示搜索使用，请勿禁用或删除邮箱。您可以执行以下步骤以确保邮箱不能访问，并且不会向其传递新邮件。

1.  使用“Active Directory 用户和计算机”或是其他 Active Directory 或帐户设置工具或脚本，禁用 Active Directory 用户帐户。这样可以阻止使用关联的用户帐户登录邮箱。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>拥有完全访问邮箱权限的用户仍能够访问邮箱。若要阻止他人访问，必须从邮箱中删除其完全访问权限。有关如何删除某个邮箱的完全访问邮箱权限的信息，请参阅<a href="manage-permissions-for-recipients-exchange-online-help.md">管理收件人的权限</a>。</td>
    </tr>
    </tbody>
    </table>


2.  将邮箱用户可以发送或接收的邮件的邮件大小限制设置为一个很小的值，如 1 KB。这样可阻止通过该邮箱发送和接收新邮件。有关详细信息，请参阅[配置邮箱的邮件大小限制](configure-message-size-limits-for-a-mailbox-exchange-2013-help.md)。

3.  配置邮件的传递限制，使任何人都无法向其发送邮件。有关详细信息，请参阅[配置邮箱的邮件传递限制](configure-message-delivery-restrictions-for-a-mailbox-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>必须执行以上步骤以及组织要求的任何其他帐户管理过程，但不禁用或删除邮箱或是删除关联用户帐户。</td>
</tr>
</tbody>
</table>


在计划为邮件保留管理 (MRM) 或就地电子数据展示实现邮箱保留时，必须考虑员工流动率。长期保留前员工的邮箱需要邮箱服务器上的额外存储，还会导致 Active Directory 数据库增大，因为要求将关联的用户帐户也保留相同的时间。此外，还可能要求更改组织的帐户设置和管理流程。

返回顶部

## 就地电子数据展示限制和限制策略

在 Exchange 2013 和 Exchange Online 中，可使用限制策略来控制就地电子数据展示可以占用的资源。

默认限制策略包含以下限制参数。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>说明</th>
<th>默认值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DiscoveryMaxConcurrency</p></td>
<td><p>可以同时在组织中运行的就地电子数据展示搜索的最大数量。</p></td>
<td><p>2</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果在仍在运行前两个搜索时启动电子数据展示搜索，第三个搜索不会排队，而将会失败。您必须等到之前的搜索中有一个完成，然后才能成功启动一个新搜索。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>DiscoveryMaxMailboxes</p></td>
<td><p>可以在单个就地电子数据展示搜索中搜索的最大邮箱数。</p></td>
<td><p>Exchange Online: 10,0001</p>
<p>Exchange 2013: 5,000</p></td>
</tr>
<tr class="odd">
<td><p>DiscoveryMaxStatsSearchMailboxes</p></td>
<td><p>可以在仍然允许您查看关键字统计信息的单个就地电子数据展示搜索中搜索到的最大邮箱数。</p></td>
<td><p>100</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>运行电子数据展示搜索估计后，您可以查看关键字统计信息。这些统计信息显示有关搜索查询中使用的每个关键字返回的项目数的详细信息。如果搜索中包括 100 个以上的源邮箱，则在试图查看关键字统计信息时会返回一个错误。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>DiscoveryMaxKeywords</p></td>
<td><p>可以在单个就地电子数据展示搜索中指定的最大关键字数。</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>DiscoveryMaxSearchResultsPageSize</p></td>
<td><p>预览就地电子数据展示搜索结果时，在单个页面上显示的最大项目数。</p></td>
<td><p>200</p></td>
</tr>
<tr class="even">
<td><p>DiscoverySearchTimeoutPeriod</p></td>
<td><p>就地电子数据展示搜索在超时之前将运行的分钟数。</p></td>
<td><p>10 分钟</p></td>
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
<td>1   如果在 Office 365 组织的 SharePoint Online 中的电子数据展示中心内启动电子数据展示搜索，一次最多可以搜索 1,500 个邮箱。</td>
</tr>
</tbody>
</table>


在 Exchange Server 2013 中，您可以更改这些参数的默认值以适合您的要求，或创建其他限制策略并将其分配给具有委派发现管理权限的用户。在 Exchange Online 中，这些限制参数的默认值是不能更改的。

## 就地电子数据展示文档

下表给出了有助于了解和管理就地电子数据展示的各个主题的链接。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="assign-ediscovery-permissions-in-exchange-exchange-2013-help.md">在 Exchange 中分配电子数据展示权限</a></p></td>
<td><p>了解如何为用户授予在 EAC 中使用就地电子数据展示搜索 Exchange 邮箱的权限。将用户添加到发现管理角色组还将允许该用户在 SharePoint 2013 和 SharePoint Online 中使用电子数据展示中心搜索 Exchange 邮箱。</p></td>
</tr>
<tr class="even">
<td><p><a href="create-a-discovery-mailbox-exchange-2013-help.md">创建发现邮箱</a></p></td>
<td><p>了解如何使用命令行管理程序创建发现邮箱并分配访问权限。</p></td>
</tr>
<tr class="odd">
<td><p><a href="create-an-in-place-ediscovery-search-exchange-2013-help.md">创建就地电子数据展示搜索</a></p></td>
<td><p>了解如何创建就地电子数据展示搜索，以及如何估计和预览电子数据展示搜索结果。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=506799">就地电子数据展示的邮件属性和搜索运算符</a></p></td>
<td><p>了解使用就地电子数据展示可以搜索哪些电子邮件属性。本主题提供每个属性的语法示例、关于 <strong>AND</strong> 和 <strong>OR</strong> 等搜索运算符的信息，以及关于其他搜索查询技术（例如，使用双引号 (&quot; &quot;) 和前缀通配符）的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/dn798915(v=exchg.150)">Exchange Online 中就地电子数据展示的搜索限制</a></p></td>
<td><p>了解 Exchange Online 中的就地电子数据展示限制有助于维护 Office 365 组织电子数据展示服务的运行状况和质量。</p></td>
</tr>
<tr class="even">
<td><p><a href="start-or-stop-an-in-place-ediscovery-search-exchange-2013-help.md">启动或停止就地电子数据展示搜索</a></p></td>
<td><p>了解如何启动、停止和重新启动电子数据展示搜索。</p></td>
</tr>
<tr class="odd">
<td><p><a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">修改就地电子数据展示搜索</a></p></td>
<td><p>了解如何修改现有的电子数据展示搜索。</p></td>
</tr>
<tr class="even">
<td><p><a href="copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md">将电子数据展示搜索结果复制到发现邮箱</a></p></td>
<td><p>了解如何将电子数据展示搜索的结果复制到发现邮箱。</p></td>
</tr>
<tr class="odd">
<td><p><a href="export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md">将电子数据展示搜索结果导出到 PST 文件</a></p></td>
<td><p>了解如何将电子数据展示搜索的结果导出到 PST 文件。</p></td>
</tr>
<tr class="even">
<td><p><a href="create-a-custom-management-scope-for-in-place-ediscovery-searches-exchange-2013-help.md">为就地电子数据展示搜索创建自定义管理范围</a></p></td>
<td><p>了解如何使用自定义管理作用域来限制发现管理员可以搜索的邮箱。</p></td>
</tr>
<tr class="odd">
<td><p><a href="remove-an-in-place-ediscovery-search-exchange-2013-help.md">删除就地电子数据展示搜索</a></p></td>
<td><p>了解如何删除电子数据展示搜索。</p></td>
</tr>
<tr class="even">
<td><p><a href="search-for-and-delete-messages-admin-help-exchange-2013-help.md">搜索和删除邮件 - 管理员帮助</a></p></td>
<td><p>了解如何使用 <strong>Search-Mailbox</strong> cmdlet 搜索并删除电子邮件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">减小 Exchange 中发现邮箱的大小</a></p></td>
<td><p>使用此过程可减小大于 50 GB 的发现邮箱的大小。</p></td>
</tr>
<tr class="even">
<td><p><a href="delete-and-re-create-the-default-discovery-mailbox-in-exchange-exchange-2013-help.md">在 Exchange 中删除和重新创建默认发现邮箱</a></p></td>
<td><p>了解如何删除和重新创建默认发现邮箱，并重新向其分配权限。如果此邮箱已超过 50 GB 的限制，且您不需要搜索结果，请使用此过程。</p></td>
</tr>
<tr class="odd">
<td><p><a href="re-create-the-discovery-system-mailbox-exchange-2013-help.md">Re-create the Discovery system mailbox</a></p></td>
<td><p>了解如何重新创建发现系统邮箱。此任务仅适用于 Exchange 2013 组织。</p></td>
</tr>
<tr class="even">
<td><p><a href="using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md">使用 OAuth 身份验证支持 Exchange 混合部署中的电子数据展示</a></p></td>
<td><p>了解 Exchange 混合部署中要求您配置 OAuth 身份验证的电子数据展示方案。</p></td>
</tr>
<tr class="odd">
<td><p><a href="configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md">针对 SharePoint eDiscovery 中心配置 Exchange</a></p></td>
<td><p>了解如何配置 Exchange 2013，以便在 SharePoint 2013 中可以使用电子数据展示中心搜索 Exchange 邮箱。</p></td>
</tr>
<tr class="even">
<td><p><a href="unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md">Exchange 电子数据展示中不可搜索的项目</a></p></td>
<td><p>了解 Exchange 搜索无法编制索引且在电子数据展示搜索结果中作为不可搜索项目返回的邮箱项目。</p></td>
</tr>
</tbody>
</table>


若要详细了解 Office 365、Exchange 2013、SharePoint 2013 和 Lync 2013 中的电子数据展示，请参阅[电子数据展示常见问题](https://go.microsoft.com/fwlink/p/?linkid=386633)。

返回页首

