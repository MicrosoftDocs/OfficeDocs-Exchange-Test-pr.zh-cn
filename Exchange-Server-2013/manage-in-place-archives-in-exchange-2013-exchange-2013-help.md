---
title: '在 Exchange 2013 中管理就地存档: Exchange 2013 Help'
TOCTitle: 在 Exchange 2013 中管理就地存档
ms:assetid: 49ef4a3e-d209-4fb2-80a3-6132b0f69bd0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ651146(v=EXCHG.150)
ms:contentKeyID: 50490489
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在 Exchange 2013 中管理就地存档

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-02-01_

“就地存档”有助于您重新获得对组织的邮件数据的控制，而无需个人存储 (.pst) 文件，并且可让您满足组织的邮件保留和电子数据展示需求。启用存档时，用户可以将邮件存储在存档邮箱（可使用 MicrosoftOutlook 和 Outlook Web App 访问）中。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“就地存档”条目。

  - 不支持将用户的主邮箱驻留在比用户存档更早的 Exchange 版本上。如果用户的主邮箱仍然位于 Exchange 2010 上，在将存档移至 Exchange 2013 的同时，必须将主邮箱移至 Exchange 2013。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 创建邮箱并启用内部部署存档

## 使用 EAC

1.  导航到“收件人”\>“邮箱”。

2.  单击“新建”\>“用户邮箱”。

3.  在“新建用户邮箱”页面中，在“别名”框中键入此用户的别名。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您将此框保留为空，则会对别名使用您在“用户登录名”框中键入的值。</td>
    </tr>
    </tbody>
    </table>


4.  
    
    选择下列选项之一：
    
      - **现有用户**   单击此按钮然后单击“浏览”可打开“选择用户 – 整个林”对话框。此对话框显示尚未启用邮件功能或没有 Exchange 邮箱的林中的 Active Directory 用户帐户的列表。选择想要为其启用邮件功能的用户帐户，然后单击“确定”。如果选择此选项，则不必提供用户帐户信息，因为这些信息已存在于 Active Directory 中。
    
      - **新建用户**   单击此按钮可在 Active Directory 中创建一个新的用户帐户，并为此用户创建一个邮箱。如果您选择此选项，则必须提供必需的用户帐户信息。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>与用户邮箱关联的 Active Directory 帐户必须与 Exchange 服务器驻留在相同的林中。要为受信任的林中存在的用户帐户创建邮箱，必须创建一个链接邮箱。有关详细信息，请参阅<a href="manage-linked-mailboxes-exchange-2013-help.md">管理链接的邮箱</a>。</td>
    </tr>
    </tbody>
    </table>


5.  
    
    单击“更多选项”配置下列设置。
    
      - **邮箱数据库**   单击“浏览”选择用于存储邮箱的邮箱数据库。如果未选择数据库，Exchange 将会自动分配一个数据库。
    
      - **存档**   选择此复选框为邮箱创建存档邮箱。如果创建存档邮箱，则邮箱项目将基于默认保留策略设置（或定义的这些内容）自动从主邮箱移动到存档。
        
        单击“浏览”以选择位于本地林中的数据库，用于存储存档邮箱。
        
        若要了解详细信息，请参阅[Exchange 2013 中的就地存档](in-place-archiving-in-exchange-2013-exchange-2013-help.md)。
    
      - **通讯簿策略**   使用此列表可为邮箱选择通讯簿策略 (ABP)。ABP 包含一个全局地址列表 (GAL)、一个脱机通讯簿 (OAB)、一个会议室列表以及一组地址列表。在分配给邮箱用户时，ABP 使这些用户可以访问 Outlook 和 Outlook Web App 中的自定义 GAL。若要了解详细信息，请参阅[通讯簿策略](address-book-policies-exchange-2013-help.md)。

6.  
    
    完成后，请单击“保存”创建邮箱。

## 使用命令行管理程序

此示例在 Active Directory 中创建用户 Chris Ashton，在邮箱数据库 DB01 中创建邮箱并启用存档。下次登录时，必须重置密码。为了设置密码的初始值，此示例创建变量 ($password)，并提示您输入密码，然后将该密码作为 SecureString 对象指定给此变量。

    $password = Read-Host "Enter password" -AsSecureString
    New-Mailbox -UserPrincipalName chris@contoso.com -Alias chris -Archive -Database "DB01" -Name ChrisAshton -OrganizationalUnit Users -Password $password -FirstName Chris -LastName Ashton -DisplayName "Chris Ashton" 

