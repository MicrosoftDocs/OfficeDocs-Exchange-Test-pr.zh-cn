---
title: 'Exchange 2013/Exchange 2010 混合部署中的传输路由: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2010 混合部署中的传输路由
ms:assetid: 7346bff7-41e0-401c-bd31-34498561f4c4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn393964(v=EXCHG.150)
ms:contentKeyID: 59636467
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2010 混合部署中的传输路由

 

_**适用于：**Exchange Online, Exchange Server, Exchange Server 2013_

_**上一次修改主题：**2016-07-29_

本主题讨论来自 Internet 的入站邮件和发送到 Internet 的出站邮件的路由选项。

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不要在处理或修改 SMTP 通信的内部部署 Exchange 服务器和 Office 365 之间放置任何服务器、服务或设备。内部部署 Exchange 组织和 Office 365 之间的安全邮件流取决于组织之间发送的邮件中包含的信息。支持允许 TCP 端口 25 上的 SMTP 通信通过而无需修改的防火墙。如果服务器、服务或设备处理内部部署 Exchange 组织和 Office 365 之间发送的邮件，此信息将被删除。如果发生这种情况，该邮件将不再被视为组织内部邮件，并且将会对其应用反垃圾邮件筛选、 传输和日记规则以及可能不适用于它的其他策略。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主题中的示例不包括将边缘传输服务器添加到混合部署中。邮件在内部部署组织、Exchange Online 组织与 Internet 之间采用的路由不会随着添加边缘传输服务器而更改。只有内部部署组织中的路由会更改。有关向混合部署添加边缘传输服务器的详细信息，请参阅 <a href="edge-transport-servers-in-exchange-2013-exchange-2010-hybrid-deployments-exchange-2013-help.md">Exchange 2013/Exchange 2010 混合部署中的边缘传输服务器</a>。</td>
</tr>
</tbody>
</table>


## 来自 Internet 的入站邮件

作为计划和配置混合部署的一部分，需要决定是否想要通过 Exchange Online 或本地组织路由来自 Internet 发件人的所有邮件。所有来自 Internet 发件人的邮件最初会传递到所选的组织，然后根据收件人邮箱所在的位置路由。是否选择通过 Exchange Online 或本地组织路由邮件取决于各种因素，包括是否想要对发送到两种组织的所有邮件应用合规性策略以及每个组织中的邮箱数等。

本地和 Exchange Online 组织中发送到收件人的路径取决于在混合部署中决定如何配置 MX 记录。首选方法是配置 MX 记录，使其指向 Office 365 中的 Exchange Online Protection (EOP)，因为该配置提供最准确的垃圾邮件筛选。混合邮件配置向导不配置本地或 Exchange Online 组织的进站 Internet 邮件的路由。如果想要更改进站 Internet 邮件传递的方式，则必须手动配置 MX 记录。

  - **如果更改你的 MX 记录使其指向 Office 365 中的 Exchange Online Protection 服务：**这是混合部署推荐的配置。所有发送到任一组织中的任何收件人的邮件都将首先通过 Exchange Online 组织路由。发往位于本地组织中的收件人的邮件会首先通过 Exchange Online 组织路由，随后传递到本地组织中的收件人。如果你的 Exchange Online 组织中的收件人数量比本地组织中的多，并且如果你希望邮件被 EOP 筛选，则推荐该路由。Exchange Online Protection 需要该配置选项，以提供对垃圾邮件的扫描和阻止。

  - **如果决定保持 MX 记录指向本地组织：   **所有发送到任一组织中的任何收件人的邮件将首先通过你的本地组织路由。发往位于 Exchange Online 中的收件人的邮件会首先通过本地组织进行路由，随后传递到 Exchange Online 中的收件人。对于具有合规性策略（该策略要求日记解决方案检查发送到和发送至组织的邮件）的组织。如果选取了该选项，则 Exchange Online Protection 将不能有效地扫描垃圾邮件。

