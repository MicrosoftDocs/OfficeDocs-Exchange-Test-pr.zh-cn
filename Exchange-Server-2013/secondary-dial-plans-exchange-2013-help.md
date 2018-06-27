---
title: '辅助拨号计划: Exchange 2013 Help'
TOCTitle: 辅助拨号计划
ms:assetid: ecf474c2-042d-4aaf-9f5b-d5138c56ef39
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff629383(v=EXCHG.150)
ms:contentKeyID: 54913714
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 辅助拨号计划

 

_**适用于：**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2015-03-09_

当为用户启用统一消息时，要求您分配一个分机号码和一个将用户关联到 UM 拨号计划的 UM 邮箱策略。用户启用 UM 后，可以为有相同拨号计划的用户分配其他分机号码，但是同一拨号计划中的分机号码必须是唯一的。在一些部署中，用户可能需要在两个独立的拨号计划中分配相同的分机号码。如果是这个情况，您可以将用户关联到辅助 UM 拨号计划。例如，如果用户有两个物理电话或者在不同地点之间出差，这将非常有用。

**目录**

概述

Use of secondary extensions

UM features that operate differently for secondary dial plans

## 概述

当为用户启用统一消息时，要求您分配一个分机号码和一个将用户关联到单个 UM 拨号计划的 UM 邮箱策略。当为用户启用统一消息并将他们关联到与 SIP URI 或 E.164 拨号计划关联的 UM 邮箱策略时，必须也提供一个 SIP 地址或有用户分机号码的 E.164 号码。UM 使用拨号计划和分机，以及 SIP 地址或 E.164 号码，以在语音邮件提交至用户邮箱时查找用户。

如果您正在使用电话分机拨号计划，并且需要为用户提供相同的分机号码，您将需要创建一个辅助拨号计划，启用为用户启用 UM 并为用户提供相同分机号码。这是因为每个分机号码在拨号计划中必须是唯一的。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>对可以为启用 UM 的用户添加的辅助分机号码的数量没有限制。</td>
</tr>
</tbody>
</table>


有时，用户可能在不同地点之间出差，拥有两个或更多电话，或者可能希望通过一个直接拨入 (DID) 分机号码接收语音邮件，而通过另一个 DID 分机号码接收传真。为此，必须再为用户邮箱添加一个 DID 分机号码，在某些情况下需添加辅助拨号计划。

在某些配置中，在主拨号计划中添加第二个分机或者向辅助拨号计划添加一个或多个分机号码之后，该用户可以使用一个或多个分机号码接收语音邮件或传真。如果希望 UM 应答这些传真呼叫并将其发送到第二个 DID 分机号码，必须将组织中的电话设备配置为将传真呼叫转移到第二个 DID 分机号码。

可以为启用 UM 的用户的邮箱分配下列分机号码：

  - 单个拨号计划的单个分机号码、会话初始协议 (SIP) 地址或 E.164 地址

  - 一个拨号计划上的多个分机号码

  - 两个独立拨号计划上的多个分机号码

当为用户启用 UM 时，必须指定一个分机号码和一个 UM 邮箱策略。当登录到 Outlook Voice Access 检索邮件时，UM 需要有可识别用户的分机号码。UM 邮箱策略包含配置属性集合，以及 UM 应用于已在该策略下启用 UM 的任何用户的值。UM 邮箱策略与其他系统（例如，语音邮件或 PBX）中的\&quot;服务类\&quot;的相似之处在于，对 UM 邮箱策略值的更改可能会影响大量关联用户的行为。

UM 邮箱策略的一个属性指 UM 拨号计划。这代表了一组电话分机。这组分机具有一个编号计划，其中不允许存在重复的分机号码。

因此，用户的分机号码在启用了 UM 的 UM 拨号计划内是唯一的。实际上，UM 拨号计划与分机号码对在组织内必须是唯一的。这是 UM 唯一标识组织中启用了 UM 的用户的一种方法。使用辅助拨号计划可以更容易保持拨号计划和分机号码在组织内唯一。例如，假设某组织有两个 UM 拨号计划：拨号计划 A 和拨号计划 B。某用户在拨号计划 A 和拨号计划 B 中的分机号码分别为 55555 和 66666。当使用辅助拨号计划时，该用户在拨号计划 A 中的分机可以为 55555，在拨号计划 B 中的分机也可以为 55555。在这两种情况下，用户在所使用的拨号计划中的分机是唯一的。

