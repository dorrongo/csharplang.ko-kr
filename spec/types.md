# <a name="types"></a><span data-ttu-id="1e968-101">유형</span><span class="sxs-lookup"><span data-stu-id="1e968-101">Types</span></span>

<span data-ttu-id="1e968-102">C# 언어 형식의 두 가지 주요 범주로 구분 됩니다. ***값 형식*** 및 ***형식을 참조***합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-102">The types of the C# language are divided into two main categories: ***value types*** and ***reference types***.</span></span> <span data-ttu-id="1e968-103">값 형식과 참조 형식 둘 다를 수 있습니다 ***제네릭 형식***에 하나를 수행 하는 ***매개 변수 입력***합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-103">Both value types and reference types may be ***generic types***, which take one or more ***type parameters***.</span></span> <span data-ttu-id="1e968-104">형식 매개 변수는 모두 값 형식을 지정 하 고 형식을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-104">Type parameters can designate both value types and reference types.</span></span>

```antlr
type
    : value_type
    | reference_type
    | type_parameter
    | type_unsafe
    ;
```

<span data-ttu-id="1e968-105">포인터 형식의 마지막 범주는 안전 하지 않은 코드 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-105">The final category of types, pointers, is available only in unsafe code.</span></span> <span data-ttu-id="1e968-106">설명에 대 한 자세한 [포인터 형식](unsafe-code.md#pointer-types)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-106">This is discussed further in [Pointer types](unsafe-code.md#pointer-types).</span></span>

<span data-ttu-id="1e968-107">값 형식이 다른 참조 형식에서 값 형식의 변수에 직접 해당 데이터를 포함 하 변수 참조의 저장소 형식을 반면 ***참조가*** 해당 데이터에 라고도 함 ***개체***.</span><span class="sxs-lookup"><span data-stu-id="1e968-107">Value types differ from reference types in that variables of the value types directly contain their data, whereas variables of the reference types store ***references*** to their data, the latter being known as ***objects***.</span></span> <span data-ttu-id="1e968-108">참조 형식에 두 가지 변수가 같은 개체를 참조 하 고 수 있으므로 작업이 다른 변수에서 참조 하는 개체에 적용할 한 변수에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-108">With reference types, it is possible for two variables to reference the same object, and thus possible for operations on one variable to affect the object referenced by the other variable.</span></span> <span data-ttu-id="1e968-109">값 형식에서는 각 변수에 데이터의 자체 사본이 이므로 작업이 다른 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-109">With value types, the variables each have their own copy of the data, and it is not possible for operations on one to affect the other.</span></span>

<span data-ttu-id="1e968-110">C#의 형식 시스템은 모든 형식의 값 개체로 처리할 수 있도록 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-110">C#'s type system is unified such that a value of any type can be treated as an object.</span></span> <span data-ttu-id="1e968-111">C#의 모든 형식은 `object` 클래스 형식에서 직접 또는 간접적으로 파생되고 `object`는 모든 형식의 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-111">Every type in C# directly or indirectly derives from the `object` class type, and `object` is the ultimate base class of all types.</span></span> <span data-ttu-id="1e968-112">참조 형식의 값은 `object`로 인식함으로써 간단히 개체로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-112">Values of reference types are treated as objects simply by viewing the values as type `object`.</span></span> <span data-ttu-id="1e968-113">값 형식의 boxing 및 unboxing 연산을 수행 하 여 개체로 처리 됩니다 ([Boxing 및 unboxing](types.md#boxing-and-unboxing)).</span><span class="sxs-lookup"><span data-stu-id="1e968-113">Values of value types are treated as objects by performing boxing and unboxing operations ([Boxing and unboxing](types.md#boxing-and-unboxing)).</span></span>

## <a name="value-types"></a><span data-ttu-id="1e968-114">값 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-114">Value types</span></span>

<span data-ttu-id="1e968-115">값 형식은 구조체 형식 또는 열거형 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-115">A value type is either a struct type or an enumeration type.</span></span> <span data-ttu-id="1e968-116">C# 이라는 미리 정의 된 구조체 형식의 집합을 제공 합니다 ***단순 형식***합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-116">C# provides a set of predefined struct types called the ***simple types***.</span></span> <span data-ttu-id="1e968-117">단순 형식 예약 된 키워드를 통해 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-117">The simple types are identified through reserved words.</span></span>

```antlr
value_type
    : struct_type
    | enum_type
    ;

struct_type
    : type_name
    | simple_type
    | nullable_type
    ;

simple_type
    : numeric_type
    | 'bool'
    ;

numeric_type
    : integral_type
    | floating_point_type
    | 'decimal'
    ;

integral_type
    : 'sbyte'
    | 'byte'
    | 'short'
    | 'ushort'
    | 'int'
    | 'uint'
    | 'long'
    | 'ulong'
    | 'char'
    ;

floating_point_type
    : 'float'
    | 'double'
    ;

nullable_type
    : non_nullable_value_type '?'
    ;

non_nullable_value_type
    : type
    ;

enum_type
    : type_name
    ;
```

<span data-ttu-id="1e968-118">참조 형식의 변수와 달리 값 형식 변수에 값을 포함할 수 `null` 값 형식이 nullable 형식인 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-118">Unlike a variable of a reference type, a variable of a value type can contain the value `null` only if the value type is a nullable type.</span></span>  <span data-ttu-id="1e968-119">모든 null이 아닌 값 형식에 대 한는 값을 더한 값의 동일한 집합을 나타내는 해당 nullable 값 형식 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-119">For every non-nullable value type there is a corresponding nullable value type denoting the same set of values plus the value `null`.</span></span>

<span data-ttu-id="1e968-120">값 형식의 변수에 할당 되 고 할당 된 값의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-120">Assignment to a variable of a value type creates a copy of the value being assigned.</span></span> <span data-ttu-id="1e968-121">이 참조 하지만 참조에 의해 식별 된 개체를 복사 하는 참조 형식의 변수에 할당에서 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-121">This differs from assignment to a variable of a reference type, which copies the reference but not the object identified by the reference.</span></span>

### <a name="the-systemvaluetype-type"></a><span data-ttu-id="1e968-122">System.ValueType 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-122">The System.ValueType type</span></span>

<span data-ttu-id="1e968-123">클래스에서 암시적으로 상속 된 모든 값 형식 `System.ValueType`는 클래스에서 상속 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-123">All value types implicitly inherit from the class `System.ValueType`, which, in turn, inherits from class `object`.</span></span> <span data-ttu-id="1e968-124">값 형식에서 파생 되는 모든 형식에 대 한 불가능 하 고 값 형식은 암시적으로 봉인 되므로 됩니다 ([클래스를 봉인](classes.md#sealed-classes)).</span><span class="sxs-lookup"><span data-stu-id="1e968-124">It is not possible for any type to derive from a value type, and value types are thus implicitly sealed ([Sealed classes](classes.md#sealed-classes)).</span></span>

<span data-ttu-id="1e968-125">사실은 `System.ValueType` 자체는 *value_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-125">Note that `System.ValueType` is not itself a *value_type*.</span></span> <span data-ttu-id="1e968-126">아니라는 것을 *class_type* 모든에서 *value_type*가 자동으로 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-126">Rather, it is a *class_type* from which all *value_type*s are automatically derived.</span></span>

### <a name="default-constructors"></a><span data-ttu-id="1e968-127">기본 생성자</span><span class="sxs-lookup"><span data-stu-id="1e968-127">Default constructors</span></span>

<span data-ttu-id="1e968-128">모든 값 형식 이라는 매개 변수가 없는 public 인스턴스 생성자를 암시적으로 선언 된 ***기본 생성자***합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-128">All value types implicitly declare a public parameterless instance constructor called the ***default constructor***.</span></span> <span data-ttu-id="1e968-129">기본 생성자로 알려진 0으로 초기화 인스턴스를 반환 합니다 ***기본값*** 값 형식에 대 한:</span><span class="sxs-lookup"><span data-stu-id="1e968-129">The default constructor returns a zero-initialized instance known as the ***default value*** for the value type:</span></span>

*  <span data-ttu-id="1e968-130">모든 *simple_type*s, 기본값은 모두 0 비트 패턴에 의해 생성 된 값:</span><span class="sxs-lookup"><span data-stu-id="1e968-130">For all *simple_type*s, the default value is the value produced by a bit pattern of all zeros:</span></span>
    * <span data-ttu-id="1e968-131">에 대 한 `sbyte`, `byte`, `short`, `ushort`를 `int`를 `uint`를 `long`, 및 `ulong`, 기본값은 `0`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-131">For `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, and `ulong`, the default value is `0`.</span></span>
    * <span data-ttu-id="1e968-132">에 대 한 `char`, 기본값은 `'\x0000'`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-132">For `char`, the default value is `'\x0000'`.</span></span>
    * <span data-ttu-id="1e968-133">에 대 한 `float`, 기본값은 `0.0f`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-133">For `float`, the default value is `0.0f`.</span></span>
    * <span data-ttu-id="1e968-134">에 대 한 `double`, 기본값은 `0.0d`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-134">For `double`, the default value is `0.0d`.</span></span>
    * <span data-ttu-id="1e968-135">에 대 한 `decimal`, 기본값은 `0.0m`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-135">For `decimal`, the default value is `0.0m`.</span></span>
    * <span data-ttu-id="1e968-136">에 대 한 `bool`, 기본값은 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-136">For `bool`, the default value is `false`.</span></span>
*  <span data-ttu-id="1e968-137">에 *enum_type* `E`, 기본값은 `0`형식으로 변환 된 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-137">For an *enum_type* `E`, the default value is `0`, converted to the type `E`.</span></span>
*  <span data-ttu-id="1e968-138">에 대 한는 *struct_type*, 기본 값 형식 필드를 기본값으로 및 모든 참조를 모든 값 형식 필드를 설정 하 여 생성 한 값은 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-138">For a *struct_type*, the default value is the value produced by setting all value type fields to their default value and all reference type fields to `null`.</span></span>
*  <span data-ttu-id="1e968-139">에 대 한를 *nullable_type* 기본값은 인스턴스입니다를 `HasValue` 속성이 false 및 `Value` 속성 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-139">For a *nullable_type* the default value is an instance for which the `HasValue` property is false and the `Value` property is undefined.</span></span> <span data-ttu-id="1e968-140">기본값은 라고도 합니다 ***값을 null*** nullable 형식의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-140">The default value is also known as the ***null value*** of the nullable type.</span></span>

<span data-ttu-id="1e968-141">사용 하 여 값 형식의 기본 생성자가 호출 하는 다른 인스턴스 생성자와 같은 `new` 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-141">Like any other instance constructor, the default constructor of a value type is invoked using the `new` operator.</span></span> <span data-ttu-id="1e968-142">효율성을 위해이 요구 사항은 없습니다 생성 생성자 호출을 구현 하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-142">For efficiency reasons, this requirement is not intended to actually have the implementation generate a constructor call.</span></span> <span data-ttu-id="1e968-143">변수 아래 예에서 `i` 고 `j` 0으로 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-143">In the example below, variables `i` and `j` are both initialized to zero.</span></span>

```csharp
class A
{
    void F() {
        int i = 0;
        int j = new int();
    }
}
```

<span data-ttu-id="1e968-144">암시적으로 모든 값 형식에 매개 변수가 없는 public 인스턴스 생성자가 되므로 구조체 형식 매개 변수가 없는 생성자의 명시적 선언을 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-144">Because every value type implicitly has a public parameterless instance constructor, it is not possible for a struct type to contain an explicit declaration of a parameterless constructor.</span></span> <span data-ttu-id="1e968-145">구조체 형식 매개 변수가 있는 인스턴스 생성자를 선언할 수 있지만 ([생성자](structs.md#constructors)).</span><span class="sxs-lookup"><span data-stu-id="1e968-145">A struct type is however permitted to declare parameterized instance constructors ([Constructors](structs.md#constructors)).</span></span>

### <a name="struct-types"></a><span data-ttu-id="1e968-146">구조체 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-146">Struct types</span></span>

<span data-ttu-id="1e968-147">구조체 형식은 상수, 필드, 메서드, 속성, 인덱서, 연산자, 인스턴스 생성자, 정적 생성자 및 중첩 된 형식을 선언할 수 있는 값 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-147">A struct type is a value type that can declare constants, fields, methods, properties, indexers, operators, instance constructors, static constructors, and nested types.</span></span> <span data-ttu-id="1e968-148">구조체 형식의 선언에 설명 되어 [구조체 선언](structs.md#struct-declarations)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-148">The declaration of struct types is described in [Struct declarations](structs.md#struct-declarations).</span></span>

### <a name="simple-types"></a><span data-ttu-id="1e968-149">단순 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-149">Simple types</span></span>

<span data-ttu-id="1e968-150">C# 이라는 미리 정의 된 구조체 형식의 집합을 제공 합니다 ***단순 형식***합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-150">C# provides a set of predefined struct types called the ***simple types***.</span></span> <span data-ttu-id="1e968-151">예약 된 단어를 통해 단순 형식 식별 하지만 이러한 예약 된 단어는 미리 정의 된 구조체 형식에 대 한 별칭을 `System` 아래 표에 설명 된 대로 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-151">The simple types are identified through reserved words, but these reserved words are simply aliases for predefined struct types in the `System` namespace, as described in the table below.</span></span>


| <span data-ttu-id="1e968-152">__예약어__</span><span class="sxs-lookup"><span data-stu-id="1e968-152">__Reserved word__</span></span> | <span data-ttu-id="1e968-153">__별칭이 지정 된 형식__</span><span class="sxs-lookup"><span data-stu-id="1e968-153">__Aliased type__</span></span> |
|-------------------|------------------|
| `sbyte`           | `System.SByte`   | 
| `byte`            | `System.Byte`    | 
| `short`           | `System.Int16`   | 
| `ushort`          | `System.UInt16`  | 
| `int`             | `System.Int32`   | 
| `uint`            | `System.UInt32`  | 
| `long`            | `System.Int64`   | 
| `ulong`           | `System.UInt64`  | 
| `char`            | `System.Char`    | 
| `float`           | `System.Single`  | 
| `double`          | `System.Double`  | 
| `bool`            | `System.Boolean` | 
| `decimal`         | `System.Decimal` | 

<span data-ttu-id="1e968-154">단순 형식의 구조체 형식 별칭을 하기 때문에 모든 단순 형식에 멤버가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-154">Because a simple type aliases a struct type, every simple type has members.</span></span> <span data-ttu-id="1e968-155">예를 들어 `int` 에 선언 된 멤버가 `System.Int32` 에서 상속 된 멤버 `System.Object`, 및 다음 문이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-155">For example, `int` has the members declared in `System.Int32` and the members inherited from `System.Object`, and the following statements are permitted:</span></span>

```csharp
int i = int.MaxValue;           // System.Int32.MaxValue constant
string s = i.ToString();        // System.Int32.ToString() instance method
string t = 123.ToString();      // System.Int32.ToString() instance method
```

<span data-ttu-id="1e968-156">단순 형식 특정 추가 작업을 허용 하는 다른 구조체 형식에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-156">The simple types differ from other struct types in that they permit certain additional operations:</span></span>

*  <span data-ttu-id="1e968-157">작성 하 여 만들려는 값을 허용 하는 대부분의 간단한 형식 *리터럴* ([리터럴](lexical-structure.md#literals)).</span><span class="sxs-lookup"><span data-stu-id="1e968-157">Most simple types permit values to be created by writing *literals* ([Literals](lexical-structure.md#literals)).</span></span> <span data-ttu-id="1e968-158">예를 들어 `123` 는 형식 리터럴 `int` 하 고 `'a'` 형식의 리터럴입니다 `char`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-158">For example, `123` is a literal of type `int` and `'a'` is a literal of type `char`.</span></span> <span data-ttu-id="1e968-159">C# 구조체 형식의 리터럴에 대 한 규정이 없습니다 일반적으로 만들고 궁극적으로 다른 구조체 형식의 기본이 아닌 값은 해당 구조체 형식의 인스턴스 생성자를 통해 항상 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-159">C# makes no provision for literals of struct types in general, and non-default values of other struct types are ultimately always created through instance constructors of those struct types.</span></span>
*  <span data-ttu-id="1e968-160">식의 피연산자가 모두 단순 형식 상수인 경우 컴파일러가 컴파일 시간 식 평가 하려면 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-160">When the operands of an expression are all simple type constants, it is possible for the compiler to evaluate the expression at compile-time.</span></span> <span data-ttu-id="1e968-161">이러한 식은 라고 한 *constant_expression* ([상수 식](expressions.md#constant-expressions)).</span><span class="sxs-lookup"><span data-stu-id="1e968-161">Such an expression is known as a *constant_expression* ([Constant expressions](expressions.md#constant-expressions)).</span></span> <span data-ttu-id="1e968-162">다른 구조체 형식으로 정의 된 연산자를 사용 하는 식은 상수 식 이어야 하는 간주 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-162">Expressions involving operators defined by other struct types are not considered to be constant expressions.</span></span>
*  <span data-ttu-id="1e968-163">통해 `const` 단순 형식의 상수를 선언할 수는 선언 ([상수](classes.md#constants)).</span><span class="sxs-lookup"><span data-stu-id="1e968-163">Through `const` declarations it is possible to declare constants of the simple types ([Constants](classes.md#constants)).</span></span> <span data-ttu-id="1e968-164">다른 구조체 형식의 상수를 가질 수 되지 않지만에서 비슷한 효과 제공 하는 `static readonly` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-164">It is not possible to have constants of other struct types, but a similar effect is provided by `static readonly` fields.</span></span>
*  <span data-ttu-id="1e968-165">사용자 정의 변환 연산자는 다른 사용자 정의 연산자의 평가에 사용 될 수 있지만 단순 형식을 포함 하는 변환 다른 구조체 형식으로 정의 하는 변환 연산자의 계산에 참여할 수 있습니다 ([평가 사용자 정의 변환은](conversions.md#evaluation-of-user-defined-conversions)).</span><span class="sxs-lookup"><span data-stu-id="1e968-165">Conversions involving simple types can participate in evaluation of conversion operators defined by other struct types, but a user-defined conversion operator can never participate in evaluation of another user-defined operator ([Evaluation of user-defined conversions](conversions.md#evaluation-of-user-defined-conversions)).</span></span>

### <a name="integral-types"></a><span data-ttu-id="1e968-166">정수 계열 형식 표</span><span class="sxs-lookup"><span data-stu-id="1e968-166">Integral types</span></span>

<span data-ttu-id="1e968-167">C# 9 개 정수 계열 형식 지원: `sbyte`, `byte`, `short`, `ushort`를 `int`를 `uint`, `long`를 `ulong`, 및 `char`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-167">C# supports nine integral types: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, and `char`.</span></span> <span data-ttu-id="1e968-168">정수 계열 형식에 다음 크기 및 값의 범위</span><span class="sxs-lookup"><span data-stu-id="1e968-168">The integral types have the following sizes and ranges of values:</span></span>

*  <span data-ttu-id="1e968-169">`sbyte` 부호 있는-128과 127 사이의 값을 가진 8 비트 정수 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-169">The `sbyte` type represents signed 8-bit integers with values between -128 and 127.</span></span>
*  <span data-ttu-id="1e968-170">`byte` 형식은 0에서 255 사이의 값을 가진 부호 없는 8 비트 정수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-170">The `byte` type represents unsigned 8-bit integers with values between 0 and 255.</span></span>
*  <span data-ttu-id="1e968-171">`short` 부호 있는-32768과 32767 사이의 값을 가진 16 비트 정수 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-171">The `short` type represents signed 16-bit integers with values between -32768 and 32767.</span></span>
*  <span data-ttu-id="1e968-172">`ushort` 형식은 0에서 65535 사이의 값을 가진 부호 없는 16 비트 정수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-172">The `ushort` type represents unsigned 16-bit integers with values between 0 and 65535.</span></span>
*  <span data-ttu-id="1e968-173">`int` 부호 있는-2147483648에서 2147483647 사이의 값을 사용 하 여 32 비트 정수 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-173">The `int` type represents signed 32-bit integers with values between -2147483648 and 2147483647.</span></span>
*  <span data-ttu-id="1e968-174">`uint` 형식은 0에서 4294967295 사이의 값을 가진 부호 없는 32 비트 정수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-174">The `uint` type represents unsigned 32-bit integers with values between 0 and 4294967295.</span></span>
*  <span data-ttu-id="1e968-175">`long` 부호 있는-9223372036854775808과 9223372036854775807 사이의 값을 가진 64 비트 정수 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-175">The `long` type represents signed 64-bit integers with values between -9223372036854775808 and 9223372036854775807.</span></span>
*  <span data-ttu-id="1e968-176">`ulong` 형식은 0과 18446744073709551615 사이의 값을 가진 부호 없는 64 비트 정수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-176">The `ulong` type represents unsigned 64-bit integers with values between 0 and 18446744073709551615.</span></span>
*  <span data-ttu-id="1e968-177">`char` 형식은 0에서 65535 사이의 값을 가진 부호 없는 16 비트 정수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-177">The `char` type represents unsigned 16-bit integers with values between 0 and 65535.</span></span> <span data-ttu-id="1e968-178">가능한 값 집합을 `char` 형식은 유니코드 문자 집합에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-178">The set of possible values for the `char` type corresponds to the Unicode character set.</span></span> <span data-ttu-id="1e968-179">하지만 `char` 동일한 표현 `ushort`를 다른 형식에서 허용 하는 모든 작업은 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-179">Although `char` has the same representation as `ushort`, not all operations permitted on one type are permitted on the other.</span></span>

<span data-ttu-id="1e968-180">정수 계열 형식의 단항 및 이항 연산자는 항상 부호 있는 32 비트 전체 자릿수, 부호 없는 32 비트 전체 자릿수, 부호 있는 64 비트 정밀도 또는 부호 없는 64 비트 정밀도 사용 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-180">The integral-type unary and binary operators always operate with signed 32-bit precision, unsigned 32-bit precision, signed 64-bit precision, or unsigned 64-bit precision:</span></span>

*  <span data-ttu-id="1e968-181">단항 `+` 하 고 `~` 연산자는 피연산자 형식으로 변환 됩니다 `T`여기서 `T` 중 첫 번째 `int`, `uint`, `long`, 및 `ulong` 모두 완벽 하 게 나타낼 수 있는 피연산자의 가능한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-181">For the unary `+` and `~` operators, the operand is converted to type `T`, where `T` is the first of `int`, `uint`, `long`, and `ulong` that can fully represent all possible values of the operand.</span></span> <span data-ttu-id="1e968-182">작업 형식의 전체 자릿수를 사용 하 여 수행 됩니다 `T`, 고 결과의 형식은 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-182">The operation is then performed using the precision of type `T`, and the type of the result is `T`.</span></span>
*  <span data-ttu-id="1e968-183">단항 `-` 연산자가 피연산자 형식으로 변환 됩니다 `T`여기서 `T` 의 첫 번째 `int` 고 `long` 피연산자의 가능한 모든 값을 완벽 하 게 나타낼 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-183">For the unary `-` operator, the operand is converted to type `T`, where `T` is the first of `int` and `long` that can fully represent all possible values of the operand.</span></span> <span data-ttu-id="1e968-184">작업 형식의 전체 자릿수를 사용 하 여 수행 됩니다 `T`, 고 결과의 형식은 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-184">The operation is then performed using the precision of type `T`, and the type of the result is `T`.</span></span> <span data-ttu-id="1e968-185">단항 `-` 형식의 피연산자에 연산자를 적용할 수 없습니다 `ulong`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-185">The unary `-` operator cannot be applied to operands of type `ulong`.</span></span>
*  <span data-ttu-id="1e968-186">이진 파일에 대 한 `+`, `-`, `*`, `/`, `%`를 `&`, `^`를 `|`, `==`를 `!=`, `>`, `<`, `>=`, 및 `<=` 연산자는 피연산자 형식으로 변환 됩니다 `T`, 여기서 `T` 첫 번째입니다 `int`를 `uint`를 `long`, 및 `ulong` 모든 가능한 완벽 하 게 나타낼 수 있는 두 피연산자의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-186">For the binary `+`, `-`, `*`, `/`, `%`, `&`, `^`, `|`, `==`, `!=`, `>`, `<`, `>=`, and `<=` operators, the operands are converted to type `T`, where `T` is the first of `int`, `uint`, `long`, and `ulong` that can fully represent all possible values of both operands.</span></span> <span data-ttu-id="1e968-187">작업 형식의 전체 자릿수를 사용 하 여 수행 됩니다 `T`, 고 결과의 형식은 `T` (또는 `bool` 관계형 연산자에 대 한).</span><span class="sxs-lookup"><span data-stu-id="1e968-187">The operation is then performed using the precision of type `T`, and the type of the result is `T` (or `bool` for the relational operators).</span></span> <span data-ttu-id="1e968-188">형식으로 하나의 피연산자에 대 한 허용 되지 않습니다 `long` 형식 이어야 하 고 다른 `ulong` 이항 연산자를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-188">It is not permitted for one operand to be of type `long` and the other to be of type `ulong` with the binary operators.</span></span>
*  <span data-ttu-id="1e968-189">이진 파일에 대 한 `<<` 하 고 `>>` 연산자는 왼쪽된 피연산자 형식으로 변환 됩니다 `T`여기서 `T` 중 첫 번째 `int`, `uint`, `long`, 및 `ulong` 모두 완벽 하 게 나타낼 수 있는 피연산자의 가능한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-189">For the binary `<<` and `>>` operators, the left operand is converted to type `T`, where `T` is the first of `int`, `uint`, `long`, and `ulong` that can fully represent all possible values of the operand.</span></span> <span data-ttu-id="1e968-190">작업 형식의 전체 자릿수를 사용 하 여 수행 됩니다 `T`, 고 결과의 형식은 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-190">The operation is then performed using the precision of type `T`, and the type of the result is `T`.</span></span>

<span data-ttu-id="1e968-191">`char` 유형이 정수 계열 형식으로 분류 됩니다 있지만 두 가지 방법으로 다른 정수 계열 형식에서 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-191">The `char` type is classified as an integral type, but it differs from the other integral types in two ways:</span></span>

*  <span data-ttu-id="1e968-192">다른 형식에서 암시적 변환은 없습니다를 `char` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-192">There are no implicit conversions from other types to the `char` type.</span></span> <span data-ttu-id="1e968-193">특히도 `sbyte`, `byte`, 및 `ushort` 형식을 사용 하 여 완벽 하 게 표현할 수 있는 값의 범위를 포함 합니다 `char` 형식에서 암시적 변환을 `sbyte`, `byte`, 또는 `ushort` 를 `char` 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-193">In particular, even though the `sbyte`, `byte`, and `ushort` types have ranges of values that are fully representable using the `char` type, implicit conversions from `sbyte`, `byte`, or `ushort` to `char` do not exist.</span></span>
*  <span data-ttu-id="1e968-194">상수는 `char` 형식으로 써야 *character_literal*s 또는 *integer_literal*형식으로 캐스팅 함께에서 s `char`입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-194">Constants of the `char` type must be written as *character_literal*s or as *integer_literal*s in combination with a cast to type `char`.</span></span> <span data-ttu-id="1e968-195">예를 들어 `(char)10`은 `'\x000A'`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-195">For example, `(char)10` is the same as `'\x000A'`.</span></span>

<span data-ttu-id="1e968-196">합니다 `checked` 하 고 `unchecked` 연산자와 문을 정수 형식 산술 연산 및 변환에 오버플로 검사를 제어 하는 ([checked 및 unchecked 연산자](expressions.md#the-checked-and-unchecked-operators)).</span><span class="sxs-lookup"><span data-stu-id="1e968-196">The `checked` and `unchecked` operators and statements are used to control overflow checking for integral-type arithmetic operations and conversions ([The checked and unchecked operators](expressions.md#the-checked-and-unchecked-operators)).</span></span> <span data-ttu-id="1e968-197">에 `checked` 컨텍스트 오버플로 컴파일 타임 오류가 발생 또는 발생을 `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-197">In a `checked` context, an overflow produces a compile-time error or causes a `System.OverflowException` to be thrown.</span></span> <span data-ttu-id="1e968-198">에 `unchecked` 컨텍스트에 오버플로 무시 되 고 대상 형식에 맞지 않는 상위 비트가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-198">In an `unchecked` context, overflows are ignored and any high-order bits that do not fit in the destination type are discarded.</span></span>

### <a name="floating-point-types"></a><span data-ttu-id="1e968-199">부동 소수점 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-199">Floating point types</span></span>

<span data-ttu-id="1e968-200">C#에서는 두 개의 부동 소수점 형식: `float` 고 `double`입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-200">C# supports two floating point types: `float` and `double`.</span></span> <span data-ttu-id="1e968-201">합니다 `float` 고 `double` 형식은 32 비트 단 정밀도 및 64 비트 배정밀도 IEEE 754 되는 형식 값 집합이 제공를 사용 하 여 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-201">The `float` and `double` types are represented using the 32-bit single-precision and 64-bit double-precision IEEE 754 formats, which provide the following sets of values:</span></span>

*  <span data-ttu-id="1e968-202">양의 0 및 음의 0입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-202">Positive zero and negative zero.</span></span> <span data-ttu-id="1e968-203">대부분의 경우, 양의 0 및 음의 0은 단순 값 0, 있지만 특정 작업의 두 구분 하는 동일 하 게 작동 ([나누기 연산자](expressions.md#division-operator)).</span><span class="sxs-lookup"><span data-stu-id="1e968-203">In most situations, positive zero and negative zero behave identically as the simple value zero, but certain operations distinguish between the two ([Division operator](expressions.md#division-operator)).</span></span>
*  <span data-ttu-id="1e968-204">양의 무한대 및 음수 무한대입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-204">Positive infinity and negative infinity.</span></span> <span data-ttu-id="1e968-205">무한대는 0이 아닌 값을 0으로 나누는 것과 같은 연산에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-205">Infinities are produced by such operations as dividing a non-zero number by zero.</span></span> <span data-ttu-id="1e968-206">예를 들어 `1.0 / 0.0` 양의 무한대를 생성 및 `-1.0 / 0.0` 음의 무한대를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-206">For example, `1.0 / 0.0` yields positive infinity, and `-1.0 / 0.0` yields negative infinity.</span></span>
*  <span data-ttu-id="1e968-207">합니다 ***Not 숫자 이외의*** 값을 종종 약식된 NaN입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-207">The ***Not-a-Number*** value, often abbreviated NaN.</span></span> <span data-ttu-id="1e968-208">0으로 나누는 등의 잘못 된 부동 소수점 작업, nan이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-208">NaNs are produced by invalid floating-point operations, such as dividing zero by zero.</span></span>
*  <span data-ttu-id="1e968-209">형식의 0이 아닌 값 집합이 유한한 `s * m * 2^e`, 여기서 `s` 이 1 또는-1 및 `m` 및 `e` 특정 부동 소수점 형식에 의해 결정 됩니다:에 대 한 `float`, `0 < m < 2^24` 및 `-149 <= e <= 104`, 한 `double`하십시오 `0 < m < 2^53` 고 `1075 <= e <= 970`입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-209">The finite set of non-zero values of the form `s * m * 2^e`, where `s` is 1 or -1, and `m` and `e` are determined by the particular floating-point type: For `float`, `0 < m < 2^24` and `-149 <= e <= 104`, and for `double`, `0 < m < 2^53` and `1075 <= e <= 970`.</span></span> <span data-ttu-id="1e968-210">정규화 되지 않은 부동 소수점 숫자에는 유효한 0이 아닌 값으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-210">Denormalized floating-point numbers are considered valid non-zero values.</span></span>

<span data-ttu-id="1e968-211">합니다 `float` 형식은 약 까지의 값을 나타낼 수 있습니다 `1.5 * 10^-45` 에 `3.4 * 10^38` 7 자리의 정밀도를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-211">The `float` type can represent values ranging from approximately `1.5 * 10^-45` to `3.4 * 10^38` with a precision of 7 digits.</span></span>

<span data-ttu-id="1e968-212">합니다 `double` 형식은 약 까지의 값을 나타낼 수 있습니다 `5.0 * 10^-324` 에 `1.7 × 10^308` 15-16 자리의 정밀도를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-212">The `double` type can represent values ranging from approximately `5.0 * 10^-324` to `1.7 × 10^308` with a precision of 15-16 digits.</span></span>

<span data-ttu-id="1e968-213">이항 연산자의 피연산자 중 하나가 부동 소수점 형식의 경우 정수 계열 형식 또는 부동 소수점 형식에서 다른 피연산자에 있어야 합니다 및 작업을 다음과 같이 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-213">If one of the operands of a binary operator is of a floating-point type, then the other operand must be of an integral type or a floating-point type, and the operation is evaluated as follows:</span></span>

*  <span data-ttu-id="1e968-214">피연산자 중 하나가 정수 계열 형식의 경우 해당 피연산자는 경우 다른 피연산자의 부동 소수점 형식으로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-214">If one of the operands is of an integral type, then that operand is converted to the floating-point type of the other operand.</span></span>
*  <span data-ttu-id="1e968-215">그런 다음 형식의 경우 피연산자 중 하나가 `double`, 다른 피연산자가 변환 `double`, 이상을 사용 하 여 작업이 수행 됩니다 `double` 범위 및 전체 자릿수 및 결과의 형식 `double` (또는 `bool` 에 대 한 합니다 관계형 연산자)입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-215">Then, if either of the operands is of type `double`, the other operand is converted to `double`, the operation is performed using at least `double` range and precision, and the type of the result is `double` (or `bool` for the relational operators).</span></span>
*  <span data-ttu-id="1e968-216">그렇지 않은 경우 작업을 수행할 때 이상을 사용 하 `float` 는 범위와 전체 자릿수 및 결과의 형식을 `float` (또는 `bool` 관계형 연산자에 대 한).</span><span class="sxs-lookup"><span data-stu-id="1e968-216">Otherwise, the operation is performed using at least `float` range and precision, and the type of the result is `float` (or `bool` for the relational operators).</span></span>

<span data-ttu-id="1e968-217">대입 연산자를 포함 하 여 연산자의 부동 소수점 예외를 생성 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-217">The floating-point operators, including the assignment operators, never produce exceptions.</span></span> <span data-ttu-id="1e968-218">대신 예외적인 상황에 부동 소수점 작업의 생성 0, 무한대 또는 NaN, 아래 설명 된 대로:</span><span class="sxs-lookup"><span data-stu-id="1e968-218">Instead, in exceptional situations, floating-point operations produce zero, infinity, or NaN, as described below:</span></span>

*  <span data-ttu-id="1e968-219">부동 소수점 연산의 결과가 너무 작아서 대상 형식에 대 한 인 경우 작업의 결과 양의 0 또는 음의 0입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-219">If the result of a floating-point operation is too small for the destination format, the result of the operation becomes positive zero or negative zero.</span></span>
*  <span data-ttu-id="1e968-220">부동 소수점 연산의 결과가 너무 커서 대상 형식에 대 한 인 경우 양의 무한대 또는 음의 무한대 연산의 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-220">If the result of a floating-point operation is too large for the destination format, the result of the operation becomes positive infinity or negative infinity.</span></span>
*  <span data-ttu-id="1e968-221">부동 소수점 연산 올바르지 않으면 작업의 결과 NaN 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-221">If a floating-point operation is invalid, the result of the operation becomes NaN.</span></span>
*  <span data-ttu-id="1e968-222">부동 소수점 연산의 피연산자 하나 또는 둘 다 NaN 인 경우 작업의 결과 NaN 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-222">If one or both operands of a floating-point operation is NaN, the result of the operation becomes NaN.</span></span>

<span data-ttu-id="1e968-223">부동 소수점 연산 작업의 결과 형식 보다 더 높은 정밀도 사용 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-223">Floating-point operations may be performed with higher precision than the result type of the operation.</span></span> <span data-ttu-id="1e968-224">예를 들어 일부 하드웨어 아키텍처 지원는 "확장" 또는 "long double" 부동 소수점 형식 보다 전체 자릿수가 큰 범위와는 `double` 를 입력 하 고 암시적으로이 더 높은 정밀도 형식을 사용 하 여 모든 부동 소수점 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-224">For example, some hardware architectures support an "extended" or "long double" floating-point type with greater range and precision than the `double` type, and implicitly perform all floating-point operations using this higher precision type.</span></span> <span data-ttu-id="1e968-225">과도 한 성능 비용만 이러한 하드웨어 아키텍처로 설정할 수 낮은 정밀도 사용 하 여 부동 소수점 작업을 수행할 수 있으며 성능 및 전체 자릿수가 모두 상실 하는 구현에 필요한 것이 아니라 C#에서는 되도록 높은 정밀도 형식 모든 부동 소수점 연산에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-225">Only at excessive cost in performance can such hardware architectures be made to perform floating-point operations with less precision, and rather than require an implementation to forfeit both performance and precision, C# allows a higher precision type to be used for all floating-point operations.</span></span> <span data-ttu-id="1e968-226">보다 정확한 결과 제공, 이외의 경우는 거의 없습니다 측정 가능한 영향을 주지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-226">Other than delivering more precise results, this rarely has any measurable effects.</span></span> <span data-ttu-id="1e968-227">폼의 식에 있지만 `x * y / z`곱하기를 벗어나는 결과 생성 하는 위치, 합니다 `double` 범위 있지만 후속 나누기는 임시 결과를 다시는 `double` 범위에 있는 식 평가 더 높은 범위의 형식 한정 된 결과 무한를 일으킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-227">However, in expressions of the form `x * y / z`, where the multiplication produces a result that is outside the `double` range, but the subsequent division brings the temporary result back into the `double` range, the fact that the expression is evaluated in a higher range format may cause a finite result to be produced instead of an infinity.</span></span>

### <a name="the-decimal-type"></a><span data-ttu-id="1e968-228">Decimal 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-228">The decimal type</span></span>

<span data-ttu-id="1e968-229">`decimal` 형식은 재무 및 통화 계산에 적합한 128비트 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-229">The `decimal` type is a 128-bit data type suitable for financial and monetary calculations.</span></span> <span data-ttu-id="1e968-230">합니다 `decimal` 형식은 까지의 값을 나타낼 수 있습니다 `1.0 * 10^-28` 에 약 `7.9 * 10^28` 28-29 유효 자릿수를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-230">The `decimal` type can represent values ranging from `1.0 * 10^-28` to approximately `7.9 * 10^28` with 28-29 significant digits.</span></span>

<span data-ttu-id="1e968-231">형식의 값 집합이 유한한 `decimal` 는 형식입니다. `(-1)^s * c * 10^-e`여기서 부호 `s` 이 0 또는 1 인 계수 `c` 를 지정 하 여 `0 <= *c* < 2^96`, 및 규모 `e` 가 되도록 `0 <= e <= 28`합니다. `decimal` 부호 있는 0이, 무한대 또는 NaN의 형식은 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-231">The finite set of values of type `decimal` are of the form `(-1)^s * c * 10^-e`, where the sign `s` is 0 or 1, the coefficient `c` is given by `0 <= *c* < 2^96`, and the scale `e` is such that `0 <= e <= 28`.The `decimal` type does not support signed zeros, infinities, or NaN's.</span></span> <span data-ttu-id="1e968-232">`decimal` 10의 거듭제곱으로 조정 된 96 비트 정수로 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-232">A `decimal` is represented as a 96-bit integer scaled by a power of ten.</span></span> <span data-ttu-id="1e968-233">에 대 한 `decimal`절대값을 사용 하 여 s 보다 작은 `1.0m`, 28 자리로를 정확 하 게 되지만 더 이상 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-233">For `decimal`s with an absolute value less than `1.0m`, the value is exact to the 28th decimal place, but no further.</span></span> <span data-ttu-id="1e968-234">에 대 한 `decimal`절대 값 보다 크거나 같음를 사용 하 여 s `1.0m`, 28 이나 29 자리까지 정확한 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-234">For `decimal`s with an absolute value greater than or equal to `1.0m`, the value is exact to 28 or 29 digits.</span></span> <span data-ttu-id="1e968-235">Contrary 하는 `float` 및 `double` 데이터 형식, 0.1과 같은 소수 10 진수 정확 하 게 나타낼 수 있습니다는 `decimal` 표현 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-235">Contrary to the `float` and `double` data types, decimal fractional numbers such as 0.1 can be represented exactly in the `decimal` representation.</span></span> <span data-ttu-id="1e968-236">에 `float` 및 `double` 표현, 이러한 숫자는 무한 소수를 반올림 발생 가능성이 해당 표현을 만드는 오류.</span><span class="sxs-lookup"><span data-stu-id="1e968-236">In the `float` and `double` representations, such numbers are often infinite fractions, making those representations more prone to round-off errors.</span></span>

<span data-ttu-id="1e968-237">형식의 경우 이항 연산자의 피연산자 중 하나가 `decimal`, 다른 피연산자는 정수 계열 형식 또는 형식 이어야 합니다. `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-237">If one of the operands of a binary operator is of type `decimal`, then the other operand must be of an integral type or of type `decimal`.</span></span> <span data-ttu-id="1e968-238">정수 계열 형식 피연산자가 있는 경우 변환할 `decimal` 작업을 수행 하기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-238">If an integral type operand is present, it is converted to `decimal` before the operation is performed.</span></span>

<span data-ttu-id="1e968-239">형식의 값에는 작업의 결과 `decimal` (각 연산자에 대해 정의 된 대로 유지 배율) 정확한 결과 계산한 다음 표현에 맞게 반올림에서 초래 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-239">The result of an operation on values of type `decimal` is that which would result from calculating an exact result (preserving scale, as defined for each operator) and then rounding to fit the representation.</span></span> <span data-ttu-id="1e968-240">결과가 반올림 되는 표현할 수 있는 값에 가장 가까운 하 고, 결과 짝수 (이 라고 "banker rounding") 최하위 숫자 위치에 있는 값으로 표현할 수 있는 두 값이 동일 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-240">Results are rounded to the nearest representable value, and, when a result is equally close to two representable values, to the value that has an even number in the least significant digit position (this is known as "banker's rounding").</span></span> <span data-ttu-id="1e968-241">0 개 결과 항상 0의 부호와 소수 자릿수가 0에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-241">A zero result always has a sign of 0 and a scale of 0.</span></span>

<span data-ttu-id="1e968-242">10 진수 산술 작업을 작은 값 보다 작거나 생성 되는 경우 `5 * 10^-29` 절대 값으로 작업의 결과 0이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-242">If a decimal arithmetic operation produces a value less than or equal to `5 * 10^-29` in absolute value, the result of the operation becomes zero.</span></span> <span data-ttu-id="1e968-243">경우는 `decimal` 산술 연산 결과가 너무 커서에 대 한는 `decimal` 형식으로는 `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-243">If a `decimal` arithmetic operation produces a result that is too large for the `decimal` format, a `System.OverflowException` is thrown.</span></span>

<span data-ttu-id="1e968-244">`decimal` 형식에 더 높은 정밀도 부동 소수점 형식 보다 높지만 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-244">The `decimal` type has greater precision but smaller range than the floating-point types.</span></span> <span data-ttu-id="1e968-245">부동 소수점 형식 변환할 때 따라서 `decimal` 오버플로 예외 및 변환에서 생성할 수 있습니다 `decimal` 부동 소수점 형식 전체 자릿수 손실이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-245">Thus, conversions from the floating-point types to `decimal` might produce overflow exceptions, and conversions from `decimal` to the floating-point types might cause loss of precision.</span></span> <span data-ttu-id="1e968-246">이러한 이유로, 부동 소수점 형식 간에 암시적 변환이 존재 하 고 `decimal`, 이므로 명시적 캐스트 없이 혼합 부동 소수점 수 및 `decimal` 같은 식에서 피연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-246">For these reasons, no implicit conversions exist between the floating-point types and `decimal`, and without explicit casts, it is not possible to mix floating-point and `decimal` operands in the same expression.</span></span>

### <a name="the-bool-type"></a><span data-ttu-id="1e968-247">Bool 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-247">The bool type</span></span>

<span data-ttu-id="1e968-248">`bool` 형식은 부울 논리 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-248">The `bool` type represents boolean logical quantities.</span></span> <span data-ttu-id="1e968-249">가능한 값 형식의 `bool` 됩니다 `true` 및 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-249">The possible values of type `bool` are `true` and `false`.</span></span>

<span data-ttu-id="1e968-250">표준 변환이 없기 서로 `bool` 및 기타 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-250">No standard conversions exist between `bool` and other types.</span></span> <span data-ttu-id="1e968-251">특히 합니다 `bool` 형식은 정수 계열 형식에서 별도 및 `bool` 그 반대로 정수 계열 값 대신 값을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-251">In particular, the `bool` type is distinct and separate from the integral types, and a `bool` value cannot be used in place of an integral value, and vice versa.</span></span>

<span data-ttu-id="1e968-252">C 및 c + + 언어에서 0 인 정수 계열 또는 부동 소수점 값 또는 null 포인터를 변환할 수 하는 부울 값 `false`를 0이 아닌 정수 계열 또는 부동 소수점 값 또는 null이 아닌 포인터를 부울 값으로 변환할 수 및 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-252">In the C and C++ languages, a zero integral or floating-point value, or a null pointer can be converted to the boolean value `false`, and a non-zero integral or floating-point value, or a non-null pointer can be converted to the boolean value `true`.</span></span> <span data-ttu-id="1e968-253">C#에서는 명시적으로 0으로 정수 계열 또는 부동 소수점 값을 비교 하 여 또는 대 한 개체 참조를 명시적으로 비교 하 여 이러한 변환이 수행 됩니다 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-253">In C#, such conversions are accomplished by explicitly comparing an integral or floating-point value to zero, or by explicitly comparing an object reference to `null`.</span></span>

### <a name="enumeration-types"></a><span data-ttu-id="1e968-254">열거형 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-254">Enumeration types</span></span>

<span data-ttu-id="1e968-255">명명 된 상수를 사용 하 여 고유 형식인 열거형 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-255">An enumeration type is a distinct type with named constants.</span></span> <span data-ttu-id="1e968-256">모든 열거형 형식 이어야 하는 내부 형식에 `byte`, `sbyte`, `short`, `ushort`를 `int`를 `uint`를 `long` 또는 `ulong`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-256">Every enumeration type has an underlying type, which must be `byte`, `sbyte`, `short`, `ushort`, `int`, `uint`, `long` or `ulong`.</span></span> <span data-ttu-id="1e968-257">열거형 형식의 값 집합이 기본 형식의 값 집합과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-257">The set of values of the enumeration type is the same as the set of values of the underlying type.</span></span> <span data-ttu-id="1e968-258">열거형 형식의 값을 명명 된 상수 값으로 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-258">Values of the enumeration type are not restricted to the values of the named constants.</span></span> <span data-ttu-id="1e968-259">열거형 형식 열거형 선언을 통해 정의 됩니다 ([열거형 선언은](enums.md#enum-declarations)).</span><span class="sxs-lookup"><span data-stu-id="1e968-259">Enumeration types are defined through enumeration declarations ([Enum declarations](enums.md#enum-declarations)).</span></span>

### <a name="nullable-types"></a><span data-ttu-id="1e968-260">Nullable 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-260">Nullable types</span></span>

<span data-ttu-id="1e968-261">Nullable 형식은 모든 값을 나타낼 수 해당 ***내부 형식*** 와 null 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-261">A nullable type can represent all values of its ***underlying type*** plus an additional null value.</span></span> <span data-ttu-id="1e968-262">Nullable 형식에 씌 `T?`여기서 `T` 기본 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-262">A nullable type is written `T?`, where `T` is the underlying type.</span></span> <span data-ttu-id="1e968-263">이 구문은 축약형 `System.Nullable<T>`, 두 개의 폼을 서로 교환해 서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-263">This syntax is shorthand for `System.Nullable<T>`, and the two forms can be used interchangeably.</span></span>

<span data-ttu-id="1e968-264">A ***nullable이 아닌 값 형식*** 는 반대로 이외의 모든 값 형식 `System.Nullable<T>` 와 해당 약어 `T?` (에 대 한 `T`), 더하기 (즉, 모두 null이 아닌 값 형식으로 제한 되는 모든 형식 매개 변수 입력 매개 변수는 `struct` 제약 조건).</span><span class="sxs-lookup"><span data-stu-id="1e968-264">A ***non-nullable value type*** conversely is any value type other than `System.Nullable<T>` and its shorthand `T?` (for any `T`), plus any type parameter that is constrained to be a non-nullable value type (that is, any type parameter with a `struct` constraint).</span></span> <span data-ttu-id="1e968-265">합니다 `System.Nullable<T>` 형식 지정에 대 한 값 형식 제약 조건 `T` ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)), 즉 nullable 형식의 기본 형식은 nullable이 아닌 값 형식일이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-265">The `System.Nullable<T>` type specifies the value type constraint for `T` ([Type parameter constraints](classes.md#type-parameter-constraints)), which means that the underlying type of a nullable type can be any non-nullable value type.</span></span> <span data-ttu-id="1e968-266">기본 형식의 nullable 형식이 nullable 형식 또는 참조 형식 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-266">The underlying type of a nullable type cannot be a nullable type or a reference type.</span></span> <span data-ttu-id="1e968-267">예를 들어 `int??` 고 `string?` 종류가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-267">For example, `int??` and `string?` are invalid types.</span></span>

<span data-ttu-id="1e968-268">Nullable 형식 인스턴스의 `T?` 에 두 개의 공용 읽기 전용 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-268">An instance of a nullable type `T?` has two public read-only properties:</span></span>

*  <span data-ttu-id="1e968-269">`HasValue` 형식의 속성 `bool`</span><span class="sxs-lookup"><span data-stu-id="1e968-269">A `HasValue` property of type `bool`</span></span>
*  <span data-ttu-id="1e968-270">`Value` 형식의 속성 `T`</span><span class="sxs-lookup"><span data-stu-id="1e968-270">A `Value` property of type `T`</span></span>

<span data-ttu-id="1e968-271">인스턴스 `HasValue` 는 null이 아닌은 true입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-271">An instance for which `HasValue` is true is said to be non-null.</span></span> <span data-ttu-id="1e968-272">Null이 아닌 인스턴스를 사용 하는 알려진된 값을 포함 하 고 `Value` 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-272">A non-null instance contains a known value and `Value` returns that value.</span></span>

<span data-ttu-id="1e968-273">인스턴스입니다 `HasValue` 는 null 일 수 false 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-273">An instance for which `HasValue` is false is said to be null.</span></span> <span data-ttu-id="1e968-274">Null 인스턴스는 정의 되지 않은 값을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-274">A null instance has an undefined value.</span></span> <span data-ttu-id="1e968-275">읽는 동안 합니다 `Value` 의 null 인스턴스를 사용 하면를 `System.InvalidOperationException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-275">Attempting to read the `Value` of a null instance causes a `System.InvalidOperationException` to be thrown.</span></span> <span data-ttu-id="1e968-276">액세스 하는 과정을 `Value` nullable 인스턴스의 속성 이라고 ***래핑 해제***합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-276">The process of accessing the `Value` property of a nullable instance is referred to as ***unwrapping***.</span></span>

<span data-ttu-id="1e968-277">기본 생성자를 모든 nullable 형식 외에도 `T?` 형식의 단일 인수를 받아들이는 public 생성자가 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-277">In addition to the default constructor, every nullable type `T?` has a public constructor that takes a single argument of type `T`.</span></span> <span data-ttu-id="1e968-278">값이 지정 `x` 형식의 `T`, 폼의 생성자 호출</span><span class="sxs-lookup"><span data-stu-id="1e968-278">Given a value `x` of type `T`, a constructor invocation of the form</span></span>

```csharp
new T?(x)
```
<span data-ttu-id="1e968-279">null이 아닌 인스턴스를 만듭니다 `T?` 는 합니다 `Value` 속성은 `x`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-279">creates a non-null instance of `T?` for which the `Value` property is `x`.</span></span> <span data-ttu-id="1e968-280">지정된 된 값 이라고에 대 한 nullable 형식의 null이 아닌 인스턴스를 만드는 과정 ***래핑***합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-280">The process of creating a non-null instance of a nullable type for a given value is referred to as ***wrapping***.</span></span>

<span data-ttu-id="1e968-281">암시적 변환에서 사용할 수는 `null` 리터럴을 `T?` ([리터럴 변환 Null](conversions.md#null-literal-conversions))에서 `T` 하 `T?` ([암시적 nullable 변환](conversions.md#implicit-nullable-conversions)).</span><span class="sxs-lookup"><span data-stu-id="1e968-281">Implicit conversions are available from the `null` literal to `T?` ([Null literal conversions](conversions.md#null-literal-conversions)) and from `T` to `T?` ([Implicit nullable conversions](conversions.md#implicit-nullable-conversions)).</span></span>

## <a name="reference-types"></a><span data-ttu-id="1e968-282">참조 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-282">Reference types</span></span>

<span data-ttu-id="1e968-283">참조 형식은 클래스 형식, 인터페이스 형식, 배열 또는 대리자 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-283">A reference type is a class type, an interface type, an array type, or a delegate type.</span></span>

```antlr
reference_type
    : class_type
    | interface_type
    | array_type
    | delegate_type
    ;

class_type
    : type_name
    | 'object'
    | 'dynamic'
    | 'string'
    ;

interface_type
    : type_name
    ;

array_type
    : non_array_type rank_specifier+
    ;

non_array_type
    : type
    ;

rank_specifier
    : '[' dim_separator* ']'
    ;

dim_separator
    : ','
    ;

delegate_type
    : type_name
    ;
```

<span data-ttu-id="1e968-284">참조 형식 값에 대 한 참조 되는 ***인스턴스*** 라고 형식의 ***개체***합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-284">A reference type value is a reference to an ***instance*** of the type, the latter known as an ***object***.</span></span> <span data-ttu-id="1e968-285">특수 값 `null` 모든 참조 형식와 호환 되 고 인스턴스가 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-285">The special value `null` is compatible with all reference types and indicates the absence of an instance.</span></span>

### <a name="class-types"></a><span data-ttu-id="1e968-286">클래스 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-286">Class types</span></span>

<span data-ttu-id="1e968-287">클래스 형식의 데이터 멤버 (상수 및 필드) 함수 멤버 (메서드, 속성, 이벤트, 인덱서, 연산자, 인스턴스 생성자, 소멸자 및 정적 생성자) 및 중첩 된 형식을 포함 하는 데이터 구조를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-287">A class type defines a data structure that contains data members (constants and fields), function members (methods, properties, events, indexers, operators, instance constructors, destructors and static constructors), and nested types.</span></span> <span data-ttu-id="1e968-288">클래스 형식은 상속을 파생된 클래스 확장 하 고 기본 클래스를 특수화할 수 가능해 집니다 메커니즘을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-288">Class types support inheritance, a mechanism whereby derived classes can extend and specialize base classes.</span></span> <span data-ttu-id="1e968-289">클래스 형식의 인스턴스를 사용 하 여 만들어집니다 *object_creation_expression*s ([개체 만들기 식](expressions.md#object-creation-expressions)).</span><span class="sxs-lookup"><span data-stu-id="1e968-289">Instances of class types are created using *object_creation_expression*s ([Object creation expressions](expressions.md#object-creation-expressions)).</span></span>

<span data-ttu-id="1e968-290">클래스 형식에 설명 되어 있습니다 [클래스](classes.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-290">Class types are described in [Classes](classes.md).</span></span>

<span data-ttu-id="1e968-291">아래 표에 설명 된 대로 C# 언어에서 특별 한 의미를 갖는 하는 특정 미리 정의 된 클래스 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-291">Certain predefined class types have special meaning in the C# language, as described in the table below.</span></span>


| <span data-ttu-id="1e968-292">__클래스 형식__</span><span class="sxs-lookup"><span data-stu-id="1e968-292">__Class type__</span></span>     | <span data-ttu-id="1e968-293">__설명__</span><span class="sxs-lookup"><span data-stu-id="1e968-293">__Description__</span></span>                                         |
|--------------------|---------------------------------------------------------|
| `System.Object`    | <span data-ttu-id="1e968-294">다른 모든 종류의 궁극적인 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-294">The ultimate base class of all other types.</span></span> <span data-ttu-id="1e968-295">참조 [개체 유형을](types.md#the-object-type)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-295">See [The object type](types.md#the-object-type).</span></span> | 
| `System.String`    | <span data-ttu-id="1e968-296">C# 언어의 문자열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-296">The string type of the C# language.</span></span> <span data-ttu-id="1e968-297">참조 [문자열 형식](types.md#the-string-type)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-297">See [The string type](types.md#the-string-type).</span></span>         |
| `System.ValueType` | <span data-ttu-id="1e968-298">모든 값 형식의 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-298">The base class of all value types.</span></span> <span data-ttu-id="1e968-299">참조 [The System.ValueType 형식](types.md#the-systemvaluetype-type)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-299">See [The System.ValueType type](types.md#the-systemvaluetype-type).</span></span>          |
| `System.Enum`      | <span data-ttu-id="1e968-300">모든 열거형 형식의 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-300">The base class of all enum types.</span></span> <span data-ttu-id="1e968-301">참조 [열거형](enums.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-301">See [Enums](enums.md).</span></span>              |
| `System.Array`     | <span data-ttu-id="1e968-302">모든 배열 형식의 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-302">The base class of all array types.</span></span> <span data-ttu-id="1e968-303">[배열](arrays.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e968-303">See [Arrays](arrays.md).</span></span>             |
| `System.Delegate`  | <span data-ttu-id="1e968-304">모든 대리자 형식의 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-304">The base class of all delegate types.</span></span> <span data-ttu-id="1e968-305">참조 [대리자](delegates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-305">See [Delegates](delegates.md).</span></span>          |
| `System.Exception` | <span data-ttu-id="1e968-306">모든 예외 형식의 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-306">The base class of all exception types.</span></span> <span data-ttu-id="1e968-307">참조 [예외](exceptions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-307">See [Exceptions](exceptions.md).</span></span>         |

### <a name="the-object-type"></a><span data-ttu-id="1e968-308">개체 유형</span><span class="sxs-lookup"><span data-stu-id="1e968-308">The object type</span></span>

<span data-ttu-id="1e968-309">`object` 클래스 유형은 다른 모든 종류의 궁극적인 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-309">The `object` class type is the ultimate base class of all other types.</span></span> <span data-ttu-id="1e968-310">C#의 모든 형식은 직접 또는 간접적으로에서 파생 되는 `object` 클래스 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-310">Every type in C# directly or indirectly derives from the `object` class type.</span></span>

<span data-ttu-id="1e968-311">키워드 `object` 은 미리 정의 된 클래스에 대 한 별칭 `System.Object`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-311">The keyword `object` is simply an alias for the predefined class `System.Object`.</span></span>

### <a name="the-dynamic-type"></a><span data-ttu-id="1e968-312">동적 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-312">The dynamic type</span></span>

<span data-ttu-id="1e968-313">합니다 `dynamic` 형식, 예: `object`, 모든 개체를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-313">The `dynamic` type, like `object`, can reference any object.</span></span> <span data-ttu-id="1e968-314">연산자가 식 형식에 적용 되는 경우 `dynamic`, 해결 프로그램이 실행 될 때까지 지연 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-314">When operators are applied to expressions of type `dynamic`, their resolution is deferred until the program is run.</span></span> <span data-ttu-id="1e968-315">따라서 참조 된 개체에 적용할 합법적으로 연산자를 사용할 수 없습니다, 하는 경우 오류가 없는 컴파일하는 동안 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-315">Thus, if the operator cannot legally be applied to the referenced object, no error is given during compilation.</span></span> <span data-ttu-id="1e968-316">대신 확인 연산자의 런타임 시 실패 한 경우 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-316">Instead an exception will be thrown when resolution of the operator fails at run-time.</span></span>

<span data-ttu-id="1e968-317">용도에 자세히 설명 된 동적 바인딩을 허용 하는 것 [동적 바인딩](expressions.md#dynamic-binding)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-317">Its purpose is to allow dynamic binding, which is described in detail in [Dynamic binding](expressions.md#dynamic-binding).</span></span>

<span data-ttu-id="1e968-318">`dynamic` 동일한 것으로 간주 `object` 다음 측면에서 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-318">`dynamic` is considered identical to `object` except in the following respects:</span></span>

*  <span data-ttu-id="1e968-319">식의 형식 연산은 `dynamic` 동적으로 바인딩할 수 있습니다 ([동적 바인딩](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="1e968-319">Operations on expressions of type `dynamic` can be dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span>
*  <span data-ttu-id="1e968-320">형식 유추 ([형식 유추](expressions.md#type-inference))를 선호 `dynamic` 를 통해 `object` 둘 다 후보입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-320">Type inference ([Type inference](expressions.md#type-inference)) will prefer `dynamic` over `object` if both are candidates.</span></span>

<span data-ttu-id="1e968-321">이 동등 인해 다음이 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-321">Because of this equivalence, the following holds:</span></span>

*  <span data-ttu-id="1e968-322">사이 변환이 암시적 id `object` 하 고 `dynamic`, 및 동일 하 게 교체 하는 경우 생성 된 형식 간의 `dynamic` 사용 하 여 `object`</span><span class="sxs-lookup"><span data-stu-id="1e968-322">There is an implicit identity conversion between `object` and `dynamic`, and between constructed types that are the same when replacing `dynamic` with `object`</span></span>
*  <span data-ttu-id="1e968-323">사이에 암시적 및 명시적 변환이 `object` 에서 적용 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-323">Implicit and explicit conversions to and from `object` also apply to and from `dynamic`.</span></span>
*  <span data-ttu-id="1e968-324">동일 하 게 교체 하는 경우 메서드 서명에 `dynamic` 사용 하 여 `object` 서명이 같은 것으로 간주 됩니다</span><span class="sxs-lookup"><span data-stu-id="1e968-324">Method signatures that are the same when replacing `dynamic` with `object` are considered the same signature</span></span>
*  <span data-ttu-id="1e968-325">형식 `dynamic` 구분 되지 않습니다 `object` 런타임 시.</span><span class="sxs-lookup"><span data-stu-id="1e968-325">The type `dynamic` is indistinguishable from `object` at run-time.</span></span>
*  <span data-ttu-id="1e968-326">형식의 식을 `dynamic` 라고 하는 ***동적 식***합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-326">An expression of the type `dynamic` is referred to as a ***dynamic expression***.</span></span>

### <a name="the-string-type"></a><span data-ttu-id="1e968-327">문자열 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-327">The string type</span></span>

<span data-ttu-id="1e968-328">합니다 `string` 형식이에서 직접 상속 되는 봉인된 클래스 형식이 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-328">The `string` type is a sealed class type that inherits directly from `object`.</span></span> <span data-ttu-id="1e968-329">인스턴스는 `string` 클래스 유니코드 문자열을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-329">Instances of the `string` class represent Unicode character strings.</span></span>

<span data-ttu-id="1e968-330">값을 `string` 형식 문자열 리터럴로 작성할 수 있습니다 ([문자열 리터럴](lexical-structure.md#string-literals)).</span><span class="sxs-lookup"><span data-stu-id="1e968-330">Values of the `string` type can be written as string literals ([String literals](lexical-structure.md#string-literals)).</span></span>

<span data-ttu-id="1e968-331">키워드 `string` 은 미리 정의 된 클래스에 대 한 별칭 `System.String`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-331">The keyword `string` is simply an alias for the predefined class `System.String`.</span></span>

### <a name="interface-types"></a><span data-ttu-id="1e968-332">인터페이스 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-332">Interface types</span></span>

<span data-ttu-id="1e968-333">인터페이스는 계약을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-333">An interface defines a contract.</span></span> <span data-ttu-id="1e968-334">클래스 또는 구조체는 인터페이스를 구현 하는 계약을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-334">A class or struct that implements an interface must adhere to its contract.</span></span> <span data-ttu-id="1e968-335">여러 기본 인터페이스에서 상속할 수 및 클래스 또는 구조체는 여러 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-335">An interface may inherit from multiple base interfaces, and a class or struct may implement multiple interfaces.</span></span>

<span data-ttu-id="1e968-336">인터페이스 형식에 설명 되어 있습니다 [인터페이스](interfaces.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-336">Interface types are described in [Interfaces](interfaces.md).</span></span>

### <a name="array-types"></a><span data-ttu-id="1e968-337">배열 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-337">Array types</span></span>

<span data-ttu-id="1e968-338">배열에는 계산 된 인덱스를 통해 액세스할 수 있는 0 개 이상의 변수를 포함 하는 데이터 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-338">An array is a data structure that contains zero or more variables which are accessed through computed indices.</span></span> <span data-ttu-id="1e968-339">배열의 요소를 배열에 포함 된 변수는 동일한 형식의 모든 및이 형식을 배열의 요소 형식 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-339">The variables contained in an array, also called the elements of the array, are all of the same type, and this type is called the element type of the array.</span></span>

<span data-ttu-id="1e968-340">배열 형식에 설명 되어 있습니다 [배열](arrays.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-340">Array types are described in [Arrays](arrays.md).</span></span>

### <a name="delegate-types"></a><span data-ttu-id="1e968-341">대리자 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-341">Delegate types</span></span>

<span data-ttu-id="1e968-342">대리자에는 하나 이상의 메서드를 가리키는 데이터 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-342">A delegate is a data structure that refers to one or more methods.</span></span> <span data-ttu-id="1e968-343">예를 들어 메서드를 의미할 수도 해당 개체 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="1e968-343">For instance methods, it also refers to their corresponding object instances.</span></span>

<span data-ttu-id="1e968-344">C 또는 c + +에서 대리자의 가장 가까운 해당 함수에 대 한 포인터 이지만 대리자 정적 참조를 인스턴스 메서드 함수 포인터를 정적 함수를 참조할 수 있습니다, 있지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-344">The closest equivalent of a delegate in C or C++ is a function pointer, but whereas a function pointer can only reference static functions, a delegate can reference both static and instance methods.</span></span> <span data-ttu-id="1e968-345">후자의 경우, 대리자 메서드의 진입점에 대 한 참조 뿐만 아니라 메서드를 호출 하는 개체 인스턴스에 대 한 참조를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-345">In the latter case, the delegate stores not only a reference to the method's entry point, but also a reference to the object instance on which to invoke the method.</span></span>

<span data-ttu-id="1e968-346">대리자 형식에 설명 되어 있습니다 [대리자](delegates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-346">Delegate types are described in [Delegates](delegates.md).</span></span>

## <a name="boxing-and-unboxing"></a><span data-ttu-id="1e968-347">boxing 및 unboxing</span><span class="sxs-lookup"><span data-stu-id="1e968-347">Boxing and unboxing</span></span>

<span data-ttu-id="1e968-348">Boxing 및 unboxing의 개념은 C#의 형식 시스템의 중심입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-348">The concept of boxing and unboxing is central to C#'s type system.</span></span> <span data-ttu-id="1e968-349">간의 브리지를 제공 *value_type*s 및 *reference_type*값을 허용 하 여는 *value_type* 형식에서 변환할 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-349">It provides a bridge between *value_type*s and *reference_type*s by permitting any value of a *value_type* to be converted to and from type `object`.</span></span> <span data-ttu-id="1e968-350">Boxing 및 unboxing에 통합된 형식 시스템의 모든 형식의 값을 개체로 처리 궁극적으로 수 여기서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-350">Boxing and unboxing enables a unified view of the type system wherein a value of any type can ultimately be treated as an object.</span></span>

### <a name="boxing-conversions"></a><span data-ttu-id="1e968-351">Boxing 변환</span><span class="sxs-lookup"><span data-stu-id="1e968-351">Boxing conversions</span></span>

<span data-ttu-id="1e968-352">boxing 변환이 허용을 *value_type* 암시적으로 변환할 수는 *reference_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-352">A boxing conversion permits a *value_type* to be implicitly converted to a *reference_type*.</span></span> <span data-ttu-id="1e968-353">다음과 같은 boxing 변환이 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-353">The following boxing conversions exist:</span></span>

*  <span data-ttu-id="1e968-354">모든 *value_type* 형식으로 `object`입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-354">From any *value_type* to the type `object`.</span></span>
*  <span data-ttu-id="1e968-355">모든 *value_type* 형식으로 `System.ValueType`입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-355">From any *value_type* to the type `System.ValueType`.</span></span>
*  <span data-ttu-id="1e968-356">*non_nullable_value_type* 하나로 *interface_type* 구현한 합니다 *value_type*.</span><span class="sxs-lookup"><span data-stu-id="1e968-356">From any *non_nullable_value_type* to any *interface_type* implemented by the *value_type*.</span></span>
*  <span data-ttu-id="1e968-357">*nullable_type* 에 *interface_type* 의 기본 형식에 의해 구현 된 *nullable_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-357">From any *nullable_type* to any *interface_type* implemented by the underlying type of the *nullable_type*.</span></span>
*  <span data-ttu-id="1e968-358">모든 *enum_type* 형식으로 `System.Enum`입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-358">From any *enum_type* to the type `System.Enum`.</span></span>
*  <span data-ttu-id="1e968-359">모든 *nullable_type* 사용 하 여 기본 *enum_type* 형식으로 `System.Enum`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-359">From any *nullable_type* with an underlying *enum_type* to the type `System.Enum`.</span></span>
*  <span data-ttu-id="1e968-360">형식 매개 변수에서의 암시적 변환이 참조 형식이 값 형식에서 변환할 끝나는 런타임에 경우 boxing 변환으로 실행 됩니다 ([형식 매개 변수를 포함 하는 암시적 변환은](conversions.md#implicit-conversions-involving-type-parameters)).</span><span class="sxs-lookup"><span data-stu-id="1e968-360">Note that an implicit conversion from a type parameter will be executed as a boxing conversion if at run-time it ends up converting from a value type to a reference type ([Implicit conversions involving type parameters](conversions.md#implicit-conversions-involving-type-parameters)).</span></span>

<span data-ttu-id="1e968-361">값을 *non_nullable_value_type* 이루어져 있습니다 개체 인스턴스를 할당 하 고 복사는 *non_nullable_value_type* 해당 인스턴스로 값.</span><span class="sxs-lookup"><span data-stu-id="1e968-361">Boxing a value of a *non_nullable_value_type* consists of allocating an object instance and copying the *non_nullable_value_type* value into that instance.</span></span>

<span data-ttu-id="1e968-362">값을 *nullable_type* 경우 null 참조를 생성 합니다 `null` 값 (`HasValue` 는 `false`), 또는 래핑 해제 하 고 그렇지 않은 경우 기본 값을 boxing의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-362">Boxing a value of a *nullable_type* produces a null reference if it is the `null` value (`HasValue` is `false`), or the result of unwrapping and boxing the underlying value otherwise.</span></span>

<span data-ttu-id="1e968-363">실제 프로세스의 값을 *non_nullable_value_type* 제네릭의 존재를 원할지 가장 잘 설명 되어 ***boxing 클래스***, 다음과 같이 선언 된 것 처럼 작동 하는:</span><span class="sxs-lookup"><span data-stu-id="1e968-363">The actual process of boxing a value of a *non_nullable_value_type* is best explained by imagining the existence of a generic ***boxing class***, which behaves as if it were declared as follows:</span></span>

```csharp
sealed class Box<T>: System.ValueType
{
    T value;

    public Box(T t) {
        value = t;
    }
}
```

<span data-ttu-id="1e968-364">값을 boxing `v` 형식의 `T` 식을 실행 이루어져 `new Box<T>(v)`, 결과 인스턴스 형식의 값으로 반환 하 고 `object`입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-364">Boxing of a value `v` of type `T` now consists of executing the expression `new Box<T>(v)`, and returning the resulting instance as a value of type `object`.</span></span> <span data-ttu-id="1e968-365">따라서 다음 문은</span><span class="sxs-lookup"><span data-stu-id="1e968-365">Thus, the statements</span></span>
```csharp
int i = 123;
object box = i;
```
<span data-ttu-id="1e968-366">에 해당 하는 개념적으로</span><span class="sxs-lookup"><span data-stu-id="1e968-366">conceptually correspond to</span></span>
```csharp
int i = 123;
object box = new Box<int>(i);
```

<span data-ttu-id="1e968-367">같은 boxing 클래스 `Box<T>` 위에 실제로 없는 boxed 값의 동적 형식에는 실제로 클래스 형식이 아닌 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-367">A boxing class like `Box<T>` above doesn't actually exist and the dynamic type of a boxed value isn't actually a class type.</span></span> <span data-ttu-id="1e968-368">대신 형식의 boxed 값 `T` 동적 형식이 `T`를 사용 하 여 동적 형식을 확인 하 고는 `is` 연산자 종류를 간단히 참조할 수 `T`입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-368">Instead, a boxed value of type `T` has the dynamic type `T`, and a dynamic type check using the `is` operator can simply reference type `T`.</span></span> <span data-ttu-id="1e968-369">예를 들어 개체에 적용된</span><span class="sxs-lookup"><span data-stu-id="1e968-369">For example,</span></span>
```csharp
int i = 123;
object box = i;
if (box is int) {
    Console.Write("Box contains an int");
}
```
<span data-ttu-id="1e968-370">문자열을 출력 "`Box contains an int`" 콘솔에서.</span><span class="sxs-lookup"><span data-stu-id="1e968-370">will output the string "`Box contains an int`" on the console.</span></span>

<span data-ttu-id="1e968-371">Boxing 변환 되 고 boxed 값의 복사본을 만드는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-371">A boxing conversion implies making a copy of the value being boxed.</span></span> <span data-ttu-id="1e968-372">이 변환에서 다른를 *reference_type* 입력 `object`, 값을 계속 동일한 인스턴스를 참조 하 고 단순히 더 적게 파생 된 형식으로 간주 됩니다 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-372">This is different from a conversion of a *reference_type* to type `object`, in which the value continues to reference the same instance and simply is regarded as the less derived type `object`.</span></span> <span data-ttu-id="1e968-373">예를 들어 선언 된 경우</span><span class="sxs-lookup"><span data-stu-id="1e968-373">For example, given the declaration</span></span>
```csharp
struct Point
{
    public int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```
<span data-ttu-id="1e968-374">다음 문은</span><span class="sxs-lookup"><span data-stu-id="1e968-374">the following statements</span></span>
```csharp
Point p = new Point(10, 10);
object box = p;
p.x = 20;
Console.Write(((Point)box).x);
```
<span data-ttu-id="1e968-375">때문에 콘솔에 있는 값 10을 출력 할당이 발생 하는 암시적 boxing 연산을 `p` 를 `box` 의 값 `p` 복사할 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-375">will output the value 10 on the console because the implicit boxing operation that occurs in the assignment of `p` to `box` causes the value of `p` to be copied.</span></span> <span data-ttu-id="1e968-376">했습니다 `Point` 된 선언를 `class` 대신 값 20 것 출력 하므로 `p` 및 `box` 동일한 인스턴스를 참조 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-376">Had `Point` been declared a `class` instead, the value 20 would be output because `p` and `box` would reference the same instance.</span></span>

### <a name="unboxing-conversions"></a><span data-ttu-id="1e968-377">Unboxing 변환</span><span class="sxs-lookup"><span data-stu-id="1e968-377">Unboxing conversions</span></span>

<span data-ttu-id="1e968-378">Unboxing 변환 허용 된 *reference_type* 명시적으로 변환할 수는 *value_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-378">An unboxing conversion permits a *reference_type* to be explicitly converted to a *value_type*.</span></span> <span data-ttu-id="1e968-379">다음과 같은 unboxing 변환이 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-379">The following unboxing conversions exist:</span></span>

*  <span data-ttu-id="1e968-380">형식에서 `object` 하나로 *value_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-380">From the type `object` to any *value_type*.</span></span>
*  <span data-ttu-id="1e968-381">형식에서 `System.ValueType` 하나로 *value_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-381">From the type `System.ValueType` to any *value_type*.</span></span>
*  <span data-ttu-id="1e968-382">*interface_type* 하나로 *non_nullable_value_type* 구현 하는 합니다 *interface_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-382">From any *interface_type* to any *non_nullable_value_type* that implements the *interface_type*.</span></span>
*  <span data-ttu-id="1e968-383">모든 *interface_type* 에 *nullable_type* 기본 형식이 구현 하는 *interface_type*.</span><span class="sxs-lookup"><span data-stu-id="1e968-383">From any *interface_type* to any *nullable_type* whose underlying type implements the *interface_type*.</span></span>
*  <span data-ttu-id="1e968-384">형식에서 `System.Enum` 하나로 *enum_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-384">From the type `System.Enum` to any *enum_type*.</span></span>
*  <span data-ttu-id="1e968-385">형식에서 `System.Enum` 하나로 *nullable_type* 사용 하 여 내부 *enum_type*.</span><span class="sxs-lookup"><span data-stu-id="1e968-385">From the type `System.Enum` to any *nullable_type* with an underlying *enum_type*.</span></span>
*  <span data-ttu-id="1e968-386">형식 매개 변수에 명시적 변환이 런타임에 값 형식이 참조 형식에서 변환할 끝나고 경우 unboxing 변환으로 실행 됩니다 ([명시적 동적 변환을](conversions.md#explicit-dynamic-conversions)).</span><span class="sxs-lookup"><span data-stu-id="1e968-386">Note that an explicit conversion to a type parameter will be executed as an unboxing conversion if at run-time it ends up converting from a reference type to a value type ([Explicit dynamic conversions](conversions.md#explicit-dynamic-conversions)).</span></span>

<span data-ttu-id="1e968-387">unboxing 작업으로 인해를 *non_nullable_value_type* 개체 인스턴스에 boxed 값은 첫 번째 검사 구성를 지정 *non_nullable_value_type*, 다음의 값을 복사 하 고는 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-387">An unboxing operation to a *non_nullable_value_type* consists of first checking that the object instance is a boxed value of the given *non_nullable_value_type*, and then copying the value out of the instance.</span></span>

<span data-ttu-id="1e968-388">unboxing를 *nullable_type* 의 null 값을 생성 합니다 *nullable_type* 소스 피연산자가 `null`, 또는 내부 형식의 개체 인스턴스를 unboxing의 래핑된 결과 *nullable_type* 그렇지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="1e968-388">Unboxing to a *nullable_type* produces the null value of the *nullable_type* if the source operand is `null`, or the wrapped result of unboxing the object instance to the underlying type of the *nullable_type* otherwise.</span></span>

<span data-ttu-id="1e968-389">Unboxing 변환 개체의 이전 섹션에 설명 된 boxing 클래스 참조 `box` 에 *value_type* `T` 식을 실행 구성 `((Box<T>)box).value`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-389">Referring to the imaginary boxing class described in the previous section, an unboxing conversion of an object `box` to a *value_type* `T` consists of executing the expression `((Box<T>)box).value`.</span></span> <span data-ttu-id="1e968-390">따라서 다음 문은</span><span class="sxs-lookup"><span data-stu-id="1e968-390">Thus, the statements</span></span>
```csharp
object box = 123;
int i = (int)box;
```
<span data-ttu-id="1e968-391">에 해당 하는 개념적으로</span><span class="sxs-lookup"><span data-stu-id="1e968-391">conceptually correspond to</span></span>
```csharp
object box = new Box<int>(123);
int i = ((Box<int>)box).value;
```

<span data-ttu-id="1e968-392">unboxing 변환에 대 한는 주어진 *non_nullable_value_type* 런타임에 성공 하려면 소스 피연산자의 값의 boxed 값에 대 한 참조 여야 합니다 *non_nullable_value_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-392">For an unboxing conversion to a given *non_nullable_value_type* to succeed at run-time, the value of the source operand must be a reference to a boxed value of that *non_nullable_value_type*.</span></span> <span data-ttu-id="1e968-393">소스 피연산자가 `null`, `System.NullReferenceException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-393">If the source operand is `null`, a `System.NullReferenceException` is thrown.</span></span> <span data-ttu-id="1e968-394">소스 피연산자가 호환 되지 않는 개체에 대 한 참조를 `System.InvalidCastException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-394">If the source operand is a reference to an incompatible object, a `System.InvalidCastException` is thrown.</span></span>

<span data-ttu-id="1e968-395">unboxing 변환에 대 한는 주어진 *nullable_type* 런타임에 성공 하려면 소스 피연산자의 값 중 하나 여야 합니다 `null` 또는 기본 boxed 값에 대 한 참조를 *non_nullable_value_type* 의 합니다 *nullable_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-395">For an unboxing conversion to a given *nullable_type* to succeed at run-time, the value of the source operand must be either `null` or a reference to a boxed value of the underlying *non_nullable_value_type* of the *nullable_type*.</span></span> <span data-ttu-id="1e968-396">소스 피연산자가 호환 되지 않는 개체에 대 한 참조를 `System.InvalidCastException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-396">If the source operand is a reference to an incompatible object, a `System.InvalidCastException` is thrown.</span></span>

## <a name="constructed-types"></a><span data-ttu-id="1e968-397">생성 된 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-397">Constructed types</span></span>

<span data-ttu-id="1e968-398">제네릭 형식 선언 자체로 나타냅니다는 ***언바운드 제네릭 형식*** 적용을 통해 다양 한 유형을 구성 하는 데 "설계도"로 사용 되는 ***형식 인수***합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-398">A generic type declaration, by itself, denotes an ***unbound generic type*** that is used as a "blueprint" to form many different types, by way of applying ***type arguments***.</span></span> <span data-ttu-id="1e968-399">형식 인수를 꺾쇠 괄호 내에 기록 됩니다 (`<` 및 `>`) 바로 다음 일반 형식의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-399">The type arguments are written within angle brackets (`<` and `>`) immediately following the name of the generic type.</span></span> <span data-ttu-id="1e968-400">하나 이상의 형식 인수를 포함 하는 형식에 호출 되는 ***생성 된 형식***합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-400">A type that includes at least one type argument is called a ***constructed type***.</span></span> <span data-ttu-id="1e968-401">생성된 된 형식은 형식 이름이 나타날 수 있는 언어의 대부분의 위치에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-401">A constructed type can be used in most places in the language in which a type name can appear.</span></span> <span data-ttu-id="1e968-402">바인딩되지 않은 제네릭 형식 내 에서만 사용할 수는 *typeof_expression* ([typeof 연산자](expressions.md#the-typeof-operator)).</span><span class="sxs-lookup"><span data-stu-id="1e968-402">An unbound generic type can only be used within a *typeof_expression* ([The typeof operator](expressions.md#the-typeof-operator)).</span></span>

<span data-ttu-id="1e968-403">생성 된 형식을 사용할 수도 있습니다 식에서 간단한 이름으로 ([단순 이름](expressions.md#simple-names)) 멤버에 액세스 하는 경우 또는 ([멤버 액세스](expressions.md#member-access)).</span><span class="sxs-lookup"><span data-stu-id="1e968-403">Constructed types can also be used in expressions as simple names ([Simple names](expressions.md#simple-names)) or when accessing a member ([Member access](expressions.md#member-access)).</span></span>

<span data-ttu-id="1e968-404">경우는 *namespace_or_type_name* 평가, 제네릭 형식과 올바른 개수의 형식 매개 변수를 사용 하는 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-404">When a *namespace_or_type_name* is evaluated, only generic types with the correct number of type parameters are considered.</span></span> <span data-ttu-id="1e968-405">따라서으로 형식을 형식 매개 변수의 수가 달라 서로 다른 형식을 식별 하려면 동일한 식별자를 사용 하는 것이 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-405">Thus, it is possible to use the same identifier to identify different types, as long as the types have different numbers of type parameters.</span></span> <span data-ttu-id="1e968-406">동일한 프로그램에서 제네릭 및 제네릭이 아닌 클래스를 혼합 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-406">This is useful when mixing generic and non-generic classes in the same program:</span></span>

```csharp
namespace Widgets
{
    class Queue {...}
    class Queue<TElement> {...}
}

namespace MyApplication
{
    using Widgets;

    class X
    {
        Queue q1;            // Non-generic Widgets.Queue
        Queue<int> q2;       // Generic Widgets.Queue
    }
}
```

<span data-ttu-id="1e968-407">A *type_name* 형식 매개 변수를 직접 지정 하지 않으면 해당 하는 경우에 생성된 된 형식을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-407">A *type_name* might identify a constructed type even though it doesn't specify type parameters directly.</span></span> <span data-ttu-id="1e968-408">이 형식을 제네릭 클래스 선언 내에 중첩 되어 및 인스턴스 유형을 포함 하는 선언의 이름 조회에 대 한 암시적으로 사용 되는 발생할 수 있습니다 ([제네릭 클래스의 형식에 중첩 된](classes.md#nested-types-in-generic-classes)):</span><span class="sxs-lookup"><span data-stu-id="1e968-408">This can occur where a type is nested within a generic class declaration, and the instance type of the containing declaration is implicitly used for name lookup ([Nested types in generic classes](classes.md#nested-types-in-generic-classes)):</span></span>

```csharp
class Outer<T>
{
    public class Inner {...}

    public Inner i;                // Type of i is Outer<T>.Inner
}
```

<span data-ttu-id="1e968-409">안전 하지 않은 코드 생성된 된 형식으로 사용할 수 없습니다는 *unmanaged_type* ([포인터 형식](unsafe-code.md#pointer-types)).</span><span class="sxs-lookup"><span data-stu-id="1e968-409">In unsafe code, a constructed type cannot be used as an *unmanaged_type* ([Pointer types](unsafe-code.md#pointer-types)).</span></span>

### <a name="type-arguments"></a><span data-ttu-id="1e968-410">형식 인수</span><span class="sxs-lookup"><span data-stu-id="1e968-410">Type arguments</span></span>

<span data-ttu-id="1e968-411">형식 인수 목록의 각 인수는 단순히를 *형식*합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-411">Each argument in a type argument list is simply a *type*.</span></span>

```antlr
type_argument_list
    : '<' type_arguments '>'
    ;

type_arguments
    : type_argument (',' type_argument)*
    ;

type_argument
    : type
    ;
```

<span data-ttu-id="1e968-412">안전 하지 않은 코드 ([안전 하지 않은 코드](unsafe-code.md)), *type_argument* 포인터 형식이 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-412">In unsafe code ([Unsafe code](unsafe-code.md)), a *type_argument* may not be a pointer type.</span></span> <span data-ttu-id="1e968-413">각 형식 인수가 형식 매개 변수를 해당 제약 조건을 충족 해야 합니다 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="1e968-413">Each type argument must satisfy any constraints on the corresponding type parameter ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span>

### <a name="open-and-closed-types"></a><span data-ttu-id="1e968-414">개방형 형식과 닫힌 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-414">Open and closed types</span></span>

<span data-ttu-id="1e968-415">모든 형식 중 하나로 분류 될 수 있습니다 ***개방형 형식만*** 하거나 ***닫힌 형식을***합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-415">All types can be classified as either ***open types*** or ***closed types***.</span></span> <span data-ttu-id="1e968-416">개방형 형식 형식이 형식 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-416">An open type is a type that involves type parameters.</span></span> <span data-ttu-id="1e968-417">좀 더 구체적으로:</span><span class="sxs-lookup"><span data-stu-id="1e968-417">More specifically:</span></span>

*  <span data-ttu-id="1e968-418">형식 매개 변수는 개방형 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-418">A type parameter defines an open type.</span></span>
*  <span data-ttu-id="1e968-419">배열 형식의 요소 형식과 개방형 형식인 경우에 열려 형식인 경우</span><span class="sxs-lookup"><span data-stu-id="1e968-419">An array type is an open type if and only if its element type is an open type.</span></span>
*  <span data-ttu-id="1e968-420">생성 된 형식이 개방형 형식 형식 인수 중 하나 이상의 개방형 형식인 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-420">A constructed type is an open type if and only if one or more of its type arguments is an open type.</span></span> <span data-ttu-id="1e968-421">생성된 된 중첩된 형식을 해당 형식 인수 또는 해당 포함 형식의 형식 인수를 하나 이상의 개방형 형식인 경우에 개방형 형식인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-421">A constructed nested type is an open type if and only if one or more of its type arguments or the type arguments of its containing type(s) is an open type.</span></span>

<span data-ttu-id="1e968-422">닫힌된 형식 형식이 개방형 형식이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-422">A closed type is a type that is not an open type.</span></span>

<span data-ttu-id="1e968-423">런타임에, 제네릭 형식 선언 내에서 코드를 모두를 제네릭 선언에 형식 인수를 적용 하 여 만들어진 여 폐쇄형된 생성된 형식의 컨텍스트에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-423">At run-time, all of the code within a generic type declaration is executed in the context of a closed constructed type that was created by applying type arguments to the generic declaration.</span></span> <span data-ttu-id="1e968-424">제네릭 형식 내에서 각 형식 매개 변수는 특정 런타임 형식에 바인딩되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-424">Each type parameter within the generic type is bound to a particular run-time type.</span></span> <span data-ttu-id="1e968-425">모든 문 및 식의 런타임 처리는 항상 발생 하는 닫힌된 형식은 부족해져 개방형 형식 컴파일 시간 동안에 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-425">The run-time processing of all statements and expressions always occurs with closed types, and open types occur only during compile-time processing.</span></span>

<span data-ttu-id="1e968-426">각 폐쇄형된 생성된 형식이 마다 고유한 정적 변수를 다른 폐쇄형된 생성된 형식와 공유 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-426">Each closed constructed type has its own set of static variables, which are not shared with any other closed constructed types.</span></span> <span data-ttu-id="1e968-427">런타임 시 개방형 형식이 없으므로 변수가 없음을 정적 개방형 형식을 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-427">Since an open type does not exist at run-time, there are no static variables associated with an open type.</span></span> <span data-ttu-id="1e968-428">두 폐쇄형된 생성된 형식 동일한 언바운드 제네릭 형식에서 생성 된 경우 해당 형식 인수는 동일한 형식은 동일한 형식은입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-428">Two closed constructed types are the same type if they are constructed from the same unbound generic type, and their corresponding type arguments are the same type.</span></span>

### <a name="bound-and-unbound-types"></a><span data-ttu-id="1e968-429">바인딩 및 바인딩되지 않은 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-429">Bound and unbound types</span></span>

<span data-ttu-id="1e968-430">용어 ***형식에 바인딩되지 않은*** 제네릭이 아닌 형식 또는 바인딩되지 않은 제네릭 형식 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-430">The term ***unbound type*** refers to a non-generic type or an unbound generic type.</span></span> <span data-ttu-id="1e968-431">용어 ***형식에 바인딩된*** 제네릭이 아닌 형식 또는 생성된 된 형식을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-431">The term ***bound type*** refers to a non-generic type or a constructed type.</span></span>

<span data-ttu-id="1e968-432">바인딩되지 않은 형식은 형식 선언에서 선언 된 엔터티를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-432">An unbound type refers to the entity declared by a type declaration.</span></span> <span data-ttu-id="1e968-433">바인딩되지 않은 제네릭 형식 자체는 형식이 이며 변수, 인수 또는 반환 값의 형식으로 또는 기본 형식으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-433">An unbound generic type is not itself a type, and cannot be used as the type of a variable, argument or return value, or as a base type.</span></span> <span data-ttu-id="1e968-434">바인딩되지 않은 제네릭 형식을 참조할 수 있습니다만 구문을 합니다 `typeof` 식 ([typeof 연산자](expressions.md#the-typeof-operator)).</span><span class="sxs-lookup"><span data-stu-id="1e968-434">The only construct in which an unbound generic type can be referenced is the `typeof` expression ([The typeof operator](expressions.md#the-typeof-operator)).</span></span>

### <a name="satisfying-constraints"></a><span data-ttu-id="1e968-435">만족 제약 조건</span><span class="sxs-lookup"><span data-stu-id="1e968-435">Satisfying constraints</span></span>

<span data-ttu-id="1e968-436">제공 된 형식 인수는 생성 된 형식 또는 제네릭 메서드를 참조할 때마다에 제네릭 형식 또는 메서드의 선언 형식 매개 변수 제약 조건을 검사할지 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="1e968-436">Whenever a constructed type or generic method is referenced, the supplied type arguments are checked against the type parameter constraints declared on the generic type or method ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span> <span data-ttu-id="1e968-437">각 `where` 절, 형식 인수 `A` 명명 된에 해당 하는 각 제약 조건에 대해 다음과 같이 형식 매개 변수를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-437">For each `where` clause, the type argument `A` that corresponds to the named type parameter is checked against each constraint as follows:</span></span>

*  <span data-ttu-id="1e968-438">클래스 형식, 인터페이스 형식 또는 형식 매개 변수 제약 조건이 있으면 수 있도록 `C` 제공 된 형식 인수를 사용 하 여 제약 조건을 제약 조건에 표시 되는 모든 형식 매개 변수 대체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-438">If the constraint is a class type, an interface type, or a type parameter, let `C` represent that constraint with the supplied type arguments substituted for any type parameters that appear in the constraint.</span></span> <span data-ttu-id="1e968-439">제약 조건을 만족를 입력 하는 경우 여야 `A` 형식으로 변환 될 `C` 다음 중 하나에서:</span><span class="sxs-lookup"><span data-stu-id="1e968-439">To satisfy the constraint, it must be the case that type `A` is convertible to type `C` by one of the following:</span></span>
    * <span data-ttu-id="1e968-440">Id 변환이 ([Id 변환을](conversions.md#identity-conversion))</span><span class="sxs-lookup"><span data-stu-id="1e968-440">An identity conversion ([Identity conversion](conversions.md#identity-conversion))</span></span>
    * <span data-ttu-id="1e968-441">암시적 참조 변환 ([암시적 참조 변환](conversions.md#implicit-reference-conversions))</span><span class="sxs-lookup"><span data-stu-id="1e968-441">An implicit reference conversion ([Implicit reference conversions](conversions.md#implicit-reference-conversions))</span></span>
    * <span data-ttu-id="1e968-442">Boxing 변환 ([Boxing 변환](conversions.md#boxing-conversions))는 형식이 nullable이 아닌 값 형식이 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="1e968-442">A boxing conversion ([Boxing conversions](conversions.md#boxing-conversions)), provided that type A is a non-nullable value type.</span></span>
    * <span data-ttu-id="1e968-443">형식 매개 변수에서 암시적 참조, boxing 또는 형식 매개 변수 변환이 `A` 에 `C`입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-443">An implicit reference, boxing or type parameter conversion from a type parameter `A` to `C`.</span></span>
*  <span data-ttu-id="1e968-444">제약 조건 참조 형식 제약 조건이 있으면 (`class`), 형식 `A` 다음 중 하나를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-444">If the constraint is the reference type constraint (`class`), the type `A` must satisfy one of the following:</span></span>
    * <span data-ttu-id="1e968-445">`A` 인터페이스 형식, 클래스 형식, 대리자 형식 또는 배열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-445">`A` is an interface type, class type, delegate type or array type.</span></span> <span data-ttu-id="1e968-446">사실은 `System.ValueType` 및 `System.Enum` 는이 제약 조건을 만족 하는 참조 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-446">Note that `System.ValueType` and `System.Enum` are reference types that satisfy this constraint.</span></span>
    * <span data-ttu-id="1e968-447">`A` 참조 형식 이어야 하 라고 하는 형식 매개 변수 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="1e968-447">`A` is a type parameter that is known to be a reference type ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span>
*  <span data-ttu-id="1e968-448">제약 조건 값 형식 제약 조건이 있으면 (`struct`), 형식 `A` 다음 중 하나를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-448">If the constraint is the value type constraint (`struct`), the type `A` must satisfy one of the following:</span></span>
    * <span data-ttu-id="1e968-449">`A` 구조체 형식 또는 열거형 형식이 아니라 nullable 형식이 아닌 경우</span><span class="sxs-lookup"><span data-stu-id="1e968-449">`A` is a struct type or enum type, but not a nullable type.</span></span> <span data-ttu-id="1e968-450">사실은 `System.ValueType` 및 `System.Enum` 는이 제약 조건을 만족 하지 않는 참조 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-450">Note that `System.ValueType` and `System.Enum` are reference types that do not satisfy this constraint.</span></span>
    * <span data-ttu-id="1e968-451">`A` 값 형식 제약 조건이 있는 형식 매개 변수입니다 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="1e968-451">`A` is a type parameter having the value type constraint ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span>
*  <span data-ttu-id="1e968-452">제약 조건을 생성자 제약 조건이 있으면 `new()`, 형식 `A` 아니어야 `abstract` 매개 변수가 없는 공용 생성자가 있어야 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-452">If the constraint is the constructor constraint `new()`, the type `A` must not be `abstract` and must have a public parameterless constructor.</span></span> <span data-ttu-id="1e968-453">이 중 하나가 참인 경우 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-453">This is satisfied if one of the following is true:</span></span>
    * <span data-ttu-id="1e968-454">`A` 값 형식 이므로 모든 값 형식에 공용 기본 생성자가 ([기본 생성자](types.md#default-constructors)).</span><span class="sxs-lookup"><span data-stu-id="1e968-454">`A` is a value type, since all value types have a public default constructor ([Default constructors](types.md#default-constructors)).</span></span>
    * <span data-ttu-id="1e968-455">`A` 생성자 제약 조건이 있는 형식 매개 변수입니다 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="1e968-455">`A` is a type parameter having the constructor constraint ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span>
    * <span data-ttu-id="1e968-456">`A` 값 형식 제약 조건이 있는 형식 매개 변수입니다 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="1e968-456">`A` is a type parameter having the value type constraint ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span>
    * <span data-ttu-id="1e968-457">`A` 없는 클래스인 `abstract` 명시적으로 선언 된 포함 및 `public` 매개 변수가 없는 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-457">`A` is a class that is not `abstract` and contains an explicitly declared `public` constructor with no parameters.</span></span>
    * <span data-ttu-id="1e968-458">`A` 아닙니다 `abstract` 기본 생성자를 포함 ([기본 생성자](classes.md#default-constructors)).</span><span class="sxs-lookup"><span data-stu-id="1e968-458">`A` is not `abstract` and has a default constructor ([Default constructors](classes.md#default-constructors)).</span></span>

<span data-ttu-id="1e968-459">컴파일 타임 오류가 발생 하는 지정 된 형식 인수에서 형식 매개 변수의 제약 조건 중 하나 이상이 충족 되지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="1e968-459">A compile-time error occurs if one or more of a type parameter's constraints are not satisfied by the given type arguments.</span></span>

<span data-ttu-id="1e968-460">제약 조건은 형식 매개 변수는 상속 되지 있으므로 되지 중 하나를 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-460">Since type parameters are not inherited, constraints are never inherited either.</span></span> <span data-ttu-id="1e968-461">아래 예에서 `D` 해당 형식 매개 변수에 제약 조건을 지정 해야 `T` 있도록 `T` 기본 클래스에 의해 적용 된 제약 조건을 만족 `B<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-461">In the example below, `D` needs to specify the constraint on its type parameter `T` so that `T` satisfies the constraint imposed by the base class `B<T>`.</span></span> <span data-ttu-id="1e968-462">반면, 클래스 `E` 때문에 제약 조건을 지정할 필요가 `List<T>` 구현 `IEnumerable` 에 대 한 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-462">In contrast, class `E` need not specify a constraint, because `List<T>` implements `IEnumerable` for any `T`.</span></span>

```csharp
class B<T> where T: IEnumerable {...}

class D<T>: B<T> where T: IEnumerable {...}

class E<T>: B<List<T>> {...}
```

## <a name="type-parameters"></a><span data-ttu-id="1e968-463">형식 매개 변수</span><span class="sxs-lookup"><span data-stu-id="1e968-463">Type parameters</span></span>

<span data-ttu-id="1e968-464">형식 매개 변수는 값 형식 또는 매개 변수에서 런타임에 바인딩되는 참조 형식 지정 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-464">A type parameter is an identifier designating a value type or reference type that the parameter is bound to at run-time.</span></span>

```antlr
type_parameter
    : identifier
    ;
```

<span data-ttu-id="1e968-465">형식 매개 변수는 많은 다른 실제 형식 인수를 사용 하 여 인스턴스화할 수 있습니다, 되므로 형식 매개 변수는 약간 다른 작업 및 기타 형식 보다 제한이 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-465">Since a type parameter can be instantiated with many different actual type arguments, type parameters have slightly different operations and restrictions than other types.</span></span> <span data-ttu-id="1e968-466">여기에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-466">These include:</span></span>

*  <span data-ttu-id="1e968-467">형식 매개 변수는 기본 클래스를 선언 하는 직접 사용할 수 없습니다 ([기본 클래스](classes.md#base-class)) 또는 인터페이스 ([Variant 형식 매개 변수 목록이](interfaces.md#variant-type-parameter-lists)).</span><span class="sxs-lookup"><span data-stu-id="1e968-467">A type parameter cannot be used directly to declare a base class ([Base class](classes.md#base-class)) or interface ([Variant type parameter lists](interfaces.md#variant-type-parameter-lists)).</span></span>
*  <span data-ttu-id="1e968-468">형식 매개 변수에 있으면 제약 조건에 따라 달라 집니다 매개 변수 형식에 멤버 조회에 대 한 규칙을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-468">The rules for member lookup on type parameters depend on the constraints, if any, applied to the type parameter.</span></span> <span data-ttu-id="1e968-469">자세히 설명 [멤버 조회](expressions.md#member-lookup)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-469">They are detailed in [Member lookup](expressions.md#member-lookup).</span></span>
*  <span data-ttu-id="1e968-470">사용 가능한 변환이 있으면 제약 조건에 따라 달라 집니다 형식 매개 변수에 대 한 형식 매개 변수에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-470">The available conversions for a type parameter depend on the constraints, if any, applied to the type parameter.</span></span> <span data-ttu-id="1e968-471">자세히 설명 [형식 매개 변수를 포함 하는 암시적 변환은](conversions.md#implicit-conversions-involving-type-parameters) 하 고 [명시적 동적 변환을](conversions.md#explicit-dynamic-conversions)입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-471">They are detailed in [Implicit conversions involving type parameters](conversions.md#implicit-conversions-involving-type-parameters) and [Explicit dynamic conversions](conversions.md#explicit-dynamic-conversions).</span></span>
*  <span data-ttu-id="1e968-472">리터럴 `null` 참조 형식으로 형식 매개 변수 라고 하는 경우 제외 하 고는 형식 매개 변수에 의해 지정 된 형식으로 변환할 수 없습니다 ([형식 매개 변수를 포함 하는 암시적 변환은](conversions.md#implicit-conversions-involving-type-parameters)).</span><span class="sxs-lookup"><span data-stu-id="1e968-472">The literal `null` cannot be converted to a type given by a type parameter, except if the type parameter is known to be a reference type ([Implicit conversions involving type parameters](conversions.md#implicit-conversions-involving-type-parameters)).</span></span> <span data-ttu-id="1e968-473">그러나를 `default` 식 ([기본값 식](expressions.md#default-value-expressions)) 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-473">However, a `default` expression ([Default value expressions](expressions.md#default-value-expressions)) can be used instead.</span></span> <span data-ttu-id="1e968-474">또한 형식 매개 변수로 지정 된 형식으로 값을 비교할 수 `null` 를 사용 하 여 `==` 하 고 `!=` ([참조 형식이 같음 연산자](expressions.md#reference-type-equality-operators)) 형식 매개 변수 값 형식 제약 조건에 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="1e968-474">In addition, a value with a type given by a type parameter can be compared with `null` using `==` and `!=` ([Reference type equality operators](expressions.md#reference-type-equality-operators)) unless the type parameter has the value type constraint.</span></span>
*  <span data-ttu-id="1e968-475">A `new` 식 ([개체 만들기 식](expressions.md#object-creation-expressions))만 사용할 수 있습니다 형식 매개 변수를 사용 하 여 형식 매개 변수에 의해 제한 되는 경우는 *constructor_constraint* 또는 값 형식 제약 조건 ([ 형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="1e968-475">A `new` expression ([Object creation expressions](expressions.md#object-creation-expressions)) can only be used with a type parameter if the type parameter is constrained by a *constructor_constraint* or the value type constraint ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span>
*  <span data-ttu-id="1e968-476">형식 매개 변수 특성 내 어디서 나 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-476">A type parameter cannot be used anywhere within an attribute.</span></span>
*  <span data-ttu-id="1e968-477">멤버 액세스에서 형식 매개 변수를 사용할 수 없습니다 ([멤버 액세스](expressions.md#member-access)) 또는 형식 이름 ([Namespace 및 형식 이름](basic-concepts.md#namespace-and-type-names)) 정적 멤버 또는 중첩된 된 형식을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-477">A type parameter cannot be used in a member access ([Member access](expressions.md#member-access)) or type name ([Namespace and type names](basic-concepts.md#namespace-and-type-names)) to identify a static member or a nested type.</span></span>
*  <span data-ttu-id="1e968-478">안전 하지 않은 코드 형식 매개 변수를 사용할 수 없습니다는 *unmanaged_type* ([포인터 형식](unsafe-code.md#pointer-types)).</span><span class="sxs-lookup"><span data-stu-id="1e968-478">In unsafe code, a type parameter cannot be used as an *unmanaged_type* ([Pointer types](unsafe-code.md#pointer-types)).</span></span>

<span data-ttu-id="1e968-479">형식으로 형식 매개 변수는 컴파일 타임 구문 순수 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-479">As a type, type parameters are purely a compile-time construct.</span></span> <span data-ttu-id="1e968-480">실행 시 각 형식 매개 변수를 제네릭 형식 선언에 형식 인수를 제공 하 여 지정 된 런타임 형식에 바인딩되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-480">At run-time, each type parameter is bound to a run-time type that was specified by supplying a type argument to the generic type declaration.</span></span> <span data-ttu-id="1e968-481">따라서 폐쇄형된 생성된 형식 수를 런타임 시 형식 매개 변수는 사용 하 여 변수의 형식을 선언 ([열기 및 닫힌 형식을](types.md#open-and-closed-types)).</span><span class="sxs-lookup"><span data-stu-id="1e968-481">Thus, the type of a variable declared with a type parameter will, at run-time, be a closed constructed type ([Open and closed types](types.md#open-and-closed-types)).</span></span> <span data-ttu-id="1e968-482">해당 매개 변수에 대 한 형식 인수로 지정 된 실제 형식을 사용 하는 모든 문 및 형식 매개 변수를 포함 하는 식의 런타임 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-482">The run-time execution of all statements and expressions involving type parameters uses the actual type that was supplied as the type argument for that parameter.</span></span>

## <a name="expression-tree-types"></a><span data-ttu-id="1e968-483">식 트리 형식</span><span class="sxs-lookup"><span data-stu-id="1e968-483">Expression tree types</span></span>

<span data-ttu-id="1e968-484">***식 트리*** 람다 식을 실행 코드 대신 데이터 구조로 나타낼 수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-484">***Expression trees*** permit lambda expressions to be represented as data structures instead of executable code.</span></span> <span data-ttu-id="1e968-485">식 트리는 값 ***식 트리 형식*** 양식의 `System.Linq.Expressions.Expression<D>`여기서 `D` 모든 대리자 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-485">Expression trees are values of ***expression tree types*** of the form `System.Linq.Expressions.Expression<D>`, where `D` is any delegate type.</span></span> <span data-ttu-id="1e968-486">이 사양의 나머지 부분에 대 한 참조는 약어를 사용 하 여 이러한 형식을 `Expression<D>`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-486">For the remainder of this specification we will refer to these types using the shorthand `Expression<D>`.</span></span>

<span data-ttu-id="1e968-487">대리자 형식에 대 한 변환이 존재 람다 식에서 경우 `D`, 식 트리 형식으로 변환도 존재 `Expression<D>`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-487">If a conversion exists from a lambda expression to a delegate type `D`, a conversion also exists to the expression tree type `Expression<D>`.</span></span> <span data-ttu-id="1e968-488">람다 식의 실행 코드를 참조 하는 대리자를 생성 하는 람다 식 대리자 형식으로 변환 하는 반면는 식 트리 형식으로 변환 하는 람다 식의 식 트리 표현을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-488">Whereas the conversion of a lambda expression to a delegate type generates a delegate that references executable code for the lambda expression, conversion to an expression tree type creates an expression tree representation of the lambda expression.</span></span>

<span data-ttu-id="1e968-489">식 트리 람다 식의 효율적인 메모리 내 데이터 표시 하 고 투명 하 고 명시적 람다 식의 구조를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-489">Expression trees are efficient in-memory data representations of lambda expressions and make the structure of the lambda expression transparent and explicit.</span></span>

<span data-ttu-id="1e968-490">마찬가지로 다음 대리자 형식을 `D`, `Expression<D>` 매개 변수 및 반환 형식 이라고의 것과 동일는 `D`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-490">Just like a delegate type `D`, `Expression<D>` is said to have parameter and return types, which are the same as those of `D`.</span></span>

<span data-ttu-id="1e968-491">다음 예제에서는 람다 식을 실행 코드와 식 트리를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-491">The following example represents a lambda expression both as executable code and as an expression tree.</span></span> <span data-ttu-id="1e968-492">에 대 한 변환이 존재 하므로 `Func<int,int>`, 변환에도 존재 `Expression<Func<int,int>>`:</span><span class="sxs-lookup"><span data-stu-id="1e968-492">Because a conversion exists to `Func<int,int>`, a conversion also exists to `Expression<Func<int,int>>`:</span></span>

```csharp
Func<int,int> del = x => x + 1;                    // Code

Expression<Func<int,int>> exp = x => x + 1;        // Data
```

<span data-ttu-id="1e968-493">다음 이러한 할당을 대리자 `del` 반환 하는 메서드를 참조 `x + 1`, 및 식 트리 `exp` 식에 설명 하는 데이터 구조를 참조 `x => x + 1`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-493">Following these assignments, the delegate `del` references a method that returns `x + 1`, and the expression tree `exp` references a data structure that describes the expression `x => x + 1`.</span></span>

<span data-ttu-id="1e968-494">제네릭 형식의 정확한 정의 `Expression<D>` 람다 식을 식 트리 형식으로 변환 되 면 식 트리를 생성 하는 것에 대 한 정확한 규칙 뿐만 아니라 둘 다이 사양의 범위 밖에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-494">The exact definition of the generic type `Expression<D>` as well as the precise rules for constructing an expression tree when a lambda expression is converted to an expression tree type, are both outside the scope of this specification.</span></span>

<span data-ttu-id="1e968-495">두 가지가 명시적으로 만들어야 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-495">Two things are important to make explicit:</span></span>

*  <span data-ttu-id="1e968-496">모든 람다 식은 식 트리로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-496">Not all lambda expressions can be converted to expression trees.</span></span> <span data-ttu-id="1e968-497">예를 들어 문 본문을 사용 하 여 람다 식 및 할당을 포함 하는 람다 식을 나타낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-497">For instance, lambda expressions with statement bodies, and lambda expressions containing assignment expressions cannot be represented.</span></span> <span data-ttu-id="1e968-498">이러한 경우에 변환은 여전히 존재 하지만, 컴파일 시 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-498">In these cases, a conversion still exists, but will fail at compile-time.</span></span> <span data-ttu-id="1e968-499">이러한 예외에 자세히 나와 [익명 함수 변환](conversions.md#anonymous-function-conversions)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-499">These exceptions are detailed in [Anonymous function conversions](conversions.md#anonymous-function-conversions).</span></span>
*   <span data-ttu-id="1e968-500">`Expression<D>` 인스턴스 메서드를 제공 `Compile` 형식의 대리자를 생성 하는 `D`:</span><span class="sxs-lookup"><span data-stu-id="1e968-500">`Expression<D>` offers an instance method `Compile` which produces a delegate of type `D`:</span></span>

    ```csharp
    Func<int,int> del2 = exp.Compile();
    ```

    <span data-ttu-id="1e968-501">실행할 식 트리로 표시 되는 코드를 하면이 대리자를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-501">Invoking this delegate causes the code represented by the expression tree to be executed.</span></span> <span data-ttu-id="1e968-502">따라서 위의 정의 지정 del 및 del2은 동일 하며 다음 두 문이 같은 효과 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-502">Thus, given the definitions above, del and del2 are equivalent, and the following two statements will have the same effect:</span></span>

    ```csharp
    int i1 = del(1);
    
    int i2 = del2(1);
    ```

    <span data-ttu-id="1e968-503">이 코드를 실행 한 후 `i1` 하 고 `i2` 값을 모두 갖습니다 `2`합니다.</span><span class="sxs-lookup"><span data-stu-id="1e968-503">After executing this code,  `i1` and `i2` will both have the value `2`.</span></span>

