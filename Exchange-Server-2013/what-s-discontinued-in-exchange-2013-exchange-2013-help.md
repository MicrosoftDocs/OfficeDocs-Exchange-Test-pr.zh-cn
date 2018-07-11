---
title: 'Exchange 2013 中的削减内容: Exchange 2013 Help'
TOCTitle: Exchange 2013 中的削减内容
ms:assetid: 0ac0001c-b314-4108-b895-d9c0e271b489
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ619283(v=EXCHG.150)
ms:contentKeyID: 50489962
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 中的削减内容

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

本主题讨论 Microsoft Exchange Server 2013 中已被删除、废弃或替换的组件或功能。

> [!NOTE]  
> 以下主题也可能会引起您的兴趣：
> <ul>
> <li><p><a href="what-s-new-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的新增功能</a>   有关 Exchange Server 2013 中的新特性和功能的信息。</p></li>
> <li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=267479">Exchange 2013 开发人员路线图</a>    有关 Exchange 2013 中废弃的 API 和开发功能的信息，请参阅“从 Exchange 中移除的开发技术”一节。</p></li>
> </ul>


## 从 Exchange 2010 到 Exchange 2013 的废弃功能

此节列出了在 Exchange 2013 中不再提供的 Exchange Server 2010 功能。

## 体系结构


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>集线器传输服务器角色</p></td>
<td><p>集线器传输服务器角色由在邮箱和客户端访问服务器角色上运行的传输服务代替。邮箱服务器角色包含 Microsoft Exchange 传输、Microsoft Exchange 邮箱传输传递和 Microsoft Exchange 邮箱传输提交服务。客户端访问服务器角色包含 Microsoft Exchange 前端传输服务。有关详细信息，请参阅<a href="mail-flow-exchange-2013-help.md">邮件流</a>。</p></td>
</tr>
<tr class="even">
<td><p>统一消息服务器角色</p></td>
<td><p>统一消息服务器角色被在邮箱和客户端访问服务器角色上运行的统一消息服务代替。邮箱服务器角色包含 Microsoft Exchange 统一消息服务，客户端访问服务器角色包含 Microsoft Exchange 统一消息呼叫路由器服务。有关详细信息，请参阅<a href="voice-architecture-changes-exchange-2013-help.md">语音体系结构更改</a>。</p></td>
</tr>
</tbody>
</table>


## 管理界面


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 管理控制台和 Exchange 控制面板</p></td>
<td><p>Exchange 管理控制台和 Exchange 控制面板已由 Exchange 管理中心 (EAC) 所替代。EAC 使用相同的虚拟目录 (/ecp) 作为 Exchange 控制面板。有关详细信息，请参阅 <a href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的 Exchange 管理中心</a>。</p></td>
</tr>
</tbody>
</table>


## 客户端访问


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>不支持 Outlook 2003</p></td>
<td><p>若要将 Microsoft Outlook 连接到 Exchange 2013，需要使用自动发现服务。但是，Microsoft Outlook 2003 不支持使用自动发现服务。</p></td>
</tr>
<tr class="even">
<td><p>对 Outlook 客户端的 RPC/TCP 访问</p></td>
<td><p>在 Exchange 2013 中，Microsoft Outlook 客户端可以使用 Exchange 2013 Service Pack 1 和 Outlook 2013 Service Pack 1 及更高版本中的 Outlook 无处不在 (RPC/HTTP) 或 MAPI over HTTP 进行连接。如果您的组织中有 Outlook 客户端，则需要使用 Outlook 无处不在 和/或 MAPI over HTTP。有关详细信息，请参阅 <a href="outlook-anywhere-exchange-2013-help.md">Outlook 无处不在</a> 和 <a href="mapi-over-http-exchange-2013-help.md">MAPI over HTTP</a>。</p></td>
</tr>
</tbody>
</table>