下表定义了论述主分机和辅助分机、Outlook Voice Access 号码及 UM 拨号计划时使用的术语。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主分机</p></td>
<td><p>在用户启用 UM 时指定的分机号码。</p></td>
</tr>
<tr class="even">
<td><p>辅助拨号计划</p></td>
<td><p>在用户启用 UM 时指定的 UM 拨号计划。启用 UM 的用户将在其链接到 UM 邮箱策略时与拨号计划关联。</p></td>
</tr>
<tr class="odd">
<td><p>主 Outlook Voice Access 号码</p></td>
<td><p>用户的主拨号计划的 Outlook Voice Access 号码。如果没有应答或者线路繁忙，该用户的呼叫将被转移到此号码。它也是该用户在要登录到 Outlook Voice Access 时所呼叫的号码。</p></td>
</tr>
<tr class="even">
<td><p>辅助分机</p></td>
<td><p>可添加到启用 UM 的用户的配置中的一个或多个分机号码。</p></td>
</tr>
<tr class="odd">
<td><p>辅助拨号计划</p></td>
<td><p>主拨号计划之外的 UM 拨号计划，可在其中配置一个或多个辅助分机。</p></td>
</tr>
<tr class="even">
<td><p>辅助 Outlook Voice Access 号码</p></td>
<td><p>用户的辅助拨号计划的 Outlook Voice Access 号码。用户要登录到 Outlook Voice Access 时，可以从其辅助分机号码呼叫该号码。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 辅助分机的使用

在大多数部署中，仅为每个启用 UM 的用户配置一个分机。但是，一些较为高级的部署要求为用户添加辅助分机。

当 Microsoft Lync Server 用于 Enterprise Voice 时，统一消息可以提供语音邮件系统。但是，用于 Enterprise Voice 的 UM 拨号计划必须是 Lync Server 的 UM 配置专用的 SIP URI 拨号计划。在这些部署中，用户的分机由 Microsoft 统一通信终结点提供，例如，运行在用户计算机上的 MicrosoftOffice Communicator 或运行在支持的 IP 电话设备上的 Office Communicator Phone Edition。因此，在大多数情况中，用户的主拨号计划必须是用于 Lync Server 的同一 SIP URI 拨号计划。但是，如果用户需要更多的分机号码，您不应向主拨号计划添加其他辅助分机。而是必须先添加一个辅助拨号计划，然后再为启用 UM 的用户添加辅助分机或 EUM 代理地址。

关于添加、删除或更改分机的更多信息，请参阅以下内容之一：

  - [更改分机号码](change-an-extension-number-exchange-2013-help.md)

  - [添加分机号码](add-an-extension-number-exchange-2013-help.md)

  - [删除分机号码](remove-an-extension-number-exchange-2013-help.md)

如果需要为启用 UM 的用户更改 SIP 地址或 E.164 号码，请参阅：

  - [添加 SIP 地址](add-a-sip-address-exchange-2013-help.md)

  - [更改 SIP 地址](change-a-sip-address-exchange-2013-help.md)

  - [删除 SIP 地址](remove-a-sip-address-exchange-2013-help.md)

  - [添加 E.164 号码](add-an-e-164-number-exchange-2013-help.md)

  - [更改 E.164 号码](change-an-e-164-number-exchange-2013-help.md)

  - [删除 E.164 号码](remove-an-e-164-number-exchange-2013-help.md)

## 呼叫应答

统一消息提供了以下两种呼叫应答方式：

  - **呼叫应答**   当用户未应答呼叫而是 UM 接听电话时发生。

  - **Outlook Voice Access**   当用户拨入语音邮件系统来访问其邮箱时使用。

常使用以下两种配置：

  - 一个启用 UM 的用户在主拨号计划中有两个分机号码（一个主分机号码和一个辅助分机号码）。这些分机与用户桌面上的不同电话对应，并连接到相同 PBX。这些不同的号码可供两个单独的受众使用。在此配置中，主分机是\&quot;常规\&quot;工作号码，辅助分机是\&quot;特定于任务\&quot;的号码，可能是支持人员线路或专用的传真号码。

  - 一位启用 UM 的用户在某段时间内（四个星期中可能会有三个星期）于公司的主办公室办公，而其余时间是在位于公司的一个远程办公地点的办公室办公。两个办公室具有不同的 PBX，而且每个 PBX 都有唯一的分机号码。在本例中，该用户被配置为在主办公室 PBX 的主拨号计划中有一个主分机，在另一办公室 PBX 的辅助拨号计划中有一个辅助分机。

在任一配置中，因任一分机号的未应答呼叫而产生的语音邮件或未接来电通知邮件将被发送到用户的收件箱中。

## Outlook Voice Access

您可能希望启用 UM 的用户能够从任何分机（主分机或辅助分机）登录到 Outlook Voice Access。如果可以这样做，可能有一些体系结构限制，防此操作对于所有分机的运行情况都相同。要登录到 Outlook Voice Access，启用 UM 的用户必须执行以下步骤：

1.  拨打 Outlook Voice Access 号码。

2.  如果是从其他电话号码呼叫，则键入其分机号码。

