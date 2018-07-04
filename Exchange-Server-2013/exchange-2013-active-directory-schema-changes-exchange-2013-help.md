---
title: 'Exchange 2013 Active Directory 架构更改: Exchange 2013 Help'
TOCTitle: Exchange 2013 Active Directory 架构更改
ms:assetid: 7e879e4e-1124-4a41-94d2-c64500beb24e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb738144(v=EXCHG.150)
ms:contentKeyID: 50491077
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 Active Directory 架构更改

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-05-18_

Microsoft Exchange Server 2013 添加新的并修改现有的 Active Directory 架构类和属性。本参考主题提供了一个在安装 Exchange 2013 的 RTM 版本或其任何累积更新或服务包时发生的 Active Directory 架构更改的摘要。关于 Active Directory 架构变更的更多信息，请参考 .ldf 文件。.ldf 文件位于 Exchange 安装文件中的 \\amd64\\Setup\\Data\\ 目录中。

Exchange 2013 架构更新为累积更新。每个版本均包括以前版本中包含的所有更改。这意味着如果您跳过某个版本，您仍然需要应用架构更新，即使您安装的版本不包括自己的更改。下表举例说明了何时将更新 Active Directory，以及它何时为最新状态。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>已安装的 Exchange 2013 当前版本</p></th>
<th><p>将要安装的 Exchange 2013 新版本</p></th>
<th><p>是否需要架构更新？</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Service Pack 1</p></td>
<td><p>累积更新 11</p></td>
<td><p><strong>是</strong>，需要更新。需应用 CU5、CU6 和 CU7 中包括的架构更新。</p></td>
</tr>
<tr class="even">
<td><p>累积更新 6</p></td>
<td><p>累积更新 11</p></td>
<td><p><strong>是</strong>，需要更新。需应用 CU7 中包括的架构更新。</p></td>
</tr>
<tr class="odd">
<td><p>累积更新 7</p></td>
<td><p>累积更新 11</p></td>
<td><p><strong>否</strong>，不需要更新。CU7 和 CU11 之间未进行任何更改。</p></td>
</tr>
</tbody>
</table>


> [!NOTE]
> 本主题中所述的 Active Directory 架构更改可能并不适用于 Exchange Server 的所有版本。<br />
> 要验证 Active Directory 已经准备成功，请参阅<a href="prepare-active-directory-and-domains-exchange-2013-help.md">准备 Active Directory 和域</a>中的“您如何知道这样可行？”一节。


本文档包括以下两节：

  - Exchange 2013 累积更新 CU8 及更高版本中的 Active Directory 架构更改

  - Exchange 2013 CU7 Active Directory 架构更改

  - Exchange 2013 CU6 Active Directory 架构更改

  - Exchange 2013 CU5 Active Directory 架构更改

  - Exchange 2013 SP1 Active Directory 架构更改

  - Exchange 2013 CU3 Active Directory 架构更改

  - Exchange 2013 CU2 Active Directory 架构更改

  - Exchange 2013 CU1 Active Directory 架构更改

  - Exchange 2013 RTM Active Directory 架构更改

## Exchange 2013 累积更新 CU8 及更高版本中的 Active Directory 架构更改

从 CU8 起的版本尚未对 Exchange 2013 中的 Active Directory 架构进行任何更改。包含架构更改的最近累积更新当前是 Exchange 2013 CU7。

未来的累积更新可能包含架构更改。在此处检查每个累积更新版本，查看已执行的架构更改。

## Exchange 2013 CU7 Active Directory 架构更改

本节总结了您在安装 Exchange 2013 CU7 时对 Active Directory 架构所作的更改。此部分包括下列子部分：

  - 由 Exchange 2013 CU7 修改的类

  - 由 Exchange 2013 CU7 添加的属性

## 由 Exchange 2013 CU7 修改的类

此部分包含在 Exchange 2013 CU7 中修改的类。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>类</th>
<th>更改</th>
<th>属性/类</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchStsRefreshTokensValidFrom</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMultiMailboxGUIDs</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMultiMailboxLocationsLink</p></td>
</tr>
<tr class="even">
<td><p>Group</p></td>
<td><p>add:auxiliaryClass</p></td>
<td><p>msExchMailStorage</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 CU7 添加的属性

本节包含了在 Exchange 2013 CU7 中添加的属性。

  - ms-Exch-Multi-Mailbox-GUID

  - ms-Exch-Sts-Refresh-Tokens-Valid-From

  - ms-Exch-Multi-Mailbox-Locations-Link

## Exchange 2013 CU6 Active Directory 架构更改

本节总结了您在安装 Exchange 2013 CU6 时对 Active Directory 架构所作的更改。此部分包括下列子部分：

  - 由 Exchange 2013 CU6 修改的类

  - 由 Exchange 2013 CU6 添加的属性

  - 由 Exchange 2013 CU6 修改的属性

## 由 Exchange 2013 CU6 修改的类

此部分包含在 Exchange 2013 CU6 中修改的类。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>类</th>
<th>更改</th>
<th>属性/类</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchAuxMailboxParentObjectIdLink</p></td>
</tr>
<tr class="even">
<td><p>Top</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchAuxMailboxParentObjectIdBL</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 CU6 添加的属性

本节包含了在 Exchange 2013 CU6 中添加的属性。

  - ms-Exch-Aux-Mailbox-Parent-Object-Id-Link

  - ms-Exch-Aux-Mailbox-Parent-Object-Id-BL

## 由 Exchange 2013 CU6 修改的属性

本节包含在 Exchange 2013 CU6 中修改的属性。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>更改</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Smtp-TLS-Certificate</p></td>
<td><p>replace:rangeUpper</p></td>
<td><p>1024</p></td>
</tr>
</tbody>
</table>


## Exchange 2013 CU5 Active Directory 架构更改

本节总结了您在安装 Exchange 2013 CU5 时对 Active Directory 架构所作的更改。此部分包括下列子部分：

  - 由 Exchange 2013 CU5 添加的类

  - 由 Exchange 2013 CU5 添加的属性

  - 由 Exchange 2013 CU5 修改的属性

## 由 Exchange 2013 CU5 添加的类

本节包含了添加到 Exchange 2013 CU5 中的类。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>类</th>
<th>更改</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Unified-Policy</p></td>
<td><p>ntdsSchemaAdd</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Unified-Rule</p></td>
<td><p>ntdsSchemaAdd</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 CU5 添加的属性

本节包含了在 Exchange 2013 CU5 中添加的属性。

  - ms-Exch-UG-Member-Link

  - ms-Exch-UG-Member-BL

## 由 Exchange 2013 CU5 修改的属性

本节包含了在 Exchange 2013 CU5 中修改的属性。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>更改</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Smtp-Receive-Tls-Certificate-Name</p></td>
<td><p>替换:rangeUpper</p></td>
<td><p>1024</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>替换:mayContain</p></td>
<td><p>msExchUGMemberLink</p></td>
</tr>
<tr class="odd">
<td><p>Top</p></td>
<td><p>替换:mayContain</p></td>
<td><p>msExchUGMemberBL</p></td>
</tr>
</tbody>
</table>


## Exchange 2013 SP1 Active Directory 架构更改

本节总结了您在安装 Exchange 2013 Service Pack 1 (SP1) 时对 Active Directory 架构所作的更改。此部分包括下列子部分：

  - 由 Exchange 2013 SP1 添加的类

  - 由 Exchange 2013 SP1 修改的类

  - 由 Exchange 2013 SP1 添加的属性

  - 由 Exchange 2013 SP1 添加的全局目录属性

  - 由 Exchange 2013 SP1 修改的属性

