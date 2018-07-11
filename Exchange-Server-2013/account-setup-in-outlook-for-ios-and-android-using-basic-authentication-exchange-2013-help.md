---
title: '在 Outlook 的 iOS 和 Android 使用基本身份验证的帐户设置: Exchange 2013 Help'
TOCTitle: 在 Outlook 的 iOS 和 Android 使用基本身份验证的帐户设置
ms:assetid: 013dbe8c-30de-4c9c-baa9-75081b9229e8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt829322(v=EXCHG.150)
ms:contentKeyID: 74518382
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在 Outlook 的 iOS 和 Android 使用基本身份验证的帐户设置

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2018-04-30_

**摘要：**  如何 Exchange 2013 组织中的用户可以快速设置自己的 Outlook iOS 和 Android 使用基本身份验证的帐户。

IOS 和 Android 的 outlook 提供 Exchange 管理员帐户配置"推送"到他们的内部用户的使用基本身份验证通过 ActiveSync 协议的能力。此功能适用于任何移动设备管理 (MDM) 提供商为 Android 的 iOS 或[Android 在企业](https://developer.android.com/samples/apprestrictions/index.html)通道使用[管理应用程序配置](https://developer.apple.com/library/content/samplecode/sc2279/introduction/intro.html)通道。

对于内部用户在 Microsoft Intune 注册，您可以部署在 Azure 门户使用 Intune 帐户配置设置。

一旦已经创建的帐户配置用户注册其设备，Outlook iOS 和 Android 将检测到的帐户是"发现"，然后将提示用户添加帐户。用户需要输入才能完成安装过程的唯一信息是他们的密码。然后，将加载该用户的邮箱内容用户才能开始使用该应用程序。

下面的图像演示后在 Azure 门户 Intune 中已配置 Outlook，iOS 和 Android 的最终用户安装过程的一个示例。

![Outlook for iOS 和 Outlook for Android 本地帐户设置](images/Mt829322.04bd56f2-5c45-4268-8762-436994acd656(EXCHG.150).png "Outlook for iOS 和 Outlook for Android 本地帐户设置")

## Outlook 为 iOS 和 Android 使用 Microsoft Intune 创建应用程序配置策略

如果使用的 Microsoft Intune 作为您的移动设备管理提供程序，下面的步骤允许您部署的内部邮箱，可以利用与 ActiveSync 协议基本身份验证的帐户配置设置。创建配置后，您可以向一组用户，在下一个部分中，指定配置设置所述分配设置。

> [!NOTE]  
> 如果您组织中的用户使用 iOS 和 Android 的工作设备，您需要创建单独的应用程序配置策略为每个平台。


1.  登录到 Azure 的门户。

2.  选择**更多服务 \> 监控 + 管理 \> Intune**。

3.  在管理列表的**移动应用程序**刀片式服务器，选择**应用程序配置策略**。

4.  在**应用程序配置策略**刀片式服务器，选择**添加**。

5.  **添加应用程序配置**刀片式服务器，应用程序配置设置中输入**名称**和可选**说明**。

6.  对于**设备注册**类型，选择**受管理设备**。

7.  为**平台**，选择**iOS**或**Android 的工作**。

8.  选择**关联的应用程序**，，然后，在**目标应用程序**刀片式服务器，选择**Microsoft Outlook 的 iOS**或**Android 的 Microsoft Outlook**。

9.  单击**确定**以返回到**应用程序配置添加**刀片式服务器。

10. 选择**配置设置**。**配置设置**刀片式服务器，定义将提供配置 Outlook，iOS 和 Android 的键/值对。您输入的键值对定义键值对的部分中，本文中稍后介绍。
    
    > [!NOTE]  
    > 要输入键/值对，您必须使用配置设计器或输入 XML 属性列表之间进行选择。


11. 操作完成后，请选择**确定**。

12. 在**添加应用程序配置**刀片式服务器，选择**创建**。

将**应用程序配置策略**刀片式服务器上显示新创建的配置策略。

## 指定配置设置

分配到 Azure Active Directory 中的用户组的上一节中创建的设置。当用户具有安装 Microsoft Outlook 应用程序时，该应用程序将管理由您指定的设置。若要此操作：

1.  在 Intune 移动应用程序管理仪表板的**移动应用程序**刀片式服务器，选择**应用程序配置策略**。

2.  从应用程序配置策略列表中，选择您要分配的一个，然后选择**工作分配**。

3.  在**分配**刀片式服务器，选择**选择组**。

4.  在**组中选择**刀片式服务器，选择要向其分配应用程序配置策略，然后选择**选择**，然后**将保存**的 Azure AD 组。

## 键/值对

在创建应用程序配置策略在 Azure 门户或通过 MDM 提供商时，您将需要下列键/值对：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>密钥</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailAccountName</p></td>
<td><p>此值指定的显示名称电子邮件帐户将显示给用户的设备上。</p>
<p><strong>已接受的值</strong>： 字符串</p>
<p><strong>如果未指定默认</strong>空白： &lt; &gt;</p>
<p><strong>示例</strong>： user@companyname.com</p>
<p><strong>Intune 标记 *</strong>: {{用户名}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.EmailAddress</p></td>
<td><p>此值指定要用于发送和接收邮件的电子邮件地址。</p>
<p><strong>已接受的值</strong>： 字符串</p>
<p><strong>如果未指定默认</strong>空白： &lt; &gt;</p>
<p><strong>示例</strong>： user@companyname.com</p>
<p><strong>Intune 标记 *</strong>: {{邮件}}</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.EmailUPN</p></td>
<td><p>此值指定将用于验证的帐户的电子邮件配置文件的用户主体名称。</p>
<p><strong>已接受的值</strong>： 字符串</p>
<p><strong>如果未指定默认</strong>空白： &lt; &gt;</p>
<p><strong>示例</strong>： userupn@companyname.com</p>
<p><strong>Intune 标记 *</strong>: {{范围内}}</p></td>
</tr>
<tr class="even">
<td><p>com.microsoft.outlook.EmailProfile.ServerAuthentication</p></td>
<td><p>此值指定用户的身份验证方法。</p>
<p><strong>已接受的值</strong>: 用户名和密码。证书</p>
<p><strong>如果未指定默认</strong>: 用户名和密码</p>
<p><strong>示例</strong>: 用户名和密码</p></td>
</tr>
<tr class="odd">
<td><p>com.microsoft.outlook.EmailProfile.ServerHostName</p></td>
<td><p>此值指定您的 Exchange 服务器的主机名。</p>
<p><strong>已接受的值</strong>： 字符串</p>
<p><strong>如果未指定默认</strong>空白： &lt; &gt;</p></td>
</tr>
</tbody>
</table>


**\***Microsoft Intune 用户可以使用将展开为正确的值根据 MDM 注册用户的令牌。[托管的 iOS 设备的添加应用程序配置策略](https://docs.microsoft.com/en-us/intune/app-configuration-policies-use-ios)的详细信息，请参见

