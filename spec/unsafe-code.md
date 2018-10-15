# <a name="unsafe-code"></a><span data-ttu-id="0de11-101">안전하지 않은 코드</span><span class="sxs-lookup"><span data-stu-id="0de11-101">Unsafe code</span></span>

<span data-ttu-id="0de11-102">핵심 C# 언어, 이전 장에서에 정의 된 대로 특히 C 및 c + +에서에서 다릅니다 포인터의 데이터 형식으로 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-102">The core C# language, as defined in the preceding chapters, differs notably from C and C++ in its omission of pointers as a data type.</span></span> <span data-ttu-id="0de11-103">대신 C# 제공 참조는 가비지 수집기에 의해 관리 되는 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-103">Instead, C# provides references and the ability to create objects that are managed by a garbage collector.</span></span> <span data-ttu-id="0de11-104">이 디자인에서는 다른 기능과 함께 사용 하면 C# C 또는 c + + 보다 훨씬 더 안전한 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-104">This design, coupled with other features, makes C# a much safer language than C or C++.</span></span> <span data-ttu-id="0de11-105">핵심 C# 언어에서 단순히 수 없는 초기화 되지 않은 변수, "현 수" 포인터 또는 배열 경계를 벗어난 인덱스 하는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-105">In the core C# language it is simply not possible to have an uninitialized variable, a "dangling" pointer, or an expression that indexes an array beyond its bounds.</span></span> <span data-ttu-id="0de11-106">버그의 전체 범주 C도 정기적으로 영향을 줄 및 c + + 프로그램 따라서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-106">Whole categories of bugs that routinely plague C and C++ programs are thus eliminated.</span></span>

<span data-ttu-id="0de11-107">C 또는 c + +의 거의 모든 포인터 형식 구조는 C#에서 참조 형식을 해당 사용자, 그럼에도 불구 하 고 가지 포인터 형식에 대 한 액세스 필요 되는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-107">While practically every pointer type construct in C or C++ has a reference type counterpart in C#, nonetheless, there are situations where access to pointer types becomes a necessity.</span></span> <span data-ttu-id="0de11-108">예를 들어, 기본 운영 체제와 상호 작용 하는 메모리 매핑된 장치에 액세스, 시간이 중요 한 알고리즘을 구현 아닐 포인터에 액세스 하지 않고도 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-108">For example, interfacing with the underlying operating system, accessing a memory-mapped device, or implementing a time-critical algorithm may not be possible or practical without access to pointers.</span></span> <span data-ttu-id="0de11-109">이 요구를 해결 하기 위해 C# 기능을 제공 작성할 ***안전 하지 않은 코드***합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-109">To address this need, C# provides the ability to write ***unsafe code***.</span></span>

<span data-ttu-id="0de11-110">안전 하지 않은 코드에서 선언에 대 한 포인터를 포인터 및 변수의 주소를 정수 계열 형식 간의 변환을 수행할 작동 및 등을 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-110">In unsafe code it is possible to declare and operate on pointers, to perform conversions between pointers and integral types, to take the address of variables, and so forth.</span></span> <span data-ttu-id="0de11-111">어떤 의미에서 안전 하지 않은 코드를 작성은 매우 C# 프로그램에서 C 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-111">In a sense, writing unsafe code is much like writing C code within a C# program.</span></span>

<span data-ttu-id="0de11-112">안전 하지 않은 코드는 실제로 개발자와 사용자의 관점에서 "안전한" 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-112">Unsafe code is in fact a "safe" feature from the perspective of both developers and users.</span></span> <span data-ttu-id="0de11-113">한정자를 사용 하 여 안전 하지 않은 코드를 명확 하 게 표시 해야 `unsafe`개발자 안전 하지 않은 기능은 사용할 수 없습니다. 실수로, 및 실행 엔진은 신뢰할 수 없는 환경에서 안전 하지 않은 코드를 실행할 수 없습니다 확인 하 게 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-113">Unsafe code must be clearly marked with the modifier `unsafe`, so developers can't possibly use unsafe features accidentally, and the execution engine works to ensure that unsafe code cannot be executed in an untrusted environment.</span></span>

## <a name="unsafe-contexts"></a><span data-ttu-id="0de11-114">안전 하지 않은 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="0de11-114">Unsafe contexts</span></span>

<span data-ttu-id="0de11-115">C#의 안전 하지 않은 기능은 안전 하지 않은 컨텍스트에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-115">The unsafe features of C# are available only in unsafe contexts.</span></span> <span data-ttu-id="0de11-116">안전 하지 않은 컨텍스트를 포함 하 여 도입 되는 `unsafe` 형식 또는 멤버의 또는 사용 하 여 선언에서 한정자를 *unsafe_statement*:</span><span class="sxs-lookup"><span data-stu-id="0de11-116">An unsafe context is introduced by including an `unsafe` modifier in the declaration of a type or member, or by employing an *unsafe_statement*:</span></span>

*  <span data-ttu-id="0de11-117">클래스, 구조체, 인터페이스 또는 대리자의 선언 포함 될 수 있습니다는 `unsafe` 한정자가 있는 경우 해당 형식 선언 (클래스, 구조체 또는 인터페이스의 본문 포함)의 전체 텍스트 범위가 안전 하지 않은 컨텍스트 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-117">A declaration of a class, struct, interface, or delegate may include an `unsafe` modifier, in which case the entire textual extent of that type declaration (including the body of the class, struct, or interface) is considered an unsafe context.</span></span>
*  <span data-ttu-id="0de11-118">필드, 메서드, 속성, 이벤트, 인덱서, 연산자, 인스턴스 생성자, 소멸자 또는 정적 생성자의 선언은 수는 `unsafe` 한정자가 있는 경우 해당 멤버 선언의 전체 텍스트 범위가 안전 하지 않은 비율은 컨텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-118">A declaration of a field, method, property, event, indexer, operator, instance constructor, destructor, or static constructor may include an `unsafe` modifier, in which case the entire textual extent of that member declaration is considered an unsafe context.</span></span>
*  <span data-ttu-id="0de11-119">*unsafe_statement* 내에서 안전 하지 않은 컨텍스트를 사용 하도록 설정 된 *블록*합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-119">An *unsafe_statement* enables the use of an unsafe context within a *block*.</span></span> <span data-ttu-id="0de11-120">연결 된 전체 텍스트 범위가 *블록* 안전 하지 않은 컨텍스트 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-120">The entire textual extent of the associated *block* is considered an unsafe context.</span></span>

<span data-ttu-id="0de11-121">연결 된 문법 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-121">The associated grammar productions are shown below.</span></span>

```antlr
class_modifier_unsafe
    : 'unsafe'
    ;

struct_modifier_unsafe
    : 'unsafe'
    ;

interface_modifier_unsafe
    : 'unsafe'
    ;

delegate_modifier_unsafe
    : 'unsafe'
    ;

field_modifier_unsafe
    : 'unsafe'
    ;

method_modifier_unsafe
    : 'unsafe'
    ;

property_modifier_unsafe
    : 'unsafe'
    ;

event_modifier_unsafe
    : 'unsafe'
    ;

indexer_modifier_unsafe
    : 'unsafe'
    ;

operator_modifier_unsafe
    : 'unsafe'
    ;

constructor_modifier_unsafe
    : 'unsafe'
    ;

destructor_declaration_unsafe
    : attributes? 'extern'? 'unsafe'? '~' identifier '(' ')' destructor_body
    | attributes? 'unsafe'? 'extern'? '~' identifier '(' ')' destructor_body
    ;

static_constructor_modifiers_unsafe
    : 'extern'? 'unsafe'? 'static'
    | 'unsafe'? 'extern'? 'static'
    | 'extern'? 'static' 'unsafe'?
    | 'unsafe'? 'static' 'extern'?
    | 'static' 'extern'? 'unsafe'?
    | 'static' 'unsafe'? 'extern'?
    ;

embedded_statement_unsafe
    : unsafe_statement
    | fixed_statement
    ;

unsafe_statement
    : 'unsafe' block
    ;
```

<span data-ttu-id="0de11-122">예제</span><span class="sxs-lookup"><span data-stu-id="0de11-122">In the example</span></span>

```csharp
public unsafe struct Node
{
    public int Value;
    public Node* Left;
    public Node* Right;
}
```

<span data-ttu-id="0de11-123">`unsafe` 한정자 구조체 선언에 지정 하면 전체 텍스트 범위가 안전 하지 않은 컨텍스트 되도록 구조체 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-123">the `unsafe` modifier specified in the struct declaration causes the entire textual extent of the struct declaration to become an unsafe context.</span></span> <span data-ttu-id="0de11-124">즉, 선언할 수는 `Left` 및 `Right` 필드는 포인터 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-124">Thus, it is possible to declare the `Left` and `Right` fields to be of a pointer type.</span></span> <span data-ttu-id="0de11-125">위의 예제를 작성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-125">The example above could also be written</span></span>

```csharp
public struct Node
{
    public int Value;
    public unsafe Node* Left;
    public unsafe Node* Right;
}
```

<span data-ttu-id="0de11-126">여기서는 `unsafe` 필드 선언에는 한정자로 인해 해당 선언이 안전 하지 않은 컨텍스트를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-126">Here, the `unsafe` modifiers in the field declarations cause those declarations to be considered unsafe contexts.</span></span>

<span data-ttu-id="0de11-127">포인터 형식의 사용을 허용 하므로 안전 하지 않은 컨텍스트를 설정 하는 `unsafe` 한정자는 형식 또는 멤버에 대 한 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-127">Other than establishing an unsafe context, thus permitting the use of pointer types, the `unsafe` modifier has no effect on a type or a member.</span></span> <span data-ttu-id="0de11-128">예제</span><span class="sxs-lookup"><span data-stu-id="0de11-128">In the example</span></span>

```csharp
public class A
{
    public unsafe virtual void F() {
        char* p;
        ...
    }
}

public class B: A
{
    public override void F() {
        base.F();
        ...
    }
}
```

<span data-ttu-id="0de11-129">`unsafe` 한정자를 `F` 에서 메서드 `A` 하면 다음의 텍스트 범위가 `F` 언어의 안전 하지 않은 기능을 사용할 수 있는 안전 하지 않은 컨텍스트를 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-129">the `unsafe` modifier on the `F` method in `A` simply causes the textual extent of `F` to become an unsafe context in which the unsafe features of the language can be used.</span></span> <span data-ttu-id="0de11-130">재정의 `F` 에 `B`를 다시 지정 하지 않아도 됩니다는 `unsafe` 한정자-하지 않는 한, 물론를 `F` 에서 메서드 `B` 안전 하지 않은 기능에 대 한 액세스를 해야 하는 자체.</span><span class="sxs-lookup"><span data-stu-id="0de11-130">In the override of `F` in `B`, there is no need to re-specify the `unsafe` modifier -- unless, of course, the `F` method in `B` itself needs access to unsafe features.</span></span>

<span data-ttu-id="0de11-131">포인터 형식에 메서드 시그니처의 일부로 경우 상황은 약간 다른</span><span class="sxs-lookup"><span data-stu-id="0de11-131">The situation is slightly different when a pointer type is part of the method's signature</span></span>

```csharp
public unsafe class A
{
    public virtual void F(char* p) {...}
}

public class B: A
{
    public unsafe override void F(char* p) {...}
}
```

<span data-ttu-id="0de11-132">여기에 있으므로 `F`의 서명 포인터 형식에만 쓸 수 있습니다 안전 하지 않은 컨텍스트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-132">Here, because `F`'s signature includes a pointer type, it can only be written in an unsafe context.</span></span> <span data-ttu-id="0de11-133">그러나 만들어 하거나 전체 클래스, 안전 하지 않은의 경우 처럼 안전 하지 않은 컨텍스트를 도입할 수 있습니다 `A`를 포함 하 여는 `unsafe` 메서드 선언에서 한정자의 경우에서 마찬가지로 `B`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-133">However, the unsafe context can be introduced by either making the entire class unsafe, as is the case in `A`, or by including an `unsafe` modifier in the method declaration, as is the case in `B`.</span></span>

## <a name="pointer-types"></a><span data-ttu-id="0de11-134">포인터 형식</span><span class="sxs-lookup"><span data-stu-id="0de11-134">Pointer types</span></span>

