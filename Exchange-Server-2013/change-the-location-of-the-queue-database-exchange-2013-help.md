---
title: '更改队列数据库的位置: Exchange 2013 Help'
TOCTitle: 更改队列数据库的位置
ms:assetid: f170cb0c-04a9-4fa7-b594-206e3a787e14
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125177(v=EXCHG.150)
ms:contentKeyID: 51408290
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 更改队列数据库的位置

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

*队列*是临时存放等待进入下一个处理阶段的邮件的位置。每个队列代表传输服务器按照特定顺序处理的逻辑邮件集。

Microsoft Exchange Server 2013 与 Exchange 之前的版本类似，使用可扩展存储引擎 (ESE) 数据库存储队列邮件。所有不同的队列都存储在一个 ESE 数据库中。队列仅存在于邮箱服务器或边缘传输服务器上。

队列数据库和队列数据库事务日志的位置由 `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML 应用程序配置文件中的键控制。此文件与 Microsoft Exchange 传输服务相关联。下表对每个键进行了详细的说明。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>键</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p>该键指定队列数据库文件的位置。文件包括：</p>
<ul>
<li><p>Mail.que</p></li>
<li><p>Trn.chk</p></li>
</ul>
<p>默认位置为 <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p>该键指定队列数据库事务日志文件的位置。文件包括：</p>
<ul>
<li><p>Trn.log</p></li>
<li><p>Trntmp.log</p></li>
<li><p>Trn<em>nnn</em>.log</p></li>
<li><p>Trnres00001.jrs</p></li>
<li><p>Trnres00002.jrs</p></li>
<li><p>Temp.edb</p></li>
</ul>
<p>请注意，启动 Microsoft Exchange 传输服务时，将使用 Temp.edb 验证队列数据库架构。尽管 Temp.edb 不是事务日志文件，但它保留在与事务日志文件相同的位置。</p>
<p>默认位置为 <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>。</p></td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟。

  - Exchange 权限不适用于本主题中的过程。这些过程在 Exchange Server 的操作系统中执行。

  - 停止或重新启动 Microsoft Exchange 传输服务时，会中断服务器上的邮件流。

  - 更改队列数据库或事务日志的位置时，不会移动现有队列数据库和事务日志文件。在新位置新建队列数据库和事务日志。现有的文件将保留在旧位置。但是，不再使用这些数据库文件。如果要在新位置复用现有队列数据库或事务日志文件，必须在 Microsoft Exchange 传输服务停止之后，在服务启动之前，将现有文件移动到新位置。

  - 如果队列数据库或事务日志的目标文件夹不存在，那么，如果父文件夹应用了下列权限，就会创建该目标文件夹：
    
      - 网络服务：完全控制
    
      - 系统：完全控制
    
      - 管理员：完全控制

  - 在您安装 Exchange 累积更新 (CU) 时，您在 Exchange XML 应用程序配置文件（例如，客户端访问服务器上的 web.config 文件，或邮箱服务器上的 EdgeTransport.exe.config 文件）中针对每个服务器所做的任何自定义设置都将被覆盖。请务必保存此类信息，以便在安装累积更新后，您可以轻松地重新配置服务器。安装 Exchange CU 后，您必须重新配置这些设置。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您想执行什么操作？

## 使用命令提示符在新位置创建新队列数据库和事务日志

1.  创建用于保存队列数据库和事务日志的文件夹。确保向该文件夹应用适当的权限。

2.  在命令提示符窗口中，通过运行以下命令在记事本中打开 EdgeTransport.exe.config 文件：
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
```

3.  修改 `<appSettings>` 部分中的以下键。
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    例如，若要在 D:\\Queue\\QueueDB 中创建新的队列数据库，在 D:\\Queue\\QueueLogs 中创建新的事务日志，请使用以下值：
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  完成后，保存并关闭 EdgeTransport.exe.config 文件。

5.  通过运行以下命令重新启动 Microsoft Exchange 传输服务：
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## 您如何知道操作成功？

若要验证是否在新位置成功新建了队列数据库和事务日志，请执行以下操作：

1.  验证新位置处是否存在新的数据库文件 Mail.que 和 Trn.chk。

2.  验证新位置处是否存在新的事务日志文件 Trn.log、Trntmp.log、Trnres00001.jrs、Trnres00002.jrs 和 Temp.edb 文件。

3.  如果可以在 Microsoft Exchange 传输服务启动之后从旧位置删除旧的队列数据库和事务日志文件，那么将无法使用这些文件。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您想执行什么操作？

## 使用命令提示符将现有队列数据库和事务日志移动到新位置

仅当出现未正常关闭 Microsoft Exchange 传输服务，或者出现硬盘驱动器故障的灾难恢复情况时，才需要还原并重新定位现有的队列数据库及其现有的事务日志。

正常情况下，没有必要复用现有的事务日志。正常关闭 Microsoft Exchange 传输服务会将所有未提交的事务日志条目写入队列数据库。此外，使用了循环日志记录，因此，包含以前提交的数据库更改的事务日志将不保留。

使用以下步骤将现有队列数据库和事务日志移动到新位置：

1.  创建用于保存队列数据库和事务日志的文件夹。确保向该文件夹应用适当的权限。

2.  在命令提示符窗口中，通过运行以下命令在记事本中打开 EdgeTransport.exe.config 文件：
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
```

3.  修改 `<appSettings>` 部分中的以下键：
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    例如，若要将队列数据库的位置更改为 D:\\Queue\\QueueDB，将事务日志的位置更改为 D:\\Queue\\QueueLogs，请使用以下值：
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  完成后，保存并关闭 EdgeTransport.exe.config 文件。

5.  通过运行以下命令停止 Microsoft Exchange 传输服务：
    
    ```powershell
net stop MSExchangeTransport
```

6.  将现有数据库文件 Mail.que 和 Trn.chk 从原始位置移动到新位置。

7.  将现有事务日志文件 Trn.log、Trntmp.log、Trn*nnnnn*.log、Trnres00001.jrs、Trnres00002.jrs 和 Temp.edb 从旧位置移动到新位置。

8.  通过运行以下命令启动 Microsoft Exchange 传输服务：
    
    ```powershell
net start MSExchangeTransport
```

## 您如何知道操作成功？

若要验证是否成功将现有队列数据库和事务日志移动到新位置，请执行以下操作：

1.  验证新位置处是否存在队列数据库文件 Mail.que 和 Trn.chk。

2.  验证新位置处是否存在事务日志文件 Trn.log、Trntmp.log、Trnres00001.jrs、Trnres00002.jrs 和 Temp.edb 文件。

3.  确认原始位置是否没有队列数据库或事务日志文件。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您想执行什么操作？

