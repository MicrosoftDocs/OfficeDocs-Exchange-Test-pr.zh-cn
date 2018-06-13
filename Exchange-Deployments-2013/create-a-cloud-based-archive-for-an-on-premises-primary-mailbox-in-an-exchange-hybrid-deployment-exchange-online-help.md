---
title: '在 Exchange 混合部署中为本地主邮箱创建基于云的存档: Exchange Online Help'
TOCTitle: 在混合部署中为本地主邮箱创建基于云的存档
ms:assetid: ecc0a687-6c05-47bd-a079-a43d83cba9ea
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt791517(v=EXCHG.150)
ms:contentKeyID: 74253088
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Exchange 混合部署中为本地主邮箱创建基于云的存档

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2017-01-20_

在 Exchange 混合部署中，可以在 Exchange Online 中为本地主邮箱配置基于云的存档邮箱。

第 1 步：为本地主邮箱启用基于云的存档邮箱

第 2 步：验证是否已创建基于云的存档邮箱

（可选）运行目录同步

## 开始之前

  - 拥有本地主邮箱的用户必须是 Office 365 组织中的用户帐户。

  - Office 365 用户帐户必须分配有 Exchange Server 适用的 Exchange Online Archiving 许可证。第 1 步中的过程包含分配许可证的步骤。

  - 在第 1 步中启用基于云的存档邮箱后，最长可能要等 30 分钟，基于云的存档邮箱才能完成预配。这是因为基于云的存档邮箱是在目录同步期间创建。在此期间，本地 Active Directory 与 Office 365 中的 Azure Active Directory (Azure AD) 同步。默认情况下，每 30 分钟运行一次目录同步。

## 第 1 步：为本地主邮箱启用基于云的存档邮箱

若要为本地主邮箱启用基于云的存档邮箱，请按以下任意一个过程操作。在本地 Exchange 组织的 Exchange 管理中心 中和 Office 365 管理中心 中按以下步骤操作。

为新用户创建基于云的存档邮箱

为现有用户创建基于云的存档邮箱

## 为新用户创建基于云的存档邮箱

1.  在本地组织的 EAC 中，依次转到\&quot;**收件人**\&quot;\>\&quot;**邮箱**\&quot;。

