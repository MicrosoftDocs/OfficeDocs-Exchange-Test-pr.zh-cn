---
title: '从托管文件夹迁移: Exchange 2013 Help'
TOCTitle: 从托管文件夹迁移
ms:assetid: 6796a79d-501e-4216-9370-77965bc5835d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298032(v=EXCHG.150)
ms:contentKeyID: 52061511
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 从托管文件夹迁移

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

在 Microsoft Exchange Server 2013 中，邮件传递记录管理 (MRM) 的执行通过使用保留标记和保留策略来进行。保留策略是一组可以应用到邮箱的保留标记。有关更多详细信息，请参阅[保留标记和保留策略](https://technet.microsoft.com/zh-cn/library/dd297955(v=exchg.150))。作为在 Exchange Server 2007 中引入的 MRM 技术，托管文件夹在此处不受支持。

应用了托管文件夹邮箱策略的邮箱可以进行迁移，从而使用保留策略。为此，必须创建与链接至用户托管文件夹邮箱策略的托管文件夹等效的保留标记。

> [!IMPORTANT]  
> 在生产环境中从托管文件夹迁移到保留策略之前，建议您先在测试环境中测试此过程。


> [!TIP]  
> 您可以将邮箱置于保留挂起，暂停对保留策略或托管文件夹邮箱策略的处理。在迁移场景中，将邮箱置于保留挂起非常有用，可避免在测试邮箱或少数生产邮箱上测试新策略设置之前删除邮件或移动邮件至存档。有关详细信息，请参阅<a href="https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/messaging-records-management/mailbox-retention-hold">放置的邮箱上保留挂起</a>。


有关与 MRM 相关的其他管理任务，请参阅[邮件记录管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 比较保留标记与托管文件夹

托管文件夹需要用户根据保留设置将项目移动至托管文件夹中。与此不同的是，保留标记可以应用于邮箱中的文件夹或单个项目。此过程对用户工作流和电子邮件组织方法的影响最小。如果文件夹应用了保留标记，则其中的所有项目将继承保留设置。通过向文件夹中的单个项目应用不同的保留标记，用户可以进一步指定保留设置。

托管文件夹支持对文件夹进行不同的托管内容设置，每个都拥有不同的消息类型（如电子邮件项或日历项）。保留标记不需要单独的托管内容设置对象，因为保留设置是在标记属性中指定的。除了可以为语音邮件创建默认策略标记 (DPT) 外，不支持为特定邮件类创建保留标记。此外，保留标记不允许使用托管文件夹助理执行的日记。

> [!NOTE]  
> 用于向日记邮箱发送邮件副本和日记报告的日记规则由日记代理在传输管道中强制应用，并且独立于 MRM。有关更多详细信息，请参阅<a href="journaling-exchange-2013-help.md">日记</a>。


下表对使用保留标记或托管文件夹时可用的 MRM 功能进行了比较。

### 保留标记与托管文件夹

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>保留标记</th>
<th>托管文件夹</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>为默认文件夹（如收件箱）指定保留设置</p></td>
<td><p>使用保留策略标记 (RPT)</p></td>
<td><p>使用托管默认文件夹</p></td>
</tr>
<tr class="even">
<td><p>为整个邮箱指定保留设置</p></td>
<td><p>使用默认策略标记 (DPT)</p></td>
<td><p>使用托管默认文件夹</p></td>
</tr>
<tr class="odd">
<td><p>对自定义文件夹使用保留设置</p></td>
<td><p>使用个人标记</p></td>
<td><p>使用托管自定义文件夹</p></td>
</tr>
<tr class="even">
<td><p>需要托管内容设置</p></td>
<td><p>否（保留标记内含有保留设置）</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>对不同邮件类（如电子邮件、语音邮件或日历项）使用保留设置</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>支持&amp;quot;移动到存档&amp;quot;操作，此操作会将各项移动到用户的存档邮箱中</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>支持&amp;quot;移动到托管文件夹&amp;quot;操作</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>允许使用托管文件夹助理执行日记</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>应用于用户的策略</p></td>
<td><p>保留策略</p></td>
<td><p>托管文件夹邮箱策略</p></td>
</tr>
<tr class="even">
<td><p>可应用于邮箱用户的最大策略数</p></td>
<td><p>1</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>由托管文件夹助理处理</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>客户端支持</p></td>
<td><p>Microsoft Outlook 2010 和 OfficeOutlook Web App</p></td>
<td><p>Outlook 2010、Office Outlook 2007 和 Outlook Web App</p></td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成时间：20 分钟。

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 您无法使用 Exchange 管理中心 (EAC) 创建基于保留策略的保留标记。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 从托管文件夹迁移邮箱用户

将用户从此托管文件夹邮箱策略迁移至保留策略的一般步骤如下所示。本主题后面将详细说明各步骤：

1.  收集有关应用于所有 Exchange 2010 和 Exchange 2007 邮箱的托管文件夹邮箱策略、各策略中的托管文件夹以及各托管文件夹托管内容设置的信息。若要获取此信息，您可以在 Exchange 2010 或 Exchange 2007 服务器上使用 EMC 或命令行管理程序。

2.  为迁移创建保留标记。

3.  创建保留策略，并将新建的保留标记链接至该策略。

4.  删除该托管文件夹邮箱策略，并将此保留策略应用至用户邮箱。
    
    > [!IMPORTANT]  
    > 将保留策略应用于用户并运行托管文件夹助理后，用户邮箱中的托管文件夹将变为非托管状态。


在以下步骤中，Contoso 邮箱的下列托管文件夹应用了托管文件夹邮箱策略。

### Contoso 托管文件夹

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
<th>托管文件夹</th>
<th>托管内容设置</th>
<th>已启用保留功能</th>
<th>保留时间</th>
<th>保留操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Corp-DeletedItems</p></td>
<td><p>CS-Corp-DeletedItems</p></td>
<td><p>是</p></td>
<td><p>30 天</p></td>
<td><p>删除但允许恢复</p></td>
</tr>
<tr class="even">
<td><p>Corp-SentItems</p></td>
<td><p>CS-Corp-SentItems</p></td>
<td><p>是</p></td>
<td><p>1,825 天</p></td>
<td><p>移至&amp;quot;已删除邮件&amp;quot;</p></td>
</tr>
<tr class="odd">
<td><p>Corp-JunkMail</p></td>
<td><p>CS-Corp-JunkMail</p></td>
<td><p>是</p></td>
<td><p>30 天</p></td>
<td><p>永久删除</p></td>
</tr>
<tr class="even">
<td><p>Corp-EntireMailbox</p></td>
<td><p>CS-Corp-EntireMailbox</p></td>
<td><p>是</p></td>
<td><p>365 天</p></td>
<td><p>移至&amp;quot;已删除邮件&amp;quot;</p></td>
</tr>
<tr class="odd">
<td><p>30 天</p></td>
<td><p>CS-30Days</p></td>
<td><p>是</p></td>
<td><p>30 天</p></td>
<td><p>移至&amp;quot;已删除邮件&amp;quot;</p></td>
</tr>
<tr class="even">
<td><p>5 年</p></td>
<td><p>CS-5Years</p></td>
<td><p>是</p></td>
<td><p>1,825 天</p></td>
<td><p>移至&amp;quot;已删除邮件&amp;quot;</p></td>
</tr>
<tr class="odd">
<td><p>永不过期</p></td>
<td><p>CS-NeverExpire</p></td>
<td><p>否</p></td>
<td><p>365 天</p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>


## 您该如何做？

## 步骤 1：为迁移创建保留标记

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 主题中的\&quot;邮件传递记录管理\&quot;条目。

此步骤有两种实现方法：

  - **根据托管文件夹及其相应托管内容设置创建保留标记**   通过此方法，您需要使用 **New-RetentionPolicyTag** cmdlet 和 *ManagedFolderToUpgrade* 参数。指定此参数时，相应的保留标记将自动应用于托管文件夹。
    
    > [!IMPORTANT]  
    > 如果要移植的托管文件夹具有不同邮件类的多个托管内容设置，将只创建一个保留标记，且会将所有托管内容设置的最长保留时间用作已移植标记的保留时间，而不考虑托管内容设置的邮件类。<br />
    > 例如，查看托管文件夹 Corp-DeletedItems 的下列托管内容设置。


  - **通过手动指定保留设置创建保留标记**   通过此方法，您需要使用 **New-RetentionPolicyTag** cmdlet 而不需要使用 *ManagedFolderToUpgrade* 参数。您若不指定此参数，则添加到该策略的所有保留策略标记均将应用于默认文件夹，且默认策略标记将应用于整个邮箱。但是，任何添加到该策略的个人标记都不会自动应用于托管文件夹。

> [!NOTE]  
> 如果是在包含 Exchange 2013 和 Exchange 2010 服务器的混合环境中，您可以在 Exchange 2010 服务器的 Exchange 管理控制台 (EMC) 上使用&amp;quot;移植托管文件夹&amp;quot;向导，将托管文件夹及相应托管内容设置轻松移植至保留标记。


**根据托管文件夹创建保留标记**

本示例根据 Contoso 托管文件夹邮箱策略中显示的相应托管内容设置创建保留标记。

```PowerShell    
    New-RetentionPolicyTag Corp-DeletedItems -ManagedFolderToUpgrade Corp-DeletedItems
    New-RetentionPolicyTag Corp-SentItems -ManagedFolderToUpgrade Corp-SentItems
    New-RetentionPolicyTag Corp-JunkMail -ManagedFolderToUpgrade Corp-JunkMail
    New-RetentionPolicyTag Corp-EntireMailbox -ManagedFolderToUpgrade Corp-EntireMailbox
    New-RetentionPolicyTag 30Days -ManagedFolderToUpgrade 30Days
    New-RetentionPolicyTag 5Years -ManagedFolderToUpgrade 5Years
    New-RetentionPolicyTag NeverExpire -ManagedFolderToUpgrade NeverExpire
```    

有关语法和参数的详细信息，请参阅 [New-RetentionPolicyTag](https://technet.microsoft.com/zh-cn/library/dd335226\(v=exchg.150\))。

**手动创建保留标记**

> [!NOTE]  
> 您也可以使用 EAC 手动创建保留标记（不根据托管文件夹内的设置）。有关详细信息，请参阅<a href="https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">创建保留策略</a>。


本示例根据托管文件夹及 Contoso 托管文件夹邮箱策略中显示的相应托管内容设置创建保留标记。手动指定保留设置，无需使用 *ManagedFolderToUpgrade* 参数。

```PowerShell
    New-RetentionPolicyTag Corp-DeletedItems -Type DeletedItems -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction DeleteAndAllowRecovery
    New-RetentionPolicyTag Corp-SentItems -Type SentItems -RetentionEnabled $true -AgeLimitforRetention 1825 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag Corp-JunkMail -Type JunkMail -RetentionEnabled $true -AgeLimitforRetention 30 -RetentionAction PermanentlyDelete
    New-RetentionPolicyTag Corp-EntireMailbox -Type All -RetentionEnabled $true -AgeLimitForRetention 365 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag 30Days -Type Personal -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag 5Years -Type Personal -RetentionEnabled $true -AgeLimitForRetention 1825 -RetentionAction MoveToDeletedItems
    New-RetentionPolicyTag NeverExpire -Type Personal -RetentionEnabled $false
```    

有关语法和参数的详细信息，请参阅 [New-RetentionPolicyTag](https://technet.microsoft.com/zh-cn/library/dd335226\(v=exchg.150\))。

## 步骤 2：创建保留策略

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;邮件记录管理\&quot;条目。

> [!NOTE]  
> 您也可以使用 EAC 创建保留策略并将保留标记添加至策略。有关详细信息，请参阅<a href="https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/messaging-records-management/create-a-retention-policy">创建保留策略</a>。


本示例创建了保留策略 RP-Corp，并将新建的保留标记链接至策略。

```PowerShell
New-RetentionPolicy RP-Corp -RetentionPolicyTagLinks Corp-DeletedItems,Corp-SentItems,Corp-JunkMail,Corp-EntireMailbox,30Days,NeverExpire
```            

有关语法和参数的详细信息，请参阅 [New-RetentionPolicy](https://technet.microsoft.com/zh-cn/library/dd297970\(v=exchg.150\))。

## 步骤 3：删除用户邮箱的托管文件夹邮箱策略

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;应用保留策略\&quot;条目。

此示例从 Ken Kwok 的邮箱中删除了托管文件夹邮箱策略和所有托管文件夹。含有任意邮件的托管文件夹并未删除。

```powershell
Set-Mailbox -Identity Kwok -RemoveManagedFolderAndPolicy RP-Corp
```

## 步骤 4：将保留策略应用于用户邮箱

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;应用保留策略\&quot;条目。

> [!NOTE]  
> 您也可以使用 EAC 将保留策略应用于用户。有关详细信息，请参阅<a href="https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/messaging-records-management/apply-retention-policy">将保留策略应用于邮箱</a>。


本示例将新建的保留策略 RP-Corp 应用于邮箱用户 Ken Kwok。

```powershell
Set-Mailbox -Identity Kwok -RetentionPolicy RP-Corp
```

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 您如何知道此任务有效？

若要验证是否已从托管文件夹迁移至保留策略，请执行以下操作：

  - 生成包含所有用户邮箱及所应用保留策略的报告。
    
    此命令可以检索应用于组织中所有邮箱的保留策略，及其保留挂起状态。
    

    ```PowerShell 
    Get-Mailbox -ResultSize unlimited -Filter {Name -NotLike "DiscoverySearch*�?} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto
    ```

  - 在托管文件夹助理采用保留策略处理邮箱之后，使用 [Get-RetentionPolicyTag](https://technet.microsoft.com/zh-cn/library/dd298009\(v=exchg.150\)) cmdlet 检索用户邮箱中设置的保留标记。
    
    此命令可检索实际应用于 April Stewart 邮箱的保留标记。
    
    ```powershell
    Get-RetentionPolicyTag -Mailbox astewart
    ```


