---
title: '在 Exchange 中提供的 DLP 策略模板: Exchange 2013 Help'
TOCTitle: 在 Exchange 中提供的 DLP 策略模板
ms:assetid: 7e1917ab-1920-4a52-97d1-7dfe2add6198
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150530(v=EXCHG.150)
ms:contentKeyID: 50489694
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在 Exchange 中提供的 DLP 策略模板

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

在 Microsoft Exchange Server 2013 和 Exchange Online 中，可以使用数据丢失预防 (DLP) 策略模板作为构建 DLP 策略的起点，这些策略可帮助满足特定法规和业务策略需求。可以修改模板以便满足组织的特定需求。

> [!CAUTION]  
> 在生产环境中运行 DLP 策略时，应在测试模式下启用这些策略。在此类测试中，建议配置示例用户邮箱并发送调用测试策略的测试邮件以便确认结果。
> 使用这些策略并不能确保遵守任何法规。在您的测试完成之后，请在 Exchange 中进行所需的配置更改，使信息传输符合您组织的策略。例如，您可能需要配置与已知业务合作伙伴的 TLS 或添加更多限制的传输规则操作，比如向包含特定类型数据的邮件添加权限保护。


## 可用于 DLP 的模板

下表列出了 Exchange 中的 DLP 策略模板。要了解有关自定义这些模板以创建 DLP 策略的详细信息，请参阅[管理 DLP 策略](manage-dlp-policies-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>模板</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>澳大利亚财务数据</p></td>
<td><p>帮助检测在澳大利亚通常被认为是财务数据的信息（包括信用卡和 SWIFT 代码）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>澳大利亚健康记录法案（HRIP 法案）</p></td>
<td><p>帮助检测在澳大利亚通常被认为受健康记录和信息保密 (HRIP) 法案约束的信息（如医疗帐号和税号）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>澳大利亚个人身份信息 (PII) 数据</p></td>
<td><p>帮助检测在澳大利亚通常被认为是个人身份信息 (PII) 的信息（如税号和驾驶执照）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>澳大利亚隐私法案</p></td>
<td><p>帮助检测在澳大利亚通常被认为受隐私法案约束的信息（如驾驶执照和护照号）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>加拿大财务数据</p></td>
<td><p>帮助检测在加拿大通常被认为是财务数据的信息（包括银行帐号和信用卡）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>加拿大健康信息法案 (HIA)</p></td>
<td><p>帮助检测受加拿大亚伯达健康信息法案 (HIA) 约束的信息（包括像护照号和健康信息这样的数据）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>加拿大个人健康法案 (PHIPA) - 安大略</p></td>
<td><p>帮助检测受加拿大安大略个人健康信息保护法案 (PHIPA) 约束的信息（包括像护照号和健康信息这样的数据）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>加拿大个人健康信息法案 (PHIA) - 马尼托巴</p></td>
<td><p>帮助检测受加拿大马尼托巴个人健康信息法案 (PHIA) 约束的信息（包括像健康信息这样的数据）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>加拿大个人信息保护法案 (PIPA)</p></td>
<td><p>帮助检测受加拿大英属哥伦比亚个人信息保护法案 (PIPA) 约束的信息（包括像护照号和健康信息这样的数据）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>加拿大个人信息保护法案 (PIPEDA)</p></td>
<td><p>帮助检测受加拿大个人信息保护和电子文件法案 (PIPEDA) 约束的信息（包括像护照号和健康信息这样的数据）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>加拿大个人身份信息 (PII) 数据</p></td>
<td><p>帮助检测在加拿大通常被认为是个人身份信息 (PII) 的信息（如健康 ID 号和社会保险号）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>法国数据保护法案</p></td>
<td><p>帮助检测在法国通常被认为受数据保护法案约束的信息（如健康保险卡号）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>法国财务数据</p></td>
<td><p>帮助检测在法国通常被认为是财务信息的信息（包括像信用卡、帐户信息和借记卡号这样的信息）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>法国个人身份信息 (PII) 数据</p></td>
<td><p>帮助检测通常认为是法国居民个人身份信息 (PII) 的信息（包括护照号码等信息）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>德国财务数据</p></td>
<td><p>帮助检测在德国通常被认为是财务数据的信息（如欧盟借记卡号）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>德国个人身份信息 (PII) 数据</p></td>
<td><p>帮助检测通常认为是德国居民个人身份信息 (PII) 的信息（包括驾驶证和护照号码）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>以色列财务数据</p></td>
<td><p>帮助检测在以色列通常被认为是财务数据的信息（包括银行帐号和 SWIFT 代码）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>以色列个人身份信息 (PII) 数据</p></td>
<td><p>帮助检测通常被认为是以色列个人可识别信息 (PII) 的信息（如国民身份证号）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>以色列隐私保护</p></td>
<td><p>帮助检测在以色列通常被认为受隐私保护约束的信息（包括像银行帐号或国民身份证号这样的信息）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>日本财务数据</p></td>
<td><p>帮助检测在日本通常被认为是财务信息的信息（包括像信用卡、帐户信息和借记卡号这样的信息）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>日本个人身份信息 (PII) 数据</p></td>
<td><p>帮助检测通常认为是日本居民个人身份信息 (PII) 的信息（包括驾驶证和护照号码）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>日本个人信息保护</p></td>
<td><p>帮助检测受日本个人信息保护法约束的信息（包括像居民注册号这样的数据）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>PCI 数据安全标准 (PCI DSS)</p></td>
<td><p>帮助检测 PCI 数据安全标准 (PCI DSS) 的信息（包括信用卡或借记卡号等信息）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>沙特阿拉伯 - 反网络犯罪法</p></td>
<td><p>帮助检测在沙特阿拉伯通常被认为受反网络犯罪法约束的信息（包括国际银行帐号和 SWIFT 代码）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>沙特阿拉伯财务数据</p></td>
<td><p>帮助检测在沙特阿拉伯通常被认为是财务数据的信息（包括国际银行帐号和 SWIFT 代码）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>沙特阿拉伯个人身份信息 (PII) 数据</p></td>
<td><p>帮助检测通常被认为是沙特阿拉伯个人身份信息 (PII) 的信息（如国民身份证号）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>英国获取医疗报告法案</p></td>
<td><p>帮助检测受英国获取医疗报告法案约束的信息（包括像国民卫生服务号这样的数据）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>英国数据保护法案</p></td>
<td><p>帮助检测受英国数据保护法案约束的信息（包括像国民保险号这样的数据）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>英国财务数据</p></td>
<td><p>帮助检测在英国通常被认为是财务信息的信息（包括像信用卡、帐户信息和借记卡号这样的信息）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>英国个人信息在线行为守则 (PIOCP)</p></td>
<td><p>帮助检测受英国个人信息在线行为守则约束的信息（包括像健康信息这样的数据）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>英国个人身份信息 (PII) 数据</p></td>
<td><p>帮助检测通常认为是英国居民个人身份信息 (PII) 的信息（包括驾驶证和护照号码等信息）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>英国隐私和电子通信规则</p></td>
<td><p>帮助检测受英国隐私和电子通信法规约束的信息（包括像财务信息这样的数据）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>美国联邦贸易委员会 (FTC) 消费者规则</p></td>
<td><p>帮助检测受美国联邦贸易委员会 (FTC) 消费者规则约束的信息（包括像信用卡号这样的数据）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>美国财务数据</p></td>
<td><p>帮助检测在美国通常被认为是财务信息的信息（包括像信用卡、帐户信息和借记卡号这样的信息）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>格雷姆-里奇-比利雷法案 (GLBA)</p></td>
<td><p>帮助检测受雷姆-里奇-比利雷法案 (GLBA) 约束的信息（包括社会保险号或信用卡号等信息）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>美国健康保险法案 (HIPAA)</p></td>
<td><p>帮助检测受美国健康保险可携性和责任法案 (HIPAA) 约束的信息（包括像社会保险号和健康信息这样的数据）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>美国爱国者法案</p></td>
<td><p>帮助检测通常受美国爱国者法案约束的信息（包括像信用卡号或税号这样的信息）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>美国个人身份信息 (PII) 数据</p></td>
<td><p>帮助检测通常认为是美国居民个人身份信息 (PII) 的信息（包括社会保险号或驾驶证号等信息）是否存在。</p></td>
</tr>
<tr class="odd">
<td><p>美国国家违约通知法</p></td>
<td><p>帮助检测受美国国家违约通知法约束的信息（包括像社会保险号和信用卡号这样的数据）是否存在。</p></td>
</tr>
<tr class="even">
<td><p>美国国家社会保险号保密法</p></td>
<td><p>帮助检测受美国国家社会保险号机密法约束的信息（包括像社会保险号这样的数据）是否存在。</p></td>
</tr>
</tbody>
</table>


## 详细信息

[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[从模板创建 DLP 策略](how-to-new-dlp-data-loss-prevention-policy-template.md)

[使用 Exchange 中的敏感信息类型查找什么](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