## Outlook Web App 和 Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解方式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>拼写检查</p></td>
<td><p>Outlook Web App 不再具有内置拼写检查服务。而是使用 Web 浏览器中的拼写检查功能。</p></td>
</tr>
<tr class="even">
<td><p>可自定义的筛选器</p></td>
<td><p>Outlook Web App 不再具有可自定义的筛选视图，也不再支持将筛选视图保存到收藏夹。可自定义的筛选器已替换为固定筛选器，可用于查看所有邮件、未读邮件、发送到用户的邮件，或带标记邮件。</p></td>
</tr>
<tr class="odd">
<td><p>邮件标志</p></td>
<td><p>在邮件标记中设置自定义日期的功能在 Outlook Web App 中不可用。您可以使用 Outlook 设置自定义日期。</p></td>
</tr>
<tr class="even">
<td><p>聊天联系人列表</p>
<p></p></td>
<td><p>显示在适用于 Exchange 2010 的 Outlook Web App 中的文件夹列表中的聊天联系人列表不再可用。</p></td>
</tr>
<tr class="odd">
<td><p>搜索文件夹</p></td>
<td><p>当前 Outlook Web App 中不提供让用户使用搜索文件夹的功能。</p></td>
</tr>
</tbody>
</table>


## 邮件流


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>链接连接器</p></td>
<td><p>无法将发送连接器链接到接收连接器。具体而言，从 <a href="https://technet.microsoft.com/zh-cn/library/aa998936(v=exchg.150)">New-SendConnector</a> 和 <a href="https://technet.microsoft.com/zh-cn/library/aa998294(v=exchg.150)">Set-SendConnector</a> 中删除了 <em>LinkedReceiveConnector</em> 参数。</p></td>
</tr>
</tbody>
</table>


## 反垃圾邮件和反恶意软件


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EMC 中的反垃圾邮件代理管理</p></td>
<td><p>在 Exchange 2010 中，当在集线器传输服务器上启用了反垃圾邮件代理时，可以在 Exchange 管理控制台 (EMC) 中管理反垃圾邮件代理。在 Exchange 2013 中，当在邮箱服务器中启用了反垃圾邮件代理时，则无法使用 EAC 管理这些代理。您只能使用命令行管理程序。有关如何在邮箱服务器上启用反垃圾邮件代理的信息，请参阅<a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">在邮箱服务器上启用反垃圾邮件功能</a>。</p></td>
</tr>
<tr class="even">
<td><p>集线器传输服务器上的连接筛选代理</p></td>
<td><p>在 Exchange 2010 中，当在集线器传输服务器上启用了反垃圾邮件代理时，附件筛选器代理是唯一不可用的反垃圾邮件代理。在 Exchange 2013 中，当在邮箱服务器中启用反垃圾邮件代理时，附件筛选器代理和连接筛选代理都不可用。连接筛选代理提供 IP 允许列表和 IP 阻止列表功能。有关如何在邮箱服务器上启用反垃圾邮件代理的信息，请参阅<a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">在邮箱服务器上启用反垃圾邮件功能</a>。</p>

> [!NOTE]  
> 无法在 Exchange 2013 客户端访问服务器上启用反垃圾邮件代理。因此，获得连接筛选代理的唯一方式是在外围网络中安装边缘传输服务器。有关详细信息，请参阅<a href="edge-transport-servers-exchange-2013-help.md">边缘传输服务器</a>。

</td>
</tr>
</tbody>
</table>


## 邮件策略和遵从性


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>托管文件夹</p></td>
<td><p>在 Exchange 2010 中，使用托管文件夹进行邮件保留管理 (MRM)。在 Exchange 2013 中，不支持托管文件夹。您必须使用 MRM 的保留策略。</p>

> [!NOTE]  
> 与托管文件夹相关的 Cmdlet 仍然可用。您可以创建托管文件夹、托管内容设置和托管文件夹邮箱策略，并且将托管文件夹邮箱策略应用于用户，但是，MRM 助手将跳过对已应用托管文件夹邮箱策略的邮箱的处理。

