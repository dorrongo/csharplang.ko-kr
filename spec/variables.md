# <a name="variables"></a>변수

변수는 저장소 위치를 나타냅니다. 모든 변수가 될 수 있는 값을 결정 하는 형식의 변수에 저장 합니다. C#은 형식이 안전한 언어 및 C# 컴파일러는 값이 변수에 저장 된 항상 적절 한 형식의 보장 합니다. 할당을 통해 또는 사용 하 여 변수 값을 변경할 수 있습니다 합니다 `++` 고 `--` 연산자입니다.

변수 여야 합니다 ***명확 하 게 할당*** ([한정 된 할당](variables.md#definite-assignment)) 전에 해당 값을 가져올 수 있습니다.

변수 중 하나는 다음 섹션에서 설명한 ***처음에 할당*** 또는 ***처음에 할당 되지 않은***합니다. 처음에 할당 된 변수를 잘 정의 된 초기 값 및을 항상 것으로 정적으로 할당 합니다. 처음에 할당 되지 않은 변수가 초기 값 없음. 특정 위치에 정적으로 할당 된 간주 되기 위해 초기에 할당 되지 않은 변수의 변수에 할당 앞에 해당 위치에 모든 가능한 실행 경로에 있어야 합니다.

## <a name="variable-categories"></a>변수 범주

C#-7 범주 변수를 정의 하는 중: 정적 변수, 인스턴스 변수, 배열 요소, 매개 변수 값, 참조 매개 변수, 출력 매개 변수 및 지역 변수입니다. 다음 단원에서는 이러한 각 범주를 설명 합니다.

예제
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
`x` 정적 변수가 `y` 는 인스턴스 변수 `v[0]` 배열 요소는 `a` 값 매개 변수 `b` 참조 매개 변수 `c` 출력 매개 변수 및 `i` 는 지역 변수.

### <a name="static-variables"></a>정적 변수

필드를 사용 하 여 선언 된 `static` 한정자가 호출을 ***정적 변수***. 정적 변수는 정적 생성자를 실행 하기 전에 존재 하 게 제공 됩니다 ([정적 생성자](classes.md#static-constructors)) 포함 하는 형식 및 연결 된 응용 프로그램 도메인 소멸 하는 경우 사라지게에 대 한 합니다.

정적 변수의 초기 값은 기본값 ([기본값](variables.md#default-values)) 변수의 형식입니다.

한정 된 할당 검사를 위해 정적 변수 처음 할당 된 것으로 간주 됩니다.

### <a name="instance-variables"></a>인스턴스 변수

없이 선언 된 필드를 `static` 한정자가 호출 되는 ***인스턴스 변수***.

#### <a name="instance-variables-in-classes"></a>클래스의 인스턴스 변수

클래스의 인스턴스 변수는 해당 클래스의 새 인스턴스를 만들고 해당 인스턴스에 대 한 참조가 없는 및 인스턴스의 소멸자 (있는 경우)가 실행 될 때 소멸 하는 경우 존재 하 게 됩니다.

클래스의 인스턴스 변수의 초기 값은 기본값 ([기본값](variables.md#default-values)) 변수의 형식입니다.

한정 된 할당 검사를 위해 클래스의 인스턴스 변수 처음 할당 된 것으로 간주 됩니다.

#### <a name="instance-variables-in-structs"></a>구조체의 인스턴스 변수

구조체의 인스턴스 변수는 자신이 속한 구조체 변수와 동일한 수명을 정확 하 게에 있습니다. 즉, 경우 구조체 형식의 변수 사라지면 나타나거나 사라집니다, 있으므로 너무 구조체의 인스턴스 변수를 수행 합니다.

초기 할당 상태 구조체의 인스턴스 변수를 포함 하는 구조체 변수의 것 같습니다. 즉, 구조체 변수를 처음으로 간주 됩니다 할당 되므로 너무 해당 인스턴스 변수 이며 구조체 변수는 처음에 할당 되지 않은 것으로 간주 됩니다을 하는 경우 해당 인스턴스 변수 마찬가지로 할당 되지 합니다.

### <a name="array-elements"></a>배열 요소

배열 요소의 배열 인스턴스를 만들 때 존재 하 게 제공 및 배열 인스턴스에 대 한 참조가 없는 경우 중단 합니다.

각 배열 요소의 초기 값은 기본값 ([기본값](variables.md#default-values)) 배열 요소의 형식입니다.

한정 된 할당 검사를 위해 배열 요소 처음 할당 된 것으로 간주 됩니다.

### <a name="value-parameters"></a>값 매개 변수

없이 선언 된 매개 변수를 `ref` 또는 `out` 한정자를 ***값 매개 변수***합니다.

값 매개 변수는 함수 멤버 (메서드, 인스턴스 생성자, 접근자 또는 연산자) 나 익명 함수 호출 시 존재 하 게 제공 하는 매개 변수가 속한 호출에 지정 된 인수의 값으로 초기화 됩니다. 값 매개 변수를 일반적으로 되 면 소멸 익명 함수 또는 함수 멤버를 반환 합니다. 그러나 값 매개 변수는 익명 함수에 의해 캡처된 경우 ([익명 함수 식](expressions.md#anonymous-function-expressions)), 수명이 대리자까지 이상 확장 또는 익명 함수에서 생성 하는 식 트리에 적합 한 가비지 컬렉션입니다.

한정 된 할당 검사를 위해 값 매개 변수를 처음에 할당 된 것으로 간주 됩니다.

### <a name="reference-parameters"></a>참조 매개 변수

사용 하 여 선언 된 매개 변수를 `ref` 한정자가을 ***매개 변수를 참조할***합니다.

참조 매개 변수는 새 저장소 위치를 만들지 않습니다. 대신 참조 매개 변수는 함수 멤버 또는 익명 함수 호출의 인수로 지정 된 변수와 동일한 저장소 위치를 나타냅니다. 따라서 참조 매개 변수의 값은 항상 내부 변수와 동일 합니다.

참조 매개 변수는 다음과 같은 한정 된 할당 규칙이 적용 됩니다. 설명 하는 출력 매개 변수에 대 한 다양 한 규칙을 참고 하십시오 [출력 매개 변수](variables.md#output-parameters)합니다.

*  변수 할당 되어야 합니다 ([한정 된 할당](variables.md#definite-assignment)) 전에 함수 멤버 또는 대리자 호출에서 참조 매개 변수로 전달할 수 있습니다.
*  함수 멤버 또는 익명 함수 내에서 처음에 할당 하는 참조 매개 변수 간주 됩니다.

인스턴스 메서드 또는 인스턴스 접근자 구조체 형식 내에서 `this` 키워드는 구조체 형식의 참조 매개 변수로 정확 하 게 작동 합니다 ([이 액세스](expressions.md#this-access)).

### <a name="output-parameters"></a>출력 매개 변수

사용 하 여 선언 된 매개 변수를 `out` 한정자가는 ***출력 매개 변수***합니다.

출력 매개 변수는 새 저장소 위치를 만들지 않습니다. 대신, 출력 매개 변수는 함수 멤버 또는 대리자 호출의 인수로 지정 된 변수와 동일한 저장소 위치를 나타냅니다. 따라서 출력 매개 변수의 값은 항상 내부 변수와 동일 합니다.

출력 매개 변수는 다음과 같은 한정 된 할당 규칙이 적용 됩니다. 설명 하는 참조 매개 변수에 대 한 다양 한 규칙을 참고 하십시오 [매개 변수를 참조할](variables.md#reference-parameters)합니다.

*  변수를 필요 하지 명확 하 게 할당 대리자 호출 또는 함수 멤버의 출력 매개 변수로 전달할 수 있습니다.
*  함수 멤버 또는 대리자 호출의 정상적인 완료를 다음 출력 매개 변수를 사용 하는 것으로 간주 하는 대로 전달 된 각 변수에 실행 경로에 할당 합니다.
*  함수 멤버 또는 익명 함수 내에서 출력 매개 변수는 처음에 할당 되지 않은 간주 됩니다.
*  익명 함수 또는 함수 멤버의 모든 출력 매개 변수 할당 되어야 합니다 ([한정 된 할당](variables.md#definite-assignment)) 함수 앞 멤버 또는 익명 함수 정상적으로 반환 합니다.

구조체 형식의 인스턴스 생성자 내에서 `this` 키워드는 구조체 형식의 출력 매개 변수로 정확 하 게 작동 합니다 ([이 액세스](expressions.md#this-access)).

### <a name="local-variables"></a>지역 변수

A ***지역 변수*** 사용 하 여 선언를 *local_variable_declaration*에서 발생할 수 있는 *블록*, *for_statement*을 *switch_statement* 또는 *using_statement*; 또는 *foreach_statement* 또는 *specific_catch_clause* 는에대한*try_statement*합니다.

지역 변수의 수명은는 저장소에 대 한 예약 되도록 보장 하는 프로그램 실행의 일부입니다. 이 수명에 대 한 항목에서 적어도 확장 합니다 *블록*, *for_statement*를 *switch_statement*, *using_statement*, *foreach_statement*, 또는 *specific_catch_clause* 에 연결 하는 실행 될 때까지 *블록*, *for_statement*, *switch_statement*를 *using_statement*하십시오 *foreach_statement*, 또는 *specific_catch_clause* 어떤 방식으로 끝납니다. (입력는 괄호로 묶인 *블록* 일시 중단 하지만 현재 실행 종료 하지 않습니다 메서드를 호출 하거나 *블록*, *for_statement*, *switch_statement* 하십시오 *using_statement*를 *foreach_statement*, 또는 *specific_catch_clause*.) 지역 변수는 익명 함수에 의해 캡처된 경우 ([외부 변수를 캡처할](expressions.md#captured-outer-variables)), 수명 기간 동안 대리자 또는 식 트리를 제공 하는 다른 개체와 함께 익명 함수에서 생성 될 때까지 적어도 확장 캡처된 변수 참조, 가비지 수집에 적합 합니다.

경우 부모 *블록*, *for_statement*, *switch_statement*하십시오 *using_statement*, *foreach_statement*, 또는 *specific_catch_clause* 입력 재귀적으로 지역 변수의 새 인스턴스를 매번 만들어집니다 및 해당 *local_variable_initializer*있는 평가 되는 경우, 각 시간입니다.

도입 된 지역 변수를 *local_variable_declaration* 자동으로 초기화 되지 않으며 따라서 기본값은 없습니다. 한정 된 할당 검사를 위해에서 도입 된 지역 변수를 *local_variable_declaration* 처음에 할당 되지 않은 것으로 간주 됩니다. A *local_variable_declaration* 포함 될 수 있습니다는 *local_variable_initializer*, 경우 변수는 정적으로 할당 초기화 식은 한 후에 ([ 선언문](variables.md#declaration-statements)).

도입 된 지역 변수의 범위를 *local_variable_declaration*, 해당 지역 변수 앞에 오는 텍스트 위치를 가리키도록 하면 컴파일 타임 오류가 발생 해당 *local_variable_declarator*. 지역 변수 선언 암시적 경우 ([지역 변수 선언](statements.md#local-variable-declarations)), 내 변수를 참조 하면 오류가 발생 이기도 해당 *local_variable_declarator*합니다.

도입 된 지역 변수를 *foreach_statement* 또는 *specific_catch_clause* 전체 범위 내에서 정적으로 할당 된 간주 됩니다.

지역 변수의 실제 수명은 구현에 따라 다릅니다. 예를 들어, 컴파일러는 블록의 지역 변수에 해당 블록의 작은 부분에만 사용 됨을 경우가 정적으로 합니다. 이 분석을 사용 하 여 컴파일러 변수 저장소 포함 블록 보다 짧은 수명 것에서 발생 하는 코드를 생성할 수 있습니다.

저장소 지역 참조 변수에서 참조 하는 로컬 참조 변수의 수명은 독립적으로 회수 ([자동 메모리 관리](basic-concepts.md#automatic-memory-management)).

## <a name="default-values"></a>기본값

다음과 같은 범주의 변수는 기본값으로 자동으로 초기화 됩니다.

*  정적 변수
*  클래스 인스턴스의 인스턴스 변수입니다.
*  배열 요소입니다.

변수의 기본값 변수의 형식에 따라 달라 집니다 하 고 다음과 같이 결정 됩니다.

*  변수에 대 한는 *value_type*, 기본값은 하 여 계산 된 값과 동일 합니다 *value_type*의 기본 생성자 ([기본 생성자](types.md#default-constructors)).
*  변수를 *reference_type*, 기본값은 `null`합니다.

Memory manager 함으로써 기본값으로 초기화는 일반적으로 수행 하거나 가비지 수집기 사용에 대 한 할당 하기 전에 모든 비트가 0 인 메모리를 초기화 합니다. Null 참조를 나타내는 모든 비트가 0을 사용 하는 것이 유용 합니다.

## <a name="definite-assignment"></a>한정 된 할당

지정 된 위치에서 실행 코드에 함수 멤버 변수를 라고 ***명확 하 게 할당*** 특정 정적 흐름 분석을 통해 경우 컴파일러가 입증할 수 있습니다 ([한정 된 결정 하는 것에 대 한 정확한 규칙 할당](variables.md#precise-rules-for-determining-definite-assignment)), 변수에 자동으로 초기화 하거나 하나 이상 할당 되었습니다. 한정 된 할당의 규칙은 비공식적으로 언급 합니다.

*  처음에 할당된 된 변수 ([처음에 할당 되는 변수](variables.md#initially-assigned-variables))는 항상 정적으로 할당 합니다.
*  처음에 할당 되지 않은 변수 ([나중에 변수를 할당](variables.md#initially-unassigned-variables)) 것으로 간주 됩니다 정적으로 할당 된 지정된 된 위치에서 해당 위치에 선행 하는 모든 가능한 실행 경로 중 하나 이상 포함 하는 경우:
    * 단순 할당 ([단순 할당](expressions.md#simple-assignment)) 변수 된 왼쪽된 피연산자.
    * 호출 식 ([호출 식](expressions.md#invocation-expressions)) 또는 개체 생성 식 ([개체 만들기 식](expressions.md#object-creation-expressions)) 출력 매개 변수로 변수를 전달 하는 합니다.
    * 지역 변수, 지역 변수 선언 ([지역 변수 선언](statements.md#local-variable-declarations)) 변수 이니셜라이저에서 예외를 포함 하는 합니다.

위의 비공식 규칙 내부 공식 사양에 설명 되어 [처음에 변수를 할당](variables.md#initially-assigned-variables)를 [나중에 변수를 할당](variables.md#initially-unassigned-variables), 및 [결정 하는 것에 대 한 정확한 규칙 한정 된 할당](variables.md#precise-rules-for-determining-definite-assignment)합니다.

인스턴스 변수의 한정 된 할당 상태를 *struct_type* 변수 개별적으로 집합적으로 추적 됩니다. 위의 규칙 이외에 다음 규칙에 적용 *struct_type* 변수 및 해당 인스턴스 변수:

*  인스턴스 변수는 정적으로 할당 하는 경우 포함 *struct_type* 변수 정적으로 할당 된 것으로 간주 됩니다.
*  A *struct_type* 각 해당 인스턴스 변수는 정적으로 할당 하는 경우 변수를 정적으로 할당 된 간주 됩니다.

한정 된 할당은 다음 경우에 요구 사항:

*  변수를 가져온 위치 값을 해당 하는 각 위치에서 확실 하 게 할당 되어야 합니다. 이 정의 되지 않은 값 되지 수행 되도록 합니다. 식에서 변수 발생 경우를 제외 하 고 변수 값을 가져올 것으로 간주 됩니다.
    * 변수는 단순 할당의 왼쪽된 피연산자
    * 변수는 output 매개 변수로 전달 됩니다 또는
    * 변수를 *struct_type* 변수 멤버 액세스의 경우 왼쪽된 피연산자와 발생 합니다.
*  변수는 참조 매개 변수로 전달 되는 각 위치에서 확실 하 게 할당 되어야 합니다. 이렇게 하면 호출 되는 함수 멤버가 처음에 할당 하는 참조 매개 변수를 고려할 수 있습니다.
*  함수 멤버의 모든 출력 매개 변수는 함수 멤버를 반환 하는 각 위치에 할당 되어야 합니다 (통해를 `return` 문 또는 멤버 함수 본문의 끝에 도달 하는 실행을 통해). 이렇게 하면는 함수 멤버 값을 반환 하지 정의 되지 않은 출력 매개 변수를 컴파일러에서 해당 변수에 할당 하는 출력 매개 변수로 변수를 사용 하는 함수 멤버 호출을 사용할 수 있게 합니다.
*  합니다 `this` 변수를 *struct_type* 인스턴스 생성자는 해당 인스턴스 생성자를 반환 하는 각 위치에 할당 되어야 합니다.

### <a name="initially-assigned-variables"></a>처음에 할당된 되는 변수

변수는 다음과 같은 범주의 처음으로 할당 된 분류 됩니다.

*  정적 변수
*  클래스 인스턴스의 인스턴스 변수입니다.
*  처음에 할당 된 구조체 변수의 인스턴스 변수입니다.
*  배열 요소입니다.
*  값 매개 변수입니다.
*  참조 매개 변수입니다.
*  에 선언 된 변수를 `catch` 절 또는 `foreach` 문입니다.

### <a name="initially-unassigned-variables"></a>처음에 할당 되지 않은 변수

다음과 같은 범주의 변수 할당 되지 않은 처음으로 분류 됩니다.

*  처음에 할당 되지 않은 구조체 변수의 인스턴스 변수입니다.
*  출력 매개 변수를 포함 하는 `this` 구조체 인스턴스 생성자의 변수입니다.
*  에 선언 된 지역 변수를 제외 된 `catch` 절 또는 `foreach` 문입니다.

### <a name="precise-rules-for-determining-definite-assignment"></a>한정 된 할당을 확인 하는 것에 대 한 정확한 규칙

사용 되는 각 변수 확실 하 게 할당 되어 있는지를 확인 하기 위해 컴파일러는이 섹션에 설명 된 것에 해당 하는 프로세스를 사용 해야 합니다.

컴파일러는 처음에 할당 되지 않은 변수를 하나 이상 있는 각 함수 멤버의 본문을 처리 합니다. 처음에 할당 되지 않은 각 변수에 대해 *v*, 컴파일러가 결정을 ***한정 된 할당 상태*** 에 대 한 *v* 각 함수 멤버의 다음 항목에서:

*  각 명령문의 시작 부분
*  끝점 ([끝점 및 연결 가능성](statements.md#end-points-and-reachability)) 각 문의
*  각 호에는 제어가 다른 문 또는 문의 끝 지점
*  각 식의 시작 부분
*  각 식의 끝

한정 된 할당 상태의 *v* 일 수 있습니다.

*  정적으로 할당 합니다. 이 시점에 있는 모든 가능한 제어 흐름에서 되었음을 *v* 값이 할당 되었습니다.
*  확실 하 게 할당 되지 않습니다. 형식 식의 끝에 변수의 상태에 대 한 `bool`, 월을 명확 하 게 할당 되지 않습니다 (하지만 반드시)는 변수의 상태는 다음과 같은 하위 상태 중 하나에 속합니다.
    * True 식 뒤 할당합니다. 이 상태는 나타냅니다 *v* 부울 식이 true로 평가 이지만 부울 식이 false로 평가 하는 경우를 반드시 할당 되지 않은 경우 정적으로 할당 됩니다.
    * False 식 뒤 할당합니다. 이 상태는 나타냅니다 *v* 부울 식이 false로 계산 되지만 부울 식이 true로 평가 하는 경우를 반드시 할당 되지 않은 경우 정적으로 할당 됩니다.

다음 규칙에 따라 방법을 변수의 상태 *v* 각 위치에서 결정 됩니다.

#### <a name="general-rules-for-statements"></a>문에 대 한 일반 규칙

*  *v* 멤버 함수 본문의 시작 부분에서 확실 하 게 할당 되지 않습니다.
*  *v* 접근할 수 없는 문의 시작 부분에 정적으로 할당 됩니다.
*  한정 된 할당 상태의 *v* 다른 명령문의 시작 부분에 한정 된 할당 상태를 확인 하 여 결정 됩니다 *v* 의 시작 부분을 대상으로 하는 모든 제어 흐름 전송 문입니다. 경우 (및 경우에) *v* 그런 다음 이러한 모든 제어 흐름 전송 할당 확실 하 게 됩니다 *v* 문의 시작 부분에 정적으로 할당 됩니다. 동일한 방식으로 문을 연결 가능성을 확인 가능한 제어 흐름 전송 집합이 결정 됩니다 ([끝점 및 연결 가능성](statements.md#end-points-and-reachability)).
*  한정 된 할당 상태 *v* 블록의 끝 시점 `checked`, `unchecked`, `if`, `while`, `do`, `for`, `foreach`, `lock`, `using`, 또는 `switch` 문에 한정 된 할당 상태를 확인 하 여 결정 됩니다 *v* 문의의 끝점을 대상으로 하는 모든 제어 흐름 전송 합니다. 하는 경우 *v* 그런 다음 이러한 모든 제어 흐름 전송 할당 확실 하 게 됩니다 *v* 문의 끝점에서 정적으로 할당 됩니다. 그렇지 않으면; *v* 문의 끝에서 확실 하 게 할당 되지 않습니다. 동일한 방식으로 문을 연결 가능성을 확인 가능한 제어 흐름 전송 집합이 결정 됩니다 ([끝점 및 연결 가능성](statements.md#end-points-and-reachability)).

#### <a name="block-statements-checked-and-unchecked-statements"></a>문 블록 옵션을 선택 및 unchecked 문

한정 된 할당 상태의 *v* 컨트롤 블록에서 문 목록의 첫 번째 문 (또는 문 목록이 비어 있으면 블록의 끝 지점) 전송이 한정 된 할당에 대 한 설명은 동일*v* 블록을 앞 `checked`, 또는 `unchecked` 문입니다.

#### <a name="expression-statements"></a>식 문

식 문에 대 한 *stmt* 식으로 이루어진 *expr*:

*  *v* 맨 앞에 한정 된 할당 상태가 동일한 *expr* 의 시작 부분으로 *stmt*합니다.
*  하는 경우 *v* 끝에 한 정적으로 할당 하는 경우 *expr*의 끝점에서 정적으로 할당 됩니다 *stmt*그렇지 의끝점에서확실하게할당되지않은*stmt*합니다.

#### <a name="declaration-statements"></a>선언문

*  하는 경우 *stmt* 다음 이니셜라이저 없이 선언 문 *v* 의 끝점에서 동일한 한정 된 할당 상태가 *stmt* 의시작부분으로*stmt*합니다.
*  하는 경우 *stmt* 는 이니셜라이저를 사용 하 여 선언 문 다음에 대 한 한정 된 할당 상태 *v* 도달한 처럼 *stmt* 문 목록 하나 할당 된 (선언) 순서 대로 이니셜라이저를 사용 하 여 각 선언에 대 한 문입니다.

#### <a name="if-statements"></a>경우 문

에 `if` 문 *stmt* 형식:
```csharp
if ( expr ) then_stmt else else_stmt
```

*  *v* 맨 앞에 한정 된 할당 상태가 동일한 *expr* 의 시작 부분으로 *stmt*합니다.
*  경우 *v* 끝에 정적으로 할당 됩니다 *expr*, 제어 흐름 전송에서 확실 하 게 할당 한 다음 *then_stmt* 및를 *else_stmt*  또는 끝점의 *stmt* 없습니다 else 절이 있는 경우.
*  경우 *v* 끝에 "true 식 뒤 확실 하 게 할당 된" 상태를 갖습니까 *expr*, 제어 흐름 전송에서 확실 하 게 할당 한 다음 *then_stmt*, 아니라 제어 흐름 전송 중 하나에서 정적으로 할당 된 *else_stmt* 또는 끝점의 *stmt* 없습니다 else 절이 있는 경우.
*  경우 *v* 끝에 "정적 false 식으로 할당" 상태를 갖습니까 *expr*, 제어 흐름 전송에서 확실 하 게 할당 한 다음 *else_stmt*, 아니라 제어 흐름 전송에 할당 *then_stmt*합니다. 끝점의 정적으로 할당 됩니다 *stmt* 끝점의 확실 하 게 할당 하는 경우에 *then_stmt*합니다.
*  이 고, 그렇지 *v* 확실 하 게 할당 하거나 제어 흐름 전송의 비율은 합니다 *then_stmt* 또는 *else_stmt*, 또는 끝점의  *stmt* 없습니다 else 절이 있는 경우.

#### <a name="switch-statements"></a>Switch 문

에 `switch` 문 *stmt* 제어 식을 사용 하 여 *expr*:

*  한정 된 할당 상태 *v* 부분 *expr* 의 상태와 같습니다 *v* 맨 앞에 *stmt*합니다.
*  한정 된 할당 상태의 *v* 제어 흐름에 연결할 수 있는 스위치 블록 문 목록에 전송할 같습니다의 한정 된 할당 상태 *v* 끝날 때 *expr*.

#### <a name="while-statements"></a>While 문

에 `while` 문 *stmt* 폼의:
```csharp
while ( expr ) while_body
```

*  *v* 맨 앞에 한정 된 할당 상태가 동일한 *expr* 의 시작 부분으로 *stmt*합니다.
*  하는 경우 *v* 끝에 정적으로 할당 됩니다 *expr*, 제어 흐름 전송에서 확실 하 게 할당 한 다음 *while_body* 를 끝점에  *stmt*합니다.
*  하는 경우 *v* 끝에 "true 식 뒤 확실 하 게 할당 된" 상태를 갖습니까 *expr*, 제어 흐름 전송에 정적으로 할당은 다음 *while_body*, 있지만 끝점의 할당 *stmt*합니다.
*  하는 경우 *v* 끝에 "정적 false 식으로 할당" 상태를 갖습니까 *expr*, 확실 하 게 제어 흐름 전송의 끝점에 할당 한 다음 *stmt* 있지만 제어 흐름 전송에서 확실 하 게 할당 되지 않음 *while_body*합니다.

#### <a name="do-statements"></a>문을 수행 합니다.

에 `do` 문 *stmt* 폼의:
```csharp
do do_body while ( expr ) ;
```

*  *v* 제어 흐름 전송의 처음부터 같은 한정 된 할당 상태를 갖습니까 *stmt* 하 *do_body* 의 시작 부분으로 *stmt*합니다.
*  *v* 맨 앞에 한정 된 할당 상태가 동일한 *expr* 끝점와 마찬가지로 *do_body*합니다.
*  하는 경우 *v* 끝에 정적으로 할당 됩니다 *expr*, 확실 하 게 제어 흐름 전송의 끝점에 할당 한 다음 *stmt*합니다.
*  하는 경우 *v* 끝에 "정적 false 식으로 할당" 상태를 갖습니까 *expr*, 확실 하 게 제어 흐름 전송의 끝점에 할당 한 다음 *stmt* .

#### <a name="for-statements"></a>문에 대 한

한정 된 할당에 대 한 검사는 `for` 폼의 문:
```csharp
for ( for_initializer ; for_condition ; for_iterator ) embedded_statement
```
문을 작성 된 것 처럼 수행 됩니다.
```csharp
{
for_initializer ;
while ( for_condition ) {
embedded_statement ;
for_iterator ;
}
}
```

경우는 *for_condition* 에서 생략 되는 `for` 문을 다음 진행 한정 된 할당의 평가 처럼 *for_condition* 대체 됨 `true` 위의 확장 .

#### <a name="break-continue-and-goto-statements"></a>중단, 계속 및 goto 문

한정 된 할당 상태 *v* 인해 제어 흐름 전송에는 `break`, `continue`, 또는 `goto` 문을의 한정 된 할당 상태와 같습니다 *v* 에 문의 시작 합니다.

#### <a name="throw-statements"></a>Throw 문

문에 대 한 *stmt* 형식의
```csharp
throw expr ;
```

한정 된 할당 상태의 *v* 부분 *expr* 의 한정 된 할당 상태와 같습니다 *v* 맨 앞에 *stmt*.

#### <a name="return-statements"></a>Return 문

문에 대 한 *stmt* 형식의
```csharp
return expr ;
```

*  한정 된 할당 상태의 *v* 부분 *expr* 의 한정 된 할당 상태와 같습니다 *v* 맨 앞에 *stmt*.
*  하는 경우 *v* 확실 하 게 할당 해야 하거나 출력 매개 변수를가 합니다.
    * 후 *expr*
    * 또는 끝에 `finally` 블록을 `try` - `finally` 또는 `try` - `catch` - `finally` 포함 하는 `return` 문입니다.

폼의 문 stmt에 대 한:
```csharp
return ;
```

*  하는 경우 *v* 확실 하 게 할당 해야 하거나 출력 매개 변수를가 합니다.
    * 전에 *stmt*
    * 또는 끝에 `finally` 블록을 `try` - `finally` 또는 `try` - `catch` - `finally` 포함 하는 `return` 문입니다.

#### <a name="try-catch-statements"></a>Try / catch 문

문에 대 한 *stmt* 형식:
```csharp
try try_block
catch(...) catch_block_1
...
catch(...) catch_block_n
```

*  한정 된 할당 상태의 *v* 부분 *try_block* 의 한정 된 할당 상태와 같습니다 *v* 맨 앞에 *stmt*.
*  한정 된 할당 상태 *v* 부분 *catch_block_i* (에 대 한 *합니까*)의 한정 된 할당 상태와 같습니다 *v*의 시작 부분 *stmt*합니다.
*  한정 된 할당 상태의 *v* 끝점의 *stmt* 정적으로 할당 된 경우 (및 경우에만)은 *v* 끝점의 확실 하 게 할당 된  *try_block* 매 *catch_block_i* (에 대 한 모든 *합니까* 1 ~ *n*).

#### <a name="try-finally-statements"></a>Try finally 문

에 `try` 문 *stmt* 폼의:
```csharp
try try_block finally finally_block
```

*  한정 된 할당 상태의 *v* 부분 *try_block* 의 한정 된 할당 상태와 같습니다 *v* 맨 앞에 *stmt*.
*  한정 된 할당 상태의 *v* 부분 *finally_block* 한정 된 할당 상태와 같습니다 *v* 맨 앞에 *stmt* .
*  한정 된 할당 상태의 *v* 끝점의 *stmt* 정적으로 할당 된 경우 (및 경우에만)는 다음 중 하나 이상:
    * *v* 끝점의 확실 하 게 할당 된 *try_block*
    * *v* 끝점의 확실 하 게 할당 된 *finally_block*

경우 제어 흐름 전송 (예를 들어를 `goto` 문)는 만들어질 내에서 시작 *try_block*, 외부 종료 *try_block*, 한 다음 *v* 이기도 경우에 제어 흐름 전송을 정적으로 할당 된 것으로 간주 *v* 끝점의 정적으로 할당 됩니다 *finally_block*합니다. (경우에만 아닙니다.-하는 경우 *v* 는 정적으로 할당 된 비율은이 제어 흐름 전송에서 다른 이유로 확실 하 게 할당 합니다.)

#### <a name="try-catch-finally-statements"></a>Try – catch – finally 문

에 대 한 한정 된 할당 분석을 `try` - `catch` - `finally` 폼의 문:
```csharp
try try_block
catch(...) catch_block_1
...
catch(...) catch_block_n
finally *finally_block*
```
문 처럼 수행 됩니다는 `try` - `finally` 문 바깥쪽을 `try` - `catch` 문:
```csharp
try {
try try_block
catch(...) catch_block_1
...
catch(...) catch_block_n
}
finally finally_block
```

다음 예제에서는 어떻게 다른 블록을를 `try` 문 ([try 문](statements.md#the-try-statement)) 한정 된 할당에 영향을 줍니다.
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

#### <a name="foreach-statements"></a>Foreach 문

에 `foreach` 문 *stmt* 폼의:
```csharp
foreach ( type identifier in expr ) embedded_statement
```

*  한정 된 할당 상태 *v* 부분 *expr* 의 상태와 같습니다 *v* 맨 앞에 *stmt*합니다.
*  한정 된 할당 상태의 *v* 제어 흐름 전송의 *embedded_statement* 또는 끝점 *stmt* 의 상태와 같습니다 *v* 끝날 때 *expr*합니다.

#### <a name="using-statements"></a>문을 사용 하 여

에 `using` 문 *stmt* 폼의:
```csharp
using ( resource_acquisition ) embedded_statement
```

*  한정 된 할당 상태의 *v* 부분 *resource_acquisition* 의 상태와 같습니다 *v* 맨 앞에 *stmt*.
*  한정 된 할당 상태의 *v* 제어 흐름 전송의 *embedded_statement* 의 상태와 동일 *v* 끝에 *resource_ 취득*합니다.

#### <a name="lock-statements"></a>Lock 문

에 `lock` 문 *stmt* 폼의:
```csharp
lock ( expr ) embedded_statement
```

*  한정 된 할당 상태 *v* 부분 *expr* 의 상태와 같습니다 *v* 맨 앞에 *stmt*합니다.
*  한정 된 할당 상태의 *v* 제어 흐름 전송의 *embedded_statement* 의 상태와 동일 *v* 끝에 *expr*.

#### <a name="yield-statements"></a>Yield 문

에 `yield return` 문 *stmt* 폼의:
```csharp
yield return expr ;
```

*  한정 된 할당 상태 *v* 부분 *expr* 의 상태와 같습니다 *v* 맨 앞에 *stmt*합니다.
*  한정 된 할당 상태의 *v* 끝 *stmt* 의 상태와 같습니다 *v* 끝에 *expr*합니다.
*  `yield break` 문에 한정 된 할당 상태에 영향을 주지 않습니다.

#### <a name="general-rules-for-simple-expressions"></a>간단한 식에 대 한 일반 규칙

이러한 종류의 식이 다음 규칙이 적용: 리터럴 ([리터럴](expressions.md#literals)), 단순한 이름 ([단순 이름](expressions.md#simple-names)), 멤버 액세스 식 ([멤버 액세스](expressions.md#member-access)), 인덱싱되지 않은 기본 액세스 식 ([액세스를 기본](expressions.md#base-access)), `typeof` 식 ([typeof 연산자](expressions.md#the-typeof-operator)), 기본값 식 ([기본 값 식 ](expressions.md#default-value-expressions)) 및 `nameof` 식 ([Nameof 식](expressions.md#nameof-expressions)).

*  한정 된 할당 상태의 *v* 식의 끝에 한정 된 할당 상태와 같습니다 *v* 식의 시작 부분에 있습니다.

#### <a name="general-rules-for-expressions-with-embedded-expressions"></a>포함 된 식 사용 하 여 식에 대 한 일반 규칙

이러한 종류의 식에는 다음 규칙이 적용 됩니다: 괄호로 묶인 식 ([괄호로 묶인 식](expressions.md#parenthesized-expressions)), 요소 액세스 식을 ([요소 액세스](expressions.md#element-access)) 기본 식을 사용 하 여 액세스 인덱싱 ([액세스를 기본](expressions.md#base-access)), 증가 및 감소 식은 ([후 위 증가 및 감소 연산자](expressions.md#postfix-increment-and-decrement-operators), [전위 증가 및 감소 연산자](expressions.md#prefix-increment-and-decrement-operators)), 캐스트 식 ([캐스트 식](expressions.md#cast-expressions)), 단항 `+`, `-`, `~`합니다 `*` 이진 식 `+`, `-`, `*`, `/`, `%`, `<<`, `>>`, `<`, `<=`, `>`, `>=`, `==`, `!=`, `is`, `as`, `&`, `|`, `^` 식 ([산술 연산자](expressions.md#arithmetic-operators)하십시오 [시프트 연산자](expressions.md#shift-operators), [관계형 및 형식 테스트 연산자](expressions.md#relational-and-type-testing-operators) 를 [논리 연산자](expressions.md#logical-operators)), 복합 대입 식 ([복합 할당](expressions.md#compound-assignment)), `checked` 하 고 `unchecked` 식 ([checked 및 unchecked 연산자](expressions.md#the-checked-and-unchecked-operators)), 배열 및 대리자 생성 식 더하기 ([new 연산자](expressions.md#the-new-operator)).

이러한 식의 각 고정 된 순서로 무조건 평가 되는 하나 이상의 하위 식에 있습니다. 예를 들어 이진 `%` 연산자의 왼쪽을 오른쪽 연산자를 평가 합니다. 인덱싱 작업 인덱싱된 식을 계산 하 고 인덱스 식의 왼쪽에서 오른쪽 순서로 각각를 평가 합니다. 식에 대 한 *expr*에 하위 식이 *(e1, e2,..., eN*, 지정 된 순서로 평가:

*  한정 된 할당 상태의 *v* 부분 *e1* 맨 앞에 한정 된 할당 상태와 같습니다 *expr*합니다.
*  한정 된 할당 상태 *v* 부분 *ei* (*i* 1 보다 큰) 이전 하위 식의 끝에 한정 된 할당 상태와 같습니다.
*  한정 된 할당 상태의 *v* 끝 *expr* 끝에 한정 된 할당 상태와 같습니다 *eN*

#### <a name="invocation-expressions-and-object-creation-expressions"></a>호출 식 및 개체 만들기

호출 식에 대 한 *expr* 형식:
```csharp
primary_expression ( arg1 , arg2 , ... , argN )
```
또는 개체 만들기 식 형식입니다.
```csharp
new type ( arg1 , arg2 , ... , argN )
```

*  호출 식의 한정 된 할당 상태에 대 한 *v* 하기 전에 *primary_expression* 상태의 동일 *v* 전에 *expr*.
*  호출 식의 한정 된 할당 상태에 대 한 *v* 하기 전에 *arg1* 상태의 동일 *v* 후 *primary_expression*.
*  개체 생성 식의 한정 된 할당 상태에 대 한 *v* 하기 전에 *arg1* 상태의 동일 *v* 전에 *expr*합니다.
*  각 인수에 대 한 *argi*에 한정 된 할당 상태 *v* 후 *argi* 무시 하 고 일반 식 규칙에 의해 결정 됩니다 `ref` 또는`out`한정자입니다.
*  각 인수에 대 한 *argi* 에 대 한 *합니까* 한정 된 할당 상태를 1 보다 큰 *v* 앞 *argi* 의 상태와 동일 *v* 이전 *arg*합니다.
*  경우 변수 *v* 로 전달 되는 `out` 인수 (즉, 폼의 인수 `out v`) 인수는 다음 상태 중 하나에서 *v* 후 *expr* 할당 됩니다. 그렇지 않으면; 상태의 *v* 한 후 *expr* 의 상태와 동일 *v* 후 *argN*합니다.
*  배열 이니셜라이저에 대 한 ([배열 만들기 식을](expressions.md#array-creation-expressions)), 개체 이니셜라이저 ([개체 이니셜라이저](expressions.md#object-initializers)), 컬렉션 이니셜라이저 ([컬렉션 이니셜라이저](expressions.md#collection-initializers)) 및 익명 개체 이니셜라이저 ([익명 개체 생성 식을](expressions.md#anonymous-object-creation-expressions))에 한정 된 할당 상태는 이러한 구문의 측면에서 정의 된 확장에 의해 결정 됩니다.

#### <a name="simple-assignment-expressions"></a>단순 할당 식

식에 대 한 *expr* 양식의 `w = expr_rhs`:

*  한정 된 할당 상태의 *v* 하기 전에 *expr_rhs* 한정 된 할당 상태와 동일 *v* 전에 *expr*합니다.
*  한정 된 할당 상태의 *v* 한 후 *expr* 에 의해 결정 됩니다.
   * 하는 경우 *w* 으로 동일한 변수가 *v*, 한정 된 할당 상태 *v* 후 *expr* 정적으로 할당 됩니다.
   * 할당 하는 경우 구조체 형식의 인스턴스 생성자 내에서 발생 하는 경우 그러지 *w* 가 자동으로 구현 된 속성을 지정 합니다. 속성 액세스 *P* 생성 되는 인스턴스에서 및 *v* 의 숨겨진된 지원 필드는 *P*에 한정 된 할당 상태 *v* 후 *expr* 확실히 할당 합니다.
   * 이 고, 그렇지 한정 된 할당 상태의 *v* 한 후 *expr* 한정 된 할당 상태와 같습니다 *v* 후 *expr_rhs*합니다.

#### <a name="-conditional-and-expressions"></a>& & (AND 조건부) 식

식에 대 한 *expr* 양식의 `expr_first && expr_second`:

*  한정 된 할당 상태의 *v* 하기 전에 *expr_first* 한정 된 할당 상태와 동일 *v* 전에 *expr*합니다.
*  한정 된 할당 상태의 *v* 하기 전에 *expr_second* 경우 확실 하 게 할당 된 상태의 *v* 후 *expr_first* 는 정적으로 할당 또는 "정적으로 할당 된 true 식 뒤"입니다. 그렇지 않으면 할당 되지 않은 확실 하 게 합니다.
*  한정 된 할당 상태의 *v* 한 후 *expr* 에 의해 결정 됩니다.
    * 하는 경우 *expr_first* 는 값을 사용 하 여 상수 식 `false`, 한정 된 할당 상태 *v* 후 *expr* 한정 된 할당와 동일 상태 *v* 한 후 *expr_first*합니다.
    * 그렇지 않은 경우, 상태 *v* 후 *expr_first* 확실 하 게 할당 되 면 다음 상태의 *v* 후 *expr* 정적으로 할당 됩니다.
    * 그렇지 않은 경우, 상태 *v* 후 *expr_second* 확실 하 게 할당 된 및 상태의 *v* 후 *expr_first* 확실히 " false 식 "을 할당 한 다음 상태의 *v* 한 후 *expr* 정적으로 할당 됩니다.
    * 그렇지 않은 경우, 상태 *v* 후 *expr_second* 정적으로 할당 하거나 "정적으로 할당 된 true 식 뒤"에 다음 상태의 *v* 후  *expr* "확실 하 게 할당 된 true 식 뒤"입니다.
    * 그렇지 않은 경우, 상태 *v* 한 후 *expr_first* "정적으로 할당 된 후 false 식", 및의 상태는 *v* 후 *expr_second* 가 "대입할 false 식 뒤" 상태의 *v* 한 후 *expr* "확실 하 게 할당 된 후 false 식"입니다.
    * 이 고, 그렇지 상태의 *v* 한 후 *expr* 확실 하 게 할당 되지 않습니다.

예제
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
변수의 `i` 의 포함 된 문 중 하나에서 정적으로 할당 된 것으로 간주 됩니다는 `if` 문이 아니라 다른 합니다. `if` 메서드의 문은 `F`, 변수의 `i` 때문에 포함 된 첫 번째 문에서 확실 하 게 할당 되었습니다 식 실행 `(i = y)` 앞에 항상이 포함 된 문 실행 합니다. 반대로, 변수의 `i` 할당 되지 않은 확실 하 게 두 번째는 포함 된 문에서 이후에 `x >= 0` 수 테스트 false, 변수에 결과 `i` 할당 되지 않은 합니다.

#### <a name="-conditional-or-expressions"></a>|| (조건부 OR) 식

식에 대 한 *expr* 양식의 `expr_first || expr_second`:

*  한정 된 할당 상태의 *v* 하기 전에 *expr_first* 한정 된 할당 상태와 동일 *v* 전에 *expr*합니다.
*  한정 된 할당 상태의 *v* 하기 전에 *expr_second* 경우 확실 하 게 할당 된 상태의 *v* 후 *expr_first* 는 정적으로 할당 또는 "정적으로 할당 된 후 false 식"입니다. 그렇지 않으면 할당 되지 않은 확실 하 게 합니다.
*  한정 된 할당 설명이 *v* 한 후 *expr* 에 의해 결정 됩니다.
    * 하는 경우 *expr_first* 는 값을 사용 하 여 상수 식 `true`, 한정 된 할당 상태 *v* 후 *expr* 한정 된 할당와 동일 상태 *v* 한 후 *expr_first*합니다.
    * 그렇지 않은 경우, 상태 *v* 후 *expr_first* 확실 하 게 할당 되 면 다음 상태의 *v* 후 *expr* 정적으로 할당 됩니다.
    * 그렇지 않은 경우, 상태 *v* 후 *expr_second* 확실 하 게 할당 된 및 상태의 *v* 후 *expr_first* 확실히 " 할당 된 true 식 뒤"다음 상태의 *v* 한 후 *expr* 정적으로 할당 됩니다.
    * 그렇지 않은 경우, 상태 *v* 후 *expr_second* 정적으로 할당 하거나 "대입할 false 식 뒤" 다음 상태의 *v* 후*expr* "확실 하 게 할당 된 후 false 식"입니다.
    * 그렇지 않은 경우, 상태 *v* 한 후 *expr_first* "정적으로 할당 된 true 식 뒤", 및의 상태는 *v* 후 *expr_second*이면 "정적으로 할당 된 true 식 뒤", 상태 *v* 한 후 *expr* "확실 하 게 할당 된 true 식 뒤"입니다.
    * 이 고, 그렇지 상태의 *v* 한 후 *expr* 확실 하 게 할당 되지 않습니다.

예제
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
변수의 `i` 의 포함 된 문 중 하나에서 정적으로 할당 된 것으로 간주 됩니다는 `if` 문이 아니라 다른 합니다. `if` 메서드의 문은 `G`, 변수의 `i` 때문에 두 번째 포함 된 문에서 확실 하 게 할당 되었습니다 식 실행 `(i = y)` 앞에 항상이 포함 된 문 실행 합니다. 반대로, 변수의 `i` 할당 되지 않은 확실 하 게 첫 번째는 포함 된 문에서 이후에 `x >= 0` 수 테스트 true 인 변수에 결과 `i` 할당 되지 않은 합니다.

#### <a name="-logical-negation-expressions"></a>! (논리적 부정) 식

식에 대 한 *expr* 양식의 `! expr_operand`:

*  한정 된 할당 상태의 *v* 하기 전에 *expr_operand* 한정 된 할당 상태와 동일 *v* 전에 *expr*합니다.
*  한정 된 할당 상태의 *v* 한 후 *expr* 에 의해 결정 됩니다.
    * 경우 상태의 *v* 후 * expr_operand * 확실 하 게 할당 되 면 다음 상태의 *v* 후 *expr* 정적으로 할당 됩니다.
    * 경우 상태의 *v* 후 * expr_operand * 확실 하 게를 할당 하지 않으면 다음 상태의 *v* 후 *expr* 확실 하 게 할당 되지 않습니다.
    * 경우 상태의 *v* 후 * expr_operand * 이면 "정적으로 할당 된 후 false 식"을 상태의 *v* 후 *expr* "확실 하 게 할당 된 후 true 식 "입니다.
    * 경우 상태의 *v* 후 * expr_operand * 이면 "정적으로 할당 된 true 식 뒤", 상태의 *v* 후 *expr* "확실 하 게 할당 된 후 false 식 "입니다.

#### <a name="-null-coalescing-expressions"></a>?? 식 (null 병합)

식에 대 한 *expr* 양식의 `expr_first ?? expr_second`:

*  한정 된 할당 상태의 *v* 하기 전에 *expr_first* 한정 된 할당 상태와 동일 *v* 전에 *expr*합니다.
*  한정 된 할당 상태의 *v* 하기 전에 *expr_second* 한정 된 할당 상태와 동일 *v* 후 *expr_first*합니다.
*  한정 된 할당 설명이 *v* 한 후 *expr* 에 의해 결정 됩니다.
    * 하는 경우 *expr_first* 상수 식입니다 ([상수 식을](expressions.md#constant-expressions)) null 값을 사용 하 여 해당 상태의 *v* 후 *expr* 동일 상태와 *v* 한 후 *expr_second*합니다.
*  이 고, 그렇지 상태의 *v* 한 후 *expr* 한정 된 할당 상태와 동일 *v* 후 *expr_first*합니다.

#### <a name="-conditional-expressions"></a>?: (conditional) 식

식에 대 한 *expr* 양식의 `expr_cond ? expr_true : expr_false`:

*  한정 된 할당 상태의 *v* 하기 전에 *expr_cond* 의 상태와 동일 *v* 전에 *expr*합니다.
*  한정 된 할당 상태의 *v* 하기 전에 *expr_true* 다음 중 하나를 보유 하는 경우에 할당 됩니다.
    * *expr_cond* 는 값을 사용 하 여 상수 식 `false`
    * 상태의 *v* 한 후 *expr_cond* 명확 하 게 할당 되었거나 "정적 true 식으로 할당" 합니다.
*  한정 된 할당 상태의 *v* 하기 전에 *expr_false* 다음 중 하나를 보유 하는 경우에 할당 됩니다.
    * *expr_cond* 는 값을 사용 하 여 상수 식 `true`
*  상태의 *v* 한 후 *expr_cond* 명확 하 게 할당 되었거나 "정적 false 식으로 할당" 합니다.
*  한정 된 할당 상태의 *v* 한 후 *expr* 에 의해 결정 됩니다.
    * 하는 경우 *expr_cond* 상수 식입니다 ([상수 식을](expressions.md#constant-expressions)) 값을 사용 하 여 `true` 상태 *v* 후 *expr* 상태와 같습니다 *v* 한 후 *expr_true*합니다.
    * 그렇지 않고 *expr_cond* 상수 식입니다 ([상수 식을](expressions.md#constant-expressions)) 값을 사용 하 여 `false` 상태 *v* 후 *expr* 상태의 동일 *v* 한 후 *expr_false*합니다.
    * 그렇지 않은 경우, 상태 *v* 후 *expr_true* 정적으로 할당 및 상태의 *v* 후 *expr_false* 확실히 할당 상태 *v* 한 후 *expr* 정적으로 할당 됩니다.
    * 이 고, 그렇지 상태의 *v* 한 후 *expr* 확실 하 게 할당 되지 않습니다.

#### <a name="anonymous-functions"></a>익명 함수

에 *lambda_expression* 또는 *anonymous_method_expression* *expr* 본문 (중 하나 *블록* 또는 *식* ) *본문*:

*  외부 변수의 한정 된 할당 상태 *v* 하기 전에 *본문* 의 상태와 동일 *v* 앞 *expr*합니다. 즉, 외부 변수의 한정 된 할당 상태는 익명 함수 측면에서 상속 됩니다.
*  외부 변수의 한정 된 할당 상태 *v* 한 후 *expr* 의 상태와 동일 *v* 전에 *expr*합니다.

이 예제에서
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
이후 컴파일 타임 오류가 `max` 익명 함수 선언 된 위치 확실 하 게 할당 되지 않습니다. 이 예제에서
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
에 대 한 할당 이후 컴파일 타임 오류를 생성 `n` 익명 함수에 영향을 주지 않습니다의 한정 된 할당 상태에 `n` 익명 함수 외부입니다.

## <a name="variable-references"></a>변수 참조

A *variable_reference* 되는 *식* 변수로 분류 되는 합니다. A *variable_reference* 현재 값을 인출 하 고 새 값을 저장할 액세스할 수 있는 저장소 위치를 나타냅니다.

```antlr
variable_reference
    : expression
    ;
```

C 및 c + +에는 *variable_reference* 이라고는 *lvalue*합니다.

## <a name="atomicity-of-variable-references"></a>변수 참조의 원자성

데이터 형식은의 읽기 및 쓰기는 원자성: `bool`, `char`, `byte`, `sbyte`, `short`를 `ushort`, `uint`를 `int`, `float`, 참조 형식입니다. 또한 위 목록에 있는 기본 형식 사용 하 여 열거형의 읽기 및 쓰기도 원자성입니다. 포함 한 다른 형식의의 읽기 및 쓰기로 `long`, `ulong`, `double`, 및 `decimal`, 사용자 정의 형식 뿐만 아니라 아닐 원자성입니다. 해당 목적에 맞게 설계 하는 라이브러리 함수 외에도 보장은 없습니다 원자성 읽기-수정-쓰기의 같은 증가 또는 감소 하는 경우.

