---
title: '下载引擎和定义更新: Exchange 2013 Help'
TOCTitle: 下载引擎和定义更新
ms:assetid: 8f2ca383-e463-4df0-aa5d-29afe2f81aaf
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657471(v=EXCHG.150)
ms:contentKeyID: 50491018
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 下载引擎和定义更新

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-04-08_

Microsoft Exchange Server 2013 管理员可以手动下载反恶意软件引擎和定义（签名）更新。强烈建议您在将 Exchange 服务器置于生产环境之前将引擎和定义更新下载到 Exchange 服务器上。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 要下载更新，您的计算机必须能够访问 Internet，并且必须能够在 TCP 端口 80 (HTTP) 上建立连接。

  - UNRESOLVED\_TOKEN\_VAL(PD\_Shell\_Only\_Procedure)

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[反垃圾邮件和反恶意软件权限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) 主题中的“反恶意软件”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

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


## 使用命令行管理程序手动下载引擎和定义更新

要下载引擎和定义更新，请运行下列命令：

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity <FQDN of server>

本示例将引擎和定义更新手动下载到名为 mailbox01.contoso.com 的服务器上：

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com

您还可以指定 –EngineUpdatePath 参数，该参数允许您从除默认路径 http://forefrontdl.microsoft.com/server/scanengineupdate 以外的其他位置下载更新。这可以是一个 HTTP 地址或一个 UNC 路径。如果是后者，则网络服务必须具有访问该路径的权限。该示例将引擎和定义更新从本地目录手动下载到名为 mailbox01.contoso.com 的服务器上：

    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com -EngineUpdatePath \\Server\sharename

## 您如何知道这有效？

要验证是否已成功下载更新，您需要访问事件查看器，然后查看事件日志。建议您按照下列步骤仅筛选 FIPFS 事件：

1.  从“开始”菜单中，单击“所有程序”\>“管理工具”\>“事件查看器”。

2.  在事件查看器中，展开“Windows 日志”文件夹，然后单击“应用程序”。

3.  在“操作”菜单中，单击“筛选当前日志”。

4.  在“筛选当前日志”对话框中，从“事件源”下列列表中，选中“FIPFS”复选框，然后单击“确定。

如果引擎已成功下载，您将看到事件 ID 6033，其中将显示类似如下的信息：

`MS Filtering Engine Update process performed a successful scan engine update.`

`Scan Engine: Microsoft`

`Update Path: http://forefrontdl.microsoft.com/server/scanengineupdate`

`Last Update time: ‎2012‎-‎08‎-‎16T13:22:17.000Z`

`Engine Version: 1.1.8601.0`

`Signature Version: 1.131.2169.0`

## 详细信息

[配置反恶意软件策略](configure-anti-malware-policies-exchange-2013-help.md)

