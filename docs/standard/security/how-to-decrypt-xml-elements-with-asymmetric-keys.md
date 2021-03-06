---
title: 如何：用非对称密钥对 XML 元素进行解密
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- System.Security.Cryptography.RSACryptoServiceProvider class
- asymmetric keys
- System.Security.Cryptography.EncryptedXml class
- XML encryption
- decryption
ms.assetid: dd5de491-dafe-4b94-966d-99714b2e754a
ms.openlocfilehash: 5ed1e2eb2518366da0a57655d7a8691e23f725d5
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/07/2020
ms.locfileid: "75706131"
---
# <a name="how-to-decrypt-xml-elements-with-asymmetric-keys"></a>如何：用非对称密钥对 XML 元素进行解密
可以使用 <xref:System.Security.Cryptography.Xml> 命名空间中的类对 XML 文档内的元素进行加密和解密。  XML 加密是交换或存储加密的 XML 数据的一种标准方式，使用后就无需担心数据被轻易读取。  有关 XML 加密标准的详细信息，请参阅万维网联合会（W3C）建议[XML 签名语法和处理](https://www.w3.org/TR/xmldsig-core/)。  
  
 此过程中的示例对使用[如何：用非对称密钥加密 XML 元素](../../../docs/standard/security/how-to-encrypt-xml-elements-with-asymmetric-keys.md)中所述的方法进行加密的 XML 元素进行解密。  它将查找 <`EncryptedData`> 元素，对元素进行解密，然后将元素替换为原始纯文本 XML 元素。  
  
 此示例使用两个密钥对 XML 元素进行解密。  它从密钥容器中检索以前生成的 RSA 私钥，然后使用 RSA 密钥对存储在 < 中的会话密钥进行解密`EncryptedKey``EncryptedData`> 元素的 > 元素。  然后此示例使用会话密钥对 XML 元素进行解密。  
  
 此示例适用于以下情况：多个应用程序必须共享加密数据，或应用程序必须保存其每次运行之间的加密数据。  
  
### <a name="to-decrypt-an-xml-element-with-an-asymmetric-key"></a>用非对称密钥对 XML 元素进行解密  
  
1. 创建 <xref:System.Security.Cryptography.CspParameters> 对象，并指定密钥容器的名称。  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#2)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#2)]  
  
2. 使用 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 对象从容器中检索以前生成的非对称密钥。  当将 <xref:System.Security.Cryptography.CspParameters> 对象传递到 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 构造函数中时，将自动从密钥容器中检索到密钥。  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#3)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#3)]  
  
3. 创建新 <xref:System.Security.Cryptography.Xml.EncryptedXml> 对象以对文档进行解密。  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#5)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#5)]  
  
4. 添加一个密钥/名称映射，以便 RSA 密钥与应该进行解密的文档中的元素相关联。  必须使用与加密文档时所用密钥名称相同的名称。  请注意，此名称独立于用来标识在步骤 1 中指定的密钥容器中的密钥名称。  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#6)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#6)]  
  
5. 调用 <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> 方法以解密 <`EncryptedData`> 元素。  此方法使用 RSA 密钥来解密会话密钥，并自动使用会话密钥来解密 XML 元素。  它还会自动将 <`EncryptedData`> 元素替换为原始纯文本。  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#7)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#7)]  
  
6. 保存 XML 文档。  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#8)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#8)]  
  
## <a name="example"></a>示例  
 此示例假定名为 `test.xml` 的文件与已编译程序存在于同一目录中。  它还假定 `test.xml` 包含使用[如何：使用非对称密钥对 XML 元素进行加密](../../../docs/standard/security/how-to-encrypt-xml-elements-with-asymmetric-keys.md)中描述的方法进行加密的 XML 元素。  
  
 [!code-csharp[HowToDecryptXMLElementAsymmetric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#1)]
 [!code-vb[HowToDecryptXMLElementAsymmetric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a>编译代码  
  
- 若要编译此示例，需要包含对 `System.Security.dll` 的引用。  
  
- 包括以下命名空间：<xref:System.Xml>、<xref:System.Security.Cryptography> 和 <xref:System.Security.Cryptography.Xml>。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 永远不要以纯文本形式存储对称加密密钥，也不要以纯文本形式在计算机之间传输对称密钥。  此外，绝不存储或传输纯文本形式的非对称密钥的私钥。  有关对称和非对称加密密钥的详细信息，请参阅[生成加密和解密密钥](../../../docs/standard/security/generating-keys-for-encryption-and-decryption.md)。  
  
 绝不将密钥直接嵌入源代码。  可以通过使用[Ildasm （IL 拆装器）](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)或在文本编辑器（如记事本）中打开程序集，轻松地从程序集中读取嵌入的密钥。  
  
 当你使用加密密钥执行操作后，通过将每个字节设置为零或通过调用托管加密类的 <xref:System.Security.Cryptography.SymmetricAlgorithm.Clear%2A> 方法来将它从内存中清除。  加密密钥有时可从内存由调试器读取，或从硬盘读取（如果内存位置分页到磁盘）。  
  
## <a name="see-also"></a>另请参阅

- <xref:System.Security.Cryptography.Xml>
- [如何：使用非对称密钥加密 XML 元素](../../../docs/standard/security/how-to-encrypt-xml-elements-with-asymmetric-keys.md)
