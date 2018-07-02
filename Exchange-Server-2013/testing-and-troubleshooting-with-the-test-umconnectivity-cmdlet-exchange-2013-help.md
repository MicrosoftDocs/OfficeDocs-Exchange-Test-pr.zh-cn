---
title: '使用 Test-UMConnectivity Cmdlet 进行测试和故障排除: Exchange 2013 Help'
TOCTitle: 使用 Test-UMConnectivity Cmdlet 进行测试和故障排除
ms:assetid: 08e67a99-e37f-4afd-bd58-455b62580af7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa995978(v=EXCHG.150)
ms:contentKeyID: 56271416
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用 Test-UMConnectivity Cmdlet 进行测试和故障排除

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-06-25_

安装客户端访问和邮箱服务器并配置统一消息后，您可以使用多个诊断测试和基于软件的电话应用程序来测试电话连接性和统一消息服务的运行情况。

## Test-UMConnectivity

**Test-UMConnectivity** cmdlet 可用于通过几种方式检查客户端访问和邮箱服务器的连接性，具体取决于该 cmdlet 使用的参数。若要对统一消息功能进行测试，可以使用以下测试：

  - **本地测试** **Test-UMConnectivity** cmdlet 验证 IP 语音 (VoIP) 与运行在同一本地计算机上的邮箱服务器之间的通信。

  - **使用 TUILogon 的本地测试** **Test-UMConnectivity** cmdlet 尝试建立 VoIP 与同一计算机上运行的邮箱服务器的通信。如果建立连接，则它将尝试通过发送邮箱的分机号码和 PIN 登录到一个或多个已启用 UM 的邮箱。如果提供了 *–TUILogon* 参数，还必须提供下列参数值以及测试邮箱的相应信息：
    
      - *–Phone*   此参数必须包含测试邮箱的分机号码。
    
      - *–PIN*   此参数必须包含已启用 UM 的邮箱的 PIN。
    
      - *–UMDialPlan   *此参数必须包含与测试邮箱相链接的拨号计划。

  - **远程测试** **Test-UMConnectivity** cmdlet 通过 VoIP 网关发出呼叫来尝试连接到远程客户端访问服务器。连接后，它将对远程客户端访问服务器和媒体路径执行连接性检查。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果收到以下消息，则应重启 MicrosoftExchange 统一消息服务，因为该服务已停止或未响应：&amp;quot;Test-UMConnectivity 任务在尝试进行呼叫时遇到错误。详细信息:无法建立连接。&amp;quot;</td>
    </tr>
    </tbody>
    </table>

