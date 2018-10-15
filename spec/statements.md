# <a name="statements"></a><span data-ttu-id="c3468-101">문</span><span class="sxs-lookup"><span data-stu-id="c3468-101">Statements</span></span>

<span data-ttu-id="c3468-102">C# 다양 한 문 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-102">C# provides a variety of statements.</span></span> <span data-ttu-id="c3468-103">대부분의 이러한 문 C 및 c + +에서 프로그래밍할는 개발자에 게 익숙할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-103">Most of these statements will be familiar to developers who have programmed in C and C++.</span></span>

```antlr
statement
    : labeled_statement
    | declaration_statement
    | embedded_statement
    ;

embedded_statement
    : block
    | empty_statement
    | expression_statement
    | selection_statement
    | iteration_statement
    | jump_statement
    | try_statement
    | checked_statement
    | unchecked_statement
    | lock_statement
    | using_statement
    | yield_statement
    | embedded_statement_unsafe
    ;
```

<span data-ttu-id="c3468-104">합니다 *embedded_statement* 비터미널 다른 문 내에서 표시 되는 문에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-104">The *embedded_statement* nonterminal is used for statements that appear within other statements.</span></span> <span data-ttu-id="c3468-105">사용 *embedded_statement* 대신 *문* 선언문 및 레이블된 문 다음 컨텍스트에서 사용을 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-105">The use of *embedded_statement* rather than *statement* excludes the use of declaration statements and labeled statements in these contexts.</span></span> <span data-ttu-id="c3468-106">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="c3468-106">The example</span></span>
```csharp
void F(bool b) {
    if (b)
        int i = 44;
}
```
<span data-ttu-id="c3468-107">때문에 컴파일 타임 오류가 발생을 `if` 문에 필요는 *embedded_statement* 아닌 *문을* 해당 경우 분기 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-107">results in a compile-time error because an `if` statement requires an *embedded_statement* rather than a *statement* for its if branch.</span></span> <span data-ttu-id="c3468-108">이 코드 된 허용 변수의 경우 `i` 을 선언할 수는 있지만 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-108">If this code were permitted, then the variable `i` would be declared, but it could never be used.</span></span> <span data-ttu-id="c3468-109">단, 배치 하 여는 `i`의 블록에서 선언 된 예제는 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-109">Note, however, that by placing `i`'s declaration in a block, the example is valid.</span></span>

## <a name="end-points-and-reachability"></a><span data-ttu-id="c3468-110">끝점 및 연결</span><span class="sxs-lookup"><span data-stu-id="c3468-110">End points and reachability</span></span>

<span data-ttu-id="c3468-111">모든 문에 ***끝점***합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-111">Every statement has an ***end point***.</span></span> <span data-ttu-id="c3468-112">직관적인 말해 문의 끝점 문 바로 뒤에 오는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-112">In intuitive terms, the end point of a statement is the location that immediately follows the statement.</span></span> <span data-ttu-id="c3468-113">복합 문 (포함 된 문이 포함 된 문)에 대 한 실행 규칙 컨트롤이 포함 된 문의 끝 지점에 도달할 때 수행 되는 동작을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-113">The execution rules for composite statements (statements that contain embedded statements) specify the action that is taken when control reaches the end point of an embedded statement.</span></span> <span data-ttu-id="c3468-114">예를 들어 제어 블록의 문이의 끝점에 도달 하면 블록의 다음 문으로 제어가 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-114">For example, when control reaches the end point of a statement in a block, control is transferred to the next statement in the block.</span></span>

<span data-ttu-id="c3468-115">문을 실행 하 여 연결할 수 수 있는 경우 문이 이라고 ***연결할***합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-115">If a statement can possibly be reached by execution, the statement is said to be ***reachable***.</span></span> <span data-ttu-id="c3468-116">반대로,를 문이 실행 되는 가능성이 있으면 문이 이라고 ***접근할 수 없는***합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-116">Conversely, if there is no possibility that a statement will be executed, the statement is said to be ***unreachable***.</span></span>

<span data-ttu-id="c3468-117">예제</span><span class="sxs-lookup"><span data-stu-id="c3468-117">In the example</span></span>
```csharp
void F() {
    Console.WriteLine("reachable");
    goto Label;
    Console.WriteLine("unreachable");
    Label:
    Console.WriteLine("reachable");
}
```
<span data-ttu-id="c3468-118">두 번째 호출 `Console.WriteLine` 에 문이 실행 되는 가능성이 있기 때문에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-118">the second invocation of `Console.WriteLine` is unreachable because there is no possibility that the statement will be executed.</span></span>

<span data-ttu-id="c3468-119">컴파일러는 문을 연결할 수 있는지 결정 하는 경우 경고가 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-119">A warning is reported if the compiler determines that a statement is unreachable.</span></span> <span data-ttu-id="c3468-120">특히 오류가 아니라 문에 연결할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="c3468-120">It is specifically not an error for a statement to be unreachable.</span></span>