有关语法和参数的详细信息，请参阅 [New-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997663\(v=exchg.150\))。

## 您如何知道这有效？

要验证通过使用内部部署存档是否成功创建了用户邮箱，可进行以下操作之一：

  - 在 EAC 中，导航到“收件人”\>“邮箱”，然后从列表中选择新的用户邮箱。在详细信息窗格中的“就地存档”下，确认已将其设置为“启用”。单击“查看详细信息”以查看存档属性，包括存档状态和在其中创建存档的邮箱数据库。

  - 在此命令行管理程序中，运行以下命令可显示有关新用户邮箱和存档的相关信息。
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress,*Archive*

  - 在此命令行管理程序中，使用 **Test-ArchiveConnectivity** cmdlet 测试存档连接情况。有关如何测试存档连接情况的示例，请参阅 [Test-ArchiveConnectivity](https://technet.microsoft.com/zh-cn/library/hh529914\(v=exchg.150\)) 中的示例部分。

## 对现有邮箱启用内部部署存档

此外，还可为已有邮箱但未启用存档的现有用户创建存档。这就是为现有邮箱*启用存档*。

## 使用 EAC

1.  导航到“收件人”\>“邮箱”。

2.  选择邮箱。

3.  在详细信息窗格中的“就地存档”下，单击“启用”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>也可以通过选择多个邮箱（使用 Shift 或 Ctrl 键）批量启用存档。选择多个邮箱后，在详细信息窗格中，单击“更多选项”。然后在“存档”下单击“启用”。</td>
    </tr>
    </tbody>
    </table>


4.  在“创建就地存档”页面上，单击“确定”让 Exchange 自动为存档选择邮箱数据库，或单击“浏览”指定一个数据库。

## 使用命令行管理程序

本示例为 Tony Smith 的邮箱启用存档。

    Enable-Mailbox "Tony Smith" -Archive

本示例在未启用内部部署或基于云的存档以及没有以 DiscoverySearchMailbox 开头的名称的数据库 DB01 中检索邮箱。它通过管道将结果传递给 **Enable-Mailbox** cmdlet，以对邮箱数据库 DB01 中的所有邮箱启用存档。

    Get-Mailbox -Database DB01 -Filter {ArchiveGuid -Eq $null -AND ArchiveDomain -eq $null -AND Name -NotLike "DiscoverySearchMailbox*"} | Enable-Mailbox -Archive

有关语法和参数的详细信息，请参阅 [Enable-Mailbox](https://technet.microsoft.com/zh-cn/library/aa998251\(v=exchg.150\)) 和 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否对现有邮箱成功启用了内部部署，可执行以下操作之一：

  - 在 EAC 中，导航到“收件人”\>“邮箱”，然后从列表中选择邮箱。在详细信息窗格中的“就地存档”下，确认已将其设置为“启用”。单击“查看详细信息”以查看存档属性，包括存档状态和在其中创建存档的邮箱数据库。

  - 在此命令行管理程序中，运行以下命令可显示有关新存档的相关信息。
    
        Get-Mailbox <Name> | FL Name,*Archive*

  - 在此命令行管理程序中，使用 **Test-ArchiveConnectivity** cmdlet 测试存档连接情况。有关如何测试存档连接情况的示例，请参阅 [Test-ArchiveConnectivity](https://technet.microsoft.com/zh-cn/library/hh529914\(v=exchg.150\)) 中的示例。

## 禁用内部部署存档

您可能需要禁用用户的存档以便进行故障排除，或者为了将邮箱移动到不支持就地存档的 Exchange 版本。如果禁用内部部署存档，则该存档中的所有信息将保留在邮箱数据库中，直到超过邮箱保留时间并永久删除内部部署存档。（默认情况下，Exchange 会将断开连接的邮箱（包括存档邮箱）保留三十天。）

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>禁用存档后将从邮箱中删除存档，并在邮箱数据库中将其标记为删除。</td>
</tr>
</tbody>
</table>


如果要将内部部署存档重新连接到该邮箱，可使用 [Connect-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997878\(v=exchg.150\)) cmdlet 和 *Archive* 参数。

## 使用 EAC

1.  导航到“收件人”\>“邮箱”。

2.  选择邮箱。

3.  在详细信息窗格中的“就地存档”下，单击“禁用”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>也可以通过选择多个邮箱（使用 Shift 或 Ctrl 键）批量禁用存档。选择多个邮箱后，在详细信息窗格中，单击“更多选项”。然后在“存档”下单击“禁用”。</td>
    </tr>
    </tbody>
    </table>


## 使用命令行管理程序

本示例禁用的是 Chris Ashton 的邮箱的存档。它不禁用邮箱。

    Disable-Mailbox -Identity "Chris Ashton" -Archive

有关语法和参数的详细信息，请参阅 [Disable-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997210\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否已成功禁用存档，请执行以下操作：

  - 在 EAC 中，选择邮箱。然后，在详细信息窗格中，检查“就地存档”下的存档状态。

  - 在此命令行管理程序中，运行以下命令检查邮箱用户的存档属性。
    
        Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*
    
    如果已禁用存档，则会返回下列与存档相关的属性值。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>属性</th>
    <th>值</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>ArchiveDatabase（针对内部部署存档）</p></td>
    <td><p>&lt;留空&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>ArchiveState</p></td>
    <td><p><code>None</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>DisabledArchiveDatabase（针对内部部署存档）</p></td>
    <td><p>&lt;邮箱数据库的名称&gt;</p></td>
    </tr>
    <tr class="even">
    <td><p>DisabledArchiveGuid</p></td>
    <td><p>&lt;禁用存档的 GUID&gt;</p></td>
    </tr>
    </tbody>
    </table>


## 连接内部部署存档

禁用存档邮箱后，它将断开连接。已断开连接的存档邮箱将在邮箱数据库中保留一段指定的时间。默认情况下，Exchange 会将已断开连接的存档保留 30 天。在此期间，可以通过将存档与现有邮箱相关联来恢复存档。可以修改已删除邮箱的保留期限，以延长或缩短删除邮箱或存档的保留期限。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果对用户禁用存档，然后对该相同用户启用存档，则用户将获取一个新存档。新存档将不包含用户已断开连接的存档中的数据。如果要将用户重新连接到他或她的已断开连接的存档，则必须执行此过程。</td>
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
<td>不能使用 EAC 将已断开连接的存档连接到邮箱用户。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序

1.  如果您不知道存档的名称，则可以通过运行以下命令在命令行管理程序中对其进行查看。本示例检索邮箱数据库 DB01，并将它通过管道传递给 **Get-MailboxStatistics** cmdlet，以检索数据库中所有邮箱的邮箱统计信息，然后使用 **Where-Object** cmdlet 筛选结果，并检索已断开连接的存档列表。此命令会显示有关每个存档的其他信息（如 GUID 和项目计数）。
    
        Get-MailboxDatabase "DB01" | Get-MailboxStatistics | Where {($_.DisconnectDate -ne $null) -and ($_.IsArchiveMailbox -eq $true)} | Format-List

2.  将存档连接到主邮箱。本示例将 Chris Ashton 的存档连接到其主邮箱，并将 GUID 用作该存档的标识。
    
        Enable-Mailbox -ArchiveGuid "8734c04e-981e-4ccf-a547-1c1ac7ebf3e2" -ArchiveDatabase "DB01" -Identity "Chris Ashton"

有关语法和参数的详细信息，请参阅下列主题：

  - [Get-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb124924\(v=exchg.150\))

  - [Get-MailboxStatistics](https://technet.microsoft.com/zh-cn/library/bb124612\(v=exchg.150\))

  - [Enable-Mailbox](https://technet.microsoft.com/zh-cn/library/aa998251\(v=exchg.150\))

## 您如何知道这有效？

要验证是否已将断开连接的存档成功连接到邮箱用户，请运行以下命令行管理程序命令检索邮箱用户的存档属性，并验证 *ArchiveGuid* 和 *ArchiveDatabase* 返回的属性值：

    Get-Mailbox -Identity "Chris Ashton" | Format-List *Archive*

