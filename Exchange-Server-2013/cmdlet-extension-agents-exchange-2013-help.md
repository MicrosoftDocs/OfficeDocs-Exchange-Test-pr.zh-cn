---
title: 'cmdlet 扩展代理: Exchange 2013 Help'
TOCTitle: cmdlet 扩展代理
ms:assetid: 0257790d-3988-46c3-8882-25ca11559e84
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335054(v=EXCHG.150)
ms:contentKeyID: 50556516
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# cmdlet 扩展代理

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

Cmdlet 扩展代理是在 cmdlet 运行时，由 Exchange 2013 cmdlet 调用的 Microsoft Exchange Server 2013 中的组件。顾名思义，cmdlet 扩展代理可扩展 cmdlet 的功能，通过帮助处理数据或执行其他基于 cmdlet 要求的操作来调用这些功能。Cmdlet 扩展代理在任何服务器角色上均可用。

这些代理可以修改、替换或扩展 Exchange 命令行管理程序 cmdlet 的功能。代理可以执行以下操作：为所需参数提供值（该值未在命令上提供）、覆盖由用户提供的值、在 cmdlet 运行时执行其他 cmdlet 工作流以外的操作等。

例如，**New-Mailbox** cmdlet 会接受 *Database* 参数，该参数指定要在其中创建新邮箱的邮箱数据库。在 Microsoft Exchange Server 2007 中，如果在运行 **New-Mailbox** cmdlet 时不指定 *Database* 参数，则该命令将失败。但是，在 Exchange 2013 中，**New-Mailbox** cmdlet 在运行时可调用 `Mailbox Resources Management` 代理。如果未指定 *Database* 参数，则 `Mailbox Resources Management` 代理将自动确定适合在其上创建新邮箱的邮箱数据库，并将该值插入到 *Database* 参数中。

只能通过 Exchange 2013 和 Microsoft Exchange Server 2010 cmdlet 来调用 cmdlet 扩展代理。Exchange 2007 cmdlet 以及由其他 Microsoft 和第三方产品提供的 cmdlet 无法调用 cmdlet 扩展代理。脚本也无法直接调用 cmdlet 扩展代理。但是，如果脚本包含 Exchange 2013 cmdlet，则这些 cmdlet 可继续调用 cmdlet 扩展代理。

若要了解与 cmdlet 扩展代理相关的管理任务，请参阅[管理 cmdlet 扩展代理](manage-cmdlet-extension-agents-exchange-2013-help.md)。

## 代理优先级

Cmdlet 运行时，代理的优先级会确定在其中调用代理的顺序。首先调用有较高优先级的代理（更接近零）。当两个或多个代理尝试设置相同属性的值时，代理的优先级变得非常重要。优先级最高的代理将成功设置某个属性值，而所有尝试设置相同属性的较低优先级代理将被忽略。例如，如果优先级为 3 的代理修改了某个对象上的 **Name** 属性，而优先级为 6 的另一个代理也修改相同对象，则由优先级为 6 的代理进行的修改将被忽略。

如果要使用 `Scripting agent` 设置可能由其他较高优先级代理设置的属性的值，则可在以下选项中进行选择：

  - 禁用当前设置该属性的代理。

  - 设置 `Scripting agent`，使其优先级高于要替换的现有代理。

  - 保持代理的优先级相同，并确保在 `Scripting agent` 下运行的脚本符合由其他代理提供的值。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>更改内置代理的优先级或替换内置代理的功能是一项高级操作。请确保您完全了解要进行的更改。</td>
</tr>
</tbody>
</table>


有关更改代理优先级的详细信息，请参阅[管理 cmdlet 扩展代理](manage-cmdlet-extension-agents-exchange-2013-help.md)。

## 内置代理

Exchange 2013 包括多个可在 cmdlet 运行时调用的代理。下表列出了这些代理、其顺序，以及默认情况下是否启用代理。无法在运行 Exchange 2013 的服务器上添加或删除代理。但是，可以使用 `Scripting agent` 运行 Windows PowerShell 脚本来扩展使用代理的 cmdlet 的功能。有关 `Scripting agent` 的详细信息，请参阅本主题后面的\&quot;脚本编写代理\&quot;部分。

如果要将某个特定代理的功能替换为您在自定义脚本（使用 `Scripting agent` 调用）中提供的功能，则可以启用或禁用代理，或者更改代理的优先级。但是，无法禁用某些代理。无法禁用的代理称为\&quot;系统代理\&quot;，其 *IsSystem* 属性设置为 `$True`。下表提供了有关 Exchange 2013 cmdlet 扩展代理（包括系统代理）的信息。

