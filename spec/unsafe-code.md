# <a name="unsafe-code"></a>안전하지 않은 코드

핵심 C# 언어, 이전 장에서에 정의 된 대로 특히 C 및 c + +에서에서 다릅니다 포인터의 데이터 형식으로 생략 합니다. 대신 C# 제공 참조는 가비지 수집기에 의해 관리 되는 개체를 만들 수 있습니다. 이 디자인에서는 다른 기능과 함께 사용 하면 C# C 또는 c + + 보다 훨씬 더 안전한 언어입니다. 핵심 C# 언어에서 단순히 수 없는 초기화 되지 않은 변수, "현 수" 포인터 또는 배열 경계를 벗어난 인덱스 하는 식입니다. 버그의 전체 범주 C도 정기적으로 영향을 줄 및 c + + 프로그램 따라서 제거 됩니다.

C 또는 c + +의 거의 모든 포인터 형식 구조는 C#에서 참조 형식을 해당 사용자, 그럼에도 불구 하 고 가지 포인터 형식에 대 한 액세스 필요 되는 경우가 있습니다. 예를 들어, 기본 운영 체제와 상호 작용 하는 메모리 매핑된 장치에 액세스, 시간이 중요 한 알고리즘을 구현 아닐 포인터에 액세스 하지 않고도 불가능 합니다. 이 요구를 해결 하기 위해 C# 기능을 제공 작성할 ***안전 하지 않은 코드***합니다.

안전 하지 않은 코드에서 선언에 대 한 포인터를 포인터 및 변수의 주소를 정수 계열 형식 간의 변환을 수행할 작동 및 등을 가능성이 있습니다. 어떤 의미에서 안전 하지 않은 코드를 작성은 매우 C# 프로그램에서 C 코드를 작성 합니다.

안전 하지 않은 코드는 실제로 개발자와 사용자의 관점에서 "안전한" 기능입니다. 한정자를 사용 하 여 안전 하지 않은 코드를 명확 하 게 표시 해야 `unsafe`개발자 안전 하지 않은 기능은 사용할 수 없습니다. 실수로, 및 실행 엔진은 신뢰할 수 없는 환경에서 안전 하지 않은 코드를 실행할 수 없습니다 확인 하 게 작동 합니다.

## <a name="unsafe-contexts"></a>안전 하지 않은 컨텍스트

C#의 안전 하지 않은 기능은 안전 하지 않은 컨텍스트에서만 사용할 수 있습니다. 안전 하지 않은 컨텍스트를 포함 하 여 도입 되는 `unsafe` 형식 또는 멤버의 또는 사용 하 여 선언에서 한정자를 *unsafe_statement*:

*  클래스, 구조체, 인터페이스 또는 대리자의 선언 포함 될 수 있습니다는 `unsafe` 한정자가 있는 경우 해당 형식 선언 (클래스, 구조체 또는 인터페이스의 본문 포함)의 전체 텍스트 범위가 안전 하지 않은 컨텍스트 간주 됩니다.
*  필드, 메서드, 속성, 이벤트, 인덱서, 연산자, 인스턴스 생성자, 소멸자 또는 정적 생성자의 선언은 수는 `unsafe` 한정자가 있는 경우 해당 멤버 선언의 전체 텍스트 범위가 안전 하지 않은 비율은 컨텍스트입니다.
*  *unsafe_statement* 내에서 안전 하지 않은 컨텍스트를 사용 하도록 설정 된 *블록*합니다. 연결 된 전체 텍스트 범위가 *블록* 안전 하지 않은 컨텍스트 것으로 간주 됩니다.

연결 된 문법 요소는 다음과 같습니다.

```antlr
class_modifier_unsafe
    : 'unsafe'
    ;

struct_modifier_unsafe
    : 'unsafe'
    ;

interface_modifier_unsafe
    : 'unsafe'
    ;

delegate_modifier_unsafe
    : 'unsafe'
    ;

field_modifier_unsafe
    : 'unsafe'
    ;

method_modifier_unsafe
    : 'unsafe'
    ;

property_modifier_unsafe
    : 'unsafe'
    ;

event_modifier_unsafe
    : 'unsafe'
    ;

indexer_modifier_unsafe
    : 'unsafe'
    ;

operator_modifier_unsafe
    : 'unsafe'
    ;

constructor_modifier_unsafe
    : 'unsafe'
    ;

destructor_declaration_unsafe
    : attributes? 'extern'? 'unsafe'? '~' identifier '(' ')' destructor_body
    | attributes? 'unsafe'? 'extern'? '~' identifier '(' ')' destructor_body
    ;

static_constructor_modifiers_unsafe
    : 'extern'? 'unsafe'? 'static'
    | 'unsafe'? 'extern'? 'static'
    | 'extern'? 'static' 'unsafe'?
    | 'unsafe'? 'static' 'extern'?
    | 'static' 'extern'? 'unsafe'?
    | 'static' 'unsafe'? 'extern'?
    ;

embedded_statement_unsafe
    : unsafe_statement
    | fixed_statement
    ;

unsafe_statement
    : 'unsafe' block
    ;
```

예제

```csharp
public unsafe struct Node
{
    public int Value;
    public Node* Left;
    public Node* Right;
}
```

`unsafe` 한정자 구조체 선언에 지정 하면 전체 텍스트 범위가 안전 하지 않은 컨텍스트 되도록 구조체 선언 합니다. 즉, 선언할 수는 `Left` 및 `Right` 필드는 포인터 형식 이어야 합니다. 위의 예제를 작성할 수도 있습니다.

```csharp
public struct Node
{
    public int Value;
    public unsafe Node* Left;
    public unsafe Node* Right;
}
```

여기서는 `unsafe` 필드 선언에는 한정자로 인해 해당 선언이 안전 하지 않은 컨텍스트를 고려해 야 합니다.

포인터 형식의 사용을 허용 하므로 안전 하지 않은 컨텍스트를 설정 하는 `unsafe` 한정자는 형식 또는 멤버에 대 한 영향을 주지 않습니다. 예제

```csharp
public class A
{
    public unsafe virtual void F() {
        char* p;
        ...
    }
}

public class B: A
{
    public override void F() {
        base.F();
        ...
    }
}
```

`unsafe` 한정자를 `F` 에서 메서드 `A` 하면 다음의 텍스트 범위가 `F` 언어의 안전 하지 않은 기능을 사용할 수 있는 안전 하지 않은 컨텍스트를 합니다. 재정의 `F` 에 `B`를 다시 지정 하지 않아도 됩니다는 `unsafe` 한정자-하지 않는 한, 물론를 `F` 에서 메서드 `B` 안전 하지 않은 기능에 대 한 액세스를 해야 하는 자체.

포인터 형식에 메서드 시그니처의 일부로 경우 상황은 약간 다른

```csharp
public unsafe class A
{
    public virtual void F(char* p) {...}
}

public class B: A
{
    public unsafe override void F(char* p) {...}
}
```

여기에 있으므로 `F`의 서명 포인터 형식에만 쓸 수 있습니다 안전 하지 않은 컨텍스트에서 합니다. 그러나 만들어 하거나 전체 클래스, 안전 하지 않은의 경우 처럼 안전 하지 않은 컨텍스트를 도입할 수 있습니다 `A`를 포함 하 여는 `unsafe` 메서드 선언에서 한정자의 경우에서 마찬가지로 `B`합니다.

## <a name="pointer-types"></a>포인터 형식

