---
title: '为邮箱数据库配置循环日志记录: Exchange 2013 Help'
TOCTitle: 为邮箱数据库配置循环日志记录
ms:assetid: 29cbd7cd-382b-4e0d-8368-2e49e75df2fc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn756374(v=EXCHG.150)
ms:contentKeyID: 62524848
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为邮箱数据库配置循环日志记录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-06-24_

当您对邮箱数据库启用循环日志时，您获得的循环日志类型取决于该邮箱数据库是否是使用连续复制进行复制的：

  - 如果该邮箱数据库未被复制，它将使用 JET 循环日志。在这种情况下，启用或禁用 JET 循环日志将需要卸载和加载数据库。

  - 如果邮箱数据库已被复制，它将使用连续复制循环日志 (CRCL)。在这种情况下，启用或禁用 CRCL 将会动态生效；无需卸载和重新加载数据库。

关于循环日志和 CRCL 的详细信息，请参阅 [Exchange Native Data Protection](backup-restore-and-disaster-recovery-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 预计完成时间：1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md) 主题中的“邮箱数据库权限”条目。

## 使用 EAC 为数据库配置循环日志。

1.  在 EAC 中，转到“服务器”\>“数据库”。

2.  选择您想进行配置的邮箱数据库，然后单击 ![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  选中或取消选中“启用循环日志”，然后单击“保存”。

4.  如果需要执行卸载或加载操作，会出现一个警告消息。单击“确定”关闭该警告消息。
    
    1.  要卸载该数据库，单击“更多”![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标")，然后单击“卸载”。当警告消息出现时，单击“是”。
    
    2.  要加载该数据库，单击“更多”![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标")，然后单击“加载”。当警告消息出现时，单击“是”。

## 使用 Shell 为数据库配置循环日志。

本示例启用了数据库 DB1 的循环日志。

```powershell
Set-MailboxDatabase DB1 -CircularLoggingEnabled $True
```

本示例禁用了数据库 DB1 的循环日志。

```powershell
Set-MailboxDatabase DB1 -CircularLoggingEnabled $False
```

有关您可以配置的其他邮箱数据库参数，请参阅[Set-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb123971\(v=exchg.150\))。

