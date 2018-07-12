---
title: '运行非所有者邮箱访问报告: Exchange 2013 Help'
TOCTitle: 运行非所有者邮箱访问报告
ms:assetid: dbbef170-e726-4735-abf1-2857db9bb52d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150575(v=EXCHG.150)
ms:contentKeyID: 50489799
ms.date: 04/17/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 运行非所有者邮箱访问报告

 

_**适用于：** Exchange Online_

_**上一次修改主题：** 2016-12-09_

Exchange 管理中心 (EAC) 中的非所有者邮箱访问报告将会列出由不是拥有邮箱的用户访问过的邮箱。在某个邮箱由非所有者访问过之后，Microsoft Exchange 将在一个邮箱审核日志中记录有关此操作的信息，该日志将作为电子邮件存储在所审核的邮箱的一个隐藏文件夹中。此日志中的条目可作为搜索结果显示，其中列出了非所有者访问过的邮箱、访问邮箱的用户和时间、非所有者执行的操作以及操作是否成功。默认情况下，邮箱审核日志中的条目将保留 90 天。

在为某个邮箱启用邮箱审核日志记录之后，Microsoft Exchange 将会记录由非所有者执行的特定操作。非所有者包括管理员和已分配了邮箱访问权限的用户（称为*“代理用户”*）。还可以将搜索范围缩小到组织内部或外部的用户。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“邮箱审核日志记录”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 启用邮箱审核日志记录

对于需要运行非所有者邮箱访问报告的每个邮箱，必须启用邮箱审核日志记录。如果未启用邮箱审核日志记录，则当您运行报告时，您将不会获得任何结果。

若要对单个邮箱启用邮箱审核日志记录，请运行以下命令行管理程序命令。

    Set-Mailbox <Identity> -AuditEnabled $true

例如，若要为名为“Florence Flipo”的用户启用邮箱审核，则运行以下命令。

    Set-Mailbox "Florence Flipo" -AuditEnabled $true

要对组织中所有用户邮箱启用邮箱审核，请运行以下命令：
```
    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
```
```
    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}
```

## 您如何知道这有效？

运行以下命令检查是否成功配置邮箱审核日志记录。

    Get-Mailbox | FL Name,AuditEnabled

*AuditEnabled* 属性的值为 `True` 验证已启用审计记录。

返回顶部

## 运行非所有者邮箱访问报告

1.  在 EAC 中，导航到“合规管理”\>“审核”。

2.  单击“运行非所有者邮箱访问报告”。
    
    默认情况下，Microsoft Exchange 将运行有关过去两周内非所有者对组织内的任何邮箱的访问情况的报告。搜索结果中列出的邮箱已启用邮箱审核日志记录。

3.  要查看特定邮箱的非所有者访问，请从邮箱列表中选择邮箱。在详细信息窗格中查看搜索结果。

> [!TIP]  
> 要缩小搜索结果的范围吗？选择开始日期、结束日期或同时选择这两个日期，并选择要搜索的特定邮箱。单击“搜索”再次运行此报告。


## 搜索特定类型的非所有者访问

您也可以指定要搜索的非所有者访问的类型（也称作“登录类型”）。您可以选择以下选项：

  - “所有非所有者”   搜索组织内的管理员和代理用户的访问。同时也包括组织外部的用户访问。

  - **外部用户**   搜索组织外部的用户访问。

  - **管理员和代理用户**   搜索组织内的管理员和代理用户的访问。

  - **管理员** 搜索组织内的管理员的访问。

返回顶部

## 您如何知道这有效？

要验证是否已成功运行非所有者邮箱访问报告，请查看搜索结果窗格。您对其行报告的邮箱将显示在窗格中。如果没有特定邮箱的结果，则可能没有非所有者访问或者在指定的日期范围内未发生非所有者访问。如之前所述，务必验证是否为要搜索非所有者访问的邮箱启用审核日志。

返回顶部

## 在邮箱审核日志中记录了哪些内容？

运行非所有者邮箱访问报告时，EAC 的搜索结果中将会显示邮箱审核日志中的条目。每个报告条目都包含以下信息：

  - 访问邮箱的用户和访问时间

  - 非所有者执行的操作

  - 受影响的邮件及其文件夹位置

  - 是否成功执行了操作

下表列出了并非由所有者执行的操作，这些操作可通过邮箱审核日志进行记录。在表中，**是**表示可为该登录类型记录操作，**否**表示操作无法记录。星号 (**\***) 表示为邮箱启用邮箱审核日志记录时，将默认记录操作。如果想要跟踪默认情况下不会记录的操作，则必须使用 PowerShell 启用对这些操作的记录。

> [!NOTE]  
> 分配了用户邮箱“完全访问”权限的管理员被视为委派用户。



<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>描述</th>
<th>管理员</th>
<th>代理用户</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>复制</strong></p></td>
<td><p>已将某个邮件复制到另一个文件夹。</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p><strong>创建</strong></p></td>
<td><p>在邮箱的日历、联系人、备注或任务文件夹中创建项目；例如，创建新的会议请求。请注意，不审核邮件或文件夹创建。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderBind</strong></p></td>
<td><p>已访问某个邮箱文件夹。</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><strong>硬删除</strong></p></td>
<td><p>已将某个邮件从“已恢复邮件”文件夹中清除。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
</tr>
<tr class="odd">
<td><p><strong>MessageBind</strong></p></td>
<td><p>在预览窗格查看邮件或打开邮件。</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p><strong>移动</strong></p></td>
<td><p>已将某个邮件移至另一个文件夹。</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><strong>移至“已删除邮件”</strong></p></td>
<td><p>已将某个邮件移至“已删除邮件”文件夹。</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><strong>代理发送</strong></p></td>
<td><p>已使用 SendAs 权限发送某个邮件。这表示另一个用户发送了邮件，而该邮件就好像来自于邮箱所有者。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
</tr>
<tr class="odd">
<td><p><strong>代表发送</strong></p></td>
<td><p>已使用 SendOnBehalf 权限发送某个邮件。这表示另一个用户代表邮箱所有者发送了邮件。此邮件将向收件人表明，此邮件是代表谁发送的以及实际发送此邮件的是谁。</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><strong>软删除</strong></p></td>
<td><p>已将某个邮件从“已删除邮件”文件夹中删除。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
</tr>
<tr class="odd">
<td><p><strong>更新</strong></p></td>
<td><p>更改了某个邮件。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> *  如果为邮箱启用了审核功能，则默认为已审核。


返回顶部