## 由 Exchange 2013 SP1 添加的类

本节包含了在 Exchange 2013 SP1 中添加的类。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>类</th>
<th>更改</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Intra-Organization-Connector</p></td>
<td><p>ntdsSchemaModify</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Client-Access-Rule</p></td>
<td><p>ntdsSchemaModify</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 SP1 修改的类

本节包含了在 Exchange 2013 SP1 中添加的属性。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>类</th>
<th>更改</th>
<th>属性/类</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxContainerGuid</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchUnifiedMailbox</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-OAB</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOABGeneratingMailboxLink</p></td>
</tr>
<tr class="even">
<td><p>Top</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOABGeneratingMailboxBL</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 SP1 添加的属性

本节包含了在 Exchange 2013 SP1 中添加的属性。

  - ms-Exch-OAB-Generating-Mailbox-Link

  - ms-Exch-OAB-Generating-Mailbox-BL

## 由 Exchange 2013 SP1 添加的全局目录属性

以下全局编录属性由 Exchange 2013 SP1 添加：

  - ms-Exch-Mailbox-Container-Guid

  - ms-Exch-Unified-Mailbox

## 由 Exchange 2013 SP1 修改的属性

本节包含了在 Exchange 2013 SP1 中修改的属性。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>更改</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ms-exch-schema-version-pt</p></td>
<td><p>rangeUpper</p></td>
<td><p>15292</p></td>
</tr>
</tbody>
</table>


## Exchange 2013 CU3 Active Directory 架构更改

本节总结了您在安装 Exchange 2013 CU3 时对 Active Directory 架构所作的更改。此部分包括下列子部分：

  - 由 Exchange 2013 CU3 添加的类

  - 由 Exchange 2013 CU3 添加的属性

  - 由 Exchange 2013 CU3 修改的属性

## 由 Exchange 2013 CU3 添加的类

本节包含了在 Exchange 2013 CU3 中添加的类。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>类</th>
<th>更改</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>msExchThrottlingPolicy</p></td>
<td><p>ntdsSchemaModify</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 CU3 添加的属性

本节包含了在 Exchange 2013 CU3 中添加的属性。

  - ms-Exch-Encryption-Throttling-Policy-State-Ex

## 由 Exchange 2013 CU3 修改的属性

本节包含了在 Exchange 2013 CU3 中修改的属性。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>更改</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Coexistence-Secure-Mail-Certificate-Thumbprintms-Exch-Sync-Cookie</p></td>
<td><p>rangeUpper</p></td>
<td><p>1024</p></td>
</tr>
</tbody>
</table>


## Exchange 2013 CU2 Active Directory 架构更改

本节总结了您在安装 Exchange 2013 CU2 时对 Active Directory 架构所作的更改。此部分包括下列子部分：

  - 由 Exchange 2013 CU2 添加的类

  - 由 Exchange 2013 CU2 修改的类

  - 由 Exchange 2013 CU2 添加的属性

  - 由 Exchange 2013 CU2 修改的属性

## 由 Exchange 2013 CU2 添加的类

本节包含了在 Exchange 2013 CU2 中添加的类。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>类</th>
<th>更改</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Config-Settings</p></td>
<td><p>ntdsSchemaAdd</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Encryption-Virtual-Directory</p></td>
<td><p>ntdsSchemaAdd</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 CU2 修改的类

本节包含了在 Exchange 2013 CU2 中修改的类。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>类</th>
<th>更改</th>
<th>属性/类</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>Add:mayContain</p></td>
<td><p>msExchTenantCountry</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>Add:mayContain</p></td>
<td><p>msExchConfigurationXML</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Account-Forest</p></td>
<td><p>Add:mayContain</p></td>
<td><p>msExchPartnerId</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 CU2 添加的属性

本节包含了在 Exchange 2013 CU2 中添加的属性。

  - ms-Exch-Tenant-Country

## 由 Exchange 2013 CU2 修改的属性

此部分包含在 Exchange 2013 CU2 中修改的属性。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>更改</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Sync-Cookie</p></td>
<td><p>rangeUpper</p></td>
<td><p>262144</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Schema-Version-Pt</p></td>
<td><p>rangeUpper</p></td>
<td><p>15281</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 CU2 添加的对象 ID

以下类对象 ID 在您安装 Exchange 2013 CU1 时添加：

  - 1.2.840.113556.1.5.7000.62.50204

  - 1.2.840.113556.1.5.7000.62.50205

以下属性对象 ID 在您安装 Exchange 2013 CU1 时添加：

  - 1.2.840.113556.1.4.7000.102.52130

## Exchange 2013 CU1 Active Directory 架构更改

本节总结了您在安装 Exchange 2013 CU1 时对 Active Directory 架构所作的更改。此部分包括下列子部分：

  - 由 Exchange 2013 CU1 修改的类

  - 由 Exchange 2013 CU1 添加的类

  - 由 Exchange 2013 CU1 修改的属性

  - 由 Exchange 2013 CU1 添加的对象 ID

  - 由 Exchange 2013 CU1 添加的已编制索引的属性

  - 由 Exchange 2013 CU1 修改的属性集

  - 由 Exchange 2013 CU1 添加的全局目录属性

## 由 Exchange 2013 CU1 修改的类

此部分包含在 Exchange 2013 CU1 中修改的类。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>类</th>
<th>更改</th>
<th>属性/类</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchArchiveRelease</p></td>
</tr>
<tr class="even">
<td><p>Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxRelease</p></td>
</tr>
<tr class="odd">
<td><p>Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchArchiveRelease</p></td>
</tr>
<tr class="even">
<td><p>Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxRelease</p></td>
</tr>
<tr class="odd">
<td><p>Exch-OAB</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchLastUpdateTime</p></td>
</tr>
<tr class="even">
<td><p>Exch-Accepted-Domain</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOfflineOrgIdHomeRealmRecord</p></td>
</tr>
<tr class="odd">
<td><p>Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCapabilityIdentifiers</p></td>
</tr>
<tr class="even">
<td><p>Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchObjectID</p></td>
</tr>
<tr class="odd">
<td><p>Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchProvisioningTags</p></td>
</tr>
<tr class="even">
<td><p>Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMaxABP</p></td>
</tr>
<tr class="odd">
<td><p>Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMaxOAB</p></td>
</tr>
<tr class="even">
<td><p>Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>pFContacts</p></td>
</tr>
<tr class="odd">
<td><p>Exch-Team-Mailbox-Provisioning-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchConfigurationXML</p></td>
</tr>
<tr class="even">
<td><p>Exch-MDB-Availability-Group</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchEvictedMembersLink</p></td>
</tr>
<tr class="odd">
<td><p>Top</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchEvictedMemebersBL</p></td>
</tr>
<tr class="even">
<td><p>Exch-On-Premises-Organization</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTrustedDomainLink</p></td>
</tr>
<tr class="odd">
<td><p>Exch-OWA-Mailbox-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchConfigurationXML</p></td>
</tr>
<tr class="even">
<td><p>Exch-OWA-Virtual-Directory</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchConfigurationXML</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 CU1 添加的类

此部分包含在 Exchange 2013 CU1 中修改的类。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>类</th>
<th>更改</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exch-Mapi-Virtual-Directory</p></td>
<td><p>ntdsSchemaAdd</p></td>
</tr>
<tr class="even">
<td><p>Exch-Push-Notifications-App</p></td>
<td><p>ntdsSchemaAdd</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 CU1 修改的属性

