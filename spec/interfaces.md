# <a name="interfaces"></a><span data-ttu-id="902c2-101">인터페이스</span><span class="sxs-lookup"><span data-stu-id="902c2-101">Interfaces</span></span>

<span data-ttu-id="902c2-102">인터페이스는 계약을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-102">An interface defines a contract.</span></span> <span data-ttu-id="902c2-103">클래스 또는 구조체는 인터페이스를 구현 하는 계약을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-103">A class or struct that implements an interface must adhere to its contract.</span></span> <span data-ttu-id="902c2-104">여러 기본 인터페이스에서 상속할 수 및 클래스 또는 구조체는 여러 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-104">An interface may inherit from multiple base interfaces, and a class or struct may implement multiple interfaces.</span></span>

<span data-ttu-id="902c2-105">인터페이스는 메서드, 속성, 이벤트 및 인덱서를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-105">Interfaces can contain methods, properties, events, and indexers.</span></span> <span data-ttu-id="902c2-106">자체 인터페이스를 정의 하는 멤버에 대 한 구현을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-106">The interface itself does not provide implementations for the members that it defines.</span></span> <span data-ttu-id="902c2-107">인터페이스는 단순히 인터페이스를 구현 하는 클래스 또는 구조체에서 제공 해야 하는 멤버를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-107">The interface merely specifies the members that must be supplied by classes or structs that implement the interface.</span></span>

## <a name="interface-declarations"></a><span data-ttu-id="902c2-108">인터페이스 선언</span><span class="sxs-lookup"><span data-stu-id="902c2-108">Interface declarations</span></span>

