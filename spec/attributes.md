# <a name="attributes"></a><span data-ttu-id="c50c2-101">특성</span><span class="sxs-lookup"><span data-stu-id="c50c2-101">Attributes</span></span>

<span data-ttu-id="c50c2-102">C# 언어의 대부분 프로그램에서 정의 된 엔터티에 대 한 선언적 정보를 지정할 수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-102">Much of the C# language enables the programmer to specify declarative information about the entities defined in the program.</span></span> <span data-ttu-id="c50c2-103">사용 하 여 데코 레이트 하 여 클래스에서 메서드의 액세스 가능성은 지정 하는 예를 들어 합니다 *method_modifier*s `public`, `protected`, `internal`, 및 `private`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-103">For example, the accessibility of a method in a class is specified by decorating it with the *method_modifier*s `public`, `protected`, `internal`, and `private`.</span></span>

<span data-ttu-id="c50c2-104">C# 프로그래머 라고 하는 선언적 정보의 새 종류를 사용 하도록 설정 ***특성***합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-104">C# enables programmers to invent new kinds of declarative information, called ***attributes***.</span></span> <span data-ttu-id="c50c2-105">다음 프로그래머에 게 다양 한 프로그램 엔터티에 특성을 연결 하 고 런타임 환경의 특성 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-105">Programmers can then attach attributes to various program entities, and retrieve attribute information in a run-time environment.</span></span> <span data-ttu-id="c50c2-106">예를 들어 프레임 워크를 정의할 수는 `HelpAttribute` 해당 프로그램 요소에서 해당 설명서로의 매핑 수 있도록 특정 프로그램 요소 (예: 클래스 및 메서드)에 배치할 수 있는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-106">For instance, a framework might define a `HelpAttribute` attribute that can be placed on certain program elements (such as classes and methods) to provide a mapping from those program elements to their documentation.</span></span>

