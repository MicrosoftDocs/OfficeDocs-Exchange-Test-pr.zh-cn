---
title: '收件人: Exchange 2013 Help'
TOCTitle: 收件人
ms:assetid: 40300ed4-85a5-463d-bb3a-cf787bd44e9d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201680(v=EXCHG.150)
ms:contentKeyID: 50490373
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 收件人

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

接收和发送邮件的人员和资源是任何邮件和协作系统的核心。在 Exchange 组织中，这些人员和资源被称为“收件人”。收件人是 Active Directory（Microsoft Exchange 可以将邮件传递或路由至其中）中所有启用邮件的对象。

## Exchange 收件人类型

Exchange 包含几种显式收件人类型。每个收件人类型在 Exchange 管理中心 (EAC) 中都有标识，并在 Exchange 命令行管理程序的 *RecipientTypeDetails* 属性中具有唯一值。使用显式收件人类型具有下列优点：

  - 可以快速区分出各种收件人类型。

  - 您可以按各种收件人类型进行搜索和排序。

  - 您可以更轻松地对选定收件人类型执行批量管理操作。

  - 由于 EAC 使用收件人类型呈现不同的属性页，因此您可以更轻松地查看收件人属性。例如，您可以查看会议室邮箱的资源容量，但无法查看用户邮箱的资源容量。

下表列出了可用的收件人类型。本主题下文中详细讨论了所有这些收件人类型。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>收件人类型</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>动态通讯组</p></td>
<td><p>发送邮件时使用收件人筛选器和条件派生其成员身份的通讯组。</p></td>
</tr>
<tr class="even">
<td><p>设备邮箱</p></td>
<td><p>一种资源邮箱，分配给不具备位置特性的资源，如便携计算机、投影仪、麦克风或公司汽车。您可以将设备邮箱作为资源包含在会议请求中，从而为用户提供一种简单有效的资源使用方式。</p></td>
</tr>
<tr class="odd">
<td><p>链接邮箱</p></td>
<td><p>分配给独立的受信任林中单个用户的邮箱。</p></td>
</tr>
<tr class="even">
<td><p>邮件联系人</p></td>
<td><p>启用邮件的 Active Directory 联系人，包含存在于 Exchange 组织外部的人员或组织的信息。每个邮件联系人都有一个外部电子邮件地址。发送给邮件联系人的所有邮件都会路由到此外部电子邮件地址。</p></td>
</tr>
<tr class="odd">
<td><p>邮件林联系人</p></td>
<td><p>表示另一个林中收件人对象的邮件联系人。邮件林联系人通常由 Microsoft Identity Integration Server (MIIS) 同步创建。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>邮件林联系人是只读的收件人对象，只能通过 MIIS 或类似的自定义同步来更新。不能使用 EAC 或命令行管理程序删除或修改邮件林联系人。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>邮件用户</p></td>
<td><p>启用邮件的 Active Directory 用户，表示 Exchange 组织外部的用户。每个邮件用户都有一个外部电子邮件地址。发送给邮件用户的所有邮件都会路由到此外部电子邮件地址。</p>
<p>邮件用户类似于邮件联系人，不同的是邮件用户拥有 Active Directory 登录凭据并且可以访问资源。</p></td>
</tr>
<tr class="odd">
<td><p>启用邮件的非通用组</p></td>
<td><p>启用邮件的 Active Directory 全局组或本地组对象。在 Exchange Server 2007 中，废弃了启用邮件的非通用组，并且这些组仅当是从 Exchange 2003 或早期版本的 Exchange 中迁移来时才会存在。您无法使用 Exchange Server 2013 创建非通用通讯组。</p></td>
</tr>
<tr class="even">
<td><p>已启用邮件的公用文件夹</p></td>
<td><p>配置用于接收邮件的 Exchange 公用文件夹。</p></td>
</tr>
<tr class="odd">
<td><p>通讯组</p></td>
<td><p>通讯组是一个启用邮件的 Active Directory 通讯组对象，仅可用于向一组收件人分发邮件。</p></td>
</tr>
<tr class="even">
<td><p>启用邮件的安全组</p></td>
<td><p>启用邮件的安全组是一个 Active Directory 通用安全组对象，可用于向 Active Directory 中的资源分配访问权限，还可以用于分发邮件。</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 收件人</p></td>
<td><p>它是提供统一的已知邮件发件人的一个特殊收件人对象，可以使用该收件人来将系统生成的邮件与其他邮件区分开来。它取代了 Exchange 早期版本中用于系统生成的邮件的“系统管理员”发件人。</p></td>
</tr>
<tr class="even">
<td><p>会议室邮箱</p></td>
<td><p>分配给会议地点（例如会议室、礼堂或培训室）的资源邮箱。会议室邮箱可以包含在会议请求的资源中，从而可以为用户的会议组织活动提供了一种简单有效的方法。</p></td>
</tr>
<tr class="odd">
<td><p>共享邮箱</p></td>
<td><p>一种基本上不与单个用户相关联且通常配置为允许多个用户访问的邮箱。</p></td>
</tr>
<tr class="even">
<td><p>网站邮箱</p></td>
<td><p>一种由用于存储电子邮件的 Exchange 邮箱和用于存储文档的 SharePoint 站点组成的邮箱。用户可使用同一客户端接口访问电子邮件和文档。有关详细信息，请参阅<a href="site-mailboxes-exchange-2013-help.md">网站邮箱</a>。</p></td>
</tr>
<tr class="odd">
<td><p>用户邮箱</p></td>
<td><p>分配给 Exchange 组织中单个用户的邮箱。用户邮箱通常包含邮件、日历项目、联系人、任务、文档以及其它重要的业务数据。</p></td>
</tr>
<tr class="even">
<td><p>Office 365 邮箱</p></td>
<td><p>在混合部署中，Office 365 邮箱由本地 Active Directory 中的邮件用户和 Exchange Online 中的相关云邮箱组成。</p></td>
</tr>
<tr class="odd">
<td><p>链接用户</p></td>
<td><p>链接用户是指邮箱位于其所在林以外的其他林的用户。</p></td>
</tr>
</tbody>
</table>