</td>
</tr>
<tr class="even">
<td><p>端口托管文件夹向导</p></td>
<td><p>在 Exchange 2010 中，使用端口托管文件夹向导基于托管文件夹和托管内容设置创建保留标记。在 Exchange 2013 中，Exchange 管理中心不包含此功能。可以使用带 <em>ManagedFolderToUpgrade</em> 参数的 <strong>New-RetentionPolicyTag</strong> cmdlet，基于托管文件夹创建保留标记。</p></td>
</tr>
</tbody>
</table>


## 统一消息和语音邮件


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用自动语音识别 (ASR) 进行 Directory 查找</p></td>
<td><p>在 Exchange 2010 中，Outlook Voice Access 用户可以通过自动语音识别 (ASR)，使用语音输入来搜索在目录中列出的用户。在 Outlook Voice Access 中，也可以使用语音输入来导航菜单、邮件和其他选项。但是，即使 Outlook Voice Access 用户可以使用语音输入，他们仍必须使用电话软键盘来输入 PIN 并导航个人选项。</p>
<p>在 Exchange 2013 中，经过身份验证和未经过身份验证的 Outlook Voice Access 用户无法使用任何语言的语音输入或 ASR 来搜索目录中的用户。但是，向自动助理发出呼叫的呼叫者可以使用多种语言的语音输入来导航自动助理菜单并搜索目录中的用户。</p></td>
</tr>
</tbody>
</table>


## 工具


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 最佳做法分析器</p></td>
<td><p>在 Exchange 2010 中，Exchange 最佳做法分析器会检查 Exchange 部署并确定配置是否符合 Microsoft 最佳做法。在 Exchange 2013 中，Exchange 最佳实践分析工具已被<a href="https://go.microsoft.com/fwlink/p/?linkid=391077">适用于 Exchange Server 2013 的 Office 365 最佳实践分析工具</a>所取代。</p></td>
</tr>
<tr class="even">
<td><p>邮件流疑难解答程序</p></td>
<td><p>在 Exchange 2010 中，邮件流疑难解答程序可帮助您解决常见邮件流问题。在 Exchange 2013 中，停用了邮件流疑难解答程序。现在可以在 Exchange 2013 中使用 EAC 中的邮件跟踪功能。有关详细信息，请参阅<a href="track-messages-with-delivery-reports-exchange-2013-help.md">使用送达报告跟踪邮件</a>。</p></td>
</tr>
<tr class="odd">
<td><p>性能监视器</p></td>
<td><p>在 Exchange 2010 中，性能监视器包含在 Exchange 工具箱中，可用于收集有关邮件系统性能的信息。性能监视器通常用于在排除性能问题时查看关键参数。在 Exchange 2013 中，在工具箱中停用了性能监视器。仍可以在 Windows Server 2008 中的“管理工具”下找到性能监视器。</p></td>
</tr>
<tr class="even">
<td><p>性能疑难解答程序</p></td>
<td><p>在 Exchange 2013 中，停用了性能疑难解答程序。</p></td>
</tr>
<tr class="odd">
<td><p>路由日志查看器</p></td>
<td><p>在 Exchange 2013 中，停用了路由日志查看器。</p></td>
</tr>
</tbody>
</table>


## 邮箱数据库副本


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Update-MailboxDatabaseCopy</p></li>
<li><p>更新邮箱数据库副本向导</p></li>
</ul></td>
<td><p>内容索引目录种子设定不再可通过复制网络实现；它仅可以通过 MAPI 网络完成。在 Update-MailboxDatabaseCopy cmdlet 中使用 <code>-Network</code> 参数时，这也适用。</p></td>
</tr>
</tbody>
</table>


## 从 Exchange 2007 到 Exchange 2013 的废弃功能

此节列出了在 Exchange 2013 中不再提供的 Exchange Server 2007 功能。

