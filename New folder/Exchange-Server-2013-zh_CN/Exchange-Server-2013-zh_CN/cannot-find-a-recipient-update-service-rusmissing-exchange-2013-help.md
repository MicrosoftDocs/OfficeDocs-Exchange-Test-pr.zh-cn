---
title: '找不到收件人更新服务 (_RUSMissing): Exchange 2013 Help'
TOCTitle: 找不到收件人更新服务 (_RUSMissing)
ms:assetid: 920fbf51-d5e4-4ac6-869f-7f1c5d9a3024
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.rusmissing(v=EXCHG.150)
ms:contentKeyID: 50491173
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 找不到收件人更新服务 (\_RUSMissing)

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-15_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为无法找到在现有 Exchange 组织中负责域的收件人更新服务 (RUS)，所以 Microsoft® Exchange Server 2007 或 Exchange Server 2010 安装程序无法继续进行。

Microsoft Exchange 安装程序要求现有 Exchange 组织中的每个域都有一个收件人更新服务实例。

如果某个域丢失了收件人更新服务实例，则在域中创建的新用户对象将不会收到发送给它们的电子邮件地址。

若要解决此问题，请验证每个域是否存在收件人更新服务的一个实例，同时为没有实例的域创建一个收件人更新服务实例，然后重新运行 Microsoft Exchange 安装程序。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>为域创建收件人更新服务实例</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>打开 Exchange 系统管理器。</p></li>
<li><p>展开&amp;quot;收件人&amp;quot;。</p></li>
<li><p>用鼠标右键单击&amp;quot;收件人更新服务&amp;quot;节点，单击&amp;quot;新建&amp;quot;，然后单击&amp;quot;收件人更新服务&amp;quot;。</p></li>
<li><p>在&amp;quot;新建对象&amp;quot;窗口中，单击&amp;quot;浏览&amp;quot;查找该域的名称。</p></li>
<li><p>选中该域的名称，然后单击&amp;quot;确定&amp;quot;。</p></li>
<li><p>在&amp;quot;新建对象&amp;quot;窗口中，单击&amp;quot;下一步&amp;quot;，然后单击&amp;quot;完成&amp;quot;。</p></li>
</ol></td>
</tr>
</tbody>
</table>


有关收件人更新服务的详细信息，请参阅下列 Microsoft 知识库文章：

  - "如何收件人更新服务应用收件人策略"([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=328738](https://go.microsoft.com/fwlink/?linkid=3052&kbid=328738))。

  - "如何收件人更新服务填充地址列表"([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253828](https://go.microsoft.com/fwlink/?linkid=3052&kbid=253828))。

  - "如何检查进度的 Exchange 收件人更新服务"([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=246127](https://go.microsoft.com/fwlink/?linkid=3052&kbid=246127))。

  - "任务执行的 Exchange 收件人更新服务"([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253770](https://go.microsoft.com/fwlink/?linkid=3052&kbid=253770))。

