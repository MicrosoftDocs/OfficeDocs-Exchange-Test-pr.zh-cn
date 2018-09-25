---
title: '查看邮件记录管理的性能计数器: Exchange 2013 Help'
TOCTitle: 查看邮件记录管理的性能计数器
ms:assetid: ec374d31-2797-4f8b-8c96-3839d01a662c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb397227(v=EXCHG.150)
ms:contentKeyID: 51408294
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 查看邮件记录管理的性能计数器

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2009-12-09_

您可以使用 Windows 可靠性和性能监视器 (Perfmon.exe) 来选择和查看邮件记录管理 (MRM) 的性能计数器。通过使用性能计数器，您可以在托管文件夹助理运行非常耗费资源的 MRM 过程的同时对其进行监视。

有关 MRM 性能计数器的列表，请参阅[可用于邮件记录管理的性能计数器](performance-counters-for-https://technet.microsoft.com/zh-cn/library/dd335093(v=exchg.150))。

要查找与监视 MRM 相关的其他任务吗？请查看[监视邮件记录管理](monitoring-https://technet.microsoft.com/zh-cn/library/dd335093(v=exchg.150))。

## 使用 Windows 可靠性和性能监视器查看 MRM 性能计数器

要执行此步骤，必须为您使用的帐户委派本地 Administrators 组中的成员身份。

1.  若要启动 Windows 可靠性和性能监视器，请依次单击“开始”、**“运行”**，然后键入 **perfmon**。

2.  在控制台树中，导航到“监视工具”\>“性能监视器”。

3.  单击工具栏上的加号 (+) 按钮。将显示“添加计数器”对话框。

4.  从“从计算机选择计数器”列表中，选择下列选项之一：
    
      - 如果要在本地计算机上执行此步骤，请选择“\<本地计算机\>”。此为默认选项。
    
      - 如果要远程执行此步骤，请选择要监视的服务器。

5.  在性能计数器列表中，展开“MSExchange 助理 - 每个数据库”或“MSExchange 托管文件夹助理”。

6.  选择要监视的性能计数器。

7.  对于“MSExchange 助理 - 每个数据库”下的性能计数器，要查看所有邮箱数据库的计数器，请在“选定对象的实例”中单击“所有实例”。或者，要指定一个或多个邮箱数据库，请从列表中选择实例。

8.  要添加选择的计数器以便计数器出现在 Windows 可靠性和性能监视器中，并开始收集性能数据，单击“添加”。

