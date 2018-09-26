---
title: '身份: Exchange 2013 Help'
TOCTitle: 身份
ms:assetid: e90fae91-37e7-4fdc-9170-44f0dc965c66
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125042(v=EXCHG.150)
ms:contentKeyID: 50491852
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 身份

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-04_

*Identity* 参数是可以与大多数 cmdlet 一起使用的特殊参数。通过 *Identity* 参数，可以访问引用 MicrosoftExchange Server 2013 中特定对象的唯一标识符。此功能允许您针对特定的 Exchange 2013 对象执行操作。

以下各节介绍 Identity 参数并提供如何有效使用此参数的示例：

Characteristics of the Identity parameter

Wildcard characters in Identity

Examples of the Identity parameter

## Identity 参数的特征

Exchange 2013 中对象的主要唯一标识符始终是 GUID。GUID 是一个 128 位标识符，例如 `63d64005-42c5-4f8f-b310-14f6cb125bf3`。此 GUID 永远不会重复，因此始终是唯一的。但是，您不希望经常键入此类 GUID。因此，*Identity* 参数通常还由其他参数的值，即一个对象中多种参数值的组合构成。这些值还可以保证在对象集中的唯一性。可以指定这些其他参数（例如 *Name* 和 *DistriguishedName*）的值，也可以让系统生成这些值。使用的其他参数（如果有）以及如何设置这些参数取决于您引用的对象。

*Identity* 参数也被视为一种位置参数。如果未指定参数标签，则假定 cmdlet 的第一个参数是 *Identity* 参数。这样可以减少键入命令时的按键次数。有关位置参数的详细信息，请参阅[参数](https://technet.microsoft.com/zh-cn/library/bb124388\(v=exchg.150\))。

以下示例通过使用接收连接器的唯一 *Name* 参数值说明 *Identity* 参数的用法。此示例还说明如何省略 *Identity* 参数名（因为 *Identity* 是一个位置参数）。

```powershell
Get-ReceiveConnector -Identity "From the Internet"
Get-ReceiveConnector "From the Internet"
```

与 Exchange 2013 中的所有对象一样，也可以使用此接收连接器的唯一 GUID 来引用它。例如，如果还向名为 `"From the Internet"` 的接收连接器分配了 GUID `63d64005-42c5-4f8f-b310-14f6cb125bf3`，则也可以使用以下命令来检索该接收连接器：

```powershell
Get-ReceiveConnector 63d64005-42c5-4f8f-b310-14f6cb125bf3
```

返回顶部

## Identity 中的通配符

运行 cmdlet 时，某些 **Get** cmdlet 可以接受通配符 (`*`) 作为提交给 *Identity* 的值的一部分。通过在 *Identity* 参数中使用通配符，可以指定部分名称并检索与该部分名称匹配的对象列表。可以将通配符放在 *Identity* 值的开头或末尾，但不能将它放在字符串中间。例如，`Get-Mailbox David*` 和 `Get-Mailbox *anders*` 命令是有效命令，但 `Get-Mailbox Reb*ca` 不是有效命令。

某些 **Get** cmdlet 会检索 Exchange 2013 中按层次结构或父子关系组织的对象。也就是说，可能存在一个父对象集合，这些父对象还包含各自的子对象。具有父子关系的对象可能具有语法为 `<parent>\<child>` 的 *Identity*。

当 *Identity* 参数的语法为 `<parent>\<child>` 时，某些 cmdlet 将允许您使用通配符 (\*) 替换所有或部分父名称或者子名称。例如，如果要在所有父对象中查找名为\&quot;Contoso\&quot;的所有子对象，可以使用语法 `"*\Contoso"`。同样，如果要查找 `"ServerA" ` 父对象下存在的部分名称为\&quot;Auth\&quot;的所有子对象，可以使用语法 `"ServerA\Auth*"`。

某些（但并非全部）cmdlet 允许您在运行命令时仅指定 Identity 参数的子部分。当您这样做时，这些 cmdlet 将默认为所访问的当前父对象。例如，MBX1 和 MBX2 上都存在名为\&quot;Contoso Receive Connector\&quot;的接收连接器。如果在 MBX2 上运行命令 `Get-ReceiveConnector "Contoso Receive Connector"`，将只返回服务器 MBX2 上的接收连接器。

Identity 参数和通配符的特定行为取决于所运行的 cmdlet。有关您要运行的 cmdlet 的详细信息，请参阅该 cmdlet 的特定于功能的内容。

返回顶部

## Identity 参数示例

本主题中介绍的示例说明 *Identity* 参数如何接受不同的唯一值，以引用 Exchange 2013 组织中特定的对象。这些示例还说明如何省略 *Identity* 参数标签，以减少键入命令时的按键次数。

## DSN 邮件

本节中的示例引用可以在 Exchange 2013 组织中配置的发送状态通知 (DSN) 邮件。第一个示例说明如何使用 **Get-SystemMessage** cmdlet 来检索 DSN 5.4.1。在 **Get-SystemMessage** cmdlet 中，*Identity* 参数由在每个 DSN 邮件对象上配置的多个数据片段组成。这些数据片段包括 DSN 的编写语言、DSN 在作用域的内部还是外部，以及以下示例中所示的 DSN 邮件代码：

```powershell
Get-SystemMessage en\internal\5.4.1
```

也可以按以下示例中所示，使用 GUID 来检索此 DSN 邮件，因为 Exchange 2013 中的所有对象都具有一个 GUID：

```powershell
Get-SystemMessage 82ca7bde-1c2d-4aa1-97e1-f298a6f10222
```

有关与 **SystemMessage** cmdlet 结合使用的 *Identity* 参数构成的详细信息，请参阅 [DSN 邮件标识](dsn-message-identity-exchange-2013-help.md)。

## 管理角色项

本节中的示例引用构成 Exchange 2013 中的管理角色的管理角色项。管理角色用于控制授予给管理员和最终用户的权限。管理角色项由以下两部分组成：相关联的管理角色和一个 cmdlet。Identity 参数同样由管理角色名称和 cmdlet 名称组成。例如，以下是 `Mail Recipients` 角色的 **Set-Mailbox** cmdlet 的角色条目：

```powershell
Mail Recipients\Set-Mailbox
```

`Mail Recipients\Set-Mailbox` 角色条目是 `Mail Recipients` 角色中的若干个角色条目之一。若要查看 `Mail Recipients` 角色中的所有角色项，可以使用以下命令：

```powershell
Get-ManagementRoleEntry "Mail Recipients\*"
```

若要查看 `Mail Recipients` 角色中包含字符串\&quot;`Mailbox`\&quot;的所有角色项，可以使用以下命令：

```powershell
Get-ManagementRoleEntry "Mail Recipients\*Mailbox*"
```

若要查看其中一个角色项为 **Set-Mailbox** 的所有管理角色，可以使用以下命令：

```powershell
Get-ManagementRoleEntry *\Set-Mailbox
```

借助角色项，可以按多种方式使用通配符在 Exchange 2013 查询您感兴趣的信息。

有关管理角色的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

返回顶部

