---
title: '安全列表聚合: Exchange 2013 Help'
TOCTitle: 安全列表聚合
ms:assetid: f05430a0-0405-4b65-a18d-18c9e86a13c4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125168(v=EXCHG.150)
ms:contentKeyID: 50491948
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 安全列表聚合

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2013-09-30_

在 Microsoft Exchange Server 2013 中，*安全列表聚合*表示在 Microsoft Outlook 和 Exchange 之间共享的反垃圾邮件功能。此功能从 Outlook 用户配置的反垃圾邮件安全收件人列表、安全发件人列表、阻止发件人列表和联系人数据中收集数据，并使 Exchange 反垃圾邮件代理可以使用这些数据。

在启用并正确地配置安全列表聚合之后，内容筛选器代理会将安全电子邮件传递到企业邮箱，不进行任何额外的处理。内容筛选器代理将 Outlook 用户从其添加到 Outlook 安全收件人列表或安全发件人列表的联系人或受信任的联系人接收的电子邮件标识为安全邮件。Outlook *联系人*是指用户组织内部或外部的某个人员，用户可以保存有关该人员的某些类型的信息，例如电子邮件和街道地址、电话和传真号码，以及网页 URL。

在 Exchange 2013 中，安全列表聚合程序也允许发件人筛选器代理阻止来自基于收件人阻止发件人列表中的邮件。

安全列表聚合可以帮助减少 Exchange 执行的反垃圾邮件筛选的误判情况。在垃圾邮件筛选环境中，如果垃圾邮件筛选器错误地将合法邮件标识为垃圾邮件，则存在*误报*。

对于每天筛选来自 Internet 的几十万封邮件的组织，如果垃圾邮件被隔离或删除，即使是小百分比的误判也意味着用户可能无法收到许多错误地标识为垃圾邮件。

安全列表聚合可能是减少邮件误报的最有效方法。在 Outlook 2010 或更高版本中，用户可以创建*安全发件人列表*。安全发件人列表指定 Outlook 用户希望从其接收邮件的域名和电子邮件地址的列表。默认情况下，Outlook 联系人和 Exchange 全局地址列表中的电子邮件地址包含在此列表中。默认情况下，Outlook 将用户向其发送邮件的所有外部联系人添加到安全发件人列表。

**目录**

Information stored in the Outlook user's safelist collection

How Exchange uses the safelist collection

Hashing of safelist collection entries

Enabling safelist aggregation

## 存储在 Outlook 用户的安全列表集合中的信息

\&quot;安全列表集合\&quot;是来自用户的安全发件人列表、安全收件人列表、阻止发件人列表和外部联系人的组合数据。此数据存储在 Outlook 中和 Exchange 邮箱中。

下列类型的信息存储在 Outlook 用户的安全列表集合中：

  - **安全发件人和安全收件人**   \&quot;发件人\&quot;邮件头表示发件人。电子邮件的\&quot;收件人\&quot;字段表示收件人。安全发件人和安全收件人通过完整的 SMTP 地址表示，例如 masato@contoso.com。Outlook 用户可以向安全列表中添加发件人和收件人。

  - **阻止发件人**   与安全发件人一样，用户也可以通过将不受欢迎的发件人添加到阻止发件人列表来阻止这些发件人。

  - **安全域**   该域是 SMTP 地址中 @ 符号后面的部分。例如，contoso.com 是 masato@contoso.com 地址中的域。Outlook 用户可以向安全列表中添加发送域。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>默认情况下，Exchange 在安全列表聚合过程中不包含域。但是，您可以将安全列表聚合配置为包含反垃圾邮件代理的安全域数据。有关详细信息，请参阅<a href="configure-content-filtering-to-use-safe-domain-data-exchange-2013-help.md">配置内容筛选以使用安全域数据</a>。</td>
    </tr>
    </tbody>
    </table>


  - **外部联系人**   安全列表聚合中可以包含两种类型的外部联系人。第一种类型的外部联系人包含 Outlook 用户已向其发送邮件的联系人。只有 Outlook 用户在 Outlook 2007 中的\&quot;垃圾邮件\&quot;设置中选择了相应的选项，此类联系人才会添加到安全发件人列表中。
    
    第二种类型的外部联系人包含用户的 Outlook 联系人。用户可以将这些联系人添加到或导入 Outlook 中。只有 Outlook 用户在 Outlook 2010 或 Outlook 2007 中的\&quot;垃圾邮件筛选器\&quot;设置中选择了相应的选项，此类联系人才会添加到安全发件人列表中。

