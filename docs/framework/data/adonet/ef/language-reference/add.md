---
title: + （添加）
ms.date: 03/30/2017
ms.assetid: 51769b02-a8f7-4177-9e99-bbd10e77092c
ms.openlocfilehash: 62bb4782f135309eed8efa7e182fd8b75f92e126
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040295"
---
# <a name="-add"></a>+（添加）
将两个数相加。  
  
## <a name="syntax"></a>语法  
  
```csharp  
expression + expression  
```  
  
## <a name="arguments"></a>自变量  
 `expression`  
 任何一种数值数据类型的任何有效表达式。  
  
## <a name="result-types"></a>结果类型  
 对这两个参数进行隐式类型提升而产生的数据类型。 有关隐式类型升级的详细信息，请参阅[类型系统](type-system-entity-sql.md)。  
  
## <a name="remarks"></a>备注  
 对于 EDM.String 类型，加法指的是串联。  
  
## <a name="example"></a>示例  
 以下 Entity SQL 查询使用 + 算术运算符将两个数值相加。 此查询基于 AdventureWorks 销售模型。 若要编译并运行此查询，请执行下列步骤：  
  
1. 执行 [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md)中的过程。  
  
2. 将以下查询作为参数传递给 `ExecuteStructuralTypeQuery` 方法：  
  
 [!code-csharp[DP EntityServices Concepts 2#ADD](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#add)]  
  
## <a name="see-also"></a>请参阅

- [实体 SQL 引用](entity-sql-reference.md)
- [概念模型类型 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#conceptual-model-types-csdl)
