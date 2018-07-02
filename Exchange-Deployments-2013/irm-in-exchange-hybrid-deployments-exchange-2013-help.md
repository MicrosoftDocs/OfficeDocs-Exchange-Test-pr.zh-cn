---
title: 'Exchange 混合部署中的 IRM: Exchange 2013 Help'
TOCTitle: Exchange 混合部署中的 IRM
ms:assetid: ba6ec48b-8f79-4807-b74b-fd442bbbe82f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ659052(v=EXCHG.150)
ms:contentKeyID: 50492081
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 混合部署中的 IRM

 

_<strong>适用于：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上一次修改主题：</strong>2016-12-09_

**摘要：** IRM 在 Exchange 混合环境中的工作方式，以及如何配置 IRM 以在 Exchange Online 和内部部署 Exchange 服务器之间工作。

信息权限管理 (IRM) 通过对电子邮件和附件提供持久联机和脱机保护来帮助防止敏感信息泄露。内部部署组织中的 Exchange 以及 Office 365 企业版中的 Exchange Online 都支持 IRM。但是，这两种实现之间有一些不同；您必须在 Exchange Online 组织中配置 IRM，然后该组织中的用户才能使用该功能。

IRM 将使用作为 Windows Server 2008 及更高版本的一个组件的 Active Directory Rights Management Services (AD RMS)。AD RMS 允许用户创建受权限保护的内容，如电子邮件和附件，并控制内容的使用方式以及分发对象。用户可以指定模板以确定内容的使用方式。例如，用户可以指定不能将某封电子邮件转发给其他收件人，或不能复制邮件中的信息。