代理的配置存储在组织级别上。启用或禁用代理，或设置其优先级时，您将在组织中的每台服务器上设置该代理配置。但是，将脚本添加到 `Scripting agent` 时除外。您必须分别对每个服务器上的脚本进行更新。有关配置与 `Scripting agent` 配合使用的脚本的详细信息，请参阅本主题后面的\&quot;脚本编写代理\&quot;部分。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果不完全了解每个代理所做的内容以及其与 Exchange cmdlet 交互的方式，则更改代理的优先级，或者启用（或禁用）代理，将会导致意外的结果。在更改任何代理的配置之前，请确保完全了解所要的更改和结果，并验证自定义脚本是否将按预期工作。</td>
</tr>
</tbody>
</table>


### Exchange 2013 cmdlet 扩展代理

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>代理名</th>
<th>优先级</th>
<th>默认情况下启用</th>
<th>系统代理</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Admin Audit Log agent</code></p></td>
<td><p>255</p></td>
<td><p>True</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><code>Scripting agent</code></p></td>
<td><p>6</p></td>
<td><p>False</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Resources Management agent</code></p></td>
<td><p>5</p></td>
<td><p>True</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p><code>OAB Resources Management agent</code></p></td>
<td><p>4</p></td>
<td><p>True</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p><code>Query Base DN agent</code></p></td>
<td><p>3</p></td>
<td><p>True</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p><code>Provisioning Policy agent</code></p></td>
<td><p>2</p></td>
<td><p>True</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p><code>Rus agent</code></p></td>
<td><p>1</p></td>
<td><p>True</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Creation Time agent</code></p></td>
<td><p>0</p></td>
<td><p>True</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>


## 脚本编写代理

可以使用 Exchange 2013 中的 `Scripting agent` cmdlet 扩展代理，将自己的脚本逻辑插入到 Exchange cmdlet 的执行中。通过使用 `Scripting agent`，可以添加条件、覆盖值并设置报告。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>启用了 <code>Scripting agent</code> cmdlet 扩展代理时，每次在运行 Exchange 2013 的服务器上运行 cmdlet 时，都会调用该代理。这不仅包括您在 Exchange 命令行管理程序中直接运行的 cmdlet，还包括 Exchange 服务和 Exchange 管理中心 (EAC) 运行的 cmdlet。强烈建议您在将更新的配置文件复制到 Exchange 2013 服务器并启用 <code>Scripting agent</code> cmdlet 扩展代理之前，测试您的脚本以及对配置文件进行的任何更改。</td>
</tr>
</tbody>
</table>


每次运行 Exchange cmdlet 时，cmdlet 都会调用 `Scripting agent` cmdlet 扩展代理。当调用此代理时，cmdlet 会检查是否有任何脚本配置为由 cmdlet 进行调用。如果应为某个 cmdlet 运行某个脚本，则该 cmdlet 会尝试调用该脚本中定义的任何 API。以下 API 可供使用，并按以下顺序进行调用：

1.  **ProvisionDefaultProperties**   此 API 可以用于在创建对象时设置对象的属性值。当设置某个值时，该值会返回给 cmdlet，而 cmdlet 会对属性设置值。您可以在用户未指定值时对属性填充值，也可以覆盖用户指定的值。此 API 会采用更高优先级代理设置的值。`Scripting agent` cmdlet 扩展代理不会覆盖由更高优先级代理设置的值。

2.  **UpdateAffectedIConfigurable**   此 API 可以用于在完成了所有其他处理（但是尚未调用 `Validate` API）之后，设置对象的属性值。此 API 会采用更高优先级代理设置的值。`Scripting agent` cmdlet 扩展代理不会覆盖由更高优先级代理设置的值。

3.  **Validate**   此 API 可以用于验证将由 cmdlet 设置的对象的属性值。此 API 就在 cmdlet 写入任何数据之前进行调用。可以配置允许 cmdlet 成功或失败的验证检查。如果某个 cmdlet 通过此 API 中的验证检查，则允许该 cmdlet 写入数据。如果 cmdlet 未能通过验证检查，则会返回此 API 中定义的任何错误。

4.  **OnComplete**   此 API 在所有 cmdlet 处理都完成之后使用。它可以用于执行处理后任务，如将数据写入外部数据库。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>当运行带有 <code>Get</code> 动词的 cmdlet 时，不会调用 <code>Scripting agent</code> cmdlet 扩展代理。</td>
</tr>
</tbody>
</table>


## 脚本编写代理配置文件

`Scripting agent` 配置文件包含您希望 `Scripting agent` 运行的所有脚本。该配置文件中的脚本包含在 XML 标记中，这些标记定义脚本的开头和结尾，以及将数据传递给脚本所需的各个输入参数。脚本使用 Windows PowerShell 语法进行编写。该配置文件是使用下表中的元素或属性的 XML 文件。

