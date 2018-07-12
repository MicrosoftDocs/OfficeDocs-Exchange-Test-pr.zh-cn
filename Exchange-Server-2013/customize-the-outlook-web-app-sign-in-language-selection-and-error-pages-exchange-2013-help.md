---
title: '自定义 Outlook Web App 的登录页、语言选择页和错误页: Exchange 2013 Help'
TOCTitle: 自定义 Outlook Web App 的登录页、语言选择页和错误页
ms:assetid: d8d9f735-7181-428f-9049-b9886dce5159
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee633483(v=EXCHG.150)
ms:contentKeyID: 54652301
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 自定义 Outlook Web App 的登录页、语言选择页和错误页

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

本主题解释如何对 Outlook Web App 自定义登录页、语言选择页和错误页的颜色和图像。

Outlook Web App号中、 语言中选择和错误页上创建了基于主题的资源文件夹中的图形和.css 文件。Outlook Web App 使用只有一组登录、 语言选择和错误页的所有主题。所有用户将会都看到对这些网页进行任何修改。在 V15\\FrontEnd\\HttpProxy\\owa\\auth\\version\\themes\\resources Exchange安装目录中，可以找到主题资源文件夹。您将需要更改的默认颜色，文本编辑器和图形编辑器来更改的图像。如果找不到匹配的[颜色表](https://go.microsoft.com/fwlink/p/?linkid=280679)必须符合特定的颜色，您可以使用图像编辑工具采集一种颜色，并确定其 HTML RGB 值。

如果用户有多个支持 Outlook Web App 的服务器并想要让这些服务器都使用相同的登陆页、语言页和错误页，则必须将修改的文件复制到每个服务器上。还应该创建自定义文件的备份副本。如果重新安装或升级 Exchange，将覆盖主题文件夹中的所有文件。重新安装或升级完成后，必须将自定义文件复制回相应的文件夹。

> [!IMPORTANT]  
> 开始创建自定义登陆页和注销页前，备份将要修改的所有文件的副本。


有关创建自定义主题的信息，请参阅[为 Outlook Web App 创建主题](create-a-theme-for-outlook-web-app-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：45 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中\&quot;Outlook Web App 权限\&quot;下的\&quot;图形编辑器\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 自定义登陆页的颜色

1.  登录到 Exchange 服务器并使用 Windows Explorer 转到 Exchange 服务器安装目录并找到 \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<版本\>\\themes\\resources。

2.  使用文本编辑器（例如记事本）打开 logon.css 文件。

3.  默认颜色值 \#0072 c 6 搜索并将其替换为您要使用的颜色的 HTML RGB 值。您可以找到 HTML RGB 值：[颜色表](https://go.microsoft.com/fwlink/p/?linkid=280679)。

4.  保存并关闭该文件。

## 自定义错误页的颜色

1.  登录到 Exchange 服务器并使用 Windows Explorer 转到 Exchange 服务器安装目录并找到 \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<版本\>\\themes\\resources。

2.  使用文本编辑器（例如记事本）打开 errorFE.css 文件。

3.  默认颜色值 \#0072 c 6 搜索并将其替换为您要使用的颜色的 HTML RGB 值。您可以找到 HTML RGB 值：[颜色表](https://go.microsoft.com/fwlink/p/?linkid=280679)。

4.  保存并关闭该文件。

## 自定义语言选择页的颜色

1.  登录到 Exchange 服务器并使用 Windows Explorer 转到 Exchange 服务器安装目录并找到 \\V15\\Client Access\\OWA\\version\\Owa2\\resources\\styles。

2.  使用文本编辑器（例如记事本）打开 LanguageSelection.css 文件。

3.  默认颜色值 \#0072 c 6 搜索并将其替换为您要使用的颜色的 HTML RGB 值。您可以找到 HTML RGB 值：[颜色表](https://go.microsoft.com/fwlink/p/?linkid=280679)。

4.  保存并关闭该文件。

## 自定义登陆页和错误页上的图像。

使用图像编辑工具打开和编辑用于制作登陆页和错误页的图像。

1.  登录到 Exchange 服务器并使用 Windows Explorer 转到 Exchange 服务器安装目录并找到 \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\\<版本\>\\themes\\resources。

2.  使用图形编辑器打开和修改以下文件：
    
      - owa\_text\_blue.png，修改\&quot;Outlook Web App\&quot;文本徽标。
    
      - olk\_logo\_white.png，修改左侧栏的应用程序徽标。
    
      - olk\_logo\_white\_cropped.png，修改错误页左侧面板的图像。
    
      - sign\_in\_arrow.png，修改\&quot;登录\&quot;按钮左边的图标。
    
      - olk\_exchange\_text\_blue.png，修改 tnarrow 布局中的\&quot;Outlook Mobile\&quot;徽标。
    
      - olk\_logo\_white\_small.png 在 tnarrow 中使用。
    
      - olk\_exchange\_text\_stacked\_white\_small.png 在 tnarrow 中使用。

3.  默认颜色值 \#0072 c 6 搜索并将其替换为您要使用的颜色的 HTML RGB 值。您可以找到 HTML RGB 值：[颜色表](https://go.microsoft.com/fwlink/p/?linkid=280679)。

4.  保存并关闭该文件。

## 您如何知道操作成功？

在 Internet Explorer 中打开 Outlook Web App 登录页面。如果要测试对托管 Outlook Web App 虚拟目录的服务器上的默认网站所做的更改，可以打开 Internet Explorer 并输入 URL https://localhost/owa 进行测试。

如果看不到所做的更改，请执行以下操作：

1.  在工具栏上，选择\&quot;设置\&quot;\>\&quot;Internet 选项\&quot;\>\&quot;常规\&quot;。

2.  在\&quot;浏览历史\&quot;下，选择\&quot;删除\&quot;。

3.  选择\&quot;临时 Internet 文件和网站文件\&quot;，然后选择\&quot;删除\&quot;。

4.  当 Internet Explorer 完成删除，选择\&quot;确定\&quot;关闭\&quot;Internet 选项\&quot;。

5.  刷新浏览器窗口。

> [!TIP]  
> 若要查看所做修改的效果，可以在保存每个修改后保持正在编辑的 .css 文件处于打开状态并刷新浏览器窗口。

