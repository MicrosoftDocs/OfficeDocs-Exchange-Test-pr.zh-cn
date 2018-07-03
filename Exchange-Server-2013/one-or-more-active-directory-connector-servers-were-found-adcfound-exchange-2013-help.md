---
title: '一个或多个 Active Directory 连接器服务器已找到 (_ADCFound): Exchange 2013 Help'
TOCTitle: 一个或多个 Active Directory 连接器服务器已找到 (_ADCFound)
ms:assetid: a874f51f-09a2-4a76-9695-d61fb1ee6c1c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.adcfound(v=EXCHG.150)
ms:contentKeyID: 50491352
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 一个或多个 Active Directory 连接器服务器已找到 (\_ADCFound)

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-15_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为在当前 Microsoft Exchange 环境中发现了一个或多个 Active Directory 连接器 (ADC)，所以 Microsoft Exchange Server 2007 和 Exchange Server 2010 安装程序无法继续进行。

ADC 在混合模式的 Microsoft Exchange 环境中，将对象从 Exchange Server 版本 5.5 复制到 Active Directory 目录服务，而 Exchange 2007 或 Exchange 2010 并不支持此行为。

Exchange 2007 或 Exchange 2010 安装程序要求删除所有 ADC 组件。

要解决此问题，请删除所有 ADC 组件，并重新运行 Exchange 2007 或 Exchange 2010 安装程序。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>删除 Active Directory 连接器组件</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>要在运行 ADC 服务的服务器上禁用 ADC 服务，请在桌面上用鼠标右键单击&amp;quot;我的电脑&amp;quot;，再单击&amp;quot;管理&amp;quot;。</p></li>
<li><p>展开&amp;quot;服务和应用程序&amp;quot;节点，再单击&amp;quot;服务&amp;quot;节点。</p></li>
<li><p>在右侧窗格中，用鼠标右键单击&amp;quot;Microsoft Active Directory 连接器&amp;quot;，然后单击&amp;quot;属性&amp;quot;。</p></li>
<li><p>将<strong>启动类型</strong>更改为<strong>禁用</strong>。下次计算机启动时，将无法启动 ADC 服务。</p></li>
<li><p>单击&amp;quot;应用&amp;quot;，然后单击&amp;quot;确定&amp;quot;。</p></li>
<li><p>要卸载 ADC 服务，请使用 Microsoft Exchange 2000 Server 或 Microsoft Exchange Server 2003年光盘上的 Active Directory 安装向导。打开 \ADC\I386 文件夹，然后双击 Setup.exe 程序。按照提示<strong>删除所有</strong>ADC 服务组件。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>第 6 步，并<strong>删除所有</strong>ADC 组件来解决此问题，您必须完成。若要禁用 ADC 服务不足。</td>
</tr>
</tbody>
</table>

</li>
</ol></td>
</tr>
</tbody>
</table>


有关 ADC 的详细信息，请参阅下列 Microsoft 知识库文章：

  - 325300，"支持网络广播︰ 活动目录连接器简介"([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325300](https://go.microsoft.com/fwlink/?linkid=3052&kbid=325300))。

  - 325221，"支持网络广播︰ Microsoft 高级 Active Directory 连接符"([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325221](https://go.microsoft.com/fwlink/?linkid=3052&kbid=325221))。

  - 312632，"如何安装和配置 Exchange 2000 Server 中的活动目录连接器"([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=312632](https://go.microsoft.com/fwlink/?linkid=3052&kbid=312632))。

