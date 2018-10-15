# <a name="interfaces"></a>인터페이스

인터페이스는 계약을 정의합니다. 클래스 또는 구조체는 인터페이스를 구현 하는 계약을 따라야 합니다. 여러 기본 인터페이스에서 상속할 수 및 클래스 또는 구조체는 여러 인터페이스를 구현할 수 있습니다.

인터페이스는 메서드, 속성, 이벤트 및 인덱서를 포함할 수 있습니다. 자체 인터페이스를 정의 하는 멤버에 대 한 구현을 제공 하지 않습니다. 인터페이스는 단순히 인터페이스를 구현 하는 클래스 또는 구조체에서 제공 해야 하는 멤버를 지정 합니다.

## <a name="interface-declarations"></a>인터페이스 선언

*interface_declaration* 되는 *type_declaration* ([형식 선언을](namespaces.md#type-declarations)) 새 인터페이스 형식을 선언 하는 합니다.

```antlr
interface_declaration
    : attributes? interface_modifier* 'partial'? 'interface'
      identifier variant_type_parameter_list? interface_base?
      type_parameter_constraints_clause* interface_body ';'?
    ;
```

*interface_declaration* 선택적 집합으로 이루어져 *특성* ([특성](attributes.md))의 선택적 집합 뒤에, *interface_modifier*s ([한정자를 인터페이스](interfaces.md#interface-modifiers)), 선택적 `partial` 키워드 뒤에 한정자 `interface` 과 *식별자* 인터페이스 이름을 지정 하는 뒤에 선택적인 *variant_type_parameter_list* 사양 ([Variant 형식 매개 변수 목록](interfaces.md#variant-type-parameter-lists)), 선택적 *interface_base* 사양 ([기본 인터페이스](interfaces.md#base-interfaces)), 선택적 *type_parameter_constraints_clause*s 사양 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)) 를 뒤에 *interface_body* ([본문 인터페이스](interfaces.md#interface-body)), 세미콜론 뒤에 선택적으로 합니다.

### <a name="interface-modifiers"></a>한정자를 인터페이스

*interface_declaration* 인터페이스 한정자 시퀀스를 선택적으로 포함할 수 있습니다.

```antlr
interface_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | interface_modifier_unsafe
    ;
```

이 인터페이스 선언에 여러 번 표시 하는 동일한 한정자에 대 한 컴파일 시간 오류입니다.

`new` 한정자는 클래스 내에 정의 된 인터페이스에만 허용 됩니다. 지정 인터페이스는 동일한 이름으로 상속된 된 멤버를 숨깁니다에 설명 된 대로 [새 한정자](classes.md#the-new-modifier)합니다.

합니다 `public`, `protected`를 `internal`, 및 `private` 한정자는 인터페이스의 접근성을 제어 합니다. 인터페이스 선언 발생 하는 컨텍스트에 따라 이러한 한정자의 일부만 허용 될 수 있습니다 ([접근성을 선언](basic-concepts.md#declared-accessibility)).

### <a name="partial-modifier"></a>Partial 한정자

합니다 `partial` 한정자가 나타내는이 *interface_declaration* 부분 형식 선언입니다. 에 지정 된 규칙에 따라 바깥쪽 형식 또는 네임 스페이스 선언 내에서 동일한 이름 가진 여러 partial 인터페이스 선언을 폼 하나의 인터페이스 선언에 결합 [부분 형식](classes.md#partial-types)합니다.

### <a name="variant-type-parameter-lists"></a>Variant 형식 매개 변수 목록

Variant 형식 매개 변수 목록 인터페이스 및 대리자 형식에만 발생할 수 있습니다. 일반적인의 차이 *type_parameter_list*가 선택적 *variance_annotation* 각 형식 매개 변수입니다.

```antlr
variant_type_parameter_list
    : '<' variant_type_parameters '>'
    ;

variant_type_parameters
    : attributes? variance_annotation? type_parameter
    | variant_type_parameters ',' attributes? variance_annotation? type_parameter
    ;

variance_annotation
    : 'in'
    | 'out'
    ;
```

분산 주석이 되 면 `out`, 형식 매개 변수 라고 ***공변 (covariant)*** 합니다. 분산 주석이 되 면 `in`, 형식 매개 변수 라고 ***반공 변***합니다. 분산 주석이 없는 경우 형식 매개 변수 라고 ***고정***합니다.

예제
```csharp
interface C<out X, in Y, Z> 
{
  X M(Y y);
  Z P { get; set; }
}
```
`X` 공변 `Y` 는 반공 변 및 `Z` 변하지 않습니다.

#### <a name="variance-safety"></a>분산 보안

형식 선언에 형식 오류가 발생할 수 있는 위치를 제한 하는 형식의 형식 매개 변수 목록의 가변성 주석 발생 합니다.

형식 `T` 됩니다 ***안전 하지 않은 출력*** 다음 중 하나를 보유 하는 경우:

*  `T` 반공 변 형식 매개 변수인
*  `T` 출력 안전 하지 않은 요소 형식 가진 배열 형식인
*  `T` 인터페이스 또는 대리자 형식인 `S<A1,...,Ak>` 제네릭 형식에서 생성 `S<X1,...,Xk>` 하나 이상에 대 한 where `Ai` 다음 중 하나를 보유 합니다.
   * `Xi` 공변 (covariant) 또는 고정 및 `Ai` 안전 하지 않은 출력 됩니다.
   * `Xi` 반공 변 또는 고정 및 `Ai` 는 입력 스레드로부터 안전 합니다.
   
형식 `T` 됩니다 ***안전 하지 않은 입력*** 다음 중 하나를 보유 하는 경우:

*  `T` 공변 (covariant) 형식 매개 변수인
*  `T` 입력이 안전 하지 않은 요소 형식 가진 배열 형식인
*  `T` 인터페이스 또는 대리자 형식인 `S<A1,...,Ak>` 제네릭 형식에서 생성 `S<X1,...,Xk>` 하나 이상에 대 한 where `Ai` 다음 중 하나를 보유 합니다.
   * `Xi` 공변 (covariant) 또는 고정 및 `Ai` 안전 하지 않은 입력 됩니다.
   * `Xi` 반공 변 또는 고정 및 `Ai` 안전 하지 않은 출력 됩니다.

직관적으로 안전 하지 않은 출력 형식의 출력 위치를 서 금지 된 및 입력된 위치에는 입력이 안전 하지 않은 형식을 사용할 수 없습니다.

형식이 ***출력 스레드로부터 안전한*** 출력 unsafe 없으면 및 ***입력 스레드로부터 안전한*** 입력 안전 하지 않은 경우.

#### <a name="variance-conversion"></a>변형 변환이

가변성 주석의 목적은 (그러나 여전히 형식 안전 하 게) 더 관대 인터페이스 및 대리자 형식 변환을 제공 하는 것입니다. 이 암시적의 정의 종료 합니다 ([암시적 변환을](conversions.md#implicit-conversions)) 및 명시적 변환 ([명시적 변환](conversions.md#explicit-conversions)) 확인 변형 다음과 같이 정의 되어 있는 개념이 사용:

형식 `T<A1,...,An>` 변형 가능은 형식 `T<B1,...,Bn>` 경우 `T` variant 형식 매개 변수를 사용 하 여 인터페이스 또는 대리자 형식을 선언 `T<X1,...,Xn>`, 및 각 variant 형식 매개 변수에 대해 `Xi` 다음 중 하나 포함합니다.

*  `Xi` 공변 (covariant)에서 암시적 참조 또는 id 변환을 존재 `Ai` 를 `Bi`
*  `Xi` 반공 변 이며 암시적 참조 또는에서 identity 변환이 존재 `Bi` 를 `Ai`
*  `Xi` 고정 되어 id에서 변환이 존재 `Ai` 를 `Bi`

### <a name="base-interfaces"></a>기본 인터페이스

인터페이스 라고 하는 0 개 이상의 인터페이스 형식에서 상속할 수는 ***명시적 기본 인터페이스*** 인터페이스입니다. 인터페이스 하나 이상의 명시적 기본 인터페이스에 있는 경우 다음에서 해당 인터페이스를 선언 인터페이스 식별자 뒤에는 콜론과 쉼표로 구분 된 목록 기본 인터페이스 형식입니다.

```antlr
interface_base
    : ':' interface_type_list
    ;
```

생성 된 인터페이스 형식에 대 한 명시적 기본 인터페이스는 제네릭 형식 선언에서 명시적 기본 인터페이스 선언을 가져오고 각각에 대 한 대체으로 형성 *type_parameter* 기본 인터페이스에서 해당 선언인 *type_argument* 생성 된 형식입니다.

인터페이스의 명시적 기본 인터페이스는 적어도 인터페이스 자체 만큼 액세스 가능 해야 합니다. ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)). 컴파일 타임 오류를 지정 하는 것이 예는 `private` 또는 `internal` 인터페이스는 *interface_base* 의 `public` 인터페이스.

이 직접 또는 간접적으로 자신 으로부터 상속에 대 한 인터페이스에 대 한 컴파일 시간 오류입니다.

합니다 ***기본 인터페이스*** 명시적 기본 인터페이스 및 해당 기본 인터페이스는 인터페이스입니다. 즉, 기본 인터페이스 집합이 명시적 기본 인터페이스는, 명시적 기본 인터페이스 및 등의 전이적 closure 완료 합니다. 인터페이스의 기본 인터페이스의 모든 멤버를 상속합니다. 예제
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}

interface IListBox: IControl
{
    void SetItems(string[] items);
}

interface IComboBox: ITextBox, IListBox {}
```
기본 인터페이스 `IComboBox` 됩니다 `IControl`를 `ITextBox`, 및 `IListBox`합니다.

즉, 합니다 `IComboBox` 위의 인터페이스 멤버를 상속 `SetText` 하 고 `SetItems` 뿐만 `Paint`합니다.

모든 기본 인터페이스는 인터페이스의 출력 안전 해야 합니다. ([분산 안전성](interfaces.md#variance-safety)). 클래스 또는 구조체는 인터페이스를 암시적으로 구현 하는 모든 인터페이스의 기본 인터페이스를 구현 합니다.

### <a name="interface-body"></a>인터페이스 본문

합니다 *interface_body* 인터페이스의 인터페이스 멤버를 정의 합니다.

```antlr
interface_body
    : '{' interface_member_declaration* '}'
    ;
```

## <a name="interface-members"></a>인터페이스 멤버

인터페이스의 멤버는 기본 인터페이스에서 상속 된 멤버 및 멤버 자체 인터페이스에서 선언 합니다.

```antlr
interface_member_declaration
    : interface_method_declaration
    | interface_property_declaration
    | interface_event_declaration
    | interface_indexer_declaration
    ;
```

인터페이스 선언 0 개 이상의 멤버를 선언할 수 있습니다. 메서드, 속성, 이벤트 또는 인덱서는 인터페이스의 멤버 여야 합니다. 인터페이스는 상수, 필드, 연산자, 인스턴스 생성자, 소멸자 또는 형식을 포함할 수 없습니다 또는 인터페이스로 모든 종류의 정적 멤버를 포함할 수 있습니다.

모든 인터페이스 멤버는 암시적으로 공용 액세스를 갖습니다. 이 한정자를 포함할에 인터페이스 멤버 선언에 대 한 컴파일 시간 오류입니다. 특히 한정자를 사용 하 여 인터페이스 멤버를 선언할 수 없습니다 `abstract`, `public`, `protected`, `internal`를 `private`를 `virtual`를 `override`, 또는 `static`합니다.

이 예제에서
```csharp
public delegate void StringListEvent(IStringList sender);

public interface IStringList
{
    void Add(string s);
    int Count { get; }
    event StringListEvent Changed;
    string this[int index] { get; set; }
}
```
멤버의 가능한 종류 각각 하나씩 포함 하는 인터페이스를 선언 합니다: 메서드, 속성, 이벤트 및 인덱서 합니다.

*interface_declaration* 새 선언 공간을 만듭니다 ([선언](basic-concepts.md#declarations)), 및 *interface_member_declaration*합니다 하여포함된즉시*interface_declaration* 이 선언 공간에 새 멤버를 정의 합니다. 다음 규칙이 적용 됩니다 *interface_member_declaration*s:

*  메서드의 이름을 모든 속성과 같은 인터페이스에 선언 된 이벤트의 이름과에서 달라 야 합니다. 또한 서명 ([시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading))의 메서드는 동일한 인터페이스에 선언 된 다른 모든 메서드의 시그니처와 달라 야 하 고 같은 인터페이스에 선언 된 두 개의 메서드 서명이 있을 수 없습니다는 전적으로 달라 `ref` 고 `out`입니다.
*  속성 또는 이벤트의 이름 같은 인터페이스에 선언 된 다른 모든 멤버의 이름과에서 달라 야 합니다.
*  인덱서의 시그니처는 동일한 인터페이스에 선언된 다른 모든 인덱서의 시그니처와 달라야 합니다.

인터페이스의 상속된 된 멤버는 특히의 일부가 아닌 인터페이스의 선언 공간입니다. 따라서 인터페이스 상속된 된 멤버와 멤버 이름 또는 시그니처가 같은를 선언할 수 있습니다. 이 경우 기본 인터페이스 멤버를 숨기려면 파생된 인터페이스 멤버 라고 합니다. 상속된 된 멤버 숨기기는 오류로 간주 하지는 않지만 컴파일러 경고가 발생 하도록 합니다. 경고를 표시 하지 않으려면 파생된 인터페이스 멤버의 선언을 포함 해야 합니다는 `new` 한정자는 파생된 멤버가 기본 멤버를 숨기려면 것을 나타냅니다. 이 항목 설명에 대 한 자세한 [상속을 통해 숨기기](basic-concepts.md#hiding-through-inheritance)합니다.

경우는 `new` 한정자는 상속 된 멤버를 숨기지 않는 선언에 포함 되어, 그 결과 경고가 발생 합니다. 이 경고를 제거 하 여 표시 되지 않는지를 `new` 한정자입니다.

클래스 멤버 `object` 엄격 하 게 말하자면 모든 인터페이스의 멤버를 하지 않습니다 ([인터페이스 멤버](interfaces.md#interface-members)). 그러나 클래스 멤버 `object` 임의의 인터페이스 형식에서 멤버 조회를 통해 사용할 수 있습니다 ([멤버 조회](expressions.md#member-lookup)).

### <a name="interface-methods"></a>인터페이스 메서드

인터페이스 메서드를 사용 하 여 선언 *interface_method_declaration*s:

```antlr
interface_method_declaration
    : attributes? 'new'? return_type identifier type_parameter_list
      '(' formal_parameter_list? ')' type_parameter_constraints_clause* ';'
    ;
```

합니다 *특성*를 *return_type*를 *식별자*, 및 *formal_parameter_list* 인터페이스 메서드 선언 동일 클래스에서 메서드 선언의 것을 의미 ([메서드](classes.md#methods)). 메서드 본문을 지정 하는 인터페이스 메서드 선언 없습니다 및 선언 하므로 항상 세미콜론으로 끝납니다.

인터페이스 메서드의 각 형식 매개 변수 형식 입력 안전 해야 합니다. ([분산 안전성](interfaces.md#variance-safety))를 반환 형식 중 하나 여야 합니다 `void` 또는 출력 스레드로부터 안전 합니다. 또한 각 클래스 형식 제약 조건, 인터페이스 형식 제약 조건 및 메서드의 형식 매개 변수에서 형식 매개 변수 제약 조건을 입력 안전 해야 합니다.

이러한 규칙 확인 모든 공변 (covariant) 또는 인터페이스의 반공 변 사용량과 형식 안전 합니다. 예를 들어 개체에 적용된
```csharp
interface I<out T> { void M<U>() where U : T; }
```
유효 하지 않은 때문에 사용법 `T` 에서 형식 매개 변수 제약 조건으로 `U` 입력 안전 하지 않습니다.

이 제한은 현재 위치에 없는 것은 다음과 같이 형식 안전성을 위반할 수 있습니다:
```csharp
class B {}
class D : B{}
class E : B {}
class C : I<D> { public void M<U>() {...} }
...
I<B> b = new C();
b.M<E>();
```
이 실제로 호출 `C.M<E>`합니다. 호출 해야 하지만 해당 `E` 에서 파생 `D`이므로 형식 안전성 위반 될 여기 있습니다.

### <a name="interface-properties"></a>인터페이스 속성

사용 하 여 인터페이스 속성 선언 된 *interface_property_declaration*s:

```antlr
interface_property_declaration
    : attributes? 'new'? type identifier '{' interface_accessors '}'
    ;

interface_accessors
    : attributes? 'get' ';'
    | attributes? 'set' ';'
    | attributes? 'get' ';' attributes? 'set' ';'
    | attributes? 'set' ';' attributes? 'get' ';'
    ;
```

합니다 *특성*, *유형*, 및 *식별자* 인터페이스 속성 선언에 속성 선언의 것과 의미가 같습니다 클래스 ([ 속성](classes.md#properties)).

클래스 속성 선언의의 접근자에 해당 하는 인터페이스 속성 선언의 접근자 ([접근자](classes.md#accessors)) 한다는 점을 제외 하는 접근자 본문 세미콜론은 항상 이어야 합니다. 따라서 접근자는 단순히 속성 읽기 / 쓰기, 읽기 전용 또는 쓰기 전용 있는지 여부를 나타냅니다.

인터페이스 속성의 형식에는 출력 안전 경우 get 접근자를 사용 해야 합니다. set 접근자 있으면 입력 스레드로부터 안전 해야 합니다.

### <a name="interface-events"></a>이벤트 인터페이스

인터페이스 이벤트를 사용 하 여 선언 된 *interface_event_declaration*s:

```antlr
interface_event_declaration
    : attributes? 'new'? 'event' type identifier ';'
    ;
```

합니다 *특성*를 *유형*, 및 *식별자* 클래스에서 인터페이스 이벤트 선언 해야 이벤트 선언 것과 의미가 같습니다 ([이벤트 ](classes.md#events)).

인터페이스 이벤트의 형식은 입력 스레드로부터 안전 해야 합니다.

### <a name="interface-indexers"></a>인터페이스 인덱서

인터페이스 인덱서를 사용 하 여 선언 된 *interface_indexer_declaration*s:

```antlr
interface_indexer_declaration
    : attributes? 'new'? type 'this' '[' formal_parameter_list ']' '{' interface_accessors '}'
    ;
```

*특성*, *형식*, 및 *formal_parameter_list* 인터페이스 인덱서 선언에 indexer 선언을의 것과 의미가 같습니다 (클래스[ 인덱서](classes.md#indexers)).

클래스 인덱서 선언의 접근자에 해당 하는 선언 인터페이스 인덱서 접근자 ([인덱서](classes.md#indexers)) 한다는 점을 제외 하는 접근자 본문 세미콜론은 항상 이어야 합니다. 따라서 접근자는 단순히 인덱서가 읽기 / 쓰기, 읽기 전용 또는 쓰기 전용 있는지 여부를 나타냅니다.

모든 정식 매개 변수 유형의 인터페이스 인덱서 입력 스레드로부터 안전 해야 합니다. 또한 모든 `out` 또는 `ref` 정식 매개 변수 형식 출력 스레드로부터 안전 해야 합니다. 참고는도 `out` 매개 변수는 기본 실행 플랫폼의 제한으로 인해 입력 스레드로부터 안전 해야 합니다.

인터페이스 인덱서 유형의 출력-안전 하 게 해야 경우 get 접근자 및 set 접근자 있으면 입력 안전 해야 합니다.

### <a name="interface-member-access"></a>인터페이스 멤버 액세스

인터페이스 멤버는 멤버 액세스를 통해 액세스할 수 있습니다 ([me](expressions.md#member-access)) 및 인덱서 액세스 ([인덱서 액세스](expressions.md#indexer-access)) 형식의 식을 `I.M` 하 고 `I[A]`여기서 `I` 인터페이스 형식 이므로 `M` 메서드, 속성 또는 해당 인터페이스 형식, 이벤트 및 `A` 은 인덱서 인수 목록입니다.

엄격 하 게 된 인터페이스에 대 한 단일 상속 (상속 체인의 각 인터페이스는 직접 기본 인터페이스를 정확히 0 개 이상의 있음), 멤버 조회의 효과 ([멤버 조회](expressions.md#member-lookup)), 메서드 호출 ([ 메서드 호출](expressions.md#method-invocations)), 및 인덱서 액세스 ([인덱서 액세스](expressions.md#indexer-access)) 규칙은 정확 하 게 클래스 및 구조체의 경우와 동일: 파생된 멤버 이름 또는 시그니처가 같은 덜 더 많이 파생 된 멤버 숨기기. 그러나 다중 상속 인터페이스에 대 한 두 개의 모호성이 발생할 수 있습니다 하거나 더 관련 되지 않은 기본 인터페이스 이름 또는 시그니처가 같은 멤버를 선언 합니다. 이 섹션에서는 이러한 상황의 몇 가지 예를 보여 줍니다. 모든 경우에는 명시적 캐스팅이 모호성을 해결 하 사용할 수 있습니다.

예제
```csharp
interface IList
{
    int Count { get; set; }
}

interface ICounter
{
    void Count(int i);
}

interface IListCounter: IList, ICounter {}

class C
{
    void Test(IListCounter x) {
        x.Count(1);                  // Error
        x.Count = 1;                 // Error
        ((IList)x).Count = 1;        // Ok, invokes IList.Count.set
        ((ICounter)x).Count(1);      // Ok, invokes ICounter.Count
    }
}
```
처음 두 문은 때문에 컴파일 시간 오류가 발생할 멤버 조회 ([멤버 조회](expressions.md#member-lookup))의 `Count` 에서 `IListCounter` 모호 합니다. 캐스팅으로 모호성이 해결은 예제에서 볼 수 있듯이, `x` 적절 한 기본 인터페이스 형식입니다. 이러한 캐스트는 런타임 비용 없이-컴파일 시간에 적은 수의 파생된 형식으로 인스턴스를 표시 하는 단순히 구성 됩니다.

예제
```csharp
interface IInteger
{
    void Add(int i);
}

interface IDouble
{
    void Add(double d);
}

interface INumber: IInteger, IDouble {}

class C
{
    void Test(INumber n) {
        n.Add(1);                // Invokes IInteger.Add
        n.Add(1.0);              // Only IDouble.Add is applicable
        ((IInteger)n).Add(1);    // Only IInteger.Add is a candidate
        ((IDouble)n).Add(1);     // Only IDouble.Add is a candidate
    }
}
```
호출 `n.Add(1)` 선택 `IInteger.Add` 의 오버 로드 해결 규칙을 적용 하 여 [오버 로드 확인](expressions.md#overload-resolution)합니다. 마찬가지로 호출 `n.Add(1.0)` 선택 `IDouble.Add`합니다. 명시적 캐스트를 삽입할 때 방법이 하나만 후보 메서드와 따라서 모호성이 없습니다.

예제
```csharp
interface IBase
{
    void F(int i);
}

interface ILeft: IBase
{
    new void F(int i);
}

interface IRight: IBase
{
    void G();
}

interface IDerived: ILeft, IRight {}

class A
{
    void Test(IDerived d) {
        d.F(1);                 // Invokes ILeft.F
        ((IBase)d).F(1);        // Invokes IBase.F
        ((ILeft)d).F(1);        // Invokes ILeft.F
        ((IRight)d).F(1);       // Invokes IBase.F
    }
}
```
합니다 `IBase.F` 하 여 멤버를 숨깁니다는 `ILeft.F` 멤버입니다. 호출 `d.F(1)` 선택 하므로 `ILeft.F`경우에 `IBase.F` 안내 하는 액세스 경로에서 숨겨져 있지가 `IRight`입니다.

다중 상속 인터페이스의 숨기기에 대 한 직관적인 규칙은 단순히이: 모든 액세스 경로에서 숨겨져 멤버 액세스 경로에서 숨겨진 경우. 때문에 액세스 경로 `IDerived` 에 `ILeft` 에 `IBase` 숨깁니다 `IBase.F`, 액세스 경로에서 멤버를 숨길 수도 `IDerived` 에 `IRight` 에 `IBase`합니다.

## <a name="fully-qualified-interface-member-names"></a>정규화 된 인터페이스 멤버 이름

인터페이스 멤버는 라고도 하 여 해당 ***정규화 된 이름을***입니다. 인터페이스 멤버의 정규화 된 이름을 인터페이스는 멤버는 선언 뒤에 점, 멤버의 이름 뒤의 이름으로 구성 됩니다. 멤버가 선언 된 인터페이스를 참조 하는 멤버의 정규화 된 이름입니다. 예를 들어 선언
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}
```
정규화 된 이름을 `Paint` 은 `IControl.Paint` 이름과 정규화 `SetText` 는 `ITextBox.SetText`합니다.

위의 예제에서는 불가능를 가리키도록 `Paint` 으로 `ITextBox.Paint`입니다.

인터페이스는 네임 스페이스의 일부가 되 면 인터페이스 멤버의 정규화 된 이름을 네임 스페이스 이름이 포함 합니다. 예
```csharp
namespace System
{
    public interface ICloneable
    {
        object Clone();
    }
}
```

정규화 된 이름, 여기서는 `Clone` 메서드는 `System.ICloneable.Clone`합니다.

## <a name="interface-implementations"></a>인터페이스 구현

인터페이스는 클래스 및 구조체에서 구현 될 수 있습니다. 클래스 또는 구조체를 직접 인터페이스를 구현 함을 나타내려면 인터페이스 식별자는 클래스 또는 구조체의 기본 클래스 목록에 포함 됩니다. 예를 들어:
```csharp
interface ICloneable
{
    object Clone();
}

interface IComparable
{
    int CompareTo(object other);
}

class ListEntry: ICloneable, IComparable
{
    public object Clone() {...}
    public int CompareTo(object other) {...}
}
```

클래스 또는 구조체 직접 인터페이스를 직접 구현 하는 모든 인터페이스의 기본 인터페이스 구현 암시적으로 합니다. 클래스 또는 구조체는 기본 클래스 목록에 모든 기본 인터페이스를 나열 명시적으로 하지 않는 경우에 마찬가지입니다. 예를 들어:
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}

class TextBox: ITextBox
{
    public void Paint() {...}
    public void SetText(string text) {...}
}
```

여기서 클래스 `TextBox` 둘 다 구현 `IControl` 고 `ITextBox`입니다.

때 클래스 `C` 직접 C에서 파생 된 모든 클래스 인터페이스 구현도 인터페이스를 암시적으로 구현 합니다. 클래스 선언에 지정 된 기본 인터페이스는 생성 된 인터페이스 형식이 될 수 있습니다 ([형식 생성](types.md#constructed-types)). 기본 인터페이스를 범위에 있는 형식 매개 변수를 포함할 수 있지만 자체적으로 형식 매개 변수 수 없습니다. 다음 코드에서는 클래스를 구현 하 고 생성 된 형식을 확장 하는 방법을 보여 줍니다.
```csharp
class C<U,V> {}

interface I1<V> {}

class D: C<string,int>, I1<string> {}

class E<T>: C<int,T>, I1<T> {}
```

제네릭 클래스 선언의 기본 인터페이스에 설명 된 고유성 규칙에 맞아야 [구현 된 인터페이스의 고유성](interfaces.md#uniqueness-of-implemented-interfaces)합니다.

### <a name="explicit-interface-member-implementations"></a>명시적 인터페이스 멤버 구현

인터페이스를 구현 하는 용도로 클래스 또는 구조체를 선언할 수 있습니다 ***명시적 인터페이스 멤버 구현을***합니다. 명시적 인터페이스 멤버 구현에는 정규화 된 인터페이스 멤버 이름을 참조 하는 메서드, 속성, 이벤트 또는 인덱서 선언입니다. 예
```csharp
interface IList<T>
{
    T[] GetElements();
}

interface IDictionary<K,V>
{
    V this[K key];
    void Add(K key, V value);
}

class List<T>: IList<T>, IDictionary<int,T>
{
    T[] IList<T>.GetElements() {...}
    T IDictionary<int,T>.this[int index] {...}
    void IDictionary<int,T>.Add(int index, T value) {...}
}
```

여기 `IDictionary<int,T>.this` 고 `IDictionary<int,T>.Add` 명시적 인터페이스 멤버 구현 됩니다.

일부 경우 인터페이스 멤버의 이름을 나타나는 경우 인터페이스 멤버 구현 될 수 있습니다 명시적 인터페이스 멤버 구현을 사용 하 여 구현 클래스에 대 한 적합 하지 않을 수도 있습니다. 예를 들어 파일 추상화를 구현 하는 클래스를 구현 가능성이 `Close` 효과가 파일 리소스를 해제 하 고 구현 하는 멤버 함수는 `Dispose` 메서드는 `IDisposable` 명시적 인터페이스를 사용 하 여 인터페이스 멤버 구현:
```csharp
interface IDisposable
{
    void Dispose();
}

class MyFile: IDisposable
{
    void IDisposable.Dispose() {
        Close();
    }

    public void Close() {
        // Do what's necessary to close the file
        System.GC.SuppressFinalize(this);
    }
}
```

명시적 인터페이스 멤버 구현을 메서드 호출, 속성 액세스 또는 인덱서 액세스의 정규화 된 이름을 통해 액세스 하는 것이 불가능 합니다. 명시적 인터페이스 멤버 구현을 인터페이스 인스턴스를 통해서만 액세스할 수 있습니다 및 멤버 이름을 사용 하 여 단순히 경우 참조 합니다.

액세스 한정자를 포함 하는 명시적 인터페이스 멤버 구현에 대 한 컴파일 시간 오류 이며 한정자를 포함 하도록 컴파일 타임 오류 `abstract`, `virtual`를 `override`, 또는 `static`합니다.

명시적 인터페이스 멤버 구현에 다른 멤버 보다 다양 한 내게 필요한 옵션 특징이 있습니다. 명시적 인터페이스 멤버 구현을 메서드 호출 또는 속성 액세스에서 정규화 된 이름을 통해 액세스할 수 없습니다 이기 때문에 개인 의미 있는 합니다. 그러나 인터페이스 인스턴스를 통해 액세스할 수 있습니다, 되므로 있는 공용도 의미 합니다.

두 가지 기본 용도로 사용 하는 명시적 인터페이스 멤버 구현:

*  명시적 인터페이스 멤버 구현 클래스 또는 구조체 인스턴스를 통해 액세스할 수 없는, 때문에 인터페이스 구현 클래스 또는 구조체의 공용 인터페이스에서 제외할 수 있습니다. 클래스는 경우에 특히 유용 하거나 구조체는 해당 클래스 또는 구조체의 소비자에 게 관심 있는 내부 인터페이스를 구현 합니다.
*  명시적 인터페이스 멤버 구현을 동일한 서명 사용 하 여 인터페이스 멤버의 명확성을 허용합니다. 명시적 인터페이스 멤버 구현 하지 않고는 것이 불가능 클래스 또는 구조체에 대 한 다른 구현이 인터페이스 시그니처가 같은 멤버 및 반환 형식에는 것이 불가능 클래스 또는 구조체에 대 한 모든 구현에 있어야 합니다. 동일한 서명 사용 하 여 인터페이스 멤버의 모든 형식을 반환 하지만 다른 합니다.

유효한 것으로 명시적 인터페이스 멤버 구현에 대 한 클래스 또는 구조체 이름을 지정 해야 해당 정규화 된 이름, 형식 및 매개 변수 형식을 정확 하 게 일치 명시적 인터페이스 멤버의 멤버를 포함 하는 기본 클래스 목록에서 인터페이스 구현입니다. 다음 클래스에 따라서
```csharp
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
    int IComparable.CompareTo(object other) {...}    // invalid
}
```
선언의 `IComparable.CompareTo` 때문에 컴파일 타임 오류가 발생 `IComparable` 의 기본 클래스 목록에 나열 되지 `Shape` 의 기본 인터페이스 아니며, `ICloneable`합니다. 마찬가지로, 선언에서
```csharp
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
}

class Ellipse: Shape
{
    object ICloneable.Clone() {...}    // invalid
}
```
선언의 `ICloneable.Clone` 에 `Ellipse` 때문에 컴파일 타임 오류가 발생 `ICloneable` 의 기본 클래스 목록에 명시적으로 나열 되지 `Ellipse`합니다.

인터페이스 멤버의 정규화 된 이름에는 멤버를 선언 하는 인터페이스를 참조 해야 합니다. 선언에 따라서
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}

class TextBox: ITextBox
{
    void IControl.Paint() {...}
    void ITextBox.SetText(string text) {...}
}
```
명시적 인터페이스 멤버 구현이 `Paint` 로 써야 `IControl.Paint`합니다.

### <a name="uniqueness-of-implemented-interfaces"></a>구현 된 인터페이스의 고유성

제네릭 형식 선언에 의해 구현 된 인터페이스는 모든 가능한 생성 된 형식에 대 한 고유 유지 되어야 합니다. 이 규칙 없이 것은 불가능 생성 된 특정 형식에 대 한 호출을 올바른 방법을 결정 합니다. 예를 들어, 제네릭 클래스 선언 된을 다음과 같이 작성할 수 있습니다.
```csharp
interface I<T>
{
    void F();
}

class X<U,V>: I<U>, I<V>                    // Error: I<U> and I<V> conflict
{
    void I<U>.F() {...}
    void I<V>.F() {...}
}
```

허용이 인 수 없기 다음과 같은 경우 실행할 코드를 확인할 수 있습니다.
```csharp
I<int> x = new X<int,int>();
x.F();
```

제네릭 형식 선언의 인터페이스 목록에 올바른 인지를 확인 하려면 다음 단계를 수행 됩니다.

*  수 있도록 `L` 제네릭 클래스, 구조체 또는 인터페이스 선언에 직접 지정 된 인터페이스의 목록 `C`합니다.
*  추가할 `L` 인터페이스에 이미 인터페이스의 기본 `L`입니다.
*  모든 중복을 제거할 `L`합니다.
*  모든 가능한 생성 형식에서 생성 하는 경우 `C` 하 고 형식 인수를 대체 한 후 `L`, 두 인터페이스를 일으킬 `L` 를 동일 하 게 선언 다음 `C` 올바르지 않습니다. 제약 조건 선언에는 모든 가능한 생성 된 형식을 결정할 때 고려 되지 않습니다.

클래스 선언에서 `X` 인터페이스 목록 위의 `L` 이루어져 `I<U>` 고 `I<V>`입니다. 생성 된 모든 사용 하 여 형식 때문에 선언은 올바르지 않습니다 `U` 고 `V` 동일한 형식이 두 인터페이스로 인해 동일한 형식입니다.

통합 다른 상속 수준에서 지정 된 인터페이스에 대 한 두는 것이 가능 합니다.
```csharp
interface I<T>
{
    void F();
}

class Base<U>: I<U>
{
    void I<U>.F() {...}
}

class Derived<U,V>: Base<U>, I<V>    // Ok
{
    void I<V>.F() {...}
}
```

이 코드는 유효 하더라도 `Derived<U,V>` 둘 다 구현 `I<U>` 고 `I<V>`입니다. 코드
```csharp
I<int> x = new Derived<int,int>();
x.F();
```
메서드를 호출 `Derived`, 이후 `Derived<int,int>` 효과적으로 다시 구현 `I<int>` ([다시 구현 하는 인터페이스](interfaces.md#interface-re-implementation)).

### <a name="implementation-of-generic-methods"></a>제네릭 메서드의 구현

때 제네릭 메서드를 암시적으로 구현 인터페이스 메서드를 각 메서드 형식 매개 변수 여야 합니다 () 선언 모두에 해당 하는 임의의 인터페이스 형식 매개 변수는 적절 한 형식 인수를 사용 하 여 대체 됩니다), (후 위치를 지정 된 제약 조건 메서드 형식 매개 변수는 왼쪽에서 오른쪽으로 서 수 위치도 식별 됩니다.

그러나 제네릭 메서드는 인터페이스 메서드를 명시적으로 구현 하는 경우 제약 조건이 없는 구현 방법에 허용 됩니다. 인터페이스 메서드에서 제약 조건은 상속 대신

```csharp
interface I<A,B,C>
{
    void F<T>(T t) where T: A;
    void G<T>(T t) where T: B;
    void H<T>(T t) where T: C;
}

class C: I<object,C,string>
{
    public void F<T>(T t) {...}                    // Ok
    public void G<T>(T t) where T: C {...}         // Ok
    public void H<T>(T t) where T: string {...}    // Error
}
```

메서드 `C.F<T>` 암시적으로 구현 `I<object,C,string>.F<T>`합니다. 이 예에서 `C.F<T>` 하지 필요한 (않으며 허용) 제약 조건을 지정 `T:object` 있으므로 `object` 모든 형식 매개 변수에서 암시적 제약 조건입니다. 메서드 `C.G<T>` 암시적으로 구현 `I<object,C,string>.G<T>` 인터페이스 형식 매개 변수는 해당 형식 인수를 사용 하 여 대체 후 인터페이스에서 이러한 제약 조건을 일치 합니다. 메서드에 대 한 제약 조건을 `C.H<T>` sealed 형식의 없으므로 오류입니다 (`string` 여기서) 제약 조건으로 사용할 수 없습니다. 제약 조건을 생략 수도 오류가 암시적 인터페이스 메서드 구현 제약 조건과 일치 해야 하므로 있습니다. 암시적으로 구현할 수는 따라서 `I<object,C,string>.H<T>`합니다. 명시적 인터페이스 멤버 구현을 사용 하 여이 인터페이스 메서드를 구현만 있습니다.
```csharp
class C: I<object,C,string>
{
    ...

    public void H<U>(U u) where U: class {...}

    void I<object,C,string>.H<T>(T t) {
        string s = t;    // Ok
        H<T>(t);
    }
}
```

이 예제에서는 명시적 인터페이스 멤버 구현이 엄격 하 게 약한 제약 조건이 있는 공용 메서드를 호출 합니다. 할당 된 `t` 하 `s` 이후 유효 `T` 의 제약 조건을 상속 `T:string`이 제약 조건은 소스 코드에 표현할 수 없는 경우에 합니다.

### <a name="interface-mapping"></a>인터페이스 매핑

클래스 또는 구조체는 클래스 또는 구조체의 기본 클래스 목록에 나열 된 인터페이스의 모든 멤버의 구현을 제공 해야 합니다. 프로세스를 구현 하는 클래스 또는 구조체에서 인터페이스 멤버의 구현을 찾는 이라고 ***인터페이스 매핑을***합니다.

클래스 또는 구조체에 대 한 인터페이스 매핑을 `C` 의 기본 클래스 목록에 지정 된 각 인터페이스의 각 멤버에 대 한 구현을 찾는 `C`합니다. 특정 인터페이스 멤버의 구현을 `I.M`, 여기서 `I` 는 인터페이스 멤버 `M` 선언, 각 클래스 또는 구조체를 검사 하 여 결정 됩니다 `S`부터 시작 하 여 `C` 및 각 후속 기본 클래스에 대 한 반복 `C`일치 하는 배치 될 때까지:

*  경우 `S` 일치 하는 명시적 인터페이스 멤버 구현 선언이 `I` 및 `M`를이 멤버는 구현의 `I.M`합니다.
*  그렇지 `S` 일치 하는 static이 아니고 public 멤버의 선언이 포함 `M`를이 멤버는 구현의 `I.M`합니다. 멤버는 구현의 멤버로 일치 항목 보다 더 지정 되지 않은 경우 `I.M`합니다. 이 이런 경우에 발생 `S` 생성 된 형식인 여기서 두 멤버를 제네릭 형식에서 선언 된 다른 서명 하지만 형식 인수를 해당 서명이 동일 합니다.

컴파일 타임 오류가 발생 하는 구현을 기본 클래스 목록에 지정 된 모든 인터페이스의 모든 멤버에 대해 찾을 수 없는 경우 `C`합니다. 인터페이스의 멤버는 기본 인터페이스에서 상속 하는 멤버만 포함 하는 참고 합니다.

인터페이스 매핑, 클래스 멤버의 목적을 위해 `A` 인터페이스 멤버를 일치 `B` 때:

*  `A` 및 `B` 메서드와 이름, 형식 및 형식 매개 변수 목록이 `A` 고 `B` 동일 합니다.
*  `A` 및 `B` 속성, 이름 및 유형의 `A` 하 고 `B` 동일 하 고 `A` 으로 동일한 접근자가 `B` (`A` 명시적 인터페이스 없으면 추가 접근자를 사용할 수 멤버 구현)입니다.
*  `A` 및 `B` 는 이벤트로, 이름 및 유형의 `A` 고 `B` 동일 합니다.
*  `A` 및 `B` 인덱서, 형식 및 형식 매개 변수 목록이 `A` 및 `B` 동일 하 고 `A` 으로 동일한 접근자가 `B` (`A` 가 없는 경우 추가 접근자를 사용할 수는 명시적 인터페이스 멤버 구현)입니다.

주목할 만한 미치는 인터페이스 매핑 알고리즘은 다음과 같습니다.

*  명시적 인터페이스 멤버 구현을 인터페이스 멤버를 구현 하는 클래스 또는 구조체 멤버를 결정할 때 동일한 클래스 또는 구조체의 다른 멤버 보다 우선 합니다.
*  Public이 아닌 나 정적 멤버가 인터페이스 매핑을에 참여합니다.

예제
```csharp
interface ICloneable
{
    object Clone();
}

class C: ICloneable
{
    object ICloneable.Clone() {...}
    public object Clone() {...}
}
```
합니다 `ICloneable.Clone` 소속 `C` 구현 되 `Clone` 에서 `ICloneable` 명시적 인터페이스 멤버 구현을 다른 멤버 보다 우선 하기 때문에 합니다.

두 클래스 또는 구조체 구현 하는 경우 또는 동일한 이름, 형식 및 매개 변수 형식을 사용 하 여 멤버를 포함 하는 자세한 인터페이스, 해당 인터페이스 멤버를 단일 클래스 또는 구조체 멤버의 각 매핑할 가능성이 있습니다. 예
```csharp
interface IControl
{
    void Paint();
}

interface IForm
{
    void Paint();
}

class Page: IControl, IForm
{
    public void Paint() {...}
}
```

여기에 `Paint` 메서드가 모두 `IControl` 및 `IForm` 에 매핑되는 `Paint` 에서 메서드 `Page`합니다. 이기도 물론 두 가지 방법에 대 한 별도 명시적 인터페이스 멤버 구현을 가질 수 있습니다.

클래스 또는 구조체는 숨겨진된 멤버를 포함 하는 인터페이스를 구현 하는 경우 일부 멤버 명시적 인터페이스 멤버 구현을 통해 구현 반드시 해야 합니다. 예
```csharp
interface IBase
{
    int P { get; }
}

interface IDerived: IBase
{
    new int P();
}
```

이 인터페이스의 구현을 하나 이상의 명시적 인터페이스 멤버 구현이 필요 하 고 다음 형식 중 하나를 수행 하는
```csharp
class C: IDerived
{
    int IBase.P { get {...} }
    int IDerived.P() {...}
}

class C: IDerived
{
    public int P { get {...} }
    int IDerived.P() {...}
}

class C: IDerived
{
    int IBase.P { get {...} }
    public int P() {...}
}
```

클래스는 동일한 기본 인터페이스는 여러 인터페이스를 구현 하는 경우 기본 인터페이스의 구현이 한 개만 있을 수 있습니다. 예제
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}

interface IListBox: IControl
{
    void SetItems(string[] items);
}

class ComboBox: IControl, ITextBox, IListBox
{
    void IControl.Paint() {...}
    void ITextBox.SetText(string text) {...}
    void IListBox.SetItems(string[] items) {...}
}
```
에 대 한 별도 구현이 불가능 합니다 `IControl` 기본 클래스 목록에 명명 된를 `IControl` 에서 상속 `ITextBox`, 및 `IControl` 상속한 `IListBox`. 실제로 이러한 인터페이스에 대 한 별도 id 개념이 없으므로 있습니다. 아니라 구현 `ITextBox` 하 고 `IListBox` 의 동일한 구현을 공유 `IControl`, 및 `ComboBox` 단순히 세 가지 인터페이스를 구현할 것으로 간주 됩니다 `IControl`, `ITextBox`, 및 `IListBox`합니다.

기본 클래스의 멤버는 인터페이스 매핑을에 참여합니다. 예제
```csharp
interface Interface1
{
    void F();
}

class Class1
{
    public void F() {}
    public void G() {}
}

class Class2: Class1, Interface1
{
    new public void G() {}
}
```
메서드 `F` 에 `Class1` 에 사용 됩니다 `Class2`의 구현의 `Interface1`합니다.

### <a name="interface-implementation-inheritance"></a>인터페이스 구현 상속

클래스는 해당 기본 클래스에서 제공 하는 모든 인터페이스 구현을 상속 합니다.

하지 않고 명시적으로 ***다시 구현*** 인터페이스 파생된 클래스를 변경할 수 없습니다 어떤 방식으로 해당 기본 클래스에서 상속 하는 인터페이스 매핑을 합니다. 예를 들어 선언에서
```csharp
interface IControl
{
    void Paint();
}

class Control: IControl
{
    public void Paint() {...}
}

class TextBox: Control
{
    new public void Paint() {...}
}
```
`Paint` 에서 메서드 `TextBox` 숨깁니다를 `Paint` 에서 메서드 `Control`, 매핑의 변경 하지 않습니다 하지만 `Control.Paint` 끌어다 `IControl.Paint`, 호출 및 `Paint` 클래스를 통해 인스턴스 및 인터페이스 인스턴스를 같은 영향을 미칠
```csharp
Control c = new Control();
TextBox t = new TextBox();
IControl ic = c;
IControl it = t;
c.Paint();            // invokes Control.Paint();
t.Paint();            // invokes TextBox.Paint();
ic.Paint();           // invokes Control.Paint();
it.Paint();           // invokes Control.Paint();
```

그러나 인터페이스 메서드는 클래스의 가상 메서드를 매핑되면 있기 파생된 클래스가 가상 메서드를 재정의 하 고 인터페이스의 구현을 변경할 수 있습니다. 예를 들어, 위의 선언을 다시 작성
```csharp
interface IControl
{
    void Paint();
}

class Control: IControl
{
    public virtual void Paint() {...}
}

class TextBox: Control
{
    public override void Paint() {...}
}
```
다음과 같은 효과 관찰 이제 됩니다.
```csharp
Control c = new Control();
TextBox t = new TextBox();
IControl ic = c;
IControl it = t;
c.Paint();            // invokes Control.Paint();
t.Paint();            // invokes TextBox.Paint();
ic.Paint();           // invokes Control.Paint();
it.Paint();           // invokes TextBox.Paint();
```

명시적 인터페이스 멤버 구현을 선언할 수 없습니다. 가상, 이후 명시적 인터페이스 멤버 구현을 재정의 하는 것이 불가능 합니다. 그러나 다른 메서드를 호출 하는 명시적 인터페이스 멤버 구현에 대 한 완벽 하 게 유효 하 고 재정의 하는 클래스를 파생 하는 다른 메서드를 선언할 수 있도록 가상입니다. 예
```csharp
interface IControl
{
    void Paint();
}

class Control: IControl
{
    void IControl.Paint() { PaintControl(); }
    protected virtual void PaintControl() {...}
}

class TextBox: Control
{
    protected override void PaintControl() {...}
}
```

여기에서 파생 된 클래스 `Control` 구현의 특수화할 수 있습니다 `IControl.Paint` 재정의 하 여는 `PaintControl` 메서드.

### <a name="interface-re-implementation"></a>다시 구현 하는 인터페이스

인터페이스 구현을 상속 된 클래스 수 ***재구현*** 기본 클래스 목록에 포함 하는 인터페이스입니다.

인터페이스를 다시 구현 정확히 동일한 규칙을 따릅니다 인터페이스 매핑을 인터페이스의 초기 구현으로 합니다. 따라서 상속 된 인터페이스 매핑을 인터페이스의 다시 구현에 대 한 설정 인터페이스 매핑에 대 한 어떠한 효과가 없습니다. 예를 들어 선언에서
```csharp
interface IControl
{
    void Paint();
}

class Control: IControl
{
    void IControl.Paint() {...}
}

class MyControl: Control, IControl
{
    public void Paint() {}
}
```
팩트는 `Control` 매핑합니다 `IControl.Paint` 끌어다 `Control.IControl.Paint` 다시 구현에 영향을 주지 않습니다 `MyControl`, 매핑되는 `IControl.Paint` 에 `MyControl.Paint`입니다.

공용 멤버 선언 및 상속 된 명시적 인터페이스 멤버 선언 다시 구현 된 인터페이스에 대 한 인터페이스 매핑 프로세스에 참여를 상속 합니다. 예
```csharp
interface IMethods
{
    void F();
    void G();
    void H();
    void I();
}

class Base: IMethods
{
    void IMethods.F() {}
    void IMethods.G() {}
    public void H() {}
    public void I() {}
}

class Derived: Base, IMethods
{
    public void F() {}
    void IMethods.H() {}
}
```

여기, 구현의 `IMethods` 에 `Derived` 인터페이스 메서드를 매핑합니다 `Derived.F`, `Base.IMethods.G`에 `Derived.IMethods.H`, 및 `Base.I`합니다.

클래스 인터페이스를 구현 하는 경우이 암시적으로 모든 해당 인터페이스의 기본 인터페이스를 구현 합니다. 마찬가지로, 인터페이스를 다시 구현 이기도 암시적으로 모든 인터페이스의 기본 인터페이스를 다시 구현 합니다. 예
```csharp
interface IBase
{
    void F();
}

interface IDerived: IBase
{
    void G();
}

class C: IDerived
{
    void IBase.F() {...}
    void IDerived.G() {...}
}

class D: C, IDerived
{
    public void F() {...}
    public void G() {...}
}
```

여기에서 다시 구현의 `IDerived` 다시 구현 `IBase`매핑이 `IBase.F` 끌어다 `D.F`합니다.

### <a name="abstract-classes-and-interfaces"></a>추상 클래스 및 인터페이스

추상 클래스는 추상 클래스와 마찬가지로 클래스의 기본 클래스 목록에 나열 된 인터페이스의 모든 멤버의 구현을 제공 해야 합니다. 그러나 추상 클래스는 인터페이스 메서드를 추상 메서드에 매핑할 허용 됩니다. 예
```csharp
interface IMethods
{
    void F();
    void G();
}

abstract class C: IMethods
{
    public abstract void F();
    public abstract void G();
}
```

여기, 구현의 `IMethods` 매핑합니다 `F` 하 고 `G` 에서 파생 된 비추상 클래스에서 재정의 되어야 하는 추상 메서드에 `C`합니다.

명시적 인터페이스 멤버 구현에서는 추상 일 수는 없지만 명시적 인터페이스 멤버 구현을 물론 추상 메서드를 호출할 수는 note 합니다. 예
```csharp
interface IMethods
{
    void F();
    void G();
}

abstract class C: IMethods
{
    void IMethods.F() { FF(); }
    void IMethods.G() { GG(); }
    protected abstract void FF();
    protected abstract void GG();
}
```

여기에서 파생 된 비추상 클래스 `C` 재정의 하는 데 필요한 `FF` 하 고 `GG`의 실제 구현을 제공 `IMethods`합니다.
