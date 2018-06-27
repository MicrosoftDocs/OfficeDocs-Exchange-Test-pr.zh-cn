---
title: '使用安装向导安装 Exchange 2013 边缘传输角色: Exchange 2013 Help'
TOCTitle: 使用安装向导安装 Exchange 2013 边缘传输角色
ms:assetid: b8e51b0b-201e-4c64-92c8-3ac0db04b6e2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn635117(v=EXCHG.150)
ms:contentKeyID: 61203689
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用安装向导安装 Exchange 2013 边缘传输角色

 

_**适用于：**Exchange Server, Exchange Server 2013_

_**上一次修改主题：**2014-06-19_

本主题说明了如何在计算机上使用 Microsoft Exchange Server 2013 安装向导来安装 Exchange 2013 边缘传输服务器角色。Exchange 2013 Service Pack 1 (SP1) 或更高版本中边缘传输角色可用。有关规划和部署 Exchange 2013 的详细信息，请参阅[规划和部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)。

我们建议在您组织的内部 Active Directory 林以外的外围网络中安装边缘传输角色。虽然您可以在联合域的计算机上安装边缘传输服务角色，但是这样做仅可启用 Windows 功能和设置的域管理。边缘传输角色本身不使用 Active Directory。相反，它使用 Active Directory 轻型目录服务 (AD LDS) Windows 功能存储配置和收件人信息。有关边缘传输角色的详细信息，请参阅[边缘传输服务器](edge-transport-servers-exchange-2013-help.md)。

如果您想在计算机上安装 Exchange 2013 邮箱或客户端访问角色，请参阅[使用安装向导安装 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)。边缘传输角色不能安装在与邮箱或客户端访问服务器角色相同的计算机上。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>你是否曾听说过 Exchange Server 部署助理？它是一款免费的联机工具，它将询问您一些问题并专门为您创建自定义部署检查表，以帮助您在组织中快速部署 Exchange 2013。若您想要了解关于它的详细信息，请转到 <a href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 部署助理</a>。</td>
</tr>
</tbody>
</table>


