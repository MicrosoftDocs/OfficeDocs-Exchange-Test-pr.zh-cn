---
title: '适用于邮箱迁移的 CSV 文件: Exchange Online Help'
TOCTitle: CSV files for mailbox migration
ms:assetid: e67b3455-3946-4335-b80c-97823c76ac54
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn170437(v=EXCHG.150)
ms:contentKeyID: 54652259
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 适用于邮箱迁移的 CSV 文件

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2017-11-16_

您可以使用 CSV 文件批量迁移大量用户邮箱。使用 Exchange 管理中心 (EAC) 或 Exchange 命令行管理程序 中的 **New-MigrationBatch** cmdlet，您可以指定一个 CSV 文件来创建迁移批处理。如果出现以下迁移情况，支持使用 CSV 文件指定要通过迁移批处理迁移的多个用户：

  - **移入本地 Exchange 组织**
    
      - **本地移动：**  本地移动是指将邮箱从一个邮箱数据库移动到另一个邮箱数据库的情况。本地移动发生在单个林内部。
    
      - **跨林企业移动：** 在跨林企业移动中，将邮箱移到一个不同的林。跨林移动可从目标林（邮箱移动的目标林）启动，也可从源林（当前托管邮箱的林）启动。

  - **Exchange Online** 中的加入和分离
    
      - **加入远程移动迁移：** 在 Exchange 混合部署中，您可以将邮箱从本地 Exchange 组织移动到 Exchange Online 中。这也称为*加入*远程移动迁移，因为您将邮箱加入到 Exchange Online 中。
    
      - **分离远程移动迁移：**  您也可以执行\&quot;分离\&quot;远程移动迁移，即将 Exchange Online 邮箱迁移到本地 Exchange 组织中。
        
        > [!NOTE]  
        > 加入和分离远程移动迁移均从 Exchange Online 组织启动。
    
      - **暂存 Exchange 迁移：** 您还可以将邮箱的一个子集从本地 Exchange 组织迁移到 Exchange Online 中。这是另一种类型的加入迁移。只能对 Exchange 2003 和 Exchange 2007 邮箱进行暂存 Exchange 迁移。不支持对 Exchange 2010 和 Exchange 2013 邮箱进行暂存迁移。在运行暂存迁移之前，您必须使用目录同步或其他一些设置来设置 Exchange Online 组织中的邮件用户。
    
      - **IMAP 迁移：** 这种类型的加入迁移将邮箱数据从 IMAP 服务器（包括 Exchange）迁移到 Exchange Online 中。对于 IMAP 迁移，您必须先在 Exchange Online 中设置邮箱，然后才能迁移邮箱数据。

> [!NOTE]  
> 不支持移交Exchange迁移，因为所有内部用户的邮箱都迁移到Exchange Online在单个批处理中使用 CSV 文件。


## 在您执行批量移动或迁移时 CSV 文件支持的属性

用于迁移用户的 CSV 文件的第一行（即\&quot;标题行\&quot;）列出了后续行中的指定属性名称或字段。每个属性名称均用逗号分隔。标题行下的每一行均代表各个用户，并提供了迁移所需的信息。每个用户行中的属性顺序必须与标题行中的属性名称顺序相同。每个属性值均用逗号分隔。如果特定记录的属性值为 Null，切勿为该属性输入任何数据。但请务必使用逗号分隔 Null 值和下一个属性。

如果您在通过 EAC 或 Exchange 命令行管理程序 创建迁移批处理时使用了对应参数，那么 CSV 文件中的属性值将替代对应参数的值。有关详细信息和示例，请参阅\&quot;CSV 文件中的属性值替代迁移批处理的值\&quot;一节。

> [!TIP]  
> 您可以使用任意文本编辑器创建 CSV 文件，但使用诸如 Microsoft Excel 之类的应用程序可以更轻松地导入数据以及配置和组织 CSV 文件。请务必将 CSV 文件保存为 .csv 或 .txt 文件。


以下各节描述了每个迁移类型的 CSV 文件的标题行的受支持的属性。每一节包括一个表，其中列出了每个受支持的特性，是否它是必需的值用于该属性，并说明的示例。

> [!NOTE]  
> 在以下部分中，<em>源环境</em>表示用户邮箱或数据库的当前位置。<em>目标环境</em>表示您要将邮箱迁移至的位置，或者您要将邮箱移动到的数据库。


## 本地移动