此部分包含在 Exchange 2013 CU1 中修改的属性。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>类</th>
<th>更改</th>
<th>属性/类</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exch-Mailflow-Policy-Transport-Rules-Template-Xml</p></td>
<td><p>rangeUpper</p></td>
<td><p>256000</p></td>
</tr>
<tr class="even">
<td><p>Exch-Configuration-Unit-Container</p></td>
<td><p>rangeUpper</p></td>
<td><p>15254</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 CU1 添加的对象 ID

以下属性对象 ID 在您安装 Exchange 2013 CU1 时添加：

  - 1.2.840.113556.1.4.7000.102.52109

  - 1.2.840.113556.1.4.7000.102.52110

  - 1.2.840.113556.1.4.7000.102.52127

  - 1.2.840.113556.1.4.7000.102.52126

  - 1.2.840.113556.1.4.7000.102.52128

  - 1.2.840.113556.1.4.7000.102.52129

当您安装 Exchange 2013 CU1 时，会添加下列类对象 ID：

  - 1.2.840.113556.1.5.7000.62.50202

  - 1.2.840.113556.1.5.7000.62.50203

## 由 Exchange 2013 CU1 添加的已编制索引的属性

下表列出了您在安装 Exchange 2013 CU1 时添加到索引属性列表中的属性。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>搜索标志值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Provisioning-Tags</p></td>
<td><p>1</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 CU1 修改的属性集

以下属性集在您安装 Exchange 2013 CU1 时修改：

  - Exchange-Information

## 由 Exchange 2013 CU1 添加的全局目录属性

以下全局编录属性由 Exchange 2013 CU1 添加：

  - ms-Exch-Offline-OrgId-Home-Realm-Record

  - ms-Exch-EvictedMembers-Link

  - ms-Exch-EvictedMemebers-BL

## Exchange 2013 RTM Active Directory 架构更改

本节总结了您在安装 Exchange 2013 RTM 时对 Active Directory 架构所作的更改。此部分包括下列子部分：

  - 由 Exchange 2013 RTM 修改的类

  - 由 Exchange 2013 RTM 修改的属性

  - 由 Exchange 2013 RTM 添加的类

  - 由 Exchange 2013 RTM 添加的属性

  - 由 Exchange 2013 RTM 添加的 MAPI ID

  - 由 Exchange 2013 RTM 添加的扩展权限

  - 由 Exchange 2013 RTM 添加的对象 ID

  - 由 Exchange 2013 RTM 添加的已编制索引的属性

  - 由 Exchange 2013 RTM 添加的全局目录属性

## 由 Exchange 2013 RTM 修改的类

此部分包含在 Exchange 2013 RTM 中修改的类。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>类</th>
<th>更改</th>
<th>属性/类</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchLocalizationFlags</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRoleGroupType</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDirsyncAuthorityMetadata</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDirsyncStatusAck</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchEdgeSyncConfigFlags</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHABRootDepartmentLink</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDefaultPublicFolderMailbox</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchForestModeFlag</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDirsyncStatus</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchIsDirsyncStatusPending</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPreviousArchiveDatabase</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDirSyncServiceInstance</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOrganizationUpgradePolicyLink</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-OWA-Mailbox-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOWASetPhotoURL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-OWA-Virtual-Directory</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOWASetPhotoURL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchWorkloadManagementPolicyLink</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>ms-DS-GeoCoordinates-Altitude</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>ms-DS-GeoCoordinates-Latitude</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>ms-DS-GeoCoordinates-Longitude</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Resource-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCustomerExpectationCritical</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Resource-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDiscretionaryCritical</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Resource-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchInternalMaintenanceCritical</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Resource-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchUrgentCritical</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Availability-Address-Space</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchFedTargetAutodiscoverEPR</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Private-MDB</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxDatabaseTransportFlags</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRecipientSoftDeletedStatus</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchWhenSoftDeletedTime</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Custom-Attributes</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchExtensionCustomAttribute1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Custom-Attributes</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchExtensionCustomAttribute2</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Custom-Attributes</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchExtensionCustomAttribute3</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Custom-Attributes</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchExtensionCustomAttribute4</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Custom-Attributes</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchExtensionCustomAttribute5</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Virtual-Directory</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMRSProxyFlags</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Virtual-Directory</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMRSProxyMaxConnections</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Active-Sync-Device</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDeviceClientType</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringDeferAttempts</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringDeferWaitTime</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringFlags</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringPrimaryUpdatePath</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringSecondaryUpdatePath</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringUpdateFrequency</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringUpdateTimeout</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTeamMailboxExpiration</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTeamMailboxOwners</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTeamMailboxSharePointLinkedBy</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTeamMailboxSharePointUrl</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTeamMailboxShowInClientList</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCalendarLoggingQuota</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMSOForwardSyncNonRecipientCookie</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMSOForwardSyncRecipientCookie</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMSOForwardSyncReplayList</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchAccountForestLink</p></td>
</tr>
<tr class="odd">
<td><p>Top</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchAccountForestBL</p></td>
</tr>
<tr class="even">
<td><p>Top</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTrustedDomainBL</p></td>
</tr>
<tr class="odd">
<td><p>Top</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchAcceptedDomainBL</p></td>
</tr>
<tr class="even">
<td><p>Top</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHygieneConfigurationMalwareBL</p></td>
</tr>
<tr class="odd">
<td><p>Top</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHygieneConfigurationSpamBL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchELCMailboxFlags</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHomeMTASL</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveSourceArchiveMDBLinkSL</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveSourceMDBLinkSL</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveTargetArchiveMDBLinkSL</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveTargetMDBLinkSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accepted-Domain</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHygieneConfigurationLink</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accepted-Domain</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTransportResellerSettingsLinkSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchManagementSiteLinkSL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOrganizationUpgradePolicyLinkSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Fed-OrgId</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchFedDelegationTrustSL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Gateway</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHomeMDBSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Gateway</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHomeMTASL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchArchiveDatabaseLinkSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchDisabledArchiveDatabaseLinkSL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHomeMDBSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveTargetMDBLinkSL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPreviousArchiveDatabaseSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mail-Storage</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPreviousHomeMDBSL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MRS-Request</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveSourceMDBLinkSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MRS-Request</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveStorageMDBLinkSL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MRS-Request</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMailboxMoveTargetMDBLinkSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-OAB</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOffLineABServerSL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Routing-Group-Connector</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHomeMTASL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Site-Connector</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchHomeMTASL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Tenant-Perimeter-Settings</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTransportResellerSettingsLinkSL</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Domain-Content-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchContentByteEncoderTypeFor7BitCharsets</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Domain-Content-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchContentPreferredInternetCodePageForShiftJis</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Domain-Content-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchContentRequiredCharSetCoverage</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Coexistence-Relationship</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCoexistenceOnPremisesSmartHost</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Coexistence-Relationship</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCoexistenceSecureMailCertificateThumbprint</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Coexistence-Relationship</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCoexistenceTransportServers</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>ms-exch-group-external-member-count</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>ms-exch-group-member-count</p></td>
</tr>
<tr class="even">
<td><p>Ms-Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>ms-exch-organization-flags-2</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchGroupExternalMemberCount</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchGroupMemberCount</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchShadowWhenSoftDeletedTime</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOrganizationFlags2</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchUMAvailableLanguages</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Control-Point-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRMSOnlineCertificationLocationUrl</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Control-Point-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRMSOnlineKeySharingLocationUrl</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Control-Point-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRMSOnlineLicensingLocationUrl</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchThrottlingPolicyFlags</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Exchange-Server</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilteringScanTimeout</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Hosted-Content-Filter-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSpamCountryBlockList</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Hosted-Content-Filter-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSpamLanguageBlockList</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Hosted-Content-Filter-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSpamNotifyOutboundRecipients</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Malware-Filter-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilterConfigExternalSenderAdminAddress</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Malware-Filter-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchMalwareFilterConfigInternalSenderAdminAddress</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchActiveInstanceSleepInterval</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPassiveInstanceSleepInterval</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSyncDaemonMaxVersion</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSyncDaemonMinVersion</p></td>
</tr>
<tr class="even">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPublicFolderMailbox</p></td>
</tr>
<tr class="odd">
<td><p>Mail-Recipient</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPublicFolderSmtpAddress</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Hosted-Content-Filter-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSpamDigestFrequency</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Hosted-Content-Filter-Config</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSpamQuarantineRetention</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchWACDiscoveryEndpoint</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchAdfsAuthenticationRawConfiguration</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Organization-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchServiceEndPointURL</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Public-Folder</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPublicFolderEntryId</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Transport-Rule</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTransportRuleImmutableId</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Transport-Settings</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTransportMaxRetriesForLocalSiteShadow</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Transport-Settings</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchTransportMaxRetriesForRemoteSiteShadow</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Transport-Settings</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchConfigurationXML</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Account-Forest</p></td>
<td><p>possSuperiors</p></td>
<td><p>msExchContainer</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCanaryData0</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCanaryData1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCanaryData2</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Base-Class</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCorrelationId</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantCompletionTargetVector</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantFlags</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantSafeLockdownSchedule</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantSourceForest</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantStartLockdown</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantStartRetired</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantStartSync</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantStatus</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantTargetForest</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRelocateTenantTransitionCounter</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Configuration-Unit-Container</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSyncCookie</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchAnonymousThrottlingPolicyStateEx</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchEASThrottlingPolicyStateEx</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchEWSThrottlingPolicyStateEx</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchGeneralThrottlingPolicyStateEx</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchIMAPThrottlingPolicyStateEx</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchOWAThrottlingPolicyStateEx</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPOPThrottlingPolicyStateEx</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchPowershellThrottlingPolicyStateEx</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Throttling-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchRCAThrottlingPolicyStateEx</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mailflow-Policy</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchImmutableId</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MDB</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchCalendarLoggingQuota</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Transport-Rule</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchImmutableId</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSyncServiceInstanceNewTenantMaxVersion</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MSO-Sync-Service-Instance</p></td>
<td><p>add:mayContain</p></td>
<td><p>msExchSyncServiceInstanceNewTenantMinVersion</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 RTM 修改的属性