<span data-ttu-id="902c2-109">*interface_declaration* 되는 *type_declaration* ([형식 선언을](namespaces.md#type-declarations)) 새 인터페이스 형식을 선언 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-109">An *interface_declaration* is a *type_declaration* ([Type declarations](namespaces.md#type-declarations)) that declares a new interface type.</span></span>

```antlr
interface_declaration
    : attributes? interface_modifier* 'partial'? 'interface'
      identifier variant_type_parameter_list? interface_base?
      type_parameter_constraints_clause* interface_body ';'?
    ;
```

<span data-ttu-id="902c2-110">*interface_declaration* 선택적 집합으로 이루어져 *특성* ([특성](attributes.md))의 선택적 집합 뒤에, *interface_modifier*s ([한정자를 인터페이스](interfaces.md#interface-modifiers)), 선택적 `partial` 키워드 뒤에 한정자 `interface` 과 *식별자* 인터페이스 이름을 지정 하는 뒤에 선택적인 *variant_type_parameter_list* 사양 ([Variant 형식 매개 변수 목록](interfaces.md#variant-type-parameter-lists)), 선택적 *interface_base* 사양 ([기본 인터페이스](interfaces.md#base-interfaces)), 선택적 *type_parameter_constraints_clause*s 사양 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)) 를 뒤에 *interface_body* ([본문 인터페이스](interfaces.md#interface-body)), 세미콜론 뒤에 선택적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-110">An *interface_declaration* consists of an optional set of *attributes* ([Attributes](attributes.md)), followed by an optional set of *interface_modifier*s ([Interface modifiers](interfaces.md#interface-modifiers)), followed by an optional `partial` modifier, followed by the keyword `interface` and an *identifier* that names the interface, followed by an optional *variant_type_parameter_list* specification ([Variant type parameter lists](interfaces.md#variant-type-parameter-lists)), followed by an optional *interface_base* specification ([Base interfaces](interfaces.md#base-interfaces)), followed by an optional *type_parameter_constraints_clause*s specification ([Type parameter constraints](classes.md#type-parameter-constraints)), followed by an *interface_body* ([Interface body](interfaces.md#interface-body)), optionally followed by a semicolon.</span></span>

### <a name="interface-modifiers"></a><span data-ttu-id="902c2-111">한정자를 인터페이스</span><span class="sxs-lookup"><span data-stu-id="902c2-111">Interface modifiers</span></span>

<span data-ttu-id="902c2-112">*interface_declaration* 인터페이스 한정자 시퀀스를 선택적으로 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-112">An *interface_declaration* may optionally include a sequence of interface modifiers:</span></span>

```antlr
interface_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | interface_modifier_unsafe
    ;
```

<span data-ttu-id="902c2-113">이 인터페이스 선언에 여러 번 표시 하는 동일한 한정자에 대 한 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-113">It is a compile-time error for the same modifier to appear multiple times in an interface declaration.</span></span>

<span data-ttu-id="902c2-114">`new` 한정자는 클래스 내에 정의 된 인터페이스에만 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-114">The `new` modifier is only permitted on interfaces defined within a class.</span></span> <span data-ttu-id="902c2-115">지정 인터페이스는 동일한 이름으로 상속된 된 멤버를 숨깁니다에 설명 된 대로 [새 한정자](classes.md#the-new-modifier)합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-115">It specifies that the interface hides an inherited member by the same name, as described in [The new modifier](classes.md#the-new-modifier).</span></span>

<span data-ttu-id="902c2-116">합니다 `public`, `protected`를 `internal`, 및 `private` 한정자는 인터페이스의 접근성을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-116">The `public`, `protected`, `internal`, and `private` modifiers control the accessibility of the interface.</span></span> <span data-ttu-id="902c2-117">인터페이스 선언 발생 하는 컨텍스트에 따라 이러한 한정자의 일부만 허용 될 수 있습니다 ([접근성을 선언](basic-concepts.md#declared-accessibility)).</span><span class="sxs-lookup"><span data-stu-id="902c2-117">Depending on the context in which the interface declaration occurs, only some of these modifiers may be permitted ([Declared accessibility](basic-concepts.md#declared-accessibility)).</span></span>

### <a name="partial-modifier"></a><span data-ttu-id="902c2-118">Partial 한정자</span><span class="sxs-lookup"><span data-stu-id="902c2-118">Partial modifier</span></span>

<span data-ttu-id="902c2-119">합니다 `partial` 한정자가 나타내는이 *interface_declaration* 부분 형식 선언입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-119">The `partial` modifier indicates that this *interface_declaration* is a partial type declaration.</span></span> <span data-ttu-id="902c2-120">에 지정 된 규칙에 따라 바깥쪽 형식 또는 네임 스페이스 선언 내에서 동일한 이름 가진 여러 partial 인터페이스 선언을 폼 하나의 인터페이스 선언에 결합 [부분 형식](classes.md#partial-types)합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-120">Multiple partial interface declarations with the same name within an enclosing namespace or type declaration combine to form one interface declaration, following the rules specified in [Partial types](classes.md#partial-types).</span></span>

### <a name="variant-type-parameter-lists"></a><span data-ttu-id="902c2-121">Variant 형식 매개 변수 목록</span><span class="sxs-lookup"><span data-stu-id="902c2-121">Variant type parameter lists</span></span>

<span data-ttu-id="902c2-122">Variant 형식 매개 변수 목록 인터페이스 및 대리자 형식에만 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-122">Variant type parameter lists can only occur on interface and delegate types.</span></span> <span data-ttu-id="902c2-123">일반적인의 차이 *type_parameter_list*가 선택적 *variance_annotation* 각 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-123">The difference from ordinary *type_parameter_list*s is the optional *variance_annotation* on each type parameter.</span></span>

```antlr
variant_type_parameter_list
    : '<' variant_type_parameters '>'
    ;

variant_type_parameters
    : attributes? variance_annotation? type_parameter
    | variant_type_parameters ',' attributes? variance_annotation? type_parameter
    ;

variance_annotation
    : 'in'
    | 'out'
    ;
```

<span data-ttu-id="902c2-124">분산 주석이 되 면 `out`, 형식 매개 변수 라고 ***공변 (covariant)*** 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-124">If the variance annotation is `out`, the type parameter is said to be ***covariant***.</span></span> <span data-ttu-id="902c2-125">분산 주석이 되 면 `in`, 형식 매개 변수 라고 ***반공 변***합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-125">If the variance annotation is `in`, the type parameter is said to be ***contravariant***.</span></span> <span data-ttu-id="902c2-126">분산 주석이 없는 경우 형식 매개 변수 라고 ***고정***합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-126">If there is no variance annotation, the type parameter is said to be ***invariant***.</span></span>

<span data-ttu-id="902c2-127">예제</span><span class="sxs-lookup"><span data-stu-id="902c2-127">In the example</span></span>
```csharp
interface C<out X, in Y, Z> 
{
  X M(Y y);
  Z P { get; set; }
}
```
<span data-ttu-id="902c2-128">`X` 공변 `Y` 는 반공 변 및 `Z` 변하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-128">`X` is covariant, `Y` is contravariant and `Z` is invariant.</span></span>

#### <a name="variance-safety"></a><span data-ttu-id="902c2-129">분산 보안</span><span class="sxs-lookup"><span data-stu-id="902c2-129">Variance safety</span></span>

<span data-ttu-id="902c2-130">형식 선언에 형식 오류가 발생할 수 있는 위치를 제한 하는 형식의 형식 매개 변수 목록의 가변성 주석 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-130">The occurrence of variance annotations in the type parameter list of a type restricts the places where types can occur within the type declaration.</span></span>

<span data-ttu-id="902c2-131">형식 `T` 됩니다 ***안전 하지 않은 출력*** 다음 중 하나를 보유 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="902c2-131">A type `T` is ***output-unsafe*** if one of the following holds:</span></span>

*  <span data-ttu-id="902c2-132">`T` 반공 변 형식 매개 변수인</span><span class="sxs-lookup"><span data-stu-id="902c2-132">`T` is a contravariant type parameter</span></span>
*  <span data-ttu-id="902c2-133">`T` 출력 안전 하지 않은 요소 형식 가진 배열 형식인</span><span class="sxs-lookup"><span data-stu-id="902c2-133">`T` is an array type with an output-unsafe element type</span></span>
*  <span data-ttu-id="902c2-134">`T` 인터페이스 또는 대리자 형식인 `S<A1,...,Ak>` 제네릭 형식에서 생성 `S<X1,...,Xk>` 하나 이상에 대 한 where `Ai` 다음 중 하나를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-134">`T` is an interface or delegate type `S<A1,...,Ak>` constructed from a generic type `S<X1,...,Xk>` where for at least one `Ai` one of the following holds:</span></span>
   * <span data-ttu-id="902c2-135">`Xi` 공변 (covariant) 또는 고정 및 `Ai` 안전 하지 않은 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-135">`Xi` is covariant or invariant and `Ai` is output-unsafe.</span></span>
   * <span data-ttu-id="902c2-136">`Xi` 반공 변 또는 고정 및 `Ai` 는 입력 스레드로부터 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-136">`Xi` is contravariant or invariant and `Ai` is input-safe.</span></span>
   
<span data-ttu-id="902c2-137">형식 `T` 됩니다 ***안전 하지 않은 입력*** 다음 중 하나를 보유 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="902c2-137">A type `T` is ***input-unsafe*** if one of the following holds:</span></span>

*  <span data-ttu-id="902c2-138">`T` 공변 (covariant) 형식 매개 변수인</span><span class="sxs-lookup"><span data-stu-id="902c2-138">`T` is a covariant type parameter</span></span>
*  <span data-ttu-id="902c2-139">`T` 입력이 안전 하지 않은 요소 형식 가진 배열 형식인</span><span class="sxs-lookup"><span data-stu-id="902c2-139">`T` is an array type with an input-unsafe element type</span></span>
*  <span data-ttu-id="902c2-140">`T` 인터페이스 또는 대리자 형식인 `S<A1,...,Ak>` 제네릭 형식에서 생성 `S<X1,...,Xk>` 하나 이상에 대 한 where `Ai` 다음 중 하나를 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-140">`T` is an interface or delegate type `S<A1,...,Ak>` constructed from a generic type `S<X1,...,Xk>` where for at least one `Ai` one of the following holds:</span></span>
   * <span data-ttu-id="902c2-141">`Xi` 공변 (covariant) 또는 고정 및 `Ai` 안전 하지 않은 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-141">`Xi` is covariant or invariant and `Ai` is input-unsafe.</span></span>
   * <span data-ttu-id="902c2-142">`Xi` 반공 변 또는 고정 및 `Ai` 안전 하지 않은 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-142">`Xi` is contravariant or invariant and `Ai` is output-unsafe.</span></span>

<span data-ttu-id="902c2-143">직관적으로 안전 하지 않은 출력 형식의 출력 위치를 서 금지 된 및 입력된 위치에는 입력이 안전 하지 않은 형식을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-143">Intuitively, an output-unsafe type is prohibited in an output position, and an input-unsafe type is prohibited in an input position.</span></span>

<span data-ttu-id="902c2-144">형식이 ***출력 스레드로부터 안전한*** 출력 unsafe 없으면 및 ***입력 스레드로부터 안전한*** 입력 안전 하지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="902c2-144">A type is ***output-safe*** if it is not output-unsafe, and ***input-safe*** if it is not input-unsafe.</span></span>

#### <a name="variance-conversion"></a><span data-ttu-id="902c2-145">변형 변환이</span><span class="sxs-lookup"><span data-stu-id="902c2-145">Variance conversion</span></span>

<span data-ttu-id="902c2-146">가변성 주석의 목적은 (그러나 여전히 형식 안전 하 게) 더 관대 인터페이스 및 대리자 형식 변환을 제공 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-146">The purpose of variance annotations is to provide for more lenient (but still type safe) conversions to interface and delegate types.</span></span> <span data-ttu-id="902c2-147">이 암시적의 정의 종료 합니다 ([암시적 변환을](conversions.md#implicit-conversions)) 및 명시적 변환 ([명시적 변환](conversions.md#explicit-conversions)) 확인 변형 다음과 같이 정의 되어 있는 개념이 사용:</span><span class="sxs-lookup"><span data-stu-id="902c2-147">To this end the definitions of implicit ([Implicit conversions](conversions.md#implicit-conversions)) and explicit conversions ([Explicit conversions](conversions.md#explicit-conversions)) make use of the notion of variance-convertibility, which is defined as follows:</span></span>

<span data-ttu-id="902c2-148">형식 `T<A1,...,An>` 변형 가능은 형식 `T<B1,...,Bn>` 경우 `T` variant 형식 매개 변수를 사용 하 여 인터페이스 또는 대리자 형식을 선언 `T<X1,...,Xn>`, 및 각 variant 형식 매개 변수에 대해 `Xi` 다음 중 하나 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-148">A type `T<A1,...,An>` is variance-convertible to a type `T<B1,...,Bn>` if `T` is either an interface or a delegate type declared with the variant type parameters `T<X1,...,Xn>`, and for each variant type parameter `Xi` one of the following holds:</span></span>

*  <span data-ttu-id="902c2-149">`Xi` 공변 (covariant)에서 암시적 참조 또는 id 변환을 존재 `Ai` 를 `Bi`</span><span class="sxs-lookup"><span data-stu-id="902c2-149">`Xi` is covariant and an implicit reference or identity conversion exists from `Ai` to `Bi`</span></span>
*  <span data-ttu-id="902c2-150">`Xi` 반공 변 이며 암시적 참조 또는에서 identity 변환이 존재 `Bi` 를 `Ai`</span><span class="sxs-lookup"><span data-stu-id="902c2-150">`Xi` is contravariant and an implicit reference or identity conversion exists from `Bi` to `Ai`</span></span>
*  <span data-ttu-id="902c2-151">`Xi` 고정 되어 id에서 변환이 존재 `Ai` 를 `Bi`</span><span class="sxs-lookup"><span data-stu-id="902c2-151">`Xi` is invariant and an identity conversion exists from `Ai` to `Bi`</span></span>

### <a name="base-interfaces"></a><span data-ttu-id="902c2-152">기본 인터페이스</span><span class="sxs-lookup"><span data-stu-id="902c2-152">Base interfaces</span></span>

<span data-ttu-id="902c2-153">인터페이스 라고 하는 0 개 이상의 인터페이스 형식에서 상속할 수는 ***명시적 기본 인터페이스*** 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-153">An interface can inherit from zero or more interface types, which are called the ***explicit base interfaces*** of the interface.</span></span> <span data-ttu-id="902c2-154">인터페이스 하나 이상의 명시적 기본 인터페이스에 있는 경우 다음에서 해당 인터페이스를 선언 인터페이스 식별자 뒤에는 콜론과 쉼표로 구분 된 목록 기본 인터페이스 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-154">When an interface has one or more explicit base interfaces, then in the declaration of that interface, the interface identifier is followed by a colon and a comma separated list of base interface types.</span></span>

```antlr
interface_base
    : ':' interface_type_list
    ;
```

<span data-ttu-id="902c2-155">생성 된 인터페이스 형식에 대 한 명시적 기본 인터페이스는 제네릭 형식 선언에서 명시적 기본 인터페이스 선언을 가져오고 각각에 대 한 대체으로 형성 *type_parameter* 기본 인터페이스에서 해당 선언인 *type_argument* 생성 된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-155">For a constructed interface type, the explicit base interfaces are formed by taking the explicit base interface declarations on the generic type declaration, and substituting, for each *type_parameter* in the base interface declaration, the corresponding *type_argument* of the constructed type.</span></span>

<span data-ttu-id="902c2-156">인터페이스의 명시적 기본 인터페이스는 적어도 인터페이스 자체 만큼 액세스 가능 해야 합니다. ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="902c2-156">The explicit base interfaces of an interface must be at least as accessible as the interface itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span> <span data-ttu-id="902c2-157">컴파일 타임 오류를 지정 하는 것이 예는 `private` 또는 `internal` 인터페이스는 *interface_base* 의 `public` 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="902c2-157">For example, it is a compile-time error to specify a `private` or `internal` interface in the *interface_base* of a `public` interface.</span></span>

<span data-ttu-id="902c2-158">이 직접 또는 간접적으로 자신 으로부터 상속에 대 한 인터페이스에 대 한 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-158">It is a compile-time error for an interface to directly or indirectly inherit from itself.</span></span>

<span data-ttu-id="902c2-159">합니다 ***기본 인터페이스*** 명시적 기본 인터페이스 및 해당 기본 인터페이스는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-159">The ***base interfaces*** of an interface are the explicit base interfaces and their base interfaces.</span></span> <span data-ttu-id="902c2-160">즉, 기본 인터페이스 집합이 명시적 기본 인터페이스는, 명시적 기본 인터페이스 및 등의 전이적 closure 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-160">In other words, the set of base interfaces is the complete transitive closure of the explicit base interfaces, their explicit base interfaces, and so on.</span></span> <span data-ttu-id="902c2-161">인터페이스의 기본 인터페이스의 모든 멤버를 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-161">An interface inherits all members of its base interfaces.</span></span> <span data-ttu-id="902c2-162">예제</span><span class="sxs-lookup"><span data-stu-id="902c2-162">In the example</span></span>
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}

interface IListBox: IControl
{
    void SetItems(string[] items);
}

interface IComboBox: ITextBox, IListBox {}
```
<span data-ttu-id="902c2-163">기본 인터페이스 `IComboBox` 됩니다 `IControl`를 `ITextBox`, 및 `IListBox`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-163">the base interfaces of `IComboBox` are `IControl`, `ITextBox`, and `IListBox`.</span></span>

<span data-ttu-id="902c2-164">즉, 합니다 `IComboBox` 위의 인터페이스 멤버를 상속 `SetText` 하 고 `SetItems` 뿐만 `Paint`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-164">In other words, the `IComboBox` interface above inherits members `SetText` and `SetItems` as well as `Paint`.</span></span>

<span data-ttu-id="902c2-165">모든 기본 인터페이스는 인터페이스의 출력 안전 해야 합니다. ([분산 안전성](interfaces.md#variance-safety)).</span><span class="sxs-lookup"><span data-stu-id="902c2-165">Every base interface of an interface must be output-safe ([Variance safety](interfaces.md#variance-safety)).</span></span> <span data-ttu-id="902c2-166">클래스 또는 구조체는 인터페이스를 암시적으로 구현 하는 모든 인터페이스의 기본 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-166">A class or struct that implements an interface also implicitly implements all of the interface's base interfaces.</span></span>

### <a name="interface-body"></a><span data-ttu-id="902c2-167">인터페이스 본문</span><span class="sxs-lookup"><span data-stu-id="902c2-167">Interface body</span></span>

<span data-ttu-id="902c2-168">합니다 *interface_body* 인터페이스의 인터페이스 멤버를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-168">The *interface_body* of an interface defines the members of the interface.</span></span>

```antlr
interface_body
    : '{' interface_member_declaration* '}'
    ;
```

## <a name="interface-members"></a><span data-ttu-id="902c2-169">인터페이스 멤버</span><span class="sxs-lookup"><span data-stu-id="902c2-169">Interface members</span></span>

<span data-ttu-id="902c2-170">인터페이스의 멤버는 기본 인터페이스에서 상속 된 멤버 및 멤버 자체 인터페이스에서 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-170">The members of an interface are the members inherited from the base interfaces and the members declared by the interface itself.</span></span>

```antlr
interface_member_declaration
    : interface_method_declaration
    | interface_property_declaration
    | interface_event_declaration
    | interface_indexer_declaration
    ;
```

<span data-ttu-id="902c2-171">인터페이스 선언 0 개 이상의 멤버를 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-171">An interface declaration may declare zero or more members.</span></span> <span data-ttu-id="902c2-172">메서드, 속성, 이벤트 또는 인덱서는 인터페이스의 멤버 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-172">The members of an interface must be methods, properties, events, or indexers.</span></span> <span data-ttu-id="902c2-173">인터페이스는 상수, 필드, 연산자, 인스턴스 생성자, 소멸자 또는 형식을 포함할 수 없습니다 또는 인터페이스로 모든 종류의 정적 멤버를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-173">An interface cannot contain constants, fields, operators, instance constructors, destructors, or types, nor can an interface contain static members of any kind.</span></span>

<span data-ttu-id="902c2-174">모든 인터페이스 멤버는 암시적으로 공용 액세스를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-174">All interface members implicitly have public access.</span></span> <span data-ttu-id="902c2-175">이 한정자를 포함할에 인터페이스 멤버 선언에 대 한 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-175">It is a compile-time error for interface member declarations to include any modifiers.</span></span> <span data-ttu-id="902c2-176">특히 한정자를 사용 하 여 인터페이스 멤버를 선언할 수 없습니다 `abstract`, `public`, `protected`, `internal`를 `private`를 `virtual`를 `override`, 또는 `static`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-176">In particular, interfaces members cannot be declared with the modifiers `abstract`, `public`, `protected`, `internal`, `private`, `virtual`, `override`, or `static`.</span></span>

<span data-ttu-id="902c2-177">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="902c2-177">The example</span></span>
```csharp
public delegate void StringListEvent(IStringList sender);

public interface IStringList
{
    void Add(string s);
    int Count { get; }
    event StringListEvent Changed;
    string this[int index] { get; set; }
}
```
<span data-ttu-id="902c2-178">멤버의 가능한 종류 각각 하나씩 포함 하는 인터페이스를 선언 합니다: 메서드, 속성, 이벤트 및 인덱서 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-178">declares an interface that contains one each of the possible kinds of members: A method, a property, an event, and an indexer.</span></span>

<span data-ttu-id="902c2-179">*interface_declaration* 새 선언 공간을 만듭니다 ([선언](basic-concepts.md#declarations)), 및 *interface_member_declaration*합니다 하여포함된즉시*interface_declaration* 이 선언 공간에 새 멤버를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-179">An *interface_declaration* creates a new declaration space ([Declarations](basic-concepts.md#declarations)), and the *interface_member_declaration*s immediately contained by the *interface_declaration* introduce new members into this declaration space.</span></span> <span data-ttu-id="902c2-180">다음 규칙이 적용 됩니다 *interface_member_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="902c2-180">The following rules apply to *interface_member_declaration*s:</span></span>

*  <span data-ttu-id="902c2-181">메서드의 이름을 모든 속성과 같은 인터페이스에 선언 된 이벤트의 이름과에서 달라 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-181">The name of a method must differ from the names of all properties and events declared in the same interface.</span></span> <span data-ttu-id="902c2-182">또한 서명 ([시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading))의 메서드는 동일한 인터페이스에 선언 된 다른 모든 메서드의 시그니처와 달라 야 하 고 같은 인터페이스에 선언 된 두 개의 메서드 서명이 있을 수 없습니다는 전적으로 달라 `ref` 고 `out`입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-182">In addition, the signature ([Signatures and overloading](basic-concepts.md#signatures-and-overloading)) of a method must differ from the signatures of all other methods declared in the same interface, and two methods declared in the same interface may not have signatures that differ solely by `ref` and `out`.</span></span>
*  <span data-ttu-id="902c2-183">속성 또는 이벤트의 이름 같은 인터페이스에 선언 된 다른 모든 멤버의 이름과에서 달라 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-183">The name of a property or event must differ from the names of all other members declared in the same interface.</span></span>
*  <span data-ttu-id="902c2-184">인덱서의 시그니처는 동일한 인터페이스에 선언된 다른 모든 인덱서의 시그니처와 달라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-184">The signature of an indexer must differ from the signatures of all other indexers declared in the same interface.</span></span>

<span data-ttu-id="902c2-185">인터페이스의 상속된 된 멤버는 특히의 일부가 아닌 인터페이스의 선언 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-185">The inherited members of an interface are specifically not part of the declaration space of the interface.</span></span> <span data-ttu-id="902c2-186">따라서 인터페이스 상속된 된 멤버와 멤버 이름 또는 시그니처가 같은를 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-186">Thus, an interface is allowed to declare a member with the same name or signature as an inherited member.</span></span> <span data-ttu-id="902c2-187">이 경우 기본 인터페이스 멤버를 숨기려면 파생된 인터페이스 멤버 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-187">When this occurs, the derived interface member is said to hide the base interface member.</span></span> <span data-ttu-id="902c2-188">상속된 된 멤버 숨기기는 오류로 간주 하지는 않지만 컴파일러 경고가 발생 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-188">Hiding an inherited member is not considered an error, but it does cause the compiler to issue a warning.</span></span> <span data-ttu-id="902c2-189">경고를 표시 하지 않으려면 파생된 인터페이스 멤버의 선언을 포함 해야 합니다는 `new` 한정자는 파생된 멤버가 기본 멤버를 숨기려면 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-189">To suppress the warning, the declaration of the derived interface member must include a `new` modifier to indicate that the derived member is intended to hide the base member.</span></span> <span data-ttu-id="902c2-190">이 항목 설명에 대 한 자세한 [상속을 통해 숨기기](basic-concepts.md#hiding-through-inheritance)합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-190">This topic is discussed further in [Hiding through inheritance](basic-concepts.md#hiding-through-inheritance).</span></span>

<span data-ttu-id="902c2-191">경우는 `new` 한정자는 상속 된 멤버를 숨기지 않는 선언에 포함 되어, 그 결과 경고가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-191">If a `new` modifier is included in a declaration that doesn't hide an inherited member, a warning is issued to that effect.</span></span> <span data-ttu-id="902c2-192">이 경고를 제거 하 여 표시 되지 않는지를 `new` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-192">This warning is suppressed by removing the `new` modifier.</span></span>

<span data-ttu-id="902c2-193">클래스 멤버 `object` 엄격 하 게 말하자면 모든 인터페이스의 멤버를 하지 않습니다 ([인터페이스 멤버](interfaces.md#interface-members)).</span><span class="sxs-lookup"><span data-stu-id="902c2-193">Note that the members in class `object` are not, strictly speaking, members of any interface ([Interface members](interfaces.md#interface-members)).</span></span> <span data-ttu-id="902c2-194">그러나 클래스 멤버 `object` 임의의 인터페이스 형식에서 멤버 조회를 통해 사용할 수 있습니다 ([멤버 조회](expressions.md#member-lookup)).</span><span class="sxs-lookup"><span data-stu-id="902c2-194">However, the members in class `object` are available via member lookup in any interface type ([Member lookup](expressions.md#member-lookup)).</span></span>

### <a name="interface-methods"></a><span data-ttu-id="902c2-195">인터페이스 메서드</span><span class="sxs-lookup"><span data-stu-id="902c2-195">Interface methods</span></span>

<span data-ttu-id="902c2-196">인터페이스 메서드를 사용 하 여 선언 *interface_method_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="902c2-196">Interface methods are declared using *interface_method_declaration*s:</span></span>

```antlr
interface_method_declaration
    : attributes? 'new'? return_type identifier type_parameter_list
      '(' formal_parameter_list? ')' type_parameter_constraints_clause* ';'
    ;
```

<span data-ttu-id="902c2-197">합니다 *특성*를 *return_type*를 *식별자*, 및 *formal_parameter_list* 인터페이스 메서드 선언 동일 클래스에서 메서드 선언의 것을 의미 ([메서드](classes.md#methods)).</span><span class="sxs-lookup"><span data-stu-id="902c2-197">The *attributes*, *return_type*, *identifier*, and *formal_parameter_list* of an interface method declaration have the same meaning as those of a method declaration in a class ([Methods](classes.md#methods)).</span></span> <span data-ttu-id="902c2-198">메서드 본문을 지정 하는 인터페이스 메서드 선언 없습니다 및 선언 하므로 항상 세미콜론으로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-198">An interface method declaration is not permitted to specify a method body, and the declaration therefore always ends with a semicolon.</span></span>

<span data-ttu-id="902c2-199">인터페이스 메서드의 각 형식 매개 변수 형식 입력 안전 해야 합니다. ([분산 안전성](interfaces.md#variance-safety))를 반환 형식 중 하나 여야 합니다 `void` 또는 출력 스레드로부터 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-199">Each formal parameter type of an interface method must be input-safe ([Variance safety](interfaces.md#variance-safety)), and the return type must be either `void` or output-safe.</span></span> <span data-ttu-id="902c2-200">또한 각 클래스 형식 제약 조건, 인터페이스 형식 제약 조건 및 메서드의 형식 매개 변수에서 형식 매개 변수 제약 조건을 입력 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-200">Furthermore, each class type constraint, interface type constraint and type parameter constraint on any type parameter of the method must be input-safe.</span></span>

<span data-ttu-id="902c2-201">이러한 규칙 확인 모든 공변 (covariant) 또는 인터페이스의 반공 변 사용량과 형식 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-201">These rules ensure that any covariant or contravariant usage of the interface remains type-safe.</span></span> <span data-ttu-id="902c2-202">예를 들어 개체에 적용된</span><span class="sxs-lookup"><span data-stu-id="902c2-202">For example,</span></span>
```csharp
interface I<out T> { void M<U>() where U : T; }
```
<span data-ttu-id="902c2-203">유효 하지 않은 때문에 사용법 `T` 에서 형식 매개 변수 제약 조건으로 `U` 입력 안전 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-203">is illegal because the usage of `T` as a type parameter constraint on `U` is not input-safe.</span></span>

<span data-ttu-id="902c2-204">이 제한은 현재 위치에 없는 것은 다음과 같이 형식 안전성을 위반할 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="902c2-204">Were this restriction not in place it would be possible to violate type safety in the following manner:</span></span>
```csharp
class B {}
class D : B{}
class E : B {}
class C : I<D> { public void M<U>() {...} }
...
I<B> b = new C();
b.M<E>();
```
<span data-ttu-id="902c2-205">이 실제로 호출 `C.M<E>`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-205">This is actually a call to `C.M<E>`.</span></span> <span data-ttu-id="902c2-206">호출 해야 하지만 해당 `E` 에서 파생 `D`이므로 형식 안전성 위반 될 여기 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-206">But that call requires that `E` derive from `D`, so type safety would be violated here.</span></span>

### <a name="interface-properties"></a><span data-ttu-id="902c2-207">인터페이스 속성</span><span class="sxs-lookup"><span data-stu-id="902c2-207">Interface properties</span></span>

<span data-ttu-id="902c2-208">사용 하 여 인터페이스 속성 선언 된 *interface_property_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="902c2-208">Interface properties are declared using *interface_property_declaration*s:</span></span>

```antlr
interface_property_declaration
    : attributes? 'new'? type identifier '{' interface_accessors '}'
    ;

interface_accessors
    : attributes? 'get' ';'
    | attributes? 'set' ';'
    | attributes? 'get' ';' attributes? 'set' ';'
    | attributes? 'set' ';' attributes? 'get' ';'
    ;
```

<span data-ttu-id="902c2-209">합니다 *특성*, *유형*, 및 *식별자* 인터페이스 속성 선언에 속성 선언의 것과 의미가 같습니다 클래스 ([ 속성](classes.md#properties)).</span><span class="sxs-lookup"><span data-stu-id="902c2-209">The *attributes*, *type*, and *identifier* of an interface property declaration have the same meaning as those of a property declaration in a class ([Properties](classes.md#properties)).</span></span>

<span data-ttu-id="902c2-210">클래스 속성 선언의의 접근자에 해당 하는 인터페이스 속성 선언의 접근자 ([접근자](classes.md#accessors)) 한다는 점을 제외 하는 접근자 본문 세미콜론은 항상 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-210">The accessors of an interface property declaration correspond to the accessors of a class property declaration ([Accessors](classes.md#accessors)), except that the accessor body must always be a semicolon.</span></span> <span data-ttu-id="902c2-211">따라서 접근자는 단순히 속성 읽기 / 쓰기, 읽기 전용 또는 쓰기 전용 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-211">Thus, the accessors simply indicate whether the property is read-write, read-only, or write-only.</span></span>

<span data-ttu-id="902c2-212">인터페이스 속성의 형식에는 출력 안전 경우 get 접근자를 사용 해야 합니다. set 접근자 있으면 입력 스레드로부터 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-212">The type of an interface property must be output-safe if there is a get accessor, and must be input-safe if there is a set accessor.</span></span>

### <a name="interface-events"></a><span data-ttu-id="902c2-213">이벤트 인터페이스</span><span class="sxs-lookup"><span data-stu-id="902c2-213">Interface events</span></span>

<span data-ttu-id="902c2-214">인터페이스 이벤트를 사용 하 여 선언 된 *interface_event_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="902c2-214">Interface events are declared using *interface_event_declaration*s:</span></span>

```antlr
interface_event_declaration
    : attributes? 'new'? 'event' type identifier ';'
    ;
```

<span data-ttu-id="902c2-215">합니다 *특성*를 *유형*, 및 *식별자* 클래스에서 인터페이스 이벤트 선언 해야 이벤트 선언 것과 의미가 같습니다 ([이벤트 ](classes.md#events)).</span><span class="sxs-lookup"><span data-stu-id="902c2-215">The *attributes*, *type*, and *identifier* of an interface event declaration have the same meaning as those of an event declaration in a class ([Events](classes.md#events)).</span></span>

<span data-ttu-id="902c2-216">인터페이스 이벤트의 형식은 입력 스레드로부터 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-216">The type of an interface event must be input-safe.</span></span>

### <a name="interface-indexers"></a><span data-ttu-id="902c2-217">인터페이스 인덱서</span><span class="sxs-lookup"><span data-stu-id="902c2-217">Interface indexers</span></span>

<span data-ttu-id="902c2-218">인터페이스 인덱서를 사용 하 여 선언 된 *interface_indexer_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="902c2-218">Interface indexers are declared using *interface_indexer_declaration*s:</span></span>

```antlr
interface_indexer_declaration
    : attributes? 'new'? type 'this' '[' formal_parameter_list ']' '{' interface_accessors '}'
    ;
```

<span data-ttu-id="902c2-219">*특성*, *형식*, 및 *formal_parameter_list* 인터페이스 인덱서 선언에 indexer 선언을의 것과 의미가 같습니다 (클래스[ 인덱서](classes.md#indexers)).</span><span class="sxs-lookup"><span data-stu-id="902c2-219">The *attributes*, *type*, and *formal_parameter_list* of an interface indexer declaration have the same meaning as those of an indexer declaration in a class ([Indexers](classes.md#indexers)).</span></span>

<span data-ttu-id="902c2-220">클래스 인덱서 선언의 접근자에 해당 하는 선언 인터페이스 인덱서 접근자 ([인덱서](classes.md#indexers)) 한다는 점을 제외 하는 접근자 본문 세미콜론은 항상 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-220">The accessors of an interface indexer declaration correspond to the accessors of a class indexer declaration ([Indexers](classes.md#indexers)), except that the accessor body must always be a semicolon.</span></span> <span data-ttu-id="902c2-221">따라서 접근자는 단순히 인덱서가 읽기 / 쓰기, 읽기 전용 또는 쓰기 전용 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-221">Thus, the accessors simply indicate whether the indexer is read-write, read-only, or write-only.</span></span>

<span data-ttu-id="902c2-222">모든 정식 매개 변수 유형의 인터페이스 인덱서 입력 스레드로부터 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-222">All the formal parameter types of an interface indexer must be input-safe .</span></span> <span data-ttu-id="902c2-223">또한 모든 `out` 또는 `ref` 정식 매개 변수 형식 출력 스레드로부터 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-223">In addition, any `out` or `ref` formal parameter types must also be output-safe.</span></span> <span data-ttu-id="902c2-224">참고는도 `out` 매개 변수는 기본 실행 플랫폼의 제한으로 인해 입력 스레드로부터 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-224">Note that even `out` parameters are required to be input-safe, due to a limitation of the underlying execution platform.</span></span>

<span data-ttu-id="902c2-225">인터페이스 인덱서 유형의 출력-안전 하 게 해야 경우 get 접근자 및 set 접근자 있으면 입력 안전 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-225">The type of an interface indexer must be output-safe if there is a get accessor, and must be input-safe if there is a set accessor.</span></span>

### <a name="interface-member-access"></a><span data-ttu-id="902c2-226">인터페이스 멤버 액세스</span><span class="sxs-lookup"><span data-stu-id="902c2-226">Interface member access</span></span>

<span data-ttu-id="902c2-227">인터페이스 멤버는 멤버 액세스를 통해 액세스할 수 있습니다 ([me](expressions.md#member-access)) 및 인덱서 액세스 ([인덱서 액세스](expressions.md#indexer-access)) 형식의 식을 `I.M` 하 고 `I[A]`여기서 `I` 인터페이스 형식 이므로 `M` 메서드, 속성 또는 해당 인터페이스 형식, 이벤트 및 `A` 은 인덱서 인수 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-227">Interface members are accessed through member access ([Member access](expressions.md#member-access)) and indexer access ([Indexer access](expressions.md#indexer-access)) expressions of the form `I.M` and `I[A]`, where `I` is an interface type, `M` is a method, property, or event of that interface type, and `A` is an indexer argument list.</span></span>

<span data-ttu-id="902c2-228">엄격 하 게 된 인터페이스에 대 한 단일 상속 (상속 체인의 각 인터페이스는 직접 기본 인터페이스를 정확히 0 개 이상의 있음), 멤버 조회의 효과 ([멤버 조회](expressions.md#member-lookup)), 메서드 호출 ([ 메서드 호출](expressions.md#method-invocations)), 및 인덱서 액세스 ([인덱서 액세스](expressions.md#indexer-access)) 규칙은 정확 하 게 클래스 및 구조체의 경우와 동일: 파생된 멤버 이름 또는 시그니처가 같은 덜 더 많이 파생 된 멤버 숨기기.</span><span class="sxs-lookup"><span data-stu-id="902c2-228">For interfaces that are strictly single-inheritance (each interface in the inheritance chain has exactly zero or one direct base interface), the effects of the member lookup ([Member lookup](expressions.md#member-lookup)), method invocation ([Method invocations](expressions.md#method-invocations)), and indexer access ([Indexer access](expressions.md#indexer-access)) rules are exactly the same as for classes and structs: More derived members hide less derived members with the same name or signature.</span></span> <span data-ttu-id="902c2-229">그러나 다중 상속 인터페이스에 대 한 두 개의 모호성이 발생할 수 있습니다 하거나 더 관련 되지 않은 기본 인터페이스 이름 또는 시그니처가 같은 멤버를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-229">However, for multiple-inheritance interfaces, ambiguities can occur when two or more unrelated base interfaces declare members with the same name or signature.</span></span> <span data-ttu-id="902c2-230">이 섹션에서는 이러한 상황의 몇 가지 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-230">This section shows several examples of such situations.</span></span> <span data-ttu-id="902c2-231">모든 경우에는 명시적 캐스팅이 모호성을 해결 하 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-231">In all cases, explicit casts can be used to resolve the ambiguities.</span></span>

<span data-ttu-id="902c2-232">예제</span><span class="sxs-lookup"><span data-stu-id="902c2-232">In the example</span></span>
```csharp
interface IList
{
    int Count { get; set; }
}

interface ICounter
{
    void Count(int i);
}

interface IListCounter: IList, ICounter {}

class C
{
    void Test(IListCounter x) {
        x.Count(1);                  // Error
        x.Count = 1;                 // Error
        ((IList)x).Count = 1;        // Ok, invokes IList.Count.set
        ((ICounter)x).Count(1);      // Ok, invokes ICounter.Count
    }
}
```
<span data-ttu-id="902c2-233">처음 두 문은 때문에 컴파일 시간 오류가 발생할 멤버 조회 ([멤버 조회](expressions.md#member-lookup))의 `Count` 에서 `IListCounter` 모호 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-233">the first two statements cause compile-time errors because the member lookup ([Member lookup](expressions.md#member-lookup)) of `Count` in `IListCounter` is ambiguous.</span></span> <span data-ttu-id="902c2-234">캐스팅으로 모호성이 해결은 예제에서 볼 수 있듯이, `x` 적절 한 기본 인터페이스 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-234">As illustrated by the example, the ambiguity is resolved by casting `x` to the appropriate base interface type.</span></span> <span data-ttu-id="902c2-235">이러한 캐스트는 런타임 비용 없이-컴파일 시간에 적은 수의 파생된 형식으로 인스턴스를 표시 하는 단순히 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-235">Such casts have no run-time costs—they merely consist of viewing the instance as a less derived type at compile-time.</span></span>

<span data-ttu-id="902c2-236">예제</span><span class="sxs-lookup"><span data-stu-id="902c2-236">In the example</span></span>
```csharp
interface IInteger
{
    void Add(int i);
}

interface IDouble
{
    void Add(double d);
}

interface INumber: IInteger, IDouble {}

class C
{
    void Test(INumber n) {
        n.Add(1);                // Invokes IInteger.Add
        n.Add(1.0);              // Only IDouble.Add is applicable
        ((IInteger)n).Add(1);    // Only IInteger.Add is a candidate
        ((IDouble)n).Add(1);     // Only IDouble.Add is a candidate
    }
}
```
<span data-ttu-id="902c2-237">호출 `n.Add(1)` 선택 `IInteger.Add` 의 오버 로드 해결 규칙을 적용 하 여 [오버 로드 확인](expressions.md#overload-resolution)합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-237">the invocation `n.Add(1)` selects `IInteger.Add` by applying the overload resolution rules of [Overload resolution](expressions.md#overload-resolution).</span></span> <span data-ttu-id="902c2-238">마찬가지로 호출 `n.Add(1.0)` 선택 `IDouble.Add`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-238">Similarly the invocation `n.Add(1.0)` selects `IDouble.Add`.</span></span> <span data-ttu-id="902c2-239">명시적 캐스트를 삽입할 때 방법이 하나만 후보 메서드와 따라서 모호성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-239">When explicit casts are inserted, there is only one candidate method, and thus no ambiguity.</span></span>

<span data-ttu-id="902c2-240">예제</span><span class="sxs-lookup"><span data-stu-id="902c2-240">In the example</span></span>
```csharp
interface IBase
{
    void F(int i);
}

interface ILeft: IBase
{
    new void F(int i);
}

interface IRight: IBase
{
    void G();
}

interface IDerived: ILeft, IRight {}

class A
{
    void Test(IDerived d) {
        d.F(1);                 // Invokes ILeft.F
        ((IBase)d).F(1);        // Invokes IBase.F
        ((ILeft)d).F(1);        // Invokes ILeft.F
        ((IRight)d).F(1);       // Invokes IBase.F
    }
}
```
<span data-ttu-id="902c2-241">합니다 `IBase.F` 하 여 멤버를 숨깁니다는 `ILeft.F` 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-241">the `IBase.F` member is hidden by the `ILeft.F` member.</span></span> <span data-ttu-id="902c2-242">호출 `d.F(1)` 선택 하므로 `ILeft.F`경우에 `IBase.F` 안내 하는 액세스 경로에서 숨겨져 있지가 `IRight`입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-242">The invocation `d.F(1)` thus selects `ILeft.F`, even though `IBase.F` appears to not be hidden in the access path that leads through `IRight`.</span></span>

<span data-ttu-id="902c2-243">다중 상속 인터페이스의 숨기기에 대 한 직관적인 규칙은 단순히이: 모든 액세스 경로에서 숨겨져 멤버 액세스 경로에서 숨겨진 경우.</span><span class="sxs-lookup"><span data-stu-id="902c2-243">The intuitive rule for hiding in multiple-inheritance interfaces is simply this: If a member is hidden in any access path, it is hidden in all access paths.</span></span> <span data-ttu-id="902c2-244">때문에 액세스 경로 `IDerived` 에 `ILeft` 에 `IBase` 숨깁니다 `IBase.F`, 액세스 경로에서 멤버를 숨길 수도 `IDerived` 에 `IRight` 에 `IBase`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-244">Because the access path from `IDerived` to `ILeft` to `IBase` hides `IBase.F`, the member is also hidden in the access path from `IDerived` to `IRight` to `IBase`.</span></span>

## <a name="fully-qualified-interface-member-names"></a><span data-ttu-id="902c2-245">정규화 된 인터페이스 멤버 이름</span><span class="sxs-lookup"><span data-stu-id="902c2-245">Fully qualified interface member names</span></span>

<span data-ttu-id="902c2-246">인터페이스 멤버는 라고도 하 여 해당 ***정규화 된 이름을***입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-246">An interface member is sometimes referred to by its ***fully qualified name***.</span></span> <span data-ttu-id="902c2-247">인터페이스 멤버의 정규화 된 이름을 인터페이스는 멤버는 선언 뒤에 점, 멤버의 이름 뒤의 이름으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-247">The fully qualified name of an interface member consists of the name of the interface in which the member is declared, followed by a dot, followed by the name of the member.</span></span> <span data-ttu-id="902c2-248">멤버가 선언 된 인터페이스를 참조 하는 멤버의 정규화 된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-248">The fully qualified name of a member references the interface in which the member is declared.</span></span> <span data-ttu-id="902c2-249">예를 들어 선언</span><span class="sxs-lookup"><span data-stu-id="902c2-249">For example, given the declarations</span></span>
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}
```
<span data-ttu-id="902c2-250">정규화 된 이름을 `Paint` 은 `IControl.Paint` 이름과 정규화 `SetText` 는 `ITextBox.SetText`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-250">the fully qualified name of `Paint` is `IControl.Paint` and the fully qualified name of `SetText` is `ITextBox.SetText`.</span></span>

<span data-ttu-id="902c2-251">위의 예제에서는 불가능를 가리키도록 `Paint` 으로 `ITextBox.Paint`입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-251">In the example above, it is not possible to refer to `Paint` as `ITextBox.Paint`.</span></span>

<span data-ttu-id="902c2-252">인터페이스는 네임 스페이스의 일부가 되 면 인터페이스 멤버의 정규화 된 이름을 네임 스페이스 이름이 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-252">When an interface is part of a namespace, the fully qualified name of an interface member includes the namespace name.</span></span> <span data-ttu-id="902c2-253">예</span><span class="sxs-lookup"><span data-stu-id="902c2-253">For example</span></span>
```csharp
namespace System
{
    public interface ICloneable
    {
        object Clone();
    }
}
```

<span data-ttu-id="902c2-254">정규화 된 이름, 여기서는 `Clone` 메서드는 `System.ICloneable.Clone`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-254">Here, the fully qualified name of the `Clone` method is `System.ICloneable.Clone`.</span></span>

## <a name="interface-implementations"></a><span data-ttu-id="902c2-255">인터페이스 구현</span><span class="sxs-lookup"><span data-stu-id="902c2-255">Interface implementations</span></span>

<span data-ttu-id="902c2-256">인터페이스는 클래스 및 구조체에서 구현 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-256">Interfaces may be implemented by classes and structs.</span></span> <span data-ttu-id="902c2-257">클래스 또는 구조체를 직접 인터페이스를 구현 함을 나타내려면 인터페이스 식별자는 클래스 또는 구조체의 기본 클래스 목록에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-257">To indicate that a class or struct directly implements an interface, the interface identifier is included in the base class list of the class or struct.</span></span> <span data-ttu-id="902c2-258">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="902c2-258">For example:</span></span>
```csharp
interface ICloneable
{
    object Clone();
}

interface IComparable
{
    int CompareTo(object other);
}

class ListEntry: ICloneable, IComparable
{
    public object Clone() {...}
    public int CompareTo(object other) {...}
}
```

<span data-ttu-id="902c2-259">클래스 또는 구조체 직접 인터페이스를 직접 구현 하는 모든 인터페이스의 기본 인터페이스 구현 암시적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-259">A class or struct that directly implements an interface also directly implements all of the interface's base interfaces implicitly.</span></span> <span data-ttu-id="902c2-260">클래스 또는 구조체는 기본 클래스 목록에 모든 기본 인터페이스를 나열 명시적으로 하지 않는 경우에 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-260">This is true even if the class or struct doesn't explicitly list all base interfaces in the base class list.</span></span> <span data-ttu-id="902c2-261">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="902c2-261">For example:</span></span>
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}

class TextBox: ITextBox
{
    public void Paint() {...}
    public void SetText(string text) {...}
}
```

<span data-ttu-id="902c2-262">여기서 클래스 `TextBox` 둘 다 구현 `IControl` 고 `ITextBox`입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-262">Here, class `TextBox` implements both `IControl` and `ITextBox`.</span></span>

<span data-ttu-id="902c2-263">때 클래스 `C` 직접 C에서 파생 된 모든 클래스 인터페이스 구현도 인터페이스를 암시적으로 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-263">When a class `C` directly implements an interface, all classes derived from C also implement the interface implicitly.</span></span> <span data-ttu-id="902c2-264">클래스 선언에 지정 된 기본 인터페이스는 생성 된 인터페이스 형식이 될 수 있습니다 ([형식 생성](types.md#constructed-types)).</span><span class="sxs-lookup"><span data-stu-id="902c2-264">The base interfaces specified in a class declaration can be constructed interface types ([Constructed types](types.md#constructed-types)).</span></span> <span data-ttu-id="902c2-265">기본 인터페이스를 범위에 있는 형식 매개 변수를 포함할 수 있지만 자체적으로 형식 매개 변수 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-265">A base interface cannot be a type parameter on its own, though it can involve the type parameters that are in scope.</span></span> <span data-ttu-id="902c2-266">다음 코드에서는 클래스를 구현 하 고 생성 된 형식을 확장 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-266">The following code illustrates how a class can implement and extend constructed types:</span></span>
```csharp
class C<U,V> {}

interface I1<V> {}

class D: C<string,int>, I1<string> {}

class E<T>: C<int,T>, I1<T> {}
```

<span data-ttu-id="902c2-267">제네릭 클래스 선언의 기본 인터페이스에 설명 된 고유성 규칙에 맞아야 [구현 된 인터페이스의 고유성](interfaces.md#uniqueness-of-implemented-interfaces)합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-267">The base interfaces of a generic class declaration must satisfy the uniqueness rule described in [Uniqueness of implemented interfaces](interfaces.md#uniqueness-of-implemented-interfaces).</span></span>

### <a name="explicit-interface-member-implementations"></a><span data-ttu-id="902c2-268">명시적 인터페이스 멤버 구현</span><span class="sxs-lookup"><span data-stu-id="902c2-268">Explicit interface member implementations</span></span>

<span data-ttu-id="902c2-269">인터페이스를 구현 하는 용도로 클래스 또는 구조체를 선언할 수 있습니다 ***명시적 인터페이스 멤버 구현을***합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-269">For purposes of implementing interfaces, a class or struct may declare ***explicit interface member implementations***.</span></span> <span data-ttu-id="902c2-270">명시적 인터페이스 멤버 구현에는 정규화 된 인터페이스 멤버 이름을 참조 하는 메서드, 속성, 이벤트 또는 인덱서 선언입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-270">An explicit interface member implementation is a method, property, event, or indexer declaration that references a fully qualified interface member name.</span></span> <span data-ttu-id="902c2-271">예</span><span class="sxs-lookup"><span data-stu-id="902c2-271">For example</span></span>
```csharp
interface IList<T>
{
    T[] GetElements();
}

interface IDictionary<K,V>
{
    V this[K key];
    void Add(K key, V value);
}

class List<T>: IList<T>, IDictionary<int,T>
{
    T[] IList<T>.GetElements() {...}
    T IDictionary<int,T>.this[int index] {...}
    void IDictionary<int,T>.Add(int index, T value) {...}
}
```

<span data-ttu-id="902c2-272">여기 `IDictionary<int,T>.this` 고 `IDictionary<int,T>.Add` 명시적 인터페이스 멤버 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-272">Here `IDictionary<int,T>.this` and `IDictionary<int,T>.Add` are explicit interface member implementations.</span></span>

<span data-ttu-id="902c2-273">일부 경우 인터페이스 멤버의 이름을 나타나는 경우 인터페이스 멤버 구현 될 수 있습니다 명시적 인터페이스 멤버 구현을 사용 하 여 구현 클래스에 대 한 적합 하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-273">In some cases, the name of an interface member may not be appropriate for the implementing class, in which case the interface member may be implemented using explicit interface member implementation.</span></span> <span data-ttu-id="902c2-274">예를 들어 파일 추상화를 구현 하는 클래스를 구현 가능성이 `Close` 효과가 파일 리소스를 해제 하 고 구현 하는 멤버 함수는 `Dispose` 메서드는 `IDisposable` 명시적 인터페이스를 사용 하 여 인터페이스 멤버 구현:</span><span class="sxs-lookup"><span data-stu-id="902c2-274">A class implementing a file abstraction, for example, would likely implement a `Close` member function that has the effect of releasing the file resource, and implement the `Dispose` method of the `IDisposable` interface using explicit interface member implementation:</span></span>
```csharp
interface IDisposable
{
    void Dispose();
}

class MyFile: IDisposable
{
    void IDisposable.Dispose() {
        Close();
    }

    public void Close() {
        // Do what's necessary to close the file
        System.GC.SuppressFinalize(this);
    }
}
```

<span data-ttu-id="902c2-275">명시적 인터페이스 멤버 구현을 메서드 호출, 속성 액세스 또는 인덱서 액세스의 정규화 된 이름을 통해 액세스 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-275">It is not possible to access an explicit interface member implementation through its fully qualified name in a method invocation, property access, or indexer access.</span></span> <span data-ttu-id="902c2-276">명시적 인터페이스 멤버 구현을 인터페이스 인스턴스를 통해서만 액세스할 수 있습니다 및 멤버 이름을 사용 하 여 단순히 경우 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-276">An explicit interface member implementation can only be accessed through an interface instance, and is in that case referenced simply by its member name.</span></span>

<span data-ttu-id="902c2-277">액세스 한정자를 포함 하는 명시적 인터페이스 멤버 구현에 대 한 컴파일 시간 오류 이며 한정자를 포함 하도록 컴파일 타임 오류 `abstract`, `virtual`를 `override`, 또는 `static`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-277">It is a compile-time error for an explicit interface member implementation to include access modifiers, and it is a compile-time error to include the modifiers `abstract`, `virtual`, `override`, or `static`.</span></span>

<span data-ttu-id="902c2-278">명시적 인터페이스 멤버 구현에 다른 멤버 보다 다양 한 내게 필요한 옵션 특징이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-278">Explicit interface member implementations have different accessibility characteristics than other members.</span></span> <span data-ttu-id="902c2-279">명시적 인터페이스 멤버 구현을 메서드 호출 또는 속성 액세스에서 정규화 된 이름을 통해 액세스할 수 없습니다 이기 때문에 개인 의미 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-279">Because explicit interface member implementations are never accessible through their fully qualified name in a method invocation or a property access, they are in a sense private.</span></span> <span data-ttu-id="902c2-280">그러나 인터페이스 인스턴스를 통해 액세스할 수 있습니다, 되므로 있는 공용도 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-280">However, since they can be accessed through an interface instance, they are in a sense also public.</span></span>

<span data-ttu-id="902c2-281">두 가지 기본 용도로 사용 하는 명시적 인터페이스 멤버 구현:</span><span class="sxs-lookup"><span data-stu-id="902c2-281">Explicit interface member implementations serve two primary purposes:</span></span>

*  <span data-ttu-id="902c2-282">명시적 인터페이스 멤버 구현 클래스 또는 구조체 인스턴스를 통해 액세스할 수 없는, 때문에 인터페이스 구현 클래스 또는 구조체의 공용 인터페이스에서 제외할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-282">Because explicit interface member implementations are not accessible through class or struct instances, they allow interface implementations to be excluded from the public interface of a class or struct.</span></span> <span data-ttu-id="902c2-283">클래스는 경우에 특히 유용 하거나 구조체는 해당 클래스 또는 구조체의 소비자에 게 관심 있는 내부 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-283">This is particularly useful when a class or struct implements an internal interface that is of no interest to a consumer of that class or struct.</span></span>
*  <span data-ttu-id="902c2-284">명시적 인터페이스 멤버 구현을 동일한 서명 사용 하 여 인터페이스 멤버의 명확성을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-284">Explicit interface member implementations allow disambiguation of interface members with the same signature.</span></span> <span data-ttu-id="902c2-285">명시적 인터페이스 멤버 구현 하지 않고는 것이 불가능 클래스 또는 구조체에 대 한 다른 구현이 인터페이스 시그니처가 같은 멤버 및 반환 형식에는 것이 불가능 클래스 또는 구조체에 대 한 모든 구현에 있어야 합니다. 동일한 서명 사용 하 여 인터페이스 멤버의 모든 형식을 반환 하지만 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-285">Without explicit interface member implementations it would be impossible for a class or struct to have different implementations of interface members with the same signature and return type, as would it be impossible for a class or struct to have any implementation at all of interface members with the same signature but with different return types.</span></span>

<span data-ttu-id="902c2-286">유효한 것으로 명시적 인터페이스 멤버 구현에 대 한 클래스 또는 구조체 이름을 지정 해야 해당 정규화 된 이름, 형식 및 매개 변수 형식을 정확 하 게 일치 명시적 인터페이스 멤버의 멤버를 포함 하는 기본 클래스 목록에서 인터페이스 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-286">For an explicit interface member implementation to be valid, the class or struct must name an interface in its base class list that contains a member whose fully qualified name, type, and parameter types exactly match those of the explicit interface member implementation.</span></span> <span data-ttu-id="902c2-287">다음 클래스에 따라서</span><span class="sxs-lookup"><span data-stu-id="902c2-287">Thus, in the following class</span></span>
```csharp
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
    int IComparable.CompareTo(object other) {...}    // invalid
}
```
<span data-ttu-id="902c2-288">선언의 `IComparable.CompareTo` 때문에 컴파일 타임 오류가 발생 `IComparable` 의 기본 클래스 목록에 나열 되지 `Shape` 의 기본 인터페이스 아니며, `ICloneable`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-288">the declaration of `IComparable.CompareTo` results in a compile-time error because `IComparable` is not listed in the base class list of `Shape` and is not a base interface of `ICloneable`.</span></span> <span data-ttu-id="902c2-289">마찬가지로, 선언에서</span><span class="sxs-lookup"><span data-stu-id="902c2-289">Likewise, in the declarations</span></span>
```csharp
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
}

class Ellipse: Shape
{
    object ICloneable.Clone() {...}    // invalid
}
```
<span data-ttu-id="902c2-290">선언의 `ICloneable.Clone` 에 `Ellipse` 때문에 컴파일 타임 오류가 발생 `ICloneable` 의 기본 클래스 목록에 명시적으로 나열 되지 `Ellipse`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-290">the declaration of `ICloneable.Clone` in `Ellipse` results in a compile-time error because `ICloneable` is not explicitly listed in the base class list of `Ellipse`.</span></span>

<span data-ttu-id="902c2-291">인터페이스 멤버의 정규화 된 이름에는 멤버를 선언 하는 인터페이스를 참조 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-291">The fully qualified name of an interface member must reference the interface in which the member was declared.</span></span> <span data-ttu-id="902c2-292">선언에 따라서</span><span class="sxs-lookup"><span data-stu-id="902c2-292">Thus, in the declarations</span></span>
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}

class TextBox: ITextBox
{
    void IControl.Paint() {...}
    void ITextBox.SetText(string text) {...}
}
```
<span data-ttu-id="902c2-293">명시적 인터페이스 멤버 구현이 `Paint` 로 써야 `IControl.Paint`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-293">the explicit interface member implementation of `Paint` must be written as `IControl.Paint`.</span></span>

### <a name="uniqueness-of-implemented-interfaces"></a><span data-ttu-id="902c2-294">구현 된 인터페이스의 고유성</span><span class="sxs-lookup"><span data-stu-id="902c2-294">Uniqueness of implemented interfaces</span></span>

<span data-ttu-id="902c2-295">제네릭 형식 선언에 의해 구현 된 인터페이스는 모든 가능한 생성 된 형식에 대 한 고유 유지 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-295">The interfaces implemented by a generic type declaration must remain unique for all possible constructed types.</span></span> <span data-ttu-id="902c2-296">이 규칙 없이 것은 불가능 생성 된 특정 형식에 대 한 호출을 올바른 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-296">Without this rule, it would be impossible to determine the correct method to call for certain constructed types.</span></span> <span data-ttu-id="902c2-297">예를 들어, 제네릭 클래스 선언 된을 다음과 같이 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-297">For example, suppose a generic class declaration were permitted to be written as follows:</span></span>
```csharp
interface I<T>
{
    void F();
}

class X<U,V>: I<U>, I<V>                    // Error: I<U> and I<V> conflict
{
    void I<U>.F() {...}
    void I<V>.F() {...}
}
```

<span data-ttu-id="902c2-298">허용이 인 수 없기 다음과 같은 경우 실행할 코드를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-298">Were this permitted, it would be impossible to determine which code to execute in the following case:</span></span>
```csharp
I<int> x = new X<int,int>();
x.F();
```

<span data-ttu-id="902c2-299">제네릭 형식 선언의 인터페이스 목록에 올바른 인지를 확인 하려면 다음 단계를 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-299">To determine if the interface list of a generic type declaration is valid, the following steps are performed:</span></span>

*  <span data-ttu-id="902c2-300">수 있도록 `L` 제네릭 클래스, 구조체 또는 인터페이스 선언에 직접 지정 된 인터페이스의 목록 `C`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-300">Let `L` be the list of interfaces directly specified in a generic class, struct, or interface declaration `C`.</span></span>
*  <span data-ttu-id="902c2-301">추가할 `L` 인터페이스에 이미 인터페이스의 기본 `L`입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-301">Add to `L` any base interfaces of the interfaces already in `L`.</span></span>
*  <span data-ttu-id="902c2-302">모든 중복을 제거할 `L`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-302">Remove any duplicates from `L`.</span></span>
*  <span data-ttu-id="902c2-303">모든 가능한 생성 형식에서 생성 하는 경우 `C` 하 고 형식 인수를 대체 한 후 `L`, 두 인터페이스를 일으킬 `L` 를 동일 하 게 선언 다음 `C` 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-303">If any possible constructed type created from `C` would, after type arguments are substituted into `L`, cause two interfaces in `L` to be identical, then the declaration of `C` is invalid.</span></span> <span data-ttu-id="902c2-304">제약 조건 선언에는 모든 가능한 생성 된 형식을 결정할 때 고려 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-304">Constraint declarations are not considered when determining all possible constructed types.</span></span>

<span data-ttu-id="902c2-305">클래스 선언에서 `X` 인터페이스 목록 위의 `L` 이루어져 `I<U>` 고 `I<V>`입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-305">In the class declaration `X` above, the interface list `L` consists of `I<U>` and `I<V>`.</span></span> <span data-ttu-id="902c2-306">생성 된 모든 사용 하 여 형식 때문에 선언은 올바르지 않습니다 `U` 고 `V` 동일한 형식이 두 인터페이스로 인해 동일한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-306">The declaration is invalid because any constructed type with `U` and `V` being the same type would cause these two interfaces to be identical types.</span></span>

<span data-ttu-id="902c2-307">통합 다른 상속 수준에서 지정 된 인터페이스에 대 한 두는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-307">It is possible for interfaces specified at different inheritance levels to unify:</span></span>
```csharp
interface I<T>
{
    void F();
}

class Base<U>: I<U>
{
    void I<U>.F() {...}
}

class Derived<U,V>: Base<U>, I<V>    // Ok
{
    void I<V>.F() {...}
}
```

<span data-ttu-id="902c2-308">이 코드는 유효 하더라도 `Derived<U,V>` 둘 다 구현 `I<U>` 고 `I<V>`입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-308">This code is valid even though `Derived<U,V>` implements both `I<U>` and `I<V>`.</span></span> <span data-ttu-id="902c2-309">코드</span><span class="sxs-lookup"><span data-stu-id="902c2-309">The code</span></span>
```csharp
I<int> x = new Derived<int,int>();
x.F();
```
<span data-ttu-id="902c2-310">메서드를 호출 `Derived`, 이후 `Derived<int,int>` 효과적으로 다시 구현 `I<int>` ([다시 구현 하는 인터페이스](interfaces.md#interface-re-implementation)).</span><span class="sxs-lookup"><span data-stu-id="902c2-310">invokes the method in `Derived`, since `Derived<int,int>` effectively re-implements `I<int>` ([Interface re-implementation](interfaces.md#interface-re-implementation)).</span></span>

### <a name="implementation-of-generic-methods"></a><span data-ttu-id="902c2-311">제네릭 메서드의 구현</span><span class="sxs-lookup"><span data-stu-id="902c2-311">Implementation of generic methods</span></span>

<span data-ttu-id="902c2-312">때 제네릭 메서드를 암시적으로 구현 인터페이스 메서드를 각 메서드 형식 매개 변수 여야 합니다 () 선언 모두에 해당 하는 임의의 인터페이스 형식 매개 변수는 적절 한 형식 인수를 사용 하 여 대체 됩니다), (후 위치를 지정 된 제약 조건 메서드 형식 매개 변수는 왼쪽에서 오른쪽으로 서 수 위치도 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-312">When a generic method implicitly implements an interface method, the constraints given for each method type parameter must be equivalent in both declarations (after any interface type parameters are replaced with the appropriate type arguments), where method type parameters are identified by ordinal positions, left to right.</span></span>

<span data-ttu-id="902c2-313">그러나 제네릭 메서드는 인터페이스 메서드를 명시적으로 구현 하는 경우 제약 조건이 없는 구현 방법에 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-313">When a generic method explicitly implements an interface method, however, no constraints are allowed on the implementing method.</span></span> <span data-ttu-id="902c2-314">인터페이스 메서드에서 제약 조건은 상속 대신</span><span class="sxs-lookup"><span data-stu-id="902c2-314">Instead, the constraints are inherited from the interface method</span></span>

```csharp
interface I<A,B,C>
{
    void F<T>(T t) where T: A;
    void G<T>(T t) where T: B;
    void H<T>(T t) where T: C;
}

class C: I<object,C,string>
{
    public void F<T>(T t) {...}                    // Ok
    public void G<T>(T t) where T: C {...}         // Ok
    public void H<T>(T t) where T: string {...}    // Error
}
```

<span data-ttu-id="902c2-315">메서드 `C.F<T>` 암시적으로 구현 `I<object,C,string>.F<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-315">The method `C.F<T>` implicitly implements `I<object,C,string>.F<T>`.</span></span> <span data-ttu-id="902c2-316">이 예에서 `C.F<T>` 하지 필요한 (않으며 허용) 제약 조건을 지정 `T:object` 있으므로 `object` 모든 형식 매개 변수에서 암시적 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-316">In this case, `C.F<T>` is not required (nor permitted) to specify the constraint `T:object` since `object` is an implicit constraint on all type parameters.</span></span> <span data-ttu-id="902c2-317">메서드 `C.G<T>` 암시적으로 구현 `I<object,C,string>.G<T>` 인터페이스 형식 매개 변수는 해당 형식 인수를 사용 하 여 대체 후 인터페이스에서 이러한 제약 조건을 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-317">The method `C.G<T>` implicitly implements `I<object,C,string>.G<T>` because the constraints match those in the interface, after the interface type parameters are replaced with the corresponding type arguments.</span></span> <span data-ttu-id="902c2-318">메서드에 대 한 제약 조건을 `C.H<T>` sealed 형식의 없으므로 오류입니다 (`string` 여기서) 제약 조건으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-318">The constraint for method `C.H<T>` is an error because sealed types (`string` in this case) cannot be used as constraints.</span></span> <span data-ttu-id="902c2-319">제약 조건을 생략 수도 오류가 암시적 인터페이스 메서드 구현 제약 조건과 일치 해야 하므로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-319">Omitting the constraint would also be an error since constraints of implicit interface method implementations are required to match.</span></span> <span data-ttu-id="902c2-320">암시적으로 구현할 수는 따라서 `I<object,C,string>.H<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-320">Thus, it is impossible to implicitly implement `I<object,C,string>.H<T>`.</span></span> <span data-ttu-id="902c2-321">명시적 인터페이스 멤버 구현을 사용 하 여이 인터페이스 메서드를 구현만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-321">This interface method can only be implemented using an explicit interface member implementation:</span></span>
```csharp
class C: I<object,C,string>
{
    ...

    public void H<U>(U u) where U: class {...}

    void I<object,C,string>.H<T>(T t) {
        string s = t;    // Ok
        H<T>(t);
    }
}
```

<span data-ttu-id="902c2-322">이 예제에서는 명시적 인터페이스 멤버 구현이 엄격 하 게 약한 제약 조건이 있는 공용 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-322">In this example, the explicit interface member implementation invokes a public method having strictly weaker constraints.</span></span> <span data-ttu-id="902c2-323">할당 된 `t` 하 `s` 이후 유효 `T` 의 제약 조건을 상속 `T:string`이 제약 조건은 소스 코드에 표현할 수 없는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-323">Note that the assignment from `t` to `s` is valid since `T` inherits a constraint of `T:string`, even though this constraint is not expressible in source code.</span></span>

### <a name="interface-mapping"></a><span data-ttu-id="902c2-324">인터페이스 매핑</span><span class="sxs-lookup"><span data-stu-id="902c2-324">Interface mapping</span></span>

<span data-ttu-id="902c2-325">클래스 또는 구조체는 클래스 또는 구조체의 기본 클래스 목록에 나열 된 인터페이스의 모든 멤버의 구현을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-325">A class or struct must provide implementations of all members of the interfaces that are listed in the base class list of the class or struct.</span></span> <span data-ttu-id="902c2-326">프로세스를 구현 하는 클래스 또는 구조체에서 인터페이스 멤버의 구현을 찾는 이라고 ***인터페이스 매핑을***합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-326">The process of locating implementations of interface members in an implementing class or struct is known as ***interface mapping***.</span></span>

<span data-ttu-id="902c2-327">클래스 또는 구조체에 대 한 인터페이스 매핑을 `C` 의 기본 클래스 목록에 지정 된 각 인터페이스의 각 멤버에 대 한 구현을 찾는 `C`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-327">Interface mapping for a class or struct `C` locates an implementation for each member of each interface specified in the base class list of `C`.</span></span> <span data-ttu-id="902c2-328">특정 인터페이스 멤버의 구현을 `I.M`, 여기서 `I` 는 인터페이스 멤버 `M` 선언, 각 클래스 또는 구조체를 검사 하 여 결정 됩니다 `S`부터 시작 하 여 `C` 및 각 후속 기본 클래스에 대 한 반복 `C`일치 하는 배치 될 때까지:</span><span class="sxs-lookup"><span data-stu-id="902c2-328">The implementation of a particular interface member `I.M`, where `I` is the interface in which the member `M` is declared, is determined by examining each class or struct `S`, starting with `C` and repeating for each successive base class of `C`, until a match is located:</span></span>

*  <span data-ttu-id="902c2-329">경우 `S` 일치 하는 명시적 인터페이스 멤버 구현 선언이 `I` 및 `M`를이 멤버는 구현의 `I.M`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-329">If `S` contains a declaration of an explicit interface member implementation that matches `I` and `M`, then this member is the implementation of `I.M`.</span></span>
*  <span data-ttu-id="902c2-330">그렇지 `S` 일치 하는 static이 아니고 public 멤버의 선언이 포함 `M`를이 멤버는 구현의 `I.M`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-330">Otherwise, if `S` contains a declaration of a non-static public member that matches `M`, then this member is the implementation of `I.M`.</span></span> <span data-ttu-id="902c2-331">멤버는 구현의 멤버로 일치 항목 보다 더 지정 되지 않은 경우 `I.M`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-331">If more than one member matches, it is unspecified which member is the implementation of `I.M`.</span></span> <span data-ttu-id="902c2-332">이 이런 경우에 발생 `S` 생성 된 형식인 여기서 두 멤버를 제네릭 형식에서 선언 된 다른 서명 하지만 형식 인수를 해당 서명이 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-332">This situation can only occur if `S` is a constructed type where the two members as declared in the generic type have different signatures, but the type arguments make their signatures identical.</span></span>

<span data-ttu-id="902c2-333">컴파일 타임 오류가 발생 하는 구현을 기본 클래스 목록에 지정 된 모든 인터페이스의 모든 멤버에 대해 찾을 수 없는 경우 `C`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-333">A compile-time error occurs if implementations cannot be located for all members of all interfaces specified in the base class list of `C`.</span></span> <span data-ttu-id="902c2-334">인터페이스의 멤버는 기본 인터페이스에서 상속 하는 멤버만 포함 하는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-334">Note that the members of an interface include those members that are inherited from base interfaces.</span></span>

<span data-ttu-id="902c2-335">인터페이스 매핑, 클래스 멤버의 목적을 위해 `A` 인터페이스 멤버를 일치 `B` 때:</span><span class="sxs-lookup"><span data-stu-id="902c2-335">For purposes of interface mapping, a class member `A` matches an interface member `B` when:</span></span>

*  <span data-ttu-id="902c2-336">`A` 및 `B` 메서드와 이름, 형식 및 형식 매개 변수 목록이 `A` 고 `B` 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-336">`A` and `B` are methods, and the name, type, and formal parameter lists of `A` and `B` are identical.</span></span>
*  <span data-ttu-id="902c2-337">`A` 및 `B` 속성, 이름 및 유형의 `A` 하 고 `B` 동일 하 고 `A` 으로 동일한 접근자가 `B` (`A` 명시적 인터페이스 없으면 추가 접근자를 사용할 수 멤버 구현)입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-337">`A` and `B` are properties, the name and type of `A` and `B` are identical, and `A` has the same accessors as `B` (`A` is permitted to have additional accessors if it is not an explicit interface member implementation).</span></span>
*  <span data-ttu-id="902c2-338">`A` 및 `B` 는 이벤트로, 이름 및 유형의 `A` 고 `B` 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-338">`A` and `B` are events, and the name and type of `A` and `B` are identical.</span></span>
*  <span data-ttu-id="902c2-339">`A` 및 `B` 인덱서, 형식 및 형식 매개 변수 목록이 `A` 및 `B` 동일 하 고 `A` 으로 동일한 접근자가 `B` (`A` 가 없는 경우 추가 접근자를 사용할 수는 명시적 인터페이스 멤버 구현)입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-339">`A` and `B` are indexers, the type and formal parameter lists of `A` and `B` are identical, and `A` has the same accessors as `B` (`A` is permitted to have additional accessors if it is not an explicit interface member implementation).</span></span>

<span data-ttu-id="902c2-340">주목할 만한 미치는 인터페이스 매핑 알고리즘은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-340">Notable implications of the interface mapping algorithm are:</span></span>

*  <span data-ttu-id="902c2-341">명시적 인터페이스 멤버 구현을 인터페이스 멤버를 구현 하는 클래스 또는 구조체 멤버를 결정할 때 동일한 클래스 또는 구조체의 다른 멤버 보다 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-341">Explicit interface member implementations take precedence over other members in the same class or struct when determining the class or struct member that implements an interface member.</span></span>
*  <span data-ttu-id="902c2-342">Public이 아닌 나 정적 멤버가 인터페이스 매핑을에 참여합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-342">Neither non-public nor static members participate in interface mapping.</span></span>

<span data-ttu-id="902c2-343">예제</span><span class="sxs-lookup"><span data-stu-id="902c2-343">In the example</span></span>
```csharp
interface ICloneable
{
    object Clone();
}

class C: ICloneable
{
    object ICloneable.Clone() {...}
    public object Clone() {...}
}
```
<span data-ttu-id="902c2-344">합니다 `ICloneable.Clone` 소속 `C` 구현 되 `Clone` 에서 `ICloneable` 명시적 인터페이스 멤버 구현을 다른 멤버 보다 우선 하기 때문에 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-344">the `ICloneable.Clone` member of `C` becomes the implementation of `Clone` in `ICloneable` because explicit interface member implementations take precedence over other members.</span></span>

<span data-ttu-id="902c2-345">두 클래스 또는 구조체 구현 하는 경우 또는 동일한 이름, 형식 및 매개 변수 형식을 사용 하 여 멤버를 포함 하는 자세한 인터페이스, 해당 인터페이스 멤버를 단일 클래스 또는 구조체 멤버의 각 매핑할 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-345">If a class or struct implements two or more interfaces containing a member with the same name, type, and parameter types, it is possible to map each of those interface members onto a single class or struct member.</span></span> <span data-ttu-id="902c2-346">예</span><span class="sxs-lookup"><span data-stu-id="902c2-346">For example</span></span>
```csharp
interface IControl
{
    void Paint();
}

interface IForm
{
    void Paint();
}

class Page: IControl, IForm
{
    public void Paint() {...}
}
```

<span data-ttu-id="902c2-347">여기에 `Paint` 메서드가 모두 `IControl` 및 `IForm` 에 매핑되는 `Paint` 에서 메서드 `Page`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-347">Here, the `Paint` methods of both `IControl` and `IForm` are mapped onto the `Paint` method in `Page`.</span></span> <span data-ttu-id="902c2-348">이기도 물론 두 가지 방법에 대 한 별도 명시적 인터페이스 멤버 구현을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-348">It is of course also possible to have separate explicit interface member implementations for the two methods.</span></span>

<span data-ttu-id="902c2-349">클래스 또는 구조체는 숨겨진된 멤버를 포함 하는 인터페이스를 구현 하는 경우 일부 멤버 명시적 인터페이스 멤버 구현을 통해 구현 반드시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-349">If a class or struct implements an interface that contains hidden members, then some members must necessarily be implemented through explicit interface member implementations.</span></span> <span data-ttu-id="902c2-350">예</span><span class="sxs-lookup"><span data-stu-id="902c2-350">For example</span></span>
```csharp
interface IBase
{
    int P { get; }
}

interface IDerived: IBase
{
    new int P();
}
```

<span data-ttu-id="902c2-351">이 인터페이스의 구현을 하나 이상의 명시적 인터페이스 멤버 구현이 필요 하 고 다음 형식 중 하나를 수행 하는</span><span class="sxs-lookup"><span data-stu-id="902c2-351">An implementation of this interface would require at least one explicit interface member implementation, and would take one of the following forms</span></span>
```csharp
class C: IDerived
{
    int IBase.P { get {...} }
    int IDerived.P() {...}
}

class C: IDerived
{
    public int P { get {...} }
    int IDerived.P() {...}
}

class C: IDerived
{
    int IBase.P { get {...} }
    public int P() {...}
}
```

<span data-ttu-id="902c2-352">클래스는 동일한 기본 인터페이스는 여러 인터페이스를 구현 하는 경우 기본 인터페이스의 구현이 한 개만 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-352">When a class implements multiple interfaces that have the same base interface, there can be only one implementation of the base interface.</span></span> <span data-ttu-id="902c2-353">예제</span><span class="sxs-lookup"><span data-stu-id="902c2-353">In the example</span></span>
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}

interface IListBox: IControl
{
    void SetItems(string[] items);
}

class ComboBox: IControl, ITextBox, IListBox
{
    void IControl.Paint() {...}
    void ITextBox.SetText(string text) {...}
    void IListBox.SetItems(string[] items) {...}
}
```
<span data-ttu-id="902c2-354">에 대 한 별도 구현이 불가능 합니다 `IControl` 기본 클래스 목록에 명명 된를 `IControl` 에서 상속 `ITextBox`, 및 `IControl` 상속한 `IListBox`.</span><span class="sxs-lookup"><span data-stu-id="902c2-354">it is not possible to have separate implementations for the `IControl` named in the base class list, the `IControl` inherited by `ITextBox`, and the `IControl` inherited by `IListBox`.</span></span> <span data-ttu-id="902c2-355">실제로 이러한 인터페이스에 대 한 별도 id 개념이 없으므로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-355">Indeed, there is no notion of a separate identity for these interfaces.</span></span> <span data-ttu-id="902c2-356">아니라 구현 `ITextBox` 하 고 `IListBox` 의 동일한 구현을 공유 `IControl`, 및 `ComboBox` 단순히 세 가지 인터페이스를 구현할 것으로 간주 됩니다 `IControl`, `ITextBox`, 및 `IListBox`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-356">Rather, the implementations of `ITextBox` and `IListBox` share the same implementation of `IControl`, and `ComboBox` is simply considered to implement three interfaces, `IControl`, `ITextBox`, and `IListBox`.</span></span>

<span data-ttu-id="902c2-357">기본 클래스의 멤버는 인터페이스 매핑을에 참여합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-357">The members of a base class participate in interface mapping.</span></span> <span data-ttu-id="902c2-358">예제</span><span class="sxs-lookup"><span data-stu-id="902c2-358">In the example</span></span>
```csharp
interface Interface1
{
    void F();
}

class Class1
{
    public void F() {}
    public void G() {}
}

class Class2: Class1, Interface1
{
    new public void G() {}
}
```
<span data-ttu-id="902c2-359">메서드 `F` 에 `Class1` 에 사용 됩니다 `Class2`의 구현의 `Interface1`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-359">the method `F` in `Class1` is used in `Class2`'s implementation of `Interface1`.</span></span>

### <a name="interface-implementation-inheritance"></a><span data-ttu-id="902c2-360">인터페이스 구현 상속</span><span class="sxs-lookup"><span data-stu-id="902c2-360">Interface implementation inheritance</span></span>

<span data-ttu-id="902c2-361">클래스는 해당 기본 클래스에서 제공 하는 모든 인터페이스 구현을 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-361">A class inherits all interface implementations provided by its base classes.</span></span>

<span data-ttu-id="902c2-362">하지 않고 명시적으로 ***다시 구현*** 인터페이스 파생된 클래스를 변경할 수 없습니다 어떤 방식으로 해당 기본 클래스에서 상속 하는 인터페이스 매핑을 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-362">Without explicitly ***re-implementing*** an interface, a derived class cannot in any way alter the interface mappings it inherits from its base classes.</span></span> <span data-ttu-id="902c2-363">예를 들어 선언에서</span><span class="sxs-lookup"><span data-stu-id="902c2-363">For example, in the declarations</span></span>
```csharp
interface IControl
{
    void Paint();
}

class Control: IControl
{
    public void Paint() {...}
}

class TextBox: Control
{
    new public void Paint() {...}
}
```
<span data-ttu-id="902c2-364">`Paint` 에서 메서드 `TextBox` 숨깁니다를 `Paint` 에서 메서드 `Control`, 매핑의 변경 하지 않습니다 하지만 `Control.Paint` 끌어다 `IControl.Paint`, 호출 및 `Paint` 클래스를 통해 인스턴스 및 인터페이스 인스턴스를 같은 영향을 미칠</span><span class="sxs-lookup"><span data-stu-id="902c2-364">the `Paint` method in `TextBox` hides the `Paint` method in `Control`, but it does not alter the mapping of `Control.Paint` onto `IControl.Paint`, and calls to `Paint` through class instances and interface instances will have the following effects</span></span>
```csharp
Control c = new Control();
TextBox t = new TextBox();
IControl ic = c;
IControl it = t;
c.Paint();            // invokes Control.Paint();
t.Paint();            // invokes TextBox.Paint();
ic.Paint();           // invokes Control.Paint();
it.Paint();           // invokes Control.Paint();
```

<span data-ttu-id="902c2-365">그러나 인터페이스 메서드는 클래스의 가상 메서드를 매핑되면 있기 파생된 클래스가 가상 메서드를 재정의 하 고 인터페이스의 구현을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-365">However, when an interface method is mapped onto a virtual method in a class, it is possible for derived classes to override the virtual method and alter the implementation of the interface.</span></span> <span data-ttu-id="902c2-366">예를 들어, 위의 선언을 다시 작성</span><span class="sxs-lookup"><span data-stu-id="902c2-366">For example, rewriting the declarations above to</span></span>
```csharp
interface IControl
{
    void Paint();
}

class Control: IControl
{
    public virtual void Paint() {...}
}

class TextBox: Control
{
    public override void Paint() {...}
}
```
<span data-ttu-id="902c2-367">다음과 같은 효과 관찰 이제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-367">the following effects will now be observed</span></span>
```csharp
Control c = new Control();
TextBox t = new TextBox();
IControl ic = c;
IControl it = t;
c.Paint();            // invokes Control.Paint();
t.Paint();            // invokes TextBox.Paint();
ic.Paint();           // invokes Control.Paint();
it.Paint();           // invokes TextBox.Paint();
```

<span data-ttu-id="902c2-368">명시적 인터페이스 멤버 구현을 선언할 수 없습니다. 가상, 이후 명시적 인터페이스 멤버 구현을 재정의 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-368">Since explicit interface member implementations cannot be declared virtual, it is not possible to override an explicit interface member implementation.</span></span> <span data-ttu-id="902c2-369">그러나 다른 메서드를 호출 하는 명시적 인터페이스 멤버 구현에 대 한 완벽 하 게 유효 하 고 재정의 하는 클래스를 파생 하는 다른 메서드를 선언할 수 있도록 가상입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-369">However, it is perfectly valid for an explicit interface member implementation to call another method, and that other method can be declared virtual to allow derived classes to override it.</span></span> <span data-ttu-id="902c2-370">예</span><span class="sxs-lookup"><span data-stu-id="902c2-370">For example</span></span>
```csharp
interface IControl
{
    void Paint();
}

class Control: IControl
{
    void IControl.Paint() { PaintControl(); }
    protected virtual void PaintControl() {...}
}

class TextBox: Control
{
    protected override void PaintControl() {...}
}
```

<span data-ttu-id="902c2-371">여기에서 파생 된 클래스 `Control` 구현의 특수화할 수 있습니다 `IControl.Paint` 재정의 하 여는 `PaintControl` 메서드.</span><span class="sxs-lookup"><span data-stu-id="902c2-371">Here, classes derived from `Control` can specialize the implementation of `IControl.Paint` by overriding the `PaintControl` method.</span></span>

### <a name="interface-re-implementation"></a><span data-ttu-id="902c2-372">다시 구현 하는 인터페이스</span><span class="sxs-lookup"><span data-stu-id="902c2-372">Interface re-implementation</span></span>

<span data-ttu-id="902c2-373">인터페이스 구현을 상속 된 클래스 수 ***재구현*** 기본 클래스 목록에 포함 하는 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-373">A class that inherits an interface implementation is permitted to ***re-implement*** the interface by including it in the base class list.</span></span>

<span data-ttu-id="902c2-374">인터페이스를 다시 구현 정확히 동일한 규칙을 따릅니다 인터페이스 매핑을 인터페이스의 초기 구현으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-374">A re-implementation of an interface follows exactly the same interface mapping rules as an initial implementation of an interface.</span></span> <span data-ttu-id="902c2-375">따라서 상속 된 인터페이스 매핑을 인터페이스의 다시 구현에 대 한 설정 인터페이스 매핑에 대 한 어떠한 효과가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-375">Thus, the inherited interface mapping has no effect whatsoever on the interface mapping established for the re-implementation of the interface.</span></span> <span data-ttu-id="902c2-376">예를 들어 선언에서</span><span class="sxs-lookup"><span data-stu-id="902c2-376">For example, in the declarations</span></span>
```csharp
interface IControl
{
    void Paint();
}

class Control: IControl
{
    void IControl.Paint() {...}
}

class MyControl: Control, IControl
{
    public void Paint() {}
}
```
<span data-ttu-id="902c2-377">팩트는 `Control` 매핑합니다 `IControl.Paint` 끌어다 `Control.IControl.Paint` 다시 구현에 영향을 주지 않습니다 `MyControl`, 매핑되는 `IControl.Paint` 에 `MyControl.Paint`입니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-377">the fact that `Control` maps `IControl.Paint` onto `Control.IControl.Paint` doesn't affect the re-implementation in `MyControl`, which maps `IControl.Paint` onto `MyControl.Paint`.</span></span>

<span data-ttu-id="902c2-378">공용 멤버 선언 및 상속 된 명시적 인터페이스 멤버 선언 다시 구현 된 인터페이스에 대 한 인터페이스 매핑 프로세스에 참여를 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-378">Inherited public member declarations and inherited explicit interface member declarations participate in the interface mapping process for re-implemented interfaces.</span></span> <span data-ttu-id="902c2-379">예</span><span class="sxs-lookup"><span data-stu-id="902c2-379">For example</span></span>
```csharp
interface IMethods
{
    void F();
    void G();
    void H();
    void I();
}

class Base: IMethods
{
    void IMethods.F() {}
    void IMethods.G() {}
    public void H() {}
    public void I() {}
}

class Derived: Base, IMethods
{
    public void F() {}
    void IMethods.H() {}
}
```

<span data-ttu-id="902c2-380">여기, 구현의 `IMethods` 에 `Derived` 인터페이스 메서드를 매핑합니다 `Derived.F`, `Base.IMethods.G`에 `Derived.IMethods.H`, 및 `Base.I`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-380">Here, the implementation of `IMethods` in `Derived` maps the interface methods onto `Derived.F`, `Base.IMethods.G`, `Derived.IMethods.H`, and `Base.I`.</span></span>

<span data-ttu-id="902c2-381">클래스 인터페이스를 구현 하는 경우이 암시적으로 모든 해당 인터페이스의 기본 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-381">When a class implements an interface, it implicitly also implements all of that interface's base interfaces.</span></span> <span data-ttu-id="902c2-382">마찬가지로, 인터페이스를 다시 구현 이기도 암시적으로 모든 인터페이스의 기본 인터페이스를 다시 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-382">Likewise, a re-implementation of an interface is also implicitly a re-implementation of all of the interface's base interfaces.</span></span> <span data-ttu-id="902c2-383">예</span><span class="sxs-lookup"><span data-stu-id="902c2-383">For example</span></span>
```csharp
interface IBase
{
    void F();
}

interface IDerived: IBase
{
    void G();
}

class C: IDerived
{
    void IBase.F() {...}
    void IDerived.G() {...}
}

class D: C, IDerived
{
    public void F() {...}
    public void G() {...}
}
```

<span data-ttu-id="902c2-384">여기에서 다시 구현의 `IDerived` 다시 구현 `IBase`매핑이 `IBase.F` 끌어다 `D.F`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-384">Here, the re-implementation of `IDerived` also re-implements `IBase`, mapping `IBase.F` onto `D.F`.</span></span>

### <a name="abstract-classes-and-interfaces"></a><span data-ttu-id="902c2-385">추상 클래스 및 인터페이스</span><span class="sxs-lookup"><span data-stu-id="902c2-385">Abstract classes and interfaces</span></span>

<span data-ttu-id="902c2-386">추상 클래스는 추상 클래스와 마찬가지로 클래스의 기본 클래스 목록에 나열 된 인터페이스의 모든 멤버의 구현을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-386">Like a non-abstract class, an abstract class must provide implementations of all members of the interfaces that are listed in the base class list of the class.</span></span> <span data-ttu-id="902c2-387">그러나 추상 클래스는 인터페이스 메서드를 추상 메서드에 매핑할 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-387">However, an abstract class is permitted to map interface methods onto abstract methods.</span></span> <span data-ttu-id="902c2-388">예</span><span class="sxs-lookup"><span data-stu-id="902c2-388">For example</span></span>
```csharp
interface IMethods
{
    void F();
    void G();
}

abstract class C: IMethods
{
    public abstract void F();
    public abstract void G();
}
```

<span data-ttu-id="902c2-389">여기, 구현의 `IMethods` 매핑합니다 `F` 하 고 `G` 에서 파생 된 비추상 클래스에서 재정의 되어야 하는 추상 메서드에 `C`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-389">Here, the implementation of `IMethods` maps `F` and `G` onto abstract methods, which must be overridden in non-abstract classes that derive from `C`.</span></span>

<span data-ttu-id="902c2-390">명시적 인터페이스 멤버 구현에서는 추상 일 수는 없지만 명시적 인터페이스 멤버 구현을 물론 추상 메서드를 호출할 수는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-390">Note that explicit interface member implementations cannot be abstract, but explicit interface member implementations are of course permitted to call abstract methods.</span></span> <span data-ttu-id="902c2-391">예</span><span class="sxs-lookup"><span data-stu-id="902c2-391">For example</span></span>
```csharp
interface IMethods
{
    void F();
    void G();
}

abstract class C: IMethods
{
    void IMethods.F() { FF(); }
    void IMethods.G() { GG(); }
    protected abstract void FF();
    protected abstract void GG();
}
```

<span data-ttu-id="902c2-392">여기에서 파생 된 비추상 클래스 `C` 재정의 하는 데 필요한 `FF` 하 고 `GG`의 실제 구현을 제공 `IMethods`합니다.</span><span class="sxs-lookup"><span data-stu-id="902c2-392">Here, non-abstract classes that derive from `C` would be required to override `FF` and `GG`, thus providing the actual implementation of `IMethods`.</span></span>