3.  如果未启用 Enterprise Voice，并从统一通信电话、Office Communicator 或 Lync Server 呼叫，则键入其 PIN。

**使用方案**

  - **Outlook Voice Access 有一个分机**   如果用户具有一个主分机，则必须始终呼叫其主 UM 拨号计划的 Outlook Voice Access 号码。如果从其分机号码进行呼叫，系统不会提示其输入分机号码，并将跳过上述步骤中的步骤 2。

  - **Outlook Voice Access 的主拨号计划中有两个分机**   如果用户只有两个分机（主分机和辅助分机），而且主分机和辅助分机属于同一 UM 拨号计划，他们必须始终呼叫该拨号计划的 Outlook Voice Access 号码。如果从主分机或辅助分机进行呼叫，系统不会提示他们输入分机号码，并将跳过上述步骤中的步骤 2。不论使用哪个分机登录，Outlook Voice Access 功能的工作方式均相同。

  - **Outlook Voice Access 的主拨号计划和辅助拨号计划中的分机**   如果用户只有两个分机（主分机和辅助分机），而且主分机和辅助分机属于不同的 UM 拨号计划（主拨号计划和辅助拨号计划），他们应呼叫相应拨号计划的 Outlook Voice Access 号码。他们应从其主分机呼叫主拨号计划的 Outlook Voice Access 号码，从其辅助分机呼叫其辅助拨号计划的 Outlook Voice Access 号码。这样，系统不会提示他们输入分机号码，并将跳过上述步骤中的步骤 2。
    
    不论使用哪个分机登录，只要不涉及出站拨号（例如，\&quot;呼叫发件人\&quot;或\&quot;呼叫办公室\&quot;），Outlook Voice Access 功能的工作方式均相同。但是，需要出站拨号的 Outlook Voice Access 功能不会按用户登录辅助拨号计划时所预期的那样工作，除非两个拨号计划中的出站拨号规则完全相同。要使出站拨号的行为完全相同，必须确保下列属性在主拨号计划和辅助拨号计划上的配置相同：
    
      - 拨号代码（电话交换机接入、国内和国际）
    
      - 国家或地区内拨号代码
    
      - 拨号规则
    
      - 拨号规则组名称

启用 UM 的用户与 UM 邮箱策略关联，而该 UM 邮箱策略与该用户的主拨号计划关联。与启用 UM 的用户的主拨号计划关联的 UM 邮箱策略设置将应用于该用户。如果某用户与包含第二个分机号码的辅助拨号计划关联，仍将应用与主拨号计划关联的 UM 邮箱策略设置。在 Outlook Voice Access 中，不论该用户呼入主拨号计划还是呼入辅助拨号计划，都将应用与主拨号计划关联的相同 UM 邮箱策略设置。

UM 邮箱策略上的 **AllowedInCountryOrRegionGroups** 和 **AllowedInternationalGroups** 属性包含在 UM 拨号计划的 **ConfiguredInCountryOrRegionGroups** 和 **ConfiguredInternationalGroups** 属性上配置的拨号规则组的名称。当启用 UM 的用户呼入 Outlook Voice Access 时，来自与主拨号计划或辅助拨号计划关联的 UM 邮箱策略的出站呼叫规则将应用于该用户发出的呼叫，具体取决于启用 UM 的用户呼入主拨号计划还是辅助拨号计划的 Outlook Voice Access 号码。

例如，如果名为\&quot;Contoso 拨号计划 1\&quot;的主拨号计划的 **ConfiguredInCountryOrRegionGroups** 属性包含名为\&quot;美国和加拿大\&quot;的拨号规则，则 UM 邮箱策略\&quot;Contoso UM 策略 1\&quot;的 **AllowedInCountryOrRegionGroups** 属性也可能包含\&quot;美国和加拿大\&quot;。如果要在\&quot;Contoso 拨号计划 2\&quot;中为\&quot;Contoso UM 策略 2\&quot;中的用户添加第二个分机，必须确保\&quot;Contoso 拨号计划 2\&quot;的 **ConfiguredInCountryOrRegionGroups** 属性也包含名为\&quot;美国和加拿大\&quot;的规则。否则，如果该用户从其辅助分机登录到 Outlook Voice Access，UM 将无法在辅助拨号计划上找到名为\&quot;美国和加拿大\&quot;的规则。如果发生这种情况，UM 将只允许该用户呼叫辅助拨号计划允许任何呼叫方呼叫的号码，这样用户可能会受到更多的限制。

返回顶部

## 对于辅助拨号计划运行方式不同的 UM 功能

有一组 UM 功能可使用辅助拨号计划，但在某些情况下可能不会正常工作。一定要了解在将启用 UM 的用户配置为使用辅助拨号计划后，这些功能会受到怎样的影响。

## 在电话上播放

