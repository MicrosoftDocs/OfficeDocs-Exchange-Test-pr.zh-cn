---
title: 与部署相关的步骤
TOCTitle: 与部署相关的步骤
ms:assetid: 6b7682bd-fe3d-43b9-a7db-66c0ac17656f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn195909(v=EXCHG.150)
ms:contentKeyID: 53275721
ms.author: dstrome
ms.date: 04/03/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 与部署相关的步骤

 

_**上一次修改主题：** 2013-04-17_

此部分包含您在使用 Exchange Server 2013 管理包时可用作参考的步骤。有关与部署后操作相关的步骤，请参阅[Procedures related to post-deployment operation](procedures-related-to-post-deployment-operation.md)。

## 验证代理部署状态

在导入 Exchange Server 2013 管理包之前，请验证 Exchang 服务器上的 SCOM 代理是否可以正常运行，以及是否可以在 SCOM 中正确报告操作系统运行状况。

您的用户帐户必须是 Operations Manager Administrators 角色的成员，才能执行此流程。

1.  登录 SCOM 服务器并开启 SCOM 控制台。

2.  单击“监视”，然后单击“Windows 计算机”。

3.  确保所有 Exchange 服务器的运行状况均显示为“Healthy”。

![SCOM 控制台中的正常代理](images/Dn195909.7d1ff0bb-419e-40dc-babf-5fa2fb7229a8(EXCHG.150).png "SCOM 控制台中的正常代理")

## 验证代理程序配置

在导入 Exchange Server 2013 管理包之前，验证 SCOM 中是否已启用代理程序发现。否则，Exchange 服务器上的代理不会报告 Exchange 的运行状况。您需要对所有 Exchange 服务器验证此配置。

您的用户帐户必须是 Operations Manager Administrators 角色的成员，才能执行此流程。

1.  登录 SCOM 服务器并开启 SCOM 控制台。

2.  在操作控制台中，单击“管理”。

3.  单击“代理管理”，用鼠标右键单击 Exchange 服务器，然后选择“属性”。

4.  在“安全”选项卡，验证是否已选中“允许此代理充当代理程序并发现其他计算机上的托管对象”复选框。

5.  单击“确定”。

## 验证代理安全配置

由于 Exchange 2013 已在此安全模型下进行测试，因此不支持在除“LocalSystem”以外的任意帐户下在 Exchange 服务器上运行 SCOM 代理。如果在除 LocalSystem 外的任意帐户下运行此代理，综合事务将无法运行。您也许还会遇到其他一些问题。

您的用户帐户必须是 Server Management 角色组的成员，才能执行此流程。

1.  登录到您的 Exchange 服务器。

2.  单击“开始”\>“管理工具”\>“服务”。

3.  向下滚动服务列表，找到“System Center Management”服务。

4.  验证“登录身份”栏是否显示“本地系统”。

5.  如果“登录身份”栏显示的是其他信息，将登录服务更改为本地系统。
    
    1.  右键单击“System Center Management”服务并选择“属性”。
    
    2.  选择“登录”选项卡。
    
    3.  单击“本地系统帐户”选项。
    
    4.  单击“确定”。

