---
title: 生成加密和解密的密钥
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- keys, encryption and decryption
- keys, asymmetric
- keys, symmetric
- encryption [.NET Framework], keys
- symmetric keys
- asymmetric keys [.NET Framework]
- cryptography [.NET Framework], keys
ms.assetid: c197dfc9-a453-4226-898d-37a16638056e
ms.openlocfilehash: 88d8dac83c3d5bf267ed90ffb313cd9e24b42dea
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/07/2020
ms.locfileid: "75706183"
---
# <a name="generating-keys-for-encryption-and-decryption"></a>生成加密和解密的密钥
创建和管理密钥是加密过程的一个重要部分。 对称算法要求创建密钥和初始化向量 (IV)。 密钥必须对不应解密数据的任何人保密。 IV 并不是一定要保密，但应定期更改。 非对称算法要求创建公钥和私钥。 公钥可以公开给任何人，而私钥必须只有将解密用公钥加密的数据的参与方知道。 本节介绍如何生成和管理对称和非对称算法的密钥。  
  
## <a name="symmetric-keys"></a>对称密钥  
 .NET Framework 所提供的对称加密类需要一个密钥和新的初始化向量 (IV) 来加密和解密数据。 每当使用无参数构造函数创建一个托管对称加密类的新实例时，都会自动创建新的密钥和 IV。 获许解密你的数据的任何人都必须具有相同的密钥和 IV 并使用相同的算法。 通常情况下，应为每个会话创建一个新的密钥和 IV，且不应为了在稍后会话中使用而存储该密钥和 IV。  
  
 为了将对称密钥和 IV 传送给远程方，通常使用不对称加密来加密对称密钥。 通过不安全的网络发送密钥而不对其进行加密会很不安全，这是因为截获密钥和 IV 的任何人都能够解密您的数据。 有关使用加密交换数据的详细信息，请参阅 [创建加密方案](../../../docs/standard/security/creating-a-cryptographic-scheme.md)。  
  
 下列示例演示如何创建 <xref:System.Security.Cryptography.TripleDESCryptoServiceProvider> 类的新实例，该类会实现 TripleDES 算法。  
  
```vb  
Dim tdes As TripleDESCryptoServiceProvider = new TripleDESCryptoServiceProvider()  
```  
  
```csharp  
TripleDESCryptoServiceProvider tdes = new TripleDESCryptoServiceProvider();  
```  
  
 执行前面的代码后，将生成新的密钥和 IV，并分别置于 **Key** 和 **IV** 属性中。  
  
 有时可能需要生成多个密钥。 在这种情况下，你可以创建会实现对称算法的类的新实例，然后通过调用 **GenerateKey** 和 **GenerateIV** 方法来创建新的密钥和 IV。 下面的代码示例演示了如何在创建了对称加密类的新实例后创建新的密钥和 IVs。  
  
```vb  
Dim tdes As TripleDESCryptoServiceProvider = new TripleDESCryptoServiceProvider()  
tdes.GenerateIV()  
tdes.GenerateKey()  
```  
  
```csharp  
TripleDESCryptoServiceProvider tdes = new TripleDESCryptoServiceProvider();  
tdes.GenerateIV();  
tdes.GenerateKey();  
```  
  
 执行前面的代码后，在创建 **TripleDESCryptoServiceProvider** 的新实例时会生成一个密钥和 IV。 调用 **GenerateKey** 和 **GenerateIV** 方法时会创建另一个密钥和 IV。  
  
## <a name="asymmetric-keys"></a>非对称密钥  
 .NET Framework 为非对称加密提供了 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 和 <xref:System.Security.Cryptography.DSACryptoServiceProvider> 类。 使用无参数构造函数创建新的实例时，这些类会创建一个公钥/私钥对。 可以存储非对称密钥以用于多个会话，也可以生成它以仅用于一个会话。 虽然公钥可以普遍可用，但私钥应受到严密保护。  
  
 每次创建非对称算法类的新实例时，都将生成一个公钥/私钥对。 在创建类的新实例后，可以使用以下两种方法之一来提取密钥信息：  
  
- <xref:System.Security.Cryptography.RSA.ToXmlString%2A> 方法，它会返回密钥信息的的 XML 表示形式。  
  
- <xref:System.Security.Cryptography.RSACryptoServiceProvider.ExportParameters%2A> 方法，它返回存储密钥信息的 <xref:System.Security.Cryptography.RSAParameters> 结构。  
  
 这两种方法接受一个布尔值，该值指示是只返回公钥信息还是同时返回公钥和私钥信息。 通过使用 **方法，** RSACryptoServiceProvider **类可以初始化为** RSAParameters <xref:System.Security.Cryptography.RSACryptoServiceProvider.ImportParameters%2A> 结构的值。  
  
 非对称私钥永远不应以原义或纯文本形式存储在本地计算机上。 如果需要存储私钥，则应使用密钥容器。 有关如何在密钥容器中存储私钥的详细信息，请参阅 [How to: Store Asymmetric Keys in a Key Container](../../../docs/standard/security/how-to-store-asymmetric-keys-in-a-key-container.md)。  
  
 下列代码示例通过创建公钥/私钥对来创建 **RSACryptoServiceProvider** 类的新实例，并将公钥信息保存到 **RSAParameters** 结构。  
  
```vb  
'Generate a public/private key pair.  
Dim rsa as RSACryptoServiceProvider = new RSACryptoServiceProvider()  
'Save the public key information to an RSAParameters structure.  
Dim rsaKeyInfo As RSAParameters = rsa.ExportParameters(false)  
```  
  
```csharp  
//Generate a public/private key pair.  
RSACryptoServiceProvider rsa = new RSACryptoServiceProvider();  
//Save the public key information to an RSAParameters structure.  
RSAParameters rsaKeyInfo = rsa.ExportParameters(false);  
```  
  
## <a name="see-also"></a>另请参阅

- [加密数据](../../../docs/standard/security/encrypting-data.md)
- [解密数据](../../../docs/standard/security/decrypting-data.md)
- [Cryptographic Services](../../../docs/standard/security/cryptographic-services.md)
- [How to: Store Asymmetric Keys in a Key Container](../../../docs/standard/security/how-to-store-asymmetric-keys-in-a-key-container.md)
