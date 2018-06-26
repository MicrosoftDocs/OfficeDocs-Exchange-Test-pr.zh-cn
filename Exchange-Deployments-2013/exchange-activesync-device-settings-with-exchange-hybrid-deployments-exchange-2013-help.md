---
title: 'Exchange ActiveSync 设备设置与 Exchange 混合部署: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync 设备设置与 Exchange 混合部署
ms:assetid: 77f7cd72-2a8a-467e-9ffd-b93f5eeb2f69
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn931281(v=EXCHG.150)
ms:contentKeyID: 64965206
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ActiveSync 设备设置与 Exchange 混合部署

 

_<strong>适用于：</strong>Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_

_<strong>上一次修改主题：</strong>2016-01-27_

当邮箱从 Exchange 内部部署组织移动到 Office 365 时，Exchange ActiveSync 设备将立即自动重新配置。Exchange ActiveSync 将在 Office 365 中查找新邮箱位置，并更新其配置，从而直接与 Office 365 通信。当 Exchange ActiveSync 设备成功重定向到 Office 365 后，此设备不会尝试与内部部署 Exchange 服务器联系。仅少数例外情况外（详情如下），用户不再需要手动设置设备来继续处理邮件。

如果您想要将邮箱移动到 Office 365，请参阅 [在混合部署的本地组织和 Exchange Online 组织之间移动邮箱](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md)。

有关混合部署的更多信息，请参阅 [Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。

若要使用自动重定向，内部部署服务器应运行 Exchange 2010、Exchange 2013、Exchange 2016 或更高版本的最新发行版。您还需要已使用 [“混合配置”向导](hybrid-configuration-wizard-exchange-2013-help.md) 设置好混合部署。Exchange ActiveSync 重定向功能将使用在组织关系对象上设置的 Web 上的 Outlook 目标 URL。运行混合配置向导时，将配置此对象。

如果您的组织满足上面列出的要求，当用户的邮箱移动时，移动设备应自动被重定向到 Office 365，无需任何其他配置。若要获得最佳体验，请确保您用户的移动设备正在运行其操作系统和电子邮件客户端的最新版本。某些移动设备（如运行 Android 操作系统的设备）可能需要相当长的时间重定向。此外，某些设备可能不正确地解释由 Exchange 发送的 Exchange ActiveSync 451 重定向说明。对于这些设备，用户仍需要手动重新配置或重新创建其设备上的电子邮件帐户。如果您对设备是否支持 Exchange ActiveSync 451 重定向有疑问，请与设备制造商联系。

在下列方案中不支持自动 Exchange ActiveSync 重定向：

  - 将邮箱从 Office 365 移动到内部部署 Exchange 组织。

  - 在内部部署 Exchange 组织之间移动邮箱。

  - 将邮箱从 Exchange 2007 服务器移动到 Office 365。

