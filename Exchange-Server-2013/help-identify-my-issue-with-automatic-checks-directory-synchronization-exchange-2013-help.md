---
title: '通过自动检查帮助识别我的问题 - 目录同步: Exchange 2013 Help'
TOCTitle: 通过自动检查帮助识别我的问题 - 目录同步
ms:assetid: e6ea900a-c382-444c-a8ce-54d392bfeca3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn793977(v=EXCHG.150)
ms:contentKeyID: 62633062
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 通过自动检查帮助识别我的问题 - 目录同步

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

您可以使用下面的自动检查，以验证您的配置并帮助您更新环境。

如果您已经拥有 Office 365 用户帐户，请选择\&quot;登录\&quot;，而无需 Azure ID 帐户。在运行检查时，可能要求您再次输入用户帐户。如果是这样，您的用户帐户的格式为 username@youroffice365login.domain 和您的密码。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您收到同步警告消息中的 Office 365 门户、 同步服务器事件日志或从 Microsoft Online Services 的非正常运行目录同步通知电子邮件中的错误，可能会出现某种类型的目录同步问题。<a href="https://aka.ms/dsup">目录同步疑难解答</a>是基于 Web 的诊断工具，专门用于帮助标识同步失败的常见类型和制定有针对性的解决方案，对发现的任何问题。在目录同步服务器，必须运行目录同步疑难解答。</td>
</tr>
</tbody>
</table>


## 先决条件

我们将查看您是否安装了 Azure Active Directory 登录助理 和 用于 Windows PowerShell 的 Azure Active Directory 模块。

Azure Active Directory 登录助理有两个版本︰ [32 位](https://go.microsoft.com/fwlink/?linkid=286261)和[64 位](https://go.microsoft.com/fwlink/?linkid=286262)。

用于 Windows PowerShell 的 Azure Active Directory 模块有两个版本︰ [32 位](https://go.microsoft.com/fwlink/?linkid=286258)和[64 位](https://go.microsoft.com/fwlink/?linkid=286259)。

## 目录同步检查


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>应用程序</p></td>
<td><p>症状</p></td>
<td><p>检查</p></td>
</tr>
<tr class="even">
<td><p>目录同步</p></td>
<td><p>不确定我的 Active Directory 用户帐户是否符合目录同步的要求。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834884">运行此检查</a></p></td>
</tr>
<tr class="odd">
<td><p>目录同步</p></td>
<td><p>不确定我的 Active Directory 域功能级别是否正确设置为 Windows Server 2003 或更高版本。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">运行此检查</a></p></td>
</tr>
<tr class="even">
<td><p>目录同步</p></td>
<td><p>不确定目录同步是否发生在过去的三个小时内。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">运行此检查</a></p></td>
</tr>
<tr class="odd">
<td><p>目录同步</p></td>
<td><p>不确定我的 Active Directory 是否具有将阻止目录同步的任何重复用户属性。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834883">运行此检查</a></p></td>
</tr>
<tr class="even">
<td><p>目录同步</p></td>
<td><p>不确定 Office 365 中是否启用目录同步。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">运行此检查</a></p></td>
</tr>
<tr class="odd">
<td><p>目录同步</p></td>
<td><p>不确定我是否可以部署 Office 365 报价限制。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834920">运行此检查</a></p></td>
</tr>
<tr class="even">
<td><p>目录同步</p></td>
<td><p>不确定我是否可以部署 Office 365 和使用默认目录同步设置。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">运行此检查</a></p></td>
</tr>
<tr class="odd">
<td><p>目录同步</p></td>
<td><p>不确定我是否可以使用 Active Directory，并且支持目录同步。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834886">运行此检查</a></p></td>
</tr>
<tr class="even">
<td><p>目录同步</p></td>
<td><p>不确定所有我的 Active Directory 用户帐户是否符合目录同步的要求。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834913">运行此检查</a></p></td>
</tr>
</tbody>
</table>

