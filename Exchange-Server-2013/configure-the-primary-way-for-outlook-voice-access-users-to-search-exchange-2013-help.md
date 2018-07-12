---
title: '配置 Outlook Voice Access 用户搜索的主要方式: Exchange Online Help'
TOCTitle: 配置 Outlook Voice Access 用户搜索的主要方式
ms:assetid: 3d93a037-5820-41d3-9206-69f534414daf
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997563(v=EXCHG.150)
ms:contentKeyID: 50490354
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置 Outlook Voice Access 用户搜索的主要方式

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-21_

创建统一邮件 (UM) 拨号计划时，您可以配置名称来查找用户拨打电话Outlook语音访问号码或有关联的拨号计划与 UM 自动助理时调用方可以搜索的主要和辅助的方法。调用方可以使用按键输入查找已启用 UM 的用户。

> [!NOTE]  
> <strong>任何</strong>不是主要的方法的调用方可以搜索名称的可用选项。当未选择<strong>任何</strong>他们可以搜索名称的辅助方式时，只的主要方式将提供给调用方。配置两个的主要和辅助方法调用方可以搜索名称，请为这两种方式都将会提示他们。


有关与 UM 拨号计划相关的其他管理任务，请参阅[UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 更改按名称拨号主要方法

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。

4.  在\&quot;设置\&quot;中的\&quot;用于搜索名称的主要方法\&quot;下，使用下拉列表选择需要的选项：
    
      - **姓 名**（默认值）
    
      - **名 姓**
    
      - **SMTP 地址**

5.  单击\&quot;保存\&quot;。

## 使用命令行管理程序更改按名称拨号主方法

本示例将名为`FirstLast`的方法设置主要拨。这样，调用方调用Outlook语音访问次数或 UM 自动助理与搜索启用 UM 的用户通过他们的名字和姓氏然后拨号计划相关联。

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary FirstLast

本示例将名为`LastFirst`的方法设置主要拨。这样，调用方调用Outlook语音访问次数或 UM 自动助理与搜索按其上次启用 UM 的用户，然后名字的拨号计划相关联。

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary LastFirst 

本示例将名为`SMTP address`的方法设置主要拨。这使呼叫者呼叫Outlook语音访问号码，或与来搜索他们的 SMTP 地址启用 UM 的用户的拨号计划关联的 UM 自动助理。

    Set-UMDialPlan -Identity MyUMDialPlan -DialByNamePrimary SMTPAddress

