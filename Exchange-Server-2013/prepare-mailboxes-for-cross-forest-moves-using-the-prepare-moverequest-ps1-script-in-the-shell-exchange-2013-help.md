---
title: '在命令行管理程序中使用 Prepare-MoveRequest.ps1 脚本准备跨林移动的邮箱: Exchange 2013 Help'
TOCTitle: 在命令行管理程序中使用 Prepare-MoveRequest.ps1 脚本准备跨林移动的邮箱
ms:assetid: 2cea59fb-69b7-4a2f-833f-de4d93cf1810
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee861103(v=EXCHG.150)
ms:contentKeyID: 50490128
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在命令行管理程序中使用 Prepare-MoveRequest.ps1 脚本准备跨林移动的邮箱

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2017-11-22_

**摘要：**  了解如何在Exchange 命令行管理程序中使用准备 MoveRequest.ps1 脚本管理跨目录林的邮箱移动和Exchange 2013的迁移。

Microsoft Exchange 2013支持邮箱移动和迁移使用的**New-MoveRequest**和**New-MigrationBatch**的 cmdlet。您还可以通过 Exchange 管理中心 (EAC) 移动邮箱。您可以移动 Exchange 2013 邮箱的 Exchange 2010 来自源Exchange林到目标的Exchange 2013目录林。

要运行 **New-MoveRequest** 和 **New-MigrationBatch** cmdlet，某个邮件用户必须存在于目标 Exchange 林中，并且该邮件用户必须拥有至少一组必需的 Active Directory 属性。

本主题中介绍的示例 Windows PowerShell 脚本支持此任务，具体方法是将 Exchange 2013 源林中的邮箱用户作为启用邮件的用户与 Exchange 2013 目标林同步。该脚本将源林中的邮箱用户的 Active Directory 属性复制到目标林，然后使用 **Update-Recipient** cmdlet 将这些目标对象转换为启用邮件的用户。

