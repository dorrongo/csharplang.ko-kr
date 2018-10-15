# <a name="delegates"></a><span data-ttu-id="ddd73-101">대리자</span><span class="sxs-lookup"><span data-stu-id="ddd73-101">Delegates</span></span>

<span data-ttu-id="ddd73-102">대리자를 사용 하면 다른 언어-c + +, Pascal Modula-등 함수 포인터를 사용 하 여 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-102">Delegates enable scenarios that other languages—such as C++, Pascal, and Modula -- have addressed with function pointers.</span></span> <span data-ttu-id="ddd73-103">그러나 c + + 함수 포인터와 달리 대리자는 개체 지향적 이며, 완전히 및 c + + 멤버 함수 포인터와 달리 대리자 개체 인스턴스 및 메서드를 캡슐화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-103">Unlike C++ function pointers, however, delegates are fully object oriented, and unlike C++ pointers to member functions, delegates encapsulate both an object instance and a method.</span></span>

<span data-ttu-id="ddd73-104">클래스에서 파생 된 클래스를 정의 하는 대리자 선언을 `System.Delegate`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-104">A delegate declaration defines a class that is derived from the class `System.Delegate`.</span></span> <span data-ttu-id="ddd73-105">대리자 인스턴스 목록인 하나 이상의 메서드를 호출 가능 엔터티로 라고 하는 각 호출 목록을 캡슐화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-105">A delegate instance encapsulates an invocation list, which is a list of one or more methods, each of which is referred to as a callable entity.</span></span> <span data-ttu-id="ddd73-106">예를 들어 메서드를 호출할 수 엔터티 구성의 인스턴스와 해당 인스턴스에 메서드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-106">For instance methods, a callable entity consists of an instance and a method on that instance.</span></span> <span data-ttu-id="ddd73-107">정적 메서드를 호출 가능한 엔터티 메서드의 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-107">For static methods, a callable entity consists of just a method.</span></span> <span data-ttu-id="ddd73-108">지정된 된 인수 집합을 사용 하 여 호출할 대리자의 호출 가능한 엔터티의 각 하면 적절 한 인수 집합을 사용 하 여 대리자 인스턴스를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-108">Invoking a delegate instance with an appropriate set of arguments causes each of the delegate's callable entities to be invoked with the given set of arguments.</span></span>

