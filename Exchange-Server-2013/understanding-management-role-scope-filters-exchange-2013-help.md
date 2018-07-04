---
title: '了解管理角色作用域筛选器: Exchange 2013 Help'
TOCTitle: 了解管理角色作用域筛选器
ms:assetid: 6acc2922-ee9c-41f1-8a0f-10a541e8c273
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298043(v=EXCHG.150)
ms:contentKeyID: 50490766
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 了解管理角色作用域筛选器

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

管理角色作用域筛选器可用来定义可高度自定义的管理作用域。使用作用域筛选器可以创建与收件人、数据库和服务器分段方式相匹配的作用域，以便管理员能够仅管理他们有访问权限的那些对象。作用域筛选器几乎可以使用所有的收件人、数据库或服务器对象属性。

若要使用管理角色作用域筛选器，您必须熟悉管理角色作用域。有关管理角色作用域的详细信息，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

通过使用 **New-ManagementScope** cmdlet 创建 Microsoft Exchange Server 2013 中的已筛选自定义作用域。收件人和配置这两种类型的已筛选作用域（由服务器和数据库作用域组成）可分为常规作用域和独占作用域。以下列表显示了 **New-ManagementScope** cmdlet 上用于创建每个类型的已筛选作用域的参数：

  - **收件人常规已筛选作用域：** 若要创建此类型的已筛选作用域，请使用 *RecipientRestrictionFilter* 参数。

  - **收件人独占已筛选作用域：** 若要创建此类型的已筛选作用域，请使用 *RecipientRestrictionFilter* 参数和 *Exclusive* 开关。

  - **基于服务器的配置常规已筛选作用域：** 若要创建此类型的已筛选作用域，请使用 *ServerRestrictionFilter* 参数。

  - **基于服务器的配置独占已筛选作用域：** 若要创建此类型的已筛选作用域，请使用 *ServerRestrictionFilter* 参数和 *Exclusive* 开关。

  - **基于数据库的配置常规已筛选作用域**   要创建此类型的已筛选作用域，请使用 *DatabaseRestrictionFilter* 参数。

  - **基于数据库的配置独占已筛选作用域**   要创建此类型的已筛选作用域，请使用 *DatabaseRestrictionFilter* 参数和 *Exclusive* 开关。

当您创建已筛选自定义作用域时，该作用域尝试将筛选器与管理角色隐式读取作用域内的任何可访问对象相匹配。如果找到某个对象，筛选器返回的结果中会包含该对象，而且自定义作用域会使该对象对管理角色可用。筛选器无法返回管理角色隐式读取作用域范围之外的结果。

如果您使用 *RecipientRestrictionFilter* 参数指定收件人筛选器，则可使用 *RecipientRoot* 参数指定组织单位 (OU)，以将筛选器限制到该组织单位。当您在 *RecipientRoot* 参数中指定 OU 时，收件人筛选器将尝试仅匹配位于该 OU 内的收件人，而不是整个隐式读取作用域内的收件人。

要使用本主题中包含的可筛选属性创建管理作用域，请参阅[创建常规或独占作用域](create-a-regular-or-exclusive-scope-exchange-2013-help.md)。

## 筛选器语法

