# <a name="statements"></a>문

C# 다양 한 문 제공합니다. 대부분의 이러한 문 C 및 c + +에서 프로그래밍할는 개발자에 게 익숙할 것입니다.

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

합니다 *embedded_statement* 비터미널 다른 문 내에서 표시 되는 문에 사용 됩니다. 사용 *embedded_statement* 대신 *문* 선언문 및 레이블된 문 다음 컨텍스트에서 사용을 제외 합니다. 이 예제에서
```csharp
void F(bool b) {
    if (b)
        int i = 44;
}
```
때문에 컴파일 타임 오류가 발생을 `if` 문에 필요는 *embedded_statement* 아닌 *문을* 해당 경우 분기 합니다. 이 코드 된 허용 변수의 경우 `i` 을 선언할 수는 있지만 사용할 수 없습니다. 단, 배치 하 여는 `i`의 블록에서 선언 된 예제는 유효 합니다.

## <a name="end-points-and-reachability"></a>끝점 및 연결

모든 문에 ***끝점***합니다. 직관적인 말해 문의 끝점 문 바로 뒤에 오는 위치입니다. 복합 문 (포함 된 문이 포함 된 문)에 대 한 실행 규칙 컨트롤이 포함 된 문의 끝 지점에 도달할 때 수행 되는 동작을 지정 합니다. 예를 들어 제어 블록의 문이의 끝점에 도달 하면 블록의 다음 문으로 제어가 전달 됩니다.

문을 실행 하 여 연결할 수 수 있는 경우 문이 이라고 ***연결할***합니다. 반대로,를 문이 실행 되는 가능성이 있으면 문이 이라고 ***접근할 수 없는***합니다.

예제
```csharp
void F() {
    Console.WriteLine("reachable");
    goto Label;
    Console.WriteLine("unreachable");
    Label:
    Console.WriteLine("reachable");
}
```
두 번째 호출 `Console.WriteLine` 에 문이 실행 되는 가능성이 있기 때문에 연결할 수 없습니다.

컴파일러는 문을 연결할 수 있는지 결정 하는 경우 경고가 보고 됩니다. 특히 오류가 아니라 문에 연결할 수 없는 경우