进一步了解 Exchange 2010 中的 IRM：[Understanding Information Rights Management](https://technet.microsoft.com/zh-cn/library/dd638140\(v=exchg.141\).aspx)（了解信息权限管理）。

在[信息权限管理](https://technet.microsoft.com/zh-cn/library/dd638140\(v=exchg.150\))进一步了解 Exchange 2013 和 Exchange 2016 中的 IRM。

有关 AD RMS 的详细信息，请参阅 [Active Directory 权限管理服务](http://go.microsoft.com/fwlink/p/?linkid=215243)。

## IRM 在 Exchange 内部部署和 Exchange Online 之中的差别

内部部署 Exchange 组织中提供的 IRM 功能可能不同于 Exchange Online 组织中提供的功能。下表汇总了在每个组织中可用的功能。（进一步了解这些功能：[信息权限管理](https://technet.microsoft.com/zh-cn/library/dd638140\(v=exchg.150\))）

### 可用的 IRM 功能

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>在 Exchange 2007 及之前版本中可用</th>
<th>在 Exchange 2010 中是否可用</th>
<th>在 Exchange Online 和 Exchange 2013 及更高版本中可用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>手动保护 Outlook 中的邮件</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>手动保护 Outlook Web App 中的邮件</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>查看 Outlook 中受 IRM 保护的邮件</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>查看 Outlook Web App 中受 IRM 保护的邮件</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>IRM 预许可代理</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>RMS 策略模板</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>传输解密</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>日记报告解密</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 搜索和发现解密</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>自动 Outlook 保护规则</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>自动传输保护规则</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


## 混合部署中的 IRM

Exchange 将使用安装有 Exchange 服务器的 Active Directory 林中的 AD RMS 服务器。对于内部部署 Exchange 服务器，使用内部部署 AD RMS 服务器。对于 Exchange Online 组织，使用在 Office 365 数据中心中维护的 AD RMS 服务器。每个 Exchange 组织使用的 AD RMS 配置独立于任何其他 AD RMS 部署。

AD RMS 配置不会在内部部署 Exchange 组织和 Exchange Online 组织之间自动进行复制，因而 IRM 配置也是如此。所定义的任何 AD RMS 模板不会自动复制到 Exchange Online 组织。如果希望相同的 AD RMS 模板在 Exchange Online 组织中可用，必须手动将模板从内部部署组织中导出，并将其应用于 Office 365 组织。请参阅本主题后面的在混合部署中配置 IRM。

## 用户体验

应用于用户的 IRM 配置取决于用户使用的客户端以及用户邮箱的位置。下表列出了用户可使用的 AD RMS 服务器。

### Active AD RMS 服务器

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端</th>
<th>内部部署邮箱</th>
<th>Exchange Online 邮箱</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 桌面客户端</p></td>
<td><p>内部部署 AD RMS</p></td>
<td><p>内部部署 AD RMS</p></td>
</tr>
<tr class="even">
<td><p>Web 上的 Outlook</p></td>
<td><p>内部部署 AD RMS</p></td>
<td><p>Exchange Online AD RMS</p></td>
</tr>
<tr class="odd">
<td><p>ActiveSync 设备</p></td>
<td><p>内部部署 AD RMS</p></td>
<td><p>Exchange Online AD RMS</p></td>
</tr>
</tbody>
</table>


根据在内部部署和基于 Exchange Online 组织中配置的 AD RMS 配置，使用 Outlook 2007 和 Web 上的 Outlook 的用户可能会看到不同的 AD RMS 模板。因此，我们强烈建议您对内部部署和 Exchange Online 组织应用相同的模板。

对于 Outlook 客户端用户，无论其邮箱是在内部部署组织中还是在 Exchange Online 组织中，其 IRM 体验应该没有任何差别。

其邮箱位于 Exchange 内部部署服务器上的 Web 上的 Outlook 用户在安装了用于 Internet Explorer 的权限管理外接程序后只能打开受权限保护的邮件，并且不能答复或新建受权限保护的邮件。

其邮箱位于 Exchange Online 中的 Web 上的 Outlook 用户无需任何附加软件便可打开受权限保护的邮件，并且可以答复和新建受权限保护的邮件。

## 服务器功能

内部部署 Exchange 服务器使用 AD RMS 预许可代理来解密受权限保护的邮件，这样用户不必提供凭据便可打开这些邮件。内部部署 Exchange 服务器将联系内部部署 AD RMS 服务器来核查使用策略和权限，并请求授权以解密邮件。

Exchange Online 组织还提供了几个与 IRM 相关的功能，这些功能使用了 Exchange Online AD RMS。通过这些功能（如日记报告解密），Exchange 服务可对受权限保护的邮件内容进行额外的处理。例如，可以与原始受权限保护的邮件一起保存已解密的日记邮件内容，以便更有利于发现。此外，使用 Outlook 保护规则或传输规则，IRM 模板可以自动应用于邮件，以确保邮件符合组织在信息保护方面的策略。

## 在混合部署中配置 IRM

Exchange 中的 IRM 依赖于在 Exchange 服务器所在的 Active Directory 林中部署的 AD RMS。AD RMS 配置不会自动在内部部署组织和 Exchange Online 组织之间进行同步。您必须从内部部署 AD RMS 服务器手动导出已知是受信任发布域 (TPD) 的 AD RMS 配置，并将该配置导入到 Exchange Online 组织中。TPD 包含 Exchange Online 组织使用 IRM 时所需要的 AD RMS 配置，包括模板。

有关更多信息，请参阅 [AD RMS 受信任发布域的注意事项](http://go.microsoft.com/fwlink/p/?linkid=215244)。

除了对 Exchange Online 组织应用内部部署 AD RMS 配置外，您还必须确保内部部署网络之外的 Outlook 和 ActiveSync 客户端能够联系到 AD RMS 服务器。如果您希望这些客户端能够访问内部部署网络之外的受权限保护的邮件，就必须做到这一点。

配置了内部部署网络并导出了 TPD 数据后，您需要通过导入 TPD 数据并启用 IRM 来配置 Exchange Online 组织。

<table>
<thead>
<tr class="header">
<th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>每当修改内部部署 AD RMS 配置时，都必须手动在 Exchange Online 组织中应用新配置。为此，请从内部部署 AD RMS 服务器导出 TPD 数据，并将其导入到 Exchange Online 组织中。</td>
</tr>
</tbody>
</table>


## 如何在 Exchange 混合部署中配置 IRM

如果在内部部署 Exchange 组织中使用 IRM，并且希望 Exchange Online 用户也使用 IRM，则需要执行以下操作：

1.  配置内部部署 Active Directory Rights Management Services (AD RMS) 服务器。

2.  在 Exchange Online 组织中启用 IRM。

3.  将导入的 AD RMS 模板分发给 Exchange Online 组织中的用户。

## 如何配置内部部署 AD RMS 服务器？

若要在混合部署中配置 IRM，需要使用 Windows PowerShell 来访问内部部署 AD RMS 服务器。有关详细信息，请参阅[使用 Windows PowerShell 管理 AD RMS](http://go.microsoft.com/fwlink/p/?linkid=214938)

执行以下操作，从内部部署 AD RMS 服务器导出受信任的发布域 (TPD) 数据，然后配置外部客户端对 AD RMS 服务器的访问。

1.  从内部部署组织导出 TPD 数据。有关详细信息，请参阅[导出受信任的发布域](http://go.microsoft.com/fwlink/p/?linkid=214942)

2.  配置外部客户端对 AD RMS 服务器的访问。有关详细信息，请参阅[添加 Extranet 群集 URL](http://go.microsoft.com/fwlink/p/?linkid=214945)

## 如何在 Exchange Online 组织中启用 IRM？

从内部部署 AD RMS 服务器导出 TPD 数据后，需要将这些数据导入到 Exchange Online 组织中，然后启用 IRM。

1.  在 Exchange Online 组织中，导入 TPD 数据。
    
        Import-RMSTrustedPublishingDomain -FileData $( [Byte[]] (Get-Content -Encoding Byte -Path "<Path to exported TPD file>" -ReadCount 0))

2.  在 Exchange Online 组织中启用 IRM。
    
        Set-IRMConfiguration -InternalLicensingEnabled $True

## 如何在 Exchange Online 组织中分发 AD RMS 模板？

在 Exchange Online 组织中启用了 IRM 之后，必须分发导入的 AD RMS 模板。以下 Exchange Online 用户和功能使用 AD RMS 模板：

  - Web 上的 Outlook 用户

  - Exchange ActiveSync 用户

  - 传输规则

  - 日记报告解密

  - Outlook 保护规则

<!-- end list -->

1.  在 Exchange Online 组织中，检索 AD RMS 模板的列表。
    
        Get-RMSTemplate -Type All

2.  将 AD RMS 模板分发给 Exchange Online 组织中的用户和功能。
    
        Set-RMSTemplate <template name> -Type Distributed
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>无法修改“不要转发”AD RMS 模板。</td>
    </tr>
    </tbody>
    </table>


3.  对要分发的每个 AD RMS 模板重复步骤 2。

## 我如何知道这有效？

Web 上的 Outlook 用户应能够将 AD RMS 模板应用于新邮件。Web 上的 Outlook 和 Exchange ActiveSync 用户应能够阅读应用了 AD RMS 模板的邮件。此外，运行 **Get-RMSTemplate** cmdlet 时，应列出从内部部署组织导入的所有 AD RMS 模板。

在 Exchange Online 组织中运行以下命令。

    Get-RMSTemplate 

可在以下位置了解详细信息：[Outlook Web App 中的信息权限管理](https://technet.microsoft.com/zh-cn/library/dd876891\(v=exchg.150\))

