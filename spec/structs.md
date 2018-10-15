# <a name="structs"></a>구조체

구조체는 데이터 멤버 및 함수 멤버를 포함할 수 있는 데이터 구조를 나타낸다는 점에서 클래스와 비슷합니다. 그러나 클래스와 달리 구조체 값 형식이 며 힙 할당이 필요 하지 않습니다. 구조체 형식의 변수는 클래스 형식의 변수 라고 개체 데이터에 대 한 참조를 포함 하는 반면 직접 구조체의 데이터를 포함 합니다.

구조체는 값 의미 체계를 갖는 작은 데이터 구조에 특히 유용합니다. 복소수, 좌표계의 점 또는 사전의 키-값 쌍이 모두 구조체의 좋은 예입니다. 이러한 데이터 구조에는 키 몇 가지 데이터 멤버의 상속 또는 참조 id를 사용 하 여 필요 하지 않습니다는 편리 하 게 구현할 수 할당에서 참조 하는 대신 값을 복사 하는 위치 값 의미 체계를 사용 하는 것입니다.

에 설명 된 대로 [단순 형식](types.md#simple-types)와 같은 C#에서 제공 하는 단순 형식을 `int`를 `double`, 및 `bool`은 실제로 모든 구조체 형식은입니다. 과 마찬가지로 이러한 미리 정의 된 형식은 구조체, 구조체 및 C# 언어에서 새 "기본" 형식을 구현 하는 오버 로드 된 연산자를 사용할 수 이기도 합니다. 이러한 형식의 두 가지 예는이 장의 끝에 제공 됩니다 ([구조체 예제](structs.md#struct-examples)).

## <a name="struct-declarations"></a>구조체 선언

A *struct_declaration* 되는 *type_declaration* ([형식 선언을](namespaces.md#type-declarations)) 새 구조체를 선언 하는:

```antlr
struct_declaration
    : attributes? struct_modifier* 'partial'? 'struct' identifier type_parameter_list?
      struct_interfaces? type_parameter_constraints_clause* struct_body ';'?
    ;
```

A *struct_declaration* 선택적 집합으로 이루어져 *특성* ([특성](attributes.md))의 선택적 집합 뒤에, *struct_modifier*s ([구조체 한정자](structs.md#struct-modifiers)), 선택적 `partial` 키워드 뒤에 한정자 `struct` 및 *식별자* 구조체 뒤에 이름을 지정 하는 선택적 *type_parameter_list* 사양 ([형식 매개 변수](classes.md#type-parameters)), 선택적 *struct_interfaces* 사양 ([Partial 한정자](structs.md#partial-modifier))), 선택적 *type_parameter_constraints_clause*s 사양 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)) 고 뒤에 *struct_body* ([구조체 본문](structs.md#struct-body)), 세미콜론 뒤에 선택적으로 합니다.

### <a name="struct-modifiers"></a>구조체 한정자

A *struct_declaration* 구조체 한정자 시퀀스를 선택적으로 포함할 수 있습니다.

```antlr
struct_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | struct_modifier_unsafe
    ;
```

이 구조체 선언에 여러 번 표시 하는 동일한 한정자에 대 한 컴파일 시간 오류입니다.

구조체 선언 한정자 클래스 선언의 동일한 의미를 가집니다 ([클래스 선언을](classes.md#class-declarations)).

### <a name="partial-modifier"></a>Partial 한정자

합니다 `partial` 한정자가 나타내는이 *struct_declaration* 부분 형식 선언입니다. 에 지정 된 규칙에 따라 구조체 선언 하나를 바깥쪽 네임 스페이스 또는 형식을 선언 내에서 동일한 이름 가진 여러 partial 구조체 선언 결합 [부분 형식](classes.md#partial-types)합니다.

### <a name="struct-interfaces"></a>구조체 인터페이스

구조체 선언 포함 될 수 있습니다는 *struct_interfaces* 사양에 지정된 된 인터페이스 형식을 직접 구현할 경우 구조체 라고 합니다.

```antlr
struct_interfaces
    : ':' interface_type_list
    ;
```

인터페이스 구현을 설명에 대 한 자세한 [인터페이스 구현을](interfaces.md#interface-implementations)합니다.

### <a name="struct-body"></a>구조체 본문

합니다 *struct_body* 구조체의 구조체의 멤버를 정의 합니다.

```antlr
struct_body
    : '{' struct_member_declaration* '}'
    ;
```

## <a name="struct-members"></a>구조체 멤버

구조체의 멤버 구성에서 도입 된 멤버의 해당 *struct_member_declaration*형식에서 상속 된 멤버 및 `System.ValueType`합니다.

```antlr
struct_member_declaration
    : constant_declaration
    | field_declaration
    | method_declaration
    | property_declaration
    | event_declaration
    | indexer_declaration
    | operator_declaration
    | constructor_declaration
    | static_constructor_declaration
    | type_declaration
    | struct_member_declaration_unsafe
    ;
```

에 명시 된 차이점을 제외 하면 [클래스 및 구조체 차이점](structs.md#class-and-struct-differences)에 대 한 설명은에서 제공 하는 클래스 멤버 [클래스 멤버](classes.md#class-members) 를 통해 [반복기](classes.md#iterators) 구조체에 적용 멤버에도 해당 합니다.

## <a name="class-and-struct-differences"></a>클래스 및 구조체 차이점

구조체는 몇 가지 주요 방식에서 클래스와 다릅니다.

*  구조체는 값 형식 ([의미 체계를 값](structs.md#value-semantics)).
*  클래스에서 암시적으로 상속 된 모든 구조체 형식은 `System.ValueType` ([상속](structs.md#inheritance)).
*  구조체 형식의 변수에 할당 되 고 할당 된 값의 복사본을 만듭니다 ([할당](structs.md#assignment)).
*  구조체의 기본 값 형식 필드를 기본값으로 및 모든 참조를 모든 값 형식 필드를 설정 하 여 생성 된 값인 `null` ([기본값](structs.md#default-values)).
*  Boxing 및 unboxing 연산을 구조체 형식 간의 변환에 사용 되 고 `object` ([Boxing 및 unboxing](structs.md#boxing-and-unboxing)).
*  의미 `this` 구조체에 대 한 다른 ([이 액세스](expressions.md#this-access)).
*  구조체에 대 한 인스턴스 필드 선언을 변수 이니셜라이저를 포함할 수 없습니다 ([이니셜라이저 필드](structs.md#field-initializers)).
*  구조체에는 매개 변수가 없는 인스턴스 생성자를 선언할 수 없습니다 ([생성자](structs.md#constructors)).
*  구조체에는 소멸자를 선언할 수 없습니다 ([소멸자](structs.md#destructors)).

### <a name="value-semantics"></a>값 의미 체계

구조체는 값 형식 ([값 형식](types.md#value-types)) 값 의미를 갖는 된다고 합니다. 클래스, 다른 한편으로 참조 형식 ([형식을 참조](types.md#reference-types)) 참조 의미 체계가 된다고 합니다.

구조체 형식의 변수는 클래스 형식의 변수 라고 개체 데이터에 대 한 참조를 포함 하는 반면 직접 구조체의 데이터를 포함 합니다. 경우 구조체 `B` 형식의 인스턴스 필드를 포함 `A` 및 `A` 구조체 형식에 대 한 컴파일 시간 오류가 발생 `A` 에 따라 달라 지도록 `B` 에서 생성 된 형식 또는 `B`합니다. 구조체 `X` ***에 직접 종속*** 구조체 `Y` 하는 경우 `X` 형식의 인스턴스 필드를 포함 `Y`합니다. 이 정의 지정 된 구조체 종속 된 구조체의 전체 집합은의 전이적 closure를 ***에 직접 종속*** 관계입니다.  예
```csharp
struct Node
{
    int data;
    Node next; // error, Node directly depends on itself
}
```
때문에 오류가 발생 하는 `Node` 자체 형식의 인스턴스 필드를 포함 합니다.  또 다른 예
```csharp
struct A { B b; }

struct B { C c; }

struct C { A a; }
```
때문에 오류가 발생 하는 각 유형의 `A`, `B`, 및 `C` 서로에 의존 합니다.

클래스를 사용 하 여 이며 두 가지 변수가 같은 개체를 참조할 수 있으므로 작업이 다른 변수에서 참조 하는 개체에 적용할 한 변수에 대 한 합니다. 각 변수 구조체를 사용 하 여 데이터의 자체 복사본을가지고 (의 경우를 제외 하 고 `ref` 및 `out` 매개 변수), 이므로 작업에 다른 영향을 미칠 수 있습니다. 또한 구조체는 참조 형식 때문에 불가능 되도록 구조체 형식의 값에 대 한 `null`합니다.

선언 된 경우
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
코드 조각
```csharp
Point a = new Point(10, 10);
Point b = a;
a.x = 100;
System.Console.WriteLine(b.x);
```
값을 출력 합니다 `10`합니다. 할당 `a` 하 `b` 값의 복사본을 만듭니다 및 `b` 따라서 할당 하는 영향을 받지 않습니다 `a.x`합니다. 했습니다 `Point` 대신 된 클래스로 선언 출력 됩니다. `100` 있으므로 `a` 및 `b` 동일한 개체를 참조 하 게 됩니다.

### <a name="inheritance"></a>상속

클래스에서 암시적으로 상속 된 모든 구조체 형식은 `System.ValueType`는 클래스에서 상속 `object`합니다. 구조체 선언에는 구현 된 인터페이스의 목록을 지정할 수 있습니다 하지만 기본 클래스를 지정 하는 구조체 선언에 대 한 불가능 합니다.

구조체 형식은 추상 되지 며 항상 암시적으로 봉인 됩니다. 합니다 `abstract` 고 `sealed` 한정자는 따라서 구조체 선언에서 허용 되지 않습니다.

구조체 멤버의 선언 된 접근성이 될 수 없습니다 구조체에 대 한 지원 되지 않습니다 상속 되므로 `protected` 또는 `protected internal`합니다.

구조체의 멤버 함수 일 수 없습니다 `abstract` 나 `virtual`, 및 `override` 에서 상속 된 메서드를 재정의할 경우에 한정자를 사용할 수 `System.ValueType`입니다.

### <a name="assignment"></a>할당

구조체 형식의 변수에 할당 되 고 할당 된 값의 복사본을 만듭니다. 이 참조 하지만 참조에 의해 식별 된 개체를 복사 하는 클래스 형식의 변수에 할당에서 서로 다릅니다.

할당에서 구조체를 값 매개 변수로 전달 하거나 함수 멤버의 결과로 반환 하는 경우와 마찬가지로 구조체의 복사본이 생성 됩니다. 구조체를 사용 하 여 함수 멤버에는 참조로 전달 될 수는 `ref` 또는 `out` 매개 변수입니다.

구조체의 인덱서 나 속성에는 할당 대상일 때 속성 또는 인덱서 액세스와 관련 된 인스턴스 식이 변수로 분류 되어야 합니다. 인스턴스 식은 값으로 분류 됩니다, 컴파일 시간 오류가 발생 합니다. 이에서 더 자세히 설명 [단순 할당](expressions.md#simple-assignment)합니다.

### <a name="default-values"></a>기본값

에 설명 된 대로 [기본값](variables.md#default-values), 일부의 변수 생성 될 때 자동으로 기본값으로 초기화 됩니다. 클래스 형식 및 다른 참조 형식 변수의 기본값은 `null`합니다. 그러나 구조체는 사용할 수 없는 값 형식 이므로 `null`, 구조체의 기본 값 형식 필드를 기본값으로 및 모든 참조를 모든 값 형식 필드를 설정 하 여 생성 한 값은 `null`합니다.

참조 하는 `Point` 위의 예제에서는 구조체 선언
```csharp
Point[] a = new Point[100];
```
각 초기화 `Point` 설정 하 여 생성 한 값으로 배열에는 `x` 및 `y` 필드를 0으로 합니다.

구조체의 기본 생성자에서 반환 된 값에 해당 하는 구조체의 기본값 ([기본 생성자](types.md#default-constructors)). 클래스와 달리 구조체는 매개 변수가 없는 인스턴스 생성자를 선언 허용 되지 않습니다. 모든 구조체가 항상 형식 필드를 기본값으로 및 모든 참조를 모든 값 형식 필드를 설정 하는 결과로 생성 되는 값을 반환 하는 매개 변수가 없는 인스턴스 생성자를 암시적으로 포함 하는 대신 `null`합니다.

구조체는 유효한 상태 기본 초기화 상태를 고려해 야 할 설계 되어야 합니다. 예제
```csharp
using System;

struct KeyValuePair
{
    string key;
    string value;

    public KeyValuePair(string key, string value) {
        if (key == null || value == null) throw new ArgumentException();
        this.key = key;
        this.value = value;
    }
}
```
사용자 정의 인스턴스 생성자만 호출 된 위치 명시적으로 null 값을 보호 합니다. 경우에서 위치는 `KeyValuePair` 변수가 기본 값을 초기화 될 수 있습니다 합니다 `key` 및 `value` 필드는 null이 됩니다 및 구조체는이 상태를 처리할 준비가 되어 있어야 합니다.

### <a name="boxing-and-unboxing"></a>boxing 및 unboxing

클래스 형식의 값을 형식으로 변환할 수 `object` 또는 컴파일 시간에 다른 형식으로 참조를 처리 하 여 클래스에 의해 구현 되는 인터페이스 형식입니다. 형식의 값 마찬가지로 `object` 또는 참조를 변경 하지 않고 클래스 형식으로 다시 변환할 수 인터페이스 형식의 값 (하지만 물론 런타임 형식 검사를 반드시이 경우).

구조체는 참조 형식 이므로 이러한 작업은 구조체 형식에 대해 다르게 구현 됩니다. 구조체 형식의 값 형식으로 변환 되 면 `object` 또는 구조체에서 구현 되는 인터페이스 형식으로 boxing 연산을 수행 합니다. 마찬가지로, 값 형식의 `object` 또는 인터페이스 형식의 값은 구조체 형식으로 다시 변환, unboxing 작업으로 이루어집니다. 클래스 형식에서 동일한 작업에서 주요한 차이점은 boxing 및 unboxing 복사 하는지 구조체 값을 내부 / 외부로 boxed 인스턴스 즉, boxing 또는 unboxing 작업을 다음 변경 unboxed 구조체가 boxed 구조체에 반영 되지 않습니다.

구조체 형식에서 상속 된 가상 메서드를 재정의 하는 경우 `System.Object` (같은 `Equals`를 `GetHashCode`, 또는 `ToString`), 구조체 형식의 인스턴스를 통해 가상 메서드를 호출할 되려면 boxing 발생 하지 않습니다. 구조체 형식 매개 변수로 사용 되 고 형식 매개 변수 형식의 인스턴스를 통해 호출이 발생 하는 경우에 마찬가지입니다. 예를 들어:
```csharp
using System;

struct Counter
{
    int value;

    public override string ToString() {
        value++;
        return value.ToString();
    }
}

class Program
{
    static void Test<T>() where T: new() {
        T x = new T();
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
    }

    static void Main() {
        Test<Counter>();
    }
}
```

프로그램의 출력이 됩니다.
```
1
2
3
```

잘못 된 스타일을 이지만 `ToString` 부작용을 보여 줍니다의 세 가지 호출에 대 한 boxing이 발생 했음을 `x.ToString()`합니다.

제한 된 형식 매개 변수의 멤버에 액세스할 때 마찬가지로, 발생 하지 않습니다 암시적으로 boxing 합니다. 예를 들어 인터페이스로 `ICounter` 메서드를 포함 `Increment` 값을 수정에 사용할 수 있는 합니다. 경우 `ICounter` 구현의 제약 조건으로 사용 되는 `Increment` 메서드는 변수에 대 한 참조를 사용 하 여는 `Increment` boxed 사본이 없습니다에서 호출 되었습니다.

```csharp
using System;

interface ICounter
{
    void Increment();
}

struct Counter: ICounter
{
    int value;

    public override string ToString() {
        return value.ToString();
    }

    void ICounter.Increment() {
        value++;
    }
}

class Program
{
    static void Test<T>() where T: ICounter, new() {
        T x = new T();
        Console.WriteLine(x);
        x.Increment();                    // Modify x
        Console.WriteLine(x);
        ((ICounter)x).Increment();        // Modify boxed copy of x
        Console.WriteLine(x);
    }

    static void Main() {
        Test<Counter>();
    }
}
```

첫 번째 호출은 `Increment` 변수의 값을 수정 `x`합니다. 두 번째 호출은 동일 하지 않습니다 `Increment`의 boxed 사본이의 값을 수정 하는 `x`합니다. 따라서 프로그램의 출력이 됩니다.
```
0
1
1
```

Boxing 및 unboxing 대 한 자세한 내용은 참조 하세요 [Boxing 및 unboxing](types.md#boxing-and-unboxing)합니다.

### <a name="meaning-of-this"></a>이의 의미

인스턴스 생성자 또는 클래스의 인스턴스 함수 멤버 내에서 `this` 값으로 분류 됩니다. 따라서 하는 동안 `this` 인스턴스를 참조할 수는 함수 멤버를 호출 하는 것에 대 한 불가능에 할당할 `this` 클래스의 함수 멤버에서입니다.

구조체의 인스턴스 생성자 내에서 `this` 에 해당 하는 `out` 매개 변수는 구조체 형식의 및 구조체의 인스턴스 함수 멤버 내 `this` 에 해당 하는 `ref` 구조체 형식의 매개 변수입니다. 두 경우 모두 `this` 변수에로 분류 됩니다을 할당 하 여 호출 된 함수 멤버는 전체 구조체를 수정 하는 것이 가능 하 고 `this` 으로 전달 하 여를 `ref` 또는 `out` 매개 변수입니다.

### <a name="field-initializers"></a>필드 이니셜라이저

에 설명 된 대로 [기본값](structs.md#default-values), 구조체의 기본 값 형식 필드를 기본값으로 및 모든 참조를 모든 값 형식 필드를 설정 하는 결과로 생성 되는 값의 구성 `null`합니다. 이러한 이유로 구조체 변수 이니셜라이저를 포함 하도록 인스턴스 필드 선언을 허용 하지 않습니다. 이 제한은 인스턴스 필드에만 적용 됩니다. 구조체의 정적 필드는 변수 이니셜라이저를 사용할 수 있습니다.

이 예제에서
```csharp
struct Point
{
    public int x = 1;  // Error, initializer not permitted
    public int y = 1;  // Error, initializer not permitted
}
```
인스턴스 필드 선언과 변수 이니셜라이저를 포함 하기 때문에 오류입니다.

### <a name="constructors"></a>생성자

클래스와 달리 구조체는 매개 변수가 없는 인스턴스 생성자를 선언 허용 되지 않습니다. 모든 구조체가 항상 모든 값 형식 필드 기본값 및 모든 참조 형식 필드를 null로 설정 하는 결과로 생성 되는 값을 반환 하는 매개 변수가 없는 인스턴스 생성자를 암시적으로 포함 하는 대신 ([기본 생성자](types.md#default-constructors)). 구조체는 매개 변수가 있는 인스턴스 생성자를 선언할 수 있습니다. 예
```csharp
struct Point
{
    int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

위의 선언, 명령문
```csharp
Point p1 = new Point();
Point p2 = new Point(0, 0);
```
둘 다 만듭니다는 `Point` 사용 하 여 `x` 및 `y` 0으로 초기화 합니다.

구조체 인스턴스 생성자가 폼의 생성자 이니셜라이저 수 없는 `base(...)`합니다.

구조체 인스턴스 생성자는 생성자 이니셜라이저를 지정 하지 않으면 합니다 `this` 에 해당 하는 변수를 `out` 유사 하 고는 구조체 형식의 매개 변수는 `out` 매개 변수를 `this` 할당 되어야 합니다 ( [한정 된 할당](variables.md#definite-assignment)) 생성자에서 반환 되는 모든 위치에 있습니다. 구조체 인스턴스 생성자를 사용 하는 생성자 이니셜라이저를 지정 하는 경우는 `this` 에 해당 하는 변수를 `ref` 유사 하 고는 구조체 형식의 매개 변수를 `ref` 매개 변수를 `this` 에 정적으로 할당 된 것으로 간주 됩니다 생성자 본문에 대 한 항목입니다. 인스턴스 생성자 구현 아래 고려 합니다.
```csharp
struct Point
{
    int x, y;

    public int X {
        set { x = value; }
    }

    public int Y {
        set { y = value; }
    }

    public Point(int x, int y) {
        X = x;        // error, this is not yet definitely assigned
        Y = y;        // error, this is not yet definitely assigned
    }
}
```

없는 인스턴스 멤버 함수 (속성에 대 한 set 접근자를 포함 하 여 `X` 고 `Y`) 생성 되 고 있는 구조체의 모든 필드가 확실 하 게 할당 될 때까지 호출할 수 있습니다. 유일한 예외는 자동으로 구현 된 속성 ([자동으로 구현 된 속성](classes.md#automatically-implemented-properties)). 한정 된 할당 규칙 ([단순 할당 식](variables.md#simple-assignment-expressions)) 특히 해당 구조체 형식의 인스턴스 생성자 내에서 구조체 형식의 auto 속성에 할당을 제외 합니다: 이러한 할당을 한정 된 것으로 간주 됩니다 auto 속성의 숨겨진된 지원 필드의 할당 합니다. 따라서 다음은 허용 합니다.

```csharp
struct Point
{
    public int X { get; set; }
    public int Y { get; set; }

    public Point(int x, int y) {
        X = x;      // allowed, definitely assigns backing field
        Y = y;      // allowed, definitely assigns backing field
    }
```

### <a name="destructors"></a>소멸자

구조체는 소멸자를 선언 하는 허용 되지 않습니다.

### <a name="static-constructors"></a>정적 생성자

구조체에 대 한 정적 생성자에는 대부분의 클래스와 동일한 규칙을 따릅니다. 구조체 형식에 대 한 정적 생성자의 실행은 다음 이벤트 중 첫 번째 응용 프로그램 도메인 내에서 발생 하 여 트리거됩니다.

*  구조체 형식의 정적 멤버로 참조 됩니다.
*  구조체 형식의 명시적으로 선언 된 생성자가 호출 됩니다.

기본값 만들기 ([기본값](structs.md#default-values)) 구조체의 형식을 정적 생성자를 트리거하지 않습니다. (이 예로 배열에 있는 요소의 초기 값입니다.)

## <a name="struct-examples"></a>구조체 예제

다음은 사용 하는 두 가지 중요 한 예가 `struct` 유사 하지만 수정 된 의미 체계 언어의 미리 정의 된 형식에 사용할 수 있는 형식을 만드는 형식입니다.

### <a name="database-integer-type"></a>데이터베이스 정수 형식

합니다 `DBInt` 구조체의 값의 전체 집합을 나타낼 수 있는 정수 형식 구현를 `int` 형식과 알 수 없는 값을 나타내는 추가 상태입니다. 이러한 특성을 사용 하 여 형식은 데이터베이스에서 일반적으로 사용 됩니다.

```csharp
using System;

public struct DBInt
{
    // The Null member represents an unknown DBInt value.

    public static readonly DBInt Null = new DBInt();

    // When the defined field is true, this DBInt represents a known value
    // which is stored in the value field. When the defined field is false,
    // this DBInt represents an unknown value, and the value field is 0.

    int value;
    bool defined;

    // Private instance constructor. Creates a DBInt with a known value.

    DBInt(int value) {
        this.value = value;
        this.defined = true;
    }

    // The IsNull property is true if this DBInt represents an unknown value.

    public bool IsNull { get { return !defined; } }

    // The Value property is the known value of this DBInt, or 0 if this
    // DBInt represents an unknown value.

    public int Value { get { return value; } }

    // Implicit conversion from int to DBInt.

    public static implicit operator DBInt(int x) {
        return new DBInt(x);
    }

    // Explicit conversion from DBInt to int. Throws an exception if the
    // given DBInt represents an unknown value.

    public static explicit operator int(DBInt x) {
        if (!x.defined) throw new InvalidOperationException();
        return x.value;
    }

    public static DBInt operator +(DBInt x) {
        return x;
    }

    public static DBInt operator -(DBInt x) {
        return x.defined ? -x.value : Null;
    }

    public static DBInt operator +(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value + y.value: Null;
    }

    public static DBInt operator -(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value - y.value: Null;
    }

    public static DBInt operator *(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value * y.value: Null;
    }

    public static DBInt operator /(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value / y.value: Null;
    }

    public static DBInt operator %(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value % y.value: Null;
    }

    public static DBBool operator ==(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value == y.value: DBBool.Null;
    }

    public static DBBool operator !=(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value != y.value: DBBool.Null;
    }

    public static DBBool operator >(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value > y.value: DBBool.Null;
    }

    public static DBBool operator <(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value < y.value: DBBool.Null;
    }

    public static DBBool operator >=(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value >= y.value: DBBool.Null;
    }

    public static DBBool operator <=(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value <= y.value: DBBool.Null;
    }

    public override bool Equals(object obj) {
        if (!(obj is DBInt)) return false;
        DBInt x = (DBInt)obj;
        return value == x.value && defined == x.defined;
    }

    public override int GetHashCode() {
        return value;
    }

    public override string ToString() {
        return defined? value.ToString(): "DBInt.Null";
    }
}
```

### <a name="database-boolean-type"></a>데이터베이스 부울 유형

`DBBool` 구조체 3 중 값 논리 형식을 구현 합니다. 이러한 종류의 가능한 값은 `DBBool.True`, `DBBool.False`, 및 `DBBool.Null`여기서는 `Null` 멤버 알 수 없는 값을 나타냅니다. 이러한 세 개의 값 논리 형식은 데이터베이스에서 자주 사용 됩니다.

```csharp
using System;

public struct DBBool
{
    // The three possible DBBool values.

    public static readonly DBBool Null = new DBBool(0);
    public static readonly DBBool False = new DBBool(-1);
    public static readonly DBBool True = new DBBool(1);

    // Private field that stores -1, 0, 1 for False, Null, True.

    sbyte value;

    // Private instance constructor. The value parameter must be -1, 0, or 1.

    DBBool(int value) {
        this.value = (sbyte)value;
    }

    // Properties to examine the value of a DBBool. Return true if this
    // DBBool has the given value, false otherwise.

    public bool IsNull { get { return value == 0; } }

    public bool IsFalse { get { return value < 0; } }

    public bool IsTrue { get { return value > 0; } }

    // Implicit conversion from bool to DBBool. Maps true to DBBool.True and
    // false to DBBool.False.

    public static implicit operator DBBool(bool x) {
        return x? True: False;
    }

    // Explicit conversion from DBBool to bool. Throws an exception if the
    // given DBBool is Null, otherwise returns true or false.

    public static explicit operator bool(DBBool x) {
        if (x.value == 0) throw new InvalidOperationException();
        return x.value > 0;
    }

    // Equality operator. Returns Null if either operand is Null, otherwise
    // returns True or False.

    public static DBBool operator ==(DBBool x, DBBool y) {
        if (x.value == 0 || y.value == 0) return Null;
        return x.value == y.value? True: False;
    }

    // Inequality operator. Returns Null if either operand is Null, otherwise
    // returns True or False.

    public static DBBool operator !=(DBBool x, DBBool y) {
        if (x.value == 0 || y.value == 0) return Null;
        return x.value != y.value? True: False;
    }

    // Logical negation operator. Returns True if the operand is False, Null
    // if the operand is Null, or False if the operand is True.

    public static DBBool operator !(DBBool x) {
        return new DBBool(-x.value);
    }

    // Logical AND operator. Returns False if either operand is False,
    // otherwise Null if either operand is Null, otherwise True.

    public static DBBool operator &(DBBool x, DBBool y) {
        return new DBBool(x.value < y.value? x.value: y.value);
    }

    // Logical OR operator. Returns True if either operand is True, otherwise
    // Null if either operand is Null, otherwise False.

    public static DBBool operator |(DBBool x, DBBool y) {
        return new DBBool(x.value > y.value? x.value: y.value);
    }

    // Definitely true operator. Returns true if the operand is True, false
    // otherwise.

    public static bool operator true(DBBool x) {
        return x.value > 0;
    }

    // Definitely false operator. Returns true if the operand is False, false
    // otherwise.

    public static bool operator false(DBBool x) {
        return x.value < 0;
    }

    public override bool Equals(object obj) {
        if (!(obj is DBBool)) return false;
        return value == ((DBBool)obj).value;
    }

    public override int GetHashCode() {
        return value;
    }

    public override string ToString() {
        if (value > 0) return "DBBool.True";
        if (value < 0) return "DBBool.False";
        return "DBBool.Null";
    }
}
```
