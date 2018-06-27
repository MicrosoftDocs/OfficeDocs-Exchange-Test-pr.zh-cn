---
title: '在命令行管理程序中使用 RollAlternateserviceAccountCredential.ps1 脚本: Exchange 2013 Help'
TOCTitle: 在命令行管理程序中使用 RollAlternateserviceAccountCredential.ps1 脚本
ms:assetid: 6ac55aae-472a-4ed6-83df-2d0e7b48e05c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff808311(v=EXCHG.150)
ms:contentKeyID: 63918695
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在命令行管理程序中使用 RollAlternateserviceAccountCredential.ps1 脚本

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

您可以使用 Exchange Server 2013 中的 RollAlternateServiceAccountPassword.ps1 脚本更新备用服务帐户凭据（ASA 凭据），并将该更新分发给指定的客户端访问服务器。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 命令行管理程序不会自动加载脚本。必须在所有脚本之前加上“.\” 。例如，要运行 RollAlternateServiceAccountPassword.ps1 脚本，则键入 <code>.\RollAlternateServiceAccountPassword.ps1</code>。</td>
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
<td>此脚本仅提供英文版本。</td>
</tr>
</tbody>
</table>


有关如何使用和编写脚本的详细信息，请参阅[使用 Exchange 命令行管理程序编写脚本](https://technet.microsoft.com/zh-cn/library/bb123798\(v=exchg.150\))。

## 语法

    RollAlternateServiceAccountPassword.ps1 -Scope <Object> -Identity <Object> -Source <Object> -

## 详细描述

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅“客户端访问权限”主题中的“客户端访问安全性”条目。

## 备用服务帐户凭据脚本的详细技术信息

此脚本简化了 ASA 凭据的安装和维护。创建 ASA 凭据并设置适当的服务主体名称后，即可使用脚本将该凭据分发给所有目标客户端访问服务器。

要使用脚本，必须确定要将哪些服务器作为目标以及要将哪个凭据用作 ASA 凭据。

## 服务器作用域

可以选择使脚本以林中的所有客户端访问服务器、特定客户端服务器阵列的所有成员或特定服务器作为目标。可用参数为 *ToEntireForest*、*ToArraryMembers* 和 *ToSpecificServers*。如果使脚本以特定服务器或特定服务器阵列的成员作为目标，则必须使用要用作目标的服务器或服务器阵列名称指定 *Identity* 参数。

## 凭据来源

可以使用脚本从现有服务器复制备用服务帐户密码。或者，也可以指定想要使用的帐户，让脚本为此帐户生成一个新密码。可用参数为 *GenerateNewPasswordFor* 和 *CopyFrom*。*GenerateNewPasswordFor* 参数要求指定一个具有以下格式的帐户字符串：域\\帐户名。如果要使用计算机帐户，则必须在帐户名称末尾附加上“$”，例如，CONTOSO\\ClientServerAcct$。*CopyFrom* 参数将现有客户端访问服务器的名称作为凭据来源。

## 为凭据生成一个新密码

已使用脚本创建密码。无需用户输入。脚本将尝试向所有目标计算机分发密码，然后将尝试用新生成的密码更新 Active Directory 帐户凭据。

新生成的密码长度为 73 个字符，并且能满足标准强密码要求。如果密码要求不同，则可能需要手动设置密码，然后将其复制到目标服务器。

为了防止服务中断，除添加新密码外，脚本还会检查各个客户端访问服务器并维护当前的密码。运行脚本后，共享的 ASA 凭据将能够使用两个密码中的任意之一：存储在 Active Directory 中的当前密码或尚未在 Active Directory 中进行设置的新密码。

将从目标服务器中删除所有不再有效的密码（如过期密码）。如果无法更改 Active Directory 中的密码（可能因为密码已经过期），脚本将尝试重置密码。这将要求帐户运行脚本，以便有权重置 Active Directory 计算机帐户密码或用户帐户密码，具体重置哪个密码取决于备用服务帐户是计算机帐户还是用户帐户。

如果没有为所有目标客户端访问服务器成功更改密码，则更新 Active Directory 密码可能会导致身份验证失败。如果在无人值守模式下运行脚本，除非已成功更新所有目标客户端访问服务器，否则将不会使用新密码更新 Active Directory 密码。如果在有人值守模式下运行脚本，则将询问您是否要更新 Active Directory 中的密码。

## 创建计划任务以自动执行密码维护

如果希望脚本创建计划任务，从而不间断地对密码进行维护，请使用 *CreateScheduledTask* 参数。此参数需要您要创建的任务的名称字符串。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>运行脚本并验证其在有人值守模式下运行正常，然后创建无人值守计划任务。</td>
</tr>
</tbody>
</table>


脚本将在其所在的文件夹内创建一个 .cmd 文件，然后会创建一项任务，以便每三周运行该 cmd 文件。可以使用 Windows 任务计划程序修改计划任务，例如，增加其运行频率或降低其运行频率。默认情况下，将以当前登录用户的身份运行该任务。此外，仅当用户登录到计算机时才会运行脚本。我们建议您修改计划任务，以便始终运行该任务 — 无论用户登录与否。如果其他帐户具有重置密码以及 Exchange 企业管理员角色的 Active Directory 权限，则还可以选择在该帐户下运行计划任务。在创建计划任务时，脚本会自动以无人参与模式运行。

## 脚本作用域范围之外的任务

脚本不会管理 ASA 凭据的 SPN 或允许从服务器中删除备用服务帐户。要从服务器中删除备用服务帐户，请参阅[为负载平衡的客户端访问服务器配置 Kerberos 身份验证](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)中的[Turn Kerberos authentication off](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)部分。

## 脚本疑难解答

建议先运行脚本并验证其在参与模式下运行正常，然后再创建无人参与计划任务。有关疑难解答信息，请参阅 [对 RollAlternateServiceAccountCredential.ps1 脚本进行故障排除](troubleshooting-the-rollalternateserviceaccountcredential-ps1-script-exchange-2013-help.md)。

## 验证脚本

交互运行脚本输出与 -verbose 标志时，该脚本输出应指示哪些脚本操作是成功的。要确认已更新客户端访问服务器，可以验证 ASA 凭据上的上次修改的时间戳。以下示例生成了客户端访问服务器的列表以及上次更新备用服务帐户的时间。

    Get-ClientAccessServer -IncludeAlternateServiceAccountCredentialstatus |Fl Name, AlternateServiceAccountConfiguration

还可以在运行脚本的计算机上检查事件日志。脚本的事件日志条目位于应用程序事件日志中，并且来自来源 *MSExchange Management Application*。下表列出了记录的事件和这些事件的含义。

### 脚本事件 ID 及其说明

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>14001</p></td>
<td><p>开始</p></td>
</tr>
<tr class="even">
<td><p>14002</p></td>
<td><p>成功（信息）</p></td>
</tr>
<tr class="odd">
<td><p>14003</p></td>
<td><p>成功，但有警告。</p>
<p>脚本遇到了一些问题，但是能够克服这些问题，或者，用户输入已确认这些问题不是必需的。如果在交互模式下运行脚本，请读取脚本输出结果以便进一步了解关于警告的详细信息。</p></td>
</tr>
<tr class="even">
<td><p>14004</p></td>
<td><p>失败</p></td>
</tr>
</tbody>
</table>


如果将脚本作为计划任务来运行，则会将其结果记录到名为“RollAlternateServiceAccountPassword”的子文件夹中的 Exchange 服务器“日志记录”文件夹中。

可以使用日志来确认已成功运行任务。

## 参数


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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ToEntireForest</em></p></td>
<td><p>可选</p></td>
<td><p><em>ToEntireForest</em> 参数使脚本以林中的所有客户端访问服务器作为目标。</p></td>
</tr>
<tr class="even">
<td><p><em>ToArrayMembers</em></p></td>
<td><p>可选</p></td>
<td><p><em>ToArrayMembers</em> 参数使脚本以特定客户端访问服务器阵列的所有成员作为目标。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果要使用 <em>ToArrayMembers</em> 参数或 <em>ToSpecificServers</em> 参数，则需要使用 <em>Identity</em> 参数指定服务器名称或服务器阵列名称。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p><em>ToSpecificServers</em></p></td>
<td><p>可选</p></td>
<td><p><em>ToSpecificServers</em> 参数使脚本以特定服务器作为目标。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果要使用 <em>ToArrayMembers</em> 参数或 <em>ToSpecificServers</em> 参数，则需要使用 <em>Identity</em> 参数指定服务器名称或服务器阵列名称。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>必需</p></td>
<td><p><em>Identity</em> 参数指定要用作目标的客户端访问服务器阵列的名称或特定服务器的名称。</p></td>
</tr>
<tr class="odd">
<td><p><em>GenerateNewPasswordFor&lt;String&gt;</em></p></td>
<td><p>可选</p></td>
<td><p><em>GenerateNewPasswordFor</em> 参数指示脚本应该为 ASA 生成一个新密码。该字符串值必须是以下格式的 ASA 帐户：域\帐户名。如果使用的是计算机帐户，则必须在帐户名称末尾附加上 $ 字符。</p></td>
</tr>
<tr class="even">
<td><p><em>CopyFrom&lt;String&gt;</em></p></td>
<td><p>可选</p></td>
<td><p><em>CopyFrom</em> 参数指示从其他客户端访问服务器复制凭据。指定的字符串值是客户端访问服务器的名称。</p></td>
</tr>
<tr class="odd">
<td><p><em>Mode</em></p></td>
<td><p>可选</p></td>
<td><p><em>Mode</em> 开关指定脚本是在有人值守还是无人值守模式下运行。无人值守模式不会提示用户输入内容，并且会在必要时自动选择更多保守选项。</p></td>
</tr>
<tr class="even">
<td><p><em>CreateScheduledTask&lt;String&gt;</em></p></td>
<td><p>可选</p></td>
<td><p><em>CreateScheduledTask</em> 参数通知脚本创建计划任务，以执行 ASA 凭据更新。字符串值是将要创建的计划任务的名称。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此脚本将在其所在的文件夹内创建 .cmd 文件。计划任务将每三周运行一次 .cmd 文件。可以直接在 Windows 任务计划程序中编辑任务，以更改任务的运行频率。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>可选</p></td>
<td><p><em>WhatIf</em> 开关指示命令模拟将对相应对象执行的操作。使用 <em>WhatIf</em> 开关，您可以查看会发生的更改，而无需应用其中任何更改。无需为 <em>WhatIf</em> 开关指定值。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>可选</p></td>
<td><p><em>Confirm</em> 开关令此命令暂停处理，并且需要您在继续处理之前确认此命令将执行的操作。无需为 <em>Confirm</em> 开关指定值。</p></td>
</tr>
<tr class="odd">
<td><p><em>Verbose</em></p></td>
<td><p>可选</p></td>
<td><p><em>Verbose</em> 参数通知脚本执行详细的日志记录，以便将关于脚本操作的其他信息写入日志文件中。</p></td>
</tr>
<tr class="even">
<td><p><em>Debug</em></p></td>
<td><p>可选</p></td>
<td><p><em>Debug</em> 参数通知脚本在调试模式下运行。此参数应该用于确定脚本失败的原因。</p></td>
</tr>
</tbody>
</table>


## 示例

## 示例 1

此示例使用脚本将凭据推送到林中的所有客户端访问服务器，以便进行首次安装。

    .\RollAlternateserviceAccountPassword.ps1 -ToEntireForest -GenerateNewPasswordFor "Contoso\ComputerAccount$" -Verbose

## 示例 2

此示例为用户帐户 ASA 凭据生成新密码，并将该密码分发给客户端访问服务器阵列中那些名称与\*邮箱\*相匹配的所有成员。

    .\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers *mailbox* -GenerateNewPasswordFor "Contoso\UserAccount" -Verbose

## 示例 3

此示例将安排一个名为“Exchange RollAsa”的每月执行一次的自动密码滚动计划任务。将使用一个由脚本生成的新密码在整个林中更新所有客户端访问服务器的 ASA 凭据。已创建计划任务，但未运行脚本。运行计划任务后，将在无人值守模式下运行脚本。

    .\RollAlternateServiceAccountPassword.ps1 -CreateScheduledTask "Exchange-RollAsa" -ToEntireForest -GenerateNewPasswordFor 'contoso\computerAccount$'

## 示例 4

此示例更新名为 CAS01 的客户端访问服务器阵列中的所有客户端访问服务器的 ASA 凭据。将从域 Contoso 中的 Active Directory 计算机帐户 ServiceAc1 中获取凭据。

    .\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers "CAS01" -GenerateNewPasswordFor "CONTOSO\ServiceAc1$" 

## 示例 5

此示例说明，在要增加服务器阵列大小或在进行维护后重新引入阵列成员的情况下，如何才能使用脚本将 ASA 分发给新计算机或重新投入使用的计算机。

必须在客户端访问服务器接收通信之前更新 ASA 凭据。请从任何已正确配置的客户端访问服务器复制共享 ASA 凭据。例如，如果服务器 A 当前拥有一个有效的 ASA 凭据，而您刚向阵列中添加了服务器 B，则可以使用脚本将凭据（包括密码）从服务器 A 复制到服务器 B。如果上次滚动密码时，服务器 B 关机或者尚未成为阵列成员，则可以使用这种方法。

    .\RollAlternateServiceAccountPassword.ps1 -CopyFrom ServerA -ToSpecificServers ServerB -Verbose

