# <a name="basic-concepts"></a><span data-ttu-id="5eabc-101">기본 개념</span><span class="sxs-lookup"><span data-stu-id="5eabc-101">Basic concepts</span></span>

## <a name="application-startup"></a><span data-ttu-id="5eabc-102">응용 프로그램 시작</span><span class="sxs-lookup"><span data-stu-id="5eabc-102">Application Startup</span></span>

<span data-ttu-id="5eabc-103">가진 어셈블리에는 ***진입점*** 호출 되는 ***응용 프로그램***합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-103">An assembly that has an ***entry point*** is called an ***application***.</span></span> <span data-ttu-id="5eabc-104">응용 프로그램은 새를 실행 하는 경우 ***응용 프로그램 도메인*** 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-104">When an application is run, a new ***application domain*** is created.</span></span> <span data-ttu-id="5eabc-105">응용 프로그램의 여러 다른 인스턴스화를 동시에 동일한 컴퓨터에 있을 수 있고 각 고유한 응용 프로그램 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-105">Several different instantiations of an application may exist on the same machine at the same time, and each has its own application domain.</span></span>

<span data-ttu-id="5eabc-106">응용 프로그램 상태에 대 한 컨테이너 역할을 하 여 응용 프로그램 격리를 활성화 하는 응용 프로그램 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-106">An application domain enables application isolation by acting as a container for application state.</span></span> <span data-ttu-id="5eabc-107">응용 프로그램 도메인 컨테이너 및 응용 프로그램에서 사용 하는 클래스 라이브러리에 정의 된 형식에 대 한 경계 역할도 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-107">An application domain acts as a container and boundary for the types defined in the application and the class libraries it uses.</span></span> <span data-ttu-id="5eabc-108">형식을 로드 한 응용 프로그램 도메인에 형식이 같은 다른 응용 프로그램 도메인에 로드와 다릅니다. 및 개체의 인스턴스 직접 응용 프로그램 도메인 간에 공유 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-108">Types loaded into one application domain are distinct from the same type loaded into another application domain, and instances of objects are not directly shared between application domains.</span></span> <span data-ttu-id="5eabc-109">예를 들어, 각 응용 프로그램 도메인에 이러한 형식에 대 한 정적 변수의 자체 복사본이 및 유형에 대 한 정적 생성자 응용 프로그램 도메인당 한 번만 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-109">For instance, each application domain has its own copy of static variables for these types, and a static constructor for a type is run at most once per application domain.</span></span> <span data-ttu-id="5eabc-110">구현을 자유롭게 응용 프로그램 도메인의 생성과 대 한 구현 별 정책 또는 메커니즘을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-110">Implementations are free to provide implementation-specific policy or mechanisms for the creation and destruction of application domains.</span></span>

<span data-ttu-id="5eabc-111">***응용 프로그램 시작*** 실행 환경에서 응용 프로그램의 진입점으로 참조 되는 지정 된 메서드를 호출할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-111">***Application startup*** occurs when the execution environment calls a designated method, which is referred to as the application's entry point.</span></span> <span data-ttu-id="5eabc-112">이 진입점 메서드 이름은 항상 `Main`, 다음 서명 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-112">This entry point method is always named `Main`, and can have one of the following signatures:</span></span>

```csharp
static void Main() {...}

static void Main(string[] args) {...}

static int Main() {...}

static int Main(string[] args) {...}
```

