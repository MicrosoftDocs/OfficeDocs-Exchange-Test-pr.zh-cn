---
title: '将 Outlook 配置为显示隔离邮箱中的原始发件人: Exchange 2013 Help'
TOCTitle: 将 Outlook 配置为显示隔离邮箱中的原始发件人
ms:assetid: 9249425d-1b06-48a0-ad95-c4eefb641ff4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee861109(v=EXCHG.150)
ms:contentKeyID: 50491032
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 将 Outlook 配置为显示隔离邮箱中的原始发件人

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

垃圾邮件隔离是内容筛选器代理的一项功能，可以减小丢失合法邮件的风险。垃圾邮件隔离功能提供了一个临时存储位置，用来存储视为垃圾邮件以及不应传递到组织内用户邮箱中的邮件。

邮件达到垃圾邮件隔离阈值时，将封装在未送达报告 (NDR) 中并传递到垃圾邮件隔离邮箱。由于隔离的邮件以 NDR 的形式存储在隔离邮箱中，因此组织的邮局主管地址将被列为所有邮件的\&quot;发件人:\&quot;地址。但是，通过将原始发件人地址、原始收件人地址和原始垃圾邮件可信度 (SCL) 列入字段列表，将令您更轻松地找到要恢复的邮件。

默认情况下，您不能在 Microsoft Outlook 中选择这些字段。在能够向邮件视图中添加这些字段之前，必须先创建一个 Outlook 窗体，用于将原始发件人、原始收件人和原始 SCL 添加为可供选择的可选字段。创建此自定义窗体之后，您便可以配置 Outlook 在邮件视图中显示这些字段。

