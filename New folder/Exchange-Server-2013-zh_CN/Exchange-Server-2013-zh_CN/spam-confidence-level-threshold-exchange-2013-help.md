---
title: '垃圾邮件可信度阈值: Exchange 2013 Help'
TOCTitle: 垃圾邮件可信度阈值
ms:assetid: 0009b4af-be6d-41d2-98bc-b5487272c74a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa995744(v=EXCHG.150)
ms:contentKeyID: 50489811
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 垃圾邮件可信度阈值

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-11-17_

> [!NOTE]
> 2016 年 11 月 1 日起，Microsoft 停止为 Exchange 和 Outlook 中的 SmartScreen 筛选器生成垃圾邮件定义更新。现有的 SmartScreen 垃圾邮件定义将予以保留，但其效力可能会随时间的推移而逐渐降低。有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=835894">停止为 Outlook 和 Exchange 中的 SmartScreen 提供支持</a>。


在 Microsoft Exchange Server 2013 中，可以根据垃圾邮件可信度 (SCL) 阈值定义特定操作。例如，可以为在运行内容筛选器代理的 Exchange 服务器上拒绝、删除或隔离邮件定义不同的阈值。

内容筛选器代理中的这种 SCL 阈值配置与用户邮箱中的 SCL 垃圾邮件文件夹配置的组合，将帮助您实现更全面和精确的反垃圾邮件策略。Exchange 2013 中的这种更精确、更详细的 SCL 阈值调整功能可以帮助您降低在整个 Exchange 组织中部署和维护反垃圾邮件解决方案的总成本。

内容筛选器代理会在反垃圾邮件周期的后期向邮件分配 SCL 分级（在其他反垃圾邮件代理处理任何入站邮件之后）。在内容筛选器代理处理入站邮件之前，其他很多反垃圾邮件代理处理这些邮件的方式是确定的。例如，在边缘传输服务器上，连接筛选器代理将拒绝从实时阻止列表中的 IP 地址发送的任何邮件。发件人筛选器代理和收件人筛选代理则以类似确定的方式处理邮件。

在 Exchange 2013 中，这些使用确定处理方式的反垃圾邮件代理将首先处理邮件，因此会极大地减少内容筛选器代理必须处理的邮件数。有关反垃圾邮件代理处理邮件的顺序的详细信息，请参阅[反垃圾邮件保护](anti-spam-protection-exchange-2013-help.md)。

由于内容筛选不是准确、明确的过程，因此，调整内容筛选器代理对不同 SCL 值所执行操作的能力是很重要的。通过认真调整 SCL 阈值配置，可使以下各项最小化：

  - 垃圾邮件隔离存储的大小

  - 被错误隔离的合法电子邮件数

  - 到达 Microsoft Outlook 用户的\&quot;垃圾邮件\&quot;文件夹的合法电子邮件数

  - 到达 Outlook 用户的\&quot;收件箱\&quot;或\&quot;垃圾邮件\&quot;文件夹的攻击性垃圾邮件数

  - 到达 Outlook 用户的\&quot;收件箱\&quot;的垃圾邮件数

## SCL 阈值操作

通过调整 SCL 阈值操作，可以对成为垃圾邮件风险较高的邮件所执行的内容筛选操作逐渐进行升级。若要理解该项新功能，理解不同的 SCL 阈值操作及其实现方式将是很有帮助的：

  - **SCL 删除阈值**   特定邮件的 SCL 值等于或大于 SCL 删除阈值时，内容筛选器代理将删除该邮件。没有协议级别的通信告诉发送系统或发件人该邮件已删除。如果邮件的 SCL 值小于 SCL 删除阈值，内容筛选器代理将不删除该邮件。而是内容筛选器代理会将 SCL 值与 SCL 拒绝阈值进行比较。

  - **SCL 拒绝阈值**   特定邮件的 SCL 值等于或大于 SCL 拒绝阈值时，内容筛选器代理将删除该邮件，并向发送系统发送拒绝响应。可以自定义拒绝响应。某些情况下，未送达报告 (NDR) 将发送给邮件的原始发件人。如果邮件的 SCL 值小于 SCL 删除阈值和 SCL 拒绝阈值，内容筛选器代理将不删除或拒绝该邮件。而是内容筛选器代理将 SCL 值与 SCL 隔离阈值进行比较。

  - **SCL 隔离阈值**   特定邮件的 SCL 值等于或大于 SCL 隔离阈值时，内容筛选器代理会将该邮件发送到隔离邮箱。电子邮件管理员必须定期检查隔离邮箱。如果邮件的 SCL 值小于 SCL 删除、拒绝和隔离阈值，内容筛选器代理将不删除、拒绝或隔离该邮件。而是由内容筛选器代理将邮件发送到适当的邮箱服务器，在那里计算该邮件的每个收件人的 SCL 垃圾邮件文件夹阈值。

  - **SCL 垃圾邮件文件夹阈值**   如果特定邮件的 SCL 值超过 SCL 垃圾邮件文件夹阈值，则该邮件会传递到用户的\&quot;垃圾邮件\&quot;文件夹。如果邮件的 SCL 值小于 SCL 删除、拒绝、隔离和垃圾邮件文件夹阈值，则该邮件会传递到用户的\&quot;收件箱\&quot;。

