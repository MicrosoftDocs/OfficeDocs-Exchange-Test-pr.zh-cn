---
title: '启用远程移动的 MRS 代理终结点: Exchange 2013 Help'
TOCTitle: 启用远程移动的 MRS 代理终结点
ms:assetid: 9840f712-127e-4c2d-bfe5-1b35cdb2a31b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn155787(v=EXCHG.150)
ms:contentKeyID: 54652290
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 启用远程移动的 MRS 代理终结点

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-07-02_

邮箱复制服务代理（MRS 代理）为内部部署 Exchange 组织与 Exchange Online 之间的跨林邮箱移动和远程移动迁移提供了便利。在 Exchange 2013 中，MRS 代理包括在邮箱服务器角色（也称为*邮箱服务器*）中。在跨林和远程移动迁移期间，客户端访问服务器充当邮箱服务器的传入移动请求的代理。默认情况下，禁止客户端访问服务器接受这些请求。要允许客户端访问服务器接受传入移动请求，必须启用 MRS 代理终结点。

启用 MRS 代理终结点的客户端访问服务器依赖于邮箱移动的类型和方向。

  - **跨林企业移动**   对于从目标环境启动的跨林移动（也称为*拉取*移动类型），必须在源环境中的客户端访问服务器上启用 MRS 代理终结点。对于从源环境启动的跨林移动（也称为*推送*移动类型），必须在目标环境中的客户端访问服务器上启用 MRS 代理终结点。

  - **内部部署 Exchange 组织与 Exchange Online 之间的远程移动迁移**   对于加入和分离远程移动迁移，必须在内部部署组织中的客户端访问服务器上启用 MRS 代理终结点。

> [!NOTE]
> 如果使用 EAC 移动邮箱，则跨林移动和加入远程移动迁移属于拉取移动类型，这是因为请求是从目标环境发出的。分离远程移动迁移属于推送移动类型，因为请求是从源环境发出的。


## 在开始之前，您需要知道什么？

  - 估计完成时间：每个服务器 2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“Exchange Web 服务权限”部分。

  - 如果在 Exchange 组织中部署了多个客户端访问服务器，则应当在每个服务器上启用 MRS 代理终结点。如果添加其他客户端访问服务器，请确保在新服务器上启用 MRS 代理终结点。如果未在所有客户端访问服务器上启用 MRS 代理终结点，则跨林移动和远程移动迁移可能失败。

  - 如果不执行跨林移动或远程移动迁移，请将 MRS 代理终结点保持为禁用状态，以减少组织的攻击面。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 启用 MRS 代理终结点

1.  在 EAC 中，导航到“收件人”\>“服务器”\>“虚拟目录。

2.  在“选择服务器”下拉列表中，选择要启用 MRS 代理终结点的客户端访问服务器的名称。或者选择“所有服务器”以显示组织中所有客户端访问服务器上的虚拟目录。

3.  在“选择类型”下拉列表中，选择“EWS”以显示选定服务器的 Exchange Web 服务 (EWS) 虚拟目录。

4.  在虚拟目录列表中，单击要配置的客户端访问服务器的“EWS (默认网站)”，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

5.  在“EWS (默认网站)”属性页上，选中“已启用 MRS 代理”复选框，然后单击“保存”。

## 使用命令行管理程序启用 MRS 代理终结点

下面的命令在名为 EXCH-SRV-01 的客户端访问服务器上启用 MRS 代理终结点。

    Set-WebServicesVirtualDirectory -Identity "EXCH-SRV-01\EWS (Default Web Site)" -MRSProxyEnabled $true

下面的命令在 Exchange 组织中的所有客户端访问服务器上启用 MRS 代理终结点。

    Get-WebServicesVirtualDirectory | Set-WebServicesVirtualDirectory -MRSProxyEnabled $true

> [!important]
> 如上所述，应当在组织中的每个客户端访问服务器上启用 MRS 代理终结点。将新客户端访问服务器添加到组织后，运行上述命令。


## 您如何知道操作成功？

若要验证是否已成功启用 MRS 代理终结点，请执行下列操作之一：

1.  在 EAC 中，导航到“收件人”\>“服务器”\>“虚拟目录。

2.  在虚拟目录列表中，单击“EWS (默认网站)”，在详细信息窗格中验证已启用 MRS 代理终结点。
    
    或者，可以单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标") 查看“EWS (默认网站)”属性页，确认已选中“已启用 MRS 代理”复选框。

或

在命令行管理程序中运行以下命令：

    Get-WebServicesVirtualDirectory | FL Identity,MRSProxyEnabled

验证 *MRSProxyEnabled* 参数是否已设置为 `True`。

验证已启用 MRS 代理终结点的另一种方法是使用 **Test-MigrationServerAvailability** cmdlet 测试与托管要移动的邮箱的远程服务器进行通信的能力，或者如果将 Exchange Online 邮箱分离到内部部署组织，则测试与内部部署组织中的服务器进行通信的能力。有关详细信息，请参阅 [Test-MigrationServerAvailability](https://technet.microsoft.com/zh-cn/library/jj219169\(v=exchg.150\))。

下面的示例测试与 corp.contoso.com 林中服务器的连接。

```
    $Credentials = Get-Credential
```
```
    Test-MigrationServerAvailability -ExchangeRemoteMove -Autodiscover -EmailAddress administrator@corp.contoso.com -Credentials $Credentials
```

要成功运行此命令，必须启用 MRS 代理终结点。

