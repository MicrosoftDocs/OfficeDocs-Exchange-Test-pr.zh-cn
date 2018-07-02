---
title: '在 Exchange 资源林拓扑中部署 Exchange 2013: Exchange 2013 Help'
TOCTitle: 在 Exchange 资源林拓扑中部署 Exchange 2013
ms:assetid: 537a7b2b-d002-40a6-84ae-fd02635f9e23
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998031(v=EXCHG.150)
ms:contentKeyID: 51408226
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在 Exchange 资源林拓扑中部署 Exchange 2013

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

本主题说明如何在 Exchange 资源林拓扑中部署 Microsoft Exchange 2013。Exchange 资源林又称为专用 Exchange 林。本主题假定不存在现有的 Exchange 2013 拓扑。

下图显示了具有资源林的 Exchange 组织。

**具有 Exchange 资源林的 Exchange 组织示例**

![具有资源林的复杂 Exchange 组织](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "具有资源林的复杂 Exchange 组织")

## 在开始之前，您需要知道什么？

要在 Exchange 2013 中执行以下步骤，请确认你已具有以下内容：

  - 具有以下两个 Active Directory 林：
    
      - 一个林包含组织的用户帐户。在此步骤中，此林称为*帐户林*。
    
      - 一个林不包含用户帐户，并且未安装 Exchange。在此步骤中，此林称为*Exchange 林*。您将使用此步骤在上述林中安装 Exchange 2013。

  - 你已为组织内的跨林名称解析正确配置了域名系统 (DNS)。若要检查是否已正确配置 DNS，请从组织内的其他林 ping 每个林。有关配置 DNS 的详细信息，请参阅 [DNS 服务器操作指南](https://go.microsoft.com/fwlink/p/?linkid=282295)。

## 在 Exchange 资源林拓扑中部署 Exchange 2013

1.  在 Exchange 林中的域控制器上创建单向传出信任，以使 Exchange 林信任帐户林。有关详细步骤，请参阅 [Create a one-way, outgoing, forest trust for both sides of the trust](https://go.microsoft.com/fwlink/p/?linkid=69130)（为信任双方创建单向传出林信任）。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>尽管我们建议您创建林信任，但是，您可以创建林信任，也可以创建外部信任。如果创建外部信任，在步骤 3 中创建链接邮箱时，在新建邮箱向导的“主帐户”页上，必须指定可以访问受信任林中的域控制器的用户帐户。不能使用当前登录所使用的凭据。如果使用 <strong>New-Mailbox</strong> cmdlet 创建链接邮箱，必须使用 <em>LinkedCredential</em> 参数指定可以访问受信任林中的域控制器的用户帐户。</td>
    </tr>
    </tbody>
    </table>


2.  在 Exchange 林中，安装 Exchange 2013。Exchange 的安装方式与在单林方案中相同。有关如何安装 Exchange 2013 的详细步骤，请参阅下列主题之一：
    
      - [部署 Exchange 2013 的新安装](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [使用安装向导安装 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

3.  在 Exchange 林中，为将在 Exchange 林中拥有邮箱的帐户林内的每个用户创建与外部帐户关联的邮箱。有关详细步骤，请参阅[管理链接的邮箱](manage-linked-mailboxes-exchange-2013-help.md)。