内容筛选器代理和\&quot;垃圾邮件\&quot;文件夹以不同的方式处理 SCL 阈值。内容筛选器代理对您配置的 SCL 阈值执行操作。\&quot;垃圾邮件\&quot;文件夹对您配置的 SCL 阈值加 1 执行操作。例如，如果您在内容筛选器代理上对 SCL 8 配置删除操作，则 SCL 不低于 8 的所有邮件都将遭到删除。不过，如果您为\&quot;垃圾邮件\&quot;文件夹配置 SCL 阈值 4，则 SCL 不低于 5 的所有邮件都将移动至\&quot;垃圾邮件\&quot;文件夹。

例如，如果将 SCL 删除阈值设置为 8，将 SCL 拒绝阈值设置为 7，将 SCL 隔离阈值设置为 6，并将 SCL 垃圾邮件文件夹阈值设置为 4，那么，SCL 小于或等于 5 的所有邮件都将传递到用户的邮箱。SCL 值为 5 的邮件会放置在用户的\&quot;垃圾邮件\&quot;文件夹中。SCL 小于或等于 4 的邮件会放置在用户的\&quot;收件箱\&quot;中。

可以在以下位置配置 SCL 删除、拒绝、隔离和\&quot;垃圾邮件\&quot;文件夹设置：

  - **在内容筛选器代理配置（每个传输服务器 SCL 配置）上**   使用 **Set-ContentFilterConfig** cmdlet 在运行内容筛选器代理的 Exchange 服务器上启用或禁用及设置 SCL 删除、拒绝和隔离阈值。一定时间后，在分析反垃圾邮件日志和报告功能所提供的垃圾邮件功能和度量值时，可以根据需要对这些 SCL 阈值配置进行其他调整。
    
    下表中介绍了可对 **Set-ContentFilterConfig** cmdlet 使用的 SCL 参数。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>参数</th>
    <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLDeleteEnabled</em></p></td>
    <td><p>此参数启用或禁用以下操作：在邮件的 SCL 值大于或等于 <em>SCLDeleteThreshold</em> 参数指定的值时删除邮件而不生成未送达报告 (NDR)。此参数的有效输入值为 <code>$true</code> 或 <code>$false</code>。</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLDeleteThreshold</em></p></td>
    <td><p>此参数的有效输入是从 0 到 9（含）的整数。此参数的值应大于或等于其他 SCL 阈值参数。此参数只在 <em>SCLDeleteEnabled</em> 参数的值是 <code>$true</code> 时才起作用。</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLRejectEnabled</em></p></td>
    <td><p>此参数启用或禁用以下操作：在邮件的 SCL 值大于或等于 <em>SCLRejectThreshold</em> 参数指定的值时使用 NDR 拒绝邮件。此参数的有效输入值为 <code>$true</code> 或 <code>$false</code>。</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLRejectThreshold</em></p></td>
    <td><p>此参数的有效输入是从 0 到 9（含）的整数。此参数的值应小于 <em>SCLDeleteThreshold</em> 参数，但是应大于其他 SCL 阈值参数。仅当 <em>SCLRejectEnabled</em> 参数的值为 <code>$true</code> 时，此参数才有意义。</p></td>
    </tr>
    <tr class="odd">
    <td><p><em>SCLQuarantineEnabled</em></p></td>
    <td><p>此参数启用或禁用以下操作：在邮件的 SCL 值大于或等于 <em>SCLQuarantineThreshold</em> 参数指定的值时将邮件发送到垃圾邮件隔离邮箱。此参数的有效输入值为 <code>$true</code> 或 <code>$false</code>。</p>
    <p>有关垃圾邮件隔离邮箱的详细信息，请参阅<a href="spam-quarantine-exchange-2013-help.md">垃圾邮件隔离</a>。</p></td>
    </tr>
    <tr class="even">
    <td><p><em>SCLQuarantineThreshold</em></p></td>
    <td><p>此参数的有效输入是从 0 到 9（含）的整数。此参数的值应小于 <em>SCLRejectThreshold</em> 参数，但是应大于 <strong>Set-OrganizationConfig</strong> 或 <strong>Set-Mailbox</strong> cmdlet 的 <em>SCLJunkThreshold</em> 参数。此参数只在 <em>SCLQuarantineThreshold</em> 参数的值是 <code>$true</code> 时才起作用。</p></td>
    </tr>
    </tbody>
    </table>


  - **在组织配置设置（组织范围 SCL 配置）上**   使用 **Set-OrganizationConfig** cmdlet 为组织中的所有邮箱设置 SCL 垃圾邮件文件夹阈值。
    
    下表中介绍了对 **Set-OrganizationConfig** cmdlet 可用的 SCL 参数。有关使用 SCLJunkThreshold 的示例，请参阅[在邮箱上配置反垃圾邮件设置](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md)。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>参数</th>
    <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkThreshold</em></p></td>
    <td><p>此参数指定将邮件移动到收件人邮箱的&amp;quot;垃圾邮件&amp;quot;文件夹时邮件必须超过的 SCL 值。此参数的有效输入是从 0 到 9（含）的整数。此参数的值应小于或等于其他 SCL 阈值参数。例如，如果指定值 4，则会将 SCL 值大于或等于 5 的邮件移动到用户的&amp;quot;垃圾邮件&amp;quot;文件夹中。</p></td>
    </tr>
    </tbody>
    </table>


  - **在用户邮箱（每个收件人 SCL 配置）上**   使用 **Set-Mailbox** cmdlet 在单个邮箱上启用或禁用及设置每个收件人的 SCL 删除、拒绝、隔离和\&quot;垃圾邮件\&quot;文件夹阈值。只能使用 **Set-Mailbox** cmdlet 在单个邮箱上启用或禁用 SCL 垃圾邮件文件夹阈值。每个收件人的 SCL 删除、拒绝和隔离阈值将存储在 Active Directory 中，并由 Microsoft Exchange EdgeSync 服务复制到订阅的边缘传输服务器。即使已经设置每个传输服务器的 SCL 配置，内容筛选器代理仍将使用每个收件人的 SCL 阈值配置。因此，如果已经设置每个收件人的 SCL 阈值，则内容筛选器代理将对特定用户使用每个收件人的 SCL 阈值，而不是内容筛选器代理上的 SCL 配置。有关示例，请参阅[在邮箱上配置反垃圾邮件设置](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md)。
    
    > [!NOTE]
    > 不会对通过通讯组接收的邮件强制执行每个收件人的 SCL 阈值。
    
    对 **Set-Mailbox** cmdlet 可用的 SCL 参数与对 **Set-ContentFilterConfig** 和 **Set-OrganizationConfig** cmdlet 可用的参数相同：
    
      - *SCLDeleteEnabled*
    
      - *SCLDeleteThreshold*
    
      - *SCLRejectEnabled*
    
      - *SCLRejectThreshold*
    
      - *SCLQuarantineEnabled*
    
      - *SCLQuarantineThreshold*
    
      - *SCLJunkThreshold*
    
    但是，**Set-Mailbox** cmdlet 上的所有 SCL 参数也可接受值 `$null`。如果某个邮箱的 SCL 设置为空 (`$null`)，则会将对应的内容筛选器代理设置或组织配置设置应用于该邮箱。如果某个邮箱的 SCL 设置的值为 `$true` 或 `$false`，则邮箱的设置会覆盖内容筛选器代理或组织配置上的对应组织范围设置。
    
    下表中介绍了只能对 **Set-Mailbox** cmdlet 可用的 SCL 参数。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>参数</th>
    <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><em>SCLJunkEnabled</em></p></td>
    <td><p>此参数启用或禁用以下操作：在邮件的 SCL 值大于 <em>SCLQuarantineThreshold</em> 参数指定的值时将邮件传递到用户的&amp;quot;垃圾邮件&amp;quot;文件夹。此参数的有效输入为 <code>$true</code>、<code>$false</code> 或 <code>$null</code>。</p>
    <p>请注意，默认情况下会针对组织中的所有用户邮箱启用垃圾邮件筛选功能。默认情况下，对于所有用户邮箱，<em>Enabled</em> 参数都会在 <strong>Set-MailboxJunkEmailConfiguration</strong> cmdlet 上设置为值 <code>$true</code>。</p></td>
    </tr>
    </tbody>
    </table>
    
    有关对邮箱配置 SCL 阈值的详细信息，请参阅[在邮箱上配置反垃圾邮件设置](configure-anti-spam-settings-on-mailboxes-exchange-2013-help.md)。

## 监视 SCL 阈值

可以使用位于 `%ExchangeInstallPath%Scripts` 文件夹中的几个内置脚本（如 **get-AntispamSCLHistogram.ps1**）来收集筛选结果数据。如果数据显示您需要立即进行调整，请重新配置 SCL 阈值。否则，应收集数据并分析垃圾邮件报告，以确定是否需要进行调整。