<span data-ttu-id="c3468-121">특정 문 또는 끝점에 연결할 수 있는지 여부를 결정할 컴파일러는 각 문에 대해 정의 된 연결 규칙에 따라 흐름 분석을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-121">To determine whether a particular statement or end point is reachable, the compiler performs flow analysis according to the reachability rules defined for each statement.</span></span> <span data-ttu-id="c3468-122">흐름 분석 고려 상수 식의 값 ([상수 식](expressions.md#constant-expressions)) 문의 동작을 제어 하는 하지만 상수가 아닌 식의 가능한 값은 고려 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-122">The flow analysis takes into account the values of constant expressions ([Constant expressions](expressions.md#constant-expressions)) that control the behavior of statements, but the possible values of non-constant expressions are not considered.</span></span> <span data-ttu-id="c3468-123">즉, 제어 흐름 분석을 위해 지정 된 형식의 상수가 아닌 식은 해당 형식의 모든 가능한 값으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-123">In other words, for purposes of control flow analysis, a non-constant expression of a given type is considered to have any possible value of that type.</span></span>

<span data-ttu-id="c3468-124">예제</span><span class="sxs-lookup"><span data-stu-id="c3468-124">In the example</span></span>
```csharp
void F() {
    const int i = 1;
    if (i == 2) Console.WriteLine("unreachable");
}
```
<span data-ttu-id="c3468-125">부울 식입니다 합니다 `if` 문 이므로 상수 식의 두 피연산자는 `==` 연산자는 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-125">the boolean expression of the `if` statement is a constant expression because both operands of the `==` operator are constants.</span></span> <span data-ttu-id="c3468-126">상수 식은 컴파일 시간에 계산 되는 값을 생성 `false`, `Console.WriteLine` 호출 접근할 수 없는 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-126">As the constant expression is evaluated at compile-time, producing the value `false`, the `Console.WriteLine` invocation is considered unreachable.</span></span> <span data-ttu-id="c3468-127">그러나 경우 `i` 지역 변수 변경</span><span class="sxs-lookup"><span data-stu-id="c3468-127">However, if `i` is changed to be a local variable</span></span>
```csharp
void F() {
    int i = 1;
    if (i == 2) Console.WriteLine("reachable");
}
```
<span data-ttu-id="c3468-128">`Console.WriteLine` 하더라도 실제로 실행 되지 않는 호출에 연결할 수 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-128">the `Console.WriteLine` invocation is considered reachable, even though, in reality, it will never be executed.</span></span>

<span data-ttu-id="c3468-129">합니다 *블록* 함수 멤버는 항상 것으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-129">The *block* of a function member is always considered reachable.</span></span> <span data-ttu-id="c3468-130">블록의 각 문이의 가능성 규칙을 연속적으로 평가 하 여 지정 된 문의 연결 가능성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-130">By successively evaluating the reachability rules of each statement in a block, the reachability of any given statement can be determined.</span></span>

<span data-ttu-id="c3468-131">예제</span><span class="sxs-lookup"><span data-stu-id="c3468-131">In the example</span></span>
```csharp
void F(int x) {
    Console.WriteLine("start");
    if (x < 0) Console.WriteLine("negative");
}
```
<span data-ttu-id="c3468-132">두 번째 연결 `Console.WriteLine` 다음과 같이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-132">the reachability of the second `Console.WriteLine` is determined as follows:</span></span>

*  <span data-ttu-id="c3468-133">첫 번째 `Console.WriteLine` 식에 연결할 수 때문에 블록을는 `F` 메서드는 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-133">The first `Console.WriteLine` expression statement is reachable because the block of the `F` method is reachable.</span></span>
*  <span data-ttu-id="c3468-134">첫 번째 끝점 `Console.WriteLine` 식 문은 해당 문을 연결할 수 때문에 연결할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-134">The end point of the first `Console.WriteLine` expression statement is reachable because that statement is reachable.</span></span>
*  <span data-ttu-id="c3468-135">`if` 문 이므로 연결할 수 있는 첫 번째 끝 지점 `Console.WriteLine` 식에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-135">The `if` statement is reachable because the end point of the first `Console.WriteLine` expression statement is reachable.</span></span>
*  <span data-ttu-id="c3468-136">두 번째 `Console.WriteLine` 식에 연결할 수 있으므로 부울 식입니다는 `if` 문은 상수 값이 없는 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-136">The second `Console.WriteLine` expression statement is reachable because the boolean expression of the `if` statement does not have the constant value `false`.</span></span>

<span data-ttu-id="c3468-137">가지는 것이 가능 하는 문의 끝점에 대 한 컴파일 시간 오류를 두 가지 상황이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-137">There are two situations in which it is a compile-time error for the end point of a statement to be reachable:</span></span>

*  <span data-ttu-id="c3468-138">때문에 `switch` 문을 다음 스위치 섹션으로 "이동" 하는 switch 섹션을 허용 하지 않습니다, 끝점에 연결할 수는 switch 섹션의 문 목록에 대 한 컴파일 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-138">Because the `switch` statement does not permit a switch section to "fall through" to the next switch section, it is a compile-time error for the end point of the statement list of a switch section to be reachable.</span></span> <span data-ttu-id="c3468-139">이 오류가 발생할 경우 일반적으로 표시 하는 `break` 문에서 누락 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-139">If this error occurs, it is typically an indication that a `break` statement is missing.</span></span>
*  <span data-ttu-id="c3468-140">이 끝점에 연결할 수 값을 계산 하는 함수 멤버의 블록에 대 한 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-140">It is a compile-time error for the end point of the block of a function member that computes a value to be reachable.</span></span> <span data-ttu-id="c3468-141">표시는 일반적으로이 오류가 발생 하는 경우는 `return` 문에서 누락 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-141">If this error occurs, it typically is an indication that a `return` statement is missing.</span></span>

## <a name="blocks"></a><span data-ttu-id="c3468-142">블록</span><span class="sxs-lookup"><span data-stu-id="c3468-142">Blocks</span></span>

<span data-ttu-id="c3468-143">*블록*은 단일 문이 허용되는 컨텍스트에서 여러 문을 쓸 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-143">A *block* permits multiple statements to be written in contexts where a single statement is allowed.</span></span>

```antlr
block
    : '{' statement_list? '}'
    ;
```

<span data-ttu-id="c3468-144">A *블록* 선택적인 이루어져 *statement_list* ([문은 나열](statements.md#statement-lists)) 중괄호로 묶어서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-144">A *block* consists of an optional *statement_list* ([Statement lists](statements.md#statement-lists)), enclosed in braces.</span></span> <span data-ttu-id="c3468-145">문 목록을 생략 하면 비워 블록 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-145">If the statement list is omitted, the block is said to be empty.</span></span>

<span data-ttu-id="c3468-146">블록 선언 문을 포함할 수 있습니다 ([선언문](statements.md#declaration-statements)).</span><span class="sxs-lookup"><span data-stu-id="c3468-146">A block may contain declaration statements ([Declaration statements](statements.md#declaration-statements)).</span></span> <span data-ttu-id="c3468-147">지역 변수 또는 상수의 범위는 블록에서 선언 된 블록.</span><span class="sxs-lookup"><span data-stu-id="c3468-147">The scope of a local variable or constant declared in a block is the block.</span></span>

<span data-ttu-id="c3468-148">블록을 다음과 같이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-148">A block is executed as follows:</span></span>

*  <span data-ttu-id="c3468-149">블록이 비어 있는 경우 제어 블록의 끝 지점에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-149">If the block is empty, control is transferred to the end point of the block.</span></span>
*  <span data-ttu-id="c3468-150">블록을 비어 있지 않은 경우 문 목록으로 제어가 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-150">If the block is not empty, control is transferred to the statement list.</span></span> <span data-ttu-id="c3468-151">시간과 제어 문 목록의 끝 지점에 도달 하면, 제어 블록의 끝 지점에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-151">When and if control reaches the end point of the statement list, control is transferred to the end point of the block.</span></span>

<span data-ttu-id="c3468-152">블록의 문은 목록은 블록 자체에 연결할 수 경우에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-152">The statement list of a block is reachable if the block itself is reachable.</span></span>

<span data-ttu-id="c3468-153">블록이 비어 있는 경우 또는 문 목록의 끝 지점에 연결할 수 경우 블록의 끝 지점에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-153">The end point of a block is reachable if the block is empty or if the end point of the statement list is reachable.</span></span>

<span data-ttu-id="c3468-154">A *블록* 하나를 포함 하는 `yield` 문 ([yield 문을](statements.md#the-yield-statement))은 반복기 블록이 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-154">A *block* that contains one or more `yield` statements ([The yield statement](statements.md#the-yield-statement)) is called an iterator block.</span></span> <span data-ttu-id="c3468-155">반복기 블록은 반복기로 함수 멤버를 구현 하는 데 사용 됩니다 ([반복기](classes.md#iterators)).</span><span class="sxs-lookup"><span data-stu-id="c3468-155">Iterator blocks are used to implement function members as iterators ([Iterators](classes.md#iterators)).</span></span> <span data-ttu-id="c3468-156">반복기 블록에 몇 가지 추가 제한 사항이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-156">Some additional restrictions apply to iterator blocks:</span></span>

*  <span data-ttu-id="c3468-157">에 대 한 컴파일 시간 오류가 발생 한 `return` 반복기 블록에서 문을 (하지만 `yield return` 문이 허용 됩니다).</span><span class="sxs-lookup"><span data-stu-id="c3468-157">It is a compile-time error for a `return` statement to appear in an iterator block (but `yield return` statements are permitted).</span></span>
*  <span data-ttu-id="c3468-158">안전 하지 않은 컨텍스트를 포함 하는 반복기 블록에 대 한 컴파일 시간 오류 ([안전 하지 않은 컨텍스트](unsafe-code.md#unsafe-contexts)).</span><span class="sxs-lookup"><span data-stu-id="c3468-158">It is a compile-time error for an iterator block to contain an unsafe context ([Unsafe contexts](unsafe-code.md#unsafe-contexts)).</span></span> <span data-ttu-id="c3468-159">반복기 블록이 항상 안전 하지 않은 컨텍스트에서 선언 중첩 된 경우에 안전한 컨텍스트를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-159">An iterator block always defines a safe context, even when its declaration is nested in an unsafe context.</span></span>

### <a name="statement-lists"></a><span data-ttu-id="c3468-160">문 목록</span><span class="sxs-lookup"><span data-stu-id="c3468-160">Statement lists</span></span>

<span data-ttu-id="c3468-161">A ***문 목록의*** 순서로 기록 하는 하나 이상의 문으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-161">A ***statement list*** consists of one or more statements written in sequence.</span></span> <span data-ttu-id="c3468-162">문 목록 나타나는 *블록*s ([블록](statements.md#blocks)) 및 *switch_block*s ([switch 문에서](statements.md#the-switch-statement)).</span><span class="sxs-lookup"><span data-stu-id="c3468-162">Statement lists occur in *block*s ([Blocks](statements.md#blocks)) and in *switch_block*s ([The switch statement](statements.md#the-switch-statement)).</span></span>

```antlr
statement_list
    : statement+
    ;
```

<span data-ttu-id="c3468-163">첫 번째 문으로 제어를 전송 하 여 문 목록의 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-163">A statement list is executed by transferring control to the first statement.</span></span> <span data-ttu-id="c3468-164">및 제어 문의 끝 지점에 도달 하면 다음 문으로 제어가 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-164">When and if control reaches the end point of a statement, control is transferred to the next statement.</span></span> <span data-ttu-id="c3468-165">및 컨트롤이 마지막 명령문의 끝점에 도달할 때 문 목록의 끝 지점으로 제어가 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-165">When and if control reaches the end point of the last statement, control is transferred to the end point of the statement list.</span></span>

<span data-ttu-id="c3468-166">문 목록의 문 중 최소한 하나가 참인 경우에 연결할 수는:</span><span class="sxs-lookup"><span data-stu-id="c3468-166">A statement in a statement list is reachable if at least one of the following is true:</span></span>

*  <span data-ttu-id="c3468-167">문의 첫 번째 문인 및 문 목록에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-167">The statement is the first statement and the statement list itself is reachable.</span></span>
*  <span data-ttu-id="c3468-168">앞의 문에서의 끝점에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-168">The end point of the preceding statement is reachable.</span></span>
*  <span data-ttu-id="c3468-169">문에 레이블이 지정 된 문 및를 연결할 수 여 레이블을 참조 하는 `goto` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-169">The statement is a labeled statement and the label is referenced by a reachable `goto` statement.</span></span>

<span data-ttu-id="c3468-170">끝점 문 목록에 연결할 수 있는 경우 목록의 마지막 명령문의 끝점에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-170">The end point of a statement list is reachable if the end point of the last statement in the list is reachable.</span></span>

## <a name="the-empty-statement"></a><span data-ttu-id="c3468-171">빈 문</span><span class="sxs-lookup"><span data-stu-id="c3468-171">The empty statement</span></span>

<span data-ttu-id="c3468-172">*empty_statement* 아무 작업도 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-172">An *empty_statement* does nothing.</span></span>

```antlr
empty_statement
    : ';'
    ;
```

<span data-ttu-id="c3468-173">빈 문의 경우 컨텍스트에서 수행할 작업이 문을 필요한 경우 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-173">An empty statement is used when there are no operations to perform in a context where a statement is required.</span></span>

<span data-ttu-id="c3468-174">단순히 빈 문의 실행 문의 끝 지점에 제어를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-174">Execution of an empty statement simply transfers control to the end point of the statement.</span></span> <span data-ttu-id="c3468-175">따라서 빈 문의 끝점에 빈 문이 연결할 수 경우 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-175">Thus, the end point of an empty statement is reachable if the empty statement is reachable.</span></span>

<span data-ttu-id="c3468-176">빈 문을 작성할 때 사용할 수는 `while` null 본문이 있는 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-176">An empty statement can be used when writing a `while` statement with a null body:</span></span>
```csharp
bool ProcessMessage() {...}

void ProcessMessages() {
    while (ProcessMessage())
        ;
}
```

<span data-ttu-id="c3468-177">또한 빈 문의 수 닫기 전에 레이블을 선언 "`}`" 블록:</span><span class="sxs-lookup"><span data-stu-id="c3468-177">Also, an empty statement can be used to declare a label just before the closing "`}`" of a block:</span></span>
```csharp
void F() {
    ...
    if (done) goto exit;
    ...
    exit: ;
}
```

## <a name="labeled-statements"></a><span data-ttu-id="c3468-178">레이블 문</span><span class="sxs-lookup"><span data-stu-id="c3468-178">Labeled statements</span></span>

<span data-ttu-id="c3468-179">A *labeled_statement* 레이블을 붙일 수 하는 문을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-179">A *labeled_statement* permits a statement to be prefixed by a label.</span></span> <span data-ttu-id="c3468-180">레이블된 문 블록에서 수 있지만 포함 문으로 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-180">Labeled statements are permitted in blocks, but are not permitted as embedded statements.</span></span>

```antlr
labeled_statement
    : identifier ':' statement
    ;
```

<span data-ttu-id="c3468-181">Labeled 문 제공한 이름을 사용 하 여 레이블을 선언 합니다 *식별자*합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-181">A labeled statement declares a label with the name given by the *identifier*.</span></span> <span data-ttu-id="c3468-182">레이블의 범위는 전체 블록 중첩 블록이 포함 하 여 레이블을 선언입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-182">The scope of a label is the whole block in which the label is declared, including any nested blocks.</span></span> <span data-ttu-id="c3468-183">이 겹치는 범위에 동일한 이름 가진 두 개의 레이블에 대 한 컴파일 시간 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-183">It is a compile-time error for two labels with the same name to have overlapping scopes.</span></span>

<span data-ttu-id="c3468-184">레이블을에서 참조할 수 있습니다 `goto` 문 ([goto 문을](statements.md#the-goto-statement)) 레이블의 범위 내에서.</span><span class="sxs-lookup"><span data-stu-id="c3468-184">A label can be referenced from `goto` statements ([The goto statement](statements.md#the-goto-statement)) within the scope of the label.</span></span> <span data-ttu-id="c3468-185">즉 `goto` 문 블록 내에서 및 블록 되었지만 블록으로 되지 제어를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-185">This means that `goto` statements can transfer control within blocks and out of blocks, but never into blocks.</span></span>

<span data-ttu-id="c3468-186">레이블을 자체 선언 공간 있고 다른 식별자를 방해 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-186">Labels have their own declaration space and do not interfere with other identifiers.</span></span> <span data-ttu-id="c3468-187">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="c3468-187">The example</span></span>
```csharp
int F(int x) {
    if (x >= 0) goto x;
    x = -x;
    x: return x;
}
```
<span data-ttu-id="c3468-188">유효 하 고 이름을 사용 하 여 `x` 매개 변수 및 레이블을으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-188">is valid and uses the name `x` as both a parameter and a label.</span></span>

<span data-ttu-id="c3468-189">레이블 다음에 문 실행에 정확히 대응 하며 레이블이 지정 된 문 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-189">Execution of a labeled statement corresponds exactly to execution of the statement following the label.</span></span>

<span data-ttu-id="c3468-190">Labeled 문 정상적인 제어 흐름에 제공한 연결 가능성, 외에 연결할 수 여 레이블을 참조 하는 경우에 연결할 수는 `goto` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-190">In addition to the reachability provided by normal flow of control, a labeled statement is reachable if the label is referenced by a reachable `goto` statement.</span></span> <span data-ttu-id="c3468-191">(예외: 경우는 `goto` 문 내에 `try` 포함 하는 `finally` 블록 및 labeled 문 벗어납니다를 `try`, 및 끝점에는 `finally` 블록을 연결할 수 없기을 레이블이 지정 된 문이 연결할 수 `goto` 문.)</span><span class="sxs-lookup"><span data-stu-id="c3468-191">(Exception: If a `goto` statement is inside a `try` that includes a `finally` block, and the labeled statement is outside the `try`, and the end point of the `finally` block is unreachable, then the labeled statement is not reachable from that `goto` statement.)</span></span>

## <a name="declaration-statements"></a><span data-ttu-id="c3468-192">선언문</span><span class="sxs-lookup"><span data-stu-id="c3468-192">Declaration statements</span></span>

<span data-ttu-id="c3468-193">A *declaration_statement* 지역 변수 또는 상수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-193">A *declaration_statement* declares a local variable or constant.</span></span> <span data-ttu-id="c3468-194">선언문 블록에서 수 있지만 포함 문으로 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-194">Declaration statements are permitted in blocks, but are not permitted as embedded statements.</span></span>

```antlr
declaration_statement
    : local_variable_declaration ';'
    | local_constant_declaration ';'
    ;
```

### <a name="local-variable-declarations"></a><span data-ttu-id="c3468-195">지역 변수 선언</span><span class="sxs-lookup"><span data-stu-id="c3468-195">Local variable declarations</span></span>

<span data-ttu-id="c3468-196">A *local_variable_declaration* 하나 이상의 로컬 변수를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-196">A *local_variable_declaration* declares one or more local variables.</span></span>

```antlr
local_variable_declaration
    : local_variable_type local_variable_declarators
    ;

local_variable_type
    : type
    | 'var'
    ;

local_variable_declarators
    : local_variable_declarator
    | local_variable_declarators ',' local_variable_declarator
    ;

local_variable_declarator
    : identifier
    | identifier '=' local_variable_initializer
    ;

local_variable_initializer
    : expression
    | array_initializer
    | local_variable_initializer_unsafe
    ;
```

<span data-ttu-id="c3468-197">합니다 *local_variable_type* 의 한 *local_variable_declaration* 선언에 의해 정의 된 변수 유형을 직접 또는 식별자를 사용 하 여 나타냅니다 `var` 는 이니셜라이저에 따라 형식을 유추할 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-197">The *local_variable_type* of a *local_variable_declaration* either directly specifies the type of the variables introduced by the declaration, or indicates with the identifier `var` that the type should be inferred based on an initializer.</span></span> <span data-ttu-id="c3468-198">형식 목록이 나옵니다 *local_variable_declarator*s, 각각 새 변수를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-198">The type is followed by a list of *local_variable_declarator*s, each of which introduces a new variable.</span></span> <span data-ttu-id="c3468-199">A *local_variable_declarator* 이루어져는 *식별자* 뒤에 선택적으로 변수의 이름을 나타내는 "`=`" 토큰 및 *local_variable_initializer* 는 변수의 초기 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-199">A *local_variable_declarator* consists of an *identifier* that names the variable, optionally followed by an "`=`" token and a *local_variable_initializer* that gives the initial value of the variable.</span></span>

<span data-ttu-id="c3468-200">지역 변수 선언 컨텍스트에서 식별자 var 상황별 키워드로 역할 ([키워드](lexical-structure.md#keywords)). 경우는 *local_variable_type* 으로 지정 됩니다 `var` 및 명명 된 형식이 없는 `var` 는 범위에서 선언 되는 ***암시적 형식 지역 변수 선언***, 형식인 연결 된 이니셜라이저 식의 형식에서 유추 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-200">In the context of a local variable declaration, the identifier var acts as a contextual keyword ([Keywords](lexical-structure.md#keywords)).When the *local_variable_type* is specified as `var` and no type named `var` is in scope, the declaration is an ***implicitly typed local variable declaration***, whose type is inferred from the type of the associated initializer expression.</span></span> <span data-ttu-id="c3468-201">암시적 형식된 지역 변수 선언은 다음과 같은 제한 사항이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-201">Implicitly typed local variable declarations are subject to the following restrictions:</span></span>

*  <span data-ttu-id="c3468-202">합니다 *local_variable_declaration* 여러 개 포함할 수 없습니다 *local_variable_declarator*s입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-202">The *local_variable_declaration* cannot include multiple *local_variable_declarator*s.</span></span>
*  <span data-ttu-id="c3468-203">합니다 *local_variable_declarator* 포함 해야 합니다는 *local_variable_initializer*합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-203">The *local_variable_declarator* must include a *local_variable_initializer*.</span></span>
*  <span data-ttu-id="c3468-204">합니다 *local_variable_initializer* 이어야 합니다는 *식*합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-204">The *local_variable_initializer* must be an *expression*.</span></span>
*  <span data-ttu-id="c3468-205">이니셜라이저가 *식* 는 컴파일 시간 형식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-205">The initializer *expression* must have a compile-time type.</span></span>
*  <span data-ttu-id="c3468-206">이니셜라이저가 *식* 자체 선언 된 변수를 참조할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-206">The initializer *expression* cannot refer to the declared variable itself</span></span>

<span data-ttu-id="c3468-207">다음은 잘못 된 암시적으로 형식화 된 지역 변수 선언의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-207">The following are examples of incorrect implicitly typed local variable declarations:</span></span>

```csharp
var x;               // Error, no initializer to infer type from
var y = {1, 2, 3};   // Error, array initializer not permitted
var z = null;        // Error, null does not have a type
var u = x => x + 1;  // Error, anonymous functions do not have a type
var v = v++;         // Error, initializer cannot refer to variable itself
```

<span data-ttu-id="c3468-208">사용 하는 식에서 가져온 지역 변수 값을 *simple_name* ([단순 이름](expressions.md#simple-names))를 사용 하 여 로컬 변수의 값은 수정는 *할당* ( [대입 연산자](expressions.md#assignment-operators)).</span><span class="sxs-lookup"><span data-stu-id="c3468-208">The value of a local variable is obtained in an expression using a *simple_name* ([Simple names](expressions.md#simple-names)), and the value of a local variable is modified using an *assignment* ([Assignment operators](expressions.md#assignment-operators)).</span></span> <span data-ttu-id="c3468-209">로컬 변수로 할당 되어야 합니다 ([한정 된 할당](variables.md#definite-assignment)) 패키지를 가져온 위치 값을 해당 하는 각 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-209">A local variable must be definitely assigned ([Definite assignment](variables.md#definite-assignment)) at each location where its value is obtained.</span></span>

<span data-ttu-id="c3468-210">에 선언 된 지역 변수의 범위를 *local_variable_declaration* 블록은 선언이 발생에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-210">The scope of a local variable declared in a *local_variable_declaration* is the block in which the declaration occurs.</span></span> <span data-ttu-id="c3468-211">지역 변수 앞에 오는 텍스트 위치를 가리키도록 하면 오류가 발생 합니다 *local_variable_declarator* 지역 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-211">It is an error to refer to a local variable in a textual position that precedes the *local_variable_declarator* of the local variable.</span></span> <span data-ttu-id="c3468-212">지역 변수의 범위 내 변수 또는 상수 이름이 같은 다른 로컬 선언에 컴파일 타임 오류를 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-212">Within the scope of a local variable, it is a compile-time error to declare another local variable or constant with the same name.</span></span>

<span data-ttu-id="c3468-213">여러 변수를 선언 하는 로컬 변수 선언은 동일한 형식 사용 하 여 단일 변수를 여러 번 선언 하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-213">A local variable declaration that declares multiple variables is equivalent to multiple declarations of single variables with the same type.</span></span> <span data-ttu-id="c3468-214">또한 선언 바로 뒤에 삽입 되는 대입문 정확 하 게 변수 이니셜라이저에서 예외는 지역 변수 선언에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-214">Furthermore, a variable initializer in a local variable declaration corresponds exactly to an assignment statement that is inserted immediately after the declaration.</span></span>

<span data-ttu-id="c3468-215">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="c3468-215">The example</span></span>
```csharp
void F() {
    int x = 1, y, z = x * 2;
}
```
<span data-ttu-id="c3468-216">정확히 일치</span><span class="sxs-lookup"><span data-stu-id="c3468-216">corresponds exactly to</span></span>
```csharp
void F() {
    int x; x = 1;
    int y;
    int z; z = x * 2;
}
```

<span data-ttu-id="c3468-217">암시적 형식된 지역 변수 선언에서 선언 되는 로컬 변수에 유형의 변수를 초기화 하는 데 사용 된 식의 형식과 동일로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-217">In an implicitly typed local variable declaration, the type of the local variable being declared is taken to be the same as the type of the expression used to initialize the variable.</span></span> <span data-ttu-id="c3468-218">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c3468-218">For example:</span></span>
```csharp
var i = 5;
var s = "Hello";
var d = 1.0;
var numbers = new int[] {1, 2, 3};
var orders = new Dictionary<int,Order>();
```

<span data-ttu-id="c3468-219">암시적으로 형식화 된 지역 변수 선언 위에 다음 명시적 형식된 선언에 정확 하 게 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-219">The implicitly typed local variable declarations above are precisely equivalent to the following explicitly typed declarations:</span></span>
```csharp
int i = 5;
string s = "Hello";
double d = 1.0;
int[] numbers = new int[] {1, 2, 3};
Dictionary<int,Order> orders = new Dictionary<int,Order>();
```

### <a name="local-constant-declarations"></a><span data-ttu-id="c3468-220">지역 상수 선언</span><span class="sxs-lookup"><span data-stu-id="c3468-220">Local constant declarations</span></span>

<span data-ttu-id="c3468-221">A *local_constant_declaration* 하나 이상의 지역 상수 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-221">A *local_constant_declaration* declares one or more local constants.</span></span>

```antlr
local_constant_declaration
    : 'const' type constant_declarators
    ;

constant_declarators
    : constant_declarator (',' constant_declarator)*
    ;

constant_declarator
    : identifier '=' constant_expression
    ;
```

<span data-ttu-id="c3468-222">*형식* 의 한 *local_constant_declaration* 선언에 의해 도입 된 상수의 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-222">The *type* of a *local_constant_declaration* specifies the type of the constants introduced by the declaration.</span></span> <span data-ttu-id="c3468-223">형식 목록이 나옵니다 *constant_declarator*s, 각각 새 상수를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-223">The type is followed by a list of *constant_declarator*s, each of which introduces a new constant.</span></span> <span data-ttu-id="c3468-224">*constant_declarator* 이루어져는 *식별자* 이름을 하는 상수를 뒤에 "`=`" 토큰, 뒤에 *constant_expression* ([ 상수 식](expressions.md#constant-expressions)) 하는 상수 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-224">A *constant_declarator* consists of an *identifier* that names the constant, followed by an "`=`" token, followed by a *constant_expression* ([Constant expressions](expressions.md#constant-expressions)) that gives the value of the constant.</span></span>

<span data-ttu-id="c3468-225">합니다 *형식* 하 고 *constant_expression* 지역 상수 선언의 상수 멤버 선언의 것와 동일한 규칙을 따라야 ([상수](classes.md#constants)).</span><span class="sxs-lookup"><span data-stu-id="c3468-225">The *type* and *constant_expression* of a local constant declaration must follow the same rules as those of a constant member declaration ([Constants](classes.md#constants)).</span></span>

<span data-ttu-id="c3468-226">지역 상수 값을 사용 하는 식에서 가져올은 *simple_name* ([단순 이름](expressions.md#simple-names)).</span><span class="sxs-lookup"><span data-stu-id="c3468-226">The value of a local constant is obtained in an expression using a *simple_name* ([Simple names](expressions.md#simple-names)).</span></span>

<span data-ttu-id="c3468-227">지역 상수의 범위는 블록 선언 발생에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-227">The scope of a local constant is the block in which the declaration occurs.</span></span> <span data-ttu-id="c3468-228">지역 상수 앞에 오는 텍스트 위치에서 참조 하는 오류는 해당 *constant_declarator*합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-228">It is an error to refer to a local constant in a textual position that precedes its *constant_declarator*.</span></span> <span data-ttu-id="c3468-229">지역 상수 범위 내 변수 또는 상수 이름이 같은 다른 로컬 선언에 컴파일 타임 오류를 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-229">Within the scope of a local constant, it is a compile-time error to declare another local variable or constant with the same name.</span></span>

<span data-ttu-id="c3468-230">여러 상수를 선언 하는 지역 상수 선언 동일한 형식 사용 하 여 여러 단일 상수 선언 하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-230">A local constant declaration that declares multiple constants is equivalent to multiple declarations of single constants with the same type.</span></span>

## <a name="expression-statements"></a><span data-ttu-id="c3468-231">식 문</span><span class="sxs-lookup"><span data-stu-id="c3468-231">Expression statements</span></span>

<span data-ttu-id="c3468-232">*expression_statement* 지정된 된 식을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-232">An *expression_statement* evaluates a given expression.</span></span> <span data-ttu-id="c3468-233">값을 계산 하 여 식이 있는 경우 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-233">The value computed by the expression, if any, is discarded.</span></span>

```antlr
expression_statement
    : statement_expression ';'
    ;

statement_expression
    : invocation_expression
    | null_conditional_invocation_expression
    | object_creation_expression
    | assignment
    | post_increment_expression
    | post_decrement_expression
    | pre_increment_expression
    | pre_decrement_expression
    | await_expression
    ;
```

<span data-ttu-id="c3468-234">일부 식으로 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-234">Not all expressions are permitted as statements.</span></span> <span data-ttu-id="c3468-235">와 같은 특히 식에서 `x + y` 및 `x == 1` 는 단순히 계산 하는 값 (내용이 취소 됨), 문으로 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-235">In particular, expressions such as `x + y` and `x == 1` that merely compute a value (which will be discarded), are not permitted as statements.</span></span>

<span data-ttu-id="c3468-236">실행을 *expression_statement* 포함 된 식을 계산 하 고 컨트롤의 끝점으로 전송 합니다 *expression_statement*합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-236">Execution of an *expression_statement* evaluates the contained expression and then transfers control to the end point of the *expression_statement*.</span></span> <span data-ttu-id="c3468-237">끝점에는 *expression_statement* 접근할 수 있으면 해당 *expression_statement* 에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-237">The end point of an *expression_statement* is reachable if that *expression_statement* is reachable.</span></span>

## <a name="selection-statements"></a><span data-ttu-id="c3468-238">선택 문</span><span class="sxs-lookup"><span data-stu-id="c3468-238">Selection statements</span></span>

<span data-ttu-id="c3468-239">선택 문 수의 일부 식의 값을 기반으로 하는 실행 가능한 문 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-239">Selection statements select one of a number of possible statements for execution based on the value of some expression.</span></span>

```antlr
selection_statement
    : if_statement
    | switch_statement
    ;
```

### <a name="the-if-statement"></a><span data-ttu-id="c3468-240">If 문</span><span class="sxs-lookup"><span data-stu-id="c3468-240">The if statement</span></span>

<span data-ttu-id="c3468-241">`if` 문은 부울 식의 값에 따라 실행할 문을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-241">The `if` statement selects a statement for execution based on the value of a boolean expression.</span></span>

```antlr
if_statement
    : 'if' '(' boolean_expression ')' embedded_statement
    | 'if' '(' boolean_expression ')' embedded_statement 'else' embedded_statement
    ;
```

<span data-ttu-id="c3468-242">`else` 부분은 연결 된 가장 가까운 앞 `if` 구문에서 허용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-242">An `else` part is associated with the lexically nearest preceding `if` that is allowed by the syntax.</span></span> <span data-ttu-id="c3468-243">따라서는 `if` 폼의 문</span><span class="sxs-lookup"><span data-stu-id="c3468-243">Thus, an `if` statement of the form</span></span>
```csharp
if (x) if (y) F(); else G();
```
<span data-ttu-id="c3468-244">위의 식은 아래의 식과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-244">is equivalent to</span></span>
```csharp
if (x) {
    if (y) {
        F();
    }
    else {
        G();
    }
}
```

<span data-ttu-id="c3468-245">`if` 문을 다음과 같이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-245">An `if` statement is executed as follows:</span></span>

*  <span data-ttu-id="c3468-246">합니다 *boolean_expression* ([부울 식](expressions.md#boolean-expressions)) 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-246">The *boolean_expression* ([Boolean expressions](expressions.md#boolean-expressions)) is evaluated.</span></span>
*  <span data-ttu-id="c3468-247">부울 식이 `true`, 포함 된 첫 번째 문으로 제어가 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-247">If the boolean expression yields `true`, control is transferred to the first embedded statement.</span></span> <span data-ttu-id="c3468-248">컨트롤의 끝 지점으로 전송 되 및 컨트롤이 해당 문의 끝 지점에 도달할 때를 `if` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-248">When and if control reaches the end point of that statement, control is transferred to the end point of the `if` statement.</span></span>
*  <span data-ttu-id="c3468-249">부울 식이 `false` 경우에 `else` 파트가 있는 두 번째 포함 문으로 제어가 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-249">If the boolean expression yields `false` and if an `else` part is present, control is transferred to the second embedded statement.</span></span> <span data-ttu-id="c3468-250">컨트롤의 끝 지점으로 전송 되 및 컨트롤이 해당 문의 끝 지점에 도달할 때를 `if` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-250">When and if control reaches the end point of that statement, control is transferred to the end point of the `if` statement.</span></span>
*  <span data-ttu-id="c3468-251">부울 식이 `false` 경우에 `else` 파트가 있는 끝점에 제어가 `if` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-251">If the boolean expression yields `false` and if an `else` part is not present, control is transferred to the end point of the `if` statement.</span></span>

<span data-ttu-id="c3468-252">첫 번째 문을 포함을 `if` 접근할 수 하는 경우는 `if` 접근할 수 및 부울 식의 상수 값이 없는 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-252">The first embedded statement of an `if` statement is reachable if the `if` statement is reachable and the boolean expression does not have the constant value `false`.</span></span>

<span data-ttu-id="c3468-253">두 번째 문을 포함을 `if` 문에 있는 경우에 연결할 수 경우 합니다 `if` 접근할 수 및 부울 식의 상수 값이 없는 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-253">The second embedded statement of an `if` statement, if present, is reachable if the `if` statement is reachable and the boolean expression does not have the constant value `true`.</span></span>

<span data-ttu-id="c3468-254">끝점에는 `if` 포함된 문 중 하나 이상의 끝점에 연결할 수 경우 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-254">The end point of an `if` statement is reachable if the end point of at least one of its embedded statements is reachable.</span></span> <span data-ttu-id="c3468-255">끝 지점 또한는 `if` no 사용 하 여 문을 `else` 파트에 연결할 수 경우 합니다 `if` 접근할 수 및 부울 식의 상수 값이 없는 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-255">In addition, the end point of an `if` statement with no `else` part is reachable if the `if` statement is reachable and the boolean expression does not have the constant value `true`.</span></span>

### <a name="the-switch-statement"></a><span data-ttu-id="c3468-256">Switch 문</span><span class="sxs-lookup"><span data-stu-id="c3468-256">The switch statement</span></span>

<span data-ttu-id="c3468-257">Switch 문 실행에 대 한 switch 식의 값에 해당 하는 연결 된 스위치 레이블이 있는 문 목록을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-257">The switch statement selects for execution a statement list having an associated switch label that corresponds to the value of the switch expression.</span></span>

```antlr
switch_statement
    : 'switch' '(' expression ')' switch_block
    ;

switch_block
    : '{' switch_section* '}'
    ;

switch_section
    : switch_label+ statement_list
    ;

switch_label
    : 'case' constant_expression ':'
    | 'default' ':'
    ;
```

<span data-ttu-id="c3468-258">A *switch_statement* 키워드로 구성 됩니다 `switch`뒤에 괄호로 묶은 식 (switch 식 이라고 함), 뒤에 *switch_block*합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-258">A *switch_statement* consists of the keyword `switch`, followed by a parenthesized expression (called the switch expression), followed by a *switch_block*.</span></span> <span data-ttu-id="c3468-259">합니다 *switch_block* 0 개 이상으로 구성 됩니다 *switch_section*s를 중괄호로 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-259">The *switch_block* consists of zero or more *switch_section*s, enclosed in braces.</span></span> <span data-ttu-id="c3468-260">각 *switch_section* 하나 이상의 구성 *switch_label*s 뒤에 *statement_list* ([문은 나열](statements.md#statement-lists)).</span><span class="sxs-lookup"><span data-stu-id="c3468-260">Each *switch_section* consists of one or more *switch_label*s followed by a *statement_list* ([Statement lists](statements.md#statement-lists)).</span></span>

<span data-ttu-id="c3468-261">합니다 ***유형을 제어 하는*** 의 `switch` 문은 switch 식으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-261">The ***governing type*** of a `switch` statement is established by the switch expression.</span></span>

*  <span data-ttu-id="c3468-262">Switch 식의 형식이 `sbyte`, `byte`, `short`, `ushort`, `int`를 `uint`, `long`, `ulong`, `bool`를 `char`, `string`, 또는 *enum_type*, 또는 이러한 형식 중 하나에 해당 하는 nullable 형식 경우 관리 되는 유형의 `switch` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-262">If the type of the switch expression is `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `bool`, `char`, `string`, or an *enum_type*, or if it is the nullable type corresponding to one of these types, then that is the governing type of the `switch` statement.</span></span>
*  <span data-ttu-id="c3468-263">그렇지 않은 경우 정확히 하나의 사용자 정의 암시적으로 변환 ([사용자 정의 변환은](conversions.md#user-defined-conversions)) 다음 가능한 형식을 제어 하는 중에 switch 식의 형식에서 존재 해야 합니다: `sbyte`를 `byte`, `short` 를 `ushort`, `int`, `uint`, `long`를 `ulong`를 `char`, `string`, 또는 이러한 형식 중 하나에 해당 하는 nullable 형식.</span><span class="sxs-lookup"><span data-stu-id="c3468-263">Otherwise, exactly one user-defined implicit conversion ([User-defined conversions](conversions.md#user-defined-conversions)) must exist from the type of the switch expression to one of the following possible governing types: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `string`, or,  a nullable type corresponding to one of those types.</span></span>
*  <span data-ttu-id="c3468-264">그렇지 않으면 이러한 암시적 변환이 존재 하거나 이러한 하나의 암시적 변환이 존재 하는 경우 두 개를 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-264">Otherwise, if no such implicit conversion exists, or if more than one such implicit conversion exists, a compile-time error occurs.</span></span>

<span data-ttu-id="c3468-265">각 상수 식을 `case` 레이블이 암시적으로 변환할 수 있는 값을 표시 해야 합니다 ([암시적 변환을](conversions.md#implicit-conversions)) 관리 유형의 `switch` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-265">The constant expression of each `case` label must denote a value that is implicitly convertible ([Implicit conversions](conversions.md#implicit-conversions)) to the governing type of the `switch` statement.</span></span> <span data-ttu-id="c3468-266">컴파일 타임 오류가 발생 하는 경우 두 개 이상의 `case` 동일한 레이블 `switch` 문에서 동일한 상수 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-266">A compile-time error occurs if two or more `case` labels in the same `switch` statement specify the same constant value.</span></span>

<span data-ttu-id="c3468-267">최대 하나만 수 `default` switch 문에서 레이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-267">There can be at most one `default` label in a switch statement.</span></span>

<span data-ttu-id="c3468-268">`switch` 문을 다음과 같이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-268">A `switch` statement is executed as follows:</span></span>

*  <span data-ttu-id="c3468-269">Switch 식 평가 되 고 관리 하는 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-269">The switch expression is evaluated and converted to the governing type.</span></span>
*  <span data-ttu-id="c3468-270">상수 중 하나를 지정 하는 경우는 `case` 동일한 레이블 `switch` 문은 switch 식의 값과 같으면 이면 일치 다음 문 목록으로 제어가 `case` 레이블.</span><span class="sxs-lookup"><span data-stu-id="c3468-270">If one of the constants specified in a `case` label in the same `switch` statement is equal to the value of the switch expression, control is transferred to the statement list following the matched `case` label.</span></span>
*  <span data-ttu-id="c3468-271">경우에 지정 된 상수 `case` 동일한 레이블 `switch` 문을 switch 식의 값과 같지 경우에 `default` 레이블이 있는 경우 목록 다음 문으로 제어가 전달 됩니다는 `default` 레이블입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-271">If none of the constants specified in `case` labels in the same `switch` statement is equal to the value of the switch expression, and if a `default` label is present, control is transferred to the statement list following the `default` label.</span></span>
*  <span data-ttu-id="c3468-272">경우에 지정 된 상수 `case` 동일한 레이블 `switch` 문을 switch 식의 값과 같지 경우 `default` 레이블이, 끝점에 제어가 `switch` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-272">If none of the constants specified in `case` labels in the same `switch` statement is equal to the value of the switch expression, and if no `default` label is present, control is transferred to the end point of the `switch` statement.</span></span>

<span data-ttu-id="c3468-273">Switch 섹션의 문 목록의 끝 지점에 연결할 수 경우 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-273">If the end point of the statement list of a switch section is reachable, a compile-time error occurs.</span></span> <span data-ttu-id="c3468-274">이 이동 금지"규칙 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-274">This is known as the "no fall through" rule.</span></span> <span data-ttu-id="c3468-275">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="c3468-275">The example</span></span>
```csharp
switch (i) {
case 0:
    CaseZero();
    break;
case 1:
    CaseOne();
    break;
default:
    CaseOthers();
    break;
}
```
<span data-ttu-id="c3468-276">없는 스위치 섹션에는 연결 가능한 끝점이 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-276">is valid because no switch section has a reachable end point.</span></span> <span data-ttu-id="c3468-277">C 및 c + +와 달리 switch 섹션이 실행 할 권한이 없습니다 "이동"에 다음 스위치 섹션 및 예제</span><span class="sxs-lookup"><span data-stu-id="c3468-277">Unlike C and C++, execution of a switch section is not permitted to "fall through" to the next switch section, and the example</span></span>
```csharp
switch (i) {
case 0:
    CaseZero();
case 1:
    CaseZeroOrOne();
default:
    CaseAny();
}
```
<span data-ttu-id="c3468-278">컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-278">results in a compile-time error.</span></span> <span data-ttu-id="c3468-279">다른 스위치 섹션에서는 명시적인 실행 하 여 다음 switch 섹션의 실행의 경우 `goto case` 또는 `goto default` 문을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-279">When execution of a switch section is to be followed by execution of another switch section, an explicit `goto case` or `goto default` statement must be used:</span></span>
```csharp
switch (i) {
case 0:
    CaseZero();
    goto case 1;
case 1:
    CaseZeroOrOne();
    goto default;
default:
    CaseAny();
    break;
}
```

<span data-ttu-id="c3468-280">레이블이 여러 개 허용 되는 *switch_section*합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-280">Multiple labels are permitted in a *switch_section*.</span></span> <span data-ttu-id="c3468-281">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="c3468-281">The example</span></span>
```csharp
switch (i) {
case 0:
    CaseZero();
    break;
case 1:
    CaseOne();
    break;
case 2:
default:
    CaseTwo();
    break;
}
```
<span data-ttu-id="c3468-282">유효합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-282">is valid.</span></span> <span data-ttu-id="c3468-283">예제 때문에 이동 금지"규칙을 위반 하지 않는 레이블을 `case 2:` 하 고 `default:` 동일의 일부인 *switch_section*합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-283">The example does not violate the "no fall through" rule because the labels `case 2:` and `default:` are part of the same *switch_section*.</span></span>

<span data-ttu-id="c3468-284">이동 금지"규칙을 사용 하면 C 및 c + +에서 발생 하는 버그의 일반적인 클래스가 때 `break` 실수로 문을 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-284">The "no fall through" rule prevents a common class of bugs that occur in C and C++ when `break` statements are accidentally omitted.</span></span> <span data-ttu-id="c3468-285">Switch 섹션을이 규칙으로 인해 또한는 `switch` 문에 문의 동작에 영향을 주지 않고 임의로 다시 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-285">In addition, because of this rule, the switch sections of a `switch` statement can be arbitrarily rearranged without affecting the behavior of the statement.</span></span> <span data-ttu-id="c3468-286">섹션의 예를 들어를 `switch` 문의 동작에 영향을 주지 않고 위의 문은 되돌릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-286">For example, the sections of the `switch` statement above can be reversed without affecting the behavior of the statement:</span></span>
```csharp
switch (i) {
default:
    CaseAny();
    break;
case 1:
    CaseZeroOrOne();
    goto default;
case 0:
    CaseZero();
    goto case 1;
}
```

<span data-ttu-id="c3468-287">Switch 섹션의 문 목록에 일반적으로 종료는 `break`, `goto case`, 또는 `goto default` 문과 비슷하지만 끝점 문 목록에 연결할 수 없는 렌더링 하는 모든 구문을 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-287">The statement list of a switch section typically ends in a `break`, `goto case`, or `goto default` statement, but any construct that renders the end point of the statement list unreachable is permitted.</span></span> <span data-ttu-id="c3468-288">예를 들어를 `while` 부울 식에 의해 제어 문을 `true` 알려져 접근 불가능 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-288">For example, a `while` statement controlled by the boolean expression `true` is known to never reach its end point.</span></span> <span data-ttu-id="c3468-289">마찬가지로, 한 `throw` 또는 `return` 문은 항상 다른 곳에서 제어를 전송 하 고 해당 끝점에 도달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-289">Likewise, a `throw` or `return` statement always transfers control elsewhere and never reaches its end point.</span></span> <span data-ttu-id="c3468-290">따라서 다음 예제에서는 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-290">Thus, the following example is valid:</span></span>
```csharp
switch (i) {
case 0:
    while (true) F();
case 1:
    throw new ArgumentException();
case 2:
    return;
}
```

<span data-ttu-id="c3468-291">관리 유형의 `switch` 문 형식 수 `string`입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-291">The governing type of a `switch` statement may be the type `string`.</span></span> <span data-ttu-id="c3468-292">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c3468-292">For example:</span></span>
```csharp
void DoCommand(string command) {
    switch (command.ToLower()) {
    case "run":
        DoRun();
        break;
    case "save":
        DoSave();
        break;
    case "quit":
        DoQuit();
        break;
    default:
        InvalidCommand(command);
        break;
    }
}
```

<span data-ttu-id="c3468-293">같은 문자열 같음 연산자 ([문자열 같음 연산자](expressions.md#string-equality-operators)), `switch` 문을 대/소문자 구분 및 스위치 식 문자열을 정확 하 게 일치 하는 경우에 지정된 switch 섹션이 실행 됩니다는 `case` 레이블 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-293">Like the string equality operators ([String equality operators](expressions.md#string-equality-operators)), the `switch` statement is case sensitive and will execute a given switch section only if the switch expression string exactly matches a `case` label constant.</span></span>

<span data-ttu-id="c3468-294">입력을 제어 하는 경우는 `switch` 문이 `string`, 값 `null` case 레이블은 상수 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-294">When the governing type of a `switch` statement is `string`, the value `null` is permitted as a case label constant.</span></span>

<span data-ttu-id="c3468-295">합니다 *statement_list*의 한 *switch_block* 선언 문을 포함할 수 있습니다 ([선언문](statements.md#declaration-statements)).</span><span class="sxs-lookup"><span data-stu-id="c3468-295">The *statement_list*s of a *switch_block* may contain declaration statements ([Declaration statements](statements.md#declaration-statements)).</span></span> <span data-ttu-id="c3468-296">지역 변수 또는 상수 스위치 블록에서 선언 된 범위가 스위치 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-296">The scope of a local variable or constant declared in a switch block is the switch block.</span></span>

<span data-ttu-id="c3468-297">지정 된 스위치 섹션의 문 목록에 연결할 수 경우는 `switch` 문에 연결할 수 이며 다음 중 하나 이상이 true.</span><span class="sxs-lookup"><span data-stu-id="c3468-297">The statement list of a given switch section is reachable if the `switch` statement is reachable and at least one of the following is true:</span></span>

*  <span data-ttu-id="c3468-298">Switch 식에는 상수가 아닌 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-298">The switch expression is a non-constant value.</span></span>
*  <span data-ttu-id="c3468-299">Switch 식은 일치 하는 상수 값을 `case` 스위치 섹션에는 레이블.</span><span class="sxs-lookup"><span data-stu-id="c3468-299">The switch expression is a constant value that matches a `case` label in the switch section.</span></span>
*  <span data-ttu-id="c3468-300">Switch 식은 일치 하지 않는 상수 값 `case` 레이블 및 스위치 섹션에 포함 된 `default` 레이블.</span><span class="sxs-lookup"><span data-stu-id="c3468-300">The switch expression is a constant value that doesn't match any `case` label, and the switch section contains the `default` label.</span></span>
*  <span data-ttu-id="c3468-301">연결할 수에서 참조 하는 switch 섹션의 스위치 레이블을 `goto case` 또는 `goto default` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-301">A switch label of the switch section is referenced by a reachable `goto case` or `goto default` statement.</span></span>

<span data-ttu-id="c3468-302">끝점에는 `switch` 다음 중 하나 이상이 true 이면 접근할 수:</span><span class="sxs-lookup"><span data-stu-id="c3468-302">The end point of a `switch` statement is reachable if at least one of the following is true:</span></span>

*  <span data-ttu-id="c3468-303">합니다 `switch` 문에 포함을 연결할 수 `break` 문을 끝내는 `switch` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-303">The `switch` statement contains a reachable `break` statement that exits the `switch` statement.</span></span>
*  <span data-ttu-id="c3468-304">합니다 `switch` 접근할 수, switch 식이 상수가 아닌 값 및 no `default` 레이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-304">The `switch` statement is reachable, the switch expression is a non-constant value, and no `default` label is present.</span></span>
*  <span data-ttu-id="c3468-305">합니다 `switch` 접근할 수는 switch 식 일치 하지 않는 상수 값을 `case` 레이블과 아니요 `default` 레이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-305">The `switch` statement is reachable, the switch expression is a constant value that doesn't match any `case` label, and no `default` label is present.</span></span>

## <a name="iteration-statements"></a><span data-ttu-id="c3468-306">반복 문</span><span class="sxs-lookup"><span data-stu-id="c3468-306">Iteration statements</span></span>

<span data-ttu-id="c3468-307">반복 문은 포함된 문을 반복적으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-307">Iteration statements repeatedly execute an embedded statement.</span></span>

```antlr
iteration_statement
    : while_statement
    | do_statement
    | for_statement
    | foreach_statement
    ;
```

### <a name="the-while-statement"></a><span data-ttu-id="c3468-308">while 문</span><span class="sxs-lookup"><span data-stu-id="c3468-308">The while statement</span></span>

<span data-ttu-id="c3468-309">`while` 문은 0 개 이상 포함 된 문에 조건부로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-309">The `while` statement conditionally executes an embedded statement zero or more times.</span></span>

```antlr
while_statement
    : 'while' '(' boolean_expression ')' embedded_statement
    ;
```

<span data-ttu-id="c3468-310">`while` 문을 다음과 같이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-310">A `while` statement is executed as follows:</span></span>

*  <span data-ttu-id="c3468-311">합니다 *boolean_expression* ([부울 식](expressions.md#boolean-expressions)) 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-311">The *boolean_expression* ([Boolean expressions](expressions.md#boolean-expressions)) is evaluated.</span></span>
*  <span data-ttu-id="c3468-312">부울 식이 `true`, 포함 문으로 제어가 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-312">If the boolean expression yields `true`, control is transferred to the embedded statement.</span></span> <span data-ttu-id="c3468-313">컨트롤에 포함 된 문의 끝 지점에 도달 하는 경우 (실행에서을 `continue` 문)의 시작 부분으로 제어가 `while` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-313">When and if control reaches the end point of the embedded statement (possibly from execution of a `continue` statement), control is transferred to the beginning of the `while` statement.</span></span>
*  <span data-ttu-id="c3468-314">부울 식이 `false`를 끝점에 제어가 `while` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-314">If the boolean expression yields `false`, control is transferred to the end point of the `while` statement.</span></span>

<span data-ttu-id="c3468-315">포함 된 문에서 `while` 문을 `break` 문 ([break 문을](statements.md#the-break-statement)) 제어 끝점에 전송할 수 있습니다를 `while` (종료 되므로 포함 된 반복 문 문) 및 `continue` 문 ([continue 문을](statements.md#the-continue-statement)) 컨트롤의 끝점이 포함된 된 문 전송할 수 있습니다 (따라서의 또 다른 반복을 수행 합니다 `while` 문).</span><span class="sxs-lookup"><span data-stu-id="c3468-315">Within the embedded statement of a `while` statement, a `break` statement ([The break statement](statements.md#the-break-statement)) may be used to transfer control to the end point of the `while` statement (thus ending iteration of the embedded statement), and a `continue` statement ([The continue statement](statements.md#the-continue-statement)) may be used to transfer control to the end point of the embedded statement (thus performing another iteration of the `while` statement).</span></span>

<span data-ttu-id="c3468-316">포함된 문에 `while` 접근할 수 하는 경우는 `while` 접근할 수 및 부울 식의 상수 값이 없는 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-316">The embedded statement of a `while` statement is reachable if the `while` statement is reachable and the boolean expression does not have the constant value `false`.</span></span>

<span data-ttu-id="c3468-317">끝점에는 `while` 다음 중 하나 이상이 true 이면 접근할 수:</span><span class="sxs-lookup"><span data-stu-id="c3468-317">The end point of a `while` statement is reachable if at least one of the following is true:</span></span>

*  <span data-ttu-id="c3468-318">합니다 `while` 문에 포함을 연결할 수 `break` 문을 끝내는 `while` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-318">The `while` statement contains a reachable `break` statement that exits the `while` statement.</span></span>
*  <span data-ttu-id="c3468-319">합니다 `while` 접근할 수 및 부울 식의 상수 값이 없는 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-319">The `while` statement is reachable and the boolean expression does not have the constant value `true`.</span></span>

### <a name="the-do-statement"></a><span data-ttu-id="c3468-320">Do 문</span><span class="sxs-lookup"><span data-stu-id="c3468-320">The do statement</span></span>

<span data-ttu-id="c3468-321">`do` 문이 포함된 문을 한 번 이상를 조건부로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-321">The `do` statement conditionally executes an embedded statement one or more times.</span></span>

```antlr
do_statement
    : 'do' embedded_statement 'while' '(' boolean_expression ')' ';'
    ;
```

<span data-ttu-id="c3468-322">`do` 문을 다음과 같이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-322">A `do` statement is executed as follows:</span></span>

*  <span data-ttu-id="c3468-323">포함 된 문으로 제어가 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-323">Control is transferred to the embedded statement.</span></span>
*  <span data-ttu-id="c3468-324">컨트롤에 포함 된 문의 끝 지점에 도달 하는 경우 (실행에서을 `continue` 문)의 *boolean_expression* ([부울 식](expressions.md#boolean-expressions)) 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-324">When and if control reaches the end point of the embedded statement (possibly from execution of a `continue` statement), the *boolean_expression* ([Boolean expressions](expressions.md#boolean-expressions)) is evaluated.</span></span> <span data-ttu-id="c3468-325">부울 식이 `true`, 시작 부분으로 제어가 `do` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-325">If the boolean expression yields `true`, control is transferred to the beginning of the `do` statement.</span></span> <span data-ttu-id="c3468-326">그렇지 않으면 제어가 끝점에는 `do` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-326">Otherwise, control is transferred to the end point of the `do` statement.</span></span>

<span data-ttu-id="c3468-327">포함 된 문에서 `do` 문을 `break` 문 ([break 문을](statements.md#the-break-statement)) 제어 끝점에 전송할 수 있습니다를 `do` (종료 되므로 포함 된 반복 문 문)와 `continue` 문 ([continue 문을](statements.md#the-continue-statement)) 컨트롤의 끝점이 포함된 된 문 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-327">Within the embedded statement of a `do` statement, a `break` statement ([The break statement](statements.md#the-break-statement)) may be used to transfer control to the end point of the `do` statement (thus ending iteration of the embedded statement), and a `continue` statement ([The continue statement](statements.md#the-continue-statement)) may be used to transfer control to the end point of the embedded statement.</span></span>

<span data-ttu-id="c3468-328">포함된 문에 `do` 접근할 수 경우는 `do` 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-328">The embedded statement of a `do` statement is reachable if the `do` statement is reachable.</span></span>

<span data-ttu-id="c3468-329">끝점에는 `do` 다음 중 하나 이상이 true 이면 접근할 수:</span><span class="sxs-lookup"><span data-stu-id="c3468-329">The end point of a `do` statement is reachable if at least one of the following is true:</span></span>

*  <span data-ttu-id="c3468-330">합니다 `do` 문에 포함을 연결할 수 `break` 문을 끝내는 `do` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-330">The `do` statement contains a reachable `break` statement that exits the `do` statement.</span></span>
*  <span data-ttu-id="c3468-331">포함된 된 문의 끝점에 연결할 수 및 부울 식의 상수 값이 없는 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-331">The end point of the embedded statement is reachable and the boolean expression does not have the constant value `true`.</span></span>

### <a name="the-for-statement"></a><span data-ttu-id="c3468-332">문에 대 한</span><span class="sxs-lookup"><span data-stu-id="c3468-332">The for statement</span></span>

<span data-ttu-id="c3468-333">`for` 문을 초기화 식의 순서를 계산 하 고 그런 다음 조건이 true 인 동안 반복 해 서 포함된 문을 실행 하 고 일련의 반복 식 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-333">The `for` statement evaluates a sequence of initialization expressions and then, while a condition is true, repeatedly executes an embedded statement and evaluates a sequence of iteration expressions.</span></span>

```antlr
for_statement
    : 'for' '(' for_initializer? ';' for_condition? ';' for_iterator? ')' embedded_statement
    ;

for_initializer
    : local_variable_declaration
    | statement_expression_list
    ;

for_condition
    : boolean_expression
    ;

for_iterator
    : statement_expression_list
    ;

statement_expression_list
    : statement_expression (',' statement_expression)*
    ;
```

<span data-ttu-id="c3468-334">합니다 *for_initializer*있을 경우 구성 됩니다는 *local_variable_declaration* ([지역 변수 선언](statements.md#local-variable-declarations)) 또는 목록을 *statement_ 식을*s ([식 문은](statements.md#expression-statements)) 쉼표로 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-334">The *for_initializer*, if present, consists of either a *local_variable_declaration* ([Local variable declarations](statements.md#local-variable-declarations)) or a list of *statement_expression*s ([Expression statements](statements.md#expression-statements)) separated by commas.</span></span> <span data-ttu-id="c3468-335">범위에서 선언 된 지역 변수를 *for_initializer* 에서 시작 합니다 *local_variable_declarator* 변수에 대 한 포함 된 문의 끝에 확장.</span><span class="sxs-lookup"><span data-stu-id="c3468-335">The scope of a local variable declared by a *for_initializer* starts at the *local_variable_declarator* for the variable and extends to the end of the embedded statement.</span></span> <span data-ttu-id="c3468-336">범위를 포함 합니다 *for_condition* 하며 *for_iterator*.</span><span class="sxs-lookup"><span data-stu-id="c3468-336">The scope includes the *for_condition* and the *for_iterator*.</span></span>

<span data-ttu-id="c3468-337">합니다 *for_condition*있을 경우 해야를 *boolean_expression* ([부울 식](expressions.md#boolean-expressions)).</span><span class="sxs-lookup"><span data-stu-id="c3468-337">The *for_condition*, if present, must be a *boolean_expression* ([Boolean expressions](expressions.md#boolean-expressions)).</span></span>

<span data-ttu-id="c3468-338">*for_iterator*있을 경우 목록으로 구성 됩니다 *statement_expression*s ([식 문은](statements.md#expression-statements)) 쉼표로 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-338">The *for_iterator*, if present, consists of a list of *statement_expression*s ([Expression statements](statements.md#expression-statements)) separated by commas.</span></span>

<span data-ttu-id="c3468-339">문에 다음과 같이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-339">A for statement is executed as follows:</span></span>

*  <span data-ttu-id="c3468-340">경우는 *for_initializer* 있는 변수 이니셜라이저 또는 문 식 작성 되는 순서 대로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-340">If a *for_initializer* is present, the variable initializers or statement expressions are executed in the order they are written.</span></span> <span data-ttu-id="c3468-341">이 단계는 한 번만 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-341">This step is only performed once.</span></span>
*  <span data-ttu-id="c3468-342">경우는 *for_condition* 가 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-342">If a *for_condition* is present, it is evaluated.</span></span>
*  <span data-ttu-id="c3468-343">경우는 *for_condition* 아니거나 현재 평가 생성 하는 경우 `true`, 포함 문으로 제어가 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-343">If the *for_condition* is not present or if the evaluation yields `true`, control is transferred to the embedded statement.</span></span> <span data-ttu-id="c3468-344">컨트롤에 포함 된 문의 끝 지점에 도달 하는 경우 (실행에서을 `continue` 문)의 식을 합니다 *for_iterator*있는 순서 대로 평가 됩니다 하 고 다른 반복 하는 경우 평가판 시작을 수행 합니다 *for_condition* 위의 단계에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-344">When and if control reaches the end point of the embedded statement (possibly from execution of a `continue` statement), the expressions of the *for_iterator*, if any, are evaluated in sequence, and then another iteration is performed, starting with evaluation of the *for_condition* in the step above.</span></span>
*  <span data-ttu-id="c3468-345">경우는 *for_condition* 이 있고, 계산 생성 `false`의 끝점으로 제어가 `for` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-345">If the *for_condition* is present and the evaluation yields `false`, control is transferred to the end point of the `for` statement.</span></span>

<span data-ttu-id="c3468-346">포함 된 문에서 `for` 문을 `break` 문 ([break 문을](statements.md#the-break-statement)) 제어 끝점에 전송할 수 있습니다를 `for` (종료 되므로 포함 된 반복 문 문) 및 `continue` 문 ([continue 문을](statements.md#the-continue-statement)) 컨트롤의 끝점이 포함된 된 문 전송할 수 있습니다 (따라서 실행 합니다 *for_iterator* 및 또 다른 반복을 수행 합니다 `for` 문을 사용 하 여 시작 합니다 *for_condition*).</span><span class="sxs-lookup"><span data-stu-id="c3468-346">Within the embedded statement of a `for` statement, a `break` statement ([The break statement](statements.md#the-break-statement)) may be used to transfer control to the end point of the `for` statement (thus ending iteration of the embedded statement), and a `continue` statement ([The continue statement](statements.md#the-continue-statement)) may be used to transfer control to the end point of the embedded statement (thus executing the *for_iterator* and performing another iteration of the `for` statement, starting with the *for_condition*).</span></span>

<span data-ttu-id="c3468-347">포함된 문에 `for` 다음 중 하나가 참인 경우에 접근할 수:</span><span class="sxs-lookup"><span data-stu-id="c3468-347">The embedded statement of a `for` statement is reachable if one of the following is true:</span></span>

*  <span data-ttu-id="c3468-348">`for` 접근할 수 없으며 *for_condition* 가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-348">The `for` statement is reachable and no *for_condition* is present.</span></span>
*  <span data-ttu-id="c3468-349">합니다 `for` 접근할 수와 *for_condition* 있고 상수 값이 없는 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-349">The `for` statement is reachable and a *for_condition* is present and does not have the constant value `false`.</span></span>

<span data-ttu-id="c3468-350">끝점에는 `for` 다음 중 하나 이상이 true 이면 접근할 수:</span><span class="sxs-lookup"><span data-stu-id="c3468-350">The end point of a `for` statement is reachable if at least one of the following is true:</span></span>

*  <span data-ttu-id="c3468-351">합니다 `for` 문에 포함을 연결할 수 `break` 문을 끝내는 `for` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-351">The `for` statement contains a reachable `break` statement that exits the `for` statement.</span></span>
*  <span data-ttu-id="c3468-352">합니다 `for` 접근할 수와 *for_condition* 있고 상수 값이 없는 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-352">The `for` statement is reachable and a *for_condition* is present and does not have the constant value `true`.</span></span>

### <a name="the-foreach-statement"></a><span data-ttu-id="c3468-353">Foreach 문</span><span class="sxs-lookup"><span data-stu-id="c3468-353">The foreach statement</span></span>

<span data-ttu-id="c3468-354">`foreach` 문 컬렉션의 각 요소에 대해 포함된 문을 실행 하 여 컬렉션의 요소를 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-354">The `foreach` statement enumerates the elements of a collection, executing an embedded statement for each element of the collection.</span></span>

```antlr
foreach_statement
    : 'foreach' '(' local_variable_type identifier 'in' expression ')' embedded_statement
    ;
```

<span data-ttu-id="c3468-355">합니다 *형식* 및 *식별자* 의 `foreach` 문에서 선언 합니다 ***반복 변수*** 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-355">The *type* and *identifier* of a `foreach` statement declare the ***iteration variable*** of the statement.</span></span> <span data-ttu-id="c3468-356">경우는 `var` 식별자로 지정 됩니다 합니다 *local_variable_type*, 및 명명 된 형식이 없는 `var` 는 범위에 반복 변수 라고는 ***암시적으로 형식화 된 반복 변수***, 해당 종류의 요소 형식으로 간주 됩니다 및는 `foreach` 아래 지정 된 대로 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-356">If the `var` identifier is given as the *local_variable_type*, and no type named `var` is in scope, the iteration variable is said to be an ***implicitly typed iteration variable***, and its type is taken to be the element type of the `foreach` statement, as specified below.</span></span> <span data-ttu-id="c3468-357">반복 변수는 포함된 된 문을 통해 확장 하는 범위를 사용 하 여 읽기 전용 지역 변수에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-357">The iteration variable corresponds to a read-only local variable with a scope that extends over the embedded statement.</span></span> <span data-ttu-id="c3468-358">실행 하는 동안는 `foreach` 문의 반복 변수는 반복은 현재 수행 중인 컬렉션 요소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-358">During execution of a `foreach` statement, the iteration variable represents the collection element for which an iteration is currently being performed.</span></span> <span data-ttu-id="c3468-359">컴파일 타임 오류가 발생 한 포함된 문을 반복 변수를 수정 하려고 하는 경우 (할당을 통해 또는 `++` 및 `--` 연산자)으로 반복 변수를 전달 하거나를 `ref` 또는 `out` 매개 변수.</span><span class="sxs-lookup"><span data-stu-id="c3468-359">A compile-time error occurs if the embedded statement attempts to modify the iteration variable (via assignment or the `++` and `--` operators) or pass the iteration variable as a `ref` or `out` parameter.</span></span>

<span data-ttu-id="c3468-360">간단히 하기 위해 다음 표에 `IEnumerable`, `IEnumerator`, `IEnumerable<T>` 및 `IEnumerator<T>` 네임 스페이스에서 해당 형식을 참조할 `System.Collections` 및 `System.Collections.Generic`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-360">In the following, for brevity, `IEnumerable`, `IEnumerator`, `IEnumerable<T>` and `IEnumerator<T>` refer to the corresponding types in the namespaces `System.Collections` and `System.Collections.Generic`.</span></span>

<span data-ttu-id="c3468-361">Foreach 문 처리 하는 컴파일 타임 먼저 확인 합니다 ***컬렉션 형식을***, ***열거자 유형을*** 및 ***요소 형식*** 식의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-361">The compile-time processing of a foreach statement first determines the ***collection type***, ***enumerator type*** and ***element type*** of the expression.</span></span> <span data-ttu-id="c3468-362">이 결정 다음과 같이 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-362">This determination proceeds as follows:</span></span>

*  <span data-ttu-id="c3468-363">경우 형식 `X` 의 *식* 은 배열 형식에서 암시적 참조 변환 됩니다 `X` 하는 `IEnumerable` 인터페이스 (있으므로 `System.Array` 이 인터페이스를 구현).</span><span class="sxs-lookup"><span data-stu-id="c3468-363">If the type `X` of *expression* is an array type then there is an implicit reference conversion from `X` to the `IEnumerable` interface (since `System.Array` implements this interface).</span></span> <span data-ttu-id="c3468-364">***컬렉션 형식*** 는 `IEnumerable` 인터페이스는 ***열거자 유형을*** 는 `IEnumerator` 인터페이스 및 ***요소 형식*** 의 요소 형식인는 배열 형식 `X`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-364">The ***collection type*** is the `IEnumerable` interface, the ***enumerator type*** is the `IEnumerator` interface and the ***element type*** is the element type of the array type `X`.</span></span>
*  <span data-ttu-id="c3468-365">경우 형식 `X` 의 *식* 됩니다 `dynamic` 는 암시적으로 변환 됩니다 *식* 에 `IEnumerable` 인터페이스 ([암시적 동적 변환](conversions.md#implicit-dynamic-conversions)).</span><span class="sxs-lookup"><span data-stu-id="c3468-365">If the type `X` of *expression* is `dynamic` then there is an implicit conversion from *expression* to the `IEnumerable` interface ([Implicit dynamic conversions](conversions.md#implicit-dynamic-conversions)).</span></span> <span data-ttu-id="c3468-366">***컬렉션 형식*** 은 합니다 `IEnumerable` 인터페이스 및 ***열거자 유형을*** 는 `IEnumerator` 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="c3468-366">The ***collection type*** is the `IEnumerable` interface and the ***enumerator type*** is the `IEnumerator` interface.</span></span> <span data-ttu-id="c3468-367">경우는 `var` 식별자로 지정 됩니다는 *local_variable_type* 그런 다음 ***요소 형식*** 는 `dynamic`, 그렇지 않으면 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-367">If the `var` identifier is given as the *local_variable_type* then the ***element type*** is `dynamic`, otherwise it is `object`.</span></span>
*  <span data-ttu-id="c3468-368">그렇지 않은 경우 확인 여부를 형식 `X` 에 적절 한 `GetEnumerator` 메서드:</span><span class="sxs-lookup"><span data-stu-id="c3468-368">Otherwise, determine whether the type `X` has an appropriate `GetEnumerator` method:</span></span>
   * <span data-ttu-id="c3468-369">형식에서 멤버 조회를 수행 `X` 식별자를 사용 하 여 `GetEnumerator` 형식 인수 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-369">Perform member lookup on the type `X` with identifier `GetEnumerator` and no type arguments.</span></span> <span data-ttu-id="c3468-370">멤버 조회 일치 항목을 생성 하지 않거나 모호성이, 또는 메서드 그룹이 없는 일치 하는, 아래 설명 된 대로 열거 가능한 인터페이스에 대 한 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-370">If the member lookup does not produce a match, or it produces an ambiguity, or produces a match that is not a method group, check for an enumerable interface as described below.</span></span> <span data-ttu-id="c3468-371">멤버 조회는 메서드 그룹 또는 일치를 제외한 모든 항목을 생성 하는 경우 경고가 발생 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-371">It is recommended that a warning be issued if member lookup produces anything except a method group or no match.</span></span>
   * <span data-ttu-id="c3468-372">빈 인수 목록 및 생성 된 메서드 그룹을 사용 하 여 오버 로드 확인을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-372">Perform overload resolution using the resulting method group and an empty argument list.</span></span> <span data-ttu-id="c3468-373">오버 로드 확인 결과에서 해당 메서드가 없는 경우 모호성을 발생 하거나 가장 적합 한 메서드가 해당 메서드가 아래 설명 된 대로 열거 가능한 인터페이스에 대 한 정적 또는 공용이 아닙니다 확인이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-373">If overload resolution results in no applicable methods, results in an ambiguity, or results in a single best method but that method is either static or not public, check for an enumerable interface as described below.</span></span> <span data-ttu-id="c3468-374">오버 로드 확인 모호 하지 않은 공용 인스턴스 메서드 또는 해당 메서드가 없는 제외한 모든 항목을 생성 하는 경우 경고가 발생 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-374">It is recommended that a warning be issued if overload resolution produces anything except an unambiguous public instance method or no applicable methods.</span></span>
   * <span data-ttu-id="c3468-375">반환 형식이 `E` 의 `GetEnumerator` 메서드는 클래스, 구조체 또는 인터페이스 형식, 오류가 생성 됩니다 아니며 추가 단계가 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-375">If the return type `E` of the `GetEnumerator` method is not a class, struct or interface type, an error is produced and no further steps are taken.</span></span>
   * <span data-ttu-id="c3468-376">멤버 조회에 이루어집니다 `E` 식별자를 사용 하 여 `Current` 형식 인수 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-376">Member lookup is performed on `E` with the identifier `Current` and no type arguments.</span></span> <span data-ttu-id="c3468-377">멤버 조회에 일치 하는 항목이 생성, 결과 오류 또는 결과 읽기를 허용 하는 공용 인스턴스 속성을 제외 하 고, 경우에 오류가 생성 되 고 추가 단계가 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-377">If the member lookup produces no match, the result is an error, or the result is anything except a public instance property that permits reading, an error is produced and no further steps are taken.</span></span>
   * <span data-ttu-id="c3468-378">멤버 조회에 이루어집니다 `E` 식별자를 사용 하 여 `MoveNext` 형식 인수 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-378">Member lookup is performed on `E` with the identifier `MoveNext` and no type arguments.</span></span> <span data-ttu-id="c3468-379">멤버 조회에 일치 하는 항목이 생성, 결과 오류 또는 결과 메서드 그룹을 제외 하 고, 경우에 오류가 생성 되 고 추가 단계가 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-379">If the member lookup produces no match, the result is an error, or the result is anything except a method group, an error is produced and no further steps are taken.</span></span>
   * <span data-ttu-id="c3468-380">오버 로드 확인은 빈 인수 목록이 있는 메서드 그룹에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-380">Overload resolution is performed on the method group with an empty argument list.</span></span> <span data-ttu-id="c3468-381">없는 해당 메서드, 모호성을에서 제거 결과 나 결과에 가장 적합 한 메서드가 해당 메서드 오버 로드 확인 결과 정적 또는 공용이 아닙니다 되었거나 해당 반환 형식이 없는 경우 `bool`오류가 생성 되 고 추가 단계가 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-381">If overload resolution results in no applicable methods, results in an ambiguity, or results in a single best method but that method is either static or not public, or its return type is not `bool`, an error is produced and no further steps are taken.</span></span>
   * <span data-ttu-id="c3468-382">***컬렉션 형식*** 는 `X`의 ***열거자 유형을*** 은 `E`, 및 ***요소 형식*** 유형의 `Current` 속성.</span><span class="sxs-lookup"><span data-stu-id="c3468-382">The ***collection type*** is `X`, the ***enumerator type*** is `E`, and the ***element type*** is the type of the `Current` property.</span></span>

*  <span data-ttu-id="c3468-383">그렇지 않으면 열거 가능한 인터페이스에 대 한 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-383">Otherwise, check for an enumerable interface:</span></span>
   * <span data-ttu-id="c3468-384">경우 모든 형식 간의 `Ti` 에 암시적 변환이 `X` 에 `IEnumerable<Ti>`, 고유한 유형이 `T` 되도록 `T` 아닙니다 `dynamic` 및 다른 모든 `Ti` 있는지는 암시적으로 변환 `IEnumerable<T>` 에 `IEnumerable<Ti>`, 해당 ***컬렉션 형식*** 는 인터페이스 `IEnumerable<T>`의 ***열거자 유형을*** 인터페이스`IEnumerator<T>`, 및 ***요소 형식이*** 는 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-384">If among all the types `Ti` for which there is an implicit conversion from `X` to `IEnumerable<Ti>`, there is a unique type `T` such that `T` is not `dynamic` and for all the other `Ti` there is an implicit conversion from `IEnumerable<T>` to `IEnumerable<Ti>`, then the ***collection type*** is the interface `IEnumerable<T>`, the ***enumerator type*** is the interface `IEnumerator<T>`, and the ***element type*** is `T`.</span></span>
   * <span data-ttu-id="c3468-385">이러한 형식이 둘 이상 있으면 그러지 `T`, 다음 오류가 생성 되 고 추가 단계가 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-385">Otherwise, if there is more than one such type `T`, then an error is produced and no further steps are taken.</span></span>
   * <span data-ttu-id="c3468-386">암시적 변환이 없는 경우에 그렇지 `X` 에 `System.Collections.IEnumerable` 인터페이스를 해당 ***컬렉션 형식*** 는이 인터페이스는 ***열거자 유형을*** 인터페이스입니다`System.Collections.IEnumerator`, 및 ***요소 형식이*** 는 `object`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-386">Otherwise, if there is an implicit conversion from `X` to the `System.Collections.IEnumerable` interface, then the ***collection type*** is this interface, the ***enumerator type*** is the interface `System.Collections.IEnumerator`, and the ***element type*** is `object`.</span></span>
   * <span data-ttu-id="c3468-387">그렇지 않으면 오류가 발생 하 고 추가 단계가 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-387">Otherwise, an error is produced and no further steps are taken.</span></span>

<span data-ttu-id="c3468-388">위의 단계를 성공 하면 컬렉션 형식을 생성할 명확 `C`, 열거자 유형을 `E` 형식과 요소 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-388">The above steps, if successful, unambiguously produce a collection type `C`, enumerator type `E` and element type `T`.</span></span> <span data-ttu-id="c3468-389">폼의 foreach 문</span><span class="sxs-lookup"><span data-stu-id="c3468-389">A foreach statement of the form</span></span>
```csharp
foreach (V v in x) embedded_statement
```
<span data-ttu-id="c3468-390">확장 한 다음:</span><span class="sxs-lookup"><span data-stu-id="c3468-390">is then expanded to:</span></span>
```csharp
{
    E e = ((C)(x)).GetEnumerator();
    try {
        while (e.MoveNext()) {
            V v = (V)(T)e.Current;
            embedded_statement
        }
    }
    finally {
        ... // Dispose e
    }
}
```

<span data-ttu-id="c3468-391">변수의 `e` 표시 또는 식에 액세스할 수 없는 `x` 포함된 문을 또는 프로그램의 다른 소스 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-391">The variable `e` is not visible to or accessible to the expression `x` or the embedded statement or any other source code of the program.</span></span> <span data-ttu-id="c3468-392">변수의 `v` 포함 된 문에서 읽기 전용입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-392">The variable `v` is read-only in the embedded statement.</span></span> <span data-ttu-id="c3468-393">명시적 변환이 없는 경우 ([명시적 변환](conversions.md#explicit-conversions))에서 `T` (요소 형식)에 `V` (합니다 *local_variable_type* foreach 문에서), 오류가 발생 및 추가 단계가 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-393">If there is not an explicit conversion ([Explicit conversions](conversions.md#explicit-conversions)) from `T` (the element type) to `V` (the *local_variable_type* in the foreach statement), an error is produced and no further steps are taken.</span></span> <span data-ttu-id="c3468-394">하는 경우 `x` 기본값이 `null`, `System.NullReferenceException` 런타임에 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-394">If `x` has the value `null`, a `System.NullReferenceException` is thrown at run-time.</span></span>

<span data-ttu-id="c3468-395">동작은 위의 확장과 일치으로 성능상의 이유로, 예: 지정 된 foreach 문에서 다르게 구현에 구현을 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-395">An implementation is permitted to implement a given foreach-statement differently, e.g. for performance reasons, as long as the behavior is consistent with the above expansion.</span></span>

<span data-ttu-id="c3468-396">배치 `v` while 루프는 익명 함수에서 발생 하 여 캡처 방법에 대 한 중요 합니다 *embedded_statement*합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-396">The placement of `v` inside the while loop is important for how it is captured by any anonymous function occurring in the *embedded_statement*.</span></span>

<span data-ttu-id="c3468-397">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c3468-397">For example:</span></span>
```csharp
int[] values = { 7, 9, 13 };
Action f = null;

foreach (var value in values)
{
    if (f == null) f = () => Console.WriteLine("First value: " + value);
}

f();
```
<span data-ttu-id="c3468-398">경우 `v` while 외부에서 선언 된 루프 후 해당 값 및 모든 반복 간에 공유할 수는에 대 한 루프 최종 값을 `13`, 인 어떤 호출 `f` 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-398">If `v` was declared outside of the while loop, it would be shared among all iterations, and its value after the for loop would be the final value, `13`, which is what the invocation of `f` would print.</span></span> <span data-ttu-id="c3468-399">대신, 각 반복에 고유한 변수 때문에 `v`에서 캡처한 것 `f` 첫 번째에서 반복 값을 보유할 계속 `7`, 인쇄 될 모양을입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-399">Instead, because each iteration has its own variable `v`, the one captured by `f` in the first iteration will continue to hold the value `7`, which is what will be printed.</span></span> <span data-ttu-id="c3468-400">(참고: 이전 버전의 C# 선언 `v` 외부 while 루프.)</span><span class="sxs-lookup"><span data-stu-id="c3468-400">(Note: earlier versions of C# declared `v` outside of the while loop.)</span></span>

<span data-ttu-id="c3468-401">본문은 블록 다음 단계에 따라 생성 되는 마지막으로:</span><span class="sxs-lookup"><span data-stu-id="c3468-401">The body of the finally block is constructed according to the following steps:</span></span>

*  <span data-ttu-id="c3468-402">암시적 변환이 없으면 `E` 에 `System.IDisposable` 다음 인터페이스</span><span class="sxs-lookup"><span data-stu-id="c3468-402">If there is an implicit conversion from `E` to the `System.IDisposable` interface, then</span></span>
   *  <span data-ttu-id="c3468-403">경우 `E` nullable이 아닌 값 형식인 경우 의미 체계에 해당 하는 절 확장 되어 마지막:</span><span class="sxs-lookup"><span data-stu-id="c3468-403">If `E` is a non-nullable value type then the finally clause is expanded to the semantic equivalent  of:</span></span>

      ```csharp
      finally {
          ((System.IDisposable)e).Dispose();
      }
      ```

   *  <span data-ttu-id="c3468-404">그렇지 않은 경우의 의미 체계에 해당 하는 절 확장 되어 마지막:</span><span class="sxs-lookup"><span data-stu-id="c3468-404">Otherwise the finally clause is expanded to the semantic equivalent of:</span></span>

      ```csharp
      finally {
          if (e != null) ((System.IDisposable)e).Dispose();
      }
      ```

   <span data-ttu-id="c3468-405">단 `E` 값 형식 인지 값 형식으로 캐스팅을 인스턴스화할 형식 매개 변수 `e` 에 `System.IDisposable` 되려면 boxing이 발생 하지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-405">except that if `E` is a value type, or a type parameter instantiated to a value type, then the cast of `e` to `System.IDisposable` will not cause boxing to occur.</span></span>

*  <span data-ttu-id="c3468-406">그렇지 않은 경우, `E` 형식이 봉인 된 절은 빈 블록으로 확장 되는 마지막으로:</span><span class="sxs-lookup"><span data-stu-id="c3468-406">Otherwise, if `E` is a sealed type, the finally clause is expanded to an empty block:</span></span>

   ```csharp
   finally {
   }
   ```

*  <span data-ttu-id="c3468-407">그렇지 않은 경우는 마지막 절을 확장 하 여:</span><span class="sxs-lookup"><span data-stu-id="c3468-407">Otherwise, the finally clause is expanded to:</span></span>

   ```csharp
   finally {
       System.IDisposable d = e as System.IDisposable;
       if (d != null) d.Dispose();
   }
   ```    

   <span data-ttu-id="c3468-408">지역 변수 `d` 에 보이지 않거나 사용자 코드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-408">The local variable `d` is not visible to or accessible to any user code.</span></span> <span data-ttu-id="c3468-409">특히 해당 범위에 포함 되는 다른 모든 변수와 충돌 하지 않는 finally 블록을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-409">In particular, it does not conflict with any other variable whose scope includes the finally block.</span></span>

<span data-ttu-id="c3468-410">순서 `foreach` 배열의 요소를 이동 하면서, 다음과 같습니다: 단일 차원 배열의 요소 인덱스의 오름차순으로 트래버스 됩니다에 대 한 인덱스를 사용 하 여 시작 `0` 인덱스까지 `Length - 1`입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-410">The order in which `foreach` traverses the elements of an array, is as follows: For single-dimensional arrays elements are traversed in increasing index order, starting with index `0` and ending with index `Length - 1`.</span></span> <span data-ttu-id="c3468-411">다차원 배열에 대 한 요소는 오른쪽에 있는 차원의 인덱스가 향상 된 첫 번째 왼쪽에 등 다음 왼쪽된 차원 트래버스 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-411">For multi-dimensional arrays, elements are traversed such that the indices of the rightmost dimension are increased first, then the next left dimension, and so on to the left.</span></span>

<span data-ttu-id="c3468-412">다음 예제에서는 요소 순서에서 2 차원 배열의 각 값 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-412">The following example prints out each value in a two-dimensional array, in element order:</span></span>
```csharp
using System;

class Test
{
    static void Main() {
        double[,] values = {
            {1.2, 2.3, 3.4, 4.5},
            {5.6, 6.7, 7.8, 8.9}
        };

        foreach (double elementValue in values)
            Console.Write("{0} ", elementValue);

        Console.WriteLine();
    }
}
```
<span data-ttu-id="c3468-413">생성 된 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-413">The output produced is as follows:</span></span>
```csharp
1.2 2.3 3.4 4.5 5.6 6.7 7.8 8.9
```

<span data-ttu-id="c3468-414">예제</span><span class="sxs-lookup"><span data-stu-id="c3468-414">In the example</span></span>
```csharp
int[] numbers = { 1, 3, 5, 7, 9 };
foreach (var n in numbers) Console.WriteLine(n);
```
<span data-ttu-id="c3468-415">유형의 `n` 로 유추 됩니다 `int`의 요소 형식 `numbers`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-415">the type of `n` is inferred to be `int`, the element type of `numbers`.</span></span>

## <a name="jump-statements"></a><span data-ttu-id="c3468-416">점프 문</span><span class="sxs-lookup"><span data-stu-id="c3468-416">Jump statements</span></span>

<span data-ttu-id="c3468-417">무조건 점프 문이 제어를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-417">Jump statements unconditionally transfer control.</span></span>

```antlr
jump_statement
    : break_statement
    | continue_statement
    | goto_statement
    | return_statement
    | throw_statement
    ;
```

<span data-ttu-id="c3468-418">점프 문이 제어를 전송 하는 위치 라고 합니다 ***대상*** 점프 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-418">The location to which a jump statement transfers control is called the ***target*** of the jump statement.</span></span>

<span data-ttu-id="c3468-419">점프 문 블록 내에서 발생 하 고 해당 점프 문의 대상이 블록 외부에 점프 문을 라고 ***종료*** 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-419">When a jump statement occurs within a block, and the target of that jump statement is outside that block, the jump statement is said to ***exit*** the block.</span></span> <span data-ttu-id="c3468-420">점프 문 블록 밖으로 제어를 전송할 수 있습니다, 있지만 블록으로 제어를 전송 하지 않습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-420">While a jump statement may transfer control out of a block, it can never transfer control into a block.</span></span>

<span data-ttu-id="c3468-421">중간으로 점프 문의 실행은 복잡 `try` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-421">Execution of jump statements is complicated by the presence of intervening `try` statements.</span></span> <span data-ttu-id="c3468-422">예: 없는 경우에서 `try` 문, 점프 문에 무조건에서 제어를 전달 점프 문이 해당 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-422">In the absence of such `try` statements, a jump statement unconditionally transfers control from the jump statement to its target.</span></span> <span data-ttu-id="c3468-423">이러한 중간 경우 `try` 문 실행은 더 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-423">In the presence of such intervening `try` statements, execution is more complex.</span></span> <span data-ttu-id="c3468-424">하나 이상의 점프 문이 종료 되 면 `try` 블록에 연결 `finally` 제어 블록은 처음에 전송 합니다 `finally` 가장 안쪽의 블록 `try` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-424">If the jump statement exits one or more `try` blocks with associated `finally` blocks, control is initially transferred to the `finally` block of the innermost `try` statement.</span></span> <span data-ttu-id="c3468-425">컨트롤의 끝점에 도달 하는 경우는 `finally` 컨트롤 블록으로 전송 됩니다는 `finally` 다음 바깥쪽 블록 `try` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-425">When and if control reaches the end point of a `finally` block, control is transferred to the `finally` block of the next enclosing `try` statement.</span></span> <span data-ttu-id="c3468-426">때까지이 프로세스를 반복 합니다 `finally` 모두의 블록 중간 `try` 문이 실행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-426">This process is repeated until the `finally` blocks of all intervening `try` statements have been executed.</span></span>

<span data-ttu-id="c3468-427">예제</span><span class="sxs-lookup"><span data-stu-id="c3468-427">In the example</span></span>
```csharp
using System;

class Test
{
    static void Main() {
        while (true) {
            try {
                try {
                    Console.WriteLine("Before break");
                    break;
                }
                finally {
                    Console.WriteLine("Innermost finally block");
                }
            }
            finally {
                Console.WriteLine("Outermost finally block");
            }
        }
        Console.WriteLine("After break");
    }
}
```
<span data-ttu-id="c3468-428">합니다 `finally` 블록과 연결 된 두 `try` 점프 문의 대상이 제어가 전에 문이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-428">the `finally` blocks associated with two `try` statements are executed before control is transferred to the target of the jump statement.</span></span>

<span data-ttu-id="c3468-429">생성 된 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-429">The output produced is as follows:</span></span>
```
Before break
Innermost finally block
Outermost finally block
After break
```

### <a name="the-break-statement"></a><span data-ttu-id="c3468-430">Break 문</span><span class="sxs-lookup"><span data-stu-id="c3468-430">The break statement</span></span>

<span data-ttu-id="c3468-431">합니다 `break` 문은 가장 가까운 바깥쪽 종료 `switch`, `while`, `do`를 `for`, 또는 `foreach` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-431">The `break` statement exits the nearest enclosing `switch`, `while`, `do`, `for`, or `foreach` statement.</span></span>

```antlr
break_statement
    : 'break' ';'
    ;
```

<span data-ttu-id="c3468-432">대상을 `break` 문은 가장 가까운 바깥쪽 끝 지점인 `switch`, `while`, `do`를 `for`, 또는 `foreach` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-432">The target of a `break` statement is the end point of the nearest enclosing `switch`, `while`, `do`, `for`, or `foreach` statement.</span></span> <span data-ttu-id="c3468-433">경우는 `break` 문에 포함 되지 않는를 `switch`, `while`, `do`, `for`, 또는 `foreach` 문에 컴파일 타임 오류가 발생 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-433">If a `break` statement is not enclosed by a `switch`, `while`, `do`, `for`, or `foreach` statement, a compile-time error occurs.</span></span>

<span data-ttu-id="c3468-434">때 여러 `switch`, `while`를 `do`, `for`, 또는 `foreach` 문을 서로 중첩 되어를 `break` 문은 가장 안쪽의 문을에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-434">When multiple `switch`, `while`, `do`, `for`, or `foreach` statements are nested within each other, a `break` statement applies only to the innermost statement.</span></span> <span data-ttu-id="c3468-435">여러 중첩 수준에서 제어를 전송 하는 `goto` 문 ([goto 문을](statements.md#the-goto-statement))를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-435">To transfer control across multiple nesting levels, a `goto` statement ([The goto statement](statements.md#the-goto-statement)) must be used.</span></span>

<span data-ttu-id="c3468-436">A `break` 문을 종료할 수 없는 한 `finally` 블록 ([try 문](statements.md#the-try-statement)).</span><span class="sxs-lookup"><span data-stu-id="c3468-436">A `break` statement cannot exit a `finally` block ([The try statement](statements.md#the-try-statement)).</span></span> <span data-ttu-id="c3468-437">때를 `break` 문 내에서 발생을 `finally` 블록의 대상을 `break` 문은 동일한 이어야 합니다. `finally` 차단. 그렇지 않으면 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-437">When a `break` statement occurs within a `finally` block, the target of the `break` statement must be within the same `finally` block; otherwise, a compile-time error occurs.</span></span>

<span data-ttu-id="c3468-438">`break` 문을 다음과 같이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-438">A `break` statement is executed as follows:</span></span>

*  <span data-ttu-id="c3468-439">경우는 `break` 문은 하나 이상의 종료 `try` 블록에 연결 `finally` 제어 블록은 처음에 전송 합니다 `finally` 가장 안쪽의 블록 `try` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-439">If the `break` statement exits one or more `try` blocks with associated `finally` blocks, control is initially transferred to the `finally` block of the innermost `try` statement.</span></span> <span data-ttu-id="c3468-440">컨트롤의 끝점에 도달 하는 경우는 `finally` 컨트롤 블록으로 전송 됩니다는 `finally` 다음 바깥쪽 블록 `try` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-440">When and if control reaches the end point of a `finally` block, control is transferred to the `finally` block of the next enclosing `try` statement.</span></span> <span data-ttu-id="c3468-441">때까지이 프로세스를 반복 합니다 `finally` 모두의 블록 중간 `try` 문이 실행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-441">This process is repeated until the `finally` blocks of all intervening `try` statements have been executed.</span></span>
*  <span data-ttu-id="c3468-442">대상에 제어가 `break` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-442">Control is transferred to the target of the `break` statement.</span></span>

<span data-ttu-id="c3468-443">때문에 `break` 문을 무조건 제어 전송 다른 곳에서 끝점에는 `break` 문에 접근할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-443">Because a `break` statement unconditionally transfers control elsewhere, the end point of a `break` statement is never reachable.</span></span>

### <a name="the-continue-statement"></a><span data-ttu-id="c3468-444">Continue 문</span><span class="sxs-lookup"><span data-stu-id="c3468-444">The continue statement</span></span>

<span data-ttu-id="c3468-445">합니다 `continue` 문은 가장 가까운 바깥쪽의 새로운 반복을 시작 `while`, `do`, `for`, 또는 `foreach` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-445">The `continue` statement starts a new iteration of the nearest enclosing `while`, `do`, `for`, or `foreach` statement.</span></span>

```antlr
continue_statement
    : 'continue' ';'
    ;
```

<span data-ttu-id="c3468-446">대상을 `continue` 문은 가장 가까운 바깥쪽 포함 된 문의 끝 점이 `while`, `do`, `for`, 또는 `foreach` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-446">The target of a `continue` statement is the end point of the embedded statement of the nearest enclosing `while`, `do`, `for`, or `foreach` statement.</span></span> <span data-ttu-id="c3468-447">경우는 `continue` 문에 포함 되지 않는를 `while`, `do`, `for`, 또는 `foreach` 문에 컴파일 타임 오류가 발생 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-447">If a `continue` statement is not enclosed by a `while`, `do`, `for`, or `foreach` statement, a compile-time error occurs.</span></span>

<span data-ttu-id="c3468-448">때 여러 `while`, `do`를 `for`, 또는 `foreach` 문을 서로 중첩 되어를 `continue` 문은 가장 안쪽의 문을에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-448">When multiple `while`, `do`, `for`, or `foreach` statements are nested within each other, a `continue` statement applies only to the innermost statement.</span></span> <span data-ttu-id="c3468-449">여러 중첩 수준에서 제어를 전송 하는 `goto` 문 ([goto 문을](statements.md#the-goto-statement))를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-449">To transfer control across multiple nesting levels, a `goto` statement ([The goto statement](statements.md#the-goto-statement)) must be used.</span></span>

<span data-ttu-id="c3468-450">A `continue` 문을 종료할 수 없는 한 `finally` 블록 ([try 문](statements.md#the-try-statement)).</span><span class="sxs-lookup"><span data-stu-id="c3468-450">A `continue` statement cannot exit a `finally` block ([The try statement](statements.md#the-try-statement)).</span></span> <span data-ttu-id="c3468-451">경우는 `continue` 문 내에서 발생를 `finally` 블록의 대상을 `continue` 문은 동일한 이어야 합니다. `finally` ; 그렇지 않으면 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-451">When a `continue` statement occurs within a `finally` block, the target of the `continue` statement must be within the same `finally` block; otherwise a compile-time error occurs.</span></span>

<span data-ttu-id="c3468-452">`continue` 문을 다음과 같이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-452">A `continue` statement is executed as follows:</span></span>

*  <span data-ttu-id="c3468-453">경우는 `continue` 문은 하나 이상의 종료 `try` 블록에 연결 `finally` 제어 블록은 처음에 전송 합니다 `finally` 가장 안쪽의 블록 `try` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-453">If the `continue` statement exits one or more `try` blocks with associated `finally` blocks, control is initially transferred to the `finally` block of the innermost `try` statement.</span></span> <span data-ttu-id="c3468-454">컨트롤의 끝점에 도달 하는 경우는 `finally` 컨트롤 블록으로 전송 됩니다는 `finally` 다음 바깥쪽 블록 `try` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-454">When and if control reaches the end point of a `finally` block, control is transferred to the `finally` block of the next enclosing `try` statement.</span></span> <span data-ttu-id="c3468-455">때까지이 프로세스를 반복 합니다 `finally` 모두의 블록 중간 `try` 문이 실행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-455">This process is repeated until the `finally` blocks of all intervening `try` statements have been executed.</span></span>
*  <span data-ttu-id="c3468-456">대상에 제어가 `continue` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-456">Control is transferred to the target of the `continue` statement.</span></span>

<span data-ttu-id="c3468-457">때문에 `continue` 문을 무조건 제어 전송 다른 곳에서 끝점에는 `continue` 문에 접근할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-457">Because a `continue` statement unconditionally transfers control elsewhere, the end point of a `continue` statement is never reachable.</span></span>

### <a name="the-goto-statement"></a><span data-ttu-id="c3468-458">goto 문</span><span class="sxs-lookup"><span data-stu-id="c3468-458">The goto statement</span></span>

<span data-ttu-id="c3468-459">`goto` 문은 레이블에 의해 표시 된 문으로 제어를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-459">The `goto` statement transfers control to a statement that is marked by a label.</span></span>

```antlr
goto_statement
    : 'goto' identifier ';'
    | 'goto' 'case' constant_expression ';'
    | 'goto' 'default' ';'
    ;
```

<span data-ttu-id="c3468-460">대상 된 `goto` *식별자* 문은 지정 된 레이블로 레이블이 지정 된 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-460">The target of a `goto` *identifier* statement is the labeled statement with the given label.</span></span> <span data-ttu-id="c3468-461">지정 된 이름을 사용 하 여 레이블을 현재 함수 멤버에 존재 하지 않는 경우 또는 경우는 `goto` 문은 아닙니다 레이블의 범위 내에서 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-461">If a label with the given name does not exist in the current function member, or if the `goto` statement is not within the scope of the label, a compile-time error occurs.</span></span> <span data-ttu-id="c3468-462">이 규칙에 사용할 수는 `goto` 문은 중첩 된 범위를 벗어날 포함 되지 않습니다 중첩된 된 범위 컨트롤을 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-462">This rule permits the use of a `goto` statement to transfer control out of a nested scope, but not into a nested scope.</span></span> <span data-ttu-id="c3468-463">예제</span><span class="sxs-lookup"><span data-stu-id="c3468-463">In the example</span></span>
```csharp
using System;

class Test
{
    static void Main(string[] args) {
        string[,] table = {
            {"Red", "Blue", "Green"},
            {"Monday", "Wednesday", "Friday"}
        };

        foreach (string str in args) {
            int row, colm;
            for (row = 0; row <= 1; ++row)
                for (colm = 0; colm <= 2; ++colm)
                    if (str == table[row,colm])
                         goto done;

            Console.WriteLine("{0} not found", str);
            continue;
    done:
            Console.WriteLine("Found {0} at [{1}][{2}]", str, row, colm);
        }
    }
}
```
<span data-ttu-id="c3468-464">`goto` 문을 사용 하 여 중첩 된 범위 밖으로 제어를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-464">a `goto` statement is used to transfer control out of a nested scope.</span></span>

<span data-ttu-id="c3468-465">대상을 `goto case` 문에 가장 가까운 바깥쪽에서 문 목록의 `switch` 문 ([switch 문](statements.md#the-switch-statement))를 포함 하는 `case` 주어진된 상수 값을 사용 하 여 레이블을.</span><span class="sxs-lookup"><span data-stu-id="c3468-465">The target of a `goto case` statement is the statement list in the immediately enclosing `switch` statement ([The switch statement](statements.md#the-switch-statement)), which contains a `case` label with the given constant value.</span></span> <span data-ttu-id="c3468-466">경우는 `goto case` 문에 포함 되지 않는를 `switch` 문을 경우는 *constant_expression* 암시적으로 변환 되지 않습니다 ([암시적 변환을](conversions.md#implicit-conversions)) 관리 형식에는 바깥쪽에 가장 가까운 `switch` 문 또는 경우에 가장 가까운 바깥쪽 `switch` 문에 포함 되지 않습니다는 `case` 컴파일 타임 오류가 발생 하는 주어진된 상수 값을 사용 하 여 레이블.</span><span class="sxs-lookup"><span data-stu-id="c3468-466">If the `goto case` statement is not enclosed by a `switch` statement, if the *constant_expression* is not implicitly convertible ([Implicit conversions](conversions.md#implicit-conversions)) to the governing type of the nearest enclosing `switch` statement, or if the nearest enclosing `switch` statement does not contain a `case` label with the given constant value, a compile-time error occurs.</span></span>

<span data-ttu-id="c3468-467">대상을 `goto default` 문에 가장 가까운 바깥쪽에서 문 목록의 `switch` 문 ([switch 문](statements.md#the-switch-statement))를 포함 하는 `default` 레이블.</span><span class="sxs-lookup"><span data-stu-id="c3468-467">The target of a `goto default` statement is the statement list in the immediately enclosing `switch` statement ([The switch statement](statements.md#the-switch-statement)), which contains a `default` label.</span></span> <span data-ttu-id="c3468-468">경우는 `goto default` 문에 포함 되지 않는를 `switch` 문을 경우 가장 가까운 바깥쪽 `switch` 문에 포함 되지 않습니다는 `default` 레이블, 컴파일 시간 오류가 발생 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-468">If the `goto default` statement is not enclosed by a `switch` statement, or if the nearest enclosing `switch` statement does not contain a `default` label, a compile-time error occurs.</span></span>

<span data-ttu-id="c3468-469">A `goto` 문을 종료할 수 없는 한 `finally` 블록 ([try 문](statements.md#the-try-statement)).</span><span class="sxs-lookup"><span data-stu-id="c3468-469">A `goto` statement cannot exit a `finally` block ([The try statement](statements.md#the-try-statement)).</span></span> <span data-ttu-id="c3468-470">경우는 `goto` 문 내에서 발생을 `finally` 블록의 대상을 `goto` 문은 동일한 이어야 합니다. `finally` 블록 그렇지 않으면 컴파일 타임 오류가 발생 하거나.</span><span class="sxs-lookup"><span data-stu-id="c3468-470">When a `goto` statement occurs within a `finally` block, the target of the `goto` statement must be within the same `finally` block, or otherwise a compile-time error occurs.</span></span>

<span data-ttu-id="c3468-471">`goto` 문을 다음과 같이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-471">A `goto` statement is executed as follows:</span></span>

*  <span data-ttu-id="c3468-472">경우는 `goto` 문은 하나 이상의 종료 `try` 블록에 연결 `finally` 제어 블록은 처음에 전송 합니다 `finally` 가장 안쪽의 블록 `try` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-472">If the `goto` statement exits one or more `try` blocks with associated `finally` blocks, control is initially transferred to the `finally` block of the innermost `try` statement.</span></span> <span data-ttu-id="c3468-473">컨트롤의 끝점에 도달 하는 경우는 `finally` 컨트롤 블록으로 전송 됩니다는 `finally` 다음 바깥쪽 블록 `try` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-473">When and if control reaches the end point of a `finally` block, control is transferred to the `finally` block of the next enclosing `try` statement.</span></span> <span data-ttu-id="c3468-474">때까지이 프로세스를 반복 합니다 `finally` 모두의 블록 중간 `try` 문이 실행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-474">This process is repeated until the `finally` blocks of all intervening `try` statements have been executed.</span></span>
*  <span data-ttu-id="c3468-475">대상에 제어가 `goto` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-475">Control is transferred to the target of the `goto` statement.</span></span>

<span data-ttu-id="c3468-476">때문에 `goto` 문을 무조건 제어 전송 다른 곳에서 끝점에는 `goto` 문에 접근할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-476">Because a `goto` statement unconditionally transfers control elsewhere, the end point of a `goto` statement is never reachable.</span></span>

### <a name="the-return-statement"></a><span data-ttu-id="c3468-477">Return 문</span><span class="sxs-lookup"><span data-stu-id="c3468-477">The return statement</span></span>

<span data-ttu-id="c3468-478">`return` 함수는 현재 호출자에 게 컨트롤을 반환 하는 명령문은 `return` 문이 나타나는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-478">The `return` statement returns control to the current caller of the function in which the `return` statement appears.</span></span>

```antlr
return_statement
    : 'return' expression? ';'
    ;
```

<span data-ttu-id="c3468-479">A `return` 식이 없는 문 결과 형식이 포함 된 메서드 즉, 값을 계산 하지 않습니다 하는 함수 멤버 에서만에서 사용할 수 있습니다 ([메서드 본문](classes.md#method-body)) `void`는 `set` 속성의 접근자 또는 인덱서는 `add` 고 `remove` 이벤트, 인스턴스 생성자, 정적 생성자 또는 소멸자의 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-479">A `return` statement with no expression can be used only in a function member that does not compute a value, that is, a method with the result type ([Method body](classes.md#method-body)) `void`, the `set` accessor of a property or indexer, the `add` and `remove` accessors of an event, an instance constructor, a static constructor, or a destructor.</span></span>

<span data-ttu-id="c3468-480">A `return` 는 void가 아닌 결과 형식이 있는 메서드 즉, 값을 계산 하는 함수 멤버 식 사용 하 여 문을 사용할 수 있습니다는 `get` 속성 또는 인덱서 또는 사용자 정의 연산자의 접근자입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-480">A `return` statement with an expression can only be used in a function member that computes a value, that is, a method with a non-void result type, the `get` accessor of a property or indexer, or a user-defined operator.</span></span> <span data-ttu-id="c3468-481">암시적으로 변환 ([암시적 변환을](conversions.md#implicit-conversions)) 식의 형식에서 포함 하는 함수 멤버의 반환 형식으로 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-481">An implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) must exist from the type of the expression to the return type of the containing function member.</span></span>

<span data-ttu-id="c3468-482">반환 문 익명 함수 식의 본문에 사용할 수도 있습니다 ([익명 함수 식](expressions.md#anonymous-function-expressions)), 이러한 함수는 변환이 존재 여부 확인에 참여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-482">Return statements can also be used in the body of anonymous function expressions ([Anonymous function expressions](expressions.md#anonymous-function-expressions)), and participate in determining which conversions exist for those functions.</span></span>

<span data-ttu-id="c3468-483">에 대 한 컴파일 시간 오류를 `return` 나타나지 문을 `finally` 블록 ([try 문](statements.md#the-try-statement)).</span><span class="sxs-lookup"><span data-stu-id="c3468-483">It is a compile-time error for a `return` statement to appear in a `finally` block ([The try statement](statements.md#the-try-statement)).</span></span>

<span data-ttu-id="c3468-484">`return` 문을 다음과 같이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-484">A `return` statement is executed as follows:</span></span>

*  <span data-ttu-id="c3468-485">경우는 `return` 문에서 식을 지정 된 식이 계산 되 고 결과 값을 암시적으로 변환 하 여 포함 된 함수의 반환 형식으로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-485">If the `return` statement specifies an expression, the expression is evaluated and the resulting value is converted to the return type of the containing function by an implicit conversion.</span></span> <span data-ttu-id="c3468-486">변환의 결과 함수에 의해 생성 된 결과 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-486">The result of the conversion becomes the result value produced by the function.</span></span>
*  <span data-ttu-id="c3468-487">경우는 `return` 문을 하나 이상으로 묶입니다 `try` 또는 `catch` 블록을 연결 된 `finally` 제어 블록은 처음에 전송 합니다 `finally` 가장 안쪽의 블록 `try` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-487">If the `return` statement is enclosed by one or more `try` or `catch` blocks with associated `finally` blocks, control is initially transferred to the `finally` block of the innermost `try` statement.</span></span> <span data-ttu-id="c3468-488">컨트롤의 끝점에 도달 하는 경우는 `finally` 컨트롤 블록으로 전송 됩니다는 `finally` 다음 바깥쪽 블록 `try` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-488">When and if control reaches the end point of a `finally` block, control is transferred to the `finally` block of the next enclosing `try` statement.</span></span> <span data-ttu-id="c3468-489">될 때까지이 프로세스를 반복 합니다 `finally` 모든 바깥쪽 블록 `try` 문이 실행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-489">This process is repeated until the `finally` blocks of all enclosing `try` statements have been executed.</span></span>
*  <span data-ttu-id="c3468-490">포함 하는 비동기 함수를 없는 경우 컨트롤이 있는 경우 결과 값과 함께 포함 된 함수의 호출자에 게 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-490">If the containing function is not an async function, control is returned to the caller of the containing function along with the result value, if any.</span></span>
*  <span data-ttu-id="c3468-491">포함 된 함수는 비동기 함수, 현재 호출자에 게 컨트롤이 반환 된 결과 값에 있는 경우에 기록 됩니다 반환 작업에 설명 된 대로 경우 ([열거자 인터페이스](classes.md#enumerator-interfaces)).</span><span class="sxs-lookup"><span data-stu-id="c3468-491">If the containing function is an async function, control is returned to the current caller, and the result value, if any, is recorded in the return task as described in ([Enumerator interfaces](classes.md#enumerator-interfaces)).</span></span>

<span data-ttu-id="c3468-492">때문에 `return` 문을 무조건 제어 전송 다른 곳에서 끝점에는 `return` 문에 접근할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-492">Because a `return` statement unconditionally transfers control elsewhere, the end point of a `return` statement is never reachable.</span></span>

### <a name="the-throw-statement"></a><span data-ttu-id="c3468-493">Throw 문</span><span class="sxs-lookup"><span data-stu-id="c3468-493">The throw statement</span></span>

<span data-ttu-id="c3468-494">`throw` 문은 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-494">The `throw` statement throws an exception.</span></span>

```antlr
throw_statement
    : 'throw' expression? ';'
    ;
```

<span data-ttu-id="c3468-495">`throw` 문 식 사용 하 여 식을 평가 하 여 생성 한 값을 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-495">A `throw` statement with an expression throws the value produced by evaluating the expression.</span></span> <span data-ttu-id="c3468-496">식은 클래스 형식 값을 표시 해야 합니다 `System.Exception`에서 파생 된 클래스 형식의 `System.Exception` 있는 매개 변수 형식 또는 `System.Exception` (또는 그 하위 클래스) 유효한 기본 클래스로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-496">The expression must denote a value of the class type `System.Exception`, of a class type that derives from `System.Exception` or of a type parameter type that has `System.Exception` (or a subclass thereof) as its effective base class.</span></span> <span data-ttu-id="c3468-497">식의 평가 생성 하는 경우 `null`, `System.NullReferenceException` 대신 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-497">If evaluation of the expression produces `null`, a `System.NullReferenceException` is thrown instead.</span></span>

<span data-ttu-id="c3468-498">A `throw` 식이 없는 문은 에서만 사용할 수 있습니다를 `catch` 문의 하 여 현재 처리 되는 예외 다시 throw 되는 경우 차단 `catch` 블록.</span><span class="sxs-lookup"><span data-stu-id="c3468-498">A `throw` statement with no expression can be used only in a `catch` block, in which case that statement re-throws the exception that is currently being handled by that `catch` block.</span></span>

<span data-ttu-id="c3468-499">때문에 `throw` 문을 무조건 제어 전송 다른 곳에서 끝점에는 `throw` 문에 접근할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-499">Because a `throw` statement unconditionally transfers control elsewhere, the end point of a `throw` statement is never reachable.</span></span>

<span data-ttu-id="c3468-500">예외가 throw 되 면 제어가 첫 번째 `catch` 바깥쪽 절 `try` 예외를 처리할 수 있는 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-500">When an exception is thrown, control is transferred to the first `catch` clause in an enclosing `try` statement that can handle the exception.</span></span> <span data-ttu-id="c3468-501">적합 한 예외 처리기로 제어를 전송 지점으로 throw 되는 예외 지점에서 발생 하는 프로세스 라고 ***예외 전파***합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-501">The process that takes place from the point of the exception being thrown to the point of transferring control to a suitable exception handler is known as ***exception propagation***.</span></span> <span data-ttu-id="c3468-502">예외가 전파 될 때까지 다음 단계를 반복 해 서 실행 구성는 `catch` 예외와 일치 하는 절을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-502">Propagation of an exception consists of repeatedly evaluating the following steps until a `catch` clause that matches the exception is found.</span></span> <span data-ttu-id="c3468-503">이 설명에는 ***지점 throw*** 위치인 처음에 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-503">In this description, the ***throw point*** is initially the location at which the exception is thrown.</span></span>

*  <span data-ttu-id="c3468-504">현재 함수 멤버의 각 `try` throw 지점을 포함 하는 문을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-504">In the current function member, each `try` statement that encloses the throw point is examined.</span></span> <span data-ttu-id="c3468-505">각 문에 대해 `S`부터 시작 하 여 가장 안쪽 `try` 문과 바깥쪽로 끝나는 `try` 문을 다음 단계를 평가:</span><span class="sxs-lookup"><span data-stu-id="c3468-505">For each statement `S`, starting with the innermost `try` statement and ending with the outermost `try` statement, the following steps are evaluated:</span></span>

   * <span data-ttu-id="c3468-506">경우는 `try` 블록 `S` 되었던 throw 지점을 포함 고 S에 하나 이상의 `catch` 절을 `catch` 절에 지정 된 규칙에 따라 예외에 대 한 적절 한 처리기를 찾으려고 모양의 순서 대로 검사 됩니다 섹션 [try 문](statements.md#the-try-statement)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-506">If the `try` block of `S` encloses the throw point and if S has one or more `catch` clauses, the `catch` clauses are examined in order of appearance to locate a suitable handler for the exception, according to the rules specified in Section [The try statement](statements.md#the-try-statement).</span></span> <span data-ttu-id="c3468-507">일치 하는 경우 `catch` 절을 블록에 제어를 전송 하 여 완료 된 예외 전파 `catch` 절.</span><span class="sxs-lookup"><span data-stu-id="c3468-507">If a matching `catch` clause is located, the exception propagation is completed by transferring control to the block of that `catch` clause.</span></span>

   * <span data-ttu-id="c3468-508">그렇지 않은 경우, 합니다 `try` 블록 또는 `catch` 블록 `S` 되었던 throw 지점을 포함 경우 `S` 에 `finally` 제어 블록으로 전송 됩니다는 `finally` 블록.</span><span class="sxs-lookup"><span data-stu-id="c3468-508">Otherwise, if the `try` block or a `catch` block of `S` encloses the throw point and if `S` has a `finally` block, control is transferred to the `finally` block.</span></span> <span data-ttu-id="c3468-509">경우는 `finally` 다른 예외를 throw 하는 블록, 현재 예외는 처리 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-509">If the `finally` block throws another exception, processing of the current exception is terminated.</span></span> <span data-ttu-id="c3468-510">컨트롤의 끝점에 도달 하는 경우 그러지는 `finally` 블록, 현재 예외 처리가 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-510">Otherwise, when control reaches the end point of the `finally` block, processing of the current exception is continued.</span></span>

*  <span data-ttu-id="c3468-511">예외 처리기가 없는 경우 현재 함수 호출에서은 함수 호출이 종료 되 면 하 고 다음 중 하나에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-511">If an exception handler was not located in the current function invocation, the function invocation is terminated, and one of the following occurs:</span></span>

   * <span data-ttu-id="c3468-512">현재 함수의 경우 비동기가 아닌 경우 위의 단계에 해당 하는 함수 멤버를 호출한 문으로 throw 지점과 함수의 호출자가 반복 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-512">If the current function is non-async, the steps above are repeated for the caller of the function with a throw point corresponding to the statement from which the function member was invoked.</span></span>

   * <span data-ttu-id="c3468-513">현재 함수가 인 비동기 작업을 반환 하는 경우 예외에 설명 된 대로 오류 또는 취소 됨 상태로 전환 됩니다는 작업의 반환에 기록 됩니다 [열거자 인터페이스](classes.md#enumerator-interfaces)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-513">If the current function is async and task-returning, the exception is recorded in the return task, which is put into a faulted or cancelled state as described in [Enumerator interfaces](classes.md#enumerator-interfaces).</span></span>

   * <span data-ttu-id="c3468-514">에 설명 된 대로 현재 스레드의 동기화 컨텍스트를 현재 함수가 void를 반환 하 고 비동기 이면 알려집니다 [열거 가능 인터페이스](classes.md#enumerable-interfaces)합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-514">If the current function is async and void-returning, the synchronization context of the current thread is notified as described in [Enumerable interfaces](classes.md#enumerable-interfaces).</span></span>

*  <span data-ttu-id="c3468-515">예외 처리 종료는 현재 스레드에서 모든 함수 멤버를 호출 하는 경우 스레드가 예외에 대 한 처리기를 나타내는 다음는 스레드는 자체 종료입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-515">If the exception processing terminates all function member invocations in the current thread, indicating that the thread has no handler for the exception, then the thread is itself terminated.</span></span> <span data-ttu-id="c3468-516">이런 종료가 미치는 구현 시 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-516">The impact of such termination is implementation-defined.</span></span>

## <a name="the-try-statement"></a><span data-ttu-id="c3468-517">Try 문</span><span class="sxs-lookup"><span data-stu-id="c3468-517">The try statement</span></span>

<span data-ttu-id="c3468-518">`try` 문 블록을 실행 하는 동안 발생 하는 예외를 catch 하기 위한 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-518">The `try` statement provides a mechanism for catching exceptions that occur during execution of a block.</span></span> <span data-ttu-id="c3468-519">또한 합니다 `try` 문은 컨트롤을 벗어나면 항상 실행 되는 코드 블록을 지정 하는 기능을 제공 합니다 `try` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-519">Furthermore, the `try` statement provides the ability to specify a block of code that is always executed when control leaves the `try` statement.</span></span>

```antlr
try_statement
    : 'try' block catch_clause+
    | 'try' block finally_clause
    | 'try' block catch_clause+ finally_clause
    ;

catch_clause
    : 'catch' exception_specifier? exception_filter?  block
    ;

exception_specifier
    : '(' type identifier? ')'
    ;

exception_filter
    : 'when' '(' expression ')'
    ;

finally_clause
    : 'finally' block
    ;
```

<span data-ttu-id="c3468-520">가능한 세 가지 형태가 `try` 문:</span><span class="sxs-lookup"><span data-stu-id="c3468-520">There are three possible forms of `try` statements:</span></span>

*  <span data-ttu-id="c3468-521">A `try` 하나 이상의 뒤에 블록 `catch` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-521">A `try` block followed by one or more `catch` blocks.</span></span>
*  <span data-ttu-id="c3468-522">A `try` 블록 뒤에 `finally` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-522">A `try` block followed by a `finally` block.</span></span>
*  <span data-ttu-id="c3468-523">A `try` 하나 이상의 블록 뒤 `catch` 뒤에 블록을 `finally` 블록.</span><span class="sxs-lookup"><span data-stu-id="c3468-523">A `try` block followed by one or more `catch` blocks followed by a `finally` block.</span></span>

<span data-ttu-id="c3468-524">경우는 `catch` 절 지정를 *exception_specifier*, 형식 이어야 `System.Exception`에서 파생 된 형식 `System.Exception` 또는 형식 매개 변수 형식에 `System.Exception` (또는 그 하위 클래스) 해당 효율적으로 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-524">When a `catch` clause specifies an *exception_specifier*, the type must be `System.Exception`, a type that derives from `System.Exception` or a type parameter type that has `System.Exception` (or a subclass thereof) as its effective base class.</span></span>

<span data-ttu-id="c3468-525">경우는 `catch` 절 모두 지정는 *exception_specifier* 사용 하 여는 *식별자*, ***예외 변수의*** 선언 된 지정 된 이름 및 형식.</span><span class="sxs-lookup"><span data-stu-id="c3468-525">When a `catch` clause specifies both an *exception_specifier* with an *identifier*, an ***exception variable*** of the given name and type is declared.</span></span> <span data-ttu-id="c3468-526">지역 변수를 통해 확장 하는 범위에 해당 하는 예외 변수는 `catch` 절.</span><span class="sxs-lookup"><span data-stu-id="c3468-526">The exception variable corresponds to a local variable with a scope that extends over the `catch` clause.</span></span> <span data-ttu-id="c3468-527">실행 하는 동안 합니다 *exception_filter* 하 고 *블록*, 예외 변수의 현재 처리 중인 예외를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-527">During execution of the *exception_filter* and *block*, the exception variable represents the exception currently being handled.</span></span> <span data-ttu-id="c3468-528">한정 된 할당 검사를 위해 예외 변수는 해당 전체 범위에 할당으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-528">For purposes of definite assignment checking, the exception variable is considered definitely assigned in its entire scope.</span></span>

<span data-ttu-id="c3468-529">하지 않는 한는 `catch` 절 예외 변수 이름이 포함, 필터에서 예외 개체에 액세스할 수 없는 및 `catch` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-529">Unless a `catch` clause includes an exception variable name, it is impossible to access the exception object in the filter and `catch` block.</span></span>

<span data-ttu-id="c3468-530">A `catch` 절을 지정 하지 않는 *exception_specifier* 는 일반 라고 `catch` 절.</span><span class="sxs-lookup"><span data-stu-id="c3468-530">A `catch` clause that does not specify an *exception_specifier* is called a general `catch` clause.</span></span>

<span data-ttu-id="c3468-531">일부 프로그래밍 언어에서 파생 된 개체에 표현할 수 없는 예외를 지원할 수 있습니다 `System.Exception`이지만 C# 코드에서 이러한 예외를 생성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-531">Some programming languages may support exceptions that are not representable as an object derived from `System.Exception`, although such exceptions could never be generated by C# code.</span></span> <span data-ttu-id="c3468-532">일반적인 `catch` 이러한 예외를 catch 할 절을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-532">A general `catch` clause may be used to catch such exceptions.</span></span> <span data-ttu-id="c3468-533">따라서 일반적인 `catch` 절은 형식을 지정 하는 의미 체계가 다르므로 `System.Exception`전자 수 다른 언어에서 예외 catch도 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-533">Thus, a general `catch` clause is semantically different from one that specifies the type `System.Exception`, in that the former may also catch exceptions from other languages.</span></span>

<span data-ttu-id="c3468-534">예외에 대 한 처리기를 찾기 위해 `catch` 절 사전적 순서 대로 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-534">In order to locate a handler for an exception, `catch` clauses are examined in lexical order.</span></span> <span data-ttu-id="c3468-535">경우는 `catch` 절 형식을 있지만 예외 필터가 지정, 나중에 대 한 것은 컴파일 타임 오류 `catch` 동일한 절 `try` 형식이 동일 하거나에서 파생 된 형식을 지정 하는 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-535">If a `catch` clause specifies a type but no exception filter, it is a compile-time error for a later `catch` clause in the same `try` statement to specify a type that is the same as, or is derived from, that type.</span></span> <span data-ttu-id="c3468-536">경우는 `catch` 형식 및 필터가 절 지정, 마지막 이어야 합니다 `catch` 절에 대 한 `try` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-536">If a `catch` clause specifies no type and no filter, it must be the last `catch` clause for that `try` statement.</span></span>

<span data-ttu-id="c3468-537">내를 `catch` 블록을 `throw` 문 ([throw 문을](statements.md#the-throw-statement)) 식 수에서 발생 된 예외 다시 throw 하는 `catch` 블록.</span><span class="sxs-lookup"><span data-stu-id="c3468-537">Within a `catch` block, a `throw` statement ([The throw statement](statements.md#the-throw-statement)) with no expression can be used to re-throw the exception that was caught by the `catch` block.</span></span> <span data-ttu-id="c3468-538">할당 된 예외 변수를 다시 throw 되는 예외를 변경 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-538">Assignments to an exception variable do not alter the exception that is re-thrown.</span></span>

<span data-ttu-id="c3468-539">예제</span><span class="sxs-lookup"><span data-stu-id="c3468-539">In the example</span></span>
```csharp
using System;

class Test
{
    static void F() {
        try {
            G();
        }
        catch (Exception e) {
            Console.WriteLine("Exception in F: " + e.Message);
            e = new Exception("F");
            throw;                // re-throw
        }
    }

    static void G() {
        throw new Exception("G");
    }

    static void Main() {
        try {
            F();
        }
        catch (Exception e) {
            Console.WriteLine("Exception in Main: " + e.Message);
        }
    }
}
```
<span data-ttu-id="c3468-540">메서드가 `F` 예외를 catch 하, 콘솔에 일부 진단 정보를 기록, 예외 변수를 변경 및 예외를 다시 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-540">the method `F` catches an exception, writes some diagnostic information to the console, alters the exception variable, and re-throws the exception.</span></span> <span data-ttu-id="c3468-541">생성 된 출력은 다시 throw 되는 예외는 원래 예외:</span><span class="sxs-lookup"><span data-stu-id="c3468-541">The exception that is re-thrown is the original exception, so the output produced is:</span></span>
```
Exception in F: G
Exception in Main: G
```

<span data-ttu-id="c3468-542">첫 번째 catch 블록에서 throw가 `e` 현재 예외를 다시 throw 하는 대신 생성 된 출력은 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-542">If the first catch block had thrown `e` instead of rethrowing the current exception, the output produced would be as follows:</span></span>
```csharp
Exception in F: G
Exception in Main: F
```

<span data-ttu-id="c3468-543">에 대 한 컴파일 시간 오류를 `break`, `continue`, 또는 `goto` 문 밖으로 제어를 전송 하는 `finally` 블록.</span><span class="sxs-lookup"><span data-stu-id="c3468-543">It is a compile-time error for a `break`, `continue`, or `goto` statement to transfer control out of a `finally` block.</span></span> <span data-ttu-id="c3468-544">경우는 `break`, `continue`, 또는 `goto` 문이에서 `finally` 문의 대상 블록은 동일한 내에 있어야 합니다. `finally` 블록 그렇지 않으면 컴파일 타임 오류가 발생 하거나 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-544">When a `break`, `continue`, or `goto` statement occurs in a `finally` block, the target of the statement must be within the same `finally` block, or otherwise a compile-time error occurs.</span></span>

<span data-ttu-id="c3468-545">에 대 한 컴파일 시간 오류를 `return` 에서 발생 하는 문을 `finally` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-545">It is a compile-time error for a `return` statement to occur in a `finally` block.</span></span>

<span data-ttu-id="c3468-546">`try` 문을 다음과 같이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-546">A `try` statement is executed as follows:</span></span>

*  <span data-ttu-id="c3468-547">제어가 `try` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-547">Control is transferred to the `try` block.</span></span>
*  <span data-ttu-id="c3468-548">컨트롤의 끝점에 도달 하는 경우는 `try` 블록:</span><span class="sxs-lookup"><span data-stu-id="c3468-548">When and if control reaches the end point of the `try` block:</span></span>
   *  <span data-ttu-id="c3468-549">경우는 `try` 문에 `finally` 블록을 `finally` 블록이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-549">If the `try` statement has a `finally` block, the `finally` block is executed.</span></span>
   *  <span data-ttu-id="c3468-550">끝점으로 제어가 `try` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-550">Control is transferred to the end point of the `try` statement.</span></span>

*  <span data-ttu-id="c3468-551">예외가 전파 되는 경우는 `try` 문을 실행 하는 동안는 `try` 블록:</span><span class="sxs-lookup"><span data-stu-id="c3468-551">If an exception is propagated to the `try` statement during execution of the `try` block:</span></span>
   *  <span data-ttu-id="c3468-552">`catch` 절에 있는 경우 순서 대로 검사 됩니다 모양의 예외에 대 한 적절 한 처리기를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-552">The `catch` clauses, if any, are examined in order of appearance to locate a suitable handler for the exception.</span></span> <span data-ttu-id="c3468-553">경우는 `catch` 절 형식을 지정 하지 않거나 예외 나 예외 형식의 기본 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-553">If a `catch` clause does not specify a type, or specifies the exception type or a base type of the exception type:</span></span>
      *  <span data-ttu-id="c3468-554">경우는 `catch` 예외 변수를 선언 하는 절, 예외 개체는 예외 변수에 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-554">If the `catch` clause declares an exception variable, the exception object is assigned to the exception variable.</span></span>
      *  <span data-ttu-id="c3468-555">경우는 `catch` 절 선언 예외 필터, 필터를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-555">If the `catch` clause declares an exception filter, the filter is evaluated.</span></span> <span data-ttu-id="c3468-556">로 평가 되 면 `false`, catch 절이 일치 하는 항목 및 검색을 통해 계속 후속 `catch` 절 적합 한 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-556">If it evaluates to `false`, the catch clause is not a match, and the search continues through any subsequent `catch` clauses for a suitable handler.</span></span>
      *  <span data-ttu-id="c3468-557">그렇지 않으면 합니다 `catch` 절에는 일치 하는 것으로 간주 됩니다 및 제어가 일치 하는 `catch` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-557">Otherwise, the `catch` clause is considered a match, and control is transferred to the matching `catch` block.</span></span>
      *  <span data-ttu-id="c3468-558">컨트롤의 끝점에 도달 하는 경우는 `catch` 블록:</span><span class="sxs-lookup"><span data-stu-id="c3468-558">When and if control reaches the end point of the `catch` block:</span></span>
         * <span data-ttu-id="c3468-559">경우는 `try` 문에 `finally` 블록을 `finally` 블록이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-559">If the `try` statement has a `finally` block, the `finally` block is executed.</span></span>
         * <span data-ttu-id="c3468-560">끝점으로 제어가 `try` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-560">Control is transferred to the end point of the `try` statement.</span></span>
      *  <span data-ttu-id="c3468-561">예외가 전파 되는 경우는 `try` 문을 실행 하는 동안는 `catch` 블록:</span><span class="sxs-lookup"><span data-stu-id="c3468-561">If an exception is propagated to the `try` statement during execution of the `catch` block:</span></span>
         *  <span data-ttu-id="c3468-562">경우는 `try` 문에 `finally` 블록을 `finally` 블록이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-562">If the `try` statement has a `finally` block, the `finally` block is executed.</span></span>
         *  <span data-ttu-id="c3468-563">다음 바깥쪽 예외가 전파 됩니다 `try` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-563">The exception is propagated to the next enclosing `try` statement.</span></span>
   *  <span data-ttu-id="c3468-564">경우는 `try` 문이 아무런 `catch` 절 없으면 또는 `catch` 절 예외와 일치:</span><span class="sxs-lookup"><span data-stu-id="c3468-564">If the `try` statement has no `catch` clauses or if no `catch` clause matches the exception:</span></span>
      *  <span data-ttu-id="c3468-565">경우는 `try` 문에 `finally` 블록을 `finally` 블록이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-565">If the `try` statement has a `finally` block, the `finally` block is executed.</span></span>
      *  <span data-ttu-id="c3468-566">다음 바깥쪽 예외가 전파 됩니다 `try` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-566">The exception is propagated to the next enclosing `try` statement.</span></span>

<span data-ttu-id="c3468-567">문의 `finally` 컨트롤을 벗어나면 블록이 항상 실행 됩니다는 `try` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-567">The statements of a `finally` block are always executed when control leaves a `try` statement.</span></span> <span data-ttu-id="c3468-568">마찬가지 제어 전송을 실행 한 결과로 일반 실행의 결과로 발생 하는 여부는 `break`, `continue`, `goto`, 또는 `return` 문, 또는 예외 전파의 결과로 `try` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-568">This is true whether the control transfer occurs as a result of normal execution, as a result of executing a `break`, `continue`, `goto`, or `return` statement, or as a result of propagating an exception out of the `try` statement.</span></span>

<span data-ttu-id="c3468-569">작업을 실행 하는 동안 예외가 발생 하는 경우는 `finally` 블록과 잡히지 않는 다음 바깥쪽 동일 finally 블록 내에서 예외가 전파 됩니다 `try` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-569">If an exception is thrown during execution of a `finally` block, and is not caught within the same finally block, the exception is propagated to the next enclosing `try` statement.</span></span> <span data-ttu-id="c3468-570">다른 예외 전파 되 고 있으면 해당 예외가 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-570">If another exception was in the process of being propagated, that exception is lost.</span></span> <span data-ttu-id="c3468-571">예외를 전파 하는 과정 설명의 설명에 추가 합니다 `throw` 문 ([throw 문을](statements.md#the-throw-statement)).</span><span class="sxs-lookup"><span data-stu-id="c3468-571">The process of propagating an exception is discussed further in the description of the `throw` statement ([The throw statement](statements.md#the-throw-statement)).</span></span>

<span data-ttu-id="c3468-572">`try` 블록을 `try` 접근할 수 경우는 `try` 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-572">The `try` block of a `try` statement is reachable if the `try` statement is reachable.</span></span>

<span data-ttu-id="c3468-573">`catch` 블록을 `try` 접근할 수 하는 경우는 `try` 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-573">A `catch` block of a `try` statement is reachable if the `try` statement is reachable.</span></span>

<span data-ttu-id="c3468-574">`finally` 블록을 `try` 접근할 수 경우는 `try` 접근할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-574">The `finally` block of a `try` statement is reachable if the `try` statement is reachable.</span></span>

<span data-ttu-id="c3468-575">끝점에는 `try` 다음 두 가지 경우에 접근할 수:</span><span class="sxs-lookup"><span data-stu-id="c3468-575">The end point of a `try` statement is reachable if both of the following are true:</span></span>

*  <span data-ttu-id="c3468-576">끝점에는 `try` 블록에 연결할 수 또는 하나 이상의의 끝 지점 `catch` 블록에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-576">The end point of the `try` block is reachable or the end point of at least one `catch` block is reachable.</span></span>
*  <span data-ttu-id="c3468-577">경우는 `finally` 블록이 있는지 끝점에는 `finally` 블록에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-577">If a `finally` block is present, the end point of the `finally` block is reachable.</span></span>

## <a name="the-checked-and-unchecked-statements"></a><span data-ttu-id="c3468-578">Checked 및 unchecked 문</span><span class="sxs-lookup"><span data-stu-id="c3468-578">The checked and unchecked statements</span></span>

<span data-ttu-id="c3468-579">`checked` 하 고 `unchecked` 제어 문을 사용 하는 ***오버플로 검사 컨텍스트에*** 정수 형식 산술 연산 및 변환에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-579">The `checked` and `unchecked` statements are used to control the ***overflow checking context*** for integral-type arithmetic operations and conversions.</span></span>

```antlr
checked_statement
    : 'checked' block
    ;

unchecked_statement
    : 'unchecked' block
    ;
```

<span data-ttu-id="c3468-580">`checked` 문을 사용 하면 모든 식에는 *블록* 확인 된 컨텍스트에서 계산할 및 `unchecked` 문을 사용 하면 모든 식에는 *블록* 평가할는 unchecked 컨텍스트를 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-580">The `checked` statement causes all expressions in the *block* to be evaluated in a checked context, and the `unchecked` statement causes all expressions in the *block* to be evaluated in an unchecked context.</span></span>

<span data-ttu-id="c3468-581">합니다 `checked` 및 `unchecked` 문은 정확 하 게 일치 합니다 `checked` 및 `unchecked` 연산자 ([checked 및 unchecked 연산자](expressions.md#the-checked-and-unchecked-operators)) 식 대신 블록에서 작동 한다는 점을 제외 하면, .</span><span class="sxs-lookup"><span data-stu-id="c3468-581">The `checked` and `unchecked` statements are precisely equivalent to the `checked` and `unchecked` operators ([The checked and unchecked operators](expressions.md#the-checked-and-unchecked-operators)), except that they operate on blocks instead of expressions.</span></span>

## <a name="the-lock-statement"></a><span data-ttu-id="c3468-582">Lock 문</span><span class="sxs-lookup"><span data-stu-id="c3468-582">The lock statement</span></span>

<span data-ttu-id="c3468-583">`lock` 문에 지정된 된 개체에 대 한 상호 배제 잠금을 가져오고, 문을 실행 하 고 다음 잠금을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-583">The `lock` statement obtains the mutual-exclusion lock for a given object, executes a statement, and then releases the lock.</span></span>

```antlr
lock_statement
    : 'lock' '(' expression ')' embedded_statement
    ;
```

<span data-ttu-id="c3468-584">식을 `lock` 문을 것으로 알려진 형식의 값을 표시 해야 합니다는 *reference_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-584">The expression of a `lock` statement must denote a value of a type known to be a *reference_type*.</span></span> <span data-ttu-id="c3468-585">암시적 boxing 변환 작업 없이 ([Boxing 변환](conversions.md#boxing-conversions))의 식에 수행한 적이 되는 `lock` 문, 따라서 되며의 값을 나타내는 식에 대 한 컴파일 시간 오류를를 *value_type*.</span><span class="sxs-lookup"><span data-stu-id="c3468-585">No implicit boxing conversion ([Boxing conversions](conversions.md#boxing-conversions)) is ever performed for the expression of a `lock` statement, and thus it is a compile-time error for the expression to denote a value of a *value_type*.</span></span>

<span data-ttu-id="c3468-586">`lock` 폼의 문</span><span class="sxs-lookup"><span data-stu-id="c3468-586">A `lock` statement of the form</span></span>
```csharp
lock (x) ...
```
<span data-ttu-id="c3468-587">여기서 `x` 식입니다를 *reference_type*는 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-587">where `x` is an expression of a *reference_type*, is precisely equivalent to</span></span>
```csharp
bool __lockWasTaken = false;
try {
    System.Threading.Monitor.Enter(x, ref __lockWasTaken);
    ...
}
finally {
    if (__lockWasTaken) System.Threading.Monitor.Exit(x);
}
```
<span data-ttu-id="c3468-588">단, `x`가 한 번만 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-588">except that `x` is only evaluated once.</span></span>

<span data-ttu-id="c3468-589">상호 배타적 잠금이 유지 되는 동안 동일한 실행 스레드에서 실행 되는 코드 또한 가져오고 수 잠금을 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-589">While a mutual-exclusion lock is held, code executing in the same execution thread can also obtain and release the lock.</span></span> <span data-ttu-id="c3468-590">그러나 다른 스레드에서 실행 되는 코드에서 잠금이 해제 될 때까지 잠금을 가져올 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-590">However, code executing in other threads is blocked from obtaining the lock until the lock is released.</span></span>

<span data-ttu-id="c3468-591">잠금 `System.Type` 정적 데이터에 대 한 액세스를 동기화 하기 위해 개체 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-591">Locking `System.Type` objects in order to synchronize access to static data is not recommended.</span></span> <span data-ttu-id="c3468-592">다른 코드 교착 상태가 발생할 수 있는 동일한 형식에 대해 잠글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-592">Other code might lock on the same type, which can result in deadlock.</span></span> <span data-ttu-id="c3468-593">전용 정적 개체를 잠그는 방식으로 정적 데이터에 대 한 액세스를 동기화 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-593">A better approach is to synchronize access to static data by locking a private static object.</span></span> <span data-ttu-id="c3468-594">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c3468-594">For example:</span></span>
```csharp
class Cache
{
    private static readonly object synchronizationObject = new object();

    public static void Add(object x) {
        lock (Cache.synchronizationObject) {
            ...
        }
    }

    public static void Remove(object x) {
        lock (Cache.synchronizationObject) {
            ...
        }
    }
}
```

## <a name="the-using-statement"></a><span data-ttu-id="c3468-595">using 문</span><span class="sxs-lookup"><span data-stu-id="c3468-595">The using statement</span></span>

<span data-ttu-id="c3468-596">`using` 문을 하나 이상의 리소스를 가져오고, 문을 실행 하 고 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-596">The `using` statement obtains one or more resources, executes a statement, and then disposes of the resource.</span></span>

```antlr
using_statement
    : 'using' '(' resource_acquisition ')' embedded_statement
    ;

resource_acquisition
    : local_variable_declaration
    | expression
    ;
```

<span data-ttu-id="c3468-597">A ***리소스*** 는 클래스 또는 구조체를 구현 하는 `System.IDisposable`, 라는 단일 매개 변수가 없는 메서드를 포함 하는 `Dispose`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-597">A ***resource*** is a class or struct that implements `System.IDisposable`, which includes a single parameterless method named `Dispose`.</span></span> <span data-ttu-id="c3468-598">리소스를 사용 하는 코드를 호출할 수 `Dispose` 더 이상 필요 없는 리소스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-598">Code that is using a resource can call `Dispose` to indicate that the resource is no longer needed.</span></span> <span data-ttu-id="c3468-599">경우 `Dispose` 자동 삭제가 가비지 컬렉션의 결과로 발생 한 다음는 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-599">If `Dispose` is not called, then automatic disposal eventually occurs as a consequence of garbage collection.</span></span>

<span data-ttu-id="c3468-600">경우 형식의 *resource_acquisition* 됩니다 *local_variable_declaration* 의 형식은 합니다 *local_variable_declaration* 중 하나 여야 합니다 `dynamic` 또는 형식 암시적으로 변환할 수 있는 `System.IDisposable`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-600">If the form of *resource_acquisition* is *local_variable_declaration* then the type of the *local_variable_declaration* must be either `dynamic` or a type that can be implicitly converted to `System.IDisposable`.</span></span> <span data-ttu-id="c3468-601">경우 형식의 *resource_acquisition* 됩니다 *식* 이 식은 암시적으로 변환할 수 있어야 다음 `System.IDisposable`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-601">If the form of *resource_acquisition* is *expression* then this expression must be implicitly convertible to `System.IDisposable`.</span></span>

<span data-ttu-id="c3468-602">선언 된 지역 변수를 *resource_acquisition* 는 읽기 전용 이며 이니셜라이저를 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-602">Local variables declared in a *resource_acquisition* are read-only, and must include an initializer.</span></span> <span data-ttu-id="c3468-603">컴파일 타임 오류가 발생 하는 포함된 된 문을 이러한 로컬 변수를 수정 하려고 하는 경우 (할당을 통해 또는 `++` 하 고 `--` 연산자), 그 중 주소 또는으로 전달할 `ref` 또는 `out` 매개 변수.</span><span class="sxs-lookup"><span data-stu-id="c3468-603">A compile-time error occurs if the embedded statement attempts to modify these local variables (via assignment or the `++` and `--` operators) , take the address of them, or pass them as `ref` or `out` parameters.</span></span>

<span data-ttu-id="c3468-604">`using` 문을 세 부분으로 변환: 취득, 사용 및 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-604">A `using` statement is translated into three parts: acquisition, usage, and disposal.</span></span> <span data-ttu-id="c3468-605">리소스의 사용량에 암시적으로 포함 되어는 `try` 문을 포함 하는 `finally` 절.</span><span class="sxs-lookup"><span data-stu-id="c3468-605">Usage of the resource is implicitly enclosed in a `try` statement that includes a `finally` clause.</span></span> <span data-ttu-id="c3468-606">이 `finally` 절 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-606">This `finally` clause disposes of the resource.</span></span> <span data-ttu-id="c3468-607">경우는 `null` 리소스를 획득 하에 대 한 호출이 다음 `Dispose` 이루어지는 고 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-607">If a `null` resource is acquired, then no call to `Dispose` is made, and no exception is thrown.</span></span> <span data-ttu-id="c3468-608">리소스 형식의 경우 `dynamic` 암시적 동적 변환을 통해 동적으로 변환 됩니다 ([암시적 동적 변환을](conversions.md#implicit-dynamic-conversions))를 `IDisposable` 변환 되는지 확인 하기 위해 획득 하는 동안 사용 및 폐기 전에 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-608">If the resource is of type `dynamic` it is dynamically converted through an implicit dynamic conversion ([Implicit dynamic conversions](conversions.md#implicit-dynamic-conversions)) to `IDisposable` during acquisition in order to ensure that the conversion is successful before the usage and disposal.</span></span>

<span data-ttu-id="c3468-609">`using` 폼의 문</span><span class="sxs-lookup"><span data-stu-id="c3468-609">A `using` statement of the form</span></span>
```csharp
using (ResourceType resource = expression) statement
```
<span data-ttu-id="c3468-610">세 가지 가능한 확장 중 하나에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-610">corresponds to one of three possible expansions.</span></span> <span data-ttu-id="c3468-611">때 `ResourceType` 형식이 nullable이 아닌 값은 확장</span><span class="sxs-lookup"><span data-stu-id="c3468-611">When `ResourceType` is a non-nullable value type, the expansion is</span></span>
```csharp
{
    ResourceType resource = expression;
    try {
        statement;
    }
    finally {
        ((IDisposable)resource).Dispose();
    }
}
```

<span data-ttu-id="c3468-612">경우에이 고, 그렇지 `ResourceType` nullable 값 형식 또는 참조 형식 이외의 `dynamic`, 확장은</span><span class="sxs-lookup"><span data-stu-id="c3468-612">Otherwise, when `ResourceType` is a nullable value type or a reference type other than `dynamic`, the expansion is</span></span>
```csharp
{
    ResourceType resource = expression;
    try {
        statement;
    }
    finally {
        if (resource != null) ((IDisposable)resource).Dispose();
    }
}
```

<span data-ttu-id="c3468-613">경우에이 고, 그렇지 `ResourceType` 는 `dynamic`, 확장은</span><span class="sxs-lookup"><span data-stu-id="c3468-613">Otherwise, when `ResourceType` is `dynamic`, the expansion is</span></span>
```csharp
{
    ResourceType resource = expression;
    IDisposable d = (IDisposable)resource;
    try {
        statement;
    }
    finally {
        if (d != null) d.Dispose();
    }
}
```

<span data-ttu-id="c3468-614">두 확장에는 `resource` 변수가 포함 된 문에서 읽기 전용 및 `d` 변수가에서 액세스할 수 없게 하 고 보이지 않는 포함된 된 문을를 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-614">In either expansion, the `resource` variable is read-only in the embedded statement, and the `d` variable is inaccessible in, and invisible to, the embedded statement.</span></span>

<span data-ttu-id="c3468-615">동작은 위의 확장과 일치으로 성능상의 이유로, 예: 지정된을 사용 하 여 문을 다르게 구현 구현을 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-615">An implementation is permitted to implement a given using-statement differently, e.g. for performance reasons, as long as the behavior is consistent with the above expansion.</span></span>

<span data-ttu-id="c3468-616">`using` 폼의 문</span><span class="sxs-lookup"><span data-stu-id="c3468-616">A `using` statement of the form</span></span>
```csharp
using (expression) statement
```
<span data-ttu-id="c3468-617">동일한 세 가지 가능한 확장에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-617">has the same three possible expansions.</span></span> <span data-ttu-id="c3468-618">이 경우 `ResourceType` 는 암시적으로의 컴파일 타임 형식은 `expression`하나 포함 된 경우.</span><span class="sxs-lookup"><span data-stu-id="c3468-618">In this case `ResourceType` is implicitly the compile-time type of the `expression`, if it has one.</span></span> <span data-ttu-id="c3468-619">그렇지 않으면 인터페이스 `IDisposable` 으로 사용 되는 자체는 `ResourceType`합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-619">Otherwise the interface `IDisposable` itself is used as the `ResourceType`.</span></span> <span data-ttu-id="c3468-620">`resource` 변수가에서 액세스할 수 없게 하 고 보이지 않는 포함된 된 문을를 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-620">The `resource` variable is inaccessible in, and invisible to, the embedded statement.</span></span>

<span data-ttu-id="c3468-621">경우는 *resource_acquisition* 형태는 *local_variable_declaration*, 지정 된 형식의 여러 리소스를 가져올 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-621">When a *resource_acquisition* takes the form of a *local_variable_declaration*, it is possible to acquire multiple resources of a given type.</span></span> <span data-ttu-id="c3468-622">`using` 폼의 문</span><span class="sxs-lookup"><span data-stu-id="c3468-622">A `using` statement of the form</span></span>
```csharp
using (ResourceType r1 = e1, r2 = e2, ..., rN = eN) statement
```
<span data-ttu-id="c3468-623">시퀀스를 해당 정확 하 게 중첩 되어 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="c3468-623">is precisely equivalent to a sequence of nested `using` statements:</span></span>
```csharp
using (ResourceType r1 = e1)
    using (ResourceType r2 = e2)
        ...
            using (ResourceType rN = eN)
                statement
```

<span data-ttu-id="c3468-624">아래 예제에서는 라는 파일을 만듭니다 `log.txt` 파일을 두 줄 텍스트를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-624">The example below creates a file named `log.txt` and writes two lines of text to the file.</span></span> <span data-ttu-id="c3468-625">읽기에 대 한 파일을 엽니다 하 고 콘솔에 포함 된 줄의 텍스트를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-625">The example then opens that same file for reading and copies the contained lines of text to the console.</span></span>
```csharp
using System;
using System.IO;

class Test
{
    static void Main() {
        using (TextWriter w = File.CreateText("log.txt")) {
            w.WriteLine("This is line one");
            w.WriteLine("This is line two");
        }

        using (TextReader r = File.OpenText("log.txt")) {
            string s;
            while ((s = r.ReadLine()) != null) {
                Console.WriteLine(s);
            }

        }
    }
}
```

<span data-ttu-id="c3468-626">있으므로 `TextWriter` 및 `TextReader` 클래스 구현 합니다 `IDisposable` 인터페이스 예제를 사용할 수 `using` 기본 파일이 올바르게 닫히도록 하기 다음 쓰기 또는 읽기 작업 문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-626">Since the `TextWriter` and `TextReader` classes implement the `IDisposable` interface, the example can use `using` statements to ensure that the underlying file is properly closed following the write or read operations.</span></span>

## <a name="the-yield-statement"></a><span data-ttu-id="c3468-627">Yield 문</span><span class="sxs-lookup"><span data-stu-id="c3468-627">The yield statement</span></span>

<span data-ttu-id="c3468-628">`yield` 문을 사용 하는 반복기 블록에서 ([블록](statements.md#blocks)) 열거자 개체에 값을 생성 하기 위해 ([열거자 개체](classes.md#enumerator-objects)) 또는 열거 가능 개체 ([열거가능한개체](classes.md#enumerable-objects)) 반복기 또는 반복의 끝을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-628">The `yield` statement is used in an iterator block ([Blocks](statements.md#blocks)) to yield a value to the enumerator object ([Enumerator objects](classes.md#enumerator-objects)) or enumerable object ([Enumerable objects](classes.md#enumerable-objects)) of an iterator or to signal the end of the iteration.</span></span>

```antlr
yield_statement
    : 'yield' 'return' expression ';'
    | 'yield' 'break' ';'
    ;
```

<span data-ttu-id="c3468-629">`yield` 예약어; 아닙니다. 이 특별 한 의미가 바로 앞에 사용 하는 경우에을 `return` 또는 `break` 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-629">`yield` is not a reserved word; it has special meaning only when used immediately before a `return` or `break` keyword.</span></span> <span data-ttu-id="c3468-630">다른 컨텍스트에서 `yield` 식별자로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-630">In other contexts, `yield` can be used as an identifier.</span></span>

<span data-ttu-id="c3468-631">위치에 몇 가지 제한 사항을 `yield` 다음에 설명 된 대로 문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-631">There are several restrictions on where a `yield` statement can appear, as described in the following.</span></span>

*  <span data-ttu-id="c3468-632">에 대 한 컴파일 시간 오류가 발생 한 `yield` 설명은 (형식 중 하나) 밖에 표시를 *method_body*, *operator_body* 또는 *accessor_body*</span><span class="sxs-lookup"><span data-stu-id="c3468-632">It is a compile-time error for a `yield` statement (of either form) to appear outside a *method_body*, *operator_body* or *accessor_body*</span></span>
*  <span data-ttu-id="c3468-633">에 대 한 컴파일 시간 오류를 `yield` 설명은 (형식 중 하나) 익명 함수 내에서 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-633">It is a compile-time error for a `yield` statement (of either form) to appear inside an anonymous function.</span></span>
*  <span data-ttu-id="c3468-634">에 대 한 컴파일 시간 오류가 발생을 `yield` 설명은 (형식 중 하나)에 표시를 `finally` 절을 `try` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-634">It is a compile-time error for a `yield` statement (of either form) to appear in the `finally` clause of a `try` statement.</span></span>
*  <span data-ttu-id="c3468-635">에 대 한 컴파일 시간 오류를 `yield return` 위치에 나 나타날 문을 `try` 문을 포함 하는 `catch` 절.</span><span class="sxs-lookup"><span data-stu-id="c3468-635">It is a compile-time error for a `yield return` statement to appear anywhere in a `try` statement that contains any `catch` clauses.</span></span>

<span data-ttu-id="c3468-636">다음 예제에서는 유효 하지 않은 사용의 `yield` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-636">The following example shows some valid and invalid uses of `yield` statements.</span></span>

```csharp
delegate IEnumerable<int> D();

IEnumerator<int> GetEnumerator() {
    try {
        yield return 1;        // Ok
        yield break;           // Ok
    }
    finally {
        yield return 2;        // Error, yield in finally
        yield break;           // Error, yield in finally
    }

    try {
        yield return 3;        // Error, yield return in try...catch
        yield break;           // Ok
    }
    catch {
        yield return 4;        // Error, yield return in try...catch
        yield break;           // Ok
    }

    D d = delegate { 
        yield return 5;        // Error, yield in an anonymous function
    }; 
}

int MyMethod() {
    yield return 1;            // Error, wrong return type for an iterator block
}
```

<span data-ttu-id="c3468-637">암시적으로 변환 ([암시적 변환을](conversions.md#implicit-conversions))에서 식의 형식에서 존재 해야 합니다는 `yield return` yield 형식의 문을 ([형식을 생성](classes.md#yield-type)) 반복기의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-637">An implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) must exist from the type of the expression in the `yield return` statement to the yield type ([Yield type](classes.md#yield-type)) of the iterator.</span></span>

<span data-ttu-id="c3468-638">`yield return` 문을 다음과 같이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-638">A `yield return` statement is executed as follows:</span></span>

*  <span data-ttu-id="c3468-639">문에 지정 된 식 계산, 암시적으로 yield 형식으로 변환 되어에 할당 된 `Current` 열거자 개체의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-639">The expression given in the statement is evaluated, implicitly converted to the yield type, and assigned to the `Current` property of the enumerator object.</span></span>
*  <span data-ttu-id="c3468-640">반복기 블록의 실행을 일시 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-640">Execution of the iterator block is suspended.</span></span> <span data-ttu-id="c3468-641">경우는 `yield return` 문 내에서 하나 이상의 됩니다 `try` 연결 된 블록 `finally` 지금은 블록이 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-641">If the `yield return` statement is within one or more `try` blocks, the associated `finally` blocks are not executed at this time.</span></span>
*  <span data-ttu-id="c3468-642">합니다 `MoveNext` 열거자 개체의 메서드 반환 `true` 다음 항목을 지났으면 열거자 개체를 나타내는 해당 호출자에 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-642">The `MoveNext` method of the enumerator object returns `true` to its caller, indicating that the enumerator object successfully advanced to the next item.</span></span>

<span data-ttu-id="c3468-643">열거자 개체의 다음 호출 `MoveNext` 메서드를 마지막으로 일시 중단에서 반복기 블록의 실행을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-643">The next call to the enumerator object's `MoveNext` method resumes execution of the iterator block from where it was last suspended.</span></span>

<span data-ttu-id="c3468-644">`yield break` 문을 다음과 같이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-644">A `yield break` statement is executed as follows:</span></span>

*  <span data-ttu-id="c3468-645">경우는 `yield break` 문을 하나 이상으로 묶입니다 `try` 블록에 연결 `finally` 제어 블록은 처음에 전송 합니다 `finally` 가장 안쪽의 블록 `try` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-645">If the `yield break` statement is enclosed by one or more `try` blocks with associated `finally` blocks, control is initially transferred to the `finally` block of the innermost `try` statement.</span></span> <span data-ttu-id="c3468-646">컨트롤의 끝점에 도달 하는 경우는 `finally` 컨트롤 블록으로 전송 됩니다는 `finally` 다음 바깥쪽 블록 `try` 문.</span><span class="sxs-lookup"><span data-stu-id="c3468-646">When and if control reaches the end point of a `finally` block, control is transferred to the `finally` block of the next enclosing `try` statement.</span></span> <span data-ttu-id="c3468-647">될 때까지이 프로세스를 반복 합니다 `finally` 모든 바깥쪽 블록 `try` 문이 실행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-647">This process is repeated until the `finally` blocks of all enclosing `try` statements have been executed.</span></span>
*  <span data-ttu-id="c3468-648">컨트롤은 반복기 블록의 호출자에 게 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-648">Control is returned to the caller of the iterator block.</span></span> <span data-ttu-id="c3468-649">이 값은 `MoveNext` 메서드 또는 `Dispose` 열거자 개체의 메서드.</span><span class="sxs-lookup"><span data-stu-id="c3468-649">This is either the `MoveNext` method or `Dispose` method of the enumerator object.</span></span>

<span data-ttu-id="c3468-650">때문에 `yield break` 문을 무조건 제어 전송 다른 곳에서 끝점에는 `yield break` 문에 접근할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c3468-650">Because a `yield break` statement unconditionally transfers control elsewhere, the end point of a `yield break` statement is never reachable.</span></span>