## 邮箱

邮箱是 Exchange 组织中信息工作人员最常用的收件人类型。每个邮箱都与一个 Active Directory 用户帐户关联。用户可以使用邮箱发送和接收邮件，并可以存储邮件、约会、任务、便笺和文档。邮箱是 Exchange 组织中用户的主要邮件传递和协作工具。

## 邮箱组件

每个邮箱由 Active Directory 用户以及存储在 Exchange 邮箱数据库中的邮箱数据组成（如下图所示）。邮箱的所有配置数据都存储在 Exchange 用户对象的 Active Directory 属性中。邮箱数据库包含与用户帐户关联的邮箱中的实际数据。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>为新用户或现有用户创建邮箱时，将邮箱需要的 Exchange 属性添加到 Active Directory 中的用户对象。在邮箱收到邮件或用户登录邮箱之前，系统不会创建相关的邮箱数据。</td>
</tr>
</tbody>
</table>


**邮箱组件**

![组成邮箱的部分](images/Bb201680.5fcb5e6d-656e-42ae-871f-0eef8aea456b(EXCHG.150).gif "组成邮箱的部分")

<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您删除邮箱，则存储在 Exchange 邮箱数据库中的邮箱数据将被标记为删除，而且关联的用户帐户也将从 Active Directory 中删除。若要保留用户帐户，仅删除邮箱数据，则必须禁用邮箱。</td>
</tr>
</tbody>
</table>


## 邮箱类型

Exchange 支持下列邮箱类型：

  - **用户邮箱**   用户邮箱将分配给 Exchange 组织中的单个用户。用户邮箱为用户提供了丰富的协作平台。用户可以发送和接收邮件、管理其联系人、安排会议和维护任务列表。他们还可以将语音邮件发送到自己的邮箱中。用户邮箱是最常用的邮箱类型，而且通常是分配给组织中用户的邮箱类型。

  - **链接邮箱**   链接邮箱是由独立的受信任林中的用户访问的邮箱。如果组织在资源林中部署 Exchange，则可能需要使用链接邮箱。资源林方案使组织可以将 Exchange 集中在单个林中，同时允许使用一个或多个受信任林中的用户帐户访问 Exchange 组织。
    
    如前所述，每个邮箱必须具有一个与其相关联的用户帐户。但是，在部署了 Exchange 的林中不存在要访问链接邮箱的用户帐户。因此，将与 Exchange 相同的林中存在的已禁用用户帐户与每个链接邮箱关联。下图说明了用于访问链接邮箱的已链接用户帐户和与链接邮箱关联的 Exchange 资源林中已禁用用户帐户之间的关系。
    
    **链接邮箱**
    
    ![具有资源林的复杂 Exchange 组织](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "具有资源林的复杂 Exchange 组织")  

  - **Office 365 邮箱：** 在混合部署中，如果您在 Exchange Online 中创建 Office 365 邮箱，则会在本地 Active Directory 中创建邮件用户。目录同步功能（如果已配置的话）会自动将此新用户对象同步到 Office 365，此对象随后将在 Exchange Online 中转换为云邮箱。您可以将 Office 365 邮箱创建为常规的用户邮箱、会议室和设备的资源邮箱以及共享邮箱。

  - **共享邮箱：** 共享邮箱基本上不与单个用户相关联，且通常配置为允许多个用户访问。
    
    虽然也可以授予其他用户登录访问任意类型邮箱的权限，但共享邮箱专用于此用途。与共享邮箱相关联的 Active Directory 用户必须是已禁用的帐户。在创建共享邮箱后，您必须为所有需要访问此共享邮箱的用户授予权限。

  - **资源邮箱**   资源邮箱是专门用于调度资源的特殊邮箱。与所有邮箱类型相同，资源邮箱具有关联的 Active Directory 用户帐户，但是该帐户必须是已禁用的帐户。资源邮箱分为以下几种类型：
    
      - **会议室邮箱：** 此类邮箱分配给各种会议地点，如会议室、礼堂和培训室。
    
      - **设备邮箱：** 此类邮箱分配给不具备位置特性的资源，如便携计算机、投影仪、麦克风或公司汽车。
    
    您可以将这两种类型的资源邮箱包含在会议请求中，从而为用户提供一种简单有效的资源使用方式。可以配置资源邮箱，使其根据资源所有者定义的资源预订策略来自动处理传入会议请求。例如，可以配置会议室，以自动接受除定期会议外的传入会议请求，这要获取资源所有者的批准。

