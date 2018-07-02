---
title: '创建邮箱审核日志搜索: Exchange 2013 Help'
TOCTitle: 创建邮箱审核日志搜索
ms:assetid: 48ba22cf-b1f2-4dbc-98fc-fed22d97db14
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff461929(v=EXCHG.150)
ms:contentKeyID: 50490472
ms.date: 01/28/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建邮箱审核日志搜索

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-11_

您可以创建邮箱审核日志搜索以对一个或多个邮箱进行异步搜索，并将搜索结果以 XML 文件的形式通过电子邮件发送至指定地址。

若要搜索单个邮箱的邮箱审核日志并在命令行管理程序中显示结果，请参阅[搜索邮箱邮箱审核日志](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md)。

关于邮箱审核日志记录的更多管理任务，请参阅[邮箱审核日志记录程序](mailbox-audit-logging-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“邮箱审核日志记录”条目。

  - 默认情况下，会为所有邮箱禁用邮箱审核日志记录。 对于要审核的每个邮箱，都必须启用审核日志记录，并指定要审核的邮箱所有者、代理人或管理员操作。 有关更多详细信息，请参阅[启用或禁用邮箱的邮箱审核日志记录](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)。

  - 无法使用 EAC 搜索所有者访问的邮箱审核日志。 EAC 中的审核部分包括非所有者邮箱访问的报告，同时还允许您搜索和导出非所有者访问事件。

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


## 您想执行什么操作？

## 使用 EAC 创建邮箱审核日志搜索

1.  导航到“合规性管理”\>“审核”。

2.  在列表视图中，选择“导出邮箱审核日志”。

3.  在“导出邮箱审核日志”中，填写下列字段，然后单击“导出”：
    
      - **开始日期**
    
      - **结束日期**
    
      - **搜索这些邮箱或保留为空，以查找所有非所有者访问的邮箱**
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>搜索所有邮箱可能需要较长时间，具体取决于您组织中的邮箱数量和每个邮箱中的邮箱审核日志数据量。</td>
        </tr>
        </tbody>
        </table>
    
      - **搜索以下人员的访问**
        
        从以下类型的访问事件中选择要搜索的访问：
        
          - **所有非所有者**
        
          - **外部用户**
        
          - **管理员和代理用户**
        
          - **管理员**
    
      - **将审核报告发送到**

## 使用命令行管理程序创建邮箱审核日志搜索

有关如何使用命令行管理程序创建邮箱审核日志搜索的示例，请参阅**New-MailboxAuditLogSearch**中的[Example 1](https://technet.microsoft.com/zh-cn/95365cab-bbb2-4a64-8e8f-1c89fa9e0352\(exchg.150\)#example1)。