<span data-ttu-id="ddd73-109">대리자 인스턴스는 흥미롭고 유용한 속성은 캡슐화; 메서드의 클래스에 대 한 처리 하거나 알고지 않습니다는 중요 한 정보는 해당 메서드에 호환 되도록 ([대리자 선언](delegates.md#delegate-declarations)) 대리자의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-109">An interesting and useful property of a delegate instance is that it does not know or care about the classes of the methods it encapsulates; all that matters is that those methods be compatible ([Delegate declarations](delegates.md#delegate-declarations)) with the delegate's type.</span></span> <span data-ttu-id="ddd73-110">따라서 대리자는 완벽 하 게 "익명" 호출에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-110">This makes delegates perfectly suited for "anonymous" invocation.</span></span>

## <a name="delegate-declarations"></a><span data-ttu-id="ddd73-111">대리자 선언</span><span class="sxs-lookup"><span data-stu-id="ddd73-111">Delegate declarations</span></span>

<span data-ttu-id="ddd73-112">A *delegate_declaration* 되는 *type_declaration* ([형식 선언을](namespaces.md#type-declarations)) 새 대리자 형식을 선언 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-112">A *delegate_declaration* is a *type_declaration* ([Type declarations](namespaces.md#type-declarations)) that declares a new delegate type.</span></span>

```antlr
delegate_declaration
    : attributes? delegate_modifier* 'delegate' return_type
      identifier variant_type_parameter_list?
      '(' formal_parameter_list? ')' type_parameter_constraints_clause* ';'
    ;

delegate_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | delegate_modifier_unsafe
    ;
```

<span data-ttu-id="ddd73-113">이를 여러 번 대리자 선언에서 동일한 한정자에 대 한 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-113">It is a compile-time error for the same modifier to appear multiple times in a delegate declaration.</span></span>

<span data-ttu-id="ddd73-114">합니다 `new` 한정자가 대리자만 허용 됩니다. 다른 형식 내에서 선언 된 경우이 이러한 대리자를 지정 숨깁니다 상속 된 멤버를 동일한 이름으로에 설명 된 대로 [new 한정자](classes.md#the-new-modifier)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-114">The `new` modifier is only permitted on delegates declared within another type, in which case it specifies that such a delegate hides an inherited member by the same name, as described in [The new modifier](classes.md#the-new-modifier).</span></span>

<span data-ttu-id="ddd73-115">합니다 `public`, `protected`를 `internal`, 및 `private` 한정자 대리자 형식의 접근성을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-115">The `public`, `protected`, `internal`, and `private` modifiers control the accessibility of the delegate type.</span></span> <span data-ttu-id="ddd73-116">대리자 선언 발생 하는 컨텍스트에 따라 이러한 한정자의 일부 없습니다 허용할 수도 있습니다 ([접근성을 선언](basic-concepts.md#declared-accessibility)).</span><span class="sxs-lookup"><span data-stu-id="ddd73-116">Depending on the context in which the delegate declaration occurs, some of these modifiers may not be permitted ([Declared accessibility](basic-concepts.md#declared-accessibility)).</span></span>

<span data-ttu-id="ddd73-117">대리자의 형식 이름은 *식별자*합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-117">The delegate's type name is *identifier*.</span></span>

<span data-ttu-id="ddd73-118">선택적 *formal_parameter_list* 대리자의 매개 변수를 지정 하 고 *return_type* 대리자의 반환 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-118">The optional *formal_parameter_list* specifies the parameters of the delegate, and *return_type* indicates the return type of the delegate.</span></span>

<span data-ttu-id="ddd73-119">선택적 *variant_type_parameter_list* ([Variant 형식 매개 변수 목록이](interfaces.md#variant-type-parameter-lists)) 자체 대리자 형식 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-119">The optional *variant_type_parameter_list* ([Variant type parameter lists](interfaces.md#variant-type-parameter-lists)) specifies the type parameters to the delegate itself.</span></span>

<span data-ttu-id="ddd73-120">대리자 형식의 반환 형식 중 하나 여야 합니다 `void`, 또는 출력 스레드로부터 안전한 ([분산 안전성](interfaces.md#variance-safety)).</span><span class="sxs-lookup"><span data-stu-id="ddd73-120">The return type of a delegate type must be either `void`, or output-safe ([Variance safety](interfaces.md#variance-safety)).</span></span>

<span data-ttu-id="ddd73-121">대리자 형식의 모든 형식 매개 변수 형식에는 입력 스레드로부터 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-121">All the formal parameter types of a delegate type must be input-safe.</span></span> <span data-ttu-id="ddd73-122">또한 `out` 또는 `ref` 매개 변수 형식 출력 스레드로부터 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-122">Additionally, any `out` or `ref` parameter types must also be output-safe.</span></span> <span data-ttu-id="ddd73-123">참고는도 `out` 매개 변수는 기본 실행 플랫폼의 제한으로 인해 입력 스레드로부터 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-123">Note that even `out` parameters are required to be input-safe, due to a limitation of the underlying execution platform.</span></span>

<span data-ttu-id="ddd73-124">C#의 대리자 형식과 해당 하는, 구조적으로 해당 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-124">Delegate types in C# are name equivalent, not structurally equivalent.</span></span> <span data-ttu-id="ddd73-125">특히, 동일한 매개 변수가 있는 두 개의 다른 대리자 형식을 나열 하 고 반환 형식에 다른 대리자 형식으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-125">Specifically, two different delegate types that have the same parameter lists and return type are considered different delegate types.</span></span> <span data-ttu-id="ddd73-126">두 개의 고유 하지만 구조적으로 동일한 대리자 형식의 인스턴스 동일한 것으로 비교할 수는 있지만 ([같음 연산자를 대리자](expressions.md#delegate-equality-operators)).</span><span class="sxs-lookup"><span data-stu-id="ddd73-126">However, instances of two distinct but structurally equivalent delegate types may compare as equal ([Delegate equality operators](expressions.md#delegate-equality-operators)).</span></span>

<span data-ttu-id="ddd73-127">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="ddd73-127">For example:</span></span>

```csharp
delegate int D1(int i, double d);

class A
{
    public static int M1(int a, double b) {...}
}

class B
{
    delegate int D2(int c, double d);
    public static int M1(int f, double g) {...}
    public static void M2(int k, double l) {...}
    public static int M3(int g) {...}
    public static void M4(int g) {...}
}
```

<span data-ttu-id="ddd73-128">그러나 메서드 `A.M1` 하 고 `B.M1 `대리자 형식과 호환 되 `D1` 및 `D2` 있기 때문에, 동일한 반환 형식과 매개 변수 목록, 이러한 대리자 형식이 되지 않으므로 두 가지는 사용이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-128">The methods `A.M1` and `B.M1 `are compatible with both the delegate types `D1` and `D2` , since they have the same return type and parameter list; however, these delegate types are two different types, so they are not interchangeable.</span></span> <span data-ttu-id="ddd73-129">메서드 `B.M2`, `B.M3`, 및 `B.M4` 대리자 형식과 호환 되지 `D1` 및 `D2`다른 반환 형식 또는 매개 변수 목록 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-129">The methods `B.M2`, `B.M3`, and `B.M4` are incompatible with the delegate types `D1` and `D2`, since they have different return types or parameter lists.</span></span>

<span data-ttu-id="ddd73-130">다른 제네릭 형식 선언에 같은 생성 된 대리자 형식을 만들려면 형식 인수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-130">Like other generic type declarations, type arguments must be given to create a constructed delegate type.</span></span> <span data-ttu-id="ddd73-131">매개 변수 형식 및 생성 된 대리자 형식의 반환 형식이 대리자 선언의 각 형식 매개 변수에 대해 생성 된 대리자 형식의 해당 형식 인수를 대체 하 여 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-131">The parameter types and return type of a constructed delegate type are created by substituting, for each type parameter in the delegate declaration, the corresponding type argument of the constructed delegate type.</span></span> <span data-ttu-id="ddd73-132">결과 반환 형식 및 매개 변수 형식은 어떤 메서드는 생성 된 대리자 형식과 호환 결정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-132">The resulting return type and parameter types are used in determining what methods are compatible with a constructed delegate type.</span></span> <span data-ttu-id="ddd73-133">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="ddd73-133">For example:</span></span>

```csharp
delegate bool Predicate<T>(T value);

class X
{
    static bool F(int i) {...}
    static bool G(string s) {...}
}
```

<span data-ttu-id="ddd73-134">메서드 `X.F` 대리자 형식과 호환 되는지 `Predicate<int>` 방법과 `X.G` 대리자 형식과 호환 되는 `Predicate<string>` 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-134">The method `X.F` is compatible with the delegate type `Predicate<int>` and the method `X.G` is compatible with the delegate type `Predicate<string>` .</span></span>

<span data-ttu-id="ddd73-135">통해 대리자 형식을 선언 하는 유일한 방법은는 *delegate_declaration*합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-135">The only way to declare a delegate type is via a *delegate_declaration*.</span></span> <span data-ttu-id="ddd73-136">대리자 형식에서 파생 된 클래스 형식은 `System.Delegate`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-136">A delegate type is a class type that is derived from `System.Delegate`.</span></span> <span data-ttu-id="ddd73-137">대리자 형식은 암시적으로 `sealed`이므로 대리자 형식에서 형식을 파생할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-137">Delegate types are implicitly `sealed`, so it is not permissible to derive any type from a delegate type.</span></span> <span data-ttu-id="ddd73-138">비 대리자 클래스 형식을 파생할 수 하지도 않습니다 `System.Delegate`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-138">It is also not permissible to derive a non-delegate class type from `System.Delegate`.</span></span> <span data-ttu-id="ddd73-139">`System.Delegate` 는 대리자 형식 자체는 모든 대리자 형식이 파생 되는 클래스 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-139">Note that `System.Delegate` is not itself a delegate type; it is a class type from which all delegate types are derived.</span></span>

<span data-ttu-id="ddd73-140">C# 특수 한 구문을 제공 대리자 인스턴스화 및 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-140">C# provides special syntax for delegate instantiation and invocation.</span></span> <span data-ttu-id="ddd73-141">인스턴스화를 제외 하 고 클래스 또는 클래스 인스턴스를 적용할 수 있는 모든 작업도 적용할 수 있습니다 대리자 클래스 또는 인스턴스를 각각.</span><span class="sxs-lookup"><span data-stu-id="ddd73-141">Except for instantiation, any operation that can be applied to a class or class instance can also be applied to a delegate class or instance, respectively.</span></span> <span data-ttu-id="ddd73-142">멤버에 액세스할 수 있기 특히는 `System.Delegate` 일반적인 멤버 액세스 구문을 통해 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-142">In particular, it is possible to access members of the `System.Delegate` type via the usual member access syntax.</span></span>

<span data-ttu-id="ddd73-143">대리자 인스턴스를 캡슐화 하는 메서드 집합에는 호출 목록을 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-143">The set of methods encapsulated by a delegate instance is called an invocation list.</span></span> <span data-ttu-id="ddd73-144">대리자 인스턴스를 만들면 ([대리자 호환성](delegates.md#delegate-compatibility)) 단일 메서드에서 해당 메서드를 캡슐화 하 고 해당 호출 목록에 항목이 하나만 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-144">When a delegate instance is created ([Delegate compatibility](delegates.md#delegate-compatibility)) from a single method, it encapsulates that method, and its invocation list contains only one entry.</span></span> <span data-ttu-id="ddd73-145">그러나 두 개의 null이 아닌 대리자 인스턴스를 결합 하면 해당 호출 목록은 연결 됩니다-순서로 왼쪽 피연산자 오른쪽 피연산자-두 개 이상의 항목을 포함 하는 새 호출 목록을 구성 하기 위해.</span><span class="sxs-lookup"><span data-stu-id="ddd73-145">However, when two non-null delegate instances are combined, their invocation lists are concatenated -- in the order left operand then right operand -- to form a new invocation list, which contains two or more entries.</span></span>

<span data-ttu-id="ddd73-146">이진 파일을 사용 하 여 대리자가 결합 `+` ([더하기 연산자](expressions.md#addition-operator)) 및 `+=` 연산자 ([복합 할당](expressions.md#compound-assignment)).</span><span class="sxs-lookup"><span data-stu-id="ddd73-146">Delegates are combined using the binary `+` ([Addition operator](expressions.md#addition-operator)) and `+=` operators ([Compound assignment](expressions.md#compound-assignment)).</span></span> <span data-ttu-id="ddd73-147">이진 파일을 사용 하 여 대리자를 조합에서 대리자를 제거할 수 있습니다 `-` ([빼기 연산자](expressions.md#subtraction-operator)) 및 `-=` 연산자 ([복합 할당](expressions.md#compound-assignment)).</span><span class="sxs-lookup"><span data-stu-id="ddd73-147">A delegate can be removed from a combination of delegates, using the binary `-` ([Subtraction operator](expressions.md#subtraction-operator)) and `-=` operators ([Compound assignment](expressions.md#compound-assignment)).</span></span> <span data-ttu-id="ddd73-148">대리자는 같은지 비교할 수 있습니다 ([같음 연산자를 대리자](expressions.md#delegate-equality-operators)).</span><span class="sxs-lookup"><span data-stu-id="ddd73-148">Delegates can be compared for equality ([Delegate equality operators](expressions.md#delegate-equality-operators)).</span></span>

<span data-ttu-id="ddd73-149">다음 예제에서는 다양 한 대리자를 인스턴스화 하 고 해당 호출과 해당 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-149">The following example shows the instantiation of a number of delegates, and their corresponding invocation lists:</span></span>

```csharp
delegate void D(int x);

class C
{
    public static void M1(int i) {...}
    public static void M2(int i) {...}

}

class Test
{
    static void Main() {
        D cd1 = new D(C.M1);      // M1
        D cd2 = new D(C.M2);      // M2
        D cd3 = cd1 + cd2;        // M1 + M2
        D cd4 = cd3 + cd1;        // M1 + M2 + M1
        D cd5 = cd4 + cd3;        // M1 + M2 + M1 + M1 + M2
    }

}
```

<span data-ttu-id="ddd73-150">때 `cd1` 고 `cd2` 는 인스턴스화된 각 메서드를 캡슐화 할 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-150">When `cd1` and `cd2` are instantiated, they each encapsulate one method.</span></span> <span data-ttu-id="ddd73-151">때 `cd3` 는 호출 목록을 두 가지 방법 중에 인스턴스화할 `M1` 및 `M2`를 주문 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-151">When `cd3` is instantiated, it has an invocation list of two methods, `M1` and `M2`, in that order.</span></span> <span data-ttu-id="ddd73-152">`cd4`호출 목록에 포함 `M1`, `M2`, 및 `M1`를 주문 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-152">`cd4`'s invocation list contains `M1`, `M2`, and `M1`, in that order.</span></span> <span data-ttu-id="ddd73-153">마지막으로, `cd5`의 호출 목록에 포함 `M1`, `M2`, `M1`를 `M1`, 및 `M2`를 주문 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-153">Finally, `cd5`'s invocation list contains `M1`, `M2`, `M1`, `M1`, and `M2`, in that order.</span></span> <span data-ttu-id="ddd73-154">(물론으로 제거) 대리자를 결합 한 더 많은 예제를 참조 하세요 [호출을 위임](delegates.md#delegate-invocation)합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-154">For more examples of combining (as well as removing) delegates, see [Delegate invocation](delegates.md#delegate-invocation).</span></span>

## <a name="delegate-compatibility"></a><span data-ttu-id="ddd73-155">대리자 호환성</span><span class="sxs-lookup"><span data-stu-id="ddd73-155">Delegate compatibility</span></span>

<span data-ttu-id="ddd73-156">메서드 또는 대리자 `M` 됩니다 ***호환*** 대리자 형식으로 `D` 다음 모두 만족 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="ddd73-156">A method or delegate `M` is ***compatible*** with a delegate type `D` if all of the following are true:</span></span>

*  <span data-ttu-id="ddd73-157">`D` 및 `M` 매개 변수 및 각 매개 변수 수가 같아야 `D` 동일 `ref` 하거나 `out` 한정자에서 해당 매개 변수로 `M`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-157">`D` and `M` have the same number of parameters, and each parameter in `D` has the same `ref` or `out` modifiers as the corresponding parameter in `M`.</span></span>
*  <span data-ttu-id="ddd73-158">각 값 매개 변수에 대해 (매개 변수 없이 `ref` 또는 `out` 한정자), id 변환이 ([Id 변환을](conversions.md#identity-conversion)) 또는 암시적 참조 변환을 ([암시적 참조 변환을](conversions.md#implicit-reference-conversions)) 매개 변수 형식에서 존재 `D` 에서 해당 매개 변수 형식에 `M`입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-158">For each value parameter (a parameter with no `ref` or `out` modifier), an identity conversion ([Identity conversion](conversions.md#identity-conversion)) or implicit reference conversion ([Implicit reference conversions](conversions.md#implicit-reference-conversions)) exists from the parameter type in `D` to the corresponding parameter type in `M`.</span></span>
*  <span data-ttu-id="ddd73-159">각 `ref` 또는 `out` 매개 변수, 매개 변수 입력 `D` 매개 변수 형식이 동일 `M`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-159">For each `ref` or `out` parameter, the parameter type in `D` is the same as the parameter type in `M`.</span></span>
*  <span data-ttu-id="ddd73-160">반환 형식에서 id 또는 암시적 참조 변환이 존재 `M` 의 반환 형식으로 `D`입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-160">An identity or implicit reference conversion exists from the return type of `M` to the return type of `D`.</span></span>

## <a name="delegate-instantiation"></a><span data-ttu-id="ddd73-161">대리자 인스턴스화</span><span class="sxs-lookup"><span data-stu-id="ddd73-161">Delegate instantiation</span></span>

<span data-ttu-id="ddd73-162">대리자 인스턴스에 만들어집니다를 *delegate_creation_expression* ([대리자 생성 식](expressions.md#delegate-creation-expressions)) 또는 대리자 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-162">An instance of a delegate is created by a *delegate_creation_expression* ([Delegate creation expressions](expressions.md#delegate-creation-expressions)) or a conversion to a delegate type.</span></span> <span data-ttu-id="ddd73-163">새로 만든된 대리자 인스턴스는 다음 중 하나를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-163">The newly created delegate instance then refers to either:</span></span>

*  <span data-ttu-id="ddd73-164">참조 하는 정적 메서드를 *delegate_creation_expression*, 또는</span><span class="sxs-lookup"><span data-stu-id="ddd73-164">The static method referenced in the *delegate_creation_expression*, or</span></span>
*  <span data-ttu-id="ddd73-165">대상 개체 (될 수 없습니다 `null`)에서 참조 하는 메서드 인스턴스를 *delegate_creation_expression*, 또는</span><span class="sxs-lookup"><span data-stu-id="ddd73-165">The target object (which cannot be `null`) and instance method referenced in the *delegate_creation_expression*, or</span></span>
*  <span data-ttu-id="ddd73-166">다른 대리자입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-166">Another delegate.</span></span>

<span data-ttu-id="ddd73-167">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="ddd73-167">For example:</span></span>

```csharp
delegate void D(int x);

class C
{
    public static void M1(int i) {...}
    public void M2(int i) {...}
}

class Test
{
    static void Main() { 
        D cd1 = new D(C.M1);        // static method
        C t = new C();
        D cd2 = new D(t.M2);        // instance method
        D cd3 = new D(cd2);        // another delegate
    }
}
```

<span data-ttu-id="ddd73-168">인스턴스화된 대리자 인스턴스는 항상 동일한 대상 개체 및 메서드를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-168">Once instantiated, delegate instances always refer to the same target object and method.</span></span> <span data-ttu-id="ddd73-169">경우 두 명의 대리자를 결합 하거나 다른 고유한 호출 목록;를 사용 하 여 새 대리자 결과에서 하나를 제거 해야 조합 하거나 제거 하는 대리자의 호출 목록을 그대로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-169">Remember, when two delegates are combined, or one is removed from another, a new delegate results with its own invocation list; the invocation lists of the delegates combined or removed remain unchanged.</span></span>

## <a name="delegate-invocation"></a><span data-ttu-id="ddd73-170">대리자 호출</span><span class="sxs-lookup"><span data-stu-id="ddd73-170">Delegate invocation</span></span>

<span data-ttu-id="ddd73-171">C# 대리자를 호출 하는 것에 대 한 특별 한 구문을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-171">C# provides special syntax for invoking a delegate.</span></span> <span data-ttu-id="ddd73-172">지정 하 고 참조와 동일한 값을 반환 하는 동일한 인수를 사용 하 여 하나의 메서드 호출 목록을 가진 하나의 항목이 포함 된 null이 아닌 대리자 인스턴스를 호출 하면 호출 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-172">When a non-null delegate instance whose invocation list contains one entry is invoked, it invokes the one method with the same arguments it was given, and returns the same value as the referred to method.</span></span> <span data-ttu-id="ddd73-173">(참조 [대리자 호출](expressions.md#delegate-invocations) 대리자 호출에 대 한 자세한 내용은 합니다.) 이러한 대리자를 호출 하는 동안 예외가 발생 하는 경우 호출 된 메서드 내에서 해당 예외 잡히지 않는 예외 catch 절을 계속 검색 대리자를 호출 하는 방법에는 직접 호출한 경우는 메서드는 대리자 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-173">(See [Delegate invocations](expressions.md#delegate-invocations) for detailed information on delegate invocation.) If an exception occurs during the invocation of such a delegate, and that exception is not caught within the method that was invoked, the search for an exception catch clause continues in the method that called the delegate, as if that method had directly called the method to which that delegate referred.</span></span>

<span data-ttu-id="ddd73-174">순서로 각 항목은 각 메서드의 호출 목록에서 동기적으로 호출 하 여 여러 항목을 포함 하는 호출 목록을 가진 대리자 인스턴스 호출 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-174">Invocation of a delegate instance whose invocation list contains multiple entries proceeds by invoking each of the methods in the invocation list, synchronously, in order.</span></span> <span data-ttu-id="ddd73-175">호출 된 각 메서드에 대리자 인스턴스를 지정 된 대로 인수 집합이 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-175">Each method so called is passed the same set of arguments as was given to the delegate instance.</span></span> <span data-ttu-id="ddd73-176">이러한 대리자 호출 참조 매개 변수를 포함 하는 경우 ([매개 변수를 참조할](classes.md#reference-parameters)), 호출 목록에서 한 메서드에서 해당 변수에 대 한 변경 내용이 됩니다; 메서드를 호출할 때마다 동일한 변수에 대 한 참조를 사용 하 여 발생 합니다. 호출 목록 아래로 추가 메서드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-176">If such a delegate invocation includes reference parameters ([Reference parameters](classes.md#reference-parameters)), each method invocation will occur with a reference to the same variable; changes to that variable by one method in the invocation list will be visible to methods further down the invocation list.</span></span> <span data-ttu-id="ddd73-177">대리자 호출 출력 매개 변수 또는 반환 값에 포함 된 경우 최종 값 목록에 있는 마지막 대리자의 호출에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-177">If the delegate invocation includes output parameters or a return value, their final value will come from the invocation of the last delegate in the list.</span></span>

<span data-ttu-id="ddd73-178">이러한 대리자의 호출을 처리 하는 동안 예외가 발생 하는 경우 호출 된 메서드 내에서 해당 예외 잡히지 않는 대리자를 호출 하는 방법에 계속 예외 catch 절을 검색 하 고 메서드 아래쪽 호출 목록이 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-178">If an exception occurs during processing of the invocation of such a delegate, and that exception is not caught within the method that was invoked, the search for an exception catch clause continues in the method that called the delegate, and any methods further down the invocation list are not invoked.</span></span>

<span data-ttu-id="ddd73-179">값이 null 결과 형식의 예외가 대리자 인스턴스를 호출 하는 동안 `System.NullReferenceException`합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-179">Attempting to invoke a delegate instance whose value is null results in an exception of type `System.NullReferenceException`.</span></span>

<span data-ttu-id="ddd73-180">다음 예제에서는 인스턴스화할 결합, 제거 및 대리자를 호출 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-180">The following example shows how to instantiate, combine, remove, and invoke delegates:</span></span>

```csharp
using System;

delegate void D(int x);

class C
{
    public static void M1(int i) {
        Console.WriteLine("C.M1: " + i);
    }

    public static void M2(int i) {
        Console.WriteLine("C.M2: " + i);
    }

    public void M3(int i) {
        Console.WriteLine("C.M3: " + i);
    }
}

class Test
{
    static void Main() { 
        D cd1 = new D(C.M1);
        cd1(-1);                // call M1

        D cd2 = new D(C.M2);
        cd2(-2);                // call M2

        D cd3 = cd1 + cd2;
        cd3(10);                // call M1 then M2

        cd3 += cd1;
        cd3(20);                // call M1, M2, then M1

        C c = new C();
        D cd4 = new D(c.M3);
        cd3 += cd4;
        cd3(30);                // call M1, M2, M1, then M3

        cd3 -= cd1;             // remove last M1
        cd3(40);                // call M1, M2, then M3

        cd3 -= cd4;
        cd3(50);                // call M1 then M2

        cd3 -= cd2;
        cd3(60);                // call M1

        cd3 -= cd2;             // impossible removal is benign
        cd3(60);                // call M1

        cd3 -= cd1;             // invocation list is empty so cd3 is null

        cd3(70);                // System.NullReferenceException thrown

        cd3 -= cd1;             // impossible removal is benign
    }
}
```

<span data-ttu-id="ddd73-181">문에서 같이 `cd3 += cd1;`를 여러 번 이러한 대리자를 호출 목록에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-181">As shown in the statement `cd3 += cd1;`, a delegate can be present in an invocation list multiple times.</span></span> <span data-ttu-id="ddd73-182">이 경우이 단순히 당 한 번씩 호출 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-182">In this case, it is simply invoked once per occurrence.</span></span> <span data-ttu-id="ddd73-183">이와 같은 호출 목록을, 대리자 제거 되 면 호출 목록에서 마지막은 실제로 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-183">In an invocation list such as this, when that delegate is removed, the last occurrence in the invocation list is the one actually removed.</span></span>

<span data-ttu-id="ddd73-184">마지막 문 실행 하기 전에 즉시 `cd3 -= cd1;`, 대리자 `cd3` 빈 호출 목록을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-184">Immediately prior to the execution of the final statement, `cd3 -= cd1;`, the delegate `cd3` refers to an empty invocation list.</span></span> <span data-ttu-id="ddd73-185">빈 목록에서 대리자를 제거 하려면 (또는 비어 있지 않은 목록에서 존재 하지 않는 대리자를 제거 하려면) 동안은 오류가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-185">Attempting to remove a delegate from an empty list (or to remove a non-existent delegate from a non-empty list) is not an error.</span></span>

<span data-ttu-id="ddd73-186">생성 된 출력이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ddd73-186">The output produced is:</span></span>

```
C.M1: -1
C.M2: -2
C.M1: 10
C.M2: 10
C.M1: 20
C.M2: 20
C.M1: 20
C.M1: 30
C.M2: 30
C.M1: 30
C.M3: 30
C.M1: 40
C.M2: 40
C.M3: 40
C.M1: 50
C.M2: 50
C.M1: 60
C.M1: 60
```