此部分包含在 Exchange 2013 RTM 中修改的属性。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>类</th>
<th>更改</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Schema-Version-Pt</p></td>
<td><p>rangeUpper</p></td>
<td><p>15137</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-HAB-Root-Department-Link</p></td>
<td><p>替换:isMemberOfPartialAttributeSet</p></td>
<td><p>TRUE</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Archive-GUID</p></td>
<td><p>替换:searchFlags</p></td>
<td><p>9</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accepted-Domain-Name</p></td>
<td><p>替换:searchFlags</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Bypass-Audit</p></td>
<td><p>替换:searchFlags</p></td>
<td><p>19</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mailbox-Audit-Enable</p></td>
<td><p>替换:searchFlags</p></td>
<td><p>19</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Extension-Custom-Attribute-1</p></td>
<td><p>isMemberOfPartialAttributeSet:</p></td>
<td><p>TRUE</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Extension-Custom-Attribute-2</p></td>
<td><p>isMemberOfPartialAttributeSet:</p></td>
<td><p>TRUE</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Extension-Custom-Attribute-3</p></td>
<td><p>isMemberOfPartialAttributeSet:</p></td>
<td><p>TRUE</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Extension-Custom-Attribute-4</p></td>
<td><p>isMemberOfPartialAttributeSet:</p></td>
<td><p>TRUE</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Extension-Custom-Attribute-5</p></td>
<td><p>isMemberOfPartialAttributeSet</p></td>
<td><p>TRUE</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Coexistence-On-Premises-Smart-Host</p></td>
<td><p>ntdsSchemaAdd</p></td>
<td><p>attributeID：1.2.840.113556.1.4.7000.102.51992 isMemberOfPartialAttributeSet：FALSE（不在全局目录中）searchFlags：0（无索引）</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Coexistence-Secure-Mail-Certificate-Thumbprint</p></td>
<td><p>ntdsSchemaAdd</p></td>
<td><p>attributeID：1.2.840.113556.1.4.7000.102.51991 isMemberOfPartialAttributeSet：FALSE（不在全局目录中）searchFlags：0（无索引）</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Coexistence-Transport-Servers</p></td>
<td><p>ntdsSchemaAdd</p></td>
<td><p>attributeID：1.2.840.113556.1.4.7000.102.51990 isMemberOfPartialAttributeSet：FALSE（不在全局目录中）searchFlags：0（无索引）</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-ELC-Mailbox-Flags</p></td>
<td><p>替换:attributeSecurityGuid</p></td>
<td><p>F6SzsVXskUGzJ7cuM+OK8g==</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Malware-Filtering-Update-Frequency</p></td>
<td><p>rangeUpper</p></td>
<td><p>38880</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-MSO-Forward-Sync-Non-Recipient-Cookie</p></td>
<td><p>rangeUpper</p></td>
<td><p>20480</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-MSO-Forward-Sync-Recipient-Cookie</p></td>
<td><p>rangeUpper</p></td>
<td><p>20480</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Role-Entries</p></td>
<td><p>rangeUpper</p></td>
<td><p>8192</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Group-External-Member-Count</p></td>
<td><p>ntdsSchemaModify</p></td>
<td><p>isMemberOfPartialAttributeSet：TRUE MAPIID:36066</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Group-Member-Count</p></td>
<td><p>ntdsSchemaModify</p></td>
<td><p>替换:isMemberOfPartialAttributeSetisMemberOfPartialAttributeSet：TRUE MAPIID：36067</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 RTM 添加的类

当您安装 Exchange 2013 RTM 时，会添加下列类：

  - ms-Exch-ActiveSync-Device-Autoblock-Threshold

  - ms-Exch-MSO-Forward-Sync-Divergence

  - ms-Exch-MSO-Sync-Service-Instance

  - ms-Exch-Organization-Upgrade-Policy

  - ms-Exch-Workload-Policy

  - ms-Exch-Resource-Policy

  - ms-Exch-Team-Mailbox-Provisioning-Policy

  - ms-Exch-Account-Forest

  - ms-Exch-Hosted-Content-Filter-Config

  - ms-Exch-Hygiene-Configuration

  - ms-Exch-Malware-Filter-Config

  - ms-Exch-Protocol-Cfg-SIP-Container

  - ms-Exch-Protocol-Cfg-SIP-FE-Server

  - ms-Exch-Exchange-Transport-Server

  - ms-Exch-Auth-Auth-Config

  - ms-Exch-Auth-Auth-Server

  - ms-Exch-Auth-Partner-Application

  - ms-Exch-Mailflow-Policy-Collection

  - ms-Exch-Mailflow-Policy

## 由 Exchange 2013 RTM 添加的属性

