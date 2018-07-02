---
title: '创建外部连接器将邮件发送至非 SMTP 传真网关: Exchange 2013 Help'
TOCTitle: 创建外部连接器将邮件发送至非 SMTP 传真网关
ms:assetid: 589db487-3c4c-409a-92e3-c78dd8f639b6
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ710163(v=EXCHG.150)
ms:contentKeyID: 50490595
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建外部连接器将邮件发送至非 SMTP 传真网关

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2012-10-17_

您可能具有这样一个方案：向未使用 SMTP 作为其主要传输机制的传真网关服务器发送邮件并从其接收邮件。按照此过程中概述的步骤可创建一个外部连接器，该连接器向外部系统传递邮件并从其接收邮件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在必须将出站邮件发送到非 SMTP 系统中的大多数情况下，我们建议使用“传递代理”连接器，因为这些连接器可以对邮件队列进行管理，邮件不必写入到文件系统中，并且还有其他优势。<a href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">传递代理和传递代理连接器</a>主题提供了更多详细信息。</td>
</tr>
</tbody>
</table>


对本程序使用的方案感兴趣？请参阅下列主题：

  - [规划和部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：30 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“外部连接器”条目。

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


## 您该如何做？

## 步骤 1：使用命令行管理程序创建一个向非 SMTP 网关服务器发送邮件的外部连接器

1.  运行以下命令以创建外部连接器：
    
        New-ForeignConnector -Name "Contoso Foreign Connector" -AddressSpaces "X400:c=US;a=Fabrikam;P=Contoso;5" -SourceTransportServers Hub01,Hub02
    
    在此示例中，Hub01 和 Hub02 是组织中的源服务器，指定这些服务器向外部系统传递邮件。使用多个源服务器可提供容错能力。

在创建了外部连接器之后，可以根据组织的要求配置投递、分拣和重播目录。

## 您如何知道此步骤有效？

若要验证是否成功创建了外部连接器，请运行以下命令：

    Get-ForeignConnector | Format-List Name

验证创建的外部连接器的名称是否出现。

## 步骤 2：使用命令行管理程序为运行传输服务的邮箱服务器配置投递目录

运行传输服务的邮箱服务器的投递目录用于传递来自外部连接器的出站邮件。

创建目录以用作本地文件系统上的投递目录。还可以使用网络文件共享上的目录。

1.  运行以下脚本以为外部连接器指定投递目录（将 *DropDirectory* 参数的值更改为适用于环境的路径）：
    
        Set-ForeignConnector "Contoso Foreign Connector" -DropDirectory "C:\Drop Directory"

## 您如何知道此步骤有效？

若要验证是否正确设置了投递目录，可以运行以下 cmdlet 脚本并验证 *DropDirectory* 参数的值：

    Get-ForeignConnector "Contoso Foreign Connector" | Format-List

在创建了外部连接器并指定了投递目录之后，可以使用在其中创建外部连接器的邮箱服务器发送邮件并验证文件是否传递到投递目录。

## 步骤 3：使用命令行管理程序为邮箱服务器上的传输服务配置分拣目录

邮箱服务器上的传输服务的分拣目录用于收集非 SMTP 系统生成的邮件。可在要通过文件传输收集非 SMTP 系统（如传真网关服务器）生成的新邮件时使用此过程。

有关配置分拣目录的详细说明，请参阅[配置拾取目录和重播目录](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md)。

## 您如何知道此步骤有效？

若要验证是否正确设置了分拣目录，可以运行以下命令并验证 *PickupDirectoryPath* 参数的值：

    Get-TransportService | Format-List PickupDirectoryPath

## 步骤 4：使用命令行管理程序为邮箱服务器上的传输服务配置重播目录

邮箱服务器上的传输服务的重播目录用于收集非 SMTP 系统生成的邮件。可在要重新提交（通常从非 SMTP 外部网关服务器）在 Exchange 环境中生成并从 Exchange 传输导出的电子邮件时，使用此过程配置重播目录。

有关配置分拣目录的详细说明，请参阅[配置拾取目录和重播目录](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md)。

## 您如何知道此步骤有效？

若要验证是否正确设置了重播目录，可以运行以下命令并验证 *ReplayDirectoryPath* 参数的值：

    Get-TransportService | Format-List ReplayDirectoryPath

## 详细信息

[外部连接器](foreign-connectors-exchange-2013-help.md)

[传递代理和传递代理连接器](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

