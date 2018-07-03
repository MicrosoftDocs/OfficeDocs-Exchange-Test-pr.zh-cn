---
title: '在跨林拓扑中部署 Exchange 2013: Exchange 2013 Help'
TOCTitle: 在跨林拓扑中部署 Exchange 2013
ms:assetid: 65be650f-d435-4f60-9ff0-5cb88a726abb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998597(v=EXCHG.150)
ms:contentKeyID: 51408232
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在跨林拓扑中部署 Exchange 2013

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

此主题介绍如何使用 Microsoft Forefront Identity Manager 2010 R2 SP1 在跨林拓扑中部署 Exchange 2013。要在跨林拓扑中部署 Exchange 2013，必须先在各个林中安装 Exchange 2013，然后连接这些林，以便用户可以跨林查看地址和可用性数据。

下图所示为两个 Exchange 2013 林之间的用户同步。

**Exchange 2013 跨林同步示例**

![Exchange 2010 多林示例](images/Aa998597.df0ba5dd-cb96-4542-98bd-2a425defe317(EXCHG.150).gif "Exchange 2010 多林示例")

本主题*不*对如何在专用 Exchange 林（或资源林）拓扑中部署 Exchange 2013 进行描述。有关如何在资源林拓扑中部署 Exchange 2013 的详细信息，请参阅[在 Exchange 资源林拓扑中部署 Exchange 2013](deploy-exchange-2013-in-an-exchange-resource-forest-topology-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

要在 Exchange 2013 中执行以下步骤，请确认以下事项：

  - 已为组织内的跨林名称解析正确配置了域名系统 (DNS)。若要验证 DNS 的配置是否正确，应使用 Ping 工具从组织中的其他林以及将运行 GALSync 代理的服务器测试与每个林的连接。

  - GALSync 管理代理 (MA) 使用 Windows PowerShell V2.0 RTM 与 Exchange 2013 林进行通信。转至控制面板，然后单击“程序和功能”，以确保此计算机上未安装 Windows PowerShell v1.0。

  - 确保尚未通过 Windows 更新安装 Windows 远程管理。

  - 安装 Windows PowerShell 和 Windows 远程管理。有关详细信息，请参阅 Microsoft 知识库文章 968930 [Windows Management Framework Core 程序包（Windows PowerShell 2.0 和 WinRM 2.0）](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930)。

  - 下载 Forefront Identity Manager 2010 R2 SP1。请参阅[下载 Microsoft Forefront Identity Manager 2010 R2 SP1](https://go.microsoft.com/fwlink/p/?linkid=279868)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用 Forefront Identity Manager 2010 R2 SP1 在跨林拓扑中部署 Exchange 2013

1.  在各个林中，分别安装 Exchange 2013。要安装 Exchange 2013，请执行与在单林拓扑中安装 Exchange 2013 时相同的步骤。有关详细步骤，请参阅下列主题之一：
    
      - [部署 Exchange 2013 的新安装](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [使用安装向导安装 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>本主题假设您尚无现有的 Exchange 2007 或 Exchange 2010 拓扑。如果存在现有的 Exchange 拓扑并且要进行升级，请参阅<a href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">从 Exchange 2010 升级至 Exchange 2013</a> 或<a href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">从 Exchange 2007 升级到 Exchange 2013</a>。</td>
        </tr>
        </tbody>
        </table>


2.  在每个林中，使用 Active Directory 用户和计算机创建一个容器，FIM 2010 R2 SP1 将在其中为另一个林中的各邮箱创建联系人。建议将此容器命名为 **FromFIM**。若要创建该容器，请选择要在其中创建容器的域，右键单击该域，选择“新建”\>“组织单位”。在“新建对象 - 组织单位”中，键入 **FromFIM**，再单击“确定”。

3.  使用 Forefront Identify Manager 为各个林创建一个 GALSync 管理代理。此操作允许您对各个林中的用户进行同步，并创建一个公用 GAL。有关详细步骤，请参阅下列资源：
    
      - [使用 Forefront Identity Manager (FIM) 2010 配置全局地址列表 (GAL) 同步](https://go.microsoft.com/fwlink/p/?linkid=279869)
    
      - [使用管理代理](https://go.microsoft.com/fwlink/p/?linkid=279870)
    
      - [Forefront Identity Manager 2010 R2 文档路线图](https://go.microsoft.com/fwlink/p/?linkid=279871)
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>虽然这些资源讨论的是 Exchange 2010，但 FIM 2010 R2 SP1 也同样支持 Exchange 2013。确保为 Exchange 2013 在 FIM 2010 R2 SP1 中配置“扩展”。</td>
    </tr>
    </tbody>
    </table>
    
    1.  在“配置扩展”页面上，在“配置分区显示名称”下，在“配置”旁边，选择“Exchange 2013”。您会看到“Exchange 2013 RPS URI”字段。输入 Exchange 2013 客户端访问服务器的 URI 以确保远程 Powershell 连接正常。“Exchange 2013 RPS URI”应为以下格式：http://CAS\_Server\_FQDN/Powershell。单击“确定”。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>确保用于连接到 Exchange 2013 林的管理员凭据还可向该林进行远程 PowerShell 连接。<br />
        下图说明了如何为 Exchange 2013 选择配置。</td>
        </tr>
        </tbody>
        </table>
        
        **为 Exchange 2013 配置 GalSync 管理代理**
        
        ![Exchange 2010 管理代理设置](images/Aa998597.8f403cda-e5e4-4edf-887f-c1ed46cee3f5(EXCHG.150).gif "Exchange 2010 管理代理设置")  

4.  在每个林中创建 SMTP 发送连接器。有关详细步骤，请参阅[配置跨林发送连接器](configure-a-cross-forest-send-connector-exchange-2013-help.md)。

5.  在每个林中启用可用性服务，以便每个林中的用户都可以查看其他林中的用户的忙/闲数据。有关详细信息，请参阅 [Exchange 2013 中的可用性服务](availability-service-in-exchange-2013-exchange-2013-help.md)。

6.  如果要通过组织中的任何林中继邮件，则必须将该林中的某个域配置为权威域。有关详细步骤，请参阅[将 Exchange 配置为接收多个权威域的邮件](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md)。