## 系统邮箱

系统邮箱由 Active Directory 林的根域中的 Exchange 在安装过程中创建。用户或管理员不能登录此类邮箱。系统邮箱是为统一消息 (UM)、迁移、邮件审批和就地电子数据展示等 Exchange 功能创建的邮箱。对于显示在 Active Directory 中的系统邮箱，此表列出了有关这些系统邮箱的信息。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>邮箱</th>
<th>名称</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>组织</p></td>
<td><p>SystemMailbox {bb558c35-97f1-4cb9-8ff7-d53741dc928c}</p></td>
</tr>
<tr class="even">
<td><p>邮件审批</p></td>
<td><p>SystemMailbox {1f05a927-<em>xxxx</em>- <em>xxxx</em> - <em>xxxx</em> -<em>xxxxxxxxxxxx</em>}</p>
<p>其中 <em>x</em> 是为各个 Exchange 林随机分配的唯一编号</p></td>
</tr>
<tr class="odd">
<td><p>UM 数据存储</p></td>
<td><p>SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}</p></td>
</tr>
<tr class="even">
<td><p>发现</p></td>
<td><p>DiscoverySearchMailbox {D919BA05-46A6-415f-80AD-7E09334BB852}</p></td>
</tr>
<tr class="odd">
<td><p>联合电子邮件</p></td>
<td><p>FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042</p></td>
</tr>
<tr class="even">
<td><p>迁移</p></td>
<td><p>Migration.8f3e7716-2011-43e4-96b1-aba62d229136</p></td>
</tr>
</tbody>
</table>


如果您要停用 Exchange 组织中的最后一台邮箱服务器，则应该先使用 [Disable-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997210\(v=exchg.150\)) cmdlet 禁用这些系统邮箱。停用包含这些系统邮箱的邮箱服务器时，应该将这些系统邮箱移到另一个邮箱服务器中，以确保功能不会丧失。

## 规划邮箱

将在已安装邮箱服务器角色的 Exchange 服务器上的邮箱数据库中创建邮箱。为了向邮箱用户提供可靠和有效的平台，对邮箱服务器和数据库部署进行详细规划是至关重要的。若要详细了解如何规划邮箱服务器和数据库，请参阅[规划和部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)。

## 通讯组

通讯组是启用邮件的 Active Directory 组对象，主要用于向多个收件人分发邮件。任何收件人类型都可以是通讯组的成员。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>请注意 Active Directory 和 Exchange 的术语差异。在 Active Directory 中，通讯组是指任何不具有安全上下文的组，而无论它是否已启用邮件。在 Exchange 中，所有启用邮件的组都称为通讯组，无论它们是否具有安全性上下文。</td>
</tr>
</tbody>
</table>


