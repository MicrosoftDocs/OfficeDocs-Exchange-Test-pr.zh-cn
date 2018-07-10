---
title: '操作系统处于调试 mode_OSCheckedBuild: Exchange 2013 Help'
TOCTitle: 操作系统处于调试 mode_OSCheckedBuild
ms:assetid: 93a1380f-1388-494d-8f78-92dfefd069bd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.oscheckedbuild(v=EXCHG.150)
ms:contentKeyID: 50491046
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 操作系统处于调试 mode\_OSCheckedBuild

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-15_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 分析器工具查询**Win32\_OperatingSystem** Microsoft Windows 管理规范 (WMI) 类，以确定是否为**调试**属性设置值。如果 Exchange Server 计算机上的此项的值设置为**True**，则显示错误。

通过在 Boot.ini 文件中添加**/debug**参数切换 Windows 调试模式。当 Windows Server 计算机的 Boot.ini 文件中指定**调试**时，内核调试程序是在启动过程中加载并一直保留在内存中。这样，以拨入到所调试的系统，即使在内核停止屏幕不挂起系统中断到调试器中，技术支持专业人员。与**/crashdebug**开关，不同**/debug**开关是否正在调试或不使用的 COM 端口。在调试定期出现的问题时使用此开关。很**可能/调试**参数设置作为一种手段来解决问题，而意外地设置。

正在运行的其他进程，因此性能受到严重的影响。因此，不建议，在调试模式下运行 Windows 的计算机上运行 Exchange Server。

要消除此错误，请编辑 Boot.ini 文件并删除 **/debug** 参数。

## 更正此错误

1.  在 Windows 资源管理器中，导航到系统分区。这是装有 NTLDR Boot.ini 等硬件特定文件的分区。

2.  如果您看不到 Boot.ini 文件，它可能是由于**文件夹选项**设置为**隐藏受保护的操作系统文件**。这种情况下，在 Windows 资源管理器窗口中，单击**工具**，单击**文件夹选项**，然后单击**查看**。清除**隐藏受保护的操作系统文件 （推荐）**复选框。出现提示时，请单击**是**。

3.  当 Boot.ini 文件显示在 Windows 资源管理器中后，用鼠标右键单击该文件，再单击\&quot;打开方式\&quot;，然后选择\&quot;记事本\&quot;打开该文件。

4.  在 **Operating Systems** 部分，删除 **/debug** 参数。

5.  保存并关闭文件，然后重新启动 Exchange Server 计算机，以使更改生效。

有关可以在 Boot.ini 文件中使用的参数的详细信息，请参阅 Microsoft 知识库文章 833721，"Windows XP 和 Windows Server 2003 Boot.ini 文件的可用开关选项"([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=833721](https://go.microsoft.com/fwlink/?linkid=3052&kbid=833721))。

