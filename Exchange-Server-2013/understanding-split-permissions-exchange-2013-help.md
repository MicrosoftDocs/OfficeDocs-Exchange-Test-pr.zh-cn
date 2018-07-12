---
title: '了解拆分权限: Exchange 2013 Help'
TOCTitle: 了解拆分权限
ms:assetid: 2b709e15-63a2-4841-94bc-b289b71166d0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638106(v=EXCHG.150)
ms:contentKeyID: 50490122
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 了解拆分权限

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

组织使用所谓的“拆分权限”模型拆分 Microsoft Exchange Server 2013 对象和 Active Directory 对象的管理。拆分权限使组织可以将特定的权限和相关任务分配给该组织中的特定组。这种工作的分离有助于维护标准和工作流，并且有助于控制组织中的更改。

拆分权限的最高级别是 Exchange 管理和 Active Directory 管理的分离。许多组织都有两个组：管理组织的 Exchange 基础结构（包括服务器和收件人）的管理员，以及管理 Active Directory 基础结构的管理员。对于许多组织而言，这种工作分离很重要，因为 Active Directory 基础结构通常会跨多个位置、域、服务、应用程序甚至 Active Directory 林。Active Directory 管理员必须确保对 Active Directory 进行的更改不会对其他任何服务产生负面影响。因此，通常仅允许一小组的管理员管理该基础结构。

同时，Exchange 的基础结构（包括服务器和收件人）也可能较为复杂，需要有专业知识的人员进行管理。此外，Exchange 存储有关组织业务的高度机密信息。Exchange 管理员可能会访问这些信息。通过限制 Exchange 管理员的人数，组织可以限制能够更改 Exchange 配置以及能够访问敏感信息的人员。

拆分权限通常会区分 Active Directory 中安全主体（如用户和安全组）的创建和对这些对象的后续配置。这样，便可以控制谁能创建对象来授予网络访问权限，因而有助于降低未经授权访问网络的机率。大多数情况下，只有 Active Directory 管理员可创建安全主体，而 Exchange 管理员等其他管理员可管理现有 Active Directory 对象的特定属性。

为了支持将 Exchange 与 Active Directory 的管理分离的不同需要，Exchange 2013 允许您选择是需要共享权限模型还是拆分权限模型。Exchange 2013 提供两种类型的拆分权限模型：RBAC 和 Active Directory。Exchange 2013 默认为共享权限模型。

**目录**

基于角色的访问控制和 Active Directory 的说明

共享权限

拆分权限

RBAC 拆分权限

Active Directory 拆分权限

## 基于角色的访问控制和 Active Directory 的说明


要了解拆分权限，您需要了解 Exchange 2013 中的基于角色的访问控制 (RBAC) 权限模型如何与 Active Directory 协同工作。RBAC 模型控制每个人员可以执行的具体操作以及这些操作所适用的对象。有关本主题中所讨论的多个 RBAC 组件的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

在 Exchange 2013 中，对 Exchange 对象执行的所有任务必须通过 Exchange 命令行管理程序或 Exchange 管理中心 (EAC) 界面来完成。这两个管理工具均使用 RBAC 对所执行的所有任务进行授权。

RBAC 是存在于每个运行 Exchange 2013 的服务器上的组件。RBAC 检查用户执行某个操作是否得到授权：

  - 如果用户未得到授权执行此操作，RBAC 将不允许操作继续进行。

  - 如果用户已获得执行此操作的授权，RBAC 将检查用户是否已获得对所请求的特定对象执行此操作的授权：
    
      - 如果用户已得到授权，RBAC 将允许操作继续进行。
    
      - 如果用户未得到授权，RBAC 将不允许操作继续进行。

如果 RBAC 允许某个操作继续进行，则该操作将在 Exchange 受信任子系统的上下文而不是用户的上下文中执行。Exchange 受信任子系统是一个具有高权限的通用安全组 (USG)，对 Exchange 组织中所有与 Exchange 相关的对象具有读/写访问权限。它还是 Administrators 本地安全组和 Exchange Windows 权限 USG 的成员，允许 Exchange 创建和管理 Active Directory 对象。