Exchange 支持下列通讯组类型：

  - **通讯组：** 这些是指启用邮件的 Active Directory 通用通讯组对象。仅可用于分发到一组收件人的邮件。

  - **启用邮件的安全组：** 这些是指启用邮件的 Active Directory 通用安全组对象。它们可用于分配对 Active Directory 中各种资源的访问权限，还可用于分发邮件。

  - **启用邮件的非通用组**   这些是启用邮件的 Active Directory 全局或本地组对象。只能创建通用通讯组或对其启用邮件。可以具有从早期版本的 Exchange 中迁移来的、并非通用组的启用邮件组。这些组仍然可以使用 EAC 或命令行管理程序进行管理。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要将本地域或全局组转换为通用组，可以使用命令行管理程序中的 <a href="https://technet.microsoft.com/zh-cn/library/bb123770(v=exchg.150)">Set-Group</a> cmdlet。</td>
    </tr>
    </tbody>
    </table>


## 动态通讯组

动态通讯组是通讯组成员基于特定收件人筛选器而不是已定义的收件人组的通讯组。

与常规通讯组不同，每次向动态通讯组发送邮件时，都将根据指定的筛选器和条件来计算该动态通讯组的成员列表。当一封电子邮件发送到某个动态通讯组时，这封电子邮件会同时传递给组织中与此动态通讯组定义的条件匹配的所有收件人。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>动态通讯组包含在发送邮件时 Active Directory 中其属性与组筛选器相匹配的所有收件人。如果将收件人属性修改为与组筛选器相匹配的属性，则该收件人可能会无意中成为组成员，并开始接收发送到动态通讯组的邮件。定义完善且一致的帐户设置过程可降低发生此问题的机率。</td>
</tr>
</tbody>
</table>


若要创建动态通讯组的收件人筛选器，可以使用固有筛选器。“固有筛选器”是一种常用的筛选器，可用来满足各种收件人筛选标准。可以使用这些筛选器指定想要在动态通讯组中包含的收件人类型。此外，还可以指定收件人必须满足的条件列表。可以根据下列属性创建固有条件：

  - 自定义属性 1–15

  - 省/市/自治区

  - 公司

  - 部门

  - “收件人”容器

您还可以根据收件人属性，而不根据以前列出的那些属性来指定条件。为此，必须使用命令行管理程序创建动态通讯组的自定义查询。请注意，具有自定义收件人筛选器的动态通讯组的筛选器和条件设置只能使用命令行管理程序进行管理。有关如何使用自定义查询创建动态通讯组的示例，请参阅[管理动态通讯组](manage-dynamic-distribution-groups-exchange-2013-help.md)。

## 邮件联系人

邮件联系人通常包含存在于 Exchange 组织外部的人员或组织信息。邮件联系人可在组织的共享通讯簿（又名“全局地址列表 (GAL)”）和其他地址列表中显示，并可作为成员添加到通讯组中。每个联系人都有一个外部电子邮件地址。发送给联系人的所有电子邮件都会自动转发到此外部电子邮件地址。联系人是非常适用于表示 Exchange 组织外部（在共享通讯簿中）不需要访问任何内部资源的人员。邮件联系人的类型如下：

  - **邮件联系人**   这些是启用邮件的 Active Directory 联系人，这些联系人包含存在于 Exchange 组织外部的人员或组织信息。

  - **邮件林联系人**   这些表示另一个林中的收件人对象。这些联系人通常是通过目录同步进行创建。邮件林联系人是只读的收件人对象，可以通过同步来更新或删除。不能使用 Exchange 管理界面来修改或删除邮件林联系人。

## 邮件用户

邮件用户与邮件联系人类似。二者均有外部电子邮件地址，均包含关于 Exchange 组织外部人员的信息，并且均可显示在共享通讯簿和其他地址列表中。不过，与邮件联系人不同，邮件用户拥有 Active Directory 登录凭据，而且可以访问已授予其权限的资源。

如果组织外部的人员需要访问网络中的资源，应为其创建一个邮件用户而不是邮件联系人。例如，对于需要访问服务器基础结构但要使用自己的外部地址的短期顾问，可能需要为其创建邮件用户。

另一种方案是针对不想要维护 Exchange 邮箱的用户创建组织中的邮件用户。例如，收购后，被收购的公司可能自己维护其单独的邮件基础结构，但是可能还需要访问您的网络中的资源。对于这些用户，可为其创建邮件用户，而不为其创建邮箱用户。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 EAC 中，您可以使用“收件人”&gt;“联系人”页面创建和管理邮件用户。暂无单独的邮件用户页面。</td>
</tr>
</tbody>
</table>


## 启用邮件的公用文件夹

公用文件夹旨在作为许多用户之间共享的一个信息库。对公用文件夹启用邮件可以为用户提供更有用的功能。用户除了能够将邮件投递到相应的文件夹以外，还能将电子邮件发送到公用文件夹，有时还能从公用文件夹接收电子邮件。每个启用邮件的文件夹在 Active Directory 中都有一个对象，其中存储了此文件夹的电子邮件地址、通讯簿名称和其他与邮件相关的属性。

