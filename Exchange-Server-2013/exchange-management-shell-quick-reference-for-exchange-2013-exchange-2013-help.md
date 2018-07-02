---
title: 'Exchange 2013 的 Exchange 命令行管理程序快速参考: Exchange 2013 Help'
TOCTitle: Exchange 2013 的 Exchange 命令行管理程序快速参考
ms:assetid: 3ea4a105-a93c-48ba-96ce-6170125354e1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ619302(v=EXCHG.150)
ms:contentKeyID: 50490419
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 的 Exchange 命令行管理程序快速参考

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

本主题介绍 Microsoft Exchange Server 2013 的正式发布 (RTM) 版本和更新版本中提供的最常用的 cmdlet，并提供它们的用法示例。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>稍后我们还将添加关于 Exchange 2013 其他方面的更多内容。</td>
</tr>
</tbody>
</table>


有关 Exchange 中的 Exchange 2013 命令行管理程序及所有可用 cmdlet 的详细信息，请参阅下列主题：

  - [将 PowerShell 与 Exchange 2013 结合使用 (Exchange Management Shell)](https://technet.microsoft.com/zh-cn/library/bb123778\(v=exchg.150\))

  - [Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

## 您希望了解哪些内容？

## 常见 cmdlet 操作

大多数 cmdlet 都支持下列与某一特定操作相关的动作。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>New</p></td>
<td><p>New 动作可创建某个实例，例如：新配置设置、新数据库或新 SMTP 连接器。</p></td>
</tr>
<tr class="even">
<td><p>Remove</p></td>
<td><p>Remove 动作删除某个实例，例如邮箱或传输规则。</p>
<p>所有 Remove cmdlet 都支持 <em>WhatIf</em> 和 <em>Confirm</em> 参数。有关这些参数的详细信息，请参阅Important Parameters。</p></td>
</tr>
<tr class="odd">
<td><p>Enable</p></td>
<td><p>Enable 动作启用某个设置或对收件人启用邮件。</p></td>
</tr>
<tr class="even">
<td><p>Disable</p></td>
<td><p>Disable 动作禁用已启用的设置或对收件人禁用邮件。</p>
<p>所有 Disable 任务也支持 <em>WhatIf</em> 和 <em>Confirm</em> 参数。有关这些参数的详细信息，请参阅Important Parameters。</p></td>
</tr>
<tr class="odd">
<td><p>Set</p></td>
<td><p>Set 动作修改对象的特定设置，例如联系人的别名或邮箱数据库中已删除项目的保留时间。</p></td>
</tr>
<tr class="even">
<td><p>Get</p></td>
<td><p>Get 动作查询特定对象或某一对象类型的子集，例如特定邮箱、所有邮箱用户或域中的邮箱用户。</p></td>
</tr>
</tbody>
</table>


## 重要参数

以下参数有助于控制命令运行的方式，并准确指定命令对数据产生影响之前所执行的操作。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Identity</p></td>
<td><p><em>Identity</em> 参数标识任务的唯一对象。通常与 Enable、Disable、Remove、Set 和 Get cmdlet 一起使用。<em>Identity</em> 还是一个位置参数，这意味着在命令行指定参数值时，不必指定 <em>Identity</em>。</p>
<p>例如，<em>Get-Mailbox -Identity user1</em> 查询 <em>user1</em> 的邮箱。<em>Get-Mailbox user1</em> 相当于 <em>Get-Mailbox -Identity user1</em>。</p></td>
</tr>
<tr class="even">
<td><p>WhatIf</p></td>
<td><p><em>WhatIf</em> 参数指示 cmdlet 模拟对要对象执行的操作。使用 <em>WhatIf</em> 参数，可以查看所要发生的更改，而无需实际应用任何更改。默认值为 <em>$true</em>。</p></td>
</tr>
<tr class="odd">
<td><p>Confirm</p></td>
<td><p><em>Confirm</em> 参数可以使 cmdlet 暂停处理，并要求管理员确认在继续处理之前 cmdlet 要执行的操作。默认值为 <em>$true</em>。</p></td>
</tr>
<tr class="even">
<td><p>Validate</p></td>
<td><p><em>Validate</em> 参数使 cmdlet 检查运行操作的所有先决条件是否都已满足，并检查操作是否将成功完成。</p></td>
</tr>
</tbody>
</table>


## 提示和技巧

下列命令与可在管理 Exchange 2013 时使用的各种任务相关联。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-Command</p></td>
<td><p>此 cmdlet 检索可在 Exchange 2013 中执行的所有任务。</p></td>
</tr>
<tr class="even">
<td><p>Get-Command *<em>keyword</em>*</p></td>
<td><p>此 cmdlet 检索 cmdlet 中具有 <em>keyword</em> 的任务。</p></td>
</tr>
<tr class="odd">
<td><p>Get-<em>task</em> | Get-Member</p></td>
<td><p>此 cmdlet 检索 <em>task</em> 的所有属性和方法。</p></td>
</tr>
<tr class="even">
<td><p>Get-<em>task</em> | Format-List</p></td>
<td><p>此 cmdlet 在格式化列表中显示查询的输出。可以通过管道将任意 Get cmdlet 的输出传递给 Format-List 以查看由该命令返回的、存在于对象上的整个属性集，也可以指定希望查看的各个属性（用逗号分隔），如以下示例所示：<em>Get-Mailbox *john* | Format-List alias,*quota</em></p></td>
</tr>
<tr class="odd">
<td><p>Help <em>task</em></p></td>
<td><p>此 cmdlet 检索 Exchange 中任意任务的 Exchange 2013 命令行管理程序帮助信息，如以下示例所示：<em>Help Get-Mailbox</em></p></td>
</tr>
<tr class="even">
<td><p>Get-<em>task</em> | Format-List &gt; <em>file.txt</em></p></td>
<td><p>此 cmdlet 将 <em>task</em> 的输出导出到文本文件：<em>file.txt</em></p></td>
</tr>
</tbody>
</table>


## 权限


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Get-RoleGroupMember &quot;<em>Organization Management</em>&quot;</p></td>
<td><p>此命令检索 <em>Organization Management</em> 管理角色组的成员。</p></td>
</tr>
<tr class="even">
<td><p>Get-ManagementRoleAssignment -Role &quot;<em>Mail Recipient Creation</em>&quot; -GetEffectiveUsers</p></td>
<td><p>此命令检索被授予 <em>Mail Recipient Creation</em> 管理角色提供的权限的所有用户的列表。这包括是角色组或通用安全组 (USG) 成员的用户，其中为这些组分配了 Mail Recipient Creation 角色。但不包括是另一个林中链接角色组成员的用户。</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -RoleAssignee <em>Administrator</em> | Get-ManagementRole | Get-ManagementRoleEntry</p></td>
<td><p>此命令检索用户 <em>Administrator</em> 可以运行的 cmdlet 的列表。</p></td>
</tr>
<tr class="even">
<td><p>ForEach ($RoleEntry in Get-ManagementRoleEntry *\<em>Remove-Mailbox</em> -parameters Identity) {Get-ManagementRoleAssignment -Role $RoleEntry.Role -GetEffectiveUsers -Delegating $False | Where-Object {$_.EffectiveUserName -Ne &quot;All Group Members&quot;} | FL Role, EffectiveUserName, AssignmentChain}</p></td>
<td><p>此命令检索可以运行 <em>Remove-Mailbox</em> cmdlet 的所有用户的列表。</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -WritableRecipient <em>kima</em> -GetEffectiveUsers | FT RoleAssigneeName, EffectiveUserName, Role, AssignmentChain</p></td>
<td><p>此命令检索可以修改 <em>kima</em> 的邮箱的所有用户的列表。</p></td>
</tr>
<tr class="even">
<td><p>New-ManagementScope &quot;<em>Seattle Users</em>&quot; -RecipientRestrictionFilter { <em>City</em> -Eq &quot;<em>Seattle</em>&quot; }</p>
<p>New-RoleGroup &quot;<em>Seattle Admins</em>&quot; -Roles &quot;<em>Mail Recipients</em>&quot;, &quot;<em>Mail Recipient Creation</em>&quot;, &quot;<em>Mailbox Import Export</em>&quot;, -CustomRecipientWriteScope &quot;<em>Seattle Users</em>&quot;</p></td>
<td><p>此命令创建新管理作用域和管理角色组，使角色组的成员能够管理位于 Seattle 的收件人。</p>
<p>首先，将创建 <em>Seattle Users</em> 管理作用域，此作用域只与其用户对象上的 <em>City</em> 属性中有 <em>Seattle</em> 的收件人匹配。</p>
<p>然后，将创建称为 <em>Seattle Admins</em> 的新角色组，并将分配 <em>Mail Recipients</em>、<em>Mail Recipient Creation</em> 和 <em>Mailbox Import Export</em> 角色。该角色组已设置作用域，以便其成员只能管理与 <em>Seattle Users</em> 收件人筛选器作用域匹配的用户。</p></td>
</tr>
<tr class="odd">
<td><p>New-ManagementScope &quot;<em>Vancouver Servers</em>&quot; -ServerRestrictionFilter { <em>ServerSite</em> -Eq &quot;<em>Vancouver</em>&quot; }</p>
<p>$RoleGroup = Get-RoleGroup &quot;<em>Server Management</em>&quot;</p>
<p>New-RoleGroup &quot;<em>Vancouver Server Management</em>&quot; -Roles $RoleGroup.Roles -CustomConfigWriteScope &quot;<em>Vancouver Servers</em>&quot;</p></td>
<td><p>此命令创建新管理作用域并复制现有角色组，使新角色组的成员只能管理 Vancouver Active Directory 站点中的服务器。</p>
<p>首先，将创建 <em>Vancouver Servers</em> 管理作用域，此作用域只与位于 <em>Vancouver</em> Active Directory 站点中的服务器匹配。Active Directory 站点存储在服务器对象上的 <em>ServerSite</em> 属性中。</p>
<p>然后，将创建称为 <em>Vancouver Server Management</em> 的新角色组，此角色组是 <em>Server Management</em> 角色组的副本。但是，此新角色组已设置作用域，只允许其成员管理与 <em>Vancouver Servers</em> 配置筛选器作用域匹配的服务器。</p></td>
</tr>
<tr class="even">
<td><p>Add-RoleGroupMember &quot;<em>Organization Management</em>&quot; -Member <em>davids</em></p></td>
<td><p>此命令将用户 <em>davids</em> 添加到 <em>Organization Management</em> 角色组。</p></td>
</tr>
<tr class="odd">
<td><p>Get-ManagementRoleAssignment -Role &quot;<em>Mail Recipient Creation</em>&quot; -RoleAssignee &quot;<em>Seattle Admins</em>&quot; | Remove-ManagementRoleAssignment</p></td>
<td><p>此命令将 <em>Mail Recipient Creation</em> 角色从 <em>Seattle Admins</em> 角色组中删除。此命令非常有用，因为您不需要知道将角色分配给角色组的管理角色分配的名称。</p></td>
</tr>
</tbody>
</table>


## 远程命令行管理程序


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://<em>ExServer.contoso.com</em>/PowerShell/ -Authentication Kerberos</p>
<p>Import-PSSession $Session</p></td>
<td><p>这些命令将在本地加入域的计算机与完全限定域名 (FQDN) 为 <em>ExServer.contoso.com</em> 的远程 Exchange 2013 服务器之间打开新的远程命令行管理程序会话。在希望管理远程 Exchange 2013 服务器、但本地计算机上仅安装了包含 Windows PowerShell 命令行界面的 Windows Management Framework 的情况下，请使用此命令。此命令将使用您的当前登录凭据对远程 Exchange 2013 服务器进行身份验证。</p></td>
</tr>
<tr class="even">
<td><p>$UserCredential = Get-Credential</p>
<p>$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://<em>ExServer.contoso.com</em>/PowerShell/ -Authentication Kerberos -Credential $UserCredential</p>
<p>Import-PSSession $Session</p></td>
<td><p>这些命令将在本地加入域的计算机与完全限定域名 (FQDN) 为 <em>ExServer.contoso.com</em> 的远程 Exchange 2013 服务器之间打开新的远程命令行管理程序会话。在希望管理远程 Exchange 2013 服务器、但本地计算机上仅安装了包含 Windows PowerShell 的 Windows Management Framework 的情况下，请使用此命令。此命令将使用您显式指定的凭据对远程 Exchange 2013 服务器进行身份验证。</p></td>
</tr>
<tr class="odd">
<td><p>Remove-PSSession $Session</p></td>
<td><p>此命令关闭本地计算机与远程 Exchange 2013 服务器之间的远程命令行管理程序会话。</p></td>
</tr>
<tr class="even">
<td><p>Import-RecipientDataProperty -Identity &quot;Tony Smith&quot; -SpokenName -FileData <em>([Byte[]]$(Get-Content -Path &quot;M:\AudioFiles\TonySmith.wma&quot; -Encoding Byte -ReadCount 0))</em></p></td>
<td><p>此命令将显示一个语法示例（以斜体显示），该语法是使用 FileData 参数在 cmdlet 上将文件导入远程 Exchange 2013 服务器时所必需的。此语法将封装 <em>M:\AudioFiles\TonySmith.wma</em> 文件中包含的数据，并将这些数据传递给 Import-RecipientDataProperty cmdlet 上的 FileData 属性。</p>
<p>FileData 参数在大多数 cmdlet 上使用此语法从本地计算机文件中接受数据。</p></td>
</tr>
<tr class="odd">
<td><p>Export-RecipientDataProperty -Identity tony@contoso.com -SpokenName <em>| ForEach { $_.FileData | Add-Content C:\tonysmith.wma -Encoding Byte}</em></p></td>
<td><p>此命令显示一个语法示例（以斜体显示），该语法是从远程 Exchange 2013 服务器上导出文件时所必需的。该语法将封装存储在由 cmdlet 返回的对象的 FileData 属性中的数据，然后将该数据传递到本地计算机上。然后，将该数据存储到 <em>C:\tonysmith.wma</em> 文件中。</p>
<p>其输出对象具有 FileData 属性的大多数 cmdlet 都使用此语法将数据导出到本地计算机上的文件中。</p></td>
</tr>
</tbody>
</table>

