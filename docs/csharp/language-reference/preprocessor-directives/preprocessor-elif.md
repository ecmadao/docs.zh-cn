---
title: '#elif - C# 参考'
ms.date: 07/20/2015
f1_keywords:
- '#elif'
helpviewer_keywords:
- '#elif directive [C#]'
ms.assetid: 731d78df-08e0-4d51-b8c8-f193c27de13f
ms.openlocfilehash: c78818f40b76414d289af6c704ff019b63befe37
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2020
ms.locfileid: "75712567"
---
# <a name="elif-c-reference"></a>#elif（C# 参考）
`#elif` 可以创建复合条件指令。 如果之前的 `#elif`#if[ 和任何之前的可选 ](./preprocessor-if.md) 指令表达式的值为 `#elif`，则计算 `true` 表达式。 如果 `#elif` 表达式计算结果为 `true`，编译器将计算 `#elif` 和下一条件指令间的所有代码。 例如:  
  
```csharp
#define VC7  
//...  
#if debug  
    Console.WriteLine("Debug build");  
#elif VC7  
    Console.WriteLine("Visual Studio 7");  
#endif  
```  
  
 可以使用运算符 `==`（相等）、`!=`（不相等）、`&&`（和）以及`||`（或）计算多个符号。 还可以用括号对符号和运算符进行分组。  
  
## <a name="remarks"></a>备注  
 `#elif` 等效于使用：  
  
```csharp
#else  
#if  
```  
  
 使用 `#elif` 更简单，因为每个 `#if` 均需要 [#endif](./preprocessor-endif.md)，但 `#elif` 可在没有匹配的 `#endif` 的情况下使用。  
  
 有关如何使用 [ 的示例，请参阅 ](./preprocessor-if.md)#if`#elif`。  
  
## <a name="see-also"></a>另请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 预处理器指令](./index.md)
