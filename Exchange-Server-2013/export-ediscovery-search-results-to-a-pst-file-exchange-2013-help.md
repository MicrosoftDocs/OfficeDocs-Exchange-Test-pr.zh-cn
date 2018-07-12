---
title: '将电子数据展示搜索结果导出到 PST 文件: Exchange Online Help'
TOCTitle: 将电子数据展示搜索结果导出到 PST 文件
ms:assetid: bc47f5f9-d056-4b69-b669-ae65fad541c8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn440164(v=EXCHG.150)
ms:contentKeyID: 59636322
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 将电子数据展示搜索结果导出到 PST 文件

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2017-09-07_

可以使用在Exchange 管理中心 (EAC) eDiscovery 导出工具将适当 eDiscovery 搜索的结果导出到 Outlook 数据文件，也称为 PST 文件。管理员可以分配到您的组织，如人力资源经理或记录管理器内的其他人员或相反法律顾问在法律案件中的搜索结果。搜索结果导出到 PST 文件之后，您或其他用户可以它们在 Outlook 中打开要查看或打印搜索结果中返回的消息。也可以在第三方 eDiscovery 和报告应用程序中打开 PST 文件。本主题演示如何执行此操作，以及解决如果您有任何问题。

## 在开始之前，您需要知道什么？

  - 估计完成时间：时间将依据要导出的搜索结果的数量和大小发生变化。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;就地电子数据展示\&quot;条目。

  - 若要将搜索结果导出到 PST 文件的计算机必须满足以下系统要求：
    
      - 32 位或 64 位版本的 Windows 7 和更高版本
    
      - Microsoft.NET Framework 4.7
    
      - 支持的浏览器：
        
          - Internet Explorer 10 和更高版本
            
            或者
        
          - Mozilla Firefox 或 Google Chrome。如果你使用上述浏览器之一，请确保安装 *ClickOnce* 扩展。若要安装 ClickOnce 外接程序，请参阅 [Mozilla ClickOnce 外接程序](https://addons.mozilla.org/zh-cn/firefox/search/?q=clickonce%26cat=1%2c0%26appver=%26platform=)或 [ClickOnce for Google Chrome](https://chrome.google.com/webstore/search/clickonce?_category=extensions)。

  - 您需要将活动邮箱连接到您希望导出的帐户。

  - 确保 Internet Explorer 中已正确设置本地 Intranet 设置。确保 **https://\*.outlook.com** 已添加到本地 Intranet 区域中。

  - 确保在受信任的站点区域中没有列出以下 URL：
    
      - https://\*.outlook.com
    
      - https://r4.res.outlook.com
    
      - https://\*.res.outlook.com

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用 Exchange 管理中心 将就地电子数据展示搜索结果导出到 PST

1.  转到\&quot;合规性管理\&quot;\>\&quot;就地电子数据展示和保留\&quot;。

2.  在列表视图中，选择要导出结果的就地电子数据展示搜索，然后单击\&quot;导出到 PST 文件\&quot;。
    
    ![导出到 PST 文件](images/Dn440164.1ebee2ac-89b3-49fa-b70c-a07c9a65f958(EXCHG.150).gif "导出到 PST 文件")  

3.  在\&quot;电子数据展示 PST 导出工具\&quot;窗口中，执行以下操作：
    
      - 单击\&quot;浏览\&quot;指定要下载 PST 文件的位置。
    
      - 单击\&quot;启用重复数据删除\&quot;复选框来排除重复的邮件。PST 文件只会包括邮件的单个实例。
    
      - 单击\&quot;包括不可搜索的项目\&quot;复选框以包括无法搜索的邮箱项目（例如，带无法被 Exchange 搜索编入索引的文件类型附件的邮件）。不可搜索的项目会被导出到一个单独的 PST 文件中。
        
        > [!IMPORTANT]  
        > 如果邮箱包含大量不可搜索的项目，在导出电子数据展示搜索结果时包括不可搜索的项目将需要更长时间。为了减少导出搜索结果所需的时间，并防止出现大型 PST 导出文件，请考虑以下建议：
        > <ul>
        > <li><p>创建多个电子数据展示搜索，每个搜索负责搜索较少数量的源邮箱。</p></li>
        > <li><p>如果您导出特定日期范围内的所有邮箱内容（但未在搜索条件中指定任何关键字），则该日期范围内的所有不可搜索项目都将自动包含在搜索结果中。因此，请不要选中&amp;quot;包括不可搜索的项目&amp;quot;复选框。</p></li>
        > </ul>


4.  单击\&quot;开始\&quot;将搜索结果导出到 PST 文件。
    
    将显示一个窗口，其中包含有关导出过程的状态信息。

## 详细信息

  - 可以减小 PST 导出文件的大小，方法就是仅导出不可搜索的项目。为此，请创建或编辑搜索，指定一个将来的开始日期，然后删除\&quot;**关键字**\&quot;框中的任何关键字。这将导致不返回任何搜索结果。当你复制或导出搜索结果并选中\&quot;**包括不可搜索的项目**\&quot;复选框时，仅不可搜索的项目会复制到发现邮箱或导出到 PST 文件。

  - 如果您启用了重复数据删除，所有搜索结果都会被导出到一个 PST 文件中。如果不启用重复数据删除，则会针对搜索中包括的每个邮箱导出一个单独的 PST 文件。此外，如上所述，不可搜索的项目将被导出到一个单独的 PST 文件中。

  - 除了包含搜索结果的 PST 文件，还会导出其他两个文件：
    
      - 一个包含有关 PST 导出请求的信息的配置文件（.txt 文件格式），如导出的电子数据展示搜索的名称、导出的日期和时间、是否启用了重复数据删除和不可搜索项目、搜索查询，以及搜索的源邮箱。
    
      - 一个搜索结果日志(.csv 文件格式），其中包含搜索结果中返回的对应于每个邮件的条目。每个条目都标识邮件所在的源邮箱。如果已启用了重复数据删除，这有助于您确定包含重复邮件的所有邮箱。

  - 搜索名称是每个导出文件的文件名的第一部分。此外，导出请求的日期和时间将被附加到每个 PST 文件的文件名和结果日志中。

  - 有关重复数据删除和不可搜索项目的详细信息，请参阅：
    
      - [Estimate, preview, and copy search results](in-place-ediscovery-exchange-2013-help.md)
    
      - [Exchange 电子数据展示中不可搜索的项目](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

  - 若要从 SharePoint 或 SharePoint Online 中的电子数据展示中心导出电子数据展示搜索结果，请参阅[导出电子数据展示内容和创建报告](https://go.microsoft.com/fwlink/p/?linkid=324757)。

## 疑难解答


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>症状</th>
<th>可能的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>无法导出到 PST 文件。</p></td>
<td><ul>
<li><p>没有连接到帐户的活动邮箱。若要导出 PST，您必须拥有活动帐户。</p></li>
<li><p>您的 Internet Explorer 版本已过期。请尝试将 IE 版本更新到 10 或更高版本。或尝试使用其他浏览器。</p></li>
<li><p>&amp;quot;基于条件筛选&amp;quot;查询中输入的搜索条件不正确。例如，输入了用户名而不是电子邮件地址。有关如何基于条件筛选的详细信息，请参阅<a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">修改就地电子数据展示搜索</a>。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>无法导出特定计算机上的搜索结果。在另一台计算机上按预期导出工作项。</p></td>
<td><p>&amp;quot;凭据管理器&amp;quot;中保存的 Windows 凭据不正确。清除您的凭据，然后再次登录。</p></td>
</tr>
<tr class="odd">
<td><p>电子数据展示 PST 导出工具无法启动。</p></td>
<td><p>Internet Explorer 中未正确设置本地 Intranet 区域设置。请确保已将 *.outlook.com、*.office365.com、*.sharepoint.com 和 *.onmicrosoft.com 添加到本地 Intranet 区域受信任的站点。</p>
<p>若要将这些站点添加到 IE 中受信任的区域，请参阅<a href="https://windows.microsoft.com/zh-cn/windows/security-zones-adding-removing-websites#1tc=windows-7">安全区域：添加或删除网站</a>。</p></td>
</tr>
</tbody>
</table>