## API 及开发


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange WebDAV</p></td>
<td><p>使用 <a href="https://go.microsoft.com/fwlink/p/?linkid=167197">Exchange Web 服务</a>或 <a href="https://go.microsoft.com/fwlink/p/?linkid=157179">EWS 托管 API</a>。另外，可以为由使用 WebDAV 的应用程序管理的邮箱维护一个 Exchange 2007 服务器。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=169474">从 WebDAV 迁移</a>。</p></td>
</tr>
</tbody>
</table>


## 体系结构


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>存储组</p></td>
<td><p>Exchange 2013 不能再使用存储组构造，并改为只是管理邮箱数据库。有关详细信息，请参阅<a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">管理 Exchange 2013 中的邮箱数据库</a>。</p></td>
</tr>
<tr class="even">
<td><p>可扩展存储引擎 (ESE) 流式备份 API</p></td>
<td><p>Exchange 2013 仅支持基于卷影复制服务 (VSS) 的 Exchange 感知备份。Exchange 2013 包含 Windows 服务器备份插件，让您能够备份和还原数据。有关信息，请参阅<a href="backup-restore-and-disaster-recovery-exchange-2013-help.md">备份、还原和灾难恢复</a>。</p></td>
</tr>
<tr class="odd">
<td><p>用户数据报协议 (UDP) 通知</p></td>
<td><p>用户数据报协议 (UDP) 通知的支持已从 Exchange 2013 中删除。这将影响 Outlook 2003 客户端连接到 Exchange 2013 服务器中邮箱时的用户体验。有关详细信息，请参阅 Microsoft 知识库文章 2009942：<a href="http://go.microsoft.com/fwlink/?linkid=3052&kbid=2009942">Exchange Server 2010 用户以联机模式使用 Outlook 2003 时更新文件夹需要很长时间</a>。</p></td>
</tr>
</tbody>
</table>


## 高可用性


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>群集连续复制 (CCR)</p></td>
<td><p>Exchange 2013 使用数据库可用性组 (DAG) 和邮箱数据库副本。有关信息，请参阅<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性和站点恢复</a>。</p></td>
</tr>
<tr class="even">
<td><p>本地连续复制 (LCR)</p></td>
<td><p>Exchange 2013 使用 DAG 和邮箱数据库副本。有关信息，请参阅<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性和站点恢复</a>。</p></td>
</tr>
<tr class="odd">
<td><p>备用连续复制 (SCR)</p></td>
<td><p>Exchange 2013 使用 DAG 和邮箱数据库副本。有关信息，请参阅<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性和站点恢复</a>。</p></td>
</tr>
<tr class="even">
<td><p>单一副本群集 (SCC)</p></td>
<td><p>Exchange 2013 使用 DAG 和邮箱数据库副本。有关信息，请参阅<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性和站点恢复</a>。</p></td>
</tr>
<tr class="odd">
<td><p>Setup /recoverCMS</p></td>
<td><p>Exchange 2013 使用 Setup /m:recoverServer。有关信息，请参阅<a href="recover-an-exchange-server-exchange-2013-help.md">恢复 Exchange 服务器</a>。</p></td>
</tr>
<tr class="even">
<td><p>群集邮箱服务器</p></td>
<td><p>Exchange 2013 使用 DAG 和邮箱数据库副本。有关信息，请参阅<a href="high-availability-and-site-resilience-exchange-2013-help.md">高可用性和站点恢复</a>。</p></td>
</tr>
</tbody>
</table>


## 客户端访问


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>对 POP3 和 IMAP4 用户使用集成 Windows 身份验证 (NTLM) 这一客户端身份验证方式</p></td>
<td><p>在 Exchange 2013 中，POP3 或 IMAP4 客户端连接不支持 NTLM。使用 NTLM 从 POP3 或 IMAP4 客户端程序连接将失败。如果您运行的是 Exchange 2013 的 RTM 版本，NTLM 的建议替代方案就是采用使用 SSL 的纯文本身份验证。</p>
<p>如果使用的是 Exchange 2013，则必须在 Exchange 2013 组织中保留一个 Exchange 2007 服务器，才能使用 NTLM。</p></td>
</tr>
</tbody>
</table>


