---
title: '为跨林移动请求准备邮箱: Exchange 2013 Help'
TOCTitle: 为跨林移动请求准备邮箱
ms:assetid: fdbed4fc-a77e-40d5-a211-863b05d74784
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee633491(v=EXCHG.150)
ms:contentKeyID: 50492027
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 为跨林移动请求准备邮箱

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2017-11-22_

**摘要：**  了解如何准备在Exchange 2013的跨目录林移动邮箱。

Microsoft Exchange 2013支持邮箱移动和迁移使用 Exchange 管理外壳，特别是**New-MoveRequest**和**New-MigrationBatch**的 cmdlet。您还可以通过 Exchange 管理中心 (EAC) 移动邮箱。请注意，可以将 Exchange 2010 和 Exchange 2013 的邮箱移动到 Exchange 2013 林。

若要将邮箱从Exchange目录林移动到Exchange 2013林， Exchange 2013目标目录林中必须包含有效的已启用邮件的用户具有一组指定的Active Directory属性。如果至少一个Exchange 2013客户端访问服务器部署在林中，林中被视为Exchange 2013林。

要准备移动邮箱，必须在目标林中创建具有所需属性且启用邮件的用户。下面是用于创建具有所需属性且启用邮件的用户的两种推荐方法：

  - 如果已为跨林全局地址列表 (GAL) 同步部署了 Microsoft Identity Lifecycle Manager (ILM)，则创建启用邮件的用户的推荐方法是，使用 ILM 2007 Feature Pack 1 (FP1) Service Pack 1 (SP1)。我们已创建了示例代码，您可以使用此示例代码了解如何自定义 ILM 同步源邮箱用户和目标邮件用户。
    
    有关包括如何下载示例代码的详细信息，请参阅[使用示例代码准备跨林移动的邮箱](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)。

  - 如果您使用 ILM/MIIS 之外的 Active Directory 创建邮箱用户，使用带 *Identity* 参数的 **Update-Recipient** cmdlet 运行地址列表服务，以为目标邮件用户生成 **LegacyExchangeDN**。我们创建了一个 Windows PowerShell 脚本示例，以读取和写入 Active Directory 并调用 **Update-Recipient** cmdlet。
    
    有关此脚本示例的详细信息，请参阅[在命令行管理程序中使用 Prepare-MoveRequest.ps1 脚本准备跨林移动的邮箱](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)。

创建完目标邮件用户之后，则可以通过运行 **New-MoveRequest** 或 **New-MigrationBatch** cmdlet 将邮箱移动到目标 Exchange 2013 林。