> [!CAUTION]  
> 请勿对 Exchange 受信任子系统安全组的成员身份进行任何手动更改。此外，请勿将它添加到对象访问控制列表 (ACL) 或从中删除它。自行更改 Exchange 受信任子系统 USG 可能会对 Exchange 组织造成无法修复的损坏。


请务必了解，用户在使用 Active Directory 管理工具时所具有的 Exchange 权限并不重要。如果用户已通过 RBAC 获得授权，可以在 Exchange 管理工具中执行某个操作，则无论该用户的 Active Directory 权限如何，他/她都可以执行该操作。反之，如果用户是 Active Directory 中的 Enterprise Admin，但未得到在 Exchange 管理工具中执行某个操作（如创建邮箱）的授权，则该操作无法成功执行，因为该用户不具备 RBAC 所要求的权限。

> [!IMPORTANT]  
> 虽然 RBAC 权限模型不适用于“Active Directory 用户和计算机”管理工具，但“Active Directory 用户和计算机”无法管理 Exchange 配置。因此，虽然某个用户可能有权修改 Active Directory 对象的某些属性（如用户的显示名称），但该用户必须使用 Exchange 管理工具并且必须获得 RBAC 的授权才能管理 Exchange 属性。


返回顶部

## 共享权限

共享权限模型是 Exchange 2013 的默认模型。如果这就是要使用的权限模型，则不需要进行任何更改。此模型不会将 Exchange 和 Active Directory 对象的管理从 Exchange 管理工具中分离。它允许管理员使用 Exchange 管理工具在 Active Directory 中创建安全主体。

下表显示了可在 Exchange 中创建安全主体的角色及其默认分配到的管理角色组。

### 安全主体管理角色

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色</th>
<th>角色组</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">邮件收件人创建角色</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">安全组创建和成员身份角色</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
</tbody>
</table>


仅分配有邮件收件人创建角色的角色组、用户或 USG 可以创建安全主体（如 Active Directory 用户）。默认情况下，会向 组织管理 和 收件人管理 角色组分配此角色。因此，这些角色组的成员可以创建安全主体。

仅分配有安全组创建和成员身份角色的角色组、用户或 USG 可以创建安全组或管理其成员身份。默认情况下，仅向 组织管理 角色组分配此角色。因此，仅 组织管理 角色组的成员可以创建或管理安全组的成员身份。

如果希望其他用户能够创建安全主体，可将邮件收件人创建角色和安全组创建和成员身份角色分配到其他角色组、用户或 USG。

为管理 Exchange 2013 中的现有安全主体，邮件收件人角色会默认分配给 组织管理 和 收件人管理 角色组。仅分配有邮件收件人角色的角色组、用户或 USG 可以管理现有安全主体。如果希望其他角色组、用户或 USG 能够管理现有安全主体，则必须为其分配邮件收件人角色。