### 脚本编写代理配置文件的属性

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>属性</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Configuration</code></p></td>
<td><p>不适用</p></td>
<td><p>此元素包含 <code>Scripting agent</code> cmdlet 扩展代理可以运行的所有脚本。<code>Feature</code> 标记是此标记的子级。</p>
<p>配置文件中只有一个 <code>Configuration</code> 标记。</p></td>
</tr>
<tr class="even">
<td><p><code>Feature</code></p></td>
<td><p>不适用</p></td>
<td><p>此元素包含与某个功能相关的一组脚本。每个脚本（在 <code>ApiCall</code> 子标记中定义）都扩展 cmdlet 执行管道的特定部分。此标记包含 <code>Name</code> 和 <code>Cmdlets</code> 属性。</p>
<p><code>Feature</code> 标记下可以有多个 <code>Configuration</code> 标记。</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>此属性包含功能的名称。使用此属性可帮助标识标记中包含的脚本所扩展的功能。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Cmdlets</code></p></td>
<td><p>此属性包含将此功能扩展中的脚本集使用的 Exchange cmdlet 列表。可以指定多个 cmdlet，使用逗号分隔每个 cmdlet。</p></td>
</tr>
<tr class="odd">
<td><p><code>ApiCall</code></p></td>
<td><p>不适用</p></td>
<td><p>此元素包含可以扩展 cmdlet 执行管道某部分的脚本。每个脚本在其扩展的 cmdlet 执行管道中，由 API 调用名称进行定义。下面是可以扩展的 API 名称：</p>
<ul>
<li><p><code>ProvisionDefaultProperties</code></p></li>
<li><p><code>UpdateAffectedIConfigurable</code></p></li>
<li><p><code>Validate</code></p></li>
<li><p><code>OnComplete</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p><code>Name</code></p></td>
<td><p>此属性包括扩展 cmdlet 执行管道的 API 调用的名称。</p></td>
</tr>
<tr class="odd">
<td><p><code>Common</code></p></td>
<td><p>不适用</p></td>
<td><p>此元素包含可以由配置文件中任何脚本使用的功能。</p></td>
</tr>
</tbody>
</table>


每个 Exchange 2013 服务器都将文件 ScriptingAgentConfig.xml.sample 放在 \<*installation path*\>\\V15\\Bin\\CmdletExtensionAgents 文件夹中。如果启用脚本代理 cmdlet 扩展代理，则必须在每个 Exchange 2013 服务器上将此文件重命名为 ScriptingAgentConfig.xml。示例配置文件包含示例脚本，可以使用这些脚本帮助了解如何向配置文件添加脚本。

在向配置文件添加了脚本之后，或如果对配置文件进行了更改，必须在组织中的每个 Exchange 2013 服务器上都更新该文件。必须进行此操作，以确保每个服务器都包含 `Scripting Agent` cmdlet 扩展代理运行的脚本的最新版本。

脚本中常用的某些字符在 XML 中也具有特殊含义。若要在脚本中使用这些字符，请使用转义序列。例如，以下字符使用了转义序列：

  - 使用 `&gt;`，而不是大于号 ( `>` )

  - 使用 `$lt;`，而不是小于号 ( `<` )

  - 使用 `&amp;`，而不是与号 ( `&` )

## 启用脚本编写代理

默认情况下，`Scripting agent` cmdlet 扩展代理处于禁用状态。启用 `Scripting agent` 时，会为整个 Exchange 2013 组织启用该代理。在启用 `Scripting agent` 之前，验证 `Scripting agent` 配置文件是否已在每个 Exchange 2013 服务器上都正确地进行了重命名，并使用脚本进行了更新。如果未正确重命名配置文件，或者从其他 Exchange 2013 服务器向此计算机复制了配置文件，则每当 cmdlet 运行时，就会收到错误消息。

若要启用 `Scripting agent`，必须执行以下操作：

1.  在组织中每个 Exchange 2013 服务器上，将 **\<安装路径\>V15\\Bin\\CmdletExtensionAgents** 中的 ScriptingAgentConfig.xml.sample 文件重命名为 ScriptingAgentConfig.xml。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>可以将配置文件从一个 Exchange 2013 服务器复制到其他 Exchange 2013 服务器。请务必先更新要复制的配置文件，然后再进行复制。</td>
    </tr>
    </tbody>
    </table>


2.  在组织中每个 Exchange 2013 服务器上，将脚本添加到重命名后的配置文件。

3.  启用 `Scripting agent` cmdlet 扩展代理。有关启用 cmdlet 扩展代理的详细信息，请参阅[管理 cmdlet 扩展代理](manage-cmdlet-extension-agents-exchange-2013-help.md)。

## 脚本编写代理优先级

默认情况下，`Scripting agent` cmdlet 扩展代理会在所有其他代理（除了 `Scripting agent` 代理）之后运行。如果要用创建的脚本替换现有代理，则必须禁用其他代理，或更改任一代理的优先级，使 `Scripting agent` cmdlet 扩展代理先运行。有关如何禁用代理或更改代理优先级的详细信息，请参阅[管理 cmdlet 扩展代理](manage-cmdlet-extension-agents-exchange-2013-help.md)。

