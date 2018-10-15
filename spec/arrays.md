# <a name="arrays"></a>배열

배열에는 여러 가지 계산 된 인덱스를 통해 액세스할 수 있는 변수를 포함 하는 데이터 구조입니다. 배열의 요소를 배열에 포함 된 변수는 동일한 형식의 모든 및이 형식을 배열의 요소 형식 이라고 합니다.

배열 차수가 각 배열 요소와 연결 된 인덱스의 수를 결정 합니다. 배열의 차수는 배열의 차수 라고도 합니다. 배열 차수 1을 사용 하 여 호출 되는 ***1 차원 배열***합니다. 하나를 호출 하는 보다 큰 차수의 배열을 ***다차원 배열***합니다. 특정 크기의 다차원 배열은 2 차원 배열, 3 차원 배열 및 등이 라고도 합니다.

배열의 각 차원에 연결 된 길이가 정수 계열 숫자 보다 크거나 0입니다. 차원 길이 배열 형식에 속하지 않는 하지만 런타임 시 배열 형식의 인스턴스가 만들어질 때 설정 됩니다. 해당 차원에 대 한 인덱스의 유효한 범위를 결정 하는 차원의 길이: 길이의 차원에 대 한 `N`, 인덱스에서 까지입니다 `0` 에 `N - 1` 포괄 합니다. 배열에 있는 요소의 총 수는 배열의 각 차원 길이 제품입니다. 배열의 차원 중 하나 이상이 0 길이의 경우 비워 배열 이라고 합니다.

배열의 요소 형식은 배열 형식을 비롯한 어떤 형식도 될 수 있습니다.

## <a name="array-types"></a>배열 형식

배열 형식으로 기록 되는 *non_array_type* 뒤에 하나 이상의 *rank_specifier*s:

```antlr
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
```

A *non_array_type* 중인 *유형* 즉 자체는 *array_type*합니다.

배열 형식의 차수를 지정 하 여 가장 왼쪽에 있는 *rank_specifier* 에 *array_type*: A *rank_specifier* 배열 차수 1을 사용 하 여 배열 임을 나타냅니다와 숫자 "`,`" 토큰이 합니다 *rank_specifier*합니다.

배열 형식의 요소 형식은 형식에서 가장 왼쪽에 있는 삭제를 일으키는 *rank_specifier*:

*  형식의 배열 형식 `T[R]` rank 통한 배열이 `R` 비 배열 요소 형식 및 `T`합니다.
*  형식의 배열 형식 `T[R][R1]...[Rn]` rank 통한 배열이 `R` 이 고 요소 형식이 `T[R1]...[Rn]`합니다.

실제로 *rank_specifier*의바로 최종 비 배열 요소 형식 앞에 왼쪽에서 읽힙니다. 형식 `int[][,,][,]` 의 2 차원 배열의 3 차원 배열의 1 차원 배열이 `int`합니다.

배열 형식의 값은 런타임 시 수 `null` 또는 배열 형식의 인스턴스에 대 한 참조입니다.

### <a name="the-systemarray-type"></a>System.Array 형식

