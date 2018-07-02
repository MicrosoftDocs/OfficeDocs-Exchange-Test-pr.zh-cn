---
title: '在混合部署的本地组织和 Exchange Online 组织之间移动邮箱: Exchange 2013 Help'
TOCTitle: 在混合部署的本地组织和 Exchange Online 组织之间移动邮箱
ms:assetid: d6289f7b-f67e-48db-9570-9fd3c9547548
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/o365e_hrcmoverequest_fl312271(v=EXCHG.150)
ms:contentKeyID: 51408301
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在混合部署的本地组织和 Exchange Online 组织之间移动邮箱

 

_<strong>适用于：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上一次修改主题：</strong>2017-10-02_

只要具备了基于 Exchange 的混合部署，您可以选择将内部部署 Exchange 邮箱移动到 Exchange Online 组织或将 Exchange Online 邮箱移动到 Exchange 组织。当您在内部部署和 Exchange Online 组织间移动邮箱时，使用迁移批处理执行远程邮箱移动请求。这个方法不必创建用户邮箱和导入用户信息就可以移动现有邮箱。这个方法与将内部部署 Exchange 组织中的用户邮箱迁移到 Exchange Online 作为 Exchange 完整迁移到云中的一部分不同。在本话题中讨论的邮箱移动在内部部署 Exchange 和 Exchange Online 组织间的长期共存关系中是管理的 Exchange 管理的一部分。

