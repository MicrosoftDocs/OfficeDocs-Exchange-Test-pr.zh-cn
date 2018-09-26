---
title: '使用克隆的配置来配置边缘传输服务器: Exchange 2013 Help'
TOCTitle: 使用克隆的配置来配置边缘传输服务器
ms:assetid: 0bbc83e3-e5e8-4480-a8a6-15f035360856
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996008(v=EXCHG.150)
ms:contentKeyID: 61183385
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用克隆的配置来配置边缘传输服务器

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-13_

您可以使用所提供的 Exchange 命令行管理程序脚本（位于 %ExchangeInstallPath%Scripts 中）来复制边缘传输服务器的配置。此过程称为*“克隆配置”*。*“克隆配置”*是根据以前配置的源服务器的配置信息部署新的边缘传输服务器的操作。即将以前配置的源服务器的配置信息复制并导出到 XML 文件，然后导入目标服务器。有关该过程的概述，请参阅[边缘传输服务器克隆配置](edge-transport-server-cloned-configuration-exchange-2013-help.md)。

边缘传输服务器配置信息存储在 Active Directory 轻型目录服务 (AD LDS) 中，而且不在多个边缘传输服务器之间进行复制。通过克隆配置，您可以确保在外围网络中部署的每个边缘传输服务器都使用相同的配置。

有两个命令行管理程序脚本可用于执行下列克隆配置任务：

  - **ExportEdgeConfig.ps1**   从边缘传输服务器导出用户配置的所有设置和数据，并将这些数据存储在 XML 文件中。

  - **ImportEdgeConfig.ps1**   在验证配置步骤中，ImportEdgeConfig.ps1 脚本将检查导出的 XML 文件，来确定服务器特定的导出设置对目标服务器是否有效。如果需要修改这些设置，则脚本会将无效设置写入到一个应答文件中，您可以修改该文件以指定在导入配置步骤中使用的目标服务器信息。在导入配置步骤中，该脚本将导入由 ExportEdgeConfig.ps1 脚本创建的中间 XML 文件中存储的所有用户配置设置和数据。

这两个脚本位于 %ExchangeInstallPath%Scripts 文件夹中。

## 开始之前

  - 估计完成该任务的时间：30 分钟。

  - [邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅“边缘传输服务器”条目。

  - 克隆配置不会复制服务器的边缘订阅设置。EdgeSync 证书未克隆。需要对每个边缘传输服务器单独运行 EdgeSync 进程。EdgeSync 覆盖包含在克隆配置信息和 EdgeSync 复制信息中的相应设置。

  - 如果将任何发送连接器配置为使用凭据，则密码将以加密字符串的形式写入到中间 XML 文件。可在 ImportEdgeConfig.ps1 和 ExportEdgeConfig.ps1 脚本中使用 *-key* 参数来指定用于密码加密和解密的 32 字节字符串。如果不使用 *-key* 参数，则使用默认加密密钥。

  - 只能使用命令行管理程序执行此过程。若要了解如何在本地 Exchange 组织中打开 Exchange 命令行管理程序，请参阅[打开命令行管理程序](https://technet.microsoft.com/zh-cn/library/dd638134\(v=exchg.150\))。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您该如何做？

## 步骤 1：将源服务器配置数据导出到源服务器上的一个文件中。

1.  将 ExportEdgeConfig.ps1 脚本复制到源服务器上用户配置文件的根文件夹中。

2.  要将源服务器配置数据导出到源服务器上的一个文件中，请使用以下语法。
    
    ```powershell
    ./ExportEdgeConfig.ps1 -CloneConfigData:"<configuration file>"
    ```
    
    例如，要将源服务器配置数据导出到文件 C:\\CloneConfigData.xml 中，请运行以下命令。
    
    ```powershell
    ./ExportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml"
    ```

## 您如何知道此步骤有效？

当确认消息“边缘配置数据已成功导出到: \<输出文件路径\>”出现时，即表示您已成功将源配置数据导出到文件中。

## 步骤 2：验证配置文件并在目标服务器上创建一个应答文件

1.  将您在上一步中导出的源服务器配置文件复制到目标边缘传输服务器中。

2.  将 ImportEdgeConfig.ps1 脚本复制到目标服务器上用户配置文件的根文件夹中。

3.  要验证配置文件并使用结果在目标服务器上创建应答文件，请使用以下语法。
    
    ```powershell
        ./ImportEdgeConfig.ps1 -CloneConfigData:"<configuration file>" -IsImport $false -CloneConfigAnswer:"<answer file>"
    ```

    例如，要验证配置文件 C:\\CloneConfigData.xml 并创建应答文件 C:\\CloneConfigAnswer.xml，请运行以下命令。
    
    ```powershell
        ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $false -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"
    ```

4.  打开应答文件并修改对目标服务器无效的所有设置。如果不需要修改，则应答文件将不会包含任何条目。保存所做的更改。

## 您如何知道此步骤有效？

当确认消息“已成功创建应答文件”出现时，即表示您已成功验证配置文件并创建应答文件。

## 步骤 3：在目标服务器上导入配置文件

要在目标服务器上导入配置文件，请使用以下语法。

```powershell
    ./ImportEdgeConfig.ps1 -CloneConfigData:"<Configuration file>" -IsImport $true -CloneConfigAnswer:"<answer file>"
```

例如，要使用应答文件 C:\\CloneConfigAnswer.xml 导入配置文件 C:\\CloneConfigData.xml，请运行以下命令。

```powershell
    ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $true -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"
```

## 您如何知道此步骤有效？

当确认消息“已成功导入边缘配置信息”出现时，即表示您已在目标服务器上成功导入配置文件。

