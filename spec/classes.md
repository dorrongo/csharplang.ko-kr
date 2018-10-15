# <a name="classes"></a><span data-ttu-id="143b6-101">클래스</span><span class="sxs-lookup"><span data-stu-id="143b6-101">Classes</span></span>

<span data-ttu-id="143b6-102">클래스에는 데이터 멤버 (상수 및 필드) 함수 멤버 (메서드, 속성, 이벤트, 인덱서, 연산자, 인스턴스 생성자, 소멸자 및 정적 생성자) 및 중첩 된 형식을 포함할 수 있는 데이터 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-102">A class is a data structure that may contain data members (constants and fields), function members (methods, properties, events, indexers, operators, instance constructors, destructors and static constructors), and nested types.</span></span> <span data-ttu-id="143b6-103">클래스 형식은 상속을 파생된 클래스를 확장 하 고 기본 클래스를 특수화할 수 가능해 집니다 메커니즘을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-103">Class types support inheritance, a mechanism whereby a derived class can extend and specialize a base class.</span></span>

## <a name="class-declarations"></a><span data-ttu-id="143b6-104">클래스 선언</span><span class="sxs-lookup"><span data-stu-id="143b6-104">Class declarations</span></span>

<span data-ttu-id="143b6-105">A *class_declaration* 되는 *type_declaration* ([형식 선언을](namespaces.md#type-declarations)) 새 클래스를 선언 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-105">A *class_declaration* is a *type_declaration* ([Type declarations](namespaces.md#type-declarations)) that declares a new class.</span></span>

```antlr
class_declaration
    : attributes? class_modifier* 'partial'? 'class' identifier type_parameter_list?
      class_base? type_parameter_constraints_clause* class_body ';'?
    ;
```

<span data-ttu-id="143b6-106">A *class_declaration* 선택적 집합으로 이루어져 *특성* ([특성](attributes.md))의 선택적 집합 뒤에, *class_modifier*s ([한정자 클래스](classes.md#class-modifiers)), 선택적 `partial` 키워드 뒤에 한정자 `class` 와 *식별자* 뒤에 클래스 이름을 지정 하는 선택적 *type_parameter_list* ([형식 매개 변수](classes.md#type-parameters)), 선택적 *class_base* 사양 ([클래스 기본 사양](classes.md#class-base-specification))의 선택적 집합 뒤 *type_parameter_constraints_clause*s ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)), 뒤에 *class_body*  ([본문 클래스](classes.md#class-body)), 세미콜론 뒤에 선택적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-106">A *class_declaration* consists of an optional set of *attributes* ([Attributes](attributes.md)), followed by an optional set of *class_modifier*s ([Class modifiers](classes.md#class-modifiers)), followed by an optional `partial` modifier, followed by the keyword `class` and an *identifier* that names the class, followed by an optional *type_parameter_list* ([Type parameters](classes.md#type-parameters)), followed by an optional *class_base* specification ([Class base specification](classes.md#class-base-specification)) , followed by an optional set of *type_parameter_constraints_clause*s ([Type parameter constraints](classes.md#type-parameter-constraints)), followed by a *class_body* ([Class body](classes.md#class-body)), optionally followed by a semicolon.</span></span>

<span data-ttu-id="143b6-107">클래스 선언에서 제공할 수 없습니다 *type_parameter_constraints_clause*s도 제공 하지 않는 경우를 *type_parameter_list*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-107">A class declaration cannot supply *type_parameter_constraints_clause*s unless it also supplies a *type_parameter_list*.</span></span>

<span data-ttu-id="143b6-108">제공 하는 클래스 선언을 *type_parameter_list* 되는 ***제네릭 클래스 선언의***.</span><span class="sxs-lookup"><span data-stu-id="143b6-108">A class declaration that supplies a *type_parameter_list* is a ***generic class declaration***.</span></span> <span data-ttu-id="143b6-109">또한 제네릭 클래스 선언 또는 일반 구조체 선언 내에 중첩 된 모든 클래스 이므로 자체 제네릭 클래스 선언 만들려면 생성된 된 형식을 포함 하는 형식에 대 한 형식 매개 변수를 제공 해야 합니다입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-109">Additionally, any class nested inside a generic class declaration or a generic struct declaration is itself a generic class declaration, since type parameters for the containing type must be supplied to create a constructed type.</span></span>

### <a name="class-modifiers"></a><span data-ttu-id="143b6-110">클래스 한정자</span><span class="sxs-lookup"><span data-stu-id="143b6-110">Class modifiers</span></span>

<span data-ttu-id="143b6-111">A *class_declaration* 클래스 한정자의 시퀀스를 선택적으로 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-111">A *class_declaration* may optionally include a sequence of class modifiers:</span></span>

```antlr
class_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'abstract'
    | 'sealed'
    | 'static'
    | class_modifier_unsafe
    ;
```

<span data-ttu-id="143b6-112">이 같은 한정자를 클래스 선언에 여러 번 표시에 대 한 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-112">It is a compile-time error for the same modifier to appear multiple times in a class declaration.</span></span>

<span data-ttu-id="143b6-113">`new` 중첩된 클래스 한정자가 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-113">The `new` modifier is permitted on nested classes.</span></span> <span data-ttu-id="143b6-114">지정 된 클래스는 동일한 이름으로 상속된 된 멤버를 숨깁니다에 설명 된 대로 [새 한정자](classes.md#the-new-modifier)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-114">It specifies that the class hides an inherited member by the same name, as described in [The new modifier](classes.md#the-new-modifier).</span></span> <span data-ttu-id="143b6-115">에 대 한 컴파일 시간 오류는 `new` 한정자를 중첩된 클래스 선언 되지 않은 클래스 선언에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-115">It is a compile-time error for the `new` modifier to appear on a class declaration that is not a nested class declaration.</span></span>

<span data-ttu-id="143b6-116">합니다 `public`, `protected`를 `internal`, 및 `private` 한정자 클래스의 접근성을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-116">The `public`, `protected`, `internal`, and `private` modifiers control the accessibility of the class.</span></span> <span data-ttu-id="143b6-117">클래스 선언 발생 하는 컨텍스트에 따라 이러한 한정자의 일부 없습니다 허용할 수도 있습니다 ([접근성을 선언](basic-concepts.md#declared-accessibility)).</span><span class="sxs-lookup"><span data-stu-id="143b6-117">Depending on the context in which the class declaration occurs, some of these modifiers may not be permitted ([Declared accessibility](basic-concepts.md#declared-accessibility)).</span></span>

<span data-ttu-id="143b6-118">합니다 `abstract`, `sealed` 및 `static` 한정자는 다음 섹션에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-118">The `abstract`, `sealed` and `static` modifiers are discussed in the following sections.</span></span>

#### <a name="abstract-classes"></a><span data-ttu-id="143b6-119">추상 클래스</span><span class="sxs-lookup"><span data-stu-id="143b6-119">Abstract classes</span></span>

<span data-ttu-id="143b6-120">`abstract` 한정자는 클래스는 불완전 한 기본 클래스로 사용할 것을 나타내는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-120">The `abstract` modifier is used to indicate that a class is incomplete and that it is intended to be used only as a base class.</span></span> <span data-ttu-id="143b6-121">추상 클래스는 다음과 같은 방법으로에서 추상이 아닌 클래스와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-121">An abstract class differs from a non-abstract class in the following ways:</span></span>

*  <span data-ttu-id="143b6-122">추상 클래스를 직접 인스턴스화할 수 없습니다 및 컴파일 시간 오류를 사용 하는 것은 `new` 추상 클래스에서 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-122">An abstract class cannot be instantiated directly, and it is a compile-time error to use the `new` operator on an abstract class.</span></span> <span data-ttu-id="143b6-123">변수 및 컴파일 시간 형식이 추상이 값을 가질 수 있지만, 이러한 변수 및 값은 반드시 일 `null` 추상 형식에서 파생 된 비추상 클래스의 인스턴스에 대 한 참조를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-123">While it is possible to have variables and values whose compile-time types are abstract, such variables and values will necessarily either be `null` or contain references to instances of non-abstract classes derived from the abstract types.</span></span>
*  <span data-ttu-id="143b6-124">추상 클래스는 허용 (하지만 필요 하지 않습니다) 추상 멤버를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-124">An abstract class is permitted (but not required) to contain abstract members.</span></span>
*  <span data-ttu-id="143b6-125">추상 클래스는 sealed 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-125">An abstract class cannot be sealed.</span></span>

<span data-ttu-id="143b6-126">비추상 클래스는 추상 클래스에서 파생 됩니다 비추상 클래스의 모든 상속 된 추상 멤버를 해당 추상 멤버를 재정의 하므로 실제 구현이 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-126">When a non-abstract class is derived from an abstract class, the non-abstract class must include actual implementations of all inherited abstract members, thereby overriding those abstract members.</span></span> <span data-ttu-id="143b6-127">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-127">In the example</span></span>
```csharp
abstract class A
{
    public abstract void F();
}

abstract class B: A
{
    public void G() {}
}

class C: B
{
    public override void F() {
        // actual implementation of F
    }
}
```
<span data-ttu-id="143b6-128">추상 클래스 `A` 추상 메서드를 소개 `F`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-128">the abstract class `A` introduces an abstract method `F`.</span></span> <span data-ttu-id="143b6-129">클래스 `B` 에서 추가 메서드 `G`, 되지만의 구현을 제공 하지 않기 때문에 `F`, `B` 추상 선언도 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-129">Class `B` introduces an additional method `G`, but since it doesn't provide an implementation of `F`, `B` must also be declared abstract.</span></span> <span data-ttu-id="143b6-130">클래스 `C` 재정의 `F` 실제 구현을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-130">Class `C` overrides `F` and provides an actual implementation.</span></span> <span data-ttu-id="143b6-131">때문에 추상 멤버가 없거나 `C`, `C` 허용 (있지만 필요 하지 않습니다) 비추상 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-131">Since there are no abstract members in `C`, `C` is permitted (but not required) to be non-abstract.</span></span>

#### <a name="sealed-classes"></a><span data-ttu-id="143b6-132">봉인된 클래스</span><span class="sxs-lookup"><span data-stu-id="143b6-132">Sealed classes</span></span>

<span data-ttu-id="143b6-133">`sealed` 클래스에서 파생을 방지 하려면 한정자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-133">The `sealed` modifier is used to prevent derivation from a class.</span></span> <span data-ttu-id="143b6-134">봉인 된 클래스는 다른 클래스의 기본 클래스로 지정 된 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-134">A compile-time error occurs if a sealed class is specified as the base class of another class.</span></span>

<span data-ttu-id="143b6-135">봉인 된 클래스는 추상 클래스 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-135">A sealed class cannot also be an abstract class.</span></span>

<span data-ttu-id="143b6-136">`sealed` 한정자 의도 하지 않은 파생을 방지 하기 위해 주로 사용 되지만 특정 런타임 최적화도 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-136">The `sealed` modifier is primarily used to prevent unintended derivation, but it also enables certain run-time optimizations.</span></span> <span data-ttu-id="143b6-137">특히 있기 때문에 절대로 모든 파생된 클래스를 봉인된 클래스 알려져 가상 함수 멤버를 sealed 클래스 인스턴스에서 호출 비가상 호출으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-137">In particular, because a sealed class is known to never have any derived classes, it is possible to transform virtual function member invocations on sealed class instances into non-virtual invocations.</span></span>

#### <a name="static-classes"></a><span data-ttu-id="143b6-138">정적 클래스</span><span class="sxs-lookup"><span data-stu-id="143b6-138">Static classes</span></span>

<span data-ttu-id="143b6-139">합니다 `static` 한정자로 선언 되는 클래스를 표시 되는 ***정적 클래스***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-139">The `static` modifier is used to mark the class being declared as a ***static class***.</span></span> <span data-ttu-id="143b6-140">정적 클래스는 인스턴스화할 수 없습니다, 형식으로 사용할 수 없습니다 및 정적 멤버만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-140">A static class cannot be instantiated, cannot be used as a type and can contain only static members.</span></span> <span data-ttu-id="143b6-141">정적 클래스에는 확장 메서드의 선언을 포함할 수만 ([확장 메서드](classes.md#extension-methods)).</span><span class="sxs-lookup"><span data-stu-id="143b6-141">Only a static class can contain declarations of extension methods ([Extension methods](classes.md#extension-methods)).</span></span>

<span data-ttu-id="143b6-142">정적 클래스 선언을 다음과 같은 제한 사항이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-142">A static class declaration is subject to the following restrictions:</span></span>

*  <span data-ttu-id="143b6-143">정적 클래스를 포함 하지 않은 한 `sealed` 또는 `abstract` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-143">A static class may not include a `sealed` or `abstract` modifier.</span></span> <span data-ttu-id="143b6-144">그러나 Note, 정적 클래스는 인스턴스화되거나에서 파생 된 수 없습니다, 이후 작동 하는지 sealed 및 abstract 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-144">Note, however, that since a static class cannot be instantiated or derived from, it behaves as if it was both sealed and abstract.</span></span>
*  <span data-ttu-id="143b6-145">정적 클래스는 포함 되지 않을 수는 *class_base* 사양 ([기본 사양 클래스](classes.md#class-base-specification)) 및 기본 클래스 또는 구현 된 인터페이스 목록에 명시적으로 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-145">A static class may not include a *class_base* specification ([Class base specification](classes.md#class-base-specification)) and cannot explicitly specify a base class or a list of implemented interfaces.</span></span> <span data-ttu-id="143b6-146">정적 클래스 형식에서 암시적으로 상속 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-146">A static class implicitly inherits from type `object`.</span></span>
*  <span data-ttu-id="143b6-147">정적 클래스는 정적 멤버만 포함할 수 있습니다 ([정적 및 인스턴스 멤버](classes.md#static-and-instance-members)).</span><span class="sxs-lookup"><span data-stu-id="143b6-147">A static class can only contain static members ([Static and instance members](classes.md#static-and-instance-members)).</span></span> <span data-ttu-id="143b6-148">참고 상수 및 중첩된 형식은 정적 구성원으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-148">Note that constants and nested types are classified as static members.</span></span>
*  <span data-ttu-id="143b6-149">정적 클래스 멤버를 사용할 수 없습니다 `protected` 또는 `protected internal` 접근성을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-149">A static class cannot have members with `protected` or `protected internal` declared accessibility.</span></span>

<span data-ttu-id="143b6-150">이는 이러한 제한 사항을 위반에 컴파일 타임 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-150">It is a compile-time error to violate any of these restrictions.</span></span>

<span data-ttu-id="143b6-151">정적 클래스 인스턴스에 생성자가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-151">A static class has no instance constructors.</span></span> <span data-ttu-id="143b6-152">정적 클래스의 인스턴스 생성자와 기본 인스턴스 생성자를 선언 하는 것이 불가능 ([기본 생성자](classes.md#default-constructors)) 정적 클래스에 대해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-152">It is not possible to declare an instance constructor in a static class, and no default instance constructor ([Default constructors](classes.md#default-constructors)) is provided for a static class.</span></span>

<span data-ttu-id="143b6-153">정적 클래스의 멤버 이며 자동으로 정적 멤버 선언에서 명시적으로 포함 해야는 `static` 한정자 (제외 하 고 상수 및 중첩 된 형식).</span><span class="sxs-lookup"><span data-stu-id="143b6-153">The members of a static class are not automatically static, and the member declarations must explicitly include a `static` modifier (except for constants and nested types).</span></span> <span data-ttu-id="143b6-154">클래스는 정적 외부 클래스 내에서 중첩 되 면 중첩 된 클래스 경우 정적 클래스를 명시적으로 포함 하지 않는 한를 `static` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-154">When a class is nested within a static outer class, the nested class is not a static class unless it explicitly includes a `static` modifier.</span></span>

<span data-ttu-id="143b6-155">__정적 클래스 형식 참조__</span><span class="sxs-lookup"><span data-stu-id="143b6-155">__Referencing static class types__</span></span>

<span data-ttu-id="143b6-156">A *namespace_or_type_name* ([Namespace 및 형식 이름](basic-concepts.md#namespace-and-type-names)) 경우에 정적 클래스를 참조할 수</span><span class="sxs-lookup"><span data-stu-id="143b6-156">A *namespace_or_type_name* ([Namespace and type names](basic-concepts.md#namespace-and-type-names)) is permitted to reference a static class if</span></span>

*  <span data-ttu-id="143b6-157">*namespace_or_type_name* 은 합니다 `T` 에 *namespace_or_type_name* 폼의 `T.I`, 또는</span><span class="sxs-lookup"><span data-stu-id="143b6-157">The *namespace_or_type_name* is the `T` in a *namespace_or_type_name* of the form `T.I`, or</span></span>
*  <span data-ttu-id="143b6-158">*namespace_or_type_name* 는 `T` 에 *typeof_expression* ([인수 목록](expressions.md#argument-lists)1) 형식의 `typeof(T)`.</span><span class="sxs-lookup"><span data-stu-id="143b6-158">The *namespace_or_type_name* is the `T` in a *typeof_expression* ([Argument lists](expressions.md#argument-lists)1) of the form `typeof(T)`.</span></span>

<span data-ttu-id="143b6-159">A *primary_expression* ([멤버 함수](expressions.md#function-members)) 경우에 정적 클래스를 참조할 수</span><span class="sxs-lookup"><span data-stu-id="143b6-159">A *primary_expression* ([Function members](expressions.md#function-members)) is permitted to reference a static class if</span></span>

*  <span data-ttu-id="143b6-160">*primary_expression* 는 `E` 에 *member_access* ([동적 오버 로드 확인 검사 하는 컴파일 타임](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) 폼의 `E.I`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-160">The *primary_expression* is the `E` in a *member_access* ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) of the form `E.I`.</span></span>

<span data-ttu-id="143b6-161">다른 컨텍스트에서 정적 클래스를 참조 하는 컴파일 타임 오류</span><span class="sxs-lookup"><span data-stu-id="143b6-161">In any other context it is a compile-time error to reference a static class.</span></span> <span data-ttu-id="143b6-162">예를 들어, 것이 구성 요소 형식, 기본 클래스로 사용 하기 위한 정적 클래스에 대 한 오류 ([중첩 형식은](classes.md#nested-types)) 멤버, 제네릭 형식 인수 또는 형식 매개 변수 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-162">For example, it is an error for a static class to be used as a base class, a constituent type ([Nested types](classes.md#nested-types)) of a member, a generic type argument, or a type parameter constraint.</span></span> <span data-ttu-id="143b6-163">마찬가지로, 배열 형식, 포인터 형식에에서 정적 클래스를 사용할 수 없습니다는 `new` 식, 캐스트 식에는 `is` 식은 `as` 식을 `sizeof` 식 또는 기본 값 식.</span><span class="sxs-lookup"><span data-stu-id="143b6-163">Likewise, a static class cannot be used in an array type, a pointer type, a `new` expression, a cast expression, an `is` expression, an `as` expression, a `sizeof` expression, or a default value expression.</span></span>

### <a name="partial-modifier"></a><span data-ttu-id="143b6-164">Partial 한정자</span><span class="sxs-lookup"><span data-stu-id="143b6-164">Partial modifier</span></span>

<span data-ttu-id="143b6-165">`partial` 한정자를 나타내는 데는이 *class_declaration* 부분 형식 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-165">The `partial` modifier is used to indicate that this *class_declaration* is a partial type declaration.</span></span> <span data-ttu-id="143b6-166">에 지정 된 규칙에 따라 바깥쪽 형식 또는 네임 스페이스 선언 내에서 동일한 이름 가진 여러 부분 형식 선언을 폼 형식 선언에 결합 [부분 형식](classes.md#partial-types)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-166">Multiple partial type declarations with the same name within an enclosing namespace or type declaration combine to form one type declaration, following the rules specified in [Partial types](classes.md#partial-types).</span></span>

<span data-ttu-id="143b6-167">별도 프로그램 텍스트 세그먼트를 분산 하는 클래스 선언에 있는 이러한 세그먼트는 생성 하거나 다른 컨텍스트에서 유지 관리 하는 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-167">Having the declaration of a class distributed over separate segments of program text can be useful if these segments are produced or maintained in different contexts.</span></span> <span data-ttu-id="143b6-168">예를 들어 다른 수동으로 작성 하는 반면 클래스 선언에의 한 부분을 생성 하는 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-168">For instance, one part of a class declaration may be machine generated, whereas the other is manually authored.</span></span> <span data-ttu-id="143b6-169">두 텍스트 분리는 다른 업데이트와의 충돌 씩 업데이트를 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-169">Textual separation of the two prevents updates by one from conflicting with updates by the other.</span></span>

### <a name="type-parameters"></a><span data-ttu-id="143b6-170">형식 매개 변수</span><span class="sxs-lookup"><span data-stu-id="143b6-170">Type parameters</span></span>

<span data-ttu-id="143b6-171">형식 매개 변수는 생성 된 형식을 만들려면 제공 되는 형식 인수에 대 한 자리 표시자를 나타내는 단순 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-171">A type parameter is a simple identifier that denotes a placeholder for a type argument supplied to create a constructed type.</span></span> <span data-ttu-id="143b6-172">형식 매개 변수는 나중에 제공 되는 형식에 대 한 형식 자리 표시자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-172">A type parameter is a formal placeholder for a type that will be supplied later.</span></span> <span data-ttu-id="143b6-173">반대로, 형식 인수 ([형식 인수](types.md#type-arguments)) 생성 된 형식을 만들 때 형식 매개 변수에 대해 대체 되는 실제 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-173">By contrast, a type argument ([Type arguments](types.md#type-arguments)) is the actual type that is substituted for the type parameter when a constructed type is created.</span></span>

```antlr
type_parameter_list
    : '<' type_parameters '>'
    ;

type_parameters
    : attributes? type_parameter
    | type_parameters ',' attributes? type_parameter
    ;

type_parameter
    : identifier
    ;
```

<span data-ttu-id="143b6-174">각 형식 매개 변수에 클래스 선언에서 선언 공간에 이름을 정의 ([선언](basic-concepts.md#declarations))는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-174">Each type parameter in a class declaration defines a name in the declaration space ([Declarations](basic-concepts.md#declarations)) of that class.</span></span> <span data-ttu-id="143b6-175">따라서 다른 형식 매개 변수와 동일한 이름을 가질 수 없습니다 또는 해당 클래스에는 멤버가 선언 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-175">Thus, it cannot have the same name as another type parameter or a member declared in that class.</span></span> <span data-ttu-id="143b6-176">형식 매개 변수 형식 자체와 동일한 이름을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-176">A type parameter cannot have the same name as the type itself.</span></span>

### <a name="class-base-specification"></a><span data-ttu-id="143b6-177">기본 클래스 사양</span><span class="sxs-lookup"><span data-stu-id="143b6-177">Class base specification</span></span>

<span data-ttu-id="143b6-178">클래스 선언 포함 될 수 있습니다는 *class_base* 인터페이스와 클래스의 직접 기본 클래스를 정의 하는 사양 ([인터페이스](interfaces.md)) 클래스에 의해 직접 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-178">A class declaration may include a *class_base* specification, which defines the direct base class of the class and the interfaces ([Interfaces](interfaces.md)) directly implemented by the class.</span></span>

```antlr
class_base
    : ':' class_type
    | ':' interface_type_list
    | ':' class_type ',' interface_type_list
    ;

interface_type_list
    : interface_type (',' interface_type)*
    ;
```

<span data-ttu-id="143b6-179">클래스 선언에 지정 된 기본 클래스는 생성 된 클래스 형식일 수 있습니다 ([형식 생성](types.md#constructed-types)).</span><span class="sxs-lookup"><span data-stu-id="143b6-179">The base class specified in a class declaration can be a constructed class type ([Constructed types](types.md#constructed-types)).</span></span> <span data-ttu-id="143b6-180">기본 클래스 범위에 있는 형식 매개 변수를 포함할 수 있지만 자체적으로 형식 매개 변수 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-180">A base class cannot be a type parameter on its own, though it can involve the type parameters that are in scope.</span></span>

```csharp
class Extend<V>: V {}            // Error, type parameter used as base class
```

#### <a name="base-classes"></a><span data-ttu-id="143b6-181">기본 클래스</span><span class="sxs-lookup"><span data-stu-id="143b6-181">Base classes</span></span>

<span data-ttu-id="143b6-182">경우는 *class_type* 에 포함 되어는 *class_base*, 선언 되는 클래스의 직접 기본 클래스는 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-182">When a *class_type* is included in the *class_base*, it specifies the direct base class of the class being declared.</span></span> <span data-ttu-id="143b6-183">클래스 선언이 없으면 *class_base*, 또는 경우에는 *class_base* 만 목록에 인터페이스 형식, 직접 기본 클래스는 것으로 간주 됩니다 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-183">If a class declaration has no *class_base*, or if the *class_base* lists only interface types, the direct base class is assumed to be `object`.</span></span> <span data-ttu-id="143b6-184">에 설명 된 대로 클래스의 직접 기본 클래스에서 멤버를 상속 [상속](classes.md#inheritance)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-184">A class inherits members from its direct base class, as described in [Inheritance](classes.md#inheritance).</span></span>

<span data-ttu-id="143b6-185">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-185">In the example</span></span>
```csharp
class A {}

class B: A {}
```
<span data-ttu-id="143b6-186">클래스 `A` 의 직접 기본 클래스 라고 `B`, 및 `B` 에서 파생 될 것 이라고 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-186">class `A` is said to be the direct base class of `B`, and `B` is said to be derived from `A`.</span></span> <span data-ttu-id="143b6-187">이후 `A` 는 직접 기본 클래스를 명시적으로 지정, 직접 기본 클래스는 암시적으로 `object`입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-187">Since `A` does not explicitly specify a direct base class, its direct base class is implicitly `object`.</span></span>

<span data-ttu-id="143b6-188">생성 된 클래스 형식에 대 한 기본 클래스는 제네릭 클래스 선언에 지정 된 경우 생성 된 형식의 기본 클래스는 가져온 각각에 대 한 대체 하 여 *type_parameter* 해당 기본 클래스 선언에서 *type_argument* 생성 된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-188">For a constructed class type, if a base class is specified in the generic class declaration, the base class of the constructed type is obtained by substituting, for each *type_parameter* in the base class declaration, the corresponding *type_argument* of the constructed type.</span></span> <span data-ttu-id="143b6-189">지정 된 제네릭 클래스 선언</span><span class="sxs-lookup"><span data-stu-id="143b6-189">Given the generic class declarations</span></span>
```csharp
class B<U,V> {...}

class G<T>: B<string,T[]> {...}
```
<span data-ttu-id="143b6-190">생성 된 형식의 기본 클래스 `G<int>` 것 `B<string,int[]>`입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-190">the base class of the constructed type `G<int>` would be `B<string,int[]>`.</span></span>

<span data-ttu-id="143b6-191">클래스 형식의 직접 기본 클래스는 적어도 클래스 형식 자체 수준 만큼 액세스 가능 해야 합니다. ([접근성 도메인](basic-concepts.md#accessibility-domains)).</span><span class="sxs-lookup"><span data-stu-id="143b6-191">The direct base class of a class type must be at least as accessible as the class type itself ([Accessibility domains](basic-concepts.md#accessibility-domains)).</span></span> <span data-ttu-id="143b6-192">예를 들어, 것이 대 한 컴파일 시간 오류를 `public` 에서 파생 된 클래스를 `private` 또는 `internal` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-192">For example, it is a compile-time error for a `public` class to derive from a `private` or `internal` class.</span></span>

<span data-ttu-id="143b6-193">클래스 형식의 직접 기본 클래스는 아니어야 다음 형식 중 하나: `System.Array`, `System.Delegate`, `System.MulticastDelegate`합니다 `System.Enum`, 또는 `System.ValueType`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-193">The direct base class of a class type must not be any of the following types: `System.Array`, `System.Delegate`, `System.MulticastDelegate`, `System.Enum`, or `System.ValueType`.</span></span> <span data-ttu-id="143b6-194">제네릭 클래스 선언의 사용할 수 없습니다는 또한 `System.Attribute` 직접 또는 간접 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-194">Furthermore, a generic class declaration cannot use `System.Attribute` as a direct or indirect base class.</span></span>

<span data-ttu-id="143b6-195">직접 기본 클래스 지정의 의미를 확인 하는 동안 `A` 클래스의 `B`에서 직접 기본 클래스 `B` 일시적으로 간주 됩니다 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-195">While determining the meaning of the direct base class specification `A` of a class `B`, the direct base class of `B` is temporarily assumed to be `object`.</span></span> <span data-ttu-id="143b6-196">직관적으로 이렇게 하면 기본 클래스를 지정 하는 의미 없는 재귀적으로 자체에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-196">Intuitively this ensures that the meaning of a base class specification cannot recursively depend on itself.</span></span> <span data-ttu-id="143b6-197">예제:</span><span class="sxs-lookup"><span data-stu-id="143b6-197">The example:</span></span>
```csharp
class A<T> {
   public class B {}
}

class C : A<C.B> {}
```
<span data-ttu-id="143b6-198">기본 클래스 사양에 올바르지 `A<C.B>` 의 직접 기본 클래스 `C` 것으로 간주 됩니다 `object`, 및 (규칙에 따라 [Namespace 및 형식 이름](basic-concepts.md#namespace-and-type-names)) `C` 간주 되지 않습니다 회원에 게 `B`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-198">is in error since in the base class specification `A<C.B>` the direct base class of `C` is considered to be `object`, and hence (by the rules of [Namespace and type names](basic-concepts.md#namespace-and-type-names))  `C` is not considered to have a member `B`.</span></span>

<span data-ttu-id="143b6-199">클래스 형식의 기본 클래스는 직접 기본 클래스 및 해당 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-199">The base classes of a class type are the direct base class and its base classes.</span></span> <span data-ttu-id="143b6-200">즉, 일련의 기본 클래스는 직접 기본 클래스 관계의 전이적 closure 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-200">In other words, the set of base classes is the transitive closure of the direct base class relationship.</span></span> <span data-ttu-id="143b6-201">참조의 기본 클래스를 위의 예에서 `B` 됩니다 `A` 및 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-201">Referring to the example above, the base classes of `B` are `A` and `object`.</span></span> <span data-ttu-id="143b6-202">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-202">In the example</span></span>
```csharp
class A {...}

class B<T>: A {...}

class C<T>: B<IComparable<T>> {...}

class D<T>: C<T[]> {...}
```
<span data-ttu-id="143b6-203">기본 클래스 `D<int>` 됩니다 `C<int[]>`를 `B<IComparable<int[]>>`를 `A`, 및 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-203">the base classes of `D<int>` are `C<int[]>`, `B<IComparable<int[]>>`, `A`, and `object`.</span></span>

<span data-ttu-id="143b6-204">클래스를 제외 하 고 `object`, 모든 클래스 형식에는 정확히 하나의 직접 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-204">Except for class `object`, every class type has exactly one direct base class.</span></span> <span data-ttu-id="143b6-205">`object` 클래스는 직접 기본 클래스가 없는 이며 다른 모든 클래스의 궁극적인 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-205">The `object` class has no direct base class and is the ultimate base class of all other classes.</span></span>

<span data-ttu-id="143b6-206">때 클래스 `B` 클래스에서 파생 `A`에 대 한 컴파일 시간 오류 `A` 에 따라 달라 지도록 `B`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-206">When a class `B` derives from a class `A`, it is a compile-time error for `A` to depend on `B`.</span></span> <span data-ttu-id="143b6-207">클래스 ***에 직접 종속*** 의 직접 기본 클래스 (있는 경우) 및 ***에 직접 종속*** 클래스는 즉시 중첩 (있는 경우).</span><span class="sxs-lookup"><span data-stu-id="143b6-207">A class ***directly depends on*** its direct base class (if any) and ***directly depends on*** the class within which it is immediately nested (if any).</span></span> <span data-ttu-id="143b6-208">이 정의 지정 된 클래스는 종속 하는 클래스의 전체 집합은 재귀 및 전이적인 종결 합니다 ***에 직접 종속*** 관계입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-208">Given this definition, the complete set of classes upon which a class depends is the reflexive and transitive closure of the ***directly depends on*** relationship.</span></span>

<span data-ttu-id="143b6-209">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-209">The example</span></span>
```csharp
class A: A {}
```
<span data-ttu-id="143b6-210">잘못 된 이므로 클래스 자체에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-210">is erroneous because the class depends on itself.</span></span> <span data-ttu-id="143b6-211">마찬가지로, 예제</span><span class="sxs-lookup"><span data-stu-id="143b6-211">Likewise, the example</span></span>
```csharp
class A: B {}
class B: C {}
class C: A {}
```
<span data-ttu-id="143b6-212">클래스는 순환적으로 자신에 종속 되어 있으므로 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-212">is in error because the classes circularly depend on themselves.</span></span> <span data-ttu-id="143b6-213">마지막으로, 예제</span><span class="sxs-lookup"><span data-stu-id="143b6-213">Finally, the example</span></span>
```csharp
class A: B.C {}

class B: A
{
    public class C {}
}
```
<span data-ttu-id="143b6-214">때문에 컴파일 타임 오류가 발생 `A` 에 따라 달라 집니다 `B.C` (직접 기본 클래스인)에 따라 다름 `B` (가장 가까운 바깥쪽 클래스)를 순환 종속 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-214">results in a compile-time error because `A` depends on `B.C` (its direct base class), which depends on `B` (its immediately enclosing class), which circularly depends on `A`.</span></span>

<span data-ttu-id="143b6-215">참고 클래스 내에 중첩 된 클래스에 종속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-215">Note that a class does not depend on the classes that are nested within it.</span></span> <span data-ttu-id="143b6-216">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-216">In the example</span></span>
```csharp
class A
{
    class B: A {}
}
```
<span data-ttu-id="143b6-217">`B` 에 따라 달라 집니다 `A` (때문 `A` 의 직접 기본 클래스와 가장 가까운 바깥쪽 클래스는), 있지만 `A` 에 의존 하지 `B` (하므로 `B` 이 기본 클래스도 아니고는 바깥쪽 클래스의 `A` ).</span><span class="sxs-lookup"><span data-stu-id="143b6-217">`B` depends on `A` (because `A` is both its direct base class and its immediately enclosing class), but `A` does not depend on `B` (since `B` is neither a base class nor an enclosing class of `A`).</span></span> <span data-ttu-id="143b6-218">따라서이 예제에서는 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-218">Thus, the example is valid.</span></span>

<span data-ttu-id="143b6-219">파생 될 수 있지는 `sealed` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-219">It is not possible to derive from a `sealed` class.</span></span> <span data-ttu-id="143b6-220">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-220">In the example</span></span>
```csharp
sealed class A {}

class B: A {}            // Error, cannot derive from a sealed class
```
<span data-ttu-id="143b6-221">클래스 `B` 에서 파생 하려고 했기 때문에 오류에는 `sealed` 클래스 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-221">class `B` is in error because it attempts to derive from the `sealed` class `A`.</span></span>

#### <a name="interface-implementations"></a><span data-ttu-id="143b6-222">인터페이스 구현</span><span class="sxs-lookup"><span data-stu-id="143b6-222">Interface implementations</span></span>

<span data-ttu-id="143b6-223">A *class_base* 사양에 있는 경우 클래스는 직접 구현 한다고 지정된 된 인터페이스 형식을 인터페이스 형식 목록이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-223">A *class_base* specification may include a list of interface types, in which case the class is said to directly implement the given interface types.</span></span> <span data-ttu-id="143b6-224">인터페이스 구현을 설명에 대 한 자세한 [인터페이스 구현을](interfaces.md#interface-implementations)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-224">Interface implementations are discussed further in [Interface implementations](interfaces.md#interface-implementations).</span></span>

### <a name="type-parameter-constraints"></a><span data-ttu-id="143b6-225">형식 매개 변수 제약 조건</span><span class="sxs-lookup"><span data-stu-id="143b6-225">Type parameter constraints</span></span>

<span data-ttu-id="143b6-226">제네릭 형식 및 메서드 선언 형식 매개 변수 제약 조건을 포함 하 여 선택적으로 지정할 수 *type_parameter_constraints_clause*s입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-226">Generic type and method declarations can optionally specify type parameter constraints by including *type_parameter_constraints_clause*s.</span></span>

```antlr
type_parameter_constraints_clause
    : 'where' type_parameter ':' type_parameter_constraints
    ;

type_parameter_constraints
    : primary_constraint
    | secondary_constraints
    | constructor_constraint
    | primary_constraint ',' secondary_constraints
    | primary_constraint ',' constructor_constraint
    | secondary_constraints ',' constructor_constraint
    | primary_constraint ',' secondary_constraints ',' constructor_constraint
    ;

primary_constraint
    : class_type
    | 'class'
    | 'struct'
    ;

secondary_constraints
    : interface_type
    | type_parameter
    | secondary_constraints ',' interface_type
    | secondary_constraints ',' type_parameter
    ;

constructor_constraint
    : 'new' '(' ')'
    ;
```

<span data-ttu-id="143b6-227">각 *type_parameter_constraints_clause* 토큰 이루어져 `where`뒤에 형식 매개 변수의 이름, 콜론 및 해당 형식 매개 변수에 대 한 제약 조건 목록 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-227">Each *type_parameter_constraints_clause* consists of the token `where`, followed by the name of a type parameter, followed by a colon and the list of constraints for that type parameter.</span></span> <span data-ttu-id="143b6-228">최대 하나만 수 `where` 각 형식 매개 변수에 대 한 절 및 `where` 절 순서에 관계 없이 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-228">There can be at most one `where` clause for each type parameter, and the `where` clauses can be listed in any order.</span></span> <span data-ttu-id="143b6-229">같은 `get` 및 `set` 속성 접근자에서 토큰을 `where` 토큰은 키워드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-229">Like the `get` and `set` tokens in a property accessor, the `where` token is not a keyword.</span></span>

<span data-ttu-id="143b6-230">에 지정 된 제약 조건 목록이 `where` 절에는 다음 구성 요소를이 순서 대로: 단일 기본 제약 조건, 하나 이상의 보조 제약 조건 및 생성자 제약 조건이 `new()`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-230">The list of constraints given in a `where` clause can include any of the following components, in this order: a single primary constraint, one or more secondary constraints, and the constructor constraint, `new()`.</span></span>

<span data-ttu-id="143b6-231">기본 제약 조건 클래스 형식이 될 수 또는 ***참조 형식 제약 조건*** `class` 또는 ***값 형식 제약 조건*** `struct`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-231">A primary constraint can be a class type or the ***reference type constraint*** `class` or the ***value type constraint*** `struct`.</span></span> <span data-ttu-id="143b6-232">보조 제약 조건 수를 *type_parameter* 하거나 *interface_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-232">A secondary constraint can be a *type_parameter* or *interface_type*.</span></span>

<span data-ttu-id="143b6-233">참조 형식 제약 조건 형식 매개 변수를 사용 하는 형식 인수가 참조 형식이 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-233">The reference type constraint specifies that a type argument used for the type parameter must be a reference type.</span></span> <span data-ttu-id="143b6-234">모든 클래스 형식, 인터페이스 형식, 대리자 형식, 배열 형식 및 형식 매개 변수는 참조 형식 (아래 정의)은 알려진이 제약 조건을 만족 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-234">All class types, interface types, delegate types, array types, and type parameters known to be a reference type (as defined below) satisfy this constraint.</span></span>

<span data-ttu-id="143b6-235">값 형식 제약 조건 형식 매개 변수에 사용 되는 형식 인수를 null이 아닌 값 형식이 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-235">The value type constraint specifies that a type argument used for the type parameter must be a non-nullable value type.</span></span> <span data-ttu-id="143b6-236">Nullable이 아닌 구조체 형식, 열거형 형식 및 값 형식 제약 조건이 있는 형식 매개 변수를 모두이 제약 조건을 만족 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-236">All non-nullable struct types, enum types, and type parameters having the value type constraint satisfy this constraint.</span></span> <span data-ttu-id="143b6-237">값 형식, null 허용 형식으로 분류 하는 있지만 ([Nullable 형식](types.md#nullable-types)) 값 형식 제약 조건을 충족 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-237">Note that although classified as a value type, a nullable type ([Nullable types](types.md#nullable-types)) does not satisfy the value type constraint.</span></span> <span data-ttu-id="143b6-238">값 형식 제약 조건이 있는 형식 매개 변수를 가질 수 없습니다는 *constructor_constraint*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-238">A type parameter having the value type constraint cannot also have the *constructor_constraint*.</span></span>

<span data-ttu-id="143b6-239">포인터 형식은 형식 인수를 허용 되지 않습니다 및 중 하나는 참조 형식 또는 값 형식 제약 조건을 만족 하는 고려 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-239">Pointer types are never allowed to be type arguments and are not considered to satisfy either the reference type or value type constraints.</span></span>

<span data-ttu-id="143b6-240">클래스 형식, 인터페이스 형식 또는 형식 매개 변수 제약 조건이 있으면 해당 형식은 최소한의 "기본 형식" 해당 형식 매개 변수에 사용 되는 모든 형식 인수를 지원 해야 하는 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-240">If a constraint is a class type, an interface type, or a type parameter, that type specifies a minimal "base type" that every type argument used for that type parameter must support.</span></span> <span data-ttu-id="143b6-241">생성 된 형식 또는 제네릭 메서드를 사용할 때마다 형식 인수는 컴파일 시 형식 매개 변수에 대 한 제약 조건에 대해 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-241">Whenever a constructed type or generic method is used, the type argument is checked against the constraints on the type parameter at compile-time.</span></span> <span data-ttu-id="143b6-242">제공 된 형식 인수에 설명 된 조건에 맞아야 [제약 조건을 만족](types.md#satisfying-constraints)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-242">The type argument supplied must satisfy the conditions described in [Satisfying constraints](types.md#satisfying-constraints).</span></span>

<span data-ttu-id="143b6-243">A *class_type* 제약 조건에는 다음 규칙을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-243">A *class_type* constraint must satisfy the following rules:</span></span>

*  <span data-ttu-id="143b6-244">형식을은 클래스 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-244">The type must be a class type.</span></span>
*  <span data-ttu-id="143b6-245">형식이 아니어야 `sealed`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-245">The type must not be `sealed`.</span></span>
*  <span data-ttu-id="143b6-246">형식이 아니어야 다음 형식 중 하나: `System.Array`, `System.Delegate`를 `System.Enum`, 또는 `System.ValueType`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-246">The type must not be one of the following types: `System.Array`, `System.Delegate`, `System.Enum`, or `System.ValueType`.</span></span>
*  <span data-ttu-id="143b6-247">형식이 아니어야 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-247">The type must not be `object`.</span></span> <span data-ttu-id="143b6-248">모든 형식에서 파생 되므로 `object`, 허용 된 경우 이러한 제약 조건을 효과가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-248">Because all types derive from `object`, such a constraint would have no effect if it were permitted.</span></span>
*  <span data-ttu-id="143b6-249">최대 제약 조건을 지정 된 형식 매개 변수는 클래스 형식일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-249">At most one constraint for a given type parameter can be a class type.</span></span>

<span data-ttu-id="143b6-250">으로 지정 된 형식을 *interface_type* 제약 조건에는 다음 규칙을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-250">A type specified as an *interface_type* constraint must satisfy the following rules:</span></span>

*  <span data-ttu-id="143b6-251">형식을은 인터페이스 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-251">The type must be an interface type.</span></span>
*  <span data-ttu-id="143b6-252">형식에서 두 번 이상 지정 하지 해야 합니다는 주어진 `where` 절.</span><span class="sxs-lookup"><span data-stu-id="143b6-252">A type must not be specified more than once in a given `where` clause.</span></span>

<span data-ttu-id="143b6-253">두 경우 모두에서 제약 조건이 연결된 형식 또는 메서드 선언을 생성 된 형식의 일부로 형식 매개 변수 중 하나를 포함할 수 있습니다 하 고 중인 선언 된 형식이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-253">In either case, the constraint can involve any of the type parameters of the associated type or method declaration as part of a constructed type, and can involve the type being declared.</span></span>

<span data-ttu-id="143b6-254">형식 매개 변수 제약 조건 이상 액세스 가능 해야 합니다. 지정 된 모든 클래스 또는 인터페이스 형식 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)) 제네릭 형식 또는 선언 되는 메서드.</span><span class="sxs-lookup"><span data-stu-id="143b6-254">Any class or interface type specified as a type parameter constraint must be at least as accessible ([Accessibility constraints](basic-concepts.md#accessibility-constraints)) as the generic type or method being declared.</span></span>

<span data-ttu-id="143b6-255">로 지정 된 형식에 *type_parameter* 제약 조건에는 다음 규칙을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-255">A type specified as a *type_parameter* constraint must satisfy the following rules:</span></span>

*  <span data-ttu-id="143b6-256">형식은 형식 매개 변수 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-256">The type must be a type parameter.</span></span>
*  <span data-ttu-id="143b6-257">형식에서 두 번 이상 지정 하지 해야 합니다는 주어진 `where` 절.</span><span class="sxs-lookup"><span data-stu-id="143b6-257">A type must not be specified more than once in a given `where` clause.</span></span>

<span data-ttu-id="143b6-258">또한 있어야 순환이 종속성으로 정의 된 전이적 관계가 인 형식 매개 변수 종속성 그래프에서:</span><span class="sxs-lookup"><span data-stu-id="143b6-258">In addition there must be no cycles in the dependency graph of type parameters, where dependency is a transitive relation defined by:</span></span>

*  <span data-ttu-id="143b6-259">경우 형식 매개 변수 `T` 형식 매개 변수는 제약 조건으로 사용 됩니다 `S` 한 다음 `S` ***종속*** `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-259">If a type parameter `T` is used as a constraint for type parameter `S` then `S` ***depends on*** `T`.</span></span>
*  <span data-ttu-id="143b6-260">경우 형식 매개 변수 `S` 형식 매개 변수에 따라 달라 집니다 `T` 하 고 `T` 형식 매개 변수에 따라 달라 집니다 `U` 한 다음 `S` ***에 따라 달라 집니다*** `U`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-260">If a type parameter `S` depends on a type parameter `T` and `T` depends on a type parameter `U` then `S` ***depends on*** `U`.</span></span>

<span data-ttu-id="143b6-261">이 관계를 지정 합니다 (직접 또는 간접적으로) 자체에 따라 형식 매개 변수의 컴파일 타임 오류를 것입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-261">Given this relation, it is a compile-time error for a type parameter to depend on itself (directly or indirectly).</span></span>

<span data-ttu-id="143b6-262">모든 제약 조건을 종속 형식 매개 변수 간에 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-262">Any constraints must be consistent among dependent type parameters.</span></span> <span data-ttu-id="143b6-263">경우 형식 매개 변수 `S` 형식 매개 변수에 따라 달라 집니다 `T` 후:</span><span class="sxs-lookup"><span data-stu-id="143b6-263">If type parameter `S` depends on type parameter `T` then:</span></span>

*  <span data-ttu-id="143b6-264">`T` 값 형식 제약 조건이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-264">`T` must not have the value type constraint.</span></span> <span data-ttu-id="143b6-265">이 고, 그렇지 `T` 는 효과적으로 봉인 되어 있으므로 `S` 를 동일한 형식 이어야 `T`, 두 형식 매개 변수에 대 한 필요성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-265">Otherwise, `T` is effectively sealed so `S` would be forced to be the same type as `T`, eliminating the need for two type parameters.</span></span>
*  <span data-ttu-id="143b6-266">경우 `S` 에 다음 값 형식 제약 조건이 `T` 없어야를 *class_type* 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-266">If `S` has the value type constraint then `T` must not have a *class_type* constraint.</span></span>
*  <span data-ttu-id="143b6-267">하는 경우 `S` 에 *class_type* 제약 조건 `A` 및 `T` 에 *class_type* 제약 조건 `B` id 변환이 있어야 암시적 또는 참조에서 변환 `A` 하 `B` 또는에서 암시적 참조 변환이 `B` 에 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-267">If `S` has a *class_type* constraint `A` and `T` has a *class_type* constraint `B` then there must be an identity conversion or implicit reference conversion from `A` to `B` or an implicit reference conversion from `B` to `A`.</span></span>
*  <span data-ttu-id="143b6-268">하는 경우 `S` 형식 매개 변수에 따라 달라 집니다 `U` 및 `U` 에 *class_type* 제약 조건 `A` 및 `T` 에 *class_type* 제약조건`B` 는 id 변환을 또는에서 암시적 참조 변환이 있어야 `A` 하 `B` 또는에서 암시적 참조 변환이 `B` 에 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-268">If `S` also depends on type parameter `U` and `U` has a *class_type* constraint `A` and `T` has a *class_type* constraint `B` then there must be an identity conversion or implicit reference conversion from `A` to `B` or an implicit reference conversion from `B` to `A`.</span></span>

<span data-ttu-id="143b6-269">에 대 한 유효 `S` 있어야 값 형식 제약 조건 및 `T` 참조 형식 제약 조건이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-269">It is valid for `S` to have the value type constraint and `T` to have the reference type constraint.</span></span> <span data-ttu-id="143b6-270">이 제한 하는 효과적으로 `T` 형식으로 `System.Object`, `System.ValueType`, `System.Enum`, 및 임의의 인터페이스 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-270">Effectively this limits `T` to the types `System.Object`, `System.ValueType`, `System.Enum`, and any interface type.</span></span>

<span data-ttu-id="143b6-271">경우는 `where` 절 형식 매개 변수에 생성자 제약 조건이 포함 되어 있습니다 (폼에 있는 `new()`)를 사용 하는 것이 가능를 `new` 형식의 인스턴스를 만들려면 연산자 ([개체 만들기 식](expressions.md#object-creation-expressions)).</span><span class="sxs-lookup"><span data-stu-id="143b6-271">If the `where` clause for a type parameter includes a constructor constraint (which has the form `new()`), it is possible to use the `new` operator to create instances of the type ([Object creation expressions](expressions.md#object-creation-expressions)).</span></span> <span data-ttu-id="143b6-272">모든 형식이 사용 되는 인수 또는 값 형식 제약 조건 또는 생성자 제약 조건 (참조 형식 매개 변수로 생성자 제약 조건이 있는 형식 매개 변수 (이 생성자 암시적으로 있는 모든 값 형식에 대 한) 매개 변수가 없는 public 생성자가 있어야 합니다 [형식 매개 변수 제약 조건](classes.md#type-parameter-constraints) 세부 정보에 대 한).</span><span class="sxs-lookup"><span data-stu-id="143b6-272">Any type argument used for a type parameter with a constructor constraint must have a public parameterless constructor (this constructor implicitly exists for any value type) or be a type parameter having the value type constraint or constructor constraint (see [Type parameter constraints](classes.md#type-parameter-constraints) for details).</span></span>

<span data-ttu-id="143b6-273">다음은 제약 조건의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-273">The following are examples of constraints:</span></span>
```csharp
interface IPrintable
{
    void Print();
}

interface IComparable<T>
{
    int CompareTo(T value);
}

interface IKeyProvider<T>
{
    T GetKey();
}

class Printer<T> where T: IPrintable {...}

class SortedList<T> where T: IComparable<T> {...}

class Dictionary<K,V>
    where K: IComparable<K>
    where V: IPrintable, IKeyProvider<K>, new()
{
    ...
}
```

<span data-ttu-id="143b6-274">다음 예제에서는 형식 매개 변수 종속성 그래프에는 순환이 발생 하기 때문에 오류가 있음:</span><span class="sxs-lookup"><span data-stu-id="143b6-274">The following example is in error because it causes a circularity in the dependency graph of the type parameters:</span></span>
```csharp
class Circular<S,T>
    where S: T
    where T: S                // Error, circularity in dependency graph
{
    ...
}
```

<span data-ttu-id="143b6-275">다음 예제에서는 추가 잘못 된 상황을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-275">The following examples illustrate additional invalid situations:</span></span>
```csharp
class Sealed<S,T>
    where S: T
    where T: struct        // Error, T is sealed
{
    ...
}

class A {...}

class B {...}

class Incompat<S,T>
    where S: A, T
    where T: B                // Error, incompatible class-type constraints
{
    ...
}

class StructWithClass<S,T,U>
    where S: struct, T
    where T: U
    where U: A                // Error, A incompatible with struct
{
    ...
}
```

<span data-ttu-id="143b6-276">합니다 ***유효한 기본 클래스*** 형식 매개 변수의 `T` 다음과 같이 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-276">The ***effective base class*** of a type parameter `T` is defined as follows:</span></span>

*  <span data-ttu-id="143b6-277">하는 경우 `T` 에 기본 제한이 아니거나 유효한 기본 클래스 형식 매개 변수 제약 조건이 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-277">If `T` has no primary constraints or type parameter constraints, its effective base class is `object`.</span></span>
*  <span data-ttu-id="143b6-278">하는 경우 `T` 값 형식 제약 조건이 유효한 기본 클래스는 `System.ValueType`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-278">If `T` has the value type constraint, its effective base class is `System.ValueType`.</span></span>
*  <span data-ttu-id="143b6-279">하는 경우 `T` 에 *class_type* 제약 조건 `C` 없는 *type_parameter* 제약 조건 적용 해당 기본 클래스는 `C`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-279">If `T` has a *class_type* constraint `C` but no *type_parameter* constraints, its effective base class is `C`.</span></span>
*  <span data-ttu-id="143b6-280">하는 경우 `T` 아무런 *class_type* 제약 조건 이지만 하나 이상의 *type_parameter* 유효한 기본 클래스 제약 조건 형식이 최하위 ([변환 리프트 연산자](conversions.md#lifted-conversion-operators))의 유효한 기본 클래스의 집합에 해당 *type_parameter* 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-280">If `T` has no *class_type* constraint but has one or more *type_parameter* constraints, its effective base class is the most encompassed type ([Lifted conversion operators](conversions.md#lifted-conversion-operators)) in the set of effective base classes of its *type_parameter* constraints.</span></span> <span data-ttu-id="143b6-281">일관성 규칙 이러한 최하위 형식이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-281">The consistency rules ensure that such a most encompassed type exists.</span></span>
*  <span data-ttu-id="143b6-282">경우 `T` 둘 다 포함 된 *class_type* 제약 조건 및 하나 이상의 *type_parameter* 유효한 기본 클래스 제약 조건 형식이 최하위 ([변환 리프트 연산자](conversions.md#lifted-conversion-operators))로 구성 된 집합에는 *class_type* 의 제약 조건을 `T` 의 유효 기본 클래스 및 해당 *type_parameter* 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-282">If `T` has both a *class_type* constraint and one or more *type_parameter* constraints, its effective base class is the most encompassed type ([Lifted conversion operators](conversions.md#lifted-conversion-operators)) in the set consisting of the *class_type* constraint of `T` and the effective base classes of its *type_parameter* constraints.</span></span> <span data-ttu-id="143b6-283">일관성 규칙 이러한 최하위 형식이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-283">The consistency rules ensure that such a most encompassed type exists.</span></span>
*  <span data-ttu-id="143b6-284">하는 경우 `T` 가 참조 형식 제약 조건 이지만 *class_type* 제약 조건 적용 해당 기본 클래스는 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-284">If `T` has the reference type constraint but no *class_type* constraints, its effective base class is `object`.</span></span>

<span data-ttu-id="143b6-285">T 제약 조건이 있으면 이러한 규칙을 위해 `V` 즉를 *value_type*의 가장 구체적인 기본 형식 대신 `V` 즉를 *class_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-285">For the purpose of these rules, if T has a constraint `V` that is a *value_type*, use instead the most specific base type of `V` that is a *class_type*.</span></span> <span data-ttu-id="143b6-286">이 절대를 명시적으로 지정 된 제약 조건에서 발생할 수 있지만 제네릭 메서드의 제약 조건을 재정의 메서드 선언 또는 인터페이스 메서드의 명시적 구현으로 암시적으로 상속 하는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-286">This can never happen in an explicitly given constraint, but may occur when the constraints of a generic method are implicitly inherited by an overriding method declaration or an explicit implementation of an interface method.</span></span>

<span data-ttu-id="143b6-287">이러한 규칙 확인 유효한 기본 클래스는 항상을 *class_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-287">These rules ensure that the effective base class is always a *class_type*.</span></span>

<span data-ttu-id="143b6-288">합니다 ***효과적인 인터페이스 집합*** 형식 매개 변수의 `T` 다음과 같이 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-288">The ***effective interface set*** of a type parameter `T` is defined as follows:</span></span>

*  <span data-ttu-id="143b6-289">하는 경우 `T` 가 없는 *secondary_constraints*, 해당 효과적인 인터페이스 집합이 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-289">If `T` has no *secondary_constraints*, its effective interface set is empty.</span></span>
*  <span data-ttu-id="143b6-290">경우 `T` 했습니다 *interface_type* 제약 조건 이지만 *type_parameter* 제약 조건과 해당 효과적인 인터페이스 집합은 해당 집합 *interface_type* 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-290">If `T` has *interface_type* constraints but no *type_parameter* constraints, its effective interface set is its set of *interface_type* constraints.</span></span>
*  <span data-ttu-id="143b6-291">하는 경우 `T` 가 없는 *interface_type* 제약 조건 않았으나 *type_parameter* 제약 조건과 해당 효과적인 인터페이스 집합이의 효과적인 인터페이스 집합의 합집합 해당 *형식 매개 변수* 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-291">If `T` has no *interface_type* constraints but has *type_parameter* constraints, its effective interface set is the union of the effective interface sets of its *type_parameter* constraints.</span></span>
*  <span data-ttu-id="143b6-292">하는 경우 `T` 가 모두 *interface_type* 제약 조건 및 *type_parameter* 제약 조건과 해당 효과적인 인터페이스 집합은 해당 집합의 합집합 *interface_type* 제약 조건 및 효과적인 인터페이스 집합을 해당 *type_parameter* 제약 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-292">If `T` has both *interface_type* constraints and *type_parameter* constraints, its effective interface set is the union of its set of *interface_type* constraints and the effective interface sets of its *type_parameter* constraints.</span></span>

<span data-ttu-id="143b6-293">형식 매개 변수 ***참조 형식으로 알려진*** 하는 경우 참조 형식 제약 조건에 없거나 유효한 기본 클래스인 `object` 또는 `System.ValueType`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-293">A type parameter is ***known to be a reference type*** if it has the reference type constraint or its effective base class is not `object` or `System.ValueType`.</span></span>

<span data-ttu-id="143b6-294">제한 된 형식 매개 변수 값 제약 조건 사용 권한에 포함 된 인스턴스 멤버에 액세스 하려면 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-294">Values of a constrained type parameter type can be used to access the instance members implied by the constraints.</span></span> <span data-ttu-id="143b6-295">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-295">In the example</span></span>
```csharp
interface IPrintable
{
    void Print();
}

class Printer<T> where T: IPrintable
{
    void PrintOne(T x) {
        x.Print();
    }
}
```
<span data-ttu-id="143b6-296">메서드 `IPrintable` 에서 직접 호출할 수 있습니다 `x` 있으므로 `T` 항상 구현 하도록 제한 됩니다 `IPrintable`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-296">the methods of `IPrintable` can be invoked directly on `x` because `T` is constrained to always implement `IPrintable`.</span></span>

### <a name="class-body"></a><span data-ttu-id="143b6-297">클래스 본문</span><span class="sxs-lookup"><span data-stu-id="143b6-297">Class body</span></span>

<span data-ttu-id="143b6-298">합니다 *class_body* 클래스의 해당 클래스의 멤버를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-298">The *class_body* of a class defines the members of that class.</span></span>

```antlr
class_body
    : '{' class_member_declaration* '}'
    ;
```

## <a name="partial-types"></a><span data-ttu-id="143b6-299">부분 형식</span><span class="sxs-lookup"><span data-stu-id="143b6-299">Partial types</span></span>

<span data-ttu-id="143b6-300">형식 선언을 여러 분할 될 수 있습니다 ***부분 형식 선언을***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-300">A type declaration can be split across multiple ***partial type declarations***.</span></span> <span data-ttu-id="143b6-301">형식 선언 프로그램의 컴파일 시간 및 런타임 처리의 나머지 부분 중 단일 선언으로 처리 됩니다 보내지고 해당 부분에서이 섹션에서는 규칙에 따라 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-301">The type declaration is constructed from its parts by following the rules in this section, whereupon it is treated as a single declaration during the remainder of the compile-time and run-time processing of the program.</span></span>

<span data-ttu-id="143b6-302">A *class_declaration*, *struct_declaration* 하거나 *interface_declaration* 포함 된 경우 부분 형식 선언을 나타냅니다는 `partial` 한정자.</span><span class="sxs-lookup"><span data-stu-id="143b6-302">A *class_declaration*, *struct_declaration* or *interface_declaration* represents a partial type declaration if it includes a `partial` modifier.</span></span> <span data-ttu-id="143b6-303">`partial` 키워드 아니며 바로 앞에 키워드 중 하나가 표시 되는 경우 해당 한정자로 역할만 `class`, `struct` 하거나 `interface` 형식 선언에서 또는 형식 앞 `void` 메서드 선언에서.</span><span class="sxs-lookup"><span data-stu-id="143b6-303">`partial` is not a keyword, and only acts as a modifier if it appears immediately before one of the keywords `class`, `struct` or `interface` in a type declaration, or before the type `void` in a method declaration.</span></span> <span data-ttu-id="143b6-304">다른 컨텍스트에서 일반 식별자로 사용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-304">In other contexts it can be used as a normal identifier.</span></span>

<span data-ttu-id="143b6-305">각 부분 부분 형식 선언 포함 해야 합니다는 `partial` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-305">Each part of a partial type declaration must include a `partial` modifier.</span></span> <span data-ttu-id="143b6-306">이름이 있어야 하 고 동일한 네임 스페이스 또는 다른 부분 형식 선언에서 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-306">It must have the same name  and be declared in the same namespace or type declaration as the other parts.</span></span> <span data-ttu-id="143b6-307">합니다 `partial` 한정자는 형식 선언의 추가 파트를 다른 곳에서 있을 수 있지만 이러한 추가 파트의 존재 여부 요구 사항은 아닙니다. 나타내고 포함할 단일 선언 된 형식에 대해 유효 합니다 `partial` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-307">The `partial` modifier indicates that additional parts of the type declaration may exist elsewhere, but the existence of such additional parts is not a requirement; it is valid for a type with a single declaration to include the `partial` modifier.</span></span>

<span data-ttu-id="143b6-308">파트에는 단일 형식 선언을 컴파일 타임에 병합할 수 있도록 부분 형식의 모든 부분을 함께 컴파일된 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-308">All parts of a partial type must be compiled together such that the parts can be merged at compile-time into a single type declaration.</span></span> <span data-ttu-id="143b6-309">부분 형식 확장 되도록 이미 컴파일된 형식을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-309">Partial types specifically do not allow already compiled types to be extended.</span></span>

<span data-ttu-id="143b6-310">중첩 된 형식을 사용 하 여 여러 부분에서 선언할 수 있습니다는 `partial` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-310">Nested types may be declared in multiple parts by using the `partial` modifier.</span></span> <span data-ttu-id="143b6-311">일반적으로 포함 하는 형식을 사용 하 여 선언 된 `partial` 하며 중첩 형식의 각 부분, 포함 하는 형식의 다른 부분에 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-311">Typically, the containing type is declared using `partial` as well, and each part of the nested type is declared in a different part of the containing type.</span></span>

<span data-ttu-id="143b6-312">`partial` 한정자 대리자 또는 열거형 선언에서 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-312">The `partial` modifier is not permitted on delegate or enum declarations.</span></span>

### <a name="attributes"></a><span data-ttu-id="143b6-313">특성</span><span class="sxs-lookup"><span data-stu-id="143b6-313">Attributes</span></span>

<span data-ttu-id="143b6-314">부분 형식의 특성은는 지정 되지 않은 순서에 따라 특성의 각 부분을 결합 하 여 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-314">The attributes of a partial type are determined by combining, in an unspecified order, the attributes of each of the parts.</span></span> <span data-ttu-id="143b6-315">특성은 여러 부분에 배치 되 면 형식에 특성을 여러 번 지정 하는 것이 같습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-315">If an attribute is placed on multiple parts, it is equivalent to specifying the attribute multiple times on the type.</span></span> <span data-ttu-id="143b6-316">예를 들어, 두 부분:</span><span class="sxs-lookup"><span data-stu-id="143b6-316">For example, the two parts:</span></span>

```csharp
[Attr1, Attr2("hello")]
partial class A {}

[Attr3, Attr2("goodbye")]
partial class A {}
```
<span data-ttu-id="143b6-317">동일 선언에 같은 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-317">are equivalent to a declaration such as:</span></span>
```csharp
[Attr1, Attr2("hello"), Attr3, Attr2("goodbye")]
class A {}
```

<span data-ttu-id="143b6-318">형식 매개 변수의 특성 비슷한 방식으로 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-318">Attributes on type parameters combine in a similar fashion.</span></span>

### <a name="modifiers"></a><span data-ttu-id="143b6-319">한정자</span><span class="sxs-lookup"><span data-stu-id="143b6-319">Modifiers</span></span>

<span data-ttu-id="143b6-320">부분 형식 선언을 내게 필요한 옵션 지정을 포함 하는 경우 (합니다 `public`, `protected`를 `internal`, 및 `private` 한정자) 내게 필요한 옵션 지정을 포함 하는 다른 모든 부분을 사용 하 여 동의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-320">When a partial type declaration includes an accessibility specification (the `public`, `protected`, `internal`, and `private` modifiers) it must agree with all other parts that include an accessibility specification.</span></span> <span data-ttu-id="143b6-321">형식을 적절 한 기본 액세스 가능성을 지정은 부분 형식 부분이 내게 필요한 옵션 사양에 포함 된 경우 ([접근성을 선언](basic-concepts.md#declared-accessibility)).</span><span class="sxs-lookup"><span data-stu-id="143b6-321">If no part of a partial type includes an accessibility specification, the type is given the appropriate default accessibility ([Declared accessibility](basic-concepts.md#declared-accessibility)).</span></span>

<span data-ttu-id="143b6-322">중첩 된 형식의 부분 선언을 하나 이상 포함 하는 경우는 `new` 한정자를 중첩 된 형식 상속된 된 멤버를 숨깁니다 하는 경우 경고 없이 보고 됩니다 ([상속을 통해 숨기기](basic-concepts.md#hiding-through-inheritance)).</span><span class="sxs-lookup"><span data-stu-id="143b6-322">If one or more partial declarations of a nested type include a `new` modifier, no warning is reported if the nested type hides an inherited member ([Hiding through inheritance](basic-concepts.md#hiding-through-inheritance)).</span></span>

<span data-ttu-id="143b6-323">클래스의 partial 선언을 하나 이상 포함 하는 경우는 `abstract` 한정자가 클래스를 abstract로 간주 됩니다 ([추상 클래스](classes.md#abstract-classes)).</span><span class="sxs-lookup"><span data-stu-id="143b6-323">If one or more partial declarations of a class include an `abstract` modifier, the class is considered abstract ([Abstract classes](classes.md#abstract-classes)).</span></span> <span data-ttu-id="143b6-324">그렇지 않은 경우 클래스는 추상이 아닌 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-324">Otherwise, the class is considered non-abstract.</span></span>

<span data-ttu-id="143b6-325">클래스의 partial 선언을 하나 이상 포함 하는 경우는 `sealed` 한정자를 클래스는 sealed로 간주 됩니다 ([클래스를 봉인](classes.md#sealed-classes)).</span><span class="sxs-lookup"><span data-stu-id="143b6-325">If one or more partial declarations of a class include a `sealed` modifier, the class is considered sealed ([Sealed classes](classes.md#sealed-classes)).</span></span> <span data-ttu-id="143b6-326">그렇지 않으면 클래스에는 것으로 간주 됩니다 봉인 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-326">Otherwise, the class is considered unsealed.</span></span>

<span data-ttu-id="143b6-327">클래스는 abstract 이면 서 sealed 일 수 없습니다는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-327">Note that a class cannot be both abstract and sealed.</span></span>

<span data-ttu-id="143b6-328">경우는 `unsafe` 한정자는 해당 특정 부분에는 안전 하지 않은 컨텍스트 것으로 간주 됩니다만 부분 형식 선언에 사용 됩니다 ([안전 하지 않은 컨텍스트](unsafe-code.md#unsafe-contexts)).</span><span class="sxs-lookup"><span data-stu-id="143b6-328">When the `unsafe` modifier is used on a partial type declaration, only that particular part is considered an unsafe context ([Unsafe contexts](unsafe-code.md#unsafe-contexts)).</span></span>

### <a name="type-parameters-and-constraints"></a><span data-ttu-id="143b6-329">형식 매개 변수 및 제약 조건</span><span class="sxs-lookup"><span data-stu-id="143b6-329">Type parameters and constraints</span></span>

<span data-ttu-id="143b6-330">제네릭 형식의 여러 파트에서 선언 된 경우 각 파트 형식 매개 변수를 명시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-330">If a generic type is declared in multiple parts, each part must state the type parameters.</span></span> <span data-ttu-id="143b6-331">각 파트 순서 대로 각 형식 매개 변수에 대해 동일한 이름과 동일한 형식 매개 변수 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-331">Each part must have the same number of type parameters, and the same name for each type parameter, in order.</span></span>

<span data-ttu-id="143b6-332">부분 제네릭 형식 선언의 제약 조건을 포함 하는 경우 (`where` 절), 제약 조건을 제약 조건을 포함 하는 다른 모든 부분에 동의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-332">When a partial generic type declaration includes constraints (`where` clauses), the constraints must agree with all other parts that include constraints.</span></span> <span data-ttu-id="143b6-333">구체적으로 제약 조건을 포함 하는 각 파트에는 동일한 형식 매개 변수 집합에 대 한 제약 조건이 있어야 합니다. 및 각 형식 매개 변수 집합을 기본 보조 및 생성자 제약 조건 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-333">Specifically, each part that includes constraints must have constraints for the same set of type parameters, and for each type parameter the sets of primary, secondary, and constructor constraints must be equivalent.</span></span> <span data-ttu-id="143b6-334">동일한 멤버를 포함 하는 경우 두 가지 제약 조건이 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-334">Two sets of constraints are equivalent if they contain the same members.</span></span> <span data-ttu-id="143b6-335">형식 매개 변수 제약 조건이 제한 되지 않은 매개 변수를 사용 하는 것으로 간주 형식을 지정 하는 부분이 부분 제네릭 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-335">If no part of a partial generic type specifies type parameter constraints, the type parameters are considered unconstrained.</span></span>

<span data-ttu-id="143b6-336">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-336">The example</span></span>
```csharp
partial class Dictionary<K,V>
    where K: IComparable<K>
    where V: IKeyProvider<K>, IPersistable
{
    ...
}

partial class Dictionary<K,V>
    where V: IPersistable, IKeyProvider<K>
    where K: IComparable<K>
{
    ...
}

partial class Dictionary<K,V>
{
    ...
}
```
<span data-ttu-id="143b6-337">올바른 제약 조건 (처음 두 개)를 효과적으로 포함 하는 부분만 지정 같은 보조의 기본 설정 및 동일한 형식 매개 변수 집합에 대 한 생성자 제약 조건 때문에 각각입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-337">is correct because those parts that include constraints (the first two) effectively specify the same set of primary, secondary, and constructor constraints for the same set of type parameters, respectively.</span></span>

### <a name="base-class"></a><span data-ttu-id="143b6-338">기본 클래스</span><span class="sxs-lookup"><span data-stu-id="143b6-338">Base class</span></span>

<span data-ttu-id="143b6-339">Partial 클래스 선언 기본 클래스 지정을 포함 하는 경우에 기본 클래스 지정을 포함 하는 다른 모든 부분을 사용 하 여 동의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-339">When a partial class declaration includes a base class specification it must agree with all other parts that include a base class specification.</span></span> <span data-ttu-id="143b6-340">Partial 클래스의 기본 클래스 지정을 포함 하는 경우 기본 클래스 됩니다 `System.Object` ([기본 클래스](classes.md#base-classes)).</span><span class="sxs-lookup"><span data-stu-id="143b6-340">If no part of a partial class includes a base class specification, the base class becomes `System.Object` ([Base classes](classes.md#base-classes)).</span></span>

### <a name="base-interfaces"></a><span data-ttu-id="143b6-341">기본 인터페이스</span><span class="sxs-lookup"><span data-stu-id="143b6-341">Base interfaces</span></span>

<span data-ttu-id="143b6-342">여러 부분으로 선언 된 형식에 대 한 기본 인터페이스 집합이 각 부분에 지정 된 기본 인터페이스의 합집합입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-342">The set of base interfaces for a type declared in multiple parts is the union of the base interfaces specified on each part.</span></span> <span data-ttu-id="143b6-343">각 부분에서 특정 기본 인터페이스를 한 번 이름은 될 수 있습니다 하지만 동일한 기본 인터페이스 이름을 여러 부분에 대 한 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-343">A particular base interface may only be named once on each part, but it is permitted for multiple parts to name the same base interface(s).</span></span> <span data-ttu-id="143b6-344">지정 된 모든 기본 인터페이스 멤버의 하나의 구현만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-344">There must only be one implementation of the members of any given base interface.</span></span>

<span data-ttu-id="143b6-345">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-345">In the example</span></span>
```csharp
partial class C: IA, IB {...}

partial class C: IC {...}

partial class C: IA, IB {...}
```
<span data-ttu-id="143b6-346">클래스에 대 한 기본 인터페이스 집합이 `C` 됩니다 `IA`를 `IB`, 및 `IC`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-346">the set of base interfaces for class `C` is `IA`, `IB`, and `IC`.</span></span>

<span data-ttu-id="143b6-347">각 부분에 해당 파트에 선언 된 인터페이스의 구현을 제공 하는 일반적으로 그러나이 요구 사항은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-347">Typically, each part provides an implementation of the interface(s) declared on that part; however, this is not a requirement.</span></span> <span data-ttu-id="143b6-348">일부 다른 부분에 선언 된 인터페이스의 구현을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-348">A part may provide the implementation for an interface declared on a different part:</span></span>
```csharp
partial class X
{
    int IComparable.CompareTo(object o) {...}
}

partial class X: IComparable
{
    ...
}
```

### <a name="members"></a><span data-ttu-id="143b6-349">멤버</span><span class="sxs-lookup"><span data-stu-id="143b6-349">Members</span></span>

<span data-ttu-id="143b6-350">부분 메서드를 제외 하 고 ([부분 메서드](classes.md#partial-methods)), 여러 부분에 선언 된 형식의 멤버 집합이 각 부분에 선언 된 멤버 집합의 합집합 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-350">With the exception of partial methods ([Partial methods](classes.md#partial-methods)), the set of members of a type declared in multiple parts is simply the union of the set of members declared in each part.</span></span> <span data-ttu-id="143b6-351">동일한 선언 공간을 공유 하는 형식 선언의 모든 부분의 본문 ([선언](basic-concepts.md#declarations)), 및 각 멤버의 범위 ([범위](basic-concepts.md#scopes)) 모든 부분의 본문을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-351">The bodies of all parts of the type declaration share the same declaration space ([Declarations](basic-concepts.md#declarations)), and the scope of each member ([Scopes](basic-concepts.md#scopes)) extends to the bodies of all the parts.</span></span> <span data-ttu-id="143b6-352">모든 멤버의 액세스 가능 도메인은 항상; 바깥쪽 형식의 모든 부분을 포함 `private` 한 부분에 선언 된 멤버는 다른 부분에서 자유롭게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-352">The accessibility domain of any member always includes all the parts of the enclosing type; a `private` member declared in one part is freely accessible from another part.</span></span> <span data-ttu-id="143b6-353">해당 멤버 형식 아닌 형식의 둘 이상의 파트가 동일한 멤버를 선언 하는 컴파일 시간 오류는 것은 `partial` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-353">It is a compile-time error to declare the same member in more than one part of the type, unless that member is a type with the `partial` modifier.</span></span>

```csharp
partial class A
{
    int x;                     // Error, cannot declare x more than once

    partial class Inner        // Ok, Inner is a partial type
    {
        int y;
    }
}

partial class A
{
    int x;                     // Error, cannot declare x more than once

    partial class Inner        // Ok, Inner is a partial type
    {
        int z;
    }
}
```

<span data-ttu-id="143b6-354">형식 내 멤버의 순서를 C# 코드를 거의 상당 하지만 다른 언어 및 환경와 상호 작용 하는 경우 상당히 높을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-354">The ordering of members within a type is rarely significant to C# code, but may be significant when interfacing with other languages and environments.</span></span> <span data-ttu-id="143b6-355">이러한 경우 여러 부분에 선언 된 형식 내 멤버의 순서가 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-355">In these cases, the ordering of members within a type declared in multiple parts is undefined.</span></span>

### <a name="partial-methods"></a><span data-ttu-id="143b6-356">부분 메서드</span><span class="sxs-lookup"><span data-stu-id="143b6-356">Partial methods</span></span>

<span data-ttu-id="143b6-357">부분 메서드 형식 선언의 한 부분에서 정의 하 고 다른 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-357">Partial methods can be defined in one part of a type declaration and implemented in another.</span></span> <span data-ttu-id="143b6-358">구현은 선택 사항입니다. 부분 메서드를 구현 하는 부분이 없으면 partial 메서드 선언 및 모든 호출에 파트의 조합을 통해 결과 형식 선언에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-358">The implementation is optional; if no part implements the partial method, the partial method declaration and all calls to it are removed from the type declaration resulting from the combination of the parts.</span></span>

<span data-ttu-id="143b6-359">부분 메서드 액세스 한정자를 정의할 수 없습니다. 하지만 암시적으로 `private`입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-359">Partial methods cannot define access modifiers, but are implicitly `private`.</span></span> <span data-ttu-id="143b6-360">반환 형식 이어야 합니다 `void`, 해당 매개 변수에 사용할 수 없습니다는 `out` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-360">Their return type must be `void`, and their parameters cannot have the `out` modifier.</span></span> <span data-ttu-id="143b6-361">식별자 `partial` 직전 표시 되는 경우에 메서드 선언에서 특별 한 키워드로 인식 되는 `void` 입력, 그렇지 않으면 일반 식별자로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-361">The identifier `partial` is recognized as a special keyword in a method declaration only if it appears right before the `void` type; otherwise it can be used as a normal identifier.</span></span> <span data-ttu-id="143b6-362">부분 메서드 인터페이스 메서드를 명시적으로 구현할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-362">A partial method cannot explicitly implement interface methods.</span></span>

<span data-ttu-id="143b6-363">(Partial method) 선언의 두 가지가: 선언을 라고 메서드 선언의 본문 세미콜론 인 경우는 ***partial 메서드 선언 정의***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-363">There are two kinds of partial method declarations: If the body of the method declaration is a semicolon, the declaration is said to be a ***defining partial method declaration***.</span></span> <span data-ttu-id="143b6-364">본문으로 지정 하는 경우는 *블록*를 선언 이라고는 ***partial 메서드 선언 구현***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-364">If the body is given as a *block*, the declaration is said to be an ***implementing partial method declaration***.</span></span> <span data-ttu-id="143b6-365">형식 선언의 파트에서 사용할 수 있습니다만 지정 된 서명 사용 하 여 partial 메서드 선언에 정의 및 지정 된 서명 사용 하 여 partial 메서드 선언 구현 하나만 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-365">Across the parts of a type declaration there can be only one defining partial method declaration with a given signature, and there can be only one implementing partial method declaration with a given signature.</span></span> <span data-ttu-id="143b6-366">다음에 지정 된 구현 partial 메서드 선언이 지정 하는, 해당 partial 메서드 선언에 정의 존재 해야 하며 선언으로 일치 해야 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="143b6-366">If an implementing partial method declaration is given, a corresponding defining partial method declaration must exist, and the declarations must match as specified in the following:</span></span>

* <span data-ttu-id="143b6-367">선언 (하지만 반드시 동일한 순서로)는 같은 한정자가 있어야 합니다, 메서드 이름, 형식 매개 변수의 수 및 매개 변수 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-367">The declarations must have the same modifiers (although not necessarily in the same order), method name, number of type parameters and number of parameters.</span></span>
* <span data-ttu-id="143b6-368">해당 매개 변수 선언에는 (하지만 반드시 동일한 순서로)는 같은 한정자 있어야 형식과 동일한 형식 매개 변수 이름과 차이점) (모듈로.</span><span class="sxs-lookup"><span data-stu-id="143b6-368">Corresponding parameters in the declarations must have the same modifiers (although not necessarily in the same order) and the same types (modulo differences in type parameter names).</span></span>
* <span data-ttu-id="143b6-369">해당 형식 매개 변수 선언에서 동일한 제약 조건 (형식 매개 변수 이름과 차이점) 모듈로 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-369">Corresponding type parameters in the declarations must have the same constraints (modulo differences in type parameter names).</span></span>

<span data-ttu-id="143b6-370">구현 partial 메서드 선언이 해당 정의 partial 메서드 선언으로 동일한 부분에 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-370">An implementing partial method declaration can appear in the same part as the corresponding defining partial method declaration.</span></span>

<span data-ttu-id="143b6-371">부분 메서드 정의 오버 로드 확인에 참여합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-371">Only a defining partial method participates in overload resolution.</span></span> <span data-ttu-id="143b6-372">따라서 여부는 구현 선언이 지정 되 면 호출 식 부분 메서드 호출을 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-372">Thus, whether or not an implementing declaration is given, invocation expressions may resolve to invocations of the partial method.</span></span> <span data-ttu-id="143b6-373">부분 메서드는 항상 반환 하므로 `void`, 이러한 호출 식에서 식 문은 항상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-373">Because a partial method always returns `void`, such invocation expressions will always be expression statements.</span></span> <span data-ttu-id="143b6-374">또한 부분 메서드를 암시적으로 이므로 `private`, 이러한 문의 부분 메서드는 선언 된 형식 선언 부분 중 하나에서 항상 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-374">Furthermore, because a partial method is implicitly `private`, such statements will always occur within one of the parts of the type declaration within which the partial method is declared.</span></span>

<span data-ttu-id="143b6-375">부분 형식 선언 부분이 지정된 부분 메서드에 대 한 구현 선언이 있으면 호출 하는 모든 식 문은 단순히 결합 된 형식 선언에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-375">If no part of a partial type declaration contains an implementing declaration for a given partial method, any expression statement invoking it is simply removed from the combined type declaration.</span></span> <span data-ttu-id="143b6-376">따라서 호출 식에 모든 구성 요소 식을 포함 하 여 런타임 시 효과가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-376">Thus the invocation expression, including any constituent expressions, has no effect at run-time.</span></span> <span data-ttu-id="143b6-377">부분 메서드 자체 제거도 되 고 결합 된 형식 선언에 소속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-377">The partial method itself is also removed and will not be a member of the combined type declaration.</span></span>

<span data-ttu-id="143b6-378">지정 된 부분 메서드의 구현 선언이 없으면 부분 메서드의 호출 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-378">If an implementing declaration exist for a given partial method, the invocations of the partial methods are retained.</span></span> <span data-ttu-id="143b6-379">부분 메서드는 다음을 제외한 구현 partial 메서드 선언 비슷합니다 메서드 선언에 증가 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-379">The partial method gives rise to a method declaration similar to the implementing partial method declaration except for the following:</span></span>

* <span data-ttu-id="143b6-380">`partial` 한정자 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-380">The `partial` modifier is not included</span></span>
* <span data-ttu-id="143b6-381">결과 메서드 선언에서 특성은 지정 되지 않은 순서로 정의 및 구현 partial 메서드 선언 결합 된 특성.</span><span class="sxs-lookup"><span data-stu-id="143b6-381">The attributes in the resulting method declaration are the combined attributes of the defining and the implementing partial method declaration in unspecified order.</span></span> <span data-ttu-id="143b6-382">중복 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-382">Duplicates are not removed.</span></span>
* <span data-ttu-id="143b6-383">결과 메서드 선언의 매개 변수에 대 한 특성은 지정 되지 않은 순서로 정의 및 구현 partial 메서드 선언 매개 변수를 해당의 결합 된 특성.</span><span class="sxs-lookup"><span data-stu-id="143b6-383">The attributes on the parameters of the resulting method declaration are the combined attributes of the corresponding parameters of the defining and the implementing partial method declaration in unspecified order.</span></span> <span data-ttu-id="143b6-384">중복 제거 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-384">Duplicates are not removed.</span></span>

<span data-ttu-id="143b6-385">부분 메서드 M에 대 한 정의 선언이 있지만 구현 선언이 없습니다 주어진 경우에 다음과 같은 제한 사항이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-385">If a defining declaration but not an implementing declaration is given for a partial method M, the following restrictions apply:</span></span>

* <span data-ttu-id="143b6-386">메서드에 대리자를 만드는 컴파일 타임 오류 ([대리자 생성 식](expressions.md#delegate-creation-expressions)).</span><span class="sxs-lookup"><span data-stu-id="143b6-386">It is a compile-time error to create a delegate to method ([Delegate creation expressions](expressions.md#delegate-creation-expressions)).</span></span>
* <span data-ttu-id="143b6-387">컴파일 타임 오류를 가리키도록 `M` 식 트리 형식으로 변환 되는 익명 함수 내에서 ([익명 함수 식 트리 형식으로의 변환의 평가](conversions.md#evaluation-of-anonymous-function-conversions-to-expression-tree-types)).</span><span class="sxs-lookup"><span data-stu-id="143b6-387">It is a compile-time error to refer to `M` inside an anonymous function that is converted to an expression tree type ([Evaluation of anonymous function conversions to expression tree types](conversions.md#evaluation-of-anonymous-function-conversions-to-expression-tree-types)).</span></span>
* <span data-ttu-id="143b6-388">호출의 일부로 발생 하는 식 `M` 한정 된 할당 상태에 영향을 주지 않습니다 ([한정 된 할당](variables.md#definite-assignment)), 잠재적으로 컴파일 시간 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-388">Expressions occurring as part of an invocation of `M` do not affect the definite assignment state ([Definite assignment](variables.md#definite-assignment)), which can potentially lead to compile-time errors.</span></span>
* <span data-ttu-id="143b6-389">`M` 응용 프로그램에 대 한 진입점이 될 수 없습니다 ([응용 프로그램 시작](basic-concepts.md#application-startup)).</span><span class="sxs-lookup"><span data-stu-id="143b6-389">`M` cannot be the entry point for an application ([Application Startup](basic-concepts.md#application-startup)).</span></span>

<span data-ttu-id="143b6-390">부분 메서드는 도구에 의해 생성 되는 예를 들어 하나는 다른 파트의 동작을 사용자 지정 형식 선언의 한 부분을 허용 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-390">Partial methods are useful for allowing one part of a type declaration to customize the behavior of another part, e.g., one that is generated by a tool.</span></span> <span data-ttu-id="143b6-391">다음 partial 클래스 선언을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="143b6-391">Consider the following partial class declaration:</span></span>
```csharp
partial class Customer
{
    string name;

    public string Name {
        get { return name; }
        set {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }

    }

    partial void OnNameChanging(string newName);

    partial void OnNameChanged();
}
```

<span data-ttu-id="143b6-392">이 클래스는 다른 부분 없이 컴파일 정의 partial 메서드 선언 및 해당 호출은 제거할 수 있으며, 결과 결합된 클래스 선언 다음에 해당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-392">If this class is compiled without any other parts, the defining partial method declarations and their invocations will be removed, and the resulting combined class declaration will be equivalent to the following:</span></span>
```csharp
class Customer
{
    string name;

    public string Name {
        get { return name; }
        set { name = value; }
    }
}
```

<span data-ttu-id="143b6-393">하지만 다른 부분을 지정 부분 메서드의 구현 선언만 제공 하는 것으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-393">Assume that another part is given, however, which provides implementing declarations of the partial methods:</span></span>
```csharp
partial class Customer
{
    partial void OnNameChanging(string newName)
    {
        Console.WriteLine("Changing " + name + " to " + newName);
    }

    partial void OnNameChanged()
    {
        Console.WriteLine("Changed to " + name);
    }
}
```

<span data-ttu-id="143b6-394">그런 다음 결과 결합된 클래스 선언 다음에 해당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-394">Then the resulting combined class declaration will be equivalent to the following:</span></span>
```csharp
class Customer
{
    string name;

    public string Name {
        get { return name; }
        set {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }

    }

    void OnNameChanging(string newName)
    {
        Console.WriteLine("Changing " + name + " to " + newName);
    }

    void OnNameChanged()
    {
        Console.WriteLine("Changed to " + name);
    }
}
```

### <a name="name-binding"></a><span data-ttu-id="143b6-395">이름 바인딩</span><span class="sxs-lookup"><span data-stu-id="143b6-395">Name binding</span></span>

<span data-ttu-id="143b6-396">하지만 동일한 네임 스페이스 안에서 선언 되어야 확장할 수 있는 형식의 각 부분을 파트를 다른 네임 스페이스 선언 내에서 일반적으로 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-396">Although each part of an extensible type must be declared within the same namespace, the parts are typically written within different namespace declarations.</span></span> <span data-ttu-id="143b6-397">따라서 다른 `using` 지시문 ([지시문을 사용 하 여](namespaces.md#using-directives)) 각 부분에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-397">Thus, different `using` directives ([Using directives](namespaces.md#using-directives)) may be present for each part.</span></span> <span data-ttu-id="143b6-398">단순 이름을 해석 하는 경우 ([형식 유추](expressions.md#type-inference))만 하나의 파트 내에서 `using` 지시문의 해당 파트를 바깥쪽 네임 스페이스 선언으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-398">When interpreting simple names ([Type inference](expressions.md#type-inference)) within one part, only the `using` directives of the namespace declaration(s) enclosing that part are considered.</span></span> <span data-ttu-id="143b6-399">이 서로 다른 부분에 다른 의미를 포함 하는 동일한 식별자에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-399">This may result in the same identifier having different meanings in different parts:</span></span>
```csharp
namespace N
{
    using List = System.Collections.ArrayList;

    partial class A
    {
        List x;                // x has type System.Collections.ArrayList
    }
}

namespace N
{
    using List = Widgets.LinkedList;

    partial class A
    {
        List y;                // y has type Widgets.LinkedList
    }
}
```

## <a name="class-members"></a><span data-ttu-id="143b6-400">클래스 멤버</span><span class="sxs-lookup"><span data-stu-id="143b6-400">Class members</span></span>

<span data-ttu-id="143b6-401">클래스의 멤버 구성에서 도입 된 멤버의 해당 *class_member_declaration*s 및 멤버는 직접 기본 클래스에서 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-401">The members of a class consist of the members introduced by its *class_member_declaration*s and the members inherited from the direct base class.</span></span>

```antlr
class_member_declaration
    : constant_declaration
    | field_declaration
    | method_declaration
    | property_declaration
    | event_declaration
    | indexer_declaration
    | operator_declaration
    | constructor_declaration
    | destructor_declaration
    | static_constructor_declaration
    | type_declaration
    ;
```

<span data-ttu-id="143b6-402">클래스 형식의 멤버는 다음 범주로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-402">The members of a class type are divided into the following categories:</span></span>

*  <span data-ttu-id="143b6-403">클래스와 연결 된 상수 값을 나타내는 상수 ([상수](classes.md#constants)).</span><span class="sxs-lookup"><span data-stu-id="143b6-403">Constants, which represent constant values associated with the class ([Constants](classes.md#constants)).</span></span>
*  <span data-ttu-id="143b6-404">클래스의 변수는 필드 ([필드](classes.md#fields)).</span><span class="sxs-lookup"><span data-stu-id="143b6-404">Fields, which are the variables of the class ([Fields](classes.md#fields)).</span></span>
*  <span data-ttu-id="143b6-405">계산 및 클래스로 수행할 수 있는 작업을 구현 하는 메서드 ([메서드](classes.md#methods)).</span><span class="sxs-lookup"><span data-stu-id="143b6-405">Methods, which implement the computations and actions that can be performed by the class ([Methods](classes.md#methods)).</span></span>
*  <span data-ttu-id="143b6-406">속성을 정의 하는 특성 이름이 및 읽기 및 쓰기 이러한 특징을 연관 된 작업 ([속성](classes.md#properties)).</span><span class="sxs-lookup"><span data-stu-id="143b6-406">Properties, which define named characteristics and the actions associated with reading and writing those characteristics ([Properties](classes.md#properties)).</span></span>
*  <span data-ttu-id="143b6-407">클래스에 의해 생성 될 수 있는 알림을 정의 하는 이벤트 ([이벤트](classes.md#events)).</span><span class="sxs-lookup"><span data-stu-id="143b6-407">Events, which define notifications that can be generated by the class ([Events](classes.md#events)).</span></span>
*  <span data-ttu-id="143b6-408">인덱서를 동일한 방식으로 허용 되는 인덱싱 클래스의 인스턴스를 허용 하는 배열로 (구문상) ([인덱서](classes.md#indexers)).</span><span class="sxs-lookup"><span data-stu-id="143b6-408">Indexers, which permit instances of the class to be indexed in the same way (syntactically) as arrays ([Indexers](classes.md#indexers)).</span></span>
*  <span data-ttu-id="143b6-409">클래스의 인스턴스를 적용할 수 있는 식 연산자를 정의 하는 연산자 ([연산자](classes.md#operators)).</span><span class="sxs-lookup"><span data-stu-id="143b6-409">Operators, which define the expression operators that can be applied to instances of the class ([Operators](classes.md#operators)).</span></span>
*  <span data-ttu-id="143b6-410">인스턴스 클래스의 인스턴스를 초기화 하는 데 필요한 작업을 구현 하는 생성자 ([인스턴스 생성자](classes.md#instance-constructors))</span><span class="sxs-lookup"><span data-stu-id="143b6-410">Instance constructors, which implement the actions required to initialize instances of the class ([Instance constructors](classes.md#instance-constructors))</span></span>
*  <span data-ttu-id="143b6-411">소멸자는 클래스의 인스턴스를 영구적으로 삭제 되기 전에 수행할 작업을 구현 하는 ([소멸자](classes.md#destructors)).</span><span class="sxs-lookup"><span data-stu-id="143b6-411">Destructors, which implement the actions to be performed before instances of the class are permanently discarded ([Destructors](classes.md#destructors)).</span></span>
*  <span data-ttu-id="143b6-412">자체 클래스를 초기화 하는 데 필요한 작업을 구현 하는 정적 생성자 ([정적 생성자](classes.md#static-constructors)).</span><span class="sxs-lookup"><span data-stu-id="143b6-412">Static constructors, which implement the actions required to initialize the class itself ([Static constructors](classes.md#static-constructors)).</span></span>
*  <span data-ttu-id="143b6-413">로컬 클래스에 있는 형식을 나타내는 형식 ([중첩 형식은](classes.md#nested-types)).</span><span class="sxs-lookup"><span data-stu-id="143b6-413">Types, which represent the types that are local to the class ([Nested types](classes.md#nested-types)).</span></span>

<span data-ttu-id="143b6-414">실행 코드를 포함할 수 있는 멤버 라고 통칭 합니다 *멤버 함수* 클래스 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-414">Members that can contain executable code are collectively known as the *function members* of the class type.</span></span> <span data-ttu-id="143b6-415">클래스 형식의 함수 멤버는 메서드, 속성, 이벤트, 인덱서, 연산자, 인스턴스 생성자, 소멸자 및 해당 클래스 형식의 정적 생성자는 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-415">The function members of a class type are the methods, properties, events, indexers, operators, instance constructors,  destructors, and static constructors of that class type.</span></span>

<span data-ttu-id="143b6-416">A *class_declaration* 새 선언 공간을 만듭니다 ([선언](basic-concepts.md#declarations)), 및 *class_member_declaration*포함 된 즉시 s는 *클래스 _declaration* 이 선언 공간에 새 멤버를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-416">A *class_declaration* creates a new declaration space ([Declarations](basic-concepts.md#declarations)), and the *class_member_declaration*s immediately contained by the *class_declaration* introduce new members into this declaration space.</span></span> <span data-ttu-id="143b6-417">다음 규칙이 적용 됩니다 *class_member_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="143b6-417">The following rules apply to *class_member_declaration*s:</span></span>

*  <span data-ttu-id="143b6-418">인스턴스 생성자, 소멸자 및 정적 생성자에는 바로 바깥쪽 클래스 이름이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-418">Instance constructors, destructors and static constructors must have the same name as the immediately enclosing class.</span></span> <span data-ttu-id="143b6-419">다른 모든 멤버에는 가장 가까운 바깥쪽 클래스의 이름에서 다른 이름이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-419">All other members must have names that differ from the name of the immediately enclosing class.</span></span>
*  <span data-ttu-id="143b6-420">상수, 필드, 속성, 이벤트 또는 형식 이름의 동일한 클래스에서 선언 된 다른 모든 멤버의 이름과에서 달라 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-420">The name of a constant, field, property, event, or type must differ from the names of all other members declared in the same class.</span></span>
*  <span data-ttu-id="143b6-421">메서드의 이름을 메서드 이름에 다른 모든 비-동일한 클래스에서 선언에서 달라 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-421">The name of a method must differ from the names of all other non-methods declared in the same class.</span></span> <span data-ttu-id="143b6-422">또한 서명 ([시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading))의 메서드는 같은 클래스에 선언 된 다른 모든 메서드의 시그니처와 달라 야 하 고 동일한 클래스에서 선언 하는 두 가지 방법만 다른 서명이 없을 수 있습니다 하 여 `ref` 고 `out`입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-422">In addition, the signature ([Signatures and overloading](basic-concepts.md#signatures-and-overloading)) of a method must differ from the signatures of all other methods declared in the same class, and two methods declared in the same class may not have signatures that differ solely by `ref` and `out`.</span></span>
*  <span data-ttu-id="143b6-423">인스턴스 생성자의 시그니처는 동일한 클래스에서 선언 된 다른 모든 인스턴스 생성자의 시그니처와에서 달라 야 하 고 동일한 클래스에서 선언 하는 두 명의 생성자에 의해만 다른 서명이 없을 `ref` 고 `out`입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-423">The signature of an instance constructor must differ from the signatures of all other instance constructors declared in the same class, and two constructors declared in the same class may not have signatures that differ solely by `ref` and `out`.</span></span>
*  <span data-ttu-id="143b6-424">인덱서의 시그니처는 동일한 클래스에서 선언 된 다른 모든 인덱서의 시그니처와 달라 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-424">The signature of an indexer must differ from the signatures of all other indexers declared in the same class.</span></span>
*  <span data-ttu-id="143b6-425">연산자의 서명이 동일한 클래스에 선언 된 다른 모든 연산자의 시그니처와에서 달라 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-425">The signature of an operator must differ from the signatures of all other operators declared in the same class.</span></span>

<span data-ttu-id="143b6-426">클래스 형식의 상속된 된 멤버 ([상속](classes.md#inheritance))은 클래스의 선언 공간에 속하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-426">The inherited members of a class type ([Inheritance](classes.md#inheritance)) are not part of the declaration space of a class.</span></span> <span data-ttu-id="143b6-427">따라서 파생된 클래스는 상속 된 멤버 (상속 된 멤버를 숨깁니다 적용)와 이름 또는 시그니처가 같은 사용 하 여 멤버를 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-427">Thus, a derived class is allowed to declare a member with the same name or signature as an inherited member (which in effect hides the inherited member).</span></span>

### <a name="the-instance-type"></a><span data-ttu-id="143b6-428">인스턴스 형식</span><span class="sxs-lookup"><span data-stu-id="143b6-428">The instance type</span></span>

<span data-ttu-id="143b6-429">각 클래스 선언에는 연관 된 바인딩된 형식 ([바인딩되며 형식에 바인딩되지 않은](types.md#bound-and-unbound-types)), ***인스턴스 유형***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-429">Each class declaration has an associated bound type ([Bound and unbound types](types.md#bound-and-unbound-types)), the ***instance type***.</span></span> <span data-ttu-id="143b6-430">제네릭 클래스 선언에 대 한 인스턴스 유형이 생성된 된 형식을 만들어 형식이 ([형식 생성](types.md#constructed-types)) 형식 선언에서 지정 된 유형의 각 인수는 해당 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-430">For a generic class declaration, the instance type is formed by creating a constructed type ([Constructed types](types.md#constructed-types)) from the type declaration, with each of the supplied type arguments being the corresponding type parameter.</span></span> <span data-ttu-id="143b6-431">형식 매개 변수를 사용 하는 인스턴스 형식에 있으므로 사용할 수 있습니다만 범위에 형식 매개 변수가 있는 즉, 클래스 선언 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-431">Since the instance type uses the type parameters, it can only be used where the type parameters are in scope; that is, inside the class declaration.</span></span> <span data-ttu-id="143b6-432">인스턴스 형식의 형식인 `this` 클래스 선언 내에서 작성 된 코드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-432">The instance type is the type of `this` for code written inside the class declaration.</span></span> <span data-ttu-id="143b6-433">제네릭이 아닌 클래스에 대 한 인스턴스 유형 단순히 선언 된 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-433">For non-generic classes, the instance type is simply the declared class.</span></span> <span data-ttu-id="143b6-434">다음은 해당 인스턴스 형식과 함께 여러 클래스 선언입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-434">The following shows several class declarations along with their instance types:</span></span> 
```csharp
class A<T>                           // instance type: A<T>
{
    class B {}                       // instance type: A<T>.B
    class C<U> {}                    // instance type: A<T>.C<U>
}

class D {}                           // instance type: D
```

### <a name="members-of-constructed-types"></a><span data-ttu-id="143b6-435">생성 된 형식의 멤버</span><span class="sxs-lookup"><span data-stu-id="143b6-435">Members of constructed types</span></span>

<span data-ttu-id="143b6-436">생성 된 형식의 상속 되지 않는 멤버 각각에 대 한 대체 하 여 가져온 *type_parameter* 해당 멤버 선언에서 *type_argument* 생성 된 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-436">The non-inherited members of a constructed type are obtained by substituting, for each *type_parameter* in the member declaration, the corresponding *type_argument* of the constructed type.</span></span> <span data-ttu-id="143b6-437">대체 프로세스의 형식 선언, 의미 체계 의미를 기반으로 하는 아니며 단순히 텍스트 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-437">The substitution process is based on the semantic meaning of type declarations, and is not simply textual substitution.</span></span>

<span data-ttu-id="143b6-438">예를 들어 제네릭 클래스 선언</span><span class="sxs-lookup"><span data-stu-id="143b6-438">For example, given the generic class declaration</span></span>
```csharp
class Gen<T,U>
{
    public T[,] a;
    public void G(int i, T t, Gen<U,T> gt) {...}
    public U Prop { get {...} set {...} }
    public int H(double d) {...}
}
```
<span data-ttu-id="143b6-439">생성된 된 형식을 `Gen<int[],IComparable<string>>` 에 다음 멤버가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-439">the constructed type `Gen<int[],IComparable<string>>` has the following members:</span></span>
```csharp
public int[,][] a;
public void G(int i, int[] t, Gen<IComparable<string>,int[]> gt) {...}
public IComparable<string> Prop { get {...} set {...} }
public int H(double d) {...}
```

<span data-ttu-id="143b6-440">멤버의 형식을 `a` 제네릭 클래스 선언에서 `Gen` 는 "2 차원 배열을 `T`" 이므로 멤버의 형식을 `a` 위의 생성 된 형식에는 "1 차원 배열의 2차원배열`int`", 또는 `int[,][]`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-440">The type of the member `a` in the generic class declaration `Gen` is "two-dimensional array of `T`", so the type of the member `a` in the constructed type above is "two-dimensional array of one-dimensional array of `int`", or `int[,][]`.</span></span>

<span data-ttu-id="143b6-441">형식의 인스턴스 함수 범위로 `this` 인스턴스 유형 인지 ([인스턴스 유형을](classes.md#the-instance-type)) 포함 하는 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-441">Within instance function members, the type of `this` is the instance type ([The instance type](classes.md#the-instance-type)) of the containing declaration.</span></span>

<span data-ttu-id="143b6-442">제네릭 클래스의 모든 멤버는 직접적으로 또는 생성 된 형식의 일부로 모든 바깥쪽 클래스에서 형식 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-442">All members of a generic class can use type parameters from any enclosing class, either directly or as part of a constructed type.</span></span> <span data-ttu-id="143b6-443">특정 닫을 때 생성 된 형식 ([열기 및 닫힌 형식을](types.md#open-and-closed-types))는 실행 시 생성 된 형식에 제공 되는 실제 형식 인수를 사용 하 여 형식 매개 변수를 사용할 때마다 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-443">When a particular closed constructed type ([Open and closed types](types.md#open-and-closed-types)) is used at run-time, each use of a type parameter is replaced with the actual type argument supplied to the constructed type.</span></span> <span data-ttu-id="143b6-444">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="143b6-444">For example:</span></span>
```csharp
class C<V>
{
    public V f1;
    public C<V> f2 = null;

    public C(V x) {
        this.f1 = x;
        this.f2 = this;
    }
}

class Application
{
    static void Main() {
        C<int> x1 = new C<int>(1);
        Console.WriteLine(x1.f1);        // Prints 1

        C<double> x2 = new C<double>(3.1415);
        Console.WriteLine(x2.f1);        // Prints 3.1415
    }
}
```

### <a name="inheritance"></a><span data-ttu-id="143b6-445">상속</span><span class="sxs-lookup"><span data-stu-id="143b6-445">Inheritance</span></span>

<span data-ttu-id="143b6-446">클래스 ***상속*** 직접 기본 클래스 형식의 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-446">A class ***inherits*** the members of its direct base class type.</span></span> <span data-ttu-id="143b6-447">상속은 클래스는 직접 기본 클래스 형식의 인스턴스 생성자, 소멸자 및 기본 클래스의 정적 생성자를 제외한 모든 멤버를 암시적으로 포함 하는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-447">Inheritance means that a class implicitly contains all members of its direct base class type, except for the instance constructors, destructors and static constructors of the base class.</span></span> <span data-ttu-id="143b6-448">상속의 몇 가지 중요 한 측면은:</span><span class="sxs-lookup"><span data-stu-id="143b6-448">Some important aspects of inheritance are:</span></span>

*  <span data-ttu-id="143b6-449">상속은 전이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-449">Inheritance is transitive.</span></span> <span data-ttu-id="143b6-450">경우 `C` 에서 파생 됩니다 `B`, 및 `B` 에서 파생 됩니다 `A`, 한 다음 `C` 에 선언 된 멤버를 상속 `B` 에 선언 된 멤버 뿐만 아니라 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-450">If `C` is derived from `B`, and `B` is derived from `A`, then `C` inherits the members declared in `B` as well as the members declared in `A`.</span></span>
*  <span data-ttu-id="143b6-451">파생된 클래스의 직접 기본 클래스를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-451">A derived class extends its direct base class.</span></span> <span data-ttu-id="143b6-452">파생된 클래스를 상속하는 대상에 새 멤버를 추가할 수 있지만 상속된 멤버의 정의를 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-452">A derived class can add new members to those it inherits, but it cannot remove the definition of an inherited member.</span></span>
*  <span data-ttu-id="143b6-453">인스턴스 생성자, 소멸자 및 정적 생성자는 상속 되지 않지만 해당 선언 된 접근성에 관계 없이 다른 모든 멤버는 ([멤버 액세스](basic-concepts.md#member-access)).</span><span class="sxs-lookup"><span data-stu-id="143b6-453">Instance constructors, destructors, and static constructors are not inherited, but all other members are, regardless of their declared accessibility ([Member access](basic-concepts.md#member-access)).</span></span> <span data-ttu-id="143b6-454">그러나 해당 선언 된 액세스 가능성에 따라 상속 된 멤버 수 없습니다 파생된 클래스에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-454">However, depending on their declared accessibility, inherited members might not be accessible in a derived class.</span></span>
*  <span data-ttu-id="143b6-455">파생된 클래스 수 ***숨기기*** ([상속을 통해 숨기기](basic-concepts.md#hiding-through-inheritance)) 상속 된 멤버 이름 또는 시그니처가 같은 새로운 멤버를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-455">A derived class can ***hide*** ([Hiding through inheritance](basic-concepts.md#hiding-through-inheritance)) inherited members by declaring new members with the same name or signature.</span></span> <span data-ttu-id="143b6-456">그러나 상속된 된 멤버를 숨기는에서는 제거 되지 않습니다 해당 멤버 —는 해당 멤버는 파생된 클래스를 통해 직접 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-456">Note however that hiding an inherited member does not remove that member—it merely makes that member inaccessible directly through the derived class.</span></span>
*  <span data-ttu-id="143b6-457">클래스의 인스턴스 클래스 및 해당 기본 클래스와 암시적 변환에 선언 된 모든 인스턴스 필드의 집합을 포함 ([암시적 참조 변환](conversions.md#implicit-reference-conversions)) 해당 기본 클래스 형식에서 파생 된 클래스 형식 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-457">An instance of a class contains a set of all instance fields declared in the class and its base classes, and an implicit conversion ([Implicit reference conversions](conversions.md#implicit-reference-conversions)) exists from a derived class type to any of its base class types.</span></span> <span data-ttu-id="143b6-458">따라서 해당 기본 클래스의 인스턴스에 대 한 참조로 몇 가지 파생된 클래스의 인스턴스에 대 한 참조를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-458">Thus, a reference to an instance of some derived class can be treated as a reference to an instance of any of its base classes.</span></span>
*  <span data-ttu-id="143b6-459">클래스는 가상 메서드, 속성 및 인덱서를 선언할 수 있습니다 및 파생된 클래스에는 이러한 함수 멤버의 구현을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-459">A class can declare virtual methods, properties, and indexers, and derived classes can override the implementation of these function members.</span></span> <span data-ttu-id="143b6-460">따라서 클래스를에서 함수 멤버 호출을 수행한 작업을 해당 하는 함수 멤버 호출에 사용 되는 인스턴스의 런타임 형식에 따라 여기서 원하는 다형성 동작을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-460">This enables classes to exhibit polymorphic behavior wherein the actions performed by a function member invocation varies depending on the run-time type of the instance through which that function member is invoked.</span></span>

<span data-ttu-id="143b6-461">생성 된 클래스 형식의 상속 된 멤버는 직접 기본 클래스 형식의 멤버 ([기본 클래스](classes.md#base-classes)), 각 해당 형식에 대해 생성 된 형식의 형식 인수를 대체 하 여 찾을 수 있는 매개 변수를 *class_base* 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-461">The inherited member of a constructed class type are the members of the immediate base class type ([Base classes](classes.md#base-classes)), which is found by substituting the type arguments of the constructed type for each occurrence of the corresponding type parameters in the *class_base* specification.</span></span> <span data-ttu-id="143b6-462">따라서 이러한 멤버 각각에 대 한 대체 하 여 변환 됩니다 *type_parameter* 해당 멤버 선언에서 *type_argument* 의 합니다 *class_base* 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-462">These members, in turn, are transformed by substituting, for each *type_parameter* in the member declaration, the corresponding *type_argument* of the *class_base* specification.</span></span>

```csharp
class B<U>
{
    public U F(long index) {...}
}

class D<T>: B<T[]>
{
    public T G(string s) {...}
}
```

<span data-ttu-id="143b6-463">위의 예에서 생성 된 형식 `D<int>` 상속 되지 않는 멤버가 `public int G(string s)` 형식 인수를 대체 하 여 얻은 `int` 형식 매개 변수에 대해 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-463">In the above example, the constructed type `D<int>` has a non-inherited member `public int G(string s)` obtained by substituting the type argument `int` for the type parameter `T`.</span></span> <span data-ttu-id="143b6-464">`D<int>` 상속된 된 멤버를 클래스 선언에서 역시 `B`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-464">`D<int>` also has an inherited member from the class declaration `B`.</span></span> <span data-ttu-id="143b6-465">이 상속 된 멤버는 기본 클래스 형식을 확인 하 여 결정 됩니다 `B<int[]>` 의 `D<int>` 대체 하 여 `int` 에 대 한 `T` 기본 클래스 사양에 `B<T[]>`입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-465">This inherited member is determined by first determining the base class type `B<int[]>` of `D<int>` by substituting `int` for `T` in the base class specification `B<T[]>`.</span></span> <span data-ttu-id="143b6-466">그런 다음에 형식 인수로 `B`, `int[]` 대체 하는 `U` 에서 `public U F(long index)`, 상속 된 멤버를 생성 `public int[] F(long index)`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-466">Then, as a type argument to `B`, `int[]` is substituted for `U` in `public U F(long index)`, yielding the inherited member `public int[] F(long index)`.</span></span>

### <a name="the-new-modifier"></a><span data-ttu-id="143b6-467">New 한정자</span><span class="sxs-lookup"><span data-stu-id="143b6-467">The new modifier</span></span>

<span data-ttu-id="143b6-468">A *class_member_declaration* 는를 사용 하 여 이름 또는 시그니처가 같은 상속된 된 멤버와 멤버를 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-468">A *class_member_declaration* is permitted to declare a member with the same name or signature as an inherited member.</span></span> <span data-ttu-id="143b6-469">이 경우 파생된 클래스 멤버를 라고 ***숨기기*** 기본 클래스 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-469">When this occurs, the derived class member is said to ***hide*** the base class member.</span></span> <span data-ttu-id="143b6-470">상속된 된 멤버 숨기기는 오류로 간주 하지는 않지만 컴파일러 경고가 발생 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-470">Hiding an inherited member is not considered an error, but it does cause the compiler to issue a warning.</span></span> <span data-ttu-id="143b6-471">경고를 표시 하지 않으려면 파생된 클래스 멤버의 선언을 포함할 수는 `new` 한정자는 파생된 멤버가 기본 멤버를 숨기려면 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-471">To suppress the warning, the declaration of the derived class member can include a `new` modifier to indicate that the derived member is intended to hide the base member.</span></span> <span data-ttu-id="143b6-472">이 항목 설명에 대 한 자세한 [상속을 통해 숨기기](basic-concepts.md#hiding-through-inheritance)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-472">This topic is discussed further in [Hiding through inheritance](basic-concepts.md#hiding-through-inheritance).</span></span>

<span data-ttu-id="143b6-473">경우는 `new` 한정자는 상속 된 멤버를 숨기지 않는 선언에 포함 되어, 그 결과 경고가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-473">If a `new` modifier is included in a declaration that doesn't hide an inherited member, a warning to that effect is issued.</span></span> <span data-ttu-id="143b6-474">이 경고를 제거 하 여 표시 되지 않는지를 `new` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-474">This warning is suppressed by removing the `new` modifier.</span></span>

### <a name="access-modifiers"></a><span data-ttu-id="143b6-475">액세스 한정자</span><span class="sxs-lookup"><span data-stu-id="143b6-475">Access modifiers</span></span>

<span data-ttu-id="143b6-476">A *class_member_declaration* 5 등의 사용 가능한 선언 된 액세스 가능성 중 하나를 가질 수 있습니다 ([접근성을 선언](basic-concepts.md#declared-accessibility)): `public`를 `protected internal`를 `protected`, `internal` 또는 `private`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-476">A *class_member_declaration* can have any one of the five possible kinds of declared accessibility ([Declared accessibility](basic-concepts.md#declared-accessibility)): `public`, `protected internal`, `protected`, `internal`, or `private`.</span></span> <span data-ttu-id="143b6-477">제외 하 고는 `protected internal` 둘 이상의 액세스 한정자를 지정 하는 컴파일 시간 오류는 조합 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-477">Except for the `protected internal` combination, it is a compile-time error to specify more than one access modifier.</span></span> <span data-ttu-id="143b6-478">경우는 *class_member_declaration* 액세스 한정자를 다루지 않습니다 `private` 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-478">When a *class_member_declaration* does not include any access modifiers, `private` is assumed.</span></span>

### <a name="constituent-types"></a><span data-ttu-id="143b6-479">구성 요소 형식</span><span class="sxs-lookup"><span data-stu-id="143b6-479">Constituent types</span></span>

<span data-ttu-id="143b6-480">멤버의 선언에 사용 되는 형식에는 해당 멤버의 구성 요소 형식 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-480">Types that are used in the declaration of a member are called the constituent types of that member.</span></span> <span data-ttu-id="143b6-481">가능한 구성 요소 유형은 상수, 필드, 속성, 이벤트 또는 인덱서의 유형, 메서드 또는 연산자의 반환 형식 및 메서드, 인덱서, 연산자 또는 인스턴스 생성자의 매개 변수 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-481">Possible constituent types are the type of a constant, field, property, event, or indexer, the return type of a method or operator, and the parameter types of a method, indexer, operator, or instance constructor.</span></span> <span data-ttu-id="143b6-482">구성 유형의 멤버를 해당 멤버 자체 만큼 액세스 가능 이상 이어야 합니다 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="143b6-482">The constituent types of a member must be at least as accessible as that member itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

### <a name="static-and-instance-members"></a><span data-ttu-id="143b6-483">정적 및 인스턴스 멤버</span><span class="sxs-lookup"><span data-stu-id="143b6-483">Static and instance members</span></span>

<span data-ttu-id="143b6-484">클래스의 멤버는 ***정적 멤버*** 하거나 ***인스턴스 멤버***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-484">Members of a class are either ***static members*** or ***instance members***.</span></span> <span data-ttu-id="143b6-485">일반적으로 정적 멤버는 클래스 형식 및 개체 (클래스 형식의 인스턴스)에 속하는 것으로 인스턴스 멤버에 속한 것으로 생각 하는 것이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-485">Generally speaking, it is useful to think of static members as belonging to class types and instance members as belonging to objects (instances of class types).</span></span>

<span data-ttu-id="143b6-486">필드, 메서드, 속성, 이벤트, 연산자 또는 생성자 선언을 포함 하는 경우는 `static` 한정자, 정적 멤버를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-486">When a field, method, property, event, operator, or constructor declaration includes a `static` modifier, it declares a static member.</span></span> <span data-ttu-id="143b6-487">또한 상수 또는 형식 선언은 암시적으로 정적 멤버를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-487">In addition, a constant or type declaration implicitly declares a static member.</span></span> <span data-ttu-id="143b6-488">정적 멤버에는 다음과 같은 특징이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-488">Static members have the following characteristics:</span></span>

*  <span data-ttu-id="143b6-489">정적 멤버가 `M` 에서 참조 되는 *member_access* ([멤버 액세스](expressions.md#member-access)) 폼의 `E.M`, `E` 포함 하는 형식 표시 해야 합니다 `M`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-489">When a static member `M` is referenced in a *member_access* ([Member access](expressions.md#member-access)) of the form `E.M`, `E` must denote a type containing `M`.</span></span> <span data-ttu-id="143b6-490">에 대 한 컴파일 시간 오류 `E` 인스턴스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-490">It is a compile-time error for `E` to denote an instance.</span></span>
*  <span data-ttu-id="143b6-491">정적 필드는 닫힌된 주어진된 클래스 형식의 모든 인스턴스에서 공유 하도록 정확히 하나의 저장 위치를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-491">A static field identifies exactly one storage location to be shared by all instances of a given closed class type.</span></span> <span data-ttu-id="143b6-492">지정 된 닫힌된 클래스 유형 인스턴스 개수를 생성 없이 정적 필드의 사본 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-492">No matter how many instances of a given closed class type are created, there is only ever one copy of a static field.</span></span>
*  <span data-ttu-id="143b6-493">정적 함수 멤버 (메서드, 속성, 이벤트, 연산자 또는 생성자)는 특정 인스턴스에 작동 하지 않고 이며 컴파일 타임 오류를 가리키는 데 `this` 함수 멤버에서입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-493">A static function member (method, property, event, operator, or constructor) does not operate on a specific instance, and it is a compile-time error to refer to `this` in such a function member.</span></span>

<span data-ttu-id="143b6-494">필드, 메서드, 속성, 이벤트, 인덱서, 생성자 또는 소멸자가 선언 포함 되지 않습니다는 `static` 한정자를 인스턴스 멤버를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-494">When a field, method, property, event, indexer, constructor, or destructor declaration does not include a `static` modifier, it declares an instance member.</span></span> <span data-ttu-id="143b6-495">(인스턴스 멤버는 비정적 멤버 라고도 함은.) 인스턴스 멤버에는 다음과 같은 특징이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-495">(An instance member is sometimes called a non-static member.) Instance members have the following characteristics:</span></span>

*  <span data-ttu-id="143b6-496">때 인스턴스 멤버 `M` 에서 참조 되는 *member_access* ([멤버 액세스](expressions.md#member-access)) 양식의 `E.M`, `E` 를포함하는형식의인스턴스를표시해야합니다`M`.</span><span class="sxs-lookup"><span data-stu-id="143b6-496">When an instance member `M` is referenced in a *member_access* ([Member access](expressions.md#member-access)) of the form `E.M`, `E` must denote an instance of a type containing `M`.</span></span> <span data-ttu-id="143b6-497">에 대 한 바인딩 시간 오류 `E` 를 나타내는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-497">It is a binding-time error for `E` to denote a type.</span></span>
*  <span data-ttu-id="143b6-498">클래스의 모든 인스턴스 클래스의 모든 인스턴스 필드의 별도 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-498">Every instance of a class contains a separate set of all instance fields of the class.</span></span>
*  <span data-ttu-id="143b6-499">클래스의 인스턴스에 인스턴스 함수 멤버 (메서드, 속성, 인덱서, 인스턴스 생성자 또는 소멸자) 작동 하 고이 인스턴스를 액세스할 수 있습니다 `this` ([이 액세스](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="143b6-499">An instance function member (method, property, indexer, instance constructor, or destructor) operates on a given instance of the class, and this instance can be accessed as `this` ([This access](expressions.md#this-access)).</span></span>

<span data-ttu-id="143b6-500">다음 예제에서는 정적 액세스 규칙 및 인스턴스 멤버를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-500">The following example illustrates the rules for accessing static and instance members:</span></span>
```csharp
class Test
{
    int x;
    static int y;

    void F() {
        x = 1;            // Ok, same as this.x = 1
        y = 1;            // Ok, same as Test.y = 1
    }

    static void G() {
        x = 1;            // Error, cannot access this.x
        y = 1;            // Ok, same as Test.y = 1
    }

    static void Main() {
        Test t = new Test();
        t.x = 1;          // Ok
        t.y = 1;          // Error, cannot access static member through instance
        Test.x = 1;       // Error, cannot access instance member through type
        Test.y = 1;       // Ok
    }
}
```

<span data-ttu-id="143b6-501">합니다 `F` 메서드는 인스턴스 함수 멤버를 보여 줍니다는 *simple_name* ([단순 이름](expressions.md#simple-names)) 인스턴스 멤버 및 정적 멤버에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-501">The `F` method shows that in an instance function member, a *simple_name* ([Simple names](expressions.md#simple-names)) can be used to access both instance members and static members.</span></span> <span data-ttu-id="143b6-502">합니다 `G` 메서드를 보여 줍니다는 정적 함수 멤버인에서는 컴파일 타임 오류를 통해 인스턴스 멤버에 액세스 하는 *simple_name*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-502">The `G` method shows that in a static function member, it is a compile-time error to access an instance member through a *simple_name*.</span></span> <span data-ttu-id="143b6-503">`Main` 메서드를 보여 줍니다에 *member_access* ([멤버 액세스](expressions.md#member-access)) 인스턴스를 인스턴스 멤버에 액세스 해야 하 고 형식을 통해 정적 멤버에 액세스 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-503">The `Main` method shows that in a *member_access* ([Member access](expressions.md#member-access)), instance members must be accessed through instances, and static members must be accessed through types.</span></span>

### <a name="nested-types"></a><span data-ttu-id="143b6-504">중첩 형식</span><span class="sxs-lookup"><span data-stu-id="143b6-504">Nested types</span></span>

<span data-ttu-id="143b6-505">클래스 또는 구조체 선언 내에서 선언 된 형식 호출 되는 ***중첩 형식이***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-505">A type declared within a class or struct declaration is called a ***nested type***.</span></span> <span data-ttu-id="143b6-506">컴파일 단위 또는 네임 스페이스 내에서 선언 된 형식 호출 되는 ***중첩 되지 않은 형식***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-506">A type that is declared within a compilation unit or namespace is called a ***non-nested type***.</span></span>

<span data-ttu-id="143b6-507">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-507">In the example</span></span>
```csharp
using System;

class A
{
    class B
    {
        static void F() {
            Console.WriteLine("A.B.F");
        }
    }
}
```
<span data-ttu-id="143b6-508">클래스 `B` 중첩된 형식 이므로 클래스 내에 선언 `A`, 및 클래스 `A` 중첩 되지 않은 형식 이므로 컴파일 단위 내에 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-508">class `B` is a nested type because it is declared within class `A`, and class `A` is a non-nested type because it is declared within a compilation unit.</span></span>

#### <a name="fully-qualified-name"></a><span data-ttu-id="143b6-509">정규화 된 이름</span><span class="sxs-lookup"><span data-stu-id="143b6-509">Fully qualified name</span></span>

<span data-ttu-id="143b6-510">정규화 된 이름 ([정규화 된 이름](basic-concepts.md#fully-qualified-names)) 중첩 된 형식에 대 한 `S.N` 여기서 `S` 유형 형식의 정규화 된 이름인 `N` 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-510">The fully qualified name ([Fully qualified names](basic-concepts.md#fully-qualified-names)) for a nested type is `S.N` where `S` is the fully qualified name of the type in which type `N` is declared.</span></span>

#### <a name="declared-accessibility"></a><span data-ttu-id="143b6-511">선언된 액세스 가능성</span><span class="sxs-lookup"><span data-stu-id="143b6-511">Declared accessibility</span></span>

<span data-ttu-id="143b6-512">비 중첩 형식도 가질 수 있습니다 `public` 하거나 `internal` 접근성을 선언 하 고 있는 `internal` 내게 필요한 옵션은 기본적으로 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-512">Non-nested types can have `public` or `internal` declared accessibility and have `internal` declared accessibility by default.</span></span> <span data-ttu-id="143b6-513">중첩된 형식은 클래스 또는 구조체를 포함 하는 형식 인지에 따라 선언 된 내게 필요한 옵션의 하나 이상의 추가 형식 및 이러한 형태의 선언 된 접근성을도 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-513">Nested types can have these forms of declared accessibility too, plus one or more additional forms of declared accessibility, depending on whether the containing type is a class or struct:</span></span>

*  <span data-ttu-id="143b6-514">클래스에서 선언 된 중첩된 형식이 선언 된 액세스 가능성의 5 가지 중 하나일 수 있습니다 (`public`, `protected internal`를 `protected`를 `internal`, 또는 `private`) 및 다른 클래스 멤버와 마찬가지로 기본값 `private` 선언 내게 필요한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-514">A nested type that is declared in a class can have any of five forms of declared accessibility (`public`, `protected internal`, `protected`, `internal`, or `private`) and, like other class members, defaults to `private` declared accessibility.</span></span>
*  <span data-ttu-id="143b6-515">구조체에 선언 된 중첩된 형식이 선언 된 액세스 가능성의 세 가지 형식 중 하나일 수 있습니다 (`public`, `internal`, 또는 `private`) 및 다른 구조체 멤버와 마찬가지로 기본값 `private` 접근성을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-515">A nested type that is declared in a struct can have any of three forms of declared accessibility (`public`, `internal`, or `private`) and, like other struct members, defaults to `private` declared accessibility.</span></span>

<span data-ttu-id="143b6-516">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-516">The example</span></span>
```csharp
public class List
{
    // Private data structure
    private class Node
    { 
        public object Data;
        public Node Next;

        public Node(object data, Node next) {
            this.Data = data;
            this.Next = next;
        }
    }

    private Node first = null;
    private Node last = null;

    // Public interface
    public void AddToFront(object o) {...}
    public void AddToBack(object o) {...}
    public object RemoveFromFront() {...}
    public object RemoveFromBack() {...}
    public int Count { get {...} }
}
```
<span data-ttu-id="143b6-517">전용 중첩된 클래스 선언 `Node`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-517">declares a private nested class `Node`.</span></span>

#### <a name="hiding"></a><span data-ttu-id="143b6-518">숨기기</span><span class="sxs-lookup"><span data-stu-id="143b6-518">Hiding</span></span>

<span data-ttu-id="143b6-519">중첩된 형식은 숨길 수 있습니다 ([이름 숨기기](basic-concepts.md#name-hiding)) 기본 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-519">A nested type may hide ([Name hiding](basic-concepts.md#name-hiding)) a base member.</span></span> <span data-ttu-id="143b6-520">`new` 숨기기를 명시적으로 표현 될 수 있도록 중첩된 형식 선언에서 한정자가 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-520">The `new` modifier is permitted on nested type declarations so that hiding can be expressed explicitly.</span></span> <span data-ttu-id="143b6-521">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-521">The example</span></span>
```csharp
using System;

class Base
{
    public static void M() {
        Console.WriteLine("Base.M");
    }
}

class Derived: Base 
{
    new public class M 
    {
        public static void F() {
            Console.WriteLine("Derived.M.F");
        }
    }
}

class Test 
{
    static void Main() {
        Derived.M.F();
    }
}
```
<span data-ttu-id="143b6-522">중첩된 클래스를 보여 줍니다 `M` 하는 메서드를 숨깁니다 `M` 에 정의 된 `Base`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-522">shows a nested class `M` that hides the method `M` defined in `Base`.</span></span>

#### <a name="this-access"></a><span data-ttu-id="143b6-523">이 액세스</span><span class="sxs-lookup"><span data-stu-id="143b6-523">this access</span></span>

<span data-ttu-id="143b6-524">중첩된 형식 및 포함 하는 형식 관련해 서는 특수 한 관계가 없는 *this_access* ([이 액세스](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="143b6-524">A nested type and its containing type do not have a special relationship with regard to *this_access* ([This access](expressions.md#this-access)).</span></span> <span data-ttu-id="143b6-525">특히 `this` 중첩된 형식 내에서 포함 하는 형식의 인스턴스 멤버 참조를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-525">Specifically, `this` within a nested type cannot be used to refer to instance members of the containing type.</span></span> <span data-ttu-id="143b6-526">중첩된 된 형식을 포함 하는 형식의 인스턴스 멤버에 대 한 액세스 해야 하는 경우에 대 한 액세스를 제공 하 여 제공할 수 있습니다는 `this` 중첩 된 형식에 대 한 생성자 인수로 포함 하는 형식 인스턴스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-526">In cases where a nested type needs access to the instance members of its containing type, access can be provided by providing the `this` for the instance of the containing type as a constructor argument for the nested type.</span></span> <span data-ttu-id="143b6-527">다음 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-527">The following example</span></span>
```csharp
using System;

class C
{
    int i = 123;

    public void F() {
        Nested n = new Nested(this);
        n.G();
    }

    public class Nested
    {
        C this_c;

        public Nested(C c) {
            this_c = c;
        }

        public void G() {
            Console.WriteLine(this_c.i);
        }
    }
}

class Test
{
    static void Main() {
        C c = new C();
        c.F();
    }
}
```
<span data-ttu-id="143b6-528">이 기술을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-528">shows this technique.</span></span> <span data-ttu-id="143b6-529">인스턴스의 `C` 의 인스턴스를 만듭니다 `Nested` 자체 전달 `this` 하 `Nested`의 생성자에 대 한 후속 액세스를 제공 하기 위해 `C`의 인스턴스 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-529">An instance of `C` creates an instance of `Nested` and passes its own `this` to `Nested`'s constructor in order to provide subsequent access to `C`'s instance members.</span></span>

#### <a name="access-to-private-and-protected-members-of-the-containing-type"></a><span data-ttu-id="143b6-530">포함 하는 형식의 private 및 protected 멤버에 대 한 액세스</span><span class="sxs-lookup"><span data-stu-id="143b6-530">Access to private and protected members of the containing type</span></span>

<span data-ttu-id="143b6-531">중첩 된 형식에 있는 포함 하는 형식의 멤버를 포함 하 여 포함 하는 형식에 액세스할 수 있는 멤버의 모든 권한을 `private` 및 `protected` 접근성을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-531">A nested type has access to all of the members that are accessible to its containing type, including members of the containing type that have `private` and `protected` declared accessibility.</span></span> <span data-ttu-id="143b6-532">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-532">The example</span></span>
```csharp
using System;

class C 
{
    private static void F() {
        Console.WriteLine("C.F");
    }

    public class Nested 
    {
        public static void G() {
            F();
        }
    }
}

class Test 
{
    static void Main() {
        C.Nested.G();
    }
}
```
<span data-ttu-id="143b6-533">클래스를 보여 줍니다 `C` 중첩된 된 클래스를 포함 하는 `Nested`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-533">shows a class `C` that contains a nested class `Nested`.</span></span> <span data-ttu-id="143b6-534">내 `Nested`, 메서드 `G` 정적 메서드를 호출 `F` 에 정의 된 `C`, 및 `F` private 선언에 내게 필요한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-534">Within `Nested`, the method `G` calls the static method `F` defined in `C`, and `F` has private declared accessibility.</span></span>

<span data-ttu-id="143b6-535">또한 중첩된 된 형식을 포함 하는 형식의 기본 형식에 정의 된 보호 된 멤버 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-535">A nested type also may access protected members defined in a base type of its containing type.</span></span> <span data-ttu-id="143b6-536">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-536">In the example</span></span>
```csharp
using System;

class Base 
{
    protected void F() {
        Console.WriteLine("Base.F");
    }
}

class Derived: Base 
{
    public class Nested 
    {
        public void G() {
            Derived d = new Derived();
            d.F();        // ok
        }
    }
}

class Test 
{
    static void Main() {
        Derived.Nested n = new Derived.Nested();
        n.G();
    }
}
```
<span data-ttu-id="143b6-537">중첩된 클래스 `Derived.Nested` 보호 된 메서드에 액세스 `F` 에 정의 된 `Derived`의 기본 클래스 `Base`의 인스턴스를 통해 호출 `Derived`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-537">the nested class `Derived.Nested` accesses the protected method `F` defined in `Derived`'s base class, `Base`, by calling through an instance of `Derived`.</span></span>

#### <a name="nested-types-in-generic-classes"></a><span data-ttu-id="143b6-538">제네릭 클래스의 중첩된 형식</span><span class="sxs-lookup"><span data-stu-id="143b6-538">Nested types in generic classes</span></span>

<span data-ttu-id="143b6-539">제네릭 클래스 선언에는 중첩된 형식 선언을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-539">A generic class declaration can contain nested type declarations.</span></span> <span data-ttu-id="143b6-540">형식 매개 변수는 바깥쪽 클래스의 중첩된 형식 내에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-540">The type parameters of the enclosing class can be used within the nested types.</span></span> <span data-ttu-id="143b6-541">중첩된 형식 선언 중첩 된 형식에만 적용 되는 추가 형식 매개 변수를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-541">A nested type declaration can contain additional type parameters that apply only to the nested type.</span></span>

<span data-ttu-id="143b6-542">제네릭 클래스 선언 내에 포함 된 모든 형식 선언은 암시적으로 제네릭 형식 선언이입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-542">Every type declaration contained within a generic class declaration is implicitly a generic type declaration.</span></span> <span data-ttu-id="143b6-543">제네릭 형식 안에 중첩 형식에 대 한 참조를 작성 하는 경우에 해당 형식 인수를 포함 하 여 포함 하는 생성 된 형식에 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-543">When writing a reference to a type nested within a generic type, the containing constructed type, including its type arguments, must be named.</span></span> <span data-ttu-id="143b6-544">그러나에서 외부 클래스 내에서 중첩된 된 형식을 사용할 수 있습니다; 한정자 없이 중첩 된 형식을 생성 하는 경우 외부 클래스의 인스턴스 유형은 암시적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-544">However, from within the outer class, the nested type can be used without qualification; the instance type of the outer class can be implicitly used when constructing the nested type.</span></span> <span data-ttu-id="143b6-545">다음 예제에서는에서 만든 생성된 된 형식을 참조 하 세 가지 올바른 `Inner`; 처음 두 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-545">The following example shows three different correct ways to refer to a constructed type created from `Inner`; the first two are equivalent:</span></span>
```csharp
class Outer<T>
{
    class Inner<U>
    {
        public static void F(T t, U u) {...}
    }

    static void F(T t) {
        Outer<T>.Inner<string>.F(t, "abc");      // These two statements have
        Inner<string>.F(t, "abc");               // the same effect

        Outer<int>.Inner<string>.F(3, "abc");    // This type is different

        Outer.Inner<string>.F(t, "abc");         // Error, Outer needs type arg
    }
}
```

<span data-ttu-id="143b6-546">잘못 된 이지만 프로그래밍 스타일을 중첩된 된 형식에 형식 매개 변수 멤버 하거나 숨기려면 형식 매개 변수가 외부 형식에서 선언:</span><span class="sxs-lookup"><span data-stu-id="143b6-546">Although it is bad programming style, a type parameter in a nested type can hide a member or type parameter declared in the outer type:</span></span>
```csharp
class Outer<T>
{
    class Inner<T>        // Valid, hides Outer's T
    {
        public T t;       // Refers to Inner's T
    }
}
```

### <a name="reserved-member-names"></a><span data-ttu-id="143b6-547">예약 된 멤버 이름</span><span class="sxs-lookup"><span data-stu-id="143b6-547">Reserved member names</span></span>

<span data-ttu-id="143b6-548">기본 C# 런타임 구현 속성, 이벤트 또는 인덱서는 각 원본 멤버 선언에 대 한를 용이 하 게 구현 멤버 선언, 해당 이름 및 형식과의 종류에 따라 두 가지 메서드 시그니처를 예약 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-548">To facilitate the underlying C# run-time implementation, for each source member declaration that is a property, event, or indexer, the implementation must reserve two method signatures based on the kind of the member declaration, its name, and its type.</span></span> <span data-ttu-id="143b6-549">기본 런타임 구현을 구성 하지 않는 경우에 멤버 중 일치 하는 시그니처를 가진 예약 서명을 선언 하는 프로그램에 대 한 컴파일 시간 오류 이러한 예약 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-549">It is a compile-time error for a program to declare a member whose signature matches one of these reserved signatures, even if the underlying run-time implementation does not make use of these reservations.</span></span>

<span data-ttu-id="143b6-550">예약된 된 이름 선언에 가져오지 마세요, 따라서 이러한에 참여 하지 않는 멤버 조회 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-550">The reserved names do not introduce declarations, thus they do not participate in member lookup.</span></span> <span data-ttu-id="143b6-551">그러나 선언 관련 서명을 수행 상속에 참여 하는 예약 된 메서드 ([상속](classes.md#inheritance))를 사용 하 여 숨길 수는 `new` 한정자 ([new 한정자](classes.md#the-new-modifier)).</span><span class="sxs-lookup"><span data-stu-id="143b6-551">However, a declaration's associated reserved method signatures do participate in inheritance ([Inheritance](classes.md#inheritance)), and can be hidden with the `new` modifier ([The new modifier](classes.md#the-new-modifier)).</span></span>

<span data-ttu-id="143b6-552">이러한 이름은 예약은 세 가지 용도로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-552">The reservation of these names serves three purposes:</span></span>

*  <span data-ttu-id="143b6-553">Get 메서드 이름으로 일반 식별자를 사용 하거나 C# 언어 기능에 대 한 액세스를 설정 하는 기본 구현을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-553">To allow the underlying implementation to use an ordinary identifier as a method name for get or set access to the C# language feature.</span></span>
*  <span data-ttu-id="143b6-554">Get 메서드 이름으로 일반 식별자를 사용 하 여 상호 운용 또는 C# 언어 기능에 대 한 액세스를 설정 하려면 다른 언어를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-554">To allow other languages to interoperate using an ordinary identifier as a method name for get or set access to the C# language feature.</span></span>
*  <span data-ttu-id="143b6-555">소스는 하나의 준수 컴파일러에서 허용 되는지 확인 하려면 수락한 경우 다른 만들어 예약 된 멤버의 특성 이름을 일관 된 모든 C# 구현에서.</span><span class="sxs-lookup"><span data-stu-id="143b6-555">To help ensure that the source accepted by one conforming compiler is accepted by another, by making the specifics of reserved member names consistent across all C# implementations.</span></span>

<span data-ttu-id="143b6-556">소멸자의 선언 ([소멸자](classes.md#destructors))도 사용 될 서명 하면 ([소멸자에 대 한 예약 된 멤버 이름](classes.md#member-names-reserved-for-destructors)).</span><span class="sxs-lookup"><span data-stu-id="143b6-556">The declaration of a destructor ([Destructors](classes.md#destructors)) also causes a signature to be reserved ([Member names reserved for destructors](classes.md#member-names-reserved-for-destructors)).</span></span>

#### <a name="member-names-reserved-for-properties"></a><span data-ttu-id="143b6-557">속성에 대 한 예약 된 멤버 이름</span><span class="sxs-lookup"><span data-stu-id="143b6-557">Member names reserved for properties</span></span>

<span data-ttu-id="143b6-558">속성에 대 한 `P` ([속성](classes.md#properties)) 형식의 `T`, 다음 시그니처만 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-558">For a property `P` ([Properties](classes.md#properties)) of type `T`, the following signatures are reserved:</span></span>

```csharp
T get_P();
void set_P(T value);
```

<span data-ttu-id="143b6-559">속성은 읽기 전용 또는 쓰기 전용일 경우에 서명은 모두 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-559">Both signatures are reserved, even if the property is read-only or write-only.</span></span>

<span data-ttu-id="143b6-560">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-560">In the example</span></span>
```csharp
using System;

class A
{
    public int P {
        get { return 123; }
    }
}

class B: A
{
    new public int get_P() {
        return 456;
    }

    new public void set_P(int value) {
    }
}

class Test
{
    static void Main() {
        B b = new B();
        A a = b;
        Console.WriteLine(a.P);
        Console.WriteLine(b.P);
        Console.WriteLine(b.get_P());
    }
}
```
<span data-ttu-id="143b6-561">클래스 `A` 읽기 전용 속성을 정의 `P`에 대해 시그니처가 `get_P` 및 `set_P` 메서드.</span><span class="sxs-lookup"><span data-stu-id="143b6-561">a class `A` defines a read-only property `P`, thus reserving signatures for `get_P` and `set_P` methods.</span></span> <span data-ttu-id="143b6-562">클래스 `B` 에서 파생 `A` 하 고 이러한 예약 된 서명을 모두 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-562">A class `B` derives from `A` and hides both of these reserved signatures.</span></span> <span data-ttu-id="143b6-563">이 예제에서는 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-563">The example produces the output:</span></span>
```
123
123
456
```

#### <a name="member-names-reserved-for-events"></a><span data-ttu-id="143b6-564">이벤트에 대 한 예약 된 멤버 이름</span><span class="sxs-lookup"><span data-stu-id="143b6-564">Member names reserved for events</span></span>

<span data-ttu-id="143b6-565">이벤트에 대 한 `E` ([이벤트](classes.md#events)) 대리자 형식 `T`, 다음 시그니처만 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-565">For an event `E` ([Events](classes.md#events)) of delegate type `T`, the following signatures are reserved:</span></span>
```csharp
void add_E(T handler);
void remove_E(T handler);
```

#### <a name="member-names-reserved-for-indexers"></a><span data-ttu-id="143b6-566">인덱서에 대 한 예약 된 멤버 이름</span><span class="sxs-lookup"><span data-stu-id="143b6-566">Member names reserved for indexers</span></span>

<span data-ttu-id="143b6-567">인덱서 ([인덱서](classes.md#indexers)) 형식의 `T` 매개 변수 목록을 사용 하 여 `L`, 다음 시그니처만 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-567">For an indexer ([Indexers](classes.md#indexers)) of type `T` with parameter-list `L`, the following signatures are reserved:</span></span>
```csharp
T get_Item(L);
void set_Item(L, T value);
```

<span data-ttu-id="143b6-568">인덱서는 읽기 전용 또는 쓰기 전용일 경우에 서명은 모두 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-568">Both signatures are reserved, even if the indexer is read-only or write-only.</span></span>

<span data-ttu-id="143b6-569">또한 멤버 이름을 `Item` 예약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-569">Furthermore the member name `Item` is reserved.</span></span>

#### <a name="member-names-reserved-for-destructors"></a><span data-ttu-id="143b6-570">소멸자에 대 한 예약 된 멤버 이름</span><span class="sxs-lookup"><span data-stu-id="143b6-570">Member names reserved for destructors</span></span>

<span data-ttu-id="143b6-571">소멸자를 포함 하는 클래스에 대 한 ([소멸자](classes.md#destructors)), 다음과 같은 시그니처가 예약 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-571">For a class containing a destructor ([Destructors](classes.md#destructors)), the following signature is reserved:</span></span>
```csharp
void Finalize();
```

## <a name="constants"></a><span data-ttu-id="143b6-572">상수</span><span class="sxs-lookup"><span data-stu-id="143b6-572">Constants</span></span>

<span data-ttu-id="143b6-573">A ***상수*** 는 상수 값을 표현 하는 클래스 멤버: 컴파일 타임에 계산할 수 있는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-573">A ***constant*** is a class member that represents a constant value: a value that can be computed at compile-time.</span></span> <span data-ttu-id="143b6-574">A *constant_declaration* 지정 된 형식의 하나 이상의 상수를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-574">A *constant_declaration* introduces one or more constants of a given type.</span></span>

```antlr
constant_declaration
    : attributes? constant_modifier* 'const' type constant_declarators ';'
    ;

constant_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    ;

constant_declarators
    : constant_declarator (',' constant_declarator)*
    ;

constant_declarator
    : identifier '=' constant_expression
    ;
```

<span data-ttu-id="143b6-575">A *constant_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)), `new` 한정자 ([new 한정자](classes.md#the-new-modifier)), 유효한 조합 된 네 가지 액세스 한정자 ([액세스 한정자](classes.md#access-modifiers)).</span><span class="sxs-lookup"><span data-stu-id="143b6-575">A *constant_declaration* may include a set of *attributes* ([Attributes](attributes.md)), a `new` modifier ([The new modifier](classes.md#the-new-modifier)), and a valid combination of the four access modifiers ([Access modifiers](classes.md#access-modifiers)).</span></span> <span data-ttu-id="143b6-576">에 의해 선언 된 멤버의 모든 적용 된 특성 및 한정자를 *constant_declaration*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-576">The attributes and modifiers apply to all of the members declared by the *constant_declaration*.</span></span> <span data-ttu-id="143b6-577">상수 정적 멤버 라고 하는 경우에을 *constant_declaration* 필요 하거나 허용 하지는 `static` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-577">Even though constants are considered static members, a *constant_declaration* neither requires nor allows a `static` modifier.</span></span> <span data-ttu-id="143b6-578">상수 선언에 여러 번 표시 하는 동일한 한정자에 대 한 오류는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-578">It is an error for the same modifier to appear multiple times in a constant declaration.</span></span>

<span data-ttu-id="143b6-579">*형식* 의 한 *constant_declaration* 선언에 의해 정의 된 멤버의 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-579">The *type* of a *constant_declaration* specifies the type of the members introduced by the declaration.</span></span> <span data-ttu-id="143b6-580">형식 목록이 나옵니다 *constant_declarator*s, 각각 새 멤버를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-580">The type is followed by a list of *constant_declarator*s, each of which introduces a new member.</span></span> <span data-ttu-id="143b6-581">*constant_declarator* 이루어져는 *식별자* 뒤에 멤버 이름을 나타내는 "`=`" 토큰, 뒤에 *constant_expression* ([ 상수 식](expressions.md#constant-expressions)) 해당 멤버의 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-581">A *constant_declarator* consists of an *identifier* that names the member, followed by an "`=`" token, followed by a *constant_expression* ([Constant expressions](expressions.md#constant-expressions)) that gives the value of the member.</span></span>

<span data-ttu-id="143b6-582">*형식* 상수에 지정 된 선언 해야 `sbyte`, `byte`, `short`를 `ushort`, `int`, `uint`, `long`를 `ulong`, `char`, `float`, `double`, `decimal`, `bool`합니다 `string`, *enum_type*, 또는 *reference_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-582">The *type* specified in a constant declaration must be `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, `bool`, `string`, an *enum_type*, or a *reference_type*.</span></span> <span data-ttu-id="143b6-583">각 *constant_expression* 대상 형식 또는 암시적으로 변환 하 여 대상 형식으로 변환할 수 있는 형식의 값을 생성 해야 합니다 ([암시적 변환을](conversions.md#implicit-conversions)).</span><span class="sxs-lookup"><span data-stu-id="143b6-583">Each *constant_expression* must yield a value of the target type or of a type that can be converted to the target type by an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)).</span></span>

<span data-ttu-id="143b6-584">합니다 *형식* 상수의 해야 적어도 상수 자체 수준 만큼 액세스 가능 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="143b6-584">The *type* of a constant must be at least as accessible as the constant itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

<span data-ttu-id="143b6-585">상수 값을 사용 하는 식에서 가져올은 *simple_name* ([단순 이름](expressions.md#simple-names)) 또는 *member_access* ([멤버 액세스](expressions.md#member-access)).</span><span class="sxs-lookup"><span data-stu-id="143b6-585">The value of a constant is obtained in an expression using a *simple_name* ([Simple names](expressions.md#simple-names)) or a *member_access* ([Member access](expressions.md#member-access)).</span></span>

<span data-ttu-id="143b6-586">상수 자체에 참여할 수는 *constant_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-586">A constant can itself participate in a *constant_expression*.</span></span> <span data-ttu-id="143b6-587">따라서 필요한 모든 구문에는 상수를 사용할 수 있습니다는 *constant_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-587">Thus, a constant may be used in any construct that requires a *constant_expression*.</span></span> <span data-ttu-id="143b6-588">이러한 구문의 예로 `case` 레이블을 `goto case` 문을 `enum` 멤버 선언, 특성 및 기타 상수 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-588">Examples of such constructs include `case` labels, `goto case` statements, `enum` member declarations, attributes, and other constant declarations.</span></span>

<span data-ttu-id="143b6-589">에 설명 된 대로 [상수 식](expressions.md#constant-expressions), *constant_expression* 컴파일 시간에 완전히 계산 될 수 있는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-589">As described in [Constant expressions](expressions.md#constant-expressions), a *constant_expression* is an expression that can be fully evaluated at compile-time.</span></span> <span data-ttu-id="143b6-590">null이 아닌 값을 만들 수 있는 유일한 방법은 *reference_type* 이외의 `string` 적용 하는 것을 `new` 연산자 및 이후를 `new` 연산자를 사용할 수 없습니다는 *constant_ 식을*의 상수에 대 한 가능한 유일한 값 *reference_type*s 이외의 `string` 는 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-590">Since the only way to create a non-null value of a *reference_type* other than `string` is to apply the `new` operator, and since the `new` operator is not permitted in a *constant_expression*, the only possible value for constants of *reference_type*s other than `string` is `null`.</span></span>

<span data-ttu-id="143b6-591">상수 값에 대 한 기호화 된 이름, 필요한 경우 하지만 때 해당 값의 형식은 상수 선언에서 허용 되지 않습니다 또는 의해 컴파일 시간에 값을 계산할 수 없는 경우는 *constant_expression*, `readonly` (필드 [읽기 전용 필드](classes.md#readonly-fields)) 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-591">When a symbolic name for a constant value is desired, but when the type of that value is not permitted in a constant declaration, or when the value cannot be computed at compile-time by a *constant_expression*, a `readonly` field ([Readonly fields](classes.md#readonly-fields)) may be used instead.</span></span>

<span data-ttu-id="143b6-592">여러 상수를 선언 하는 상수 선언 동일한 특성, 한정자 및 형식을 사용 하 여 단일 상수 여러 번 선언 하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-592">A constant declaration that declares multiple constants is equivalent to multiple declarations of single constants with the same attributes, modifiers, and type.</span></span> <span data-ttu-id="143b6-593">예</span><span class="sxs-lookup"><span data-stu-id="143b6-593">For example</span></span>
```csharp
class A
{
    public const double X = 1.0, Y = 2.0, Z = 3.0;
}
```
<span data-ttu-id="143b6-594">위의 식은 아래의 식과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-594">is equivalent to</span></span>
```csharp
class A
{
    public const double X = 1.0;
    public const double Y = 2.0;
    public const double Z = 3.0;
}
```

<span data-ttu-id="143b6-595">상수는 순환적 종속성 없는으로 동일한 프로그램 안에 다른 상수에 따라 달라 지도록 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-595">Constants are permitted to depend on other constants within the same program as long as the dependencies are not of a circular nature.</span></span> <span data-ttu-id="143b6-596">컴파일러는 자동으로 적절 한 순서로 상수 선언 평가를 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-596">The compiler automatically arranges to evaluate the constant declarations in the appropriate order.</span></span> <span data-ttu-id="143b6-597">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-597">In the example</span></span>
```csharp
class A
{
    public const int X = B.Z + 1;
    public const int Y = 10;
}

class B
{
    public const int Z = A.Y + 1;
}
```
<span data-ttu-id="143b6-598">컴파일러는 먼저 계산 `A.Y`, 그런 다음 계산 `B.Z`, 마지막으로 평가 하 고 `A.X`, 값을 생성 `10`, `11`, 및 `12`.</span><span class="sxs-lookup"><span data-stu-id="143b6-598">the compiler first evaluates `A.Y`, then evaluates `B.Z`, and finally evaluates `A.X`, producing the values `10`, `11`, and `12`.</span></span> <span data-ttu-id="143b6-599">상수 선언 다른 프로그램에서 상수에 따라 달라질 수 있습니다 되지만 이러한 종속성 단방향에서 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-599">Constant declarations may depend on constants from other programs, but such dependencies are only possible in one direction.</span></span> <span data-ttu-id="143b6-600">경우 위 예제를 참조 `A` 및 `B` 선언 된 별도 프로그램의 수에 대 한 `A.X` 에 따라 달라 지도록 `B.Z`, 하지만 `B.Z` 동시에 종속 다음 수 `A.Y`.</span><span class="sxs-lookup"><span data-stu-id="143b6-600">Referring to the example above, if `A` and `B` were declared in separate programs, it would be possible for `A.X` to depend on `B.Z`, but `B.Z` could then not simultaneously depend on `A.Y`.</span></span>

## <a name="fields"></a><span data-ttu-id="143b6-601">필드</span><span class="sxs-lookup"><span data-stu-id="143b6-601">Fields</span></span>

<span data-ttu-id="143b6-602">A ***필드*** 개체 또는 클래스와 연결 된 변수를 나타내는 멤버가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-602">A ***field*** is a member that represents a variable associated with an object or class.</span></span> <span data-ttu-id="143b6-603">A *field_declaration* 지정 된 형식의 하나 이상의 필드를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-603">A *field_declaration* introduces one or more fields of a given type.</span></span>

```antlr
field_declaration
    : attributes? field_modifier* type variable_declarators ';'
    ;

field_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'static'
    | 'readonly'
    | 'volatile'
    | field_modifier_unsafe
    ;

variable_declarators
    : variable_declarator (',' variable_declarator)*
    ;

variable_declarator
    : identifier ('=' variable_initializer)?
    ;

variable_initializer
    : expression
    | array_initializer
    ;
```

<span data-ttu-id="143b6-604">A *field_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)), `new` 한정자 ([new 한정자](classes.md#the-new-modifier)), 유효한 조합 된 네 가지 액세스 한정자 ([액세스 한정자](classes.md#access-modifiers)), 및 `static` 한정자 ([정적 및 인스턴스 필드](classes.md#static-and-instance-fields)).</span><span class="sxs-lookup"><span data-stu-id="143b6-604">A *field_declaration* may include a set of *attributes* ([Attributes](attributes.md)), a `new` modifier ([The new modifier](classes.md#the-new-modifier)), a valid combination of the four access modifiers ([Access modifiers](classes.md#access-modifiers)), and a `static` modifier ([Static and instance fields](classes.md#static-and-instance-fields)).</span></span> <span data-ttu-id="143b6-605">또한를 *field_declaration* 포함 될 수 있습니다는 `readonly` 한정자 ([읽기 전용 필드](classes.md#readonly-fields)) 또는 `volatile` 한정자 ([Volatile 필드](classes.md#volatile-fields)) 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-605">In addition, a *field_declaration* may include a `readonly` modifier ([Readonly fields](classes.md#readonly-fields)) or a `volatile` modifier ([Volatile fields](classes.md#volatile-fields)) but not both.</span></span> <span data-ttu-id="143b6-606">에 의해 선언 된 멤버의 모든 적용 된 특성 및 한정자를 *field_declaration*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-606">The attributes and modifiers apply to all of the members declared by the *field_declaration*.</span></span> <span data-ttu-id="143b6-607">해당 필드 선언에 여러 번 표시 하는 동일한 한정자에 대 한 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-607">It is an error for the same modifier to appear multiple times in a field declaration.</span></span>

<span data-ttu-id="143b6-608">*형식* 의 한 *field_declaration* 선언에 의해 정의 된 멤버의 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-608">The *type* of a *field_declaration* specifies the type of the members introduced by the declaration.</span></span> <span data-ttu-id="143b6-609">형식 목록이 나옵니다 *variable_declarator*s, 각각 새 멤버를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-609">The type is followed by a list of *variable_declarator*s, each of which introduces a new member.</span></span> <span data-ttu-id="143b6-610">*variable_declarator* 이루어져 있습니다를 *식별자* 뒤에 선택적으로 해당 멤버에 이름을 지정 하는 "`=`" 토큰으로 *variable_initializer* ([ 변수 이니셜라이저](classes.md#variable-initializers)) 해당 멤버의 초기 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-610">A *variable_declarator* consists of an *identifier* that names that member, optionally followed by an "`=`" token and a *variable_initializer* ([Variable initializers](classes.md#variable-initializers)) that gives the initial value of that member.</span></span>

<span data-ttu-id="143b6-611">합니다 *형식* 필드의 해야 적어도 필드 자체 만큼 액세스 가능 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="143b6-611">The *type* of a field must be at least as accessible as the field itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

<span data-ttu-id="143b6-612">사용 하는 식에서 가져올 필드의 값을 *simple_name* ([단순 이름](expressions.md#simple-names)) 또는 *member_access* ([멤버 액세스](expressions.md#member-access)).</span><span class="sxs-lookup"><span data-stu-id="143b6-612">The value of a field is obtained in an expression using a *simple_name* ([Simple names](expressions.md#simple-names)) or a *member_access* ([Member access](expressions.md#member-access)).</span></span> <span data-ttu-id="143b6-613">사용 하 여 읽기 전용이 아닌 필드의 값은 수정 된 *할당* ([대입 연산자](expressions.md#assignment-operators)).</span><span class="sxs-lookup"><span data-stu-id="143b6-613">The value of a non-readonly field is modified using an *assignment* ([Assignment operators](expressions.md#assignment-operators)).</span></span> <span data-ttu-id="143b6-614">읽기 전용이 아닌 필드의 값은 후 위 증가 및 감소 연산자를 모두 가져와 사용 하 여 수정할 수 있습니다 ([후 위 증가 및 감소 연산자](expressions.md#postfix-increment-and-decrement-operators)) 전위 증가 및 감소 연산자 ([접두사 증가 및 감소 연산자](expressions.md#prefix-increment-and-decrement-operators)).</span><span class="sxs-lookup"><span data-stu-id="143b6-614">The value of a non-readonly field can be both obtained and modified using postfix increment and decrement operators ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators)) and prefix increment and decrement operators ([Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)).</span></span>

<span data-ttu-id="143b6-615">여러 필드를 선언 하는 필드 선언은 동일한 특성, 한정자 및 형식을 사용 하 여 단일 필드의 여러 선언 하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-615">A field declaration that declares multiple fields is equivalent to multiple declarations of single fields with the same attributes, modifiers, and type.</span></span> <span data-ttu-id="143b6-616">예</span><span class="sxs-lookup"><span data-stu-id="143b6-616">For example</span></span>
```csharp
class A
{
    public static int X = 1, Y, Z = 100;
}
```
<span data-ttu-id="143b6-617">위의 식은 아래의 식과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-617">is equivalent to</span></span>
```csharp
class A
{
    public static int X = 1;
    public static int Y;
    public static int Z = 100;
}
```

### <a name="static-and-instance-fields"></a><span data-ttu-id="143b6-618">정적 및 인스턴스 필드</span><span class="sxs-lookup"><span data-stu-id="143b6-618">Static and instance fields</span></span>

<span data-ttu-id="143b6-619">필드 선언 포함 되는 경우는 `static` 한정자를 선언에 의해 도입 된 필드는 ***정적 필드***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-619">When a field declaration includes a `static` modifier, the fields introduced by the declaration are ***static fields***.</span></span> <span data-ttu-id="143b6-620">없는 경우 `static` 한정자가 있는 선언에 의해 도입 된 필드는 ***인스턴스 필드***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-620">When no `static` modifier is present, the fields introduced by the declaration are ***instance fields***.</span></span> <span data-ttu-id="143b6-621">정적 필드 및 인스턴스 필드는 두 일부의 변수 ([변수](variables.md)) C#에서 지원 되며 때때로 이러한 라고 ***정적 변수*** 및 ***인스턴스 변수*** , 각각.</span><span class="sxs-lookup"><span data-stu-id="143b6-621">Static fields and instance fields are two of the several kinds of variables ([Variables](variables.md)) supported by C#, and at times they are referred to as ***static variables*** and ***instance variables***, respectively.</span></span>

<span data-ttu-id="143b6-622">정적 필드는 특정 인스턴스에;의 일부가 아닙니다. 닫힌 형식의 모든 인스턴스 간에 공유 되는 대신 ([열기 및 닫힌 형식을](types.md#open-and-closed-types)).</span><span class="sxs-lookup"><span data-stu-id="143b6-622">A static field is not part of a specific instance; instead, it is shared amongst all instances of a closed type ([Open and closed types](types.md#open-and-closed-types)).</span></span> <span data-ttu-id="143b6-623">닫힌된 클래스 유형 인스턴스 개수를 생성 없이 연결 된 응용 프로그램 도메인에 대 한 정적 필드의 사본 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-623">No matter how many instances of a closed class type are created, there is only ever one copy of a static field for the associated application domain.</span></span>

<span data-ttu-id="143b6-624">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="143b6-624">For example:</span></span>
```csharp
class C<V>
{
    static int count = 0;

    public C() {
        count++;
    }

    public static int Count {
        get { return count; }
    }
}

class Application
{
    static void Main() {
        C<int> x1 = new C<int>();
        Console.WriteLine(C<int>.Count);        // Prints 1

        C<double> x2 = new C<double>();
        Console.WriteLine(C<int>.Count);        // Prints 1

        C<int> x3 = new C<int>();
        Console.WriteLine(C<int>.Count);        // Prints 2
    }
}
```

<span data-ttu-id="143b6-625">인스턴스 필드 인스턴스에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-625">An instance field belongs to an instance.</span></span> <span data-ttu-id="143b6-626">특히 클래스의 모든 인스턴스는 해당 클래스의 모든 인스턴스 필드는 별도 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-626">Specifically, every instance of a class contains a separate set of all the instance fields of that class.</span></span>

<span data-ttu-id="143b6-627">필드에서 참조 하는 경우는 *member_access* ([멤버 액세스](expressions.md#member-access)) 형식의 `E.M`이면 `M` 은 정적 필드 `E` 포함 하는 형식 표시 해야 합니다 `M` 경우에 `M` 인스턴스 필드, E를 포함 하는 형식 인스턴스의 나타내야 `M`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-627">When a field is referenced in a *member_access* ([Member access](expressions.md#member-access)) of the form `E.M`, if `M` is a static field, `E` must denote a type containing `M`, and if `M` is an instance field, E must denote an instance of a type containing `M`.</span></span>

<span data-ttu-id="143b6-628">정적 간의 차이점 및 인스턴스 멤버 설명에 대 한 자세한 [정적 및 인스턴스 멤버](classes.md#static-and-instance-members)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-628">The differences between static and instance members are discussed further in [Static and instance members](classes.md#static-and-instance-members).</span></span>

### <a name="readonly-fields"></a><span data-ttu-id="143b6-629">읽기 전용 필드</span><span class="sxs-lookup"><span data-stu-id="143b6-629">Readonly fields</span></span>

<span data-ttu-id="143b6-630">경우는 *field_declaration* 포함을 `readonly` 한정자를 선언에 의해 도입 된 필드는 ***읽기 전용 필드***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-630">When a *field_declaration* includes a `readonly` modifier, the fields introduced by the declaration are ***readonly fields***.</span></span> <span data-ttu-id="143b6-631">읽기 전용 필드에 직접 할당의 일부로 해당 선언 또는 인스턴스 생성자 또는 동일한 클래스의 정적 생성자 에서만 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-631">Direct assignments to readonly fields can only occur as part of that declaration or in an instance constructor or static constructor in the same class.</span></span> <span data-ttu-id="143b6-632">(읽기 전용 필드는 할당할 수 있습니다를 여러 번 이러한 컨텍스트에서.) 특히, 직접 할당 하는 `readonly` 필드는 다음 경우에 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-632">(A readonly field can be assigned to multiple times in these contexts.) Specifically, direct assignments to a `readonly` field are permitted only in the following contexts:</span></span>

*  <span data-ttu-id="143b6-633">에 *variable_declarator* 필드를 도입 하는 (포함 하 여를 *variable_initializer* 선언에서).</span><span class="sxs-lookup"><span data-stu-id="143b6-633">In the *variable_declarator* that introduces the field (by including a *variable_initializer* in the declaration).</span></span>
*  <span data-ttu-id="143b6-634">필드 선언;를 포함 하는 클래스의 인스턴스 생성자에는 인스턴스 필드 에 대 한 필드 선언을 포함 하는 클래스의 정적 생성자에서 정적 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-634">For an instance field, in the instance constructors of the class that contains the field declaration; for a static field, in the static constructor of the class that contains the field declaration.</span></span> <span data-ttu-id="143b6-635">이러한 경우는 전달할 수만 컨텍스트를 `readonly` 필드를 `out` 또는 `ref` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-635">These are also the only contexts in which it is valid to pass a `readonly` field as an `out` or `ref` parameter.</span></span>

<span data-ttu-id="143b6-636">에 할당 하는 `readonly` 필드 또는 변수로 전달를 `out` 또는 `ref` 다른 컨텍스트에서 매개 변수는 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-636">Attempting to assign to a `readonly` field or pass it as an `out` or `ref` parameter in any other context is a compile-time error.</span></span>

#### <a name="using-static-readonly-fields-for-constants"></a><span data-ttu-id="143b6-637">상수에 대 한 정적 읽기 전용 필드를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="143b6-637">Using static readonly fields for constants</span></span>

<span data-ttu-id="143b6-638">`static readonly` 경우 상수 값에 대 한 기호화 된 이름이 필요 하지만 값의 형식에서 허용 되지 않습니다 때 필드 유용 합니다.는 `const` 선언 또는 경우 컴파일 타임에 값을 계산할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-638">A `static readonly` field is useful when a symbolic name for a constant value is desired, but when the type of the value is not permitted in a `const` declaration, or when the value cannot be computed at compile-time.</span></span> <span data-ttu-id="143b6-639">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-639">In the example</span></span>
```csharp
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);

    private byte red, green, blue;

    public Color(byte r, byte g, byte b) {
        red = r;
        green = g;
        blue = b;
    }
}
```
<span data-ttu-id="143b6-640">`Black`, `White`, `Red`, `Green`, 및 `Blue` 으로 멤버를 선언할 수 없습니다 `const` 멤버 하므로 컴파일 타임에 해당 값을 계산할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-640">the `Black`, `White`, `Red`, `Green`, and `Blue` members cannot be declared as `const` members because their values cannot be computed at compile-time.</span></span> <span data-ttu-id="143b6-641">그러나 선언 `static readonly` 대신 훨씬 같은 효과가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-641">However, declaring them `static readonly` instead has much the same effect.</span></span>

#### <a name="versioning-of-constants-and-static-readonly-fields"></a><span data-ttu-id="143b6-642">상수 및 정적 읽기 전용 필드의 버전 관리</span><span class="sxs-lookup"><span data-stu-id="143b6-642">Versioning of constants and static readonly fields</span></span>

<span data-ttu-id="143b6-643">상수 및 읽기 전용 필드 의미 체계가 서로 다른 이진 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-643">Constants and readonly fields have different binary versioning semantics.</span></span> <span data-ttu-id="143b6-644">컴파일 타임에 상수 값을 가져오는 식에서 상수를 참조할 때 있지만 필드의 값 식에서 읽기 전용 필드를 참조 하는 경우 실행 시간까지 가져오지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-644">When an expression references a constant, the value of the constant is obtained at compile-time, but when an expression references a readonly field, the value of the field is not obtained until run-time.</span></span> <span data-ttu-id="143b6-645">별개의 두 프로그램으로 구성 된 응용 프로그램을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-645">Consider an application that consists of two separate programs:</span></span>
```csharp
using System;

namespace Program1
{
    public class Utils
    {
        public static readonly int X = 1;
    }
}

namespace Program2
{
    class Test
    {
        static void Main() {
            Console.WriteLine(Program1.Utils.X);
        }
    }
}
```

<span data-ttu-id="143b6-646">합니다 `Program1` 고 `Program2` 네임 스페이스 별도로 컴파일된 두 프로그램을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-646">The `Program1` and `Program2` namespaces denote two programs that are compiled separately.</span></span> <span data-ttu-id="143b6-647">때문에 `Program1.Utils.X` 정적 읽기 전용 필드에서 출력 값으로 선언 되는 `Console.WriteLine` 문은 컴파일 타임에 알려지지 않은 하지만 런타임 시 가져온 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-647">Because `Program1.Utils.X` is declared as a static readonly field, the value output by the `Console.WriteLine` statement is not known at compile-time, but rather is obtained at run-time.</span></span> <span data-ttu-id="143b6-648">따라서 경우 값 `X` 변경 및 `Program1` 를 다시 컴파일하면를 `Console.WriteLine` 문의 경우 새 값에도 출력 `Program2` 다시 컴파일할 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-648">Thus, if the value of `X` is changed and `Program1` is recompiled, the `Console.WriteLine` statement will output the new value even if `Program2` isn't recompiled.</span></span> <span data-ttu-id="143b6-649">그러나 때로는 `X` 된 상수, 값 `X` 얻은 시 `Program2` 컴파일된, 및 변경의 영향을 받지 않은 상태로 유지 됩니다 `Program1` 될 때까지 `Program2` 다시 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-649">However, had `X` been a constant, the value of `X` would have been obtained at the time `Program2` was compiled, and would remain unaffected by changes in `Program1` until `Program2` is recompiled.</span></span>

### <a name="volatile-fields"></a><span data-ttu-id="143b6-650">Volatile 필드</span><span class="sxs-lookup"><span data-stu-id="143b6-650">Volatile fields</span></span>

<span data-ttu-id="143b6-651">경우는 *field_declaration* 포함을 `volatile` 한정자는 선언에서 정의한 필드는 ***volatile 필드***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-651">When a *field_declaration* includes a `volatile` modifier, the fields introduced by that declaration are ***volatile fields***.</span></span>

<span data-ttu-id="143b6-652">비 volatile 필드에 대 한 명령을 다시 정렬할 수 있는 최적화 방법에서 제공 하는 동기화 되지 않은 필드에 액세스 하는 다중 스레드 프로그램에서 예기치 않은 및 예기치 않은 결과가 발생할 수 있습니다는 *lock_statement*  ([Lock 문에](statements.md#the-lock-statement)).</span><span class="sxs-lookup"><span data-stu-id="143b6-652">For non-volatile fields, optimization techniques that reorder instructions can lead to unexpected and unpredictable results in multi-threaded programs that access fields without synchronization such as that provided by the *lock_statement* ([The lock statement](statements.md#the-lock-statement)).</span></span> <span data-ttu-id="143b6-653">컴파일러, 런타임 시스템 또는 하드웨어에서 이러한 최적화를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-653">These optimizations can be performed by the compiler, by the run-time system, or by hardware.</span></span> <span data-ttu-id="143b6-654">Volatile 필드에 대 한 이러한 다시 정렬 하는 최적화 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-654">For volatile fields, such reordering optimizations are restricted:</span></span>

*  <span data-ttu-id="143b6-655">Volatile 필드의 읽기 호출 되는 ***volatile 읽기***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-655">A read of a volatile field is called a ***volatile read***.</span></span> <span data-ttu-id="143b6-656">Volatile 읽기는 "acquire 의미 체계"; 즉, 반드시 후 명령 시퀀스에서 발생 하는 메모리에 대 한 참조 하기 전에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-656">A volatile read has "acquire semantics"; that is, it is guaranteed to occur prior to any references to memory that occur after it in the instruction sequence.</span></span>
*  <span data-ttu-id="143b6-657">Volatile 필드 쓰기 호출 되는 ***volatile 쓰기***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-657">A write of a volatile field is called a ***volatile write***.</span></span> <span data-ttu-id="143b6-658">Volatile 쓰기에 "release 의미 체계"; 즉, 반드시는 메모리 참조는 명령 시퀀스의 쓰기 명령 전에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-658">A volatile write has "release semantics"; that is, it is guaranteed to happen after any memory references prior to the write instruction in the instruction sequence.</span></span>

<span data-ttu-id="143b6-659">이러한 제한 사항은 모든 스레드가 수행된 순서대로 다른 스레드가 휘발성 쓰기를 수행하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-659">These restrictions ensure that all threads will observe volatile writes performed by any other thread in the order in which they were performed.</span></span> <span data-ttu-id="143b6-660">표준에 맞는 구현은 단일 총의 순서를 실행 하는 모든 스레드 표시 된 volatile 쓰기 제공할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-660">A conforming implementation is not required to provide a single total ordering of volatile writes as seen from all threads of execution.</span></span> <span data-ttu-id="143b6-661">Volatile 필드의 형식은 다음 중 하나 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-661">The type of a volatile field must be one of the following:</span></span>

*  <span data-ttu-id="143b6-662">A *reference_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-662">A *reference_type*.</span></span>
*  <span data-ttu-id="143b6-663">형식 `byte`, `sbyte`, `short`, `ushort`, `int`를 `uint`, `char`, `float`, `bool`를 `System.IntPtr`, 또는` System.UIntPtr`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-663">The type `byte`, `sbyte`, `short`, `ushort`, `int`, `uint`, `char`, `float`, `bool`, `System.IntPtr`, or` System.UIntPtr`.</span></span>
*  <span data-ttu-id="143b6-664">*enum_type* 열거형의 기본 형식을 `byte`, `sbyte`를 `short`를 `ushort`, `int`, 또는 `uint`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-664">An *enum_type* having an enum base type of `byte`, `sbyte`, `short`, `ushort`, `int`, or `uint`.</span></span>

<span data-ttu-id="143b6-665">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-665">The example</span></span>
```csharp
using System;
using System.Threading;

class Test
{
    public static int result;   
    public static volatile bool finished;

    static void Thread2() {
        result = 143;    
        finished = true; 
    }

    static void Main() {
        finished = false;

        // Run Thread2() in a new thread
        new Thread(new ThreadStart(Thread2)).Start();

        // Wait for Thread2 to signal that it has a result by setting
        // finished to true.
        for (;;) {
            if (finished) {
                Console.WriteLine("result = {0}", result);
                return;
            }
        }
    }
}
```
<span data-ttu-id="143b6-666">다음 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-666">produces the output:</span></span>
```
result = 143
```

<span data-ttu-id="143b6-667">이 예제에서는 메서드 `Main` 메서드를 실행 하는 새 스레드 시작 `Thread2`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-667">In this example, the method `Main` starts a new thread that runs the method `Thread2`.</span></span> <span data-ttu-id="143b6-668">이 메서드는 호출 비 volatile 필드에 값을 저장 `result`를 저장 한 다음 `true` volatile 필드에 `finished`입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-668">This method stores a value into a non-volatile field called `result`, then stores `true` in the volatile field `finished`.</span></span> <span data-ttu-id="143b6-669">필드에 대 한 주 스레드가 대기 `finished` 로 설정 해야 `true`, 다음 필드를 읽고 `result`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-669">The main thread waits for the field `finished` to be set to `true`, then reads the field `result`.</span></span> <span data-ttu-id="143b6-670">이후 `finished` 선언한 `volatile`, main 메서드가 값을 읽어야 합니다. `143` 필드에서 `result`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-670">Since `finished` has been declared `volatile`, the main thread must read the value `143` from the field `result`.</span></span> <span data-ttu-id="143b6-671">경우 필드 `finished` 가 선언 되지 `volatile`를 저장소에 대 한 허용 될 `result` 저장소 후 주 스레드를 표시 하도록 `finished`, 및 값을 읽을 수 주 스레드에 대 한 `0` 에서 필드 `result`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-671">If the field `finished` had not been declared `volatile`, then it would be permissible for the store to `result` to be visible to the main thread after the store to `finished`, and hence for the main thread to read the value `0` from the field `result`.</span></span> <span data-ttu-id="143b6-672">선언 `finished` 으로 `volatile` 필드는 이러한 불일치를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-672">Declaring `finished` as a `volatile` field prevents any such inconsistency.</span></span>

### <a name="field-initialization"></a><span data-ttu-id="143b6-673">필드 초기화</span><span class="sxs-lookup"><span data-stu-id="143b6-673">Field initialization</span></span>

<span data-ttu-id="143b6-674">초기 값 필드의 정적 필드 또는 인스턴스 필드의 경우 든은 기본값 ([기본값](variables.md#default-values)) 필드의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-674">The initial value of a field, whether it be a static field or an instance field, is the default value ([Default values](variables.md#default-values)) of the field's type.</span></span> <span data-ttu-id="143b6-675">이 기본 초기화 발생 하 고 따라서 필드는 "초기화 되지 않은" 되지 전에 필드의 값을 관찰 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-675">It is not possible to observe the value of a field before this default initialization has occurred, and a field is thus never "uninitialized".</span></span> <span data-ttu-id="143b6-676">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-676">The example</span></span>
```csharp
using System;

class Test
{
    static bool b;
    int i;

    static void Main() {
        Test t = new Test();
        Console.WriteLine("b = {0}, i = {1}", b, t.i);
    }
}
```
<span data-ttu-id="143b6-677">는 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-677">produces the output</span></span>
```
b = False, i = 0
```
<span data-ttu-id="143b6-678">때문에 `b` 고 `i` 는 모두 자동으로 기본값으로 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-678">because `b` and `i` are both automatically initialized to default values.</span></span>

### <a name="variable-initializers"></a><span data-ttu-id="143b6-679">변수 이니셜라이저</span><span class="sxs-lookup"><span data-stu-id="143b6-679">Variable initializers</span></span>

<span data-ttu-id="143b6-680">필드 선언이 포함 될 수 있습니다 *variable_initializer*s입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-680">Field declarations may include *variable_initializer*s.</span></span> <span data-ttu-id="143b6-681">정적 필드에 대 한 변수 이니셜라이저 클래스 초기화 하는 동안 실행 되는 대입문에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-681">For static fields, variable initializers correspond to assignment statements that are executed during class initialization.</span></span> <span data-ttu-id="143b6-682">예를 들어 필드를 변수 이니셜라이저 해당 클래스의 인스턴스를 만들 때 실행 되는 대입문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-682">For instance fields, variable initializers correspond to assignment statements that are executed when an instance of the class is created.</span></span>

<span data-ttu-id="143b6-683">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-683">The example</span></span>
```csharp
using System;

class Test
{
    static double x = Math.Sqrt(2.0);
    int i = 100;
    string s = "Hello";

    static void Main() {
        Test a = new Test();
        Console.WriteLine("x = {0}, i = {1}, s = {2}", x, a.i, a.s);
    }
}
```
<span data-ttu-id="143b6-684">는 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-684">produces the output</span></span>
```
x = 1.4142135623731, i = 100, s = Hello
```
<span data-ttu-id="143b6-685">때문에 할당할 `x` 발생 할당 및 정적 필드 이니셜라이저를 실행할 때 `i` 및 `s` 인스턴스 필드 이니셜라이저를 실행할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-685">because an assignment to `x` occurs when static field initializers execute and assignments to `i` and `s` occur when the instance field initializers execute.</span></span>

<span data-ttu-id="143b6-686">에 설명 된 기본 값 초기화 [필드 초기화](classes.md#field-initialization) 변수 이니셜라이저는 필드를 포함 하 고 모든 필드에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-686">The default value initialization described in [Field initialization](classes.md#field-initialization) occurs for all fields, including fields that have variable initializers.</span></span> <span data-ttu-id="143b6-687">따라서 클래스 초기화 될 때 해당 클래스의 모든 정적 필드는 기본값으로, 먼저 초기화 하 고 후 정적 필드 이니셜라이저 텍스트 순서 대로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-687">Thus, when a class is initialized, all static fields in that class are first initialized to their default values, and then the static field initializers are executed in textual order.</span></span> <span data-ttu-id="143b6-688">마찬가지로 클래스의 인스턴스를 만들 때 먼저 해당 인스턴스에 있는 모든 인스턴스 필드가 해당 기본값으로 초기화 됩니다 및 인스턴스 필드 이니셜라이저 텍스트 순서 대로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-688">Likewise, when an instance of a class is created, all instance fields in that instance are first initialized to their default values, and then the instance field initializers are executed in textual order.</span></span>

<span data-ttu-id="143b6-689">기본값 상태로 사용 되는 변수 이니셜라이저를 사용 하 여 정적 필드에 대 한 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-689">It is possible for static fields with variable initializers to be observed in their default value state.</span></span> <span data-ttu-id="143b6-690">그러나이 스타일의 문제로 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-690">However, this is strongly discouraged as a matter of style.</span></span> <span data-ttu-id="143b6-691">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-691">The example</span></span>
```csharp
using System;

class Test
{
    static int a = b + 1;
    static int b = a + 1;

    static void Main() {
        Console.WriteLine("a = {0}, b = {1}", a, b);
    }
}
```
<span data-ttu-id="143b6-692">이러한 동작을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-692">exhibits this behavior.</span></span> <span data-ttu-id="143b6-693">순환 정의도 불구 하 고는 되며 b는 프로그램은 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-693">Despite the circular definitions of a and b, the program is valid.</span></span> <span data-ttu-id="143b6-694">그 결과 출력</span><span class="sxs-lookup"><span data-stu-id="143b6-694">It results in the output</span></span>
```
a = 1, b = 2
```
<span data-ttu-id="143b6-695">때문에 정적 필드를 `a` 하 고 `b` 으로 초기화 됩니다 `0` (의 기본값 `int`) 해당 이니셜라이저가 실행 되기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-695">because the static fields `a` and `b` are initialized to `0` (the default value for `int`) before their initializers are executed.</span></span> <span data-ttu-id="143b6-696">경우에 대 한 이니셜라이저 `a` 를 실행 하 고 값 `b` 가 0 이면 등 `a` 으로 초기화 됩니다 `1`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-696">When the initializer for `a` runs, the value of `b` is zero, and so `a` is initialized to `1`.</span></span> <span data-ttu-id="143b6-697">경우에 대 한 이니셜라이저 `b` 를 실행 하 고 값 `a` 이미 `1`, 등 `b` 초기화 됩니다 `2`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-697">When the initializer for `b` runs, the value of `a` is already `1`, and so `b` is initialized to `2`.</span></span>

#### <a name="static-field-initialization"></a><span data-ttu-id="143b6-698">정적 필드 초기화</span><span class="sxs-lookup"><span data-stu-id="143b6-698">Static field initialization</span></span>

<span data-ttu-id="143b6-699">클래스의 정적 필드 변수 이니셜라이저 할당의 클래스 선언에 나타나는 텍스트 순서 대로 실행 되는 시퀀스에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-699">The static field variable initializers of a class correspond to a sequence of assignments that are executed in the textual order in which they appear in the class declaration.</span></span> <span data-ttu-id="143b6-700">경우 정적 생성자 ([정적 생성자](classes.md#static-constructors))가 클래스의 정적 필드 이니셜라이저는 실행 정적 생성자를 실행 하기 전에 즉시 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-700">If a static constructor ([Static constructors](classes.md#static-constructors)) exists in the class, execution of the static field initializers occurs immediately prior to executing that static constructor.</span></span> <span data-ttu-id="143b6-701">그렇지 않은 경우 정적 필드 이니셜라이저를 해당 클래스의 정적 필드의 첫 번째 사용 하기 전에 구현에 따라 다릅니다 시간에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-701">Otherwise, the static field initializers are executed at an implementation-dependent time prior to the first use of a static field of that class.</span></span> <span data-ttu-id="143b6-702">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-702">The example</span></span>
```csharp
using System;

class Test 
{ 
    static void Main() {
        Console.WriteLine("{0} {1}", B.Y, A.X);
    }

    public static int F(string s) {
        Console.WriteLine(s);
        return 1;
    }
}

class A
{
    public static int X = Test.F("Init A");
}

class B
{
    public static int Y = Test.F("Init B");
}
```
<span data-ttu-id="143b6-703">두 출력을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-703">might produce either the output:</span></span>
```
Init A
Init B
1 1
```
<span data-ttu-id="143b6-704">또는 출력을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-704">or the output:</span></span>
```
Init B
Init A
1 1
```
<span data-ttu-id="143b6-705">때문에 실행 `X`의 이니셜라이저 및 `Y`의 이니셜라이저는 어떤 순서로 든 발생할 수 있습니다; 그리고 해당 필드에 대 한 참조 앞에 오는 제한만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-705">because the execution of `X`'s initializer and `Y`'s initializer could occur in either order; they are only constrained to occur before the references to those fields.</span></span> <span data-ttu-id="143b6-706">그러나 예제의:</span><span class="sxs-lookup"><span data-stu-id="143b6-706">However, in the example:</span></span>
```csharp
using System;

class Test
{
    static void Main() {
        Console.WriteLine("{0} {1}", B.Y, A.X);
    }

    public static int F(string s) {
        Console.WriteLine(s);
        return 1;
    }
}

class A
{
    static A() {}

    public static int X = Test.F("Init A");
}

class B
{
    static B() {}

    public static int Y = Test.F("Init B");
}
```
<span data-ttu-id="143b6-707">출력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-707">the output must be:</span></span>
```
Init B
Init A
1 1
```
<span data-ttu-id="143b6-708">때문에 정적 생성자가 실행 하는 시기에 대 한 규칙 (에 정의 된 대로 [정적 생성자](classes.md#static-constructors))를 제공 `B`의 정적 생성자 (및 따라서 `B`의 정적 필드 이니셜라이저) 보다먼저실행해야`A`의 정적 생성자 및 필드 이니셜라이저입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-708">because the rules for when static constructors execute (as defined in [Static constructors](classes.md#static-constructors)) provide that `B`'s static constructor (and hence `B`'s static field initializers) must run before `A`'s static constructor and field initializers.</span></span>

#### <a name="instance-field-initialization"></a><span data-ttu-id="143b6-709">인스턴스 필드 초기화</span><span class="sxs-lookup"><span data-stu-id="143b6-709">Instance field initialization</span></span>

<span data-ttu-id="143b6-710">인스턴스 생성자 중 하나에 진입할 때 즉시 실행 되는 할당의 시퀀스에 해당 하는 클래스의 인스턴스 필드 변수 이니셜라이저 ([생성자 이니셜라이저](classes.md#constructor-initializers))는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-710">The instance field variable initializers of a class correspond to a sequence of assignments that are executed immediately upon entry to any one of the instance constructors ([Constructor initializers](classes.md#constructor-initializers)) of that class.</span></span> <span data-ttu-id="143b6-711">변수 이니셜라이저는 클래스 선언에 나타나는 텍스트 순서 대로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-711">The variable initializers are executed in the textual order in which they appear in the class declaration.</span></span> <span data-ttu-id="143b6-712">클래스 인스턴스 만들기 및 초기화 프로세스에서 자세히 설명 되어 [인스턴스 생성자](classes.md#instance-constructors)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-712">The class instance creation and initialization process is described further in [Instance constructors](classes.md#instance-constructors).</span></span>

<span data-ttu-id="143b6-713">인스턴스 필드에 대 한 변수 이니셜라이저에서 예외는 생성 되는 인스턴스를 참조할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-713">A variable initializer for an instance field cannot reference the instance being created.</span></span> <span data-ttu-id="143b6-714">컴파일 타임 오류를 참조 하는 것이 따라서 `this` 변수 이니셜라이저에서 예외를 그대로를 통해 인스턴스 멤버를 참조 변수 이니셜라이저에서 예외에 대 한 컴파일 시간 오류를 *simple_name*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-714">Thus, it is a compile-time error to reference `this` in a variable initializer, as it is a compile-time error for a variable initializer to reference any instance member through a *simple_name*.</span></span> <span data-ttu-id="143b6-715">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-715">In the example</span></span>
```csharp
class A
{
    int x = 1;
    int y = x + 1;        // Error, reference to instance member of this
}
```
<span data-ttu-id="143b6-716">에 대 한 변수 이니셜라이저 `y` 만들어지는 인스턴스 멤버를 참조 하기 때문에 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-716">the variable initializer for `y` results in a compile-time error because it references a member of the instance being created.</span></span>

## <a name="methods"></a><span data-ttu-id="143b6-717">메서드</span><span class="sxs-lookup"><span data-stu-id="143b6-717">Methods</span></span>

<span data-ttu-id="143b6-718">***메서드***는 개체 또는 클래스에서 수행할 수 있는 계산이나 작업을 구현하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-718">A ***method*** is a member that implements a computation or action that can be performed by an object or class.</span></span> <span data-ttu-id="143b6-719">메서드를 사용 하 여 선언 *method_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="143b6-719">Methods are declared using *method_declaration*s:</span></span>

```antlr
method_declaration
    : method_header method_body
    ;

method_header
    : attributes? method_modifier* 'partial'? return_type member_name type_parameter_list?
      '(' formal_parameter_list? ')' type_parameter_constraints_clause*
    ;

method_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'static'
    | 'virtual'
    | 'sealed'
    | 'override'
    | 'abstract'
    | 'extern'
    | 'async'
    | method_modifier_unsafe
    ;

return_type
    : type
    | 'void'
    ;

member_name
    : identifier
    | interface_type '.' identifier
    ;

method_body
    : block
    | '=>' expression ';'
    | ';'
    ;
```

<span data-ttu-id="143b6-720">A *method_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)) 및 네 가지 액세스 한정자의 유효한 조합이 ([액세스 한정자 ](classes.md#access-modifiers)), `new` ([새 한정자](classes.md#the-new-modifier)), `static` ([정적 메서드와 인스턴스](classes.md#static-and-instance-methods)), `virtual` ([가상메서드](classes.md#virtual-methods)), `override` ([메서드를 재정의](classes.md#override-methods)), `sealed` ([메서드를 봉인](classes.md#sealed-methods)), `abstract` ([추상 메서드](classes.md#abstract-methods)), 및 `extern` ([외부 메서드](classes.md#external-methods)) 한정자.</span><span class="sxs-lookup"><span data-stu-id="143b6-720">A *method_declaration* may include a set of *attributes* ([Attributes](attributes.md)) and a valid combination of the four access modifiers ([Access modifiers](classes.md#access-modifiers)), the `new` ([The new modifier](classes.md#the-new-modifier)),  `static` ([Static and instance methods](classes.md#static-and-instance-methods)), `virtual` ([Virtual methods](classes.md#virtual-methods)), `override` ([Override methods](classes.md#override-methods)), `sealed` ([Sealed methods](classes.md#sealed-methods)), `abstract` ([Abstract methods](classes.md#abstract-methods)), and `extern` ([External methods](classes.md#external-methods)) modifiers.</span></span>

<span data-ttu-id="143b6-721">선언에는 다음과 같은 경우 한정자의 유효한 조합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-721">A declaration has a valid combination of modifiers if all of the following are true:</span></span>

*  <span data-ttu-id="143b6-722">선언에 대 한 액세스 한정자의 유효한 조합이 포함 ([액세스 한정자](classes.md#access-modifiers)).</span><span class="sxs-lookup"><span data-stu-id="143b6-722">The declaration includes a valid combination of access modifiers ([Access modifiers](classes.md#access-modifiers)).</span></span>
*  <span data-ttu-id="143b6-723">선언 한정자를 동일한 여러 번 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-723">The declaration does not include the same modifier multiple times.</span></span>
*  <span data-ttu-id="143b6-724">다음 한정자 중 하나만 선언 포함: `static`, `virtual`, 및 `override`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-724">The declaration includes at most one of the following modifiers: `static`, `virtual`, and `override`.</span></span>
*  <span data-ttu-id="143b6-725">선언에는 다음 한정자 중 하나만 포함 합니다. `new` 및 `override`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-725">The declaration includes at most one of the following modifiers: `new` and `override`.</span></span>
*  <span data-ttu-id="143b6-726">선언에 포함 하는 경우는 `abstract` 한정자를 다음 선언을 포함 하지 않습니다 다음 한정자 중: `static`를 `virtual`, `sealed` 또는 `extern`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-726">If the declaration includes the `abstract` modifier, then the declaration does not include any of the following modifiers: `static`, `virtual`, `sealed` or `extern`.</span></span>
*  <span data-ttu-id="143b6-727">선언에 포함 하는 경우는 `private` 한정자를 다음 선언을 포함 하지 않습니다 다음 한정자 중: `virtual`를 `override`, 또는 `abstract`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-727">If the declaration includes the `private` modifier, then the declaration does not include any of the following modifiers: `virtual`, `override`, or `abstract`.</span></span>
*  <span data-ttu-id="143b6-728">선언에 포함 하는 경우는 `sealed` 한정자를 선언도 포함 됩니다는 `override` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-728">If the declaration includes the `sealed` modifier, then the declaration also includes the `override` modifier.</span></span>
*  <span data-ttu-id="143b6-729">선언을 포함 하는 경우는 `partial` 한다면 한정자를 포함 하지 않습니다 다음 한정자 중: `new`, `public`, `protected`, `internal`를 `private`, `virtual`를 `sealed`, `override` 하십시오 `abstract`, 또는 `extern`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-729">If the declaration includes the `partial` modifier, then it does not include any of the following modifiers: `new`, `public`, `protected`, `internal`, `private`, `virtual`, `sealed`, `override`, `abstract`, or `extern`.</span></span>

<span data-ttu-id="143b6-730">포함 된 메서드를 `async` 한정자는 비동기 함수 및에 설명 된 규칙을 따릅니다 [비동기 함수](classes.md#async-functions)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-730">A method that has the `async` modifier is an async function and follows the rules described in [Async functions](classes.md#async-functions).</span></span>

<span data-ttu-id="143b6-731">합니다 *return_type* 메서드의 선언은 계산 및 확장 메서드에서 반환한 값의 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-731">The *return_type* of a method declaration specifies the type of the value computed and returned by the method.</span></span> <span data-ttu-id="143b6-732">합니다 *return_type* 는 `void` 메서드 값을 반환 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="143b6-732">The *return_type* is `void` if the method does not return a value.</span></span> <span data-ttu-id="143b6-733">선언에 포함 하는 경우는 `partial` 한정자, 반환 형식 가능 해야 합니다 `void`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-733">If the declaration includes the `partial` modifier, then the return type must be `void`.</span></span>

<span data-ttu-id="143b6-734">합니다 *member_name* 메서드의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-734">The *member_name* specifies the name of the method.</span></span> <span data-ttu-id="143b6-735">메서드는 명시적 인터페이스 멤버 구현 하지 않는 한 ([명시적 인터페이스 멤버 구현을](interfaces.md#explicit-interface-member-implementations)), *member_name* 되는 단순히 *식별자*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-735">Unless the method is an explicit interface member implementation ([Explicit interface member implementations](interfaces.md#explicit-interface-member-implementations)), the *member_name* is simply an *identifier*.</span></span> <span data-ttu-id="143b6-736">명시적 인터페이스 멤버 구현에 대 한 합니다 *member_name* 이루어져는 *interface_type* 뒤에 "`.`" 및 *식별자*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-736">For an explicit interface member implementation, the *member_name* consists of an *interface_type* followed by a "`.`" and an *identifier*.</span></span>

<span data-ttu-id="143b6-737">선택적 *type_parameter_list* 메서드의 형식 매개 변수 지정 ([매개 변수 입력](classes.md#type-parameters)).</span><span class="sxs-lookup"><span data-stu-id="143b6-737">The optional *type_parameter_list* specifies the type parameters of the method ([Type parameters](classes.md#type-parameters)).</span></span> <span data-ttu-id="143b6-738">경우는 *type_parameter_list* 메서드는 지정 된 된 ***제네릭 메서드***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-738">If a *type_parameter_list* is specified the method is a ***generic method***.</span></span> <span data-ttu-id="143b6-739">메서드에 `extern` 한정자를 *type_parameter_list* 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-739">If the method has an `extern` modifier, a *type_parameter_list* cannot be specified.</span></span>

<span data-ttu-id="143b6-740">선택적 *formal_parameter_list* 메서드의 매개 변수 지정 ([메서드 매개 변수](classes.md#method-parameters)).</span><span class="sxs-lookup"><span data-stu-id="143b6-740">The optional *formal_parameter_list* specifies the parameters of the method ([Method parameters](classes.md#method-parameters)).</span></span>

<span data-ttu-id="143b6-741">선택적 *type_parameter_constraints_clause*은 개별 형식 매개 변수에 대 한 제약 조건 지정 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)) 하는 경우에 지정할 수 있습니다 및는 *type_parameter_ 목록* 변수도 제공한 메서드가 없는 `override` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-741">The optional *type_parameter_constraints_clause*s specify constraints on individual type parameters ([Type parameter constraints](classes.md#type-parameter-constraints)) and may only be specified if a *type_parameter_list* is also supplied, and the method does not have an `override` modifier.</span></span>

<span data-ttu-id="143b6-742">합니다 *return_type* 에서 참조 되는 형식의 각 합니다 *formal_parameter_list* 메서드의 해야 적어도 메서드 자체 만큼 액세스 가능 ([접근성 제약 조건](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="143b6-742">The *return_type* and each of the types referenced in the *formal_parameter_list* of a method must be at least as accessible as the method itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

<span data-ttu-id="143b6-743">*method_body* 중 하나는 세미콜론을 ***문 본문*** 요소나 ***식 본문***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-743">The *method_body* is either a semicolon, a ***statement body*** or an ***expression body***.</span></span> <span data-ttu-id="143b6-744">문 본문으로 구성 됩니다는 *블록*, 메서드가 호출 될 때 실행할 문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-744">A statement body consists of a *block*, which specifies the statements to execute when the method is invoked.</span></span> <span data-ttu-id="143b6-745">식 본문이 이루어져 `=>` 뒤에 *식* 및 세미콜론 메서드가 호출 될 때 수행 하는 단일 식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-745">An expression body consists of `=>` followed by an *expression* and a semicolon, and denotes a single expression to perform when the method is invoked.</span></span> 

<span data-ttu-id="143b6-746">에 대 한 `abstract` 하 고 `extern` 메서드는 *method_body* 세미콜론으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-746">For `abstract` and `extern` methods, the *method_body* consists simply of a semicolon.</span></span> <span data-ttu-id="143b6-747">에 대 한 `partial` 메서드를 *method_body* 세미콜론, 블록 본문 또는 식 본문이 구성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-747">For `partial` methods the *method_body* may consist of either a semicolon, a block body or an expression body.</span></span> <span data-ttu-id="143b6-748">다른 모든 메서드는 *method_body* 되었거나 블록 본문을 식 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-748">For all other methods, the *method_body* is either a block body or an expression body.</span></span>

<span data-ttu-id="143b6-749">경우는 *method_body* 선언을 포함 하지 않을 경우 다음을 세미콜론으로 구성 됩니다는 `async` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-749">If the *method_body* consists of a semicolon, then the declaration may not include the `async` modifier.</span></span>

<span data-ttu-id="143b6-750">시그니처를 정의 하는 이름, 형식 매개 변수 목록 및 메서드의 정식 매개 변수 목록 ([시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading)) 메서드.</span><span class="sxs-lookup"><span data-stu-id="143b6-750">The name, the type parameter list and the formal parameter list of a method define the signature ([Signatures and overloading](basic-concepts.md#signatures-and-overloading)) of the method.</span></span> <span data-ttu-id="143b6-751">특히 메서드의 시그니처에 해당 이름의 형식 매개 변수 수, 한정자 및 형식 매개 변수 유형의 수가 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-751">Specifically, the signature of a method consists of its name, the number of type parameters and the number, modifiers, and types of its formal parameters.</span></span> <span data-ttu-id="143b6-752">이러한 목적을 위해 형식 매개 변수 형식에서 발생 하는 메서드의 형식 매개 변수에 메서드의 형식 인수 목록에 있는 서 수 위치를 기준으로 하지만 해당 이름으로 식별 됩니다. 형식 매개 변수 또는 형식 매개 변수 이름을 반환 형식은 없으며 메서드 서명의 일부가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-752">For these purposes, any type parameter of the method that occurs in the type of a formal parameter is identified not by its name, but by its ordinal position in the type argument list of the method.The return type is not part of a method's signature, nor are the names of the type parameters or the formal parameters.</span></span>

<span data-ttu-id="143b6-753">메서드의 이름을 메서드 이름에 다른 모든 비-동일한 클래스에서 선언에서 달라 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-753">The name of a method must differ from the names of all other non-methods declared in the same class.</span></span> <span data-ttu-id="143b6-754">또한 메서드의 시그니처는 동일한 클래스에서 선언 된 다른 모든 메서드의 시그니처와 달라 야 하 고 동일한 클래스에서 선언 하는 두 가지 방법으로만 다른 서명이 없을 `ref` 고 `out`입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-754">In addition, the signature of a method must differ from the signatures of all other methods declared in the same class, and two methods declared in the same class may not have signatures that differ solely by `ref` and `out`.</span></span>

<span data-ttu-id="143b6-755">메서드의 *type_parameter*가 전체 범위에는 *method_declaration*, 해당 범위에서 전체 폼 형식에 사용할 수 있습니다 *return_type*를 *method_body*, 및 *type_parameter_constraints_clause*s 되지 않습니다 *특성*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-755">The method's *type_parameter*s are in scope throughout the *method_declaration*, and can be used to form types throughout that scope in *return_type*, *method_body*, and *type_parameter_constraints_clause*s but not in *attributes*.</span></span>

<span data-ttu-id="143b6-756">모든 정식 매개 변수 및 형식 매개 변수 이름과 달라 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-756">All formal parameters and type parameters must have different names.</span></span>

### <a name="method-parameters"></a><span data-ttu-id="143b6-757">메서드 매개 변수</span><span class="sxs-lookup"><span data-stu-id="143b6-757">Method parameters</span></span>

<span data-ttu-id="143b6-758">메서드의 매개 변수 있는 경우 여 선언 된 메서드의 *formal_parameter_list*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-758">The parameters of a method, if any, are declared by the method's *formal_parameter_list*.</span></span>

```antlr
formal_parameter_list
    : fixed_parameters
    | fixed_parameters ',' parameter_array
    | parameter_array
    ;

fixed_parameters
    : fixed_parameter (',' fixed_parameter)*
    ;

fixed_parameter
    : attributes? parameter_modifier? type identifier default_argument?
    ;

default_argument
    : '=' expression
    ;

parameter_modifier
    : 'ref'
    | 'out'
    | 'this'
    ;

parameter_array
    : attributes? 'params' array_type identifier
    ;
```

<span data-ttu-id="143b6-759">정식 매개 변수 목록이 하나 이상의 쉼표로 구분 된 매개 변수는 마지막만 될 수 있습니다는 *parameter_array*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-759">The formal parameter list consists of one or more comma-separated parameters of which only the last may be a *parameter_array*.</span></span>

<span data-ttu-id="143b6-760">*fixed_parameter* 선택적 집합으로 이루어져 *특성* ([특성](attributes.md)), 선택적인 `ref`를 `out` 또는 `this` 한정자는 *형식*, *식별자* 및 선택적 *default_argument*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-760">A *fixed_parameter* consists of an optional set of *attributes* ([Attributes](attributes.md)), an optional `ref`, `out` or `this` modifier, a *type*, an *identifier* and an optional *default_argument*.</span></span> <span data-ttu-id="143b6-761">각 *fixed_parameter* 지정 된 이름의 지정 된 형식의 매개 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-761">Each *fixed_parameter* declares a parameter of the given type with the given name.</span></span> <span data-ttu-id="143b6-762">`this` 한정자를 확장 메서드로 메서드를 지정 하 고 정적 메서드의 첫 번째 매개 변수 에서만 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-762">The `this` modifier designates the method as an extension method and is only allowed on the first parameter of a static method.</span></span> <span data-ttu-id="143b6-763">확장 메서드에 추가로 나와 [확장 메서드](classes.md#extension-methods)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-763">Extension methods are further described in [Extension methods](classes.md#extension-methods).</span></span>

<span data-ttu-id="143b6-764">A *fixed_parameter* 사용 하 여를 *default_argument* 라고는 ***선택적 매개 변수***반면를 *fixed_parameter* 없이 *default_argument* 되는 ***필수 매개 변수***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-764">A *fixed_parameter* with a *default_argument* is known as an ***optional parameter***, whereas a *fixed_parameter* without a *default_argument* is a ***required parameter***.</span></span> <span data-ttu-id="143b6-765">필수 매개 변수는 선택적 매개 변수 후 나타나지 않을 수 있습니다는 *formal_parameter_list*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-765">A required parameter may not appear after an optional parameter in a *formal_parameter_list*.</span></span>

<span data-ttu-id="143b6-766">A `ref` 나 `out` 매개 변수에 사용할 수 없습니다는 *default_argument*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-766">A `ref` or `out` parameter cannot have a *default_argument*.</span></span> <span data-ttu-id="143b6-767">합니다 *식* 에 *default_argument* 다음 중 하나 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-767">The *expression* in a *default_argument* must be one of the following:</span></span>

*  <span data-ttu-id="143b6-768">*constant_expression*</span><span class="sxs-lookup"><span data-stu-id="143b6-768">a *constant_expression*</span></span>
*  <span data-ttu-id="143b6-769">폼의 식을 `new S()` 여기서 `S` 값 형식인</span><span class="sxs-lookup"><span data-stu-id="143b6-769">an expression of the form `new S()` where `S` is a value type</span></span>
*  <span data-ttu-id="143b6-770">폼의 식을 `default(S)` 여기서 `S` 값 형식인</span><span class="sxs-lookup"><span data-stu-id="143b6-770">an expression of the form `default(S)` where `S` is a value type</span></span>

<span data-ttu-id="143b6-771">합니다 *식* id 또는 nullable 매개 변수의 형식 변환 하 여 암시적으로 변환할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-771">The *expression* must be implicitly convertible by an identity or nullable conversion to the type of the parameter.</span></span>

<span data-ttu-id="143b6-772">선택적 매개 변수를 구현 하는 partial 메서드 선언에서 발생 하는 경우 ([부분 메서드](classes.md#partial-methods))에 명시적 인터페이스 멤버 구현 ([명시적 인터페이스 멤버 구현을](interfaces.md#explicit-interface-member-implementations)) 또는 단일 매개 변수 인덱서 선언이 있다고 가정 ([인덱서](classes.md#indexers)) 컴파일러가 이러한 멤버를 생략할 수에 대 한 인수를 허용 하는 방식으로 호출 되지 수 있으므로 경고를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-772">If optional parameters occur in an implementing partial method declaration ([Partial methods](classes.md#partial-methods)) , an explicit interface member implementation ([Explicit interface member implementations](interfaces.md#explicit-interface-member-implementations)) or in a single-parameter indexer declaration ([Indexers](classes.md#indexers)) the compiler should give a warning, since these members can never be invoked in a way that permits arguments to be omitted.</span></span>

<span data-ttu-id="143b6-773">A *parameter_array* 선택적 집합으로 이루어져 *특성* ([특성](attributes.md)), `params` 한정자는 *array_type*, 및 *식별자*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-773">A *parameter_array* consists of an optional set of *attributes* ([Attributes](attributes.md)), a `params` modifier, an *array_type*, and an *identifier*.</span></span> <span data-ttu-id="143b6-774">매개 변수 배열에 지정 된 이름의 지정 된 배열 형식의 단일 매개 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-774">A parameter array declares a single parameter of the given array type with the given name.</span></span> <span data-ttu-id="143b6-775">합니다 *array_type* 매개 변수의 배열에는 1 차원 배열 형식 이어야 합니다 ([배열 형식을](arrays.md#array-types)).</span><span class="sxs-lookup"><span data-stu-id="143b6-775">The *array_type* of a parameter array must be a single-dimensional array type ([Array types](arrays.md#array-types)).</span></span> <span data-ttu-id="143b6-776">메서드 호출을 매개 변수 배열에 지정 된 주어진된 배열 형식의 단일 인수를 허용 하거나 지정 배열 요소 형식의 0 개 이상의 인수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-776">In a method invocation, a parameter array permits either a single argument of the given array type to be specified, or it permits zero or more arguments of the array element type to be specified.</span></span> <span data-ttu-id="143b6-777">매개 변수 배열에 자세히 설명 되어 [매개 변수 배열](classes.md#parameter-arrays)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-777">Parameter arrays are described further in [Parameter arrays](classes.md#parameter-arrays).</span></span>

<span data-ttu-id="143b6-778">A *parameter_array* 선택적 매개 변수를 한 후 발생할 수 있지만 생략에 대 한 인수의 기본 값을 사용할 수 없습니다는 *parameter_array* 대신 초래 빈 배열 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-778">A *parameter_array* may occur after an optional parameter, but cannot have a default value -- the omission of arguments for a *parameter_array* would instead result in the creation of an empty array.</span></span>

<span data-ttu-id="143b6-779">다음 예제에서는 다른 종류를의 매개 변수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-779">The following example illustrates different kinds of parameters:</span></span>
```csharp
public void M(
    ref int      i,
    decimal      d,
    bool         b = false,
    bool?        n = false,
    string       s = "Hello",
    object       o = null,
    T            t = default(T),
    params int[] a
) { }
```

<span data-ttu-id="143b6-780">에 *formal_parameter_list* 에 대 한 `M`, `i` 필수 ref 매개 변수 `d` 필수 값 매개 변수 `b`를 `s`를 `o` 및 `t` 선택적 값 매개 변수 및 `a` 매개 변수 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-780">In the *formal_parameter_list* for `M`, `i` is a required ref parameter, `d` is a required value parameter, `b`, `s`, `o` and `t` are optional value parameters and `a` is a parameter array.</span></span>

<span data-ttu-id="143b6-781">메서드 선언 매개 변수, 형식 매개 변수 및 지역 변수에 대 한 별도 선언 공간을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-781">A method declaration creates a separate declaration space for parameters, type parameters and local variables.</span></span> <span data-ttu-id="143b6-782">이름에서 지역 변수 선언 및 형식 매개 변수 목록 및 메서드의 정식 매개 변수 목록에서이 선언 공간에 도입 된 합니다 *블록* 메서드.</span><span class="sxs-lookup"><span data-stu-id="143b6-782">Names are introduced into this declaration space by the type parameter list and the formal parameter list of the method and by local variable declarations in the *block* of the method.</span></span> <span data-ttu-id="143b6-783">이 동일한 이름을 갖도록 메서드 선언 공간의 두 멤버에 대 한 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-783">It is an error for two members of a method declaration space to have the same name.</span></span> <span data-ttu-id="143b6-784">메서드 선언 공간 및 동일한 이름 가진 요소를 포함 하는 중첩 된 선언 공간의 지역 변수 선언 공간에 대 한 오류는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-784">It is an error for the method declaration space and the local variable declaration space of a nested declaration space to contain elements with the same name.</span></span>

<span data-ttu-id="143b6-785">메서드 호출 ([메서드 호출](expressions.md#method-invocations)) 특정 해당 호출에는 복사본을 만들고, 정식 매개 변수 및 호출의 인수 목록과 메서드의 지역 변수 값 또는 변수 참조를 할당 합니다 새로 만든 정식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-785">A method invocation ([Method invocations](expressions.md#method-invocations)) creates a copy, specific to that invocation, of the formal parameters and local variables of the method, and the argument list of the invocation assigns values or variable references to the newly created formal parameters.</span></span> <span data-ttu-id="143b6-786">내 합니다 *블록* 메서드의 정식 매개 변수에서 해당 식별자에서 참조할 수 *simple_name* 식 ([단순 이름](expressions.md#simple-names)).</span><span class="sxs-lookup"><span data-stu-id="143b6-786">Within the *block* of a method, formal parameters can be referenced by their identifiers in *simple_name* expressions ([Simple names](expressions.md#simple-names)).</span></span>

<span data-ttu-id="143b6-787">정식 매개 변수는 다음과 같은 네 가지 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-787">There are four kinds of formal parameters:</span></span>

*  <span data-ttu-id="143b6-788">모든 한정자 없이 선언 된 값 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-788">Value parameters, which are declared without any modifiers.</span></span>
*  <span data-ttu-id="143b6-789">매개 변수를 사용 하 여 선언 된 참조는 `ref` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-789">Reference parameters, which are declared with the `ref` modifier.</span></span>
*  <span data-ttu-id="143b6-790">출력 매개 변수를 사용 하 여 선언 된 `out` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-790">Output parameters, which are declared with the `out` modifier.</span></span>
*  <span data-ttu-id="143b6-791">선언 된 매개 변수 배열과 `params` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-791">Parameter arrays, which are declared with the `params` modifier.</span></span>

<span data-ttu-id="143b6-792">에 설명 된 대로 [시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading), `ref` 하 고 `out` 한정자는 메서드 시그니처의 일부로 하지만 `params` 한정자는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-792">As described in [Signatures and overloading](basic-concepts.md#signatures-and-overloading), the `ref` and `out` modifiers are part of a method's signature, but the `params` modifier is not.</span></span>

#### <a name="value-parameters"></a><span data-ttu-id="143b6-793">값 매개 변수</span><span class="sxs-lookup"><span data-stu-id="143b6-793">Value parameters</span></span>

<span data-ttu-id="143b6-794">없는 한정자를 사용 하 여 선언 된 매개 변수는 값 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-794">A parameter declared with no modifiers is a value parameter.</span></span> <span data-ttu-id="143b6-795">값 매개 변수를 메서드 호출에 제공 하는 해당 인수에서 초기 값을 가져오는 지역 변수에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-795">A value parameter corresponds to a local variable that gets its initial value from the corresponding argument supplied in the method invocation.</span></span>

<span data-ttu-id="143b6-796">메서드 호출을 해당 인수 암시적으로 변환할 수 있는 식 이어야 값 매개 변수는 정식 매개 변수를 사용 하는 경우 ([암시적 변환을](conversions.md#implicit-conversions)) 정식 매개 변수 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-796">When a formal parameter is a value parameter, the corresponding argument in a method invocation must be an expression that is implicitly convertible ([Implicit conversions](conversions.md#implicit-conversions)) to the formal parameter type.</span></span>

<span data-ttu-id="143b6-797">메서드는 값 매개 변수에 새 값을 할당 하도록 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-797">A method is permitted to assign new values to a value parameter.</span></span> <span data-ttu-id="143b6-798">이러한 할당 값 매개 변수에서 나타내는 로컬 저장소 위치에만 영향을 주며-메서드 호출에 지정 된 실제 인수에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-798">Such assignments only affect the local storage location represented by the value parameter—they have no effect on the actual argument given in the method invocation.</span></span>

#### <a name="reference-parameters"></a><span data-ttu-id="143b6-799">참조 매개 변수</span><span class="sxs-lookup"><span data-stu-id="143b6-799">Reference parameters</span></span>

<span data-ttu-id="143b6-800">매개 변수를 사용 하 여 선언 된 `ref` 한정자는 참조 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-800">A parameter declared with a `ref` modifier is a reference parameter.</span></span> <span data-ttu-id="143b6-801">값 매개 변수를 달리 참조 매개 변수는 새 저장소 위치를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-801">Unlike a value parameter, a reference parameter does not create a new storage location.</span></span> <span data-ttu-id="143b6-802">대신 참조 매개 변수는 메서드 호출의 인수로 지정 된 변수와 동일한 저장소 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-802">Instead, a reference parameter represents the same storage location as the variable given as the argument in the method invocation.</span></span>

<span data-ttu-id="143b6-803">메서드 호출을 해당 인수 키워드 구성 되어야 합니다는 정식 매개 변수는 참조 매개 변수 이면 `ref` 뒤에 *variable_reference* ([결정 하는 것에 대 한 정확한 규칙 한정 된 할당](variables.md#precise-rules-for-determining-definite-assignment))의 형식 매개 변수 형식과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-803">When a formal parameter is a reference parameter, the corresponding argument in a method invocation must consist of the keyword `ref` followed by a *variable_reference* ([Precise rules for determining definite assignment](variables.md#precise-rules-for-determining-definite-assignment)) of the same type as the formal parameter.</span></span> <span data-ttu-id="143b6-804">변수 참조 매개 변수로 전달할 수 전에 확실 하 게 할당 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-804">A variable must be definitely assigned before it can be passed as a reference parameter.</span></span>

<span data-ttu-id="143b6-805">인 메서드 내부의 참조 매개 변수는 항상 정적으로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-805">Within a method, a reference parameter is always considered definitely assigned.</span></span>

<span data-ttu-id="143b6-806">반복기로 선언 된 메서드 ([반복기](classes.md#iterators)) 참조 매개 변수를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-806">A method declared as an iterator ([Iterators](classes.md#iterators)) cannot have reference parameters.</span></span>

<span data-ttu-id="143b6-807">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-807">The example</span></span>
```csharp
using System;

class Test
{
    static void Swap(ref int x, ref int y) {
        int temp = x;
        x = y;
        y = temp;
    }

    static void Main() {
        int i = 1, j = 2;
        Swap(ref i, ref j);
        Console.WriteLine("i = {0}, j = {1}", i, j);
    }
}
```
<span data-ttu-id="143b6-808">는 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-808">produces the output</span></span>
```
i = 2, j = 1
```

<span data-ttu-id="143b6-809">호출에 대 한 `Swap` 에 `Main`, `x` 나타냅니다 `i` 하 고 `y` 나타냅니다 `j`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-809">For the invocation of `Swap` in `Main`, `x` represents `i` and `y` represents `j`.</span></span> <span data-ttu-id="143b6-810">따라서 호출 효과가 값의 교환을 `i` 고 `j`입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-810">Thus, the invocation has the effect of swapping the values of `i` and `j`.</span></span>

<span data-ttu-id="143b6-811">메서드에서 여러 이름이 동일한 저장소 위치를 나타낼 수 하는 참조 매개 변수를 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-811">In a method that takes reference parameters it is possible for multiple names to represent the same storage location.</span></span> <span data-ttu-id="143b6-812">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-812">In the example</span></span>
```csharp
class A
{
    string s;

    void F(ref string a, ref string b) {
        s = "One";
        a = "Two";
        b = "Three";
    }

    void G() {
        F(ref s, ref s);
    }
}
```
<span data-ttu-id="143b6-813">호출 `F` 에 `G` 에 대 한 참조를 전달 `s` 둘 다에 대해 `a` 고 `b`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-813">the invocation of `F` in `G` passes a reference to `s` for both `a` and `b`.</span></span> <span data-ttu-id="143b6-814">이 호출의 경우 이름에 따라서 `s`, `a`, 및 `b` 동일한 저장소 위치, 모든 참조 및 인스턴스 필드를 수정 하는 모든 세 가지 할당 `s`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-814">Thus, for that invocation, the names `s`, `a`, and `b` all refer to the same storage location, and the three assignments all modify the instance field `s`.</span></span>

#### <a name="output-parameters"></a><span data-ttu-id="143b6-815">출력 매개 변수</span><span class="sxs-lookup"><span data-stu-id="143b6-815">Output parameters</span></span>

<span data-ttu-id="143b6-816">사용 하 여 선언 된 매개 변수는 `out` 한정자 출력 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-816">A parameter declared with an `out` modifier is an output parameter.</span></span> <span data-ttu-id="143b6-817">참조 매개 변수와 마찬가지로 출력 매개 변수 만들어지지는지 않습니다 새 저장소 위치.</span><span class="sxs-lookup"><span data-stu-id="143b6-817">Similar to a reference parameter, an output parameter does not create a new storage location.</span></span> <span data-ttu-id="143b6-818">대신, 출력 매개 변수는 메서드 호출의 인수로 지정 된 변수와 동일한 저장소 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-818">Instead, an output parameter represents the same storage location as the variable given as the argument in the method invocation.</span></span>

<span data-ttu-id="143b6-819">메서드 호출을 해당 인수 키워드는 이루어져야 정식 매개 변수가 출력 매개 변수 이면 `out` 뒤에 *variable_reference* ([결정 하는 것에 대 한 정확한 규칙 한정 된 할당](variables.md#precise-rules-for-determining-definite-assignment))의 형식 매개 변수 형식과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-819">When a formal parameter is an output parameter, the corresponding argument in a method invocation must consist of the keyword `out` followed by a *variable_reference* ([Precise rules for determining definite assignment](variables.md#precise-rules-for-determining-definite-assignment)) of the same type as the formal parameter.</span></span> <span data-ttu-id="143b6-820">변수를 필요 하지 명확 하 게 할당 output 매개 변수로 전달할 수 있습니다 하지만 변수는 출력 매개 변수로 전달 된 위치에 호출을 다음 변수의 정적으로 할당 된 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-820">A variable need not be definitely assigned before it can be passed as an output parameter, but following an invocation where a variable was passed as an output parameter, the variable is considered definitely assigned.</span></span>

<span data-ttu-id="143b6-821">인 메서드 내부의 마찬가지로 로컬 변수를 output 매개 변수 처음 것으로 간주 되어 할당 되지 않은 해당 값을 사용 하기 전에 반드시 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-821">Within a method, just like a local variable, an output parameter is initially considered unassigned and must be definitely assigned before its value is used.</span></span>

<span data-ttu-id="143b6-822">메서드의 모든 출력 매개 변수는 메서드가 반환 되기 전에 확실 하 게 할당 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-822">Every output parameter of a method must be definitely assigned before the method returns.</span></span>

<span data-ttu-id="143b6-823">부분 메서드로 메서드를 선언 ([부분 메서드](classes.md#partial-methods)) 또는 반복기 ([반복기](classes.md#iterators)) 출력 매개 변수를 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-823">A method declared as a partial method ([Partial methods](classes.md#partial-methods)) or an iterator ([Iterators](classes.md#iterators)) cannot have output parameters.</span></span>

<span data-ttu-id="143b6-824">출력 매개 변수는 일반적으로 여러 개의 반환 값을 생성 하는 메서드에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-824">Output parameters are typically used in methods that produce multiple return values.</span></span> <span data-ttu-id="143b6-825">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="143b6-825">For example:</span></span>
```csharp
using System;

class Test
{
    static void SplitPath(string path, out string dir, out string name) {
        int i = path.Length;
        while (i > 0) {
            char ch = path[i - 1];
            if (ch == '\\' || ch == '/' || ch == ':') break;
            i--;
        }
        dir = path.Substring(0, i);
        name = path.Substring(i);
    }

    static void Main() {
        string dir, name;
        SplitPath("c:\\Windows\\System\\hello.txt", out dir, out name);
        Console.WriteLine(dir);
        Console.WriteLine(name);
    }
}
```

<span data-ttu-id="143b6-826">이 예제에서는 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-826">The example produces the output:</span></span>
```
c:\Windows\System\
hello.txt
```

<span data-ttu-id="143b6-827">`dir` 하 고 `name` 에 전달 되기 전에 변수에 할당 될 수 있습니다 `SplitPath`, 하는 것이 호출 다음에 정적으로 할당 하 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-827">Note that the `dir` and `name` variables can be unassigned before they are passed to `SplitPath`, and that they are considered definitely assigned following the call.</span></span>

#### <a name="parameter-arrays"></a><span data-ttu-id="143b6-828">매개 변수 배열</span><span class="sxs-lookup"><span data-stu-id="143b6-828">Parameter arrays</span></span>

<span data-ttu-id="143b6-829">사용 하 여 선언 된 매개 변수는 `params` 한정자 매개 변수 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-829">A parameter declared with a `params` modifier is a parameter array.</span></span> <span data-ttu-id="143b6-830">정식 매개 변수 목록에서 매개 변수 배열에 포함 된 경우 목록에서 마지막 매개 변수 여야 합니다 및 1 차원 배열 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-830">If a formal parameter list includes a parameter array, it must be the last parameter in the list and it must be of a single-dimensional array type.</span></span> <span data-ttu-id="143b6-831">예를 들어, 형식 `string[]` 하 고 `string[][]` 매개 변수 배열의 형식이 있지만 형식으로 사용할 수 있습니다 `string[,]` 할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-831">For example, the types `string[]` and `string[][]` can be used as the type of a parameter array, but the type `string[,]` can not.</span></span> <span data-ttu-id="143b6-832">결합 하는 것이 불가능 합니다 `params` 한정자를 사용 하 여 한정자 `ref` 고 `out`입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-832">It is not possible to combine the `params` modifier with the modifiers `ref` and `out`.</span></span>

<span data-ttu-id="143b6-833">매개 변수 배열에 메서드 호출에서 두 가지 방법 중 하나에 지정 된 수에 대 한 인수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-833">A parameter array permits arguments to be specified in one of two ways in a method invocation:</span></span>

*  <span data-ttu-id="143b6-834">매개 변수 배열로 암시적으로 변환할 수 있는 단일 식 수에 대 한 지정 된 인수 ([암시적 변환을](conversions.md#implicit-conversions)) 매개 변수 배열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-834">The argument given for a parameter array can be a single expression that is implicitly convertible ([Implicit conversions](conversions.md#implicit-conversions)) to the parameter array type.</span></span> <span data-ttu-id="143b6-835">이 경우 매개 변수 배열의 값 매개 변수 처럼 정확 하 게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-835">In this case, the parameter array acts precisely like a value parameter.</span></span>
*  <span data-ttu-id="143b6-836">호출 또는 각 인수는 암시적으로 변환할 수 있는 식을 매개 변수 배열에 대해 0 개 이상의 인수를 지정할 수 ([암시적 변환을](conversions.md#implicit-conversions)) 매개 변수 배열의 요소 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-836">Alternatively, the invocation can specify zero or more arguments for the parameter array, where each argument is an expression that is implicitly convertible ([Implicit conversions](conversions.md#implicit-conversions)) to the element type of the parameter array.</span></span> <span data-ttu-id="143b6-837">호출을 인수의 번호에 해당 하는 길이 사용 하 여 매개 변수 배열 형식의 인스턴스를 만듭니다, 그리고 요소의 지정 된 인수 값을 사용 하 여 배열 인스턴스를 초기화 및 새로 만든된 배열 인스턴스는 실제 사용 하 여이 예제의 경우 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-837">In this case, the invocation creates an instance of the parameter array type with a length corresponding to the number of arguments, initializes the elements of the array instance with the given argument values, and uses the newly created array instance as the actual argument.</span></span>

<span data-ttu-id="143b6-838">호출에 가변 개수의 인수를 허용 하는 제외 하 고 매개 변수 배열에는 정확 하 게 값 매개 변수 ([매개 변수 값](classes.md#value-parameters)) 동일한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-838">Except for allowing a variable number of arguments in an invocation, a parameter array is precisely equivalent to a value parameter ([Value parameters](classes.md#value-parameters)) of the same type.</span></span>

<span data-ttu-id="143b6-839">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-839">The example</span></span>
```csharp
using System;

class Test
{
    static void F(params int[] args) {
        Console.Write("Array contains {0} elements:", args.Length);
        foreach (int i in args) 
            Console.Write(" {0}", i);
        Console.WriteLine();
    }

    static void Main() {
        int[] arr = {1, 2, 3};
        F(arr);
        F(10, 20, 30, 40);
        F();
    }
}
```
<span data-ttu-id="143b6-840">는 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-840">produces the output</span></span>
```
Array contains 3 elements: 1 2 3
Array contains 4 elements: 10 20 30 40
Array contains 0 elements:
```

<span data-ttu-id="143b6-841">첫 번째 호출 `F` 배열이 전달 `a` 값 매개 변수로 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-841">The first invocation of `F` simply passes the array `a` as a value parameter.</span></span> <span data-ttu-id="143b6-842">두 번째 호출 `F` 4 개 요소를 자동으로 만듭니다 `int[]` 지정 된 요소 값 및 값 매개 변수로 인스턴스 배열을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-842">The second invocation of `F` automatically creates a four-element `int[]` with the given element values and passes that array instance as a value parameter.</span></span> <span data-ttu-id="143b6-843">마찬가지로, 세 번째 호출 `F` 0 요소를 만듭니다 `int[]` 값 매개 변수로 해당 인스턴스를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-843">Likewise, the third invocation of `F` creates a zero-element `int[]` and passes that instance as a value parameter.</span></span> <span data-ttu-id="143b6-844">두 번째와 세 번째 호출은 작성 정확 하 게 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-844">The second and third invocations are precisely equivalent to writing:</span></span>
```csharp
F(new int[] {10, 20, 30, 40});
F(new int[] {});
```

<span data-ttu-id="143b6-845">매개 변수 배열 사용 하 여 메서드 오버 로드 확인을 수행할 때 일반적인 형태로 또는 확장 된 형태로 적용할 수 수 있습니다 ([적용 가능한 함수 멤버](expressions.md#applicable-function-member)).</span><span class="sxs-lookup"><span data-stu-id="143b6-845">When performing overload resolution, a method with a parameter array may be applicable either in its normal form or in its expanded form ([Applicable function member](expressions.md#applicable-function-member)).</span></span> <span data-ttu-id="143b6-846">메서드의 확장 된 폼이 메서드의 일반적인 형태를 적용할 수 없는 경우에 및 확장 형식과 동일한 서명 사용 하 여 해당 메서드는 동일한 형식에 이미 선언 되지 않은 경우에 사용할 수 있는 경우</span><span class="sxs-lookup"><span data-stu-id="143b6-846">The expanded form of a method is available only if the normal form of the method is not applicable and only if an applicable method with the same signature as the expanded form is not already declared in the same type.</span></span>

<span data-ttu-id="143b6-847">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-847">The example</span></span>
```csharp
using System;

class Test
{
    static void F(params object[] a) {
        Console.WriteLine("F(object[])");
    }

    static void F() {
        Console.WriteLine("F()");
    }

    static void F(object a0, object a1) {
        Console.WriteLine("F(object,object)");
    }

    static void Main() {
        F();
        F(1);
        F(1, 2);
        F(1, 2, 3);
        F(1, 2, 3, 4);
    }
}
```
<span data-ttu-id="143b6-848">는 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-848">produces the output</span></span>
```
F();
F(object[]);
F(object,object);
F(object[]);
F(object[]);
```

<span data-ttu-id="143b6-849">예제에서는 두 개의 매개 변수 배열 사용 하 여 메서드의 확장된 가능한 폼 이미 포함 됩니다 클래스의 일반 메서드로.</span><span class="sxs-lookup"><span data-stu-id="143b6-849">In the example, two of the possible expanded forms of the method with a parameter array are already included in the class as regular methods.</span></span> <span data-ttu-id="143b6-850">이 확장된 형식을 고려 하지 않으므로, 오버 로드 확인을 수행할 때 및 첫 번째 및 세 번째 메서드 호출 하므로 일반 메서드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-850">These expanded forms are therefore not considered when performing overload resolution, and the first and third method invocations thus select the regular methods.</span></span> <span data-ttu-id="143b6-851">클래스는 매개 변수 배열 사용 하 여 메서드를 선언 하는 경우 드물지 않습니다도 일반 메서드로 확장된 형식 중 일부를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-851">When a class declares a method with a parameter array, it is not uncommon to also include some of the expanded forms as regular methods.</span></span> <span data-ttu-id="143b6-852">배열 할당을 막을 수 있기 때문에 수행 하 여 인스턴스를 확장 된 형식 매개 변수 배열 사용한 메서드 때 발생 하는 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-852">By doing so it is possible to avoid the allocation of an array instance that occurs when an expanded form of a method with a parameter array is invoked.</span></span>

<span data-ttu-id="143b6-853">매개 변수 배열 형식의 경우 `object[]`, 메서드의 일반 양식 및 단일에 대 한 확장된 형식 간에 잠재적인 모호성이 발생 `object` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-853">When the type of a parameter array is `object[]`, a potential ambiguity arises between the normal form of the method and the expended form for a single `object` parameter.</span></span> <span data-ttu-id="143b6-854">모호성에 대 한 이유는는 `object[]` 형식으로 암시적으로 변환할 수는 그 자체가 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-854">The reason for the ambiguity is that an `object[]` is itself implicitly convertible to type `object`.</span></span> <span data-ttu-id="143b6-855">그러나 모호성 문제가 발생 하지, 하므로 필요한 경우 캐스트를 삽입 하 여 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-855">The ambiguity presents no problem, however, since it can be resolved by inserting a cast if needed.</span></span>

<span data-ttu-id="143b6-856">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-856">The example</span></span>
```csharp
using System;

class Test
{
    static void F(params object[] args) {
        foreach (object o in args) {
            Console.Write(o.GetType().FullName);
            Console.Write(" ");
        }
        Console.WriteLine();
    }

    static void Main() {
        object[] a = {1, "Hello", 123.456};
        object o = a;
        F(a);
        F((object)a);
        F(o);
        F((object[])o);
    }
}
```
<span data-ttu-id="143b6-857">는 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-857">produces the output</span></span>
```
System.Int32 System.String System.Double
System.Object[]
System.Object[]
System.Int32 System.String System.Double
```

<span data-ttu-id="143b6-858">첫 번째 및 마지막 호출에서 `F`의 정규형 `F` 매개 변수 형식과 인수 형식에서 암시적 변환이 존재 하기 때문에 적용 됩니다 (둘 다 형식의 `object[]`).</span><span class="sxs-lookup"><span data-stu-id="143b6-858">In the first and last invocations of `F`, the normal form of `F` is applicable because an implicit conversion exists from the argument type to the parameter type (both are of type `object[]`).</span></span> <span data-ttu-id="143b6-859">오버 로드 확인의 기본 폼을 선택 하는 따라서 `F`, 인수가 일반 값 매개 변수로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-859">Thus, overload resolution selects the normal form of `F`, and the argument is passed as a regular value parameter.</span></span> <span data-ttu-id="143b6-860">두 번째 및 세 번째 호출에서의 일반적인 형태 `F` 매개 변수 형식과 인수 형식에서 암시적 변환이 존재 하기 때문에 적용 되지 않습니다 (형식 `object` 형식으로 암시적으로 변환할 수 없습니다. `object[]`).</span><span class="sxs-lookup"><span data-stu-id="143b6-860">In the second and third invocations, the normal form of `F` is not applicable because no implicit conversion exists from the argument type to the parameter type (type `object` cannot be implicitly converted to type `object[]`).</span></span> <span data-ttu-id="143b6-861">그러나 확장 된 형태의 `F` 적용 될 수 있으므로 오버 로드 확인으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-861">However, the expanded form of `F` is applicable, so it is selected by overload resolution.</span></span> <span data-ttu-id="143b6-862">결과적으로 요소가 하나인 `object[]` 호출에 의해 만들어집니다 배열의 단일 요소에 지정 된 인수 값으로 초기화 됩니다 (에 대 한 참조 되는 자체는 `object[]`).</span><span class="sxs-lookup"><span data-stu-id="143b6-862">As a result, a one-element `object[]` is created by the invocation, and the single element of the array is initialized with the given argument value (which itself is a reference to an `object[]`).</span></span>

### <a name="static-and-instance-methods"></a><span data-ttu-id="143b6-863">정적 및 인스턴스 메서드</span><span class="sxs-lookup"><span data-stu-id="143b6-863">Static and instance methods</span></span>

<span data-ttu-id="143b6-864">메서드 선언을 포함 하는 경우는 `static` 한정자, 메서드는 정적 메서드를 라고는 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-864">When a method declaration includes a `static` modifier, that method is said to be a static method.</span></span> <span data-ttu-id="143b6-865">없는 경우 `static` 한정자가 있는 메서드는 인스턴스 메서드를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-865">When no `static` modifier is present, the method is said to be an instance method.</span></span>

<span data-ttu-id="143b6-866">정적 메서드는 특정 인스턴스에 작동 하지 않고 이며 컴파일 타임 오류를 가리키는 데 `this` 정적 메서드에서.</span><span class="sxs-lookup"><span data-stu-id="143b6-866">A static method does not operate on a specific instance, and it is a compile-time error to refer to `this` in a static method.</span></span>

<span data-ttu-id="143b6-867">인스턴스 메서드를 클래스의 인스턴스에 작동 하 고 해당 인스턴스를 액세스할 수 있습니다 `this` ([이 액세스](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="143b6-867">An instance method operates on a given instance of a class, and that instance can be accessed as `this` ([This access](expressions.md#this-access)).</span></span>

<span data-ttu-id="143b6-868">메서드를 참조 하는 경우는 *member_access* ([멤버 액세스](expressions.md#member-access)) 형식의 `E.M`이면 `M` 가 정적 메서드가 `E` 를포함하는형식을표시해야합니다`M`, 경우에 `M` 인스턴스 메서드 `E` 포함 하는 형식 인스턴스를 나타내야 `M`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-868">When a method is referenced in a *member_access* ([Member access](expressions.md#member-access)) of the form `E.M`, if `M` is a static method, `E` must denote a type containing `M`, and if `M` is an instance method, `E` must denote an instance of a type containing `M`.</span></span>

<span data-ttu-id="143b6-869">정적 간의 차이점 및 인스턴스 멤버 설명에 대 한 자세한 [정적 및 인스턴스 멤버](classes.md#static-and-instance-members)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-869">The differences between static and instance members are discussed further in [Static and instance members](classes.md#static-and-instance-members).</span></span>

### <a name="virtual-methods"></a><span data-ttu-id="143b6-870">가상 메서드</span><span class="sxs-lookup"><span data-stu-id="143b6-870">Virtual methods</span></span>

<span data-ttu-id="143b6-871">인스턴스 메서드 선언 포함 되는 경우는 `virtual` 한정자, 메서드가 가상 메서드를 포함 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-871">When an instance method declaration includes a `virtual` modifier, that method is said to be a virtual method.</span></span> <span data-ttu-id="143b6-872">없는 경우 `virtual` 한정자가 있는 메서드는 비가상 메서드를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-872">When no `virtual` modifier is present, the method is said to be a non-virtual method.</span></span>

<span data-ttu-id="143b6-873">비가상 메서드의 구현은 variant: 구현은 동일 클래스의 인스턴스는 메서드를 호출 하는지 여부를 선언 하거나 파생된 클래스의 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="143b6-873">The implementation of a non-virtual method is invariant: The implementation is the same whether the method is invoked on an instance of the class in which it is declared or an instance of a derived class.</span></span> <span data-ttu-id="143b6-874">반면, 가상 메서드의 구현은 파생 클래스로 대체 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-874">In contrast, the implementation of a virtual method can be superseded by derived classes.</span></span> <span data-ttu-id="143b6-875">상속 된 가상 메서드의 구현을 대체 하는 프로세스 라고 ***재정의*** 메서드 ([메서드를 재정의](classes.md#override-methods)).</span><span class="sxs-lookup"><span data-stu-id="143b6-875">The process of superseding the implementation of an inherited virtual method is known as ***overriding*** that method ([Override methods](classes.md#override-methods)).</span></span>

<span data-ttu-id="143b6-876">가상 메서드 호출에서는 합니다 ***런타임 형식*** 해당 호출을 사용 하는 인스턴스의 위치는 호출할 실제 메서드 구현이 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-876">In a virtual method invocation, the ***run-time type*** of the instance for which that invocation takes place determines the actual method implementation to invoke.</span></span> <span data-ttu-id="143b6-877">비가상 메서드 호출에서는 합니다 ***컴파일 타임 형식*** 인스턴스의 결정 요인입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-877">In a non-virtual method invocation, the ***compile-time type*** of the instance is the determining factor.</span></span> <span data-ttu-id="143b6-878">라는 메서드가 정밀 하 게 말해 `N` 인수 목록을 사용 하 여 호출 `A` 컴파일 타임 형식 인스턴스에 대해 `C` 런타임 형식이 `R` (여기서 `R` 는 `C` 파생 된 클래스 또는 `C`), 다음과 같이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-878">In precise terms, when a method named `N` is invoked with an argument list `A` on an instance with a compile-time type `C` and a run-time type `R` (where `R` is either `C` or a class derived from `C`), the invocation is processed as follows:</span></span>

*  <span data-ttu-id="143b6-879">먼저, 오버 로드 확인에 적용 됩니다 `C`, `N`, 및 `A`특정 메서드를 사용 하려면 `M` 상속에 선언 된 메서드 집합에서 `C`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-879">First, overload resolution is applied to `C`, `N`, and `A`, to select a specific method `M` from the set of methods declared in and inherited by `C`.</span></span> <span data-ttu-id="143b6-880">에 설명 되어 [메서드 호출](expressions.md#method-invocations)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-880">This is described in [Method invocations](expressions.md#method-invocations).</span></span>
*  <span data-ttu-id="143b6-881">그런 다음 if `M` 비가상 메서드입니다 `M` 가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-881">Then, if `M` is a non-virtual method, `M` is invoked.</span></span>
*  <span data-ttu-id="143b6-882">이 고, 그렇지 `M` 가상 메서드를 이며 가장 많이 파생 된 구현의 `M` 기준으로 `R` 가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-882">Otherwise, `M` is a virtual method, and the most derived implementation of `M` with respect to `R` is invoked.</span></span>

<span data-ttu-id="143b6-883">모든 가상 메서드에 의해 클래스에서 선언 되거나 상속에 대 한 존재는 ***구현 최다 파생*** 해당 클래스에 대해 메서드.</span><span class="sxs-lookup"><span data-stu-id="143b6-883">For every virtual method declared in or inherited by a class, there exists a ***most derived implementation*** of the method with respect to that class.</span></span> <span data-ttu-id="143b6-884">가장 많이 파생 된 가상 메서드 구현의 `M` 클래스와 관련 하 여 `R` 다음과 같이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-884">The most derived implementation of a virtual method `M` with respect to a class `R` is determined as follows:</span></span>

*  <span data-ttu-id="143b6-885">경우 `R` 포함 된 소개 `virtual` 선언의 `M`, 가장 많이 파생 된 구현입니다 `M`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-885">If `R` contains the introducing `virtual` declaration of `M`, then this is the most derived implementation of `M`.</span></span>
*  <span data-ttu-id="143b6-886">그렇지 않고 `R` 포함를 `override` 의 `M`, 가장 많이 파생 된 구현입니다 `M`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-886">Otherwise, if `R` contains an `override` of `M`, then this is the most derived implementation of `M`.</span></span>
*  <span data-ttu-id="143b6-887">대부분의 구현을 파생 하는 고, 그렇지 `M` 기준으로 `R` 의 가장 많이 파생 된 구현으로 동일 `M` 의 직접 기본 클래스와 관련 하 여 `R`입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-887">Otherwise, the most derived implementation of `M` with respect to `R` is the same as the most derived implementation of `M` with respect to the direct base class of `R`.</span></span>

<span data-ttu-id="143b6-888">다음 예제에서는 가상 및 비가상 메서드 간의 차이점을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-888">The following example illustrates the differences between virtual and non-virtual methods:</span></span>
```csharp
using System;

class A
{
    public void F() { Console.WriteLine("A.F"); }

    public virtual void G() { Console.WriteLine("A.G"); }
}

class B: A
{
    new public void F() { Console.WriteLine("B.F"); }

    public override void G() { Console.WriteLine("B.G"); }
}

class Test
{
    static void Main() {
        B b = new B();
        A a = b;
        a.F();
        b.F();
        a.G();
        b.G();
    }
}
```

<span data-ttu-id="143b6-889">예에서 `A` 비가상 방법이 도입 되었습니다 `F` 가상 메서드 및 `G`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-889">In the example, `A` introduces a non-virtual method `F` and a virtual method `G`.</span></span> <span data-ttu-id="143b6-890">클래스 `B` 새 비가상 방법이 도입 되었습니다 `F`, 따라서는 상속 된 변수 숨기기 `F`, 또한 상속 된 메서드를 재정의 하 고 `G`입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-890">The class `B` introduces a new non-virtual method `F`, thus hiding the inherited `F`, and also overrides the inherited method `G`.</span></span> <span data-ttu-id="143b6-891">이 예제에서는 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-891">The example produces the output:</span></span>
```
A.F
B.F
B.G
B.G
```

<span data-ttu-id="143b6-892">문이 `a.G()` 호출 `B.G`아니라 `A.G`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-892">Notice that the statement `a.G()` invokes `B.G`, not `A.G`.</span></span> <span data-ttu-id="143b6-893">인스턴스의 런타임 형식 이므로 (되 `B`), 인스턴스 컴파일 시간 형식이 아닌 (는 `A`), 호출할 실제 메서드 구현이 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-893">This is because the run-time type of the instance (which is `B`), not the compile-time type of the instance (which is `A`), determines the actual method implementation to invoke.</span></span>

<span data-ttu-id="143b6-894">있기 때문에 메서드를 상속 된 메서드를 숨길 수 동일한 서명 사용 하 여 여러 가상 메서드를 포함 하는 클래스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-894">Because methods are allowed to hide inherited methods, it is possible for a class to contain several virtual methods with the same signature.</span></span> <span data-ttu-id="143b6-895">이 가장 많이 파생 된 메서드를 제외한 모든 숨겨져 있으므로 모호성 문제를를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-895">This does not present an ambiguity problem, since all but the most derived method are hidden.</span></span> <span data-ttu-id="143b6-896">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-896">In the example</span></span>
```csharp
using System;

class A
{
    public virtual void F() { Console.WriteLine("A.F"); }
}

class B: A
{
    public override void F() { Console.WriteLine("B.F"); }
}

class C: B
{
    new public virtual void F() { Console.WriteLine("C.F"); }
}

class D: C
{
    public override void F() { Console.WriteLine("D.F"); }
}

class Test
{
    static void Main() {
        D d = new D();
        A a = d;
        B b = d;
        C c = d;
        a.F();
        b.F();
        c.F();
        d.F();
    }
}
```
<span data-ttu-id="143b6-897">`C` 하 고 `D` 시그니처가 동일한 두 개의 가상 메서드를 포함 하는 클래스:에서 도입 된 것 `A` 및에 도입 된 것 `C`.</span><span class="sxs-lookup"><span data-stu-id="143b6-897">the `C` and `D` classes contain two virtual methods with the same signature: The one introduced by `A` and the one introduced by `C`.</span></span> <span data-ttu-id="143b6-898">도입 된 메서드 `C` 에서 상속 된 메서드를 숨깁니다. `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-898">The method introduced by `C` hides the method inherited from `A`.</span></span> <span data-ttu-id="143b6-899">따라서의 재정의 선언이 `D` 에서 도입 된 메서드를 재정의 `C`, 수 이며 `D` 도입 된 메서드를 재정의 하 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-899">Thus, the override declaration in `D` overrides the method introduced by `C`, and it is not possible for `D` to override the method introduced by `A`.</span></span> <span data-ttu-id="143b6-900">이 예제에서는 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-900">The example produces the output:</span></span>
```
B.F
B.F
D.F
D.F
```

<span data-ttu-id="143b6-901">인스턴스에 액세스 하 여 숨겨진된 가상 메서드를 호출할 수는 `D` 작음 통해 파생 형식이 없는 메서드 숨겨져 있지 않으면입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-901">Note that it is possible to invoke the hidden virtual method by accessing an instance of `D` through a less derived type in which the method is not hidden.</span></span>

### <a name="override-methods"></a><span data-ttu-id="143b6-902">메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-902">Override methods</span></span>

<span data-ttu-id="143b6-903">인스턴스 메서드 선언 포함 되는 경우는 `override` 한정자를 메서드 라고는 ***메서드를 재정의***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-903">When an instance method declaration includes an `override` modifier, the method is said to be an ***override method***.</span></span> <span data-ttu-id="143b6-904">재정의 메서드 시그니처가 같은 상속된 된 가상 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-904">An override method overrides an inherited virtual method with the same signature.</span></span> <span data-ttu-id="143b6-905">가상 메서드 선언은 새 메서드를 도입하지만 재정의 메서드 선언은 해당 메서드의 새 구현을 제공하여 기존의 상속된 가상 메서드를 특수화합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-905">Whereas a virtual method declaration introduces a new method, an override method declaration specializes an existing inherited virtual method by providing a new implementation of that method.</span></span>

<span data-ttu-id="143b6-906">에 의해 재정의 메서드는 `override` 선언 이라고 합니다 ***기본 메서드를 재정의***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-906">The method overridden by an `override` declaration is known as the ***overridden base method***.</span></span> <span data-ttu-id="143b6-907">재정의 메서드에 대 한 `M` 클래스에 선언 `C`, 재정의 된 기본 메서드는 각 기본 클래스 유형의 검사 하 여 결정 됩니다 `C`부터 시작 하 여 직접 기본 클래스 형식의 `C` 각 진행 및 연속 직접 기본 클래스 형식에 지정 된 기본 클래스 형식에 액세스할 수 있는 메서드는 하나 이상 있는 때까지 동일한 서명을 가진 `M` 형식 인수의 대체 후 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-907">For an override method `M` declared in a class `C`, the overridden base method is determined by examining each base class type of `C`, starting with the direct base class type of `C` and continuing with each successive direct base class type, until in a given base class type at least one accessible method is located which has the same signature as `M` after substitution of type arguments.</span></span> <span data-ttu-id="143b6-908">재정의 된 기본 메서드를 찾기 위해, 메서드 있으면 액세스할 수 있는 비율은 `public`있으면 `protected`있으면 `protected internal`, 인스턴스인 경우 `internal` 같은 프로그램에서 선언 된 `C`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-908">For the purposes of locating the overridden base method, a method is considered accessible if it is `public`, if it is `protected`, if it is `protected internal`, or if it is `internal` and declared in the same program as `C`.</span></span>

<span data-ttu-id="143b6-909">컴파일 타임 오류가 발생 하는 다음의 모든 재정의 선언에 대해 충족 되지 않으면:</span><span class="sxs-lookup"><span data-stu-id="143b6-909">A compile-time error occurs unless all of the following are true for an override declaration:</span></span>

*  <span data-ttu-id="143b6-910">재정의 된 기본 메서드는 위에서 설명한 대로 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-910">An overridden base method can be located as described above.</span></span>
*  <span data-ttu-id="143b6-911">이러한 재정의 된 기본 메서드가 정확히 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-911">There is exactly one such overridden base method.</span></span> <span data-ttu-id="143b6-912">이 제한은 기본 클래스 형식을 생성 된 형식인 위치 형식 인수의 대체 하면 서명이 두 가지 방법 중 동일한 경우에 효과가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-912">This restriction has effect only if the base class type is a constructed type where the substitution of type arguments makes the signature of two methods the same.</span></span>
*  <span data-ttu-id="143b6-913">재정의 된 기본 메서드는 가상, 추상 되었거나 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-913">The overridden base method is a virtual, abstract, or override method.</span></span> <span data-ttu-id="143b6-914">즉, 재정의 된 기본 메서드는 정적 또는 가상 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-914">In other words, the overridden base method cannot be static or non-virtual.</span></span>
*  <span data-ttu-id="143b6-915">재정의 된 기본 메서드를 봉인된 메서드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-915">The overridden base method is not a sealed method.</span></span>
*  <span data-ttu-id="143b6-916">재정의 메서드 및 재정의 된 기본 메서드는 동일한 형식이 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-916">The override method and the overridden base method have the same return type.</span></span>
*  <span data-ttu-id="143b6-917">재정의 선언 및 재정의 된 기본 메서드 선언 된 접근성이 동일한 경우</span><span class="sxs-lookup"><span data-stu-id="143b6-917">The override declaration and the overridden base method have the same declared accessibility.</span></span> <span data-ttu-id="143b6-918">즉, 재정의 선언 가상 메서드의 접근성을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-918">In other words, an override declaration cannot change the accessibility of the virtual method.</span></span> <span data-ttu-id="143b6-919">그러나 재정의 된 기본 메서드는 내부 보호 되 고 선언 재정의 메서드를 재정의 메서드를 포함 하는 어셈블리 보다 다른 어셈블리에 선언 된 접근성 보호 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-919">However, if the overridden base method is protected internal and it is declared in a different assembly than the assembly containing the override method then the override method's declared accessibility must be protected.</span></span>
*  <span data-ttu-id="143b6-920">재정의 선언에서 형식 매개 변수-제약 조건 절을 지정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-920">The override declaration does not specify type-parameter-constraints-clauses.</span></span> <span data-ttu-id="143b6-921">대신 제약 조건은 재정의 된 기본 메서드에서 상속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-921">Instead the constraints are inherited from the overridden base method.</span></span> <span data-ttu-id="143b6-922">참고는 재정의 된 메서드의 형식 매개 변수는 제약 조건을 상속 된 제약 조건에 대 한 형식 인수 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-922">Note that constraints that are type parameters in the overridden method may be replaced by type arguments in the inherited constraint.</span></span> <span data-ttu-id="143b6-923">이 잘못 되었습니다. 값 형식 또는 sealed 형식 등과 같은 명시적으로 지정 하는 경우 제약 조건에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-923">This can lead to constraints that are not legal when explicitly specified, such as value types or sealed types.</span></span>

<span data-ttu-id="143b6-924">다음 예제에서는 제네릭 클래스에 대 한 재정의 규칙이 어떻게 작동 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-924">The following example demonstrates how the overriding rules work for generic classes:</span></span>
```csharp
abstract class C<T>
{
    public virtual T F() {...}
    public virtual C<T> G() {...}
    public virtual void H(C<T> x) {...}
}

class D: C<string>
{
    public override string F() {...}            // Ok
    public override C<string> G() {...}         // Ok
    public override void H(C<T> x) {...}        // Error, should be C<string>
}

class E<T,U>: C<U>
{
    public override U F() {...}                 // Ok
    public override C<U> G() {...}              // Ok
    public override void H(C<T> x) {...}        // Error, should be C<U>
}
```

<span data-ttu-id="143b6-925">재정의 선언 재정의 된 기본 메서드를 통해 액세스할 수는 *base_access* ([액세스를 기본](expressions.md#base-access)).</span><span class="sxs-lookup"><span data-stu-id="143b6-925">An override declaration can access the overridden base method using a *base_access* ([Base access](expressions.md#base-access)).</span></span> <span data-ttu-id="143b6-926">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-926">In the example</span></span>
```csharp
class A
{
    int x;

    public virtual void PrintFields() {
        Console.WriteLine("x = {0}", x);
    }
}

class B: A
{
    int y;

    public override void PrintFields() {
        base.PrintFields();
        Console.WriteLine("y = {0}", y);
    }
}
```
<span data-ttu-id="143b6-927">`base.PrintFields()` 에서 호출 `B` 를 호출 하는 `PrintFields` 에 선언 된 메서드 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-927">the `base.PrintFields()` invocation in `B` invokes the `PrintFields` method declared in `A`.</span></span> <span data-ttu-id="143b6-928">A *base_access* 가상 호출 메커니즘을 사용 하지 않도록 설정 하 고 단순히 비가상 메서드로 기본 메서드를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-928">A *base_access* disables the virtual invocation mechanism and simply treats the base method as a non-virtual method.</span></span> <span data-ttu-id="143b6-929">호출 했습니다 `B` 된 기록 `((A)this).PrintFields()`, 재귀적으로 것 호출를 `PrintFields` 에 선언 된 메서드 `B`, 아니라 선언 `A`, 있으므로 `PrintFields` 가상 및 런타임 유형의 `((A)this)` 는 `B`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-929">Had the invocation in `B` been written `((A)this).PrintFields()`, it would recursively invoke the `PrintFields` method declared in `B`, not the one declared in `A`, since `PrintFields` is virtual and the run-time type of `((A)this)` is `B`.</span></span>

<span data-ttu-id="143b6-930">포함 하 여만 `override` 한정자 수 메서드는 다른 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-930">Only by including an `override` modifier can a method override another method.</span></span> <span data-ttu-id="143b6-931">다른 모든 경우에서 상속 된 메서드와 동일한 시그니처가 있는 메서드는 단순히 상속 된 메서드를 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-931">In all other cases, a method with the same signature as an inherited method simply hides the inherited method.</span></span> <span data-ttu-id="143b6-932">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-932">In the example</span></span>
```csharp
class A
{
    public virtual void F() {}
}

class B: A
{
    public virtual void F() {}        // Warning, hiding inherited F()
}
```
<span data-ttu-id="143b6-933">`F` 의 메서드 `B` 포함 되지 않습니다는 `override` 한정자 재정의 되지 않습니다 및 합니다 `F` 에서 메서드 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-933">the `F` method in `B` does not include an `override` modifier and therefore does not override the `F` method in `A`.</span></span> <span data-ttu-id="143b6-934">대신 합니다 `F` 에서 메서드 `B` 메서드를 숨기 `A`, 및 선언에 포함 되지 않아 보고 되는 경고를 `new` 한정자.</span><span class="sxs-lookup"><span data-stu-id="143b6-934">Rather, the `F` method in `B` hides the method in `A`, and a warning is reported because the declaration does not include a `new` modifier.</span></span>

<span data-ttu-id="143b6-935">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-935">In the example</span></span>
```csharp
class A
{
    public virtual void F() {}
}

class B: A
{
    new private void F() {}        // Hides A.F within body of B
}

class C: B
{
    public override void F() {}    // Ok, overrides A.F
}
```
<span data-ttu-id="143b6-936">합니다 `F` 의 메서드 `B` 가상 숨깁니다 `F` 에서 상속 된 메서드 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-936">the `F` method in `B` hides the virtual `F` method inherited from `A`.</span></span> <span data-ttu-id="143b6-937">새 이후 `F` 에 `B` 개인 액세스 권한이 해당 범위에만 클래스 본문에 포함 `B` 로 확장 되지 않습니다 및 `C`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-937">Since the new `F` in `B` has private access, its scope only includes the class body of `B` and does not extend to `C`.</span></span> <span data-ttu-id="143b6-938">따라서 선언은 `F` 에서 `C` 를 재정의할 수는 `F` 에서 상속 되며, `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-938">Therefore, the declaration of `F` in `C` is permitted to override the `F` inherited from `A`.</span></span>

### <a name="sealed-methods"></a><span data-ttu-id="143b6-939">봉인된 메서드</span><span class="sxs-lookup"><span data-stu-id="143b6-939">Sealed methods</span></span>

<span data-ttu-id="143b6-940">인스턴스 메서드 선언 포함 되는 경우는 `sealed` 한정자, 메서드를 라고 하는 ***메서드를 봉인***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-940">When an instance method declaration includes a `sealed` modifier, that method is said to be a ***sealed method***.</span></span> <span data-ttu-id="143b6-941">인스턴스 메서드 선언에 포함 된 경우는 `sealed` 한정자를 포함 해야 합니다 `override` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-941">If an instance method declaration includes the  `sealed` modifier, it must also include the `override` modifier.</span></span> <span data-ttu-id="143b6-942">사용 된 `sealed` 한정자는 파생된 클래스에서 추가 메서드를 재정의 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-942">Use of the `sealed` modifier prevents a derived class from further overriding the method.</span></span>

<span data-ttu-id="143b6-943">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-943">In the example</span></span>
```csharp
using System;

class A
{
    public virtual void F() {
        Console.WriteLine("A.F");
    }

    public virtual void G() {
        Console.WriteLine("A.G");
    }
}

class B: A
{
    sealed override public void F() {
        Console.WriteLine("B.F");
    } 

    override public void G() {
        Console.WriteLine("B.G");
    } 
}

class C: B
{
    override public void G() {
        Console.WriteLine("C.G");
    } 
}
```
<span data-ttu-id="143b6-944">클래스 `B` 메서드를 재정의 하는 두 가지 제공:는 `F` 변수가 있는 메서드는 `sealed` 한정자 및 `G` 하지 않는 메서드.</span><span class="sxs-lookup"><span data-stu-id="143b6-944">the class `B` provides two override methods: an `F` method that has the `sealed` modifier and a `G` method that does not.</span></span> <span data-ttu-id="143b6-945">`B`봉인 된 사용의 `modifier` 방지 `C` 추가로 재정의에서 `F`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-945">`B`'s use of the sealed `modifier` prevents `C` from further overriding `F`.</span></span>

### <a name="abstract-methods"></a><span data-ttu-id="143b6-946">추상 메서드</span><span class="sxs-lookup"><span data-stu-id="143b6-946">Abstract methods</span></span>

<span data-ttu-id="143b6-947">인스턴스 메서드 선언 포함 되는 경우는 `abstract` 한정자, 메서드를 라고 하는 ***추상 메서드에***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-947">When an instance method declaration includes an `abstract` modifier, that method is said to be an ***abstract method***.</span></span> <span data-ttu-id="143b6-948">한정자를 가질 수 없습니다 경우에 추상 메서드를 암시적으로 가상 메서드 `virtual`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-948">Although an abstract method is implicitly also a virtual method, it cannot have the modifier `virtual`.</span></span>

<span data-ttu-id="143b6-949">추상 메서드 선언은 새 가상 메서드로 있지만 해당 메서드의 구현을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-949">An abstract method declaration introduces a new virtual method but does not provide an implementation of that method.</span></span> <span data-ttu-id="143b6-950">대신, 비추상 파생된 클래스는 메서드를 재정의 하 여 고유한 구현을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-950">Instead, non-abstract derived classes are required to provide their own implementation by overriding that method.</span></span> <span data-ttu-id="143b6-951">추상 메서드 구현을 제공 하지 않으므로 실제, 합니다 *method_body* 추상 메서드는 세미콜론 구성 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-951">Because an abstract method provides no actual implementation, the *method_body* of an abstract method simply consists of a semicolon.</span></span>

<span data-ttu-id="143b6-952">추상 메서드 선언은 추상 클래스 에서만 허용 됩니다 ([추상 클래스](classes.md#abstract-classes)).</span><span class="sxs-lookup"><span data-stu-id="143b6-952">Abstract method declarations are only permitted in abstract classes ([Abstract classes](classes.md#abstract-classes)).</span></span>

<span data-ttu-id="143b6-953">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-953">In the example</span></span>
```csharp
public abstract class Shape
{
    public abstract void Paint(Graphics g, Rectangle r);
}

public class Ellipse: Shape
{
    public override void Paint(Graphics g, Rectangle r) {
        g.DrawEllipse(r);
    }
}

public class Box: Shape
{
    public override void Paint(Graphics g, Rectangle r) {
        g.DrawRect(r);
    }
}
```
<span data-ttu-id="143b6-954">`Shape` 클래스 자체를 그릴 수 있는 기하학적 도형 개체의 추상 개념을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-954">the `Shape` class defines the abstract notion of a geometrical shape object that can paint itself.</span></span> <span data-ttu-id="143b6-955">`Paint` 방법은 추상 때문에 의미 있는 기본값을 구현 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-955">The `Paint` method is abstract because there is no meaningful default implementation.</span></span> <span data-ttu-id="143b6-956">합니다 `Ellipse` 하 고 `Box` 클래스는 구체적인 `Shape` 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-956">The `Ellipse` and `Box` classes are concrete `Shape` implementations.</span></span> <span data-ttu-id="143b6-957">이러한 클래스는 추상 이기 때문에 이러한 재정의 해야 하는 `Paint` 메서드 및 실제 구현을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-957">Because these classes are non-abstract, they are required to override the `Paint` method and provide an actual implementation.</span></span>

<span data-ttu-id="143b6-958">에 대 한 컴파일 시간 오류를 *base_access* ([액세스를 기본](expressions.md#base-access)) 추상 메서드를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-958">It is a compile-time error for a *base_access* ([Base access](expressions.md#base-access)) to reference an abstract method.</span></span> <span data-ttu-id="143b6-959">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-959">In the example</span></span>
```csharp
abstract class A
{
    public abstract void F();
}

class B: A
{
    public override void F() {
        base.F();                        // Error, base.F is abstract
    }
}
```
<span data-ttu-id="143b6-960">에 대 한 컴파일 타임 오류가 보고 되는 `base.F()` 호출 추상 메서드를 참조 하기 때문에 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-960">a compile-time error is reported for the `base.F()` invocation because it references an abstract method.</span></span>

<span data-ttu-id="143b6-961">추상 메서드 선언은 가상 메서드를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-961">An abstract method declaration is permitted to override a virtual method.</span></span> <span data-ttu-id="143b6-962">이 강제로 다시 파생된 클래스에서 메서드를 구현 하는 추상 클래스를 허용 하며 메서드의 원래 구현을 사용할 수 없게 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-962">This allows an abstract class to force re-implementation of the method in derived classes, and makes the original implementation of the method unavailable.</span></span> <span data-ttu-id="143b6-963">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-963">In the example</span></span>
```csharp
using System;

class A
{
    public virtual void F() {
        Console.WriteLine("A.F");
    }
}

abstract class B: A
{
    public abstract override void F();
}

class C: B
{
    public override void F() {
        Console.WriteLine("C.F");
    }
}
```
<span data-ttu-id="143b6-964">클래스 `A` 가상 메서드를 클래스 선언 `B` 추상 메서드 및 클래스를 사용 하 여이 메서드를 재정의 `C` 자체 구현을 제공 하기 위해 추상 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-964">class `A` declares a virtual method, class `B` overrides this method with an abstract method, and class `C` overrides the abstract method to provide its own implementation.</span></span>

### <a name="external-methods"></a><span data-ttu-id="143b6-965">외부 메서드</span><span class="sxs-lookup"><span data-stu-id="143b6-965">External methods</span></span>

<span data-ttu-id="143b6-966">메서드 선언을 포함 하는 경우는 `extern` 한정자, 메서드를 라고 하는 ***외부 메서드의***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-966">When a method declaration includes an `extern` modifier, that method is said to be an ***external method***.</span></span> <span data-ttu-id="143b6-967">외부 메서드는 일반적으로 C# 이외의 언어를 사용 하 여 외부적으로 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-967">External methods are implemented externally, typically using a language other than C#.</span></span> <span data-ttu-id="143b6-968">외부 메서드 선언은 실제 구현을 제공 하기 때문에 합니다 *method_body* 외부 메서드의 세미콜론의 구성 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-968">Because an external method declaration provides no actual implementation, the *method_body* of an external method simply consists of a semicolon.</span></span> <span data-ttu-id="143b6-969">외부 메서드를 제네릭일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-969">An external method may not be generic.</span></span>

<span data-ttu-id="143b6-970">합니다 `extern` 한정자와 함께에서 일반적으로 사용 됩니다는 `DllImport` 특성 ([Win32 및 COM 구성 요소와 상호 운용](attributes.md#interoperation-with-com-and-win32-components)), Dll (동적 연결 라이브러리)에 의해 구현 되어야 하는 외부 메서드를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-970">The `extern` modifier is typically used in conjunction with a `DllImport` attribute ([Interoperation with COM and Win32 components](attributes.md#interoperation-with-com-and-win32-components)), allowing external methods to be implemented by DLLs (Dynamic Link Libraries).</span></span> <span data-ttu-id="143b6-971">실행 환경 외부 메서드의 구현을 제공할 수 있습니다 가능해 집니다 다른 메커니즘을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-971">The execution environment may support other mechanisms whereby implementations of external methods can be provided.</span></span>

<span data-ttu-id="143b6-972">외부 메서드를 포함 하는 경우는 `DllImport` 특성인 메서드 선언도 포함 해야 합니다는 `static` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-972">When an external method includes a `DllImport` attribute, the method declaration must also include a `static` modifier.</span></span> <span data-ttu-id="143b6-973">이 예제에서는 사용 합니다 `extern` 한정자와 `DllImport` 특성:</span><span class="sxs-lookup"><span data-stu-id="143b6-973">This example demonstrates the use of the `extern` modifier and the `DllImport` attribute:</span></span>
```csharp
using System.Text;
using System.Security.Permissions;
using System.Runtime.InteropServices;

class Path
{
    [DllImport("kernel32", SetLastError=true)]
    static extern bool CreateDirectory(string name, SecurityAttribute sa);

    [DllImport("kernel32", SetLastError=true)]
    static extern bool RemoveDirectory(string name);

    [DllImport("kernel32", SetLastError=true)]
    static extern int GetCurrentDirectory(int bufSize, StringBuilder buf);

    [DllImport("kernel32", SetLastError=true)]
    static extern bool SetCurrentDirectory(string name);
}
```

### <a name="partial-methods-recap"></a><span data-ttu-id="143b6-974">부분 메서드 (정리)</span><span class="sxs-lookup"><span data-stu-id="143b6-974">Partial methods (recap)</span></span>

<span data-ttu-id="143b6-975">메서드 선언을 포함 하는 경우는 `partial` 한정자, 메서드를 라고 하는 ***부분 메서드***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-975">When a method declaration includes a `partial` modifier, that method is said to be a ***partial method***.</span></span> <span data-ttu-id="143b6-976">부분 메서드는 부분 형식의 멤버로 선언할 수 있습니다 ([부분 형식](classes.md#partial-types)), 여러 가지 제한이 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-976">Partial methods can only be declared as members of partial types ([Partial types](classes.md#partial-types)), and are subject to a number of restrictions.</span></span> <span data-ttu-id="143b6-977">부분 메서드에 추가로 나와 [부분 메서드](classes.md#partial-methods)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-977">Partial methods are further described in [Partial methods](classes.md#partial-methods).</span></span>

### <a name="extension-methods"></a><span data-ttu-id="143b6-978">확장 메서드</span><span class="sxs-lookup"><span data-stu-id="143b6-978">Extension methods</span></span>

<span data-ttu-id="143b6-979">메서드의 첫 번째 매개 변수를 포함 하는 경우는 `this` 한정자, 메서드를 라고 하는 ***확장 메서드***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-979">When the first parameter of a method includes the `this` modifier, that method is said to be an ***extension method***.</span></span> <span data-ttu-id="143b6-980">확장 메서드는 제네릭이 아닌 비중첩 정적 클래스에서 선언할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-980">Extension methods can only be declared in non-generic, non-nested static classes.</span></span> <span data-ttu-id="143b6-981">확장 메서드의 첫 번째 매개 변수는 이외의 없습니다 한정자를 사용할 수 있습니다 `this`, 및 매개 변수 형식에 대 한 포인터 형식일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-981">The first parameter of an extension method can have no modifiers other than `this`, and the parameter type cannot be a pointer type.</span></span>

<span data-ttu-id="143b6-982">다음은 예제 확장 메서드를 선언 하는 정적 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-982">The following is an example of a static class that declares two extension methods:</span></span>
```csharp
public static class Extensions
{
    public static int ToInt32(this string s) {
        return Int32.Parse(s);
    }

    public static T[] Slice<T>(this T[] source, int index, int count) {
        if (index < 0 || count < 0 || source.Length - index < count)
            throw new ArgumentException();
        T[] result = new T[count];
        Array.Copy(source, index, result, 0, count);
        return result;
    }
}
```

<span data-ttu-id="143b6-983">확장 메서드는 일반 정적 메서드.</span><span class="sxs-lookup"><span data-stu-id="143b6-983">An extension method is a regular static method.</span></span> <span data-ttu-id="143b6-984">또한 정적 바깥쪽 클래스 범위에 있는 확장 메서드를 호출할 수 인스턴스 메서드 호출 구문을 사용 하 여 ([확장 메서드 호출](expressions.md#extension-method-invocations)), 받는 사람 식을 첫 번째 인수로 사용 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-984">In addition, where its enclosing static class is in scope, an extension method can be invoked using instance method invocation syntax ([Extension method invocations](expressions.md#extension-method-invocations)), using the receiver expression as the first argument.</span></span>

<span data-ttu-id="143b6-985">다음 프로그램은 위에서 선언 된 확장 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-985">The following program uses the extension methods declared above:</span></span>
```csharp
static class Program
{
    static void Main() {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in strings.Slice(1, 2)) {
            Console.WriteLine(s.ToInt32());
        }
    }
}
```

<span data-ttu-id="143b6-986">`Slice` 메서드는에서 사용할 수는 `string[]`, 및 `ToInt32` 메서드는에서 사용할 수 `string`이므로 확장 메서드로 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-986">The `Slice` method is available on the `string[]`, and the `ToInt32` method is available on `string`, because they have been declared as extension methods.</span></span> <span data-ttu-id="143b6-987">프로그램의 의미는 다음을 사용 하 여 일반 정적 메서드 호출과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-987">The meaning of the program is the same as the following, using ordinary static method calls:</span></span>
```csharp
static class Program
{
    static void Main() {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in Extensions.Slice(strings, 1, 2)) {
            Console.WriteLine(Extensions.ToInt32(s));
        }
    }
}
```

### <a name="method-body"></a><span data-ttu-id="143b6-988">메서드 본문</span><span class="sxs-lookup"><span data-stu-id="143b6-988">Method body</span></span>

<span data-ttu-id="143b6-989">합니다 *method_body* 메서드 선언에 블록 본문을 식 본문이 또는 세미콜론으로 하는 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-989">The *method_body* of a method declaration consists of either a block body, an expression body or a semicolon.</span></span>

<span data-ttu-id="143b6-990">합니다 ***결과 형식이*** 메서드는 `void` 반환 형식이 `void`, 경우 메서드는 비동기 반환 형식 또는 `System.Threading.Tasks.Task`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-990">The ***result type*** of a method is `void` if the return type is `void`, or if the method is async and the return type is `System.Threading.Tasks.Task`.</span></span> <span data-ttu-id="143b6-991">비동기 메서드의 결과 형식을 해당 반환 형식이 며 반환 형식 사용 하 여 비동기 메서드의 결과 형식이 고, 그렇지 `System.Threading.Tasks.Task<T>` 는 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-991">Otherwise, the result type of a non-async method is its return type, and the result type of an async method with return type `System.Threading.Tasks.Task<T>` is `T`.</span></span>

<span data-ttu-id="143b6-992">메서드가 경우를 `void` 형식을 한 블록 본문을 발생 `return` 문 ([return 문을](statements.md#the-return-statement)) 블록에서 허용 되지 않습니다는 식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-992">When a method has a `void` result type and a block body, `return` statements ([The return statement](statements.md#the-return-statement)) in the block are not permitted to specify an expression.</span></span> <span data-ttu-id="143b6-993">Void 메서드는 블록의 실행 정상적으로 완료 되는 경우 (즉, 제어 흐름이 메서드 본문의 끝)는 메서드를 단순히 현재 호출자에 게 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-993">If execution of the block of a void method completes normally (that is, control flows off the end of the method body), that method simply returns to its current caller.</span></span>
    
<span data-ttu-id="143b6-994">메서드가 경우는 `void` 결과 식 본문을 식 `E` 이어야 합니다는 *statement_expression*, 본문은 폼의 블록 본문을 동일 하 고 `{ E; }`.</span><span class="sxs-lookup"><span data-stu-id="143b6-994">When a method has a `void` result and an expression body, the expression `E` must be a *statement_expression*, and the body is exactly equivalent to a block body of the form `{ E; }`.</span></span>
    
<span data-ttu-id="143b6-995">메서드는 void가 아닌 결과 형식이 면 및 블록 본문을 각 `return` 블록의 문은 결과 유형으로 암시적으로 변환할 수 있는 식을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-995">When a method has a non-void result type and a block body, each `return` statement in the block must specify an expression that is implicitly convertible to the result type.</span></span> <span data-ttu-id="143b6-996">끝점 값 반환 하는 메서드에 블록 본문을 연결할 수 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-996">The endpoint of a block body of a value-returning method must not be reachable.</span></span> <span data-ttu-id="143b6-997">즉, 블록 본문을 사용 하 여 값을 반환 메서드에서 제어 흐름 메서드 본문의 끝에 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-997">In other words, in a value-returning method with a block body, control is not permitted to flow off the end of the method body.</span></span>
    
<span data-ttu-id="143b6-998">메서드는 void가 아닌 결과 형식이 있고 식 본문이 식 결과 형식으로 암시적으로 변환할 수 있어야 하 고 본문은 폼의 블록 본문을 동일 `{ return E; }`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-998">When a method has a non-void result type and an expression body, the expression must be implicitly convertible to the result type, and the body is exactly equivalent to a block body of the form `{ return E; }`.</span></span>
    
<span data-ttu-id="143b6-999">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-999">In the example</span></span>
```csharp
class A
{
    public int F() {}            // Error, return value required

    public int G() {
        return 1;
    }

    public int H(bool b) {
        if (b) {
            return 1;
        }
        else {
            return 0;
        }
    }

    public int I(bool b) => b ? 1 : 0;
}
```
<span data-ttu-id="143b6-1000">값 반환 `F` 컨트롤 메서드 본문의 끝을 벗어날 수 있으므로 메서드는 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1000">the value-returning `F` method results in a compile-time error because control can flow off the end of the method body.</span></span> <span data-ttu-id="143b6-1001">합니다 `G` 고 `H` return 문의 반환 값을 지정 하는 모든 가능한 실행 경로 종료 되므로 메서드는 올바른 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1001">The `G` and `H` methods are correct because all possible execution paths end in a return statement that specifies a return value.</span></span> <span data-ttu-id="143b6-1002">`I` 메서드 올바른지 이므로 해당 본문에 단일 return 문으로을 사용 하 여 문 블록에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1002">The `I` method is correct, because its body is equivalent to a statement block with just a single return statement in it.</span></span>

### <a name="method-overloading"></a><span data-ttu-id="143b6-1003">메서드 오버로드</span><span class="sxs-lookup"><span data-stu-id="143b6-1003">Method overloading</span></span>

<span data-ttu-id="143b6-1004">메서드 오버 로드 확인 규칙에 설명 되어 있습니다 [형식 유추](expressions.md#type-inference)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1004">The method overload resolution rules are described in [Type inference](expressions.md#type-inference).</span></span>

## <a name="properties"></a><span data-ttu-id="143b6-1005">속성</span><span class="sxs-lookup"><span data-stu-id="143b6-1005">Properties</span></span>

<span data-ttu-id="143b6-1006">A ***속성*** 는 개체 또는 클래스의 특징에 대 한 액세스를 제공 하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1006">A ***property*** is a member that provides access to a characteristic of an object or a class.</span></span> <span data-ttu-id="143b6-1007">속성의 예로, 고객의 이름 창의 캡션 글꼴의 크기 문자열의 길이 등에입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1007">Examples of properties include the length of a string, the size of a font, the caption of a window, the name of a customer, and so on.</span></span> <span data-ttu-id="143b6-1008">속성은 필드의 기본 확장-모두 연결 된 형식이 멤버 라고 하며 필드 및 속성에 액세스 하기 위한 구문은 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1008">Properties are a natural extension of fields—both are named members with associated types, and the syntax for accessing fields and properties is the same.</span></span> <span data-ttu-id="143b6-1009">그러나 필드와 달리 속성은 저장 위치를 명시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1009">However, unlike fields, properties do not denote storage locations.</span></span> <span data-ttu-id="143b6-1010">대신, 속성에는 해당 값을 읽거나 쓸 때 실행될 문을 지정하는 ***접근자***가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1010">Instead, properties have ***accessors*** that specify the statements to be executed when their values are read or written.</span></span> <span data-ttu-id="143b6-1011">속성 읽기 및 쓰기; 개체의 특성을 사용 하 여 작업을 연결 하기 위한 메커니즘을 제공 하므로 또한 이러한 특성을 계산할 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1011">Properties thus provide a mechanism for associating actions with the reading and writing of an object's attributes; furthermore, they permit such attributes to be computed.</span></span>

<span data-ttu-id="143b6-1012">속성은 사용 하 여 선언 됩니다 *property_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="143b6-1012">Properties are declared using *property_declaration*s:</span></span>

```antlr
property_declaration
    : attributes? property_modifier* type member_name property_body
    ;

property_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'static'
    | 'virtual'
    | 'sealed'
    | 'override'
    | 'abstract'
    | 'extern'
    | property_modifier_unsafe
    ;

property_body
    : '{' accessor_declarations '}' property_initializer?
    | '=>' expression ';'
    ;

property_initializer
    : '=' variable_initializer ';'
    ;
```

<span data-ttu-id="143b6-1013">A *property_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)) 및 네 가지 액세스 한정자의 유효한 조합이 ([액세스 한정자 ](classes.md#access-modifiers)), `new` ([새 한정자](classes.md#the-new-modifier)), `static` ([정적 메서드와 인스턴스](classes.md#static-and-instance-methods)), `virtual` ([가상메서드](classes.md#virtual-methods)), `override` ([메서드를 재정의](classes.md#override-methods)), `sealed` ([메서드를 봉인](classes.md#sealed-methods)), `abstract` ([추상 메서드](classes.md#abstract-methods)), 및 `extern` ([외부 메서드](classes.md#external-methods)) 한정자.</span><span class="sxs-lookup"><span data-stu-id="143b6-1013">A *property_declaration* may include a set of *attributes* ([Attributes](attributes.md)) and a valid combination of the four access modifiers ([Access modifiers](classes.md#access-modifiers)), the `new` ([The new modifier](classes.md#the-new-modifier)),  `static` ([Static and instance methods](classes.md#static-and-instance-methods)), `virtual` ([Virtual methods](classes.md#virtual-methods)), `override` ([Override methods](classes.md#override-methods)), `sealed` ([Sealed methods](classes.md#sealed-methods)), `abstract` ([Abstract methods](classes.md#abstract-methods)), and `extern` ([External methods](classes.md#external-methods)) modifiers.</span></span>

<span data-ttu-id="143b6-1014">속성 선언을 메서드 선언으로 동일한 규칙이 적용 됩니다 ([메서드](classes.md#methods)) 한정자의 유효한 조합을 관련 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1014">Property declarations are subject to the same rules as method declarations ([Methods](classes.md#methods)) with regard to valid combinations of modifiers.</span></span>

<span data-ttu-id="143b6-1015">합니다 *형식* 선언 속성의 선언에서 도입 된 속성의 종류를 지정 하며 *member_name* 속성의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1015">The *type* of a property declaration specifies the type of the property introduced by the declaration, and the *member_name* specifies the name of the property.</span></span> <span data-ttu-id="143b6-1016">속성에는 명시적 인터페이스 멤버 구현이 아닌 합니다 *member_name* 는 단순히 *식별자*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1016">Unless the property is an explicit interface member implementation, the *member_name* is simply an *identifier*.</span></span> <span data-ttu-id="143b6-1017">명시적 인터페이스 멤버 구현에 대 한 ([명시적 인터페이스 멤버 구현을](interfaces.md#explicit-interface-member-implementations)), *member_name* 이루어져는 *interface_type* 뒤에 " `.`"및 *식별자*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1017">For an explicit interface member implementation ([Explicit interface member implementations](interfaces.md#explicit-interface-member-implementations)), the *member_name* consists of an *interface_type* followed by a "`.`" and an *identifier*.</span></span>

<span data-ttu-id="143b6-1018">합니다 *형식* 속성의 해야 적어도 속성 자체 만큼 액세스 가능 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1018">The *type* of a property must be at least as accessible as the property itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

<span data-ttu-id="143b6-1019">A *property_body* 하나 구성 될 수 있습니다는 ***접근자 본문*** 요소나 ***식 본문***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1019">A *property_body* may either consist of an ***accessor body*** or an ***expression body***.</span></span> <span data-ttu-id="143b6-1020">접근자 본문을 *accessor_declarations*는 묶어야 "`{`"및"`}`" 접근자를 선언 하는 토큰 ([접근자](classes.md#accessors)) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1020">In an accessor body,  *accessor_declarations*, which must be enclosed in "`{`" and "`}`" tokens, declare the accessors ([Accessors](classes.md#accessors)) of the property.</span></span> <span data-ttu-id="143b6-1021">접근자에는 읽기 및 쓰기 속성을 사용 하 여 연결 된 실행 가능 문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1021">The accessors specify the executable statements associated with reading and writing the property.</span></span>

<span data-ttu-id="143b6-1022">구성 된 식 본문이 `=>` 뒤에 *식을* `E` 세미콜론은 문 본문을 동일 하 고 `{ get { return E; } }`, 따라서 사용할 수 있습니다만 getter 전용으로 지정 하 고 속성 getter의 결과가 단일 식을 사용 하 여 여기서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1022">An expression body consisting of `=>` followed by an *expression* `E` and a semicolon is exactly equivalent to the statement body `{ get { return E; } }`, and can therefore only be used to specify getter-only properties where the result of the getter is given by a single expression.</span></span>

<span data-ttu-id="143b6-1023">A *property_initializer* 자동으로 구현 된 속성에 부여 될 수 있습니다 ([자동으로 구현 된 속성](classes.md#automatically-implemented-properties)), 이러한 내부 필드를 초기화 하 고 지정 된 값을 사용 하 여 속성을 *식*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1023">A *property_initializer* may only be given for an automatically implemented property ([Automatically implemented properties](classes.md#automatically-implemented-properties)), and causes the initialization of the underlying field of such properties with the value given by the *expression*.</span></span>

<span data-ttu-id="143b6-1024">경우에 속성에 액세스 하는 구문은 동일 필드, 속성을 분류 되지 않은 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1024">Even though the syntax for accessing a property is the same as that for a field, a property is not classified as a variable.</span></span> <span data-ttu-id="143b6-1025">따라서 불가능 속성으로 전달 하는 `ref` 또는 `out` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1025">Thus, it is not possible to pass a property as a `ref` or `out` argument.</span></span>

<span data-ttu-id="143b6-1026">속성 선언을 포함 하는 경우는 `extern` 한정자를 속성 이라고는 ***외부 속성***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1026">When a property declaration includes an `extern` modifier, the property is said to be an ***external property***.</span></span> <span data-ttu-id="143b6-1027">외부 속성 선언에는 각 실제 구현을 제공 하기 때문에 해당 *accessor_declarations* 세미콜론으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1027">Because an external property declaration provides no actual implementation, each of its *accessor_declarations* consists of a semicolon.</span></span>

### <a name="static-and-instance-properties"></a><span data-ttu-id="143b6-1028">정적 및 인스턴스 속성</span><span class="sxs-lookup"><span data-stu-id="143b6-1028">Static and instance properties</span></span>

<span data-ttu-id="143b6-1029">속성 선언을 포함 하는 경우는 `static` 한정자를 속성 이라고는 ***정적 속성***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1029">When a property declaration includes a `static` modifier, the property is said to be a ***static property***.</span></span> <span data-ttu-id="143b6-1030">없는 경우 `static` 한정자가 있는 속성 이라고는 ***속성을 인스턴스***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1030">When no `static` modifier is present, the property is said to be an ***instance property***.</span></span>

<span data-ttu-id="143b6-1031">정적 속성 특정 인스턴스와 연결 되며 컴파일 타임 오류를 가리키는 데 `this` 정적 속성의 접근자에서.</span><span class="sxs-lookup"><span data-stu-id="143b6-1031">A static property is not associated with a specific instance, and it is a compile-time error to refer to `this` in the accessors of a static property.</span></span>

<span data-ttu-id="143b6-1032">인스턴스 속성을 클래스의 특정 인스턴스와 연결 되며으로 해당 인스턴스에 액세스할 수 있습니다 `this` ([이 액세스](expressions.md#this-access))에서 해당 속성의 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1032">An instance property is associated with a given instance of a class, and that instance can be accessed as `this` ([This access](expressions.md#this-access)) in the accessors of that property.</span></span>

<span data-ttu-id="143b6-1033">속성에서 참조 되는 경우는 *member_access* ([멤버 액세스](expressions.md#member-access)) 형식의 `E.M`이면 `M` 정적 속성인 `E` 를포함하는형식을표시해야합니다`M`, 경우에 `M` 인스턴스 속성을 E를 포함 하는 형식 인스턴스의 나타내야 `M`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1033">When a property is referenced in a *member_access* ([Member access](expressions.md#member-access)) of the form `E.M`, if `M` is a static property, `E` must denote a type containing `M`, and if `M` is an instance property, E must denote an instance of a type containing `M`.</span></span>

<span data-ttu-id="143b6-1034">정적 간의 차이점 및 인스턴스 멤버 설명에 대 한 자세한 [정적 및 인스턴스 멤버](classes.md#static-and-instance-members)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1034">The differences between static and instance members are discussed further in [Static and instance members](classes.md#static-and-instance-members).</span></span>

### <a name="accessors"></a><span data-ttu-id="143b6-1035">접근자</span><span class="sxs-lookup"><span data-stu-id="143b6-1035">Accessors</span></span>

<span data-ttu-id="143b6-1036">합니다 *accessor_declarations* 속성 읽기 및 쓰기 속성을 사용 하 여 연결 된 실행 가능 문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1036">The *accessor_declarations* of a property specify the executable statements associated with reading and writing that property.</span></span>

```antlr
accessor_declarations
    : get_accessor_declaration set_accessor_declaration?
    | set_accessor_declaration get_accessor_declaration?
    ;

get_accessor_declaration
    : attributes? accessor_modifier? 'get' accessor_body
    ;

set_accessor_declaration
    : attributes? accessor_modifier? 'set' accessor_body
    ;

accessor_modifier
    : 'protected'
    | 'internal'
    | 'private'
    | 'protected' 'internal'
    | 'internal' 'protected'
    ;

accessor_body
    : block
    | ';'
    ;
```

<span data-ttu-id="143b6-1037">접근자 선언을 이루어진를 *get_accessor_declaration*, *set_accessor_declaration*, 또는 둘 다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1037">The accessor declarations consist of a *get_accessor_declaration*, a *set_accessor_declaration*, or both.</span></span> <span data-ttu-id="143b6-1038">각 접근자 선언의 토큰 이루어져 `get` 또는 `set` 뒤에 선택적인 *accessor_modifier* 와 *accessor_body*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1038">Each accessor declaration consists of the token `get` or `set` followed by an optional *accessor_modifier* and an *accessor_body*.</span></span>

<span data-ttu-id="143b6-1039">사용 *accessor_modifier*s 다음과 같은 제한 사항이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1039">The use of *accessor_modifier*s is governed by the following restrictions:</span></span>

*  <span data-ttu-id="143b6-1040">*accessor_modifier* 인터페이스 또는 명시적 인터페이스 멤버 구현에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1040">An *accessor_modifier* may not be used in an interface or in an explicit interface member implementation.</span></span>
*  <span data-ttu-id="143b6-1041">속성 또는 인덱서가 없는 `override` 한정자는 *accessor_modifier* 속성 또는 인덱서는 둘 다 포함 하는 경우에 허용 됩니다는 `get` 및 `set` 접근자 중 하나에 허용 됩니다 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1041">For a property or indexer that has no `override` modifier, an *accessor_modifier* is permitted only if the property or indexer has both a `get` and `set` accessor, and then is permitted only on one of those accessors.</span></span>
*  <span data-ttu-id="143b6-1042">속성 또는 인덱서를 포함 하는 `override` 한정자가 접근자와 일치 해야 합니다는 *accessor_modifier*재정의 접근자의 경우.</span><span class="sxs-lookup"><span data-stu-id="143b6-1042">For a property or indexer that includes an `override` modifier, an accessor must match the *accessor_modifier*, if any, of the accessor being overridden.</span></span>
*  <span data-ttu-id="143b6-1043">합니다 *accessor_modifier* 속성 또는 인덱서 자체의 선언 된 접근성 보다 더 엄격 하 게 제한적인 접근성을 선언 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1043">The *accessor_modifier* must declare an accessibility that is strictly more restrictive than the declared accessibility of the property or indexer itself.</span></span> <span data-ttu-id="143b6-1044">정확 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1044">To be precise:</span></span>
   * <span data-ttu-id="143b6-1045">선언 된 접근성 속성 또는 인덱서 수 있는지 `public`는 *accessor_modifier* 중 하나일 수 있습니다 `protected internal`를 `internal`를 `protected`, 또는 `private`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1045">If the property or indexer has a declared accessibility of `public`, the *accessor_modifier* may be either `protected internal`, `internal`, `protected`, or `private`.</span></span>
   * <span data-ttu-id="143b6-1046">선언 된 접근성 속성 또는 인덱서 수 있는지 `protected internal`는 *accessor_modifier* 중 하나일 수 있습니다 `internal`에 `protected`, 또는 `private`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1046">If the property or indexer has a declared accessibility of `protected internal`, the *accessor_modifier* may be either `internal`, `protected`, or `private`.</span></span>
   * <span data-ttu-id="143b6-1047">선언 된 접근성 속성 또는 인덱서 수 있는지 `internal` 또는 `protected`서 *accessor_modifier* 여야 합니다 `private`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1047">If the property or indexer has a declared accessibility of `internal` or `protected`, the *accessor_modifier* must be `private`.</span></span>
   * <span data-ttu-id="143b6-1048">선언 된 접근성 속성 또는 인덱서 수 있는지 `private`, no *accessor_modifier* 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1048">If the property or indexer has a declared accessibility of `private`, no *accessor_modifier* may be used.</span></span>

<span data-ttu-id="143b6-1049">에 대 한 `abstract` 하 고 `extern` 속성을 *accessor_body* 지정 된 각 접근자는 단순히 세미콜론에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1049">For `abstract` and `extern` properties, the *accessor_body* for each accessor specified is simply a semicolon.</span></span> <span data-ttu-id="143b6-1050">각 extern이 아닌 비추상 속성 있을 *accessor_body* 세미콜론 일 경우에서는 ***자동으로 구현 된 속성*** ([자동으로 구현 된 속성 ](classes.md#automatically-implemented-properties)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1050">A non-abstract, non-extern property may have each *accessor_body* be a semicolon, in which case it is an ***automatically implemented property*** ([Automatically implemented properties](classes.md#automatically-implemented-properties)).</span></span> <span data-ttu-id="143b6-1051">자동으로 구현 된 속성 get 접근자를 하나 이상 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1051">An automatically implemented property must have at least a get accessor.</span></span> <span data-ttu-id="143b6-1052">모든 다른 비추상, extern이 아닌 속성의 접근자에는 *accessor_body* 는 *블록* 해당 접근자가 호출 될 때 실행할 문을 지정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1052">For the accessors of any other non-abstract, non-extern property, the *accessor_body* is a *block* which specifies the statements to be executed when the corresponding accessor is invoked.</span></span>

<span data-ttu-id="143b6-1053">`get` 접근자는 속성 형식의 반환 값을 사용 하 여 매개 변수가 없는 메서드에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1053">A `get` accessor corresponds to a parameterless method with a return value of the property type.</span></span> <span data-ttu-id="143b6-1054">속성 식에서 참조 될 때 할당의 대상으로 제외 합니다 `get` 속성의 접근자 속성의 값을 계산 하기 위해 호출 되 ([식의 값](expressions.md#values-of-expressions)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1054">Except as the target of an assignment, when a property is referenced in an expression, the `get` accessor of the property is invoked to compute the value of the property ([Values of expressions](expressions.md#values-of-expressions)).</span></span> <span data-ttu-id="143b6-1055">본문을 `get` 접근자는 값을 반환 하는 것에 대 한 규칙을 따라야 합니다에 설명 된 메서드 [메서드 본문](classes.md#method-body)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1055">The body of a `get` accessor must conform to the rules for value-returning methods described in [Method body](classes.md#method-body).</span></span> <span data-ttu-id="143b6-1056">특히, 모든 `return` 문의 본문에는 `get` 접근자 속성 형식을 암시적으로 변환할 수 있는 식을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1056">In particular, all `return` statements in the body of a `get` accessor must specify an expression that is implicitly convertible to the property type.</span></span> <span data-ttu-id="143b6-1057">또한 끝점을 `get` 접근자를 연결할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1057">Furthermore, the endpoint of a `get` accessor must not be reachable.</span></span>

<span data-ttu-id="143b6-1058">A `set` 접근자 메서드에 해당 하는 속성 형식의 단일 값 매개 변수를 사용 하 여 및 `void` 형식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1058">A `set` accessor corresponds to a method with a single value parameter of the property type and a `void` return type.</span></span> <span data-ttu-id="143b6-1059">암시적 매개 변수를 `set` 접근자의 이름은 항상 `value`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1059">The implicit parameter of a `set` accessor is always named `value`.</span></span> <span data-ttu-id="143b6-1060">속성이 할당의 대상으로 참조 되는 경우 ([대입 연산자](expressions.md#assignment-operators)), 또는의 피연산자로 `++` 하거나 `--` ([후 위 증가 및 감소 연산자](expressions.md#postfix-increment-and-decrement-operators), [ 전위 증가 및 감소 연산자](expressions.md#prefix-increment-and-decrement-operators)), `set` 인수를 사용 하 여 접근자가 호출 됩니다 (의 피연산자 또는 할당의 오른쪽에 있는 값인 합니다 `++` 또는 `--` 연산자)는 새 값을 제공 합니다 ([단순 할당](expressions.md#simple-assignment)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1060">When a property is referenced as the target of an assignment ([Assignment operators](expressions.md#assignment-operators)), or as the operand of `++` or `--` ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators), [Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)), the `set` accessor is invoked with an argument (whose value is that of the right-hand side of the assignment or the operand of the `++` or `--` operator) that provides the new value ([Simple assignment](expressions.md#simple-assignment)).</span></span> <span data-ttu-id="143b6-1061">본문을 `set` 접근자에 대 한 규칙을 따라야 `void` 에 설명 된 방법을 [메서드 본문](classes.md#method-body)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1061">The body of a `set` accessor must conform to the rules for `void` methods described in [Method body](classes.md#method-body).</span></span> <span data-ttu-id="143b6-1062">특히 `return` 문에서 `set` 접근자 본문 식을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1062">In particular, `return` statements in the `set` accessor body are not permitted to specify an expression.</span></span> <span data-ttu-id="143b6-1063">있으므로 `set` 접근자에는 암시적으로 명명 된 매개 변수가 `value`에서 지역 변수 또는 상수 선언에 대 한 컴파일 시간 오류가 발생을 `set` 해당 이름을 가진 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1063">Since a `set` accessor implicitly has a parameter named `value`, it is a compile-time error for a local variable or constant declaration in a `set` accessor to have that name.</span></span>

<span data-ttu-id="143b6-1064">유무에 따라 합니다 `get` 및 `set` 접근자 속성을 다음과 같이 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1064">Based on the presence or absence of the `get` and `set` accessors, a property is classified as follows:</span></span>

*  <span data-ttu-id="143b6-1065">모두 포함 하는 속성을 `get` 접근자 및 `set` 접근자를 라고는 ***읽기 / 쓰기*** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1065">A property that includes both a `get` accessor and a `set` accessor is said to be a ***read-write*** property.</span></span>
*  <span data-ttu-id="143b6-1066">만 있는 속성을 `get` 접근자를 라고는 ***읽기 전용*** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1066">A property that has only a `get` accessor is said to be a ***read-only*** property.</span></span> <span data-ttu-id="143b6-1067">이 할당 대상일 수 읽기 전용 속성에 대 한 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1067">It is a compile-time error for a read-only property to be the target of an assignment.</span></span>
*  <span data-ttu-id="143b6-1068">만 있는 속성을 `set` 접근자를 라고는 ***쓰기 전용*** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1068">A property that has only a `set` accessor is said to be a ***write-only*** property.</span></span> <span data-ttu-id="143b6-1069">제외 할당의 대상으로는 쓰기 전용 속성 식에서 참조 하는 컴파일 타임 오류가 것입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1069">Except as the target of an assignment, it is a compile-time error to reference a write-only property in an expression.</span></span>

<span data-ttu-id="143b6-1070">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-1070">In the example</span></span>
```csharp
public class Button: Control
{
    private string caption;

    public string Caption {
        get {
            return caption;
        }
        set {
            if (caption != value) {
                caption = value;
                Repaint();
            }
        }
    }

    public override void Paint(Graphics g, Rectangle r) {
        // Painting code goes here
    }
}
```
<span data-ttu-id="143b6-1071">합니다 `Button` 컨트롤에는 공용 선언 `Caption` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1071">the `Button` control declares a public `Caption` property.</span></span> <span data-ttu-id="143b6-1072">`get` 의 접근자는 `Caption` 개인에 저장 된 문자열을 반환 하는 속성 `caption` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1072">The `get` accessor of the `Caption` property returns the string stored in the private `caption` field.</span></span> <span data-ttu-id="143b6-1073">`set` 접근자는 새 값이 현재 값과 다른 경우 새 값을 저장 및 확인 하 고 컨트롤을 다시 그립니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1073">The `set` accessor checks if the new value is different from the current value, and if so, it stores the new value and repaints the control.</span></span> <span data-ttu-id="143b6-1074">속성 위에 표시 된 패턴을 따르는 경우가 많습니다:는 `get` 접근자는 단순히 개인 필드에 저장 된 값을 반환 하며 `set` 접근자는 private 필드를 수정 하 고 완벽 하 게 상태를 업데이트 하는 데 필요한 모든 추가 작업을 수행 합니다 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1074">Properties often follow the pattern shown above: The `get` accessor simply returns a value stored in a private field, and the `set` accessor modifies that private field and then performs any additional actions required to fully update the state of the object.</span></span>

<span data-ttu-id="143b6-1075">지정 된 `Button` 위의 사용 되는 클래스, 다음은 사용의 예로 `Caption` 속성:</span><span class="sxs-lookup"><span data-stu-id="143b6-1075">Given the `Button` class above, the following is an example of use of the `Caption` property:</span></span>
```csharp
Button okButton = new Button();
okButton.Caption = "OK";            // Invokes set accessor
string s = okButton.Caption;        // Invokes get accessor
```

<span data-ttu-id="143b6-1076">여기에 `set` 속성에 값을 할당 하 여 접근자가 호출 및 `get` 접근자는 속성 식에서 참조 하 여 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1076">Here, the `set` accessor is invoked by assigning a value to the property, and the `get` accessor is invoked by referencing the property in an expression.</span></span>

<span data-ttu-id="143b6-1077">합니다 `get` 및 `set` 접근자 속성의 고유 멤버는 이므로 속성의 접근자를 개별적으로 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1077">The `get` and `set` accessors of a property are not distinct members, and it is not possible to declare the accessors of a property separately.</span></span> <span data-ttu-id="143b6-1078">따라서 서로 다른 액세스 가능성을 갖도록 하는 읽기 / 쓰기 속성의 두 접근자에 대 한 가능한 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1078">As such, it is not possible for the two accessors of a read-write property to have different accessibility.</span></span> <span data-ttu-id="143b6-1079">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-1079">The example</span></span>
```csharp
class A
{
    private string name;

    public string Name {                // Error, duplicate member name
        get { return name; }
    }

    public string Name {                // Error, duplicate member name
        set { name = value; }
    }
}
```
<span data-ttu-id="143b6-1080">단일 읽기 / 쓰기 속성을 선언 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1080">does not declare a single read-write property.</span></span> <span data-ttu-id="143b6-1081">대신, 읽기 전용으로 하나는 동일한 이름의 두 속성을 선언 하 고 쓰기 전용 하나.</span><span class="sxs-lookup"><span data-stu-id="143b6-1081">Rather, it declares two properties with the same name, one read-only and one write-only.</span></span> <span data-ttu-id="143b6-1082">동일한 클래스에 선언 된 두 명의 멤버 이름이 가질 수 있으므로 예제는 컴파일 타임 오류가 발생 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1082">Since two members declared in the same class cannot have the same name, the example causes a compile-time error to occur.</span></span>

<span data-ttu-id="143b6-1083">상속 된 속성으로 같은 이름의 속성을 선언 하는 파생된 클래스에서 파생 된 속성 읽기와 쓰기에 대해 상속 된 속성을 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1083">When a derived class declares a property by the same name as an inherited property, the derived property hides the inherited property with respect to both reading and writing.</span></span> <span data-ttu-id="143b6-1084">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-1084">In the example</span></span>
```csharp
class A
{
    public int P {
        set {...}
    }
}

class B: A
{
    new public int P {
        get {...}
    }
}
```
<span data-ttu-id="143b6-1085">`P` 속성에서 `B` 숨깁니다 합니다 `P` 속성에서 `A` 읽기와 쓰기에 대해 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1085">the `P` property in `B` hides the `P` property in `A` with respect to both reading and writing.</span></span> <span data-ttu-id="143b6-1086">따라서 문에서</span><span class="sxs-lookup"><span data-stu-id="143b6-1086">Thus, in the statements</span></span>
```csharp
B b = new B();
b.P = 1;          // Error, B.P is read-only
((A)b).P = 1;     // Ok, reference to A.P
```
<span data-ttu-id="143b6-1087">에 대 한 할당 `b.P` 이후 읽기 전용 보고 컴파일 타임 오류가 발생 `P` 속성에서 `B` 쓰기 전용 숨깁니다 `P` 속성에서 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1087">the assignment to `b.P` causes a compile-time error to be reported, since the read-only `P` property in `B` hides the write-only `P` property in `A`.</span></span> <span data-ttu-id="143b6-1088">단, 숨겨진 액세스 하는 캐스트를 사용할 수 있도록 `P` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1088">Note, however, that a cast can be used to access the hidden `P` property.</span></span>

<span data-ttu-id="143b6-1089">공용 필드와 달리 속성 개체의 내부 상태와 해당 공용 인터페이스 간의 분리를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1089">Unlike public fields, properties provide a separation between an object's internal state and its public interface.</span></span> <span data-ttu-id="143b6-1090">예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1090">Consider the example:</span></span>
```csharp
class Label
{
    private int x, y;
    private string caption;

    public Label(int x, int y, string caption) {
        this.x = x;
        this.y = y;
        this.caption = caption;
    }

    public int X {
        get { return x; }
    }

    public int Y {
        get { return y; }
    }

    public Point Location {
        get { return new Point(x, y); }
    }

    public string Caption {
        get { return caption; }
    }
}
```

<span data-ttu-id="143b6-1091">여기에 `Label` 클래스는 두 개의 `int` 필드 `x` 및 `y`, 해당 위치를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1091">Here, the `Label` class uses two `int` fields, `x` and `y`, to store its location.</span></span> <span data-ttu-id="143b6-1092">위치는 공개적으로으로 노출 되는 `X` 및 `Y` 속성와는 `Location` 형식의 속성 `Point`.</span><span class="sxs-lookup"><span data-stu-id="143b6-1092">The location is publicly exposed both as an `X` and a `Y` property and as a `Location` property of type `Point`.</span></span> <span data-ttu-id="143b6-1093">나중 버전의 경우 `Label`, 위치를 저장 하는 편리한 되기를 `Point` 변경 클래스의 공용 인터페이스에 영향을 주지 않고 내부적으로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1093">If, in a future version of `Label`, it becomes more convenient to store the location as a `Point` internally, the change can be made without affecting the public interface of the class:</span></span>
```csharp
class Label
{
    private Point location;
    private string caption;

    public Label(int x, int y, string caption) {
        this.location = new Point(x, y);
        this.caption = caption;
    }

    public int X {
        get { return location.x; }
    }

    public int Y {
        get { return location.y; }
    }

    public Point Location {
        get { return location; }
    }

    public string Caption {
        get { return caption; }
    }
}
```

<span data-ttu-id="143b6-1094">했습니다 `x` 하 고 `y` 대신 되었습니다 `public readonly` 필드 것이 더 하지를 이러한 변경 수는 `Label` 클래스.</span><span class="sxs-lookup"><span data-stu-id="143b6-1094">Had `x` and `y` instead been `public readonly` fields, it would have been impossible to make such a change to the `Label` class.</span></span>

<span data-ttu-id="143b6-1095">상태 속성을 통해 노출 필드를 직접 노출 하는 경우 반드시 만큼 효율적 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1095">Exposing state through properties is not necessarily any less efficient than exposing fields directly.</span></span> <span data-ttu-id="143b6-1096">특히 속성은 비가상 약간의 코드가 포함을 실행 환경에는 접근자의 실제 코드를 사용 하 여 접근자에 대 한 호출을 대체할 수 있으며.</span><span class="sxs-lookup"><span data-stu-id="143b6-1096">In particular, when a property is non-virtual and contains only a small amount of code, the execution environment may replace calls to accessors with the actual code of the accessors.</span></span> <span data-ttu-id="143b6-1097">이 프로세스는 이라고 ***인라인***, 속성 액세스를 효율적으로 필드 액세스를 사용 하면 아직 속성의 뛰어난 유연성을 유지 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1097">This process is known as ***inlining***, and it makes property access as efficient as field access, yet preserves the increased flexibility of properties.</span></span>

<span data-ttu-id="143b6-1098">호출 이후를 `get` 접근자의 필드 값을 읽는 개념적으로 동일, 잘못 된 프로그래밍 스타일에 대 한 것으로 간주 됩니다 `get` observable 의도 하지 않은 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1098">Since invoking a `get` accessor is conceptually equivalent to reading the value of a field, it is considered bad programming style for `get` accessors to have observable side-effects.</span></span> <span data-ttu-id="143b6-1099">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-1099">In the example</span></span>
```csharp
class Counter
{
    private int next;

    public int Next {
        get { return next++; }
    }
}
```
<span data-ttu-id="143b6-1100">값을 `Next` 속성 속성에 이전에 액세스 하는 횟수에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1100">the value of the `Next` property depends on the number of times the property has previously been accessed.</span></span> <span data-ttu-id="143b6-1101">따라서 눈에 띄는-부작용을 생성 속성에 액세스 하 고 대신 속성을 메서드로 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1101">Thus, accessing the property produces an observable side-effect, and the property should be implemented as a method instead.</span></span>

<span data-ttu-id="143b6-1102">"의도" 규칙에 대 한 `get` 접근자는 한다고 `get` 접근자 단순히 필드에 저장 된 값을 반환 하도록 항상 작성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1102">The "no side-effects" convention for `get` accessors doesn't mean that `get` accessors should always be written to simply return values stored in fields.</span></span> <span data-ttu-id="143b6-1103">실제로 `get` 접근자 종종 여러 필드에 액세스 하거나 메서드를 호출 하 여 속성의 값을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1103">Indeed, `get` accessors often compute the value of a property by accessing multiple fields or invoking methods.</span></span> <span data-ttu-id="143b6-1104">그러나 제대로 설계 된 `get` 접근자 개체의 상태 observable 변경 시키는 없는 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1104">However, a properly designed `get` accessor performs no actions that cause observable changes in the state of the object.</span></span>

<span data-ttu-id="143b6-1105">속성을 사용 하 여 처음 참조 될 때까지 리소스의 초기화를 지연 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1105">Properties can be used to delay initialization of a resource until the moment it is first referenced.</span></span> <span data-ttu-id="143b6-1106">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="143b6-1106">For example:</span></span>
```csharp
using System.IO;

public class Console
{
    private static TextReader reader;
    private static TextWriter writer;
    private static TextWriter error;

    public static TextReader In {
        get {
            if (reader == null) {
                reader = new StreamReader(Console.OpenStandardInput());
            }
            return reader;
        }
    }

    public static TextWriter Out {
        get {
            if (writer == null) {
                writer = new StreamWriter(Console.OpenStandardOutput());
            }
            return writer;
        }
    }

    public static TextWriter Error {
        get {
            if (error == null) {
                error = new StreamWriter(Console.OpenStandardError());
            }
            return error;
        }
    }
}
```

<span data-ttu-id="143b6-1107">합니다 `Console` 세 가지 속성이 포함 된 클래스 `In`, `Out`, 및 `Error`는 표준 입력, 출력 및 오류 장치 각각 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1107">The `Console` class contains three properties, `In`, `Out`, and `Error`, that represent the standard input, output, and error devices, respectively.</span></span> <span data-ttu-id="143b6-1108">이러한 멤버 속성으로 노출 하 여는 `Console` 실제로 사용 될 때까지 클래스 초기화를 지연 시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1108">By exposing these members as properties, the `Console` class can delay their initialization until they are actually used.</span></span> <span data-ttu-id="143b6-1109">예를 들어, 첫 번째 참조 시는 `Out` 에서처럼 속성</span><span class="sxs-lookup"><span data-stu-id="143b6-1109">For example, upon first referencing the `Out` property, as in</span></span>
```csharp
Console.Out.WriteLine("hello, world");
```
<span data-ttu-id="143b6-1110">기본 `TextWriter` 출력 장치 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1110">the underlying `TextWriter` for the output device is created.</span></span> <span data-ttu-id="143b6-1111">응용 프로그램에 대 한 참조를 만들면 하지만 합니다 `In` 및 `Error` 해당 장치에 대 한 속성을 다음 개체가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1111">But if the application makes no reference to the `In` and `Error` properties, then no objects are created for those devices.</span></span>

### <a name="automatically-implemented-properties"></a><span data-ttu-id="143b6-1112">자동으로 구현 된 속성</span><span class="sxs-lookup"><span data-stu-id="143b6-1112">Automatically implemented properties</span></span>

<span data-ttu-id="143b6-1113">자동으로 구현 된 속성 (또는 ***auto 속성*** 줄여서), 세미콜론으로 전용 접근자 본문을 사용 하 여 추상이 아닌 extern이 아닌 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1113">An automatically implemented property (or ***auto-property*** for short), is a non-abstract non-extern property with semicolon-only accessor bodies.</span></span> <span data-ttu-id="143b6-1114">Auto 속성 get 접근자가 있어야 합니다 및 set 접근자를 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1114">Auto-properties must have a get accessor and can optionally have a set accessor.</span></span>

<span data-ttu-id="143b6-1115">속성을 자동으로 구현 된 속성으로 지정 하면 숨겨진된 지원 필드를 속성에 대해 자동으로 제공 되며 지원 필드를 읽고 접근자 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1115">When a property is specified as an automatically implemented property, a hidden backing field is automatically available for the property, and the accessors are implemented to read from and write to that backing field.</span></span> <span data-ttu-id="143b6-1116">Auto 속성 set 접근자가 없는, 지원 필드 것으로 간주 됩니다 `readonly` ([읽기 전용 필드](classes.md#readonly-fields)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1116">If the auto-property has no set accessor, the backing field is considered `readonly` ([Readonly fields](classes.md#readonly-fields)).</span></span> <span data-ttu-id="143b6-1117">마찬가지로 `readonly` 필드에는 getter 전용 auto 속성 할당할 수도 있습니다를 바깥쪽 클래스의 생성자의 본문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1117">Just like a `readonly` field, a getter-only auto-property can also be assigned to in the body of a constructor of the enclosing class.</span></span> <span data-ttu-id="143b6-1118">속성의 읽기 전용 지원 필드에 직접 할당을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1118">Such an assignment assigns directly to the readonly backing field of the property.</span></span>

<span data-ttu-id="143b6-1119">Auto 속성을 가질 수도 있습니다는 *property_initializer*,으로 지원 필드에 직접 적용 되는 *variable_initializer* ([변수 이니셜라이저](classes.md#variable-initializers)) .</span><span class="sxs-lookup"><span data-stu-id="143b6-1119">An auto-property may optionally have a *property_initializer*, which is applied directly to the backing field as a *variable_initializer* ([Variable initializers](classes.md#variable-initializers)).</span></span>

<span data-ttu-id="143b6-1120">다음 예제:</span><span class="sxs-lookup"><span data-stu-id="143b6-1120">The following example:</span></span>
```csharp
public class Point {
    public int X { get; set; } = 0;
    public int Y { get; set; } = 0;
}
```
<span data-ttu-id="143b6-1121">다음 선언에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1121">is equivalent to the following declaration:</span></span>
```csharp
public class Point {
    private int __x = 0;
    private int __y = 0;
    public int X { get { return __x; } set { __x = value; } }
    public int Y { get { return __y; } set { __y = value; } }
}
```

<span data-ttu-id="143b6-1122">다음 예제:</span><span class="sxs-lookup"><span data-stu-id="143b6-1122">The following example:</span></span>
```csharp
public class ReadOnlyPoint
{
    public int X { get; }
    public int Y { get; }
    public ReadOnlyPoint(int x, int y) { X = x; Y = y; }
}
```
<span data-ttu-id="143b6-1123">다음 선언에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1123">is equivalent to the following declaration:</span></span>
```csharp
public class ReadOnlyPoint
{
    private readonly int __x;
    private readonly int __y;
    public int X { get { return __x; } }
    public int Y { get { return __y; } }
    public ReadOnlyPoint(int x, int y) { __x = x; __y = y; }
}
```

<span data-ttu-id="143b6-1124">읽기 전용 필드에 할당 된 유효 생성자 내에서 발생 하기 때문에 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1124">Notice that the assignments to the readonly field are legal, because they occur within the constructor.</span></span>


### <a name="accessibility"></a><span data-ttu-id="143b6-1125">액세스 가능성</span><span class="sxs-lookup"><span data-stu-id="143b6-1125">Accessibility</span></span>

<span data-ttu-id="143b6-1126">접근자에는 *accessor_modifier*를 액세스 가능 도메인 ([접근성 도메인](basic-concepts.md#accessibility-domains))의 선언 된 접근성을 사용 하 여 결정 됩니다 접근자의는 *accessor_modifier* .</span><span class="sxs-lookup"><span data-stu-id="143b6-1126">If an accessor has an *accessor_modifier*, the accessibility domain ([Accessibility domains](basic-concepts.md#accessibility-domains)) of the accessor is determined using the declared accessibility of the *accessor_modifier*.</span></span> <span data-ttu-id="143b6-1127">접근자에 없는 경우는 *accessor_modifier*, 접근자의 접근성 도메인은 속성 또는 인덱서의 선언된 된 액세스 가능성에서 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1127">If an accessor does not have an *accessor_modifier*, the accessibility domain of the accessor is determined from the declared accessibility of the property or indexer.</span></span>

<span data-ttu-id="143b6-1128">현재 상태를 *accessor_modifier* 멤버 조회에 영향을 미치지 ([연산자](expressions.md#operators)) 또는 오버 로드 확인 ([오버 로드 확인](expressions.md#overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1128">The presence of an *accessor_modifier* never affects member lookup ([Operators](expressions.md#operators)) or overload resolution ([Overload resolution](expressions.md#overload-resolution)).</span></span> <span data-ttu-id="143b6-1129">속성 또는 인덱서 한정자는 속성 또는 인덱서는 바인딩되는 액세스의 컨텍스트에서 관계 없이 항상 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1129">The modifiers on the property or indexer always determine which property or indexer is bound to, regardless of the context of the access.</span></span>

<span data-ttu-id="143b6-1130">특정 속성 또는 인덱서 선택 되 면 관련 된 특정 접근자의 접근성 도메인은 사용량 유효한 지 확인 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1130">Once a particular property or indexer has been selected, the accessibility domains of the specific accessors involved are used to determine if that usage is valid:</span></span>

*  <span data-ttu-id="143b6-1131">값으로 사용 되는 경우 ([식의 값](expressions.md#values-of-expressions)), `get` 접근자 존재 하며 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1131">If the usage is as a value ([Values of expressions](expressions.md#values-of-expressions)), the `get` accessor must exist and be accessible.</span></span>
*  <span data-ttu-id="143b6-1132">사용법은 단순한 할당을 대상으로 하는 경우 ([단순 할당](expressions.md#simple-assignment)), `set` 접근자 존재 하며 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1132">If the usage is as the target of a simple assignment ([Simple assignment](expressions.md#simple-assignment)), the `set` accessor must exist and be accessible.</span></span>
*  <span data-ttu-id="143b6-1133">복합 할당의 대상으로 사용 되는 경우 ([복합 할당](expressions.md#compound-assignment)), 또는 대상으로 합니다 `++` 또는 `--` 연산자 ([함수 멤버](expressions.md#function-members).9, [ 호출 식](expressions.md#invocation-expressions)), 두 합니다 `get` 접근자 및 `set` 접근자 존재 하며 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1133">If the usage is as the target of compound assignment ([Compound assignment](expressions.md#compound-assignment)), or as the target of the `++` or `--` operators ([Function members](expressions.md#function-members).9, [Invocation expressions](expressions.md#invocation-expressions)), both the `get` accessors and the `set` accessor must exist and be accessible.</span></span>

<span data-ttu-id="143b6-1134">다음 예제에서는 속성에에서 `A.Text` 속성에 의해 숨겨져 `B.Text`, 경우에 컨텍스트에서는 `set` 접근자가 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1134">In the following example, the property `A.Text` is hidden by the property `B.Text`, even in contexts where only the `set` accessor is called.</span></span> <span data-ttu-id="143b6-1135">반대로, 속성 `B.Count` 클래스에 액세스할 수 없는 `M`이므로 액세스할 수 있는 속성이 `A.Count` 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1135">In contrast, the property `B.Count` is not accessible to class `M`, so the accessible property `A.Count` is used instead.</span></span>

```csharp
class A
{
    public string Text {
        get { return "hello"; }
        set { }
    }

    public int Count {
        get { return 5; }
        set { }
    }
}

class B: A
{
    private string text = "goodbye"; 
    private int count = 0;

    new public string Text {
        get { return text; }
        protected set { text = value; }
    }

    new protected int Count { 
        get { return count; }
        set { count = value; }
    }
}

class M
{
    static void Main() {
        B b = new B();
        b.Count = 12;             // Calls A.Count set accessor
        int i = b.Count;          // Calls A.Count get accessor
        b.Text = "howdy";         // Error, B.Text set accessor not accessible
        string s = b.Text;        // Calls B.Text get accessor
    }
}
```

<span data-ttu-id="143b6-1136">인터페이스를 구현 하는 데 사용 되는 접근자 있을 수 없습니다는 *accessor_modifier*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1136">An accessor that is used to implement an interface may not have an *accessor_modifier*.</span></span> <span data-ttu-id="143b6-1137">인터페이스를 구현 해야 하나의 접근자가 사용 되었다면 다른 접근자를 사용 하 여 선언할 수 있습니다는 *accessor_modifier*:</span><span class="sxs-lookup"><span data-stu-id="143b6-1137">If only one accessor is used to implement an interface, the other accessor may be declared with an *accessor_modifier*:</span></span>
```csharp
public interface I
{
    string Prop { get; }
}

public class C: I
{
    public Prop {
        get { return "April"; }       // Must not have a modifier here
        internal set {...}            // Ok, because I.Prop has no set accessor
    }
}
```

### <a name="virtual-sealed-override-and-abstract-property-accessors"></a><span data-ttu-id="143b6-1138">Sealed, 가상, 재정 및 추상 속성 접근자</span><span class="sxs-lookup"><span data-stu-id="143b6-1138">Virtual, sealed, override, and abstract property accessors</span></span>

<span data-ttu-id="143b6-1139">`virtual` 속성 선언은 속성 접근자는 가상를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1139">A `virtual` property declaration specifies that the accessors of the property are virtual.</span></span> <span data-ttu-id="143b6-1140">`virtual` 한정자는 읽기 / 쓰기 속성의 접근자를 모두에 적용-읽기 / 쓰기 속성 하나만 접근자는 virtual 일 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1140">The `virtual` modifier applies to both accessors of a read-write property—it is not possible for only one accessor of a read-write property to be virtual.</span></span>

<span data-ttu-id="143b6-1141">`abstract` 속성 선언을 지정 속성의 접근자 가상 하지만 접근자의 실제 구현을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1141">An `abstract` property declaration specifies that the accessors of the property are virtual, but does not provide an actual implementation of the accessors.</span></span> <span data-ttu-id="143b6-1142">대신, 비추상 파생된 클래스 속성을 재정의 하 여 접근자에 대 한 자체 구현을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1142">Instead, non-abstract derived classes are required to provide their own implementation for the accessors by overriding the property.</span></span> <span data-ttu-id="143b6-1143">추상 속성 선언에 대 한 접근자 실제 구현을 제공 하기 때문에 해당 *accessor_body* 단순히를 세미콜론으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1143">Because an accessor for an abstract property declaration provides no actual implementation, its *accessor_body* simply consists of a semicolon.</span></span>

<span data-ttu-id="143b6-1144">모두 포함 하는 속성 선언을 합니다 `abstract` 및 `override` 속성 추상 이며 기본 속성을 재정의 한정자를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1144">A property declaration that includes both the `abstract` and `override` modifiers specifies that the property is abstract and overrides a base property.</span></span> <span data-ttu-id="143b6-1145">이러한 속성의 접근자도 추상입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1145">The accessors of such a property are also abstract.</span></span>

<span data-ttu-id="143b6-1146">추상 속성 선언은 추상 클래스 에서만 허용 됩니다 ([추상 클래스](classes.md#abstract-classes)). 지정 하는 속성 선언을 포함 하 여 파생된 클래스에서 상속된 된 가상 속성의 접근자를 재정의할 수 있습니다는 `override` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1146">Abstract property declarations are only permitted in abstract classes ([Abstract classes](classes.md#abstract-classes)).The accessors of an inherited virtual property can be overridden in a derived class by including a property declaration that specifies an `override` directive.</span></span> <span data-ttu-id="143b6-1147">이 ***재정의 속성 선언은***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1147">This is known as an ***overriding property declaration***.</span></span> <span data-ttu-id="143b6-1148">재정의 속성 선언은 새 속성을 선언 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1148">An overriding property declaration does not declare a new property.</span></span> <span data-ttu-id="143b6-1149">대신, 기존 가상 속성의 접근자의 구현을 단순히 특수화 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1149">Instead, it simply specializes the implementations of the accessors of an existing virtual property.</span></span>

<span data-ttu-id="143b6-1150">재정의 속성 선언은 상속 된 속성과 정확 하 게 동일한 액세스 가능성 한정자, 형식 및 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1150">An overriding property declaration must specify the exact same accessibility modifiers, type, and name as the inherited property.</span></span> <span data-ttu-id="143b6-1151">경우는 상속 된 경우 속성은 단일 접근자만 (즉, 상속 된 속성이 읽기 전용 또는 쓰기 전용), 재정의 속성에는 해당 접근자만 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1151">If the inherited property has only a single accessor (i.e., if the inherited property is read-only or write-only), the overriding property must include only that accessor.</span></span> <span data-ttu-id="143b6-1152">경우 상속 된 속성 접근자를 모두 포함 되어 있습니다 (즉, 경우 상속 된 속성은 읽기 / 쓰기), 재정의 속성은 단일 접근자 또는 접근자를 모두 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1152">If the inherited property includes both accessors (i.e., if the inherited property is read-write), the overriding property can include either a single accessor or both accessors.</span></span>

<span data-ttu-id="143b6-1153">재정의 속성 선언은 포함 될 수 있습니다는 `sealed` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1153">An overriding property declaration may include the `sealed` modifier.</span></span> <span data-ttu-id="143b6-1154">이 한정자를 사용 하는 추가 속성을 재정의에서 파생된 클래스를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1154">Use of this modifier prevents a derived class from further overriding the property.</span></span> <span data-ttu-id="143b6-1155">봉인 된 속성의 접근자도 봉인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1155">The accessors of a sealed property are also sealed.</span></span>

<span data-ttu-id="143b6-1156">선언 및 호출의 차이 제외 하 고 구문, 가상, sealed 재정 및 추상 접근자는 가상, sealed 재정 및 추상 메서드 똑같이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1156">Except for differences in declaration and invocation syntax, virtual, sealed, override, and abstract accessors behave exactly like virtual, sealed, override and abstract methods.</span></span> <span data-ttu-id="143b6-1157">규칙에서 설명 하는 특히 [가상 메서드](classes.md#virtual-methods), [메서드를 재정의](classes.md#override-methods)합니다 [메서드를 봉인](classes.md#sealed-methods), 및 [추상 메서드](classes.md#abstract-methods) 적용 처럼 접근자에는 해당 폼의 메서드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1157">Specifically, the rules described in [Virtual methods](classes.md#virtual-methods), [Override methods](classes.md#override-methods), [Sealed methods](classes.md#sealed-methods), and [Abstract methods](classes.md#abstract-methods) apply as if accessors were methods of a corresponding form:</span></span>

*  <span data-ttu-id="143b6-1158">`get` 접근자 메서드에 해당 하는 매개 변수가 없는 속성 형식 및 포함 하는 속성과 같은 한정자의 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1158">A `get` accessor corresponds to a parameterless method with a return value of the property type and the same modifiers as the containing property.</span></span>
*  <span data-ttu-id="143b6-1159">A `set` 접근자 메서드에 해당 하는 속성 형식의 단일 값 매개 변수를 사용 하 여를 `void` 형식 및 포함 하는 속성과 같은 한정자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1159">A `set` accessor corresponds to a method with a single value parameter of the property type, a `void` return type, and the same modifiers as the containing property.</span></span>

<span data-ttu-id="143b6-1160">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-1160">In the example</span></span>
```csharp
abstract class A
{
    int y;

    public virtual int X {
        get { return 0; }
    }

    public virtual int Y {
        get { return y; }
        set { y = value; }
    }

    public abstract int Z { get; set; }
}
```
<span data-ttu-id="143b6-1161">`X` 가상 읽기 전용 속성은 `Y` 은 가상 읽기 / 쓰기 속성 및 `Z` 추상 읽기 / 쓰기 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1161">`X` is a virtual read-only property, `Y` is a virtual read-write property, and `Z` is an abstract read-write property.</span></span> <span data-ttu-id="143b6-1162">때문에 `Z` 는 추상 클래스를 포함 하는 클래스 `A` 추상 선언도 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1162">Because `Z` is abstract, the containing class `A` must also be declared abstract.</span></span>

<span data-ttu-id="143b6-1163">파생 된 클래스 `A` 아래에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1163">A class that derives from `A` is show below:</span></span>
```csharp
class B: A
{
    int z;

    public override int X {
        get { return base.X + 1; }
    }

    public override int Y {
        set { base.Y = value < 0? 0: value; }
    }

    public override int Z {
        get { return z; }
        set { z = value; }
    }
}
```

<span data-ttu-id="143b6-1164">여기, 선언을 `X`, `Y`, 및 `Z` 속성 선언을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1164">Here, the declarations of `X`, `Y`, and `Z` are overriding property declarations.</span></span> <span data-ttu-id="143b6-1165">각 속성 선언 된 접근성 한정자, 형식 및 해당 상속 된 속성의 이름에 정확히 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1165">Each property declaration exactly matches the accessibility modifiers, type, and name of the corresponding inherited property.</span></span> <span data-ttu-id="143b6-1166">합니다 `get` 의 접근자 `X` 및 `set` 의 접근자 `Y` 사용 하 여는 `base` 상속 된 접근자에 액세스 하는 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1166">The `get` accessor of `X` and the `set` accessor of `Y` use the `base` keyword to access the inherited accessors.</span></span> <span data-ttu-id="143b6-1167">선언의 `Z` 추상 접근자를 모두 재정의-따라서 가지에서 해결 되지 않은 추상 함수 멤버 없이 `B`, 및 `B` 추상 클래스일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1167">The declaration of `Z` overrides both abstract accessors—thus, there are no outstanding abstract function members in `B`, and `B` is permitted to be a non-abstract class.</span></span>

<span data-ttu-id="143b6-1168">속성으로 선언 되는 경우는 `override`, 재정의 된 접근자 재정의 코드에 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1168">When a property is declared as an `override`, any overridden accessors must be accessible to the overriding code.</span></span> <span data-ttu-id="143b6-1169">또한 선언 된 접근성 및 접근자 속성 또는 인덱서 자체를 모두의 재정의 된 멤버의 형식과 접근자는 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1169">In addition, the declared accessibility of both the property or indexer itself, and of the accessors, must match that of the overridden member and accessors.</span></span> <span data-ttu-id="143b6-1170">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="143b6-1170">For example:</span></span>
```csharp
public class B
{
    public virtual int P {
        protected set {...}
        get {...}
    }
}

public class D: B
{
    public override int P {
        protected set {...}            // Must specify protected here
        get {...}                      // Must not have a modifier here
    }
}
```

## <a name="events"></a><span data-ttu-id="143b6-1171">이벤트</span><span class="sxs-lookup"><span data-stu-id="143b6-1171">Events</span></span>

<span data-ttu-id="143b6-1172">***이벤트*** 는 개체 또는 알림을 제공 하는 클래스를 사용 하도록 설정 하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1172">An ***event*** is a member that enables an object or class to provide notifications.</span></span> <span data-ttu-id="143b6-1173">클라이언트를 제공 하 여 이벤트에 대 한 실행 코드를 추가할 수 있습니다 ***이벤트 처리기***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1173">Clients can attach executable code for events by supplying ***event handlers***.</span></span>

<span data-ttu-id="143b6-1174">이벤트를 사용 하 여 선언 된 *event_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="143b6-1174">Events are declared using *event_declaration*s:</span></span>

```antlr
event_declaration
    : attributes? event_modifier* 'event' type variable_declarators ';'
    | attributes? event_modifier* 'event' type member_name '{' event_accessor_declarations '}'
    ;

event_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'static'
    | 'virtual'
    | 'sealed'
    | 'override'
    | 'abstract'
    | 'extern'
    | event_modifier_unsafe
    ;

event_accessor_declarations
    : add_accessor_declaration remove_accessor_declaration
    | remove_accessor_declaration add_accessor_declaration
    ;

add_accessor_declaration
    : attributes? 'add' block
    ;

remove_accessor_declaration
    : attributes? 'remove' block
    ;
```

<span data-ttu-id="143b6-1175">*event_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)) 및 네 가지 액세스 한정자의 유효한 조합이 ([액세스 한정자 ](classes.md#access-modifiers)), `new` ([새 한정자](classes.md#the-new-modifier)), `static` ([정적 메서드와 인스턴스](classes.md#static-and-instance-methods)), `virtual` ([가상메서드](classes.md#virtual-methods)), `override` ([메서드를 재정의](classes.md#override-methods)), `sealed` ([메서드를 봉인](classes.md#sealed-methods)), `abstract` ([추상 메서드](classes.md#abstract-methods)), 및 `extern` ([외부 메서드](classes.md#external-methods)) 한정자.</span><span class="sxs-lookup"><span data-stu-id="143b6-1175">An *event_declaration* may include a set of *attributes* ([Attributes](attributes.md)) and a valid combination of the four access modifiers ([Access modifiers](classes.md#access-modifiers)), the `new` ([The new modifier](classes.md#the-new-modifier)),  `static` ([Static and instance methods](classes.md#static-and-instance-methods)), `virtual` ([Virtual methods](classes.md#virtual-methods)), `override` ([Override methods](classes.md#override-methods)), `sealed` ([Sealed methods](classes.md#sealed-methods)), `abstract` ([Abstract methods](classes.md#abstract-methods)), and `extern` ([External methods](classes.md#external-methods)) modifiers.</span></span>

<span data-ttu-id="143b6-1176">이벤트 선언 (method) 선언으로 동일한 규칙이 적용 됩니다 ([메서드](classes.md#methods)) 한정자의 유효한 조합을 관련 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1176">Event declarations are subject to the same rules as method declarations ([Methods](classes.md#methods)) with regard to valid combinations of modifiers.</span></span>

<span data-ttu-id="143b6-1177">*형식* 이벤트 선언 해야를 *delegate_type* ([참조 형식](types.md#reference-types)), 올바르고 *delegate_type* 이상 이어야 합니다으로 이벤트 자체 만큼 액세스 가능 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1177">The *type* of an event declaration must be a *delegate_type* ([Reference types](types.md#reference-types)), and that *delegate_type* must be at least as accessible as the event itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

<span data-ttu-id="143b6-1178">이벤트 선언이 포함 될 수 있습니다 *event_accessor_declarations*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1178">An event declaration may include *event_accessor_declarations*.</span></span> <span data-ttu-id="143b6-1179">그러나 그렇지 않은 경우, extern이 아닌 한 추상이 아닌 이벤트를 컴파일러가 자동으로 제공 ([필드와 유사한 이벤트](classes.md#field-like-events)); extern 이벤트에 대 한 접근자 외부적으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1179">However, if it does not, for non-extern, non-abstract events, the compiler supplies them automatically ([Field-like events](classes.md#field-like-events)); for extern events, the accessors are provided externally.</span></span>

<span data-ttu-id="143b6-1180">생략 하는 이벤트 선언 *event_accessor_declarations* 하나 이상의 이벤트를 정의 각각에 대 한 합니다 *variable_declarator*s입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1180">An event declaration that omits *event_accessor_declarations* defines one or more events—one for each of the *variable_declarator*s.</span></span> <span data-ttu-id="143b6-1181">이러한 선언 된 멤버의 모든 적용 된 특성 및 한정자를 *event_declaration*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1181">The attributes and modifiers apply to all of the members declared by such an *event_declaration*.</span></span>

<span data-ttu-id="143b6-1182">에 대 한 컴파일 시간 오류를 *event_declaration* 둘 다 포함 하는 `abstract` 한정자 중괄호로 구분 및 *event_accessor_declarations*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1182">It is a compile-time error for an *event_declaration* to include both the `abstract` modifier and brace-delimited *event_accessor_declarations*.</span></span>

<span data-ttu-id="143b6-1183">이벤트 선언이 포함 된 경우는 `extern` 한정자를 이벤트 라고는 ***외부 이벤트***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1183">When an event declaration includes an `extern` modifier, the event is said to be an ***external event***.</span></span> <span data-ttu-id="143b6-1184">외부 이벤트 선언은 실제 구현을 제공 되므로 둘 다 포함에 대 한 오류를 `extern` 한정자와 *event_accessor_declarations*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1184">Because an external event declaration provides no actual implementation, it is an error for it to include both the `extern` modifier and *event_accessor_declarations*.</span></span>

<span data-ttu-id="143b6-1185">에 대 한 컴파일 시간 오류를 *variable_declarator* 사용 하 여 이벤트 선언는 `abstract` 또는 `external` 한정자를 포함는 *variable_initializer*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1185">It is a compile-time error for a *variable_declarator* of an event declaration with an `abstract` or `external` modifier to include a *variable_initializer*.</span></span>

<span data-ttu-id="143b6-1186">이벤트의 왼쪽 피연산자로 사용할 수는 `+=` 하 고 `-=` 연산자 ([이벤트 할당](expressions.md#event-assignment)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1186">An event can be used as the left-hand operand of the `+=` and `-=` operators ([Event assignment](expressions.md#event-assignment)).</span></span> <span data-ttu-id="143b6-1187">이러한 연산자는 사용 각각 이벤트 처리기를 연결 하거나 이벤트에서 이벤트 처리기를 제거 하 고 이러한 연산이 허용 되는 컨텍스트를 제어 하는 이벤트의 액세스 한정자.</span><span class="sxs-lookup"><span data-stu-id="143b6-1187">These operators are used, respectively, to attach event handlers to or to remove event handlers from an event, and the access modifiers of the event control the contexts in which such operations are permitted.</span></span>

<span data-ttu-id="143b6-1188">이후 `+=` 고 `-=` 이벤트, 외부 코드를 선언 하는 형식 외부 이벤트에 허용 되는 유일한 작업 수 추가 및 이벤트 처리기를 제거 하지만 수 없습니다. 다른 방식으로 가져올 또는 이벤트의 기본 목록을 수정 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1188">Since `+=` and `-=` are the only operations that are permitted on an event outside the type that declares the event, external code can add and remove handlers for an event, but cannot in any other way obtain or modify the underlying list of event handlers.</span></span>

<span data-ttu-id="143b6-1189">폼의 작업에서 `x += y` 또는 `x -= y`면 `x` 이벤트 이며 참조의 선언을 포함 하는 형식 외부 이루어집니다 `x`, 작업의 결과 형식이 `void` (대신 유형의 `x`의 값을 사용 하 여 `x` 할당 후).</span><span class="sxs-lookup"><span data-stu-id="143b6-1189">In an operation of the form `x += y` or `x -= y`, when `x` is an event and the reference takes place outside the type that contains the declaration of `x`, the result of the operation has type `void` (as opposed to having the type of `x`, with the value of `x` after the assignment).</span></span> <span data-ttu-id="143b6-1190">이 규칙에서 이벤트의 내부 대리자를 직접 검사 외부 코드를 금지 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1190">This rule prohibits external code from indirectly examining the underlying delegate of an event.</span></span>

<span data-ttu-id="143b6-1191">다음 예제에서는 이벤트 처리기의 인스턴스에 연결 된 방법의 `Button` 클래스:</span><span class="sxs-lookup"><span data-stu-id="143b6-1191">The following example shows how event handlers are attached to instances of the `Button` class:</span></span>
```csharp
public delegate void EventHandler(object sender, EventArgs e);

public class Button: Control
{
    public event EventHandler Click;
}

public class LoginDialog: Form
{
    Button OkButton;
    Button CancelButton;

    public LoginDialog() {
        OkButton = new Button(...);
        OkButton.Click += new EventHandler(OkButtonClick);
        CancelButton = new Button(...);
        CancelButton.Click += new EventHandler(CancelButtonClick);
    }

    void OkButtonClick(object sender, EventArgs e) {
        // Handle OkButton.Click event
    }

    void CancelButtonClick(object sender, EventArgs e) {
        // Handle CancelButton.Click event
    }
}
```

<span data-ttu-id="143b6-1192">여기에 `LoginDialog` 인스턴스 생성자 두 개를 만듭니다 `Button` 인스턴스 및 이벤트 처리기를 연결 합니다 `Click` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1192">Here, the `LoginDialog` instance constructor creates two `Button` instances and attaches event handlers to the `Click` events.</span></span>

### <a name="field-like-events"></a><span data-ttu-id="143b6-1193">필드와 유사한 이벤트</span><span class="sxs-lookup"><span data-stu-id="143b6-1193">Field-like events</span></span>

<span data-ttu-id="143b6-1194">클래스 또는 이벤트 선언이 포함 된 구조체의 프로그램 텍스트를 내 필드와 같은 특정 이벤트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1194">Within the program text of the class or struct that contains the declaration of an event, certain events can be used like fields.</span></span> <span data-ttu-id="143b6-1195">이 방식으로 사용할 이벤트 수 없습니다 `abstract` 나 `extern`를 명시적으로 포함 하지 않아야 하 고 *event_accessor_declarations*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1195">To be used in this way, an event must not be `abstract` or `extern`, and must not explicitly include *event_accessor_declarations*.</span></span> <span data-ttu-id="143b6-1196">이러한 이벤트 필드를 허용 하는 모든 컨텍스트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1196">Such an event can be used in any context that permits a field.</span></span> <span data-ttu-id="143b6-1197">대리자를 포함 하는 필드 ([대리자](delegates.md))이 이벤트에 추가 된 이벤트 처리기의 목록을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1197">The field contains a delegate ([Delegates](delegates.md)) which refers to the list of event handlers that have been added to the event.</span></span> <span data-ttu-id="143b6-1198">필드를 포함 하는 이벤트 처리기에 추가한 경우 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1198">If no event handlers have been added, the field contains `null`.</span></span>

<span data-ttu-id="143b6-1199">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-1199">In the example</span></span>
```csharp
public delegate void EventHandler(object sender, EventArgs e);

public class Button: Control
{
    public event EventHandler Click;

    protected void OnClick(EventArgs e) {
        if (Click != null) Click(this, e);
    }

    public void Reset() {
        Click = null;
    }
}
```
<span data-ttu-id="143b6-1200">`Click` 내에서 필드로 사용 되는 `Button` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1200">`Click` is used as a field within the `Button` class.</span></span> <span data-ttu-id="143b6-1201">예제에 따라 필드 수 검사, 수정 하 고 대리자 호출 식에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1201">As the example demonstrates, the field can be examined, modified, and used in delegate invocation expressions.</span></span> <span data-ttu-id="143b6-1202">`OnClick` 의 메서드를 `Button` "발생" 클래스는 `Click` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1202">The `OnClick` method in the `Button` class "raises" the `Click` event.</span></span> <span data-ttu-id="143b6-1203">이벤트 발생 개념은 이벤트가 나타내는 대리자를 호출하는 것과 정확히 동일하므로 이벤트 발생을 위한 특수한 언어 구문은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1203">The notion of raising an event is precisely equivalent to invoking the delegate represented by the event—thus, there are no special language constructs for raising events.</span></span> <span data-ttu-id="143b6-1204">대리자가 null이 아닌지 확인 하 여 대리자 호출 앞에 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1204">Note that the delegate invocation is preceded by a check that ensures the delegate is non-null.</span></span>

<span data-ttu-id="143b6-1205">선언의 외부에 `Button` 클래스를 `Click` 멤버의 왼쪽 에서만 사용할 수는 `+=` 및 `-=` 에서처럼 연산자</span><span class="sxs-lookup"><span data-stu-id="143b6-1205">Outside the declaration of the `Button` class, the `Click` member can only be used on the left-hand side of the `+=` and `-=` operators, as in</span></span>
```csharp
b.Click += new EventHandler(...);
```
<span data-ttu-id="143b6-1206">대리자의 호출 목록에 추가 된 `Click` 이벤트 및</span><span class="sxs-lookup"><span data-stu-id="143b6-1206">which appends a delegate to the invocation list of the `Click` event, and</span></span>
```csharp
b.Click -= new EventHandler(...);
```
<span data-ttu-id="143b6-1207">대리자의 호출 목록에서 제거 된 `Click` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1207">which removes a delegate from the invocation list of the `Click` event.</span></span>

<span data-ttu-id="143b6-1208">필드와 유사한 이벤트를 컴파일할 때 컴파일러는 자동으로 대리자를 포함 하는 저장소가 만들고 추가 하거나 이벤트 처리기 대리자 필드를 제거 하는 이벤트에 대 한 접근자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1208">When compiling a field-like event, the compiler automatically creates storage to hold the delegate, and creates accessors for the event that add or remove event handlers to the delegate field.</span></span> <span data-ttu-id="143b6-1209">추가 및 제거 작업은 스레드로부터 안전 하 게 될 수 있습니다 (하며 필요 하지 않습니다) 동안에는 수행할된 수는 잠금을 보유 ([lock 문](statements.md#the-lock-statement)) 인스턴스 이벤트를 포함 하는 개체 또는 형식 개체 ([익명 개체 만들기 식](expressions.md#anonymous-object-creation-expressions)) 정적 이벤트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1209">The addition and removal operations are thread safe, and may (but are not required to) be done while holding the lock ([The lock statement](statements.md#the-lock-statement)) on the containing object for an instance event, or the type object ([Anonymous object creation expressions](expressions.md#anonymous-object-creation-expressions)) for a static event.</span></span>

<span data-ttu-id="143b6-1210">따라서 인스턴스 이벤트 선언 형식:</span><span class="sxs-lookup"><span data-stu-id="143b6-1210">Thus, an instance event declaration of the form:</span></span>
```csharp
class X
{
    public event D Ev;
}
```
<span data-ttu-id="143b6-1211">에 해당 하는 것으로 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1211">will be compiled to something equivalent to:</span></span>
```csharp
class X
{
    private D __Ev;  // field to hold the delegate

    public event D Ev {
        add {
            /* add the delegate in a thread safe way */
        }

        remove {
            /* remove the delegate in a thread safe way */
        }
    }
}
```
<span data-ttu-id="143b6-1212">클래스 내의 `X`에 대 한 참조 `Ev` 의 왼쪽에는 `+=` 및 `-=` 연산자를 추가 하면 및 remove 접근자를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1212">Within the class `X`, references to `Ev` on the left-hand side of the `+=` and `-=` operators cause the add and remove accessors to be invoked.</span></span> <span data-ttu-id="143b6-1213">다른 모든 참조가 `Ev` 숨겨진된 필드를 참조 하도록 컴파일된 `__Ev` 대신 ([멤버 액세스](expressions.md#member-access)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1213">All other references to `Ev` are compiled to reference the hidden field `__Ev` instead ([Member access](expressions.md#member-access)).</span></span> <span data-ttu-id="143b6-1214">이름을 "`__Ev`"은 임의의; 숨김된 필드를 가지기 모든 이름 또는 이름이 없는 전혀 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1214">The name "`__Ev`" is arbitrary; the hidden field could have any name or no name at all.</span></span>

### <a name="event-accessors"></a><span data-ttu-id="143b6-1215">이벤트 접근자</span><span class="sxs-lookup"><span data-stu-id="143b6-1215">Event accessors</span></span>

<span data-ttu-id="143b6-1216">이벤트 선언에서 일반적으로 생략 *event_accessor_declarations*에서 같이 `Button` 위의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1216">Event declarations typically omit *event_accessor_declarations*, as in the `Button` example above.</span></span> <span data-ttu-id="143b6-1217">따라서 수행 하기 위한 한 가지 상황은는 이벤트당 하나의 필드는 저장소 비용을 허용 되지 경우 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1217">One situation for doing so involves the case in which the storage cost of one field per event is not acceptable.</span></span> <span data-ttu-id="143b6-1218">이러한 경우 클래스를 포함할 수 있습니다 *event_accessor_declarations* 및 이벤트 처리기의 목록을 저장 하는 데는 개인 메커니즘을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1218">In such cases, a class can include *event_accessor_declarations* and use a private mechanism for storing the list of event handlers.</span></span>

<span data-ttu-id="143b6-1219">합니다 *event_accessor_declarations* 이벤트의 이벤트 처리기 추가 및 제거와 관련 된 실행 가능 문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1219">The *event_accessor_declarations* of an event specify the executable statements associated with adding and removing event handlers.</span></span>

<span data-ttu-id="143b6-1220">접근자 선언을 이루어진를 *add_accessor_declaration* 와 *remove_accessor_declaration*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1220">The accessor declarations consist of an *add_accessor_declaration* and a *remove_accessor_declaration*.</span></span> <span data-ttu-id="143b6-1221">각 접근자 선언의 토큰 이루어져 `add` 또는 `remove` 뒤에 *블록*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1221">Each accessor declaration consists of the token `add` or `remove` followed by a *block*.</span></span> <span data-ttu-id="143b6-1222">*블록* 연관는 *add_accessor_declaration* 이벤트 처리기에 추가 될 때 실행할 문을 지정 하며 *블록* 를연관*remove_accessor_declaration* 이벤트 처리기를 제거할 때 실행할 문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1222">The *block* associated with an *add_accessor_declaration* specifies the statements to execute when an event handler is added, and the *block* associated with a *remove_accessor_declaration* specifies the statements to execute when an event handler is removed.</span></span>

<span data-ttu-id="143b6-1223">각 *add_accessor_declaration* 및 *remove_accessor_declaration* 이벤트 형식의 단일 값 매개 변수를 사용 하 여 메서드에 해당 하 고 `void` 형식을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1223">Each *add_accessor_declaration* and *remove_accessor_declaration* corresponds to a method with a single value parameter of the event type and a `void` return type.</span></span> <span data-ttu-id="143b6-1224">이벤트 접근자의 암시적 매개 변수 이름은 `value`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1224">The implicit parameter of an event accessor is named `value`.</span></span> <span data-ttu-id="143b6-1225">이벤트 이벤트 할당에 사용할 적절 한 이벤트 접근자 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1225">When an event is used in an event assignment, the appropriate event accessor is used.</span></span> <span data-ttu-id="143b6-1226">특히 할당 연산자가 `+=` add 접근자를 사용 하 고 할당 연산자가 `-=` remove 접근자가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1226">Specifically, if the assignment operator is `+=` then the add accessor is used, and if the assignment operator is `-=` then the remove accessor is used.</span></span> <span data-ttu-id="143b6-1227">두 경우 모두 대입 연산자의 오른쪽 피연산자는 이벤트 접근자에 대 한 인수로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1227">In either case, the right-hand operand of the assignment operator is used as the argument to the event accessor.</span></span> <span data-ttu-id="143b6-1228">블록에는 *add_accessor_declaration* 또는 *remove_accessor_declaration* 규칙을 따라야 `void` 에 설명 된 방법 [메서드 본문](classes.md#method-body)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1228">The block of an *add_accessor_declaration* or a *remove_accessor_declaration* must conform to the rules for `void` methods described in [Method body](classes.md#method-body).</span></span> <span data-ttu-id="143b6-1229">특히 `return` 이러한 블록의 문은 식을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1229">In particular, `return` statements in such a block are not permitted to specify an expression.</span></span>

<span data-ttu-id="143b6-1230">이벤트 접근자에는 암시적으로 명명 된 매개 변수가 있으므로 `value`, 해당 이름을 가진에 대 한 이벤트 접근자에 선언 된 지역 변수 또는 상수에 대 한 것은 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1230">Since an event accessor implicitly has a parameter named `value`, it is a compile-time error for a local variable or constant declared in an event accessor to have that name.</span></span>

<span data-ttu-id="143b6-1231">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-1231">In the example</span></span>
```csharp
class Control: Component
{
    // Unique keys for events
    static readonly object mouseDownEventKey = new object();
    static readonly object mouseUpEventKey = new object();

    // Return event handler associated with key
    protected Delegate GetEventHandler(object key) {...}

    // Add event handler associated with key
    protected void AddEventHandler(object key, Delegate handler) {...}

    // Remove event handler associated with key
    protected void RemoveEventHandler(object key, Delegate handler) {...}

    // MouseDown event
    public event MouseEventHandler MouseDown {
        add { AddEventHandler(mouseDownEventKey, value); }
        remove { RemoveEventHandler(mouseDownEventKey, value); }
    }

    // MouseUp event
    public event MouseEventHandler MouseUp {
        add { AddEventHandler(mouseUpEventKey, value); }
        remove { RemoveEventHandler(mouseUpEventKey, value); }
    }

    // Invoke the MouseUp event
    protected void OnMouseUp(MouseEventArgs args) {
        MouseEventHandler handler; 
        handler = (MouseEventHandler)GetEventHandler(mouseUpEventKey);
        if (handler != null)
            handler(this, args);
    }
}
```
<span data-ttu-id="143b6-1232">`Control` 클래스 이벤트에 대 한 내부 저장소 메커니즘을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1232">the `Control` class implements an internal storage mechanism for events.</span></span> <span data-ttu-id="143b6-1233">`AddEventHandler` 메서드는 키를 사용 하 여 대리자 값을 연결 합니다 `GetEventHandler` 메서드는 현재 키와 연결 된 대리자를 반환 및 `RemoveEventHandler` 로 지정된 된 이벤트에 대 한 이벤트 처리기 대리자를 제거 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="143b6-1233">The `AddEventHandler` method associates a delegate value with a key, the `GetEventHandler` method returns the delegate currently associated with a key, and the `RemoveEventHandler` method removes a delegate as an event handler for the specified event.</span></span> <span data-ttu-id="143b6-1234">연결에 대 한 비용은 되도록 기본 저장소 메커니즘은 아마도 `null` 키가 들어 있는 값을 위임 하 고 따라서 처리 되지 않은 이벤트 저장소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1234">Presumably, the underlying storage mechanism is designed such that there is no cost for associating a `null` delegate value with a key, and thus unhandled events consume no storage.</span></span>

### <a name="static-and-instance-events"></a><span data-ttu-id="143b6-1235">정적 및 인스턴스 이벤트</span><span class="sxs-lookup"><span data-stu-id="143b6-1235">Static and instance events</span></span>

<span data-ttu-id="143b6-1236">이벤트 선언이 포함 된 경우는 `static` 한정자를 이벤트 라고는 ***정적 이벤트***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1236">When an event declaration includes a `static` modifier, the event is said to be a ***static event***.</span></span> <span data-ttu-id="143b6-1237">없는 경우 `static` 한정자가 있는 이벤트 라고는 ***인스턴스 이벤트***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1237">When no `static` modifier is present, the event is said to be an ***instance event***.</span></span>

<span data-ttu-id="143b6-1238">정적 이벤트를 특정 인스턴스와 연결 되며 컴파일 타임 오류를 가리키는 데 `this` 정적 이벤트의 접근자에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1238">A static event is not associated with a specific instance, and it is a compile-time error to refer to `this` in the accessors of a static event.</span></span>

<span data-ttu-id="143b6-1239">인스턴스 이벤트는 클래스의 특정된 인스턴스와 연결 된 및로이 인스턴스를 액세스할 수 있습니다 `this` ([이 액세스](expressions.md#this-access))에서 해당 이벤트의 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1239">An instance event is associated with a given instance of a class, and this instance can be accessed as `this` ([This access](expressions.md#this-access)) in the accessors of that event.</span></span>

<span data-ttu-id="143b6-1240">이벤트에서 참조 하는 경우는 *member_access* ([멤버 액세스](expressions.md#member-access)) 형식의 `E.M`이면 `M` 이벤트를 사용 하는 정적 이벤트 `E` 를포함하는형식을표시해야합니다`M`, 경우에 `M` 인스턴스 이벤트가 E를 포함 하는 형식 인스턴스의 나타내야 `M`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1240">When an event is referenced in a *member_access* ([Member access](expressions.md#member-access)) of the form `E.M`, if `M` is a static event, `E` must denote a type containing `M`, and if `M` is an instance event, E must denote an instance of a type containing `M`.</span></span>

<span data-ttu-id="143b6-1241">정적 간의 차이점 및 인스턴스 멤버 설명에 대 한 자세한 [정적 및 인스턴스 멤버](classes.md#static-and-instance-members)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1241">The differences between static and instance members are discussed further in [Static and instance members](classes.md#static-and-instance-members).</span></span>

### <a name="virtual-sealed-override-and-abstract-event-accessors"></a><span data-ttu-id="143b6-1242">Sealed, 가상, 재정 및 추상 이벤트 접근자</span><span class="sxs-lookup"><span data-stu-id="143b6-1242">Virtual, sealed, override, and abstract event accessors</span></span>

<span data-ttu-id="143b6-1243">`virtual` 이벤트 선언은 해당 이벤트의 접근자는 가상를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1243">A `virtual` event declaration specifies that the accessors of that event are virtual.</span></span> <span data-ttu-id="143b6-1244">`virtual` 한정자는 이벤트의 접근자를 모두에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1244">The `virtual` modifier applies to both accessors of an event.</span></span>

<span data-ttu-id="143b6-1245">`abstract` 이벤트 선언에 지정 된 이벤트의 접근자 가상 하지만 접근자의 실제 구현을 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1245">An `abstract` event declaration specifies that the accessors of the event are virtual, but does not provide an actual implementation of the accessors.</span></span> <span data-ttu-id="143b6-1246">대신, 비추상 파생된 클래스는 이벤트를 재정의 하 여 접근자에 대 한 자체 구현을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1246">Instead, non-abstract derived classes are required to provide their own implementation for the accessors by overriding the event.</span></span> <span data-ttu-id="143b6-1247">추상 이벤트 선언은 실제 구현을 제공 하기 때문에 중괄호로 구분 제공할 수 없습니다 *event_accessor_declarations*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1247">Because an abstract event declaration provides no actual implementation, it cannot provide brace-delimited *event_accessor_declarations*.</span></span>

<span data-ttu-id="143b6-1248">모두 포함 하는 이벤트 선언 된 `abstract` 및 `override` 한정자 이벤트 추상 이며 재정의 기본 이벤트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1248">An event declaration that includes both the `abstract` and `override` modifiers specifies that the event is abstract and overrides a base event.</span></span> <span data-ttu-id="143b6-1249">이러한 이벤트의 접근자도 추상입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1249">The accessors of such an event are also abstract.</span></span>

<span data-ttu-id="143b6-1250">추상 이벤트 선언에서 추상 클래스 에서만 허용 됩니다 ([추상 클래스](classes.md#abstract-classes)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1250">Abstract event declarations are only permitted in abstract classes ([Abstract classes](classes.md#abstract-classes)).</span></span>

<span data-ttu-id="143b6-1251">지정 하는 이벤트 선언을 포함 하 여 파생된 클래스에서 상속 된 가상 이벤트의 접근자를 재정의할 수 있습니다는 `override` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1251">The accessors of an inherited virtual event can be overridden in a derived class by including an event declaration that specifies an `override` modifier.</span></span> <span data-ttu-id="143b6-1252">이 ***이벤트 선언 재정의***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1252">This is known as an ***overriding event declaration***.</span></span> <span data-ttu-id="143b6-1253">재정의 하는 이벤트 선언 새 이벤트를 선언 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1253">An overriding event declaration does not declare a new event.</span></span> <span data-ttu-id="143b6-1254">대신, 기존 가상 이벤트의 접근자의 구현을 단순히 특수화 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1254">Instead, it simply specializes the implementations of the accessors of an existing virtual event.</span></span>

<span data-ttu-id="143b6-1255">재정의 하는 이벤트 선언 재정의 된 이벤트와 정확 하 게 동일한 액세스 가능성 한정자, 형식 및 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1255">An overriding event declaration must specify the exact same accessibility modifiers, type, and name as the overridden event.</span></span>

<span data-ttu-id="143b6-1256">재정의 이벤트 선언이 포함 될 수 있습니다는 `sealed` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1256">An overriding event declaration may include the `sealed` modifier.</span></span> <span data-ttu-id="143b6-1257">이 한정자를 사용 하는 추가 이벤트를 재정의에서 파생된 클래스를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1257">Use of this modifier prevents a derived class from further overriding the event.</span></span> <span data-ttu-id="143b6-1258">봉인 된 이벤트의 접근자도 봉인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1258">The accessors of a sealed event are also sealed.</span></span>

<span data-ttu-id="143b6-1259">포함 하도록 재정의 이벤트 선언에 대 한 컴파일 시간 오류가 발생 한 `new` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1259">It is a compile-time error for an overriding event declaration to include a `new` modifier.</span></span>

<span data-ttu-id="143b6-1260">선언 및 호출의 차이 제외 하 고 구문, 가상, sealed 재정 및 추상 접근자는 가상, sealed 재정 및 추상 메서드 똑같이 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1260">Except for differences in declaration and invocation syntax, virtual, sealed, override, and abstract accessors behave exactly like virtual, sealed, override and abstract methods.</span></span> <span data-ttu-id="143b6-1261">규칙에서 설명 하는 특히 [가상 메서드](classes.md#virtual-methods), [메서드를 재정의](classes.md#override-methods)합니다 [메서드를 봉인](classes.md#sealed-methods), 및 [추상 메서드](classes.md#abstract-methods) 적용 처럼 접근자는 해당 폼의 메서드를 했습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1261">Specifically, the rules described in [Virtual methods](classes.md#virtual-methods), [Override methods](classes.md#override-methods), [Sealed methods](classes.md#sealed-methods), and [Abstract methods](classes.md#abstract-methods) apply as if accessors were methods of a corresponding form.</span></span> <span data-ttu-id="143b6-1262">이벤트 형식의 단일 값 매개 변수를 사용 하 여 메서드에 해당 하는 각 접근자는 `void` 형식 및 포함 하는 이벤트는 같은 한정자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1262">Each accessor corresponds to a method with a single value parameter of the event type, a `void` return type, and the same modifiers as the containing event.</span></span>

## <a name="indexers"></a><span data-ttu-id="143b6-1263">인덱서</span><span class="sxs-lookup"><span data-stu-id="143b6-1263">Indexers</span></span>

<span data-ttu-id="143b6-1264">***인덱서*** 는 동일한 방식으로 배열에서 인덱싱할 수 있도록 하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1264">An ***indexer*** is a member that enables an object to be indexed in the same way as an array.</span></span> <span data-ttu-id="143b6-1265">인덱서를 사용 하 여 선언 된 *indexer_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="143b6-1265">Indexers are declared using *indexer_declaration*s:</span></span>

```antlr
indexer_declaration
    : attributes? indexer_modifier* indexer_declarator indexer_body
    ;

indexer_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'virtual'
    | 'sealed'
    | 'override'
    | 'abstract'
    | 'extern'
    | indexer_modifier_unsafe
    ;

indexer_declarator
    : type 'this' '[' formal_parameter_list ']'
    | type interface_type '.' 'this' '[' formal_parameter_list ']'
    ;

indexer_body
    : '{' accessor_declarations '}' 
    | '=>' expression ';'
    ;
```

<span data-ttu-id="143b6-1266">*indexer_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)) 및 네 가지 액세스 한정자의 유효한 조합이 ([액세스 한정자 ](classes.md#access-modifiers)), `new` ([새 한정자](classes.md#the-new-modifier)), `virtual` ([가상 메서드](classes.md#virtual-methods)), `override` ([메서드를 재정의](classes.md#override-methods) )를 `sealed` ([메서드를 봉인](classes.md#sealed-methods)), `abstract` ([추상 메서드](classes.md#abstract-methods)), 및 `extern` ([외부 메서드](classes.md#external-methods)) 한정자.</span><span class="sxs-lookup"><span data-stu-id="143b6-1266">An *indexer_declaration* may include a set of *attributes* ([Attributes](attributes.md)) and a valid combination of the four access modifiers ([Access modifiers](classes.md#access-modifiers)), the `new` ([The new modifier](classes.md#the-new-modifier)), `virtual` ([Virtual methods](classes.md#virtual-methods)), `override` ([Override methods](classes.md#override-methods)), `sealed` ([Sealed methods](classes.md#sealed-methods)), `abstract` ([Abstract methods](classes.md#abstract-methods)), and `extern` ([External methods](classes.md#external-methods)) modifiers.</span></span>

<span data-ttu-id="143b6-1267">Indexer 선언을 메서드 선언으로 동일한 규칙이 적용 됩니다 ([메서드](classes.md#methods)) 한정자의 유효한 조합을 관련 하 여 static 한정자를 되는 한 가지 예외를 사용 하 여에서 허용 되지 않습니다는 인덱서 선언이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1267">Indexer declarations are subject to the same rules as method declarations ([Methods](classes.md#methods)) with regard to valid combinations of modifiers, with the one exception being that the static modifier is not permitted on an indexer declaration.</span></span>

<span data-ttu-id="143b6-1268">Modifiers `virtual`, `override`, 및 `abstract` 한 경우 제외 하 고 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1268">The modifiers `virtual`, `override`, and `abstract` are mutually exclusive except in one case.</span></span> <span data-ttu-id="143b6-1269">합니다 `abstract` 고 `override` 추상 인덱서는 가상 인터페이스가 재정의할 수 있도록 한정자 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1269">The `abstract` and `override` modifiers may be used together so that an abstract indexer can override a virtual one.</span></span>

<span data-ttu-id="143b6-1270">합니다 *형식* 인덱서의 선언은 선언에 의해 정의 된 인덱서의 요소 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1270">The *type* of an indexer declaration specifies the element type of the indexer introduced by the declaration.</span></span> <span data-ttu-id="143b6-1271">인덱서는 명시적 인터페이스 멤버 구현이 아닌 합니다 *형식* 키워드 뒤 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1271">Unless the indexer is an explicit interface member implementation, the *type* is followed by the keyword `this`.</span></span> <span data-ttu-id="143b6-1272">명시적 인터페이스 멤버 구현에 대 한 합니다 *형식* 뒤에 *interface_type*, "`.`", 및 키워드 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1272">For an explicit interface member implementation, the *type* is followed by an *interface_type*, a "`.`", and the keyword `this`.</span></span> <span data-ttu-id="143b6-1273">다른 멤버와 달리 인덱서는 사용자 정의 이름을 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1273">Unlike other members, indexers do not have user-defined names.</span></span>

<span data-ttu-id="143b6-1274">합니다 *formal_parameter_list* 인덱서에 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1274">The *formal_parameter_list* specifies the parameters of the indexer.</span></span> <span data-ttu-id="143b6-1275">메서드는 해당 하는 인덱서의 정식 매개 변수 목록 ([메서드 매개 변수](classes.md#method-parameters)) 매개 변수가 하나 이상 지정 해야 한다는 점을 제외 하면, 및를 `ref` 고 `out` 매개 변수 한정자는 허용 되지 않습니다 .</span><span class="sxs-lookup"><span data-stu-id="143b6-1275">The formal parameter list of an indexer corresponds to that of a method ([Method parameters](classes.md#method-parameters)), except that at least one parameter must be specified, and that the `ref` and `out` parameter modifiers are not permitted.</span></span>

<span data-ttu-id="143b6-1276">*형식* 인덱서 및 각 형식에서 참조 되는 *formal_parameter_list* 적어도 인덱서 자체 만큼 액세스 가능 해야 합니다 ([접근성 제약 조건](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1276">The *type* of an indexer and each of the types referenced in the *formal_parameter_list* must be at least as accessible as the indexer itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

<span data-ttu-id="143b6-1277">*indexer_body* 하나 구성 될 수 있습니다는 ***접근자 본문*** 요소나 ***식 본문***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1277">An *indexer_body* may either consist of an ***accessor body*** or an ***expression body***.</span></span> <span data-ttu-id="143b6-1278">접근자 본문을 *accessor_declarations*는 묶어야 "`{`"및"`}`" 접근자를 선언 하는 토큰 ([접근자](classes.md#accessors)) 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1278">In an accessor body, *accessor_declarations*, which must be enclosed in "`{`" and "`}`" tokens, declare the accessors ([Accessors](classes.md#accessors)) of the property.</span></span> <span data-ttu-id="143b6-1279">접근자에는 읽기 및 쓰기 속성을 사용 하 여 연결 된 실행 가능 문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1279">The accessors specify the executable statements associated with reading and writing the property.</span></span>

<span data-ttu-id="143b6-1280">구성 된 식 본문이 "`=>`" 뒤에 식이 `E` 세미콜론은 문 본문을 동일 하 고 `{ get { return E; } }`, 따라서 사용할 수 있습니다만 getter 전용 인덱서를 지정 하는 결과인 getter 인 및 단일 식으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1280">An expression body consisting of "`=>`" followed by an expression `E` and a semicolon is exactly equivalent to the statement body `{ get { return E; } }`, and can therefore only be used to specify getter-only indexers where the result of the getter is given by a single expression.</span></span>

<span data-ttu-id="143b6-1281">인덱서 요소에 액세스 하기 위한 구문은 동일 배열 요소에 대 한, 경우에 인덱서 요소 분류 되지 않은 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1281">Even though the syntax for accessing an indexer element is the same as that for an array element, an indexer element is not classified as a variable.</span></span> <span data-ttu-id="143b6-1282">따라서 불가능으로 인덱서 요소를 전달 하는 `ref` 또는 `out` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1282">Thus, it is not possible to pass an indexer element as a `ref` or `out` argument.</span></span>

<span data-ttu-id="143b6-1283">시그니처를 정의 하는 인덱서의 정식 매개 변수 목록 ([시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading)) 인덱서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1283">The formal parameter list of an indexer defines the signature ([Signatures and overloading](basic-concepts.md#signatures-and-overloading)) of the indexer.</span></span> <span data-ttu-id="143b6-1284">특히, 인덱서의 시그니처는 정식 매개 변수의 형식과 수 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1284">Specifically, the signature of an indexer consists of the number and types of its formal parameters.</span></span> <span data-ttu-id="143b6-1285">요소 형식 및 형식 매개 변수의 이름이 인덱서의 시그니처의 일부로 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1285">The element type and names of the formal parameters are not part of an indexer's signature.</span></span>

<span data-ttu-id="143b6-1286">인덱서의 시그니처는 동일한 클래스에서 선언 된 다른 모든 인덱서의 시그니처와 달라 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1286">The signature of an indexer must differ from the signatures of all other indexers declared in the same class.</span></span>

<span data-ttu-id="143b6-1287">인덱서 및 속성은 개념적으로 매우 유사 하지만 다음과 같이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1287">Indexers and properties are very similar in concept, but differ in the following ways:</span></span>

*  <span data-ttu-id="143b6-1288">속성 인덱서 시그니처에으로 식별 되는 반면 해당 이름으로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1288">A property is identified by its name, whereas an indexer is identified by its signature.</span></span>
*  <span data-ttu-id="143b6-1289">속성을 통해 액세스를 *simple_name* ([단순 이름](expressions.md#simple-names)) 또는 *member_access* ([멤버 액세스](expressions.md#member-access)) 인 반면, 인덱서 요소를 통해 액세스를 *element_access* ([인덱서 액세스](expressions.md#indexer-access)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1289">A property is accessed through a *simple_name* ([Simple names](expressions.md#simple-names)) or a *member_access* ([Member access](expressions.md#member-access)), whereas an indexer element is accessed through an *element_access* ([Indexer access](expressions.md#indexer-access)).</span></span>
*  <span data-ttu-id="143b6-1290">속성 수는 `static` 멤버 인덱서는 항상 인스턴스 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1290">A property can be a `static` member, whereas an indexer is always an instance member.</span></span>
*  <span data-ttu-id="143b6-1291">A `get` 속성의 접근자 메서드에 해당 하는 매개 변수가 없는 반면를 `get` 인덱서의 접근자 메서드에 해당 하는 인덱서와 동일한 형식 매개 변수 목록 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1291">A `get` accessor of a property corresponds to a method with no parameters, whereas a `get` accessor of an indexer corresponds to a method with the same formal parameter list as the indexer.</span></span>
*  <span data-ttu-id="143b6-1292">A `set` 라는 단일 매개 변수를 사용 하 여 메서드에 해당 하는 속성의 접근자 `value`반면를 `set` 인덱서의 접근자 메서드에 해당 하는 추가 매개 변수, 인덱서가와 동일한 형식 매개 변수 목록 사용 하 여 명명 된 `value`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1292">A `set` accessor of a property corresponds to a method with a single parameter named `value`, whereas a `set` accessor of an indexer corresponds to a method with the same formal parameter list as the indexer, plus an additional parameter named `value`.</span></span>
*  <span data-ttu-id="143b6-1293">해당 인덱서 매개 변수로 동일한 이름 가진 지역 변수 선언에 대 한 인덱서 접근자에 대 한 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1293">It is a compile-time error for an indexer accessor to declare a local variable with the same name as an indexer parameter.</span></span>
*  <span data-ttu-id="143b6-1294">구문을 사용 하 여 상속 된 속성에 액세스 하는 재정의 속성 선언에 `base.P`여기서 `P` 속성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1294">In an overriding property declaration, the inherited property is accessed using the syntax `base.P`, where `P` is the property name.</span></span> <span data-ttu-id="143b6-1295">재정의 인덱서 선언에서 상속 된 인덱서 액세스 구문을 사용 하 여 `base[E]`여기서 `E` 은 식의 쉼표로 구분 된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1295">In an overriding indexer declaration, the inherited indexer is accessed using the syntax `base[E]`, where `E` is a comma separated list of expressions.</span></span>
*  <span data-ttu-id="143b6-1296">"자동으로 구현 된 인덱서" 개념이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1296">There is no concept of an "automatically implemented indexer".</span></span> <span data-ttu-id="143b6-1297">것 세미콜론 접근자를 사용 하 여 추상이 아닌, 비 외부 인덱서를 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1297">It is an error to have a non-abstract, non-external indexer with semicolon accessors.</span></span>

<span data-ttu-id="143b6-1298">이러한 차이 외에 정의 된 모든 규칙 [접근자](classes.md#accessors) 하 고 [자동으로 구현 된 속성](classes.md#automatically-implemented-properties) 속성 접근자에 대 한 인덱서 접근자를도에 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1298">Aside from these differences, all rules defined in [Accessors](classes.md#accessors) and [Automatically implemented properties](classes.md#automatically-implemented-properties) apply to indexer accessors as well as to property accessors.</span></span>

<span data-ttu-id="143b6-1299">Indexer 선언을 포함 하는 경우는 `extern` 한정자를 인덱서 라고는 ***외부 인덱서***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1299">When an indexer declaration includes an `extern` modifier, the indexer is said to be an ***external indexer***.</span></span> <span data-ttu-id="143b6-1300">외부 indexer 선언을 각각의 실제 구현을 제공 하기 때문에 해당 *accessor_declarations* 세미콜론으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1300">Because an external indexer declaration provides no actual implementation, each of its *accessor_declarations* consists of a semicolon.</span></span>

<span data-ttu-id="143b6-1301">아래 예제에서는 선언 된 `BitArray` 의 비트 배열의 개별 비트에 액세스 하기 위한 인덱서를 구현 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1301">The example below declares a `BitArray` class that implements an indexer for accessing the individual bits in the bit array.</span></span>
```csharp
using System;

class BitArray
{
    int[] bits;
    int length;

    public BitArray(int length) {
        if (length < 0) throw new ArgumentException();
        bits = new int[((length - 1) >> 5) + 1];
        this.length = length;
    }

    public int Length {
        get { return length; }
    }

    public bool this[int index] {
        get {
            if (index < 0 || index >= length) {
                throw new IndexOutOfRangeException();
            }
            return (bits[index >> 5] & 1 << index) != 0;
        }
        set {
            if (index < 0 || index >= length) {
                throw new IndexOutOfRangeException();
            }
            if (value) {
                bits[index >> 5] |= 1 << index;
            }
            else {
                bits[index >> 5] &= ~(1 << index);
            }
        }
    }
}
```

<span data-ttu-id="143b6-1302">인스턴스를 `BitArray` 해당 보다 상당히 적은 메모리를 사용 하는 클래스 `bool[]` (앞의 각 값 대신 하나의 비트만 차지 하므로 후자의 1 바이트), 같은 작업을 허용 하지만 `bool[]`입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1302">An instance of the `BitArray` class consumes substantially less memory than a corresponding `bool[]` (since each value of the former occupies only one bit instead of the latter's one byte), but it permits the same operations as a `bool[]`.</span></span>

<span data-ttu-id="143b6-1303">다음 `CountPrimes` 클래스가 사용 하는 `BitArray` 알고리즘과 고전 "체" prime 1 사이의 지정된 된 최대 수를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1303">The following `CountPrimes` class uses a `BitArray` and the classical "sieve" algorithm to compute the number of primes between 1 and a given maximum:</span></span>
```csharp
class CountPrimes
{
    static int Count(int max) {
        BitArray flags = new BitArray(max + 1);
        int count = 1;
        for (int i = 2; i <= max; i++) {
            if (!flags[i]) {
                for (int j = i * 2; j <= max; j += i) flags[j] = true;
                count++;
            }
        }
        return count;
    }

    static void Main(string[] args) {
        int max = int.Parse(args[0]);
        int count = Count(max);
        Console.WriteLine("Found {0} primes between 1 and {1}", count, max);
    }
}
```

<span data-ttu-id="143b6-1304">요소에 액세스 하는 구문은 `BitArray` 과 동일 하 게 정확 하 게 되는 `bool[]`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1304">Note that the syntax for accessing elements of the `BitArray` is precisely the same as for a `bool[]`.</span></span>

<span data-ttu-id="143b6-1305">다음 예제에서는 두 개의 매개 변수를 사용 하 여 인덱서를 26 \* 10 표 클래스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1305">The following example shows a 26 \* 10 grid class that has an indexer with two parameters.</span></span> <span data-ttu-id="143b6-1306">대문자 또는 소문자 A-z, 범위에서 첫 번째 매개 변수가 필요 하 고 두 번째 정수 0-9 범위 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1306">The first parameter is required to be an upper- or lowercase letter in the range A-Z, and the second is required to be an integer in the range 0-9.</span></span>

```csharp
using System;

class Grid
{
    const int NumRows = 26;
    const int NumCols = 10;

    int[,] cells = new int[NumRows, NumCols];

    public int this[char c, int col] {
        get {
            c = Char.ToUpper(c);
            if (c < 'A' || c > 'Z') {
                throw new ArgumentException();
            }
            if (col < 0 || col >= NumCols) {
                throw new IndexOutOfRangeException();
            }
            return cells[c - 'A', col];
        }

        set {
            c = Char.ToUpper(c);
            if (c < 'A' || c > 'Z') {
                throw new ArgumentException();
            }
            if (col < 0 || col >= NumCols) {
                throw new IndexOutOfRangeException();
            }
            cells[c - 'A', col] = value;
        }
    }
}
```

### <a name="indexer-overloading"></a><span data-ttu-id="143b6-1307">인덱서 오버 로드</span><span class="sxs-lookup"><span data-stu-id="143b6-1307">Indexer overloading</span></span>

<span data-ttu-id="143b6-1308">인덱서 오버 로드 확인 규칙에 설명 되어 있습니다 [형식 유추](expressions.md#type-inference)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1308">The indexer overload resolution rules are described in [Type inference](expressions.md#type-inference).</span></span>

## <a name="operators"></a><span data-ttu-id="143b6-1309">연산자</span><span class="sxs-lookup"><span data-stu-id="143b6-1309">Operators</span></span>

<span data-ttu-id="143b6-1310">***연산자*** 는 클래스의 인스턴스를 적용할 수 있는 식 연산자의 의미를 정의 하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1310">An ***operator*** is a member that defines the meaning of an expression operator that can be applied to instances of the class.</span></span> <span data-ttu-id="143b6-1311">연산자를 사용 하 여 선언 된 *operator_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="143b6-1311">Operators are declared using *operator_declaration*s:</span></span>

```antlr
operator_declaration
    : attributes? operator_modifier+ operator_declarator operator_body
    ;

operator_modifier
    : 'public'
    | 'static'
    | 'extern'
    | operator_modifier_unsafe
    ;

operator_declarator
    : unary_operator_declarator
    | binary_operator_declarator
    | conversion_operator_declarator
    ;

unary_operator_declarator
    : type 'operator' overloadable_unary_operator '(' type identifier ')'
    ;

overloadable_unary_operator
    : '+' | '-' | '!' | '~' | '++' | '--' | 'true' | 'false'
    ;

binary_operator_declarator
    : type 'operator' overloadable_binary_operator '(' type identifier ',' type identifier ')'
    ;

overloadable_binary_operator
    : '+'   | '-'   | '*'   | '/'   | '%'   | '&'   | '|'   | '^'   | '<<'
    | 'right_shift' | '=='  | '!='  | '>'   | '<'   | '>='  | '<='
    ;

conversion_operator_declarator
    : 'implicit' 'operator' type '(' type identifier ')'
    | 'explicit' 'operator' type '(' type identifier ')'
    ;

operator_body
    : block
    | '=>' expression ';'
    | ';'
    ;
```

<span data-ttu-id="143b6-1312">연산자를 오버 로드할 수 있는 세 종류: 단항 연산자 ([단항 연산자](classes.md#unary-operators)), 이항 연산자 ([이항 연산자](classes.md#binary-operators)), 및 변환 연산자 ([변환 연산자 ](classes.md#conversion-operators)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1312">There are three categories of overloadable operators: Unary operators ([Unary operators](classes.md#unary-operators)), binary operators ([Binary operators](classes.md#binary-operators)), and conversion operators ([Conversion operators](classes.md#conversion-operators)).</span></span>

<span data-ttu-id="143b6-1313">*operator_body* 중 하나는 세미콜론을 ***문 본문*** 요소나 ***식 본문***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1313">The *operator_body* is either a semicolon, a ***statement body*** or an ***expression body***.</span></span> <span data-ttu-id="143b6-1314">문 본문으로 구성 됩니다는 *블록*, 연산자 호출 될 때 실행할 문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1314">A statement body consists of a *block*, which specifies the statements to execute when the operator is invoked.</span></span> <span data-ttu-id="143b6-1315">합니다 *블록* 값을 반환 하는 것에 대 한 규칙을 따라야에 설명 된 방법을 [메서드 본문](classes.md#method-body)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1315">The *block* must conform to the rules for value-returning methods described in [Method body](classes.md#method-body).</span></span> <span data-ttu-id="143b6-1316">식 본문이 이루어져 `=>` 식과 세미콜론, 뒤 및 연산자가 호출 되 면 하는 데 단일 식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1316">An expression body consists of `=>` followed by an expression and a semicolon, and denotes a single expression to perform when the operator is invoked.</span></span>

<span data-ttu-id="143b6-1317">에 대 한 `extern` 연산자는 *operator_body* 세미콜론으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1317">For `extern` operators, the *operator_body* consists simply of a semicolon.</span></span> <span data-ttu-id="143b6-1318">다른 모든 연산자에 대 한 합니다 *operator_body* 되었거나 블록 본문을 식 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1318">For all other operators, the *operator_body* is either a block body or an expression body.</span></span>

<span data-ttu-id="143b6-1319">모든 연산자 선언에는 다음 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1319">The following rules apply to all operator declarations:</span></span>

*  <span data-ttu-id="143b6-1320">연산자 선언 모두 포함 해야 합니다는 `public` 및 `static` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1320">An operator declaration must include both a `public` and a `static` modifier.</span></span>
*  <span data-ttu-id="143b6-1321">연산자의 매개 변수 값 매개 변수 여야 합니다. ([매개 변수 값](variables.md#value-parameters)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1321">The parameter(s) of an operator must be value parameters ([Value parameters](variables.md#value-parameters)).</span></span> <span data-ttu-id="143b6-1322">지정 하는 연산자 선언에 대 한 컴파일 타임 오류 `ref` 또는 `out` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1322">It is a compile-time error for an operator declaration to specify `ref` or `out` parameters.</span></span>
*  <span data-ttu-id="143b6-1323">연산자의 시그니처에 ([단항 연산자](classes.md#unary-operators)를 [이항 연산자](classes.md#binary-operators), [변환 연산자](classes.md#conversion-operators))에 선언 된 다른 모든 연산자의 시그니처와에서 달라 야 합니다 동일한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1323">The signature of an operator ([Unary operators](classes.md#unary-operators), [Binary operators](classes.md#binary-operators), [Conversion operators](classes.md#conversion-operators)) must differ from the signatures of all other operators declared in the same class.</span></span>
*  <span data-ttu-id="143b6-1324">연산자 선언에서 참조 하는 모든 형식은 적어도 연산자 자체 수준 만큼 액세스 가능 이어야 합니다 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1324">All types referenced in an operator declaration must be at least as accessible as the operator itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>
*  <span data-ttu-id="143b6-1325">연산자 선언에 여러 번 표시 하는 동일한 한정자에 대 한 오류는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1325">It is an error for the same modifier to appear multiple times in an operator declaration.</span></span>

<span data-ttu-id="143b6-1326">각 연산자 범주는 다음 섹션에 설명 된 대로 추가 제한을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1326">Each operator category imposes additional restrictions, as described in the following sections.</span></span>

<span data-ttu-id="143b6-1327">다른 멤버와 마찬가지로 기본 클래스에서 선언 된 연산자는 파생된 클래스에서 상속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1327">Like other members, operators declared in a base class are inherited by derived classes.</span></span> <span data-ttu-id="143b6-1328">연산자 선언에는 반드시 클래스 또는 구조체 연산자는 연산자의 시그니처에 참여 하도록 선언 되는, 때문에 기본 클래스에 선언 된 운영자를 숨기려면 파생된 클래스에서 선언 하는 연산자에 대 한는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1328">Because operator declarations always require the class or struct in which the operator is declared to participate in the signature of the operator, it is not possible for an operator declared in a derived class to hide an operator declared in a base class.</span></span> <span data-ttu-id="143b6-1329">따라서는 `new` 한정자 필요 하지 이며 따라서 되지 허용 연산자 선언에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1329">Thus, the `new` modifier is never required, and therefore never permitted, in an operator declaration.</span></span>

<span data-ttu-id="143b6-1330">단항 및 이항 연산자에 대 한 추가 정보에서 찾을 수 있습니다 [연산자](expressions.md#operators)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1330">Additional information on unary and binary operators can be found in [Operators](expressions.md#operators).</span></span>

<span data-ttu-id="143b6-1331">변환 연산자에 대 한 추가 정보를 찾을 수 있습니다 [사용자 정의 변환은](conversions.md#user-defined-conversions)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1331">Additional information on conversion operators can be found in [User-defined conversions](conversions.md#user-defined-conversions).</span></span>

### <a name="unary-operators"></a><span data-ttu-id="143b6-1332">단항 연산자</span><span class="sxs-lookup"><span data-stu-id="143b6-1332">Unary operators</span></span>

<span data-ttu-id="143b6-1333">단항 연산자 선언에는 다음 규칙이 적용 됩니다. 여기서 `T` 클래스 또는 연산자 선언이 포함 된 구조체의 인스턴스 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1333">The following rules apply to unary operator declarations, where `T` denotes the instance type of the class or struct that contains the operator declaration:</span></span>

*  <span data-ttu-id="143b6-1334">단항 `+`, `-`를 `!`, 또는 `~` 연산자 형식의 단일 매개 변수를 사용 해야 `T` 또는 `T?` 모든 형식을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1334">A unary `+`, `-`, `!`, or `~` operator must take a single parameter of type `T` or `T?` and can return any type.</span></span>
*  <span data-ttu-id="143b6-1335">단항 `++` 나 `--` 연산자 형식의 단일 매개 변수를 사용 해야 `T` 또는 `T?` 하며 동일한 형식 또는 형식에서 파생 된 반환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1335">A unary `++` or `--` operator must take a single parameter of type `T` or `T?` and must return that same type or a type derived from it.</span></span>
*  <span data-ttu-id="143b6-1336">단항 `true` 또는 `false` 연산자 형식의 단일 매개 변수를 사용 해야 `T` 또는 `T?` 형식을 반환 해야 합니다 및 `bool`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1336">A unary `true` or `false` operator must take a single parameter of type `T` or `T?` and must return type `bool`.</span></span>

<span data-ttu-id="143b6-1337">단항 연산자의 서명은 연산자 토큰의 (`+`, `-`, `!`, `~`, `++`를 `--`, `true`, 또는 `false`) 및 단일 정식 매개 변수 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1337">The signature of a unary operator consists of the operator token (`+`, `-`, `!`, `~`, `++`, `--`, `true`, or `false`) and the type of the single formal parameter.</span></span> <span data-ttu-id="143b6-1338">반환 형식은 단항 연산자의 서명의 일부가 아닌 하거나 형식 매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1338">The return type is not part of a unary operator's signature, nor is the name of the formal parameter.</span></span>

<span data-ttu-id="143b6-1339">합니다 `true` 고 `false` 단항 연산자는 쌍 단위 선언 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1339">The `true` and `false` unary operators require pair-wise declaration.</span></span> <span data-ttu-id="143b6-1340">클래스 선언도 다른 선언 하지 않고 이러한 연산자 중 하나는 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1340">A compile-time error occurs if a class declares one of these operators without also declaring the other.</span></span> <span data-ttu-id="143b6-1341">`true` 하 고 `false` 연산자에 자세히 설명 되어 [사용자 정의 조건부 논리 연산자](expressions.md#user-defined-conditional-logical-operators) 하 고 [부울 식](expressions.md#boolean-expressions).</span><span class="sxs-lookup"><span data-stu-id="143b6-1341">The `true` and `false` operators are described further in [User-defined conditional logical operators](expressions.md#user-defined-conditional-logical-operators) and [Boolean expressions](expressions.md#boolean-expressions).</span></span>

<span data-ttu-id="143b6-1342">다음 예제에서는 구현 및의 후속 사용 `operator ++` 정수 벡터 클래스:</span><span class="sxs-lookup"><span data-stu-id="143b6-1342">The following example shows an implementation and subsequent usage of `operator ++` for an integer vector class:</span></span>
```csharp
public class IntVector
{
    public IntVector(int length) {...}

    public int Length {...}                 // read-only property

    public int this[int index] {...}        // read-write indexer

    public static IntVector operator ++(IntVector iv) {
        IntVector temp = new IntVector(iv.Length);
        for (int i = 0; i < iv.Length; i++)
            temp[i] = iv[i] + 1;
        return temp;
    }
}

class Test
{
    static void Main() {
        IntVector iv1 = new IntVector(4);    // vector of 4 x 0
        IntVector iv2;

        iv2 = iv1++;    // iv2 contains 4 x 0, iv1 contains 4 x 1
        iv2 = ++iv1;    // iv2 contains 4 x 2, iv1 contains 4 x 2
    }
}
```

<span data-ttu-id="143b6-1343">연산자 메서드 후 위 증가 마찬가지로 피연산자를 1을 추가 하 여 생성 한 값을 반환 하는 방법 및 감소 연산자 ([후 위 증가 및 감소 연산자](expressions.md#postfix-increment-and-decrement-operators)), 접두사 증가 및 감소 연산자 ([전위 증가 및 감소 연산자](expressions.md#prefix-increment-and-decrement-operators)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1343">Note how the operator method returns the value produced by adding 1 to the operand, just like the  postfix increment and decrement operators ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators)), and the prefix increment and decrement operators ([Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)).</span></span> <span data-ttu-id="143b6-1344">와 달리 c + +에서는이 메서드가 필요 직접 수정 하지는 피연산자의 값.</span><span class="sxs-lookup"><span data-stu-id="143b6-1344">Unlike in C++, this method need not modify the value of its operand directly.</span></span> <span data-ttu-id="143b6-1345">사실, 피연산자 값을 수정 후 위 증가 연산자의 표준 의미 체계를 위반 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1345">In fact, modifying the operand value would violate the standard semantics of the postfix increment operator.</span></span>

### <a name="binary-operators"></a><span data-ttu-id="143b6-1346">이항 연산자</span><span class="sxs-lookup"><span data-stu-id="143b6-1346">Binary operators</span></span>

<span data-ttu-id="143b6-1347">이항 연산자 선언에는 다음 규칙이 적용 됩니다. 여기서 `T` 클래스 또는 연산자 선언이 포함 된 구조체의 인스턴스 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1347">The following rules apply to binary operator declarations, where `T` denotes the instance type of the class or struct that contains the operator declaration:</span></span>

*  <span data-ttu-id="143b6-1348">이진 앤 시프트 연산자는 하나 이상의 형식이 있어야 하는 두 개의 매개 변수를 사용 해야 합니다 `T` 또는 `T?`, 모든 형식을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1348">A binary non-shift operator must take two parameters, at least one of which must have type `T` or `T?`, and can return any type.</span></span>
*  <span data-ttu-id="143b6-1349">이진 `<<` 또는 `>>` 연산자는 첫 번째 형식이 있어야 합니다. 두 매개 변수를 사용 해야 `T` 또는 `T?` 의 두 번째 형식이 있어야 하 고 `int` 또는 `int?`, 모든 형식을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1349">A binary `<<` or `>>` operator must take two parameters, the first of which must have type `T` or `T?` and the second of which must have type `int` or `int?`, and can return any type.</span></span>

<span data-ttu-id="143b6-1350">이항 연산자의 서명은 연산자 토큰의 (`+`, `-`, `*`, `/`, `%`를 `&`, `|`를 `^`를 `<<`, `>>`, `==`, `!=`를 `>`, `<`를 `>=`, 또는 `<=`) 및 두 개의 형식 매개 변수의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1350">The signature of a binary operator consists of the operator token (`+`, `-`, `*`, `/`, `%`, `&`, `|`, `^`, `<<`, `>>`, `==`, `!=`, `>`, `<`, `>=`, or `<=`) and the types of the two formal parameters.</span></span> <span data-ttu-id="143b6-1351">반환 형식 및 형식 매개 변수의 이름을 이항 연산자의 시그니처의 일부로 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1351">The return type and the names of the formal parameters are not part of a binary operator's signature.</span></span>

<span data-ttu-id="143b6-1352">특정 이진 연산자에는 쌍 단위 선언이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1352">Certain binary operators require pair-wise declaration.</span></span> <span data-ttu-id="143b6-1353">쌍의 두 연산자의 모든 선언에 대 한 쌍의 다른 연산자의 일치 하는 선언 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1353">For every declaration of either operator of a pair, there must be a matching declaration of the other operator of the pair.</span></span> <span data-ttu-id="143b6-1354">두 연산자 선언에는 각 매개 변수에 대해 동일한 형식과 반환 형식이 있을 경우 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1354">Two operator declarations match when they have the same return type and the same type for each parameter.</span></span> <span data-ttu-id="143b6-1355">다음과 같은 연산자에는 쌍 단위 선언이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1355">The following operators require pair-wise declaration:</span></span>

*  <span data-ttu-id="143b6-1356">`operator ==` 및 `operator !=`</span><span class="sxs-lookup"><span data-stu-id="143b6-1356">`operator ==` and `operator !=`</span></span>
*  <span data-ttu-id="143b6-1357">`operator >` 및 `operator <`</span><span class="sxs-lookup"><span data-stu-id="143b6-1357">`operator >` and `operator <`</span></span>
*  <span data-ttu-id="143b6-1358">`operator >=` 및 `operator <=`</span><span class="sxs-lookup"><span data-stu-id="143b6-1358">`operator >=` and `operator <=`</span></span>

### <a name="conversion-operators"></a><span data-ttu-id="143b6-1359">변환 연산자</span><span class="sxs-lookup"><span data-stu-id="143b6-1359">Conversion operators</span></span>

<span data-ttu-id="143b6-1360">변환 연산자 선언은 소개를 ***사용자 정의 변환이*** ([사용자 정의 변환은](conversions.md#user-defined-conversions)) 미리 정의 된 암시적 및 명시적 변환을 확대 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1360">A conversion operator declaration introduces a ***user-defined conversion*** ([User-defined conversions](conversions.md#user-defined-conversions)) which augments the pre-defined implicit and explicit conversions.</span></span>

<span data-ttu-id="143b6-1361">포함 하는 변환 연산자 선언은 `implicit` 키워드는 사용자 정의 된 암시적 변환을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1361">A conversion operator declaration that includes the `implicit` keyword introduces a user-defined implicit conversion.</span></span> <span data-ttu-id="143b6-1362">다양 한 상황, 멤버 호출 함수, 캐스트 식 및 할당을 포함 하 여 암시적으로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1362">Implicit conversions can occur in a variety of situations, including function member invocations, cast expressions, and assignments.</span></span> <span data-ttu-id="143b6-1363">이에서 더 자세히 설명 [암시적 변환을](conversions.md#implicit-conversions)입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1363">This is described further in [Implicit conversions](conversions.md#implicit-conversions).</span></span>

<span data-ttu-id="143b6-1364">포함 하는 변환 연산자 선언은 `explicit` 키워드는 사용자 정의 명시적 변환을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1364">A conversion operator declaration that includes the `explicit` keyword introduces a user-defined explicit conversion.</span></span> <span data-ttu-id="143b6-1365">명시적 변환은 cast 식에서 발생할 수 있으며에 자세히 설명 되어 [명시적 변환](conversions.md#explicit-conversions)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1365">Explicit conversions can occur in cast expressions, and are described further in [Explicit conversions](conversions.md#explicit-conversions).</span></span>

<span data-ttu-id="143b6-1366">변환 연산자 변환 연산자의 반환 형식으로 표시 된 대상 형식으로 변환 연산자의 매개 변수 형식으로 표시 된 원본 형식에서 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1366">A conversion operator converts from a source type, indicated by the parameter type of the conversion operator, to a target type, indicated by the return type of the conversion operator.</span></span>

<span data-ttu-id="143b6-1367">지정 된 소스 형식에 대 한 `S` 대상 유형 및 `T`이면 `S` 또는 `T` nullable 형식 수 있도록 `S0` 및 `T0` 그렇지 않으면 해당 기본 형식 참조 `S0` 및 `T0` 됩니다 같음 `S` 고 `T` 각각.</span><span class="sxs-lookup"><span data-stu-id="143b6-1367">For a given source type `S` and target type `T`, if `S` or `T` are nullable types, let `S0` and `T0` refer to their underlying types, otherwise `S0` and `T0` are equal to `S` and `T` respectively.</span></span> <span data-ttu-id="143b6-1368">클래스 또는 구조체를 선언할 수 원본 형식에서 변환 `S` 대상 형식으로 `T` 다음 모두 만족 하는 경우에:</span><span class="sxs-lookup"><span data-stu-id="143b6-1368">A class or struct is permitted to declare a conversion from a source type `S` to a target type `T` only if all of the following are true:</span></span>

*  <span data-ttu-id="143b6-1369">`S0` 및 `T0` 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1369">`S0` and `T0` are different types.</span></span>
*  <span data-ttu-id="143b6-1370">중 하나 `S0` 또는 `T0` 는 연산자 선언이 발생 하는 클래스 또는 구조체 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1370">Either `S0` or `T0` is the class or struct type in which the operator declaration takes place.</span></span>
*  <span data-ttu-id="143b6-1371">모두 `S0` 나 `T0` 되는 *interface_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1371">Neither `S0` nor `T0` is an *interface_type*.</span></span>
*  <span data-ttu-id="143b6-1372">사용자 정의 변환을 제외 하 고 변환에서 존재 하지 않습니다 `S` 하 `T` 주고 `T` 에 `S`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1372">Excluding user-defined conversions, a conversion does not exist from `S` to `T` or from `T` to `S`.</span></span>

<span data-ttu-id="143b6-1373">이러한 규칙에서는 모든 입력 매개 변수 연관 `S` 또는 `T` 상속 관계가 없는 다른 형식 사용 및 매개 변수는 무시 됩니다. 해당 형식에 모든 제약 조건이 있는 고유 형식으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1373">For the purposes of these rules, any type parameters associated with `S` or `T` are considered to be unique types that have no inheritance relationship with other types, and any constraints on those type parameters are ignored.</span></span>

<span data-ttu-id="143b6-1374">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-1374">In the example</span></span>
```csharp
class C<T> {...}

class D<T>: C<T>
{
    public static implicit operator C<int>(D<T> value) {...}      // Ok
    public static implicit operator C<string>(D<T> value) {...}   // Ok
    public static implicit operator C<T>(D<T> value) {...}        // Error
}
```
<span data-ttu-id="143b6-1375">첫 번째 두 연산자 선언 되기 때문에 허용 됩니다의 목적 [인덱서](classes.md#indexers).3 `T` 하 고 `int` 및 `string` 각각에 없는 관계를 사용 하 여 고유 형식으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1375">the first two operator declarations are permitted because, for the purposes of [Indexers](classes.md#indexers).3, `T` and `int` and `string` respectively are considered unique types with no relationship.</span></span> <span data-ttu-id="143b6-1376">그러나 세 번째 연산자 이므로 오류로 `C<T>` 의 기본 클래스인 `D<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1376">However, the third operator is an error because `C<T>` is the base class of `D<T>`.</span></span>

<span data-ttu-id="143b6-1377">두 번째 규칙에서 변환 연산자 또는 연산자가 선언 된 클래스 또는 구조체 형식에서 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1377">From the second rule it follows that a conversion operator must convert either to or from the class or struct type in which the operator is declared.</span></span> <span data-ttu-id="143b6-1378">예를 들어 있기 클래스 또는 구조체 형식에 대 한 `C` 에서 변환을 정의 하 고 `C` 를 `int` 들어오고 `int` 에 `C`, 아닌 `int` 를 `bool`.</span><span class="sxs-lookup"><span data-stu-id="143b6-1378">For example, it is possible for a class or struct type `C` to define a conversion from `C` to `int` and from `int` to `C`, but not from `int` to `bool`.</span></span>

<span data-ttu-id="143b6-1379">직접 미리 정의 된 변환이 다시 정의 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1379">It is not possible to directly redefine a pre-defined conversion.</span></span> <span data-ttu-id="143b6-1380">따라서 변환 연산자는에서 변환할 수 없습니다 `object` 암시적 변환과 명시적 변환 간에 이미 존재 하므로 `object` 및 기타 모든 형식.</span><span class="sxs-lookup"><span data-stu-id="143b6-1380">Thus, conversion operators are not allowed to convert from or to `object` because implicit and explicit conversions already exist between `object` and all other types.</span></span> <span data-ttu-id="143b6-1381">마찬가지로, 원본이 나 변환의 대상 형식 수 있습니다 다른 기본 형식 이므로 변환이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1381">Likewise, neither the source nor the target types of a conversion can be a base type of the other, since a conversion would then already exist.</span></span>

<span data-ttu-id="143b6-1382">그러나 연산자를 지정 하는, 특정 형식 인수에 대해 변환이 이미 존재 하는 미리 정의 된 변환으로 제네릭 형식으로 선언 하는 것이 같습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1382">However, it is possible to declare operators on generic types that, for particular type arguments, specify conversions that already exist as pre-defined conversions.</span></span> <span data-ttu-id="143b6-1383">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-1383">In the example</span></span>
```csharp
struct Convertible<T>
{
    public static implicit operator Convertible<T>(T value) {...}
    public static explicit operator T(Convertible<T> value) {...}
}
```
<span data-ttu-id="143b6-1384">입력할 때 `object` 에 대 한 형식 인수로 지정 된 `T`, 두 번째 연산자는 이미 존재 하는 변환을 선언 (암시적, 및도 명시적, 형식 모두에서 변환이 존재 `object`).</span><span class="sxs-lookup"><span data-stu-id="143b6-1384">when type `object` is specified as a type argument for `T`, the second operator declares a conversion that already exists (an implicit, and therefore also an explicit, conversion exists from any type to type `object`).</span></span>

<span data-ttu-id="143b6-1385">두 형식 간에 미리 정의 된 변환이 있는 경우에는 해당 형식 간의 모든 사용자 정의 변환은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1385">In cases where a pre-defined conversion exists between two types, any user-defined conversions between those types are ignored.</span></span> <span data-ttu-id="143b6-1386">구체적으로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1386">Specifically:</span></span>

*  <span data-ttu-id="143b6-1387">미리 정의 된 암시적 변환 경우 ([암시적 변환을](conversions.md#implicit-conversions)) 형식에서 존재 `S` 형식으로 `T`, 모든 사용자 정의 변환 (암시적 또는 명시적)에서 `S` 에 `T` 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1387">If a pre-defined implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) exists from type `S` to type `T`, all user-defined conversions (implicit or explicit) from `S` to `T` are ignored.</span></span>
*  <span data-ttu-id="143b6-1388">미리 정의 된 명시적 변환 경우 ([명시적 변환](conversions.md#explicit-conversions)) 형식에서 존재 `S` 형식으로 `T`, 모든 사용자 정의 명시적 변환에서 `S` 에 `T` 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1388">If a pre-defined explicit conversion ([Explicit conversions](conversions.md#explicit-conversions)) exists from type `S` to type `T`, any user-defined explicit conversions from `S` to `T` are ignored.</span></span> <span data-ttu-id="143b6-1389">또한:</span><span class="sxs-lookup"><span data-stu-id="143b6-1389">Furthermore:</span></span>

<span data-ttu-id="143b6-1390">하는 경우 `T` 로 암시적으로 사용자 정의 인터페이스 형식 이므로 `S` 에 `T` 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1390">If `T` is an interface type, user-defined implicit conversions from `S` to `T` are ignored.</span></span>

<span data-ttu-id="143b6-1391">로 암시적으로, 사용자 정의 그렇지 `S` 에 `T` 여전히 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1391">Otherwise, user-defined implicit conversions from `S` to `T` are still considered.</span></span>

<span data-ttu-id="143b6-1392">모든 형식에 대 한 하지만 `object`, 연산자를 선언 하 여는 `Convertible<T>` 미리 정의 된 변환이 있는 형식 위의 충돌 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1392">For all types but `object`, the operators declared by the `Convertible<T>` type above do not conflict with pre-defined conversions.</span></span> <span data-ttu-id="143b6-1393">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="143b6-1393">For example:</span></span>
```csharp
void F(int i, Convertible<int> n) {
    i = n;                          // Error
    i = (int)n;                     // User-defined explicit conversion
    n = i;                          // User-defined implicit conversion
    n = (Convertible<int>)i;        // User-defined implicit conversion
}
```

<span data-ttu-id="143b6-1394">그러나 형식에 대 한 `object`, 미리 정의 된 변환의 모든 경우 사용할 수 있지만 사용자 정의 변환을 숨기기:</span><span class="sxs-lookup"><span data-stu-id="143b6-1394">However, for type `object`, pre-defined conversions hide the user-defined conversions in all cases but one:</span></span>

```csharp
void F(object o, Convertible<object> n) {
    o = n;                         // Pre-defined boxing conversion
    o = (object)n;                 // Pre-defined boxing conversion
    n = o;                         // User-defined implicit conversion
    n = (Convertible<object>)o;    // Pre-defined unboxing conversion
}
```

<span data-ttu-id="143b6-1395">변환할 사용자 정의 변환은 허용 되지 않습니다 *interface_type*s입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1395">User-defined conversions are not allowed to convert from or to *interface_type*s.</span></span> <span data-ttu-id="143b6-1396">특히,이 제한 하면 사용자 정의 변환 하지 않고도 변환할 때 발생 하는 *interface_type*, 및 변환할은 *interface_type* 경우에 성공 개체 지정 된 구현 실제로 변환할 *interface_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1396">In particular, this restriction ensures that no user-defined transformations occur when converting to an *interface_type*, and that a conversion to an *interface_type* succeeds only if the object being converted actually implements the specified *interface_type*.</span></span>

<span data-ttu-id="143b6-1397">변환 연산자의 서명이 소스 형식과 대상 유형으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1397">The signature of a conversion operator consists of the source type and the target type.</span></span> <span data-ttu-id="143b6-1398">(이 유일한 형태의 멤버는 반환 형식 서명에서 참여 note 합니다.) 합니다 `implicit` 또는 `explicit` 변환 연산자의 분류 운영자의 서명의 일부가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1398">(Note that this is the only form of member for which the return type participates in the signature.) The `implicit` or `explicit` classification of a conversion operator is not part of the operator's signature.</span></span> <span data-ttu-id="143b6-1399">즉, 클래스 또는 구조체를 선언할 수 없습니다. 둘 다를 `implicit` 및 `explicit` 동일한 원본 및 대상 형식 사용 하 여 변환 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1399">Thus, a class or struct cannot declare both an `implicit` and an `explicit` conversion operator with the same source and target types.</span></span>

<span data-ttu-id="143b6-1400">일반적으로 암시적 변환은 사용자 정의 예외를 throw 하지 않는 및 정보가 손실 되지 않도록 설계 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1400">In general, user-defined implicit conversions should be designed to never throw exceptions and never lose information.</span></span> <span data-ttu-id="143b6-1401">사용자 정의 변환이 발생할 수 있습니다 예외 (예를 들어 있으므로 원본 인수가 범위를 벗어났습니다.) 또는 손실 정보 (예: 상위 비트가 삭제)을 해당 변환으로 변환 하는 명시적 변환을 정의 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1401">If a user-defined conversion can give rise to exceptions (for example, because the source argument is out of range) or loss of information (such as discarding high-order bits), then that conversion should be defined as an explicit conversion.</span></span>

<span data-ttu-id="143b6-1402">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-1402">In the example</span></span>
```csharp
using System;

public struct Digit
{
    byte value;

    public Digit(byte value) {
        if (value < 0 || value > 9) throw new ArgumentException();
        this.value = value;
    }

    public static implicit operator byte(Digit d) {
        return d.value;
    }

    public static explicit operator Digit(byte b) {
        return new Digit(b);
    }
}
```
<span data-ttu-id="143b6-1403">변환 `Digit` 를 `byte` 되지 예외를 throw 하거나 내용은 있지만 손실 때문에 암시적 `byte` 하 `Digit` 은 이후 명시적 `Digit` 가능한 하위 집합을 나타낼 수 있습니다 값을 `byte`입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1403">the conversion from `Digit` to `byte` is implicit because it never throws exceptions or loses information, but the conversion from `byte` to `Digit` is explicit since `Digit` can only represent a subset of the possible values of a `byte`.</span></span>

## <a name="instance-constructors"></a><span data-ttu-id="143b6-1404">인스턴스 생성자</span><span class="sxs-lookup"><span data-stu-id="143b6-1404">Instance constructors</span></span>

<span data-ttu-id="143b6-1405">***인스턴스 생성자***는 클래스의 인스턴스를 초기화하는 데 필요한 작업을 구현하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1405">An ***instance constructor*** is a member that implements the actions required to initialize an instance of a class.</span></span> <span data-ttu-id="143b6-1406">인스턴스 생성자를 사용 하 여 선언 된 *constructor_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="143b6-1406">Instance constructors are declared using *constructor_declaration*s:</span></span>

```antlr
constructor_declaration
    : attributes? constructor_modifier* constructor_declarator constructor_body
    ;

constructor_modifier
    : 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'extern'
    | constructor_modifier_unsafe
    ;

constructor_declarator
    : identifier '(' formal_parameter_list? ')' constructor_initializer?
    ;

constructor_initializer
    : ':' 'base' '(' argument_list? ')'
    | ':' 'this' '(' argument_list? ')'
    ;

constructor_body
    : block
    | ';'
    ;
```

<span data-ttu-id="143b6-1407">A *constructor_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)), 네 가지 액세스 한정자의 유효한 조합이 ([액세스 한정자 ](classes.md#access-modifiers)), 및 `extern` ([외부 메서드](classes.md#external-methods)) 한정자.</span><span class="sxs-lookup"><span data-stu-id="143b6-1407">A *constructor_declaration* may include a set of *attributes* ([Attributes](attributes.md)), a valid combination of the four access modifiers ([Access modifiers](classes.md#access-modifiers)), and an `extern` ([External methods](classes.md#external-methods)) modifier.</span></span> <span data-ttu-id="143b6-1408">생성자 선언 여러 번 같은 한정자를 포함 하도록 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1408">A constructor declaration is not permitted to include the same modifier multiple times.</span></span>

<span data-ttu-id="143b6-1409">합니다 *식별자* 의 한 *constructor_declarator* 인스턴스 생성자 선언 되는 클래스 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1409">The *identifier* of a *constructor_declarator* must name the class in which the instance constructor is declared.</span></span> <span data-ttu-id="143b6-1410">다른 이름을 지정 하는 경우 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1410">If any other name is specified, a compile-time error occurs.</span></span>

<span data-ttu-id="143b6-1411">선택적 *formal_parameter_list* 인스턴스의 생성자가 동일한 규칙을 적용 합니다 *formal_parameter_list* 메서드 ([메서드](classes.md#methods)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1411">The optional *formal_parameter_list* of an instance constructor is subject to the same rules as the *formal_parameter_list* of a method ([Methods](classes.md#methods)).</span></span> <span data-ttu-id="143b6-1412">시그니처를 정의 하는 정식 매개 변수 목록 ([시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading)) 인스턴스 생성자의 프로세스를 여기서 제어 및 오버 로드 확인 ([형식 유추](expressions.md#type-inference)) 특정 선택 인스턴스 생성자를 호출에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1412">The formal parameter list defines the signature ([Signatures and overloading](basic-concepts.md#signatures-and-overloading)) of an instance constructor and governs the process whereby overload resolution ([Type inference](expressions.md#type-inference)) selects a particular instance constructor in an invocation.</span></span>

<span data-ttu-id="143b6-1413">참조 되는 형식의 각 합니다 *formal_parameter_list* 인스턴스의 생성자 적어도 생성자 자체 수준 만큼 액세스 가능 해야 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1413">Each of the types referenced in the *formal_parameter_list* of an instance constructor must be at least as accessible as the constructor itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

<span data-ttu-id="143b6-1414">선택적 *constructor_initializer* 호출에 지정 된 문을 실행 하기 전에 다른 인스턴스 생성자를 지정 합니다 *constructor_body* 이 인스턴스 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1414">The optional *constructor_initializer* specifies another instance constructor to invoke before executing the statements given in the *constructor_body* of this instance constructor.</span></span> <span data-ttu-id="143b6-1415">이에서 더 자세히 설명 [생성자 이니셜라이저](classes.md#constructor-initializers)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1415">This is described further in [Constructor initializers](classes.md#constructor-initializers).</span></span>

<span data-ttu-id="143b6-1416">생성자 선언에 포함 되어는 `extern` 한정자를 생성자 라고는 ***외부 생성자***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1416">When a constructor declaration includes an `extern` modifier, the constructor is said to be an ***external constructor***.</span></span> <span data-ttu-id="143b6-1417">외부 생성자 선언에는 실제 구현을 제공 하기 때문에 해당 *constructor_body* 세미콜론으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1417">Because an external constructor declaration provides no actual implementation, its *constructor_body* consists of a semicolon.</span></span> <span data-ttu-id="143b6-1418">다른 모든 생성자는 *constructor_body* 이루어져를 *블록* 클래스의 새 인스턴스를 초기화 하는 문을 지정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1418">For all other constructors, the *constructor_body* consists of a *block* which specifies the statements to initialize a new instance of the class.</span></span> <span data-ttu-id="143b6-1419">이 예제는 다음과 같습니다 합니다 *블록* 사용 하 여 인스턴스 메서드는 `void` 반환 형식 ([메서드 본문](classes.md#method-body)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1419">This corresponds exactly to the *block* of an instance method with a `void` return type ([Method body](classes.md#method-body)).</span></span>

<span data-ttu-id="143b6-1420">인스턴스 생성자 상속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1420">Instance constructors are not inherited.</span></span> <span data-ttu-id="143b6-1421">따라서 클래스 인스턴스 생성자가 없는 클래스에서 실제로 선언 이외의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1421">Thus, a class has no instance constructors other than those actually declared in the class.</span></span> <span data-ttu-id="143b6-1422">기본 생성자가 자동으로 제공 클래스에 인스턴스 생성자 선언이 없는 경우 ([기본 생성자](classes.md#default-constructors)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1422">If a class contains no instance constructor declarations, a default instance constructor is automatically provided ([Default constructors](classes.md#default-constructors)).</span></span>

<span data-ttu-id="143b6-1423">인스턴스 생성자는 호출한 *object_creation_expression*s ([개체 만들기 식](expressions.md#object-creation-expressions)) 및 *constructor_initializer*s입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1423">Instance constructors are invoked by *object_creation_expression*s ([Object creation expressions](expressions.md#object-creation-expressions)) and through *constructor_initializer*s.</span></span>

### <a name="constructor-initializers"></a><span data-ttu-id="143b6-1424">생성자 이니셜라이저</span><span class="sxs-lookup"><span data-stu-id="143b6-1424">Constructor initializers</span></span>

<span data-ttu-id="143b6-1425">모든 인스턴스 생성자 (클래스에 대 한 파일을 제외한 `object`) 암시적으로 바로 앞의 다른 인스턴스 생성자 호출을 포함 합니다 *constructor_body*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1425">All instance constructors (except those for class `object`) implicitly include an invocation of another instance constructor immediately before the *constructor_body*.</span></span> <span data-ttu-id="143b6-1426">암시적으로 호출할 생성자에 의해 결정 됩니다 합니다 *constructor_initializer*:</span><span class="sxs-lookup"><span data-stu-id="143b6-1426">The constructor to implicitly invoke is determined by the *constructor_initializer*:</span></span>

*  <span data-ttu-id="143b6-1427">형식의 인스턴스 생성자 이니셜라이저 `base(argument_list)` 또는 `base()` 에서 호출할 직접 기본 클래스는 인스턴스 생성자를 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1427">An instance constructor initializer of the form `base(argument_list)` or `base()` causes an instance constructor from the direct base class to be invoked.</span></span> <span data-ttu-id="143b6-1428">해당 생성자를 사용 하 여 선택 *argument_list* 하는 경우 표시 되 고의 오버 로드 확인 규칙 [오버 로드 확인](expressions.md#overload-resolution)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1428">That constructor is selected using *argument_list* if present and the overload resolution rules of [Overload resolution](expressions.md#overload-resolution).</span></span> <span data-ttu-id="143b6-1429">기본 생성자를 직접 기본 클래스에 포함 된 모든 액세스 가능한 인스턴스 생성자의 후보 인스턴스 생성자를 집합으로 구성 됩니다 ([기본 생성자](classes.md#default-constructors)) 없는 인스턴스 생성자에 선언 된 경우는 직접 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1429">The set of candidate instance constructors consists of all accessible instance constructors contained in the direct base class, or the default constructor ([Default constructors](classes.md#default-constructors)), if no instance constructors are declared in the direct base class.</span></span> <span data-ttu-id="143b6-1430">이 집합이 비어 있는 경우 또는 단일 최상의 인스턴스 생성자를 식별할 수 없는 경우 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1430">If this set is empty, or if a single best instance constructor cannot be identified, a compile-time error occurs.</span></span>
*  <span data-ttu-id="143b6-1431">형식의 인스턴스 생성자 이니셜라이저 `this(argument-list)` 또는 `this()` 호출할 자체 클래스에서 인스턴스 생성자를 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1431">An instance constructor initializer of the form `this(argument-list)` or `this()` causes an instance constructor from the class itself to be invoked.</span></span> <span data-ttu-id="143b6-1432">생성자를 사용 하 여 선택 *argument_list* 하는 경우 표시 되 고의 오버 로드 확인 규칙 [오버 로드 확인](expressions.md#overload-resolution)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1432">The constructor is selected using *argument_list* if present and the overload resolution rules of [Overload resolution](expressions.md#overload-resolution).</span></span> <span data-ttu-id="143b6-1433">자체 클래스에서 선언 하는 모든 가능한 인스턴스 생성자의 후보 인스턴스 생성자의 집합이 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1433">The set of candidate instance constructors consists of all accessible instance constructors declared in the class itself.</span></span> <span data-ttu-id="143b6-1434">이 집합이 비어 있는 경우 또는 단일 최상의 인스턴스 생성자를 식별할 수 없는 경우 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1434">If this set is empty, or if a single best instance constructor cannot be identified, a compile-time error occurs.</span></span> <span data-ttu-id="143b6-1435">인스턴스 생성자 선언 자체 생성자를 호출 하는 생성자 이니셜라이저를 포함 하는 경우 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1435">If an instance constructor declaration includes a constructor initializer that invokes the constructor itself, a compile-time error occurs.</span></span>

<span data-ttu-id="143b6-1436">인스턴스 생성자에 폼의 생성자 이니셜라이저가 생성자 이니셜라이저가 없기 경우 `base()` 암시적으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1436">If an instance constructor has no constructor initializer, a constructor initializer of the form `base()` is implicitly provided.</span></span> <span data-ttu-id="143b6-1437">따라서 형식의 인스턴스 생성자 선언</span><span class="sxs-lookup"><span data-stu-id="143b6-1437">Thus, an instance constructor declaration of the form</span></span>
```csharp
C(...) {...}
```
<span data-ttu-id="143b6-1438">동일</span><span class="sxs-lookup"><span data-stu-id="143b6-1438">is exactly equivalent to</span></span>
```csharp
C(...): base() {...}
```

<span data-ttu-id="143b6-1439">제공한 매개 변수의 범위는 *formal_parameter_list* 선언 인스턴스 생성자의 해당 선언의 생성자 이니셜라이저를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1439">The scope of the parameters given by the *formal_parameter_list* of an instance constructor declaration includes the constructor initializer of that declaration.</span></span> <span data-ttu-id="143b6-1440">따라서 생성자 이니셜라이저는 생성자의 매개 변수에 액세스 하도록 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1440">Thus, a constructor initializer is permitted to access the parameters of the constructor.</span></span> <span data-ttu-id="143b6-1441">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="143b6-1441">For example:</span></span>
```csharp
class A
{
    public A(int x, int y) {}
}

class B: A
{
    public B(int x, int y): base(x + y, x - y) {}
}
```

<span data-ttu-id="143b6-1442">인스턴스 생성자 이니셜라이저는 생성 되는 인스턴스를 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1442">An instance constructor initializer cannot access the instance being created.</span></span> <span data-ttu-id="143b6-1443">따라서 컴파일 타임 오류를 참조 하는 것 `this` 생성자 이니셜라이저 인수 식에서으로 것을 통해 인스턴스 멤버를 참조 하는 인수 식에 대 한 컴파일 시간 오류를 *simple_name*.</span><span class="sxs-lookup"><span data-stu-id="143b6-1443">Therefore it is a compile-time error to reference `this` in an argument expression of the constructor initializer, as is it a compile-time error for an argument expression to reference any instance member through a *simple_name*.</span></span>

### <a name="instance-variable-initializers"></a><span data-ttu-id="143b6-1444">인스턴스 변수 이니셜라이저</span><span class="sxs-lookup"><span data-stu-id="143b6-1444">Instance variable initializers</span></span>

<span data-ttu-id="143b6-1445">경우는 인스턴스 생성자가 없는 생성자 이니셜라이저 또는 폼의 생성자 이니셜라이저가 `base(...)`, 해당 생성자에서 지정 된 초기화를 암시적으로 수행 합니다 *variable_initializer*의 인스턴스 필드는 해당 클래스에 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1445">When an instance constructor has no constructor initializer, or it has a constructor initializer of the form `base(...)`, that constructor implicitly performs the initializations specified by the *variable_initializer*s of the instance fields declared in its class.</span></span> <span data-ttu-id="143b6-1446">이 항목의 생성자를 직접 기본 클래스 생성자가 암시적으로 호출 하기 전에 바로 실행 되는 할당의 시퀀스에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1446">This corresponds to a sequence of assignments that are executed immediately upon entry to the constructor and before the implicit invocation of the direct base class constructor.</span></span> <span data-ttu-id="143b6-1447">변수 이니셜라이저는 클래스 선언에 나타나는 텍스트 순서 대로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1447">The variable initializers are executed in the textual order in which they appear in the class declaration.</span></span>

### <a name="constructor-execution"></a><span data-ttu-id="143b6-1448">생성자 실행</span><span class="sxs-lookup"><span data-stu-id="143b6-1448">Constructor execution</span></span>

<span data-ttu-id="143b6-1449">변수 이니셜라이저는 대입문, 변환 및 이러한 대입문 기본 클래스 인스턴스 생성자가 호출 되기 전에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1449">Variable initializers are transformed into assignment statements, and these assignment statements are executed before the invocation of the base class instance constructor.</span></span> <span data-ttu-id="143b6-1450">이렇게 순서를 지정 하면 해당 인스턴스에 액세스할 수 있는 모든 문이 실행 되기 전에 모든 인스턴스 필드가 해당 변수 이니셜라이저에 의해 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1450">This ordering ensures that all instance fields are initialized by their variable initializers before any statements that have access to that instance are executed.</span></span>

<span data-ttu-id="143b6-1451">예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1451">Given the example</span></span>
```csharp
using System;

class A
{
    public A() {
        PrintFields();
    }

    public virtual void PrintFields() {}
}

class B: A
{
    int x = 1;
    int y;

    public B() {
        y = -1;
    }

    public override void PrintFields() {
        Console.WriteLine("x = {0}, y = {1}", x, y);
    }
}
```
<span data-ttu-id="143b6-1452">때 `new B()` 의 인스턴스를 만드는 데 사용 됩니다 `B`에 다음 출력이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1452">when `new B()` is used to create an instance of `B`, the following output is produced:</span></span>
```
x = 1, y = 0
```

<span data-ttu-id="143b6-1453">변수의 `x` 1 이므로 변수 이니셜라이저에서 예외는 기본 클래스 인스턴스 생성자가 호출 되기 전에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1453">The value of `x` is 1 because the variable initializer is executed before the base class instance constructor is invoked.</span></span> <span data-ttu-id="143b6-1454">그러나 값 `y` 은 0 (기본값은 `int`) 때문에 할당 하는 `y` 기본 클래스 생성자는 반환 될 때까지 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1454">However, the value of `y` is 0 (the default value of an `int`) because the assignment to `y` is not executed until after the base class constructor returns.</span></span>

<span data-ttu-id="143b6-1455">인스턴스 변수 이니셜라이저 및 생성자 이니셜라이저 하기 전에 자동으로 삽입 되는 명령문으로 생각 하는 것이 유용 합니다 *constructor_body*합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1455">It is useful to think of instance variable initializers and constructor initializers as statements that are automatically inserted before the *constructor_body*.</span></span> <span data-ttu-id="143b6-1456">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-1456">The example</span></span>
```csharp
using System;
using System.Collections;

class A
{
    int x = 1, y = -1, count;

    public A() {
        count = 0;
    }

    public A(int n) {
        count = n;
    }
}

class B: A
{
    double sqrt2 = Math.Sqrt(2.0);
    ArrayList items = new ArrayList(100);
    int max;

    public B(): this(100) {
        items.Add("default");
    }

    public B(int n): base(n - 1) {
        max = n;
    }
}
```
<span data-ttu-id="143b6-1457">여러 변수 이니셜라이저를 포함합니다. 두 형태 모두의 생성자 이니셜라이저 포함 (`base` 고 `this`).</span><span class="sxs-lookup"><span data-stu-id="143b6-1457">contains several variable initializers; it also contains constructor initializers of both forms (`base` and `this`).</span></span> <span data-ttu-id="143b6-1458">예제 코드에 해당 하는 아래에 나와 있는 경우 각 주석 (자동으로 삽입 된 생성자 호출에 사용 되는 구문은 유효 하지 않으면 하지만 으로만 작동 하는 메커니즘을 설명 하기 위해)를 자동으로 삽입 된 문을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1458">The example corresponds to the code shown below, where each comment indicates an automatically inserted statement (the syntax used for the automatically inserted constructor invocations isn't valid, but merely serves to illustrate the mechanism).</span></span>

```csharp
using System.Collections;

class A
{
    int x, y, count;

    public A() {
        x = 1;                       // Variable initializer
        y = -1;                      // Variable initializer
        object();                    // Invoke object() constructor
        count = 0;
    }

    public A(int n) {
        x = 1;                       // Variable initializer
        y = -1;                      // Variable initializer
        object();                    // Invoke object() constructor
        count = n;
    }
}

class B: A
{
    double sqrt2;
    ArrayList items;
    int max;

    public B(): this(100) {
        B(100);                      // Invoke B(int) constructor
        items.Add("default");
    }

    public B(int n): base(n - 1) {
        sqrt2 = Math.Sqrt(2.0);      // Variable initializer
        items = new ArrayList(100);  // Variable initializer
        A(n - 1);                    // Invoke A(int) constructor
        max = n;
    }
}
```

### <a name="default-constructors"></a><span data-ttu-id="143b6-1459">기본 생성자</span><span class="sxs-lookup"><span data-stu-id="143b6-1459">Default constructors</span></span>

<span data-ttu-id="143b6-1460">클래스에 인스턴스 생성자 선언이 없는 경우 기본 인스턴스 생성자를 자동으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1460">If a class contains no instance constructor declarations, a default instance constructor is automatically provided.</span></span> <span data-ttu-id="143b6-1461">해당 기본 생성자는 단순히 직접 기본 클래스의 매개 변수가 없는 생성자를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1461">That default constructor simply invokes the parameterless constructor of the direct base class.</span></span> <span data-ttu-id="143b6-1462">클래스는 추상 선언 된 접근성이 기본 생성자에 대 한 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1462">If the class is abstract then the declared accessibility for the default constructor is protected.</span></span> <span data-ttu-id="143b6-1463">그렇지 않으면 선언 된 접근성이 기본 생성자는 공용입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1463">Otherwise, the declared accessibility for the default constructor is public.</span></span> <span data-ttu-id="143b6-1464">따라서 기본 생성자는 항상</span><span class="sxs-lookup"><span data-stu-id="143b6-1464">Thus, the default constructor is always of the form</span></span>

```csharp
protected C(): base() {}
```
<span data-ttu-id="143b6-1465">또는</span><span class="sxs-lookup"><span data-stu-id="143b6-1465">or</span></span>
```csharp
public C(): base() {}
```
<span data-ttu-id="143b6-1466">여기서 `C` 클래스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1466">where `C` is the name of the class.</span></span> <span data-ttu-id="143b6-1467">오버 로드 확인에 기본 클래스 생성자 이니셜라이저에 대 한 고유 최상의 후보를 확인할 수 없는 경우 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1467">If overload resolution is unable to determine a unique best candidate for the base class constructor initializer then a compile-time error occurs.</span></span>

<span data-ttu-id="143b6-1468">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-1468">In the example</span></span>
```csharp
class Message
{
    object sender;
    string text;
}
```
<span data-ttu-id="143b6-1469">기본 생성자를 클래스에 인스턴스 생성자 선언이 없으면 때문에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1469">a default constructor is provided because the class contains no instance constructor declarations.</span></span> <span data-ttu-id="143b6-1470">따라서이 예제는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1470">Thus, the example is precisely equivalent to</span></span>
```csharp
class Message
{
    object sender;
    string text;

    public Message(): base() {}
}
```

### <a name="private-constructors"></a><span data-ttu-id="143b6-1471">Private 생성자</span><span class="sxs-lookup"><span data-stu-id="143b6-1471">Private constructors</span></span>

<span data-ttu-id="143b6-1472">때 클래스 `T` 만 개인 인스턴스 생성자를 선언, 외부의 프로그램 텍스트 클래스에 대 한 불가능 `T` 에서 파생 시키는 `T` 의 인스턴스를 직접 만들려면 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1472">When a class `T` declares only private instance constructors, it is not possible for classes outside the program text of `T` to derive from `T` or to directly create instances of `T`.</span></span> <span data-ttu-id="143b6-1473">따라서 클래스 정적 멤버만 포함 하 고 인스턴스화할 수 없습니다, 하는 경우 개인 빈 인스턴스 생성자를 추가 인스턴스화가 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1473">Thus, if a class contains only static members and isn't intended to be instantiated, adding an empty private instance constructor will prevent instantiation.</span></span> <span data-ttu-id="143b6-1474">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="143b6-1474">For example:</span></span>
```csharp
public class Trig
{
    private Trig() {}        // Prevent instantiation

    public const double PI = 3.14159265358979323846;

    public static double Sin(double x) {...}
    public static double Cos(double x) {...}
    public static double Tan(double x) {...}
}
```

<span data-ttu-id="143b6-1475">`Trig` 클래스 관련 메서드와 상수가, 그룹을 수행 하지만 인스턴스화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1475">The `Trig` class groups related methods and constants, but is not intended to be instantiated.</span></span> <span data-ttu-id="143b6-1476">따라서 단일 빈 개인 인스턴스 생성자를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1476">Therefore it declares a single empty private instance constructor.</span></span> <span data-ttu-id="143b6-1477">기본 생성자를 자동으로 생성 하지 않으려면 하나 이상의 인스턴스 생성자를 선언 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1477">At least one instance constructor must be declared to suppress the automatic generation of a default constructor.</span></span>

### <a name="optional-instance-constructor-parameters"></a><span data-ttu-id="143b6-1478">선택적 인스턴스 생성자 매개 변수</span><span class="sxs-lookup"><span data-stu-id="143b6-1478">Optional instance constructor parameters</span></span>

<span data-ttu-id="143b6-1479">`this(...)` 형식의 생성자 이니셜라이저는 대개 오버 로드와 함께에서 선택적 인스턴스 생성자 매개 변수를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1479">The `this(...)` form of constructor initializer is commonly used in conjunction with overloading to implement optional instance constructor parameters.</span></span> <span data-ttu-id="143b6-1480">예제</span><span class="sxs-lookup"><span data-stu-id="143b6-1480">In the example</span></span>
```csharp
class Text
{
    public Text(): this(0, 0, null) {}

    public Text(int x, int y): this(x, y, null) {}

    public Text(int x, int y, string s) {
        // Actual constructor implementation
    }
}
```
<span data-ttu-id="143b6-1481">첫 번째 두 개의 인스턴스 생성자는 단순히 누락 된 인수에 대 한 기본 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1481">the first two instance constructors merely provide the default values for the missing arguments.</span></span> <span data-ttu-id="143b6-1482">둘 다 사용을 `this(...)` 실제로 새 인스턴스를 초기화 하는 작업을 수행 하는 세 번째 인스턴스 생성자를 호출 하는 생성자 이니셜라이저입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1482">Both use a `this(...)` constructor initializer to invoke the third instance constructor, which actually does the work of initializing the new instance.</span></span> <span data-ttu-id="143b6-1483">효과 사용 하면 선택적 생성자 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1483">The effect is that of optional constructor parameters:</span></span>
```csharp
Text t1 = new Text();                    // Same as Text(0, 0, null)
Text t2 = new Text(5, 10);               // Same as Text(5, 10, null)
Text t3 = new Text(5, 20, "Hello");
```

## <a name="static-constructors"></a><span data-ttu-id="143b6-1484">정적 생성자</span><span class="sxs-lookup"><span data-stu-id="143b6-1484">Static constructors</span></span>

<span data-ttu-id="143b6-1485">A ***정적 생성자*** 는 닫힌된 클래스 형식을 초기화 하는 데 필요한 작업을 구현 하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1485">A ***static constructor*** is a member that implements the actions required to initialize a closed class type.</span></span> <span data-ttu-id="143b6-1486">정적 생성자를 사용 하 여 선언 된 *static_constructor_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="143b6-1486">Static constructors are declared using *static_constructor_declaration*s:</span></span>

```antlr
static_constructor_declaration
    : attributes? static_constructor_modifiers identifier '(' ')' static_constructor_body
    ;

static_constructor_modifiers
    : 'extern'? 'static'
    | 'static' 'extern'?
    | static_constructor_modifiers_unsafe
    ;

static_constructor_body
    : block
    | ';'
    ;
```

<span data-ttu-id="143b6-1487">A *static_constructor_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)) 및 `extern` 한정자 ([외부메서드](classes.md#external-methods)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1487">A *static_constructor_declaration* may include a set of *attributes* ([Attributes](attributes.md)) and an `extern` modifier ([External methods](classes.md#external-methods)).</span></span>

<span data-ttu-id="143b6-1488">합니다 *식별자* 의 한 *static_constructor_declaration* 정적 생성자 선언 되는 클래스 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1488">The *identifier* of a *static_constructor_declaration* must name the class in which the static constructor is declared.</span></span> <span data-ttu-id="143b6-1489">다른 이름을 지정 하는 경우 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1489">If any other name is specified, a compile-time error occurs.</span></span>

<span data-ttu-id="143b6-1490">정적 생성자 선언에 포함 되어는 `extern` 한정자를 정적 생성자를 라고는 ***외부 정적 생성자***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1490">When a static constructor declaration includes an `extern` modifier, the static constructor is said to be an ***external static constructor***.</span></span> <span data-ttu-id="143b6-1491">외부 정적 생성자 선언에는 실제 구현을 제공 하기 때문에 해당 *static_constructor_body* 세미콜론으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1491">Because an external static constructor declaration provides no actual implementation, its *static_constructor_body* consists of a semicolon.</span></span> <span data-ttu-id="143b6-1492">다른 모든 정적 생성자 선언에 대 한 합니다 *static_constructor_body* 이루어져를 *블록* 클래스를 초기화 하기 위해 실행할 문을 지정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1492">For all other static constructor declarations, the *static_constructor_body* consists of a *block* which specifies the statements to execute in order to initialize the class.</span></span> <span data-ttu-id="143b6-1493">이 예제는 다음과 같습니다 합니다 *method_body* 사용 하 여 정적 메서드는 `void` 반환 형식 ([메서드 본문](classes.md#method-body)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1493">This corresponds exactly to the *method_body* of a static method with a `void` return type ([Method body](classes.md#method-body)).</span></span>

<span data-ttu-id="143b6-1494">정적 생성자는 상속 되지 않으며 직접 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1494">Static constructors are not inherited, and cannot be called directly.</span></span>

<span data-ttu-id="143b6-1495">닫힌된 클래스 형식에 대 한 정적 생성자는 지정 된 응용 프로그램 도메인에서 한 번만 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1495">The static constructor for a closed class type executes at most once in a given application domain.</span></span> <span data-ttu-id="143b6-1496">정적 생성자의 실행은 다음 이벤트 중 첫 번째 응용 프로그램 도메인 내에서 발생 하 여 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1496">The execution of a static constructor is triggered by the first of the following events to occur within an application domain:</span></span>

*  <span data-ttu-id="143b6-1497">클래스 형식의 인스턴스가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1497">An instance of the class type is created.</span></span>
*  <span data-ttu-id="143b6-1498">클래스 형식의 정적 멤버가 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1498">Any of the static members of the class type are referenced.</span></span>

<span data-ttu-id="143b6-1499">클래스를 포함 하는 경우는 `Main` 메서드 ([응용 프로그램 시작](basic-concepts.md#application-startup))에 실행이 시작 정적 생성자 보다 먼저 실행 되는 클래스에 대 한는 `Main` 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1499">If a class contains the `Main` method ([Application Startup](basic-concepts.md#application-startup)) in which execution begins, the static constructor for that class executes before the `Main` method is called.</span></span>

<span data-ttu-id="143b6-1500">새 닫힌된 클래스 형식에 정적 필드의 새 집합을 먼저 초기화 ([정적 및 인스턴스 필드](classes.md#static-and-instance-fields))에 해당 특정 닫힌된 유형이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1500">To initialize a new closed class type, first a new set of static fields ([Static and instance fields](classes.md#static-and-instance-fields)) for that particular closed type is created.</span></span> <span data-ttu-id="143b6-1501">각 정적 필드를 기본값으로 초기화 됩니다 ([기본값](variables.md#default-values)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1501">Each of the static fields is initialized to its default value ([Default values](variables.md#default-values)).</span></span> <span data-ttu-id="143b6-1502">다음으로 정적 필드 이니셜라이저 ([정적 필드 초기화](classes.md#static-field-initialization)) 정적 필드에 대해 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1502">Next, the static field initializers ([Static field initialization](classes.md#static-field-initialization)) are executed for those static fields.</span></span> <span data-ttu-id="143b6-1503">마지막으로, 정적 생성자가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1503">Finally, the static constructor is executed.</span></span>

<span data-ttu-id="143b6-1504">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-1504">The example</span></span>
```csharp
using System;

class Test
{
    static void Main() {
        A.F();
        B.F();
    }
}

class A
{
    static A() {
        Console.WriteLine("Init A");
    }
    public static void F() {
        Console.WriteLine("A.F");
    }
}

class B
{
    static B() {
        Console.WriteLine("Init B");
    }
    public static void F() {
        Console.WriteLine("B.F");
    }
}
```
<span data-ttu-id="143b6-1505">출력을 생성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1505">must produce the output:</span></span>
```
Init A
A.F
Init B
B.F
```
<span data-ttu-id="143b6-1506">때문에 실행 `A`의 정적 생성자에 대 한 호출에 의해 트리거되면 `A.F`, 및 실행 `B`의 정적 생성자에 대 한 호출에 의해 트리거되는 `B.F`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1506">because the execution of `A`'s static constructor is triggered by the call to `A.F`, and the execution of `B`'s static constructor is triggered by the call to `B.F`.</span></span>

<span data-ttu-id="143b6-1507">기본값 상태로 사용 되는 변수 이니셜라이저를 사용 하 여 정적 필드를 허용 하는 순환 종속성을 생성 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1507">It is possible to construct circular dependencies that allow static fields with variable initializers to be observed in their default value state.</span></span>

<span data-ttu-id="143b6-1508">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="143b6-1508">The example</span></span>
```csharp
using System;

class A
{
    public static int X;

    static A() {
        X = B.Y + 1;
    }
}

class B
{
    public static int Y = A.X + 1;

    static B() {}

    static void Main() {
        Console.WriteLine("X = {0}, Y = {1}", A.X, B.Y);
    }
}
```
<span data-ttu-id="143b6-1509">는 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1509">produces the output</span></span>
```
X = 1, Y = 2
```

<span data-ttu-id="143b6-1510">실행 하는 `Main` 메서드를 시스템에 대 한 이니셜라이저 처음 실행할 `B.Y`클래스에 이전, `B`의 정적 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1510">To execute the `Main` method, the system first runs the initializer for `B.Y`, prior to class `B`'s static constructor.</span></span> <span data-ttu-id="143b6-1511">`Y`이니셜라이저에서 `A`의 때문에 실행 하는 정적 생성자의 값 `A.X` 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1511">`Y`'s initializer causes `A`'s static constructor to be run because the value of `A.X` is referenced.</span></span> <span data-ttu-id="143b6-1512">정적 생성자 `A` 의 값을 계산 차례로 진행 `X`, 있으며 따라서 인출의 기본 값 `Y`, 0 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1512">The static constructor of `A` in turn proceeds to compute the value of `X`, and in doing so fetches the default value of `Y`, which is zero.</span></span> <span data-ttu-id="143b6-1513">`A.X` 1로 초기화 되므로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1513">`A.X` is thus initialized to 1.</span></span> <span data-ttu-id="143b6-1514">실행의 프로세스 `A`정적 필드 이니셜라이저 및 정적 생성자의 다음 완료 되 면의 초기 값을 계산 하려면 반환 `Y`, 결과 2가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1514">The process of running `A`'s static field initializers and static constructor then completes, returning to the calculation of the initial value of `Y`, the result of which becomes 2.</span></span>

<span data-ttu-id="143b6-1515">정적 생성자가 각 폐쇄형 생성 된 클래스 형식에 대 한 정확히 한 번 실행, 이므로 제약 조건을 통해 컴파일 타임에 검사할 수 없습니다. 형식 매개 변수에 대 한 런타임 검사를 적용 하는 데 편리한 위치 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1515">Because the static constructor is executed exactly once for each closed constructed class type, it is a convenient place to enforce run-time checks on the type parameter that cannot be checked at compile-time via constraints ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span> <span data-ttu-id="143b6-1516">예를 들어, 다음과 같은 형식이 열거형 형식 인수는 적용할 정적 생성자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1516">For example, the following type uses a static constructor to enforce that the type argument is an enum:</span></span>
```csharp
class Gen<T> where T: struct
{
    static Gen() {
        if (!typeof(T).IsEnum) {
            throw new ArgumentException("T must be an enum");
        }
    }
}
```

## <a name="destructors"></a><span data-ttu-id="143b6-1517">소멸자</span><span class="sxs-lookup"><span data-stu-id="143b6-1517">Destructors</span></span>

<span data-ttu-id="143b6-1518">A ***소멸자*** 는 클래스의 인스턴스를 소멸 하는 데 필요한 작업을 구현 하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1518">A ***destructor*** is a member that implements the actions required to destruct an instance of a class.</span></span> <span data-ttu-id="143b6-1519">소멸자를 사용 하 여 선언 되는 *destructor_declaration*:</span><span class="sxs-lookup"><span data-stu-id="143b6-1519">A destructor is declared using a *destructor_declaration*:</span></span>

```antlr
destructor_declaration
    : attributes? 'extern'? '~' identifier '(' ')' destructor_body
    | destructor_declaration_unsafe
    ;

destructor_body
    : block
    | ';'
    ;
```

<span data-ttu-id="143b6-1520">A *destructor_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1520">A *destructor_declaration* may include a set of *attributes* ([Attributes](attributes.md)).</span></span>

<span data-ttu-id="143b6-1521">합니다 *식별자* 의 한 *destructor_declaration* 소멸자가 선언 되는 클래스 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1521">The *identifier* of a *destructor_declaration* must name the class in which the destructor is declared.</span></span> <span data-ttu-id="143b6-1522">다른 이름을 지정 하는 경우 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1522">If any other name is specified, a compile-time error occurs.</span></span>

<span data-ttu-id="143b6-1523">소멸자 선언 포함 되는 경우는 `extern` 한정자를 소멸자를 라고는 ***외부 소멸자***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1523">When a destructor declaration includes an `extern` modifier, the destructor is said to be an ***external destructor***.</span></span> <span data-ttu-id="143b6-1524">외부 소멸자 선언은 실제 구현을 제공 하기 때문에 해당 *destructor_body* 세미콜론으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1524">Because an external destructor declaration provides no actual implementation, its *destructor_body* consists of a semicolon.</span></span> <span data-ttu-id="143b6-1525">다른 모든 소멸자에 대 한 합니다 *destructor_body* 이루어져를 *블록* 클래스의 인스턴스를 소멸 하기 위해 실행할 문을 지정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1525">For all other destructors, the *destructor_body* consists of a *block* which specifies the statements to execute in order to destruct an instance of the class.</span></span> <span data-ttu-id="143b6-1526">A *destructor_body* 정확 하 게 일치 합니다 *method_body* 사용 하 여 인스턴스 메서드를 `void` 반환 형식 ([메서드 본문](classes.md#method-body)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1526">A *destructor_body* corresponds exactly to the *method_body* of an instance method with a `void` return type ([Method body](classes.md#method-body)).</span></span>

<span data-ttu-id="143b6-1527">소멸자는 상속 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1527">Destructors are not inherited.</span></span> <span data-ttu-id="143b6-1528">따라서 클래스에는 해당 클래스에서 선언 될 수 있는 것 이외의 없는 소멸자</span><span class="sxs-lookup"><span data-stu-id="143b6-1528">Thus, a class has no destructors other than the one which may be declared in that class.</span></span>

<span data-ttu-id="143b6-1529">소멸자를 매개 변수가 없어야 하는 데 필요 하므로 클래스를 가질 수 있도록, 최대, 소멸자가 하나씩 오버 로드 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1529">Since a destructor is required to have no parameters, it cannot be overloaded, so a class can have, at most, one destructor.</span></span>

<span data-ttu-id="143b6-1530">소멸자는 자동으로 호출 및 명시적으로 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1530">Destructors are invoked automatically, and cannot be invoked explicitly.</span></span> <span data-ttu-id="143b6-1531">더 이상 해당 인스턴스를 사용 하는 코드에 대 한 가능한 경우 인스턴스를 소멸 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1531">An instance becomes eligible for destruction when it is no longer possible for any code to use that instance.</span></span> <span data-ttu-id="143b6-1532">실행 인스턴스에 대 한 소멸자의 인스턴스를 소멸할 수 있게 되 면 언제 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1532">Execution of the destructor for the instance may occur at any time after the instance becomes eligible for destruction.</span></span> <span data-ttu-id="143b6-1533">순서로 해당 인스턴스의 상속 체인의 소멸자가 호출 된 인스턴스는 소멸 됩니다을 하는 경우 가장 많이 파생 이상 파생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1533">When an instance is destructed, the destructors in that instance's inheritance chain are called, in order, from most derived to least derived.</span></span> <span data-ttu-id="143b6-1534">소멸자는 모든 스레드에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1534">A destructor may be executed on any thread.</span></span> <span data-ttu-id="143b6-1535">에 대 한 자세한 설명은 시기 및 소멸자가 실행 되는 방식을 제어 하는 규칙을 참조 하세요 [자동 메모리 관리](basic-concepts.md#automatic-memory-management)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1535">For further discussion of the rules that govern when and how a destructor is executed, see [Automatic memory management](basic-concepts.md#automatic-memory-management).</span></span>

<span data-ttu-id="143b6-1536">예제의 출력</span><span class="sxs-lookup"><span data-stu-id="143b6-1536">The output of the example</span></span>
```csharp
using System;

class A
{
    ~A() {
        Console.WriteLine("A's destructor");
    }
}

class B: A
{
    ~B() {
        Console.WriteLine("B's destructor");
    }
}

class Test
{
   static void Main() {
        B b = new B();
        b = null;
        GC.Collect();
        GC.WaitForPendingFinalizers();
   }
}
```
<span data-ttu-id="143b6-1537">is</span><span class="sxs-lookup"><span data-stu-id="143b6-1537">is</span></span>
```
B's destructor
A's destructor
```
<span data-ttu-id="143b6-1538">순서 대로 상속 체인의 소멸자가 호출 되므로 가장 많이 파생 이상 파생 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1538">since destructors in an inheritance chain are called in order, from most derived to least derived.</span></span>

<span data-ttu-id="143b6-1539">소멸자는 가상 메서드를 재정의 하 여 구현 됩니다 `Finalize` 에서 `System.Object`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1539">Destructors are implemented by overriding the virtual method `Finalize` on `System.Object`.</span></span> <span data-ttu-id="143b6-1540">이 메서드를 재정의 하거나 (또는 해당 재정의)를 호출 하는 C# 프로그램 허용 되지 않습니다 직접.</span><span class="sxs-lookup"><span data-stu-id="143b6-1540">C# programs are not permitted to override this method or call it (or overrides of it) directly.</span></span> <span data-ttu-id="143b6-1541">예를 들어 프로그램</span><span class="sxs-lookup"><span data-stu-id="143b6-1541">For instance, the program</span></span>
```csharp
class A 
{
    override protected void Finalize() {}    // error

    public void F() {
        this.Finalize();                     // error
    }
}
```
<span data-ttu-id="143b6-1542">두 가지 오류를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1542">contains two errors.</span></span>

<span data-ttu-id="143b6-1543">컴파일러는이 메서드를 재정의 하지만 전혀 존재 하지 않는 경우에 따라 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1543">The compiler behaves as if this method, and overrides of it, do not exist at all.</span></span> <span data-ttu-id="143b6-1544">따라서이 프로그램:</span><span class="sxs-lookup"><span data-stu-id="143b6-1544">Thus, this program:</span></span>
```csharp
class A 
{
    void Finalize() {}                            // permitted
}
```
<span data-ttu-id="143b6-1545">유효 하면 메서드가 표시 숨깁니다 `System.Object`의 `Finalize` 메서드.</span><span class="sxs-lookup"><span data-stu-id="143b6-1545">is valid, and the method shown hides `System.Object`'s `Finalize` method.</span></span>

<span data-ttu-id="143b6-1546">동작의 소멸자에서 예외가 throw 되 면 참조 [예외를 처리 하는 방법을](exceptions.md#how-exceptions-are-handled)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1546">For a discussion of the behavior when an exception is thrown from a destructor, see [How exceptions are handled](exceptions.md#how-exceptions-are-handled).</span></span>

## <a name="iterators"></a><span data-ttu-id="143b6-1547">반복기</span><span class="sxs-lookup"><span data-stu-id="143b6-1547">Iterators</span></span>

<span data-ttu-id="143b6-1548">함수 멤버 ([멤버 함수](expressions.md#function-members))은 반복기 블록이 사용 하 여 구현 ([블록](statements.md#blocks)) 호출 되는 ***반복기***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1548">A function member ([Function members](expressions.md#function-members)) implemented using an iterator block ([Blocks](statements.md#blocks)) is called an ***iterator***.</span></span>

<span data-ttu-id="143b6-1549">반복기 블록이 해당 하는 함수 멤버의 반환 형식 열거자 인터페이스 중 하나는 함수 멤버의 본문으로 사용할 수 있습니다 ([열거자 인터페이스](classes.md#enumerator-interfaces)) 또는 열거 가능 인터페이스 중 하나 ([열거 가능 인터페이스](classes.md#enumerable-interfaces)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1549">An iterator block may be used as the body of a function member as long as the return type of the corresponding function member is one of the enumerator interfaces ([Enumerator interfaces](classes.md#enumerator-interfaces)) or one of the enumerable interfaces ([Enumerable interfaces](classes.md#enumerable-interfaces)).</span></span> <span data-ttu-id="143b6-1550">으로 발생할 수 있습니다는 *method_body*를 *operator_body* 하거나 *accessor_body*반면 이벤트, 인스턴스 생성자, 정적 생성자 및 소멸자 수 없습니다 반복기로 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1550">It can occur as a *method_body*, *operator_body* or *accessor_body*, whereas events, instance constructors, static constructors and destructors cannot be implemented as iterators.</span></span>

<span data-ttu-id="143b6-1551">정식 매개 변수 목록 지정 하는 함수 멤버에 대 한 컴파일 시간 오류 것은 반복기 블록이 사용 하 여 함수 멤버 구현 될 때 `ref` 또는 `out` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1551">When a function member is implemented using an iterator block, it is a compile-time error for the formal parameter list of the function member to specify any `ref` or `out` parameters.</span></span>

### <a name="enumerator-interfaces"></a><span data-ttu-id="143b6-1552">열거자 인터페이스</span><span class="sxs-lookup"><span data-stu-id="143b6-1552">Enumerator interfaces</span></span>

<span data-ttu-id="143b6-1553">합니다 ***열거자 인터페이스*** 제네릭이 아닌 인터페이스는 `System.Collections.IEnumerator` 및 제네릭 인터페이스의 모든 인스턴스화에 `System.Collections.Generic.IEnumerator<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1553">The ***enumerator interfaces*** are the non-generic interface `System.Collections.IEnumerator` and all instantiations of the generic interface `System.Collections.Generic.IEnumerator<T>`.</span></span> <span data-ttu-id="143b6-1554">간단히 하기 위해이 챕터에 이러한 인터페이스 라고 `IEnumerator` 고 `IEnumerator<T>`, 각각.</span><span class="sxs-lookup"><span data-stu-id="143b6-1554">For the sake of brevity, in this chapter these interfaces are referenced as `IEnumerator` and `IEnumerator<T>`, respectively.</span></span>

### <a name="enumerable-interfaces"></a><span data-ttu-id="143b6-1555">열거 가능 인터페이스</span><span class="sxs-lookup"><span data-stu-id="143b6-1555">Enumerable interfaces</span></span>

<span data-ttu-id="143b6-1556">합니다 ***열거 가능 인터페이스*** 제네릭이 아닌 인터페이스는 `System.Collections.IEnumerable` 및 제네릭 인터페이스의 모든 인스턴스화에 `System.Collections.Generic.IEnumerable<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1556">The ***enumerable interfaces*** are the non-generic interface `System.Collections.IEnumerable` and all instantiations of the generic interface `System.Collections.Generic.IEnumerable<T>`.</span></span> <span data-ttu-id="143b6-1557">간단히 하기 위해이 챕터에 이러한 인터페이스 라고 `IEnumerable` 고 `IEnumerable<T>`, 각각.</span><span class="sxs-lookup"><span data-stu-id="143b6-1557">For the sake of brevity, in this chapter these interfaces are referenced as `IEnumerable` and `IEnumerable<T>`, respectively.</span></span>

### <a name="yield-type"></a><span data-ttu-id="143b6-1558">형식 생성</span><span class="sxs-lookup"><span data-stu-id="143b6-1558">Yield type</span></span>

<span data-ttu-id="143b6-1559">동일한 형식의 모든 값의 시퀀스를 생성 하는 반복기입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1559">An iterator produces a sequence of values, all of the same type.</span></span> <span data-ttu-id="143b6-1560">이 형식 이라고 합니다 ***형식을 생성*** 반복기의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1560">This type is called the ***yield type*** of the iterator.</span></span>

*  <span data-ttu-id="143b6-1561">반환 하는 반복기는 yield 유형의 `IEnumerator` 나 `IEnumerable` 는 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1561">The yield type of an iterator that returns `IEnumerator` or `IEnumerable` is `object`.</span></span>
*  <span data-ttu-id="143b6-1562">반환 하는 반복기는 yield 유형의 `IEnumerator<T>` 나 `IEnumerable<T>` 는 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1562">The yield type of an iterator that returns `IEnumerator<T>` or `IEnumerable<T>` is `T`.</span></span>

### <a name="enumerator-objects"></a><span data-ttu-id="143b6-1563">열거자 개체</span><span class="sxs-lookup"><span data-stu-id="143b6-1563">Enumerator objects</span></span>

<span data-ttu-id="143b6-1564">인터페이스 형식 열거자를 반환 합니다. 함수 멤버 반복기 블록을 사용 하 여 구현 될 때 호출 하는 함수 멤버 실행 되지 않습니다 즉시 코드 반복기 블록에서.</span><span class="sxs-lookup"><span data-stu-id="143b6-1564">When a function member returning an enumerator interface type is implemented using an iterator block, invoking the function member does not immediately execute the code in the iterator block.</span></span> <span data-ttu-id="143b6-1565">대신에 ***열거자 개체*** 가 만들어져 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1565">Instead, an ***enumerator object*** is created and returned.</span></span> <span data-ttu-id="143b6-1566">반복기 블록에 지정 된 코드를 캡슐화 하는이 개체 및 반복기 블록에서 코드의 실행이 발생 하는 경우 열거자 개체의 `MoveNext` 메서드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1566">This object encapsulates the code specified in the iterator block, and execution of the code in the iterator block occurs when the enumerator object's `MoveNext` method is invoked.</span></span> <span data-ttu-id="143b6-1567">열거자 개체에는 다음과 같은 특징이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1567">An enumerator object has the following characteristics:</span></span>

*  <span data-ttu-id="143b6-1568">구현 `IEnumerator` 하 고 `IEnumerator<T>`여기서 `T` 반복기의 yield 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1568">It implements `IEnumerator` and `IEnumerator<T>`, where `T` is the yield type of the iterator.</span></span>
*  <span data-ttu-id="143b6-1569">`System.IDisposable`을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1569">It implements `System.IDisposable`.</span></span>
*  <span data-ttu-id="143b6-1570">인수 값의 복사본으로 초기화 됩니다 (있는 경우) 및 함수 멤버에 전달 된 인스턴스 값입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1570">It is initialized with a copy of the argument values (if any) and instance value passed to the function member.</span></span>
*  <span data-ttu-id="143b6-1571">네 가지 상태만 있기 ***하기 전에***, ***실행***를 ***일시 중단***, 및 ***후***, 처음부터 및는 ***하기 전에***  상태입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1571">It has four potential states, ***before***, ***running***, ***suspended***, and ***after***, and is initially in the ***before*** state.</span></span>

<span data-ttu-id="143b6-1572">열거자 개체는 일반적으로 반복기 블록에서 코드를 캡슐화 하 고 열거자 인터페이스를 구현 하는 열거자 컴파일러에서 생성 된 클래스의 인스턴스 되지만 다른 메서드 구현 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1572">An enumerator object is typically an instance of a compiler-generated enumerator class that encapsulates the code in the iterator block and implements the enumerator interfaces, but other methods of implementation are possible.</span></span> <span data-ttu-id="143b6-1573">열거자 클래스는 컴파일러에서 생성 되 면 해당 클래스를 중첩할 수는, 직접 또는 간접적으로 함수 멤버를 포함 하는 클래스에서 private 액세스 가능성이 더 및 컴파일러 사용 하도록 예약 된 이름을 가진 것 ([식별자 ](lexical-structure.md#identifiers)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1573">If an enumerator class is generated by the compiler, that class will be nested, directly or indirectly, in the class containing the function member, it will have private accessibility, and it will have a name reserved for compiler use ([Identifiers](lexical-structure.md#identifiers)).</span></span>

<span data-ttu-id="143b6-1574">열거자 개체 위에 지정 된 것 보다 더 많은 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1574">An enumerator object may implement more interfaces than those specified above.</span></span>

<span data-ttu-id="143b6-1575">정확한 동작을 설명 하는 다음 섹션에서는 합니다 `MoveNext`, `Current`, 및 `Dispose` 의 멤버는 `IEnumerable` 및 `IEnumerable<T>` 인터페이스 구현을 열거자 개체에 의해 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1575">The following sections describe the exact behavior of the `MoveNext`, `Current`, and `Dispose` members of the `IEnumerable` and `IEnumerable<T>` interface implementations provided by an enumerator object.</span></span>

<span data-ttu-id="143b6-1576">열거자 개체를 지원 하지 않습니다는 `IEnumerator.Reset` 메서드.</span><span class="sxs-lookup"><span data-stu-id="143b6-1576">Note that enumerator objects do not support the `IEnumerator.Reset` method.</span></span> <span data-ttu-id="143b6-1577">이 메서드를 호출 하면를 `System.NotSupportedException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1577">Invoking this method causes a `System.NotSupportedException` to be thrown.</span></span>

#### <a name="the-movenext-method"></a><span data-ttu-id="143b6-1578">MoveNext 메서드</span><span class="sxs-lookup"><span data-stu-id="143b6-1578">The MoveNext method</span></span>

<span data-ttu-id="143b6-1579">`MoveNext` 열거자 개체의 메서드를 반복기 블록의 코드를 캡슐화 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1579">The `MoveNext` method of an enumerator object encapsulates the code of an iterator block.</span></span> <span data-ttu-id="143b6-1580">호출 된 `MoveNext` 집합과 반복기 블록에서 코드를 실행 하는 메서드를 `Current` 적절 하 게 열거자 개체의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1580">Invoking the `MoveNext` method executes code in the iterator block and sets the `Current` property of the enumerator object as appropriate.</span></span> <span data-ttu-id="143b6-1581">수행한 작업을 정확히 `MoveNext` 열거자 개체의 상태에 따라 달라 집니다 때 `MoveNext` 가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1581">The precise action performed by `MoveNext` depends on the state of the enumerator object when `MoveNext` is invoked:</span></span>

*  <span data-ttu-id="143b6-1582">열거자 개체의 상태가 ***하기 전에***호출, `MoveNext`:</span><span class="sxs-lookup"><span data-stu-id="143b6-1582">If the state of the enumerator object is ***before***, invoking `MoveNext`:</span></span>
   * <span data-ttu-id="143b6-1583">상태를 변경 합니다 ***실행***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1583">Changes the state to ***running***.</span></span>
   * <span data-ttu-id="143b6-1584">매개 변수를 초기화 (포함 하 여 `this`) 인수 값 및 인스턴스 값 열거자 개체 초기화 될 때 저장 된 반복기 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1584">Initializes the parameters (including `this`) of the iterator block to the argument values and instance value saved when the enumerator object was initialized.</span></span>
   * <span data-ttu-id="143b6-1585">(아래 설명 참조)으로 실행이 중단 될 때까지 반복기 블록 시작 부분에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1585">Executes the iterator block from the beginning until execution is interrupted (as described below).</span></span>
*  <span data-ttu-id="143b6-1586">열거자 개체의 상태가 ***실행***를 호출한 결과로 `MoveNext` 지정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1586">If the state of the enumerator object is ***running***, the result of invoking `MoveNext` is unspecified.</span></span>
*  <span data-ttu-id="143b6-1587">열거자 개체의 상태가 ***일시 중단***호출, `MoveNext`:</span><span class="sxs-lookup"><span data-stu-id="143b6-1587">If the state of the enumerator object is ***suspended***, invoking `MoveNext`:</span></span>
   * <span data-ttu-id="143b6-1588">상태를 변경 합니다 ***실행***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1588">Changes the state to ***running***.</span></span>
   * <span data-ttu-id="143b6-1589">반복기 블록의 실행이 일시 중단 된 마지막으로 저장 된 값으로 모든 지역 변수 및 매개 변수 (이 포함)의 값을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1589">Restores the values of all local variables and parameters (including this) to the values saved when execution of the iterator block was last suspended.</span></span> <span data-ttu-id="143b6-1590">Movenext 이전 호출 이후 변경 된 경우이 변수가 참조 하는 모든 개체의 내용을 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1590">Note that the contents of any objects referenced by these variables may have changed since the previous call to MoveNext.</span></span>
   * <span data-ttu-id="143b6-1591">바로 다음 반복기 블록의 실행을 다시 시작을 `yield return` 문 실행의 일시 중단이 발생입니다 (아래 설명 참조)으로 실행이 중단 될 때까지 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1591">Resumes execution of the iterator block immediately following the `yield return` statement that caused the suspension of execution and continues until execution is interrupted (as described below).</span></span>
*  <span data-ttu-id="143b6-1592">열거자 개체의 상태가 ***한 후***, 호출 `MoveNext` 반환 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1592">If the state of the enumerator object is ***after***, invoking `MoveNext` returns `false`.</span></span>


<span data-ttu-id="143b6-1593">때 `MoveNext` 반복기 블록을 실행 네 가지 방법으로 실행이 중단 될 수 있습니다: 여는 `yield return` 문는 `yield break` 문에서 발생 하는 반복기 블록의 끝에서 예외로 인해 throw 되 고 전파는 반복기 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1593">When `MoveNext` executes the iterator block, execution can be interrupted in four ways: By a `yield return` statement, by a `yield break` statement, by encountering the end of the iterator block, and by an exception being thrown and propagated out of the iterator block.</span></span>

*  <span data-ttu-id="143b6-1594">경우는 `yield return` 문이 ([yield 문을](statements.md#the-yield-statement)):</span><span class="sxs-lookup"><span data-stu-id="143b6-1594">When a `yield return` statement is encountered ([The yield statement](statements.md#the-yield-statement)):</span></span>
   * <span data-ttu-id="143b6-1595">문에 지정 된 식 계산, 암시적으로 yield 형식으로 변환 되어에 할당 된 `Current` 열거자 개체의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1595">The expression given in the statement is evaluated, implicitly converted to the yield type, and assigned to the `Current` property of the enumerator object.</span></span>
   * <span data-ttu-id="143b6-1596">반복기 본문의 실행을 일시 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1596">Execution of the iterator body is suspended.</span></span> <span data-ttu-id="143b6-1597">모든 지역 변수 및 매개 변수의 값 (포함 `this`)이 위치를 그대로 저장 됩니다 `yield return` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1597">The values of all local variables and parameters (including `this`) are saved, as is the location of this `yield return` statement.</span></span> <span data-ttu-id="143b6-1598">경우는 `yield return` 문 내에서 하나 이상의 됩니다 `try` 연결 된 블록 `finally` 지금은 블록이 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1598">If the `yield return` statement is within one or more `try` blocks, the associated `finally` blocks are not executed at this time.</span></span>
   * <span data-ttu-id="143b6-1599">열거자 개체의 상태가으로 변경 됩니다 ***일시 중단***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1599">The state of the enumerator object is changed to ***suspended***.</span></span>
   * <span data-ttu-id="143b6-1600">합니다 `MoveNext` 메서드가 반환 되는 `true` 는 반복 성공적으로 이동 하는 데 다음 값을 나타내는 해당 호출자에 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1600">The `MoveNext` method returns `true` to its caller, indicating that the iteration successfully advanced to the next value.</span></span>
*  <span data-ttu-id="143b6-1601">경우는 `yield break` 문이 ([yield 문을](statements.md#the-yield-statement)):</span><span class="sxs-lookup"><span data-stu-id="143b6-1601">When a `yield break` statement is encountered ([The yield statement](statements.md#the-yield-statement)):</span></span>
   * <span data-ttu-id="143b6-1602">경우는 `yield break` 문 내에서 하나 이상의 됩니다 `try` 연결 된 블록 `finally` 블록이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1602">If the `yield break` statement is within one or more `try` blocks, the associated `finally` blocks are executed.</span></span>
   * <span data-ttu-id="143b6-1603">열거자 개체의 상태가으로 변경 됩니다 ***후***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1603">The state of the enumerator object is changed to ***after***.</span></span>
   * <span data-ttu-id="143b6-1604">합니다 `MoveNext` 메서드가 반환 되는 `false` 반복 완료 되었음을 나타내는 호출자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1604">The `MoveNext` method returns `false` to its caller, indicating that the iteration is complete.</span></span>
*  <span data-ttu-id="143b6-1605">반복기 본문의 끝 발생 시:</span><span class="sxs-lookup"><span data-stu-id="143b6-1605">When the end of the iterator body is encountered:</span></span>
   * <span data-ttu-id="143b6-1606">열거자 개체의 상태가으로 변경 됩니다 ***후***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1606">The state of the enumerator object is changed to ***after***.</span></span>
   * <span data-ttu-id="143b6-1607">합니다 `MoveNext` 메서드가 반환 되는 `false` 반복 완료 되었음을 나타내는 호출자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1607">The `MoveNext` method returns `false` to its caller, indicating that the iteration is complete.</span></span>
*  <span data-ttu-id="143b6-1608">예외가 throw 되 고 반복기 블록에서 전파 하면:</span><span class="sxs-lookup"><span data-stu-id="143b6-1608">When an exception is thrown and propagated out of the iterator block:</span></span>
   * <span data-ttu-id="143b6-1609">적절 한 `finally` 반복기 본문의 요소는 예외 전파 하 여 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1609">Appropriate `finally` blocks in the iterator body will have been executed by the exception propagation.</span></span>
   * <span data-ttu-id="143b6-1610">열거자 개체의 상태가으로 변경 됩니다 ***후***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1610">The state of the enumerator object is changed to ***after***.</span></span>
   * <span data-ttu-id="143b6-1611">호출자에 게 계속 예외 전파를 `MoveNext` 메서드.</span><span class="sxs-lookup"><span data-stu-id="143b6-1611">The exception propagation continues to the caller of the `MoveNext` method.</span></span>

#### <a name="the-current-property"></a><span data-ttu-id="143b6-1612">현재 속성</span><span class="sxs-lookup"><span data-stu-id="143b6-1612">The Current property</span></span>

<span data-ttu-id="143b6-1613">열거자 개체의 `Current` 속성은 영향을 받지 `yield return` 반복기 블록에서 문입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1613">An enumerator object's `Current` property is affected by `yield return` statements in the iterator block.</span></span>

<span data-ttu-id="143b6-1614">열거자 개체의 경우는 ***일시 중단*** 상태, 값 `Current` 에 대 한 이전 호출에서 설정한 값은 `MoveNext`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1614">When an enumerator object is in the ***suspended*** state, the value of `Current` is the value set by the previous call to `MoveNext`.</span></span> <span data-ttu-id="143b6-1615">열거자 개체의 경우는 ***하기 전에***를 ***실행***, 또는 ***후*** 상태를 결과 액세스 하는 `Current` 지정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1615">When an enumerator object is in the ***before***, ***running***, or ***after*** states, the result of accessing `Current` is unspecified.</span></span>

<span data-ttu-id="143b6-1616">Yield 사용 하는 반복기에 대 한 입력 이외의 `object`에 액세스 하는 결과 `Current` 열거자 개체를 통해 `IEnumerable` 구현에 액세스 하려면 해당 `Current` 열거자 개체를 통해 `IEnumerator<T>` 구현 및 결과를 캐스팅 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1616">For an iterator with a yield type other than `object`, the result of accessing `Current` through the enumerator object's `IEnumerable` implementation corresponds to accessing `Current` through the enumerator object's `IEnumerator<T>` implementation and casting the result to `object`.</span></span>

#### <a name="the-dispose-method"></a><span data-ttu-id="143b6-1617">Dispose 메서드</span><span class="sxs-lookup"><span data-stu-id="143b6-1617">The Dispose method</span></span>

<span data-ttu-id="143b6-1618">`Dispose` 메서드를 사용는 열거자 개체를 가져와서 반복을 정리 합니다 ***후*** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1618">The `Dispose` method is used to clean up the iteration by bringing the enumerator object to the ***after*** state.</span></span>

*  <span data-ttu-id="143b6-1619">열거자 개체의 상태가 ***하기 전에***, 호출 `Dispose` 상태를 변경 합니다 ***후***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1619">If the state of the enumerator object is ***before***, invoking `Dispose` changes the state to ***after***.</span></span>
*  <span data-ttu-id="143b6-1620">열거자 개체의 상태가 ***실행***를 호출한 결과로 `Dispose` 지정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1620">If the state of the enumerator object is ***running***, the result of invoking `Dispose` is unspecified.</span></span>
*  <span data-ttu-id="143b6-1621">열거자 개체의 상태가 ***일시 중단***호출, `Dispose`:</span><span class="sxs-lookup"><span data-stu-id="143b6-1621">If the state of the enumerator object is ***suspended***, invoking `Dispose`:</span></span>
   * <span data-ttu-id="143b6-1622">상태를 변경 합니다 ***실행***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1622">Changes the state to ***running***.</span></span>
   * <span data-ttu-id="143b6-1623">실행 된 마지막 블록 마지막으로 실행 된 것 처럼 `yield return` 문이 된를 `yield break` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1623">Executes any finally blocks as if the last executed `yield return` statement were a `yield break` statement.</span></span> <span data-ttu-id="143b6-1624">열거자 개체의 상태를로 예외를 throw 하 고 반복기 본문 밖으로 전파할 수 이면 ***한 후*** 예외를 호출자에 게 전파 되는 `Dispose` 메서드.</span><span class="sxs-lookup"><span data-stu-id="143b6-1624">If this causes an exception to be thrown and propagated out of the iterator body, the state of the enumerator object is set to ***after*** and the exception is propagated to the caller of the `Dispose` method.</span></span>
   * <span data-ttu-id="143b6-1625">상태를 변경 합니다 ***후***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1625">Changes the state to ***after***.</span></span>
*  <span data-ttu-id="143b6-1626">열거자 개체의 상태가 ***한 후***호출, `Dispose` 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1626">If the state of the enumerator object is ***after***, invoking `Dispose` has no affect.</span></span>

### <a name="enumerable-objects"></a><span data-ttu-id="143b6-1627">열거 가능한 개체</span><span class="sxs-lookup"><span data-stu-id="143b6-1627">Enumerable objects</span></span>

<span data-ttu-id="143b6-1628">함수 멤버를 열거 가능한 인터페이스 형식을 반환은 반복기 블록이 사용 하 여 구현 될 때 호출 하는 함수 멤버 실행 되지 않습니다 즉시 코드 반복기 블록에서.</span><span class="sxs-lookup"><span data-stu-id="143b6-1628">When a function member returning an enumerable interface type is implemented using an iterator block, invoking the function member does not immediately execute the code in the iterator block.</span></span> <span data-ttu-id="143b6-1629">대신는 ***열거 가능한 개체*** 가 만들어져 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1629">Instead, an ***enumerable object*** is created and returned.</span></span> <span data-ttu-id="143b6-1630">열거 가능한 개체의 `GetEnumerator` 반환 반복기 블록에서 코드를 캡슐화 하는 열거자 개체를 지정 하 고 반복기 블록에서 코드의 실행이 발생 경우 열거자 개체의 `MoveNext` 메서드가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1630">The enumerable object's `GetEnumerator` method returns an enumerator object that encapsulates the code specified in the iterator block, and execution of the code in the iterator block occurs when the enumerator object's `MoveNext` method is invoked.</span></span> <span data-ttu-id="143b6-1631">열거 가능한 개체에는 다음과 같은 특징이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1631">An enumerable object has the following characteristics:</span></span>

*  <span data-ttu-id="143b6-1632">구현 `IEnumerable` 하 고 `IEnumerable<T>`여기서 `T` 반복기의 yield 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1632">It implements `IEnumerable` and `IEnumerable<T>`, where `T` is the yield type of the iterator.</span></span>
*  <span data-ttu-id="143b6-1633">인수 값의 복사본으로 초기화 됩니다 (있는 경우) 및 함수 멤버에 전달 된 인스턴스 값입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1633">It is initialized with a copy of the argument values (if any) and instance value passed to the function member.</span></span>

<span data-ttu-id="143b6-1634">열거 가능한 개체는 일반적으로 반복기 블록에서 코드를 캡슐화 하 고 열거 가능한 인터페이스를 구현 하는 컴파일러에서 생성 된 enumerable 클래스의 인스턴스 되지만 다른 메서드 구현 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1634">An enumerable object is typically an instance of a compiler-generated enumerable class that encapsulates the code in the iterator block and implements the enumerable interfaces, but other methods of implementation are possible.</span></span> <span data-ttu-id="143b6-1635">Enumerable 클래스는 컴파일러에서 생성 되 면 해당 클래스를 중첩할 수는, 직접 또는 간접적으로 함수 멤버를 포함 하는 클래스에서 private 액세스 가능성이 더 및 컴파일러 사용 하도록 예약 된 이름을 가진 것 ([식별자 ](lexical-structure.md#identifiers)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1635">If an enumerable class is generated by the compiler, that class will be nested, directly or indirectly, in the class containing the function member, it will have private accessibility, and it will have a name reserved for compiler use ([Identifiers](lexical-structure.md#identifiers)).</span></span>

<span data-ttu-id="143b6-1636">열거 가능한 개체 위에 지정 된 것 보다 더 많은 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1636">An enumerable object may implement more interfaces than those specified above.</span></span> <span data-ttu-id="143b6-1637">특히 열거 가능한 개체 구현할 수도 있습니다 `IEnumerator` 고 `IEnumerator<T>`, 열거 및 열거자로 제공할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1637">In particular, an enumerable object may also implement `IEnumerator` and `IEnumerator<T>`, enabling it to serve as both an enumerable and an enumerator.</span></span> <span data-ttu-id="143b6-1638">해당 형식의 구현, 처음 열거 가능한 개체의 `GetEnumerator` 메서드를 호출 하면 열거 가능한 개체 자체가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1638">In that type of implementation, the first time an enumerable object's `GetEnumerator` method is invoked, the enumerable object itself is returned.</span></span> <span data-ttu-id="143b6-1639">열거 가능한 개체의 후속 호출 `GetEnumerator`이면 있는 열거 가능한 개체의 복사본을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1639">Subsequent invocations of the enumerable object's `GetEnumerator`, if any, return a copy of the enumerable object.</span></span> <span data-ttu-id="143b6-1640">따라서 반환 된 각 열거자에는 자체 상태 및 하나의 열거자에 대 한 변경 내용을 다른 레코드에 영향을 주지는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1640">Thus, each returned enumerator has its own state and changes in one enumerator will not affect another.</span></span>

#### <a name="the-getenumerator-method"></a><span data-ttu-id="143b6-1641">GetEnumerator 메서드가</span><span class="sxs-lookup"><span data-stu-id="143b6-1641">The GetEnumerator method</span></span>

<span data-ttu-id="143b6-1642">열거 가능한 개체의 구현을 제공 합니다 `GetEnumerator` 의 메서드를 `IEnumerable` 및 `IEnumerable<T>` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1642">An enumerable object provides an implementation of the `GetEnumerator` methods of the `IEnumerable` and `IEnumerable<T>` interfaces.</span></span> <span data-ttu-id="143b6-1643">두 `GetEnumerator` 메서드 획득 하 고 사용할 수 있는 열거자 개체를 반환 하는 일반적인 구현을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1643">The two `GetEnumerator` methods share a common implementation that acquires and returns an available enumerator object.</span></span> <span data-ttu-id="143b6-1644">열거자 개체 인수 값으로 초기화 되 고 인스턴스 열거 가능 개체를 초기화 하지만 그렇지 않으면 때 저장 된 값에 설명 된 대로 열거자 개체 함수 [열거자 개체](classes.md#enumerator-objects)합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1644">The enumerator object is initialized with the argument values and instance value saved when the enumerable object was initialized, but otherwise the enumerator object functions as described in [Enumerator objects](classes.md#enumerator-objects).</span></span>

### <a name="implementation-example"></a><span data-ttu-id="143b6-1645">구현 예제</span><span class="sxs-lookup"><span data-stu-id="143b6-1645">Implementation example</span></span>

<span data-ttu-id="143b6-1646">이 섹션에서는 표준 C# 구문 측면에서 반복기의 가능한 구현을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1646">This section describes a possible implementation of iterators in terms of standard C# constructs.</span></span> <span data-ttu-id="143b6-1647">여기에 설명 된 구현은 Microsoft C# 컴파일러에 의해 사용 되는 동일한 원칙에 기반 하지만 위임된 구현 또는 하나의 가능한 되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1647">The implementation described here is based on the same principles used by the Microsoft C# compiler, but it is by no means a mandated implementation or the only one possible.</span></span>

<span data-ttu-id="143b6-1648">다음 `Stack<T>` 구현 클래스는 `GetEnumerator` 반복기를 사용 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="143b6-1648">The following `Stack<T>` class implements its `GetEnumerator` method using an iterator.</span></span> <span data-ttu-id="143b6-1649">위에서 아래 순 스택의의 요소를 열거 하는 반복기입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1649">The iterator enumerates the elements of the stack in top to bottom order.</span></span>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;

class Stack<T>: IEnumerable<T>
{
    T[] items;
    int count;

    public void Push(T item) {
        if (items == null) {
            items = new T[4];
        }
        else if (items.Length == count) {
            T[] newItems = new T[count * 2];
            Array.Copy(items, 0, newItems, 0, count);
            items = newItems;
        }
        items[count++] = item;
    }

    public T Pop() {
        T result = items[--count];
        items[count] = default(T);
        return result;
    }

    public IEnumerator<T> GetEnumerator() {
        for (int i = count - 1; i >= 0; --i) yield return items[i];
    }
}
```

<span data-ttu-id="143b6-1650">`GetEnumerator` 메서드 다음에 표시 된 대로 반복기 블록에서 코드를 캡슐화 하는 열거자 컴파일러에서 생성 된 클래스의 인스턴스화로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1650">The `GetEnumerator` method can be translated into an instantiation of a compiler-generated enumerator class that encapsulates the code in the iterator block, as shown in the following.</span></span>

```csharp
class Stack<T>: IEnumerable<T>
{
    ...

    public IEnumerator<T> GetEnumerator() {
        return new __Enumerator1(this);
    }

    class __Enumerator1: IEnumerator<T>, IEnumerator
    {
        int __state;
        T __current;
        Stack<T> __this;
        int i;

        public __Enumerator1(Stack<T> __this) {
            this.__this = __this;
        }

        public T Current {
            get { return __current; }
        }

        object IEnumerator.Current {
            get { return __current; }
        }

        public bool MoveNext() {
            switch (__state) {
                case 1: goto __state1;
                case 2: goto __state2;
            }
            i = __this.count - 1;
        __loop:
            if (i < 0) goto __state2;
            __current = __this.items[i];
            __state = 1;
            return true;
        __state1:
            --i;
            goto __loop;
        __state2:
            __state = 2;
            return false;
        }

        public void Dispose() {
            __state = 2;
        }

        void IEnumerator.Reset() {
            throw new NotSupportedException();
        }
    }
}
```

<span data-ttu-id="143b6-1651">이전 번역을 반복기 블록에서 코드가 상태 시스템으로 설정 되 고 있는 `MoveNext` 열거자 클래스의 메서드.</span><span class="sxs-lookup"><span data-stu-id="143b6-1651">In the preceding translation, the code in the iterator block is turned into a state machine and placed in the `MoveNext` method of the enumerator class.</span></span> <span data-ttu-id="143b6-1652">또한 지역 변수 `i` 호출의 존재를 계속할 수 있도록 열거자 개체의 필드로 꺼져 `MoveNext`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1652">Furthermore, the local variable `i` is turned into a field in the enumerator object so it can continue to exist across invocations of `MoveNext`.</span></span>

<span data-ttu-id="143b6-1653">다음 예제에서는 1부터 10 까지의 정수의 단순 곱셈표를 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1653">The following example prints a simple multiplication table of the integers 1 through 10.</span></span> <span data-ttu-id="143b6-1654">`FromTo` 예제의 메서드 열거 가능한 개체를 반환 하며 반복기를 사용 하 여 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1654">The `FromTo` method in the example returns an enumerable object and is implemented using an iterator.</span></span>

```csharp
using System;
using System.Collections.Generic;

class Test
{
    static IEnumerable<int> FromTo(int from, int to) {
        while (from <= to) yield return from++;
    }

    static void Main() {
        IEnumerable<int> e = FromTo(1, 10);
        foreach (int x in e) {
            foreach (int y in e) {
                Console.Write("{0,3} ", x * y);
            }
            Console.WriteLine();
        }
    }
}
```

<span data-ttu-id="143b6-1655">`FromTo` 메서드 다음에 표시 된 대로 반복기 블록에서 코드를 캡슐화 하는 컴파일러에서 생성 된 enumerable 클래스의 인스턴스화로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1655">The `FromTo` method can be translated into an instantiation of a compiler-generated enumerable class that encapsulates the code in the iterator block, as shown in the following.</span></span>

```csharp
using System;
using System.Threading;
using System.Collections;
using System.Collections.Generic;

class Test
{
    ...

    static IEnumerable<int> FromTo(int from, int to) {
        return new __Enumerable1(from, to);
    }

    class __Enumerable1:
        IEnumerable<int>, IEnumerable,
        IEnumerator<int>, IEnumerator
    {
        int __state;
        int __current;
        int __from;
        int from;
        int to;
        int i;

        public __Enumerable1(int __from, int to) {
            this.__from = __from;
            this.to = to;
        }

        public IEnumerator<int> GetEnumerator() {
            __Enumerable1 result = this;
            if (Interlocked.CompareExchange(ref __state, 1, 0) != 0) {
                result = new __Enumerable1(__from, to);
                result.__state = 1;
            }
            result.from = result.__from;
            return result;
        }

        IEnumerator IEnumerable.GetEnumerator() {
            return (IEnumerator)GetEnumerator();
        }

        public int Current {
            get { return __current; }
        }

        object IEnumerator.Current {
            get { return __current; }
        }

        public bool MoveNext() {
            switch (__state) {
            case 1:
                if (from > to) goto case 2;
                __current = from++;
                __state = 1;
                return true;
            case 2:
                __state = 2;
                return false;
            default:
                throw new InvalidOperationException();
            }
        }

        public void Dispose() {
            __state = 2;
        }

        void IEnumerator.Reset() {
            throw new NotSupportedException();
        }
    }
}
```

<span data-ttu-id="143b6-1656">Enumerable 클래스는 열거 가능 인터페이스 및 열거자 인터페이스, 열거형 및 열거자로 제공할 수 있도록 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1656">The enumerable class implements both the enumerable interfaces and the enumerator interfaces, enabling it to serve as both an enumerable and an enumerator.</span></span> <span data-ttu-id="143b6-1657">처음으로 `GetEnumerator` 메서드를 호출 하면 열거 가능한 개체 자체가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1657">The first time the `GetEnumerator` method is invoked, the enumerable object itself is returned.</span></span> <span data-ttu-id="143b6-1658">열거 가능한 개체의 후속 호출 `GetEnumerator`이면 있는 열거 가능한 개체의 복사본을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1658">Subsequent invocations of the enumerable object's `GetEnumerator`, if any, return a copy of the enumerable object.</span></span> <span data-ttu-id="143b6-1659">따라서 반환 된 각 열거자에는 자체 상태 및 하나의 열거자에 대 한 변경 내용을 다른 레코드에 영향을 주지는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1659">Thus, each returned enumerator has its own state and changes in one enumerator will not affect another.</span></span> <span data-ttu-id="143b6-1660">`Interlocked.CompareExchange` 스레드로부터 안전한 작업 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1660">The `Interlocked.CompareExchange` method is used to ensure thread-safe operation.</span></span>

<span data-ttu-id="143b6-1661">합니다 `from` 및 `to` 매개 변수는 enumerable 클래스의 필드로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1661">The `from` and `to` parameters are turned into fields in the enumerable class.</span></span> <span data-ttu-id="143b6-1662">때문에 `from` 은 추가 반복기 블록에서 수정할 `__from` 필드에 지정 된 초기 값을 저장 하기 위해 도입 되었습니다 `from` 각 열거자에 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1662">Because `from` is modified in the iterator block, an additional `__from` field is introduced to hold the initial value given to `from` in each enumerator.</span></span>

<span data-ttu-id="143b6-1663">합니다 `MoveNext` 메서드가 throw를 `InvalidOperationException` 때 호출 되 면 `__state` 는 `0`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1663">The `MoveNext` method throws an `InvalidOperationException` if it is called when `__state` is `0`.</span></span> <span data-ttu-id="143b6-1664">이 첫 번째 호출 하지 않고 열거자 개체를 열거 가능한 개체의 사용을 방지 `GetEnumerator`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1664">This protects against use of the enumerable object as an enumerator object without first calling `GetEnumerator`.</span></span>

<span data-ttu-id="143b6-1665">다음 예제에서는 간단한 트리에서 클래스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1665">The following example shows a simple tree class.</span></span> <span data-ttu-id="143b6-1666">합니다 `Tree<T>` 구현 클래스 해당 `GetEnumerator` 반복기를 사용 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1666">The `Tree<T>` class implements its `GetEnumerator` method using an iterator.</span></span> <span data-ttu-id="143b6-1667">반복기 중 위 순서로 트리의 요소를 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1667">The iterator enumerates the elements of the tree in infix order.</span></span>

```csharp
using System;
using System.Collections.Generic;

class Tree<T>: IEnumerable<T>
{
    T value;
    Tree<T> left;
    Tree<T> right;

    public Tree(T value, Tree<T> left, Tree<T> right) {
        this.value = value;
        this.left = left;
        this.right = right;
    }

    public IEnumerator<T> GetEnumerator() {
        if (left != null) foreach (T x in left) yield x;
        yield value;
        if (right != null) foreach (T x in right) yield x;
    }
}

class Program
{
    static Tree<T> MakeTree<T>(T[] items, int left, int right) {
        if (left > right) return null;
        int i = (left + right) / 2;
        return new Tree<T>(items[i], 
            MakeTree(items, left, i - 1),
            MakeTree(items, i + 1, right));
    }

    static Tree<T> MakeTree<T>(params T[] items) {
        return MakeTree(items, 0, items.Length - 1);
    }

    // The output of the program is:
    // 1 2 3 4 5 6 7 8 9
    // Mon Tue Wed Thu Fri Sat Sun

    static void Main() {
        Tree<int> ints = MakeTree(1, 2, 3, 4, 5, 6, 7, 8, 9);
        foreach (int i in ints) Console.Write("{0} ", i);
        Console.WriteLine();

        Tree<string> strings = MakeTree(
            "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun");
        foreach (string s in strings) Console.Write("{0} ", s);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="143b6-1668">`GetEnumerator` 메서드 다음에 표시 된 대로 반복기 블록에서 코드를 캡슐화 하는 열거자 컴파일러에서 생성 된 클래스의 인스턴스화로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1668">The `GetEnumerator` method can be translated into an instantiation of a compiler-generated enumerator class that encapsulates the code in the iterator block, as shown in the following.</span></span>

```csharp
class Tree<T>: IEnumerable<T>
{
    ...

    public IEnumerator<T> GetEnumerator() {
        return new __Enumerator1(this);
    }

    class __Enumerator1 : IEnumerator<T>, IEnumerator
    {
        Node<T> __this;
        IEnumerator<T> __left, __right;
        int __state;
        T __current;

        public __Enumerator1(Node<T> __this) {
            this.__this = __this;
        }

        public T Current {
            get { return __current; }
        }

        object IEnumerator.Current {
            get { return __current; }
        }

        public bool MoveNext() {
            try {
                switch (__state) {

                case 0:
                    __state = -1;
                    if (__this.left == null) goto __yield_value;
                    __left = __this.left.GetEnumerator();
                    goto case 1;

                case 1:
                    __state = -2;
                    if (!__left.MoveNext()) goto __left_dispose;
                    __current = __left.Current;
                    __state = 1;
                    return true;

                __left_dispose:
                    __state = -1;
                    __left.Dispose();

                __yield_value:
                    __current = __this.value;
                    __state = 2;
                    return true;

                case 2:
                    __state = -1;
                    if (__this.right == null) goto __end;
                    __right = __this.right.GetEnumerator();
                    goto case 3;

                case 3:
                    __state = -3;
                    if (!__right.MoveNext()) goto __right_dispose;
                    __current = __right.Current;
                    __state = 3;
                    return true;

                __right_dispose:
                    __state = -1;
                    __right.Dispose();

                __end:
                    __state = 4;
                    break;

                }
            }
            finally {
                if (__state < 0) Dispose();
            }
            return false;
        }

        public void Dispose() {
            try {
                switch (__state) {

                case 1:
                case -2:
                    __left.Dispose();
                    break;

                case 3:
                case -3:
                    __right.Dispose();
                    break;

                }
            }
            finally {
                __state = 4;
            }
        }

        void IEnumerator.Reset() {
            throw new NotSupportedException();
        }
    }
}
```

<span data-ttu-id="143b6-1669">에 사용 되는 컴파일러에서 생성 된 임시 개체는 `foreach` 로 문 리프팅되며 합니다 `__left` 및 `__right` 열거자 개체의 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1669">The compiler generated temporaries used in the `foreach` statements are lifted into the `__left` and `__right` fields of the enumerator object.</span></span> <span data-ttu-id="143b6-1670">`__state` 열거자 개체의 필드 업데이트 신중 하 게 됩니다 있도록 올바른 `Dispose()` 메서드가 호출 됩니다 올바르게 경우 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1670">The `__state` field of the enumerator object is carefully updated so that the correct `Dispose()` method will be called correctly if an exception is thrown.</span></span> <span data-ttu-id="143b6-1671">간단한을 사용 하 여 번역 된 코드를 작성할 수는 `foreach` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1671">Note that it is not possible to write the translated code with simple `foreach` statements.</span></span>

## <a name="async-functions"></a><span data-ttu-id="143b6-1672">비동기 함수</span><span class="sxs-lookup"><span data-stu-id="143b6-1672">Async functions</span></span>

<span data-ttu-id="143b6-1673">메서드 ([메서드](classes.md#methods)) 또는 익명 함수 ([익명 함수 식](expressions.md#anonymous-function-expressions))으로 `async` 한정자 라고는 ***비동기 함수***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1673">A method ([Methods](classes.md#methods)) or anonymous function ([Anonymous function expressions](expressions.md#anonymous-function-expressions)) with the `async` modifier is called an ***async function***.</span></span> <span data-ttu-id="143b6-1674">일반적으로 용어 ***비동기*** 모든 종류의 함수를 설명 하는 데 사용 되는 `async` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1674">In general, the term ***async*** is used to describe any kind of function that has the `async` modifier.</span></span>

<span data-ttu-id="143b6-1675">정식 매개 변수 목록 지정 하는 비동기 함수에 대 한 컴파일 타임 오류 `ref` 또는 `out` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1675">It is a compile-time error for the formal parameter list of an async function to specify any `ref` or `out` parameters.</span></span>

<span data-ttu-id="143b6-1676">합니다 *return_type* 의 비동기 메서드 중 하나 여야 합니다 `void` 또는 ***작업 종류***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1676">The *return_type* of an async method must be either `void` or a ***task type***.</span></span> <span data-ttu-id="143b6-1677">작업 유형은 `System.Threading.Tasks.Task` 에서 생성 된 형식 및 `System.Threading.Tasks.Task<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1677">The task types are `System.Threading.Tasks.Task` and types constructed from `System.Threading.Tasks.Task<T>`.</span></span> <span data-ttu-id="143b6-1678">간단히 하기 위해이 챕터에 이러한 형식은 라고 `Task` 및 `Task<T>`, 각각.</span><span class="sxs-lookup"><span data-stu-id="143b6-1678">For the sake of brevity, in this chapter these types are referenced as `Task` and `Task<T>`, respectively.</span></span> <span data-ttu-id="143b6-1679">작업 형식을 반환 비동기 메서드는 작업을 반환 하 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1679">An async method returning a task type is said to be task-returning.</span></span>

<span data-ttu-id="143b6-1680">작업 유형은의 정확한 정의 구현 정의 이지만 언어의 관점에서 작업 유형 성공 또는 오류가 발생 한 완료 되지 않은 상태 중 하나가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1680">The exact definition of the task types is implementation defined, but from the language's point of view a task type is in one of the states incomplete, succeeded or faulted.</span></span> <span data-ttu-id="143b6-1681">오류가 발생 한 작업 관련 예외를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1681">A faulted task records a pertinent exception.</span></span> <span data-ttu-id="143b6-1682">성공 `Task<T>` 형식의 결과 기록 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1682">A succeeded `Task<T>` records a result of type `T`.</span></span> <span data-ttu-id="143b6-1683">작업 형식에는 대기 가능, 및의 피연산자가 될 수 있습니다 await 식 ([Await 식](expressions.md#await-expressions)).</span><span class="sxs-lookup"><span data-stu-id="143b6-1683">Task types are awaitable, and can therefore be the operands of await expressions ([Await expressions](expressions.md#await-expressions)).</span></span>

<span data-ttu-id="143b6-1684">비동기 함수 호출에 계산을 일시 중단 하는 기능 이용 하 여 await 식 ([Await 식](expressions.md#await-expressions)) 본문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1684">An async function invocation has the ability to suspend evaluation by means of await expressions ([Await expressions](expressions.md#await-expressions)) in its body.</span></span> <span data-ttu-id="143b6-1685">평가 될 수 있습니다 나중에 다시 시작할 일시 중단 된 시점에서 await 식 방법으로 ***다시 시작 대리자***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1685">Evaluation may later be resumed at the point of the suspending await expression by means of a ***resumption delegate***.</span></span> <span data-ttu-id="143b6-1686">다시 시작 대리자 형식입니다 `System.Action`, 고 중단 된 await 식에서 비동기 함수 호출의 평가 다시 시작 됩니다 호출 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1686">The resumption delegate is of type `System.Action`, and when it is invoked, evaluation of the async function invocation will resume from the await expression where it left off.</span></span> <span data-ttu-id="143b6-1687">합니다 ***현재 호출자*** 비동기 함수의 호출 라인인 함수를 호출 하지 일시 중단 된 경우 원래 호출자 또는 다시 시작 대리자의 가장 최근 호출자입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1687">The ***current caller*** of an async function invocation is the original caller if the function invocation has never been suspended, or the most recent caller of the resumption delegate otherwise.</span></span>

### <a name="evaluation-of-a-task-returning-async-function"></a><span data-ttu-id="143b6-1688">작업 반환 비동기 함수 계산</span><span class="sxs-lookup"><span data-stu-id="143b6-1688">Evaluation of a task-returning async function</span></span>

<span data-ttu-id="143b6-1689">작업 반환 비동기 함수를 호출 하면 반환 된 작업 유형 생성할 인스턴스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1689">Invocation of a task-returning async function causes an instance of the returned task type to be generated.</span></span> <span data-ttu-id="143b6-1690">이 호출 되는 ***task 반환*** 비동기 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1690">This is called the ***return task*** of the async function.</span></span> <span data-ttu-id="143b6-1691">작업이 처음에 불완전 한 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1691">The task is initially in an incomplete state.</span></span>

<span data-ttu-id="143b6-1692">비동기 함수 본문은 다음 지점 제어 반환 함께 호출자에 게 반환 되는 중 (await 식에 도달)에 의해 일시 중단 또는 종료 될 때까지 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1692">The async function body is then evaluated until it is either suspended (by reaching an await expression) or terminates, at which point control is returned to the caller, along with the return task.</span></span>

<span data-ttu-id="143b6-1693">비동기 함수 본문에는 다음이 종료 되 면 반환 작업 완료 되지 않은 상태로 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1693">When the body of the async function terminates, the return task is moved out of the incomplete state:</span></span>

*  <span data-ttu-id="143b6-1694">함수 본문 return 문이 또는 본문의 끝에 도달의 결과로 종료 되 면 결과 값은 성공된 상태에 배치 되는 작업의 반환에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1694">If the function body terminates as the result of reaching a return statement or the end of the body, any result value is recorded in the return task, which is put into a succeeded state.</span></span>
*  <span data-ttu-id="143b6-1695">함수 본문 예외로 인해 종료 되는 경우 ([throw 문](statements.md#the-throw-statement)) 예외는 faulted 상태로 전환 되는 task 반환에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1695">If the function body terminates as the result of an uncaught exception ([The throw statement](statements.md#the-throw-statement)) the exception is recorded in the return task which is put into a faulted state.</span></span>

### <a name="evaluation-of-a-void-returning-async-function"></a><span data-ttu-id="143b6-1696">Void 반환 비동기 함수 계산</span><span class="sxs-lookup"><span data-stu-id="143b6-1696">Evaluation of a void-returning async function</span></span>

<span data-ttu-id="143b6-1697">비동기 함수의 반환 형식이 `void`을 위에서 다음과 같이 달라 집니다 평가: 작업이 반환 되기 때문에 함수 완성 및 현재 스레드의 예외를 대신 통신 ***동기화 상황에 맞는***합니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1697">If the return type of the async function is `void`, evaluation differs from the above in the following way: Because no task is returned, the function instead communicates completion and exceptions to the current thread's ***synchronization context***.</span></span> <span data-ttu-id="143b6-1698">동기화 컨텍스트의 정확한 정의 구현에 종속 된 이지만 표현인 현재 스레드가 실행 되 고 "where"입니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1698">The exact definition of synchronization context is implementation-dependent, but is a representation of "where" the current thread is running.</span></span> <span data-ttu-id="143b6-1699">동기화 컨텍스트는 void 반환 비동기 함수 시작, 완료 되 면 또는 확인할 수 없는 예외를 throw 하는 경우에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="143b6-1699">The synchronization context is notified when evaluation of a void-returning async function commences, completes successfully, or causes an uncaught exception to be thrown.</span></span>

<span data-ttu-id="143b6-1700">이렇게 하면 얼마나 많은 void 반환 비동기 기능을 실행 하는 추적 하 고 발생 하는 예외를 전파 하는 방법을 결정 하는 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="143b6-1700">This allows the context to keep track of how many void-returning async functions are running under it, and to decide how to propagate exceptions coming out of them.</span></span>
