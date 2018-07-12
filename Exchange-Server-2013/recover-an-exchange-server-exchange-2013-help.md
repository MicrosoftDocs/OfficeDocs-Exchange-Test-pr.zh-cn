---
title: '恢复 Exchange 服务器: Exchange 2013 Help'
TOCTitle: 恢复 Exchange 服务器
ms:assetid: 46e9a1cf-b64c-43c3-a898-6171176da761
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876880(v=EXCHG.150)
ms:contentKeyID: 50490461
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 恢复 Exchange 服务器

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

通过在 Microsoft Exchange Server 2013 中使用 **Setup /m:RecoverServer** 开关，可以恢复丢失的服务器。运行 Exchange 2013 的计算机的大多数设置都存储在 Active Directory 中。*/m:RecoverServer* 开关使用 Exchange 中存储的设置及其他信息，重建具有相同名称的 Active Directory 服务器。

恢复丢失的 Exchange 服务器通常是通过使用新硬件完成的。但是，您也可以使用现有的服务器。

本主题显示了如何恢复并非数据库可用性组 (DAG) 成员的丢失 Exchange 2013 服务器。有关恢复 DAG 成员服务器的详细步骤，请参阅[恢复数据库可用性组成员服务器](recover-a-database-availability-group-member-server-exchange-2013-help.md)。

> [!NOTE]  
> 如果 Exchange 不是安装在默认位置，则必须使用 <em>/TargetDir</em> 开关指定 Exchange 二进制文件的位置。如果不使用 <em>/TargetDir</em> 开关，则 Exchange 文件将安装在默认位置 (%programfiles%\Microsoft\Exchange Server\V15) 中。<br />
> 若要确定安装位置，请执行下列步骤：
> <ol>
> <li><p>打开 ADSIEDIT.MSC 或 LDP.EXE。</p></li>
> <li><p>导航到以下位置：<strong>CN=ExServerName,CN=Servers,CN=First Administrative Group,CN=Administrative Groups,CN=ExOrg Name,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=DomainName,CN=Com</strong></p></li>
> <li><p>右键单击 Exchange 服务器对象，然后单击“属性”。</p></li>
> <li><p>找到 <strong>msExchInstallPath</strong> 属性。此属性存储当前安装路径。</p></li>
> </ol>


是否要查找与备份和还原数据相关的其他管理任务？请查看[备份、还原和灾难恢复](backup-restore-and-disaster-recovery-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：20 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的“Exchange 基础结构权限”部分。

  - 执行恢复操作的服务器必须运行与丢失服务器相同的操作系统。例如，您无法在运行 Windows Server 2012 的服务器上恢复运行 Exchange 2013 和 Windows Server 2008 R2 的服务器，反之亦然。同样，您无法在运行 Windows Server 2012 R2 的服务器上恢复运行 Exchange 2013 和 Windows Server 2012 的服务器，反之亦然。

  - 在运行恢复的服务器上必须存在用于装入的数据库的故障服务器上的相同磁盘驱动器号。

  - 执行恢复操作的服务器必须与丢失服务器拥有相同的性能特征和硬件配置。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 恢复丢失的 Exchange 服务器

1.  重置丢失的服务器的计算机帐户。有关详细步骤，请参阅[重置计算机帐户](https://go.microsoft.com/fwlink/p/?linkid=165388)。

2.  安装正确的操作系统，并采用与丢失服务器相同的名称命名新的服务器。如果执行恢复操作的服务器与丢失的服务器名称不同，则无法成功恢复。

3.  将该服务器加入与丢失服务器相同的域中。

4.  安装必需的先决条件和操作系统组件。有关详细信息，请参阅[Exchange 2013 系统要求](exchange-2013-system-requirements-exchange-2013-help.md)和[Exchange 2013 先决条件](exchange-2013-prerequisites-exchange-2013-help.md)。

5.  登录到正恢复的服务器上，打开命令提示符。

6.  导航到 Exchange 2013 安装文件，然后运行以下命令。
    
        Setup /m:RecoverServer /IAcceptExchangeServerLicenseTerms

7.  在安装程序完成之后，恢复的服务器投入使用之前，重新配置以前存在于该服务器上的所有自定义设置，然后重新启动该服务器。

## 您如何知道这有效？

成功完成的安装程序将成为主指示器，这表示恢复成功。若要进一步验证是否成功恢复了丢失的服务器，请执行以下操作：

  - 打开 Windows 服务工具 (services.msc) 并验证 Microsoft Exchange 服务是否已安装和运行。

