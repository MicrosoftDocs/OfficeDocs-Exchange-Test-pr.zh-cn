---
title: 'Active Directory 的访问权限: Exchange 2013 Help'
TOCTitle: Active Directory 的访问权限
ms:assetid: 61080b45-8bce-4c23-b744-ed264d5f0b7d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998561(v=EXCHG.150)
ms:contentKeyID: 50490674
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory 的访问权限

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

Microsoft Exchange Server 2013 将所有配置和收件人信息存储在 Active Directory 目录服务数据库中。如果运行 Exchange 2013 的计算机需要有关收件人的信息以及 Exchange 组织的配置信息，则其必须查询 Active Directory 才能访问所需信息。要使 Active Directory 正确运行，必须有可用的 Exchange 2013 服务器。

本主题说明了 Exchange 2013 如何在 Active Directory 中存储和检索信息，以便您可以规划对 Active Directory 的访问。另外，本主题还讨论了当尝试恢复已删除的 Exchange 2013Active Directory 对象时应当注意的问题。

## 存储在 Active Directory 中的 Exchange 信息

Active Directory 数据库将信息存储在下面几节描述的三种类型的逻辑分区中：

  - 架构分区

  - 配置分区

  - 域分区

## 架构分区

架构分区存储以下两种类型的信息：

  - **架构类**定义可在 Active Directory 中创建和存储的对象的所有类型。

  - **架构属性**定义可用于描述存储在 Active Directory 中的对象的所有属性。

在林中安装第一个 Exchange 2013 服务器角色或运行 Active Directory 准备过程时，Active Directory 准备过程会将多个类和属性添加到 Active Directory 架构中。添加到架构中的类用于创建特定于 Exchange 的对象，比如代理和连接器。添加到架构中的属性用于配置特定于 Exchange 的对象和已启用邮件的用户和组。这些属性包括诸如 MicrosoftOffice Outlook Web Access 设置和 MicrosoftExchange 统一消息 (UM) 设置这样的属性。林中的每个域控制器和全局编录服务器都包含架构分区的完整副本。

有关 Exchange 2013 中的架构修改的详细信息，请参阅 [Exchange 2013 Active Directory 架构更改](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)。

## 配置分区

配置分区存储有关林范围内的配置信息。此配置信息包括 Active Directory 站点的配置、Exchange 全局设置、传输设置和邮箱策略。每种类型的配置信息都存储在配置分区的容器中。Exchange 的配置信息存储在配置分区的服务容器下面的子文件夹中。存储在此容器中的信息包含以下内容：

  - 地址列表

  - 通讯簿邮箱策略

  - 管理组

  - 客户端访问设置

  - 连接

  - 移动邮箱设置

  - 全局设置

  - 监视设置

  - 系统策略

  - 保留策略容器

  - 传输设置

林中的每个域控制器和全局编录服务器都包含配置分区的完整副本。

## 域分区

域分区将信息存储在默认容器以及由 Active Directory 管理员创建的组织单位中。这些容器包含特定于域的对象。这些数据包括 Exchange 系统对象以及有关域中的计算机、用户和组的信息。安装 Exchange 2013 后，Exchange 将更新此分区中的对象，以支持 Exchange 功能。此功能会影响收件人信息的存储和访问方式。

每个域控制器都包含有其已获授权的域的域分区完整副本。林中的每个全局编录服务器都包含林中每个域分区中的信息子集。

## Exchange 2013 如何访问 Active Directory 中的信息

Exchange 2013 利用 Active Directory API 来访问存储在 Active Directory 中的信息。Microsoft ExchangeActive Directory 拓扑服务可针对所有 Exchange 2013 服务器角色运行。此服务将从所有 Active Directory 分区中读取信息。检索到的数据将被缓存并由 Exchange 2013 服务器用于发现组织中所有 Active Directory 服务的 Exchange 站点位置。

有关拓扑和服务发现的详细信息，请参阅[规划使用 Active Directory 站点路由邮件](planning-to-use-active-directory-sites-for-routing-mail-exchange-2013-help.md)。

Exchange 2013 是一种具有 Active Directory 站点感知功能的应用程序，它会优先与位于 Exchange 服务器所在相同站点中的目录服务器进行通信，以优化网络通信。每个 Exchange 2013 组织服务器角色必须与 Active Directory 进行通信以检索有关收件人的信息以及有关其他 Exchange 2013 服务器角色的信息。下面几节将说明每个服务器角色获取的数据。