안전 하지 않은 컨텍스트에서 *형식* ([형식](types.md)) 수는 *pointer_type* 뿐만 *value_type* 또는 *reference_type* . 그러나를 *pointer_type* 에서 사용할 수도 있습니다는 `typeof` 식 ([익명 개체 생성 식을](expressions.md#anonymous-object-creation-expressions)) 안전 하지 않은 컨텍스트 외부에서 같이 사용법은 안전 하지 않은 합니다.

```antlr
type_unsafe
    : pointer_type
    ;
```

*pointer_type* 으로 기록 되는 *unmanaged_type* 또는 키워드 `void`뒤를 `*` 토큰:

```antlr
pointer_type
    : unmanaged_type '*'
    | 'void' '*'
    ;

unmanaged_type
    : type
    ;
```

전에 지정 된 형식 합니다 `*` 포인터에서 형식이 호출 됩니다 합니다 ***referent 형식을*** 포인터 형식의 합니다. 포인터 형식의 값이 가리키는 변수의 형식을 나타냅니다.

참조 (참조 형식의 값)와 달리 포인터는 가비지 수집기에 의해 추적 되지 않습니다-가비지 수집기는 포인터와 지점이 있는 데이터의 알지 못합니다. 에 대 한 참조를 가리키도록 포인터이 따라서 허용 되지 않습니다 또는 구조체에 참조를 포함 하는 포인터의 참조 형식 이어야 합니다는 *unmanaged_type*합니다.

*unmanaged_type* 는 없는 모든 형식을 *reference_type* 가 포함 되어 생성 된 형식, 또는 *reference_type* 또는 모든 수준에서 형식 필드를 생성 합니다. 중첩 합니다. 즉, 한 *unmanaged_type* 다음 중 하나입니다.

*  `sbyte``byte`, `short`, `ushort`, `int`, `uint`를 `long`, `ulong`, `char`, `float`를 `double`, `decimal`, 또는 `bool`합니다.
*  모든 *enum_type*합니다.
*  모든 *pointer_type*합니다.
*  모든 사용자 정의 *struct_type* 생성 된 형식이 아닌 하의 필드를 포함 하 *unmanaged_type*만 합니다.

포인터 및 참조를 혼합 하는 것에 대 한 직관적인 규칙 참조 (개체)의 참조 대상이 포인터를 포함 하도록 허용 되는 포인터의 참조 대상이 참조를 포함할 수 없습니다 경우

포인터 형식의 몇 가지 예는 아래 표에 제공 됩니다.

| __예제__ | __설명__                               |
|-------------|-----------------------------------------------|
| `byte*`     | 에 대 한 포인터 `byte`                             |
| `char*`     | 에 대 한 포인터 `char`                             |
| `int**`     | 에 대 한 포인터에 대 한 포인터 `int`                   |
| `int*[]`    | 에 대 한 포인터의 1 차원 배열 `int` |
| `void*`     | 알 수 없는 형식에 대 한 포인터                       |

지정 된 구현에 대 한 모든 포인터 형식에 같은 크기 및 표현 있어야 합니다.

C 및 c + +, C#에서 동일한 선언에서 여러 포인터 선언 된 경우와 달리는 `*` 각 포인터 이름의 접두 문장 부호로 아니라 기본 형식에만 함께 기록 됩니다. 예

```csharp
int* pi, pj;    // NOT as int *pi, *pj;
```

형식의 포인터 값 `T*` 형식의 변수에 대 한 주소를 나타내는 `T`합니다. 포인터 간접 참조 연산자 `*` ([포인터 간접 참조](unsafe-code.md#pointer-indirection))에서이 변수에 액세스할 수 있습니다. 예를 들어 변수를 지정 `P` 형식의 `int*`, 식이 `*P` 나타냅니다 합니다 `int` 에 포함 된 주소에 있는 변수 `P`합니다.

개체 참조와 같은 포인터 수 `null`입니다. 간접 참조 연산자를 적용 한 `null` 포인터 구현 시 정의 된 동작이 발생 합니다. 값을 사용 하 여 포인터 `null` 모든 비트가 0으로 표시 됩니다.

`void*` 형식은 알 수 없는 형식에 대 한 포인터를 나타냅니다. Referent 형식을 알려진 아니므로 형식의 포인터에 간접 참조 연산자를 적용할 수 없습니다 `void*`, 또는에서 이러한 포인터 산술 연산을 수행할 수 있습니다. 그러나 형식의 포인터 `void*` 다른 포인터 형식 (또는 그 반대로) 캐스팅 될 수 있습니다.

포인터 형식은 형식의 별도 범주입니다. 참조 형식 및 값 형식의 경우와 달리 포인터 형식에서 상속 하지 않습니다 `object` 포인터 형식 간의 변환이 존재 하 고 `object`입니다. 특히, boxing 및 unboxing ([Boxing 및 unboxing](types.md#boxing-and-unboxing)) 포인터에 대 한 지원 되지 않습니다. 그러나 포인터 형식과 정수 계열 형식 간 및 서로 다른 포인터 형식 간에 변환할 수 있습니다. 에 설명 되어 [포인터 변환](unsafe-code.md#pointer-conversions)합니다.

A *pointer_type* 형식 인수로 사용할 수 없습니다 ([형식 생성](types.md#constructed-types))과 형식 유추 ([형식 유추](expressions.md#type-inference)) 유추 있어야 하는 제네릭 메서드 호출에서 실패를 형식 인수는 포인터 형식 이어야 합니다.

A *pointer_type* volatile 필드의 형식으로 사용할 수 있습니다 ([Volatile 필드](classes.md#volatile-fields)).

포인터로 전달 될 수 있지만 `ref` 또는 `out` 매개 변수를 이렇게 포인터도 수 있으므로 정의 되지 않은 동작이 발생할 수 없습니다 더 이상 호출된 된 메서드가 반환 될 때 존재 하는 지역 변수 또는 고정된 하는 개체를 가리키도록 설정 지점에 사용 되는, 더 이상 고정 됩니다. 예를 들어:

```csharp
using System;

class Test
{
    static int value = 20;

    unsafe static void F(out int* pi1, ref int* pi2) {
        int i = 10;
        pi1 = &i;

        fixed (int* pj = &value) {
            // ...
            pi2 = pj;
        }
    }

    static void Main() {
        int i = 10;
        unsafe {
            int* px1;
            int* px2 = &i;

            F(out px1, ref px2);

            Console.WriteLine("*px1 = {0}, *px2 = {1}",
                *px1, *px2);    // undefined behavior
        }
    }
}
```

메서드가 일부 형식의 값을 반환할 수 및 해당 형식에 대 한 포인터를 수 있습니다. 예를 들어의 연속 시퀀스에 대 한 포인터를 지정 하는 경우 `int`s, 해당 시퀀스의 요소 수 및 일부 기타 `int` 값 일치 하는 경우 다음 메서드는 시퀀스의 해당 값의 주소를 반환, 그렇지 않으면 를반환합니다`null`:

```csharp
unsafe static int* Find(int* pi, int size, int value) {
    for (int i = 0; i < size; ++i) {
        if (*pi == value) 
            return pi;
        ++pi;
    }
    return null;
}
```

안전 하지 않은 컨텍스트에서 다양 한 구문을 포인터 연산에 사용할 수 있습니다.

*  합니다 `*` 연산자는 포인터 간접 참조 하는 데 사용할 수 있습니다 ([포인터 간접 참조](unsafe-code.md#pointer-indirection)).
*  합니다 `->` 포인터를 통해 구조체의 멤버에 액세스 하려면 연산자를 사용할 수 있습니다 ([포인터 멤버 액세스](unsafe-code.md#pointer-member-access)).
*  합니다 `[]` 포인터 인덱싱 연산자를 사용할 수 있습니다 ([포인터 요소 액세스](unsafe-code.md#pointer-element-access)).
*  합니다 `&` 연산자는 변수에 대 한 주소를 가져오는 데 사용할 수 있습니다 ([address-of 연산자](unsafe-code.md#the-address-of-operator)).
*  합니다 `++` 하 고 `--` 포인터 증가 및 감소 연산자를 사용할 수 있습니다 ([포인터 증가 및 감소](unsafe-code.md#pointer-increment-and-decrement)).
*  합니다 `+` 하 고 `-` 포인터 산술 연산을 수행 하는 연산자를 사용할 수 있습니다 ([포인터 산술 연산을](unsafe-code.md#pointer-arithmetic)).
*  합니다 `==`, `!=`를 `<`, `>`를 `<=`, 및 `=>` 연산자를 사용 하 여 포인터를 비교할 수 있습니다 ([포인터 비교](unsafe-code.md#pointer-comparison)).
*  합니다 `stackalloc` 연산자를 사용 하 여 호출 스택에서 메모리를 할당할 수 있습니다 ([고정 크기 버퍼](unsafe-code.md#fixed-size-buffers)).
*  합니다 `fixed` 문은 일시적으로 변수를 수정 하므로 해당 주소를 가져올 수 있습니다 데 사용할 수 있습니다 ([fixed 문을](unsafe-code.md#the-fixed-statement)).

## <a name="fixed-and-moveable-variables"></a>고정 및 고정 되지 않은 변수

Address-of 연산자 ([address-of 연산자](unsafe-code.md#the-address-of-operator)) 및 `fixed` 문 ([fixed 문을](unsafe-code.md#the-fixed-statement)) 변수 두 가지 범주로 나눌: ***변수고정***하 고 ***이동 가능한 변수***합니다.

고정된 변수 가비지 수집기의 작업에 의해 영향을 받지 않는 저장소 위치에 있어야 합니다. (고정 변수의 예로 지역 변수, 값 매개 변수 및 포인터를 역참조 하 여 만든 변수.) 다른 한편으로 고정 되지 않은 변수 재배치 또는 가비지 수집기에 의해 삭제 될 수 있는 저장소 위치에 있어야 합니다. (고정 되지 않은 변수의 예로 필드 개체 및 배열 요소에 있습니다.)

합니다 `&` 연산자 ([address-of 연산자](unsafe-code.md#the-address-of-operator)) 제한 없이 가져올 고정 변수의 주소를 허용 합니다. 그러나 변수인 재배치 또는 가비지 수집기에 의해 삭제 될 수 있습니다 이기 때문에 고정 되지 않은 변수에 대 한 주소만 가져올 수 있습니다 사용 하는 `fixed` 문 ([fixed 문을](unsafe-code.md#the-fixed-statement)), 및 해당 주소 해당 기간 동안에 `fixed` 문입니다.

정확 하 게 말해에서 고정된 변수는 다음 중 하나:

*  결과에서 변수를 *simple_name* ([단순 이름](expressions.md#simple-names)) 참조 하는 지역 변수 또는 값 매개 변수는 익명 함수에 의해 캡처됩니다 하지 않는 한 합니다.
*  변수 결과 *member_access* ([멤버 액세스](expressions.md#member-access)) 형식의 `V.I`여기서 `V` 고정 변수입니다를 *struct_type*합니다.
*  결과에서 변수를 *pointer_indirection_expression* ([포인터 간접 참조](unsafe-code.md#pointer-indirection)) 형식의 `*P`, *pointer_member_access* ([포인터 멤버 액세스](unsafe-code.md#pointer-member-access)) 형식의 `P->I`, 또는 *pointer_element_access* ([포인터 요소 액세스](unsafe-code.md#pointer-element-access)) 형식의 `P[E]`합니다.

다른 모든 변수가 고정 되지 않은 변수도 분류 됩니다.

정적 필드 변수인으로 분류 되는 참고 합니다. 또한 한 `ref` 또는 `out` 매개 변수에 대해 지정 된 인수 변수는 고정 하는 경우에 매개 변수인으로 분류 됩니다. 마지막으로, 메모에 대 한 포인터를 역참조 하 여 생성 되는 변수는 항상 고정된 변수로으로 분류 됩니다.

## <a name="pointer-conversions"></a>포인터 변환

안전 하지 않은 컨텍스트에서만 사용할 수 있는 암시적 변환 집합 ([암시적 변환을](conversions.md#implicit-conversions)) 다음 암시적 포인터 변환을 포함 하도록 확장 되었습니다.

*  모든 *pointer_type* 형식으로 `void*`입니다.
*  `null` 에 리터럴 *pointer_type*합니다.

또한 안전 하지 않은 컨텍스트에서 사용할 수 있는 명시적 변환 집합 ([명시적 변환](conversions.md#explicit-conversions)) 다음과 같은 명시적 포인터 변환은 포함 하도록 확장 되었습니다.

*  모든 *pointer_type* 다른 *pointer_type*합니다.
*  `sbyte`, `byte`, `short`, `ushort`를 `int`를 `uint`를 `long`, 또는 `ulong` 에 *pointer_type*합니다.
*  *pointer_type* 하 `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`를 `long`, 또는 `ulong`합니다.

안전 하지 않은 컨텍스트 표준 암시적 변환 집합에서 마지막으로 ([표준 암시적 변환이](conversions.md#standard-implicit-conversions)) 다음과 같은 포인터 변환에 포함 되어 있습니다.

*  모든 *pointer_type* 형식으로 `void*`입니다.

두 포인터 형식 간의 변환에는 실제 포인터 값은 변경 되지 않습니다. 즉, 다른 하나는 포인터 형식에서 변환 포인터에 의해 제공 된 기본 주소에 영향을 주지 합니다.

포인터 형식으로 변환할 때 다른 결과 포인터를 가리키는 형식에 대해 올바르게 정렬 되지 않은 경우에 결과 역참조 하는 경우 동작이 정의 되지 않습니다. 일반적으로 "올바르게 정렬 된" 개념은 전이적: 경우 입력에 대 한 포인터 `A` 입력에 대 한 포인터에 대 한 올바르게 정렬 될 `B`는 차례로 올바르게 맞춰진 입력에 대 한 포인터에 대 한 `C`, 다음에 대 한 포인터 형식 `A`형식의 포인터에 대 한 올바르게 맞춰진 `C`합니다.

다른 형식에 대 한 포인터를 통해 액세스 한 형식이 있는 변수는 다음과 같은 경우를 고려 합니다.

```csharp
char c = 'A';
char* pc = &c;
void* pv = pc;
int* pi = (int*)pv;
int i = *pi;         // undefined
*pi = 123456;        // undefined
```

포인터 형식 변환 되 면 바이트에 대 한 포인터는 변수의 최하위 주소 지정된 바이트를 결과 지점. 변수의 크기를 최대 결과의 연속적 증분 해당 변수의 나머지 바이트에 대 한 포인터를 생성합니다. 예를 들어, 다음에 메서드가 표시 각 8 바이트는 double 값을 16 진수 값으로:

```csharp
using System;

class Test
{
    unsafe static void Main() {
      double d = 123.456e23;
        unsafe {
           byte* pb = (byte*)&d;
            for (int i = 0; i < sizeof(double); ++i)
               Console.Write("{0:X2} ", *pb++);
            Console.WriteLine();
        }
    }
}
```

물론, 생성 된 출력 엔디언에 따라 달라 집니다.

포인터와 정수 간의 매핑을 구현 시 정의 됩니다. 그러나 32에서 * 선형 주소 공간을 사용 하는 64 비트 CPU 아키텍처, 정수 계열 형식에서 포인터의 변환은 일반적으로 처럼 정확 하 게 변환을 `uint` 또는 `ulong` 값을 각각 해당 정수 계열 형식에서입니다.

### <a name="pointer-arrays"></a>포인터 배열

안전 하지 않은 컨텍스트에서 포인터 배열은 생성할 수 있습니다. 다른 배열 형식에 적용 되는 변환 중 일부만 대 한 포인터 배열에서 허용 됩니다.

*  암시적 참조 변환을 ([암시적 참조 변환을](conversions.md#implicit-reference-conversions))에서 *array_type* 에 `System.Array` 도 구현 하는 인터페이스 포인터 배열에 적용 합니다. 그러나 통해 배열 요소에 액세스 하려고 `System.Array` 하거나, 포인터 형식으로 변환 될으로 구현 하는 인터페이스에서 런타임 시 예외를 발생 하면 `object`합니다.
*  암시적 및 명시적 참조 변환을 ([암시적 참조 변환을](conversions.md#implicit-reference-conversions), [명시적 참조 변환이](conversions.md#explicit-reference-conversions))는 1 차원 배열 형식에서 `S[]` 에 `System.Collections.Generic.IList<T>` 및 제네릭 기본 인터페이스로 적용 하지는 않습니다 포인터 배열의 포인터 형식은 형식 인수로 사용할 수 없습니다 및 포인터가 아닌 형식에 대 한 포인터 형식에서 변환이 없기 때문입니다.
*  명시적 참조 변환이 ([명시적 참조 변환을](conversions.md#explicit-reference-conversions))에서 `System.Array` 인터페이스를 구현 하 고 *array_type* 포인터 배열에 적용 됩니다.
*  명시적 참조 변환을 ([명시적 참조 변환을](conversions.md#explicit-reference-conversions))에서 `System.Collections.Generic.IList<S>` 는 1 차원 배열 형식에 기본 인터페이스 및 `T[]` 포인터 형식 수 없으므로 포인터 배열에 적용 되지 않습니다 사용 되는 인수 형식 및 포인터가 아닌 형식에 대 한 포인터 형식에서 변환이 없습니다.

이러한 제한에 대 한 확장 함을 의미 합니다 `foreach` 에 설명 된 배열에 대 문을 [foreach 문을](statements.md#the-foreach-statement) 포인터 배열에 적용할 수 없습니다. 대신, 폼의 foreach 문을

```csharp
foreach (V v in x) embedded_statement
```

여기서 형식의 `x` 형식의 배열 형식인 `T[,,...,]`, `N` 차원에서 1 뺀 수는 및 `T` 또는 `V` 포인터 형식이, 중첩 된 for 루프를 사용 하 여 다음과 같이 확장 됩니다:

```csharp
{
    T[,,...,] a = x;
    for (int i0 = a.GetLowerBound(0); i0 <= a.GetUpperBound(0); i0++)
    for (int i1 = a.GetLowerBound(1); i1 <= a.GetUpperBound(1); i1++)
    ...
    for (int iN = a.GetLowerBound(N); iN <= a.GetUpperBound(N); iN++) {
        V v = (V)a.GetValue(i0,i1,...,iN);
        embedded_statement
    }
}
```

변수 `a`, `i0`를 `i1`,..., `iN` 에 표시 하거나 액세스할 수 없는지 `x` 또는 *embedded_statement* 또는 프로그램의 다른 소스 코드입니다. 변수의 `v` 포함 된 문에서 읽기 전용입니다. 명시적 변환이 없는 경우 ([포인터 변환](unsafe-code.md#pointer-conversions))에서 `T` (요소 형식)를 `V`오류가 생성 되 고 추가 단계가 수행 되지 않습니다. 하는 경우 `x` 기본값이 `null`, `System.NullReferenceException` 런타임에 throw 됩니다.

## <a name="pointers-in-expressions"></a>식에 대 한 포인터

안전 하지 않은 컨텍스트에서 식을 포인터 형식의 결과 생성할 수 있습니다 이지만 안전 하지 않은 컨텍스트 외부 포인터 형식 이어야 하는 식에 대 한 컴파일 시간 오류입니다. 정확 하 게 말해에서 안전 하지 않은 컨텍스트 외부 컴파일 타임 오류가 발생 하는 경우 *simple_name* ([단순 이름](expressions.md#simple-names)), *member_access* ([멤버 액세스 ](expressions.md#member-access)), *invocation_expression* ([호출 식](expressions.md#invocation-expressions)), 또는 *element_access* ([요소 액세스](expressions.md#element-access))는 포인터 형식입니다.

안전 하지 않은 컨텍스트에서 *primary_no_array_creation_expression* ([기본 식](expressions.md#primary-expressions)) 및 *unary_expression* ([단항연산자](expressions.md#unary-operators)) 프로덕션에는 다음과 같은 추가 구문이 허용:

```antlr
primary_no_array_creation_expression_unsafe
    : pointer_member_access
    | pointer_element_access
    | sizeof_expression
    ;

unary_expression_unsafe
    : pointer_indirection_expression
    | addressof_expression
    ;
```

이러한 구조는 다음 섹션에 설명 되어 있습니다. 우선 순위 및 결합성 안전 하지 않은 연산자의 문법으로 포함 됩니다.

### <a name="pointer-indirection"></a>포인터 간접 참조

A *pointer_indirection_expression* 별표 이루어져 있습니다 (`*`) 뒤에 *unary_expression*합니다.

```antlr
pointer_indirection_expression
    : '*' unary_expression
    ;
```

단항 `*` 연산자를 포인터 간접 참조를 나타냅니다. 포인터를 가리키는 변수를 가져오는 데 사용 됩니다. 평가 결과 `*P`여기서 `P` 포인터 형식의 식이 `T*`, 형식의 변수가 `T`합니다. 단항 적용할 컴파일 타임 오류 `*` 형식의 식에 연산자 `void*` 또는 포인터 형식이 아닌 식입니다.

단항 적용 `*` 연산자는 `null` 포인터 구현 시 정의 됩니다. 특히 보장이 없습니다이 작업에서 throw 하는 `System.NullReferenceException`합니다.

잘못 된 값을 포인터에 단항의 동작에 대 한 할당 된 경우 `*` 연산자 정의 되지 않습니다. 단항에서 포인터를 역참조에 대 한 잘못 된 값에 속하지 `*` 연산자는 형식 지정에 대 한 부적절 하 게 정렬 하는 주소 (에서 예제를 참조 하세요 [포인터 변환](unsafe-code.md#pointer-conversions)), 및 후 변수의 주소는 수명이 종료 합니다.

한정 된 할당 분석을 위해 폼의 식을 계산 하 여 생성 되는 변수 `*P` 처음에 할당 된 것으로 간주 됩니다 ([처음에 할당 되는 변수](variables.md#initially-assigned-variables)).

### <a name="pointer-member-access"></a>포인터 멤버 액세스

*pointer_member_access* 이루어져 있습니다를 *primary_expression*뒤를 "`->`" 토큰, 뒤에 *식별자* 및는 선택적 *type_argument_list*합니다.

```antlr
pointer_member_access
    : primary_expression '->' identifier
    ;
```

형식의 포인터 멤버 액세스 `P->I`, `P` 이외의 포인터 형식의 식 이어야 `void*`, 및 `I` 는 형식의 액세스 가능 멤버를 표시 해야 합니다 `P` 지점입니다.

형식의 포인터 멤버 액세스 `P->I` 와 동일 하 게 평가 됩니다 `(*P).I`합니다. 에 대 한 설명은 포인터 간접 참조 연산자 (`*`)를 참조 하세요 [포인터 간접 참조](unsafe-code.md#pointer-indirection)합니다. 에 대 한 설명은 멤버 액세스 연산자 (`.`)를 참조 하세요 [멤버 액세스](expressions.md#member-access)합니다.

예제

```csharp
using System;

struct Point
{
    public int x;
    public int y;

    public override string ToString() {
        return "(" + x + "," + y + ")";
    }
}

class Test
{
    static void Main() {
        Point point;
        unsafe {
            Point* p = &point;
            p->x = 10;
            p->y = 20;
            Console.WriteLine(p->ToString());
        }
    }
}
```

`->` 연산자는 필드에 액세스 하 고 포인터를 통해 구조체의 메서드를 호출 하는 데 사용 됩니다. 때문에 작업 `P->I` 정확 하 게 해당 하는 `(*P).I`, `Main` 메서드 작성 원활 하 게 수:

```csharp
class Test
{
    static void Main() {
        Point point;
        unsafe {
            Point* p = &point;
            (*p).x = 10;
            (*p).y = 20;
            Console.WriteLine((*p).ToString());
        }
    }
}
```

### <a name="pointer-element-access"></a>포인터 요소 액세스

A *pointer_element_access* 이루어져를 *primary_no_array_creation_expression* 묶인 식을 뒤에 "`[`"및"`]`"입니다.

```antlr
pointer_element_access
    : primary_no_array_creation_expression '[' expression ']'
    ;
```

형식의 포인터 요소 액세스 `P[E]`, `P` 이외의 포인터 형식의 식 이어야 `void*`, 및 `E` 에 암시적으로 변환할 수 있는 식 이어야 합니다 `int`, `uint`를 `long`, 또는 `ulong`합니다.

형식의 포인터 요소 액세스 `P[E]` 와 동일 하 게 평가 됩니다 `*(P + E)`합니다. 에 대 한 설명은 포인터 간접 참조 연산자 (`*`)를 참조 하세요 [포인터 간접 참조](unsafe-code.md#pointer-indirection)합니다. 에 대 한 설명은 포인터 더하기 연산자 (`+`)를 참조 하세요 [포인터 산술 연산을](unsafe-code.md#pointer-arithmetic).

예제

```csharp
class Test
{
    static void Main() {
        unsafe {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) p[i] = (char)i;
        }
    }
}
```

포인터 요소 액세스는 초기화 하는 데에 문자 버퍼를 `for` 루프입니다. 때문에 작업이 `P[E]` 정확 하 게 해당 하는 `*(P + E)`, 예제도 동일 하 게 작성 될 수도:

```csharp
class Test
{
    static void Main() {
        unsafe {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) *(p + i) = (char)i;
        }
    }
}
```

에 대 한 포인터 요소 액세스 연산자에 대 한 범위를 벗어나는 확인 하지 오류 및 동작에 액세스 하는 경우는 범위를 벗어나는 요소 정의 되지 않습니다. C 및 c + +와 같습니다.

### <a name="the-address-of-operator"></a>Address-of 연산자

*addressof_expression* 앰퍼샌드 이루어져 있습니다 (`&`) 뒤에 *unary_expression*합니다.

```antlr
addressof_expression
    : '&' unary_expression
    ;
```

식에 지정 되었습니다 `E` 는 형식인 `T` 와 고정 변수로 분류 ([고정 및 고정 되지 않은 변수](unsafe-code.md#fixed-and-moveable-variables)), 구문 `&E` 제공한변수의주소를계산`E`. 결과의 형식은 `T*` 와 값으로 분류 합니다. 컴파일 타임 오류가 발생 하는 경우 `E` 분류 되지 않은 변수를 하는 경우 `E` 읽기 전용 지역 변수로 분류 됩니다 이거나 `E` 변수인을 나타냅니다. 마지막 경우 fixed 문 ([fixed 문을](unsafe-code.md#the-fixed-statement)) 일시적으로 "수정" 변수의 해당 주소를 얻기 전에 사용할 수 있습니다. 에 명시 된 대로 [me](expressions.md#member-access), 인스턴스 생성자 또는 정적 생성자 정의 하는 클래스 또는 구조체 외부를 `readonly` 필드를 해당 필드 값을 변수가 아니라 간주 됩니다. 따라서 해당 주소를 가져올 수 없습니다. 마찬가지로, 상수의 주소를 가져올 수 없습니다.

합니다 `&` 연산자는 정적으로 할당 된 제공 되지만 다음 인수를 필요 하지 않습니다는 `&` 작업 연산자 적용 되는 변수의 작업 발생 하는 실행 경로에 정적으로 할당 된 간주 됩니다. 변수는 올바른 초기화 되도록 프로그래머의 책임 실제로 수행 되었는지이 이런 이며

예제

```csharp
using System;

class Test
{
    static void Main() {
        int i;
        unsafe {
            int* p = &i;
            *p = 123;
        }
        Console.WriteLine(i);
    }
}
```

`i` 다음 정적으로 할당 된 것으로 간주 됩니다 합니다 `&i` 초기화를 사용 하는 작업 `p`합니다. 에 대 한 할당 `*p` 초기화 적용 `i`, 하지만이 초기화 포함은 프로그래머의 책임 및 할당 제거 된 경우 컴파일 타임 오류가 발생 합니다.

규칙에 대 한 한정 된 할당에는 `&` 연산자 존재는 지역 변수 초기화 중복을 방지할 수 있습니다. 예를 들어, 대부분의 외부 Api API에 의해 채워진 구조체 포인터를 이동 합니다. 이러한 Api에 대 한 호출에는 일반적으로 로컬 구조체 변수의 주소를 전달 하 고 규칙 없이 구조체 변수의 중복 초기화 필요한 것입니다.

### <a name="pointer-increment-and-decrement"></a>포인터 증가 및 감소

안전 하지 않은 컨텍스트에서 `++` 하 고 `--` 연산자 ([후 위 증가 및 감소 연산자](expressions.md#postfix-increment-and-decrement-operators) 하 고 [전위 증가 및 감소 연산자](expressions.md#prefix-increment-and-decrement-operators)) 포인터에 적용할 수 있습니다 제외한 모든 형식의 변수 `void*`합니다. 따라서 모든 포인터 형식에 대 한 `T*`, 다음 연산자를 암시적으로 정의 됩니다.

```csharp
T* operator ++(T* x);
T* operator --(T* x);
```

연산자와 동일한 결과 생성할 `x + 1` 하 고 `x - 1`각각 ([포인터 산술 연산을](unsafe-code.md#pointer-arithmetic)). 형식의 포인터 변수에 대 한 다시 말해 `T*`, `++` 연산자는 추가 `sizeof(T)` 변수에 포함 된 주소로 및 `--` 연산자 뺍니다 `sizeof(T)` 변수에 포함 된 주소에서 합니다.

포인터 증가 또는 감소 하는 경우 포인터 형식의 도메인을 오버플로 하는 작업 결과 구현 정의 되지만 예외가 생성 됩니다.

### <a name="pointer-arithmetic"></a>포인터 산술 연산

안전 하지 않은 컨텍스트에서 `+` 하 고 `-` 연산자 ([더하기 연산자](expressions.md#addition-operator) 하 고 [빼기 연산자](expressions.md#subtraction-operator)) 제외 하 고 모든 포인터 형식의 값에 적용할 수 있습니다 `void*`. 따라서 모든 포인터 형식에 대 한 `T*`, 다음 연산자를 암시적으로 정의 됩니다.

```csharp
T* operator +(T* x, int y);
T* operator +(T* x, uint y);
T* operator +(T* x, long y);
T* operator +(T* x, ulong y);

T* operator +(int x, T* y);
T* operator +(uint x, T* y);
T* operator +(long x, T* y);
T* operator +(ulong x, T* y);

T* operator -(T* x, int y);
T* operator -(T* x, uint y);
T* operator -(T* x, long y);
T* operator -(T* x, ulong y);

long operator -(T* x, T* y);
```

식에 지정 되었습니다 `P` 포인터 형식의 `T*` 및 식을 `N` 형식의 `int`, `uint`를 `long`, 또는 `ulong`, 식 `P + N` 및 `N + P` 계산는 형식의 포인터 값 `T*` 결과 추가에서 나온 `N * sizeof(T)` 제공한 주소로 `P`합니다. 마찬가지로, 식이 `P - N` 형식의 포인터 값을 계산 `T*` 뺀 결과 `N * sizeof(T)` 제공한 주소에서 `P`합니다.

지정 된 두 식 `P` 하 고 `Q`, 포인터 형식의 `T*`, 식을 `P - Q` 제공한 주소 간의 차이 계산 `P` 및 `Q` 다음 차이점 나눕니다및`sizeof(T)`. 결과의 형식은 항상 `long`합니다. 사실 `P - Q` 로 계산 됩니다 `((long)(P) - (long)(Q)) / sizeof(T)`합니다.

예를 들어:

```csharp
using System;

class Test
{
    static void Main() {
        unsafe {
            int* values = stackalloc int[20];
            int* p = &values[1];
            int* q = &values[15];
            Console.WriteLine("p - q = {0}", p - q);
            Console.WriteLine("q - p = {0}", q - p);
        }
    }
}
```

출력을 생성합니다.

```
p - q = -14
q - p = 14
```

포인터 형식의 도메인을 오버플로 하는 포인터 산술 연산, 결과 구현 시 정의 된 방식으로 잘렸습니다. 되지만 예외가 생성 됩니다.

### <a name="pointer-comparison"></a>포인터 비교

안전 하지 않은 컨텍스트에서 `==`, `!=`, `<`, `>`합니다 `<=`, 및 `=>` 연산자 ([관계형 및 형식 테스트 연산자](expressions.md#relational-and-type-testing-operators)) 모든 값에 적용할 수 있습니다 포인터 형식입니다. 포인터 비교 연산자는 다음과 같습니다.

```csharp
bool operator ==(void* x, void* y);
bool operator !=(void* x, void* y);
bool operator <(void* x, void* y);
bool operator >(void* x, void* y);
bool operator <=(void* x, void* y);
bool operator >=(void* x, void* y);
```

모든 포인터 형식으로의 암시적 변환이 존재 하기 때문에 `void*` 이러한 연산자를 사용 하 여 형식에 대 한 포인터 형식의 피연산자를 비교할 수 있습니다. 비교 연산자는 부호 없는 정수 처럼 두 개의 피연산자가 제공한 주소를 비교 합니다.

### <a name="the-sizeof-operator"></a>Sizeof 연산자

`sizeof` 연산자에 지정 된 형식의 변수가 차지 하는 바이트 수를 반환 합니다. 피연산자로 지정 된 형식 `sizeof` 이어야 합니다는 *unmanaged_type* ([포인터 형식](unsafe-code.md#pointer-types)).

```antlr
sizeof_expression
    : 'sizeof' '(' unmanaged_type ')'
    ;
```

결과 `sizeof` 연산자는 형식의 값 `int`합니다. 특정 미리 정의 된 형식에는 `sizeof` 연산자는 아래 표에 나와 있는 것 처럼 상수 값을 생성 합니다.


| __식__   | __결과__ |
|------------------|------------|
| `sizeof(sbyte)`  | `1`        |
| `sizeof(byte)`   | `1`        |
| `sizeof(short)`  | `2`        |
| `sizeof(ushort)` | `2`        |
| `sizeof(int)`    | `4`        |
| `sizeof(uint)`   | `4`        |
| `sizeof(long)`   | `8`        |
| `sizeof(ulong)`  | `8`        |
| `sizeof(char)`   | `2`        |
| `sizeof(float)`  | `4`        |
| `sizeof(double)` | `8`        |
| `sizeof(bool)`   | `1`        |

다른 모든 종류의 결과 대 한는 `sizeof` 연산자는 구현 시 정의 및 상수가 아닌 값으로 분류 됩니다.

멤버가 구조체에 압축 되는 순서가 지정 되지 않습니다.

맞춤을 위해 있을 수 있습니다 하지 명명 된 구조체 내의 구조체의 시작 부분 및 구조체의 끝에 패딩 합니다. 안쪽 여백으로 비트 내용의 확정적이 지 않습니다.

구조체 형식의 피연산자에 적용 되 면 결과 안쪽 여백을 포함 하 여 해당 형식의 변수에 바이트의 총 수입니다.

## <a name="the-fixed-statement"></a>Fixed 문

안전 하지 않은 컨텍스트에서 *embedded_statement* ([문을](statements.md)) 프로덕션에는 추가 구문 허용을 `fixed` 변수인 "해결" 하는 데 사용 되는 문이 되도록 해당 주소를 문의 기간에 대 한 일정 하 게 유지 합니다.

```antlr
fixed_statement
    : 'fixed' '(' pointer_type fixed_pointer_declarators ')' embedded_statement
    ;

fixed_pointer_declarators
    : fixed_pointer_declarator (','  fixed_pointer_declarator)*
    ;

fixed_pointer_declarator
    : identifier '=' fixed_pointer_initializer
    ;

fixed_pointer_initializer
    : '&' variable_reference
    | expression
    ;
```

각 *fixed_pointer_declarator* 의 로컬 변수를 선언 하는 지정 된 *pointer_type* 해당 계산 하는 주소를 사용 하 여 해당 로컬 변수를 초기화 하 고 *fixed_ pointer_initializer*합니다. 에 선언 된 지역 변수를 `fixed` 문 하나에 액세스할 수 *fixed_pointer_initializer*가 해당 변수의 선언 오른쪽에서 발생 합니다 *embedded_statement* 의 `fixed` 문입니다. 선언 된 지역 변수는 `fixed` 문을 읽기 전용으로 간주 됩니다. 포함된 된 문을이 로컬 변수를 수정 하려고 하면 컴파일 타임 오류가 발생 (할당을 통해 또는 `++` 하 고 `--` 연산자)로 전달 하거나를 `ref` 또는 `out` 매개 변수입니다.

A *fixed_pointer_initializer* 다음 중 하나일 수 있습니다.

*  토큰 "`&`" 뒤에 *variable_reference* ([한정 된 할당을 확인 하는 것에 대 한 정확한 규칙](variables.md#precise-rules-for-determining-definite-assignment)) 고정 되지 않은 변수에 ([고정 및 고정 되지 않은 변수](unsafe-code.md#fixed-and-moveable-variables)) 관리 되지 않는 형식의 `T`, 형식 제공 `T*` 에 지정 된 포인터 형식으로 암시적으로 변환할 수는 `fixed` 문입니다. 이 경우 이니셜라이저는 지정 된 변수의 주소를 계산 하 고 변수의 기간에 대 한 고정된 주소를 유지 하도록 보장 됩니다는 `fixed` 문입니다.
*  식을 *array_type* 관리 되지 않는 형식의 요소를 사용 하 여 `T`, 형식을 제공 `T*` 에 지정 된 포인터 형식으로 암시적으로 변환할 수는 `fixed` 문. 이 경우 이니셜라이저는 배열에서 첫 번째 요소의 주소를 계산 하 고 배열 전체 기간에 대 한 고정된 주소를 유지 하도록 보장 됩니다는 `fixed` 문입니다. 배열 식이 null 인지 또는 배열에 요소가 없는 경우 이니셜라이저 주소 등호를 0으로 계산 합니다.
*  형식의 식을 `string`, 형식을 제공 `char*` 에 지정 된 포인터 형식으로 암시적으로 변환할 수는 `fixed` 문. 이 경우 이니셜라이저는 문자열에서 첫 번째 문자의 주소를 계산 하 고 전체 문자열의 기간에 대 한 고정된 주소를 유지 하도록 보장 됩니다는 `fixed` 문입니다. 동작을 `fixed` 문에 구현 시 정의 된 null 이면 문자열 식입니다.
*  A *simple_name* 하거나 *member_access* 참조 하는 고정된 크기 버퍼 소속 변수인 고정된 크기 버퍼 멤버의 형식이 지정 된 포인터 형식으로 암시적으로 변환할 제공 에 `fixed` 문입니다. 이니셜라이저는 고정된 크기 버퍼의 첫 번째 요소에 대 한 포인터를 계산 하는 예제의 경우 ([식에서 고정 크기 버퍼](unsafe-code.md#fixed-size-buffers-in-expressions)), 고정된 크기 버퍼는 기간에대한고정된주소를유지하도록보장됩니다및`fixed`문입니다.

계산 하는 각 주소에 대 한는 *fixed_pointer_initializer* 는 `fixed` 문을 사용 하면 주소로 참조 변수의 재배치 하거나 기간에 대 한 가비지 수집기에서 삭제할 아닌지는 `fixed` 문입니다. 예를 들어 주소에서 계산을 *fixed_pointer_initializer* 개체의 필드 또는 배열 인스턴스 요소의 참조는 `fixed` 문을 사용 하면 포함 된 개체 인스턴스 재배치 하지 않으면 또는 명령문의 수명 동안 삭제 합니다.

포인터에서 만들어졌는지 확인 해야 하는 프로그래머의 `fixed` 문을 이러한 문의 실행은 초과 남지 않습니다. 예를 들어 포인터 하 여 만든 경우 `fixed` 문 외부 Api에 전달 됩니다 이며 프로그래머는 Api 메모리가 없습니다. 이러한 포인터를 유지 하도록 합니다.

(이동할 수 없습니다) 하므로 고정된 개체 힙의 조각화를 발생할 수 있습니다. 이런 이유로 개체 수정 해야 반드시 필요한 경우에 차례로 돌아가도록 가능한 시간에 대해서만 합니다.

이 예제에서

```csharp
class Test
{
    static int x;
    int y;

    unsafe static void F(int* p) {
        *p = 1;
    }

    static void Main() {
        Test t = new Test();
        int[] a = new int[10];
        unsafe {
            fixed (int* p = &x) F(p);
            fixed (int* p = &t.y) F(p);
            fixed (int* p = &a[0]) F(p);
            fixed (int* p = a) F(p);
        }
    }
}
```

몇 가지 사용 방법을 보여 줍니다는 `fixed` 문입니다. 첫 번째 문을 수정 하 고 정적 필드의 주소를 가져옵니다, 두 번째 문을 수정 하 고는 인스턴스 필드의 주소를 가져옵니다 및 세 번째 문을 수정 하 고 배열 요소의 주소를 가져옵니다. 각각의 경우에서 것이 더 일반적인을 사용 하 여 `&` 연산자 이므로 변수를 모두 고정 되지 않은 변수도 분류 됩니다.

네 번째 `fixed` 위의 예에서 문은 세 비슷한 결과 생성 합니다.

이 예제는 `fixed` 문 사용 하 여 `string`:

```csharp
class Test
{
    static string name = "xx";

    unsafe static void F(char* p) {
        for (int i = 0; p[i] != '\0'; ++i)
            Console.WriteLine(p[i]);
    }

    static void Main() {
        unsafe {
            fixed (char* p = name) F(p);
            fixed (char* p = "xx") F(p);
        }
    }
}
```

안전 하지 않은 컨텍스트에서 단일 차원 배열의 배열 요소 인덱스부터 증가 인덱스 순서로 저장 됩니다 `0` 인덱스까지 `Length - 1`입니다. 다차원 배열에서 맨 오른쪽 차원의 인덱스는 먼저 증가 되도록 요소가 저장 되는 배열에 대 한 다음 다음 왼쪽 차원 등에서 왼쪽입니다. 내를 `fixed` 문에 대 한 포인터를 가져오는 `p` 배열 인스턴스에 `a`, 까지의 포인터 값 `p` 에 `p + a.Length - 1` 배열에서 요소의 주소를 나타냅니다. 범위의 변수 마찬가지로 `p[0]` 에 `p[a.Length - 1]` 실제 배열 요소를 나타냅니다. 배열 저장 되는 방식으로 지정 되 면에서는 선형 것 처럼 모든 차원 배열을 처리할 수 있습니다.

예를 들어:

```csharp
using System;

class Test
{
    static void Main() {
        int[,,] a = new int[2,3,4];
        unsafe {
            fixed (int* p = a) {
                for (int i = 0; i < a.Length; ++i)    // treat as linear
                    p[i] = i;
            }
        }

        for (int i = 0; i < 2; ++i)
            for (int j = 0; j < 3; ++j) {
                for (int k = 0; k < 4; ++k)
                    Console.Write("[{0},{1},{2}] = {3,2} ", i, j, k, a[i,j,k]);
                Console.WriteLine();
            }
    }
}
```

출력을 생성합니다.

```
[0,0,0] =  0 [0,0,1] =  1 [0,0,2] =  2 [0,0,3] =  3
[0,1,0] =  4 [0,1,1] =  5 [0,1,2] =  6 [0,1,3] =  7
[0,2,0] =  8 [0,2,1] =  9 [0,2,2] = 10 [0,2,3] = 11
[1,0,0] = 12 [1,0,1] = 13 [1,0,2] = 14 [1,0,3] = 15
[1,1,0] = 16 [1,1,1] = 17 [1,1,2] = 18 [1,1,3] = 19
[1,2,0] = 20 [1,2,1] = 21 [1,2,2] = 22 [1,2,3] = 23
```

예제

```csharp
class Test
{
    unsafe static void Fill(int* p, int count, int value) {
        for (; count != 0; count--) *p++ = value;
    }

    static void Main() {
        int[] a = new int[100];
        unsafe {
            fixed (int* p = a) Fill(p, 100, -1);
        }
    }
}
```

`fixed` 해당 주소에 대 한 포인터를 사용 하는 메서드에 전달할 수 있도록 배열을 수정 문을 사용 합니다.

예제:

```csharp
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}

class Test
{
    unsafe static void PutString(string s, char* buffer, int bufSize) {
        int len = s.Length;
        if (len > bufSize) len = bufSize;
        for (int i = 0; i < len; i++) buffer[i] = s[i];
        for (int i = len; i < bufSize; i++) buffer[i] = (char)0;
    }

    Font f;

    unsafe static void Main()
    {
        Test test = new Test();
        test.f.size = 10;
        fixed (char* p = test.f.name) {
            PutString("Times New Roman", p, 32);
        }
    }
}
```

fixed 문에 대 한 포인터로 해당 주소를 사용할 수 있도록 고정된 크기 버퍼는 구조체의 해결 됩니다.

`char*` 문자열 인스턴스를 null로 끝나는 문자열을 가리키는 항상 수정 하 여 생성 된 값입니다. Fixed 문에 대 한 포인터를 가져오는 내 `p` 문자열 인스턴스로 `s`, 까지의 포인터 값 `p` 에 `p + s.Length - 1` 문자열과 포인터 값에 있는 문자의 주소를 나타냅니다 `p + s.Length` 항상 null 문자를 가리키는 (값을 갖는 문자 `'\0'`).

정의 되지 않은 동작이 발생할 수 있습니다. 고정된 포인터를 통해 관리 되는 형식의 개체를 수정 합니다. 예를 들어, 문자열을 변경할 수 없기 때문에 고정된 문자열에 대 한 포인터에서 참조 하는 문자는 수정 되지 않습니다 있도록 프로그래머의 몫입니다.

문자열의 자동 null 종료 "C-스타일" 문자열을 필요로 하는 외부 Api를 호출 하는 경우에 특히 유용 합니다. 그러나 문자열 인스턴스는 null 문자를 포함 하도록 허용 하는 합니다. 이러한 null 문자가 있는 경우 문자열은 잘린 상태로 나타날 null로 끝나는 취급 하는 경우 `char*`합니다.

## <a name="fixed-size-buffers"></a>고정된 크기 버퍼

고정된 크기 버퍼 "C 스타일" 인라인 배열을 구조체의 멤버로 선언 하는 데 사용 되 고 관리 되지 않는 Api와의 상호 작용에 주로 유용 합니다.

### <a name="fixed-size-buffer-declarations"></a>고정된 크기 버퍼 선언

A ***고정 크기 버퍼*** 는 지정 된 형식의 변수는 고정된 길이 버퍼에 대 한 저장소를 나타내는 멤버입니다. 고정된 크기 버퍼 선언에서는 지정 된 요소 형식의 하나 이상의 고정된 크기 버퍼를 소개합니다. 고정된 크기 버퍼는 구조체 선언 에서만 허용 됩니다 하 고 안전 하지 않은 컨텍스트에서 에서만 발생할 수 있습니다 ([안전 하지 않은 컨텍스트](unsafe-code.md#unsafe-contexts)).

```antlr
struct_member_declaration_unsafe
    : fixed_size_buffer_declaration
    ;

fixed_size_buffer_declaration
    : attributes? fixed_size_buffer_modifier* 'fixed' buffer_element_type fixed_size_buffer_declarator+ ';'
    ;

fixed_size_buffer_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'unsafe'
    ;

buffer_element_type
    : type
    ;

fixed_size_buffer_declarator
    : identifier '[' constant_expression ']'
    ;
```

고정된 크기 버퍼 선언 특성 집합이 포함 될 수 있습니다 ([특성](attributes.md)), `new` 한정자 ([한정자](classes.md#modifiers)), 네 가지 액세스 한정자의 유효한 조합이 ([형식 매개 변수 및 제약 조건](classes.md#type-parameters-and-constraints)) 및 `unsafe` 한정자 ([안전 하지 않은 컨텍스트](unsafe-code.md#unsafe-contexts)). 특성 및 한정자 모든 고정된 크기 버퍼 선언에서 선언 된 멤버에 적용 됩니다. 이를 여러 번 고정된 크기 버퍼 선언에서 동일한 한정자에 대 한 오류입니다.

고정된 크기 버퍼 선언 포함 하도록 허용 되지 않습니다는 `static` 한정자입니다.

고정된 크기 버퍼 선언의 버퍼 요소 형식 선언에 의해 도입 된 버퍼의 요소 형식 지정 합니다. 버퍼 요소 형식 미리 정의 된 형식 중 하나 여야 `sbyte`, `byte`, `short`, `ushort`, `int`를 `uint`, `long`, `ulong`, `char`, `float`를 `double`, 또는 `bool`합니다.

버퍼 요소 형식 새 멤버를 소개 하는 각 고정된 크기 버퍼 선언 자 목록이 나옵니다. 고정된 크기 버퍼 선언 자 뒤에 묶인 상수 식을 사용 하 여 멤버의 이름을 지정 하는 식별자 이루어져 `[` 고 `]` 토큰입니다. 상수 식은 해당 고정된 크기 버퍼 선언 자에 의해 정의 된 멤버의 요소 수를 나타냅니다. 상수 식의 형식은 형식으로 암시적으로 변환할 수 있어야 합니다 `int`, 값 0이 아닌 양의 정수 여야 합니다.

고정된 크기 버퍼의 요소는 메모리에서 순차적으로 배치 보장 됩니다.

고정된 크기 버퍼를 여러 개 선언 하는 고정된 크기 버퍼 선언은 요소 형식과 동일한 특성을 사용 하는 단일 고정된 크기 버퍼 선언이 여러 번 선언 하는 것과 같습니다. 예

```csharp
unsafe struct A
{
   public fixed int x[5], y[10], z[100];
}
```

위의 식은 아래의 식과 동일합니다.

```csharp
unsafe struct A
{
   public fixed int x[5];
   public fixed int y[10];
   public fixed int z[100];
}
```

### <a name="fixed-size-buffers-in-expressions"></a>식에서 고정된 크기 버퍼

멤버 조회 ([연산자](expressions.md#operators)) 고정된 된 크기의 버퍼 멤버 필드의 멤버 조회와 동일 하 게 진행 합니다.

고정된 크기 버퍼를 사용 하는 식에서 참조할 수는 *simple_name* ([형식 유추](expressions.md#type-inference)) 또는 *member_access* ([컴파일 타임 검사 동적 오버 로드 확인](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).

고정된 크기 버퍼 멤버는 단순한 이름으로 참조 되는 경우는 효과가 동일 형식의 멤버 액세스로 `this.I`여기서 `I` 고정된 크기 버퍼 멤버입니다.

형식의 멤버 액세스에서 `E.I`이면 `E` 구조체 형식 및 멤버 조회입니다 `I` 구조체 형식 하 게 식별 하는 고정된 크기 멤버 다음에 `E.I` 는 분류는 다음과 같이 계산:

*  경우 식 `E.I` 컴파일 타임 오류가 발생 하는 안전 하지 않은 컨텍스트에서 발생 하지 않습니다.
*  경우 `E` 컴파일 타임 오류가 발생 하는 값으로 분류 됩니다.
*  그렇지 않고 `E` 변수인은 ([고정 및 고정 되지 않은 변수](unsafe-code.md#fixed-and-moveable-variables)) 및 식 `E.I` 아닙니다를 *fixed_pointer_initializer* ([고정 문을](unsafe-code.md#the-fixed-statement)), 컴파일 시간 오류가 발생 합니다.
*  이 고, 그렇지 `E` 고정된 변수 참조 식의 결과 고정된 크기 버퍼 멤버의 첫 번째 요소에 대 한 포인터 `I` 에서 `E`합니다. 결과 형식입니다 `S*`, 여기서 `S` 의 요소 형식인 `I`와 값으로 분류 합니다.

고정된 크기 버퍼의 후속 요소는 첫 번째 요소에서 포인터 연산을 사용 하 여 액세스할 수 있습니다. 배열에 대 한 액세스를 달리 고정된 크기 버퍼의 요소에 대 한 액세스는 안전 하지 않은 작업이 며 선택 범위가 아닙니다.

다음 예제에서는 선언 하 고 고정된 크기 버퍼 멤버와 구조체를 사용 합니다.

```csharp
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}

class Test
{
    unsafe static void PutString(string s, char* buffer, int bufSize) {
        int len = s.Length;
        if (len > bufSize) len = bufSize;
        for (int i = 0; i < len; i++) buffer[i] = s[i];
        for (int i = len; i < bufSize; i++) buffer[i] = (char)0;
    }

    unsafe static void Main()
    {
        Font f;
        f.size = 10;
        PutString("Times New Roman", f.name, 32);
    }
}
```

### <a name="definite-assignment-checking"></a>한정 된 할당 검사

고정된 크기 버퍼는 한정 된 할당을 확인 하는 적용 되지 않습니다 ([한정 된 할당](variables.md#definite-assignment)), 고정된 크기 버퍼 멤버는 구조체 형식 변수를 검사 하는 한정 된 할당의 목적을 위해 무시 됩니다.

고정된 크기 버퍼 멤버의 포함 된 가장 바깥쪽 구조체 변수 정적 변수, 배열 요소 또는 클래스 인스턴스를 인스턴스 변수 경우 고정된 크기 버퍼의 요소는 자동으로 기본값으로 초기화 됩니다 ([기본값](variables.md#default-values)). 다른 모든 경우에는 고정된 크기 버퍼의 초기 콘텐츠 정의 되지 않습니다.

## <a name="stack-allocation"></a>스택 할당

안전 하지 않은 컨텍스트에서 지역 변수 선언 ([지역 변수 선언](statements.md#local-variable-declarations)) 호출 스택에서 메모리를 할당 하는 스택 할당 이니셜라이저를 포함할 수 있습니다.

```antlr
local_variable_initializer_unsafe
    : stackalloc_initializer
    ;

stackalloc_initializer
    : 'stackalloc' unmanaged_type '[' expression ']'
    ;
```

합니다 *unmanaged_type* 새로 할당 된 위치에 저장할 항목의 형식을 나타내는 하며 *식* 이러한 항목의 수를 나타냅니다. 필요한 할당 크기를 지정 전체적으로 볼 때, 이러한 합니다. 이기 때문에 스택 할당의 크기는 음수일 수 없습니다, 항목의 수를 지정 하는 컴파일 시간 오류를 *constant_expression* 음수 값으로 계산 되는 합니다.

폼의 스택 할당 이니셜라이저 `stackalloc T[E]` 필요 `T` 는 관리 되지 않는 형식 ([포인터 형식](unsafe-code.md#pointer-types)) 및 `E` 형식의 식으로 `int`입니다. 할당 구문을 `E * sizeof(T)` 호출에서 바이트 스택 및 형식의 포인터를 반환 `T*`, 새로 할당 된 블록입니다. 경우 `E` 음수 값 이면 동작이 정의 되지 않습니다. 경우 `E` 가 0 이면 할당이 없습니다를 수행 하 고 반환 된 포인터는 구현 시 정의 합니다. 지정된 된 크기의 블록을 할당할 수 있는 충분 한 메모리가 없을 경우는 `System.StackOverflowException` throw 됩니다.

새로 할당 된 메모리의 내용을 정의 되지 않습니다.

스택 할당 이니셜라이저에 허용 되지 않는 `catch` 나 `finally` 블록 ([try 문](statements.md#the-try-statement)).

명시적으로 사용 하 여 할당 된 메모리를 해제할 방법이 없기 `stackalloc`합니다. 함수 멤버의 실행 중에 만들어진 모든 스택 할당 된 메모리 블록은 해당 하는 함수 멤버는 반환 될 때 자동으로 삭제 됩니다. 이에 해당 합니다 `alloca` 함수, C 및 c + + 구현에서 흔히 발견 되는 확장 합니다.

예제

```csharp
using System;

class Test
{
    static string IntToString(int value) {
        int n = value >= 0? value: -value;
        unsafe {
            char* buffer = stackalloc char[16];
            char* p = buffer + 16;
            do {
                *--p = (char)(n % 10 + '0');
                n /= 10;
            } while (n != 0);
            if (value < 0) *--p = '-';
            return new string(p, 0, (int)(buffer + 16 - p));
        }
    }

    static void Main() {
        Console.WriteLine(IntToString(12345));
        Console.WriteLine(IntToString(-999));
    }
}
```

`stackalloc` 이니셜라이저에 사용 되는 `IntToString` 스택에 16 자 버퍼를 할당 하는 방법. 버퍼의 메서드가 반환 될 때 자동으로 삭제 됩니다.

## <a name="dynamic-memory-allocation"></a>동적 메모리 할당

제외 하 고는 `stackalloc` 아닌 가비지 수집 된 메모리를 관리 하기 위한 미리 정의 된 구문은 없습니다 연산자, C# 제공 합니다. 이러한 서비스는 일반적으로 클래스 라이브러리를 지원 하 여 제공 하거나 기본 운영 체제에서 직접 가져온 됩니다. 예를 들어는 `Memory` 아래 클래스 C#에서 기본 운영 체제의 힙 함수를 어떻게 액세스할 수 있는지 보여 줍니다.

```csharp
using System;
using System.Runtime.InteropServices;

public unsafe class Memory
{
    // Handle for the process heap. This handle is used in all calls to the
    // HeapXXX APIs in the methods below.
    static int ph = GetProcessHeap();

    // Private instance constructor to prevent instantiation.
    private Memory() {}

    // Allocates a memory block of the given size. The allocated memory is
    // automatically initialized to zero.
    public static void* Alloc(int size) {
        void* result = HeapAlloc(ph, HEAP_ZERO_MEMORY, size);
        if (result == null) throw new OutOfMemoryException();
        return result;
    }

    // Copies count bytes from src to dst. The source and destination
    // blocks are permitted to overlap.
    public static void Copy(void* src, void* dst, int count) {
        byte* ps = (byte*)src;
        byte* pd = (byte*)dst;
        if (ps > pd) {
            for (; count != 0; count--) *pd++ = *ps++;
        }
        else if (ps < pd) {
            for (ps += count, pd += count; count != 0; count--) *--pd = *--ps;
        }
    }

    // Frees a memory block.
    public static void Free(void* block) {
        if (!HeapFree(ph, 0, block)) throw new InvalidOperationException();
    }

    // Re-allocates a memory block. If the reallocation request is for a
    // larger size, the additional region of memory is automatically
    // initialized to zero.
    public static void* ReAlloc(void* block, int size) {
        void* result = HeapReAlloc(ph, HEAP_ZERO_MEMORY, block, size);
        if (result == null) throw new OutOfMemoryException();
        return result;
    }

    // Returns the size of a memory block.
    public static int SizeOf(void* block) {
        int result = HeapSize(ph, 0, block);
        if (result == -1) throw new InvalidOperationException();
        return result;
    }

    // Heap API flags
    const int HEAP_ZERO_MEMORY = 0x00000008;

    // Heap API functions
    [DllImport("kernel32")]
    static extern int GetProcessHeap();

    [DllImport("kernel32")]
    static extern void* HeapAlloc(int hHeap, int flags, int size);

    [DllImport("kernel32")]
    static extern bool HeapFree(int hHeap, int flags, void* block);

    [DllImport("kernel32")]
    static extern void* HeapReAlloc(int hHeap, int flags, void* block, int size);

    [DllImport("kernel32")]
    static extern int HeapSize(int hHeap, int flags, void* block);
}
```

사용 하는 예제는 `Memory` 클래스는 아래에 나와 있습니다.

```csharp
class Test
{
    static void Main() {
        unsafe {
            byte* buffer = (byte*)Memory.Alloc(256);
            try {
                for (int i = 0; i < 256; i++) buffer[i] = (byte)i;
                byte[] array = new byte[256];
                fixed (byte* p = array) Memory.Copy(buffer, p, 256); 
            }
            finally {
                Memory.Free(buffer);
            }
            for (int i = 0; i < 256; i++) Console.WriteLine(array[i]);
        }
    }
}
```

이 예제에서는 할당을 통해 메모리의 256 바이트 `Memory.Alloc` 0에서 255 개로 증가 하는 값을 사용 하 여 메모리 블록을 초기화 합니다. 그런 다음 요소 256 바이트 배열을 할당 하 고 사용 하 여 `Memory.Copy` 메모리 블록의 내용을 바이트 배열로 복사 합니다. 마지막으로, 메모리 블록을 사용 하 여 해제 됩니다 `Memory.Free` 및 바이트 배열의 내용을 콘솔에 출력 됩니다.
