---
title: 枚举类型 - C# 参考
description: 了解表示选项或选项组合的 C# 枚举类型
ms.date: 12/13/2019
f1_keywords:
- enum
- enum_CSharpKeyword
helpviewer_keywords:
- enum keyword [C#]
- enum type [C#]
- enumeration type [C#]
- bit flags [C#]
ms.assetid: bbeb9a0f-e9b3-41ab-b0a6-c41b1a08974c
ms.openlocfilehash: 72bc867bf0a789279da9a01f97c85d96b78684ed
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75437953"
---
# <a name="enumeration-types-c-reference"></a><span data-ttu-id="5e0a8-103">枚举类型（C# 参考）</span><span class="sxs-lookup"><span data-stu-id="5e0a8-103">Enumeration types (C# reference)</span></span>

<span data-ttu-id="5e0a8-104">枚举类型是由基础[整数数值](integral-numeric-types.md)类型的一组命名常量定义的值类型。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-104">An enumeration type (or enum type) is a value type defined by a set of named constants of the underlying [integral numeric](integral-numeric-types.md) type.</span></span> <span data-ttu-id="5e0a8-105">若要定义枚举类型，请使用 `enum` 关键字并指定枚举成员  的名称：</span><span class="sxs-lookup"><span data-stu-id="5e0a8-105">To define an enumeration type, use the `enum` keyword and specify the names of *enum members*:</span></span>

```csharp
enum Season
{
    Spring,
    Summer,
    Autumn,
    Winter
}
```

<span data-ttu-id="5e0a8-106">默认情况下，枚举成员的关联常数值为类型 `int`；它们从零开始，并按定义文本顺序递增 1。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-106">By default, the associated constant values of enum members are of type `int`; they start with zero and increase by one following the definition text order.</span></span> <span data-ttu-id="5e0a8-107">可以显式指定任何其他[整数数值](integral-numeric-types.md)类型作为枚举类型的基础类型。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-107">You can explicitly specify any other [integral numeric](integral-numeric-types.md) type as an underlying type of an enumeration type.</span></span> <span data-ttu-id="5e0a8-108">还可以显式指定关联的常数值，如下面的示例所示：</span><span class="sxs-lookup"><span data-stu-id="5e0a8-108">You also can explicitly specify the associated constant values, as the following example shows:</span></span>

```csharp
enum ErrorCode : ushort
{
    None = 0,
    Unknown = 1,
    ConnectionLost = 100,
    OutlierReading = 200
}
```

<span data-ttu-id="5e0a8-109">不能在枚举类型的定义内定义方法。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-109">You cannot define a method inside the definition of an enumeration type.</span></span> <span data-ttu-id="5e0a8-110">若要向枚举类型添加功能，请创建[扩展方法](../../programming-guide/classes-and-structs/extension-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-110">To add functionality to an enumeration type, create an [extension method](../../programming-guide/classes-and-structs/extension-methods.md).</span></span>

<span data-ttu-id="5e0a8-111">枚举类型 `E` 的默认值是由表达式 `(E)0` 生成的值，即使零没有相应的枚举成员也是如此。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-111">The default value of an enumeration type `E` is the value produced by expression `(E)0`, even if zero doesn't have the corresponding enum member.</span></span>

<span data-ttu-id="5e0a8-112">可以使用枚举类型，通过一组互斥值或选项组合来表示选项。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-112">You use an enumeration type to represent a choice from a set of mutually exclusive values or a combination of choices.</span></span> <span data-ttu-id="5e0a8-113">若要表示选项组合，请将枚举类型定义为位标志。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-113">To represent a combination of choices, define an enumeration type as bit flags.</span></span>

## <a name="enumeration-types-as-bit-flags"></a><span data-ttu-id="5e0a8-114">作为位标志的枚举类型</span><span class="sxs-lookup"><span data-stu-id="5e0a8-114">Enumeration types as bit flags</span></span>

<span data-ttu-id="5e0a8-115">如果希望枚举类型表示选项组合，请为这些选项定义枚举成员，以便单个选项成为位字段。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-115">If you want an enumeration type to represent a combination of choices, define enum members for those choices such that an individual choice is a bit field.</span></span> <span data-ttu-id="5e0a8-116">也就是说，这些枚举成员的关联值应该是 2 的幂。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-116">That is, the associated values of those enum members should be the powers of two.</span></span> <span data-ttu-id="5e0a8-117">然后，可以使用[按位逻辑运算符`|`或 `&`](../operators/bitwise-and-shift-operators.md#enumeration-logical-operators) 分别合并选项或交叉组合选项。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-117">Then, you can use the [bitwise logical operators `|` or `&`](../operators/bitwise-and-shift-operators.md#enumeration-logical-operators) to combine choices or intersect combinations of choices, respectively.</span></span> <span data-ttu-id="5e0a8-118">若要指示枚举类型声明位字段，请对其应用 [Flags](xref:System.FlagsAttribute) 属性。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-118">To indicate that an enumeration type declares bit fields, apply the [Flags](xref:System.FlagsAttribute) attribute to it.</span></span> <span data-ttu-id="5e0a8-119">如下面的示例所示，还可以在枚举类型的定义中包含一些典型组合。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-119">As the following example shows, you also can include some typical combinations in the definition of an enumeration type.</span></span>

[!code-csharp[enum flags](~/samples/csharp/language-reference/builtin-types/EnumType.cs#Flags)]

<span data-ttu-id="5e0a8-120">有关详细信息和示例，请参阅 <xref:System.FlagsAttribute?displayProperty=nameWithType> API 参考页和 <xref:System.Enum?displayProperty=nameWithType> API 参考页的[非独占成员和 Flags 属性](/dotnet/api/system.enum#non-exclusive-members-and-the-flags-attribute)部分。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-120">For more information and examples, see the <xref:System.FlagsAttribute?displayProperty=nameWithType> API reference page and the [Non-exclusive members and the Flags attribute](/dotnet/api/system.enum#non-exclusive-members-and-the-flags-attribute) section of the <xref:System.Enum?displayProperty=nameWithType> API reference page.</span></span>

## <a name="the-systemenum-type-and-enum-constraint"></a><span data-ttu-id="5e0a8-121">System.Enum 类型和枚举约束</span><span class="sxs-lookup"><span data-stu-id="5e0a8-121">The System.Enum type and enum constraint</span></span>

<span data-ttu-id="5e0a8-122"><xref:System.Enum?displayProperty=nameWithType> 类型是所有枚举类型的抽象基类。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-122">The <xref:System.Enum?displayProperty=nameWithType> type is the abstract base class of all enumeration types.</span></span> <span data-ttu-id="5e0a8-123">它提供多种方法来获取有关枚举类型及其值的信息。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-123">It provides a number of methods to get information about an enumeration type and its values.</span></span> <span data-ttu-id="5e0a8-124">有关更多信息和示例，请参阅 <xref:System.Enum?displayProperty=nameWithType> API 参考页。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-124">For more information and examples, see the <xref:System.Enum?displayProperty=nameWithType> API reference page.</span></span>

<span data-ttu-id="5e0a8-125">从 C# 7.3 开始，你可以在基类约束中使用 `System.Enum`（称为[枚举约束](../../programming-guide/generics/constraints-on-type-parameters.md#enum-constraints)），以指定类型参数为枚举类型。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-125">Beginning with C# 7.3, you can use `System.Enum` in a base class constraint (that is known as the [enum constraint](../../programming-guide/generics/constraints-on-type-parameters.md#enum-constraints)) to specify that a type parameter is an enumeration type.</span></span>

## <a name="conversions"></a><span data-ttu-id="5e0a8-126">转换</span><span class="sxs-lookup"><span data-stu-id="5e0a8-126">Conversions</span></span>

<span data-ttu-id="5e0a8-127">对于任何枚举类型，枚举类型与其基础整型类型之间存在显式转换。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-127">For any enumeration type, there exist explicit conversions between the enumeration type and its underlying integral type.</span></span> <span data-ttu-id="5e0a8-128">如果将枚举值[转换](../operators/type-testing-and-cast.md#cast-operator-)为其基础类型，则结果为枚举成员的关联整数值。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-128">If you [cast](../operators/type-testing-and-cast.md#cast-operator-) an enum value to its underlying type, the result is the associated integral value of an enum member.</span></span>

[!code-csharp[enum conversions](~/samples/csharp/language-reference/builtin-types/EnumType.cs#Conversions)]

<span data-ttu-id="5e0a8-129">使用 <xref:System.Enum.IsDefined%2A?displayProperty=nameWithType> 方法来确定枚举类型是否包含具有特定关联值的枚举成员。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-129">Use the <xref:System.Enum.IsDefined%2A?displayProperty=nameWithType> method to determine whether an enumeration type contains an enum member with the certain associated value.</span></span>

<span data-ttu-id="5e0a8-130">对于任何枚举类型，都存在分别与 <xref:System.Enum?displayProperty=nameWithType> 类型的[装箱和取消装箱](../../programming-guide/types/boxing-and-unboxing.md)相互转换。</span><span class="sxs-lookup"><span data-stu-id="5e0a8-130">For any enumeration type, there exist [boxing and unboxing](../../programming-guide/types/boxing-and-unboxing.md) conversions to and from the <xref:System.Enum?displayProperty=nameWithType> type, respectively.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="5e0a8-131">C# 语言规范</span><span class="sxs-lookup"><span data-stu-id="5e0a8-131">C# language specification</span></span>

<span data-ttu-id="5e0a8-132">有关更多信息，请参阅 [C# 语言规范](~/_csharplang/spec/introduction.md)的以下部分：</span><span class="sxs-lookup"><span data-stu-id="5e0a8-132">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="5e0a8-133">枚举</span><span class="sxs-lookup"><span data-stu-id="5e0a8-133">Enums</span></span>](~/_csharplang/spec/enums.md)
- [<span data-ttu-id="5e0a8-134">枚举值和操作</span><span class="sxs-lookup"><span data-stu-id="5e0a8-134">Enum values and operations</span></span>](~/_csharplang/spec/enums.md#enum-values-and-operations)
- [<span data-ttu-id="5e0a8-135">枚举逻辑运算符</span><span class="sxs-lookup"><span data-stu-id="5e0a8-135">Enumeration logical operators</span></span>](~/_csharplang/spec/expressions.md#enumeration-logical-operators)
- [<span data-ttu-id="5e0a8-136">枚举比较运算符</span><span class="sxs-lookup"><span data-stu-id="5e0a8-136">Enumeration comparison operators</span></span>](~/_csharplang/spec/expressions.md#enumeration-comparison-operators)
- [<span data-ttu-id="5e0a8-137">显式枚举转换</span><span class="sxs-lookup"><span data-stu-id="5e0a8-137">Explicit enumeration conversions</span></span>](~/_csharplang/spec/conversions.md#explicit-enumeration-conversions)
- [<span data-ttu-id="5e0a8-138">隐式枚举转换</span><span class="sxs-lookup"><span data-stu-id="5e0a8-138">Implicit enumeration conversions</span></span>](~/_csharplang/spec/conversions.md#implicit-enumeration-conversions)

## <a name="see-also"></a><span data-ttu-id="5e0a8-139">请参阅</span><span class="sxs-lookup"><span data-stu-id="5e0a8-139">See also</span></span>

- [<span data-ttu-id="5e0a8-140">C# 参考</span><span class="sxs-lookup"><span data-stu-id="5e0a8-140">C# reference</span></span>](../index.md)
- [<span data-ttu-id="5e0a8-141">枚举格式字符串</span><span class="sxs-lookup"><span data-stu-id="5e0a8-141">Enumeration format strings</span></span>](../../../standard/base-types/enumeration-format-strings.md)
- [<span data-ttu-id="5e0a8-142">枚举命名约定</span><span class="sxs-lookup"><span data-stu-id="5e0a8-142">Enum naming conventions</span></span>](../../../standard/design-guidelines/names-of-classes-structs-and-interfaces.md#naming-enumerations)
- [<span data-ttu-id="5e0a8-143">switch 语句</span><span class="sxs-lookup"><span data-stu-id="5e0a8-143">switch statement</span></span>](../keywords/switch.md)