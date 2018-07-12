---
title: '导出邮箱审核日志: Exchange 2013 Help'
TOCTitle: 导出邮箱审核日志
ms:assetid: b458a95a-3321-4647-8884-cf97f8e7186a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150552(v=EXCHG.150)
ms:contentKeyID: 50489726
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 导出邮箱审核日志

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

在为某个邮箱启用邮箱审核之后，只要非所有者的用户访问该邮箱，Microsoft Exchange 就会在*邮箱审核日志*中记录相关信息。每个日志条目都包含以下相关信息：访问邮箱的用户及访问时间、非所有者执行的操作以及是否成功执行操作。默认情况下，邮箱审核日志中的条目将保留 90 天。可以使用邮箱审核日志来确定某个非邮箱所有者的用户是否访问过邮箱。

当您导出邮箱审核日志中的条目时，Microsoft Exchange 会将这些条目保存在一个 XML 文件中，然后将其附加到发送到指定收件人的电子邮件中。

**目录**

开始之前

配置邮箱审核日志记录

导出邮箱审核日志

查看邮箱审核日志

详细信息

## 开始之前

  - 估计完成每个步骤时间：时间是变量。在 Exchange Online 中，邮箱审核日志会在导出之后数天内发送。

  - 在 Exchange Online 中，您必须使用远程 Windows PowerShell 来执行本主题中的许多过程。有关详细信息，请参阅[使用远程 PowerShell 连接到 Exchange Online](https://technet.microsoft.com/zh-cn/library/jj984289\(v=exchg.150\))。

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 配置邮箱审核日志记录

在可以导出和查看邮箱审核日志之前，必须为您想要审核的每个邮箱启用邮箱审核日志记录。此外，还必须配置 Microsoft Outlook Web App 以允许 XML 附件使用 Outlook Web App 访问审核日志。

## 步骤 1：启用邮箱审核日志记录

对于需要运行非所有者邮箱访问报告的每个邮箱，必须启用邮箱审核日志记录。如果未对邮箱启用邮箱审核日志记录，则当导出邮箱审核日志时，将不会获得有关该邮箱的任何结果。

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“邮箱审核日志记录”条目。

若要对单个邮箱启用邮箱审核日志记录，请运行命令行管理程序中的命令：

    Set-Mailbox <Identity> -AuditEnabled $true

若要对组织中所有用户邮箱启用邮箱审核日志记录，请运行以下命令：

```
    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
```
```
    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}
```

## 步骤 2：配置 Outlook Web App 以允许 XML 附件

当您导出邮箱审核日志时，Microsoft Exchange 会将该审核日志（即一个 XML 文件）附加到电子邮件。但是，默认情况下，Outlook Web App 将阻止 XML 附件。若要访问导出的审核日志，必须使用 Microsoft Outlook 或配置 Outlook Web App 以允许 XML 附件。

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“Outlook Web App 邮箱策略”条目。

执行以下过程以在 Outlook Web App 中允许添加 XML 附件。在 Exchange Server 2013 中，对 *Identity* 参数使用 `Default` 值。

1.  运行以下命令，将 XML 添加到 Outlook Web App 中允许的文件类型列表。
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -AllowedFileTypes @{add='.xml'}

2.  运行以下命令，将 XML 从 Outlook Web App 中被阻止的文件类型列表中删除。
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -BlockedFileTypes @{remove='.xml'}

## 您如何知道这有效？

若要验证是否已成功配置邮箱审核日志记录，请执行以下操作：

1.  运行以下命令以验证是否已对邮箱配置审核日志记录：
    
        Get-Mailbox | FL Name,AuditEnabled
    
    *AuditEnabled* 属性的值为 `True` 验证已启用审计记录。

2.  运行以下命令以验证 Outlook Web App 中是否允许使用 XML 附件。
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty AllowedFileTypes
    
    请验证 `.xml` 是否已包含在允许的文件类型列表中。

3.  运行以下命令以验证是否已将 XML 附件从 Outlook Web App 中被阻止的文件列表中删除。
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty BlockedFileTypes
    
    验证 `.xml` 是否未包含在受阻止的文件类型列表中。

返回顶部

## 导出邮箱审核日志

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的“仅查看管理员审核日志记录”条目。

1.  在 Exchange 管理中心 (EAC) 中，转到“合规性管理”\>“审核”。

2.  单击“导出邮箱审核日志”。

3.  配置以下搜索条件以导出邮箱审核日志中的条目：
    
      - **开始和结束日期**   选择要在导出文件中包含的条目的日期范围。
    
      - **要为其搜索审核日志的邮箱** 选择要为其检索审核日志条目的邮箱。
    
      - **非所有者访问的类型** 选择下列选项之一来定义要为其检索条目的非所有者访问类型：
        
          - **全部非所有者** 搜索组织内部的管理员和受委派用户的访问以及 Exchange Online 中的 Microsoft 数据中心管理员的访问。
        
          - **外部用户**   搜索 Microsoft 数据中心管理员的访问。
        
          - **管理员和代理用户**   搜索组织内的管理员和代理用户的访问。
        
          - **管理员** 搜索组织内的管理员的访问。
    
      - **收件人**   选择要将邮箱核日志发送到的用户。

4.  单击“导出”。
    
    Microsoft Exchange 将在邮箱审核日志中检索符合搜索条件的条目，并将这些条目保存到一个名为 SearchResult.xml 的文件中，然后再将该 XML 文件附加到发送到指定收件人的电子邮件。

## 您如何知道这有效？

登录到已将邮箱审核日志发送到的邮箱。如果已成功导出审核日志，则将收到 Exchange 发送的邮件。在 Exchange Online 中，可能需要几天才能收到此邮件。邮箱审核日志（名为 SearchResult.xml）将附加到此邮件。如果您已正确配置 Outlook Web App 以允许 XML 附件，您就可以下载附加的 XML 文件。

返回顶部

## 查看邮箱审核日志

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的“仅查看管理员审核日志记录”条目。

要保存并查看 SearchResult.xml 文件，请执行以下操作：

1.  登录到已将邮箱审核日志发送到的邮箱。

2.  在“收件箱”中，打开 Microsoft Exchange 发送的带有 XMl 文件附件的邮件。请注意，此电子邮件的正文包含搜索条件。

3.  单击附件，并选择以下载该 XML 文件。

4.  在 Microsoft Excel 中打开 SearchResult.xml。

返回顶部

## 详细信息

  - **邮箱审核日志中的条目**   以下示例显示 SearchResult.xml 文件中包含的邮箱审核日志中的条目。每个条目以 **\<Event\>** XML 标记开头，并以 **\</Event\>** XML 标记结尾。此条目显示，管理员于 2010 年 4 月 30 日从 David 的邮箱中“可恢复的项目”文件夹中清除了主题为“**Notification of litigation hold**”的邮件。
    
        <Event MailboxGuid="6d4fbdae-e3ae-4530-8d0b-f62a14687939" 
          Owner="PPLNSL-dom\david50001-1363917750" 
          LastAccessed="2010-04-30T11:01:55.140625-07:00" 
          Operation="HardDelete" 
          OperationResult="Succeeded" 
          LogonType="Admin"
         FolderId="0000000073098C3277988F4CB882F5B82EBF64610100A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000"
          FolderPathName="\Recoverable Items\Deletions"
          ClientInfoString="Client=OWA;Action=ViaProxy" 
          ClientIPAddress="10.196.241.168" 
          InternalLogonType="Owner"
          MailboxOwnerUPN="david@contoso.com"
          MailboxOwnerSid="S-1-5-21-290112810-296651436-1966561949-1151" 
          CrossMailboxOperation="false" 
          LogonUserDN="Administrator"
          LogonUserSid="S-1-5-21-290112810-296651436-1966561949-1149">
          <SourceItems>
           <ItemId="0000000073098C3277988F4CB882F5B82EBF64610700A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000A7C317F68C24304BBD18ABE1F185E79B00000026BD540"
            Subject="Notification of litigation hold"
            FolderPathName="\Recoverable Items\Deletions" /> 
          </SourceItems>
        </Event>

  - **邮箱审核日志中的有用字段**   以下是对邮箱审核日志中的有用字段的说明。这些字段可帮助您标识有关某个邮箱的每个非所有者访问实例的特定信息。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>字段</th>
    <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Owner</strong></p></td>
    <td><p>非所有者访问过的邮箱的所有者。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>LastAccessed</strong></p></td>
    <td><p>访问邮箱的日期和时间。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Operation</strong></p></td>
    <td><p>非所有者执行的操作。有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/jj156300(v=exchg.150)">了解有关运行非所有者邮箱访问报告的详细信息</a>中的“在邮箱审核日志中记录了哪些内容？”部分。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OperationResult</strong></p></td>
    <td><p>非所有者执行的操作是成功还是失败。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonType</strong></p></td>
    <td><p>非所有者访问的类型。这些类型包括管理员、受委派用户和外部用户。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>FolderPathName</strong></p></td>
    <td><p>包含受非所有者影响的邮件的文件夹的名称。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>ClientInfoString</strong></p></td>
    <td><p>有关非所有者访问此邮箱所使用的邮件客户端的信息。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ClientIPAddress</strong></p></td>
    <td><p>非所有者访问此邮箱所使用的计算机的 IP 地址。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>InternalLogonType</strong></p></td>
    <td><p>非所有者访问此邮箱所使用的帐户登录类型。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>MailboxOwnerUPN</strong></p></td>
    <td><p>邮箱所有者的电子邮件地址。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonUserDN</strong></p></td>
    <td><p>非所有者的显示名称。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Subject</strong></p></td>
    <td><p>受非所有者影响的电子邮件的主题行。</p></td>
    </tr>
    </tbody>
    </table>
    
    返回顶部