형식 `System.Array` 모든 배열 형식의 추상 기본 형식입니다. 암시적 참조 변환 ([암시적 참조 변환](conversions.md#implicit-reference-conversions)) 모든 배열 형식에서 존재 `System.Array`, 및 명시적 참조 변환이 ([명시적 참조 변환을](conversions.md#explicit-reference-conversions)) 있습니다. `System.Array` 모든 배열 형식입니다. 사실은 `System.Array` 자체는 *array_type*합니다. 아니라는 것을 *class_type* 모든에서 *array_type*가 파생 됩니다.

런타임 형식의 값에 `System.Array` 수 `null` 또는 배열 형식의 모든 인스턴스에 대 한 참조입니다.

### <a name="arrays-and-the-generic-ilist-interface"></a>배열 및 제네릭 IList 인터페이스

1 차원 배열 `T[]` 인터페이스를 구현 `System.Collections.Generic.IList<T>` (`IList<T>` 줄여서)와 해당 기본 인터페이스입니다. 따라서 암시적 변환이 있기 `T[]` 에 `IList<T>` 와 해당 기본 인터페이스입니다. 또한에서 암시적 참조 변환이 없는 경우 `S` 에 `T` 한 다음 `S[]` 구현 `IList<T>` 에서 암시적 참조 변환 되며 `S[]` 를 `IList<T>` 및 기본 인터페이스 ( [암시적 참조 변환](conversions.md#implicit-reference-conversions)). 명시적 참조 변환이 없는 경우 `S` 하 `T` 에서 명시적 참조 변환이 됩니다 `S[]` 하 `IList<T>` 와 해당 기본 인터페이스 ([명시적 참조 변환을](conversions.md#explicit-reference-conversions)). 예를 들어:
```csharp
using System.Collections.Generic;

class Test
{
    static void Main() {
        string[] sa = new string[5];
        object[] oa1 = new object[5];
        object[] oa2 = sa;

        IList<string> lst1 = sa;                    // Ok
        IList<string> lst2 = oa1;                   // Error, cast needed
        IList<object> lst3 = sa;                    // Ok
        IList<object> lst4 = oa1;                   // Ok

        IList<string> lst5 = (IList<string>)oa1;    // Exception
        IList<string> lst6 = (IList<string>)oa2;    // Ok
    }
}
```

할당 `lst2 = oa1` 변환 이후 컴파일 타임 오류가 `object[]` 에 `IList<string>` 없습니다 암시적 명시적 변환이 됩니다. 캐스팅 `(IList<string>)oa1` 이후 실행 시 throw 하면 예외가 발생 합니다 `oa1` 참조는 `object[]` 아니라는 `string[]`합니다. 그러나 캐스팅 `(IList<string>)oa2` 이후 throw 예외가 발생 하지 것입니다 `oa2` 참조는 `string[]`합니다.

때마다는 암시적 또는 명시적 참조에서 변환이 `S[]` 하 `IList<T>`에서 명시적 참조 변환이 이기도 `IList<T>` 기본 인터페이스 및 `S[]` ([명시적 참조 변환](conversions.md#explicit-reference-conversions)).

때 배열 형식 `S[]` 구현 `IList<T>`에 구현된 된 인터페이스 멤버의 일부 예외를 throw 할 수 있습니다. 인터페이스의 구현 하는 정확한 동작을이 사양의 범위를 벗어납니다.

## <a name="array-creation"></a>배열 만들기

배열 인스턴스에 의해 만들어집니다 *array_creation_expression*s ([배열 만들기 식을](expressions.md#array-creation-expressions)) 또는 필드 또는 지역 변수 선언을 포함 하는 *array_initializer*([배열 이니셜라이저](arrays.md#array-initializers)).

배열 인스턴스를 만들 때 순위와 각 차원의 길이 설정 및 인스턴스 전체 수명 동안 그대로 유지 됩니다. 즉, 기존 배열 인스턴스, 차수를 변경할 수 없는 아니고 차원 크기를 조정할 수 있습니다.

배열 인스턴스는 항상 배열 형식입니다. `System.Array` 형식은 인스턴스화할 수 없는 추상 형식입니다.

만든 배열의 요소 *array_creation_expression*s 항상 기본값으로 초기화 됩니다 ([기본값](variables.md#default-values)).

## <a name="array-element-access"></a>배열 요소 액세스

배열 요소를 사용 하 여 액세스 하 *element_access* 식 ([배열 액세스](expressions.md#array-access)) 형식의 `A[I1, I2, ..., In]`여기서 `A` 배열 형식 및 각 식 `Ix` 되는 형식의 식입니다 `int`, `uint`를 `long`, `ulong`, 또는 이러한 형식 중 하나 이상에 암시적으로 변환할 수 있습니다. 배열 요소 액세스의 결과 변수, 즉 인덱스에서 선택한 배열 요소.

사용 하 여 배열의 요소를 열거할 수는 `foreach` 문 ([foreach 문을](statements.md#the-foreach-statement)).

## <a name="array-members"></a>배열 멤버

모든 배열 형식에서 선언 된 멤버를 상속 된 `System.Array` 형식입니다.

## <a name="array-covariance"></a>배열 공변성 (covariance)

두에 대 한 *reference_type*s `A` 하 고 `B`하는 경우 암시적 참조 변환, ([암시적 참조 변환](conversions.md#implicit-reference-conversions)) 나 명시적 참조 변환을 ([ 명시적 참조 변환을](conversions.md#explicit-reference-conversions))에서 존재 `A` 하 `B`, 배열 형식에서 동일한 참조 변환도 존재 합니다 `A[R]` 배열 형식으로 `B[R]`여기서 `R` 중인 지정 된 *rank_specifier* (하지만 둘 다에 대해 동일한 배열 형식). 이 관계 라고 ***배열 공변성 (covariance)*** 합니다. 배열 공변성 (covariance) 특히 의미 하는 배열 형식의 값 `A[R]` 배열 형식의 인스턴스에 대 한 참조는 실제로 있을 `B[R]`경우에서 암시적 참조 변환이 존재 `B` 하려면 `A`합니다.

배열 공 분산으로 인해 참조 형식 배열의 요소에 대 한 할당 배열 요소에 할당 되는 값이 허용 된 형식의 실제로 인지 확인 하는 런타임 검사를 포함 ([단순 할당](expressions.md#simple-assignment)). 예를 들어:
```csharp
class Test
{
    static void Fill(object[] array, int index, int count, object value) {
        for (int i = index; i < index + count; i++) array[i] = value;
    }

    static void Main() {
        string[] strings = new string[100];
        Fill(strings, 0, 100, "Undefined");
        Fill(strings, 0, 10, null);
        Fill(strings, 90, 10, 0);
    }
}
```

에 대 한 할당 `array[i]` 에 `Fill` 메서드는 암시적으로 참조 하는 개체가 되도록 하는 런타임 검사를 포함 `value` 는 `null` 의실제요소형식이호환되는인스턴스또는`array`. `Main`의 처음 두 호출 `Fill` 성공 하지만 세 번째 호출 하면을 `System.ArrayTypeMismatchException` 첫 번째 할당을 실행할 때 throw 될 `array[i]`합니다. 예외가 발생 하기 때문에 boxed `int` 에 저장할 수 없습니다는 `string` 배열입니다.

배열 공변성 (covariance) 특히 배열을로 확장 되지 않습니다 *value_type*s입니다. 예를 들어, 변환할 수 없는 해당 콘텐츠는 `int[]` 로 처리할지를 `object[]`.

## <a name="array-initializers"></a>배열 이니셜라이저

필드 선언에서 배열 이니셜라이저를 지정할 수 있습니다 ([필드](classes.md#fields)), 지역 변수 선언 ([지역 변수 선언](statements.md#local-variable-declarations)), 및 배열 만들기 식 ([배열 만들기 식](expressions.md#array-creation-expressions)):

```antlr
array_initializer
    : '{' variable_initializer_list? '}'
    | '{' variable_initializer_list ',' '}'
    ;

variable_initializer_list
    : variable_initializer (',' variable_initializer)*
    ;

variable_initializer
    : expression
    | array_initializer
    ;
```

배열 이니셜라이저를 묶어 변수 이니셜라이저의 시퀀스로 구성 됩니다. "`{`"및"`}`"토큰을 구분 하 여"`,`" 토큰입니다. 각 변수 이니셜라이저는 식 또는을 다차원 배열에 중첩 된 배열 이니셜라이저를 사용 하는 경우.

배열 이니셜라이저를 사용 하는 컨텍스트 초기화 되는 배열 형식을 결정 합니다. 배열 만들기 식을 배열 형식이 즉시, 이니셜라이저 앞 또는 배열 이니셜라이저 식에서 유추 됩니다. 필드 또는 변수 선언에서 배열 유형 선언 되는 변수 또는 필드의 형식이입니다. 배열 이니셜라이저를 사용 하면 필드 또는 변수 선언에 같은:
```csharp
int[] a = {0, 2, 4, 6, 8};
```
해당 하는 배열 생성 식에 대 한 줄인 것입니다.
```csharp
int[] a = new int[] {0, 2, 4, 6, 8};
```

1 차원 배열에 대 한 배열 이니셜라이저 할당 배열의 요소 형식이 호환 되는 식의 시퀀스가 구성 되어야 합니다. 시작 인덱스 0에 있는 요소를 사용 하 여 오름차순으로 배열 요소를 초기화 하는 식입니다. 배열 이니셜라이저 식의 수는 만들어지는 배열 인스턴스의 길이 결정 합니다. 예를 들어, 위의 배열 이니셜라이저를 만듭니다는 `int[]` 길이가 5 인의 인스턴스를 다음 값을 사용 하 여 인스턴스를 초기화 합니다.
```csharp
a[0] = 0; a[1] = 2; a[2] = 4; a[3] = 6; a[4] = 8;
```

다차원 배열의 배열 이니셜라이저에 중첩 된 배열의 차원 수 만큼 많은 수준의 있어야 합니다. 가장 왼쪽의 차원에 해당 하는 가장 바깥쪽 중첩 수준 및 오른쪽에 있는 차원에 해당 하는 가장 안쪽의 중첩 수준입니다. 배열의 각 차원 길이 배열 이니셜라이저에 해당 하는 중첩 수준에 있는 요소 수가 결정 됩니다. 각 중첩 된 배열 이니셜라이저 요소 수가 다른 배열 이니셜라이저는 같은 수준으로 동일 해야 합니다. 예제:
```csharp
int[,] b = {{0, 1}, {2, 3}, {4, 5}, {6, 7}, {8, 9}};
```
왼쪽에 있는 차원에 대 한 5이 고 길이가 오른쪽에 있는 차원에 대 한 두 개를 사용 하 여 2 차원 배열을 만듭니다.
```csharp
int[,] b = new int[5, 2];
```
및 다음 초기화 배열은 다음 값을 인스턴스:
```csharp
b[0, 0] = 0; b[0, 1] = 1;
b[1, 0] = 2; b[1, 1] = 3;
b[2, 0] = 4; b[2, 1] = 5;
b[3, 0] = 6; b[3, 1] = 7;
b[4, 0] = 8; b[4, 1] = 9;
```

맨 오른쪽 이외의 차원 길이가 0 인을 사용 하 여 주어진 경우 후속 크기 길이도 0으로 간주 됩니다. 예제:
```csharp
int[,] c = {};
```
왼쪽 및 오른쪽에 있는 차원에 대 한 0 길이의 2 차원 배열을 만듭니다.
```csharp
int[,] c = new int[0, 0];
```

배열 만들기 식을 배열 이니셜라이저 및 명시적 차원 길이 포함 하는 경우 길이 상수 식 이어야 합니다 하 고 각 중첩 수준에 있는 요소의 수에는 해당 차원 길이 일치 해야 합니다. 다음은 몇 가지 예입니다.
```csharp
int i = 3;
int[] x = new int[3] {0, 1, 2};        // OK
int[] y = new int[i] {0, 1, 2};        // Error, i not a constant
int[] z = new int[3] {0, 1, 2, 3};     // Error, length/initializer mismatch
```

여기에 대 한 이니셜라이저 `y` 차원 길이가 식이 상수 및 이니셜라이저가 없기 때문에 컴파일 타임 오류가 발생 `z` 때문에 컴파일 타임 오류가 발생 길이의 요소 수를 이니셜라이저 일치 하지 않습니다.
