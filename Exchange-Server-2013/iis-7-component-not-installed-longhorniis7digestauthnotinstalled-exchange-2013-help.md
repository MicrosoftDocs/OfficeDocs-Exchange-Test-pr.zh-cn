﻿---
title: 'IIS 7 组件未安装 (_LonghornIIS7DigestAuthNotInstalled): Exchange 2013 Help'
TOCTitle: IIS 7 组件未安装 (_LonghornIIS7DigestAuthNotInstalled)
ms:assetid: 5c0523d3-f1ba-4197-9c9f-715673dc1436
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.longhorniis7digestauthnotinstalled(v=EXCHG.150)
ms:contentKeyID: 50490644
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IIS 7 组件未安装 (\_LonghornIIS7DigestAuthNotInstalled)

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2015-03-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

由于未安装所需 Internet 信息服务 (IIS) 7 组件，Microsoft Exchange Server 2010 安装程序或 Microsoft Exchange Server 2007 安装程序无法在基于 Microsoft Windows Server 2008 的计算机或基于 Windows Server 2008 R2 的计算机上安装客户端访问服务器 (CAS) 角色或邮箱服务器角色。

Exchange 2010 安装程序和 Exchange 2007 安装程序需要您安装 CAS 角色的基于 Windows Server 2008 的计算机或基于 Windows Server 2008 R2 的计算机装有以下 IIS 7 组件。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>CAS 服务器角色所需的 IIS 7 组件</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>动态内容压缩</p></td>
</tr>
<tr class="even">
<td><p>静态内容压缩</p></td>
</tr>
<tr class="odd">
<td><p>基本身份验证</p></td>
</tr>
<tr class="even">
<td><p>Windows 身份验证</p></td>
</tr>
<tr class="odd">
<td><p>IIS 7 摘要式身份验证</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET</p></td>
</tr>
<tr class="odd">
<td><p>客户端证书映射</p></td>
</tr>
<tr class="even">
<td><p>目录浏览</p></td>
</tr>
<tr class="odd">
<td><p>HTTP 错误</p></td>
</tr>
<tr class="even">
<td><p>HTTP 日志记录</p></td>
</tr>
<tr class="odd">
<td><p>HTTP 重定向</p></td>
</tr>
<tr class="even">
<td><p>跟踪</p></td>
</tr>
<tr class="odd">
<td><p>ISAPI 筛选器</p></td>
</tr>
<tr class="even">
<td><p>请求监视器</p></td>
</tr>
<tr class="odd">
<td><p>静态内容</p></td>
</tr>
</tbody>
</table>


Exchange 2010 安装程序和 Exchange 2007 安装程序需要您安装邮箱服务器角色的基于 Windows Server 2008 的计算机或基于 Windows Server 2008 R2 的计算机装有以下 IIS 7 组件。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>邮箱服务器角色所需的 IIS 7 组件</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>基本身份验证</p></td>
</tr>
<tr class="even">
<td><p>Windows 身份验证</p></td>
</tr>
</tbody>
</table>


若要解决此问题，请遵照相应步骤来安装所需 IIS 7 组件到目标计算机，然后再次运行 Microsoft Exchange 安装程序。

**使用 Windows Server 2008 服务器管理器为 CAS 服务器角色安装 IIS 7 组件。**

1.  依次单击“开始”、“管理工具”和“服务器管理器”。

2.  在导航窗格中，展开“角色”，右键单击“Web 服务器 (IIS)”，然后单击“添加角色服务”。

3.  在“选择角色服务”窗格上，向下滚动到“IIS”。

4.  在“**安全**”区域，单击以选中以下复选框：
    
      - **基本身份验证**
    
      - **摘要式身份验证**
    
      - **Windows 身份验证**

5.  在“**性能**”区域，单击以选中以下复选框：
    
      - **静态压缩**
    
      - **动态压缩**

6.  在“选择角色服务”窗格中，单击“下一步”，然后单击“确认安装选择”窗格中的“安装”。

7.  单击“关闭”退出“添加角色服务”向导。

**使用 Windows Server 2008 服务器管理器为邮箱服务器角色安装 IIS 7 组件。**

1.  依次单击“开始”、“管理工具”和“服务器管理器”。

2.  在导航窗格中，展开“角色”，右键单击“Web 服务器 (IIS)”，然后单击“添加角色服务”。

3.  在“选择角色服务”窗格上，向下滚动到“IIS”。

4.  在“**安全**”区域，单击以选中以下复选框：
    
      - **基本身份验证**
    
      - **Windows 身份验证**

5.  在“选择角色服务”窗格中，单击“下一步”，然后单击“确认安装选择”窗格中的“安装”。

6.  单击“关闭”退出“添加角色服务”向导。