下列属性包含一组新功能所需的更改，在您安装 Exchange 2013 RTM 时进行添加：

  - ms-Exch-ActiveSync-Device-AutoBlock-Duration

  - ms-Exch-ActiveSync-Device-Autoblock-Threshold-Incidence-Duration

  - ms-Exch-ActiveSync-Device-Autoblock-Threshold-Incidence-Limit

  - ms-Exch-ActiveSync-Device-Autoblock-Threshold-Type

  - ms-Exch-Dirsync-Authority-Metadata

  - ms-Exch-Dirsync-Status

  - ms-Exch-Dirsync-Status-Ack

  - ms-Exch-Edge-Sync-Config-Flags

  - ms-Exch-Is-Dirsync-Status-Pending,

  - ms-Exch-Localization-Flags

  - ms-Exch-Previous-Archive-Database

  - ms-Exch-RoleGroup-Type

  - ms-Exch-External-Directory-Object-Class

  - ms-Exch-MSO-Forward-Sync-Divergence-Count

  - ms-Exch-MSO-Forward-Sync-Divergence-Timestamp

  - ms-Exch-MSO-Forward-Sync-Divergence-Related-Object-Link

  - ms-Exch-Default-Public-Folder-Mailbox

  - ms-Exch-Forest-Mode-Flag

  - ms-Exch-Dir-Sync-Service-Instance

  - ms-Exch-Organization-Upgrade-Policy-Date

  - ms-Exch-Organization-Upgrade-Policy-Enabled

  - ms-Exch-Organization-Upgrade-Policy-MaxMailboxes

  - ms-Exch-Organization-Upgrade-Policy-Priority

  - ms-Exch-Organization-Upgrade-Policy-Source-Version

  - ms-Exch-Organization-Upgrade-Policy-Status

  - ms-Exch-Organization-Upgrade-Policy-Target-Version

  - ms-Exch-OWA-Set-Photo-URL

  - ms-Exch-Organization-Upgrade-Policy-Link

  - ms-Exch-Organization-Upgrade-Policy-BL

  - ms-Exch-Workload-Classification

  - ms-Exch-Workload-Management-Is-Enabled

  - ms-Exch-Workload-Type

  - ms-Exch-Workload-Management-Policy-Link

  - ms-Exch-Workload-Management-Policy-BL

  - ms-Exch-Workload-Management-Policy

  - ms-Exch-Customer-Expectation-Overloaded

  - ms-Exch-Customer-Expectation-Underloaded

  - ms-Exch-Discretionary-Overloaded

  - ms-Exch-Discretionary-Underloaded

  - ms-Exch-Internal-Maintenance-Overloaded

  - ms-Exch-Internal-Maintenance-Underloaded

  - ms-Exch-Resource-Type

  - ms-Exch-Urgent-Overloaded

  - ms-Exch-Urgent-Underloaded

  - ms-DS-GeoCoordinates-Altitude

  - ms-DS-GeoCoordinates-Latitude

  - ms-DS-GeoCoordinates-Longitude

  - ms-Exch-Customer-Expectation-Critical

  - ms-Exch-Discretionary-Critical

  - ms-Exch-Internal-Maintenance-Critical

  - ms-Exch-Urgent-Critical

  - ms-Exch-Mailbox-Database-Transport-Flags

  - ms-Exch-Extension-Custom-Attribute-1

  - ms-Exch-Extension-Custom-Attribute-2

  - ms-Exch-Extension-Custom-Attribute-3

  - ms-Exch-Extension-Custom-Attribute-4

  - ms-Exch-Extension-Custom-Attribute-5

  - ms-Exch-MRS-Proxy-Flags

  - ms-Exch-MRS-Proxy-Max-Connections

  - ms-Exch-Recipient-SoftDeleted-Status

  - ms-Exch-When-Soft-Deleted-Time

  - ms-Exch-Device-Client-Type

  - ms-Exch-Malware-Filtering-Defer-Attempts

  - ms-Exch-Malware-Filtering-Defer-Wait-Time

  - ms-Exch-Malware-Filtering-Flags

  - ms-Exch-Malware-Filtering-Primary-Update-Path

  - ms-Exch-Malware-Filtering-Secondary-Update-Path

  - ms-Exch-Malware-Filtering-Update-Frequency

  - ms-Exch-Malware-Filtering-Update-Timeout

  - ms-Exch-Team-Mailbox-Expiration

  - ms-Exch-Team-Mailbox-Expiry-Days

  - ms-Exch-Team-Mailbox-Owners

  - ms-Exch-Team-Mailbox-SharePoint-Linked-By

  - ms-Exch-Team-Mailbox-SharePoint-Url

  - ms-Exch-Team-Mailbox-Show-In-Client-List

  - ms-Exch-Account-Forest-Link

  - ms-Exch-Account-Forest-BL

  - ms-Exch-Trusted-Domain-Link

  - ms-Exch-Trusted-Domain-BL

  - ms-Exch-Archive-Database-Link-SL

  - ms-Exch-Disabled-Archive-Database-Link-SL

  - ms-Exch-Fed-Delegation-Trust-SL

  - ms-Exch-Home-MDB-SL

  - ms-Exch-Home-MTA-SL

  - ms-Exch-Mailbox-Move-Source-Archive-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Source-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Storage-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Target-Archive-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Target-MDB-Link-SL

  - ms-Exch-Malware-Filter-Config-Alert-Text

  - ms-Exch-Malware-Filter-Config-External-Body

  - ms-Exch-Malware-Filter-Config-External-Subject

  - ms-Exch-Malware-Filter-Config-Flags

  - ms-Exch-Malware-Filter-Config-From-Address

  - ms-Exch-Malware-Filter-Config-From-Name

  - ms-Exch-Malware-Filter-Config-Internal-Body

  - ms-Exch-Malware-Filter-Config-Internal-Subject

  - ms-Exch-Management-Site-Link-SL

  - ms-Exch-Off-Line-AB-Server-SL

  - ms-Exch-Organization-Upgrade-Policy-Link-SL

  - ms-Exch-Previous-Archive-Database-SL

  - ms-Exch-Previous-Home-MDB-SL

  - ms-Exch-RMS-Computer-Accounts-Link-SL

  - ms-Exch-Spam-Add-Header

  - ms-Exch-Spam-Asf-Settings

  - ms-Exch-Spam-Asf-Test-Bcc-Address

  - ms-Exch-Spam-False-Positive-Cc

  - ms-Exch-Spam-Flags

  - ms-Exch-Spam-Modify-Subject

  - ms-Exch-Spam-Outbound-Spam-Cc

  - ms-Exch-Spam-Redirect-Address

  - ms-Exch-Transport-Reseller-Settings-Link-SL

  - ms-Exch-Hygiene-Configuration-Link

  - ms-Exch-Accepted-Domain-BL

  - ms-Exch-Malware-Filter-Config-Link

  - ms-Exch-Hygiene-Configuration-Malware-BL

  - ms-Exch-Hosted-Content-Filter-Config-Link

  - ms-Exch-Hygiene-Configuration-Spam-BL

  - ms-Exch-Content-Byte-Encoder-Type-For-7-Bit-Charsets

  - ms-Exch-Content-Preferred-Internet-Code-Page-For-Shift-Jis

  - ms-Exch-Content-Required-Char-Set-Coverage

  - ms-Exch-Group-External-Member-Count

  - ms-Exch-Group-Member-Count

  - ms-Exch-Organization-Flags-2

  - ms-Exch-RMSOnline-Certification-Location-Url

  - ms-Exch-RMSOnline-Key-Sharing-Location-Url

  - ms-Exch-RMSOnline-Licensing-Location-Url

  - ms-Exch-Shadow-When-Soft-Deleted-Time

  - ms-Exch-Throttling-Policy-Flags

  - ms-Exch-Malware-Filter-Config-External-Sender-Admin-Address

  - ms-Exch-Malware-Filter-Config-Internal-Sender-Admin-Address

  - ms-Exch-Malware-Filtering-Scan-Timeout

  - ms-Exch-Spam-Country-Block-List

  - ms-Exch-Spam-Language-Block-List

  - ms-Exch-Spam-Notify-Outbound-Recipients

  - ms-Exch-Auth-App-Secret

  - ms-Exch-Auth-Application-Identifier

  - ms-Exch-Auth-Auth-Server-Type

  - ms-Exch-Auth-Authorization-Url

  - ms-Exch-Auth-Certificate-Data

  - ms-Exch-Auth-Certificate-Thumbprint

  - ms-Exch-Auth-Flags

  - ms-Exch-Auth-Issuer-Name

  - ms-Exch-Auth-Issuing-Url

  - ms-Exch-Auth-Linked-Account

  - ms-Exch-Auth-Metadata-Url

  - ms-Exch-Auth-Realm

  - ms-Exch-Mailflow-Policy-Countries

  - ms-Exch-Mailflow-Policy-Keywords

  - ms-Exch-Mailflow-Policy-Publisher-Name

  - ms-Exch-Mailflow-Policy-Transport-Rules-Template-Xml

  - ms-Exch-Mailflow-Policy-Version

  - ms-Exch-Public-Folder-EntryId

  - ms-Exch-Public-Folder-Mailbox

  - ms-Exch-Public-Folder-Smtp-Address

  - ms-Exch-Spam-Digest-Frequency

  - ms-Exch-Spam-Quarantine-Retention

  - ms-Exch-Transport-MaxRetriesForLocalSiteShadow

  - ms-Exch-Transport-MaxRetriesForRemoteSiteShadow

  - ms-Exch-Transport-Rule-Immutable-Id

  - ms-Exch-WAC-Discovery-Endpoint

  - ms-Exch-Anonymous-Throttling-Policy-State-Ex

  - ms-Exch-Canary-Data-0

  - ms-Exch-Canary-Data-1

  - ms-Exch-Canary-Data-2

  - ms-Exch-Correlation-Id

  - ms-Exch-EAS-Throttling-Policy-State-Ex

  - ms-Exch-EWS-Throttling-Policy-State-Ex

  - ms-Exch-General-Throttling-Policy-State-Ex

  - ms-Exch-IMAP-Throttling-Policy-State-Ex

  - ms-Exch-OWA-Throttling-Policy-State-Ex

  - ms-Exch-POP-Throttling-Policy-State-Ex

  - ms-Exch-Powershell-Throttling-Policy-State-Ex

  - ms-Exch-RCA-Throttling-Policy-State-Ex

  - ms-Exch-Relocate-Tenant-Completion-Target-Vector

  - ms-Exch-Relocate-Tenant-Flags

  - ms-Exch-Relocate-Tenant-Safe-Lockdown-Schedule

  - ms-Exch-Relocate-Tenant-Source-Forest

  - ms-Exch-Relocate-Tenant-Start-Lockdown

  - ms-Exch-Relocate-Tenant-Start-Retired

  - ms-Exch-Relocate-Tenant-Start-Sync

  - ms-Exch-Relocate-Tenant-Status

  - ms-Exch-Relocate-Tenant-Target-Forest

  - ms-Exch-Relocate-Tenant-Transition-Counter

  - ms-Exch-Sync-Cookie

  - ms-Exch-Adfs-Authentication-Raw-Configuration

  - ms-Exch-Service-End-Point-URL

  - ms-Exch-Sync-Service-Instance-New-Tenant-Max-Version

  - ms-Exch-Sync-Service-Instance-New-Tenant-Min-Version

