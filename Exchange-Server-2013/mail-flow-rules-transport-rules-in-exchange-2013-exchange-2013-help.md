---
title: '邮件流或传输规则: Exchange 2013 Help'
TOCTitle: 邮件流规则（传输规则）
ms:assetid: c3d2031c-fb7b-4866-8ae1-32928d0138ef
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351127(v=EXCHG.150)
ms:contentKeyID: 50491650
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 邮件流或传输规则

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2017-04-28_

可以使用邮件流规则（也称为传输规则）识别通过 Exchange 2013 组织进行传递的邮件并对其进行操作。邮件流规则与 Outlook 和 Outlook Web App 中提供的收件箱规则类似。主要区别在于邮件流规则在邮件传输过程中对其进行操作，而不是在邮件传递到邮箱后进行操作。邮件流规则包含更丰富的条件、例外和操作集，让你能灵活实现多种类型的邮件策略。

本文介绍了邮件流规则的组件及其工作方式。

若要了解 Exchange Online 中的邮件流规则，请参阅 [Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\))。若要了解 Exchange Online Protection 中的邮件流规则，请参阅 [Exchange Online Protection 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/dn271424\(v=exchg.150\))

可以使用 Exchange 管理中心 (EAC) 或 Exchange 命令行管理程序来管理邮件流规则。有关如何管理传输规则的说明，请参阅 [管理邮件流规则](https://technet.microsoft.com/zh-cn/library/jj657505(v=exchg.150))。

可以选择强制实施每个规则、只是测试规则，或测试每个规则并通知发件人。要了解测试选项的详细信息，请参阅[测试邮件流规则](https://technet.microsoft.com/zh-cn/library/dn831862(v=exchg.150))和[策略提示](https://technet.microsoft.com/zh-cn/library/jj150512(v=exchg.150))。

若要通过使用邮件流规则实现特定的邮件策略，请参阅下列主题：

  - [使用传输规则检查邮件附件](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [常见的附件阻止方案](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/mail-flow-rules/common-attachment-blocking-scenarios)

  - [组织范围内的免责声明、签名、脚注或标头](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [使用邮件流规则以便邮件可以规避待筛选邮件功能](https://technet.microsoft.com/zh-cn/library/dn896639(v=exchg.150))

  - [使用邮件流规则根据字词、短语或模式的列表路由电子邮件](https://technet.microsoft.com/zh-cn/library/dn951131(v=exchg.150))

  - [常见邮件审批方案](https://technet.microsoft.com/zh-cn/library/dd298007(v=exchg.150))

## 邮件流规则组件

邮件流规则由条件、例外、操作和属性组成：

  - **条件**   用于标识要将操作应用到的邮件。一些条件检查邮件头字段（例如“收件人”、“发件人”或“抄送”字段）。其他条件检查邮件属性（例如邮件主题、正文、附件、邮件大小或邮件分类）。大多数条件要求你指定比较运算符（例如等于、不等于或包含）以及要匹配的值。如果没有条件或例外，规则将应用到所有邮件。
    
    若要详细了解 Exchange 2013 中的邮件流规则条件，请参阅 [传输规则条件（谓词）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)。

  - **例外**   选择性地识别操作不应应用到的邮件。条件中可用的相同邮件标识符同样在例外中可用。例外会覆盖条件并阻止规则操作应用于邮件，即使邮件匹配所有配置的条件也是如此。

  - **操作**   指定对匹配规则中的条件而不匹配任何例外的邮件执行哪些操作。有许多可用操作，例如拒绝、删除或重定向邮件、添加其他收件人、在邮件主题中添加前缀或在邮件正文中插入免责声明。
    
    若要详细了解 Exchange 2013 中的邮件流规则操作，请参阅 [传输规则操作](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)。

  - **属性** 指定条件、例外和操作之外的其他规则设置。例如，应何时应用规则、是否强制实施或测试规则，以及规则可用的时间段。
    
    有关详细信息，请参阅本主题中的邮件流规则属性部分。

## 多个条件、例外和操作

下表显示了在规则中处理的多个条件、条件值、例外和操作。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>组件</th>
<th>逻辑</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>多个条件</p></td>
<td><p>AND</p></td>
<td><p>邮件必须匹配该规则的所有条件。如果需要匹配一个条件或另一个条件，请对每个条件使用不同的规则。例如，如果要为带有附件的邮件和包含指定文本的邮件添加相同的免责声明，请为每个条件创建一个规则。在 EAC 中，你可以轻松地复制规则。</p></td>
</tr>
<tr class="even">
<td><p>一个条件具有多个值</p></td>
<td><p>OR</p></td>
<td><p>一些条件允许你指定多个值。邮件必须匹配任一（并非全部）指定值。例如，如果电子邮件的主题为 <strong>Stock price information</strong>，并且<strong>主题包含这些词中的任一个</strong>条件被配置为匹配单词 <strong>Contoso</strong> 或 <strong>stock</strong>，则符合该条件，因为主题中至少包含指定值中的一个。</p></td>
</tr>
<tr class="odd">
<td><p>多个例外</p></td>
<td><p>OR</p></td>
<td><p>如果邮件匹配任何例外，则操作不会应用到邮件。该邮件不需要匹配所有例外。</p></td>
</tr>
<tr class="even">
<td><p>多个操作</p></td>
<td><p>AND</p></td>
<td><p>匹配规则条件的邮件获取规则中指定的所有操作。例如，如果选择了操作“<strong>在邮件主题前面追加</strong>”和“<strong>将收件人添加到密件抄送框</strong>”，则两种操作都将应用至邮件。</p>
<p>要记住，某些操作（例如<strong>在不通知任何人的情况下删除邮件</strong>操作）会阻止后续规则应用于邮件。其他操作，例如“转发邮件”不允许其他操作。</p>
<p>还可以为规则设置操作，以便在应用该规则时，后续规则不会应用至邮件。</p></td>
</tr>
</tbody>
</table>


邮件流规则组件

## 邮件流规则属性

下表介绍了邮件流规则中所提供的规则属性。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的属性名称</th>
<th>PowerShell 中的参数名称</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>优先级</strong></p></td>
<td><p><em>Priority</em></p></td>
<td><p>指示规则应用于邮件的顺序。默认优先级基于规则创建的先后顺序（较早规则的优先级高于较新规则的优先级，先处理具有较高优先级的规则，然后再处理具有较低优先级的规则）。</p>
<p>通过在规则列表中上移或下移规则可更改 EAC 中规则的优先级。在 PowerShell中，可设置优先级编号（0 表示最高优先级）。</p>
<p>例如，如果有一个拒绝包含信用卡号码的邮件的规则，还有一个需要批准的规则，你希望拒绝规则先发生，并停止应用其他规则。</p>
<p>有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/jj657505(v=exchg.150)">设置邮件流规则的优先级</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>模式</strong></p></td>
<td><p><em>Mode</em></p></td>
<td><p>可以指定是否让规则立即处理邮件，或是否在不影响邮件传递（启用或不启用数据丢失防护或 DLP 策略提示）的情况下测试规则。</p>
<p>策略提示在 Outlook 或 Web 上的 Outlook 中显示简短说明，该说明可提供有关邮件创建者可能违反策略的信息。有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/jj150512(v=exchg.150)">策略提示</a>。</p>
<p>有关模式的详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/dn831862(v=exchg.150)">测试邮件流规则</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>在以下日期激活此规则</strong></p>
<p><strong>在以下日期停用此规则</strong></p></td>
<td><p><em>ActivationDate</em></p>
<p><em>ExpiryDate</em></p></td>
<td><p>指定启用该规则的日期范围。</p></td>
</tr>
<tr class="even">
<td><p>选中或未选中 <strong>On</strong> 复选框</p></td>
<td><p>新规则：<strong>New-TransportRule</strong> cmdlet 中的 <em>Enabled</em> 参数。</p>
<p>现有规则：使用 <strong>Enable-TransportRule</strong> 或 <strong>Disable-TransportRule</strong> cmdlet。</p>
<p>该值显示在规则的 <strong>State</strong> 属性中。</p></td>
<td><p>可以创建一个禁用规则，并在准备测试它时将其启用。或者，在不删除该规则的情况下将其禁用，以保留设置。</p></td>
</tr>
<tr class="odd">
<td><p><strong>如果规则处理未完成，则延迟邮件</strong></p></td>
<td><p><em>RuleErrorAction</em></p></td>
<td><p>如果无法完成规则处理，可以指定邮件的处理方式。默认情况下，系统将忽略该规则，但可以选择重新提交邮件进行处理。</p></td>
</tr>
<tr class="even">
<td><p><strong>匹配邮件中的发件人地址</strong></p></td>
<td><p><em>SenderAddressLocation</em></p></td>
<td><p>如果规则使用检查发件人的电子邮件地址的条件或例外，则可以在邮件标头、 邮件信封或同时在两者中查找该值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>停止处理更多规则</strong></p></td>
<td><p><em>SenderAddressLocation</em></p></td>
<td><p>这是一种规则操作，但它看起来像 EAC 中的属性。你可以选择在规则处理完某个邮件后，停止向邮件应用其他规则。</p></td>
</tr>
<tr class="even">
<td><p><strong>注释</strong></p></td>
<td><p><em>Comments</em></p></td>
<td><p>可以输入有关规则的描述性注释。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 如何将邮件流规则应用于邮件

根据组织的已启用邮件流规则来评估组织中的所有邮件。规则会按照 EAC 中“邮件流”\>“规则”页中列出的顺序，或者根据 PowerShell 中相应的 *Priority* 参数值执行。

每个规则还提供在规则匹配时停止处理其他规则的选项。此设置对于匹配多个邮件流规则中条件的邮件而言非常重要（想要哪个规则应用于邮件？全部？还是一个？）。

## 基于消息类型处理的差异

通过组织进行传递的邮件有几种类型。下表显示了哪些邮件类型可以通过邮件流规则进行处理。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>消息类型</th>
<th>是否可以应用规则？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>常规邮件</strong> 包含单个富文本格式 (RTF)、HTML、纯文本邮件正文、多部分或备用的邮件正文集的邮件。</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><strong>Office 365 邮件加密</strong>    邮件通过 Office 365 中的 Office 365 邮件加密 进行加密。有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=392525">Office 365 邮件加密</a>。</p></td>
<td><p>规则可始终根据检查这些标头的条件来访问信封头并处理邮件。</p>
<p>对于检查或修改加密邮件内容的规则，需要验证是否启用了传输解密（强制或可选；默认为可选）。有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=848060">Enable or disable transport decryption</a>（启用或禁用传输解密）。</p>
<p>还可以创建规则，自动解密加密邮件。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=402846">为加密或解密电子邮件定义规则</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>S/MIME 加密邮件</strong></p></td>
<td><p>规则仅可根据检查这些标头的条件来访问信封头并处理邮件。</p>
<p>无法处理具有需要检查邮件内容的条件的规则或可以修改邮件内容的操作。</p></td>
</tr>
<tr class="even">
<td><p><strong>RMS 保护的邮件</strong>   应用 Active Directory Rights Management Services (AD RMS) 或 Azure 权限管理 (RMS) 策略的邮件。</p></td>
<td><p>规则可始终根据检查这些标头的条件来访问信封头并处理邮件。</p>
<p>对于检查或修改 RMS 保护的邮件内容的规则，需要验证是否启用了传输解密（强制或可选；默认为可选）。有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=848060">Enable or disable transport decryption</a>（启用或禁用传输解密）。</p></td>
</tr>
<tr class="odd">
<td><p><strong>已明文签名的邮件</strong>   已签名但未加密的邮件。</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><strong>UM 邮件</strong> 由统一消息服务创建或处理的邮件，如语音邮件、传真、未接来电通知以及使用 Microsoft Outlook Voice Access 创建或转发的邮件。</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><strong>匿名邮件</strong>   由匿名发件人发送的邮件。</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><strong>读取报告</strong>   为响应发件人的阅读回执请求而生成的报告。读取报告具有邮件类别 <code>IPM.Note*.MdnRead</code> 或 <code>IPM.Note*.MdnNotRead</code>。</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


## 传输规则和组成员资格

在使用可展开通讯组成员身份的条件定义传输规则时，将由应用该规则的邮箱服务器上的传输服务缓存收件人的结果列表。这称为“展开组缓存”，还供日志代理用来评估日志规则的组成员身份。默认情况下，展开组缓存存储组成员身份四个小时。此外，还将存储由动态通讯组的收件人筛选器返回的收件人。展开组缓存进行到 Active Directory 的重复往返并避免由于解析组成员身份生成的网络通信。

在 Exchange 2013 中，与展开组缓存相关的此间隔和其他参数是可配置的。您可以减小缓存过期间隔，或一同禁用缓存，以确保可以更频繁地刷新组成员身份。必须为通讯组展开查询计划 Active Directory 域控制器上相应的负载增加。此外，还可以通过重新启动邮箱服务器上的 Microsoft Exchange 传输服务，来清除该服务器上的缓存。必须在要清除缓存的每个邮箱服务器上执行此操作。对于使用基于通讯组成员身份的条件的传输规则，在创建、测试这些规则，以及对这些规则进行故障排除时，还必须考虑展开组缓存的影响。

## 规则存储和复制

在邮箱服务器上创建和配置的邮件流规则存储在 Active Directory 中，这些规则通过组织中所有邮箱服务器上的传输服务读取并应用。创建、修改或删除邮件流规则时，此更改会在组织中的域控制器间进行复制。这样，Exchange 可以为整个组织提供一致的邮件流规则集。

**注意：** 

  - 域控制器之间的复制取决于不受 Exchange 控制的因素（例如，Active Directory 网站数量和网络链接的速度）。因此，在组织中实现邮件流规则时，需要考虑复制延迟。有关 Active Directory 复制的详细信息，请参阅[使用 Windows PowerShell 进行 Active Directory 复制和拓扑管理简介](https://go.microsoft.com/fwlink/p/?linkid=274904)。

  - 每个邮箱服务器缓存已展开通讯组来避免重复的 Active Directory 查询，以确定组成员资格。默认情况下，展开的组缓存中的条目将每四个小时过期一次。因此，在更新展开的组缓存之前，对组成员资格的更改不能通过邮件流规则检测。要强制在邮箱服务器上立即更新缓存，请重启 Microsoft Exchange 传输服务。若要强制更新缓存，需要重启邮箱服务器上的服务。

在边缘传输服务器上创建并配置的邮件流规则存储在服务器上的 AD LDS 本地实例中。邮件流规则不会在边缘传输服务器上进行自动复制。边缘传输服务器上的规则仅应用于通过本地服务器传递的邮件。如果需要在多个边缘传输服务器上应用相同的邮件流规则集，则可以克隆边缘传输服务器配置，或导出和导入邮件流规则。有关详细信息，请参阅[边缘传输服务器克隆配置](edge-transport-server-cloned-configuration-exchange-2013-help.md)和[导入或导出邮件流规则集合](https://technet.microsoft.com/zh-cn/library/jj657505(v=exchg.150))。

每当邮箱服务器或边缘传输服务器上的传输服务检测到已修改的邮件流规则时，事件将记录在事件查看器中的应用程序日志中（邮箱服务器上的事件 ID 4002 以及边缘传输服务器上的事件 ID 16028）。

## 混合环境中的规则复制和存储

Exchange 2013 中有两种常见的混合环境方案：

  - **其中部分组织驻留在 UNRESOLVED\_TOKEN\_VAL(Office365)** 中的混合部署
    
    在混合环境中，本地 Exchange 组织和 UNRESOLVED\_TOKEN\_VAL(Office365) 之间不存在规则复制。因此，你在 Exchange 中创建规则时，需要在 UNRESOLVED\_TOKEN\_VAL(Office365) 中创建匹配规则。你在 UNRESOLVED\_TOKEN\_VAL(Office365) 中创建的规则存储在云中，但你在本地组织中创建的规则存储在本地 Active Directory 中。在混合环境中管理规则时，通过设置为可同时在两个环境进行更改，或者在一个环境中进行更改，然后导出规则并将其导入到另一个环境中，可使这两个规则集保持同步。
    
    > [!IMPORTANT]  
    > 即使 UNRESOLVED_TOKEN_VAL(Office365) 和 Exchange Server 中可用的条件和操作之间有巨大的重叠，两者仍然有差异。如果你计划在两处位置创建相同的规则，请确保要使用的所有条件和操作都可用。要查看 UNRESOLVED_TOKEN_VAL(Office365) 中的可用条件和操作列表，请参阅下列主题：<br />
    > <a href="https://technet.microsoft.com/zh-cn/library/jj919235(v=exchg.150)">在联机 Exchange 邮件流规则条件和例外 （谓语）</a><br />
    > <a href="https://technet.microsoft.com/zh-cn/library/jj919237(v=exchg.150)">联机在 Exchange 邮件流规则操作</a>


  - **与 Exchange 2010 或 Exchange 2007 共存**
    
    与 Exchange 2010 或 Exchange 2007 共存时，无论使用哪版 Exchange Server 创建规则，所有邮件流规则都存储在 Active Directory 中，并可以跨组织进行复制。不过，所有邮件流规则都与用于创建它们的 Exchange Server 服务器版本相关联，并且都存储在 Active Directory 的特定版本容器中。在组织中首次部署 Exchange 2013 时，所有现有规则都会在设置过程中导入 Exchange 2013。不过，之后如有任何更改，两个版本必须进行相同的更改。例如，如果更改了 Exchange 2013（Exchange 命令行管理程序或 EAC）中的现有规则，需要在 Exchange 2010（Exchange 命令行管理程序或 UNRESOLVED\_TOKEN\_VAL(exEMC)）中进行相同的更改。也可以从 Exchange 2013 导出规则，并将它们导入 Exchange 2010。
    
    Exchange 2010 无法处理 **Version** 或 **RuleVersion** 值为 15.*n*.*n*.*n* 的规则。为确保可以处理所有规则，请仅使用值为 14.*n*.*n*.*n* 的规则。

## 详细信息

[管理邮件流规则](https://technet.microsoft.com/zh-cn/library/jj657505(v=exchg.150))

[传输规则条件（谓词）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[传输规则操作](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[传输代理](transport-agents-exchange-2013-help.md)

