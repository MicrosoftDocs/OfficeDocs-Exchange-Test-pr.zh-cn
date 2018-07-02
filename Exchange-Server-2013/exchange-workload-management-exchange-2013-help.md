---
title: 'Exchange 工作负载管理: Exchange 2013 Help'
TOCTitle: Exchange 工作负载管理
ms:assetid: 276740c4-bdb7-49f1-9470-ae6f2bfd65aa
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150503(v=EXCHG.150)
ms:contentKeyID: 50490225
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 工作负载管理

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2014-11-16_

Exchange 工作负载是一个 Exchange Server 功能、协议或服务，为管理 Exchange 系统资源而明确定义。每个 Exchange 工作负载都会占用系统资源（例如，CPU、邮箱数据库操作或 Active Directory 请求）以运行用户请求或后台工作。Exchange 工作负载的示例包括 Outlook Web App、Exchange ActiveSync、邮箱迁移和邮箱助理。

您通过控制单个用户消耗资源的方式来管理 Exchange 工作负载（有时称为 Exchange 2010 中的用户限制）。在 Exchange Server 2010 中控制单个用户消耗 Exchange 系统资源的方式是可能的，且这一功能已经为 Exchange Server 2013 进行了扩展。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>只能在 Microsoft 客户服务和支持的指导下，通过监视组织中系统资源在 Exchange 服务器上的运行状况来管理工作负载。</td>
</tr>
</tbody>
</table>


## 通过控制各个用户使用资源的方式来管理工作负载

Exchange 2013 中增强了限制功能。该增强功能可帮助确保各个用户过多的资源消耗不会对服务器性能或用户体验产生负面影响。

默认情况下，Exchange 2013 中的用户限制允许用户短时间内增加资源消耗，而不会遇到任何带宽缩减情况。另外，完全锁定资源使用量非常大的用户的情况不经常发生或从不发生。最好在对服务器产生显著影响之前进行限制，使进程延迟时间很短（将其视为“微延迟”），而不是完全阻止用户执行操作。

**功能重要事项**

下面是一些重要事项，描述了在 Exchange 2013 中 Exchange 控制各个用户如何使用资源的方式：

  - **突发补偿**   突发补偿让用户可以处理短时间内的资源消耗增加情况，不会遇到任何限制。

  - **补给率**   补给率通过使用资源预算系统管理用户的资源消耗。您可以设置补给用户资源预算的速率。例如，值 600,000（以毫秒为单位）表示用户预算的补给率是一小时内每使用十分钟补给一次。

  - **流量调整**   当某个用户的资源使用率在一段时间内达到配置的限制时，最好在对服务器产生显著影响之前，使该用户延迟很短时间。用户通常注意不到这些“微延迟”。此过程使 Exchange 2013 能够高效地调整流量，而不会影响用户的工作效率。流量调整对用户的影响小于提前锁定，并且显著减少锁定发生的机会。

  - **最大使用率**   在极少数情况下，用户可能会在较短的一段时间内消耗非常大量的资源。为预防起见，可能会临时阻止达到最大使用率阈值的用户使用资源。被临时阻止使用资源的用户在其使用预算得到补给后会立即取消阻止。

有关您可用于控制各个用户资源使用方式的 cmdlet 列表，请参阅本主题后面的“用于控制各个用户资源使用方式的 cmdlet”。

**Exchange 2013 限制功能和部署注意事项**

无论是执行 Exchange 2013 的全新安装还是将 Exchange 2013 安装到包含 Exchange 2010 计算机的共存环境中，都会使用新 Exchange 2013 限制功能对在运行 Exchange 2013 的计算机上拥有邮箱的所有用户进行限制。但是，当这些用户通过 Exchange 2010 客户端访问服务器来访问其邮箱时，仍会通过 Exchange 2010 限制功能来限制 Exchange 2010 邮箱。

在将 Exchange 2013 安装到共存环境中时，Exchange 2013 安装过程可能会尝试继承在 Exchange 2010 配置中设置的一些限制设置。但是，Exchange 2013 限制功能各不相同，以至于任何旧限制设置的影响通常不会影响限制在 Exchange 2013 中的工作方式。

**通过使用作用域管理限制策略**

与 Exchange 2010 类似，Exchange 2013 中存在单个默认限制策略。在 Exchange 2013 中，默认限制策略名为 **GlobalThrottlingPolicy**。此策略的作用域为 **Global**。其他可用的用户限制作用域为 **Organization** 和 **Regular**。由于为 Exchange 2013 用户限制策略引入了作用域分配，因此限制策略的管理不同于 Exchange 2010。**GlobalThrottlingPolicy** 为组织中每个新的和现有的用户定义默认的基线限制设置，除非您已为组织自定义限制策略。在许多典型的 Exchange 部署方案中，**GlobalThrottlingPolicy** 足以管理您的用户。

强烈建议您不要通过修改 **GlobalThrottlingPolicy** 来自定义限制设置。您应该创建其他限制策略。通过创建其他限制策略可帮助您更好地管理工作负载。还可阻止对限制策略设置进行的任何修改被将来的 Exchange 2013 更新所覆盖。

要自定义应用于组织中所有用户的限制设置，请创建一个作用域分配为 **Organization** 的新限制策略。在新的组织作用域策略中，您只应设置不同于 **GlobalThrottlingPolicy** 中的限制设置的设置。要自定义仅应用于组织中特定用户的限制设置，请创建一个作用域分配为 **Regular** 的新限制策略。在新的常规作用域策略中，您只应设置不同于 **GlobalThrottlingPolicy** 及任何其他组织策略中的限制设置的设置。这有助于您继承 **GlobalThrottlingPolicy** 中的其余策略设置，并让您受益于将来 Exchange 更新中添加的任何限制策略更新。

## 管理工作负载限制设置

通过使用 Exchange 命令行管理程序管理 Exchange 工作负载限制设置。

**用于控制各个用户资源使用方式的 cmdlet**

使用 Exchange 2010 中引入的以下 cmdlet 管理限制设置：

管理限制策略

  - [Get-ThrottlingPolicy](https://technet.microsoft.com/zh-cn/library/dd351264\(v=exchg.150\))

  - [New-ThrottlingPolicy](https://technet.microsoft.com/zh-cn/library/dd351045\(v=exchg.150\))

  - [Remove-ThrottlingPolicy](https://technet.microsoft.com/zh-cn/library/dd351178\(v=exchg.150\))

  - [Set-ThrottlingPolicy](https://technet.microsoft.com/zh-cn/library/dd298094\(v=exchg.150\))

分配限制策略

  - [Get-ThrottlingPolicyAssociation](https://technet.microsoft.com/zh-cn/library/ff459241\(v=exchg.150\))

  - [Set-ThrottlingPolicyAssociation](https://technet.microsoft.com/zh-cn/library/ff459231\(v=exchg.150\))

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>已弃用 <strong>*-ResourcePolicy</strong>、<strong>*-WorkloadManagementPolicy</strong> 和 <strong>*-WorkloadPolicy</strong> 系统工作负载管理 cmdlet。应仅在 Microsoft 客户服务和支持的指导下，对系统工作负载管理设置进行自定义。</td>
</tr>
</tbody>
</table>

