# <a name="enums"></a>열거형

***열거형*** 는 고유 값 형식 ([값 형식](types.md#value-types)) 명명 된 상수 집합을 선언 하는 합니다.

이 예제에서

```csharp
enum Color
{
    Red,
    Green,
    Blue
}
```

명명 된 열거형 형식을 선언 `Color` 구성원과 `Red`를 `Green`, 및 `Blue`합니다.

## <a name="enum-declarations"></a>열거형 선언

새 열거형 형식을 선언 하는 열거형 선언 합니다. 열거형 선언 키워드로 시작 `enum`, 이름, 액세스 가능성, 기본 형식 및 열거형의 멤버를 정의 합니다.

```antlr
enum_declaration
    : attributes? enum_modifier* 'enum' identifier enum_base? enum_body ';'?
    ;

enum_base
    : ':' integral_type
    ;

enum_body
    : '{' enum_member_declarations? '}'
    | '{' enum_member_declarations ',' '}'
    ;
```

각 열거형 형식이 정수 계열 형식이 호출에 ***내부 형식*** 열거형 형식입니다. 이 기본 형식은 열거형에 정의 된 모든 열거자 값을 나타내는 수 있어야 합니다. 열거형 선언의 내부 형식을 명시적으로 선언할 수 있습니다 `byte`, `sbyte`, `short`, `ushort`를 `int`를 `uint`를 `long` 또는 `ulong`합니다. `char` 기본 형식으로 사용할 수 없습니다. 내부 형식은 내부 형식을 명시적으로 선언 하지 않는 열거형 선언 `int`합니다.

이 예제에서

```csharp
enum Color: long
{
    Red,
    Green,
    Blue
}
```

열거형의 내부 형식을 사용 하 여 선언 `long`합니다. 기본 형식을 사용 하는 개발자를 선택할 수 있습니다 `long`범위에 있는 값을 사용할 수 있도록 예제 에서처럼 `long` 아니라 범위의 `int`, 또는 미래에 대해이 옵션을 유지 하기 위해.

## <a name="enum-modifiers"></a>열거형 한정자

*enum_declaration* 열거형 한정자 시퀀스를 선택적으로 포함할 수 있습니다.

```antlr
enum_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    ;
```

이를 여러 번 열거형 선언에서 동일한 한정자에 대 한 컴파일 시간 오류입니다.

열거형 선언 한정자 클래스 선언의 동일한 의미를 가집니다 ([한정자를 클래스](classes.md#class-modifiers)). 단, 하는 `abstract` 및 `sealed` 한정자 열거형 선언에서 허용 되지 않습니다. 열거형 추상적일 수 없으며 파생이 허용 되지 않습니다.

## <a name="enum-members"></a>열거형 멤버

열거형 형식 선언의 본문 열거형 형식의 명명 된 상수는 0 개 이상의 열거형 멤버를 정의 합니다. 없는 두 열거형 멤버 이름이 있을 수 있습니다.

```antlr
enum_member_declarations
    : enum_member_declaration (',' enum_member_declaration)*
    ;

enum_member_declaration
    : attributes? identifier ('=' constant_expression)?
    ;
```

각 열거형 멤버에는 연결 된 상수 값입니다. 이 값의 형식은 포함 하는 열거형의 내부 형식입니다. 각 열거형 멤버에 대 한 상수 값을 열거형에 대 한 기본 형식의 범위에 있어야 합니다. 이 예제에서

```csharp
enum Color: uint
{
    Red = -1,
    Green = -2,
    Blue = -3
}
```

때문에 컴파일 타임 오류가 발생 상수 값 `-1`, `-2`, 및 `-3` 기본 정수 계열 형식의 범위에 있지 않은 `uint`합니다.

여러 열거형 멤버와 연결된 된 동일한 값을 공유할 수 있습니다. 이 예제에서

```csharp
enum Color 
{
    Red,
    Green,
    Blue,

    Max = Blue
}
```

-두 열거형 멤버의 열거형을 보여 줍니다 `Blue` 고 `Max` -동일한 연결 된 값입니다.

열거형 멤버의 관련된 값에는 암시적 또는 명시적으로 할당 됩니다. 열거형 멤버의 선언에는 *constant_expression* 이니셜라이저, 열거형의 내부 형식으로 암시적으로 변환 하는 상수 식의 값을 열거형 멤버의 관련된 값입니다. 열거형 멤버의 선언에 이니셜라이저가 없기를 다음과 같이 암시적으로 연결 된 값이 설정 됩니다.

*  열거형 멤버는 열거형 형식에 선언 된 첫 번째 열거형 멤버를 해당 연결 된 값은 0입니다.
*  이 고, 그렇지 씩 더한 이전 열거형 멤버의 관련된 값을 늘려 열거형 멤버의 관련된 값을 가져옵니다. 이 값은 기본 형식으로 나타낼 수 있는 값의 범위 내에 있어야 합니다. 그렇지 않으면 컴파일 타임 오류가 발생 합니다.

이 예제에서

```csharp
using System;

enum Color
{
    Red,
    Green = 10,
    Blue
}

class Test
{
    static void Main() {
        Console.WriteLine(StringFromColor(Color.Red));
        Console.WriteLine(StringFromColor(Color.Green));
        Console.WriteLine(StringFromColor(Color.Blue));
    }

    static string StringFromColor(Color c) {
        switch (c) {
            case Color.Red: 
                return String.Format("Red = {0}", (int) c);

            case Color.Green:
                return String.Format("Green = {0}", (int) c);

            case Color.Blue:
                return String.Format("Blue = {0}", (int) c);

            default:
                return "Invalid color";
        }
    }
}
```

열거형 멤버 이름 및 연결 된 값을 출력 합니다. 출력은 다음과 같습니다.

```
Red = 0
Green = 10
Blue = 11
```

다음과 같은 이유로:

*  열거형 멤버 `Red` 값 0 (하므로 이니셜라이저가 없기는 첫 번째 열거형 멤버)를 자동으로 할당 됩니다
*  열거형 멤버 `Green` 값을 명시적으로 부여 됩니다 `10`;
*  열거형 멤버가 `Blue` 텍스트가 앞에 오는 멤버 보다 하나 더 큰 값을 자동으로 할당 됩니다.

열거형 멤버의 관련된 값 않을 직접 또는 간접적으로 자체 연관 된 열거형 멤버의 값을 사용 합니다. 이러한 순환 제한과 열거형 멤버 이니셜라이저가 임의로 텍스트 위치에 관계 없이 다른 열거형 멤버 이니셜라이저를 참조할 수 있습니다. 다른 열거형 멤버 값의 열거형 멤버 이니셜라이저 내에서 항상 다른 열거형 멤버를 참조할 때 캐스트는 필요 없습니다 있도록 해당 내부 형식의 형식으로 처리 됩니다.

이 예제에서

```csharp
enum Circular
{
    A = B,
    B
}
```

때문에 컴파일 타임 오류가 발생 선언을 `A` 고 `B` 순환 됩니다. `A` 에 따라 달라 집니다 `B` 명시적으로 및 `B` 에 따라 달라 집니다 `A` 암시적으로 합니다.

열거형 멤버 명명 되 고 클래스 내의 필드와 거의 비슷한 방식으로 범위가 지정 됩니다. 열거형 멤버의 범위에 포함 된 열거형 형식의 본문입니다. 해당 범위 내에서 간단한 이름으로 열거형 멤버를 참조할 수 있습니다. 다른 모든 코드에서 열거형 멤버의 이름은 해당 열거형 형식의 이름으로 한정 되어야 합니다. 열거형 멤버는 선언 된 접근성 없는-열거형 멤버를 포함 하는 열거형 형식에 액세스할 수 있는 경우에 액세스할 수 있습니다.

## <a name="the-systemenum-type"></a>System.Enum 형식

형식 `System.Enum` 는 모든 열거형 형식 (이 distinct 및 열거형 형식의 기본 형식에서 다른)의 추상 기본 클래스에서 상속 된 멤버 및 `System.Enum` 모든 열거형 형식에서 사용할 수 있습니다. Boxing 변환 ([Boxing 변환](types.md#boxing-conversions)) 모든 열거형 형식에서 존재 `System.Enum`, 및 unboxing 변환 ([Unboxing 변환](types.md#unboxing-conversions))에서 존재 `System.Enum` 모든 열거형 형식입니다.

사실은 `System.Enum` 자체는 *enum_type*합니다. 아니라는 것을 *class_type* 모든에서 *enum_type*가 파생 됩니다. 형식 `System.Enum` 형식에서 상속 `System.ValueType` ([The System.ValueType 형식](types.md#the-systemvaluetype-type))는 형식에서 상속 `object`합니다. 런타임 형식의 값에 `System.Enum` 수 `null` 또는 열거형 형식의 boxed 값에 대 한 참조입니다.

## <a name="enum-values-and-operations"></a>열거형 값 및 작업

각 열거형 형식이 고유 형식을; 정의 명시적 열거형 변환은 ([명시적 열거형 변환](conversions.md#explicit-enumeration-conversions)) 열거형 형식 및 정수 계열 형식 간에 또는 두 열거형 형식 간에 변환 하는 데 필요한 합니다. 열거형 형식에 사용할 수 있는 값의 집합은은 열거형 멤버에 제한 되지 않습니다. 특히, 열거형의 기본 형식의 모든 값은 열거형 형식으로 캐스팅 될 수 이며 해당 열거형의 유효한 고유 값입니다.

열거형 멤버 형식이 포함 하는 열거형 형식 (다른 열거형 멤버 이니셜라이저 내: 참조 [열거형 멤버](enums.md#enum-members)). 열거형 형식에 선언 된 열거형 멤버의 값 `E` 연관 된 값을 사용 하 여 `v` 는 `(E)v`합니다.

열거형 형식의 값에서 다음 연산자를 사용할 수 있습니다: `==`, `!=`, `<`, `>`, `<=`, `>=` ([열거형 비교 연산자](expressions.md#enumeration-comparison-operators)), 이진 `+` ([더하기 연산자](expressions.md#addition-operator)), 이진 `-` ([빼기 연산자](expressions.md#subtraction-operator)), `^`를 `&`를 `|` ([논리 열거형 연산자](expressions.md#enumeration-logical-operators)), `~` ([비트 보수 연산자](expressions.md#bitwise-complement-operator)), `++` 하 고 `--` ([후 위 증가 및 감소 연산자](expressions.md#postfix-increment-and-decrement-operators) 하고[ 전위 증가 및 감소 연산자](expressions.md#prefix-increment-and-decrement-operators)).

모든 열거형 형식 클래스에서 자동으로 파생 `System.Enum` (,에서 파생 `System.ValueType` 및 `object`). 따라서 열거형 형식의 값에이 클래스의 상속 된 메서드 및 속성을 사용할 수 있습니다.
