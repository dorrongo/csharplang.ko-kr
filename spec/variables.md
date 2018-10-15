# <a name="variables"></a><span data-ttu-id="b3bf2-101">변수</span><span class="sxs-lookup"><span data-stu-id="b3bf2-101">Variables</span></span>

<span data-ttu-id="b3bf2-102">변수는 저장소 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-102">Variables represent storage locations.</span></span> <span data-ttu-id="b3bf2-103">모든 변수가 될 수 있는 값을 결정 하는 형식의 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-103">Every variable has a type that determines what values can be stored in the variable.</span></span> <span data-ttu-id="b3bf2-104">C#은 형식이 안전한 언어 및 C# 컴파일러는 값이 변수에 저장 된 항상 적절 한 형식의 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-104">C# is a type-safe language, and the C# compiler guarantees that values stored in variables are always of the appropriate type.</span></span> <span data-ttu-id="b3bf2-105">할당을 통해 또는 사용 하 여 변수 값을 변경할 수 있습니다 합니다 `++` 고 `--` 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-105">The value of a variable can be changed through assignment or through use of the `++` and `--` operators.</span></span>

<span data-ttu-id="b3bf2-106">변수 여야 합니다 ***명확 하 게 할당*** ([한정 된 할당](variables.md#definite-assignment)) 전에 해당 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-106">A variable must be ***definitely assigned*** ([Definite assignment](variables.md#definite-assignment)) before its value can be obtained.</span></span>

<span data-ttu-id="b3bf2-107">변수 중 하나는 다음 섹션에서 설명한 ***처음에 할당*** 또는 ***처음에 할당 되지 않은***합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-107">As described in the following sections, variables are either ***initially assigned*** or ***initially unassigned***.</span></span> <span data-ttu-id="b3bf2-108">처음에 할당 된 변수를 잘 정의 된 초기 값 및을 항상 것으로 정적으로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-108">An initially assigned variable has a well-defined initial value and is always considered definitely assigned.</span></span> <span data-ttu-id="b3bf2-109">처음에 할당 되지 않은 변수가 초기 값 없음.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-109">An initially unassigned variable has no initial value.</span></span> <span data-ttu-id="b3bf2-110">특정 위치에 정적으로 할당 된 간주 되기 위해 초기에 할당 되지 않은 변수의 변수에 할당 앞에 해당 위치에 모든 가능한 실행 경로에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-110">For an initially unassigned variable to be considered definitely assigned at a certain location, an assignment to the variable must occur in every possible execution path leading to that location.</span></span>

## <a name="variable-categories"></a><span data-ttu-id="b3bf2-111">변수 범주</span><span class="sxs-lookup"><span data-stu-id="b3bf2-111">Variable categories</span></span>

<span data-ttu-id="b3bf2-112">C#-7 범주 변수를 정의 하는 중: 정적 변수, 인스턴스 변수, 배열 요소, 매개 변수 값, 참조 매개 변수, 출력 매개 변수 및 지역 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-112">C# defines seven categories of variables: static variables, instance variables, array elements, value parameters, reference parameters, output parameters, and local variables.</span></span> <span data-ttu-id="b3bf2-113">다음 단원에서는 이러한 각 범주를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-113">The sections that follow describe each of these categories.</span></span>

<span data-ttu-id="b3bf2-114">예제</span><span class="sxs-lookup"><span data-stu-id="b3bf2-114">In the example</span></span>
```csharp
class A
{
public static int x;
int y;

void F(int[] v, int a, ref int b, out int c) {
int i = 1;
c = a + b++;
}
}
```
<span data-ttu-id="b3bf2-115">`x` 정적 변수가 `y` 는 인스턴스 변수 `v[0]` 배열 요소는 `a` 값 매개 변수 `b` 참조 매개 변수 `c` 출력 매개 변수 및 `i` 는 지역 변수.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-115">`x` is a static variable, `y` is an instance variable, `v[0]` is an array element, `a` is a value parameter, `b` is a reference parameter, `c` is an output parameter, and `i` is a local variable.</span></span>

### <a name="static-variables"></a><span data-ttu-id="b3bf2-116">정적 변수</span><span class="sxs-lookup"><span data-stu-id="b3bf2-116">Static variables</span></span>

<span data-ttu-id="b3bf2-117">필드를 사용 하 여 선언 된 `static` 한정자가 호출을 ***정적 변수***.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-117">A field declared with the `static` modifier is called a ***static variable***.</span></span> <span data-ttu-id="b3bf2-118">정적 변수는 정적 생성자를 실행 하기 전에 존재 하 게 제공 됩니다 ([정적 생성자](classes.md#static-constructors)) 포함 하는 형식 및 연결 된 응용 프로그램 도메인 소멸 하는 경우 사라지게에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-118">A static variable comes into existence before execution of the static constructor ([Static constructors](classes.md#static-constructors)) for its containing type, and ceases to exist when the associated application domain ceases to exist.</span></span>

<span data-ttu-id="b3bf2-119">정적 변수의 초기 값은 기본값 ([기본값](variables.md#default-values)) 변수의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-119">The initial value of a static variable is the default value ([Default values](variables.md#default-values)) of the variable's type.</span></span>

<span data-ttu-id="b3bf2-120">한정 된 할당 검사를 위해 정적 변수 처음 할당 된 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-120">For purposes of definite assignment checking, a static variable is considered initially assigned.</span></span>

### <a name="instance-variables"></a><span data-ttu-id="b3bf2-121">인스턴스 변수</span><span class="sxs-lookup"><span data-stu-id="b3bf2-121">Instance variables</span></span>

<span data-ttu-id="b3bf2-122">없이 선언 된 필드를 `static` 한정자가 호출 되는 ***인스턴스 변수***.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-122">A field declared without the `static` modifier is called an ***instance variable***.</span></span>

#### <a name="instance-variables-in-classes"></a><span data-ttu-id="b3bf2-123">클래스의 인스턴스 변수</span><span class="sxs-lookup"><span data-stu-id="b3bf2-123">Instance variables in classes</span></span>

<span data-ttu-id="b3bf2-124">클래스의 인스턴스 변수는 해당 클래스의 새 인스턴스를 만들고 해당 인스턴스에 대 한 참조가 없는 및 인스턴스의 소멸자 (있는 경우)가 실행 될 때 소멸 하는 경우 존재 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-124">An instance variable of a class comes into existence when a new instance of that class is created, and ceases to exist when there are no references to that instance and the instance's destructor (if any) has executed.</span></span>

<span data-ttu-id="b3bf2-125">클래스의 인스턴스 변수의 초기 값은 기본값 ([기본값](variables.md#default-values)) 변수의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-125">The initial value of an instance variable of a class is the default value ([Default values](variables.md#default-values)) of the variable's type.</span></span>

<span data-ttu-id="b3bf2-126">한정 된 할당 검사를 위해 클래스의 인스턴스 변수 처음 할당 된 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-126">For the purpose of definite assignment checking, an instance variable of a class is considered initially assigned.</span></span>

#### <a name="instance-variables-in-structs"></a><span data-ttu-id="b3bf2-127">구조체의 인스턴스 변수</span><span class="sxs-lookup"><span data-stu-id="b3bf2-127">Instance variables in structs</span></span>

<span data-ttu-id="b3bf2-128">구조체의 인스턴스 변수는 자신이 속한 구조체 변수와 동일한 수명을 정확 하 게에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-128">An instance variable of a struct has exactly the same lifetime as the struct variable to which it belongs.</span></span> <span data-ttu-id="b3bf2-129">즉, 경우 구조체 형식의 변수 사라지면 나타나거나 사라집니다, 있으므로 너무 구조체의 인스턴스 변수를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-129">In other words, when a variable of a struct type comes into existence or ceases to exist, so too do the instance variables of the struct.</span></span>

<span data-ttu-id="b3bf2-130">초기 할당 상태 구조체의 인스턴스 변수를 포함 하는 구조체 변수의 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-130">The initial assignment state of an instance variable of a struct is the same as that of the containing struct variable.</span></span> <span data-ttu-id="b3bf2-131">즉, 구조체 변수를 처음으로 간주 됩니다 할당 되므로 너무 해당 인스턴스 변수 이며 구조체 변수는 처음에 할당 되지 않은 것으로 간주 됩니다을 하는 경우 해당 인스턴스 변수 마찬가지로 할당 되지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-131">In other words, when a struct variable is considered initially assigned, so too are its instance variables, and when a struct variable is considered initially unassigned, its instance variables are likewise unassigned.</span></span>

### <a name="array-elements"></a><span data-ttu-id="b3bf2-132">배열 요소</span><span class="sxs-lookup"><span data-stu-id="b3bf2-132">Array elements</span></span>

<span data-ttu-id="b3bf2-133">배열 요소의 배열 인스턴스를 만들 때 존재 하 게 제공 및 배열 인스턴스에 대 한 참조가 없는 경우 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-133">The elements of an array come into existence when an array instance is created, and cease to exist when there are no references to that array instance.</span></span>

<span data-ttu-id="b3bf2-134">각 배열 요소의 초기 값은 기본값 ([기본값](variables.md#default-values)) 배열 요소의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-134">The initial value of each of the elements of an array is the default value ([Default values](variables.md#default-values)) of the type of the array elements.</span></span>

<span data-ttu-id="b3bf2-135">한정 된 할당 검사를 위해 배열 요소 처음 할당 된 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-135">For the purpose of definite assignment checking, an array element is considered initially assigned.</span></span>

### <a name="value-parameters"></a><span data-ttu-id="b3bf2-136">값 매개 변수</span><span class="sxs-lookup"><span data-stu-id="b3bf2-136">Value parameters</span></span>

<span data-ttu-id="b3bf2-137">없이 선언 된 매개 변수를 `ref` 또는 `out` 한정자를 ***값 매개 변수***합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-137">A parameter declared without a `ref` or `out` modifier is a ***value parameter***.</span></span>

<span data-ttu-id="b3bf2-138">값 매개 변수는 함수 멤버 (메서드, 인스턴스 생성자, 접근자 또는 연산자) 나 익명 함수 호출 시 존재 하 게 제공 하는 매개 변수가 속한 호출에 지정 된 인수의 값으로 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-138">A value parameter comes into existence upon invocation of the function member (method, instance constructor, accessor, or operator) or anonymous function to which the parameter belongs, and is initialized with the value of the argument given in the invocation.</span></span> <span data-ttu-id="b3bf2-139">값 매개 변수를 일반적으로 되 면 소멸 익명 함수 또는 함수 멤버를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-139">A value parameter normally ceases to exist upon return of the function member or anonymous function.</span></span> <span data-ttu-id="b3bf2-140">그러나 값 매개 변수는 익명 함수에 의해 캡처된 경우 ([익명 함수 식](expressions.md#anonymous-function-expressions)), 수명이 대리자까지 이상 확장 또는 익명 함수에서 생성 하는 식 트리에 적합 한 가비지 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-140">However, if the value parameter is captured by an anonymous function ([Anonymous function expressions](expressions.md#anonymous-function-expressions)), its life time extends at least until the delegate or expression tree created from that anonymous function is eligible for garbage collection.</span></span>

<span data-ttu-id="b3bf2-141">한정 된 할당 검사를 위해 값 매개 변수를 처음에 할당 된 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-141">For the purpose of definite assignment checking, a value parameter is considered initially assigned.</span></span>

### <a name="reference-parameters"></a><span data-ttu-id="b3bf2-142">참조 매개 변수</span><span class="sxs-lookup"><span data-stu-id="b3bf2-142">Reference parameters</span></span>

<span data-ttu-id="b3bf2-143">사용 하 여 선언 된 매개 변수를 `ref` 한정자가을 ***매개 변수를 참조할***합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-143">A parameter declared with a `ref` modifier is a ***reference parameter***.</span></span>

<span data-ttu-id="b3bf2-144">참조 매개 변수는 새 저장소 위치를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-144">A reference parameter does not create a new storage location.</span></span> <span data-ttu-id="b3bf2-145">대신 참조 매개 변수는 함수 멤버 또는 익명 함수 호출의 인수로 지정 된 변수와 동일한 저장소 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-145">Instead, a reference parameter represents the same storage location as the variable given as the argument in the function member or anonymous function invocation.</span></span> <span data-ttu-id="b3bf2-146">따라서 참조 매개 변수의 값은 항상 내부 변수와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-146">Thus, the value of a reference parameter is always the same as the underlying variable.</span></span>

<span data-ttu-id="b3bf2-147">참조 매개 변수는 다음과 같은 한정 된 할당 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-147">The following definite assignment rules apply to reference parameters.</span></span> <span data-ttu-id="b3bf2-148">설명 하는 출력 매개 변수에 대 한 다양 한 규칙을 참고 하십시오 [출력 매개 변수](variables.md#output-parameters)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-148">Note the different rules for output parameters described in [Output parameters](variables.md#output-parameters).</span></span>

*  <span data-ttu-id="b3bf2-149">변수 할당 되어야 합니다 ([한정 된 할당](variables.md#definite-assignment)) 전에 함수 멤버 또는 대리자 호출에서 참조 매개 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-149">A variable must be definitely assigned ([Definite assignment](variables.md#definite-assignment)) before it can be passed as a reference parameter in a function member or delegate invocation.</span></span>
*  <span data-ttu-id="b3bf2-150">함수 멤버 또는 익명 함수 내에서 처음에 할당 하는 참조 매개 변수 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-150">Within a function member or anonymous function, a reference parameter is considered initially assigned.</span></span>

<span data-ttu-id="b3bf2-151">인스턴스 메서드 또는 인스턴스 접근자 구조체 형식 내에서 `this` 키워드는 구조체 형식의 참조 매개 변수로 정확 하 게 작동 합니다 ([이 액세스](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="b3bf2-151">Within an instance method or instance accessor of a struct type, the `this` keyword behaves exactly as a reference parameter of the struct type ([This access](expressions.md#this-access)).</span></span>

### <a name="output-parameters"></a><span data-ttu-id="b3bf2-152">출력 매개 변수</span><span class="sxs-lookup"><span data-stu-id="b3bf2-152">Output parameters</span></span>

<span data-ttu-id="b3bf2-153">사용 하 여 선언 된 매개 변수를 `out` 한정자가는 ***출력 매개 변수***합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-153">A parameter declared with an `out` modifier is an ***output parameter***.</span></span>

<span data-ttu-id="b3bf2-154">출력 매개 변수는 새 저장소 위치를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-154">An output parameter does not create a new storage location.</span></span> <span data-ttu-id="b3bf2-155">대신, 출력 매개 변수는 함수 멤버 또는 대리자 호출의 인수로 지정 된 변수와 동일한 저장소 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-155">Instead, an output parameter represents the same storage location as the variable given as the argument in the function member or delegate invocation.</span></span> <span data-ttu-id="b3bf2-156">따라서 출력 매개 변수의 값은 항상 내부 변수와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-156">Thus, the value of an output parameter is always the same as the underlying variable.</span></span>

<span data-ttu-id="b3bf2-157">출력 매개 변수는 다음과 같은 한정 된 할당 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-157">The following definite assignment rules apply to output parameters.</span></span> <span data-ttu-id="b3bf2-158">설명 하는 참조 매개 변수에 대 한 다양 한 규칙을 참고 하십시오 [매개 변수를 참조할](variables.md#reference-parameters)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-158">Note the different rules for reference parameters described in [Reference parameters](variables.md#reference-parameters).</span></span>

*  <span data-ttu-id="b3bf2-159">변수를 필요 하지 명확 하 게 할당 대리자 호출 또는 함수 멤버의 출력 매개 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-159">A variable need not be definitely assigned before it can be passed as an output parameter in a function member or delegate invocation.</span></span>
*  <span data-ttu-id="b3bf2-160">함수 멤버 또는 대리자 호출의 정상적인 완료를 다음 출력 매개 변수를 사용 하는 것으로 간주 하는 대로 전달 된 각 변수에 실행 경로에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-160">Following the normal completion of a function member or delegate invocation, each variable that was passed as an output parameter is considered assigned in that execution path.</span></span>
*  <span data-ttu-id="b3bf2-161">함수 멤버 또는 익명 함수 내에서 출력 매개 변수는 처음에 할당 되지 않은 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-161">Within a function member or anonymous function, an output parameter is considered initially unassigned.</span></span>
*  <span data-ttu-id="b3bf2-162">익명 함수 또는 함수 멤버의 모든 출력 매개 변수 할당 되어야 합니다 ([한정 된 할당](variables.md#definite-assignment)) 함수 앞 멤버 또는 익명 함수 정상적으로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-162">Every output parameter of a function member or anonymous function must be definitely assigned ([Definite assignment](variables.md#definite-assignment)) before the function member or anonymous function returns normally.</span></span>

<span data-ttu-id="b3bf2-163">구조체 형식의 인스턴스 생성자 내에서 `this` 키워드는 구조체 형식의 출력 매개 변수로 정확 하 게 작동 합니다 ([이 액세스](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="b3bf2-163">Within an instance constructor of a struct type, the `this` keyword behaves exactly as an output parameter of the struct type ([This access](expressions.md#this-access)).</span></span>

### <a name="local-variables"></a><span data-ttu-id="b3bf2-164">지역 변수</span><span class="sxs-lookup"><span data-stu-id="b3bf2-164">Local variables</span></span>

<span data-ttu-id="b3bf2-165">A ***지역 변수*** 사용 하 여 선언를 *local_variable_declaration*에서 발생할 수 있는 *블록*, *for_statement*을 *switch_statement* 또는 *using_statement*; 또는 *foreach_statement* 또는 *specific_catch_clause* 는에대한*try_statement*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-165">A ***local variable*** is declared by a *local_variable_declaration*, which may occur in a *block*, a *for_statement*, a *switch_statement* or a *using_statement*; or by a *foreach_statement* or a *specific_catch_clause* for a *try_statement*.</span></span>

<span data-ttu-id="b3bf2-166">지역 변수의 수명은는 저장소에 대 한 예약 되도록 보장 하는 프로그램 실행의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-166">The lifetime of a local variable is the portion of program execution during which storage is guaranteed to be reserved for it.</span></span> <span data-ttu-id="b3bf2-167">이 수명에 대 한 항목에서 적어도 확장 합니다 *블록*, *for_statement*를 *switch_statement*, *using_statement*, *foreach_statement*, 또는 *specific_catch_clause* 에 연결 하는 실행 될 때까지 *블록*, *for_statement*, *switch_statement*를 *using_statement*하십시오 *foreach_statement*, 또는 *specific_catch_clause* 어떤 방식으로 끝납니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-167">This lifetime extends at least from entry into the *block*, *for_statement*, *switch_statement*, *using_statement*, *foreach_statement*, or *specific_catch_clause* with which it is associated, until execution of that *block*, *for_statement*, *switch_statement*, *using_statement*, *foreach_statement*, or *specific_catch_clause* ends in any way.</span></span> <span data-ttu-id="b3bf2-168">(입력는 괄호로 묶인 *블록* 일시 중단 하지만 현재 실행 종료 하지 않습니다 메서드를 호출 하거나 *블록*, *for_statement*, *switch_statement* 하십시오 *using_statement*를 *foreach_statement*, 또는 *specific_catch_clause*.) 지역 변수는 익명 함수에 의해 캡처된 경우 ([외부 변수를 캡처할](expressions.md#captured-outer-variables)), 수명 기간 동안 대리자 또는 식 트리를 제공 하는 다른 개체와 함께 익명 함수에서 생성 될 때까지 적어도 확장 캡처된 변수 참조, 가비지 수집에 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-168">(Entering an enclosed *block* or calling a method suspends, but does not end, execution of the current *block*, *for_statement*, *switch_statement*, *using_statement*, *foreach_statement*, or *specific_catch_clause*.) If the local variable is captured by an anonymous function ([Captured outer variables](expressions.md#captured-outer-variables)), its lifetime extends at least until the delegate or expression tree created from the anonymous function, along with any other objects that come to reference the captured variable, are eligible for garbage collection.</span></span>

<span data-ttu-id="b3bf2-169">경우 부모 *블록*, *for_statement*, *switch_statement*하십시오 *using_statement*, *foreach_statement*, 또는 *specific_catch_clause* 입력 재귀적으로 지역 변수의 새 인스턴스를 매번 만들어집니다 및 해당 *local_variable_initializer*있는 평가 되는 경우, 각 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-169">If the parent *block*, *for_statement*, *switch_statement*, *using_statement*, *foreach_statement*, or *specific_catch_clause* is entered recursively, a new instance of the local variable is created each time, and its *local_variable_initializer*, if any, is evaluated each time.</span></span>

<span data-ttu-id="b3bf2-170">도입 된 지역 변수를 *local_variable_declaration* 자동으로 초기화 되지 않으며 따라서 기본값은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-170">A local variable introduced by a *local_variable_declaration* is not automatically initialized and thus has no default value.</span></span> <span data-ttu-id="b3bf2-171">한정 된 할당 검사를 위해에서 도입 된 지역 변수를 *local_variable_declaration* 처음에 할당 되지 않은 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-171">For the purpose of definite assignment checking, a local variable introduced by a *local_variable_declaration* is considered initially unassigned.</span></span> <span data-ttu-id="b3bf2-172">A *local_variable_declaration* 포함 될 수 있습니다는 *local_variable_initializer*, 경우 변수는 정적으로 할당 초기화 식은 한 후에 ([ 선언문](variables.md#declaration-statements)).</span><span class="sxs-lookup"><span data-stu-id="b3bf2-172">A *local_variable_declaration* may include a *local_variable_initializer*, in which case the variable is considered definitely assigned only after the initializing expression ([Declaration statements](variables.md#declaration-statements)).</span></span>

<span data-ttu-id="b3bf2-173">도입 된 지역 변수의 범위를 *local_variable_declaration*, 해당 지역 변수 앞에 오는 텍스트 위치를 가리키도록 하면 컴파일 타임 오류가 발생 해당 *local_variable_declarator*.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-173">Within the scope of a local variable introduced by a *local_variable_declaration*, it is a compile-time error to refer to that local variable in a textual position that precedes its *local_variable_declarator*.</span></span> <span data-ttu-id="b3bf2-174">지역 변수 선언 암시적 경우 ([지역 변수 선언](statements.md#local-variable-declarations)), 내 변수를 참조 하면 오류가 발생 이기도 해당 *local_variable_declarator*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-174">If the local variable declaration is implicit ([Local variable declarations](statements.md#local-variable-declarations)), it is also an error to refer to the variable within its *local_variable_declarator*.</span></span>

<span data-ttu-id="b3bf2-175">도입 된 지역 변수를 *foreach_statement* 또는 *specific_catch_clause* 전체 범위 내에서 정적으로 할당 된 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-175">A local variable introduced by a *foreach_statement* or a *specific_catch_clause* is considered definitely assigned in its entire scope.</span></span>

<span data-ttu-id="b3bf2-176">지역 변수의 실제 수명은 구현에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-176">The actual lifetime of a local variable is implementation-dependent.</span></span> <span data-ttu-id="b3bf2-177">예를 들어, 컴파일러는 블록의 지역 변수에 해당 블록의 작은 부분에만 사용 됨을 경우가 정적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-177">For example, a compiler might statically determine that a local variable in a block is only used for a small portion of that block.</span></span> <span data-ttu-id="b3bf2-178">이 분석을 사용 하 여 컴파일러 변수 저장소 포함 블록 보다 짧은 수명 것에서 발생 하는 코드를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-178">Using this analysis, the compiler could generate code that results in the variable's storage having a shorter lifetime than its containing block.</span></span>

<span data-ttu-id="b3bf2-179">저장소 지역 참조 변수에서 참조 하는 로컬 참조 변수의 수명은 독립적으로 회수 ([자동 메모리 관리](basic-concepts.md#automatic-memory-management)).</span><span class="sxs-lookup"><span data-stu-id="b3bf2-179">The storage referred to by a local reference variable is reclaimed independently of the lifetime of that local reference variable ([Automatic memory management](basic-concepts.md#automatic-memory-management)).</span></span>

## <a name="default-values"></a><span data-ttu-id="b3bf2-180">기본값</span><span class="sxs-lookup"><span data-stu-id="b3bf2-180">Default values</span></span>

<span data-ttu-id="b3bf2-181">다음과 같은 범주의 변수는 기본값으로 자동으로 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-181">The following categories of variables are automatically initialized to their default values:</span></span>

*  <span data-ttu-id="b3bf2-182">정적 변수</span><span class="sxs-lookup"><span data-stu-id="b3bf2-182">Static variables.</span></span>
*  <span data-ttu-id="b3bf2-183">클래스 인스턴스의 인스턴스 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-183">Instance variables of class instances.</span></span>
*  <span data-ttu-id="b3bf2-184">배열 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-184">Array elements.</span></span>

<span data-ttu-id="b3bf2-185">변수의 기본값 변수의 형식에 따라 달라 집니다 하 고 다음과 같이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-185">The default value of a variable depends on the type of the variable and is determined as follows:</span></span>

*  <span data-ttu-id="b3bf2-186">변수에 대 한는 *value_type*, 기본값은 하 여 계산 된 값과 동일 합니다 *value_type*의 기본 생성자 ([기본 생성자](types.md#default-constructors)).</span><span class="sxs-lookup"><span data-stu-id="b3bf2-186">For a variable of a *value_type*, the default value is the same as the value computed by the *value_type*'s default constructor ([Default constructors](types.md#default-constructors)).</span></span>
*  <span data-ttu-id="b3bf2-187">변수를 *reference_type*, 기본값은 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-187">For a variable of a *reference_type*, the default value is `null`.</span></span>

<span data-ttu-id="b3bf2-188">Memory manager 함으로써 기본값으로 초기화는 일반적으로 수행 하거나 가비지 수집기 사용에 대 한 할당 하기 전에 모든 비트가 0 인 메모리를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-188">Initialization to default values is typically done by having the memory manager or garbage collector initialize memory to all-bits-zero before it is allocated for use.</span></span> <span data-ttu-id="b3bf2-189">Null 참조를 나타내는 모든 비트가 0을 사용 하는 것이 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-189">For this reason, it is convenient to use all-bits-zero to represent the null reference.</span></span>

## <a name="definite-assignment"></a><span data-ttu-id="b3bf2-190">한정 된 할당</span><span class="sxs-lookup"><span data-stu-id="b3bf2-190">Definite assignment</span></span>

<span data-ttu-id="b3bf2-191">지정 된 위치에서 실행 코드에 함수 멤버 변수를 라고 ***명확 하 게 할당*** 특정 정적 흐름 분석을 통해 경우 컴파일러가 입증할 수 있습니다 ([한정 된 결정 하는 것에 대 한 정확한 규칙 할당](variables.md#precise-rules-for-determining-definite-assignment)), 변수에 자동으로 초기화 하거나 하나 이상 할당 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-191">At a given location in the executable code of a function member, a variable is said to be ***definitely assigned*** if the compiler can prove, by a particular static flow analysis ([Precise rules for determining definite assignment](variables.md#precise-rules-for-determining-definite-assignment)), that the variable has been automatically initialized or has been the target of at least one assignment.</span></span> <span data-ttu-id="b3bf2-192">한정 된 할당의 규칙은 비공식적으로 언급 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-192">Informally stated, the rules of definite assignment are:</span></span>

*  <span data-ttu-id="b3bf2-193">처음에 할당된 된 변수 ([처음에 할당 되는 변수](variables.md#initially-assigned-variables))는 항상 정적으로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-193">An initially assigned variable ([Initially assigned variables](variables.md#initially-assigned-variables)) is always considered definitely assigned.</span></span>
*  <span data-ttu-id="b3bf2-194">처음에 할당 되지 않은 변수 ([나중에 변수를 할당](variables.md#initially-unassigned-variables)) 것으로 간주 됩니다 정적으로 할당 된 지정된 된 위치에서 해당 위치에 선행 하는 모든 가능한 실행 경로 중 하나 이상 포함 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-194">An initially unassigned variable ([Initially unassigned variables](variables.md#initially-unassigned-variables)) is considered definitely assigned at a given location if all possible execution paths leading to that location contain at least one of the following:</span></span>
    * <span data-ttu-id="b3bf2-195">단순 할당 ([단순 할당](expressions.md#simple-assignment)) 변수 된 왼쪽된 피연산자.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-195">A simple assignment ([Simple assignment](expressions.md#simple-assignment)) in which the variable is the left operand.</span></span>
    * <span data-ttu-id="b3bf2-196">호출 식 ([호출 식](expressions.md#invocation-expressions)) 또는 개체 생성 식 ([개체 만들기 식](expressions.md#object-creation-expressions)) 출력 매개 변수로 변수를 전달 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-196">An invocation expression ([Invocation expressions](expressions.md#invocation-expressions)) or object creation expression ([Object creation expressions](expressions.md#object-creation-expressions)) that passes the variable as an output parameter.</span></span>
    * <span data-ttu-id="b3bf2-197">지역 변수, 지역 변수 선언 ([지역 변수 선언](statements.md#local-variable-declarations)) 변수 이니셜라이저에서 예외를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-197">For a local variable, a local variable declaration ([Local variable declarations](statements.md#local-variable-declarations)) that includes a variable initializer.</span></span>

<span data-ttu-id="b3bf2-198">위의 비공식 규칙 내부 공식 사양에 설명 되어 [처음에 변수를 할당](variables.md#initially-assigned-variables)를 [나중에 변수를 할당](variables.md#initially-unassigned-variables), 및 [결정 하는 것에 대 한 정확한 규칙 한정 된 할당](variables.md#precise-rules-for-determining-definite-assignment)합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-198">The formal specification underlying the above informal rules is described in [Initially assigned variables](variables.md#initially-assigned-variables), [Initially unassigned variables](variables.md#initially-unassigned-variables), and [Precise rules for determining definite assignment](variables.md#precise-rules-for-determining-definite-assignment).</span></span>

<span data-ttu-id="b3bf2-199">인스턴스 변수의 한정 된 할당 상태를 *struct_type* 변수 개별적으로 집합적으로 추적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-199">The definite assignment states of instance variables of a *struct_type* variable are tracked individually as well as collectively.</span></span> <span data-ttu-id="b3bf2-200">위의 규칙 이외에 다음 규칙에 적용 *struct_type* 변수 및 해당 인스턴스 변수:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-200">In additional to the rules above, the following rules apply to *struct_type* variables and their instance variables:</span></span>

*  <span data-ttu-id="b3bf2-201">인스턴스 변수는 정적으로 할당 하는 경우 포함 *struct_type* 변수 정적으로 할당 된 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-201">An instance variable is considered definitely assigned if its containing *struct_type* variable is considered definitely assigned.</span></span>
*  <span data-ttu-id="b3bf2-202">A *struct_type* 각 해당 인스턴스 변수는 정적으로 할당 하는 경우 변수를 정적으로 할당 된 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-202">A *struct_type* variable is considered definitely assigned if each of its instance variables is considered definitely assigned.</span></span>

<span data-ttu-id="b3bf2-203">한정 된 할당은 다음 경우에 요구 사항:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-203">Definite assignment is a requirement in the following contexts:</span></span>

*  <span data-ttu-id="b3bf2-204">변수를 가져온 위치 값을 해당 하는 각 위치에서 확실 하 게 할당 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-204">A variable must be definitely assigned at each location where its value is obtained.</span></span> <span data-ttu-id="b3bf2-205">이 정의 되지 않은 값 되지 수행 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-205">This ensures that undefined values never occur.</span></span> <span data-ttu-id="b3bf2-206">식에서 변수 발생 경우를 제외 하 고 변수 값을 가져올 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-206">The occurrence of a variable in an expression is considered to obtain the value of the variable, except when</span></span>
    * <span data-ttu-id="b3bf2-207">변수는 단순 할당의 왼쪽된 피연산자</span><span class="sxs-lookup"><span data-stu-id="b3bf2-207">the variable is the left operand of a simple assignment,</span></span>
    * <span data-ttu-id="b3bf2-208">변수는 output 매개 변수로 전달 됩니다 또는</span><span class="sxs-lookup"><span data-stu-id="b3bf2-208">the variable is passed as an output parameter, or</span></span>
    * <span data-ttu-id="b3bf2-209">변수를 *struct_type* 변수 멤버 액세스의 경우 왼쪽된 피연산자와 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-209">the variable is a *struct_type* variable and occurs as the left operand of a member access.</span></span>
*  <span data-ttu-id="b3bf2-210">변수는 참조 매개 변수로 전달 되는 각 위치에서 확실 하 게 할당 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-210">A variable must be definitely assigned at each location where it is passed as a reference parameter.</span></span> <span data-ttu-id="b3bf2-211">이렇게 하면 호출 되는 함수 멤버가 처음에 할당 하는 참조 매개 변수를 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-211">This ensures that the function member being invoked can consider the reference parameter initially assigned.</span></span>
*  <span data-ttu-id="b3bf2-212">함수 멤버의 모든 출력 매개 변수는 함수 멤버를 반환 하는 각 위치에 할당 되어야 합니다 (통해를 `return` 문 또는 멤버 함수 본문의 끝에 도달 하는 실행을 통해).</span><span class="sxs-lookup"><span data-stu-id="b3bf2-212">All output parameters of a function member must be definitely assigned at each location where the function member returns (through a `return` statement or through execution reaching the end of the function member body).</span></span> <span data-ttu-id="b3bf2-213">이렇게 하면는 함수 멤버 값을 반환 하지 정의 되지 않은 출력 매개 변수를 컴파일러에서 해당 변수에 할당 하는 출력 매개 변수로 변수를 사용 하는 함수 멤버 호출을 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-213">This ensures that function members do not return undefined values in output parameters, thus enabling the compiler to consider a function member invocation that takes a variable as an output parameter equivalent to an assignment to the variable.</span></span>
*  <span data-ttu-id="b3bf2-214">합니다 `this` 변수를 *struct_type* 인스턴스 생성자는 해당 인스턴스 생성자를 반환 하는 각 위치에 할당 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-214">The `this` variable of a *struct_type* instance constructor must be definitely assigned at each location where that instance constructor returns.</span></span>

### <a name="initially-assigned-variables"></a><span data-ttu-id="b3bf2-215">처음에 할당된 되는 변수</span><span class="sxs-lookup"><span data-stu-id="b3bf2-215">Initially assigned variables</span></span>

<span data-ttu-id="b3bf2-216">변수는 다음과 같은 범주의 처음으로 할당 된 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-216">The following categories of variables are classified as initially assigned:</span></span>

*  <span data-ttu-id="b3bf2-217">정적 변수</span><span class="sxs-lookup"><span data-stu-id="b3bf2-217">Static variables.</span></span>
*  <span data-ttu-id="b3bf2-218">클래스 인스턴스의 인스턴스 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-218">Instance variables of class instances.</span></span>
*  <span data-ttu-id="b3bf2-219">처음에 할당 된 구조체 변수의 인스턴스 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-219">Instance variables of initially assigned struct variables.</span></span>
*  <span data-ttu-id="b3bf2-220">배열 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-220">Array elements.</span></span>
*  <span data-ttu-id="b3bf2-221">값 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-221">Value parameters.</span></span>
*  <span data-ttu-id="b3bf2-222">참조 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-222">Reference parameters.</span></span>
*  <span data-ttu-id="b3bf2-223">에 선언 된 변수를 `catch` 절 또는 `foreach` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-223">Variables declared in a `catch` clause or a `foreach` statement.</span></span>

### <a name="initially-unassigned-variables"></a><span data-ttu-id="b3bf2-224">처음에 할당 되지 않은 변수</span><span class="sxs-lookup"><span data-stu-id="b3bf2-224">Initially unassigned variables</span></span>

<span data-ttu-id="b3bf2-225">다음과 같은 범주의 변수 할당 되지 않은 처음으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-225">The following categories of variables are classified as initially unassigned:</span></span>

*  <span data-ttu-id="b3bf2-226">처음에 할당 되지 않은 구조체 변수의 인스턴스 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-226">Instance variables of initially unassigned struct variables.</span></span>
*  <span data-ttu-id="b3bf2-227">출력 매개 변수를 포함 하는 `this` 구조체 인스턴스 생성자의 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-227">Output parameters, including the `this` variable of struct instance constructors.</span></span>
*  <span data-ttu-id="b3bf2-228">에 선언 된 지역 변수를 제외 된 `catch` 절 또는 `foreach` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-228">Local variables, except those declared in a `catch` clause or a `foreach` statement.</span></span>

### <a name="precise-rules-for-determining-definite-assignment"></a><span data-ttu-id="b3bf2-229">한정 된 할당을 확인 하는 것에 대 한 정확한 규칙</span><span class="sxs-lookup"><span data-stu-id="b3bf2-229">Precise rules for determining definite assignment</span></span>

<span data-ttu-id="b3bf2-230">사용 되는 각 변수 확실 하 게 할당 되어 있는지를 확인 하기 위해 컴파일러는이 섹션에 설명 된 것에 해당 하는 프로세스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-230">In order to determine that each used variable is definitely assigned, the compiler must use a process that is equivalent to the one described in this section.</span></span>

<span data-ttu-id="b3bf2-231">컴파일러는 처음에 할당 되지 않은 변수를 하나 이상 있는 각 함수 멤버의 본문을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-231">The compiler processes the body of each function member that has one or more initially unassigned variables.</span></span> <span data-ttu-id="b3bf2-232">처음에 할당 되지 않은 각 변수에 대해 *v*, 컴파일러가 결정을 ***한정 된 할당 상태*** 에 대 한 *v* 각 함수 멤버의 다음 항목에서:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-232">For each initially unassigned variable *v*, the compiler determines a ***definite assignment state*** for *v* at each of the following points in the function member:</span></span>

*  <span data-ttu-id="b3bf2-233">각 명령문의 시작 부분</span><span class="sxs-lookup"><span data-stu-id="b3bf2-233">At the beginning of each statement</span></span>
*  <span data-ttu-id="b3bf2-234">끝점 ([끝점 및 연결 가능성](statements.md#end-points-and-reachability)) 각 문의</span><span class="sxs-lookup"><span data-stu-id="b3bf2-234">At the end point ([End points and reachability](statements.md#end-points-and-reachability)) of each statement</span></span>
*  <span data-ttu-id="b3bf2-235">각 호에는 제어가 다른 문 또는 문의 끝 지점</span><span class="sxs-lookup"><span data-stu-id="b3bf2-235">On each arc which transfers control to another statement or to the end point of a statement</span></span>
*  <span data-ttu-id="b3bf2-236">각 식의 시작 부분</span><span class="sxs-lookup"><span data-stu-id="b3bf2-236">At the beginning of each expression</span></span>
*  <span data-ttu-id="b3bf2-237">각 식의 끝</span><span class="sxs-lookup"><span data-stu-id="b3bf2-237">At the end of each expression</span></span>

<span data-ttu-id="b3bf2-238">한정 된 할당 상태의 *v* 일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-238">The definite assignment state of *v* can be either:</span></span>

*  <span data-ttu-id="b3bf2-239">정적으로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-239">Definitely assigned.</span></span> <span data-ttu-id="b3bf2-240">이 시점에 있는 모든 가능한 제어 흐름에서 되었음을 *v* 값이 할당 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-240">This indicates that on all possible control flows to this point, *v* has been assigned a value.</span></span>
*  <span data-ttu-id="b3bf2-241">확실 하 게 할당 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-241">Not definitely assigned.</span></span> <span data-ttu-id="b3bf2-242">형식 식의 끝에 변수의 상태에 대 한 `bool`, 월을 명확 하 게 할당 되지 않습니다 (하지만 반드시)는 변수의 상태는 다음과 같은 하위 상태 중 하나에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-242">For the state of a variable at the end of an expression of type `bool`, the state of a variable that isn't definitely assigned may (but doesn't necessarily) fall into one of the following sub-states:</span></span>
    * <span data-ttu-id="b3bf2-243">True 식 뒤 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-243">Definitely assigned after true expression.</span></span> <span data-ttu-id="b3bf2-244">이 상태는 나타냅니다 *v* 부울 식이 true로 평가 이지만 부울 식이 false로 평가 하는 경우를 반드시 할당 되지 않은 경우 정적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-244">This state indicates that *v* is definitely assigned if the boolean expression evaluated as true, but is not necessarily assigned if the boolean expression evaluated as false.</span></span>
    * <span data-ttu-id="b3bf2-245">False 식 뒤 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-245">Definitely assigned after false expression.</span></span> <span data-ttu-id="b3bf2-246">이 상태는 나타냅니다 *v* 부울 식이 false로 계산 되지만 부울 식이 true로 평가 하는 경우를 반드시 할당 되지 않은 경우 정적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-246">This state indicates that *v* is definitely assigned if the boolean expression evaluated as false, but is not necessarily assigned if the boolean expression evaluated as true.</span></span>

<span data-ttu-id="b3bf2-247">다음 규칙에 따라 방법을 변수의 상태 *v* 각 위치에서 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-247">The following rules govern how the state of a variable *v* is determined at each location.</span></span>

#### <a name="general-rules-for-statements"></a><span data-ttu-id="b3bf2-248">문에 대 한 일반 규칙</span><span class="sxs-lookup"><span data-stu-id="b3bf2-248">General rules for statements</span></span>

*  <span data-ttu-id="b3bf2-249">*v* 멤버 함수 본문의 시작 부분에서 확실 하 게 할당 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-249">*v* is not definitely assigned at the beginning of a function member body.</span></span>
*  <span data-ttu-id="b3bf2-250">*v* 접근할 수 없는 문의 시작 부분에 정적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-250">*v* is definitely assigned at the beginning of any unreachable statement.</span></span>
*  <span data-ttu-id="b3bf2-251">한정 된 할당 상태의 *v* 다른 명령문의 시작 부분에 한정 된 할당 상태를 확인 하 여 결정 됩니다 *v* 의 시작 부분을 대상으로 하는 모든 제어 흐름 전송 문입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-251">The definite assignment state of *v* at the beginning of any other statement is determined by checking the definite assignment state of *v* on all control flow transfers that target the beginning of that statement.</span></span> <span data-ttu-id="b3bf2-252">경우 (및 경우에) *v* 그런 다음 이러한 모든 제어 흐름 전송 할당 확실 하 게 됩니다 *v* 문의 시작 부분에 정적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-252">If (and only if) *v* is definitely assigned on all such control flow transfers, then *v* is definitely assigned at the beginning of the statement.</span></span> <span data-ttu-id="b3bf2-253">동일한 방식으로 문을 연결 가능성을 확인 가능한 제어 흐름 전송 집합이 결정 됩니다 ([끝점 및 연결 가능성](statements.md#end-points-and-reachability)).</span><span class="sxs-lookup"><span data-stu-id="b3bf2-253">The set of possible control flow transfers is determined in the same way as for checking statement reachability ([End points and reachability](statements.md#end-points-and-reachability)).</span></span>
*  <span data-ttu-id="b3bf2-254">한정 된 할당 상태 *v* 블록의 끝 시점 `checked`, `unchecked`, `if`, `while`, `do`, `for`, `foreach`, `lock`, `using`, 또는 `switch` 문에 한정 된 할당 상태를 확인 하 여 결정 됩니다 *v* 문의의 끝점을 대상으로 하는 모든 제어 흐름 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-254">The definite assignment state of *v* at the end point of a block, `checked`, `unchecked`, `if`, `while`, `do`, `for`, `foreach`, `lock`, `using`, or `switch` statement is determined by checking the definite assignment state of *v* on all control flow transfers that target the end point of that statement.</span></span> <span data-ttu-id="b3bf2-255">하는 경우 *v* 그런 다음 이러한 모든 제어 흐름 전송 할당 확실 하 게 됩니다 *v* 문의 끝점에서 정적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-255">If *v* is definitely assigned on all such control flow transfers, then *v* is definitely assigned at the end point of the statement.</span></span> <span data-ttu-id="b3bf2-256">그렇지 않으면; *v* 문의 끝에서 확실 하 게 할당 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-256">Otherwise; *v* is not definitely assigned at the end point of the statement.</span></span> <span data-ttu-id="b3bf2-257">동일한 방식으로 문을 연결 가능성을 확인 가능한 제어 흐름 전송 집합이 결정 됩니다 ([끝점 및 연결 가능성](statements.md#end-points-and-reachability)).</span><span class="sxs-lookup"><span data-stu-id="b3bf2-257">The set of possible control flow transfers is determined in the same way as for checking statement reachability ([End points and reachability](statements.md#end-points-and-reachability)).</span></span>

#### <a name="block-statements-checked-and-unchecked-statements"></a><span data-ttu-id="b3bf2-258">문 블록 옵션을 선택 및 unchecked 문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-258">Block statements, checked, and unchecked statements</span></span>

<span data-ttu-id="b3bf2-259">한정 된 할당 상태의 *v* 컨트롤 블록에서 문 목록의 첫 번째 문 (또는 문 목록이 비어 있으면 블록의 끝 지점) 전송이 한정 된 할당에 대 한 설명은 동일*v* 블록을 앞 `checked`, 또는 `unchecked` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-259">The definite assignment state of *v* on the control transfer to the first statement of the statement list in the block (or to the end point of the block, if the statement list is empty) is the same as the definite assignment statement of *v* before the block, `checked`, or `unchecked` statement.</span></span>

#### <a name="expression-statements"></a><span data-ttu-id="b3bf2-260">식 문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-260">Expression statements</span></span>

<span data-ttu-id="b3bf2-261">식 문에 대 한 *stmt* 식으로 이루어진 *expr*:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-261">For an expression statement *stmt* that consists of the expression *expr*:</span></span>

*  <span data-ttu-id="b3bf2-262">*v* 맨 앞에 한정 된 할당 상태가 동일한 *expr* 의 시작 부분으로 *stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-262">*v* has the same definite assignment state at the beginning of *expr* as at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-263">하는 경우 *v* 끝에 한 정적으로 할당 하는 경우 *expr*의 끝점에서 정적으로 할당 됩니다 *stmt*그렇지 의끝점에서확실하게할당되지않은*stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-263">If *v* if definitely assigned at the end of *expr*, it is definitely assigned at the end point of *stmt*; otherwise; it is not definitely assigned at the end point of *stmt*.</span></span>

#### <a name="declaration-statements"></a><span data-ttu-id="b3bf2-264">선언문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-264">Declaration statements</span></span>

*  <span data-ttu-id="b3bf2-265">하는 경우 *stmt* 다음 이니셜라이저 없이 선언 문 *v* 의 끝점에서 동일한 한정 된 할당 상태가 *stmt* 의시작부분으로*stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-265">If *stmt* is a declaration statement without initializers, then *v* has the same definite assignment state at the end point of *stmt* as at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-266">하는 경우 *stmt* 는 이니셜라이저를 사용 하 여 선언 문 다음에 대 한 한정 된 할당 상태 *v* 도달한 처럼 *stmt* 문 목록 하나 할당 된 (선언) 순서 대로 이니셜라이저를 사용 하 여 각 선언에 대 한 문입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-266">If *stmt* is a declaration statement with initializers, then the definite assignment state for *v* is determined as if *stmt* were a statement list, with one assignment statement for each declaration with an initializer (in the order of declaration).</span></span>

#### <a name="if-statements"></a><span data-ttu-id="b3bf2-267">경우 문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-267">If statements</span></span>

<span data-ttu-id="b3bf2-268">에 `if` 문 *stmt* 형식:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-268">For an `if` statement *stmt* of the form:</span></span>
```csharp
if ( expr ) then_stmt else else_stmt
```

*  <span data-ttu-id="b3bf2-269">*v* 맨 앞에 한정 된 할당 상태가 동일한 *expr* 의 시작 부분으로 *stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-269">*v* has the same definite assignment state at the beginning of *expr* as at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-270">경우 *v* 끝에 정적으로 할당 됩니다 *expr*, 제어 흐름 전송에서 확실 하 게 할당 한 다음 *then_stmt* 및를 *else_stmt*  또는 끝점의 *stmt* 없습니다 else 절이 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-270">If *v* is definitely assigned at the end of *expr*, then it is definitely assigned on the control flow transfer to *then_stmt* and to either *else_stmt* or to the end-point of *stmt* if there is no else clause.</span></span>
*  <span data-ttu-id="b3bf2-271">경우 *v* 끝에 "true 식 뒤 확실 하 게 할당 된" 상태를 갖습니까 *expr*, 제어 흐름 전송에서 확실 하 게 할당 한 다음 *then_stmt*, 아니라 제어 흐름 전송 중 하나에서 정적으로 할당 된 *else_stmt* 또는 끝점의 *stmt* 없습니다 else 절이 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-271">If *v* has the state "definitely assigned after true expression" at the end of *expr*, then it is definitely assigned on the control flow transfer to *then_stmt*, and not definitely assigned on the control flow transfer to either *else_stmt* or to the end-point of *stmt* if there is no else clause.</span></span>
*  <span data-ttu-id="b3bf2-272">경우 *v* 끝에 "정적 false 식으로 할당" 상태를 갖습니까 *expr*, 제어 흐름 전송에서 확실 하 게 할당 한 다음 *else_stmt*, 아니라 제어 흐름 전송에 할당 *then_stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-272">If *v* has the state "definitely assigned after false expression" at the end of *expr*, then it is definitely assigned on the control flow transfer to *else_stmt*, and not definitely assigned on the control flow transfer to *then_stmt*.</span></span> <span data-ttu-id="b3bf2-273">끝점의 정적으로 할당 됩니다 *stmt* 끝점의 확실 하 게 할당 하는 경우에 *then_stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-273">It is definitely assigned at the end-point of *stmt* if and only if it is definitely assigned at the end-point of *then_stmt*.</span></span>
*  <span data-ttu-id="b3bf2-274">이 고, 그렇지 *v* 확실 하 게 할당 하거나 제어 흐름 전송의 비율은 합니다 *then_stmt* 또는 *else_stmt*, 또는 끝점의  *stmt* 없습니다 else 절이 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-274">Otherwise, *v* is considered not definitely assigned on the control flow transfer to either the *then_stmt* or *else_stmt*, or to the end-point of *stmt* if there is no else clause.</span></span>

#### <a name="switch-statements"></a><span data-ttu-id="b3bf2-275">Switch 문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-275">Switch statements</span></span>

<span data-ttu-id="b3bf2-276">에 `switch` 문 *stmt* 제어 식을 사용 하 여 *expr*:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-276">In a `switch` statement *stmt* with a controlling expression *expr*:</span></span>

*  <span data-ttu-id="b3bf2-277">한정 된 할당 상태 *v* 부분 *expr* 의 상태와 같습니다 *v* 맨 앞에 *stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-277">The definite assignment state of *v* at the beginning of *expr* is the same as the state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-278">한정 된 할당 상태의 *v* 제어 흐름에 연결할 수 있는 스위치 블록 문 목록에 전송할 같습니다의 한정 된 할당 상태 *v* 끝날 때 *expr*.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-278">The definite assignment state of *v* on the control flow transfer to a reachable switch block statement list is the same as the definite assignment state of *v* at the end of *expr*.</span></span>

#### <a name="while-statements"></a><span data-ttu-id="b3bf2-279">While 문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-279">While statements</span></span>

<span data-ttu-id="b3bf2-280">에 `while` 문 *stmt* 폼의:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-280">For a `while` statement *stmt* of the form:</span></span>
```csharp
while ( expr ) while_body
```

*  <span data-ttu-id="b3bf2-281">*v* 맨 앞에 한정 된 할당 상태가 동일한 *expr* 의 시작 부분으로 *stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-281">*v* has the same definite assignment state at the beginning of *expr* as at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-282">하는 경우 *v* 끝에 정적으로 할당 됩니다 *expr*, 제어 흐름 전송에서 확실 하 게 할당 한 다음 *while_body* 를 끝점에  *stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-282">If *v* is definitely assigned at the end of *expr*, then it is definitely assigned on the control flow transfer to *while_body* and to the end point of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-283">하는 경우 *v* 끝에 "true 식 뒤 확실 하 게 할당 된" 상태를 갖습니까 *expr*, 제어 흐름 전송에 정적으로 할당은 다음 *while_body*, 있지만 끝점의 할당 *stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-283">If *v* has the state "definitely assigned after true expression" at the end of *expr*, then it is definitely assigned on the control flow transfer to *while_body*, but not definitely assigned at the end-point of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-284">하는 경우 *v* 끝에 "정적 false 식으로 할당" 상태를 갖습니까 *expr*, 확실 하 게 제어 흐름 전송의 끝점에 할당 한 다음 *stmt* 있지만 제어 흐름 전송에서 확실 하 게 할당 되지 않음 *while_body*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-284">If *v* has the state "definitely assigned after false expression" at the end of *expr*, then it is definitely assigned on the control flow transfer to the end point of *stmt*, but not definitely assigned on the control flow transfer to *while_body*.</span></span>

#### <a name="do-statements"></a><span data-ttu-id="b3bf2-285">문을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-285">Do statements</span></span>

<span data-ttu-id="b3bf2-286">에 `do` 문 *stmt* 폼의:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-286">For a `do` statement *stmt* of the form:</span></span>
```csharp
do do_body while ( expr ) ;
```

*  <span data-ttu-id="b3bf2-287">*v* 제어 흐름 전송의 처음부터 같은 한정 된 할당 상태를 갖습니까 *stmt* 하 *do_body* 의 시작 부분으로 *stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-287">*v* has the same definite assignment state on the control flow transfer from the beginning of *stmt* to *do_body* as at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-288">*v* 맨 앞에 한정 된 할당 상태가 동일한 *expr* 끝점와 마찬가지로 *do_body*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-288">*v* has the same definite assignment state at the beginning of *expr* as at the end point of *do_body*.</span></span>
*  <span data-ttu-id="b3bf2-289">하는 경우 *v* 끝에 정적으로 할당 됩니다 *expr*, 확실 하 게 제어 흐름 전송의 끝점에 할당 한 다음 *stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-289">If *v* is definitely assigned at the end of *expr*, then it is definitely assigned on the control flow transfer to the end point of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-290">하는 경우 *v* 끝에 "정적 false 식으로 할당" 상태를 갖습니까 *expr*, 확실 하 게 제어 흐름 전송의 끝점에 할당 한 다음 *stmt* .</span><span class="sxs-lookup"><span data-stu-id="b3bf2-290">If *v* has the state "definitely assigned after false expression" at the end of *expr*, then it is definitely assigned on the control flow transfer to the end point of *stmt*.</span></span>

#### <a name="for-statements"></a><span data-ttu-id="b3bf2-291">문에 대 한</span><span class="sxs-lookup"><span data-stu-id="b3bf2-291">For statements</span></span>

<span data-ttu-id="b3bf2-292">한정 된 할당에 대 한 검사는 `for` 폼의 문:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-292">Definite assignment checking for a `for` statement of the form:</span></span>
```csharp
for ( for_initializer ; for_condition ; for_iterator ) embedded_statement
```
<span data-ttu-id="b3bf2-293">문을 작성 된 것 처럼 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-293">is done as if the statement were written:</span></span>
```csharp
{
for_initializer ;
while ( for_condition ) {
embedded_statement ;
for_iterator ;
}
}
```

<span data-ttu-id="b3bf2-294">경우는 *for_condition* 에서 생략 되는 `for` 문을 다음 진행 한정 된 할당의 평가 처럼 *for_condition* 대체 됨 `true` 위의 확장 .</span><span class="sxs-lookup"><span data-stu-id="b3bf2-294">If the *for_condition* is omitted from the `for` statement, then evaluation of definite assignment proceeds as if *for_condition* were replaced with `true` in the above expansion.</span></span>

#### <a name="break-continue-and-goto-statements"></a><span data-ttu-id="b3bf2-295">중단, 계속 및 goto 문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-295">Break, continue, and goto statements</span></span>

<span data-ttu-id="b3bf2-296">한정 된 할당 상태 *v* 인해 제어 흐름 전송에는 `break`, `continue`, 또는 `goto` 문을의 한정 된 할당 상태와 같습니다 *v* 에 문의 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-296">The definite assignment state of *v* on the control flow transfer caused by a `break`, `continue`, or `goto` statement is the same as the definite assignment state of *v* at the beginning of the statement.</span></span>

#### <a name="throw-statements"></a><span data-ttu-id="b3bf2-297">Throw 문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-297">Throw statements</span></span>

<span data-ttu-id="b3bf2-298">문에 대 한 *stmt* 형식의</span><span class="sxs-lookup"><span data-stu-id="b3bf2-298">For a statement *stmt* of the form</span></span>
```csharp
throw expr ;
```

<span data-ttu-id="b3bf2-299">한정 된 할당 상태의 *v* 부분 *expr* 의 한정 된 할당 상태와 같습니다 *v* 맨 앞에 *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-299">The definite assignment state of *v* at the beginning of *expr* is the same as the definite assignment state of *v* at the beginning of *stmt*.</span></span>

#### <a name="return-statements"></a><span data-ttu-id="b3bf2-300">Return 문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-300">Return statements</span></span>

<span data-ttu-id="b3bf2-301">문에 대 한 *stmt* 형식의</span><span class="sxs-lookup"><span data-stu-id="b3bf2-301">For a statement *stmt* of the form</span></span>
```csharp
return expr ;
```

*  <span data-ttu-id="b3bf2-302">한정 된 할당 상태의 *v* 부분 *expr* 의 한정 된 할당 상태와 같습니다 *v* 맨 앞에 *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-302">The definite assignment state of *v* at the beginning of *expr* is the same as the definite assignment state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-303">하는 경우 *v* 확실 하 게 할당 해야 하거나 출력 매개 변수를가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-303">If *v* is an output parameter, then it must be definitely assigned either:</span></span>
    * <span data-ttu-id="b3bf2-304">후 *expr*</span><span class="sxs-lookup"><span data-stu-id="b3bf2-304">after *expr*</span></span>
    * <span data-ttu-id="b3bf2-305">또는 끝에 `finally` 블록을 `try` - `finally` 또는 `try` - `catch` - `finally` 포함 하는 `return` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-305">or at the end of the `finally` block of a `try`-`finally` or `try`-`catch`-`finally` that encloses the `return` statement.</span></span>

<span data-ttu-id="b3bf2-306">폼의 문 stmt에 대 한:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-306">For a statement stmt of the form:</span></span>
```csharp
return ;
```

*  <span data-ttu-id="b3bf2-307">하는 경우 *v* 확실 하 게 할당 해야 하거나 출력 매개 변수를가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-307">If *v* is an output parameter, then it must be definitely assigned either:</span></span>
    * <span data-ttu-id="b3bf2-308">전에 *stmt*</span><span class="sxs-lookup"><span data-stu-id="b3bf2-308">before *stmt*</span></span>
    * <span data-ttu-id="b3bf2-309">또는 끝에 `finally` 블록을 `try` - `finally` 또는 `try` - `catch` - `finally` 포함 하는 `return` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-309">or at the end of the `finally` block of a `try`-`finally` or `try`-`catch`-`finally` that encloses the `return` statement.</span></span>

#### <a name="try-catch-statements"></a><span data-ttu-id="b3bf2-310">Try / catch 문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-310">Try-catch statements</span></span>

<span data-ttu-id="b3bf2-311">문에 대 한 *stmt* 형식:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-311">For a statement *stmt* of the form:</span></span>
```csharp
try try_block
catch(...) catch_block_1
...
catch(...) catch_block_n
```

*  <span data-ttu-id="b3bf2-312">한정 된 할당 상태의 *v* 부분 *try_block* 의 한정 된 할당 상태와 같습니다 *v* 맨 앞에 *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-312">The definite assignment state of *v* at the beginning of *try_block* is the same as the definite assignment state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-313">한정 된 할당 상태 *v* 부분 *catch_block_i* (에 대 한 *합니까*)의 한정 된 할당 상태와 같습니다 *v*의 시작 부분 *stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-313">The definite assignment state of *v* at the beginning of *catch_block_i* (for any *i*) is the same as the definite assignment state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-314">한정 된 할당 상태의 *v* 끝점의 *stmt* 정적으로 할당 된 경우 (및 경우에만)은 *v* 끝점의 확실 하 게 할당 된  *try_block* 매 *catch_block_i* (에 대 한 모든 *합니까* 1 ~ *n*).</span><span class="sxs-lookup"><span data-stu-id="b3bf2-314">The definite assignment state of *v* at the end-point of *stmt* is definitely assigned if (and only if) *v* is definitely assigned at the end-point of *try_block* and every *catch_block_i* (for every *i* from 1 to *n*).</span></span>

#### <a name="try-finally-statements"></a><span data-ttu-id="b3bf2-315">Try finally 문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-315">Try-finally statements</span></span>

<span data-ttu-id="b3bf2-316">에 `try` 문 *stmt* 폼의:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-316">For a `try` statement *stmt* of the form:</span></span>
```csharp
try try_block finally finally_block
```

*  <span data-ttu-id="b3bf2-317">한정 된 할당 상태의 *v* 부분 *try_block* 의 한정 된 할당 상태와 같습니다 *v* 맨 앞에 *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-317">The definite assignment state of *v* at the beginning of *try_block* is the same as the definite assignment state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-318">한정 된 할당 상태의 *v* 부분 *finally_block* 한정 된 할당 상태와 같습니다 *v* 맨 앞에 *stmt* .</span><span class="sxs-lookup"><span data-stu-id="b3bf2-318">The definite assignment state of *v* at the beginning of *finally_block* is the same as the definite assignment state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-319">한정 된 할당 상태의 *v* 끝점의 *stmt* 정적으로 할당 된 경우 (및 경우에만)는 다음 중 하나 이상:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-319">The definite assignment state of *v* at the end-point of *stmt* is definitely assigned if (and only if) at least one of the following is true:</span></span>
    * <span data-ttu-id="b3bf2-320">*v* 끝점의 확실 하 게 할당 된 *try_block*</span><span class="sxs-lookup"><span data-stu-id="b3bf2-320">*v* is definitely assigned at the end-point of *try_block*</span></span>
    * <span data-ttu-id="b3bf2-321">*v* 끝점의 확실 하 게 할당 된 *finally_block*</span><span class="sxs-lookup"><span data-stu-id="b3bf2-321">*v* is definitely assigned at the end-point of *finally_block*</span></span>

<span data-ttu-id="b3bf2-322">경우 제어 흐름 전송 (예를 들어를 `goto` 문)는 만들어질 내에서 시작 *try_block*, 외부 종료 *try_block*, 한 다음 *v* 이기도 경우에 제어 흐름 전송을 정적으로 할당 된 것으로 간주 *v* 끝점의 정적으로 할당 됩니다 *finally_block*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-322">If a control flow transfer (for example, a `goto` statement) is made that begins within *try_block*, and ends outside of *try_block*, then *v* is also considered definitely assigned on that control flow transfer if *v* is definitely assigned at the end-point of *finally_block*.</span></span> <span data-ttu-id="b3bf2-323">(경우에만 아닙니다.-하는 경우 *v* 는 정적으로 할당 된 비율은이 제어 흐름 전송에서 다른 이유로 확실 하 게 할당 합니다.)</span><span class="sxs-lookup"><span data-stu-id="b3bf2-323">(This is not an only if—if *v* is definitely assigned for another reason on this control flow transfer, then it is still considered definitely assigned.)</span></span>

#### <a name="try-catch-finally-statements"></a><span data-ttu-id="b3bf2-324">Try – catch – finally 문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-324">Try-catch-finally statements</span></span>

<span data-ttu-id="b3bf2-325">에 대 한 한정 된 할당 분석을 `try` - `catch` - `finally` 폼의 문:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-325">Definite assignment analysis for a `try`-`catch`-`finally` statement of the form:</span></span>
```csharp
try try_block
catch(...) catch_block_1
...
catch(...) catch_block_n
finally *finally_block*
```
<span data-ttu-id="b3bf2-326">문 처럼 수행 됩니다는 `try` - `finally` 문 바깥쪽을 `try` - `catch` 문:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-326">is done as if the statement were a `try`-`finally` statement enclosing a `try`-`catch` statement:</span></span>
```csharp
try {
try try_block
catch(...) catch_block_1
...
catch(...) catch_block_n
}
finally finally_block
```

<span data-ttu-id="b3bf2-327">다음 예제에서는 어떻게 다른 블록을를 `try` 문 ([try 문](statements.md#the-try-statement)) 한정 된 할당에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-327">The following example demonstrates how the different blocks of a `try` statement ([The try statement](statements.md#the-try-statement)) affect definite assignment.</span></span>
```csharp
class A
{
static void F() {
int i, j;
try {
goto LABEL;
// neither i nor j definitely assigned
i = 1;
// i definitely assigned
}

catch {
// neither i nor j definitely assigned
i = 3;
// i definitely assigned
}

finally {
// neither i nor j definitely assigned
j = 5;
// j definitely assigned
}
// i and j definitely assigned
LABEL:;
// j definitely assigned

}
}
```

#### <a name="foreach-statements"></a><span data-ttu-id="b3bf2-328">Foreach 문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-328">Foreach statements</span></span>

<span data-ttu-id="b3bf2-329">에 `foreach` 문 *stmt* 폼의:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-329">For a `foreach` statement *stmt* of the form:</span></span>
```csharp
foreach ( type identifier in expr ) embedded_statement
```

*  <span data-ttu-id="b3bf2-330">한정 된 할당 상태 *v* 부분 *expr* 의 상태와 같습니다 *v* 맨 앞에 *stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-330">The definite assignment state of *v* at the beginning of *expr* is the same as the state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-331">한정 된 할당 상태의 *v* 제어 흐름 전송의 *embedded_statement* 또는 끝점 *stmt* 의 상태와 같습니다 *v* 끝날 때 *expr*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-331">The definite assignment state of *v* on the control flow transfer to *embedded_statement* or to the end point of *stmt* is the same as the state of *v* at the end of *expr*.</span></span>

#### <a name="using-statements"></a><span data-ttu-id="b3bf2-332">문을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b3bf2-332">Using statements</span></span>

<span data-ttu-id="b3bf2-333">에 `using` 문 *stmt* 폼의:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-333">For a `using` statement *stmt* of the form:</span></span>
```csharp
using ( resource_acquisition ) embedded_statement
```

*  <span data-ttu-id="b3bf2-334">한정 된 할당 상태의 *v* 부분 *resource_acquisition* 의 상태와 같습니다 *v* 맨 앞에 *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-334">The definite assignment state of *v* at the beginning of *resource_acquisition* is the same as the state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-335">한정 된 할당 상태의 *v* 제어 흐름 전송의 *embedded_statement* 의 상태와 동일 *v* 끝에 *resource_ 취득*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-335">The definite assignment state of *v* on the control flow transfer to *embedded_statement* is the same as the state of *v* at the end of *resource_acquisition*.</span></span>

#### <a name="lock-statements"></a><span data-ttu-id="b3bf2-336">Lock 문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-336">Lock statements</span></span>

<span data-ttu-id="b3bf2-337">에 `lock` 문 *stmt* 폼의:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-337">For a `lock` statement *stmt* of the form:</span></span>
```csharp
lock ( expr ) embedded_statement
```

*  <span data-ttu-id="b3bf2-338">한정 된 할당 상태 *v* 부분 *expr* 의 상태와 같습니다 *v* 맨 앞에 *stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-338">The definite assignment state of *v* at the beginning of *expr* is the same as the state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-339">한정 된 할당 상태의 *v* 제어 흐름 전송의 *embedded_statement* 의 상태와 동일 *v* 끝에 *expr*.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-339">The definite assignment state of *v* on the control flow transfer to *embedded_statement* is the same as the state of *v* at the end of *expr*.</span></span>

#### <a name="yield-statements"></a><span data-ttu-id="b3bf2-340">Yield 문</span><span class="sxs-lookup"><span data-stu-id="b3bf2-340">Yield statements</span></span>

<span data-ttu-id="b3bf2-341">에 `yield return` 문 *stmt* 폼의:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-341">For a `yield return` statement *stmt* of the form:</span></span>
```csharp
yield return expr ;
```

*  <span data-ttu-id="b3bf2-342">한정 된 할당 상태 *v* 부분 *expr* 의 상태와 같습니다 *v* 맨 앞에 *stmt*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-342">The definite assignment state of *v* at the beginning of *expr* is the same as the state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b3bf2-343">한정 된 할당 상태의 *v* 끝 *stmt* 의 상태와 같습니다 *v* 끝에 *expr*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-343">The definite assignment state of *v* at the end of *stmt* is the same as the state of *v* at the end of *expr*.</span></span>
*  <span data-ttu-id="b3bf2-344">`yield break` 문에 한정 된 할당 상태에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-344">A `yield break` statement has no effect on the definite assignment state.</span></span>

#### <a name="general-rules-for-simple-expressions"></a><span data-ttu-id="b3bf2-345">간단한 식에 대 한 일반 규칙</span><span class="sxs-lookup"><span data-stu-id="b3bf2-345">General rules for simple expressions</span></span>

<span data-ttu-id="b3bf2-346">이러한 종류의 식이 다음 규칙이 적용: 리터럴 ([리터럴](expressions.md#literals)), 단순한 이름 ([단순 이름](expressions.md#simple-names)), 멤버 액세스 식 ([멤버 액세스](expressions.md#member-access)), 인덱싱되지 않은 기본 액세스 식 ([액세스를 기본](expressions.md#base-access)), `typeof` 식 ([typeof 연산자](expressions.md#the-typeof-operator)), 기본값 식 ([기본 값 식 ](expressions.md#default-value-expressions)) 및 `nameof` 식 ([Nameof 식](expressions.md#nameof-expressions)).</span><span class="sxs-lookup"><span data-stu-id="b3bf2-346">The following rule applies to these kinds of expressions: literals ([Literals](expressions.md#literals)), simple names ([Simple names](expressions.md#simple-names)), member access expressions ([Member access](expressions.md#member-access)), non-indexed base access expressions ([Base access](expressions.md#base-access)), `typeof` expressions ([The typeof operator](expressions.md#the-typeof-operator)), default value expressions ([Default value expressions](expressions.md#default-value-expressions)) and `nameof` expressions ([Nameof expressions](expressions.md#nameof-expressions)).</span></span>

*  <span data-ttu-id="b3bf2-347">한정 된 할당 상태의 *v* 식의 끝에 한정 된 할당 상태와 같습니다 *v* 식의 시작 부분에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-347">The definite assignment state of *v* at the end of such an expression is the same as the definite assignment state of *v* at the beginning of the expression.</span></span>

#### <a name="general-rules-for-expressions-with-embedded-expressions"></a><span data-ttu-id="b3bf2-348">포함 된 식 사용 하 여 식에 대 한 일반 규칙</span><span class="sxs-lookup"><span data-stu-id="b3bf2-348">General rules for expressions with embedded expressions</span></span>

<span data-ttu-id="b3bf2-349">이러한 종류의 식에는 다음 규칙이 적용 됩니다: 괄호로 묶인 식 ([괄호로 묶인 식](expressions.md#parenthesized-expressions)), 요소 액세스 식을 ([요소 액세스](expressions.md#element-access)) 기본 식을 사용 하 여 액세스 인덱싱 ([액세스를 기본](expressions.md#base-access)), 증가 및 감소 식은 ([후 위 증가 및 감소 연산자](expressions.md#postfix-increment-and-decrement-operators), [전위 증가 및 감소 연산자](expressions.md#prefix-increment-and-decrement-operators)), 캐스트 식 ([캐스트 식](expressions.md#cast-expressions)), 단항 `+`, `-`, `~`합니다 `*` 이진 식 `+`, `-`, `*`, `/`, `%`, `<<`, `>>`, `<`, `<=`, `>`, `>=`, `==`, `!=`, `is`, `as`, `&`, `|`, `^` 식 ([산술 연산자](expressions.md#arithmetic-operators)하십시오 [시프트 연산자](expressions.md#shift-operators), [관계형 및 형식 테스트 연산자](expressions.md#relational-and-type-testing-operators) 를 [논리 연산자](expressions.md#logical-operators)), 복합 대입 식 ([복합 할당](expressions.md#compound-assignment)), `checked` 하 고 `unchecked` 식 ([checked 및 unchecked 연산자](expressions.md#the-checked-and-unchecked-operators)), 배열 및 대리자 생성 식 더하기 ([new 연산자](expressions.md#the-new-operator)).</span><span class="sxs-lookup"><span data-stu-id="b3bf2-349">The following rules apply to these kinds of expressions: parenthesized expressions ([Parenthesized expressions](expressions.md#parenthesized-expressions)), element access expressions ([Element access](expressions.md#element-access)), base access expressions with indexing ([Base access](expressions.md#base-access)), increment and decrement expressions ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators), [Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)), cast expressions ([Cast expressions](expressions.md#cast-expressions)), unary `+`, `-`, `~`, `*` expressions, binary `+`, `-`, `*`, `/`, `%`, `<<`, `>>`, `<`, `<=`, `>`, `>=`, `==`, `!=`, `is`, `as`, `&`, `|`, `^` expressions ([Arithmetic operators](expressions.md#arithmetic-operators), [Shift operators](expressions.md#shift-operators), [Relational and type-testing operators](expressions.md#relational-and-type-testing-operators), [Logical operators](expressions.md#logical-operators)), compound assignment expressions ([Compound assignment](expressions.md#compound-assignment)), `checked` and `unchecked` expressions ([The checked and unchecked operators](expressions.md#the-checked-and-unchecked-operators)), plus array and delegate creation expressions ([The new operator](expressions.md#the-new-operator)).</span></span>

<span data-ttu-id="b3bf2-350">이러한 식의 각 고정 된 순서로 무조건 평가 되는 하나 이상의 하위 식에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-350">Each of these expressions has one or more sub-expressions that are unconditionally evaluated in a fixed order.</span></span> <span data-ttu-id="b3bf2-351">예를 들어 이진 `%` 연산자의 왼쪽을 오른쪽 연산자를 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-351">For example, the binary `%` operator evaluates the left hand side of the operator, then the right hand side.</span></span> <span data-ttu-id="b3bf2-352">인덱싱 작업 인덱싱된 식을 계산 하 고 인덱스 식의 왼쪽에서 오른쪽 순서로 각각를 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-352">An indexing operation evaluates the indexed expression, and then evaluates each of the index expressions, in order from left to right.</span></span> <span data-ttu-id="b3bf2-353">식에 대 한 *expr*에 하위 식이 *(e1, e2,..., eN*, 지정 된 순서로 평가:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-353">For an expression *expr*, which has sub-expressions *e1, e2, ..., eN*, evaluated in that order:</span></span>

*  <span data-ttu-id="b3bf2-354">한정 된 할당 상태의 *v* 부분 *e1* 맨 앞에 한정 된 할당 상태와 같습니다 *expr*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-354">The definite assignment state of *v* at the beginning of *e1* is the same as the definite assignment state at the beginning of *expr*.</span></span>
*  <span data-ttu-id="b3bf2-355">한정 된 할당 상태 *v* 부분 *ei* (*i* 1 보다 큰) 이전 하위 식의 끝에 한정 된 할당 상태와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-355">The definite assignment state of *v* at the beginning of *ei* (*i* greater than one) is the same as the definite assignment state at the end of the previous sub-expression.</span></span>
*  <span data-ttu-id="b3bf2-356">한정 된 할당 상태의 *v* 끝 *expr* 끝에 한정 된 할당 상태와 같습니다 *eN*</span><span class="sxs-lookup"><span data-stu-id="b3bf2-356">The definite assignment state of *v* at the end of *expr* is the same as the definite assignment state at the end of *eN*</span></span>

#### <a name="invocation-expressions-and-object-creation-expressions"></a><span data-ttu-id="b3bf2-357">호출 식 및 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="b3bf2-357">Invocation expressions and object creation expressions</span></span>

<span data-ttu-id="b3bf2-358">호출 식에 대 한 *expr* 형식:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-358">For an invocation expression *expr* of the form:</span></span>
```csharp
primary_expression ( arg1 , arg2 , ... , argN )
```
<span data-ttu-id="b3bf2-359">또는 개체 만들기 식 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-359">or an object creation expression of the form:</span></span>
```csharp
new type ( arg1 , arg2 , ... , argN )
```

*  <span data-ttu-id="b3bf2-360">호출 식의 한정 된 할당 상태에 대 한 *v* 하기 전에 *primary_expression* 상태의 동일 *v* 전에 *expr*.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-360">For an invocation expression, the definite assignment state of *v* before *primary_expression* is the same as the state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b3bf2-361">호출 식의 한정 된 할당 상태에 대 한 *v* 하기 전에 *arg1* 상태의 동일 *v* 후 *primary_expression*.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-361">For an invocation expression, the definite assignment state of *v* before *arg1* is the same as the state of *v* after *primary_expression*.</span></span>
*  <span data-ttu-id="b3bf2-362">개체 생성 식의 한정 된 할당 상태에 대 한 *v* 하기 전에 *arg1* 상태의 동일 *v* 전에 *expr*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-362">For an object creation expression, the definite assignment state of *v* before *arg1* is the same as the state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b3bf2-363">각 인수에 대 한 *argi*에 한정 된 할당 상태 *v* 후 *argi* 무시 하 고 일반 식 규칙에 의해 결정 됩니다 `ref` 또는`out`한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-363">For each argument *argi*, the definite assignment state of *v* after *argi* is determined by the normal expression rules, ignoring any `ref` or `out` modifiers.</span></span>
*  <span data-ttu-id="b3bf2-364">각 인수에 대 한 *argi* 에 대 한 *합니까* 한정 된 할당 상태를 1 보다 큰 *v* 앞 *argi* 의 상태와 동일 *v* 이전 *arg*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-364">For each argument *argi* for any *i* greater than one, the definite assignment state of *v* before *argi* is the same as the state of *v* after the previous *arg*.</span></span>
*  <span data-ttu-id="b3bf2-365">경우 변수 *v* 로 전달 되는 `out` 인수 (즉, 폼의 인수 `out v`) 인수는 다음 상태 중 하나에서 *v* 후 *expr* 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-365">If the variable *v* is passed as an `out` argument (i.e., an argument of the form `out v`) in any of the arguments, then the state of *v* after *expr* is definitely assigned.</span></span> <span data-ttu-id="b3bf2-366">그렇지 않으면; 상태의 *v* 한 후 *expr* 의 상태와 동일 *v* 후 *argN*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-366">Otherwise; the state of *v* after *expr* is the same as the state of *v* after *argN*.</span></span>
*  <span data-ttu-id="b3bf2-367">배열 이니셜라이저에 대 한 ([배열 만들기 식을](expressions.md#array-creation-expressions)), 개체 이니셜라이저 ([개체 이니셜라이저](expressions.md#object-initializers)), 컬렉션 이니셜라이저 ([컬렉션 이니셜라이저](expressions.md#collection-initializers)) 및 익명 개체 이니셜라이저 ([익명 개체 생성 식을](expressions.md#anonymous-object-creation-expressions))에 한정 된 할당 상태는 이러한 구문의 측면에서 정의 된 확장에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-367">For array initializers ([Array creation expressions](expressions.md#array-creation-expressions)), object initializers ([Object initializers](expressions.md#object-initializers)), collection initializers ([Collection initializers](expressions.md#collection-initializers)) and anonymous object initializers ([Anonymous object creation expressions](expressions.md#anonymous-object-creation-expressions)), the definite assignment state is determined by the expansion that these constructs are defined in terms of.</span></span>

#### <a name="simple-assignment-expressions"></a><span data-ttu-id="b3bf2-368">단순 할당 식</span><span class="sxs-lookup"><span data-stu-id="b3bf2-368">Simple assignment expressions</span></span>

<span data-ttu-id="b3bf2-369">식에 대 한 *expr* 양식의 `w = expr_rhs`:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-369">For an expression *expr* of the form `w = expr_rhs`:</span></span>

*  <span data-ttu-id="b3bf2-370">한정 된 할당 상태의 *v* 하기 전에 *expr_rhs* 한정 된 할당 상태와 동일 *v* 전에 *expr*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-370">The definite assignment state of *v* before *expr_rhs* is the same as the definite assignment state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b3bf2-371">한정 된 할당 상태의 *v* 한 후 *expr* 에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-371">The definite assignment state of *v* after *expr* is determined by:</span></span>
   * <span data-ttu-id="b3bf2-372">하는 경우 *w* 으로 동일한 변수가 *v*, 한정 된 할당 상태 *v* 후 *expr* 정적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-372">If *w* is the same variable as *v*, then the definite assignment state of *v* after *expr* is definitely assigned.</span></span>
   * <span data-ttu-id="b3bf2-373">할당 하는 경우 구조체 형식의 인스턴스 생성자 내에서 발생 하는 경우 그러지 *w* 가 자동으로 구현 된 속성을 지정 합니다. 속성 액세스 *P* 생성 되는 인스턴스에서 및 *v* 의 숨겨진된 지원 필드는 *P*에 한정 된 할당 상태 *v* 후 *expr* 확실히 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-373">Otherwise, if the assignment occurs within the instance constructor of a struct type, if *w* is a property access designating an automatically implemented property *P* on the instance being constructed and *v* is the hidden backing field of *P*, then the definite assignment state of *v* after *expr* is definitely assigned.</span></span>
   * <span data-ttu-id="b3bf2-374">이 고, 그렇지 한정 된 할당 상태의 *v* 한 후 *expr* 한정 된 할당 상태와 같습니다 *v* 후 *expr_rhs*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-374">Otherwise, the definite assignment state of *v* after *expr* is the same as the definite assignment state of *v* after *expr_rhs*.</span></span>

#### <a name="-conditional-and-expressions"></a><span data-ttu-id="b3bf2-375">& & (AND 조건부) 식</span><span class="sxs-lookup"><span data-stu-id="b3bf2-375">&& (conditional AND) expressions</span></span>

<span data-ttu-id="b3bf2-376">식에 대 한 *expr* 양식의 `expr_first && expr_second`:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-376">For an expression *expr* of the form `expr_first && expr_second`:</span></span>

*  <span data-ttu-id="b3bf2-377">한정 된 할당 상태의 *v* 하기 전에 *expr_first* 한정 된 할당 상태와 동일 *v* 전에 *expr*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-377">The definite assignment state of *v* before *expr_first* is the same as the definite assignment state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b3bf2-378">한정 된 할당 상태의 *v* 하기 전에 *expr_second* 경우 확실 하 게 할당 된 상태의 *v* 후 *expr_first* 는 정적으로 할당 또는 "정적으로 할당 된 true 식 뒤"입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-378">The definite assignment state of *v* before *expr_second* is definitely assigned if the state of *v* after *expr_first* is either definitely assigned or "definitely assigned after true expression".</span></span> <span data-ttu-id="b3bf2-379">그렇지 않으면 할당 되지 않은 확실 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-379">Otherwise, it is not definitely assigned.</span></span>
*  <span data-ttu-id="b3bf2-380">한정 된 할당 상태의 *v* 한 후 *expr* 에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-380">The definite assignment state of *v* after *expr* is determined by:</span></span>
    * <span data-ttu-id="b3bf2-381">하는 경우 *expr_first* 는 값을 사용 하 여 상수 식 `false`, 한정 된 할당 상태 *v* 후 *expr* 한정 된 할당와 동일 상태 *v* 한 후 *expr_first*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-381">If *expr_first* is a constant expression with the value `false`, then the definite assignment state of *v* after *expr* is the same as the definite assignment state of *v* after *expr_first*.</span></span>
    * <span data-ttu-id="b3bf2-382">그렇지 않은 경우, 상태 *v* 후 *expr_first* 확실 하 게 할당 되 면 다음 상태의 *v* 후 *expr* 정적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-382">Otherwise, if the state of *v* after *expr_first* is definitely assigned, then the state of *v* after *expr* is definitely assigned.</span></span>
    * <span data-ttu-id="b3bf2-383">그렇지 않은 경우, 상태 *v* 후 *expr_second* 확실 하 게 할당 된 및 상태의 *v* 후 *expr_first* 확실히 " false 식 "을 할당 한 다음 상태의 *v* 한 후 *expr* 정적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-383">Otherwise, if the state of *v* after *expr_second* is definitely assigned, and the state of *v* after *expr_first* is "definitely assigned after false expression", then the state of *v* after *expr* is definitely assigned.</span></span>
    * <span data-ttu-id="b3bf2-384">그렇지 않은 경우, 상태 *v* 후 *expr_second* 정적으로 할당 하거나 "정적으로 할당 된 true 식 뒤"에 다음 상태의 *v* 후  *expr* "확실 하 게 할당 된 true 식 뒤"입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-384">Otherwise, if the state of *v* after *expr_second* is definitely assigned or "definitely assigned after true expression", then the state of *v* after *expr* is "definitely assigned after true expression".</span></span>
    * <span data-ttu-id="b3bf2-385">그렇지 않은 경우, 상태 *v* 한 후 *expr_first* "정적으로 할당 된 후 false 식", 및의 상태는 *v* 후 *expr_second* 가 "대입할 false 식 뒤" 상태의 *v* 한 후 *expr* "확실 하 게 할당 된 후 false 식"입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-385">Otherwise, if the state of *v* after *expr_first* is "definitely assigned after false expression", and the state of *v* after *expr_second* is "definitely assigned after false expression", then the state of *v* after *expr* is "definitely assigned after false expression".</span></span>
    * <span data-ttu-id="b3bf2-386">이 고, 그렇지 상태의 *v* 한 후 *expr* 확실 하 게 할당 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-386">Otherwise, the state of *v* after *expr* is not definitely assigned.</span></span>

<span data-ttu-id="b3bf2-387">예제</span><span class="sxs-lookup"><span data-stu-id="b3bf2-387">In the example</span></span>
```csharp
class A
{
    static void F(int x, int y) {
        int i;
        if (x >= 0 && (i = y) >= 0) {
            // i definitely assigned
        }
        else {
            // i not definitely assigned
        }
        // i not definitely assigned
    }
}
```
<span data-ttu-id="b3bf2-388">변수의 `i` 의 포함 된 문 중 하나에서 정적으로 할당 된 것으로 간주 됩니다는 `if` 문이 아니라 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-388">the variable `i` is considered definitely assigned in one of the embedded statements of an `if` statement but not in the other.</span></span> <span data-ttu-id="b3bf2-389">`if` 메서드의 문은 `F`, 변수의 `i` 때문에 포함 된 첫 번째 문에서 확실 하 게 할당 되었습니다 식 실행 `(i = y)` 앞에 항상이 포함 된 문 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-389">In the `if` statement in method `F`, the variable `i` is definitely assigned in the first embedded statement because execution of the expression `(i = y)` always precedes execution of this embedded statement.</span></span> <span data-ttu-id="b3bf2-390">반대로, 변수의 `i` 할당 되지 않은 확실 하 게 두 번째는 포함 된 문에서 이후에 `x >= 0` 수 테스트 false, 변수에 결과 `i` 할당 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-390">In contrast, the variable `i` is not definitely assigned in the second embedded statement, since `x >= 0` might have tested false, resulting in the variable `i` being unassigned.</span></span>

#### <a name="-conditional-or-expressions"></a><span data-ttu-id="b3bf2-391">|| (조건부 OR) 식</span><span class="sxs-lookup"><span data-stu-id="b3bf2-391">|| (conditional OR) expressions</span></span>

<span data-ttu-id="b3bf2-392">식에 대 한 *expr* 양식의 `expr_first || expr_second`:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-392">For an expression *expr* of the form `expr_first || expr_second`:</span></span>

*  <span data-ttu-id="b3bf2-393">한정 된 할당 상태의 *v* 하기 전에 *expr_first* 한정 된 할당 상태와 동일 *v* 전에 *expr*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-393">The definite assignment state of *v* before *expr_first* is the same as the definite assignment state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b3bf2-394">한정 된 할당 상태의 *v* 하기 전에 *expr_second* 경우 확실 하 게 할당 된 상태의 *v* 후 *expr_first* 는 정적으로 할당 또는 "정적으로 할당 된 후 false 식"입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-394">The definite assignment state of *v* before *expr_second* is definitely assigned if the state of *v* after *expr_first* is either definitely assigned or "definitely assigned after false expression".</span></span> <span data-ttu-id="b3bf2-395">그렇지 않으면 할당 되지 않은 확실 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-395">Otherwise, it is not definitely assigned.</span></span>
*  <span data-ttu-id="b3bf2-396">한정 된 할당 설명이 *v* 한 후 *expr* 에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-396">The definite assignment statement of *v* after *expr* is determined by:</span></span>
    * <span data-ttu-id="b3bf2-397">하는 경우 *expr_first* 는 값을 사용 하 여 상수 식 `true`, 한정 된 할당 상태 *v* 후 *expr* 한정 된 할당와 동일 상태 *v* 한 후 *expr_first*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-397">If *expr_first* is a constant expression with the value `true`, then the definite assignment state of *v* after *expr* is the same as the definite assignment state of *v* after *expr_first*.</span></span>
    * <span data-ttu-id="b3bf2-398">그렇지 않은 경우, 상태 *v* 후 *expr_first* 확실 하 게 할당 되 면 다음 상태의 *v* 후 *expr* 정적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-398">Otherwise, if the state of *v* after *expr_first* is definitely assigned, then the state of *v* after *expr* is definitely assigned.</span></span>
    * <span data-ttu-id="b3bf2-399">그렇지 않은 경우, 상태 *v* 후 *expr_second* 확실 하 게 할당 된 및 상태의 *v* 후 *expr_first* 확실히 " 할당 된 true 식 뒤"다음 상태의 *v* 한 후 *expr* 정적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-399">Otherwise, if the state of *v* after *expr_second* is definitely assigned, and the state of *v* after *expr_first* is "definitely assigned after true expression", then the state of *v* after *expr* is definitely assigned.</span></span>
    * <span data-ttu-id="b3bf2-400">그렇지 않은 경우, 상태 *v* 후 *expr_second* 정적으로 할당 하거나 "대입할 false 식 뒤" 다음 상태의 *v* 후*expr* "확실 하 게 할당 된 후 false 식"입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-400">Otherwise, if the state of *v* after *expr_second* is definitely assigned or "definitely assigned after false expression", then the state of *v* after *expr* is "definitely assigned after false expression".</span></span>
    * <span data-ttu-id="b3bf2-401">그렇지 않은 경우, 상태 *v* 한 후 *expr_first* "정적으로 할당 된 true 식 뒤", 및의 상태는 *v* 후 *expr_second*이면 "정적으로 할당 된 true 식 뒤", 상태 *v* 한 후 *expr* "확실 하 게 할당 된 true 식 뒤"입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-401">Otherwise, if the state of *v* after *expr_first* is "definitely assigned after true expression", and the state of *v* after *expr_second* is "definitely assigned after true expression", then the state of *v* after *expr* is "definitely assigned after true expression".</span></span>
    * <span data-ttu-id="b3bf2-402">이 고, 그렇지 상태의 *v* 한 후 *expr* 확실 하 게 할당 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-402">Otherwise, the state of *v* after *expr* is not definitely assigned.</span></span>

<span data-ttu-id="b3bf2-403">예제</span><span class="sxs-lookup"><span data-stu-id="b3bf2-403">In the example</span></span>
```csharp
class A
{
    static void G(int x, int y) {
        int i;
        if (x >= 0 || (i = y) >= 0) {
            // i not definitely assigned
        }
        else {
            // i definitely assigned
        }
        // i not definitely assigned
    }
}
```
<span data-ttu-id="b3bf2-404">변수의 `i` 의 포함 된 문 중 하나에서 정적으로 할당 된 것으로 간주 됩니다는 `if` 문이 아니라 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-404">the variable `i` is considered definitely assigned in one of the embedded statements of an `if` statement but not in the other.</span></span> <span data-ttu-id="b3bf2-405">`if` 메서드의 문은 `G`, 변수의 `i` 때문에 두 번째 포함 된 문에서 확실 하 게 할당 되었습니다 식 실행 `(i = y)` 앞에 항상이 포함 된 문 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-405">In the `if` statement in method `G`, the variable `i` is definitely assigned in the second embedded statement because execution of the expression `(i = y)` always precedes execution of this embedded statement.</span></span> <span data-ttu-id="b3bf2-406">반대로, 변수의 `i` 할당 되지 않은 확실 하 게 첫 번째는 포함 된 문에서 이후에 `x >= 0` 수 테스트 true 인 변수에 결과 `i` 할당 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-406">In contrast, the variable `i` is not definitely assigned in the first embedded statement, since `x >= 0` might have tested true, resulting in the variable `i` being unassigned.</span></span>

#### <a name="-logical-negation-expressions"></a><span data-ttu-id="b3bf2-407">!</span><span class="sxs-lookup"><span data-stu-id="b3bf2-407">!</span></span> <span data-ttu-id="b3bf2-408">(논리적 부정) 식</span><span class="sxs-lookup"><span data-stu-id="b3bf2-408">(logical negation) expressions</span></span>

<span data-ttu-id="b3bf2-409">식에 대 한 *expr* 양식의 `! expr_operand`:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-409">For an expression *expr* of the form `! expr_operand`:</span></span>

*  <span data-ttu-id="b3bf2-410">한정 된 할당 상태의 *v* 하기 전에 *expr_operand* 한정 된 할당 상태와 동일 *v* 전에 *expr*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-410">The definite assignment state of *v* before *expr_operand* is the same as the definite assignment state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b3bf2-411">한정 된 할당 상태의 *v* 한 후 *expr* 에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-411">The definite assignment state of *v* after *expr* is determined by:</span></span>
    * <span data-ttu-id="b3bf2-412">경우 상태의 *v* 후 \* expr_operand \* 확실 하 게 할당 되 면 다음 상태의 *v* 후 *expr* 정적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-412">If the state of *v* after \*expr_operand \*is definitely assigned, then the state of *v* after *expr* is definitely assigned.</span></span>
    * <span data-ttu-id="b3bf2-413">경우 상태의 *v* 후 \* expr_operand \* 확실 하 게를 할당 하지 않으면 다음 상태의 *v* 후 *expr* 확실 하 게 할당 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-413">If the state of *v* after \*expr_operand \*is not definitely assigned, then the state of *v* after *expr* is not definitely assigned.</span></span>
    * <span data-ttu-id="b3bf2-414">경우 상태의 *v* 후 \* expr_operand \* 이면 "정적으로 할당 된 후 false 식"을 상태의 *v* 후 *expr* "확실 하 게 할당 된 후 true 식 "입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-414">If the state of *v* after \*expr_operand \*is "definitely assigned after false expression", then the state of *v* after *expr* is "definitely assigned after true expression".</span></span>
    * <span data-ttu-id="b3bf2-415">경우 상태의 *v* 후 \* expr_operand \* 이면 "정적으로 할당 된 true 식 뒤", 상태의 *v* 후 *expr* "확실 하 게 할당 된 후 false 식 "입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-415">If the state of *v* after \*expr_operand \*is "definitely assigned after true expression", then the state of *v* after *expr* is "definitely assigned after false expression".</span></span>

#### <a name="-null-coalescing-expressions"></a><span data-ttu-id="b3bf2-416">??</span><span class="sxs-lookup"><span data-stu-id="b3bf2-416">??</span></span> <span data-ttu-id="b3bf2-417">식 (null 병합)</span><span class="sxs-lookup"><span data-stu-id="b3bf2-417">(null coalescing) expressions</span></span>

<span data-ttu-id="b3bf2-418">식에 대 한 *expr* 양식의 `expr_first ?? expr_second`:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-418">For an expression *expr* of the form `expr_first ?? expr_second`:</span></span>

*  <span data-ttu-id="b3bf2-419">한정 된 할당 상태의 *v* 하기 전에 *expr_first* 한정 된 할당 상태와 동일 *v* 전에 *expr*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-419">The definite assignment state of *v* before *expr_first* is the same as the definite assignment state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b3bf2-420">한정 된 할당 상태의 *v* 하기 전에 *expr_second* 한정 된 할당 상태와 동일 *v* 후 *expr_first*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-420">The definite assignment state of *v* before *expr_second* is the same as the definite assignment state of *v* after *expr_first*.</span></span>
*  <span data-ttu-id="b3bf2-421">한정 된 할당 설명이 *v* 한 후 *expr* 에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-421">The definite assignment statement of *v* after *expr* is determined by:</span></span>
    * <span data-ttu-id="b3bf2-422">하는 경우 *expr_first* 상수 식입니다 ([상수 식을](expressions.md#constant-expressions)) null 값을 사용 하 여 해당 상태의 *v* 후 *expr* 동일 상태와 *v* 한 후 *expr_second*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-422">If *expr_first* is a constant expression ([Constant expressions](expressions.md#constant-expressions)) with value null, then the the state of *v* after *expr* is the same as the state of *v* after *expr_second*.</span></span>
*  <span data-ttu-id="b3bf2-423">이 고, 그렇지 상태의 *v* 한 후 *expr* 한정 된 할당 상태와 동일 *v* 후 *expr_first*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-423">Otherwise, the state of *v* after *expr* is the same as the definite assignment state of *v* after *expr_first*.</span></span>

#### <a name="-conditional-expressions"></a><span data-ttu-id="b3bf2-424">?: (conditional) 식</span><span class="sxs-lookup"><span data-stu-id="b3bf2-424">?: (conditional) expressions</span></span>

<span data-ttu-id="b3bf2-425">식에 대 한 *expr* 양식의 `expr_cond ? expr_true : expr_false`:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-425">For an expression *expr* of the form `expr_cond ? expr_true : expr_false`:</span></span>

*  <span data-ttu-id="b3bf2-426">한정 된 할당 상태의 *v* 하기 전에 *expr_cond* 의 상태와 동일 *v* 전에 *expr*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-426">The definite assignment state of *v* before *expr_cond* is the same as the state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b3bf2-427">한정 된 할당 상태의 *v* 하기 전에 *expr_true* 다음 중 하나를 보유 하는 경우에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-427">The definite assignment state of *v* before *expr_true* is definitely assigned if and only if one of the following holds:</span></span>
    * <span data-ttu-id="b3bf2-428">*expr_cond* 는 값을 사용 하 여 상수 식 `false`</span><span class="sxs-lookup"><span data-stu-id="b3bf2-428">*expr_cond* is a constant expression with the value `false`</span></span>
    * <span data-ttu-id="b3bf2-429">상태의 *v* 한 후 *expr_cond* 명확 하 게 할당 되었거나 "정적 true 식으로 할당" 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-429">the state of *v* after *expr_cond* is definitely assigned or "definitely assigned after true expression".</span></span>
*  <span data-ttu-id="b3bf2-430">한정 된 할당 상태의 *v* 하기 전에 *expr_false* 다음 중 하나를 보유 하는 경우에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-430">The definite assignment state of *v* before *expr_false* is definitely assigned if and only if one of the following holds:</span></span>
    * <span data-ttu-id="b3bf2-431">*expr_cond* 는 값을 사용 하 여 상수 식 `true`</span><span class="sxs-lookup"><span data-stu-id="b3bf2-431">*expr_cond* is a constant expression with the value `true`</span></span>
*  <span data-ttu-id="b3bf2-432">상태의 *v* 한 후 *expr_cond* 명확 하 게 할당 되었거나 "정적 false 식으로 할당" 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-432">the state of *v* after *expr_cond* is definitely assigned or "definitely assigned after false expression".</span></span>
*  <span data-ttu-id="b3bf2-433">한정 된 할당 상태의 *v* 한 후 *expr* 에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-433">The definite assignment state of *v* after *expr* is determined by:</span></span>
    * <span data-ttu-id="b3bf2-434">하는 경우 *expr_cond* 상수 식입니다 ([상수 식을](expressions.md#constant-expressions)) 값을 사용 하 여 `true` 상태 *v* 후 *expr* 상태와 같습니다 *v* 한 후 *expr_true*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-434">If *expr_cond* is a constant expression ([Constant expressions](expressions.md#constant-expressions)) with value `true` then the state of *v* after *expr* is the same as the state of *v* after *expr_true*.</span></span>
    * <span data-ttu-id="b3bf2-435">그렇지 않고 *expr_cond* 상수 식입니다 ([상수 식을](expressions.md#constant-expressions)) 값을 사용 하 여 `false` 상태 *v* 후 *expr* 상태의 동일 *v* 한 후 *expr_false*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-435">Otherwise, if *expr_cond* is a constant expression ([Constant expressions](expressions.md#constant-expressions)) with value `false` then the state of *v* after *expr* is the same as the state of *v* after *expr_false*.</span></span>
    * <span data-ttu-id="b3bf2-436">그렇지 않은 경우, 상태 *v* 후 *expr_true* 정적으로 할당 및 상태의 *v* 후 *expr_false* 확실히 할당 상태 *v* 한 후 *expr* 정적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-436">Otherwise, if the state of *v* after *expr_true* is definitely assigned and the state of *v* after *expr_false* is definitely assigned, then the state of *v* after *expr* is definitely assigned.</span></span>
    * <span data-ttu-id="b3bf2-437">이 고, 그렇지 상태의 *v* 한 후 *expr* 확실 하 게 할당 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-437">Otherwise, the state of *v* after *expr* is not definitely assigned.</span></span>

#### <a name="anonymous-functions"></a><span data-ttu-id="b3bf2-438">익명 함수</span><span class="sxs-lookup"><span data-stu-id="b3bf2-438">Anonymous functions</span></span>

<span data-ttu-id="b3bf2-439">에 *lambda_expression* 또는 *anonymous_method_expression* *expr* 본문 (중 하나 *블록* 또는 *식* ) *본문*:</span><span class="sxs-lookup"><span data-stu-id="b3bf2-439">For a *lambda_expression* or *anonymous_method_expression* *expr* with a body (either *block* or *expression*) *body*:</span></span>

*  <span data-ttu-id="b3bf2-440">외부 변수의 한정 된 할당 상태 *v* 하기 전에 *본문* 의 상태와 동일 *v* 앞 *expr*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-440">The definite assignment state of an outer variable *v* before *body* is the same as the state of *v* before *expr*.</span></span> <span data-ttu-id="b3bf2-441">즉, 외부 변수의 한정 된 할당 상태는 익명 함수 측면에서 상속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-441">That is, definite assignment state of outer variables is inherited from the context of the anonymous function.</span></span>
*  <span data-ttu-id="b3bf2-442">외부 변수의 한정 된 할당 상태 *v* 한 후 *expr* 의 상태와 동일 *v* 전에 *expr*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-442">The definite assignment state of an outer variable *v* after *expr* is the same as the state of *v* before *expr*.</span></span>

<span data-ttu-id="b3bf2-443">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="b3bf2-443">The example</span></span>
```csharp
delegate bool Filter(int i);

void F() {
    int max;

    // Error, max is not definitely assigned
    Filter f = (int n) => n < max;

    max = 5;
    DoWork(f);
}
```
<span data-ttu-id="b3bf2-444">이후 컴파일 타임 오류가 `max` 익명 함수 선언 된 위치 확실 하 게 할당 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-444">generates a compile-time error since `max` is not definitely assigned where the anonymous function is declared.</span></span> <span data-ttu-id="b3bf2-445">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="b3bf2-445">The example</span></span>
```csharp
delegate void D();

void F() {
    int n;
    D d = () => { n = 1; };

    d();

    // Error, n is not definitely assigned
    Console.WriteLine(n);
}
```
<span data-ttu-id="b3bf2-446">에 대 한 할당 이후 컴파일 타임 오류를 생성 `n` 익명 함수에 영향을 주지 않습니다의 한정 된 할당 상태에 `n` 익명 함수 외부입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-446">also generates a compile-time error since the assignment to `n` in the anonymous function has no affect on the definite assignment state of `n` outside the anonymous function.</span></span>

## <a name="variable-references"></a><span data-ttu-id="b3bf2-447">변수 참조</span><span class="sxs-lookup"><span data-stu-id="b3bf2-447">Variable references</span></span>

<span data-ttu-id="b3bf2-448">A *variable_reference* 되는 *식* 변수로 분류 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-448">A *variable_reference* is an *expression* that is classified as a variable.</span></span> <span data-ttu-id="b3bf2-449">A *variable_reference* 현재 값을 인출 하 고 새 값을 저장할 액세스할 수 있는 저장소 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-449">A *variable_reference* denotes a storage location that can be accessed both to fetch the current value and to store a new value.</span></span>

```antlr
variable_reference
    : expression
    ;
```

<span data-ttu-id="b3bf2-450">C 및 c + +에는 *variable_reference* 이라고는 *lvalue*합니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-450">In C and C++, a *variable_reference* is known as an *lvalue*.</span></span>

## <a name="atomicity-of-variable-references"></a><span data-ttu-id="b3bf2-451">변수 참조의 원자성</span><span class="sxs-lookup"><span data-stu-id="b3bf2-451">Atomicity of variable references</span></span>

<span data-ttu-id="b3bf2-452">데이터 형식은의 읽기 및 쓰기는 원자성: `bool`, `char`, `byte`, `sbyte`, `short`를 `ushort`, `uint`를 `int`, `float`, 참조 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-452">Reads and writes of the following data types are atomic: `bool`, `char`, `byte`, `sbyte`, `short`, `ushort`, `uint`, `int`, `float`, and reference types.</span></span> <span data-ttu-id="b3bf2-453">또한 위 목록에 있는 기본 형식 사용 하 여 열거형의 읽기 및 쓰기도 원자성입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-453">In addition, reads and writes of enum types with an underlying type in the previous list are also atomic.</span></span> <span data-ttu-id="b3bf2-454">포함 한 다른 형식의의 읽기 및 쓰기로 `long`, `ulong`, `double`, 및 `decimal`, 사용자 정의 형식 뿐만 아니라 아닐 원자성입니다.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-454">Reads and writes of other types, including `long`, `ulong`, `double`, and `decimal`, as well as user-defined types, are not guaranteed to be atomic.</span></span> <span data-ttu-id="b3bf2-455">해당 목적에 맞게 설계 하는 라이브러리 함수 외에도 보장은 없습니다 원자성 읽기-수정-쓰기의 같은 증가 또는 감소 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="b3bf2-455">Aside from the library functions designed for that purpose, there is no guarantee of atomic read-modify-write, such as in the case of increment or decrement.</span></span>

