---
title: '回滚从 Exchange 2013 到 Exchange Online 的公用文件夹迁移: Exchange 2013 Help'
TOCTitle: 回滚从 Exchange 2013 到 Exchange Online 的公用文件夹迁移
ms:assetid: bcd54aa0-aa45-4c68-b504-1475842d4b96
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt798259(v=EXCHG.150)
ms:contentKeyID: 74432703
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 回滚从 Exchange 2013 到 Exchange Online 的公用文件夹迁移

 

_**上一次修改主题：** 2017-03-20_

**摘要：** 按照这些步骤将公用文件夹基础结构返回到其在 Exchange 2013 本地组织中的迁移前状态。

如果在将公用文件夹迁移到 Exchange Online 方面遇到问题，或者由于其他原因需要重新激活 Exchange 2013 公用文件夹，请按照以下步骤操作。

## 回滚迁移

请注意，如果回滚迁移，将丢失通过客户端或通过电子邮件（针对已启用邮件的公用文件夹）添加到迁移后 Exchange Online 的公用文件夹的所有内容。若要保存此内容，可以将迁移后的公用文件夹内容导出到 .pst 文件，然后可以在回滚完成后将其导入到本地公用文件夹。

1.  在 Exchange 本地环境中，运行以下命令解锁 Exchange 2013 公用文件夹（请注意解锁可能需要几个小时的时间）：
    
        Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false -PublicFoldersEnabled Local 

2.  在 Exchange 本地环境中，还原任意已启用邮件的公用文件夹的 `ExternalEmailAddress`，而该文件夹已通过 SetMailPublicFolderExternalAddress.ps1（*步骤 8：测试和解锁 Exchange Online 中的公用文件夹* 所使用的脚本，此步骤来自[使用批处理迁移将 Exchange 2013 公用文件夹迁移到 Exchange Online](use-batch-migration-to-migrate-exchange-2013-public-folders-to-exchange-online-exchange-online-help.md)）进行更新。可以参阅此脚本创建的摘要文件来标识经过修改的内容，或使用之前在同一个批处理迁移进程中生成的文件 OnPrem\_MEPF.xml 获取所有已启用邮件的公用文件夹的原始属性。

3.  在 Exchange Online PowerShell 中，运行以下命令以删除所有 Exchange Online 公用文件夹和邮箱：
    
        Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
        Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true

4.  在 Exchange Online 环境中运行以下命令，将公用文件夹流量重定向回本地环境 (Exchange 2013)：
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote

5.  请参阅[针对混合部署配置 Exchange 2013 公用文件夹](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)，了解有关重新配置对本地公用文件夹的访问权限的说明，以便 Exchange Online 用户可以访问它们。

