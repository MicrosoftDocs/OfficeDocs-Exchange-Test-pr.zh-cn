---
title: '修改、 禁用或删除共享策略: Exchange 2013 Help'
TOCTitle: 修改、 禁用或删除共享策略
ms:assetid: 714af42d-ca29-4bb4-ac48-f0b3d4fd1c15
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657460(v=EXCHG.150)
ms:contentKeyID: 50490902
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 修改、 禁用或删除共享策略

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-02-15_

通过共享策略，Exchange 组织中的各个用户可以与其他联合 Exchange 组织、非联合 Exchange 组织以及各个 Internet 用户共享日历忙/闲信息。在正常操作过程中，您可能希望更改某些共享策略属性，例如修改共享规则、更改忙/闲访问级别、临时禁用共享策略或删除完整的共享策略。

要了解有关联合共享的详细信息，请参阅[共享](sharing-exchange-2013-help.md)

有关如何创建共享策略的详细信息，请参阅[创建共享策略](create-a-sharing-policy-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;日历和共享权限\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 修改共享策略

1.  导航到\&quot;组织\&quot;\>\&quot;共享\&quot;。

2.  在\&quot;单独共享\&quot;下，选择一个共享策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;共享策略\&quot;中，单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  在\&quot;共享规则\&quot;中，相应地修改共享规则。您可以更改一些设置，例如要与之共享信息的域及日历约会的共享级别。完成后，单击\&quot;保存\&quot;以关闭\&quot;共享规则\&quot;对话框。

5.  在\&quot;共享策略\&quot;中，单击\&quot;保存\&quot;以更新共享策略。

## 使用 EAC 将共享策略设置为默认共享策略

1.  导航到\&quot;组织\&quot;\>\&quot;共享\&quot;。

2.  在\&quot;单独共享\&quot;下，选择一个共享策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;共享策略\&quot;中，选中\&quot;将此策略作为我的默认共享策略\&quot;复选框。

4.  单击\&quot;保存\&quot;以更新共享策略。

## 使用 EAC 禁用共享策略

1.  导航到\&quot;组织\&quot; \>\&quot;分享\&quot;。

2.  在\&quot;单个共享\&quot;下选择共享策略。

3.  在\&quot;启用\&quot;列中，清除要禁用的共享策略对应的复选框。

## 使用 EAC 删除共享策略

> [!IMPORTANT]  
> 在删除某个共享策略之前，该共享策略必须从所有用户邮箱中删除。


1.  导航到\&quot;组织\&quot;\>\&quot;共享\&quot;。

2.  在\&quot;单个共享\&quot;下，选择一个共享策略，然后单击\&quot;删除\&quot;![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

3.  在警告框中，单击\&quot;是\&quot;删除共享策略。

## 使用命令行管理程序修改、禁用或删除共享策略

  - 本示例修改组织的外部域 contoso.com 的共享策略 Contoso。此策略允许 Contoso 域中的用户查看简单的忙/闲信息。
    
    ```powershell
    Set-SharingPolicy -Identity Contoso -Domains 'sales.contoso.com: CalendarSharingFreeBusySimple'
    ```

  - 此示例将第二个域添加到共享策略 Contoso。将域添加到现有策略时，必须包括任何以前包括的域。
    
    ```powershell
        Set-SharingPolicy -Identity Contoso -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'atlanta.contoso.com: CalendarSharingFreeBusyReviewer', 'beijing.contoso.com: CalendarSharingFreeBusyReviewer'
    ```
    
  - 此示例将共享策略 Contoso 设置为默认共享策略。
    
    ```powershell
    Set-SharingPolicy -Identity Contoso -Default $True
    ```

  - 此示例禁用共享策略 Contoso。
    
    ```powershell
    Set-SharingPolicy -Identity "Contoso" -Enabled $False
    ```

  - 第一个示例删除共享策略 Contoso。第二个示例删除共享策略 Contoso，并且禁止显示对要删除策略的确认。
      
    ```powershell
    Remove-SharingPolicy -Identity Contoso
    ```

    ```powershell
    Remove-SharingPolicy -Identity Contoso -Confirm
    ```
      
      
有关语法和参数的详细信息，请参阅 [Set-SharingPolicy](https://technet.microsoft.com/zh-cn/library/dd297931\(v=exchg.150\)) 和 [Remove-SharingPolicy](https://technet.microsoft.com/zh-cn/library/dd351071\(v=exchg.150\))。