<span data-ttu-id="0de11-135">안전 하지 않은 컨텍스트에서 *형식* ([형식](types.md)) 수는 *pointer_type* 뿐만 *value_type* 또는 *reference_type* .</span><span class="sxs-lookup"><span data-stu-id="0de11-135">In an unsafe context, a *type* ([Types](types.md)) may be a *pointer_type* as well as a *value_type* or a *reference_type*.</span></span> <span data-ttu-id="0de11-136">그러나를 *pointer_type* 에서 사용할 수도 있습니다는 `typeof` 식 ([익명 개체 생성 식을](expressions.md#anonymous-object-creation-expressions)) 안전 하지 않은 컨텍스트 외부에서 같이 사용법은 안전 하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-136">However, a *pointer_type* may also be used in a `typeof` expression ([Anonymous object creation expressions](expressions.md#anonymous-object-creation-expressions)) outside of an unsafe context as such usage is not unsafe.</span></span>

```antlr
type_unsafe
    : pointer_type
    ;
```

<span data-ttu-id="0de11-137">*pointer_type* 으로 기록 되는 *unmanaged_type* 또는 키워드 `void`뒤를 `*` 토큰:</span><span class="sxs-lookup"><span data-stu-id="0de11-137">A *pointer_type* is written as an *unmanaged_type* or the keyword `void`, followed by a `*` token:</span></span>

```antlr
pointer_type
    : unmanaged_type '*'
    | 'void' '*'
    ;

unmanaged_type
    : type
    ;
```

<span data-ttu-id="0de11-138">전에 지정 된 형식 합니다 `*` 포인터에서 형식이 호출 됩니다 합니다 ***referent 형식을*** 포인터 형식의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-138">The type specified before the `*` in a pointer type is called the ***referent type*** of the pointer type.</span></span> <span data-ttu-id="0de11-139">포인터 형식의 값이 가리키는 변수의 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-139">It represents the type of the variable to which a value of the pointer type points.</span></span>

<span data-ttu-id="0de11-140">참조 (참조 형식의 값)와 달리 포인터는 가비지 수집기에 의해 추적 되지 않습니다-가비지 수집기는 포인터와 지점이 있는 데이터의 알지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-140">Unlike references (values of reference types), pointers are not tracked by the garbage collector -- the garbage collector has no knowledge of pointers and the data to which they point.</span></span> <span data-ttu-id="0de11-141">에 대 한 참조를 가리키도록 포인터이 따라서 허용 되지 않습니다 또는 구조체에 참조를 포함 하는 포인터의 참조 형식 이어야 합니다는 *unmanaged_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-141">For this reason a pointer is not permitted to point to a reference or to a struct that contains references, and the referent type of a pointer must be an *unmanaged_type*.</span></span>

<span data-ttu-id="0de11-142">*unmanaged_type* 는 없는 모든 형식을 *reference_type* 가 포함 되어 생성 된 형식, 또는 *reference_type* 또는 모든 수준에서 형식 필드를 생성 합니다. 중첩 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-142">An *unmanaged_type* is any type that isn't a *reference_type* or constructed type, and doesn't contain *reference_type* or constructed type fields at any level of nesting.</span></span> <span data-ttu-id="0de11-143">즉, 한 *unmanaged_type* 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-143">In other words, an *unmanaged_type* is one of the following:</span></span>

*  <span data-ttu-id="0de11-144">`sbyte``byte`, `short`, `ushort`, `int`, `uint`를 `long`, `ulong`, `char`, `float`를 `double`, `decimal`, 또는 `bool`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-144">`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, or `bool`.</span></span>
*  <span data-ttu-id="0de11-145">모든 *enum_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-145">Any *enum_type*.</span></span>
*  <span data-ttu-id="0de11-146">모든 *pointer_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-146">Any *pointer_type*.</span></span>
*  <span data-ttu-id="0de11-147">모든 사용자 정의 *struct_type* 생성 된 형식이 아닌 하의 필드를 포함 하 *unmanaged_type*만 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-147">Any user-defined *struct_type* that is not a constructed type and contains fields of *unmanaged_type*s only.</span></span>

<span data-ttu-id="0de11-148">포인터 및 참조를 혼합 하는 것에 대 한 직관적인 규칙 참조 (개체)의 참조 대상이 포인터를 포함 하도록 허용 되는 포인터의 참조 대상이 참조를 포함할 수 없습니다 경우</span><span class="sxs-lookup"><span data-stu-id="0de11-148">The intuitive rule for mixing of pointers and references is that referents of references (objects) are permitted to contain pointers, but referents of pointers are not permitted to contain references.</span></span>

<span data-ttu-id="0de11-149">포인터 형식의 몇 가지 예는 아래 표에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-149">Some examples of pointer types are given in the table below:</span></span>

| <span data-ttu-id="0de11-150">__예제__</span><span class="sxs-lookup"><span data-stu-id="0de11-150">__Example__</span></span> | <span data-ttu-id="0de11-151">__설명__</span><span class="sxs-lookup"><span data-stu-id="0de11-151">__Description__</span></span>                               |
|-------------|-----------------------------------------------|
| `byte*`     | <span data-ttu-id="0de11-152">에 대 한 포인터 `byte`</span><span class="sxs-lookup"><span data-stu-id="0de11-152">Pointer to `byte`</span></span>                             |
| `char*`     | <span data-ttu-id="0de11-153">에 대 한 포인터 `char`</span><span class="sxs-lookup"><span data-stu-id="0de11-153">Pointer to `char`</span></span>                             |
| `int**`     | <span data-ttu-id="0de11-154">에 대 한 포인터에 대 한 포인터 `int`</span><span class="sxs-lookup"><span data-stu-id="0de11-154">Pointer to pointer to `int`</span></span>                   |
| `int*[]`    | <span data-ttu-id="0de11-155">에 대 한 포인터의 1 차원 배열 `int`</span><span class="sxs-lookup"><span data-stu-id="0de11-155">Single-dimensional array of pointers to `int`</span></span> |
| `void*`     | <span data-ttu-id="0de11-156">알 수 없는 형식에 대 한 포인터</span><span class="sxs-lookup"><span data-stu-id="0de11-156">Pointer to unknown type</span></span>                       |

<span data-ttu-id="0de11-157">지정 된 구현에 대 한 모든 포인터 형식에 같은 크기 및 표현 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-157">For a given implementation, all pointer types must have the same size and representation.</span></span>

<span data-ttu-id="0de11-158">C 및 c + +, C#에서 동일한 선언에서 여러 포인터 선언 된 경우와 달리는 `*` 각 포인터 이름의 접두 문장 부호로 아니라 기본 형식에만 함께 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-158">Unlike C and C++, when multiple pointers are declared in the same declaration, in C# the `*` is written along with the underlying type only, not as a prefix punctuator on each pointer name.</span></span> <span data-ttu-id="0de11-159">예</span><span class="sxs-lookup"><span data-stu-id="0de11-159">For example</span></span>

```csharp
int* pi, pj;    // NOT as int *pi, *pj;
```

<span data-ttu-id="0de11-160">형식의 포인터 값 `T*` 형식의 변수에 대 한 주소를 나타내는 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-160">The value of a pointer having type `T*` represents the address of a variable of type `T`.</span></span> <span data-ttu-id="0de11-161">포인터 간접 참조 연산자 `*` ([포인터 간접 참조](unsafe-code.md#pointer-indirection))에서이 변수에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-161">The pointer indirection operator `*` ([Pointer indirection](unsafe-code.md#pointer-indirection)) may be used to access this variable.</span></span> <span data-ttu-id="0de11-162">예를 들어 변수를 지정 `P` 형식의 `int*`, 식이 `*P` 나타냅니다 합니다 `int` 에 포함 된 주소에 있는 변수 `P`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-162">For example, given a variable `P` of type `int*`, the expression `*P` denotes the `int` variable found at the address contained in `P`.</span></span>

<span data-ttu-id="0de11-163">개체 참조와 같은 포인터 수 `null`입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-163">Like an object reference, a pointer may be `null`.</span></span> <span data-ttu-id="0de11-164">간접 참조 연산자를 적용 한 `null` 포인터 구현 시 정의 된 동작이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-164">Applying the indirection operator to a `null` pointer results in implementation-defined behavior.</span></span> <span data-ttu-id="0de11-165">값을 사용 하 여 포인터 `null` 모든 비트가 0으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-165">A pointer with value `null` is represented by all-bits-zero.</span></span>

<span data-ttu-id="0de11-166">`void*` 형식은 알 수 없는 형식에 대 한 포인터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-166">The `void*` type represents a pointer to an unknown type.</span></span> <span data-ttu-id="0de11-167">Referent 형식을 알려진 아니므로 형식의 포인터에 간접 참조 연산자를 적용할 수 없습니다 `void*`, 또는에서 이러한 포인터 산술 연산을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-167">Because the referent type is unknown, the indirection operator cannot be applied to a pointer of type `void*`, nor can any arithmetic be performed on such a pointer.</span></span> <span data-ttu-id="0de11-168">그러나 형식의 포인터 `void*` 다른 포인터 형식 (또는 그 반대로) 캐스팅 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-168">However, a pointer of type `void*` can be cast to any other pointer type (and vice versa).</span></span>

<span data-ttu-id="0de11-169">포인터 형식은 형식의 별도 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-169">Pointer types are a separate category of types.</span></span> <span data-ttu-id="0de11-170">참조 형식 및 값 형식의 경우와 달리 포인터 형식에서 상속 하지 않습니다 `object` 포인터 형식 간의 변환이 존재 하 고 `object`입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-170">Unlike reference types and value types, pointer types do not inherit from `object` and no conversions exist between pointer types and `object`.</span></span> <span data-ttu-id="0de11-171">특히, boxing 및 unboxing ([Boxing 및 unboxing](types.md#boxing-and-unboxing)) 포인터에 대 한 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-171">In particular, boxing and unboxing ([Boxing and unboxing](types.md#boxing-and-unboxing)) are not supported for pointers.</span></span> <span data-ttu-id="0de11-172">그러나 포인터 형식과 정수 계열 형식 간 및 서로 다른 포인터 형식 간에 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-172">However, conversions are permitted between different pointer types and between pointer types and the integral types.</span></span> <span data-ttu-id="0de11-173">에 설명 되어 [포인터 변환](unsafe-code.md#pointer-conversions)합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-173">This is described in [Pointer conversions](unsafe-code.md#pointer-conversions).</span></span>

<span data-ttu-id="0de11-174">A *pointer_type* 형식 인수로 사용할 수 없습니다 ([형식 생성](types.md#constructed-types))과 형식 유추 ([형식 유추](expressions.md#type-inference)) 유추 있어야 하는 제네릭 메서드 호출에서 실패를 형식 인수는 포인터 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-174">A *pointer_type* cannot be used as a type argument ([Constructed types](types.md#constructed-types)), and type inference ([Type inference](expressions.md#type-inference)) fails on generic method calls that would have inferred a type argument to be a pointer type.</span></span>

<span data-ttu-id="0de11-175">A *pointer_type* volatile 필드의 형식으로 사용할 수 있습니다 ([Volatile 필드](classes.md#volatile-fields)).</span><span class="sxs-lookup"><span data-stu-id="0de11-175">A *pointer_type* may be used as the type of a volatile field ([Volatile fields](classes.md#volatile-fields)).</span></span>

<span data-ttu-id="0de11-176">포인터로 전달 될 수 있지만 `ref` 또는 `out` 매개 변수를 이렇게 포인터도 수 있으므로 정의 되지 않은 동작이 발생할 수 없습니다 더 이상 호출된 된 메서드가 반환 될 때 존재 하는 지역 변수 또는 고정된 하는 개체를 가리키도록 설정 지점에 사용 되는, 더 이상 고정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-176">Although pointers can be passed as `ref` or `out` parameters, doing so can cause undefined behavior, since the pointer may well be set to point to a local variable which no longer exists when the called method returns, or the fixed object to which it used to point, is no longer fixed.</span></span> <span data-ttu-id="0de11-177">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="0de11-177">For example:</span></span>

```csharp
using System;

class Test
{
    static int value = 20;

    unsafe static void F(out int* pi1, ref int* pi2) {
        int i = 10;
        pi1 = &i;

        fixed (int* pj = &value) {
            // ...
            pi2 = pj;
        }
    }

    static void Main() {
        int i = 10;
        unsafe {
            int* px1;
            int* px2 = &i;

            F(out px1, ref px2);

            Console.WriteLine("*px1 = {0}, *px2 = {1}",
                *px1, *px2);    // undefined behavior
        }
    }
}
```

<span data-ttu-id="0de11-178">메서드가 일부 형식의 값을 반환할 수 및 해당 형식에 대 한 포인터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-178">A method can return a value of some type, and that type can be a pointer.</span></span> <span data-ttu-id="0de11-179">예를 들어의 연속 시퀀스에 대 한 포인터를 지정 하는 경우 `int`s, 해당 시퀀스의 요소 수 및 일부 기타 `int` 값 일치 하는 경우 다음 메서드는 시퀀스의 해당 값의 주소를 반환, 그렇지 않으면 를반환합니다`null`:</span><span class="sxs-lookup"><span data-stu-id="0de11-179">For example, when given a pointer to a contiguous sequence of `int`s, that sequence's element count, and some other `int` value, the following method returns the address of that value in that sequence, if a match occurs; otherwise it returns `null`:</span></span>

```csharp
unsafe static int* Find(int* pi, int size, int value) {
    for (int i = 0; i < size; ++i) {
        if (*pi == value) 
            return pi;
        ++pi;
    }
    return null;
}
```

<span data-ttu-id="0de11-180">안전 하지 않은 컨텍스트에서 다양 한 구문을 포인터 연산에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-180">In an unsafe context, several constructs are available for operating on pointers:</span></span>

*  <span data-ttu-id="0de11-181">합니다 `*` 연산자는 포인터 간접 참조 하는 데 사용할 수 있습니다 ([포인터 간접 참조](unsafe-code.md#pointer-indirection)).</span><span class="sxs-lookup"><span data-stu-id="0de11-181">The `*` operator may be used to perform pointer indirection ([Pointer indirection](unsafe-code.md#pointer-indirection)).</span></span>
*  <span data-ttu-id="0de11-182">합니다 `->` 포인터를 통해 구조체의 멤버에 액세스 하려면 연산자를 사용할 수 있습니다 ([포인터 멤버 액세스](unsafe-code.md#pointer-member-access)).</span><span class="sxs-lookup"><span data-stu-id="0de11-182">The `->` operator may be used to access a member of a struct through a pointer ([Pointer member access](unsafe-code.md#pointer-member-access)).</span></span>
*  <span data-ttu-id="0de11-183">합니다 `[]` 포인터 인덱싱 연산자를 사용할 수 있습니다 ([포인터 요소 액세스](unsafe-code.md#pointer-element-access)).</span><span class="sxs-lookup"><span data-stu-id="0de11-183">The `[]` operator may be used to index a pointer ([Pointer element access](unsafe-code.md#pointer-element-access)).</span></span>
*  <span data-ttu-id="0de11-184">합니다 `&` 연산자는 변수에 대 한 주소를 가져오는 데 사용할 수 있습니다 ([address-of 연산자](unsafe-code.md#the-address-of-operator)).</span><span class="sxs-lookup"><span data-stu-id="0de11-184">The `&` operator may be used to obtain the address of a variable ([The address-of operator](unsafe-code.md#the-address-of-operator)).</span></span>
*  <span data-ttu-id="0de11-185">합니다 `++` 하 고 `--` 포인터 증가 및 감소 연산자를 사용할 수 있습니다 ([포인터 증가 및 감소](unsafe-code.md#pointer-increment-and-decrement)).</span><span class="sxs-lookup"><span data-stu-id="0de11-185">The `++` and `--` operators may be used to increment and decrement pointers ([Pointer increment and decrement](unsafe-code.md#pointer-increment-and-decrement)).</span></span>
*  <span data-ttu-id="0de11-186">합니다 `+` 하 고 `-` 포인터 산술 연산을 수행 하는 연산자를 사용할 수 있습니다 ([포인터 산술 연산을](unsafe-code.md#pointer-arithmetic)).</span><span class="sxs-lookup"><span data-stu-id="0de11-186">The `+` and `-` operators may be used to perform pointer arithmetic ([Pointer arithmetic](unsafe-code.md#pointer-arithmetic)).</span></span>
*  <span data-ttu-id="0de11-187">합니다 `==`, `!=`를 `<`, `>`를 `<=`, 및 `=>` 연산자를 사용 하 여 포인터를 비교할 수 있습니다 ([포인터 비교](unsafe-code.md#pointer-comparison)).</span><span class="sxs-lookup"><span data-stu-id="0de11-187">The `==`, `!=`, `<`, `>`, `<=`, and `=>` operators may be used to compare pointers ([Pointer comparison](unsafe-code.md#pointer-comparison)).</span></span>
*  <span data-ttu-id="0de11-188">합니다 `stackalloc` 연산자를 사용 하 여 호출 스택에서 메모리를 할당할 수 있습니다 ([고정 크기 버퍼](unsafe-code.md#fixed-size-buffers)).</span><span class="sxs-lookup"><span data-stu-id="0de11-188">The `stackalloc` operator may be used to allocate memory from the call stack ([Fixed size buffers](unsafe-code.md#fixed-size-buffers)).</span></span>
*  <span data-ttu-id="0de11-189">합니다 `fixed` 문은 일시적으로 변수를 수정 하므로 해당 주소를 가져올 수 있습니다 데 사용할 수 있습니다 ([fixed 문을](unsafe-code.md#the-fixed-statement)).</span><span class="sxs-lookup"><span data-stu-id="0de11-189">The `fixed` statement may be used to temporarily fix a variable so its address can be obtained ([The fixed statement](unsafe-code.md#the-fixed-statement)).</span></span>

## <a name="fixed-and-moveable-variables"></a><span data-ttu-id="0de11-190">고정 및 고정 되지 않은 변수</span><span class="sxs-lookup"><span data-stu-id="0de11-190">Fixed and moveable variables</span></span>

<span data-ttu-id="0de11-191">Address-of 연산자 ([address-of 연산자](unsafe-code.md#the-address-of-operator)) 및 `fixed` 문 ([fixed 문을](unsafe-code.md#the-fixed-statement)) 변수 두 가지 범주로 나눌: ***변수고정***하 고 ***이동 가능한 변수***합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-191">The address-of operator ([The address-of operator](unsafe-code.md#the-address-of-operator)) and the `fixed` statement ([The fixed statement](unsafe-code.md#the-fixed-statement)) divide variables into two categories: ***Fixed variables*** and ***moveable variables***.</span></span>

<span data-ttu-id="0de11-192">고정된 변수 가비지 수집기의 작업에 의해 영향을 받지 않는 저장소 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-192">Fixed variables reside in storage locations that are unaffected by operation of the garbage collector.</span></span> <span data-ttu-id="0de11-193">(고정 변수의 예로 지역 변수, 값 매개 변수 및 포인터를 역참조 하 여 만든 변수.) 다른 한편으로 고정 되지 않은 변수 재배치 또는 가비지 수집기에 의해 삭제 될 수 있는 저장소 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-193">(Examples of fixed variables include local variables, value parameters, and variables created by dereferencing pointers.) On the other hand, moveable variables reside in storage locations that are subject to relocation or disposal by the garbage collector.</span></span> <span data-ttu-id="0de11-194">(고정 되지 않은 변수의 예로 필드 개체 및 배열 요소에 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="0de11-194">(Examples of moveable variables include fields in objects and elements of arrays.)</span></span>

<span data-ttu-id="0de11-195">합니다 `&` 연산자 ([address-of 연산자](unsafe-code.md#the-address-of-operator)) 제한 없이 가져올 고정 변수의 주소를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-195">The `&` operator ([The address-of operator](unsafe-code.md#the-address-of-operator)) permits the address of a fixed variable to be obtained without restrictions.</span></span> <span data-ttu-id="0de11-196">그러나 변수인 재배치 또는 가비지 수집기에 의해 삭제 될 수 있습니다 이기 때문에 고정 되지 않은 변수에 대 한 주소만 가져올 수 있습니다 사용 하는 `fixed` 문 ([fixed 문을](unsafe-code.md#the-fixed-statement)), 및 해당 주소 해당 기간 동안에 `fixed` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-196">However, because a moveable variable is subject to relocation or disposal by the garbage collector, the address of a moveable variable can only be obtained using a `fixed` statement ([The fixed statement](unsafe-code.md#the-fixed-statement)), and that address remains valid only for the duration of that `fixed` statement.</span></span>

<span data-ttu-id="0de11-197">정확 하 게 말해에서 고정된 변수는 다음 중 하나:</span><span class="sxs-lookup"><span data-stu-id="0de11-197">In precise terms, a fixed variable is one of the following:</span></span>

*  <span data-ttu-id="0de11-198">결과에서 변수를 *simple_name* ([단순 이름](expressions.md#simple-names)) 참조 하는 지역 변수 또는 값 매개 변수는 익명 함수에 의해 캡처됩니다 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-198">A variable resulting from a *simple_name* ([Simple names](expressions.md#simple-names)) that refers to a local variable or a value parameter, unless the variable is captured by an anonymous function.</span></span>
*  <span data-ttu-id="0de11-199">변수 결과 *member_access* ([멤버 액세스](expressions.md#member-access)) 형식의 `V.I`여기서 `V` 고정 변수입니다를 *struct_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-199">A variable resulting from a *member_access* ([Member access](expressions.md#member-access)) of the form `V.I`, where `V` is a fixed variable of a *struct_type*.</span></span>
*  <span data-ttu-id="0de11-200">결과에서 변수를 *pointer_indirection_expression* ([포인터 간접 참조](unsafe-code.md#pointer-indirection)) 형식의 `*P`, *pointer_member_access* ([포인터 멤버 액세스](unsafe-code.md#pointer-member-access)) 형식의 `P->I`, 또는 *pointer_element_access* ([포인터 요소 액세스](unsafe-code.md#pointer-element-access)) 형식의 `P[E]`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-200">A variable resulting from a *pointer_indirection_expression* ([Pointer indirection](unsafe-code.md#pointer-indirection)) of the form `*P`, a *pointer_member_access* ([Pointer member access](unsafe-code.md#pointer-member-access)) of the form `P->I`, or a *pointer_element_access* ([Pointer element access](unsafe-code.md#pointer-element-access)) of the form `P[E]`.</span></span>

<span data-ttu-id="0de11-201">다른 모든 변수가 고정 되지 않은 변수도 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-201">All other variables are classified as moveable variables.</span></span>

<span data-ttu-id="0de11-202">정적 필드 변수인으로 분류 되는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-202">Note that a static field is classified as a moveable variable.</span></span> <span data-ttu-id="0de11-203">또한 한 `ref` 또는 `out` 매개 변수에 대해 지정 된 인수 변수는 고정 하는 경우에 매개 변수인으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-203">Also note that a `ref` or `out` parameter is classified as a moveable variable, even if the argument given for the parameter is a fixed variable.</span></span> <span data-ttu-id="0de11-204">마지막으로, 메모에 대 한 포인터를 역참조 하 여 생성 되는 변수는 항상 고정된 변수로으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-204">Finally, note that a variable produced by dereferencing a pointer is always classified as a fixed variable.</span></span>

## <a name="pointer-conversions"></a><span data-ttu-id="0de11-205">포인터 변환</span><span class="sxs-lookup"><span data-stu-id="0de11-205">Pointer conversions</span></span>

<span data-ttu-id="0de11-206">안전 하지 않은 컨텍스트에서만 사용할 수 있는 암시적 변환 집합 ([암시적 변환을](conversions.md#implicit-conversions)) 다음 암시적 포인터 변환을 포함 하도록 확장 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-206">In an unsafe context, the set of available implicit conversions ([Implicit conversions](conversions.md#implicit-conversions)) is extended to include the following implicit pointer conversions:</span></span>

*  <span data-ttu-id="0de11-207">모든 *pointer_type* 형식으로 `void*`입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-207">From any *pointer_type* to the type `void*`.</span></span>
*  <span data-ttu-id="0de11-208">`null` 에 리터럴 *pointer_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-208">From the `null` literal to any *pointer_type*.</span></span>

<span data-ttu-id="0de11-209">또한 안전 하지 않은 컨텍스트에서 사용할 수 있는 명시적 변환 집합 ([명시적 변환](conversions.md#explicit-conversions)) 다음과 같은 명시적 포인터 변환은 포함 하도록 확장 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-209">Additionally, in an unsafe context, the set of available explicit conversions ([Explicit conversions](conversions.md#explicit-conversions)) is extended to include the following explicit pointer conversions:</span></span>

*  <span data-ttu-id="0de11-210">모든 *pointer_type* 다른 *pointer_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-210">From any *pointer_type* to any other *pointer_type*.</span></span>
*  <span data-ttu-id="0de11-211">`sbyte`, `byte`, `short`, `ushort`를 `int`를 `uint`를 `long`, 또는 `ulong` 에 *pointer_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-211">From `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, or `ulong` to any *pointer_type*.</span></span>
*  <span data-ttu-id="0de11-212">*pointer_type* 하 `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`를 `long`, 또는 `ulong`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-212">From any *pointer_type* to `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, or `ulong`.</span></span>

<span data-ttu-id="0de11-213">안전 하지 않은 컨텍스트 표준 암시적 변환 집합에서 마지막으로 ([표준 암시적 변환이](conversions.md#standard-implicit-conversions)) 다음과 같은 포인터 변환에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-213">Finally, in an unsafe context, the set of standard implicit conversions ([Standard implicit conversions](conversions.md#standard-implicit-conversions)) includes the following pointer conversion:</span></span>

*  <span data-ttu-id="0de11-214">모든 *pointer_type* 형식으로 `void*`입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-214">From any *pointer_type* to the type `void*`.</span></span>

<span data-ttu-id="0de11-215">두 포인터 형식 간의 변환에는 실제 포인터 값은 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-215">Conversions between two pointer types never change the actual pointer value.</span></span> <span data-ttu-id="0de11-216">즉, 다른 하나는 포인터 형식에서 변환 포인터에 의해 제공 된 기본 주소에 영향을 주지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-216">In other words, a conversion from one pointer type to another has no effect on the underlying address given by the pointer.</span></span>

<span data-ttu-id="0de11-217">포인터 형식으로 변환할 때 다른 결과 포인터를 가리키는 형식에 대해 올바르게 정렬 되지 않은 경우에 결과 역참조 하는 경우 동작이 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-217">When one pointer type is converted to another, if the resulting pointer is not correctly aligned for the pointed-to type, the behavior is undefined if the result is dereferenced.</span></span> <span data-ttu-id="0de11-218">일반적으로 "올바르게 정렬 된" 개념은 전이적: 경우 입력에 대 한 포인터 `A` 입력에 대 한 포인터에 대 한 올바르게 정렬 될 `B`는 차례로 올바르게 맞춰진 입력에 대 한 포인터에 대 한 `C`, 다음에 대 한 포인터 형식 `A`형식의 포인터에 대 한 올바르게 맞춰진 `C`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-218">In general, the concept "correctly aligned" is transitive: if a pointer to type `A` is correctly aligned for a pointer to type `B`, which, in turn, is correctly aligned for a pointer to type `C`, then a pointer to type `A` is correctly aligned for a pointer to type `C`.</span></span>

<span data-ttu-id="0de11-219">다른 형식에 대 한 포인터를 통해 액세스 한 형식이 있는 변수는 다음과 같은 경우를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-219">Consider the following case in which a variable having one type is accessed via a pointer to a different type:</span></span>

```csharp
char c = 'A';
char* pc = &c;
void* pv = pc;
int* pi = (int*)pv;
int i = *pi;         // undefined
*pi = 123456;        // undefined
```

<span data-ttu-id="0de11-220">포인터 형식 변환 되 면 바이트에 대 한 포인터는 변수의 최하위 주소 지정된 바이트를 결과 지점.</span><span class="sxs-lookup"><span data-stu-id="0de11-220">When a pointer type is converted to a pointer to byte, the result points to the lowest addressed byte of the variable.</span></span> <span data-ttu-id="0de11-221">변수의 크기를 최대 결과의 연속적 증분 해당 변수의 나머지 바이트에 대 한 포인터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-221">Successive increments of the result, up to the size of the variable, yield pointers to the remaining bytes of that variable.</span></span> <span data-ttu-id="0de11-222">예를 들어, 다음에 메서드가 표시 각 8 바이트는 double 값을 16 진수 값으로:</span><span class="sxs-lookup"><span data-stu-id="0de11-222">For example, the following method displays each of the eight bytes in a double as a hexadecimal value:</span></span>

```csharp
using System;

class Test
{
    unsafe static void Main() {
      double d = 123.456e23;
        unsafe {
           byte* pb = (byte*)&d;
            for (int i = 0; i < sizeof(double); ++i)
               Console.Write("{0:X2} ", *pb++);
            Console.WriteLine();
        }
    }
}
```

<span data-ttu-id="0de11-223">물론, 생성 된 출력 엔디언에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-223">Of course, the output produced depends on endianness.</span></span>

<span data-ttu-id="0de11-224">포인터와 정수 간의 매핑을 구현 시 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-224">Mappings between pointers and integers are implementation-defined.</span></span> <span data-ttu-id="0de11-225">그러나 32에서 \* 선형 주소 공간을 사용 하는 64 비트 CPU 아키텍처, 정수 계열 형식에서 포인터의 변환은 일반적으로 처럼 정확 하 게 변환을 `uint` 또는 `ulong` 값을 각각 해당 정수 계열 형식에서입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-225">However, on 32\* and 64-bit CPU architectures with a linear address space, conversions of pointers to or from integral types typically behave exactly like conversions of `uint` or `ulong` values, respectively, to or from those integral types.</span></span>

### <a name="pointer-arrays"></a><span data-ttu-id="0de11-226">포인터 배열</span><span class="sxs-lookup"><span data-stu-id="0de11-226">Pointer arrays</span></span>

<span data-ttu-id="0de11-227">안전 하지 않은 컨텍스트에서 포인터 배열은 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-227">In an unsafe context, arrays of pointers can be constructed.</span></span> <span data-ttu-id="0de11-228">다른 배열 형식에 적용 되는 변환 중 일부만 대 한 포인터 배열에서 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-228">Only some of the conversions that apply to other array types are allowed on pointer arrays:</span></span>

*  <span data-ttu-id="0de11-229">암시적 참조 변환을 ([암시적 참조 변환을](conversions.md#implicit-reference-conversions))에서 *array_type* 에 `System.Array` 도 구현 하는 인터페이스 포인터 배열에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-229">The implicit reference conversion ([Implicit reference conversions](conversions.md#implicit-reference-conversions)) from any *array_type* to `System.Array` and the interfaces it implements also applies to pointer arrays.</span></span> <span data-ttu-id="0de11-230">그러나 통해 배열 요소에 액세스 하려고 `System.Array` 하거나, 포인터 형식으로 변환 될으로 구현 하는 인터페이스에서 런타임 시 예외를 발생 하면 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-230">However, any attempt to access the array elements through `System.Array` or the interfaces it implements will result in an exception at run-time, as pointer types are not convertible to `object`.</span></span>
*  <span data-ttu-id="0de11-231">암시적 및 명시적 참조 변환을 ([암시적 참조 변환을](conversions.md#implicit-reference-conversions), [명시적 참조 변환이](conversions.md#explicit-reference-conversions))는 1 차원 배열 형식에서 `S[]` 에 `System.Collections.Generic.IList<T>` 및 제네릭 기본 인터페이스로 적용 하지는 않습니다 포인터 배열의 포인터 형식은 형식 인수로 사용할 수 없습니다 및 포인터가 아닌 형식에 대 한 포인터 형식에서 변환이 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-231">The implicit and explicit reference conversions ([Implicit reference conversions](conversions.md#implicit-reference-conversions), [Explicit reference conversions](conversions.md#explicit-reference-conversions)) from a single-dimensional array type `S[]` to `System.Collections.Generic.IList<T>` and its generic base interfaces never apply to pointer arrays, since pointer types cannot be used as type arguments, and there are no conversions from pointer types to non-pointer types.</span></span>
*  <span data-ttu-id="0de11-232">명시적 참조 변환이 ([명시적 참조 변환을](conversions.md#explicit-reference-conversions))에서 `System.Array` 인터페이스를 구현 하 고 *array_type* 포인터 배열에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-232">The explicit reference conversion ([Explicit reference conversions](conversions.md#explicit-reference-conversions)) from `System.Array` and the interfaces it implements to any *array_type* applies to pointer arrays.</span></span>
*  <span data-ttu-id="0de11-233">명시적 참조 변환을 ([명시적 참조 변환을](conversions.md#explicit-reference-conversions))에서 `System.Collections.Generic.IList<S>` 는 1 차원 배열 형식에 기본 인터페이스 및 `T[]` 포인터 형식 수 없으므로 포인터 배열에 적용 되지 않습니다 사용 되는 인수 형식 및 포인터가 아닌 형식에 대 한 포인터 형식에서 변환이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-233">The explicit reference conversions ([Explicit reference conversions](conversions.md#explicit-reference-conversions)) from `System.Collections.Generic.IList<S>` and its base interfaces to a single-dimensional array type `T[]` never applies to pointer arrays, since pointer types cannot be used as type arguments, and there are no conversions from pointer types to non-pointer types.</span></span>

<span data-ttu-id="0de11-234">이러한 제한에 대 한 확장 함을 의미 합니다 `foreach` 에 설명 된 배열에 대 문을 [foreach 문을](statements.md#the-foreach-statement) 포인터 배열에 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-234">These restrictions mean that the expansion for the `foreach` statement over arrays described in [The foreach statement](statements.md#the-foreach-statement) cannot be applied to pointer arrays.</span></span> <span data-ttu-id="0de11-235">대신, 폼의 foreach 문을</span><span class="sxs-lookup"><span data-stu-id="0de11-235">Instead, a foreach statement of the form</span></span>

```csharp
foreach (V v in x) embedded_statement
```

<span data-ttu-id="0de11-236">여기서 형식의 `x` 형식의 배열 형식인 `T[,,...,]`, `N` 차원에서 1 뺀 수는 및 `T` 또는 `V` 포인터 형식이, 중첩 된 for 루프를 사용 하 여 다음과 같이 확장 됩니다:</span><span class="sxs-lookup"><span data-stu-id="0de11-236">where the type of `x` is an array type of the form `T[,,...,]`, `N` is the number of dimensions minus 1 and `T` or `V` is a pointer type, is expanded using nested for-loops as follows:</span></span>

```csharp
{
    T[,,...,] a = x;
    for (int i0 = a.GetLowerBound(0); i0 <= a.GetUpperBound(0); i0++)
    for (int i1 = a.GetLowerBound(1); i1 <= a.GetUpperBound(1); i1++)
    ...
    for (int iN = a.GetLowerBound(N); iN <= a.GetUpperBound(N); iN++) {
        V v = (V)a.GetValue(i0,i1,...,iN);
        embedded_statement
    }
}
```

<span data-ttu-id="0de11-237">변수 `a`, `i0`를 `i1`,..., `iN` 에 표시 하거나 액세스할 수 없는지 `x` 또는 *embedded_statement* 또는 프로그램의 다른 소스 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-237">The variables `a`, `i0`, `i1`, ..., `iN` are not visible to or accessible to `x` or the *embedded_statement* or any other source code of the program.</span></span> <span data-ttu-id="0de11-238">변수의 `v` 포함 된 문에서 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-238">The variable `v` is read-only in the embedded statement.</span></span> <span data-ttu-id="0de11-239">명시적 변환이 없는 경우 ([포인터 변환](unsafe-code.md#pointer-conversions))에서 `T` (요소 형식)를 `V`오류가 생성 되 고 추가 단계가 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-239">If there is not an explicit conversion ([Pointer conversions](unsafe-code.md#pointer-conversions)) from `T` (the element type) to `V`, an error is produced and no further steps are taken.</span></span> <span data-ttu-id="0de11-240">하는 경우 `x` 기본값이 `null`, `System.NullReferenceException` 런타임에 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-240">If `x` has the value `null`, a `System.NullReferenceException` is thrown at run-time.</span></span>

## <a name="pointers-in-expressions"></a><span data-ttu-id="0de11-241">식에 대 한 포인터</span><span class="sxs-lookup"><span data-stu-id="0de11-241">Pointers in expressions</span></span>

<span data-ttu-id="0de11-242">안전 하지 않은 컨텍스트에서 식을 포인터 형식의 결과 생성할 수 있습니다 이지만 안전 하지 않은 컨텍스트 외부 포인터 형식 이어야 하는 식에 대 한 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-242">In an unsafe context, an expression may yield a result of a pointer type, but outside an unsafe context it is a compile-time error for an expression to be of a pointer type.</span></span> <span data-ttu-id="0de11-243">정확 하 게 말해에서 안전 하지 않은 컨텍스트 외부 컴파일 타임 오류가 발생 하는 경우 *simple_name* ([단순 이름](expressions.md#simple-names)), *member_access* ([멤버 액세스 ](expressions.md#member-access)), *invocation_expression* ([호출 식](expressions.md#invocation-expressions)), 또는 *element_access* ([요소 액세스](expressions.md#element-access))는 포인터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-243">In precise terms, outside an unsafe context a compile-time error occurs if any *simple_name* ([Simple names](expressions.md#simple-names)), *member_access* ([Member access](expressions.md#member-access)), *invocation_expression* ([Invocation expressions](expressions.md#invocation-expressions)), or *element_access* ([Element access](expressions.md#element-access)) is of a pointer type.</span></span>

<span data-ttu-id="0de11-244">안전 하지 않은 컨텍스트에서 *primary_no_array_creation_expression* ([기본 식](expressions.md#primary-expressions)) 및 *unary_expression* ([단항연산자](expressions.md#unary-operators)) 프로덕션에는 다음과 같은 추가 구문이 허용:</span><span class="sxs-lookup"><span data-stu-id="0de11-244">In an unsafe context, the *primary_no_array_creation_expression* ([Primary expressions](expressions.md#primary-expressions)) and *unary_expression* ([Unary operators](expressions.md#unary-operators)) productions permit the following additional constructs:</span></span>

```antlr
primary_no_array_creation_expression_unsafe
    : pointer_member_access
    | pointer_element_access
    | sizeof_expression
    ;

unary_expression_unsafe
    : pointer_indirection_expression
    | addressof_expression
    ;
```

<span data-ttu-id="0de11-245">이러한 구조는 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-245">These constructs are described in the following sections.</span></span> <span data-ttu-id="0de11-246">우선 순위 및 결합성 안전 하지 않은 연산자의 문법으로 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-246">The precedence and associativity of the unsafe operators is implied by the grammar.</span></span>

### <a name="pointer-indirection"></a><span data-ttu-id="0de11-247">포인터 간접 참조</span><span class="sxs-lookup"><span data-stu-id="0de11-247">Pointer indirection</span></span>

<span data-ttu-id="0de11-248">A *pointer_indirection_expression* 별표 이루어져 있습니다 (`*`) 뒤에 *unary_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-248">A *pointer_indirection_expression* consists of an asterisk (`*`) followed by a *unary_expression*.</span></span>

```antlr
pointer_indirection_expression
    : '*' unary_expression
    ;
```

<span data-ttu-id="0de11-249">단항 `*` 연산자를 포인터 간접 참조를 나타냅니다. 포인터를 가리키는 변수를 가져오는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-249">The unary `*` operator denotes pointer indirection and is used to obtain the variable to which a pointer points.</span></span> <span data-ttu-id="0de11-250">평가 결과 `*P`여기서 `P` 포인터 형식의 식이 `T*`, 형식의 변수가 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-250">The result of evaluating `*P`, where `P` is an expression of a pointer type `T*`, is a variable of type `T`.</span></span> <span data-ttu-id="0de11-251">단항 적용할 컴파일 타임 오류 `*` 형식의 식에 연산자 `void*` 또는 포인터 형식이 아닌 식입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-251">It is a compile-time error to apply the unary `*` operator to an expression of type `void*` or to an expression that isn't of a pointer type.</span></span>

<span data-ttu-id="0de11-252">단항 적용 `*` 연산자는 `null` 포인터 구현 시 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-252">The effect of applying the unary `*` operator to a `null` pointer is implementation-defined.</span></span> <span data-ttu-id="0de11-253">특히 보장이 없습니다이 작업에서 throw 하는 `System.NullReferenceException`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-253">In particular, there is no guarantee that this operation throws a `System.NullReferenceException`.</span></span>

<span data-ttu-id="0de11-254">잘못 된 값을 포인터에 단항의 동작에 대 한 할당 된 경우 `*` 연산자 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-254">If an invalid value has been assigned to the pointer, the behavior of the unary `*` operator is undefined.</span></span> <span data-ttu-id="0de11-255">단항에서 포인터를 역참조에 대 한 잘못 된 값에 속하지 `*` 연산자는 형식 지정에 대 한 부적절 하 게 정렬 하는 주소 (에서 예제를 참조 하세요 [포인터 변환](unsafe-code.md#pointer-conversions)), 및 후 변수의 주소는 수명이 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-255">Among the invalid values for dereferencing a pointer by the unary `*` operator are an address inappropriately aligned for the type pointed to (see example in [Pointer conversions](unsafe-code.md#pointer-conversions)), and the address of a variable after the end of its lifetime.</span></span>

<span data-ttu-id="0de11-256">한정 된 할당 분석을 위해 폼의 식을 계산 하 여 생성 되는 변수 `*P` 처음에 할당 된 것으로 간주 됩니다 ([처음에 할당 되는 변수](variables.md#initially-assigned-variables)).</span><span class="sxs-lookup"><span data-stu-id="0de11-256">For purposes of definite assignment analysis, a variable produced by evaluating an expression of the form `*P` is considered initially assigned ([Initially assigned variables](variables.md#initially-assigned-variables)).</span></span>

### <a name="pointer-member-access"></a><span data-ttu-id="0de11-257">포인터 멤버 액세스</span><span class="sxs-lookup"><span data-stu-id="0de11-257">Pointer member access</span></span>

<span data-ttu-id="0de11-258">*pointer_member_access* 이루어져 있습니다를 *primary_expression*뒤를 "`->`" 토큰, 뒤에 *식별자* 및는 선택적 *type_argument_list*합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-258">A *pointer_member_access* consists of a *primary_expression*, followed by a "`->`" token, followed by an *identifier* and an optional *type_argument_list*.</span></span>

```antlr
pointer_member_access
    : primary_expression '->' identifier
    ;
```

<span data-ttu-id="0de11-259">형식의 포인터 멤버 액세스 `P->I`, `P` 이외의 포인터 형식의 식 이어야 `void*`, 및 `I` 는 형식의 액세스 가능 멤버를 표시 해야 합니다 `P` 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-259">In a pointer member access of the form `P->I`, `P` must be an expression of a pointer type other than `void*`, and `I` must denote an accessible member of the type to which `P` points.</span></span>

<span data-ttu-id="0de11-260">형식의 포인터 멤버 액세스 `P->I` 와 동일 하 게 평가 됩니다 `(*P).I`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-260">A pointer member access of the form `P->I` is evaluated exactly as `(*P).I`.</span></span> <span data-ttu-id="0de11-261">에 대 한 설명은 포인터 간접 참조 연산자 (`*`)를 참조 하세요 [포인터 간접 참조](unsafe-code.md#pointer-indirection)합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-261">For a description of the pointer indirection operator (`*`), see [Pointer indirection](unsafe-code.md#pointer-indirection).</span></span> <span data-ttu-id="0de11-262">에 대 한 설명은 멤버 액세스 연산자 (`.`)를 참조 하세요 [멤버 액세스](expressions.md#member-access)합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-262">For a description of the member access operator (`.`), see [Member access](expressions.md#member-access).</span></span>

<span data-ttu-id="0de11-263">예제</span><span class="sxs-lookup"><span data-stu-id="0de11-263">In the example</span></span>

```csharp
using System;

struct Point
{
    public int x;
    public int y;

    public override string ToString() {
        return "(" + x + "," + y + ")";
    }
}

class Test
{
    static void Main() {
        Point point;
        unsafe {
            Point* p = &point;
            p->x = 10;
            p->y = 20;
            Console.WriteLine(p->ToString());
        }
    }
}
```

<span data-ttu-id="0de11-264">`->` 연산자는 필드에 액세스 하 고 포인터를 통해 구조체의 메서드를 호출 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-264">the `->` operator is used to access fields and invoke a method of a struct through a pointer.</span></span> <span data-ttu-id="0de11-265">때문에 작업 `P->I` 정확 하 게 해당 하는 `(*P).I`, `Main` 메서드 작성 원활 하 게 수:</span><span class="sxs-lookup"><span data-stu-id="0de11-265">Because the operation `P->I` is precisely equivalent to `(*P).I`, the `Main` method could equally well have been written:</span></span>

```csharp
class Test
{
    static void Main() {
        Point point;
        unsafe {
            Point* p = &point;
            (*p).x = 10;
            (*p).y = 20;
            Console.WriteLine((*p).ToString());
        }
    }
}
```

### <a name="pointer-element-access"></a><span data-ttu-id="0de11-266">포인터 요소 액세스</span><span class="sxs-lookup"><span data-stu-id="0de11-266">Pointer element access</span></span>

<span data-ttu-id="0de11-267">A *pointer_element_access* 이루어져를 *primary_no_array_creation_expression* 묶인 식을 뒤에 "`[`"및"`]`"입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-267">A *pointer_element_access* consists of a *primary_no_array_creation_expression* followed by an expression enclosed in "`[`" and "`]`".</span></span>

```antlr
pointer_element_access
    : primary_no_array_creation_expression '[' expression ']'
    ;
```

<span data-ttu-id="0de11-268">형식의 포인터 요소 액세스 `P[E]`, `P` 이외의 포인터 형식의 식 이어야 `void*`, 및 `E` 에 암시적으로 변환할 수 있는 식 이어야 합니다 `int`, `uint`를 `long`, 또는 `ulong`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-268">In a pointer element access of the form `P[E]`, `P` must be an expression of a pointer type other than `void*`, and `E` must be an expression that can be implicitly converted to `int`, `uint`, `long`, or `ulong`.</span></span>

<span data-ttu-id="0de11-269">형식의 포인터 요소 액세스 `P[E]` 와 동일 하 게 평가 됩니다 `*(P + E)`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-269">A pointer element access of the form `P[E]` is evaluated exactly as `*(P + E)`.</span></span> <span data-ttu-id="0de11-270">에 대 한 설명은 포인터 간접 참조 연산자 (`*`)를 참조 하세요 [포인터 간접 참조](unsafe-code.md#pointer-indirection)합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-270">For a description of the pointer indirection operator (`*`), see [Pointer indirection](unsafe-code.md#pointer-indirection).</span></span> <span data-ttu-id="0de11-271">에 대 한 설명은 포인터 더하기 연산자 (`+`)를 참조 하세요 [포인터 산술 연산을](unsafe-code.md#pointer-arithmetic).</span><span class="sxs-lookup"><span data-stu-id="0de11-271">For a description of the pointer addition operator (`+`), see [Pointer arithmetic](unsafe-code.md#pointer-arithmetic).</span></span>

<span data-ttu-id="0de11-272">예제</span><span class="sxs-lookup"><span data-stu-id="0de11-272">In the example</span></span>

```csharp
class Test
{
    static void Main() {
        unsafe {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) p[i] = (char)i;
        }
    }
}
```

<span data-ttu-id="0de11-273">포인터 요소 액세스는 초기화 하는 데에 문자 버퍼를 `for` 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-273">a pointer element access is used to initialize the character buffer in a `for` loop.</span></span> <span data-ttu-id="0de11-274">때문에 작업이 `P[E]` 정확 하 게 해당 하는 `*(P + E)`, 예제도 동일 하 게 작성 될 수도:</span><span class="sxs-lookup"><span data-stu-id="0de11-274">Because the operation `P[E]` is precisely equivalent to `*(P + E)`, the example could equally well have been written:</span></span>

```csharp
class Test
{
    static void Main() {
        unsafe {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) *(p + i) = (char)i;
        }
    }
}
```

<span data-ttu-id="0de11-275">에 대 한 포인터 요소 액세스 연산자에 대 한 범위를 벗어나는 확인 하지 오류 및 동작에 액세스 하는 경우는 범위를 벗어나는 요소 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-275">The pointer element access operator does not check for out-of-bounds errors and the behavior when accessing an out-of-bounds element is undefined.</span></span> <span data-ttu-id="0de11-276">C 및 c + +와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-276">This is the same as C and C++.</span></span>

### <a name="the-address-of-operator"></a><span data-ttu-id="0de11-277">Address-of 연산자</span><span class="sxs-lookup"><span data-stu-id="0de11-277">The address-of operator</span></span>

<span data-ttu-id="0de11-278">*addressof_expression* 앰퍼샌드 이루어져 있습니다 (`&`) 뒤에 *unary_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-278">An *addressof_expression* consists of an ampersand (`&`) followed by a *unary_expression*.</span></span>

```antlr
addressof_expression
    : '&' unary_expression
    ;
```

<span data-ttu-id="0de11-279">식에 지정 되었습니다 `E` 는 형식인 `T` 와 고정 변수로 분류 ([고정 및 고정 되지 않은 변수](unsafe-code.md#fixed-and-moveable-variables)), 구문 `&E` 제공한변수의주소를계산`E`.</span><span class="sxs-lookup"><span data-stu-id="0de11-279">Given an expression `E` which is of a type `T` and is classified as a fixed variable ([Fixed and moveable variables](unsafe-code.md#fixed-and-moveable-variables)), the construct `&E` computes the address of the variable given by `E`.</span></span> <span data-ttu-id="0de11-280">결과의 형식은 `T*` 와 값으로 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-280">The type of the result is `T*` and is classified as a value.</span></span> <span data-ttu-id="0de11-281">컴파일 타임 오류가 발생 하는 경우 `E` 분류 되지 않은 변수를 하는 경우 `E` 읽기 전용 지역 변수로 분류 됩니다 이거나 `E` 변수인을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-281">A compile-time error occurs if `E` is not classified as a variable, if `E` is classified as a read-only local variable, or if `E` denotes a moveable variable.</span></span> <span data-ttu-id="0de11-282">마지막 경우 fixed 문 ([fixed 문을](unsafe-code.md#the-fixed-statement)) 일시적으로 "수정" 변수의 해당 주소를 얻기 전에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-282">In the last case, a fixed statement ([The fixed statement](unsafe-code.md#the-fixed-statement)) can be used to temporarily "fix" the variable before obtaining its address.</span></span> <span data-ttu-id="0de11-283">에 명시 된 대로 [me](expressions.md#member-access), 인스턴스 생성자 또는 정적 생성자 정의 하는 클래스 또는 구조체 외부를 `readonly` 필드를 해당 필드 값을 변수가 아니라 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-283">As stated in [Member access](expressions.md#member-access), outside an instance constructor or static constructor for a struct or class that defines a `readonly` field, that field is considered a value, not a variable.</span></span> <span data-ttu-id="0de11-284">따라서 해당 주소를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-284">As such, its address cannot be taken.</span></span> <span data-ttu-id="0de11-285">마찬가지로, 상수의 주소를 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-285">Similarly, the address of a constant cannot be taken.</span></span>

<span data-ttu-id="0de11-286">합니다 `&` 연산자는 정적으로 할당 된 제공 되지만 다음 인수를 필요 하지 않습니다는 `&` 작업 연산자 적용 되는 변수의 작업 발생 하는 실행 경로에 정적으로 할당 된 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-286">The `&` operator does not require its argument to be definitely assigned, but following an `&` operation, the variable to which the operator is applied is considered definitely assigned in the execution path in which the operation occurs.</span></span> <span data-ttu-id="0de11-287">변수는 올바른 초기화 되도록 프로그래머의 책임 실제로 수행 되었는지이 이런 이며</span><span class="sxs-lookup"><span data-stu-id="0de11-287">It is the responsibility of the programmer to ensure that correct initialization of the variable actually does take place in this situation.</span></span>

<span data-ttu-id="0de11-288">예제</span><span class="sxs-lookup"><span data-stu-id="0de11-288">In the example</span></span>

```csharp
using System;

class Test
{
    static void Main() {
        int i;
        unsafe {
            int* p = &i;
            *p = 123;
        }
        Console.WriteLine(i);
    }
}
```

<span data-ttu-id="0de11-289">`i` 다음 정적으로 할당 된 것으로 간주 됩니다 합니다 `&i` 초기화를 사용 하는 작업 `p`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-289">`i` is considered definitely assigned following the `&i` operation used to initialize `p`.</span></span> <span data-ttu-id="0de11-290">에 대 한 할당 `*p` 초기화 적용 `i`, 하지만이 초기화 포함은 프로그래머의 책임 및 할당 제거 된 경우 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-290">The assignment to `*p` in effect initializes `i`, but the inclusion of this initialization is the responsibility of the programmer, and no compile-time error would occur if the assignment was removed.</span></span>

<span data-ttu-id="0de11-291">규칙에 대 한 한정 된 할당에는 `&` 연산자 존재는 지역 변수 초기화 중복을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-291">The rules of definite assignment for the `&` operator exist such that redundant initialization of local variables can be avoided.</span></span> <span data-ttu-id="0de11-292">예를 들어, 대부분의 외부 Api API에 의해 채워진 구조체 포인터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-292">For example, many external APIs take a pointer to a structure which is filled in by the API.</span></span> <span data-ttu-id="0de11-293">이러한 Api에 대 한 호출에는 일반적으로 로컬 구조체 변수의 주소를 전달 하 고 규칙 없이 구조체 변수의 중복 초기화 필요한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-293">Calls to such APIs typically pass the address of a local struct variable, and without the rule, redundant initialization of the struct variable would be required.</span></span>

### <a name="pointer-increment-and-decrement"></a><span data-ttu-id="0de11-294">포인터 증가 및 감소</span><span class="sxs-lookup"><span data-stu-id="0de11-294">Pointer increment and decrement</span></span>

<span data-ttu-id="0de11-295">안전 하지 않은 컨텍스트에서 `++` 하 고 `--` 연산자 ([후 위 증가 및 감소 연산자](expressions.md#postfix-increment-and-decrement-operators) 하 고 [전위 증가 및 감소 연산자](expressions.md#prefix-increment-and-decrement-operators)) 포인터에 적용할 수 있습니다 제외한 모든 형식의 변수 `void*`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-295">In an unsafe context, the `++` and `--` operators ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators) and [Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)) can be applied to pointer variables of all types except `void*`.</span></span> <span data-ttu-id="0de11-296">따라서 모든 포인터 형식에 대 한 `T*`, 다음 연산자를 암시적으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-296">Thus, for every pointer type `T*`, the following operators are implicitly defined:</span></span>

```csharp
T* operator ++(T* x);
T* operator --(T* x);
```

<span data-ttu-id="0de11-297">연산자와 동일한 결과 생성할 `x + 1` 하 고 `x - 1`각각 ([포인터 산술 연산을](unsafe-code.md#pointer-arithmetic)).</span><span class="sxs-lookup"><span data-stu-id="0de11-297">The operators produce the same results as `x + 1` and `x - 1`, respectively ([Pointer arithmetic](unsafe-code.md#pointer-arithmetic)).</span></span> <span data-ttu-id="0de11-298">형식의 포인터 변수에 대 한 다시 말해 `T*`, `++` 연산자는 추가 `sizeof(T)` 변수에 포함 된 주소로 및 `--` 연산자 뺍니다 `sizeof(T)` 변수에 포함 된 주소에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-298">In other words, for a pointer variable of type `T*`, the `++` operator adds `sizeof(T)` to the address contained in the variable, and the `--` operator subtracts `sizeof(T)` from the address contained in the variable.</span></span>

<span data-ttu-id="0de11-299">포인터 증가 또는 감소 하는 경우 포인터 형식의 도메인을 오버플로 하는 작업 결과 구현 정의 되지만 예외가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-299">If a pointer increment or decrement operation overflows the domain of the pointer type, the result is implementation-defined, but no exceptions are produced.</span></span>

### <a name="pointer-arithmetic"></a><span data-ttu-id="0de11-300">포인터 산술 연산</span><span class="sxs-lookup"><span data-stu-id="0de11-300">Pointer arithmetic</span></span>

<span data-ttu-id="0de11-301">안전 하지 않은 컨텍스트에서 `+` 하 고 `-` 연산자 ([더하기 연산자](expressions.md#addition-operator) 하 고 [빼기 연산자](expressions.md#subtraction-operator)) 제외 하 고 모든 포인터 형식의 값에 적용할 수 있습니다 `void*`.</span><span class="sxs-lookup"><span data-stu-id="0de11-301">In an unsafe context, the `+` and `-` operators ([Addition operator](expressions.md#addition-operator) and [Subtraction operator](expressions.md#subtraction-operator)) can be applied to values of all pointer types except `void*`.</span></span> <span data-ttu-id="0de11-302">따라서 모든 포인터 형식에 대 한 `T*`, 다음 연산자를 암시적으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-302">Thus, for every pointer type `T*`, the following operators are implicitly defined:</span></span>

```csharp
T* operator +(T* x, int y);
T* operator +(T* x, uint y);
T* operator +(T* x, long y);
T* operator +(T* x, ulong y);

T* operator +(int x, T* y);
T* operator +(uint x, T* y);
T* operator +(long x, T* y);
T* operator +(ulong x, T* y);

T* operator -(T* x, int y);
T* operator -(T* x, uint y);
T* operator -(T* x, long y);
T* operator -(T* x, ulong y);

long operator -(T* x, T* y);
```

<span data-ttu-id="0de11-303">식에 지정 되었습니다 `P` 포인터 형식의 `T*` 및 식을 `N` 형식의 `int`, `uint`를 `long`, 또는 `ulong`, 식 `P + N` 및 `N + P` 계산는 형식의 포인터 값 `T*` 결과 추가에서 나온 `N * sizeof(T)` 제공한 주소로 `P`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-303">Given an expression `P` of a pointer type `T*` and an expression `N` of type `int`, `uint`, `long`, or `ulong`, the expressions `P + N` and `N + P` compute the pointer value of type `T*` that results from adding `N * sizeof(T)` to the address given by `P`.</span></span> <span data-ttu-id="0de11-304">마찬가지로, 식이 `P - N` 형식의 포인터 값을 계산 `T*` 뺀 결과 `N * sizeof(T)` 제공한 주소에서 `P`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-304">Likewise, the expression `P - N` computes the pointer value of type `T*` that results from subtracting `N * sizeof(T)` from the address given by `P`.</span></span>

<span data-ttu-id="0de11-305">지정 된 두 식 `P` 하 고 `Q`, 포인터 형식의 `T*`, 식을 `P - Q` 제공한 주소 간의 차이 계산 `P` 및 `Q` 다음 차이점 나눕니다및`sizeof(T)`.</span><span class="sxs-lookup"><span data-stu-id="0de11-305">Given two expressions, `P` and `Q`, of a pointer type `T*`, the expression `P - Q` computes the difference between the addresses given by `P` and `Q` and then divides that difference by `sizeof(T)`.</span></span> <span data-ttu-id="0de11-306">결과의 형식은 항상 `long`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-306">The type of the result is always `long`.</span></span> <span data-ttu-id="0de11-307">사실 `P - Q` 로 계산 됩니다 `((long)(P) - (long)(Q)) / sizeof(T)`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-307">In effect, `P - Q` is computed as `((long)(P) - (long)(Q)) / sizeof(T)`.</span></span>

<span data-ttu-id="0de11-308">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="0de11-308">For example:</span></span>

```csharp
using System;

class Test
{
    static void Main() {
        unsafe {
            int* values = stackalloc int[20];
            int* p = &values[1];
            int* q = &values[15];
            Console.WriteLine("p - q = {0}", p - q);
            Console.WriteLine("q - p = {0}", q - p);
        }
    }
}
```

<span data-ttu-id="0de11-309">출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-309">which produces the output:</span></span>

```
p - q = -14
q - p = 14
```

<span data-ttu-id="0de11-310">포인터 형식의 도메인을 오버플로 하는 포인터 산술 연산, 결과 구현 시 정의 된 방식으로 잘렸습니다. 되지만 예외가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-310">If a pointer arithmetic operation overflows the domain of the pointer type, the result is truncated in an implementation-defined fashion, but no exceptions are produced.</span></span>

### <a name="pointer-comparison"></a><span data-ttu-id="0de11-311">포인터 비교</span><span class="sxs-lookup"><span data-stu-id="0de11-311">Pointer comparison</span></span>

<span data-ttu-id="0de11-312">안전 하지 않은 컨텍스트에서 `==`, `!=`, `<`, `>`합니다 `<=`, 및 `=>` 연산자 ([관계형 및 형식 테스트 연산자](expressions.md#relational-and-type-testing-operators)) 모든 값에 적용할 수 있습니다 포인터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-312">In an unsafe context, the `==`, `!=`, `<`, `>`, `<=`, and `=>` operators ([Relational and type-testing operators](expressions.md#relational-and-type-testing-operators)) can be applied to values of all pointer types.</span></span> <span data-ttu-id="0de11-313">포인터 비교 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-313">The pointer comparison operators are:</span></span>

```csharp
bool operator ==(void* x, void* y);
bool operator !=(void* x, void* y);
bool operator <(void* x, void* y);
bool operator >(void* x, void* y);
bool operator <=(void* x, void* y);
bool operator >=(void* x, void* y);
```

<span data-ttu-id="0de11-314">모든 포인터 형식으로의 암시적 변환이 존재 하기 때문에 `void*` 이러한 연산자를 사용 하 여 형식에 대 한 포인터 형식의 피연산자를 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-314">Because an implicit conversion exists from any pointer type to the `void*` type, operands of any pointer type can be compared using these operators.</span></span> <span data-ttu-id="0de11-315">비교 연산자는 부호 없는 정수 처럼 두 개의 피연산자가 제공한 주소를 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-315">The comparison operators compare the addresses given by the two operands as if they were unsigned integers.</span></span>

### <a name="the-sizeof-operator"></a><span data-ttu-id="0de11-316">Sizeof 연산자</span><span class="sxs-lookup"><span data-stu-id="0de11-316">The sizeof operator</span></span>

<span data-ttu-id="0de11-317">`sizeof` 연산자에 지정 된 형식의 변수가 차지 하는 바이트 수를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-317">The `sizeof` operator returns the number of bytes occupied by a variable of a given type.</span></span> <span data-ttu-id="0de11-318">피연산자로 지정 된 형식 `sizeof` 이어야 합니다는 *unmanaged_type* ([포인터 형식](unsafe-code.md#pointer-types)).</span><span class="sxs-lookup"><span data-stu-id="0de11-318">The type specified as an operand to `sizeof` must be an *unmanaged_type* ([Pointer types](unsafe-code.md#pointer-types)).</span></span>

```antlr
sizeof_expression
    : 'sizeof' '(' unmanaged_type ')'
    ;
```

<span data-ttu-id="0de11-319">결과 `sizeof` 연산자는 형식의 값 `int`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-319">The result of the `sizeof` operator is a value of type `int`.</span></span> <span data-ttu-id="0de11-320">특정 미리 정의 된 형식에는 `sizeof` 연산자는 아래 표에 나와 있는 것 처럼 상수 값을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-320">For certain predefined types, the `sizeof` operator yields a constant value as shown in the table below.</span></span>


| <span data-ttu-id="0de11-321">__식__</span><span class="sxs-lookup"><span data-stu-id="0de11-321">__Expression__</span></span>   | <span data-ttu-id="0de11-322">__결과__</span><span class="sxs-lookup"><span data-stu-id="0de11-322">__Result__</span></span> |
|------------------|------------|
| `sizeof(sbyte)`  | `1`        |
| `sizeof(byte)`   | `1`        |
| `sizeof(short)`  | `2`        |
| `sizeof(ushort)` | `2`        |
| `sizeof(int)`    | `4`        |
| `sizeof(uint)`   | `4`        |
| `sizeof(long)`   | `8`        |
| `sizeof(ulong)`  | `8`        |
| `sizeof(char)`   | `2`        |
| `sizeof(float)`  | `4`        |
| `sizeof(double)` | `8`        |
| `sizeof(bool)`   | `1`        |

<span data-ttu-id="0de11-323">다른 모든 종류의 결과 대 한는 `sizeof` 연산자는 구현 시 정의 및 상수가 아닌 값으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-323">For all other types, the result of the `sizeof` operator is implementation-defined and is classified as a value, not a constant.</span></span>

<span data-ttu-id="0de11-324">멤버가 구조체에 압축 되는 순서가 지정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-324">The order in which members are packed into a struct is unspecified.</span></span>

<span data-ttu-id="0de11-325">맞춤을 위해 있을 수 있습니다 하지 명명 된 구조체 내의 구조체의 시작 부분 및 구조체의 끝에 패딩 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-325">For alignment purposes, there may be unnamed padding at the beginning of a struct, within a struct, and at the end of the struct.</span></span> <span data-ttu-id="0de11-326">안쪽 여백으로 비트 내용의 확정적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-326">The contents of the bits used as padding are indeterminate.</span></span>

<span data-ttu-id="0de11-327">구조체 형식의 피연산자에 적용 되 면 결과 안쪽 여백을 포함 하 여 해당 형식의 변수에 바이트의 총 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-327">When applied to an operand that has struct type, the result is the total number of bytes in a variable of that type, including any padding.</span></span>

## <a name="the-fixed-statement"></a><span data-ttu-id="0de11-328">Fixed 문</span><span class="sxs-lookup"><span data-stu-id="0de11-328">The fixed statement</span></span>

<span data-ttu-id="0de11-329">안전 하지 않은 컨텍스트에서 *embedded_statement* ([문을](statements.md)) 프로덕션에는 추가 구문 허용을 `fixed` 변수인 "해결" 하는 데 사용 되는 문이 되도록 해당 주소를 문의 기간에 대 한 일정 하 게 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-329">In an unsafe context, the *embedded_statement* ([Statements](statements.md)) production permits an additional construct, the `fixed` statement, which is used to "fix" a moveable variable such that its address remains constant for the duration of the statement.</span></span>

```antlr
fixed_statement
    : 'fixed' '(' pointer_type fixed_pointer_declarators ')' embedded_statement
    ;

fixed_pointer_declarators
    : fixed_pointer_declarator (','  fixed_pointer_declarator)*
    ;

fixed_pointer_declarator
    : identifier '=' fixed_pointer_initializer
    ;

fixed_pointer_initializer
    : '&' variable_reference
    | expression
    ;
```

<span data-ttu-id="0de11-330">각 *fixed_pointer_declarator* 의 로컬 변수를 선언 하는 지정 된 *pointer_type* 해당 계산 하는 주소를 사용 하 여 해당 로컬 변수를 초기화 하 고 *fixed_ pointer_initializer*합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-330">Each *fixed_pointer_declarator* declares a local variable of the given *pointer_type* and initializes that local variable with the address computed by the corresponding *fixed_pointer_initializer*.</span></span> <span data-ttu-id="0de11-331">에 선언 된 지역 변수를 `fixed` 문 하나에 액세스할 수 *fixed_pointer_initializer*가 해당 변수의 선언 오른쪽에서 발생 합니다 *embedded_statement* 의 `fixed` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-331">A local variable declared in a `fixed` statement is accessible in any *fixed_pointer_initializer*s occurring to the right of that variable's declaration, and in the *embedded_statement* of the `fixed` statement.</span></span> <span data-ttu-id="0de11-332">선언 된 지역 변수는 `fixed` 문을 읽기 전용으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-332">A local variable declared by a `fixed` statement is considered read-only.</span></span> <span data-ttu-id="0de11-333">포함된 된 문을이 로컬 변수를 수정 하려고 하면 컴파일 타임 오류가 발생 (할당을 통해 또는 `++` 하 고 `--` 연산자)로 전달 하거나를 `ref` 또는 `out` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-333">A compile-time error occurs if the embedded statement attempts to modify this local variable (via assignment or the `++` and `--` operators) or pass it as a `ref` or `out` parameter.</span></span>

<span data-ttu-id="0de11-334">A *fixed_pointer_initializer* 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-334">A *fixed_pointer_initializer* can be one of the following:</span></span>

*  <span data-ttu-id="0de11-335">토큰 "`&`" 뒤에 *variable_reference* ([한정 된 할당을 확인 하는 것에 대 한 정확한 규칙](variables.md#precise-rules-for-determining-definite-assignment)) 고정 되지 않은 변수에 ([고정 및 고정 되지 않은 변수](unsafe-code.md#fixed-and-moveable-variables)) 관리 되지 않는 형식의 `T`, 형식 제공 `T*` 에 지정 된 포인터 형식으로 암시적으로 변환할 수는 `fixed` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-335">The token "`&`" followed by a *variable_reference* ([Precise rules for determining definite assignment](variables.md#precise-rules-for-determining-definite-assignment)) to a moveable variable ([Fixed and moveable variables](unsafe-code.md#fixed-and-moveable-variables)) of an unmanaged type `T`, provided the type `T*` is implicitly convertible to the pointer type given in the `fixed` statement.</span></span> <span data-ttu-id="0de11-336">이 경우 이니셜라이저는 지정 된 변수의 주소를 계산 하 고 변수의 기간에 대 한 고정된 주소를 유지 하도록 보장 됩니다는 `fixed` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-336">In this case, the initializer computes the address of the given variable, and the variable is guaranteed to remain at a fixed address for the duration of the `fixed` statement.</span></span>
*  <span data-ttu-id="0de11-337">식을 *array_type* 관리 되지 않는 형식의 요소를 사용 하 여 `T`, 형식을 제공 `T*` 에 지정 된 포인터 형식으로 암시적으로 변환할 수는 `fixed` 문.</span><span class="sxs-lookup"><span data-stu-id="0de11-337">An expression of an *array_type* with elements of an unmanaged type `T`, provided the type `T*` is implicitly convertible to the pointer type given in the `fixed` statement.</span></span> <span data-ttu-id="0de11-338">이 경우 이니셜라이저는 배열에서 첫 번째 요소의 주소를 계산 하 고 배열 전체 기간에 대 한 고정된 주소를 유지 하도록 보장 됩니다는 `fixed` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-338">In this case, the initializer computes the address of the first element in the array, and the entire array is guaranteed to remain at a fixed address for the duration of the `fixed` statement.</span></span> <span data-ttu-id="0de11-339">배열 식이 null 인지 또는 배열에 요소가 없는 경우 이니셜라이저 주소 등호를 0으로 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-339">If the array expression is null or if the array has zero elements, the initializer computes an address equal to zero.</span></span>
*  <span data-ttu-id="0de11-340">형식의 식을 `string`, 형식을 제공 `char*` 에 지정 된 포인터 형식으로 암시적으로 변환할 수는 `fixed` 문.</span><span class="sxs-lookup"><span data-stu-id="0de11-340">An expression of type `string`, provided the type `char*` is implicitly convertible to the pointer type given in the `fixed` statement.</span></span> <span data-ttu-id="0de11-341">이 경우 이니셜라이저는 문자열에서 첫 번째 문자의 주소를 계산 하 고 전체 문자열의 기간에 대 한 고정된 주소를 유지 하도록 보장 됩니다는 `fixed` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-341">In this case, the initializer computes the address of the first character in the string, and the entire string is guaranteed to remain at a fixed address for the duration of the `fixed` statement.</span></span> <span data-ttu-id="0de11-342">동작을 `fixed` 문에 구현 시 정의 된 null 이면 문자열 식입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-342">The behavior of the `fixed` statement is implementation-defined if the string expression is null.</span></span>
*  <span data-ttu-id="0de11-343">A *simple_name* 하거나 *member_access* 참조 하는 고정된 크기 버퍼 소속 변수인 고정된 크기 버퍼 멤버의 형식이 지정 된 포인터 형식으로 암시적으로 변환할 제공 에 `fixed` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-343">A *simple_name* or *member_access* that references a fixed size buffer member of a moveable variable, provided the type of the fixed size buffer member is implicitly convertible to the pointer type given in the `fixed` statement.</span></span> <span data-ttu-id="0de11-344">이니셜라이저는 고정된 크기 버퍼의 첫 번째 요소에 대 한 포인터를 계산 하는 예제의 경우 ([식에서 고정 크기 버퍼](unsafe-code.md#fixed-size-buffers-in-expressions)), 고정된 크기 버퍼는 기간에대한고정된주소를유지하도록보장됩니다및`fixed`문입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-344">In this case, the initializer computes a pointer to the first element of the fixed size buffer ([Fixed size buffers in expressions](unsafe-code.md#fixed-size-buffers-in-expressions)), and the fixed size buffer is guaranteed to remain at a fixed address for the duration of the `fixed` statement.</span></span>

<span data-ttu-id="0de11-345">계산 하는 각 주소에 대 한는 *fixed_pointer_initializer* 는 `fixed` 문을 사용 하면 주소로 참조 변수의 재배치 하거나 기간에 대 한 가비지 수집기에서 삭제할 아닌지는 `fixed` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-345">For each address computed by a *fixed_pointer_initializer* the `fixed` statement ensures that the variable referenced by the address is not subject to relocation or disposal by the garbage collector for the duration of the `fixed` statement.</span></span> <span data-ttu-id="0de11-346">예를 들어 주소에서 계산을 *fixed_pointer_initializer* 개체의 필드 또는 배열 인스턴스 요소의 참조는 `fixed` 문을 사용 하면 포함 된 개체 인스턴스 재배치 하지 않으면 또는 명령문의 수명 동안 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-346">For example, if the address computed by a *fixed_pointer_initializer* references a field of an object or an element of an array instance, the `fixed` statement guarantees that the containing object instance is not relocated or disposed of during the lifetime of the statement.</span></span>

<span data-ttu-id="0de11-347">포인터에서 만들어졌는지 확인 해야 하는 프로그래머의 `fixed` 문을 이러한 문의 실행은 초과 남지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-347">It is the programmer's responsibility to ensure that pointers created by `fixed` statements do not survive beyond execution of those statements.</span></span> <span data-ttu-id="0de11-348">예를 들어 포인터 하 여 만든 경우 `fixed` 문 외부 Api에 전달 됩니다 이며 프로그래머는 Api 메모리가 없습니다. 이러한 포인터를 유지 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-348">For example, when pointers created by `fixed` statements are passed to external APIs, it is the programmer's responsibility to ensure that the APIs retain no memory of these pointers.</span></span>

<span data-ttu-id="0de11-349">(이동할 수 없습니다) 하므로 고정된 개체 힙의 조각화를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-349">Fixed objects may cause fragmentation of the heap (because they can't be moved).</span></span> <span data-ttu-id="0de11-350">이런 이유로 개체 수정 해야 반드시 필요한 경우에 차례로 돌아가도록 가능한 시간에 대해서만 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-350">For that reason, objects should be fixed only when absolutely necessary and then only for the shortest amount of time possible.</span></span>

<span data-ttu-id="0de11-351">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="0de11-351">The example</span></span>

```csharp
class Test
{
    static int x;
    int y;

    unsafe static void F(int* p) {
        *p = 1;
    }

    static void Main() {
        Test t = new Test();
        int[] a = new int[10];
        unsafe {
            fixed (int* p = &x) F(p);
            fixed (int* p = &t.y) F(p);
            fixed (int* p = &a[0]) F(p);
            fixed (int* p = a) F(p);
        }
    }
}
```

<span data-ttu-id="0de11-352">몇 가지 사용 방법을 보여 줍니다는 `fixed` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-352">demonstrates several uses of the `fixed` statement.</span></span> <span data-ttu-id="0de11-353">첫 번째 문을 수정 하 고 정적 필드의 주소를 가져옵니다, 두 번째 문을 수정 하 고는 인스턴스 필드의 주소를 가져옵니다 및 세 번째 문을 수정 하 고 배열 요소의 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-353">The first statement fixes and obtains the address of a static field, the second statement fixes and obtains the address of an instance field, and the third statement fixes and obtains the address of an array element.</span></span> <span data-ttu-id="0de11-354">각각의 경우에서 것이 더 일반적인을 사용 하 여 `&` 연산자 이므로 변수를 모두 고정 되지 않은 변수도 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-354">In each case it would have been an error to use the regular `&` operator since the variables are all classified as moveable variables.</span></span>

<span data-ttu-id="0de11-355">네 번째 `fixed` 위의 예에서 문은 세 비슷한 결과 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-355">The fourth `fixed` statement in the example above produces a similar result to the third.</span></span>

<span data-ttu-id="0de11-356">이 예제는 `fixed` 문 사용 하 여 `string`:</span><span class="sxs-lookup"><span data-stu-id="0de11-356">This example of the `fixed` statement uses `string`:</span></span>

```csharp
class Test
{
    static string name = "xx";

    unsafe static void F(char* p) {
        for (int i = 0; p[i] != '\0'; ++i)
            Console.WriteLine(p[i]);
    }

    static void Main() {
        unsafe {
            fixed (char* p = name) F(p);
            fixed (char* p = "xx") F(p);
        }
    }
}
```

<span data-ttu-id="0de11-357">안전 하지 않은 컨텍스트에서 단일 차원 배열의 배열 요소 인덱스부터 증가 인덱스 순서로 저장 됩니다 `0` 인덱스까지 `Length - 1`입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-357">In an unsafe context array elements of single-dimensional arrays are stored in increasing index order, starting with index `0` and ending with index `Length - 1`.</span></span> <span data-ttu-id="0de11-358">다차원 배열에서 맨 오른쪽 차원의 인덱스는 먼저 증가 되도록 요소가 저장 되는 배열에 대 한 다음 다음 왼쪽 차원 등에서 왼쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-358">For multi-dimensional arrays, array elements are stored such that the indices of the rightmost dimension are increased first, then the next left dimension, and so on to the left.</span></span> <span data-ttu-id="0de11-359">내를 `fixed` 문에 대 한 포인터를 가져오는 `p` 배열 인스턴스에 `a`, 까지의 포인터 값 `p` 에 `p + a.Length - 1` 배열에서 요소의 주소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-359">Within a `fixed` statement that obtains a pointer `p` to an array instance `a`, the pointer values ranging from `p` to `p + a.Length - 1` represent addresses of the elements in the array.</span></span> <span data-ttu-id="0de11-360">범위의 변수 마찬가지로 `p[0]` 에 `p[a.Length - 1]` 실제 배열 요소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-360">Likewise, the variables ranging from `p[0]` to `p[a.Length - 1]` represent the actual array elements.</span></span> <span data-ttu-id="0de11-361">배열 저장 되는 방식으로 지정 되 면에서는 선형 것 처럼 모든 차원 배열을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-361">Given the way in which arrays are stored, we can treat an array of any dimension as though it were linear.</span></span>

<span data-ttu-id="0de11-362">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="0de11-362">For example:</span></span>

```csharp
using System;

class Test
{
    static void Main() {
        int[,,] a = new int[2,3,4];
        unsafe {
            fixed (int* p = a) {
                for (int i = 0; i < a.Length; ++i)    // treat as linear
                    p[i] = i;
            }
        }

        for (int i = 0; i < 2; ++i)
            for (int j = 0; j < 3; ++j) {
                for (int k = 0; k < 4; ++k)
                    Console.Write("[{0},{1},{2}] = {3,2} ", i, j, k, a[i,j,k]);
                Console.WriteLine();
            }
    }
}
```

<span data-ttu-id="0de11-363">출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-363">which produces the output:</span></span>

```
[0,0,0] =  0 [0,0,1] =  1 [0,0,2] =  2 [0,0,3] =  3
[0,1,0] =  4 [0,1,1] =  5 [0,1,2] =  6 [0,1,3] =  7
[0,2,0] =  8 [0,2,1] =  9 [0,2,2] = 10 [0,2,3] = 11
[1,0,0] = 12 [1,0,1] = 13 [1,0,2] = 14 [1,0,3] = 15
[1,1,0] = 16 [1,1,1] = 17 [1,1,2] = 18 [1,1,3] = 19
[1,2,0] = 20 [1,2,1] = 21 [1,2,2] = 22 [1,2,3] = 23
```

<span data-ttu-id="0de11-364">예제</span><span class="sxs-lookup"><span data-stu-id="0de11-364">In the example</span></span>

```csharp
class Test
{
    unsafe static void Fill(int* p, int count, int value) {
        for (; count != 0; count--) *p++ = value;
    }

    static void Main() {
        int[] a = new int[100];
        unsafe {
            fixed (int* p = a) Fill(p, 100, -1);
        }
    }
}
```

<span data-ttu-id="0de11-365">`fixed` 해당 주소에 대 한 포인터를 사용 하는 메서드에 전달할 수 있도록 배열을 수정 문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-365">a `fixed` statement is used to fix an array so its address can be passed to a method that takes a pointer.</span></span>

<span data-ttu-id="0de11-366">예제:</span><span class="sxs-lookup"><span data-stu-id="0de11-366">In the example:</span></span>

```csharp
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}

class Test
{
    unsafe static void PutString(string s, char* buffer, int bufSize) {
        int len = s.Length;
        if (len > bufSize) len = bufSize;
        for (int i = 0; i < len; i++) buffer[i] = s[i];
        for (int i = len; i < bufSize; i++) buffer[i] = (char)0;
    }

    Font f;

    unsafe static void Main()
    {
        Test test = new Test();
        test.f.size = 10;
        fixed (char* p = test.f.name) {
            PutString("Times New Roman", p, 32);
        }
    }
}
```

<span data-ttu-id="0de11-367">fixed 문에 대 한 포인터로 해당 주소를 사용할 수 있도록 고정된 크기 버퍼는 구조체의 해결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-367">a fixed statement is used to fix a fixed size buffer of a struct so its address can be used as a pointer.</span></span>

<span data-ttu-id="0de11-368">`char*` 문자열 인스턴스를 null로 끝나는 문자열을 가리키는 항상 수정 하 여 생성 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-368">A `char*` value produced by fixing a string instance always points to a null-terminated string.</span></span> <span data-ttu-id="0de11-369">Fixed 문에 대 한 포인터를 가져오는 내 `p` 문자열 인스턴스로 `s`, 까지의 포인터 값 `p` 에 `p + s.Length - 1` 문자열과 포인터 값에 있는 문자의 주소를 나타냅니다 `p + s.Length` 항상 null 문자를 가리키는 (값을 갖는 문자 `'\0'`).</span><span class="sxs-lookup"><span data-stu-id="0de11-369">Within a fixed statement that obtains a pointer `p` to a string instance `s`, the pointer values ranging from `p` to `p + s.Length - 1` represent addresses of the characters in the string, and the pointer value `p + s.Length` always points to a null character (the character with value `'\0'`).</span></span>

<span data-ttu-id="0de11-370">정의 되지 않은 동작이 발생할 수 있습니다. 고정된 포인터를 통해 관리 되는 형식의 개체를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-370">Modifying objects of managed type through fixed pointers can results in undefined behavior.</span></span> <span data-ttu-id="0de11-371">예를 들어, 문자열을 변경할 수 없기 때문에 고정된 문자열에 대 한 포인터에서 참조 하는 문자는 수정 되지 않습니다 있도록 프로그래머의 몫입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-371">For example, because strings are immutable, it is the programmer's responsibility to ensure that the characters referenced by a pointer to a fixed string are not modified.</span></span>

<span data-ttu-id="0de11-372">문자열의 자동 null 종료 "C-스타일" 문자열을 필요로 하는 외부 Api를 호출 하는 경우에 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-372">The automatic null-termination of strings is particularly convenient when calling external APIs that expect "C-style" strings.</span></span> <span data-ttu-id="0de11-373">그러나 문자열 인스턴스는 null 문자를 포함 하도록 허용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-373">Note, however, that a string instance is permitted to contain null characters.</span></span> <span data-ttu-id="0de11-374">이러한 null 문자가 있는 경우 문자열은 잘린 상태로 나타날 null로 끝나는 취급 하는 경우 `char*`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-374">If such null characters are present, the string will appear truncated when treated as a null-terminated `char*`.</span></span>

## <a name="fixed-size-buffers"></a><span data-ttu-id="0de11-375">고정된 크기 버퍼</span><span class="sxs-lookup"><span data-stu-id="0de11-375">Fixed size buffers</span></span>

<span data-ttu-id="0de11-376">고정된 크기 버퍼 "C 스타일" 인라인 배열을 구조체의 멤버로 선언 하는 데 사용 되 고 관리 되지 않는 Api와의 상호 작용에 주로 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-376">Fixed size buffers are used to declare "C style" in-line arrays as members of structs, and are primarily useful for interfacing with unmanaged APIs.</span></span>

### <a name="fixed-size-buffer-declarations"></a><span data-ttu-id="0de11-377">고정된 크기 버퍼 선언</span><span class="sxs-lookup"><span data-stu-id="0de11-377">Fixed size buffer declarations</span></span>

<span data-ttu-id="0de11-378">A ***고정 크기 버퍼*** 는 지정 된 형식의 변수는 고정된 길이 버퍼에 대 한 저장소를 나타내는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-378">A ***fixed size buffer*** is a member that represents storage for a fixed length buffer of variables of a given type.</span></span> <span data-ttu-id="0de11-379">고정된 크기 버퍼 선언에서는 지정 된 요소 형식의 하나 이상의 고정된 크기 버퍼를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-379">A fixed size buffer declaration introduces one or more fixed size buffers of a given element type.</span></span> <span data-ttu-id="0de11-380">고정된 크기 버퍼는 구조체 선언 에서만 허용 됩니다 하 고 안전 하지 않은 컨텍스트에서 에서만 발생할 수 있습니다 ([안전 하지 않은 컨텍스트](unsafe-code.md#unsafe-contexts)).</span><span class="sxs-lookup"><span data-stu-id="0de11-380">Fixed size buffers are only permitted in struct declarations and can only occur in unsafe contexts ([Unsafe contexts](unsafe-code.md#unsafe-contexts)).</span></span>

```antlr
struct_member_declaration_unsafe
    : fixed_size_buffer_declaration
    ;

fixed_size_buffer_declaration
    : attributes? fixed_size_buffer_modifier* 'fixed' buffer_element_type fixed_size_buffer_declarator+ ';'
    ;

fixed_size_buffer_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'unsafe'
    ;

buffer_element_type
    : type
    ;

fixed_size_buffer_declarator
    : identifier '[' constant_expression ']'
    ;
```

<span data-ttu-id="0de11-381">고정된 크기 버퍼 선언 특성 집합이 포함 될 수 있습니다 ([특성](attributes.md)), `new` 한정자 ([한정자](classes.md#modifiers)), 네 가지 액세스 한정자의 유효한 조합이 ([형식 매개 변수 및 제약 조건](classes.md#type-parameters-and-constraints)) 및 `unsafe` 한정자 ([안전 하지 않은 컨텍스트](unsafe-code.md#unsafe-contexts)).</span><span class="sxs-lookup"><span data-stu-id="0de11-381">A fixed size buffer declaration may include a set of attributes ([Attributes](attributes.md)), a `new` modifier ([Modifiers](classes.md#modifiers)), a valid combination of the four access modifiers ([Type parameters and constraints](classes.md#type-parameters-and-constraints)) and an `unsafe` modifier ([Unsafe contexts](unsafe-code.md#unsafe-contexts)).</span></span> <span data-ttu-id="0de11-382">특성 및 한정자 모든 고정된 크기 버퍼 선언에서 선언 된 멤버에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-382">The attributes and modifiers apply to all of the members declared by the fixed size buffer declaration.</span></span> <span data-ttu-id="0de11-383">이를 여러 번 고정된 크기 버퍼 선언에서 동일한 한정자에 대 한 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-383">It is an error for the same modifier to appear multiple times in a fixed size buffer declaration.</span></span>

<span data-ttu-id="0de11-384">고정된 크기 버퍼 선언 포함 하도록 허용 되지 않습니다는 `static` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-384">A fixed size buffer declaration is not permitted to include the `static` modifier.</span></span>

<span data-ttu-id="0de11-385">고정된 크기 버퍼 선언의 버퍼 요소 형식 선언에 의해 도입 된 버퍼의 요소 형식 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-385">The buffer element type of a fixed size buffer declaration specifies the element type of the buffer(s) introduced by the declaration.</span></span> <span data-ttu-id="0de11-386">버퍼 요소 형식 미리 정의 된 형식 중 하나 여야 `sbyte`, `byte`, `short`, `ushort`, `int`를 `uint`, `long`, `ulong`, `char`, `float`를 `double`, 또는 `bool`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-386">The buffer element type must be one of the predefined types `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, or `bool`.</span></span>

<span data-ttu-id="0de11-387">버퍼 요소 형식 새 멤버를 소개 하는 각 고정된 크기 버퍼 선언 자 목록이 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-387">The buffer element type is followed by a list of fixed size buffer declarators, each of which introduces a new member.</span></span> <span data-ttu-id="0de11-388">고정된 크기 버퍼 선언 자 뒤에 묶인 상수 식을 사용 하 여 멤버의 이름을 지정 하는 식별자 이루어져 `[` 고 `]` 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-388">A fixed size buffer declarator consists of an identifier that names the member, followed by a constant expression enclosed in `[` and `]` tokens.</span></span> <span data-ttu-id="0de11-389">상수 식은 해당 고정된 크기 버퍼 선언 자에 의해 정의 된 멤버의 요소 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-389">The constant expression denotes the number of elements in the member introduced by that fixed size buffer declarator.</span></span> <span data-ttu-id="0de11-390">상수 식의 형식은 형식으로 암시적으로 변환할 수 있어야 합니다 `int`, 값 0이 아닌 양의 정수 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-390">The type of the constant expression must be implicitly convertible to type `int`, and the value must be a non-zero positive integer.</span></span>

<span data-ttu-id="0de11-391">고정된 크기 버퍼의 요소는 메모리에서 순차적으로 배치 보장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-391">The elements of a fixed size buffer are guaranteed to be laid out sequentially in memory.</span></span>

<span data-ttu-id="0de11-392">고정된 크기 버퍼를 여러 개 선언 하는 고정된 크기 버퍼 선언은 요소 형식과 동일한 특성을 사용 하는 단일 고정된 크기 버퍼 선언이 여러 번 선언 하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-392">A fixed size buffer declaration that declares multiple fixed size buffers is equivalent to multiple declarations of a single fixed size buffer declaration with the same attributes, and element types.</span></span> <span data-ttu-id="0de11-393">예</span><span class="sxs-lookup"><span data-stu-id="0de11-393">For example</span></span>

```csharp
unsafe struct A
{
   public fixed int x[5], y[10], z[100];
}
```

<span data-ttu-id="0de11-394">위의 식은 아래의 식과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-394">is equivalent to</span></span>

```csharp
unsafe struct A
{
   public fixed int x[5];
   public fixed int y[10];
   public fixed int z[100];
}
```

### <a name="fixed-size-buffers-in-expressions"></a><span data-ttu-id="0de11-395">식에서 고정된 크기 버퍼</span><span class="sxs-lookup"><span data-stu-id="0de11-395">Fixed size buffers in expressions</span></span>

<span data-ttu-id="0de11-396">멤버 조회 ([연산자](expressions.md#operators)) 고정된 된 크기의 버퍼 멤버 필드의 멤버 조회와 동일 하 게 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-396">Member lookup ([Operators](expressions.md#operators)) of a fixed size buffer member proceeds exactly like member lookup of a field.</span></span>

<span data-ttu-id="0de11-397">고정된 크기 버퍼를 사용 하는 식에서 참조할 수는 *simple_name* ([형식 유추](expressions.md#type-inference)) 또는 *member_access* ([컴파일 타임 검사 동적 오버 로드 확인](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="0de11-397">A fixed size buffer can be referenced in an expression using a *simple_name* ([Type inference](expressions.md#type-inference)) or a *member_access* ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span></span>

<span data-ttu-id="0de11-398">고정된 크기 버퍼 멤버는 단순한 이름으로 참조 되는 경우는 효과가 동일 형식의 멤버 액세스로 `this.I`여기서 `I` 고정된 크기 버퍼 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-398">When a fixed size buffer member is referenced as a simple name, the effect is the same as a member access of the form `this.I`, where `I` is the fixed size buffer member.</span></span>

<span data-ttu-id="0de11-399">형식의 멤버 액세스에서 `E.I`이면 `E` 구조체 형식 및 멤버 조회입니다 `I` 구조체 형식 하 게 식별 하는 고정된 크기 멤버 다음에 `E.I` 는 분류는 다음과 같이 계산:</span><span class="sxs-lookup"><span data-stu-id="0de11-399">In a member access of the form `E.I`, if `E` is of a struct type and a member lookup of `I` in that struct type identifies a fixed size member, then `E.I` is evaluated an classified as follows:</span></span>

*  <span data-ttu-id="0de11-400">경우 식 `E.I` 컴파일 타임 오류가 발생 하는 안전 하지 않은 컨텍스트에서 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-400">If the expression `E.I` does not occur in an unsafe context, a compile-time error occurs.</span></span>
*  <span data-ttu-id="0de11-401">경우 `E` 컴파일 타임 오류가 발생 하는 값으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-401">If `E` is classified as a value, a compile-time error occurs.</span></span>
*  <span data-ttu-id="0de11-402">그렇지 않고 `E` 변수인은 ([고정 및 고정 되지 않은 변수](unsafe-code.md#fixed-and-moveable-variables)) 및 식 `E.I` 아닙니다를 *fixed_pointer_initializer* ([고정 문을](unsafe-code.md#the-fixed-statement)), 컴파일 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-402">Otherwise, if `E` is a moveable variable ([Fixed and moveable variables](unsafe-code.md#fixed-and-moveable-variables)) and the expression `E.I` is not a *fixed_pointer_initializer* ([The fixed statement](unsafe-code.md#the-fixed-statement)), a compile-time error occurs.</span></span>
*  <span data-ttu-id="0de11-403">이 고, 그렇지 `E` 고정된 변수 참조 식의 결과 고정된 크기 버퍼 멤버의 첫 번째 요소에 대 한 포인터 `I` 에서 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-403">Otherwise, `E` references a fixed variable and the result of the expression is a pointer to the first element of the fixed size buffer member `I` in `E`.</span></span> <span data-ttu-id="0de11-404">결과 형식입니다 `S*`, 여기서 `S` 의 요소 형식인 `I`와 값으로 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-404">The result is of type `S*`, where `S` is the element type of `I`, and is classified as a value.</span></span>

<span data-ttu-id="0de11-405">고정된 크기 버퍼의 후속 요소는 첫 번째 요소에서 포인터 연산을 사용 하 여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-405">The subsequent elements of the fixed size buffer can be accessed using pointer operations from the first element.</span></span> <span data-ttu-id="0de11-406">배열에 대 한 액세스를 달리 고정된 크기 버퍼의 요소에 대 한 액세스는 안전 하지 않은 작업이 며 선택 범위가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-406">Unlike access to arrays, access to the elements of a fixed size buffer is an unsafe operation and is not range checked.</span></span>

<span data-ttu-id="0de11-407">다음 예제에서는 선언 하 고 고정된 크기 버퍼 멤버와 구조체를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-407">The following example declares and uses a struct with a fixed size buffer member.</span></span>

```csharp
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}

class Test
{
    unsafe static void PutString(string s, char* buffer, int bufSize) {
        int len = s.Length;
        if (len > bufSize) len = bufSize;
        for (int i = 0; i < len; i++) buffer[i] = s[i];
        for (int i = len; i < bufSize; i++) buffer[i] = (char)0;
    }

    unsafe static void Main()
    {
        Font f;
        f.size = 10;
        PutString("Times New Roman", f.name, 32);
    }
}
```

### <a name="definite-assignment-checking"></a><span data-ttu-id="0de11-408">한정 된 할당 검사</span><span class="sxs-lookup"><span data-stu-id="0de11-408">Definite assignment checking</span></span>

<span data-ttu-id="0de11-409">고정된 크기 버퍼는 한정 된 할당을 확인 하는 적용 되지 않습니다 ([한정 된 할당](variables.md#definite-assignment)), 고정된 크기 버퍼 멤버는 구조체 형식 변수를 검사 하는 한정 된 할당의 목적을 위해 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-409">Fixed size buffers are not subject to definite assignment checking ([Definite assignment](variables.md#definite-assignment)), and fixed size buffer members are ignored for purposes of definite assignment checking of struct type variables.</span></span>

<span data-ttu-id="0de11-410">고정된 크기 버퍼 멤버의 포함 된 가장 바깥쪽 구조체 변수 정적 변수, 배열 요소 또는 클래스 인스턴스를 인스턴스 변수 경우 고정된 크기 버퍼의 요소는 자동으로 기본값으로 초기화 됩니다 ([기본값](variables.md#default-values)).</span><span class="sxs-lookup"><span data-stu-id="0de11-410">When the outermost containing struct variable of a fixed size buffer member is a static variable, an instance variable of a class instance, or an array element, the elements of the fixed size buffer are automatically initialized to their default values ([Default values](variables.md#default-values)).</span></span> <span data-ttu-id="0de11-411">다른 모든 경우에는 고정된 크기 버퍼의 초기 콘텐츠 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-411">In all other cases, the initial content of a fixed size buffer is undefined.</span></span>

## <a name="stack-allocation"></a><span data-ttu-id="0de11-412">스택 할당</span><span class="sxs-lookup"><span data-stu-id="0de11-412">Stack allocation</span></span>

<span data-ttu-id="0de11-413">안전 하지 않은 컨텍스트에서 지역 변수 선언 ([지역 변수 선언](statements.md#local-variable-declarations)) 호출 스택에서 메모리를 할당 하는 스택 할당 이니셜라이저를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-413">In an unsafe context, a local variable declaration ([Local variable declarations](statements.md#local-variable-declarations)) may include a stack allocation initializer which allocates memory from the call stack.</span></span>

```antlr
local_variable_initializer_unsafe
    : stackalloc_initializer
    ;

stackalloc_initializer
    : 'stackalloc' unmanaged_type '[' expression ']'
    ;
```

<span data-ttu-id="0de11-414">합니다 *unmanaged_type* 새로 할당 된 위치에 저장할 항목의 형식을 나타내는 하며 *식* 이러한 항목의 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-414">The *unmanaged_type* indicates the type of the items that will be stored in the newly allocated location, and the *expression* indicates the number of these items.</span></span> <span data-ttu-id="0de11-415">필요한 할당 크기를 지정 전체적으로 볼 때, 이러한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-415">Taken together, these specify the required allocation size.</span></span> <span data-ttu-id="0de11-416">이기 때문에 스택 할당의 크기는 음수일 수 없습니다, 항목의 수를 지정 하는 컴파일 시간 오류를 *constant_expression* 음수 값으로 계산 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-416">Since the size of a stack allocation cannot be negative, it is a compile-time error to specify the number of items as a *constant_expression* that evaluates to a negative value.</span></span>

<span data-ttu-id="0de11-417">폼의 스택 할당 이니셜라이저 `stackalloc T[E]` 필요 `T` 는 관리 되지 않는 형식 ([포인터 형식](unsafe-code.md#pointer-types)) 및 `E` 형식의 식으로 `int`입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-417">A stack allocation initializer of the form `stackalloc T[E]` requires `T` to be an unmanaged type ([Pointer types](unsafe-code.md#pointer-types)) and `E` to be an expression of type `int`.</span></span> <span data-ttu-id="0de11-418">할당 구문을 `E * sizeof(T)` 호출에서 바이트 스택 및 형식의 포인터를 반환 `T*`, 새로 할당 된 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-418">The construct allocates `E * sizeof(T)` bytes from the call stack and returns a pointer, of type `T*`, to the newly allocated block.</span></span> <span data-ttu-id="0de11-419">경우 `E` 음수 값 이면 동작이 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-419">If `E` is a negative value, then the behavior is undefined.</span></span> <span data-ttu-id="0de11-420">경우 `E` 가 0 이면 할당이 없습니다를 수행 하 고 반환 된 포인터는 구현 시 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-420">If `E` is zero, then no allocation is made, and the pointer returned is implementation-defined.</span></span> <span data-ttu-id="0de11-421">지정된 된 크기의 블록을 할당할 수 있는 충분 한 메모리가 없을 경우는 `System.StackOverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-421">If there is not enough memory available to allocate a block of the given size, a `System.StackOverflowException` is thrown.</span></span>

<span data-ttu-id="0de11-422">새로 할당 된 메모리의 내용을 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-422">The content of the newly allocated memory is undefined.</span></span>

<span data-ttu-id="0de11-423">스택 할당 이니셜라이저에 허용 되지 않는 `catch` 나 `finally` 블록 ([try 문](statements.md#the-try-statement)).</span><span class="sxs-lookup"><span data-stu-id="0de11-423">Stack allocation initializers are not permitted in `catch` or `finally` blocks ([The try statement](statements.md#the-try-statement)).</span></span>

<span data-ttu-id="0de11-424">명시적으로 사용 하 여 할당 된 메모리를 해제할 방법이 없기 `stackalloc`합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-424">There is no way to explicitly free memory allocated using `stackalloc`.</span></span> <span data-ttu-id="0de11-425">함수 멤버의 실행 중에 만들어진 모든 스택 할당 된 메모리 블록은 해당 하는 함수 멤버는 반환 될 때 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-425">All stack allocated memory blocks created during the execution of a function member are automatically discarded when that function member returns.</span></span> <span data-ttu-id="0de11-426">이에 해당 합니다 `alloca` 함수, C 및 c + + 구현에서 흔히 발견 되는 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-426">This corresponds to the `alloca` function, an extension commonly found in C and C++ implementations.</span></span>

<span data-ttu-id="0de11-427">예제</span><span class="sxs-lookup"><span data-stu-id="0de11-427">In the example</span></span>

```csharp
using System;

class Test
{
    static string IntToString(int value) {
        int n = value >= 0? value: -value;
        unsafe {
            char* buffer = stackalloc char[16];
            char* p = buffer + 16;
            do {
                *--p = (char)(n % 10 + '0');
                n /= 10;
            } while (n != 0);
            if (value < 0) *--p = '-';
            return new string(p, 0, (int)(buffer + 16 - p));
        }
    }

    static void Main() {
        Console.WriteLine(IntToString(12345));
        Console.WriteLine(IntToString(-999));
    }
}
```

<span data-ttu-id="0de11-428">`stackalloc` 이니셜라이저에 사용 되는 `IntToString` 스택에 16 자 버퍼를 할당 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="0de11-428">a `stackalloc` initializer is used in the `IntToString` method to allocate a buffer of 16 characters on the stack.</span></span> <span data-ttu-id="0de11-429">버퍼의 메서드가 반환 될 때 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-429">The buffer is automatically discarded when the method returns.</span></span>

## <a name="dynamic-memory-allocation"></a><span data-ttu-id="0de11-430">동적 메모리 할당</span><span class="sxs-lookup"><span data-stu-id="0de11-430">Dynamic memory allocation</span></span>

<span data-ttu-id="0de11-431">제외 하 고는 `stackalloc` 아닌 가비지 수집 된 메모리를 관리 하기 위한 미리 정의 된 구문은 없습니다 연산자, C# 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-431">Except for the `stackalloc` operator, C# provides no predefined constructs for managing non-garbage collected memory.</span></span> <span data-ttu-id="0de11-432">이러한 서비스는 일반적으로 클래스 라이브러리를 지원 하 여 제공 하거나 기본 운영 체제에서 직접 가져온 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-432">Such services are typically provided by supporting class libraries or imported directly from the underlying operating system.</span></span> <span data-ttu-id="0de11-433">예를 들어는 `Memory` 아래 클래스 C#에서 기본 운영 체제의 힙 함수를 어떻게 액세스할 수 있는지 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-433">For example, the `Memory` class below illustrates how the heap functions of an underlying operating system might be accessed from C#:</span></span>

```csharp
using System;
using System.Runtime.InteropServices;

public unsafe class Memory
{
    // Handle for the process heap. This handle is used in all calls to the
    // HeapXXX APIs in the methods below.
    static int ph = GetProcessHeap();

    // Private instance constructor to prevent instantiation.
    private Memory() {}

    // Allocates a memory block of the given size. The allocated memory is
    // automatically initialized to zero.
    public static void* Alloc(int size) {
        void* result = HeapAlloc(ph, HEAP_ZERO_MEMORY, size);
        if (result == null) throw new OutOfMemoryException();
        return result;
    }

    // Copies count bytes from src to dst. The source and destination
    // blocks are permitted to overlap.
    public static void Copy(void* src, void* dst, int count) {
        byte* ps = (byte*)src;
        byte* pd = (byte*)dst;
        if (ps > pd) {
            for (; count != 0; count--) *pd++ = *ps++;
        }
        else if (ps < pd) {
            for (ps += count, pd += count; count != 0; count--) *--pd = *--ps;
        }
    }

    // Frees a memory block.
    public static void Free(void* block) {
        if (!HeapFree(ph, 0, block)) throw new InvalidOperationException();
    }

    // Re-allocates a memory block. If the reallocation request is for a
    // larger size, the additional region of memory is automatically
    // initialized to zero.
    public static void* ReAlloc(void* block, int size) {
        void* result = HeapReAlloc(ph, HEAP_ZERO_MEMORY, block, size);
        if (result == null) throw new OutOfMemoryException();
        return result;
    }

    // Returns the size of a memory block.
    public static int SizeOf(void* block) {
        int result = HeapSize(ph, 0, block);
        if (result == -1) throw new InvalidOperationException();
        return result;
    }

    // Heap API flags
    const int HEAP_ZERO_MEMORY = 0x00000008;

    // Heap API functions
    [DllImport("kernel32")]
    static extern int GetProcessHeap();

    [DllImport("kernel32")]
    static extern void* HeapAlloc(int hHeap, int flags, int size);

    [DllImport("kernel32")]
    static extern bool HeapFree(int hHeap, int flags, void* block);

    [DllImport("kernel32")]
    static extern void* HeapReAlloc(int hHeap, int flags, void* block, int size);

    [DllImport("kernel32")]
    static extern int HeapSize(int hHeap, int flags, void* block);
}
```

<span data-ttu-id="0de11-434">사용 하는 예제는 `Memory` 클래스는 아래에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-434">An example that uses the `Memory` class is given below:</span></span>

```csharp
class Test
{
    static void Main() {
        unsafe {
            byte* buffer = (byte*)Memory.Alloc(256);
            try {
                for (int i = 0; i < 256; i++) buffer[i] = (byte)i;
                byte[] array = new byte[256];
                fixed (byte* p = array) Memory.Copy(buffer, p, 256); 
            }
            finally {
                Memory.Free(buffer);
            }
            for (int i = 0; i < 256; i++) Console.WriteLine(array[i]);
        }
    }
}
```

<span data-ttu-id="0de11-435">이 예제에서는 할당을 통해 메모리의 256 바이트 `Memory.Alloc` 0에서 255 개로 증가 하는 값을 사용 하 여 메모리 블록을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-435">The example allocates 256 bytes of memory through `Memory.Alloc` and initializes the memory block with values increasing from 0 to 255.</span></span> <span data-ttu-id="0de11-436">그런 다음 요소 256 바이트 배열을 할당 하 고 사용 하 여 `Memory.Copy` 메모리 블록의 내용을 바이트 배열로 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-436">It then allocates a 256 element byte array and uses `Memory.Copy` to copy the contents of the memory block into the byte array.</span></span> <span data-ttu-id="0de11-437">마지막으로, 메모리 블록을 사용 하 여 해제 됩니다 `Memory.Free` 및 바이트 배열의 내용을 콘솔에 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de11-437">Finally, the memory block is freed using `Memory.Free` and the contents of the byte array are output on the console.</span></span>
