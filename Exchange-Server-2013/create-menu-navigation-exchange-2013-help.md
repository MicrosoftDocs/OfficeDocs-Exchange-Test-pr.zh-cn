---
title: '创建菜单导航: Exchange Online Help'
TOCTitle: 创建菜单导航
ms:assetid: 3cfc9a01-0a61-4d15-9561-621568dc30d9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997471(v=EXCHG.150)
ms:contentKeyID: 50490392
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.AutoAttendantKeyMappingControl
ms.translationtype: MT
---

# 创建菜单导航

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-05_

可以使用**新的菜单导航条目**页后，可以创建一个或多个键映射为企业或营业时间主菜单提示的自动助理。您可以定义在电话键盘上的键按下时，例如，将呼叫转移到分机号码或另一个自动助理将执行的操作。

有关与 UM 自动助理相关的更多管理任务，请参阅 [UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## EAC 用于配置 UM 自动助理的导航菜单

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在**UM 拨号计划**页的**UM 自动助理**下,，选择您要为其创建菜单导航的 UM 自动助理。在工具栏上，单击**编辑**![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在**UM 自动助理**页面上，单击**导航菜单**，选择**启用营业时间菜单导航**或**启用非营业时间菜单导航**，，然后单击**添加**![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在**新的菜单导航条目**页上，进行以下配置 ︰
    
      - **提示**  使用此框可以键入新的导航菜单的名称。导航菜单名称仅用于显示。这是必填的字段。
        
        因为您可能想要指定多个新的导航菜单，我们建议您使用您的键映射为有意义的名称。键的映射的名称的最大长度为 64 个字符，而且它可以包含空格。但是，它不能包含任何以下字符:"/ \\ \[\]:; |= , + \* ?\< \>。
    
      - **按下此键时**  使用此列表可以启用键映射。键的映射是调用方按需要执行特定操作的自动助理转发到另一个自动助理或运算符的调用方的数字键。默认情况下，定义没有条目。
        
        使用下拉列表选择调用方必须按下的数字键 （从 1 到 9)。自动助理运算符保留为零 (0)。
        
        如果从下拉列表中选择**超时**，它使调用程序可以被转移到分机号码或其他自动助理如果他们不在电话键盘上按任意键。例如，"请保持在线状态，并将下一个可用代表回答您的呼叫"。默认设置为 5 秒。如果您启用此选项，将创建空的键映射。
    
      - **播放以下音频文件**  使用此选项可以选择一个以前录制的音频文件的调用方。单击**更改**，然后单击**浏览**以找到该音频文件。
    
      - **执行此附加操作**   选择以下选项之一可定义您希望自动助理为呼叫者执行的操作。
        
          - **无**  如果您不希望自动助理转接呼叫到扩展或其他自动助理，或者将其保留用户的消息，请使用此选项。
        
          - **转到此分机**  选择此选项可启用呼叫转移到分机号码。如果您启用此选项，使用框中键入扩展名将其中转接呼叫。此字段允许仅包含数字字符。它不能包含任何以下字符:"/ \\ \[\]:; |= , + \* ?\< \>。
        
          - **转移到此 UM 自动助理**  选择此选项可将呼叫转给自动助理。单击**浏览**以找到要使用的自动助理。在启用此选项之前，您必须首先创建并配置自动助理。当您创建 UM 自动助理的父/子结构时，使用此选项。
        
          - **此用户的语音留言**  选择此选项以使调用方可以留下语音邮件用户位于同一拨号计划为要配置的 UM 自动助理。调用方从自动助理菜单中选择此选项，系统将提示他们留语音邮件时所选用户。单击**浏览**以定位已启用 UM 的用户。
        
          - **公布公司位置**  选择此选项可启用自动助理的菜单选项中选择，然后听到业务配置 UM 自动助理的位置的调用方。若要使此操作正确，您必须首先营业地点**营业地点**在框中输入 UM 自动助理**常规**页。
        
          - **公告的营业时间**  选择此选项可启用呼叫者选择自动助理的菜单选项，然后听到配置 UM 自动助理的业务操作的时间。若要使此操作正确，您必须首先配置 UM 自动助理**营业时间**页上的营业时间。

5.  单击\&quot;确定\&quot;可创建新的菜单导航。

6.  在\&quot;UM 自动助理\&quot;页面上，单击\&quot;保存\&quot;以保存您的更改。

## 使用 Shell 配置 UM 自动助理键映射

本示例启用营业时间键映射，以便 ︰

  - 当调用方按 1 时，它们将被转发到另一个名为`SalesAutoAttendant`的 UM 自动助理。

  - 当他们按 2 时，它们将被转发到分机号码 12345 寻求支持。

  - 当他们按 3 时，他们将发送到另一台将播放音频文件的自动助理。

<!-- end list -->

    Set-UMAutoAttendant -id MyAutoAttendant -BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

本示例设置在一个逗号分隔值 (.csv) 文件中定义的键映射。必须先创建.csv 文件具有以下标题和正确的条目 ︰ \< 键 \> \< 说明 \> \< 扩展 \> \[\< 自动助理名称 \>\] \< promptfilenamepath \> \[\< asrphrase1; asrphrase2 \>\]，\< leavevoicemailfor \> \< transfertomailbox \>。括号中的值是可选的。创建.csv 文件之后，将使用**Import-csv** cmdlet 的.csv 文件导入。

    $o = Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    Set-UMAutoAttendant MyAutoAttendant -BusinessHoursKeyMapping $o

本示例从现有 UM 自动助理的键映射导出到一个.csv 文件，然后再将相同的键映射导入到另一台 UM 自动助理。可以还将键映射导出到一个.csv 文件、 编辑或修改.csv 文件中的键映射，然后将这些密钥映射导入到另一台 UM 自动助理。

    $aa = Get-UMAutoAttendant -id MyAutoAttendant
    $aa1 = Get-UMAutoAttendant -id MyAutoAttendant2
    $aa.BusinessHoursKeyMapping | Export-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    $aa1.BusinessHoursKeyMapping = (Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv")