## 由 Exchange 2013 RTM 添加的 MAPI ID

当您安装 Exchange 2013 RTM 时，会添加下列 MAPI ID：

  - 36066

  - 36067

## 由 Exchange 2013 RTM 添加的扩展权限

下表列出在安装 Exchange 2013 RTM 时添加的扩展权限。安装 Exchange 2013 RTM 并不会修改任何现有的扩展权限。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>标识符</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CN=ms-Exch-SMTP-Accept-XProxyFrom,CN=Extended-Rights,&lt;ConfigurationContainerDN&gt;</p></td>
<td><p>changetype:ntdsSchemaAdd</p>
<p>displayName：Accept XProxyFrom</p>
<p>objectClass: controlAccessRight</p>
<p>rightsGuid：5bee2b72-50d7-49c7-ba66-39a25daa1e92</p>
<p>validAccesses: 256</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 RTM 添加的对象 ID

当您安装 Exchange 2013 RTM 时，会添加下列属性对象 ID：

  - 1.2.840.113556.1.4.7000.102.51794

  - 1.2.840.113556.1.4.7000.102.51795

  - 1.2.840.113556.1.4.7000.102.51792

  - 1.2.840.113556.1.4.7000.102.51791

  - 1.2.840.113556.1.4.7000.102.51789

  - 1.2.840.113556.1.4.7000.102.51787

  - 1.2.840.113556.1.4.7000.102.51788

  - 1.2.840.113556.1.4.7000.102.51786

  - 1.2.840.113556.1.4.7000.102.51790

  - 1.2.840.113556.1.4.7000.102.51774

  - 1.2.840.113556.1.4.7000.102.51773

  - 1.2.840.113556.1.4.7000.102.51775

  - 1.2.840.113556.1.4.7000.102.51798

  - 1.2.840.113556.1.4.7000.102.51801

  - 1.2.840.113556.1.4.7000.102.51800

  - 1.2.840.113556.1.4.7000.102.51799

  - 1.2.840.113556.1.4.7000.102.51805

  - 1.2.840.113556.1.4.7000.102.51796

  - 1.2.840.113556.1.4.7000.102.51797

  - 1.2.840.113556.1.4.7000.102.51814

  - 1.2.840.113556.1.4.7000.102.51813

  - 1.2.840.113556.1.4.7000.102.51815

  - 1.2.840.113556.1.4.7000.102.51816

  - 1.2.840.113556.1.4.7000.102.51818

  - 1.2.840.113556.1.4.7000.102.51812

  - 1.2.840.113556.1.4.7000.102.51819

  - 1.2.840.113556.1.4.7000.102.51806

  - 1.2.840.113556.1.4.7000.102.51820

  - 1.2.840.113556.1.4.7000.102.51821

  - 1.2.840.113556.1.4.7000.102.51811

  - 1.2.840.113556.1.4.7000.102.51807

  - 1.2.840.113556.1.4.7000.102.51810

  - 1.2.840.113556.1.4.7000.102.51808

  - 1.2.840.113556.1.4.7000.102.51809

  - 1.2.840.113556.1.4.7000.102.51830

  - 1.2.840.113556.1.4.7000.102.51829

  - 1.2.840.113556.1.4.7000.102.51824

  - 1.2.840.113556.1.4.7000.102.51823

  - 1.2.840.113556.1.4.7000.102.51827

  - 1.2.840.113556.1.4.7000.102.51826

  - 1.2.840.113556.1.4.7000.102.51822

  - 1.2.840.113556.1.4.7000.102.51833

  - 1.2.840.113556.1.4.7000.102.51832

  - 1.2.840.113556.1.4.2183

  - 1.2.840.113556.1.4.2184

  - 1.2.840.113556.1.4.2185

  - 1.2.840.113556.1.4.7000.102.51838

  - 1.2.840.113556.1.4.7000.102.51836

  - 1.2.840.113556.1.4.7000.102.51837

  - 1.2.840.113556.1.4.7000.102.51839

  - 1.2.840.113556.1.4.7000.102.51840

  - 1.2.840.113556.1.4.7000.102.51876

  - 1.2.840.113556.1.4.7000.102.51877

  - 1.2.840.113556.1.4.7000.102.51878

  - 1.2.840.113556.1.4.7000.102.51879

  - 1.2.840.113556.1.4.7000.102.51880

  - 1.2.840.113556.1.4.7000.102.51851

  - 1.2.840.113556.1.4.7000.102.51852

  - 1.2.840.113556.1.4.7000.102.51859

  - 1.2.840.113556.1.4.7000.102.51860

  - 1.2.840.113556.1.4.7000.102.51861

  - 1.2.840.113556.1.4.7000.102.51864

  - 1.2.840.113556.1.4.7000.102.51863

  - 1.2.840.113556.1.4.7000.102.51862

  - 1.2.840.113556.1.4.7000.102.51865

  - 1.2.840.113556.1.4.7000.102.51866

  - 1.2.840.113556.1.4.7000.102.51867

  - 1.2.840.113556.1.4.7000.102.51868

  - 1.2.840.113556.1.4.7000.102.51871

  - 1.2.840.113556.1.4.7000.102.51870

  - 1.2.840.113556.1.4.7000.102.51872

  - 1.2.840.113556.1.4.7000.102.51875

  - 1.2.840.113556.1.4.7000.102.51874

  - 1.2.840.113556.1.4.7000.102.51873

  - 1.2.840.113556.1.4.7000.102.51869

  - 1.2.840.113556.1.4.7000.102.51915

  - 1.2.840.113556.1.4.7000.102.51883

  - 1.2.840.113556.1.4.7000.102.51914

  - 1.2.840.113556.1.4.7000.102.51931

  - 1.2.840.113556.1.4.7000.102.51932

  - 1.2.840.113556.1.4.7000.102.51939

  - 1.2.840.113556.1.4.7000.102.51930

  - 1.2.840.113556.1.4.7000.102.51940

  - 1.2.840.113556.1.4.7000.102.51933

  - 1.2.840.113556.1.4.7000.102.51934

  - 1.2.840.113556.1.4.7000.102.51935

  - 1.2.840.113556.1.4.7000.102.51936

  - 1.2.840.113556.1.4.7000.102.51952

  - 1.2.840.113556.1.4.7000.102.51923

  - 1.2.840.113556.1.4.7000.102.51927

  - 1.2.840.113556.1.4.7000.102.51926

  - 1.2.840.113556.1.4.7000.102.51922

  - 1.2.840.113556.1.4.7000.102.51929

  - 1.2.840.113556.1.4.7000.102.51928

  - 1.2.840.113556.1.4.7000.102.51925

  - 1.2.840.113556.1.4.7000.102.51924

  - 1.2.840.113556.1.4.7000.102.51941

  - 1.2.840.113556.1.4.7000.102.51942

  - 1.2.840.113556.1.4.7000.102.51937

  - 1.2.840.113556.1.4.7000.102.51943

  - 1.2.840.113556.1.4.7000.102.51944

  - 1.2.840.113556.1.4.7000.102.51938

  - 1.2.840.113556.1.4.7000.102.51882

  - 1.2.840.113556.1.4.7000.102.51881

  - 1.2.840.113556.1.4.7000.102.51921

  - 1.2.840.113556.1.4.7000.102.51918

  - 1.2.840.113556.1.4.7000.102.51920

  - 1.2.840.113556.1.4.7000.102.51916

  - 1.2.840.113556.1.4.7000.102.51919

  - 1.2.840.113556.1.4.7000.102.51917

  - 1.2.840.113556.1.4.7000.102.51945

  - 1.2.840.113556.1.4.7000.102.51946

  - 1.2.840.113556.1.4.7000.102.51948

  - 1.2.840.113556.1.4.7000.102.51949

  - 1.2.840.113556.1.4.7000.102.51947

  - 1.2.840.113556.1.4.7000.102.51950

  - 1.2.840.113556.1.4.7000.102.51951

  - 1.2.840.113556.1.4.7000.102.51954

  - 1.2.840.113556.1.4.7000.102.51955

  - 1.2.840.113556.1.4.7000.102.51953

  - 1.2.840.113556.1.4.7000.102.51993

  - 1.2.840.113556.1.4.7000.102.51995

  - 1.2.840.113556.1.4.7000.102.51994

  - 1.2.840.113556.1.4.7000.102.51998

  - 1.2.840.113556.1.4.7000.102.51997

  - 1.2.840.113556.1.4.7000.102.52004

  - 1.2.840.113556.1.4.7000.102.52003

  - 1.2.840.113556.1.4.7000.102.52002

  - 1.2.840.113556.1.4.7000.102.52001

  - 1.2.840.113556.1.4.7000.102.52005

  - 1.2.840.113556.1.4.7000.102.52007

  - 1.2.840.113556.1.4.7000.102.52006

  - 1.2.840.113556.1.4.7000.102.51996

  - 1.2.840.113556.1.4.7000.102.52008

  - 1.2.840.113556.1.4.7000.102.52017

  - 1.2.840.113556.1.4.7000.102.52014

  - 1.2.840.113556.1.4.7000.102.52021

  - 1.2.840.113556.1.4.7000.102.52020

  - 1.2.840.113556.1.4.7000.102.52012

  - 1.2.840.113556.1.4.7000.102.52011

  - 1.2.840.113556.1.4.7000.102.52013

  - 1.2.840.113556.1.4.7000.102.52018

  - 1.2.840.113556.1.4.7000.102.52019

  - 1.2.840.113556.1.4.7000.102.52022

  - 1.2.840.113556.1.4.7000.102.52015

  - 1.2.840.113556.1.4.7000.102.52016

  - 1.2.840.113556.1.4.7000.102.52029

  - 1.2.840.113556.1.4.7000.102.52030

  - 1.2.840.113556.1.4.7000.102.52039

  - 1.2.840.113556.1.4.7000.102.52041

  - 1.2.840.113556.1.4.7000.102.52037

  - 1.2.840.113556.1.4.7000.102.52035

  - 1.2.840.113556.1.4.7000.102.52034

  - 1.2.840.113556.1.4.7000.102.52036

  - 1.2.840.113556.1.4.7000.102.52032

  - 1.2.840.113556.1.4.7000.102.52033

  - 1.2.840.113556.1.4.7000.102.52031

  - 1.2.840.113556.1.4.7000.102.52024

  - 1.2.840.113556.1.4.7000.102.52040

  - 1.2.840.113556.1.4.7000.102.52023

  - 1.2.840.113556.1.4.7000.102.52042

  - 1.2.840.113556.1.4.7000.102.52051

  - 1.2.840.113556.1.4.7000.102.52052

  - 1.2.840.113556.1.4.7000.102.52053

  - 1.2.840.113556.1.4.7000.102.52065

  - 1.2.840.113556.1.4.7000.102.52043

  - 1.2.840.113556.1.4.7000.102.52044

  - 1.2.840.113556.1.4.7000.102.52045

  - 1.2.840.113556.1.4.7000.102.52046

  - 1.2.840.113556.1.4.7000.102.52047

  - 1.2.840.113556.1.4.7000.102.52048

  - 1.2.840.113556.1.4.7000.102.52049

  - 1.2.840.113556.1.4.7000.102.52050

  - 1.2.840.113556.1.4.7000.102.52063

  - 1.2.840.113556.1.4.7000.102.52061

  - 1.2.840.113556.1.4.7000.102.52059

  - 1.2.840.113556.1.4.7000.102.52058

  - 1.2.840.113556.1.4.7000.102.52055

  - 1.2.840.113556.1.4.7000.102.52056

  - 1.2.840.113556.1.4.7000.102.52054

  - 1.2.840.113556.1.4.7000.102.52060

  - 1.2.840.113556.1.4.7000.102.52057

  - 1.2.840.113556.1.4.7000.102.52062

  - 1.2.840.113556.1.4.7000.102.52064

