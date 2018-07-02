---
title: '自定义详细信息模板: Exchange 2013 Help'
TOCTitle: 自定义详细信息模板
ms:assetid: b4beeedd-e46f-442e-844a-e8575f95dca0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.toolbox.detailstemplate(v=EXCHG.150)
ms:contentKeyID: 50491329
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 自定义详细信息模板

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-09-25_

使用详细信息模板编辑器可以自定义对象属性的客户端图形用户界面 (GUI) 的表示形式，可使用 MicrosoftOutlook 中的地址列表访问这些属性。例如，用户在 Outlook 中打开地址列表时，特定对象的属性按照 Exchange 组织中详细信息模板的定义来表示。可以通过改变字段大小、添加或删除字段、添加或删除选项卡以及重排字段来自定义对象。这些模板的布局因语言而异。

## 在开始之前，您需要知道什么？

  - 详细信息模板编辑器中没有撤消选项。如果您误操作，则需要恢复回上一版本。有关详细信息，请参阅[还原到默认配置的详细信息模板](restore-a-details-template-to-the-default-configuration-exchange-2013-help.md)。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的\&quot;详细信息模板\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 自定义详细信息模板

1.  在\&quot;Exchange 工具箱\&quot;中，单击\&quot;详细信息模板编辑器\&quot;，然后在操作窗格中单击\&quot;打开工具\&quot;。

2.  在详细信息模板编辑器的控制台树中，单击\&quot;详细信息模板\&quot;。
    
    在详细信息窗格中，显示以下各列：
    
      - **语言**   此列列出创建模板所用的语言。
    
      - **模板类型**   此列列出可自定义的模板类型。
    
      - **标识**   此列列出模板的唯一标识。
    
      - **创建时间**   此列列出创建模板的日期和时间。
    
      - **修改时间**   此列列出上次修改模板的日期和时间。

3.  若要编辑模板，请依次单击相应的模板和操作窗格中的\&quot;编辑\&quot;。例如，下图中显示的是\&quot;英语(美国)\&quot;联系人详细信息模板。
    
    **通过 Outlook 2013 查看到的默认详细信息模板**
    
    ![Outlook 2007 中的默认详细信息模板](images/JJ673049.a0af8aca-663d-4702-ab2f-9a342f481cdf(EXCHG.150).gif "Outlook 2007 中的默认详细信息模板")  

4.  单击\&quot;编辑\&quot;后，可以执行多项任务来自定义详细信息模板：
    
      - 若要在设计器窗格中移动对象，请选择相应的对象，然后将其拖到模板上的新位置。在移动对象时，我们将为您提供对齐线。
    
      - 若要更改标签文本，请在设计窗格中选择相应的标签。在属性窗格中的\&quot;文本\&quot;框内键入新文本。若要创建键盘快捷方式，可以使用 & 号。将 & 号置于快捷方式字母前。
    
      - 要更改对象大小，请选择该对象，然后拖动大小句柄直到该对象达到所需的形状和大小。
    
      - 若要删除对象，请选择该对象，然后按 Delete 键。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>详细信息模板编辑器不包含&amp;quot;撤消&amp;quot;按钮，您也不能使用键盘快捷方式撤消某个操作。若要撤消对模板进行的添加操作，您必须使用 DELETE 键。若要撤消删除操作，您必须重新应用设置。您还可以在退出详细信息模板编辑器时不保存所做更改，从而还原到初始设置。若要撤消已保存的更改，您可以还原模板。如果您还原模板，则会丢失所有自定义设置，且模板会还原至原始配置。若要详细了解如何还原详细信息模板，请参阅<a href="restore-a-details-template-to-the-default-configuration-exchange-2013-help.md">还原到默认配置的详细信息模板</a>。</td>
        </tr>
        </tbody>
        </table>
    
      - 若要在工具箱窗格中添加\&quot;编辑\&quot;文本框、列表框、多值下拉框或多值列表框，请将对象拖动到设计窗格中。单击属性窗格中的属性下拉框，然后选择将由 Exchange 使用的属性，设置对象的属性。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>必须将对象与属性相关联，这样 Exchange 才能使用它。此外，属性还确定了在 Outlook 中向最终用户显示的内容。如果您不选择属性，则系统会自动随机选择某个属性。</td>
        </tr>
        </tbody>
        </table>
    
      - 若要添加分组框，请将对象拖到设计窗格中。然后，在属性窗格中的\&quot;文本\&quot;框内键入名称。使用分组框可以对相似对象进行分组。
    
      - 若要将选项卡添加到模板中，请右键单击现有选项卡，然后单击\&quot;添加选项卡\&quot;。此时，系统会显示一个空白选项卡。要命名此选项卡，请在属性窗格中的\&quot;文本\&quot;框内键入名称。
    
      - 若要从模板中删除选项卡，请右键单击相应的选项卡，然后单击\&quot;删除选项卡\&quot;。此时，系统会显示一个警告。单击\&quot;确定\&quot;，确认要删除此选项卡。
    
      - 若要更改选项卡上各对象的 Tab 键顺序，以便用户可以使用 Tab 键按您所需的顺序导航对象，请在设计窗格中选择相应的对象。然后，在属性窗格中，使用\&quot;TabIndex\&quot;框更改顺序。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>若要确保用户不能使用 Tab 键访问对象的标签（例如，&amp;quot;名称&amp;quot;或&amp;quot;别名&amp;quot;），请更改标签的次序以便这些标签处在 Tab 键次序的最后。</td>
        </tr>
        </tbody>
        </table>


5.  要保存对详细信息模板的更改，请在\&quot;文件\&quot;菜单上，单击\&quot;保存\&quot;。

6.  要关闭模板，请在\&quot;文件\&quot;菜单上，单击\&quot;退出\&quot;。

