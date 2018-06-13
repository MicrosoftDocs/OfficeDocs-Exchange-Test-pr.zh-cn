---
title: 'Exchange 混合部署中共享的忙/闲信息: Exchange 2013 Help'
TOCTitle: Exchange 混合部署中共享的忙/闲信息
ms:assetid: bd3884de-80ee-4ff2-a8a3-eacd5aa3e51b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ650274(v=EXCHG.150)
ms:contentKeyID: 50492083
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 混合部署中共享的忙/闲信息

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2016-04-29_

在位于内部部署和 Exchange Online 组织中的用户之间共享忙/闲（日历可用性）信息是混合部署的主要好处之一。两种组织中的用户都可以查看彼此的日历，就如同这些用户位于同一个物理组织中一样。如此便可以方便且高效地进行会议和资源调度。

需要混合部署中的几个组件在本地 Exchange 组织和 Exchange Online 组织之间启用共享忙/闲功能。

  - **联合身份验证信任**   本地组织和 Office 365 服务组织都需要与 Azure AD 身份验证系统建立联合身份验证信任。联合身份验证信任是与 Azure AD 身份验证系统的一对一关系，该关系会定义 Exchange 组织的参数。该系统在充当本地组织与 Office 365 服务组织之间的信任代理时，使用这些参数在本地组织用户与 Exchange Online 组织用户之间交换忙/闲信息。
    
    在创建帐户时，将自动为 Office 365 服务组织配置与该系统的联合信任。混合配置向导会自动查看对于本地组织，是否存在与 Azure AD 身份验证系统之间的现有联合身份验证信任。如果存在，则现有联合身份验证信任将用于支持混合部署。如果不存在，则向导会为本地组织创建与 Azure AD 身份验证系统之间的联合身份验证信任。该向导还会将在“混合配置”向导中选择的所有域都添加到本地组织联合身份验证信任中。
    
    有关详细信息，请参阅 [共享](https://technet.microsoft.com/zh-cn/library/dd638083\(v=exchg.150\))。

  - **组织关系**   内部部署组织和 Exchange Online 组织都需要组织关系，并由“混合配置”向导自动配置这些关系。组织关系将定义组织共享的忙/闲信息级别。
    
    默认情况下，内部部署与 Exchange Online 组织关系的忙/闲数据访问共享级别都为“考虑时间、主题和位置的忙/闲访问”。如果需要修改内部部署组织用户与 Exchange Online 组织用户之间的忙/闲共享访问，可以在完成“混合配置”向导后手动配置组织关系访问级别。
    
    有关详细信息，请参阅 [共享](https://technet.microsoft.com/zh-cn/library/dd638083\(v=exchg.150\))。

为组织部署混合部署时，在所有情况下，“混合配置”向导都会自动配置共享忙/闲日历访问。混合部署要求创建与 Azure AD 身份验证系统的联合身份验证信任，并为本地组织和 Exchange Online 组织配置组织关系。如果不希望内部部署组织用户与 Exchange Online 组织用户在混合部署中共享忙/闲信息，则可手动禁用忙/闲共享，方法是：在完成“混合配置”向导后使用Exchange 命令行管理程序和 [Set-HybridConfiguration](https://technet.microsoft.com/zh-cn/library/hh529932\(v=exchg.150\)) cmdlet。

下表中显示的混合部署功能依赖于联合身份验证信任和组织关系。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>邮件传递区域</th>
<th>功能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>电子邮件客户端</p></td>
<td><ul>
<li><p>邮件跟踪</p></li>
<li><p>邮件提示</p></li>
<li><p>多邮箱搜索</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>合规性</p></td>
<td><ul>
<li><p>Exchange 联机存档</p></li>
<li><p>Exchange 就地电子数据展示</p></li>
</ul></td>
</tr>
</tbody>
</table>