当您安装 Exchange 2013 RTM 时，会添加下列类对象 ID：

  - 1.2.840.113556.1.5.7000.62.50161

  - 1.2.840.113556.1.5.7000.62.50162

  - 1.2.840.113556.1.5.7000.62.50163

  - 1.2.840.113556.1.5.7000.62.50166

  - 1.2.840.113556.1.5.7000.62.50164

  - 1.2.840.113556.1.5.7000.62.50165

  - 1.2.840.113556.1.5.7000.62.50167

  - 1.2.840.113556.1.5.7000.62.50170

  - 1.2.840.113556.1.5.7000.62.50172

  - 1.2.840.113556.1.5.7000.62.50171

  - 1.2.840.113556.1.5.7000.62.50173

  - 1.2.840.113556.1.5.7000.62.50178

  - 1.2.840.113556.1.5.7000.62.50174

  - 1.2.840.113556.1.5.7000.62.50176

  - 1.2.840.113556.1.5.7000.62.50177

  - 1.2.840.113556.1.5.7000.62.50187

  - 1.2.840.113556.1.5.7000.62.50188

  - 1.2.840.113556.1.5.7000.62.50190

  - 1.2.840.113556.1.5.7000.62.50189

  - 1.2.840.113556.1.5.7000.62.50191

  - 1.2.840.113556.1.5.7000.62.50192