有关将本地 Exchange 组织迁移至 Exchange Online 的详细信息，请参阅[将多个电子邮件帐户迁移至 Office 365 的方法](https://go.microsoft.com/fwlink/p/?linkid=524030)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>必须在内部部署和 Exchange Online 组织间配置一个混合部署以完成本话题中的邮箱移动过程。有关混合部署的更多信息，请参阅 <a href="exchange-server-hybrid-deployments-exchange-2013-help.md">Exchange Server 混合部署</a>。<br />
<br />
你需要确保本地的 Skype for Business 2015、Skype for Business Online 和 Exchange Online 全部符合“<a href="hybrid-deployment-prerequisites-exchange-2013-help.md">混合部署先决条件</a>”中指定的要求，然后才能将已启用统一消息 (UM) 的邮箱移动到 Exchange Online。有关如何将本地 UM 邮箱策略映射到 Exchange Online 中的策略的信息，请参阅 <a href="https://technet.microsoft.com/zh-cn/library/bb124903(v=exchg.150)">Set-UMMailboxPolicy</a>。</td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成时间：用 10 分钟的时间来配置迁移批处理，但是完成迁移的总时间取决于每个迁移批处理所包括的邮箱数量。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](https://technet.microsoft.com/zh-cn/library/dd638132\(v=exchg.150\))主题中的“邮箱移动和迁移权限”部分。

  - 在您的内部部署和 Exchange Online 组织间配置混合部署。

  - 如果您运行的是 Exchange 2013，确保已在您的内部部署 Exchange 2013 客户端访问服务器上启用了邮箱复制服务代理 (MRSProxy)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](https://technet.microsoft.com/zh-cn/library/jj150484\(v=exchg.150\))。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ659053.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 步骤 1：创建迁移终结点

在 Exchange 混合部署中执行场内传输和场外传输远程移动迁移前，建议您创建 Exchange 远程迁移终结点。迁移终结点包含运行 MRS 代理服务的内部部署 Exchange 服务器的连接设置，这需要从 Exchange Online 执行远程移动迁移和执行远程移动迁移到 Exchange Online。

有关分步步骤说明，请参阅创建迁移终结点。

## 步骤 2：启用 MRSProxy 服务

如果没有启用内部部署 Exchange 2013 客户端访问服务器上的 MRSProxy 服务，则按照 Exchange 管理中心 (EAC) 中的步骤操作：

1.  打开 EAC，导航到“服务器”\>“虚拟目录”。

2.  选择客户端访问服务器，选择“EWS”虚拟目录，然后单击“编辑”![编辑图标](images/JJ906432.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  选择“已启用 MRS 代理”复选框，然后单击“保存”。

## 步骤 3：使用 EAC 移动邮箱

您可以使用 Exchange 服务器上的 EAC 中的“Office 365”选项卡上的远程移动迁移向导，将内部部署组织中的现有用户邮箱移动到 Exchange Online 组织或将 Exchange Online 邮箱移动到内部部署组织。选择下列过程之一：

## 将内部部署邮箱移动到 Exchange Online

您可以使用 Exchange 服务器上的 EAC 中的“Office 365”选项卡上的远程移动迁移向导，将内部部署组织中的现有用户邮箱移动到 Exchange Online 组织。按照以下步骤执行操作：

1.  打开 EAC 并导航到“Office 365”\>“收件人”\>“迁移”。

2.  单击“添加”![添加图标](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，然后选择“迁移到 Exchange Online”。

3.  在“选择迁移类型”页上，选择“远程移动迁移”，然后单击“下一步”。

4.  在“选择用户”页上，单击“添加”![添加图标](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，选择要移至 Office 365 的内部部署用户并单击“添加”，然后单击“确定”。单击“下一步”。

5.  在“输入 Windows 用户帐户凭据”页上的“内部部署管理员名称”文本字段中，输入内部部署管理员帐户名称，然后在“内部部署管理员密码”文本字段中输入与此帐户关联的密码。例如，“corp\\administrator”和密码。单击“下一步”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您已经创建了一个迁移终结点，那么就会收到此步骤的终结点确认提示。如果您创建了两个或多个迁移终结点，那么您必须在迁移终结点下拉菜单中选择一个终结点。</td>
    </tr>
    </tbody>
    </table>


6.  在“确认迁移终结点”页上，验证向导确认迁移终结点时是否会列出内部部署 Exchange 服务器的 FDQN。例如，“mail.contoso.com”。单击“下一步”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>当选择将多个邮箱移动到 Exchange Online 时，Exchange 服务器上的 MRSProxy 服务会自动限制邮箱移动请求。完成邮箱移动操作的总时间取决于选定邮箱的总数、邮箱大小和 MRSProxy 的配置。若要了解有关自定义 MRSProxy 的详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/bb232205(v=exchg.150)">邮件限制</a>。</td>
    </tr>
    </tbody>
    </table>


7.  在“移动配置”页上的“新迁移批处理名称”文本字段中，输入迁移批处理的名称。使用向下箭头 ![向下键图标](images/JJ906432.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "向下键图标") 选择“迁移到 Office 365 的邮箱的目标传递域”。在大多数混合部署中，这是用于 Exchange Online 组织邮箱的主 SMTP 域。例如，contoso.mail.onmicrosoft.com。确认已选中“移动主邮箱及存档邮箱”选项，然后单击“下一步”。

8.  在“启动批处理”页上，至少选择一个接收批处理完成报告的收件人。确认已选中“自动启动批处理”选项，然后选中“自动完成迁移批处理”复选框。单击“新建”。

## 将 Exchange Online 邮箱移至内部部署组织

您可以使用 Exchange 服务器上的 EAC 中的“Office 365”选项卡上的远程移动迁移向导，将内部部署组织中的现有用户邮箱移动到 Exchange Online 组织：

1.  打开 EAC 并导航到“Office 365”\>“收件人”\>“迁移”。

2.  单击“添加”![添加图标](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，然后选择“从 Exchange Online 迁移”。

3.  在“选择用户”页上，选择“选择要移动的用户”，然后单击“下一步”。

4.  在“选择用户”页上，单击“添加”![添加图标](images/JJ906432.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，选择要移至内部部署组织的 Exchange Online 用户并单击“添加”，然后单击“确定”。单击“下一步”。

5.  在“确认迁移终结点”页上，验证向导确认迁移终结点时是否会列出内部部署 Exchange 服务器的 FDQN。例如，“mail.contoso.com”。单击“下一步”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>当选择将多个邮箱移动到 Exchange Online 时，Exchange 服务器上的 MRSProxy 服务会自动限制邮箱移动请求。完成邮箱移动操作的总时间取决于选定邮箱的总数、邮箱大小和 MRSProxy 的属性。若要了解有关自定义 MRSProxy 的详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/bb232205(v=exchg.150)">邮件限制</a>。</td>
    </tr>
    </tbody>
    </table>


6.  在“移动配置”页上的“新迁移批处理名称”文本字段中，输入迁移批处理的名称。然后在“迁移到 Office 365 的邮箱的目标传递域”字段中输入目标传递域。在大多数混合部署中，这是用于本地和 Exchange Online 组织邮箱的主 SMTP 域。例如，contoso.com。

7.  选择是否也移动选定用户的存档邮箱，并在“目标数据库”文本字段中输入想要将这个邮箱移动到的数据库名称。例如，邮箱数据库 123456789。单击“下一步”。

8.  在“启动批处理”页上，至少选择一个接收批处理完成报告的收件人。确认已选中“自动启动批处理”，然后选中“自动完成迁移批处理”复选框。单击“新建”。

## 步骤 4：删除已完成的迁移批处理

在邮箱移动完成后，我们建议删除已完成的迁移批处理，以在相同的用户再次移动时将错误的可能性降到最低。

若要删除已完成的迁移批处理，请执行下列操作：

1.  打开 EAC 并导航到“Office 365”\>“收件人”\>“迁移”。

2.  单击已完成的迁移批处理，然后单击“删除”![删除图标](images/JJ906432.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

3.  在删除警告确认对话框上，单击“是”。

## 步骤 5：为 Web 上的 Outlook 重新启用脱机访问

当不能连接到网络时，Web 上的 Outlook 中的脱机访问（以前称为 Outlook Web App）允许用户访问他们的邮箱。如果你将 Exchange 邮箱迁移到 Exchange Online，用户需要重置浏览器中的脱机访问设置以脱机使用 Web 上的 Outlook。有关在 Web 上的 Outlook 中脱机访问、支持脱机访问的浏览器和如何打开的详细信息，请参阅[脱机使用 Outlook Web App](https://go.microsoft.com/fwlink/p/?linkid=286942)。

## 您如何知道操作成功？

当在内部部署和 Exchange Online 组织间移动现有用户邮箱时，成功完成远程移动向导初步表示，移动邮箱按预期完成。

邮箱移动过程需要几分钟才能完成，因此您还可以确认此移动是否运行正确，方法是打开 EAC 并选择“Office 365”\>“收件人”\>“迁移”，以显示远程移动向导中所选邮箱的移动状态。在邮箱移动过程中，“状态”的值为“正在同步”，在邮箱成功移至内部部署或 Exchange Online 组织后，该值为“已完成”。

邮箱移动完成后，您可以通过验证邮箱属性来检查是否已成功移动了位于内部部署或 Exchange Online 组织中的远程邮箱。为此，需导航到内部部署组织或 Exchange Online 组织的 EAC 中的“收件人”\>“邮箱”。对于 Exchange Online 邮箱，用户邮箱的“邮箱类型”应该显示为“Office 365”；对于内部部署邮箱，则显示为“用户”。

您也可以运行 Exchange 命令行管理程序中的以下 cmdlet 来确认迁移批处理的状态。

    Get-MigrationBatch -Identity <batch name>

有疑问吗？请在 Office 365 论坛中寻求帮助。若要访问论坛，必须使用已拥有对基于云的服务的管理员访问权限的帐户进行登录。请访问以下论坛：[Office 365 论坛](https://go.microsoft.com/fwlink/p/?linkid=201915)

## 刚开始接触 Office 365？


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="“领英学习”短图标" alt="“领英学习”短图标" /> <strong>刚开始接触 Office 365？</strong><br />
发现 LinkedIn Learning 向 <a href="https://support.office.com/zh-cn/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>提供的免费视频课程。</p></td>
</tr>
</tbody>
</table>

