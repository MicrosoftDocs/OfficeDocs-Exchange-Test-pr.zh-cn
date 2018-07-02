---
title: '不在架构主站点/域中_NotInSchemaMasterDomain: Exchange 2013 Help'
TOCTitle: 不在架构主站点/域中_NotInSchemaMasterDomain
ms:assetid: 5e44eb33-4c30-4c3d-ba68-5c30bef1731f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.notinschemamasterdomain(v=EXCHG.150)
ms:contentKeyID: 50490661
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 不在架构主站点/域中\_NotInSchemaMasterDomain

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

由于运行安装程序的计算机与分配了域架构主机角色（又称灵活单一主机操作或 FSMO）的服务器不在同一 Active Directory® 目录服务站点或域中，Microsoft® Exchange Server 2007 安装程序无法继续。

Exchange 2007 安装程序要求用作域架构主机的域控制器与运行 Exchange 安装程序的本地计算机位于同一站点或域中。

域架构主机控制对 Active Directory 构架的所有更新和修改。

若要解决此问题，请使用 **/prepareschema** 和 **/prepareAD** 开关从与域架构主机所在的同一站点或域运行 Exchange Server 2007 安装程序。

有关**/prepareschema**和**/prepareAD**安装程序命令行开关的详细信息，请参阅 Exchange 2007 产品文档主题"如何到准备活动目录和域"(<https://go.microsoft.com/fwlink/?linkid=78453>)

可以使用架构主机工具标识角色。不过，必须注册 Schmmgmt.dll DLL 才能使架构主机工具作为 MMC 管理单元使用。

查看当前的架构主机

1.  在命令提示符处键入 **regsvr32 schmmgmt.dll**
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果显示以下对话框，则表示已成功注册 <strong>RegSvr32</strong>：<br />
    schmmgmt.dll 中的 DllRegisterServer 已成功注册。</td>
    </tr>
    </tbody>
    </table>


2.  若要打开新的管理控制台，请依次单击\&quot;开始\&quot;和\&quot;运行\&quot;，然后键入 **mmc**。

3.  在\&quot;控制台\&quot;菜单上，单击\&quot;添加/删除管理单元\&quot;。

4.  单击\&quot;添加\&quot;打开\&quot;添加独立管理单元\&quot;对话框。

5.  选择\&quot;Active Directory 架构\&quot;，然后单击\&quot;添加\&quot;。

6.  \&quot;添加/删除管理单元\&quot;中将显示\&quot;Active Directory 架构\&quot;。单击\&quot;关闭\&quot;，然后单击\&quot;确定\&quot;返回控制。

7.  选择\&quot;Active Directory 架构\&quot;，随后将会在右侧显示\&quot;类\&quot;和\&quot;属性\&quot;区域。

8.  右键单击\&quot;Active Directory 架构\&quot;，然后单击\&quot;操作主机\&quot;。

9.  将显示当前的架构主机

在识别当前架构主机后，确定架构主机所在的子网。然后，使用以下方法之一安装 Exchange：

  - 修改 Exchange 服务器上的子网，将其移动到架构主机所在的站点。然后，安装 Exchange。

  - 临时强制 Exchange 服务器的站点成员身份更改，然后安装 Exchange。安装好 Exchange 后，将 Exchange 服务器返回其原始站点。

若要强制站点成员身份

1.  在您要安装 Exchange 的服务器上，启动注册表编辑器。为此，单击\&quot;开始\&quot;，再单击\&quot;运行\&quot;，键入 **regedit**，然后单击\&quot;确定\&quot;。

2.  查找以下注册表子项：
    
    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\Netlogon\\Parameters**

3.  创建以下新\&quot;**字符串**\&quot;值：
    
    值名称：** SiteName**
    
    值类型：** REG\_SZ**
    
    值数据：** \<site\_that\_contains\_the\_schema\_master\>**

4.  退出注册表编辑器，然后重新启动 Netlogon 服务。该操作将强制 Exchange 服务器加入您指定的站点。

5.  安装 Exchange。

6.  删除您在第 3 步中添加的注册表条目。

7.  重新启动 Netlogon 服务。此操作会将 Exchange 返回到原始站点。