특정 문 또는 끝점에 연결할 수 있는지 여부를 결정할 컴파일러는 각 문에 대해 정의 된 연결 규칙에 따라 흐름 분석을 수행 합니다. 흐름 분석 고려 상수 식의 값 ([상수 식](expressions.md#constant-expressions)) 문의 동작을 제어 하는 하지만 상수가 아닌 식의 가능한 값은 고려 되지 않습니다. 즉, 제어 흐름 분석을 위해 지정 된 형식의 상수가 아닌 식은 해당 형식의 모든 가능한 값으로 간주 됩니다.

예제
```csharp
void F() {
    const int i = 1;
    if (i == 2) Console.WriteLine("unreachable");
}
```
부울 식입니다 합니다 `if` 문 이므로 상수 식의 두 피연산자는 `==` 연산자는 상수입니다. 상수 식은 컴파일 시간에 계산 되는 값을 생성 `false`, `Console.WriteLine` 호출 접근할 수 없는 것으로 간주 됩니다. 그러나 경우 `i` 지역 변수 변경
```csharp
void F() {
    int i = 1;
    if (i == 2) Console.WriteLine("reachable");
}
```
`Console.WriteLine` 하더라도 실제로 실행 되지 않는 호출에 연결할 수 간주 됩니다.

합니다 *블록* 함수 멤버는 항상 것으로 연결할 수 있습니다. 블록의 각 문이의 가능성 규칙을 연속적으로 평가 하 여 지정 된 문의 연결 가능성을 확인할 수 있습니다.

예제
```csharp
void F(int x) {
    Console.WriteLine("start");
    if (x < 0) Console.WriteLine("negative");
}
```
두 번째 연결 `Console.WriteLine` 다음과 같이 결정 됩니다.

*  첫 번째 `Console.WriteLine` 식에 연결할 수 때문에 블록을는 `F` 메서드는 연결할 수 있습니다.
*  첫 번째 끝점 `Console.WriteLine` 식 문은 해당 문을 연결할 수 때문에 연결할 수입니다.
*  `if` 문 이므로 연결할 수 있는 첫 번째 끝 지점 `Console.WriteLine` 식에 연결할 수 있습니다.
*  두 번째 `Console.WriteLine` 식에 연결할 수 있으므로 부울 식입니다는 `if` 문은 상수 값이 없는 `false`합니다.

가지는 것이 가능 하는 문의 끝점에 대 한 컴파일 시간 오류를 두 가지 상황이 있습니다.

*  때문에 `switch` 문을 다음 스위치 섹션으로 "이동" 하는 switch 섹션을 허용 하지 않습니다, 끝점에 연결할 수는 switch 섹션의 문 목록에 대 한 컴파일 시간 오류가 발생 합니다. 이 오류가 발생할 경우 일반적으로 표시 하는 `break` 문에서 누락 되었습니다.
*  이 끝점에 연결할 수 값을 계산 하는 함수 멤버의 블록에 대 한 컴파일 시간 오류입니다. 표시는 일반적으로이 오류가 발생 하는 경우는 `return` 문에서 누락 되었습니다.

## <a name="blocks"></a>블록

*블록*은 단일 문이 허용되는 컨텍스트에서 여러 문을 쓸 수 있도록 허용합니다.

```antlr
block
    : '{' statement_list? '}'
    ;
```

A *블록* 선택적인 이루어져 *statement_list* ([문은 나열](statements.md#statement-lists)) 중괄호로 묶어서 합니다. 문 목록을 생략 하면 비워 블록 이라고 합니다.

블록 선언 문을 포함할 수 있습니다 ([선언문](statements.md#declaration-statements)). 지역 변수 또는 상수의 범위는 블록에서 선언 된 블록.

블록을 다음과 같이 실행 됩니다.

*  블록이 비어 있는 경우 제어 블록의 끝 지점에 전송 됩니다.
*  블록을 비어 있지 않은 경우 문 목록으로 제어가 전달 됩니다. 시간과 제어 문 목록의 끝 지점에 도달 하면, 제어 블록의 끝 지점에 전송 됩니다.

블록의 문은 목록은 블록 자체에 연결할 수 경우에 연결할 수 있습니다.

블록이 비어 있는 경우 또는 문 목록의 끝 지점에 연결할 수 경우 블록의 끝 지점에 연결할 수 있습니다.

A *블록* 하나를 포함 하는 `yield` 문 ([yield 문을](statements.md#the-yield-statement))은 반복기 블록이 호출 됩니다. 반복기 블록은 반복기로 함수 멤버를 구현 하는 데 사용 됩니다 ([반복기](classes.md#iterators)). 반복기 블록에 몇 가지 추가 제한 사항이 적용 됩니다.

*  에 대 한 컴파일 시간 오류가 발생 한 `return` 반복기 블록에서 문을 (하지만 `yield return` 문이 허용 됩니다).
*  안전 하지 않은 컨텍스트를 포함 하는 반복기 블록에 대 한 컴파일 시간 오류 ([안전 하지 않은 컨텍스트](unsafe-code.md#unsafe-contexts)). 반복기 블록이 항상 안전 하지 않은 컨텍스트에서 선언 중첩 된 경우에 안전한 컨텍스트를 정의 합니다.

### <a name="statement-lists"></a>문 목록

A ***문 목록의*** 순서로 기록 하는 하나 이상의 문으로 구성 됩니다. 문 목록 나타나는 *블록*s ([블록](statements.md#blocks)) 및 *switch_block*s ([switch 문에서](statements.md#the-switch-statement)).

```antlr
statement_list
    : statement+
    ;
```

첫 번째 문으로 제어를 전송 하 여 문 목록의 실행 됩니다. 및 제어 문의 끝 지점에 도달 하면 다음 문으로 제어가 전달 됩니다. 및 컨트롤이 마지막 명령문의 끝점에 도달할 때 문 목록의 끝 지점으로 제어가 전달 됩니다.

문 목록의 문 중 최소한 하나가 참인 경우에 연결할 수는:

*  문의 첫 번째 문인 및 문 목록에 연결할 수 있습니다.
*  앞의 문에서의 끝점에 연결할 수 있습니다.
*  문에 레이블이 지정 된 문 및를 연결할 수 여 레이블을 참조 하는 `goto` 문입니다.

끝점 문 목록에 연결할 수 있는 경우 목록의 마지막 명령문의 끝점에 연결할 수 있습니다.

## <a name="the-empty-statement"></a>빈 문

*empty_statement* 아무 작업도 수행 합니다.

```antlr
empty_statement
    : ';'
    ;
```

빈 문의 경우 컨텍스트에서 수행할 작업이 문을 필요한 경우 사용 됩니다.

단순히 빈 문의 실행 문의 끝 지점에 제어를 전송합니다. 따라서 빈 문의 끝점에 빈 문이 연결할 수 경우 연결할 수 있습니다.

빈 문을 작성할 때 사용할 수는 `while` null 본문이 있는 문.
```csharp
bool ProcessMessage() {...}

void ProcessMessages() {
    while (ProcessMessage())
        ;
}
```

또한 빈 문의 수 닫기 전에 레이블을 선언 "`}`" 블록:
```csharp
void F() {
    ...
    if (done) goto exit;
    ...
    exit: ;
}
```

## <a name="labeled-statements"></a>레이블 문

A *labeled_statement* 레이블을 붙일 수 하는 문을 허용 합니다. 레이블된 문 블록에서 수 있지만 포함 문으로 허용 되지 않습니다.

```antlr
labeled_statement
    : identifier ':' statement
    ;
```

Labeled 문 제공한 이름을 사용 하 여 레이블을 선언 합니다 *식별자*합니다. 레이블의 범위는 전체 블록 중첩 블록이 포함 하 여 레이블을 선언입니다. 이 겹치는 범위에 동일한 이름 가진 두 개의 레이블에 대 한 컴파일 시간 오류입니다.

레이블을에서 참조할 수 있습니다 `goto` 문 ([goto 문을](statements.md#the-goto-statement)) 레이블의 범위 내에서. 즉 `goto` 문 블록 내에서 및 블록 되었지만 블록으로 되지 제어를 이동할 수 있습니다.

레이블을 자체 선언 공간 있고 다른 식별자를 방해 하지 않습니다. 이 예제에서
```csharp
int F(int x) {
    if (x >= 0) goto x;
    x = -x;
    x: return x;
}
```
유효 하 고 이름을 사용 하 여 `x` 매개 변수 및 레이블을으로 합니다.

레이블 다음에 문 실행에 정확히 대응 하며 레이블이 지정 된 문 실행 합니다.

Labeled 문 정상적인 제어 흐름에 제공한 연결 가능성, 외에 연결할 수 여 레이블을 참조 하는 경우에 연결할 수는 `goto` 문입니다. (예외: 경우는 `goto` 문 내에 `try` 포함 하는 `finally` 블록 및 labeled 문 벗어납니다를 `try`, 및 끝점에는 `finally` 블록을 연결할 수 없기을 레이블이 지정 된 문이 연결할 수 `goto` 문.)

## <a name="declaration-statements"></a>선언문

A *declaration_statement* 지역 변수 또는 상수를 선언 합니다. 선언문 블록에서 수 있지만 포함 문으로 허용 되지 않습니다.

```antlr
declaration_statement
    : local_variable_declaration ';'
    | local_constant_declaration ';'
    ;
```

### <a name="local-variable-declarations"></a>지역 변수 선언

A *local_variable_declaration* 하나 이상의 로컬 변수를 선언 합니다.

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

합니다 *local_variable_type* 의 한 *local_variable_declaration* 선언에 의해 정의 된 변수 유형을 직접 또는 식별자를 사용 하 여 나타냅니다 `var` 는 이니셜라이저에 따라 형식을 유추할 수 해야 합니다. 형식 목록이 나옵니다 *local_variable_declarator*s, 각각 새 변수를 소개 합니다. A *local_variable_declarator* 이루어져는 *식별자* 뒤에 선택적으로 변수의 이름을 나타내는 "`=`" 토큰 및 *local_variable_initializer* 는 변수의 초기 값을 제공 합니다.

지역 변수 선언 컨텍스트에서 식별자 var 상황별 키워드로 역할 ([키워드](lexical-structure.md#keywords)). 경우는 *local_variable_type* 으로 지정 됩니다 `var` 및 명명 된 형식이 없는 `var` 는 범위에서 선언 되는 ***암시적 형식 지역 변수 선언***, 형식인 연결 된 이니셜라이저 식의 형식에서 유추 합니다. 암시적 형식된 지역 변수 선언은 다음과 같은 제한 사항이 적용 됩니다.

*  합니다 *local_variable_declaration* 여러 개 포함할 수 없습니다 *local_variable_declarator*s입니다.
*  합니다 *local_variable_declarator* 포함 해야 합니다는 *local_variable_initializer*합니다.
*  합니다 *local_variable_initializer* 이어야 합니다는 *식*합니다.
*  이니셜라이저가 *식* 는 컴파일 시간 형식이 있어야 합니다.
*  이니셜라이저가 *식* 자체 선언 된 변수를 참조할 수 없습니다.

다음은 잘못 된 암시적으로 형식화 된 지역 변수 선언의 예제입니다.

```csharp
var x;               // Error, no initializer to infer type from
var y = {1, 2, 3};   // Error, array initializer not permitted
var z = null;        // Error, null does not have a type
var u = x => x + 1;  // Error, anonymous functions do not have a type
var v = v++;         // Error, initializer cannot refer to variable itself
```

사용 하는 식에서 가져온 지역 변수 값을 *simple_name* ([단순 이름](expressions.md#simple-names))를 사용 하 여 로컬 변수의 값은 수정는 *할당* ( [대입 연산자](expressions.md#assignment-operators)). 로컬 변수로 할당 되어야 합니다 ([한정 된 할당](variables.md#definite-assignment)) 패키지를 가져온 위치 값을 해당 하는 각 위치에 있습니다.

에 선언 된 지역 변수의 범위를 *local_variable_declaration* 블록은 선언이 발생에서 합니다. 지역 변수 앞에 오는 텍스트 위치를 가리키도록 하면 오류가 발생 합니다 *local_variable_declarator* 지역 변수입니다. 지역 변수의 범위 내 변수 또는 상수 이름이 같은 다른 로컬 선언에 컴파일 타임 오류를 것입니다.

여러 변수를 선언 하는 로컬 변수 선언은 동일한 형식 사용 하 여 단일 변수를 여러 번 선언 하는 것과 같습니다. 또한 선언 바로 뒤에 삽입 되는 대입문 정확 하 게 변수 이니셜라이저에서 예외는 지역 변수 선언에 해당 합니다.

이 예제에서
```csharp
void F() {
    int x = 1, y, z = x * 2;
}
```
정확히 일치
```csharp
void F() {
    int x; x = 1;
    int y;
    int z; z = x * 2;
}
```

암시적 형식된 지역 변수 선언에서 선언 되는 로컬 변수에 유형의 변수를 초기화 하는 데 사용 된 식의 형식과 동일로 간주 됩니다. 예를 들어:
```csharp
var i = 5;
var s = "Hello";
var d = 1.0;
var numbers = new int[] {1, 2, 3};
var orders = new Dictionary<int,Order>();
```

암시적으로 형식화 된 지역 변수 선언 위에 다음 명시적 형식된 선언에 정확 하 게 동일합니다.
```csharp
int i = 5;
string s = "Hello";
double d = 1.0;
int[] numbers = new int[] {1, 2, 3};
Dictionary<int,Order> orders = new Dictionary<int,Order>();
```

### <a name="local-constant-declarations"></a>지역 상수 선언

A *local_constant_declaration* 하나 이상의 지역 상수 선언 합니다.

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

*형식* 의 한 *local_constant_declaration* 선언에 의해 도입 된 상수의 형식을 지정 합니다. 형식 목록이 나옵니다 *constant_declarator*s, 각각 새 상수를 소개 합니다. *constant_declarator* 이루어져는 *식별자* 이름을 하는 상수를 뒤에 "`=`" 토큰, 뒤에 *constant_expression* ([ 상수 식](expressions.md#constant-expressions)) 하는 상수 값을 제공 합니다.

합니다 *형식* 하 고 *constant_expression* 지역 상수 선언의 상수 멤버 선언의 것와 동일한 규칙을 따라야 ([상수](classes.md#constants)).

지역 상수 값을 사용 하는 식에서 가져올은 *simple_name* ([단순 이름](expressions.md#simple-names)).

지역 상수의 범위는 블록 선언 발생에서 합니다. 지역 상수 앞에 오는 텍스트 위치에서 참조 하는 오류는 해당 *constant_declarator*합니다. 지역 상수 범위 내 변수 또는 상수 이름이 같은 다른 로컬 선언에 컴파일 타임 오류를 것입니다.

여러 상수를 선언 하는 지역 상수 선언 동일한 형식 사용 하 여 여러 단일 상수 선언 하는 것과 같습니다.

## <a name="expression-statements"></a>식 문

*expression_statement* 지정된 된 식을 평가 합니다. 값을 계산 하 여 식이 있는 경우 삭제 됩니다.

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

일부 식으로 허용 됩니다. 와 같은 특히 식에서 `x + y` 및 `x == 1` 는 단순히 계산 하는 값 (내용이 취소 됨), 문으로 허용 되지 않습니다.

실행을 *expression_statement* 포함 된 식을 계산 하 고 컨트롤의 끝점으로 전송 합니다 *expression_statement*합니다. 끝점에는 *expression_statement* 접근할 수 있으면 해당 *expression_statement* 에 연결할 수 있습니다.

## <a name="selection-statements"></a>선택 문

선택 문 수의 일부 식의 값을 기반으로 하는 실행 가능한 문 중 하나를 선택 합니다.

```antlr
selection_statement
    : if_statement
    | switch_statement
    ;
```

### <a name="the-if-statement"></a>If 문

`if` 문은 부울 식의 값에 따라 실행할 문을 선택 합니다.

```antlr
if_statement
    : 'if' '(' boolean_expression ')' embedded_statement
    | 'if' '(' boolean_expression ')' embedded_statement 'else' embedded_statement
    ;
```

`else` 부분은 연결 된 가장 가까운 앞 `if` 구문에서 허용 되는 합니다. 따라서는 `if` 폼의 문
```csharp
if (x) if (y) F(); else G();
```
위의 식은 아래의 식과 동일합니다.
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

`if` 문을 다음과 같이 실행 됩니다.

*  합니다 *boolean_expression* ([부울 식](expressions.md#boolean-expressions)) 계산 됩니다.
*  부울 식이 `true`, 포함 된 첫 번째 문으로 제어가 전달 됩니다. 컨트롤의 끝 지점으로 전송 되 및 컨트롤이 해당 문의 끝 지점에 도달할 때를 `if` 문.
*  부울 식이 `false` 경우에 `else` 파트가 있는 두 번째 포함 문으로 제어가 전달 됩니다. 컨트롤의 끝 지점으로 전송 되 및 컨트롤이 해당 문의 끝 지점에 도달할 때를 `if` 문.
*  부울 식이 `false` 경우에 `else` 파트가 있는 끝점에 제어가 `if` 문입니다.

첫 번째 문을 포함을 `if` 접근할 수 하는 경우는 `if` 접근할 수 및 부울 식의 상수 값이 없는 `false`합니다.

두 번째 문을 포함을 `if` 문에 있는 경우에 연결할 수 경우 합니다 `if` 접근할 수 및 부울 식의 상수 값이 없는 `true`합니다.

끝점에는 `if` 포함된 문 중 하나 이상의 끝점에 연결할 수 경우 접근할 수 있습니다. 끝 지점 또한는 `if` no 사용 하 여 문을 `else` 파트에 연결할 수 경우 합니다 `if` 접근할 수 및 부울 식의 상수 값이 없는 `true`합니다.

### <a name="the-switch-statement"></a>Switch 문

Switch 문 실행에 대 한 switch 식의 값에 해당 하는 연결 된 스위치 레이블이 있는 문 목록을 선택 합니다.

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

A *switch_statement* 키워드로 구성 됩니다 `switch`뒤에 괄호로 묶은 식 (switch 식 이라고 함), 뒤에 *switch_block*합니다. 합니다 *switch_block* 0 개 이상으로 구성 됩니다 *switch_section*s를 중괄호로 묶습니다. 각 *switch_section* 하나 이상의 구성 *switch_label*s 뒤에 *statement_list* ([문은 나열](statements.md#statement-lists)).

합니다 ***유형을 제어 하는*** 의 `switch` 문은 switch 식으로 설정 됩니다.

*  Switch 식의 형식이 `sbyte`, `byte`, `short`, `ushort`, `int`를 `uint`, `long`, `ulong`, `bool`를 `char`, `string`, 또는 *enum_type*, 또는 이러한 형식 중 하나에 해당 하는 nullable 형식 경우 관리 되는 유형의 `switch` 문입니다.
*  그렇지 않은 경우 정확히 하나의 사용자 정의 암시적으로 변환 ([사용자 정의 변환은](conversions.md#user-defined-conversions)) 다음 가능한 형식을 제어 하는 중에 switch 식의 형식에서 존재 해야 합니다: `sbyte`를 `byte`, `short` 를 `ushort`, `int`, `uint`, `long`를 `ulong`를 `char`, `string`, 또는 이러한 형식 중 하나에 해당 하는 nullable 형식.
*  그렇지 않으면 이러한 암시적 변환이 존재 하거나 이러한 하나의 암시적 변환이 존재 하는 경우 두 개를 컴파일 타임 오류가 발생 합니다.

각 상수 식을 `case` 레이블이 암시적으로 변환할 수 있는 값을 표시 해야 합니다 ([암시적 변환을](conversions.md#implicit-conversions)) 관리 유형의 `switch` 문. 컴파일 타임 오류가 발생 하는 경우 두 개 이상의 `case` 동일한 레이블 `switch` 문에서 동일한 상수 값을 지정 합니다.

최대 하나만 수 `default` switch 문에서 레이블이 있습니다.

`switch` 문을 다음과 같이 실행 됩니다.

*  Switch 식 평가 되 고 관리 하는 형식으로 변환 합니다.
*  상수 중 하나를 지정 하는 경우는 `case` 동일한 레이블 `switch` 문은 switch 식의 값과 같으면 이면 일치 다음 문 목록으로 제어가 `case` 레이블.
*  경우에 지정 된 상수 `case` 동일한 레이블 `switch` 문을 switch 식의 값과 같지 경우에 `default` 레이블이 있는 경우 목록 다음 문으로 제어가 전달 됩니다는 `default` 레이블입니다.
*  경우에 지정 된 상수 `case` 동일한 레이블 `switch` 문을 switch 식의 값과 같지 경우 `default` 레이블이, 끝점에 제어가 `switch` 문.

Switch 섹션의 문 목록의 끝 지점에 연결할 수 경우 컴파일 타임 오류가 발생 합니다. 이 이동 금지"규칙 이라고 합니다. 이 예제에서
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
없는 스위치 섹션에는 연결 가능한 끝점이 유효 합니다. C 및 c + +와 달리 switch 섹션이 실행 할 권한이 없습니다 "이동"에 다음 스위치 섹션 및 예제
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
컴파일 타임 오류가 발생 합니다. 다른 스위치 섹션에서는 명시적인 실행 하 여 다음 switch 섹션의 실행의 경우 `goto case` 또는 `goto default` 문을 사용 해야 합니다.
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

레이블이 여러 개 허용 되는 *switch_section*합니다. 이 예제에서
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
유효합니다. 예제 때문에 이동 금지"규칙을 위반 하지 않는 레이블을 `case 2:` 하 고 `default:` 동일의 일부인 *switch_section*합니다.

이동 금지"규칙을 사용 하면 C 및 c + +에서 발생 하는 버그의 일반적인 클래스가 때 `break` 실수로 문을 생략 합니다. Switch 섹션을이 규칙으로 인해 또한는 `switch` 문에 문의 동작에 영향을 주지 않고 임의로 다시 정렬할 수 있습니다. 섹션의 예를 들어를 `switch` 문의 동작에 영향을 주지 않고 위의 문은 되돌릴 수 있습니다.
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

Switch 섹션의 문 목록에 일반적으로 종료는 `break`, `goto case`, 또는 `goto default` 문과 비슷하지만 끝점 문 목록에 연결할 수 없는 렌더링 하는 모든 구문을 허용 됩니다. 예를 들어를 `while` 부울 식에 의해 제어 문을 `true` 알려져 접근 불가능 끝점입니다. 마찬가지로, 한 `throw` 또는 `return` 문은 항상 다른 곳에서 제어를 전송 하 고 해당 끝점에 도달 하지 않습니다. 따라서 다음 예제에서는 유효합니다.
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

관리 유형의 `switch` 문 형식 수 `string`입니다. 예를 들어:
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

같은 문자열 같음 연산자 ([문자열 같음 연산자](expressions.md#string-equality-operators)), `switch` 문을 대/소문자 구분 및 스위치 식 문자열을 정확 하 게 일치 하는 경우에 지정된 switch 섹션이 실행 됩니다는 `case` 레이블 상수입니다.

입력을 제어 하는 경우는 `switch` 문이 `string`, 값 `null` case 레이블은 상수 허용 됩니다.

합니다 *statement_list*의 한 *switch_block* 선언 문을 포함할 수 있습니다 ([선언문](statements.md#declaration-statements)). 지역 변수 또는 상수 스위치 블록에서 선언 된 범위가 스위치 블록입니다.

지정 된 스위치 섹션의 문 목록에 연결할 수 경우는 `switch` 문에 연결할 수 이며 다음 중 하나 이상이 true.

*  Switch 식에는 상수가 아닌 값입니다.
*  Switch 식은 일치 하는 상수 값을 `case` 스위치 섹션에는 레이블.
*  Switch 식은 일치 하지 않는 상수 값 `case` 레이블 및 스위치 섹션에 포함 된 `default` 레이블.
*  연결할 수에서 참조 하는 switch 섹션의 스위치 레이블을 `goto case` 또는 `goto default` 문입니다.

끝점에는 `switch` 다음 중 하나 이상이 true 이면 접근할 수:

*  합니다 `switch` 문에 포함을 연결할 수 `break` 문을 끝내는 `switch` 문입니다.
*  합니다 `switch` 접근할 수, switch 식이 상수가 아닌 값 및 no `default` 레이블이 있습니다.
*  합니다 `switch` 접근할 수는 switch 식 일치 하지 않는 상수 값을 `case` 레이블과 아니요 `default` 레이블이 있습니다.

## <a name="iteration-statements"></a>반복 문

반복 문은 포함된 문을 반복적으로 실행합니다.

```antlr
iteration_statement
    : while_statement
    | do_statement
    | for_statement
    | foreach_statement
    ;
```

### <a name="the-while-statement"></a>while 문

`while` 문은 0 개 이상 포함 된 문에 조건부로 실행 합니다.

```antlr
while_statement
    : 'while' '(' boolean_expression ')' embedded_statement
    ;
```

`while` 문을 다음과 같이 실행 됩니다.

*  합니다 *boolean_expression* ([부울 식](expressions.md#boolean-expressions)) 계산 됩니다.
*  부울 식이 `true`, 포함 문으로 제어가 전달 됩니다. 컨트롤에 포함 된 문의 끝 지점에 도달 하는 경우 (실행에서을 `continue` 문)의 시작 부분으로 제어가 `while` 문.
*  부울 식이 `false`를 끝점에 제어가 `while` 문.

포함 된 문에서 `while` 문을 `break` 문 ([break 문을](statements.md#the-break-statement)) 제어 끝점에 전송할 수 있습니다를 `while` (종료 되므로 포함 된 반복 문 문) 및 `continue` 문 ([continue 문을](statements.md#the-continue-statement)) 컨트롤의 끝점이 포함된 된 문 전송할 수 있습니다 (따라서의 또 다른 반복을 수행 합니다 `while` 문).

포함된 문에 `while` 접근할 수 하는 경우는 `while` 접근할 수 및 부울 식의 상수 값이 없는 `false`합니다.

끝점에는 `while` 다음 중 하나 이상이 true 이면 접근할 수:

*  합니다 `while` 문에 포함을 연결할 수 `break` 문을 끝내는 `while` 문입니다.
*  합니다 `while` 접근할 수 및 부울 식의 상수 값이 없는 `true`합니다.

### <a name="the-do-statement"></a>Do 문

`do` 문이 포함된 문을 한 번 이상를 조건부로 실행 합니다.

```antlr
do_statement
    : 'do' embedded_statement 'while' '(' boolean_expression ')' ';'
    ;
```

`do` 문을 다음과 같이 실행 됩니다.

*  포함 된 문으로 제어가 전달 됩니다.
*  컨트롤에 포함 된 문의 끝 지점에 도달 하는 경우 (실행에서을 `continue` 문)의 *boolean_expression* ([부울 식](expressions.md#boolean-expressions)) 평가 됩니다. 부울 식이 `true`, 시작 부분으로 제어가 `do` 문입니다. 그렇지 않으면 제어가 끝점에는 `do` 문입니다.

포함 된 문에서 `do` 문을 `break` 문 ([break 문을](statements.md#the-break-statement)) 제어 끝점에 전송할 수 있습니다를 `do` (종료 되므로 포함 된 반복 문 문)와 `continue` 문 ([continue 문을](statements.md#the-continue-statement)) 컨트롤의 끝점이 포함된 된 문 전송할 수 있습니다.

포함된 문에 `do` 접근할 수 경우는 `do` 접근할 수 있습니다.

끝점에는 `do` 다음 중 하나 이상이 true 이면 접근할 수:

*  합니다 `do` 문에 포함을 연결할 수 `break` 문을 끝내는 `do` 문입니다.
*  포함된 된 문의 끝점에 연결할 수 및 부울 식의 상수 값이 없는 `true`합니다.

### <a name="the-for-statement"></a>문에 대 한

`for` 문을 초기화 식의 순서를 계산 하 고 그런 다음 조건이 true 인 동안 반복 해 서 포함된 문을 실행 하 고 일련의 반복 식 평가 합니다.

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

합니다 *for_initializer*있을 경우 구성 됩니다는 *local_variable_declaration* ([지역 변수 선언](statements.md#local-variable-declarations)) 또는 목록을 *statement_ 식을*s ([식 문은](statements.md#expression-statements)) 쉼표로 구분 합니다. 범위에서 선언 된 지역 변수를 *for_initializer* 에서 시작 합니다 *local_variable_declarator* 변수에 대 한 포함 된 문의 끝에 확장. 범위를 포함 합니다 *for_condition* 하며 *for_iterator*.

합니다 *for_condition*있을 경우 해야를 *boolean_expression* ([부울 식](expressions.md#boolean-expressions)).

*for_iterator*있을 경우 목록으로 구성 됩니다 *statement_expression*s ([식 문은](statements.md#expression-statements)) 쉼표로 구분 합니다.

문에 다음과 같이 실행 됩니다.

*  경우는 *for_initializer* 있는 변수 이니셜라이저 또는 문 식 작성 되는 순서 대로 실행 됩니다. 이 단계는 한 번만 수행 됩니다.
*  경우는 *for_condition* 가 평가 됩니다.
*  경우는 *for_condition* 아니거나 현재 평가 생성 하는 경우 `true`, 포함 문으로 제어가 전달 됩니다. 컨트롤에 포함 된 문의 끝 지점에 도달 하는 경우 (실행에서을 `continue` 문)의 식을 합니다 *for_iterator*있는 순서 대로 평가 됩니다 하 고 다른 반복 하는 경우 평가판 시작을 수행 합니다 *for_condition* 위의 단계에서 합니다.
*  경우는 *for_condition* 이 있고, 계산 생성 `false`의 끝점으로 제어가 `for` 문.

포함 된 문에서 `for` 문을 `break` 문 ([break 문을](statements.md#the-break-statement)) 제어 끝점에 전송할 수 있습니다를 `for` (종료 되므로 포함 된 반복 문 문) 및 `continue` 문 ([continue 문을](statements.md#the-continue-statement)) 컨트롤의 끝점이 포함된 된 문 전송할 수 있습니다 (따라서 실행 합니다 *for_iterator* 및 또 다른 반복을 수행 합니다 `for` 문을 사용 하 여 시작 합니다 *for_condition*).

포함된 문에 `for` 다음 중 하나가 참인 경우에 접근할 수:

*  `for` 접근할 수 없으며 *for_condition* 가 있습니다.
*  합니다 `for` 접근할 수와 *for_condition* 있고 상수 값이 없는 `false`합니다.

끝점에는 `for` 다음 중 하나 이상이 true 이면 접근할 수:

*  합니다 `for` 문에 포함을 연결할 수 `break` 문을 끝내는 `for` 문입니다.
*  합니다 `for` 접근할 수와 *for_condition* 있고 상수 값이 없는 `true`합니다.

### <a name="the-foreach-statement"></a>Foreach 문

`foreach` 문 컬렉션의 각 요소에 대해 포함된 문을 실행 하 여 컬렉션의 요소를 열거 합니다.

```antlr
foreach_statement
    : 'foreach' '(' local_variable_type identifier 'in' expression ')' embedded_statement
    ;
```

합니다 *형식* 및 *식별자* 의 `foreach` 문에서 선언 합니다 ***반복 변수*** 문의 합니다. 경우는 `var` 식별자로 지정 됩니다 합니다 *local_variable_type*, 및 명명 된 형식이 없는 `var` 는 범위에 반복 변수 라고는 ***암시적으로 형식화 된 반복 변수***, 해당 종류의 요소 형식으로 간주 됩니다 및는 `foreach` 아래 지정 된 대로 문. 반복 변수는 포함된 된 문을 통해 확장 하는 범위를 사용 하 여 읽기 전용 지역 변수에 해당 합니다. 실행 하는 동안는 `foreach` 문의 반복 변수는 반복은 현재 수행 중인 컬렉션 요소를 나타냅니다. 컴파일 타임 오류가 발생 한 포함된 문을 반복 변수를 수정 하려고 하는 경우 (할당을 통해 또는 `++` 및 `--` 연산자)으로 반복 변수를 전달 하거나를 `ref` 또는 `out` 매개 변수.

간단히 하기 위해 다음 표에 `IEnumerable`, `IEnumerator`, `IEnumerable<T>` 및 `IEnumerator<T>` 네임 스페이스에서 해당 형식을 참조할 `System.Collections` 및 `System.Collections.Generic`합니다.

Foreach 문 처리 하는 컴파일 타임 먼저 확인 합니다 ***컬렉션 형식을***, ***열거자 유형을*** 및 ***요소 형식*** 식의 합니다. 이 결정 다음과 같이 진행 됩니다.

*  경우 형식 `X` 의 *식* 은 배열 형식에서 암시적 참조 변환 됩니다 `X` 하는 `IEnumerable` 인터페이스 (있으므로 `System.Array` 이 인터페이스를 구현). ***컬렉션 형식*** 는 `IEnumerable` 인터페이스는 ***열거자 유형을*** 는 `IEnumerator` 인터페이스 및 ***요소 형식*** 의 요소 형식인는 배열 형식 `X`합니다.
*  경우 형식 `X` 의 *식* 됩니다 `dynamic` 는 암시적으로 변환 됩니다 *식* 에 `IEnumerable` 인터페이스 ([암시적 동적 변환](conversions.md#implicit-dynamic-conversions)). ***컬렉션 형식*** 은 합니다 `IEnumerable` 인터페이스 및 ***열거자 유형을*** 는 `IEnumerator` 인터페이스. 경우는 `var` 식별자로 지정 됩니다는 *local_variable_type* 그런 다음 ***요소 형식*** 는 `dynamic`, 그렇지 않으면 `object`합니다.
*  그렇지 않은 경우 확인 여부를 형식 `X` 에 적절 한 `GetEnumerator` 메서드:
   * 형식에서 멤버 조회를 수행 `X` 식별자를 사용 하 여 `GetEnumerator` 형식 인수 없이 합니다. 멤버 조회 일치 항목을 생성 하지 않거나 모호성이, 또는 메서드 그룹이 없는 일치 하는, 아래 설명 된 대로 열거 가능한 인터페이스에 대 한 확인 합니다. 멤버 조회는 메서드 그룹 또는 일치를 제외한 모든 항목을 생성 하는 경우 경고가 발생 하는 것이 좋습니다.
   * 빈 인수 목록 및 생성 된 메서드 그룹을 사용 하 여 오버 로드 확인을 수행 합니다. 오버 로드 확인 결과에서 해당 메서드가 없는 경우 모호성을 발생 하거나 가장 적합 한 메서드가 해당 메서드가 아래 설명 된 대로 열거 가능한 인터페이스에 대 한 정적 또는 공용이 아닙니다 확인이 발생 합니다. 오버 로드 확인 모호 하지 않은 공용 인스턴스 메서드 또는 해당 메서드가 없는 제외한 모든 항목을 생성 하는 경우 경고가 발생 하는 것이 좋습니다.
   * 반환 형식이 `E` 의 `GetEnumerator` 메서드는 클래스, 구조체 또는 인터페이스 형식, 오류가 생성 됩니다 아니며 추가 단계가 수행 되지 않습니다.
   * 멤버 조회에 이루어집니다 `E` 식별자를 사용 하 여 `Current` 형식 인수 없이 합니다. 멤버 조회에 일치 하는 항목이 생성, 결과 오류 또는 결과 읽기를 허용 하는 공용 인스턴스 속성을 제외 하 고, 경우에 오류가 생성 되 고 추가 단계가 수행 되지 않습니다.
   * 멤버 조회에 이루어집니다 `E` 식별자를 사용 하 여 `MoveNext` 형식 인수 없이 합니다. 멤버 조회에 일치 하는 항목이 생성, 결과 오류 또는 결과 메서드 그룹을 제외 하 고, 경우에 오류가 생성 되 고 추가 단계가 수행 되지 않습니다.
   * 오버 로드 확인은 빈 인수 목록이 있는 메서드 그룹에서 수행 됩니다. 없는 해당 메서드, 모호성을에서 제거 결과 나 결과에 가장 적합 한 메서드가 해당 메서드 오버 로드 확인 결과 정적 또는 공용이 아닙니다 되었거나 해당 반환 형식이 없는 경우 `bool`오류가 생성 되 고 추가 단계가 수행 되지 않습니다.
   * ***컬렉션 형식*** 는 `X`의 ***열거자 유형을*** 은 `E`, 및 ***요소 형식*** 유형의 `Current` 속성.

*  그렇지 않으면 열거 가능한 인터페이스에 대 한 확인 합니다.
   * 경우 모든 형식 간의 `Ti` 에 암시적 변환이 `X` 에 `IEnumerable<Ti>`, 고유한 유형이 `T` 되도록 `T` 아닙니다 `dynamic` 및 다른 모든 `Ti` 있는지는 암시적으로 변환 `IEnumerable<T>` 에 `IEnumerable<Ti>`, 해당 ***컬렉션 형식*** 는 인터페이스 `IEnumerable<T>`의 ***열거자 유형을*** 인터페이스`IEnumerator<T>`, 및 ***요소 형식이*** 는 `T`합니다.
   * 이러한 형식이 둘 이상 있으면 그러지 `T`, 다음 오류가 생성 되 고 추가 단계가 수행 되지 않습니다.
   * 암시적 변환이 없는 경우에 그렇지 `X` 에 `System.Collections.IEnumerable` 인터페이스를 해당 ***컬렉션 형식*** 는이 인터페이스는 ***열거자 유형을*** 인터페이스입니다`System.Collections.IEnumerator`, 및 ***요소 형식이*** 는 `object`합니다.
   * 그렇지 않으면 오류가 발생 하 고 추가 단계가 수행 되지 않습니다.

위의 단계를 성공 하면 컬렉션 형식을 생성할 명확 `C`, 열거자 유형을 `E` 형식과 요소 `T`합니다. 폼의 foreach 문
```csharp
foreach (V v in x) embedded_statement
```
확장 한 다음:
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

변수의 `e` 표시 또는 식에 액세스할 수 없는 `x` 포함된 문을 또는 프로그램의 다른 소스 코드입니다. 변수의 `v` 포함 된 문에서 읽기 전용입니다. 명시적 변환이 없는 경우 ([명시적 변환](conversions.md#explicit-conversions))에서 `T` (요소 형식)에 `V` (합니다 *local_variable_type* foreach 문에서), 오류가 발생 및 추가 단계가 수행 되지 않습니다. 하는 경우 `x` 기본값이 `null`, `System.NullReferenceException` 런타임에 throw 됩니다.

동작은 위의 확장과 일치으로 성능상의 이유로, 예: 지정 된 foreach 문에서 다르게 구현에 구현을 허용 됩니다.

배치 `v` while 루프는 익명 함수에서 발생 하 여 캡처 방법에 대 한 중요 합니다 *embedded_statement*합니다.

예를 들어:
```csharp
int[] values = { 7, 9, 13 };
Action f = null;

foreach (var value in values)
{
    if (f == null) f = () => Console.WriteLine("First value: " + value);
}

f();
```
경우 `v` while 외부에서 선언 된 루프 후 해당 값 및 모든 반복 간에 공유할 수는에 대 한 루프 최종 값을 `13`, 인 어떤 호출 `f` 인쇄 합니다. 대신, 각 반복에 고유한 변수 때문에 `v`에서 캡처한 것 `f` 첫 번째에서 반복 값을 보유할 계속 `7`, 인쇄 될 모양을입니다. (참고: 이전 버전의 C# 선언 `v` 외부 while 루프.)

본문은 블록 다음 단계에 따라 생성 되는 마지막으로:

*  암시적 변환이 없으면 `E` 에 `System.IDisposable` 다음 인터페이스
   *  경우 `E` nullable이 아닌 값 형식인 경우 의미 체계에 해당 하는 절 확장 되어 마지막:

      ```csharp
      finally {
          ((System.IDisposable)e).Dispose();
      }
      ```

   *  그렇지 않은 경우의 의미 체계에 해당 하는 절 확장 되어 마지막:

      ```csharp
      finally {
          if (e != null) ((System.IDisposable)e).Dispose();
      }
      ```

   단 `E` 값 형식 인지 값 형식으로 캐스팅을 인스턴스화할 형식 매개 변수 `e` 에 `System.IDisposable` 되려면 boxing이 발생 하지 것입니다.

*  그렇지 않은 경우, `E` 형식이 봉인 된 절은 빈 블록으로 확장 되는 마지막으로:

   ```csharp
   finally {
   }
   ```

*  그렇지 않은 경우는 마지막 절을 확장 하 여:

   ```csharp
   finally {
       System.IDisposable d = e as System.IDisposable;
       if (d != null) d.Dispose();
   }
   ```    

   지역 변수 `d` 에 보이지 않거나 사용자 코드에 액세스할 수 있습니다. 특히 해당 범위에 포함 되는 다른 모든 변수와 충돌 하지 않는 finally 블록을 사용 합니다.

순서 `foreach` 배열의 요소를 이동 하면서, 다음과 같습니다: 단일 차원 배열의 요소 인덱스의 오름차순으로 트래버스 됩니다에 대 한 인덱스를 사용 하 여 시작 `0` 인덱스까지 `Length - 1`입니다. 다차원 배열에 대 한 요소는 오른쪽에 있는 차원의 인덱스가 향상 된 첫 번째 왼쪽에 등 다음 왼쪽된 차원 트래버스 됩니다.

다음 예제에서는 요소 순서에서 2 차원 배열의 각 값 인쇄합니다.
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
생성 된 출력은 다음과 같습니다.
```csharp
1.2 2.3 3.4 4.5 5.6 6.7 7.8 8.9
```

예제
```csharp
int[] numbers = { 1, 3, 5, 7, 9 };
foreach (var n in numbers) Console.WriteLine(n);
```
유형의 `n` 로 유추 됩니다 `int`의 요소 형식 `numbers`합니다.

## <a name="jump-statements"></a>점프 문

무조건 점프 문이 제어를 전송 합니다.

```antlr
jump_statement
    : break_statement
    | continue_statement
    | goto_statement
    | return_statement
    | throw_statement
    ;
```

점프 문이 제어를 전송 하는 위치 라고 합니다 ***대상*** 점프 문의 합니다.

점프 문 블록 내에서 발생 하 고 해당 점프 문의 대상이 블록 외부에 점프 문을 라고 ***종료*** 블록입니다. 점프 문 블록 밖으로 제어를 전송할 수 있습니다, 있지만 블록으로 제어를 전송 하지 않습니다 것입니다.

중간으로 점프 문의 실행은 복잡 `try` 문입니다. 예: 없는 경우에서 `try` 문, 점프 문에 무조건에서 제어를 전달 점프 문이 해당 대상으로 합니다. 이러한 중간 경우 `try` 문 실행은 더 복잡 합니다. 하나 이상의 점프 문이 종료 되 면 `try` 블록에 연결 `finally` 제어 블록은 처음에 전송 합니다 `finally` 가장 안쪽의 블록 `try` 문. 컨트롤의 끝점에 도달 하는 경우는 `finally` 컨트롤 블록으로 전송 됩니다는 `finally` 다음 바깥쪽 블록 `try` 문. 때까지이 프로세스를 반복 합니다 `finally` 모두의 블록 중간 `try` 문이 실행 되었습니다.

예제
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
합니다 `finally` 블록과 연결 된 두 `try` 점프 문의 대상이 제어가 전에 문이 실행 됩니다.

생성 된 출력은 다음과 같습니다.
```
Before break
Innermost finally block
Outermost finally block
After break
```

### <a name="the-break-statement"></a>Break 문

합니다 `break` 문은 가장 가까운 바깥쪽 종료 `switch`, `while`, `do`를 `for`, 또는 `foreach` 문.

```antlr
break_statement
    : 'break' ';'
    ;
```

대상을 `break` 문은 가장 가까운 바깥쪽 끝 지점인 `switch`, `while`, `do`를 `for`, 또는 `foreach` 문. 경우는 `break` 문에 포함 되지 않는를 `switch`, `while`, `do`, `for`, 또는 `foreach` 문에 컴파일 타임 오류가 발생 하는 합니다.

때 여러 `switch`, `while`를 `do`, `for`, 또는 `foreach` 문을 서로 중첩 되어를 `break` 문은 가장 안쪽의 문을에 적용 됩니다. 여러 중첩 수준에서 제어를 전송 하는 `goto` 문 ([goto 문을](statements.md#the-goto-statement))를 사용 해야 합니다.

A `break` 문을 종료할 수 없는 한 `finally` 블록 ([try 문](statements.md#the-try-statement)). 때를 `break` 문 내에서 발생을 `finally` 블록의 대상을 `break` 문은 동일한 이어야 합니다. `finally` 차단. 그렇지 않으면 컴파일 타임 오류가 발생 합니다.

`break` 문을 다음과 같이 실행 됩니다.

*  경우는 `break` 문은 하나 이상의 종료 `try` 블록에 연결 `finally` 제어 블록은 처음에 전송 합니다 `finally` 가장 안쪽의 블록 `try` 문. 컨트롤의 끝점에 도달 하는 경우는 `finally` 컨트롤 블록으로 전송 됩니다는 `finally` 다음 바깥쪽 블록 `try` 문. 때까지이 프로세스를 반복 합니다 `finally` 모두의 블록 중간 `try` 문이 실행 되었습니다.
*  대상에 제어가 `break` 문입니다.

때문에 `break` 문을 무조건 제어 전송 다른 곳에서 끝점에는 `break` 문에 접근할 수 없습니다.

### <a name="the-continue-statement"></a>Continue 문

합니다 `continue` 문은 가장 가까운 바깥쪽의 새로운 반복을 시작 `while`, `do`, `for`, 또는 `foreach` 문입니다.

```antlr
continue_statement
    : 'continue' ';'
    ;
```

대상을 `continue` 문은 가장 가까운 바깥쪽 포함 된 문의 끝 점이 `while`, `do`, `for`, 또는 `foreach` 문입니다. 경우는 `continue` 문에 포함 되지 않는를 `while`, `do`, `for`, 또는 `foreach` 문에 컴파일 타임 오류가 발생 하는 합니다.

때 여러 `while`, `do`를 `for`, 또는 `foreach` 문을 서로 중첩 되어를 `continue` 문은 가장 안쪽의 문을에 적용 됩니다. 여러 중첩 수준에서 제어를 전송 하는 `goto` 문 ([goto 문을](statements.md#the-goto-statement))를 사용 해야 합니다.

A `continue` 문을 종료할 수 없는 한 `finally` 블록 ([try 문](statements.md#the-try-statement)). 경우는 `continue` 문 내에서 발생를 `finally` 블록의 대상을 `continue` 문은 동일한 이어야 합니다. `finally` ; 그렇지 않으면 컴파일 타임 오류가 발생 합니다.

`continue` 문을 다음과 같이 실행 됩니다.

*  경우는 `continue` 문은 하나 이상의 종료 `try` 블록에 연결 `finally` 제어 블록은 처음에 전송 합니다 `finally` 가장 안쪽의 블록 `try` 문. 컨트롤의 끝점에 도달 하는 경우는 `finally` 컨트롤 블록으로 전송 됩니다는 `finally` 다음 바깥쪽 블록 `try` 문. 때까지이 프로세스를 반복 합니다 `finally` 모두의 블록 중간 `try` 문이 실행 되었습니다.
*  대상에 제어가 `continue` 문입니다.

때문에 `continue` 문을 무조건 제어 전송 다른 곳에서 끝점에는 `continue` 문에 접근할 수 없습니다.

### <a name="the-goto-statement"></a>goto 문

`goto` 문은 레이블에 의해 표시 된 문으로 제어를 전달 합니다.

```antlr
goto_statement
    : 'goto' identifier ';'
    | 'goto' 'case' constant_expression ';'
    | 'goto' 'default' ';'
    ;
```

대상 된 `goto` *식별자* 문은 지정 된 레이블로 레이블이 지정 된 문. 지정 된 이름을 사용 하 여 레이블을 현재 함수 멤버에 존재 하지 않는 경우 또는 경우는 `goto` 문은 아닙니다 레이블의 범위 내에서 컴파일 타임 오류가 발생 합니다. 이 규칙에 사용할 수는 `goto` 문은 중첩 된 범위를 벗어날 포함 되지 않습니다 중첩된 된 범위 컨트롤을 전송 합니다. 예제
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
`goto` 문을 사용 하 여 중첩 된 범위 밖으로 제어를 전송 합니다.

대상을 `goto case` 문에 가장 가까운 바깥쪽에서 문 목록의 `switch` 문 ([switch 문](statements.md#the-switch-statement))를 포함 하는 `case` 주어진된 상수 값을 사용 하 여 레이블을. 경우는 `goto case` 문에 포함 되지 않는를 `switch` 문을 경우는 *constant_expression* 암시적으로 변환 되지 않습니다 ([암시적 변환을](conversions.md#implicit-conversions)) 관리 형식에는 바깥쪽에 가장 가까운 `switch` 문 또는 경우에 가장 가까운 바깥쪽 `switch` 문에 포함 되지 않습니다는 `case` 컴파일 타임 오류가 발생 하는 주어진된 상수 값을 사용 하 여 레이블.

대상을 `goto default` 문에 가장 가까운 바깥쪽에서 문 목록의 `switch` 문 ([switch 문](statements.md#the-switch-statement))를 포함 하는 `default` 레이블. 경우는 `goto default` 문에 포함 되지 않는를 `switch` 문을 경우 가장 가까운 바깥쪽 `switch` 문에 포함 되지 않습니다는 `default` 레이블, 컴파일 시간 오류가 발생 하는 합니다.

A `goto` 문을 종료할 수 없는 한 `finally` 블록 ([try 문](statements.md#the-try-statement)). 경우는 `goto` 문 내에서 발생을 `finally` 블록의 대상을 `goto` 문은 동일한 이어야 합니다. `finally` 블록 그렇지 않으면 컴파일 타임 오류가 발생 하거나.

`goto` 문을 다음과 같이 실행 됩니다.

*  경우는 `goto` 문은 하나 이상의 종료 `try` 블록에 연결 `finally` 제어 블록은 처음에 전송 합니다 `finally` 가장 안쪽의 블록 `try` 문. 컨트롤의 끝점에 도달 하는 경우는 `finally` 컨트롤 블록으로 전송 됩니다는 `finally` 다음 바깥쪽 블록 `try` 문. 때까지이 프로세스를 반복 합니다 `finally` 모두의 블록 중간 `try` 문이 실행 되었습니다.
*  대상에 제어가 `goto` 문입니다.

때문에 `goto` 문을 무조건 제어 전송 다른 곳에서 끝점에는 `goto` 문에 접근할 수 없습니다.

### <a name="the-return-statement"></a>Return 문

`return` 함수는 현재 호출자에 게 컨트롤을 반환 하는 명령문은 `return` 문이 나타나는 합니다.

```antlr
return_statement
    : 'return' expression? ';'
    ;
```

A `return` 식이 없는 문 결과 형식이 포함 된 메서드 즉, 값을 계산 하지 않습니다 하는 함수 멤버 에서만에서 사용할 수 있습니다 ([메서드 본문](classes.md#method-body)) `void`는 `set` 속성의 접근자 또는 인덱서는 `add` 고 `remove` 이벤트, 인스턴스 생성자, 정적 생성자 또는 소멸자의 접근자입니다.

A `return` 는 void가 아닌 결과 형식이 있는 메서드 즉, 값을 계산 하는 함수 멤버 식 사용 하 여 문을 사용할 수 있습니다는 `get` 속성 또는 인덱서 또는 사용자 정의 연산자의 접근자입니다. 암시적으로 변환 ([암시적 변환을](conversions.md#implicit-conversions)) 식의 형식에서 포함 하는 함수 멤버의 반환 형식으로 존재 해야 합니다.

반환 문 익명 함수 식의 본문에 사용할 수도 있습니다 ([익명 함수 식](expressions.md#anonymous-function-expressions)), 이러한 함수는 변환이 존재 여부 확인에 참여 합니다.

에 대 한 컴파일 시간 오류를 `return` 나타나지 문을 `finally` 블록 ([try 문](statements.md#the-try-statement)).

`return` 문을 다음과 같이 실행 됩니다.

*  경우는 `return` 문에서 식을 지정 된 식이 계산 되 고 결과 값을 암시적으로 변환 하 여 포함 된 함수의 반환 형식으로 변환 됩니다. 변환의 결과 함수에 의해 생성 된 결과 값이 됩니다.
*  경우는 `return` 문을 하나 이상으로 묶입니다 `try` 또는 `catch` 블록을 연결 된 `finally` 제어 블록은 처음에 전송 합니다 `finally` 가장 안쪽의 블록 `try` 문. 컨트롤의 끝점에 도달 하는 경우는 `finally` 컨트롤 블록으로 전송 됩니다는 `finally` 다음 바깥쪽 블록 `try` 문. 될 때까지이 프로세스를 반복 합니다 `finally` 모든 바깥쪽 블록 `try` 문이 실행 되었습니다.
*  포함 하는 비동기 함수를 없는 경우 컨트롤이 있는 경우 결과 값과 함께 포함 된 함수의 호출자에 게 반환 됩니다.
*  포함 된 함수는 비동기 함수, 현재 호출자에 게 컨트롤이 반환 된 결과 값에 있는 경우에 기록 됩니다 반환 작업에 설명 된 대로 경우 ([열거자 인터페이스](classes.md#enumerator-interfaces)).

때문에 `return` 문을 무조건 제어 전송 다른 곳에서 끝점에는 `return` 문에 접근할 수 없습니다.

### <a name="the-throw-statement"></a>Throw 문

`throw` 문은 예외를 throw 합니다.

```antlr
throw_statement
    : 'throw' expression? ';'
    ;
```

`throw` 문 식 사용 하 여 식을 평가 하 여 생성 한 값을 throw 합니다. 식은 클래스 형식 값을 표시 해야 합니다 `System.Exception`에서 파생 된 클래스 형식의 `System.Exception` 있는 매개 변수 형식 또는 `System.Exception` (또는 그 하위 클래스) 유효한 기본 클래스로 합니다. 식의 평가 생성 하는 경우 `null`, `System.NullReferenceException` 대신 throw 됩니다.

A `throw` 식이 없는 문은 에서만 사용할 수 있습니다를 `catch` 문의 하 여 현재 처리 되는 예외 다시 throw 되는 경우 차단 `catch` 블록.

때문에 `throw` 문을 무조건 제어 전송 다른 곳에서 끝점에는 `throw` 문에 접근할 수 없습니다.

예외가 throw 되 면 제어가 첫 번째 `catch` 바깥쪽 절 `try` 예외를 처리할 수 있는 문. 적합 한 예외 처리기로 제어를 전송 지점으로 throw 되는 예외 지점에서 발생 하는 프로세스 라고 ***예외 전파***합니다. 예외가 전파 될 때까지 다음 단계를 반복 해 서 실행 구성는 `catch` 예외와 일치 하는 절을 찾을 수 있습니다. 이 설명에는 ***지점 throw*** 위치인 처음에 예외가 throw 됩니다.

*  현재 함수 멤버의 각 `try` throw 지점을 포함 하는 문을 검사 합니다. 각 문에 대해 `S`부터 시작 하 여 가장 안쪽 `try` 문과 바깥쪽로 끝나는 `try` 문을 다음 단계를 평가:

   * 경우는 `try` 블록 `S` 되었던 throw 지점을 포함 고 S에 하나 이상의 `catch` 절을 `catch` 절에 지정 된 규칙에 따라 예외에 대 한 적절 한 처리기를 찾으려고 모양의 순서 대로 검사 됩니다 섹션 [try 문](statements.md#the-try-statement)합니다. 일치 하는 경우 `catch` 절을 블록에 제어를 전송 하 여 완료 된 예외 전파 `catch` 절.

   * 그렇지 않은 경우, 합니다 `try` 블록 또는 `catch` 블록 `S` 되었던 throw 지점을 포함 경우 `S` 에 `finally` 제어 블록으로 전송 됩니다는 `finally` 블록. 경우는 `finally` 다른 예외를 throw 하는 블록, 현재 예외는 처리 종료 됩니다. 컨트롤의 끝점에 도달 하는 경우 그러지는 `finally` 블록, 현재 예외 처리가 계속 됩니다.

*  예외 처리기가 없는 경우 현재 함수 호출에서은 함수 호출이 종료 되 면 하 고 다음 중 하나에 발생 합니다.

   * 현재 함수의 경우 비동기가 아닌 경우 위의 단계에 해당 하는 함수 멤버를 호출한 문으로 throw 지점과 함수의 호출자가 반복 됩니다.

   * 현재 함수가 인 비동기 작업을 반환 하는 경우 예외에 설명 된 대로 오류 또는 취소 됨 상태로 전환 됩니다는 작업의 반환에 기록 됩니다 [열거자 인터페이스](classes.md#enumerator-interfaces)합니다.

   * 에 설명 된 대로 현재 스레드의 동기화 컨텍스트를 현재 함수가 void를 반환 하 고 비동기 이면 알려집니다 [열거 가능 인터페이스](classes.md#enumerable-interfaces)합니다.

*  예외 처리 종료는 현재 스레드에서 모든 함수 멤버를 호출 하는 경우 스레드가 예외에 대 한 처리기를 나타내는 다음는 스레드는 자체 종료입니다. 이런 종료가 미치는 구현 시 정의 됩니다.

## <a name="the-try-statement"></a>Try 문

`try` 문 블록을 실행 하는 동안 발생 하는 예외를 catch 하기 위한 메커니즘을 제공 합니다. 또한 합니다 `try` 문은 컨트롤을 벗어나면 항상 실행 되는 코드 블록을 지정 하는 기능을 제공 합니다 `try` 문입니다.

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

가능한 세 가지 형태가 `try` 문:

*  A `try` 하나 이상의 뒤에 블록 `catch` 블록입니다.
*  A `try` 블록 뒤에 `finally` 블록입니다.
*  A `try` 하나 이상의 블록 뒤 `catch` 뒤에 블록을 `finally` 블록.

경우는 `catch` 절 지정를 *exception_specifier*, 형식 이어야 `System.Exception`에서 파생 된 형식 `System.Exception` 또는 형식 매개 변수 형식에 `System.Exception` (또는 그 하위 클래스) 해당 효율적으로 기본 클래스입니다.

경우는 `catch` 절 모두 지정는 *exception_specifier* 사용 하 여는 *식별자*, ***예외 변수의*** 선언 된 지정 된 이름 및 형식. 지역 변수를 통해 확장 하는 범위에 해당 하는 예외 변수는 `catch` 절. 실행 하는 동안 합니다 *exception_filter* 하 고 *블록*, 예외 변수의 현재 처리 중인 예외를 나타냅니다. 한정 된 할당 검사를 위해 예외 변수는 해당 전체 범위에 할당으로 간주 됩니다.

하지 않는 한는 `catch` 절 예외 변수 이름이 포함, 필터에서 예외 개체에 액세스할 수 없는 및 `catch` 블록입니다.

A `catch` 절을 지정 하지 않는 *exception_specifier* 는 일반 라고 `catch` 절.

일부 프로그래밍 언어에서 파생 된 개체에 표현할 수 없는 예외를 지원할 수 있습니다 `System.Exception`이지만 C# 코드에서 이러한 예외를 생성할 수 없습니다. 일반적인 `catch` 이러한 예외를 catch 할 절을 사용할 수 있습니다. 따라서 일반적인 `catch` 절은 형식을 지정 하는 의미 체계가 다르므로 `System.Exception`전자 수 다른 언어에서 예외 catch도 해당 합니다.

예외에 대 한 처리기를 찾기 위해 `catch` 절 사전적 순서 대로 검사 됩니다. 경우는 `catch` 절 형식을 있지만 예외 필터가 지정, 나중에 대 한 것은 컴파일 타임 오류 `catch` 동일한 절 `try` 형식이 동일 하거나에서 파생 된 형식을 지정 하는 문입니다. 경우는 `catch` 형식 및 필터가 절 지정, 마지막 이어야 합니다 `catch` 절에 대 한 `try` 문.

내를 `catch` 블록을 `throw` 문 ([throw 문을](statements.md#the-throw-statement)) 식 수에서 발생 된 예외 다시 throw 하는 `catch` 블록. 할당 된 예외 변수를 다시 throw 되는 예외를 변경 하지 않습니다.

예제
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
메서드가 `F` 예외를 catch 하, 콘솔에 일부 진단 정보를 기록, 예외 변수를 변경 및 예외를 다시 throw 합니다. 생성 된 출력은 다시 throw 되는 예외는 원래 예외:
```
Exception in F: G
Exception in Main: G
```

첫 번째 catch 블록에서 throw가 `e` 현재 예외를 다시 throw 하는 대신 생성 된 출력은 다음과 같을 수 있습니다.
```csharp
Exception in F: G
Exception in Main: F
```

에 대 한 컴파일 시간 오류를 `break`, `continue`, 또는 `goto` 문 밖으로 제어를 전송 하는 `finally` 블록. 경우는 `break`, `continue`, 또는 `goto` 문이에서 `finally` 문의 대상 블록은 동일한 내에 있어야 합니다. `finally` 블록 그렇지 않으면 컴파일 타임 오류가 발생 하거나 합니다.

에 대 한 컴파일 시간 오류를 `return` 에서 발생 하는 문을 `finally` 블록입니다.

`try` 문을 다음과 같이 실행 됩니다.

*  제어가 `try` 블록입니다.
*  컨트롤의 끝점에 도달 하는 경우는 `try` 블록:
   *  경우는 `try` 문에 `finally` 블록을 `finally` 블록이 실행 됩니다.
   *  끝점으로 제어가 `try` 문입니다.

*  예외가 전파 되는 경우는 `try` 문을 실행 하는 동안는 `try` 블록:
   *  `catch` 절에 있는 경우 순서 대로 검사 됩니다 모양의 예외에 대 한 적절 한 처리기를 찾을 수 있습니다. 경우는 `catch` 절 형식을 지정 하지 않거나 예외 나 예외 형식의 기본 형식을 지정 합니다.
      *  경우는 `catch` 예외 변수를 선언 하는 절, 예외 개체는 예외 변수에 할당 됩니다.
      *  경우는 `catch` 절 선언 예외 필터, 필터를 계산 합니다. 로 평가 되 면 `false`, catch 절이 일치 하는 항목 및 검색을 통해 계속 후속 `catch` 절 적합 한 처리기입니다.
      *  그렇지 않으면 합니다 `catch` 절에는 일치 하는 것으로 간주 됩니다 및 제어가 일치 하는 `catch` 블록입니다.
      *  컨트롤의 끝점에 도달 하는 경우는 `catch` 블록:
         * 경우는 `try` 문에 `finally` 블록을 `finally` 블록이 실행 됩니다.
         * 끝점으로 제어가 `try` 문입니다.
      *  예외가 전파 되는 경우는 `try` 문을 실행 하는 동안는 `catch` 블록:
         *  경우는 `try` 문에 `finally` 블록을 `finally` 블록이 실행 됩니다.
         *  다음 바깥쪽 예외가 전파 됩니다 `try` 문입니다.
   *  경우는 `try` 문이 아무런 `catch` 절 없으면 또는 `catch` 절 예외와 일치:
      *  경우는 `try` 문에 `finally` 블록을 `finally` 블록이 실행 됩니다.
      *  다음 바깥쪽 예외가 전파 됩니다 `try` 문입니다.

문의 `finally` 컨트롤을 벗어나면 블록이 항상 실행 됩니다는 `try` 문입니다. 마찬가지 제어 전송을 실행 한 결과로 일반 실행의 결과로 발생 하는 여부는 `break`, `continue`, `goto`, 또는 `return` 문, 또는 예외 전파의 결과로 `try` 문입니다.

작업을 실행 하는 동안 예외가 발생 하는 경우는 `finally` 블록과 잡히지 않는 다음 바깥쪽 동일 finally 블록 내에서 예외가 전파 됩니다 `try` 문입니다. 다른 예외 전파 되 고 있으면 해당 예외가 손실 됩니다. 예외를 전파 하는 과정 설명의 설명에 추가 합니다 `throw` 문 ([throw 문을](statements.md#the-throw-statement)).

`try` 블록을 `try` 접근할 수 경우는 `try` 접근할 수 있습니다.

`catch` 블록을 `try` 접근할 수 하는 경우는 `try` 접근할 수 있습니다.

`finally` 블록을 `try` 접근할 수 경우는 `try` 접근할 수 있습니다.

끝점에는 `try` 다음 두 가지 경우에 접근할 수:

*  끝점에는 `try` 블록에 연결할 수 또는 하나 이상의의 끝 지점 `catch` 블록에 연결할 수 있습니다.
*  경우는 `finally` 블록이 있는지 끝점에는 `finally` 블록에 연결할 수 있습니다.

## <a name="the-checked-and-unchecked-statements"></a>Checked 및 unchecked 문

`checked` 하 고 `unchecked` 제어 문을 사용 하는 ***오버플로 검사 컨텍스트에*** 정수 형식 산술 연산 및 변환에 대 한 합니다.

```antlr
checked_statement
    : 'checked' block
    ;

unchecked_statement
    : 'unchecked' block
    ;
```

`checked` 문을 사용 하면 모든 식에는 *블록* 확인 된 컨텍스트에서 계산할 및 `unchecked` 문을 사용 하면 모든 식에는 *블록* 평가할는 unchecked 컨텍스트를 합니다.

합니다 `checked` 및 `unchecked` 문은 정확 하 게 일치 합니다 `checked` 및 `unchecked` 연산자 ([checked 및 unchecked 연산자](expressions.md#the-checked-and-unchecked-operators)) 식 대신 블록에서 작동 한다는 점을 제외 하면, .

## <a name="the-lock-statement"></a>Lock 문

`lock` 문에 지정된 된 개체에 대 한 상호 배제 잠금을 가져오고, 문을 실행 하 고 다음 잠금을 해제 합니다.

```antlr
lock_statement
    : 'lock' '(' expression ')' embedded_statement
    ;
```

식을 `lock` 문을 것으로 알려진 형식의 값을 표시 해야 합니다는 *reference_type*합니다. 암시적 boxing 변환 작업 없이 ([Boxing 변환](conversions.md#boxing-conversions))의 식에 수행한 적이 되는 `lock` 문, 따라서 되며의 값을 나타내는 식에 대 한 컴파일 시간 오류를를 *value_type*.

`lock` 폼의 문
```csharp
lock (x) ...
```
여기서 `x` 식입니다를 *reference_type*는 동일 합니다.
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
단, `x`가 한 번만 계산됩니다.

상호 배타적 잠금이 유지 되는 동안 동일한 실행 스레드에서 실행 되는 코드 또한 가져오고 수 잠금을 해제 합니다. 그러나 다른 스레드에서 실행 되는 코드에서 잠금이 해제 될 때까지 잠금을 가져올 차단 됩니다.

잠금 `System.Type` 정적 데이터에 대 한 액세스를 동기화 하기 위해 개체 권장 되지 않습니다. 다른 코드 교착 상태가 발생할 수 있는 동일한 형식에 대해 잠글 수 있습니다. 전용 정적 개체를 잠그는 방식으로 정적 데이터에 대 한 액세스를 동기화 하는 것이 좋습니다. 예를 들어:
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

## <a name="the-using-statement"></a>using 문

`using` 문을 하나 이상의 리소스를 가져오고, 문을 실행 하 고 리소스를 삭제 합니다.

```antlr
using_statement
    : 'using' '(' resource_acquisition ')' embedded_statement
    ;

resource_acquisition
    : local_variable_declaration
    | expression
    ;
```

A ***리소스*** 는 클래스 또는 구조체를 구현 하는 `System.IDisposable`, 라는 단일 매개 변수가 없는 메서드를 포함 하는 `Dispose`합니다. 리소스를 사용 하는 코드를 호출할 수 `Dispose` 더 이상 필요 없는 리소스를 나타냅니다. 경우 `Dispose` 자동 삭제가 가비지 컬렉션의 결과로 발생 한 다음는 호출 되지 않습니다.

경우 형식의 *resource_acquisition* 됩니다 *local_variable_declaration* 의 형식은 합니다 *local_variable_declaration* 중 하나 여야 합니다 `dynamic` 또는 형식 암시적으로 변환할 수 있는 `System.IDisposable`합니다. 경우 형식의 *resource_acquisition* 됩니다 *식* 이 식은 암시적으로 변환할 수 있어야 다음 `System.IDisposable`합니다.

선언 된 지역 변수를 *resource_acquisition* 는 읽기 전용 이며 이니셜라이저를 포함 해야 합니다. 컴파일 타임 오류가 발생 하는 포함된 된 문을 이러한 로컬 변수를 수정 하려고 하는 경우 (할당을 통해 또는 `++` 하 고 `--` 연산자), 그 중 주소 또는으로 전달할 `ref` 또는 `out` 매개 변수.

`using` 문을 세 부분으로 변환: 취득, 사용 및 삭제 합니다. 리소스의 사용량에 암시적으로 포함 되어는 `try` 문을 포함 하는 `finally` 절. 이 `finally` 절 리소스를 삭제 합니다. 경우는 `null` 리소스를 획득 하에 대 한 호출이 다음 `Dispose` 이루어지는 고 예외가 throw 됩니다. 리소스 형식의 경우 `dynamic` 암시적 동적 변환을 통해 동적으로 변환 됩니다 ([암시적 동적 변환을](conversions.md#implicit-dynamic-conversions))를 `IDisposable` 변환 되는지 확인 하기 위해 획득 하는 동안 사용 및 폐기 전에 성공 합니다.

`using` 폼의 문
```csharp
using (ResourceType resource = expression) statement
```
세 가지 가능한 확장 중 하나에 해당 합니다. 때 `ResourceType` 형식이 nullable이 아닌 값은 확장
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

경우에이 고, 그렇지 `ResourceType` nullable 값 형식 또는 참조 형식 이외의 `dynamic`, 확장은
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

경우에이 고, 그렇지 `ResourceType` 는 `dynamic`, 확장은
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

두 확장에는 `resource` 변수가 포함 된 문에서 읽기 전용 및 `d` 변수가에서 액세스할 수 없게 하 고 보이지 않는 포함된 된 문을를 합니다.

동작은 위의 확장과 일치으로 성능상의 이유로, 예: 지정된을 사용 하 여 문을 다르게 구현 구현을 허용 됩니다.

`using` 폼의 문
```csharp
using (expression) statement
```
동일한 세 가지 가능한 확장에 있습니다. 이 경우 `ResourceType` 는 암시적으로의 컴파일 타임 형식은 `expression`하나 포함 된 경우. 그렇지 않으면 인터페이스 `IDisposable` 으로 사용 되는 자체는 `ResourceType`합니다. `resource` 변수가에서 액세스할 수 없게 하 고 보이지 않는 포함된 된 문을를 합니다.

경우는 *resource_acquisition* 형태는 *local_variable_declaration*, 지정 된 형식의 여러 리소스를 가져올 수 합니다. `using` 폼의 문
```csharp
using (ResourceType r1 = e1, r2 = e2, ..., rN = eN) statement
```
시퀀스를 해당 정확 하 게 중첩 되어 `using` 문:
```csharp
using (ResourceType r1 = e1)
    using (ResourceType r2 = e2)
        ...
            using (ResourceType rN = eN)
                statement
```

아래 예제에서는 라는 파일을 만듭니다 `log.txt` 파일을 두 줄 텍스트를 씁니다. 읽기에 대 한 파일을 엽니다 하 고 콘솔에 포함 된 줄의 텍스트를 복사 합니다.
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

있으므로 `TextWriter` 및 `TextReader` 클래스 구현 합니다 `IDisposable` 인터페이스 예제를 사용할 수 `using` 기본 파일이 올바르게 닫히도록 하기 다음 쓰기 또는 읽기 작업 문을 합니다.

## <a name="the-yield-statement"></a>Yield 문

`yield` 문을 사용 하는 반복기 블록에서 ([블록](statements.md#blocks)) 열거자 개체에 값을 생성 하기 위해 ([열거자 개체](classes.md#enumerator-objects)) 또는 열거 가능 개체 ([열거가능한개체](classes.md#enumerable-objects)) 반복기 또는 반복의 끝을 표시 합니다.

```antlr
yield_statement
    : 'yield' 'return' expression ';'
    | 'yield' 'break' ';'
    ;
```

`yield` 예약어; 아닙니다. 이 특별 한 의미가 바로 앞에 사용 하는 경우에을 `return` 또는 `break` 키워드입니다. 다른 컨텍스트에서 `yield` 식별자로 사용할 수 있습니다.

위치에 몇 가지 제한 사항을 `yield` 다음에 설명 된 대로 문을 사용할 수 있습니다.

*  에 대 한 컴파일 시간 오류가 발생 한 `yield` 설명은 (형식 중 하나) 밖에 표시를 *method_body*, *operator_body* 또는 *accessor_body*
*  에 대 한 컴파일 시간 오류를 `yield` 설명은 (형식 중 하나) 익명 함수 내에서 표시 합니다.
*  에 대 한 컴파일 시간 오류가 발생을 `yield` 설명은 (형식 중 하나)에 표시를 `finally` 절을 `try` 문.
*  에 대 한 컴파일 시간 오류를 `yield return` 위치에 나 나타날 문을 `try` 문을 포함 하는 `catch` 절.

다음 예제에서는 유효 하지 않은 사용의 `yield` 문입니다.

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

암시적으로 변환 ([암시적 변환을](conversions.md#implicit-conversions))에서 식의 형식에서 존재 해야 합니다는 `yield return` yield 형식의 문을 ([형식을 생성](classes.md#yield-type)) 반복기의 합니다.

`yield return` 문을 다음과 같이 실행 됩니다.

*  문에 지정 된 식 계산, 암시적으로 yield 형식으로 변환 되어에 할당 된 `Current` 열거자 개체의 속성입니다.
*  반복기 블록의 실행을 일시 중단 됩니다. 경우는 `yield return` 문 내에서 하나 이상의 됩니다 `try` 연결 된 블록 `finally` 지금은 블록이 실행 되지 않습니다.
*  합니다 `MoveNext` 열거자 개체의 메서드 반환 `true` 다음 항목을 지났으면 열거자 개체를 나타내는 해당 호출자에 게 합니다.

열거자 개체의 다음 호출 `MoveNext` 메서드를 마지막으로 일시 중단에서 반복기 블록의 실행을 다시 시작 합니다.

`yield break` 문을 다음과 같이 실행 됩니다.

*  경우는 `yield break` 문을 하나 이상으로 묶입니다 `try` 블록에 연결 `finally` 제어 블록은 처음에 전송 합니다 `finally` 가장 안쪽의 블록 `try` 문. 컨트롤의 끝점에 도달 하는 경우는 `finally` 컨트롤 블록으로 전송 됩니다는 `finally` 다음 바깥쪽 블록 `try` 문. 될 때까지이 프로세스를 반복 합니다 `finally` 모든 바깥쪽 블록 `try` 문이 실행 되었습니다.
*  컨트롤은 반복기 블록의 호출자에 게 반환 됩니다. 이 값은 `MoveNext` 메서드 또는 `Dispose` 열거자 개체의 메서드.

때문에 `yield break` 문을 무조건 제어 전송 다른 곳에서 끝점에는 `yield break` 문에 접근할 수 없습니다.
