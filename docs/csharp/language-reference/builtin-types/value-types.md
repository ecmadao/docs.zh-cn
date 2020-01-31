---
title: 值类型 - C# 参考
ms.date: 01/22/2020
f1_keywords:
- cs.valuetypes
helpviewer_keywords:
- value types [C#]
- types [C#], value types
- C# language, value types
ms.assetid: 471eb994-2958-49d5-a6be-19b4313f80a3
ms.openlocfilehash: 6b96d65f657f2af1af5c9a245e956640ee06260e
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2020
ms.locfileid: "76748487"
---
# <a name="value-types-c-reference"></a><span data-ttu-id="d5b2b-102">值类型（C# 参考）</span><span class="sxs-lookup"><span data-stu-id="d5b2b-102">Value types (C# reference)</span></span>

<span data-ttu-id="d5b2b-103">值类型  和[引用类型](../keywords/reference-types.md)是 C# 类型的两个主要类别。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-103">*Value types* and [reference types](../keywords/reference-types.md) are the two main categories of C# types.</span></span> <span data-ttu-id="d5b2b-104">值类型的变量包含类型的实例。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-104">A variable of a value type contains an instance of the type.</span></span> <span data-ttu-id="d5b2b-105">它不同于引用类型的变量，后者包含对类型实例的引用。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-105">This differs from a variable of a reference type, which contains a reference to an instance of the type.</span></span> <span data-ttu-id="d5b2b-106">默认情况下，在[分配](../operators/assignment-operator.md)中，通过将自变量传递给方法或返回方法结果，来复制变量值。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-106">By default, on [assignment](../operators/assignment-operator.md), passing an argument to a method, or returning a method result, variable values are copied.</span></span> <span data-ttu-id="d5b2b-107">对于值类型变量，会复制相应的类型实例。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-107">In the case of value-type variables, the corresponding type instances are copied.</span></span> <span data-ttu-id="d5b2b-108">以下示例演示了该行为：</span><span class="sxs-lookup"><span data-stu-id="d5b2b-108">The following example demonstrates that behavior:</span></span>

[!code-csharp[copy of values](~/samples/csharp/language-reference/builtin-types/ValueTypes.cs#ValueTypeCopied)]

<span data-ttu-id="d5b2b-109">如前面的示例所示，对值类型变量的操作只影响存储在变量中的值类型实例。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-109">As the preceding example shows, operations on a value-type variable affect only that instance of the value type, stored in the variable.</span></span>

<span data-ttu-id="d5b2b-110">如果值类型包含引用类型的数据成员，则在复制值类型实例时，只会复制对引用类型实例的引用。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-110">If a value type contains a data member of a reference type, only the reference to the instance of the reference type is copied when a value-type instance is copied.</span></span> <span data-ttu-id="d5b2b-111">副本和原始值类型实例都具有对同一引用类型实例的访问权限。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-111">Both the copy and original value-type instance have access to the same reference-type instance.</span></span> <span data-ttu-id="d5b2b-112">以下示例演示了该行为：</span><span class="sxs-lookup"><span data-stu-id="d5b2b-112">The following example demonstrates that behavior:</span></span>

[!code-csharp[shallow copy](~/samples/csharp/language-reference/builtin-types/ValueTypes.cs#ShallowCopy)]

> [!NOTE]
> <span data-ttu-id="d5b2b-113">若要使代码更不易出错、更可靠，请定义并使用不可变的值类型。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-113">To make your code less error-prone and more robust, define and use immutable value types.</span></span> <span data-ttu-id="d5b2b-114">本文仅为演示目的使用可变值类型。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-114">This article uses mutable value types only for demonstration purposes.</span></span>

## <a name="kinds-of-value-types"></a><span data-ttu-id="d5b2b-115">值类型的种类</span><span class="sxs-lookup"><span data-stu-id="d5b2b-115">Kinds of value types</span></span>

<span data-ttu-id="d5b2b-116">值类型可以是以下种类之一：</span><span class="sxs-lookup"><span data-stu-id="d5b2b-116">A value type can be one of the two following kinds:</span></span>

- <span data-ttu-id="d5b2b-117">[结构类型](../keywords/struct.md)，用于封装数据和相关功能</span><span class="sxs-lookup"><span data-stu-id="d5b2b-117">a [structure type](../keywords/struct.md), which encapsulates data and related functionality</span></span>
- <span data-ttu-id="d5b2b-118">[枚举类型](enum.md)，由一组命名常数定义，表示一个选择或选择组合</span><span class="sxs-lookup"><span data-stu-id="d5b2b-118">an [enumeration type](enum.md), which is defined by a set of named constants and represents a choice or a combination of choices</span></span>

<span data-ttu-id="d5b2b-119">[可为 null 值类型](nullable-value-types.md) `T?` 表示其基础值类型 `T` 的所有值及额外的 [null](../keywords/null.md) 值。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-119">A [nullable value type](nullable-value-types.md) `T?` represents all values of its underlying value type `T` and an additional [null](../keywords/null.md) value.</span></span> <span data-ttu-id="d5b2b-120">不能将 `null` 分配给值类型的变量，除非它是可为 null 的值类型。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-120">You cannot assign `null` to a variable of a value type, unless it's a nullable value type.</span></span>

## <a name="built-in-value-types"></a><span data-ttu-id="d5b2b-121">内置值类型</span><span class="sxs-lookup"><span data-stu-id="d5b2b-121">Built-in value types</span></span>

<span data-ttu-id="d5b2b-122">C# 提供以下内置值类型，也称为“简单类型”  ：</span><span class="sxs-lookup"><span data-stu-id="d5b2b-122">C# provides the following built-in value types, also known as *simple types*:</span></span>

- [<span data-ttu-id="d5b2b-123">整型数值类型</span><span class="sxs-lookup"><span data-stu-id="d5b2b-123">Integral numeric types</span></span>](integral-numeric-types.md)
- [<span data-ttu-id="d5b2b-124">浮点型数值类型</span><span class="sxs-lookup"><span data-stu-id="d5b2b-124">Floating-point numeric types</span></span>](floating-point-numeric-types.md)
- <span data-ttu-id="d5b2b-125">[bool](bool.md)，表示布尔值</span><span class="sxs-lookup"><span data-stu-id="d5b2b-125">[bool](bool.md) that represents a Boolean value</span></span>
- <span data-ttu-id="d5b2b-126">[char](char.md)，表示 Unicode UTF-16 字符</span><span class="sxs-lookup"><span data-stu-id="d5b2b-126">[char](char.md) that represents a Unicode UTF-16 character</span></span>

<span data-ttu-id="d5b2b-127">所有简单值都是结构类型，它们与其他结构类型的不同之处在于，它们允许特定的额外操作：</span><span class="sxs-lookup"><span data-stu-id="d5b2b-127">All simple types are structure types and differ from other structure types in that they permit certain additional operations:</span></span>

- <span data-ttu-id="d5b2b-128">可以使用文字为简单类型提供值。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-128">You can use literals to provide a value of a simple type.</span></span> <span data-ttu-id="d5b2b-129">例如，`'A'` 是类型 `char` 的文本，`2001` 是类型 `int` 的文本。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-129">For example, `'A'` is a literal of the type `char` and `2001` is a literal of the type `int`.</span></span>

- <span data-ttu-id="d5b2b-130">可以使用 [const](../keywords/const.md) 关键字声明简单类型的常数。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-130">You can declare constants of the simple types with the [const](../keywords/const.md) keyword.</span></span> <span data-ttu-id="d5b2b-131">不能具有其他结构类型的常数。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-131">It's not possible to have constants of other structure types.</span></span>

- <span data-ttu-id="d5b2b-132">常数表达式的操作数都是简单类型的常数，在编译时进行评估。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-132">Constant expressions, whose operands are all constants of the simple types, are evaluated at compile time.</span></span>

<span data-ttu-id="d5b2b-133">从 C# 7.0 开始，C# 支持[值元组](../../tuples.md)。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-133">Beginning with C# 7.0, C# supports [value tuples](../../tuples.md).</span></span> <span data-ttu-id="d5b2b-134">值元组是值类型，而不是简单类型。</span><span class="sxs-lookup"><span data-stu-id="d5b2b-134">A value tuple is a value type, but not a simple type.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="d5b2b-135">C# 语言规范</span><span class="sxs-lookup"><span data-stu-id="d5b2b-135">C# language specification</span></span>

<span data-ttu-id="d5b2b-136">有关更多信息，请参阅 [C# 语言规范](~/_csharplang/spec/introduction.md)的以下部分：</span><span class="sxs-lookup"><span data-stu-id="d5b2b-136">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="d5b2b-137">值类型</span><span class="sxs-lookup"><span data-stu-id="d5b2b-137">Value types</span></span>](~/_csharplang/spec/types.md#value-types)
- [<span data-ttu-id="d5b2b-138">简单类型</span><span class="sxs-lookup"><span data-stu-id="d5b2b-138">Simple types</span></span>](~/_csharplang/spec/types.md#simple-types)
- [<span data-ttu-id="d5b2b-139">变量</span><span class="sxs-lookup"><span data-stu-id="d5b2b-139">Variables</span></span>](~/_csharplang/spec/variables.md)

## <a name="see-also"></a><span data-ttu-id="d5b2b-140">请参阅</span><span class="sxs-lookup"><span data-stu-id="d5b2b-140">See also</span></span>

- [<span data-ttu-id="d5b2b-141">C# 参考</span><span class="sxs-lookup"><span data-stu-id="d5b2b-141">C# reference</span></span>](../index.md)
- <xref:System.ValueType?displayProperty=nameWithType>
- [<span data-ttu-id="d5b2b-142">引用类型</span><span class="sxs-lookup"><span data-stu-id="d5b2b-142">Reference types</span></span>](../keywords/reference-types.md)