在 Outlook Web App 中，\&quot;在电话上播放\&quot;使用与用户主拨号计划相关的 VoIP 网关来发出出站呼叫。它将应用来自主拨号计划的拨号规则及与该用户的邮箱关联的 UM 邮箱策略。

## 目录搜索 (Outlook Voice Access)

依据以下规则，在目录中搜索已通过身份验证的用户：

  - 仅当执行搜索的用户已启用 UM，而且在与被呼叫用户相同的拨号计划上有主分机时，才能搜索用户并在之后留下语音邮件或者呼叫用户。如果是这样，按姓名、别名及主分机执行搜索将找到该用户。但是，使用辅助分机进行搜索将不会找到该用户。

  - 如果所搜索的用户已启用 UM，而且其在被叫拨号计划上有辅助分机，则按姓名、别名及辅助分机进行搜索将找到该用户。但是，尽管将提供留下语音邮件和呼叫联系人的选项，但是呼叫联系人选项无法成功。在这种情况下，按主分机进行搜索不会找到该用户。

  - 要找到所搜索的用户并能够发出呼叫或留下语音邮件，启用 UM 的用户应通过其主拨号计划的 Outlook Voice Access 号码使用 Outlook Voice Access，并按姓名、别名或主分机进行搜索。如果使用辅助拨号计划的 Outlook Voice Access 号码呼叫所搜索的用户，则仅当按姓名、别名或辅助分机进行搜索时才能找到该用户。如果使用主分机，用户只能选择留下语音邮件。

## 目录搜索 (Outlook Voice Access)

依据以下规则，在目录中搜索尚未通过身份验证的用户：

  - 仅当所搜索的用户已启用 UM，而且其在被叫拨号计划上有主分机时，才能找到该用户并选择留下语音邮件或发出呼叫。如果是这样，按姓名、别名及主分机进行搜索将找到该用户。但是，按辅助分机进行搜索将不会找到该用户。

  - 如果搜索的用户已启用 UM，在呼叫拨号计划中有一个辅助分机号码，而且选择了呼叫拨号计划中的\&quot;传输和搜索\&quot;\>\&quot;允许呼叫者\&quot;\>\&quot;留下语音消息而不拨打用户电话\&quot;选项，则按姓名、别名和辅助分机进行搜索将找到他们。但是，呼叫者可以选择留下语音邮件，而无法进行呼叫。

  - 要找到某用户并能够发出呼叫或留下语音邮件，呼叫者必须呼叫该用户的主拨号计划的 Outlook Voice Access 号码，并按姓名、别名或该用户的辅助分机进行搜索。如果呼叫用户的辅助 Outlook Voice Access 号码，他们将只有在\&quot;允许呼叫者按别名进行搜索\&quot;选项设置为\&quot;在整个组织中\&quot;的情况下，才能被找到。在这种情况下，将仅提供留下语音邮件的选项。

## 呼叫发件人 (Outlook Voice Access)

当用户呼入 Outlook Voice Access 并选择\&quot;呼叫发件人\&quot;选项时，他们可以向启用 UM 的用户发送电子邮件或语音邮件。可用的选项取决于呼叫者是否与所呼叫的发件人的拨号计划关联。当呼叫者呼入 Outlook Voice Access 号码或呼叫者已通过身份验证时，对启用 UM 的用户的呼叫将遵循以下规则：

  - **电子邮件**   如果电子邮件的发件人是启用 UM 的用户，选择呼叫发件人的选项将导致呼叫在该用户的主拨号计划上配置的发件人的主分机。如果发件人的主分机与呼叫者位于不同的拨号计划上，则仅在当为发件人配置了办公电话、家庭电话或移动电话而且拨号规则配置为允许呼叫时，才会提供\&quot;呼叫发件人\&quot;的提示。

  - **语音邮件**   如果呼叫者是启用 UM 的用户，则呼叫发件人的选项始终都将导致呼叫发件人留下语音邮件所使用的分机。如果此分机的位数与被呼叫的拨号计划不同，则除非置入的拨号规则允许呼叫，否则将不会提供呼叫发件人的提示。例如：
    
      - 如果发件人使用拨号计划上用来发送语音邮件的分机，将提供\&quot;呼叫发件人\&quot;选项。
    
      - 如果发件人使用与用于 Outlook Voice Access 的拨号计划不同的拨号计划中的分机来发送语音邮件，而且两个拨号计划的位数相同，将播放\&quot;呼叫发件人\&quot;选项。呼叫是否成功将取决于 VoIP 网关和 PBX 基础结构是否允许呼叫转移。
    
      - 如果发件人使用与用于 Outlook Voice Access 的拨号计划不同的拨号计划中的分机来发送语音邮件，两个拨号计划的位数不同，而且没有与发件人的分机匹配的出站规则，不会播放\&quot;呼叫发件人\&quot;选项。

返回顶部

