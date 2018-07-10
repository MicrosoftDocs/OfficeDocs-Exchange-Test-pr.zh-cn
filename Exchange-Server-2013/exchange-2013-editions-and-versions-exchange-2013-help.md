---
title: 'Exchange 2013：版次和版本: Exchange 2013 Help'
TOCTitle: Exchange 2013：版次和版本
ms:assetid: b563b543-fb3f-4465-9a54-cbfd680aee1f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232170(v=EXCHG.150)
ms:contentKeyID: 50556663
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013：版次和版本

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

Microsoft Exchange Server 2013 有两种服务器版本：标准版和企业版。企业版可以在正式发布 (RTM) 版本和累计更新 1 (CU1) 版本中扩展到为每个服务器装入 50 个数据库，而在累计更新 2 (CU2) 版本和更高版本中扩展到为每个服务器装入 100 个数据库；标准版限制在每个服务器中装入 5 个数据库。装入数据库是正在使用的数据库。装入数据库可以是装入以供客户端使用的活动邮箱数据库，或者是在恢复中装入以便用于日志复制和重播的被动邮箱数据库。虽然您可以创建多于以上限值的数据库，但您只能装入以上指定的最大数量的数据库。恢复数据库不计入该限值。

这些是由产品密钥定义的许可版本。输入有效的授权产品密钥后，就为服务器建立了受支持的版本。产品密钥仅可用于相同版本密钥的交换和升级；产品密钥不可用于降级。可使用有效的产品密钥从 Exchange 2013 的评估版（试用版）移动到标准版或企业版。也可使用有效的产品密钥从标准版移动到企业版。

还可以使用相同版本的产品密钥再次授权服务器。例如，如果您有两台具有两个不同密钥的标准版服务器，但意外对两台服务器使用了同一个密钥，则可以将其中一台服务器的密钥更改为颁发给您的另一个密钥。无须重新安装或重新配置任何内容即可执行上述操作。输入产品密钥并重新启动 Microsoft Exchange 信息存储服务后，与该产品密钥对应的版本就会得到反映。

在试用版过期时不会丢失功能，因此您的实验室、演示、培训和其他非生产环境可以继续维持 120 天，不用重新安装 Exchange 2013 的试用版。

如前面提到的，不能使用产品密钥从企业版降级到标准版，也不能使用产品密钥将企业版或标准版还原为试用版。上述类型的降级仅可通过卸载 Exchange 2013 后重新安装 Exchange 2013 并输入正确的产品密钥才能实现。

## Exchange 2013 版本

要查看 Exchange 2013 版本列表以及如何下载和升级到 Exchange 2013 最新版本的信息，请参阅以下主题：

  - [Exchange Server 更新：内部版本号和发行日期](https://technet.microsoft.com/zh-cn/library/hh135098\(v=exchg.150\))

  - [将 Exchange 2013 升级到最新累积更新或 Service Pack](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)

若要查看您正在运行的 Exchange 2013 版本的内部版本号，请在 Exchange 命令行管理程序中运行以下命令。

    Get-ExchangeServer | fl name,edition,admindisplayversion

## Exchange 2013 许可证类型

Exchange 2013 在服务器/客户端访问许可证 (CAL) 模型中进行授权，与 Exchange 2010 的授权方式类似。下面介绍了许可证的类型：

  - **服务器许可证**   必须为正在运行的服务器软件的每个实例分配一个许可证。销售的服务器许可证有两种服务器版本：标准版和企业版。

  - **客户端访问许可证 (CAL)**   Exchange 2013 还提供了两种客户端访问许可证 (CAL) 版本，称为标准版 CAL 和企业版 CAL。您可以混合匹配服务器版本和 CAL 类型。例如，可以将企业版 CAL 用于 Exchange 2013 标准版。同样，可以将标准版 CAL 用于 Exchange 2013 企业版。

有关 Exchange 许可证类型的详细信息，请参阅[许可](https://go.microsoft.com/fwlink/p/?linkid=392675)。

