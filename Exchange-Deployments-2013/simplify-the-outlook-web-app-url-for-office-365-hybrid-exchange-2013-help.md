---
title: '为 Office 365 混合简化 Outlook Web App URL: Exchange 2013 Help'
TOCTitle: 为 Office 365 混合简化 Outlook Web App URL
ms:assetid: 19449aee-3796-4298-90c6-c7579b8d2f7a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt791749(v=EXCHG.150)
ms:contentKeyID: 74259162
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为 Office 365 混合简化 Outlook Web App URL

 

_**上一次修改主题：** 2016-11-11_

了解如何在混合环境中为云邮箱用户配置 Web 上的 Outlook (Outlook Web App) URL。

对于从本地 Exchange 迁移到 Office 365 的组织，主要关注的是用户体验。用户需要的是邮箱访问不受中断，无论邮箱在何时被移动到何处。考虑到这一点，Web 上的 Outlook（旧称“Outlook Web App”）共存情景很重要。

假设应用场景如下：某公司使用混合部署将一些邮箱从本地 Exchange 迁移到 Office 365。在迁移前的星期五，用户使用 URL https://mail.contoso.com/owa 访问本地邮箱。在迁移后的星期一，相同用户尝试使用该 URL 访问邮箱时却看到了错误消息。

为了让受影响的用户可以使用 Web 上的 Outlook连接邮箱，可以采用下列两种方式之一：

  - **告诉用户新 URL（例如，https://outlook.com/owa/contoso.com）**   这种方式存在以下问题：
    
      - URL 非常复杂。
    
      - 受影响的用户无法获得顺畅体验。

  - **在组织关系上配置 TargetOWAUrl 设置**   这种方式存在以下问题：
    
      - 云邮箱的终结点在外部（并不在用户所需的域中）。
    
      - 终结点需要在 URL 中指定域（以区分 Office 365 商业服务和 outlook.com 使用者服务）。
    
      - 终结点导致用户看到证书不匹配警告。

若要为有云邮箱的用户解决这些问题，请按以下步骤操作：

1.  **在 DNS 中创建指向 mail.office365.com 的 CNAME 记录（例如，cloudowa.contoso.com）**
    
      - 请务必在内部和外部（公共）DNS 中创建此 CNAME 记录，因为用户可能会通过内部或外部 Internet 连接进行连接。
    
      - 在我们的示例中，请求中使用的是域 contoso.com（舍弃了 cloudowa 部分）。也就是说，无需在 URL 中指定域。

2.  **在本地组织关系中配置 Web 上的 Outlook重定向**   为此，请在本地 Exchange 的 Exchange 命令行管理程序中使用以下语法：
    
        Set-OrganizationRelationship -TargetOWAUrl http://<CNAME value>/owa
    
    例如，如果你在第 1 步中创建的 CNAME 记录为 cloudowa.contoso.com，请运行以下命令：
    
        Set-OrganizationRelationship -TargetOWAUrl http://cloudowa.contoso.com/owa
    
    **注意：**
    
      - 请使用 http，而不是 https。
    
      - 在组织关系中，末尾必须有值 /owa，而在 URL 中用户无需输入 /owa。

## 多重身份验证提示

用户可能会收到多重身份验证提示，具体取决于：

  - 连接起始位置（内部还是外部 Internet 连接）。

  - 计算机是否已加入域。

  - 是否在混合环境中使用了联合身份验证。

下表介绍了可能会向用户提供的身份验证提示体验。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>身份验证方法</th>
<th>客户端计算机</th>
<th>身份验证提示体验</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>联合身份验证</p></td>
<td><p>内部 Internet 连接</p></td>
<td><p>单一提示</p></td>
</tr>
<tr class="even">
<td><p>联合身份验证</p></td>
<td><p>外部 Internet 连接</p></td>
<td><p>双重提示</p></td>
</tr>
<tr class="odd">
<td><p>无联合身份验证</p></td>
<td><p>已加入域（内部或外部）</p></td>
<td><p>双重提示</p></td>
</tr>
<tr class="even">
<td><p>有或无联合身份验证</p></td>
<td><p>未加入域（内部或外部）</p></td>
<td><p>双重提示</p></td>
</tr>
</tbody>
</table>


**注意：**联合身份验证要求在 Internet Explorer 的 Intranet 区域中配置 AD FS 终结点（如 <https://go.microsoft.com/fwlink/p/?linkid=834460> 中的主题所述），并要求根据常规 Office 365 指导配置 AD FS。

