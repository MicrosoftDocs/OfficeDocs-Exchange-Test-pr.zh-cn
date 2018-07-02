---
title: '设置新组织中的公用文件夹: Exchange 2013 Help'
TOCTitle: 设置新组织中的公用文件夹
ms:assetid: 7b419906-8977-47f0-8687-a87911b5ebec
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ651147(v=EXCHG.150)
ms:contentKeyID: 50490893
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 设置新组织中的公用文件夹

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-11-09_

**摘要：** 如何设置公用文件夹，包括在 EAC 中为其指派权限。

本主题为您演示如何配置公用文件夹以及如何在新组织中或以前从未拥有公用文件夹的组织中运行公用文件夹。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>有关存储配额和公用文件夹的限制的详细信息，请参阅以下主题：
<ul>
<li><p>若要了解 Office 365 中的公用文件夹，请参阅 <a href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online 限制</a>。</p></li>
<li><p>有关本地 Exchange Server 2013 中的公用文件夹的信息，请参阅<a href="limits-for-public-folders-exchange-2013-help.md">公用文件夹的限制</a>。</p></li>
</ul></td>
</tr>
</tbody>
</table>


有关与 Exchange Server 2013 中公用文件夹相关的其他管理任务，请参阅[公用文件夹程序](public-folder-procedures-exchange-2013-help.md)。

有关与 Exchange Online 中公用文件夹相关的其他管理任务，请参阅[Office 365 和 Exchange Online 中的公用文件夹程序](https://technet.microsoft.com/zh-cn/library/jj966272\(v=exchg.150\))。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：30 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[共享和协作权限](sharing-and-collaboration-permissions-exchange-2013-help.md)主题中的“公用文件夹”条目。

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

## 步骤 1：创建主公用文件夹邮箱

主公用文件夹邮箱包含一个公用文件夹层次结构和内容的可写副本，是为组织创建的第一个公用文件夹邮箱。后续公用文件夹邮箱将是辅助公用文件夹邮箱，将包含层次结构和内容的只读副本。

有关详细步骤，请参阅[创建公用文件夹邮箱](create-a-public-folder-mailbox-exchange-2013-help.md)。

## 步骤 2：创建第一个公用文件夹

有关详细步骤，请参阅[创建公用文件夹](create-a-public-folder-exchange-2013-help.md)。

## 步骤 3：分配对公用文件夹的权限

创建公用文件夹之后，您需要分配“所有者”权限级别，以便至少一个用户可以从客户端访问该公用文件夹并创建子文件夹。在此公用文件夹之后创建的所有公用文件夹都将继承父公用文件夹的权限。

1.  在 Exchange 管理中心 (EAC) 中，导航到“公用文件夹”\>“公用文件夹”。

2.  在列表视图中选择公用文件夹。

3.  在详细信息窗格中的“文件夹权限”下，单击“管理”。

4.  在“公用文件夹权限”中，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

5.  单击“浏览”选择用户。

6.  在“权限级别”列表中，选择一个级别。至少应有一个用户是“所有者”。

7.  单击“保存”。

8.  您可以通过单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 并使用以上步骤分配相应的权限来添加多个用户。您还可以通过选中或清除相应的复选框来自定义权限级别。编辑预定义的权限级别（如“所有者”）时，该权限级别将更改为“自定义”。

有关如何使用命令行管理程序分配公用文件夹权限的信息，请参阅 [Add-PublicFolderClientPermission](https://technet.microsoft.com/zh-cn/library/bb124743\(v=exchg.150\))。

## 步骤 4（可选）：已启用邮件的公用文件夹

如果希望用户将邮件发送到公用文件夹，您可以对公用文件夹启用邮件功能。此步骤是可选的。如果不对公用文件夹启用邮件功能，则用户可以通过从 Outlook 中将项目拖到公用文件夹来将邮件投递到其中。

1.  在 EAC 中，导航到“公用文件夹”\>“公用文件夹”。

2.  在列表视图中，选择要启用邮件的公用文件夹。

3.  在详细信息窗格中的“邮件设置 – 已禁用”下，单击“启用”。
    
    将显示警告，询问您是否确定要为公用文件夹启用邮件功能。单击“是”。

将为公用文件夹启用邮件功能，并且公用文件夹的名称将变为公用文件夹的别名。如果您具有多个使用该名称的收件人，则公用文件夹的别名将追加一个数字。例如，如果您有一个名为 SalesTeam 的通讯组，并创建一个名为 SalesTeam 的公用文件夹，然后对该公用文件夹启用邮件功能，则该公用文件夹的别名将是 SalesTeam1。

有关如何使用命令行管理程序为公用文件夹启用邮件的信息，请参阅 [Enable-MailPublicFolder](https://technet.microsoft.com/zh-cn/library/aa998824\(v=exchg.150\))。

