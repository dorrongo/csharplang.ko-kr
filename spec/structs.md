# <a name="structs"></a><span data-ttu-id="8bfd0-101">구조체</span><span class="sxs-lookup"><span data-stu-id="8bfd0-101">Structs</span></span>

<span data-ttu-id="8bfd0-102">구조체는 데이터 멤버 및 함수 멤버를 포함할 수 있는 데이터 구조를 나타낸다는 점에서 클래스와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-102">Structs are similar to classes in that they represent data structures that can contain data members and function members.</span></span> <span data-ttu-id="8bfd0-103">그러나 클래스와 달리 구조체 값 형식이 며 힙 할당이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-103">However, unlike classes, structs are value types and do not require heap allocation.</span></span> <span data-ttu-id="8bfd0-104">구조체 형식의 변수는 클래스 형식의 변수 라고 개체 데이터에 대 한 참조를 포함 하는 반면 직접 구조체의 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-104">A variable of a struct type directly contains the data of the struct, whereas a variable of a class type contains a reference to the data, the latter known as an object.</span></span>

<span data-ttu-id="8bfd0-105">구조체는 값 의미 체계를 갖는 작은 데이터 구조에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-105">Structs are particularly useful for small data structures that have value semantics.</span></span> <span data-ttu-id="8bfd0-106">복소수, 좌표계의 점 또는 사전의 키-값 쌍이 모두 구조체의 좋은 예입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-106">Complex numbers, points in a coordinate system, or key-value pairs in a dictionary are all good examples of structs.</span></span> <span data-ttu-id="8bfd0-107">이러한 데이터 구조에는 키 몇 가지 데이터 멤버의 상속 또는 참조 id를 사용 하 여 필요 하지 않습니다는 편리 하 게 구현할 수 할당에서 참조 하는 대신 값을 복사 하는 위치 값 의미 체계를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-107">Key to these data structures is that they have few data members, that they do not require use of inheritance or referential identity, and that they can be conveniently implemented using value semantics where assignment copies the value instead of the reference.</span></span>