下表介绍了您在执行本地移动时 CSV 文件支持的属性。有关详细信息，请参阅[管理内部部署移动](manage-on-premises-moves-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>必需还是可选</th>
<th>可接受的值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必需</p></td>
<td><p>用户的 SMTP 地址</p></td>
<td><p>指定要移动的用户。</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>可选</p></td>
<td><p>数据库名称</p></td>
<td><p>指定用户的主邮箱将被移动到的邮箱数据库。不同的行中的 CSV 文件，这样就可以将同一个迁移批处理中的邮箱移动到不同的数据库，您可以指定一个不同的数据库。</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>可选</p></td>
<td><p>数据库名称</p></td>
<td><p>指定用户的存档邮箱 （如果存在） 将被移动到的邮箱数据库。不同的行中的 CSV 文件，这样就可以将同一个迁移批处理中的存档邮箱移动到不同的数据库，您可以指定一个不同的数据库。</p>

> [!NOTE]  
> 如果不指定存档数据库，存档邮箱移到主邮箱所在的数据库。

</td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>可选</p></td>
<td><p><code>Unlimited</code> 或介于 <code>0</code>（默认值）到 <code>2147483647</code>（最大值）之间的一个非负整数</p></td>
<td><p>指定当迁移服务在邮箱中遇到损坏的项目时要跳过的错误项目数。如果 CSV 文件中包含该属性，那么若您在使用 EAC 或 Exchange 命令行管理程序 创建迁移批处理时添加 <em>BadItemLimit</em> 参数，该属性值将替代默认值或您指定的值。</p>

> [!TIP]  
> 我们建议您使用默认值 0，并且仅在无法对特定用户进行移动或迁移操作时才增加相应用户的错误项目数限制值。

<p></p></td>
</tr>
<tr class="odd">
<td><p>MailboxType</p></td>
<td><p>可选</p></td>
<td><p>使用下列值之一：</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code>（默认值）</p></li>
</ul></td>
<td><p>指定是否将移动用户的主邮箱和 / 或存档邮箱。</p></td>
</tr>
</tbody>
</table>


## 混合部署中的加入远程移动迁移

在混合部署中，您可以将邮箱从本地 Exchange 组织移动到 Exchange Online 中。当您在加入邮箱时，迁移批处理是在 Exchange Online 组织中创建，并由 Exchange Online 管理员启动。有关详细信息，请参阅[在混合部署的本地组织和 Exchange Online 组织之间移动邮箱](https://technet.microsoft.com/zh-cn/library/jj906432\(v=exchg.150\))。

下表介绍了您在执行加入远程移动迁移时 CSV 文件支持的属性。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>必需还是可选</th>
<th>可接受的值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必需</p></td>
<td><p>用户的 SMTP 地址</p></td>
<td><p>指定 Exchange Online 组织中与要迁移的本地用户邮箱对应的启用邮件的用户的电子邮件地址。</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>可选</p></td>
<td><p><code>Unlimited</code> 或介于 <code>0</code>（默认值）到 <code>2147483647</code>（最大值）之间的一个非负整数</p></td>
<td><p>指定当迁移服务在邮箱中遇到损坏的项目时要跳过的错误项目数。如果 CSV 文件中包含该属性，那么若您在使用 EAC 或 Exchange 命令行管理程序 创建迁移批处理时添加 <em>BadItemLimit</em> 参数，该属性值将替代默认值或您指定的值。</p>

> [!TIP]  
> 我们建议您使用默认值 0，并且仅在无法对特定用户进行移动或迁移操作时才增加相应用户的错误项目数限制值。

</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>可选</p></td>
<td><p><code>Unlimited</code> 或介于 <code>0</code>（默认值）到最大值之间的一个非负整数</p></td>
<td><p>指定将被跳过的用户的邮箱中的大项目数。当较大的项目数超出此值时，邮箱迁移将失败。</p>
<p>默认值为 0，表示邮箱中包含任何大项目都会导致迁移失败。</p>
<p>当您将邮箱加入 Exchange Online 时，可迁移的最大项目为 35 MB。</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>可选</p></td>
<td><p>使用下列值之一：</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code>（默认值）</p></li>
</ul></td>
<td><p>指定是否将移动用户的主邮箱和 / 或存档邮箱。</p></td>
</tr>
</tbody>
</table>


## 混合部署中的跨林企业移动和分离远程移动迁移

如前所述，您既可以从目标林开始跨林移动，也可以从源林开始跨林移动。分离远程移动迁移是从 Exchange Online 组织启动。有关详细信息，请参阅：

  - [为跨林移动请求准备邮箱](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [在混合部署的本地组织和 Exchange Online 组织之间移动邮箱](https://technet.microsoft.com/zh-cn/library/jj906432\(v=exchg.150\))

下表介绍了您在 Exchange 混合部署中执行跨林企业移动和分离远程移动迁移时 CSV 文件支持的属性。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>必需还是可选</th>
<th>可接受的值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必需</p></td>
<td><p>用户的 SMTP 地址</p></td>
<td><p>对于跨林企业移动，该属性指定了源林中的邮箱或启用邮件的用户。</p>
<p>对于分离远程移动迁移，该属性指定了 Exchange Online 邮箱。</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>对于分离远程移动迁移和从源林启动的跨林企业移动，该属性是必需的。或者，您也可以在 EAC 中或使用 Exchange 命令行管理程序 创建迁移批处理时指定该属性。</p>
<p>对于从目标林启动的跨林企业移动，该属性是可选的。</p></td>
<td><p>数据库名称</p></td>
<td><p>在目标林中的用户的主邮箱将被移动到指定的邮箱数据库。不同的行中的 CSV 文件，这样就可以将同一个迁移批处理中的邮箱移动到不同的数据库，您可以指定一个不同的数据库。</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>可选</p></td>
<td><p>数据库名称</p></td>
<td><p>在目标林中的用户的存档邮箱将被移动到指定的邮箱数据库。不同的行中的 CSV 文件，这样就可以将同一个迁移批处理中的存档邮箱移动到不同的数据库，您可以指定一个不同的数据库。</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>可选</p></td>
<td><p><code>Unlimited</code> 或介于 <code>0</code>（默认值）到 <code>2147483647</code>（最大值）之间的一个非负整数</p></td>
<td><p>指定当迁移服务在邮箱中遇到损坏的项目时要跳过的错误项目数。如果 CSV 文件中包含该属性，那么若您在使用 EAC 或 Exchange 命令行管理程序 创建迁移批处理时添加 <em>BadItemLimit</em> 参数，该属性值将替代默认值或您指定的值。</p>

> [!TIP]  
> 我们建议您使用默认值 0，并且仅在无法对特定用户进行移动或迁移操作时才增加相应用户的错误项目数限制值。

</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>可选</p></td>
<td><p><code>Unlimited</code> 或介于 <code>0</code>（默认值）到最大值之间的一个非负整数</p></td>
<td><p>指定将被跳过的用户的邮箱中的大项目数。当较大的项目数超出此值时，邮箱迁移将失败。</p>
<p>默认值为 0，表示邮箱中包含任何大项目都会导致迁移失败。</p>
<p>当您将邮箱加入 Exchange Online 时，可迁移的最大项目为 35 MB。</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>可选</p></td>
<td><p>使用下列值之一：</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code>（默认值）</p></li>
</ul></td>
<td><p>指定是否将移动用户的主邮箱和 / 或存档邮箱。</p></td>
</tr>
</tbody>
</table>


## 暂存 Exchange 迁移

如果您想要使用暂存 Exchange 迁移将 Exchange 2003 和 Exchange 2007 本地邮箱迁移到 Exchange Online 中，必须使用 CSV 文件确认迁移批处理的用户组。使用暂存 Exchange 迁移可以迁移到云中的邮箱数没有限制。不过，迁移批处理的 CSV 文件最多可包含 1,000 行。若要迁移超过 1,000 个邮箱，您需要创建其他 CSV 文件，然后使用每个文件新建一个迁移批处理。有关暂存 Exchange 迁移的详细信息，请参阅[使用暂存迁移将邮箱迁移到 Exchange Online](https://technet.microsoft.com/zh-cn/library/jj874018\(v=exchg.150\))。

下表介绍了您在执行暂存 Exchange 迁移时 CSV 文件支持的属性。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>必需还是可选</th>
<th>可接受的值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必需</p></td>
<td><p>用户的 SMTP 地址</p></td>
<td><p>指定已启用邮件的用户 （或如果您要重试迁移的邮箱） 的电子邮件地址相对应的内部用户邮箱，将迁移到Exchange Online中。在Exchange Online目录同步的结果或另一个资源调配过程中创建已启用邮件的用户。已启用邮件的用户的电子邮件地址必须与相应的内部邮箱的<em>WindowsEmailAddress</em>属性相匹配。</p></td>
</tr>
<tr class="even">
<td><p>Password</p></td>
<td><p>可选</p></td>
<td><p>密码最短不得短于 8 个字符，并且必须符合 Office 365 组织适用的所有密码限制。</p></td>
<td><p>当 Exchange Online 中对应的启用邮件的用户在迁移过程中转换为邮箱时，该密码设置在用户帐户上。</p></td>
</tr>
<tr class="odd">
<td><p>ForceChangePassword</p></td>
<td><p>可选</p></td>
<td><p><code>True</code> 或 <code>False</code></p></td>
<td><p>指定用户在首次登录自己的 Exchange Online 邮箱时是否必须更改密码。</p>

> [!NOTE]  
> 如果您已经通过内部组织中部署活动目录联合身份验证服务 2.0 (AD FS 2.0) 实现单个登录解决方案，必须将<code>False</code>用于此属性的值。

</td>
</tr>
</tbody>
</table>


## IMAP 迁移

IMAP 迁移批处理的 CSV 文件最多可包含 50,000 行。但最好是将用户分成多个较小的批处理来进行迁移。有关 IMAP 迁移的详细信息，请参阅下列主题：

  - [将邮箱从 IMAP 服务器迁移到 Exchange Online 邮箱](https://technet.microsoft.com/zh-cn/library/jj874015\(v=exchg.150\))

  - [IMAP 迁移批处理的 CSV 文件](https://technet.microsoft.com/zh-cn/library/jj200730\(v=exchg.150\))

下表介绍了您在执行 IMAP 迁移时 CSV 文件支持的属性。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>必需还是可选</th>
<th>可接受的值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>必需</p></td>
<td><p>用户的 SMTP 地址</p></td>
<td><p>指定用户 Exchange Online 邮箱的用户 ID。</p></td>
</tr>
<tr class="even">
<td><p>UserName</p></td>
<td><p>必需</p></td>
<td><p>用于在 IMAP 邮件系统上标识用户的字符串（采用 IMAP 服务器支持的格式）</p></td>
<td><p>IMAP 邮件系统 （源环境） 中指定用户帐户的登录的名。除了用户名称，您可以使用已分配必要的权限来访问 IMAP 服务器上的邮箱帐户的凭据。有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/jj200730(v=exchg.150)">IMAP 迁移批处理的 CSV 文件</a>。</p></td>
</tr>
<tr class="odd">
<td><p>Password</p></td>
<td><p>必需</p></td>
<td><p>密码字符串</p></td>
<td><p>指定&amp;quot;UserName&amp;quot;属性指定的用户帐户密码。</p></td>
</tr>
</tbody>
</table>


## CSV 文件中的属性值替代迁移批处理的值

如果您在通过 EAC 或 Exchange 命令行管理程序 创建迁移批处理时使用了对应参数，那么 CSV 文件中的属性值将替代对应参数的值。如果您想要对用户应用迁移批处理值，请将 CSV 文件中的相应单元格留空。这样，您可以为一个迁移批处理中的选定用户混合和匹配特定属性值。

例如，我们假定您创建一批Exchange 命令行管理程序对企业跨目录林移动用户的主和到目标目录林使用以下Exchange 命令行管理程序命令的存档邮箱中。

    New-MigrationBatch -Name CrossForestBatch1 -SourceEndpoint ForestEndpoint1 -TargetDeliveryDomain forest2.contoso.com -TargetDatabases @(EXCH-MBX-02,EXCH-MBX-03) -TargetArchiveDatabases @(EXCH-MBX-A02,EXCH-MBX-A03) -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\CrossForestBatch1.csv")) -AutoStart

> [!NOTE]  
> 默认设置是主要通过移动和存档邮箱，因为您不必在Exchange 命令行管理程序命令中显式指定。


该迁移批处理的 CrossForestBatch1.csv 文件的一部分如下所示：

    EmailAddress,TargetDatabase,TargetArchiveDatabase
    user1@contoso.com,EXCH-MBX-01,EXCH-MBX-A01
    user2@contoso.com,,
    user3@contoso.com,EXCH-MBX-01,
    ...

由于 CSV 文件中的值替代迁移批处理的值，因此用户 1 的主邮箱和存档邮箱分别移动到目标林中的 EXCH-MBX-01 和 EXCH-MBX-A01。用户 2 的主邮箱和存档邮箱移动到 EXCH-MBX-02 或 EXCH-MBX-03。用户 3 的主邮箱移动到 EXCH-MBX-01，存档邮箱移动到 EXCH-MBX-A02 或 EXCH-MBX-A03。

在另一示例中，假设在混合部署将存档邮箱移动到Exchange Online ，使用以下命令创建板载远程移动迁移一批。

    New-MigrationBatch -Name OnBoarding1 -SourceEndpoint RemoteEndpoint1 -TargetDeliveryDomain cloud.contoso.com -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\OnBoarding1.csv")) -MailboxType ArchiveOnly -AutoStart

但由于您还希望移动选定用户的主邮箱，因此该迁移批处理的 OnBoarding1.csv 文件的一部分如下所示：

    EmailAddress,MailboxType
    user1@contoso.com,
    user2@contoso.com,
    user3@cloud.contoso.com,PrimaryAndArchive
    user4@cloud.contoso.com,PrimaryAndArchive
    ...

由于 CSV 文件中的邮箱类型值替代用于创建批处理的命令中的 *MailboxType* 参数值，因此只有用户 1 和 2 的存档邮箱会迁移到 Exchange Online 中，而用户 3 和 4 的主邮箱和存档邮箱则移动到 Exchange Online 中。

