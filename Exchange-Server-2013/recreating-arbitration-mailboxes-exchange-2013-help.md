---
title: 'Recreating arbitration mailboxes: Exchange 2013 Help'
TOCTitle: Recreating arbitration mailboxes
ms:assetid: bb6b8524-aaee-4be8-a04e-e61cd2ab3465
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt829264(v=EXCHG.150)
ms:contentKeyID: 74518125
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recreating arbitration mailboxes

 

_**上一次修改主题：** 2018-01-17_

**摘要：**  有关仲裁邮箱Exchange 2013以及如何重新创建它们。

Exchange 2013带有五个称为*仲裁邮箱*的系统邮箱。用于存储不同类型的系统数据和用于管理消息处理审批工作流使用仲裁的邮箱。图表下方列出了每种类型的仲裁邮箱，他们的职责。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>仲裁邮箱名称</th>
<th>显示名称</th>
<th>保留的功能</th>
<th>函数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042</p></td>
<td><p>联盟的 Microsoft Exchange 邮箱</p></td>
<td><p>{}</p></td>
<td><p>此邮箱存储数据用于维护不同 Exchange 组织之间的联盟。这包括权限管理服务、 跨内部邮件流监视探测和响应、 通知， 在线档案、 邮件记录管理和交叉场所忙/闲信息。</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{1f05a927-9350-4efe-a823-5529c2d64109}</p></td>
<td><p>Microsoft Exchange 批准助理</p></td>
<td><p>{}</p></td>
<td><p>此邮箱的收件人的裁决和自动组审批请求交换批准框架提供使用。</p></td>
</tr>
<tr class="odd">
<td><p>Migration.8f3e7716-2011-43e4-96b1-aba62d229136</p></td>
<td><p>Microsoft Exchange 迁移</p></td>
<td><p>{OrganizationCapabilityManagement}</p></td>
<td><p>将 Exchange 迁移服务，以时移动邮箱在批处理中的使用的数据存储。</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMDataStorage}</p></td>
<td><p>发现系统邮箱。</p>
<p>用于设置通过电子邮件发现功能，法规遵从性监察官用于查找与指定的选择条件匹配的邮件。 此邮箱还可通过统一消息存储 UM 控制台参加文件和其他信息。</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMGrammarReady, OrganizationCapabilityPstProvider, OrganizationCapabilityMessageTracking, OrganizationCapabilityMailRouting, OrganizationCapabilityClientExtensions, OrganizationCapabilityGMGen, OrganizationCapabilityOABGen, OrganizationCapabilityUMGrammar}</p></td>
<td><p>这就是一个组织的邮箱。它用来创建脱机通讯簿 (OABs)。对负载平衡 OAB 生成整个组织，包括跨地理位置上分散的站点，您可以创建其他组织邮箱。</p></td>
</tr>
</tbody>
</table>


如果您需要重新创建一个或多个这些仲裁的邮箱，请参阅后面的说明。

## 在开始之前应了解的内容

  - 估计完成时间： 10 分钟，每个过程。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;收件人设置权限\&quot;部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 使用Exchange 命令行管理程序重新创建仲裁邮箱

请按照以下说明重新创建特定类型的仲裁邮箱。

> [!NOTE]  
> 以下各节中的所有步骤必须都运行相同的目录中提取 Exchange 安装媒体的位置。


## 重新创建 Microsoft Exchange 联盟邮箱

若要重新创建仲裁邮箱 FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042:

1.  如果丢失了任何仲裁的邮箱，请运行以下命令：
    
    ```powershell
.\Setup /preparead /IAcceptExchangeServerLicenseTerms
```

2.  在Exchange 命令行管理程序，运行以下命令：
    
    ```powershell
Enable-Mailbox -Arbitration -Identity "FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042"
```

## 重新创建 Microsoft Exchange 助手审批的邮箱

若要重新创建仲裁邮箱 SystemMailbox {1f05a927-9350-4efe-a823-5529c2d64109}:

1.  如果丢失了任何仲裁的邮箱，请运行以下命令：
    
    ```powershell
.\Setup /preparead /IAcceptExchangeServerLicenseTerms
```

2.  在Exchange 命令行管理程序，运行以下命令：
    
        Get-User | Where-Object {$_.Name -like "SystemMailbox{1f05a927-7709-4e35-9dbe-d0f608fb781a}"} | Enable-Mailbox -Arbitration

## 重新创建 Microsoft Exchange 迁移邮箱

若要重新创建仲裁邮箱 Migration.8f3e7716-2011年-43e4-96b1-aba62d229136:

1.  如果丢失了任何仲裁的邮箱，请运行以下命令：
    
    ```powershell
.\Setup /preparead /IAcceptExchangeServerLicenseTerms
```

2.  在Exchange 命令行管理程序，运行以下命令：
    
    ```powershell
Enable-Mailbox -Arbitration -Identity "Migration.8f3e7716-2011-43e4-96b1-aba62d229136"
```

3.  在Exchange 命令行管理程序，通过运行以下命令来设置保留功能 (msExchCapabilityIdentifiers):
    
    ```powershell
Set-Mailbox "Migration.8f3e7716-2011-43e4-96b1-aba62d229136" -Arbitration -Management:$True -Force
```

## 重新创建 Microsoft Exchange 发现系统邮箱

若要重新创建仲裁邮箱 SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}:

1.  运行以下命令：
    
    ```powershell
.\Setup /preparead /IAcceptExchangeServerLicenseTerms
```

## 重新创建 Microsoft Exchange 组织邮箱 OABs

若要重新创建仲裁邮箱 SystemMailbox {bb558c35-97f1-4cb9-8ff7-d53741dc928c}:

1.  如果丢失了任何仲裁的邮箱，请运行以下命令：
    
    ```powershell
.\Setup /preparead /IAcceptExchangeServerLicenseTerms
```

2.  在Exchange 命令行管理程序，运行以下命令：
    
    ```powershell
Enable-Mailbox -Arbitration -Identity "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}"
```

3.  在Exchange 命令行管理程序，通过运行以下命令来设置保留功能 (msExchCapabilityIdentifiers):
    
        Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration | Set-Mailbox -Arbitration -UMGrammar:$True -OABGen:$True -GMGen:$True -ClientExtensions:$True -MessageTracking:$True -PstProvider:$True -MaxSendSize 1GB -Force

当完成后，如果运行命令`$OABMBX = Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration (Get-ADUser $OABMBX.SamAccountName -Properties *).msExchCapabilityIdentifiers` ，您将看到，46、 47 和 51 丢失了。运行下面的命令以添加所有的功能恢复：

    Set-ADUser $OABMBX.SamAccountName -Add @{"msExchCapabilityIdentifiers"="40","42","43","44","47","51","52","46"}

## 我如何知道这有效？

若要验证成功有重新创建仲裁邮箱，使用*Arbitration*开关**Get-Mailbox** cmdlet 检索系统邮箱。

```powershell
Get-Mailbox -Arbitration | Format-Table Name, DisplayName
```

查看命令来验证已重新创建该适当的系统邮箱，或者按名称或从上面的表中，显示名称的结果。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

