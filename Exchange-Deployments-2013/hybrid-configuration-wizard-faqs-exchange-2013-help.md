---
title: '混合配置向导 FAQ: Exchange 2013 Help'
TOCTitle: 混合配置向导 FAQ
ms:assetid: e911e6e0-e36e-4430-ac36-c745a10d6c26
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt488940(v=EXCHG.150)
ms:contentKeyID: 72045783
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 混合配置向导 FAQ

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2016-12-09_

Microsoft 发布了新的混合配置向导，该向导简化了混合部署的配置，允许更灵活地进行混合配置，并确保始终运行最新版本的体验。此版本的混合向导内置在于 Exchange 2016 和从累积更新 10 开始的 Exchange 2013 版本中，但是，即使正在运行较旧的 Exchange 2013 累积更新 (CU) 或 Exchange 2010 Service Pack 3 (SP3)，仍可以下载新的向导。

有关 Office 365 混合配置向导的详细信息，请在 Exchange 团队博客上参阅 [Introducing the Microsoft Office 365 Hybrid Configuration Wizard](http://go.microsoft.com/fwlink/?linkid=717122)（引入 Microsoft Office 365 混合配置向导）和 [Office 365 Hybrid Configuration Wizard for Exchange 2010](http://go.microsoft.com/fwlink/?linkid=730687)（适用于 Exchange 2010 的 Office 365 混合配置向导）。

若要下载 Office 365 混合配置向导，请转到 [http://aka.ms/HybridWizard](http://aka.ms/hybridwizard)。

## 客户提出的常见问题

  - 问：什么版本的 Exchange 支持新的混合配置向导？  
    答：需要至少具有一台满足以下要求的服务器：
    
      - **Exchange 2010**Exchange 2010 SP3 需要至少安装在一台运行邮箱、集线器传输和客户端访问服务器角色的服务器上。我们还强烈建议安装适用于 Exchange 2010 SP3 的最新可用的更新汇总。
    
      - **Exchange 2013**最新的 Exchange 2013 CU 需要至少安装在一台运行邮箱和客户端访问服务器角色的服务器上。如果无法安装最新的 CU，则也支持前一版本。不支持较旧的 CU。
    
      - **Exchange 2016**最新版本的 Exchange 2016 需要至少安装在一台运行邮箱服务器角色的服务器上。
    
    例如，假设已在本地组织中安装了 Exchange 2013 CU8，则 Exchange 2013 的最新可用版本就是 CU10。为了保持处于受支持的混合配置中，需要将 Exchange 2013 服务器至少升级到 CU9。但是，我们强烈建议升级到 CU10。
    
    累积更新按季度有规律地进行发布。如果定期需要额外一些时间来完成升级，那么请让服务器始终使用最新的累积更新，这将带来更多的灵活性。

<!-- end list -->

  - 问：此混合配置向导是否适用于 Exchange 2007？  
    答：可以在组织中使用 Exchange 2007 配置混合部署。但是，若要执行此操作，需要部署至少一台运行满足上述要求的 Exchange 2013 的服务器。

<!-- end list -->

  - 问：是否可以退出新混合配置向导？  
    答：不可以。目前，新混合配置向导是在 Exchange 2010、Exchange 2013 和 Exchange 2016 中唯一受支持的向导。

<!-- end list -->

  - 问：是否可以使用新混合配置向导将当前的 Exchange 2010 混合配置升级到 Exchange 2013 或 Exchange 2016？  
    答：可以。确保至少有一台服务器满足当前混合配置向导要求，然后运行该服务器。该向导将会了解混合配置的当前状态，并无缝指导你完成升级过程。

