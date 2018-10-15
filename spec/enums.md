# <a name="enums"></a><span data-ttu-id="be14d-101">열거형</span><span class="sxs-lookup"><span data-stu-id="be14d-101">Enums</span></span>

<span data-ttu-id="be14d-102">***열거형*** 는 고유 값 형식 ([값 형식](types.md#value-types)) 명명 된 상수 집합을 선언 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-102">An ***enum type*** is a distinct value type ([Value types](types.md#value-types)) that declares a set of named constants.</span></span>

<span data-ttu-id="be14d-103">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="be14d-103">The example</span></span>

```csharp
enum Color
{
    Red,
    Green,
    Blue
}
```

<span data-ttu-id="be14d-104">명명 된 열거형 형식을 선언 `Color` 구성원과 `Red`를 `Green`, 및 `Blue`합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-104">declares an enum type named `Color` with members `Red`, `Green`, and `Blue`.</span></span>

## <a name="enum-declarations"></a><span data-ttu-id="be14d-105">열거형 선언</span><span class="sxs-lookup"><span data-stu-id="be14d-105">Enum declarations</span></span>

<span data-ttu-id="be14d-106">새 열거형 형식을 선언 하는 열거형 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-106">An enum declaration declares a new enum type.</span></span> <span data-ttu-id="be14d-107">열거형 선언 키워드로 시작 `enum`, 이름, 액세스 가능성, 기본 형식 및 열거형의 멤버를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-107">An enum declaration begins with the keyword `enum`, and defines the name, accessibility, underlying type, and members of the enum.</span></span>

```antlr
enum_declaration
    : attributes? enum_modifier* 'enum' identifier enum_base? enum_body ';'?
    ;

enum_base
    : ':' integral_type
    ;

enum_body
    : '{' enum_member_declarations? '}'
    | '{' enum_member_declarations ',' '}'
    ;
```

<span data-ttu-id="be14d-108">각 열거형 형식이 정수 계열 형식이 호출에 ***내부 형식*** 열거형 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-108">Each enum type has a corresponding integral type called the ***underlying type*** of the enum type.</span></span> <span data-ttu-id="be14d-109">이 기본 형식은 열거형에 정의 된 모든 열거자 값을 나타내는 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-109">This underlying type must be able to represent all the enumerator values defined in the enumeration.</span></span> <span data-ttu-id="be14d-110">열거형 선언의 내부 형식을 명시적으로 선언할 수 있습니다 `byte`, `sbyte`, `short`, `ushort`를 `int`를 `uint`를 `long` 또는 `ulong`합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-110">An enum declaration may explicitly declare an underlying type of `byte`, `sbyte`, `short`, `ushort`, `int`, `uint`, `long` or `ulong`.</span></span> <span data-ttu-id="be14d-111">`char` 기본 형식으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-111">Note that `char` cannot be used as an underlying type.</span></span> <span data-ttu-id="be14d-112">내부 형식은 내부 형식을 명시적으로 선언 하지 않는 열거형 선언 `int`합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-112">An enum declaration that does not explicitly declare an underlying type has an underlying type of `int`.</span></span>

<span data-ttu-id="be14d-113">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="be14d-113">The example</span></span>

```csharp
enum Color: long
{
    Red,
    Green,
    Blue
}
```

<span data-ttu-id="be14d-114">열거형의 내부 형식을 사용 하 여 선언 `long`합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-114">declares an enum with an underlying type of `long`.</span></span> <span data-ttu-id="be14d-115">기본 형식을 사용 하는 개발자를 선택할 수 있습니다 `long`범위에 있는 값을 사용할 수 있도록 예제 에서처럼 `long` 아니라 범위의 `int`, 또는 미래에 대해이 옵션을 유지 하기 위해.</span><span class="sxs-lookup"><span data-stu-id="be14d-115">A developer might choose to use an underlying type of `long`, as in the example, to enable the use of values that are in the range of `long` but not in the range of `int`, or to preserve this option for the future.</span></span>

## <a name="enum-modifiers"></a><span data-ttu-id="be14d-116">열거형 한정자</span><span class="sxs-lookup"><span data-stu-id="be14d-116">Enum modifiers</span></span>

<span data-ttu-id="be14d-117">*enum_declaration* 열거형 한정자 시퀀스를 선택적으로 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-117">An *enum_declaration* may optionally include a sequence of enum modifiers:</span></span>

```antlr
enum_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    ;
```

<span data-ttu-id="be14d-118">이를 여러 번 열거형 선언에서 동일한 한정자에 대 한 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-118">It is a compile-time error for the same modifier to appear multiple times in an enum declaration.</span></span>

<span data-ttu-id="be14d-119">열거형 선언 한정자 클래스 선언의 동일한 의미를 가집니다 ([한정자를 클래스](classes.md#class-modifiers)).</span><span class="sxs-lookup"><span data-stu-id="be14d-119">The modifiers of an enum declaration have the same meaning as those of a class declaration ([Class modifiers](classes.md#class-modifiers)).</span></span> <span data-ttu-id="be14d-120">단, 하는 `abstract` 및 `sealed` 한정자 열거형 선언에서 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-120">Note, however, that the `abstract` and `sealed` modifiers are not permitted in an enum declaration.</span></span> <span data-ttu-id="be14d-121">열거형 추상적일 수 없으며 파생이 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-121">Enums cannot be abstract and do not permit derivation.</span></span>

## <a name="enum-members"></a><span data-ttu-id="be14d-122">열거형 멤버</span><span class="sxs-lookup"><span data-stu-id="be14d-122">Enum members</span></span>

<span data-ttu-id="be14d-123">열거형 형식 선언의 본문 열거형 형식의 명명 된 상수는 0 개 이상의 열거형 멤버를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-123">The body of an enum type declaration defines zero or more enum members, which are the named constants of the enum type.</span></span> <span data-ttu-id="be14d-124">없는 두 열거형 멤버 이름이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-124">No two enum members can have the same name.</span></span>

```antlr
enum_member_declarations
    : enum_member_declaration (',' enum_member_declaration)*
    ;

enum_member_declaration
    : attributes? identifier ('=' constant_expression)?
    ;
```

<span data-ttu-id="be14d-125">각 열거형 멤버에는 연결 된 상수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-125">Each enum member has an associated constant value.</span></span> <span data-ttu-id="be14d-126">이 값의 형식은 포함 하는 열거형의 내부 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-126">The type of this value is the underlying type for the containing enum.</span></span> <span data-ttu-id="be14d-127">각 열거형 멤버에 대 한 상수 값을 열거형에 대 한 기본 형식의 범위에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-127">The constant value for each enum member must be in the range of the underlying type for the enum.</span></span> <span data-ttu-id="be14d-128">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="be14d-128">The example</span></span>

```csharp
enum Color: uint
{
    Red = -1,
    Green = -2,
    Blue = -3
}
```

<span data-ttu-id="be14d-129">때문에 컴파일 타임 오류가 발생 상수 값 `-1`, `-2`, 및 `-3` 기본 정수 계열 형식의 범위에 있지 않은 `uint`합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-129">results in a compile-time error because the constant values `-1`, `-2`, and `-3` are not in the range of the underlying integral type `uint`.</span></span>

<span data-ttu-id="be14d-130">여러 열거형 멤버와 연결된 된 동일한 값을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-130">Multiple enum members may share the same associated value.</span></span> <span data-ttu-id="be14d-131">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="be14d-131">The example</span></span>

```csharp
enum Color 
{
    Red,
    Green,
    Blue,

    Max = Blue
}
```

<span data-ttu-id="be14d-132">-두 열거형 멤버의 열거형을 보여 줍니다 `Blue` 고 `Max` -동일한 연결 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-132">shows an enum in which two enum members -- `Blue` and `Max` -- have the same associated value.</span></span>

<span data-ttu-id="be14d-133">열거형 멤버의 관련된 값에는 암시적 또는 명시적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-133">The associated value of an enum member is assigned either implicitly or explicitly.</span></span> <span data-ttu-id="be14d-134">열거형 멤버의 선언에는 *constant_expression* 이니셜라이저, 열거형의 내부 형식으로 암시적으로 변환 하는 상수 식의 값을 열거형 멤버의 관련된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-134">If the declaration of the enum member has a *constant_expression* initializer, the value of that constant expression, implicitly converted to the underlying type of the enum, is the associated value of the enum member.</span></span> <span data-ttu-id="be14d-135">열거형 멤버의 선언에 이니셜라이저가 없기를 다음과 같이 암시적으로 연결 된 값이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-135">If the declaration of the enum member has no initializer, its associated value is set implicitly, as follows:</span></span>

*  <span data-ttu-id="be14d-136">열거형 멤버는 열거형 형식에 선언 된 첫 번째 열거형 멤버를 해당 연결 된 값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-136">If the enum member is the first enum member declared in the enum type, its associated value is zero.</span></span>
*  <span data-ttu-id="be14d-137">이 고, 그렇지 씩 더한 이전 열거형 멤버의 관련된 값을 늘려 열거형 멤버의 관련된 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-137">Otherwise, the associated value of the enum member is obtained by increasing the associated value of the textually preceding enum member by one.</span></span> <span data-ttu-id="be14d-138">이 값은 기본 형식으로 나타낼 수 있는 값의 범위 내에 있어야 합니다. 그렇지 않으면 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-138">This increased value must be within the range of values that can be represented by the underlying type, otherwise a compile-time error occurs.</span></span>

<span data-ttu-id="be14d-139">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="be14d-139">The example</span></span>

```csharp
using System;

enum Color
{
    Red,
    Green = 10,
    Blue
}

class Test
{
    static void Main() {
        Console.WriteLine(StringFromColor(Color.Red));
        Console.WriteLine(StringFromColor(Color.Green));
        Console.WriteLine(StringFromColor(Color.Blue));
    }

    static string StringFromColor(Color c) {
        switch (c) {
            case Color.Red: 
                return String.Format("Red = {0}", (int) c);

            case Color.Green:
                return String.Format("Green = {0}", (int) c);

            case Color.Blue:
                return String.Format("Blue = {0}", (int) c);

            default:
                return "Invalid color";
        }
    }
}
```

<span data-ttu-id="be14d-140">열거형 멤버 이름 및 연결 된 값을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-140">prints out the enum member names and their associated values.</span></span> <span data-ttu-id="be14d-141">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-141">The output is:</span></span>

```
Red = 0
Green = 10
Blue = 11
```

<span data-ttu-id="be14d-142">다음과 같은 이유로:</span><span class="sxs-lookup"><span data-stu-id="be14d-142">for the following reasons:</span></span>

*  <span data-ttu-id="be14d-143">열거형 멤버 `Red` 값 0 (하므로 이니셜라이저가 없기는 첫 번째 열거형 멤버)를 자동으로 할당 됩니다</span><span class="sxs-lookup"><span data-stu-id="be14d-143">the enum member `Red` is automatically assigned the value zero (since it has no initializer and is the first enum member);</span></span>
*  <span data-ttu-id="be14d-144">열거형 멤버 `Green` 값을 명시적으로 부여 됩니다 `10`;</span><span class="sxs-lookup"><span data-stu-id="be14d-144">the enum member `Green` is explicitly given the value `10`;</span></span>
*  <span data-ttu-id="be14d-145">열거형 멤버가 `Blue` 텍스트가 앞에 오는 멤버 보다 하나 더 큰 값을 자동으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-145">and the enum member `Blue` is automatically assigned the value one greater than the member that textually precedes it.</span></span>

<span data-ttu-id="be14d-146">열거형 멤버의 관련된 값 않을 직접 또는 간접적으로 자체 연관 된 열거형 멤버의 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-146">The associated value of an enum member may not, directly or indirectly, use the value of its own associated enum member.</span></span> <span data-ttu-id="be14d-147">이러한 순환 제한과 열거형 멤버 이니셜라이저가 임의로 텍스트 위치에 관계 없이 다른 열거형 멤버 이니셜라이저를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-147">Other than this circularity restriction, enum member initializers may freely refer to other enum member initializers, regardless of their textual position.</span></span> <span data-ttu-id="be14d-148">다른 열거형 멤버 값의 열거형 멤버 이니셜라이저 내에서 항상 다른 열거형 멤버를 참조할 때 캐스트는 필요 없습니다 있도록 해당 내부 형식의 형식으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-148">Within an enum member initializer, values of other enum members are always treated as having the type of their underlying type, so that casts are not necessary when referring to other enum members.</span></span>

<span data-ttu-id="be14d-149">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="be14d-149">The example</span></span>

```csharp
enum Circular
{
    A = B,
    B
}
```

<span data-ttu-id="be14d-150">때문에 컴파일 타임 오류가 발생 선언을 `A` 고 `B` 순환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-150">results in a compile-time error because the declarations of `A` and `B` are circular.</span></span> <span data-ttu-id="be14d-151">`A` 에 따라 달라 집니다 `B` 명시적으로 및 `B` 에 따라 달라 집니다 `A` 암시적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-151">`A` depends on `B` explicitly, and `B` depends on `A` implicitly.</span></span>

<span data-ttu-id="be14d-152">열거형 멤버 명명 되 고 클래스 내의 필드와 거의 비슷한 방식으로 범위가 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-152">Enum members are named and scoped in a manner exactly analogous to fields within classes.</span></span> <span data-ttu-id="be14d-153">열거형 멤버의 범위에 포함 된 열거형 형식의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-153">The scope of an enum member is the body of its containing enum type.</span></span> <span data-ttu-id="be14d-154">해당 범위 내에서 간단한 이름으로 열거형 멤버를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-154">Within that scope, enum members can be referred to by their simple name.</span></span> <span data-ttu-id="be14d-155">다른 모든 코드에서 열거형 멤버의 이름은 해당 열거형 형식의 이름으로 한정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-155">From all other code, the name of an enum member must be qualified with the name of its enum type.</span></span> <span data-ttu-id="be14d-156">열거형 멤버는 선언 된 접근성 없는-열거형 멤버를 포함 하는 열거형 형식에 액세스할 수 있는 경우에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-156">Enum members do not have any declared accessibility -- an enum member is accessible if its containing enum type is accessible.</span></span>

## <a name="the-systemenum-type"></a><span data-ttu-id="be14d-157">System.Enum 형식</span><span class="sxs-lookup"><span data-stu-id="be14d-157">The System.Enum type</span></span>

<span data-ttu-id="be14d-158">형식 `System.Enum` 는 모든 열거형 형식 (이 distinct 및 열거형 형식의 기본 형식에서 다른)의 추상 기본 클래스에서 상속 된 멤버 및 `System.Enum` 모든 열거형 형식에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-158">The type `System.Enum` is the abstract base class of all enum types (this is distinct and different from the underlying type of the enum type), and the members inherited from `System.Enum` are available in any enum type.</span></span> <span data-ttu-id="be14d-159">Boxing 변환 ([Boxing 변환](types.md#boxing-conversions)) 모든 열거형 형식에서 존재 `System.Enum`, 및 unboxing 변환 ([Unboxing 변환](types.md#unboxing-conversions))에서 존재 `System.Enum` 모든 열거형 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-159">A boxing conversion ([Boxing conversions](types.md#boxing-conversions)) exists from any enum type to `System.Enum`, and an unboxing conversion ([Unboxing conversions](types.md#unboxing-conversions)) exists from `System.Enum` to any enum type.</span></span>

<span data-ttu-id="be14d-160">사실은 `System.Enum` 자체는 *enum_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-160">Note that `System.Enum` is not itself an *enum_type*.</span></span> <span data-ttu-id="be14d-161">아니라는 것을 *class_type* 모든에서 *enum_type*가 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-161">Rather, it is a *class_type* from which all *enum_type*s are derived.</span></span> <span data-ttu-id="be14d-162">형식 `System.Enum` 형식에서 상속 `System.ValueType` ([The System.ValueType 형식](types.md#the-systemvaluetype-type))는 형식에서 상속 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-162">The type `System.Enum` inherits from the type `System.ValueType` ([The System.ValueType type](types.md#the-systemvaluetype-type)), which, in turn, inherits from type `object`.</span></span> <span data-ttu-id="be14d-163">런타임 형식의 값에 `System.Enum` 수 `null` 또는 열거형 형식의 boxed 값에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-163">At run-time, a value of type `System.Enum` can be `null` or a reference to a boxed value of any enum type.</span></span>

## <a name="enum-values-and-operations"></a><span data-ttu-id="be14d-164">열거형 값 및 작업</span><span class="sxs-lookup"><span data-stu-id="be14d-164">Enum values and operations</span></span>

<span data-ttu-id="be14d-165">각 열거형 형식이 고유 형식을; 정의 명시적 열거형 변환은 ([명시적 열거형 변환](conversions.md#explicit-enumeration-conversions)) 열거형 형식 및 정수 계열 형식 간에 또는 두 열거형 형식 간에 변환 하는 데 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-165">Each enum type defines a distinct type; an explicit enumeration conversion ([Explicit enumeration conversions](conversions.md#explicit-enumeration-conversions)) is required to convert between an enum type and an integral type, or between two enum types.</span></span> <span data-ttu-id="be14d-166">열거형 형식에 사용할 수 있는 값의 집합은은 열거형 멤버에 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-166">The set of values that an enum type can take on is not limited by its enum members.</span></span> <span data-ttu-id="be14d-167">특히, 열거형의 기본 형식의 모든 값은 열거형 형식으로 캐스팅 될 수 이며 해당 열거형의 유효한 고유 값입니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-167">In particular, any value of the underlying type of an enum can be cast to the enum type, and is a distinct valid value of that enum type.</span></span>

<span data-ttu-id="be14d-168">열거형 멤버 형식이 포함 하는 열거형 형식 (다른 열거형 멤버 이니셜라이저 내: 참조 [열거형 멤버](enums.md#enum-members)).</span><span class="sxs-lookup"><span data-stu-id="be14d-168">Enum members have the type of their containing enum type (except within other enum member initializers: see [Enum members](enums.md#enum-members)).</span></span> <span data-ttu-id="be14d-169">열거형 형식에 선언 된 열거형 멤버의 값 `E` 연관 된 값을 사용 하 여 `v` 는 `(E)v`합니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-169">The value of an enum member declared in enum type `E` with associated value `v` is `(E)v`.</span></span>

<span data-ttu-id="be14d-170">열거형 형식의 값에서 다음 연산자를 사용할 수 있습니다: `==`, `!=`, `<`, `>`, `<=`, `>=` ([열거형 비교 연산자](expressions.md#enumeration-comparison-operators)), 이진 `+` ([더하기 연산자](expressions.md#addition-operator)), 이진 `-` ([빼기 연산자](expressions.md#subtraction-operator)), `^`를 `&`를 `|` ([논리 열거형 연산자](expressions.md#enumeration-logical-operators)), `~` ([비트 보수 연산자](expressions.md#bitwise-complement-operator)), `++` 하 고 `--` ([후 위 증가 및 감소 연산자](expressions.md#postfix-increment-and-decrement-operators) 하고[ 전위 증가 및 감소 연산자](expressions.md#prefix-increment-and-decrement-operators)).</span><span class="sxs-lookup"><span data-stu-id="be14d-170">The following operators can be used on values of enum types: `==`, `!=`, `<`, `>`, `<=`, `>=` ([Enumeration comparison operators](expressions.md#enumeration-comparison-operators)), binary `+` ([Addition operator](expressions.md#addition-operator)), binary `-` ([Subtraction operator](expressions.md#subtraction-operator)), `^`, `&`, `|` ([Enumeration logical operators](expressions.md#enumeration-logical-operators)), `~` ([Bitwise complement operator](expressions.md#bitwise-complement-operator)), `++` and `--` ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators) and [Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)).</span></span>

<span data-ttu-id="be14d-171">모든 열거형 형식 클래스에서 자동으로 파생 `System.Enum` (,에서 파생 `System.ValueType` 및 `object`).</span><span class="sxs-lookup"><span data-stu-id="be14d-171">Every enum type automatically derives from the class `System.Enum` (which, in turn, derives from `System.ValueType` and `object`).</span></span> <span data-ttu-id="be14d-172">따라서 열거형 형식의 값에이 클래스의 상속 된 메서드 및 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be14d-172">Thus, inherited methods and properties of this class can be used on values of an enum type.</span></span>
