---
title: '从队列查看器中导出列表: Exchange 2013 Help'
TOCTitle: 从队列查看器中导出列表
ms:assetid: dcb829cd-0ffd-4ea9-ac3e-eaac5a8d1194
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb691328(v=EXCHG.150)
ms:contentKeyID: 50491785
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 从队列查看器中导出列表

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2012-09-25_

该主题说明了如何使用 Exchange 工具箱中的队列查看器导出邮件或队列列表。

可以将列表导出为下列文件格式：

  - 文本文件（制表符分隔）

  - 文本文件（逗号分隔）

  - Unicode 文本文件（制表符分隔）

  - Unicode 文本文件（逗号分隔）

## 在开始之前，您需要知道什么？

  - 估计完成时间：10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“队列”条目。

  - 默认情况下，队列查看器中的结果窗格仅显示前 1,000 个对象。 若要更改该值，请参阅[设置队列查看器选项](set-queue-viewer-options-exchange-2013-help.md)。

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


## 从队列查看器中的结果窗格中导出列表

1.  单击“开始”\>“所有程序”\>“Microsoft Exchange 2013”\>“Exchange 工具箱”。

2.  在“邮件流”部分下，双击“队列查看器”。

3.  在队列查看器中，选择“队列”选项卡或“邮件”选项卡。 在任一选项卡上，单击“创建筛选器”来限制结果。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果结果窗格未刷新，请在操作窗格中单击“刷新”。 长列表刷新可能需要几分钟。</td>
    </tr>
    </tbody>
    </table>


4.  在操作窗格中，单击“导出列表”。 此时将出现“导出列表”对话框。

5.  在“导出列表”中，在“文件名称”框中键入文件的名称，然后从“保存类型”列表中选择文件格式。

6.  单击“保存”。

