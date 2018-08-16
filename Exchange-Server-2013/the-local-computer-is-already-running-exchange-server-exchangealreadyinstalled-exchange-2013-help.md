---
title: '本地计算机已在运行 Exchange Server_ExchangeAlreadyInstalled: Exchange 2013 Help'
TOCTitle: 本地计算机已在运行 Exchange Server_ExchangeAlreadyInstalled
ms:assetid: 3f168b5d-9910-418f-86fb-e99d852dcb5e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.exchangealreadyinstalled(v=EXCHG.150)
ms:contentKeyID: 50490367
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 本地计算机已在运行 Exchange Server\_ExchangeAlreadyInstalled

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为本地计算机安装了以前版本的 Microsoft Exchange 组件，所以 Microsoft® Exchange Server 2007 安装程序无法继续进行。

Exchange 2007 安装程序要求本地计算机不能安装现有的 Microsoft Exchange 组件。

若要解决此问题，请删除所有 Microsoft Exchange 2000 Server 或 Microsoft Exchange Server 2003 组件，然后重新运行 Microsoft Exchange 安装程序。

删除 Microsoft Exchange 组件

1.  单击&#34;开始&#34;，指向&#34;设置&#34;，然后单击&#34;控制面板&#34;。

2.  双击&#34;添加或删除程序&#34;。

3.  在&#34;当前安装的程序&#34;列表中，依次单击&#34;Microsoft Exchange&#34;和&#34;更改/删除&#34;。

4.  在 Microsoft Exchange 安装向导中，单击&#34;下一步&#34;。

5.  在组件选择页的操作列表中，单击每个已安装的组件旁边的向下箭头，然后单击&#34;删除&#34;。
    
    > [!NOTE]  
    > 对于已安装的组件，操作列表中会显示相应的选中标记。在您单击&amp;quot;删除&amp;quot;后，选中标记就会替换为&amp;quot;删除&amp;quot;一词。


6.  单击<strong>"下一步"</strong>两次。

7.  单击&#34;完成&#34;。

