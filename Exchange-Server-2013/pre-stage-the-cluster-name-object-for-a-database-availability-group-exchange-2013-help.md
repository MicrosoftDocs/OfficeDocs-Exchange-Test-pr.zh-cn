---
title: '为数据库可用性组预留群集名称对象: Exchange 2013 Help'
TOCTitle: 为数据库可用性组预留群集名称对象
ms:assetid: 51ebf2f6-8a02-44ef-a489-ca361cb0f63a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff367878(v=EXCHG.150)
ms:contentKeyID: 50490558
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为数据库可用性组预留群集名称对象

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2014-08-14_

在计算机帐户创建受限制或计算机帐户在非默认计算机容器创建的环境中，您可以预存群集名称对象 (CNO) ，然后通过向其分配权限来配置 CNO。由于 Windows 中计算机对象的权限变更，因此还需要为 Windows Server 2012 和 Windows Server 2012 R2 DAG 成员预先暂存 CNO。在使用运行 Windows Server 2012 或 Windows Server 2012 R2 的邮箱服务器部署数据库可用性组 (DAG) 时，必需预先暂存和设置 CNO，除非您部署的 DAG 不包含群集管理访问点。不包含群集管理访问点的 DAG 不使用 CNO，因此，不需要为这些 DAG 预先暂存 CNO。

您可为 CNO 创建和禁用计算机帐户，然后执行以下操作之一：

  - 向您要添加到 DAG 的第一个邮箱服务器的计算机帐户分配对该计算机帐户的完全控制权限。

  - 向 Exchange 受信任子系统通用安全组 (USG) 分配对该计算机帐户的完全控制权限。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟

  - 必须使用拥有可在 Active Directory 中创建计算机对象的权限的帐户。

  - 完成以下步骤后，请等待 Active Directory 复制发生。对象复制后，就可向 DAG 添加第一个成员。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 预留 CNO

1.  打开 Active Directory 用户和计算机。

2.  展开林节点。

3.  右键单击要在其中创建新帐户的组织单位 (OU)，选择“新建”，然后选择“计算机”。

4.  在“新建对象 - 计算机”中的“计算机名称”框中键入 CNO 的计算机帐户名称。这是您将用于 DAG 的名称。单击“确定”创建帐户。

5.  右键单击新的计算机帐户，然后单击“禁用帐户”。单击“是”以确认禁用操作，然后单击“确定”。

## 将权限分配给 CNO

1.  打开 Active Directory 用户和计算机。

2.  如果未启用高级功能，请单击“视图”，然后单击“高级功能”，启用这些高级功能。

3.  右键单击新的计算机帐户，然后单击“属性”。

4.  在“\<计算机名称\> 属性”中的“安全”选项卡上单击“添加”，为要添加到 DAG 的第一个节点添加计算机帐户，或者添加 Exchange 受信任子系统 USG：
    
      - 若要添加 Exchange 受信任子系统，请在“输入对象名称来选择”字段中键入 **Exchange Trusted Subsystem**。单击“确定”添加 USG。选择 Exchange Trusted Subsystem USG，并在“Exchange Trusted Subsystem 的权限”字段的“允许”列中选择“完全控制”。单击“确定”以保存权限设置。
    
      - 若要为要添加到 DAG 的第一个节点添加计算机帐户，请单击“对象类型”。在“对象类型”对话框中，清除“内置安全主体”、“组”和“用户”复选框。选中“计算机”复选框，然后单击“确定”。在“输入对象名称来选择”字段中，键入要添加到 DAG 的第一个邮箱服务器的名称，然后单击“确定”。选择第一个节点的计算机帐户，并在“\<节点名称\>的权限”字段中的“允许”列中选择“完全控制”。单击“确定”以保存权限设置。

## 您如何知道这有效？

若要验证是否成功创建了 CNO，请执行以下操作：

1.  打开 Active Directory 用户和计算机。

2.  展开林节点。

3.  打开在其中创建了帐户的组织单位 (OU)，然后验证是否列出了帐户。