<span data-ttu-id="c50c2-107">특성은 특성 클래스의 선언을 통해 정의 됩니다 ([특성 클래스가](attributes.md#attribute-classes))에 위치와 명명 된 매개 변수가 있을 수 ([위치 및 명명 된 매개 변수](attributes.md#positional-and-named-parameters)).</span><span class="sxs-lookup"><span data-stu-id="c50c2-107">Attributes are defined through the declaration of attribute classes ([Attribute classes](attributes.md#attribute-classes)), which may have positional and named parameters ([Positional and named parameters](attributes.md#positional-and-named-parameters)).</span></span> <span data-ttu-id="c50c2-108">특성은 특성 사양을 사용 하 여 C# 프로그램의 엔터티에 연결 됩니다 ([특성 사양](attributes.md#attribute-specification)), 특성 인스턴스로 런타임에 검색할 수 있습니다 ([인스턴스 특성](attributes.md#attribute-instances)).</span><span class="sxs-lookup"><span data-stu-id="c50c2-108">Attributes are attached to entities in a C# program using attribute specifications ([Attribute specification](attributes.md#attribute-specification)), and can be retrieved at run-time as attribute instances ([Attribute instances](attributes.md#attribute-instances)).</span></span>

## <a name="attribute-classes"></a><span data-ttu-id="c50c2-109">특성 클래스</span><span class="sxs-lookup"><span data-stu-id="c50c2-109">Attribute classes</span></span>

<span data-ttu-id="c50c2-110">추상 클래스에서 파생 된 클래스 `System.Attribute`직접 또는 간접적으로 여부와 관계 없이 되는 ***특성 클래스***합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-110">A class that derives from the abstract class `System.Attribute`, whether directly or indirectly, is an ***attribute class***.</span></span> <span data-ttu-id="c50c2-111">특성 클래스의 선언 정의 종류의 새 ***특성*** 선언에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-111">The declaration of an attribute class defines a new kind of ***attribute*** that can be placed on a declaration.</span></span> <span data-ttu-id="c50c2-112">규칙에 따라 특성 클래스의 접미사가 붙은 `Attribute`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-112">By convention, attribute classes are named with a suffix of `Attribute`.</span></span> <span data-ttu-id="c50c2-113">특성의 사용 하 여 포함 하거나이 접미사를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-113">Uses of an attribute may either include or omit this suffix.</span></span>

### <a name="attribute-usage"></a><span data-ttu-id="c50c2-114">특성 사용</span><span class="sxs-lookup"><span data-stu-id="c50c2-114">Attribute usage</span></span>

<span data-ttu-id="c50c2-115">특성 `AttributeUsage` ([The AttributeUsage 특성](attributes.md#the-attributeusage-attribute)) 특성 클래스를 사용할 수 있는 방법을 설명 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-115">The attribute `AttributeUsage` ([The AttributeUsage attribute](attributes.md#the-attributeusage-attribute)) is used to describe how an attribute class can be used.</span></span>

<span data-ttu-id="c50c2-116">`AttributeUsage` 위치 매개 변수 ([위치 및 명명 된 매개 변수](attributes.md#positional-and-named-parameters)) 특성 클래스를 사용할 수 있습니다 선언의 종류를 지정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-116">`AttributeUsage` has a positional parameter ([Positional and named parameters](attributes.md#positional-and-named-parameters)) that enables an attribute class to specify the kinds of declarations on which it can be used.</span></span> <span data-ttu-id="c50c2-117">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="c50c2-117">The example</span></span>

```csharp
using System;

[AttributeUsage(AttributeTargets.Class | AttributeTargets.Interface)]
public class SimpleAttribute: Attribute 
{
    ...
}
```

<span data-ttu-id="c50c2-118">명명 된 특성 클래스를 정의 `SimpleAttribute` 에 배치할 수 있습니다 *class_declaration*s 및 *interface_declaration*만 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-118">defines an attribute class named `SimpleAttribute` that can be placed on *class_declaration*s and *interface_declaration*s only.</span></span> <span data-ttu-id="c50c2-119">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="c50c2-119">The example</span></span>

```csharp
[Simple] class Class1 {...}

[Simple] interface Interface1 {...}
```

<span data-ttu-id="c50c2-120">여러 번 사용 된 `Simple` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-120">shows several uses of the `Simple` attribute.</span></span> <span data-ttu-id="c50c2-121">이름을 사용 하 여이 특성이 정의 되어 있지만 `SimpleAttribute`이 특성을 사용 하는 경우는 `Attribute` 접미사 생략할 수 있으며, 짧은 이름에 결과 `Simple`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-121">Although this attribute is defined with the name `SimpleAttribute`, when this attribute is used, the `Attribute` suffix may be omitted, resulting in the short name `Simple`.</span></span> <span data-ttu-id="c50c2-122">따라서 위의 예제에서는 다음과 의미 체계가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-122">Thus, the example above is semantically equivalent to the following:</span></span>

```csharp
[SimpleAttribute] class Class1 {...}

[SimpleAttribute] interface Interface1 {...}
```

<span data-ttu-id="c50c2-123">`AttributeUsage` 명명 된 매개 변수 ([위치 및 명명 된 매개 변수](attributes.md#positional-and-named-parameters)) 이라는 `AllowMultiple`, 특성 지정 된 엔터티에 대 한 두 번 이상 지정할 수 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-123">`AttributeUsage` has a named parameter ([Positional and named parameters](attributes.md#positional-and-named-parameters)) called `AllowMultiple`, which indicates whether the attribute can be specified more than once for a given entity.</span></span> <span data-ttu-id="c50c2-124">하는 경우 `AllowMultiple` 특성에 대 한 클래스는 물론 다음 특성 클래스는를 ***다중 사용 특성 클래스***, 엔터티의 두 번 이상 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-124">If `AllowMultiple` for an attribute class is true, then that attribute class is a ***multi-use attribute class***, and can be specified more than once on an entity.</span></span> <span data-ttu-id="c50c2-125">하는 경우 `AllowMultiple` 특성에 대 한 클래스 false 또는 지정 되지 않으면 해당 특성 클래스는를 ***1 회용 특성 클래스***, 엔터티에 대해 한 번만 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-125">If `AllowMultiple` for an attribute class is false or it is unspecified, then that attribute class is a ***single-use attribute class***, and can be specified at most once on an entity.</span></span>

<span data-ttu-id="c50c2-126">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="c50c2-126">The example</span></span>

```csharp
using System;

[AttributeUsage(AttributeTargets.Class, AllowMultiple = true)]
public class AuthorAttribute: Attribute
{
    private string name;

    public AuthorAttribute(string name) {
        this.name = name;
    }

    public string Name {
        get { return name; }
    }
}
```

<span data-ttu-id="c50c2-127">라는 다중 사용 특성 클래스를 정의 `AuthorAttribute`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-127">defines a multi-use attribute class named `AuthorAttribute`.</span></span> <span data-ttu-id="c50c2-128">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="c50c2-128">The example</span></span>

```csharp
[Author("Brian Kernighan"), Author("Dennis Ritchie")] 
class Class1
{
    ...
}
```

<span data-ttu-id="c50c2-129">두 가지 용도 사용 하 여 클래스 선언을 보여 줍니다는 `Author` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-129">shows a class declaration with two uses of the `Author` attribute.</span></span>

<span data-ttu-id="c50c2-130">`AttributeUsage` 호출 하는 다른 명명 된 매개 변수가 `Inherited`, 특성, 기본 클래스에서 지정 된 경우 해당 기본 클래스에서 파생 된 클래스에서 상속 되었는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-130">`AttributeUsage` has another named parameter called `Inherited`, which indicates whether the attribute, when specified on a base class, is also inherited by classes that derive from that base class.</span></span> <span data-ttu-id="c50c2-131">경우 `Inherited` 클래스가 true 이면 특성에 대 한 다음 해당 특성에 상속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-131">If `Inherited` for an attribute class is true, then that attribute is inherited.</span></span> <span data-ttu-id="c50c2-132">경우 `Inherited` 특성 클래스는 false를 해당 특성은 상속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-132">If `Inherited` for an attribute class is false then that attribute is not inherited.</span></span> <span data-ttu-id="c50c2-133">이 지정 된 경우 해당 기본값은 true입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-133">If it is unspecified, its default value is true.</span></span>

<span data-ttu-id="c50c2-134">특성 클래스 `X` 없는 `AttributeUsage` 특성에서와 같이 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-134">An attribute class `X` not having an `AttributeUsage` attribute attached to it, as in</span></span>

```csharp
using System;

class X: Attribute {...}
```

<span data-ttu-id="c50c2-135">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-135">is equivalent to the following:</span></span>

```csharp
using System;

[AttributeUsage(
    AttributeTargets.All,
    AllowMultiple = false,
    Inherited = true)
]
class X: Attribute {...}
```

### <a name="positional-and-named-parameters"></a><span data-ttu-id="c50c2-136">위치 인수와 명명 된 매개 변수</span><span class="sxs-lookup"><span data-stu-id="c50c2-136">Positional and named parameters</span></span>

<span data-ttu-id="c50c2-137">특성 클래스를 가질 수 있습니다 ***위치 매개 변수*** 하 고 ***명명 된 매개 변수***합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-137">Attribute classes can have ***positional parameters*** and ***named parameters***.</span></span> <span data-ttu-id="c50c2-138">각 public 인스턴스 생성자는 특성 클래스에 대 한 올바른 시퀀스로 해당 특성 클래스에 대 한 위치 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-138">Each public instance constructor for an attribute class defines a valid sequence of positional parameters for that attribute class.</span></span> <span data-ttu-id="c50c2-139">특성 클래스에 대 한 각 속성과 비정적 공용 읽기 / 쓰기 필드인 특성 클래스에 대 한 명명된 된 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-139">Each non-static public read-write field and property for an attribute class defines a named parameter for the attribute class.</span></span>

<span data-ttu-id="c50c2-140">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="c50c2-140">The example</span></span>

```csharp
using System;

[AttributeUsage(AttributeTargets.Class)]
public class HelpAttribute: Attribute
{
    public HelpAttribute(string url) {        // Positional parameter
        ...
    }

    public string Topic {                     // Named parameter
        get {...}
        set {...}
    }

    public string Url {
        get {...}
    }
}
```

<span data-ttu-id="c50c2-141">명명 된 특성 클래스를 정의 `HelpAttribute` 위치 매개 변수를 `url`, 및 하나의 명명 된 매개 변수, `Topic`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-141">defines an attribute class named `HelpAttribute` that has one positional parameter, `url`, and one named parameter, `Topic`.</span></span> <span data-ttu-id="c50c2-142">Static이 아니고, 공용 속성 이지만 `Url` 읽기 / 쓰기 아니므로 명명된 된 매개 변수를 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-142">Although it is non-static and public, the property `Url` does not define a named parameter, since it is not read-write.</span></span>

<span data-ttu-id="c50c2-143">이 특성 클래스는 다음과 같이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-143">This attribute class might be used as follows:</span></span>

```csharp
[Help("http://www.mycompany.com/.../Class1.htm")]
class Class1
{
    ...
}

[Help("http://www.mycompany.com/.../Misc.htm", Topic = "Class2")]
class Class2
{
    ...
}
```

### <a name="attribute-parameter-types"></a><span data-ttu-id="c50c2-144">특성 매개 변수 형식</span><span class="sxs-lookup"><span data-stu-id="c50c2-144">Attribute parameter types</span></span>

<span data-ttu-id="c50c2-145">특성 클래스에 대 한 위치 및 명명 된 매개 변수 유형은 제한 합니다 ***매개 변수 형식 특성***는:</span><span class="sxs-lookup"><span data-stu-id="c50c2-145">The types of positional and named parameters for an attribute class are limited to the ***attribute parameter types***, which are:</span></span>

*  <span data-ttu-id="c50c2-146">다음 형식 중 하나: `bool`, `byte`, `char`, `double`, `float`, `int`, `long`를 `sbyte`, `short`를 `string`를 `uint`, `ulong`, `ushort`.</span><span class="sxs-lookup"><span data-stu-id="c50c2-146">One of the following types: `bool`, `byte`, `char`, `double`, `float`, `int`, `long`, `sbyte`, `short`, `string`, `uint`, `ulong`, `ushort`.</span></span>
*  <span data-ttu-id="c50c2-147">`object` 형식</span><span class="sxs-lookup"><span data-stu-id="c50c2-147">The type `object`.</span></span>
*  <span data-ttu-id="c50c2-148">`System.Type` 형식</span><span class="sxs-lookup"><span data-stu-id="c50c2-148">The type `System.Type`.</span></span>
*  <span data-ttu-id="c50c2-149">열거형 형식에 public 액세스 가능성이 있으며 있는 것은 중첩 된 형식을 (있는 경우)도 public 접근성이 있어야 제공 ([특성 사양](attributes.md#attribute-specification)).</span><span class="sxs-lookup"><span data-stu-id="c50c2-149">An enum type, provided it has public accessibility and the types in which it is nested (if any) also have public accessibility ([Attribute specification](attributes.md#attribute-specification)).</span></span>
*  <span data-ttu-id="c50c2-150">위 형식의 1 차원 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-150">Single-dimensional arrays of the above types.</span></span>
*  <span data-ttu-id="c50c2-151">특성 사양에서 위치 또는 명명 된 매개 변수로 생성자 인수 또는 이러한 형식 중 하나가 없는 public 필드를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-151">A constructor argument or public field which does not have one of these types, cannot be used as a positional or named parameter in an attribute specification.</span></span>

## <a name="attribute-specification"></a><span data-ttu-id="c50c2-152">특성 사양</span><span class="sxs-lookup"><span data-stu-id="c50c2-152">Attribute specification</span></span>

<span data-ttu-id="c50c2-153">***특성 사양*** 선언에는 이전에 정의 된 특성의 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-153">***Attribute specification*** is the application of a previously defined attribute to a declaration.</span></span> <span data-ttu-id="c50c2-154">특성 선언에 지정 된 추가 선언 정보 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-154">An attribute is a piece of additional declarative information that is specified for a declaration.</span></span> <span data-ttu-id="c50c2-155">특성 (특성을 포함 하는 어셈블리 또는 모듈에서 지정) 하는 전역 범위에서 지정할 수 있습니다 및에 대 한 *type_declaration*s ([형식 선언을](namespaces.md#type-declarations)), *class_member_declaration* s ([입력 매개 변수 제약 조건이](classes.md#type-parameter-constraints)), *interface_member_declaration*s ([인터페이스 멤버](interfaces.md#interface-members)), *struct_member _declaration*s ([구조체 멤버](structs.md#struct-members)), *enum_member_declaration*s ([열거형 멤버](enums.md#enum-members)), *accessor_declarations*  ([접근자](classes.md#accessors)), *event_accessor_declarations* ([필드와 유사한 이벤트](classes.md#field-like-events)), 및 *formal_parameter_list*s ([메서드 매개 변수](classes.md#method-parameters)).</span><span class="sxs-lookup"><span data-stu-id="c50c2-155">Attributes can be specified at global scope (to specify attributes on the containing assembly or module) and for *type_declaration*s ([Type declarations](namespaces.md#type-declarations)), *class_member_declaration*s ([Type parameter constraints](classes.md#type-parameter-constraints)), *interface_member_declaration*s ([Interface members](interfaces.md#interface-members)), *struct_member_declaration*s ([Struct members](structs.md#struct-members)), *enum_member_declaration*s ([Enum members](enums.md#enum-members)), *accessor_declarations* ([Accessors](classes.md#accessors)), *event_accessor_declarations* ([Field-like events](classes.md#field-like-events)), and *formal_parameter_list*s ([Method parameters](classes.md#method-parameters)).</span></span>

<span data-ttu-id="c50c2-156">에 지정 된 특성 ***섹션에서는 특성***합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-156">Attributes are specified in ***attribute sections***.</span></span> <span data-ttu-id="c50c2-157">특성 섹션을 쉼표로 구분 된 목록을 하나 이상의 특성을 감싸는 대괄호 쌍으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-157">An attribute section consists of a pair of square brackets, which surround a comma-separated list of one or more attributes.</span></span> <span data-ttu-id="c50c2-158">해당 목록에 지정 된 특성 및 동일한 프로그램 엔터티를 연결 하는 섹션 순서 정렬 순서는 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-158">The order in which attributes are specified in such a list, and the order in which sections attached to the same program entity are arranged, is not significant.</span></span> <span data-ttu-id="c50c2-159">예를 들어 특성 사양 `[A][B]`, `[B][A]`를 `[A,B]`, 및 `[B,A]` 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-159">For instance, the attribute specifications `[A][B]`, `[B][A]`, `[A,B]`, and `[B,A]` are equivalent.</span></span>

```antlr
global_attributes
    : global_attribute_section+
    ;

global_attribute_section
    : '[' global_attribute_target_specifier attribute_list ']'
    | '[' global_attribute_target_specifier attribute_list ',' ']'
    ;

global_attribute_target_specifier
    : global_attribute_target ':'
    ;

global_attribute_target
    : 'assembly'
    | 'module'
    ;

attributes
    : attribute_section+
    ;

attribute_section
    : '[' attribute_target_specifier? attribute_list ']'
    | '[' attribute_target_specifier? attribute_list ',' ']'
    ;

attribute_target_specifier
    : attribute_target ':'
    ;

attribute_target
    : 'field'
    | 'event'
    | 'method'
    | 'param'
    | 'property'
    | 'return'
    | 'type'
    ;

attribute_list
    : attribute (',' attribute)*
    ;

attribute
    : attribute_name attribute_arguments?
    ;

attribute_name
    : type_name
    ;

attribute_arguments
    : '(' positional_argument_list? ')'
    | '(' positional_argument_list ',' named_argument_list ')'
    | '(' named_argument_list ')'
    ;

positional_argument_list
    : positional_argument (',' positional_argument)*
    ;

positional_argument
    : attribute_argument_expression
    ;

named_argument_list
    : named_argument (','  named_argument)*
    ;

named_argument
    : identifier '=' attribute_argument_expression
    ;

attribute_argument_expression
    : expression
    ;
```

<span data-ttu-id="c50c2-160">특성으로 구성 됩니다는 *attribute_name* 및 선택적 인수 및 명명 된 인수 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-160">An attribute consists of an *attribute_name* and an optional list of positional and named arguments.</span></span> <span data-ttu-id="c50c2-161">위치 인수 (있는 경우) 명명 된 인수 앞에 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-161">The positional arguments (if any) precede the named arguments.</span></span> <span data-ttu-id="c50c2-162">구성 위치 인수는 *attribute_argument_expression*; 명명된 된 인수 뒤에 등호 뒤에 이름, 구성는 *attribute_argument_expression*는 함께 간단한 할당으로 동일한 규칙으로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-162">A positional argument consists of an *attribute_argument_expression*; a named argument consists of a name, followed by an equal sign, followed by an *attribute_argument_expression*, which, together, are constrained by the same rules as simple assignment.</span></span> <span data-ttu-id="c50c2-163">명명 된 인수의 순서가 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-163">The order of named arguments is not significant.</span></span>

<span data-ttu-id="c50c2-164">합니다 *attribute_name* 특성 클래스를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-164">The *attribute_name* identifies an attribute class.</span></span> <span data-ttu-id="c50c2-165">경우 형태로 *attribute_name* 됩니다 *type_name* 다음 특성 클래스에이 이름을 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-165">If the form of *attribute_name* is *type_name* then this name must refer to an attribute class.</span></span> <span data-ttu-id="c50c2-166">그렇지 않으면 컴파일 타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-166">Otherwise, a compile-time error occurs.</span></span> <span data-ttu-id="c50c2-167">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="c50c2-167">The example</span></span>

```csharp
class Class1 {}

[Class1] class Class2 {}    // Error
```

<span data-ttu-id="c50c2-168">사용 하려고 했기 때문에 컴파일 타임 오류가 발생 `Class1` 클래스를 특성으로 `Class1` 특성 클래스가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-168">results in a compile-time error because it attempts to use `Class1` as an attribute class when `Class1` is not an attribute class.</span></span>

<span data-ttu-id="c50c2-169">특정 컨텍스트 둘 이상의 대상에 특성의 사양을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-169">Certain contexts permit the specification of an attribute on more than one target.</span></span> <span data-ttu-id="c50c2-170">프로그램을 포함 하 여 대상을 명시적으로 지정할 수는 *attribute_target_specifier*합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-170">A program can explicitly specify the target by including an *attribute_target_specifier*.</span></span> <span data-ttu-id="c50c2-171">특성은 전역 수준에서 배치 되는 경우는 *global_attribute_target_specifier* 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-171">When an attribute is placed at the global level, a *global_attribute_target_specifier* is required.</span></span> <span data-ttu-id="c50c2-172">다른 모든 위치에서 적절 한 기본값은 적용 되지만 *attribute_target_specifier* 확인 하거나 특정 모호한 경우에서 기본값을 재정의 하려면 (또는 모호 하지 않은 경우에서 기본값을 확인만)에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-172">In all other locations, a reasonable default is applied, but an *attribute_target_specifier* can be used to affirm or override the default in certain ambiguous cases (or to just affirm the default in non-ambiguous cases).</span></span> <span data-ttu-id="c50c2-173">따라서, 일반적으로 *attribute_target_specifier*전역 수준에서 제외 하 고 s를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-173">Thus, typically, *attribute_target_specifier*s can be omitted except at the global level.</span></span> <span data-ttu-id="c50c2-174">잠재적으로 모호한 컨텍스트는 다음과 같이 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-174">The potentially ambiguous contexts are resolved as follows:</span></span>

*  <span data-ttu-id="c50c2-175">전역 범위에서 지정 된 특성 대상 어셈블리 또는 대상 모듈에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-175">An attribute specified at global scope can apply either to the target assembly or the target module.</span></span> <span data-ttu-id="c50c2-176">따라서이 컨텍스트에 대 한 기본값이 존재를 *attribute_target_specifier* 이 컨텍스트에서 항상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-176">No default exists for this context, so an *attribute_target_specifier* is always required in this context.</span></span> <span data-ttu-id="c50c2-177">현재 상태를 `assembly` *attribute_target_specifier* 대상 특성 적용 된다고 어셈블리;의 현재 상태를 `module` *attribute_target_specifier* 대상 모듈에는 특성이 적용 되는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-177">The presence of the `assembly` *attribute_target_specifier* indicates that the attribute applies to the target assembly; the presence of the `module` *attribute_target_specifier* indicates that the attribute applies to the target module.</span></span>
*  <span data-ttu-id="c50c2-178">Delegate 선언에서 지정 된 특성 선언 되는 대리자 또는 해당 반환 값에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-178">An attribute specified on a delegate declaration can apply either to the delegate being declared or to its return value.</span></span> <span data-ttu-id="c50c2-179">없는 경우에는 *attribute_target_specifier*, 특성이 대리자에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-179">In the absence of an *attribute_target_specifier*, the attribute applies to the delegate.</span></span> <span data-ttu-id="c50c2-180">현재 상태를 `type` *attribute_target_specifier* 대리자; 특성 적용 된다고의 존재를 `return` *attribute_target_specifier* 반환 값에는 특성이 적용 되는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-180">The presence of the `type` *attribute_target_specifier* indicates that the attribute applies to the delegate; the presence of the `return` *attribute_target_specifier* indicates that the attribute applies to the return value.</span></span>
*  <span data-ttu-id="c50c2-181">메서드 선언에서 지정 된 특성 선언 되는 메서드 또는 해당 반환 값에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-181">An attribute specified on a method declaration can apply either to the method being declared or to its return value.</span></span> <span data-ttu-id="c50c2-182">없는 경우에는 *attribute_target_specifier*, 메서드에 특성이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-182">In the absence of an *attribute_target_specifier*, the attribute applies to the method.</span></span> <span data-ttu-id="c50c2-183">현재 상태를 `method` *attribute_target_specifier* ; 메서드에 특성 적용 된다고의 존재를 `return` *attribute_target_specifier* 나타냅니다 특성에는 반환 값에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-183">The presence of the `method` *attribute_target_specifier* indicates that the attribute applies to the method; the presence of the `return` *attribute_target_specifier* indicates that the attribute applies to the return value.</span></span>
*  <span data-ttu-id="c50c2-184">연산자 선언에 지정 된 특성 선언 되는 연산자 또는 해당 반환 값에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-184">An attribute specified on an operator declaration can apply either to the operator being declared or to its return value.</span></span> <span data-ttu-id="c50c2-185">없는 경우에는 *attribute_target_specifier*, 특성 연산자에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-185">In the absence of an *attribute_target_specifier*, the attribute applies to the operator.</span></span> <span data-ttu-id="c50c2-186">현재 상태를 `method` *attribute_target_specifier* 연산자 특성 적용 된다고의 존재를 `return` *attribute_target_specifier* 반환 값에는 특성이 적용 되는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-186">The presence of the `method` *attribute_target_specifier* indicates that the attribute applies to the operator; the presence of the `return` *attribute_target_specifier* indicates that the attribute applies to the return value.</span></span>
*  <span data-ttu-id="c50c2-187">이벤트 접근자를 생략 하는 이벤트 선언에서 지정 된 특성 선언 되는 이벤트, (이벤트가 추상이 아닌) 하는 경우 연결 된 필드 또는 관련된 추가 적용 하 고 메서드를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-187">An attribute specified on an event declaration that omits event accessors can apply to the event being declared, to the associated field (if the event is not abstract), or to the associated add and remove methods.</span></span> <span data-ttu-id="c50c2-188">없는 경우에는 *attribute_target_specifier*, 이벤트에 특성이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-188">In the absence of an *attribute_target_specifier*, the attribute applies to the event.</span></span> <span data-ttu-id="c50c2-189">현재 상태를 `event` *attribute_target_specifier* 이벤트 특성 적용 된다고의 존재를 `field` *attribute_target_specifier* 나타냅니다 특성 필드에 적용 합니다. 및의 현재 상태를 `method` *attribute_target_specifier* 메서드에 특성 적용 된다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-189">The presence of the `event` *attribute_target_specifier* indicates that the attribute applies to the event; the presence of the `field` *attribute_target_specifier* indicates that the attribute applies to the field; and the presence of the `method` *attribute_target_specifier* indicates that the attribute applies to the methods.</span></span>
*  <span data-ttu-id="c50c2-190">속성 또는 인덱서의 선언에 대 한 get 접근자 선언에 지정 된 특성이 연결된 된 메서드 또는 해당 반환 값에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-190">An attribute specified on a get accessor declaration for a property or indexer declaration can apply either to the associated method or to its return value.</span></span> <span data-ttu-id="c50c2-191">없는 경우에는 *attribute_target_specifier*, 메서드에 특성이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-191">In the absence of an *attribute_target_specifier*, the attribute applies to the method.</span></span> <span data-ttu-id="c50c2-192">현재 상태를 `method` *attribute_target_specifier* ; 메서드에 특성 적용 된다고의 존재를 `return` *attribute_target_specifier* 나타냅니다 특성에는 반환 값에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-192">The presence of the `method` *attribute_target_specifier* indicates that the attribute applies to the method; the presence of the `return` *attribute_target_specifier* indicates that the attribute applies to the return value.</span></span>
*  <span data-ttu-id="c50c2-193">속성 또는 인덱서의 선언에 대 한 set 접근자에 지정 된 특성의 유일한 암시적 매개 변수 또는 연결된 된 메서드를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-193">An attribute specified on a set accessor for a property or indexer declaration can apply either to the associated method or to its lone implicit parameter.</span></span> <span data-ttu-id="c50c2-194">없는 경우에는 *attribute_target_specifier*, 메서드에 특성이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-194">In the absence of an *attribute_target_specifier*, the attribute applies to the method.</span></span> <span data-ttu-id="c50c2-195">현재 상태를 `method` *attribute_target_specifier* ; 메서드에 특성 적용 된다고의 존재를 `param` *attribute_target_specifier* 나타냅니다 매개 변수에;는 특성이 적용 되는 현재 상태를 `return` *attribute_target_specifier* 특성 반환 값에 적용 되도록 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-195">The presence of the `method` *attribute_target_specifier* indicates that the attribute applies to the method; the presence of the `param` *attribute_target_specifier* indicates that the attribute applies to the parameter; the presence of the `return` *attribute_target_specifier* indicates that the attribute applies to the return value.</span></span>
*  <span data-ttu-id="c50c2-196">이벤트 선언 또는 연결된 된 메서드의 유일한 매개 변수를 적용할 수에 add 또는 remove 접근자 선언에 지정 된 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-196">An attribute specified on an add or remove accessor declaration for an event declaration can apply either to the associated method or to its lone parameter.</span></span> <span data-ttu-id="c50c2-197">없는 경우에는 *attribute_target_specifier*, 메서드에 특성이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-197">In the absence of an *attribute_target_specifier*, the attribute applies to the method.</span></span> <span data-ttu-id="c50c2-198">현재 상태를 `method` *attribute_target_specifier* ; 메서드에 특성 적용 된다고의 존재를 `param` *attribute_target_specifier* 나타냅니다 매개 변수에;는 특성이 적용 되는 현재 상태를 `return` *attribute_target_specifier* 특성 반환 값에 적용 되도록 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-198">The presence of the `method` *attribute_target_specifier* indicates that the attribute applies to the method; the presence of the `param` *attribute_target_specifier* indicates that the attribute applies to the parameter; the presence of the `return` *attribute_target_specifier* indicates that the attribute applies to the return value.</span></span>

<span data-ttu-id="c50c2-199">다른 컨텍스트에서 포함 여부는 *attribute_target_specifier* 허용 하지만 불필요 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-199">In other contexts, inclusion of an *attribute_target_specifier* is permitted but unnecessary.</span></span> <span data-ttu-id="c50c2-200">예를 들어, 클래스 선언 수 포함 하거나 지정자를 생략 `type`:</span><span class="sxs-lookup"><span data-stu-id="c50c2-200">For instance, a class declaration may either include or omit the specifier `type`:</span></span>

```csharp
[type: Author("Brian Kernighan")]
class Class1 {}

[Author("Dennis Ritchie")]
class Class2 {}
```

<span data-ttu-id="c50c2-201">잘못 된을 지정 하면 오류가 발생 *attribute_target_specifier*합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-201">It is an error to specify an invalid *attribute_target_specifier*.</span></span> <span data-ttu-id="c50c2-202">예를 들어 지정자 `param` 클래스 선언에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-202">For instance, the specifier `param` cannot be used on a class declaration:</span></span>

```csharp
[param: Author("Brian Kernighan")]        // Error
class Class1 {}
```

<span data-ttu-id="c50c2-203">규칙에 따라 특성 클래스의 접미사가 붙은 `Attribute`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-203">By convention, attribute classes are named with a suffix of `Attribute`.</span></span> <span data-ttu-id="c50c2-204">*attribute_name* 양식의 *type_name* 포함 하거나이 접미사를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-204">An *attribute_name* of the form *type_name* may either include or omit this suffix.</span></span> <span data-ttu-id="c50c2-205">있으면 특성 클래스 둘 다 사용 하 여 하지 않고이 접미사는 모호성을 사용할 수 있는지 및 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-205">If an attribute class is found both with and without this suffix, an ambiguity is present, and a compile-time error results.</span></span> <span data-ttu-id="c50c2-206">경우는 *attribute_name* 철자가 되도록 해당 가장 오른쪽 *식별자* 축 자 식별자 ([식별자](lexical-structure.md#identifiers)), 접미사가 없는 특성만 일치 하면 다음 따라서 해결 해야 하는 이러한 모호성을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-206">If the *attribute_name* is spelled such that its right-most *identifier* is a verbatim identifier ([Identifiers](lexical-structure.md#identifiers)), then only an attribute without a suffix is matched, thus enabling such an ambiguity to be resolved.</span></span> <span data-ttu-id="c50c2-207">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="c50c2-207">The example</span></span>

```csharp
using System;

[AttributeUsage(AttributeTargets.All)]
public class X: Attribute
{}

[AttributeUsage(AttributeTargets.All)]
public class XAttribute: Attribute
{}

[X]                     // Error: ambiguity
class Class1 {}

[XAttribute]            // Refers to XAttribute
class Class2 {}

[@X]                    // Refers to X
class Class3 {}

[@XAttribute]           // Refers to XAttribute
class Class4 {}
```

<span data-ttu-id="c50c2-208">두 특성 클래스 표시 `X` 고 `XAttribute`입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-208">shows two attribute classes named `X` and `XAttribute`.</span></span> <span data-ttu-id="c50c2-209">특성 `[X]` 되며 중 하나를 참조할 수 있으므로 모호한 `X` 또는 `XAttribute`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-209">The attribute `[X]` is ambiguous, since it could refer to either `X` or `XAttribute`.</span></span> <span data-ttu-id="c50c2-210">축 자 식별자를 사용 하 여 정확한 의도를 이러한 드문 경우에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-210">Using a verbatim identifier allows the exact intent to be specified in such rare cases.</span></span> <span data-ttu-id="c50c2-211">특성 `[XAttribute]` 모호 하지 않은 경우 (특성 클래스가 되었으면 하지만 `XAttributeAttribute`!).</span><span class="sxs-lookup"><span data-stu-id="c50c2-211">The attribute `[XAttribute]` is not ambiguous (although it would be if there was an attribute class named `XAttributeAttribute`!).</span></span> <span data-ttu-id="c50c2-212">경우 클래스의 선언을 `X` 제거 되 면 두 특성 모두 라는 특성 클래스를 참조 하는 다음 `XAttribute`같이:</span><span class="sxs-lookup"><span data-stu-id="c50c2-212">If the declaration for class `X` is removed, then both attributes refer to the attribute class named `XAttribute`, as follows:</span></span>

```csharp
using System;

[AttributeUsage(AttributeTargets.All)]
public class XAttribute: Attribute
{}

[X]                     // Refers to XAttribute
class Class1 {}

[XAttribute]            // Refers to XAttribute
class Class2 {}

[@X]                    // Error: no attribute named "X"
class Class3 {}
```

<span data-ttu-id="c50c2-213">이 클래스를 사용 하는 1 회용 특성 두 번 이상 동일한 엔터티에 컴파일 타임 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-213">It is a compile-time error to use a single-use attribute class more than once on the same entity.</span></span> <span data-ttu-id="c50c2-214">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="c50c2-214">The example</span></span>

```csharp
using System;

[AttributeUsage(AttributeTargets.Class)]
public class HelpStringAttribute: Attribute
{
    string value;

    public HelpStringAttribute(string value) {
        this.value = value;
    }

    public string Value {
        get {...}
    }
}

[HelpString("Description of Class1")]
[HelpString("Another description of Class1")]
public class Class1 {}
```

<span data-ttu-id="c50c2-215">사용 하려고 했기 때문에 컴파일 타임 오류가 발생 `HelpString`에 1 회용 특성 클래스에 두 번 이상 선언 시 `Class1`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-215">results in a compile-time error because it attempts to use `HelpString`, which is a single-use attribute class, more than once on the declaration of `Class1`.</span></span>

<span data-ttu-id="c50c2-216">식을 `E` 되는 *attribute_argument_expression* 다음 문 중 모두 만족 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="c50c2-216">An expression `E` is an *attribute_argument_expression* if all of the following statements are true:</span></span>

*  <span data-ttu-id="c50c2-217">유형의 `E` 특성 매개 변수 형식입니다 ([매개 변수 형식 특성](attributes.md#attribute-parameter-types)).</span><span class="sxs-lookup"><span data-stu-id="c50c2-217">The type of `E` is an attribute parameter type ([Attribute parameter types](attributes.md#attribute-parameter-types)).</span></span>
*  <span data-ttu-id="c50c2-218">컴파일 타임의 값에 `E` 다음 중 하나를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-218">At compile-time, the value of `E` can be resolved to one of the following:</span></span>
   * <span data-ttu-id="c50c2-219">상수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-219">A constant value.</span></span>
   * <span data-ttu-id="c50c2-220">`System.Type` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-220">A `System.Type` object.</span></span>
   * <span data-ttu-id="c50c2-221">1 차원 배열의 *attribute_argument_expression*s입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-221">A one-dimensional array of *attribute_argument_expression*s.</span></span>

<span data-ttu-id="c50c2-222">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c50c2-222">For example:</span></span>

```csharp
using System;

[AttributeUsage(AttributeTargets.Class)]
public class TestAttribute: Attribute
{
    public int P1 {
        get {...}
        set {...}
    }

    public Type P2 {
        get {...}
        set {...}
    }

    public object P3 {
        get {...}
        set {...}
    }
}

[Test(P1 = 1234, P3 = new int[] {1, 3, 5}, P2 = typeof(float))]
class MyClass {}
```

<span data-ttu-id="c50c2-223">A *typeof_expression* ([typeof 연산자](expressions.md#the-typeof-operator)) 사용 하는 제네릭이 아닌 형식, 폐쇄형된 생성된 형식, 또는 바인딩되지 않은 제네릭 형식이 특성 인수 식을 참조할 수 있지만 참조할 수 없습니다는 형식을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-223">A *typeof_expression* ([The typeof operator](expressions.md#the-typeof-operator)) used as an attribute argument expression can reference a non-generic type, a closed constructed type, or an unbound generic type, but it cannot reference an open type.</span></span> <span data-ttu-id="c50c2-224">이렇게 하면 컴파일 시간 식을 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-224">This is to ensure that the expression can be resolved at compile-time.</span></span>

```csharp
class A: Attribute
{
    public A(Type t) {...}
}

class G<T>
{
    [A(typeof(T))] T t;                  // Error, open type in attribute
}

class X
{
    [A(typeof(List<int>))] int x;        // Ok, closed constructed type
    [A(typeof(List<>))] int y;           // Ok, unbound generic type
}
```

## <a name="attribute-instances"></a><span data-ttu-id="c50c2-225">특성 인스턴스</span><span class="sxs-lookup"><span data-stu-id="c50c2-225">Attribute instances</span></span>

<span data-ttu-id="c50c2-226">***특성 인스턴스가*** 런타임 시 특성을 나타내는 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-226">An ***attribute instance*** is an instance that represents an attribute at run-time.</span></span> <span data-ttu-id="c50c2-227">특성은 특성 클래스를 위치 인수를 사용 하 여 정의 되 고 명명 된 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-227">An attribute is defined with an attribute class, positional arguments, and named arguments.</span></span> <span data-ttu-id="c50c2-228">특성 인스턴스는 위치와 명명 된 인수를 사용 하 여 초기화 되는 특성 클래스의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-228">An attribute instance is an instance of the attribute class that is initialized with the positional and named arguments.</span></span>

<span data-ttu-id="c50c2-229">다음 섹션에 설명 된 대로 컴파일 타임 및 런타임 모두 처리를 포함 하는 특성 인스턴스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-229">Retrieval of an attribute instance involves both compile-time and run-time processing, as described in the following sections.</span></span>

### <a name="compilation-of-an-attribute"></a><span data-ttu-id="c50c2-230">특성의 컴파일</span><span class="sxs-lookup"><span data-stu-id="c50c2-230">Compilation of an attribute</span></span>

<span data-ttu-id="c50c2-231">컴파일하는 *특성* 특성 클래스를 사용 하 여 `T`, *positional_argument_list* `P` 고 *named_argument_list* `N`, 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-231">The compilation of an *attribute* with attribute class `T`, *positional_argument_list* `P` and *named_argument_list* `N`, consists of the following steps:</span></span>

*  <span data-ttu-id="c50c2-232">컴파일에 대 한 컴파일 시간 처리 단계는 *object_creation_expression* 양식의 `new T(P)`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-232">Follow the compile-time processing steps for compiling an *object_creation_expression* of the form `new T(P)`.</span></span> <span data-ttu-id="c50c2-233">이 단계는 컴파일 타임 오류가를 발생 시키거나 결정 인스턴스 생성자 `C` 에서 `T` 런타임 시 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-233">These steps either result in a compile-time error, or determine an instance constructor `C` on `T` that can be invoked at run-time.</span></span>
*  <span data-ttu-id="c50c2-234">경우 `C` 되지 않은 public 액세스 가능성을 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-234">If `C` does not have public accessibility, then a compile-time error occurs.</span></span>
*  <span data-ttu-id="c50c2-235">각 *named_argument* `Arg` 에서 `N`:</span><span class="sxs-lookup"><span data-stu-id="c50c2-235">For each *named_argument* `Arg` in `N`:</span></span>
   * <span data-ttu-id="c50c2-236">수 있도록 `Name` 수는 *식별자* 의 합니다 *named_argument* `Arg`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-236">Let `Name` be the *identifier* of the *named_argument* `Arg`.</span></span>
   * <span data-ttu-id="c50c2-237">`Name` 비정적 읽기 / 쓰기 공용 필드 또는 속성을 식별 해야 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-237">`Name` must identify a non-static read-write public field or property on `T`.</span></span> <span data-ttu-id="c50c2-238">경우 `T` 그러한 필드 또는 속성에 컴파일 타임 오류가 발생 하는 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-238">If `T` has no such field or property, then a compile-time error occurs.</span></span>
*  <span data-ttu-id="c50c2-239">특성의 런타임 인스턴스화에 대 한 다음 정보를 보관: 특성 클래스 `T`, 인스턴스 생성자 `C` 온 `T`의 *positional_argument_list* `P` 하며 *named_argument_list* `N`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-239">Keep the following information for run-time instantiation of the attribute: the attribute class `T`, the instance constructor `C` on `T`, the *positional_argument_list* `P` and the *named_argument_list* `N`.</span></span>

### <a name="run-time-retrieval-of-an-attribute-instance"></a><span data-ttu-id="c50c2-240">특성 인스턴스의 런타임 검색</span><span class="sxs-lookup"><span data-stu-id="c50c2-240">Run-time retrieval of an attribute instance</span></span>

<span data-ttu-id="c50c2-241">컴파일하는 *특성* 특성 클래스를 생성 `T`, 인스턴스 생성자 `C` 에 `T`, *positional_argument_list* `P`, 및 *named_argument_list* `N`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-241">Compilation of an *attribute* yields an attribute class `T`, an instance constructor `C` on `T`, a *positional_argument_list* `P`, and a *named_argument_list* `N`.</span></span> <span data-ttu-id="c50c2-242">주어진이 정보로 특성 인스턴스를 다음 단계를 사용 하 여 런타임 시 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-242">Given this information, an attribute instance can be retrieved at run-time using the following steps:</span></span>

*  <span data-ttu-id="c50c2-243">실행에 대 한 런타임 처리 단계는 *object_creation_expression* 양식의 `new T(P)`, 인스턴스 생성자를 사용 하 여 `C` 컴파일 시간에 따라.</span><span class="sxs-lookup"><span data-stu-id="c50c2-243">Follow the run-time processing steps for executing an *object_creation_expression* of the form `new T(P)`, using the instance constructor `C` as determined at compile-time.</span></span> <span data-ttu-id="c50c2-244">이러한 단계는 예외를 발생 시키거나 인스턴스를 생성 `O` 의 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-244">These steps either result in an exception, or produce an instance `O` of `T`.</span></span>
*  <span data-ttu-id="c50c2-245">각 *named_argument* `Arg` 에서 `N`, 순서에서:</span><span class="sxs-lookup"><span data-stu-id="c50c2-245">For each *named_argument* `Arg` in `N`, in order:</span></span>
   * <span data-ttu-id="c50c2-246">수 있도록 `Name` 수는 *식별자* 의 합니다 *named_argument* `Arg`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-246">Let `Name` be the *identifier* of the *named_argument* `Arg`.</span></span> <span data-ttu-id="c50c2-247">하는 경우 `Name` 비정적 공용 읽기 / 쓰기 필드 또는 속성으로 식별 하지 않습니다 `O`, 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-247">If `Name` does not identify a non-static public read-write field or property on `O`, then an exception is thrown.</span></span>
   * <span data-ttu-id="c50c2-248">수 있도록 `Value` 평가의 결과 *attribute_argument_expression* 의 `Arg`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-248">Let `Value` be the result of evaluating the *attribute_argument_expression* of `Arg`.</span></span>
   * <span data-ttu-id="c50c2-249">하는 경우 `Name` 에서 필드를 식별 `O`, 그런 다음이 필드를 설정 `Value`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-249">If `Name` identifies a field on `O`, then set this field to `Value`.</span></span>
   * <span data-ttu-id="c50c2-250">그렇지 않으면 `Name` 에서 속성을 식별 `O`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-250">Otherwise, `Name` identifies a property on `O`.</span></span> <span data-ttu-id="c50c2-251">이 속성을 설정 `Value`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-251">Set this property to `Value`.</span></span>
   * <span data-ttu-id="c50c2-252">결과 `O`, 특성 클래스의 인스턴스 `T` 로 초기화 된는 합니다 *positional_argument_list* `P` 하며 *named_argument_list* `N`.</span><span class="sxs-lookup"><span data-stu-id="c50c2-252">The result is `O`, an instance of the attribute class `T` that has been initialized with the *positional_argument_list* `P` and the *named_argument_list* `N`.</span></span>

## <a name="reserved-attributes"></a><span data-ttu-id="c50c2-253">예약 된 특성</span><span class="sxs-lookup"><span data-stu-id="c50c2-253">Reserved attributes</span></span>

<span data-ttu-id="c50c2-254">소수의 특성 어떤 방식으로든에서 언어를 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-254">A small number of attributes affect the language in some way.</span></span> <span data-ttu-id="c50c2-255">이러한 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-255">These attributes include:</span></span>

*  <span data-ttu-id="c50c2-256">`System.AttributeUsageAttribute` ([The AttributeUsage 특성](attributes.md#the-attributeusage-attribute))에 특성 클래스를 사용할 수 있는 방법에 설명 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-256">`System.AttributeUsageAttribute` ([The AttributeUsage attribute](attributes.md#the-attributeusage-attribute)), which is used to describe the ways in which an attribute class can be used.</span></span>
*  <span data-ttu-id="c50c2-257">`System.Diagnostics.ConditionalAttribute` ([The 조건부 특성](attributes.md#the-conditional-attribute))에 조건부 메서드를 정의 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-257">`System.Diagnostics.ConditionalAttribute` ([The Conditional attribute](attributes.md#the-conditional-attribute)), which is used to define conditional methods.</span></span>
*  <span data-ttu-id="c50c2-258">`System.ObsoleteAttribute` ([The Obsolete 특성](attributes.md#the-obsolete-attribute))에 사용 되지 않는 멤버를 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-258">`System.ObsoleteAttribute` ([The Obsolete attribute](attributes.md#the-obsolete-attribute)), which is used to mark a member as obsolete.</span></span>
*  <span data-ttu-id="c50c2-259">`System.Runtime.CompilerServices.CallerLineNumberAttribute`를 `System.Runtime.CompilerServices.CallerFilePathAttribute` 하 고 `System.Runtime.CompilerServices.CallerMemberNameAttribute` ([호출자 정보 특성](attributes.md#caller-info-attributes)), 선택적 매개 변수를 호출 컨텍스트에 대 한 정보를 제공 하는 데 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-259">`System.Runtime.CompilerServices.CallerLineNumberAttribute`, `System.Runtime.CompilerServices.CallerFilePathAttribute` and `System.Runtime.CompilerServices.CallerMemberNameAttribute` ([Caller info attributes](attributes.md#caller-info-attributes)), which are used to supply information about the calling context to optional parameters.</span></span>

### <a name="the-attributeusage-attribute"></a><span data-ttu-id="c50c2-260">AttributeUsage 특성</span><span class="sxs-lookup"><span data-stu-id="c50c2-260">The AttributeUsage attribute</span></span>

<span data-ttu-id="c50c2-261">특성 `AttributeUsage` 특성 클래스를 사용할 수 있는 방식으로 설명 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-261">The attribute `AttributeUsage` is used to describe the manner in which the attribute class can be used.</span></span>

<span data-ttu-id="c50c2-262">사용 하 여 데코 레이트 된 클래스는 `AttributeUsage` 특성에서 파생 되어야 합니다 `System.Attribute`를 직접 또는 간접적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-262">A class that is decorated with the `AttributeUsage` attribute must derive from `System.Attribute`, either directly or indirectly.</span></span> <span data-ttu-id="c50c2-263">그렇지 않으면 컴파일 타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-263">Otherwise, a compile-time error occurs.</span></span>

```csharp
namespace System
{
    [AttributeUsage(AttributeTargets.Class)]
    public class AttributeUsageAttribute: Attribute
    {
        public AttributeUsageAttribute(AttributeTargets validOn) {...}
        public virtual bool AllowMultiple { get {...} set {...} }
        public virtual bool Inherited { get {...} set {...} }
        public virtual AttributeTargets ValidOn { get {...} }
    }

    public enum AttributeTargets
    {
        Assembly     = 0x0001,
        Module       = 0x0002,
        Class        = 0x0004,
        Struct       = 0x0008,
        Enum         = 0x0010,
        Constructor  = 0x0020,
        Method       = 0x0040,
        Property     = 0x0080,
        Field        = 0x0100,
        Event        = 0x0200,
        Interface    = 0x0400,
        Parameter    = 0x0800,
        Delegate     = 0x1000,
        ReturnValue  = 0x2000,

        All = Assembly | Module | Class | Struct | Enum | Constructor | 
            Method | Property | Field | Event | Interface | Parameter | 
            Delegate | ReturnValue
    }
}
```

### <a name="the-conditional-attribute"></a><span data-ttu-id="c50c2-264">조건부 특성</span><span class="sxs-lookup"><span data-stu-id="c50c2-264">The Conditional attribute</span></span>

<span data-ttu-id="c50c2-265">특성 `Conditional` 의 정의 사용 하도록 설정 ***조건부 메서드이므로*** 하 고 ***조건부 특성 클래스***합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-265">The attribute `Conditional` enables the definition of ***conditional methods*** and ***conditional attribute classes***.</span></span>

```csharp
namespace System.Diagnostics
{
    [AttributeUsage(AttributeTargets.Method | AttributeTargets.Class, AllowMultiple = true)]
    public class ConditionalAttribute: Attribute
    {
        public ConditionalAttribute(string conditionString) {...}
        public string ConditionString { get {...} }
    }
}
```

#### <a name="conditional-methods"></a><span data-ttu-id="c50c2-266">조건부 메서드</span><span class="sxs-lookup"><span data-stu-id="c50c2-266">Conditional methods</span></span>

<span data-ttu-id="c50c2-267">메서드를 사용 하 여 데코 레이트 된 `Conditional` 특성이 조건부 메서드.</span><span class="sxs-lookup"><span data-stu-id="c50c2-267">A method decorated with the `Conditional` attribute is a conditional method.</span></span> <span data-ttu-id="c50c2-268">`Conditional` 특성 조건부 컴파일 기호를 테스트 하 여 상태를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-268">The `Conditional` attribute indicates a condition by testing a conditional compilation symbol.</span></span> <span data-ttu-id="c50c2-269">조건부 메서드를 호출 포함 되거나 호출 시이 기호가 정의 되었는지 여부에 따라 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-269">Calls to a conditional method are either included or omitted depending on whether this symbol is defined at the point of the call.</span></span> <span data-ttu-id="c50c2-270">기호가 정의 된 경우 호출 포함 합니다. 그렇지 않으면 호출 (수신기의 평가 및 호출의 매개 변수 포함)은 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-270">If the symbol is defined, the call is included; otherwise, the call (including evaluation of the receiver and parameters of the call) is omitted.</span></span>

<span data-ttu-id="c50c2-271">조건부 메서드는 다음과 같은 제한 사항이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-271">A conditional method is subject to the following restrictions:</span></span>

*  <span data-ttu-id="c50c2-272">조건부 메서드는 메서드가 이어야 합니다는 *class_declaration* 하거나 *struct_declaration*합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-272">The conditional method must be a method in a *class_declaration* or *struct_declaration*.</span></span> <span data-ttu-id="c50c2-273">컴파일 타임 오류가 발생 하는 경우는 `Conditional` 인터페이스 선언에서 메서드에 특성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-273">A compile-time error occurs if the `Conditional` attribute is specified on a method in an interface declaration.</span></span>
*  <span data-ttu-id="c50c2-274">조건부 메서드는 반환 형식이 있어야 합니다. `void`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-274">The conditional method must have a return type of `void`.</span></span>
*  <span data-ttu-id="c50c2-275">조건부 메서드를 사용 하 여 표시 되 면 안 된 `override` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-275">The conditional method must not be marked with the `override` modifier.</span></span> <span data-ttu-id="c50c2-276">하지만 조건부 메서드를 사용 하 여 표시 될 수도 있습니다는 `virtual` 한정자 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-276">A conditional method may be marked with the `virtual` modifier, however.</span></span> <span data-ttu-id="c50c2-277">이러한 메서드의 재정의 암시적 조건부 및 사용 하 여 명시적으로 표시 해서는 안을 `Conditional` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-277">Overrides of such a method are implicitly conditional, and must not be explicitly marked with a `Conditional` attribute.</span></span>
*  <span data-ttu-id="c50c2-278">조건부 메서드는 인터페이스 메서드의 구현을 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-278">The conditional method must not be an implementation of an interface method.</span></span> <span data-ttu-id="c50c2-279">그렇지 않으면 컴파일 타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-279">Otherwise, a compile-time error occurs.</span></span>

<span data-ttu-id="c50c2-280">또한 컴파일 시간 오류가 발생 하는 조건부 메서드를 사용 하는 경우는 *delegate_creation_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-280">In addition, a compile-time error occurs if a conditional method is used in a *delegate_creation_expression*.</span></span> <span data-ttu-id="c50c2-281">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="c50c2-281">The example</span></span>

```csharp
#define DEBUG

using System;
using System.Diagnostics;

class Class1 
{
    [Conditional("DEBUG")]
    public static void M() {
        Console.WriteLine("Executed Class1.M");
    }
}

class Class2
{
    public static void Test() {
        Class1.M();
    }
}
```

<span data-ttu-id="c50c2-282">선언 `Class1.M` 조건부 메서드로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-282">declares `Class1.M` as a conditional method.</span></span> <span data-ttu-id="c50c2-283">`Class2``Test` 메서드에서이 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-283">`Class2`'s `Test` method calls this method.</span></span> <span data-ttu-id="c50c2-284">조건부 컴파일 기호를 이후 `DEBUG` 정의 된 경우 `Class2.Test` 은 호출, 호출 `M`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-284">Since the conditional compilation symbol `DEBUG` is defined, if `Class2.Test` is called, it will call `M`.</span></span> <span data-ttu-id="c50c2-285">경우 기호가 `DEBUG` 하지을 정의한 후 `Class2.Test` 호출 하지는 `Class1.M`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-285">If the symbol `DEBUG` had not been defined, then `Class2.Test` would not call `Class1.M`.</span></span>

<span data-ttu-id="c50c2-286">호출 시 조건부 컴파일 기호로 포함 또는 제외 조건부 메서드 호출의 제어 하는 것이 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-286">It is important to note that the inclusion or exclusion of a call to a conditional method is controlled by the conditional compilation symbols at the point of the call.</span></span> <span data-ttu-id="c50c2-287">예제</span><span class="sxs-lookup"><span data-stu-id="c50c2-287">In the example</span></span>

<span data-ttu-id="c50c2-288">파일 `class1.cs`:</span><span class="sxs-lookup"><span data-stu-id="c50c2-288">File `class1.cs`:</span></span>

```csharp
using System.Diagnostics;

class Class1 
{
    [Conditional("DEBUG")]
    public static void F() {
        Console.WriteLine("Executed Class1.F");
    }
}
```

<span data-ttu-id="c50c2-289">파일 `class2.cs`:</span><span class="sxs-lookup"><span data-stu-id="c50c2-289">File `class2.cs`:</span></span>

```csharp
#define DEBUG

class Class2
{
    public static void G() {
        Class1.F();                // F is called
    }
}
```

<span data-ttu-id="c50c2-290">파일 `class3.cs`:</span><span class="sxs-lookup"><span data-stu-id="c50c2-290">File `class3.cs`:</span></span>

```csharp
#undef DEBUG

class Class3
{
    public static void H() {
        Class1.F();                // F is not called
    }
}
```

<span data-ttu-id="c50c2-291">클래스 `Class2` 하 고 `Class3` 조건부 메서드 호출이 각각 포함 `Class1.F`, 여부에 따라 조건부는 `DEBUG` 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-291">the classes `Class2` and `Class3` each contain calls to the conditional method `Class1.F`, which is conditional based on whether or not `DEBUG` is defined.</span></span> <span data-ttu-id="c50c2-292">컨텍스트에서이 기호 정의 되므로 `Class2` 아닌 `Class3`에 대 한 호출 `F` 에서 `Class2` 호출 하는 동안 포함 되어 `F` 에서 `Class3` 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-292">Since this symbol is defined in the context of `Class2` but not `Class3`, the call to `F` in `Class2` is included, while the call to `F` in `Class3` is omitted.</span></span>

<span data-ttu-id="c50c2-293">상속 체인의 조건부 메서드를 사용 하는 혼동 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-293">The use of conditional methods in an inheritance chain can be confusing.</span></span> <span data-ttu-id="c50c2-294">통해 조건부 메서드 호출 `base`, 폼의 `base.M`, 일반 조건부 메서드 호출 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-294">Calls made to a conditional method through `base`, of the form `base.M`, are subject to the normal conditional method call rules.</span></span> <span data-ttu-id="c50c2-295">예제</span><span class="sxs-lookup"><span data-stu-id="c50c2-295">In the example</span></span>

<span data-ttu-id="c50c2-296">파일 `class1.cs`:</span><span class="sxs-lookup"><span data-stu-id="c50c2-296">File `class1.cs`:</span></span>

```csharp
using System;
using System.Diagnostics;

class Class1 
{
    [Conditional("DEBUG")]
    public virtual void M() {
        Console.WriteLine("Class1.M executed");
    }
}
```

<span data-ttu-id="c50c2-297">파일 `class2.cs`:</span><span class="sxs-lookup"><span data-stu-id="c50c2-297">File `class2.cs`:</span></span>

```csharp
using System;

class Class2: Class1
{
    public override void M() {
        Console.WriteLine("Class2.M executed");
        base.M();                        // base.M is not called!
    }
}
```

<span data-ttu-id="c50c2-298">파일 `class3.cs`:</span><span class="sxs-lookup"><span data-stu-id="c50c2-298">File `class3.cs`:</span></span>

```csharp
#define DEBUG

using System;

class Class3
{
    public static void Test() {
        Class2 c = new Class2();
        c.M();                            // M is called
    }
}
```

<span data-ttu-id="c50c2-299">`Class2` 호출을 포함 합니다 `M` 기본 클래스에서 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-299">`Class2` includes a call to the `M` defined in its base class.</span></span> <span data-ttu-id="c50c2-300">기본 메서드는 기호 유무에 따라 조건부 때문에이 호출이 생략 됩니다 `DEBUG`, 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-300">This call is omitted because the base method is conditional based on the presence of the symbol `DEBUG`, which is undefined.</span></span> <span data-ttu-id="c50c2-301">따라서 메서드는 콘솔에 씁니다 "`Class2.M executed`"만 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-301">Thus, the method writes to the console "`Class2.M executed`" only.</span></span> <span data-ttu-id="c50c2-302">적절히 사용 *pp_declaration*s는 이러한 문제를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-302">Judicious use of *pp_declaration*s can eliminate such problems.</span></span>

#### <a name="conditional-attribute-classes"></a><span data-ttu-id="c50c2-303">조건부 특성 클래스</span><span class="sxs-lookup"><span data-stu-id="c50c2-303">Conditional attribute classes</span></span>

<span data-ttu-id="c50c2-304">특성 클래스 ([특성 클래스가](attributes.md#attribute-classes)) 하나 이상의으로 데코 레이트 `Conditional` 특성은는 ***조건부 특성 클래스***합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-304">An attribute class ([Attribute classes](attributes.md#attribute-classes)) decorated with one or more `Conditional` attributes is a ***conditional attribute class***.</span></span> <span data-ttu-id="c50c2-305">에 선언 된 조건부 컴파일 기호를 사용 하 여 조건부 특성 클래스는 연결 되므로 해당 `Conditional` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-305">A conditional attribute class is thus associated with the conditional compilation symbols declared in its `Conditional` attributes.</span></span> <span data-ttu-id="c50c2-306">이 예제에서:</span><span class="sxs-lookup"><span data-stu-id="c50c2-306">This example:</span></span>

```csharp
using System;
using System.Diagnostics;
[Conditional("ALPHA")]
[Conditional("BETA")]
public class TestAttribute : Attribute {}
```

<span data-ttu-id="c50c2-307">선언 `TestAttribute` 조건부 컴파일 기호를 사용 하 여 연결 하는 조건부 특성 클래스로 `ALPHA` 고 `BETA`입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-307">declares `TestAttribute` as a conditional attribute class associated with the conditional compilations symbols `ALPHA` and `BETA`.</span></span>

<span data-ttu-id="c50c2-308">특성 사양 ([특성 사양](attributes.md#attribute-specification)) 조건부 특성의 경우 포함 된 해당 연결 된 조건부 컴파일 기호 중 하나 이상이 고, 그렇지 시점 사양에 정의 된 특성 사양 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-308">Attribute specifications ([Attribute specification](attributes.md#attribute-specification)) of a conditional attribute are included if one or more of its associated conditional compilation symbols is defined at the point of specification, otherwise the attribute specification is omitted.</span></span>

<span data-ttu-id="c50c2-309">포함 또는 제외의 조건부 특성 클래스의 특성 사양 조건부 컴파일 기호 지정 시점으로 제어 됩니다 하는 것이 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-309">It is important to note that the inclusion or exclusion of an attribute specification of a conditional attribute class is controlled by the conditional compilation symbols at the point of the specification.</span></span> <span data-ttu-id="c50c2-310">예제</span><span class="sxs-lookup"><span data-stu-id="c50c2-310">In the example</span></span>

<span data-ttu-id="c50c2-311">파일 `test.cs`:</span><span class="sxs-lookup"><span data-stu-id="c50c2-311">File `test.cs`:</span></span>

```csharp
using System;
using System.Diagnostics;

[Conditional("DEBUG")]

public class TestAttribute : Attribute {}
```

<span data-ttu-id="c50c2-312">파일 `class1.cs`:</span><span class="sxs-lookup"><span data-stu-id="c50c2-312">File `class1.cs`:</span></span>

```csharp
#define DEBUG

[Test]                // TestAttribute is specified

class Class1 {}
```

<span data-ttu-id="c50c2-313">파일 `class2.cs`:</span><span class="sxs-lookup"><span data-stu-id="c50c2-313">File `class2.cs`:</span></span>

```csharp
#undef DEBUG

[Test]                 // TestAttribute is not specified

class Class2 {}
```

<span data-ttu-id="c50c2-314">클래스 `Class1` 하 고 `Class2` 는 특성으로 데코레이팅된 각 `Test`, 여부에 따라 조건부는 `DEBUG` 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-314">the classes `Class1` and `Class2` are each decorated with attribute `Test`, which is conditional based on whether or not `DEBUG` is defined.</span></span> <span data-ttu-id="c50c2-315">컨텍스트에서이 기호 정의 되므로 `Class1` 아닌 `Class2`, 사양의 `Test` 특성을 `Class1` 지정 하는 동안 포함 됩니다는 `Test` 특성을 `Class2` 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-315">Since this symbol is defined in the context of `Class1` but not `Class2`, the specification of the `Test` attribute on `Class1` is included, while the specification of the `Test` attribute on `Class2` is omitted.</span></span>

### <a name="the-obsolete-attribute"></a><span data-ttu-id="c50c2-316">Obsolete 특성</span><span class="sxs-lookup"><span data-stu-id="c50c2-316">The Obsolete attribute</span></span>

<span data-ttu-id="c50c2-317">특성 `Obsolete` 형식 및 더 이상 사용 해야 하는 형식의 멤버를 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-317">The attribute `Obsolete` is used to mark types and members of types that should no longer be used.</span></span>

```csharp
namespace System
{
    [AttributeUsage(
        AttributeTargets.Class | 
        AttributeTargets.Struct |
        AttributeTargets.Enum | 
        AttributeTargets.Interface | 
        AttributeTargets.Delegate |
        AttributeTargets.Method | 
        AttributeTargets.Constructor |
        AttributeTargets.Property | 
        AttributeTargets.Field |
        AttributeTargets.Event,
        Inherited = false)
    ]
    public class ObsoleteAttribute: Attribute
    {
        public ObsoleteAttribute() {...}
        public ObsoleteAttribute(string message) {...}
        public ObsoleteAttribute(string message, bool error) {...}
        public string Message { get {...} }
        public bool IsError { get {...} }
    }
}
```

<span data-ttu-id="c50c2-318">형식 또는 멤버가 사용 하 여 데코 레이트 된 프로그램을 사용 하는 경우는 `Obsolete` 특성, 컴파일러가 경고 또는 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-318">If a program uses a type or member that is decorated with the `Obsolete` attribute, the compiler issues a warning or an error.</span></span> <span data-ttu-id="c50c2-319">특히, 컴파일러가 경고 또는 오류 매개 변수가 제공 되 고 기본값이 없는 오류 매개 변수를 제공 하는 경우 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-319">Specifically, the compiler issues a warning if no error parameter is provided, or if the error parameter is provided and has the value `false`.</span></span> <span data-ttu-id="c50c2-320">컴파일러에서 오류가 발생 하는 경우 오류 매개 변수가 지정 되 고 기본값이 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-320">The compiler issues an error if the error parameter is specified and has the value `true`.</span></span>

<span data-ttu-id="c50c2-321">예제</span><span class="sxs-lookup"><span data-stu-id="c50c2-321">In the example</span></span>

```csharp
[Obsolete("This class is obsolete; use class B instead")]
class A
{
    public void F() {}
}

class B
{
    public void F() {}
}

class Test
{
    static void Main() {
        A a = new A();         // Warning
        a.F();
    }
}
```

<span data-ttu-id="c50c2-322">클래스 `A` 으로 데코 레이트 된는 `Obsolete` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-322">the class `A` is decorated with the `Obsolete` attribute.</span></span> <span data-ttu-id="c50c2-323">사용할 때마다 `A` 에서 `Main` 지정된 된 메시지를 포함 하는 경고 결과 "이이 클래스는 사용 되지 않습니다. 클래스 B 대신 사용 합니다. "</span><span class="sxs-lookup"><span data-stu-id="c50c2-323">Each use of `A` in `Main` results in a warning that includes the specified message, "This class is obsolete; use class B instead."</span></span>

### <a name="caller-info-attributes"></a><span data-ttu-id="c50c2-324">호출자 정보 특성</span><span class="sxs-lookup"><span data-stu-id="c50c2-324">Caller info attributes</span></span>

<span data-ttu-id="c50c2-325">로깅 및 보고와 같은 용도로 유용한 경우가 함수 멤버 호출 코드에 대 한 특정 컴파일 시간 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-325">For purposes such as logging and reporting, it is sometimes useful for a function member to obtain certain compile-time information about the calling code.</span></span> <span data-ttu-id="c50c2-326">호출자 정보 특성에는 이러한 정보를 투명 하 게 전달 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-326">The caller info attributes provide a way to pass such information transparently.</span></span>

<span data-ttu-id="c50c2-327">호출자 정보 특성 중 하나를 사용 하 여 선택적 매개 변수 주석이 지정 되어 있는 경우 호출에서 해당 인수를 생략 하면 발생 하지 않습니다 반드시 대체 해야 하는 기본 매개 변수 값.</span><span class="sxs-lookup"><span data-stu-id="c50c2-327">When an optional parameter is annotated with one of the caller info attributes, omitting the corresponding argument in a call does not necessarily cause the default parameter value to be substituted.</span></span> <span data-ttu-id="c50c2-328">대신 호출 컨텍스트에 대해 지정 된 정보를 사용할 수 있는 경우 해당 정보는 인수 값으로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-328">Instead, if the specified information about the calling context is available, that information will be passed as the argument value.</span></span>

<span data-ttu-id="c50c2-329">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c50c2-329">For example:</span></span>

```csharp
using System.Runtime.CompilerServices

...

public void Log(
    [CallerLineNumber] int line = -1,
    [CallerFilePath]   string path = null,
    [CallerMemberName] string name = null
)
{
    Console.WriteLine((line < 0) ? "No line" : "Line "+ line);
    Console.WriteLine((path == null) ? "No file path" : path);
    Console.WriteLine((name == null) ? "No member name" : name);
}
```

<span data-ttu-id="c50c2-330">에 대 한 호출 `Log()` 인수 없이 호출의 줄 번호 및 파일 경로는 호출이 발생 한 멤버의 이름을 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-330">A call to `Log()` with no arguments would print the line number and file path of the call, as well as the name of the member within which the call occurred.</span></span>

<span data-ttu-id="c50c2-331">호출자 정보 특성 대리자 선언을 포함 하 여 선택적 매개 변수 어디에서 나 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-331">Caller info attributes can occur on optional parameters anywhere, including in delegate declarations.</span></span> <span data-ttu-id="c50c2-332">그러나 특정 호출자 정보 특성 매개 변수 형식으로 암시적 변환이 대체 값에서은 항상 특성 수는 매개 변수의 형식에 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-332">However, the specific caller info attributes have restrictions on the types of the parameters they can attribute, so that there will always be an implicit conversion from a substituted value to the parameter type.</span></span>

<span data-ttu-id="c50c2-333">이 동일한 호출자 정보 특성 매개 변수 정의 및 partial 메서드 선언의 일부를 구현 하는 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-333">It is an error to have the same caller info attribute on a parameter of both the defining and implementing part of a partial method declaration.</span></span> <span data-ttu-id="c50c2-334">구현에 발생 하는 호출자 정보 특성은 무시 됩니다. 반면 호출자 정보 특성 정의에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-334">Only caller info attributes in the defining part are applied, whereas caller info attributes occurring only in the implementing part are ignored.</span></span>

<span data-ttu-id="c50c2-335">호출자 정보 오버 로드 확인에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-335">Caller information does not affect overload resolution.</span></span> <span data-ttu-id="c50c2-336">오버 로드 확인 다른 생략 된 선택적 매개 변수는 무시 동일한 방식으로 이러한 매개 변수를 무시 호출자의 소스 코드에서 여전히 생략 하면 선택적 매개 변수에 특성 사용된 하는 대로 ([오버 로드 확인](expressions.md#overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="c50c2-336">As the attributed optional parameters are still omitted from the source code of the caller, overload resolution ignores those parameters in the same way it ignores other omitted optional parameters ([Overload resolution](expressions.md#overload-resolution)).</span></span>

<span data-ttu-id="c50c2-337">호출자 정보는 함수의 소스 코드에서 명시적으로 호출 될 때에 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-337">Caller information is only substituted when a function is explicitly invoked in source code.</span></span> <span data-ttu-id="c50c2-338">암시적 부모 생성자 호출 같은 암시적 호출 원본 위치를 갖지 않으며 호출자 정보를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-338">Implicit invocations such as implicit parent constructor calls do not have a source location and will not substitute caller information.</span></span> <span data-ttu-id="c50c2-339">또한 동적으로 바인딩되는 호출이 호출자 정보를 대체 하지 않습니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-339">Also, calls that are dynamically bound will not substitute caller information.</span></span> <span data-ttu-id="c50c2-340">때 이러한 경우 특성이 지정 된 매개 변수가 생략 되는 호출자 정보, 매개 변수는 지정 된 기본 값 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-340">When a caller info attributed parameter is omitted in such cases, the specified default value of the parameter is used instead.</span></span>

<span data-ttu-id="c50c2-341">예외에는 쿼리 식입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-341">One exception is query-expressions.</span></span> <span data-ttu-id="c50c2-342">구문 확장 간주 됩니다 및 호출자 정보 호출자 정보 특성을 사용 하 여 선택적 매개 변수를 생략 하려면 확장할 호출을 하는 경우 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-342">These are considered syntactic expansions, and if the calls they expand to omit optional parameters with caller info attributes, caller information will be substituted.</span></span> <span data-ttu-id="c50c2-343">사용 되는 위치에는 호출에서 생성 된 쿼리 절의 위치가입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-343">The location used is the location of the query clause which the call was generated from.</span></span>

<span data-ttu-id="c50c2-344">다음 순서 대로 기본 설정 된 둘 이상의 호출자 정보 특성을 지정 된 매개 변수에서 지정 하는 경우: `CallerLineNumber`하십시오 `CallerFilePath`, `CallerMemberName`합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-344">If more than one caller info attribute is specified on a given parameter, they are preferred in the following order: `CallerLineNumber`, `CallerFilePath`, `CallerMemberName`.</span></span>

#### <a name="the-callerlinenumber-attribute"></a><span data-ttu-id="c50c2-345">CallerLineNumber 특성</span><span class="sxs-lookup"><span data-stu-id="c50c2-345">The CallerLineNumber attribute</span></span>

<span data-ttu-id="c50c2-346">`System.Runtime.CompilerServices.CallerLineNumberAttribute` 표준 암시적 변환을 때 선택적 매개 변수에서 허용 됩니다 ([표준 암시적 변환이](conversions.md#standard-implicit-conversions))에서 상수 값을 `int.MaxValue` 매개 변수의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-346">The `System.Runtime.CompilerServices.CallerLineNumberAttribute` is allowed on optional parameters when there is a standard implicit conversion ([Standard implicit conversions](conversions.md#standard-implicit-conversions)) from the constant value `int.MaxValue` to the parameter's type.</span></span> <span data-ttu-id="c50c2-347">이렇게 하면 오류 없이 해당 값까지 모든 음수가 아닌 줄 번호를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-347">This ensures that any non-negative line number up to that value can be passed without error.</span></span>

<span data-ttu-id="c50c2-348">소스 코드의 위치에서 함수 호출을 사용 하 여 선택적 매개 변수를 생략 하는 경우는 `CallerLineNumberAttribute`, 해당 위치의 줄 번호를 나타내는 숫자 리터럴을 기본 매개 변수 값을 대신 호출에 대 한 인수로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-348">If a function invocation from a location in source code omits an optional parameter with the `CallerLineNumberAttribute`, then a numeric literal representing that location's line number is used as an argument to the invocation instead of the default parameter value.</span></span>

<span data-ttu-id="c50c2-349">호출에서 여러 줄에 걸쳐 있는 경우 선택한 줄은 구현에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-349">If the invocation spans multiple lines, the line chosen is implementation-dependent.</span></span>

<span data-ttu-id="c50c2-350">줄 번호를 영향을 받을 수 있는 참고 `#line` 지시문 ([지시문 줄](lexical-structure.md#line-directives)).</span><span class="sxs-lookup"><span data-stu-id="c50c2-350">Note that the line number may be affected by `#line` directives ([Line directives](lexical-structure.md#line-directives)).</span></span>

#### <a name="the-callerfilepath-attribute"></a><span data-ttu-id="c50c2-351">CallerFilePath 특성</span><span class="sxs-lookup"><span data-stu-id="c50c2-351">The CallerFilePath attribute</span></span>

<span data-ttu-id="c50c2-352">합니다 `System.Runtime.CompilerServices.CallerFilePathAttribute` 표준 암시적 변환을 때 선택적 매개 변수에서 허용 됩니다 ([표준 암시적 변환이](conversions.md#standard-implicit-conversions))에서 `string` 매개 변수의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-352">The `System.Runtime.CompilerServices.CallerFilePathAttribute` is allowed on optional parameters when there is a standard implicit conversion ([Standard implicit conversions](conversions.md#standard-implicit-conversions)) from `string` to the parameter's type.</span></span>

<span data-ttu-id="c50c2-353">소스 코드의 위치에서 함수 호출을 사용 하 여 선택적 매개 변수를 생략 하는 경우는 `CallerFilePathAttribute`, 해당 위치의 파일 경로 나타내는 문자열 리터럴 매개 변수 기본값 대신 호출에 대 한 인수로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-353">If a function invocation from a location in source code omits an optional parameter with the `CallerFilePathAttribute`, then a string literal representing that location's file path is used as an argument to the invocation instead of the default parameter value.</span></span>

<span data-ttu-id="c50c2-354">파일 경로의 형식은 구현에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-354">The format of the file path is implementation-dependent.</span></span>

<span data-ttu-id="c50c2-355">파일 경로 따라 달라질 수 있습니다 `#line` 지시문 ([지시문 줄](lexical-structure.md#line-directives)).</span><span class="sxs-lookup"><span data-stu-id="c50c2-355">Note that the file path may be affected by `#line` directives ([Line directives](lexical-structure.md#line-directives)).</span></span>

#### <a name="the-callermembername-attribute"></a><span data-ttu-id="c50c2-356">CallerMemberName 특성</span><span class="sxs-lookup"><span data-stu-id="c50c2-356">The CallerMemberName attribute</span></span>

<span data-ttu-id="c50c2-357">합니다 `System.Runtime.CompilerServices.CallerMemberNameAttribute` 표준 암시적 변환을 때 선택적 매개 변수에서 허용 됩니다 ([표준 암시적 변환이](conversions.md#standard-implicit-conversions))에서 `string` 매개 변수의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-357">The `System.Runtime.CompilerServices.CallerMemberNameAttribute` is allowed on optional parameters when there is a standard implicit conversion ([Standard implicit conversions](conversions.md#standard-implicit-conversions)) from `string` to the parameter's type.</span></span>

<span data-ttu-id="c50c2-358">소스 코드와 선택적 매개 변수를 생략 자체 또는 해당 반환 형식, 매개 변수 또는 형식 매개 변수에 함수 멤버에 적용 되는 위치 특성 또는 함수 멤버의 본문 내에서 함수 호출을 하는 경우는 `CallerMemberNameAttribute`에 해당 멤버의 이름을 나타내는 문자열 리터럴 매개 변수 기본값 대신 호출에 대 한 인수로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-358">If a function invocation from a location within the body of a function member or within an attribute applied to the function member itself or its return type, parameters or type parameters in source code omits an optional parameter with the `CallerMemberNameAttribute`, then a string literal representing the name of that member is used as an argument to the invocation instead of the default parameter value.</span></span>

<span data-ttu-id="c50c2-359">제네릭 메서드 내에서 발생 하는 호출에 대 한 메서드 이름 자체 형식 매개 변수 목록 없이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-359">For invocations that occur within generic methods, only the method name itself is used, without the type parameter list.</span></span>

<span data-ttu-id="c50c2-360">명시적 인터페이스 멤버 구현 내에서 발생 하는 호출에 대 한 메서드 이름 자체 이전 인터페이스 한정자 없이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-360">For invocations that occur within explicit interface member implementations, only the method name itself is used, without the preceding interface qualification.</span></span>

<span data-ttu-id="c50c2-361">속성 또는 이벤트 접근자 내에서 발생 하는 호출에 사용 되는 멤버 이름 속성 또는 이벤트 자체의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-361">For invocations that occur within property or event accessors, the member name used is that of the property or event itself.</span></span>

<span data-ttu-id="c50c2-362">인덱서 접근자 내에서 발생 하는 호출을 사용 하는 멤버 이름이에서 제공 하는 `IndexerNameAttribute` ([The IndexerName 특성](attributes.md#the-indexername-attribute)) 있는 경우 인덱서 멤버 또는 기본 이름을 `Item` 그렇지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="c50c2-362">For invocations that occur within indexer accessors, the member name used is that supplied by an `IndexerNameAttribute` ([The IndexerName attribute](attributes.md#the-indexername-attribute)) on the indexer member, if present, or the default name `Item` otherwise.</span></span>

<span data-ttu-id="c50c2-363">멤버의 인스턴스 생성자, 정적 생성자, 소멸자 및 연산자 선언 내에서 발생 하는 호출에 사용 된 이름은 구현에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-363">For invocations that occur within declarations of instance constructors, static constructors, destructors and operators the member name used is implementation-dependent.</span></span>

## <a name="attributes-for-interoperation"></a><span data-ttu-id="c50c2-364">상호 운용성에 대 한 특성</span><span class="sxs-lookup"><span data-stu-id="c50c2-364">Attributes for Interoperation</span></span>

<span data-ttu-id="c50c2-365">참고:이 섹션에서는 C#의 Microsoft.NET 구현에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-365">Note: This section is applicable only to the Microsoft .NET implementation of C#.</span></span>

### <a name="interoperation-with-com-and-win32-components"></a><span data-ttu-id="c50c2-366">Win32 및 COM 구성 요소와 상호 운용</span><span class="sxs-lookup"><span data-stu-id="c50c2-366">Interoperation with COM and Win32 components</span></span>

<span data-ttu-id="c50c2-367">.NET 런타임 많은 COM 및 Win32 Dll을 사용 하 여 작성 된 구성 요소와 상호 운용 하도록 C# 프로그램을 사용 하도록 설정 하는 특성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-367">The .NET run-time provides a large number of attributes that enable C# programs to interoperate with components written using COM and Win32 DLLs.</span></span> <span data-ttu-id="c50c2-368">예를 들어 합니다 `DllImport` 특성에서 사용할 수 있습니다는 `static extern` 메서드의 구현에서 Win32 DLL을 찾을 임을 나타내려면 메서드.</span><span class="sxs-lookup"><span data-stu-id="c50c2-368">For example, the `DllImport` attribute can be used on a `static extern` method to indicate that the implementation of the method is to be found in a Win32 DLL.</span></span> <span data-ttu-id="c50c2-369">이러한 특성에 포함 됩니다는 `System.Runtime.InteropServices` 네임 스페이스 및 이러한 특성에 대 한 자세한 설명서는 설명서에에서 나와 있는.NET 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-369">These attributes are found in the `System.Runtime.InteropServices` namespace, and detailed documentation for these attributes is found in the .NET runtime documentation.</span></span>

### <a name="interoperation-with-other-net-languages"></a><span data-ttu-id="c50c2-370">다른.NET 언어와 상호 운용</span><span class="sxs-lookup"><span data-stu-id="c50c2-370">Interoperation with other .NET languages</span></span>

#### <a name="the-indexername-attribute"></a><span data-ttu-id="c50c2-371">IndexerName 특성</span><span class="sxs-lookup"><span data-stu-id="c50c2-371">The IndexerName attribute</span></span>

<span data-ttu-id="c50c2-372">인덱서 인덱싱된 속성을 사용 하 여.NET에서 구현 되 고.NET 메타 데이터에서 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-372">Indexers are implemented in .NET using indexed properties, and have a name in the .NET metadata.</span></span> <span data-ttu-id="c50c2-373">없으면 `IndexerName` 인덱서를 그 이름 특성이 `Item` 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-373">If no `IndexerName` attribute is present for an indexer, then the name `Item` is used by default.</span></span> <span data-ttu-id="c50c2-374">`IndexerName` 특성을 사용 하면 개발자가이 기본값을 재정의 하 고 다른 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c50c2-374">The `IndexerName` attribute enables a developer to override this default and specify a different name.</span></span>

```csharp
namespace System.Runtime.CompilerServices.CSharp
{
    [AttributeUsage(AttributeTargets.Property)]
    public class IndexerNameAttribute: Attribute
    {
        public IndexerNameAttribute(string indexerName) {...}
        public string Value { get {...} } 
    }
}
```