2.  依次单击\&quot;**新建**![添加图标](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")\&quot;\>\&quot;**用户邮箱**\&quot;。

3.  在\&quot;**新建用户邮箱**\&quot;页上，为新用户或现有用户创建邮箱。若要详细了解如何创建用户邮箱，请参阅[创建用户邮箱](https://technet.microsoft.com/zh-cn/library/jj991919\(v=exchg.150\))。

4.  单击\&quot;**更多选项**\&quot;，启用基于云的存档邮箱。

5.  在\&quot;**存档**\&quot;下，单击选中\&quot;**为此用户创建就地存档**\&quot;复选框，然后单击\&quot;**基于云的存档**\&quot;。此时，系统会显示要预配存档邮箱的域名。
    
    ![在\&quot;存档\&quot;下，单击选中复选框，然后单击\&quot;基于云的存档\&quot;](images/Mt791517.43d0473e-30ad-4021-94bc-a9c5449f43ba(EXCHG.150).png "在&quot;存档&quot;下，单击选中复选框，然后单击&quot;基于云的存档&quot;")  

6.  单击\&quot;**保存**\&quot;，创建邮箱和基于云的存档。
    
    请注意，在\&quot;**邮箱**\&quot;页上，选定邮箱的\&quot;**邮箱类型**\&quot;列中显示值\&quot;**用户(存档)**\&quot;。

7.  最长可能要等 30 分钟，目录同步才能完成。完成后才能在 Office 365 中创建相应的用户帐户。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ659053.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在 Office 365 管理中心 中，依次转到&amp;quot;<strong>运行状况</strong>&amp;quot;&gt;&amp;quot;<strong>目录同步状态</strong>&amp;quot;，查看上次目录同步时间。</td>
    </tr>
    </tbody>
    </table>


8.  在确认本地邮箱新建后已进行过目录同步后，在 Office 365 管理中心 中，依次转到\&quot;**用户**\&quot;\>\&quot;**活动用户**\&quot;，然后选择为新本地邮箱创建的新 Office 365 用户帐户。

9.  在随即显示的用户属性页上，单击\&quot;**产品许可证**\&quot;部分中的\&quot;**编辑**\&quot;。
    
    ![单击细节窗格中的\&quot;编辑\&quot;，向选定用户分配许可证](images/Mt791517.383a9068-53cb-420a-a05e-823e8b5a2c25(EXCHG.150).png "单击细节窗格中的&quot;编辑&quot;，向选定用户分配许可证")  

10. 在\&quot;**位置**\&quot;下拉菜单下，选择用户的位置。

11. 展开 Office 365 企业许可证列表，然后分配\&quot;**Exchange Server 适用的 Exchange Online Archiving**\&quot;许可证，并保存更改。
    
    此时，在用户列表的\&quot;**状态**\&quot;列中，你会发现许可证已分配给用户。

12. 同样，最长可能要等 30 分钟，目录同步才能完成。完成后才能预配基于云的存档邮箱。转到第 2 步，了解如何确认基于云的存档邮箱是否已创建。创建存档邮箱后，用户可以使用 Outlook 或 Web 上的 Outlook 对其进行访问。

返回顶部

## 为现有用户创建基于云的存档邮箱

1.  在 Office 365 管理中心 中，依次转到\&quot;**用户**\&quot;\>\&quot;**活动用户**\&quot;，然后选择要为其创建基于云的存档邮箱的用户帐户。

2.  在随即显示的用户属性页上，单击\&quot;**产品许可证**\&quot;部分中的\&quot;**编辑**\&quot;。
    
    ![单击细节窗格中的\&quot;编辑\&quot;，向选定用户分配许可证](images/Mt791517.383a9068-53cb-420a-a05e-823e8b5a2c25(EXCHG.150).png "单击细节窗格中的&quot;编辑&quot;，向选定用户分配许可证")  

3.  在\&quot;**位置**\&quot;下拉菜单下，选择用户的位置。

4.  展开 Office 365 企业许可证列表，然后分配\&quot;**Exchange Server 适用的 Exchange Online Archiving**\&quot;许可证，并保存更改。
    
    此时，在用户列表的\&quot;**状态**\&quot;列中，你会发现许可证已分配给用户。

5.  在本地组织的 EAC 中，依次转到\&quot;**收件人**\&quot;\>\&quot;**邮箱**\&quot;。

6.  在邮箱列表中，选择刚刚向其分配许可证的用户。

7.  在详细信息窗格中的\&quot;就地存档\&quot;下，单击\&quot;启用\&quot;。
    
    ![单击细节窗格中的\&quot;启用\&quot;，为选定用户启用存档邮箱](images/Mt791517.17ce99f7-d154-4e21-bec1-c938af1d4a0a(EXCHG.150).png "单击细节窗格中的&quot;启用&quot;，为选定用户启用存档邮箱")  

8.  在\&quot;**创建就地存档**\&quot;页上，依次单击\&quot;**基于云的存档**\&quot;和\&quot;**确认**\&quot;。此时，系统会显示要预配存档邮箱的域名。
    
    ![在\&quot;创建就地存档\&quot;页上，单击\&quot;基于云的存档\&quot;](images/Mt791517.9ad047c9-ef47-47df-93cc-0fab872f1ae1(EXCHG.150).png "在&quot;创建就地存档&quot;页上，单击&quot;基于云的存档&quot;")  
    
    请注意，在\&quot;**邮箱**\&quot;页上，选定邮箱的\&quot;**邮箱类型**\&quot;列中显示值\&quot;**用户(存档)**\&quot;。

9.  最长可能要等 30 分钟，目录同步才能完成。完成后才能创建基于云的存档邮箱。转到第 2 步，了解如何确认基于云的存档邮箱是否已创建。创建存档邮箱后，用户可以使用 Outlook 或 Web 上的 Outlook 对其进行访问。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ659053.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在 Office 365 管理中心 中，依次转到&amp;quot;<strong>运行状况</strong>&amp;quot;&gt;&amp;quot;<strong>目录同步状态</strong>&amp;quot;，查看上次运行目录同步的时间。</td>
    </tr>
    </tbody>
    </table>


返回顶部

## 第 2 步：确认基于云的存档邮箱是否已创建

如前所述，基于云的存档邮箱的启用时间与其实际创建时间之间可能有延迟。这是因为必须运行目录同步才能创建基于云的存档邮箱。下面介绍了几种用于确认基于云的存档邮箱是否已创建的方法。

您Exchange Online的组织中运行以下的 PowerShell 命令，以显示与用户的存档邮箱相关的属性。若要连接到使用远程 PowerShell Exchange Online ，请参阅[连接到 Exchange 联机 PowerShell](https://go.microsoft.com/fwlink/?/linkid=396554)。

    Get-MailUser <cloud mail user> | FL *archive*

以下屏幕截图显示了待预配基于云的存档邮箱时和创建存档邮箱后返回的属性。

**通过目录同步预配基于云的存档邮箱前的邮件用户属性**

![预配基于云的存档前基于云的邮件用户属性](images/Mt791517.c6a42713-f061-4761-93c1-2b5478953e46(EXCHG.150).png "预配基于云的存档前基于云的邮件用户属性")

通过目录同步预配基于云的存档前，*ArchiveStatus* 属性设置为 `None`。此外，还请注意，*ArchiveGuid* 和 *ArchiveName* 属性为空。

**通过目录同步预配基于云的存档邮箱后的邮件用户属性**

![预配基于云的存档后基于云的邮件用户属性](images/Mt791517.005fcc87-6253-4218-aafc-50f212de54fa(EXCHG.150).png "预配基于云的存档后基于云的邮件用户属性")

通过目录同步预配基于云的存档后，*ArchiveStatus* 属性设置为 `Active`，且 *ArchiveGuid* 和 *ArchiveName* 属性已经过填充。此时，用户可以在 Outlook 或 Web 上的 Outlook 中访问其基于云的存档邮箱。

![用户可以在 Outlook 或 Outlook 网页版中访问基于云的存档邮箱](images/Mt791517.8777bc4d-05c3-4489-8d8c-ff5429a0b2c3(EXCHG.150).png "用户可以在 Outlook 或 Outlook 网页版中访问基于云的存档邮箱")

也可以在本地 Exchange 组织中运行以下 PowerShell 命令，以显示与用户基于云的存档邮箱有关的属性。

    Get-Mailbox <on-premises user mailbox> | FL *archive*

**通过目录同步预配基于云的存档邮箱前的本地邮箱属性**

![预配基于云的存档前的邮箱属性](images/Mt791517.d5625bc8-03de-439a-8a0a-051ff537a0bf(EXCHG.150).png "预配基于云的存档前的邮箱属性")

通过目录同步预配基于云的存档前，*ArchiveStatus* 属性设置为 `None`，*ArchiveState* 属性设置为 `HostedPending`。

**通过目录同步预配基于云的存档邮箱后的本地邮箱属性**

![预配基于云的存档后的邮箱属性](images/Mt791517.9b42d562-1b0a-4722-97aa-35d0ef6f9372(EXCHG.150).png "预配基于云的存档后的邮箱属性")

通过目录同步预配基于云的存档邮箱后，*ArchiveStatus* 属性设置为 `Active`，*ArchiveState* 属性设置为 `HostedProvisioned`。此时，用户可以在 Outlook 或 Web 上的 Outlook 中访问其基于云的存档邮箱。

返回顶部

## （可选）运行目录同步

如前所述，基于云的存档邮箱是在目录同步期间创建。默认情况下，本地 Active Directory 每 30 分钟与 Office 365 中的 Azure AD 同步一次。可以查看上次运行目录同步的时间，只需在 Office 365 管理中心 中依次转到\&quot;**运行状况**\&quot;\>\&quot;**目录同步状态**\&quot;即可。

在某些情况下，不妨启动目录同步，以在运行下一个计划同步前预配基于云的存档邮箱。为此，可在安装了 Azure AD Connect 的服务器上运行以下 PowerShell 命令。

    Start-ADSyncSyncCycle -PolicyType Delta

有关详细信息，请参阅 [Azure AD Connect sync:Scheduler](https://go.microsoft.com/fwlink/p/?linkid=836813)（Azure AD Connect 同步：计划程序）。

返回顶部

