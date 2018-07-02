---
title: '配置拨号代码: Exchange Online Help'
TOCTitle: 配置拨号代码
ms:assetid: e5b5efee-b734-4f70-8357-11be07b23bd0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124992(v=EXCHG.150)
ms:contentKeyID: 51408288
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置拨号代码

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

您可以配置拨号代码、 号码的前缀，并由统一消息用于拨号的启用了 UM 的用户的传入和传出呼叫的数字格式。在大多数情况下，您将配置拨号代码、 前缀和数字格式当前在电话网络上配置拨号计划。

使用拨号代码和编号的前缀来确定正确的号码拨用于放置的已启用 UM 的用户的传出呼叫。*Outdialing*是用来说明通过该 UM 拨号计划中的用户发出传出调用的过程的术语。数字格式可用于在一个国家或地区、 国际电话或拨号计划中拨叫的电话来电。您可以配置拨号计划与国家/地区和国际数字的传入呼叫号码格式匹配。配置的国家/地区和国际数字格式时，您可以限制为拨号计划与链接的用户的传入呼叫。

有关与外拨相关的其他管理任务，请参阅[允许用户进行调用过程](allowing-users-to-make-calls-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 要执行什么操作？

## 使用 EAC 配置拨号代码、号码前缀和号码格式

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  选择您想要管理的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。

4.  在\&quot;UM 拨号计划\&quot;页面 \>\&quot;拨号代码\&quot;上，配置下列选项：
    
      - **外线接入编码**
    
      - **国际接入编码**
    
      - **国家/地区号码前缀**
    
      - **国家/地区代码**

5.  在\&quot;拨号计划间的拨号号码格式\&quot;下，配置下列选项：
    
      - **国家/地区号码格式**
    
      - **国际号码格式**
    
      - \&quot;同一拨号计划内的传入呼叫号码格式\&quot;   若要添加号码格式，请单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

6.  单击\&quot;保存\&quot;保存更改。

## 使用命令行管理程序配置拨号代码、号码前缀和号码格式

本示例为名为 `MyUMDialPlan` 的 UM 拨号计划配置国家/地区内号码格式、国际号码格式和以下拨号代码：

  - 9 表示外线接入编码

  - 011 表示国际接入编码

  - 1 表示国家/地区号码前缀

  - 1 表示国家/地区代码

<!-- end list -->

    Set-UMDialPlan -Identity MyUMDialPlan -OutsideLineAccessCode 9 -InternationalAccessCode 011 -NationalNumberPrefix 1 CountryorRegionCode 1 -InCountryOrRegionNumberFormat 1425xxxxxxx -InternationalNumberFormat 441425xxxxxxx