有关详细信息，请参阅 [Exchange Online 和 Office 365 邮件流最佳做法（概述）](https://technet.microsoft.com/zh-cn/library/jj937232\(v=exchg.150\))。

阅读下面与您计划将从 Internet 收件人发送的邮件路由到内部部署和 Exchange Online 收件人的方式相匹配的章节。

## 通过 Exchange Online 组织路由入站 Internet 邮件

以下步骤和图表举例说明了在指向 MX 记录到 Office 365 组织中的 EOP 服务的情况下，混合部署中出现的入站邮件路径。邮件路径因是否选择启用集中邮件传输而异。

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>对于接收首先传递到 EOP 然后通过 Exchange Online 组织进行路由的邮件的每个内部部署邮箱，可能需要购买 EOP 许可证。有关详细信息，请与您的 Microsoft 经销商联系。</td>
</tr>
</tbody>
</table>


当集中邮件传输被*禁用*（默认配置）时，混合部署中的入站 Internet 邮件按以下路由：

1.  入站邮件从 Internet 发件人发送给收件人 chris@contoso.com 和 david@contoso.com。Chris 的邮箱位于内部部署组织中的 Exchange 2010 邮箱服务器上。David 的邮箱位于 Exchange Online 中。

2.  因为这两个收件人都有 contoso.com 电子邮件地址，并且 contoso.com 的 MX 记录指向 EOP，所以邮件会传递到 EOP。

3.  EOP 将两个收件人的邮件都路由到 Exchange Online。

4.  Exchange Online 对邮件进行病毒扫描并对每个收件人执行查找。通过查找，确定 Chris 的邮箱位于内部部署组织中，而 David 的邮箱位于 Exchange Online 组织中。

5.  Exchange Online 将邮件拆分为两个副本。将邮件的一个副本传递到 David 的邮箱。

6.  将第二个副本从 Exchange Online 发送回 EOP。

7.  EOP 发送邮件到内部部署组织中的 Exchange 2013 客户端访问服务器。

8.  Exchange 2013 客户端访问服务器通过在 Exchange 2013 服务器和 Exchange 2010 集线器传输服务器之间配置的路由组连接器发送邮件。

9.  Exchange 2010 邮箱服务器接收邮件并传递到 Chris 的邮箱。在此示例中，客户端访问和邮箱服务器角色安装在同一 Exchange 2013 服务器上。

**通过 Exchange Online 组织为内部部署组织和 Exchange Online 组织路由邮件，同时禁用集中邮件传输（默认配置）**

![通过 EXO 的入站邮件（未集中传输）](images/Dn393964.23b8c817-1bf1-4a00-b722-a78548c39cb0(EXCHG.150).png "通过 EXO 的入站邮件（未集中传输）")

当集中邮件传输被*启用*时，混合部署中的入站 Internet 邮件按以下路由：

1.  入站邮件从 Internet 发件人发送给收件人 chris@contoso.com 和 david@contoso.com。Chris 的邮箱位于内部部署组织中的 Exchange 2010 邮箱服务器上。David 的邮箱位于 Exchange Online 中。

2.  因为这两个收件人都有 contoso.com 电子邮件地址，并且 contoso.com 的 MX 记录指向 EOP，所以邮件会传递到 EOP 并扫描病毒。

3.  由于启用了集中邮件传输，EOP 会将这两个收件人的邮件路由到内部部署 Exchange 2013 客户端访问服务器。

4.  Exchange 2013 服务器为每个收件人执行查找。通过查找，确定 Chris 的邮箱位于内部部署组织中，而 David 的邮箱位于 Exchange Online 组织中。

5.  Exchange 2013 服务器将邮件拆分为两个副本。邮件的一个副本被发送给 Chris 在内部部署 Exchange 2010 邮箱服务器中的邮箱。

6.  第二个副本从 Exchange 2013 服务器发送回 EOP。

7.  EOP 将邮件发送到 Exchange Online。

8.  Exchange 将邮件发送到 David 的邮箱。在此示例中，客户端访问和邮箱服务器角色安装在同一 Exchange 2013 服务器上。

**通过 Exchange Online 组织为内部部署组织和 Exchange Online 组织路由邮件，同时启用集中邮件传输**

![通过 EXO 的入站邮件（集中传输）](images/Dn393964.8b664544-60d5-4251-90aa-d0797963889f(EXCHG.150).png "通过 EXO 的入站邮件（集中传输）")

## 通过内部部署组织路由入站 Internet 邮件

以下步骤和图表举例说明了在决定保持指向您的内部部署组织的 MX 记录的情况下，混合部署中将出现的入站 Internet 邮件路径。

1.  入站邮件从 Internet 发件人发送给收件人 chris@contoso.com 和 david@contoso.com。Chris 的邮箱位于内部部署组织中的 Exchange 2010 邮箱服务器上。David 的邮箱位于 Exchange Online 中。

2.  因为这两个收件人都有 contoso.com 电子邮件地址，并且 contoso.com 的 MX 记录指向内部部署组织，所以邮件会传递到 Exchange 2010 集线器传输服务器。

3.  Exchange 2010 邮箱服务器使用内部部署全局编录服务器对每个收件人执行查找。通过全局编录查找，该服务器可确定 Chris 的邮箱位于 Exchange 2010 邮箱服务器上，而 David 的邮箱在 Exchange Online 组织中，并具有混合路由地址 david@contoso.mail.onmicrosoft.com。

4.  Exchange 2010 邮箱服务器将邮件拆分为两个副本。将邮件的一个副本传递到 Chris 的邮箱。

5.  邮件的第二个副本通过在 Exchange 2013 服务器与 Exchange 2010 服务器之间配置的路由组连接器发送。

6.  Exchange 2013 邮箱服务器通过配置为使用 TLS 的发送连接器将邮件发送到 EOP。EOP 接收传送给 Exchange Online 组织的邮件。

7.  EOP 将邮件发送到 Exchange Online 组织，在该组织中对邮件进行病毒和基于内容的垃圾邮件的扫描并将其传递到 David 的邮箱。在此示例中，客户端访问和邮箱服务器角色安装在同一 Exchange 2013 服务器上。

**通过内部部署组织为内部部署组织和 Exchange Online 组织路由邮件**

![通过内部部署的入站邮件](images/Dn393964.6fa63ea0-65f5-473a-b0e7-51a2e315286d(EXCHG.150).png "通过内部部署的入站邮件")

## 发送到 Internet 的出站邮件

除了选择如何对发送给组织中的收件人的入站邮件进行路由之外，还可以选择如何对从 Exchange Online 收件人发送的出站邮件进行路由。运行“混合配置”向导时，可以选择两个选项之一：

  - **不启用集中邮件传输**   该选项在混合配置向导中默认选择，可直接将从 Exchange Online 组织发送的出站邮件路由到 Internet。如果无需将任何内部部署合规性策略或其他处理规则应用于从 Exchange Online 组织中的收件人发送的邮件，请使用此选项。

  - **启用集中邮件控制**   选择此选项将通过内部部署组织路由从 Exchange Online 组织发送的出站邮件。除了向同一个 Exchange Online 组织中的其他收件人发送的邮件之外，从 Exchange Online 组织中的收件人发送的所有出站邮件都会通过内部部署组织发送。这使您可以将合规性规则应用于这些邮件以及必须应用于所有收件人（无论这些收件人是处于 Exchange Online 组织中还是处于内部部署组织中）的任何其他过程或要求。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>仅对具有与符合性相关的特定传输需求的组织推荐使用集中式邮件传输。我们建议典型的 Exchange 组织不要启用集中式邮件传输。</td>
    </tr>
    </tbody>
    </table>


从内部部署收件人发送的邮件会始终使用 DNS 直接发送到 Internet 收件人（无论在“混合配置”向导中选择了以上哪个选项）。

以下步骤和图表说明从内部部署收件人发送的邮件的出站邮件路径。

1.  在内部部署 Exchange 2010 邮箱服务器上拥有一个邮箱的 Chris 将一封邮件发送给外部 Internet 收件人 erin@cpandl.com。

2.  Exchange 2010 邮箱服务器将邮件发送到 Exchange 2010 集线器传输服务器。

3.  Exchange 2010 集线器传输服务器查找 cpandl.com 的 MX 记录，然后将邮件发送到位于 Internet 上的 cpandl.com 邮件服务器。

**从内部部署发件人发送给 Internet 收件人的邮件**

![从内部部署发出的出站邮件](images/Dn393964.fdad1c2d-03a9-496b-9c4f-9d791a4adc80(EXCHG.150).png "从内部部署发出的出站邮件")

阅读下面与您计划将从 Exchange Online 组织中收件人发送的邮件路由到 Internet 收件人的方式相匹配的章节。

## 使用 DNS（集中式邮件传输已禁用）传递来自 Exchange Online 的 Internet 邮件。

以下步骤和图表举例说明了在混合配置向导中未选择“启用集中邮件传输”（这是默认配置）的情况下，从 Exchange Online 收件人发送给 Internet 收件人邮件会出现的出站邮件路径。

1.  在内部部署 Exchange Online 组织中拥有一个邮箱的 David 将一封邮件发送给外部 Internet 收件人 erin@cpandl.com。

2.  Exchange Online 对邮件进行病毒扫描并将邮件发送给 Exchange Online EOP 服务。

3.  EOP 会在 MX 记录中查找 cpandl.com，并将邮件发送给位于 Internet 上的 cpandl.com 邮件服务器。

**来自 Exchange Online 发件人的邮件将直接路由到 Internet，同时禁用集中邮件传输（默认配置）**

![直接从 Exchange Online 发出的出站邮件](images/Dn393964.1f7743de-94ef-4d03-a1ed-682739546ad0(EXCHG.150).png "直接从 Exchange Online 发出的出站邮件")

## 通过本地组织路由来自 Exchange Online 的 Internet 邮件（集中式邮件传输已启用

以下步骤和图表举例说明了在混合配置向导中选择“启用集中邮件传输”的情况下，从 Exchange Online 收件人发送给 Internet 收件人邮件会出现的出站邮件路径。

1.  在内部部署 Exchange Online 组织中拥有一个邮箱的 David 将一封邮件发送给外部 Internet 收件人 erin@cpandl.com。

2.  Exchange Online 对邮件进行病毒扫描并将邮件发送给 EOP。

3.  EOP 配置为将所有 Internet 出站邮件发送给内部部署服务器，因此邮件会路由到 Exchange 2013 客户端访问服务器。邮件使用 TLS 发送。

4.  Exchange 2013 客户端访问服务器对 David 的邮件执行遵从性、防病毒以及管理员配置的任何其他过程。

5.  Exchange 2013 客户端访问服务器将邮件转发到 Exchange 2010 集线器传输服务器。在此示例中，客户端访问和邮箱服务器角色安装在同一 Exchange 2013 服务器上。

6.  Exchange 2010 集线器传输服务器查找 cpandl.com 的 MX 记录，然后将邮件发送到位于 Internet 上的 cpandl.com 邮件服务器。

**通过内部部署组织路由的来自 Exchange Online 发件人的邮件（启用集中邮件传输）**

![通过内部部署的 Exchange Online 出站邮件](images/Dn393964.b60237c7-fc7a-472a-a7cd-f7b228cd64e2(EXCHG.150).png "通过内部部署的 Exchange Online 出站邮件")