有关使用和编写脚本的详细信息，请参阅[使用 Exchange 命令行管理程序编写脚本](https://technet.microsoft.com/zh-cn/library/bb123798\(v=exchg.150\))。有关为跨林移动做准备的详细信息，请参阅[为跨林移动请求准备邮箱](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)。

要查找与远程移动请求相关的其他管理任务吗？请查看[管理内部部署移动](manage-on-premises-moves-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 在以下位置找到该脚本：Program Files\\Microsoft\\Exchange Server\\V15\\Scripts

  - 若要运行该示例脚本，您需要以下各项：
    
      - Exchange源目录林，当前驻留邮箱。这可以是一个 Exchange 2010 或 Exchange 2013 的邮箱。
    
      - 安装了 Exchange 2013 的目标林，这是邮箱将要移动到的位置。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用 Prepare-MoveRequest.ps1 脚本为跨林移动准备邮箱

从命令行管理程序对目标 Exchange 2013 林中某个运行 Exchange 2013 的服务器角色运行该脚本。该脚本会从源林中复制邮箱属性。

若要为远程林域控制器分配特定身份验证凭据，必须首先运行 Windows PowerShell **Get-Credential** cmdlet，并在临时变量中存储用户输入。运行 **Get-Credential** cmdlet 时，该 cmdlet 会要求输入在对远程林域控制器进行身份验证期间使用的帐户用户名和密码。随后您便可以在 Prepare-MoveRequest.ps1 脚本中使用临时变量。有关 **Get-Credential** cmdlet 的详细信息，请参阅 [Get-Credential](https://go.microsoft.com/fwlink/p/?linkid=142122)。

> [!NOTE]  
> 请确保在调用此脚本时，对本地林和远程林使用两个不同的凭据。


1.  运行以下命令以获取本地林和远程林凭据。
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  运行以下命令将凭据信息传递给 Prepare-MoveRequest.ps1 脚本中的 *LocalForestCredential* 和 *RemoteForestCredential* 参数。
    
        Prepare-MoveRequest.ps1 -Identity JohnSmith@Fabrikan.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials

## 脚本的参数集

下表介绍了该脚本的参数集。

### Prepare-MoveRequest.ps1 脚本的参数集

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>必需</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>必需</p></td>
<td><p><em>Identity</em> 参数唯一标识源林中的邮箱。标识可以为以下任何一项：</p>
<ul>
<li><p>公用名 (CN)</p></li>
<li><p>别名</p></li>
<li><p><strong>proxyAddress</strong> 属性</p></li>
<li><p><strong>objectGuid</strong> 属性</p></li>
<li><p><strong>DisplayName</strong> 属性</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>RemoteForestCredential</em></p></td>
<td><p>必需</p></td>
<td><p><em>RemoteForestCredential</em> 参数指定有权从源林 Active Directory 中复制数据的管理员。</p></td>
</tr>
<tr class="odd">
<td><p><em>RemoteForestDomainController</em></p></td>
<td><p>必需</p></td>
<td><p><em>RemoteForestDomainController</em> 参数指定邮箱所在源林中的域控制器。</p></td>
</tr>
<tr class="even">
<td><p><em>DisableEmailAddressPolicy</em></p></td>
<td><p>可选</p></td>
<td><p><em>DisableEmailAddressPolicy</em> 参数指定在目标林中创建 <strong>MailUser</strong> 对象时是否应禁用电子邮件地址策略 (EAP)。</p>
<p>当指定此参数时，不会应用目标林中的 EAP。</p>

> [!NOTE]  
> 当指定此参数时，<strong>MailUser</strong> 对象的本地林域中的电子邮件地址映射不会具有标记。这通常由 EAP 进行标记。

</td>
</tr>
<tr class="odd">
<td><p><em>LinkedMailUser</em></p></td>
<td><p>可选</p></td>
<td><p><em>LinkedMailUser</em> 开关指定是否在本地林中为远程林中的邮箱用户创建链接的 MailUser。</p>
<p>如果提供该开关，则脚本会创建链接到源邮箱的目标 <strong>MailUser</strong> 对象。如果省略该开关，则脚本会创建常规的目标 <strong>MailUser</strong> 对象。</p></td>
</tr>
<tr class="even">
<td><p><em>LocalForestCredential</em></p></td>
<td><p>可选</p></td>
<td><p><em>LocalForestCredential</em> 参数指定有权将数据写入目标林 Active Directory 的管理员。</p>
<p>建议您显式指定此参数以避免 Active Directory 权限问题。</p>
<p>如果远程林和本地林配置了受信任关系，请勿使用远程林中的用户帐户作为本地林凭据，即使远程用户帐户可能有权修改本地林中的 Active Directory 也是如此。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalForestDomainController</em></p></td>
<td><p>可选</p></td>
<td><p><em>LocalForestDomainController</em> 参数指定目标林（将在其中创建启用邮件的用户）中的域控制器。</p>
<p>建议您指定此参数以避免在本地林中出现可能的域控制器复制延迟问题（如果选择了随机域控制器，则可能出现这些问题）。</p></td>
</tr>
<tr class="even">
<td><p><em>MailboxDeliveryDomain</em></p></td>
<td><p>可选</p></td>
<td><p><em>MailboxDeliveryDomain</em> 参数指定源林的权威域，以便脚本可以选择正确源邮箱用户的 <strong>proxyAddress</strong> 属性作为启用邮件的目标用户的 <strong>targetAddress</strong> 属性。</p>
<p>默认情况下，源邮箱用户的主 SMTP 地址设置为启用邮件的目标用户的 <strong>targetAddress</strong> 属性。</p></td>
</tr>
<tr class="odd">
<td><p><em>OverWriteLocalObject</em></p></td>
<td><p>可选</p></td>
<td><p><em>OverWriteLocalObject</em> 参数用于由 Active Directory 迁移工具创建的用户。属性会由现有邮件联系人复制到新创建的邮件用户。但是在此复制之后，脚本还会将属性从源林用户复制到新创建的邮件用户。</p></td>
</tr>
<tr class="even">
<td><p><em>TargetMailUserOU</em></p></td>
<td><p>可选</p></td>
<td><p><em>TargetMailuserOU</em> 参数指定在其下创建启用邮件的目标用户的组织单位 (OU)。</p></td>
</tr>
<tr class="odd">
<td><p><em>UseLocalObject</em></p></td>
<td><p>可选</p></td>
<td><p><em>UseLocalObject</em> 参数指定在脚本检测到本地林中的对象与即将创建的启用邮件的用户冲突时，是否将现有本地对象转换为所需的启用邮件的目标用户。</p></td>
</tr>
</tbody>
</table>


## 示例

本节包含有关如何使用 Prepare-MoveRequest.ps1 脚本的几个示例。

## 示例：单个启用邮件的链接用户

当远程林与本地林之间存在林信任时，此示例在本地林中设置一个启用邮件的链接用户。

1.  运行以下命令以获取本地林和远程林凭据。
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  运行以下命令将凭据信息传递给 Prepare-MoveRequest.ps1 脚本中的 *LocalForestCredential* 和 *RemoteForestCredential* 参数。
    
        Prepare-MoveRequest.ps1 -Identity JamesAlvord@Contoso.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials -LinkedMailUser 

## 示例：管道传输

如果您提供邮箱标识的列表，则此示例支持管道传输。

1.  运行以下命令。
    
        $UserCredentials = Get-Credential

2.  运行以下命令将凭据信息传递给 Prepare-MoveRequest.ps1 脚本中的 *RemoteForestCredential* 参数。
    
        "IanP@Contoso.com", "JoeAn@Contoso.com" | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## 示例：使用 .csv 文件批量创建启用邮件的用户

您可以生成一个 .csv 文件，其中包含源林中的邮箱标识的列表，从而使您可以将此文件的内容通过管道传输到脚本中，以批量创建启用邮件的目标用户。

例如，该 CSV 文件的内容可以是：

Identity

Ian@contoso.com

John@contoso.com

Cindy@contoso.com

此示例调用一个 .csv 文件以批量创建启用邮件的目标用户。

1.  运行以下命令以获取远程林凭据。
    
        $UserCredentials = Get-Credential

2.  运行以下命令将凭据信息传递给 Prepare-MoveRequest.ps1 脚本中的 *RemoteForestCredential* 参数。
    
        Import-Csv Test.csv | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## 每个目标对象的脚本行为

本节介绍对于若干目标对象方案如何执行脚本。

## 重复的启用邮件的目标对象

当脚本尝试根据源邮箱用户创建启用邮件的目标用户，并且检测到重复的启用邮件的本地用户时，会使用以下逻辑：

  - 如果源邮箱用户的 **masterAccountSid** 属性等于任何目标对象的 **objectSid** 或 **masterAccountSid** 属性：
    
      - 如果目标对象未启用邮件，则脚本会返回错误，因为脚本不支持将未启用邮件的对象转换为启用邮件的用户。
    
      - 如果目标对象启用了邮件，则目标对象是重复的。

  - 如果源邮箱用户的 **proxyAddress** 属性（仅限 smtp/x500）中的地址等于目标对象的 **proxyAddress** 属性（仅限 smtp/x500）中的地址，则目标对象是重复的。

脚本会提示用户存在重复对象。

如果启用邮件的目标对象为启用邮件的用户或联系人（最可能由跨林（基于 Identity Lifecycle Management 2007 Service Pack 1）全局地址列表 (GAL) 同步部署创建），则用户可以使用 *UseLocalObject* 参数再次运行脚本，以将启用邮件的目标对象用于邮箱迁移。

## 启用邮件的用户

如果目标对象为启用邮件的用户，则脚本会将以下属性从源邮箱用户复制到启用邮件的目标用户：

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

如果设置了 *LinkedMailUser* 参数，则脚本会复制源 **objectSid**/**masterAccountSid** 属性。

## 启用邮件的联系人

如果目标对象为启用邮件的联系人，则脚本会删除现有联系人并将其所有属性复制到启用邮件的新用户。脚本还会从源邮箱用户复制以下属性：

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

  - **sAMAccountName**

  - **userAccountControl**（设置为 514 //等效于 0x202，ACCOUNTDISABLE | NORMAL\_ACCOUNT）

  - **userPrincipalName**

如果设置了 *LinkedMailUser* 参数，则脚本会复制源 **objectSid**/**masterAccountSid** 属性。

## LegacyExchangeDN 属性

在调用 **Update-Recipient** cmdlet 以将目标对象转换为启用邮件的用户时，会为启用邮件的目标用户生成新的 **LegacyExchangeDN** 属性。脚本会将启用邮件的目标用户的 **LegacyExchangeDN** 属性作为 x500 地址复制到源邮箱用户的 **proxyAddress** 属性。