## Outlook Web App 和 Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>文档访问</p></td>
<td><p>Outlook Web App 不能用于访问 Microsoft SharePoint 文档库和 Windows 文件共享。</p></td>
</tr>
<tr class="even">
<td><p>邮件标志</p></td>
<td><p>在 Outlook Web App 2013 中，无法在邮件标记上设置自定义日期。您可以使用 Outlook 设置自定义日期。</p></td>
</tr>
<tr class="odd">
<td><p>拼写检查</p></td>
<td><p>Outlook Web App 使用 Web 浏览器中的拼写检查功能。</p></td>
</tr>
<tr class="even">
<td><p>搜索文件夹</p></td>
<td><p>当前 Outlook Web App 中不提供让用户使用搜索文件夹的功能。</p></td>
</tr>
<tr class="odd">
<td><p>最大缓存视图数</p></td>
<td><p>Exchange 2007 支持为 Outlook 客户端的每个数据库 (msExchMaxCachedViews) 参数修改最大缓存视图数。Exchange 2013 不再使用此参数。</p></td>
</tr>
</tbody>
</table>


## 与收件人有关的功能


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Export-Mailbox</strong> cmdlet 和 <strong>Import-Mailbox</strong> cmdlet</p></td>
<td><p>在 Exchange 2013 中，使用导出请求或导入请求。有关详细信息，请参阅<a href="mailbox-import-and-export-requests-exchange-2013-help.md">邮箱导入和导出请求</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>Move-Mailbox</strong> cmdlet 集</p></td>
<td><p>在 Exchange 2013 中，使用移动请求来移动邮箱。有关信息，请参阅 <a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的邮箱移动</a>。</p></td>
</tr>
<tr class="odd">
<td><p>ISInteg</p></td>
<td><p>在 Exchange 2013 中，使用 <a href="https://technet.microsoft.com/zh-cn/library/ff625226(v=exchg.150)">New-MailboxRepairRequest</a>。</p></td>
</tr>
</tbody>
</table>


## 邮件策略和合规性


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>托管文件夹</p></td>
<td><p>在 Exchange 2007 中，使用托管文件夹进行邮件保留管理 (MRM)。在 Exchange 2013 中，不支持托管文件夹。您必须使用 MRM 的保留策略。</p>

> [!NOTE]  
> 与托管文件夹相关的 Cmdlet 仍然可用。您可以创建托管文件夹、托管内容设置和托管文件夹邮箱策略，并且将托管文件夹邮箱策略应用于用户，但是，MRM 助手将跳过对已应用托管文件夹邮箱策略的邮箱的处理。

</td>
</tr>
</tbody>
</table>


## 统一消息和语音邮件


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>注释和缓解操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用用于 Outlook Voice Access 的自动语音识别 (ASR) 的目录查找</p></td>
<td><p>在 Exchange 2007 中，Outlook Voice Access 用户可以通过英语（美国）(en-US) 自动语音识别 (ASR)，使用语音输入来搜索在目录中列出的用户。在 Outlook Voice Access 中，也可以使用语音输入来导航菜单、邮件和其他选项。但是，即使 Outlook Voice Access 用户可以使用语音输入，他们仍需使用电话软键盘来输入 PIN 和导航个人选项。</p>
<p>在 Exchange 2013 中，经过身份验证和未经过身份验证的 Outlook Voice Access 用户无法使用任何语言的语音输入或 ASR 来搜索目录中的用户。但是，向自动助理发出呼叫的呼叫者可以使用多种语言的语音输入来导航自动助理菜单和搜索目录中的用户。</p></td>
</tr>
</tbody>
</table>