## 在开始之前，您需要知道什么？

  - 估计完成该过程的时间：15 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的\&quot;邮箱访问\&quot;条目。

  - 此过程要求配置了反垃圾邮件隔离邮箱。有关详细信息，请参阅[配置垃圾邮件隔离邮箱](configure-a-spam-quarantine-mailbox-exchange-2013-help.md)。

  - 若要访问隔离邮箱，您需要配置该邮箱的 Outlook 配置文件，然后打开使用 Outlook 邮箱。有关配置和使用多个 Outlook 配置文件的详细信息，请参阅[概述的 Outlook 电子邮件配置文件](https://go.microsoft.com/fwlink/p/?linkid=178975)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 步骤 1：使用记事本创建一个自定义 Outlook 窗体

1.  打开记事本，将下列代码复制到文档中。
    
        [Description]
        MessageClass=IPM.Note
        CLSID={00020D31-0000-0000-C000-000000000046}
        DisplayName=Quarantine Extension Form
        Category=Standard
        Subcategory=Form
        Comment=This form allows the Original Sender (ReceivedRepresentingEmailAddress), Original Recipient (To), and Original SCL (OriginalScl) values to be viewed as columns.
        LargeIcon=IPML.ico
        SmallIcon=IPMS.ico
        Version=3.0
        Locale=enu
        Hidden=1
        Owner=Microsoft Corporation
        Contact=Your Name
        
        [Platforms]
        Platform1=Win16
        Platform2=NTx86
        Platform9=Win95
        
        [Platform.Win16]
        CPU=ix86
        OSVersion=Win3.1
        
        [Platform.NTx86]
        CPU=ix86
        OSVersion=WinNT3.5
        
        [Platform.Win95]
        CPU=ix86
        OSVersion=Win95
        
        [Properties]
        Property01=ReceivedRepresentingEmailAddress
        Property02=DisplayTo
        Property03=OriginalScl
        
        [Property.ReceivedRepresentingEmailAddress]
        Type=31
        NmidInteger=0x0078
        DisplayName=ReceivedRepresentingEmailAddress
        
        [Property.DisplayTo]
        Type=31
        NmidInteger=0x0E04
        DisplayName=DisplayTo
        
        [Property.OriginalScl]
        Type=3
        NmidPropset={41F28F13-83F4-4114-A584-EEDB5A6B0BFF}
        NmidString=OriginalScl
        DisplayName=OriginalScl
        
        [Verbs]
        Verb1=1
        
        [Verb.1]
        DisplayName=&Open
        Code=0
        Flags=0
        Attribs=2
        
        [Extensions]
        Extensions1=1
        
        [Extension.1]
        Type=31
        NmidPropset={00020D0C-0000-0000-C000-000000000046}
        NmidInteger=1
        Value=1000000000000000

2.  使用下列各值将文件保存在 Office Forms 文件夹中：
    
      - **路径** *\<Office Install Path\>*\\\<*OfficeVersion\>*\\Forms\\*\<LCID\>*
        
          - *\<Office Install Path\>*   对于 32 位版本 Microsoft Windows 上的 32 位版本 Office，或 64 位版本 Windows 上的 64 位版本 Office，默认路径为 `C:\Program Files\Microsoft Office`。对于 64 位版本 Windows 上的 32 位版本 Office，默认路径为 `C:\Program Files (x86)\Microsoft Office`。
        
          - *\<OfficeVersion\>*   对于 Outlook 2007，值为 `Office12`。对于 Outlook 2010，值为 `Office14`。对于 Outlook 2013，值为 `Office15`。
        
          - *\<LCID\>*   此值为您的区域设置 ID (LCID) 值。例如，美国英语的 LCID 是 1033。有关详细信息，请参阅 [KB221435：Word 中支持的区域设置标识符列表](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid+=+221435)。
    
      - **名称**   对于此过程的其余部分，假定文件命名为 `QTNE.cfg`。文件名称并不重要，但一定要在该值前后加上引号，以便文件以 QTNE.cfg 格式（而非 QTNE.cfg.txt）格式保存。
    
    例如，对于安装在 64 位版本 Windows 上的 32 位美国英语版本 Outlook 2013， 将文件另存为：
    
        "C:\Program Files (x86)\Microsoft Office\Office15\Forms\1033\QTNE.cfg"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果 Windows 用户访问控制 (UAC) 阻止您将文件保存在正确的位置，则先将其保存到一个临时位置，然后再进行复制。</td>
    </tr>
    </tbody>
    </table>


## 步骤 2：配置 Outlook 使用自定义的 Outlook 窗体

根据您的计算机上安装的 Outlook 版本，使用下列操作过程之一：

## 配置 Outlook 2010 或 Outlook 2013

1.  在 Outlook 2010 或 Outlook 2013 中，单击\&quot;文件\&quot;\>\&quot;选项\&quot;\>\&quot;高级\&quot;。

2.  在\&quot;开发人员\&quot;部分，单击\&quot;自定义窗体\&quot;。

3.  在\&quot;选项\&quot;对话框中，单击\&quot;管理窗体\&quot;。

4.  在\&quot;窗体管理程序\&quot;对话框中，单击\&quot;安装\&quot;。浏览至 `QTNE.cfg` 文件的位置，选择它，并单击\&quot;打开\&quot;。在\&quot;窗体属性\&quot;对话框中，查看信息，然后单击\&quot;确定\&quot;安装个人窗体库中的隔离扩展窗体。

5.  在\&quot;窗体管理程序\&quot;对话框中，单击\&quot;关闭\&quot;。单击\&quot;确定\&quot;两次，关闭其余对话框并返回到 Outlook 主界面。

6.  在收件箱的\&quot;邮件\&quot;视图中的\&quot;主页\&quot;选项卡上，右击单击列标题行（您可能需要拉宽消息列表才能看到列），然后选择\&quot;视图设置\&quot;。

7.  在\&quot;高级视图设置\&quot;对话框中，单击\&quot;列\&quot;。

8.  在\&quot;显示列\&quot;对话框中，在\&quot;可用列选自\&quot;下拉列表中，滚动到列表末尾，然后选择\&quot;窗体\&quot;。

9.  在\&quot;为此文件夹选择企业窗体\&quot;对话框中，在\&quot;选定的窗体\&quot;字段中，选择\&quot;邮件\&quot;，然后单击\&quot;删除\&quot;。在\&quot;个人窗体\&quot;字段中，选择\&quot;隔离扩展窗体\&quot;，然后单击\&quot;添加\&quot;。完成后，单击\&quot;关闭\&quot;。

10. 在\&quot;显示列\&quot;对话框中的\&quot;可用列\&quot;部分，选择以下字段中的一个或多个字段，然后单击所选字段后的\&quot;添加\&quot;。
    
      - **ReceivedRepresentingEmailAddress**   原始发件人
    
      - **DisplayTo**   原始收件人（注意，在添加原始收件人后，这会显示为\&quot;收件人\&quot;）
    
      - **OriginalScl**   原始 SCL
    
    使用\&quot;上移\&quot;或\&quot;下移\&quot;按钮确定各列在视图中的位置。为了获得最佳结果，请将三个新字段放置在\&quot;附件\&quot;字段后面、\&quot;发件人\&quot;字段前面。完成后，单击\&quot;确定\&quot;两次，返回到 Outlook 主界面。

## 配置 Outlook 2007

1.  在 Outlook 2007 中，单击\&quot;工具\&quot;\>\&quot;选项\&quot;。

2.  在\&quot;选项\&quot;对话框中，单击\&quot;其他\&quot;选项卡，然后在\&quot;常规\&quot;下单击\&quot;高级选项\&quot;。

3.  在\&quot;高级选项\&quot;对话框中单击\&quot;自定义窗体\&quot;，然后在\&quot;自定义窗体\&quot;对话框中单击\&quot;管理窗体\&quot;。

4.  在\&quot;窗体管理程序\&quot;对话框中，单击\&quot;安装\&quot;。浏览至 `QTNE.cfg` 文件的位置，选择它，并单击\&quot;打开\&quot;。在\&quot;窗体属性\&quot;对话框中，查看信息，然后单击\&quot;确定\&quot;安装个人窗体库中的隔离扩展窗体。

5.  关闭\&quot;窗体管理程序\&quot;对话框，然后单击\&quot;确定\&quot;三次来关闭剩余的对话框，并返回到 Outlook 2007 主界面。

6.  在收件箱的\&quot;邮件\&quot;视图中，右键单击列标题行（您可能需要拉宽消息列表才能看到列），然后选择\&quot;自定义当前视图\&quot;。

7.  在\&quot;自定义视图: 消息\&quot;对话框中，单击\&quot;显示字段\&quot;。

8.  在\&quot;显示字段\&quot;对话框的\&quot;可用字段选自\&quot;下拉列表中，滚动到列表的末尾，并选择\&quot;窗体\&quot;。

9.  在\&quot;为此文件夹选择企业窗体\&quot;对话框中，在\&quot;选定的窗体\&quot;字段中，选择\&quot;邮件\&quot;，然后单击\&quot;删除\&quot;。在\&quot;个人窗体\&quot;字段中，选择\&quot;隔离扩展窗体\&quot;，然后单击\&quot;添加\&quot;。完成后，单击\&quot;关闭\&quot;。

10. 在\&quot;显示字段\&quot;对话框的\&quot;可用字段\&quot;部分，选择一个或多个以下字段，并在您选择的每个字段后面单击\&quot;添加\&quot;。
    
      - **ReceivedRepresentingEmailAddress**   原始发件人
    
      - **DisplayTo**   原始收件人（注意，在添加原始收件人后，这会显示为\&quot;收件人\&quot;）
    
      - **OriginalScl**   原始 SCL
    
    使用\&quot;上移\&quot;或\&quot;下移\&quot;按钮确定各列在视图中的位置。为了获得最佳结果，请将三个新字段放置在\&quot;附件\&quot;字段后面、\&quot;发件人\&quot;字段前面。完成后，单击\&quot;确定\&quot;两次以返回到 Outlook 2007 的主界面。

## 您如何知道这有效？

如果您可以使用 Outlook 查看垃圾邮件隔离邮箱中的隔离邮件的原始发件人、原始收件人或原始 SCL 值，说明该操作过程有效。

