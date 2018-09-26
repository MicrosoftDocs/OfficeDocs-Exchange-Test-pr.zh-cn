---
title: '管理 Exchange 2013 中的邮箱数据库: Exchange 2013 Help'
TOCTitle: 管理 Exchange 2013 中的邮箱数据库
ms:assetid: ead4a96b-1717-435b-bcfc-9901ac4e3b58
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150580(v=EXCHG.150)
ms:contentKeyID: 50491902
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理 Exchange 2013 中的邮箱数据库

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-04-29_

邮箱数据库是创建和存储邮箱的粒度的单位。邮箱数据库以 Exchange 数据库 (.edb) 文件的形式存储。在 Microsoft Exchange Server 2013 中，每个邮箱数据库均有可供配置的其自己的属性。

该主题显示了如何对 Microsoft Exchange Server 2013 中与管理邮箱数据库相联系的任务进行配置。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“邮箱数据库”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 创建邮箱数据库

## 使用 EAC 创建邮箱数据库

1.  从 Exchange 管理员中心中，导航至“服务器”。

2.  选择“数据库”，并单击“+”符号，创建数据库。

3.  使用新的数据库向导来创建数据库。

## 使用命令行管理程序创建邮箱数据库

有关如何创建邮箱数据的示例，请参阅 [New-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/aa997976\(v=exchg.150\)) 中的示例 1。

## 您如何知道这有效？

验证是否已成功创建了数据库，请执行以下操作：

  - 从 EAC 确认在“数据库”页上，是否列出了您创建的邮箱数据库。

  - 在命令行管理程序中，通过运行以下命令验证是否在服务器 Mailbox01 上创建了数据库。
    
    ```powershell
    Get-MailboxDatabase -Server "Mailbox01"
    ```

## 获得邮箱数据库属性

有关语法和参数的详细信息，请参阅 [Get-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb124924\(v=exchg.150\))。

## 使用命令行管理程序获取邮箱数据库属性

有关如何获取邮箱数据库属性的示例，请参阅 [New-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/aa997976\(v=exchg.150\)) 中的示例 2。

## 您如何知道这有效？

验证是否已成功检索了邮箱数据库信息，请执行以下操作：

从命令行管理程序，确认所有您的邮箱数据库信息是否正确。

## 设置邮箱数据库属性

## 使用 EAC 设置邮箱数据库属性

1.  从 EAC 中，导航至“服务器”。

2.  选择“数据库”，随后单击选择想要配置的邮箱数据库。

3.  单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")，配置邮箱数据库属性。

