---
title: '为 Outlook Web App 创建主题: Exchange 2013 Help'
TOCTitle: 为 Outlook Web App 创建主题
ms:assetid: 7e1fa13c-3de3-45c2-b1fa-e74fc8487bda
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201700(v=EXCHG.150)
ms:contentKeyID: 54652281
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 为 Outlook Web App 创建主题

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

*主题*定义 MicrosoftOutlook Web App 所使用的背景色、字体、突出显示颜色、图标和标题。每个主题是存储在 MicrosoftExchange 服务器上安装目录的 \\Client Access\\OWA\\prem\\*version*\\resources\\themes 中的媒体文件和级联样式表 (.css) 文件的集合。每个主题存储在 \\themes 各自的子目录中。

可以在 \\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base 中找到默认主题。每个主题文件夹中包含定义主题所需的所有文件。这些文件包括 CSS 文件、图形以及定义主题名称的 .xml 文件。通过将一个主题中的所有文件复制到新文件夹中并根据需要修改这些文件，可以创建其他主题。

默认情况下，当安装 Exchange Server 2013 时会安装多个主题，如下所示：

  - CSS (.css) 文件定义颜色、渐变方式和字体。

  - 图像 (.png) 文件提供图标和其他图形元素。编辑任何图标时，请勿更改其大小。如果更改了任何图形元素的大小，应测试所做更改，以验证这些元素是否仍能正确配合在一起。

这些文件存储在客户端访问服务器上安装目录的 \\Client Access\\OWA\\prem\\*\<version\>*\\resources\\themes 中。每个主题都存储在主题的一个子目录中。可以通过复制现有主题和修改副本来创建其他主题。

在创建主题之后，您可能还需要[自定义 Outlook Web App 的登录页、语言选择页和错误页](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md)。

> [!NOTE]  
> Outlook Web App 基本客户端不支持主题。


> [!CAUTION]  
> 如果您有多个支持 Outlook Web App 的服务器，则必须将自定义主题复制到每个服务器。还应该创建自定义文件的备份副本。如果重新安装或升级 Exchange，将覆盖主题文件夹中的所有文件。重新安装或升级完成后，必须将主题复制回相应的文件夹。
> 在开始创建自定义主题之前，为将要更改的所有文件制作备份副本。


## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：60 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的\&quot;Outlook Web App 虚拟目录\&quot;条目。

  - 需要具有本地服务器管理员访问权限，才能执行这些步骤。

  - 您将需要更改的默认颜色，文本编辑器和图形编辑器来更改的图像。如果找不到匹配的[颜色表](https://go.microsoft.com/fwlink/p/?linkid=280679)必须符合特定的颜色，您可以使用图像编辑工具采集一种颜色，并确定其 HTML RGB 值。

  - 建议您只要更改或创建 Outlook Web App 主题，最好遵循下列原则：
    
      - 如果决定编辑现有主题，则在开始编辑它们之前需要制作原始文件的备份副本。
    
      - 请勿删除 \\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base 文件夹或其中的任何文件。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您该如何做？

## 步骤 1：创建新 Outlook Web App 主题

先为新主题创建一个文件夹，然后将现有主题中的文件复制到新文件夹中。

1.  使用已委派了本地 Administrators 组成员身份的帐户登录到托管 Outlook Web App 虚拟目录的 Exchange 服务器。

2.  打开 Windows 资源管理器，然后找到 Exchange 服务器安装目录。

3.  在 \\Client Access\\OWA\\prem\\*version*\\resources\\themes 中，新建一个文件夹并为其命名，例如 Fourth Coffee。

4.  将另一个主题中的所有文件复制到新文件夹中。

## 步骤 2：命名新主题

要设置新主题的显示名称，请执行下列操作：

1.  打开刚创建的自定义主题文件夹中的 themeinfo.xml 副本。

2.  找到该主题的 `displayname` 值，然后将该值更改为希望使用的名称。例如 `displayname = "Fourth Coffee Theme"`。

3.  保存并关闭 themeinfo.xml。

## 步骤 3：更改新主题的排序顺序（可选）

如果需要，可以通过编辑 themeinfo.xml 文件更改新主题的排序顺序。排序顺序决定了\&quot;设置\&quot;菜单中\&quot;更改主题\&quot;面板中的主题位置。

要使用 themeinfo.xml 文件更改新主题的排序顺序，请执行下列操作：

1.  打开自定义主题文件夹中的 themeinfo.xml 副本。

2.  找到该主题的 `sortorder` 值，更改该值以反映您希望新主题在列表中出现的位置。主题将按数字值的升序排序。默认情况下，基本主题排在第一个，其 `sortorder` 值为\&quot;0\&quot;。例如 `sortorder="<number>"`。

3.  保存并关闭 themeinfo.xml。

## 步骤 4：修改新主题

您已复制文件并命名主题，现在可以对其进行自定义。可以在 Outlook Web App 主题中自定义下列元素：

  - 用于定义标题区域和图标的图像文件。

  - 用于定义字体和颜色的 CSS 文件。

## 图像文件

主题图像存储在 \\themes*\\\<theme name\>*\\images\\ 中的两个文件夹中。\\images\\0 文件夹包含将在从左到右语言（如英语）中使用的图像，从右到左阅读的语言将使用 \\images\\rtl 文件夹中的图像。

> [!NOTE]  
> \images\rtl 文件夹中的某些图像与 \images\0 文件夹中相同，只不过它们相互是镜像图像。


要自定义主题，可以使用图像编辑工具打开并修改下列图像：

  - Headerbgmain.png
    
      - 这是主标题图像。建议该图像不要超过 30 像素的标题高度。默认主题不使用背景图像，因此该图像是透明的。有关具有自定义背景图像的主题的示例，请参阅\&quot;Blueprint\&quot;主题文件夹中的图像。

  - Headerbgright.png
    
      - 它用作标题后的平铺图像。默认主题不使用平铺背景图像，因此该图像是透明的。有关具有自定义平铺背景图像的主题的示例，请参阅\&quot;Blueprint\&quot;主题文件夹中的图像。

  - sprite1.mouse.png
    
      - 它包含主题中使用的大多数图像。可以更改图像颜色以匹配您的主题，还可以更改默认 Outlook Web App 文本徽标。
    
      - 为了避免任何问题，请不要更改 sprite 中任何单个图标的大小，并确保它保存为透明的 .png 文件。

  - themepreview.png
    
      - 此图像将用来表示 Outlook Web App\&quot;设置\&quot;菜单中的\&quot;更改主题\&quot;面板中的主题。

## 颜色和字体

级联样式表 (.css) 文件定义将在主题中使用并存储在 \\themes\\*\<theme name\>* 下的多个文件夹中的颜色和字体。\\*\<theme name\>*\\0 文件夹包含将在从左到右语言（如英语）中使用的 .css 文件，从右到左阅读的语言将使用 \\*\<theme name\>*\\rtl 文件夹中的 .css 文件。还有特定于语言的文件夹（例如 \\ja、\\ko、\\zhs 和 \\zht），其中包含要用于这些语言的 .css 文件。

从修改 \\*\<theme name\>*\\images\\0 文件夹开始操作。在每个可自定义的主题中，使用了四种颜色。

  - BrandColor：\#0072C6

  - NavBarHoverColor：\#4C9CD7

  - UnreadColor：\#2A8DD4

  - FocusColor：\#DFEDFA

可以使用文本编辑器（如记事本）在下列两个文件中搜索这些值的所有实例，并将其替换为您的主题的颜色：owa2styles.mouseCSS 和 owa2styles2.mouseCSS。必须在新主题中包含这些 .css 文件的每个文件夹中完成此操作。

## 步骤 5：设置默认 Outlook Web App 主题

设置新默认主题仅影响尚未通过 Outlook Web App 中的\&quot;设置\&quot;菜单更改其主题的用户。

若要强制所有用户使用默认主题，除了设置默认主题之外，还必须禁用主题选择。

## 使用命令行管理程序为 Outlook Web App 设置默认主题

此示例设置 Outlook Web App 的默认主题，其中服务器名称为 `fourthcoffee`，虚拟目录名称为 `owa`，网站名称为 `default web site`，主题位于名为 `Custom` 的文件夹中。

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom 

有关语法和参数的详细信息，请参阅[Set-OwaVirtualDirectory](https://technet.microsoft.com/zh-cn/library/bb123515\(v=exchg.150\))。

## 使用命令行管理程序为 Outlook Web App 禁用主题选择

此示例在 Outlook Web App 中禁用主题选择，其中服务器名称为 `fourthcoffee`，虚拟目录名称为 `owa`，网站名称为 `default web site`。

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -themeselectionenabled $false 

也可以按以下示例中所示，同时完成这两个命令：

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom -themeselectionenabled $false

有关语法和参数的详细信息，请参阅[Set-OwaVirtualDirectory](https://technet.microsoft.com/zh-cn/library/bb123515\(v=exchg.150\))。

## 步骤 6：运行 iisreset/noforce 保存您的更改

如果添加或更改主题，更改主题名称或者更改主题的排序顺序，则必须停止并启动 Internet 信息服务 (IIS) 才能使更改生效。为此，请在创建新主题的服务器上打开命令提示窗口，运行命令 **iisresest /nforce**。

## 您如何知道此任务有效？

1.  使用创建新主题的服务器上的虚拟目录登录 Outlook Web App。如果要测试对托管 Outlook Web App 虚拟目录的 Exchange 服务器上的默认网站所做的更改，可以通过打开 Internet Explorer 并输入 URL https://localhost/owa 来测试主题。

2.  通过选择\&quot;设置\&quot;菜单 \>\&quot;更改主题\&quot; 并选择自定义主题，可以切换到自定义主题。

## 如果看不到最新更改且已经运行 iisreset/noforce

1.  在 Internet Explorer 工具栏上，选择\&quot;设置\&quot;菜单 \>\&quot;Internet 选项\&quot;。

2.  在\&quot;常规\&quot;选项卡上的\&quot;浏览历史记录\&quot;下，选择\&quot;删除\&quot;，然后验证已选中\&quot;临时 Internet 文件和网站文件\&quot;。然后，选择\&quot;删除\&quot;删除这些文件。

3.  选择\&quot;确定\&quot;关闭\&quot;Internet 选项\&quot;。

4.  选择\&quot;刷新\&quot;查看所做更改。

每次对主题文件进行更改时，可能必须重复这些步骤才能看到更改。如果您正在进行一些更改，则可以保持 Outlook Web App 打开，在服务器上重复运行 **iisreset/noforce** 并根据需要从 Internet Explorer 清除临时文件。