收件人和配置筛选器使用相同语法来创建筛选器查询。所有筛选器查询都必须至少具有以下组件：

  - **左括号**   左大括号 ({) 表示筛选器查询的开始。

  - **要检查的属性：** 该属性是要测试的对象的值。例如，该属性可以是收件人对象的城市或部门，服务器配置对象的 Active Directory 站点名称或服务器名称，或者是数据库配置对象的数据库名称。

  - **比较运算符：** 比较运算符指示查询应如何根据属性中存储的值计算您指定的值。例如，比较运算符可以是 **Eq**（表示等于）、**Ne**（表示不等于）、**Like**（表示近似于）等。有关能在 Exchange 命令行管理程序中使用的运算符的完整列表，请参阅[比较运算符](https://technet.microsoft.com/zh-cn/library/bb125229\(v=exchg.150\))。

  - **要比较的值：** 您在筛选器查询中指定的值将与您指定的属性中存储的值进行比较。指定的值必须括在引号 (") 中。如果您想指定部分字符串，则可将您提供的字符串加上通配符 (\*)，并使用支持通配符的比较运算符，例如 **Like**。任何包含部分字符串的字符串都将与筛选器查询匹配。

  - **右括号**   右大括号 (}) 表示筛选器查询的结束。

下列组件是可选组件，可用于创建更复杂的筛选器查询：

  - **圆括号：** 像数学中一样，筛选器查询中的圆括号 ( ) 可用于限定操作发生的顺序。首先计算最里面的圆括号，然后筛选器查询逐个向外操作，直到最外面的圆括号。

  - **逻辑运算符：** 逻辑运算符将一个或多个比较运算符捆绑在一起，并要求筛选器查询计算整个语句。例如，逻辑运算符包括 **And**、**Or** 和 **Not**。

合在一起后，一个简单的查询就类似于 `{ City -Eq "Vancouver" }`。该筛选器将匹配属性 **City** 中的值等于字符串\&quot;Vancouver\&quot;的任何收件人。

另一个复杂些的查询是 `{ ((City -Eq "Vancouver") -And (Department -Eq "Sales")) -Or (Title -Like "*Manager*") }`。筛选器查询的计算顺序如下：

1.  对属性 **City** 和 **Department** 进行计算。根据每个属性内存储值的不同，将每个属性设置为 `True` 或 `False`。

2.  然后计算 **City** 和 **Department** 语句的结果。如果两者都是 `True`，则整个 **And** 语句将变为 `True`。如果一个或两个是 `False`，则整个 **And** 语句将变为 `False`。下列情况适用：
    
      - 如果 **And** 语句的计算结果为 `True`，整个筛选器查询将变为 `True`，因为 **Or** 运算符表示查询的一侧或另一侧必须为 `True`。该对象将进行角色分配。
    
      - 如果 **And** 语句为 `False`，筛选器查询将继续计算 **Title** 属性。

3.  然后计算 **Title** 属性。它将被设置为 `True` 或 `False`，具体取决于 **Title** 属性内存储的值。下列情况适用：
    
      - 如果 **Title** 属性的计算结果为 `True`，整个筛选器查询将变为 `True`，因为 **Or** 运算符表示查询的一侧或另一侧必须为 `True`。该对象将进行角色分配。
    
      - 如果 **Title** 属性的计算结果为 `False`，则整个筛选器查询的计算结果为 `False`，而且该对象不进行角色分配。

下表显示了一个包含值的示例，此示例指示了复杂查询的计算结果何时为 `True`，何时为 `False`。

### 复杂查询

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>City</th>
<th>Department</th>
<th>Title</th>
<th>结果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Sales (True)</p></td>
<td><p>CEO (False)</p></td>
<td><p>因为 <strong>City</strong> 和 <strong>Department</strong> 的计算结果都为 True，所以结果为 True。未计算 <strong>Title</strong>，因为已满足筛选器查询条件。</p></td>
</tr>
<tr class="even">
<td><p>Seattle (False)</p></td>
<td><p>Sales (True)</p></td>
<td><p>IT Manager (True)</p></td>
<td><p>因为 <strong>Title</strong> 的计算结果为 True，所以结果为 True。<strong>City</strong> 和 <strong>Department</strong> 的比较结果将被丢弃，因为 <strong>Title</strong> 的计算结果为 True，已满足筛选器查询条件。</p>

> [!NOTE]
> &amp;quot;IT Manager&amp;quot;和筛选器查询匹配，因为使用了 <strong>Like</strong> 比较运算符，当筛选器查询中使用通配符 (*) 时，该字符串和部分字符串匹配。

</td>
</tr>
<tr class="odd">
<td><p>Vancouver (True)</p></td>
<td><p>Marketing (False)</p></td>
<td><p>Writer (False)</p></td>
<td><p>因为 <strong>City</strong> 和 <strong>Department</strong> 的计算结果并非都为 True，而且 <strong>Title</strong> 的计算结果也不为 True，所以结果为 False。</p></td>
</tr>
</tbody>
</table>


## 可筛选的收件人属性

创建收件人筛选器时，您几乎可以使用收件人对象的任何属性。有关可筛选收件人属性的列表，请参阅 [-RecipientFilter 参数的可筛选属性](https://technet.microsoft.com/zh-cn/library/bb738157\(v=exchg.150\))。本主题讨论的属性可与其他 cmdlet 上的 *RecipientFilter* 参数一起使用，而这些属性中的大多数也可与 **New-ManagementScope** cmdlet 上的 *RecipientRestrictionFilter* 参数一起使用。

## 可筛选的服务器属性

当您使用 *ServerRestrictionFilter* 参数创建管理作用域时，可以使用以下服务器属性：

  - **CurrentServerRole**

  - **CustomerFeedbackEnabled**

  - **DataPath**

  - **DistinguishedName**

  - **ExchangeLegacyDN**

  - **ExchangeLegacyServerRole**

  - **ExchangeVersion**

  - **Fqdn**

  - **Guid**

  - **InternetWebProxy**

  - **Name**

  - **NetworkAddress**

  - **ObjectCategory**

  - **ObjectClass**

  - **ProductID**

  - **ServerRole**

  - **ServerSite**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

## 可筛选的数据库属性

当您使用 *DatabaseRestrictionFilter* 参数创建管理作用域时，可以使用以下数据库属性：

  - **AdminDisplayName**

  - **AllowFileRestore**

  - **BackgroundDatabaseMaintenance**

  - **CircularLoggingEnabled**

  - **DatabaseCreated**

  - **DeletedItemRetention**

  - **Description**

  - **DistinguishedName**

  - **EdbFilePath**

  - **EventHistoryRetentionPeriod**

  - **ExchangeLegacyDN**

  - **ExchangeVersion**

  - **Guid**

  - **IssueWarningQuota**

  - **LogFilePrefix**

  - **LogFileSize**

  - **LogFolderPath**

  - **MasterServerOrAvailabilityGroup**

  - **MountAtStartup**

  - **Name**

  - **ObjectCategory**

  - **ObjectClass**

  - **RetainDeletedItemsUntilBackup**

  - **Server**

  - **WhenChanged**

  - **WhenChangedUTC**

  - **WhenCreated**

  - **WhenCreatedUTC**