您可以使用 EAC 或命令行管理程序来管理公用文件夹。若要详细了解如何管理公用文件夹，请参阅[公用文件夹](public-folders-exchange-2013-help.md)。

## Microsoft Exchange 收件人

Microsoft Exchange 收件人是提供统一的已知邮件发件人的一个特殊收件人对象，可以使用该收件人来将系统生成的邮件与其他邮件区分开来。它取代了在早期版本的 Exchange 中对系统生成的邮件使用的“系统管理员”发件人。

Microsoft Exchange 收件人不是典型的收件人对象（例如邮箱、邮件用户或邮件联系人），并且该收件人不是使用典型的收件人工具进行管理的。但是，可以在命令行管理程序中使用 [Set-OrganizationConfig](https://technet.microsoft.com/zh-cn/library/aa997443\(v=exchg.150\)) cmdlet 来配置 Microsoft Exchange 收件人。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>将系统生成的邮件发送给外部发件人时，不使用 Microsoft Exchange 收件人作为邮件的发件人。使用 <a href="https://technet.microsoft.com/zh-cn/library/bb124151(v=exchg.150)">Set-TransportConfig</a> cmdlet 中的 <em>ExternalPostmasterAddress</em> 参数所指定的电子邮件地址。</td>
</tr>
</tbody>
</table>


## 收件人文档

下表列出了各个主题的链接，可帮助您了解和管理 Exchange 收件人。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">创建用户邮箱</a></p></td>
<td><p>了解如何使用 Exchange 管理中心或 Exchange 命令行管理程序来创建用户邮箱。</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-user-mailboxes-exchange-2013-help.md">管理用户邮箱</a></p></td>
<td><p>了解如何创建用户邮箱、更改邮箱属性和批量编辑多个邮箱的选定属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-linked-mailboxes-exchange-2013-help.md">管理链接的邮箱</a></p></td>
<td><p>了解链接邮箱的要求、如何创建链接邮箱并将它们链接到主帐户，以及如何更改链接邮箱的属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="create-and-manage-distribution-groups-exchange-2013-help.md">创建和管理通讯组</a></p></td>
<td><p>了解如何创建和管理通讯组，以及如何为组织创建组命名策略。</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mail-enabled-security-groups-exchange-2013-help.md">管理启用邮件的安全组</a></p></td>
<td><p>了解如何创建和管理启用邮件的安全组。</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-dynamic-distribution-groups-exchange-2013-help.md">管理动态通讯组</a></p></td>
<td><p>了解如何创建动态通讯组和管理动态通讯组属性，如使用自定义属性和其他属性确定组成员。</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mail-contacts-exchange-2013-help.md">管理邮件联系人</a></p></td>
<td><p>了解如何创建和管理邮件联系人。</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-mail-users-exchange-2013-help.md">管理邮件用户</a></p></td>
<td><p>了解如何创建和管理邮件用户。</p></td>
</tr>
<tr class="odd">
<td><p><a href="create-and-manage-room-mailboxes-exchange-2013-help.md">创建和管理会议室邮箱</a></p></td>
<td><p>了解如何创建会议室邮箱和管理会议室邮箱属性，如启用定期会议和配置预订与调度选项。</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-equipment-mailboxes-exchange-2013-help.md">管理设备邮箱</a></p></td>
<td><p>了解如何创建设备邮箱、配置预订与调度选项，以及如何管理其他邮箱属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="disconnected-mailboxes-exchange-2013-help.md">断开连接的邮箱</a></p></td>
<td><p>了解两类已断开连接的邮箱以及使用方法。</p></td>
</tr>
<tr class="even">
<td><p><a href="custom-attributes-exchange-2013-help.md">自定义属性</a></p></td>
<td><p>了解如何使用自定义属性添加收件人的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/bb124268(v=exchg.150)">收件人命令行管理程序命令中的筛选器</a></p></td>
<td><p>了解如何将固有筛选器或自定义筛选器与命令结合使用来筛选一组收件人。</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-permissions-for-recipients-exchange-online-help.md">管理收件人的权限</a></p></td>
<td><p>了解如何使用 EAC 或命令行管理程序来为用户和组分配权限。</p></td>
</tr>
<tr class="odd">
<td><p><a href="automatic-mailbox-distribution-exchange-2013-help.md">自动邮箱分发</a></p></td>
<td><p>了解自动邮箱分布的工作方式，以及如何控制为新邮箱和移动的邮箱选择哪些邮箱数据库。</p></td>
</tr>
</tbody>
</table>

