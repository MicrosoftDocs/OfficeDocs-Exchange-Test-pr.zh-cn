---
title: '收件人权限: Exchange 2013 Help'
TOCTitle: 收件人权限
ms:assetid: 5b690bcb-c6df-4511-90e1-08ca91f43b37
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638132(v=EXCHG.150)
ms:contentKeyID: 50490641
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 收件人权限

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

执行收件人管理任务所需的权限视所执行的过程或要运行的 cmdlet 而定。

若要了解执行过程或运行 cmdlet 所需的权限，请执行以下操作：

1.  在下表中查找与所要执行的过程或要运行的 cmdlet 最相关的功能。

2.  接下来，查看该功能所需的权限。您必须被分配到其中一个角色组、等效的自定义角色组或等效的管理角色。还可以单击角色组查看其管理角色。如果某个功能列出多个角色组，则您只需要被分配到其中一个角色组就可以使用此功能。有关角色组和管理角色的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

3.  现在运行 **Get-ManagementRoleAssignment** cmdlet 以查看分配给您的角色组或管理角色，以便确定您是否具有管理该功能所需的权限。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>必须分配了 Role Management 管理角色才能运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet。如果没有运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet 的权限，则请求 Exchange 管理员检索分配给您的角色组或管理角色。</td>
    </tr>
    </tbody>
    </table>


如果要将管理一项功能的权限委派给另一个用户，请参阅[委派角色分配](delegate-role-assignments-exchange-2013-help.md)。

## 邮箱服务器权限

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>日历修复、服务器配置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>委派邮箱服务器</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>电子邮件地址策略</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange 搜索</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 搜索 - 诊断</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p>
<p>支持诊断角色</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>未对角色组分配支持诊断角色。有关详细信息，请参阅<a href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">向用户或 USG 添加角色</a>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>组指标</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>导入导出</p></td>
<td><p>邮箱导入导出角色</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>未对角色组分配邮箱导入导出角色。有关详细信息，请参阅<a href="mailbox-import-export-role-exchange-2013-help.md">邮箱导入导出角色</a>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>邮箱助理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>邮箱移动</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>邮箱恢复</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>邮箱修复请求</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>邮箱还原请求</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>邮箱服务器配置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>管理邮箱服务器上的 Exchange 搜索索引器服务</p></td>
<td><p>邮箱服务器上的本地管理员</p></td>
</tr>
<tr class="odd">
<td><p>MAPI 连接</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>OAB 虚拟目录</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>删除存储邮箱</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
</tbody>
</table>


## 日历和共享权限

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>日历配置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
</tr>
<tr class="even">
<td><p>日历诊断</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">清洁管理</a></p>
<p><a href="compliance-management-exchange-2013-help.md">遵从性管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
</tr>
<tr class="odd">
<td><p>日历处理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
</tr>
<tr class="even">
<td><p>通知</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>组织关系</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>共享策略</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
</tbody>
</table>


## 资源邮箱配置权限

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>预订策略</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
</tr>
<tr class="even">
<td><p>委派</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>资源邮箱架构配置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
</tbody>
</table>


## 邮箱数据库权限

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>邮箱数据库</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
</tbody>
</table>


## 收件人设置权限

此表包含管理收件人所需的各种权限。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>地址列表、GAL</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>反垃圾邮件</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>适用于 Outlook 的应用程序</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
</tr>
<tr class="even">
<td><p>应用共享策略</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>仲裁</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>存档连接</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>分配脱机通讯簿</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>自动答复</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
</tr>
<tr class="odd">
<td><p>日历配置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>日历修复</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>联系人聚合设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>断开连接的邮箱</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
</tr>
<tr class="odd">
<td><p>通讯组</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>动态通讯组</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>电子邮件地址</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="um-management-exchange-2013-help.md">UM 管理</a></p></td>
</tr>
<tr class="even">
<td><p>收件箱规则</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
</tr>
<tr class="odd">
<td><p>邮件联系人</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>邮件提示</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>邮件用户</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>邮箱文件夹权限</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
</tr>
<tr class="odd">
<td><p>邮箱文件夹</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>MAPI 连接</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>邮件配置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
</tr>
<tr class="even">
<td><p>邮件配额</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>裁决</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>权限和委派</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>存档邮箱</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>收件人数据属性</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>远程邮箱</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>保留和合法保留</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
</tr>
<tr class="odd">
<td><p>代理发送</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>拼写配置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
</tr>
<tr class="odd">
<td><p>统一消息</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="um-management-exchange-2013-help.md">UM 管理</a></p></td>
</tr>
<tr class="even">
<td><p>用户邮箱</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>用户照片</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
</tr>
</tbody>
</table>


## 邮箱移动和迁移权限

该表包含将内部部署邮箱移动到不同域或林以及将内部部署邮箱移动到基于云的组织和从基于云的组织移动内部部署邮箱所需的权限。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>邮箱移动（本地或跨林）</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>邮箱移动（混合部署）</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>迁移（云内和云外）</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
</tbody>
</table>