有关远程移动请求的详细信息，请参阅下列主题：

  - [New-MigrationBatch](https://technet.microsoft.com/zh-cn/library/jj219166\(v=exchg.150\))

  - [New-MoveRequest](https://technet.microsoft.com/zh-cn/library/dd351123\(v=exchg.150\))

有关远程邮箱移动和远程旧版邮箱移动的详细信息，请参阅[Exchange 2013 中的邮箱移动](mailbox-moves-in-exchange-2013-exchange-2013-help.md)。

本主题的剩余部分介绍了邮箱移动所需的 Active Directory 邮件用户属性。当您使用代码或脚本以准备邮箱移动时配置这些属性。但是，您可以使用 Active Directory 编辑器手动复制这些属性。

## 移动邮箱时必需的 Active Directory 用户属性

要支持远程邮箱移动，目标 Exchange 2013 林中的邮件用户对象必须具有本节中所介绍的以下 Active Directory 属性：

  - 强制属性

  - 可选属性

  - 链接的属性

  - 链接的用户属性

  - 资源邮箱属性

  - 附加属性

## 强制属性

下表列出了为确保 **New-MoveRequest** cmdlet 正常运行，需要在 ILM 中对目标邮件用户配置的最少的一组属性。

### 邮件用户的属性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>邮件用户的 Active Directory 属性</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>displayName</strong></p></td>
<td><p>复制源邮箱的相应属性或生成新值。</p></td>
</tr>
<tr class="even">
<td><p><strong>Mail</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>mailNickname</strong></p></td>
<td><p>复制源邮箱的相应属性或生成新值。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchArchiveGUID and msExchArchiveName</strong></p></td>
<td><p>直接复制源邮箱的相应属性。仅当源邮箱为 Exchange 2010 时，这些属性才可用。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMailboxGUID</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>-2147483642（十进制）//等于 0x80000006（十六进制）。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientTypeDetails</strong></p></td>
<td><p>128（十进制）/0x80（十六进制）。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUserCulture</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchVersion</strong></p></td>
<td><p>44220983382016（十进制）。</p></td>
</tr>
<tr class="even">
<td><p><strong>cn</strong></p></td>
<td><p>复制源邮箱的相应属性或生成新值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>proxyAddresses</strong></p></td>
<td><p>复制源邮箱的 <strong>proxyAddresses</strong> 属性。此外，复制源邮箱的 <strong>LegacyExchangeDN</strong> 作为目标邮件用户的 <strong>proxyAddresses</strong> 属性中的 X500 地址。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>源邮箱用户的 <strong>proxyAddresses</strong> 必须含有与目标林的权威域相匹配的 SMTP 地址。这将允许 <strong>New-MoveRequest</strong> cmdlet 正确选择已启用源邮件的用户（此用户为完成邮箱移动请求后从源邮箱用户转换而来的用户）的 <strong>targetAddress</strong>，从而确保邮件路由继续进行下去。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><strong>sAMAccountName</strong></p></td>
<td><p>复制源邮箱的相应属性或生成新值。</p>
<p>确保该值在目标邮件用户所属的目标林域中是唯一的。</p></td>
</tr>
<tr class="odd">
<td><p><strong>targetAddress</strong></p></td>
<td><p>将此属性设置为源邮箱的 <strong>proxyAddresses</strong> 属性中的 SMTP 地址。</p>
<p>此 SMTP 地址必须属于源林的权威域。</p></td>
</tr>
<tr class="even">
<td><p><strong>userAccountControl</strong></p></td>
<td><p>常量：514 //等于 0x202, ACCOUNTDISABLE | NORMAL_ACCOUNT。</p></td>
</tr>
<tr class="odd">
<td><p><strong>userPrincipalName</strong></p></td>
<td><p>复制源邮箱的相应属性或生成新值。因为已禁用邮件用户登录，所以，未使用此 <strong>userPrincipalName</strong>。</p></td>
</tr>
</tbody>
</table>


## 可选特性

不必为确保 **New-MoveRequest** cmdlet 正常运行而配置下列属性；但是，在移动邮箱后同步这些属性可以提供更好的端到端用户体验。由于目标林中的 GAL 会显示此目标邮件用户，因此，您应设置下列与 GAL 相关的属性。

### 与 GAL 相关的属性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>邮件用户的 Active Directory 属性</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>c</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>co</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>countryCode</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>company</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>department</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>facsimileTelephoneNumber</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>givenName</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>homePhone</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>info</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>initials</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>l</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>mobile</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchAssistantName</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchHideFromAddressLists</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherHomePhone</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>otherTelephone</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>pager</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>physicalDeliveryOfficeName</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalCode</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>sn</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>st</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>streetAddress</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>telephoneAssistant</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>telephoneNumber</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>title</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
</tbody>
</table>


## 链接的属性

链接的属性是引用本地林中的其他 Active Directory 对象的 Active Directory 属性。您无法直接将链接的属性值从源林中的邮箱复制到目标林中的邮件用户。首先，必须在源林中找到源邮箱属性引用的 Active Directory 对象。然后，必须在目标林中找到与上面提到的源林中的 Active Directory 对象相对应的 Active Directory 对象。最后，将目标邮件用户的属性设置为引用目标林中的 Active Directory 对象。

### 链接的属性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>邮件用户的 Active Directory 属性</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>altRecipient</strong></p></td>
<td><p>对应于源邮箱的 <strong>altRecipient</strong> 属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>deliverAndRedirect</strong></p></td>
<td><p>直接复制源邮箱的相应属性。此属性是一个布尔值，应与 <strong>altRecipient</strong> 同时设置。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Manager</strong>（及其反向链接）</p></td>
<td><p>对应于源邮箱的管理器属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>MemberOf</strong>（反向链接）</p></td>
<td><p>它是组成员属性的反向链接。</p></td>
</tr>
<tr class="odd">
<td><p><strong>publicDelegates</strong>（及其反向链接）</p></td>
<td><p>对应于源邮箱的 <strong>publicDelegates</strong> 属性。</p></td>
</tr>
</tbody>
</table>


## 链接的用户属性

如果希望将邮箱移动到 Exchange 2013 资源林，该资源林中的邮箱将被视为\&quot;链接的邮箱\&quot;。在这种情况下，您需要在（目标）资源林中创建一个链接的邮件用户。要创建链接的邮件用户，您需要设置下表中显示的属性。

### 链接的邮件用户属性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>邮件用户的 Active Directory 属性</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchMasterAccountHistory</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMasterAccountSid</strong></p></td>
<td><p>如果源邮箱中具有 <strong>msExchMasterAccountSid</strong>，请复制该属性。否则，复制源邮箱的 <strong>objectSid</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>常量：-1073741818（十进制）//等于 *无符号* 0xC0000006。</p></td>
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
<td>只有在源林和目标林之间存在林信任时，才能创建链接的邮箱。</td>
</tr>
</tbody>
</table>


如果禁用了源对象，且 **msExchMasterAccountSid** 属性已设置为自身（资源邮箱，共享邮箱），请勿对目标用户标记任何内容。

如果禁用了源对象，且未设置 **msExchMasterAccountSid** 属性，则邮箱无效。

如果启用了源对象，且已设置 **msExchMasterAccountSid** 属性，则邮箱无效。

## 资源邮箱属性

如果希望将资源邮箱移动到 Exchange 2013 林，则需要对目标邮件用户设置下表中显示的属性。

### 资源邮箱属性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>邮件用户的 Active Directory 属性</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>msExchRecipientDisplayType</strong></p></td>
<td><p>如果源邮箱是一个会议室邮箱：</p>
<ul>
<li><p><strong>常量</strong>   -2147481850（十进制）//等于 *无符号* 0x80000706。</p></li>
</ul>
<p>如果源邮箱是一个设备邮箱：</p>
<ul>
<li><p><strong>常量</strong>   -2147481594（十进制）//等于 *无符号* 0x80000806。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceCapacity</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceDisplay</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchResourceMetaData</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchResourceSearchProperties</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
</tbody>
</table>


## 附加属性

在 Exchange 2007 中，**Move-Mailbox** cmdlet 在移动邮箱时还复制了下表中显示的属性。根据组织需要，您可以选择复制这些属性。

### 资源邮箱属性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>邮件用户的 Active Directory 属性</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>comment</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>deletedItemFlags</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>delivContLength</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>departmentNumber</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>description</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>division</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeID</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>employeeNumber</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>employeeType</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>extensionAttribute1-15</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>homePostalAddress</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>internationalISDNNumber</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ipPhone</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>language</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>lmPwdHistory</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>localeID</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>mAPIRecipient</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>middleName</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticCompanyName</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticDepartment</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticDisplayName</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msDS-PhoneticFirstName</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msDS-PhoneticLastName</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchBlockedSendersHash</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCExpirySuspensionEnd</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchELCExpirySuspensionStart</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchELCMailboxFlags</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchExternalOOFOptions</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneFlags</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLDeleteThreshold</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLJunkThreshold</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMessageHygieneSCLQuarantineThreshold</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchMessageHygieneSCLRejectThreshold</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchMDBRulesQuota</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchPoliciesExcluded</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchSafeRecipientsHash</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>msExchSafeSendersHash</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>msExchUMSpokenName</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherFacsimileTelephoneNumber</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>otherIpPhone</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>otherMobile</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>otherPager</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>preferredDeliveryMethod</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>personalPager</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>personalTitle</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>photo</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>pOPCharacterSet</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>pOPContentFormat</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>postalAddress</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>postOfficeBox</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>primaryInternationalISDNNumber</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>primaryTelexNumber</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>showInAdvancedViewOnly</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>street</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>terminalServer</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>textEncodedORAddress</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>thumbnailLogo</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>thumbnailPhoto</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>url</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>userCert</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>userCertificate</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>userSMIMECertificate</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>wWWHomePage</strong></p></td>
<td><p>直接复制源邮箱的相应属性。</p></td>
</tr>
</tbody>
</table>