有关安装之后要完成的任务的信息，请参阅 [Exchange 2013 安装后任务](exchange-2013-post-installation-tasks-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 预计完成时间：40 分钟

  - 确保在安装 Exchange 2013 之前阅读了发行说明。有关详细信息，请参阅[Exchange 2013 发行说明](release-notes-for-exchange-2013-exchange-2013-help.md)。

  - 您安装 Exchange 2013 的计算机必须使用受支持的操作系统（如 Windows Server 2008 R2 with SP1、Windows Server 2012 R2 或 Windows Server 2012），拥有足够的磁盘空间，并满足其他要求。有关系统要求的信息，请参阅 [Exchange 2013 系统要求](exchange-2013-system-requirements-exchange-2013-help.md)。

  - 要运行 Exchange 2013 设置，您必须安装 Microsoft .NET Framework 4.5、Windows Management Framework 和其他所需的软件。若要了解所有服务器角色的先决条件，请参阅 [Exchange 2013 先决条件](exchange-2013-prerequisites-exchange-2013-help.md)。

  - 您需要在计算机上配置主 DNS 后缀。例如，如果您的计算机的完全限定域名为 edge.contoso.com，计算机的 DNS 后缀是 contoso.com。有关详细信息，请参阅[缺少主要的 DNS 后缀](primary-dns-suffix-is-missing-exchange-2013-help.md)。

  - Exchange 2007 和 Exchange 2010 中心传输服务器更新之后，您才可以在它们和 Exchange 2013 边缘传输服务器之间创建 EdgeSync 订阅。如果您不安装此更新，EdgeSync 订阅将不会正常工作。有关详细信息，请参阅 [Exchange 2013 系统要求](exchange-2013-system-requirements-exchange-2013-help.md)中的“受支持的共存方案”一节。

  - 确保您使用的帐户是您正在安装边缘传输角色的计算机上本地管理员组中的成员。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在服务器上安装 Exchange 之后，不得更改服务器名称。不支持在安装了 Exchange 服务器角色之后重命名服务器。</td>
</tr>
</tbody>
</table>


## 安装 Exchange Server 2013

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要下载 Exchange 2013 的最新版本，请参阅 <a href="updates-for-exchange-2013-exchange-2013-help.md">Exchange 2013 更新</a>。</td>
</tr>
</tbody>
</table>


1.  登录到要安装 Exchange 2013 的计算机。

2.  导航到 Exchange 2013 安装文件的网络位置。

3.  通过双击 `Setup.exe` 启动 Exchange 2013 安装程序
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果启用了用户访问控制 (UAC)，则必须右键单击 <code>Setup.exe</code> 并选择“以管理员身份运行”。</td>
    </tr>
    </tbody>
    </table>


4.  在“检查更新？”页面，选择是否希望安装程序连接到 Internet 并下载 Exchange 2013 的产品和安全更新。如果您选择“连接到 Internet 并检查更新”，安装程序将下载更新，并在应用这些更新后继续。如果您选择“现在不检查更新”，您可在随后手动下载和安装更新。我们建议您现在下载并安装更新。单击“下一步”继续。

5.  
    
    “简介”页开始将 Exchange 安装到组织中的过程。它将引导您完成安装。这里列出几个有助于部署的链接。我们建议您在继续安装之前访问这些链接。单击“下一步”继续。

6.  
    
    在“许可协议”页上，查看软件许可条款。如果同意这些条款，请选择“我接受许可协议中的条款”，然后单击“下一步”。

7.  
    
    在“推荐设置”页面上，选择是否要使用建议设置。如果选择“使用建议设置”，Exchange 将自动将错误报告和有关您的计算机硬件以及如何使用 Exchange 的信息发送至 Microsoft。如果选择“不使用建议设置”，这些设置将保持禁用，但是可在设置完成后随时启用它们。有关这些设置以及如何使用发送至 Microsoft 的信息的详细信息，请单击“?”。

8.  
    
    在“服务器角色选择”页上，选择“边缘传输”。请记住，不能将邮箱服务器或客户端访问服务器角色添加到安装了边缘传输角色的计算机。如果安装任何服务器角色，将自动安装管理工具。
    
    选择“自动安装要安装 Exchange Server 所需的 Windows Server 角色和功能”让安装向导安装必需的 Windows 组件。您可能需要重新启动计算机以完成一些 Windows 功能的安装。如果不选择该选项，您必须手动安装 Windows 功能。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此选项仅安装 Exchange 所需的 Windows 功能。您必须手动安装其他必备组件。有关详细信息，请参阅<a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 先决条件</a>。</td>
    </tr>
    </tbody>
    </table>
    
    单击“下一步”继续。

9.  在“安装空间和位置”页上，或者接受默认安全位置，或者单击“浏览”选择新位置。确保您要安装 Exchange 的位置有足够磁盘空间。单击“下一步”继续。

10. 
    
    在“准备情况检查”页上，查看状态以确定是否成功完成了组织和服务器角色先决条件检查。如果未成功完成操作，则必须解决所有报告的错误，然后才能安装 Exchange 2013。解决某些先决条件错误时，不需要退出安装程序。解决报告的错误后，单击“返回”，然后单击“下一步”运行先决条件检查。此外，请务必检查报告的所有警告。如果已成功完成所有准备情况检查，请单击“下一步”以安装 Exchange 2013。

11. 
    
    在“完成”页上，单击“完成”。

12. 在 Exchange 2013 完成之后重新启动计算机。

13. 通过执行 [Exchange 2013 安装后任务](exchange-2013-post-installation-tasks-exchange-2013-help.md) 中提供的任务完成部署。

## 您如何知道这样可行？

要验证是否成功安装 Exchange 2013，请参阅[验证 Exchange 2013 安装](verify-an-exchange-2013-installation-exchange-2013-help.md)。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