有关如何将角色添加到角色组、用户或 USG 的详细信息，请参阅下列主题：

  - [管理角色组](manage-role-groups-exchange-2013-help.md)

  - [向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

如果已切换到拆分权限模型但希望改回到共享权限模型，请参阅[为 Exchange 2013 配置共享权限](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md)。

返回顶部

## 拆分权限

如果组织将 Exchange 管理和 Active Directory 管理分离，则需要配置 Exchange 以支持拆分权限模型。如果已正确配置，则只有您希望创建安全主体的管理员（如 Active Directory 管理员）可以执行此操作，且只有 Exchange 管理员可以修改现有安全主体上的 Exchange 属性。这种权限拆分也大致按照 Active Directory 中的域和配置分区进行。分区也称为命名上下文。域分区存储特定域的用户、组和其他对象。配置分区存储使用 Active Directory 的服务（如 Exchange）的林范围配置信息。存储在域分区中的数据通常由 Active Directory 管理员进行管理，但对象可能包含可以由 Exchange 管理员管理的、特定于 Exchange 的属性。存储在配置分区中的数据由将数据存储在此分区中的各个服务的管理员进行管理。对于 Exchange，通常是 Exchange 管理员。

Exchange 2013 支持以下两种类型的拆分权限：

  - **RBAC 拆分权限**   用于在 Active Directory 域分区中创建安全主体的权限由 RBAC 控制。只有 Exchange 服务器、服务以及适当角色组的成员才能创建安全主体。

  - **Active Directory 拆分权限**   从任何 Active Directory 用户、服务或服务器完全删除了用于在 Exchange 域分区中创建安全主体的权限。RBAC 中未提供用于创建安全主体的任何选项。必须使用 Active Directory 管理工具在 Active Directory 中创建安全主体。
    
    > [!IMPORTANT]  
    > 虽然可以通过在安装了 Exchange 2013 的计算机上运行安装程序来启用或禁用 Active Directory 拆分权限，但 Active Directory 拆分权限配置可同时应用于 Exchange 2013 和 Exchange 2010 服务器。但是，它不会对 Microsoft Exchange Server 2007 服务器产生任何影响。


如果您的组织选择使用拆分权限模型而不是共享权限，则建议您使用 RBAC 拆分权限模型。RBAC 拆分权限模型可提供显著提高的灵活性，同时可提供与 Active Directory 拆分权限几乎相同的管理分离，只不过 Exchange 服务器和服务可以在 RBAC 拆分权限模型中创建安全主体。

在安装过程中，系统会询问您是否要启用 Active Directory 拆分权限。如果您选择启用 Active Directory 拆分权限，则只能通过重新运行安装程序并禁用 Active Directory 拆分权限，更改为共享权限或 RBAC 拆分权限。此选项可应用于组织中的所有 Exchange 2010 和 Exchange 2013 服务器。

以下各节更加详细地介绍了 RBAC 和 Active Directory 拆分权限。

返回顶部

## RBAC 拆分权限

RBAC 安全模型修改了默认管理角色分配，将可在 Active Directory 域分区中创建安全主体的人员与管理 Exchange 配置分区中的 Active Directory 组织数据的人员分开。如果管理员是“邮件收件人创建”及“安全组创建和成员身份”角色的成员，则该管理员可创建安全主体，如具有邮箱的用户以及通讯组。这些权限仍与在 Exchange 管理工具之外创建安全主体所需的权限分离。未分配“邮件收件人创建”或“安全组创建和成员身份”角色的 Exchange 管理员仍可以修改安全主体上与 Exchange 相关的属性。Active Directory 管理员也可以选择使用 Exchange 管理工具创建 Active Directory 安全主体。

Exchange 服务器和 Exchange 受信任子系统也有权代表用户以及与 RBAC 集成的第三方程序，在 Active Directory 中创建安全主体。

如果满足以下条件，则 RBAC 拆分权限对于您的组织是个不错的选择：

  - 您的组织不要求仅使用 Active Directory 管理工具并且仅由分配了特定 Active Directory 权限的用户创建安全主体。

  - 您的组织允许服务（如 Exchange 服务器）创建安全主体。

  - 您希望允许从 Exchange 管理工具创建邮箱、启用邮件的用户、通讯组和角色组，从而简化创建这些对象所需的过程。

  - 您希望在 Exchange 管理工具中管理通讯组和角色组的成员身份。

  - 您拥有的第三方程序要求 Exchange 服务器能够代表其创建安全主体。

如果您的组织需要完全分离 Exchange 与 Active Directory 管理，使得不能使用 Active Directory 管理工具或由 Exchange 服务执行任何 Exchange 管理，请参阅本主题后面的 Active Directory 拆分权限一节。

从共享权限切换为 RBAC 拆分权限是一个手动过程，在此过程中，您会从角色组删除创建安全主体所需的权限（在默认情况下会向角色组授予这些权限）。下表显示了可在 Exchange 中创建安全主体的角色及其默认分配到的管理角色组。

### 安全主体管理角色

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色</th>
<th>角色组</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">邮件收件人创建角色</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">安全组创建和成员身份角色</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
</tbody>
</table>


默认情况下，组织管理 和 收件人管理 角色组的成员可以创建安全主体。必须将创建安全主体的权限从内置角色组转移到新创建的角色组。

若要配置 RBAC 拆分权限，必须执行以下操作：

1.  禁用 Active Directory 拆分权限（如果已启用）。

2.  创建角色组，其中将包含能够创建安全主体的 Active Directory 管理员。

3.  在邮件收件人创建角色和新角色组之间创建常规角色分配和委派角色分配。

4.  在安全组创建和成员身份角色和新角色组之间创建常规角色分配和委派角色分配。

5.  删除“邮件收件人创建”角色以及 组织管理 和 收件人管理 角色组之间的常规管理角色分配和委派管理角色分配。

6.  删除“安全组创建和成员身份”角色和 组织管理 角色组之间的常规角色分配和委派角色分配。

完成此操作后，只有新创建角色组的成员能够创建邮箱等安全主体。新组将仅能够创建对象。它将无法配置新对象的 Exchange 属性。Active Directory 管理员（新组的成员）将需要创建对象，然后 Exchange 管理员将需要配置对象的 Exchange 属性。Exchange 管理员将无法使用以下 cmdlet：

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

但是，Exchange 管理员将能够创建和管理特定于 Exchange 的对象（如传输规则和通讯组等），并能够管理任何对象上与 Exchange 相关的属性。

此外，EAC 和 Outlook Web App 中的相关功能（如新建邮箱向导）也将不再可用，如果您尝试使用这些功能，则会生成错误。

如果希望新角色组也能够管理新对象的 Exchange 属性，则还需要将邮件收件人角色分配到新角色组。

有关配置拆分权限模型的详细信息，请参阅[为 Exchange 2013 配置拆分权限](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)。

返回顶部

## Active Directory 拆分权限

对于 Active Directory 拆分权限，必须使用 Active Directory 管理工具在 Active Directory 域分区中创建安全主体（如邮箱和通讯组）。系统会对授予 Exchange 受信任子系统和 Exchange 服务器的权限进行了一些更改，以限制 Exchange 管理员和服务器可以执行的操作。当您启用 Active Directory 拆分权限时，会发生以下功能更改：

  - 不能从 Exchange 管理工具创建邮箱、启用邮件的用户、通讯组和其他安全主体。

  - 不能从 Exchange 管理工具添加和删除通讯组成员。

  - 会删除向 Exchange 受信任子系统和 Exchange 服务器授予的所有用于创建安全主体的权限。

  - Exchange 服务器和 Exchange 管理工具只能修改 Exchange 中现有安全主体的 Active Directory 属性。

例如，若要创建启用 Active Directory 拆分权限的邮箱，必须首先由具有所需 Active Directory 权限的用户使用 Active Directory 工具来创建一个用户。然后，可以使用 Exchange 管理工具为该用户启用邮箱。Exchange 管理员使用 Exchange 管理工具只能修改与 Exchange 相关的邮箱属性。

如果满足以下条件，则 Active Directory 拆分权限对于您的组织是个不错的选择：

  - 您的组织要求仅使用 Active Directory 管理工具或仅由在 Active Directory 中授予了特定权限的用户来创建安全主体。

  - 您希望管理 Exchange 组织的人员完全不具备创建安全主体的能力。

  - 您希望使用 Active Directory 管理工具执行所有通讯组管理，包括创建通讯组以及添加和删除这些组的成员。

  - 您不希望 Exchange 服务器或代表其使用 Exchange 的第三方程序创建安全主体。

> [!IMPORTANT]  
> 通过使用安装向导，或通过在从命令行运行 <code>setup.exe</code> 时使用 <em>ActiveDirectorySplitPermissions</em> 参数，可以在安装 Exchange 2013 时选择切换为 Active Directory 拆分权限。也可以通过从命令行重新运行 <code>setup.exe</code>，在安装了 Active Directory 后启用或禁用 Exchange 2013 拆分权限。若要启用 Active Directory 拆分权限，请将 <em>ActiveDirectorySplitPermissions</em> 参数设置为 <code>true</code>。若要禁用该拆分权限，请将此参数设置为 <code>false</code>。您必须始终随 <em>ActiveDirectorySplitPermissions</em> 参数一起指定 <em>PrepareAD</em> 开关。<br />
> 如果同一林中有多个域，则还必须在应用 Active Directory 拆分权限时指定 <em>PrepareAllDomains</em> 开关，或在每个域中运行带有 <em>PrepareDomain</em> 开关的安装程序。如果选择在每个域中运行带有 <em>PrepareDomain</em> 开关的安装程序而非使用 <em>PrepareAllDomains</em> 开关，则必须准备每个包含以下项的域：Exchange 服务器、启用了邮件功能的对象，或者可由 Exchange 服务器访问的全局编录服务器。


> [!IMPORTANT]  
> 如果您已在域控制器上安装了 Exchange 2010 或 Exchange 2013，则不能启用 Active Directory 拆分权限。<br />
> 在您启用或禁用 Active Directory 拆分权限后，我们建议您重启组织中的 Exchange 2010 和 Exchange 2013 服务器，以强制这些服务器选取具有更新后权限的新 Active Directory 访问令牌。


Exchange 2013 通过删除 ExchangeWindows 权限安全组的权限和成员身份来实现 Active Directory 拆分权限。在共享权限 RBAC 拆分权限中，向此安全组授予了对整个 Active Directory 中的许多非 Exchange 对象和属性的权限。通过删除此安全组的权限和成员身份，可防止 Exchange 管理员和服务创建或修改这些非 Exchange Active Directory 对象。

有关在启用或禁用 Exchange 拆分权限时，对 Windows Exchange 权限安全组和其他 Active Directory 组件进行的更改的列表，请参阅下表。

> [!NOTE]  
> 在启用 Exchange 拆分权限时，删除了使 Active Directory 管理员可以创建安全主体的角色组角色分配。这样做是为了删除对某些 cmdlet 的访问权限，否则在运行这些 cmdlet 时会生成错误，因为它们无权创建关联 Active Directory 对象。


### Active Directory 拆分权限更改

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>Exchange 执行的更改</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在第一次安装 Exchange 2013 服务器的过程中启用 Active Directory 拆分权限</p></td>
<td><p>在您通过安装向导或通过运行带有 <code>/PrepareAD</code> 和 <code>/ActiveDirectorySplitPermissions:true</code> 参数的 <code>setup.exe</code> 来启用 Active Directory 拆分权限时，会发生以下情况：</p>
<ul>
<li><p>创建一个“Microsoft Exchange 保护组”组织单位 (OU)。</p></li>
<li><p>在“Microsoft Exchange 保护组”OU 中创建“Exchange Windows 权限”安全组。</p></li>
<li><p>不会将“Exchange 受信任子系统”安全组添加到“Exchange Windows 权限”安全组中。</p></li>
<li><p>不会创建对具有以下管理角色类型的管理角色的非委派管理角色分配：</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p>不会将本应已分配给“Exchange Windows 权限”安全组的访问控制条目 (ACE) 添加到 Active Directory 域对象中。</p></li>
</ul>
<p>如果您运行带有 <em>PrepareAllDomains</em> 或 <em>PrepareDomain</em> 开关的安装程序，则在所准备的每个子域中都会发生以下情况：</p>
<ul>
<li><p>从域对象中删除分配给“Exchange Windows 权限”安全组的所有 ACE。</p></li>
<li><p>在每个域中设置 ACE，但不包括分配给“Exchange Windows 权限”安全组的全部 ACE。</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>从共享权限或 RBAC 拆分权限切换为 Active Directory 拆分权限</p></td>
<td><p>在您运行带有 <code>/PrepareAD</code> 和 <code>/ActiveDirectorySplitPermissions:true</code> 参数的 <code>setup.exe</code> 命令时，会发生以下情况：</p>
<ul>
<li><p>创建一个“Microsoft Exchange 保护组”OU。</p></li>
<li><p>将“Exchange Windows 权限”安全组移到“Microsoft Exchange 保护组”OU 中。</p></li>
<li><p>从“Exchange Windows 权限”安全组中删除“Exchange 受信任子系统”安全组。</p></li>
<li><p>删除对具有以下角色类型的管理角色的任何非委派角色分配：</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p>从域对象中删除分配给“Exchange Windows 权限”安全组的所有 ACE。</p></li>
</ul>
<p>如果您运行带有 <em>PrepareAllDomains</em> 或 <em>PrepareDomain</em> 开关的安装程序，则在所准备的每个子域中都会发生以下情况：</p>
<ul>
<li><p>从域对象中删除分配给“Exchange Windows 权限”安全组的所有 ACE。</p></li>
<li><p>在每个域中设置 ACE，但不包括分配给“Exchange Windows 权限”安全组的全部 ACE。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>从 Active Directory 拆分权限切换为共享权限或 RBAC 拆分权限</p></td>
<td><p>在您运行带有 <code>/PrepareAD</code> 和 <code>/ActiveDirectorySplitPermissions:false</code> 参数的 <code>setup.exe</code> 命令时，会发生以下情况：</p>
<ul>
<li><p>将“Exchange Windows 权限”安全组移到“Microsoft Exchange 安全组”OU 中。</p></li>
<li><p>删除“Microsoft Exchange 保护组”OU。</p></li>
<li><p>将“Exchange 受信任子系统”安全组添加到“Exchange Windows 权限”安全组中。</p></li>
<li><p>将 ACE 添加到“Exchange Windows 权限”安全组的域对象中。</p></li>
</ul>
<p>如果您运行带有 <em>PrepareAllDomains</em> 或 <em>PrepareDomain</em> 开关的安装程序，则在所准备的每个子域中都会发生以下情况：</p>
<ul>
<li><p>将 ACE 添加到“Exchange Windows 权限”安全组的域对象中。</p></li>
<li><p>在每个域中设置 ACE，其中包括分配给“Exchange Windows 权限”安全组的 ACE。</p></li>
</ul>
<p>在从 Active Directory 拆分权限切换为共享权限时，不会自动创建对“邮件收件人创建”及“安全组创建和成员身份”角色的角色分配。如果委派角色分配在 Active Directory 拆分权限启用之前就已经自定义，那么这些自定义会保持不变。若要创建这些角色与 组织管理 角色组之间的角色分配，请参阅<a href="configure-exchange-2013-for-shared-permissions-exchange-2013-help.md">为 Exchange 2013 配置共享权限</a>。</p></td>
</tr>
</tbody>
</table>


在启用 Active Directory 拆分权限之后，以下 cmdlet 将不再可用：

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

在启用 Active Directory 拆分权限之后，可以访问以下 cmdlet，但是不能使用这些 cmdlet 创建通讯组或修改通讯组成员身份：

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Update-DistributionGroupMember**

在 Active Directory 拆分权限下使用时，某些 cmdlet 尽管仍然可用，但只能提供有限功能。这是因为使用这些 cmdlet 可以配置处于域 Active Directory 分区中的收件人对象和处于配置 Exchange 分区中的 Active Directory 配置对象。使用这些 cmdlet 还可以在存储于域分区中的对象上配置与 Exchange 相关的属性。如果尝试使用这些 cmdlet 在域分区中创建对象或修改对象上与 Exchange 无关的属性，则会导致错误。例如，如果您尝试向邮箱添加权限，则 **Add-ADPermission** cmdlet 会返回错误。然而，如果您在接收连接器上配置权限，则 **Add-ADPermission** cmdlet 会成功。这是因为邮箱存储在域分区中，而接收连接器存储在配置分区中。

此外，Exchange 管理中心和 Outlook Web App 中的相关功能（如新建邮箱向导）也将不再可用，如果您尝试使用这些功能，则会生成错误。

但是，Exchange 管理员将能够创建和管理特定于 Exchange 的对象，如传输规则等。

有关配置 Active Directory 拆分权限模型的详细信息，请参阅[为 Exchange 2013 配置拆分权限](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)。

返回顶部

