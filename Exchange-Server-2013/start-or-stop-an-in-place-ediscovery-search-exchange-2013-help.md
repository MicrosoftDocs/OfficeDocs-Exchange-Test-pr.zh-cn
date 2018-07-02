---
title: '启动或停止就地电子数据展示搜索: Exchange Online Help'
TOCTitle: 启动或停止就地电子数据展示搜索
ms:assetid: 0d546763-4bf5-4523-91f4-d181b7ee4ac2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335090(v=EXCHG.150)
ms:contentKeyID: 50489985
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启动或停止就地电子数据展示搜索

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2014-07-14_

可以随时停止或重新启动就地电子数据展示搜索。例如，如果要修改搜索的关键字或邮箱等搜索属性，必须首先停止搜索。在做出所需的更改后，即可重新开始搜索。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果重新启动就地电子数据展示搜索，则会删除复制到搜索中指定的发现邮箱的搜索结果。</td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;就地电子数据展示\&quot;条目。

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

## 使用 EAC 启动或停止就地电子数据展示搜索

1.  导航到\&quot;合规性管理\&quot;\>\&quot;就地电子数据展示和保留\&quot;。

2.  若要停止正在进行的搜索，请选择该搜索，然后单击\&quot;停止搜索\&quot;。

3.  若要启动停止的搜索，请选择该搜索，然后单击\&quot;恢复搜索\&quot;。

## 使用命令行管理程序启动或停止就地电子数据展示搜索

有关如何启动就地电子数据展示搜索的示例，请参阅 [Start-MailboxSearch](https://technet.microsoft.com/zh-cn/library/dd351245\(v=exchg.150\)) 中的\&quot;示例 1\&quot;。

有关如何停止就地电子数据展示搜索的示例，请参阅 [Stop-MailboxSearch](https://technet.microsoft.com/zh-cn/library/dd351075\(v=exchg.150\)) 中的\&quot;示例 1\&quot;。