默认情况下，只要 Exchange 2013 服务器启动，它就会绑定到其所属站点中随机选择的域控制器和全局编录服务器。通过使用 Exchange 命令行管理程序中的 **Get-ExchangeServer** cmdlet 可以查看所选目录服务器。您还可以使用 **Set-ExchangeServer** cmdlet 来配置 Exchange 2013 服务器应绑定到的域控制器的静态列表或者应被排除的域控制器的列表。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>可以将 Windows Server 2008 域控制器配置为只读目录服务器。如果希望在远程站点中部署域控制器或全局编录服务器来进行身份验证和授权，但又不希望允许该站点的管理员将更改写入 Active Directory，此项配置将十分有用。但是，不能在仅包含只读目录服务器的任何站点中部署 Exchange 2013 服务器。</td>
</tr>
</tbody>
</table>


## 邮箱服务器角色

邮箱服务器角色将有关邮箱用户和存储的配置信息存储在 Active Directory 中。此外，对于 Exchange 2013，邮箱服务器包含可在 Exchange 2010 中找到的所有传统服务器组件：客户端访问协议、传输服务、邮箱数据库和统一消息。邮箱服务器处理该服务器上活动邮箱的所有活动。

## 客户端访问服务器角色

在 Exchange 2013 中，客户端访问服务器将提供身份验证、有限重定向和代理服务。客户端访问服务器本身不进行任何数据呈现。客户端访问服务器是无状态瘦服务器。客户端访问服务器上从不会排队或存储任何内容。客户端访问服务器提供所有常用的客户端访问协议：HTTP、POP 和 IMAP 和 SMTP。

## 恢复已删除的 Exchange 对象

Active Directory 回收站可在不从备份还原 Active Directory 数据、不重新启动 Active Directory 域服务 (AD DS) 或域控制器的情况下，增强保留和恢复意外删除的 Active Directory 对象的能力，从而有效减少目录服务的停机时间。

对于恢复已删除的与 Exchange 相关的 Active Directory 对象，最需要了解的一点是 Exchange 对象不是孤立存在的。例如，对用户启用邮件时，将根据您当前的 Exchange 配置为此用户计算多个不同的策略和链接。还原已删除的 Exchange 配置或收件人对象时，可能会出现两个问题：

  - **冲突**   某些 Exchange 属性必须在林中唯一。例如，两个不同用户的代理（电子邮件）地址不能相同。Active Directory 不强制要求代理地址的唯一性，但 Exchange 管理工具会检查唯一性。另外，Exchange 电子邮件地址策略还会根据确定的规则自动解决代理地址分配中可能存在的冲突。因此，可以还原 Exchange 用户对象，并从而创建代理地址或其他应唯一的属性的冲突。

  - **错误配置**   Exchange 具有可分配各种策略或设置的自动规则。如果删除了收件人，然后更改了规则或策略，则还原 Exchange 用户对象可能会导致用户被分配到错误的策略（或者甚至不复存在的策略）。

以下准则可最大限度地减少恢复已删除的与 Exchange 相关的对象时遇到的困难或问题：

  - 如果您使用 Exchange 管理工具删除了某个 Exchange 配置对象，则不要还原该对象。请使用 Exchange 管理工具（Exchange 管理中心或 Exchange 命令行管理程序）重新创建该对象。

  - 如果不是使用 Exchange 管理工具删除了 Exchange 配置对象，请尽快将其恢复。删除后在系统中所做的管理和配置更改越多，还原对象所造成错误配置的可能性就越大。

  - 如果您恢复了已删除的 Exchange 收件人（联系人、用户或通讯组），请密切监视是否存在与已恢复的对象相关的冲突和错误。如果在删除后可能已修改 Exchange 策略或其他与收件人相关的配置，请将当前策略重新应用到已还原的收件人，以确保正确配置这些收件人。

## 详细信息

[Active Directory 回收站分步指南](https://go.microsoft.com/fwlink/p/?linkid=178720)

[Active Directory 管理中心增强功能简介（级别 100）](https://go.microsoft.com/fwlink/p/?linkid=267641)

[使用 Active Directory 管理中心进行高级 AD DS 管理（级别 200）](https://go.microsoft.com/fwlink/p/?linkid=267642)