<span data-ttu-id="8bfd0-108">에 설명 된 대로 [단순 형식](types.md#simple-types)와 같은 C#에서 제공 하는 단순 형식을 `int`를 `double`, 및 `bool`은 실제로 모든 구조체 형식은입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-108">As described in [Simple types](types.md#simple-types), the simple types provided by C#, such as `int`, `double`, and `bool`, are in fact all struct types.</span></span> <span data-ttu-id="8bfd0-109">과 마찬가지로 이러한 미리 정의 된 형식은 구조체, 구조체 및 C# 언어에서 새 "기본" 형식을 구현 하는 오버 로드 된 연산자를 사용할 수 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-109">Just as these predefined types are structs, it is also possible to use structs and operator overloading to implement new "primitive" types in the C# language.</span></span> <span data-ttu-id="8bfd0-110">이러한 형식의 두 가지 예는이 장의 끝에 제공 됩니다 ([구조체 예제](structs.md#struct-examples)).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-110">Two examples of such types are given at the end of this chapter ([Struct examples](structs.md#struct-examples)).</span></span>

## <a name="struct-declarations"></a><span data-ttu-id="8bfd0-111">구조체 선언</span><span class="sxs-lookup"><span data-stu-id="8bfd0-111">Struct declarations</span></span>

<span data-ttu-id="8bfd0-112">A *struct_declaration* 되는 *type_declaration* ([형식 선언을](namespaces.md#type-declarations)) 새 구조체를 선언 하는:</span><span class="sxs-lookup"><span data-stu-id="8bfd0-112">A *struct_declaration* is a *type_declaration* ([Type declarations](namespaces.md#type-declarations)) that declares a new struct:</span></span>

```antlr
struct_declaration
    : attributes? struct_modifier* 'partial'? 'struct' identifier type_parameter_list?
      struct_interfaces? type_parameter_constraints_clause* struct_body ';'?
    ;
```

<span data-ttu-id="8bfd0-113">A *struct_declaration* 선택적 집합으로 이루어져 *특성* ([특성](attributes.md))의 선택적 집합 뒤에, *struct_modifier*s ([구조체 한정자](structs.md#struct-modifiers)), 선택적 `partial` 키워드 뒤에 한정자 `struct` 및 *식별자* 구조체 뒤에 이름을 지정 하는 선택적 *type_parameter_list* 사양 ([형식 매개 변수](classes.md#type-parameters)), 선택적 *struct_interfaces* 사양 ([Partial 한정자](structs.md#partial-modifier))), 선택적 *type_parameter_constraints_clause*s 사양 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)) 고 뒤에 *struct_body* ([구조체 본문](structs.md#struct-body)), 세미콜론 뒤에 선택적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-113">A *struct_declaration* consists of an optional set of *attributes* ([Attributes](attributes.md)), followed by an optional set of *struct_modifier*s ([Struct modifiers](structs.md#struct-modifiers)), followed by an optional `partial` modifier, followed by the keyword `struct` and an *identifier* that names the struct, followed by an optional *type_parameter_list* specification ([Type parameters](classes.md#type-parameters)), followed by an optional *struct_interfaces* specification ([Partial modifier](structs.md#partial-modifier)) ), followed by an optional *type_parameter_constraints_clause*s specification ([Type parameter constraints](classes.md#type-parameter-constraints)), followed by a *struct_body* ([Struct body](structs.md#struct-body)), optionally followed by a semicolon.</span></span>

### <a name="struct-modifiers"></a><span data-ttu-id="8bfd0-114">구조체 한정자</span><span class="sxs-lookup"><span data-stu-id="8bfd0-114">Struct modifiers</span></span>

<span data-ttu-id="8bfd0-115">A *struct_declaration* 구조체 한정자 시퀀스를 선택적으로 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-115">A *struct_declaration* may optionally include a sequence of struct modifiers:</span></span>

```antlr
struct_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | struct_modifier_unsafe
    ;
```

<span data-ttu-id="8bfd0-116">이 구조체 선언에 여러 번 표시 하는 동일한 한정자에 대 한 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-116">It is a compile-time error for the same modifier to appear multiple times in a struct declaration.</span></span>

<span data-ttu-id="8bfd0-117">구조체 선언 한정자 클래스 선언의 동일한 의미를 가집니다 ([클래스 선언을](classes.md#class-declarations)).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-117">The modifiers of a struct declaration have the same meaning as those of a class declaration ([Class declarations](classes.md#class-declarations)).</span></span>

### <a name="partial-modifier"></a><span data-ttu-id="8bfd0-118">Partial 한정자</span><span class="sxs-lookup"><span data-stu-id="8bfd0-118">Partial modifier</span></span>

<span data-ttu-id="8bfd0-119">합니다 `partial` 한정자가 나타내는이 *struct_declaration* 부분 형식 선언입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-119">The `partial` modifier indicates that this *struct_declaration* is a partial type declaration.</span></span> <span data-ttu-id="8bfd0-120">에 지정 된 규칙에 따라 구조체 선언 하나를 바깥쪽 네임 스페이스 또는 형식을 선언 내에서 동일한 이름 가진 여러 partial 구조체 선언 결합 [부분 형식](classes.md#partial-types)합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-120">Multiple partial struct declarations with the same name within an enclosing namespace or type declaration combine to form one struct declaration, following the rules specified in [Partial types](classes.md#partial-types).</span></span>

### <a name="struct-interfaces"></a><span data-ttu-id="8bfd0-121">구조체 인터페이스</span><span class="sxs-lookup"><span data-stu-id="8bfd0-121">Struct interfaces</span></span>

<span data-ttu-id="8bfd0-122">구조체 선언 포함 될 수 있습니다는 *struct_interfaces* 사양에 지정된 된 인터페이스 형식을 직접 구현할 경우 구조체 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-122">A struct declaration may include a *struct_interfaces* specification, in which case the struct is said to directly implement the given interface types.</span></span>

```antlr
struct_interfaces
    : ':' interface_type_list
    ;
```

<span data-ttu-id="8bfd0-123">인터페이스 구현을 설명에 대 한 자세한 [인터페이스 구현을](interfaces.md#interface-implementations)합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-123">Interface implementations are discussed further in [Interface implementations](interfaces.md#interface-implementations).</span></span>

### <a name="struct-body"></a><span data-ttu-id="8bfd0-124">구조체 본문</span><span class="sxs-lookup"><span data-stu-id="8bfd0-124">Struct body</span></span>

<span data-ttu-id="8bfd0-125">합니다 *struct_body* 구조체의 구조체의 멤버를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-125">The *struct_body* of a struct defines the members of the struct.</span></span>

```antlr
struct_body
    : '{' struct_member_declaration* '}'
    ;
```

## <a name="struct-members"></a><span data-ttu-id="8bfd0-126">구조체 멤버</span><span class="sxs-lookup"><span data-stu-id="8bfd0-126">Struct members</span></span>

<span data-ttu-id="8bfd0-127">구조체의 멤버 구성에서 도입 된 멤버의 해당 *struct_member_declaration*형식에서 상속 된 멤버 및 `System.ValueType`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-127">The members of a struct consist of the members introduced by its *struct_member_declaration*s and the members inherited from the type `System.ValueType`.</span></span>

```antlr
struct_member_declaration
    : constant_declaration
    | field_declaration
    | method_declaration
    | property_declaration
    | event_declaration
    | indexer_declaration
    | operator_declaration
    | constructor_declaration
    | static_constructor_declaration
    | type_declaration
    | struct_member_declaration_unsafe
    ;
```

<span data-ttu-id="8bfd0-128">에 명시 된 차이점을 제외 하면 [클래스 및 구조체 차이점](structs.md#class-and-struct-differences)에 대 한 설명은에서 제공 하는 클래스 멤버 [클래스 멤버](classes.md#class-members) 를 통해 [반복기](classes.md#iterators) 구조체에 적용 멤버에도 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-128">Except for the differences noted in [Class and struct differences](structs.md#class-and-struct-differences), the descriptions of class members provided in [Class members](classes.md#class-members) through [Iterators](classes.md#iterators) apply to struct members as well.</span></span>

## <a name="class-and-struct-differences"></a><span data-ttu-id="8bfd0-129">클래스 및 구조체 차이점</span><span class="sxs-lookup"><span data-stu-id="8bfd0-129">Class and struct differences</span></span>

<span data-ttu-id="8bfd0-130">구조체는 몇 가지 주요 방식에서 클래스와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-130">Structs differ from classes in several important ways:</span></span>

*  <span data-ttu-id="8bfd0-131">구조체는 값 형식 ([의미 체계를 값](structs.md#value-semantics)).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-131">Structs are value types ([Value semantics](structs.md#value-semantics)).</span></span>
*  <span data-ttu-id="8bfd0-132">클래스에서 암시적으로 상속 된 모든 구조체 형식은 `System.ValueType` ([상속](structs.md#inheritance)).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-132">All struct types implicitly inherit from the class `System.ValueType` ([Inheritance](structs.md#inheritance)).</span></span>
*  <span data-ttu-id="8bfd0-133">구조체 형식의 변수에 할당 되 고 할당 된 값의 복사본을 만듭니다 ([할당](structs.md#assignment)).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-133">Assignment to a variable of a struct type creates a copy of the value being assigned ([Assignment](structs.md#assignment)).</span></span>
*  <span data-ttu-id="8bfd0-134">구조체의 기본 값 형식 필드를 기본값으로 및 모든 참조를 모든 값 형식 필드를 설정 하 여 생성 된 값인 `null` ([기본값](structs.md#default-values)).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-134">The default value of a struct is the value produced by setting all value type fields to their default value and all reference type fields to `null` ([Default values](structs.md#default-values)).</span></span>
*  <span data-ttu-id="8bfd0-135">Boxing 및 unboxing 연산을 구조체 형식 간의 변환에 사용 되 고 `object` ([Boxing 및 unboxing](structs.md#boxing-and-unboxing)).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-135">Boxing and unboxing operations are used to convert between a struct type and `object` ([Boxing and unboxing](structs.md#boxing-and-unboxing)).</span></span>
*  <span data-ttu-id="8bfd0-136">의미 `this` 구조체에 대 한 다른 ([이 액세스](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-136">The meaning of `this` is different for structs ([This access](expressions.md#this-access)).</span></span>
*  <span data-ttu-id="8bfd0-137">구조체에 대 한 인스턴스 필드 선언을 변수 이니셜라이저를 포함할 수 없습니다 ([이니셜라이저 필드](structs.md#field-initializers)).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-137">Instance field declarations for a struct are not permitted to include variable initializers ([Field initializers](structs.md#field-initializers)).</span></span>
*  <span data-ttu-id="8bfd0-138">구조체에는 매개 변수가 없는 인스턴스 생성자를 선언할 수 없습니다 ([생성자](structs.md#constructors)).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-138">A struct is not permitted to declare a parameterless instance constructor ([Constructors](structs.md#constructors)).</span></span>
*  <span data-ttu-id="8bfd0-139">구조체에는 소멸자를 선언할 수 없습니다 ([소멸자](structs.md#destructors)).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-139">A struct is not permitted to declare a destructor ([Destructors](structs.md#destructors)).</span></span>

### <a name="value-semantics"></a><span data-ttu-id="8bfd0-140">값 의미 체계</span><span class="sxs-lookup"><span data-stu-id="8bfd0-140">Value semantics</span></span>

<span data-ttu-id="8bfd0-141">구조체는 값 형식 ([값 형식](types.md#value-types)) 값 의미를 갖는 된다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-141">Structs are value types ([Value types](types.md#value-types)) and are said to have value semantics.</span></span> <span data-ttu-id="8bfd0-142">클래스, 다른 한편으로 참조 형식 ([형식을 참조](types.md#reference-types)) 참조 의미 체계가 된다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-142">Classes, on the other hand, are reference types ([Reference types](types.md#reference-types)) and are said to have reference semantics.</span></span>

<span data-ttu-id="8bfd0-143">구조체 형식의 변수는 클래스 형식의 변수 라고 개체 데이터에 대 한 참조를 포함 하는 반면 직접 구조체의 데이터를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-143">A variable of a struct type directly contains the data of the struct, whereas a variable of a class type contains a reference to the data, the latter known as an object.</span></span> <span data-ttu-id="8bfd0-144">경우 구조체 `B` 형식의 인스턴스 필드를 포함 `A` 및 `A` 구조체 형식에 대 한 컴파일 시간 오류가 발생 `A` 에 따라 달라 지도록 `B` 에서 생성 된 형식 또는 `B`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-144">When a struct `B` contains an instance field of type `A` and `A` is a struct type, it is a compile-time error for `A` to depend on `B` or a type constructed from `B`.</span></span> <span data-ttu-id="8bfd0-145">구조체 `X` ***에 직접 종속*** 구조체 `Y` 하는 경우 `X` 형식의 인스턴스 필드를 포함 `Y`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-145">A struct `X` ***directly depends on*** a struct `Y` if `X` contains an instance field of type `Y`.</span></span> <span data-ttu-id="8bfd0-146">이 정의 지정 된 구조체 종속 된 구조체의 전체 집합은의 전이적 closure를 ***에 직접 종속*** 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-146">Given this definition, the complete set of structs upon which a struct depends is the transitive closure of the ***directly depends on*** relationship.</span></span>  <span data-ttu-id="8bfd0-147">예</span><span class="sxs-lookup"><span data-stu-id="8bfd0-147">For example</span></span>
```csharp
struct Node
{
    int data;
    Node next; // error, Node directly depends on itself
}
```
<span data-ttu-id="8bfd0-148">때문에 오류가 발생 하는 `Node` 자체 형식의 인스턴스 필드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-148">is an error because `Node` contains an instance field of its own type.</span></span>  <span data-ttu-id="8bfd0-149">또 다른 예</span><span class="sxs-lookup"><span data-stu-id="8bfd0-149">Another example</span></span>
```csharp
struct A { B b; }

struct B { C c; }

struct C { A a; }
```
<span data-ttu-id="8bfd0-150">때문에 오류가 발생 하는 각 유형의 `A`, `B`, 및 `C` 서로에 의존 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-150">is an error because each of the types `A`, `B`, and `C` depend on each other.</span></span>

<span data-ttu-id="8bfd0-151">클래스를 사용 하 여 이며 두 가지 변수가 같은 개체를 참조할 수 있으므로 작업이 다른 변수에서 참조 하는 개체에 적용할 한 변수에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-151">With classes, it is possible for two variables to reference the same object, and thus possible for operations on one variable to affect the object referenced by the other variable.</span></span> <span data-ttu-id="8bfd0-152">각 변수 구조체를 사용 하 여 데이터의 자체 복사본을가지고 (의 경우를 제외 하 고 `ref` 및 `out` 매개 변수), 이므로 작업에 다른 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-152">With structs, the variables each have their own copy of the data (except in the case of `ref` and `out` parameter variables), and it is not possible for operations on one to affect the other.</span></span> <span data-ttu-id="8bfd0-153">또한 구조체는 참조 형식 때문에 불가능 되도록 구조체 형식의 값에 대 한 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-153">Furthermore, because structs are not reference types, it is not possible for values of a struct type to be `null`.</span></span>

<span data-ttu-id="8bfd0-154">선언 된 경우</span><span class="sxs-lookup"><span data-stu-id="8bfd0-154">Given the declaration</span></span>
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
<span data-ttu-id="8bfd0-155">코드 조각</span><span class="sxs-lookup"><span data-stu-id="8bfd0-155">the code fragment</span></span>
```csharp
Point a = new Point(10, 10);
Point b = a;
a.x = 100;
System.Console.WriteLine(b.x);
```
<span data-ttu-id="8bfd0-156">값을 출력 합니다 `10`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-156">outputs the value `10`.</span></span> <span data-ttu-id="8bfd0-157">할당 `a` 하 `b` 값의 복사본을 만듭니다 및 `b` 따라서 할당 하는 영향을 받지 않습니다 `a.x`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-157">The assignment of `a` to `b` creates a copy of the value, and `b` is thus unaffected by the assignment to `a.x`.</span></span> <span data-ttu-id="8bfd0-158">했습니다 `Point` 대신 된 클래스로 선언 출력 됩니다. `100` 있으므로 `a` 및 `b` 동일한 개체를 참조 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-158">Had `Point` instead been declared as a class, the output would be `100` because `a` and `b` would reference the same object.</span></span>

### <a name="inheritance"></a><span data-ttu-id="8bfd0-159">상속</span><span class="sxs-lookup"><span data-stu-id="8bfd0-159">Inheritance</span></span>

<span data-ttu-id="8bfd0-160">클래스에서 암시적으로 상속 된 모든 구조체 형식은 `System.ValueType`는 클래스에서 상속 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-160">All struct types implicitly inherit from the class `System.ValueType`, which, in turn, inherits from class `object`.</span></span> <span data-ttu-id="8bfd0-161">구조체 선언에는 구현 된 인터페이스의 목록을 지정할 수 있습니다 하지만 기본 클래스를 지정 하는 구조체 선언에 대 한 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-161">A struct declaration may specify a list of implemented interfaces, but it is not possible for a struct declaration to specify a base class.</span></span>

<span data-ttu-id="8bfd0-162">구조체 형식은 추상 되지 며 항상 암시적으로 봉인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-162">Struct types are never abstract and are always implicitly sealed.</span></span> <span data-ttu-id="8bfd0-163">합니다 `abstract` 고 `sealed` 한정자는 따라서 구조체 선언에서 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-163">The `abstract` and `sealed` modifiers are therefore not permitted in a struct declaration.</span></span>

<span data-ttu-id="8bfd0-164">구조체 멤버의 선언 된 접근성이 될 수 없습니다 구조체에 대 한 지원 되지 않습니다 상속 되므로 `protected` 또는 `protected internal`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-164">Since inheritance isn't supported for structs, the declared accessibility of a struct member cannot be `protected` or `protected internal`.</span></span>

<span data-ttu-id="8bfd0-165">구조체의 멤버 함수 일 수 없습니다 `abstract` 나 `virtual`, 및 `override` 에서 상속 된 메서드를 재정의할 경우에 한정자를 사용할 수 `System.ValueType`입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-165">Function members in a struct cannot be `abstract` or `virtual`, and the `override` modifier is allowed only to override methods inherited from `System.ValueType`.</span></span>

### <a name="assignment"></a><span data-ttu-id="8bfd0-166">할당</span><span class="sxs-lookup"><span data-stu-id="8bfd0-166">Assignment</span></span>

<span data-ttu-id="8bfd0-167">구조체 형식의 변수에 할당 되 고 할당 된 값의 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-167">Assignment to a variable of a struct type creates a copy of the value being assigned.</span></span> <span data-ttu-id="8bfd0-168">이 참조 하지만 참조에 의해 식별 된 개체를 복사 하는 클래스 형식의 변수에 할당에서 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-168">This differs from assignment to a variable of a class type, which copies the reference but not the object identified by the reference.</span></span>

<span data-ttu-id="8bfd0-169">할당에서 구조체를 값 매개 변수로 전달 하거나 함수 멤버의 결과로 반환 하는 경우와 마찬가지로 구조체의 복사본이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-169">Similar to an assignment, when a struct is passed as a value parameter or returned as the result of a function member, a copy of the struct is created.</span></span> <span data-ttu-id="8bfd0-170">구조체를 사용 하 여 함수 멤버에는 참조로 전달 될 수는 `ref` 또는 `out` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-170">A struct may be passed by reference to a function member using a `ref` or `out` parameter.</span></span>

<span data-ttu-id="8bfd0-171">구조체의 인덱서 나 속성에는 할당 대상일 때 속성 또는 인덱서 액세스와 관련 된 인스턴스 식이 변수로 분류 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-171">When a property or indexer of a struct is the target of an assignment, the instance expression associated with the property or indexer access must be classified as a variable.</span></span> <span data-ttu-id="8bfd0-172">인스턴스 식은 값으로 분류 됩니다, 컴파일 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-172">If the instance expression is classified as a value, a compile-time error occurs.</span></span> <span data-ttu-id="8bfd0-173">이에서 더 자세히 설명 [단순 할당](expressions.md#simple-assignment)합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-173">This is described in further detail in [Simple assignment](expressions.md#simple-assignment).</span></span>

### <a name="default-values"></a><span data-ttu-id="8bfd0-174">기본값</span><span class="sxs-lookup"><span data-stu-id="8bfd0-174">Default values</span></span>

<span data-ttu-id="8bfd0-175">에 설명 된 대로 [기본값](variables.md#default-values), 일부의 변수 생성 될 때 자동으로 기본값으로 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-175">As described in [Default values](variables.md#default-values), several kinds of variables are automatically initialized to their default value when they are created.</span></span> <span data-ttu-id="8bfd0-176">클래스 형식 및 다른 참조 형식 변수의 기본값은 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-176">For variables of class types and other reference types, this default value is `null`.</span></span> <span data-ttu-id="8bfd0-177">그러나 구조체는 사용할 수 없는 값 형식 이므로 `null`, 구조체의 기본 값 형식 필드를 기본값으로 및 모든 참조를 모든 값 형식 필드를 설정 하 여 생성 한 값은 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-177">However, since structs are value types that cannot be `null`, the default value of a struct is the value produced by setting all value type fields to their default value and all reference type fields to `null`.</span></span>

<span data-ttu-id="8bfd0-178">참조 하는 `Point` 위의 예제에서는 구조체 선언</span><span class="sxs-lookup"><span data-stu-id="8bfd0-178">Referring to the `Point` struct declared above, the example</span></span>
```csharp
Point[] a = new Point[100];
```
<span data-ttu-id="8bfd0-179">각 초기화 `Point` 설정 하 여 생성 한 값으로 배열에는 `x` 및 `y` 필드를 0으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-179">initializes each `Point` in the array to the value produced by setting the `x` and `y` fields to zero.</span></span>

<span data-ttu-id="8bfd0-180">구조체의 기본 생성자에서 반환 된 값에 해당 하는 구조체의 기본값 ([기본 생성자](types.md#default-constructors)).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-180">The default value of a struct corresponds to the value returned by the default constructor of the struct ([Default constructors](types.md#default-constructors)).</span></span> <span data-ttu-id="8bfd0-181">클래스와 달리 구조체는 매개 변수가 없는 인스턴스 생성자를 선언 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-181">Unlike a class, a struct is not permitted to declare a parameterless instance constructor.</span></span> <span data-ttu-id="8bfd0-182">모든 구조체가 항상 형식 필드를 기본값으로 및 모든 참조를 모든 값 형식 필드를 설정 하는 결과로 생성 되는 값을 반환 하는 매개 변수가 없는 인스턴스 생성자를 암시적으로 포함 하는 대신 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-182">Instead, every struct implicitly has a parameterless instance constructor which always returns the value that results from setting all value type fields to their default value and all reference type fields to `null`.</span></span>

<span data-ttu-id="8bfd0-183">구조체는 유효한 상태 기본 초기화 상태를 고려해 야 할 설계 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-183">Structs should be designed to consider the default initialization state a valid state.</span></span> <span data-ttu-id="8bfd0-184">예제</span><span class="sxs-lookup"><span data-stu-id="8bfd0-184">In the example</span></span>
```csharp
using System;

struct KeyValuePair
{
    string key;
    string value;

    public KeyValuePair(string key, string value) {
        if (key == null || value == null) throw new ArgumentException();
        this.key = key;
        this.value = value;
    }
}
```
<span data-ttu-id="8bfd0-185">사용자 정의 인스턴스 생성자만 호출 된 위치 명시적으로 null 값을 보호 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-185">the user-defined instance constructor protects against null values only where it is explicitly called.</span></span> <span data-ttu-id="8bfd0-186">경우에서 위치는 `KeyValuePair` 변수가 기본 값을 초기화 될 수 있습니다 합니다 `key` 및 `value` 필드는 null이 됩니다 및 구조체는이 상태를 처리할 준비가 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-186">In cases where a `KeyValuePair` variable is subject to default value initialization, the `key` and `value` fields will be null, and the struct must be prepared to handle this state.</span></span>

### <a name="boxing-and-unboxing"></a><span data-ttu-id="8bfd0-187">boxing 및 unboxing</span><span class="sxs-lookup"><span data-stu-id="8bfd0-187">Boxing and unboxing</span></span>

<span data-ttu-id="8bfd0-188">클래스 형식의 값을 형식으로 변환할 수 `object` 또는 컴파일 시간에 다른 형식으로 참조를 처리 하 여 클래스에 의해 구현 되는 인터페이스 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-188">A value of a class type can be converted to type `object` or to an interface type that is implemented by the class simply by treating the reference as another type at compile-time.</span></span> <span data-ttu-id="8bfd0-189">형식의 값 마찬가지로 `object` 또는 참조를 변경 하지 않고 클래스 형식으로 다시 변환할 수 인터페이스 형식의 값 (하지만 물론 런타임 형식 검사를 반드시이 경우).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-189">Likewise, a value of type `object` or a value of an interface type can be converted back to a class type without changing the reference (but of course a run-time type check is required in this case).</span></span>

<span data-ttu-id="8bfd0-190">구조체는 참조 형식 이므로 이러한 작업은 구조체 형식에 대해 다르게 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-190">Since structs are not reference types, these operations are implemented differently for struct types.</span></span> <span data-ttu-id="8bfd0-191">구조체 형식의 값 형식으로 변환 되 면 `object` 또는 구조체에서 구현 되는 인터페이스 형식으로 boxing 연산을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-191">When a value of a struct type is converted to type `object` or to an interface type that is implemented by the struct, a boxing operation takes place.</span></span> <span data-ttu-id="8bfd0-192">마찬가지로, 값 형식의 `object` 또는 인터페이스 형식의 값은 구조체 형식으로 다시 변환, unboxing 작업으로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-192">Likewise, when a value of type `object` or a value of an interface type is converted back to a struct type, an unboxing operation takes place.</span></span> <span data-ttu-id="8bfd0-193">클래스 형식에서 동일한 작업에서 주요한 차이점은 boxing 및 unboxing 복사 하는지 구조체 값을 내부 / 외부로 boxed 인스턴스</span><span class="sxs-lookup"><span data-stu-id="8bfd0-193">A key difference from the same operations on class types is that boxing and unboxing copies the struct value either into or out of the boxed instance.</span></span> <span data-ttu-id="8bfd0-194">즉, boxing 또는 unboxing 작업을 다음 변경 unboxed 구조체가 boxed 구조체에 반영 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-194">Thus, following a boxing or unboxing operation, changes made to the unboxed struct are not reflected in the boxed struct.</span></span>

<span data-ttu-id="8bfd0-195">구조체 형식에서 상속 된 가상 메서드를 재정의 하는 경우 `System.Object` (같은 `Equals`를 `GetHashCode`, 또는 `ToString`), 구조체 형식의 인스턴스를 통해 가상 메서드를 호출할 되려면 boxing 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-195">When a struct type overrides a virtual method inherited from `System.Object` (such as `Equals`, `GetHashCode`, or `ToString`), invocation of the virtual method through an instance of the struct type does not cause boxing to occur.</span></span> <span data-ttu-id="8bfd0-196">구조체 형식 매개 변수로 사용 되 고 형식 매개 변수 형식의 인스턴스를 통해 호출이 발생 하는 경우에 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-196">This is true even when the struct is used as a type parameter and the invocation occurs through an instance of the type parameter type.</span></span> <span data-ttu-id="8bfd0-197">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="8bfd0-197">For example:</span></span>
```csharp
using System;

struct Counter
{
    int value;

    public override string ToString() {
        value++;
        return value.ToString();
    }
}

class Program
{
    static void Test<T>() where T: new() {
        T x = new T();
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
    }

    static void Main() {
        Test<Counter>();
    }
}
```

<span data-ttu-id="8bfd0-198">프로그램의 출력이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-198">The output of the program is:</span></span>
```
1
2
3
```

<span data-ttu-id="8bfd0-199">잘못 된 스타일을 이지만 `ToString` 부작용을 보여 줍니다의 세 가지 호출에 대 한 boxing이 발생 했음을 `x.ToString()`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-199">Although it is bad style for `ToString` to have side effects, the example demonstrates that no boxing occurred for the three invocations of `x.ToString()`.</span></span>

<span data-ttu-id="8bfd0-200">제한 된 형식 매개 변수의 멤버에 액세스할 때 마찬가지로, 발생 하지 않습니다 암시적으로 boxing 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-200">Similarly, boxing never implicitly occurs when accessing a member on a constrained type parameter.</span></span> <span data-ttu-id="8bfd0-201">예를 들어 인터페이스로 `ICounter` 메서드를 포함 `Increment` 값을 수정에 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-201">For example, suppose an interface `ICounter` contains a method `Increment` which can be used to modify a value.</span></span> <span data-ttu-id="8bfd0-202">경우 `ICounter` 구현의 제약 조건으로 사용 되는 `Increment` 메서드는 변수에 대 한 참조를 사용 하 여는 `Increment` boxed 사본이 없습니다에서 호출 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-202">If `ICounter` is used as a constraint, the implementation of the `Increment` method is called with a reference to the variable that `Increment` was called on, never a boxed copy.</span></span>

```csharp
using System;

interface ICounter
{
    void Increment();
}

struct Counter: ICounter
{
    int value;

    public override string ToString() {
        return value.ToString();
    }

    void ICounter.Increment() {
        value++;
    }
}

class Program
{
    static void Test<T>() where T: ICounter, new() {
        T x = new T();
        Console.WriteLine(x);
        x.Increment();                    // Modify x
        Console.WriteLine(x);
        ((ICounter)x).Increment();        // Modify boxed copy of x
        Console.WriteLine(x);
    }

    static void Main() {
        Test<Counter>();
    }
}
```

<span data-ttu-id="8bfd0-203">첫 번째 호출은 `Increment` 변수의 값을 수정 `x`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-203">The first call to `Increment` modifies the value in the variable `x`.</span></span> <span data-ttu-id="8bfd0-204">두 번째 호출은 동일 하지 않습니다 `Increment`의 boxed 사본이의 값을 수정 하는 `x`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-204">This is not equivalent to the second call to `Increment`, which modifies the value in a boxed copy of `x`.</span></span> <span data-ttu-id="8bfd0-205">따라서 프로그램의 출력이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-205">Thus, the output of the program is:</span></span>
```
0
1
1
```

<span data-ttu-id="8bfd0-206">Boxing 및 unboxing 대 한 자세한 내용은 참조 하세요 [Boxing 및 unboxing](types.md#boxing-and-unboxing)합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-206">For further details on boxing and unboxing, see [Boxing and unboxing](types.md#boxing-and-unboxing).</span></span>

### <a name="meaning-of-this"></a><span data-ttu-id="8bfd0-207">이의 의미</span><span class="sxs-lookup"><span data-stu-id="8bfd0-207">Meaning of this</span></span>

<span data-ttu-id="8bfd0-208">인스턴스 생성자 또는 클래스의 인스턴스 함수 멤버 내에서 `this` 값으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-208">Within an instance constructor or instance function member of a class, `this` is classified as a value.</span></span> <span data-ttu-id="8bfd0-209">따라서 하는 동안 `this` 인스턴스를 참조할 수는 함수 멤버를 호출 하는 것에 대 한 불가능에 할당할 `this` 클래스의 함수 멤버에서입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-209">Thus, while `this` can be used to refer to the instance for which the function member was invoked, it is not possible to assign to `this` in a function member of a class.</span></span>

<span data-ttu-id="8bfd0-210">구조체의 인스턴스 생성자 내에서 `this` 에 해당 하는 `out` 매개 변수는 구조체 형식의 및 구조체의 인스턴스 함수 멤버 내 `this` 에 해당 하는 `ref` 구조체 형식의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-210">Within an instance constructor of a struct, `this` corresponds to an `out` parameter of the struct type, and within an instance function member of a struct, `this` corresponds to a `ref` parameter of the struct type.</span></span> <span data-ttu-id="8bfd0-211">두 경우 모두 `this` 변수에로 분류 됩니다을 할당 하 여 호출 된 함수 멤버는 전체 구조체를 수정 하는 것이 가능 하 고 `this` 으로 전달 하 여를 `ref` 또는 `out` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-211">In both cases, `this` is classified as a variable, and it is possible to modify the entire struct for which the function member was invoked by assigning to `this` or by passing this as a `ref` or `out` parameter.</span></span>

### <a name="field-initializers"></a><span data-ttu-id="8bfd0-212">필드 이니셜라이저</span><span class="sxs-lookup"><span data-stu-id="8bfd0-212">Field initializers</span></span>

<span data-ttu-id="8bfd0-213">에 설명 된 대로 [기본값](structs.md#default-values), 구조체의 기본 값 형식 필드를 기본값으로 및 모든 참조를 모든 값 형식 필드를 설정 하는 결과로 생성 되는 값의 구성 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-213">As described in [Default values](structs.md#default-values), the default value of a struct consists of the value that results from setting all value type fields to their default value and all reference type fields to `null`.</span></span> <span data-ttu-id="8bfd0-214">이러한 이유로 구조체 변수 이니셜라이저를 포함 하도록 인스턴스 필드 선언을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-214">For this reason, a struct does not permit instance field declarations to include variable initializers.</span></span> <span data-ttu-id="8bfd0-215">이 제한은 인스턴스 필드에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-215">This restriction applies only to instance fields.</span></span> <span data-ttu-id="8bfd0-216">구조체의 정적 필드는 변수 이니셜라이저를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-216">Static fields of a struct are permitted to include variable initializers.</span></span>

<span data-ttu-id="8bfd0-217">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="8bfd0-217">The example</span></span>
```csharp
struct Point
{
    public int x = 1;  // Error, initializer not permitted
    public int y = 1;  // Error, initializer not permitted
}
```
<span data-ttu-id="8bfd0-218">인스턴스 필드 선언과 변수 이니셜라이저를 포함 하기 때문에 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-218">is in error because the instance field declarations include variable initializers.</span></span>

### <a name="constructors"></a><span data-ttu-id="8bfd0-219">생성자</span><span class="sxs-lookup"><span data-stu-id="8bfd0-219">Constructors</span></span>

<span data-ttu-id="8bfd0-220">클래스와 달리 구조체는 매개 변수가 없는 인스턴스 생성자를 선언 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-220">Unlike a class, a struct is not permitted to declare a parameterless instance constructor.</span></span> <span data-ttu-id="8bfd0-221">모든 구조체가 항상 모든 값 형식 필드 기본값 및 모든 참조 형식 필드를 null로 설정 하는 결과로 생성 되는 값을 반환 하는 매개 변수가 없는 인스턴스 생성자를 암시적으로 포함 하는 대신 ([기본 생성자](types.md#default-constructors)).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-221">Instead, every struct implicitly has a parameterless instance constructor which always returns the value that results from setting all value type fields to their default value and all reference type fields to null ([Default constructors](types.md#default-constructors)).</span></span> <span data-ttu-id="8bfd0-222">구조체는 매개 변수가 있는 인스턴스 생성자를 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-222">A struct can declare instance constructors having parameters.</span></span> <span data-ttu-id="8bfd0-223">예</span><span class="sxs-lookup"><span data-stu-id="8bfd0-223">For example</span></span>
```csharp
struct Point
{
    int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

<span data-ttu-id="8bfd0-224">위의 선언, 명령문</span><span class="sxs-lookup"><span data-stu-id="8bfd0-224">Given the above declaration, the statements</span></span>
```csharp
Point p1 = new Point();
Point p2 = new Point(0, 0);
```
<span data-ttu-id="8bfd0-225">둘 다 만듭니다는 `Point` 사용 하 여 `x` 및 `y` 0으로 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-225">both create a `Point` with `x` and `y` initialized to zero.</span></span>

<span data-ttu-id="8bfd0-226">구조체 인스턴스 생성자가 폼의 생성자 이니셜라이저 수 없는 `base(...)`합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-226">A struct instance constructor is not permitted to include a constructor initializer of the form `base(...)`.</span></span>

<span data-ttu-id="8bfd0-227">구조체 인스턴스 생성자는 생성자 이니셜라이저를 지정 하지 않으면 합니다 `this` 에 해당 하는 변수를 `out` 유사 하 고는 구조체 형식의 매개 변수는 `out` 매개 변수를 `this` 할당 되어야 합니다 ( [한정 된 할당](variables.md#definite-assignment)) 생성자에서 반환 되는 모든 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-227">If the struct instance constructor doesn't specify a constructor initializer, the `this` variable corresponds to an `out` parameter of the struct type, and similar to an `out` parameter, `this` must be definitely assigned ([Definite assignment](variables.md#definite-assignment)) at every location where the constructor returns.</span></span> <span data-ttu-id="8bfd0-228">구조체 인스턴스 생성자를 사용 하는 생성자 이니셜라이저를 지정 하는 경우는 `this` 에 해당 하는 변수를 `ref` 유사 하 고는 구조체 형식의 매개 변수를 `ref` 매개 변수를 `this` 에 정적으로 할당 된 것으로 간주 됩니다 생성자 본문에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-228">If the struct instance constructor specifies a constructor initializer, the `this` variable corresponds to a `ref` parameter of the struct type, and similar to a `ref` parameter, `this` is considered definitely assigned on entry to the constructor body.</span></span> <span data-ttu-id="8bfd0-229">인스턴스 생성자 구현 아래 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-229">Consider the instance constructor implementation below:</span></span>
```csharp
struct Point
{
    int x, y;

    public int X {
        set { x = value; }
    }

    public int Y {
        set { y = value; }
    }

    public Point(int x, int y) {
        X = x;        // error, this is not yet definitely assigned
        Y = y;        // error, this is not yet definitely assigned
    }
}
```

<span data-ttu-id="8bfd0-230">없는 인스턴스 멤버 함수 (속성에 대 한 set 접근자를 포함 하 여 `X` 고 `Y`) 생성 되 고 있는 구조체의 모든 필드가 확실 하 게 할당 될 때까지 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-230">No instance member function (including the set accessors for the properties `X` and `Y`) can be called until all fields of the struct being constructed have been definitely assigned.</span></span> <span data-ttu-id="8bfd0-231">유일한 예외는 자동으로 구현 된 속성 ([자동으로 구현 된 속성](classes.md#automatically-implemented-properties)).</span><span class="sxs-lookup"><span data-stu-id="8bfd0-231">The only exception involves automatically implemented properties ([Automatically implemented properties](classes.md#automatically-implemented-properties)).</span></span> <span data-ttu-id="8bfd0-232">한정 된 할당 규칙 ([단순 할당 식](variables.md#simple-assignment-expressions)) 특히 해당 구조체 형식의 인스턴스 생성자 내에서 구조체 형식의 auto 속성에 할당을 제외 합니다: 이러한 할당을 한정 된 것으로 간주 됩니다 auto 속성의 숨겨진된 지원 필드의 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-232">The definite assignment rules ([Simple assignment expressions](variables.md#simple-assignment-expressions)) specifically exempt assignment to an auto-property of a struct type within an instance constructor of that struct type: such an assignment is considered a definite assignment of the hidden backing field of the auto-property.</span></span> <span data-ttu-id="8bfd0-233">따라서 다음은 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-233">Thus, the following is allowed:</span></span>

```csharp
struct Point
{
    public int X { get; set; }
    public int Y { get; set; }

    public Point(int x, int y) {
        X = x;      // allowed, definitely assigns backing field
        Y = y;      // allowed, definitely assigns backing field
    }
```

### <a name="destructors"></a><span data-ttu-id="8bfd0-234">소멸자</span><span class="sxs-lookup"><span data-stu-id="8bfd0-234">Destructors</span></span>

<span data-ttu-id="8bfd0-235">구조체는 소멸자를 선언 하는 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-235">A struct is not permitted to declare a destructor.</span></span>

### <a name="static-constructors"></a><span data-ttu-id="8bfd0-236">정적 생성자</span><span class="sxs-lookup"><span data-stu-id="8bfd0-236">Static constructors</span></span>

<span data-ttu-id="8bfd0-237">구조체에 대 한 정적 생성자에는 대부분의 클래스와 동일한 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-237">Static constructors for structs follow most of the same rules as for classes.</span></span> <span data-ttu-id="8bfd0-238">구조체 형식에 대 한 정적 생성자의 실행은 다음 이벤트 중 첫 번째 응용 프로그램 도메인 내에서 발생 하 여 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-238">The execution of a static constructor for a struct type is triggered by the first of the following events to occur within an application domain:</span></span>

*  <span data-ttu-id="8bfd0-239">구조체 형식의 정적 멤버로 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-239">A static member of the struct type is referenced.</span></span>
*  <span data-ttu-id="8bfd0-240">구조체 형식의 명시적으로 선언 된 생성자가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-240">An explicitly declared constructor of the struct type is called.</span></span>

<span data-ttu-id="8bfd0-241">기본값 만들기 ([기본값](structs.md#default-values)) 구조체의 형식을 정적 생성자를 트리거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-241">The creation of default values ([Default values](structs.md#default-values)) of struct types does not trigger the static constructor.</span></span> <span data-ttu-id="8bfd0-242">(이 예로 배열에 있는 요소의 초기 값입니다.)</span><span class="sxs-lookup"><span data-stu-id="8bfd0-242">(An example of this is the initial value of elements in an array.)</span></span>

## <a name="struct-examples"></a><span data-ttu-id="8bfd0-243">구조체 예제</span><span class="sxs-lookup"><span data-stu-id="8bfd0-243">Struct examples</span></span>

<span data-ttu-id="8bfd0-244">다음은 사용 하는 두 가지 중요 한 예가 `struct` 유사 하지만 수정 된 의미 체계 언어의 미리 정의 된 형식에 사용할 수 있는 형식을 만드는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-244">The following shows two significant examples of using `struct` types to create types that can be used similarly to the predefined types of the language, but with modified semantics.</span></span>

### <a name="database-integer-type"></a><span data-ttu-id="8bfd0-245">데이터베이스 정수 형식</span><span class="sxs-lookup"><span data-stu-id="8bfd0-245">Database integer type</span></span>

<span data-ttu-id="8bfd0-246">합니다 `DBInt` 구조체의 값의 전체 집합을 나타낼 수 있는 정수 형식 구현를 `int` 형식과 알 수 없는 값을 나타내는 추가 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-246">The `DBInt` struct below implements an integer type that can represent the complete set of values of the `int` type, plus an additional state that indicates an unknown value.</span></span> <span data-ttu-id="8bfd0-247">이러한 특성을 사용 하 여 형식은 데이터베이스에서 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-247">A type with these characteristics is commonly used in databases.</span></span>

```csharp
using System;

public struct DBInt
{
    // The Null member represents an unknown DBInt value.

    public static readonly DBInt Null = new DBInt();

    // When the defined field is true, this DBInt represents a known value
    // which is stored in the value field. When the defined field is false,
    // this DBInt represents an unknown value, and the value field is 0.

    int value;
    bool defined;

    // Private instance constructor. Creates a DBInt with a known value.

    DBInt(int value) {
        this.value = value;
        this.defined = true;
    }

    // The IsNull property is true if this DBInt represents an unknown value.

    public bool IsNull { get { return !defined; } }

    // The Value property is the known value of this DBInt, or 0 if this
    // DBInt represents an unknown value.

    public int Value { get { return value; } }

    // Implicit conversion from int to DBInt.

    public static implicit operator DBInt(int x) {
        return new DBInt(x);
    }

    // Explicit conversion from DBInt to int. Throws an exception if the
    // given DBInt represents an unknown value.

    public static explicit operator int(DBInt x) {
        if (!x.defined) throw new InvalidOperationException();
        return x.value;
    }

    public static DBInt operator +(DBInt x) {
        return x;
    }

    public static DBInt operator -(DBInt x) {
        return x.defined ? -x.value : Null;
    }

    public static DBInt operator +(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value + y.value: Null;
    }

    public static DBInt operator -(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value - y.value: Null;
    }

    public static DBInt operator *(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value * y.value: Null;
    }

    public static DBInt operator /(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value / y.value: Null;
    }

    public static DBInt operator %(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value % y.value: Null;
    }

    public static DBBool operator ==(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value == y.value: DBBool.Null;
    }

    public static DBBool operator !=(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value != y.value: DBBool.Null;
    }

    public static DBBool operator >(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value > y.value: DBBool.Null;
    }

    public static DBBool operator <(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value < y.value: DBBool.Null;
    }

    public static DBBool operator >=(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value >= y.value: DBBool.Null;
    }

    public static DBBool operator <=(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value <= y.value: DBBool.Null;
    }

    public override bool Equals(object obj) {
        if (!(obj is DBInt)) return false;
        DBInt x = (DBInt)obj;
        return value == x.value && defined == x.defined;
    }

    public override int GetHashCode() {
        return value;
    }

    public override string ToString() {
        return defined? value.ToString(): "DBInt.Null";
    }
}
```

### <a name="database-boolean-type"></a><span data-ttu-id="8bfd0-248">데이터베이스 부울 유형</span><span class="sxs-lookup"><span data-stu-id="8bfd0-248">Database boolean type</span></span>

<span data-ttu-id="8bfd0-249">`DBBool` 구조체 3 중 값 논리 형식을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-249">The `DBBool` struct below implements a three-valued logical type.</span></span> <span data-ttu-id="8bfd0-250">이러한 종류의 가능한 값은 `DBBool.True`, `DBBool.False`, 및 `DBBool.Null`여기서는 `Null` 멤버 알 수 없는 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-250">The possible values of this type are `DBBool.True`, `DBBool.False`, and `DBBool.Null`, where the `Null` member indicates an unknown value.</span></span> <span data-ttu-id="8bfd0-251">이러한 세 개의 값 논리 형식은 데이터베이스에서 자주 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bfd0-251">Such three-valued logical types are commonly used in databases.</span></span>

```csharp
using System;

public struct DBBool
{
    // The three possible DBBool values.

    public static readonly DBBool Null = new DBBool(0);
    public static readonly DBBool False = new DBBool(-1);
    public static readonly DBBool True = new DBBool(1);

    // Private field that stores -1, 0, 1 for False, Null, True.

    sbyte value;

    // Private instance constructor. The value parameter must be -1, 0, or 1.

    DBBool(int value) {
        this.value = (sbyte)value;
    }

    // Properties to examine the value of a DBBool. Return true if this
    // DBBool has the given value, false otherwise.

    public bool IsNull { get { return value == 0; } }

    public bool IsFalse { get { return value < 0; } }

    public bool IsTrue { get { return value > 0; } }

    // Implicit conversion from bool to DBBool. Maps true to DBBool.True and
    // false to DBBool.False.

    public static implicit operator DBBool(bool x) {
        return x? True: False;
    }

    // Explicit conversion from DBBool to bool. Throws an exception if the
    // given DBBool is Null, otherwise returns true or false.

    public static explicit operator bool(DBBool x) {
        if (x.value == 0) throw new InvalidOperationException();
        return x.value > 0;
    }

    // Equality operator. Returns Null if either operand is Null, otherwise
    // returns True or False.

    public static DBBool operator ==(DBBool x, DBBool y) {
        if (x.value == 0 || y.value == 0) return Null;
        return x.value == y.value? True: False;
    }

    // Inequality operator. Returns Null if either operand is Null, otherwise
    // returns True or False.

    public static DBBool operator !=(DBBool x, DBBool y) {
        if (x.value == 0 || y.value == 0) return Null;
        return x.value != y.value? True: False;
    }

    // Logical negation operator. Returns True if the operand is False, Null
    // if the operand is Null, or False if the operand is True.

    public static DBBool operator !(DBBool x) {
        return new DBBool(-x.value);
    }

    // Logical AND operator. Returns False if either operand is False,
    // otherwise Null if either operand is Null, otherwise True.

    public static DBBool operator &(DBBool x, DBBool y) {
        return new DBBool(x.value < y.value? x.value: y.value);
    }

    // Logical OR operator. Returns True if either operand is True, otherwise
    // Null if either operand is Null, otherwise False.

    public static DBBool operator |(DBBool x, DBBool y) {
        return new DBBool(x.value > y.value? x.value: y.value);
    }

    // Definitely true operator. Returns true if the operand is True, false
    // otherwise.

    public static bool operator true(DBBool x) {
        return x.value > 0;
    }

    // Definitely false operator. Returns true if the operand is False, false
    // otherwise.

    public static bool operator false(DBBool x) {
        return x.value < 0;
    }

    public override bool Equals(object obj) {
        if (!(obj is DBBool)) return false;
        return value == ((DBBool)obj).value;
    }

    public override int GetHashCode() {
        return value;
    }

    public override string ToString() {
        if (value > 0) return "DBBool.True";
        if (value < 0) return "DBBool.False";
        return "DBBool.Null";
    }
}
```