4.  使用“常规”选项卡可以查看有关邮箱数据库的状态，包括邮箱数据库路径、最后一个备份和邮箱数据库状态：
    
      - **数据库路径**   此只读字段为所选邮箱数据库显示 Exchange 2013 数据库 (.edb) 文件的完整路径。若要查看完整路径，可能必须单击该路径并使用右箭头键。无法使用此字段更改路径。要更改数据库文件的位置，可使用 [Move-DatabasePath](https://technet.microsoft.com/zh-cn/library/bb124742\(v=exchg.150\)) cmdlet。
    
      - **上次完整备份**   此只读字段显示邮箱数据库的上次完整备份的日期和时间。
    
      - **上次增量备份**   此只读字段显示邮箱数据库的上次增量备份的日期和时间。
    
      - **状态**   此只读字段显示是装入还是卸除邮箱数据库。
    
      - **装入服务器**   此只读字段显示在哪个服务器上装入了数据库。
    
      - **主机**   此只读字段显示邮箱数据库的主服务器。承载数据库活动副本的邮箱服务器称为“邮箱数据库主机”。
    
      - **主机类型**   此只读字段显示邮箱数据库主机的类型。
    
      - **修改时间**   此只读字段显示上次修改数据库的日期和时间。
    
      - **驻留此数据库副本的服务器**   此只读字段显示有此数据库副本的其他服务器。

5.  使用“维护”选项卡可以配置邮箱数据库设置，包括指定日记收件人、设置维护日程安排和启动时装入数据库：
    
      - “日记收件人”   单击“浏览”来指定收件人以启用该邮箱数据库上的日记。删除列出的收件人以禁用日记功能。
    
      - **维护日程安排**：使用此列表可以选择其中一个预先设置的维护日程安排。还可以配置自定义日程安排。若要配置自定义日程安排，请单击“自定义”。
    
      - **启用后台数据库维护(24 x 7 ESE 扫描)**   选中此复选框可以启用联机数据库扫描，该扫描在后台持续运行。联机数据库扫描执行数据库的校验和计算并执行允许 Exchange 扫描数据库上的丢失空间然后对其进行恢复的操作。如果选中此复选框，Exchange 扫描数据库的次数最多只有一天一次，如果无法在七天内完成扫描数据库，会发出警告。
    
      - **启动时不装入此数据库**：选中此复选框以阻止 Exchange 在其启动时装入此邮箱数据库。
    
      - **还原时可以覆盖此数据库**：选中此复选框以允许在还原进程期间覆盖邮箱数据库。
    
      - **启用循环日志记录**：选中此复选框以启用循环日志记录。

6.  使用“限制”选项卡可以指定邮箱数据库的存储限制、警告邮件间隔和删除设置：
    
      - “达到该限度时发出警告 (GB)”   选中此复选框将自动警告邮箱用户其邮箱已接近存储限制。若要指定存储限制，请选中该复选框，然后指定在向邮箱用户发送警告电子邮件之前可以在邮箱中存储多少内容，单位为 gigabyte (GB)。可以输入 0 到 2,097,151 MB (2.0 TB) 之间的值。
    
      - “达到该限度时禁止发送 (GB)”   选中此复选框可以在用户的邮箱大小达到指定的限制之后禁止用户发送新的电子邮件。若要指定此限制，请选中该复选框，再键入要在达到该值后则禁止发送新电子邮件并通知用户的邮箱大小，单位为 GB。可以输入 0 到 2,097,151 MB (2.0 TB) 之间的值。
    
      - “达到该限度时禁止发送和接收 (GB)”   选中此复选框可以在用户的邮箱大小达到指定的限制之后禁止用户发送和接收电子邮件。若要指定此限制，请选中该复选框，再键入要在达到该值后则禁止发送和接收电子邮件并通知用户的邮箱大小，单位为 GB。可以输入 0 到 2,097,151 MB (2.0 TB) 之间的值。
    
      - “保留已删除项目的期限(天)”   使用此复选框可以设置已删除项目保留在邮箱中的天数。可以输入 0 到 24,855 天之间的值。
    
      - “保留已删除邮箱的期限(天)”   使用此复选框可以设置已删除项目保留在邮箱中的天数。可以输入 0 到 24,855 天之间的值。
    
      - “在完成对数据库的备份之前不要永久删除项目”   在邮箱数据库已被备份之前，选中此复选框可以避免邮箱和电子邮件被永久删除。

7.  使用“客户端设置”选项卡，以选择邮箱的脱机通讯薄 (OAB)：
    
      - “脱机通讯薄”   要选择脱机通讯薄，单击“浏览”，随后选择脱机通讯薄。

## 使用命令行管理程序设置邮箱数据库属性

有关如何设置邮箱数据库属性的示例，请参阅 [Set-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb123971\(v=exchg.150\)) 中的示例 1。

## 您如何知道这有效？

验证是否已成功设置了属性，请执行以下操作：

  - 验证 EAC 中是否保存您的更改。

  - 从命令行管理程序执行以下命令，检索邮箱数据库属性。
    
    ```powershell
    Get-MailboxDatabase -Identity MailboxDatabase01 -Status | Format-List
    ```

## 转移邮箱数据库路径

有关语法和参数的详细信息，请参阅 [Move-DatabasePath](https://technet.microsoft.com/zh-cn/library/bb124742\(v=exchg.150\))。

## 使用命令行管理程序移动邮箱数据库路径

有关如何设置邮箱数据库属性的示例，请参阅 [Move-DatabasePath](https://technet.microsoft.com/zh-cn/library/bb124742\(v=exchg.150\)) 中的示例 1。

## 您如何知道这有效？

验证是否已成功转移了数据库路径，请执行以下操作：

1.  从 EAC 选择“服务器” \>“数据库”，然后单击选择恰当的邮箱。

2.  单击“pen” 符号，并确认数据库路径是否正确。

## 装入邮箱数据库

有关语法和参数的详细信息，请参阅 [Mount-Database](https://technet.microsoft.com/zh-cn/library/aa998871\(v=exchg.150\))。

## 使用命令行管理程序装载邮箱数据库

有关如何安装邮箱数据库的示例，请参阅 [Mount-Database](https://technet.microsoft.com/zh-cn/library/aa998871\(v=exchg.150\)) 中的示例 1。

## 您如何知道这有效？

验证是否已成功装载了邮箱数据库，请执行以下操作。

  - 从命令行管理程序执行以下命令，检索所有邮箱数据库的邮箱数据库属性。
    
    ```powershell
    Get-MailboxDatabase -IncludePreExchange2013
    ```

## 卸除邮箱数据库

有关语法和参数的详细信息，请参阅 [Dismount-Database](https://technet.microsoft.com/zh-cn/library/bb124936\(v=exchg.150\))。

## 使用命令行管理程序卸除邮箱数据库

有关如何卸载邮箱数据库的示例，请参阅 [Dismount-Database](https://technet.microsoft.com/zh-cn/library/bb124936\(v=exchg.150\)) 中的示例 1。

## 您如何知道这有效？

验证是否已成功卸除了数据库，请执行以下操作：

1.  从 EAC 选择“服务器” \>“数据库”，然后单击选择恰当的邮箱。

2.  单击“pen”符号，并确认数据库状态是否为“已卸除”。

## 删除邮箱数据库

## 使用 EAC 删除邮箱数据库

1.  从 EAC 选择“服务器” \>“数据库”，然后单击选择恰当的邮箱。

2.  单击“删除”![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")，以删除邮箱数据库。

## 使用命令行管理程序删除邮箱数据库

有关语法和参数的详细信息，请参阅 [Remove-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/aa997931\(v=exchg.150\))。

1.  运行以下命令来删除邮箱数据库 MyDatabase。
    
    ```powershell
    Remove-MailboxDatabase -Identity "MyDatabase"
    ```

2.  系统提示是否确实要执行该操作时，键入 **Y**。

3.  出现提示已成功删除数据库的对话框时，记下 Exchange 2013 数据库 (.edb) 文件的位置。如果要从硬盘驱动器中删除该文件，必须手动将其删除。

## 您如何知道这有效？

验证是否已成功删除了邮箱数据库，请执行以下操作：

  - 在 EAC 中，选择“服务器”\>“数据库”。

  - 确认邮箱数据库已被删除。

