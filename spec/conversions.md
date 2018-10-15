# <a name="conversions"></a>변환

A ***변환*** 식을 특정 형식으로 처리 될 수 있습니다. 변환을 다른 형식으로 처리 됨을 지정 된 형식의 식의 않을 또는 형식 유형을 알 수 없는 식 발생할 수 있습니다. 변환 될 수 있습니다 ***암시적*** 또는 ***명시적***에 명시적 캐스트가 필요 여부를 결정 하 고 있습니다. 예를 들어, 형식 변환 `int` 형식으로 `long` 암시적 따라서 식의 형식 `int` 형식으로 암시적으로 처리 될 수 있습니다 `long`합니다. 형식에서 변환, `long` 형식으로 `int`, 명시적 이므로 명시적 캐스트가 필요 합니다.

```csharp
int a = 123;
long b = a;         // implicit conversion from int to long
int c = (int) b;    // explicit conversion from long to int
```

변환 중 일부는 언어에서 정의 됩니다. 프로그램에 고유한 변환을 정의할 수도 있습니다 ([사용자 정의 변환은](conversions.md#user-defined-conversions)).

## <a name="implicit-conversions"></a>암시적 변환

다음 변환은 암시적 변환으로 분류 됩니다.

*  Identity 변환
*  암시적 숫자 변환
*  암시적 열거형 변환 합니다.
*  Nullable 암시적 변환
*  Null 리터럴 변환
*  암시적 참조 변환
*  Boxing 변환
*  동적 암시적 변환
*  암시적 상수 식 변환
*  암시적 사용자 정의 변환
*  익명 함수 변환
*  메서드 그룹 변환

암시적으로 다양 한 함수 멤버 호출을 포함 하 여 환경에서에서 발생할 수 있습니다 ([동적 오버 로드 확인 검사 하는 컴파일 타임](expressions.md#compile-time-checking-of-dynamic-overload-resolution)), 캐스트 식 ([캐스트 식](expressions.md#cast-expressions)), 및 할당 ([대입 연산자](expressions.md#assignment-operators)).

미리 정의 된 암시적 변환이 항상 성공 하 고 throw 되는 예외를 일으키지 않습니다. 올바르게 설계 된 사용자 정의 된 암시적 변환도 이러한 특징을 나타내는입니다.

형식 변환의 목적 `object` 고 `dynamic` 동일 하다 고 간주 합니다.

그러나 동적 변환을 ([암시적 동적 변환을](conversions.md#implicit-dynamic-conversions) 하 고 [명시적 동적 변환을](conversions.md#explicit-dynamic-conversions)) 형식의 식에만 적용 `dynamic` ([동적 형식](types.md#the-dynamic-type)).

### <a name="identity-conversion"></a>Identity 변환

Id 변환이 모든 형식에서 동일한 형식으로 변환합니다. 이 변환은 해당 형식으로 변환할 수는 필수 형식이 이미 있는 엔터티의 한다고 할 수 있습니다.

*  개체 및 동적 동일 하다 고 간주 이므로 간의 id 변환이 `object` 하 고 `dynamic`, 및 서로 동일의 모든 항목을 바꿀 때 생성 된 형식 `dynamic` 사용 하 여 `object`.

### <a name="implicit-numeric-conversions"></a>암시적 숫자 변환

암시적 숫자 변환 됩니다.

*  `sbyte` 하 `short`, `int`, `long`, `float`를 `double`, 또는 `decimal`합니다.
*  `byte` 하 `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `float`, `double`, 또는 `decimal`합니다.
*  `short` 하 `int`를 `long`, `float`를 `double`, 또는 `decimal`합니다.
*  `ushort` 하 `int`, `uint`, `long`, `ulong`를 `float`, `double`, 또는 `decimal`합니다.
*  `int` 하 `long`를 `float`를 `double`, 또는 `decimal`합니다.
*  `uint` 하 `long`를 `ulong`, `float`를 `double`, 또는 `decimal`합니다.
*  `long` 하 `float`를 `double`, 또는 `decimal`합니다.
*  `ulong` 하 `float`를 `double`, 또는 `decimal`합니다.
*  `char` 하 `ushort`, `int`, `uint`, `long`, `ulong`, `float`를 `double`, 또는 `decimal`합니다.
*  `float` 에 `double`입니다.

변환할 `int`, `uint`, `long`, 또는 `ulong` 에 `float` 들어오고 `long` 또는 `ulong` 를 `double` 정밀도 손실 될 수 있지만 두지 원인 크기는 손실 합니다. 다른 암시적 숫자 변환에는 모든 정보가 손실 되지 않도록 합니다.

으로 암시적 변환은 없습니다 합니다 `char` 입력을 다른 정수 계열 형식의 값을 자동으로 변환 하지 않습니다는 `char` 형식입니다.

### <a name="implicit-enumeration-conversions"></a>열거형 암시적 변환

변환 하는 열거형 암시적 변환을 허용 합니다 *decimal_integer_literal* `0` 에 변환할 *enum_type* 및 모든 *nullable_type* 입니다 내부 형식에 *enum_type*합니다. 후자의 경우 변환이 기본으로 전환 하 여 계산 *enum_type* 결과 줄 바꿈 ([Nullable 형식](types.md#nullable-types)).

### <a name="implicit-interpolated-string-conversions"></a>보간된 문자열의 암시적 변환

암시적 보간된 문자열 변환 허용을 *interpolated_string_expression* ([보간된 문자열](expressions.md#interpolated-strings))로 변환할 `System.IFormattable` 또는 `System.FormattableString` (구현 하는 `System.IFormattable`).

이 변환을 적용 될 때 문자열 값은 하지 보간된 문자열에서 구성 됩니다. 대신의 인스턴스이고 `System.FormattableString` 만든 이면에 설명 된 대로 [보간된 문자열](expressions.md#interpolated-strings)합니다.

### <a name="implicit-nullable-conversions"></a>Nullable 암시적 변환

Nullable이 아닌 값 형식에서 작동 하는 미리 정의 된 암시적 변환이 이러한 형식의 null 허용 형식으로 사용할 수도 있습니다. 각각의 미리 정의 된 암시적 id 및 nullable이 아닌 값 형식에서 변환 하는 숫자 변환에 대 한 `S` nullable이 아닌 값 형식에 `T`, 다음과 같은 암시적 nullable 변환이 존재 합니다.

*  암시적 변환이 `S?` 에 `T?`입니다.
*  암시적 변환이 `S` 에 `T?`입니다.

Null 허용의 암시적 변환이 평가에서 변환 하는 기본 변환을 기반 `S` 에 `T` 다음과 같이 진행 됩니다.

*  nullable 변환 되는 경우 `S?` 에 `T?`:
    * 원본 값이 null (`HasValue` 속성은 false), 결과 형식의 null 값 `T?`합니다.
    * 변환에서 래핑 해제를으로 평가 되는 고, 그렇지 `S?` 하 `S`고 뒤에 변환 하는 기본 `S` 하 `T`뒤에 래핑, ([Nullable 형식](types.md#nullable-types)) 에서`T` 에 `T?`입니다.

*  nullable 변환 되는 경우 `S` 에 `T?`, 변환에서 기본 변환으로 평가 됩니다 `S` 에 `T` 뒤에에서 배치 `T` 를 `T?`입니다.

### <a name="null-literal-conversions"></a>Null 리터럴 변환

암시적 변환이 존재 합니다 `null` 모든 nullable 형식 리터럴. 이 변환은 null 값을 생성 ([Nullable 형식](types.md#nullable-types)) 지정된 된 nullable 형식입니다.

### <a name="implicit-reference-conversions"></a>암시적 참조 변환

암시적 참조 변환 됩니다.

*  모든 *reference_type* 하 `object` 및 `dynamic`합니다.
*  *class_type* `S` 하나로 *class_type* `T`제공 `S` 에서 파생 된 `T`합니다.
*  *class_type* `S` 하나로 *interface_type* `T`제공 `S` 구현 `T`합니다.
*  *interface_type* `S` 하나로 *interface_type* `T`제공 `S` 에서 파생 된 `T`합니다.
*  *array_type* `S` 요소 형식을 가진 `SE` 에 *array_type* `T` 요소 형식을 가진 `TE`경우 다음 모두:
    * `S` 및 `T` 요소 형식에 의해서만 달라 집니다. 다시 말해 `S` 및 `T` 차원 수가 같아야 합니다.
    * 둘 다 `SE` 하 고 `TE` 됩니다 *reference_type*s입니다.
    * 암시적 참조 변환이 존재 `SE` 에 `TE`입니다.
*  모든 *array_type* 에 `System.Array` 및 인터페이스를 구현 합니다.
*  1 차원 배열 형식에서 `S[]` 하 `System.Collections.Generic.IList<T>` 및 해당 기본 인터페이스를 암시적 id 또는 참조 변환이 제공 `S` 에 `T`입니다.
*  모든 *delegate_type* 에 `System.Delegate` 및 인터페이스를 구현 합니다.
*  에 null 리터럴에서 *reference_type*합니다.
*  *reference_type* 에 *reference_type* `T` 으로 암시적 id 또는 참조 변환이 있는 경우를 *reference_type* `T0` 및 `T0` 에 identity 변환할 `T`합니다.
*  모든 *reference_type* 인터페이스 또는 대리자 형식으로 `T` 인터페이스 또는 대리자 형식에 암시적 id 또는 참조 변환이 있으면 `T0` 및 `T0` 은 변환 ([ 변형 변환이](interfaces.md#variance-conversion))를 `T`입니다.
*  암시적 변환이 포함 된 참조 형식에 알려지지 않은 매개 변수를 입력 합니다. 참조 [형식 매개 변수를 포함 하는 암시적 변환은](conversions.md#implicit-conversions-involving-type-parameters) 형식 매개 변수를 포함 하는 암시적 변환에 대 한 자세한 내용은 합니다.

암시적 참조 변환 사이의 이러한 변환은 *reference_type*항상 성공으로 입증할 수 고 따라서 런타임에 검사를 요구 하는 s입니다.

참조 변환, 암시적 또는 명시적 변환 되는 개체의 참조 id를 변경 되어서는 안됩니다. 즉, 변환은 참조 변환이 참조의 형식 변경 될 수 있지만,이 변경 되지 않습니다 형식 또는 참조 되는 개체의 값.

### <a name="boxing-conversions"></a>Boxing 변환

boxing 변환이 허용을 *value_type* 참조 형식으로 암시적으로 변환할 수 있습니다. Boxing 변환에서 존재 *non_nullable_value_type* 에 `object` 하 고 `dynamic`를 `System.ValueType` 및 모든 *interface_type* 구현한는 *non_ nullable_value_type*합니다. 또한 프로그램 *enum_type* 형식으로 변환할 수 `System.Enum`입니다.

boxing 변환이 존재를 *nullable_type* 참조 형식으로 boxing 변환이 경우에 있는 기본 *non_nullable_value_type* 참조 형식입니다.

값 형식에는 인터페이스 형식으로 boxing 변환 `I` 인터페이스 형식으로는 boxing 변환이 있는지 `I0` 및 `I0` 에 identity 변환할 `I`합니다.

값 형식은 인터페이스 형식으로는 boxing 변환이 `I` 인터페이스 또는 대리자 형식에는 boxing 변환이 있을 경우 `I0` 하 고 `I0` 변환 됩니다 ([변형 변환이](interfaces.md#variance-conversion)) 를`I`.

값을 *non_nullable_value_type* 이루어져 있습니다 개체 인스턴스를 할당 하 고 복사는 *value_type* 해당 인스턴스로 값. 구조체 형식에 넣을 수 있습니다 `System.ValueType`구조체에 대 한 기본 클래스 이므로, ([상속](structs.md#inheritance)).

값을 *nullable_type* 다음과 같이 진행 됩니다.

*  원본 값이 null 이면 (`HasValue` 속성이 false 이면), 결과 대상 형식의 null 참조입니다.
*  그렇지 않으면 결과 boxed 참조 `T` 압축을 풀고 원본 값을 boxing 하 여 생성 합니다.

Boxing 변환에 자세히 설명 되어 [Boxing 변환](types.md#boxing-conversions)합니다.

### <a name="implicit-dynamic-conversions"></a>동적 암시적 변환

형식의 식에서 암시적 동적 변환이 존재 `dynamic` 형식으로 `T`입니다. 변환 바인딩된 동적으로 ([동적 바인딩](expressions.md#dynamic-binding))를 런타임에 식의 런타임 형식에서 암시적 변환이 발생을 검색 하는 것이 즉 `T`합니다. 변환 작업 없이 있으면 런타임 예외가 throw 됩니다.

이 암시적 변환은의 시작 부분에서 권장 하는 것 처럼 보이는 위반 하는 참고 [암시적 변환을](conversions.md#implicit-conversions) 암시적 변환이 예외를 발생 시키는 하지 않습니다. 그러나 없는 자체 변환 하지만 *찾기* 예외를 발생 시키는 변환 합니다. 런타임 예외 위험이 동적 바인딩 사용 하 여에 정렬이 내재 되어 있습니다. 변환의 동적 바인딩 원하지 않는 경우 식 먼저 변환할 수 `object`, 한 다음 원하는 형식.

다음 예제에서는 암시적 동적 변환을 보여 줍니다.

```csharp
object o  = "object"
dynamic d = "dynamic";

string s1 = o; // Fails at compile-time -- no conversion exists
string s2 = d; // Compiles and succeeds at run-time
int i     = d; // Compiles but fails at run-time -- no conversion exists
```

에 할당 `s2` 및 `i` 암시적 동적 변환 작업의 바인딩을 런타임까지 일시 중단 된 둘 다 사용 합니다. 실행 시의 런타임 형식에서 암시적 변환의 찾는 `d`  --  `string` -대상 형식입니다. 변환이 `string` 없습니다 `int`합니다.

### <a name="implicit-constant-expression-conversions"></a>암시적 상수 식 변환

다음과 같은 변환이 허용 하는 상수 식을 암시적 변환이 발생 합니다.

*  A *constant_expression* ([상수 식](expressions.md#constant-expressions)) 형식의 `int` 형식으로 변환 될 수 있습니다 `sbyte`를 `byte`를 `short`, `ushort`를 `uint`, 또는 `ulong`의 값을 제공 합니다 *constant_expression* 대상 형식의 범위 내입니다.
*  A *constant_expression* 형식의 `long` 형식으로 변환 될 수 있습니다 `ulong`의 값을 제공 합니다 *constant_expression* 는 음수가 아닙니다.

### <a name="implicit-conversions-involving-type-parameters"></a>형식 매개 변수를 포함 하는 암시적 변환

지정 된 형식 매개 변수는 다음과 같은 암시적 변환이 존재 `T`:

*  `T` 유효한 기본 클래스에 `C`에서 `T` 의 모든 기본 클래스 `C`, 및 `T` 구현한 인터페이스 `C`합니다. 에 런타임 경우 `T` 값 형식이 boxing 변환으로 변환 실행 됩니다. 그렇지 않으면 변환이 암시적 참조 변환 또는 id 변환을 실행 됩니다.
*  `T` 인터페이스 형식으로 `I` 에서 `T`의 효과적인 인터페이스 집합 들어오고 `T` 의 기본 인터페이스 `I`합니다. 에 런타임 경우 `T` 값 형식이 boxing 변환으로 변환 실행 됩니다. 그렇지 않으면 변환이 암시적 참조 변환 또는 id 변환을 실행 됩니다.
*  `T` 형식 매개 변수에 `U`제공 `T` 에 따라 달라 집니다 `U` ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)). 런타임 경우 at `U` 이 값 형식이 면 `T` 및 `U` 반드시 동일한 형식이 고 변환이 수행 되지 않습니다. 그렇지 않은 경우, `T` 값 형식이 boxing 변환으로 변환 실행 됩니다. 그렇지 않으면 변환이 암시적 참조 변환 또는 id 변환을 실행 됩니다.
*  null 리터럴을 `T`제공 `T` 참조 형식일 것으로 알려져 있습니다.
*  `T` 참조 형식으로 `I` 참조 형식으로 변환 하는 암시적 변환이 있는지 `S0` 하 고 `S0` 에 id 변환이 `S`입니다. 변환은 동일한 방식으로 변환으로을 실행 하는 데 런타임 시 `S0`합니다.
*  `T` 인터페이스 형식으로 `I` 인터페이스 또는 대리자 형식으로 암시적 변환이 있는 경우 `I0` 하 고 `I0` 변환 됩니다 하 `I` ([변형 변환이](interfaces.md#variance-conversion) ). 에 런타임 경우 `T` 값 형식이 boxing 변환으로 변환 실행 됩니다. 그렇지 않으면 변환이 암시적 참조 변환 또는 id 변환을 실행 됩니다.

하는 경우 `T` 참조 형식인 것으로 알려진 ([입력 매개 변수 제약 조건이](classes.md#type-parameter-constraints)), 위의 변환은 모든 암시적 참조 변환으로 분류 됩니다 ([암시적 참조 변환](conversions.md#implicit-reference-conversions)). 하는 경우 `T` 는 참조 형식으로 알 수 없는 위의 변환은 boxing 변환으로 분류 됩니다 ([Boxing 변환](conversions.md#boxing-conversions)).

### <a name="user-defined-implicit-conversions"></a>암시적 사용자 정의 변환

사용자 정의 된 암시적 변환이 선택적 표준 암시적 변환이 뒤에 다른 선택적 표준 암시적 변환이 암시적 사용자 정의 변환 연산자를 실행 하 여 다음 이루어져 있습니다. 암시적 사용자 정의 변환 평가 대 한 정확한 규칙에 설명 되어 있습니다 [암시적 사용자 정의 변환 처리](conversions.md#processing-of-user-defined-implicit-conversions)합니다.

### <a name="anonymous-function-conversions-and-method-group-conversions"></a>익명 함수 변환 및 메서드 그룹 변환

익명 함수 및 메서드 그룹에 자체의 형식 필요가 없지만 형식 또는 식 트리 형식의 대리자를 암시적으로 변환 될 수 있습니다. 익명 함수 변환에 자세히 설명 되어 있습니다 [익명 함수 변환](conversions.md#anonymous-function-conversions) 및에 메서드 그룹 변환 [메서드 그룹 변환](conversions.md#method-group-conversions)합니다.

## <a name="explicit-conversions"></a>명시적 변환

다음 변환은 명시적 변환으로 분류 됩니다.

*  모든 암시적 변환입니다.
*  명시적 숫자 변환 합니다.
*  명시적 열거형 변환 합니다.
*  명시적 nullable 변환 합니다.
*  명시적 참조 변환 합니다.
*  명시적 인터페이스 변환 합니다.
*  Unboxing 변환 합니다.
*  동적 명시적 변환
*  사용자 정의 명시적 변환 합니다.

명시적 변환은 cast 식에서 발생할 수 있습니다 ([캐스트 식](expressions.md#cast-expressions)).

명시적 변환의 집합에는 모든 암시적 변환이 포함 됩니다. 즉, 중복 된 캐스트 식이 허용 됩니다.

명시적 변환은 암시적 변환 되지 않은 값은 명시적 요구를 충분히 서로 다른 형식의 도메인에 걸쳐 항상 성공으로 입증할 수 없는 변환, 내용은 손실 될 수도 있는 변환 및 변환 표기법입니다.

### <a name="explicit-numeric-conversions"></a>명시적 숫자 변환

명시적 숫자 변환에서 변환 되는 *numeric_type* 간 *numeric_type* 는 암시적 숫자 변환이 ([암시적 숫자 변환](conversions.md#implicit-numeric-conversions)) 아직 없으면:

*  `sbyte` 하 `byte`를 `ushort`, `uint`를 `ulong`, 또는 `char`합니다.
*  `byte` 하 `sbyte` 고 `char`입니다.
*  `short` 하 `sbyte`, `byte`, `ushort`, `uint`를 `ulong`, 또는 `char`합니다.
*  `ushort` 하 `sbyte`를 `byte`를 `short`, 또는 `char`합니다.
*  `int` 하 `sbyte`, `byte`, `short`, `ushort`를 `uint`, `ulong`, 또는 `char`합니다.
*  `uint` 하 `sbyte`, `byte`, `short`, `ushort`를 `int`, 또는 `char`합니다.
*  `long` 하 `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`를 `ulong`, 또는 `char`합니다.
*  `ulong` 하 `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`를 `long`, 또는 `char`합니다.
*  `char` 하 `sbyte`를 `byte`, 또는 `short`합니다.
*  `float` 하 `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, 또는 `decimal`합니다.
*  `double` 하 `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, 또는 `decimal`합니다.
*  `decimal` 하 `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, 또는 `double`합니다.

있기 때문에 모든 명시적 및 암시적 숫자 변환에 포함 하는 명시적 변환을 항상에서 변환할 *numeric_type* 다른 *numeric_type* 캐스트 식 (사용 하 여 [캐스트 식](expressions.md#cast-expressions)).

명시적 숫자 변환 정보가 손실 될 또는 예외가 throw 됩니다. 명시적 숫자 변환은 다음과 같이 처리 됩니다.

*  정수 계열 형식에서 다른 정수 계열 형식으로 변환의 처리에 따라 달라 집니다 오버플로 검사 컨텍스트에 ([checked 및 unchecked 연산자](expressions.md#the-checked-and-unchecked-operators)) 변환 되는 배치 합니다.
    * 에 `checked` 컨텍스트에서 소스 피연산자의 값이 대상 형식의 범위 내에 있지만 throw 하는 경우 변환이 성공는 `System.OverflowException` 소스 피연산자의 값이 대상 형식의 범위를 벗어난 경우.
    * 에 `unchecked` 컨텍스트에 변환이 항상 성공 하 고 다음과 같이 진행 됩니다.
        * 소스 형식이 대상 형식보다 큰 경우 소스 값은 가장 중요한 비트인 해당 "extra"를 삭제함으로써 잘립니다. 그런 다음, 결과는 대상 형식의 값으로 처리됩니다.
        * 소스 형식이 대상 형식보다 작은 경우 소스 값은 대상 형식과 크기가 같도록 부호 확장 또는 0 확장 중 하나입니다. 부호 확장은 소스 형식이 서명된 경우 사용되며, 소스 형식이 서명되지 않은 경우 0 확장이 사용됩니다. 그런 다음, 결과는 대상 형식의 값으로 처리됩니다.
        * 소스 형식이 대상 형식과 동일한 크기인 경우 소스 값은 대상 형식의 값으로 처리됩니다.
*  변환에 대 한 `decimal` 정수 계열 형식으로 원본 값이 0에 가장 가까운 정수 값으로 반올림 됩니다 및 정수 계열 값이 변환의 결과가 됩니다. 결과 정수 값을 대상 형식의 범위를 벗어난 경우는 `System.OverflowException` throw 됩니다.
*  변환에 대 한 `float` 나 `double` 정수 계열 형식으로 처리 하는 종속 오버플로 검사 컨텍스트에 ([checked 및 unchecked 연산자](expressions.md#the-checked-and-unchecked-operators)) 변환 되는 배치:
    * 에 `checked` 컨텍스트 변환 다음과 같이 진행 됩니다.
        * 피연산자의 값이 NaN 또는 무한 한 `System.OverflowException` throw 됩니다.
        * 그렇지 않으면 소스 피연산자는 0에 가장 가까운 정수 값으로 반올림 됩니다. 정수 계열 값이 대상 형식의 범위 내에 있으면이 값은 변환의 결과입니다.
        * 그렇지 않으면 `System.OverflowException`이 throw됩니다.
    * 에 `unchecked` 컨텍스트에 변환이 항상 성공 하 고 다음과 같이 진행 됩니다.
        * 피연산자의 값 NaN 또는 무한 인 경우 변환 결과 값인 지정 되지 않은 대상 형식입니다.
        * 그렇지 않으면 소스 피연산자는 0에 가장 가까운 정수 값으로 반올림 됩니다. 정수 계열 값이 대상 형식의 범위 내에 있으면이 값은 변환의 결과입니다.
        * 그렇지 않은 경우 변환의 결과 대상 형식의 값을 알 수 없는 경우
*  변환에 대 한 `double` 하 `float`의 `double` 값은 반올림 가장 가까운 `float` 값입니다. 경우는 `double` 값이 너무 작아서로 나타낼 수는 `float`, 결과 양의 0 또는 음의 0입니다. 경우는 `double` 값이 너무 커서로 나타낼 수는 `float`, 결과 양의 무한대 또는 음의 무한대입니다. 경우는 `double` 값이 NaN, 결과가 NaN 이기도 합니다.
*  변환에 대 한 `float` 또는 `double` 하 `decimal`, 소스 값으로 변환 됩니다 `decimal` 표현이 필요한 경우 가장 가까운 28 소수 자릿수가 반올림 ([10 진수 형식](types.md#the-decimal-type)). 원본 값이 너무 작아로 나타낼 수 없는 경우는 `decimal`, 결과 0이 됩니다. 원본 값이 NaN, 무한대 또는 너무 커서로 나타낼 수는 `decimal`, `System.OverflowException` throw 됩니다.
*  변환에 대 한 `decimal` 하 `float` 또는 `double`의 `decimal` 값은 반올림 가장 가까운 `double` 또는 `float` 값입니다. 이 변환의 정밀도 떨어지는는 예외를 throw 하지 않습니다 발생 합니다.

### <a name="explicit-enumeration-conversions"></a>명시적 열거형 변환

명시적 열거형 변환은 다음과 같습니다.

*  `sbyte`, `byte`, `short`, `ushort`, `int`를 `uint`, `long`, `ulong`, `char`, `float`, `double`, 또는 `decimal` 모든 를*enum_type*합니다.
*  *enum_type* 하 `sbyte`, `byte`, `short`를 `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, 또는 `decimal`합니다.
*  모든 *enum_type* 다른 *enum_type*합니다.

두 형식 간의 명시적 열거형 변환은 모든 참여 하 고 처리 하 여 처리 됩니다 *enum_type* 의 내부 형식으로 *enum_type*, 암시적 또는 명시적를 만든 후 수행 결과 형식 간의 변환 숫자입니다. 예를 들어를 *enum_type* `E` 사용 하 여의 내부 형식 및 `int`, 변환 `E` 하 `byte` 명시적 숫자 변환으로 처리 됩니다 ([Explicit 숫자 변환](conversions.md#explicit-numeric-conversions))에서 `int` 하 `byte`에서 변환이 `byte` 하 `E` 암시적 숫자 변환으로 처리 됩니다 ([암시적 숫자 변환](conversions.md#implicit-numeric-conversions)) `byte` 에 `int`입니다.

### <a name="explicit-nullable-conversions"></a>명시적 nullable 변환

***Null을 허용 하는 명시적 변환을*** 허용 미리도 이러한 형식의 null 허용 형식으로 사용할 nullable이 아닌 값 형식에서 작동 하는 명시적 변환을 정의 합니다. Nullable이 아닌 값 형식에서 변환 하는 미리 정의 된 명시적 변환의 각 `S` nullable이 아닌 값 형식 `T` ([Id 변환을](conversions.md#identity-conversion), [암시적숫자변환](conversions.md#implicit-numeric-conversions), [암시적 열거형 변환](conversions.md#implicit-enumeration-conversions)를 [명시적 숫자 변환](conversions.md#explicit-numeric-conversions), 및 [명시적 열거형 변환](conversions.md#explicit-enumeration-conversions)), 다음 nullable 변환 존재합니다.

*  변환 하는 명시적 변환을 `S?` 에 `T?`입니다.
*  변환 하는 명시적 변환을 `S` 에 `T?`입니다.
*  변환 하는 명시적 변환을 `S?` 에 `T`입니다.

평가 nullable 변환에서 변환 하는 기본 변환을 기반 `S` 에 `T` 다음과 같이 진행 됩니다.

*  nullable 변환 되는 경우 `S?` 에 `T?`:
    * 원본 값이 null (`HasValue` 속성은 false), 결과 형식의 null 값 `T?`합니다.
    * 변환에서 래핑 해제를으로 평가 되는 고, 그렇지 `S?` 에 `S`고 뒤에 변환 하는 기본 `S` 에 `T`에서 래핑 뒤 `T` 에 `T?`합니다.
*  nullable 변환 되는 경우 `S` 에 `T?`, 변환에서 기본 변환으로 평가 됩니다 `S` 에 `T` 뒤에에서 배치 `T` 를 `T?`입니다.
*  nullable 변환 되는 경우 `S?` 하 `T`, 변환에서 래핑 해제를로 평가 됩니다 `S?` 에 `S` 뒤에 변환 하는 기본 `S` 에 `T`입니다.

값이 null 허용 값을 래핑 해제 하려고 한 경우 예외가 throw 됩니다 `null`합니다.

### <a name="explicit-reference-conversions"></a>명시적 참조 변환

명시적 참조 변환은 다음과 같습니다.

*  `object` 하 고 `dynamic` 다른 *reference_type*합니다.
*  *class_type* `S` 하나로 *class_type* `T`제공 `S` 의 기본 클래스인 `T`합니다.
*  *class_type* `S` 하나로 *interface_type* `T`제공 `S` 봉인 되거나 제공 되지 않은 `S` 구현 하지 않는 `T`.
*  *interface_type* `S` 하나로 *class_type* `T`제공 `T` 봉인 되거나 제공 되지 `T` 구현 `S`합니다.
*  *interface_type* `S` 하나로 *interface_type* `T`제공 `S` 에서 파생 되지 않은 `T`합니다.
*  *array_type* `S` 요소 형식을 가진 `SE` 에 *array_type* `T` 요소 형식을 가진 `TE`경우 다음 모두:
    * `S` 및 `T` 요소 형식에 의해서만 달라 집니다. 다시 말해 `S` 및 `T` 차원 수가 같아야 합니다.
    * 둘 다 `SE` 하 고 `TE` 됩니다 *reference_type*s입니다.
    * 명시적 참조 변환이 존재 `SE` 에 `TE`입니다.
*  `System.Array` 인터페이스를 구현 하 고 *array_type*합니다.
*  1 차원 배열 형식에서 `S[]` 하 `System.Collections.Generic.IList<T>` 및 해당 기본 인터페이스에서 명시적 참조 변환이 제공 `S` 에 `T`입니다.
*  `System.Collections.Generic.IList<S>` 및 1 차원 배열 형식에 기본 인터페이스 `T[]`에서 사용 되는 명시적 id 또는 참조 변환이 있는 경우 `S` 하려면 `T`합니다.
*  `System.Delegate` 인터페이스를 구현 하 고 *delegate_type*합니다.
*  참조 형식에 대 한 참조 형식에서 `T` 참조 형식으로 변환 하는 명시적 참조 변환이 있는지 `T0` 하 고 `T0` id 변환이 `T`입니다.
*  인터페이스 또는 대리자 형식에 대 한 참조 형식에서 `T` 인터페이스 또는 대리자 형식으로 명시적 참조 변환이 있을 경우 `T0` 고 `T0` 변형 가능은 하 `T` 또는 `T` 는 분산-변환할 `T0` ([변형 변환이](interfaces.md#variance-conversion)).
*  `D<S1...Sn>` 하 `D<T1...Tn>` 여기서 `D<X1...Xn>` 제네릭 대리자 형식인 `D<S1...Sn>` 동일 하거나 호환 되지 `D<T1...Tn>`, 및 각 형식 매개 변수에 `Xi` 의 `D` 다음 포함:
    * 하는 경우 `Xi` 다음 변형의 경우 아닙니다 `Si` 동일 `Ti`합니다.
    * 하는 경우 `Xi` 는 공변 (covariant)는 암시적 또는 명시적 id 또는 참조 변환이에서 됩니다 `Si` 를 `Ti`합니다.
    * 하는 경우 `Xi` 반공 분산 이면 `Si` 및 `Ti` 은 동일한 또는 둘 다 참조 형식입니다.
*  명시적 변환 관련 된 참조 형식에 알려지지 않은 매개 변수를 입력 합니다. 형식 매개 변수를 포함 하는 명시적 변환에 대 한 자세한 내용은 참조 하세요. [형식 매개 변수를 포함 하는 명시적 변환은](conversions.md#explicit-conversions-involving-type-parameters)합니다.

명시적 참조 변환은 정확한 지 확인에 런타임 검사를 해야 하는 참조 형식 간의 변환입니다.

명시적 참조를 성공적으로 변환 런타임에 소스 피연산자의 값은 `null`, 소스 피연산자가 참조 하는 개체의 실제 형식에 대 한 암시적 참조가 대상 형식으로 변환 될 수 있는 형식 이어야 합니다. 또는 변환 ([암시적 참조 변환을](conversions.md#implicit-reference-conversions)) boxing 변환이 나 ([Boxing 변환](conversions.md#boxing-conversions)). 명시적 참조 변환이 실패 하는 경우는 `System.InvalidCastException` throw 됩니다.

참조 변환, 암시적 또는 명시적 변환 되는 개체의 참조 id를 변경 되어서는 안됩니다. 즉, 변환은 참조 변환이 참조의 형식 변경 될 수 있지만,이 변경 되지 않습니다 형식 또는 참조 되는 개체의 값.

### <a name="unboxing-conversions"></a>Unboxing 변환

Unboxing 변환 허용 참조 형식을 명시적으로 변환할 수는 *value_type*합니다. Unboxing 변환 유형에 서 존재 `object`, `dynamic` 하 고 `System.ValueType` 에 *non_nullable_value_type*, 및에서 *interface_type* 에 *non_ nullable_value_type* 를 구현 하는 *interface_type*합니다. 또한 입력 `System.Enum` boxed를 취소할 수 있습니다 *enum_type*합니다.

Unboxing 변환 하기 위해 참조 형식에서 존재를 *nullable_type* 있으면 unboxing 변환 참조 형식에서 기본 *non_nullable_value_type* 의  *nullable_type*합니다.

값 형식 `S` 에 인터페이스 형식에서 unboxing 변환 `I` 인터페이스 형식에서 unboxing 변환 있는지 `I0` 및 `I0` 에 id 변환이 `I`.

값 형식 `S` 에 인터페이스 형식에서 unboxing 변환 `I` 인터페이스 또는 대리자 형식에서 unboxing 변환 되었으면 `I0` 고 `I0` 변환 됩니다를 `I` 또는 `I`변형 가능은 하 `I0` ([변형 변환이](interfaces.md#variance-conversion)).

개체 인스턴스에 boxed 값은 첫 번째 검사 unboxing 작업으로 구성 됩니다는 지정 된 *value_type*, 다음 인스턴스에서 값을 복사 합니다. Null 참조를 unboxing을 *nullable_type* 의 null 값을 생성 합니다 *nullable_type*합니다. 구조체에 연결할 수 형식에서 boxed `System.ValueType`구조체에 대 한 기본 클래스 이므로, ([상속](structs.md#inheritance)).

Unboxing 변환에 자세히 설명 되어 [Unboxing 변환](types.md#unboxing-conversions)합니다.

### <a name="explicit-dynamic-conversions"></a>동적 명시적 변환

형식의 식에서 명시적 동적 변환이 존재 `dynamic` 형식으로 `T`입니다. 변환 바인딩된 동적으로 ([동적 바인딩](expressions.md#dynamic-binding))를 런타임에 식의 런타임 형식에서 변환 하는 명시적 변환을 검색 하는 것이 즉 `T`합니다. 변환 작업 없이 있으면 런타임 예외가 throw 됩니다.

변환의 동적 바인딩 원하지 않는 경우 식 먼저 변환할 수 `object`, 한 다음 원하는 형식.

다음 클래스 정의 되었다고 가정 합니다.
```csharp
class C
{
    int i;

    public C(int i) { this.i = i; }

    public static explicit operator C(string s) 
    {
        return new C(int.Parse(s));
    }
}
```

다음 예제에서는 명시적 동적 변환을 보여 줍니다.
```csharp
object o  = "1";
dynamic d = "2";

var c1 = (C)o; // Compiles, but explicit reference conversion fails
var c2 = (C)d; // Compiles and user defined conversion succeeds
```

변환 하는 가장 좋은 `o` 에 `C` 명시적 참조 변환이 되도록 컴파일 타임에 합니다. 때문에 런타임 시 실패 하는이 `"1"` 팩트에 있지는 `C`합니다. 그러나 변환 `d` 하 `C` 명시적 동적 변환을로 일시 중지 런타임, 여기서 사용자 정의 변수의 런타임 형식에서 변환 `d`  --  `string` -에 `C` 발견 되 면 성공 합니다.

### <a name="explicit-conversions-involving-type-parameters"></a>형식 매개 변수를 포함 하는 명시적 변환

지정 된 형식 매개 변수는 다음과 같은 명시적 변환이 존재 `T`:

*  유효한 기본 클래스에서 `C` 의 `T` 하 `T` 의 모든 기본 클래스에서 `C` 에 `T`입니다. 에 런타임 경우 `T` 값 형식이 변환 unboxing 변환으로 실행 됩니다. 그렇지 않으면 변환이 명시적 참조 변환이 또는 id 변환을 실행 됩니다.
*  모든 인터페이스 형식에서 `T`합니다. 에 런타임 경우 `T` 값 형식이 변환 unboxing 변환으로 실행 됩니다. 그렇지 않으면 변환이 명시적 참조 변환이 또는 id 변환을 실행 됩니다.
*  `T` 하나로 *interface_type* `I` 아직 없는 암시적 변환이 제공 `T` 에 `I`입니다. 에 런타임 경우 `T` 값 형식이 변환 뒤에 변환 하는 명시적 참조 변환을 boxing 변환으로 실행 됩니다. 그렇지 않으면 변환이 명시적 참조 변환이 또는 id 변환을 실행 됩니다.
*  형식 매개 변수에서 `U` 하 `T`제공 `T` 에 따라 달라 집니다 `U` ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)). 런타임 경우 at `U` 이 값 형식이 면 `T` 및 `U` 반드시 동일한 형식이 고 변환이 수행 되지 않습니다. 그렇지 않은 경우, `T` 값 형식이 변환 unboxing 변환으로 실행 됩니다. 그렇지 않으면 변환이 명시적 참조 변환이 또는 id 변환을 실행 됩니다.

하는 경우 `T` 는 참조 형식으로 알려진, 위의 변환은 모든 변환으로 분류 됩니다 명시적 참조 ([명시적 참조 변환을](conversions.md#explicit-reference-conversions)). 하는 경우 `T` 는 참조 형식으로 알 수 없는 위의 변환은 unboxing 변환으로 분류 됩니다 ([Unboxing 변환](conversions.md#unboxing-conversions)).

위의 규칙을 허용 하지 않습니다 인터페이스가 아닌 형식에 제한 되지 않은 형식 매개 변수에서 직접 명시적 변환 다르다는 점에 놀라실 수도 있습니다. 이 규칙에 대 한 이유는 혼동을 방지 하기를 이러한 변환이 명확한의 의미 체계를 확인 하는 것입니다. 예를 들어, 다음 선언을 참조하십시오.
```csharp
class X<T>
{
    public static long F(T t) {
        return (long)t;                // Error 
    }
}
```

경우 직접 명시적 변환 `t` 하 `int` 쉽게 예상할 수 허용 되는 `X<int>.F(7)` 반환 `7L`합니다. 그러나 것 하지 형식 바인딩 시간에 숫자 것으로 알려진 경우에 표준 숫자 변환 간주 되기 때문에 있습니다. 의미 체계를 확인 하기 위해 명확 하 고 위의 예제에서는 대신 써야 합니다.
```csharp
class X<T>
{
    public static long F(T t) {
        return (long)(object)t;        // Ok, but will only work when T is long
    }
}
```

이 코드는 컴파일되지 이제 실행 되지만 `X<int>.F(7)` boxed 이후 실행 시 예외를 throw 한 다음는 `int` 로 바로 변환 될 수 없습니다는 `long`합니다.

### <a name="user-defined-explicit-conversions"></a>사용자 정의 명시적 변환

사용자 정의 명시적 변환 선택적 표준 명시적 변환이 다른 선택적 표준 명시적 변환 뒤에 사용자 정의 된 암시적 또는 명시적 변환 연산자를 실행 하 여 다음 이루어져 있습니다. 사용자 정의 명시적 변환 평가 대 한 정확한 규칙에 설명 되어 있습니다 [사용자 정의 명시적 변환 처리](conversions.md#processing-of-user-defined-explicit-conversions)합니다.

## <a name="standard-conversions"></a>표준 변환

표준 변환은 사용자 정의 변환의 일부로 발생할 수 있는 이러한 미리 정의 된 변환입니다.

### <a name="standard-implicit-conversions"></a>표준 암시적 변환

다음과 같은 암시적 변환이 표준 암시적 변환으로 분류 됩니다.

*  Identity 변환 ([Id 변환을](conversions.md#identity-conversion))
*  암시적 숫자 변환 ([암시적 숫자 변환](conversions.md#implicit-numeric-conversions))
*  암시적 nullable 변환 ([암시적 nullable 변환](conversions.md#implicit-nullable-conversions))
*  암시적 참조 변환 ([암시적 참조 변환](conversions.md#implicit-reference-conversions))
*  Boxing 변환 ([Boxing 변환](conversions.md#boxing-conversions))
*  암시적 상수 식 변환 ([암시적 동적 변환을](conversions.md#implicit-dynamic-conversions))
*  형식 매개 변수를 포함 하는 암시적 변환은 ([형식 매개 변수를 포함 하는 암시적 변환은](conversions.md#implicit-conversions-involving-type-parameters))

특히 표준 암시적 변환이 암시적 변환을 사용자 정의 제외합니다.

### <a name="standard-explicit-conversions"></a>표준 명시적 변환

표준 명시적 변환은 모든 표준 암시적 변환 및 반대 표준 암시적 변환이 존재 하는 명시적 변환의 하위 집합입니다. 즉, 표준 암시적 변환이 있는 경우 형식에서 `A` 형식으로 `B`, 형식에서 표준 명시적 변환이 존재 합니다 `A` 형식으로 `B` 형식에서 `B` 형식으로 `A`입니다.

## <a name="user-defined-conversions"></a>사용자 정의 변환

C# 확대 하 여 미리 정의 된 암시적 변환과 명시적 변환에서는 ***사용자 정의 변환은***합니다. 변환 연산자를 선언 하 여 도입 된 사용자 정의 변환 ([변환 연산자](classes.md#conversion-operators)) 클래스 및 구조체 형식입니다.

### <a name="permitted-user-defined-conversions"></a>사용자 정의 변환은 허용

C#만 선언 될 특정 사용자 정의 변환은 허용 합니다. 특히 변환 하는 기존 암시적 또는 명시적 변환을 다시 정의할 수는 없습니다.

지정 된 소스 형식에 대 한 `S` 대상 유형 및 `T`이면 `S` 또는 `T` nullable 형식 수 있도록 `S0` 및 `T0` 그렇지 않으면 해당 기본 형식 참조 `S0` 및 `T0` 됩니다 같음 `S` 고 `T` 각각. 클래스 또는 구조체를 선언할 수 원본 형식에서 변환 `S` 대상 형식으로 `T` 다음 모두 만족 하는 경우에:

*  `S0` 및 `T0` 가지 유형이 있습니다.
*  중 하나 `S0` 또는 `T0` 는 연산자 선언이 발생 하는 클래스 또는 구조체 형식입니다.
*  모두 `S0` 나 `T0` 되는 *interface_type*합니다.
*  사용자 정의 변환을 제외 하 고 변환에서 존재 하지 않습니다 `S` 하 `T` 주고 `T` 에 `S`합니다.

사용자 정의 변환에 적용 되는 제한 사항 설명에 대 한 자세한 [변환 연산자](classes.md#conversion-operators)합니다.

### <a name="lifted-conversion-operators"></a>리프트 변환 연산자

Nullable이 아닌 값 형식에서 변환 하는 사용자 정의 변환 연산자를 지정 된 `S` nullable이 아닌 값 형식 `T`, ***변환 연산자를 리프트*** 에서 변환 하는 존재 `S?` 에`T?`. 이 리프트 변환 연산자에서 래핑 해제를 수행 `S?` 에 `S` 뒤에 사용자 정의 변환 `S` 에 `T` 뒤에에서 배치 `T` 에 `T?`점을 제외 하 고, null 소중한 `S?` 값을 null로 직접 변환 `T?`합니다.

리프트 변환 연산자에 해당 기본 사용자 정의 변환 연산자와 같은 암시적 또는 명시적 분류 합니다. "사용자 정의 변환" 사용을 적용할 용어 사용자 정의 및 변환 연산자를 적용 되지 않습니다.

### <a name="evaluation-of-user-defined-conversions"></a>사용자 정의 변환에 대 한 평가

사용자 정의 변환이 호출 해당 형식에서 값을 변환 합니다 ***원본 유형***를 다른 형식으로 호출 합니다 ***대상 유형***. 사용자 정의 변환의 평가 센터 찾기에는 ***가장 구체적인*** 특정 소스 및 대상 형식에 대 한 사용자 정의 변환 연산자입니다. 이 결정 여러 단계로 나뉩니다.

*  클래스 및 사용자 정의 변환 연산자 고려해 야 하는 구조체의 집합을 찾기. 이 집합의 소스 형식 및 해당 기본 클래스 및 대상 형식과 해당 기본 클래스 (클래스 및 구조체는 사용자 정의 연산자를 선언할 수 있습니다 하 고 비 클래스 형식에 기본 클래스가 없고 있는 암시적 가정)으로 구성 됩니다. 원본 또는 대상 유형이 경우이 단계를 위해 한 *nullable_type*등의 기본 형식 대신 사용 됩니다.
*  형식의 해당 집합에서 결정 하는 사용자 정의 변환 연산자를 리프트 적용할 수 있습니다. 변환 연산자를 적용 하기 위해 있어야 표준 변환을 수행할 수 있습니다 ([표준 변환](conversions.md#standard-conversions)) 피연산자 원본 형식에서 연산자 및 해당 형식의 표준 변환을 수행할 수 있어야 대상 형식으로 연산자의 결과 형식입니다.
*  해당 사용자 정의 연산자의 집합에서 명확 하 게 가장 관련 된 어떤 운영자를 결정 합니다. 일반적인 측면에서 가장 구체적인 연산자는 피연산자 형식이 소스 형식으로 "가장 가까운" 이며 결과 형식이 대상 형식으로 "가장 가까운" 연산자를 사용 합니다. 사용자 정의 변환 연산자는 리프트 변환 연산자 보다 우선 합니다. 가장 구체적인 사용자 정의 변환 연산자를 설정 하는 것에 대 한 정확한 규칙은 다음 섹션에 정의 됩니다.

가장 구체적인 사용자 정의 변환 연산자를 식별 한 후 사용자 정의 변환의 실제 실행에는 최대 세 가지 단계가 포함 됩니다.

*  먼저 필요한 경우 원본 유형에 서 또는 리프트 된 사용자 정의 변환 연산자의 피연산자 형식으로 변환 하는 표준 변환이 수행 합니다.
*  다음으로 변환 하는 데 사용자 정의 또는 리프트 변환 연산자를 호출 합니다.
*  마지막으로, 필요한 경우에 대상 형식으로 변환의 사용자 정의 또는 리프트 된 연산자의 결과 형식은의 표준 변환이 수행 합니다.

사용자 정의 변환 되지의 평가 둘 이상의 사용자 정의 또는 리프트 변환 연산자에 포함 됩니다. 즉, 형식 변환 `S` 형식으로 `T` 에서 사용자 정의 변환을 실행 되지 `S` 에 `X` 에서 사용자 정의 변환을 실행 하 고 `X` 를 `T`합니다.

사용자 정의 된 암시적 또는 명시적 변환에 대 한 평가의 정확한 정의 다음 섹션에서 제공 됩니다. 정의 사용 하면 다음과 같은 용어가 사용:

*  표준 암시적 변환 경우 ([표준 암시적 변환이](conversions.md#standard-implicit-conversions)) 형식에서 존재 `A` 형식으로 `B`, 모두 및 `A` 나 `B` 는 *interface_type*s, 한 다음 `A` 이라고 ***에 의해 포함 된*** `B`, 및 `B` 이라고 ***encompass*** `A`합니다.
*  합니다 ***최상위 형식*** 형식 집합이 집합의 다른 모든 형식을 포함 하는 형식입니다. 다른 모든 형식을 포함 하는 단일 형식이 없는, 하는 경우 집합에 최상위 형식이 없습니다. 직관적인 측면에서 최상위 형식은 집합의 "큰" 유형에-는 각각 다른 형식의 암시적으로 변환할 수는 형식입니다.
*  합니다 ***형식이 포함 된 가장*** 형식 집합이 집합의 다른 모든 형식으로 포함 되는 형식입니다. 단일 형식이 없는 다른 모든 형식으로 롤포워드되지 않았습니다, 경우 집합에는 형식 가장 하지 않습니다 포함 했습니다. 직관적인 측면에서 최하위 형식은 집합의 "작은" 형식-각 다른 형식에 암시적으로 변환할 수는 형식입니다.

### <a name="processing-of-user-defined-implicit-conversions"></a>암시적 사용자 정의 변환 처리

형식에서 사용자 정의 된 암시적 변환이 `S` 형식으로 `T` 다음과 같이 처리 됩니다.

*  형식을 확인할 `S0` 고 `T0`입니다. 하는 경우 `S` 또는 `T` nullable 형식 `S0` 하 고 `T0` 가 해당 기본 형식인 경우이 고, 그렇지 `S0` 및 `T0` 같은지 `S` 및 `T` 각각.
*  형식의 집합을 찾을 `D`는 사용자 정의 변환 연산자 고려해 야 합니다. 이 집합으로 구성 됩니다 `S0` (하는 경우 `S0` 는 클래스 또는 구조체)의 기본 클래스 `S0` (경우 `S0` 클래스인), 및 `T0` (경우 `T0` 클래스 또는 구조체).
*  해당 사용자 정의 및 리프트 변환 연산자 집합을 찾을 `U`합니다. 이 구성 된이 집합을 사용자 정의 및 리프트 된 암시적 변환 연산자는 클래스 또는 구조체 선언 `D` 포괄 하는 형식에서 변환 하는 `S` 에 의해 포함 된 형식으로 `T`입니다. 경우 `U` 는 비어 있는 경우 변환이 정의 되지 않으며 컴파일 타임 오류가 발생 합니다.
*  가장 구체적인 원본 유형을 찾습니다 `SX`에서 연산자의 `U`:
    * 연산자 중 하나가 되 면 `U` 에서 변환 `S`, 한 다음 `SX` 는 `S`합니다.
    * 그렇지 않으면 `SX` 원본 형식에서 연산자의 결합 된 집합의 최하위 형식인 `U`합니다. 가장 하나만 포함 하는 경우에 형식을 찾을 수 없는 한 변환이 모호 하 고 컴파일 타임 오류가 발생 하는 키를 누릅니다.
*  가장 구체적인 대상 형식과 찾을 `TX`에서 연산자의 `U`:
    * 연산자 중 하나가 되 면 `U` 변환할 `T`, 한 다음 `TX` 는 `T`합니다.
    * 그렇지 않으면 `TX` 대상 유형의에서 연산자의 조합된 된 집합의 최상위 형식인 `U`합니다. 정확히 하나의 최상위 형식 찾을 수 없는 경우 다음 변환이 모호 합니다. 및 컴파일 타임 오류가 발생 합니다.
*  가장 구체적인 변환 연산자를 찾습니다.
    * 하는 경우 `U` 로 변환 하는 사용자 정의 변환 연산자를 하나만 포함 `SX` 에 `TX`, 가장 구체적인 변환 연산자입니다.
    * 그렇지 않고 `U` 로 변환 하는 정확히 하나의 리프트 변환 연산자를 포함 `SX` 에 `TX`, 가장 구체적인 변환 연산자입니다.
    * 이 고, 그렇지 변환이 모호 하 고 컴파일 타임 오류가 발생 합니다.
*  마지막으로 변환이 적용 됩니다.
    * 하는 경우 `S` 아닙니다 `SX`의 표준 암시적 변환이 다음 `S` 에 `SX` 수행 됩니다.
    * 변환할 가장 구체적인 변환 연산자가 호출 `SX` 에 `TX`입니다.
    * 하는 경우 `TX` 아닙니다 `T`의 표준 암시적 변환이 다음 `TX` 에 `T` 수행 됩니다.

### <a name="processing-of-user-defined-explicit-conversions"></a>사용자 정의 명시적 변환 처리

형식에서 사용자 정의 명시적 변환 `S` 형식으로 `T` 다음과 같이 처리 됩니다.

*  형식을 확인할 `S0` 고 `T0`입니다. 하는 경우 `S` 또는 `T` nullable 형식 `S0` 하 고 `T0` 가 해당 기본 형식인 경우이 고, 그렇지 `S0` 및 `T0` 같은지 `S` 및 `T` 각각.
*  형식의 집합을 찾을 `D`는 사용자 정의 변환 연산자 고려해 야 합니다. 이 집합으로 구성 됩니다 `S0` (하는 경우 `S0` 는 클래스 또는 구조체)의 기본 클래스 `S0` (경우 `S0` 클래스인), `T0` (경우 `T0` 클래스 또는 구조체), 및의 기본 클래스 `T0` (경우 `T0`는 클래스).
*  해당 사용자 정의 및 리프트 변환 연산자 집합을 찾을 `U`합니다. 이 집합은 사용자 정의 및 구성 리프트 된 암시적 또는 명시적 변환 연산자는 클래스 또는 구조체 선언 `D` 포괄 하는 형식에서 변환 하는 하거나에 의해 포함 된 `S` 에의해포함된클래스나형식`T`. 경우 `U` 는 비어 있는 경우 변환이 정의 되지 않으며 컴파일 타임 오류가 발생 합니다.
*  가장 구체적인 원본 유형을 찾습니다 `SX`에서 연산자의 `U`:
    * 연산자 중 하나가 되 면 `U` 에서 변환 `S`, 한 다음 `SX` 는 `S`합니다.
    * 그렇지 않으면 연산자 중 하나 `U` 을 포함 하는 형식에서 변환 `S`, 다음 `SX` 원본 유형의 해당 연산자의 조합된 된 집합의 최하위 형식입니다. 없는 대부분 포함 하는 경우에 형식을 찾을 수를 한 변환이 모호 하 고 컴파일 타임 오류가 발생 하는 키를 누릅니다.
    * 그렇지 않으면 `SX` 결합된 된 집합에 있는 연산자의 원본 유형 중에서 최상위 형식인 `U`합니다. 정확히 하나의 최상위 형식 찾을 수 없는 경우 다음 변환이 모호 합니다. 및 컴파일 타임 오류가 발생 합니다.
*  가장 구체적인 대상 형식과 찾을 `TX`에서 연산자의 `U`:
    * 연산자 중 하나가 되 면 `U` 변환할 `T`, 한 다음 `TX` 는 `T`합니다.
    * 그렇지 않으면 연산자 중 하나 `U` 하 여 포함 된 형식으로 변환 `T`, 다음 `TX` 대상 유형의 해당 연산자의 조합된 된 집합의 최상위 형식입니다. 정확히 하나의 최상위 형식 찾을 수 없는 경우 다음 변환이 모호 합니다. 및 컴파일 타임 오류가 발생 합니다.
    * 그렇지 않으면 `TX` 대상 유형의에서 연산자의 조합된 된 집합의 최하위 형식인 `U`합니다. 없는 대부분 포함 하는 경우에 형식을 찾을 수를 한 변환이 모호 하 고 컴파일 타임 오류가 발생 하는 키를 누릅니다.
*  가장 구체적인 변환 연산자를 찾습니다.
    * 하는 경우 `U` 로 변환 하는 사용자 정의 변환 연산자를 하나만 포함 `SX` 에 `TX`, 가장 구체적인 변환 연산자입니다.
    * 그렇지 않고 `U` 로 변환 하는 정확히 하나의 리프트 변환 연산자를 포함 `SX` 에 `TX`, 가장 구체적인 변환 연산자입니다.
    * 이 고, 그렇지 변환이 모호 하 고 컴파일 타임 오류가 발생 합니다.
*  마지막으로 변환이 적용 됩니다.
    * 하는 경우 `S` 아닙니다 `SX`에서 표준 명시적 변환이 다음 `S` 에 `SX` 수행 됩니다.
    * 변환할 가장 구체적인 사용자 정의 변환 연산자가 호출 `SX` 에 `TX`입니다.
    * 하는 경우 `TX` 아닙니다 `T`에서 표준 명시적 변환이 다음 `TX` 에 `T` 수행 됩니다.

## <a name="anonymous-function-conversions"></a>익명 함수 변환

*anonymous_method_expression* 하거나 *lambda_expression* 익명 함수로 분류 됩니다 ([익명 함수 식](expressions.md#anonymous-function-expressions)). 식 형식 없지만 호환 되는 대리자 형식 또는 식 트리 형식을 암시적으로 변환할 수 있습니다. 특히, 익명 함수 `F` 대리자 형식과 호환 되는 `D` 제공 합니다.

*  하는 경우 `F` 포함를 *anonymous_function_signature*, 한 다음 `D` 및 `F` 매개 변수 수가 같아야 합니다.
*  경우 `F` 없습니다를 *anonymous_function_signature*, 한 다음 `D` 의 매개 변수가 없는으로 모든 형식의 매개 변수를 0 개 이상 있을 수 있습니다 `D` 에 `out` 매개 변수 한정자.
*  하는 경우 `F` 에 명시적으로 형식화 된 매개 변수 목록이, 각 매개 변수에 `D` 에서 해당 매개 변수로 동일한 형식 및 한정자가 `F`입니다.
*  하는 경우 `F` 는 암시적으로 형식화 된 매개 변수 목록이 `D` 아무런 `ref` 또는 `out` 매개 변수입니다.
*  경우 본문 `F` 이 고 식 `D` 에 `void` 반환 형식 또는 `F` 는 비동기 및 `D` 반환 형식이 `Task`때 각 매개 변수에 `F` 의 형식이 지정 되며를 해당 매개 변수에 `D`, 본문 `F` 유효한 식입니다 (wrt [식을](expressions.md))으로 사용할 수 있는 *statement_expression* ([식 문은](statements.md#expression-statements)).
*  경우 본문 `F` 이 고, 문 블록 `D` 에 `void` 반환 형식 또는 `F` 는 비동기 및 `D` 반환 형식이 `Task`때 각 매개 변수에 `F` 의 형식이 지정 되며 해당 매개 변수 `D`, 본문 `F` 유효한 문 블록 (wrt [블록](statements.md#blocks)) 않는 `return` 문에서 식을 지정 합니다.
*  경우 본문 `F` 식, 및 *중 하나* `F` 은 비동기가 아닌 및 `D` void가 아닌 반환 형식이 `T`를 *또는* `F` 는 비동기 및 `D` 반환 형식을 갖는 `Task<T>`때 각 매개 변수에 `F` 에서 해당 매개 변수의 형식이 지정 되며 `D`, 본문 `F` 유효한 식입니다 (wrt [ 식을](expressions.md))로 암시적으로 변환할 수는 `T`합니다.
*  경우 본문 `F` , 문 블록은 및 *어느* `F` 은 비동기가 아닌 및 `D` void가 아닌 반환 형식이 `T`, *또는* `F` 는 비동기 및 `D` 반환 형식이 `Task<T>`때 각 매개 변수에 `F` 에서 해당 매개 변수의 형식이 지정 되며 `D`, 본문 `F` 는 유효한 문 블록 (wrt [블록 ](statements.md#blocks)) 각 연결할 수 없는 끝점을 사용 하 여 `return` 문은 암시적으로 변환할 수 있는 식을 지정 `T`합니다.

작업 형식에 대 한이 섹션에서는 약식 간 결함을 위해 `Task` 하 고 `Task<T>` ([비동기 함수](classes.md#async-functions)).

람다 식 `F` 는 식 트리 형식과 호환 되는지 `Expression<D>` 하는 경우 `F` 대리자 형식과 호환 되는 `D`합니다. Note 무명 메서드, 람다 식만에 적용 되지 않습니다.

특정 람다 식을 식 트리 형식으로 변환할 수 없습니다: 경우에 변환을 *존재*, 컴파일 시 실패 합니다. 이 경우 람다 식입니다.

*  에 *블록* 본문
*  단순 또는 복합 할당 연산자를 포함합니다.
*  동적으로 바인딩된 식을 포함
*  비동기는

이 예제에서는 제네릭 대리자 형식을 사용할 `Func<A,R>` 형식의 인수를 사용 하는 함수를 나타내는 `A` 형식의 값을 반환 하 고 `R`:
```csharp
delegate R Func<A,R>(A arg);
```

할당에서
```csharp
Func<int,int> f1 = x => x + 1;                 // Ok

Func<int,double> f2 = x => x + 1;              // Ok

Func<double,int> f3 = x => x + 1;              // Error

Func<int, Task<int>> f4 = async x => x + 1;    // Ok
```
각 익명 함수의 매개 변수와 반환 형식이 익명 함수는 할당 된 변수 형식에서 결정 됩니다.

첫 번째 할당에서는 대리자 형식으로 익명 함수를 성공적으로 변환 `Func<int,int>` 때문에, `x` 형식이 지정 되며 `int`합니다 `x+1` 형식으로 암시적으로 변환할 수 있는 유효한 식입니다 `int`합니다.

마찬가지로 두 번째 할당을 성공적으로 익명 함수를 대리자 형식 변환 `Func<int,double>` 있으므로 결과인 `x+1` (형식의 `int`) 형식으로 암시적으로 변환할 수 `double`합니다.

그러나 세 번째 할당 되므로 컴파일 타임 오류가 때 `x` 형식이 지정 되며 `double`, 결과인 `x+1` (형식의 `double`) 형식으로 암시적으로 변환 되지 않습니다 `int`합니다.

네 번째 할당 대리자 형식으로 익명 비동기 함수를 성공적으로 변환 `Func<int, Task<int>>` 있으므로 결과인 `x+1` (형식의 `int`) 결과 유형으로 암시적으로 변환할 수 `int` 작업형식의`Task<int>`.

익명 함수는 오버 로드 확인에 영향을 줄 및 형식 유추에 참여할 수 있습니다. 참조 [멤버 함수](expressions.md#function-members) 자세한 내용은 합니다.

### <a name="evaluation-of-anonymous-function-conversions-to-delegate-types"></a>대리자 형식으로 익명 함수 변환에 대 한 평가

익명 함수 이며 평가 당시 활성 상태인 캡처된 외부 변수 (비어 있을 수 있는) 집합을 참조 하는 대리자 인스턴스를 생성 하는 익명 함수는 대리자 형식으로 변환 합니다. 대리자를 호출 하면 익명 함수 본문 실행 됩니다. 본문의 코드는 대리자가 참조 하는 캡처된 외부 변수 집합을 사용 하 여 실행 됩니다.

익명 함수에서 생성 된 대리자의 호출 목록에는 단일 항목을 포함 합니다. 정확한 대상 개체 및 대리자 대상 메서드의 지정 되지 않습니다. 특히 지정 되지 않습니다 대리자의 대상 개체 인지 `null`, `this` 바깥쪽 함수 멤버 또는 일부 다른 개체의 값입니다.

동일한 대리자 형식에 동일한 (비어 있을 수 있는) 인스턴스 집합을 캡처된 외부 변수를 사용 하 여과 의미상 동일 익명 함수 변환 허용 (있고 필요 하지 않습니다) 동일한 대리자 인스턴스를 반환 합니다. 과 의미상 동일 용어는 익명 함수 실행을, 모든 경우에 생성 됩니다 동일한 인수를 지정 된 동일한 효력을 평균값으로 사용 됩니다. 이 규칙은 최적화 되도록 다음과 같은 코드를 허용 합니다.

```csharp
delegate double Function(double x);

class Test
{
    static double[] Apply(double[] a, Function f) {
        double[] result = new double[a.Length];
        for (int i = 0; i < a.Length; i++) result[i] = f(a[i]);
        return result;
    }

    static void F(double[] a, double[] b) {
        a = Apply(a, (double x) => Math.Sin(x));
        b = Apply(b, (double y) => Math.Sin(y));
        ...
    }
}
```

두 익명 함수 대리자를 동일한 (비어 있음) 외부 캡처된 변수의 및 익명 함수 의미상 동일 하므로 설정 하므로, 컴파일러는 동일한 대상 메서드를 참조 하는 대리자가 하도록 허용 됩니다. 실제로 컴파일러는 모두 익명 함수 식에서 똑같은 대리자 인스턴스를 반환 하도록 허용 됩니다.

### <a name="evaluation-of-anonymous-function-conversions-to-expression-tree-types"></a>익명 함수 식 트리 형식으로의 변환의 평가

식 트리를 생성 하는 익명 함수는 식 트리 형식으로 변환 ([식 트리 형식](types.md#expression-tree-types)). 보다 정확 하 게 평가 익명 함수 변환의 익명 함수 자체의 구조를 나타내는 개체 구조를 생성 하면 됩니다. 만들기 위한 정확한 프로세스 뿐만 아니라 식 트리를 정확한 구조는 정의 된 구현입니다.

### <a name="implementation-example"></a>구현 예제

이 섹션에서는 다른 C# 구문 측면에서 익명 함수 변환의 가능한 구현을 설명 합니다. 여기에 설명 된 구현은 Microsoft C# 컴파일러에 의해 사용 되는 동일한 원칙에 기반 하지만 위임된 구현 되지는 않습니다 자신과 하나만 가능한 것입니다. 아주 잠시 동안만이 사양의 범위 외부의 정확한 의미 체계는 식 트리로 변환 언급 합니다.

이 섹션의 나머지 부분은 다른 특징을 가진 익명 함수를 포함 하는 코드의 몇 가지 예를 제공 합니다. 각 예를 들어만 다른 C# 구문을 사용 하는 코드를 해당 번역이 제공 됩니다. 이 예제에서는 식별자에에서 `D` 다음 대리자 형식을 나타내는으로 간주 됩니다.
```csharp
public delegate void D();
```

가장 간단한 형태의 익명 함수를은 없는 외부 변수를 캡처하는 하나입니다.
```csharp
class Test
{
    static void F() {
        D d = () => { Console.WriteLine("test"); };
    }
}
```

익명 함수의 코드가 배치 되는 컴파일러에서 생성 된 정적 메서드를 참조 하는 대리자 인스턴스화를 변환할 수 있습니다.
```csharp
class Test
{
    static void F() {
        D d = new D(__Method1);
    }

    static void __Method1() {
        Console.WriteLine("test");
    }
}
```

다음 예제에서는 익명 함수 참조의 인스턴스 멤버 `this`:
```csharp
class Test
{
    int x;

    void F() {
        D d = () => { Console.WriteLine(x); };
    }
}
```

익명 함수의 코드를 포함 하는 컴파일러에서 생성 된 인스턴스 메서드를 변환할 수 있습니다.
```csharp
class Test
{
    int x;

    void F() {
        D d = new D(__Method1);
    }

    void __Method1() {
        Console.WriteLine(x);
    }
}
```

이 예제에서는 익명 함수는 지역 변수를 캡처합니다.
```csharp
class Test
{
    void F() {
        int y = 123;
        D d = () => { Console.WriteLine(y); };
    }
}
```

로컬 변수의 수명은 이제를 확장 하 이상 익명 함수 대리자의 수명입니다. 이 지역 변수를 컴파일러에서 생성 된 클래스의 필드에 "호이스팅" 하 여 구현할 수 있습니다. 지역 변수의 인스턴스화 ([로컬 변수의 인스턴스화](expressions.md#instantiation-of-local-variables)) 인스턴스의 필드에 액세스에 해당 하는 로컬 변수에 액세스 하는 컴파일러에서 생성 된 클래스의 인스턴스를 만드는 다음 해당 컴파일러에서 생성 된 클래스입니다. 또한 익명 함수는 컴파일러에서 생성 된 클래스의 인스턴스 메서드 됩니다.
```csharp
class Test
{
    void F() {
        __Locals1 __locals1 = new __Locals1();
        __locals1.y = 123;
        D d = new D(__locals1.__Method1);
    }

    class __Locals1
    {
        public int y;

        public void __Method1() {
            Console.WriteLine(y);
        }
    }
}
```

마지막으로 다음 익명 함수 캡처 `this` 다른 수명 사용 하 여 두 개의 로컬 변수 뿐만 아니라:
```csharp
class Test
{
    int x;

    void F() {
        int y = 123;
        for (int i = 0; i < 10; i++) {
            int z = i * 2;
            D d = () => { Console.WriteLine(x + y + z); };
        }
    }
}
```

각 문에 대해 컴파일러에서 생성 된 클래스를 만들 여기서 블록에 지역 변수는 다른 블록에서 지역 변수는 독립적인 수명 수 있도록 캡처됩니다. 인스턴스의 `__Locals2`, 로컬 변수를 포함 하는 내부 문 블록에 대 한 컴파일러에서 생성 된 클래스 `z` 의 인스턴스를 참조 하는 필드와 `__Locals1`합니다.  인스턴스의 `__Locals1`, 로컬 변수를 포함 하는 외부 문 블록에 대 한 컴파일러에서 생성 된 클래스 `y` 를 참조 하는 필드와 `this` 바깥쪽 함수 멤버의 합니다. 이러한 데이터 구조에 연결할 수 있기를 사용 하 여 모든 인스턴스를 통해 외부 변수 캡처할 `__Local2`, 익명 함수의 코드를 해당 클래스의 인스턴스 메서드로 구현할 수 있으므로 합니다.

```csharp
class Test
{
    void F() {
        __Locals1 __locals1 = new __Locals1();
        __locals1.__this = this;
        __locals1.y = 123;
        for (int i = 0; i < 10; i++) {
            __Locals2 __locals2 = new __Locals2();
            __locals2.__locals1 = __locals1;
            __locals2.z = i * 2;
            D d = new D(__locals2.__Method1);
        }
    }

    class __Locals1
    {
        public Test __this;
        public int y;
    }

    class __Locals2
    {
        public __Locals1 __locals1;
        public int z;

        public void __Method1() {
            Console.WriteLine(__locals1.__this.x + __locals1.y + z);
        }
    }
}
```

익명 함수 식 트리로 변환 하는 경우에 기술은 여기 적용할 로컬 변수를 캡처를 사용할 수 있습니다: 식 트리에서 컴파일러에서 생성 된 개체에 대 한 참조를 저장 될 수 있으며 로컬 변수에 액세스할 수 있습니다. 이러한 개체에 액세스 하는 필드 표시 합니다. 이 방식의 장점은 "리프트" 로컬 변수를 식 트리 및 대리자 간에 공유할 수 있도록 한다는 점입니다.

## <a name="method-group-conversions"></a>메서드 그룹 변환

암시적으로 변환 ([암시적 변환을](conversions.md#implicit-conversions)) 메서드 그룹에서 존재 ([식 분류](expressions.md#expression-classifications)) 호환 되는 대리자 형식입니다. 지정 된 대리자 형식 `D` 및 식을 `E` 메서드 그룹으로 분류 되는의 암시적 변환이 존재 `E` 에 `D` 경우 `E` 해당 정규형 (에서 적용 되는 하나 이상의 메서드를 포함 [적용 가능한 함수 멤버](expressions.md#applicable-function-member))의 한정자 및 형식 매개 변수는 사용 하 여 생성 된 인수 목록에 `D`다음에 설명 된 대로 합니다.

메서드 그룹 변환의 컴파일 타임 응용 프로그램 `E` 대리자 형식에 `D` 다음에 설명 되어 있습니다. 암시적 변환이 존재 `E` 에 `D` 오류 없이 컴파일 타임 응용 프로그램 변환의 성공 한다는 사실을 보장 하지 않습니다.

*  단일 메서드 `M` 메서드 호출에 해당 선택 ([메서드 호출](expressions.md#method-invocations)) 형식의 `E(A)`, 다음 수정:
    * 인수 목록 `A` 은 식, 변수 및 형식 및 한정자를 사용 하 여 각 분류 목록 (`ref` 또는 `out`)에서 해당 매개 변수를 *formal_parameter_list* 의`D`.
    * 간주 후보 메서드는 해당 기본 폼에 적용 되는 방법만 ([적용 가능한 함수 멤버](expressions.md#applicable-function-member)), 해당 확장된 형식에만 적용할 수는 없습니다.
*  하는 경우의 알고리즘 [메서드 호출](expressions.md#method-invocations) 컴파일 타임 오류가 발생 하는 다음 오류를 발생 시킵니다. 알고리즘은 단일 최상의 메서드를 생성 하는 고, 그렇지 `M` 는 동일한 매개 변수 수가 `D` 변환이 있는 것으로 간주 됩니다.
*  선택한 메서드 `M` 호환 되어야 합니다 ([대리자 호환성](delegates.md#delegate-compatibility)) 대리자 형식을 사용 하 여 `D`, 또는 그렇지 않으면 컴파일 타임 오류가 발생 합니다.
*  경우 선택한 메서드 `M` 되는 인스턴스 메서드를 사용 하 여 연결 된 인스턴스 식이 `E` 대리자의 대상 개체를 결정 합니다.
*  선택한 메서드 M 확장 메서드가 인스턴스 식에는 멤버 액세스를 사용 하 여 표시 되는 경우 해당 인스턴스 식이 대리자의 대상 개체를 결정 합니다.
*  변환의 결과 형식의 값 `D`, 선택한 메서드 및 대상 개체를 참조 하는 새로 만든된 대리자 즉 합니다.
*  이 프로세스는 확장 메서드는 대리자를 만들 경우 발생할 수 있습니다는 알고리즘 [메서드 호출](expressions.md#method-invocations) 인스턴스 메서드를 찾지 못하면 하지만 호출 처리 성공 `E(A)` 확장으로 메서드 호출 ([확장 메서드 호출](expressions.md#extension-method-invocations)). 따라서 만든 대리자의 첫 번째 인수가 뿐만 아니라 확장 메서드를 캡처합니다.

다음 예제에서는 메서드 그룹 변환 하는 방법을 보여 줍니다.
```csharp
delegate string D1(object o);

delegate object D2(string s);

delegate object D3();

delegate string D4(object o, params object[] a);

delegate string D5(int i);

class Test
{
    static string F(object o) {...}

    static void G() {
        D1 d1 = F;            // Ok
        D2 d2 = F;            // Ok
        D3 d3 = F;            // Error -- not applicable
        D4 d4 = F;            // Error -- not applicable in normal form
        D5 d5 = F;            // Error -- applicable but not compatible

    }
}
```

에 대 한 할당 `d1` 메서드 그룹을 암시적으로 변환 `F` 형식의 값으로 `D1`입니다.

에 대 한 할당 `d2` 에 더 적게 파생 된 (변성이) 매개 변수 형식 및 더 파생 (공변 (covariant)) 반환 형식 메서드에 대리자를 만드는 방법을 보여 줍니다.

에 대 한 할당 `d3` 메서드에 적용할 수 없는 경우 변환 작업 없이 존재 하는 방법을 보여 줍니다.

에 대 한 할당 `d4` 메서드 일반적인 형태로 적용할 수 있어야 하는 방법을 보여 줍니다.

에 대 한 할당 `d5` 메서드와 대리자의 매개 변수 및 반환 형식을 참조 형식에 대해서만 다를 수는 방법을 보여 줍니다.

모든 다른 암시적 변환과 명시적 변환, 마찬가지로 캐스트 연산자를 메서드 그룹 변환 명시적으로 하는 데 사용할 수 있습니다. 따라서 예제
```csharp
object obj = new EventHandler(myDialog.OkClick);
```
대신 작성할 수 있습니다.
```csharp
object obj = (EventHandler)myDialog.OkClick;
```

메서드 그룹 오버 로드 확인에 영향을 줄 및 형식 유추에 참여할 수 있습니다. 참조 [멤버 함수](expressions.md#function-members) 자세한 내용은 합니다.

메서드 그룹 변환의 런타임 평가 다음과 같이 진행 됩니다.

*  대리자의 대상 개체와 연결 된 인스턴스 식에서 도달한 경우 컴파일 타임에 선택한 메서드는 인스턴스 메서드 또는 인스턴스 메서드로 액세스 하는 확장 메서드는, `E`:
    * 인스턴스 식은 계산 됩니다. 이 평가 예외를 발생 시키는 경우에 추가 단계 없이 실행 됩니다.
    * 인스턴스 식의 경우는 *reference_type*, 인스턴스 식에서 계산 된 값은 대상 개체입니다. 경우 선택한 메서드는 인스턴스 메서드를 이며 대상 개체가 `null`, `System.NullReferenceException` throw 되 고 추가 단계 없이 실행 됩니다.
    * 인스턴스 식의 경우는 *value_type*, boxing 작업이 ([Boxing 변환](types.md#boxing-conversions)) 개체에 값을 변환 하기 위해 수행 됩니다 대상 개체가 되 고이 개체 및 합니다.
*  선택한 메서드는 정적 메서드 호출의 일부인 그렇지 않은 경우 및 대리자의 대상 개체가 `null`합니다.
*  대리자 형식의 새 인스턴스를 `D` 할당 됩니다. 새 인스턴스를 할당할 수 있는 충분 한 메모리가 없을 경우는 `System.OutOfMemoryException` throw 되 고 추가 단계 없이 실행 됩니다.
*  위의 계산 대상 개체에 대 한 참조 및 컴파일 타임에 확인 된 메서드에 대 한 참조를 사용 하 여 새 대리자 인스턴스를 초기화 됩니다.
