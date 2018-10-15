# <a name="types"></a>유형

C# 언어 형식의 두 가지 주요 범주로 구분 됩니다. ***값 형식*** 및 ***형식을 참조***합니다. 값 형식과 참조 형식 둘 다를 수 있습니다 ***제네릭 형식***에 하나를 수행 하는 ***매개 변수 입력***합니다. 형식 매개 변수는 모두 값 형식을 지정 하 고 형식을 참조할 수 있습니다.

```antlr
type
    : value_type
    | reference_type
    | type_parameter
    | type_unsafe
    ;
```

포인터 형식의 마지막 범주는 안전 하지 않은 코드 에서만 사용할 수 있습니다. 설명에 대 한 자세한 [포인터 형식](unsafe-code.md#pointer-types)합니다.

값 형식이 다른 참조 형식에서 값 형식의 변수에 직접 해당 데이터를 포함 하 변수 참조의 저장소 형식을 반면 ***참조가*** 해당 데이터에 라고도 함 ***개체***. 참조 형식에 두 가지 변수가 같은 개체를 참조 하 고 수 있으므로 작업이 다른 변수에서 참조 하는 개체에 적용할 한 변수에 대 한 것입니다. 값 형식에서는 각 변수에 데이터의 자체 사본이 이므로 작업이 다른 영향을 미칠 수 있습니다.

C#의 형식 시스템은 모든 형식의 값 개체로 처리할 수 있도록 통합 됩니다. C#의 모든 형식은 `object` 클래스 형식에서 직접 또는 간접적으로 파생되고 `object`는 모든 형식의 기본 클래스입니다. 참조 형식의 값은 `object`로 인식함으로써 간단히 개체로 처리됩니다. 값 형식의 boxing 및 unboxing 연산을 수행 하 여 개체로 처리 됩니다 ([Boxing 및 unboxing](types.md#boxing-and-unboxing)).

## <a name="value-types"></a>값 형식

값 형식은 구조체 형식 또는 열거형 형식입니다. C# 이라는 미리 정의 된 구조체 형식의 집합을 제공 합니다 ***단순 형식***합니다. 단순 형식 예약 된 키워드를 통해 식별 됩니다.

```antlr
value_type
    : struct_type
    | enum_type
    ;

struct_type
    : type_name
    | simple_type
    | nullable_type
    ;

simple_type
    : numeric_type
    | 'bool'
    ;

numeric_type
    : integral_type
    | floating_point_type
    | 'decimal'
    ;

integral_type
    : 'sbyte'
    | 'byte'
    | 'short'
    | 'ushort'
    | 'int'
    | 'uint'
    | 'long'
    | 'ulong'
    | 'char'
    ;

floating_point_type
    : 'float'
    | 'double'
    ;

nullable_type
    : non_nullable_value_type '?'
    ;

non_nullable_value_type
    : type
    ;

enum_type
    : type_name
    ;
```

참조 형식의 변수와 달리 값 형식 변수에 값을 포함할 수 `null` 값 형식이 nullable 형식인 경우에 합니다.  모든 null이 아닌 값 형식에 대 한는 값을 더한 값의 동일한 집합을 나타내는 해당 nullable 값 형식 `null`합니다.

값 형식의 변수에 할당 되 고 할당 된 값의 복사본을 만듭니다. 이 참조 하지만 참조에 의해 식별 된 개체를 복사 하는 참조 형식의 변수에 할당에서 서로 다릅니다.

### <a name="the-systemvaluetype-type"></a>System.ValueType 형식

클래스에서 암시적으로 상속 된 모든 값 형식 `System.ValueType`는 클래스에서 상속 `object`합니다. 값 형식에서 파생 되는 모든 형식에 대 한 불가능 하 고 값 형식은 암시적으로 봉인 되므로 됩니다 ([클래스를 봉인](classes.md#sealed-classes)).

사실은 `System.ValueType` 자체는 *value_type*합니다. 아니라는 것을 *class_type* 모든에서 *value_type*가 자동으로 파생 됩니다.

### <a name="default-constructors"></a>기본 생성자

모든 값 형식 이라는 매개 변수가 없는 public 인스턴스 생성자를 암시적으로 선언 된 ***기본 생성자***합니다. 기본 생성자로 알려진 0으로 초기화 인스턴스를 반환 합니다 ***기본값*** 값 형식에 대 한:

*  모든 *simple_type*s, 기본값은 모두 0 비트 패턴에 의해 생성 된 값:
    * 에 대 한 `sbyte`, `byte`, `short`, `ushort`를 `int`를 `uint`를 `long`, 및 `ulong`, 기본값은 `0`합니다.
    * 에 대 한 `char`, 기본값은 `'\x0000'`합니다.
    * 에 대 한 `float`, 기본값은 `0.0f`합니다.
    * 에 대 한 `double`, 기본값은 `0.0d`합니다.
    * 에 대 한 `decimal`, 기본값은 `0.0m`합니다.
    * 에 대 한 `bool`, 기본값은 `false`합니다.
*  에 *enum_type* `E`, 기본값은 `0`형식으로 변환 된 `E`합니다.
*  에 대 한는 *struct_type*, 기본 값 형식 필드를 기본값으로 및 모든 참조를 모든 값 형식 필드를 설정 하 여 생성 한 값은 `null`합니다.
*  에 대 한를 *nullable_type* 기본값은 인스턴스입니다를 `HasValue` 속성이 false 및 `Value` 속성 정의 되지 않습니다. 기본값은 라고도 합니다 ***값을 null*** nullable 형식의 합니다.

사용 하 여 값 형식의 기본 생성자가 호출 하는 다른 인스턴스 생성자와 같은 `new` 연산자입니다. 효율성을 위해이 요구 사항은 없습니다 생성 생성자 호출을 구현 하는 옵션이 있습니다. 변수 아래 예에서 `i` 고 `j` 0으로 초기화 됩니다.

```csharp
class A
{
    void F() {
        int i = 0;
        int j = new int();
    }
}
```

암시적으로 모든 값 형식에 매개 변수가 없는 public 인스턴스 생성자가 되므로 구조체 형식 매개 변수가 없는 생성자의 명시적 선언을 포함할 수 없습니다. 구조체 형식 매개 변수가 있는 인스턴스 생성자를 선언할 수 있지만 ([생성자](structs.md#constructors)).

### <a name="struct-types"></a>구조체 형식

구조체 형식은 상수, 필드, 메서드, 속성, 인덱서, 연산자, 인스턴스 생성자, 정적 생성자 및 중첩 된 형식을 선언할 수 있는 값 형식입니다. 구조체 형식의 선언에 설명 되어 [구조체 선언](structs.md#struct-declarations)합니다.

### <a name="simple-types"></a>단순 형식

C# 이라는 미리 정의 된 구조체 형식의 집합을 제공 합니다 ***단순 형식***합니다. 예약 된 단어를 통해 단순 형식 식별 하지만 이러한 예약 된 단어는 미리 정의 된 구조체 형식에 대 한 별칭을 `System` 아래 표에 설명 된 대로 네임 스페이스입니다.


| __예약어__ | __별칭이 지정 된 형식__ |
|-------------------|------------------|
| `sbyte`           | `System.SByte`   | 
| `byte`            | `System.Byte`    | 
| `short`           | `System.Int16`   | 
| `ushort`          | `System.UInt16`  | 
| `int`             | `System.Int32`   | 
| `uint`            | `System.UInt32`  | 
| `long`            | `System.Int64`   | 
| `ulong`           | `System.UInt64`  | 
| `char`            | `System.Char`    | 
| `float`           | `System.Single`  | 
| `double`          | `System.Double`  | 
| `bool`            | `System.Boolean` | 
| `decimal`         | `System.Decimal` | 

단순 형식의 구조체 형식 별칭을 하기 때문에 모든 단순 형식에 멤버가 있습니다. 예를 들어 `int` 에 선언 된 멤버가 `System.Int32` 에서 상속 된 멤버 `System.Object`, 및 다음 문이 허용 됩니다.

```csharp
int i = int.MaxValue;           // System.Int32.MaxValue constant
string s = i.ToString();        // System.Int32.ToString() instance method
string t = 123.ToString();      // System.Int32.ToString() instance method
```

단순 형식 특정 추가 작업을 허용 하는 다른 구조체 형식에서 다릅니다.

*  작성 하 여 만들려는 값을 허용 하는 대부분의 간단한 형식 *리터럴* ([리터럴](lexical-structure.md#literals)). 예를 들어 `123` 는 형식 리터럴 `int` 하 고 `'a'` 형식의 리터럴입니다 `char`합니다. C# 구조체 형식의 리터럴에 대 한 규정이 없습니다 일반적으로 만들고 궁극적으로 다른 구조체 형식의 기본이 아닌 값은 해당 구조체 형식의 인스턴스 생성자를 통해 항상 만들어집니다.
*  식의 피연산자가 모두 단순 형식 상수인 경우 컴파일러가 컴파일 시간 식 평가 하려면 가능성이 있습니다. 이러한 식은 라고 한 *constant_expression* ([상수 식](expressions.md#constant-expressions)). 다른 구조체 형식으로 정의 된 연산자를 사용 하는 식은 상수 식 이어야 하는 간주 되지 않습니다.
*  통해 `const` 단순 형식의 상수를 선언할 수는 선언 ([상수](classes.md#constants)). 다른 구조체 형식의 상수를 가질 수 되지 않지만에서 비슷한 효과 제공 하는 `static readonly` 필드입니다.
*  사용자 정의 변환 연산자는 다른 사용자 정의 연산자의 평가에 사용 될 수 있지만 단순 형식을 포함 하는 변환 다른 구조체 형식으로 정의 하는 변환 연산자의 계산에 참여할 수 있습니다 ([평가 사용자 정의 변환은](conversions.md#evaluation-of-user-defined-conversions)).

### <a name="integral-types"></a>정수 계열 형식 표

C# 9 개 정수 계열 형식 지원: `sbyte`, `byte`, `short`, `ushort`를 `int`를 `uint`, `long`를 `ulong`, 및 `char`합니다. 정수 계열 형식에 다음 크기 및 값의 범위

*  `sbyte` 부호 있는-128과 127 사이의 값을 가진 8 비트 정수 형식을 나타냅니다.
*  `byte` 형식은 0에서 255 사이의 값을 가진 부호 없는 8 비트 정수를 나타냅니다.
*  `short` 부호 있는-32768과 32767 사이의 값을 가진 16 비트 정수 형식을 나타냅니다.
*  `ushort` 형식은 0에서 65535 사이의 값을 가진 부호 없는 16 비트 정수를 나타냅니다.
*  `int` 부호 있는-2147483648에서 2147483647 사이의 값을 사용 하 여 32 비트 정수 형식을 나타냅니다.
*  `uint` 형식은 0에서 4294967295 사이의 값을 가진 부호 없는 32 비트 정수를 나타냅니다.
*  `long` 부호 있는-9223372036854775808과 9223372036854775807 사이의 값을 가진 64 비트 정수 형식을 나타냅니다.
*  `ulong` 형식은 0과 18446744073709551615 사이의 값을 가진 부호 없는 64 비트 정수를 나타냅니다.
*  `char` 형식은 0에서 65535 사이의 값을 가진 부호 없는 16 비트 정수를 나타냅니다. 가능한 값 집합을 `char` 형식은 유니코드 문자 집합에 해당 합니다. 하지만 `char` 동일한 표현 `ushort`를 다른 형식에서 허용 하는 모든 작업은 허용 합니다.

정수 계열 형식의 단항 및 이항 연산자는 항상 부호 있는 32 비트 전체 자릿수, 부호 없는 32 비트 전체 자릿수, 부호 있는 64 비트 정밀도 또는 부호 없는 64 비트 정밀도 사용 하 여 작동 합니다.

*  단항 `+` 하 고 `~` 연산자는 피연산자 형식으로 변환 됩니다 `T`여기서 `T` 중 첫 번째 `int`, `uint`, `long`, 및 `ulong` 모두 완벽 하 게 나타낼 수 있는 피연산자의 가능한 값입니다. 작업 형식의 전체 자릿수를 사용 하 여 수행 됩니다 `T`, 고 결과의 형식은 `T`합니다.
*  단항 `-` 연산자가 피연산자 형식으로 변환 됩니다 `T`여기서 `T` 의 첫 번째 `int` 고 `long` 피연산자의 가능한 모든 값을 완벽 하 게 나타낼 수 있는 합니다. 작업 형식의 전체 자릿수를 사용 하 여 수행 됩니다 `T`, 고 결과의 형식은 `T`합니다. 단항 `-` 형식의 피연산자에 연산자를 적용할 수 없습니다 `ulong`합니다.
*  이진 파일에 대 한 `+`, `-`, `*`, `/`, `%`를 `&`, `^`를 `|`, `==`를 `!=`, `>`, `<`, `>=`, 및 `<=` 연산자는 피연산자 형식으로 변환 됩니다 `T`, 여기서 `T` 첫 번째입니다 `int`를 `uint`를 `long`, 및 `ulong` 모든 가능한 완벽 하 게 나타낼 수 있는 두 피연산자의 값입니다. 작업 형식의 전체 자릿수를 사용 하 여 수행 됩니다 `T`, 고 결과의 형식은 `T` (또는 `bool` 관계형 연산자에 대 한). 형식으로 하나의 피연산자에 대 한 허용 되지 않습니다 `long` 형식 이어야 하 고 다른 `ulong` 이항 연산자를 사용 하 여 합니다.
*  이진 파일에 대 한 `<<` 하 고 `>>` 연산자는 왼쪽된 피연산자 형식으로 변환 됩니다 `T`여기서 `T` 중 첫 번째 `int`, `uint`, `long`, 및 `ulong` 모두 완벽 하 게 나타낼 수 있는 피연산자의 가능한 값입니다. 작업 형식의 전체 자릿수를 사용 하 여 수행 됩니다 `T`, 고 결과의 형식은 `T`합니다.

`char` 유형이 정수 계열 형식으로 분류 됩니다 있지만 두 가지 방법으로 다른 정수 계열 형식에서 달라 집니다.

*  다른 형식에서 암시적 변환은 없습니다를 `char` 형식입니다. 특히도 `sbyte`, `byte`, 및 `ushort` 형식을 사용 하 여 완벽 하 게 표현할 수 있는 값의 범위를 포함 합니다 `char` 형식에서 암시적 변환을 `sbyte`, `byte`, 또는 `ushort` 를 `char` 존재 하지 않습니다.
*  상수는 `char` 형식으로 써야 *character_literal*s 또는 *integer_literal*형식으로 캐스팅 함께에서 s `char`입니다. 예를 들어 `(char)10`은 `'\x000A'`과 같습니다.

합니다 `checked` 하 고 `unchecked` 연산자와 문을 정수 형식 산술 연산 및 변환에 오버플로 검사를 제어 하는 ([checked 및 unchecked 연산자](expressions.md#the-checked-and-unchecked-operators)). 에 `checked` 컨텍스트 오버플로 컴파일 타임 오류가 발생 또는 발생을 `System.OverflowException` throw 됩니다. 에 `unchecked` 컨텍스트에 오버플로 무시 되 고 대상 형식에 맞지 않는 상위 비트가 삭제 됩니다.

### <a name="floating-point-types"></a>부동 소수점 형식

C#에서는 두 개의 부동 소수점 형식: `float` 고 `double`입니다. 합니다 `float` 고 `double` 형식은 32 비트 단 정밀도 및 64 비트 배정밀도 IEEE 754 되는 형식 값 집합이 제공를 사용 하 여 표현 됩니다.

*  양의 0 및 음의 0입니다. 대부분의 경우, 양의 0 및 음의 0은 단순 값 0, 있지만 특정 작업의 두 구분 하는 동일 하 게 작동 ([나누기 연산자](expressions.md#division-operator)).
*  양의 무한대 및 음수 무한대입니다. 무한대는 0이 아닌 값을 0으로 나누는 것과 같은 연산에 의해 생성 됩니다. 예를 들어 `1.0 / 0.0` 양의 무한대를 생성 및 `-1.0 / 0.0` 음의 무한대를 생성 합니다.
*  합니다 ***Not 숫자 이외의*** 값을 종종 약식된 NaN입니다. 0으로 나누는 등의 잘못 된 부동 소수점 작업, nan이 생성 됩니다.
*  형식의 0이 아닌 값 집합이 유한한 `s * m * 2^e`, 여기서 `s` 이 1 또는-1 및 `m` 및 `e` 특정 부동 소수점 형식에 의해 결정 됩니다:에 대 한 `float`, `0 < m < 2^24` 및 `-149 <= e <= 104`, 한 `double`하십시오 `0 < m < 2^53` 고 `1075 <= e <= 970`입니다. 정규화 되지 않은 부동 소수점 숫자에는 유효한 0이 아닌 값으로 간주 됩니다.

합니다 `float` 형식은 약 까지의 값을 나타낼 수 있습니다 `1.5 * 10^-45` 에 `3.4 * 10^38` 7 자리의 정밀도를 사용 하 여 합니다.

합니다 `double` 형식은 약 까지의 값을 나타낼 수 있습니다 `5.0 * 10^-324` 에 `1.7 × 10^308` 15-16 자리의 정밀도를 사용 하 여 합니다.

이항 연산자의 피연산자 중 하나가 부동 소수점 형식의 경우 정수 계열 형식 또는 부동 소수점 형식에서 다른 피연산자에 있어야 합니다 및 작업을 다음과 같이 평가 됩니다.

*  피연산자 중 하나가 정수 계열 형식의 경우 해당 피연산자는 경우 다른 피연산자의 부동 소수점 형식으로 변환 됩니다.
*  그런 다음 형식의 경우 피연산자 중 하나가 `double`, 다른 피연산자가 변환 `double`, 이상을 사용 하 여 작업이 수행 됩니다 `double` 범위 및 전체 자릿수 및 결과의 형식 `double` (또는 `bool` 에 대 한 합니다 관계형 연산자)입니다.
*  그렇지 않은 경우 작업을 수행할 때 이상을 사용 하 `float` 는 범위와 전체 자릿수 및 결과의 형식을 `float` (또는 `bool` 관계형 연산자에 대 한).

대입 연산자를 포함 하 여 연산자의 부동 소수점 예외를 생성 하지 않습니다. 대신 예외적인 상황에 부동 소수점 작업의 생성 0, 무한대 또는 NaN, 아래 설명 된 대로:

*  부동 소수점 연산의 결과가 너무 작아서 대상 형식에 대 한 인 경우 작업의 결과 양의 0 또는 음의 0입니다.
*  부동 소수점 연산의 결과가 너무 커서 대상 형식에 대 한 인 경우 양의 무한대 또는 음의 무한대 연산의 결과가 됩니다.
*  부동 소수점 연산 올바르지 않으면 작업의 결과 NaN 됩니다.
*  부동 소수점 연산의 피연산자 하나 또는 둘 다 NaN 인 경우 작업의 결과 NaN 됩니다.

부동 소수점 연산 작업의 결과 형식 보다 더 높은 정밀도 사용 하 여 수행할 수 있습니다. 예를 들어 일부 하드웨어 아키텍처 지원는 "확장" 또는 "long double" 부동 소수점 형식 보다 전체 자릿수가 큰 범위와는 `double` 를 입력 하 고 암시적으로이 더 높은 정밀도 형식을 사용 하 여 모든 부동 소수점 작업을 수행 합니다. 과도 한 성능 비용만 이러한 하드웨어 아키텍처로 설정할 수 낮은 정밀도 사용 하 여 부동 소수점 작업을 수행할 수 있으며 성능 및 전체 자릿수가 모두 상실 하는 구현에 필요한 것이 아니라 C#에서는 되도록 높은 정밀도 형식 모든 부동 소수점 연산에 사용 합니다. 보다 정확한 결과 제공, 이외의 경우는 거의 없습니다 측정 가능한 영향을 주지 있습니다. 폼의 식에 있지만 `x * y / z`곱하기를 벗어나는 결과 생성 하는 위치, 합니다 `double` 범위 있지만 후속 나누기는 임시 결과를 다시는 `double` 범위에 있는 식 평가 더 높은 범위의 형식 한정 된 결과 무한를 일으킬 수 있습니다.

### <a name="the-decimal-type"></a>Decimal 형식

`decimal` 형식은 재무 및 통화 계산에 적합한 128비트 데이터 형식입니다. 합니다 `decimal` 형식은 까지의 값을 나타낼 수 있습니다 `1.0 * 10^-28` 에 약 `7.9 * 10^28` 28-29 유효 자릿수를 사용 하 여 합니다.

형식의 값 집합이 유한한 `decimal` 는 형식입니다. `(-1)^s * c * 10^-e`여기서 부호 `s` 이 0 또는 1 인 계수 `c` 를 지정 하 여 `0 <= *c* < 2^96`, 및 규모 `e` 가 되도록 `0 <= e <= 28`합니다. `decimal` 부호 있는 0이, 무한대 또는 NaN의 형식은 지원 하지 않습니다. `decimal` 10의 거듭제곱으로 조정 된 96 비트 정수로 표현 됩니다. 에 대 한 `decimal`절대값을 사용 하 여 s 보다 작은 `1.0m`, 28 자리로를 정확 하 게 되지만 더 이상 값이 있습니다. 에 대 한 `decimal`절대 값 보다 크거나 같음를 사용 하 여 s `1.0m`, 28 이나 29 자리까지 정확한 값이 있습니다. Contrary 하는 `float` 및 `double` 데이터 형식, 0.1과 같은 소수 10 진수 정확 하 게 나타낼 수 있습니다는 `decimal` 표현 합니다. 에 `float` 및 `double` 표현, 이러한 숫자는 무한 소수를 반올림 발생 가능성이 해당 표현을 만드는 오류.

형식의 경우 이항 연산자의 피연산자 중 하나가 `decimal`, 다른 피연산자는 정수 계열 형식 또는 형식 이어야 합니다. `decimal`합니다. 정수 계열 형식 피연산자가 있는 경우 변환할 `decimal` 작업을 수행 하기 전에 합니다.

형식의 값에는 작업의 결과 `decimal` (각 연산자에 대해 정의 된 대로 유지 배율) 정확한 결과 계산한 다음 표현에 맞게 반올림에서 초래 되는 합니다. 결과가 반올림 되는 표현할 수 있는 값에 가장 가까운 하 고, 결과 짝수 (이 라고 "banker rounding") 최하위 숫자 위치에 있는 값으로 표현할 수 있는 두 값이 동일 하 게 합니다. 0 개 결과 항상 0의 부호와 소수 자릿수가 0에 있습니다.

10 진수 산술 작업을 작은 값 보다 작거나 생성 되는 경우 `5 * 10^-29` 절대 값으로 작업의 결과 0이 됩니다. 경우는 `decimal` 산술 연산 결과가 너무 커서에 대 한는 `decimal` 형식으로는 `System.OverflowException` throw 됩니다.

`decimal` 형식에 더 높은 정밀도 부동 소수점 형식 보다 높지만 범위입니다. 부동 소수점 형식 변환할 때 따라서 `decimal` 오버플로 예외 및 변환에서 생성할 수 있습니다 `decimal` 부동 소수점 형식 전체 자릿수 손실이 발생할 수 있습니다. 이러한 이유로, 부동 소수점 형식 간에 암시적 변환이 존재 하 고 `decimal`, 이므로 명시적 캐스트 없이 혼합 부동 소수점 수 및 `decimal` 같은 식에서 피연산자입니다.

### <a name="the-bool-type"></a>Bool 형식

`bool` 형식은 부울 논리 값을 나타냅니다. 가능한 값 형식의 `bool` 됩니다 `true` 및 `false`합니다.

표준 변환이 없기 서로 `bool` 및 기타 형식입니다. 특히 합니다 `bool` 형식은 정수 계열 형식에서 별도 및 `bool` 그 반대로 정수 계열 값 대신 값을 사용할 수 없습니다.

C 및 c + + 언어에서 0 인 정수 계열 또는 부동 소수점 값 또는 null 포인터를 변환할 수 하는 부울 값 `false`를 0이 아닌 정수 계열 또는 부동 소수점 값 또는 null이 아닌 포인터를 부울 값으로 변환할 수 및 `true`합니다. C#에서는 명시적으로 0으로 정수 계열 또는 부동 소수점 값을 비교 하 여 또는 대 한 개체 참조를 명시적으로 비교 하 여 이러한 변환이 수행 됩니다 `null`합니다.

### <a name="enumeration-types"></a>열거형 형식

명명 된 상수를 사용 하 여 고유 형식인 열거형 형식입니다. 모든 열거형 형식 이어야 하는 내부 형식에 `byte`, `sbyte`, `short`, `ushort`를 `int`를 `uint`를 `long` 또는 `ulong`합니다. 열거형 형식의 값 집합이 기본 형식의 값 집합과 동일 합니다. 열거형 형식의 값을 명명 된 상수 값으로 제한 되지 않습니다. 열거형 형식 열거형 선언을 통해 정의 됩니다 ([열거형 선언은](enums.md#enum-declarations)).

### <a name="nullable-types"></a>Nullable 형식

Nullable 형식은 모든 값을 나타낼 수 해당 ***내부 형식*** 와 null 값을 추가 합니다. Nullable 형식에 씌 `T?`여기서 `T` 기본 형식입니다. 이 구문은 축약형 `System.Nullable<T>`, 두 개의 폼을 서로 교환해 서 사용할 수 있습니다.

A ***nullable이 아닌 값 형식*** 는 반대로 이외의 모든 값 형식 `System.Nullable<T>` 와 해당 약어 `T?` (에 대 한 `T`), 더하기 (즉, 모두 null이 아닌 값 형식으로 제한 되는 모든 형식 매개 변수 입력 매개 변수는 `struct` 제약 조건). 합니다 `System.Nullable<T>` 형식 지정에 대 한 값 형식 제약 조건 `T` ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)), 즉 nullable 형식의 기본 형식은 nullable이 아닌 값 형식일이 아닐 수 있습니다. 기본 형식의 nullable 형식이 nullable 형식 또는 참조 형식 수 없습니다. 예를 들어 `int??` 고 `string?` 종류가 잘못 되었습니다.

Nullable 형식 인스턴스의 `T?` 에 두 개의 공용 읽기 전용 속성이 있습니다.

*  `HasValue` 형식의 속성 `bool`
*  `Value` 형식의 속성 `T`

인스턴스 `HasValue` 는 null이 아닌은 true입니다. Null이 아닌 인스턴스를 사용 하는 알려진된 값을 포함 하 고 `Value` 값을 반환 합니다.

인스턴스입니다 `HasValue` 는 null 일 수 false 라고 합니다. Null 인스턴스는 정의 되지 않은 값을 갖습니다. 읽는 동안 합니다 `Value` 의 null 인스턴스를 사용 하면를 `System.InvalidOperationException` throw 됩니다. 액세스 하는 과정을 `Value` nullable 인스턴스의 속성 이라고 ***래핑 해제***합니다.

기본 생성자를 모든 nullable 형식 외에도 `T?` 형식의 단일 인수를 받아들이는 public 생성자가 `T`합니다. 값이 지정 `x` 형식의 `T`, 폼의 생성자 호출

```csharp
new T?(x)
```
null이 아닌 인스턴스를 만듭니다 `T?` 는 합니다 `Value` 속성은 `x`합니다. 지정된 된 값 이라고에 대 한 nullable 형식의 null이 아닌 인스턴스를 만드는 과정 ***래핑***합니다.

암시적 변환에서 사용할 수는 `null` 리터럴을 `T?` ([리터럴 변환 Null](conversions.md#null-literal-conversions))에서 `T` 하 `T?` ([암시적 nullable 변환](conversions.md#implicit-nullable-conversions)).

## <a name="reference-types"></a>참조 형식

참조 형식은 클래스 형식, 인터페이스 형식, 배열 또는 대리자 형식입니다.

```antlr
reference_type
    : class_type
    | interface_type
    | array_type
    | delegate_type
    ;

class_type
    : type_name
    | 'object'
    | 'dynamic'
    | 'string'
    ;

interface_type
    : type_name
    ;

array_type
    : non_array_type rank_specifier+
    ;

non_array_type
    : type
    ;

rank_specifier
    : '[' dim_separator* ']'
    ;

dim_separator
    : ','
    ;

delegate_type
    : type_name
    ;
```

참조 형식 값에 대 한 참조 되는 ***인스턴스*** 라고 형식의 ***개체***합니다. 특수 값 `null` 모든 참조 형식와 호환 되 고 인스턴스가 없음을 나타냅니다.

### <a name="class-types"></a>클래스 형식

클래스 형식의 데이터 멤버 (상수 및 필드) 함수 멤버 (메서드, 속성, 이벤트, 인덱서, 연산자, 인스턴스 생성자, 소멸자 및 정적 생성자) 및 중첩 된 형식을 포함 하는 데이터 구조를 정의 합니다. 클래스 형식은 상속을 파생된 클래스 확장 하 고 기본 클래스를 특수화할 수 가능해 집니다 메커니즘을 지원 합니다. 클래스 형식의 인스턴스를 사용 하 여 만들어집니다 *object_creation_expression*s ([개체 만들기 식](expressions.md#object-creation-expressions)).

클래스 형식에 설명 되어 있습니다 [클래스](classes.md)합니다.

아래 표에 설명 된 대로 C# 언어에서 특별 한 의미를 갖는 하는 특정 미리 정의 된 클래스 형식입니다.


| __클래스 형식__     | __설명__                                         |
|--------------------|---------------------------------------------------------|
| `System.Object`    | 다른 모든 종류의 궁극적인 기본 클래스입니다. 참조 [개체 유형을](types.md#the-object-type)합니다. | 
| `System.String`    | C# 언어의 문자열 형식입니다. 참조 [문자열 형식](types.md#the-string-type)합니다.         |
| `System.ValueType` | 모든 값 형식의 기본 클래스입니다. 참조 [The System.ValueType 형식](types.md#the-systemvaluetype-type)합니다.          |
| `System.Enum`      | 모든 열거형 형식의 기본 클래스입니다. 참조 [열거형](enums.md)합니다.              |
| `System.Array`     | 모든 배열 형식의 기본 클래스입니다. [배열](arrays.md)을 참조하세요.             |
| `System.Delegate`  | 모든 대리자 형식의 기본 클래스입니다. 참조 [대리자](delegates.md)합니다.          |
| `System.Exception` | 모든 예외 형식의 기본 클래스입니다. 참조 [예외](exceptions.md)합니다.         |

### <a name="the-object-type"></a>개체 유형

`object` 클래스 유형은 다른 모든 종류의 궁극적인 기본 클래스입니다. C#의 모든 형식은 직접 또는 간접적으로에서 파생 되는 `object` 클래스 유형입니다.

키워드 `object` 은 미리 정의 된 클래스에 대 한 별칭 `System.Object`합니다.

### <a name="the-dynamic-type"></a>동적 형식

합니다 `dynamic` 형식, 예: `object`, 모든 개체를 참조할 수 있습니다. 연산자가 식 형식에 적용 되는 경우 `dynamic`, 해결 프로그램이 실행 될 때까지 지연 됩니다. 따라서 참조 된 개체에 적용할 합법적으로 연산자를 사용할 수 없습니다, 하는 경우 오류가 없는 컴파일하는 동안 지정 됩니다. 대신 확인 연산자의 런타임 시 실패 한 경우 예외가 throw 됩니다.

용도에 자세히 설명 된 동적 바인딩을 허용 하는 것 [동적 바인딩](expressions.md#dynamic-binding)합니다.

`dynamic` 동일한 것으로 간주 `object` 다음 측면에서 제외 합니다.

*  식의 형식 연산은 `dynamic` 동적으로 바인딩할 수 있습니다 ([동적 바인딩](expressions.md#dynamic-binding)).
*  형식 유추 ([형식 유추](expressions.md#type-inference))를 선호 `dynamic` 를 통해 `object` 둘 다 후보입니다.

이 동등 인해 다음이 포함합니다.

*  사이 변환이 암시적 id `object` 하 고 `dynamic`, 및 동일 하 게 교체 하는 경우 생성 된 형식 간의 `dynamic` 사용 하 여 `object`
*  사이에 암시적 및 명시적 변환이 `object` 에서 적용 `dynamic`합니다.
*  동일 하 게 교체 하는 경우 메서드 서명에 `dynamic` 사용 하 여 `object` 서명이 같은 것으로 간주 됩니다
*  형식 `dynamic` 구분 되지 않습니다 `object` 런타임 시.
*  형식의 식을 `dynamic` 라고 하는 ***동적 식***합니다.

### <a name="the-string-type"></a>문자열 형식

합니다 `string` 형식이에서 직접 상속 되는 봉인된 클래스 형식이 `object`합니다. 인스턴스는 `string` 클래스 유니코드 문자열을 나타냅니다.

값을 `string` 형식 문자열 리터럴로 작성할 수 있습니다 ([문자열 리터럴](lexical-structure.md#string-literals)).

키워드 `string` 은 미리 정의 된 클래스에 대 한 별칭 `System.String`합니다.

### <a name="interface-types"></a>인터페이스 형식

인터페이스는 계약을 정의합니다. 클래스 또는 구조체는 인터페이스를 구현 하는 계약을 따라야 합니다. 여러 기본 인터페이스에서 상속할 수 및 클래스 또는 구조체는 여러 인터페이스를 구현할 수 있습니다.

인터페이스 형식에 설명 되어 있습니다 [인터페이스](interfaces.md)합니다.

### <a name="array-types"></a>배열 형식

배열에는 계산 된 인덱스를 통해 액세스할 수 있는 0 개 이상의 변수를 포함 하는 데이터 구조입니다. 배열의 요소를 배열에 포함 된 변수는 동일한 형식의 모든 및이 형식을 배열의 요소 형식 이라고 합니다.

배열 형식에 설명 되어 있습니다 [배열](arrays.md)합니다.

### <a name="delegate-types"></a>대리자 형식

대리자에는 하나 이상의 메서드를 가리키는 데이터 구조입니다. 예를 들어 메서드를 의미할 수도 해당 개체 인스턴스.

C 또는 c + +에서 대리자의 가장 가까운 해당 함수에 대 한 포인터 이지만 대리자 정적 참조를 인스턴스 메서드 함수 포인터를 정적 함수를 참조할 수 있습니다, 있지만 합니다. 후자의 경우, 대리자 메서드의 진입점에 대 한 참조 뿐만 아니라 메서드를 호출 하는 개체 인스턴스에 대 한 참조를 저장 합니다.

대리자 형식에 설명 되어 있습니다 [대리자](delegates.md)합니다.

## <a name="boxing-and-unboxing"></a>boxing 및 unboxing

Boxing 및 unboxing의 개념은 C#의 형식 시스템의 중심입니다. 간의 브리지를 제공 *value_type*s 및 *reference_type*값을 허용 하 여는 *value_type* 형식에서 변환할 `object`합니다. Boxing 및 unboxing에 통합된 형식 시스템의 모든 형식의 값을 개체로 처리 궁극적으로 수 여기서 볼 수 있습니다.

### <a name="boxing-conversions"></a>Boxing 변환

boxing 변환이 허용을 *value_type* 암시적으로 변환할 수는 *reference_type*합니다. 다음과 같은 boxing 변환이 존재합니다.

*  모든 *value_type* 형식으로 `object`입니다.
*  모든 *value_type* 형식으로 `System.ValueType`입니다.
*  *non_nullable_value_type* 하나로 *interface_type* 구현한 합니다 *value_type*.
*  *nullable_type* 에 *interface_type* 의 기본 형식에 의해 구현 된 *nullable_type*합니다.
*  모든 *enum_type* 형식으로 `System.Enum`입니다.
*  모든 *nullable_type* 사용 하 여 기본 *enum_type* 형식으로 `System.Enum`합니다.
*  형식 매개 변수에서의 암시적 변환이 참조 형식이 값 형식에서 변환할 끝나는 런타임에 경우 boxing 변환으로 실행 됩니다 ([형식 매개 변수를 포함 하는 암시적 변환은](conversions.md#implicit-conversions-involving-type-parameters)).

값을 *non_nullable_value_type* 이루어져 있습니다 개체 인스턴스를 할당 하 고 복사는 *non_nullable_value_type* 해당 인스턴스로 값.

값을 *nullable_type* 경우 null 참조를 생성 합니다 `null` 값 (`HasValue` 는 `false`), 또는 래핑 해제 하 고 그렇지 않은 경우 기본 값을 boxing의 결과입니다.

실제 프로세스의 값을 *non_nullable_value_type* 제네릭의 존재를 원할지 가장 잘 설명 되어 ***boxing 클래스***, 다음과 같이 선언 된 것 처럼 작동 하는:

```csharp
sealed class Box<T>: System.ValueType
{
    T value;

    public Box(T t) {
        value = t;
    }
}
```

값을 boxing `v` 형식의 `T` 식을 실행 이루어져 `new Box<T>(v)`, 결과 인스턴스 형식의 값으로 반환 하 고 `object`입니다. 따라서 다음 문은
```csharp
int i = 123;
object box = i;
```
에 해당 하는 개념적으로
```csharp
int i = 123;
object box = new Box<int>(i);
```

같은 boxing 클래스 `Box<T>` 위에 실제로 없는 boxed 값의 동적 형식에는 실제로 클래스 형식이 아닌 및 합니다. 대신 형식의 boxed 값 `T` 동적 형식이 `T`를 사용 하 여 동적 형식을 확인 하 고는 `is` 연산자 종류를 간단히 참조할 수 `T`입니다. 예를 들어 개체에 적용된
```csharp
int i = 123;
object box = i;
if (box is int) {
    Console.Write("Box contains an int");
}
```
문자열을 출력 "`Box contains an int`" 콘솔에서.

Boxing 변환 되 고 boxed 값의 복사본을 만드는 것을 의미 합니다. 이 변환에서 다른를 *reference_type* 입력 `object`, 값을 계속 동일한 인스턴스를 참조 하 고 단순히 더 적게 파생 된 형식으로 간주 됩니다 `object`합니다. 예를 들어 선언 된 경우
```csharp
struct Point
{
    public int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```
다음 문은
```csharp
Point p = new Point(10, 10);
object box = p;
p.x = 20;
Console.Write(((Point)box).x);
```
때문에 콘솔에 있는 값 10을 출력 할당이 발생 하는 암시적 boxing 연산을 `p` 를 `box` 의 값 `p` 복사할 합니다. 했습니다 `Point` 된 선언를 `class` 대신 값 20 것 출력 하므로 `p` 및 `box` 동일한 인스턴스를 참조 하 게 됩니다.

### <a name="unboxing-conversions"></a>Unboxing 변환

Unboxing 변환 허용 된 *reference_type* 명시적으로 변환할 수는 *value_type*합니다. 다음과 같은 unboxing 변환이 존재합니다.

*  형식에서 `object` 하나로 *value_type*합니다.
*  형식에서 `System.ValueType` 하나로 *value_type*합니다.
*  *interface_type* 하나로 *non_nullable_value_type* 구현 하는 합니다 *interface_type*합니다.
*  모든 *interface_type* 에 *nullable_type* 기본 형식이 구현 하는 *interface_type*.
*  형식에서 `System.Enum` 하나로 *enum_type*합니다.
*  형식에서 `System.Enum` 하나로 *nullable_type* 사용 하 여 내부 *enum_type*.
*  형식 매개 변수에 명시적 변환이 런타임에 값 형식이 참조 형식에서 변환할 끝나고 경우 unboxing 변환으로 실행 됩니다 ([명시적 동적 변환을](conversions.md#explicit-dynamic-conversions)).

unboxing 작업으로 인해를 *non_nullable_value_type* 개체 인스턴스에 boxed 값은 첫 번째 검사 구성를 지정 *non_nullable_value_type*, 다음의 값을 복사 하 고는 인스턴스입니다.

unboxing를 *nullable_type* 의 null 값을 생성 합니다 *nullable_type* 소스 피연산자가 `null`, 또는 내부 형식의 개체 인스턴스를 unboxing의 래핑된 결과 *nullable_type* 그렇지 않은 경우.

Unboxing 변환 개체의 이전 섹션에 설명 된 boxing 클래스 참조 `box` 에 *value_type* `T` 식을 실행 구성 `((Box<T>)box).value`합니다. 따라서 다음 문은
```csharp
object box = 123;
int i = (int)box;
```
에 해당 하는 개념적으로
```csharp
object box = new Box<int>(123);
int i = ((Box<int>)box).value;
```

unboxing 변환에 대 한는 주어진 *non_nullable_value_type* 런타임에 성공 하려면 소스 피연산자의 값의 boxed 값에 대 한 참조 여야 합니다 *non_nullable_value_type*합니다. 소스 피연산자가 `null`, `System.NullReferenceException` throw 됩니다. 소스 피연산자가 호환 되지 않는 개체에 대 한 참조를 `System.InvalidCastException` throw 됩니다.

unboxing 변환에 대 한는 주어진 *nullable_type* 런타임에 성공 하려면 소스 피연산자의 값 중 하나 여야 합니다 `null` 또는 기본 boxed 값에 대 한 참조를 *non_nullable_value_type* 의 합니다 *nullable_type*합니다. 소스 피연산자가 호환 되지 않는 개체에 대 한 참조를 `System.InvalidCastException` throw 됩니다.

## <a name="constructed-types"></a>생성 된 형식

제네릭 형식 선언 자체로 나타냅니다는 ***언바운드 제네릭 형식*** 적용을 통해 다양 한 유형을 구성 하는 데 "설계도"로 사용 되는 ***형식 인수***합니다. 형식 인수를 꺾쇠 괄호 내에 기록 됩니다 (`<` 및 `>`) 바로 다음 일반 형식의 이름입니다. 하나 이상의 형식 인수를 포함 하는 형식에 호출 되는 ***생성 된 형식***합니다. 생성된 된 형식은 형식 이름이 나타날 수 있는 언어의 대부분의 위치에서 사용할 수 있습니다. 바인딩되지 않은 제네릭 형식 내 에서만 사용할 수는 *typeof_expression* ([typeof 연산자](expressions.md#the-typeof-operator)).

생성 된 형식을 사용할 수도 있습니다 식에서 간단한 이름으로 ([단순 이름](expressions.md#simple-names)) 멤버에 액세스 하는 경우 또는 ([멤버 액세스](expressions.md#member-access)).

경우는 *namespace_or_type_name* 평가, 제네릭 형식과 올바른 개수의 형식 매개 변수를 사용 하는 것으로 간주 됩니다. 따라서으로 형식을 형식 매개 변수의 수가 달라 서로 다른 형식을 식별 하려면 동일한 식별자를 사용 하는 것이 같습니다. 동일한 프로그램에서 제네릭 및 제네릭이 아닌 클래스를 혼합 하는 경우에 유용 합니다.

```csharp
namespace Widgets
{
    class Queue {...}
    class Queue<TElement> {...}
}

namespace MyApplication
{
    using Widgets;

    class X
    {
        Queue q1;            // Non-generic Widgets.Queue
        Queue<int> q2;       // Generic Widgets.Queue
    }
}
```

A *type_name* 형식 매개 변수를 직접 지정 하지 않으면 해당 하는 경우에 생성된 된 형식을 식별할 수 있습니다. 이 형식을 제네릭 클래스 선언 내에 중첩 되어 및 인스턴스 유형을 포함 하는 선언의 이름 조회에 대 한 암시적으로 사용 되는 발생할 수 있습니다 ([제네릭 클래스의 형식에 중첩 된](classes.md#nested-types-in-generic-classes)):

```csharp
class Outer<T>
{
    public class Inner {...}

    public Inner i;                // Type of i is Outer<T>.Inner
}
```

안전 하지 않은 코드 생성된 된 형식으로 사용할 수 없습니다는 *unmanaged_type* ([포인터 형식](unsafe-code.md#pointer-types)).

### <a name="type-arguments"></a>형식 인수

형식 인수 목록의 각 인수는 단순히를 *형식*합니다.

```antlr
type_argument_list
    : '<' type_arguments '>'
    ;

type_arguments
    : type_argument (',' type_argument)*
    ;

type_argument
    : type
    ;
```

안전 하지 않은 코드 ([안전 하지 않은 코드](unsafe-code.md)), *type_argument* 포인터 형식이 되지 않을 수 있습니다. 각 형식 인수가 형식 매개 변수를 해당 제약 조건을 충족 해야 합니다 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).

### <a name="open-and-closed-types"></a>개방형 형식과 닫힌 형식

모든 형식 중 하나로 분류 될 수 있습니다 ***개방형 형식만*** 하거나 ***닫힌 형식을***합니다. 개방형 형식 형식이 형식 매개 변수를 포함 합니다. 좀 더 구체적으로:

*  형식 매개 변수는 개방형 형식을 정의합니다.
*  배열 형식의 요소 형식과 개방형 형식인 경우에 열려 형식인 경우
*  생성 된 형식이 개방형 형식 형식 인수 중 하나 이상의 개방형 형식인 경우에 합니다. 생성된 된 중첩된 형식을 해당 형식 인수 또는 해당 포함 형식의 형식 인수를 하나 이상의 개방형 형식인 경우에 개방형 형식인 합니다.

닫힌된 형식 형식이 개방형 형식이 아닙니다.

런타임에, 제네릭 형식 선언 내에서 코드를 모두를 제네릭 선언에 형식 인수를 적용 하 여 만들어진 여 폐쇄형된 생성된 형식의 컨텍스트에서 실행 됩니다. 제네릭 형식 내에서 각 형식 매개 변수는 특정 런타임 형식에 바인딩되어 있습니다. 모든 문 및 식의 런타임 처리는 항상 발생 하는 닫힌된 형식은 부족해져 개방형 형식 컴파일 시간 동안에 처리 합니다.

각 폐쇄형된 생성된 형식이 마다 고유한 정적 변수를 다른 폐쇄형된 생성된 형식와 공유 되지 않습니다. 런타임 시 개방형 형식이 없으므로 변수가 없음을 정적 개방형 형식을 사용 하 여 연결 합니다. 두 폐쇄형된 생성된 형식 동일한 언바운드 제네릭 형식에서 생성 된 경우 해당 형식 인수는 동일한 형식은 동일한 형식은입니다.

### <a name="bound-and-unbound-types"></a>바인딩 및 바인딩되지 않은 형식

용어 ***형식에 바인딩되지 않은*** 제네릭이 아닌 형식 또는 바인딩되지 않은 제네릭 형식 참조입니다. 용어 ***형식에 바인딩된*** 제네릭이 아닌 형식 또는 생성된 된 형식을 참조 합니다.

바인딩되지 않은 형식은 형식 선언에서 선언 된 엔터티를 가리킵니다. 바인딩되지 않은 제네릭 형식 자체는 형식이 이며 변수, 인수 또는 반환 값의 형식으로 또는 기본 형식으로 사용할 수 없습니다. 바인딩되지 않은 제네릭 형식을 참조할 수 있습니다만 구문을 합니다 `typeof` 식 ([typeof 연산자](expressions.md#the-typeof-operator)).

### <a name="satisfying-constraints"></a>만족 제약 조건

제공 된 형식 인수는 생성 된 형식 또는 제네릭 메서드를 참조할 때마다에 제네릭 형식 또는 메서드의 선언 형식 매개 변수 제약 조건을 검사할지 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)). 각 `where` 절, 형식 인수 `A` 명명 된에 해당 하는 각 제약 조건에 대해 다음과 같이 형식 매개 변수를 확인 합니다.

*  클래스 형식, 인터페이스 형식 또는 형식 매개 변수 제약 조건이 있으면 수 있도록 `C` 제공 된 형식 인수를 사용 하 여 제약 조건을 제약 조건에 표시 되는 모든 형식 매개 변수 대체를 나타냅니다. 제약 조건을 만족를 입력 하는 경우 여야 `A` 형식으로 변환 될 `C` 다음 중 하나에서:
    * Id 변환이 ([Id 변환을](conversions.md#identity-conversion))
    * 암시적 참조 변환 ([암시적 참조 변환](conversions.md#implicit-reference-conversions))
    * Boxing 변환 ([Boxing 변환](conversions.md#boxing-conversions))는 형식이 nullable이 아닌 값 형식이 있는 경우.
    * 형식 매개 변수에서 암시적 참조, boxing 또는 형식 매개 변수 변환이 `A` 에 `C`입니다.
*  제약 조건 참조 형식 제약 조건이 있으면 (`class`), 형식 `A` 다음 중 하나를 충족 해야 합니다.
    * `A` 인터페이스 형식, 클래스 형식, 대리자 형식 또는 배열 형식입니다. 사실은 `System.ValueType` 및 `System.Enum` 는이 제약 조건을 만족 하는 참조 형식입니다.
    * `A` 참조 형식 이어야 하 라고 하는 형식 매개 변수 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).
*  제약 조건 값 형식 제약 조건이 있으면 (`struct`), 형식 `A` 다음 중 하나를 충족 해야 합니다.
    * `A` 구조체 형식 또는 열거형 형식이 아니라 nullable 형식이 아닌 경우 사실은 `System.ValueType` 및 `System.Enum` 는이 제약 조건을 만족 하지 않는 참조 형식입니다.
    * `A` 값 형식 제약 조건이 있는 형식 매개 변수입니다 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).
*  제약 조건을 생성자 제약 조건이 있으면 `new()`, 형식 `A` 아니어야 `abstract` 매개 변수가 없는 공용 생성자가 있어야 하 고 있습니다. 이 중 하나가 참인 경우 충족 합니다.
    * `A` 값 형식 이므로 모든 값 형식에 공용 기본 생성자가 ([기본 생성자](types.md#default-constructors)).
    * `A` 생성자 제약 조건이 있는 형식 매개 변수입니다 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).
    * `A` 값 형식 제약 조건이 있는 형식 매개 변수입니다 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).
    * `A` 없는 클래스인 `abstract` 명시적으로 선언 된 포함 및 `public` 매개 변수가 없는 생성자입니다.
    * `A` 아닙니다 `abstract` 기본 생성자를 포함 ([기본 생성자](classes.md#default-constructors)).

컴파일 타임 오류가 발생 하는 지정 된 형식 인수에서 형식 매개 변수의 제약 조건 중 하나 이상이 충족 되지 않은 경우.

제약 조건은 형식 매개 변수는 상속 되지 있으므로 되지 중 하나를 상속 합니다. 아래 예에서 `D` 해당 형식 매개 변수에 제약 조건을 지정 해야 `T` 있도록 `T` 기본 클래스에 의해 적용 된 제약 조건을 만족 `B<T>`합니다. 반면, 클래스 `E` 때문에 제약 조건을 지정할 필요가 `List<T>` 구현 `IEnumerable` 에 대 한 `T`합니다.

```csharp
class B<T> where T: IEnumerable {...}

class D<T>: B<T> where T: IEnumerable {...}

class E<T>: B<List<T>> {...}
```

## <a name="type-parameters"></a>형식 매개 변수

형식 매개 변수는 값 형식 또는 매개 변수에서 런타임에 바인딩되는 참조 형식 지정 식별자입니다.

```antlr
type_parameter
    : identifier
    ;
```

형식 매개 변수는 많은 다른 실제 형식 인수를 사용 하 여 인스턴스화할 수 있습니다, 되므로 형식 매개 변수는 약간 다른 작업 및 기타 형식 보다 제한이 갖습니다. 여기에는 다음이 포함됩니다.

*  형식 매개 변수는 기본 클래스를 선언 하는 직접 사용할 수 없습니다 ([기본 클래스](classes.md#base-class)) 또는 인터페이스 ([Variant 형식 매개 변수 목록이](interfaces.md#variant-type-parameter-lists)).
*  형식 매개 변수에 있으면 제약 조건에 따라 달라 집니다 매개 변수 형식에 멤버 조회에 대 한 규칙을 적용 합니다. 자세히 설명 [멤버 조회](expressions.md#member-lookup)합니다.
*  사용 가능한 변환이 있으면 제약 조건에 따라 달라 집니다 형식 매개 변수에 대 한 형식 매개 변수에 적용 합니다. 자세히 설명 [형식 매개 변수를 포함 하는 암시적 변환은](conversions.md#implicit-conversions-involving-type-parameters) 하 고 [명시적 동적 변환을](conversions.md#explicit-dynamic-conversions)입니다.
*  리터럴 `null` 참조 형식으로 형식 매개 변수 라고 하는 경우 제외 하 고는 형식 매개 변수에 의해 지정 된 형식으로 변환할 수 없습니다 ([형식 매개 변수를 포함 하는 암시적 변환은](conversions.md#implicit-conversions-involving-type-parameters)). 그러나를 `default` 식 ([기본값 식](expressions.md#default-value-expressions)) 대신 사용할 수 있습니다. 또한 형식 매개 변수로 지정 된 형식으로 값을 비교할 수 `null` 를 사용 하 여 `==` 하 고 `!=` ([참조 형식이 같음 연산자](expressions.md#reference-type-equality-operators)) 형식 매개 변수 값 형식 제약 조건에 없는 경우.
*  A `new` 식 ([개체 만들기 식](expressions.md#object-creation-expressions))만 사용할 수 있습니다 형식 매개 변수를 사용 하 여 형식 매개 변수에 의해 제한 되는 경우는 *constructor_constraint* 또는 값 형식 제약 조건 ([ 형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).
*  형식 매개 변수 특성 내 어디서 나 사용할 수 없습니다.
*  멤버 액세스에서 형식 매개 변수를 사용할 수 없습니다 ([멤버 액세스](expressions.md#member-access)) 또는 형식 이름 ([Namespace 및 형식 이름](basic-concepts.md#namespace-and-type-names)) 정적 멤버 또는 중첩된 된 형식을 식별 합니다.
*  안전 하지 않은 코드 형식 매개 변수를 사용할 수 없습니다는 *unmanaged_type* ([포인터 형식](unsafe-code.md#pointer-types)).

형식으로 형식 매개 변수는 컴파일 타임 구문 순수 하 게 됩니다. 실행 시 각 형식 매개 변수를 제네릭 형식 선언에 형식 인수를 제공 하 여 지정 된 런타임 형식에 바인딩되어 있습니다. 따라서 폐쇄형된 생성된 형식 수를 런타임 시 형식 매개 변수는 사용 하 여 변수의 형식을 선언 ([열기 및 닫힌 형식을](types.md#open-and-closed-types)). 해당 매개 변수에 대 한 형식 인수로 지정 된 실제 형식을 사용 하는 모든 문 및 형식 매개 변수를 포함 하는 식의 런타임 실행 합니다.

## <a name="expression-tree-types"></a>식 트리 형식

***식 트리*** 람다 식을 실행 코드 대신 데이터 구조로 나타낼 수를 허용 합니다. 식 트리는 값 ***식 트리 형식*** 양식의 `System.Linq.Expressions.Expression<D>`여기서 `D` 모든 대리자 형식입니다. 이 사양의 나머지 부분에 대 한 참조는 약어를 사용 하 여 이러한 형식을 `Expression<D>`합니다.

대리자 형식에 대 한 변환이 존재 람다 식에서 경우 `D`, 식 트리 형식으로 변환도 존재 `Expression<D>`합니다. 람다 식의 실행 코드를 참조 하는 대리자를 생성 하는 람다 식 대리자 형식으로 변환 하는 반면는 식 트리 형식으로 변환 하는 람다 식의 식 트리 표현을 만듭니다.

식 트리 람다 식의 효율적인 메모리 내 데이터 표시 하 고 투명 하 고 명시적 람다 식의 구조를 확인 합니다.

마찬가지로 다음 대리자 형식을 `D`, `Expression<D>` 매개 변수 및 반환 형식 이라고의 것과 동일는 `D`합니다.

다음 예제에서는 람다 식을 실행 코드와 식 트리를 나타냅니다. 에 대 한 변환이 존재 하므로 `Func<int,int>`, 변환에도 존재 `Expression<Func<int,int>>`:

```csharp
Func<int,int> del = x => x + 1;                    // Code

Expression<Func<int,int>> exp = x => x + 1;        // Data
```

다음 이러한 할당을 대리자 `del` 반환 하는 메서드를 참조 `x + 1`, 및 식 트리 `exp` 식에 설명 하는 데이터 구조를 참조 `x => x + 1`합니다.

제네릭 형식의 정확한 정의 `Expression<D>` 람다 식을 식 트리 형식으로 변환 되 면 식 트리를 생성 하는 것에 대 한 정확한 규칙 뿐만 아니라 둘 다이 사양의 범위 밖에 있습니다.

두 가지가 명시적으로 만들어야 하는 것이 중요 합니다.

*  모든 람다 식은 식 트리로 변환할 수 있습니다. 예를 들어 문 본문을 사용 하 여 람다 식 및 할당을 포함 하는 람다 식을 나타낼 수 없습니다. 이러한 경우에 변환은 여전히 존재 하지만, 컴파일 시 실패 합니다. 이러한 예외에 자세히 나와 [익명 함수 변환](conversions.md#anonymous-function-conversions)합니다.
*   `Expression<D>` 인스턴스 메서드를 제공 `Compile` 형식의 대리자를 생성 하는 `D`:

    ```csharp
    Func<int,int> del2 = exp.Compile();
    ```

    실행할 식 트리로 표시 되는 코드를 하면이 대리자를 호출 합니다. 따라서 위의 정의 지정 del 및 del2은 동일 하며 다음 두 문이 같은 효과 갖습니다.

    ```csharp
    int i1 = del(1);
    
    int i2 = del2(1);
    ```

    이 코드를 실행 한 후 `i1` 하 고 `i2` 값을 모두 갖습니다 `2`합니다.