<span data-ttu-id="5eabc-113">표시 된 대로 진입점 선택적으로 반환할 수 있습니다는 `int` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-113">As shown, the entry point may optionally return an `int` value.</span></span> <span data-ttu-id="5eabc-114">이 반환 값을 응용 프로그램 종료에서 사용 ([응용 프로그램 종료](basic-concepts.md#application-termination)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-114">This return value is used in application termination ([Application termination](basic-concepts.md#application-termination)).</span></span>

<span data-ttu-id="5eabc-115">진입점 필요에 따라 하나의 형식 매개 변수가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-115">The entry point may optionally have one formal parameter.</span></span> <span data-ttu-id="5eabc-116">매개 변수 이름을 지정할 수 있지만 매개 변수 형식의 해야 `string[]`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-116">The parameter may have any name, but the type of the parameter must be `string[]`.</span></span> <span data-ttu-id="5eabc-117">실행 환경을 만들고 전달 정식 매개 변수가 있는 경우는 `string[]` 인수는 명령줄 인수를 포함 하는 응용 프로그램이 시작 된 경우를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-117">If the formal parameter is present, the execution environment creates and passes a `string[]` argument containing the command-line arguments that were specified when the application was started.</span></span> <span data-ttu-id="5eabc-118">`string[]` 인수가 null 되지 않지만 명령줄 인수 없이 지정 된 경우 길이가 0 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-118">The `string[]` argument is never null, but it may have a length of zero if no command-line arguments were specified.</span></span>

<span data-ttu-id="5eabc-119">C#는 메서드 오버 로딩을 지원 하므로 클래스 또는 구조체를 포함할 수 있습니다 일부 메서드의 정의가 여러 개 제공 각 메서드의 서명이 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-119">Since C# supports method overloading, a class or struct may contain multiple definitions of some method, provided each has a different signature.</span></span> <span data-ttu-id="5eabc-120">그러나 하나의 프로그램 내에서 클래스 또는 구조체 없습니다 포함 될 수 있습니다 호출 하는 메서드가 둘 이상 `Main` 정의가 한정 응용 프로그램 진입점으로 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-120">However, within a single program, no class or struct may contain more than one method called `Main` whose definition qualifies it to be used as an application entry point.</span></span> <span data-ttu-id="5eabc-121">하지만 다른 오버 로드 된 버전의 `Main` 는 허용 둘 이상의 매개 변수를 나가 유일한 매개 변수는 형식이 아닌 제공 `string[]`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-121">Other overloaded versions of `Main` are permitted, however, provided they have more than one parameter, or their only parameter is other than type `string[]`.</span></span>

<span data-ttu-id="5eabc-122">응용 프로그램의 여러 클래스 또는 구조체 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-122">An application can be made up of multiple classes or structs.</span></span> <span data-ttu-id="5eabc-123">라는 메서드를 포함 하도록 이러한 클래스나 구조체의 두 개 이상의 가능성이 `Main` 정의가 한정 응용 프로그램 진입점으로 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-123">It is possible for more than one of these classes or structs to contain a method called `Main` whose definition qualifies it to be used as an application entry point.</span></span> <span data-ttu-id="5eabc-124">이러한 경우에 외부 메커니즘 (예: 명령줄 컴파일러 옵션) 다음 중 하나를 선택 하려면 사용 해야 `Main` 진입점 메서드.</span><span class="sxs-lookup"><span data-stu-id="5eabc-124">In such cases, an external mechanism (such as a command-line compiler option) must be used to select one of these `Main` methods as the entry point.</span></span>

<span data-ttu-id="5eabc-125">C#에서 모든 메서드는 클래스 또는 구조체의 멤버로 정의 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-125">In C#, every method must be defined as a member of a class or struct.</span></span> <span data-ttu-id="5eabc-126">일반적으로 선언 된 접근성 ([접근성을 선언](basic-concepts.md#declared-accessibility)) 메서드의 액세스 한정자에 의해 결정 됩니다 ([액세스 한정자](classes.md#access-modifiers))에 선언과 마찬가지로 선언 된 지정 형식의 액세스 가능성은 해당 선언에 지정 된 액세스 한정자에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-126">Ordinarily, the declared accessibility ([Declared accessibility](basic-concepts.md#declared-accessibility)) of a method is determined by the access modifiers ([Access modifiers](classes.md#access-modifiers)) specified in its declaration, and similarly the declared accessibility of a type is determined by the access modifiers specified in its declaration.</span></span> <span data-ttu-id="5eabc-127">순서로 지정 된 형식의 지정 된 메서드를 호출할 수, 형식 및 멤버를 모두 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-127">In order for a given method of a given type to be callable, both the type and the member must be accessible.</span></span> <span data-ttu-id="5eabc-128">그러나 응용 프로그램 진입점이 특별 한 경우.</span><span class="sxs-lookup"><span data-stu-id="5eabc-128">However, the application entry point is a special case.</span></span> <span data-ttu-id="5eabc-129">특히, 실행 환경에는 해당 선언 된 접근성에 관계 없이 및 해당 바깥쪽 형식 선언에 선언 된 접근성에 관계 없이 응용 프로그램의 진입점을 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-129">Specifically, the execution environment can access the application's entry point regardless of its declared accessibility and regardless of the declared accessibility of its enclosing type declarations.</span></span>

<span data-ttu-id="5eabc-130">응용 프로그램 진입점 메서드는 제네릭 클래스 선언에서 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-130">The application entry point method may not be in a generic class declaration.</span></span>

<span data-ttu-id="5eabc-131">다른 모든 측면에서 진입점 메서드의 진입점이 아닌 것 처럼 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-131">In all other respects, entry point methods behave like those that are not entry points.</span></span>

## <a name="application-termination"></a><span data-ttu-id="5eabc-132">응용 프로그램 종료</span><span class="sxs-lookup"><span data-stu-id="5eabc-132">Application termination</span></span>

<span data-ttu-id="5eabc-133">***응용 프로그램 종료*** 실행 환경에 컨트롤을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-133">***Application termination*** returns control to the execution environment.</span></span>

<span data-ttu-id="5eabc-134">응용 프로그램의 반환 형식이 ***진입점*** 메서드는 `int`, 반환 되는 값은 응용 프로그램의 역할도 ***종료 상태 코드***합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-134">If the return type of the application's ***entry point*** method is `int`, the value returned serves as the application's ***termination status code***.</span></span> <span data-ttu-id="5eabc-135">이 코드의 목적은 성공 또는 실패를 실행 환경으로의 통신을 허용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-135">The purpose of this code is to allow communication of success or failure to the execution environment.</span></span>

<span data-ttu-id="5eabc-136">진입점 메서드 반환 형식의 경우 `void`, 오른쪽 중괄호에 도달 (`}`)를 종료 하는 메서드 또는 실행을 `return` 종료 상태 코드에 없는 식이 포함 된 문의 결과 `0`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-136">If the return type of the entry point method is `void`, reaching the right brace (`}`) which terminates that method, or executing a `return` statement that has no expression, results in a termination status code of `0`.</span></span>

<span data-ttu-id="5eabc-137">응용 프로그램의 종료 하기 전에 모든 아직 가비지 수집 되지 않은 개체에 대 한 소멸자는 호출 이러한 정리 억제 하지 않는 한 (라이브러리 메서드를 호출 하 여 `GC.SuppressFinalize`예를 들어).</span><span class="sxs-lookup"><span data-stu-id="5eabc-137">Prior to an application's termination, destructors for all of its objects that have not yet been garbage collected are called, unless such cleanup has been suppressed (by a call to the library method `GC.SuppressFinalize`, for example).</span></span>

## <a name="declarations"></a><span data-ttu-id="5eabc-138">선언</span><span class="sxs-lookup"><span data-stu-id="5eabc-138">Declarations</span></span>

<span data-ttu-id="5eabc-139">프로그램의 구성 요소를 정의 하는 C# 프로그램의 선언입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-139">Declarations in a C# program define the constituent elements of the program.</span></span> <span data-ttu-id="5eabc-140">C# 프로그램이 구성 되는 네임 스페이스를 사용 하 여 ([네임 스페이스](namespaces.md)), 형식을 포함할 수 있는 선언 및 중첩 된 네임 스페이스 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-140">C# programs are organized using namespaces ([Namespaces](namespaces.md)), which can contain type declarations and nested namespace declarations.</span></span> <span data-ttu-id="5eabc-141">형식 선언 ([형식 선언을](namespaces.md#type-declarations)) 클래스를 정의 하는 데 사용 됩니다 ([클래스](classes.md)), 구조체 ([구조체](structs.md)), 인터페이스 ([인터페이스](interfaces.md) )를 열거형 ([열거형](enums.md)), 및 대리자 ([대리자](delegates.md)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-141">Type declarations ([Type declarations](namespaces.md#type-declarations)) are used to define classes ([Classes](classes.md)), structs ([Structs](structs.md)), interfaces ([Interfaces](interfaces.md)), enums ([Enums](enums.md)), and delegates ([Delegates](delegates.md)).</span></span> <span data-ttu-id="5eabc-142">형식 선언의 형식에서 형식 선언에 허용 되는 멤버의 종류에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-142">The kinds of members permitted in a type declaration depend on the form of the type declaration.</span></span> <span data-ttu-id="5eabc-143">예를 들어, 클래스 선언 상수에 대 한 선언을 포함할 수 있습니다 ([상수](classes.md#constants)), 필드 ([필드](classes.md#fields)), 메서드 ([메서드](classes.md#methods)), 속성 ([ 속성](classes.md#properties)), 이벤트 ([이벤트](classes.md#events)), 인덱서 ([인덱서](classes.md#indexers)), 연산자 ([연산자](classes.md#operators)), 인스턴스 생성자 ([ 인스턴스 생성자](classes.md#instance-constructors)), 정적 생성자 ([정적 생성자](classes.md#static-constructors)), 소멸자 ([소멸자](classes.md#destructors)), 중첩 형식 및 ([중첩 형식은](classes.md#nested-types)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-143">For instance, class declarations can contain declarations for constants ([Constants](classes.md#constants)), fields ([Fields](classes.md#fields)), methods ([Methods](classes.md#methods)), properties ([Properties](classes.md#properties)), events ([Events](classes.md#events)), indexers ([Indexers](classes.md#indexers)), operators ([Operators](classes.md#operators)), instance constructors ([Instance constructors](classes.md#instance-constructors)), static constructors ([Static constructors](classes.md#static-constructors)), destructors ([Destructors](classes.md#destructors)), and nested types ([Nested types](classes.md#nested-types)).</span></span>

<span data-ttu-id="5eabc-144">선언에서 이름을 정의 합니다 ***선언 공간*** 선언 속한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-144">A declaration defines a name in the ***declaration space*** to which the declaration belongs.</span></span> <span data-ttu-id="5eabc-145">제외 하 고 멤버를 오버 로드 된 ([시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading)), 선언 공간에서 동일한 이름 가진 멤버를 정의 하는 두 개 이상의 선언이 있어야 하면 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-145">Except for overloaded members ([Signatures and overloading](basic-concepts.md#signatures-and-overloading)), it is a compile-time error to have two or more declarations that introduce members with the same name in a declaration space.</span></span> <span data-ttu-id="5eabc-146">다양 한 같은 이름 가진 멤버를 포함 하도록 선언 공간에는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-146">It is never possible for a declaration space to contain different kinds of members with the same name.</span></span> <span data-ttu-id="5eabc-147">예를 들어 선언 공간을 포함할 수 있습니다 하지 메서드와 필드를 같은 이름으로.</span><span class="sxs-lookup"><span data-stu-id="5eabc-147">For example, a declaration space can never contain a field and a method by the same name.</span></span>

<span data-ttu-id="5eabc-148">다음에 설명 된 대로 여러 가지 선언 공백이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-148">There are several different types of declaration spaces, as described in the following.</span></span>

*  <span data-ttu-id="5eabc-149">프로그램의 모든 소스 파일 내의 *namespace_member_declaration*없습니다 바깥쪽 s *namespace_declaration* 이라는 단일 결합 된 선언 공간의 멤버인는 ***전역 선언 공간***입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-149">Within all source files of a program, *namespace_member_declaration*s with no enclosing *namespace_declaration* are members of a single combined declaration space called the ***global declaration space***.</span></span>
*  <span data-ttu-id="5eabc-150">프로그램의 모든 소스 파일 내의 *namespace_member_declaration*내 *namespace_declaration*정규화 된 네임 스페이스 이름이 포함 된 단일 결합 된 선언의 멤버인 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-150">Within all source files of a program, *namespace_member_declaration*s within *namespace_declaration*s that have the same fully qualified namespace name are members of a single combined declaration space.</span></span>
*  <span data-ttu-id="5eabc-151">각 클래스, 구조체 또는 인터페이스 선언에는 새 선언 공간을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-151">Each class, struct, or interface declaration creates a new declaration space.</span></span> <span data-ttu-id="5eabc-152">이름을 통해이 선언 공간에 도입 된 *class_member_declaration*개이면 *struct_member_declaration*개이면 *interface_member_declaration*s, 또는 *type_parameter*s입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-152">Names are introduced into this declaration space through *class_member_declaration*s, *struct_member_declaration*s, *interface_member_declaration*s, or *type_parameter*s.</span></span> <span data-ttu-id="5eabc-153">오버 로드 된 인스턴스 생성자를 제외 하 고 선언 및 정적 생성자 선언, 클래스 또는 구조체는 클래스 또는 구조체와 같은 이름 사용 하는 멤버 선언이 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-153">Except for overloaded instance constructor declarations and static constructor declarations, a class or struct cannot contain a member declaration with the same name as the class or struct.</span></span> <span data-ttu-id="5eabc-154">클래스, 구조체 또는 인터페이스의 오버 로드 된 메서드 및 인덱서 선언이 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-154">A class, struct, or interface permits the declaration of overloaded methods and indexers.</span></span> <span data-ttu-id="5eabc-155">또한 클래스 또는 구조체 선언의 인스턴스 오버 로드 된 생성자 및 연산자를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-155">Furthermore, a class or struct permits the declaration of overloaded instance constructors and operators.</span></span> <span data-ttu-id="5eabc-156">예를 들어, 클래스, 구조체 또는 인터페이스 선언을 포함할 수 있습니다 여러 메서드는 동일한 이름 가진 이러한 메서드 선언은 해당 서명을 다른 제공 ([시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-156">For example, a class, struct, or interface may contain multiple method declarations with the same name, provided these method declarations differ in their signature ([Signatures and overloading](basic-concepts.md#signatures-and-overloading)).</span></span> <span data-ttu-id="5eabc-157">기본 클래스는 클래스의 선언 공간에 영향을 주지를 기본 인터페이스는 인터페이스 선언 공간에 영향을 주지 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-157">Note that base classes do not contribute to the declaration space of a class, and base interfaces do not contribute to the declaration space of an interface.</span></span> <span data-ttu-id="5eabc-158">따라서 파생된 클래스 또는 인터페이스를 상속된 된 멤버와 동일한 이름 가진 멤버를 선언할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-158">Thus, a derived class or interface is allowed to declare a member with the same name as an inherited member.</span></span> <span data-ttu-id="5eabc-159">이러한 멤버 라고 ***숨기기*** 상속 된 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-159">Such a member is said to ***hide*** the inherited member.</span></span>
*  <span data-ttu-id="5eabc-160">각 대리자 선언을 새 선언 공간을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-160">Each delegate declaration creates a new declaration space.</span></span> <span data-ttu-id="5eabc-161">정식 매개 변수를 통해이 선언 공간에 도입 된 이름 (*fixed_parameter*s 및 *parameter_array*s) 및 *type_parameter*s입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-161">Names are introduced into this declaration space through formal parameters (*fixed_parameter*s and *parameter_array*s) and *type_parameter*s.</span></span>
*  <span data-ttu-id="5eabc-162">각 열거형 선언은 새 선언 공간을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-162">Each enumeration declaration creates a new declaration space.</span></span> <span data-ttu-id="5eabc-163">이름을 통해이 선언 공간에 도입 된 *enum_member_declarations*합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-163">Names are introduced into this declaration space through *enum_member_declarations*.</span></span>
*  <span data-ttu-id="5eabc-164">각 메서드 선언, 인덱서, 연산자 선언, 인스턴스 생성자 선언 선언과 익명 함수 라는 새 선언 공간을 만듭니다는 ***지역 변수 선언 공간***입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-164">Each method declaration, indexer declaration, operator declaration, instance constructor declaration and anonymous function creates a new declaration space called a ***local variable declaration space***.</span></span> <span data-ttu-id="5eabc-165">정식 매개 변수를 통해이 선언 공간에 도입 된 이름 (*fixed_parameter*s 및 *parameter_array*s) 및 *type_parameter*s입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-165">Names are introduced into this declaration space through formal parameters (*fixed_parameter*s and *parameter_array*s) and *type_parameter*s.</span></span> <span data-ttu-id="5eabc-166">함수 멤버 또는 익명 함수 본문에 있는 경우 지역 변수 선언 공간 내에 중첩 될으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-166">The body of the function member or anonymous function, if any, is considered to be nested within the local variable declaration space.</span></span> <span data-ttu-id="5eabc-167">이 지역 변수 선언 공간 및 동일한 이름 가진 요소를 포함 하는 중첩 된 지역 변수 선언 공간에 대 한 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-167">It is an error for a local variable declaration space and a nested local variable declaration space to contain elements with the same name.</span></span> <span data-ttu-id="5eabc-168">따라서 중첩 된 선언 공간 내에서 수 없는 바깥쪽 선언 공간에서 로컬 변수 또는 지역 변수와 동일한 이름을 가진 상수 또는 상수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-168">Thus, within a nested declaration space it is not possible to declare a local variable or constant with the same name as a local variable or constant in an enclosing declaration space.</span></span> <span data-ttu-id="5eabc-169">두 선언 공간을 모두 선언 공간 다른 값을 포함으로 동일한 이름 가진 요소를 포함 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-169">It is possible for two declaration spaces to contain elements with the same name as long as neither declaration space contains the other.</span></span>
*  <span data-ttu-id="5eabc-170">각 *블록* 또는 *switch_block* , 뿐만 *에 대 한*를 *foreach* 하 고 *사용 하 여* 문을 만듭니다는 지역 변수 및 지역 상수에 대 한 지역 변수 선언 공간입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-170">Each *block* or *switch_block* , as well as a *for*, *foreach* and *using* statement, creates a local variable declaration space for local variables and local constants .</span></span> <span data-ttu-id="5eabc-171">이름을 통해이 선언 공간에 도입 된 *local_variable_declaration*s 및 *local_constant_declaration*s입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-171">Names are introduced into this declaration space through *local_variable_declaration*s and *local_constant_declaration*s.</span></span> <span data-ttu-id="5eabc-172">블록 또는 함수 멤버 또는 익명 함수 본문 내에서 발생 하는 해당 매개 변수에 대 한 함수로 선언 된 지역 변수 선언 공간 내에서 중첩 되는 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-172">Note that blocks that occur as or within the body of a function member or anonymous function are nested within the local variable declaration space declared by those functions for their parameters.</span></span> <span data-ttu-id="5eabc-173">즉 로컬 변수와 이름이 같은 매개 변수를 사용 하 여 메서드가 있으면 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-173">Thus it is an error to have e.g. a method with a local variable and a parameter of the same name.</span></span>
*  <span data-ttu-id="5eabc-174">각 *블록* 하거나 *switch_block* 레이블에 대 한 별도 선언 공간을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-174">Each *block* or *switch_block* creates a separate declaration space for labels.</span></span> <span data-ttu-id="5eabc-175">이름을 통해이 선언 공간에 도입 된 *labeled_statement*및 이름을 통해 참조 되 *goto_statement*s입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-175">Names are introduced into this declaration space through *labeled_statement*s, and the names are referenced through *goto_statement*s.</span></span> <span data-ttu-id="5eabc-176">합니다 ***선언 공간 레이블을*** 블록의 모든 중첩 된 블록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-176">The ***label declaration space*** of a block includes any nested blocks.</span></span> <span data-ttu-id="5eabc-177">따라서 중첩된 된 블록 내에서 수 없는 바깥쪽 블록의 레이블로 동일한 이름 사용 하 여 레이블을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-177">Thus, within a nested block it is not possible to declare a label with the same name as a label in an enclosing block.</span></span>

<span data-ttu-id="5eabc-178">이름이 선언 되는 텍스트 순서는 일반적으로 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-178">The textual order in which names are declared is generally of no significance.</span></span> <span data-ttu-id="5eabc-179">특히 텍스트 순서 선언 및 네임 스페이스, 상수, 메서드, 속성, 이벤트, 인덱서, 연산자, 인스턴스 생성자, 소멸자, 정적 생성자 및 형식 사용에 대 한 중요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-179">In particular, textual order is not significant for the declaration and use of namespaces, constants, methods, properties, events, indexers, operators, instance constructors, destructors, static constructors, and types.</span></span> <span data-ttu-id="5eabc-180">선언 순서는 다음과 같은 방법에서 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-180">Declaration order is significant in the following ways:</span></span>

*  <span data-ttu-id="5eabc-181">필드 선언 및 지역 변수 선언에 대 한 선언 순서 대로 (있는 경우) 해당 이니셜라이저가 실행 되는 순서를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-181">Declaration order for field declarations and local variable declarations determines the order in which their initializers (if any) are executed.</span></span>
*  <span data-ttu-id="5eabc-182">지역 변수는 사용 하기 전에 정의 되어야 합니다 ([범위](basic-concepts.md#scopes)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-182">Local variables must be defined before they are used ([Scopes](basic-concepts.md#scopes)).</span></span>
*  <span data-ttu-id="5eabc-183">열거형 멤버 선언에 대 한 선언 순서 대로 ([열거형 멤버](enums.md#enum-members)) 때 상당한 *constant_expression* 값이 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-183">Declaration order for enum member declarations ([Enum members](enums.md#enum-members)) is significant when *constant_expression* values are omitted.</span></span>

<span data-ttu-id="5eabc-184">네임 스페이스의 선언 공간 "종료"를 열고 두 네임 스페이스 정규화 된 이름이 같은 선언이 동일한 선언 공간 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-184">The declaration space of a namespace is "open ended", and two namespace declarations with the same fully qualified name contribute to the same declaration space.</span></span> <span data-ttu-id="5eabc-185">예</span><span class="sxs-lookup"><span data-stu-id="5eabc-185">For example</span></span>
```csharp
namespace Megacorp.Data
{
    class Customer
    {
        ...
    }
}

namespace Megacorp.Data
{
    class Order
    {
        ...
    }
}
```

<span data-ttu-id="5eabc-186">이 경우 정규화 된 이름 사용 하 여 두 개의 클래스를 선언으로 동일한 선언 공간에 영향을 위의 두 가지 네임 스페이스 선언 `Megacorp.Data.Customer` 고 `Megacorp.Data.Order`입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-186">The two namespace declarations above contribute to the same declaration space, in this case declaring two classes with the fully qualified names `Megacorp.Data.Customer` and `Megacorp.Data.Order`.</span></span> <span data-ttu-id="5eabc-187">두 선언이 동일한 선언 공간, 때문에 발생할 수 컴파일 타임 오류를 각각 동일한 이름 가진 클래스의 선언을 포함 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="5eabc-187">Because the two declarations contribute to the same declaration space, it would have caused a compile-time error if each contained a declaration of a class with the same name.</span></span>

<span data-ttu-id="5eabc-188">위에 지정 된 대로 선언 공간 블록의 모든 중첩 된 블록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-188">As specified above, the declaration space of a block includes any nested blocks.</span></span> <span data-ttu-id="5eabc-189">따라서 다음 예제에에서는 `F` 및 `G` 때문에 컴파일 타임 오류가 발생 되는 메서드 이름을 `i` 바깥쪽 블록에서 선언 되 고 내부 블록에 다시 선언할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-189">Thus, in the following example, the `F` and `G` methods result in a compile-time error because the name `i` is declared in the outer block and cannot be redeclared in the inner block.</span></span> <span data-ttu-id="5eabc-190">그러나를 `H` 하 고 `I` 이후 두 메서드는 유효한 `i`의 별도 중첩 되지 않은 블록에서 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-190">However, the `H` and `I` methods are valid since the two `i`'s are declared in separate non-nested blocks.</span></span>

```csharp
class A
{
    void F() {
        int i = 0;
        if (true) {
            int i = 1;            
        }
    }

    void G() {
        if (true) {
            int i = 0;
        }
        int i = 1;                
    }

    void H() {
        if (true) {
            int i = 0;
        }
        if (true) {
            int i = 1;
        }
    }

    void I() {
        for (int i = 0; i < 10; i++)
            H();
        for (int i = 0; i < 10; i++)
            H();
    }
}
```

## <a name="members"></a><span data-ttu-id="5eabc-191">멤버</span><span class="sxs-lookup"><span data-stu-id="5eabc-191">Members</span></span>

<span data-ttu-id="5eabc-192">네임 스페이스 및 형식에는 ***멤버***합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-192">Namespaces and types have ***members***.</span></span> <span data-ttu-id="5eabc-193">엔터티의 멤버 뒤에 엔터티에 대 한 참조를 사용 하 여 시작 하는 정규화 된 이름을 사용 하 여 일반 공급 되는 "`.`" 토큰, 멤버의 이름 뒤에.</span><span class="sxs-lookup"><span data-stu-id="5eabc-193">The members of an entity are generally available through the use of a qualified name that starts with a reference to the entity, followed by a "`.`" token, followed by the name of the member.</span></span>

<span data-ttu-id="5eabc-194">형식의 멤버는 형식 선언에서 선언 하거나 또는 ***상속*** 형식의 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-194">Members of a type are either declared in the type declaration or ***inherited*** from the base class of the type.</span></span> <span data-ttu-id="5eabc-195">기본 클래스에서 상속 되는 형식, 파생 된 형식의 멤버로 인스턴스 생성자, 소멸자 및 정적 생성자를 제외 하 고 기본 클래스의 모든 멤버에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-195">When a type inherits from a base class, all members of the base class, except instance constructors, destructors and static constructors, become members of the derived type.</span></span> <span data-ttu-id="5eabc-196">기본 클래스 멤버의 선언 된 접근성이 멤버의 상속 여부를 제어 하지는 않습니다-상속 인스턴스 생성자, 정적 생성자 또는 소멸자가 없는 멤버를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-196">The declared accessibility of a base class member does not control whether the member is inherited—inheritance extends to any member that isn't an instance constructor, static constructor, or destructor.</span></span> <span data-ttu-id="5eabc-197">그러나 상속된 된 멤버를 해당 선언 된 접근성 때문 하거나 파생된 형식에서 액세스할 수 없습니다 ([접근성을 선언](basic-concepts.md#declared-accessibility)) 또는 형식 자체에서 선언에 의해 숨겨져 있기 때문에 ([통해 숨기기 상속](basic-concepts.md#hiding-through-inheritance)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-197">However, an inherited member may not be accessible in a derived type, either because of its declared accessibility ([Declared accessibility](basic-concepts.md#declared-accessibility)) or because it is hidden by a declaration in the type itself ([Hiding through inheritance](basic-concepts.md#hiding-through-inheritance)).</span></span>

### <a name="namespace-members"></a><span data-ttu-id="5eabc-198">Namespace 멤버</span><span class="sxs-lookup"><span data-stu-id="5eabc-198">Namespace members</span></span>

<span data-ttu-id="5eabc-199">네임 스페이스 및 형식 바깥쪽 네임 스페이스에는의 멤버는 ***전역 네임 스페이스***합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-199">Namespaces and types that have no enclosing namespace are members of the ***global namespace***.</span></span> <span data-ttu-id="5eabc-200">이 전역 선언 공간에 선언 된 이름에 직접 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-200">This corresponds directly to the names declared in the global declaration space.</span></span>

<span data-ttu-id="5eabc-201">네임 스페이스 및 네임 스페이스 내에 선언 된 유형에 해당 네임 스페이스의 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-201">Namespaces and types declared within a namespace are members of that namespace.</span></span> <span data-ttu-id="5eabc-202">이 네임 스페이스의 선언 공간에 선언 된 이름에 직접 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-202">This corresponds directly to the names declared in the declaration space of the namespace.</span></span>

<span data-ttu-id="5eabc-203">네임스페이스에는 액세스 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-203">Namespaces have no access restrictions.</span></span> <span data-ttu-id="5eabc-204">Private, protected 또는 internal 네임 스페이스를 선언 하는 것이 불가능 하 고 네임 스페이스 이름은 항상 공개적으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-204">It is not possible to declare private, protected, or internal namespaces, and namespace names are always publicly accessible.</span></span>

### <a name="struct-members"></a><span data-ttu-id="5eabc-205">구조체 멤버</span><span class="sxs-lookup"><span data-stu-id="5eabc-205">Struct members</span></span>

<span data-ttu-id="5eabc-206">구조체의 멤버는 구조체에서 선언 된 멤버와 구조체의 직접 기본 클래스에서 상속 된 멤버 `System.ValueType` 간접 기본 클래스 및 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-206">The members of a struct are the members declared in the struct and the members inherited from the struct's direct base class `System.ValueType` and the indirect base class `object`.</span></span>

<span data-ttu-id="5eabc-207">단순 형식의 멤버 단순 유형에 따라 구조체 형식 별칭의 멤버에 직접 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-207">The members of a simple type correspond directly to the members of the struct type aliased by the simple type:</span></span>

*  <span data-ttu-id="5eabc-208">멤버 `sbyte` 의 멤버는 `System.SByte` 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-208">The members of `sbyte` are the members of the `System.SByte` struct.</span></span>
*  <span data-ttu-id="5eabc-209">멤버 `byte` 의 멤버는 `System.Byte` 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-209">The members of `byte` are the members of the `System.Byte` struct.</span></span>
*  <span data-ttu-id="5eabc-210">멤버 `short` 의 멤버는 `System.Int16` 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-210">The members of `short` are the members of the `System.Int16` struct.</span></span>
*  <span data-ttu-id="5eabc-211">멤버 `ushort` 의 멤버는 `System.UInt16` 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-211">The members of `ushort` are the members of the `System.UInt16` struct.</span></span>
*  <span data-ttu-id="5eabc-212">멤버 `int` 의 멤버는 `System.Int32` 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-212">The members of `int` are the members of the `System.Int32` struct.</span></span>
*  <span data-ttu-id="5eabc-213">멤버 `uint` 의 멤버는 `System.UInt32` 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-213">The members of `uint` are the members of the `System.UInt32` struct.</span></span>
*  <span data-ttu-id="5eabc-214">멤버 `long` 의 멤버는 `System.Int64` 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-214">The members of `long` are the members of the `System.Int64` struct.</span></span>
*  <span data-ttu-id="5eabc-215">멤버 `ulong` 의 멤버는 `System.UInt64` 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-215">The members of `ulong` are the members of the `System.UInt64` struct.</span></span>
*  <span data-ttu-id="5eabc-216">멤버 `char` 의 멤버는 `System.Char` 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-216">The members of `char` are the members of the `System.Char` struct.</span></span>
*  <span data-ttu-id="5eabc-217">멤버 `float` 의 멤버는 `System.Single` 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-217">The members of `float` are the members of the `System.Single` struct.</span></span>
*  <span data-ttu-id="5eabc-218">멤버 `double` 의 멤버는 `System.Double` 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-218">The members of `double` are the members of the `System.Double` struct.</span></span>
*  <span data-ttu-id="5eabc-219">멤버 `decimal` 의 멤버는 `System.Decimal` 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-219">The members of `decimal` are the members of the `System.Decimal` struct.</span></span>
*  <span data-ttu-id="5eabc-220">멤버 `bool` 의 멤버는 `System.Boolean` 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-220">The members of `bool` are the members of the `System.Boolean` struct.</span></span>

### <a name="enumeration-members"></a><span data-ttu-id="5eabc-221">열거형 멤버</span><span class="sxs-lookup"><span data-stu-id="5eabc-221">Enumeration members</span></span>

<span data-ttu-id="5eabc-222">열거형의 멤버는 열거형의 선언 된 상수 및 열거형의 직접 기본 클래스에서 상속 된 멤버 `System.Enum` 및 간접 기본 클래스 `System.ValueType` 고 `object`입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-222">The members of an enumeration are the constants declared in the enumeration and the members inherited from the enumeration's direct base class `System.Enum` and the indirect base classes `System.ValueType` and `object`.</span></span>

### <a name="class-members"></a><span data-ttu-id="5eabc-223">클래스 멤버</span><span class="sxs-lookup"><span data-stu-id="5eabc-223">Class members</span></span>

<span data-ttu-id="5eabc-224">클래스의 멤버는 클래스에서 선언 된 멤버 및 기본 클래스에서 상속 된 멤버 (클래스를 제외 하 고 `object` 있는 기본 클래스 없음).</span><span class="sxs-lookup"><span data-stu-id="5eabc-224">The members of a class are the members declared in the class and the members inherited from the base class (except for class `object` which has no base class).</span></span> <span data-ttu-id="5eabc-225">기본 클래스에서 상속 된 멤버는 상수, 필드, 메서드, 속성, 이벤트, 인덱서, 연산자 및 유형의 기본 클래스인 하지만 하지는 인스턴스 생성자, 소멸자 및 기본 클래스의 정적 생성자를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-225">The members inherited from the base class include the constants, fields, methods, properties, events, indexers, operators, and types of the base class, but not the instance constructors, destructors and static constructors of the base class.</span></span> <span data-ttu-id="5eabc-226">기본 클래스 멤버의 액세스 가능성에 관계 없이 상속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-226">Base class members are inherited without regard to their accessibility.</span></span>

<span data-ttu-id="5eabc-227">클래스 선언에는 상수, 필드, 메서드, 속성, 이벤트, 인덱서, 연산자, 인스턴스 생성자, 소멸자, 정적 생성자 및 형식 선언을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-227">A class declaration may contain declarations of constants, fields, methods, properties, events, indexers, operators, instance constructors, destructors, static constructors and types.</span></span>

<span data-ttu-id="5eabc-228">멤버 `object` 고 `string` 해당 클래스 형식의 멤버에 직접 해당 별칭:</span><span class="sxs-lookup"><span data-stu-id="5eabc-228">The members of `object` and `string` correspond directly to the members of the class types they alias:</span></span>

*  <span data-ttu-id="5eabc-229">멤버 `object` 의 멤버는 `System.Object` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-229">The members of `object` are the members of the `System.Object` class.</span></span>
*  <span data-ttu-id="5eabc-230">멤버 `string` 의 멤버는 `System.String` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-230">The members of `string` are the members of the `System.String` class.</span></span>

### <a name="interface-members"></a><span data-ttu-id="5eabc-231">인터페이스 멤버</span><span class="sxs-lookup"><span data-stu-id="5eabc-231">Interface members</span></span>

<span data-ttu-id="5eabc-232">인터페이스의 멤버는 인터페이스의 모든 기본 인터페이스 및 인터페이스에서 선언 된 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-232">The members of an interface are the members declared in the interface and in all base interfaces of the interface.</span></span> <span data-ttu-id="5eabc-233">클래스 멤버 `object` 엄격 하 게 말하자면 모든 인터페이스의 멤버를 하지 않습니다 ([인터페이스 멤버](interfaces.md#interface-members)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-233">The members in class `object` are not, strictly speaking, members of any interface ([Interface members](interfaces.md#interface-members)).</span></span> <span data-ttu-id="5eabc-234">그러나 클래스 멤버 `object` 임의의 인터페이스 형식에서 멤버 조회를 통해 사용할 수 있습니다 ([멤버 조회](expressions.md#member-lookup)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-234">However, the members in class `object` are available via member lookup in any interface type ([Member lookup](expressions.md#member-lookup)).</span></span>

### <a name="array-members"></a><span data-ttu-id="5eabc-235">배열 멤버</span><span class="sxs-lookup"><span data-stu-id="5eabc-235">Array members</span></span>

<span data-ttu-id="5eabc-236">배열 멤버는 클래스에서 상속 된 멤버 `System.Array`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-236">The members of an array are the members inherited from class `System.Array`.</span></span>

### <a name="delegate-members"></a><span data-ttu-id="5eabc-237">대리자 멤버</span><span class="sxs-lookup"><span data-stu-id="5eabc-237">Delegate members</span></span>

<span data-ttu-id="5eabc-238">대리자는 클래스에서 상속 된 멤버 `System.Delegate`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-238">The members of a delegate are the members inherited from class `System.Delegate`.</span></span>

## <a name="member-access"></a><span data-ttu-id="5eabc-239">멤버 액세스</span><span class="sxs-lookup"><span data-stu-id="5eabc-239">Member access</span></span>

<span data-ttu-id="5eabc-240">멤버 액세스 제어를 허용 하는 멤버를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-240">Declarations of members allow control over member access.</span></span> <span data-ttu-id="5eabc-241">멤버의 액세스 가능성 선언 된 액세스 가능성에 의해 설정 됩니다 ([접근성을 선언](basic-concepts.md#declared-accessibility)) 멤버의 결합 된 위 형식의 액세스 가능성을 가진 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-241">The accessibility of a member is established by the declared accessibility ([Declared accessibility](basic-concepts.md#declared-accessibility)) of the member combined with the accessibility of the immediately containing type, if any.</span></span>

<span data-ttu-id="5eabc-242">특정 멤버에 대 한 액세스 허용 되 면 멤버 라고 ***액세스할 수 있는***합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-242">When access to a particular member is allowed, the member is said to be ***accessible***.</span></span> <span data-ttu-id="5eabc-243">반대로, 특정 멤버에 대 한 액세스 허용 되지 않는 경우 멤버 라고 ***액세스할 수 없는***합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-243">Conversely, when access to a particular member is disallowed, the member is said to be ***inaccessible***.</span></span> <span data-ttu-id="5eabc-244">텍스트 위치는 액세스가 이루어지는 액세스 가능 도메인에 포함 되 면 멤버에 대 한 액세스가 허용 됩니다 ([접근성 도메인](basic-concepts.md#accessibility-domains)) 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-244">Access to a member is permitted when the textual location in which the access takes place is included in the accessibility domain ([Accessibility domains](basic-concepts.md#accessibility-domains)) of the member.</span></span>

### <a name="declared-accessibility"></a><span data-ttu-id="5eabc-245">선언된 액세스 가능성</span><span class="sxs-lookup"><span data-stu-id="5eabc-245">Declared accessibility</span></span>

<span data-ttu-id="5eabc-246">합니다 ***접근성을 선언*** 의 구성원은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-246">The ***declared accessibility*** of a member can be one of the following:</span></span>

*  <span data-ttu-id="5eabc-247">가 포함 하 여 선택 하는 공용을 `public` 멤버 선언에서 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-247">Public, which is selected by including a `public` modifier in the member declaration.</span></span> <span data-ttu-id="5eabc-248">직관적인 의미 `public` "액세스가 제한 되지 않음" 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-248">The intuitive meaning of `public` is "access not limited".</span></span>
*  <span data-ttu-id="5eabc-249">포함 하 여 선택 되어 보호는 `protected` 멤버 선언에서 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-249">Protected, which is selected by including a `protected` modifier in the member declaration.</span></span> <span data-ttu-id="5eabc-250">직관적인 의미 `protected` "포함 하는 클래스 또는 형식에 대해서만 액세스 클래스에서 파생 되는 포함 하 는".</span><span class="sxs-lookup"><span data-stu-id="5eabc-250">The intuitive meaning of `protected` is "access limited to the containing class or types derived from the containing class".</span></span>
*  <span data-ttu-id="5eabc-251">가 포함 하 여 선택 하는 내부는 `internal` 멤버 선언에서 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-251">Internal, which is selected by including an `internal` modifier in the member declaration.</span></span> <span data-ttu-id="5eabc-252">직관적인 의미 `internal` "이이 프로그램에 대해서만 액세스"가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-252">The intuitive meaning of `internal` is "access limited to this program".</span></span>
*  <span data-ttu-id="5eabc-253">내부 (즉 protected 또는 internal), 보호 모두를 포함 하 여 선택 하는 `protected` 및 `internal` 멤버 선언에서 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-253">Protected internal (meaning protected or internal), which is selected by including both a `protected` and an `internal` modifier in the member declaration.</span></span> <span data-ttu-id="5eabc-254">직관적인 의미 `protected internal` "이이 프로그램에 대해서만 액세스 또는 포함 하는 클래스에서 파생 된 형식"입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-254">The intuitive meaning of `protected internal` is "access limited to this program or types derived from the containing class".</span></span>
*  <span data-ttu-id="5eabc-255">가 포함 하 여 선택 하는 개인을 `private` 멤버 선언에서 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-255">Private, which is selected by including a `private` modifier in the member declaration.</span></span> <span data-ttu-id="5eabc-256">직관적인 의미 `private` "액세스를 포함 하는 형식 제한" 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-256">The intuitive meaning of `private` is "access limited to the containing type".</span></span>

<span data-ttu-id="5eabc-257">멤버 선언이 발생 하는 컨텍스트에 따라, 특정 형식의 선언 된 접근성만 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-257">Depending on the context in which a member declaration takes place, only certain types of declared accessibility are permitted.</span></span> <span data-ttu-id="5eabc-258">또한 멤버 선언 액세스 한정자를 포함 하지 않습니다는 선언이 발생 하는 컨텍스트 선언 된 기본을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-258">Furthermore, when a member declaration does not include any access modifiers, the context in which the declaration takes place determines the default declared accessibility.</span></span>

*  <span data-ttu-id="5eabc-259">네임 스페이스에서는 암시적으로 있음 `public` 접근성을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-259">Namespaces implicitly have `public` declared accessibility.</span></span> <span data-ttu-id="5eabc-260">액세스 한정자가 없습니다 네임 스페이스 선언에서 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-260">No access modifiers are allowed on namespace declarations.</span></span>
*  <span data-ttu-id="5eabc-261">컴파일 단위 또는 네임 스페이스에 선언 된 형식을 가질 수 있습니다 `public` 나 `internal` 내게 필요한 옵션 및 기본적으로 선언 된 `internal` 접근성을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-261">Types declared in compilation units or namespaces can have `public` or `internal` declared accessibility and default to `internal` declared accessibility.</span></span>
*  <span data-ttu-id="5eabc-262">클래스 멤버 선언 된 액세스 가능성의 다섯 가지 종류 중 하나를 포함할 수 있으며 기본적으로 `private` 접근성을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-262">Class members can have any of the five kinds of declared accessibility and default to `private` declared accessibility.</span></span> <span data-ttu-id="5eabc-263">(형식 선언 클래스의 멤버는 5 가지 선언 된 접근성 중 하나일 수 있습니다 하는 대로 네임 스페이스의 멤버 수만 있는 선언 된 형식은 `public` 또는 `internal` 접근성을 선언 합니다.)</span><span class="sxs-lookup"><span data-stu-id="5eabc-263">(Note that a type declared as a member of a class can have any of the five kinds of declared accessibility, whereas a type declared as a member of a namespace can have only `public` or `internal` declared accessibility.)</span></span>
*  <span data-ttu-id="5eabc-264">구조체 멤버를 가질 수 있습니다 `public`, `internal`, 또는 `private` 내게 필요한 옵션 및 기본적으로 선언 된 `private` 구조체는 암시적으로 봉인 되므로 접근성을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-264">Struct members can have `public`, `internal`, or `private` declared accessibility and default to `private` declared accessibility because structs are implicitly sealed.</span></span> <span data-ttu-id="5eabc-265">구조체 멤버 (즉, 해당 구조체에서 상속 되지 않습니다) 구조체에서 도입 된 사용할 수 없습니다 `protected` 또는 `protected internal` 접근성을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-265">Struct members introduced in a struct (that is, not inherited by that struct) cannot have `protected` or `protected internal` declared accessibility.</span></span> <span data-ttu-id="5eabc-266">(구조체의 멤버 수 있는 형식을 선언 `public`, `internal`, 또는 `private` 네임 스페이스의 멤버 수만 있는 선언 된 형식은 접근성을 선언 `public` 또는 `internal` 접근성을 선언 합니다.)</span><span class="sxs-lookup"><span data-stu-id="5eabc-266">(Note that a type declared as a member of a struct can have `public`, `internal`, or `private` declared accessibility, whereas a type declared as a member of a namespace can have only `public` or `internal` declared accessibility.)</span></span>
*  <span data-ttu-id="5eabc-267">인터페이스 멤버를 암시적으로 사용할 `public` 접근성을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-267">Interface members implicitly have `public` declared accessibility.</span></span> <span data-ttu-id="5eabc-268">액세스 한정자가 없습니다 인터페이스 멤버 선언에서 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-268">No access modifiers are allowed on interface member declarations.</span></span>
*  <span data-ttu-id="5eabc-269">열거형 멤버를 암시적으로 있는 `public` 접근성을 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-269">Enumeration members implicitly have `public` declared accessibility.</span></span> <span data-ttu-id="5eabc-270">액세스 한정자가 없습니다 열거형 멤버 선언에서 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-270">No access modifiers are allowed on enumeration member declarations.</span></span>

### <a name="accessibility-domains"></a><span data-ttu-id="5eabc-271">접근성 도메인</span><span class="sxs-lookup"><span data-stu-id="5eabc-271">Accessibility domains</span></span>

<span data-ttu-id="5eabc-272">합니다 ***접근성 도메인*** 멤버의 프로그램 텍스트 멤버에 대 한 액세스 허용 됩니다 (분리 된) 섹션 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-272">The ***accessibility domain*** of a member consists of the (possibly disjoint) sections of program text in which access to the member is permitted.</span></span> <span data-ttu-id="5eabc-273">멤버의 액세스 가능성 도메인을 정의 하는 용도로 멤버 라고 ***최상위*** 형식에 선언 하지 않은 경우 멤버 라고 ***중첩*** 다른 형식 내에서 선언 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="5eabc-273">For purposes of defining the accessibility domain of a member, a member is said to be ***top-level*** if it is not declared within a type, and a member is said to be ***nested*** if it is declared within another type.</span></span> <span data-ttu-id="5eabc-274">또한 합니다 ***프로그램 텍스트*** 모든 프로그램에 포함 된 텍스트 형식의 프로그램 텍스트를 정의 하 고 프로그램의 모든 소스 파일에 포함 된 텍스트를 프로그래밍 하는 모든 정의 된 프로그램의는 *type_declaration*등, 필요에 따라 형식 내에서 중첩 된 형식을 해당 형식의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-274">Furthermore, the ***program text*** of a program is defined as all program text contained in all source files of the program, and the program text of a type is defined as all program text contained in the *type_declaration*s of that type (including, possibly, types that are nested within the type).</span></span>

<span data-ttu-id="5eabc-275">미리 정의 된 형식의 액세스 가능 도메인 (같은 `object`, `int`, 또는 `double`) 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-275">The accessibility domain of a predefined type (such as `object`, `int`, or `double`) is unlimited.</span></span>

<span data-ttu-id="5eabc-276">최상위의 접근성 도메인 형식 바인딩되지 않은 `T` ([바인딩되며 형식에 바인딩되지 않은](types.md#bound-and-unbound-types)) 프로그램에 선언 된 `P` 다음과 같이 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-276">The accessibility domain of a top-level unbound type `T` ([Bound and unbound types](types.md#bound-and-unbound-types)) that is declared in a program `P` is defined as follows:</span></span>

*  <span data-ttu-id="5eabc-277">경우 선언된 된 접근성 `T` 됩니다 `public`의 접근성 도메인 `T` 의 프로그램 텍스트입니다 `P` 및 참조 하는 프로그램 `P`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-277">If the declared accessibility of `T` is `public`, the accessibility domain of `T` is the program text of `P` and any program that references `P`.</span></span>
*  <span data-ttu-id="5eabc-278">`T`에 대해 선언된 액세스 가능성이 `internal`인 경우 `T`의 액세스 가능 도메인은 `P`의 프로그램 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-278">If the declared accessibility of `T` is `internal`, the accessibility domain of `T` is the program text of `P`.</span></span>

<span data-ttu-id="5eabc-279">이러한 정의 바인딩되지 않은 최상위 형식의 액세스 가능 도메인은 항상 최소한 다음을 입력 하는 프로그램의 프로그램 텍스트 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-279">From these definitions it follows that the accessibility domain of a top-level unbound type is always at least the program text of the program in which that type is declared.</span></span>

<span data-ttu-id="5eabc-280">생성된 된 형식에 대 한 액세스 가능성 도메인 `T<A1, ..., An>` 언바운드 제네릭 형식의 액세스 가능 도메인의 교집합 `T` , 형식 인수의 접근성 도메인 `A1, ..., An`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-280">The accessibility domain for a constructed type `T<A1, ..., An>` is the intersection of the accessibility domain of the unbound generic type `T` and the accessibility domains of the type arguments `A1, ..., An`.</span></span>

<span data-ttu-id="5eabc-281">중첩 된 멤버의 접근성 도메인 `M` 형식에서 선언 `T` 프로그램 내 `P` 다음과 같이 정의 됩니다 (에 `M` 자체 형식 되었을 수 있습니다).</span><span class="sxs-lookup"><span data-stu-id="5eabc-281">The accessibility domain of a nested member `M` declared in a type `T` within a program `P` is defined as follows (noting that `M` itself may possibly be a type):</span></span>

*  <span data-ttu-id="5eabc-282">`M`에 대해 선언된 액세스 가능성이 `public`인 경우 `M`의 액세스 가능 도메인은 `T`의 액세스 가능 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-282">If the declared accessibility of `M` is `public`, the accessibility domain of `M` is the accessibility domain of `T`.</span></span>
*  <span data-ttu-id="5eabc-283">경우 선언된 된 접근성 `M` 됩니다 `protected internal`, `D` 의 프로그램 텍스트의 합집합 `P` 에서 파생 된 모든 형식의 프로그램 텍스트 `T`, 외부 선언 된 `P`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-283">If the declared accessibility of `M` is `protected internal`, let `D` be the union of the program text of `P` and the program text of any type derived from `T`, which is declared outside `P`.</span></span> <span data-ttu-id="5eabc-284">접근성 도메인 `M` 의 접근성 도메인의 교집합 `T` 사용 하 여 `D`입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-284">The accessibility domain of `M` is the intersection of the accessibility domain of `T` with `D`.</span></span>
*  <span data-ttu-id="5eabc-285">경우 선언된 된 접근성 `M` 는 `protected`, let `D` 의 프로그램 텍스트의 합집합 `T` 에서 파생 된 모든 형식의 프로그램 텍스트 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-285">If the declared accessibility of `M` is `protected`, let `D` be the union of the program text of `T` and the program text of any type derived from `T`.</span></span> <span data-ttu-id="5eabc-286">접근성 도메인 `M` 의 접근성 도메인의 교집합 `T` 사용 하 여 `D`입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-286">The accessibility domain of `M` is the intersection of the accessibility domain of `T` with `D`.</span></span>
*  <span data-ttu-id="5eabc-287">`M`에 대해 선언된 액세스 가능성이 `internal`인 경우 `M`의 액세스 가능 도메인은 `T`의 프로그램 텍스트를 가진 `P`의 액세스 가능 도메인의 교집합 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-287">If the declared accessibility of `M` is `internal`, the accessibility domain of `M` is the intersection of the accessibility domain of `T` with the program text of `P`.</span></span>
*  <span data-ttu-id="5eabc-288">`M`에 대해 선언된 액세스 가능성이 `private`인 경우 `M`의 액세스 가능 도메인은 `T`의 프로그램 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-288">If the declared accessibility of `M` is `private`, the accessibility domain of `M` is the program text of `T`.</span></span>

<span data-ttu-id="5eabc-289">이러한 정의 중첩 된 멤버의 접근성 도메인은 항상 최소한 따릅니다 멤버가 선언 된 형식의 프로그램 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-289">From these definitions it follows that the accessibility domain of a nested member is always at least the program text of the type in which the member is declared.</span></span> <span data-ttu-id="5eabc-290">또한 멤버의 액세스 가능 도메인은 멤버가 선언 된 형식의 액세스 가능 도메인은 보다 더 포함 되지를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-290">Furthermore, it follows that the accessibility domain of a member is never more inclusive than the accessibility domain of the type in which the member is declared.</span></span>

<span data-ttu-id="5eabc-291">직관적인 관점에서 형식 또는 멤버 `M` 은 액세스가 허용 되는지 확인 하려면 다음 단계를 실행 액세스:</span><span class="sxs-lookup"><span data-stu-id="5eabc-291">In intuitive terms, when a type or member `M` is accessed, the following steps are evaluated to ensure that the access is permitted:</span></span>

*  <span data-ttu-id="5eabc-292">첫째, `M` 컴파일 타임 오류가 발생 하는 해당 형식에 액세스할 수 없는 경우 (것과 반대로 컴파일 단위 또는 네임 스페이스), 형식 내에서 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-292">First, if `M` is declared within a type (as opposed to a compilation unit or a namespace), a compile-time error occurs if that type is not accessible.</span></span>
*  <span data-ttu-id="5eabc-293">그런 다음 if `M` 는 `public`, 액세스가 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-293">Then, if `M` is `public`, the access is permitted.</span></span>
*  <span data-ttu-id="5eabc-294">그렇지 않은 경우, `M` 됩니다 `protected internal`는 프로그램 내에서 발생 하는 경우 액세스가 허용 됩니다 `M` 선언 되는 클래스에서 파생 된 클래스 내에서 발생 하는 경우 또는 `M` 선언 되 고 파생을 통해 수행 클래스 유형 ([보호 된 멤버 액세스 예를 들어](basic-concepts.md#protected-access-for-instance-members)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-294">Otherwise, if `M` is `protected internal`, the access is permitted if it occurs within the program in which `M` is declared, or if it occurs within a class derived from the class in which `M` is declared and takes place through the derived class type ([Protected access for instance members](basic-concepts.md#protected-access-for-instance-members)).</span></span>
*  <span data-ttu-id="5eabc-295">그렇지 않은 경우, `M` 됩니다 `protected`는 클래스 내에서 발생 하는 경우 액세스가 허용 됩니다 `M` 선언 되는 클래스에서 파생 된 클래스 내에서 발생 하는 경우 또는 `M` 선언 되 고 파생을 통해 수행 클래스 유형 ([보호 된 멤버 액세스 예를 들어](basic-concepts.md#protected-access-for-instance-members)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-295">Otherwise, if `M` is `protected`, the access is permitted if it occurs within the class in which `M` is declared, or if it occurs within a class derived from the class in which `M` is declared and takes place through the derived class type ([Protected access for instance members](basic-concepts.md#protected-access-for-instance-members)).</span></span>
*  <span data-ttu-id="5eabc-296">그렇지 않은 경우, `M` 은 `internal`에는 프로그램 내에서 발생 하는 경우 액세스가 허용 됩니다 `M` 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-296">Otherwise, if `M` is `internal`, the access is permitted if it occurs within the program in which `M` is declared.</span></span>
*  <span data-ttu-id="5eabc-297">그렇지 않은 경우, `M` 은 `private`에는 형식 내에서 발생 하는 경우 액세스가 허용 됩니다 `M` 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-297">Otherwise, if `M` is `private`, the access is permitted if it occurs within the type in which `M` is declared.</span></span>
*  <span data-ttu-id="5eabc-298">이 고, 그렇지 형식 또는 멤버에 액세스할 수 없는 및 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-298">Otherwise, the type or member is inaccessible, and a compile-time error occurs.</span></span>

<span data-ttu-id="5eabc-299">예제</span><span class="sxs-lookup"><span data-stu-id="5eabc-299">In the example</span></span>
```csharp
public class A
{
    public static int X;
    internal static int Y;
    private static int Z;
}

internal class B
{
    public static int X;
    internal static int Y;
    private static int Z;

    public class C
    {
        public static int X;
        internal static int Y;
        private static int Z;
    }

    private class D
    {
        public static int X;
        internal static int Y;
        private static int Z;
    }
}
```
<span data-ttu-id="5eabc-300">클래스 및 멤버 액세스 가능성 도메인에</span><span class="sxs-lookup"><span data-stu-id="5eabc-300">the classes and members have the following accessibility domains:</span></span>

*  <span data-ttu-id="5eabc-301">접근성 도메인 `A` 고 `A.X` 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-301">The accessibility domain of `A` and `A.X` is unlimited.</span></span>
*  <span data-ttu-id="5eabc-302">접근성 도메인 `A.Y`, `B`를 `B.X`, `B.Y`를 `B.C`를 `B.C.X`, 및 `B.C.Y` 포함 하는 프로그램의 프로그램 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-302">The accessibility domain of `A.Y`, `B`, `B.X`, `B.Y`, `B.C`, `B.C.X`, and `B.C.Y` is the program text of the containing program.</span></span>
*  <span data-ttu-id="5eabc-303">접근성 도메인 `A.Z` 의 프로그램 텍스트 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-303">The accessibility domain of `A.Z` is the program text of `A`.</span></span>
*  <span data-ttu-id="5eabc-304">접근성 도메인 `B.Z` 하 고 `B.D` 의 프로그램 텍스트입니다 `B`의 프로그램 텍스트를 포함 하 여 `B.C` 및 `B.D`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-304">The accessibility domain of `B.Z` and `B.D` is the program text of `B`, including the program text of `B.C` and `B.D`.</span></span>
*  <span data-ttu-id="5eabc-305">접근성 도메인 `B.C.Z` 의 프로그램 텍스트 `B.C`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-305">The accessibility domain of `B.C.Z` is the program text of `B.C`.</span></span>
*  <span data-ttu-id="5eabc-306">접근성 도메인 `B.D.X` 하 고 `B.D.Y` 의 프로그램 텍스트입니다 `B`의 프로그램 텍스트를 포함 하 여 `B.C` 및 `B.D`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-306">The accessibility domain of `B.D.X` and `B.D.Y` is the program text of `B`, including the program text of `B.C` and `B.D`.</span></span>
*  <span data-ttu-id="5eabc-307">접근성 도메인 `B.D.Z` 의 프로그램 텍스트 `B.D`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-307">The accessibility domain of `B.D.Z` is the program text of `B.D`.</span></span>

<span data-ttu-id="5eabc-308">위의 예제와 같이 멤버의 액세스 가능성 도메인을 포함 하는 보다 크지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-308">As the example illustrates, the accessibility domain of a member is never larger than that of a containing type.</span></span> <span data-ttu-id="5eabc-309">예를 들어, 경우에 모든 `X` 멤버는 public 선언 된 액세스 가능성을 제외한 모든 `A.X` 액세스 가능 도메인을 포함 하는 형식에 의해 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-309">For example, even though all `X` members have public declared accessibility, all but `A.X` have accessibility domains that are constrained by a containing type.</span></span>

<span data-ttu-id="5eabc-310">에 설명 된 대로 [멤버](basic-concepts.md#members), 예를 들어 생성자, 소멸자 및 정적 생성자를 제외 하 고 기본 클래스의 모든 멤버는 파생된 형식에서 상속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-310">As described in [Members](basic-concepts.md#members), all members of a base class, except for instance constructors, destructors and static constructors, are inherited by derived types.</span></span> <span data-ttu-id="5eabc-311">기본 클래스의 private 멤버 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-311">This includes even private members of a base class.</span></span> <span data-ttu-id="5eabc-312">그러나 개인 멤버의 액세스 가능 도메인은 멤버가 선언 된 형식의 프로그램 텍스트만을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-312">However, the accessibility domain of a private member includes only the program text of the type in which the member is declared.</span></span> <span data-ttu-id="5eabc-313">예제</span><span class="sxs-lookup"><span data-stu-id="5eabc-313">In the example</span></span>
```csharp
class A
{
    int x;

    static void F(B b) {
        b.x = 1;        // Ok
    }
}

class B: A
{
    static void F(B b) {
        b.x = 1;        // Error, x not accessible
    }
}
```
<span data-ttu-id="5eabc-314">합니다 `B` 클래스는 private 멤버를 상속 `x` 에서 `A` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-314">the `B` class inherits the private member `x` from the `A` class.</span></span> <span data-ttu-id="5eabc-315">내에서 액세스할 수만 전용 멤버 이므로 합니다 *class_body* 의 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-315">Because the member is private, it is only accessible within the *class_body* of `A`.</span></span> <span data-ttu-id="5eabc-316">따라서에 대 한 액세스 `b.x` 성공 합니다 `A.F` 메서드이지만에서 실패를 `B.F` 메서드.</span><span class="sxs-lookup"><span data-stu-id="5eabc-316">Thus, the access to `b.x` succeeds in the `A.F` method, but fails in the `B.F` method.</span></span>

### <a name="protected-access-for-instance-members"></a><span data-ttu-id="5eabc-317">인스턴스 멤버에 대 한 보호 된 액세스</span><span class="sxs-lookup"><span data-stu-id="5eabc-317">Protected access for instance members</span></span>

<span data-ttu-id="5eabc-318">경우는 `protected` 인스턴스 멤버에 선언 된 클래스의 프로그램 텍스트 외부 액세스 및 시기를 `protected internal` 인스턴스 멤버는 선언 되는 프로그램의 프로그램 텍스트 외부 액세스, 액세스 내에서 발생 해야 합니다.는 이전에 선언 되는 클래스에서 파생 되는 클래스 선언입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-318">When a `protected` instance member is accessed outside the program text of the class in which it is declared, and when a `protected internal` instance member is accessed outside the program text of the program in which it is declared, the access must take place within a class declaration that derives from the class in which it is declared.</span></span> <span data-ttu-id="5eabc-319">또한 액세스는 여기에서 생성 되는 클래스 형식 또는 해당 파생된 클래스 형식의 인스턴스를 통해 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-319">Furthermore, the access is required to take place through an instance of that derived class type or a class type constructed from it.</span></span> <span data-ttu-id="5eabc-320">하나의 파생된 클래스 멤버는 동일한 기본 클래스에서 상속 하는 경우에 다른 파생된 클래스의 protected 멤버에 액세스 하지 못하도록 방지 하는이 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-320">This restriction prevents one derived class from accessing protected members of other derived classes, even when the members are inherited from the same base class.</span></span>

<span data-ttu-id="5eabc-321">수 있도록 `B` 보호 된 인스턴스 멤버를 선언 하는 기본 클래스일 `M`, 말고 `D` 에서 파생 된 클래스 수 `B`입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-321">Let `B` be a base class that declares a protected instance member `M`, and let `D` be a class that derives from `B`.</span></span> <span data-ttu-id="5eabc-322">내 합니다 *class_body* 의 `D`에 대 한 액세스 `M` 다음 형식 중 하나를 수행:</span><span class="sxs-lookup"><span data-stu-id="5eabc-322">Within the *class_body* of `D`, access to `M` can take one of the following forms:</span></span>

*  <span data-ttu-id="5eabc-323">정규화 되지 않은 *type_name* 하거나 *primary_expression* 양식의 `M`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-323">An unqualified *type_name* or *primary_expression* of the form `M`.</span></span>
*  <span data-ttu-id="5eabc-324">*primary_expression* 양식의 `E.M`, 형식의 제공 `E` 는 `T` 에서 파생 된 클래스 또는 `T`여기서 `T` 클래스 형식인 `D`, 또는 클래스 형식이 생성 `D`</span><span class="sxs-lookup"><span data-stu-id="5eabc-324">A *primary_expression* of the form `E.M`, provided the type of `E` is `T` or a class derived from `T`, where `T` is the class type `D`, or a class type constructed from `D`</span></span>
*  <span data-ttu-id="5eabc-325">A *primary_expression* 양식의 `base.M`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-325">A *primary_expression* of the form `base.M`.</span></span>

<span data-ttu-id="5eabc-326">이러한 형태의 액세스 하는 것 외에도 파생된 클래스에서 기본 클래스의 보호 된 인스턴스 생성자에 액세스할 수는 *constructor_initializer* ([생성자 이니셜라이저](classes.md#constructor-initializers)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-326">In addition to these forms of access, a derived class can access a protected instance constructor of a base class in a *constructor_initializer* ([Constructor initializers](classes.md#constructor-initializers)).</span></span>

<span data-ttu-id="5eabc-327">예제</span><span class="sxs-lookup"><span data-stu-id="5eabc-327">In the example</span></span>
```csharp
public class A
{
    protected int x;

    static void F(A a, B b) {
        a.x = 1;        // Ok
        b.x = 1;        // Ok
    }
}

public class B: A
{
    static void F(A a, B b) {
        a.x = 1;        // Error, must access through instance of B
        b.x = 1;        // Ok
    }
}
```
<span data-ttu-id="5eabc-328">내 `A`, 액세스 하는 것이 불가능 `x` 둘 다의 인스턴스를 통해 `A` 및 `B`든에서 액세스가 이루어지는의 인스턴스를 통해 때문 `A` 에서 파생 된 클래스 또는 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-328">within `A`, it is possible to access `x` through instances of both `A` and `B`, since in either case the access takes place through an instance of `A` or a class derived from `A`.</span></span> <span data-ttu-id="5eabc-329">그러나 내 `B`에 액세스할 수 없는 `x` 의 인스턴스를 통해 `A`, 하므로 `A` 에서 파생 되지 않습니다 `B`.</span><span class="sxs-lookup"><span data-stu-id="5eabc-329">However, within `B`, it is not possible to access `x` through an instance of `A`, since `A` does not derive from `B`.</span></span>

<span data-ttu-id="5eabc-330">예제</span><span class="sxs-lookup"><span data-stu-id="5eabc-330">In the example</span></span>
```csharp
class C<T>
{
    protected T x;
}

class D<T>: C<T>
{
    static void F() {
        D<T> dt = new D<T>();
        D<int> di = new D<int>();
        D<string> ds = new D<string>();
        dt.x = default(T);
        di.x = 123;
        ds.x = "test";
    }
}
```
<span data-ttu-id="5eabc-331">세 가지 할당을 `x` 모두를 제네릭 형식에서 생성 된 클래스 형식의 인스턴스를 통해 발생할 없기 때문에 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-331">the three assignments to `x` are permitted because they all take place through instances of class types constructed from the generic type.</span></span>

### <a name="accessibility-constraints"></a><span data-ttu-id="5eabc-332">내게 필요한 옵션의 제약 조건</span><span class="sxs-lookup"><span data-stu-id="5eabc-332">Accessibility constraints</span></span>

<span data-ttu-id="5eabc-333">C# 언어의 몇 가지 구문에는 형식이 되도록 필요 ***만큼 액세스 가능 이상*** 멤버 또는 다른 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-333">Several constructs in the C# language require a type to be ***at least as accessible as*** a member or another type.</span></span> <span data-ttu-id="5eabc-334">형식 `T` 멤버 또는 형식으로 액세스할 수 있도록 이라고 `M` 하는 경우의 접근성 도메인 `T` 의 접근성 도메인은 `M`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-334">A type `T` is said to be at least as accessible as a member or type `M` if the accessibility domain of `T` is a superset of the accessibility domain of `M`.</span></span> <span data-ttu-id="5eabc-335">즉, `T` 이상으로 액세스할 수 `M` 경우 `T` 에 액세스할 수 있는 모든 컨텍스트에서 `M` 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-335">In other words, `T` is at least as accessible as `M` if `T` is accessible in all contexts in which `M` is accessible.</span></span>

<span data-ttu-id="5eabc-336">다음 내게 필요한 옵션 제약 조건이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-336">The following accessibility constraints exist:</span></span>

*  <span data-ttu-id="5eabc-337">클래스 형식의 직접 기본 클래스는 적어도 클래스 형식 자체 수준만큼 액세스 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-337">The direct base class of a class type must be at least as accessible as the class type itself.</span></span>
*  <span data-ttu-id="5eabc-338">인터페이스 형식의 명시적 기본 인터페이스는 적어도 인터페이스 형식 자체 수준만큼 액세스 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-338">The explicit base interfaces of an interface type must be at least as accessible as the interface type itself.</span></span>
*  <span data-ttu-id="5eabc-339">대리자 형식의 반환 형식 및 매개 변수 형식은 적어도 대리자 형식 자체 수준만큼 액세스 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-339">The return type and parameter types of a delegate type must be at least as accessible as the delegate type itself.</span></span>
*  <span data-ttu-id="5eabc-340">상수의 형식은 적어도 상수 자체 수준만큼 액세스 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-340">The type of a constant must be at least as accessible as the constant itself.</span></span>
*  <span data-ttu-id="5eabc-341">필드의 형식은 적어도 필드 자체 수준만큼 액세스 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-341">The type of a field must be at least as accessible as the field itself.</span></span>
*  <span data-ttu-id="5eabc-342">메서드의 반환 형식 및 매개 변수 형식은 적어도 메서드 자체 수준만큼 액세스 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-342">The return type and parameter types of a method must be at least as accessible as the method itself.</span></span>
*  <span data-ttu-id="5eabc-343">속성의 형식은 적어도 속성 자체 수준만큼 액세스 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-343">The type of a property must be at least as accessible as the property itself.</span></span>
*  <span data-ttu-id="5eabc-344">이벤트의 형식은 적어도 이벤트 자체 수준만큼 액세스 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-344">The type of an event must be at least as accessible as the event itself.</span></span>
*  <span data-ttu-id="5eabc-345">인덱서의 형식 및 매개 변수 형식은 적어도 인덱서 자체 수준만큼 액세스 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-345">The type and parameter types of an indexer must be at least as accessible as the indexer itself.</span></span>
*  <span data-ttu-id="5eabc-346">연산자의 반환 형식 및 매개 변수 형식은 적어도 연산자 자체 수준만큼 액세스 가능해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-346">The return type and parameter types of an operator must be at least as accessible as the operator itself.</span></span>
*  <span data-ttu-id="5eabc-347">인스턴스 생성자의 매개 변수 형식은 적어도 인스턴스 생성자 자체 수준 만큼 액세스 가능 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-347">The parameter types of an instance constructor must be at least as accessible as the instance constructor itself.</span></span>

<span data-ttu-id="5eabc-348">예제</span><span class="sxs-lookup"><span data-stu-id="5eabc-348">In the example</span></span>
```csharp
class A {...}

public class B: A {...}
```
<span data-ttu-id="5eabc-349">합니다 `B` 있으므로 클래스는 컴파일 타임 오류가 발생 `A` 이상으로 액세스할 수 없는 `B`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-349">the `B` class results in a compile-time error because `A` is not at least as accessible as `B`.</span></span>

<span data-ttu-id="5eabc-350">예와 마찬가지로</span><span class="sxs-lookup"><span data-stu-id="5eabc-350">Likewise, in the example</span></span>
```csharp
class A {...}

public class B
{
    A F() {...}

    internal A G() {...}

    public A H() {...}
}
```
<span data-ttu-id="5eabc-351">합니다 `H` 의 메서드 `B` 반환 형식 때문에 컴파일 타임 오류가 발생 `A` 이상 방법으로 액세스할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-351">the `H` method in `B` results in a compile-time error because the return type `A` is not at least as accessible as the method.</span></span>

## <a name="signatures-and-overloading"></a><span data-ttu-id="5eabc-352">시그니처 및 오버 로드</span><span class="sxs-lookup"><span data-stu-id="5eabc-352">Signatures and overloading</span></span>

<span data-ttu-id="5eabc-353">메서드, 인스턴스 생성자, 인덱서 및 연산자에 따라 구분 됩니다 자신의 ***서명을***:</span><span class="sxs-lookup"><span data-stu-id="5eabc-353">Methods, instance constructors, indexers, and operators are characterized by their ***signatures***:</span></span>

*  <span data-ttu-id="5eabc-354">메서드 시그니처 메서드, 형식 매개 변수의 개수, 종류 및 종류 (값, 참조 또는 출력)의 왼쪽에서 오른쪽 순서로 것으로 간주 하는 정식 매개 변수의 각 이름을 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-354">The signature of a method consists of the name of the method, the number of type parameters and the type and kind (value, reference, or output) of each of its formal parameters, considered in the order left to right.</span></span> <span data-ttu-id="5eabc-355">이러한 목적을 위해 형식 매개 변수 형식에서 발생 하는 메서드의 형식 매개 변수에 메서드의 형식 인수 목록에 있는 서 수 위치를 기준으로 하지만 해당 이름으로 식별 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-355">For these purposes, any type parameter of the method that occurs in the type of a formal parameter is identified not by its name, but by its ordinal position in the type argument list of the method.</span></span> <span data-ttu-id="5eabc-356">메서드 서명의 포함 되지 않습니다 반환 형식으로는 `params` 가장 오른쪽 매개 변수 및 선택적 형식 매개 변수 제약 조건에 대해 지정 될 수 있는 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-356">The signature of a method specifically does not include the return type, the `params` modifier that may be specified for the right-most parameter, nor the optional type parameter constraints.</span></span>
*  <span data-ttu-id="5eabc-357">인스턴스 생성자 서명의 형식 및 종류 (값, 참조 또는 출력)의 왼쪽에서 오른쪽 순서로 것으로 간주 하는 정식 매개 변수의 각 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-357">The signature of an instance constructor consists of the type and kind (value, reference, or output) of each of its formal parameters, considered in the order left to right.</span></span> <span data-ttu-id="5eabc-358">인스턴스 생성자의 시그니처에 포함 하지 않습니다는 `params` 가장 오른쪽 매개 변수에 대해 지정 될 수 있는 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-358">The signature of an instance constructor specifically does not include the `params` modifier that may be specified for the right-most parameter.</span></span>
*  <span data-ttu-id="5eabc-359">인덱서의 시그니처 각각 왼쪽에서 오른쪽 순서로 것으로 간주 하는 정식 매개 변수의 형식으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-359">The signature of an indexer consists of the type of each of its formal parameters, considered in the order left to right.</span></span> <span data-ttu-id="5eabc-360">인덱서의 시그니처는 포함 되지 않습니다 요소 형식에도 포함 되지 않습니다는 `params` 가장 오른쪽 매개 변수에 대해 지정 될 수 있는 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-360">The signature of an indexer specifically does not include the element type, nor does it include the `params` modifier that may be specified for the right-most parameter.</span></span>
*  <span data-ttu-id="5eabc-361">연산자의 시그니처에 연산자 및 각각 왼쪽에서 오른쪽 순서로 것으로 간주 하는 정식 매개 변수의 형식 이름으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-361">The signature of an operator consists of the name of the operator and the type of each of its formal parameters, considered in the order left to right.</span></span> <span data-ttu-id="5eabc-362">연산자의 시그니처에 결과 형식은 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-362">The signature of an operator specifically does not include the result type.</span></span>

<span data-ttu-id="5eabc-363">시그니처는 사용 하도록 설정 하는 메커니즘 ***오버 로드*** 클래스, 구조체 및 인터페이스의 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-363">Signatures are the enabling mechanism for ***overloading*** of members in classes, structs, and interfaces:</span></span>

*  <span data-ttu-id="5eabc-364">메서드의 오버 로드는 클래스, 구조체 또는 인터페이스는 클래스, 구조체 또는 인터페이스 내에서 고유 시그니처가 동일한 이름의 여러 메서드를 선언할 수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-364">Overloading of methods permits a class, struct, or interface to declare multiple methods with the same name, provided their signatures are unique within that class, struct, or interface.</span></span>
*  <span data-ttu-id="5eabc-365">이러한 시그니처는 해당 클래스 또는 구조체 내에서 고유 제공 클래스 또는 여러 인스턴스 생성자를 선언 하는 구조체를 허용 인스턴스 생성자의 오버 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-365">Overloading of instance constructors permits a class or struct to declare multiple instance constructors, provided their signatures are unique within that class or struct.</span></span>
*  <span data-ttu-id="5eabc-366">이러한 시그니처는 해당 클래스, 구조체 또는 인터페이스 내에서 고유 제공 클래스, 구조체 또는 여러 인덱서를 선언 하는 인터페이스를 허용 인덱서 오버 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-366">Overloading of indexers permits a class, struct, or interface to declare multiple indexers, provided their signatures are unique within that class, struct, or interface.</span></span>
*  <span data-ttu-id="5eabc-367">연산자 오버 로드는 클래스 또는 구조체는 클래스 또는 구조체 내에서 고유 시그니처가 동일한 이름의 여러 연산자를 선언할 수를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-367">Overloading of operators permits a class or struct to declare multiple operators with the same name, provided their signatures are unique within that class or struct.</span></span>

<span data-ttu-id="5eabc-368">하지만 `out` 하 고 `ref` 매개 변수 한정자를 시그니처의 일부로 간주 되, 단일 형식에 선언 된 멤버 시그니처의 전적으로 달라 `ref` 고 `out`입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-368">Although `out` and `ref` parameter modifiers are considered part of a signature, members declared in a single type cannot differ in signature solely by `ref` and `out`.</span></span> <span data-ttu-id="5eabc-369">컴파일 타임 오류가 발생 하는 경우 모든 매개 변수를 가진 두 메서드에 동일한 서명 사용 하 여 동일한 형식의 두 멤버는 선언 `out` 한정자로 변경 된 `ref` 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-369">A compile-time error occurs if two members are declared in the same type with signatures that would be the same if all parameters in both methods with `out` modifiers were changed to `ref` modifiers.</span></span> <span data-ttu-id="5eabc-370">서명이 일치 하는 다른 용도로 (예를 들어 숨기기 나 재정의), `ref` 고 `out` 시그니처의 일부로 간주 되 고 서로 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-370">For other purposes of signature matching (e.g., hiding or overriding), `ref` and `out` are considered part of the signature and do not match each other.</span></span> <span data-ttu-id="5eabc-371">(이 제한은 C# 프로그램에는 인프라 CLI (공용 언어)에 다른 메서드를 정의 하는 방법을 제공 하지 않는 실행을 쉽게 번역할 수 있도록 `ref` 고 `out`.)</span><span class="sxs-lookup"><span data-stu-id="5eabc-371">(This restriction is to allow C#  programs to be easily translated to run on the Common Language Infrastructure (CLI), which does not provide a way to define methods that differ solely in `ref` and `out`.)</span></span>

<span data-ttu-id="5eabc-372">형식 서명의 용도로 `object` 및 `dynamic` 동일한 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-372">For the purposes of signatures, the types `object` and `dynamic` are considered the same.</span></span> <span data-ttu-id="5eabc-373">단일 형식에 선언 된 멤버 달라질 수 있습니다 따라서 하지 서명에서 전적으로 `object` 고 `dynamic`입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-373">Members declared in a single type can therefore not differ in signature solely by `object` and `dynamic`.</span></span>

<span data-ttu-id="5eabc-374">다음 예제에서는 해당 서명이 함께 오버 로드 된 메서드 선언 집합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-374">The following example shows a set of overloaded method declarations along with their signatures.</span></span>
```csharp
interface ITest
{
    void F();                        // F()

    void F(int x);                   // F(int)

    void F(ref int x);               // F(ref int)

    void F(out int x);               // F(out int)      error

    void F(int x, int y);            // F(int, int)

    int F(string s);                 // F(string)

    int F(int x);                    // F(int)          error

    void F(string[] a);              // F(string[])

    void F(params string[] a);       // F(string[])     error
}
```

<span data-ttu-id="5eabc-375">모든 `ref` 하 고 `out` 매개 변수 한정자 ([메서드 매개 변수](classes.md#method-parameters)) 서명의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-375">Note that any `ref` and `out` parameter modifiers ([Method parameters](classes.md#method-parameters)) are part of a signature.</span></span> <span data-ttu-id="5eabc-376">따라서 `F(int)` 고 `F(ref int)` 고유한 서명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-376">Thus, `F(int)` and `F(ref int)` are unique signatures.</span></span> <span data-ttu-id="5eabc-377">그러나 `F(ref int)` 하 고 `F(out int)` 시그니처에 여만 다르므로 동일한 인터페이스 내에서 선언할 수 없습니다 `ref` 및 `out`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-377">However, `F(ref int)` and `F(out int)` cannot be declared within the same interface because their signatures differ solely by `ref` and `out`.</span></span> <span data-ttu-id="5eabc-378">반환 형식은 참고 또한 하며 `params` 한정자의 일부가 아닌 서명을 있으므로 또는 포함 또는 제외의 반환 형식에 따라 전적으로 오버 로드할 수 없습니다는 `params` 한정자.</span><span class="sxs-lookup"><span data-stu-id="5eabc-378">Also, note that the return type and the `params` modifier are not part of a signature, so it is not possible to overload solely based on return type or on the inclusion or exclusion of the `params` modifier.</span></span> <span data-ttu-id="5eabc-379">따라서 메서드 선언을 `F(int)` 및 `F(params string[])` 컴파일 타임 오류가 발생 하는 위에서 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-379">As such, the declarations of the methods `F(int)` and `F(params string[])` identified above result in a compile-time error.</span></span>

## <a name="scopes"></a><span data-ttu-id="5eabc-380">범위</span><span class="sxs-lookup"><span data-stu-id="5eabc-380">Scopes</span></span>

<span data-ttu-id="5eabc-381">합니다 ***범위*** 이름의 있는 이름의 한정자 없이 이름으로 선언 된 엔터티를 참조할 수는 프로그램 텍스트의 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-381">The ***scope*** of a name is the region of program text within which it is possible to refer to the entity declared by the name without qualification of the name.</span></span> <span data-ttu-id="5eabc-382">그러나 범위 수 ***중첩***, 및 내부 범위에서 외부 범위에서 이름의 의미를 다시 선언할 수 있습니다 (이 따른 제한의 제거 하지 않습니다 [선언](basic-concepts.md#declarations) 중첩된 된 블록 내에서 한 것 지역 변수는 바깥쪽 블록에 동일한 이름 가진 지역 변수를 선언할 수).</span><span class="sxs-lookup"><span data-stu-id="5eabc-382">Scopes can be ***nested***, and an inner scope may redeclare the meaning of a name from an outer scope (this does not, however, remove the restriction imposed by [Declarations](basic-concepts.md#declarations) that within a nested block it is not possible to declare a local variable with the same name as a local variable in an enclosing block).</span></span> <span data-ttu-id="5eabc-383">외부 범위에서 이름을 다음 이라고 ***숨겨진*** 프로그램의 지역에서 내부 범위에서 텍스트 설명 및 이름을 정규화 하 여 외부 이름에 대 한 액세스는 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-383">The name from the outer scope is then said to be ***hidden*** in the region of program text covered by the inner scope, and access to the outer name is only possible by qualifying the name.</span></span>

*  <span data-ttu-id="5eabc-384">으로 선언 된 네임 스페이스 멤버의 범위를 *namespace_member_declaration* ([Namespace 멤버](namespaces.md#namespace-members)) 없는 바깥쪽 *namespace_declaration* 전체 프로그램이 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-384">The scope of a namespace member declared by a *namespace_member_declaration* ([Namespace members](namespaces.md#namespace-members)) with no enclosing *namespace_declaration* is the entire program text.</span></span>
*  <span data-ttu-id="5eabc-385">선언 된 네임 스페이스 멤버의 범위를 *namespace_member_declaration* 내는 *namespace_declaration* 정규화 된 이름이 `N` 는 *namespace_body*  의 모든 *namespace_declaration* 정규화 된 이름이 `N` 시작 또는 `N`뒤에 마침표, 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-385">The scope of a namespace member declared by a *namespace_member_declaration* within a *namespace_declaration* whose fully qualified name is `N` is the *namespace_body* of every *namespace_declaration* whose fully qualified name is `N` or starts with `N`, followed by a period.</span></span>
*  <span data-ttu-id="5eabc-386">정의한 이름의 범위는 *extern_alias_directive* 으로 확장 되는 *using_directive*개이면 *global_attributes* 및 *namespace_member_ 선언*직접 포함 하는 컴파일 단위 또는 네임 스페이스 본문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-386">The scope of name defined by an *extern_alias_directive* extends over the *using_directive*s, *global_attributes* and *namespace_member_declaration*s of its immediately containing compilation unit or namespace body.</span></span> <span data-ttu-id="5eabc-387">*extern_alias_directive* 기본 선언 공간에 새 멤버를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-387">An *extern_alias_directive* does not contribute any new members to the underlying declaration space.</span></span> <span data-ttu-id="5eabc-388">즉, 한 *extern_alias_directive* 은 전이적이 아니므로 하지만 대신 컴파일 단위 또는 네임 스페이스 본문만 발생 하는 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-388">In other words, an *extern_alias_directive* is not transitive, but, rather, affects only the compilation unit or namespace body in which it occurs.</span></span>
*  <span data-ttu-id="5eabc-389">이름 범위 정의 또는 가져온를 *using_directive* ([지시문을 사용 하 여](namespaces.md#using-directives))으로 확장 되는 *namespace_member_declaration*의  *compilation_unit* 하거나 *namespace_body* 나타나는 합니다 *using_directive* 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-389">The scope of a name defined or imported by a *using_directive* ([Using directives](namespaces.md#using-directives)) extends over the *namespace_member_declaration*s of the *compilation_unit* or *namespace_body* in which the *using_directive* occurs.</span></span> <span data-ttu-id="5eabc-390">A *using_directive* 특정 내에서 사용할 수 있는 0 개 이상의 네임 스페이스, 형식 또는 멤버 이름 확인 될 수 있습니다 *compilation_unit* 또는 *namespace_body*, 되지 않지만 새 멤버를 내부 선언 공간에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-390">A *using_directive* may make zero or more namespace, type or member names available within a particular *compilation_unit* or *namespace_body*, but does not contribute any new members to the underlying declaration space.</span></span> <span data-ttu-id="5eabc-391">즉, 한 *using_directive* 전이 되지 않지만 대신에 영향을 줍니다는 *compilation_unit* 또는 *namespace_body* 에서 발생 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-391">In other words, a *using_directive* is not transitive but rather affects only the *compilation_unit* or *namespace_body* in which it occurs.</span></span>
*  <span data-ttu-id="5eabc-392">으로 선언 된 형식 매개 변수의 범위를 *type_parameter_list* 에 *class_declaration* ([클래스 선언을](classes.md#class-declarations))는는 *class_base*하십시오 *type_parameter_constraints_clause*s, 및 *class_body* 의 *class_declaration*.</span><span class="sxs-lookup"><span data-stu-id="5eabc-392">The scope of a type parameter declared by a *type_parameter_list* on a *class_declaration* ([Class declarations](classes.md#class-declarations)) is the *class_base*, *type_parameter_constraints_clause*s, and *class_body* of that *class_declaration*.</span></span>
*  <span data-ttu-id="5eabc-393">으로 선언 된 형식 매개 변수의 범위를 *type_parameter_list* 에 *struct_declaration* ([구조체 선언](structs.md#struct-declarations))는는 *struct_interfaces* , *type_parameter_constraints_clause*s, 및 *struct_body* 의 *struct_declaration*합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-393">The scope of a type parameter declared by a *type_parameter_list* on a *struct_declaration* ([Struct declarations](structs.md#struct-declarations)) is the *struct_interfaces*, *type_parameter_constraints_clause*s, and *struct_body* of that *struct_declaration*.</span></span>
*  <span data-ttu-id="5eabc-394">으로 선언 된 형식 매개 변수의 범위를 *type_parameter_list* 에 *interface_declaration* ([인터페이스 선언](interfaces.md#interface-declarations))는는 *interface_base* , *type_parameter_constraints_clause*s, 및 *interface_body* 의 *interface_declaration*합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-394">The scope of a type parameter declared by a *type_parameter_list* on an *interface_declaration* ([Interface declarations](interfaces.md#interface-declarations)) is the *interface_base*, *type_parameter_constraints_clause*s, and *interface_body* of that *interface_declaration*.</span></span>
*  <span data-ttu-id="5eabc-395">으로 선언 된 형식 매개 변수의 범위를 *type_parameter_list* 에 *delegate_declaration* ([대리자 선언](delegates.md#delegate-declarations))는는 *return_type*, *formal_parameter_list*, 및 *type_parameter_constraints_clause*는 s *delegate_declaration*합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-395">The scope of a type parameter declared by a *type_parameter_list* on a *delegate_declaration* ([Delegate declarations](delegates.md#delegate-declarations)) is the *return_type*, *formal_parameter_list*, and *type_parameter_constraints_clause*s of that *delegate_declaration*.</span></span>
*  <span data-ttu-id="5eabc-396">선언 된 멤버의 범위를 *class_member_declaration* ([본문 클래스](classes.md#class-body))는는 *class_body* 선언이 발생에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-396">The scope of a member declared by a *class_member_declaration* ([Class body](classes.md#class-body)) is the *class_body* in which the declaration occurs.</span></span> <span data-ttu-id="5eabc-397">클래스 멤버의 범위를 확장 하는 또한 합니다 *class_body* 의 파생 클래스의 액세스 가능 도메인에 포함 된 ([접근성 도메인](basic-concepts.md#accessibility-domains)) 멤버의 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-397">In addition, the scope of a class member extends to the *class_body* of those derived classes that are included in the accessibility domain ([Accessibility domains](basic-concepts.md#accessibility-domains)) of the member.</span></span>
*  <span data-ttu-id="5eabc-398">선언 된 멤버의 범위는 *struct_member_declaration* ([구조체 멤버](structs.md#struct-members))는는 *struct_body* 선언이 발생에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-398">The scope of a member declared by a *struct_member_declaration* ([Struct members](structs.md#struct-members)) is the *struct_body* in which the declaration occurs.</span></span>
*  <span data-ttu-id="5eabc-399">선언 된 멤버의 범위는 *enum_member_declaration* ([열거형 멤버](enums.md#enum-members))는는 *enum_body* 선언이 발생에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-399">The scope of a member declared by an *enum_member_declaration*  ([Enum members](enums.md#enum-members)) is the *enum_body* in which the declaration occurs.</span></span>
*  <span data-ttu-id="5eabc-400">에 선언 된 매개 변수의 범위를 *method_declaration* ([메서드](classes.md#methods))은 합니다 *method_body* 의 *method_declaration*.</span><span class="sxs-lookup"><span data-stu-id="5eabc-400">The scope of a parameter declared in a *method_declaration* ([Methods](classes.md#methods)) is the *method_body* of that *method_declaration*.</span></span>
*  <span data-ttu-id="5eabc-401">에 선언 된 매개 변수의 범위는 *indexer_declaration* ([인덱서](classes.md#indexers))은 합니다 *accessor_declarations* 는 *indexer_declaration*.</span><span class="sxs-lookup"><span data-stu-id="5eabc-401">The scope of a parameter declared in an *indexer_declaration* ([Indexers](classes.md#indexers)) is the *accessor_declarations* of that *indexer_declaration*.</span></span>
*  <span data-ttu-id="5eabc-402">에 선언 된 매개 변수의 범위는 *operator_declaration* ([연산자](classes.md#operators))은 합니다 *블록* 의 *operator_declaration*.</span><span class="sxs-lookup"><span data-stu-id="5eabc-402">The scope of a parameter declared in an *operator_declaration* ([Operators](classes.md#operators)) is the *block* of that *operator_declaration*.</span></span>
*  <span data-ttu-id="5eabc-403">에 선언 된 매개 변수의 범위를 *constructor_declaration* ([인스턴스 생성자](classes.md#instance-constructors))은 합니다 *constructor_initializer* 및 *블록* 해당 *constructor_declaration*합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-403">The scope of a parameter declared in a *constructor_declaration* ([Instance constructors](classes.md#instance-constructors)) is the *constructor_initializer* and *block* of that *constructor_declaration*.</span></span>
*  <span data-ttu-id="5eabc-404">에 선언 된 매개 변수의 범위를 *lambda_expression* ([익명 함수 식](expressions.md#anonymous-function-expressions))은 합니다 *anonymous_function_body* 는 *lambda_ 식*</span><span class="sxs-lookup"><span data-stu-id="5eabc-404">The scope of a parameter declared in a *lambda_expression* ([Anonymous function expressions](expressions.md#anonymous-function-expressions)) is the *anonymous_function_body* of that *lambda_expression*</span></span>
*  <span data-ttu-id="5eabc-405">에 선언 된 매개 변수의 범위는 *anonymous_method_expression* ([익명 함수 식](expressions.md#anonymous-function-expressions))은 합니다 *블록* 는 *anonymous_method _expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-405">The scope of a parameter declared in an *anonymous_method_expression* ([Anonymous function expressions](expressions.md#anonymous-function-expressions)) is the *block* of that *anonymous_method_expression*.</span></span>
*  <span data-ttu-id="5eabc-406">레이블의 범위에서 선언 된를 *labeled_statement* ([문을 레이블이 지정 된](statements.md#labeled-statements))는는 *블록* 선언이 발생에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-406">The scope of a label declared in a *labeled_statement* ([Labeled statements](statements.md#labeled-statements)) is the *block* in which the declaration occurs.</span></span>
*  <span data-ttu-id="5eabc-407">에 선언 된 지역 변수의 범위를 *local_variable_declaration* ([지역 변수 선언](statements.md#local-variable-declarations)) 블록입니다 선언이 발생에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-407">The scope of a local variable declared in a *local_variable_declaration* ([Local variable declarations](statements.md#local-variable-declarations)) is the block in which the declaration occurs.</span></span>
*  <span data-ttu-id="5eabc-408">에 선언 된 지역 변수의 범위를 *switch_block* 의 `switch` 문 ([switch 문](statements.md#the-switch-statement))은 합니다 *switch_block*.</span><span class="sxs-lookup"><span data-stu-id="5eabc-408">The scope of a local variable declared in a *switch_block* of a `switch` statement ([The switch statement](statements.md#the-switch-statement)) is the *switch_block*.</span></span>
*  <span data-ttu-id="5eabc-409">에 선언 된 지역 변수의 범위를 *for_initializer* 의 `for` 문 ([는 문에 대 한](statements.md#the-for-statement))는 합니다 *for_initializer*,  *for_condition*는 *for_iterator*, 및 포함 된 *문* 의 `for` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-409">The scope of a local variable declared in a *for_initializer* of a `for` statement ([The for statement](statements.md#the-for-statement)) is the *for_initializer*, the *for_condition*, the *for_iterator*, and the contained *statement* of the `for` statement.</span></span>
*  <span data-ttu-id="5eabc-410">범위의 지역 상수 선언에 *local_constant_declaration* ([지역 상수 선언](statements.md#local-constant-declarations)) 블록입니다 선언이 발생에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-410">The scope of a local constant declared in a *local_constant_declaration* ([Local constant declarations](statements.md#local-constant-declarations)) is the block in which the declaration occurs.</span></span> <span data-ttu-id="5eabc-411">지역 상수 앞에 오는 텍스트 위치에서 참조 하는 컴파일 시간 오류는 해당 *constant_declarator*합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-411">It is a compile-time error to refer to a local constant in a textual position that precedes its *constant_declarator*.</span></span>
*  <span data-ttu-id="5eabc-412">일부로 선언 된 변수의 범위를 *foreach_statement*, *using_statement*, *lock_statement* 하거나 *query_expression* 는 지정 된 구문의 확장에 의해 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-412">The scope of a variable declared as part of a *foreach_statement*, *using_statement*, *lock_statement* or *query_expression* is determined by the expansion of the given construct.</span></span>

<span data-ttu-id="5eabc-413">네임 스페이스, 클래스, 구조체 또는 열거형 멤버의 범위 내에서 멤버의 선언 앞에 오는 텍스트 위치에서 멤버를 참조 하는 것이 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-413">Within the scope of a namespace, class, struct, or enumeration member it is possible to refer to the member in a textual position that precedes the declaration of the member.</span></span> <span data-ttu-id="5eabc-414">예</span><span class="sxs-lookup"><span data-stu-id="5eabc-414">For example</span></span>
```csharp
class A
{
    void F() {
        i = 1;
    }

    int i = 0;
}
```
<span data-ttu-id="5eabc-415">여기에 사용할 `F` 가리키도록 `i` 먼저 선언 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-415">Here, it is valid for `F` to refer to `i` before it is declared.</span></span>

<span data-ttu-id="5eabc-416">지역 변수의 범위 내는 것은 컴파일 타임 오류 지역 변수 앞에 오는 텍스트 위치를 가리키도록 합니다 *local_variable_declarator* 지역 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-416">Within the scope of a local variable, it is a compile-time error to refer to the local variable in a textual position that precedes the *local_variable_declarator* of the local variable.</span></span> <span data-ttu-id="5eabc-417">예</span><span class="sxs-lookup"><span data-stu-id="5eabc-417">For example</span></span>
```csharp
class A
{
    int i = 0;

    void F() {
        i = 1;                  // Error, use precedes declaration
        int i;
        i = 2;
    }

    void G() {
        int j = (j = 1);        // Valid
    }

    void H() {
        int a = 1, b = ++a;    // Valid
    }
}
```

<span data-ttu-id="5eabc-418">에 `F` 위의 메서드를 첫 번째 할당을 `i` 외부 범위에서 선언 된 필드 참조 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-418">In the `F` method above, the first assignment to `i` specifically does not refer to the field declared in the outer scope.</span></span> <span data-ttu-id="5eabc-419">아니라 참조 지역 변수 및 변수 선언 앞에 오는 텍스트가 때문에 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-419">Rather, it refers to the local variable and it results in a compile-time error because it textually precedes the declaration of the variable.</span></span> <span data-ttu-id="5eabc-420">에 `G` 메서드를 사용 `j` 선언에 대 한 이니셜라이저에서 `j` 를 사용 하 여 앞에 오지 않습니다 때문에 유효를 *local_variable_declarator*합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-420">In the `G` method, the use of `j` in the initializer for the declaration of `j` is valid because the use does not precede the *local_variable_declarator*.</span></span> <span data-ttu-id="5eabc-421">에 `H` 메서드를 선택 하 여 후속 *local_variable_declarator* 이전에 선언 된 지역 변수를 올바르게 가리킵니다 *local_variable_declarator* 동일한  *local_variable_declaration*합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-421">In the `H` method, a subsequent *local_variable_declarator* correctly refers to a local variable declared in an earlier *local_variable_declarator* within the same *local_variable_declaration*.</span></span>

<span data-ttu-id="5eabc-422">지역 변수에 대 한 범위 지정 규칙 식 컨텍스트에서 사용 되는 이름의 의미는 항상 블록 내에서 동일 하 게 보장 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-422">The scoping rules for local variables are designed to guarantee that the meaning of a name used in an expression context is always the same within a block.</span></span> <span data-ttu-id="5eabc-423">지역 변수의 범위는 블록의 끝에만 해당 선언에서에서 확장 한다면 그런 다음 위의 예제에서 첫 번째 할당에서는 인스턴스 변수에 할당 하 고 두 번째 할당도 록 로컬 변수에 할당 블록의 문은 까지로 경우 컴파일 타임 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-423">If the scope of a local variable were to extend only from its declaration to the end of the block, then in the example above, the first assignment would assign to the instance variable and the second assignment would assign to the local variable, possibly leading to compile-time errors if the statements of the block were later to be rearranged.</span></span>

<span data-ttu-id="5eabc-424">블록 내에서 이름의 의미가 이름을 사용 하는 컨텍스트에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-424">The meaning of a name within a block may differ based on the context in which the name is used.</span></span> <span data-ttu-id="5eabc-425">예제</span><span class="sxs-lookup"><span data-stu-id="5eabc-425">In the example</span></span>
```csharp
using System;

class A {}

class Test
{
    static void Main() {
        string A = "hello, world";
        string s = A;                            // expression context

        Type t = typeof(A);                      // type context

        Console.WriteLine(s);                    // writes "hello, world"
        Console.WriteLine(t);                    // writes "A"
    }
}
```
<span data-ttu-id="5eabc-426">이름을 `A` 식 컨텍스트에서 로컬 변수를 참조 하는 데 사용 됩니다 `A` 클래스를 참조 하는 유형 컨텍스트에서 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-426">the name `A` is used in an expression context to refer to the local variable `A` and in a type context to refer to the class `A`.</span></span>

### <a name="name-hiding"></a><span data-ttu-id="5eabc-427">이름 숨기기</span><span class="sxs-lookup"><span data-stu-id="5eabc-427">Name hiding</span></span>

<span data-ttu-id="5eabc-428">엔터티의 범위는 일반적으로 엔터티의 선언 공간 보다 자세한 프로그램 텍스트를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-428">The scope of an entity typically encompasses more program text than the declaration space of the entity.</span></span> <span data-ttu-id="5eabc-429">특히 엔터티 범위 이름이 같은 엔터티를 포함 하는 새 선언 공간을 정의 하는 선언이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-429">In particular, the scope of an entity may include declarations that introduce new declaration spaces containing entities of the same name.</span></span> <span data-ttu-id="5eabc-430">이러한 선언이 발생 되도록 원래 엔터티입니다 ***숨겨진***합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-430">Such declarations cause the original entity to become ***hidden***.</span></span> <span data-ttu-id="5eabc-431">반대로, 엔터티 라고 ***표시*** 하지으로 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-431">Conversely, an entity is said to be ***visible*** when it is not hidden.</span></span>

<span data-ttu-id="5eabc-432">이름 숨기기에 중첩 되 고 상속을 통해 범위와 일치 하는 경우를 통해 범위가 겹치는 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-432">Name hiding occurs when scopes overlap through nesting and when scopes overlap through inheritance.</span></span> <span data-ttu-id="5eabc-433">두 가지 유형의 숨기기의 특징은 다음 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-433">The characteristics of the two types of hiding are described in the following sections.</span></span>

#### <a name="hiding-through-nesting"></a><span data-ttu-id="5eabc-434">통한 숨기기</span><span class="sxs-lookup"><span data-stu-id="5eabc-434">Hiding through nesting</span></span>

<span data-ttu-id="5eabc-435">중첩을 사용한 이름 숨기기 중첩 네임 스페이스 또는 형식 클래스 또는 구조체 내에서 및 매개 변수 및 로컬 변수 선언으로 인해 중첩의 결과로 네임 스페이스 내의 형식으로 인해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-435">Name hiding through nesting can occur as a result of nesting namespaces or types within namespaces, as a result of nesting types within classes or structs, and as a result of parameter and local variable declarations.</span></span>

<span data-ttu-id="5eabc-436">예제</span><span class="sxs-lookup"><span data-stu-id="5eabc-436">In the example</span></span>
```csharp
class A
{
    int i = 0;

    void F() {
        int i = 1;
    }

    void G() {
        i = 1;
    }
}
```
<span data-ttu-id="5eabc-437">내에서 `F` 메서드, 인스턴스 변수 `i` 지역 변수에서 숨겨져 `i`, 하지만 내 합니다 `G` 메서드를 `i` 여전히 인스턴스 변수를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-437">within the `F` method, the instance variable `i` is hidden by the local variable `i`, but within the `G` method, `i` still refers to the instance variable.</span></span>

<span data-ttu-id="5eabc-438">내부 범위에서 이름을 숨깁니다 외부 범위에서 이름, 해당 이름의 오버 로드 된 모든 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-438">When a name in an inner scope hides a name in an outer scope, it hides all overloaded occurrences of that name.</span></span> <span data-ttu-id="5eabc-439">예제</span><span class="sxs-lookup"><span data-stu-id="5eabc-439">In the example</span></span>
```csharp
class Outer
{
    static void F(int i) {}

    static void F(string s) {}

    class Inner
    {
        void G() {
            F(1);              // Invokes Outer.Inner.F
            F("Hello");        // Error
        }

        static void F(long l) {}
    }
}
```
<span data-ttu-id="5eabc-440">호출 `F(1)` 를 호출 하는 `F` 에 선언 된 `Inner` 때문에 모든 외부 항목의 `F` 내부 선언에 의해 숨겨집니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-440">the call `F(1)` invokes the `F` declared in `Inner` because all outer occurrences of `F` are hidden by the inner declaration.</span></span> <span data-ttu-id="5eabc-441">동일한 이유로 호출 `F("Hello")` 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-441">For the same reason, the call `F("Hello")` results in a compile-time error.</span></span>

#### <a name="hiding-through-inheritance"></a><span data-ttu-id="5eabc-442">상속을 통해 숨기기</span><span class="sxs-lookup"><span data-stu-id="5eabc-442">Hiding through inheritance</span></span>

<span data-ttu-id="5eabc-443">이름 숨기기 상속을 통해 클래스 또는 구조체에는 기본 클래스에서 상속 된 이름을 다시 선언할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-443">Name hiding through inheritance occurs when classes or structs redeclare names that were inherited from base classes.</span></span> <span data-ttu-id="5eabc-444">이 유형의 이름 숨기기 다음 형식 중 하나를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-444">This type of name hiding takes one of the following forms:</span></span>

*  <span data-ttu-id="5eabc-445">상수, 필드, 속성, 이벤트 또는 클래스나 구조체에 도입 된 형식 이름이 같은 모든 기본 클래스 멤버를 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-445">A constant, field, property, event, or type introduced in a class or struct hides all base class members with the same name.</span></span>
*  <span data-ttu-id="5eabc-446">클래스 또는 구조체에 도입 된 메서드는 동일한 이름의 모든 메서드가 아닌 기본 클래스 멤버와 동일한 서명이 (메서드 이름 및 매개 변수 수, 한정자 및 형식)를 사용 하 여 모든 기본 클래스 메서드를 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-446">A method introduced in a class or struct hides all non-method base class members with the same name, and all base class methods with the same signature (method name and parameter count, modifiers, and types).</span></span>
*  <span data-ttu-id="5eabc-447">클래스 또는 구조체에서 인덱서 (매개 변수 개수 및 형식) 동일한 서명 사용 하 여 모든 기본 클래스 인덱서를 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-447">An indexer introduced in a class or struct hides all base class indexers with the same signature (parameter count and types).</span></span>

<span data-ttu-id="5eabc-448">연산자 선언을 제어 하는 규칙 ([연산자](classes.md#operators)) 기본 클래스의 연산자와 동일한 서명 사용 하 여 연산자를 선언 하는 파생된 클래스에 대 한 불가능 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-448">The rules governing operator declarations ([Operators](classes.md#operators)) make it impossible for a derived class to declare an operator with the same signature as an operator in a base class.</span></span> <span data-ttu-id="5eabc-449">따라서 연산자 숨기지 않습니다 서로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-449">Thus, operators never hide one another.</span></span>

<span data-ttu-id="5eabc-450">외부 범위에서 이름 숨기기 달리 상속된 된 범위에서 액세스 가능한 이름을 숨기면 경고 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-450">Contrary to hiding a name from an outer scope, hiding an accessible name from an inherited scope causes a warning to be reported.</span></span> <span data-ttu-id="5eabc-451">예제</span><span class="sxs-lookup"><span data-stu-id="5eabc-451">In the example</span></span>
```csharp
class Base
{
    public void F() {}
}

class Derived: Base
{
    public void F() {}        // Warning, hiding an inherited name
}
```
<span data-ttu-id="5eabc-452">선언의 `F` 에서 `Derived` 보고 되는 경고를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-452">the declaration of `F` in `Derived` causes a warning to be reported.</span></span> <span data-ttu-id="5eabc-453">상속된 된 이름을 숨기기 이므로 하지 오류가 발생 하는 기본 클래스의 별도 진화를 방해는입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-453">Hiding an inherited name is specifically not an error, since that would preclude separate evolution of base classes.</span></span> <span data-ttu-id="5eabc-454">예를 들어 위와 같은 상황이 발생 하기 때문에 이후 버전의 `Base` 도입을 `F` 클래스의 이전 버전에 없는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-454">For example, the above situation might have come about because a later version of `Base` introduced an `F` method that wasn't present in an earlier version of the class.</span></span> <span data-ttu-id="5eabc-455">위와 같은 상황이 오류가 같다고, 다음 변경 내용이 다른 버전의 클래스 라이브러리의 기본 클래스 발생할 수 있습니다 파생된 클래스를 사용할 수 없게 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-455">Had the above situation been an error, then any change made to a base class in a separately versioned class library could potentially cause derived classes to become invalid.</span></span>

<span data-ttu-id="5eabc-456">상속된 된 이름을 숨기기 인해 경고를 사용 하 여 제거할 수는 `new` 한정자:</span><span class="sxs-lookup"><span data-stu-id="5eabc-456">The warning caused by hiding an inherited name can be eliminated through use of the `new` modifier:</span></span>
```csharp
class Base
{
    public void F() {}
}

class Derived: Base
{
    new public void F() {}
}
```

<span data-ttu-id="5eabc-457">`new` 한정자가 나타내는 합니다 `F` 에서 `Derived` 상속 된 멤버를 숨기려면 것 실제로 고 "new"입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-457">The `new` modifier indicates that the `F` in `Derived` is "new", and that it is indeed intended to hide the inherited member.</span></span>

<span data-ttu-id="5eabc-458">새 멤버의 선언에는 새 멤버의 범위 내 에서만 상속 된 멤버를 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-458">A declaration of a new member hides an inherited member only within the scope of the new member.</span></span>

```csharp
class Base
{
    public static void F() {}
}

class Derived: Base
{
    new private static void F() {}    // Hides Base.F in Derived only
}

class MoreDerived: Derived
{
    static void G() { F(); }          // Invokes Base.F
}
```

<span data-ttu-id="5eabc-459">선언의 위의 예에서 `F` 에 `Derived` 숨깁니다 합니다 `F` 에서 상속 된는 `Base`, 하지만 새 `F` 에서 `Derived` 개인 액세스 권한이 해당 범위로 확장 되지 않습니다 `MoreDerived` .</span><span class="sxs-lookup"><span data-stu-id="5eabc-459">In the example above, the declaration of `F` in `Derived` hides the `F` that was inherited from `Base`, but since the new `F` in `Derived` has private access, its scope does not extend to `MoreDerived`.</span></span> <span data-ttu-id="5eabc-460">따라서 호출 `F()` 에 `MoreDerived.G` 유효 하 고 호출 `Base.F`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-460">Thus, the call `F()` in `MoreDerived.G` is valid and will invoke `Base.F`.</span></span>

## <a name="namespace-and-type-names"></a><span data-ttu-id="5eabc-461">Namespace 및 형식 이름</span><span class="sxs-lookup"><span data-stu-id="5eabc-461">Namespace and type names</span></span>

<span data-ttu-id="5eabc-462">C# 프로그램의 여러 컨텍스트 필요는 *namespace_name* 또는 *type_name* 를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-462">Several contexts in a C# program require a *namespace_name* or a *type_name* to be specified.</span></span>

```antlr
namespace_name
    : namespace_or_type_name
    ;

type_name
    : namespace_or_type_name
    ;

namespace_or_type_name
    : identifier type_argument_list?
    | namespace_or_type_name '.' identifier type_argument_list?
    | qualified_alias_member
    ;
```

<span data-ttu-id="5eabc-463">A *namespace_name* 되는 *namespace_or_type_name* 네임 스페이스를 참조 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-463">A *namespace_name* is a *namespace_or_type_name* that refers to a namespace.</span></span> <span data-ttu-id="5eabc-464">아래 설명 된 대로 확인을 수행 합니다 *namespace_or_type_name* 의 *namespace_name* 네임 스페이스를 참조 해야 합니다 또는 그렇지 않으면 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-464">Following resolution as described below, the *namespace_or_type_name* of a *namespace_name* must refer to a namespace, or otherwise a compile-time error occurs.</span></span> <span data-ttu-id="5eabc-465">형식 인수 없이 ([형식 인수가](types.md#type-arguments))에 있을 수는 *namespace_name* (형식 형식 인수를 가질 수 있음)만 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-465">No type arguments ([Type arguments](types.md#type-arguments)) can be present in a *namespace_name* (only types can have type arguments).</span></span>

<span data-ttu-id="5eabc-466">A *type_name* 되는 *namespace_or_type_name* 형식을 참조 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-466">A *type_name* is a *namespace_or_type_name* that refers to a type.</span></span> <span data-ttu-id="5eabc-467">아래 설명 된 대로 확인을 수행를 *namespace_or_type_name* 의 *type_name* 형식을 참조 해야 합니다 또는 그렇지 않으면 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-467">Following resolution as described below, the *namespace_or_type_name* of a *type_name* must refer to a type, or otherwise a compile-time error occurs.</span></span>

<span data-ttu-id="5eabc-468">경우는 *namespace_or_type_name* 멤버인 정규화-별칭-해당 의미는에 설명 된 대로 [Namespace 별칭 한정자](namespaces.md#namespace-alias-qualifiers)합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-468">If the *namespace_or_type_name* is a qualified-alias-member its meaning is as described in [Namespace alias qualifiers](namespaces.md#namespace-alias-qualifiers).</span></span> <span data-ttu-id="5eabc-469">그렇지 않은 경우는 *namespace_or_type_name* 에 네 가지 형태 중 하나:</span><span class="sxs-lookup"><span data-stu-id="5eabc-469">Otherwise, a *namespace_or_type_name* has one of four forms:</span></span>

*  `I`
*  `I<A1, ..., Ak>`
*  `N.I`
*  `N.I<A1, ..., Ak>`

<span data-ttu-id="5eabc-470">여기서 `I` 는 단일 식별자 `N` 되는 *namespace_or_type_name* 및 `<A1, ..., Ak>` 선택적 *type_argument_list*합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-470">where `I` is a single identifier, `N` is a *namespace_or_type_name* and `<A1, ..., Ak>` is an optional *type_argument_list*.</span></span> <span data-ttu-id="5eabc-471">없는 경우 *type_argument_list* 가 지정 하는 것이 좋습니다 `k` 0입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-471">When no *type_argument_list* is specified, consider `k` to be zero.</span></span>

<span data-ttu-id="5eabc-472">의미는 *namespace_or_type_name* 다음과 같이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-472">The meaning of a *namespace_or_type_name* is determined as follows:</span></span>

*   <span data-ttu-id="5eabc-473">경우는 *namespace_or_type_name* 형식인 `I` 또는 양식의 `I<A1, ..., Ak>`:</span><span class="sxs-lookup"><span data-stu-id="5eabc-473">If the *namespace_or_type_name* is of the form `I` or of the form `I<A1, ..., Ak>`:</span></span>
    * <span data-ttu-id="5eabc-474">하는 경우 `K` 가 0 및 *namespace_or_type_name* 제네릭 메서드 선언 내에 나타납니다 ([메서드](classes.md#methods)) 및 해당 선언 형식 매개 변수를 포함 하는 경우 ([형식 매개 변수](classes.md#type-parameters)) 이름의 `I`, 해당 *namespace_or_type_name* 해당 형식 매개 변수를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-474">If `K` is zero and the *namespace_or_type_name* appears within a generic method declaration ([Methods](classes.md#methods)) and if that declaration includes a type parameter ([Type parameters](classes.md#type-parameters)) with name `I`, then the *namespace_or_type_name* refers to that type parameter.</span></span>
    * <span data-ttu-id="5eabc-475">그렇지 않은 경우, 합니다 *namespace_or_type_name* 형식 선언에서 다음 각 인스턴스 유형에 대해 나타납니다 `T` ([인스턴스 유형을](classes.md#the-instance-type)) 해당 형식의 인스턴스를 사용 하 여 시작 선언 및 (있는 경우) 각 바깥쪽 클래스 또는 구조체 선언의 인스턴스 형식을 사용 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-475">Otherwise, if the *namespace_or_type_name* appears within a type declaration, then for each instance type `T` ([The instance type](classes.md#the-instance-type)), starting with the instance type of that type declaration and continuing with the instance type of each enclosing class or struct declaration (if any):</span></span>
        * <span data-ttu-id="5eabc-476">하는 경우 `K` 0 이며 선언의 `T` 이름의 형식 매개 변수가 포함 `I`, 해당 *namespace_or_type_name* 해당 형식 매개 변수를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-476">If `K` is zero and the declaration of `T` includes a type parameter with name `I`, then the *namespace_or_type_name* refers to that type parameter.</span></span>
        * <span data-ttu-id="5eabc-477">그렇지 않은 경우를 *namespace_or_type_name* 형식 선언의 본문 내에 표시 하 고 `T` 이름의 중첩된 액세스할 수 있는 형식을 포함 해당 기본 형식 또는 `I` 및 `K` 형식 매개 변수 해당 *namespace_or_type_name* 지정 된 형식 인수를 사용 하 여 생성 하는 형식을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-477">Otherwise, if the *namespace_or_type_name* appears within the body of the type declaration, and `T` or any of its base types contain a nested accessible type having name `I` and `K` type parameters, then the *namespace_or_type_name* refers to that type constructed with the given type arguments.</span></span> <span data-ttu-id="5eabc-478">이러한 형식이 둘 이상 있으면 더 많이 파생 된 형식 내에서 선언 된 형식이 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-478">If there is more than one such type, the type declared within the more derived type is selected.</span></span> <span data-ttu-id="5eabc-479">형식이 아닌 멤버 (상수, 필드, 메서드, 속성, 인덱서, 연산자, 인스턴스 생성자, 소멸자 및 정적 생성자) 및 다양 한 개수의 형식 매개 변수를 사용 하 여 형식 멤버의 의미를 결정할 때 무시 됩니다는 *namespace_or_type_name*합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-479">Note that non-type members (constants, fields, methods, properties, indexers, operators, instance constructors, destructors, and static constructors) and type members with a different number of type parameters are ignored when determining the meaning of the *namespace_or_type_name*.</span></span>
    * <span data-ttu-id="5eabc-480">이전 단계를 각 네임 스페이스에 대 한 다음 실패 한 경우 `N`네임 스페이스를 사용 하 여 시작 합니다 *namespace_or_type_name* 각 바깥쪽 네임 스페이스 (있을 경우)를 사용 하 여 계속 해 서 끝나는 발생 합니다 전역 네임 스페이스는 엔터티를 찾을 때까지 다음 단계를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-480">If the previous steps were unsuccessful then, for each namespace `N`, starting with the namespace in which the *namespace_or_type_name* occurs, continuing with each enclosing namespace (if any), and ending with the global namespace, the following steps are evaluated until an entity is located:</span></span>
        * <span data-ttu-id="5eabc-481">경우 `K` 가 0 및 `I` 네임 스페이스의 이름은 `N`, 다음:</span><span class="sxs-lookup"><span data-stu-id="5eabc-481">If `K` is zero and `I` is the name of a namespace in `N`, then:</span></span>
            * <span data-ttu-id="5eabc-482">경우 위치 위치는 *namespace_or_type_name* 발생에 대 한 네임 스페이스 선언을 괄호로 묶여 `N` 네임 스페이스 선언을 포함 하는 *extern_alias_directive* 또는 *using_alias_directive* 이름을 연결 하는 `I` 형식 또는 네임 스페이스를 사용 하 여 해당 *namespace_or_type_name* 모호 하 고 컴파일 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-482">If the location where the *namespace_or_type_name* occurs is enclosed by a namespace declaration for `N` and the namespace declaration contains an *extern_alias_directive* or *using_alias_directive* that associates the name `I` with a namespace or type, then the *namespace_or_type_name* is ambiguous and a compile-time error occurs.</span></span>
            * <span data-ttu-id="5eabc-483">이 고, 그렇지 합니다 *namespace_or_type_name* 라는 네임 스페이스 참조 `I` 에서 `N`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-483">Otherwise, the *namespace_or_type_name* refers to the namespace named `I` in `N`.</span></span>
        * <span data-ttu-id="5eabc-484">그렇지 않은 경우, `N` 이름의 액세스할 수 있는 형식이 포함 되어 `I` 및 `K` 다음 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-484">Otherwise, if `N` contains an accessible type having name `I` and `K` type parameters, then:</span></span>
            * <span data-ttu-id="5eabc-485">하는 경우 `K` 0 및 위치는 여기서는 *namespace_or_type_name* 발생에 대 한 네임 스페이스 선언을 괄호로 묶여 `N` 네임 스페이스 선언을 포함 하 고는 *extern_alias_directive*  나 *using_alias_directive* 이름을 연결 하는 `I` 네임 스페이스 또는 형식을 사용 하 여 해당 *namespace_or_type_name* 모호 하며 컴파일 타임에는 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-485">If `K` is zero and the location where the *namespace_or_type_name* occurs is enclosed by a namespace declaration for `N` and the namespace declaration contains an *extern_alias_directive* or *using_alias_directive* that associates the name `I` with a namespace or type, then the *namespace_or_type_name* is ambiguous and a compile-time error occurs.</span></span>
            * <span data-ttu-id="5eabc-486">그렇지 않은 경우는 *namespace_or_type_name* 지정 된 형식 인수를 사용 하 여 생성 된 형식을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-486">Otherwise, the *namespace_or_type_name* refers to the type constructed with the given type arguments.</span></span>
        * <span data-ttu-id="5eabc-487">그렇지 않은 경우, 위치 여기서 합니다 *namespace_or_type_name* 발생에 대 한 네임 스페이스 선언을 괄호로 묶여 `N`:</span><span class="sxs-lookup"><span data-stu-id="5eabc-487">Otherwise, if the location where the *namespace_or_type_name* occurs is enclosed by a namespace declaration for `N`:</span></span>
            * <span data-ttu-id="5eabc-488">하는 경우 `K` 이 0이 고 네임 스페이스 선언에는 *extern_alias_directive* 또는 *using_alias_directive* 이름을 연결 하는 `I` 가져온된 네임 스페이스를 사용 하 여 또는 형식, 해당 *namespace_or_type_name* 해당 네임 스페이스 또는 형식을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-488">If `K` is zero and the namespace declaration contains an *extern_alias_directive* or *using_alias_directive* that associates the name `I` with an imported namespace or type, then the *namespace_or_type_name* refers to that namespace or type.</span></span>
            * <span data-ttu-id="5eabc-489">네임 스페이스 및 형식 선언에서 가져온 경우는 *using_namespace_directive*s 및 *using_alias_directive*네임 스페이스 선언 중 하나만 액세스할 수 있는 형식을 포함 이름의 `I` 하 고 `K` 매개 변수를 입력 하면 *namespace_or_type_name* 지정 된 형식 인수를 사용 하 여 생성 하는 형식을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-489">Otherwise, if the namespaces and type declarations imported by the *using_namespace_directive*s and *using_alias_directive*s of the namespace declaration contain exactly one accessible type having name `I` and `K` type parameters, then the *namespace_or_type_name* refers to that type constructed with the given type arguments.</span></span>
            * <span data-ttu-id="5eabc-490">네임 스페이스 및 형식 선언에서 가져온 경우는 *using_namespace_directive*s 및 *using_alias_directive*네임 스페이스 선언의 s 둘 이상의 액세스할 수 있는 형식을 포함 이름의 `I` 및 `K` 매개 변수를 입력 하면 *namespace_or_type_name* 모호 합니다. 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-490">Otherwise, if the namespaces and type declarations imported by the *using_namespace_directive*s and *using_alias_directive*s of the namespace declaration contain more than one accessible type having name `I` and `K` type parameters, then the *namespace_or_type_name* is ambiguous and an error occurs.</span></span>
    * <span data-ttu-id="5eabc-491">이 고, 그렇지 합니다 *namespace_or_type_name* 가 정의 되지 않은 하 고 컴파일 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-491">Otherwise, the *namespace_or_type_name* is undefined and a compile-time error occurs.</span></span>
*  <span data-ttu-id="5eabc-492">이 고, 그렇지 합니다 *namespace_or_type_name* 형식인 `N.I` 또는 양식의 `N.I<A1, ..., Ak>`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-492">Otherwise, the *namespace_or_type_name* is of the form `N.I` or of the form `N.I<A1, ..., Ak>`.</span></span> <span data-ttu-id="5eabc-493">`N` 먼저 됨을 *namespace_or_type_name*합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-493">`N` is first resolved as a *namespace_or_type_name*.</span></span> <span data-ttu-id="5eabc-494">하는 경우의 해결 방법을 `N` 정상적이 지 않습니다 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-494">If the resolution of `N` is not successful, a compile-time error occurs.</span></span> <span data-ttu-id="5eabc-495">그렇지 않으면 `N.I` 또는 `N.I<A1, ..., Ak>` 같이 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-495">Otherwise, `N.I` or `N.I<A1, ..., Ak>` is resolved as follows:</span></span>
    * <span data-ttu-id="5eabc-496">경우 `K` 0 및 `N` 네임 스페이스를 참조 하 고 `N` 이름의 중첩된 된 네임 스페이스를 포함 `I`, 해당 *namespace_or_type_name* 중첩 된 네임 스페이스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-496">If `K` is zero and `N` refers to a namespace and `N` contains a nested namespace with name `I`, then the *namespace_or_type_name* refers to that nested namespace.</span></span>
    * <span data-ttu-id="5eabc-497">그렇지 `N` 네임 스페이스를 참조 및 `N` 이름의 액세스할 수 있는 형식이 포함 되어 `I` 및 `K` 매개 변수를 입력 하면 *namespace_or_type_name* 해당 형식을 참조 지정 된 형식 인수를 사용 하 여 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-497">Otherwise, if `N` refers to a namespace and `N` contains an accessible type having name `I` and `K` type parameters, then the *namespace_or_type_name* refers to that type constructed with the given type arguments.</span></span>
    * <span data-ttu-id="5eabc-498">그렇지 않은 경우, `N` (가능한 경우 생성 된) 클래스 또는 구조체 형식을 참조 및 `N` 이름의 중첩된 액세스할 수 있는 형식을 포함 한 모든 기본 클래스 `I` 하 고 `K` 매개 변수를 입력 하면 *네임 스페이스 _or_type_name* 지정 된 형식 인수를 사용 하 여 생성 하는 형식을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-498">Otherwise, if `N` refers to a (possibly constructed) class or struct type and `N` or any of its base classes contain a nested accessible type having name `I` and `K` type parameters, then the *namespace_or_type_name* refers to that type constructed with the given type arguments.</span></span> <span data-ttu-id="5eabc-499">이러한 형식이 둘 이상 있으면 더 많이 파생 된 형식 내에서 선언 된 형식이 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-499">If there is more than one such type, the type declared within the more derived type is selected.</span></span> <span data-ttu-id="5eabc-500">경우의 의미를 확인 `N.I` 결정 하는 기본 클래스 지정을 확인 하는 일부로 `N` 직접 기본 클래스의 다음 `N` 개체로 간주 됩니다 ([기본 클래스](classes.md#base-classes)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-500">Note that if the meaning of `N.I` is being determined as part of resolving the base class specification of `N` then the direct base class of `N` is considered to be object ([Base classes](classes.md#base-classes)).</span></span>
    * <span data-ttu-id="5eabc-501">이 고, 그렇지 `N.I` 잘못 된 *namespace_or_type_name*, 컴파일 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-501">Otherwise, `N.I` is an invalid *namespace_or_type_name*, and a compile-time error occurs.</span></span>

<span data-ttu-id="5eabc-502">A *namespace_or_type_name* 정적 클래스를 참조 하도록 허용 됩니다 ([정적 클래스](classes.md#static-classes)) 경우에만</span><span class="sxs-lookup"><span data-stu-id="5eabc-502">A *namespace_or_type_name* is permitted to reference a static class ([Static classes](classes.md#static-classes)) only if</span></span>

*  <span data-ttu-id="5eabc-503">*namespace_or_type_name* 은 합니다 `T` 에 *namespace_or_type_name* 폼의 `T.I`, 또는</span><span class="sxs-lookup"><span data-stu-id="5eabc-503">The *namespace_or_type_name* is the `T` in a *namespace_or_type_name* of the form `T.I`, or</span></span>
*  <span data-ttu-id="5eabc-504">*namespace_or_type_name* 는 `T` 에 *typeof_expression* ([인수 목록](expressions.md#argument-lists)1) 형식의 `typeof(T)`.</span><span class="sxs-lookup"><span data-stu-id="5eabc-504">The *namespace_or_type_name* is the `T` in a *typeof_expression* ([Argument lists](expressions.md#argument-lists)1) of the form `typeof(T)`.</span></span>

### <a name="fully-qualified-names"></a><span data-ttu-id="5eabc-505">정규화 된 이름</span><span class="sxs-lookup"><span data-stu-id="5eabc-505">Fully qualified names</span></span>

<span data-ttu-id="5eabc-506">모든 네임 스페이스 및 형식에는 ***정규화 된 이름을***를 고유 하 게 식별 하는 네임 스페이스 또는 다른 모든 형식과 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-506">Every namespace and type has a ***fully qualified name***, which uniquely identifies the namespace or type amongst all others.</span></span> <span data-ttu-id="5eabc-507">형식 또는 네임 스페이스의 정규화 된 이름을 `N` 다음과 같이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-507">The fully qualified name of a namespace or type `N` is determined as follows:</span></span>

*  <span data-ttu-id="5eabc-508">하는 경우 `N` 멤버인 정규화 된 이름은 전역 네임 스페이스는 `N`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-508">If `N` is a member of the global namespace, its fully qualified name is `N`.</span></span>
*  <span data-ttu-id="5eabc-509">그렇지 않으면 해당 정규화 된 이름을 `S.N`여기서 `S` 네임 스페이스 또는 형식의는 정규화 된 이름인 `N` 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-509">Otherwise, its fully qualified name is `S.N`, where `S` is the fully qualified name of the namespace or type in which `N` is declared.</span></span>

<span data-ttu-id="5eabc-510">즉, 정규화 된 이름의 `N` 로 안내 하는 식별자의 전체 계층적 경로인 `N`전역 네임 스페이스에서 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-510">In other words, the fully qualified name of `N` is the complete hierarchical path of identifiers that lead to `N`, starting from the global namespace.</span></span> <span data-ttu-id="5eabc-511">형식 또는 네임 스페이스의 모든 멤버 고유 이름이 있어야 하므로 항상 형식 또는 네임 스페이스의 정규화 된 이름을 고유함을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-511">Because every member of a namespace or type must have a unique name, it follows that the fully qualified name of a namespace or type is always unique.</span></span>

<span data-ttu-id="5eabc-512">아래 예제에는 연결 된 해당 정규화 된 이름이 여러 네임 스페이스 및 형식 선언을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-512">The example below shows several namespace and type declarations along with their associated fully qualified names.</span></span>
```csharp
class A {}                // A

namespace X               // X
{
    class B               // X.B
    {
        class C {}        // X.B.C
    }

    namespace Y           // X.Y
    {
        class D {}        // X.Y.D
    }
}

namespace X.Y             // X.Y
{
    class E {}            // X.Y.E
}
```

## <a name="automatic-memory-management"></a><span data-ttu-id="5eabc-513">자동 메모리 관리</span><span class="sxs-lookup"><span data-stu-id="5eabc-513">Automatic memory management</span></span>

<span data-ttu-id="5eabc-514">C# 개발자가 수동으로 할당 하 고 개체에 의해 점유 메모리에서 해제는 자동 메모리 관리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-514">C# employs automatic memory management, which frees developers from manually allocating and freeing the memory occupied by objects.</span></span> <span data-ttu-id="5eabc-515">자동 메모리 관리 정책이 구현 되는 ***가비지 수집기***합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-515">Automatic memory management policies are implemented by a ***garbage collector***.</span></span> <span data-ttu-id="5eabc-516">개체의 메모리 관리 수명 주기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-516">The memory management life cycle of an object is as follows:</span></span>

1. <span data-ttu-id="5eabc-517">개체를 만들 때 할당 된 메모리, 생성자를 실행 및 개체 라이브 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-517">When the object is created, memory is allocated for it, the constructor is run, and the object is considered live.</span></span>
2. <span data-ttu-id="5eabc-518">개체 또는 그 일부를 실행 가능한 모든 연속 하 여 액세스할 수 없으면, 소멸자를 실행 이외의 개체 간주 되 더 이상 사용에서 고 소멸 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-518">If the object, or any part of it, cannot be accessed by any possible continuation of execution, other than the running of destructors, the object is considered no longer in use, and it becomes eligible for destruction.</span></span> <span data-ttu-id="5eabc-519">C# 컴파일러와 가비지 수집기가 개체에 대 한 참조는 나중에 사용할 수 있습니다를 확인 하는 코드를 분석할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-519">The C# compiler and the garbage collector may choose to analyze code to determine which references to an object may be used in the future.</span></span> <span data-ttu-id="5eabc-520">예를 들어 범위 내에 있는 로컬 변수는 개체에 기존 참조 하지만 해당 로컬 변수는 프로시저에서 가리킨 현재 실행의 실행 가능한 모든 연속에서 참조 되지 않는 경우 가비지 수집기가 될 수 있습니다 (하지만 아닙니다. 에 필요) 사용에서을 더 이상 개체를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-520">For instance, if a local variable that is in scope is the only existing reference to an object, but that local variable is never referred to in any possible continuation of execution from the current execution point in the procedure, the garbage collector may (but is not required to) treat the object as no longer in use.</span></span>
3. <span data-ttu-id="5eabc-521">개체를 소멸할 수 있으면 나중에 지정 되지 않은 몇 가지 시간 소멸자 ([소멸자](classes.md#destructors)) (있는 경우) 개체가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-521">Once the object is eligible for destruction, at some unspecified later time the destructor ([Destructors](classes.md#destructors)) (if any) for the object is run.</span></span> <span data-ttu-id="5eabc-522">정상적인 소멸자는 개체에 대 한 구현 관련 Api에는이 동작을 재정의할 수 수 있지만 한 번만 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-522">Under normal circumstances the destructor for the object is run once only, though implementation-specific APIs may allow this behavior to be overridden.</span></span>
4. <span data-ttu-id="5eabc-523">개체 또는 그 일부를 실행, 소멸자를 실행 하는 등의 가능한 모든 연속 하 여 액세스할 수 없는 경우 개체에 대 한 소멸자가 실행 되 면 개체 액세스할 수 없는 것으로 간주 됩니다 및 개체 컬렉션에 대 한 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-523">Once the destructor for an object is run, if that object, or any part of it, cannot be accessed by any possible continuation of execution, including the running of destructors, the object is considered inaccessible and the object becomes eligible for collection.</span></span>
5. <span data-ttu-id="5eabc-524">마지막으로, 특정 시간에 개체 컬렉션을 사용할 수 있게 되 면 가비지 수집기가 메모리를 해제 개체와 관련 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-524">Finally, at some time after the object becomes eligible for collection, the garbage collector frees the memory associated with that object.</span></span>

<span data-ttu-id="5eabc-525">가비지 수집기는 개체 사용에 대 한 정보를 유지 관리 하 고 개체와 개체가 위치를 변경 하는 더 이상 사용에서 되거나 액세스할 수 없는 경우 새로 생성된 된 개체를 찾을 수 있는 메모리 위치와 같은 메모리 관리 의사 결정을 확인 합니다.이 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-525">The garbage collector maintains information about object usage, and uses this information to make memory management decisions, such as where in memory to locate a newly created object, when to relocate an object, and when an object is no longer in use or inaccessible.</span></span>

<span data-ttu-id="5eabc-526">가비지 수집기의 존재 여부를 가정 하는 다른 언어와 마찬가지로 C#는 설계 되어 가비지 수집기는 다양 한 범위의 메모리 관리 정책 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-526">Like other languages that assume the existence of a garbage collector, C# is designed so that the garbage collector may implement a wide range of memory management policies.</span></span> <span data-ttu-id="5eabc-527">예를 들어 C# 필요가 없습니다 소멸자를 실행 하는 것에 자격이 되는 개체는 수집 수 또는 특정 순서에 관계 없이 또는 특정 스레드에서 소멸자를 실행 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-527">For instance, C# does not require that destructors be run or that objects be collected as soon as they are eligible, or that destructors be run in any particular order, or on any particular thread.</span></span>

<span data-ttu-id="5eabc-528">가비지 수집의 동작을 제어할 수 클래스에서 정적 메서드를 통해 어느 정도 `System.GC`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-528">The behavior of the garbage collector can be controlled, to some degree, via static methods on the class `System.GC`.</span></span> <span data-ttu-id="5eabc-529">이 클래스는 소멸자 수 실행 (또는 실행 되지)가 발생 하는 컬렉션을 요청에 사용할 수 있습니다 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-529">This class can be used to request a collection to occur, destructors to be run (or not run), and so forth.</span></span>

<span data-ttu-id="5eabc-530">가비지 수집기가 개체를 수집 하 고 소멸자를 실행 하는 경우 유연 하 게 결정할 허용 하므로 표준에 맞는 구현에 다음 코드에 의해 표시 되는 다른 출력을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-530">Since the garbage collector is allowed wide latitude in deciding when to collect objects and run destructors, a conforming implementation may produce output that differs from that shown by the following code.</span></span> <span data-ttu-id="5eabc-531">프로그램</span><span class="sxs-lookup"><span data-stu-id="5eabc-531">The program</span></span>
```csharp
using System;

class A
{
    ~A() {
        Console.WriteLine("Destruct instance of A");
    }
}

class B
{
    object Ref;

    public B(object o) {
        Ref = o;
    }

    ~B() {
        Console.WriteLine("Destruct instance of B");
    }
}

class Test
{
    static void Main() {
        B b = new B(new A());
        b = null;
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```
<span data-ttu-id="5eabc-532">클래스의 인스턴스를 만듭니다 `A` 클래스의 인스턴스 `B`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-532">creates an instance of class `A` and an instance of class `B`.</span></span> <span data-ttu-id="5eabc-533">이러한 개체가 가비지 수집에 적합 하 게 될 때 변수의 `b` 값이 할당 됩니다 `null`아니므로이 시간 후에 액세스할 모든 사용자가 작성 한 코드에 대 한 가능한, 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-533">These objects become eligible for garbage collection when the variable `b` is assigned the value `null`, since after this time it is impossible for any user-written code to access them.</span></span> <span data-ttu-id="5eabc-534">출력 될 수 있음</span><span class="sxs-lookup"><span data-stu-id="5eabc-534">The output could be either</span></span>
```
Destruct instance of A
Destruct instance of B
```
<span data-ttu-id="5eabc-535">또는</span><span class="sxs-lookup"><span data-stu-id="5eabc-535">or</span></span>
```
Destruct instance of B
Destruct instance of A
```
<span data-ttu-id="5eabc-536">언어 순서 없는 제약 조건을 설정 때문에 개체에서 가비지 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-536">because the language imposes no constraints on the order in which objects are garbage collected.</span></span>

<span data-ttu-id="5eabc-537">경우에 따라 "를 소멸할 수" 및 "컬렉션에 대 한 적격"의 차이 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-537">In subtle cases, the distinction between "eligible for destruction" and "eligible for collection" can be important.</span></span> <span data-ttu-id="5eabc-538">예를 들어 개체에 적용된</span><span class="sxs-lookup"><span data-stu-id="5eabc-538">For example,</span></span>
```csharp
using System;

class A
{
    ~A() {
        Console.WriteLine("Destruct instance of A");
    }

    public void F() {
        Console.WriteLine("A.F");
        Test.RefA = this;
    }
}

class B
{
    public A Ref;

    ~B() {
        Console.WriteLine("Destruct instance of B");
        Ref.F();
    }
}

class Test
{
    public static A RefA;
    public static B RefB;

    static void Main() {
        RefB = new B();
        RefA = new A();
        RefB.Ref = RefA;
        RefB = null;
        RefA = null;

        // A and B now eligible for destruction
        GC.Collect();
        GC.WaitForPendingFinalizers();

        // B now eligible for collection, but A is not
        if (RefA != null)
            Console.WriteLine("RefA is not null");
    }
}
```

<span data-ttu-id="5eabc-539">위의 프로그램에서 가비지 수집기의 소멸자를 실행 하 고 싶다면 `A` 소멸자 전에 `B`,이 프로그램의 출력 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="5eabc-539">In the above program, if the garbage collector chooses to run the destructor of `A` before the destructor of `B`, then the output of this program might be:</span></span>
```
Destruct instance of A
Destruct instance of B
A.F
RefA is not null
```

<span data-ttu-id="5eabc-540">인스턴스의 `A` 사용 되지 않았습니다 및 `A`의 소멸자가 실행 되는 수의 메서드에 대 한 `A` (이 예제의 경우 `F`) 다른 소멸자에서 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-540">Note that although the instance of `A` was not in use and `A`'s destructor was run, it is still possible for methods of `A` (in this case, `F`) to be called from another destructor.</span></span> <span data-ttu-id="5eabc-541">또한 참고를 소멸자는 실행이 다시 주 프로그램에서 사용할 수 있게 하는 개체를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-541">Also, note that running of a destructor may cause an object to become usable from the mainline program again.</span></span> <span data-ttu-id="5eabc-542">이 예에서 실행 `B`소멸자 발생의 인스턴스에 `A` 는 이전에 사용 되지 않으면 라이브 참조에서 액세스할 수 있게 `Test.RefA`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-542">In this case, the running of `B`'s destructor caused an instance of `A` that was previously not in use to become accessible from the live reference `Test.RefA`.</span></span> <span data-ttu-id="5eabc-543">호출한 후 `WaitForPendingFinalizers`, 인스턴스의 `B` 인스턴스가 되지만 컬렉션에 적합 한 `A` 를 참조 하지 않으면 `Test.RefA`합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-543">After the call to `WaitForPendingFinalizers`, the instance of `B` is eligible for collection, but the instance of `A` is not, because of the reference `Test.RefA`.</span></span>

<span data-ttu-id="5eabc-544">예기치 않은 동작과 혼동을 방지 하려면 것이 좋습니다 일반적으로 소멸자에 대 한만 해당 개체의 필드에 저장 된 데이터 정리를 수행 하 고 참조 된 개체 또는 정적 필드에 작업을 수행할 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-544">To avoid confusion and unexpected behavior, it is generally a good idea for destructors to only perform cleanup on data stored in their object's own fields, and not to perform any actions on referenced objects or static fields.</span></span>

<span data-ttu-id="5eabc-545">소멸자를 사용 하는 대신 구현 클래스를 사용 하는 것은 `System.IDisposable` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-545">An alternative to using destructors is to let a class implement the `System.IDisposable` interface.</span></span> <span data-ttu-id="5eabc-546">이 통해 리소스로 개체에 액세스 하 여 일반적으로 개체의 리소스를 해제 하는 시기를 결정 하는 개체의 클라이언트는 `using` 문 ([는 문을 사용 하 여](statements.md#the-using-statement)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-546">This allows the client of the object to determine when to release the resources of the object, typically by accessing the object as a resource in a `using` statement ([The using statement](statements.md#the-using-statement)).</span></span>

## <a name="execution-order"></a><span data-ttu-id="5eabc-547">실행 순서</span><span class="sxs-lookup"><span data-stu-id="5eabc-547">Execution order</span></span>

<span data-ttu-id="5eabc-548">C# 프로그램의 실행에는 각 실행 스레드에의 한 부작용 중요 실행 시점에 유지 됩니다 있도록 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-548">Execution of a C# program proceeds such that the side effects of each executing thread are preserved at critical execution points.</span></span> <span data-ttu-id="5eabc-549">A ***부작용*** 읽기 또는 쓰기 volatile 필드의, 비 volatile 변수에 쓰기 예외를 throw 하 고 외부 리소스를 쓸으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-549">A ***side effect*** is defined as a read or write of a volatile field, a write to a non-volatile variable, a write to an external resource, and the throwing of an exception.</span></span> <span data-ttu-id="5eabc-550">이러한 부작용의 순서를 유지 해야 하는 중요 한 실행 지점은 volatile 필드에 대 한 참조 ([Volatile 필드](classes.md#volatile-fields)), `lock` 문 ([lock 문에](statements.md#the-lock-statement)), 및 스레드 생성 및 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-550">The critical execution points at which the order of these side effects must be preserved are references to volatile fields ([Volatile fields](classes.md#volatile-fields)), `lock` statements ([The lock statement](statements.md#the-lock-statement)), and thread creation and termination.</span></span> <span data-ttu-id="5eabc-551">실행 환경에서는 다음 제약 조건에 따라 C# 프로그램에서의 실행 순서를 변경 하려면:</span><span class="sxs-lookup"><span data-stu-id="5eabc-551">The execution environment is free to change the order of execution of a C# program, subject to the following constraints:</span></span>

*  <span data-ttu-id="5eabc-552">데이터 종속성 실행의 스레드 내에서 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-552">Data dependence is preserved within a thread of execution.</span></span> <span data-ttu-id="5eabc-553">즉, 각 변수의 값은 원래 프로그램 순서로 스레드에서 모든 문이 실행 된 것 처럼 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-553">That is, the value of each variable is computed as if all statements in the thread were executed in original program order.</span></span>
*  <span data-ttu-id="5eabc-554">초기화 순서 규칙에서 유지 됩니다 ([필드 초기화](classes.md#field-initialization) 하 고 [변수 이니셜라이저](classes.md#variable-initializers)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-554">Initialization ordering rules are preserved ([Field initialization](classes.md#field-initialization) and [Variable initializers](classes.md#variable-initializers)).</span></span>
*  <span data-ttu-id="5eabc-555">Volatile 읽기 및 쓰기와 관련 하 여 의도의 순서는 유지 ([Volatile 필드](classes.md#volatile-fields)).</span><span class="sxs-lookup"><span data-stu-id="5eabc-555">The ordering of side effects is preserved with respect to volatile reads and writes ([Volatile fields](classes.md#volatile-fields)).</span></span> <span data-ttu-id="5eabc-556">또한 실행 환경 해당 식의 값을 사용 하지 않도록 하 고 필요한 부작용이 없습니다 (volatile 필드에 액세스 하거나 메서드를 호출 하 여 발생 한 모든 포함)이 생성 되는 추론할 수 있습니다 하는 경우 식의 일부를 평가 하지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-556">Additionally, the execution environment need not evaluate part of an expression if it can deduce that that expression's value is not used and that no needed side effects are produced (including any caused by calling a method or accessing a volatile field).</span></span> <span data-ttu-id="5eabc-557">비동기 이벤트 (예: 다른 스레드에 의해 throw 된 예외)에 의해 프로그램 실행이 중단 되며 때 눈에 띄는 부작용 원래 프로그램 순서로 표시 되는지 보장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5eabc-557">When program execution is interrupted by an asynchronous event (such as an exception thrown by another thread), it is not guaranteed that the observable side effects are visible in the original program order.</span></span>