返回顶部

## Exchange 如何使用安全列表集合

安全列表集合存储在用户的邮箱服务器上。用户在安全列表集合中最多可以有 1024 个唯一条目。Exchange 2013 带有一个邮箱助理（称为垃圾邮件选项邮箱助理），可监视对邮箱的安全列表集合的更改。它还会将这些更改复制到 Active Directory（安全列表集合存储在后者的每个用户对象中）。如果将安全列表集合存储在 Active Directory 的用户对象中，则将使用 Exchange 2013 的反垃圾邮件功能聚合安全列表集合，并针对最少的存储和复制优化安全列表集合。Exchange 在内容筛选过程中使用安全列表集合数据。如果您已经在您的外围网络中订阅了边缘传输服务器，则 Microsoft Exchange EdgeSync 服务将复制安全列表集合至边缘传统服务器上的 Active Directory Lightweight Directory Service (AD LDS) 实例。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>尽管安全收件人数据存储于 Outlook 中且可以聚合到安全列表集合中，但内容筛选功能不会对安全收件人数据进行操作。</td>
</tr>
</tbody>
</table>


返回顶部

## 安全列表集合条目的哈希值计算

安全列表集合条目在跨三个用户对象属性 **msExchSafeSenderHash**、**msExchSafeRecipientHash** 和 **msExchBlockedSendersHash**（作为二进制大对象）存储为数组集之前单向计算哈希值 (SHA-256)。计算数据哈希值时，将生成固定长度的输出，并且输出可能是唯一的。若要计算安全列表集合条目的哈希值，将生成 4 个字节的哈希值。从 Internet 接收邮件时，Exchange 将计算发件人地址的哈希值，并将其与代表邮件收件人 Outlook 用户存储的哈希值进行比较。如果发件人与安全发件人哈希值匹配，将不对邮件进行内容筛选。如果发件人与阻止发件人哈希值匹配，则会阻止该邮件。

安全列表集合条目的单向哈希值计算执行下列重要功能：

  - **最小化存储空间和复制空间**   大多数情况下，哈希值计算可以减小计算哈希值的数据的大小。因此，保存和传输安全列表集合的哈希值版本可以节省存储空间并缩短复制时间。例如，在安全列表集合中包含 200 个条目的用户将创建大约 800 个字节的哈希值数据，在 Active Director 中存储和复制。

  - **使恶意用户无法使用用户安全列表集合**   因为单向哈希值无法反向工程为原始 SMTP 地址或域，所以，安全列表集合不会为可能威胁 Exchange 服务器安全的恶意用户生成可使用的电子邮件地址。

返回顶部

## 启用安全列表聚合

默认情况下，Exchange 2013 中启用了安全列表聚合。与 Exchange Server 2007 中不同，您不需要手动运行 **Update-SafeList** cmdlet 来计算哈希值并将安全列表集合数据写入 Active Directory。在 Exchange 2013 中，安全列表集合数据由垃圾邮件选项邮箱助理写入 Active Directory。

要使 Active Directory 中的安全聚合数据可用于外围网络中的边缘传输服务器，必须安装并配置 Microsoft Exchange EdgeSync 服务，以便将安全列表聚合数据复制到 AD LDS。

您仍然可以通过 **UpdateSafelist** cmdlet 来手动运行安全列表聚合。然而，您应了解在运行该命令时可能会生成的网络和复制通信。如果在大量使用安全列表的多个邮箱运行 **Update-Safelist**，则可能生成大量通信。如果要对多个邮箱运行该命令，则建议您在非通信高峰期或非上班时间运行该命令。

**Update-SafeList** cmdlet 将从用户邮箱读取安全列表集合，对各个项进行散列算法处理，对项进行排序以便于搜索，然后将散列值转换成二进制属性。最后，**Update-SafeList** cmdlet 会将创建的二进制属性与属性中存储的任何值进行比较。如果这两个值完全相同，则 **Update-SafeList** cmdlet 不使用安全列表聚合数据更新用户属性值。如果这两个属性值不同，**Update-SafeList** cmdlet 将更新安全列表聚合值。

返回顶部