## 由 Exchange 2013 RTM 添加的已编制索引的属性

下表列出安装 Exchange 2013 RTM 时添加到已编制索引的属性列表中的属性。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>搜索标志值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-Is-Dirsync-Status-Pending</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Archive-GUID</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accepted-Domain-Name</p></td>
<td><p>9</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Bypass-Audit</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mailbox-Audit-Enable</p></td>
<td><p>19</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Default-Public-Folder-Mailbox</p></td>
<td><p>19</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-OWA-Set-Photo-URL</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Organization-Upgrade-Policy-Link</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-DS-GeoCoordinates-Altitude</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-DS-GeoCoordinates-Latitude</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-DS-GeoCoordinates-Longitude</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mailbox-Database-Transport-Flags</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Extension-Custom-Attribute-1</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Extension-Custom-Attribute-2</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Extension-Custom-Attribute-3</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Extension-Custom-Attribute-4</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Extension-Custom-Attribute-5</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Recipient-SoftDeleted-Status</p></td>
<td><p>27</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-When-Soft-Deleted-Time</p></td>
<td><p>17</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Device-Client-Type</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Team-Mailbox-Expiration</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Team-Mailbox-Expiry-Days</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Team-Mailbox-Owners</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Team-Mailbox-SharePoint-Linked-By</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Team-Mailbox-SharePoint-Url</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Team-Mailbox-Show-In-Client-List</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Home-MDB-SL</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Home-MTA-SL</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mailbox-Move-Source-Archive-MDB-Link-SL</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Mailbox-Move-Source-MDB-Link-SL</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Mailbox-Move-Target-Archive-MDB-Link-SL</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Organization-Upgrade-Policy-Link-SL</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Previous-Archive-Database-SL</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Previous-Home-MDB-SL</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Auth-Issuer-Name</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Auth-Application-Identifier</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Transport-Rule-Immutable-Id</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Public-Folder-EntryId</p></td>
<td><p>24</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Public-Folder-Mailbox</p></td>
<td><p>24</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Public-Folder-Smtp-Address</p></td>
<td><p>24</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Relocate-Tenant-Completion-Target-Vector</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Relocate-Tenant-Flags</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Relocate-Tenant-Safe-Lockdown-Schedule</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Relocate-Tenant-Start-Lockdown</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Relocate-Tenant-Start-Retired</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Relocate-Tenant-Start-Sync</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Relocate-Tenant-Transition-Counter</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Sync-Cookie</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Relocate-Tenant-Source-Forest</p></td>
<td><p>9</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Relocate-Tenant-Status,</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Relocate-Tenant-Target-Forest</p></td>
<td><p>9</p></td>
</tr>
</tbody>
</table>


## 由 Exchange 2013 RTM 添加的全局目录属性

以下全局目录属性由 Exchange 2013 RTM 添加：

  - ms-Exch-Dirsync-Authority-Metadata

  - ms-Exch-Dirsync-Status

  - ms-Exch-Dirsync-Status-Ack

  - ms-Exch-Edge-Sync-Config-Flags

  - ms-Exch-Is-Dirsync-Status-Pending

  - ms-Exch-Localization-Flags

  - ms-Exch-Previous-Archive-Database

  - ms-Exch-RoleGroup-Type

  - ms-Exch-HAB-Root-Department-Link

  - ms-Exch-Default-Public-Folder-Mailbox

  - ms-Exch-Team-Mailbox-Expiration

  - ms-Exch-Team-Mailbox-Expiry-Days

  - ms-Exch-Team-Mailbox-Owners

  - ms-Exch-Team-Mailbox-SharePoint-Linked-By

  - ms-Exch-Team-Mailbox-SharePoint-Url

  - ms-Exch-Team-Mailbox-Show-In-Client-List

  - ms-Exch-Recipient-SoftDeleted-Status

  - ms-Exch-When-Soft-Deleted-Time

  - ms-Exch-Device-Client-Type

  - ms-Exch-Extension-Custom-Attribute-1

  - ms-Exch-Extension-Custom-Attribute-2

  - ms-Exch-Extension-Custom-Attribute-3

  - ms-Exch-Extension-Custom-Attribute-4

  - ms-Exch-Extension-Custom-Attribute-5

  - ms-Exch-Archive-Database-Link-SL

  - ms-Exch-Disabled-Archive-Database-Link-SL

  - ms-Exch-Home-MDB-SL

  - ms-Exch-Home-MTA-SL

  - ms-Exch-Mailbox-Move-Source-Archive-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Source-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Storage-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Target-Archive-MDB-Link-SL

  - ms-Exch-Mailbox-Move-Target-MDB-Link-SL

  - ms-Exch-Previous-Archive-Database-SL

  - ms-Exch-Previous-Home-MDB-SL

  - ms-Exch-RMS-Computer-Accounts-Link-SL

  - ms-Exch-Group-Member-Count

  - ms-Exch-Group-External-Member-Count

  - ms-Exch-Correlation-Id

  - ms-Exch-Relocate-Tenant-Completion-Target-Vector,

  - ms-Exch-Relocate-Tenant-Flags

  - ms-Exch-Relocate-Tenant-Safe-Lockdown-Schedule

  - ms-Exch-Relocate-Tenant-Source-Forest

  - ms-Exch-Relocate-Tenant-Start-Lockdown

  - ms-Exch-Relocate-Tenant-Start-Retired

  - ms-Exch-Relocate-Tenant-Start-Sync

  - ms-Exch-Relocate-Tenant-Status

  - ms-Exch-Relocate-Tenant-Target-Forest

  - ms-Exch-Relocate-Tenant-Transition-Counter

  - ms-Exch-Sync-Cookie

