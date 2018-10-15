# <a name="expressions"></a><span data-ttu-id="602c5-101">식</span><span class="sxs-lookup"><span data-stu-id="602c5-101">Expressions</span></span>

<span data-ttu-id="602c5-102">식은 연산자와 피연산자의 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-102">An expression is a sequence of operators and operands.</span></span> <span data-ttu-id="602c5-103">이 장에서 구문, 피연산자 및 연산자를 평가 및 식의 의미는 순서를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-103">This chapter defines the syntax, order of evaluation of operands and operators, and meaning of expressions.</span></span>

## <a name="expression-classifications"></a><span data-ttu-id="602c5-104">식 분류</span><span class="sxs-lookup"><span data-stu-id="602c5-104">Expression classifications</span></span>

<span data-ttu-id="602c5-105">식은 다음 중 하나로 분류됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-105">An expression is classified as one of the following:</span></span>

*  <span data-ttu-id="602c5-106">값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-106">A value.</span></span> <span data-ttu-id="602c5-107">모든 값에는 연결된 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-107">Every value has an associated type.</span></span>
*  <span data-ttu-id="602c5-108">변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-108">A variable.</span></span> <span data-ttu-id="602c5-109">모든 변수에는 연결된 형식, 즉 변수의 선언 된 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-109">Every variable has an associated type, namely the declared type of the variable.</span></span>
*  <span data-ttu-id="602c5-110">네임스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-110">A namespace.</span></span> <span data-ttu-id="602c5-111">이 분류를 사용 하 여 식 왼쪽에만 나타날 수 있습니다는 *member_access* ([멤버 액세스](expressions.md#member-access)).</span><span class="sxs-lookup"><span data-stu-id="602c5-111">An expression with this classification can only appear as the left hand side of a *member_access* ([Member access](expressions.md#member-access)).</span></span> <span data-ttu-id="602c5-112">다른 컨텍스트에서 네임 스페이스로 분류 되는 식 하면 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-112">In any other context, an expression classified as a namespace causes a compile-time error.</span></span>
*  <span data-ttu-id="602c5-113">형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-113">A type.</span></span> <span data-ttu-id="602c5-114">이 분류를 사용 하 여 식 왼쪽에만 나타날 수 있습니다는 *member_access* ([멤버 액세스](expressions.md#member-access)), 또는 대 한 피연산자로 합니다 `as` 연산자 ([As 연산자 ](expressions.md#the-as-operator)), `is` 연산자 ([는 연산자가](expressions.md#the-is-operator)), 또는 `typeof` 연산자 ([typeof 연산자](expressions.md#the-typeof-operator)).</span><span class="sxs-lookup"><span data-stu-id="602c5-114">An expression with this classification can only appear as the left hand side of a *member_access* ([Member access](expressions.md#member-access)), or as an operand for the `as` operator ([The as operator](expressions.md#the-as-operator)), the `is` operator ([The is operator](expressions.md#the-is-operator)), or the `typeof` operator ([The typeof operator](expressions.md#the-typeof-operator)).</span></span> <span data-ttu-id="602c5-115">다른 컨텍스트에서 형식으로 분류 되는 식 하면 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-115">In any other context, an expression classified as a type causes a compile-time error.</span></span>
*  <span data-ttu-id="602c5-116">멤버 조회에서 발생 하는 오버 로드 된 메서드 집합인 메서드 그룹 ([멤버 조회](expressions.md#member-lookup)).</span><span class="sxs-lookup"><span data-stu-id="602c5-116">A method group, which is a set of overloaded methods resulting from a member lookup ([Member lookup](expressions.md#member-lookup)).</span></span> <span data-ttu-id="602c5-117">메서드 그룹을 연결 된 인스턴스 식과 연결 된 형식 인수 목록에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-117">A method group may have an associated instance expression and an associated type argument list.</span></span> <span data-ttu-id="602c5-118">인스턴스 식의 평가 결과에서 표시 되는 인스턴스가 인스턴스 메서드를 호출 하면 `this` ([이 액세스](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="602c5-118">When an instance method is invoked, the result of evaluating the instance expression becomes the instance represented by `this` ([This access](expressions.md#this-access)).</span></span> <span data-ttu-id="602c5-119">메서드 그룹에서 허용 되는 *invocation_expression* ([호출 식](expressions.md#invocation-expressions)), *delegate_creation_expression* ([대리자 생성 식을](expressions.md#delegate-creation-expressions))와 왼쪽에는 연산자 이며 호환 되는 대리자 형식으로 암시적으로 변환할 수 있습니다 ([메서드 그룹 변환](conversions.md#method-group-conversions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-119">A method group is permitted in an *invocation_expression* ([Invocation expressions](expressions.md#invocation-expressions)) , a *delegate_creation_expression* ([Delegate creation expressions](expressions.md#delegate-creation-expressions)) and as the left hand side of an is operator, and can be implicitly converted to a compatible delegate type ([Method group conversions](conversions.md#method-group-conversions)).</span></span> <span data-ttu-id="602c5-120">다른 컨텍스트에서 메서드 그룹으로 분류 되는 식은 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-120">In any other context, an expression classified as a method group causes a compile-time error.</span></span>
*  <span data-ttu-id="602c5-121">Null 리터럴입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-121">A null literal.</span></span> <span data-ttu-id="602c5-122">이 분류를 사용 하 여 식은 참조 형식 또는 nullable 형식에 암시적으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-122">An expression with this classification can be implicitly converted to a reference type or nullable type.</span></span>
*  <span data-ttu-id="602c5-123">익명 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-123">An anonymous function.</span></span> <span data-ttu-id="602c5-124">이 분류를 사용 하 여 식은 호환 되는 대리자 형식 또는 식 트리 형식을 암시적으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-124">An expression with this classification can be implicitly converted to a compatible delegate type or expression tree type.</span></span>
*  <span data-ttu-id="602c5-125">속성 액세스입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-125">A property access.</span></span> <span data-ttu-id="602c5-126">모든 속성 액세스에는 연관 된 형식, 즉 속성의 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-126">Every property access has an associated type, namely the type of the property.</span></span> <span data-ttu-id="602c5-127">또한 속성 액세스는 연결된 된 인스턴스 식이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-127">Furthermore, a property access may have an associated instance expression.</span></span> <span data-ttu-id="602c5-128">접근자 (합니다 `get` 또는 `set` 블록) 인스턴스의 속성 액세스 호출 되 면 인스턴스 식의 평가 결과가 됩니다 하 여 표시 되는 인스턴스 `this` ([이 액세스](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="602c5-128">When an accessor (the `get` or `set` block) of an instance property access is invoked, the result of evaluating the instance expression becomes the instance represented by `this` ([This access](expressions.md#this-access)).</span></span>
*  <span data-ttu-id="602c5-129">이벤트 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-129">An event access.</span></span> <span data-ttu-id="602c5-130">모든 이벤트 액세스에는 연관 된 형식, 즉 이벤트 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-130">Every event access has an associated type, namely the type of the event.</span></span> <span data-ttu-id="602c5-131">또한 이벤트 액세스 연결된 된 인스턴스 식이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-131">Furthermore, an event access may have an associated instance expression.</span></span> <span data-ttu-id="602c5-132">왼쪽 피연산자와 이벤트 액세스 나타날 수 있습니다 합니다 `+=` 하 고 `-=` 연산자 ([이벤트 할당](expressions.md#event-assignment)).</span><span class="sxs-lookup"><span data-stu-id="602c5-132">An event access may appear as the left hand operand of the `+=` and `-=` operators ([Event assignment](expressions.md#event-assignment)).</span></span> <span data-ttu-id="602c5-133">다른 컨텍스트에서 이벤트 액세스로 분류 되는 식 하면 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-133">In any other context, an expression classified as an event access causes a compile-time error.</span></span>
*  <span data-ttu-id="602c5-134">인덱서 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-134">An indexer access.</span></span> <span data-ttu-id="602c5-135">모든 인덱서 액세스에는 연관 된 형식, 즉 인덱서의 요소 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-135">Every indexer access has an associated type, namely the element type of the indexer.</span></span> <span data-ttu-id="602c5-136">또한 인덱서 액세스에 연결 된 인수 목록과 연결된 된 인스턴스 식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-136">Furthermore, an indexer access has an associated instance expression and an associated argument list.</span></span> <span data-ttu-id="602c5-137">접근자 (합니다 `get` 또는 `set` 블록) 인덱서의 액세스 호출 되 면 인스턴스 식의 평가 결과 나타내는 인스턴스 `this` ([이 액세스](expressions.md#this-access)), 및의 결과 인수 목록의 계산 매개 변수 목록이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-137">When an accessor (the `get` or `set` block) of an indexer access is invoked, the result of evaluating the instance expression becomes the instance represented by `this` ([This access](expressions.md#this-access)), and the result of evaluating the argument list becomes the parameter list of the invocation.</span></span>
*  <span data-ttu-id="602c5-138">항목이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-138">Nothing.</span></span> <span data-ttu-id="602c5-139">식의 반환 형식과 메서드를 호출 하는 경우 이런 `void`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-139">This occurs when the expression is an invocation of a method with a return type of `void`.</span></span> <span data-ttu-id="602c5-140">그대로 아무만의 컨텍스트에서 분류 되는 식에 *statement_expression* ([식 문은](statements.md#expression-statements)).</span><span class="sxs-lookup"><span data-stu-id="602c5-140">An expression classified as nothing is only valid in the context of a *statement_expression* ([Expression statements](statements.md#expression-statements)).</span></span>

<span data-ttu-id="602c5-141">식의 최종 결과 네임 스페이스, 유형, 메서드 그룹 또는 이벤트 액세스 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-141">The final result of an expression is never a namespace, type, method group, or event access.</span></span> <span data-ttu-id="602c5-142">대신 위에서 설명한 대로 식의 이러한 범주는 특정 컨텍스트에서 허용 되는 중간 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-142">Rather, as noted above, these categories of expressions are intermediate constructs that are only permitted in certain contexts.</span></span>

<span data-ttu-id="602c5-143">속성 액세스 또는 인덱서 액세스는 항상 다시 분류 값으로 호출을 수행 하 여 합니다 *get 접근자* 또는 *set 접근자*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-143">A property access or indexer access is always reclassified as a value by performing an invocation of the *get accessor* or the *set accessor*.</span></span> <span data-ttu-id="602c5-144">특정 접근자는 속성 또는 인덱서 액세스의 컨텍스트에 의해 결정 됩니다: 액세스는 할당 대상일 경우는 *set 접근자* 새 값을 할당 하기 위해 호출 됩니다 ([단순 할당](expressions.md#simple-assignment)) .</span><span class="sxs-lookup"><span data-stu-id="602c5-144">The particular accessor is determined by the context of the property or indexer access: If the access is the target of an assignment, the *set accessor* is invoked to assign a new value ([Simple assignment](expressions.md#simple-assignment)).</span></span> <span data-ttu-id="602c5-145">그렇지 않은 경우는 *get 접근자* 가 현재 값을 얻기 위해 호출 됩니다 ([식의 값](expressions.md#values-of-expressions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-145">Otherwise, the *get accessor* is invoked to obtain the current value ([Values of expressions](expressions.md#values-of-expressions)).</span></span>

### <a name="values-of-expressions"></a><span data-ttu-id="602c5-146">식의 값</span><span class="sxs-lookup"><span data-stu-id="602c5-146">Values of expressions</span></span>

<span data-ttu-id="602c5-147">대부분의 식을 포함 하는 구문에는 궁극적으로을 나타내는 식이 필요는 ***값***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-147">Most of the constructs that involve an expression ultimately require the expression to denote a ***value***.</span></span> <span data-ttu-id="602c5-148">이러한 경우에는 실제 식 나타냅니다 네임 스페이스, 형식, 메서드 그룹 또는 아무 것도 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-148">In such cases, if the actual expression denotes a namespace, a type, a method group, or nothing, a compile-time error occurs.</span></span> <span data-ttu-id="602c5-149">그러나 식 속성 액세스, 인덱서 액세스, 또는 변수를 표시할 경우 속성, 인덱서 또는 변수 값은 암시적으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-149">However, if the expression denotes a property access, an indexer access, or a variable, the value of the property, indexer, or variable is implicitly substituted:</span></span>

*  <span data-ttu-id="602c5-150">변수 값은 단순히 현재 변수로 식별 된 저장소 위치에 저장 된 값.</span><span class="sxs-lookup"><span data-stu-id="602c5-150">The value of a variable is simply the value currently stored in the storage location identified by the variable.</span></span> <span data-ttu-id="602c5-151">변수는 정적으로 할당 된 간주 해야 합니다 ([한정 된 할당](variables.md#definite-assignment)) 해당 값을 가져올 수 있습니다 하거나 그렇지 않으면 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-151">A variable must be considered definitely assigned ([Definite assignment](variables.md#definite-assignment)) before its value can be obtained, or otherwise a compile-time error occurs.</span></span>
*  <span data-ttu-id="602c5-152">호출 하 여 가져올 속성 액세스 식의 값을 *get 접근자* 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-152">The value of a property access expression is obtained by invoking the *get accessor* of the property.</span></span> <span data-ttu-id="602c5-153">속성에 없는 경우 *get 접근자*, 컴파일 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-153">If the property has no *get accessor*, a compile-time error occurs.</span></span> <span data-ttu-id="602c5-154">이 고, 그렇지 함수 멤버 호출 ([컴파일 타임 동적 오버 로드 확인 검사](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) 수행한 호출의 결과 속성 액세스 식의 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-154">Otherwise, a function member invocation ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) is performed, and the result of the invocation becomes the value of the property access expression.</span></span>
*  <span data-ttu-id="602c5-155">호출 하 여 가져온 인덱서 액세스 식의 값을 *get 접근자* 인덱서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-155">The value of an indexer access expression is obtained by invoking the *get accessor* of the indexer.</span></span> <span data-ttu-id="602c5-156">인덱서가 없으면 *get 접근자*, 컴파일 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-156">If the indexer has no *get accessor*, a compile-time error occurs.</span></span> <span data-ttu-id="602c5-157">이 고, 그렇지 함수 멤버 호출 ([컴파일 타임 동적 오버 로드 확인 검사](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) 인수를 사용 하 여 수행 됩니다 인덱서 액세스 식과 사용 하 여 연결 된 목록 및 호출의 결과 값이 됩니다. 인덱서 액세스 식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-157">Otherwise, a function member invocation ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) is performed with the argument list associated with the indexer access expression, and the result of the invocation becomes the value of the indexer access expression.</span></span>

## <a name="static-and-dynamic-binding"></a><span data-ttu-id="602c5-158">정적 및 동적 바인딩</span><span class="sxs-lookup"><span data-stu-id="602c5-158">Static and Dynamic Binding</span></span>

<span data-ttu-id="602c5-159">형식 또는 구성 식 (인수, 피연산자, 수신자)의 값에 따라 작업의 의미를 확인 하는 과정은 라고도 ***바인딩***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-159">The process of determining the meaning of an operation based on the type or value of constituent expressions (arguments, operands, receivers) is often referred to as ***binding***.</span></span> <span data-ttu-id="602c5-160">예를 들어 메서드 호출의 의미를 사용 하 고 수신자와 인수의 형식에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-160">For instance the meaning of a method call is determined based on the type of the receiver and arguments.</span></span> <span data-ttu-id="602c5-161">연산자의 의미는 해당 피연산자의 형식에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-161">The meaning of an operator is determined based on the type of its operands.</span></span>

<span data-ttu-id="602c5-162">C#의 경우이 작업의 의미는 일반적으로 결정 됩니다 컴파일 타임에 구성 식 중 컴파일 타임 형식을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-162">In C# the meaning of an operation is usually determined at compile-time, based on the compile-time type of its constituent expressions.</span></span> <span data-ttu-id="602c5-163">마찬가지로, 식에 오류가 있으면 오류가 감지 되 고 컴파일러에서 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-163">Likewise, if an expression contains an error, the error is detected and reported by the compiler.</span></span> <span data-ttu-id="602c5-164">이 접근 방식 이라고 ***정적 바인딩***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-164">This approach is known as ***static binding***.</span></span>

<span data-ttu-id="602c5-165">그러나 식이 동적 식을 경우 (즉, 형식이 `dynamic`) 형식에 해당 하는 대신에 참여 하는 모든 바인딩을 기반으로 해당 런타임 형식 (즉, 런타임에 나타냅니다 개체의 실제 형식)를 나타냅니다 컴파일 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-165">However, if an expression is a dynamic expression (i.e. has the type `dynamic`) this indicates that any binding that it participates in should be based on its run-time type (i.e. the actual type of the object it denotes at run-time) rather than the type it has at compile-time.</span></span> <span data-ttu-id="602c5-166">따라서 이러한 작업의 바인딩은 작업이 프로그램을 실행 하는 동안 실행할 수 있는 시간까지 지연 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-166">The binding of such an operation is therefore deferred until the time where the operation is to be executed during the running of the program.</span></span> <span data-ttu-id="602c5-167">이 이라고 ***동적 바인딩***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-167">This is referred to as ***dynamic binding***.</span></span>

<span data-ttu-id="602c5-168">작업을 동적으로 바인딩하면 컴파일러에서 거의 또는 전혀 검사를 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-168">When an operation is dynamically bound, little or no checking is performed by the compiler.</span></span> <span data-ttu-id="602c5-169">대신 런타임에 바인딩이 실패 한 경우 오류는 런타임 시 예외로 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-169">Instead if the run-time binding fails, errors are reported as exceptions at run-time.</span></span>

<span data-ttu-id="602c5-170">C#에서 다음 작업을는 바인딩에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-170">The following operations in C# are subject to binding:</span></span>

*  <span data-ttu-id="602c5-171">멤버 액세스: `e.M`</span><span class="sxs-lookup"><span data-stu-id="602c5-171">Member access: `e.M`</span></span>
*  <span data-ttu-id="602c5-172">메서드 호출: `e.M(e1, ..., eN)`</span><span class="sxs-lookup"><span data-stu-id="602c5-172">Method invocation: `e.M(e1, ..., eN)`</span></span>
*  <span data-ttu-id="602c5-173">대리자 호출:`e(e1, ..., eN)`</span><span class="sxs-lookup"><span data-stu-id="602c5-173">Delegate invocation:`e(e1, ..., eN)`</span></span>
*  <span data-ttu-id="602c5-174">요소 액세스: `e[e1, ..., eN]`</span><span class="sxs-lookup"><span data-stu-id="602c5-174">Element access: `e[e1, ..., eN]`</span></span>
*  <span data-ttu-id="602c5-175">개체 만들기: `new C(e1, ..., eN)`</span><span class="sxs-lookup"><span data-stu-id="602c5-175">Object creation: `new C(e1, ..., eN)`</span></span>
*  <span data-ttu-id="602c5-176">오버 로드 된 단항 연산자: `+`, `-`를 `!`를 `~`를 `++`를 `--`, `true`, `false`</span><span class="sxs-lookup"><span data-stu-id="602c5-176">Overloaded unary operators: `+`, `-`, `!`, `~`, `++`, `--`, `true`, `false`</span></span>
*  <span data-ttu-id="602c5-177">이항 연산자를 오버 로드 된: `+`, `-`, `*`, `/`, `%`를 `&`, `&&`를 `|`, `||`를 `??`, `^`, `<<` , `>>`, `==`,`!=`, `>`, `<`, `>=`, `<=`</span><span class="sxs-lookup"><span data-stu-id="602c5-177">Overloaded binary operators: `+`, `-`, `*`, `/`, `%`, `&`, `&&`, `|`, `||`, `??`, `^`, `<<`, `>>`, `==`,`!=`, `>`, `<`, `>=`, `<=`</span></span>
*  <span data-ttu-id="602c5-178">할당 연산자: `=`, `+=`, `-=`, `*=`, `/=`를 `%=`, `&=`를 `|=`를 `^=`, `<<=`, `>>=`</span><span class="sxs-lookup"><span data-stu-id="602c5-178">Assignment operators: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `|=`, `^=`, `<<=`, `>>=`</span></span>
*  <span data-ttu-id="602c5-179">암시적 변환과 명시적 변환</span><span class="sxs-lookup"><span data-stu-id="602c5-179">Implicit and explicit conversions</span></span>

<span data-ttu-id="602c5-180">동적 식을 없는 관련 된 경우 C# 기본값은 정적 바인딩 구성 식의 컴파일 시간 형식 선택 프로세스에서 사용 되는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-180">When no dynamic expressions are involved, C# defaults to static binding, which means that the compile-time types of constituent expressions are used in the selection process.</span></span> <span data-ttu-id="602c5-181">그러나 위에 나열 된 작업에 구성 식 중 하나는 동적 식인 경우 작업 대신 동적으로 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-181">However, when one of the constituent expressions in the operations listed above is a dynamic expression, the operation is instead dynamically bound.</span></span>

### <a name="binding-time"></a><span data-ttu-id="602c5-182">바인딩 시간</span><span class="sxs-lookup"><span data-stu-id="602c5-182">Binding-time</span></span>

<span data-ttu-id="602c5-183">런타임 시 동적 바인딩을 수행 하는 반면 정적 바인딩 작업 컴파일 타임에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-183">Static binding takes place at compile-time, whereas dynamic binding takes place at run-time.</span></span> <span data-ttu-id="602c5-184">다음 섹션에서는 용어 ***바인딩 시간*** 컴파일 타임 또는 런타임 바인딩 위치를 사용 하는 경우에 따라을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-184">In the following sections, the term ***binding-time*** refers to either compile-time or run-time, depending on when the binding takes place.</span></span>

<span data-ttu-id="602c5-185">다음 예제에서는 정적 및 동적 바인딩 및 바인딩 시간 개념을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-185">The following example illustrates the notions of static and dynamic binding and of binding-time:</span></span>
```csharp
object  o = 5;
dynamic d = 5;

Console.WriteLine(5);  // static  binding to Console.WriteLine(int)
Console.WriteLine(o);  // static  binding to Console.WriteLine(object)
Console.WriteLine(d);  // dynamic binding to Console.WriteLine(int)
```

<span data-ttu-id="602c5-186">처음 두 호출 정적으로 바인딩된: 오버 로드 `Console.WriteLine` 해당 인수의 컴파일 타임 형식에 따라 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-186">The first two calls are statically bound: the overload of `Console.WriteLine` is picked based on the compile-time type of their argument.</span></span> <span data-ttu-id="602c5-187">따라서 바인딩-시간은 컴파일 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-187">Thus, the binding-time is compile-time.</span></span>

<span data-ttu-id="602c5-188">세 번째 호출을 동적으로 바인딩됩니다: 오버 로드 `Console.WriteLine` 인수의 런타임 형식에 따라 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-188">The third call is dynamically bound: the overload of `Console.WriteLine` is picked based on the run-time type of its argument.</span></span> <span data-ttu-id="602c5-189">인수는 동적 식 때문에 이런-컴파일 타임 형식은 해당 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-189">This happens because the argument is a dynamic expression -- its compile-time type is `dynamic`.</span></span> <span data-ttu-id="602c5-190">따라서 세 번째 호출에 대 한 바인딩 시간 런타임 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-190">Thus, the binding-time for the third call is run-time.</span></span>

### <a name="dynamic-binding"></a><span data-ttu-id="602c5-191">동적 바인딩</span><span class="sxs-lookup"><span data-stu-id="602c5-191">Dynamic binding</span></span>

<span data-ttu-id="602c5-192">C# 프로그램이 상호 작용할 수 있도록 동적 바인딩 목적은 ***동적 개체***, 즉, C#의 일반 규칙을 따르지 않는 개체 형식 시스템.</span><span class="sxs-lookup"><span data-stu-id="602c5-192">The purpose of dynamic binding is to allow C# programs to interact with ***dynamic objects***, i.e. objects that do not follow the normal rules of the C# type system.</span></span> <span data-ttu-id="602c5-193">동적 개체를 다른 형식 시스템을 사용 하 여 다른 프로그래밍 언어의 개체 수 또는 프로그래밍 방식으로 다른 작업에 대 한 자신의 바인딩 의미 체계를 구현 하는 설치 된 개체가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-193">Dynamic objects may be objects from other programming languages with different types systems, or they may be objects that are programmatically setup to implement their own binding semantics for different operations.</span></span>

<span data-ttu-id="602c5-194">동적 개체는 해당 의미 체계를 구현 하는 메커니즘은 정의 된 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-194">The mechanism by which a dynamic object implements its own semantics is implementation defined.</span></span> <span data-ttu-id="602c5-195">지정 된 인터페이스-다시 정의 된 구현-신호를 보내는 데 C# 런타임 특별 한 의미를가지고 있다고 동적 개체로 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-195">A given interface -- again implementation defined -- is implemented by dynamic objects to signal to the C# run-time that they have special semantics.</span></span> <span data-ttu-id="602c5-196">따라서 동적 개체에 대 한 작업에 동적으로 바운드 때마다 자신의 바인딩 의미 체계 보다는이 문서에 지정 된 대로 C#의 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-196">Thus, whenever operations on a dynamic object are dynamically bound, their own binding semantics, rather than those of C# as specified in this document, take over.</span></span>

<span data-ttu-id="602c5-197">동적 바인딩의 목적은 동적 개체를 사용 하 여 상호 운용 있도록 이지만, C# 동적 바인딩할 수 모든 개체에 있는지 동적 여부.</span><span class="sxs-lookup"><span data-stu-id="602c5-197">While the purpose of dynamic binding is to allow interoperation with dynamic objects, C# allows dynamic binding on all objects, whether they are dynamic or not.</span></span> <span data-ttu-id="602c5-198">이렇게 하면 동적 개체의 원활 하 게 통합 하는 작업의 결과 하지 자체 동적 개체 일 수 있지만 컴파일 타임에 프로그래머에 게 알 수 없는 형식으로 계속 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-198">This allows for a smoother integration of dynamic objects, as the results of operations on them may not themselves be dynamic objects, but are still of a type unknown to the programmer at compile-time.</span></span> <span data-ttu-id="602c5-199">도 동적 바인딩 관련된 없는 개체에 동적 개체가 있는 경우에 오류가 리플렉션 기반 코드를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-199">Also dynamic binding can help eliminate error-prone reflection-based code even when no objects involved are dynamic objects.</span></span>

<span data-ttu-id="602c5-200">다음 섹션에서는 정확 하 게 동적 바인딩이 적용 될 때, 어떤 컴파일 타임 검사-모든-적용 되는 경우 및 컴파일 시간 식 및 결과 분류 어떤 언어로 각 구문에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-200">The following sections describe for each construct in the language exactly when dynamic binding is applied, what compile time checking -- if any -- is applied, and what the compile-time result and expression classification is.</span></span>

### <a name="types-of-constituent-expressions"></a><span data-ttu-id="602c5-201">구성 요소 식의 형식</span><span class="sxs-lookup"><span data-stu-id="602c5-201">Types of constituent expressions</span></span>

<span data-ttu-id="602c5-202">작업을 정적으로 바인딩하면 (예:: 수신기에 및 인수, 인덱스 또는 피연산자) 구성 요소 식의 형식은 해당 식의 컴파일 시간 형식으로 항상 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-202">When an operation is statically bound, the type of a constituent expression (e.g. a receiver, and argument, an index or an operand) is always considered to be the compile-time type of that expression.</span></span>

<span data-ttu-id="602c5-203">작업을 동적으로 바인딩하면 구성 식의 컴파일 시간 형식에 따라 다양 한 방식에서 구성 식의 형식이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-203">When an operation is dynamically bound, the type of a constituent expression is determined in different ways depending on the compile-time type of the constituent expression:</span></span>

*  <span data-ttu-id="602c5-204">컴파일 타임 형식 구성 식 `dynamic` 런타임에 식이 계산 되는 실제 값의 형식이 것으로 간주 됩니다</span><span class="sxs-lookup"><span data-stu-id="602c5-204">A constituent expression of compile-time type `dynamic` is considered to have the type of the actual value that the expression evaluates to at runtime</span></span>
*  <span data-ttu-id="602c5-205">컴파일 타임 형식은 해당 형식 매개 변수는 구성 요소 식 형식이 런타임 시 형식 매개 변수에 바인딩되는 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-205">A constituent expression whose compile-time type is a type parameter is considered to have the type which the type parameter is bound to at runtime</span></span>
*  <span data-ttu-id="602c5-206">그렇지 않으면 구성 식은 컴파일 시간 형식으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-206">Otherwise the constituent expression is considered to have its compile-time type.</span></span>

## <a name="operators"></a><span data-ttu-id="602c5-207">연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-207">Operators</span></span>

<span data-ttu-id="602c5-208">식에서 생성 됩니다 ***피연산자*** 하 고 ***연산자***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-208">Expressions are constructed from ***operands*** and ***operators***.</span></span> <span data-ttu-id="602c5-209">식의 연산자는 피연산자에 적용할 연산을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-209">The operators of an expression indicate which operations to apply to the operands.</span></span> <span data-ttu-id="602c5-210">연산자의 예로 `+`, `-`, `*`, `/` 및 `new`가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-210">Examples of operators include `+`, `-`, `*`, `/`, and `new`.</span></span> <span data-ttu-id="602c5-211">피연산자의 예로는 리터럴, 필드, 지역 변수 및 식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-211">Examples of operands include literals, fields, local variables, and expressions.</span></span>

<span data-ttu-id="602c5-212">연산자는 다음과 같은 세 가지 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-212">There are three kinds of operators:</span></span>

*  <span data-ttu-id="602c5-213">단항 연산자.</span><span class="sxs-lookup"><span data-stu-id="602c5-213">Unary operators.</span></span> <span data-ttu-id="602c5-214">단항 연산자는 피연산자 하나를 사용 하 고 두 접두사 표기법을 사용 (같은 `--x`) 또는 후 위 표기법 (같은 `x++`).</span><span class="sxs-lookup"><span data-stu-id="602c5-214">The unary operators take one operand and use either prefix notation (such as `--x`) or postfix notation (such as `x++`).</span></span>
*  <span data-ttu-id="602c5-215">이항 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-215">Binary operators.</span></span> <span data-ttu-id="602c5-216">이항 연산자의 피연산자 2 개 및 중 위 표기법을 사용 하 여 모든 (같은 `x + y`).</span><span class="sxs-lookup"><span data-stu-id="602c5-216">The binary operators take two operands and all use infix notation (such as `x + y`).</span></span>
*  <span data-ttu-id="602c5-217">삼진 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-217">Ternary operator.</span></span> <span data-ttu-id="602c5-218">삼항 연산자만 `?:`에 있으면 세 개의 피연산자를 사용 하 고 사용 하 여 위 표기법 (`c ? x : y`).</span><span class="sxs-lookup"><span data-stu-id="602c5-218">Only one ternary operator, `?:`, exists; it takes three operands and uses infix notation (`c ? x : y`).</span></span>

<span data-ttu-id="602c5-219">식에서 연산자의 계산 순서에 의해 결정 됩니다 합니다 ***우선 순위*** 하 고 ***결합성*** 연산자 ([연산자 우선순위 및 결합성](expressions.md#operator-precedence-and-associativity)) .</span><span class="sxs-lookup"><span data-stu-id="602c5-219">The order of evaluation of operators in an expression is determined by the ***precedence*** and ***associativity*** of the operators ([Operator precedence and associativity](expressions.md#operator-precedence-and-associativity)).</span></span>

<span data-ttu-id="602c5-220">식의 피연산자는 왼쪽에서 오른쪽으로 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-220">Operands in an expression are evaluated from left to right.</span></span> <span data-ttu-id="602c5-221">예를 들어 `F(i) + G(i++) * H(i)`, 메서드 `F` 의 이전 값을 사용 하 여 호출 됩니다 `i`, then 메서드 `G` 의 이전 값을 사용 하 여 호출 됩니다 `i`, 및 마지막으로 메서드 `H` 의새값을사용하여라고`i`.</span><span class="sxs-lookup"><span data-stu-id="602c5-221">For example, in `F(i) + G(i++) * H(i)`, method `F` is called using the old value of `i`, then method `G` is called with the old value of `i`, and, finally, method `H` is called with the new value of `i`.</span></span> <span data-ttu-id="602c5-222">연산자 우선 순위를 별도로 관련이 없는입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-222">This is separate from and unrelated to operator precedence.</span></span>

<span data-ttu-id="602c5-223">특정 연산자 수 ***오버 로드 된***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-223">Certain operators can be ***overloaded***.</span></span> <span data-ttu-id="602c5-224">사용자 정의 연산자 구현 하나 있는 작업에 대 한 지정을 허용 하는 연산자 오버 로드 또는 두 피연산자 모두 사용자 정의 클래스 또는 구조체 형식 ([연산자 오버 로드](expressions.md#operator-overloading)).</span><span class="sxs-lookup"><span data-stu-id="602c5-224">Operator overloading permits user-defined operator implementations to be specified for operations where one or both of the operands are of a user-defined class or struct type ([Operator overloading](expressions.md#operator-overloading)).</span></span>

### <a name="operator-precedence-and-associativity"></a><span data-ttu-id="602c5-225">연산자 우선 순위 및 결합성</span><span class="sxs-lookup"><span data-stu-id="602c5-225">Operator precedence and associativity</span></span>

<span data-ttu-id="602c5-226">식에 여러 연산자가 포함되어 있으면 연산자의 ***우선 순위***에 따라 개별 연산자가 계산되는 순서가 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-226">When an expression contains multiple operators, the ***precedence*** of the operators controls the order in which the individual operators are evaluated.</span></span> <span data-ttu-id="602c5-227">예를 들어 식 `x + y * z` 로 평가 됩니다 `x + (y * z)` 때문에 `*` 연산자 보다 우선 순위가 더 높은 이진 `+` 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-227">For example, the expression `x + y * z` is evaluated as `x + (y * z)` because the `*` operator has higher precedence than the binary `+` operator.</span></span> <span data-ttu-id="602c5-228">연산자의 우선 순위는 해당 연결 된 문법 프로덕션의 정의에서 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-228">The precedence of an operator is established by the definition of its associated grammar production.</span></span> <span data-ttu-id="602c5-229">예를 들어를 *additive_expression* 의 시퀀스로 구성 됩니다 *multiplicative_expression*s 구분 `+` 또는 `-` 연산자에 게는 `+` 및 `-` 연산자 보다 우선 순위가 낮은 합니다 `*`를 `/`, 및 `%` 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-229">For example, an *additive_expression* consists of a sequence of *multiplicative_expression*s separated by `+` or `-` operators, thus giving the `+` and `-` operators lower precedence than the `*`, `/`, and `%` operators.</span></span>

<span data-ttu-id="602c5-230">다음 표에서 순위가 가장 높은 우선 순위에 따라에서 모든 연산자를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-230">The following table summarizes all operators in order of precedence from highest to lowest:</span></span>

| <span data-ttu-id="602c5-231">__섹션__</span><span class="sxs-lookup"><span data-stu-id="602c5-231">__Section__</span></span>                                                                                   | <span data-ttu-id="602c5-232">__범주__</span><span class="sxs-lookup"><span data-stu-id="602c5-232">__Category__</span></span>                | <span data-ttu-id="602c5-233">__연산자__</span><span class="sxs-lookup"><span data-stu-id="602c5-233">__Operators__</span></span> | 
|-----------------------------------------------------------------------------------------------|-----------------------------|---------------|
| [<span data-ttu-id="602c5-234">기본 식</span><span class="sxs-lookup"><span data-stu-id="602c5-234">Primary expressions</span></span>](expressions.md#primary-expressions)                                     | <span data-ttu-id="602c5-235">기본 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-235">Primary</span></span>                     | <span data-ttu-id="602c5-236">`x.y`  `f(x)`  `a[x]`  `x++`  `x--`  `new`  `typeof`  `default`  `checked`  `unchecked`  `delegate`</span><span class="sxs-lookup"><span data-stu-id="602c5-236">`x.y`  `f(x)`  `a[x]`  `x++`  `x--`  `new`  `typeof`  `default`  `checked`  `unchecked`  `delegate`</span></span> | 
| [<span data-ttu-id="602c5-237">단항 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-237">Unary operators</span></span>](expressions.md#unary-operators)                                             | <span data-ttu-id="602c5-238">단항</span><span class="sxs-lookup"><span data-stu-id="602c5-238">Unary</span></span>                       | <span data-ttu-id="602c5-239">`+`  `-`  `!`  `~`  `++x`  `--x`  `(T)x`</span><span class="sxs-lookup"><span data-stu-id="602c5-239">`+`  `-`  `!`  `~`  `++x`  `--x`  `(T)x`</span></span> | 
| [<span data-ttu-id="602c5-240">산술 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-240">Arithmetic operators</span></span>](expressions.md#arithmetic-operators)                                   | <span data-ttu-id="602c5-241">곱하기</span><span class="sxs-lookup"><span data-stu-id="602c5-241">Multiplicative</span></span>              | <span data-ttu-id="602c5-242">`*`  `/`  `%`</span><span class="sxs-lookup"><span data-stu-id="602c5-242">`*`  `/`  `%`</span></span> | 
| [<span data-ttu-id="602c5-243">산술 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-243">Arithmetic operators</span></span>](expressions.md#arithmetic-operators)                                   | <span data-ttu-id="602c5-244">더하기</span><span class="sxs-lookup"><span data-stu-id="602c5-244">Additive</span></span>                    | <span data-ttu-id="602c5-245">`+`  `-`</span><span class="sxs-lookup"><span data-stu-id="602c5-245">`+`  `-`</span></span>      | 
| [<span data-ttu-id="602c5-246">시프트 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-246">Shift operators</span></span>](expressions.md#shift-operators)                                             | <span data-ttu-id="602c5-247">시프트</span><span class="sxs-lookup"><span data-stu-id="602c5-247">Shift</span></span>                       | <span data-ttu-id="602c5-248">`<<`  `>>`</span><span class="sxs-lookup"><span data-stu-id="602c5-248">`<<`  `>>`</span></span>    | 
| [<span data-ttu-id="602c5-249">관계형 및 형식 테스트 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-249">Relational and type-testing operators</span></span>](expressions.md#relational-and-type-testing-operators) | <span data-ttu-id="602c5-250">관계형 및 형식 테스트</span><span class="sxs-lookup"><span data-stu-id="602c5-250">Relational and type testing</span></span> | <span data-ttu-id="602c5-251">`<`  `>`  `<=`  `>=`  `is`  `as`</span><span class="sxs-lookup"><span data-stu-id="602c5-251">`<`  `>`  `<=`  `>=`  `is`  `as`</span></span> | 
| [<span data-ttu-id="602c5-252">관계형 및 형식 테스트 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-252">Relational and type-testing operators</span></span>](expressions.md#relational-and-type-testing-operators) | <span data-ttu-id="602c5-253">같음</span><span class="sxs-lookup"><span data-stu-id="602c5-253">Equality</span></span>                    | <span data-ttu-id="602c5-254">`==`  `!=`</span><span class="sxs-lookup"><span data-stu-id="602c5-254">`==`  `!=`</span></span>    | 
| [<span data-ttu-id="602c5-255">논리 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-255">Logical operators</span></span>](expressions.md#logical-operators)                                         | <span data-ttu-id="602c5-256">논리적 AND</span><span class="sxs-lookup"><span data-stu-id="602c5-256">Logical AND</span></span>                 | `&`           | 
| [<span data-ttu-id="602c5-257">논리 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-257">Logical operators</span></span>](expressions.md#logical-operators)                                         | <span data-ttu-id="602c5-258">논리 XOR</span><span class="sxs-lookup"><span data-stu-id="602c5-258">Logical XOR</span></span>                 | `^`           | 
| [<span data-ttu-id="602c5-259">논리 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-259">Logical operators</span></span>](expressions.md#logical-operators)                                         | <span data-ttu-id="602c5-260">논리적 OR</span><span class="sxs-lookup"><span data-stu-id="602c5-260">Logical OR</span></span>                  | `|`           |
| [<span data-ttu-id="602c5-261">조건부 논리 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-261">Conditional logical operators</span></span>](expressions.md#conditional-logical-operators)                 | <span data-ttu-id="602c5-262">조건부 AND</span><span class="sxs-lookup"><span data-stu-id="602c5-262">Conditional AND</span></span>             | `&&`          | 
| [<span data-ttu-id="602c5-263">조건부 논리 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-263">Conditional logical operators</span></span>](expressions.md#conditional-logical-operators)                 | <span data-ttu-id="602c5-264">조건부 OR</span><span class="sxs-lookup"><span data-stu-id="602c5-264">Conditional OR</span></span>              | `||`          | 
| [<span data-ttu-id="602c5-265">Null 결합 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-265">The null coalescing operator</span></span>](expressions.md#the-null-coalescing-operator)                   | <span data-ttu-id="602c5-266">Null 결합</span><span class="sxs-lookup"><span data-stu-id="602c5-266">Null coalescing</span></span>             | `??`          | 
| [<span data-ttu-id="602c5-267">조건 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-267">Conditional operator</span></span>](expressions.md#conditional-operator)                                   | <span data-ttu-id="602c5-268">조건</span><span class="sxs-lookup"><span data-stu-id="602c5-268">Conditional</span></span>                 | `?:`          | 
| <span data-ttu-id="602c5-269">[대입 연산자](expressions.md#assignment-operators), [익명 함수 식](expressions.md#anonymous-function-expressions)</span><span class="sxs-lookup"><span data-stu-id="602c5-269">[Assignment operators](expressions.md#assignment-operators), [Anonymous function expressions](expressions.md#anonymous-function-expressions)</span></span>  | <span data-ttu-id="602c5-270">할당 및 람다 식</span><span class="sxs-lookup"><span data-stu-id="602c5-270">Assignment and lambda expression</span></span> | <span data-ttu-id="602c5-271">`=`  `*=`  `/=`  `%=`  `+=`  `-=`  `<<=`  `>>=`  `&=`  `^=`  \`</span><span class="sxs-lookup"><span data-stu-id="602c5-271">`=`  `*=`  `/=`  `%=`  `+=`  `-=`  `<<=`  `>>=`  `&=`  `^=`  \`</span></span>|=`  `=>` | 

<span data-ttu-id="602c5-272">피연산자 간에 두 연산자의 우선 순위가 같은 경우 연산자의 결합성 순서를 제어 합니다 작업이 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-272">When an operand occurs between two operators with the same precedence, the associativity of the operators controls the order in which the operations are performed:</span></span>

*  <span data-ttu-id="602c5-273">모든 이항 연산자는 대입 연산자 및 null 병합 연산자를 제외 하 고 ***왼쪽 결합성***에 작업을 수행 왼쪽에서 오른쪽으로 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-273">Except for the assignment operators and the null coalescing operator, all binary operators are ***left-associative***, meaning that operations are performed from left to right.</span></span> <span data-ttu-id="602c5-274">예를 들어, `x + y + z`는 `(x + y) + z`로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-274">For example, `x + y + z` is evaluated as `(x + y) + z`.</span></span>
*  <span data-ttu-id="602c5-275">대입 연산자, null 병합 연산자 및 조건부 연산자 (`?:`)은 ***오른쪽 결합성***, 즉 연산이 오른쪽에서 왼쪽으로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-275">The assignment operators, the null coalescing operator and the conditional operator (`?:`) are ***right-associative***, meaning that operations are performed from right to left.</span></span> <span data-ttu-id="602c5-276">예를 들어, `x = y = z`는 `x = (y = z)`로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-276">For example, `x = y = z` is evaluated as `x = (y = z)`.</span></span>

<span data-ttu-id="602c5-277">우선 순위 및 결합성은 괄호를 사용하여 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-277">Precedence and associativity can be controlled using parentheses.</span></span> <span data-ttu-id="602c5-278">예를 들어 `x + y * z`는 먼저 `y`와 `z`를 곱한 다음 그 결과를 `x`와 더하지만 `(x + y) * z`는 먼저 `x`와 `y`를 더한 다음 그 결과에 `z`를 곱합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-278">For example, `x + y * z` first multiplies `y` by `z` and then adds the result to `x`, but `(x + y) * z` first adds `x` and `y` and then multiplies the result by `z`.</span></span>

### <a name="operator-overloading"></a><span data-ttu-id="602c5-279">연산자 오버 로드</span><span class="sxs-lookup"><span data-stu-id="602c5-279">Operator overloading</span></span>

<span data-ttu-id="602c5-280">모든 단항 및 이항 연산자 구현을 자동으로 모든 식에서 사용할 수 있는 미리 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-280">All unary and binary operators have predefined implementations that are automatically available in any expression.</span></span> <span data-ttu-id="602c5-281">미리 정의 된 구현 하는 것 외에도 구현을 사용자 정의 포함 하 여 도입 수 `operator` 클래스 및 구조체에서 선언 ([연산자](classes.md#operators)).</span><span class="sxs-lookup"><span data-stu-id="602c5-281">In addition to the predefined implementations, user-defined implementations can be introduced by including `operator` declarations in classes and structs ([Operators](classes.md#operators)).</span></span> <span data-ttu-id="602c5-282">사용자 정의 연산자 구현 보다 항상 우선 미리 정의 된 연산자 구현: 구현할 필요 없이 해당 사용자 정의 연산자가 있는 경우 미리 정의 된 연산자 구현을 고려해 야 에설명된대로[ 단항 연산자 오버 로드 확인](expressions.md#unary-operator-overload-resolution) 하 고 [이항 연산자 오버 로드 확인](expressions.md#binary-operator-overload-resolution)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-282">User-defined operator implementations always take precedence over predefined operator implementations: Only when no applicable user-defined operator implementations exist will the predefined operator implementations be considered, as described in [Unary operator overload resolution](expressions.md#unary-operator-overload-resolution) and [Binary operator overload resolution](expressions.md#binary-operator-overload-resolution).</span></span>

<span data-ttu-id="602c5-283">합니다 ***오버 로드할 수 있는 단항 연산자*** 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-283">The ***overloadable unary operators*** are:</span></span>
```csharp
+   -   !   ~   ++   --   true   false
```

<span data-ttu-id="602c5-284">하지만 `true` 하 고 `false` 식에 명시적으로 사용 되지 않습니다 (않으며의 우선 순위 표에 포함 되지 않습니다 [연산자 우선순위 및 결합성](expressions.md#operator-precedence-and-associativity)), 이기 때문에 연산자 간주 되므로 여러 식 컨텍스트에서 호출: 부울 식 ([부울 식](expressions.md#boolean-expressions)) 및 조건부 포함 하는 식 ([조건부 연산자](expressions.md#conditional-operator)), 및 조건부 논리 연산자 ([조건부 논리 연산자](expressions.md#conditional-logical-operators)).</span><span class="sxs-lookup"><span data-stu-id="602c5-284">Although `true` and `false` are not used explicitly in expressions (and therefore are not included in the precedence table in [Operator precedence and associativity](expressions.md#operator-precedence-and-associativity)), they are considered operators because they are invoked in several expression contexts: boolean expressions ([Boolean expressions](expressions.md#boolean-expressions)) and expressions involving the conditional ([Conditional operator](expressions.md#conditional-operator)), and conditional logical operators ([Conditional logical operators](expressions.md#conditional-logical-operators)).</span></span>

<span data-ttu-id="602c5-285">합니다 ***이항 연산자를 오버 로드할 수 있는*** 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-285">The ***overloadable binary operators*** are:</span></span>
```csharp
+   -   *   /   %   &   |   ^   <<   >>   ==   !=   >   <   >=   <=
```

<span data-ttu-id="602c5-286">위에 나열 된 연산자만 오버 로드 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-286">Only the operators listed above can be overloaded.</span></span> <span data-ttu-id="602c5-287">멤버 액세스, 메서드 호출 오버 로드할 수는 특히 또는 `=`, `&&`, `||`, `??`를 `?:`를 `=>`, `checked`를 `unchecked`, `new`, `typeof`, `default`하십시오 `as`, 및 `is` 연산자.</span><span class="sxs-lookup"><span data-stu-id="602c5-287">In particular, it is not possible to overload member access, method invocation, or the `=`, `&&`, `||`, `??`, `?:`, `=>`, `checked`, `unchecked`, `new`, `typeof`, `default`, `as`, and `is` operators.</span></span>

<span data-ttu-id="602c5-288">이항 연산자가 오버로드되면 해당 대입 연산자도 암시적으로 오버로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-288">When a binary operator is overloaded, the corresponding assignment operator, if any, is also implicitly overloaded.</span></span> <span data-ttu-id="602c5-289">예를 들어, 연산자 오버 로드 `*` 연산자를 오버 이기도 `*=`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-289">For example, an overload of operator `*` is also an overload of operator `*=`.</span></span> <span data-ttu-id="602c5-290">이에서 더 자세히 설명 [복합 할당](expressions.md#compound-assignment)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-290">This is described further in [Compound assignment](expressions.md#compound-assignment).</span></span> <span data-ttu-id="602c5-291">대입 연산자 (`=`) 오버 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-291">Note that the assignment operator itself (`=`) cannot be overloaded.</span></span> <span data-ttu-id="602c5-292">변수에 값 단순한 비트 복사를 수행 하는 항상 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-292">An assignment always performs a simple bit-wise copy of a value into a variable.</span></span>

<span data-ttu-id="602c5-293">와 같은 작업을 캐스팅할 `(T)x`, 사용자 정의 변환 함으로써 오버 로드 됩니다 ([사용자 정의 변환은](conversions.md#user-defined-conversions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-293">Cast operations, such as `(T)x`, are overloaded by providing user-defined conversions ([User-defined conversions](conversions.md#user-defined-conversions)).</span></span>

<span data-ttu-id="602c5-294">요소와 같은 액세스 `a[x]`를 오버 로드할 수 있는 운영자 간주 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-294">Element access, such as `a[x]`, is not considered an overloadable operator.</span></span> <span data-ttu-id="602c5-295">인덱서를 통해 사용자 정의 인덱싱이 지원 되는 대신 ([인덱서](classes.md#indexers)).</span><span class="sxs-lookup"><span data-stu-id="602c5-295">Instead, user-defined indexing is supported through indexers ([Indexers](classes.md#indexers)).</span></span>

<span data-ttu-id="602c5-296">식에서 연산자 연산자 표기법을 사용 하 여 참조 하는 및 선언에서 연산자 기능적 표기법을 사용 하 여 참조 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-296">In expressions, operators are referenced using operator notation, and in declarations, operators are referenced using functional notation.</span></span> <span data-ttu-id="602c5-297">다음 표에서 연산자와 단항 및 이항 연산자에 대 한 기능적 표기법의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-297">The following table shows the relationship between operator and functional notations for unary and binary operators.</span></span> <span data-ttu-id="602c5-298">첫 번째 항목에서 *op* 모든 오버 로드할 수 있는 단항 전위 연산자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-298">In the first entry, *op* denotes any overloadable unary prefix operator.</span></span> <span data-ttu-id="602c5-299">두 번째 항목에서 *op* 단항 후 위 나타냅니다 `++` 고 `--` 연산자.</span><span class="sxs-lookup"><span data-stu-id="602c5-299">In the second entry, *op* denotes the unary postfix `++` and `--` operators.</span></span> <span data-ttu-id="602c5-300">세 번째 항목에서 *op* 오버 로드할 수 있는 모든 이항 연산자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-300">In the third entry, *op* denotes any overloadable binary operator.</span></span>


| <span data-ttu-id="602c5-301">__연산자 표기법__</span><span class="sxs-lookup"><span data-stu-id="602c5-301">__Operator notation__</span></span> | <span data-ttu-id="602c5-302">__기능적 표기법__</span><span class="sxs-lookup"><span data-stu-id="602c5-302">__Functional notation__</span></span> |
|-----------------------|-------------------------|
| `op x`                | `operator op(x)`        | 
| `x op`                | `operator op(x)`        | 
| `x op y`              | `operator op(x,y)`      | 

<span data-ttu-id="602c5-303">항상 사용자 정의 연산자 선언에 연산자 선언을 포함 하는 클래스 또는 구조체 형식의 매개 변수 중 하나 이상이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-303">User-defined operator declarations always require at least one of the parameters to be of the class or struct type that contains the operator declaration.</span></span> <span data-ttu-id="602c5-304">따라서 수 없으면 사용자 정의 연산자는 미리 정의 된 연산자와 동일한 시그니처가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-304">Thus, it is not possible for a user-defined operator to have the same signature as a predefined operator.</span></span>

<span data-ttu-id="602c5-305">사용자 정의 연산자 선언에는 구문, 우선 순위 또는 연산자의 결합성 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-305">User-defined operator declarations cannot modify the syntax, precedence, or associativity of an operator.</span></span> <span data-ttu-id="602c5-306">예를 들어 합니다 `/` 연산자는 이항 연산자가 항상이 수준의 우선 순위에 지정 된 항상 [연산자 우선순위 및 결합성](expressions.md#operator-precedence-and-associativity), 이며 항상 왼쪽 결합성 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-306">For example, the `/` operator is always a binary operator, always has the precedence level specified in [Operator precedence and associativity](expressions.md#operator-precedence-and-associativity), and is always left-associative.</span></span>

<span data-ttu-id="602c5-307">계산이 든 수행 하는 사용자 정의 연산자에 대 한 가능한 상태인 직관적으로 예상 되는 것과 다른 결과 생성 하는 구현 해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-307">While it is possible for a user-defined operator to perform any computation it pleases, implementations that produce results other than those that are intuitively expected are strongly discouraged.</span></span> <span data-ttu-id="602c5-308">예를 들어 구현을 `operator ==` 같음에 대 한 두 피연산자를 비교 하 고 적절 한 반환 해야 `bool` 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-308">For example, an implementation of `operator ==` should compare the two operands for equality and return an appropriate `bool` result.</span></span>

<span data-ttu-id="602c5-309">개별 연산자에 대 한 설명은 [기본 식](expressions.md#primary-expressions) 를 통해 [조건부 논리 연산자](expressions.md#conditional-logical-operators) 미리 정의 된 연산자 및 적용 되는 추가 규칙의 구현을 지정 합니다. 각 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-309">The descriptions of individual operators in [Primary expressions](expressions.md#primary-expressions) through [Conditional logical operators](expressions.md#conditional-logical-operators) specify the predefined implementations of the operators and any additional rules that apply to each operator.</span></span> <span data-ttu-id="602c5-310">설명을 확인 사용 조건의 ***단항 연산자 오버 로드 확인***, ***이항 연산자 오버 로드 확인에***, 및 ***숫자 승격이***정의 다음 섹션에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-310">The descriptions make use of the terms ***unary operator overload resolution***, ***binary operator overload resolution***, and ***numeric promotion***, definitions of which are found in the following sections.</span></span>

### <a name="unary-operator-overload-resolution"></a><span data-ttu-id="602c5-311">단항 연산자 오버 로드 확인</span><span class="sxs-lookup"><span data-stu-id="602c5-311">Unary operator overload resolution</span></span>

<span data-ttu-id="602c5-312">폼의 작업 `op x` 또는 `x op`여기서 `op` 오버 로드할 수 있는 단항 연산자는 및 `x` 식 형식입니다 `X`, 다음과 같이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-312">An operation of the form `op x` or `x op`, where `op` is an overloadable unary operator, and `x` is an expression of type `X`, is processed as follows:</span></span>

*  <span data-ttu-id="602c5-313">제공한 후보 사용자 정의 연산자 집합 `X` 작업용 `operator op(x)` 규칙을 사용 하 여 결정 됩니다 [후보 사용자 정의 연산자](expressions.md#candidate-user-defined-operators)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-313">The set of candidate user-defined operators provided by `X` for the operation `operator op(x)` is determined using the rules of [Candidate user-defined operators](expressions.md#candidate-user-defined-operators).</span></span>
*  <span data-ttu-id="602c5-314">사용자 정의 연산자 후보 집합이 비어 있지 않은 경우 작업에 대 한 후보 연산자 집합이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-314">If the set of candidate user-defined operators is not empty, then this becomes the set of candidate operators for the operation.</span></span> <span data-ttu-id="602c5-315">그렇지 않으면 미리 정의 된 단항 `operator op` 구현에서는 해당 리프트 된 폼을 포함 하 여 작업에 대 한 후보 연산자의 집합이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-315">Otherwise, the predefined unary `operator op` implementations, including their lifted forms, become the set of candidate operators for the operation.</span></span> <span data-ttu-id="602c5-316">연산자의 설명에 지정된 된 운영자의 미리 정의 된 구현 된 ([기본 식](expressions.md#primary-expressions) 하 고 [단항 연산자](expressions.md#unary-operators)).</span><span class="sxs-lookup"><span data-stu-id="602c5-316">The predefined implementations of a given operator are specified in the description of the operator ([Primary expressions](expressions.md#primary-expressions) and [Unary operators](expressions.md#unary-operators)).</span></span>
*  <span data-ttu-id="602c5-317">오버 로드 확인 규칙 [오버 로드 확인](expressions.md#overload-resolution) 인수 목록에 대해 최상의 연산자를 선택 후보 연산자 집합에 적용 됩니다 `(x)`, 하며이 연산자가 오버 로드 하면 됩니다. 확인 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-317">The overload resolution rules of [Overload resolution](expressions.md#overload-resolution) are applied to the set of candidate operators to select the best operator with respect to the argument list `(x)`, and this operator becomes the result of the overload resolution process.</span></span> <span data-ttu-id="602c5-318">오버 로드 확인을 최상의 single 연산자를 선택 하지 못하면 바인딩 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-318">If overload resolution fails to select a single best operator, a binding-time error occurs.</span></span>

### <a name="binary-operator-overload-resolution"></a><span data-ttu-id="602c5-319">이항 연산자 오버 로드 확인</span><span class="sxs-lookup"><span data-stu-id="602c5-319">Binary operator overload resolution</span></span>

<span data-ttu-id="602c5-320">폼의 작업 `x op y`, 여기서 `op` 를 오버 로드할 수 있는 이항 연산자는 `x` 형식의 식 `X`, 및 `y` 형식의 식 `Y`, 다음과 같이 처리 됩니다:</span><span class="sxs-lookup"><span data-stu-id="602c5-320">An operation of the form `x op y`, where `op` is an overloadable binary operator, `x` is an expression of type `X`, and `y` is an expression of type `Y`, is processed as follows:</span></span>

*  <span data-ttu-id="602c5-321">제공한 후보 사용자 정의 연산자 집합 `X` 하 고 `Y` 작업용 `operator op(x,y)` 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-321">The set of candidate user-defined operators provided by `X` and `Y` for the operation `operator op(x,y)` is determined.</span></span> <span data-ttu-id="602c5-322">집합은 구성에서 제공 하는 후보 연산자의 합집합 `X` 및에서 제공 하는 후보 연산자 `Y`, 각각의 규칙을 사용 하 여 결정 [후보 사용자 정의 연산자](expressions.md#candidate-user-defined-operators)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-322">The set consists of the union of the candidate operators provided by `X` and the candidate operators provided by `Y`, each determined using the rules of [Candidate user-defined operators](expressions.md#candidate-user-defined-operators).</span></span> <span data-ttu-id="602c5-323">하는 경우 `X` 및 `Y` 동일한 형식 이거나 `X` 및 `Y` 공유 후보 연산자 결합된 된 집합에서 한 번만 발생한 다음 일반적인 기본 형식에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-323">If `X` and `Y` are the same type, or if `X` and `Y` are derived from a common base type, then shared candidate operators only occur in the combined set once.</span></span>
*  <span data-ttu-id="602c5-324">사용자 정의 연산자 후보 집합이 비어 있지 않은 경우 작업에 대 한 후보 연산자 집합이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-324">If the set of candidate user-defined operators is not empty, then this becomes the set of candidate operators for the operation.</span></span> <span data-ttu-id="602c5-325">그렇지 않으면 미리 정의 된 이진 `operator op` 구현에서는 해당 리프트 된 폼을 포함 하 여 작업에 대 한 후보 연산자의 집합이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-325">Otherwise, the predefined binary `operator op` implementations, including their lifted forms,  become the set of candidate operators for the operation.</span></span> <span data-ttu-id="602c5-326">연산자의 설명에 지정된 된 운영자의 미리 정의 된 구현 된 ([산술 연산자](expressions.md#arithmetic-operators) 를 통해 [조건부 논리 연산자](expressions.md#conditional-logical-operators)).</span><span class="sxs-lookup"><span data-stu-id="602c5-326">The predefined implementations of a given operator are specified in the description of the operator ([Arithmetic operators](expressions.md#arithmetic-operators) through [Conditional logical operators](expressions.md#conditional-logical-operators)).</span></span> <span data-ttu-id="602c5-327">미리 정의 된 열거형 및 대리자 연산자에 대 한 것으로 간주 하는 유일한 연산자는 피연산자 중 하나의 바인딩 시간 형식인 열거형 또는 대리자 형식에 의해 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-327">For predefined enum and delegate operators, the only operators considered are those defined by an enum or delegate type that is the binding-time type of one of the operands.</span></span>
*  <span data-ttu-id="602c5-328">오버 로드 확인 규칙 [오버 로드 확인](expressions.md#overload-resolution) 인수 목록에 대해 최상의 연산자를 선택 후보 연산자 집합에 적용 됩니다 `(x,y)`, 하며이 연산자가 오버 로드 하면 됩니다. 확인 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-328">The overload resolution rules of [Overload resolution](expressions.md#overload-resolution) are applied to the set of candidate operators to select the best operator with respect to the argument list `(x,y)`, and this operator becomes the result of the overload resolution process.</span></span> <span data-ttu-id="602c5-329">오버 로드 확인을 최상의 single 연산자를 선택 하지 못하면 바인딩 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-329">If overload resolution fails to select a single best operator, a binding-time error occurs.</span></span>

### <a name="candidate-user-defined-operators"></a><span data-ttu-id="602c5-330">후보 사용자 정의 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-330">Candidate user-defined operators</span></span>

<span data-ttu-id="602c5-331">지정 된 형식 `T` 및 작업 `operator op(A)`, 여기서 `op` 는 오버 로드할 수 있는 연산자 및 `A` 후보 집합이 인수 목록에서 제공 하는 사용자 정의 연산자는 `T` 에 대 한 `operator op(A)` 결정 됩니다 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-331">Given a type `T` and an operation `operator op(A)`, where `op` is an overloadable operator and `A` is an argument list, the set of candidate user-defined operators provided by `T` for `operator op(A)` is determined as follows:</span></span>

*  <span data-ttu-id="602c5-332">형식을 확인할 `T0`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-332">Determine the type `T0`.</span></span> <span data-ttu-id="602c5-333">하는 경우 `T` nullable 형식인 `T0` 해당 내부 형식이, 그렇지 않으면 `T0` 값과 같음 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-333">If `T` is a nullable type, `T0` is its underlying type, otherwise `T0` is equal to `T`.</span></span>
*  <span data-ttu-id="602c5-334">모든 `operator op` 의 선언 `T0` 및 하나 이상의 연산자를 적용할 수 있는 경우 이러한 연산자의 형태를 리프트 모든 ([적용 가능한 함수 멤버](expressions.md#applicable-function-member)) 인수 목록 `A`, 다음 집합 후보 연산자에서 이러한 모든 적용 가능한 연산자 이루어져 `T0`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-334">For all `operator op` declarations in `T0` and all lifted forms of such operators, if at least one operator is applicable ([Applicable function member](expressions.md#applicable-function-member)) with respect to the argument list `A`, then the set of candidate operators consists of all such applicable operators in `T0`.</span></span>
*  <span data-ttu-id="602c5-335">그렇지 않은 경우, `T0` 는 `object`, 후보 연산자 집합이 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-335">Otherwise, if `T0` is `object`, the set of candidate operators is empty.</span></span>
*  <span data-ttu-id="602c5-336">후보 연산자 집합에서 제공 하는 고, 그렇지 `T0` 직접 기본 클래스에서 제공 하는 후보 연산자 집합이 `T0`, 또는의 유효 기본 클래스 `T0` 경우 `T0` 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-336">Otherwise, the set of candidate operators provided by `T0` is the set of candidate operators provided by the direct base class of `T0`, or the effective base class of `T0` if `T0` is a type parameter.</span></span>

### <a name="numeric-promotions"></a><span data-ttu-id="602c5-337">숫자 프로 모션</span><span class="sxs-lookup"><span data-stu-id="602c5-337">Numeric promotions</span></span>

<span data-ttu-id="602c5-338">숫자 승격이 자동으로 미리 정의 된 단항 및 이항 숫자 연산자의 피연산자는 특정 암시적 변환을 수행 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-338">Numeric promotion consists of automatically performing certain implicit conversions of the operands of the predefined unary and binary numeric operators.</span></span> <span data-ttu-id="602c5-339">숫자 승격이 고유 메커니즘을 아니라 대신 미리 정의 된 연산자를 오버 로드 확인을 적용 하는 효과입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-339">Numeric promotion is not a distinct mechanism, but rather an effect of applying overload resolution to the predefined operators.</span></span> <span data-ttu-id="602c5-340">숫자 승격이 특히 영향을 주지 않습니다 사용자 정의 연산자의 계산 되지만 비슷한 효과 나타낼 하도록 사용자 정의 연산자를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-340">Numeric promotion specifically does not affect evaluation of user-defined operators, although user-defined operators can be implemented to exhibit similar effects.</span></span>

<span data-ttu-id="602c5-341">숫자 승격이의 예를 들어, 이진 파일의 미리 정의 된 구현 고려 `*` 연산자:</span><span class="sxs-lookup"><span data-stu-id="602c5-341">As an example of numeric promotion, consider the predefined implementations of the binary `*` operator:</span></span>

```csharp
int operator *(int x, int y);
uint operator *(uint x, uint y);
long operator *(long x, long y);
ulong operator *(ulong x, ulong y);
float operator *(float x, float y);
double operator *(double x, double y);
decimal operator *(decimal x, decimal y);
```

<span data-ttu-id="602c5-342">때 오버 로드 해결 규칙 ([오버 로드 확인](expressions.md#overload-resolution))이이 집합에 적용 됩니다 효과 연산자의 피연산자 형식에서 암시적 변환이 있는 연산자의 첫 번째 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-342">When overload resolution rules ([Overload resolution](expressions.md#overload-resolution)) are applied to this set of operators, the effect is to select the first of the operators for which implicit conversions exist from the operand types.</span></span> <span data-ttu-id="602c5-343">작업에 대 한 예를 들어 `b * s`, 여기서 `b` 는 `byte` 및 `s` 는 `short`, 해상도 오버 로드 `operator *(int,int)` 최상의 연산자로.</span><span class="sxs-lookup"><span data-stu-id="602c5-343">For example, for the operation `b * s`, where `b` is a `byte` and `s` is a `short`, overload resolution selects `operator *(int,int)` as the best operator.</span></span> <span data-ttu-id="602c5-344">따라서 결과 `b` 및 `s` 변환할 `int`, 및 결과의 형식은 `int`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-344">Thus, the effect is that `b` and `s` are converted to `int`, and the type of the result is `int`.</span></span> <span data-ttu-id="602c5-345">마찬가지로, 작업에 대 한 `i * d`, 여기서 `i` 는 `int` 및 `d` 는 `double`, 해상도 오버 로드 `operator *(double,double)` 최상의 연산자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-345">Likewise, for the operation `i * d`, where `i` is an `int` and `d` is a `double`, overload resolution selects `operator *(double,double)` as the best operator.</span></span>

#### <a name="unary-numeric-promotions"></a><span data-ttu-id="602c5-346">단항 숫자 프로 모션</span><span class="sxs-lookup"><span data-stu-id="602c5-346">Unary numeric promotions</span></span>

<span data-ttu-id="602c5-347">미리 정의 된 피연산자에 대 한 단항 숫자 승격이 발생 `+`, `-`, 및 `~` 단항 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-347">Unary numeric promotion occurs for the operands of the predefined `+`, `-`, and `~` unary operators.</span></span> <span data-ttu-id="602c5-348">단항 숫자 승격이 형식의 피연산자를 변환 만으로 구성 됩니다 `sbyte`, `byte`를 `short`를 `ushort`, 또는 `char` 형식으로 `int`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-348">Unary numeric promotion simply consists of converting operands of type `sbyte`, `byte`, `short`, `ushort`, or `char` to type `int`.</span></span> <span data-ttu-id="602c5-349">단항에 대 한 뿐만 `-` 연산자를 단항 숫자 승격이 형식의 피연산자를 변환 `uint` 형식으로 `long`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-349">Additionally, for the unary `-` operator, unary numeric promotion converts operands of type `uint` to type `long`.</span></span>

#### <a name="binary-numeric-promotions"></a><span data-ttu-id="602c5-350">이진 숫자 프로 모션</span><span class="sxs-lookup"><span data-stu-id="602c5-350">Binary numeric promotions</span></span>

<span data-ttu-id="602c5-351">미리 정의 된 피연산자에 대 한 이진 숫자 승격이 발생 `+`, `-`, `*`, `/`, `%`를 `&`, `|`를 `^`를 `==`, `!=`, `>`, `<`를 `>=`, 및 `<=` 이항 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-351">Binary numeric promotion occurs for the operands of the predefined `+`, `-`, `*`, `/`, `%`, `&`, `|`, `^`, `==`, `!=`, `>`, `<`, `>=`, and `<=` binary operators.</span></span> <span data-ttu-id="602c5-352">이진 숫자 승격이 비 관계형 연산자의 경우 작업의 결과 형식은 또한 되는 공용 형식으로 두 피연산자를 암시적으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-352">Binary numeric promotion implicitly converts both operands to a common type which, in case of the non-relational operators, also becomes the result type of the operation.</span></span> <span data-ttu-id="602c5-353">여기에 표시 되는 순서에서 다음 규칙을 적용 하는 이진 숫자 승격이 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-353">Binary numeric promotion consists of applying the following rules, in the order they appear here:</span></span>

*  <span data-ttu-id="602c5-354">피연산자 중 하나가 형식인 경우 `decimal`, 다른 피연산자는 형식으로 변환 됩니다 `decimal`, 또는 바인딩 시간 오류가 발생 하는 경우 다른 피연산자가 형식의 `float` 또는 `double`.</span><span class="sxs-lookup"><span data-stu-id="602c5-354">If either operand is of type `decimal`, the other operand is converted to type `decimal`, or a binding-time error occurs if the other operand is of type `float` or `double`.</span></span>
*  <span data-ttu-id="602c5-355">피연산자 중 하나가 형식인 경우 그러지 `double`, 다른 피연산자는 형식으로 변환 됩니다 `double`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-355">Otherwise, if either operand is of type `double`, the other operand is converted to type `double`.</span></span>
*  <span data-ttu-id="602c5-356">피연산자 중 하나가 형식인 경우 그러지 `float`, 다른 피연산자는 형식으로 변환 됩니다 `float`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-356">Otherwise, if either operand is of type `float`, the other operand is converted to type `float`.</span></span>
*  <span data-ttu-id="602c5-357">피연산자 중 하나가 형식인 경우 그러지 `ulong`, 다른 피연산자는 형식으로 변환 됩니다 `ulong`, 바인딩 시간 오류가 발생 하는 경우 다른 피연산자는 형식 또는 `sbyte`, `short`를 `int`, 또는 `long`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-357">Otherwise, if either operand is of type `ulong`, the other operand is converted to type `ulong`, or a binding-time error occurs if the other operand is of type `sbyte`, `short`, `int`, or `long`.</span></span>
*  <span data-ttu-id="602c5-358">피연산자 중 하나가 형식인 경우 그러지 `long`, 다른 피연산자는 형식으로 변환 됩니다 `long`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-358">Otherwise, if either operand is of type `long`, the other operand is converted to type `long`.</span></span>
*  <span data-ttu-id="602c5-359">피연산자 중 하나가 형식인 경우 그러지 `uint` 이 고 다른 피연산자가 형식의 `sbyte`, `short`, 또는 `int`, 두 피연산자는 형식으로 변환 됩니다 `long`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-359">Otherwise, if either operand is of type `uint` and the other operand is of type `sbyte`, `short`, or `int`, both operands are converted to type `long`.</span></span>
*  <span data-ttu-id="602c5-360">피연산자 중 하나가 형식인 경우 그러지 `uint`, 다른 피연산자는 형식으로 변환 됩니다 `uint`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-360">Otherwise, if either operand is of type `uint`, the other operand is converted to type `uint`.</span></span>
*  <span data-ttu-id="602c5-361">그렇지 않은 경우 두 피연산자는 형식으로 변환할 `int`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-361">Otherwise, both operands are converted to type `int`.</span></span>

<span data-ttu-id="602c5-362">첫 번째 규칙을 혼합 하는 작업을 허용 하지 않습니다는 참고 합니다 `decimal` 유형과 합니다 `double` 및 `float` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-362">Note that the first rule disallows any operations that mix the `decimal` type with the `double` and `float` types.</span></span> <span data-ttu-id="602c5-363">간의 암시적 변환은 없습니다 한다는 사실에서 규칙을 따릅니다 합니다 `decimal` 형식 및 `double` 및 `float` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-363">The rule follows from the fact that there are no implicit conversions between the `decimal` type and the `double` and `float` types.</span></span>

<span data-ttu-id="602c5-364">형식의 피연산자에 대 한 수 있다는 것을 참고 `ulong` 경우 다른 피연산자가 부호 있는 정수 계열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-364">Also note that it is not possible for an operand to be of type `ulong` when the other operand is of a signed integral type.</span></span> <span data-ttu-id="602c5-365">정수 계열 형식이 존재 하지 않습니다 하는 이유는 전체 범위를 나타낼 수 있습니다 `ulong` 부호 있는 정수 계열 형식 뿐만 아니라 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-365">The reason is that no integral type exists that can represent the full range of `ulong` as well as the signed integral types.</span></span>

<span data-ttu-id="602c5-366">위의 경우 모두, 캐스트 식은 다른 피연산자와 호환 되는 형식에 하나의 피연산자를 명시적으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-366">In both of the above cases, a cast expression can be used to explicitly convert one operand to a type that is compatible with the other operand.</span></span>

<span data-ttu-id="602c5-367">예제</span><span class="sxs-lookup"><span data-stu-id="602c5-367">In the example</span></span>
```csharp
decimal AddPercent(decimal x, double percent) {
    return x * (1.0 + percent / 100.0);
}
```
<span data-ttu-id="602c5-368">바인딩 시간 오류 때문에 발생 한 `decimal` 곱할 수 없습니다는 `double`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-368">a binding-time error occurs because a `decimal` cannot be multiplied by a `double`.</span></span> <span data-ttu-id="602c5-369">두 번째 피연산자를 명시적으로 변환 하 여 오류가 해결 될 `decimal`다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-369">The error is resolved by explicitly converting the second operand to `decimal`, as follows:</span></span>

```csharp
decimal AddPercent(decimal x, double percent) {
    return x * (decimal)(1.0 + percent / 100.0);
}
```

### <a name="lifted-operators"></a><span data-ttu-id="602c5-370">리프트 된 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-370">Lifted operators</span></span>

<span data-ttu-id="602c5-371">***연산자 리프트*** 도 이러한 형식의 null 허용 형식으로 사용할 nullable이 아닌 값 형식에서 작동 하는 미리 정의 된 및 사용자 정의 연산자를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-371">***Lifted operators*** permit predefined and user-defined operators that operate on non-nullable value types to also be used with nullable forms of those types.</span></span> <span data-ttu-id="602c5-372">리프트 된 연산자는 다음에 설명 된 대로 특정 요구 사항을 충족 하는 미리 정의 된 및 사용자 정의 연산자에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-372">Lifted operators are constructed from predefined and user-defined operators that meet certain requirements, as described in the following:</span></span>

*   <span data-ttu-id="602c5-373">단항 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-373">For the unary operators</span></span>

    ```csharp
    +  ++  -  --  !  ~
    ```

    <span data-ttu-id="602c5-374">운영자의 리프트 된 형태는 피연산자와 결과 형식이 모두 nullable이 아닌 값 형식인 경우 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-374">a lifted form of an operator exists if the operand and result types are both non-nullable value types.</span></span> <span data-ttu-id="602c5-375">리프트는 폼이 단일을 추가 하 여 생성 된 `?` 피연산자와 결과 형식에는 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-375">The lifted form is constructed by adding a single `?` modifier to the operand and result types.</span></span> <span data-ttu-id="602c5-376">리프트 된 연산자는 피연산자가 null 이면 null 값을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-376">The lifted operator produces a null value if the operand is null.</span></span> <span data-ttu-id="602c5-377">이 고, 그렇지 리프트 된 연산자는 피연산자의 래핑을 해제 기본 연산자를 적용 되며 결과 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-377">Otherwise, the lifted operator unwraps the operand, applies the underlying operator, and wraps the result.</span></span>

*   <span data-ttu-id="602c5-378">이항 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-378">For the binary operators</span></span>

    ```csharp
    +  -  *  /  %  &  |  ^  <<  >>
    ```

    <span data-ttu-id="602c5-379">운영자의 리프트 된 형태는 피연산자와 결과 형식이 모든 비 nullable 값 형식인 경우 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-379">a lifted form of an operator exists if the operand and result types are all non-nullable value types.</span></span> <span data-ttu-id="602c5-380">리프트는 폼이 단일을 추가 하 여 생성 된 `?` 각 피연산자와 결과 형식에는 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-380">The lifted form is constructed by adding a single `?` modifier to each operand and result type.</span></span> <span data-ttu-id="602c5-381">리프트 된 연산자를 null 값을 생성 하는 경우 하나 또는 두 피연산자가 null 인 (되는 예외를 `&` 하 고 `|` 연산자는 `bool?` 에 설명 된 대로 입력 [부울 논리 연산자](expressions.md#boolean-logical-operators)).</span><span class="sxs-lookup"><span data-stu-id="602c5-381">The lifted operator produces a null value if one or both operands are null (an exception being the `&` and `|` operators of the `bool?` type, as described in [Boolean logical operators](expressions.md#boolean-logical-operators)).</span></span> <span data-ttu-id="602c5-382">이 고, 그렇지 리프트 된 연산자는 피연산자의 래핑을 해제 기본 연산자에 적용 되며 결과 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-382">Otherwise, the lifted operator unwraps the operands, applies the underlying operator, and wraps the result.</span></span>

*   <span data-ttu-id="602c5-383">같음 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-383">For the equality operators</span></span>

    ```csharp
    ==  !=
    ```

    <span data-ttu-id="602c5-384">리프트 된 연산자의 형태가 피연산자 형식이 nullable이 아닌 값 형식 및 결과 형식이 인지 모두 않으면 `bool`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-384">a lifted form of an operator exists if the operand types are both non-nullable value types and if the result type is `bool`.</span></span> <span data-ttu-id="602c5-385">리프트는 폼이 단일을 추가 하 여 생성 된 `?` 각 피연산자 형식에는 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-385">The lifted form is constructed by adding a single `?` modifier to each operand type.</span></span> <span data-ttu-id="602c5-386">리프트 된 연산자 고려 두 개의 null 값 같음 및 null 값을 null이 아닌 값으로 같지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-386">The lifted operator considers two null values equal, and a null value unequal to any non-null value.</span></span> <span data-ttu-id="602c5-387">두 피연산자 모두 null이 아닌 경우 리프트 된 연산자 피연산자의 래핑을 해제 하 고 생성 하는 기본 연산자를 적용 합니다 `bool` 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-387">If both operands are non-null, the lifted operator unwraps the operands and applies the underlying operator to produce the `bool` result.</span></span>

*   <span data-ttu-id="602c5-388">관계형 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-388">For the relational operators</span></span>

    ```csharp
    <  >  <=  >=
    ```

    <span data-ttu-id="602c5-389">리프트 된 연산자의 형태가 피연산자 형식이 nullable이 아닌 값 형식 및 결과 형식이 인지 모두 않으면 `bool`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-389">a lifted form of an operator exists if the operand types are both non-nullable value types and if the result type is `bool`.</span></span> <span data-ttu-id="602c5-390">리프트는 폼이 단일을 추가 하 여 생성 된 `?` 각 피연산자 형식에는 한정자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-390">The lifted form is constructed by adding a single `?` modifier to each operand type.</span></span> <span data-ttu-id="602c5-391">리프트 된 연산자에 값을 생성 `false` 하나 또는 두 피연산자가 null 인 경우.</span><span class="sxs-lookup"><span data-stu-id="602c5-391">The lifted operator produces the value `false` if one or both operands are null.</span></span> <span data-ttu-id="602c5-392">리프트 된 연산자는 피연산자의 래핑을 해제 하 고 생성 하는 기본 연산자를 적용 하는 고, 그렇지는 `bool` 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-392">Otherwise, the lifted operator unwraps the operands and applies the underlying operator to produce the `bool` result.</span></span>

## <a name="member-lookup"></a><span data-ttu-id="602c5-393">멤버 조회</span><span class="sxs-lookup"><span data-stu-id="602c5-393">Member lookup</span></span>

<span data-ttu-id="602c5-394">멤버 조회 하는 프로세스 컨텍스트에서 형식 이름의 의미를 여기서 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-394">A member lookup is the process whereby the meaning of a name in the context of a type is determined.</span></span> <span data-ttu-id="602c5-395">멤버 조회 평가의 일부로 발생할 수 있습니다는 *simple_name* ([단순 이름](expressions.md#simple-names)) 또는 *member_access* ([멤버 액세스](expressions.md#member-access))에 식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-395">A member lookup can occur as part of evaluating a *simple_name* ([Simple names](expressions.md#simple-names)) or a *member_access* ([Member access](expressions.md#member-access)) in an expression.</span></span> <span data-ttu-id="602c5-396">경우는 *simple_name* 또는 *member_access* 으로 발생 합니다 *primary_expression* 의 *invocation_expression* ([ 메서드 호출](expressions.md#method-invocations)), 호출할 멤버 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-396">If the *simple_name* or *member_access* occurs as the *primary_expression* of an *invocation_expression* ([Method invocations](expressions.md#method-invocations)), the member is said to be invoked.</span></span>

<span data-ttu-id="602c5-397">구성원은 메서드 또는 이벤트 또는 상수, 필드 또는 속성 중 하나는 대리자 형식의 경우 ([대리자](delegates.md)) 또는 형식 `dynamic` ([동적 형식](types.md#the-dynamic-type)), 멤버 를라고합니다.그런다음*invocable*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-397">If a member is a method or event, or if it is a constant, field or property of either a delegate type ([Delegates](delegates.md)) or the type `dynamic` ([The dynamic type](types.md#the-dynamic-type)), then the member is said to be *invocable*.</span></span>

<span data-ttu-id="602c5-398">멤버 조회 뿐만 아니라 이름의 멤버 뿐만 아니라 개수 멤버에 형식 매개 변수 및 멤버에 액세스할 수 있는지 여부를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-398">Member lookup considers not only the name of a member but also the number of type parameters the member has and whether the member is accessible.</span></span> <span data-ttu-id="602c5-399">멤버 조회에서는 제네릭 메서드 및 중첩 된 제네릭 형식을 형식 매개 변수는 해당 선언에 지정 된 수 있고 다른 모든 멤버 0 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-399">For the purposes of member lookup, generic methods and nested generic types have the number of type parameters indicated in their respective declarations and all other members have zero type parameters.</span></span>

<span data-ttu-id="602c5-400">이름의 멤버 조회 `N` 사용 하 여 `K` 형식에서 형식 매개 변수 `T` 다음과 같이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-400">A member lookup of a name `N` with `K` type parameters in a type `T` is processed as follows:</span></span>

*  <span data-ttu-id="602c5-401">먼저, 액세스할 수 있는 멤버를 명명 된 집합이 `N` 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-401">First, a set of accessible members named `N` is determined:</span></span>
    * <span data-ttu-id="602c5-402">하는 경우 `T` 가 형식 매개 변수 집합에 액세스할 수 있는 멤버를 명명 된 집합의 합집합 `N` 각 보조 제약 조건 또는 기본 제약 조건으로 지정 된 형식에서 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints))에 대 한 `T`에 액세스할 수 있는 멤버를 명명 된 집합이 함께 `N` 에서 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-402">If `T` is a type parameter, then the set is the union of the sets of accessible members named `N` in each of the types specified as a primary constraint or secondary constraint ([Type parameter constraints](classes.md#type-parameter-constraints)) for `T`, along with the set of accessible members named `N` in `object`.</span></span>
    * <span data-ttu-id="602c5-403">이 고, 그렇지는 구성 된 집합 모두 액세스할 수 있습니다 ([멤버 액세스](basic-concepts.md#member-access)) 라는 멤버 `N` 에서 `T`상속 된 멤버 및 명명 된 액세스할 수 있는 멤버를 비롯 한 `N` 에서 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-403">Otherwise, the set consists of all accessible ([Member access](basic-concepts.md#member-access)) members named `N` in `T`, including inherited members and the accessible members named `N` in `object`.</span></span> <span data-ttu-id="602c5-404">하는 경우 `T` 생성 된 형식인 멤버 집합에 설명 된 대로 형식 인수를 대체 하 여 가져온 [생성 된 형식의 멤버](classes.md#members-of-constructed-types)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-404">If `T` is a constructed type, the set of members is obtained by substituting type arguments as described in [Members of constructed types](classes.md#members-of-constructed-types).</span></span> <span data-ttu-id="602c5-405">포함 하는 멤버는 `override` 한정자 집합에서 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-405">Members that include an `override` modifier are excluded from the set.</span></span>
*  <span data-ttu-id="602c5-406">다음으로 `K` 가 0 이면 모든 중첩 된 형식을 형식 매개 변수를 포함 하는 해당 선언에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-406">Next, if `K` is zero, all nested types whose declarations include type parameters are removed.</span></span> <span data-ttu-id="602c5-407">경우 `K` 0이 아니면 모든 멤버 수가 서로 다른 형식 매개 변수가 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-407">If `K` is not zero, all members with a different number of type parameters are removed.</span></span> <span data-ttu-id="602c5-408">경우 `K` 0 메서드 형식 매개 변수 제거 되지 않습니다 형식 유추 프로세스 이후 것 ([형식 유추](expressions.md#type-inference)) 형식 인수를 유추 하는 일을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-408">Note that when `K` is zero, methods having type parameters are not removed, since the type inference process ([Type inference](expressions.md#type-inference)) might be able to infer the type arguments.</span></span>
*  <span data-ttu-id="602c5-409">다음을 멤버인 경우 *호출*, 모든 비-*invocable* 멤버 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-409">Next, if the member is *invoked*, all non-*invocable* members are removed from the set.</span></span>
*  <span data-ttu-id="602c5-410">다음으로, 다른 멤버가 숨겨져 있는 멤버 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-410">Next, members that are hidden by other members are removed from the set.</span></span> <span data-ttu-id="602c5-411">모든 멤버에 대 한 `S.M` 집합에 위치 `S` 는 형식이 멤버 `M` 가 선언 된 다음 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-411">For every member `S.M` in the set, where `S` is the type in which the member `M` is declared, the following rules are applied:</span></span>
    * <span data-ttu-id="602c5-412">하는 경우 `M` 의 기본 형식에서 선언 된 모든 멤버는 상수, 필드, 속성, 이벤트 또는 열거형 멤버를이 `S` 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-412">If `M` is a constant, field, property, event, or enumeration member, then all members declared in a base type of `S` are removed from the set.</span></span>
    * <span data-ttu-id="602c5-413">경우 `M` 형식 선언 이면 모든 아닌 형식을 기본 형식에서 선언 `S` 집합에서 제거 됩니다 모든 형식으로 형식 매개 변수 수가 사용 하 여 선언 하 고 `M` 의 기본 형식에서 선언 된 `S` 제거 됩니다 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-413">If `M` is a type declaration, then all non-types declared in a base type of `S` are removed from the set, and all type declarations with the same number of type parameters as `M` declared in a base type of `S` are removed from the set.</span></span>
    * <span data-ttu-id="602c5-414">하는 경우 `M` 모든 메서드가 아닌 멤버의 기본 형식에서 선언 된 메서드를가 `S` 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-414">If `M` is a method, then all non-method members declared in a base type of `S` are removed from the set.</span></span>
*  <span data-ttu-id="602c5-415">다음으로, 클래스 멤버에 의해 숨겨진 된 인터페이스 멤버 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-415">Next, interface members that are hidden by class members are removed from the set.</span></span> <span data-ttu-id="602c5-416">이 단계에만 적용 하는 경우 `T` 는 형식 매개 변수 및 `T` 이외의 모두는 유효한 기본 클래스에 `object` 설정 비어 있지 않은 효과적인 인터페이스 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="602c5-416">This step only has an effect if `T` is a type parameter and `T` has both an effective base class other than `object` and a non-empty effective interface set ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span> <span data-ttu-id="602c5-417">모든 멤버에 대 한 `S.M` 집합에 있는 `S` 나타나는 형식인 멤버 `M` 가 선언 된 경우 다음 규칙이 적용 됩니다 `S` 은 클래스 선언 이외의 `object`:</span><span class="sxs-lookup"><span data-stu-id="602c5-417">For every member `S.M` in the set, where `S` is the type in which the member `M` is declared, the following rules are applied if `S` is a class declaration other than `object`:</span></span>
    * <span data-ttu-id="602c5-418">경우 `M` 이면 상수, 필드, 속성, 이벤트, 열거형 멤버 또는 형식 선언 인터페이스 선언에서 선언 된 모든 멤버 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-418">If `M` is a constant, field, property, event, enumeration member, or type declaration, then all members declared in an interface declaration are removed from the set.</span></span>
    * <span data-ttu-id="602c5-419">하는 경우 `M` 인터페이스 선언에서 선언 된 모든 메서드가 아닌 멤버 집합과 동일한 시그니처가 있는 모든 방법에서 제거 되는 메서드이기 `M` 선언 된 인터페이스 선언 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-419">If `M` is a method, then all non-method members declared in an interface declaration are removed from the set, and all methods with the same signature as `M` declared in an interface declaration are removed from the set.</span></span>
*  <span data-ttu-id="602c5-420">조회 결과 숨겨진된 멤버를 제거, 마지막으로 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-420">Finally, having removed hidden members, the result of the lookup is determined:</span></span>
    * <span data-ttu-id="602c5-421">집합 메서드 없는 단일 구성원으로 구성 된 경우이 멤버는 조회 결과.</span><span class="sxs-lookup"><span data-stu-id="602c5-421">If the set consists of a single member that is not a method, then this member is the result of the lookup.</span></span>
    * <span data-ttu-id="602c5-422">이 고, 그렇지 집합 방법만 있으면 메서드의이 그룹은 조회 결과.</span><span class="sxs-lookup"><span data-stu-id="602c5-422">Otherwise, if the set contains only methods, then this group of methods is the result of the lookup.</span></span>
    * <span data-ttu-id="602c5-423">이 고, 그렇지 조회 모호 하 고 바인딩 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-423">Otherwise, the lookup is ambiguous, and a binding-time error occurs.</span></span>

<span data-ttu-id="602c5-424">형식 매개 변수 및 인터페이스 이외의 형식에서 멤버 조회 및 단일 상속 된 인터페이스 멤버 조회에 대 한 (상속 체인의 각 인터페이스에 정확히 0 개 이상의 직접 기본 인터페이스)는 조회 규칙의 효과 단순히는 멤버 이름 또는 시그니처가 같은 사용 하 여 기본 멤버 숨기기를 파생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-424">For member lookups in types other than type parameters and interfaces, and member lookups in interfaces that are strictly single-inheritance (each interface in the inheritance chain has exactly zero or one direct base interface), the effect of the lookup rules is simply that derived members hide base members with the same name or signature.</span></span> <span data-ttu-id="602c5-425">이러한 단일 상속 조회는 모호 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-425">Such single-inheritance lookups are never ambiguous.</span></span> <span data-ttu-id="602c5-426">설명 하는 다중 상속 인터페이스의 멤버 조회에서 발생할 수 있는 모호성 [인터페이스 멤버 액세스](interfaces.md#interface-member-access)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-426">The ambiguities that can possibly arise from member lookups in multiple-inheritance interfaces are described in [Interface member access](interfaces.md#interface-member-access).</span></span>

### <a name="base-types"></a><span data-ttu-id="602c5-427">기본 형식</span><span class="sxs-lookup"><span data-stu-id="602c5-427">Base types</span></span>

<span data-ttu-id="602c5-428">형식 멤버 조회의 목적을 위해 `T` 기본 형식은 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-428">For purposes of member lookup, a type `T` is considered to have the following base types:</span></span>

*  <span data-ttu-id="602c5-429">하는 경우 `T` 됩니다 `object`, 다음 `T` 에 기본 형식이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-429">If `T` is `object`, then `T` has no base type.</span></span>
*  <span data-ttu-id="602c5-430">경우 `T` 은 *enum_type*, 기본 유형의 `T` 클래스 유형은 `System.Enum`, `System.ValueType`, 및 `object`.</span><span class="sxs-lookup"><span data-stu-id="602c5-430">If `T` is an *enum_type*, the base types of `T` are the class types `System.Enum`, `System.ValueType`, and `object`.</span></span>
*  <span data-ttu-id="602c5-431">경우 `T` 은 *struct_type*, 기본 유형의 `T` 클래스 유형은 `System.ValueType` 및 `object`.</span><span class="sxs-lookup"><span data-stu-id="602c5-431">If `T` is a *struct_type*, the base types of `T` are the class types `System.ValueType` and `object`.</span></span>
*  <span data-ttu-id="602c5-432">경우 `T` 은 *class_type*, 기본 유형의 `T` 의 기본 클래스는 `T`, 클래스 유형을 포함 하 여 `object`.</span><span class="sxs-lookup"><span data-stu-id="602c5-432">If `T` is a *class_type*, the base types of `T` are the base classes of `T`, including the class type `object`.</span></span>
*  <span data-ttu-id="602c5-433">경우 `T` 은 *interface_type*, 기본 유형의 `T` 의 기본 인터페이스는 `T` 클래스 형식과 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-433">If `T` is an *interface_type*, the base types of `T` are the base interfaces of `T` and the class type `object`.</span></span>
*  <span data-ttu-id="602c5-434">경우 `T` 은 *array_type*, 기본 유형의 `T` 클래스 유형은 `System.Array` 및 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-434">If `T` is an *array_type*, the base types of `T` are the class types `System.Array` and `object`.</span></span>
*  <span data-ttu-id="602c5-435">경우 `T` 은 *delegate_type*, 기본 유형의 `T` 클래스 유형은 `System.Delegate` 및 `object`.</span><span class="sxs-lookup"><span data-stu-id="602c5-435">If `T` is a *delegate_type*, the base types of `T` are the class types `System.Delegate` and `object`.</span></span>

## <a name="function-members"></a><span data-ttu-id="602c5-436">함수 멤버</span><span class="sxs-lookup"><span data-stu-id="602c5-436">Function members</span></span>

<span data-ttu-id="602c5-437">멤버 함수는 실행 가능 문을 포함 하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-437">Function members are members that contain executable statements.</span></span> <span data-ttu-id="602c5-438">함수 멤버는 형식의 멤버는 항상 및 네임 스페이스의 구성원이 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-438">Function members are always members of types and cannot be members of namespaces.</span></span> <span data-ttu-id="602c5-439">C#에서는 다음과 같은 범주의 함수 멤버를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-439">C# defines the following categories of function members:</span></span>

*  <span data-ttu-id="602c5-440">메서드</span><span class="sxs-lookup"><span data-stu-id="602c5-440">Methods</span></span>
*  <span data-ttu-id="602c5-441">속성</span><span class="sxs-lookup"><span data-stu-id="602c5-441">Properties</span></span>
*  <span data-ttu-id="602c5-442">이벤트</span><span class="sxs-lookup"><span data-stu-id="602c5-442">Events</span></span>
*  <span data-ttu-id="602c5-443">인덱서</span><span class="sxs-lookup"><span data-stu-id="602c5-443">Indexers</span></span>
*  <span data-ttu-id="602c5-444">사용자 정의 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-444">User-defined operators</span></span>
*  <span data-ttu-id="602c5-445">인스턴스 생성자</span><span class="sxs-lookup"><span data-stu-id="602c5-445">Instance constructors</span></span>
*  <span data-ttu-id="602c5-446">정적 생성자</span><span class="sxs-lookup"><span data-stu-id="602c5-446">Static constructors</span></span>
*  <span data-ttu-id="602c5-447">소멸자</span><span class="sxs-lookup"><span data-stu-id="602c5-447">Destructors</span></span>

<span data-ttu-id="602c5-448">(명시적으로 호출할 수 없습니다)는 정적 생성자 및 소멸자를 제외 하 고 함수 멤버에 포함 된 문의 함수 멤버 호출을 통해 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-448">Except for destructors and static constructors (which cannot be invoked explicitly), the statements contained in function members are executed through function member invocations.</span></span> <span data-ttu-id="602c5-449">함수 멤버 호출을 작성 하는 실제 구문은 특정 함수 멤버 범주에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-449">The actual syntax for writing a function member invocation depends on the particular function member category.</span></span>

<span data-ttu-id="602c5-450">인수 목록 ([인수 목록](expressions.md#argument-lists)) 함수 멤버의 호출 실제 값 또는 변수 참조를 제공 하는 함수 멤버의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-450">The argument list ([Argument lists](expressions.md#argument-lists)) of a function member invocation provides actual values or variable references for the parameters of the function member.</span></span>

<span data-ttu-id="602c5-451">제네릭 메서드는 호출 된 메서드에 전달할 형식 인수 집합을 결정 하는 형식 유추를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-451">Invocations of generic methods may employ type inference to determine the set of type arguments to pass to the method.</span></span> <span data-ttu-id="602c5-452">이 프로세스에 설명 되어 [형식 유추](expressions.md#type-inference)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-452">This process is described in [Type inference](expressions.md#type-inference).</span></span>

<span data-ttu-id="602c5-453">메서드, 인덱서, 연산자 및 인스턴스 생성자의 호출 함수를 호출 하는 멤버의 후보 집합을 결정 하기 위해 오버 로드 확인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-453">Invocations of methods, indexers, operators and instance constructors employ overload resolution to determine which of a candidate set of function members to invoke.</span></span> <span data-ttu-id="602c5-454">이 프로세스에 설명 되어 [오버 로드 확인](expressions.md#overload-resolution)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-454">This process is described in [Overload resolution](expressions.md#overload-resolution).</span></span>

<span data-ttu-id="602c5-455">바인딩 시간에 특정 함수 멤버를 식별 가능한 오버 로드 확인을 통해 호출 하는 함수 멤버의 실제 런타임 프로세스에서 설명 하는 [컴파일 타임 검사가동적오버로드확인](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="602c5-455">Once a particular function member has been identified at binding-time, possibly through overload resolution, the actual run-time process of invoking the function member is described in [Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span></span>

<span data-ttu-id="602c5-456">다음 표에서 명시적으로 호출할 수 있는 함수 멤버의 6 개 범주를 포함 하는 구문에서 발생 하는 과정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-456">The following table summarizes the processing that takes place in constructs involving the six categories of function members that can be explicitly invoked.</span></span> <span data-ttu-id="602c5-457">표에 `e`, `x`, `y`, 및 `value` 변수 또는 값으로 분류 하는 식을 나타내는 `T` 형식으로 분류 하는 식을 나타내는 `F` 메서드와 간단한이름인`P` 속성의 단순한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-457">In the table, `e`, `x`, `y`, and `value` indicate expressions classified as variables or values, `T` indicates an expression classified as a type, `F` is the simple name of a method, and `P` is the simple name of a property.</span></span>


| <span data-ttu-id="602c5-458">__구문__</span><span class="sxs-lookup"><span data-stu-id="602c5-458">__Construct__</span></span>     | <span data-ttu-id="602c5-459">__예제__</span><span class="sxs-lookup"><span data-stu-id="602c5-459">__Example__</span></span>    | <span data-ttu-id="602c5-460">__설명__</span><span class="sxs-lookup"><span data-stu-id="602c5-460">__Description__</span></span> |
|-------------------|----------------|-----------------|
| <span data-ttu-id="602c5-461">메서드 호출</span><span class="sxs-lookup"><span data-stu-id="602c5-461">Method invocation</span></span> | `F(x,y)`       | <span data-ttu-id="602c5-462">최상의 방법을 선택 하기 오버 로드 확인을 적용 `F` 클래스 또는 구조체에서.</span><span class="sxs-lookup"><span data-stu-id="602c5-462">Overload resolution is applied to select the best method `F` in the containing class or struct.</span></span> <span data-ttu-id="602c5-463">메서드가 호출 된 인수 목록을 사용 하 여 `(x,y)`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-463">The method is invoked with the argument list `(x,y)`.</span></span> <span data-ttu-id="602c5-464">메서드가 없는 경우 `static`, 인스턴스 식은 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-464">If the method is not `static`, the instance expression is `this`.</span></span> | 
|                   | `T.F(x,y)`     | <span data-ttu-id="602c5-465">최상의 방법을 선택 하기 오버 로드 확인을 적용 `F` 클래스나 구조체에서 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-465">Overload resolution is applied to select the best method `F` in the class or struct `T`.</span></span> <span data-ttu-id="602c5-466">바인딩 시간 오류가 발생 하는 메서드가 없는 경우 `static`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-466">A binding-time error occurs if the method is not `static`.</span></span> <span data-ttu-id="602c5-467">메서드가 호출 된 인수 목록을 사용 하 여 `(x,y)`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-467">The method is invoked with the argument list `(x,y)`.</span></span> | 
|                   | `e.F(x,y)`     | <span data-ttu-id="602c5-468">클래스, 구조체 또는 인터페이스의 형식에 의해 지정 된 최상의 방법을 F를 선택 하기 오버 로드 확인을 적용 `e`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-468">Overload resolution is applied to select the best method F in the class, struct, or interface given by the type of `e`.</span></span> <span data-ttu-id="602c5-469">바인딩 시간 오류가 발생 하는 방법이 `static`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-469">A binding-time error occurs if the method is `static`.</span></span> <span data-ttu-id="602c5-470">메서드가 호출 된 인스턴스 식이 `e` 및 인수 목록을 `(x,y)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-470">The method is invoked with the instance expression `e` and the argument list `(x,y)`.</span></span> | 
| <span data-ttu-id="602c5-471">속성 액세스</span><span class="sxs-lookup"><span data-stu-id="602c5-471">Property access</span></span>   | `P`            | <span data-ttu-id="602c5-472">합니다 `get` 속성의 접근자 `P` 클래스 또는 구조체에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-472">The `get` accessor of the property `P` in the containing class or struct is invoked.</span></span> <span data-ttu-id="602c5-473">컴파일 타임 오류가 발생 하는 경우 `P` 쓰기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-473">A compile-time error occurs if `P` is write-only.</span></span> <span data-ttu-id="602c5-474">하는 경우 `P` 아닙니다 `static`, 인스턴스 식은 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-474">If `P` is not `static`, the instance expression is `this`.</span></span> | 
|                   | `P = value`    | <span data-ttu-id="602c5-475">합니다 `set` 속성의 접근자 `P` 포함 하는 클래스나 구조체가 호출 된 인수 목록과 `(value)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-475">The `set` accessor of the property `P` in the containing class or struct is invoked with the argument list `(value)`.</span></span> <span data-ttu-id="602c5-476">컴파일 타임 오류가 발생 하는 경우 `P` 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-476">A compile-time error occurs if `P` is read-only.</span></span> <span data-ttu-id="602c5-477">하는 경우 `P` 아닙니다 `static`, 인스턴스 식은 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-477">If `P` is not `static`, the instance expression is `this`.</span></span> | 
|                   | `T.P`          | <span data-ttu-id="602c5-478">합니다 `get` 속성의 접근자 `P` 클래스나 구조체에서 `T` 가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-478">The `get` accessor of the property `P` in the class or struct `T` is invoked.</span></span> <span data-ttu-id="602c5-479">컴파일 타임 오류가 발생 하는 경우 `P` 아닙니다 `static` 이거나 `P` 쓰기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-479">A compile-time error occurs if `P` is not `static` or if `P` is write-only.</span></span> | 
|                   | `T.P = value`  | <span data-ttu-id="602c5-480">`set` 속성의 접근자 `P` 클래스 또는 구조체 `T` 인수 목록을 사용 하 여 호출 `(value)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-480">The `set` accessor of the property `P` in the class or struct `T` is invoked with the argument list `(value)`.</span></span> <span data-ttu-id="602c5-481">컴파일 타임 오류가 발생 하는 경우 `P` 아닙니다 `static` 이거나 `P` 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-481">A compile-time error occurs if `P` is not `static` or if `P` is read-only.</span></span> | 
|                   | `e.P`          | <span data-ttu-id="602c5-482">합니다 `get` 속성의 접근자 `P` 클래스, 구조체 또는 인터페이스의 형식에 의해 지정 된 `e` 인스턴스 식을 사용 하 여 호출 `e`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-482">The `get` accessor of the property `P` in the class, struct, or interface given by the type of `e` is invoked with the instance expression `e`.</span></span> <span data-ttu-id="602c5-483">바인딩 시간 오류가 발생 하는 경우 `P` 됩니다 `static` 이거나 `P` 쓰기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-483">A binding-time error occurs if `P` is `static` or if `P` is write-only.</span></span> | 
|                   | `e.P = value`  | <span data-ttu-id="602c5-484">합니다 `set` 속성의 접근자 `P` 클래스, 구조체 또는 인터페이스의 형식에 의해 지정 된 `e` 인스턴스 식을 사용 하 여 호출 됩니다 `e` 인수 목록과 `(value)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-484">The `set` accessor of the property `P` in the class, struct, or interface given by the type of `e` is invoked with the instance expression `e` and the argument list `(value)`.</span></span> <span data-ttu-id="602c5-485">바인딩 시간 오류가 발생 하는 경우 `P` 됩니다 `static` 이거나 `P` 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-485">A binding-time error occurs if `P` is `static` or if `P` is read-only.</span></span> | 
| <span data-ttu-id="602c5-486">이벤트 액세스</span><span class="sxs-lookup"><span data-stu-id="602c5-486">Event access</span></span>      | `E += value`   | <span data-ttu-id="602c5-487">합니다 `add` 이벤트의 접근자 `E` 클래스 또는 구조체에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-487">The `add` accessor of the event `E` in the containing class or struct is invoked.</span></span> <span data-ttu-id="602c5-488">하는 경우 `E` 는 static이 아닌 인스턴스 식은 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-488">If `E` is not static, the instance expression is `this`.</span></span> | 
|                   | `E -= value`   | <span data-ttu-id="602c5-489">합니다 `remove` 이벤트의 접근자 `E` 클래스 또는 구조체에서 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-489">The `remove` accessor of the event `E` in the containing class or struct is invoked.</span></span> <span data-ttu-id="602c5-490">하는 경우 `E` 는 static이 아닌 인스턴스 식은 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-490">If `E` is not static, the instance expression is `this`.</span></span> | 
|                   | `T.E += value` | <span data-ttu-id="602c5-491">합니다 `add` 이벤트의 접근자 `E` 클래스나 구조체에서 `T` 가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-491">The `add` accessor of the event `E` in the class or struct `T` is invoked.</span></span> <span data-ttu-id="602c5-492">바인딩 시간 오류가 발생 하는 경우 `E` static이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-492">A binding-time error occurs if `E` is not static.</span></span> | 
|                   | `T.E -= value` | <span data-ttu-id="602c5-493">합니다 `remove` 이벤트의 접근자 `E` 클래스나 구조체에서 `T` 가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-493">The `remove` accessor of the event `E` in the class or struct `T` is invoked.</span></span> <span data-ttu-id="602c5-494">바인딩 시간 오류가 발생 하는 경우 `E` static이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-494">A binding-time error occurs if `E` is not static.</span></span> | 
|                   | `e.E += value` | <span data-ttu-id="602c5-495">합니다 `add` 이벤트의 접근자 `E` 클래스, 구조체 또는 인터페이스의 형식에 의해 지정 된 `e` 인스턴스 식을 사용 하 여 호출 `e`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-495">The `add` accessor of the event `E` in the class, struct, or interface given by the type of `e` is invoked with the instance expression `e`.</span></span> <span data-ttu-id="602c5-496">바인딩 시간 오류가 발생 하는 경우 `E` 고정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-496">A binding-time error occurs if `E` is static.</span></span> | 
|                   | `e.E -= value` | <span data-ttu-id="602c5-497">합니다 `remove` 이벤트의 접근자 `E` 클래스, 구조체 또는 인터페이스의 형식에 의해 지정 된 `e` 인스턴스 식을 사용 하 여 호출 `e`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-497">The `remove` accessor of the event `E` in the class, struct, or interface given by the type of `e` is invoked with the instance expression `e`.</span></span> <span data-ttu-id="602c5-498">바인딩 시간 오류가 발생 하는 경우 `E` 고정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-498">A binding-time error occurs if `E` is static.</span></span> | 
| <span data-ttu-id="602c5-499">인덱서 액세스</span><span class="sxs-lookup"><span data-stu-id="602c5-499">Indexer access</span></span>    | `e[x,y]`       | <span data-ttu-id="602c5-500">오버 로드 확인은 최고 클래스, 구조체 또는 e 형식으로 지정 된 인터페이스의 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-500">Overload resolution is applied to select the best indexer in the class, struct, or interface given by the type of e.</span></span> <span data-ttu-id="602c5-501">합니다 `get` 인덱서의 접근자가 인스턴스 식을 사용 하 여 호출 됩니다 `e` 인수 목록과 `(x,y)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-501">The `get` accessor of the indexer is invoked with the instance expression `e` and the argument list `(x,y)`.</span></span> <span data-ttu-id="602c5-502">인덱서는 쓰기 전용 바인딩 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-502">A binding-time error occurs if the indexer is write-only.</span></span> | 
|                   | `e[x,y] = value` | <span data-ttu-id="602c5-503">오버 로드 확인은 최고 클래스, 구조체 또는 인터페이스의 형식에 의해 지정 된 선택 적용할 `e`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-503">Overload resolution is applied to select the best indexer in the class, struct, or interface given by the type of `e`.</span></span> <span data-ttu-id="602c5-504">합니다 `set` 인덱서의 접근자가 인스턴스 식을 사용 하 여 호출 됩니다 `e` 인수 목록과 `(x,y,value)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-504">The `set` accessor of the indexer is invoked with the instance expression `e` and the argument list `(x,y,value)`.</span></span> <span data-ttu-id="602c5-505">인덱서는 읽기 전용 바인딩 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-505">A binding-time error occurs if the indexer is read-only.</span></span> | 
| <span data-ttu-id="602c5-506">연산자 호출</span><span class="sxs-lookup"><span data-stu-id="602c5-506">Operator invocation</span></span> | `-x`         | <span data-ttu-id="602c5-507">클래스 또는 구조체의 형식이 지정한 최상의 단항 연산자를 선택 하기 오버 로드 확인을 적용 `x`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-507">Overload resolution is applied to select the best unary operator in the class or struct given by the type of `x`.</span></span> <span data-ttu-id="602c5-508">인수 목록을 사용 하 여 선택한 연산자가 호출 `(x)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-508">The selected operator is invoked with the argument list `(x)`.</span></span> | 
|                     | `x + y`      | <span data-ttu-id="602c5-509">클래스 또는 구조체 형식에 따라 지정 된 가장 이항 연산자를 선택 하기 오버 로드 확인을 적용 `x` 고 `y`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-509">Overload resolution is applied to select the best binary operator in the classes or structs given by the types of `x` and `y`.</span></span> <span data-ttu-id="602c5-510">인수 목록을 사용 하 여 선택한 연산자가 호출 `(x,y)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-510">The selected operator is invoked with the argument list `(x,y)`.</span></span> | 
| <span data-ttu-id="602c5-511">인스턴스 생성자 호출</span><span class="sxs-lookup"><span data-stu-id="602c5-511">Instance constructor invocation</span></span> | `new T(x,y)` | <span data-ttu-id="602c5-512">클래스 또는 구조체에서 최상의 인스턴스 생성자를 선택 하기 오버 로드 확인을 적용 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-512">Overload resolution is applied to select the best instance constructor in the class or struct `T`.</span></span> <span data-ttu-id="602c5-513">인스턴스 생성자가 인수 목록을 사용 하 여 호출 `(x,y)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-513">The instance constructor is invoked with the argument list `(x,y)`.</span></span> | 

### <a name="argument-lists"></a><span data-ttu-id="602c5-514">인수 목록</span><span class="sxs-lookup"><span data-stu-id="602c5-514">Argument lists</span></span>

<span data-ttu-id="602c5-515">모든 함수 멤버 및 대리자 호출 하는 함수 멤버의 매개 변수에 대 한 실제 값 또는 변수 참조를 제공 하는 인수 목록이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-515">Every function member and delegate invocation includes an argument list which provides actual values or variable references for the parameters of the function member.</span></span> <span data-ttu-id="602c5-516">함수 멤버 호출의 인수 목록을 지정 하는 구문은 함수 멤버 범주에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-516">The syntax for specifying the argument list of a function member invocation depends on the function member category:</span></span>

*  <span data-ttu-id="602c5-517">예를 들어 생성자, 메서드, 인덱서 및 대리자의 인수는 *argument_list*아래 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-517">For instance constructors, methods, indexers and delegates, the arguments are specified as an *argument_list*, as described below.</span></span> <span data-ttu-id="602c5-518">인덱서를 호출할 때에 `set` 접근자 인수 목록에 대입 연산자의 오른쪽 피연산자로 지정 된 식이 또한 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-518">For indexers, when invoking the `set` accessor, the argument list additionally includes the expression specified as the right operand of the assignment operator.</span></span>
*  <span data-ttu-id="602c5-519">속성에 대 한 인수 목록이 비어를 호출할 때 합니다 `get` 접근자를 호출할 때 대입 연산자의 오른쪽 피연산자로 지정 된 식으로 구성 하 고는 `set` 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-519">For properties, the argument list is empty when invoking the `get` accessor, and consists of the expression specified as the right operand of the assignment operator when invoking the `set` accessor.</span></span>
*  <span data-ttu-id="602c5-520">이벤트에 대 한의 오른쪽 피연산자로 지정 된 식의 인수 목록을 구성 합니다 `+=` 또는 `-=` 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-520">For events, the argument list consists of the expression specified as the right operand of the `+=` or `-=` operator.</span></span>
*  <span data-ttu-id="602c5-521">사용자 정의 연산자에 대 한 인수 목록에는 단항 연산자의 단일 피연산자는 이항 연산자의 두 피연산자의 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-521">For user-defined operators, the argument list consists of the single operand of the unary operator or the two operands of the binary operator.</span></span>

<span data-ttu-id="602c5-522">속성의 인수 ([속성](classes.md#properties)), 이벤트 ([이벤트](classes.md#events)), 및 사용자 정의 연산자 ([연산자](classes.md#operators))는 항상 값 매개 변수로 전달 됩니다 ([ 매개 변수 값](classes.md#value-parameters)).</span><span class="sxs-lookup"><span data-stu-id="602c5-522">The arguments of properties ([Properties](classes.md#properties)), events ([Events](classes.md#events)), and user-defined operators ([Operators](classes.md#operators)) are always passed as value parameters ([Value parameters](classes.md#value-parameters)).</span></span> <span data-ttu-id="602c5-523">인덱서 인수 ([인덱서](classes.md#indexers))는 항상 값 매개 변수로 전달 됩니다 ([매개 변수 값](classes.md#value-parameters)) 또는 매개 변수 배열 ([매개 변수 배열](classes.md#parameter-arrays)).</span><span class="sxs-lookup"><span data-stu-id="602c5-523">The arguments of indexers ([Indexers](classes.md#indexers)) are always passed as value parameters ([Value parameters](classes.md#value-parameters)) or parameter arrays ([Parameter arrays](classes.md#parameter-arrays)).</span></span> <span data-ttu-id="602c5-524">참조 및 출력 매개 변수는 함수 멤버의 이러한 범주에 대 한 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-524">Reference and output parameters are not supported for these categories of function members.</span></span>

<span data-ttu-id="602c5-525">으로 지정 된 인스턴스 생성자, 메서드, 인덱서 또는 대리자 호출의 인수는 *argument_list*:</span><span class="sxs-lookup"><span data-stu-id="602c5-525">The arguments of an instance constructor, method, indexer or delegate invocation are specified as an *argument_list*:</span></span>

```antlr
argument_list
    : argument (',' argument)*
    ;

argument
    : argument_name? argument_value
    ;

argument_name
    : identifier ':'
    ;

argument_value
    : expression
    | 'ref' variable_reference
    | 'out' variable_reference
    ;
```

<span data-ttu-id="602c5-526">*argument_list* 하나 이상의 구성 *인수*s, 쉼표로 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-526">An *argument_list* consists of one or more *argument*s, separated by commas.</span></span> <span data-ttu-id="602c5-527">각 인수는 선택적 구성 *argument_name* 뒤에 *argument_value*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-527">Each argument consists of an optional  *argument_name* followed by an *argument_value*.</span></span> <span data-ttu-id="602c5-528">*인수* 사용 하 여는 *argument_name* 라고는 ***명명 된 인수가***반면는 *인수* 없이  *argument_name* 되는 ***위치 인수***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-528">An *argument* with an *argument_name* is referred to as a ***named argument***, whereas an *argument* without an *argument_name* is a ***positional argument***.</span></span> <span data-ttu-id="602c5-529">명명 된 인수를 뒤에 위치 인수에 대 한 오류가 발생 한 *argument_list*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-529">It is an error for a positional argument to appear after a named argument in an *argument_list*.</span></span>

<span data-ttu-id="602c5-530">합니다 *argument_value* 다음 형식 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-530">The *argument_value* can take one of the following forms:</span></span>

*  <span data-ttu-id="602c5-531">*식*를 나타내는 인수가 값 매개 변수로 전달 됩니다 ([매개 변수 값](classes.md#value-parameters)).</span><span class="sxs-lookup"><span data-stu-id="602c5-531">An *expression*, indicating that the argument is passed as a value parameter ([Value parameters](classes.md#value-parameters)).</span></span>
*  <span data-ttu-id="602c5-532">키워드 `ref` 뒤에 *variable_reference* ([변수 참조](variables.md#variable-references))를 나타내는 인수는 참조 매개 변수로 전달 되는 ([참조 매개 변수 ](classes.md#reference-parameters)).</span><span class="sxs-lookup"><span data-stu-id="602c5-532">The keyword `ref` followed by a *variable_reference* ([Variable references](variables.md#variable-references)), indicating that the argument is passed as a reference parameter ([Reference parameters](classes.md#reference-parameters)).</span></span> <span data-ttu-id="602c5-533">변수 할당 되어야 합니다 ([한정 된 할당](variables.md#definite-assignment)) 전에 참조 매개 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-533">A variable must be definitely assigned ([Definite assignment](variables.md#definite-assignment)) before it can be passed as a reference parameter.</span></span> <span data-ttu-id="602c5-534">키워드 `out` 뒤에 *variable_reference* ([변수 참조](variables.md#variable-references))를 나타내는 인수는 출력 매개 변수로 전달 되는 ([매개변수를출력합니다.](classes.md#output-parameters)).</span><span class="sxs-lookup"><span data-stu-id="602c5-534">The keyword `out` followed by a *variable_reference* ([Variable references](variables.md#variable-references)), indicating that the argument is passed as an output parameter ([Output parameters](classes.md#output-parameters)).</span></span> <span data-ttu-id="602c5-535">변수를 정적으로 할당 된 것으로 간주 됩니다 ([한정 된 할당](variables.md#definite-assignment)) output 매개 변수로 전달 되는 변수는 함수 멤버 호출을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-535">A variable is considered definitely assigned ([Definite assignment](variables.md#definite-assignment)) following a function member invocation in which the variable is passed as an output parameter.</span></span>

#### <a name="corresponding-parameters"></a><span data-ttu-id="602c5-536">해당 매개 변수</span><span class="sxs-lookup"><span data-stu-id="602c5-536">Corresponding parameters</span></span>

<span data-ttu-id="602c5-537">인수 목록의 각 인수에 대 한 더 함수 멤버 또는 호출 되는 대리자를 해당 매개 변수 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-537">For each argument in an argument list there has to be a corresponding parameter in the function member or delegate being invoked.</span></span>

<span data-ttu-id="602c5-538">매개 변수 목록 다음에 사용 되는 다음과 같이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-538">The parameter list used in the following is determined as follows:</span></span>

*  <span data-ttu-id="602c5-539">가상 메서드 및 클래스에 정의 된 인덱서의 경우 매개 변수 목록 가장 구체적인 선언에서 선택 하거나 수신기의 정적 형식을 사용 하 여 시작 하 고 해당 기본 클래스를 통해 검색 함수 멤버를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-539">For virtual methods and indexers defined in classes, the parameter list is picked from the most specific declaration or override of the function member, starting with the static type of the receiver, and searching through its base classes.</span></span>
*  <span data-ttu-id="602c5-540">인터페이스 메서드 및 인덱서의 경우 매개 변수 목록 선택은 가장 구체적인 인터페이스 형식을 사용 하 여 시작 하 고 기본 인터페이스를 통해 검색 된 멤버의 정의 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-540">For interface methods and indexers, the parameter list is picked form the most specific definition of the member, starting with the interface type and searching through the base interfaces.</span></span> <span data-ttu-id="602c5-541">고유한 매개 변수 목록이 없는 발견 되 면 호출 명명 된 매개 변수를 사용 하거나 선택적 인수를 생략할 수 없습니다 있도록 액세스할 수 없는 이름 및 선택적 매개 변수 없이 사용 하 여 매개 변수 목록이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-541">If no unique parameter list is found, a parameter list with inaccessible names and no optional parameters is constructed, so that invocations cannot use named parameters or omit optional arguments.</span></span>
*  <span data-ttu-id="602c5-542">부분 메서드를 정의 하는 partial 메서드 선언 매개 변수 목록을 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-542">For partial methods, the parameter list of the defining partial method declaration is used.</span></span>
*  <span data-ttu-id="602c5-543">모든 기타 함수 멤버 및 대리자에 사용 되는 단일 매개 변수 목록만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-543">For all other function members and delegates there is only a single parameter list, which is the one used.</span></span>

<span data-ttu-id="602c5-544">매개 변수 또는 인수의 위치 인수 또는 인수 목록 또는 매개 변수 목록에서 앞에 매개 변수 수가 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-544">The position of an argument or parameter is defined as the number of arguments or parameters preceding it in the argument list or parameter list.</span></span>

<span data-ttu-id="602c5-545">함수 멤버 인수에 대 한 해당 매개 변수를 다음과 같이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-545">The corresponding parameters for function member arguments are established as follows:</span></span>

*  <span data-ttu-id="602c5-546">인수에는 *argument_list* 인스턴스 생성자, 메서드, 인덱서 및 대리자.</span><span class="sxs-lookup"><span data-stu-id="602c5-546">Arguments in the *argument_list* of instance constructors, methods, indexers and delegates:</span></span>
    * <span data-ttu-id="602c5-547">고정된 매개 변수가 매개 변수 목록의 동일한 위치에서 발생 하는 위치 인수는 해당 매개 변수에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-547">A positional argument where a fixed parameter occurs at the same position in the parameter list corresponds to that parameter.</span></span>
    * <span data-ttu-id="602c5-548">일반적인 형태로 호출 하는 매개 변수 배열 사용 하 여 함수 멤버의 위치 인수 매개 변수 목록의 동일한 위치에서 발생 해야 하는 매개 변수 배열에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-548">A positional argument of a function member with a parameter array invoked in its normal form corresponds to the parameter  array, which must occur at the same position in the parameter list.</span></span>
    * <span data-ttu-id="602c5-549">매개 변수가 없는 고정된이 발생 한 위치 매개 변수 목록의 동일한 위치에 있는 확장 된 형태로 호출 매개 변수 배열로 함수 멤버의 위치 인수 매개 변수 배열의 요소에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-549">A positional argument of a function member with a parameter array invoked in its expanded form, where no fixed parameter occurs at the same position in the parameter list, corresponds to an element in the parameter array.</span></span>
    * <span data-ttu-id="602c5-550">명명된 된 인수 매개 변수 목록에 같은 이름의 매개 변수에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-550">A named argument corresponds to the parameter of the same name in the parameter list.</span></span>
    * <span data-ttu-id="602c5-551">인덱서를 호출할 때 합니다 `set` 접근자, 대입 연산자의 오른쪽 피연산자에 암시적으로 지정 된 식을 `value` 의 매개 변수는 `set` 접근자 선언의 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-551">For indexers, when invoking the `set` accessor, the expression specified as the right operand of the assignment operator corresponds to the implicit `value` parameter of the `set` accessor declaration.</span></span>
*  <span data-ttu-id="602c5-552">속성을 호출 하는 경우에 `get` 있습니다 접근자에 인수가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-552">For properties, when invoking the `get` accessor there are no arguments.</span></span> <span data-ttu-id="602c5-553">호출할 때 합니다 `set` 접근자, 대입 연산자의 오른쪽 피연산자에 암시적으로 지정 된 식을 `value` 의 매개 변수는 `set` 접근자 선언의 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-553">When invoking the `set` accessor, the expression specified as the right operand of the assignment operator corresponds to the implicit `value` parameter of the `set` accessor declaration.</span></span>
*  <span data-ttu-id="602c5-554">사용자 정의 단항 연산자 (변환 포함)에 대 한 단일 피연산자 연산자 선언의 단일 매개 변수에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-554">For user-defined unary operators (including conversions), the single operand corresponds to the single parameter of the operator declaration.</span></span>
*  <span data-ttu-id="602c5-555">사용자 정의 이항 연산자의 첫 번째 매개 변수에 해당 하는 왼쪽된 피연산자 및 연산자 선언의 두 번째 매개 변수에 해당 하는 오른쪽 피연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-555">For user-defined binary operators, the left operand corresponds to the first parameter, and the right operand corresponds to the second parameter of the operator declaration.</span></span>

#### <a name="run-time-evaluation-of-argument-lists"></a><span data-ttu-id="602c5-556">인수 목록의 런타임에 평가</span><span class="sxs-lookup"><span data-stu-id="602c5-556">Run-time evaluation of argument lists</span></span>

<span data-ttu-id="602c5-557">멤버 함수 호출의 런타임 처리를 사용 하는 동안 ([컴파일 타임 동적 오버 로드 확인 검사](expressions.md#compile-time-checking-of-dynamic-overload-resolution)), 식 또는 변수 참조 인수 목록의 왼쪽에서 오른쪽 순서로 평가 됩니다 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-557">During the run-time processing of a function member invocation ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)), the expressions or variable references of an argument list are evaluated in order, from left to right, as follows:</span></span>

*  <span data-ttu-id="602c5-558">인수 식이 계산 되는 값 매개 변수에 대 한 암시적으로 변환 하 고 ([암시적 변환을](conversions.md#implicit-conversions)) 해당 매개 변수에 형식 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-558">For a value parameter, the argument expression is evaluated and an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) to the corresponding parameter type is performed.</span></span> <span data-ttu-id="602c5-559">결과 값을 멤버 함수 호출에 값 매개 변수의 초기 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-559">The resulting value becomes the initial value of the value parameter in the function member invocation.</span></span>
*  <span data-ttu-id="602c5-560">참조 또는 출력 매개 변수의 경우 변수 참조는 평가 하 고 결과 저장소 위치는 멤버 함수 호출에서 매개 변수가 나타내는 저장소 위치가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-560">For a reference or output parameter, the variable reference is evaluated and the resulting storage location becomes the storage location represented by the parameter in the function member invocation.</span></span> <span data-ttu-id="602c5-561">참조 또는 출력 매개 변수로 지정 된 변수 참조의 배열 요소 이면을 *reference_type*, 런타임 검사를 수행 하 여 배열의 요소 형식 매개 변수의 유형과 동일 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-561">If the variable reference given as a reference or output parameter is an array element of a *reference_type*, a run-time check is performed to ensure that the element type of the array is identical to the type of the parameter.</span></span> <span data-ttu-id="602c5-562">이 검사가 실패 하는 경우는 `System.ArrayTypeMismatchException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-562">If this check fails, a `System.ArrayTypeMismatchException` is thrown.</span></span>

<span data-ttu-id="602c5-563">메서드, 인덱서 및 인스턴스 생성자는 매개 변수 배열에 맨 오른쪽 매개 변수를 선언할 수 있습니다 ([매개 변수 배열](classes.md#parameter-arrays)).</span><span class="sxs-lookup"><span data-stu-id="602c5-563">Methods, indexers, and instance constructors may declare their right-most parameter to be a parameter array ([Parameter arrays](classes.md#parameter-arrays)).</span></span> <span data-ttu-id="602c5-564">이러한 함수 멤버에 적용 되는에 따라 해당 확장된 형식 또는 해당 기본 폼의 호출 됩니다 ([적용 가능한 함수 멤버](expressions.md#applicable-function-member)):</span><span class="sxs-lookup"><span data-stu-id="602c5-564">Such function members are invoked either in their normal form or in their expanded form depending on which is applicable ([Applicable function member](expressions.md#applicable-function-member)):</span></span>

*  <span data-ttu-id="602c5-565">매개 변수 배열에 대 한 지정 된 인수 암시적으로 변환할 수 있는 단일 식 이어야 합니다 일반적인 형태로 함수 멤버는 매개 변수 배열 사용 하 여 호출 되 면 ([암시적 변환을](conversions.md#implicit-conversions)) 매개 변수 배열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-565">When a function member with a parameter array is invoked in its normal form, the argument given for the parameter array must be a single expression that is implicitly convertible ([Implicit conversions](conversions.md#implicit-conversions)) to the parameter array type.</span></span> <span data-ttu-id="602c5-566">이 경우 매개 변수 배열의 값 매개 변수 처럼 정확 하 게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-566">In this case, the parameter array acts precisely like a value parameter.</span></span>
*  <span data-ttu-id="602c5-567">확장 된 형태로 매개 변수 배열로 함수 멤버를 호출 하면 호출 각 인수는 암시적으로 변환할 수 있는 식을 매개 변수 배열에 대해 0 개 이상의 위치 인수를 지정 해야 합니다 ([암시적 변환](conversions.md#implicit-conversions)) 매개 변수 배열의 요소 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-567">When a function member with a parameter array is invoked in its expanded form, the invocation must specify zero or more positional arguments for the parameter array, where each argument is an expression that is implicitly convertible ([Implicit conversions](conversions.md#implicit-conversions)) to the element type of the parameter array.</span></span> <span data-ttu-id="602c5-568">호출을 인수의 번호에 해당 하는 길이 사용 하 여 매개 변수 배열 형식의 인스턴스를 만듭니다, 그리고 요소의 지정 된 인수 값을 사용 하 여 배열 인스턴스를 초기화 및 새로 만든된 배열 인스턴스는 실제 사용 하 여이 예제의 경우 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-568">In this case, the invocation creates an instance of the parameter array type with a length corresponding to the number of arguments, initializes the elements of the array instance with the given argument values, and uses the newly created array instance as the actual argument.</span></span>

<span data-ttu-id="602c5-569">인수 목록의 식은 항상 기록 될 때 해당 순서로 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-569">The expressions of an argument list are always evaluated in the order they are written.</span></span> <span data-ttu-id="602c5-570">따라서 예제</span><span class="sxs-lookup"><span data-stu-id="602c5-570">Thus, the example</span></span>
```csharp
class Test
{
    static void F(int x, int y = -1, int z = -2) {
        System.Console.WriteLine("x = {0}, y = {1}, z = {2}", x, y, z);
    }

    static void Main() {
        int i = 0;
        F(i++, i++, i++);
        F(z: i++, x: i++);
    }
}
```
<span data-ttu-id="602c5-571">는 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-571">produces the output</span></span>
```
x = 0, y = 1, z = 2
x = 4, y = -1, z = 3
```

<span data-ttu-id="602c5-572">배열 공동 분산 규칙 ([배열 공변성 (covariance)](arrays.md#array-covariance)) 배열 형식의 값을 허용 `A[]` 배열 형식의 인스턴스에 대 한 참조가 되도록 `B[]`암시적 참조 변환이 존재에서 제공 하는, `B` 를 `A`.</span><span class="sxs-lookup"><span data-stu-id="602c5-572">The array co-variance rules ([Array covariance](arrays.md#array-covariance)) permit a value of an array type `A[]` to be a reference to an instance of an array type `B[]`, provided an implicit reference conversion exists from `B` to `A`.</span></span> <span data-ttu-id="602c5-573">이러한 규칙의 경우 배열 요소의 때문를 *reference_type* 전달 되는 런타임 검사 되는 실제 요소 배열의 형식은 동일한 매개 변수를 확인 하는 데 필요한 참조 또는 출력 매개 변수로 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-573">Because of these rules, when an array element of a *reference_type* is passed as a reference or output parameter, a run-time check is required to ensure that the actual element type of the array is identical to that of the parameter.</span></span> <span data-ttu-id="602c5-574">예제</span><span class="sxs-lookup"><span data-stu-id="602c5-574">In the example</span></span>
```csharp
class Test
{
    static void F(ref object x) {...}

    static void Main() {
        object[] a = new object[10];
        object[] b = new string[10];
        F(ref a[0]);        // Ok
        F(ref b[1]);        // ArrayTypeMismatchException
    }
}
```
<span data-ttu-id="602c5-575">두 번째로 호출 하면 `F` 발생을 `System.ArrayTypeMismatchException` 의 실제 요소 형식 때문 `b` 는 `string` 아니라 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-575">the second invocation of `F` causes a `System.ArrayTypeMismatchException` to be thrown because the actual element type of `b` is `string` and not `object`.</span></span>

<span data-ttu-id="602c5-576">확장 된 형태로 매개 변수 배열로 함수 멤버를 호출 하면 호출 됩니다 것 처럼 처리 배열 만들기 식을 배열 이니셜라이저로 ([배열 만들기 식](expressions.md#array-creation-expressions)) 주위에 삽입 된는 확장 된 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-576">When a function member with a parameter array is invoked in its expanded form, the invocation is processed exactly as if an array creation expression with an array initializer ([Array creation expressions](expressions.md#array-creation-expressions)) was inserted around the expanded parameters.</span></span> <span data-ttu-id="602c5-577">예를 들어 선언 된 경우</span><span class="sxs-lookup"><span data-stu-id="602c5-577">For example, given the declaration</span></span>
```csharp
void F(int x, int y, params object[] args);
```
<span data-ttu-id="602c5-578">다음 호출의 확장 된 형태의 메서드</span><span class="sxs-lookup"><span data-stu-id="602c5-578">the following invocations of the expanded form of the method</span></span>
```csharp
F(10, 20);
F(10, 20, 30, 40);
F(10, 20, 1, "hello", 3.0);
```
<span data-ttu-id="602c5-579">정확히 일치</span><span class="sxs-lookup"><span data-stu-id="602c5-579">correspond exactly to</span></span>
```csharp
F(10, 20, new object[] {});
F(10, 20, new object[] {30, 40});
F(10, 20, new object[] {1, "hello", 3.0});
```

<span data-ttu-id="602c5-580">특히, 매개 변수 배열에 대 한 인수가 있으면 빈 배열을 만들어졌는지 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-580">In particular, note that an empty array is created when there are zero arguments given for the parameter array.</span></span>

<span data-ttu-id="602c5-581">해당 선택적 매개 변수를 사용 하 여 멤버 함수에서에서 인수를 생략 하면 함수 멤버 선언의 기본 인수를 암시적으로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-581">When arguments are omitted from a function member with corresponding optional parameters, the default arguments of the function member declaration are implicitly passed.</span></span> <span data-ttu-id="602c5-582">이기 때문에 항상 상수 평가 나머지 인수의 평가 순서 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-582">Because these are always constant, their evaluation will not impact the evaluation order of the remaining arguments.</span></span>

### <a name="type-inference"></a><span data-ttu-id="602c5-583">형식 유추</span><span class="sxs-lookup"><span data-stu-id="602c5-583">Type inference</span></span>

<span data-ttu-id="602c5-584">형식 인수를 지정 하지 않고 제네릭 메서드를 호출 하는 경우는 ***형식 유추*** 프로세스 호출에 대 한 형식 인수를 유추 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-584">When a generic method is called without specifying type arguments, a ***type inference*** process attempts to infer type arguments for the call.</span></span> <span data-ttu-id="602c5-585">형식 유추의 존재는 제네릭 메서드 호출에 사용 되는 더 편리한 구문을 허용 하 고 중복 형식 정보를 지정 하지 않으려면 프로그래머를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-585">The presence of type inference allows a more convenient syntax to be used for calling a generic method, and allows the programmer to avoid specifying redundant type information.</span></span> <span data-ttu-id="602c5-586">예를 들어 다음과 같습니다. 메서드 선언</span><span class="sxs-lookup"><span data-stu-id="602c5-586">For example, given the method declaration:</span></span>
```csharp
class Chooser
{
    static Random rand = new Random();

    public static T Choose<T>(T first, T second) {
        return (rand.Next(2) == 0)? first: second;
    }
}
```
<span data-ttu-id="602c5-587">호출 하는 것이 불가능 합니다 `Choose` 형식 인수를 명시적으로 지정 하지 않고 메서드:</span><span class="sxs-lookup"><span data-stu-id="602c5-587">it is possible to invoke the `Choose` method without explicitly specifying a type argument:</span></span>
```csharp
int i = Chooser.Choose(5, 213);                 // Calls Choose<int>

string s = Chooser.Choose("foo", "bar");        // Calls Choose<string>
```

<span data-ttu-id="602c5-588">형식 인수를 형식 유추를 통해서도 `int` 고 `string` 메서드에 인수에서 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-588">Through type inference, the type arguments `int` and `string` are determined from the arguments to the method.</span></span>

<span data-ttu-id="602c5-589">형식 유추 메서드 호출을 처리 하는 바인딩 시간 부분으로 이루어집니다 ([메서드 호출](expressions.md#method-invocations)) 및 이전 호출의 오버 로드 확인 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-589">Type inference occurs as part of the binding-time processing of a method invocation ([Method invocations](expressions.md#method-invocations)) and takes place before the overload resolution step of the invocation.</span></span> <span data-ttu-id="602c5-590">특정 메서드 그룹은 메서드 호출에 지정 된 메서드 호출의 일부로 지정 된 형식 인수가 없는 경우 형식 유추는 메서드 그룹에 각 제네릭 메서드에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-590">When a particular method group is specified in a method invocation, and no type arguments are specified as part of the method invocation, type inference is applied to each generic method in the method group.</span></span> <span data-ttu-id="602c5-591">형식 유추에 성공 하면 후속 오버 로드 확인에 대 한 인수의 유형을 확인 하는 유추 된 형식 인수가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-591">If type inference succeeds, then the inferred type arguments are used to determine the types of arguments for subsequent overload resolution.</span></span> <span data-ttu-id="602c5-592">오버 로드 확인 제네릭 메서드를 호출 하는 것을 선택 하는 경우 유추 된 형식 인수는 호출에 대 한 실제 형식 인수로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-592">If overload resolution chooses a generic method as the one to invoke, then the inferred type arguments are used as the actual type arguments for the invocation.</span></span> <span data-ttu-id="602c5-593">특정 메서드에 대 한 형식 유추에 실패 하면 해당 메서드 오버 로드 확인에 참여 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-593">If type inference for a particular method fails, that method does not participate in overload resolution.</span></span> <span data-ttu-id="602c5-594">형식 유추를 자체, 오류의 바인딩 시간 오류를 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-594">The failure of type inference, in and of itself, does not cause a binding-time error.</span></span> <span data-ttu-id="602c5-595">그러나 종종 바인딩 시간 오류를 하지 못하면 오버 로드 확인 한 다음 해당 메서드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-595">However, it often leads to a binding-time error when overload resolution then fails to find any applicable methods.</span></span>

<span data-ttu-id="602c5-596">제공 된 인수 개수는 메서드의 매개 변수 수가 다른 경우 유추 즉시 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-596">If the supplied number of arguments is different than the number of parameters in the method, then inference immediately fails.</span></span> <span data-ttu-id="602c5-597">그렇지 않으면 제네릭 메서드 시그니처가 다음 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-597">Otherwise, assume that the generic method has the following signature:</span></span>
```csharp
Tr M<X1,...,Xn>(T1 x1, ..., Tm xm)
```

<span data-ttu-id="602c5-598">형식의 메서드 호출으로 `M(E1...Em)` 형식 유추는 작업은 고유한 형식 인수를 찾으려면 `S1...Sn` 각 형식 매개 변수에 대해 `X1...Xn` 있도록 호출 `M<S1...Sn>(E1...Em)` 유효 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-598">With a method call of the form `M(E1...Em)` the task of type inference is to find unique type arguments `S1...Sn` for each of the type parameters `X1...Xn` so that the call `M<S1...Sn>(E1...Em)` becomes valid.</span></span>

<span data-ttu-id="602c5-599">각 형식 매개 변수는 유추 과정 `Xi` 중 하나는 *고정* 특정 형식에 `Si` 또는 *고정 되지 않은* 연결된 집합이 있는 *범위*.</span><span class="sxs-lookup"><span data-stu-id="602c5-599">During the process of inference each type parameter `Xi` is either *fixed* to a particular type `Si` or *unfixed* with an associated set of *bounds*.</span></span> <span data-ttu-id="602c5-600">각 경계는 일부 형식 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-600">Each of the bounds is some type `T`.</span></span> <span data-ttu-id="602c5-601">각 형식 변수에 처음 `Xi` 경계 빈 집합을 사용 하 여 고정 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-601">Initially each type variable `Xi` is unfixed with an empty set of bounds.</span></span>

<span data-ttu-id="602c5-602">형식 유추 단계로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-602">Type inference takes place in phases.</span></span> <span data-ttu-id="602c5-603">각 단계는 이전 단계의 결과에 따라 자세한 형식 변수에 대 한 형식 인수를 유추 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-603">Each phase will try to infer type arguments for more type variables based on the findings of the previous phase.</span></span> <span data-ttu-id="602c5-604">첫 번째 단계는 두 번째 단계는 특정 형식에 형식 변수를 수정 하 고 범위를 유추 하는 반면 일부 초기 추론을 경계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-604">The first phase makes some initial inferences of bounds, whereas the second phase fixes type variables to specific types and infers further bounds.</span></span> <span data-ttu-id="602c5-605">두 번째 단계는 해야 할 수 있습니다 횟수 만큼 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-605">The second phase may have to be repeated a number of times.</span></span>

<span data-ttu-id="602c5-606">*참고:* 제네릭 메서드를 호출 하는 경우에 뿐만 아니라 수행 하는 형식 유추 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-606">*Note:* Type inference takes place not only when a generic method is called.</span></span> <span data-ttu-id="602c5-607">에 설명 된 메서드 그룹 변환에 대 한 형식 유추 [메서드 그룹 변환에 대 한 형식 유추](expressions.md#type-inference-for-conversion-of-method-groups) 에 설명 된 식 집합의 가장 일반적인 형식이 찾기 및 [집합의 가장 일반적인 형식 찾기 식의](expressions.md#finding-the-best-common-type-of-a-set-of-expressions)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-607">Type inference for conversion of method groups is described in [Type inference for conversion of method groups](expressions.md#type-inference-for-conversion-of-method-groups) and finding the best common type of a set of expressions is described in [Finding the best common type of a set of expressions](expressions.md#finding-the-best-common-type-of-a-set-of-expressions).</span></span>

#### <a name="the-first-phase"></a><span data-ttu-id="602c5-608">첫 번째 단계</span><span class="sxs-lookup"><span data-stu-id="602c5-608">The first phase</span></span>

<span data-ttu-id="602c5-609">각 메서드 인수에 대 한 `Ei`:</span><span class="sxs-lookup"><span data-stu-id="602c5-609">For each of the method arguments `Ei`:</span></span>

*   <span data-ttu-id="602c5-610">하는 경우 `Ei` 는 익명 함수는 *명시적 매개 변수 형식 유추* ([명시적 매개 변수 형식 추론](expressions.md#explicit-parameter-type-inferences))에서 만들어진 `Ei` 를 `Ti`</span><span class="sxs-lookup"><span data-stu-id="602c5-610">If `Ei` is an anonymous function, an *explicit parameter type inference* ([Explicit parameter type inferences](expressions.md#explicit-parameter-type-inferences)) is made from `Ei` to `Ti`</span></span>
*   <span data-ttu-id="602c5-611">그렇지 않은 경우, `Ei` 형식이 `U` 하 고 `xi` 값 매개 변수는 *유추가* 이루어집니다 *에서* `U` *를* `Ti`.</span><span class="sxs-lookup"><span data-stu-id="602c5-611">Otherwise, if `Ei` has a type `U` and `xi` is a value parameter then a *lower-bound inference* is made *from* `U` *to* `Ti`.</span></span>
*   <span data-ttu-id="602c5-612">그렇지 않은 경우, `Ei` 형식이 `U` 하 고 `xi` 은 `ref` 또는 `out` 매개 변수는 *유추 정확한* 이루어집니다 *에서* `U` *하* `Ti`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-612">Otherwise, if `Ei` has a type `U` and `xi` is a `ref` or `out` parameter then an *exact inference* is made *from* `U` *to* `Ti`.</span></span>
*   <span data-ttu-id="602c5-613">그렇지 않은 경우이 인수에 대 한 유추가 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-613">Otherwise, no inference is made for this argument.</span></span>


#### <a name="the-second-phase"></a><span data-ttu-id="602c5-614">두 번째 단계</span><span class="sxs-lookup"><span data-stu-id="602c5-614">The second phase</span></span>

<span data-ttu-id="602c5-615">두 번째 단계는 다음과 같이 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-615">The second phase proceeds as follows:</span></span>

*   <span data-ttu-id="602c5-616">모든 *고정 되지 않은* 변수를 입력 `Xi` 하지 않는 *종속* ([종속성](expressions.md#dependence)) 모든 `Xj` 수정 ([수정](expressions.md#fixing)).</span><span class="sxs-lookup"><span data-stu-id="602c5-616">All *unfixed* type variables `Xi` which do not *depend on* ([Dependence](expressions.md#dependence)) any `Xj` are fixed ([Fixing](expressions.md#fixing)).</span></span>
*   <span data-ttu-id="602c5-617">모든 없는 이러한 형식 변수가 존재 하는 경우 *고정 되지 않은* 변수를 입력 `Xi` 됩니다 *고정* 저장한 다음이 모두는:</span><span class="sxs-lookup"><span data-stu-id="602c5-617">If no such type variables exist, all *unfixed* type variables `Xi` are *fixed* for which all of the following hold:</span></span>
    *   <span data-ttu-id="602c5-618">하나 이상의 형식 변수가 `Xj` 에 종속 된 `Xi`</span><span class="sxs-lookup"><span data-stu-id="602c5-618">There is at least one type variable `Xj` that depends on `Xi`</span></span>
    *   <span data-ttu-id="602c5-619">`Xi` 집합이 아닌-빈 범위</span><span class="sxs-lookup"><span data-stu-id="602c5-619">`Xi` has a non-empty set of bounds</span></span>
*   <span data-ttu-id="602c5-620">이러한 없는 형식 변수가 존재 하 고 여전히 *고정 되지 않은* 변수 형식 유추 실패를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-620">If no such type variables exist and there are still *unfixed* type variables, type inference fails.</span></span>
*   <span data-ttu-id="602c5-621">그렇지 않으면 더 이상 *고정 되지 않은* 형식 변수, 형식 유추 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-621">Otherwise, if no further *unfixed* type variables exist, type inference succeeds.</span></span>
*   <span data-ttu-id="602c5-622">모든 인수에 대 한이 고, 그렇지 `Ei` 해당 매개 변수 형식과 `Ti` 여기서 합니다 *출력 형식* ([출력 형식](expressions.md#output-types))를 포함 *고정 되지 않은* 변수를 입력 `Xj` 되지만 *입력 형식을* ([입력 형식을](expressions.md#input-types)) 하지는 *출력 형식 유추* ([출력 형식 추론 ](expressions.md#output-type-inferences)) 이루어집니다 *에서* `Ei` *하* `Ti`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-622">Otherwise, for all arguments `Ei` with corresponding parameter type `Ti` where the *output types* ([Output types](expressions.md#output-types)) contain *unfixed* type variables `Xj` but the *input types* ([Input types](expressions.md#input-types)) do not, an *output type inference* ([Output type inferences](expressions.md#output-type-inferences)) is made *from* `Ei` *to* `Ti`.</span></span> <span data-ttu-id="602c5-623">다음 두 번째 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-623">Then the second phase is repeated.</span></span>

#### <a name="input-types"></a><span data-ttu-id="602c5-624">입력된 형식</span><span class="sxs-lookup"><span data-stu-id="602c5-624">Input types</span></span>

<span data-ttu-id="602c5-625">경우 `E` 는 메서드 그룹 또는 익명 함수를 암시적으로 형식화 및 `T` 인 대리자 형식 또는 식 트리 형식의 모든 매개 변수 형식은 `T` 됩니다 *입력 형식을* 의 `E` *형식과* `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-625">If `E` is a method group or implicitly typed anonymous function and `T` is a delegate type or expression tree type then all the parameter types of `T` are *input types* of `E` *with type* `T`.</span></span>

####  <a name="output-types"></a><span data-ttu-id="602c5-626">출력 형식</span><span class="sxs-lookup"><span data-stu-id="602c5-626">Output types</span></span>

<span data-ttu-id="602c5-627">경우 `E` 메서드 그룹 또는 익명 함수 및 `T` 인 대리자 형식 또는 식 트리 형식의 반환 형식을 `T` 가 *유형의 출력* `E` *형식을 사용 하 여*  `T`.</span><span class="sxs-lookup"><span data-stu-id="602c5-627">If `E` is a method group or an anonymous function and `T` is a delegate type or expression tree type then the return type of `T` is an *output type of* `E` *with type* `T`.</span></span>

#### <a name="dependence"></a><span data-ttu-id="602c5-628">종속성</span><span class="sxs-lookup"><span data-stu-id="602c5-628">Dependence</span></span>

<span data-ttu-id="602c5-629">*고정 되지 않은* 유형 변수에 `Xi` *에 직접 종속* 고정 되지 않은 형식 변수를 `Xj` 경우에 일부 인수에 대 한 `Ek` 형식과 `Tk` `Xj` 발생을 *입력 유형* 의 `Ek` 형식과 `Tk` 및 `Xi` 에서 발생는 *출력 형식* 의 `Ek` 형식을 사용 하 여 `Tk`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-629">An *unfixed* type variable `Xi` *depends directly on* an unfixed type variable `Xj` if for some argument `Ek` with type `Tk` `Xj` occurs in an *input type* of `Ek` with type `Tk` and `Xi` occurs in an *output type* of `Ek` with type `Tk`.</span></span>

<span data-ttu-id="602c5-630">`Xj` *에 따라 달라 집니다* `Xi` 하는 경우 `Xj` *에 직접 종속* `Xi` 이거나 `Xi` *에 직접 종속* `Xk` 고 `Xk` *에 따라 달라 집니다* `Xj`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-630">`Xj` *depends on* `Xi` if `Xj` *depends directly on* `Xi` or if `Xi` *depends directly on* `Xk` and `Xk` *depends on* `Xj`.</span></span> <span data-ttu-id="602c5-631">따라서 "에 종속"는 "에 직접 종속" 전이적 하지만 하지 반사 종결 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-631">Thus "depends on" is the transitive but not reflexive closure of "depends directly on".</span></span>

#### <a name="output-type-inferences"></a><span data-ttu-id="602c5-632">출력 형식 추론</span><span class="sxs-lookup"><span data-stu-id="602c5-632">Output type inferences</span></span>

<span data-ttu-id="602c5-633">*출력 형식 유추* 이루어집니다 *에서* 식을 `E` *하* 형식 `T` 다음과 같은 방식:</span><span class="sxs-lookup"><span data-stu-id="602c5-633">An *output type inference* is made *from* an expression `E` *to* a type `T` in the following way:</span></span>

*  <span data-ttu-id="602c5-634">하는 경우 `E` 유추 된 반환 형식이 익명 함수로 `U` ([유추 반환 형식](expressions.md#inferred-return-type)) 및 `T` 대리자 형식 또는 반환 형식 가진 식 트리 형식 `Tb`, 다음을 *유추가* ([하한값 추론](expressions.md#lower-bound-inferences)) 이루어집니다 *에서* `U` *하* `Tb`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-634">If `E` is an anonymous function with inferred return type  `U` ([Inferred return type](expressions.md#inferred-return-type)) and `T` is a delegate type or expression tree type with return type `Tb`, then a *lower-bound inference* ([Lower-bound inferences](expressions.md#lower-bound-inferences)) is made *from* `U` *to* `Tb`.</span></span>
*  <span data-ttu-id="602c5-635">그렇지 않은 경우, `E` 는 메서드 그룹 및 `T` 대리자 형식 또는 매개 변수 형식 가진 식 트리 형식 `T1...Tk` 및 반환 형식을 `Tb`의 오버 로드 확인 하 고 `E` 형식을 사용 하 여 `T1...Tk` 생성을 메서드 반환 형식 사용 하 여 단일 `U`에 *유추가* 이루어집니다 *에서* `U` *에* `Tb`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-635">Otherwise, if `E` is a method group and `T` is a delegate type or expression tree type with parameter types `T1...Tk` and return type `Tb`, and overload resolution of `E` with the types `T1...Tk` yields a single method with return type `U`, then a *lower-bound inference* is made *from* `U` *to* `Tb`.</span></span>
*  <span data-ttu-id="602c5-636">그렇지 `E` 형식 사용 하 여 식 `U`에 *유추가* 이루어집니다 *에서* `U` *를* `T`.</span><span class="sxs-lookup"><span data-stu-id="602c5-636">Otherwise, if `E` is an expression with type `U`, then a *lower-bound inference* is made *from* `U` *to* `T`.</span></span>
*  <span data-ttu-id="602c5-637">그렇지 않으면 없습니다 추론이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-637">Otherwise, no inferences are made.</span></span>

#### <a name="explicit-parameter-type-inferences"></a><span data-ttu-id="602c5-638">명시적 매개 변수 형식 추론</span><span class="sxs-lookup"><span data-stu-id="602c5-638">Explicit parameter type inferences</span></span>

<span data-ttu-id="602c5-639">*명시적 매개 변수 형식 유추* 이루어집니다 *에서* 식을 `E` *하* 형식 `T` 다음과 같은 방법으로:</span><span class="sxs-lookup"><span data-stu-id="602c5-639">An *explicit parameter type inference* is made *from* an expression `E` *to* a type `T` in the following way:</span></span>

*  <span data-ttu-id="602c5-640">경우 `E` 매개 변수 형식이 명시적으로 형식화 된 익명 함수로 `U1...Uk` 하 고 `T` 대리자 형식 또는 매개 변수 형식 가진 식 트리 형식 `V1...Vk` 각각에 대 한 다음 `Ui` 는 *정확한 유추* ([추론 정확한](expressions.md#exact-inferences)) 이루어집니다 *에서* `Ui` *하* 해당 `Vi`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-640">If `E` is an explicitly typed anonymous function with parameter types `U1...Uk` and `T` is a delegate type or expression tree type with parameter types `V1...Vk` then for each `Ui` an *exact inference* ([Exact inferences](expressions.md#exact-inferences)) is made *from* `Ui` *to* the corresponding `Vi`.</span></span>

#### <a name="exact-inferences"></a><span data-ttu-id="602c5-641">정확한 추론</span><span class="sxs-lookup"><span data-stu-id="602c5-641">Exact inferences</span></span>

<span data-ttu-id="602c5-642">*유추 정확한* *에서* 형식 `U` *에* 형식 `V` 다음과 같이 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-642">An *exact inference* *from* a type `U` *to* a type `V` is made as follows:</span></span>

*  <span data-ttu-id="602c5-643">경우 `V` 중 하나인 합니다 *고정 되지 않은* `Xi` 한 다음 `U` 집합에 대 한 정확한 범위에 추가 됩니다 `Xi`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-643">If `V` is one of the *unfixed* `Xi` then `U` is added to the set of exact bounds for `Xi`.</span></span>

*  <span data-ttu-id="602c5-644">설정 하 고, 그렇지 `V1...Vk` 고 `U1...Uk` 다음 경우 중 하나라도 있는지 확인 하 여 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-644">Otherwise, sets `V1...Vk` and `U1...Uk` are determined by checking if any of the following cases apply:</span></span>

   *  <span data-ttu-id="602c5-645">`V` 배열 형식인 `V1[...]` 하 고 `U` 배열 형식인 `U1[...]` 같은 순위</span><span class="sxs-lookup"><span data-stu-id="602c5-645">`V` is an array type `V1[...]` and `U` is an array type `U1[...]`  of the same rank</span></span>
   *  <span data-ttu-id="602c5-646">`V` 형식인 `V1?` 고 `U` 형식인 `U1?`</span><span class="sxs-lookup"><span data-stu-id="602c5-646">`V` is the type `V1?` and `U` is the type `U1?`</span></span>
   *  <span data-ttu-id="602c5-647">`V` 생성 된 형식인 `C<V1...Vk>`고 `U` 생성 된 형식인 `C<U1...Uk>`</span><span class="sxs-lookup"><span data-stu-id="602c5-647">`V` is a constructed type `C<V1...Vk>`and `U` is a constructed type `C<U1...Uk>`</span></span>

   <span data-ttu-id="602c5-648">이러한 경우 다음에 적용 하는 경우는 *유추 정확한* 이루어집니다 *에서* 각 `Ui` *하* 해당 `Vi`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-648">If any of these cases apply then an *exact inference* is made *from* each `Ui` *to* the corresponding `Vi`.</span></span>

*  <span data-ttu-id="602c5-649">그렇지 않으면 없습니다 추론이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-649">Otherwise no inferences are made.</span></span>

#### <a name="lower-bound-inferences"></a><span data-ttu-id="602c5-650">하한값 추론</span><span class="sxs-lookup"><span data-stu-id="602c5-650">Lower-bound inferences</span></span>

<span data-ttu-id="602c5-651">A *유추가* *에서* 형식 `U` *를* 형식 `V` 다음과 같이 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-651">A *lower-bound inference* *from* a type `U` *to* a type `V` is made as follows:</span></span>

*  <span data-ttu-id="602c5-652">경우 `V` 중 하나인 합니다 *고정 되지 않은* `Xi` 한 다음 `U` 집합에 대 한 하한값을 추가할 `Xi`.</span><span class="sxs-lookup"><span data-stu-id="602c5-652">If `V` is one of the *unfixed* `Xi` then `U` is added to the set of lower bounds for `Xi`.</span></span>
*  <span data-ttu-id="602c5-653">그렇지 않은 경우, `V` 형식인 `V1?`하 고 `U` 형식인 `U1?` 하한값 유추에서 수행할 `U1` 에 `V1`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-653">Otherwise, if `V` is the type `V1?`and `U` is the type `U1?` then a lower bound inference is made from `U1` to `V1`.</span></span>
*  <span data-ttu-id="602c5-654">설정 하 고, 그렇지 `U1...Uk` 고 `V1...Vk` 다음 경우 중 하나라도 있는지 확인 하 여 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-654">Otherwise, sets `U1...Uk` and `V1...Vk` are determined by checking if any of the following cases apply:</span></span>
   *  <span data-ttu-id="602c5-655">`V` 배열 형식입니다 `V1[...]` 하 고 `U` 배열 형식인 `U1[...]` (유효한 기본 형식의 형식 매개 변수나 `U1[...]`) 같은 순위</span><span class="sxs-lookup"><span data-stu-id="602c5-655">`V` is an array type `V1[...]` and `U` is an array type `U1[...]` (or a type parameter whose effective base type is `U1[...]`) of the same rank</span></span>
   *  <span data-ttu-id="602c5-656">`V` 중 하나인 `IEnumerable<V1>`, `ICollection<V1>` 또는 `IList<V1>` 하 고 `U` 형식인 1 차원 배열 `U1[]`(유효한 기본 형식의 형식 매개 변수나 `U1[]`)</span><span class="sxs-lookup"><span data-stu-id="602c5-656">`V` is one of `IEnumerable<V1>`, `ICollection<V1>` or `IList<V1>` and `U` is a one-dimensional array type `U1[]`(or a type parameter whose effective base type is `U1[]`)</span></span>
   *  <span data-ttu-id="602c5-657">`V` 생성 된 클래스, 구조체, 인터페이스 또는 대리자 형식인 `C<V1...Vk>` 고유한 형식이 며 `C<U1...Uk>` 되도록 `U` (또는 `U` 형식 매개 변수, 유효한 기본 클래스 또는 효과적인 인터페이스 집합의 모든 멤버)는 과 동일 (직접 또는 간접적으로)에서 상속 되거나 (직접 또는 간접적으로) 구현 `C<U1...Uk>`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-657">`V` is a constructed class, struct, interface or delegate type `C<V1...Vk>` and there is a unique type `C<U1...Uk>` such that `U` (or, if `U` is a type parameter, its effective base class or any member of its effective interface set) is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) `C<U1...Uk>`.</span></span>

      <span data-ttu-id="602c5-658">("고유성" 제한 사례 인터페이스의 의미 `C<T> {} class U: C<X>, C<Y> {}`, 유추가에서 유추 하는 경우 수행할 `U` 에 `C<T>` 때문에 `U1` 일 수 있습니다 `X` 또는 `Y`.)</span><span class="sxs-lookup"><span data-stu-id="602c5-658">(The "uniqueness" restriction means that in the case interface `C<T> {} class U: C<X>, C<Y> {}`, then no inference is made when inferring from `U` to `C<T>` because `U1` could be `X` or `Y`.)</span></span>

   <span data-ttu-id="602c5-659">이러한 경우는 유추 수행할를 적용 하는 경우 *에서* 각 `Ui` *를* 해당 `Vi` 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-659">If any of these cases apply then an inference is made *from* each `Ui` *to* the corresponding `Vi` as follows:</span></span>

   *  <span data-ttu-id="602c5-660">하는 경우 `Ui` 참조 형식으로 알려지지 않은 됩니다 *유추 정확한* 됩니다</span><span class="sxs-lookup"><span data-stu-id="602c5-660">If `Ui` is not known to be a reference type then an *exact inference* is made</span></span>
   *  <span data-ttu-id="602c5-661">그렇지 않고 `U` 배열 형식인는 *유추가* 됩니다</span><span class="sxs-lookup"><span data-stu-id="602c5-661">Otherwise, if `U` is an array type then a *lower-bound inference* is made</span></span>
   *  <span data-ttu-id="602c5-662">그렇지 않고 `V` 됩니다 `C<V1...Vk>` 유추 i 번째 형식 매개 변수에 따라 다음 `C`:</span><span class="sxs-lookup"><span data-stu-id="602c5-662">Otherwise, if `V` is `C<V1...Vk>` then inference depends on the i-th type parameter of `C`:</span></span>
      *  <span data-ttu-id="602c5-663">공변 (covariant) 경우는 *유추가* 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-663">If it is covariant then a *lower-bound inference* is made.</span></span>
      *  <span data-ttu-id="602c5-664">반공 변 경우는 *상한을 유추* 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-664">If it is contravariant then an *upper-bound inference* is made.</span></span>
      *  <span data-ttu-id="602c5-665">Variant 없으면 됩니다 *유추 정확한* 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-665">If it is invariant then an *exact inference* is made.</span></span>
*  <span data-ttu-id="602c5-666">그렇지 않으면 없습니다 추론이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-666">Otherwise, no inferences are made.</span></span>

#### <a name="upper-bound-inferences"></a><span data-ttu-id="602c5-667">상한 추론</span><span class="sxs-lookup"><span data-stu-id="602c5-667">Upper-bound inferences</span></span>

<span data-ttu-id="602c5-668">*상한을 유추* *에서* 형식 `U` *에* 형식 `V` 다음과 같이 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-668">An *upper-bound inference* *from* a type `U` *to* a type `V` is made as follows:</span></span>

*  <span data-ttu-id="602c5-669">경우 `V` 중 하나인 합니다 *고정 되지 않은* `Xi` 한 다음 `U` 상한의 집합에 추가 됩니다 `Xi`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-669">If `V` is one of the *unfixed* `Xi` then `U` is added to the set of upper bounds for `Xi`.</span></span>
*  <span data-ttu-id="602c5-670">설정 하 고, 그렇지 `V1...Vk` 고 `U1...Uk` 다음 경우 중 하나라도 있는지 확인 하 여 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-670">Otherwise, sets `V1...Vk` and `U1...Uk` are determined by checking if any of the following cases apply:</span></span>
   *  <span data-ttu-id="602c5-671">`U` 배열 형식인 `U1[...]` 하 고 `V` 배열 형식인 `V1[...]` 같은 순위</span><span class="sxs-lookup"><span data-stu-id="602c5-671">`U` is an array type `U1[...]` and `V` is an array type `V1[...]` of the same rank</span></span>
   *  <span data-ttu-id="602c5-672">`U` 중 하나인 `IEnumerable<Ue>`, `ICollection<Ue>` 하거나 `IList<Ue>` 고 `V` 형식인 1 차원 배열 `Ve[]`</span><span class="sxs-lookup"><span data-stu-id="602c5-672">`U` is one of `IEnumerable<Ue>`, `ICollection<Ue>` or `IList<Ue>` and `V` is a one-dimensional array type `Ve[]`</span></span>
   *  <span data-ttu-id="602c5-673">`U` 형식인 `U1?` 고 `V` 형식인 `V1?`</span><span class="sxs-lookup"><span data-stu-id="602c5-673">`U` is the type `U1?` and `V` is the type `V1?`</span></span>
   *  <span data-ttu-id="602c5-674">`U` 생성 된 클래스, 구조체, 인터페이스 또는 대리자 형식 `C<U1...Uk>` 및 `V` (직접 또는 간접적으로) 클래스, 구조체, 인터페이스 또는 대리자 형식에서 상속 (직접 또는 간접적으로)를 동일한 또는 구현 되는 고유한 형식 `C<V1...Vk>`</span><span class="sxs-lookup"><span data-stu-id="602c5-674">`U` is constructed class, struct, interface or delegate type `C<U1...Uk>` and `V` is a class, struct, interface or delegate type which is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) a unique type `C<V1...Vk>`</span></span>

      <span data-ttu-id="602c5-675">("고유성" 제한 한다는 것을 의미 했습니다 `interface C<T>{} class V<Z>: C<X<Z>>, C<Y<Z>>{}`에서 유추할 때 유추가 수행할 `C<U1>` 에 `V<Q>`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-675">(The "uniqueness" restriction means that if we have `interface C<T>{} class V<Z>: C<X<Z>>, C<Y<Z>>{}`, then no inference is made when inferring from `C<U1>` to `V<Q>`.</span></span> <span data-ttu-id="602c5-676">추론에서 되지 `U1` 하나로 `X<Q>` 또는 `Y<Q>`.)</span><span class="sxs-lookup"><span data-stu-id="602c5-676">Inferences are not made from `U1` to either `X<Q>` or `Y<Q>`.)</span></span>

   <span data-ttu-id="602c5-677">이러한 경우는 유추 수행할를 적용 하는 경우 *에서* 각 `Ui` *를* 해당 `Vi` 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-677">If any of these cases apply then an inference is made *from* each `Ui` *to* the corresponding `Vi` as follows:</span></span>
   *  <span data-ttu-id="602c5-678">하는 경우 `Ui` 참조 형식으로 알려지지 않은 됩니다 *유추 정확한* 됩니다</span><span class="sxs-lookup"><span data-stu-id="602c5-678">If  `Ui` is not known to be a reference type then an *exact inference* is made</span></span>
   *  <span data-ttu-id="602c5-679">그렇지 않은 경우, `V` 배열 형식인 됩니다 *상한을 유추* 됩니다</span><span class="sxs-lookup"><span data-stu-id="602c5-679">Otherwise, if `V` is an array type then an *upper-bound inference* is made</span></span>
   *  <span data-ttu-id="602c5-680">그렇지 않고 `U` 됩니다 `C<U1...Uk>` 유추 i 번째 형식 매개 변수에 따라 다음 `C`:</span><span class="sxs-lookup"><span data-stu-id="602c5-680">Otherwise, if `U` is `C<U1...Uk>` then inference depends on the i-th type parameter of `C`:</span></span>
      *  <span data-ttu-id="602c5-681">공변 (covariant) 경우는 *상한을 유추* 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-681">If it is covariant then an *upper-bound inference* is made.</span></span>
      *  <span data-ttu-id="602c5-682">반공 변 경우는 *유추가* 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-682">If it is contravariant then a *lower-bound inference* is made.</span></span>
      *  <span data-ttu-id="602c5-683">Variant 없으면 됩니다 *유추 정확한* 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-683">If it is invariant then an *exact inference* is made.</span></span>
*  <span data-ttu-id="602c5-684">그렇지 않으면 없습니다 추론이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-684">Otherwise, no inferences are made.</span></span>   

#### <a name="fixing"></a><span data-ttu-id="602c5-685">수정</span><span class="sxs-lookup"><span data-stu-id="602c5-685">Fixing</span></span>

<span data-ttu-id="602c5-686">*고정 되지 않은* 유형의 변수에 `Xi` 경계 설정 *고정* 다음과 같습니다:</span><span class="sxs-lookup"><span data-stu-id="602c5-686">An *unfixed* type variable `Xi` with a set of bounds is *fixed* as follows:</span></span>

*  <span data-ttu-id="602c5-687">집합이 *후보 형식* `Uj` 경계를 집합에서 모든 종류의 집합으로 시작 `Xi`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-687">The set of *candidate types* `Uj` starts out as the set of all types in the set of bounds for `Xi`.</span></span>
*  <span data-ttu-id="602c5-688">그런 다음 각 경계를 살펴봅니다 `Xi` 차례로: 각 정확한 범위에 대 한 `U` 의 `Xi` 유형도 `Uj` 와 동일 하지 않습니다 `U` 후보 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-688">We then examine each bound for `Xi` in turn: For each exact bound `U` of `Xi` all types `Uj` which are not identical to `U` are removed from the candidate set.</span></span> <span data-ttu-id="602c5-689">각 범위에 대 한 `U` 의 `Xi` 유형도 `Uj` 는 여기에는 *하지* 암시적 변환이 `U` 후보 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-689">For each lower bound `U` of `Xi` all types `Uj` to which there is *not* an implicit conversion from `U` are removed from the candidate set.</span></span> <span data-ttu-id="602c5-690">각 상한 값에 대 한 `U` 의 `Xi` 유형도 `Uj` 는 여기에서 *하지* 암시적 변환 `U` 후보 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-690">For each upper bound `U` of `Xi` all types `Uj` from which there is *not* an implicit conversion to `U` are removed from the candidate set.</span></span>
*  <span data-ttu-id="602c5-691">If 나머지 후보 형식 간의 `Uj` 고유 유형이 `V` 는 암시적 변환이 모든 다른 후보 유형으로 다음에서 `Xi` 로 고정 됩니다 `V`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-691">If among the remaining candidate types `Uj` there is a unique type `V` from which there is an implicit conversion to all the other candidate types, then `Xi` is fixed to `V`.</span></span>
*  <span data-ttu-id="602c5-692">그렇지 않은 경우 형식 유추가 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-692">Otherwise, type inference fails.</span></span>

#### <a name="inferred-return-type"></a><span data-ttu-id="602c5-693">유추 반환 형식</span><span class="sxs-lookup"><span data-stu-id="602c5-693">Inferred return type</span></span>

<span data-ttu-id="602c5-694">유추 된 익명 함수 유형을 반환 `F` 형식 유추 및 오버 로드 확인 중에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-694">The inferred return type of an anonymous function `F` is used during type inference and overload resolution.</span></span> <span data-ttu-id="602c5-695">유추 반환 형식 종류를 알고 있는 경우 하거나 명시적으로 학생은 때문에 모든 매개 변수는 익명 함수 변환을 통해 제공 하거나 유추 하는 동안에 형식 유추 바깥쪽 제네릭 있는 익명 함수에만 확인할 수 있습니다. 메서드 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-695">The inferred return type can only be determined for an anonymous function where all parameter types are known, either because they are explicitly given, provided through an anonymous function conversion or inferred during type inference on an enclosing generic method invocation.</span></span>

<span data-ttu-id="602c5-696">합니다 ***결과 형식 유추*** 다음과 같이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-696">The ***inferred result type*** is determined as follows:</span></span>

*  <span data-ttu-id="602c5-697">경우 본문 `F` 은 *식* 형식에 다음의 유추 된 결과 형식에는 `F` 해당 식의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-697">If the body of `F` is an *expression* that has a type, then the inferred result type of `F` is the type of that expression.</span></span>
*  <span data-ttu-id="602c5-698">경우 본문 `F` 되는 *블록* 및 식 블록의 집합 `return` 문을 가장 일반적인 형식이 `T` ([식집합의가장일반적인형식찾기](expressions.md#finding-the-best-common-type-of-a-set-of-expressions))의 유추 된 결과 형식은 `F` 는 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-698">If the body of `F` is a *block* and the set of expressions in the block's `return` statements has a best common type `T` ([Finding the best common type of a set of expressions](expressions.md#finding-the-best-common-type-of-a-set-of-expressions)), then the inferred result type of `F` is `T`.</span></span>
*  <span data-ttu-id="602c5-699">에 대 한 결과 형식을 유추할 수 없습니다이 고, 그렇지 `F`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-699">Otherwise, a result type cannot be inferred for `F`.</span></span>

<span data-ttu-id="602c5-700">합니다 ***반환 형식을 유추*** 다음과 같이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-700">The ***inferred return type*** is determined as follows:</span></span>

*  <span data-ttu-id="602c5-701">하는 경우 `F` 비동기 이며 본문 `F` nothing으로 분류 하거나 식 ([식 분류](expressions.md#expression-classifications)), 또는 return 문은 없습니다 있는 식, 문 블록을 유추 된 반환 형식은 `System.Threading.Tasks.Task`</span><span class="sxs-lookup"><span data-stu-id="602c5-701">If `F` is async and the body of `F` is either an expression classified as nothing ([Expression classifications](expressions.md#expression-classifications)), or a statement block where no return statements have expressions, the inferred return type is `System.Threading.Tasks.Task`</span></span>
*  <span data-ttu-id="602c5-702">하는 경우 `F` 비동기 이며 유추 결과 형식이 `T`, 유추 된 반환 형식이 `System.Threading.Tasks.Task<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-702">If `F` is async and has an inferred result type `T`, the inferred return type is `System.Threading.Tasks.Task<T>`.</span></span>
*  <span data-ttu-id="602c5-703">하는 경우 `F` 비동기가 아닌 이며 유추 결과 형식이 `T`, 유추 된 반환 형식이 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-703">If `F` is non-async and has an inferred result type `T`, the inferred return type is `T`.</span></span>
*  <span data-ttu-id="602c5-704">에 대 한 반환 형식을 유추할 수 없습니다이 고, 그렇지 `F`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-704">Otherwise a return type cannot be inferred for `F`.</span></span>

<span data-ttu-id="602c5-705">익명 함수를 포함 하는 형식 유추의 예로 `Select` 에 선언 된 확장 메서드는 `System.Linq.Enumerable` 클래스:</span><span class="sxs-lookup"><span data-stu-id="602c5-705">As an example of type inference involving anonymous functions, consider the `Select` extension method declared in the `System.Linq.Enumerable` class:</span></span>
```csharp
namespace System.Linq
{
    public static class Enumerable
    {
        public static IEnumerable<TResult> Select<TSource,TResult>(
            this IEnumerable<TSource> source,
            Func<TSource,TResult> selector)
        {
            foreach (TSource element in source) yield return selector(element);
        }
    }
}
```

<span data-ttu-id="602c5-706">가정 합니다 `System.Linq` 네임 스페이스를 사용 하 여 가져온를 `using` 절 클래스가 있다고 가정 하 고 `Customer` 사용 하 여를 `Name` 형식의 속성 `string`, `Select` 메서드 고객 목록의 이름을 선택 하는데 사용할 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="602c5-706">Assuming the `System.Linq` namespace was imported with a `using` clause, and given a class `Customer` with a `Name` property of type `string`, the `Select` method can be used to select the names of a list of customers:</span></span>
```csharp
List<Customer> customers = GetCustomerList();
IEnumerable<string> names = customers.Select(c => c.Name);
```

<span data-ttu-id="602c5-707">확장 메서드 호출 ([확장 메서드 호출](expressions.md#extension-method-invocations))의 `Select` 정적 메서드 호출에 대 한 호출을 다시 작성 하 여 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-707">The extension method invocation ([Extension method invocations](expressions.md#extension-method-invocations)) of `Select` is processed by rewriting the invocation to a static method invocation:</span></span>
```csharp
IEnumerable<string> names = Enumerable.Select(customers, c => c.Name);
```

<span data-ttu-id="602c5-708">형식 인수를 명시적으로 지정 되지 않았습니다, 이후 형식 유추 형식 인수를 유추 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-708">Since type arguments were not explicitly specified, type inference is used to infer the type arguments.</span></span> <span data-ttu-id="602c5-709">먼저 합니다 `customers` 인수는 관련이 합니다 `source` 매개 변수를 유추 `T` 되도록 `Customer`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-709">First, the `customers` argument is related to the `source` parameter, inferring `T` to be `Customer`.</span></span> <span data-ttu-id="602c5-710">익명 함수를 사용 하 여 위에서 설명한 유추 과정을 입력 하는 한 `c` 형식이 지정 되며 `Customer`, 및 식 `c.Name` 의 반환 형식은 관련이 합니다 `selector` 매개 변수를 유추 `S` 되도록`string`.</span><span class="sxs-lookup"><span data-stu-id="602c5-710">Then, using the anonymous function type inference process described above, `c` is given type `Customer`, and the expression `c.Name` is related to the return type of the `selector` parameter, inferring `S` to be `string`.</span></span> <span data-ttu-id="602c5-711">따라서 호출에 해당 하는</span><span class="sxs-lookup"><span data-stu-id="602c5-711">Thus, the invocation is equivalent to</span></span>
```csharp
Sequence.Select<Customer,string>(customers, (Customer c) => c.Name)
```
<span data-ttu-id="602c5-712">형식의 결과 `IEnumerable<string>`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-712">and the result is of type `IEnumerable<string>`.</span></span>

<span data-ttu-id="602c5-713">다음 예제에서는 어떻게 익명 함수 형식 유추 "흘러나오는" 제네릭 메서드 호출의 인수 간의 형식 정보를 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-713">The following example demonstrates how anonymous function type inference allows type information to "flow" between arguments in a generic method invocation.</span></span> <span data-ttu-id="602c5-714">메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-714">Given the method:</span></span>
```csharp
static Z F<X,Y,Z>(X value, Func<X,Y> f1, Func<Y,Z> f2) {
    return f2(f1(value));
}
```

<span data-ttu-id="602c5-715">호출에 대 한 형식 유추 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-715">Type inference for the invocation:</span></span>
```csharp
double seconds = F("1:15:30", s => TimeSpan.Parse(s), t => t.TotalSeconds);
```
<span data-ttu-id="602c5-716">다음과 같이 진행 됩니다: 첫 번째 인수 `"1:15:30"` 관련이 `value` 매개 변수를 유추 `X` 되도록 `string`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-716">proceeds as follows: First, the argument `"1:15:30"` is related to the `value` parameter, inferring `X` to be `string`.</span></span> <span data-ttu-id="602c5-717">다음, 첫 번째 익명 함수의 매개 변수 `s`, 유추 된 형식이 지정 되며 `string`, 및 식 `TimeSpan.Parse(s)` 의 반환 형식은 관련이 `f1`, 유추 `Y` 되도록 `System.TimeSpan`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-717">Then, the parameter of the first anonymous function, `s`, is given the inferred type `string`, and the expression `TimeSpan.Parse(s)` is related to the return type of `f1`, inferring `Y` to be `System.TimeSpan`.</span></span> <span data-ttu-id="602c5-718">마지막으로, 두 번째 익명 함수의 매개 변수 `t`, 유추 된 형식이 지정 되며 `System.TimeSpan`, 및 식 `t.TotalSeconds` 의 반환 형식은 관련이 `f2`, 유추 `Z` 되도록 `double`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-718">Finally, the parameter of the second anonymous function, `t`, is given the inferred type `System.TimeSpan`, and the expression `t.TotalSeconds` is related to the return type of `f2`, inferring `Z` to be `double`.</span></span> <span data-ttu-id="602c5-719">따라서 호출의 결과 형식 `double`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-719">Thus, the result of the invocation is of type `double`.</span></span>

#### <a name="type-inference-for-conversion-of-method-groups"></a><span data-ttu-id="602c5-720">메서드 그룹 변환에 대 한 형식 유추</span><span class="sxs-lookup"><span data-stu-id="602c5-720">Type inference for conversion of method groups</span></span>

<span data-ttu-id="602c5-721">비슷하게 제네릭 메서드 호출 형식 유추도 적용 해야 때 메서드 그룹이 `M` 지정 된 대리자 형식을 제네릭 메서드가 포함 된 변환할 `D` ([메서드 그룹 변환](conversions.md#method-group-conversions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-721">Similar to calls of generic methods, type inference must also be applied when a method group `M` containing a generic method is converted to a given delegate type `D` ([Method group conversions](conversions.md#method-group-conversions)).</span></span> <span data-ttu-id="602c5-722">지정 된 메서드</span><span class="sxs-lookup"><span data-stu-id="602c5-722">Given a method</span></span>
```csharp
Tr M<X1...Xn>(T1 x1 ... Tm xm)
```
<span data-ttu-id="602c5-723">메서드 그룹과 `M` 대리자 형식에 할당할 `D` 형식 인수를 검색할 형식 유추는 작업은 `S1...Sn` 있도록 식:</span><span class="sxs-lookup"><span data-stu-id="602c5-723">and the method group `M` being assigned to the delegate type `D` the task of type inference is to find type arguments `S1...Sn` so that the expression:</span></span>
```csharp
M<S1...Sn>
```
<span data-ttu-id="602c5-724">호환 됩니다 ([대리자 선언](delegates.md#delegate-declarations)) 사용 하 여 `D`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-724">becomes compatible ([Delegate declarations](delegates.md#delegate-declarations)) with `D`.</span></span>

<span data-ttu-id="602c5-725">제네릭 메서드 호출에 대 한 형식 유추 알고리즘, 달리이 경우 가지 인수만 *형식*에 인수가 없습니다 *식을*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-725">Unlike the type inference algorithm for generic method calls, in this case there are only argument *types*, no argument *expressions*.</span></span> <span data-ttu-id="602c5-726">특히 가지 익명 함수가 없습니다. 따라서 유추의 여러 단계에 대 한 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-726">In particular, there are no anonymous functions and hence no need for multiple phases of inference.</span></span>

<span data-ttu-id="602c5-727">대신, 모든 `Xi` 것으로 간주 됩니다 *고정 되지 않은*, 및 *유추가* 이루어집니다 *에서* 각 인수 형식이 `Uj` 의 `D` *하* 해당 매개 변수 형식 `Tj` 의 `M`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-727">Instead, all `Xi` are considered *unfixed*, and a *lower-bound inference* is made *from* each argument type `Uj` of `D` *to* the corresponding parameter type `Tj` of `M`.</span></span> <span data-ttu-id="602c5-728">에 대 한 경우에는 `Xi` 없는 경계를 찾을 수 없습니다, 형식 유추가 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-728">If for any of the `Xi` no bounds were found, type inference fails.</span></span> <span data-ttu-id="602c5-729">그렇지 않으면 모든 `Xi` 는 *고정* 해당 `Si`, 형식 유추의 결과.</span><span class="sxs-lookup"><span data-stu-id="602c5-729">Otherwise, all `Xi` are *fixed* to corresponding `Si`, which are the result of type inference.</span></span>

#### <a name="finding-the-best-common-type-of-a-set-of-expressions"></a><span data-ttu-id="602c5-730">식 집합의 가장 일반적인 형식 찾기</span><span class="sxs-lookup"><span data-stu-id="602c5-730">Finding the best common type of a set of expressions</span></span>

<span data-ttu-id="602c5-731">경우에 따라 공용 형식 식의 집합에 대 한 유추 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-731">In some cases, a common type needs to be inferred for a set of expressions.</span></span> <span data-ttu-id="602c5-732">특히, 암시적으로 형식화 된 배열의 요소 형식 및 포함 된 익명 함수의 반환 형식은 *블록* 본문이 이렇게에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-732">In particular, the element types of implicitly typed arrays and the return types of anonymous functions with *block* bodies are found in this way.</span></span>

<span data-ttu-id="602c5-733">직관적으로 지정 된 식 집합 `E1...Em` 이 유추에 해당 하는 메서드를 호출 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-733">Intuitively, given a set of expressions `E1...Em` this inference should be equivalent to calling a method</span></span>
```csharp
Tr M<X>(X x1 ... X xm)
```
<span data-ttu-id="602c5-734">사용 하 여는 `Ei` 인수로 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-734">with the `Ei` as arguments.</span></span>

<span data-ttu-id="602c5-735">보다 정확 하 게 유추가 시작을 *고정 되지 않은* 유형의 변수에 `X`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-735">More precisely, the inference starts out with an *unfixed* type variable `X`.</span></span> <span data-ttu-id="602c5-736">*출력 형식 유추* 됩니다 *에서* 각 `Ei` *하* `X`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-736">*Output type inferences* are then made *from* each `Ei` *to* `X`.</span></span> <span data-ttu-id="602c5-737">마지막으로, `X` 됩니다 *고정* 하 고 성공 하면 결과 입력 `S` 식의 결과 가장 일반적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-737">Finally, `X` is *fixed* and, if successful, the resulting type `S` is the resulting best common type for the expressions.</span></span> <span data-ttu-id="602c5-738">그러한 `S` 있는 식이 있는 가장 일반적인 형식이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-738">If no such `S` exists, the expressions have no best common type.</span></span>

### <a name="overload-resolution"></a><span data-ttu-id="602c5-739">오버 로드 확인</span><span class="sxs-lookup"><span data-stu-id="602c5-739">Overload resolution</span></span>

<span data-ttu-id="602c5-740">오버 로드 확인은 인수 목록 및 후보 함수 멤버 집합을 호출할 최상의 함수 멤버를 선택 하는 바인딩 타임 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-740">Overload resolution is a binding-time mechanism for selecting the best function member to invoke given an argument list and a set of candidate function members.</span></span> <span data-ttu-id="602c5-741">오버 로드 확인은 다음과 같은 컨텍스트 내에서 C#를 호출 하는 함수 멤버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-741">Overload resolution selects the function member to invoke in the following distinct contexts within C#:</span></span>

*  <span data-ttu-id="602c5-742">에 명명 된 메서드 호출을 *invocation_expression* ([메서드 호출](expressions.md#method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="602c5-742">Invocation of a method named in an *invocation_expression* ([Method invocations](expressions.md#method-invocations)).</span></span>
*  <span data-ttu-id="602c5-743">에 명명 된 인스턴스 생성자의 호출을 *object_creation_expression* ([개체 만들기 식](expressions.md#object-creation-expressions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-743">Invocation of an instance constructor named in an *object_creation_expression* ([Object creation expressions](expressions.md#object-creation-expressions)).</span></span>
*  <span data-ttu-id="602c5-744">통해 인덱서 접근자의 호출을 *element_access* ([요소 액세스](expressions.md#element-access)).</span><span class="sxs-lookup"><span data-stu-id="602c5-744">Invocation of an indexer accessor through an *element_access* ([Element access](expressions.md#element-access)).</span></span>
*  <span data-ttu-id="602c5-745">호출 식에서 참조 하는 미리 정의 된 또는 사용자 정의 연산자 ([단항 연산자 오버 로드 확인](expressions.md#unary-operator-overload-resolution) 하 고 [이항 연산자 오버 로드 확인에](expressions.md#binary-operator-overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="602c5-745">Invocation of a predefined or user-defined operator referenced in an expression ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution) and [Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)).</span></span>

<span data-ttu-id="602c5-746">이러한 각 컨텍스트 정의 후보 함수 멤버 집합 및 인수 목록을 자체 고유한 방식으로 위의 섹션에서 자세히 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-746">Each of these contexts defines the set of candidate function members and the list of arguments in its own unique way, as described in detail in the sections listed above.</span></span> <span data-ttu-id="602c5-747">예를 들어, 메서드 호출에 대 한 후보 집합을 표시 하는 방법을 다루지 않습니다 `override` ([멤버 조회](expressions.md#member-lookup)), 기본 클래스에서 메서드 후보가 아닙니다 파생된 클래스에서 모든 메서드는 해당 하는 경우 및 ([ 메서드 호출](expressions.md#method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="602c5-747">For example, the set of candidates for a method invocation does not include methods marked `override` ([Member lookup](expressions.md#member-lookup)), and methods in a base class are not candidates if any method in a derived class is applicable ([Method invocations](expressions.md#method-invocations)).</span></span>

<span data-ttu-id="602c5-748">후보 함수 멤버 및 인수 목록을 식별 되 면 최상의 함수 멤버를 선택은 모든 경우에서와 동일:</span><span class="sxs-lookup"><span data-stu-id="602c5-748">Once the candidate function members and the argument list have been identified, the selection of the best function member is the same in all cases:</span></span>

*  <span data-ttu-id="602c5-749">최상의 집합이 멤버를 함수 적용 가능한 후보 함수 멤버 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-749">Given the set of applicable candidate function members, the best function member in that set is located.</span></span> <span data-ttu-id="602c5-750">집합 함수 멤버가 하나만 있으면 해당 하는 함수 멤버는 최상의 함수 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-750">If the set contains only one function member, then that function member is the best function member.</span></span> <span data-ttu-id="602c5-751">최상의 함수 멤버는 각 함수 멤버의 규칙을 사용 하 여 모든 기타 함수 멤버과 비교 되는 지정 된 인수 목록에 대해 모든 기타 함수 멤버 보다는 하나의 함수 멤버가 고, 그렇지 [ 최상의 함수 멤버](expressions.md#better-function-member)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-751">Otherwise, the best function member is the one function member that is better than all other function members with respect to the given argument list, provided that each function member is compared to all other function members using the rules in [Better function member](expressions.md#better-function-member).</span></span> <span data-ttu-id="602c5-752">정확 하 게 모든 기타 함수 멤버 보다 나은 함수 멤버가 하나 있으면 함수 멤버 호출이 모호 합니다 및 바인딩 시간에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-752">If there is not exactly one function member that is better than all other function members, then the function member invocation is ambiguous and a binding-time error occurs.</span></span>

<span data-ttu-id="602c5-753">다음 섹션에서는 정의 용어의 정확한 의미 ***적용 가능한 함수 멤버*** 하 고 ***최상의 함수 멤버***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-753">The following sections define the exact meanings of the terms ***applicable function member*** and ***better function member***.</span></span>

#### <a name="applicable-function-member"></a><span data-ttu-id="602c5-754">적용 가능한 함수 멤버</span><span class="sxs-lookup"><span data-stu-id="602c5-754">Applicable function member</span></span>

<span data-ttu-id="602c5-755">함수 멤버 라고는 ***적용 가능한 함수 멤버*** 인수 목록에 대해 `A` 경우 다음 모두:</span><span class="sxs-lookup"><span data-stu-id="602c5-755">A function member is said to be an ***applicable function member*** with respect to an argument list `A` when all of the following are true:</span></span>

*  <span data-ttu-id="602c5-756">각 인수 `A` 에 설명 된 대로 함수 멤버 선언의 매개 변수에 해당 [해당 매개 변수](expressions.md#corresponding-parameters)를 인수 없이 해당 하는 모든 매개 변수는 선택적 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-756">Each argument in `A` corresponds to a parameter in the function member declaration as described in [Corresponding parameters](expressions.md#corresponding-parameters), and any parameter to which no argument corresponds is an optional parameter.</span></span>
*  <span data-ttu-id="602c5-757">각 인수에 대 한 `A`모드는 인수를 전달 매개 변수 (즉, 값 `ref`, 또는 `out`) 해당 매개 변수의 매개 변수 전달 모드와 동일 하 고</span><span class="sxs-lookup"><span data-stu-id="602c5-757">For each argument in `A`, the parameter passing mode of the argument (i.e., value, `ref`, or `out`) is identical to the parameter passing mode of the corresponding parameter, and</span></span>
   *  <span data-ttu-id="602c5-758">값 매개 변수 또는 매개 변수 배열로 암시적 변환에 대 한 ([암시적 변환을](conversions.md#implicit-conversions)) 해당 매개 변수의 형식 인수에서 존재 또는</span><span class="sxs-lookup"><span data-stu-id="602c5-758">for a value parameter or a parameter array, an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) exists from the argument to the type of the corresponding parameter, or</span></span>
   *  <span data-ttu-id="602c5-759">에 `ref` 또는 `out` 매개 변수 인수의 형식은 해당 매개 변수의 유형과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-759">for a `ref` or `out` parameter, the type of the argument is identical to the type of the corresponding parameter.</span></span> <span data-ttu-id="602c5-760">결국에 `ref` 또는 `out` 매개 변수는 전달 된 인수에 대 한 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-760">After all, a `ref` or `out` parameter is an alias for the argument passed.</span></span>

<span data-ttu-id="602c5-761">매개 변수 배열에 포함 하는 함수 멤버에 적용할 라고 하는 함수 멤버를 위의 규칙에 따라 적용할 수 있는 경우 해당 ***정규형***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-761">For a function member that includes a parameter array, if the function member is applicable by the above rules, it is said to be applicable in its ***normal form***.</span></span> <span data-ttu-id="602c5-762">함수 멤버 대신에 적용할 수 있습니다 매개 변수 배열을 포함 하는 함수 멤버를 해당 기본 형식에 적용할 수 없는 경우 해당 ***폼을 확장***:</span><span class="sxs-lookup"><span data-stu-id="602c5-762">If a function member that includes a parameter array is not applicable in its normal form, the function member may instead be applicable in its ***expanded form***:</span></span>

*  <span data-ttu-id="602c5-763">함수 멤버 선언의 매개 변수 배열의 0으로 대체 하 여 생성 된 확장 된 형식 또는 매개 변수의 요소 형식의 자세한 값 매개 변수 배열 같은 해당 인수 목록의 인수 개수 `A` 합계와 일치 매개 변수 개수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-763">The expanded form is constructed by replacing the parameter array in the function member declaration with zero or more value parameters of the element type of the parameter array such that the number of arguments in the argument list `A` matches the total number of parameters.</span></span> <span data-ttu-id="602c5-764">경우 `A` 함수 멤버 선언에서 고정 된 매개 변수 개수 보다 더 적은 인수가, 확장 된 형태의 함수 멤버를 생성할 수 없습니다 하 고 있으므로 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-764">If `A` has fewer arguments than the number of fixed parameters in the function member declaration, the expanded form of the function member cannot be constructed and is thus not applicable.</span></span>
*  <span data-ttu-id="602c5-765">확장 된 형식 그러지 않으면 각 인수에 대해 작업 하는 경우 해당은 `A` 인수 매개 변수 전달 모드는 해당 매개 변수의 매개 변수 전달 모드와 동일 하 고</span><span class="sxs-lookup"><span data-stu-id="602c5-765">Otherwise, the expanded form is applicable if for each argument in `A` the parameter passing mode of the argument is identical to the parameter passing mode of the corresponding parameter, and</span></span>
   *  <span data-ttu-id="602c5-766">고정된 값 매개 변수 또는 암시적 변환이 확장을 통해 만들어진 값 매개 변수 ([암시적 변환을](conversions.md#implicit-conversions)) 형식 인수의 형식에서 해당 매개 변수의 형식으로 또는</span><span class="sxs-lookup"><span data-stu-id="602c5-766">for a fixed value parameter or a value parameter created by the expansion, an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) exists from the type of the argument to the type of the corresponding parameter, or</span></span>
   *  <span data-ttu-id="602c5-767">에 `ref` 또는 `out` 매개 변수 인수의 형식은 해당 매개 변수의 유형과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-767">for a `ref` or `out` parameter, the type of the argument is identical to the type of the corresponding parameter.</span></span>

#### <a name="better-function-member"></a><span data-ttu-id="602c5-768">최상의 함수 멤버</span><span class="sxs-lookup"><span data-stu-id="602c5-768">Better function member</span></span>

<span data-ttu-id="602c5-769">최상의 함수 멤버를 결정 하는 용도로 인수 식 자체 원래 인수 목록에 표시 되는 순서 대로 포함 하는 축소 된 기본 인수 목록을 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-769">For the purposes of determining the better function member, a stripped-down argument list A is constructed containing just the argument expressions themselves in the order they appear in the original argument list.</span></span>

<span data-ttu-id="602c5-770">각 멤버는 다음과 같은 방법으로 생성 된 후보 함수에 대 한 매개 변수는 나열:</span><span class="sxs-lookup"><span data-stu-id="602c5-770">Parameter lists for each of the candidate function members are constructed in the following way:</span></span>

*  <span data-ttu-id="602c5-771">확장 된 양식은 함수 멤버를 확장 된 형식에만 해당 하는 경우에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-771">The expanded form is used if the function member was applicable only in the expanded form.</span></span>
*  <span data-ttu-id="602c5-772">해당 인수를 사용 하 여 선택적 매개 변수는 매개 변수 목록에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-772">Optional parameters with no corresponding arguments are removed from the parameter list</span></span>
*  <span data-ttu-id="602c5-773">매개 변수는 인수 목록의 해당 인수와 동일한 위치에서 발생 하는 기록 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-773">The parameters are reordered so that they occur at the same position as the corresponding argument in the argument list.</span></span>

<span data-ttu-id="602c5-774">인수 목록 `A` 인수 식의 집합을 사용 하 여 `{E1, E2, ..., En}` 및 두 적용 가능한 함수 멤버 `Mp` 및 `Mq` 매개 변수 형식을 가진 `{P1, P2, ..., Pn}` 및 `{Q1, Q2, ..., Qn}`, `Mp` 것으로 정의 되는 ***최상의 함수 멤버*** 보다 `Mq` 경우</span><span class="sxs-lookup"><span data-stu-id="602c5-774">Given an argument list `A` with a set of argument expressions `{E1, E2, ..., En}` and two applicable function members `Mp` and `Mq` with parameter types `{P1, P2, ..., Pn}` and `{Q1, Q2, ..., Qn}`, `Mp` is defined to be a ***better function member*** than `Mq` if</span></span>

*  <span data-ttu-id="602c5-775">각 인수에 암시적으로 변환 `Ex` 하 `Qx` 암시적으로 변환 보다 좋습니다 `Ex` 에 `Px`, 및</span><span class="sxs-lookup"><span data-stu-id="602c5-775">for each argument, the implicit conversion from `Ex` to `Qx` is not better than the implicit conversion from `Ex` to `Px`, and</span></span>
*  <span data-ttu-id="602c5-776">하나 이상의 인수를 변환에 대 한 `Ex` 하 `Px` 변환 보다 나은 `Ex` 에 `Qx`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-776">for at least one argument, the conversion from `Ex` to `Px` is better than the conversion from `Ex` to `Qx`.</span></span>

<span data-ttu-id="602c5-777">이 평가 수행할 때 `Mp` 또는 `Mq` 이면 해당 확장된 형식에 적용할 수 `Px` 또는 `Qx` 확장된 형식의 매개 변수 목록에서 매개 변수를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-777">When performing this evaluation, if `Mp` or `Mq` is applicable in its expanded form, then `Px` or `Qx` refers to a parameter in the expanded form of the parameter list.</span></span>

<span data-ttu-id="602c5-778">매개 변수는 시퀀스를 입력 하는 경우 `{P1, P2, ..., Pn}` 하 고 `{Q1, Q2, ..., Qn}` 동일 (즉, 각 `Pi` 에 해당 하는 id 변환을 `Qi`)를 향상을 확인 하려면 다음 주요 동률 규칙이 적용 됩니다 함수 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-778">In case the parameter type sequences `{P1, P2, ..., Pn}` and `{Q1, Q2, ..., Qn}` are equivalent (i.e. each `Pi` has an identity conversion to the corresponding `Qi`), the following tie-breaking rules are applied, in order, to determine the better function member.</span></span>

*  <span data-ttu-id="602c5-779">하는 경우 `Mp` 제네릭이 아닌 메서드는 및 `Mq` 제네릭 메서드 이면 `Mp` 보다 나은 `Mq`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-779">If `Mp` is a non-generic method and `Mq` is a generic method, then `Mp` is better than `Mq`.</span></span>
*  <span data-ttu-id="602c5-780">그렇지 않은 경우, `Mp` 해당 기본 폼에 적용 됩니다 및 `Mq` 에 `params` 배열을 가져온 다음 해당 확장된 형식에만 적용 됩니다 `Mp` 보다 나은 `Mq`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-780">Otherwise, if `Mp` is applicable in its normal form and `Mq` has a `params` array and is applicable only in its expanded form, then `Mp` is better than `Mq`.</span></span>
*  <span data-ttu-id="602c5-781">그렇지 않은 경우, `Mp` 보다 매개 변수를 더 선언에 `Mq`, 한 다음 `Mp` 보다 나은 `Mq`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-781">Otherwise, if `Mp` has more declared parameters than `Mq`, then `Mp` is better than `Mq`.</span></span> <span data-ttu-id="602c5-782">두 방법 모두 경우 발생할 수 있습니다이 `params` 배열 및 확장된의 형식에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-782">This can occur if both methods have `params` arrays and are applicable only in their expanded forms.</span></span>
*  <span data-ttu-id="602c5-783">그렇지 않은 경우의 모든 매개 변수 `Mp` 기본 인수에 하나 이상의 선택적 매개 변수를 대체 해야 하는 반면 해당 인수를 가질 `Mq` 한 다음 `Mp` 보다는 낫습니다 `Mq`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-783">Otherwise if all parameters of `Mp` have a corresponding argument whereas default arguments need to be substituted for at least one optional parameter in `Mq` then `Mp` is better than `Mq`.</span></span>
*  <span data-ttu-id="602c5-784">그렇지 않은 경우, `Mp` 보다 구체적인 매개 변수 형식이 `Mq`, 한 다음 `Mp` 보다 나은 `Mq`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-784">Otherwise, if `Mp` has more specific parameter types than `Mq`, then `Mp` is better than `Mq`.</span></span> <span data-ttu-id="602c5-785">수 있도록 `{R1, R2, ..., Rn}` 하 고 `{S1, S2, ..., Sn}` 인스턴스화되지 않은 및 확장 되지 않은 매개 변수 형식을 나타내는 `Mp` 및 `Mq`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-785">Let `{R1, R2, ..., Rn}` and `{S1, S2, ..., Sn}` represent the uninstantiated and unexpanded parameter types of `Mp` and `Mq`.</span></span> <span data-ttu-id="602c5-786">`Mp`매개 변수 유형은 보다 구체적인 `Mq`의 경우 각 매개 변수에 `Rx` 보다 덜 구체적인 아닙니다 `Sx`, 및 하나 이상의 매개 변수가 `Rx` 보다 구체적인 `Sx`:</span><span class="sxs-lookup"><span data-stu-id="602c5-786">`Mp`'s parameter types are more specific than `Mq`'s if, for each parameter, `Rx` is not less specific than `Sx`, and, for at least one parameter, `Rx` is more specific than `Sx`:</span></span>
   *  <span data-ttu-id="602c5-787">형식 매개 변수는 비형식 매개 변수 보다 덜 구체적입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-787">A type parameter is less specific than a non-type parameter.</span></span>
   *  <span data-ttu-id="602c5-788">재귀적으로 생성된 된 형식을 다른 생성 된 형식 (동일한 개수의 형식 인수) 하나 이상의 인수를 입력 하는 경우 보다 구체적인 이며 형식 인수 없이 다른의 해당 형식 인수 보다 덜 구체적인 것 보다 더 구체적입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-788">Recursively, a constructed type is more specific than another constructed type (with the same number of type arguments) if at least one type argument is more specific and no type argument is less specific than the corresponding type argument in the other.</span></span>
   *  <span data-ttu-id="602c5-789">배열 형식 (사용 하 여 동일한 차원 수) 다른 배열 형식 보다 구체적인 경우 첫 번째 요소 형식은 두 번째 요소 형식 보다 더 구체적입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-789">An array type is more specific than another array type (with the same number of dimensions) if the element type of the first is more specific than the element type of the second.</span></span>
*  <span data-ttu-id="602c5-790">그렇지 않으면 멤버가 하나는 비 리프트 된 연산자는 다른 리프트 된 연산자를 리프트 되지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-790">Otherwise if one member is a non-lifted operator and  the other is a lifted operator, the non-lifted one is better.</span></span>
*  <span data-ttu-id="602c5-791">그렇지 않으면 함수 멤버 모두이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-791">Otherwise, neither function member is better.</span></span>

#### <a name="better-conversion-from-expression"></a><span data-ttu-id="602c5-792">식에서 더 나은 변환</span><span class="sxs-lookup"><span data-stu-id="602c5-792">Better conversion from expression</span></span>

<span data-ttu-id="602c5-793">암시적 변환을 지정 `C1` 식에서 변환 하 `E` 형식으로 `T1`, 및 변환 하는 암시적 변환을 `C2` 식에서 변환 `E` 형식으로 `T2`, `C1` ***향상 된 변환*** 보다 `C2` 하는 경우 `E` 정확히 일치 하지 않는 `T2` 다음 중 하나 이상 보유 하 고:</span><span class="sxs-lookup"><span data-stu-id="602c5-793">Given an implicit conversion `C1` that converts from an expression `E` to a type `T1`, and an implicit conversion `C2` that converts from an expression `E` to a type `T2`, `C1` is a ***better conversion*** than `C2` if `E` does not exactly match `T2` and at least one of the following holds:</span></span>

* <span data-ttu-id="602c5-794">`E` 정확히 일치 `T1` ([정확 하 게 일치 식](expressions.md#exactly-matching-expression))</span><span class="sxs-lookup"><span data-stu-id="602c5-794">`E` exactly matches `T1` ([Exactly matching Expression](expressions.md#exactly-matching-expression))</span></span>
* <span data-ttu-id="602c5-795">`T1` 보다 나은 변환 대상인 `T2` ([변환 대상 더 나은](expressions.md#better-conversion-target))</span><span class="sxs-lookup"><span data-stu-id="602c5-795">`T1` is a better conversion target than `T2` ([Better conversion target](expressions.md#better-conversion-target))</span></span>

#### <a name="exactly-matching-expression"></a><span data-ttu-id="602c5-796">정확히 일치 하는 식</span><span class="sxs-lookup"><span data-stu-id="602c5-796">Exactly matching Expression</span></span>

<span data-ttu-id="602c5-797">식에 지정 되었습니다 `E` 형식과 `T`를 `E` 정확히 일치 `T` 다음 중 하나를 보유 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-797">Given an expression `E` and a type `T`, `E` exactly matches `T` if one of the following holds:</span></span>

*  <span data-ttu-id="602c5-798">`E` 형식이 `S`, 및에서 id 변환이 존재 `S` 를 `T`</span><span class="sxs-lookup"><span data-stu-id="602c5-798">`E` has a type `S`, and an identity conversion exists from `S` to `T`</span></span>
*  <span data-ttu-id="602c5-799">`E` 익명 함수 `T` 이 대리자 형식이 `D` 또는 식 트리 형식 `Expression<D>` 다음 중 하나를 보유 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-799">`E` is an anonymous function, `T` is either a delegate type `D` or an expression tree type `Expression<D>` and one of the following holds:</span></span>
   *  <span data-ttu-id="602c5-800">유추 된 반환 형식 `X` 에 대 한 존재 `E` 매개 변수 목록이의 컨텍스트에서 `D` ([유추 반환 형식](expressions.md#inferred-return-type))에서 id 변환이 존재 `X` 의 반환 형식 `D`</span><span class="sxs-lookup"><span data-stu-id="602c5-800">An inferred return type `X` exists for `E` in the context of the parameter list of `D` ([Inferred return type](expressions.md#inferred-return-type)), and an identity conversion exists from `X` to the return type of `D`</span></span>
   *  <span data-ttu-id="602c5-801">어느 `E` 은 비동기가 아닌 및 `D` 반환 형식이 `Y` 또는 `E` 는 비동기 및 `D` 반환 형식이 `Task<Y>`, 다음 중 하나를 보유 하 고:</span><span class="sxs-lookup"><span data-stu-id="602c5-801">Either `E` is non-async and `D` has a return type `Y` or `E` is async and `D` has a return type `Task<Y>`, and one of the following holds:</span></span>
      * <span data-ttu-id="602c5-802">본문 `E` 정확 하 게 일치 하는 식 `Y`</span><span class="sxs-lookup"><span data-stu-id="602c5-802">The body of `E` is an expression that exactly matches `Y`</span></span>
      * <span data-ttu-id="602c5-803">본문 `E` 은 문 블록이 모든 return 문이 반환 하는 위치 식을 정확 하 게 일치 `Y`</span><span class="sxs-lookup"><span data-stu-id="602c5-803">The body of `E` is a statement block where every return statement returns an expression that exactly matches `Y`</span></span>

#### <a name="better-conversion-target"></a><span data-ttu-id="602c5-804">더 나은 변환 대상</span><span class="sxs-lookup"><span data-stu-id="602c5-804">Better conversion target</span></span>

<span data-ttu-id="602c5-805">두 가지 유형이 지정 된 `T1` 및 `T2`를 `T1` 보다는 더 나은 변환 대상 `T2` 경우에서 암시적 변환은 없습니다 `T2` 에 `T1` 가 다음 중 하나 이상 보유 하 고:</span><span class="sxs-lookup"><span data-stu-id="602c5-805">Given two different types `T1` and `T2`, `T1` is a better conversion target than `T2` if no implicit conversion from `T2` to `T1` exists, and at least one of the following holds:</span></span>

*  <span data-ttu-id="602c5-806">암시적 변환이 `T1` 에 `T2` 존재</span><span class="sxs-lookup"><span data-stu-id="602c5-806">An implicit conversion from `T1` to `T2` exists</span></span>
*  <span data-ttu-id="602c5-807">`T1` 이 대리자 형식이 `D1` 또는 식 트리 형식을 `Expression<D1>`, `T2` 이 대리자 형식이 `D2` 또는 식 트리 형식 `Expression<D2>`를 `D1` 반환 형식이 `S1` 및 중 하나는 다음 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-807">`T1` is either a delegate type `D1` or an expression tree type `Expression<D1>`, `T2` is either a delegate type `D2` or an expression tree type `Expression<D2>`, `D1` has a return type `S1` and one of the following holds:</span></span>
   * <span data-ttu-id="602c5-808">`D2` void 반환</span><span class="sxs-lookup"><span data-stu-id="602c5-808">`D2` is void returning</span></span>
   * <span data-ttu-id="602c5-809">`D2` 반환 형식이 `S2`, 및 `S1` 보다는 더 나은 변환 대상 `S2`</span><span class="sxs-lookup"><span data-stu-id="602c5-809">`D2` has a return type `S2`, and `S1` is a better conversion target than `S2`</span></span>
*  <span data-ttu-id="602c5-810">`T1` 됩니다 `Task<S1>`, `T2` 됩니다 `Task<S2>`, 및 `S1` 보다는 더 나은 변환 대상 `S2`</span><span class="sxs-lookup"><span data-stu-id="602c5-810">`T1` is `Task<S1>`, `T2` is `Task<S2>`, and `S1` is a better conversion target than `S2`</span></span>
*  <span data-ttu-id="602c5-811">`T1` `S1` 또는 `S1?` 여기서 `S1` 부호 있는 정수 계열 형식이, 및 `T2` 는 `S2` 또는 `S2?` 여기서 `S2` 부호 없는 정수 계열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-811">`T1` is `S1` or `S1?` where `S1` is a signed integral type, and `T2` is `S2` or `S2?` where `S2` is an unsigned integral type.</span></span> <span data-ttu-id="602c5-812">구체적으로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-812">Specifically:</span></span>
   * <span data-ttu-id="602c5-813">`S1` `sbyte` 하 고 `S2` 됩니다 `byte`, `ushort`, `uint`, 또는 `ulong`</span><span class="sxs-lookup"><span data-stu-id="602c5-813">`S1` is `sbyte` and `S2` is `byte`, `ushort`, `uint`, or `ulong`</span></span>
   * <span data-ttu-id="602c5-814">`S1` `short` 하 고 `S2` 됩니다 `ushort`, `uint`, 또는 `ulong`</span><span class="sxs-lookup"><span data-stu-id="602c5-814">`S1` is `short` and `S2` is `ushort`, `uint`, or `ulong`</span></span>
   * <span data-ttu-id="602c5-815">`S1` 됩니다 `int` 하 고 `S2` 는 `uint`, 또는 `ulong`</span><span class="sxs-lookup"><span data-stu-id="602c5-815">`S1` is `int` and `S2` is `uint`, or `ulong`</span></span>
   * <span data-ttu-id="602c5-816">`S1` 됩니다 `long` 고 `S2` 됩니다 `ulong`</span><span class="sxs-lookup"><span data-stu-id="602c5-816">`S1` is `long` and `S2` is `ulong`</span></span>

#### <a name="overloading-in-generic-classes"></a><span data-ttu-id="602c5-817">제네릭 클래스에서 오버 로드</span><span class="sxs-lookup"><span data-stu-id="602c5-817">Overloading in generic classes</span></span>

<span data-ttu-id="602c5-818">선언 된 서명이 고유 해야 하는 동안 가능성이 동일한 서명에서 형식 인수는 대체 결과 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-818">While signatures as declared must be unique, it is possible that substitution of type arguments results in identical signatures.</span></span> <span data-ttu-id="602c5-819">이러한 경우에 동률 주요 규칙 위의 오버 로드 확인에는 대부분의 특정 멤버를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-819">In such cases, the tie-breaking rules of overload resolution above will pick the most specific member.</span></span>

<span data-ttu-id="602c5-820">다음 예에서는 유효 하 고이 규칙에 따라 잘못 된 오버 로드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-820">The following examples show overloads that are valid and invalid according to this rule:</span></span>

```csharp
interface I1<T> {...}

interface I2<T> {...}

class G1<U>
{
    int F1(U u);                  // Overload resolution for G<int>.F1
    int F1(int i);                // will pick non-generic

    void F2(I1<U> a);             // Valid overload
    void F2(I2<U> a);
}

class G2<U,V>
{
    void F3(U u, V v);            // Valid, but overload resolution for
    void F3(V v, U u);            // G2<int,int>.F3 will fail

    void F4(U u, I1<V> v);        // Valid, but overload resolution for    
    void F4(I1<V> v, U u);        // G2<I1<int>,int>.F4 will fail

    void F5(U u1, I1<V> v2);      // Valid overload
    void F5(V v1, U u2);

    void F6(ref U u);             // valid overload
    void F6(out V v);
}
```

### <a name="compile-time-checking-of-dynamic-overload-resolution"></a><span data-ttu-id="602c5-821">컴파일 타임 검사 동적 오버 로드 확인</span><span class="sxs-lookup"><span data-stu-id="602c5-821">Compile-time checking of dynamic overload resolution</span></span>

<span data-ttu-id="602c5-822">대부분 동적으로 바인딩된 작업에 대 한 해결 방법에 대 한 가능한 후보 집합이 컴파일 타임에 알려진 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-822">For most dynamically bound operations the set of possible candidates for resolution is unknown at compile-time.</span></span> <span data-ttu-id="602c5-823">그러나 경우에 따라 후보 집합이 컴파일 타임에 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-823">In certain cases, however the candidate set is known at compile-time:</span></span>

*  <span data-ttu-id="602c5-824">동적 인수를 사용 하 여 정적 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="602c5-824">Static method calls with dynamic arguments</span></span>
*  <span data-ttu-id="602c5-825">수신자가 동적 식이 아닌 인스턴스 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="602c5-825">Instance method calls where the receiver is not a dynamic expression</span></span>
*  <span data-ttu-id="602c5-826">인덱서 호출 수신자가 동적 식이 아닌</span><span class="sxs-lookup"><span data-stu-id="602c5-826">Indexer calls where the receiver is not a dynamic expression</span></span>
*  <span data-ttu-id="602c5-827">동적 인수를 사용 하 여 생성자 호출</span><span class="sxs-lookup"><span data-stu-id="602c5-827">Constructor calls with dynamic arguments</span></span>

<span data-ttu-id="602c5-828">이러한 경우 경우 고 가능한 경우 적용할 수 런타임 시 확인 하려면 각 후보에 대 한 제한 된 컴파일 타임 검사를 수행 됩니다. 이 검사는 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-828">In these cases a limited compile-time check is performed for each candidate to see if any of them could possibly apply at run-time.This check consists of the following steps:</span></span>

*  <span data-ttu-id="602c5-829">부분 형식 유추: 모든 형식 인수 형식의 인수에 직접 또는 간접적으로 종속 되지 않습니다 `dynamic` 의 규칙을 사용 하 여 유추 [형식 유추](expressions.md#type-inference)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-829">Partial type inference: Any type argument that does not depend directly or indirectly on an argument of type `dynamic` is inferred using the rules of [Type inference](expressions.md#type-inference).</span></span> <span data-ttu-id="602c5-830">알 수 없는 나머지 형식 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-830">The remaining type arguments are unknown.</span></span>
*  <span data-ttu-id="602c5-831">부분 적용 가능성 확인: 적용 가능성에 따라 확인란이 [적용 가능한 함수 멤버](expressions.md#applicable-function-member)에 형식이 알려지지 않은 매개 변수는 무시 되지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-831">Partial applicability check: Applicability is checked according to [Applicable function member](expressions.md#applicable-function-member), but ignoring parameters whose types are unknown.</span></span>
*  <span data-ttu-id="602c5-832">없는 후보가이 테스트를 통과 하는 경우 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-832">If no candidate passes this test, a compile-time error occurs.</span></span>

### <a name="function-member-invocation"></a><span data-ttu-id="602c5-833">함수 멤버 호출</span><span class="sxs-lookup"><span data-stu-id="602c5-833">Function member invocation</span></span>

<span data-ttu-id="602c5-834">이 섹션에서는 특정 함수 멤버를 호출 하려면 런타임 시 발생 하는 프로세스를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-834">This section describes the process that takes place at run-time to invoke a particular function member.</span></span> <span data-ttu-id="602c5-835">바인딩 시간 프로세스 호출, 가능한 경우 적용 하 여 오버 로드 확인 후보 함수 멤버 집합에 특정 멤버를 이미 결정에 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-835">It is assumed that a binding-time process has already determined the particular member to invoke, possibly by applying overload resolution to a set of candidate function members.</span></span>

<span data-ttu-id="602c5-836">호출 프로세스를 설명 하는 용도로 함수 멤버 두 범주로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-836">For purposes of describing the invocation process, function members are divided into two categories:</span></span>

*  <span data-ttu-id="602c5-837">정적 함수 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-837">Static function members.</span></span> <span data-ttu-id="602c5-838">이들은, 인스턴스 생성자, 정적 메서드를 정적 속성 접근자 및 사용자 정의 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-838">These are instance constructors, static methods, static property accessors, and user-defined operators.</span></span> <span data-ttu-id="602c5-839">정적 함수 멤버는 항상 가상입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-839">Static function members are always non-virtual.</span></span>
*  <span data-ttu-id="602c5-840">인스턴스 함수 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-840">Instance function members.</span></span> <span data-ttu-id="602c5-841">이들은, 인스턴스 메서드, 인스턴스 속성 접근자 및 인덱서 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-841">These are instance methods, instance property accessors, and indexer accessors.</span></span> <span data-ttu-id="602c5-842">인스턴스 함수 멤버 비가상 이거나 가상 되며 특정 인스턴스에서 항상 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-842">Instance function members are either non-virtual or virtual, and are always invoked on a particular instance.</span></span> <span data-ttu-id="602c5-843">인스턴스를 인스턴스 식에서 계산 되 고으로 함수 멤버에 액세스할 수 있습니다 `this` ([이 액세스](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="602c5-843">The instance is computed by an instance expression, and it becomes accessible within the function member as `this` ([This access](expressions.md#this-access)).</span></span>

<span data-ttu-id="602c5-844">멤버 함수 호출의 런타임 처리는 다음 단계로 구성 됩니다 여기서 `M` 함수 멤버인 경우 `M` 는 인스턴스 멤버 `E` 인스턴스 식:</span><span class="sxs-lookup"><span data-stu-id="602c5-844">The run-time processing of a function member invocation consists of the following steps, where `M` is the function member and, if `M` is an instance member, `E` is the instance expression:</span></span>

*  <span data-ttu-id="602c5-845">경우 `M` 멤버인 정적 함수:</span><span class="sxs-lookup"><span data-stu-id="602c5-845">If `M` is a static function member:</span></span>
   * <span data-ttu-id="602c5-846">인수 목록에 설명 된 대로 평가 됩니다 [인수 목록](expressions.md#argument-lists)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-846">The argument list is evaluated as described in [Argument lists](expressions.md#argument-lists).</span></span>
   * <span data-ttu-id="602c5-847">`M` 가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-847">`M` is invoked.</span></span>

*  <span data-ttu-id="602c5-848">하는 경우 `M` 인스턴스 함수 멤버에 선언 된 *value_type*:</span><span class="sxs-lookup"><span data-stu-id="602c5-848">If `M` is an instance function member declared in a *value_type*:</span></span>
   * <span data-ttu-id="602c5-849">`E` 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-849">`E` is evaluated.</span></span> <span data-ttu-id="602c5-850">이 평가 예외를 발생 시키는 경우에 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-850">If this evaluation causes an exception, then no further steps are executed.</span></span>
   * <span data-ttu-id="602c5-851">하는 경우 `E` 변수를 다음의 임시 로컬 변수로 분류 되지 않은 `E`의 형식을 만들 값 `E` 해당 변수에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-851">If `E` is not classified as a variable, then a temporary local variable of `E`'s type is created and the value of `E` is assigned to that variable.</span></span> <span data-ttu-id="602c5-852">`E` 해당 임시 지역 변수에 대 한 참조로 다시 다음 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-852">`E` is then reclassified as a reference to that temporary local variable.</span></span> <span data-ttu-id="602c5-853">임시 변수가로 액세스할 수 있습니다 `this` 내에서 `M`에 있지만 다른 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-853">The temporary variable is accessible as `this` within `M`, but not in any other way.</span></span> <span data-ttu-id="602c5-854">경우에 따라서만 `E` true 변수는 호출자가 변경 내용을 관찰할 수 있는 `M` 게 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-854">Thus, only when `E` is a true variable is it possible for the caller to observe the changes that `M` makes to `this`.</span></span>
   * <span data-ttu-id="602c5-855">인수 목록에 설명 된 대로 평가 됩니다 [인수 목록](expressions.md#argument-lists)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-855">The argument list is evaluated as described in [Argument lists](expressions.md#argument-lists).</span></span>
   * <span data-ttu-id="602c5-856">`M` 가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-856">`M` is invoked.</span></span> <span data-ttu-id="602c5-857">참조 변수의 `E` 변수에서 참조 됩니다 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-857">The variable referenced by `E` becomes the variable referenced by `this`.</span></span>

*  <span data-ttu-id="602c5-858">하는 경우 `M` 인스턴스 함수 멤버에 선언 된 *reference_type*:</span><span class="sxs-lookup"><span data-stu-id="602c5-858">If `M` is an instance function member declared in a *reference_type*:</span></span>
   * <span data-ttu-id="602c5-859">`E` 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-859">`E` is evaluated.</span></span> <span data-ttu-id="602c5-860">이 평가 예외를 발생 시키는 경우에 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-860">If this evaluation causes an exception, then no further steps are executed.</span></span>
   * <span data-ttu-id="602c5-861">인수 목록에 설명 된 대로 평가 됩니다 [인수 목록](expressions.md#argument-lists)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-861">The argument list is evaluated as described in [Argument lists](expressions.md#argument-lists).</span></span>
   * <span data-ttu-id="602c5-862">경우 형식의 `E` 되는 *value_type*, boxing 변환 ([Boxing 변환](types.md#boxing-conversions)) 변환 하기 위해 수행 됩니다 `E` 형식으로 `object`, 및 `E` 것으로 간주 됩니다 형식의 `object` 다음 단계에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-862">If the type of `E` is a *value_type*, a boxing conversion ([Boxing conversions](types.md#boxing-conversions)) is performed to convert `E` to type `object`, and `E` is considered to be of type `object` in the following steps.</span></span> <span data-ttu-id="602c5-863">이 예에서 `M` 의 멤버일 수만 있습니다 `System.Object`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-863">In this case, `M` could only be a member of `System.Object`.</span></span>
   * <span data-ttu-id="602c5-864">변수의 `E` 유효한 것으로 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-864">The value of `E` is checked to be valid.</span></span> <span data-ttu-id="602c5-865">경우 값 `E` 은 `null`, `System.NullReferenceException` throw 되 고 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-865">If the value of `E` is `null`, a `System.NullReferenceException` is thrown and no further steps are executed.</span></span>
   * <span data-ttu-id="602c5-866">호출 하는 함수 멤버 구현은 다음과 같이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-866">The function member implementation to invoke is determined:</span></span>
     * <span data-ttu-id="602c5-867">에 바인딩 형식이 `E` 인터페이스를 호출 하는 함수 멤버의 구현인 `M` 에서 참조 하는 인스턴스의 런타임 형식에서 제공 `E`.</span><span class="sxs-lookup"><span data-stu-id="602c5-867">If the binding-time type of `E` is an interface, the function member to invoke is the implementation of `M` provided by the run-time type of the instance referenced by `E`.</span></span> <span data-ttu-id="602c5-868">이 함수 멤버 인터페이스 매핑 규칙을 적용 하 여 결정 됩니다 ([인터페이스 매핑을](interfaces.md#interface-mapping)) 구현의 결정할 `M` 런타임 형식에서 참조 하는 인스턴스의 제공한 `E`.</span><span class="sxs-lookup"><span data-stu-id="602c5-868">This function member is determined by applying the interface mapping rules ([Interface mapping](interfaces.md#interface-mapping)) to determine the implementation of `M` provided by the run-time type of the instance referenced by `E`.</span></span>
     * <span data-ttu-id="602c5-869">그렇지 않은 경우, `M` 멤버인 가상 함수를 호출 하는 함수 멤버의 구현인 `M` 에서 참조 하는 인스턴스의 런타임 형식에서 제공 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-869">Otherwise, if `M` is a virtual function member, the function member to invoke is the implementation of `M` provided by the run-time type of the instance referenced by `E`.</span></span> <span data-ttu-id="602c5-870">이 함수 멤버는 가장 많이 파생 된 구현 결정 하는 것에 대 한 규칙을 적용 하 여 결정 됩니다 ([가상 메서드](classes.md#virtual-methods))의 `M` 런타임 형식에서 참조 하는 인스턴스의 관련 하 여 `E`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-870">This function member is determined by applying the rules for determining the most derived implementation ([Virtual methods](classes.md#virtual-methods)) of `M` with respect to the run-time type of the instance referenced by `E`.</span></span>
     * <span data-ttu-id="602c5-871">그렇지 않으면 `M` 비가상 함수 멤버 이며를 호출 하는 함수 멤버 `M` 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-871">Otherwise, `M` is a non-virtual function member, and the function member to invoke is `M` itself.</span></span>
   * <span data-ttu-id="602c5-872">위의 단계에서 결정 함수 멤버 구현이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-872">The function member implementation determined in the step above is invoked.</span></span> <span data-ttu-id="602c5-873">참조 하는 개체가 `E` 가 참조 하는 개체가 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-873">The object referenced by `E` becomes the object referenced by `this`.</span></span>

#### <a name="invocations-on-boxed-instances"></a><span data-ttu-id="602c5-874">Boxed 인스턴스에서 호출</span><span class="sxs-lookup"><span data-stu-id="602c5-874">Invocations on boxed instances</span></span>

<span data-ttu-id="602c5-875">구현 되는 함수 멤버를 *value_type* 의 boxed 인스턴스를 통해 호출할 수 있습니다 *value_type* 다음과 같은 경우에서:</span><span class="sxs-lookup"><span data-stu-id="602c5-875">A function member implemented in a *value_type* can be invoked through a boxed instance of that *value_type* in the following situations:</span></span>

*  <span data-ttu-id="602c5-876">함수 멤버의 경우는 `override` 형식에서 상속 된 메서드 `object` 형식의 인스턴스 식을 통해 호출 되 고 `object`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-876">When the function member is an `override` of a method inherited from type `object` and is invoked through an instance expression of type `object`.</span></span>
*  <span data-ttu-id="602c5-877">함수 멤버 인터페이스 함수 멤버의 구현인 시점과의 인스턴스 식을 통해 호출 되는 *interface_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-877">When the function member is an implementation of an interface function member and is invoked through an instance expression of an *interface_type*.</span></span>
*  <span data-ttu-id="602c5-878">대리자를 통해 함수 멤버를 호출할 때 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-878">When the function member is invoked through a delegate.</span></span>

<span data-ttu-id="602c5-879">이러한 상황에서는 boxed 인스턴스 변수를 포함할 것으로 간주 합니다 *value_type*,이 변수에서 참조 하는 변수가 되며 `this` 함수 멤버 호출 내에서.</span><span class="sxs-lookup"><span data-stu-id="602c5-879">In these situations, the boxed instance is considered to contain a variable of the *value_type*, and this variable becomes the variable referenced by `this` within the function member invocation.</span></span> <span data-ttu-id="602c5-880">특히,이 함수 멤버 boxed 인스턴스에서 호출 되 면 수 있다는 것 boxed 인스턴스에 포함 된 값을 수정 하는 함수 멤버에 대 한 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-880">In particular, this means that when a function member is invoked on a boxed instance, it is possible for the function member to modify the value contained in the boxed instance.</span></span>

## <a name="primary-expressions"></a><span data-ttu-id="602c5-881">기본 식</span><span class="sxs-lookup"><span data-stu-id="602c5-881">Primary expressions</span></span>

<span data-ttu-id="602c5-882">기본 식에는 가장 간단한 형태의 식 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-882">Primary expressions include the simplest forms of expressions.</span></span>

```antlr
primary_expression
    : primary_no_array_creation_expression
    | array_creation_expression
    ;

primary_no_array_creation_expression
    : literal
    | interpolated_string_expression
    | simple_name
    | parenthesized_expression
    | member_access
    | invocation_expression
    | element_access
    | this_access
    | base_access
    | post_increment_expression
    | post_decrement_expression
    | object_creation_expression
    | delegate_creation_expression
    | anonymous_object_creation_expression
    | typeof_expression
    | checked_expression
    | unchecked_expression
    | default_value_expression
    | nameof_expression
    | anonymous_method_expression
    | primary_no_array_creation_expression_unsafe
    ;
```

<span data-ttu-id="602c5-883">기본 식 간에 나뉩니다 *array_creation_expression*s 및 *primary_no_array_creation_expression*s입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-883">Primary expressions are divided between *array_creation_expression*s and *primary_no_array_creation_expression*s.</span></span> <span data-ttu-id="602c5-884">이 방식으로 배열 만들기 식 처리, 다른 간단한 식 형태와 함께 나열 하는 대신 사용 하면와 같은 잠재적으로 혼란 스러운 코드를 허용 하지 않도록 문법</span><span class="sxs-lookup"><span data-stu-id="602c5-884">Treating array-creation-expression in this way, rather than listing it along with the other simple expression forms, enables the grammar to disallow potentially confusing code such as</span></span>
```csharp
object o = new int[3][1];
```
<span data-ttu-id="602c5-885">하는 것으로 해석 될</span><span class="sxs-lookup"><span data-stu-id="602c5-885">which would otherwise be interpreted as</span></span>
```csharp
object o = (new int[3])[1];
```

### <a name="literals"></a><span data-ttu-id="602c5-886">리터럴</span><span class="sxs-lookup"><span data-stu-id="602c5-886">Literals</span></span>

<span data-ttu-id="602c5-887">A *primary_expression* 으로 구성 된를 *리터럴* ([리터럴](lexical-structure.md#literals)) 값으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-887">A *primary_expression* that consists of a *literal* ([Literals](lexical-structure.md#literals)) is classified as a value.</span></span>


### <a name="interpolated-strings"></a><span data-ttu-id="602c5-888">보간된 문자열</span><span class="sxs-lookup"><span data-stu-id="602c5-888">Interpolated strings</span></span>

<span data-ttu-id="602c5-889">*interpolated_string_expression* 이루어져를 `$` 여기서 구멍을 구분 기호 뒤에 정기적으로 또는 축 자 문자열 리터럴 `{` 및 `}`, 식 및 서식 지정 사양입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-889">An *interpolated_string_expression* consists of a `$` sign followed by a regular or verbatim string literal, wherein holes, delimited by `{` and `}`, enclose expressions and formatting specifications.</span></span> <span data-ttu-id="602c5-890">보간된 문자열 식의 결과인를 *interpolated_string_literal* 는 분할 된 개별 토큰에에 설명 된 대로 [보간된 문자열 리터럴을](lexical-structure.md#interpolated-string-literals)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-890">An interpolated string expression is the result of an *interpolated_string_literal* that has been broken up into individual tokens, as described in [Interpolated string literals](lexical-structure.md#interpolated-string-literals).</span></span>

```antlr
interpolated_string_expression
    : '$' interpolated_regular_string
    | '$' interpolated_verbatim_string
    ;

interpolated_regular_string
    : interpolated_regular_string_whole
    | interpolated_regular_string_start interpolated_regular_string_body interpolated_regular_string_end
    ;

interpolated_regular_string_body
    : interpolation (interpolated_regular_string_mid interpolation)*
    ;

interpolation
    : expression
    | expression ',' constant_expression
    ;

interpolated_verbatim_string
    : interpolated_verbatim_string_whole
    | interpolated_verbatim_string_start interpolated_verbatim_string_body interpolated_verbatim_string_end
    ;

interpolated_verbatim_string_body
    : interpolation (interpolated_verbatim_string_mid interpolation)+
    ;
```

<span data-ttu-id="602c5-891">합니다 *constant_expression* 보간을으로 암시적 변환이 있어야 합니다 `int`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-891">The *constant_expression* in an interpolation must have an implicit conversion to `int`.</span></span>

<span data-ttu-id="602c5-892">*interpolated_string_expression* 값으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-892">An *interpolated_string_expression* is classified as a value.</span></span> <span data-ttu-id="602c5-893">즉시 변환할 경우 `System.IFormattable` 또는 `System.FormattableString` 변환 하는 보간된 문자열의 암시적 변환을 사용 하 여 ([암시적 보간된 문자열 변환](conversions.md#implicit-interpolated-string-conversions)), 보간된 문자열 식은 해당 형식이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-893">If it is immediately converted to `System.IFormattable` or `System.FormattableString` with an implicit interpolated string conversion ([Implicit interpolated string conversions](conversions.md#implicit-interpolated-string-conversions)), the interpolated string expression has that type.</span></span> <span data-ttu-id="602c5-894">형식 그러지 `string`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-894">Otherwise, it has the type `string`.</span></span>

<span data-ttu-id="602c5-895">보간된 문자열의 형식이 `System.IFormattable` 또는 `System.FormattableString`, 의미에 대 한 호출을는 `System.Runtime.CompilerServices.FormattableStringFactory.Create`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-895">If the type of an interpolated string is `System.IFormattable` or `System.FormattableString`, the meaning is a call to `System.Runtime.CompilerServices.FormattableStringFactory.Create`.</span></span> <span data-ttu-id="602c5-896">형식이 `string`, 식의 의미는 호출 `string.Format`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-896">If the type is `string`, the meaning of the expression is a call to `string.Format`.</span></span> <span data-ttu-id="602c5-897">두 경우 모두 호출의 인수 목록 형식 문자열 리터럴을 각 보간에 대 한 자리 표시자 및 자리 표시자를 해당 하는 각 식에 대 한 인수로 사용 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-897">In both cases, the argument list of the call consists of a format string literal with placeholders for each interpolation, and an argument for each expression corresponding to the place holders.</span></span>

<span data-ttu-id="602c5-898">형식 문자열 리터럴을 다음과 같이 생성 된 위치 `N` 보간의 수를 *interpolated_string_expression*:</span><span class="sxs-lookup"><span data-stu-id="602c5-898">The format string literal is constructed as follows, where `N` is the number of interpolations in the *interpolated_string_expression*:</span></span>

*  <span data-ttu-id="602c5-899">경우는 *interpolated_regular_string_whole* 요소나 *interpolated_verbatim_string_whole* 따릅니다는 `$` 형식 문자열 리터럴에 해당 토큰에 서명.</span><span class="sxs-lookup"><span data-stu-id="602c5-899">If an *interpolated_regular_string_whole* or an *interpolated_verbatim_string_whole* follows the `$` sign, then the format string literal is that token.</span></span>
*  <span data-ttu-id="602c5-900">그렇지 않은 경우 형식 문자열 리터럴을 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-900">Otherwise, the format string literal consists of:</span></span> 
   *  <span data-ttu-id="602c5-901">첫 번째는 *interpolated_regular_string_start* 또는 *interpolated_verbatim_string_start*</span><span class="sxs-lookup"><span data-stu-id="602c5-901">First the *interpolated_regular_string_start* or *interpolated_verbatim_string_start*</span></span>
   *  <span data-ttu-id="602c5-902">각 숫자에 대 한 다음 `I` 에서 `0` 에 `N-1`:</span><span class="sxs-lookup"><span data-stu-id="602c5-902">Then for each number `I` from `0` to `N-1`:</span></span> 
      * <span data-ttu-id="602c5-903">소수 표현 `I`</span><span class="sxs-lookup"><span data-stu-id="602c5-903">The decimal representation of `I`</span></span>
      * <span data-ttu-id="602c5-904">그런 다음 해당 *보간* 에 *constant_expression*, `,` 값의 소수 표현 뒤에 (쉼표)를 *constant_expression*</span><span class="sxs-lookup"><span data-stu-id="602c5-904">Then, if the corresponding *interpolation* has a *constant_expression*, a `,` (comma) followed by the decimal representation of the value of the *constant_expression*</span></span>
      * <span data-ttu-id="602c5-905">그런 다음 *interpolated_regular_string_mid*를 *interpolated_regular_string_end*하십시오 *interpolated_verbatim_string_mid* 또는 *interpolated_ verbatim_string_end* 즉시 해당 보간을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-905">Then the *interpolated_regular_string_mid*, *interpolated_regular_string_end*, *interpolated_verbatim_string_mid* or *interpolated_verbatim_string_end* immediately following the corresponding interpolation.</span></span>

<span data-ttu-id="602c5-906">이후 인수는 단순히 합니다 *식* 에서 합니다 *보간* (있는 경우), 순서로.</span><span class="sxs-lookup"><span data-stu-id="602c5-906">The subsequent arguments are simply the *expressions* from the *interpolations* (if any), in order.</span></span>

<span data-ttu-id="602c5-907">TODO: 예.</span><span class="sxs-lookup"><span data-stu-id="602c5-907">TODO: examples.</span></span>


### <a name="simple-names"></a><span data-ttu-id="602c5-908">단순 이름</span><span class="sxs-lookup"><span data-stu-id="602c5-908">Simple names</span></span>

<span data-ttu-id="602c5-909">A *simple_name* 식별자 형식 인수 목록 뒤에 선택적으로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-909">A *simple_name* consists of an identifier, optionally followed by a type argument list:</span></span>

```antlr
simple_name
    : identifier type_argument_list?
    ;
```

<span data-ttu-id="602c5-910">A *simple_name* 형식 중 하나는 `I` 또는 양식의 `I<A1,...,Ak>`여기서 `I` 는 단일 식별자 및 `<A1,...,Ak>` 선택적 *type_argument_list*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-910">A *simple_name* is either of the form `I` or of the form `I<A1,...,Ak>`, where `I` is a single identifier and `<A1,...,Ak>` is an optional *type_argument_list*.</span></span> <span data-ttu-id="602c5-911">없는 경우 *type_argument_list* 가 지정 하는 것이 좋습니다 `K` 0입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-911">When no *type_argument_list* is specified, consider `K` to be zero.</span></span> <span data-ttu-id="602c5-912">합니다 *simple_name* 평가 되 고 다음과 같이 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-912">The *simple_name* is evaluated and classified as follows:</span></span>

*  <span data-ttu-id="602c5-913">경우 `K` 가 0 및 *simple_name* 내에 표시 되는 *블록* 경우에 *블록*의 (바깥쪽 또는 *블록*의) 로컬 변수 선언 공간 ([선언](basic-concepts.md#declarations)) 로컬 변수, 매개 변수 또는 상수 이름이 포함 `I`, 해당 *simple_name* 해당 로컬 변수 참조 매개 변수 또는 상수와 변수 또는 값으로 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-913">If `K` is zero and the *simple_name* appears within a *block* and if the *block*'s (or an enclosing *block*'s) local variable declaration space ([Declarations](basic-concepts.md#declarations)) contains a local variable, parameter or constant with name `I`, then the *simple_name* refers to that local variable, parameter or constant and is classified as a variable or value.</span></span>
*  <span data-ttu-id="602c5-914">경우 `K` 0 및 *simple_name* 제네릭 메서드 선언의 본문 내에 표시 및 해당 선언 이름의 형식 매개 변수를 포함 하는 경우 `I`, 그런 다음 *simple_name*해당 형식 매개 변수를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-914">If `K` is zero and the *simple_name* appears within the body of a generic method declaration and if that declaration includes a type parameter with name `I`, then the *simple_name* refers to that type parameter.</span></span>
*  <span data-ttu-id="602c5-915">각 인스턴스 유형에 대해이 고, 그렇지 `T` ([인스턴스 유형을](classes.md#the-instance-type)), 바로 바깥쪽 형식 선언의 인스턴스 형식을 사용 하 여 시작 하 고 각 바깥쪽 클래스 또는 구조체의 인스턴스 형식을 사용 하 여 계속 합니다. 선언 (있는 경우):</span><span class="sxs-lookup"><span data-stu-id="602c5-915">Otherwise, for each instance type `T` ([The instance type](classes.md#the-instance-type)), starting with the instance type of the immediately enclosing type declaration and continuing with the instance type of each enclosing class or struct declaration (if any):</span></span>
   *  <span data-ttu-id="602c5-916">하는 경우 `K` 0 이며 선언의 `T` 이름의 형식 매개 변수가 포함 `I`, 해당 *simple_name* 해당 형식 매개 변수를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-916">If `K` is zero and the declaration of `T` includes a type parameter with name `I`, then the *simple_name* refers to that type parameter.</span></span>
   *  <span data-ttu-id="602c5-917">그렇지 않고 멤버 조회 ([멤버 조회](expressions.md#member-lookup))의 `I` 에서 `T` 사용 하 여 `K` 일치 하는 항목을 생성 하는 형식 인수:</span><span class="sxs-lookup"><span data-stu-id="602c5-917">Otherwise, if a member lookup ([Member lookup](expressions.md#member-lookup)) of `I` in `T` with `K` type arguments produces a match:</span></span>
      * <span data-ttu-id="602c5-918">하는 경우 `T` 가 바로 바깥쪽 클래스 또는 구조체 형식의 인스턴스 유형 및 조회 하나를 식별 합니다. 또는 이상의 메서드를 결과 메서드 그룹의 연결 된 인스턴스 식이 있는 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-918">If `T` is the instance type of the immediately enclosing class or struct type and the lookup identifies one or more methods, the result is a method group with an associated instance expression of `this`.</span></span> <span data-ttu-id="602c5-919">제네릭 메서드를 호출할 때 사용 되는 형식 인수 목록을 지정 하는 경우 ([메서드 호출](expressions.md#method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="602c5-919">If a type argument list was specified, it is used in calling a generic method ([Method invocations](expressions.md#method-invocations)).</span></span>
      * <span data-ttu-id="602c5-920">그렇지 않은 경우, `T` 이며 바로 바깥쪽 클래스 또는 구조체 형식의 인스턴스 유형을 조회 인스턴스 멤버를 식별 하는 경우 참조는 인스턴스 생성자, 인스턴스 메서드 또는 인스턴스 접근자의 본문 내에서 발생 하는 경우는 결과 멤버 액세스가와 같습니다 ([me](expressions.md#member-access)) 형식의 `this.I`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-920">Otherwise, if `T` is the instance type of the immediately enclosing class or struct type, if the lookup identifies an instance member, and if the reference occurs within the body of an instance constructor, an instance method, or an instance accessor, the result is the same as a member access ([Member access](expressions.md#member-access)) of the form `this.I`.</span></span> <span data-ttu-id="602c5-921">만 발생할 수 있습니다 때 `K` 은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-921">This can only happen when `K` is zero.</span></span>
      * <span data-ttu-id="602c5-922">그렇지 않으면 결과 멤버 액세스와 동일 ([me](expressions.md#member-access)) 형식의 `T.I` 또는 `T.I<A1,...,Ak>`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-922">Otherwise, the result is the same as a member access ([Member access](expressions.md#member-access)) of the form `T.I` or `T.I<A1,...,Ak>`.</span></span> <span data-ttu-id="602c5-923">에 대 한 바인딩 시간 오류는 것이 경우에 *simple_name* 인스턴스 멤버를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-923">In this case, it is a binding-time error for the *simple_name* to refer to an instance member.</span></span>

*  <span data-ttu-id="602c5-924">각 네임 스페이스이 고, 그렇지 `N`네임 스페이스를 사용 하 여 시작 합니다 *simple_name* 발생 하는 다음 단계는 각 바깥쪽 네임 스페이스 (있는 경우) 및 전역 네임 스페이스를 사용 하 여 종료를 사용 하 여 계속 엔터티를 찾을 때까지 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-924">Otherwise, for each namespace `N`, starting with the namespace in which the *simple_name* occurs, continuing with each enclosing namespace (if any), and ending with the global namespace, the following steps are evaluated until an entity is located:</span></span>
   *  <span data-ttu-id="602c5-925">경우 `K` 가 0 및 `I` 네임 스페이스의 이름은 `N`, 다음:</span><span class="sxs-lookup"><span data-stu-id="602c5-925">If `K` is zero and `I` is the name of a namespace in `N`, then:</span></span>
      * <span data-ttu-id="602c5-926">경우 위치 위치는 *simple_name* 발생에 대 한 네임 스페이스 선언을 괄호로 묶여 `N` 네임 스페이스 선언을 포함 하는 *extern_alias_directive* 또는  *using_alias_directive* 이름을 연결 하는 `I` 형식 또는 네임 스페이스를 사용 하 여 해당 *simple_name* 모호 하 고 컴파일 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-926">If the location where the *simple_name* occurs is enclosed by a namespace declaration for `N` and the namespace declaration contains an *extern_alias_directive* or *using_alias_directive* that associates the name `I` with a namespace or type, then the *simple_name* is ambiguous and a compile-time error occurs.</span></span>
      * <span data-ttu-id="602c5-927">이 고, 그렇지 합니다 *simple_name* 라는 네임 스페이스 참조 `I` 에서 `N`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-927">Otherwise, the *simple_name* refers to the namespace named `I` in `N`.</span></span>
   *  <span data-ttu-id="602c5-928">그렇지 않은 경우, `N` 이름의 액세스할 수 있는 형식이 포함 되어 `I` 및 `K` 다음 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-928">Otherwise, if `N` contains an accessible type having name `I` and `K` type parameters, then:</span></span>
      * <span data-ttu-id="602c5-929">하는 경우 `K` 0 및 위치는 여기서는 *simple_name* 발생에 대 한 네임 스페이스 선언을 괄호로 묶여 `N` 네임 스페이스 선언을 포함 하 고는 *extern_alias_directive*또는 *using_alias_directive* 이름을 연결 하는 `I` 형식 또는 네임 스페이스를 사용 하 여 해당 *simple_name* 모호 하 고 컴파일 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-929">If `K` is zero and the location where the *simple_name* occurs is enclosed by a namespace declaration for `N` and the namespace declaration contains an *extern_alias_directive* or *using_alias_directive* that associates the name `I` with a namespace or type, then the *simple_name* is ambiguous and a compile-time error occurs.</span></span>
      * <span data-ttu-id="602c5-930">그렇지 않은 경우는 *namespace_or_type_name* 지정 된 형식 인수를 사용 하 여 생성 된 형식을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-930">Otherwise, the *namespace_or_type_name* refers to the type constructed with the given type arguments.</span></span>
   *  <span data-ttu-id="602c5-931">그렇지 않은 경우, 위치 여기서 합니다 *simple_name* 발생에 대 한 네임 스페이스 선언을 괄호로 묶여 `N`:</span><span class="sxs-lookup"><span data-stu-id="602c5-931">Otherwise, if the location where the *simple_name* occurs is enclosed by a namespace declaration for `N`:</span></span>
      * <span data-ttu-id="602c5-932">하는 경우 `K` 이 0이 고 네임 스페이스 선언에는 *extern_alias_directive* 또는 *using_alias_directive* 이름을 연결 하는 `I` 가져온된 네임 스페이스를 사용 하 여 또는 형식, 해당 *simple_name* 해당 네임 스페이스 또는 형식을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-932">If `K` is zero and the namespace declaration contains an *extern_alias_directive* or *using_alias_directive* that associates the name `I` with an imported namespace or type, then the *simple_name* refers to that namespace or type.</span></span>
      * <span data-ttu-id="602c5-933">네임 스페이스 및 형식 선언에서 가져온 경우는 *using_namespace_directive*s 및 *using_static_directive*네임 스페이스 선언 중 하나만 액세스할 수 있는 형식을 포함 하거나 에서 확장 되지 않은 정적 멤버 이름의 `I` 하 고 `K` 매개 변수를 입력 하면 *simple_name* 해당 형식 또는 지정 된 형식 인수를 사용 하 여 생성 하는 멤버를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-933">Otherwise, if the namespaces and type declarations imported by the *using_namespace_directive*s and *using_static_directive*s of the namespace declaration contain exactly one accessible type or non-extension static member having name `I` and `K` type parameters, then the *simple_name* refers to that type or member constructed with the given type arguments.</span></span>
      * <span data-ttu-id="602c5-934">가져온 네임 스페이스 및 형식 그러지 합니다 *using_namespace_directive*둘 이상의 액세스할 수 있는 형식을 또는 이름의 확장 메서드가 아닌 정적 멤버의 네임 스페이스 선언 포함 `I` 및`K` 매개 변수를 입력 하면 *simple_name* 모호 합니다. 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-934">Otherwise, if the namespaces and types imported by the *using_namespace_directive*s of the namespace declaration contain more than one accessible type or non-extension-method static member having name `I` and `K` type parameters, then the *simple_name* is ambiguous and an error occurs.</span></span>

   <span data-ttu-id="602c5-935">이 단계는 정확 하 게 병렬 처리 하는 단계는 해당 하는 *namespace_or_type_name* ([Namespace 및 형식 이름](basic-concepts.md#namespace-and-type-names)).</span><span class="sxs-lookup"><span data-stu-id="602c5-935">Note that this entire step is exactly parallel to the corresponding step in the processing of a *namespace_or_type_name* ([Namespace and type names](basic-concepts.md#namespace-and-type-names)).</span></span>

*  <span data-ttu-id="602c5-936">이 고, 그렇지 합니다 *simple_name* 가 정의 되지 않은 하 고 컴파일 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-936">Otherwise, the *simple_name* is undefined and a compile-time error occurs.</span></span>


### <a name="parenthesized-expressions"></a><span data-ttu-id="602c5-937">괄호로 묶인 식</span><span class="sxs-lookup"><span data-stu-id="602c5-937">Parenthesized expressions</span></span>

<span data-ttu-id="602c5-938">*parenthesized_expression* 이루어져는 *식* 괄호로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-938">A *parenthesized_expression* consists of an *expression* enclosed in parentheses.</span></span>

```antlr
parenthesized_expression
    : '(' expression ')'
    ;
```

<span data-ttu-id="602c5-939">A *parenthesized_expression* 평가 하 여 평가 되는 *식* 괄호 안에 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-939">A *parenthesized_expression* is evaluated by evaluating the *expression* within the parentheses.</span></span> <span data-ttu-id="602c5-940">경우는 *식* 괄호 안에 나타냅니다 네임 스페이스 또는 형식에는 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-940">If the *expression* within the parentheses denotes a namespace or type, a compile-time error occurs.</span></span> <span data-ttu-id="602c5-941">이 고, 그렇지의 결과 *parenthesized_expression* 포함된 된 계산의 결과인 *식*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-941">Otherwise, the result of the *parenthesized_expression* is the result of the evaluation of the contained *expression*.</span></span>

### <a name="member-access"></a><span data-ttu-id="602c5-942">멤버 액세스</span><span class="sxs-lookup"><span data-stu-id="602c5-942">Member access</span></span>

<span data-ttu-id="602c5-943">A *member_access* 이루어져 있습니다를 *primary_expression*, *predefined_type*, 또는 *qualified_alias_member*"뒤,`.`"토큰, 뒤에 *식별자*뒤에 선택적으로,는 *type_argument_list*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-943">A *member_access* consists of a *primary_expression*, a *predefined_type*, or a *qualified_alias_member*, followed by a "`.`" token, followed by an *identifier*, optionally followed by a *type_argument_list*.</span></span>

```antlr
member_access
    : primary_expression '.' identifier type_argument_list?
    | predefined_type '.' identifier type_argument_list?
    | qualified_alias_member '.' identifier
    ;

predefined_type
    : 'bool'   | 'byte'  | 'char'  | 'decimal' | 'double' | 'float' | 'int' | 'long'
    | 'object' | 'sbyte' | 'short' | 'string'  | 'uint'   | 'ulong' | 'ushort'
    ;
```

<span data-ttu-id="602c5-944">합니다 *qualified_alias_member* 프로덕션에 정의 된 [Namespace 별칭 한정자](namespaces.md#namespace-alias-qualifiers)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-944">The *qualified_alias_member* production is defined in [Namespace alias qualifiers](namespaces.md#namespace-alias-qualifiers).</span></span>

<span data-ttu-id="602c5-945">A *member_access* 형식 중 하나는 `E.I` 또는 양식의 `E.I<A1, ..., Ak>`여기서 `E` 은 기본 식 `I` 는 단일 식별자 및 `<A1, ..., Ak>` 선택적  *type_argument_list*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-945">A *member_access* is either of the form `E.I` or of the form `E.I<A1, ..., Ak>`, where `E` is a primary-expression, `I` is a single identifier and `<A1, ..., Ak>` is an optional *type_argument_list*.</span></span> <span data-ttu-id="602c5-946">없는 경우 *type_argument_list* 가 지정 하는 것이 좋습니다 `K` 0입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-946">When no *type_argument_list* is specified, consider `K` to be zero.</span></span>

<span data-ttu-id="602c5-947">A *member_access* 사용 하 여를 *primary_expression* 형식의 `dynamic` 동적으로 바인딩된 ([동적 바인딩](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="602c5-947">A *member_access* with a *primary_expression* of type `dynamic` is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="602c5-948">컴파일러가 형식의 속성 액세스로 멤버 액세스를 분류 하는 예제의 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-948">In this case the compiler classifies the member access as a property access of type `dynamic`.</span></span> <span data-ttu-id="602c5-949">의미를 확인 하려면 아래의 규칙 합니다 *member_access* 런타임의 컴파일 타임 형식 대신 런타임 형식 사용 시 적용 되는 *primary_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-949">The rules below to determine the meaning of the *member_access* are then applied at run-time, using the run-time type instead of the compile-time type of the *primary_expression*.</span></span> <span data-ttu-id="602c5-950">이 런타임 분류 메서드 그룹을 발생 시키는 경우 멤버 액세스 해야 합니다 *primary_expression* 의 *invocation_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-950">If this run-time classification leads to a method group, then the member access must be the *primary_expression* of an *invocation_expression*.</span></span>

<span data-ttu-id="602c5-951">합니다 *member_access* 평가 되 고 다음과 같이 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-951">The *member_access* is evaluated and classified as follows:</span></span>

*  <span data-ttu-id="602c5-952">하는 경우 `K` 가 0 및 `E` 네임 스페이스 및 `E` 이름의 중첩된 된 네임 스페이스를 포함 `I`, 결과 해당 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-952">If `K` is zero and `E` is a namespace and `E` contains a nested namespace with name `I`, then the result is that namespace.</span></span>
*  <span data-ttu-id="602c5-953">그렇지 `E` 네임 스페이스 및 `E` 이름의 액세스할 수 있는 형식이 포함 되어 `I` 및 `K` 결과 지정 된 형식 인수를 사용 하 여 생성 된 해당 형식 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-953">Otherwise, if `E` is a namespace and `E` contains an accessible type having name `I` and `K` type parameters, then the result is that type constructed with the given type arguments.</span></span>
*  <span data-ttu-id="602c5-954">경우 `E` 되는 *predefined_type* 또는 *primary_expression* 경우 형식으로 분류 `E` 형식 매개 변수가 아닌 경우 멤버 조회 ([멤버 조회](expressions.md#member-lookup)) `I` 에 `E` 사용 하 여 `K` 형식 매개 변수에 일치 하는 항목을 다음 생성 `E.I` 평가 되 고 다음과 같이 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-954">If `E` is a *predefined_type* or a *primary_expression* classified as a type, if `E` is not a type parameter, and if a member lookup ([Member lookup](expressions.md#member-lookup)) of `I` in `E` with `K` type parameters produces a match, then `E.I` is evaluated and classified as follows:</span></span>
   *  <span data-ttu-id="602c5-955">경우 `I` 결과 지정 된 형식 인수를 사용 하 여 생성 하는 형식임을 유형을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-955">If `I` identifies a type, then the result is that type constructed with the given type arguments.</span></span>
   *  <span data-ttu-id="602c5-956">경우 `I` 결과 연결 된 인스턴스 식이 없는 메서드 그룹을 하나 이상의 메서드를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-956">If `I` identifies one or more methods, then the result is a method group with no associated instance expression.</span></span> <span data-ttu-id="602c5-957">제네릭 메서드를 호출할 때 사용 되는 형식 인수 목록을 지정 하는 경우 ([메서드 호출](expressions.md#method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="602c5-957">If a type argument list was specified, it is used in calling a generic method ([Method invocations](expressions.md#method-invocations)).</span></span>
   *  <span data-ttu-id="602c5-958">경우 `I` 식별 하는 `static` 속성인 결과 연결 된 인스턴스 식이 없는 속성 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-958">If `I` identifies a `static` property, then the result is a property access with no associated instance expression.</span></span>
   *  <span data-ttu-id="602c5-959">하는 경우 `I` 식별 하는 `static` 필드:</span><span class="sxs-lookup"><span data-stu-id="602c5-959">If `I` identifies a `static` field:</span></span>
      * <span data-ttu-id="602c5-960">필드가 `readonly` 참조를 클래스 또는 구조체 필드 선언 되는 정적 생성자 외부에서 발생 하 고 결과 값, 즉 정적 필드의 값은 `I` 에서 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-960">If the field is `readonly` and the reference occurs outside the static constructor of the class or struct in which the field is declared, then the result is a value, namely the value of the static field `I` in `E`.</span></span>
      * <span data-ttu-id="602c5-961">결과 변수, 즉 정적 필드가 고, 그렇지 `I` 에서 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-961">Otherwise, the result is a variable, namely the static field `I` in `E`.</span></span>
   *  <span data-ttu-id="602c5-962">하는 경우 `I` 식별 하는 `static` 이벤트:</span><span class="sxs-lookup"><span data-stu-id="602c5-962">If `I` identifies a `static` event:</span></span>
      * <span data-ttu-id="602c5-963">참조를 클래스 또는 구조체는 이벤트 선언 되 고 없이 선언 된 이벤트 내에서 발생 하는 경우 *event_accessor_declarations* ([이벤트](classes.md#events)), 다음 `E.I` 정확 하 게 처리 처럼 `I` 된 정적 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-963">If the reference occurs within the class or struct in which the event is declared, and the event was declared without *event_accessor_declarations* ([Events](classes.md#events)), then `E.I` is processed exactly as if `I` were a static field.</span></span>
      * <span data-ttu-id="602c5-964">그렇지 않으면 연결 된 인스턴스 식이 없는 이벤트 액세스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-964">Otherwise, the result is an event access with no associated instance expression.</span></span>
   *  <span data-ttu-id="602c5-965">경우 `I` 결과 값, 즉 해당 상수 값을 사용 하는 상수를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-965">If `I` identifies a constant, then the result is a value, namely the value of that constant.</span></span>
    * <span data-ttu-id="602c5-966">경우 `I` 결과 값, 즉 해당 열거형 멤버의 값은 열거형 멤버를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-966">If `I` identifies an enumeration member, then the result is a value, namely the value of that enumeration member.</span></span>
    * <span data-ttu-id="602c5-967">그렇지 않으면 `E.I` 는 잘못 된 멤버 참조 이며 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-967">Otherwise, `E.I` is an invalid member reference, and a compile-time error occurs.</span></span>
*  <span data-ttu-id="602c5-968">하는 경우 `E` 속성 액세스, 인덱서 액세스, 변수 또는 값의 형식이 `T`, 및 멤버 조회 ([멤버 조회](expressions.md#member-lookup))의 `I` 에서 `T` 사용 하 여 `K` 형식 인수 그런 다음 일치 하는 항목을 생성 `E.I` 평가 되 고 다음과 같이 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-968">If `E` is a property access, indexer access, variable, or value, the type of which is `T`, and a member lookup ([Member lookup](expressions.md#member-lookup)) of `I` in `T` with `K` type arguments produces a match, then `E.I` is evaluated and classified as follows:</span></span>
   *  <span data-ttu-id="602c5-969">첫째, `E` 속성 또는 인덱서 액세스 속성의 값이 또는 인덱서 액세스 ([식의 값](expressions.md#values-of-expressions)) 및 `E` 는 값으로 다시 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-969">First, if `E` is a property or indexer access, then the value of the property or indexer access is obtained ([Values of expressions](expressions.md#values-of-expressions)) and `E` is reclassified as a value.</span></span>
   *  <span data-ttu-id="602c5-970">하는 경우 `I` 결과 메서드 그룹의 연결 된 인스턴스 식이 있는 하나 이상의 메서드를 식별 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-970">If `I` identifies one or more methods, then the result is a method group with an associated instance expression of `E`.</span></span> <span data-ttu-id="602c5-971">제네릭 메서드를 호출할 때 사용 되는 형식 인수 목록을 지정 하는 경우 ([메서드 호출](expressions.md#method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="602c5-971">If a type argument list was specified, it is used in calling a generic method ([Method invocations](expressions.md#method-invocations)).</span></span>
   *  <span data-ttu-id="602c5-972">경우 `I` 인스턴스 속성을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-972">If `I` identifies an instance property,</span></span>
      * <span data-ttu-id="602c5-973">경우 `E` 됩니다 `this`를 `I` 는 자동으로 구현 된 속성을 식별 ([자동으로 구현 된 속성](classes.md#automatically-implemented-properties)), setter 및 참조에 대 한 인스턴스 생성자 내에서 발생 하지 않고는 클래스 또는 구조체 형식인 `T`, 결과 변수, 즉 제공한 auto 속성에 대 한 숨겨진된 지원 필드 `I` 인스턴스의 `T` 여 `this`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-973">If `E` is `this`, `I` identifies an automatically implemented property ([Automatically implemented properties](classes.md#automatically-implemented-properties)) without a setter, and the reference occurs within an instance constructor for a class or struct type `T`, then the result is a variable, namely the hidden backing field for the auto-property given by `I` in the instance of `T` given by `this`.</span></span>
      * <span data-ttu-id="602c5-974">그렇지 않으면 결과 속성 액세스의 연결 된 인스턴스 식이 있는 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-974">Otherwise, the result is a property access with an associated instance expression of `E`.</span></span>
   *  <span data-ttu-id="602c5-975">경우 `T` 되는 *class_type* 및 `I` 식별 하는 인스턴스 필드 *class_type*:</span><span class="sxs-lookup"><span data-stu-id="602c5-975">If `T` is a *class_type* and `I` identifies an instance field of that *class_type*:</span></span>
      * <span data-ttu-id="602c5-976">경우 값 `E` 됩니다 `null`는 `System.NullReferenceException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-976">If the value of `E` is `null`, then a `System.NullReferenceException` is thrown.</span></span>
      * <span data-ttu-id="602c5-977">필드가 그러지 `readonly` 참조, 필드 선언 되는 클래스의 인스턴스 생성자 외부에서 발생 하 고 결과 값, 필드의 값 즉 `I` 참조 하는 개체에서 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-977">Otherwise, if the field is `readonly` and the reference occurs outside an instance constructor of the class in which the field is declared, then the result is a value, namely the value of the field `I` in the object referenced by `E`.</span></span>
      * <span data-ttu-id="602c5-978">결과 변수, 즉 필드가 고, 그렇지 `I` 에서 참조 하는 개체가 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-978">Otherwise, the result is a variable, namely the field `I` in the object referenced by `E`.</span></span>
   *  <span data-ttu-id="602c5-979">경우 `T` 되는 *struct_type* 및 `I` 식별 하는 인스턴스 필드 *struct_type*:</span><span class="sxs-lookup"><span data-stu-id="602c5-979">If `T` is a *struct_type* and `I` identifies an instance field of that *struct_type*:</span></span>
      * <span data-ttu-id="602c5-980">하는 경우 `E` 값인 경우 필드 이면 `readonly` 참조 필드 선언 되는 구조체의 인스턴스 생성자 외부에서 발생 하 고 결과 값, 필드의 값 즉 `I` 제공한 구조체 인스턴스 `E`.</span><span class="sxs-lookup"><span data-stu-id="602c5-980">If `E` is a value, or if the field is `readonly` and the reference occurs outside an instance constructor of the struct in which the field is declared, then the result is a value, namely the value of the field `I` in the struct instance given by `E`.</span></span>
      * <span data-ttu-id="602c5-981">결과 변수, 즉 필드가 고, 그렇지 `I` 제공한 구조체 인스턴스의 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-981">Otherwise, the result is a variable, namely the field `I` in the struct instance given by `E`.</span></span>
   *  <span data-ttu-id="602c5-982">경우 `I` 인스턴스 이벤트를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-982">If `I` identifies an instance event:</span></span>
      * <span data-ttu-id="602c5-983">참조를 클래스 또는 구조체는 이벤트 선언 되 고 없이 선언 된 이벤트 내에서 발생 하는 경우 *event_accessor_declarations* ([이벤트](classes.md#events)), 참조로 발생 하지 않습니다는 왼쪽에 있는 `+=` 또는 `-=` 연산자를 한 다음 `E.I` 정확 하 게 처리 됩니다 처럼 `I` 인스턴스 필드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-983">If the reference occurs within the class or struct in which the event is declared, and the event was declared without *event_accessor_declarations* ([Events](classes.md#events)), and the reference does not occur as the left-hand side of a `+=` or `-=` operator, then `E.I` is processed exactly as if `I` was an instance field.</span></span>
      * <span data-ttu-id="602c5-984">그렇지 않으면 결과의 연결 된 인스턴스 식이 있는 이벤트 액세스가 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-984">Otherwise, the result is an event access with an associated instance expression of `E`.</span></span>
*  <span data-ttu-id="602c5-985">처리 하려고 할이 고, 그렇지 `E.I` 확장 메서드 호출으로 ([확장 메서드 호출](expressions.md#extension-method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="602c5-985">Otherwise, an attempt is made to process `E.I` as an extension method invocation ([Extension method invocations](expressions.md#extension-method-invocations)).</span></span> <span data-ttu-id="602c5-986">이 작업이 실패 하면 `E.I` 는 잘못 된 멤버 참조 및 바인딩 시간에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-986">If this fails, `E.I` is an invalid member reference, and a binding-time error occurs.</span></span>

#### <a name="identical-simple-names-and-type-names"></a><span data-ttu-id="602c5-987">동일한 단순 이름 및 형식 이름</span><span class="sxs-lookup"><span data-stu-id="602c5-987">Identical simple names and type names</span></span>

<span data-ttu-id="602c5-988">형태의 멤버 액세스에서 `E.I`이면 `E` 는 단일 식별자 경우의 의미 `E` 으로 *simple_name* ([단순 이름](expressions.md#simple-names)) 상수, 필드, 속성 지역 변수 또는의 의미와 동일한 형식 매개 변수 `E` 으로 *type_name* ([Namespace 및 형식 이름](basic-concepts.md#namespace-and-type-names)), 다음의 두 가지 의미 `E` 됩니다 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-988">In a member access of the form `E.I`, if `E` is a single identifier, and if the meaning of `E` as a *simple_name* ([Simple names](expressions.md#simple-names)) is a constant, field, property, local variable, or parameter with the same type as the meaning of `E` as a *type_name* ([Namespace and type names](basic-concepts.md#namespace-and-type-names)), then both possible meanings of `E` are permitted.</span></span> <span data-ttu-id="602c5-989">두 가지 의미 `E.I` 는 이후 모호 하지 않습니다 `I` 형식의 멤버를 반드시 해야 `E` 두 경우 모두 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-989">The two possible meanings of `E.I` are never ambiguous, since `I` must necessarily be a member of the type `E` in both cases.</span></span> <span data-ttu-id="602c5-990">즉, 규칙 단순히 액세스를 허용 하 고 정적 멤버의 중첩된 형식 `E` 컴파일 시간 오류는이 고, 그렇지가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-990">In other words, the rule simply permits access to the static members and nested types of `E` where a compile-time error would otherwise have occurred.</span></span> <span data-ttu-id="602c5-991">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="602c5-991">For example:</span></span>
```csharp
struct Color
{
    public static readonly Color White = new Color(...);
    public static readonly Color Black = new Color(...);

    public Color Complement() {...}
}

class A
{
    public Color Color;                // Field Color of type Color

    void F() {
        Color = Color.Black;           // References Color.Black static member
        Color = Color.Complement();    // Invokes Complement() on Color field
    }

    static void G() {
        Color c = Color.White;         // References Color.White static member
    }
}
```

#### <a name="grammar-ambiguities"></a><span data-ttu-id="602c5-992">문법 모호성</span><span class="sxs-lookup"><span data-stu-id="602c5-992">Grammar ambiguities</span></span>

<span data-ttu-id="602c5-993">에 대 한 프로덕션 *simple_name* ([단순 이름](expressions.md#simple-names)) 및 *member_access* ([멤버 액세스](expressions.md#member-access))의 모호성을 낼 수 있습니다는 식 문법입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-993">The productions for *simple_name* ([Simple names](expressions.md#simple-names)) and *member_access* ([Member access](expressions.md#member-access)) can give rise to ambiguities in the grammar for expressions.</span></span> <span data-ttu-id="602c5-994">예를 들어 문:</span><span class="sxs-lookup"><span data-stu-id="602c5-994">For example, the statement:</span></span>
```
F(G<A,B>(7));
```
<span data-ttu-id="602c5-995">에 대 한 호출으로 해석 될 수 있었습니다 `F` 두 개의 인수를 사용 하 여 `G < A` 및 `B > (7)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-995">could be interpreted as a call to `F` with two arguments, `G < A` and `B > (7)`.</span></span> <span data-ttu-id="602c5-996">또는 호출으로 해석 될 수 있었습니다 `F` 제네릭 메서드를 호출은 하나의 인수를 사용 하 여 `G` 두 개의 형식 인수 및 일반 인수 하나를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-996">Alternatively, it could be interpreted as a call to `F` with one argument, which is a call to a generic method `G` with two type arguments and one regular argument.</span></span>

<span data-ttu-id="602c5-997">경우 일련의 토큰으로 구문 분석할 수 (컨텍스트에서)를 *simple_name* ([단순 이름](expressions.md#simple-names)), *member_access* ([멤버 액세스](expressions.md#member-access)), 또는 *pointer_member_access* ([포인터 멤버 액세스](unsafe-code.md#pointer-member-access))로 끝나는 *type_argument_list* ([형식 인수](types.md#type-arguments)), 토큰 바로 뒤에 닫는 `>` 토큰을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-997">If a sequence of tokens can be parsed (in context) as a *simple_name* ([Simple names](expressions.md#simple-names)), *member_access* ([Member access](expressions.md#member-access)), or *pointer_member_access* ([Pointer member access](unsafe-code.md#pointer-member-access)) ending with a *type_argument_list* ([Type arguments](types.md#type-arguments)), the token immediately following the closing `>` token is examined.</span></span> <span data-ttu-id="602c5-998">중 하나인 경우</span><span class="sxs-lookup"><span data-stu-id="602c5-998">If it is one of</span></span>
```csharp
(  )  ]  }  :  ;  ,  .  ?  ==  !=  |  ^
```
<span data-ttu-id="602c5-999">그런 다음 *type_argument_list* 의 일부로 유지 됩니다 합니다 *simple_name*에 *member_access* 또는 *pointer_member_access* 및 토큰 시퀀스의 가능한 다른 구문 분석 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-999">then the *type_argument_list* is retained as part of the *simple_name*, *member_access* or *pointer_member_access* and any other possible parse of the sequence of tokens is discarded.</span></span> <span data-ttu-id="602c5-1000">그렇지 않은 경우는 *type_argument_list* 의 일부로 간주 되지 않습니다는 *simple_name*, *member_access* 또는 *pointer_member_access*토큰 시퀀스의 다른 가능한 parse 없는 경우에, 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1000">Otherwise, the *type_argument_list* is not considered to be part of the *simple_name*, *member_access* or *pointer_member_access*, even if there is no other possible parse of the sequence of tokens.</span></span> <span data-ttu-id="602c5-1001">구문 분석할 때 이러한 규칙은 하지는 적용을 *type_argument_list* 에 *namespace_or_type_name* ([Namespace 및 형식 이름](basic-concepts.md#namespace-and-type-names)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1001">Note that these rules are not applied when parsing a *type_argument_list* in a *namespace_or_type_name* ([Namespace and type names](basic-concepts.md#namespace-and-type-names)).</span></span> <span data-ttu-id="602c5-1002">다음 문은</span><span class="sxs-lookup"><span data-stu-id="602c5-1002">The statement</span></span>
```csharp
F(G<A,B>(7));
```
<span data-ttu-id="602c5-1003">이 규칙에 따라 해석에 대 한 호출으로 `F` 제네릭 메서드를 호출은 하나의 인수를 사용 하 여 `G` 두 개의 형식 인수 및 일반 인수 하나를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1003">will, according to this rule, be interpreted as a call to `F` with one argument, which is a call to a generic method `G` with two type arguments and one regular argument.</span></span> <span data-ttu-id="602c5-1004">문</span><span class="sxs-lookup"><span data-stu-id="602c5-1004">The statements</span></span>
```csharp
F(G < A, B > 7);
F(G < A, B >> 7);
```
<span data-ttu-id="602c5-1005">각로 해석 됩니다에 대 한 호출 `F` 두 인수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1005">will each be interpreted as a call to `F` with two arguments.</span></span> <span data-ttu-id="602c5-1006">다음 문은</span><span class="sxs-lookup"><span data-stu-id="602c5-1006">The statement</span></span>
```csharp
x = F < A > +y;
```
<span data-ttu-id="602c5-1007">문이 작성 되었습니다 했습니다 처럼를 보다 작음 연산자, 연산자 및 단항 더하기 연산자 보다 큰로 해석 됩니다 `x = (F < A) > (+y)`을 대신으로 *simple_name* 사용 하 여를 *type_argument_list* 이진 더하기 연산자 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1007">will be interpreted as a less than operator, greater than operator, and unary plus operator, as if the statement had been written `x = (F < A) > (+y)`, instead of as a *simple_name* with a *type_argument_list* followed by a binary plus operator.</span></span> <span data-ttu-id="602c5-1008">문에서</span><span class="sxs-lookup"><span data-stu-id="602c5-1008">In the statement</span></span>
```csharp
x = y is C<T> + z;
```
<span data-ttu-id="602c5-1009">토큰 `C<T>` 로 해석 되는 *namespace_or_type_name* 사용 하 여를 *type_argument_list*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1009">the tokens `C<T>` are interpreted as a *namespace_or_type_name* with a *type_argument_list*.</span></span>

### <a name="invocation-expressions"></a><span data-ttu-id="602c5-1010">호출 식</span><span class="sxs-lookup"><span data-stu-id="602c5-1010">Invocation expressions</span></span>

<span data-ttu-id="602c5-1011">*invocation_expression* 메서드를 호출 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1011">An *invocation_expression* is used to invoke a method.</span></span>

```antlr
invocation_expression
    : primary_expression '(' argument_list? ')'
    ;
```

<span data-ttu-id="602c5-1012">*invocation_expression* 동적으로 바인딩된 ([동적 바인딩](expressions.md#dynamic-binding)) 다음 중 하나 이상 보유 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-1012">An *invocation_expression* is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)) if at least one of the following holds:</span></span>

* <span data-ttu-id="602c5-1013">합니다 *primary_expression* 컴파일 시간 형식이 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1013">The *primary_expression* has compile-time type `dynamic`.</span></span>
* <span data-ttu-id="602c5-1014">선택적 인수가 하나 이상 *argument_list* 컴파일 시간 형식이 `dynamic` 하며 *primary_expression* 대리자 형식이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1014">At least one argument of the optional *argument_list* has compile-time type `dynamic` and the *primary_expression* does not have a delegate type.</span></span>

<span data-ttu-id="602c5-1015">이 경우 컴파일러 분류 합니다 *invocation_expression* 형식의 값으로 `dynamic`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1015">In this case the compiler classifies the *invocation_expression* as a value of type `dynamic`.</span></span> <span data-ttu-id="602c5-1016">의미를 확인 하려면 아래의 규칙 합니다 *invocation_expression* 런타임에, 런타임 형식의의 컴파일 타임 형식 대신 사용 하 여 적용 되는 *primary_expression* 및 컴파일 타임 형식 인수 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1016">The rules below to determine the meaning of the *invocation_expression* are then applied at run-time, using the run-time type instead of the compile-time type of those of the *primary_expression* and arguments which have the compile-time type `dynamic`.</span></span> <span data-ttu-id="602c5-1017">경우는 *primary_expression* 컴파일 시간 형식이 없습니다 `dynamic`, 메서드 호출에 설명 된 대로 제한 된 컴파일 시간 검사를 거칩니다 그런 다음 [컴파일 타임 검사 동적 오버 로드 확인 ](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="602c5-1017">If the *primary_expression* does not have compile-time type `dynamic`, then the method invocation undergoes a limited compile time check as described in [Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span></span>

<span data-ttu-id="602c5-1018">합니다 *primary_expression* 의 *invocation_expression* 메서드 그룹 또는 값 이어야 합니다는 *delegate_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1018">The *primary_expression* of an *invocation_expression* must be a method group or a value of a *delegate_type*.</span></span> <span data-ttu-id="602c5-1019">경우는 *primary_expression* 그룹인 메서드는 *invocation_expression* 은 메서드 호출 ([메서드 호출](expressions.md#method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1019">If the *primary_expression* is a method group, the *invocation_expression* is a method invocation ([Method invocations](expressions.md#method-invocations)).</span></span> <span data-ttu-id="602c5-1020">경우는 *primary_expression* 의 값이를 *delegate_type*의 *invocation_expression* 은 대리자 호출 ([대리자 호출](expressions.md#delegate-invocations)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1020">If the *primary_expression* is a value of a *delegate_type*, the *invocation_expression* is a delegate invocation ([Delegate invocations](expressions.md#delegate-invocations)).</span></span> <span data-ttu-id="602c5-1021">경우는 *primary_expression* 이 메서드 그룹도 아니고 값을 *delegate_type*, 바인딩 시간 오류가 발생 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1021">If the *primary_expression* is neither a method group nor a value of a *delegate_type*, a binding-time error occurs.</span></span>

<span data-ttu-id="602c5-1022">선택적 *argument_list* ([인수 목록](expressions.md#argument-lists)) 메서드의 매개 변수 값 또는 변수 참조를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1022">The optional *argument_list* ([Argument lists](expressions.md#argument-lists)) provides values or variable references for the parameters of the method.</span></span>

<span data-ttu-id="602c5-1023">평가 결과 *invocation_expression* 다음과 같이 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1023">The result of evaluating an *invocation_expression* is classified as follows:</span></span>

*  <span data-ttu-id="602c5-1024">경우는 *invocation_expression* 메서드 또는 대리자를 반환 하는 호출 `void`, 결과 아무 작업도 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1024">If the *invocation_expression* invokes a method or delegate that returns `void`, the result is nothing.</span></span> <span data-ttu-id="602c5-1025">컨텍스트에서만에서 대체가 아무로 분류 되는 식을 *statement_expression* ([식 문은](statements.md#expression-statements)) 또는 본문을 *lambda_expression*([익명 함수 식](expressions.md#anonymous-function-expressions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1025">An expression that is classified as nothing is permitted only in the context of a *statement_expression* ([Expression statements](statements.md#expression-statements)) or as the body of a *lambda_expression* ([Anonymous function expressions](expressions.md#anonymous-function-expressions)).</span></span> <span data-ttu-id="602c5-1026">그렇지 않으면 바인딩 시간 오류를 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1026">Otherwise a binding-time error occurs.</span></span>
*  <span data-ttu-id="602c5-1027">그렇지 않으면 결과 메서드 또는 대리자를 반환한 형식의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1027">Otherwise, the result is a value of the type returned by the method or delegate.</span></span>

#### <a name="method-invocations"></a><span data-ttu-id="602c5-1028">메서드 호출</span><span class="sxs-lookup"><span data-stu-id="602c5-1028">Method invocations</span></span>

<span data-ttu-id="602c5-1029">메서드 호출에 대 한 합니다 *primary_expression* 의 합니다 *invocation_expression* 메서드 그룹 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1029">For a method invocation, the *primary_expression* of the *invocation_expression* must be a method group.</span></span> <span data-ttu-id="602c5-1030">메서드 그룹에는 하나의 메서드를 호출 하거나 호출할 특정 메서드를 선택할 수 있는 오버 로드 된 메서드 집합을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1030">The method group identifies the one method to invoke or the set of overloaded methods from which to choose a specific method to invoke.</span></span> <span data-ttu-id="602c5-1031">후자의 경우에 호출 하 고 특정 메서드의 결정은 컨텍스트를 기반으로 인수 형식에서 제공 합니다 *argument_list*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1031">In the latter case, determination of the specific method to invoke is based on the context provided by the types of the arguments in the *argument_list*.</span></span>

<span data-ttu-id="602c5-1032">형식의 메서드 호출을 처리 하는 바인딩 시간 `M(A)`, 여기서 `M` 그룹인 메서드 (포함 될 수도 있습니다는 *type_argument_list*), 및 `A` 선택적 *argument_ 목록*, 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1032">The binding-time processing of a method invocation of the form `M(A)`, where `M` is a method group (possibly including a *type_argument_list*), and `A` is an optional *argument_list*, consists of the following steps:</span></span>

*  <span data-ttu-id="602c5-1033">메서드 호출에 대 한 후보 메서드 집합이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1033">The set of candidate methods for the method invocation is constructed.</span></span> <span data-ttu-id="602c5-1034">각 메서드에 대 한 `F` 메서드 그룹과 연결 된 `M`:</span><span class="sxs-lookup"><span data-stu-id="602c5-1034">For each method `F` associated with the method group `M`:</span></span>
   *  <span data-ttu-id="602c5-1035">하는 경우 `F` 제네릭이 아닌 `F` 후보 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-1035">If `F` is non-generic, `F` is a candidate when:</span></span>
      * <span data-ttu-id="602c5-1036">`M` 형식 인수 목록이 없는 및</span><span class="sxs-lookup"><span data-stu-id="602c5-1036">`M` has no type argument list, and</span></span>
      * <span data-ttu-id="602c5-1037">`F` 기준으로 적용 됩니다 `A` ([적용 가능한 함수 멤버](expressions.md#applicable-function-member)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1037">`F` is applicable with respect to `A` ([Applicable function member](expressions.md#applicable-function-member)).</span></span>
   *  <span data-ttu-id="602c5-1038">하는 경우 `F` 제네릭인 및 `M` 없습니다 형식 인수 목록이 `F` 후보 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-1038">If `F` is generic and `M` has no type argument list, `F` is a candidate when:</span></span>
      * <span data-ttu-id="602c5-1039">형식 유추 ([형식 유추](expressions.md#type-inference))에 성공 하면 호출에 대해 형식 인수 목록이 유추 및</span><span class="sxs-lookup"><span data-stu-id="602c5-1039">Type inference ([Type inference](expressions.md#type-inference)) succeeds, inferring a list of type arguments for the call, and</span></span>
      * <span data-ttu-id="602c5-1040">F의 모든 생성 된 형식 매개 변수 목록에서 해당 제약 조건을 충족할 유추 된 형식 인수가 해당 메서드 형식 매개 변수를 대체 되 면 ([제약 조건을 만족](types.md#satisfying-constraints)), 및 매개 변수 목록이 `F` 기준으로 적용 됩니다 `A` ([적용 가능한 함수 멤버](expressions.md#applicable-function-member)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1040">Once the inferred type arguments are substituted for the corresponding method type parameters, all constructed types in the parameter list of F satisfy their constraints ([Satisfying constraints](types.md#satisfying-constraints)), and the parameter list of `F` is applicable with respect to `A` ([Applicable function member](expressions.md#applicable-function-member)).</span></span>
   *  <span data-ttu-id="602c5-1041">하는 경우 `F` 제네릭인 및 `M` 형식 인수 목록을 포함 `F` 후보 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-1041">If `F` is generic and `M` includes a type argument list, `F` is a candidate when:</span></span>
      * <span data-ttu-id="602c5-1042">`F` 에 형식 인수 목록에 제공 된 동일한 개수의 메서드 형식 매개 변수 및</span><span class="sxs-lookup"><span data-stu-id="602c5-1042">`F` has the same number of method type parameters as were supplied in the type argument list, and</span></span>
      * <span data-ttu-id="602c5-1043">F의 모든 생성 된 형식 매개 변수 목록에서 해당 제약 조건을 충족할 형식 인수를 해당 메서드 형식 매개 변수를 대체 되 면 ([제약 조건을 만족](types.md#satisfying-constraints)), 및 매개 변수 목록이 `F` 기준으로 적용 됩니다 `A` ([적용 가능한 함수 멤버](expressions.md#applicable-function-member)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1043">Once the type arguments are substituted for the corresponding method type parameters, all constructed types in the parameter list of F satisfy their constraints ([Satisfying constraints](types.md#satisfying-constraints)), and the parameter list of `F` is applicable with respect to `A` ([Applicable function member](expressions.md#applicable-function-member)).</span></span>
*  <span data-ttu-id="602c5-1044">후보 메서드 집합을 가장 많이 파생 된 형식에서 메서드만 포함 하도록 줄어듭니다: 각 메서드에 대 한 `C.F` 집합에 있는 `C` 는 형식인 메서드 `F` 기본형식에서선언된모든메서드가선언된`C`집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1044">The set of candidate methods is reduced to contain only methods from the most derived types: For each method `C.F` in the set, where `C` is the type in which the method `F` is declared, all methods declared in a base type of `C` are removed from the set.</span></span> <span data-ttu-id="602c5-1045">또한 경우 `C` 이외의 클래스 형식인 `object`, 인터페이스 형식에 선언 된 모든 메서드 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1045">Furthermore, if `C` is a class type other than `object`, all methods declared in an interface type are removed from the set.</span></span> <span data-ttu-id="602c5-1046">(이 두 번째 규칙만에 영향을 메서드 그룹 결과 형식 매개 변수에 유효한 기본 클래스 개체 이외의 및 설정 하는 비어 있지 않은 유효한 인터페이스 멤버 조회의 경우)</span><span class="sxs-lookup"><span data-stu-id="602c5-1046">(This latter rule only has affect when the method group was the result of a member lookup on a type parameter having an effective base class other than object and a non-empty effective interface set.)</span></span>
*  <span data-ttu-id="602c5-1047">중단 된 후 다음 단계를 따라 추가 처리 및 확장 메서드 호출으로 호출을 처리 하려고 할 대신 후보 메서드 결과 집합이 비어 있으면 ([확장 메서드 호출](expressions.md#extension-method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1047">If the resulting set of candidate methods is empty, then further processing along the following steps are abandoned, and instead an attempt is made to process the invocation as an extension method invocation ([Extension method invocations](expressions.md#extension-method-invocations)).</span></span> <span data-ttu-id="602c5-1048">이 작업이 실패 하면, 해당 메서드가 없는 존재 하 고 바인딩 시간에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1048">If this fails, then no applicable methods exist, and a binding-time error occurs.</span></span>
*  <span data-ttu-id="602c5-1049">후보는 메서드의 집합의 최상의 방법을의 오버 로드 확인 규칙을 사용 하 여 식별 됩니다 [오버 로드 확인](expressions.md#overload-resolution)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1049">The best method of the set of candidate methods is identified using the overload resolution rules of [Overload resolution](expressions.md#overload-resolution).</span></span> <span data-ttu-id="602c5-1050">단일 최상의 메서드를 식별할 수 없으면, 메서드 호출이 모호 합니다 및 바인딩 시간에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1050">If a single best method cannot be identified, the method invocation is ambiguous, and a binding-time error occurs.</span></span> <span data-ttu-id="602c5-1051">오버 로드 확인을 수행할 때 제네릭 메서드의 매개 변수를 해당 메서드 형식 매개 변수에 대해 형식 인수 (제공 되거나 유추 된)를 대체 한 후 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1051">When performing overload resolution, the parameters of a generic method are considered after substituting the type arguments (supplied or inferred) for the corresponding method type parameters.</span></span>
*  <span data-ttu-id="602c5-1052">선택한 모범 메서드의 마지막 유효성 검사가 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1052">Final validation of the chosen best method is performed:</span></span>
   * <span data-ttu-id="602c5-1053">메서드를 메서드 그룹의 컨텍스트에서 유효성을 검사: 메서드 그룹에서 했 해야 최상의 방법을 정적 메서드인 경우는 *simple_name* 또는 *member_access* 형식을 통해.</span><span class="sxs-lookup"><span data-stu-id="602c5-1053">The method is validated in the context of the method group: If the best method is a static method, the method group must have resulted from a *simple_name* or a *member_access* through a type.</span></span> <span data-ttu-id="602c5-1054">메서드 그룹에서 했 해야 최상의 방법을 인스턴스 메서드인 경우는 *simple_name*, *member_access* 변수 또는 값을 통해 또는 *base_access*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1054">If the best method is an instance method, the method group must have resulted from a *simple_name*, a *member_access* through a variable or value, or a *base_access*.</span></span> <span data-ttu-id="602c5-1055">이러한 요구 사항을 모두 true 인 경우 바인딩 시간 오류를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1055">If neither of these requirements is true, a binding-time error occurs.</span></span>
   * <span data-ttu-id="602c5-1056">형식 인수 (제공 되거나 유추)는 가장 좋은 방법은 제네릭 메서드 이면 제약 조건을 검사할지 ([제약 조건을 만족](types.md#satisfying-constraints)) 제네릭 메서드의 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1056">If the best method is a generic method, the type arguments (supplied or inferred) are checked against the constraints ([Satisfying constraints](types.md#satisfying-constraints)) declared on the generic method.</span></span> <span data-ttu-id="602c5-1057">형식 인수가 형식 매개 변수에 해당 제약 조건은 개입니다를 충족 하지 않으면 바인딩 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1057">If any type argument does not satisfy the corresponding constraint(s) on the type parameter, a binding-time error occurs.</span></span>

<span data-ttu-id="602c5-1058">실제 런타임 호출에서 설명 하는 함수 멤버 호출 규칙에 따라 처리 메서드를 선택 하 고 위의 단계에 따라 바인딩 시간에 유효성을 검사 된 후 [컴파일 타임 검사 동적 오버 로드 확인 ](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="602c5-1058">Once a method has been selected and validated at binding-time by the above steps, the actual run-time invocation is processed according to the rules of function member invocation described in [Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span></span>

<span data-ttu-id="602c5-1059">위에서 설명한 해결 규칙을 직관적은 다음과 같습니다: 메서드 호출을 호출 하는 특정 메서드를 찾으려면 메서드 호출에 의해 지정 된 형식을 사용 하 여 시작 하 고 하나 이상의 해당 될 때까지 상속 체인을 진행 합니다. 액세스할 수 있는, 재정의 되지 않는 메서드 선언을 발견 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1059">The intuitive effect of the resolution rules described above is as follows: To locate the particular method invoked by a method invocation, start with the type indicated by the method invocation and proceed up the inheritance chain until at least one applicable, accessible, non-override method declaration is found.</span></span> <span data-ttu-id="602c5-1060">형식 유추를 수행 및 오버 로드 확인에 해당 형식에서 선언 된 해당, 액세스할 수 있는, 재정의 되지 않는 메서드 집합에 고 따라서 선택한 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1060">Then perform type inference and overload resolution on the set of applicable, accessible, non-override methods declared in that type and invoke the method thus selected.</span></span> <span data-ttu-id="602c5-1061">메서드가 없습니다 있으면 하려고 대신 확장 메서드 호출으로 호출을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1061">If no method was found, try instead to process the invocation as an extension method invocation.</span></span>

#### <a name="extension-method-invocations"></a><span data-ttu-id="602c5-1062">확장 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="602c5-1062">Extension method invocations</span></span>

<span data-ttu-id="602c5-1063">메서드 호출에서 ([boxed 인스턴스에서 호출](expressions.md#invocations-on-boxed-instances)) 형식 중 하나</span><span class="sxs-lookup"><span data-stu-id="602c5-1063">In a method invocation ([Invocations on boxed instances](expressions.md#invocations-on-boxed-instances)) of one of the forms</span></span>
```csharp
expr . identifier ( )

expr . identifier ( args )

expr . identifier < typeargs > ( )

expr . identifier < typeargs > ( args )
```
<span data-ttu-id="602c5-1064">해당 메서드가 없는 찾으면, 호출의 일반적인 처리는 확장 메서드 호출 구문을 처리 시도가 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1064">if the normal processing of the invocation finds no applicable methods, an attempt is made to process the construct as an extension method invocation.</span></span> <span data-ttu-id="602c5-1065">하는 경우 *expr* 또는 합니다 *args* 컴파일 시간 형식이 `dynamic`, 확장 메서드는 적용 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1065">If *expr* or any of the *args* has compile-time type `dynamic`, extension methods will not apply.</span></span>

<span data-ttu-id="602c5-1066">가장 찾을 목적은 *type_name* `C`해당 정적 메서드 호출이 수행 될 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1066">The objective is to find the best *type_name* `C`, so that the corresponding static method invocation can take place:</span></span>
```csharp
C . identifier ( expr )

C . identifier ( expr , args )

C . identifier < typeargs > ( expr )

C . identifier < typeargs > ( expr , args )
```

<span data-ttu-id="602c5-1067">확장 메서드 `Ci.Mj` 됩니다 ***적격*** 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-1067">An extension method `Ci.Mj` is ***eligible*** if:</span></span>

*  <span data-ttu-id="602c5-1068">`Ci` 제네릭이 아닌 비중첩 클래스</span><span class="sxs-lookup"><span data-stu-id="602c5-1068">`Ci` is a non-generic, non-nested class</span></span>
*  <span data-ttu-id="602c5-1069">이름을 `Mj` 는 *식별자*</span><span class="sxs-lookup"><span data-stu-id="602c5-1069">The name of `Mj` is *identifier*</span></span>
*  <span data-ttu-id="602c5-1070">`Mj` 액세스할 수 있고 위에 표시 된 대로 정적 메서드로 인수에 적용 하는 경우에 적용</span><span class="sxs-lookup"><span data-stu-id="602c5-1070">`Mj` is accessible and applicable when applied to the arguments as a static method as shown above</span></span>
*  <span data-ttu-id="602c5-1071">암시적 id, 참조 또는 boxing 변환이 존재 *expr* 의 첫 번째 매개 변수 형식으로 `Mj`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1071">An implicit identity, reference or boxing conversion exists from *expr* to the type of the first parameter of `Mj`.</span></span>

<span data-ttu-id="602c5-1072">검색 `C` 다음과 같이 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1072">The search for `C` proceeds as follows:</span></span>

*  <span data-ttu-id="602c5-1073">가장 가까운 바깥쪽 네임 스페이스 선언, 각 바깥쪽 네임 스페이스 선언을 사용 하 여 계속 해 서 포함 된 컴파일 단위에 끝나는 연속 된 시도 확장 메서드의 후보 집합을 찾기 위해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1073">Starting with the closest enclosing namespace declaration, continuing with each enclosing namespace declaration, and ending with the containing compilation unit, successive attempts are made to find a candidate set of extension methods:</span></span>
   * <span data-ttu-id="602c5-1074">제네릭이 아닌 형식을 선언에 지정 된 네임 스페이스 또는 컴파일 단위의 경우 직접 포함 `Ci` 적합 한 확장 메서드를 사용 하 여 `Mj`, 이러한 확장 메서드 집합을 후보 집합이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1074">If the given namespace or compilation unit directly contains non-generic type declarations `Ci` with eligible extension methods `Mj`, then the set of those extension methods is the candidate set.</span></span>
   * <span data-ttu-id="602c5-1075">경우 형식 `Ci` 에서 가져온 *using_static_declarations* 에서 가져온 네임 스페이스에서 선언 된 직접 *using_namespace_directive*지정 된 네임 스페이스 또는 컴파일 단위에 직접 s 적합 한 확장 메서드를 포함 `Mj`, 이러한 확장 메서드 집합을 후보 집합이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1075">If types `Ci` imported by *using_static_declarations* and directly declared in namespaces imported by *using_namespace_directive*s in the given namespace or compilation unit directly contain eligible extension methods `Mj`, then the set of those extension methods is the candidate set.</span></span>
*  <span data-ttu-id="602c5-1076">후보 집합이 없는 모든 바깥쪽 네임 스페이스 선언 또는 컴파일 단위에 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1076">If no candidate set is found in any enclosing namespace declaration or compilation unit, a compile-time error occurs.</span></span>
*  <span data-ttu-id="602c5-1077">에 설명 된 대로 설정 후보를 오버 로드 확인이 적용 하는 그렇지 않은 경우 ([오버 로드 확인](expressions.md#overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1077">Otherwise, overload resolution is applied to the candidate set as described in ([Overload resolution](expressions.md#overload-resolution)).</span></span> <span data-ttu-id="602c5-1078">최상의 방법에는 여러 있으면 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1078">If no single best method is found, a compile-time error occurs.</span></span>
*  <span data-ttu-id="602c5-1079">`C` 가장 좋은 방법은 확장 메서드로 선언 된 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1079">`C` is the type within which the best method is declared as an extension method.</span></span>

<span data-ttu-id="602c5-1080">사용 하 여 `C` 대상으로 메서드 호출은 정적 메서드 호출으로 처리 한 다음 ([동적 오버 로드 확인 검사 하는 컴파일 타임](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1080">Using `C` as a target, the method call is then processed as a static method invocation ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span></span>

<span data-ttu-id="602c5-1081">인스턴스 메서드와 확장 메서드가 보다 우선적으로 적용 하는 내부 네임 스페이스 선언에서 사용할 수 있는 확장 메서드 우선 외부 네임 스페이스 선언 및 해당 확장에서 사용할 수 있는 확장 메서드, 이전 규칙 의미 네임 스페이스에 직접 선언 된 메서드를 사용 하 여 동일한 네임 스페이스를 가져올 확장 메서드 보다 우선적으로 적용 네임 스페이스 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1081">The preceding rules mean that instance methods take precedence over extension methods, that extension methods available in inner namespace declarations take precedence over extension methods available in outer namespace declarations, and that extension methods declared directly in a namespace take precedence over extension methods imported into that same namespace with a using namespace directive.</span></span> <span data-ttu-id="602c5-1082">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="602c5-1082">For example:</span></span>
```csharp
public static class E
{
    public static void F(this object obj, int i) { }

    public static void F(this object obj, string s) { }
}

class A { }

class B
{
    public void F(int i) { }
}

class C
{
    public void F(object obj) { }
}

class X
{
    static void Test(A a, B b, C c) {
        a.F(1);              // E.F(object, int)
        a.F("hello");        // E.F(object, string)

        b.F(1);              // B.F(int)
        b.F("hello");        // E.F(object, string)

        c.F(1);              // C.F(object)
        c.F("hello");        // C.F(object)
    }
}
```

<span data-ttu-id="602c5-1083">예에서 `B`의 메서드는 첫 번째 확장 메서드인 보다 우선 및 `C`의 메서드 두 확장 메서드보다 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1083">In the example, `B`'s method takes precedence over the first extension method, and `C`'s method takes precedence over both extension methods.</span></span>

```csharp
public static class C
{
    public static void F(this int i) { Console.WriteLine("C.F({0})", i); }
    public static void G(this int i) { Console.WriteLine("C.G({0})", i); }
    public static void H(this int i) { Console.WriteLine("C.H({0})", i); }
}

namespace N1
{
    public static class D
    {
        public static void F(this int i) { Console.WriteLine("D.F({0})", i); }
        public static void G(this int i) { Console.WriteLine("D.G({0})", i); }
    }
}

namespace N2
{
    using N1;

    public static class E
    {
        public static void F(this int i) { Console.WriteLine("E.F({0})", i); }
    }

    class Test
    {
        static void Main(string[] args)
        {
            1.F();
            2.G();
            3.H();
        }
    }
}
```

<span data-ttu-id="602c5-1084">이 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1084">The output of this example is:</span></span>
```
E.F(1)
D.G(2)
C.H(3)
```
<span data-ttu-id="602c5-1085">`D.G` 우선 `C.G`, 및 `E.F` 둘 다 보다 우선 `D.F` 및 `C.F`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1085">`D.G` takes precedence over `C.G`, and `E.F` takes precedence over both `D.F` and `C.F`.</span></span>

#### <a name="delegate-invocations"></a><span data-ttu-id="602c5-1086">대리자 호출</span><span class="sxs-lookup"><span data-stu-id="602c5-1086">Delegate invocations</span></span>

<span data-ttu-id="602c5-1087">대리자 호출에 대 한 합니다 *primary_expression* 의 *invocation_expression* 의 값 이어야 합니다는 *delegate_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1087">For a delegate invocation, the *primary_expression* of the *invocation_expression* must be a value of a *delegate_type*.</span></span> <span data-ttu-id="602c5-1088">또한 고려 합니다 *delegate_type* 같은 매개 변수 목록 사용 하 여 함수 멤버 여야 합니다 *delegate_type*, *delegate_type* 적용 (이어야 합니다 [적용 가능한 함수 멤버](expressions.md#applicable-function-member))을 기준으로 합니다 *argument_list* 의 합니다 *invocation_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1088">Furthermore, considering the *delegate_type* to be a function member with the same parameter list as the *delegate_type*, the *delegate_type* must be applicable ([Applicable function member](expressions.md#applicable-function-member)) with respect to the *argument_list* of the *invocation_expression*.</span></span>

<span data-ttu-id="602c5-1089">폼의 대리자 호출을 처리 하는 런타임 `D(A)`, 여기서 `D` 는 *primary_expression* 의 *delegate_type* 및 `A` 되는 선택적 *argument_list*, 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1089">The run-time processing of a delegate invocation of the form `D(A)`, where `D` is a *primary_expression* of a *delegate_type* and `A` is an optional *argument_list*, consists of the following steps:</span></span>

*  <span data-ttu-id="602c5-1090">`D` 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1090">`D` is evaluated.</span></span> <span data-ttu-id="602c5-1091">이 평가 예외를 발생 시키는 경우에 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1091">If this evaluation causes an exception, no further steps are executed.</span></span>
*  <span data-ttu-id="602c5-1092">변수의 `D` 유효한 것으로 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1092">The value of `D` is checked to be valid.</span></span> <span data-ttu-id="602c5-1093">경우 값 `D` 은 `null`, `System.NullReferenceException` throw 되 고 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1093">If the value of `D` is `null`, a `System.NullReferenceException` is thrown and no further steps are executed.</span></span>
*  <span data-ttu-id="602c5-1094">그렇지 않으면 `D` 대리자 인스턴스에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1094">Otherwise, `D` is a reference to a delegate instance.</span></span> <span data-ttu-id="602c5-1095">멤버 호출 함수 ([컴파일 타임 동적 오버 로드 확인 검사](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) 각 대리자의 호출 목록에서 호출할 엔터티에 대해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1095">Function member invocations ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) are performed on each of the callable entities in the invocation list of the delegate.</span></span> <span data-ttu-id="602c5-1096">구성 된 인스턴스 및 인스턴스 메서드를 호출할 엔터티에 대해 호출에 대 한 인스턴스는 호출 가능 엔터티에 포함 된 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1096">For callable entities consisting of an instance and instance method, the instance for the invocation is the instance contained in the callable entity.</span></span>

### <a name="element-access"></a><span data-ttu-id="602c5-1097">요소 액세스</span><span class="sxs-lookup"><span data-stu-id="602c5-1097">Element access</span></span>

<span data-ttu-id="602c5-1098">*element_access* 이루어져 있습니다를 *primary_no_array_creation_expression*뒤를 "`[`" 토큰, 뒤에 *argument_list*뒤를 " `]`"토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1098">An *element_access* consists of a *primary_no_array_creation_expression*, followed by a "`[`" token, followed by an *argument_list*, followed by a "`]`" token.</span></span> <span data-ttu-id="602c5-1099">합니다 *argument_list* 하나 이상의 구성 *인수*s, 쉼표로 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1099">The *argument_list* consists of one or more *argument*s, separated by commas.</span></span>

```antlr
element_access
    : primary_no_array_creation_expression '[' expression_list ']'
    ;
```

<span data-ttu-id="602c5-1100">합니다 *argument_list* 의 *element_access* 포함 되지 `ref` 또는 `out` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1100">The *argument_list* of an *element_access* is not allowed to contain `ref` or `out` arguments.</span></span>

<span data-ttu-id="602c5-1101">*element_access* 동적으로 바인딩된 ([동적 바인딩](expressions.md#dynamic-binding)) 다음 중 하나 이상 보유 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-1101">An *element_access* is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)) if at least one of the following holds:</span></span>

* <span data-ttu-id="602c5-1102">합니다 *primary_no_array_creation_expression* 컴파일 시간 형식이 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1102">The *primary_no_array_creation_expression* has compile-time type `dynamic`.</span></span>
* <span data-ttu-id="602c5-1103">하나 이상의 식입니다를 *argument_list* 컴파일 시간 형식이 `dynamic` 하며 *primary_no_array_creation_expression* 배열 형식이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1103">At least one expression of the *argument_list* has compile-time type `dynamic` and the *primary_no_array_creation_expression* does not have an array type.</span></span>

<span data-ttu-id="602c5-1104">이 경우 컴파일러 분류 합니다 *element_access* 형식의 값으로 `dynamic`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1104">In this case the compiler classifies the *element_access* as a value of type `dynamic`.</span></span> <span data-ttu-id="602c5-1105">의미를 확인 하려면 아래의 규칙 합니다 *element_access* 런타임에, 런타임 형식의의 컴파일 타임 형식 대신 사용 하 여 적용 되는 *primary_no_array_creation_expression*하 고 *argument_list* 식은 컴파일 시간 형식이 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1105">The rules below to determine the meaning of the *element_access* are then applied at run-time, using the run-time type instead of the compile-time type of those of the *primary_no_array_creation_expression* and *argument_list* expressions which have the compile-time type `dynamic`.</span></span> <span data-ttu-id="602c5-1106">경우는 *primary_no_array_creation_expression* 컴파일 시간 형식이 없습니다 `dynamic`, 요소 액세스에 설명 된 대로 제한 된 컴파일 시간 검사를 거칩니다 그런 다음 [컴파일 타임 동적 검사 오버 로드 확인](expressions.md#compile-time-checking-of-dynamic-overload-resolution)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1106">If the *primary_no_array_creation_expression* does not have compile-time type `dynamic`, then the element access undergoes a limited compile time check as described in [Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span></span>

<span data-ttu-id="602c5-1107">경우는 *primary_no_array_creation_expression* 의 *element_access* 의 값이를 *array_type*, *element_access* 는 배열 액세스 ([액세스 배열](expressions.md#array-access)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1107">If the *primary_no_array_creation_expression* of an *element_access* is a value of an *array_type*, the *element_access* is an array access ([Array access](expressions.md#array-access)).</span></span> <span data-ttu-id="602c5-1108">이 고, 그렇지 합니다 *primary_no_array_creation_expression* 변수나 클래스, 구조체 또는 인터페이스 형식에 하나 이상의 인덱서 멤버가 있는 경우에 값 이어야 합니다 합니다 *element_access* 는 인덱서 액세스 ([인덱서 액세스](expressions.md#indexer-access)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1108">Otherwise, the *primary_no_array_creation_expression* must be a variable or value of a class, struct, or interface type that has one or more indexer members, in which case the *element_access* is an indexer access ([Indexer access](expressions.md#indexer-access)).</span></span>

#### <a name="array-access"></a><span data-ttu-id="602c5-1109">배열 액세스</span><span class="sxs-lookup"><span data-stu-id="602c5-1109">Array access</span></span>

<span data-ttu-id="602c5-1110">배열 액세스의 경우는 *primary_no_array_creation_expression* 의 *element_access* 의 값 이어야 합니다는 *array_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1110">For an array access, the *primary_no_array_creation_expression* of the *element_access* must be a value of an *array_type*.</span></span> <span data-ttu-id="602c5-1111">또한 합니다 *argument_list* 배열을 액세스가 명명 된 인수를 포함 하도록 허용 되지 않습니다. 식의 수를 *argument_list* 의 순위와 동일 해야 합니다 *array_type*, 각 식 형식 이어야 하 고 `int`, `uint`, `long`, `ulong`, 또는 이러한 형식 중 하나 이상의 암시적으로 변환할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1111">Furthermore, the *argument_list* of an array access is not allowed to contain named arguments.The number of expressions in the *argument_list* must be the same as the rank of the *array_type*, and each expression must be of type `int`, `uint`, `long`, `ulong`, or must be implicitly convertible to one or more of these types.</span></span>

<span data-ttu-id="602c5-1112">Namely에서 절입니다의 값으로 선택 배열 요소 배열의 요소 형식의 변수가 배열 액세스 평가의 결과 *argument_list*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1112">The result of evaluating an array access is a variable of the element type of the array, namely the array element selected by the value(s) of the expression(s) in the *argument_list*.</span></span>

<span data-ttu-id="602c5-1113">형식의 배열 액세스를 처리 하는 런타임 `P[A]`여기서 `P` 되는 *primary_no_array_creation_expression* 의 *array_type* 및 `A` 되는 *argument_list*, 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1113">The run-time processing of an array access of the form `P[A]`, where `P` is a *primary_no_array_creation_expression* of an *array_type* and `A` is an *argument_list*, consists of the following steps:</span></span>

*  <span data-ttu-id="602c5-1114">`P` 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1114">`P` is evaluated.</span></span> <span data-ttu-id="602c5-1115">이 평가 예외를 발생 시키는 경우에 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1115">If this evaluation causes an exception, no further steps are executed.</span></span>
*  <span data-ttu-id="602c5-1116">인덱스 식의 *argument_list* 왼쪽에서 오른쪽 순서로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1116">The index expressions of the *argument_list* are evaluated in order, from left to right.</span></span> <span data-ttu-id="602c5-1117">각 인덱스 식의 암시적 변환이 평가 ([암시적 변환을](conversions.md#implicit-conversions)) 다음 형식 중 하나로 수행 됩니다: `int`, `uint`에 `long`, `ulong`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1117">Following evaluation of each index expression, an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) to one of the following types is performed: `int`, `uint`, `long`, `ulong`.</span></span> <span data-ttu-id="602c5-1118">암시적 변환이 존재 하는이 목록의 첫 번째 형식이 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1118">The first type in this list for which an implicit conversion exists is chosen.</span></span> <span data-ttu-id="602c5-1119">예를 들어 된 인덱스 식 형식의 경우 `short` 으로 암시적 변환이 다음 `int` 에서 암시적 변환이 수행 됩니다 `short` 를 `int` 들어오고 `short` 를 `long` 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1119">For instance, if the index expression is of type `short` then an implicit conversion to `int` is performed, since implicit conversions from `short` to `int` and from `short` to `long` are possible.</span></span> <span data-ttu-id="602c5-1120">인덱스 식의 후속 암시적 변환 평가 예외를 발생 시키는 경우 다음 인덱스 식은 더 이상 계산 되 고 단계를 실행 하는 더 이상.</span><span class="sxs-lookup"><span data-stu-id="602c5-1120">If evaluation of an index expression or the subsequent implicit conversion causes an exception, then no further index expressions are evaluated and no further steps are executed.</span></span>
*  <span data-ttu-id="602c5-1121">변수의 `P` 유효한 것으로 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1121">The value of `P` is checked to be valid.</span></span> <span data-ttu-id="602c5-1122">경우 값 `P` 은 `null`, `System.NullReferenceException` throw 되 고 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1122">If the value of `P` is `null`, a `System.NullReferenceException` is thrown and no further steps are executed.</span></span>
*  <span data-ttu-id="602c5-1123">각 식의 값을 *argument_list* 과 비교 하는 각 차원에서 참조 하는 배열 인스턴스의 실제 범위는 `P`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1123">The value of each expression in the *argument_list* is checked against the actual bounds of each dimension of the array instance referenced by `P`.</span></span> <span data-ttu-id="602c5-1124">하나 이상의 값 범위를 벗어나는 경우는 `System.IndexOutOfRangeException` throw 되 고 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1124">If one or more values are out of range, a `System.IndexOutOfRangeException` is thrown and no further steps are executed.</span></span>
*  <span data-ttu-id="602c5-1125">인덱스 식이 지정 된 배열 요소의 위치를 계산 하 고이 위치 배열 액세스의 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1125">The location of the array element given by the index expression(s) is computed, and this location becomes the result of the array access.</span></span>

#### <a name="indexer-access"></a><span data-ttu-id="602c5-1126">인덱서 액세스</span><span class="sxs-lookup"><span data-stu-id="602c5-1126">Indexer access</span></span>

<span data-ttu-id="602c5-1127">인덱서 액세스의 경우는 *primary_no_array_creation_expression* 의 합니다 *element_access* 변수 또는 값 클래스, 구조체 또는 인터페이스 형식 이어야 합니다이 형식이 하나 이상 구현 해야 하 고 기준으로 적용 되는 인덱서를 *argument_list* 의 합니다 *element_access*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1127">For an indexer access, the *primary_no_array_creation_expression* of the *element_access* must be a variable or value of a class, struct, or interface type, and this type must implement one or more indexers that are applicable with respect to the *argument_list* of the *element_access*.</span></span>

<span data-ttu-id="602c5-1128">형식의 인덱서 액세스를 처리 하는 바인딩 시간 `P[A]`여기서 `P` 되는 *primary_no_array_creation_expression* 클래스, 구조체 또는 인터페이스 형식입니다 `T`, 및 `A` 는 *argument_list*, 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1128">The binding-time processing of an indexer access of the form `P[A]`, where `P` is a *primary_no_array_creation_expression* of a class, struct, or interface type `T`, and `A` is an *argument_list*, consists of the following steps:</span></span>

*  <span data-ttu-id="602c5-1129">집합에서 제공 하는 인덱서의 `T` 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1129">The set of indexers provided by `T` is constructed.</span></span> <span data-ttu-id="602c5-1130">집합은 구성에서 선언 된 모든 인덱서의 `T` 또는 기본 형식의 `T` 없는 `override` 선언과 현재 컨텍스트에서 액세스할 수 있습니다 ([멤버 액세스](basic-concepts.md#member-access)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1130">The set consists of all indexers declared in `T` or a base type of `T` that are not `override` declarations and are accessible in the current context ([Member access](basic-concepts.md#member-access)).</span></span>
*  <span data-ttu-id="602c5-1131">집합을 다른 인덱서에서 숨겨지지 않은 하 고 해당 되는 이러한 인덱서 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1131">The set is reduced to those indexers that are applicable and not hidden by other indexers.</span></span> <span data-ttu-id="602c5-1132">각 인덱서는 다음 규칙이 적용 됩니다 `S.I` 집합에 있는 `S` 는 형식이 인덱서 `I` 선언:</span><span class="sxs-lookup"><span data-stu-id="602c5-1132">The following rules are applied to each indexer `S.I` in the set, where `S` is the type in which the indexer `I` is declared:</span></span>
   * <span data-ttu-id="602c5-1133">하는 경우 `I` 기준으로 적용 되지 않습니다 `A` ([적용 가능한 함수 멤버](expressions.md#applicable-function-member)), 다음 `I` 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1133">If `I` is not applicable with respect to `A` ([Applicable function member](expressions.md#applicable-function-member)), then `I` is removed from the set.</span></span>
   * <span data-ttu-id="602c5-1134">하는 경우 `I` 기준으로 적용 됩니다 `A` ([적용 가능한 함수 멤버](expressions.md#applicable-function-member)), 기본 형식의 모든 인덱서에 선언 `S` 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1134">If `I` is applicable with respect to `A` ([Applicable function member](expressions.md#applicable-function-member)), then all indexers declared in a base type of `S` are removed from the set.</span></span>
   * <span data-ttu-id="602c5-1135">하는 경우 `I` 기준으로 적용 됩니다 `A` ([적용 가능한 함수 멤버](expressions.md#applicable-function-member)) 및 `S` 이외의 클래스 형식인 `object`, 인터페이스에서 선언 된 모든 인덱서 집합에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1135">If `I` is applicable with respect to `A` ([Applicable function member](expressions.md#applicable-function-member)) and `S` is a class type other than `object`, all indexers declared in an interface are removed from the set.</span></span>
*  <span data-ttu-id="602c5-1136">후보 인덱서 결과 집합이 비어 있으면 다음 적용 가능한 인덱서가 없습니다 존재 및 바인딩 시간에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1136">If the resulting set of candidate indexers is empty, then no applicable indexers exist, and a binding-time error occurs.</span></span>
*  <span data-ttu-id="602c5-1137">후보 인덱서의 집합의 최상의 인덱서의 오버 로드 확인 규칙을 사용 하 여 식별 됩니다 [오버 로드 확인](expressions.md#overload-resolution)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1137">The best indexer of the set of candidate indexers is identified using the overload resolution rules of [Overload resolution](expressions.md#overload-resolution).</span></span> <span data-ttu-id="602c5-1138">가장 하는 단일 인덱서를 식별할 수 없으면, 인덱서 액세스를 모호 하 게 되며 바인딩 시간 오류를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1138">If a single best indexer cannot be identified, the indexer access is ambiguous, and a binding-time error occurs.</span></span>
*  <span data-ttu-id="602c5-1139">인덱스 식의 *argument_list* 왼쪽에서 오른쪽 순서로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1139">The index expressions of the *argument_list* are evaluated in order, from left to right.</span></span> <span data-ttu-id="602c5-1140">인덱서 액세스를 처리 하는 결과 인덱서 액세스로 분류 되는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1140">The result of processing the indexer access is an expression classified as an indexer access.</span></span> <span data-ttu-id="602c5-1141">인덱서 액세스 식 참조 하는 위의 단계에서 결정 된 인덱서 있고는 연결 된 인스턴스 식이 `P` 관련된 인수 목록과 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1141">The indexer access expression references the indexer determined in the step above, and has an associated instance expression of `P` and an associated argument list of `A`.</span></span>

<span data-ttu-id="602c5-1142">사용 되는 컨텍스트에 따라 인덱서 액세스 하면 중 호출 된 *get 접근자* 또는 *set 접근자* 인덱서의.</span><span class="sxs-lookup"><span data-stu-id="602c5-1142">Depending on the context in which it is used, an indexer access causes invocation of either the *get accessor* or the *set accessor* of the indexer.</span></span> <span data-ttu-id="602c5-1143">인덱서 액세스는 할당 대상일 경우 합니다 *set 접근자* 새 값을 할당 하기 위해 호출 됩니다 ([단순 할당](expressions.md#simple-assignment)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1143">If the indexer access is the target of an assignment, the *set accessor* is invoked to assign a new value ([Simple assignment](expressions.md#simple-assignment)).</span></span> <span data-ttu-id="602c5-1144">다른 모든 경우에는 *get 접근자* 가 현재 값을 얻기 위해 호출 됩니다 ([식의 값](expressions.md#values-of-expressions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1144">In all other cases, the *get accessor* is invoked to obtain the current value ([Values of expressions](expressions.md#values-of-expressions)).</span></span>

### <a name="this-access"></a><span data-ttu-id="602c5-1145">이 액세스</span><span class="sxs-lookup"><span data-stu-id="602c5-1145">This access</span></span>

<span data-ttu-id="602c5-1146">A *this_access* 예약어 이루어져 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1146">A *this_access* consists of the reserved word `this`.</span></span>

```antlr
this_access
    : 'this'
    ;
```

<span data-ttu-id="602c5-1147">*this_access* 에서만 허용 되는 *블록* 인스턴스 생성자, 인스턴스 메서드 또는 인스턴스 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1147">A *this_access* is permitted only in the *block* of an instance constructor, an instance method, or an instance accessor.</span></span> <span data-ttu-id="602c5-1148">의미 중 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1148">It has one of the following meanings:</span></span>

*  <span data-ttu-id="602c5-1149">때 `this` 에 사용 되는 *primary_expression* 클래스의 인스턴스 생성자, 내 값으로 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1149">When `this` is used in a *primary_expression* within an instance constructor of a class, it is classified as a value.</span></span> <span data-ttu-id="602c5-1150">값의 형식은 인스턴스 형식 ([인스턴스 유형을](classes.md#the-instance-type))는 사용 된 하 고 값이 생성 되는 개체에 대 한 참조는 클래스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1150">The type of the value is the instance type ([The instance type](classes.md#the-instance-type)) of the class within which the usage occurs, and the value is a reference to the object being constructed.</span></span>
*  <span data-ttu-id="602c5-1151">때 `this` 에 사용 되는 *primary_expression* 인스턴스 메서드 또는 클래스의 인스턴스 접근자에서 값으로 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1151">When `this` is used in a *primary_expression* within an instance method or instance accessor of a class, it is classified as a value.</span></span> <span data-ttu-id="602c5-1152">값의 형식은 인스턴스 형식 ([인스턴스 유형을](classes.md#the-instance-type))는 사용 된 하 고 값이 있는 메서드 또는 접근자가 호출에 대 한 참조는 클래스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1152">The type of the value is the instance type ([The instance type](classes.md#the-instance-type)) of the class within which the usage occurs, and the value is a reference to the object for which the method or accessor was invoked.</span></span>
*  <span data-ttu-id="602c5-1153">때 `this` 에 사용 되는 *primary_expression* 구조체의 인스턴스 생성자, 내에서 변수로 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1153">When `this` is used in a *primary_expression* within an instance constructor of a struct, it is classified as a variable.</span></span> <span data-ttu-id="602c5-1154">변수의 형식은 인스턴스 형식 ([인스턴스 유형을](classes.md#the-instance-type))는 사용 된 및 변수 생성 되 고 있는 구조체를 나타내는 구조체의 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1154">The type of the variable is the instance type ([The instance type](classes.md#the-instance-type)) of the struct within which the usage occurs, and the variable represents the struct being constructed.</span></span> <span data-ttu-id="602c5-1155">합니다 `this` 동일 하 게 동작 하는 구조체의 인스턴스 생성자의 변수는 `out` 구조체 형식의 매개 변수-특히 인스턴스에 대 한 모든 실행 경로에서 변수를 확실 하 게 할당 해야 함을 의미이 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1155">The `this` variable of an instance constructor of a struct behaves exactly the same as an `out` parameter of the struct type—in particular, this means that the variable must be definitely assigned in every execution path of the instance constructor.</span></span>
*  <span data-ttu-id="602c5-1156">때 `this` 에 사용 되는 *primary_expression* 인스턴스 메서드 또는 인스턴스 접근자 구조체의에서 변수로 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1156">When `this` is used in a *primary_expression* within an instance method or instance accessor of a struct, it is classified as a variable.</span></span> <span data-ttu-id="602c5-1157">변수의 형식은 인스턴스 형식 ([인스턴스 유형을](classes.md#the-instance-type)) 사용량을 발생 하는 구조체의 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1157">The type of the variable is the instance type ([The instance type](classes.md#the-instance-type)) of the struct within which the usage occurs.</span></span>
   * <span data-ttu-id="602c5-1158">메서드 또는 접근자는 반복기가 하는 경우 ([반복기](classes.md#iterators)), `this` 변수는 메서드 또는 접근자 호출 되었는지와 동일 하 게 동작 구조체를 나타냅니다는 `ref` 구조체 형식의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1158">If the method or accessor is not an iterator ([Iterators](classes.md#iterators)), the `this` variable represents the struct for which the method or accessor was invoked, and behaves exactly the same as a `ref` parameter of the struct type.</span></span>
   * <span data-ttu-id="602c5-1159">메서드 또는 접근자가 반복기는 `this` 변수는 메서드 또는 접근자가 호출 됩니다 및 값 매개 변수는 구조체 형식의 정확히 동일 하 게 동작 하는 구조체의 복사본을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1159">If the method or accessor is an iterator, the `this` variable represents a copy of the struct for which the method or accessor was invoked, and behaves exactly the same as a value parameter of the struct type.</span></span>

<span data-ttu-id="602c5-1160">이용 `this` 에 *primary_expression* 위에 나열 된 것 이외의 컨텍스트에서 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1160">Use of `this` in a *primary_expression* in a context other than the ones listed above is a compile-time error.</span></span> <span data-ttu-id="602c5-1161">참조할 수는 특히 `this` 또는 정적 메서드를 정적 속성 접근자에는 *variable_initializer* 필드 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1161">In particular, it is not possible to refer to `this` in a static method, a static property accessor, or in a *variable_initializer* of a field declaration.</span></span>

### <a name="base-access"></a><span data-ttu-id="602c5-1162">기본 액세스</span><span class="sxs-lookup"><span data-stu-id="602c5-1162">Base access</span></span>

<span data-ttu-id="602c5-1163">A *base_access* 예약어 이루어져 `base` 뒤에 하나는 "`.`" 토큰 및 식별자 또는 *argument_list* 대괄호로:</span><span class="sxs-lookup"><span data-stu-id="602c5-1163">A *base_access* consists of the reserved word `base` followed by either a "`.`" token and an identifier or an *argument_list* enclosed in square brackets:</span></span>

```antlr
base_access
    : 'base' '.' identifier
    | 'base' '[' expression_list ']'
    ;
```

<span data-ttu-id="602c5-1164">A *base_access* 현재 클래스 또는 구조체에서 비슷한 이름의 멤버가 숨겨져 있는 기본 클래스 멤버에 액세스 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1164">A *base_access* is used to access base class members that are hidden by similarly named members in the current class or struct.</span></span> <span data-ttu-id="602c5-1165">*base_access* 에서만 허용 되는 *블록* 인스턴스 생성자, 인스턴스 메서드 또는 인스턴스 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1165">A *base_access* is permitted only in the *block* of an instance constructor, an instance method, or an instance accessor.</span></span> <span data-ttu-id="602c5-1166">때 `base.I` 클래스 또는 구조체에서 발생 `I` 해당 클래스 또는 구조체의 기본 클래스의 멤버를 나타내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1166">When `base.I` occurs in a class or struct, `I` must denote a member of the base class of that class or struct.</span></span> <span data-ttu-id="602c5-1167">마찬가지로, `base[E]` 해당 인덱서는 기본 클래스에 있어야 합니다. 클래스에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1167">Likewise, when `base[E]` occurs in a class, an applicable indexer must exist in the base class.</span></span>

<span data-ttu-id="602c5-1168">바인딩 시 *base_access* 형식의 식을 `base.I` 하 고 `base[E]` 작성 된 것 처럼 정확 하 게 평가 됩니다 `((B)this).I` 하 고 `((B)this)[E]`여기서 `B` 클래스의 기본 클래스인 또는 구문을 발생 하는 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1168">At binding-time, *base_access* expressions of the form `base.I` and `base[E]` are evaluated exactly as if they were written `((B)this).I` and `((B)this)[E]`, where `B` is the base class of the class or struct in which the construct occurs.</span></span> <span data-ttu-id="602c5-1169">따라서 `base.I` 및 `base[E]` 에 해당 `this.I` 및 `this[E]`를 제외한 `this` 는 기본 클래스의 인스턴스로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1169">Thus, `base.I` and `base[E]` correspond to `this.I` and `this[E]`, except `this` is viewed as an instance of the base class.</span></span>

<span data-ttu-id="602c5-1170">경우는 *base_access* 는 확인에 런타임 시 호출할 멤버 함수는 가상 함수 멤버 (메서드, 속성 또는 인덱서)을 참조 ([컴파일 타임 검사 동적 오버 로드 확인 ](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1170">When a *base_access* references a virtual function member (a method, property, or indexer), the determination of which function member to invoke at run-time ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) is changed.</span></span> <span data-ttu-id="602c5-1171">가장 많이 파생 된 구현을 찾아 확인 하는 호출 되는 함수 멤버 ([가상 메서드](classes.md#virtual-methods))의 기준으로 하는 함수 멤버 `B` (대신의 런타임 형식에 대해 `this`, 으로 것 기본이 아닌 액세스의 일반적인)입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1171">The function member that is invoked is determined by finding the most derived implementation ([Virtual methods](classes.md#virtual-methods)) of the function member with respect to `B` (instead of with respect to the run-time type of `this`, as would be usual in a non-base access).</span></span> <span data-ttu-id="602c5-1172">따라서 내는 `override` 의 `virtual` 함수 멤버를 *base_access* 함수 멤버의 상속된 된 구현 호출에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1172">Thus, within an `override` of a `virtual` function member, a *base_access* can be used to invoke the inherited implementation of the function member.</span></span> <span data-ttu-id="602c5-1173">참조 하는 함수 멤버를 *base_access* 바인딩 시간 오류가 발생 하는 추상 클래스가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1173">If the function member referenced by a *base_access* is abstract, a binding-time error occurs.</span></span>

### <a name="postfix-increment-and-decrement-operators"></a><span data-ttu-id="602c5-1174">후 위 증가 및 감소 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1174">Postfix increment and decrement operators</span></span>

```antlr
post_increment_expression
    : primary_expression '++'
    ;

post_decrement_expression
    : primary_expression '--'
    ;
```

<span data-ttu-id="602c5-1175">피연산자는 후 위 증가 또는 감소 작업 변수, 속성 액세스 또는 인덱서 액세스로 분류 되는 식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1175">The operand of a postfix increment or decrement operation must be an expression classified as a variable, a property access, or an indexer access.</span></span> <span data-ttu-id="602c5-1176">작업의 결과 피연산자와 동일한 형식의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1176">The result of the operation is a value of the same type as the operand.</span></span>

<span data-ttu-id="602c5-1177">경우는 *primary_expression* 컴파일 시간 형식이 `dynamic` 연산자를 동적으로 바인딩되는 다음 ([동적 바인딩](expressions.md#dynamic-binding)), *post_increment_expression*나 *post_decrement_expression* 컴파일 시간 형식이 `dynamic` 의 런타임 형식을 사용 하 여 런타임 시 다음과 같은 규칙이 적용 됩니다는 *primary_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1177">If the *primary_expression* has the compile-time type `dynamic` then the operator is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)), the *post_increment_expression* or *post_decrement_expression* has the compile-time type `dynamic` and the following rules are applied at run-time using the run-time type of the *primary_expression*.</span></span>

<span data-ttu-id="602c5-1178">피연산자는 후 위 증가 하는 경우 감소 작업은 속성 또는 인덱서 액세스, 속성 또는 인덱서 둘 다 있어야 합니다는 `get` 및 `set` 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1178">If the operand of a postfix increment or decrement operation is a property or indexer access, the property or indexer must have both a `get` and a `set` accessor.</span></span> <span data-ttu-id="602c5-1179">이 경우 바인딩 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1179">If this is not the case, a binding-time error occurs.</span></span>

<span data-ttu-id="602c5-1180">단항 연산자 오버 로드 확인 ([단항 연산자 오버 로드 확인](expressions.md#unary-operator-overload-resolution)) 특정 연산자 구현을 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1180">Unary operator overload resolution ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="602c5-1181">미리 정의 된 `++` 하 고 `--` 연산자는 다음 형식에 대해 존재: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char` 를 `float`, `double`, `decimal`, 및 열거형 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1181">Predefined `++` and `--` operators exist for the following types: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, and any enum type.</span></span> <span data-ttu-id="602c5-1182">미리 정의 된 `++` 연산자는 피연산자 및 미리 정의 된에 1을 추가 하 여 생성 한 값을 반환 `--` 연산자는 피연산자에서 1을 뺀 값으로 계산 된 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1182">The predefined `++` operators return the value produced by adding 1 to the operand, and the predefined `--` operators return the value produced by subtracting 1 from the operand.</span></span> <span data-ttu-id="602c5-1183">에 `checked` 컨텍스트를 결과 형식이 정수 계열 형식 또는 열거형 형식에는이 더하기 또는 빼기의 결과 결과 형식 범위를 벗어나는 경우는 `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1183">In a `checked` context, if the result of this addition or subtraction is outside the range of the result type and the result type is an integral type or enum type, a `System.OverflowException` is thrown.</span></span>

<span data-ttu-id="602c5-1184">후 위 증가 처리 하는 런타임 또는 폼의 작업 감소 `x++` 또는 `x--` 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1184">The run-time processing of a postfix increment or decrement operation of the form `x++` or `x--` consists of the following steps:</span></span>

*   <span data-ttu-id="602c5-1185">경우 `x` 변수로로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1185">If `x` is classified as a variable:</span></span>
    * <span data-ttu-id="602c5-1186">`x` 변수를 생성 하기 위해 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1186">`x` is evaluated to produce the variable.</span></span>
    * <span data-ttu-id="602c5-1187">변수의 `x` 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1187">The value of `x` is saved.</span></span>
    * <span data-ttu-id="602c5-1188">선택한 연산자의 저장된 된 값을 사용 하 여 호출 `x` 인수로 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1188">The selected operator is invoked with the saved value of `x` as its argument.</span></span>
    * <span data-ttu-id="602c5-1189">연산자로 반환 되는 값을 평가 하 여 지정 된 위치에 저장 됩니다 `x`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1189">The value returned by the operator is stored in the location given by the evaluation of `x`.</span></span>
    * <span data-ttu-id="602c5-1190">저장된 된 값의 `x` 연산의 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1190">The saved value of `x` becomes the result of the operation.</span></span>
*   <span data-ttu-id="602c5-1191">경우 `x` 속성 또는 인덱서에 액세스로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1191">If `x` is classified as a property or indexer access:</span></span>
    * <span data-ttu-id="602c5-1192">인스턴스 식 (하는 경우 `x` 아닙니다 `static`) 및 인수 목록을 (경우 `x` 인덱서 액세스할)와 연결 된 `x` 평가 결과에서 사용 하는 후속 `get` 및 `set` 접근자 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1192">The instance expression (if `x` is not `static`) and the argument list (if `x` is an indexer access) associated with `x` are evaluated, and the results are used in the subsequent `get` and `set` accessor invocations.</span></span>
    * <span data-ttu-id="602c5-1193">`get` 접근자의 `x` 가 호출 하 고 반환 된 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1193">The `get` accessor of `x` is invoked and the returned value is saved.</span></span>
    * <span data-ttu-id="602c5-1194">선택한 연산자의 저장된 된 값을 사용 하 여 호출 `x` 인수로 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1194">The selected operator is invoked with the saved value of `x` as its argument.</span></span>
    * <span data-ttu-id="602c5-1195">합니다 `set` 의 접근자 `x` 으로 연산자로 반환 되는 값을 사용 하 여 호출 해당 `value` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1195">The `set` accessor of `x` is invoked with the value returned by the operator as its `value` argument.</span></span>
    * <span data-ttu-id="602c5-1196">저장된 된 값의 `x` 연산의 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1196">The saved value of `x` becomes the result of the operation.</span></span>

<span data-ttu-id="602c5-1197">합니다 `++` 하 고 `--` 연산자에도 접두사 표기법 지원 ([전위 증가 및 감소 연산자](expressions.md#prefix-increment-and-decrement-operators)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1197">The `++` and `--` operators also support prefix notation ([Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)).</span></span> <span data-ttu-id="602c5-1198">일반적으로 결과 `x++` 또는 `x--` 의 값인 `x` 작업 전에 반면 결과인 `++x` 또는 `--x` 의 값인 `x` 작업 후.</span><span class="sxs-lookup"><span data-stu-id="602c5-1198">Typically, the result of `x++` or `x--` is the value of `x` before the operation, whereas the result of `++x` or `--x` is the value of `x` after the operation.</span></span> <span data-ttu-id="602c5-1199">두 경우 모두 `x` 작업 후 같은 값을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1199">In either case, `x` itself has the same value after the operation.</span></span>

<span data-ttu-id="602c5-1200">`operator ++` 또는 `operator --` 구현 후 위 또는 접두사 표기법을 사용 하 여 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1200">An `operator ++` or `operator --` implementation can be invoked using either postfix or prefix notation.</span></span> <span data-ttu-id="602c5-1201">두 표기법이 대 한 별도 연산자 구현이 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1201">It is not possible to have separate operator implementations for the two notations.</span></span>

### <a name="the-new-operator"></a><span data-ttu-id="602c5-1202">new 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1202">The new operator</span></span>

<span data-ttu-id="602c5-1203">`new` 연산자 형식의 새 인스턴스를 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1203">The `new` operator is used to create new instances of types.</span></span>

<span data-ttu-id="602c5-1204">세 가지 `new` 식:</span><span class="sxs-lookup"><span data-stu-id="602c5-1204">There are three forms of `new` expressions:</span></span>

*  <span data-ttu-id="602c5-1205">개체 만들기 식은 클래스 형식 및 값 형식의 새 인스턴스를 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1205">Object creation expressions are used to create new instances of class types and value types.</span></span>
*  <span data-ttu-id="602c5-1206">배열 만들기 식은 배열 형식의 새 인스턴스를 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1206">Array creation expressions are used to create new instances of array types.</span></span>
*  <span data-ttu-id="602c5-1207">대리자 생성 식 형식을 대리자의 새 인스턴스를 만드는 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1207">Delegate creation expressions are used to create new instances of delegate types.</span></span>

<span data-ttu-id="602c5-1208">`new` 연산자 형식의 인스턴스를 만들 것을 의미 하지만 반드시 메모리의 동적 할당을 의미 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1208">The `new` operator implies creation of an instance of a type, but does not necessarily imply dynamic allocation of memory.</span></span> <span data-ttu-id="602c5-1209">값 형식의 인스턴스는 주는지 및 없는 동적 할당이 발생 변수 이외의 추가 메모리가 필요 하는 특히 때 `new` 값 형식의 인스턴스를 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1209">In particular, instances of value types require no additional memory beyond the variables in which they reside, and no dynamic allocations occur when `new` is used to create instances of value types.</span></span>

#### <a name="object-creation-expressions"></a><span data-ttu-id="602c5-1210">개체 만들기 식</span><span class="sxs-lookup"><span data-stu-id="602c5-1210">Object creation expressions</span></span>

<span data-ttu-id="602c5-1211">*object_creation_expression* 의 새 인스턴스를 만드는 데 사용 되는 *class_type* 또는 *value_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1211">An *object_creation_expression* is used to create a new instance of a *class_type* or a *value_type*.</span></span>

```antlr
object_creation_expression
    : 'new' type '(' argument_list? ')' object_or_collection_initializer?
    | 'new' type object_or_collection_initializer
    ;

object_or_collection_initializer
    : object_initializer
    | collection_initializer
    ;
```

<span data-ttu-id="602c5-1212">합니다 *형식* 의 *object_creation_expression* 이어야 합니다는 *class_type*, *value_type* 또는 *type_parameter* .</span><span class="sxs-lookup"><span data-stu-id="602c5-1212">The *type* of an *object_creation_expression* must be a *class_type*, a *value_type* or a *type_parameter*.</span></span> <span data-ttu-id="602c5-1213">합니다 *형식* 일 수 없습니다는 `abstract` *class_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1213">The *type* cannot be an `abstract` *class_type*.</span></span>

<span data-ttu-id="602c5-1214">선택적 *argument_list* ([인수 목록](expressions.md#argument-lists)) 경우에 허용 됩니다는 *형식* 되는 *class_type* 또는 *struct_ 형식*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1214">The optional *argument_list* ([Argument lists](expressions.md#argument-lists)) is permitted only if the *type* is a *class_type* or a *struct_type*.</span></span>

<span data-ttu-id="602c5-1215">개체 생성 식을 생성자 인수 목록을 생략할 수 및 개체 이니셜라이저 또는 컬렉션 이니셜라이저를 포함 하는 제공 된 바깥쪽 괄호입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1215">An object creation expression can omit the constructor argument list and enclosing parentheses provided it includes an object initializer or collection initializer.</span></span> <span data-ttu-id="602c5-1216">생성자 인수 목록을 생략 하 고 괄호 빈 인수 목록에 지정 하는 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1216">Omitting the constructor argument list and enclosing parentheses is equivalent to specifying an empty argument list.</span></span>

<span data-ttu-id="602c5-1217">먼저 인스턴스 생성자를 처리 하 고 개체 이니셜라이저 (지정된멤버또는요소초기화를처리하는다음개체이니셜라이저또는컬렉션이니셜라이저를포함하는개체생성식처리구성[ 개체 이니셜라이저](expressions.md#object-initializers)) 또는 컬렉션 이니셜라이저 ([컬렉션 이니셜라이저](expressions.md#collection-initializers)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1217">Processing of an object creation expression that includes an object initializer or collection initializer consists of first processing the instance constructor and then processing the member or element initializations specified by the object initializer ([Object initializers](expressions.md#object-initializers)) or collection initializer ([Collection initializers](expressions.md#collection-initializers)).</span></span>

<span data-ttu-id="602c5-1218">선택적 인수 중 하나가 되 면 *argument_list* 컴파일 시간 형식이 `dynamic` 하면 *object_creation_expression* 바인딩된 동적으로 ([동적바인딩](expressions.md#dynamic-binding)) 이러한 인수의 런타임 형식을 사용 하 여 런타임 시 다음과 같은 규칙이 적용 됩니다는 *argument_list* 컴파일 타임 형식에 있는 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1218">If any of the arguments in the optional *argument_list* has the compile-time type `dynamic` then the *object_creation_expression* is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)) and the following rules are applied at run-time using the run-time type of those arguments of the *argument_list* that have the compile time type `dynamic`.</span></span> <span data-ttu-id="602c5-1219">에 설명 된 대로 개체 만들기를 제한 된 컴파일 시간 검사를 수행 하는 반면 [컴파일 타임 동적 오버 로드 확인 검사](expressions.md#compile-time-checking-of-dynamic-overload-resolution)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1219">However, the object creation undergoes a limited compile time check as described in [Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span></span>

<span data-ttu-id="602c5-1220">바인딩 시간 처리를 *object_creation_expression* 형식의 `new T(A)`여기서 `T` 는 *class_type* 또는 *value_type* 및 `A` 선택적 *argument_list*, 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1220">The binding-time processing of an *object_creation_expression* of the form `new T(A)`, where `T` is a *class_type* or a *value_type* and `A` is an optional *argument_list*, consists of the following steps:</span></span>

*   <span data-ttu-id="602c5-1221">하는 경우 `T` 되는 *value_type* 및 `A` 없는:</span><span class="sxs-lookup"><span data-stu-id="602c5-1221">If `T` is a *value_type* and `A` is not present:</span></span>
    * <span data-ttu-id="602c5-1222">합니다 *object_creation_expression* 는 기본 생성자 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1222">The *object_creation_expression* is a default constructor invocation.</span></span> <span data-ttu-id="602c5-1223">결과 *object_creation_expression* 형식의 값은 `T`를 namely에 대 한 기본 값 `T` 에 정의 된 대로 [The System.ValueType 형식](types.md#the-systemvaluetype-type)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1223">The result of the *object_creation_expression* is a value of type `T`, namely the default value for `T` as defined in [The System.ValueType type](types.md#the-systemvaluetype-type).</span></span>
*   <span data-ttu-id="602c5-1224">그렇지 `T` 되는 *type_parameter* 및 `A` 없는:</span><span class="sxs-lookup"><span data-stu-id="602c5-1224">Otherwise, if `T` is a *type_parameter* and `A` is not present:</span></span>
    * <span data-ttu-id="602c5-1225">값 형식 제약 조건 또는 생성자 제약 조건이 없는 경우 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints))에 대 한 지정 된 `T`, 바인딩 시간에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1225">If no value type constraint or constructor constraint ([Type parameter constraints](classes.md#type-parameter-constraints)) has been specified for `T`, a binding-time error occurs.</span></span>
    * <span data-ttu-id="602c5-1226">결과 *object_creation_expression* 런타임 형식에 바인딩된 형식 매개 변수 값은 해당 형식의 기본 생성자를 호출한 결과로 namely 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1226">The result of the *object_creation_expression* is a value of the run-time type that the type parameter has been bound to, namely the result of invoking the default constructor of that type.</span></span> <span data-ttu-id="602c5-1227">런타임 형식에는 참조 형식 또는 값 형식 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1227">The run-time type may be a reference type or a value type.</span></span>
*   <span data-ttu-id="602c5-1228">그렇지 않고 `T` 되는 *class_type* 또는 *struct_type*:</span><span class="sxs-lookup"><span data-stu-id="602c5-1228">Otherwise, if `T` is a *class_type* or a *struct_type*:</span></span>
    * <span data-ttu-id="602c5-1229">하는 경우 `T` 은 `abstract` *class_type*, 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1229">If `T` is an `abstract` *class_type*, a compile-time error occurs.</span></span>
    * <span data-ttu-id="602c5-1230">호출할 인스턴스 생성자의 오버 로드 확인 규칙을 사용 하 여 결정 됩니다 [오버 로드 확인](expressions.md#overload-resolution)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1230">The instance constructor to invoke is determined using the overload resolution rules of [Overload resolution](expressions.md#overload-resolution).</span></span> <span data-ttu-id="602c5-1231">후보 인스턴스 생성자의 집합은 구성에서 선언 된 모든 액세스 가능한 인스턴스 생성자 `T` 을 기준으로 적용할 수 있는 `A` ([적용 가능한 함수 멤버](expressions.md#applicable-function-member)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1231">The set of candidate instance constructors consists of all accessible instance constructors declared in `T` which are applicable with respect to `A` ([Applicable function member](expressions.md#applicable-function-member)).</span></span> <span data-ttu-id="602c5-1232">후보 인스턴스 생성자의 집합이 비어 있는 경우, 단일 최상의 인스턴스 생성자를 식별할 수 없는 경우 바인딩을 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1232">If the set of candidate instance constructors is empty, or if a single best instance constructor cannot be identified, a binding-time error occurs.</span></span>
    * <span data-ttu-id="602c5-1233">결과 *object_creation_expression* 형식의 값은 `T`, 즉 위의 단계에서 결정 인스턴스 생성자를 호출 하 여 생성 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1233">The result of the *object_creation_expression* is a value of type `T`, namely the value produced by invoking the instance constructor determined in the step above.</span></span>
*  <span data-ttu-id="602c5-1234">이 고, 그렇지 합니다 *object_creation_expression* 유효 하지 않은 바인딩 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1234">Otherwise, the *object_creation_expression* is invalid, and a binding-time error occurs.</span></span>

<span data-ttu-id="602c5-1235">경우에 합니다 *object_creation_expression* 동적으로 바인딩된 컴파일 타임 형식은 여전히 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1235">Even if the *object_creation_expression* is dynamically bound, the compile-time type is still `T`.</span></span>

<span data-ttu-id="602c5-1236">런타임 처리를 *object_creation_expression* 양식의 `new T(A)`여기서 `T` 은 *class_type* 또는 *struct_type* 및 `A` 선택적 *argument_list*, 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1236">The run-time processing of an *object_creation_expression* of the form `new T(A)`, where `T` is *class_type* or a *struct_type* and `A` is an optional *argument_list*, consists of the following steps:</span></span>

*   <span data-ttu-id="602c5-1237">하는 경우 `T` 되는 *class_type*:</span><span class="sxs-lookup"><span data-stu-id="602c5-1237">If `T` is a *class_type*:</span></span>
    * <span data-ttu-id="602c5-1238">클래스의 새 인스턴스를 `T` 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1238">A new instance of class `T` is allocated.</span></span> <span data-ttu-id="602c5-1239">새 인스턴스를 할당할 수 있는 충분 한 메모리가 없을 경우는 `System.OutOfMemoryException` throw 되 고 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1239">If there is not enough memory available to allocate the new instance, a `System.OutOfMemoryException` is thrown and no further steps are executed.</span></span>
    * <span data-ttu-id="602c5-1240">새 인스턴스의 모든 필드를 기본값으로 초기화 됩니다 ([기본값](variables.md#default-values)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1240">All fields of the new instance are initialized to their default values ([Default values](variables.md#default-values)).</span></span>
    * <span data-ttu-id="602c5-1241">함수 멤버 호출 규칙에 따라 인스턴스 생성자가 호출 됩니다 ([컴파일 타임 동적 오버 로드 확인 검사](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1241">The instance constructor is invoked according to the rules of function member invocation ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span></span> <span data-ttu-id="602c5-1242">새로 할당 된 인스턴스에 대 한 참조를 자동으로 인스턴스 생성자에 전달 하 고 해당 생성자 내에서 인스턴스를 액세스할 수 있습니다 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1242">A reference to the newly allocated instance is automatically passed to the instance constructor and the instance can be accessed from within that constructor as `this`.</span></span>
*   <span data-ttu-id="602c5-1243">하는 경우 `T` 되는 *struct_type*:</span><span class="sxs-lookup"><span data-stu-id="602c5-1243">If `T` is a *struct_type*:</span></span>
    * <span data-ttu-id="602c5-1244">형식의 인스턴스로 `T` 임시 로컬 변수를 할당 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1244">An instance of type `T` is created by allocating a temporary local variable.</span></span> <span data-ttu-id="602c5-1245">인스턴스 생성자를 이후를 *struct_type* 확실 하 게 임시 변수의 초기화가 반드시 생성 되는 인스턴스의 각 필드에 값을 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1245">Since an instance constructor of a *struct_type* is required to definitely assign a value to each field of the instance being created, no initialization of the temporary variable is necessary.</span></span>
    * <span data-ttu-id="602c5-1246">함수 멤버 호출 규칙에 따라 인스턴스 생성자가 호출 됩니다 ([컴파일 타임 동적 오버 로드 확인 검사](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1246">The instance constructor is invoked according to the rules of function member invocation ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span></span> <span data-ttu-id="602c5-1247">새로 할당 된 인스턴스에 대 한 참조를 자동으로 인스턴스 생성자에 전달 하 고 해당 생성자 내에서 인스턴스를 액세스할 수 있습니다 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1247">A reference to the newly allocated instance is automatically passed to the instance constructor and the instance can be accessed from within that constructor as `this`.</span></span>

#### <a name="object-initializers"></a><span data-ttu-id="602c5-1248">개체 이니셜라이저</span><span class="sxs-lookup"><span data-stu-id="602c5-1248">Object initializers</span></span>

<span data-ttu-id="602c5-1249">***개체 이니셜라이저*** 0 개 이상의 필드, 속성 또는 개체의 인덱싱된 요소에 대 한 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1249">An ***object initializer*** specifies values for zero or more fields, properties or indexed elements of an object.</span></span>

```antlr
object_initializer
    : '{' member_initializer_list? '}'
    | '{' member_initializer_list ',' '}'
    ;

member_initializer_list
    : member_initializer (',' member_initializer)*
    ;

member_initializer
    : initializer_target '=' initializer_value
    ;

initializer_target
    : identifier
    | '[' argument_list ']'
    ;

initializer_value
    : expression
    | object_or_collection_initializer
    ;
```

<span data-ttu-id="602c5-1250">개체 이니셜라이저로 묶인 멤버 이니셜라이저의 시퀀스로 구성 됩니다 `{` 고 `}` 토큰 및 쉼표로 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1250">An object initializer consists of a sequence of member initializers, enclosed by `{` and `}` tokens and separated by commas.</span></span> <span data-ttu-id="602c5-1251">각 *member_initializer* 초기화에 대 한 대상을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1251">Each *member_initializer* designates a target for the initialization.</span></span> <span data-ttu-id="602c5-1252">*식별자* 반면는 액세스할 수 있는 필드 또는 속성 초기화 되는 개체의 이름을 지정 해야는 *argument_list* 묶인 대괄호에 액세스할 수 있는 인덱서 인수를 지정 해야 합니다 초기화 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1252">An *identifier* must name an accessible field or property of the object being initialized, whereas an *argument_list* enclosed in square brackets must specify arguments for an accessible indexer on the object being initialized.</span></span> <span data-ttu-id="602c5-1253">이 동일한 필드 또는 속성에 대해 둘 이상의 멤버 이니셜라이저를 포함 하도록 개체 이니셜라이저에 대 한 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1253">It is an error for an object initializer to include more than one member initializer for the same field or property.</span></span>

<span data-ttu-id="602c5-1254">각 *initializer_target* 등호 식, 개체 이니셜라이저 또는 컬렉션 이니셜라이저를 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1254">Each *initializer_target* is followed by an equals sign and either an expression, an object initializer or a collection initializer.</span></span> <span data-ttu-id="602c5-1255">개체 이니셜라이저를 초기화 하 고 새로 만든된 개체를 참조 하려면 내의 식에서 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1255">It is not possible for expressions within the object initializer to refer to the newly created object it is initializing.</span></span>

<span data-ttu-id="602c5-1256">등호 기호 할당으로 동일한 방식으로 처리 된 후 식을 지정 하는 멤버 이니셜라이저 ([단순 할당](expressions.md#simple-assignment)) 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1256">A member initializer that specifies an expression after the equals sign is processed in the same way as an assignment ([Simple assignment](expressions.md#simple-assignment)) to the target.</span></span>

<span data-ttu-id="602c5-1257">등호 되 면 개체 이니셜라이저를 지정 하는 멤버 이니셜라이저는 ***중첩 된 개체 이니셜라이저***, 즉, 포함된 된 개체의 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1257">A member initializer that specifies an object initializer after the equals sign is a ***nested object initializer***, i.e. an initialization of an embedded object.</span></span> <span data-ttu-id="602c5-1258">필드 또는 속성에는 새 값을 할당 하는 대신 중첩된 개체 이니셜라이저에서 할당 필드 또는 속성의 멤버에 대 한 할당으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1258">Instead of assigning a new value to the field or property, the assignments in the nested object initializer are treated as assignments to members of the field or property.</span></span> <span data-ttu-id="602c5-1259">값 형식 사용 하 여 읽기 전용 필드 또는 속성으로 값 형식에 중첩 된 개체 이니셜라이저를 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1259">Nested object initializers cannot be applied to properties with a value type, or to read-only fields with a value type.</span></span>

<span data-ttu-id="602c5-1260">등호 기호 뒤 컬렉션 이니셜라이저를 지정 하는 멤버 이니셜라이저는 포함 된 컬렉션을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1260">A member initializer that specifies a collection initializer after the equals sign is an initialization of an embedded collection.</span></span> <span data-ttu-id="602c5-1261">새 컬렉션에는 대상 필드, 속성 또는 인덱서에를 할당 하는 대신 이니셜라이저에 지정 된 요소는 대상에서 참조 하는 컬렉션에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1261">Instead of assigning a new collection to the target field, property or indexer, the elements given in the initializer are added to the collection referenced by the target.</span></span> <span data-ttu-id="602c5-1262">대상에 지정 된 요구 사항을 충족 하는 컬렉션 형식 이어야 합니다 [컬렉션 이니셜라이저](expressions.md#collection-initializers)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1262">The target must be of a collection type that satisfies the requirements specified in [Collection initializers](expressions.md#collection-initializers).</span></span>

<span data-ttu-id="602c5-1263">인덱스 이니셜라이저에 대 한 인수는 정확히 한 번만 항상 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1263">The arguments to an index initializer will always be evaluated exactly once.</span></span> <span data-ttu-id="602c5-1264">따라서 인수를 종료 하지 않습니다 (예: 중첩 된 빈 이니셜라이저)으로 인해 사용 시작 하는 경우에 해당 파생 작업에 대해 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1264">Thus, even if the arguments end up never getting used (e.g. because of an empty nested initializer), they will be evaluated for their side effects.</span></span>

<span data-ttu-id="602c5-1265">다음 클래스는 두 개의 좌표를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1265">The following class represents a point with two coordinates:</span></span>
```csharp
public class Point
{
    int x, y;

    public int X { get { return x; } set { x = value; } }
    public int Y { get { return y; } set { y = value; } }
}
```

<span data-ttu-id="602c5-1266">인스턴스의 `Point` 만들고 다음과 같이 초기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1266">An instance of `Point` can be created and initialized as follows:</span></span>
```csharp
Point a = new Point { X = 0, Y = 1 };
```
<span data-ttu-id="602c5-1267">하는 것과 동일한 효과가 있습니까</span><span class="sxs-lookup"><span data-stu-id="602c5-1267">which has the same effect as</span></span>
```csharp
Point __a = new Point();
__a.X = 0;
__a.Y = 1; 
Point a = __a;
```
<span data-ttu-id="602c5-1268">여기서 `__a` 그렇지 않으면 보이지 않는 하 고 액세스할 수 없는 임시 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1268">where `__a` is an otherwise invisible and inaccessible temporary variable.</span></span> <span data-ttu-id="602c5-1269">다음 클래스는 두 지점에서 생성 하는 사각형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1269">The following class represents a rectangle created from two points:</span></span>
```csharp
public class Rectangle
{
    Point p1, p2;

    public Point P1 { get { return p1; } set { p1 = value; } }
    public Point P2 { get { return p2; } set { p2 = value; } }
}
```

<span data-ttu-id="602c5-1270">인스턴스의 `Rectangle` 만들고 다음과 같이 초기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1270">An instance of `Rectangle` can be created and initialized as follows:</span></span>
```csharp
Rectangle r = new Rectangle {
    P1 = new Point { X = 0, Y = 1 },
    P2 = new Point { X = 2, Y = 3 }
};
```
<span data-ttu-id="602c5-1271">하는 것과 동일한 효과가 있습니까</span><span class="sxs-lookup"><span data-stu-id="602c5-1271">which has the same effect as</span></span>
```csharp
Rectangle __r = new Rectangle();
Point __p1 = new Point();
__p1.X = 0;
__p1.Y = 1;
__r.P1 = __p1;
Point __p2 = new Point();
__p2.X = 2;
__p2.Y = 3;
__r.P2 = __p2; 
Rectangle r = __r;
```
<span data-ttu-id="602c5-1272">여기서 `__r`, `__p1` 및 `__p2` 보이지 않는 및 액세스할 수 있는 임시 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1272">where `__r`, `__p1` and `__p2` are temporary variables that are otherwise invisible and inaccessible.</span></span>

<span data-ttu-id="602c5-1273">하는 경우 `Rectangle`의 생성자에 포함 된 두 할당 `Point` 인스턴스</span><span class="sxs-lookup"><span data-stu-id="602c5-1273">If `Rectangle`'s constructor allocates the two embedded `Point` instances</span></span>
```csharp
public class Rectangle
{
    Point p1 = new Point();
    Point p2 = new Point();

    public Point P1 { get { return p1; } }
    public Point P2 { get { return p2; } }
}
```
<span data-ttu-id="602c5-1274">다음 구문은 수 포함 된 초기화 `Point` 새 인스턴스를 할당 하는 대신 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="602c5-1274">the following construct can be used to initialize the embedded `Point` instances instead of assigning new instances:</span></span>
```csharp
Rectangle r = new Rectangle {
    P1 = { X = 0, Y = 1 },
    P2 = { X = 2, Y = 3 }
};
```
<span data-ttu-id="602c5-1275">하는 것과 동일한 효과가 있습니까</span><span class="sxs-lookup"><span data-stu-id="602c5-1275">which has the same effect as</span></span>
```csharp
Rectangle __r = new Rectangle();
__r.P1.X = 0;
__r.P1.Y = 1;
__r.P2.X = 2;
__r.P2.Y = 3;
Rectangle r = __r;
```

<span data-ttu-id="602c5-1276">다음 예제에서는 C의 적절 한 정의 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1276">Given an appropriate definition of C, the following example:</span></span>
```csharp
var c = new C {
    x = true,
    y = { a = "Hello" },
    z = { 1, 2, 3 },
    ["x"] = 5,
    [0,0] = { "a", "b" },
    [1,2] = {}
};
```
<span data-ttu-id="602c5-1277">이 시리즈 할당의 결과가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1277">is equivalent to this series of assignments:</span></span>
```csharp
C __c = new C();
__c.x = true;
__c.y.a = "Hello";
__c.z.Add(1); 
__c.z.Add(2);
__c.z.Add(3);
string __i1 = "x";
__c[__i1] = 5;
int __i2 = 0, __i3 = 0;
__c[__i2,__i3].Add("a");
__c[__i2,__i3].Add("b");
int __i4 = 1, __i5 = 2;
var c = __c;
```
<span data-ttu-id="602c5-1278">여기서 `__c`등 보이지 않는 및 소스 코드에 액세스할 수 없게 되는 생성 된 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1278">where `__c`, etc., are generated variables that are invisible and inaccessible to the source code.</span></span> <span data-ttu-id="602c5-1279">인수 `[0,0]` 평가 한 번만, 및에 대 한 인수는 `[1,2]` 사용 되지 않기에 한 번 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1279">Note that the arguments for `[0,0]` are evaluated only once, and the arguments for `[1,2]` are evaluated once even though they are never used.</span></span>

#### <a name="collection-initializers"></a><span data-ttu-id="602c5-1280">컬렉션 이니셜라이저</span><span class="sxs-lookup"><span data-stu-id="602c5-1280">Collection initializers</span></span>

<span data-ttu-id="602c5-1281">컬렉션 이니셜라이저를 컬렉션의 요소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1281">A collection initializer specifies the elements of a collection.</span></span>

```antlr
collection_initializer
    : '{' element_initializer_list '}'
    | '{' element_initializer_list ',' '}'
    ;

element_initializer_list
    : element_initializer (',' element_initializer)*
    ;

element_initializer
    : non_assignment_expression
    | '{' expression_list '}'
    ;

expression_list
    : expression (',' expression)*
    ;
```

<span data-ttu-id="602c5-1282">컬렉션 이니셜라이저를 묶어 요소 이니셜라이저의 시퀀스로 구성 됩니다 `{` 고 `}` 토큰 및 쉼표로 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1282">A collection initializer consists of a sequence of element initializers, enclosed by `{` and `}` tokens and separated by commas.</span></span> <span data-ttu-id="602c5-1283">초기화 되는 컬렉션 개체에 추가할 요소를 지정 하 고로 묶인 식의 목록으로 구성 하는 각 요소 이니셜라이저 `{` 고 `}` 토큰 및 쉼표로 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1283">Each element initializer specifies an element to be added to the collection object being initialized, and consists of a list of expressions enclosed by `{` and `}` tokens and separated by commas.</span></span>  <span data-ttu-id="602c5-1284">단일 식 요소 이니셜라이저를 괄호 없이 작성할 수 있지만 할당 식 멤버 이니셜라이저를 사용 하 여 모호성을 피하기 위해 됩니다 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1284">A single-expression element initializer can be written without braces, but cannot then be an assignment expression, to avoid ambiguity with member initializers.</span></span> <span data-ttu-id="602c5-1285">합니다 *non_assignment_expression* 프로덕션에 정의 된 [식](expressions.md#expression)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1285">The *non_assignment_expression* production is defined in [Expression](expressions.md#expression).</span></span>

<span data-ttu-id="602c5-1286">다음은 컬렉션 이니셜라이저를 포함 하는 개체 생성 식의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1286">The following is an example of an object creation expression that includes a collection initializer:</span></span>
```csharp
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
```

<span data-ttu-id="602c5-1287">컬렉션 이니셜라이저를 적용 되는 컬렉션 개체를 구현 하는 형식 이어야 합니다 `System.Collections.IEnumerable` 했거나 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1287">The collection object to which a collection initializer is applied must be of a type that implements `System.Collections.IEnumerable` or a compile-time error occurs.</span></span> <span data-ttu-id="602c5-1288">컬렉션 이니셜라이저를 호출 하는 순서로 지정 된 요소 각각에 대 한는 `Add` 대상 메서드 일반 멤버 조회 적용 인수 목록과 식 목록을 요소 이니셜라이저를 사용 하 여 개체 및 오버 로드를 호출할 때마다 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1288">For each specified element in order, the collection initializer invokes an `Add` method on the target object with the expression list of the element initializer as argument list, applying normal member lookup and overload resolution for each invocation.</span></span> <span data-ttu-id="602c5-1289">따라서 컬렉션 개체는 해당 인스턴스 또는 확장 메서드 이름의 있어야 `Add` 각 요소 이니셜라이저에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1289">Thus, the collection object must have an applicable instance or extension method with the name `Add` for each element initializer.</span></span>

<span data-ttu-id="602c5-1290">다음 클래스 이름과 전화 번호 목록을 사용 하 여 연락처를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1290">The following class represents a contact with a name and a list of phone numbers:</span></span>
```csharp
public class Contact
{
    string name;
    List<string> phoneNumbers = new List<string>();

    public string Name { get { return name; } set { name = value; } }

    public List<string> PhoneNumbers { get { return phoneNumbers; } }
}
```

<span data-ttu-id="602c5-1291">`List<Contact>` 만들고 다음과 같이 초기화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1291">A `List<Contact>` can be created and initialized as follows:</span></span>
```csharp
var contacts = new List<Contact> {
    new Contact {
        Name = "Chris Smith",
        PhoneNumbers = { "206-555-0101", "425-882-8080" }
    },
    new Contact {
        Name = "Bob Harris",
        PhoneNumbers = { "650-555-0199" }
    }
};
```
<span data-ttu-id="602c5-1292">하는 것과 동일한 효과가 있습니까</span><span class="sxs-lookup"><span data-stu-id="602c5-1292">which has the same effect as</span></span>
```csharp
var __clist = new List<Contact>();
Contact __c1 = new Contact();
__c1.Name = "Chris Smith";
__c1.PhoneNumbers.Add("206-555-0101");
__c1.PhoneNumbers.Add("425-882-8080");
__clist.Add(__c1);
Contact __c2 = new Contact();
__c2.Name = "Bob Harris";
__c2.PhoneNumbers.Add("650-555-0199");
__clist.Add(__c2);
var contacts = __clist;
```
<span data-ttu-id="602c5-1293">여기서 `__clist`, `__c1` 및 `__c2` 보이지 않는 및 액세스할 수 있는 임시 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1293">where `__clist`, `__c1` and `__c2` are temporary variables that are otherwise invisible and inaccessible.</span></span>

#### <a name="array-creation-expressions"></a><span data-ttu-id="602c5-1294">배열 만들기 식</span><span class="sxs-lookup"><span data-stu-id="602c5-1294">Array creation expressions</span></span>

<span data-ttu-id="602c5-1295">*array_creation_expression* 의 새 인스턴스를 만드는 데 사용 되는 *array_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1295">An *array_creation_expression* is used to create a new instance of an *array_type*.</span></span>

```antlr
array_creation_expression
    : 'new' non_array_type '[' expression_list ']' rank_specifier* array_initializer?
    | 'new' array_type array_initializer
    | 'new' rank_specifier array_initializer
    ;
```

<span data-ttu-id="602c5-1296">첫 번째 폼의 배열 만들기 식을 식 목록에서 삭제 하는 각 개별 식의 결과로 생성 되는 형식의 배열 인스턴스를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1296">An array creation expression of the first form allocates an array instance of the type that results from deleting each of the individual expressions from the expression list.</span></span> <span data-ttu-id="602c5-1297">배열 생성 식 예를 들어 `new int[10,20]` 형식의 배열 인스턴스 생성 `int[,]`, 및 배열 만들기 식을 `new int[10][,]` 형식의 배열을 생성 `int[][,]`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1297">For example, the array creation expression `new int[10,20]` produces an array instance of type `int[,]`, and the array creation expression `new int[10][,]` produces an array of type `int[][,]`.</span></span> <span data-ttu-id="602c5-1298">식 목록에서 각 식 형식 이어야 합니다 `int`, `uint`를 `long`, 또는 `ulong`, 또는 이러한 형식 중 하나 이상의 암시적으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1298">Each expression in the expression list must be of type `int`, `uint`, `long`, or `ulong`, or implicitly convertible to one or more of these types.</span></span> <span data-ttu-id="602c5-1299">각 식의 값을 새로 할당 된 배열 인스턴스에 해당 차원의 길이 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1299">The value of each expression determines the length of the corresponding dimension in the newly allocated array instance.</span></span> <span data-ttu-id="602c5-1300">배열 차원의 길이 음수가 아니어야 합니다, 이므로 할는 컴파일 타임 오류를 *constant_expression* 식 목록에 음수 값을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1300">Since the length of an array dimension must be nonnegative, it is a compile-time error to have a *constant_expression* with a negative value in the expression list.</span></span>

<span data-ttu-id="602c5-1301">안전 하지 않은 컨텍스트에서 제외 하 고 ([안전 하지 않은 컨텍스트](unsafe-code.md#unsafe-contexts)), 배열 레이아웃 지정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1301">Except in an unsafe context ([Unsafe contexts](unsafe-code.md#unsafe-contexts)), the layout of arrays is unspecified.</span></span>

<span data-ttu-id="602c5-1302">첫 번째 폼의 배열 만들기 식을 배열 이니셜라이저를 포함 하는 경우 식 목록에서 각 식에는 상수 여야 합니다. 및 식 목록으로 지정 된 순위 및 차원 길이 배열 이니셜라이저의 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1302">If an array creation expression of the first form includes an array initializer, each expression in the expression list must be a constant and the rank and dimension lengths specified by the expression list must match those of the array initializer.</span></span>

<span data-ttu-id="602c5-1303">두 번째 또는 세 번째 폼의 배열 만들기 식을 배열 이니셜라이저는 지정 된 배열 형식 또는 차수 지정자의 순위 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1303">In an array creation expression of the second or third form, the rank of the specified array type or rank specifier must match that of the array initializer.</span></span> <span data-ttu-id="602c5-1304">개별 차원 길이 각 배열 이니셜라이저의 해당 중첩 수준에 있는 요소의 수에서 유추 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1304">The individual dimension lengths are inferred from the number of elements in each of the corresponding nesting levels of the array initializer.</span></span> <span data-ttu-id="602c5-1305">따라서, 다음 식은</span><span class="sxs-lookup"><span data-stu-id="602c5-1305">Thus, the expression</span></span>
```csharp
new int[,] {{0, 1}, {2, 3}, {4, 5}}
```
<span data-ttu-id="602c5-1306">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1306">exactly corresponds to</span></span>
```csharp
new int[3, 2] {{0, 1}, {2, 3}, {4, 5}}
```

<span data-ttu-id="602c5-1307">세 번째 형식의 배열 생성 식 이라고 하는 ***배열 생성 식에 암시적으로 형식화***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1307">An array creation expression of the third form is referred to as an ***implicitly typed array creation expression***.</span></span> <span data-ttu-id="602c5-1308">배열의 요소 형식을 명시적으로 지정 하지 않으면 하지만 가장 일반적인 형식으로 결정 한다는 점을 제외 하면 두 번째 형태에서 유사한 것 ([가장 일반적인 유형의 식 집합을 찾는](expressions.md#finding-the-best-common-type-of-a-set-of-expressions)) 배열에 있는 식 집합의 이니셜라이저입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1308">It is similar to the second form, except that the element type of the array is not explicitly given, but determined as the best common type ([Finding the best common type of a set of expressions](expressions.md#finding-the-best-common-type-of-a-set-of-expressions)) of the set of expressions in the array initializer.</span></span> <span data-ttu-id="602c5-1309">다차원 배열에 대 한 곳, 즉 합니다 *rank_specifier* 하나 이상의 쉼표가 포함 되어이 모든 구성 *식*가 있는 중첩 *array_initializer*s입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1309">For a multidimensional array, i.e., one where the *rank_specifier* contains at least one comma, this set comprises all *expression*s found in nested *array_initializer*s.</span></span>

<span data-ttu-id="602c5-1310">배열 이니셜라이저에 자세히 설명 되어 [배열 이니셜라이저](arrays.md#array-initializers)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1310">Array initializers are described further in [Array initializers](arrays.md#array-initializers).</span></span>

<span data-ttu-id="602c5-1311">배열 생성 식 평가의 결과 값을 namely 새로 할당 된 배열 인스턴스에 대 한 참조로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1311">The result of evaluating an array creation expression is classified as a value, namely a reference to the newly allocated array instance.</span></span> <span data-ttu-id="602c5-1312">배열 생성 식의 런타임 처리는 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1312">The run-time processing of an array creation expression consists of the following steps:</span></span>

*  <span data-ttu-id="602c5-1313">차원 길이 식 합니다 *expression_list* 왼쪽에서 오른쪽 순서로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1313">The dimension length expressions of the *expression_list* are evaluated in order, from left to right.</span></span> <span data-ttu-id="602c5-1314">각 식의 암시적 변환이 평가 ([암시적 변환을](conversions.md#implicit-conversions)) 다음 형식 중 하나로 수행 됩니다: `int`를 `uint`를 `long`, `ulong`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1314">Following evaluation of each expression, an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) to one of the following types is performed: `int`, `uint`, `long`, `ulong`.</span></span> <span data-ttu-id="602c5-1315">암시적 변환이 존재 하는이 목록의 첫 번째 형식이 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1315">The first type in this list for which an implicit conversion exists is chosen.</span></span> <span data-ttu-id="602c5-1316">평가 식의 후속 암시적 변환으로 인해 예외가 발생 하는 경우 다음 식은 더 이상 계산 되 고 더 이상 진행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1316">If evaluation of an expression or the subsequent implicit conversion causes an exception, then no further expressions are evaluated and no further steps are executed.</span></span>
*  <span data-ttu-id="602c5-1317">차원 길이가 계산 된 값은 다음과 같이 유효성이 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1317">The computed values for the dimension lengths are validated as follows.</span></span> <span data-ttu-id="602c5-1318">하나 이상의 값은 0 보다 작은 경우는 `System.OverflowException` throw 되 고 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1318">If one or more of the values are less than zero, a `System.OverflowException` is thrown and no further steps are executed.</span></span>
*  <span data-ttu-id="602c5-1319">지정된 된 차원의 길이 사용 하 여 배열 인스턴스가 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1319">An array instance with the given dimension lengths is allocated.</span></span> <span data-ttu-id="602c5-1320">새 인스턴스를 할당할 수 있는 충분 한 메모리가 없을 경우는 `System.OutOfMemoryException` throw 되 고 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1320">If there is not enough memory available to allocate the new instance, a `System.OutOfMemoryException` is thrown and no further steps are executed.</span></span>
*  <span data-ttu-id="602c5-1321">새 배열 인스턴스의 모든 요소를 기본값으로 초기화 됩니다 ([기본값](variables.md#default-values)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1321">All elements of the new array instance are initialized to their default values ([Default values](variables.md#default-values)).</span></span>
*  <span data-ttu-id="602c5-1322">배열 만들기 식을 배열 이니셜라이저를 포함 하는 경우 다음 배열 이니셜라이저에 각 식 평가 되 고 해당 하는 배열 요소에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1322">If the array creation expression contains an array initializer, then each expression in the array initializer is evaluated and assigned to its corresponding array element.</span></span> <span data-ttu-id="602c5-1323">평가 및 할당 식 배열 이니셜라이저에 기록 된 순서에서 수행 됩니다-즉, 요소가 오름차순 인덱스를 늘리면 먼저 오른쪽에 있는 차원입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1323">The evaluations and assignments are performed in the order the expressions are written in the array initializer—in other words, elements are initialized in increasing index order, with the rightmost dimension increasing first.</span></span> <span data-ttu-id="602c5-1324">지정된 된 식의 후속 대입 해당 배열 요소에는 평가 예외를 발생 시키는 경우 더 이상 요소가 초기화 됩니다 (고 나머지 요소를 기본값으로 되지 것입니다).</span><span class="sxs-lookup"><span data-stu-id="602c5-1324">If evaluation of a given expression or the subsequent assignment to the corresponding array element causes an exception, then no further elements are initialized (and the remaining elements will thus have their default values).</span></span>

<span data-ttu-id="602c5-1325">배열 만들기 식을 배열 형식의 요소가 있는 배열을 인스턴스화할 수 있지만 이러한 배열의 요소를 수동으로 초기화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1325">An array creation expression permits instantiation of an array with elements of an array type, but the elements of such an array must be manually initialized.</span></span> <span data-ttu-id="602c5-1326">예를 들어, 다음 문</span><span class="sxs-lookup"><span data-stu-id="602c5-1326">For example, the statement</span></span>
```csharp
int[][] a = new int[100][];
```
<span data-ttu-id="602c5-1327">형식의 요소를 100 개를 사용 하 여 1 차원 배열을 만듭니다 `int[]`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1327">creates a single-dimensional array with 100 elements of type `int[]`.</span></span> <span data-ttu-id="602c5-1328">각 요소의 초기 값은 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1328">The initial value of each element is `null`.</span></span> <span data-ttu-id="602c5-1329">또한 하위 배열과 문을 인스턴스화하기 위해 동일한 배열 생성 식에 대 한 불가능</span><span class="sxs-lookup"><span data-stu-id="602c5-1329">It is not possible for the same array creation expression to also instantiate the sub-arrays, and the statement</span></span>
```csharp
int[][] a = new int[100][5];        // Error
```
<span data-ttu-id="602c5-1330">컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1330">results in a compile-time error.</span></span> <span data-ttu-id="602c5-1331">하위 배열의 인스턴스화는 수동으로 에서처럼 대신 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1331">Instantiation of the sub-arrays must instead be performed manually, as in</span></span>
```csharp
int[][] a = new int[100][];
for (int i = 0; i < 100; i++) a[i] = new int[5];
```

<span data-ttu-id="602c5-1332">배열의 배열에 하위 배열과 길이가 같은 모든 경우는 "사각형" 셰이프를 하는 경우에 다차원 배열을 사용 하는 것이 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1332">When an array of arrays has a "rectangular" shape, that is when the sub-arrays are all of the same length, it is more efficient to use a multi-dimensional array.</span></span> <span data-ttu-id="602c5-1333">위의 예제에서는 배열의 배열 인스턴스화 101 개체를 만듭니다-하나의 외부 배열 및 100 개의 하위 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1333">In the example above, instantiation of the array of arrays creates 101 objects—one outer array and 100 sub-arrays.</span></span> <span data-ttu-id="602c5-1334">반면,</span><span class="sxs-lookup"><span data-stu-id="602c5-1334">In contrast,</span></span>
```csharp
int[,] = new int[100, 5];
```
<span data-ttu-id="602c5-1335">단일 개체만, 2 차원 배열을 만들고 단일 문에서 할당을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1335">creates only a single object, a two-dimensional array, and accomplishes the allocation in a single statement.</span></span>

<span data-ttu-id="602c5-1336">다음은 암시적으로 형식화 된 배열 생성 식의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1336">The following are examples of implicitly typed array creation expressions:</span></span>
```csharp
var a = new[] { 1, 10, 100, 1000 };                       // int[]

var b = new[] { 1, 1.5, 2, 2.5 };                         // double[]

var c = new[,] { { "hello", null }, { "world", "!" } };   // string[,]

var d = new[] { 1, "one", 2, "two" };                     // Error
```

<span data-ttu-id="602c5-1337">마지막 식 때문에 컴파일 타임 오류가 발생 하지 않습니다 `int` 나 `string` 다른 암시적으로 변환할 수 없으므로 더 가장 일반적으로 입력 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1337">The last expression causes a compile-time error because neither `int` nor `string` is implicitly convertible to the other, and so there is no best common type.</span></span> <span data-ttu-id="602c5-1338">명시적으로 형식화 된 배열 만들기 식을 사용 해야이 예제의 경우 예를 들어 형식이 되도록 지정 `object[]`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1338">An explicitly typed array creation expression must be used in this case, for example specifying the type to be `object[]`.</span></span> <span data-ttu-id="602c5-1339">또는 일반적인 기본 형식으로 유추 요소 형식 다음 요소 중 하나를 캐스팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1339">Alternatively, one of the elements can be cast to a common base type, which would then become the inferred element type.</span></span>

<span data-ttu-id="602c5-1340">익명 개체 이니셜라이저를 사용 하 여 암시적으로 형식화 된 배열 만들기 식을 결합할 수 있습니다 ([익명 개체 생성 식을](expressions.md#anonymous-object-creation-expressions)) 익명으로 만들려면 데이터 구조를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1340">Implicitly typed array creation expressions can be combined with anonymous object initializers ([Anonymous object creation expressions](expressions.md#anonymous-object-creation-expressions)) to create anonymously typed data structures.</span></span> <span data-ttu-id="602c5-1341">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="602c5-1341">For example:</span></span>
```csharp
var contacts = new[] {
    new {
        Name = "Chris Smith",
        PhoneNumbers = new[] { "206-555-0101", "425-882-8080" }
    },
    new {
        Name = "Bob Harris",
        PhoneNumbers = new[] { "650-555-0199" }
    }
};
```

#### <a name="delegate-creation-expressions"></a><span data-ttu-id="602c5-1342">대리자 생성 식</span><span class="sxs-lookup"><span data-stu-id="602c5-1342">Delegate creation expressions</span></span>

<span data-ttu-id="602c5-1343">A *delegate_creation_expression* 의 새 인스턴스를 만드는 데 사용 되는 *delegate_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1343">A *delegate_creation_expression* is used to create a new instance of a *delegate_type*.</span></span>

```antlr
delegate_creation_expression
    : 'new' delegate_type '(' expression ')'
    ;
```

<span data-ttu-id="602c5-1344">대리자 생성 식의 인수는 메서드 그룹, 익명 함수 또는 컴파일 타임 형식 값 이어야 합니다 `dynamic` 또는 *delegate_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1344">The argument of a delegate creation expression must be a method group, an anonymous function or a value of either the compile time type `dynamic` or a *delegate_type*.</span></span> <span data-ttu-id="602c5-1345">인수는 메서드 그룹 인 경우 메서드를 식별 및 인스턴스 메서드를 대리자를 만들 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1345">If the argument is a method group, it identifies the method and, for an instance method, the object for which to create a delegate.</span></span> <span data-ttu-id="602c5-1346">익명 함수 인수가 직접 매개 변수 및 대리자 대상의 메서드 본문을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1346">If the argument is an anonymous function it directly defines the parameters and method body of the delegate target.</span></span> <span data-ttu-id="602c5-1347">인수 값 이면의 복사본을 만드는 데 사용할 대리자 인스턴스를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1347">If the argument is a value it identifies a delegate instance of which to create a copy.</span></span>

<span data-ttu-id="602c5-1348">경우는 *식* 컴파일 시간 형식이 `dynamic`의 *delegate_creation_expression* 바인딩된 동적으로 ([동적 바인딩](expressions.md#dynamic-binding)), 및 아래 규칙 런타임 형식을 사용 하 여 런타임 시 적용 되는 *식*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1348">If the *expression* has the compile-time type `dynamic`, the *delegate_creation_expression* is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)), and the rules below are applied at run-time using the run-time type of the *expression*.</span></span> <span data-ttu-id="602c5-1349">그렇지 않으면 컴파일 타임에 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1349">Otherwise the rules are applied at compile-time.</span></span>

<span data-ttu-id="602c5-1350">바인딩 시간 처리를 *delegate_creation_expression* 폼의 `new D(E)`여기서 `D` 는 *delegate_type* 및 `E` 는 *식* , 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1350">The binding-time processing of a *delegate_creation_expression* of the form `new D(E)`, where `D` is a *delegate_type* and `E` is an *expression*, consists of the following steps:</span></span>

*  <span data-ttu-id="602c5-1351">하는 경우 `E` 메서드 그룹은 대리자 생성 식 메서드 그룹 변환으로 동일한 방식으로 처리 됩니다 ([메서드 그룹 변환](conversions.md#method-group-conversions))에서 `E` 에 `D`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1351">If `E` is a method group, the delegate creation expression is processed in the same way as a method group conversion ([Method group conversions](conversions.md#method-group-conversions)) from `E` to `D`.</span></span>
*  <span data-ttu-id="602c5-1352">하는 경우 `E` 는 익명 함수 대리자 생성 식 동일한 방식으로 익명 함수 변환으로 처리 됩니다 ([익명 함수 변환](conversions.md#anonymous-function-conversions))에서 `E` 에 `D`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1352">If `E` is an anonymous function, the delegate creation expression is processed in the same way as an anonymous function conversion ([Anonymous function conversions](conversions.md#anonymous-function-conversions)) from `E` to `D`.</span></span>
*  <span data-ttu-id="602c5-1353">하는 경우 `E` 값인 `E` 호환 되어야 합니다 ([대리자 선언](delegates.md#delegate-declarations))와 `D`, 결과 형식의 새로 만든된 대리자에 대 한 참조 이며 `D` 동일한 호출을 참조 하는 목록 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1353">If `E` is a value, `E` must be compatible ([Delegate declarations](delegates.md#delegate-declarations)) with `D`, and the result is a reference to a newly created delegate of type `D` that refers to the same invocation list as `E`.</span></span> <span data-ttu-id="602c5-1354">하는 경우 `E` 와 호환 되지 않습니다 `D`, 컴파일 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1354">If `E` is not compatible with `D`, a compile-time error occurs.</span></span>

<span data-ttu-id="602c5-1355">런타임 처리를 *delegate_creation_expression* 형식의 `new D(E)`여기서 `D` 는 *delegate_type* 및 `E` 가 *식* , 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1355">The run-time processing of a *delegate_creation_expression* of the form `new D(E)`, where `D` is a *delegate_type* and `E` is an *expression*, consists of the following steps:</span></span>

*   <span data-ttu-id="602c5-1356">하는 경우 `E` 메서드 그룹은 대리자 생성 식 메서드 그룹 변환으로 평가 됩니다 ([메서드 그룹 변환](conversions.md#method-group-conversions))에서 `E` 에 `D`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1356">If `E` is a method group, the delegate creation expression is evaluated as a method group conversion ([Method group conversions](conversions.md#method-group-conversions)) from `E` to `D`.</span></span>
*   <span data-ttu-id="602c5-1357">하는 경우 `E` 는 익명 함수 대리자 만들기는 익명 함수 변환으로 평가 됩니다 `E` 하 `D` ([익명 함수 변환](conversions.md#anonymous-function-conversions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1357">If `E` is an anonymous function, the delegate creation is evaluated as an anonymous function conversion from `E` to `D` ([Anonymous function conversions](conversions.md#anonymous-function-conversions)).</span></span>
*   <span data-ttu-id="602c5-1358">하는 경우 `E` 의 값을 *delegate_type*:</span><span class="sxs-lookup"><span data-stu-id="602c5-1358">If `E` is a value of a *delegate_type*:</span></span>
    * <span data-ttu-id="602c5-1359">`E` 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1359">`E` is evaluated.</span></span> <span data-ttu-id="602c5-1360">이 평가 예외를 발생 시키는 경우에 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1360">If this evaluation causes an exception, no further steps are executed.</span></span>
    * <span data-ttu-id="602c5-1361">경우 값 `E` 은 `null`, `System.NullReferenceException` throw 되 고 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1361">If the value of `E` is `null`, a `System.NullReferenceException` is thrown and no further steps are executed.</span></span>
    * <span data-ttu-id="602c5-1362">대리자 형식의 새 인스턴스를 `D` 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1362">A new instance of the delegate type `D` is allocated.</span></span> <span data-ttu-id="602c5-1363">새 인스턴스를 할당할 수 있는 충분 한 메모리가 없을 경우는 `System.OutOfMemoryException` throw 되 고 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1363">If there is not enough memory available to allocate the new instance, a `System.OutOfMemoryException` is thrown and no further steps are executed.</span></span>
    * <span data-ttu-id="602c5-1364">제공한 대리자 인스턴스와 같은 호출 목록을 가진 새 대리자 인스턴스가 초기화 되었음을 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1364">The new delegate instance is initialized with the same invocation list as the delegate instance given by `E`.</span></span>

<span data-ttu-id="602c5-1365">대리자의 호출 목록에는 대리자 인스턴스화되고 대리자의 전체 수명 동안 일정을 유지 하는 경우 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1365">The invocation list of a delegate is determined when the delegate is instantiated and then remains constant for the entire lifetime of the delegate.</span></span> <span data-ttu-id="602c5-1366">즉, 만들어진 후에 대리자의 대상 호출 가능 엔터티를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1366">In other words, it is not possible to change the target callable entities of a delegate once it has been created.</span></span> <span data-ttu-id="602c5-1367">때 두 명의 대리자가 결합 되거나 다른 하나를 제거 ([대리자 선언](delegates.md#delegate-declarations)), 새 대리자를 되며 대리자가 변경 내용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1367">When two delegates are combined or one is removed from another ([Delegate declarations](delegates.md#delegate-declarations)), a new delegate results; no existing delegate has its contents changed.</span></span>

<span data-ttu-id="602c5-1368">속성, 인덱서, 사용자 정의 연산자, 인스턴스 생성자, 소멸자 또는 정적 생성자를 참조 하는 대리자를 만들 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1368">It is not possible to create a delegate that refers to a property, indexer, user-defined operator, instance constructor, destructor, or static constructor.</span></span>

<span data-ttu-id="602c5-1369">위에서 설명한 대로 경우 대리자는 메서드 그룹에 정식 매개 변수 목록에서 만들어지고 대리자의 반환 형식을 선택 하는 오버 로드 된 방법의 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1369">As described above, when a delegate is created from a method group, the formal parameter list and return type of the delegate determine which of the overloaded methods to select.</span></span> <span data-ttu-id="602c5-1370">예제</span><span class="sxs-lookup"><span data-stu-id="602c5-1370">In the example</span></span>
```csharp
delegate double DoubleFunc(double x);

class A
{
    DoubleFunc f = new DoubleFunc(Square);

    static float Square(float x) {
        return x * x;
    }

    static double Square(double x) {
        return x * x;
    }
}
```
<span data-ttu-id="602c5-1371">`A.f` 필드는 두 번째 참조 하는 대리자를 사용 하 여 초기화 `Square` 메서드는 메서드 형식 매개 변수 목록 및 반환 형식의 정확 하 게 일치 하기 때문에 `DoubleFunc`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1371">the `A.f` field is initialized with a delegate that refers to the second `Square` method because that method exactly matches the formal parameter list and return type of `DoubleFunc`.</span></span> <span data-ttu-id="602c5-1372">두 번째 했습니다 `Square` 없으면 메서드는 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1372">Had the second `Square` method not been present, a compile-time error would have occurred.</span></span>

#### <a name="anonymous-object-creation-expressions"></a><span data-ttu-id="602c5-1373">익명 개체 만들기 식</span><span class="sxs-lookup"><span data-stu-id="602c5-1373">Anonymous object creation expressions</span></span>

<span data-ttu-id="602c5-1374">*anonymous_object_creation_expression* 무명 형식의 개체를 만드는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1374">An *anonymous_object_creation_expression* is used to create an object of an anonymous type.</span></span>

```antlr
anonymous_object_creation_expression
    : 'new' anonymous_object_initializer
    ;

anonymous_object_initializer
    : '{' member_declarator_list? '}'
    | '{' member_declarator_list ',' '}'
    ;

member_declarator_list
    : member_declarator (',' member_declarator)*
    ;

member_declarator
    : simple_name
    | member_access
    | base_access
    | null_conditional_member_access
    | identifier '=' expression
    ;
```

<span data-ttu-id="602c5-1375">익명 개체 이니셜라이저를 익명 형식을 선언 하 고 해당 형식의 인스턴스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1375">An anonymous object initializer declares an anonymous type and returns an instance of that type.</span></span> <span data-ttu-id="602c5-1376">익명 형식은에서 직접 상속 하는 이름이 없는 클래스 형식 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1376">An anonymous type is a nameless class type that inherits directly from `object`.</span></span> <span data-ttu-id="602c5-1377">익명 형식의 멤버는 형식의 인스턴스를 만드는 데 익명 개체 이니셜라이저에서 유추 읽기 전용 속성의 시퀀스.</span><span class="sxs-lookup"><span data-stu-id="602c5-1377">The members of an anonymous type are a sequence of read-only properties inferred from the anonymous object initializer used to create an instance of the type.</span></span> <span data-ttu-id="602c5-1378">특히, 폼의 익명 개체 이니셜라이저</span><span class="sxs-lookup"><span data-stu-id="602c5-1378">Specifically, an anonymous object initializer of the form</span></span>
```csharp
new { p1 = e1, p2 = e2, ..., pn = en }
```
<span data-ttu-id="602c5-1379">폼의 익명 형식 선언</span><span class="sxs-lookup"><span data-stu-id="602c5-1379">declares an anonymous type of the form</span></span>
```csharp
class __Anonymous1
{
    private readonly T1 f1;
    private readonly T2 f2;
    ...
    private readonly Tn fn;

    public __Anonymous1(T1 a1, T2 a2, ..., Tn an) {
        f1 = a1;
        f2 = a2;
        ...
        fn = an;
    }

    public T1 p1 { get { return f1; } }
    public T2 p2 { get { return f2; } }
    ...
    public Tn pn { get { return fn; } }

    public override bool Equals(object __o) { ... }
    public override int GetHashCode() { ... }
}
```
<span data-ttu-id="602c5-1380">여기서 각 `Tx` 해당 식의 형식이 `ex`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1380">where each `Tx` is the type of the corresponding expression `ex`.</span></span> <span data-ttu-id="602c5-1381">사용 된 식에 *member_declarator* 형식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1381">The expression used in a *member_declarator* must have a type.</span></span> <span data-ttu-id="602c5-1382">즉의 식에 대 한 컴파일 시간 오류를 *member_declarator* null 또는 익명 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1382">Thus, it is a compile-time error for an expression in a *member_declarator* to be null or an anonymous function.</span></span> <span data-ttu-id="602c5-1383">형식이 안전 하지 않은 식에 대해 컴파일 시간 오류를 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1383">It is also a compile-time error for the expression to have an unsafe type.</span></span>

<span data-ttu-id="602c5-1384">무명 형식 및 매개 변수의 이름을 해당 `Equals` 메서드는 컴파일러에서 자동으로 생성 하 고 프로그램 텍스트에서 참조할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1384">The names of an anonymous type and of the parameter to its `Equals` method are automatically generated by the compiler and cannot be referenced in program text.</span></span>

<span data-ttu-id="602c5-1385">동일한 프로그램에서 동일한 순서로 동일한 이름 및 컴파일 타임 형식 속성의 순서를 지정 하는 두 명의 익명 개체 이니셜라이저는 동일한 익명 형식의 인스턴스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1385">Within the same program, two anonymous object initializers that specify a sequence of properties of the same names and compile-time types in the same order will produce instances of the same anonymous type.</span></span>

<span data-ttu-id="602c5-1386">예제</span><span class="sxs-lookup"><span data-stu-id="602c5-1386">In the example</span></span>
```csharp
var p1 = new { Name = "Lawnmower", Price = 495.00 };
var p2 = new { Name = "Shovel", Price = 26.95 };
p1 = p2;
```
<span data-ttu-id="602c5-1387">마지막 줄에서 할당 되지 않으므로 위 `p1` 및 `p2` 같은 익명 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1387">the assignment on the last line is permitted because `p1` and `p2` are of the same anonymous type.</span></span>

<span data-ttu-id="602c5-1388">`Equals` 및 `GetHashcode` 에서 상속 된 메서드를 재정의 하는 익명 형식에 메서드 `object`, 및의 측면에서 정의 됩니다는 `Equals` 및 `GetHashcode` 속성의 동일한 익명 형식의 두 인스턴스가 같은지를 경우 및 해당 속성이 모두 같은 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1388">The `Equals` and `GetHashcode` methods on anonymous types override the methods inherited from `object`, and are defined in terms of the `Equals` and `GetHashcode` of the properties, so that two instances of the same anonymous type are equal if and only if all their properties are equal.</span></span>

<span data-ttu-id="602c5-1389">멤버 선언 자는 단순한 이름으로 축약할 수 있습니다 ([형식 유추](expressions.md#type-inference)), 멤버 액세스 ([동적 오버 로드 확인 검사 하는 컴파일 타임](expressions.md#compile-time-checking-of-dynamic-overload-resolution)), 기본 액세스 ([액세스기반](expressions.md#base-access)) 또는 null 조건부 멤버 액세스 ([프로젝션 이니셜라이저 식이 Null 조건부](expressions.md#null-conditional-expressions-as-projection-initializers)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1389">A member declarator can be abbreviated to a simple name ([Type inference](expressions.md#type-inference)), a member access ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)), a base access ([Base access](expressions.md#base-access)) or a null-conditional member access ([Null-conditional expressions as projection initializers](expressions.md#null-conditional-expressions-as-projection-initializers)).</span></span> <span data-ttu-id="602c5-1390">이 호출 되는 ***프로젝션 이니셜라이저*** 축약형 선언 및 동일한 이름 가진 속성에 할당 되며.</span><span class="sxs-lookup"><span data-stu-id="602c5-1390">This is called a ***projection initializer*** and is shorthand for a declaration of and assignment to a property with the same name.</span></span> <span data-ttu-id="602c5-1391">폼의 특히 멤버 선언 자</span><span class="sxs-lookup"><span data-stu-id="602c5-1391">Specifically, member declarators of the forms</span></span>
```csharp
identifier
expr.identifier
```
<span data-ttu-id="602c5-1392">각각은 다음을 정확 하 게 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1392">are precisely equivalent to the following, respectively:</span></span>
```csharp
identifier = identifier
identifier = expr.identifier
```

<span data-ttu-id="602c5-1393">프로젝션 이니셜라이저에 따라서 합니다 *식별자* 값 및 필드 또는 값이 할당 된 속성 모두를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1393">Thus, in a projection initializer the *identifier* selects both the value and the field or property to which the value is assigned.</span></span> <span data-ttu-id="602c5-1394">직관적으로 프로젝션 이니셜라이저를 프로젝트 뿐 아니라 값 뿐만 아니라 값의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1394">Intuitively, a projection initializer projects not just a value, but also the name of the value.</span></span>

### <a name="the-typeof-operator"></a><span data-ttu-id="602c5-1395">Typeof 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1395">The typeof operator</span></span>

<span data-ttu-id="602c5-1396">`typeof` 연산자를 가져오는 데 사용 되는 `System.Type` 개체 유형에 대 한.</span><span class="sxs-lookup"><span data-stu-id="602c5-1396">The `typeof` operator is used to obtain the `System.Type` object for a type.</span></span>

```antlr
typeof_expression
    : 'typeof' '(' type ')'
    | 'typeof' '(' unbound_type_name ')'
    | 'typeof' '(' 'void' ')'
    ;

unbound_type_name
    : identifier generic_dimension_specifier?
    | identifier '::' identifier generic_dimension_specifier?
    | unbound_type_name '.' identifier generic_dimension_specifier?
    ;

generic_dimension_specifier
    : '<' comma* '>'
    ;

comma
    : ','
    ;
```

<span data-ttu-id="602c5-1397">첫 번째 형태 *typeof_expression* 이루어져를 `typeof` 키워드 뒤에 괄호로 묶고 *형식*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1397">The first form of *typeof_expression* consists of a `typeof` keyword followed by a parenthesized *type*.</span></span> <span data-ttu-id="602c5-1398">이 폼의 식의 결과 `System.Type` 표시 된 형식에 대 한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1398">The result of an expression of this form is the `System.Type` object for the indicated type.</span></span> <span data-ttu-id="602c5-1399">하나만 `System.Type` 임의의 형식에 대 한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1399">There is only one `System.Type` object for any given type.</span></span> <span data-ttu-id="602c5-1400">형식에 대 한 즉 `T`, `typeof(T) == typeof(T)` 는 항상 true입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1400">This means that for a type `T`, `typeof(T) == typeof(T)` is always true.</span></span> <span data-ttu-id="602c5-1401">합니다 *형식* 일 수 없습니다 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1401">The *type* cannot be `dynamic`.</span></span>

<span data-ttu-id="602c5-1402">두 번째 형태 *typeof_expression* 이루어져를 `typeof` 키워드 뒤에 괄호로 묶고 *unbound_type_name*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1402">The second form of *typeof_expression* consists of a `typeof` keyword followed by a parenthesized *unbound_type_name*.</span></span> <span data-ttu-id="602c5-1403">*unbound_type_name* 매우 비슷합니다는 *type_name* ([Namespace 및 형식 이름](basic-concepts.md#namespace-and-type-names)) 점을 제외 하 고는 *unbound_type_name* 포함 *generic_dimension_specifier*s 여기서는 *type_name* 포함 *type_argument_list*s입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1403">An *unbound_type_name* is very similar to a *type_name* ([Namespace and type names](basic-concepts.md#namespace-and-type-names)) except that an *unbound_type_name* contains *generic_dimension_specifier*s where a *type_name* contains *type_argument_list*s.</span></span> <span data-ttu-id="602c5-1404">때의 피연산자는 *typeof_expression* 둘 다의 문법에 맞는 토큰의 순서가 *unbound_type_name* 및 *type_name*, 즉 포함 되어 있을 때는 모두를 *generic_dimension_specifier* 또는 *type_argument_list*, 일련의 토큰으로 간주 됩니다는 *type_name*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1404">When the operand of a *typeof_expression* is a sequence of tokens that satisfies the grammars of both *unbound_type_name* and *type_name*, namely when it contains neither a *generic_dimension_specifier* nor a *type_argument_list*, the sequence of tokens is considered to be a *type_name*.</span></span> <span data-ttu-id="602c5-1405">의미는 *unbound_type_name* 다음과 같이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1405">The meaning of an *unbound_type_name* is determined as follows:</span></span>

*  <span data-ttu-id="602c5-1406">토큰을 시퀀스로 변환를 *type_name* 각 바꿔 *generic_dimension_specifier* 사용 하 여를 *type_argument_list* 쉼표 동일한 수 및 키워드 `object` 각 *type_argument*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1406">Convert the sequence of tokens to a *type_name* by replacing each *generic_dimension_specifier* with a *type_argument_list* having the same number of commas and the keyword `object` as each *type_argument*.</span></span>
*  <span data-ttu-id="602c5-1407">평가 결과 *type_name*, 모든 형식 매개 변수 제약 조건을 무시 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1407">Evaluate the resulting *type_name*, while ignoring all type parameter constraints.</span></span>
*  <span data-ttu-id="602c5-1408">합니다 *unbound_type_name* 결과로 생성 된 형식과 사용 하 여 연결 하는 언바운드 제네릭 형식으로 확인 ([바인딩되며 형식에 바인딩되지 않은](types.md#bound-and-unbound-types)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1408">The *unbound_type_name* resolves to the unbound generic type associated with the resulting constructed type ([Bound and unbound types](types.md#bound-and-unbound-types)).</span></span>

<span data-ttu-id="602c5-1409">결과 *typeof_expression* 는 `System.Type` 제네릭 형식에 바인딩되지 않은 결과 대 한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1409">The result of the *typeof_expression* is the `System.Type` object for the resulting unbound generic type.</span></span>

<span data-ttu-id="602c5-1410">세 번째 형태의 *typeof_expression* 이루어져를 `typeof` 키워드 뒤에 괄호로 묶고 `void` 키워드.</span><span class="sxs-lookup"><span data-stu-id="602c5-1410">The third form of *typeof_expression* consists of a `typeof` keyword followed by a parenthesized `void` keyword.</span></span> <span data-ttu-id="602c5-1411">이 폼의 식의 결과 `System.Type` 형식의 없음을 나타내는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1411">The result of an expression of this form is the `System.Type` object that represents the absence of a type.</span></span> <span data-ttu-id="602c5-1412">반환 된 형식 개체 `typeof(void)` 모든 형식에 대해 반환 되는 형식 개체와에서 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1412">The type object returned by `typeof(void)` is distinct from the type object returned for any type.</span></span> <span data-ttu-id="602c5-1413">이러한 메서드는 수의 인스턴스를 사용 하 여 void 메서드를 포함 하 여 모든 메서드의 반환 형식을 나타내는 하려는 메서드에 리플렉션을 언어에서 허용 하는 클래스 라이브러리의이 특별 한 형식 개체는 유용한 `System.Type`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1413">This special type object is useful in class libraries that allow reflection onto methods in the language, where those methods wish to have a way to represent the return type of any method, including void methods, with an instance of `System.Type`.</span></span>

<span data-ttu-id="602c5-1414">`typeof` 형식 매개 변수에서 연산자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1414">The `typeof` operator can be used on a type parameter.</span></span> <span data-ttu-id="602c5-1415">결과 `System.Type` 형식 매개 변수에 바인딩된 런타임 형식에 대 한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1415">The result is the `System.Type` object for the run-time type that was bound to the type parameter.</span></span> <span data-ttu-id="602c5-1416">합니다 `typeof` 연산자는 언바운드 제네릭 형식 또는 생성된 된 형식을 사용할 수도 있습니다 ([바인딩되며 형식에 바인딩되지 않은](types.md#bound-and-unbound-types)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1416">The `typeof` operator can also be used on a constructed type or an unbound generic type ([Bound and unbound types](types.md#bound-and-unbound-types)).</span></span> <span data-ttu-id="602c5-1417">`System.Type` 바인딩되지 않은 제네릭 형식이 동일 하지 않습니다 개체는 `System.Type` 인스턴스 형식의 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1417">The `System.Type` object for an unbound generic type is not the same as the `System.Type` object of the instance type.</span></span> <span data-ttu-id="602c5-1418">인스턴스 형식이 항상 런타임 시 폐쇄형된 생성된 형식 이므로 해당 `System.Type` 언바운드 제네릭 형식에 형식 인수 없이 개체 사용에 런타임에 형식 인수에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1418">The instance type is always a closed constructed type at run-time so its `System.Type` object depends on the run-time type arguments in use, while the unbound generic type has no type arguments.</span></span>

<span data-ttu-id="602c5-1419">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-1419">The example</span></span>
```csharp
using System;

class X<T>
{
    public static void PrintTypes() {
        Type[] t = {
            typeof(int),
            typeof(System.Int32),
            typeof(string),
            typeof(double[]),
            typeof(void),
            typeof(T),
            typeof(X<T>),
            typeof(X<X<T>>),
            typeof(X<>)
        };
        for (int i = 0; i < t.Length; i++) {
            Console.WriteLine(t[i]);
        }
    }
}

class Test
{
    static void Main() {
        X<int>.PrintTypes();
    }
}
```
<span data-ttu-id="602c5-1420">다음 출력이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1420">produces the following output:</span></span>
```
System.Int32
System.Int32
System.String
System.Double[]
System.Void
System.Int32
X`1[System.Int32]
X`1[X`1[System.Int32]]
X`1[T]
```

<span data-ttu-id="602c5-1421">사실은 `int` 및 `System.Int32` 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1421">Note that `int` and `System.Int32` are the same type.</span></span>

<span data-ttu-id="602c5-1422">또한 결과인 `typeof(X<>)` 종속 되지 않는 형식 인수가 있지만 결과 `typeof(X<T>)` 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1422">Also note that the result of `typeof(X<>)` does not depend on the type argument but the result of `typeof(X<T>)` does.</span></span>

### <a name="the-checked-and-unchecked-operators"></a><span data-ttu-id="602c5-1423">Checked 및 unchecked 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1423">The checked and unchecked operators</span></span>

<span data-ttu-id="602c5-1424">합니다 `checked` 및 `unchecked` 연산자는 제어 하는 데 사용 되는 ***오버플로 검사 컨텍스트에*** 정수 형식 산술 연산 및 변환에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1424">The `checked` and `unchecked` operators are used to control the ***overflow checking context*** for integral-type arithmetic operations and conversions.</span></span>

```antlr
checked_expression
    : 'checked' '(' expression ')'
    ;

unchecked_expression
    : 'unchecked' '(' expression ')'
    ;
```

<span data-ttu-id="602c5-1425">합니다 `checked` 연산자 확인 된 컨텍스트에서 포함 된 식 및 `unchecked` 연산자 unchecked 컨텍스트에서 포함 된 식을 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1425">The `checked` operator evaluates the contained expression in a checked context, and the `unchecked` operator evaluates the contained expression in an unchecked context.</span></span> <span data-ttu-id="602c5-1426">A *checked_expression* 하거나 *unchecked_expression* 정확히 일치를 *parenthesized_expression* ([괄호로 묶인 식](expressions.md#parenthesized-expressions))에 지정 된 오버플로 검사 컨텍스트에 포함 된 식이 계산 되는 점을 제외 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1426">A *checked_expression* or *unchecked_expression* corresponds exactly to a *parenthesized_expression* ([Parenthesized expressions](expressions.md#parenthesized-expressions)), except that the contained expression is evaluated in the given overflow checking context.</span></span>

<span data-ttu-id="602c5-1427">오버플로 검사 컨텍스트를 통해 제어할 수도 있습니다는 `checked` 하 고 `unchecked` 문 ([checked 및 unchecked 문](statements.md#the-checked-and-unchecked-statements)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1427">The overflow checking context can also be controlled through the `checked` and `unchecked` statements ([The checked and unchecked statements](statements.md#the-checked-and-unchecked-statements)).</span></span>

<span data-ttu-id="602c5-1428">다음 작업은 오버플로 검사 하 여 설정 하는 컨텍스트에 영향을 받지 합니다 `checked` 고 `unchecked` 연산자와 문을:</span><span class="sxs-lookup"><span data-stu-id="602c5-1428">The following operations are affected by the overflow checking context established by the `checked` and `unchecked` operators and statements:</span></span>

*  <span data-ttu-id="602c5-1429">미리 정의 된 `++` 하 고 `--` 단항 연산자 ([후 위 증가 및 감소 연산자](expressions.md#postfix-increment-and-decrement-operators) 하 고 [전위 증가 및 감소 연산자](expressions.md#prefix-increment-and-decrement-operators)) 정수 계열 피연산자가 하는 경우 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1429">The predefined `++` and `--` unary operators ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators) and [Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)), when the operand is of an integral type.</span></span>
*  <span data-ttu-id="602c5-1430">미리 정의 된 `-` 단항 연산자 ([단항 빼기 연산자](expressions.md#unary-minus-operator)), 피연산자가 정수 계열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1430">The predefined `-` unary operator ([Unary minus operator](expressions.md#unary-minus-operator)), when the operand is of an integral type.</span></span>
*  <span data-ttu-id="602c5-1431">미리 정의 된 `+`, `-`를 `*`, 및 `/` 이항 연산자 ([산술 연산자](expressions.md#arithmetic-operators)), 두 피연산자 모두 정수 계열 형식의 경우.</span><span class="sxs-lookup"><span data-stu-id="602c5-1431">The predefined `+`, `-`, `*`, and `/` binary operators ([Arithmetic operators](expressions.md#arithmetic-operators)), when both operands are of integral types.</span></span>
*  <span data-ttu-id="602c5-1432">명시적 숫자 변환 ([명시적 숫자 변환](conversions.md#explicit-numeric-conversions)) 또는 다른 정수 계열 형식으로 한 정수 계열 형식에서 `float` 또는 `double` 정수 계열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1432">Explicit numeric conversions ([Explicit numeric conversions](conversions.md#explicit-numeric-conversions)) from one integral type to another integral type, or from `float` or `double` to an integral type.</span></span>

<span data-ttu-id="602c5-1433">경우에 너무 커서 대상 유형에 컨텍스트는 작업을 수행된 하는 컨트롤 결과 동작을 나타낼 수 있는 결과 생성 하면 위 작업 중 하나:</span><span class="sxs-lookup"><span data-stu-id="602c5-1433">When one of the above operations produce a result that is too large to represent in the destination type, the context in which the operation is performed controls the resulting behavior:</span></span>

*  <span data-ttu-id="602c5-1434">에 `checked` 컨텍스트, 작업에는 상수 식 ([상수 식](expressions.md#constant-expressions)), 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1434">In a `checked` context, if the operation is a constant expression ([Constant expressions](expressions.md#constant-expressions)), a compile-time error occurs.</span></span> <span data-ttu-id="602c5-1435">실행 시 작업을 수행할 때 그러지는 `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1435">Otherwise, when the operation is performed at run-time, a `System.OverflowException` is thrown.</span></span>
*  <span data-ttu-id="602c5-1436">에 `unchecked` 컨텍스트를 결과 대상 형식에 맞지 않는 상위 비트가 삭제 되어 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1436">In an `unchecked` context, the result is truncated by discarding any high-order bits that do not fit in the destination type.</span></span>

<span data-ttu-id="602c5-1437">상수가 아닌 식 (런타임 시 계산 되는 식)는 포함 되지 않는 모든 `checked` 또는 `unchecked` 기본 오버플로 검사 컨텍스트에 연산자, 문 `unchecked` 외부 (예: 컴파일러 고려 하지 않으면 스위치 및 실행 환경 구성은)에 대 한 호출 `checked` 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1437">For non-constant expressions (expressions that are evaluated at run-time) that are not enclosed by any `checked` or `unchecked` operators or statements, the default overflow checking context is `unchecked` unless external factors (such as compiler switches and execution environment configuration) call for `checked` evaluation.</span></span>

<span data-ttu-id="602c5-1438">상수 식 (컴파일 타임에 완벽 하 게 평가할 수 있는 식)에 대 한 기본 오버플로 검사 컨텍스트에 항상 `checked`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1438">For constant expressions (expressions that can be fully evaluated at compile-time), the default overflow checking context is always `checked`.</span></span> <span data-ttu-id="602c5-1439">상수 식에 명시적으로 배치 됩니다 하지 않는 한는 `unchecked` 컨텍스트를 항상 식의 컴파일 타임 확인 하는 동안 발생 하는 오버플로 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1439">Unless a constant expression is explicitly placed in an `unchecked` context, overflows that occur during the compile-time evaluation of the expression always cause compile-time errors.</span></span>

<span data-ttu-id="602c5-1440">익명 함수의 본문에서 영향을 받지 `checked` 또는 `unchecked` 익명 함수 발생 하는 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="602c5-1440">The body of an anonymous function is not affected by `checked` or `unchecked` contexts in which the anonymous function occurs.</span></span>

<span data-ttu-id="602c5-1441">예제</span><span class="sxs-lookup"><span data-stu-id="602c5-1441">In the example</span></span>
```csharp
class Test
{
    static readonly int x = 1000000;
    static readonly int y = 1000000;

    static int F() {
        return checked(x * y);      // Throws OverflowException
    }

    static int G() {
        return unchecked(x * y);    // Returns -727379968
    }

    static int H() {
        return x * y;               // Depends on default
    }
}
```
<span data-ttu-id="602c5-1442">식의 어느 컴파일 타임에 평가할 수 있으므로 컴파일 타임 오류가 보고 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1442">no compile-time errors are reported since neither of the expressions can be evaluated at compile-time.</span></span> <span data-ttu-id="602c5-1443">실행 시 합니다 `F` 메서드가 throw를 `System.OverflowException`, 및 `G` -727379968 (범위를 벗어난 결과의 하위 32 비트)를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1443">At run-time, the `F` method throws a `System.OverflowException`, and the `G` method returns -727379968 (the lower 32 bits of the out-of-range result).</span></span> <span data-ttu-id="602c5-1444">동작을 `H` 메서드 기본 오버플로 검사 컨텍스트를 컴파일하는 경우에 따라 달라 지지만 동일 하거나 것 `F` 또는 같은 `G`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1444">The behavior of the `H` method depends on the default overflow checking context for the compilation, but it is either the same as `F` or the same as `G`.</span></span>

<span data-ttu-id="602c5-1445">예제</span><span class="sxs-lookup"><span data-stu-id="602c5-1445">In the example</span></span>
```csharp
class Test
{
    const int x = 1000000;
    const int y = 1000000;

    static int F() {
        return checked(x * y);      // Compile error, overflow
    }

    static int G() {
        return unchecked(x * y);    // Returns -727379968
    }

    static int H() {
        return x * y;               // Compile error, overflow
    }
}
```
<span data-ttu-id="602c5-1446">상수 식을 계산할 때 발생 하는 오버플로 `F` 및 `H` 식의 평가 되기 때문에 보고 되어야 하도록 컴파일 타임 오류가 발생을 `checked` 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="602c5-1446">the overflows that occur when evaluating the constant expressions in `F` and `H` cause compile-time errors to be reported because the expressions are evaluated in a `checked` context.</span></span> <span data-ttu-id="602c5-1447">상수 식을 계산 하는 경우에 오버플로가 발생 `G`, 평가 수행 되기 때문 이지만 `unchecked` 컨텍스트에 오버플로 보고 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1447">An overflow also occurs when evaluating the constant expression in `G`, but since the evaluation takes place in an `unchecked` context, the overflow is not reported.</span></span>

<span data-ttu-id="602c5-1448">합니다 `checked` 하 고 `unchecked` 연산자는 오버플로 검사 컨텍스트 내에서 텍스트가 포함 된 이러한 작업에 영향을 줍니다는 "`(`"및"`)`" 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1448">The `checked` and `unchecked` operators only affect the overflow checking context for those operations that are textually contained within the "`(`" and "`)`" tokens.</span></span> <span data-ttu-id="602c5-1449">연산자에 포함 된 식을 평가 결과로 호출 되는 함수 멤버 효과가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1449">The operators have no effect on function members that are invoked as a result of evaluating the contained expression.</span></span> <span data-ttu-id="602c5-1450">예제</span><span class="sxs-lookup"><span data-stu-id="602c5-1450">In the example</span></span>
```csharp
class Test
{
    static int Multiply(int x, int y) {
        return x * y;
    }

    static int F() {
        return checked(Multiply(1000000, 1000000));
    }
}
```
<span data-ttu-id="602c5-1451">사용 `checked` 에 `F` 평가 하는 데 영향을 주지 않습니다 `x * y` 에서 `Multiply`이므로 `x * y` 기본 오버플로 검사 컨텍스트에에서 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1451">the use of `checked` in `F` does not affect the evaluation of `x * y` in `Multiply`, so `x * y` is evaluated in the default overflow checking context.</span></span>

<span data-ttu-id="602c5-1452">`unchecked` 연산자는 16 진수 표기법의 부호 있는 정수 계열 형식의 상수를 작성 하는 경우에 편리 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1452">The `unchecked` operator is convenient when writing constants of the signed integral types in hexadecimal notation.</span></span> <span data-ttu-id="602c5-1453">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="602c5-1453">For example:</span></span>
```csharp
class Test
{
    public const int AllBits = unchecked((int)0xFFFFFFFF);

    public const int HighBit = unchecked((int)0x80000000);
}
```

<span data-ttu-id="602c5-1454">위의 16 진수 상수에 모두 형식의 `uint`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1454">Both of the hexadecimal constants above are of type `uint`.</span></span> <span data-ttu-id="602c5-1455">상수 외부 되므로 합니다 `int` 없이 범위를 `unchecked` 연산자, 캐스트를 `int` 컴파일 타임 오류가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1455">Because the constants are outside the `int` range, without the `unchecked` operator, the casts to `int` would produce compile-time errors.</span></span>

<span data-ttu-id="602c5-1456">합니다 `checked` 및 `unchecked` 연산자와 문을 프로그래머에 게 몇 가지 숫자 계산의 특정 측면을 제어할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1456">The `checked` and `unchecked` operators and statements allow programmers to control certain aspects of some numeric calculations.</span></span> <span data-ttu-id="602c5-1457">그러나 일부 숫자 연산자의 동작 해당 피연산자의 데이터 형식에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1457">However, the behavior of some numeric operators depends on their operands' data types.</span></span> <span data-ttu-id="602c5-1458">예를 들어 항상 두 자리를 곱한 결과 오버플로 예외가 내 에서도 명시적으로 `unchecked` 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1458">For example, multiplying two decimals always results in an exception on overflow even within an explicitly `unchecked` construct.</span></span> <span data-ttu-id="602c5-1459">마찬가지로, 두 개를 곱한 부동 되지 결과 오버플로 예외가 내 에서도 명시적으로 `checked` 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1459">Similarly, multiplying two floats never results in an exception on overflow even within an explicitly `checked` construct.</span></span> <span data-ttu-id="602c5-1460">다른 연산자 검사 모드의 영향을 받지 않습니다 또한, 기본 여부 또는 명시적입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1460">In addition, other operators are never affected by the mode of checking, whether default or explicit.</span></span>

### <a name="default-value-expressions"></a><span data-ttu-id="602c5-1461">기본 값 식</span><span class="sxs-lookup"><span data-stu-id="602c5-1461">Default value expressions</span></span>

<span data-ttu-id="602c5-1462">기본 값 식의 기본값을 가져오는 데 사용 됩니다 ([기본값](variables.md#default-values)) 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1462">A default value expression is used to obtain the default value ([Default values](variables.md#default-values)) of a type.</span></span> <span data-ttu-id="602c5-1463">일반적으로 확인할 수 없는 경우 형식 매개 변수 값 형식 또는 참조 형식 이므로 형식 매개 변수에 대해 기본값 식을 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1463">Typically a default value expression is used for type parameters, since it may not be known if the type parameter is a value type or a reference type.</span></span> <span data-ttu-id="602c5-1464">(변환 된 항목이 없고에서 `null` 형식 매개 변수는 참조 형식으로 알려져 경우가 아니면 형식 매개 변수에 리터럴.)</span><span class="sxs-lookup"><span data-stu-id="602c5-1464">(No conversion exists from the `null` literal to a type parameter unless the type parameter is known to be a reference type.)</span></span>

```antlr
default_value_expression
    : 'default' '(' type ')'
    ;
```

<span data-ttu-id="602c5-1465">경우는 *형식* 에 *default_value_expression* 평가 런타임 참조 형식으로 결과 `null` 해당 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1465">If the *type* in a *default_value_expression* evaluates at run-time to a reference type, the result is `null` converted to that type.</span></span> <span data-ttu-id="602c5-1466">경우는 *형식* 에 *default_value_expression* 평가 결과 런타임에 값 형식에 *value_type*의 기본값 ([기본 생성자](types.md#default-constructors)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1466">If the *type* in a *default_value_expression* evaluates at run-time to a value type, the result is the *value_type*'s default value ([Default constructors](types.md#default-constructors)).</span></span>

<span data-ttu-id="602c5-1467">A *default_value_expression* 상수 식입니다 ([상수 식을](expressions.md#constant-expressions)) 형식이 참조 형식 또는 참조 형식으로 알려진 형식 매개 변수 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1467">A *default_value_expression* is a constant expression ([Constant expressions](expressions.md#constant-expressions)) if the type is a reference type or a type parameter that is known to be a reference type ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span> <span data-ttu-id="602c5-1468">또한를 *default_value_expression* 형식을 사용 하면 다음과 같은 값 형식 중 하나인 경우에 상수 식: `sbyte`, `byte`를 `short`를 `ushort`를 `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`를 `decimal`, `bool`, 또는 열거형 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1468">In addition, a *default_value_expression* is a constant expression if the type is one of the following value types: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, `bool`, or any enumeration type.</span></span>


### <a name="nameof-expressions"></a><span data-ttu-id="602c5-1469">Nameof 식</span><span class="sxs-lookup"><span data-stu-id="602c5-1469">Nameof expressions</span></span>

<span data-ttu-id="602c5-1470">A *nameof_expression* 상수 문자열로 프로그램 엔터티의 이름을 가져오는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1470">A *nameof_expression* is used to obtain the name of a program entity as a constant string.</span></span>

```antlr
nameof_expression
    : 'nameof' '(' named_entity ')'
    ;

named_entity
    : simple_name
    | named_entity_target '.' identifier type_argument_list?
    ;

named_entity_target
    : 'this'
    | 'base'
    | named_entity 
    | predefined_type 
    | qualified_alias_member
    ;
```

<span data-ttu-id="602c5-1471">문법적으로 말하자면 합니다 *named_entity* 피연산자는 항상 식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1471">Grammatically speaking, the *named_entity* operand is always an expression.</span></span> <span data-ttu-id="602c5-1472">때문에 `nameof` 는 예약된 키워드가 아닙니다 nameof 식은 단순한 이름 호출을 사용 하 여 구문상 모호한 항상 `nameof`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1472">Because `nameof` is not a reserved keyword, a nameof expression is always syntactically ambiguous with an invocation of the simple name `nameof`.</span></span> <span data-ttu-id="602c5-1473">호환성을 위해, 이름 조회 하는 경우 ([단순 이름](expressions.md#simple-names)) 이름의 `nameof` 성공 하면 식으로 처리 됩니다는 *invocation_expression* 호출 인지 여부에 관계 없이- 법률.</span><span class="sxs-lookup"><span data-stu-id="602c5-1473">For compatibility reasons, if a name lookup ([Simple names](expressions.md#simple-names)) of the name `nameof` succeeds, the expression is treated as an *invocation_expression* -- regardless of whether the invocation is legal.</span></span> <span data-ttu-id="602c5-1474">그렇지 않으면이 생성자는 *nameof_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1474">Otherwise it is a *nameof_expression*.</span></span>

<span data-ttu-id="602c5-1475">의미는 *named_entity* 의 *nameof_expression* ; 식으로의 의미으로 즉, 하나는 *simple_name*, *base_access*  또는 *member_access*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1475">The meaning of the *named_entity* of a *nameof_expression* is the meaning of it as an expression; that is, either as a *simple_name*, a *base_access* or a *member_access*.</span></span> <span data-ttu-id="602c5-1476">그러나 여기서 조회에 설명 된 [단순 이름](expressions.md#simple-names) 및 [멤버 액세스](expressions.md#member-access) 정적 컨텍스트에서 인스턴스 멤버를 찾을 수 없어서 오류가 발생 한 *nameof_expression*이러한 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1476">However, where the lookup described in [Simple names](expressions.md#simple-names) and [Member access](expressions.md#member-access) results in an error because an instance member was found in a static context, a *nameof_expression* produces no such error.</span></span>

<span data-ttu-id="602c5-1477">에 대 한 컴파일 시간 오류를 *named_entity* 있어야 하는 메서드 그룹을 지정을 *type_argument_list*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1477">It is a compile-time error for a *named_entity* designating a method group to have a *type_argument_list*.</span></span> <span data-ttu-id="602c5-1478">에 대 한 컴파일 시간 오류가 발생 한 *named_entity_target* 형식을 갖도록 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1478">It is a compile time error for a *named_entity_target* to have the type `dynamic`.</span></span>

<span data-ttu-id="602c5-1479">A *nameof_expression* 형식의 상수 식 `string`, 런타임 시 효과가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1479">A *nameof_expression* is a constant expression of type `string`, and has no effect at runtime.</span></span> <span data-ttu-id="602c5-1480">특히, 해당 *named_entity* 계산 되지 않습니다 및 한정 된 할당 분석을 위해 무시 됩니다 ([단순 식에 대 한 일반 규칙](variables.md#general-rules-for-simple-expressions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1480">Specifically, its *named_entity* is not evaluated, and is ignored for the purposes of definite assignment analysis ([General rules for simple expressions](variables.md#general-rules-for-simple-expressions)).</span></span> <span data-ttu-id="602c5-1481">해당 값은 마지막 식별자를 *named_entity* 선택적 최종 전에 *type_argument_list*같은 방식으로 변환 된:</span><span class="sxs-lookup"><span data-stu-id="602c5-1481">Its value is the last identifier of the *named_entity* before the optional final *type_argument_list*, transformed in the following way:</span></span>

* <span data-ttu-id="602c5-1482">접두사 "`@`"를 사용 하는 경우 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1482">The prefix "`@`", if used, is removed.</span></span>
* <span data-ttu-id="602c5-1483">각 *unicode_escape_sequence* 해당 유니코드 문자로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1483">Each *unicode_escape_sequence* is transformed into its corresponding Unicode character.</span></span>
* <span data-ttu-id="602c5-1484">모든 *formatting_characters* 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1484">Any *formatting_characters* are removed.</span></span>

<span data-ttu-id="602c5-1485">에 적용 되는 동일한 변형 이들은 [식별자](lexical-structure.md#identifiers) 식별자 같은지를 테스트 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="602c5-1485">These are the same transformations applied in [Identifiers](lexical-structure.md#identifiers) when testing equality between identifiers.</span></span>

<span data-ttu-id="602c5-1486">TODO: 예제</span><span class="sxs-lookup"><span data-stu-id="602c5-1486">TODO: examples</span></span>

### <a name="anonymous-method-expressions"></a><span data-ttu-id="602c5-1487">무명 메서드 식</span><span class="sxs-lookup"><span data-stu-id="602c5-1487">Anonymous method expressions</span></span>

<span data-ttu-id="602c5-1488">*anonymous_method_expression* 익명 함수를 정의 하는 두 가지 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1488">An *anonymous_method_expression* is one of two ways of defining an anonymous function.</span></span> <span data-ttu-id="602c5-1489">에 설명 된 추가 이러한 [익명 함수 식](expressions.md#anonymous-function-expressions)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1489">These are further described in [Anonymous function expressions](expressions.md#anonymous-function-expressions).</span></span>

## <a name="unary-operators"></a><span data-ttu-id="602c5-1490">단항 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1490">Unary operators</span></span>

<span data-ttu-id="602c5-1491">`?`, `+`, `-`, `!`를 `~`를 `++`, `--`캐스팅, 및 `await` 연산자는 단항 연산자 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1491">The `?`, `+`, `-`, `!`, `~`, `++`, `--`, cast, and `await` operators are called the unary operators.</span></span>

```antlr
unary_expression
    : primary_expression
    | null_conditional_expression
    | '+' unary_expression
    | '-' unary_expression
    | '!' unary_expression
    | '~' unary_expression
    | pre_increment_expression
    | pre_decrement_expression
    | cast_expression
    | await_expression
    | unary_expression_unsafe
    ;
```

<span data-ttu-id="602c5-1492">하는 경우의 피연산자는 *unary_expression* 컴파일 시간 형식이 `dynamic`, 동적으로 바인딩되어 ([동적 바인딩](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1492">If the operand of a *unary_expression* has the compile-time type `dynamic`, it is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="602c5-1493">이 경우 컴파일 타임 유형의 합니다 *unary_expression* 는 `dynamic`, 및 아래에 설명 된 해결 방법을 피연산자의 런타임 형식을 사용 하 여 런타임 시 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1493">In this case the compile-time type of the *unary_expression* is `dynamic`, and the resolution described below will take place at run-time using the run-time type of the operand.</span></span>

### <a name="null-conditional-operator"></a><span data-ttu-id="602c5-1494">Null 조건부 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1494">Null-conditional operator</span></span>

<span data-ttu-id="602c5-1495">Null 조건부 연산자는 피연산자가 null이 아닌 경우에 해당 피연산자에 작업 목록이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1495">The null-conditional operator applies a list of operations to its operand only if that operand is non-null.</span></span> <span data-ttu-id="602c5-1496">그렇지 않으면 연산자를 적용 한 결과 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1496">Otherwise the result of applying the operator is `null`.</span></span>

```antlr
null_conditional_expression
    : primary_expression null_conditional_operations
    ;

null_conditional_operations
    : null_conditional_operations? '?' '.' identifier type_argument_list?
    | null_conditional_operations? '?' '[' argument_list ']'
    | null_conditional_operations '.' identifier type_argument_list?
    | null_conditional_operations '[' argument_list ']'
    | null_conditional_operations '(' argument_list? ')'
    ;
```

<span data-ttu-id="602c5-1497">작업 목록에는 호출 뿐만 아니라 멤버 액세스 및 요소 액세스 작업 (null 조건부 자체 일 수 있음)를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1497">The list of operations can include member access and element access operations (which may themselves be null-conditional), as well as invocation.</span></span>

<span data-ttu-id="602c5-1498">예를 들어 식 `a.b?[0]?.c()` 되는 *null_conditional_expression* 사용 하 여를 *primary_expression* `a.b` 및 *null_conditional_operations* `?[0]` (null 조건부 요소 액세스)를 `?.c` (null 조건부 멤버 액세스) 및 `()` (호출).</span><span class="sxs-lookup"><span data-stu-id="602c5-1498">For example, the expression `a.b?[0]?.c()` is a *null_conditional_expression* with a *primary_expression* `a.b` and *null_conditional_operations* `?[0]` (null-conditional element access), `?.c` (null-conditional member access) and `()` (invocation).</span></span>

<span data-ttu-id="602c5-1499">에 대 한는 *null_conditional_expression* `E` 사용 하 여를 *primary_expression* `P`let, `E0` 텍스트가 앞에 오는 를제거하여얻은식일`?`각 합니다 *null_conditional_operations* 의 `E` 하나 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1499">For a *null_conditional_expression* `E` with a *primary_expression* `P`, let `E0` be the expression obtained by textually removing the leading `?` from each of the *null_conditional_operations* of `E` that have one.</span></span> <span data-ttu-id="602c5-1500">개념적으로 `E0` 를 나타내는 null 검사를 하나도 경우 평가할 식 합니다 `?`s 검색 하려면를 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1500">Conceptually, `E0` is the expression that will be evaluated if none of the null checks represented by the `?`s do find a `null`.</span></span>

<span data-ttu-id="602c5-1501">또한 `E1` 텍스트가 앞에 오는 제거 하 여 얻은 식일 `?` 만에서 첫 번째는 *null_conditional_operations* 에서 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1501">Also, let `E1` be the expression obtained by textually removing the leading `?` from just the first of the *null_conditional_operations* in `E`.</span></span> <span data-ttu-id="602c5-1502">이로 인해 발생할 수 있습니다는 *기본 식을* (하나만 있으면 `?`) 또는 다른 *null_conditional_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1502">This may lead to a *primary-expression* (if there was just one `?`) or to another *null_conditional_expression*.</span></span>

<span data-ttu-id="602c5-1503">예를 들어 경우 `E` 식 `a.b?[0]?.c()`, 한 다음 `E0` 식 `a.b[0].c()` 및 `E1` 식 `a.b[0]?.c()`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1503">For example, if `E` is the expression `a.b?[0]?.c()`, then `E0` is the expression `a.b[0].c()` and `E1` is the expression `a.b[0]?.c()`.</span></span>

<span data-ttu-id="602c5-1504">하는 경우 `E0` 한 후 아무 것도로 분류 됩니다 `E` nothing으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1504">If `E0` is classified as nothing, then `E` is classified as nothing.</span></span> <span data-ttu-id="602c5-1505">그렇지 않으면 전자를 값으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1505">Otherwise E is classified as a value.</span></span>

<span data-ttu-id="602c5-1506">`E0` 및 `E1` 의 의미를 확인 하는 데 사용 됩니다 `E`:</span><span class="sxs-lookup"><span data-stu-id="602c5-1506">`E0` and `E1` are used to determine the meaning of `E`:</span></span>

*  <span data-ttu-id="602c5-1507">하는 경우 `E` 으로 발생 한 *statement_expression* 의 의미를 `E` 문과 동일</span><span class="sxs-lookup"><span data-stu-id="602c5-1507">If `E` occurs as a *statement_expression* the meaning of `E` is the same as the statement</span></span>

   ```csharp
   if ((object)P != null) E1;
   ```

   <span data-ttu-id="602c5-1508">제외 하 고 P가 한 번만 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1508">except that P is evaluated only once.</span></span>

*  <span data-ttu-id="602c5-1509">그렇지 않은 경우, `E0` 컴파일 타임 오류가 발생 하는 것으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1509">Otherwise, if `E0` is classified as nothing a compile-time error occurs.</span></span>

*  <span data-ttu-id="602c5-1510">수이 고, 그렇지 `T0` 가 형식의 `E0`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1510">Otherwise, let `T0` be the type of `E0`.</span></span>

   *  <span data-ttu-id="602c5-1511">경우 `T0` 는 컴파일 타임 오류가 발생 하는 참조 형식 또는 nullable이 아닌 값 형식 이어야 알려지지 않은 형식 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1511">If `T0` is a type parameter that is not known to be a reference type or a non-nullable value type, a compile-time error occurs.</span></span>

   *  <span data-ttu-id="602c5-1512">경우 `T0` 가 null이 아닌 값 형식 유형의 `E` 은 `T0?`, 및의 의미를 `E` 같습니다</span><span class="sxs-lookup"><span data-stu-id="602c5-1512">If `T0` is a non-nullable value type, then the type of `E` is `T0?`, and the meaning of `E` is the same as</span></span>

      ```csharp
      ((object)P == null) ? (T0?)null : E1
      ```

      <span data-ttu-id="602c5-1513">점을 제외 하 고 `P` 한 번만 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1513">except that `P` is evaluated only once.</span></span>

   *  <span data-ttu-id="602c5-1514">그렇지 않으면 E 형식이 T0, 이며 E의 의미와 동일</span><span class="sxs-lookup"><span data-stu-id="602c5-1514">Otherwise the type of E is T0, and the meaning of E is the same as</span></span>

      ```csharp
      ((object)P == null) ? null : E1
      ```

      <span data-ttu-id="602c5-1515">점을 제외 하 고 `P` 한 번만 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1515">except that `P` is evaluated only once.</span></span>

<span data-ttu-id="602c5-1516">경우 `E1` 자체는 *null_conditional_expression*, 그런 다음 이러한 규칙은 다시에 대 한 테스트를 중첩 `null` 없을 때까지 더 이상 `?`의 식 아래로 줄었습니다 및 기본 식 `E0`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1516">If `E1` is itself a *null_conditional_expression*, then these rules are applied again, nesting the tests for `null` until there are no further `?`'s, and the expression has been reduced all the way down to the primary-expression `E0`.</span></span>

<span data-ttu-id="602c5-1517">예를 들어 경우 식 `a.b?[0]?.c()` 문-식으로 문에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1517">For example, if the expression `a.b?[0]?.c()` occurs as a statement-expression, as in the statement:</span></span>
```csharp
a.b?[0]?.c();
```
<span data-ttu-id="602c5-1518">해당 의미는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1518">its meaning is equivalent to:</span></span>
```csharp
if (a.b != null) a.b[0]?.c();
```
<span data-ttu-id="602c5-1519">다시 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1519">which again is equivalent to:</span></span>
```csharp
if (a.b != null) if (a.b[0] != null) a.b[0].c();
```
<span data-ttu-id="602c5-1520">한다는 `a.b` 고 `a.b[0]` 한 번만 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1520">Except that `a.b` and `a.b[0]` are evaluated only once.</span></span>

<span data-ttu-id="602c5-1521">경우는 해당 값이 사용에서 같이 컨텍스트에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1521">If it occurs in a context where its value is used, as in:</span></span>
```csharp
var x = a.b?[0]?.c();
```
<span data-ttu-id="602c5-1522">및 해당 의미에 해당 하는 마지막 호출의 형식이 nullable이 아닌 값 형식이 아닌를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1522">and assuming that the type of the final invocation is not a non-nullable value type, its meaning is equivalent to:</span></span>
```csharp
var x = (a.b == null) ? null : (a.b[0] == null) ? null : a.b[0].c();
```
<span data-ttu-id="602c5-1523">한다는 `a.b` 고 `a.b[0]` 한 번만 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1523">except that `a.b` and `a.b[0]` are evaluated only once.</span></span>

#### <a name="null-conditional-expressions-as-projection-initializers"></a><span data-ttu-id="602c5-1524">Null 조건부 식을 프로젝션 이니셜라이저</span><span class="sxs-lookup"><span data-stu-id="602c5-1524">Null-conditional expressions as projection initializers</span></span>

<span data-ttu-id="602c5-1525">Null 조건부 식 으로만 사용할 수는 *member_declarator* 에 *anonymous_object_creation_expression* ([익명 개체 생성 식을](expressions.md#anonymous-object-creation-expressions)) 하는 경우 (필요에 따라 null 조건부) 멤버 액세스를 사용 하 여 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1525">A null-conditional expression is only allowed as a *member_declarator* in an *anonymous_object_creation_expression* ([Anonymous object creation expressions](expressions.md#anonymous-object-creation-expressions)) if it ends with an (optionally null-conditional) member access.</span></span> <span data-ttu-id="602c5-1526">문법적으로,이 요구 사항으로 표현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1526">Grammatically, this requirement can be expressed as:</span></span>

```antlr
null_conditional_member_access
    : primary_expression null_conditional_operations? '?' '.' identifier type_argument_list?
    | primary_expression null_conditional_operations '.' identifier type_argument_list?
    ;
```

<span data-ttu-id="602c5-1527">에 대 한 문법의 특별 한 경우 이것이 *null_conditional_expression* 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1527">This is a special case of the grammar for *null_conditional_expression* above.</span></span> <span data-ttu-id="602c5-1528">에 대 한 프로덕션 *member_declarator* 에 [익명 개체 생성 식을](expressions.md#anonymous-object-creation-expressions) 만 포함 됩니다 *null_conditional_member_access*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1528">The production for *member_declarator* in [Anonymous object creation expressions](expressions.md#anonymous-object-creation-expressions) then includes only *null_conditional_member_access*.</span></span>

#### <a name="null-conditional-expressions-as-statement-expressions"></a><span data-ttu-id="602c5-1529">Null 조건부 식 문의 식으로</span><span class="sxs-lookup"><span data-stu-id="602c5-1529">Null-conditional expressions as statement expressions</span></span>

<span data-ttu-id="602c5-1530">Null 조건부 식 으로만 사용할 수는 *statement_expression* ([식 문은](statements.md#expression-statements)) 호출으로 끝나는 경우.</span><span class="sxs-lookup"><span data-stu-id="602c5-1530">A null-conditional expression is only allowed as a *statement_expression* ([Expression statements](statements.md#expression-statements)) if it ends with an invocation.</span></span> <span data-ttu-id="602c5-1531">문법적으로,이 요구 사항으로 표현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1531">Grammatically, this requirement can be expressed as:</span></span>

```antlr
null_conditional_invocation_expression
    : primary_expression null_conditional_operations '(' argument_list? ')'
    ;
```

<span data-ttu-id="602c5-1532">에 대 한 문법의 특별 한 경우 이것이 *null_conditional_expression* 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1532">This is a special case of the grammar for *null_conditional_expression* above.</span></span> <span data-ttu-id="602c5-1533">에 대 한 프로덕션 *statement_expression* 에 [식 문은](statements.md#expression-statements) 만 포함 됩니다 *null_conditional_invocation_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1533">The production for *statement_expression* in [Expression statements](statements.md#expression-statements) then includes only *null_conditional_invocation_expression*.</span></span>


### <a name="unary-plus-operator"></a><span data-ttu-id="602c5-1534">단항 더하기 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1534">Unary plus operator</span></span>

<span data-ttu-id="602c5-1535">폼의 작업에 대 한 `+x`, 단항 연산자 오버 로드 확인 ([단항 연산자 오버 로드 확인](expressions.md#unary-operator-overload-resolution)) 특정 연산자 구현을 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1535">For an operation of the form `+x`, unary operator overload resolution ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="602c5-1536">피연산자는 선택한 연산자의 매개 변수 형식으로 변환 됩니다 및 결과의 형식은 연산자의 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1536">The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator.</span></span> <span data-ttu-id="602c5-1537">미리 정의 된 단항 더하기 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1537">The predefined unary plus operators are:</span></span>

```csharp
int operator +(int x);
uint operator +(uint x);
long operator +(long x);
ulong operator +(ulong x);
float operator +(float x);
double operator +(double x);
decimal operator +(decimal x);
```

<span data-ttu-id="602c5-1538">이러한 연산자의 각각에 대 한 결과 단순히 피연산자의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1538">For each of these operators, the result is simply the value of the operand.</span></span>

### <a name="unary-minus-operator"></a><span data-ttu-id="602c5-1539">단항 빼기 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1539">Unary minus operator</span></span>

<span data-ttu-id="602c5-1540">폼의 작업에 대 한 `-x`, 단항 연산자 오버 로드 확인 ([단항 연산자 오버 로드 확인](expressions.md#unary-operator-overload-resolution)) 특정 연산자 구현을 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1540">For an operation of the form `-x`, unary operator overload resolution ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="602c5-1541">피연산자는 선택한 연산자의 매개 변수 형식으로 변환 됩니다 및 결과의 형식은 연산자의 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1541">The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator.</span></span> <span data-ttu-id="602c5-1542">미리 정의 된 부정 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1542">The predefined negation operators are:</span></span>

*  <span data-ttu-id="602c5-1543">정수 부정:</span><span class="sxs-lookup"><span data-stu-id="602c5-1543">Integer negation:</span></span>

   ```csharp
   int operator -(int x);
   long operator -(long x);
   ```

   <span data-ttu-id="602c5-1544">빼는 방식으로 결과가 `x` 0에서.</span><span class="sxs-lookup"><span data-stu-id="602c5-1544">The result is computed by subtracting `x` from zero.</span></span> <span data-ttu-id="602c5-1545">하는 경우의 값 `x` 피연산자 형식의 표현할 수 있는 가장 작은 값 (-2 ^31에 대 한 `int` -2 ^63에 대 한 `long`)의 산술 부정 다음 `x` 피연산자 형식 내에서 표현할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1545">If the value of of `x` is the smallest representable value of the operand type (-2^31 for `int` or -2^63 for `long`), then the mathematical negation of `x` is not representable within the operand type.</span></span> <span data-ttu-id="602c5-1546">내에서이 문제가 발생 하면를 `checked` 컨텍스트에 `System.OverflowException` 예외가; 내에서 발생 하는 경우는 `unchecked` 컨텍스트는 결과 피연산자의 값 및 오버플로 보고 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1546">If this occurs within a `checked` context, a `System.OverflowException` is thrown; if it occurs within an `unchecked` context, the result is the value of the operand and the overflow is not reported.</span></span>

   <span data-ttu-id="602c5-1547">부정 연산자의 피연산자는 형식입니다 `uint`, 형식으로 변환 됩니다 `long`, 및 결과의 형식은 `long`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1547">If the operand of the negation operator is of type `uint`, it is converted to type `long`, and the type of the result is `long`.</span></span> <span data-ttu-id="602c5-1548">예외는 허용 하는 규칙을 `int` -2147483648 값 (-2 ^31) 리터럴 10 진수 정수로 쓸 ([정수 리터럴](lexical-structure.md#integer-literals)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1548">An exception is the rule that permits the `int` value -2147483648 (-2^31) to be written as a decimal integer literal ([Integer literals](lexical-structure.md#integer-literals)).</span></span>

   <span data-ttu-id="602c5-1549">부정 연산자의 피연산자는 형식입니다 `ulong`, 컴파일 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1549">If the operand of the negation operator is of type `ulong`, a compile-time error occurs.</span></span> <span data-ttu-id="602c5-1550">예외는 허용 하는 규칙을 `long` -9223372036854775808 값 (-2 ^63) 10 진수 정수 리터럴로 작성 ([정수 리터럴](lexical-structure.md#integer-literals)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1550">An exception is the rule that permits the `long` value -9223372036854775808 (-2^63) to be written as a decimal integer literal ([Integer literals](lexical-structure.md#integer-literals)).</span></span>

*  <span data-ttu-id="602c5-1551">부동 소수점 부정:</span><span class="sxs-lookup"><span data-stu-id="602c5-1551">Floating-point negation:</span></span>

   ```csharp
   float operator -(float x);
   double operator -(double x);
   ```

   <span data-ttu-id="602c5-1552">결과의 값인 `x` 의 부호를 반전 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1552">The result is the value of `x` with its sign inverted.</span></span> <span data-ttu-id="602c5-1553">경우 `x` 가 NaN 결과가 NaN 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1553">If `x` is NaN, the result is also NaN.</span></span>

*  <span data-ttu-id="602c5-1554">10 진수 부정:</span><span class="sxs-lookup"><span data-stu-id="602c5-1554">Decimal negation:</span></span>

   ```csharp
   decimal operator -(decimal x);
   ```

   <span data-ttu-id="602c5-1555">빼는 방식으로 결과가 `x` 0에서.</span><span class="sxs-lookup"><span data-stu-id="602c5-1555">The result is computed by subtracting `x` from zero.</span></span> <span data-ttu-id="602c5-1556">10 진수 부정 연산을 사용 하는 단항 빼기 연산자 형식의 `System.Decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1556">Decimal negation is equivalent to using the unary minus operator of type `System.Decimal`.</span></span>

### <a name="logical-negation-operator"></a><span data-ttu-id="602c5-1557">논리 부정 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1557">Logical negation operator</span></span>

<span data-ttu-id="602c5-1558">폼의 작업에 대 한 `!x`, 단항 연산자 오버 로드 확인 ([단항 연산자 오버 로드 확인](expressions.md#unary-operator-overload-resolution)) 특정 연산자 구현을 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1558">For an operation of the form `!x`, unary operator overload resolution ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="602c5-1559">피연산자는 선택한 연산자의 매개 변수 형식으로 변환 됩니다 및 결과의 형식은 연산자의 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1559">The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator.</span></span> <span data-ttu-id="602c5-1560">미리 정의 된 논리 부정 연산자를 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1560">Only one predefined logical negation operator exists:</span></span>
```csharp
bool operator !(bool x);
```

<span data-ttu-id="602c5-1561">이 연산자는 피연산자의 논리 부정을 계산: 피연산자가 `true`, 결과 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1561">This operator computes the logical negation of the operand: If the operand is `true`, the result is `false`.</span></span> <span data-ttu-id="602c5-1562">피연산자가 `false`, 결과 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1562">If the operand is `false`, the result is `true`.</span></span>

### <a name="bitwise-complement-operator"></a><span data-ttu-id="602c5-1563">비트 보수 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1563">Bitwise complement operator</span></span>

<span data-ttu-id="602c5-1564">폼의 작업에 대 한 `~x`, 단항 연산자 오버 로드 확인 ([단항 연산자 오버 로드 확인](expressions.md#unary-operator-overload-resolution)) 특정 연산자 구현을 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1564">For an operation of the form `~x`, unary operator overload resolution ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="602c5-1565">피연산자는 선택한 연산자의 매개 변수 형식으로 변환 됩니다 및 결과의 형식은 연산자의 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1565">The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator.</span></span> <span data-ttu-id="602c5-1566">미리 정의 된 비트 보수 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1566">The predefined bitwise complement operators are:</span></span>
```csharp
int operator ~(int x);
uint operator ~(uint x);
long operator ~(long x);
ulong operator ~(ulong x);
```

<span data-ttu-id="602c5-1567">이러한 연산자의 각각에 대 한 작업의 결과의 비트 보수 `x`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1567">For each of these operators, the result of the operation is the bitwise complement of `x`.</span></span>

<span data-ttu-id="602c5-1568">모든 열거형 형식 `E` 암시적으로 다음 비트 보수 연산자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1568">Every enumeration type `E` implicitly provides the following bitwise complement operator:</span></span>

```csharp
E operator ~(E x);
```

<span data-ttu-id="602c5-1569">평가 결과 `~x`, 여기서 `x` 열거형 형식의 식이 `E` 기본 형식을 사용 하 여 `U`, 같습니다 정확 하 게 평가 `(E)(~(U)x)`점을 제외 하 고로 변환 `E` 는 으로 항상 수행의 경우는 `unchecked` 컨텍스트 ([checked 및 unchecked 연산자](expressions.md#the-checked-and-unchecked-operators)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1569">The result of evaluating `~x`, where `x` is an expression of an enumeration type `E` with an underlying type `U`, is exactly the same as evaluating `(E)(~(U)x)`, except that the conversion to `E` is always performed as if in an `unchecked` context ([The checked and unchecked operators](expressions.md#the-checked-and-unchecked-operators)).</span></span>

### <a name="prefix-increment-and-decrement-operators"></a><span data-ttu-id="602c5-1570">전위 증가 및 감소 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1570">Prefix increment and decrement operators</span></span>

```antlr
pre_increment_expression
    : '++' unary_expression
    ;

pre_decrement_expression
    : '--' unary_expression
    ;
```

<span data-ttu-id="602c5-1571">피연산자 전위 증가 또는 감소 작업 변수, 속성 액세스 또는 인덱서 액세스로 분류 되는 식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1571">The operand of a prefix increment or decrement operation must be an expression classified as a variable, a property access, or an indexer access.</span></span> <span data-ttu-id="602c5-1572">작업의 결과 피연산자와 동일한 형식의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1572">The result of the operation is a value of the same type as the operand.</span></span>

<span data-ttu-id="602c5-1573">접두사의 피연산자가 증가 하는 경우 감소 작업은 속성 또는 인덱서 액세스, 속성 또는 인덱서 둘 다 있어야 합니다는 `get` 및 `set` 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1573">If the operand of a prefix increment or decrement operation is a property or indexer access, the property or indexer must have both a `get` and a `set` accessor.</span></span> <span data-ttu-id="602c5-1574">이 경우 바인딩 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1574">If this is not the case, a binding-time error occurs.</span></span>

<span data-ttu-id="602c5-1575">단항 연산자 오버 로드 확인 ([단항 연산자 오버 로드 확인](expressions.md#unary-operator-overload-resolution)) 특정 연산자 구현을 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1575">Unary operator overload resolution ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="602c5-1576">미리 정의 된 `++` 하 고 `--` 연산자는 다음 형식에 대해 존재: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char` 를 `float`, `double`, `decimal`, 및 열거형 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1576">Predefined `++` and `--` operators exist for the following types: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, and any enum type.</span></span> <span data-ttu-id="602c5-1577">미리 정의 된 `++` 연산자는 피연산자 및 미리 정의 된에 1을 추가 하 여 생성 한 값을 반환 `--` 연산자는 피연산자에서 1을 뺀 값으로 계산 된 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1577">The predefined `++` operators return the value produced by adding 1 to the operand, and the predefined `--` operators return the value produced by subtracting 1 from the operand.</span></span> <span data-ttu-id="602c5-1578">에 `checked` 컨텍스트를 결과 형식이 정수 계열 형식 또는 열거형 형식에는이 더하기 또는 빼기의 결과 결과 형식 범위를 벗어나는 경우는 `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1578">In a `checked` context, if the result of this addition or subtraction is outside the range of the result type and the result type is an integral type or enum type, a `System.OverflowException` is thrown.</span></span>

<span data-ttu-id="602c5-1579">접두사 증가 처리 하는 런타임 또는 폼의 작업 감소 `++x` 또는 `--x` 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1579">The run-time processing of a prefix increment or decrement operation of the form `++x` or `--x` consists of the following steps:</span></span>

*   <span data-ttu-id="602c5-1580">경우 `x` 변수로로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1580">If `x` is classified as a variable:</span></span>
    * <span data-ttu-id="602c5-1581">`x` 변수를 생성 하기 위해 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1581">`x` is evaluated to produce the variable.</span></span>
    * <span data-ttu-id="602c5-1582">선택한 연산자의 값을 사용 하 여 호출 `x` 인수로 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1582">The selected operator is invoked with the value of `x` as its argument.</span></span>
    * <span data-ttu-id="602c5-1583">연산자로 반환 되는 값을 평가 하 여 지정 된 위치에 저장 됩니다 `x`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1583">The value returned by the operator is stored in the location given by the evaluation of `x`.</span></span>
    * <span data-ttu-id="602c5-1584">연산자에서 반환 된 값에는 작업의 결과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1584">The value returned by the operator becomes the result of the operation.</span></span>
*   <span data-ttu-id="602c5-1585">경우 `x` 속성 또는 인덱서에 액세스로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1585">If `x` is classified as a property or indexer access:</span></span>
    * <span data-ttu-id="602c5-1586">인스턴스 식 (하는 경우 `x` 아닙니다 `static`) 및 인수 목록을 (경우 `x` 인덱서 액세스할)와 연결 된 `x` 평가 결과에서 사용 하는 후속 `get` 및 `set` 접근자 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1586">The instance expression (if `x` is not `static`) and the argument list (if `x` is an indexer access) associated with `x` are evaluated, and the results are used in the subsequent `get` and `set` accessor invocations.</span></span>
    * <span data-ttu-id="602c5-1587">합니다 `get` 접근자의 `x` 가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1587">The `get` accessor of `x` is invoked.</span></span>
    * <span data-ttu-id="602c5-1588">선택한 연산자에서 반환 된 값을 사용 하 여 호출 되는 `get` 인수로 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1588">The selected operator is invoked with the value returned by the `get` accessor as its argument.</span></span>
    * <span data-ttu-id="602c5-1589">합니다 `set` 의 접근자 `x` 으로 연산자로 반환 되는 값을 사용 하 여 호출 해당 `value` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1589">The `set` accessor of `x` is invoked with the value returned by the operator as its `value` argument.</span></span>
    * <span data-ttu-id="602c5-1590">연산자에서 반환 된 값에는 작업의 결과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1590">The value returned by the operator becomes the result of the operation.</span></span>

<span data-ttu-id="602c5-1591">합니다 `++` 하 고 `--` 연산자는 후 위 기능도 표기법 ([후 위 증가 및 감소 연산자](expressions.md#postfix-increment-and-decrement-operators)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1591">The `++` and `--` operators also support postfix notation ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators)).</span></span> <span data-ttu-id="602c5-1592">일반적으로 결과 `x++` 또는 `x--` 의 값인 `x` 작업 전에 반면 결과인 `++x` 또는 `--x` 의 값인 `x` 작업 후.</span><span class="sxs-lookup"><span data-stu-id="602c5-1592">Typically, the result of `x++` or `x--` is the value of `x` before the operation, whereas the result of `++x` or `--x` is the value of `x` after the operation.</span></span> <span data-ttu-id="602c5-1593">두 경우 모두 `x` 작업 후 같은 값을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1593">In either case, `x` itself has the same value after the operation.</span></span>

<span data-ttu-id="602c5-1594">`operator++` 또는 `operator--` 구현 후 위 또는 접두사 표기법을 사용 하 여 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1594">An `operator++` or `operator--` implementation can be invoked using either postfix or prefix notation.</span></span> <span data-ttu-id="602c5-1595">두 표기법이 대 한 별도 연산자 구현이 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1595">It is not possible to have separate operator implementations for the two notations.</span></span>

### <a name="cast-expressions"></a><span data-ttu-id="602c5-1596">캐스트 식</span><span class="sxs-lookup"><span data-stu-id="602c5-1596">Cast expressions</span></span>

<span data-ttu-id="602c5-1597">A *cast_expression* 식이 지정된 된 형식으로 명시적으로 변환 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1597">A *cast_expression* is used to explicitly convert an expression to a given type.</span></span>

```antlr
cast_expression
    : '(' type ')' unary_expression
    ;
```

<span data-ttu-id="602c5-1598">*cast_expression* 양식의 `(T)E`여기서 `T` 는 *형식* 및 `E` 는 *unary_expression*, 명시적인 수행 변환 ([명시적 변환](conversions.md#explicit-conversions))의 값 `E` 형식으로 `T`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1598">A *cast_expression* of the form `(T)E`, where `T` is a *type* and `E` is a *unary_expression*, performs an explicit conversion ([Explicit conversions](conversions.md#explicit-conversions)) of the value of `E` to type `T`.</span></span> <span data-ttu-id="602c5-1599">명시적 변환이 없는 경우 `E` 에 `T`, 바인딩 시간에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1599">If no explicit conversion exists from `E` to `T`, a binding-time error occurs.</span></span> <span data-ttu-id="602c5-1600">그렇지 않으면 결과 명시적 변환에 의해 생성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1600">Otherwise, the result is the value produced by the explicit conversion.</span></span> <span data-ttu-id="602c5-1601">결과 항상 값으로 분류 됩니다. 경우에 `E` 변수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1601">The result is always classified as a value, even if `E` denotes a variable.</span></span>

<span data-ttu-id="602c5-1602">에 대 한 문법을 *cast_expression* 특정 구문 모호성이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1602">The grammar for a *cast_expression* leads to certain syntactic ambiguities.</span></span> <span data-ttu-id="602c5-1603">예를 들어 식 `(x)-y` 하거나로 해석 될 수는 *cast_expression* (캐스트 `-y` 형식으로 `x`) 또는 *additive_expression* 함께 *parenthesized_expression* (값을 계산 하는 `x - y)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1603">For example, the expression `(x)-y` could either be interpreted as a *cast_expression* (a cast of `-y` to type `x`) or as an *additive_expression* combined with a *parenthesized_expression* (which computes the value `x - y)`.</span></span>

<span data-ttu-id="602c5-1604">해결 하려면 *cast_expression* 모호성이 있으면 다음과 같은 규칙이 존재: 하나 이상의 시퀀스 *토큰*s ([공백](lexical-structure.md#white-space)) 묶인 괄호 안에 있는 것으로 간주 됩니다 시작 한 *cast_expression* 다음 중 하나 이상에 해당할 경우에:</span><span class="sxs-lookup"><span data-stu-id="602c5-1604">To resolve *cast_expression* ambiguities, the following rule exists: A sequence of one or more *token*s ([White space](lexical-structure.md#white-space)) enclosed in parentheses is considered the start of a *cast_expression* only if at least one of the following are true:</span></span>

*  <span data-ttu-id="602c5-1605">토큰의 순서가 올바른 문법에 대 한는 *형식*, 아니라는 *식*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1605">The sequence of tokens is correct grammar for a *type*, but not for an *expression*.</span></span>
*  <span data-ttu-id="602c5-1606">토큰의 순서가 올바른 문법에 대 한는 *형식*, 닫는 괄호 바로 다음에 오는 토큰은 토큰 및 "`~`", 토큰 "`!`", 토큰 "`(`",  *식별자* ([유니코드 문자 이스케이프 시퀀스인](lexical-structure.md#unicode-character-escape-sequences)), *리터럴* ([리터럴](lexical-structure.md#literals)), 또는 *키워드*([키워드](lexical-structure.md#keywords))를 제외한 `as` 고 `is`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1606">The sequence of tokens is correct grammar for a *type*, and the token immediately following the closing parentheses is the token "`~`", the token "`!`", the token "`(`", an *identifier* ([Unicode character escape sequences](lexical-structure.md#unicode-character-escape-sequences)), a *literal* ([Literals](lexical-structure.md#literals)), or any *keyword* ([Keywords](lexical-structure.md#keywords)) except `as` and `is`.</span></span>

<span data-ttu-id="602c5-1607">용어 "올바른 문법" 위에 특정 문법 프로덕션 토큰 시퀀스를 따라야 한다는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1607">The term "correct grammar" above means only that the sequence of tokens must conform to the particular grammatical production.</span></span> <span data-ttu-id="602c5-1608">구체적으로 구성 하는 식별자의 실제 의미를 고려 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1608">It specifically does not consider the actual meaning of any constituent identifiers.</span></span> <span data-ttu-id="602c5-1609">예를 들어 경우 `x` 및 `y` 있다면 식별자 `x.y` 형식에 대 한 올바른 문법은 경우에 `x.y` 실제로 형식을 나타내지.</span><span class="sxs-lookup"><span data-stu-id="602c5-1609">For example, if `x` and `y` are identifiers, then `x.y` is correct grammar for a type, even if `x.y` doesn't actually denote a type.</span></span>

<span data-ttu-id="602c5-1610">경우 따릅니다는 명확성 규칙에서 `x` 및 `y` 가 식별자 인 `(x)y`, `(x)(y)`, 및 `(x)(-y)` 됩니다 *cast_expression*s, 하지만 `(x)-y` 그렇지 않을 경우에 `x` 형식을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1610">From the disambiguation rule it follows that, if `x` and `y` are identifiers, `(x)y`, `(x)(y)`, and `(x)(-y)` are *cast_expression*s, but `(x)-y` is not, even if `x` identifies a type.</span></span> <span data-ttu-id="602c5-1611">그러나 경우 `x` 미리 정의 된 형식을 식별 하는 키워드 (같은 `int`), 다음 4 가지 형태가 모두 *cast_expression*s (이러한 키워드 수 있는 수 없으므로 식 자체).</span><span class="sxs-lookup"><span data-stu-id="602c5-1611">However, if `x` is a keyword that identifies a predefined type (such as `int`), then all four forms are *cast_expression*s (because such a keyword could not possibly be an expression by itself).</span></span>

### <a name="await-expressions"></a><span data-ttu-id="602c5-1612">Await 식</span><span class="sxs-lookup"><span data-stu-id="602c5-1612">Await expressions</span></span>

<span data-ttu-id="602c5-1613">Await 연산자는 피연산자를 나타내는 비동기 작업이 완료 될 때까지 바깥쪽 비동기 함수를 일시 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1613">The await operator is used to suspend evaluation of the enclosing async function until the asynchronous operation represented by the operand has completed.</span></span>

```antlr
await_expression
    : 'await' unary_expression
    ;
```

<span data-ttu-id="602c5-1614">*await_expression* 비동기 함수의 본문 에서만 허용 됩니다 ([반복기](classes.md#iterators)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1614">An *await_expression* is only allowed in the body of an async function ([Iterators](classes.md#iterators)).</span></span> <span data-ttu-id="602c5-1615">가장 가까운 바깥쪽 내 비동기 함수는 *await_expression* 이러한 위치에서 발생 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1615">Within the nearest enclosing async function, an *await_expression* may not occur in these places:</span></span>

*  <span data-ttu-id="602c5-1616">중첩 된 (비동기가 아닌) 익명 함수 내에서</span><span class="sxs-lookup"><span data-stu-id="602c5-1616">Inside a nested (non-async) anonymous function</span></span>
*  <span data-ttu-id="602c5-1617">블록을 *lock_statement*</span><span class="sxs-lookup"><span data-stu-id="602c5-1617">Inside the block of a *lock_statement*</span></span>
*  <span data-ttu-id="602c5-1618">안전 하지 않은 컨텍스트에서</span><span class="sxs-lookup"><span data-stu-id="602c5-1618">In an unsafe context</span></span>

<span data-ttu-id="602c5-1619">*await_expression* 내에서 대부분의 위치에 사용할 수 없습니다는 *query_expression*이므로 해당 구문이 비동기 람다 식을 사용 하 여 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1619">Note that an *await_expression* cannot occur in most places within a *query_expression*, because those are syntactically transformed to use non-async lambda expressions.</span></span>

<span data-ttu-id="602c5-1620">비동기 함수 내에서 `await` 식별자로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1620">Inside of an async function, `await` cannot be used as an identifier.</span></span> <span data-ttu-id="602c5-1621">Await 식 및 식별자를 포함 하는 다양 한 식 사이 없는 구문 모호성이 되므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1621">There is therefore no syntactic ambiguity between await-expressions and various expressions involving identifiers.</span></span> <span data-ttu-id="602c5-1622">비동기 함수 외부에서 `await` 일반 식별자 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1622">Outside of async functions, `await` acts as a normal identifier.</span></span>

<span data-ttu-id="602c5-1623">피연산자는 *await_expression* 라고 합니다 ***태스크***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1623">The operand of an *await_expression* is called the ***task***.</span></span> <span data-ttu-id="602c5-1624">되었거나 완전 하지 않을 경우에는 비동기 작업을 나타내므로 합니다 *await_expression* 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1624">It represents an asynchronous operation that may or may not be complete at the time the *await_expression* is evaluated.</span></span> <span data-ttu-id="602c5-1625">Await 연산자의 목적은 대기 중인된 작업이 완료 될 때까지 바깥쪽 비동기 함수의 실행을 중단 하 고 그런 다음 해당 결과 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1625">The purpose of the await operator is to suspend execution of the enclosing async function until the awaited task is complete, and then obtain its outcome.</span></span>

#### <a name="awaitable-expressions"></a><span data-ttu-id="602c5-1626">대기 가능 식</span><span class="sxs-lookup"><span data-stu-id="602c5-1626">Awaitable expressions</span></span>

<span data-ttu-id="602c5-1627">Await 식이 작업 되어야 할 ***awaitable***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1627">The task of an await expression is required to be ***awaitable***.</span></span> <span data-ttu-id="602c5-1628">식을 `t` 비동기로 다음 중 하나를 보유 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-1628">An expression `t` is awaitable if one of the following holds:</span></span>

*  <span data-ttu-id="602c5-1629">`t` 컴파일 시간 형식입니다. `dynamic`</span><span class="sxs-lookup"><span data-stu-id="602c5-1629">`t` is of compile time type `dynamic`</span></span>
*  <span data-ttu-id="602c5-1630">`t` 호출 액세스할 수 있는 인스턴스 또는 확장 메서드를 포함 `GetAwaiter` 매개 변수 없이 없는 형식 매개 변수 및 반환 형식을 `A` 저장한 다음이 모두는:</span><span class="sxs-lookup"><span data-stu-id="602c5-1630">`t` has an accessible instance or extension method called `GetAwaiter` with no parameters and no type parameters, and a return type `A` for which all of the following hold:</span></span>
   * <span data-ttu-id="602c5-1631">`A` 인터페이스를 구현 `System.Runtime.CompilerServices.INotifyCompletion` (이 이라고 `INotifyCompletion` 간략하게 표현 하기 위해)</span><span class="sxs-lookup"><span data-stu-id="602c5-1631">`A` implements the interface `System.Runtime.CompilerServices.INotifyCompletion` (hereafter known as `INotifyCompletion` for brevity)</span></span>
   * <span data-ttu-id="602c5-1632">`A` 에 액세스할 수 있는 읽을 수 있는 인스턴스 속성 `IsCompleted` 형식 `bool`</span><span class="sxs-lookup"><span data-stu-id="602c5-1632">`A` has an accessible, readable instance property `IsCompleted` of type `bool`</span></span>
   * <span data-ttu-id="602c5-1633">`A` 에 액세스할 수 있는 인스턴스 메서드가 `GetResult` 매개 변수 없이와 없는 형식 매개 변수</span><span class="sxs-lookup"><span data-stu-id="602c5-1633">`A` has an accessible instance method `GetResult` with no parameters and no type parameters</span></span>

<span data-ttu-id="602c5-1634">용도 `GetAwaiter` 가져오려고 메서드는는 ***awaiter*** 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1634">The purpose of the `GetAwaiter` method is to obtain an ***awaiter*** for the task.</span></span> <span data-ttu-id="602c5-1635">형식 `A` 라고 합니다 ***awaiter 형식*** await 식에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1635">The type `A` is called the ***awaiter type*** for the await expression.</span></span>

<span data-ttu-id="602c5-1636">용도 `IsCompleted` 속성 작업은 이미 완료 하는 경우를 결정 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1636">The purpose of the `IsCompleted` property is to determine if the task is already complete.</span></span> <span data-ttu-id="602c5-1637">따라서 있는지 평가 일시 중단할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1637">If so, there is no need to suspend evaluation.</span></span>

<span data-ttu-id="602c5-1638">목적은 `INotifyCompletion.OnCompleted` 방법은 태스크; "continuation" 등록 하는 대리자, 즉 (형식의 `System.Action`) 작업이 완료 되 면 호출 되는.</span><span class="sxs-lookup"><span data-stu-id="602c5-1638">The purpose of the `INotifyCompletion.OnCompleted` method is to sign up a "continuation" to the task; i.e. a delegate (of type `System.Action`) that will be invoked once the task is complete.</span></span>

<span data-ttu-id="602c5-1639">용도 `GetResult` 메서드는 완료 되 면 작업의 결과 가져오려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1639">The purpose of the `GetResult` method is to obtain the outcome of the task once it is complete.</span></span> <span data-ttu-id="602c5-1640">이 결과 결과 값을 사용 하 여 성공적으로 완료 되었거나 예외가 throw 되는 것은 `GetResult` 메서드.</span><span class="sxs-lookup"><span data-stu-id="602c5-1640">This outcome may be successful completion, possibly with a result value, or it may be an exception which is thrown by the `GetResult` method.</span></span>

#### <a name="classification-of-await-expressions"></a><span data-ttu-id="602c5-1641">Await 식 분류</span><span class="sxs-lookup"><span data-stu-id="602c5-1641">Classification of await expressions</span></span>

<span data-ttu-id="602c5-1642">식을 `await t` 식과 동일한 방식으로 분류 됩니다 `(t).GetAwaiter().GetResult()`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1642">The expression `await t` is classified the same way as the expression `(t).GetAwaiter().GetResult()`.</span></span> <span data-ttu-id="602c5-1643">따라서의 반환 형식이 `GetResult` 됩니다 `void`의 *await_expression* nothing으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1643">Thus, if the return type of `GetResult` is `void`, the *await_expression* is classified as nothing.</span></span> <span data-ttu-id="602c5-1644">Void가 아닌 반환 형식이 있을 경우 `T`서 *await_expression* 형식의 값으로 분류 됩니다 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1644">If it has a non-void return type `T`, the *await_expression* is classified as a value of type `T`.</span></span>

#### <a name="runtime-evaluation-of-await-expressions"></a><span data-ttu-id="602c5-1645">런타임 평가 await 식</span><span class="sxs-lookup"><span data-stu-id="602c5-1645">Runtime evaluation of await expressions</span></span>

<span data-ttu-id="602c5-1646">런타임에 식 `await t` 다음과 같이 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1646">At runtime, the expression `await t` is evaluated as follows:</span></span>

*  <span data-ttu-id="602c5-1647">Awaiter `a` 식을 평가 하 여 가져온 `(t).GetAwaiter()`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1647">An awaiter `a` is obtained by evaluating the expression `(t).GetAwaiter()`.</span></span>
*  <span data-ttu-id="602c5-1648">A `bool` `b` 식을 평가 하 여 가져온 `(a).IsCompleted`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1648">A `bool` `b` is obtained by evaluating the expression `(a).IsCompleted`.</span></span>
*  <span data-ttu-id="602c5-1649">경우 `b` 됩니다 `false` 을 평가 하는지에 따라 다릅니다 `a` 인터페이스를 구현 `System.Runtime.CompilerServices.ICriticalNotifyCompletion` (이 이라고 `ICriticalNotifyCompletion` 간략하게 표현 하기 위해).</span><span class="sxs-lookup"><span data-stu-id="602c5-1649">If `b` is `false` then evaluation depends on whether `a` implements the interface `System.Runtime.CompilerServices.ICriticalNotifyCompletion` (hereafter known as `ICriticalNotifyCompletion` for brevity).</span></span> <span data-ttu-id="602c5-1650">이 확인은 바인딩 시간;에서 수행 됩니다. 즉, 런타임에 경우 `a` 컴파일 시간 형식이 `dynamic`, 그렇지 않으면 컴파일 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1650">This check is done at binding time; i.e. at runtime if `a` has the compile time type `dynamic`, and at compile time otherwise.</span></span> <span data-ttu-id="602c5-1651">수 있도록 `r` 다시 시작 대리자를 나타냅니다 ([반복기](classes.md#iterators)):</span><span class="sxs-lookup"><span data-stu-id="602c5-1651">Let `r` denote the resumption delegate ([Iterators](classes.md#iterators)):</span></span>
    * <span data-ttu-id="602c5-1652">경우 `a` 를 구현 하지 않습니다 `ICriticalNotifyCompletion`, 다음 식은 `(a as (INotifyCompletion)).OnCompleted(r)` 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1652">If `a` does not implement `ICriticalNotifyCompletion`, then the expression `(a as (INotifyCompletion)).OnCompleted(r)` is evaluated.</span></span>
    * <span data-ttu-id="602c5-1653">경우 `a` 는 구현 `ICriticalNotifyCompletion`, 다음 식은 `(a as (ICriticalNotifyCompletion)).UnsafeOnCompleted(r)` 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1653">If `a` does implement `ICriticalNotifyCompletion`, then the expression `(a as (ICriticalNotifyCompletion)).UnsafeOnCompleted(r)` is evaluated.</span></span>
    * <span data-ttu-id="602c5-1654">평가 후 일시 중단 하 고 컨트롤이 비동기 함수의 현재 호출자에 게 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1654">Evaluation is then suspended, and control is returned to the current caller of the async function.</span></span>
*  <span data-ttu-id="602c5-1655">하거나 직후 (하는 경우 `b` 되었습니다 `true`), 또는 나중에 다시 시작 대리자의 호출 시 (경우 `b` 되었습니다 `false`), 식 `(a).GetResult()` 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1655">Either immediately after (if `b` was `true`), or upon later invocation of the resumption delegate (if `b` was `false`), the expression `(a).GetResult()` is evaluated.</span></span> <span data-ttu-id="602c5-1656">값이 결과 값을 반환 하는 경우는 *await_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1656">If it returns a value, that value is the result of the *await_expression*.</span></span> <span data-ttu-id="602c5-1657">그렇지 않으면 결과 아무 작업도 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1657">Otherwise the result is nothing.</span></span>

<span data-ttu-id="602c5-1658">인터페이스 메서드의 awaiter 구현 `INotifyCompletion.OnCompleted` 및 `ICriticalNotifyCompletion.UnsafeOnCompleted` 대리자 시키는 `r` 한 번만 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1658">An awaiter's implementation of the interface methods `INotifyCompletion.OnCompleted` and `ICriticalNotifyCompletion.UnsafeOnCompleted` should cause the delegate `r` to be invoked at most once.</span></span> <span data-ttu-id="602c5-1659">그렇지 않은 경우 바깥쪽 비동기 함수의 동작이 정의 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1659">Otherwise, the behavior of the enclosing async function is undefined.</span></span>

## <a name="arithmetic-operators"></a><span data-ttu-id="602c5-1660">산술 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1660">Arithmetic operators</span></span>

<span data-ttu-id="602c5-1661">`*`, `/`를 `%`, `+`, 및 `-` 연산자는 산술 연산자 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1661">The `*`, `/`, `%`, `+`, and `-` operators are called the arithmetic operators.</span></span>

```antlr
multiplicative_expression
    : unary_expression
    | multiplicative_expression '*' unary_expression
    | multiplicative_expression '/' unary_expression
    | multiplicative_expression '%' unary_expression
    ;

additive_expression
    : multiplicative_expression
    | additive_expression '+' multiplicative_expression
    | additive_expression '-' multiplicative_expression
    ;
```

<span data-ttu-id="602c5-1662">산술 연산자의 피연산자는 컴파일 시간 형식에 있는지 `dynamic`, 다음 식이 동적으로 바인딩 되었는지 ([동적 바인딩](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="602c5-1662">If an operand of an arithmetic operator has the compile-time type `dynamic`, then the expression is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="602c5-1663">이 경우 컴파일 시간 식의 형식이 `dynamic`, 아래에 설명 된 해결 방법을 컴파일 시간 형식이 해당 피연산자의 런타임 형식을 사용 하 여 런타임 시 수행 됩니다 및 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1663">In this case the compile-time type of the expression is `dynamic`, and the resolution described below will take place at run-time using the run-time type of those operands that have the compile-time type `dynamic`.</span></span>

### <a name="multiplication-operator"></a><span data-ttu-id="602c5-1664">곱하기 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1664">Multiplication operator</span></span>

<span data-ttu-id="602c5-1665">폼의 작업에 대 한 `x * y`, 이항 연산자 오버 로드 확인 ([이항 연산자 오버 로드 확인](expressions.md#binary-operator-overload-resolution)) 특정 연산자 구현을 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1665">For an operation of the form `x * y`, binary operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="602c5-1666">피연산자는 선택한 연산자의 매개 변수 형식으로 변환 됩니다 하 고 결과의 형식은 연산자의 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1666">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="602c5-1667">미리 정의 된 곱하기 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1667">The predefined multiplication operators are listed below.</span></span> <span data-ttu-id="602c5-1668">모든 연산자의 곱을 계산 합니다 `x` 고 `y`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1668">The operators all compute the product of `x` and `y`.</span></span>

*  <span data-ttu-id="602c5-1669">정수 곱하기</span><span class="sxs-lookup"><span data-stu-id="602c5-1669">Integer multiplication:</span></span>

   ```csharp
   int operator *(int x, int y);
   uint operator *(uint x, uint y);
   long operator *(long x, long y);
   ulong operator *(ulong x, ulong y);
   ```

   <span data-ttu-id="602c5-1670">에 `checked` 제품 결과 형식 범위를 벗어난 경우 컨텍스트는 `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1670">In a `checked` context, if the product is outside the range of the result type, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="602c5-1671">에 `unchecked` 컨텍스트에 오버플로 보고 되지 않으며 결과 형식 범위 밖에 있는 경우 중요 한 모든 상위 비트는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1671">In an `unchecked` context, overflows are not reported and any significant high-order bits outside the range of the result type are discarded.</span></span>


*  <span data-ttu-id="602c5-1672">부동 소수점 곱셈:</span><span class="sxs-lookup"><span data-stu-id="602c5-1672">Floating-point multiplication:</span></span>

   ```csharp
   float operator *(float x, float y);
   double operator *(double x, double y);
   ```

   <span data-ttu-id="602c5-1673">IEEE 754 산술 규칙에 따라 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1673">The product is computed according to the rules of IEEE 754 arithmetic.</span></span> <span data-ttu-id="602c5-1674">다음 표에서 한정 된 0이 아닌 값의 가능한 모든 조합, 0으로, 무한대 및 NaN의 결과 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1674">The following table lists the results of all possible combinations of nonzero finite values, zeros, infinities, and NaN's.</span></span> <span data-ttu-id="602c5-1675">표에 `x` 고 `y` 유한 값이 양수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1675">In the table, `x` and `y` are positive finite values.</span></span> <span data-ttu-id="602c5-1676">`z` 결과인 `x * y`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1676">`z` is the result of `x * y`.</span></span> <span data-ttu-id="602c5-1677">결과가 너무 커서 대상 유형에 적합 이면 `z` 무한대 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1677">If the result is too large for the destination type, `z` is infinity.</span></span> <span data-ttu-id="602c5-1678">결과 대상 형식에 대해 너무 작으면 `z` 은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1678">If the result is too small for the destination type, `z` is zero.</span></span>

   |      |      |      |     |     |      |      |     |
   |:----:|-----:|:----:|:---:|:---:|:----:|:----:|:----|
   |      | <span data-ttu-id="602c5-1679">+ y</span><span class="sxs-lookup"><span data-stu-id="602c5-1679">+y</span></span>   | <span data-ttu-id="602c5-1680">-y</span><span class="sxs-lookup"><span data-stu-id="602c5-1680">-y</span></span>   | <span data-ttu-id="602c5-1681">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1681">+0</span></span>  | <span data-ttu-id="602c5-1682">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1682">-0</span></span>  | <span data-ttu-id="602c5-1683">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1683">+inf</span></span> | <span data-ttu-id="602c5-1684">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1684">-inf</span></span> | <span data-ttu-id="602c5-1685">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1685">NaN</span></span> | 
   | <span data-ttu-id="602c5-1686">+ x</span><span class="sxs-lookup"><span data-stu-id="602c5-1686">+x</span></span>   | <span data-ttu-id="602c5-1687">+ z</span><span class="sxs-lookup"><span data-stu-id="602c5-1687">+z</span></span>   | <span data-ttu-id="602c5-1688">-z</span><span class="sxs-lookup"><span data-stu-id="602c5-1688">-z</span></span>   | <span data-ttu-id="602c5-1689">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1689">+0</span></span>  | <span data-ttu-id="602c5-1690">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1690">-0</span></span>  | <span data-ttu-id="602c5-1691">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1691">+inf</span></span> | <span data-ttu-id="602c5-1692">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1692">-inf</span></span> | <span data-ttu-id="602c5-1693">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1693">NaN</span></span> | 
   | <span data-ttu-id="602c5-1694">-x</span><span class="sxs-lookup"><span data-stu-id="602c5-1694">-x</span></span>   | <span data-ttu-id="602c5-1695">-z</span><span class="sxs-lookup"><span data-stu-id="602c5-1695">-z</span></span>   | <span data-ttu-id="602c5-1696">+ z</span><span class="sxs-lookup"><span data-stu-id="602c5-1696">+z</span></span>   | <span data-ttu-id="602c5-1697">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1697">-0</span></span>  | <span data-ttu-id="602c5-1698">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1698">+0</span></span>  | <span data-ttu-id="602c5-1699">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1699">-inf</span></span> | <span data-ttu-id="602c5-1700">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1700">+inf</span></span> | <span data-ttu-id="602c5-1701">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1701">NaN</span></span> | 
   | <span data-ttu-id="602c5-1702">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1702">+0</span></span>   | <span data-ttu-id="602c5-1703">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1703">+0</span></span>   | <span data-ttu-id="602c5-1704">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1704">-0</span></span>   | <span data-ttu-id="602c5-1705">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1705">+0</span></span>  | <span data-ttu-id="602c5-1706">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1706">-0</span></span>  | <span data-ttu-id="602c5-1707">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1707">NaN</span></span>  | <span data-ttu-id="602c5-1708">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1708">NaN</span></span>  | <span data-ttu-id="602c5-1709">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1709">NaN</span></span> | 
   | <span data-ttu-id="602c5-1710">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1710">-0</span></span>   | <span data-ttu-id="602c5-1711">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1711">-0</span></span>   | <span data-ttu-id="602c5-1712">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1712">+0</span></span>   | <span data-ttu-id="602c5-1713">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1713">-0</span></span>  | <span data-ttu-id="602c5-1714">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1714">+0</span></span>  | <span data-ttu-id="602c5-1715">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1715">NaN</span></span>  | <span data-ttu-id="602c5-1716">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1716">NaN</span></span>  | <span data-ttu-id="602c5-1717">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1717">NaN</span></span> | 
   | <span data-ttu-id="602c5-1718">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1718">+inf</span></span> | <span data-ttu-id="602c5-1719">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1719">+inf</span></span> | <span data-ttu-id="602c5-1720">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1720">-inf</span></span> | <span data-ttu-id="602c5-1721">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1721">NaN</span></span> | <span data-ttu-id="602c5-1722">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1722">NaN</span></span> | <span data-ttu-id="602c5-1723">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1723">+inf</span></span> | <span data-ttu-id="602c5-1724">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1724">-inf</span></span> | <span data-ttu-id="602c5-1725">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1725">NaN</span></span> | 
   | <span data-ttu-id="602c5-1726">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1726">-inf</span></span> | <span data-ttu-id="602c5-1727">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1727">-inf</span></span> | <span data-ttu-id="602c5-1728">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1728">+inf</span></span> | <span data-ttu-id="602c5-1729">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1729">NaN</span></span> | <span data-ttu-id="602c5-1730">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1730">NaN</span></span> | <span data-ttu-id="602c5-1731">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1731">-inf</span></span> | <span data-ttu-id="602c5-1732">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1732">+inf</span></span> | <span data-ttu-id="602c5-1733">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1733">NaN</span></span> | 
   | <span data-ttu-id="602c5-1734">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1734">NaN</span></span>  | <span data-ttu-id="602c5-1735">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1735">NaN</span></span>  | <span data-ttu-id="602c5-1736">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1736">NaN</span></span>  | <span data-ttu-id="602c5-1737">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1737">NaN</span></span> | <span data-ttu-id="602c5-1738">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1738">NaN</span></span> | <span data-ttu-id="602c5-1739">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1739">NaN</span></span>  | <span data-ttu-id="602c5-1740">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1740">NaN</span></span>  | <span data-ttu-id="602c5-1741">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1741">NaN</span></span> | 

*  <span data-ttu-id="602c5-1742">10 진수 곱하기.</span><span class="sxs-lookup"><span data-stu-id="602c5-1742">Decimal multiplication:</span></span>

   ```csharp
   decimal operator *(decimal x, decimal y);
   ```

   <span data-ttu-id="602c5-1743">결과 값이 너무 커서에 나타낼 수 없는 경우는 `decimal` 형식으로는 `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1743">If the resulting value is too large to represent in the `decimal` format, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="602c5-1744">결과 값이 너무 작아서 나타낼 수 없는 경우는 `decimal` 형식으로 결과 0입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1744">If the result value is too small to represent in the `decimal` format, the result is zero.</span></span> <span data-ttu-id="602c5-1745">모든 반올림 하기 전에 결과의 배율은 두 피연산자의 눈금의 합계입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1745">The scale of the result, before any rounding, is the sum of the scales of the two operands.</span></span>

   <span data-ttu-id="602c5-1746">곱하기 10 진수 형식의 곱하기 연산자를 사용 하 여 동일 `System.Decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1746">Decimal multiplication is equivalent to using the multiplication operator of type `System.Decimal`.</span></span>


### <a name="division-operator"></a><span data-ttu-id="602c5-1747">나누기 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1747">Division operator</span></span>

<span data-ttu-id="602c5-1748">폼의 작업에 대 한 `x / y`, 이항 연산자 오버 로드 확인 ([이항 연산자 오버 로드 확인](expressions.md#binary-operator-overload-resolution)) 특정 연산자 구현을 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1748">For an operation of the form `x / y`, binary operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="602c5-1749">피연산자는 선택한 연산자의 매개 변수 형식으로 변환 됩니다 하 고 결과의 형식은 연산자의 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1749">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="602c5-1750">미리 정의 된 나누기 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1750">The predefined division operators are listed below.</span></span> <span data-ttu-id="602c5-1751">모든 연산자의 몫을 계산 `x` 고 `y`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1751">The operators all compute the quotient of `x` and `y`.</span></span>

*  <span data-ttu-id="602c5-1752">정수 나누기의 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-1752">Integer division:</span></span>

   ```csharp
   int operator /(int x, int y);
   uint operator /(uint x, uint y);
   long operator /(long x, long y);
   ulong operator /(ulong x, ulong y);
   ```

   <span data-ttu-id="602c5-1753">오른쪽 피연산자의 값이 0 인 경우는 `System.DivideByZeroException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1753">If the value of the right operand is zero, a `System.DivideByZeroException` is thrown.</span></span>

   <span data-ttu-id="602c5-1754">나누기 0으로 반올림 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1754">The division rounds the result towards zero.</span></span> <span data-ttu-id="602c5-1755">따라서 결과의 절대값은 두 피연산자의 몫의 절대 값 보다 작거나는 가장 큰 정수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1755">Thus the absolute value of the result is the largest possible integer that is less than or equal to the absolute value of the quotient of the two operands.</span></span> <span data-ttu-id="602c5-1756">결과 두 피연산자와 동일한 로그인이 있고 0 또는 음수 기호가 두 피연산자의 경우 0 또는 양수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1756">The result is zero or positive when the two operands have the same sign and zero or negative when the two operands have opposite signs.</span></span>

   <span data-ttu-id="602c5-1757">왼쪽된 피연산자가 가장 작은 표현할 수 있는 경우 `int` 나 `long` 값과 오른쪽 피연산자는 `-1`, 오버플로가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1757">If the left operand is the smallest representable `int` or `long` value and the right operand is `-1`, an overflow occurs.</span></span> <span data-ttu-id="602c5-1758">에 `checked` 컨텍스트, 이렇게 하면를 `System.ArithmeticException` (또는 그 하위 클래스) throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1758">In a `checked` context, this causes a `System.ArithmeticException` (or a subclass thereof) to be thrown.</span></span> <span data-ttu-id="602c5-1759">에 `unchecked` 컨텍스트에 것 여부에 대 한 구현 시 정의 `System.ArithmeticException` (또는 그 하위 클래스)이 throw 됩니다 결과 왼쪽된 피연산자의 값을 사용 하 여 오버플로 보고 되지 않은 이동 또는 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1759">In an `unchecked` context, it is implementation-defined as to whether a `System.ArithmeticException` (or a subclass thereof) is thrown or the overflow goes unreported with the resulting value being that of the left operand.</span></span>

*  <span data-ttu-id="602c5-1760">부동 소수점 나누기의 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-1760">Floating-point division:</span></span>

   ```csharp
   float operator /(float x, float y);
   double operator /(double x, double y);
   ```

   <span data-ttu-id="602c5-1761">몫 산술 IEEE 754 규칙에 따라 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1761">The quotient is computed according to the rules of IEEE 754 arithmetic.</span></span> <span data-ttu-id="602c5-1762">다음 표에서 한정 된 0이 아닌 값의 가능한 모든 조합, 0으로, 무한대 및 NaN의 결과 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1762">The following table lists the results of all possible combinations of nonzero finite values, zeros, infinities, and NaN's.</span></span> <span data-ttu-id="602c5-1763">표에 `x` 고 `y` 유한 값이 양수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1763">In the table, `x` and `y` are positive finite values.</span></span> <span data-ttu-id="602c5-1764">`z` 결과인 `x / y`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1764">`z` is the result of `x / y`.</span></span> <span data-ttu-id="602c5-1765">결과가 너무 커서 대상 유형에 적합 이면 `z` 무한대 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1765">If the result is too large for the destination type, `z` is infinity.</span></span> <span data-ttu-id="602c5-1766">결과 대상 형식에 대해 너무 작으면 `z` 은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1766">If the result is too small for the destination type, `z` is zero.</span></span>

   |      |      |      |      |      |      |      |      |
   |:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
   |      | <span data-ttu-id="602c5-1767">+ y</span><span class="sxs-lookup"><span data-stu-id="602c5-1767">+y</span></span>   | <span data-ttu-id="602c5-1768">-y</span><span class="sxs-lookup"><span data-stu-id="602c5-1768">-y</span></span>   | <span data-ttu-id="602c5-1769">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1769">+0</span></span>   | <span data-ttu-id="602c5-1770">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1770">-0</span></span>   | <span data-ttu-id="602c5-1771">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1771">+inf</span></span> | <span data-ttu-id="602c5-1772">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1772">-inf</span></span> | <span data-ttu-id="602c5-1773">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1773">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1774">+ x</span><span class="sxs-lookup"><span data-stu-id="602c5-1774">+x</span></span>   | <span data-ttu-id="602c5-1775">+ z</span><span class="sxs-lookup"><span data-stu-id="602c5-1775">+z</span></span>   | <span data-ttu-id="602c5-1776">-z</span><span class="sxs-lookup"><span data-stu-id="602c5-1776">-z</span></span>   | <span data-ttu-id="602c5-1777">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1777">+inf</span></span> | <span data-ttu-id="602c5-1778">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1778">-inf</span></span> | <span data-ttu-id="602c5-1779">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1779">+0</span></span>   | <span data-ttu-id="602c5-1780">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1780">-0</span></span>   | <span data-ttu-id="602c5-1781">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1781">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1782">-x</span><span class="sxs-lookup"><span data-stu-id="602c5-1782">-x</span></span>   | <span data-ttu-id="602c5-1783">-z</span><span class="sxs-lookup"><span data-stu-id="602c5-1783">-z</span></span>   | <span data-ttu-id="602c5-1784">+ z</span><span class="sxs-lookup"><span data-stu-id="602c5-1784">+z</span></span>   | <span data-ttu-id="602c5-1785">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1785">-inf</span></span> | <span data-ttu-id="602c5-1786">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1786">+inf</span></span> | <span data-ttu-id="602c5-1787">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1787">-0</span></span>   | <span data-ttu-id="602c5-1788">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1788">+0</span></span>   | <span data-ttu-id="602c5-1789">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1789">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1790">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1790">+0</span></span>   | <span data-ttu-id="602c5-1791">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1791">+0</span></span>   | <span data-ttu-id="602c5-1792">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1792">-0</span></span>   | <span data-ttu-id="602c5-1793">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1793">NaN</span></span>  | <span data-ttu-id="602c5-1794">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1794">NaN</span></span>  | <span data-ttu-id="602c5-1795">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1795">+0</span></span>   | <span data-ttu-id="602c5-1796">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1796">-0</span></span>   | <span data-ttu-id="602c5-1797">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1797">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1798">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1798">-0</span></span>   | <span data-ttu-id="602c5-1799">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1799">-0</span></span>   | <span data-ttu-id="602c5-1800">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1800">+0</span></span>   | <span data-ttu-id="602c5-1801">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1801">NaN</span></span>  | <span data-ttu-id="602c5-1802">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1802">NaN</span></span>  | <span data-ttu-id="602c5-1803">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1803">-0</span></span>   | <span data-ttu-id="602c5-1804">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1804">+0</span></span>   | <span data-ttu-id="602c5-1805">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1805">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1806">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1806">+inf</span></span> | <span data-ttu-id="602c5-1807">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1807">+inf</span></span> | <span data-ttu-id="602c5-1808">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1808">-inf</span></span> | <span data-ttu-id="602c5-1809">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1809">+inf</span></span> | <span data-ttu-id="602c5-1810">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1810">-inf</span></span> | <span data-ttu-id="602c5-1811">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1811">NaN</span></span>  | <span data-ttu-id="602c5-1812">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1812">NaN</span></span>  | <span data-ttu-id="602c5-1813">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1813">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1814">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1814">-inf</span></span> | <span data-ttu-id="602c5-1815">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1815">-inf</span></span> | <span data-ttu-id="602c5-1816">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1816">+inf</span></span> | <span data-ttu-id="602c5-1817">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1817">-inf</span></span> | <span data-ttu-id="602c5-1818">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1818">+inf</span></span> | <span data-ttu-id="602c5-1819">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1819">NaN</span></span>  | <span data-ttu-id="602c5-1820">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1820">NaN</span></span>  | <span data-ttu-id="602c5-1821">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1821">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1822">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1822">NaN</span></span>  | <span data-ttu-id="602c5-1823">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1823">NaN</span></span>  | <span data-ttu-id="602c5-1824">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1824">NaN</span></span>  | <span data-ttu-id="602c5-1825">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1825">NaN</span></span>  | <span data-ttu-id="602c5-1826">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1826">NaN</span></span>  | <span data-ttu-id="602c5-1827">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1827">NaN</span></span>  | <span data-ttu-id="602c5-1828">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1828">NaN</span></span>  | <span data-ttu-id="602c5-1829">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1829">NaN</span></span>  | 

*  <span data-ttu-id="602c5-1830">10 진수 나누기의 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-1830">Decimal division:</span></span>

   ```csharp
   decimal operator /(decimal x, decimal y);
   ```

   <span data-ttu-id="602c5-1831">오른쪽 피연산자의 값이 0 인 경우는 `System.DivideByZeroException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1831">If the value of the right operand is zero, a `System.DivideByZeroException` is thrown.</span></span> <span data-ttu-id="602c5-1832">결과 값이 너무 커서에 나타낼 수 없는 경우는 `decimal` 형식으로는 `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1832">If the resulting value is too large to represent in the `decimal` format, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="602c5-1833">결과 값이 너무 작아서 나타낼 수 없는 경우는 `decimal` 형식으로 결과 0입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1833">If the result value is too small to represent in the `decimal` format, the result is zero.</span></span> <span data-ttu-id="602c5-1834">결과의 소수 자릿수가 유지 하는 결과 같은 가장 작은 눈금을 표현할 수 있는 10 진수 값을 true 수학 결과 가장 가까운 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1834">The scale of the result is the smallest scale that will preserve a result equal to the nearest representable decimal value to the true mathematical result.</span></span>

   <span data-ttu-id="602c5-1835">10 진수 나누기 형식의 나누기 연산자를 사용 하 여 동일 `System.Decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1835">Decimal division is equivalent to using the division operator of type `System.Decimal`.</span></span>


### <a name="remainder-operator"></a><span data-ttu-id="602c5-1836">나머지 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1836">Remainder operator</span></span>

<span data-ttu-id="602c5-1837">폼의 작업에 대 한 `x % y`, 이항 연산자 오버 로드 확인 ([이항 연산자 오버 로드 확인](expressions.md#binary-operator-overload-resolution)) 특정 연산자 구현을 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1837">For an operation of the form `x % y`, binary operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="602c5-1838">피연산자는 선택한 연산자의 매개 변수 형식으로 변환 됩니다 하 고 결과의 형식은 연산자의 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1838">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="602c5-1839">미리 정의 된 나머지 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1839">The predefined remainder operators are listed below.</span></span> <span data-ttu-id="602c5-1840">모든 연산자 간 나누기의 나머지를 계산 `x` 고 `y`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1840">The operators all compute the remainder of the division between `x` and `y`.</span></span>

*  <span data-ttu-id="602c5-1841">정수 나머지:</span><span class="sxs-lookup"><span data-stu-id="602c5-1841">Integer remainder:</span></span>

   ```csharp
   int operator %(int x, int y);
   uint operator %(uint x, uint y);
   long operator %(long x, long y);
   ulong operator %(ulong x, ulong y);
   ```

   <span data-ttu-id="602c5-1842">결과인 `x % y` 값으로 생성 `x - (x / y) * y`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1842">The result of `x % y` is the value produced by `x - (x / y) * y`.</span></span> <span data-ttu-id="602c5-1843">하는 경우 `y` 가 0 이면는 `System.DivideByZeroException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1843">If `y` is zero, a `System.DivideByZeroException` is thrown.</span></span>

   <span data-ttu-id="602c5-1844">왼쪽된 피연산자가 가장 작은 `int` 또는 `long` 값 이며 오른쪽 피연산자 `-1`, `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1844">If the left operand is the smallest `int` or `long` value and the right operand is `-1`, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="602c5-1845">없는 경우에는 `x % y` 예외를 throw 여기서 `x / y` 은 예외를 throw 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1845">In no case does `x % y` throw an exception where `x / y` would not throw an exception.</span></span>

*  <span data-ttu-id="602c5-1846">부동 소수점 나머지:</span><span class="sxs-lookup"><span data-stu-id="602c5-1846">Floating-point remainder:</span></span>

   ```csharp
   float operator %(float x, float y);
   double operator %(double x, double y);
   ```

   <span data-ttu-id="602c5-1847">다음 표에서 한정 된 0이 아닌 값의 가능한 모든 조합, 0으로, 무한대 및 NaN의 결과 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1847">The following table lists the results of all possible combinations of nonzero finite values, zeros, infinities, and NaN's.</span></span> <span data-ttu-id="602c5-1848">표에 `x` 고 `y` 유한 값이 양수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1848">In the table, `x` and `y` are positive finite values.</span></span> <span data-ttu-id="602c5-1849">`z` 결과인 `x % y` 로 계산 됩니다 `x - n * y`, 여기서 `n` 보다 작거나 같은 가장 큰 정수는 `x / y`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1849">`z` is the result of `x % y` and is computed as `x - n * y`, where `n` is the largest possible integer that is less than or equal to `x / y`.</span></span> <span data-ttu-id="602c5-1850">나머지 컴퓨팅이 메서드는 정수 피연산자에 사용 되는 것과 유사 하지만 IEEE 754 정의에서 다릅니다 (나타나는 `n` 정수를 가장 가까운 `x / y`).</span><span class="sxs-lookup"><span data-stu-id="602c5-1850">This method of computing the remainder is analogous to that used for integer operands, but differs from the IEEE 754 definition (in which `n` is the integer closest to `x / y`).</span></span>

   |      |      |      |      |      |      |      |      |
   |:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
   |      | <span data-ttu-id="602c5-1851">+ y</span><span class="sxs-lookup"><span data-stu-id="602c5-1851">+y</span></span>   | <span data-ttu-id="602c5-1852">-y</span><span class="sxs-lookup"><span data-stu-id="602c5-1852">-y</span></span>   | <span data-ttu-id="602c5-1853">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1853">+0</span></span>   | <span data-ttu-id="602c5-1854">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1854">-0</span></span>   | <span data-ttu-id="602c5-1855">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1855">+inf</span></span> | <span data-ttu-id="602c5-1856">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1856">-inf</span></span> | <span data-ttu-id="602c5-1857">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1857">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1858">+ x</span><span class="sxs-lookup"><span data-stu-id="602c5-1858">+x</span></span>   | <span data-ttu-id="602c5-1859">+ z</span><span class="sxs-lookup"><span data-stu-id="602c5-1859">+z</span></span>   | <span data-ttu-id="602c5-1860">+ z</span><span class="sxs-lookup"><span data-stu-id="602c5-1860">+z</span></span>   | <span data-ttu-id="602c5-1861">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1861">NaN</span></span>  | <span data-ttu-id="602c5-1862">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1862">NaN</span></span>  | <span data-ttu-id="602c5-1863">x</span><span class="sxs-lookup"><span data-stu-id="602c5-1863">x</span></span>    | <span data-ttu-id="602c5-1864">x</span><span class="sxs-lookup"><span data-stu-id="602c5-1864">x</span></span>    | <span data-ttu-id="602c5-1865">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1865">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1866">-x</span><span class="sxs-lookup"><span data-stu-id="602c5-1866">-x</span></span>   | <span data-ttu-id="602c5-1867">-z</span><span class="sxs-lookup"><span data-stu-id="602c5-1867">-z</span></span>   | <span data-ttu-id="602c5-1868">-z</span><span class="sxs-lookup"><span data-stu-id="602c5-1868">-z</span></span>   | <span data-ttu-id="602c5-1869">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1869">NaN</span></span>  | <span data-ttu-id="602c5-1870">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1870">NaN</span></span>  | <span data-ttu-id="602c5-1871">-x</span><span class="sxs-lookup"><span data-stu-id="602c5-1871">-x</span></span>   | <span data-ttu-id="602c5-1872">-x</span><span class="sxs-lookup"><span data-stu-id="602c5-1872">-x</span></span>   | <span data-ttu-id="602c5-1873">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1873">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1874">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1874">+0</span></span>   | <span data-ttu-id="602c5-1875">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1875">+0</span></span>   | <span data-ttu-id="602c5-1876">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1876">+0</span></span>   | <span data-ttu-id="602c5-1877">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1877">NaN</span></span>  | <span data-ttu-id="602c5-1878">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1878">NaN</span></span>  | <span data-ttu-id="602c5-1879">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1879">+0</span></span>   | <span data-ttu-id="602c5-1880">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1880">+0</span></span>   | <span data-ttu-id="602c5-1881">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1881">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1882">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1882">-0</span></span>   | <span data-ttu-id="602c5-1883">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1883">-0</span></span>   | <span data-ttu-id="602c5-1884">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1884">-0</span></span>   | <span data-ttu-id="602c5-1885">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1885">NaN</span></span>  | <span data-ttu-id="602c5-1886">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1886">NaN</span></span>  | <span data-ttu-id="602c5-1887">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1887">-0</span></span>   | <span data-ttu-id="602c5-1888">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1888">-0</span></span>   | <span data-ttu-id="602c5-1889">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1889">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1890">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1890">+inf</span></span> | <span data-ttu-id="602c5-1891">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1891">NaN</span></span>  | <span data-ttu-id="602c5-1892">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1892">NaN</span></span>  | <span data-ttu-id="602c5-1893">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1893">NaN</span></span>  | <span data-ttu-id="602c5-1894">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1894">NaN</span></span>  | <span data-ttu-id="602c5-1895">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1895">NaN</span></span>  | <span data-ttu-id="602c5-1896">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1896">NaN</span></span>  | <span data-ttu-id="602c5-1897">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1897">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1898">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1898">-inf</span></span> | <span data-ttu-id="602c5-1899">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1899">NaN</span></span>  | <span data-ttu-id="602c5-1900">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1900">NaN</span></span>  | <span data-ttu-id="602c5-1901">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1901">NaN</span></span>  | <span data-ttu-id="602c5-1902">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1902">NaN</span></span>  | <span data-ttu-id="602c5-1903">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1903">NaN</span></span>  | <span data-ttu-id="602c5-1904">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1904">NaN</span></span>  | <span data-ttu-id="602c5-1905">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1905">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1906">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1906">NaN</span></span>  | <span data-ttu-id="602c5-1907">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1907">NaN</span></span>  | <span data-ttu-id="602c5-1908">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1908">NaN</span></span>  | <span data-ttu-id="602c5-1909">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1909">NaN</span></span>  | <span data-ttu-id="602c5-1910">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1910">NaN</span></span>  | <span data-ttu-id="602c5-1911">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1911">NaN</span></span>  | <span data-ttu-id="602c5-1912">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1912">NaN</span></span>  | <span data-ttu-id="602c5-1913">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1913">NaN</span></span>  | 

*  <span data-ttu-id="602c5-1914">10 진수 나머지:</span><span class="sxs-lookup"><span data-stu-id="602c5-1914">Decimal remainder:</span></span>

   ```csharp
   decimal operator %(decimal x, decimal y);
   ```

   <span data-ttu-id="602c5-1915">오른쪽 피연산자의 값이 0 인 경우는 `System.DivideByZeroException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1915">If the value of the right operand is zero, a `System.DivideByZeroException` is thrown.</span></span> <span data-ttu-id="602c5-1916">모든 반올림 하기 전에 결과의 소수 자릿수가 두 피연산자 중 확장 중 더 큰 이며 결과의 기호를 0이 아닌 경우와 동일한 `x`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1916">The scale of the result, before any rounding, is the larger of the scales of the two operands, and the sign of the result, if non-zero, is the same as that of `x`.</span></span>

   <span data-ttu-id="602c5-1917">나머지 10 진수 형식의 나머지 연산자를 사용 하 여 동일 `System.Decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1917">Decimal remainder is equivalent to using the remainder operator of type `System.Decimal`.</span></span>


### <a name="addition-operator"></a><span data-ttu-id="602c5-1918">더하기 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-1918">Addition operator</span></span>

<span data-ttu-id="602c5-1919">폼의 작업에 대 한 `x + y`, 이항 연산자 오버 로드 확인 ([이항 연산자 오버 로드 확인](expressions.md#binary-operator-overload-resolution)) 특정 연산자 구현을 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1919">For an operation of the form `x + y`, binary operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="602c5-1920">피연산자는 선택한 연산자의 매개 변수 형식으로 변환 됩니다 하 고 결과의 형식은 연산자의 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1920">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="602c5-1921">미리 정의 된 더하기 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1921">The predefined addition operators are listed below.</span></span> <span data-ttu-id="602c5-1922">숫자 및 열거형 형식에 대 한 미리 정의 된 더하기 연산자는 두 피연산자의 합계를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1922">For numeric and enumeration types, the predefined addition operators compute the sum of the two operands.</span></span> <span data-ttu-id="602c5-1923">피연산자 하나 또는 둘 다 문자열 형식의 경우 미리 정의 된 더하기 연산자는 피연산자의 문자열 표현을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1923">When one or both operands are of type string, the predefined addition operators concatenate the string representation of the operands.</span></span>

*  <span data-ttu-id="602c5-1924">정수 추가:</span><span class="sxs-lookup"><span data-stu-id="602c5-1924">Integer addition:</span></span>

   ```csharp
   int operator +(int x, int y);
   uint operator +(uint x, uint y);
   long operator +(long x, long y);
   ulong operator +(ulong x, ulong y);
   ```

   <span data-ttu-id="602c5-1925">에 `checked` 합계 결과 형식 범위를 벗어난 경우 컨텍스트는 `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1925">In a `checked` context, if the sum is outside the range of the result type, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="602c5-1926">에 `unchecked` 컨텍스트에 오버플로 보고 되지 않으며 결과 형식 범위 밖에 있는 경우 중요 한 모든 상위 비트는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1926">In an `unchecked` context, overflows are not reported and any significant high-order bits outside the range of the result type are discarded.</span></span>

*  <span data-ttu-id="602c5-1927">부동 소수점 더하기의 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-1927">Floating-point addition:</span></span>

   ```csharp
   float operator +(float x, float y);
   double operator +(double x, double y);
   ```

   <span data-ttu-id="602c5-1928">합계는 산술 IEEE 754 규칙에 따라 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1928">The sum is computed according to the rules of IEEE 754 arithmetic.</span></span> <span data-ttu-id="602c5-1929">다음 표에서 한정 된 0이 아닌 값의 가능한 모든 조합, 0으로, 무한대 및 NaN의 결과 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1929">The following table lists the results of all possible combinations of nonzero finite values, zeros, infinities, and NaN's.</span></span> <span data-ttu-id="602c5-1930">표에 `x` 및 `y` 유한 값이 0이 아닌, 및 `z` 결과인 `x + y`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1930">In the table, `x` and `y` are nonzero finite values, and `z` is the result of `x + y`.</span></span> <span data-ttu-id="602c5-1931">경우 `x` 하 고 `y` 동일한 크기가 있는 하지만 부호가 반대 `z` 양의 0.</span><span class="sxs-lookup"><span data-stu-id="602c5-1931">If `x` and `y` have the same magnitude but opposite signs, `z` is positive zero.</span></span> <span data-ttu-id="602c5-1932">하는 경우 `x + y` 너무 커서 대상 형식에 나타낼 `z` 같은 부호를 사용 하 여 무한대 인지 `x + y`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1932">If `x + y` is too large to represent in the destination type, `z` is an infinity with the same sign as `x + y`.</span></span>

   |      |      |      |      |      |      |      |
   |:----:|:----:|:----:|:----:|:----:|:----:|:----:|
   |      | <span data-ttu-id="602c5-1933">y</span><span class="sxs-lookup"><span data-stu-id="602c5-1933">y</span></span>    | <span data-ttu-id="602c5-1934">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1934">+0</span></span>   | <span data-ttu-id="602c5-1935">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1935">-0</span></span>   | <span data-ttu-id="602c5-1936">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1936">+inf</span></span> | <span data-ttu-id="602c5-1937">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1937">-inf</span></span> | <span data-ttu-id="602c5-1938">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1938">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1939">x</span><span class="sxs-lookup"><span data-stu-id="602c5-1939">x</span></span>    | <span data-ttu-id="602c5-1940">z</span><span class="sxs-lookup"><span data-stu-id="602c5-1940">z</span></span>    | <span data-ttu-id="602c5-1941">x</span><span class="sxs-lookup"><span data-stu-id="602c5-1941">x</span></span>    | <span data-ttu-id="602c5-1942">x</span><span class="sxs-lookup"><span data-stu-id="602c5-1942">x</span></span>    | <span data-ttu-id="602c5-1943">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1943">+inf</span></span> | <span data-ttu-id="602c5-1944">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1944">-inf</span></span> | <span data-ttu-id="602c5-1945">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1945">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1946">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1946">+0</span></span>   | <span data-ttu-id="602c5-1947">y</span><span class="sxs-lookup"><span data-stu-id="602c5-1947">y</span></span>    | <span data-ttu-id="602c5-1948">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1948">+0</span></span>   | <span data-ttu-id="602c5-1949">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1949">+0</span></span>   | <span data-ttu-id="602c5-1950">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1950">+inf</span></span> | <span data-ttu-id="602c5-1951">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1951">-inf</span></span> | <span data-ttu-id="602c5-1952">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1952">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1953">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1953">-0</span></span>   | <span data-ttu-id="602c5-1954">y</span><span class="sxs-lookup"><span data-stu-id="602c5-1954">y</span></span>    | <span data-ttu-id="602c5-1955">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-1955">+0</span></span>   | <span data-ttu-id="602c5-1956">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-1956">-0</span></span>   | <span data-ttu-id="602c5-1957">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1957">+inf</span></span> | <span data-ttu-id="602c5-1958">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1958">-inf</span></span> | <span data-ttu-id="602c5-1959">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1959">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1960">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1960">+inf</span></span> | <span data-ttu-id="602c5-1961">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1961">+inf</span></span> | <span data-ttu-id="602c5-1962">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1962">+inf</span></span> | <span data-ttu-id="602c5-1963">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1963">+inf</span></span> | <span data-ttu-id="602c5-1964">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1964">+inf</span></span> | <span data-ttu-id="602c5-1965">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1965">NaN</span></span>  | <span data-ttu-id="602c5-1966">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1966">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1967">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1967">-inf</span></span> | <span data-ttu-id="602c5-1968">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1968">-inf</span></span> | <span data-ttu-id="602c5-1969">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1969">-inf</span></span> | <span data-ttu-id="602c5-1970">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1970">-inf</span></span> | <span data-ttu-id="602c5-1971">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1971">NaN</span></span>  | <span data-ttu-id="602c5-1972">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-1972">-inf</span></span> | <span data-ttu-id="602c5-1973">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1973">NaN</span></span>  | 
   | <span data-ttu-id="602c5-1974">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1974">NaN</span></span>  | <span data-ttu-id="602c5-1975">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1975">NaN</span></span>  | <span data-ttu-id="602c5-1976">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1976">NaN</span></span>  | <span data-ttu-id="602c5-1977">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1977">NaN</span></span>  | <span data-ttu-id="602c5-1978">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1978">NaN</span></span>  | <span data-ttu-id="602c5-1979">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1979">NaN</span></span>  | <span data-ttu-id="602c5-1980">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-1980">NaN</span></span>  | 

*  <span data-ttu-id="602c5-1981">10 진수 추가:</span><span class="sxs-lookup"><span data-stu-id="602c5-1981">Decimal addition:</span></span>

   ```csharp
   decimal operator +(decimal x, decimal y);
   ```

   <span data-ttu-id="602c5-1982">결과 값이 너무 커서에 나타낼 수 없는 경우는 `decimal` 형식으로는 `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1982">If the resulting value is too large to represent in the `decimal` format, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="602c5-1983">모든 반올림 하기 전에 결과의 소수 자릿수가 두 피연산자의 확장 중 큰 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1983">The scale of the result, before any rounding, is the larger of the scales of the two operands.</span></span>

   <span data-ttu-id="602c5-1984">10 진수 추가 사용 하는 형식의 더하기 연산자 `System.Decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1984">Decimal addition is equivalent to using the addition operator of type `System.Decimal`.</span></span>

*  <span data-ttu-id="602c5-1985">열거형을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1985">Enumeration addition.</span></span> <span data-ttu-id="602c5-1986">모든 열거형 형식은 다음 미리 정의 된 연산자를 암시적으로 제공 위치 `E` 은 열거형 형식 및 `U` 의 기본 형식인 `E`:</span><span class="sxs-lookup"><span data-stu-id="602c5-1986">Every enumeration type implicitly provides the following predefined operators, where `E` is the enum type, and `U` is the underlying type of `E`:</span></span>

   ```csharp
   E operator +(E x, U y);
   E operator +(U x, E y);
   ```

   <span data-ttu-id="602c5-1987">런타임 시 이러한 연산자와 동일 하 게 계산 됩니다 `(E)((U)x + (U)y)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1987">At run-time these operators are evaluated exactly as `(E)((U)x + (U)y)`.</span></span>

*  <span data-ttu-id="602c5-1988">문자열 연결:</span><span class="sxs-lookup"><span data-stu-id="602c5-1988">String concatenation:</span></span>

   ```csharp
   string operator +(string x, string y);
   string operator +(string x, object y);
   string operator +(object x, string y);
   ```

   <span data-ttu-id="602c5-1989">이러한 오버 로드 된 이진 파일의 `+` 연산자 문자열 연결을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1989">These overloads of the binary `+` operator perform string concatenation.</span></span> <span data-ttu-id="602c5-1990">피연산자 문자열 연결의 경우 `null`, 빈 문자열은 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1990">If an operand of string concatenation is `null`, an empty string is substituted.</span></span> <span data-ttu-id="602c5-1991">가상 호출 하 여 해당 문자열 표현으로 문자열이 아닌 인수가 변환 되는 고, 그렇지 `ToString` 형식에서 상속 된 메서드 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1991">Otherwise, any non-string argument is converted to its string representation by invoking the virtual `ToString` method inherited from type `object`.</span></span> <span data-ttu-id="602c5-1992">하는 경우 `ToString` 반환 `null`, 빈 문자열은 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1992">If `ToString` returns `null`, an empty string is substituted.</span></span>

   ```csharp
   using System;
   
   class Test
   {
       static void Main() {
           string s = null;
           Console.WriteLine("s = >" + s + "<");        // displays s = ><
           int i = 1;
           Console.WriteLine("i = " + i);               // displays i = 1
           float f = 1.2300E+15F;
           Console.WriteLine("f = " + f);               // displays f = 1.23E+15
           decimal d = 2.900m;
           Console.WriteLine("d = " + d);               // displays d = 2.900
       }
   }
   ```

   문자열 연결 연산자의 결과 오른쪽 피연산자의 문자 뒤에 왼쪽된 피연산자의 문자로 구성 된 문자열입니다. 문자열 연결 연산자는 반환 하지 않습니다는 `null` 값입니다. <span data-ttu-id="602c5-1995">`System.OutOfMemoryException` 결과 문자열에 할당할 수 있는 충분 한 메모리가 없을 경우에 throw 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1995">A `System.OutOfMemoryException` may be thrown if there is not enough memory available to allocate the resulting string.</span></span>

*  <span data-ttu-id="602c5-1996">대리자 결합 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1996">Delegate combination.</span></span> <span data-ttu-id="602c5-1997">다음 미리 정의 된 연산자를 암시적으로 제공 하는 모든 대리자 형식 여기서 `D` 대리자 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1997">Every delegate type implicitly provides the following predefined operator, where `D` is the delegate type:</span></span>

   ```csharp
   D operator +(D x, D y);
   ```

   <span data-ttu-id="602c5-1998">이진 `+` 연산자는 피연산자가 모두 대리자 일종의 경우 대리자 결합을 수행 `D`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-1998">The binary `+` operator performs delegate combination when both operands are of some delegate type `D`.</span></span> <span data-ttu-id="602c5-1999">(피연산자가 서로 다른 대리자 형식에 있으면 바인딩 시간 오류를 발생 합니다.) 첫 번째 피연산자가 `null`, 작업의 결과 두 번째 피연산자의 값 (이기도 하는 경우에 `null`).</span><span class="sxs-lookup"><span data-stu-id="602c5-1999">(If the operands have different delegate types, a binding-time error occurs.) If the first operand is `null`, the result of the operation is the value of the second operand (even if that is also `null`).</span></span> <span data-ttu-id="602c5-2000">그렇지 않으면 두 번째 피연산자가 `null`, 작업의 결과 첫 번째 피연산자의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2000">Otherwise, if the second operand is `null`, then the result of the operation is the value of the first operand.</span></span> <span data-ttu-id="602c5-2001">이 고, 그렇지 연산의 결과 새 대리자 인스턴스가 호출, 첫 번째 피연산자를 호출 하 고, 다음 두 번째 피연산자를 호출 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="602c5-2001">Otherwise, the result of the operation is a new delegate instance that, when invoked, invokes the first operand and then invokes the second operand.</span></span> <span data-ttu-id="602c5-2002">대리자 결합의 예제를 참조 하세요 [빼기 연산자](expressions.md#subtraction-operator) 하 고 [대리자 호출](delegates.md#delegate-invocation)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2002">For examples of delegate combination, see [Subtraction operator](expressions.md#subtraction-operator) and [Delegate invocation](delegates.md#delegate-invocation).</span></span> <span data-ttu-id="602c5-2003">이후 `System.Delegate` 대리자 형식이 아닙니다 `operator` `+` 에 대 한 정의 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2003">Since `System.Delegate` is not a delegate type, `operator` `+` is not defined for it.</span></span>

### <a name="subtraction-operator"></a><span data-ttu-id="602c5-2004">빼기 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2004">Subtraction operator</span></span>

<span data-ttu-id="602c5-2005">폼의 작업에 대 한 `x - y`, 이항 연산자 오버 로드 확인 ([이항 연산자 오버 로드 확인](expressions.md#binary-operator-overload-resolution)) 특정 연산자 구현을 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2005">For an operation of the form `x - y`, binary operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="602c5-2006">피연산자는 선택한 연산자의 매개 변수 형식으로 변환 됩니다 하 고 결과의 형식은 연산자의 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2006">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="602c5-2007">미리 정의 된 빼기 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2007">The predefined subtraction operators are listed below.</span></span> <span data-ttu-id="602c5-2008">모든 빼기 연산자 `y` 에서 `x`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2008">The operators all subtract `y` from `x`.</span></span>

*  <span data-ttu-id="602c5-2009">정수 빼기</span><span class="sxs-lookup"><span data-stu-id="602c5-2009">Integer subtraction:</span></span>

   ```csharp
   int operator -(int x, int y);
   uint operator -(uint x, uint y);
   long operator -(long x, long y);
   ulong operator -(ulong x, ulong y);
   ```

   <span data-ttu-id="602c5-2010">에 `checked` 차이 결과 형식 범위를 벗어난 경우 컨텍스트는 `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2010">In a `checked` context, if the difference is outside the range of the result type, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="602c5-2011">에 `unchecked` 컨텍스트에 오버플로 보고 되지 않으며 결과 형식 범위 밖에 있는 경우 중요 한 모든 상위 비트는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2011">In an `unchecked` context, overflows are not reported and any significant high-order bits outside the range of the result type are discarded.</span></span>

*  <span data-ttu-id="602c5-2012">부동 소수점 빼기</span><span class="sxs-lookup"><span data-stu-id="602c5-2012">Floating-point subtraction:</span></span>

   ```csharp
   float operator -(float x, float y);
   double operator -(double x, double y);
   ```

   <span data-ttu-id="602c5-2013">차이점은 산술 IEEE 754 규칙에 따라 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2013">The difference is computed according to the rules of IEEE 754 arithmetic.</span></span> <span data-ttu-id="602c5-2014">다음 표에서 한정 된 0이 아닌 값의 가능한 모든 조합, 0으로, 무한대 및 Nan 결과 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2014">The following table lists the results of all possible combinations of nonzero finite values, zeros, infinities, and NaNs.</span></span> <span data-ttu-id="602c5-2015">표에 `x` 및 `y` 유한 값이 0이 아닌, 및 `z` 결과인 `x - y`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2015">In the table, `x` and `y` are nonzero finite values, and `z` is the result of `x - y`.</span></span> <span data-ttu-id="602c5-2016">하는 경우 `x` 하 고 `y` 같지 `z` 양의 0입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2016">If `x` and `y` are equal, `z` is positive zero.</span></span> <span data-ttu-id="602c5-2017">하는 경우 `x - y` 너무 커서 대상 형식에 나타낼 `z` 같은 부호를 사용 하 여 무한대 인지 `x - y`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2017">If `x - y` is too large to represent in the destination type, `z` is an infinity with the same sign as `x - y`.</span></span>

   |      |      |      |      |      |      |     |
   |:----:|:----:|:----:|:----:|:----:|:----:|:---:|
   | <span data-ttu-id="602c5-2018">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2018">NaN</span></span>  | <span data-ttu-id="602c5-2019">y</span><span class="sxs-lookup"><span data-stu-id="602c5-2019">y</span></span>    | <span data-ttu-id="602c5-2020">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-2020">+0</span></span>   | <span data-ttu-id="602c5-2021">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-2021">-0</span></span>   | <span data-ttu-id="602c5-2022">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2022">+inf</span></span> | <span data-ttu-id="602c5-2023">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2023">-inf</span></span> | <span data-ttu-id="602c5-2024">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2024">NaN</span></span> | 
   | <span data-ttu-id="602c5-2025">x</span><span class="sxs-lookup"><span data-stu-id="602c5-2025">x</span></span>    | <span data-ttu-id="602c5-2026">z</span><span class="sxs-lookup"><span data-stu-id="602c5-2026">z</span></span>    | <span data-ttu-id="602c5-2027">x</span><span class="sxs-lookup"><span data-stu-id="602c5-2027">x</span></span>    | <span data-ttu-id="602c5-2028">x</span><span class="sxs-lookup"><span data-stu-id="602c5-2028">x</span></span>    | <span data-ttu-id="602c5-2029">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2029">-inf</span></span> | <span data-ttu-id="602c5-2030">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2030">+inf</span></span> | <span data-ttu-id="602c5-2031">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2031">NaN</span></span> | 
   | <span data-ttu-id="602c5-2032">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-2032">+0</span></span>   | <span data-ttu-id="602c5-2033">-y</span><span class="sxs-lookup"><span data-stu-id="602c5-2033">-y</span></span>   | <span data-ttu-id="602c5-2034">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-2034">+0</span></span>   | <span data-ttu-id="602c5-2035">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-2035">+0</span></span>   | <span data-ttu-id="602c5-2036">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2036">-inf</span></span> | <span data-ttu-id="602c5-2037">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2037">+inf</span></span> | <span data-ttu-id="602c5-2038">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2038">NaN</span></span> | 
   | <span data-ttu-id="602c5-2039">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-2039">-0</span></span>   | <span data-ttu-id="602c5-2040">-y</span><span class="sxs-lookup"><span data-stu-id="602c5-2040">-y</span></span>   | <span data-ttu-id="602c5-2041">-0</span><span class="sxs-lookup"><span data-stu-id="602c5-2041">-0</span></span>   | <span data-ttu-id="602c5-2042">+0</span><span class="sxs-lookup"><span data-stu-id="602c5-2042">+0</span></span>   | <span data-ttu-id="602c5-2043">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2043">-inf</span></span> | <span data-ttu-id="602c5-2044">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2044">+inf</span></span> | <span data-ttu-id="602c5-2045">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2045">NaN</span></span> | 
   | <span data-ttu-id="602c5-2046">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2046">+inf</span></span> | <span data-ttu-id="602c5-2047">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2047">+inf</span></span> | <span data-ttu-id="602c5-2048">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2048">+inf</span></span> | <span data-ttu-id="602c5-2049">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2049">+inf</span></span> | <span data-ttu-id="602c5-2050">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2050">NaN</span></span>  | <span data-ttu-id="602c5-2051">+inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2051">+inf</span></span> | <span data-ttu-id="602c5-2052">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2052">NaN</span></span> | 
   | <span data-ttu-id="602c5-2053">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2053">-inf</span></span> | <span data-ttu-id="602c5-2054">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2054">-inf</span></span> | <span data-ttu-id="602c5-2055">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2055">-inf</span></span> | <span data-ttu-id="602c5-2056">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2056">-inf</span></span> | <span data-ttu-id="602c5-2057">-inf</span><span class="sxs-lookup"><span data-stu-id="602c5-2057">-inf</span></span> | <span data-ttu-id="602c5-2058">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2058">NaN</span></span>  | <span data-ttu-id="602c5-2059">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2059">NaN</span></span> | 
   | <span data-ttu-id="602c5-2060">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2060">NaN</span></span>  | <span data-ttu-id="602c5-2061">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2061">NaN</span></span>  | <span data-ttu-id="602c5-2062">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2062">NaN</span></span>  | <span data-ttu-id="602c5-2063">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2063">NaN</span></span>  | <span data-ttu-id="602c5-2064">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2064">NaN</span></span>  | <span data-ttu-id="602c5-2065">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2065">NaN</span></span>  | <span data-ttu-id="602c5-2066">NaN</span><span class="sxs-lookup"><span data-stu-id="602c5-2066">NaN</span></span> | 

*  <span data-ttu-id="602c5-2067">10 진수 빼기의 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-2067">Decimal subtraction:</span></span>

   ```csharp
   decimal operator -(decimal x, decimal y);
   ```

   <span data-ttu-id="602c5-2068">결과 값이 너무 커서에 나타낼 수 없는 경우는 `decimal` 형식으로는 `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2068">If the resulting value is too large to represent in the `decimal` format, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="602c5-2069">모든 반올림 하기 전에 결과의 소수 자릿수가 두 피연산자의 확장 중 큰 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2069">The scale of the result, before any rounding, is the larger of the scales of the two operands.</span></span>

   <span data-ttu-id="602c5-2070">10 진수 빼기 형식의 빼기 연산자를 사용 하 여 동일 `System.Decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2070">Decimal subtraction is equivalent to using the subtraction operator of type `System.Decimal`.</span></span>

*  <span data-ttu-id="602c5-2071">열거형 빼기입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2071">Enumeration subtraction.</span></span> <span data-ttu-id="602c5-2072">모든 열거형은 다음과 같은 미리 정의 된 연산자를 암시적으로 제공 위치 `E` 은 열거형 형식 및 `U` 의 기본 형식인 `E`:</span><span class="sxs-lookup"><span data-stu-id="602c5-2072">Every enumeration type implicitly provides the following predefined operator, where `E` is the enum type, and `U` is the underlying type of `E`:</span></span>

   ```csharp
   U operator -(E x, E y);
   ```

   <span data-ttu-id="602c5-2073">이 연산자는 대로 정확 하 게 계산 됩니다 `(U)((U)x - (U)y)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2073">This operator is evaluated exactly as `(U)((U)x - (U)y)`.</span></span> <span data-ttu-id="602c5-2074">연산자의 서 수 값 간의 차이 계산 하는, 즉 `x` 및 `y`, 고 결과의 형식 열거형의 기본 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2074">In other words, the operator computes the difference between the ordinal values of `x` and `y`, and the type of the result is the underlying type of the enumeration.</span></span>

   ```csharp
   E operator -(E x, U y);
   ```

   <span data-ttu-id="602c5-2075">이 연산자는 대로 정확 하 게 계산 됩니다 `(E)((U)x - y)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2075">This operator is evaluated exactly as `(E)((U)x - y)`.</span></span> <span data-ttu-id="602c5-2076">즉, 연산자는 열거형의 값이 구해지 기 열거형의 내부 형식에서 값을 뺍니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2076">In other words, the operator subtracts a value from the underlying type of the enumeration, yielding a value of the enumeration.</span></span>

*  <span data-ttu-id="602c5-2077">제거를 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2077">Delegate removal.</span></span> <span data-ttu-id="602c5-2078">다음 미리 정의 된 연산자를 암시적으로 제공 하는 모든 대리자 형식 여기서 `D` 대리자 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2078">Every delegate type implicitly provides the following predefined operator, where `D` is the delegate type:</span></span>

   ```csharp
   D operator -(D x, D y);
   ```

   <span data-ttu-id="602c5-2079">이진 `-` 연산자는 피연산자가 모두 대리자 일종의 경우 대리자 제거를 수행 `D`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2079">The binary `-` operator performs delegate removal when both operands are of some delegate type `D`.</span></span> <span data-ttu-id="602c5-2080">피연산자가 서로 다른 대리자 형식 바인딩 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2080">If the operands have different delegate types, a binding-time error occurs.</span></span> <span data-ttu-id="602c5-2081">첫 번째 피연산자가 `null`, 작업의 결과 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2081">If the first operand is `null`, the result of the operation is `null`.</span></span> <span data-ttu-id="602c5-2082">그렇지 않으면 두 번째 피연산자가 `null`, 작업의 결과 첫 번째 피연산자의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2082">Otherwise, if the second operand is `null`, then the result of the operation is the value of the first operand.</span></span> <span data-ttu-id="602c5-2083">두 피연산자의 호출 목록을 나타내는 고, 그렇지 ([대리자 선언](delegates.md#delegate-declarations)) 하나 이상의 항목을 선택한 결과 것이 첫 번째 피연산자의 목록에서 제거 하는 두 번째 피연산자의 항목으로 구성 된 새 호출 목록 두 번째 피연산자의 목록을 제공 하는 첫 번째의 적절 한 연속 하위 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2083">Otherwise, both operands represent invocation lists ([Delegate declarations](delegates.md#delegate-declarations)) having one or more entries, and the result is a new invocation list consisting of the first operand's list with the second operand's entries removed from it, provided the second operand's list is a proper contiguous sublist of the first's.</span></span>     <span data-ttu-id="602c5-2084">(하위 목록 같은지를 확인 하려면 해당 항목을 대리자 같음 연산자와 비교 ([같음 연산자를 대리자](expressions.md#delegate-equality-operators)).) 그렇지 않으면 결과 왼쪽된 피연산자의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2084">(To determine sublist equality, corresponding entries are compared as for the delegate equality operator ([Delegate equality operators](expressions.md#delegate-equality-operators)).) Otherwise, the result is the value of the left operand.</span></span> <span data-ttu-id="602c5-2085">모두 피연산자 목록은 과정에서 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2085">Neither of the operands' lists is changed in the process.</span></span> <span data-ttu-id="602c5-2086">두 번째 피연산자의 목록에 여러 하위 목록의 첫 번째 피연산자의 목록에서 인접 한 항목의 일치 하는 경우 인접 한 항목의 가장 오른쪽에 일치 하는 하위 목록 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2086">If the second operand's list matches multiple sublists of contiguous entries in the first operand's list, the right-most matching sublist of contiguous entries is removed.</span></span> <span data-ttu-id="602c5-2087">결과 빈 목록에서 제거 결과 경우 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2087">If removal results in an empty list, the result is `null`.</span></span> <span data-ttu-id="602c5-2088">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="602c5-2088">For example:</span></span>

   ```csharp
   delegate void D(int x);
   
   class C
   {
       public static void M1(int i) { /* ... */ }
       public static void M2(int i) { /* ... */ }
   }

   class Test
   {
       static void Main() { 
           D cd1 = new D(C.M1);
           D cd2 = new D(C.M2);
           D cd3 = cd1 + cd2 + cd2 + cd1;   // M1 + M2 + M2 + M1
           cd3 -= cd1;                      // => M1 + M2 + M2
   
           cd3 = cd1 + cd2 + cd2 + cd1;     // M1 + M2 + M2 + M1
           cd3 -= cd1 + cd2;                // => M2 + M1
   
           cd3 = cd1 + cd2 + cd2 + cd1;     // M1 + M2 + M2 + M1
           cd3 -= cd2 + cd2;                // => M1 + M1
   
           cd3 = cd1 + cd2 + cd2 + cd1;     // M1 + M2 + M2 + M1
           cd3 -= cd2 + cd1;                // => M1 + M2
   
           cd3 = cd1 + cd2 + cd2 + cd1;     // M1 + M2 + M2 + M1
           cd3 -= cd1 + cd1;                // => M1 + M2 + M2 + M1
       }
   }
   ```

## <a name="shift-operators"></a><span data-ttu-id="602c5-2089">시프트 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2089">Shift operators</span></span>

<span data-ttu-id="602c5-2090">합니다 `<<` 고 `>>` 연산자는 비트 시프트 연산을 수행 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2090">The `<<` and `>>` operators are used to perform bit shifting operations.</span></span>

```antlr
shift_expression
    : additive_expression
    | shift_expression '<<' additive_expression
    | shift_expression right_shift additive_expression
    ;
```

<span data-ttu-id="602c5-2091">경우의 피연산자는 *shift_expression* 컴파일 시간 형식이 `dynamic`, 다음 식이 동적으로 바인딩 되었는지 ([동적 바인딩](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2091">If an operand of a *shift_expression* has the compile-time type `dynamic`, then the expression is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="602c5-2092">이 경우 컴파일 시간 식의 형식이 `dynamic`, 아래에 설명 된 해결 방법을 컴파일 시간 형식이 해당 피연산자의 런타임 형식을 사용 하 여 런타임 시 수행 됩니다 및 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2092">In this case the compile-time type of the expression is `dynamic`, and the resolution described below will take place at run-time using the run-time type of those operands that have the compile-time type `dynamic`.</span></span>

<span data-ttu-id="602c5-2093">폼의 작업에 대 한 `x << count` 또는 `x >> count`, 이항 연산자 오버 로드 확인 ([이항 연산자 오버 로드 확인](expressions.md#binary-operator-overload-resolution)) 특정 연산자 구현을 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2093">For an operation of the form `x << count` or `x >> count`, binary operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="602c5-2094">피연산자는 선택한 연산자의 매개 변수 형식으로 변환 됩니다 하 고 결과의 형식은 연산자의 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2094">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="602c5-2095">오버 로드 된 시프트 연산자를 선언할 때 첫 번째 피연산자의 형식은 항상 이어야 클래스 또는 구조체 연산자 선언에 포함 된 하며 두 번째 피연산자의 형식은 항상 해야 `int`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2095">When declaring an overloaded shift operator, the type of the first operand must always be the class or struct containing the operator declaration, and the type of the second operand must always be `int`.</span></span>

<span data-ttu-id="602c5-2096">미리 정의 된 시프트 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2096">The predefined shift operators are listed below.</span></span>

*  <span data-ttu-id="602c5-2097">왼쪽으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2097">Shift left:</span></span>

   ```csharp
   int operator <<(int x, int count);
   uint operator <<(uint x, int count);
   long operator <<(long x, int count);
   ulong operator <<(ulong x, int count);
   ```

   <span data-ttu-id="602c5-2098">합니다 `<<` 연산자 shifts `x` 비트 수 만큼 왼쪽 아래에 설명 된 대로 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2098">The `<<` operator shifts `x` left by a number of bits computed as described below.</span></span>

   <span data-ttu-id="602c5-2099">결과 형식 범위 밖에 있는 경우 상위 비트 `x` 는 삭제, 나머지 비트를 왼쪽으로 시프트는 및 낮은 빈 비트 위치가 0으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2099">The high-order bits outside the range of the result type of `x` are discarded, the remaining bits are shifted left, and the low-order empty bit positions are set to zero.</span></span>

*  <span data-ttu-id="602c5-2100">오른쪽으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2100">Shift right:</span></span>

   ```csharp
   int operator >>(int x, int count);
   uint operator >>(uint x, int count);
   long operator >>(long x, int count);
   ulong operator >>(ulong x, int count);
   ```

   <span data-ttu-id="602c5-2101">합니다 `>>` 연산자 shifts `x` 비트 수 만큼 오른쪽 아래에 설명 된 대로 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2101">The `>>` operator shifts `x` right by a number of bits computed as described below.</span></span>

   <span data-ttu-id="602c5-2102">때 `x` 형식입니다 `int` 또는 `long`의 하위 비트로 `x` 는 무시 나머지 비트는 오른쪽으로 시프트 하 고 높은 차수의 빈 비트 위치는 0으로 설정 됩니다 `x` 이며 음수가 아닌 설정 중 하나를 `x` 음수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2102">When `x` is of type `int` or `long`, the low-order bits of `x` are discarded, the remaining bits are shifted right, and the high-order empty bit positions are set to zero if `x` is non-negative and set to one if `x` is negative.</span></span>

   <span data-ttu-id="602c5-2103">때 `x` 유형의 `uint` 또는 `ulong`의 낮은 순서 비트 `x` 는 상위 빈 비트 위치는 0으로 설정 및 삭제 하 고, 나머지 비트는 오른쪽으로 시프트 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2103">When `x` is of type `uint` or `ulong`, the low-order bits of `x` are discarded, the remaining bits are shifted right, and the high-order empty bit positions are set to zero.</span></span>

<span data-ttu-id="602c5-2104">미리 정의 된 연산자에 대 한 이동할 비트 수는 다음과 같이 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2104">For the predefined operators, the number of bits to shift is computed as follows:</span></span>

*  <span data-ttu-id="602c5-2105">때 유형의 `x` 됩니다 `int` 또는 `uint`의 하위 5 비트로 시프트 수가 지정 됩니다 `count`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2105">When the type of `x` is `int` or `uint`, the shift count is given by the low-order five bits of `count`.</span></span> <span data-ttu-id="602c5-2106">시프트 수가 계산 되는 즉, `count & 0x1F`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2106">In other words, the shift count is computed from `count & 0x1F`.</span></span>
*  <span data-ttu-id="602c5-2107">때 유형의 `x` 됩니다 `long` 또는 `ulong`의 하위 6 비트로 시프트 수가 지정 됩니다 `count`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2107">When the type of `x` is `long` or `ulong`, the shift count is given by the low-order six bits of `count`.</span></span> <span data-ttu-id="602c5-2108">시프트 수가 계산 되는 즉, `count & 0x3F`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2108">In other words, the shift count is computed from `count & 0x3F`.</span></span>

<span data-ttu-id="602c5-2109">시프트 연산자의 값을 단순히 반환 결과 시프트 수가 0 인 경우 `x`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2109">If the resulting shift count is zero, the shift operators simply return the value of `x`.</span></span>

<span data-ttu-id="602c5-2110">오버플로 일으키지 및에서 동일한 결과 생성 하지 시프트 연산을 `checked` 고 `unchecked` 컨텍스트.</span><span class="sxs-lookup"><span data-stu-id="602c5-2110">Shift operations never cause overflows and produce the same results in `checked` and `unchecked` contexts.</span></span>

<span data-ttu-id="602c5-2111">때의 왼쪽된 피연산자는 `>>` 연산자는 부호 있는 정수 형식, 연산자는 산술 오른쪽 시프트는 피연산자의 가장 중요 한 비트 (부호 비트)의 값이 전파 됩니다 여기서 상위 빈 비트 위치로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2111">When the left operand of the `>>` operator is of a signed integral type, the operator performs an arithmetic shift right wherein the value of the most significant bit (the sign bit) of the operand is propagated to the high-order empty bit positions.</span></span> <span data-ttu-id="602c5-2112">때의 왼쪽된 피연산자는 `>>` 연산자는 부호 없는 정수 형식, 연산자는 논리 시프트 수행 바로 여기서 상위 빈 비트 위치는 항상 0으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2112">When the left operand of the `>>` operator is of an unsigned integral type, the operator performs a logical shift right wherein high-order empty bit positions are always set to zero.</span></span> <span data-ttu-id="602c5-2113">피연산자 형식에서 유추 되는 연산의 반대 작업을 수행 하려면 명시적 캐스트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2113">To perform the opposite operation of that inferred from the operand type, explicit casts can be used.</span></span> <span data-ttu-id="602c5-2114">예를 들어 경우 `x` 형식의 변수가 `int`, 작업 `unchecked((int)((uint)x >> y))` 오른쪽 논리 시프트를 수행 `x`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2114">For example, if `x` is a variable of type `int`, the operation `unchecked((int)((uint)x >> y))` performs a logical shift right of `x`.</span></span>

## <a name="relational-and-type-testing-operators"></a><span data-ttu-id="602c5-2115">관계형 및 형식 테스트 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2115">Relational and type-testing operators</span></span>

<span data-ttu-id="602c5-2116">`==`, `!=`, `<`, `>`를 `<=`를 `>=`를 `is` 및 `as` 연산자는 관계형 및 형식 테스트 연산자 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2116">The `==`, `!=`, `<`, `>`, `<=`, `>=`, `is` and `as` operators are called the relational and type-testing operators.</span></span>

```antlr
relational_expression
    : shift_expression
    | relational_expression '<' shift_expression
    | relational_expression '>' shift_expression
    | relational_expression '<=' shift_expression
    | relational_expression '>=' shift_expression
    | relational_expression 'is' type
    | relational_expression 'as' type
    ;

equality_expression
    : relational_expression
    | equality_expression '==' relational_expression
    | equality_expression '!=' relational_expression
    ;
```

<span data-ttu-id="602c5-2117">합니다 `is` 연산자에 설명 되어 [는 연산자가](expressions.md#the-is-operator) 및 `as` 연산자에 설명 되어 [As 연산자](expressions.md#the-as-operator)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2117">The `is` operator is described in [The is operator](expressions.md#the-is-operator) and the `as` operator is described in [The as operator](expressions.md#the-as-operator).</span></span>

<span data-ttu-id="602c5-2118">`==`, `!=`, `<`, `>`, `<=` 하 고 `>=` 연산자는 ***비교 연산자***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2118">The `==`, `!=`, `<`, `>`, `<=` and `>=` operators are ***comparison operators***.</span></span>

<span data-ttu-id="602c5-2119">비교 연산자의 피연산자는 컴파일 시간 형식에 있는지 `dynamic`, 다음 식이 동적으로 바인딩 되었는지 ([동적 바인딩](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2119">If an operand of a comparison operator has the compile-time type `dynamic`, then the expression is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="602c5-2120">이 경우 컴파일 시간 식의 형식이 `dynamic`, 아래에 설명 된 해결 방법을 컴파일 시간 형식이 해당 피연산자의 런타임 형식을 사용 하 여 런타임 시 수행 됩니다 및 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2120">In this case the compile-time type of the expression is `dynamic`, and the resolution described below will take place at run-time using the run-time type of those operands that have the compile-time type `dynamic`.</span></span>

<span data-ttu-id="602c5-2121">폼의 작업에 대 한 `x` *op* `y`여기서 *op* 는 비교 연산자를 오버 로드 확인 ([이항 연산자 오버 로드 확인](expressions.md#binary-operator-overload-resolution))는 특정 연산자 구현 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2121">For an operation of the form `x` *op* `y`, where *op* is a comparison operator, overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="602c5-2122">피연산자는 선택한 연산자의 매개 변수 형식으로 변환 됩니다 하 고 결과의 형식은 연산자의 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2122">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="602c5-2123">미리 정의 된 비교 연산자는 다음 섹션에서 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2123">The predefined comparison operators are described in the following sections.</span></span> <span data-ttu-id="602c5-2124">형식의 결과 반환 하는 모든 미리 정의 된 비교 연산자 `bool`다음 표에 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2124">All predefined comparison operators return a result of type `bool`, as described in the following table.</span></span>


| <span data-ttu-id="602c5-2125">__작업__</span><span class="sxs-lookup"><span data-stu-id="602c5-2125">__Operation__</span></span> | <span data-ttu-id="602c5-2126">__결과__</span><span class="sxs-lookup"><span data-stu-id="602c5-2126">__Result__</span></span>                                                       |
|---------------|------------------------------------------------------------------|
| `x == y`      | <span data-ttu-id="602c5-2127">`true` 하는 경우 `x` 값과 같음 `y`, `false` 그렇지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="602c5-2127">`true` if `x` is equal to `y`, `false` otherwise</span></span>                 | 
| `x != y`      | <span data-ttu-id="602c5-2128">`true` 하는 경우 `x` 같지 `y`, `false` 그렇지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="602c5-2128">`true` if `x` is not equal to `y`, `false` otherwise</span></span>             | 
| `x < y`       | <span data-ttu-id="602c5-2129">`true` 하는 경우 `x` 는 보다 작은 `y`, `false` 그렇지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="602c5-2129">`true` if `x` is less than `y`, `false` otherwise</span></span>                | 
| `x > y`       | <span data-ttu-id="602c5-2130">`true` 하는 경우 `x` 보다 크면 `y`, `false` 그렇지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="602c5-2130">`true` if `x` is greater than `y`, `false` otherwise</span></span>             | 
| `x <= y`      | <span data-ttu-id="602c5-2131">`true` 하는 경우 `x` 보다 작거나 같음 `y`, `false` 그렇지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="602c5-2131">`true` if `x` is less than or equal to `y`, `false` otherwise</span></span>    | 
| `x >= y`      | <span data-ttu-id="602c5-2132">`true` 하는 경우 `x` 보다 크거나 같음 `y`, `false` 그렇지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="602c5-2132">`true` if `x` is greater than or equal to `y`, `false` otherwise</span></span> | 

### <a name="integer-comparison-operators"></a><span data-ttu-id="602c5-2133">정수 비교 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2133">Integer comparison operators</span></span>

<span data-ttu-id="602c5-2134">미리 정의 된 정수 비교 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2134">The predefined integer comparison operators are:</span></span>
```csharp
bool operator ==(int x, int y);
bool operator ==(uint x, uint y);
bool operator ==(long x, long y);
bool operator ==(ulong x, ulong y);

bool operator !=(int x, int y);
bool operator !=(uint x, uint y);
bool operator !=(long x, long y);
bool operator !=(ulong x, ulong y);

bool operator <(int x, int y);
bool operator <(uint x, uint y);
bool operator <(long x, long y);
bool operator <(ulong x, ulong y);

bool operator >(int x, int y);
bool operator >(uint x, uint y);
bool operator >(long x, long y);
bool operator >(ulong x, ulong y);

bool operator <=(int x, int y);
bool operator <=(uint x, uint y);
bool operator <=(long x, long y);
bool operator <=(ulong x, ulong y);

bool operator >=(int x, int y);
bool operator >=(uint x, uint y);
bool operator >=(long x, long y);
bool operator >=(ulong x, ulong y);
```

<span data-ttu-id="602c5-2135">두 정수 피연산자와 반환의 숫자 값을 비교 하 여 이러한 각 연산자는 `bool` 특정 관계 인지 여부를 나타내는 값 `true` 또는 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2135">Each of these operators compares the numeric values of the two integer operands and returns a `bool` value that indicates whether the particular relation is `true` or `false`.</span></span>

### <a name="floating-point-comparison-operators"></a><span data-ttu-id="602c5-2136">부동 소수점 비교 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2136">Floating-point comparison operators</span></span>

<span data-ttu-id="602c5-2137">미리 정의 된 부동 소수점 비교 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2137">The predefined floating-point comparison operators are:</span></span>
```csharp
bool operator ==(float x, float y);
bool operator ==(double x, double y);

bool operator !=(float x, float y);
bool operator !=(double x, double y);

bool operator <(float x, float y);
bool operator <(double x, double y);

bool operator >(float x, float y);
bool operator >(double x, double y);

bool operator <=(float x, float y);
bool operator <=(double x, double y);

bool operator >=(float x, float y);
bool operator >=(double x, double y);
```

<span data-ttu-id="602c5-2138">연산자는 IEEE 754 표준 규칙에 따라 피연산자를 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2138">The operators compare the operands according to the rules of the IEEE 754 standard:</span></span>

*  <span data-ttu-id="602c5-2139">결과 피연산자 중 하나가 NaN 이면 `false` 제외한 모든 연산자에 대 한 `!=`, 결과 인 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2139">If either operand is NaN, the result is `false` for all operators except `!=`, for which the result is `true`.</span></span> <span data-ttu-id="602c5-2140">모든 두 피연산자에 대 한 `x != y` 와 동일한 결과가 항상 `!(x == y)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2140">For any two operands, `x != y` always produces the same result as `!(x == y)`.</span></span> <span data-ttu-id="602c5-2141">그러나 하나 혹은 두 피연산자로 경우 NaN 합니다 `<`, `>`를 `<=`, 및 `>=` 연산자 반대 연산자의 논리 부정으로 동일한 결과 생성 하지.</span><span class="sxs-lookup"><span data-stu-id="602c5-2141">However, when one or both operands are NaN, the `<`, `>`, `<=`, and `>=` operators do not produce the same results as the logical negation of the opposite operator.</span></span> <span data-ttu-id="602c5-2142">예를 들어 경우의 `x` 및 `y` NaN 이면 `x < y` 됩니다 `false`, 하지만 `!(x >= y)` 는 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2142">For example, if either of `x` and `y` is NaN, then `x < y` is `false`, but `!(x >= y)` is `true`.</span></span>
*  <span data-ttu-id="602c5-2143">연산자를 순서 대로 부동 소수점 두 피연산자의 값을 비교 피연산자가 모두 NaN,</span><span class="sxs-lookup"><span data-stu-id="602c5-2143">When neither operand is NaN, the operators compare the values of the two floating-point operands with respect to the ordering</span></span>

   ```
   -inf < -max < ... < -min < -0.0 == +0.0 < +min < ... < +max < +inf
   ```

   <span data-ttu-id="602c5-2144">여기서 `min` 및 `max` 최소 및 최대 양수 유한 값은 지정 된 부동 소수점 형식으로 표현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2144">where `min` and `max` are the smallest and largest positive finite values that can be represented in the given floating-point format.</span></span> <span data-ttu-id="602c5-2145">이렇게 순서를 지정 하는 주목할 만한 미치는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2145">Notable effects of this ordering are:</span></span>
   * <span data-ttu-id="602c5-2146">양수 및 음수 0으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2146">Negative and positive zeros are considered equal.</span></span>
   * <span data-ttu-id="602c5-2147">음의 무한대는 다른 모든 값 보다는 같지만 다른 음의 무한대로 작을 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2147">A negative infinity is considered less than all other values, but equal to another negative infinity.</span></span>
   * <span data-ttu-id="602c5-2148">다른 모든 값을 초과 하지만 다른 양의 무한대와 양의 무한대로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2148">A positive infinity is considered greater than all other values, but equal to another positive infinity.</span></span>

### <a name="decimal-comparison-operators"></a><span data-ttu-id="602c5-2149">10 진수 비교 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2149">Decimal comparison operators</span></span>

<span data-ttu-id="602c5-2150">미리 정의 된 10 진수 비교 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2150">The predefined decimal comparison operators are:</span></span>
```csharp
bool operator ==(decimal x, decimal y);
bool operator !=(decimal x, decimal y);
bool operator <(decimal x, decimal y);
bool operator >(decimal x, decimal y);
bool operator <=(decimal x, decimal y);
bool operator >=(decimal x, decimal y);
```

<span data-ttu-id="602c5-2151">두 개의 10 진수 피연산자와 반환의 숫자 값을 비교 하 여 이러한 각 연산자는 `bool` 특정 관계 인지 여부를 나타내는 값 `true` 또는 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2151">Each of these operators compares the numeric values of the two decimal operands and returns a `bool` value that indicates whether the particular relation is `true` or `false`.</span></span> <span data-ttu-id="602c5-2152">10 진수 각 비교는 해당 관계 나 형식의 같음 연산자를 사용 하 여 `System.Decimal`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2152">Each decimal comparison is equivalent to using the corresponding relational or equality operator of type `System.Decimal`.</span></span>

### <a name="boolean-equality-operators"></a><span data-ttu-id="602c5-2153">부울 같음 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2153">Boolean equality operators</span></span>

<span data-ttu-id="602c5-2154">미리 정의 된 부울 같음 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2154">The predefined boolean equality operators are:</span></span>
```csharp
bool operator ==(bool x, bool y);
bool operator !=(bool x, bool y);
```

<span data-ttu-id="602c5-2155">결과 `==` 는 `true` 둘 다 `x` 및 `y` 됩니다 `true` 둘 다 또는 `x` 및 `y` 는 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2155">The result of `==` is `true` if both `x` and `y` are `true` or if both `x` and `y` are `false`.</span></span> <span data-ttu-id="602c5-2156">그렇지 않으면 결과 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2156">Otherwise, the result is `false`.</span></span>

<span data-ttu-id="602c5-2157">결과 `!=` 는 `false` 둘 다 `x` 및 `y` 됩니다 `true` 둘 다 또는 `x` 및 `y` 는 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2157">The result of `!=` is `false` if both `x` and `y` are `true` or if both `x` and `y` are `false`.</span></span> <span data-ttu-id="602c5-2158">그렇지 않으면 결과 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2158">Otherwise, the result is `true`.</span></span> <span data-ttu-id="602c5-2159">형식의 피연산자가 하는 경우 `bool`는 `!=` 연산자와 동일한 결과 생성 합니다 `^` 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2159">When the operands are of type `bool`, the `!=` operator produces the same result as the `^` operator.</span></span>

### <a name="enumeration-comparison-operators"></a><span data-ttu-id="602c5-2160">열거형 비교 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2160">Enumeration comparison operators</span></span>

<span data-ttu-id="602c5-2161">모든 열거형에는 다음 미리 정의 된 비교 연산자를 암시적으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2161">Every enumeration type implicitly provides the following predefined comparison operators:</span></span>
```csharp
bool operator ==(E x, E y);
bool operator !=(E x, E y);
bool operator <(E x, E y);
bool operator >(E x, E y);
bool operator <=(E x, E y);
bool operator >=(E x, E y);
```

<span data-ttu-id="602c5-2162">평가 결과 `x op y`여기서 `x` 하 고 `y` 열거형 형식의 식이 `E` 기본 형식을 사용 하 여 `U`, 및 `op` 는 비교 연산자 중 하나를 정확 하 게 동일 평가 `((U)x) op ((U)y)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2162">The result of evaluating `x op y`, where `x` and `y` are expressions of an enumeration type `E` with an underlying type `U`, and `op` is one of the comparison operators, is exactly the same as evaluating `((U)x) op ((U)y)`.</span></span> <span data-ttu-id="602c5-2163">즉, 열거형 형식 비교 연산자는 단순히 두 피연산자의 기본 정수 값을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2163">In other words, the enumeration type comparison operators simply compare the underlying integral values of the two operands.</span></span>

### <a name="reference-type-equality-operators"></a><span data-ttu-id="602c5-2164">참조 형식이 같음 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2164">Reference type equality operators</span></span>

<span data-ttu-id="602c5-2165">미리 정의 된 참조 형식이 같음 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2165">The predefined reference type equality operators are:</span></span>
```csharp
bool operator ==(object x, object y);
bool operator !=(object x, object y);
```

<span data-ttu-id="602c5-2166">연산자는 두 참조 같음 또는 같지 않은지 비교의 결과 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2166">The operators return the result of comparing the two references for equality or non-equality.</span></span>

<span data-ttu-id="602c5-2167">미리 정의 된 참조 형식이 같음 연산자 형식의 피연산자를 사용할 수 있으므로 `object`를 선언 하지 마십시오. 해당 하는 모든 형식에 적용 `operator ==` 고 `operator !=` 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2167">Since the predefined reference type equality operators accept operands of type `object`, they apply to all types that do not declare applicable `operator ==` and `operator !=` members.</span></span> <span data-ttu-id="602c5-2168">반대로, 모든 적용 가능한 사용자 정의 같음 연산자는 효과적으로 미리 정의 된 참조 형식이 같음 연산자를 숨깁니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2168">Conversely, any applicable user-defined equality operators effectively hide the predefined reference type equality operators.</span></span>

<span data-ttu-id="602c5-2169">미리 정의 된 참조 형식이 같음 연산자에는 다음 중 하나 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2169">The predefined reference type equality operators require one of the following:</span></span>

*  <span data-ttu-id="602c5-2170">두 피연산자가 모두 것으로 알려진 형식의 값을 *reference_type* 또는 리터럴 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2170">Both operands are a value of a type known to be a *reference_type* or the literal `null`.</span></span> <span data-ttu-id="602c5-2171">또한 명시적 참조 변환이 ([명시적 참조 변환을](conversions.md#explicit-reference-conversions)) 두 피연산자의 형식에서 다른 피연산자의 형식으로 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2171">Furthermore, an explicit reference conversion ([Explicit reference conversions](conversions.md#explicit-reference-conversions)) exists from the type of either operand to the type of the other operand.</span></span>
*  <span data-ttu-id="602c5-2172">한 피연산자가 형식의 값입니다 `T` 여기서 `T` 는 *type_parameter* 이 고 다른 피연산자가 리터럴 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2172">One operand is a value of type `T` where `T` is a *type_parameter* and the other operand is the literal `null`.</span></span> <span data-ttu-id="602c5-2173">또한 `T` 값 형식 제약 조건이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2173">Furthermore `T` does not have the value type constraint.</span></span>

<span data-ttu-id="602c5-2174">이러한 조건 중 하나가 true 인 경우가 아니면 바인딩 시간 오류를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2174">Unless one of these conditions are true, a binding-time error occurs.</span></span> <span data-ttu-id="602c5-2175">이러한 규칙의 주목할 만한 영향 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2175">Notable implications of these rules are:</span></span>

*  <span data-ttu-id="602c5-2176">이 미리 정의 된 참조 형식이 같음 연산자를 사용 하 여 바인딩 시간에 다른 것으로 알려져 있는 두 개의 참조를 비교할에 바인딩 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2176">It is a binding-time error to use the predefined reference type equality operators to compare two references that are known to be different at binding-time.</span></span> <span data-ttu-id="602c5-2177">예를 들어 바인딩 시간에 대 한 유형의 피연산자가 두 클래스 형식인 경우 `A` 및 `B`, 경우 모두 `A` 도 `B` 는 것이 불가능 동일한 개체를 참조 하는 두 피연산자에 대 한 다음 다른에서 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2177">For example, if the binding-time types of the operands are two class types `A` and `B`, and if neither `A` nor `B` derives from the other, then it would be impossible for the two operands to reference the same object.</span></span> <span data-ttu-id="602c5-2178">따라서 작업 바인딩 시간 오류로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2178">Thus, the operation is considered a binding-time error.</span></span>
*  <span data-ttu-id="602c5-2179">미리 정의 된 참조 형식이 같음 연산자 값 형식 피연산자 비교할 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2179">The predefined reference type equality operators do not permit value type operands to be compared.</span></span> <span data-ttu-id="602c5-2180">따라서 구조체 형식이 고유한 같음 연산자를 선언 하지 않으면 수 없는 해당 구조체 형식의 값을 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2180">Therefore, unless a struct type declares its own equality operators, it is not possible to compare values of that struct type.</span></span>
*  <span data-ttu-id="602c5-2181">미리 정의 된 참조 형식이 같음 연산자는 피연산자에 대 한 되려면 boxing 작업을 일으키지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2181">The predefined reference type equality operators never cause boxing operations to occur for their operands.</span></span> <span data-ttu-id="602c5-2182">새로 할당 된 boxed 인스턴스에 대 한 참조는 다른 모든 참조에서 다를 반드시 하므로 이러한 boxing 작업을 수행 하는 의미 없는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2182">It would be meaningless to perform such boxing operations, since references to the newly allocated boxed instances would necessarily differ from all other references.</span></span>
*  <span data-ttu-id="602c5-2183">경우 형식 매개 변수 형식의 피연산자 `T` 비교할 `null`, 및 런타임 유형의 `T` 형식인 값 비교의 결과 `false`.</span><span class="sxs-lookup"><span data-stu-id="602c5-2183">If an operand of a type parameter type `T` is compared to `null`, and the run-time type of `T` is a value type, the result of the comparison is `false`.</span></span>

<span data-ttu-id="602c5-2184">다음 예제에서는 제한 되지 않은 형식 매개 변수 형식의 인수 인지 확인 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2184">The following example checks whether an argument of an unconstrained type parameter type is `null`.</span></span>
```csharp
class C<T>
{
    void F(T x) {
        if (x == null) throw new ArgumentNullException();
        ...
    }
}
```

<span data-ttu-id="602c5-2185">합니다 `x == null` 구문도 허용 됩니다 `T` 결과 단순히 되도록 정의 및 값 형식에 나타낼 수 있습니다 `false` 때 `T` 값 형식인 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2185">The `x == null` construct is permitted even though `T` could represent a value type, and the result is simply defined to be `false` when `T` is a value type.</span></span>

<span data-ttu-id="602c5-2186">폼의 작업에 대 한 `x == y` 또는 `x != y`해당 하는 경우 `operator ==` 또는 `operator !=` 존재 연산자 오버 로드 확인 ([이항 연산자 오버 로드 확인](expressions.md#binary-operator-overload-resolution)) 하는 규칙 선택 미리 정의 된 참조 형식의 같음 연산자 대신 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2186">For an operation of the form `x == y` or `x != y`, if any applicable `operator ==` or `operator !=` exists, the operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) rules will select that operator instead of the predefined reference type equality operator.</span></span> <span data-ttu-id="602c5-2187">그러나 것이 항상 미리 정의 된 참조 형식의 같음 연산자의 피연산자는 형식 중 하나 또는 모두를 명시적으로 캐스팅 하 여 선택할 수 `object`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2187">However, it is always possible to select the predefined reference type equality operator by explicitly casting one or both of the operands to type `object`.</span></span> <span data-ttu-id="602c5-2188">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2188">The example</span></span>
```csharp
using System;

class Test
{
    static void Main() {
        string s = "Test";
        string t = string.Copy(s);
        Console.WriteLine(s == t);
        Console.WriteLine((object)s == t);
        Console.WriteLine(s == (object)t);
        Console.WriteLine((object)s == (object)t);
    }
}
```
<span data-ttu-id="602c5-2189">는 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2189">produces the output</span></span>
```
True
False
False
False
```

<span data-ttu-id="602c5-2190">`s` 하 고 `t` 별개의 두 변수 참조 `string` 같은 문자가 포함 되는 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="602c5-2190">The `s` and `t` variables refer to two distinct `string` instances containing the same characters.</span></span> <span data-ttu-id="602c5-2191">첫 번째 비교 출력 `True` 때문에 미리 정의 된 문자열 같음 연산자 ([문자열 같음 연산자](expressions.md#string-equality-operators)) 형식의 두 피연산자가 선택 됩니다 `string`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2191">The first comparison outputs `True` because the predefined string equality operator ([String equality operators](expressions.md#string-equality-operators)) is selected when both operands are of type `string`.</span></span> <span data-ttu-id="602c5-2192">나머지 모든 비교 출력 `False` 미리 정의 된 참조 형식의 같음 연산자는 피연산자 중 하나 이상이 유형이 면 선택한 없기 때문에 `object`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2192">The remaining comparisons all output `False` because the predefined reference type equality operator is selected when one or both of the operands are of type `object`.</span></span>

<span data-ttu-id="602c5-2193">참고에서 위의 방법을 값 형식에 대해 의미가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2193">Note that the above technique is not meaningful for value types.</span></span> <span data-ttu-id="602c5-2194">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2194">The example</span></span>
```csharp
class Test
{
    static void Main() {
        int i = 123;
        int j = 123;
        System.Console.WriteLine((object)i == (object)j);
    }
}
```
<span data-ttu-id="602c5-2195">출력 `False` 캐스팅의 두 가지 별도 인스턴스에 대 한 참조를 만들기 때문에 boxed `int` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2195">outputs `False` because the casts create references to two separate instances of boxed `int` values.</span></span>

### <a name="string-equality-operators"></a><span data-ttu-id="602c5-2196">문자열 같음 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2196">String equality operators</span></span>

<span data-ttu-id="602c5-2197">미리 정의 된 문자열 같음 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2197">The predefined string equality operators are:</span></span>
```csharp
bool operator ==(string x, string y);
bool operator !=(string x, string y);
```

<span data-ttu-id="602c5-2198">두 `string` 값 중 하나가 true 인 경우 같다고 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2198">Two `string` values are considered equal when one of the following is true:</span></span>

*  <span data-ttu-id="602c5-2199">값이 모두 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2199">Both values are `null`.</span></span>
*  <span data-ttu-id="602c5-2200">두 값은 null이 아닌 각 문자 위치에 동일한 길이 및 똑같은 문자가 있는 문자열 인스턴스에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2200">Both values are non-null references to string instances that have identical lengths and identical characters in each character position.</span></span>

<span data-ttu-id="602c5-2201">문자열 같음 연산자는 문자열 참조가 아닌 문자열 값을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2201">The string equality operators compare string values rather than string references.</span></span> <span data-ttu-id="602c5-2202">동일한 일련의 문자를 포함 하는 두 개의 별도 문자열 인스턴스를 하는 경우 문자열의 값이 같으면 하지만 참조는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2202">When two separate string instances contain the exact same sequence of characters, the values of the strings are equal, but the references are different.</span></span> <span data-ttu-id="602c5-2203">에 설명 된 대로 [참조 형식이 같음 연산자](expressions.md#reference-type-equality-operators), 참조 형식이 같음 연산자를 사용 하 여 문자열 값 대신 문자열 참조를 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2203">As described in [Reference type equality operators](expressions.md#reference-type-equality-operators), the reference type equality operators can be used to compare string references instead of string values.</span></span>

### <a name="delegate-equality-operators"></a><span data-ttu-id="602c5-2204">대리자 같음 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2204">Delegate equality operators</span></span>

<span data-ttu-id="602c5-2205">모든 대리자 형식에는 다음과 같은 미리 정의 된 비교 연산자를 암시적으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2205">Every delegate type implicitly provides the following predefined comparison operators:</span></span>

```csharp
bool operator ==(System.Delegate x, System.Delegate y);
bool operator !=(System.Delegate x, System.Delegate y);
```

<span data-ttu-id="602c5-2206">두 명의 대리자 인스턴스가 동일한 지 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2206">Two delegate instances are considered equal as follows:</span></span>

*  <span data-ttu-id="602c5-2207">대리자 인스턴스 중 하나에 해당 하는 경우 `null`, 경우에 둘 다 같은지 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2207">If either of the delegate instances is `null`, they are equal if and only if both are `null`.</span></span>
*  <span data-ttu-id="602c5-2208">대리자는 항상 서로 다른 런타임 형식이 있으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2208">If the delegates have different run-time type they are never equal.</span></span>
*  <span data-ttu-id="602c5-2209">대리자 인스턴스 둘 다 호출 목록이 있으면 ([대리자 선언](delegates.md#delegate-declarations)), 경우에 해당 호출 목록이 동일한 길이 되며 호출 목록의 각 항목은 같은 (아래 정의)은 해당 인스턴스가 같으면 해당 항목에 다른의 호출 목록에서 주문 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2209">If both of the delegate instances have an invocation list ([Delegate declarations](delegates.md#delegate-declarations)), those instances are equal if and only if their invocation lists are the same length, and each entry in one's invocation list is equal (as defined below) to the corresponding entry, in order, in the other's invocation list.</span></span>

<span data-ttu-id="602c5-2210">호출 목록 항목의 일치 여부를 제어 하는 다음 규칙:</span><span class="sxs-lookup"><span data-stu-id="602c5-2210">The following rules govern the equality of invocation list entries:</span></span>

*  <span data-ttu-id="602c5-2211">두 개의 호출 목록 항목이 모두 동일한 정적 참조 이면 메서드 다음 항목은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2211">If two invocation list entries both refer to the same static method then the entries are equal.</span></span>
*  <span data-ttu-id="602c5-2212">(정의 된 대로 참조 같음 연산자) 두 개의 호출 목록 항목이 모두 동일한 대상 개체 동일한 비정적 메서드를 참조 하는 경우 다음 항목은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2212">If two invocation list entries both refer to the same non-static method on the same target object (as defined by the reference equality operators) then the entries are equal.</span></span>
*  <span data-ttu-id="602c5-2213">호출 목록 항목과 의미상 동일 평가에서 생성 된 *anonymous_method_expression*s 또는 *lambda_expression*캡처된 외부 변수 (비어 있을 수 있는) 집합이 함께 인스턴스는 허용 (하지만 필요 하지 않습니다)과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2213">Invocation list entries produced from evaluation of semantically identical *anonymous_method_expression*s or *lambda_expression*s with the same (possibly empty) set of captured outer variable instances are permitted (but not required) to be equal.</span></span>

### <a name="equality-operators-and-null"></a><span data-ttu-id="602c5-2214">같음 연산자 및 null</span><span class="sxs-lookup"><span data-stu-id="602c5-2214">Equality operators and null</span></span>

<span data-ttu-id="602c5-2215">합니다 `==` 및 `!=` 연산자를 nullable 형식 및 다른 값으로 피연산자 하나를 허용 합니다 `null` 리터럴, 미리 정의 되거나 사용자 정의 연산자 (에서 unlifted 또는 폼 리프트) 작업에 대해 존재 하는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2215">The `==` and `!=` operators permit one operand to be a value of a nullable type and the other to be the `null` literal, even if no predefined or user-defined operator (in unlifted or lifted form) exists for the operation.</span></span>

<span data-ttu-id="602c5-2216">작업의 형식 중 하나</span><span class="sxs-lookup"><span data-stu-id="602c5-2216">For an operation of one of the forms</span></span>
```csharp
x == null
null == x
x != null
null != x
```
<span data-ttu-id="602c5-2217">여기서 `x` 연산자 오버 로드를 확인 하는 경우는 nullable 형식의 식 ([이항 연산자 오버 로드 확인](expressions.md#binary-operator-overload-resolution))를 해당 연산자의 결과 찾지 못한에서 대신 계산 되는 `HasValue` 속성의 `x`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2217">where `x` is an expression of a nullable type, if operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) fails to find an applicable operator, the result is instead computed from the `HasValue` property of `x`.</span></span> <span data-ttu-id="602c5-2218">먼저 두 가지 형식으로 변환 됩니다 특히 `!x.HasValue`, 마지막으로 두 가지 형식으로 변환 됩니다 및 `x.HasValue`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2218">Specifically, the first two forms are translated into `!x.HasValue`, and last two forms are translated into `x.HasValue`.</span></span>

### <a name="the-is-operator"></a><span data-ttu-id="602c5-2219">여는 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2219">The is operator</span></span>

<span data-ttu-id="602c5-2220">`is` 연산자는 동적으로 개체의 런타임 형식을 지정 된 형식과 호환 되는지 확인 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2220">The `is` operator is used to dynamically check if the run-time type of an object is compatible with a given type.</span></span> <span data-ttu-id="602c5-2221">작업의 결과 `E is T`, 여기서 `E` 식 및 `T` 형식인 부울을 나타내는 값 여부를 `E` 형식으로 성공적으로 변환 될 수 있습니다 `T` 참조 변환을 boxing 하 여 변환 또는 unboxing 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2221">The result of the operation `E is T`, where `E` is an expression and `T` is a type, is a boolean value indicating whether `E` can successfully be converted to type `T` by a reference conversion, a boxing conversion, or an unboxing conversion.</span></span> <span data-ttu-id="602c5-2222">모든 형식 매개 변수에 대해 형식 인수 대체 된 후 작업을 다음과 같이 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2222">The operation is evaluated as follows, after type arguments have been substituted for all type parameters:</span></span>

*  <span data-ttu-id="602c5-2223">경우 `E` 는 컴파일 타임 오류가 발생 하는 익명 함수</span><span class="sxs-lookup"><span data-stu-id="602c5-2223">If `E` is an anonymous function, a compile-time error occurs</span></span>
*  <span data-ttu-id="602c5-2224">경우 `E` 는 메서드 그룹 또는 `null` 경우 리터럴 형식의 `E` 참조 형식 또는 nullable 형식 및 값 `E` 가 null 이면 결과 false입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2224">If `E` is a method group or the `null` literal, of if the type of `E` is a reference type or a nullable type and the value of `E` is null, the result is false.</span></span>
*  <span data-ttu-id="602c5-2225">수이 고, 그렇지 `D` 의 동적 형식을 나타내는 `E` 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2225">Otherwise, let `D` represent the dynamic type of `E` as follows:</span></span>
   * <span data-ttu-id="602c5-2226">경우 유형의 `E` 참조 형식인 `D` 하 여 인스턴스 참조의 런타임 형식인 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2226">If the type of `E` is a reference type, `D` is the run-time type of the instance reference by `E`.</span></span>
   * <span data-ttu-id="602c5-2227">경우 유형의 `E` nullable 형식인 `D` 는 nullable 형식의 기본 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2227">If the type of `E` is a nullable type, `D` is the underlying type of that nullable type.</span></span>
   * <span data-ttu-id="602c5-2228">경우 유형의 `E` nullable이 아닌 값 형식인 `D` 유형의 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2228">If the type of `E` is a non-nullable value type, `D` is the type of `E`.</span></span>
*  <span data-ttu-id="602c5-2229">작업의 결과에 따라 달라 집니다 `D` 및 `T` 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2229">The result of the operation depends on `D` and `T` as follows:</span></span>
   * <span data-ttu-id="602c5-2230">하는 경우 `T` 참조 형식인 결과가 true 인 경우 `D` 및 `T` 는 동일한 형식인 경우 `D` 는 및 참조 형식에서 암시적 참조 변환이 `D` 에 `T` 가 이거나 `D` 값 형식과 boxing 변환 `D` 에 `T` 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2230">If `T` is a reference type, the result is true if `D` and `T` are the same type, if `D` is a reference type and an implicit reference conversion from `D` to `T` exists, or if `D` is a value type and a boxing conversion from `D` to `T` exists.</span></span>
   * <span data-ttu-id="602c5-2231">하는 경우 `T` nullable 형식인 결과가 true 인 경우 `D` 의 기본 형식인 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2231">If `T` is a nullable type, the result is true if `D` is the underlying type of `T`.</span></span>
   * <span data-ttu-id="602c5-2232">하는 경우 `T` nullable이 아닌 값 형식인 결과가 true 인 경우 `D` 및 `T` 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2232">If `T` is a non-nullable value type, the result is true if `D` and `T` are the same type.</span></span>
   * <span data-ttu-id="602c5-2233">그렇지 않으면 결과 false입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2233">Otherwise, the result is false.</span></span>

<span data-ttu-id="602c5-2234">사용자 정의 변환으로 간주 되지 않습니다 참고는 `is` 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2234">Note that user defined conversions, are not considered by the `is` operator.</span></span>

### <a name="the-as-operator"></a><span data-ttu-id="602c5-2235">As 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2235">The as operator</span></span>

<span data-ttu-id="602c5-2236">`as` 연산자는 지정 된 참조 형식 또는 nullable 형식과 값을 명시적으로 변환를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2236">The `as` operator is used to explicitly convert a value to a given reference type or nullable type.</span></span> <span data-ttu-id="602c5-2237">Cast 식과 달리 ([캐스트 식](expressions.md#cast-expressions)), `as` 연산자 절대 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2237">Unlike a cast expression ([Cast expressions](expressions.md#cast-expressions)), the `as` operator never throws an exception.</span></span> <span data-ttu-id="602c5-2238">대신, 표시 된 변환이 가능 하지 않은 경우 결과 값은 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2238">Instead, if the indicated conversion is not possible, the resulting value is `null`.</span></span>

<span data-ttu-id="602c5-2239">폼의 작업에서 `E as T`, `E` 식 이어야 하 고 `T` 참조 형식 또는 nullable 형식을 알려진 형식 매개 변수는 참조 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2239">In an operation of the form `E as T`, `E` must be an expression and `T` must be a reference type, a type parameter known to be a reference type, or a nullable type.</span></span> <span data-ttu-id="602c5-2240">또한 다음 중 하나 이상의 true 이거나 그렇지 않으면 컴파일 타임 오류가 발생 하는:</span><span class="sxs-lookup"><span data-stu-id="602c5-2240">Furthermore, at least one of the following must be true, or otherwise a compile-time error occurs:</span></span>

*  <span data-ttu-id="602c5-2241">Id ([Id 변환을](conversions.md#identity-conversion)), 암시적 null을 허용 ([암시적 nullable 변환](conversions.md#implicit-nullable-conversions))에 대 한 암시적 참조가 ([암시적 참조 변환](conversions.md#implicit-reference-conversions)), boxing ([ Boxing 변환](conversions.md#boxing-conversions)) 명시적 nullable ([명시적 nullable 변환](conversions.md#explicit-nullable-conversions))를 명시적으로 참조 ([명시적 참조 변환을](conversions.md#explicit-reference-conversions)), unboxing 또는 ([Unboxing 변환](conversions.md#unboxing-conversions))에서 변환이 존재 `E` 에 `T`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2241">An identity ([Identity conversion](conversions.md#identity-conversion)), implicit nullable ([Implicit nullable conversions](conversions.md#implicit-nullable-conversions)), implicit reference ([Implicit reference conversions](conversions.md#implicit-reference-conversions)), boxing ([Boxing conversions](conversions.md#boxing-conversions)), explicit nullable ([Explicit nullable conversions](conversions.md#explicit-nullable-conversions)), explicit reference ([Explicit reference conversions](conversions.md#explicit-reference-conversions)), or unboxing ([Unboxing conversions](conversions.md#unboxing-conversions)) conversion exists from `E` to `T`.</span></span>
*  <span data-ttu-id="602c5-2242">유형의 `E` 또는 `T` 은 개방형 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2242">The type of `E` or `T` is an open type.</span></span>
*  <span data-ttu-id="602c5-2243">`E` 가 `null` 리터럴.</span><span class="sxs-lookup"><span data-stu-id="602c5-2243">`E` is the `null` literal.</span></span>

<span data-ttu-id="602c5-2244">형식이 컴파일 타임 `E` 아닙니다 `dynamic`, 작업 `E as T` 와 동일한 결과 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2244">If the compile-time type of `E` is not `dynamic`, the operation `E as T` produces the same result as</span></span>
```csharp
E is T ? (T)(E) : (T)null
```
<span data-ttu-id="602c5-2245">단, `E`가 한 번만 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2245">except that `E` is only evaluated once.</span></span> <span data-ttu-id="602c5-2246">컴파일러 최적화를 사용할 수 `E as T` 위의 확장 사용 권한에 포함 된 두 개의 동적 형식 검사와 달리 최대 하나의 동적 형식 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2246">The compiler can be expected to optimize `E as T` to perform at most one dynamic type check as opposed to the two dynamic type checks implied by the expansion above.</span></span>

<span data-ttu-id="602c5-2247">컴파일 타임의 형식이 `E` 됩니다 `dynamic`, 캐스트 연산자와 달리 합니다 `as` 연산자를 동적으로 바인딩되지 않은 ([동적 바인딩](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2247">If the compile-time type of `E` is `dynamic`, unlike the cast operator the `as` operator is not dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="602c5-2248">따라서 확장이 예제의 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-2248">Therefore the expansion in this case is:</span></span>
```csharp
E is T ? (T)(object)(E) : (T)null
```

<span data-ttu-id="602c5-2249">사용자 정의 변환 등의 일부 변환에서 사용할 수 없는 참고는 `as` 연산자 대신 cast 식을 사용 하 여 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2249">Note that some conversions, such as user defined conversions, are not possible with the `as` operator and should instead be performed using cast expressions.</span></span>

<span data-ttu-id="602c5-2250">예제</span><span class="sxs-lookup"><span data-stu-id="602c5-2250">In the example</span></span>
```csharp
class X
{

    public string F(object o) {
        return o as string;        // OK, string is a reference type
    }

    public T G<T>(object o) where T: Attribute {
        return o as T;             // Ok, T has a class constraint
    }

    public U H<U>(object o) {
        return o as U;             // Error, U is unconstrained 
    }
}
```
<span data-ttu-id="602c5-2251">형식 매개 변수 `T` 의 `G` 클래스 제약 조건이 있기 때문에 참조 형식일 것으로 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2251">the type parameter `T` of `G` is known to be a reference type, because it has the class constraint.</span></span> <span data-ttu-id="602c5-2252">그러나 형식 매개 변수 `U` 의 `H` 없습니다 되므로 사용 하는 것은 `as` 연산자 `H` 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2252">The type parameter `U` of `H` is not however; hence the use of the `as` operator in `H` is disallowed.</span></span>

## <a name="logical-operators"></a><span data-ttu-id="602c5-2253">논리 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2253">Logical operators</span></span>

<span data-ttu-id="602c5-2254">합니다 `&`, `^`, 및 `|` 연산자는 논리 연산자 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2254">The `&`, `^`, and `|` operators are called the logical operators.</span></span>

```antlr
and_expression
    : equality_expression
    | and_expression '&' equality_expression
    ;

exclusive_or_expression
    : and_expression
    | exclusive_or_expression '^' and_expression
    ;

inclusive_or_expression
    : exclusive_or_expression
    | inclusive_or_expression '|' exclusive_or_expression
    ;
```

<span data-ttu-id="602c5-2255">논리 연산자의 피연산자는 컴파일 시간 형식에 있는지 `dynamic`, 다음 식이 동적으로 바인딩 되었는지 ([동적 바인딩](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2255">If an operand of a logical operator has the compile-time type `dynamic`, then the expression is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="602c5-2256">이 경우 컴파일 시간 식의 형식이 `dynamic`, 아래에 설명 된 해결 방법을 컴파일 시간 형식이 해당 피연산자의 런타임 형식을 사용 하 여 런타임 시 수행 됩니다 및 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2256">In this case the compile-time type of the expression is `dynamic`, and the resolution described below will take place at run-time using the run-time type of those operands that have the compile-time type `dynamic`.</span></span>

<span data-ttu-id="602c5-2257">폼의 작업에 대 한 `x op y`, 여기서 `op` 논리 연산자를 오버 로드 확인 중 하나입니다 ([이항 연산자 오버 로드 확인](expressions.md#binary-operator-overload-resolution)) 특정 연산자 구현을 선택에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2257">For an operation of the form `x op y`, where `op` is one of the logical operators, overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="602c5-2258">피연산자는 선택한 연산자의 매개 변수 형식으로 변환 됩니다 하 고 결과의 형식은 연산자의 반환 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2258">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="602c5-2259">미리 정의 된 논리 연산자는 다음 섹션에서 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2259">The predefined logical operators are described in the following sections.</span></span>

### <a name="integer-logical-operators"></a><span data-ttu-id="602c5-2260">정수 논리 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2260">Integer logical operators</span></span>

<span data-ttu-id="602c5-2261">미리 정의 된 정수 논리 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2261">The predefined integer logical operators are:</span></span>
```csharp
int operator &(int x, int y);
uint operator &(uint x, uint y);
long operator &(long x, long y);
ulong operator &(ulong x, ulong y);

int operator |(int x, int y);
uint operator |(uint x, uint y);
long operator |(long x, long y);
ulong operator |(ulong x, ulong y);

int operator ^(int x, int y);
uint operator ^(uint x, uint y);
long operator ^(long x, long y);
ulong operator ^(ulong x, ulong y);
```

<span data-ttu-id="602c5-2262">`&` 연산자는 비트를 계산 논리 `AND` 두 피연산자 중 합니다 `|` 연산자는 비트를 계산 논리 `OR` 는 두 피연산자의 및 `^` 연산자 계산 논리 배타적 비트 `OR` 두 피연산자의 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2262">The `&` operator computes the bitwise logical `AND` of the two operands, the `|` operator computes the bitwise logical `OR` of the two operands, and the `^` operator computes the bitwise logical exclusive `OR` of the two operands.</span></span> <span data-ttu-id="602c5-2263">이러한 작업에서 없습니다 오버플로 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2263">No overflows are possible from these operations.</span></span>

### <a name="enumeration-logical-operators"></a><span data-ttu-id="602c5-2264">열거형 논리 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2264">Enumeration logical operators</span></span>

<span data-ttu-id="602c5-2265">모든 열거형 형식 `E` 암시적으로 다음 미리 정의 된 논리 연산자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2265">Every enumeration type `E` implicitly provides the following predefined logical operators:</span></span>

```csharp
E operator &(E x, E y);
E operator |(E x, E y);
E operator ^(E x, E y);
```

<span data-ttu-id="602c5-2266">평가 결과 `x op y`여기서 `x` 하 고 `y` 열거형 형식의 식이 `E` 기본 형식을 사용 하 여 `U`, 및 `op` 는 논리 연산자 중 하나를 정확 하 게 동일 평가 `(E)((U)x op (U)y)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2266">The result of evaluating `x op y`, where `x` and `y` are expressions of an enumeration type `E` with an underlying type `U`, and `op` is one of the logical operators, is exactly the same as evaluating `(E)((U)x op (U)y)`.</span></span> <span data-ttu-id="602c5-2267">즉, 열거형 형식 논리 연산자는 단순히 두 피연산자의 내부 형식에 논리 연산을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2267">In other words, the enumeration type logical operators simply perform the logical operation on the underlying type of the two operands.</span></span>

### <a name="boolean-logical-operators"></a><span data-ttu-id="602c5-2268">부울 논리 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2268">Boolean logical operators</span></span>

<span data-ttu-id="602c5-2269">논리 연산자는 미리 정의 된 부울 값:</span><span class="sxs-lookup"><span data-stu-id="602c5-2269">The predefined boolean logical operators are:</span></span>
```csharp
bool operator &(bool x, bool y);
bool operator |(bool x, bool y);
bool operator ^(bool x, bool y);
```

<span data-ttu-id="602c5-2270">결과 `x & y` 는 `true` 둘 다 `x` 하 고 `y` 는 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2270">The result of `x & y` is `true` if both `x` and `y` are `true`.</span></span> <span data-ttu-id="602c5-2271">그렇지 않으면 결과 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2271">Otherwise, the result is `false`.</span></span>

<span data-ttu-id="602c5-2272">결과인 `x | y` 됩니다 `true` 경우 `x` 또는 `y` 는 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2272">The result of `x | y` is `true` if either `x` or `y` is `true`.</span></span> <span data-ttu-id="602c5-2273">그렇지 않으면 결과 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2273">Otherwise, the result is `false`.</span></span>

<span data-ttu-id="602c5-2274">결과 `x ^ y` 는 `true` 경우 `x` 는 `true` 및 `y` 됩니다 `false`, 또는 `x` 는 `false` 및 `y` 는 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2274">The result of `x ^ y` is `true` if `x` is `true` and `y` is `false`, or `x` is `false` and `y` is `true`.</span></span> <span data-ttu-id="602c5-2275">그렇지 않으면 결과 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2275">Otherwise, the result is `false`.</span></span> <span data-ttu-id="602c5-2276">형식의 피연산자가 하는 경우 `bool`는 `^` 연산자와 동일한 결과 계산 합니다 `!=` 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2276">When the operands are of type `bool`, the `^` operator computes the same result as the `!=` operator.</span></span>

### <a name="nullable-boolean-logical-operators"></a><span data-ttu-id="602c5-2277">Null 허용 부울 논리 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2277">Nullable boolean logical operators</span></span>

<span data-ttu-id="602c5-2278">Nullable 부울 형식 `bool?` 세 가지 값을 나타낼 수 있습니다 `true`, `false`, 및 `null`, SQL의 부울 식에 사용 되는 세 개의 값 형식을 개념적으로 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2278">The nullable boolean type `bool?` can represent three values, `true`, `false`, and `null`, and is conceptually similar to the three-valued type used for boolean expressions in SQL.</span></span> <span data-ttu-id="602c5-2279">생성 되는 결과 보장 하는 `&` 및 `|` 연산자에 대 한 `bool?` 피연산자는 SQL의 세 개의 값 논리를 사용 하 여 일관성이 다음 미리 정의 된 연산자가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2279">To ensure that the results produced by the `&` and `|` operators for `bool?` operands are consistent with SQL's three-valued logic, the following predefined operators are provided:</span></span>

```csharp
bool? operator &(bool? x, bool? y);
bool? operator |(bool? x, bool? y);
```

<span data-ttu-id="602c5-2280">다음 표에서 값의 모든 조합에 대 한 이러한 연산자에서 생성 되는 결과 `true`, `false`, 및 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2280">The following table lists the results produced by these operators for all combinations of the values `true`, `false`, and `null`.</span></span>

| `x`     | `y`     | `x & y` | <span data-ttu-id="602c5-2281">' x</span><span class="sxs-lookup"><span data-stu-id="602c5-2281">\`x</span></span> | <span data-ttu-id="602c5-2282">y'</span><span class="sxs-lookup"><span data-stu-id="602c5-2282">y\`</span></span> |
|:-------:|:-------:|:-------:|:-------:|
| `true`  | `true`  | `true`  | `true`  | 
| `true`  | `false` | `false` | `true`  | 
| `true`  | `null`  | `null`  | `true`  | 
| `false` | `true`  | `false` | `true`  | 
| `false` | `false` | `false` | `false` | 
| `false` | `null`  | `false` | `null`  | 
| `null`  | `true`  | `null`  | `true`  | 
| `null`  | `false` | `false` | `null`  | 
| `null`  | `null`  | `null`  | `null`  | 

## <a name="conditional-logical-operators"></a><span data-ttu-id="602c5-2283">조건부 논리 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2283">Conditional logical operators</span></span>

<span data-ttu-id="602c5-2284">합니다 `&&` 및 `||` 연산자에는 조건부 논리 연산자 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2284">The `&&` and `||` operators are called the conditional logical operators.</span></span> <span data-ttu-id="602c5-2285">"단락" 논리 연산자 에서도 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2285">They are also called the "short-circuiting" logical operators.</span></span>

```antlr
conditional_and_expression
    : inclusive_or_expression
    | conditional_and_expression '&&' inclusive_or_expression
    ;

conditional_or_expression
    : conditional_and_expression
    | conditional_or_expression '||' conditional_and_expression
    ;
```

<span data-ttu-id="602c5-2286">합니다 `&&` 하 고 `||` 연산자는 조건부 버전의는 `&` 및 `|` 연산자:</span><span class="sxs-lookup"><span data-stu-id="602c5-2286">The `&&` and `||` operators are conditional versions of the `&` and `|` operators:</span></span>

*  <span data-ttu-id="602c5-2287">작업이 `x && y` 작업에 해당 `x & y`점을 제외 하 고 `y` 경우에 평가 됩니다 `x` 아닙니다 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2287">The operation `x && y` corresponds to the operation `x & y`, except that `y` is evaluated only if `x` is not `false`.</span></span>
*  <span data-ttu-id="602c5-2288">작업이 `x || y` 작업에 해당 `x | y`점을 제외 하 고 `y` 경우에 평가 됩니다 `x` 아닙니다 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2288">The operation `x || y` corresponds to the operation `x | y`, except that `y` is evaluated only if `x` is not `true`.</span></span>

<span data-ttu-id="602c5-2289">조건부 논리 연산자의 피연산자는 컴파일 시간 형식에 있는지 `dynamic`, 다음 식이 동적으로 바인딩 되었는지 ([동적 바인딩](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2289">If an operand of a conditional logical operator has the compile-time type `dynamic`, then the expression is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="602c5-2290">이 경우 컴파일 시간 식의 형식이 `dynamic`, 아래에 설명 된 해결 방법을 컴파일 시간 형식이 해당 피연산자의 런타임 형식을 사용 하 여 런타임 시 수행 됩니다 및 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2290">In this case the compile-time type of the expression is `dynamic`, and the resolution described below will take place at run-time using the run-time type of those operands that have the compile-time type `dynamic`.</span></span>

<span data-ttu-id="602c5-2291">폼의 작업 `x && y` 나 `x || y` 오버 로드 확인을 적용 하 여 처리 됩니다 ([이항 연산자 오버 로드 확인에](expressions.md#binary-operator-overload-resolution)) 작업 작성 된 것 처럼 `x & y` 또는 `x | y`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2291">An operation of the form `x && y` or `x || y` is processed by applying overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) as if the operation was written `x & y` or `x | y`.</span></span> <span data-ttu-id="602c5-2292">그런 다음</span><span class="sxs-lookup"><span data-stu-id="602c5-2292">Then,</span></span>

*  <span data-ttu-id="602c5-2293">오버 로드 확인 최상의 single 연산자를 찾지 못하면 또는 오버 로드 확인 미리 정의 된 정수 논리 연산자 중 하나를 선택 하는 경우 바인딩 시간 오류를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2293">If overload resolution fails to find a single best operator, or if overload resolution selects one of the predefined integer logical operators, a binding-time error occurs.</span></span>
*  <span data-ttu-id="602c5-2294">그렇지 않으면 선택한 연산자가 미리 정의 된 부울 논리 연산자 중 하나 ([부울 논리 연산자](expressions.md#boolean-logical-operators)) 또는 null 허용 부울 논리 연산자 ([Nullable 부울 논리 연산자](expressions.md#nullable-boolean-logical-operators)), 에 설명 된 대로 작업이 처리 됩니다 [조건부 논리 연산자를 부울](expressions.md#boolean-conditional-logical-operators)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2294">Otherwise, if the selected operator is one of the predefined boolean logical operators ([Boolean logical operators](expressions.md#boolean-logical-operators)) or nullable boolean logical operators ([Nullable boolean logical operators](expressions.md#nullable-boolean-logical-operators)), the operation is processed as described in [Boolean conditional logical operators](expressions.md#boolean-conditional-logical-operators).</span></span>
*  <span data-ttu-id="602c5-2295">그렇지 않으면 선택한 연산자가 사용자 정의 연산자를 하 고에 설명 된 대로 작업이 처리 됩니다 [사용자 정의 조건부 논리 연산자](expressions.md#user-defined-conditional-logical-operators)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2295">Otherwise, the selected operator is a user-defined operator, and the operation is processed as described in [User-defined conditional logical operators](expressions.md#user-defined-conditional-logical-operators).</span></span>

<span data-ttu-id="602c5-2296">직접 조건부 논리 연산자를 오버 로드 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2296">It is not possible to directly overload the conditional logical operators.</span></span> <span data-ttu-id="602c5-2297">그러나 일반 논리 연산자를 기준으로 조건부 논리 연산자를 평가 하기 때문에 일반 논리 연산자의 오버 로드를 특정 제한 사항으로 간주 됩니다 조건부 논리 연산자의 오버 로드.</span><span class="sxs-lookup"><span data-stu-id="602c5-2297">However, because the conditional logical operators are evaluated in terms of the regular logical operators, overloads of the regular logical operators are, with certain restrictions, also considered overloads of the conditional logical operators.</span></span> <span data-ttu-id="602c5-2298">이에서 더 자세히 설명 [사용자 정의 조건부 논리 연산자](expressions.md#user-defined-conditional-logical-operators)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2298">This is described further in [User-defined conditional logical operators](expressions.md#user-defined-conditional-logical-operators).</span></span>

### <a name="boolean-conditional-logical-operators"></a><span data-ttu-id="602c5-2299">부울 조건부 논리 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2299">Boolean conditional logical operators</span></span>

<span data-ttu-id="602c5-2300">때의 피연산자 `&&` 또는 `||` 형식의 `bool`, 해당를 정의 하지 않은 형식의 피연산자가 하는 경우 또는 `operator &` 또는 `operator |`로 암시적으로 정의지 않습니다 하지만 `bool`, 작업이 다음과 같이 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2300">When the operands of `&&` or `||` are of type `bool`, or when the operands are of types that do not define an applicable `operator &` or `operator |`, but do define implicit conversions to `bool`, the operation is processed as follows:</span></span>

*  <span data-ttu-id="602c5-2301">작업이 `x && y` 로 평가 됩니다 `x ? y : false`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2301">The operation `x && y` is evaluated as `x ? y : false`.</span></span> <span data-ttu-id="602c5-2302">다시 말해 `x` 먼저 평가 되 고 형식으로 변환할 `bool`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2302">In other words, `x` is first evaluated and converted to type `bool`.</span></span> <span data-ttu-id="602c5-2303">그런 다음 경우 `x` 는 `true`, `y` 평가 되 고 형식으로 변환할 `bool`, 작업의 결과이 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2303">Then, if `x` is `true`, `y` is evaluated and converted to type `bool`, and this becomes the result of the operation.</span></span> <span data-ttu-id="602c5-2304">작업의 결과 그러지 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2304">Otherwise, the result of the operation is `false`.</span></span>
*  <span data-ttu-id="602c5-2305">작업이 `x || y` 로 평가 됩니다 `x ? true : y`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2305">The operation `x || y` is evaluated as `x ? true : y`.</span></span> <span data-ttu-id="602c5-2306">다시 말해 `x` 먼저 평가 되 고 형식으로 변환할 `bool`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2306">In other words, `x` is first evaluated and converted to type `bool`.</span></span> <span data-ttu-id="602c5-2307">그런 다음 경우 `x` 됩니다 `true`, 작업의 결과 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2307">Then, if `x` is `true`, the result of the operation is `true`.</span></span> <span data-ttu-id="602c5-2308">이 고, 그렇지 `y` 평가 되 고 형식으로 변환할 `bool`, 작업의 결과이 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2308">Otherwise, `y` is evaluated and converted to type `bool`, and this becomes the result of the operation.</span></span>

### <a name="user-defined-conditional-logical-operators"></a><span data-ttu-id="602c5-2309">사용자 정의 조건부 논리 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2309">User-defined conditional logical operators</span></span>

<span data-ttu-id="602c5-2310">때의 피연산자 `&&` 또는 `||` 되는 해당 선언 된 형식의 사용자 정의 `operator &` 또는 `operator |`, 다음 두 가지 true 여야 여기서 `T` 는 선택한 연산자 선언 되는 형식:</span><span class="sxs-lookup"><span data-stu-id="602c5-2310">When the operands of `&&` or `||` are of types that declare an applicable user-defined `operator &` or `operator |`, both of the following must be true, where `T` is the type in which the selected operator is declared:</span></span>

*  <span data-ttu-id="602c5-2311">반환 형식 및 선택한 연산자의 각 매개 변수의 형식이 있어야 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2311">The return type and the type of each parameter of the selected operator must be `T`.</span></span> <span data-ttu-id="602c5-2312">즉, 연산자 논리 계산 해야 합니다 `AND` 또는 논리 `OR` 형식의 두 피연산자의 `T`, 형식의 결과 반환 해야 하 고 `T`.</span><span class="sxs-lookup"><span data-stu-id="602c5-2312">In other words, the operator must compute the logical `AND` or the logical `OR` of two operands of type `T`, and must return a result of type `T`.</span></span>
*  <span data-ttu-id="602c5-2313">`T` 선언이 있어야 `operator true` 고 `operator false`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2313">`T` must contain declarations of `operator true` and `operator false`.</span></span>

<span data-ttu-id="602c5-2314">이러한 요구 사항을 하나라도 충족 되지 않으면 바인딩 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2314">A binding-time error occurs if either of these requirements is not satisfied.</span></span> <span data-ttu-id="602c5-2315">이 고, 그렇지 합니다 `&&` 하거나 `||` 작업은 사용자 정의 결합 하 여 평가 됩니다 `operator true` 또는 `operator false` 선택한 사용자 정의 연산자를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="602c5-2315">Otherwise, the `&&` or `||` operation is evaluated by combining the user-defined `operator true` or `operator false` with the selected user-defined operator:</span></span>

*  <span data-ttu-id="602c5-2316">작업 `x && y` 로 평가 됩니다 `T.false(x) ? x : T.&(x, y)`여기서 `T.false(x)` 호출 되는 `operator false` 에 선언 된 `T`, 및 `T.&(x, y)` 는 선택한 호출 `operator &`.</span><span class="sxs-lookup"><span data-stu-id="602c5-2316">The operation `x && y` is evaluated as `T.false(x) ? x : T.&(x, y)`, where `T.false(x)` is an invocation of the `operator false` declared in `T`, and `T.&(x, y)` is an invocation of the selected `operator &`.</span></span> <span data-ttu-id="602c5-2317">즉, `x` 먼저 평가 됩니다 및 `operator false` 여부를 확인 하려면 결과에서 호출 되는 `x` false 확실 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2317">In other words, `x` is first evaluated and `operator false` is invoked on the result to determine if `x` is definitely false.</span></span> <span data-ttu-id="602c5-2318">그런 다음 if `x` 확실 하 게 false 연산의 결과 대해 이전에 계산 된 값입니다 `x`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2318">Then, if `x` is definitely false, the result of the operation is the value previously computed for `x`.</span></span> <span data-ttu-id="602c5-2319">이 고, 그렇지 `y` 계산과 선택한 `operator &` 에 대해 이전에 계산 된 값에 호출 됩니다 `x` 의 값을 계산 `y` 작업의 결과 생성 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2319">Otherwise, `y` is evaluated, and the selected `operator &` is invoked on the value previously computed for `x` and the value computed for `y` to produce the result of the operation.</span></span>
*  <span data-ttu-id="602c5-2320">작업 `x || y` 로 평가 됩니다 `T.true(x) ? x : T.|(x, y)`여기서 `T.true(x)` 호출 되는 `operator true` 에 선언 된 `T`, 및 `T.|(x,y)` 는 선택한 호출 `operator|`.</span><span class="sxs-lookup"><span data-stu-id="602c5-2320">The operation `x || y` is evaluated as `T.true(x) ? x : T.|(x, y)`, where `T.true(x)` is an invocation of the `operator true` declared in `T`, and `T.|(x,y)` is an invocation of the selected `operator|`.</span></span> <span data-ttu-id="602c5-2321">즉, `x` 먼저 평가 됩니다 및 `operator true` 여부를 확인 하려면 결과에서 호출 되는 `x` 분명히 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2321">In other words, `x` is first evaluated and `operator true` is invoked on the result to determine if `x` is definitely true.</span></span> <span data-ttu-id="602c5-2322">그런 다음 if `x` 확실 하 게 true 이면 작업의 결과 이전에 계산한 값 `x`.</span><span class="sxs-lookup"><span data-stu-id="602c5-2322">Then, if `x` is definitely true, the result of the operation is the value previously computed for `x`.</span></span> <span data-ttu-id="602c5-2323">이 고, 그렇지 `y` 계산과 선택한 `operator |` 에 대해 이전에 계산 된 값에 호출 됩니다 `x` 의 값을 계산 `y` 작업의 결과 생성 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2323">Otherwise, `y` is evaluated, and the selected `operator |` is invoked on the value previously computed for `x` and the value computed for `y` to produce the result of the operation.</span></span>

<span data-ttu-id="602c5-2324">지정 된 식이 이러한 작업 중 하나로 `x` 이며 한 번 계산만에서 지정 된 식이 `y` 이 없거나 계산 또는 정확히 한 번 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2324">In either of these operations, the expression given by `x` is only evaluated once, and the expression given by `y` is either not evaluated or evaluated exactly once.</span></span>

<span data-ttu-id="602c5-2325">구현 하는 형식의 예 `operator true` 및 `operator false`를 참조 하십시오 [데이터베이스 부울 유형](structs.md#database-boolean-type)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2325">For an example of a type that implements `operator true` and `operator false`, see [Database boolean type](structs.md#database-boolean-type).</span></span>

## <a name="the-null-coalescing-operator"></a><span data-ttu-id="602c5-2326">Null 병합 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2326">The null coalescing operator</span></span>

<span data-ttu-id="602c5-2327">`??` 연산자는 null 병합 연산자 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2327">The `??` operator is called the null coalescing operator.</span></span>

```antlr
null_coalescing_expression
    : conditional_or_expression
    | conditional_or_expression '??' null_coalescing_expression
    ;
```

<span data-ttu-id="602c5-2328">null 병합 식 형식의 `a ?? b` 필요 `a` nullable 형식 또는 참조 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2328">A null coalescing expression of the form `a ?? b` requires `a` to be of a nullable type or reference type.</span></span> <span data-ttu-id="602c5-2329">경우 `a` 가 null이 아닌 결과인 `a ?? b` 됩니다 `a`이 고, 그렇지 않으면 결과 `b`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2329">If `a` is non-null, the result of `a ?? b` is `a`; otherwise, the result is `b`.</span></span> <span data-ttu-id="602c5-2330">평가 하는 작업 `b` 경우에만 `a` null입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2330">The operation evaluates `b` only if `a` is null.</span></span>

<span data-ttu-id="602c5-2331">Null 병합 연산자는 오른쪽 결합성 작업은 오른쪽에서 왼쪽으로 그룹화 되어 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2331">The null coalescing operator is right-associative, meaning that operations are grouped from right to left.</span></span> <span data-ttu-id="602c5-2332">예를 들어, 폼의 식을 `a ?? b ?? c` 로 평가 됩니다 `a ?? (b ?? c)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2332">For example, an expression of the form `a ?? b ?? c` is evaluated as `a ?? (b ?? c)`.</span></span> <span data-ttu-id="602c5-2333">일반적으로 조건에 식 형식의 `E1 ?? E2 ?? ... ?? En` null이 아닌 경우 또는 모든 피연산자가 null 인 경우 null 첫 번째 피연산자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2333">In general terms, an expression of the form `E1 ?? E2 ?? ... ?? En` returns the first of the operands that is non-null, or null if all operands are null.</span></span>

<span data-ttu-id="602c5-2334">식의 형식은 `a ?? b` 는 암시적 변환이 피연산자에 사용할 수에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2334">The type of the expression `a ?? b` depends on which implicit conversions are available on the operands.</span></span> <span data-ttu-id="602c5-2335">유형의 기본 설정 순서에 `a ?? b` 는 `A0`, `A`, 또는 `B`여기서 `A` 의 형식인 `a` (제공한 `a` 형식이), `B` 유형의 `b` ( 제공한 `b` 형식이), 및 `A0` 의 기본 형식인 `A` 경우 `A` 이 nullable 형식이 또는 `A` 그렇지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="602c5-2335">In order of preference, the type of `a ?? b` is `A0`, `A`, or `B`, where `A` is the type of `a` (provided that `a` has a type), `B` is the type of `b` (provided that `b` has a type), and `A0` is the underlying type of `A` if `A` is a nullable type, or `A` otherwise.</span></span> <span data-ttu-id="602c5-2336">특히 `a ?? b` 다음과 같이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2336">Specifically, `a ?? b` is processed as follows:</span></span>

*  <span data-ttu-id="602c5-2337">경우 `A` 있는지 그리고 nullable 형식 또는 참조 형식에서 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2337">If `A` exists and is not a nullable type or a reference type, a compile-time error occurs.</span></span>
*  <span data-ttu-id="602c5-2338">하는 경우 `b` 는 동적 식이 결과 형식은 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2338">If `b` is a dynamic expression, the result type is `dynamic`.</span></span> <span data-ttu-id="602c5-2339">실행 시 `a` 먼저 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2339">At run-time, `a` is first evaluated.</span></span> <span data-ttu-id="602c5-2340">하는 경우 `a` null이 아니면 `a` 를 동적으로 변환 하는이 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2340">If `a` is not null, `a` is converted to dynamic, and this becomes the result.</span></span> <span data-ttu-id="602c5-2341">이 고, 그렇지 `b` 평가 결과가이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2341">Otherwise, `b` is evaluated, and this becomes the result.</span></span>
*  <span data-ttu-id="602c5-2342">그렇지 않은 경우, `A` 존재이 nullable 형식이 고에서 암시적 변환이 존재 `b` 하 `A0`, 결과 형식은 `A0`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2342">Otherwise, if `A` exists and is a nullable type and an implicit conversion exists from `b` to `A0`, the result type is `A0`.</span></span> <span data-ttu-id="602c5-2343">실행 시 `a` 먼저 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2343">At run-time, `a` is first evaluated.</span></span> <span data-ttu-id="602c5-2344">하는 경우 `a` null이 아니면 `a` 입력 래핑이 해제 되어 `A0`,이 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2344">If `a` is not null, `a` is unwrapped to type `A0`, and this becomes the result.</span></span> <span data-ttu-id="602c5-2345">이 고, 그렇지 `b` 평가 되 고 형식으로 변환할 `A0`에이 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2345">Otherwise, `b` is evaluated and converted to type `A0`, and this becomes the result.</span></span>
*  <span data-ttu-id="602c5-2346">그렇지 않은 경우, `A` 존재에서 암시적 변환이 존재 하 고 `b` 하 `A`, 결과 형식은 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2346">Otherwise, if `A` exists and an implicit conversion exists from `b` to `A`, the result type is `A`.</span></span> <span data-ttu-id="602c5-2347">실행 시 `a` 먼저 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2347">At run-time, `a` is first evaluated.</span></span> <span data-ttu-id="602c5-2348">하는 경우 `a` null이 아니면 `a` 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2348">If `a` is not null, `a` becomes the result.</span></span> <span data-ttu-id="602c5-2349">이 고, 그렇지 `b` 평가 되 고 형식으로 변환할 `A`에이 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2349">Otherwise, `b` is evaluated and converted to type `A`, and this becomes the result.</span></span>
*  <span data-ttu-id="602c5-2350">그렇지 않은 경우, `b` 형식이 `B` 에서 암시적 변환이 존재 하 고 `a` 하 `B`, 결과 형식은 `B`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2350">Otherwise, if `b` has a type `B` and an implicit conversion exists from `a` to `B`, the result type is `B`.</span></span> <span data-ttu-id="602c5-2351">실행 시 `a` 먼저 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2351">At run-time, `a` is first evaluated.</span></span> <span data-ttu-id="602c5-2352">하는 경우 `a` null이 아니면 `a` 입력 래핑이 해제 되어 `A0` (경우 `A` 존재 이며 null을 허용) 형식으로 변환 하 고 `B`,이 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2352">If `a` is not null, `a` is unwrapped to type `A0` (if `A` exists and is nullable) and converted to type `B`, and this becomes the result.</span></span> <span data-ttu-id="602c5-2353">그렇지 않으면 `b` 평가 되 고 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2353">Otherwise, `b` is evaluated and becomes the result.</span></span>
*  <span data-ttu-id="602c5-2354">그렇지 않으면 `a` 고 `b` 는 호환 되지 않으며 및 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2354">Otherwise, `a` and `b` are incompatible, and a compile-time error occurs.</span></span>

## <a name="conditional-operator"></a><span data-ttu-id="602c5-2355">조건 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2355">Conditional operator</span></span>

<span data-ttu-id="602c5-2356">`?:` 연산자 조건부 연산자 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2356">The `?:` operator is called the conditional operator.</span></span> <span data-ttu-id="602c5-2357">또한 때때로 삼진 연산자를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2357">It is at times also called the ternary operator.</span></span>

```antlr
conditional_expression
    : null_coalescing_expression
    | null_coalescing_expression '?' expression ':' expression
    ;
```

<span data-ttu-id="602c5-2358">형식의 조건식 `b ? x : y` 먼저 조건을 평가 `b`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2358">A conditional expression of the form `b ? x : y` first evaluates the condition `b`.</span></span> <span data-ttu-id="602c5-2359">그런 다음 if `b` 은 `true`, `x` 평가 되 고 작업의 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2359">Then, if `b` is `true`, `x` is evaluated and becomes the result of the operation.</span></span> <span data-ttu-id="602c5-2360">그렇지 않으면 `y` 평가 되 고 작업의 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2360">Otherwise, `y` is evaluated and becomes the result of the operation.</span></span> <span data-ttu-id="602c5-2361">조건부 식을 모두 것도 계산 하지 않습니다 `x` 고 `y`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2361">A conditional expression never evaluates both `x` and `y`.</span></span>

<span data-ttu-id="602c5-2362">조건 연산자는 오른쪽 결합성 작업은 오른쪽에서 왼쪽으로 그룹화 되어 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2362">The conditional operator is right-associative, meaning that operations are grouped from right to left.</span></span> <span data-ttu-id="602c5-2363">예를 들어, 폼의 식을 `a ? b : c ? d : e` 로 평가 됩니다 `a ? b : (c ? d : e)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2363">For example, an expression of the form `a ? b : c ? d : e` is evaluated as `a ? b : (c ? d : e)`.</span></span>

<span data-ttu-id="602c5-2364">첫 번째 피연산자는 `?:` 연산자를 암시적으로 변환할 수 있는 식 이어야 합니다. `bool`, 또는 구현 하는 형식의 식을 `operator true`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2364">The first operand of the `?:` operator must be an expression that can be implicitly converted to `bool`, or an expression of a type that implements `operator true`.</span></span> <span data-ttu-id="602c5-2365">이러한 요구 사항을 모두 충족 되는 경우 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2365">If neither of these requirements is satisfied, a compile-time error occurs.</span></span>

<span data-ttu-id="602c5-2366">두 번째와 세 번째 피연산자 `x` 하 고 `y`의 `?:` 연산자 조건식의 형식을 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2366">The second and third operands, `x` and `y`, of the `?:` operator control the type of the conditional expression.</span></span>

*  <span data-ttu-id="602c5-2367">하는 경우 `x` 형식이 `X` 하 고 `y` 형식이 `Y` 다음</span><span class="sxs-lookup"><span data-stu-id="602c5-2367">If `x` has type `X` and `y` has type `Y` then</span></span>
   * <span data-ttu-id="602c5-2368">암시적으로 변환 하는 경우 ([암시적 변환을](conversions.md#implicit-conversions))에서 존재 `X` 를 `Y`에서 아니라 `Y` 를 `X`, 다음 `Y` 조건식의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2368">If an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) exists from `X` to `Y`, but not from `Y` to `X`, then `Y` is the type of the conditional expression.</span></span>
   * <span data-ttu-id="602c5-2369">암시적으로 변환 하는 경우 ([암시적 변환을](conversions.md#implicit-conversions))에서 존재 `Y` 를 `X`에서 아니라 `X` 를 `Y`, 다음 `X` 조건식의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2369">If an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) exists from `Y` to `X`, but not from `X` to `Y`, then `X` is the type of the conditional expression.</span></span>
   * <span data-ttu-id="602c5-2370">이 고, 그렇지 확인할 수 없는 식 형식이 없는 및 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2370">Otherwise, no expression type can be determined, and a compile-time error occurs.</span></span>
*  <span data-ttu-id="602c5-2371">경우에 중 하나 `x` 및 `y` 있고 형식 둘 다 `x` 및 `y`의 형식으로 암시적으로 변환할 수 있으면이 조건식의 형식을 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2371">If only one of `x` and `y` has a type, and both `x` and `y`, of are implicitly convertible to that type, then that is the type of the conditional expression.</span></span>
*  <span data-ttu-id="602c5-2372">이 고, 그렇지 확인할 수 없는 식 형식이 없는 및 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2372">Otherwise, no expression type can be determined, and a compile-time error occurs.</span></span>

<span data-ttu-id="602c5-2373">폼의 조건 식의 런타임 처리 `b ? x : y` 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2373">The run-time processing of a conditional expression of the form `b ? x : y` consists of the following steps:</span></span>

*  <span data-ttu-id="602c5-2374">먼저 `b` 계산 및 `bool` 의 값 `b` 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2374">First, `b` is evaluated, and the `bool` value of `b` is determined:</span></span>
   * <span data-ttu-id="602c5-2375">경우의 형식에서 암시적 변환을 `b` 하 `bool` 가 생성이 암시적 변환은 수행 됩니다는 `bool` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2375">If an implicit conversion from the type of `b` to `bool` exists, then this implicit conversion is performed to produce a `bool` value.</span></span>
   * <span data-ttu-id="602c5-2376">이 고, 그렇지는 `operator true` 의 형식에 의해 정의 된 `b` 생성 하기 위해 호출 되는 `bool` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2376">Otherwise, the `operator true` defined by the type of `b` is invoked to produce a `bool` value.</span></span>
*  <span data-ttu-id="602c5-2377">경우는 `bool` 위의 단계에서 생성 하는 값이 `true`, 다음 `x` 평가 되 고 조건부 식의 형식으로 변환할 조건 식의 결과이 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2377">If the `bool` value produced by the step above is `true`, then `x` is evaluated and converted to the type of the conditional expression, and this becomes the result of the conditional expression.</span></span>
*  <span data-ttu-id="602c5-2378">이 고, 그렇지 `y` 평가 되 고 조건부 식의 형식으로 변환 및 조건 식의 결과 이것이 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2378">Otherwise, `y` is evaluated and converted to the type of the conditional expression, and this becomes the result of the conditional expression.</span></span>

## <a name="anonymous-function-expressions"></a><span data-ttu-id="602c5-2379">익명 함수 식</span><span class="sxs-lookup"><span data-stu-id="602c5-2379">Anonymous function expressions</span></span>

<span data-ttu-id="602c5-2380">***익명 함수*** "인라인" 메서드 정의 나타내는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2380">An ***anonymous function*** is an expression that represents an "in-line" method definition.</span></span> <span data-ttu-id="602c5-2381">익명 함수 형식 또는 값 자체에 없지만 호환 되는 대리자 또는 식 트리 형식으로 변환 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2381">An anonymous function does not have a value or type in and of itself, but is convertible to a compatible delegate or expression tree type.</span></span> <span data-ttu-id="602c5-2382">변환의 대상 형식에는 익명 함수 변환의 평가 따라 달라 집니다: 대리자 형식이 인 경우 변환 익명 함수를 정의 하는 메서드를 참조 하는 대리자 값으로 계산 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2382">The evaluation of an anonymous function conversion depends on the target type of the conversion: If it is a delegate type, the conversion evaluates to a delegate value referencing the method which the anonymous function defines.</span></span> <span data-ttu-id="602c5-2383">식 트리 형식을 인 경우 변환 개체 구조와 메서드의 구조를 나타내는 식 트리를 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2383">If it is an expression tree type, the conversion evaluates to an expression tree which represents the structure of the method as an object structure.</span></span>

<span data-ttu-id="602c5-2384">기록을 위해 가지 익명 함수에 두 가지 구문 버전 namely *lambda_expression*s 및 *anonymous_method_expression*s입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2384">For historical reasons there are two syntactic flavors of anonymous functions, namely *lambda_expression*s and *anonymous_method_expression*s.</span></span> <span data-ttu-id="602c5-2385">거의 모든 용도로 *lambda_expression*가 더 간결 하 고 보다 표현 *anonymous_method_expression*언어에 대 한 이전 버전과 호환성 유지 되는 s입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2385">For almost all purposes, *lambda_expression*s are more concise and expressive than *anonymous_method_expression*s, which remain in the language for backwards compatibility.</span></span>

```antlr
lambda_expression
    : anonymous_function_signature '=>' anonymous_function_body
    ;

anonymous_method_expression
    : 'delegate' explicit_anonymous_function_signature? block
    ;

anonymous_function_signature
    : explicit_anonymous_function_signature
    | implicit_anonymous_function_signature
    ;

explicit_anonymous_function_signature
    : '(' explicit_anonymous_function_parameter_list? ')'
    ;

explicit_anonymous_function_parameter_list
    : explicit_anonymous_function_parameter (',' explicit_anonymous_function_parameter)*
    ;

explicit_anonymous_function_parameter
    : anonymous_function_parameter_modifier? type identifier
    ;

anonymous_function_parameter_modifier
    : 'ref'
    | 'out'
    ;

implicit_anonymous_function_signature
    : '(' implicit_anonymous_function_parameter_list? ')'
    | implicit_anonymous_function_parameter
    ;

implicit_anonymous_function_parameter_list
    : implicit_anonymous_function_parameter (',' implicit_anonymous_function_parameter)*
    ;

implicit_anonymous_function_parameter
    : identifier
    ;

anonymous_function_body
    : expression
    | block
    ;
```

<span data-ttu-id="602c5-2386">합니다 `=>` 연산자가 할당 우선 순위가 (`=`)와 같으며 오른쪽 결합성 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2386">The `=>` operator has the same precedence as assignment (`=`) and is right-associative.</span></span>

<span data-ttu-id="602c5-2387">사용 하 여 익명 함수는 `async` 한정자는 비동기 함수 및에 설명 된 규칙을 따릅니다 [반복기](classes.md#iterators)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2387">An anonymous function with the `async` modifier is an async function and follows the rules described in [Iterators](classes.md#iterators).</span></span>

<span data-ttu-id="602c5-2388">형식의 익명 함수의 매개 변수를 *lambda_expression* 명시적 또는 암시적으로 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2388">The parameters of an anonymous function in the form of a *lambda_expression* can be explicitly or implicitly typed.</span></span> <span data-ttu-id="602c5-2389">명시적으로 형식화 된 매개 변수 목록의 각 매개 변수의 형식은 명시적으로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2389">In an explicitly typed parameter list, the type of each parameter is explicitly stated.</span></span> <span data-ttu-id="602c5-2390">익명 함수 발생 하는 컨텍스트에서 유추는 매개 변수의 형식을 암시적으로 형식화 된 매개 변수 목록의-특히 익명 함수 변환 되 면 호환 되는 대리자 형식 또는 형식에서 제공 하는 식 트리 형식 매개 변수 형식 ([익명 함수 변환](conversions.md#anonymous-function-conversions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2390">In an implicitly typed parameter list, the types of the parameters are inferred from the context in which the anonymous function occurs—specifically, when the anonymous function is converted to a compatible delegate type or expression tree type, that type provides the parameter types ([Anonymous function conversions](conversions.md#anonymous-function-conversions)).</span></span>

<span data-ttu-id="602c5-2391">단일, 암시적으로 형식화 된 매개 변수를 사용 하 여 익명 함수에서 매개 변수 목록 괄호를 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2391">In an anonymous function with a single, implicitly typed parameter, the parentheses may be omitted from the parameter list.</span></span> <span data-ttu-id="602c5-2392">즉, 폼의 익명 함수</span><span class="sxs-lookup"><span data-stu-id="602c5-2392">In other words, an anonymous function of the form</span></span>
```csharp
( param ) => expr
```
<span data-ttu-id="602c5-2393">로 축약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2393">can be abbreviated to</span></span>
```csharp
param => expr
```

<span data-ttu-id="602c5-2394">매개 변수 목록이 형식의 익명 함수는 *anonymous_method_expression* 는 선택 사항.</span><span class="sxs-lookup"><span data-stu-id="602c5-2394">The parameter list of an anonymous function in the form of an *anonymous_method_expression* is optional.</span></span> <span data-ttu-id="602c5-2395">주어진 경우 매개 변수를 명시적으로 형식화 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2395">If given, the parameters must be explicitly typed.</span></span> <span data-ttu-id="602c5-2396">익명 함수는 매개 변수를 사용 하 여 대리자 변환할 그렇지 않은 경우 포함 되지 않은 목록 `out` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2396">If not, the anonymous function is convertible to a delegate with any parameter list not containing `out` parameters.</span></span>

<span data-ttu-id="602c5-2397">A *블록* 익명 함수의 본문에 연결할 수 ([끝점 및 연결 가능성](statements.md#end-points-and-reachability)) 익명 함수는 연결할 수 없는 문 내에서 발생 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2397">A *block* body of an anonymous function is reachable ([End points and reachability](statements.md#end-points-and-reachability)) unless the anonymous function occurs inside an unreachable statement.</span></span>

<span data-ttu-id="602c5-2398">익명 함수의 몇 가지 예가 아래 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2398">Some examples of anonymous functions follow below:</span></span>

```csharp
x => x + 1                              // Implicitly typed, expression body
x => { return x + 1; }                  // Implicitly typed, statement body
(int x) => x + 1                        // Explicitly typed, expression body
(int x) => { return x + 1; }            // Explicitly typed, statement body
(x, y) => x * y                         // Multiple parameters
() => Console.WriteLine()               // No parameters
async (t1,t2) => await t1 + await t2    // Async
delegate (int x) { return x + 1; }      // Anonymous method expression
delegate { return 1 + 1; }              // Parameter list omitted
```

<span data-ttu-id="602c5-2399">동작은 *lambda_expression*s 및 *anonymous_method_expression*가 다음 사항을 제외 하 고 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2399">The behavior of *lambda_expression*s and *anonymous_method_expression*s is the same except for the following points:</span></span>

*  <span data-ttu-id="602c5-2400">*anonymous_method_expression*s 허용 매개 변수 목록을 완전히 생략 대리자 매개 변수 값의 모든 목록 형식으로 변환 가능성을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2400">*anonymous_method_expression*s permit the parameter list to be omitted entirely, yielding convertibility to delegate types of any list of value parameters.</span></span>
*  <span data-ttu-id="602c5-2401">*lambda_expression*s 허용 매개 변수 형식을 생략 되어 있지만 유추 *anonymous_method_expression*s 필요한 매개 변수 형식을 명시적으로 지정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2401">*lambda_expression*s permit parameter types to be omitted and inferred whereas *anonymous_method_expression*s require parameter types to be explicitly stated.</span></span>
*  <span data-ttu-id="602c5-2402">본문을 *lambda_expression* 반면 식이나 문 블록을 수 있습니다의 본문을 *anonymous_method_expression* 문 블록 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2402">The body of a *lambda_expression* can be an expression or a statement block whereas the body of an *anonymous_method_expression* must be a statement block.</span></span>
*  <span data-ttu-id="602c5-2403">만 *lambda_expression*호환 식 트리 형식으로의 변환 있습니다 ([식 트리 형식](types.md#expression-tree-types)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2403">Only *lambda_expression*s have conversions to compatible expression tree types ([Expression tree types](types.md#expression-tree-types)).</span></span>

### <a name="anonymous-function-signatures"></a><span data-ttu-id="602c5-2404">익명 함수 시그니처</span><span class="sxs-lookup"><span data-stu-id="602c5-2404">Anonymous function signatures</span></span>

<span data-ttu-id="602c5-2405">선택적 *anonymous_function_signature* 익명 함수는 이름 및 필요에 따라 익명 함수에 대 한 정식 매개 변수의 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2405">The optional *anonymous_function_signature* of an anonymous function defines the names and optionally the types of the formal parameters for the anonymous function.</span></span> <span data-ttu-id="602c5-2406">익명 함수의 매개 변수 범위는 *anonymous_function_body*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2406">The scope of the parameters of the anonymous function is the *anonymous_function_body*.</span></span> <span data-ttu-id="602c5-2407">([범위](basic-concepts.md#scopes)) 매개 변수 목록 (제공 된 경우)와 함께 익명 메서드 본문 구성 선언 공간 ([선언](basic-concepts.md#declarations)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2407">([Scopes](basic-concepts.md#scopes)) Together with the parameter list (if given) the anonymous-method-body constitutes a declaration space ([Declarations](basic-concepts.md#declarations)).</span></span> <span data-ttu-id="602c5-2408">따라서는 지역 변수, 지역 상수 또는 해당 범위에 포함 하는 매개 변수 이름과 일치 하는 익명 함수 매개 변수의 이름에 대 한 컴파일 시간 오류를 *anonymous_method_expression* 또는 *lambda_ 식*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2408">It is thus a compile-time error for the name of a parameter of the anonymous function to match the name of a local variable, local constant or parameter whose scope includes the *anonymous_method_expression* or *lambda_expression*.</span></span>

<span data-ttu-id="602c5-2409">익명 함수에는 *explicit_anonymous_function_signature*, 식 트리 형식과 호환 되는 대리자 형식 집합이 동일한 순서로 동일한 매개 변수 형식 및 한정자에 있는 원하는 언어로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2409">If an anonymous function has an *explicit_anonymous_function_signature*, then the set of compatible delegate types and expression tree types is restricted to those that have the same parameter types and modifiers in the same order.</span></span> <span data-ttu-id="602c5-2410">메서드 그룹 변환 달리 ([메서드 그룹 변환](conversions.md#method-group-conversions)), 익명 함수 매개 변수 형식의 반 공변성은 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2410">In contrast to method group conversions ([Method group conversions](conversions.md#method-group-conversions)), contra-variance of anonymous function parameter types is not supported.</span></span> <span data-ttu-id="602c5-2411">익명 함수에 없는 경우는 *anonymous_function_signature*, 식 트리 형식과 호환 되는 대리자 형식 집합이 없는 것으로 제한 됩니다 `out` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2411">If an anonymous function does not have an *anonymous_function_signature*, then the set of compatible delegate types and expression tree types is restricted to those that have no `out` parameters.</span></span>

<span data-ttu-id="602c5-2412">한 *anonymous_function_signature* 특성 또는 매개 변수 배열에 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2412">Note that an *anonymous_function_signature* cannot include attributes or a parameter array.</span></span> <span data-ttu-id="602c5-2413">그럼에도 불구 하 고는 *anonymous_function_signature* 매개 변수 목록을 가진 매개 변수 배열에 포함 된 대리자 형식과 호환 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2413">Nevertheless, an *anonymous_function_signature* may be compatible with a delegate type whose parameter list contains a parameter array.</span></span>

<span data-ttu-id="602c5-2414">호환 되는, 컴파일 시간에 실패할 수 있습니다 하는 경우에는 식 트리 형식으로 변환 하는 또한 ([식 트리 형식](types.md#expression-tree-types)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2414">Note also that conversion to an expression tree type, even if compatible, may still fail at compile-time ([Expression tree types](types.md#expression-tree-types)).</span></span>

### <a name="anonymous-function-bodies"></a><span data-ttu-id="602c5-2415">익명 함수 본문</span><span class="sxs-lookup"><span data-stu-id="602c5-2415">Anonymous function bodies</span></span>

<span data-ttu-id="602c5-2416">본문 (*식* 하거나 *블록*)는 다음 규칙에 따라 익명 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2416">The body (*expression* or *block*) of an anonymous function is subject to the following rules:</span></span>

*  <span data-ttu-id="602c5-2417">익명 함수 시그니처를 포함 하는 경우에 서명에 지정 된 매개 변수가 본문에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2417">If the anonymous function includes a signature, the parameters specified in the signature are available in the body.</span></span> <span data-ttu-id="602c5-2418">대리자 형식 또는 매개 변수 식 형식을 변환할 수 익명 함수 서명이 없는 경우 ([익명 함수 변환](conversions.md#anonymous-function-conversions)), 하지만 매개 변수를 본문에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2418">If the anonymous function has no signature it can be converted to a delegate type or expression type having parameters ([Anonymous function conversions](conversions.md#anonymous-function-conversions)), but the parameters cannot be accessed in the body.</span></span>
*  <span data-ttu-id="602c5-2419">제외 하 고 `ref` 또는 `out` 바로 바깥쪽의 시그니처 (있는 경우)에 지정 된 매개 변수는 본문의 액세스에 대 한 컴파일 시간 오류 것 익명 함수는 `ref` 또는 `out` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2419">Except for `ref` or `out` parameters specified in the signature (if any) of the nearest enclosing anonymous function, it is a compile-time error for the body to access a `ref` or `out` parameter.</span></span>
*  <span data-ttu-id="602c5-2420">때 유형의 `this` 구조체 형식인 본문에 액세스 하려면 컴파일 시간 오류 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2420">When the type of `this` is a struct type, it is a compile-time error for the body to access `this`.</span></span> <span data-ttu-id="602c5-2421">이 true 인지 여부입니다 액세스 명시적 (에서처럼 `this.x`) 또는 암시적 (에서처럼 `x` 여기서 `x` 구조체의 인스턴스 멤버입니다).</span><span class="sxs-lookup"><span data-stu-id="602c5-2421">This is true whether the access is explicit (as in `this.x`) or implicit (as in `x` where `x` is an instance member of the struct).</span></span> <span data-ttu-id="602c5-2422">이 규칙은 단순히 이러한 액세스를 금지 하 구조체의 멤버에서 멤버 조회 결과 여부에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2422">This rule simply prohibits such access and does not affect whether member lookup results in a member of the struct.</span></span>
*  <span data-ttu-id="602c5-2423">본문이 외부 변수에 액세스할 수 있습니다 ([외부 변수](expressions.md#outer-variables)) 익명 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2423">The body has access to the outer variables ([Outer variables](expressions.md#outer-variables)) of the anonymous function.</span></span> <span data-ttu-id="602c5-2424">외부 변수의 액세스는 시점에 활성 상태인 변수의 인스턴스를 참조 합니다 *lambda_expression* 또는 *anonymous_method_expression* 계산 됩니다 ([평가 익명 함수 식](expressions.md#evaluation-of-anonymous-function-expressions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2424">Access of an outer variable will reference the instance of the variable that is active at the time the *lambda_expression* or *anonymous_method_expression* is evaluated ([Evaluation of anonymous function expressions](expressions.md#evaluation-of-anonymous-function-expressions)).</span></span>
*  <span data-ttu-id="602c5-2425">포함 하도록 본문에 대 한 컴파일 시간 오류가 발생을 `goto` 문을 `break` 문 또는 `continue` 문이 포함 된 익명 함수의 본문 내에서 또는 본문 외부를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2425">It is a compile-time error for the body to contain a `goto` statement, `break` statement, or `continue` statement whose target is outside the body or within the body of a contained anonymous function.</span></span>
*  <span data-ttu-id="602c5-2426">`return` 가장 가까운 바깥쪽 호출에서 제어를 반환 하는 본문에는 문을 바깥쪽 함수 멤버를 제외할 익명 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2426">A `return` statement in the body returns control from an invocation of the nearest enclosing anonymous function, not from the enclosing function member.</span></span> <span data-ttu-id="602c5-2427">에 지정 된 식을 `return` 문은 암시적으로 대리자 형식 또는 식 트리 형식의 반환 형식 이어야 합니다. 가장 가까운 바깥쪽 *lambda_expression* 또는 *anonymous_ method_expression* 변환 됩니다 ([익명 함수 변환](conversions.md#anonymous-function-conversions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2427">An expression specified in a `return` statement must be implicitly convertible to the return type of the delegate type or expression tree type to which the nearest enclosing *lambda_expression* or *anonymous_method_expression* is converted ([Anonymous function conversions](conversions.md#anonymous-function-conversions)).</span></span>

<span data-ttu-id="602c5-2428">평가 및 호출을 통해 익명 함수 보다 다른 블록을 실행 하는 모든 방법은 여부를 명시적으로 지정 되지 않습니다 합니다 *lambda_expression* 또는 *anonymous_method_expression*.</span><span class="sxs-lookup"><span data-stu-id="602c5-2428">It is explicitly unspecified whether there is any way to execute the block of an anonymous function other than through evaluation and invocation of the *lambda_expression* or *anonymous_method_expression*.</span></span> <span data-ttu-id="602c5-2429">특히, 컴파일러가 하나를 취합 하 여 익명 함수를 구현 하도록 선택할 수 또는 이상의 명명 된 메서드 또는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2429">In particular, the compiler may choose to implement an anonymous function by synthesizing one or more named methods or types.</span></span> <span data-ttu-id="602c5-2430">이러한 합성 된 요소의 이름은 컴파일러 사용 하도록 예약 된 양식의 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2430">The names of any such synthesized elements must be of a form reserved for compiler use.</span></span>

### <a name="overload-resolution-and-anonymous-functions"></a><span data-ttu-id="602c5-2431">오버 로드 확인 및 익명 함수</span><span class="sxs-lookup"><span data-stu-id="602c5-2431">Overload resolution and anonymous functions</span></span>

<span data-ttu-id="602c5-2432">익명 함수는 인수 목록의 형식 유추에 참여 하 고 오버 로드를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2432">Anonymous functions in an argument list participate in type inference and overload resolution.</span></span> <span data-ttu-id="602c5-2433">참조 하십시오 [형식 유추](expressions.md#type-inference) 하 고 [오버 로드 확인](expressions.md#overload-resolution) 정확한 규칙에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2433">Please refer to [Type inference](expressions.md#type-inference) and [Overload resolution](expressions.md#overload-resolution) for the exact rules.</span></span>

<span data-ttu-id="602c5-2434">다음 예제에서는 익명 함수 오버 로드 확인에서 효과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2434">The following example illustrates the effect of anonymous functions on overload resolution.</span></span>

```csharp
class ItemList<T>: List<T>
{
    public int Sum(Func<T,int> selector) {
        int sum = 0;
        foreach (T item in this) sum += selector(item);
        return sum;
    }

    public double Sum(Func<T,double> selector) {
        double sum = 0;
        foreach (T item in this) sum += selector(item);
        return sum;
    }
}
```

<span data-ttu-id="602c5-2435">합니다 `ItemList<T>` 클래스에는 두 개의 `Sum` 메서드.</span><span class="sxs-lookup"><span data-stu-id="602c5-2435">The `ItemList<T>` class has two `Sum` methods.</span></span> <span data-ttu-id="602c5-2436">각각을 `selector` 목록 항목에서 합계를 통해 값을 추출 하는 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2436">Each takes a `selector` argument, which extracts the value to sum over from a list item.</span></span> <span data-ttu-id="602c5-2437">추출 된 값을 `int` 또는 `double` 결과 성이 합계와 마찬가지로 하나는 `int` 또는 `double`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2437">The extracted value can be either an `int` or a `double` and the resulting sum is likewise either an `int` or a `double`.</span></span>

<span data-ttu-id="602c5-2438">`Sum` 순서로 세부 선의 목록의 합계를 계산 하려면 메서드 예를 들어 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2438">The `Sum` methods could for example be used to compute sums from a list of detail lines in an order.</span></span>

```csharp
class Detail
{
    public int UnitCount;
    public double UnitPrice;
    ...
}

void ComputeSums() {
    ItemList<Detail> orderDetails = GetOrderDetails(...);
    int totalUnits = orderDetails.Sum(d => d.UnitCount);
    double orderTotal = orderDetails.Sum(d => d.UnitPrice * d.UnitCount);
    ...
}
```

<span data-ttu-id="602c5-2439">첫 번째 호출에서 `orderDetails.Sum`모두 `Sum` 방법이 적합 하므로 익명 함수 `d => d. UnitCount` 둘 다와 호환 되 `Func<Detail,int>` 및 `Func<Detail,double>`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2439">In the first invocation of `orderDetails.Sum`, both `Sum` methods are applicable because the anonymous function `d => d. UnitCount` is compatible with both `Func<Detail,int>` and `Func<Detail,double>`.</span></span> <span data-ttu-id="602c5-2440">그러나 오버 로드 확인의 첫 번째 선택 `Sum` 메서드 때문에 변환 `Func<Detail,int>` 변환 보다 나은 `Func<Detail,double>`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2440">However, overload resolution picks the first `Sum` method because the conversion to `Func<Detail,int>` is better than the conversion to `Func<Detail,double>`.</span></span>

<span data-ttu-id="602c5-2441">두 번째 호출에서 `orderDetails.Sum`, 두 번째만 `Sum` 메서드를 적용할 수 있으므로 익명 함수 `d => d.UnitPrice * d.UnitCount` 형식의 값을 생성 `double`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2441">In the second invocation of `orderDetails.Sum`, only the second `Sum` method is applicable because the anonymous function `d => d.UnitPrice * d.UnitCount` produces a value of type `double`.</span></span> <span data-ttu-id="602c5-2442">따라서 오버 로드 확인에는 두 번째 선택 `Sum` 메서드는 호출에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2442">Thus, overload resolution picks the second `Sum` method for that invocation.</span></span>

### <a name="anonymous-functions-and-dynamic-binding"></a><span data-ttu-id="602c5-2443">익명 함수 및 동적 바인딩</span><span class="sxs-lookup"><span data-stu-id="602c5-2443">Anonymous functions and dynamic binding</span></span>

<span data-ttu-id="602c5-2444">익명 함수는 받는 사람, 인수 또는 동적으로 바인딩된 연산의 피연산자 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2444">An anonymous function cannot be a receiver, argument or operand of a dynamically bound operation.</span></span>

### <a name="outer-variables"></a><span data-ttu-id="602c5-2445">외부 변수</span><span class="sxs-lookup"><span data-stu-id="602c5-2445">Outer variables</span></span>

<span data-ttu-id="602c5-2446">모든 로컬 변수, 값 매개 변수 또는 매개 변수 배열 범위가 포함 된 *lambda_expression* 또는 *anonymous_method_expression* 라고는 ***외부 변수*** 익명 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2446">Any local variable, value parameter, or parameter array whose scope includes the *lambda_expression* or *anonymous_method_expression* is called an ***outer variable*** of the anonymous function.</span></span> <span data-ttu-id="602c5-2447">클래스의 인스턴스 멤버 함수에에서는 `this` 값 매개 변수 값으로 간주 됩니다 및 함수 멤버 내에 포함 된 익명 함수는 외부 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2447">In an instance function member of a class, the `this` value is considered a value parameter and is an outer variable of any anonymous function contained within the function member.</span></span>

#### <a name="captured-outer-variables"></a><span data-ttu-id="602c5-2448">캡처된 외부 변수</span><span class="sxs-lookup"><span data-stu-id="602c5-2448">Captured outer variables</span></span>

<span data-ttu-id="602c5-2449">외부 변수를 익명 함수에서 참조 하는 외부 변수 라고 되었습니다 ***캡처된*** 익명 함수에 의해 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2449">When an outer variable is referenced by an anonymous function, the outer variable is said to have been ***captured*** by the anonymous function.</span></span> <span data-ttu-id="602c5-2450">일반적으로 로컬 변수의 수명은와 연관 된 문이나 블록의 실행 제한 됩니다 ([지역 변수](variables.md#local-variables)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2450">Ordinarily, the lifetime of a local variable is limited to execution of the block or statement with which it is associated ([Local variables](variables.md#local-variables)).</span></span> <span data-ttu-id="602c5-2451">그러나 대리자까지 캡처된 외부 변수의 수명은 이상 확장 또는 익명 함수에서 생성 하는 식 트리 가비지 수집 대상이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2451">However, the lifetime of a captured outer variable is extended at least until the delegate or expression tree created from the anonymous function becomes eligible for garbage collection.</span></span>

<span data-ttu-id="602c5-2452">예제</span><span class="sxs-lookup"><span data-stu-id="602c5-2452">In the example</span></span>
```csharp
using System;

delegate int D();

class Test
{
    static D F() {
        int x = 0;
        D result = () => ++x;
        return result;
    }

    static void Main() {
        D d = F();
        Console.WriteLine(d());
        Console.WriteLine(d());
        Console.WriteLine(d());
    }
}
```
<span data-ttu-id="602c5-2453">지역 변수 `x` 의 수명과 익명 함수에 의해 캡처된 `x` 대리자에서 반환 될 때까지 적어도 확장은 `F` (맨 끝까지 발생 하지 않은 가비지 수집 대상이 될 프로그램)입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2453">the local variable `x` is captured by the anonymous function, and the lifetime of `x` is extended at least until the delegate returned from `F` becomes eligible for garbage collection (which doesn't happen until the very end of the program).</span></span> <span data-ttu-id="602c5-2454">익명 함수를 호출할 때마다 동일한 인스턴스에서 작동 하므로 `x`, 예제의 출력은:</span><span class="sxs-lookup"><span data-stu-id="602c5-2454">Since each invocation of the anonymous function operates on the same instance of `x`, the output of the example is:</span></span>
```
1
2
3
```

<span data-ttu-id="602c5-2455">지역 변수 또는 값 매개 변수는 익명 함수에 의해 캡처된 지역 변수 또는 매개 변수를 더 이상 것으로 간주 됩니다 고정된 변수 이어야 합니다 ([고정 및 고정 되지 않은 변수](unsafe-code.md#fixed-and-moveable-variables)), 대신 것으로 간주 됩니다는 moveable 하지만 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2455">When a local variable or a value parameter is captured by an anonymous function, the local variable or parameter is no longer considered to be a fixed variable ([Fixed and moveable variables](unsafe-code.md#fixed-and-moveable-variables)), but is instead considered to be a moveable variable.</span></span> <span data-ttu-id="602c5-2456">따라서 모든 `unsafe` 캡처된 외부 변수의 주소를 사용 하는 코드를 먼저 사용 해야는 `fixed` 문을 변수를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2456">Thus any `unsafe` code that takes the address of a captured outer variable must first use the `fixed` statement to fix the variable.</span></span>

<span data-ttu-id="602c5-2457">Uncaptured 변수는 달리, 캡처된 지역 변수는 다중 스레드 방식의 실행을 동시에 노출 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2457">Note that unlike an uncaptured variable, a captured local variable can be simultaneously exposed to multiple threads of execution.</span></span>

#### <a name="instantiation-of-local-variables"></a><span data-ttu-id="602c5-2458">지역 변수의 인스턴스화</span><span class="sxs-lookup"><span data-stu-id="602c5-2458">Instantiation of local variables</span></span>

<span data-ttu-id="602c5-2459">지역 변수 것으로 간주 됩니다 ***인스턴스화할*** 실행에서 변수의 범위를 입력 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="602c5-2459">A local variable is considered to be ***instantiated*** when execution enters the scope of the variable.</span></span> <span data-ttu-id="602c5-2460">예를 들어 다음 메서드를 호출 하는 경우, 지역 변수 `x` 인스턴스화되고 세 번 초기화-루프의 각 반복에 한 번씩입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2460">For example, when the following method is invoked, the local variable `x` is instantiated and initialized three times—once for each iteration of the loop.</span></span>

```csharp
static void F() {
    for (int i = 0; i < 3; i++) {
        int x = i * 2 + 1;
        ...
    }
}
```

<span data-ttu-id="602c5-2461">그러나 선언 이동 `x` 루프 결과의 단일 인스턴스화를 외부 `x`:</span><span class="sxs-lookup"><span data-stu-id="602c5-2461">However, moving the declaration of `x` outside the loop results in a single instantiation of `x`:</span></span>
```csharp
static void F() {
    int x;
    for (int i = 0; i < 3; i++) {
        x = i * 2 + 1;
        ...
    }
}
```

<span data-ttu-id="602c5-2462">지역 변수 인스턴스화될 정확한 빈도 확인할 방법이 없기 캡처되지 않습니다 때-있기 때문에 인스턴스화의 수명을 결합 되지 않았는지, 동일한 저장소 위치를 사용 하기만 하면 각 인스턴스화에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2462">When not captured, there is no way to observe exactly how often a local variable is instantiated—because the lifetimes of the instantiations are disjoint, it is possible for each instantiation to simply use the same storage location.</span></span> <span data-ttu-id="602c5-2463">그러나 익명 함수 로컬 변수를 캡처한 인스턴스화 미치는 드러납니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2463">However, when an anonymous function captures a local variable, the effects of instantiation become apparent.</span></span>

<span data-ttu-id="602c5-2464">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2464">The example</span></span>
```csharp
using System;

delegate void D();

class Test
{
    static D[] F() {
        D[] result = new D[3];
        for (int i = 0; i < 3; i++) {
            int x = i * 2 + 1;
            result[i] = () => { Console.WriteLine(x); };
        }
        return result;
    }

    static void Main() {
        foreach (D d in F()) d();
    }
}
```
<span data-ttu-id="602c5-2465">다음 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2465">produces the output:</span></span>
```
1
3
5
```

<span data-ttu-id="602c5-2466">하지만 경우 선언의 `x` 루프 밖으로 이동 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2466">However, when the declaration of `x` is moved outside the loop:</span></span>
```csharp
static D[] F() {
    D[] result = new D[3];
    int x;
    for (int i = 0; i < 3; i++) {
        x = i * 2 + 1;
        result[i] = () => { Console.WriteLine(x); };
    }
    return result;
}
```
<span data-ttu-id="602c5-2467">출력이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2467">the output is:</span></span>
```
5
5
5
```

<span data-ttu-id="602c5-2468">For 루프 반복 변수를 선언 하는 경우 해당 변수 자체는 루프 외부에서 선언으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2468">If a for-loop declares an iteration variable, that variable itself is considered to be declared outside of the loop.</span></span> <span data-ttu-id="602c5-2469">따라서 예제를 캡처하는 반복 변수 자체가 변경 된 경우:</span><span class="sxs-lookup"><span data-stu-id="602c5-2469">Thus, if the example is changed to capture the iteration variable itself:</span></span>

```csharp
static D[] F() {
    D[] result = new D[3];
    for (int i = 0; i < 3; i++) {
        result[i] = () => { Console.WriteLine(i); };
    }
    return result;
}
```
<span data-ttu-id="602c5-2470">출력을 생성 하는 반복 변수의 인스턴스가 하나만 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2470">only one instance of the iteration variable is captured, which produces the output:</span></span>
```
3
3
3
```

<span data-ttu-id="602c5-2471">일부 캡처된 변수를 공유 하면서 다른 별도 인스턴스가 있는 익명 함수 대리자에 대 한 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2471">It is possible for anonymous function delegates to share some captured variables yet have separate instances of others.</span></span> <span data-ttu-id="602c5-2472">예를 들어 경우 `F` 로 변경 됩니다</span><span class="sxs-lookup"><span data-stu-id="602c5-2472">For example, if `F` is changed to</span></span>
```csharp
static D[] F() {
    D[] result = new D[3];
    int x = 0;
    for (int i = 0; i < 3; i++) {
        int y = 0;
        result[i] = () => { Console.WriteLine("{0} {1}", ++x, ++y); };
    }
    return result;
}
```
<span data-ttu-id="602c5-2473">대리자 3 개 캡처의 동일한 인스턴스에 `x` 의 인스턴스를 구분 하지만 `y`, 출력 및:</span><span class="sxs-lookup"><span data-stu-id="602c5-2473">the three delegates capture the same instance of `x` but separate instances of `y`, and the output is:</span></span>
```
1 1
2 1
3 1
```

<span data-ttu-id="602c5-2474">별도 익명 함수는 동일한 인스턴스의 외부 변수를 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2474">Separate anonymous functions can capture the same instance of an outer variable.</span></span> <span data-ttu-id="602c5-2475">예제:</span><span class="sxs-lookup"><span data-stu-id="602c5-2475">In the example:</span></span>
```csharp
using System;

delegate void Setter(int value);

delegate int Getter();

class Test
{
    static void Main() {
        int x = 0;
        Setter s = (int value) => { x = value; };
        Getter g = () => { return x; };
        s(5);
        Console.WriteLine(g());
        s(10);
        Console.WriteLine(g());
    }
}
```
<span data-ttu-id="602c5-2476">두 개의 익명 함수 캡처 지역 변수의 같은 인스턴스 `x`를 수 있으므로 "통신" 해당 변수를 통해.</span><span class="sxs-lookup"><span data-stu-id="602c5-2476">the two anonymous functions capture the same instance of the local variable `x`, and they can thus "communicate" through that variable.</span></span> <span data-ttu-id="602c5-2477">예제의 출력이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2477">The output of the example is:</span></span>
```
5
10
```

### <a name="evaluation-of-anonymous-function-expressions"></a><span data-ttu-id="602c5-2478">익명 함수 식의 평가</span><span class="sxs-lookup"><span data-stu-id="602c5-2478">Evaluation of anonymous function expressions</span></span>

<span data-ttu-id="602c5-2479">익명 함수 `F` 항상 대리자 형식으로 변환 해야 합니다 `D` 또는 식 트리 형식을 `E`에서 직접 또는 대리자 생성 식의 실행을 통해 `new D(F)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2479">An anonymous function `F` must always be converted to a delegate type `D` or an expression tree type `E`, either directly or through the execution of a delegate creation expression `new D(F)`.</span></span> <span data-ttu-id="602c5-2480">이 변환 결과 확인 합니다 익명 함수에 설명 된 대로 [익명 함수 변환](conversions.md#anonymous-function-conversions)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2480">This conversion determines the result of the anonymous function, as described in [Anonymous function conversions](conversions.md#anonymous-function-conversions).</span></span>

## <a name="query-expressions"></a><span data-ttu-id="602c5-2481">쿼리 식</span><span class="sxs-lookup"><span data-stu-id="602c5-2481">Query expressions</span></span>

<span data-ttu-id="602c5-2482">***쿼리 식*** SQL 및 XQuery와 같은 관계형 쿼리와 계층형 쿼리 언어와 유사한는 쿼리용 언어 통합 구문을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2482">***Query expressions*** provide a language integrated syntax for queries that is similar to relational and hierarchical query languages such as SQL and XQuery.</span></span>

```antlr
query_expression
    : from_clause query_body
    ;

from_clause
    : 'from' type? identifier 'in' expression
    ;

query_body
    : query_body_clauses? select_or_group_clause query_continuation?
    ;

query_body_clauses
    : query_body_clause
    | query_body_clauses query_body_clause
    ;

query_body_clause
    : from_clause
    | let_clause
    | where_clause
    | join_clause
    | join_into_clause
    | orderby_clause
    ;

let_clause
    : 'let' identifier '=' expression
    ;

where_clause
    : 'where' boolean_expression
    ;

join_clause
    : 'join' type? identifier 'in' expression 'on' expression 'equals' expression
    ;

join_into_clause
    : 'join' type? identifier 'in' expression 'on' expression 'equals' expression 'into' identifier
    ;

orderby_clause
    : 'orderby' orderings
    ;

orderings
    : ordering (',' ordering)*
    ;

ordering
    : expression ordering_direction?
    ;

ordering_direction
    : 'ascending'
    | 'descending'
    ;

select_or_group_clause
    : select_clause
    | group_clause
    ;

select_clause
    : 'select' expression
    ;

group_clause
    : 'group' expression 'by' expression
    ;

query_continuation
    : 'into' identifier query_body
    ;
```

<span data-ttu-id="602c5-2483">쿼리 식 시작을 `from` 절을 사용 하 여 종료를 `select` 또는 `group` 절.</span><span class="sxs-lookup"><span data-stu-id="602c5-2483">A query expression begins with a `from` clause and ends with either a `select` or `group` clause.</span></span> <span data-ttu-id="602c5-2484">초기 `from` 절 0 개 이상의가 올 수 있습니다 `from`를 `let`를 `where`합니다 `join` 또는 `orderby` 절.</span><span class="sxs-lookup"><span data-stu-id="602c5-2484">The initial `from` clause can be followed by zero or more `from`, `let`, `where`, `join` or `orderby` clauses.</span></span> <span data-ttu-id="602c5-2485">각 `from` 절이 생성기를 소개를 ***범위 변수*** 의 요소를 통해 범위는 한 ***시퀀스***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2485">Each `from` clause is a generator introducing a ***range variable*** which ranges over the elements of a ***sequence***.</span></span> <span data-ttu-id="602c5-2486">각 `let` 절 이전 범위 변수를 사용 하 여 계산 된 값을 나타내는 범위 변수를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2486">Each `let` clause introduces a range variable representing a value computed by means of previous range variables.</span></span> <span data-ttu-id="602c5-2487">각 `where` 절은 결과에서 항목을 제외 하는 필터입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2487">Each `where` clause is a filter that excludes items from the result.</span></span> <span data-ttu-id="602c5-2488">각 `join` 절 일치 하는 쌍을 생성 하는 다른 시퀀스의 키를 사용 하 여 소스 시퀀스의 지정 된 키를 비교 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2488">Each `join` clause compares specified keys of the source sequence with keys of another sequence, yielding matching pairs.</span></span> <span data-ttu-id="602c5-2489">각 `orderby` 절에 지정 된 조건에 따라 항목 다시 정렬 합니다. 최종 `select` 또는 `group` 절의 범위 변수를 기준으로 결과의 셰이프를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2489">Each `orderby` clause reorders items according to specified criteria.The final `select` or `group` clause specifies the shape of the result in terms of the range variables.</span></span> <span data-ttu-id="602c5-2490">마지막으로 `into` 쿼리를 후속 쿼리에 생성기로 한 쿼리의 결과 처리 하 여 "splice" 할 절을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2490">Finally, an `into` clause can be used to "splice" queries by treating the results of one query as a generator in a subsequent query.</span></span>

### <a name="ambiguities-in-query-expressions"></a><span data-ttu-id="602c5-2491">쿼리 식에 모호성이</span><span class="sxs-lookup"><span data-stu-id="602c5-2491">Ambiguities in query expressions</span></span>

<span data-ttu-id="602c5-2492">쿼리 식은 다양 한 "상황에 맞는 키워드", 즉, 특정 컨텍스트에서 특별 한 의미 있는 식별자를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2492">Query expressions contain a number of "contextual keywords", i.e., identifiers that have special meaning in a given context.</span></span> <span data-ttu-id="602c5-2493">특히 이러한 `from`, `where`, `join`, `on`, `equals`를 `into`, `let`를 `orderby`, `ascending`를 `descending`, `select`, `group` 및 `by`.</span><span class="sxs-lookup"><span data-stu-id="602c5-2493">Specifically these are `from`, `where`, `join`, `on`, `equals`, `into`, `let`, `orderby`, `ascending`, `descending`, `select`, `group` and `by`.</span></span> <span data-ttu-id="602c5-2494">키워드 또는 단순한 이름으로 이러한 식별자의 혼합된 사용 하 여 발생 하는 쿼리 식의 모호성을 피하기 위해 이러한 식별자는 쿼리 식 내에서 아무 곳 이나 발생 하는 경우 키워드를 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2494">In order to avoid ambiguities in query expressions caused by mixed use of these identifiers as keywords or simple names, these identifiers are considered keywords when occurring anywhere within a query expression.</span></span>

<span data-ttu-id="602c5-2495">이 작업을 위해 쿼리 식은로 시작 하는 모든 식 "`from identifier`"를 제외한 모든 토큰 뒤 에"`;`","`=`"또는"`,`"입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2495">For this purpose, a query expression is any expression that starts with "`from identifier`" followed by any token except "`;`", "`=`" or "`,`".</span></span>

<span data-ttu-id="602c5-2496">쿼리 식 내에서 식별자로 이러한 단어를 사용 하려면 해당 접두사로 붙일 수 있습니다 "`@`" ([식별자](lexical-structure.md#identifiers)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2496">In order to use these words as identifiers within a query expression, they can be prefixed with "`@`" ([Identifiers](lexical-structure.md#identifiers)).</span></span>

### <a name="query-expression-translation"></a><span data-ttu-id="602c5-2497">쿼리 식 변환</span><span class="sxs-lookup"><span data-stu-id="602c5-2497">Query expression translation</span></span>

<span data-ttu-id="602c5-2498">C# 언어는 쿼리 식의 실행 의미 체계를 지정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2498">The C# language does not specify the execution semantics of query expressions.</span></span> <span data-ttu-id="602c5-2499">쿼리 식을 준수 하는 메서드 호출으로 변환 됩니다 아니라 합니다 *쿼리 식 패턴* ([쿼리 식 패턴](expressions.md#the-query-expression-pattern)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2499">Rather, query expressions are translated into invocations of methods that adhere to the *query expression pattern* ([The query expression pattern](expressions.md#the-query-expression-pattern)).</span></span> <span data-ttu-id="602c5-2500">쿼리 식 라는 메서드 호출으로 변환 됩니다 특히 `Where`, `Select`, `SelectMany`, `Join`, `GroupJoin`를 `OrderBy`, `OrderByDescending`를 `ThenBy`, `ThenByDescending`, `GroupBy`, 및 `Cast`합니다. 이러한 메서드 해야 하는 특정 서명 및 결과 형식을에 설명 된 대로 [쿼리 식 패턴](expressions.md#the-query-expression-pattern)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2500">Specifically, query expressions are translated into invocations of methods named `Where`, `Select`, `SelectMany`, `Join`, `GroupJoin`, `OrderBy`, `OrderByDescending`, `ThenBy`, `ThenByDescending`, `GroupBy`, and `Cast`.These methods are expected to have particular signatures and result types, as described in [The query expression pattern](expressions.md#the-query-expression-pattern).</span></span> <span data-ttu-id="602c5-2501">이러한 메서드는 쿼리 하는 개체의 인스턴스 메서드 또는 외부 개체에 있는 확장 메서드 일 수 있습니다 하 고 구현 하는 쿼리의 실제 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2501">These methods can be instance methods of the object being queried or extension methods that are external to the object, and they implement the actual execution of the query.</span></span>

<span data-ttu-id="602c5-2502">쿼리 식에서 변환 메서드 호출에는 모든 형식 바인딩을 앞에 오는 구문 매핑이 또는 오버 로드 확인을 수행한 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2502">The translation from query expressions to method invocations is a syntactic mapping that occurs before any type binding or overload resolution has been performed.</span></span> <span data-ttu-id="602c5-2503">변환 구문이 올바르지 않습니다 하지만 의미적으로 C# 코드를 생성 하는 보장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2503">The translation is guaranteed to be syntactically correct, but it is not guaranteed to produce semantically correct C# code.</span></span> <span data-ttu-id="602c5-2504">다음 쿼리 식 변환 결과 메서드 호출을 일반 메서드 호출으로 처리 되 고 아니면 메서드는 제네릭 메서드가 없는 경우, 인수 형식이 잘못 된 경우에 예를 들어 오류를 발견할 수 있습니다이 고 형식 유추가 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2504">Following translation of query expressions, the resulting method invocations are processed as regular method invocations, and this may in turn uncover errors, for example if the methods do not exist, if arguments have wrong types, or if the methods are generic and type inference fails.</span></span>

<span data-ttu-id="602c5-2505">쿼리 식 없습니다 추가로 절감할 수 있습니다 때까지 다음 번역을 반복적으로 적용 하 여 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2505">A query expression is processed by repeatedly applying the following translations until no further reductions are possible.</span></span> <span data-ttu-id="602c5-2506">번역은 응용 프로그램의 순서로 나열 됩니다: 각 섹션 가정 하 고 이전 섹션에서 번역을 철저히 수행한 고갈 되 면 섹션은 하지 나중 플러그인 같은 쿼리 식 처리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2506">The translations are listed in order of application: each section assumes that the translations in the preceding sections have been performed exhaustively, and once exhausted, a section will not later be revisited in the processing of the same query expression.</span></span>

<span data-ttu-id="602c5-2507">쿼리 식의 범위 변수를 할당할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2507">Assignment to range variables is not allowed in query expressions.</span></span> <span data-ttu-id="602c5-2508">그러나 C#으로 구현 하므로이 경우에 따라 못할 여기에 제시 된 구문 변환 스키마를 사용 하 여이 제한으로 항상 그렇지는 않습니다 적용 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2508">However a C# implementation is permitted to not always enforce this restriction, since this may sometimes not be possible with the syntactic translation scheme presented here.</span></span>

<span data-ttu-id="602c5-2509">특정 번역 가리키는 투명 식별자를 사용 하 여 범위 변수를 삽입할 `*`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2509">Certain translations inject range variables with transparent identifiers denoted by `*`.</span></span> <span data-ttu-id="602c5-2510">투명 식별자의 특별 한 속성 설명에 대 한 자세한 [투명 식별자](expressions.md#transparent-identifiers)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2510">The special properties of transparent identifiers are discussed further in [Transparent identifiers](expressions.md#transparent-identifiers).</span></span>

#### <a name="select-and-groupby-clauses-with-continuations"></a><span data-ttu-id="602c5-2511">Continuation 사용 하 여 선택 하 고 groupby 절</span><span class="sxs-lookup"><span data-stu-id="602c5-2511">Select and groupby clauses with continuations</span></span>

<span data-ttu-id="602c5-2512">연속 작업을 사용 하 여 쿼리 식</span><span class="sxs-lookup"><span data-stu-id="602c5-2512">A query expression with a continuation</span></span>
```csharp
from ... into x ...
```
<span data-ttu-id="602c5-2513">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2513">is translated into</span></span>
```csharp
from x in ( from ... ) ...
```

<span data-ttu-id="602c5-2514">다음 섹션에서 번역 쿼리 없는 가정 `into` 연속 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2514">The translations in the following sections assume that queries have no `into` continuations.</span></span>

<span data-ttu-id="602c5-2515">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2515">The example</span></span>
```csharp
from c in customers
group c by c.Country into g
select new { Country = g.Key, CustCount = g.Count() }
```
<span data-ttu-id="602c5-2516">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2516">is translated into</span></span>
```csharp
from g in
    from c in customers
    group c by c.Country
select new { Country = g.Key, CustCount = g.Count() }
```
<span data-ttu-id="602c5-2517">최종 번역이</span><span class="sxs-lookup"><span data-stu-id="602c5-2517">the final translation of which is</span></span>
```csharp
customers.
GroupBy(c => c.Country).
Select(g => new { Country = g.Key, CustCount = g.Count() })
```

#### <a name="explicit-range-variable-types"></a><span data-ttu-id="602c5-2518">명시적 범위 변수 형식</span><span class="sxs-lookup"><span data-stu-id="602c5-2518">Explicit range variable types</span></span>

<span data-ttu-id="602c5-2519">`from` 범위 변수 형식을 명시적으로 지정 하는 절</span><span class="sxs-lookup"><span data-stu-id="602c5-2519">A `from` clause that explicitly specifies a range variable type</span></span>
```csharp
from T x in e
```
<span data-ttu-id="602c5-2520">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2520">is translated into</span></span>
```csharp
from x in ( e ) . Cast < T > ( )
```

<span data-ttu-id="602c5-2521">`join` 범위 변수 형식을 명시적으로 지정 하는 절</span><span class="sxs-lookup"><span data-stu-id="602c5-2521">A `join` clause that explicitly specifies a range variable type</span></span>
```
join T x in e on k1 equals k2
```
<span data-ttu-id="602c5-2522">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2522">is translated into</span></span>
```
join x in ( e ) . Cast < T > ( ) on k1 equals k2
```

<span data-ttu-id="602c5-2523">다음 섹션에서 번역은 쿼리 명시적 범위 변수 형식이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2523">The translations in the following sections assume that queries have no explicit range variable types.</span></span>

<span data-ttu-id="602c5-2524">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2524">The example</span></span>
```csharp
from Customer c in customers
where c.City == "London"
select c
```
<span data-ttu-id="602c5-2525">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2525">is translated into</span></span>
```csharp
from c in customers.Cast<Customer>()
where c.City == "London"
select c
```
<span data-ttu-id="602c5-2526">최종 번역이</span><span class="sxs-lookup"><span data-stu-id="602c5-2526">the final translation of which is</span></span>
```csharp
customers.
Cast<Customer>().
Where(c => c.City == "London")
```

<span data-ttu-id="602c5-2527">제네릭이 아닌 구현 하는 컬렉션을 쿼리 하는 데에 명시적 범위 변수의 유형을 `IEnumerable` 제네릭 하지 않고 인터페이스만 `IEnumerable<T>` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2527">Explicit range variable types are useful for querying collections that implement the non-generic `IEnumerable` interface, but not the generic `IEnumerable<T>` interface.</span></span> <span data-ttu-id="602c5-2528">위의 예에서 경우 것 `customers` 형식 이었습니다 `ArrayList`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2528">In the example above, this would be the case if `customers` were of type `ArrayList`.</span></span>

#### <a name="degenerate-query-expressions"></a><span data-ttu-id="602c5-2529">디 제너 레이트 쿼리 식</span><span class="sxs-lookup"><span data-stu-id="602c5-2529">Degenerate query expressions</span></span>

<span data-ttu-id="602c5-2530">폼의 쿼리 식</span><span class="sxs-lookup"><span data-stu-id="602c5-2530">A query expression of the form</span></span>
```csharp
from x in e select x
```
<span data-ttu-id="602c5-2531">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2531">is translated into</span></span>
```csharp
( e ) . Select ( x => x )
```

<span data-ttu-id="602c5-2532">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2532">The example</span></span>
```csharp
from c in customers
select c
```
<span data-ttu-id="602c5-2533">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2533">is translated into</span></span>
```csharp
customers.Select(c => c)
```

<span data-ttu-id="602c5-2534">디 제너 레이트 쿼리 식은 일반적으로 소스 요소를 선택 하는 경우</span><span class="sxs-lookup"><span data-stu-id="602c5-2534">A degenerate query expression is one that trivially selects the elements of the source.</span></span> <span data-ttu-id="602c5-2535">번역의 이후 단계를 해당 원본과를 대체 하 여 다른 변환 단계에서 중복 제거 쿼리에 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2535">A later phase of the translation removes degenerate queries introduced by other translation steps by replacing them with their source.</span></span> <span data-ttu-id="602c5-2536">하지만 것이 중요 쿼리의 결과 되도록 식 되지 소스 개체 자체는 그림 형식 및 id 원본에 쿼리 클라이언트에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2536">It is important however to ensure that the result of a query expression is never the source object itself, as that would reveal the type and identity of the source to the client of the query.</span></span> <span data-ttu-id="602c5-2537">이 단계에서 명시적으로 호출 하 여 소스 코드에서 직접 작성 하는 중복 제거 쿼리를 보호 하는 따라서 `Select` 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2537">Therefore this step protects degenerate queries written directly in source code by explicitly calling `Select` on the source.</span></span> <span data-ttu-id="602c5-2538">구현자 그러면 `Select` 및 이러한 메서드는 원본 개체 자체를 반환 하지 않도록 하기 위해 다른 쿼리 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2538">It is then up to the implementers of `Select` and other query operators to ensure that these methods never return the source object itself.</span></span>

#### <a name="from-let-where-join-and-orderby-clauses"></a><span data-ttu-id="602c5-2539">, let, where,: 조인 및 orderby 절</span><span class="sxs-lookup"><span data-stu-id="602c5-2539">From, let, where, join and orderby clauses</span></span>

<span data-ttu-id="602c5-2540">두 번째 쿼리 식을 `from` 뒤에 절을 `select` 절</span><span class="sxs-lookup"><span data-stu-id="602c5-2540">A query expression with a second `from` clause followed by a `select` clause</span></span>
```csharp
from x1 in e1
from x2 in e2
select v
```
<span data-ttu-id="602c5-2541">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2541">is translated into</span></span>
```csharp
( e1 ) . SelectMany( x1 => e2 , ( x1 , x2 ) => v )
```

<span data-ttu-id="602c5-2542">두 번째 쿼리 식을 `from` 절 뒤에 것 이외의 `select` 절:</span><span class="sxs-lookup"><span data-stu-id="602c5-2542">A query expression with a second `from` clause followed by something other than a `select` clause:</span></span>

```csharp
from x1 in e1
from x2 in e2
...
```
<span data-ttu-id="602c5-2543">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2543">is translated into</span></span>
```csharp
from * in ( e1 ) . SelectMany( x1 => e2 , ( x1 , x2 ) => new { x1 , x2 } )
...
```

<span data-ttu-id="602c5-2544">쿼리 식에는 `let` 절</span><span class="sxs-lookup"><span data-stu-id="602c5-2544">A query expression with a `let` clause</span></span>
```csharp
from x in e
let y = f
...
```
<span data-ttu-id="602c5-2545">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2545">is translated into</span></span>
```csharp
from * in ( e ) . Select ( x => new { x , y = f } )
...
```

<span data-ttu-id="602c5-2546">쿼리 식에는 `where` 절</span><span class="sxs-lookup"><span data-stu-id="602c5-2546">A query expression with a `where` clause</span></span>
```csharp
from x in e
where f
...
```
<span data-ttu-id="602c5-2547">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2547">is translated into</span></span>
```csharp
from x in ( e ) . Where ( x => f )
...
```

<span data-ttu-id="602c5-2548">쿼리 식에는 `join` 없이 절을 `into` 뒤에 `select` 절</span><span class="sxs-lookup"><span data-stu-id="602c5-2548">A query expression with a `join` clause without an `into` followed by a `select` clause</span></span>
```csharp
from x1 in e1
join x2 in e2 on k1 equals k2
select v
```
<span data-ttu-id="602c5-2549">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2549">is translated into</span></span>
```csharp
( e1 ) . Join( e2 , x1 => k1 , x2 => k2 , ( x1 , x2 ) => v )
```

<span data-ttu-id="602c5-2550">쿼리 식에는 `join` 절 없이 `into` 것 이외의 뒤를 `select` 절</span><span class="sxs-lookup"><span data-stu-id="602c5-2550">A query expression with a `join` clause without an `into` followed by something other than a `select` clause</span></span>
```csharp
from x1 in e1
join x2 in e2 on k1 equals k2
...
```
<span data-ttu-id="602c5-2551">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2551">is translated into</span></span>
```csharp
from * in ( e1 ) . Join( e2 , x1 => k1 , x2 => k2 , ( x1 , x2 ) => new { x1 , x2 })
...
```

<span data-ttu-id="602c5-2552">쿼리 식에는 `join` 절을 `into` 뒤에 `select` 절</span><span class="sxs-lookup"><span data-stu-id="602c5-2552">A query expression with a `join` clause with an `into` followed by a `select` clause</span></span>
```csharp
from x1 in e1
join x2 in e2 on k1 equals k2 into g
select v
```
<span data-ttu-id="602c5-2553">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2553">is translated into</span></span>
```csharp
( e1 ) . GroupJoin( e2 , x1 => k1 , x2 => k2 , ( x1 , g ) => v )
```

<span data-ttu-id="602c5-2554">쿼리 식에는 `join` 절을 `into` 것 이외의 뒤를 `select` 절</span><span class="sxs-lookup"><span data-stu-id="602c5-2554">A query expression with a `join` clause with an `into` followed by something other than a `select` clause</span></span>
```csharp
from x1 in e1
join x2 in e2 on k1 equals k2 into g
...
```
<span data-ttu-id="602c5-2555">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2555">is translated into</span></span>
```csharp
from * in ( e1 ) . GroupJoin( e2 , x1 => k1 , x2 => k2 , ( x1 , g ) => new { x1 , g })
...
```

<span data-ttu-id="602c5-2556">쿼리 식에는 `orderby` 절</span><span class="sxs-lookup"><span data-stu-id="602c5-2556">A query expression with an `orderby` clause</span></span>
```csharp
from x in e
orderby k1 , k2 , ..., kn
...
```
<span data-ttu-id="602c5-2557">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2557">is translated into</span></span>
```csharp
from x in ( e ) . 
OrderBy ( x => k1 ) . 
ThenBy ( x => k2 ) .
... .
ThenBy ( x => kn )
...
```

<span data-ttu-id="602c5-2558">절 지정 하는 경우 순서는 `descending` 방향 표시기, 호출 `OrderByDescending` 또는 `ThenByDescending` 대신 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2558">If an ordering clause specifies a `descending` direction indicator, an invocation of `OrderByDescending` or `ThenByDescending` is produced instead.</span></span>

<span data-ttu-id="602c5-2559">번역 있는지 가정 없음 `let`, `where`, `join` 또는 `orderby` 절 및는 하나의 초기 `from` 각 쿼리 식 절.</span><span class="sxs-lookup"><span data-stu-id="602c5-2559">The following translations assume that there are no `let`, `where`, `join` or `orderby` clauses, and no more than the one initial `from` clause in each query expression.</span></span>

<span data-ttu-id="602c5-2560">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2560">The example</span></span>
```csharp
from c in customers
from o in c.Orders
select new { c.Name, o.OrderID, o.Total }
```
<span data-ttu-id="602c5-2561">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2561">is translated into</span></span>
```csharp
customers.
SelectMany(c => c.Orders,
     (c,o) => new { c.Name, o.OrderID, o.Total }
)
```

<span data-ttu-id="602c5-2562">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2562">The example</span></span>
```csharp
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.OrderID, o.Total }
```
<span data-ttu-id="602c5-2563">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2563">is translated into</span></span>
```csharp
from * in customers.
    SelectMany(c => c.Orders, (c,o) => new { c, o })
orderby o.Total descending
select new { c.Name, o.OrderID, o.Total }
```
<span data-ttu-id="602c5-2564">최종 번역이</span><span class="sxs-lookup"><span data-stu-id="602c5-2564">the final translation of which is</span></span>
```csharp
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(x => x.o.Total).
Select(x => new { x.c.Name, x.o.OrderID, x.o.Total })
```
<span data-ttu-id="602c5-2565">여기서 `x` 즉 액세스할 수 없는 컴파일러에서 생성 된 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2565">where `x` is a compiler generated identifier that is otherwise invisible and inaccessible.</span></span>

<span data-ttu-id="602c5-2566">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2566">The example</span></span>
```csharp
from o in orders
let t = o.Details.Sum(d => d.UnitPrice * d.Quantity)
where t >= 1000
select new { o.OrderID, Total = t }
```
<span data-ttu-id="602c5-2567">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2567">is translated into</span></span>
```csharp
from * in orders.
    Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) })
where t >= 1000 
select new { o.OrderID, Total = t }
```
<span data-ttu-id="602c5-2568">최종 번역이</span><span class="sxs-lookup"><span data-stu-id="602c5-2568">the final translation of which is</span></span>
```csharp
orders.
Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) }).
Where(x => x.t >= 1000).
Select(x => new { x.o.OrderID, Total = x.t })
```
<span data-ttu-id="602c5-2569">여기서 `x` 즉 액세스할 수 없는 컴파일러에서 생성 된 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2569">where `x` is a compiler generated identifier that is otherwise invisible and inaccessible.</span></span>

<span data-ttu-id="602c5-2570">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2570">The example</span></span>
```csharp
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
select new { c.Name, o.OrderDate, o.Total }
```
<span data-ttu-id="602c5-2571">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2571">is translated into</span></span>
```csharp
customers.Join(orders, c => c.CustomerID, o => o.CustomerID,
    (c, o) => new { c.Name, o.OrderDate, o.Total })
```

<span data-ttu-id="602c5-2572">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2572">The example</span></span>
```csharp
from c in customers
join o in orders on c.CustomerID equals o.CustomerID into co
let n = co.Count()
where n >= 10
select new { c.Name, OrderCount = n }
```
<span data-ttu-id="602c5-2573">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2573">is translated into</span></span>
```csharp
from * in customers.
    GroupJoin(orders, c => c.CustomerID, o => o.CustomerID,
        (c, co) => new { c, co })
let n = co.Count()
where n >= 10 
select new { c.Name, OrderCount = n }
```
<span data-ttu-id="602c5-2574">최종 번역이</span><span class="sxs-lookup"><span data-stu-id="602c5-2574">the final translation of which is</span></span>
```csharp
customers.
GroupJoin(orders, c => c.CustomerID, o => o.CustomerID,
    (c, co) => new { c, co }).
Select(x => new { x, n = x.co.Count() }).
Where(y => y.n >= 10).
Select(y => new { y.x.c.Name, OrderCount = y.n)
```
<span data-ttu-id="602c5-2575">여기서 `x` 및 `y` 액세스할 수 없는 고 그렇지 않은 컴파일러에서 생성 된 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2575">where `x` and `y` are compiler generated identifiers that are otherwise invisible and inaccessible.</span></span>

<span data-ttu-id="602c5-2576">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2576">The example</span></span>
```csharp
from o in orders
orderby o.Customer.Name, o.Total descending
select o
```
<span data-ttu-id="602c5-2577">최종 번역에</span><span class="sxs-lookup"><span data-stu-id="602c5-2577">has the final translation</span></span>
```csharp
orders.
OrderBy(o => o.Customer.Name).
ThenByDescending(o => o.Total)
```

#### <a name="select-clauses"></a><span data-ttu-id="602c5-2578">Select 절</span><span class="sxs-lookup"><span data-stu-id="602c5-2578">Select clauses</span></span>

<span data-ttu-id="602c5-2579">폼의 쿼리 식</span><span class="sxs-lookup"><span data-stu-id="602c5-2579">A query expression of the form</span></span>
```csharp
from x in e select v
```
<span data-ttu-id="602c5-2580">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2580">is translated into</span></span>
```csharp
( e ) . Select ( x => v )
```
<span data-ttu-id="602c5-2581">v 식별자 인 경우 제외 x 번역은 단순히</span><span class="sxs-lookup"><span data-stu-id="602c5-2581">except when v is the identifier x, the translation is simply</span></span>
```csharp
( e )
```

<span data-ttu-id="602c5-2582">예</span><span class="sxs-lookup"><span data-stu-id="602c5-2582">For example</span></span>
```csharp
from c in customers.Where(c => c.City == "London")
select c
```
<span data-ttu-id="602c5-2583">단순히 변환</span><span class="sxs-lookup"><span data-stu-id="602c5-2583">is simply translated into</span></span>
```csharp
customers.Where(c => c.City == "London")
```

#### <a name="groupby-clauses"></a><span data-ttu-id="602c5-2584">Groupby 절</span><span class="sxs-lookup"><span data-stu-id="602c5-2584">Groupby clauses</span></span>

<span data-ttu-id="602c5-2585">폼의 쿼리 식</span><span class="sxs-lookup"><span data-stu-id="602c5-2585">A query expression of the form</span></span>
```csharp
from x in e group v by k
```
<span data-ttu-id="602c5-2586">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2586">is translated into</span></span>
```csharp
( e ) . GroupBy ( x => k , x => v )
```
<span data-ttu-id="602c5-2587">v 식별자 인 경우 제외 x 번역이</span><span class="sxs-lookup"><span data-stu-id="602c5-2587">except when v is the identifier x, the translation is</span></span>
```csharp
( e ) . GroupBy ( x => k )
```

<span data-ttu-id="602c5-2588">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2588">The example</span></span>
```csharp
from c in customers
group c.Name by c.Country
```
<span data-ttu-id="602c5-2589">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2589">is translated into</span></span>
```csharp
customers.
GroupBy(c => c.Country, c => c.Name)
```

#### <a name="transparent-identifiers"></a><span data-ttu-id="602c5-2590">투명 식별자</span><span class="sxs-lookup"><span data-stu-id="602c5-2590">Transparent identifiers</span></span>

<span data-ttu-id="602c5-2591">특정 번역 삽입할 범위 변수와 ***투명 식별자*** 가리키는 `*`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2591">Certain translations inject range variables with ***transparent identifiers*** denoted by `*`.</span></span> <span data-ttu-id="602c5-2592">투명 식별자는 적절 한 언어 기능이; 하지 않습니다. 쿼리 식 변환 프로세스에서 중간 단계로 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2592">Transparent identifiers are not a proper language feature; they exist only as an intermediate step in the query expression translation process.</span></span>

<span data-ttu-id="602c5-2593">쿼리 변환 투명 식별자를 삽입 하는 경우 변환 단계 투명 식별자 익명 함수 및 익명 개체 이니셜라이저에 전파 추가.</span><span class="sxs-lookup"><span data-stu-id="602c5-2593">When a query translation injects a transparent identifier, further translation steps propagate the transparent identifier into anonymous functions and anonymous object initializers.</span></span> <span data-ttu-id="602c5-2594">이러한 컨텍스트 투명 식별자에는 다음 동작:</span><span class="sxs-lookup"><span data-stu-id="602c5-2594">In those contexts, transparent identifiers have the following behavior:</span></span>

*  <span data-ttu-id="602c5-2595">익명 함수에 매개 변수로 식별자를 투명 하 게 발생 하면 연결 된 익명 형식의 멤버는 자동으로 범위 내에서에 익명 함수의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2595">When a transparent identifier occurs as a parameter in an anonymous function, the members of the associated anonymous type are automatically in scope in the body of the anonymous function.</span></span>
*  <span data-ttu-id="602c5-2596">투명 식별자 멤버가 범위의 경우 해당 멤버의 멤버는 범위의 도입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2596">When a member with a transparent identifier is in scope, the members of that member are in scope as well.</span></span>
*  <span data-ttu-id="602c5-2597">투명 식별자는 익명 개체 이니셜라이저에서 멤버 선언으로 발생 하면 투명 식별자 멤버가 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2597">When a transparent identifier occurs as a member declarator in an anonymous object initializer, it introduces a member with a transparent identifier.</span></span>
*  <span data-ttu-id="602c5-2598">위에서 설명한 변환 단계에서는 투명 한 식별자는 항상 단일 개체의 구성원으로 여러 개의 범위 변수를 캡처의 의도 사용 하 여 익명 형식과 함께 도입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2598">In the translation steps described above, transparent identifiers are always introduced together with anonymous types, with the intent of capturing multiple range variables as members of a single object.</span></span> <span data-ttu-id="602c5-2599">익명 형식 보다 다른 메커니즘을 여러 개의 범위 변수를 함께 그룹화 하는 데 C#의 구현을 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2599">An implementation of C# is permitted to use a different mechanism than anonymous types to group together multiple range variables.</span></span> <span data-ttu-id="602c5-2600">다음 변환 예제에서는 무명 형식을 사용 하 고 투명도 식별자 표시 가정 바로 변환 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2600">The following translation examples assume that anonymous types are used, and show how transparent identifiers can be translated away.</span></span>

<span data-ttu-id="602c5-2601">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2601">The example</span></span>
```csharp
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.Total }
```
<span data-ttu-id="602c5-2602">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2602">is translated into</span></span>
```csharp
from * in customers.
    SelectMany(c => c.Orders, (c,o) => new { c, o })
orderby o.Total descending
select new { c.Name, o.Total }
```

<span data-ttu-id="602c5-2603">변환 추가</span><span class="sxs-lookup"><span data-stu-id="602c5-2603">which is further translated into</span></span>
```csharp
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(* => o.Total).
Select(* => new { c.Name, o.Total })
```
<span data-ttu-id="602c5-2604">투명 식별자 지워진 경우와 동일</span><span class="sxs-lookup"><span data-stu-id="602c5-2604">which, when transparent identifiers are erased, is equivalent to</span></span>
```csharp
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(x => x.o.Total).
Select(x => new { x.c.Name, x.o.Total })
```
<span data-ttu-id="602c5-2605">여기서 `x` 즉 액세스할 수 없는 컴파일러에서 생성 된 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2605">where `x` is a compiler generated identifier that is otherwise invisible and inaccessible.</span></span>

<span data-ttu-id="602c5-2606">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="602c5-2606">The example</span></span>
```csharp
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
join d in details on o.OrderID equals d.OrderID
join p in products on d.ProductID equals p.ProductID
select new { c.Name, o.OrderDate, p.ProductName }
```
<span data-ttu-id="602c5-2607">로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2607">is translated into</span></span>
```csharp
from * in customers.
    Join(orders, c => c.CustomerID, o => o.CustomerID, 
        (c, o) => new { c, o })
join d in details on o.OrderID equals d.OrderID
join p in products on d.ProductID equals p.ProductID
select new { c.Name, o.OrderDate, p.ProductName }
```
<span data-ttu-id="602c5-2608">축소는 추가</span><span class="sxs-lookup"><span data-stu-id="602c5-2608">which is further reduced to</span></span>
```csharp
customers.
Join(orders, c => c.CustomerID, o => o.CustomerID, (c, o) => new { c, o }).
Join(details, * => o.OrderID, d => d.OrderID, (*, d) => new { *, d }).
Join(products, * => d.ProductID, p => p.ProductID, (*, p) => new { *, p }).
Select(* => new { c.Name, o.OrderDate, p.ProductName })
```
<span data-ttu-id="602c5-2609">최종 번역이</span><span class="sxs-lookup"><span data-stu-id="602c5-2609">the final translation of which is</span></span>
```csharp
customers.
Join(orders, c => c.CustomerID, o => o.CustomerID,
    (c, o) => new { c, o }).
Join(details, x => x.o.OrderID, d => d.OrderID,
    (x, d) => new { x, d }).
Join(products, y => y.d.ProductID, p => p.ProductID,
    (y, p) => new { y, p }).
Select(z => new { z.y.x.c.Name, z.y.x.o.OrderDate, z.p.ProductName })
```
<span data-ttu-id="602c5-2610">여기서 `x`, `y`, 및 `z` 액세스할 수 없는 고 그렇지 않은 컴파일러에서 생성 된 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2610">where `x`, `y`, and `z` are compiler generated identifiers that are otherwise invisible and inaccessible.</span></span>

### <a name="the-query-expression-pattern"></a><span data-ttu-id="602c5-2611">쿼리 식 패턴</span><span class="sxs-lookup"><span data-stu-id="602c5-2611">The query expression pattern</span></span>

<span data-ttu-id="602c5-2612">합니다 ***쿼리 식 패턴*** 패턴 형식 쿼리 식을 지원 하기 위해 구현할 수 있는 메서드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2612">The ***Query expression pattern*** establishes a pattern of methods that types can implement to support query expressions.</span></span> <span data-ttu-id="602c5-2613">쿼리 식 구문 매핑을 통해 메서드 호출으로 변환 됩니다, 때문에 형식 쿼리 식 패턴을 구현 하는 방법에 유연성을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2613">Because query expressions are translated to method invocations by means of a syntactic mapping, types have considerable flexibility in how they implement the query expression pattern.</span></span> <span data-ttu-id="602c5-2614">예를 들어 패턴의 메서드를 구현할 수 있습니다 인스턴스 메서드 또는 확장 메서드로 둘 다 동일한 호출 구문을 이므로 익명 함수 둘 다으로 변환할 수 없으므로 메서드를 대리자 또는 식 트리를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2614">For example, the methods of the pattern can be implemented as instance methods or as extension methods because the two have the same invocation syntax, and the methods can request delegates or expression trees because anonymous functions are convertible to both.</span></span>

<span data-ttu-id="602c5-2615">제네릭 형식의 권장 되는 모양을 `C<T>` 는 지원의 쿼리 식 패턴은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2615">The recommended shape of a generic type `C<T>` that supports the query expression pattern is shown below.</span></span> <span data-ttu-id="602c5-2616">제네릭 형식 매개 변수 및 결과 형식 간의 적절 한 관계를 보여 주기 위해는 하지만 제네릭이 아닌 형식에 대 한 패턴을 구현 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2616">A generic type is used in order to illustrate the proper relationships between parameter and result types, but it is possible to implement the pattern for non-generic types as well.</span></span>

```csharp
delegate R Func<T1,R>(T1 arg1);

delegate R Func<T1,T2,R>(T1 arg1, T2 arg2);

class C
{
    public C<T> Cast<T>();
}

class C<T> : C
{
    public C<T> Where(Func<T,bool> predicate);

    public C<U> Select<U>(Func<T,U> selector);

    public C<V> SelectMany<U,V>(Func<T,C<U>> selector,
        Func<T,U,V> resultSelector);

    public C<V> Join<U,K,V>(C<U> inner, Func<T,K> outerKeySelector,
        Func<U,K> innerKeySelector, Func<T,U,V> resultSelector);

    public C<V> GroupJoin<U,K,V>(C<U> inner, Func<T,K> outerKeySelector,
        Func<U,K> innerKeySelector, Func<T,C<U>,V> resultSelector);

    public O<T> OrderBy<K>(Func<T,K> keySelector);

    public O<T> OrderByDescending<K>(Func<T,K> keySelector);

    public C<G<K,T>> GroupBy<K>(Func<T,K> keySelector);

    public C<G<K,E>> GroupBy<K,E>(Func<T,K> keySelector,
        Func<T,E> elementSelector);
}

class O<T> : C<T>
{
    public O<T> ThenBy<K>(Func<T,K> keySelector);

    public O<T> ThenByDescending<K>(Func<T,K> keySelector);
}

class G<K,T> : C<T>
{
    public K Key { get; }
}
```

<span data-ttu-id="602c5-2617">위의 메서드는 제네릭 대리자 형식을 사용 `Func<T1,R>` 및 `Func<T1,T2,R>`, 이러한 수 원활 하 게 형식을 사용 하는 다른 대리자 또는 식 트리에서 매개 변수 및 결과 형식에서 동일한 관계 있지만.</span><span class="sxs-lookup"><span data-stu-id="602c5-2617">The methods above use the generic delegate types `Func<T1,R>` and `Func<T1,T2,R>`, but they could equally well have used other delegate or expression tree types with the same relationships in parameter and result types.</span></span>

<span data-ttu-id="602c5-2618">권장 되는 관계를 확인할 수 있습니다 `C<T>` 및 `O<T>` 되도록 하는 합니다 `ThenBy` 및 `ThenByDescending` 메서드를 결과에 대해서만 사용할 수는 `OrderBy` 또는 `OrderByDescending`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2618">Notice the recommended relationship between `C<T>` and `O<T>` which ensures that the `ThenBy` and `ThenByDescending` methods are available only on the result of an `OrderBy` or `OrderByDescending`.</span></span> <span data-ttu-id="602c5-2619">또한 결과의 권장 되는 모양을 확인할 수 있습니다 `GroupBy` -시퀀스의 시퀀스를 각 내부 시퀀스에 추가 `Key` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2619">Also notice the recommended shape of the result of `GroupBy` -- a sequence of sequences, where each inner sequence has an additional `Key` property.</span></span>

<span data-ttu-id="602c5-2620">합니다 `System.Linq` 네임 스페이스를 구현 하는 모든 형식에 대 한 쿼리 연산자 패턴의 구현을 제공 합니다 `System.Collections.Generic.IEnumerable<T>` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2620">The `System.Linq` namespace provides an implementation of the query operator pattern for any type that implements the `System.Collections.Generic.IEnumerable<T>` interface.</span></span>

## <a name="assignment-operators"></a><span data-ttu-id="602c5-2621">대입 연산자</span><span class="sxs-lookup"><span data-stu-id="602c5-2621">Assignment operators</span></span>

<span data-ttu-id="602c5-2622">대입 연산자는 변수, 속성, 이벤트 또는 인덱서 요소를 새 값을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2622">The assignment operators assign a new value to a variable, a property, an event, or an indexer element.</span></span>

```antlr
assignment
    : unary_expression assignment_operator expression
    ;

assignment_operator
    : '='
    | '+='
    | '-='
    | '*='
    | '/='
    | '%='
    | '&='
    | '|='
    | '^='
    | '<<='
    | right_shift_assignment
    ;
```

<span data-ttu-id="602c5-2623">할당의 왼쪽된 피연산자는 변수, 속성 액세스, 인덱서 액세스, 또는 이벤트 액세스로 분류 되는 식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2623">The left operand of an assignment must be an expression classified as a variable, a property access, an indexer access, or an event access.</span></span>

<span data-ttu-id="602c5-2624">합니다 `=` 연산자를 호출 합니다 ***단순 할당 연산자***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2624">The `=` operator is called the ***simple assignment operator***.</span></span> <span data-ttu-id="602c5-2625">오른쪽 피연산자의 값은 왼쪽된 피연산자가 지정 된 변수, 속성 또는 인덱서 요소에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2625">It assigns the value of the right operand to the variable, property, or indexer element given by the left operand.</span></span> <span data-ttu-id="602c5-2626">단순 할당 연산자의 왼쪽된 피연산자 이벤트 액세스 되지 않을 수 있습니다 (에 설명 된 대로 except [필드와 유사한 이벤트](classes.md#field-like-events)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2626">The left operand of the simple assignment operator may not be an event access (except as described in [Field-like events](classes.md#field-like-events)).</span></span> <span data-ttu-id="602c5-2627">단순 할당 연산자에서 설명한 [단순 할당](expressions.md#simple-assignment)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2627">The simple assignment operator is described in [Simple assignment](expressions.md#simple-assignment).</span></span>

<span data-ttu-id="602c5-2628">이외의 할당 연산자는 `=` 연산자 라고 합니다 ***복합 할당 연산자***합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2628">The assignment operators other than the `=` operator are called the ***compound assignment operators***.</span></span> <span data-ttu-id="602c5-2629">이러한 연산자는 두 피연산자에 지정 된 작업을 수행 하 고 왼쪽 피연산자로 지정 된 변수, 속성 또는 인덱서 요소 결과 값을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2629">These operators perform the indicated operation on the two operands, and then assign the resulting value to the variable, property, or indexer element given by the left operand.</span></span> <span data-ttu-id="602c5-2630">복합 할당 연산자에 나와 [복합 할당](expressions.md#compound-assignment)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2630">The compound assignment operators are described in [Compound assignment](expressions.md#compound-assignment).</span></span>

<span data-ttu-id="602c5-2631">합니다 `+=` 및 `-=` 왼쪽 피연산자로 이벤트 액세스 식 사용 하 여 연산자 라고 합니다 *이벤트 대입 연산자*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2631">The `+=` and `-=` operators with an event access expression as the left operand are called the *event assignment operators*.</span></span> <span data-ttu-id="602c5-2632">왼쪽된 피연산자와 기타 할당 연산자는 이벤트 액세스를 사용 하 여 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2632">No other assignment operator is valid with an event access as the left operand.</span></span> <span data-ttu-id="602c5-2633">이벤트 대입 연산자에 나와 [이벤트 할당](expressions.md#event-assignment)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2633">The event assignment operators are described in [Event assignment](expressions.md#event-assignment).</span></span>

<span data-ttu-id="602c5-2634">대입 연산자는 오른쪽 결합성 작업은 오른쪽에서 왼쪽으로 그룹화 되어 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2634">The assignment operators are right-associative, meaning that operations are grouped from right to left.</span></span> <span data-ttu-id="602c5-2635">예를 들어, 폼의 식을 `a = b = c` 로 평가 됩니다 `a = (b = c)`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2635">For example, an expression of the form `a = b = c` is evaluated as `a = (b = c)`.</span></span>

### <a name="simple-assignment"></a><span data-ttu-id="602c5-2636">단순 할당</span><span class="sxs-lookup"><span data-stu-id="602c5-2636">Simple assignment</span></span>

<span data-ttu-id="602c5-2637">`=` 연산자는 단순 할당 연산자 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2637">The `=` operator is called the simple assignment operator.</span></span>

<span data-ttu-id="602c5-2638">단순 할당의 왼쪽된 피연산자 형식 인지 `E.P` 또는 `E[Ei]` 여기서 `E` 컴파일 시간 형식이 `dynamic`, 바인딩된 동적으로 할당 한 다음 ([동적 바인딩](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2638">If the left operand of a simple assignment is of the form `E.P` or `E[Ei]` where `E` has the compile-time type `dynamic`, then the assignment is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="602c5-2639">이 경우 컴파일 타임 대입 식의 형식이 `dynamic`, 아래에 설명 된 해결의 런타임 형식을 기반으로 런타임 시 수행 됩니다 및 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2639">In this case the compile-time type of the assignment expression is `dynamic`, and the resolution described below will take place at run-time based on the run-time type of `E`.</span></span>

<span data-ttu-id="602c5-2640">단순 할당에서 오른쪽 피연산자의 왼쪽된 피연산자의 형식으로 암시적으로 변환할 수 있는 식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2640">In a simple assignment, the right operand must be an expression that is implicitly convertible to the type of the left operand.</span></span> <span data-ttu-id="602c5-2641">작업은 왼쪽된 피연산자가 지정 된 변수, 속성 또는 인덱서 요소에 오른쪽 피연산자의 값을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2641">The operation assigns the value of the right operand to the variable, property, or indexer element given by the left operand.</span></span>

<span data-ttu-id="602c5-2642">단순 할당 식의 결과 왼쪽된 피연산자에 할당 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2642">The result of a simple assignment expression is the value assigned to the left operand.</span></span> <span data-ttu-id="602c5-2643">결과 왼쪽된 피연산자와 동일한 형식 및는 항상 값으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2643">The result has the same type as the left operand and is always classified as a value.</span></span>

<span data-ttu-id="602c5-2644">속성 또는 인덱서 있어야 왼쪽된 피연산자 인 속성 또는 인덱서 액세스를 사용 하는 경우는 `set` 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2644">If the left operand is a property or indexer access, the property or indexer must have a `set` accessor.</span></span> <span data-ttu-id="602c5-2645">이 경우 바인딩 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2645">If this is not the case, a binding-time error occurs.</span></span>

<span data-ttu-id="602c5-2646">폼의 단순한 할당을 처리 하는 런타임 `x = y` 다음 단계로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2646">The run-time processing of a simple assignment of the form `x = y` consists of the following steps:</span></span>

*  <span data-ttu-id="602c5-2647">경우 `x` 변수로로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2647">If `x` is classified as a variable:</span></span>
   * <span data-ttu-id="602c5-2648">`x` 변수를 생성 하기 위해 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2648">`x` is evaluated to produce the variable.</span></span>
   * <span data-ttu-id="602c5-2649">`y` 평가 되 고, 필요한 경우의 형식으로 변환할 `x` 는 암시적 변환을 통해 ([암시적 변환을](conversions.md#implicit-conversions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2649">`y` is evaluated and, if required, converted to the type of `x` through an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)).</span></span>
   * <span data-ttu-id="602c5-2650">경우 제공한 변수의 `x` 의 배열 요소를 *reference_type*에 대 한 계산한 값을 확인 하는 런타임 검사가 수행 됩니다 `y` 있는 배열 인스턴스의와 호환 되 `x` 는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2650">If the variable given by `x` is an array element of a *reference_type*, a run-time check is performed to ensure that the value computed for `y` is compatible with the array instance of which `x` is an element.</span></span> <span data-ttu-id="602c5-2651">검사가 성공 `y` 됩니다 `null`, 경우 암시적 참조 변환 또는 ([암시적 참조 변환](conversions.md#implicit-reference-conversions))에서 참조 하는 인스턴스의 실제 형식이 존재 `y` 실제 요소 형식으로 포함 하는 배열 인스턴스 `x`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2651">The check succeeds if `y` is `null`, or if an implicit reference conversion ([Implicit reference conversions](conversions.md#implicit-reference-conversions)) exists from the actual type of the instance referenced by `y` to the actual element type of the array instance containing `x`.</span></span> <span data-ttu-id="602c5-2652">그렇지 않으면 `System.ArrayTypeMismatchException`이 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2652">Otherwise, a `System.ArrayTypeMismatchException` is thrown.</span></span>
   * <span data-ttu-id="602c5-2653">계산 하 고 변환의 결과 값 `y` 계산 하 여 지정 된 위치에 저장 됩니다 `x`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2653">The value resulting from the evaluation and conversion of `y` is stored into the location given by the evaluation of `x`.</span></span>
*  <span data-ttu-id="602c5-2654">경우 `x` 속성 또는 인덱서에 액세스로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2654">If `x` is classified as a property or indexer access:</span></span>
   * <span data-ttu-id="602c5-2655">인스턴스 식 (경우 `x` 아닙니다 `static`) 및 인수 목록을 (경우 `x` 인덱서 액세스할)와 연결 된 `x` 평가 결과에서 사용 하는 후속 `set` 접근자 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2655">The instance expression (if `x` is not `static`) and the argument list (if `x` is an indexer access) associated with `x` are evaluated, and the results are used in the subsequent `set` accessor invocation.</span></span>
   * <span data-ttu-id="602c5-2656">`y` 평가 되 고, 필요한 경우의 형식으로 변환할 `x` 는 암시적 변환을 통해 ([암시적 변환을](conversions.md#implicit-conversions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2656">`y` is evaluated and, if required, converted to the type of `x` through an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)).</span></span>
   * <span data-ttu-id="602c5-2657">합니다 `set` 의 접근자 `x` 에 대 한 계산 된 값을 사용 하 여 호출 `y` 으로 해당 `value` 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2657">The `set` accessor of `x` is invoked with the value computed for `y` as its `value` argument.</span></span>

<span data-ttu-id="602c5-2658">배열 공동 분산 규칙 ([배열 공변성 (covariance)](arrays.md#array-covariance)) 배열 형식의 값을 허용 `A[]` 배열 형식의 인스턴스에 대 한 참조가 되도록 `B[]`암시적 참조 변환이 존재에서 제공 하는, `B` 를 `A`.</span><span class="sxs-lookup"><span data-stu-id="602c5-2658">The array co-variance rules ([Array covariance](arrays.md#array-covariance)) permit a value of an array type `A[]` to be a reference to an instance of an array type `B[]`, provided an implicit reference conversion exists from `B` to `A`.</span></span> <span data-ttu-id="602c5-2659">이러한 규칙의 배열 요소에 대 한 할당으로 인해를 *reference_type* 할당 되는 값 배열 인스턴스와 호환 되는지 확인 하는 런타임 검사가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2659">Because of these rules, assignment to an array element of a *reference_type* requires a run-time check to ensure that the value being assigned is compatible with the array instance.</span></span> <span data-ttu-id="602c5-2660">예제</span><span class="sxs-lookup"><span data-stu-id="602c5-2660">In the example</span></span>
```csharp
string[] sa = new string[10];
object[] oa = sa;

oa[0] = null;               // Ok
oa[1] = "Hello";            // Ok
oa[2] = new ArrayList();    // ArrayTypeMismatchException
```
<span data-ttu-id="602c5-2661">마지막으로 할당 하면를 `System.ArrayTypeMismatchException` 때문 인스턴스의 `ArrayList` 의 요소에 저장할 수는 `string[]`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2661">the last assignment causes a `System.ArrayTypeMismatchException` to be thrown because an instance of `ArrayList` cannot be stored in an element of a `string[]`.</span></span>

<span data-ttu-id="602c5-2662">속성 또는 인덱서를 선언 하는 경우는 *struct_type* 인스턴스 식이 할당 대상 연관 된 속성 또는 인덱서 액세스 변수로 분류 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2662">When a property or indexer declared in a *struct_type* is the target of an assignment, the instance expression associated with the property or indexer access must be classified as a variable.</span></span> <span data-ttu-id="602c5-2663">인스턴스 식은 값으로 분류 되는 바인딩 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2663">If the instance expression is classified as a value, a binding-time error occurs.</span></span> <span data-ttu-id="602c5-2664">때문에 [멤버 액세스](expressions.md#member-access), 동일한 규칙을 필드에도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2664">Because of [Member access](expressions.md#member-access), the same rule also applies to fields.</span></span>

<span data-ttu-id="602c5-2665">다음과 같은 선언이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2665">Given the declarations:</span></span>
```csharp
struct Point
{
    int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int X {
        get { return x; }
        set { x = value; }
    }

    public int Y {
        get { return y; }
        set { y = value; }
    }
}

struct Rectangle
{
    Point a, b;

    public Rectangle(Point a, Point b) {
        this.a = a;
        this.b = b;
    }

    public Point A {
        get { return a; }
        set { a = value; }
    }

    public Point B {
        get { return b; }
        set { b = value; }
    }
}
```
<span data-ttu-id="602c5-2666">예제</span><span class="sxs-lookup"><span data-stu-id="602c5-2666">in the example</span></span>
```csharp
Point p = new Point();
p.X = 100;
p.Y = 100;
Rectangle r = new Rectangle();
r.A = new Point(10, 10);
r.B = p;
```
<span data-ttu-id="602c5-2667">에 할당 `p.X`, `p.Y`, `r.A`, 및 `r.B` 때문에 허용 됩니다 `p` 및 `r` 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2667">the assignments to `p.X`, `p.Y`, `r.A`, and `r.B` are permitted because `p` and `r` are variables.</span></span> <span data-ttu-id="602c5-2668">그러나 예제의</span><span class="sxs-lookup"><span data-stu-id="602c5-2668">However, in the example</span></span>
```csharp
Rectangle r = new Rectangle();
r.A.X = 10;
r.A.Y = 10;
r.B.X = 100;
r.B.Y = 100;
```
<span data-ttu-id="602c5-2669">할당은 유효 하지 않거나 모든 이후 `r.A` 고 `r.B` 변수가 아닌 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2669">the assignments are all invalid, since `r.A` and `r.B` are not variables.</span></span>

### <a name="compound-assignment"></a><span data-ttu-id="602c5-2670">복합 할당</span><span class="sxs-lookup"><span data-stu-id="602c5-2670">Compound assignment</span></span>

<span data-ttu-id="602c5-2671">복합 대입의 왼쪽된 피연산자가 폼의 경우 `E.P` 또는 `E[Ei]` 여기서 `E` 컴파일 시간 형식이 `dynamic`, 바인딩된 동적으로 할당 한 다음 ([동적 바인딩](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2671">If the left operand of a compound assignment is of the form `E.P` or `E[Ei]` where `E` has the compile-time type `dynamic`, then the assignment is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="602c5-2672">이 경우 컴파일 타임 대입 식의 형식이 `dynamic`, 아래에 설명 된 해결의 런타임 형식을 기반으로 런타임 시 수행 됩니다 및 `E`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2672">In this case the compile-time type of the assignment expression is `dynamic`, and the resolution described below will take place at run-time based on the run-time type of `E`.</span></span>

<span data-ttu-id="602c5-2673">폼의 작업 `x op= y` 이항 연산자 오버 로드 확인을 적용 하 여 처리 됩니다 ([이항 연산자 오버 로드 확인](expressions.md#binary-operator-overload-resolution)) 작업 작성 된 것 처럼 `x op y`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2673">An operation of the form `x op= y` is processed by applying binary operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) as if the operation was written `x op y`.</span></span> <span data-ttu-id="602c5-2674">그런 다음</span><span class="sxs-lookup"><span data-stu-id="602c5-2674">Then,</span></span>

*  <span data-ttu-id="602c5-2675">선택한 연산자의 반환 형식을 형식으로 암시적으로 변환할 수 있으면 `x`를 작업으로 계산 됩니다 `x = x op y`점을 제외 하 고 `x` 한 번만 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2675">If the return type of the selected operator is implicitly convertible to the type of `x`, the operation is evaluated as `x = x op y`, except that `x` is evaluated only once.</span></span>
*  <span data-ttu-id="602c5-2676">그렇지 않으면 선택한 연산자는 선택한 연산자의 반환 형식으로의 형식으로 명시적으로 변환할 경우 미리 정의 된 연산자 `x`, 경우에 `y` 의 형식으로 암시적으로 변환할 수 `x` 또는 운영자가을 시프트 연산자, 작업으로 평가 됩니다 `x = (T)(x op y)`, 여기서 `T` 유형의 `x`점을 제외 하 고 `x` 한 번만 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2676">Otherwise, if the selected operator is a predefined operator, if the return type of the selected operator is explicitly convertible to the type of `x`, and if `y` is implicitly convertible to the type of `x` or the operator is a shift operator, then the operation is evaluated as `x = (T)(x op y)`, where `T` is the type of `x`, except that `x` is evaluated only once.</span></span>
*  <span data-ttu-id="602c5-2677">이 고, 그렇지 복합 할당 유효 하지 않은 및 바인딩 시간에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2677">Otherwise, the compound assignment is invalid, and a binding-time error occurs.</span></span>

<span data-ttu-id="602c5-2678">"한 번만 계산" 이라는 용어는의 평가에 의미 `x op y`, 구성 식의 결과 `x` 일시적으로 저장 되 고 할당을 수행할 때 다시 `x`입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2678">The term "evaluated only once" means that in the evaluation of `x op y`, the results of any constituent expressions of `x` are temporarily saved and then reused when performing the assignment to `x`.</span></span> <span data-ttu-id="602c5-2679">할당의 예를 들어 `A()[B()] += C()`여기서 `A` 반환 하는 `int[]`, 및 `B` 하 고 `C` 반환 하는 메서드는 `int`, 메서드는 순서 대로 한 번만 호출 됩니다 `A`, `B`, `C`.</span><span class="sxs-lookup"><span data-stu-id="602c5-2679">For example, in the assignment `A()[B()] += C()`, where `A` is a method returning `int[]`, and `B` and `C` are methods returning `int`, the methods are invoked only once, in the order `A`, `B`, `C`.</span></span>

<span data-ttu-id="602c5-2680">복합 대입의 왼쪽된 피연산자는 속성 액세스 또는 인덱서 액세스 경우 속성 또는 인덱서를 모두가지고 있어야를 `get` 접근자 및 `set` 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2680">When the left operand of a compound assignment is a property access or indexer access, the property or indexer must have both a `get` accessor and a `set` accessor.</span></span> <span data-ttu-id="602c5-2681">이 경우 바인딩 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2681">If this is not the case, a binding-time error occurs.</span></span>

<span data-ttu-id="602c5-2682">허용 위의 두 번째 규칙 `x op= y` 로 평가 되도록 하려는 `x = (T)(x op y)` 특정 컨텍스트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2682">The second rule above permits `x op= y` to be evaluated as `x = (T)(x op y)` in certain contexts.</span></span> <span data-ttu-id="602c5-2683">규칙이 존재 하는 형식의 왼쪽된 피연산자가 복합 연산자는 미리 정의 된 연산자를 사용할 수 있습니다 `sbyte`, `byte`를 `short`합니다 `ushort`, 또는 `char`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2683">The rule exists such that the predefined operators can be used as compound operators when the left operand is of type `sbyte`, `byte`, `short`, `ushort`, or `char`.</span></span> <span data-ttu-id="602c5-2684">미리 정의 된 연산자를 생성도 경우 두 인수가 모두 이러한 형식 중 하나를 결과 유형이 `int`에 설명 된 대로 [이진 숫자 프로 모션](expressions.md#binary-numeric-promotions)합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2684">Even when both arguments are of one of those types, the predefined operators produce a result of type `int`, as described in [Binary numeric promotions](expressions.md#binary-numeric-promotions).</span></span> <span data-ttu-id="602c5-2685">따라서 캐스팅 하지 않고는 결과 왼쪽된 피연산자에 할당 하려면 불가능 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2685">Thus, without a cast it would not be possible to assign the result to the left operand.</span></span>

<span data-ttu-id="602c5-2686">미리 정의 된 연산자에 대 한 규칙의 직관적인 효과 단순히 `x op= y` 모두 허용 됩니다의 `x op y` 고 `x = y` 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2686">The intuitive effect of the rule for predefined operators is simply that `x op= y` is permitted if both of `x op y` and `x = y` are permitted.</span></span> <span data-ttu-id="602c5-2687">예제</span><span class="sxs-lookup"><span data-stu-id="602c5-2687">In the example</span></span>
```csharp
byte b = 0;
char ch = '\0';
int i = 0;

b += 1;             // Ok
b += 1000;          // Error, b = 1000 not permitted
b += i;             // Error, b = i not permitted
b += (byte)i;       // Ok

ch += 1;            // Error, ch = 1 not permitted
ch += (char)1;      // Ok
```
<span data-ttu-id="602c5-2688">직관적인 각 오류 원인은 해당 단순 할당은 또한 셨 기를 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2688">the intuitive reason for each error is that a corresponding simple assignment would also have been an error.</span></span>

<span data-ttu-id="602c5-2689">즉, 작업은 지원 되는 복합 할당 작업 리프트는 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2689">This also means that compound assignment operations support lifted operations.</span></span> <span data-ttu-id="602c5-2690">예제</span><span class="sxs-lookup"><span data-stu-id="602c5-2690">In the example</span></span>
```csharp
int? i = 0;
i += 1;             // Ok
```
<span data-ttu-id="602c5-2691">리프트 된 연산자 `+(int?,int?)` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2691">the lifted operator `+(int?,int?)` is used.</span></span>

### <a name="event-assignment"></a><span data-ttu-id="602c5-2692">이벤트 할당</span><span class="sxs-lookup"><span data-stu-id="602c5-2692">Event assignment</span></span>

<span data-ttu-id="602c5-2693">하는 경우의 왼쪽된 피연산자는 `+=` 또는 `-=` 연산자는 이벤트 액세스로 분류 됩니다 다음 식은 다음과 같이 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2693">If the left operand of a `+=` or `-=` operator is classified as an event access, then the expression is evaluated as follows:</span></span>

*  <span data-ttu-id="602c5-2694">인스턴스 식이 있는 경우 이벤트 액세스 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2694">The instance expression, if any, of the event access is evaluated.</span></span>
*  <span data-ttu-id="602c5-2695">오른쪽 피연산자는 `+=` 또는 `-=` 연산자 계산을 변환 하는 암시적 변환을 통해 왼쪽된 피연산자의 형식으로 변환 하는 필요한 경우 ([암시적 변환을](conversions.md#implicit-conversions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2695">The right operand of the `+=` or `-=` operator is evaluated, and, if required, converted to the type of the left operand through an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)).</span></span>
*  <span data-ttu-id="602c5-2696">오른쪽 피연산자 평가 후 구성 된 인수 목록을 사용 하 여 이벤트의 이벤트 접근자가 호출 하 고, 필요한 경우 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2696">An event accessor of the event is invoked, with argument list consisting of the right operand, after evaluation and, if necessary, conversion.</span></span> <span data-ttu-id="602c5-2697">연산자 되었으면 `+=`, `add` 접근자가 호출 됩니다; 연산자 되었으면 `-=`, `remove` 접근자가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2697">If the operator was `+=`, the `add` accessor is invoked; if the operator was `-=`, the `remove` accessor is invoked.</span></span>

<span data-ttu-id="602c5-2698">이벤트 대입 식에서 값을 생성 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2698">An event assignment expression does not yield a value.</span></span> <span data-ttu-id="602c5-2699">따라서 이벤트 대입 식 에서만 유효의 컨텍스트를 *statement_expression* ([식 문은](statements.md#expression-statements)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2699">Thus, an event assignment expression is valid only in the context of a *statement_expression* ([Expression statements](statements.md#expression-statements)).</span></span>

## <a name="expression"></a><span data-ttu-id="602c5-2700">식</span><span class="sxs-lookup"><span data-stu-id="602c5-2700">Expression</span></span>

<span data-ttu-id="602c5-2701">*식* 이 *non_assignment_expression* 요소나 *할당*.</span><span class="sxs-lookup"><span data-stu-id="602c5-2701">An *expression* is either a *non_assignment_expression* or an *assignment*.</span></span>

```antlr
expression
    : non_assignment_expression
    | assignment
    ;

non_assignment_expression
    : conditional_expression
    | lambda_expression
    | query_expression
    ;
```

## <a name="constant-expressions"></a><span data-ttu-id="602c5-2702">상수 식</span><span class="sxs-lookup"><span data-stu-id="602c5-2702">Constant expressions</span></span>

<span data-ttu-id="602c5-2703">A *constant_expression* 컴파일 시간에 완전히 계산 될 수 있는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2703">A *constant_expression* is an expression that can be fully evaluated at compile-time.</span></span>

```antlr
constant_expression
    : expression
    ;
```

<span data-ttu-id="602c5-2704">상수 식 이어야 합니다는 `null` 리터럴 또는 다음 형식 중 하나를 사용 하 여 값: `sbyte`, `byte`, `short`, `ushort`를 `int`, `uint`를 `long`를 `ulong`, `char` `float`, `double`, `decimal`, `bool`를 `object`, `string`, 또는 열거형 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2704">A constant expression must be the `null` literal or a value with one of  the following types: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, `bool`, `object`, `string`, or any enumeration type.</span></span> <span data-ttu-id="602c5-2705">상수 식에서는 다음과 같은 구문이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2705">Only the following constructs are permitted in constant expressions:</span></span>

*  <span data-ttu-id="602c5-2706">리터럴 (포함 된 `null` 리터럴)입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2706">Literals (including the `null` literal).</span></span>
*  <span data-ttu-id="602c5-2707">에 대 한 참조 `const` 클래스 및 구조체 형식의 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2707">References to `const` members of class and struct types.</span></span>
*  <span data-ttu-id="602c5-2708">열거형 형식의 멤버에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2708">References to members of enumeration types.</span></span>
*  <span data-ttu-id="602c5-2709">에 대 한 참조 `const` 매개 변수 또는 지역 변수</span><span class="sxs-lookup"><span data-stu-id="602c5-2709">References to `const` parameters or local variables</span></span>
*  <span data-ttu-id="602c5-2710">괄호로 묶은 하위 식에서은 그 자체가 상수 식입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2710">Parenthesized sub-expressions, which are themselves constant expressions.</span></span>
*  <span data-ttu-id="602c5-2711">대상 유형이 제공 되는 캐스트 식 위에 나열 된 형식 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2711">Cast expressions, provided the target type is one of the types listed above.</span></span>
*  <span data-ttu-id="602c5-2712">`checked` 및 `unchecked` 식</span><span class="sxs-lookup"><span data-stu-id="602c5-2712">`checked` and `unchecked` expressions</span></span>
*  <span data-ttu-id="602c5-2713">기본 값 식</span><span class="sxs-lookup"><span data-stu-id="602c5-2713">Default value expressions</span></span>
*  <span data-ttu-id="602c5-2714">Nameof 식</span><span class="sxs-lookup"><span data-stu-id="602c5-2714">Nameof expressions</span></span>
*  <span data-ttu-id="602c5-2715">미리 정의 된 `+`, `-`를 `!`, 및 `~` 단항 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2715">The predefined `+`, `-`, `!`, and `~` unary operators.</span></span>
*  <span data-ttu-id="602c5-2716">미리 정의 된 `+`, `-`, `*`, `/`, `%`를 `<<`, `>>`를 `&`, `|`를 `^`, `&&`, `||`, `==`, `!=`, `<`를 `>`, `<=`, 및 `>=` 각 피연산자가 위에 나열 된 형식의 이진 연산자를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2716">The predefined `+`, `-`, `*`, `/`, `%`, `<<`, `>>`, `&`, `|`, `^`, `&&`, `||`, `==`, `!=`, `<`, `>`, `<=`, and `>=` binary operators, provided each operand is of a type listed above.</span></span>
*  <span data-ttu-id="602c5-2717">`?:` 조건부 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2717">The `?:` conditional operator.</span></span>

<span data-ttu-id="602c5-2718">상수 식에는 다음과 같은 변환이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2718">The following conversions are permitted in constant expressions:</span></span>

*  <span data-ttu-id="602c5-2719">Identity 변환</span><span class="sxs-lookup"><span data-stu-id="602c5-2719">Identity conversions</span></span>
*  <span data-ttu-id="602c5-2720">숫자 변환</span><span class="sxs-lookup"><span data-stu-id="602c5-2720">Numeric conversions</span></span>
*  <span data-ttu-id="602c5-2721">열거형 변환</span><span class="sxs-lookup"><span data-stu-id="602c5-2721">Enumeration conversions</span></span>
*  <span data-ttu-id="602c5-2722">상수 식 변환</span><span class="sxs-lookup"><span data-stu-id="602c5-2722">Constant expression conversions</span></span>
*  <span data-ttu-id="602c5-2723">암시적 및 명시적 참조 변환, 상수 식에서 null 값으로 계산 되는 변환의 소스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2723">Implicit and explicit reference conversions, provided that the source of the conversions is a constant expression that evaluates to the null value.</span></span>

<span data-ttu-id="602c5-2724">Boxing을 비롯 한 다른 변환 상수 식에서 null이 아닌 값의 unboxing 변환과 암시적 참조 변환이 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2724">Other conversions including boxing, unboxing and implicit reference conversions of non-null values are not permitted in constant expressions.</span></span> <span data-ttu-id="602c5-2725">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="602c5-2725">For example:</span></span>
```csharp
class C {
    const object i = 5;         // error: boxing conversion not permitted
    const object str = "hello"; // error: implicit reference conversion
}
```
<span data-ttu-id="602c5-2726">초기화 하는 boxing 변환이 필요 하기 때문에 i는 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2726">the initialization of i is an error because a boxing conversion is required.</span></span> <span data-ttu-id="602c5-2727">Str의 초기화는 null이 아닌 값에서 암시적 참조 변환이 필요 하기 때문에 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2727">The initialization of str is an error because an implicit reference conversion from a non-null value is required.</span></span>

<span data-ttu-id="602c5-2728">위에 나열 된 요구 사항을 충족 하는 식, 때마다 식은 컴파일 시간에 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2728">Whenever an expression fulfills the requirements listed above, the expression is evaluated at compile-time.</span></span> <span data-ttu-id="602c5-2729">식은 하위 식 상수가 아닌 생성자가 포함 된 더 큰 식의 경우에 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2729">This is true even if the expression is a sub-expression of a larger expression that contains non-constant constructs.</span></span>

<span data-ttu-id="602c5-2730">컴파일 타임 오류가 발생 하면 여기서 런타임 계산이 throw 된 예외를 컴파일 시간 계산이 한다는 상수가 아닌 식은 런타임에 평가와 동일한 규칙을 사용 하는 컴파일 시간 상수 식 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2730">The compile-time evaluation of constant expressions uses the same rules as run-time evaluation of non-constant expressions, except that where run-time evaluation would have thrown an exception, compile-time evaluation causes a compile-time error to occur.</span></span>

<span data-ttu-id="602c5-2731">상수 식에 명시적으로 배치 됩니다 하지 않는 한는 `unchecked` 컨텍스트, 정수 형식 산술 연산 및 변환에서 항상 식의 컴파일 타임 확인 하는 동안 발생 하는 오버플로 컴파일 타임 오류를 일으킬 ([상수 식](expressions.md#constant-expressions)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2731">Unless a constant expression is explicitly placed in an `unchecked` context, overflows that occur in integral-type arithmetic operations and conversions during the compile-time evaluation of the expression always cause compile-time errors ([Constant expressions](expressions.md#constant-expressions)).</span></span>

<span data-ttu-id="602c5-2732">상수 식은 아래에 나열 된 컨텍스트에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2732">Constant expressions occur in the contexts listed below.</span></span> <span data-ttu-id="602c5-2733">이러한 컨텍스트에서 식을 컴파일할 때 완벽 하 게 평가할 수 없습니다는 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2733">In these contexts, a compile-time error occurs if an expression cannot be fully evaluated at compile-time.</span></span>

*  <span data-ttu-id="602c5-2734">상수 선언 ([상수](classes.md#constants)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2734">Constant declarations ([Constants](classes.md#constants)).</span></span>
*  <span data-ttu-id="602c5-2735">열거형 멤버 선언 ([열거형 멤버](enums.md#enum-members)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2735">Enumeration member declarations ([Enum members](enums.md#enum-members)).</span></span>
*  <span data-ttu-id="602c5-2736">기본 인수를 형식 매개 변수 목록 ([메서드 매개 변수](classes.md#method-parameters))</span><span class="sxs-lookup"><span data-stu-id="602c5-2736">Default arguments of formal parameter lists ([Method parameters](classes.md#method-parameters))</span></span>
*  <span data-ttu-id="602c5-2737">`case` 레이블에 `switch` 문 ([switch 문](statements.md#the-switch-statement)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2737">`case` labels of a `switch` statement ([The switch statement](statements.md#the-switch-statement)).</span></span>
*  <span data-ttu-id="602c5-2738">`goto case` 문 ([goto 문을](statements.md#the-goto-statement)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2738">`goto case` statements ([The goto statement](statements.md#the-goto-statement)).</span></span>
*  <span data-ttu-id="602c5-2739">차원 배열 생성 식의 길이 ([배열 만들기 식](expressions.md#array-creation-expressions)) 이니셜라이저를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2739">Dimension lengths in an array creation expression ([Array creation expressions](expressions.md#array-creation-expressions)) that includes an initializer.</span></span>
*  <span data-ttu-id="602c5-2740">특성 ([특성](attributes.md)).</span><span class="sxs-lookup"><span data-stu-id="602c5-2740">Attributes ([Attributes](attributes.md)).</span></span>

<span data-ttu-id="602c5-2741">변환 하는 상수 식 암시적 변환을 ([암시적 상수 식 변환](conversions.md#implicit-constant-expression-conversions)) 형식의 상수 식을 허용 `int` 변환할 `sbyte`를 `byte`, `short`를 `ushort`, `uint`, 또는 `ulong`, 상수 식의 값이 대상 형식의 범위 내에 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2741">An implicit constant expression conversion ([Implicit constant expression conversions](conversions.md#implicit-constant-expression-conversions)) permits a constant expression of type `int` to be converted to `sbyte`, `byte`, `short`, `ushort`, `uint`, or `ulong`, provided the value of the constant expression is within the range of the destination type.</span></span>

## <a name="boolean-expressions"></a><span data-ttu-id="602c5-2742">부울 식</span><span class="sxs-lookup"><span data-stu-id="602c5-2742">Boolean expressions</span></span>

<span data-ttu-id="602c5-2743">A *boolean_expression* 형식의 결과 생성 하는 식 `bool`; 하거나 직접 또는 응용 프로그램을 통해 `operator true` 다음에 지정 된 대로 특정 컨텍스트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2743">A *boolean_expression* is an expression that yields a result of type `bool`; either directly or through application of `operator true` in certain contexts as specified in the following.</span></span>

```antlr
boolean_expression
    : expression
    ;
```

<span data-ttu-id="602c5-2744">조건식의 제어를 *if_statement* ([if 문을](statements.md#the-if-statement)), *while_statement* ([는 while 문](statements.md#the-while-statement)), *do_statement* ([do 문에](statements.md#the-do-statement)), 또는 *for_statement* ([는 문에 대 한](statements.md#the-for-statement)) 되는 *boolean_ 식*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2744">The controlling conditional expression of an *if_statement* ([The if statement](statements.md#the-if-statement)), *while_statement* ([The while statement](statements.md#the-while-statement)), *do_statement* ([The do statement](statements.md#the-do-statement)), or *for_statement* ([The for statement](statements.md#the-for-statement)) is a *boolean_expression*.</span></span> <span data-ttu-id="602c5-2745">조건식의 제어를 `?:` 연산자 ([조건부 연산자](expressions.md#conditional-operator))와 동일한 규칙을 따릅니다를 *boolean_expression*, 우선 순위 연산자의 이유로 분류 되지만 로 *conditional_or_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2745">The controlling conditional expression of the `?:` operator ([Conditional operator](expressions.md#conditional-operator)) follows the same rules as a *boolean_expression*, but for reasons of operator precedence is classified as a *conditional_or_expression*.</span></span>

<span data-ttu-id="602c5-2746">A *boolean_expression* `E` 형식의 값을 생성할 수 하는 데 필요한 `bool`, 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2746">A *boolean_expression* `E` is required to be able to produce a value of type `bool`, as follows:</span></span>

*  <span data-ttu-id="602c5-2747">하는 경우 `E` 암시적으로 변환할 수 `bool` 런타임에 암시적 변환이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2747">If `E` is implicitly convertible to `bool` then at runtime that implicit conversion is applied.</span></span>
*  <span data-ttu-id="602c5-2748">단항 연산자 오버 로드 확인이 고, 그렇지 ([단항 연산자 오버 로드 확인](expressions.md#unary-operator-overload-resolution)) 연산자의 고유한 모범 구현을 찾는 데 사용 됩니다 `true` 에서 `E`, 구현에는 런타임에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2748">Otherwise, unary operator overload resolution ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution)) is used to find a unique best implementation of operator `true` on `E`, and that implementation is applied at runtime.</span></span>
*  <span data-ttu-id="602c5-2749">이러한 연산자가 있으면 바인딩 시간 오류를 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2749">If no such operator is found, a binding-time error occurs.</span></span>

<span data-ttu-id="602c5-2750">`DBBool` 에서 구조체 형식 [데이터베이스 부울 유형](structs.md#database-boolean-type) 구현 하는 형식의 예가 나와 `operator true` 및 `operator false`합니다.</span><span class="sxs-lookup"><span data-stu-id="602c5-2750">The `DBBool` struct type in [Database boolean type](structs.md#database-boolean-type) provides an example of a type that implements `operator true` and `operator false`.</span></span>
