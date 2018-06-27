---
title: 'Exchange 服务器可支持性矩阵: Exchange 2013 Help'
TOCTitle: Exchange 服务器可支持性矩阵
ms:assetid: dbac2d40-da8b-469f-a265-1d1f948fe446
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff728623(v=EXCHG.150)
ms:contentKeyID: 54652303
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 服务器可支持性矩阵

 

_**适用于：**Exchange Server 2007, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2018-03-20_

Exchange Server 可支持性矩阵为 Microsoft Exchange 管理员提供了一个集中来源，以便于他们查找有关受支持 Microsoft Exchange 版本的任何配置或所需组件的可用支持级别信息。

## 发布模式

下表列出了每个受支持的 Exchange 版本的发布模式。发布模式由 X 字符标识。

对于 Exchange 2013 之前的 Exchange 版本，每个更新汇总包都针对整个产品进行累积。因此，如果将某个更新汇总包应用到 Exchange Server 2010，则将应用此更新汇总包中包含的所有修补程序。这包括每个早期更新汇总程序包中包含的所有修补程序。当针对早期版本的 Exchange 创建更新或修补程序时，将累积包括在更新或修补程序中的一个或多个二进制文件。即针对文件的内容进行累积。而不是针对整个 Exchange 产品进行累积。有关详细信息，请参阅 [Exchange 2010 服务](https://go.microsoft.com/fwlink/p/?linkid=298627)。

随着 Exchange 2013 的问世，我们改变了提供修补程序和 Service Pack 的方式。以前版本的Exchange 使用优先级驱动的修补程序版本和更新汇总模型，而现在 Exchange 2013 及更高版本采用的是计划交付模型。在此模型中，每三个月发布一次累积更新。Exchange 2013 及更高版本的累积更新 (CU) 是作为 Exchange 的完全更新版发行的，类似于产品升级或 Service Pack 版本。有关详细信息，请参阅 [Exchange 2013 更新](updates-for-exchange-2013-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>服务发布模式</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>累积更新</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>更新汇总</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>单独交付的安全修补程序</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 支持生命周期

有关 Exchange 或 MicrosoftWindows 服务器或客户端操作系统的特定版本的支持生命周期的详细信息，请参阅 [Microsoft 支持生命周期](https://go.microsoft.com/fwlink/p/?linkid=55839)页。有关 Microsoft 支持生命周期的详细信息，请参阅 [Microsoft 支持生命周期策略常见问题解答](https://go.microsoft.com/fwlink/p/?linkid=158902)。

## 停用 Exchange Server 2007

Exchange 2007到达末尾在 4 月 11，2017，每个[Microsoft 生命周期策略](https://go.microsoft.com/fwlink/p/?linkid=833210)上的支持。作为提醒，有该日期将没有新的安全更新后非安全更新、 释放或支付协助的支持选项或在线技术的内容更新。此外，如采用 Office 365 的加速和云使用增加，用于 Office 产品的自定义支持选项将不可用。这包括 Exchange Server 以及 Office 套件;SharePoint 服务器;办公通信服务器;Lync 服务器;Skype 业务服务器;Project Server，并且 Visio。达到的Exchange 2007支持日期结束，我们鼓励客户完成他们迁移和升级计划。我们建议客户能够利用部署软件保证部署和规划提供 Microsoft 和 Microsoft 认证合作伙伴包括[Microsoft FastTrack](https://go.microsoft.com/fwlink/p/?linkid=238431)云迁移和[的优点服务](https://go.microsoft.com/fwlink/p/?linkid=833211)内部升级。

## 受支持的操作系统平台

下表标识了可以运行每个 Exchange 版本的操作系统平台。支持的平台用 X 字符标识。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不支持下表中未列出的 Windows Server 和 Windows 客户端版本使用任何版本的 Exchange。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>操作系统平台</th>
<th>Exchange 2016 CU3 及更高版本</th>
<th>Exchange 2016 CU2 及更早版本</th>
<th>Exchange 2013 SP1 及更高版本</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Vista SP2</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 SP2</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 R2 SP1</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows 7 SP1</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
</tr>
<tr class="odd">
<td><p>Windows 8</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>Windows 8.1</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Windows 10</p></td>
<td><p>X1</p></td>
<td><p>X1</p></td>
<td><p></p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2016</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


1仅适用于 Exchange 管理工具

## 受支持的 Active Directory 环境

下表标识了每个 Exchange 版本可与之通信的操作 Active Directory 环境。支持的环境用 X 字符标识。Active Directory 服务器指的是可写的全局编录服务器和可写的域控制器。不支持只读全局编录服务器和只读域控制器。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>操作系统环境</th>
<th>Exchange 2016 CU3 及更高版本</th>
<th>Exchange 2016 CU2 及更早版本</th>
<th>Exchange 2013 SP1 及更高版本</th>
<th>Exchange 2010 SP3 RU5 或更高版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2003 SP2 Active Directory 服务器</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 SP2 Active Directory 服务器</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 R2 SP1 Active Directory 服务器</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012 Active Directory 服务器</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2 Active Directory 服务器</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2016 Active Directory 服务器</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>林功能级别</th>
<th>Exchange 2016 CU3 及更高版本</th>
<th>Exchange 2016 CU2 及更早版本</th>
<th>Exchange 2013 SP1 及更高版本</th>
<th>Exchange 2010 SP3 RU5 或更高版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Server 2003 林功能级别</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 林功能级别</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008 R2 SP1 林功能级别</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012 林功能级别</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012 R2 林功能级别</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2016 林功能级别</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 支持与 Outlook Web App 或 Web 上的 Outlook 高级版本一起使用的 Web 浏览器

下表标识出支持与 Outlook Web App 或 Web 上的 Outlook 高级版本一起使用的 Web 浏览器。支持的浏览器用 X 字符标识。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>浏览器</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 及更高版本</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Microsoft Edge 的当前版本</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Internet Explorer 的当前版本或上一个版本</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Firefox</p></td>
<td><p>Firefox 的当前版本或上一个版本</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>Firefox 3.0.1 或更高版本</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Firefox 12 或更高版本</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Safari</p></td>
<td><p>Safari 的当前版本</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
</tr>
<tr class="even">
<td><p>Safari 3.1 或更高版本</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Safari 5.0 或更高版本</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome</p></td>
<td><p>Chrome 的当前版本</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>Chrome 3.0.195 或更高版本</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome 18 或更高版本</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## 支持与 Outlook Web App 或 Web 上的 Outlook 基本版本一起使用的 Web 浏览器

下表标识出支持与 Outlook Web App 或 Web 上的 Outlook 精简（基本）版本一起使用的 Web 浏览器。支持的浏览器用 X 字符标识。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Outlook Web App Basic (Outlook Web App Light) 支持在移动浏览器中使用。但是，如果在移动浏览器中出现呈现或验证问题，请确定在支持的浏览器的完整客户端中是否可使用 Outlook Web App Light 再现该问题。例如，在 Safari、Chrome 或 Internet Explorer 中测试使用 Outlook Web App Light。如果无法在完整客户端中再现问题，我们建议您联系移动设备供应商获得帮助。在这些情况下，我们根据情况与供应商合作。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>浏览器</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Microsoft Edge 的当前版本</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Internet Explorer 的当前版本或上一个版本</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X<span></span></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td><p> </p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Safari</p></td>
<td><p>Safari 的当前版本</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Firefox</p></td>
<td><p>Firefox 的当前版本或上一个版本</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Chrome</p></td>
<td><p>Chrome 的当前版本</p></td>
<td><p>N/A</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>Opera</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## 支持将 S/MIME 与 Outlook Web App 或 Web 上的 Outlook 一起使用的 Web 浏览器

下表标识出将 S/MIME 与 Outlook Web App 或 Web 上的 Outlook 一起使用的 Web 浏览器。支持的浏览器用 X 字符标识。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>浏览器</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 及更高版本</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Edge</p></td>
<td><p>Microsoft Edge 的当前版本</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer</p></td>
<td><p>Internet Explorer 的当前版本或上一个版本</p></td>
<td><p>N/A</p></td>
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 11</p></td>
<td> </td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 10</p></td>
<td> </td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 9</p></td>
<td> </td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Internet Explorer 8</p></td>
<td> </td>
<td><p></p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Internet Explorer 7</p></td>
<td> </td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## 客户端

下表标识了支持与每个 Exchange 版本一起使用的邮箱客户端。支持的客户端用 X 字符标识。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 及更高版本</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p></p></td>
<td><p>X1</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2010</p></td>
<td><p>X4</p></td>
<td><p>X2</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2016</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>适用于 Office 365 的 Outlook for Mac</p></td>
<td><p>X4</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Phone 7.5</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Phone 8</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Windows Phone 8.1</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Mobile 10</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>Entourage 2008 (EWS)</p></td>
<td><p>X3</p></td>
<td><p>X3</p></td>
<td><p>X3</p></td>
</tr>
</tbody>
</table>


1需要 Outlook 2007 Service Pack 3 和公用的最新更新。

2需要 Outlook 2010 Service Pack 1 和公用的最新更新。

3仅 EWS。没有为Exchange 2010DAV 支持。

4支持最新的 Office service pack 和公共更新。

## 工具

下表标识了可以与 Microsoft Exchange 的组织间复制工具（Exscfg.exe、Exssrv.exe）一起使用的 Microsoft Exchange 版本。此工具用于在 Exchange 组织间复制公用文件夹信息（包括闲/忙信息）。有关详细信息，请参阅 [Microsoft Exchange Server 组织间复制](https://go.microsoft.com/fwlink/?linkid=22455)。支持的版本用 X 字符标识。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>工具</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 及更高版本</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>组织间复制工具</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Microsoft .NET Framework

下表标识了可与每个 Exchange 版本一起使用的 Microsoft.NET Framework 版本。支持的版本用 X 字符标识。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>任何版本的 Exchange 都不支持下表中未列出的 .NET Framework 版本。</strong>这包括 .NET Framework 的次要版本和修补级别版本。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不受支持的 CU Exchange 升级到当前的 CU 和任何中间 CUs 可用时，您应升级到最新版本的.NET 支持的第一个，然后立即升级到当前的 CU 的交换。此方法不是取代需要跟您的 Exchange 服务器上，到目前为止，在最新的支持的 CU。<br />
Microsoft 不做任何评论，升级失败不会使用这种方法，这可能会导致与 Microsoft 支持服务的需要。</td>
</tr>
</tbody>
</table>



<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>.NET Framework</th>
<th>交换 2016 CU8</th>
<th>交换 2016 CU5-CU7</th>
<th>交换 2013 CU19</th>
<th>交换 2013 CU16-CU18</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>.NET Framework 3.5</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p>X1</p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 3.5 SP1</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>.NET Framework 4.0</p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1,2</p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 4.5</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X1,2 </p></td>
</tr>
<tr class="odd">
<td><p>.NET Framework 4.6.2</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>.NET Framework 4.7.1</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


1 如果你使用的是 Windows Server 2012，则必须先安装 .NET Framework 3.5，然后才能使用 Exchange 2010 SP3。

2 Exchange 2010 仅使用 .NET .NET Framework 3.5 和 .NET .NET Framework 3.5 SP1 库。如果已安装在计算机上，则不会使用 .NET .NET Framework 4.5 库。我们支持安装 .NET .NET Framework 4.5 的任何主要或次要版本（例如，.NET .NET Framework 4.5.1, .NET .NET Framework 4.5.2 等），前提是 .NET .NET Framework 3.5 或.NET .NET Framework 3.5 SP1 也安装在计算机上。

## Windows 管理框架

下表标识了可与每个 Exchange 版本一起使用的 Windows Management Framework 版本，其中包含 Windows PowerShell 命令行界面。支持的版本用 X 字符标识。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows PowerShell</th>
<th>Exchange 2016</th>
<th>Exchange 2013</th>
<th>Exchange 2010</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows PowerShell 2.0</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Management Framework</p></td>
<td><p>Windows Management Framework 版本内置于你在其上安装 Exchange 的 Windows Server 的发布版本中。</p></td>
<td><p>Windows Management Framework 版本内置于你在其上安装 Exchange 的 Windows Server 的发布版本中。</p></td>
<td><p>Windows Management Framework 版本内置于你在其上安装 Exchange 的 Windows Server 的发布版本中。1</p></td>
</tr>
</tbody>
</table>


1在运行 Exchange 2010 SP3 RU5 或更高版本的计算机上，Windows Management Framework 3.0 和 Windows Management Framework 4.0 可用于执行与操作系统相关的管理任务。但是，Exchange 2010 cmdlet 和 Exchange 2010 脚本需要 Windows PowerShell 2.0。不支持将 Exchange 2010 cmdlet 和脚本与 Windows Management Framework 3.0 或 Windows Management Framework 4.0 一起使用。

## Microsoft 管理控制台

下表标识了可与每个 Exchange 版本一起使用的 Microsoft 管理控制台 (MMC) 版本。支持的版本用 X 字符标识。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>MMC</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 或更高版本</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MMC 3.0</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


## Windows Installer

下表标识了能够与每个 Exchange 版本一起使用的 Windows Installer 版本。支持的版本用 X 字符标识。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows Installer</th>
<th>Exchange 2016</th>
<th>Exchange 2013 SP1 及更高版本</th>
<th>Exchange 2010 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Installer 4.5</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Installer 5.0</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

