---
title: '设置队列查看器选项: Exchange 2013 Help'
TOCTitle: 设置队列查看器选项
ms:assetid: 03a9134c-0714-4c13-b286-92bccc7ec05e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa995934(v=EXCHG.150)
ms:contentKeyID: 50489847
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 设置队列查看器选项

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2012-10-03_

可以在队列查看器中设置选项，以调整页面上显示的项目数，并调整自动刷新间隔。自动刷新间隔用于确定队列查看器中结果的更新频率。

## 在开始之前，您需要知道什么？

  - 估计完成时间：10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“队列”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用 Exchange 工具箱设置队列查看器选项

1.  单击“开始”\>“所有程序”\>“Microsoft Exchange Server 2013”\>“Exchange 工具箱”。

2.  在“邮件流工具”下，双击“队列查看器”。

3.  在“队列查看器”中，单击“查看”\>“选项”，以在“队列查看器选项”对话框中配置以下设置：
    
    1.  在“刷新间隔(秒)”字段中，输入队列查看器应当更新显示的频率。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>默认的自动刷新间隔是 30 秒，并且不能设置为更短的时间。如果通过在“队列查看器选项”页上清除“自动刷新屏幕”复选框禁用了自动刷新功能，则必须单击“刷新”才能手动更新队列查看器中显示的结果。</td>
        </tr>
        </tbody>
        </table>
    
    2.  在“每页显示的项目数”字段中，输入可在队列查看器中显示的最大项目数。此数字必须在 1 到 10,000 之间。如果项目数超过限制，则将以最大项目数分组显示这些项目。例如，下图显示了一个包含 14 个邮件的队列，其队列查看器配置为每页显示 10 个项目。对象数显示在该页的右上方。在该页的底部，您可以看到队列中的总项目数。您可以使用导航控件查看队列中的其他项目。

4.  完成后，单击“确定”。
    
    **队列查看器**
    
    ![项目超过项目限制的队列查看器](images/Aa995934.e82196e6-002a-4e9e-823d-b244b0bd25e2(EXCHG.150).gif "项目超过项目限制的队列查看器")  

## 您如何知道这有效？

如果队列查看器使用刷新间隔和每页项目数设置，则表明此过程有效。

