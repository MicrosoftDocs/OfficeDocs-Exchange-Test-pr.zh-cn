---
title: '管理边缘订阅: Exchange 2013 Help'
TOCTitle: 管理边缘订阅
ms:assetid: 27de4104-fb8e-4eab-9ad2-a64f81a4fb69
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996865(v=EXCHG.150)
ms:contentKeyID: 61183387
ms.date: 04/27/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理边缘订阅

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2018-04-16_

本主题详细介绍了各种边缘订阅管理任务。

**目录**

订阅边缘传输服务器

删除边缘订阅

重新订阅边缘传输服务器

添加或删除邮箱服务器

手动运行 EdgeSync

验证 EdgeSync 结果

## 在开始之前，您需要知道什么？

  - 完成每个过程的估计时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“EdgeSync”条目和“边缘传输服务器”部分。

  - 您需要将边缘服务器订阅到面向 Internet 的 Active Directory 站点。有关详细信息，请参阅[配置通过所订阅的边缘传输服务器的 Internet 邮件流](configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 订阅边缘传输服务器

您可以将一个或多个边缘传输服务器订阅到一个 Active Directory 站点。如果您在外围网络中部署其他边缘传输服务器，并且将它们订阅到已存在边缘订阅的同一个 Active Directory 站点，则会触发下列操作：

  - 在 Active Directory 中新建一个边缘订阅对象。

  - 为 Active Directory 站点中的每个邮箱服务器创建额外的 ESRA 帐户。在与新服务器同步期间，这些帐户会复制到 Active Directory 轻型目录服务 (AD LDS)，并供 EdgeSync 同步过程使用。

  - 新边缘订阅会添加到连接到 Internet 的自动发送连接器的源服务器列表中。已提交到该连接器进行处理的邮件会在已订阅的边缘传输服务器之间平衡负载。

  - 自动创建从边缘传输服务器到 Exchange 组织的入站发送连接器。

  - 开始向边缘传输服务器进行 EdgeSync 同步。

## 删除边缘订阅

有时，您可能想将边缘订阅从 Exchange 组织或 Exchange 组织和边缘传输服务器删除。如果您打算以后重新将边缘传输服务器订阅到 Exchange 组织，请勿将边缘订阅从边缘传输服务器删除。将边缘订阅从边缘传输服务器删除后，所有复制的数据也会从 AD LDS 删除。如果您有大量的收件人数据，则耗时可能很长。

若要完全删除边缘订阅，您需要在要删除的边缘传输服务器上和边缘传输服务器订阅到的 Active Directory 站点中的 Exchange 2013 邮箱服务器上运行此程序。

在您删除边缘订阅之后，从 AD LDS 进行的信息同步就停止了。存储在 AD LDS 中的所有帐户都将删除，边缘传输服务器也将从任意发送连接器的源服务器列表中删除。您将无法再使用依赖于 Active Directory 数据的边缘传输服务器功能。

1.  若要从边缘传输服务器删除边缘订阅，请使用以下语法。
    
        Remove-EdgeSubscription <EdgeTransportServerIdentity>
    
    例如，若要从名为 Edge01 的边缘传输服务器删除边缘订阅，请运行以下命令。
    
        Remove-EdgeSubscription Edge01

2.  若要从邮箱服务器删除边缘订阅，请使用以下语法。
    
        Remove-EdgeSubscription <MailboxServerIdentity>
    
    例如，若要从名为 Mailbox01 的邮箱服务器删除边缘订阅，请运行以下命令。
    
        Remove-EdgeSubscription Mailbox01

在以下情况下，您需要删除边缘订阅：

  - 您不再希望边缘传输服务器参与 EdgeSync 同步。您需要从边缘传输服务器和 Exchange 组织删除边缘订阅。

  - 正在取消配置边缘传输服务器。在此情景中，您只需将边缘订阅从 Exchange 组织中删除。如果您将边缘传输服务器角色从计算机卸载，那么 AD LDS 实例以及 AD LDS 中存储的所有 Active Directory 数据也将会删除。

  - 您希望更改边缘订阅的 Active Directory 站点关联。您只需将边缘订阅从 Exchange 组织中删除。将边缘订阅从 Exchange 组织中删除后，您可以将边缘传输服务器重新订阅到其他 Active Directory 站点。

如果您从 Exchange 组织删除边缘订阅：

  - 从 Active Directory 向 AD LDS 进行的信息同步停止。

  - ESRA 帐户从 Active Directory 和 AD LDS 中删除。

  - 边缘传输服务器会从所有发送连接器的 *SourceTransportServers* 属性中删除。

  - 从边缘传输服务器到 Exchange 组织的自动入站发送连接器会从 AD LDS 中删除。

如果您从边缘传输服务器删除边缘订阅：

  - 您无法再使用依赖于 Active Directory 数据的边缘传输服务器功能。

  - 复制的数据会从 AD LDS 中删除。

  - 创建边缘订阅时禁用的任务会重新启用，以便进行本地配置。

## 重新订阅边缘传输服务器

有时，您可能需要将边缘传输服务器重新订阅到 Active Directory 站点。在边缘订阅重新创建后，新的凭据会生成，您需要按照完整的边缘订阅过程执行操作。在以下情况下，您需要重新订阅边缘传输服务器：

  - 您在已订阅的 Active Directory 站点中添加了新的邮箱服务器，并且想让新的邮箱服务器参与 EdgeSync 同步。

  - 您在创建边缘订阅后应用了边缘传输服务器的许可证密钥。在边缘订阅创建后，边缘传输服务器的许可信息将会得到捕获。只有在边缘传输服务器上应用许可证密钥之后将其订阅到 Exchange 组织，已订阅的边缘服务器才会显示为已获许可。如果您在执行边缘订阅过程后在边缘传输服务器上应用许可证密钥，则 Exchange 组织中的许可信息不会更新，您需要重新订阅边缘传输服务器。

  - ESRA 凭据泄漏。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要重新订阅边缘传输服务器，请在边缘传输服务器上导出新边缘订阅文件，然后在邮箱服务器上导入 XML 文件。您需要将边缘传输服务器重新订阅到原来所订阅的同一个 Active Directory 站点。不必先删除原来的边缘订阅；重新订阅过程会覆盖现有的边缘订阅。</td>
    </tr>
    </tbody>
    </table>


## 添加或删除邮箱服务器

如果您将邮箱服务器添加到已经订阅边缘传输服务器的 Active Directory 站点，则新邮箱服务器不会自动参与 EdgeSync 同步。若要启用新部署的邮箱服务器，使其能够参与 EdgeSync 同步，您需要将每个边缘传输服务器重新订阅到 Active Directory 站点。

从已经订阅边缘传输服务器的 Active Directory 站点中删除邮箱服务器不会影响 EdgeSync 同步，除非所删除的邮箱服务器是该站点中的唯一邮箱服务器。如果您从已经订阅边缘传输服务器的 Active Directory 站点中删除所有邮箱服务器，则该站点所订阅的边缘传输服务器会遭到孤立。

## 手动运行 EdgeSync

如果您已对 Active Directory 中的配置或收件人进行了大量更改，并想立即同步这些更改，则不妨手动运行 EdgeSync。您可以运行完全同步，或仅同步在上次复制后做出的更改。

手动运行 EdgeSync 会重置 EdgeSync 同步计划。下一次自动同步取决于您运行手动同步的时间。

若要手动运行 EdgeSync，请使用以下语法。

    Start-EdgeSynchronization [-Server <MailboxServerIdentity>] [-TargetServer <EdgeTransportServerIdentity> [-ForceFullSync]

下面的示例介绍了在启动 EdgeSync 时可以选择的选项：

  - 从名为 Mailbox01 的 Exchange 2013 邮箱服务器启动同步。

  - 同步所有的边缘传输服务器。

  - 只同步在上次复制后做出的更改。

<!-- end list -->

    Start-EdgeSynchronization -Server Mailbox01

本示例介绍了在启动 EdgeSync 时可以选择的选项：

  - 从本地邮箱服务器启动同步。

  - 只同步名为 Edge03 的边缘传输服务器。

  - 完全同步所有的收件人和配置数据。

<!-- end list -->

    Start-EdgeSynchronization -TargetServer Edge03 -ForceFullSync

## 验证 EdgeSync 结果

可以使用 **Test-EdgeSynchronization** cmdlet 来验证边缘同步是否正在运行。此 cmdlet 报告已订阅的边缘传输服务器的同步状态。

通过此 cmdlet 的输出，您可以查看哪些对象尚未同步到边缘传输服务器。该任务比较存储在 Active Directory 中的数据与存储在 AD LDS 中的数据，并报告所有不一致的数据。

可以在 **Test-EdgeSynchronization** cmdlet 中使用 *ExcludeRecipientTest* 参数来排除对收件人数据同步的验证。如果您添加此参数，则只会对配置对象的同步进行验证。与只验证配置数据相比，验证收件人数据的耗时要更长。

## 验证单个收件人的 EdgeSync 结果

若要验证单个收件人的 EdgeSync 结果，请在已订阅的 Active Directory 站点中的邮箱服务器上使用以下语法。

    Test-EdgeSynchronization -VerifyRecipient <emailaddress>

本示例验证用户 kate@contoso.com 的 EdgeSync 结果。

    Test-EdgeSynchronization -VerifyRecipient kate@contoso.com

返回顶部

