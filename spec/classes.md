# <a name="classes"></a>클래스

클래스에는 데이터 멤버 (상수 및 필드) 함수 멤버 (메서드, 속성, 이벤트, 인덱서, 연산자, 인스턴스 생성자, 소멸자 및 정적 생성자) 및 중첩 된 형식을 포함할 수 있는 데이터 구조입니다. 클래스 형식은 상속을 파생된 클래스를 확장 하 고 기본 클래스를 특수화할 수 가능해 집니다 메커니즘을 지원 합니다.

## <a name="class-declarations"></a>클래스 선언

A *class_declaration* 되는 *type_declaration* ([형식 선언을](namespaces.md#type-declarations)) 새 클래스를 선언 하는 합니다.

```antlr
class_declaration
    : attributes? class_modifier* 'partial'? 'class' identifier type_parameter_list?
      class_base? type_parameter_constraints_clause* class_body ';'?
    ;
```

A *class_declaration* 선택적 집합으로 이루어져 *특성* ([특성](attributes.md))의 선택적 집합 뒤에, *class_modifier*s ([한정자 클래스](classes.md#class-modifiers)), 선택적 `partial` 키워드 뒤에 한정자 `class` 와 *식별자* 뒤에 클래스 이름을 지정 하는 선택적 *type_parameter_list* ([형식 매개 변수](classes.md#type-parameters)), 선택적 *class_base* 사양 ([클래스 기본 사양](classes.md#class-base-specification))의 선택적 집합 뒤 *type_parameter_constraints_clause*s ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)), 뒤에 *class_body*  ([본문 클래스](classes.md#class-body)), 세미콜론 뒤에 선택적으로 합니다.

클래스 선언에서 제공할 수 없습니다 *type_parameter_constraints_clause*s도 제공 하지 않는 경우를 *type_parameter_list*합니다.

제공 하는 클래스 선언을 *type_parameter_list* 되는 ***제네릭 클래스 선언의***. 또한 제네릭 클래스 선언 또는 일반 구조체 선언 내에 중첩 된 모든 클래스 이므로 자체 제네릭 클래스 선언 만들려면 생성된 된 형식을 포함 하는 형식에 대 한 형식 매개 변수를 제공 해야 합니다입니다.

### <a name="class-modifiers"></a>클래스 한정자

A *class_declaration* 클래스 한정자의 시퀀스를 선택적으로 포함할 수 있습니다.

```antlr
class_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'abstract'
    | 'sealed'
    | 'static'
    | class_modifier_unsafe
    ;
```

이 같은 한정자를 클래스 선언에 여러 번 표시에 대 한 컴파일 시간 오류입니다.

`new` 중첩된 클래스 한정자가 허용 합니다. 지정 된 클래스는 동일한 이름으로 상속된 된 멤버를 숨깁니다에 설명 된 대로 [새 한정자](classes.md#the-new-modifier)합니다. 에 대 한 컴파일 시간 오류는 `new` 한정자를 중첩된 클래스 선언 되지 않은 클래스 선언에 표시 합니다.

합니다 `public`, `protected`를 `internal`, 및 `private` 한정자 클래스의 접근성을 제어 합니다. 클래스 선언 발생 하는 컨텍스트에 따라 이러한 한정자의 일부 없습니다 허용할 수도 있습니다 ([접근성을 선언](basic-concepts.md#declared-accessibility)).

합니다 `abstract`, `sealed` 및 `static` 한정자는 다음 섹션에서 설명 합니다.

#### <a name="abstract-classes"></a>추상 클래스

`abstract` 한정자는 클래스는 불완전 한 기본 클래스로 사용할 것을 나타내는 데 사용 됩니다. 추상 클래스는 다음과 같은 방법으로에서 추상이 아닌 클래스와 다릅니다.

*  추상 클래스를 직접 인스턴스화할 수 없습니다 및 컴파일 시간 오류를 사용 하는 것은 `new` 추상 클래스에서 연산자입니다. 변수 및 컴파일 시간 형식이 추상이 값을 가질 수 있지만, 이러한 변수 및 값은 반드시 일 `null` 추상 형식에서 파생 된 비추상 클래스의 인스턴스에 대 한 참조를 포함 합니다.
*  추상 클래스는 허용 (하지만 필요 하지 않습니다) 추상 멤버를 포함 합니다.
*  추상 클래스는 sealed 일 수 없습니다.

비추상 클래스는 추상 클래스에서 파생 됩니다 비추상 클래스의 모든 상속 된 추상 멤버를 해당 추상 멤버를 재정의 하므로 실제 구현이 포함 되어야 합니다. 예제
```csharp
abstract class A
{
    public abstract void F();
}

abstract class B: A
{
    public void G() {}
}

class C: B
{
    public override void F() {
        // actual implementation of F
    }
}
```
추상 클래스 `A` 추상 메서드를 소개 `F`합니다. 클래스 `B` 에서 추가 메서드 `G`, 되지만의 구현을 제공 하지 않기 때문에 `F`, `B` 추상 선언도 해야 합니다. 클래스 `C` 재정의 `F` 실제 구현을 제공 합니다. 때문에 추상 멤버가 없거나 `C`, `C` 허용 (있지만 필요 하지 않습니다) 비추상 되도록 합니다.

#### <a name="sealed-classes"></a>봉인된 클래스

`sealed` 클래스에서 파생을 방지 하려면 한정자를 사용 합니다. 봉인 된 클래스는 다른 클래스의 기본 클래스로 지정 된 컴파일 타임 오류가 발생 합니다.

봉인 된 클래스는 추상 클래스 수도 없습니다.

`sealed` 한정자 의도 하지 않은 파생을 방지 하기 위해 주로 사용 되지만 특정 런타임 최적화도 가능 합니다. 특히 있기 때문에 절대로 모든 파생된 클래스를 봉인된 클래스 알려져 가상 함수 멤버를 sealed 클래스 인스턴스에서 호출 비가상 호출으로 변환 합니다.

#### <a name="static-classes"></a>정적 클래스

합니다 `static` 한정자로 선언 되는 클래스를 표시 되는 ***정적 클래스***합니다. 정적 클래스는 인스턴스화할 수 없습니다, 형식으로 사용할 수 없습니다 및 정적 멤버만 포함할 수 있습니다. 정적 클래스에는 확장 메서드의 선언을 포함할 수만 ([확장 메서드](classes.md#extension-methods)).

정적 클래스 선언을 다음과 같은 제한 사항이 적용 됩니다.

*  정적 클래스를 포함 하지 않은 한 `sealed` 또는 `abstract` 한정자입니다. 그러나 Note, 정적 클래스는 인스턴스화되거나에서 파생 된 수 없습니다, 이후 작동 하는지 sealed 및 abstract 것 처럼 합니다.
*  정적 클래스는 포함 되지 않을 수는 *class_base* 사양 ([기본 사양 클래스](classes.md#class-base-specification)) 및 기본 클래스 또는 구현 된 인터페이스 목록에 명시적으로 지정할 수 없습니다. 정적 클래스 형식에서 암시적으로 상속 `object`합니다.
*  정적 클래스는 정적 멤버만 포함할 수 있습니다 ([정적 및 인스턴스 멤버](classes.md#static-and-instance-members)). 참고 상수 및 중첩된 형식은 정적 구성원으로 분류 됩니다.
*  정적 클래스 멤버를 사용할 수 없습니다 `protected` 또는 `protected internal` 접근성을 선언 합니다.

이는 이러한 제한 사항을 위반에 컴파일 타임 오류입니다.

정적 클래스 인스턴스에 생성자가 없습니다. 정적 클래스의 인스턴스 생성자와 기본 인스턴스 생성자를 선언 하는 것이 불가능 ([기본 생성자](classes.md#default-constructors)) 정적 클래스에 대해 제공 됩니다.

정적 클래스의 멤버 이며 자동으로 정적 멤버 선언에서 명시적으로 포함 해야는 `static` 한정자 (제외 하 고 상수 및 중첩 된 형식). 클래스는 정적 외부 클래스 내에서 중첩 되 면 중첩 된 클래스 경우 정적 클래스를 명시적으로 포함 하지 않는 한를 `static` 한정자입니다.

__정적 클래스 형식 참조__

A *namespace_or_type_name* ([Namespace 및 형식 이름](basic-concepts.md#namespace-and-type-names)) 경우에 정적 클래스를 참조할 수

*  *namespace_or_type_name* 은 합니다 `T` 에 *namespace_or_type_name* 폼의 `T.I`, 또는
*  *namespace_or_type_name* 는 `T` 에 *typeof_expression* ([인수 목록](expressions.md#argument-lists)1) 형식의 `typeof(T)`.

A *primary_expression* ([멤버 함수](expressions.md#function-members)) 경우에 정적 클래스를 참조할 수

*  *primary_expression* 는 `E` 에 *member_access* ([동적 오버 로드 확인 검사 하는 컴파일 타임](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) 폼의 `E.I`합니다.

다른 컨텍스트에서 정적 클래스를 참조 하는 컴파일 타임 오류 예를 들어, 것이 구성 요소 형식, 기본 클래스로 사용 하기 위한 정적 클래스에 대 한 오류 ([중첩 형식은](classes.md#nested-types)) 멤버, 제네릭 형식 인수 또는 형식 매개 변수 제약 조건입니다. 마찬가지로, 배열 형식, 포인터 형식에에서 정적 클래스를 사용할 수 없습니다는 `new` 식, 캐스트 식에는 `is` 식은 `as` 식을 `sizeof` 식 또는 기본 값 식.

### <a name="partial-modifier"></a>Partial 한정자

`partial` 한정자를 나타내는 데는이 *class_declaration* 부분 형식 선언 합니다. 에 지정 된 규칙에 따라 바깥쪽 형식 또는 네임 스페이스 선언 내에서 동일한 이름 가진 여러 부분 형식 선언을 폼 형식 선언에 결합 [부분 형식](classes.md#partial-types)합니다.

별도 프로그램 텍스트 세그먼트를 분산 하는 클래스 선언에 있는 이러한 세그먼트는 생성 하거나 다른 컨텍스트에서 유지 관리 하는 경우에 유용할 수 있습니다. 예를 들어 다른 수동으로 작성 하는 반면 클래스 선언에의 한 부분을 생성 하는 컴퓨터를 수 있습니다. 두 텍스트 분리는 다른 업데이트와의 충돌 씩 업데이트를 하지 않습니다.

### <a name="type-parameters"></a>형식 매개 변수

형식 매개 변수는 생성 된 형식을 만들려면 제공 되는 형식 인수에 대 한 자리 표시자를 나타내는 단순 식별자입니다. 형식 매개 변수는 나중에 제공 되는 형식에 대 한 형식 자리 표시자입니다. 반대로, 형식 인수 ([형식 인수](types.md#type-arguments)) 생성 된 형식을 만들 때 형식 매개 변수에 대해 대체 되는 실제 형식입니다.

```antlr
type_parameter_list
    : '<' type_parameters '>'
    ;

type_parameters
    : attributes? type_parameter
    | type_parameters ',' attributes? type_parameter
    ;

type_parameter
    : identifier
    ;
```

각 형식 매개 변수에 클래스 선언에서 선언 공간에 이름을 정의 ([선언](basic-concepts.md#declarations))는 클래스입니다. 따라서 다른 형식 매개 변수와 동일한 이름을 가질 수 없습니다 또는 해당 클래스에는 멤버가 선언 되었습니다. 형식 매개 변수 형식 자체와 동일한 이름을 사용할 수 없습니다.

### <a name="class-base-specification"></a>기본 클래스 사양

클래스 선언 포함 될 수 있습니다는 *class_base* 인터페이스와 클래스의 직접 기본 클래스를 정의 하는 사양 ([인터페이스](interfaces.md)) 클래스에 의해 직접 구현 합니다.

```antlr
class_base
    : ':' class_type
    | ':' interface_type_list
    | ':' class_type ',' interface_type_list
    ;

interface_type_list
    : interface_type (',' interface_type)*
    ;
```

클래스 선언에 지정 된 기본 클래스는 생성 된 클래스 형식일 수 있습니다 ([형식 생성](types.md#constructed-types)). 기본 클래스 범위에 있는 형식 매개 변수를 포함할 수 있지만 자체적으로 형식 매개 변수 수 없습니다.

```csharp
class Extend<V>: V {}            // Error, type parameter used as base class
```

#### <a name="base-classes"></a>기본 클래스

경우는 *class_type* 에 포함 되어는 *class_base*, 선언 되는 클래스의 직접 기본 클래스는 지정 합니다. 클래스 선언이 없으면 *class_base*, 또는 경우에는 *class_base* 만 목록에 인터페이스 형식, 직접 기본 클래스는 것으로 간주 됩니다 `object`합니다. 에 설명 된 대로 클래스의 직접 기본 클래스에서 멤버를 상속 [상속](classes.md#inheritance)합니다.

예제
```csharp
class A {}

class B: A {}
```
클래스 `A` 의 직접 기본 클래스 라고 `B`, 및 `B` 에서 파생 될 것 이라고 `A`합니다. 이후 `A` 는 직접 기본 클래스를 명시적으로 지정, 직접 기본 클래스는 암시적으로 `object`입니다.

생성 된 클래스 형식에 대 한 기본 클래스는 제네릭 클래스 선언에 지정 된 경우 생성 된 형식의 기본 클래스는 가져온 각각에 대 한 대체 하 여 *type_parameter* 해당 기본 클래스 선언에서 *type_argument* 생성 된 형식입니다. 지정 된 제네릭 클래스 선언
```csharp
class B<U,V> {...}

class G<T>: B<string,T[]> {...}
```
생성 된 형식의 기본 클래스 `G<int>` 것 `B<string,int[]>`입니다.

클래스 형식의 직접 기본 클래스는 적어도 클래스 형식 자체 수준 만큼 액세스 가능 해야 합니다. ([접근성 도메인](basic-concepts.md#accessibility-domains)). 예를 들어, 것이 대 한 컴파일 시간 오류를 `public` 에서 파생 된 클래스를 `private` 또는 `internal` 클래스입니다.

클래스 형식의 직접 기본 클래스는 아니어야 다음 형식 중 하나: `System.Array`, `System.Delegate`, `System.MulticastDelegate`합니다 `System.Enum`, 또는 `System.ValueType`합니다. 제네릭 클래스 선언의 사용할 수 없습니다는 또한 `System.Attribute` 직접 또는 간접 기본 클래스입니다.

직접 기본 클래스 지정의 의미를 확인 하는 동안 `A` 클래스의 `B`에서 직접 기본 클래스 `B` 일시적으로 간주 됩니다 `object`합니다. 직관적으로 이렇게 하면 기본 클래스를 지정 하는 의미 없는 재귀적으로 자체에 따라 달라 집니다. 예제:
```csharp
class A<T> {
   public class B {}
}

class C : A<C.B> {}
```
기본 클래스 사양에 올바르지 `A<C.B>` 의 직접 기본 클래스 `C` 것으로 간주 됩니다 `object`, 및 (규칙에 따라 [Namespace 및 형식 이름](basic-concepts.md#namespace-and-type-names)) `C` 간주 되지 않습니다 회원에 게 `B`합니다.

클래스 형식의 기본 클래스는 직접 기본 클래스 및 해당 기본 클래스입니다. 즉, 일련의 기본 클래스는 직접 기본 클래스 관계의 전이적 closure 합니다. 참조의 기본 클래스를 위의 예에서 `B` 됩니다 `A` 및 `object`합니다. 예제
```csharp
class A {...}

class B<T>: A {...}

class C<T>: B<IComparable<T>> {...}

class D<T>: C<T[]> {...}
```
기본 클래스 `D<int>` 됩니다 `C<int[]>`를 `B<IComparable<int[]>>`를 `A`, 및 `object`합니다.

클래스를 제외 하 고 `object`, 모든 클래스 형식에는 정확히 하나의 직접 기본 클래스입니다. `object` 클래스는 직접 기본 클래스가 없는 이며 다른 모든 클래스의 궁극적인 기본 클래스입니다.

때 클래스 `B` 클래스에서 파생 `A`에 대 한 컴파일 시간 오류 `A` 에 따라 달라 지도록 `B`합니다. 클래스 ***에 직접 종속*** 의 직접 기본 클래스 (있는 경우) 및 ***에 직접 종속*** 클래스는 즉시 중첩 (있는 경우). 이 정의 지정 된 클래스는 종속 하는 클래스의 전체 집합은 재귀 및 전이적인 종결 합니다 ***에 직접 종속*** 관계입니다.

이 예제에서
```csharp
class A: A {}
```
잘못 된 이므로 클래스 자체에 따라 달라 집니다. 마찬가지로, 예제
```csharp
class A: B {}
class B: C {}
class C: A {}
```
클래스는 순환적으로 자신에 종속 되어 있으므로 오류입니다. 마지막으로, 예제
```csharp
class A: B.C {}

class B: A
{
    public class C {}
}
```
때문에 컴파일 타임 오류가 발생 `A` 에 따라 달라 집니다 `B.C` (직접 기본 클래스인)에 따라 다름 `B` (가장 가까운 바깥쪽 클래스)를 순환 종속 `A`합니다.

참고 클래스 내에 중첩 된 클래스에 종속 되지 않습니다. 예제
```csharp
class A
{
    class B: A {}
}
```
`B` 에 따라 달라 집니다 `A` (때문 `A` 의 직접 기본 클래스와 가장 가까운 바깥쪽 클래스는), 있지만 `A` 에 의존 하지 `B` (하므로 `B` 이 기본 클래스도 아니고는 바깥쪽 클래스의 `A` ). 따라서이 예제에서는 유효합니다.

파생 될 수 있지는 `sealed` 클래스입니다. 예제
```csharp
sealed class A {}

class B: A {}            // Error, cannot derive from a sealed class
```
클래스 `B` 에서 파생 하려고 했기 때문에 오류에는 `sealed` 클래스 `A`합니다.

#### <a name="interface-implementations"></a>인터페이스 구현

A *class_base* 사양에 있는 경우 클래스는 직접 구현 한다고 지정된 된 인터페이스 형식을 인터페이스 형식 목록이 포함 될 수 있습니다. 인터페이스 구현을 설명에 대 한 자세한 [인터페이스 구현을](interfaces.md#interface-implementations)합니다.

### <a name="type-parameter-constraints"></a>형식 매개 변수 제약 조건

제네릭 형식 및 메서드 선언 형식 매개 변수 제약 조건을 포함 하 여 선택적으로 지정할 수 *type_parameter_constraints_clause*s입니다.

```antlr
type_parameter_constraints_clause
    : 'where' type_parameter ':' type_parameter_constraints
    ;

type_parameter_constraints
    : primary_constraint
    | secondary_constraints
    | constructor_constraint
    | primary_constraint ',' secondary_constraints
    | primary_constraint ',' constructor_constraint
    | secondary_constraints ',' constructor_constraint
    | primary_constraint ',' secondary_constraints ',' constructor_constraint
    ;

primary_constraint
    : class_type
    | 'class'
    | 'struct'
    ;

secondary_constraints
    : interface_type
    | type_parameter
    | secondary_constraints ',' interface_type
    | secondary_constraints ',' type_parameter
    ;

constructor_constraint
    : 'new' '(' ')'
    ;
```

각 *type_parameter_constraints_clause* 토큰 이루어져 `where`뒤에 형식 매개 변수의 이름, 콜론 및 해당 형식 매개 변수에 대 한 제약 조건 목록 뒤에 있습니다. 최대 하나만 수 `where` 각 형식 매개 변수에 대 한 절 및 `where` 절 순서에 관계 없이 나열할 수 있습니다. 같은 `get` 및 `set` 속성 접근자에서 토큰을 `where` 토큰은 키워드가 아닙니다.

에 지정 된 제약 조건 목록이 `where` 절에는 다음 구성 요소를이 순서 대로: 단일 기본 제약 조건, 하나 이상의 보조 제약 조건 및 생성자 제약 조건이 `new()`합니다.

기본 제약 조건 클래스 형식이 될 수 또는 ***참조 형식 제약 조건*** `class` 또는 ***값 형식 제약 조건*** `struct`합니다. 보조 제약 조건 수를 *type_parameter* 하거나 *interface_type*합니다.

참조 형식 제약 조건 형식 매개 변수를 사용 하는 형식 인수가 참조 형식이 되도록 지정 합니다. 모든 클래스 형식, 인터페이스 형식, 대리자 형식, 배열 형식 및 형식 매개 변수는 참조 형식 (아래 정의)은 알려진이 제약 조건을 만족 합니다.

값 형식 제약 조건 형식 매개 변수에 사용 되는 형식 인수를 null이 아닌 값 형식이 되도록 지정 합니다. Nullable이 아닌 구조체 형식, 열거형 형식 및 값 형식 제약 조건이 있는 형식 매개 변수를 모두이 제약 조건을 만족 합니다. 값 형식, null 허용 형식으로 분류 하는 있지만 ([Nullable 형식](types.md#nullable-types)) 값 형식 제약 조건을 충족 하지 않습니다. 값 형식 제약 조건이 있는 형식 매개 변수를 가질 수 없습니다는 *constructor_constraint*합니다.

포인터 형식은 형식 인수를 허용 되지 않습니다 및 중 하나는 참조 형식 또는 값 형식 제약 조건을 만족 하는 고려 되지 않습니다.

클래스 형식, 인터페이스 형식 또는 형식 매개 변수 제약 조건이 있으면 해당 형식은 최소한의 "기본 형식" 해당 형식 매개 변수에 사용 되는 모든 형식 인수를 지원 해야 하는 지정 합니다. 생성 된 형식 또는 제네릭 메서드를 사용할 때마다 형식 인수는 컴파일 시 형식 매개 변수에 대 한 제약 조건에 대해 확인 됩니다. 제공 된 형식 인수에 설명 된 조건에 맞아야 [제약 조건을 만족](types.md#satisfying-constraints)합니다.

A *class_type* 제약 조건에는 다음 규칙을 충족 해야 합니다.

*  형식을은 클래스 형식 이어야 합니다.
*  형식이 아니어야 `sealed`합니다.
*  형식이 아니어야 다음 형식 중 하나: `System.Array`, `System.Delegate`를 `System.Enum`, 또는 `System.ValueType`합니다.
*  형식이 아니어야 `object`합니다. 모든 형식에서 파생 되므로 `object`, 허용 된 경우 이러한 제약 조건을 효과가 해야 합니다.
*  최대 제약 조건을 지정 된 형식 매개 변수는 클래스 형식일 수 있습니다.

으로 지정 된 형식을 *interface_type* 제약 조건에는 다음 규칙을 충족 해야 합니다.

*  형식을은 인터페이스 형식 이어야 합니다.
*  형식에서 두 번 이상 지정 하지 해야 합니다는 주어진 `where` 절.

두 경우 모두에서 제약 조건이 연결된 형식 또는 메서드 선언을 생성 된 형식의 일부로 형식 매개 변수 중 하나를 포함할 수 있습니다 하 고 중인 선언 된 형식이 포함 될 수 있습니다.

형식 매개 변수 제약 조건 이상 액세스 가능 해야 합니다. 지정 된 모든 클래스 또는 인터페이스 형식 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)) 제네릭 형식 또는 선언 되는 메서드.

로 지정 된 형식에 *type_parameter* 제약 조건에는 다음 규칙을 충족 해야 합니다.

*  형식은 형식 매개 변수 이어야 합니다.
*  형식에서 두 번 이상 지정 하지 해야 합니다는 주어진 `where` 절.

또한 있어야 순환이 종속성으로 정의 된 전이적 관계가 인 형식 매개 변수 종속성 그래프에서:

*  경우 형식 매개 변수 `T` 형식 매개 변수는 제약 조건으로 사용 됩니다 `S` 한 다음 `S` ***종속*** `T`합니다.
*  경우 형식 매개 변수 `S` 형식 매개 변수에 따라 달라 집니다 `T` 하 고 `T` 형식 매개 변수에 따라 달라 집니다 `U` 한 다음 `S` ***에 따라 달라 집니다*** `U`합니다.

이 관계를 지정 합니다 (직접 또는 간접적으로) 자체에 따라 형식 매개 변수의 컴파일 타임 오류를 것입니다.

모든 제약 조건을 종속 형식 매개 변수 간에 일치 해야 합니다. 경우 형식 매개 변수 `S` 형식 매개 변수에 따라 달라 집니다 `T` 후:

*  `T` 값 형식 제약 조건이 없어야 합니다. 이 고, 그렇지 `T` 는 효과적으로 봉인 되어 있으므로 `S` 를 동일한 형식 이어야 `T`, 두 형식 매개 변수에 대 한 필요성을 제거 합니다.
*  경우 `S` 에 다음 값 형식 제약 조건이 `T` 없어야를 *class_type* 제약 조건입니다.
*  하는 경우 `S` 에 *class_type* 제약 조건 `A` 및 `T` 에 *class_type* 제약 조건 `B` id 변환이 있어야 암시적 또는 참조에서 변환 `A` 하 `B` 또는에서 암시적 참조 변환이 `B` 에 `A`합니다.
*  하는 경우 `S` 형식 매개 변수에 따라 달라 집니다 `U` 및 `U` 에 *class_type* 제약 조건 `A` 및 `T` 에 *class_type* 제약조건`B` 는 id 변환을 또는에서 암시적 참조 변환이 있어야 `A` 하 `B` 또는에서 암시적 참조 변환이 `B` 에 `A`합니다.

에 대 한 유효 `S` 있어야 값 형식 제약 조건 및 `T` 참조 형식 제약 조건이 있어야 합니다. 이 제한 하는 효과적으로 `T` 형식으로 `System.Object`, `System.ValueType`, `System.Enum`, 및 임의의 인터페이스 형식입니다.

경우는 `where` 절 형식 매개 변수에 생성자 제약 조건이 포함 되어 있습니다 (폼에 있는 `new()`)를 사용 하는 것이 가능를 `new` 형식의 인스턴스를 만들려면 연산자 ([개체 만들기 식](expressions.md#object-creation-expressions)). 모든 형식이 사용 되는 인수 또는 값 형식 제약 조건 또는 생성자 제약 조건 (참조 형식 매개 변수로 생성자 제약 조건이 있는 형식 매개 변수 (이 생성자 암시적으로 있는 모든 값 형식에 대 한) 매개 변수가 없는 public 생성자가 있어야 합니다 [형식 매개 변수 제약 조건](classes.md#type-parameter-constraints) 세부 정보에 대 한).

다음은 제약 조건의 예입니다.
```csharp
interface IPrintable
{
    void Print();
}

interface IComparable<T>
{
    int CompareTo(T value);
}

interface IKeyProvider<T>
{
    T GetKey();
}

class Printer<T> where T: IPrintable {...}

class SortedList<T> where T: IComparable<T> {...}

class Dictionary<K,V>
    where K: IComparable<K>
    where V: IPrintable, IKeyProvider<K>, new()
{
    ...
}
```

다음 예제에서는 형식 매개 변수 종속성 그래프에는 순환이 발생 하기 때문에 오류가 있음:
```csharp
class Circular<S,T>
    where S: T
    where T: S                // Error, circularity in dependency graph
{
    ...
}
```

다음 예제에서는 추가 잘못 된 상황을 보여 줍니다.
```csharp
class Sealed<S,T>
    where S: T
    where T: struct        // Error, T is sealed
{
    ...
}

class A {...}

class B {...}

class Incompat<S,T>
    where S: A, T
    where T: B                // Error, incompatible class-type constraints
{
    ...
}

class StructWithClass<S,T,U>
    where S: struct, T
    where T: U
    where U: A                // Error, A incompatible with struct
{
    ...
}
```

합니다 ***유효한 기본 클래스*** 형식 매개 변수의 `T` 다음과 같이 정의 됩니다.

*  하는 경우 `T` 에 기본 제한이 아니거나 유효한 기본 클래스 형식 매개 변수 제약 조건이 `object`합니다.
*  하는 경우 `T` 값 형식 제약 조건이 유효한 기본 클래스는 `System.ValueType`합니다.
*  하는 경우 `T` 에 *class_type* 제약 조건 `C` 없는 *type_parameter* 제약 조건 적용 해당 기본 클래스는 `C`합니다.
*  하는 경우 `T` 아무런 *class_type* 제약 조건 이지만 하나 이상의 *type_parameter* 유효한 기본 클래스 제약 조건 형식이 최하위 ([변환 리프트 연산자](conversions.md#lifted-conversion-operators))의 유효한 기본 클래스의 집합에 해당 *type_parameter* 제약 조건입니다. 일관성 규칙 이러한 최하위 형식이 있는지 확인 합니다.
*  경우 `T` 둘 다 포함 된 *class_type* 제약 조건 및 하나 이상의 *type_parameter* 유효한 기본 클래스 제약 조건 형식이 최하위 ([변환 리프트 연산자](conversions.md#lifted-conversion-operators))로 구성 된 집합에는 *class_type* 의 제약 조건을 `T` 의 유효 기본 클래스 및 해당 *type_parameter* 제약 조건입니다. 일관성 규칙 이러한 최하위 형식이 있는지 확인 합니다.
*  하는 경우 `T` 가 참조 형식 제약 조건 이지만 *class_type* 제약 조건 적용 해당 기본 클래스는 `object`합니다.

T 제약 조건이 있으면 이러한 규칙을 위해 `V` 즉를 *value_type*의 가장 구체적인 기본 형식 대신 `V` 즉를 *class_type*합니다. 이 절대를 명시적으로 지정 된 제약 조건에서 발생할 수 있지만 제네릭 메서드의 제약 조건을 재정의 메서드 선언 또는 인터페이스 메서드의 명시적 구현으로 암시적으로 상속 하는 경우 발생할 수 있습니다.

이러한 규칙 확인 유효한 기본 클래스는 항상을 *class_type*합니다.

합니다 ***효과적인 인터페이스 집합*** 형식 매개 변수의 `T` 다음과 같이 정의 됩니다.

*  하는 경우 `T` 가 없는 *secondary_constraints*, 해당 효과적인 인터페이스 집합이 비어 있습니다.
*  경우 `T` 했습니다 *interface_type* 제약 조건 이지만 *type_parameter* 제약 조건과 해당 효과적인 인터페이스 집합은 해당 집합 *interface_type* 제약 조건입니다.
*  하는 경우 `T` 가 없는 *interface_type* 제약 조건 않았으나 *type_parameter* 제약 조건과 해당 효과적인 인터페이스 집합이의 효과적인 인터페이스 집합의 합집합 해당 *형식 매개 변수* 제약 조건입니다.
*  하는 경우 `T` 가 모두 *interface_type* 제약 조건 및 *type_parameter* 제약 조건과 해당 효과적인 인터페이스 집합은 해당 집합의 합집합 *interface_type* 제약 조건 및 효과적인 인터페이스 집합을 해당 *type_parameter* 제약 조건입니다.

형식 매개 변수 ***참조 형식으로 알려진*** 하는 경우 참조 형식 제약 조건에 없거나 유효한 기본 클래스인 `object` 또는 `System.ValueType`합니다.

제한 된 형식 매개 변수 값 제약 조건 사용 권한에 포함 된 인스턴스 멤버에 액세스 하려면 사용할 수 있습니다. 예제
```csharp
interface IPrintable
{
    void Print();
}

class Printer<T> where T: IPrintable
{
    void PrintOne(T x) {
        x.Print();
    }
}
```
메서드 `IPrintable` 에서 직접 호출할 수 있습니다 `x` 있으므로 `T` 항상 구현 하도록 제한 됩니다 `IPrintable`합니다.

### <a name="class-body"></a>클래스 본문

합니다 *class_body* 클래스의 해당 클래스의 멤버를 정의 합니다.

```antlr
class_body
    : '{' class_member_declaration* '}'
    ;
```

## <a name="partial-types"></a>부분 형식

형식 선언을 여러 분할 될 수 있습니다 ***부분 형식 선언을***합니다. 형식 선언 프로그램의 컴파일 시간 및 런타임 처리의 나머지 부분 중 단일 선언으로 처리 됩니다 보내지고 해당 부분에서이 섹션에서는 규칙에 따라 생성 됩니다.

A *class_declaration*, *struct_declaration* 하거나 *interface_declaration* 포함 된 경우 부분 형식 선언을 나타냅니다는 `partial` 한정자. `partial` 키워드 아니며 바로 앞에 키워드 중 하나가 표시 되는 경우 해당 한정자로 역할만 `class`, `struct` 하거나 `interface` 형식 선언에서 또는 형식 앞 `void` 메서드 선언에서. 다른 컨텍스트에서 일반 식별자로 사용 될 수 있습니다.

각 부분 부분 형식 선언 포함 해야 합니다는 `partial` 한정자입니다. 이름이 있어야 하 고 동일한 네임 스페이스 또는 다른 부분 형식 선언에서 선언 합니다. 합니다 `partial` 한정자는 형식 선언의 추가 파트를 다른 곳에서 있을 수 있지만 이러한 추가 파트의 존재 여부 요구 사항은 아닙니다. 나타내고 포함할 단일 선언 된 형식에 대해 유효 합니다 `partial` 한정자입니다.

파트에는 단일 형식 선언을 컴파일 타임에 병합할 수 있도록 부분 형식의 모든 부분을 함께 컴파일된 수 있어야 합니다. 부분 형식 확장 되도록 이미 컴파일된 형식을 허용 하지 않습니다.

중첩 된 형식을 사용 하 여 여러 부분에서 선언할 수 있습니다는 `partial` 한정자입니다. 일반적으로 포함 하는 형식을 사용 하 여 선언 된 `partial` 하며 중첩 형식의 각 부분, 포함 하는 형식의 다른 부분에 선언 됩니다.

`partial` 한정자 대리자 또는 열거형 선언에서 허용 되지 않습니다.

### <a name="attributes"></a>특성

부분 형식의 특성은는 지정 되지 않은 순서에 따라 특성의 각 부분을 결합 하 여 결정 됩니다. 특성은 여러 부분에 배치 되 면 형식에 특성을 여러 번 지정 하는 것이 같습니다. 예를 들어, 두 부분:

```csharp
[Attr1, Attr2("hello")]
partial class A {}

[Attr3, Attr2("goodbye")]
partial class A {}
```
동일 선언에 같은 합니다.
```csharp
[Attr1, Attr2("hello"), Attr3, Attr2("goodbye")]
class A {}
```

형식 매개 변수의 특성 비슷한 방식으로 결합합니다.

### <a name="modifiers"></a>한정자

부분 형식 선언을 내게 필요한 옵션 지정을 포함 하는 경우 (합니다 `public`, `protected`를 `internal`, 및 `private` 한정자) 내게 필요한 옵션 지정을 포함 하는 다른 모든 부분을 사용 하 여 동의 해야 합니다. 형식을 적절 한 기본 액세스 가능성을 지정은 부분 형식 부분이 내게 필요한 옵션 사양에 포함 된 경우 ([접근성을 선언](basic-concepts.md#declared-accessibility)).

중첩 된 형식의 부분 선언을 하나 이상 포함 하는 경우는 `new` 한정자를 중첩 된 형식 상속된 된 멤버를 숨깁니다 하는 경우 경고 없이 보고 됩니다 ([상속을 통해 숨기기](basic-concepts.md#hiding-through-inheritance)).

클래스의 partial 선언을 하나 이상 포함 하는 경우는 `abstract` 한정자가 클래스를 abstract로 간주 됩니다 ([추상 클래스](classes.md#abstract-classes)). 그렇지 않은 경우 클래스는 추상이 아닌 간주 됩니다.

클래스의 partial 선언을 하나 이상 포함 하는 경우는 `sealed` 한정자를 클래스는 sealed로 간주 됩니다 ([클래스를 봉인](classes.md#sealed-classes)). 그렇지 않으면 클래스에는 것으로 간주 됩니다 봉인 되지 않은 합니다.

클래스는 abstract 이면 서 sealed 일 수 없습니다는 참고 합니다.

경우는 `unsafe` 한정자는 해당 특정 부분에는 안전 하지 않은 컨텍스트 것으로 간주 됩니다만 부분 형식 선언에 사용 됩니다 ([안전 하지 않은 컨텍스트](unsafe-code.md#unsafe-contexts)).

### <a name="type-parameters-and-constraints"></a>형식 매개 변수 및 제약 조건

제네릭 형식의 여러 파트에서 선언 된 경우 각 파트 형식 매개 변수를 명시 해야 합니다. 각 파트 순서 대로 각 형식 매개 변수에 대해 동일한 이름과 동일한 형식 매개 변수 수 있어야 합니다.

부분 제네릭 형식 선언의 제약 조건을 포함 하는 경우 (`where` 절), 제약 조건을 제약 조건을 포함 하는 다른 모든 부분에 동의 해야 합니다. 구체적으로 제약 조건을 포함 하는 각 파트에는 동일한 형식 매개 변수 집합에 대 한 제약 조건이 있어야 합니다. 및 각 형식 매개 변수 집합을 기본 보조 및 생성자 제약 조건 동일 해야 합니다. 동일한 멤버를 포함 하는 경우 두 가지 제약 조건이 동일 합니다. 형식 매개 변수 제약 조건이 제한 되지 않은 매개 변수를 사용 하는 것으로 간주 형식을 지정 하는 부분이 부분 제네릭 형식입니다.

이 예제에서
```csharp
partial class Dictionary<K,V>
    where K: IComparable<K>
    where V: IKeyProvider<K>, IPersistable
{
    ...
}

partial class Dictionary<K,V>
    where V: IPersistable, IKeyProvider<K>
    where K: IComparable<K>
{
    ...
}

partial class Dictionary<K,V>
{
    ...
}
```
올바른 제약 조건 (처음 두 개)를 효과적으로 포함 하는 부분만 지정 같은 보조의 기본 설정 및 동일한 형식 매개 변수 집합에 대 한 생성자 제약 조건 때문에 각각입니다.

### <a name="base-class"></a>기본 클래스

Partial 클래스 선언 기본 클래스 지정을 포함 하는 경우에 기본 클래스 지정을 포함 하는 다른 모든 부분을 사용 하 여 동의 해야 합니다. Partial 클래스의 기본 클래스 지정을 포함 하는 경우 기본 클래스 됩니다 `System.Object` ([기본 클래스](classes.md#base-classes)).

### <a name="base-interfaces"></a>기본 인터페이스

여러 부분으로 선언 된 형식에 대 한 기본 인터페이스 집합이 각 부분에 지정 된 기본 인터페이스의 합집합입니다. 각 부분에서 특정 기본 인터페이스를 한 번 이름은 될 수 있습니다 하지만 동일한 기본 인터페이스 이름을 여러 부분에 대 한 허용 됩니다. 지정 된 모든 기본 인터페이스 멤버의 하나의 구현만 있어야 합니다.

예제
```csharp
partial class C: IA, IB {...}

partial class C: IC {...}

partial class C: IA, IB {...}
```
클래스에 대 한 기본 인터페이스 집합이 `C` 됩니다 `IA`를 `IB`, 및 `IC`합니다.

각 부분에 해당 파트에 선언 된 인터페이스의 구현을 제공 하는 일반적으로 그러나이 요구 사항은 아닙니다. 일부 다른 부분에 선언 된 인터페이스의 구현을 제공할 수 있습니다.
```csharp
partial class X
{
    int IComparable.CompareTo(object o) {...}
}

partial class X: IComparable
{
    ...
}
```

### <a name="members"></a>멤버

부분 메서드를 제외 하 고 ([부분 메서드](classes.md#partial-methods)), 여러 부분에 선언 된 형식의 멤버 집합이 각 부분에 선언 된 멤버 집합의 합집합 하기만 하면 됩니다. 동일한 선언 공간을 공유 하는 형식 선언의 모든 부분의 본문 ([선언](basic-concepts.md#declarations)), 및 각 멤버의 범위 ([범위](basic-concepts.md#scopes)) 모든 부분의 본문을 확장 합니다. 모든 멤버의 액세스 가능 도메인은 항상; 바깥쪽 형식의 모든 부분을 포함 `private` 한 부분에 선언 된 멤버는 다른 부분에서 자유롭게 액세스할 수 있습니다. 해당 멤버 형식 아닌 형식의 둘 이상의 파트가 동일한 멤버를 선언 하는 컴파일 시간 오류는 것은 `partial` 한정자입니다.

```csharp
partial class A
{
    int x;                     // Error, cannot declare x more than once

    partial class Inner        // Ok, Inner is a partial type
    {
        int y;
    }
}

partial class A
{
    int x;                     // Error, cannot declare x more than once

    partial class Inner        // Ok, Inner is a partial type
    {
        int z;
    }
}
```

형식 내 멤버의 순서를 C# 코드를 거의 상당 하지만 다른 언어 및 환경와 상호 작용 하는 경우 상당히 높을 수 있습니다. 이러한 경우 여러 부분에 선언 된 형식 내 멤버의 순서가 정의 되지 않습니다.

### <a name="partial-methods"></a>부분 메서드

부분 메서드 형식 선언의 한 부분에서 정의 하 고 다른 구현 합니다. 구현은 선택 사항입니다. 부분 메서드를 구현 하는 부분이 없으면 partial 메서드 선언 및 모든 호출에 파트의 조합을 통해 결과 형식 선언에서 제거 됩니다.

부분 메서드 액세스 한정자를 정의할 수 없습니다. 하지만 암시적으로 `private`입니다. 반환 형식 이어야 합니다 `void`, 해당 매개 변수에 사용할 수 없습니다는 `out` 한정자입니다. 식별자 `partial` 직전 표시 되는 경우에 메서드 선언에서 특별 한 키워드로 인식 되는 `void` 입력, 그렇지 않으면 일반 식별자로 사용할 수 있습니다. 부분 메서드 인터페이스 메서드를 명시적으로 구현할 수 없습니다.

(Partial method) 선언의 두 가지가: 선언을 라고 메서드 선언의 본문 세미콜론 인 경우는 ***partial 메서드 선언 정의***합니다. 본문으로 지정 하는 경우는 *블록*를 선언 이라고는 ***partial 메서드 선언 구현***합니다. 형식 선언의 파트에서 사용할 수 있습니다만 지정 된 서명 사용 하 여 partial 메서드 선언에 정의 및 지정 된 서명 사용 하 여 partial 메서드 선언 구현 하나만 있을 수 있습니다. 다음에 지정 된 구현 partial 메서드 선언이 지정 하는, 해당 partial 메서드 선언에 정의 존재 해야 하며 선언으로 일치 해야 하는 경우:

* 선언 (하지만 반드시 동일한 순서로)는 같은 한정자가 있어야 합니다, 메서드 이름, 형식 매개 변수의 수 및 매개 변수 개수입니다.
* 해당 매개 변수 선언에는 (하지만 반드시 동일한 순서로)는 같은 한정자 있어야 형식과 동일한 형식 매개 변수 이름과 차이점) (모듈로.
* 해당 형식 매개 변수 선언에서 동일한 제약 조건 (형식 매개 변수 이름과 차이점) 모듈로 있어야 합니다.

구현 partial 메서드 선언이 해당 정의 partial 메서드 선언으로 동일한 부분에 나타날 수 있습니다.

부분 메서드 정의 오버 로드 확인에 참여합니다. 따라서 여부는 구현 선언이 지정 되 면 호출 식 부분 메서드 호출을 해결할 수 있습니다. 부분 메서드는 항상 반환 하므로 `void`, 이러한 호출 식에서 식 문은 항상 됩니다. 또한 부분 메서드를 암시적으로 이므로 `private`, 이러한 문의 부분 메서드는 선언 된 형식 선언 부분 중 하나에서 항상 발생 합니다.

부분 형식 선언 부분이 지정된 부분 메서드에 대 한 구현 선언이 있으면 호출 하는 모든 식 문은 단순히 결합 된 형식 선언에서 제거 됩니다. 따라서 호출 식에 모든 구성 요소 식을 포함 하 여 런타임 시 효과가 없습니다. 부분 메서드 자체 제거도 되 고 결합 된 형식 선언에 소속 되지 않습니다.

지정 된 부분 메서드의 구현 선언이 없으면 부분 메서드의 호출 유지 됩니다. 부분 메서드는 다음을 제외한 구현 partial 메서드 선언 비슷합니다 메서드 선언에 증가 제공합니다.

* `partial` 한정자 포함 되지 않습니다.
* 결과 메서드 선언에서 특성은 지정 되지 않은 순서로 정의 및 구현 partial 메서드 선언 결합 된 특성. 중복 제거 되지 않습니다.
* 결과 메서드 선언의 매개 변수에 대 한 특성은 지정 되지 않은 순서로 정의 및 구현 partial 메서드 선언 매개 변수를 해당의 결합 된 특성. 중복 제거 되지 않습니다.

부분 메서드 M에 대 한 정의 선언이 있지만 구현 선언이 없습니다 주어진 경우에 다음과 같은 제한 사항이 적용 됩니다.

* 메서드에 대리자를 만드는 컴파일 타임 오류 ([대리자 생성 식](expressions.md#delegate-creation-expressions)).
* 컴파일 타임 오류를 가리키도록 `M` 식 트리 형식으로 변환 되는 익명 함수 내에서 ([익명 함수 식 트리 형식으로의 변환의 평가](conversions.md#evaluation-of-anonymous-function-conversions-to-expression-tree-types)).
* 호출의 일부로 발생 하는 식 `M` 한정 된 할당 상태에 영향을 주지 않습니다 ([한정 된 할당](variables.md#definite-assignment)), 잠재적으로 컴파일 시간 오류가 발생할 수 있습니다.
* `M` 응용 프로그램에 대 한 진입점이 될 수 없습니다 ([응용 프로그램 시작](basic-concepts.md#application-startup)).

부분 메서드는 도구에 의해 생성 되는 예를 들어 하나는 다른 파트의 동작을 사용자 지정 형식 선언의 한 부분을 허용 하는 데 유용 합니다. 다음 partial 클래스 선언을 살펴보세요.
```csharp
partial class Customer
{
    string name;

    public string Name {
        get { return name; }
        set {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }

    }

    partial void OnNameChanging(string newName);

    partial void OnNameChanged();
}
```

이 클래스는 다른 부분 없이 컴파일 정의 partial 메서드 선언 및 해당 호출은 제거할 수 있으며, 결과 결합된 클래스 선언 다음에 해당 됩니다.
```csharp
class Customer
{
    string name;

    public string Name {
        get { return name; }
        set { name = value; }
    }
}
```

하지만 다른 부분을 지정 부분 메서드의 구현 선언만 제공 하는 것으로 가정 합니다.
```csharp
partial class Customer
{
    partial void OnNameChanging(string newName)
    {
        Console.WriteLine("Changing " + name + " to " + newName);
    }

    partial void OnNameChanged()
    {
        Console.WriteLine("Changed to " + name);
    }
}
```

그런 다음 결과 결합된 클래스 선언 다음에 해당 됩니다.
```csharp
class Customer
{
    string name;

    public string Name {
        get { return name; }
        set {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }

    }

    void OnNameChanging(string newName)
    {
        Console.WriteLine("Changing " + name + " to " + newName);
    }

    void OnNameChanged()
    {
        Console.WriteLine("Changed to " + name);
    }
}
```

### <a name="name-binding"></a>이름 바인딩

하지만 동일한 네임 스페이스 안에서 선언 되어야 확장할 수 있는 형식의 각 부분을 파트를 다른 네임 스페이스 선언 내에서 일반적으로 기록 됩니다. 따라서 다른 `using` 지시문 ([지시문을 사용 하 여](namespaces.md#using-directives)) 각 부분에 있을 수 있습니다. 단순 이름을 해석 하는 경우 ([형식 유추](expressions.md#type-inference))만 하나의 파트 내에서 `using` 지시문의 해당 파트를 바깥쪽 네임 스페이스 선언으로 간주 됩니다. 이 서로 다른 부분에 다른 의미를 포함 하는 동일한 식별자에 발생할 수 있습니다.
```csharp
namespace N
{
    using List = System.Collections.ArrayList;

    partial class A
    {
        List x;                // x has type System.Collections.ArrayList
    }
}

namespace N
{
    using List = Widgets.LinkedList;

    partial class A
    {
        List y;                // y has type Widgets.LinkedList
    }
}
```

## <a name="class-members"></a>클래스 멤버

클래스의 멤버 구성에서 도입 된 멤버의 해당 *class_member_declaration*s 및 멤버는 직접 기본 클래스에서 상속 합니다.

```antlr
class_member_declaration
    : constant_declaration
    | field_declaration
    | method_declaration
    | property_declaration
    | event_declaration
    | indexer_declaration
    | operator_declaration
    | constructor_declaration
    | destructor_declaration
    | static_constructor_declaration
    | type_declaration
    ;
```

클래스 형식의 멤버는 다음 범주로 구분 됩니다.

*  클래스와 연결 된 상수 값을 나타내는 상수 ([상수](classes.md#constants)).
*  클래스의 변수는 필드 ([필드](classes.md#fields)).
*  계산 및 클래스로 수행할 수 있는 작업을 구현 하는 메서드 ([메서드](classes.md#methods)).
*  속성을 정의 하는 특성 이름이 및 읽기 및 쓰기 이러한 특징을 연관 된 작업 ([속성](classes.md#properties)).
*  클래스에 의해 생성 될 수 있는 알림을 정의 하는 이벤트 ([이벤트](classes.md#events)).
*  인덱서를 동일한 방식으로 허용 되는 인덱싱 클래스의 인스턴스를 허용 하는 배열로 (구문상) ([인덱서](classes.md#indexers)).
*  클래스의 인스턴스를 적용할 수 있는 식 연산자를 정의 하는 연산자 ([연산자](classes.md#operators)).
*  인스턴스 클래스의 인스턴스를 초기화 하는 데 필요한 작업을 구현 하는 생성자 ([인스턴스 생성자](classes.md#instance-constructors))
*  소멸자는 클래스의 인스턴스를 영구적으로 삭제 되기 전에 수행할 작업을 구현 하는 ([소멸자](classes.md#destructors)).
*  자체 클래스를 초기화 하는 데 필요한 작업을 구현 하는 정적 생성자 ([정적 생성자](classes.md#static-constructors)).
*  로컬 클래스에 있는 형식을 나타내는 형식 ([중첩 형식은](classes.md#nested-types)).

실행 코드를 포함할 수 있는 멤버 라고 통칭 합니다 *멤버 함수* 클래스 형식입니다. 클래스 형식의 함수 멤버는 메서드, 속성, 이벤트, 인덱서, 연산자, 인스턴스 생성자, 소멸자 및 해당 클래스 형식의 정적 생성자는 합니다.

A *class_declaration* 새 선언 공간을 만듭니다 ([선언](basic-concepts.md#declarations)), 및 *class_member_declaration*포함 된 즉시 s는 *클래스 _declaration* 이 선언 공간에 새 멤버를 정의 합니다. 다음 규칙이 적용 됩니다 *class_member_declaration*s:

*  인스턴스 생성자, 소멸자 및 정적 생성자에는 바로 바깥쪽 클래스 이름이 있어야 합니다. 다른 모든 멤버에는 가장 가까운 바깥쪽 클래스의 이름에서 다른 이름이 있어야 합니다.
*  상수, 필드, 속성, 이벤트 또는 형식 이름의 동일한 클래스에서 선언 된 다른 모든 멤버의 이름과에서 달라 야 합니다.
*  메서드의 이름을 메서드 이름에 다른 모든 비-동일한 클래스에서 선언에서 달라 야 합니다. 또한 서명 ([시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading))의 메서드는 같은 클래스에 선언 된 다른 모든 메서드의 시그니처와 달라 야 하 고 동일한 클래스에서 선언 하는 두 가지 방법만 다른 서명이 없을 수 있습니다 하 여 `ref` 고 `out`입니다.
*  인스턴스 생성자의 시그니처는 동일한 클래스에서 선언 된 다른 모든 인스턴스 생성자의 시그니처와에서 달라 야 하 고 동일한 클래스에서 선언 하는 두 명의 생성자에 의해만 다른 서명이 없을 `ref` 고 `out`입니다.
*  인덱서의 시그니처는 동일한 클래스에서 선언 된 다른 모든 인덱서의 시그니처와 달라 야 합니다.
*  연산자의 서명이 동일한 클래스에 선언 된 다른 모든 연산자의 시그니처와에서 달라 야 합니다.

클래스 형식의 상속된 된 멤버 ([상속](classes.md#inheritance))은 클래스의 선언 공간에 속하지 않습니다. 따라서 파생된 클래스는 상속 된 멤버 (상속 된 멤버를 숨깁니다 적용)와 이름 또는 시그니처가 같은 사용 하 여 멤버를 선언할 수 있습니다.

### <a name="the-instance-type"></a>인스턴스 형식

각 클래스 선언에는 연관 된 바인딩된 형식 ([바인딩되며 형식에 바인딩되지 않은](types.md#bound-and-unbound-types)), ***인스턴스 유형***합니다. 제네릭 클래스 선언에 대 한 인스턴스 유형이 생성된 된 형식을 만들어 형식이 ([형식 생성](types.md#constructed-types)) 형식 선언에서 지정 된 유형의 각 인수는 해당 형식 매개 변수입니다. 형식 매개 변수를 사용 하는 인스턴스 형식에 있으므로 사용할 수 있습니다만 범위에 형식 매개 변수가 있는 즉, 클래스 선언 안에 있습니다. 인스턴스 형식의 형식인 `this` 클래스 선언 내에서 작성 된 코드에 대 한 합니다. 제네릭이 아닌 클래스에 대 한 인스턴스 유형 단순히 선언 된 클래스입니다. 다음은 해당 인스턴스 형식과 함께 여러 클래스 선언입니다. 
```csharp
class A<T>                           // instance type: A<T>
{
    class B {}                       // instance type: A<T>.B
    class C<U> {}                    // instance type: A<T>.C<U>
}

class D {}                           // instance type: D
```

### <a name="members-of-constructed-types"></a>생성 된 형식의 멤버

생성 된 형식의 상속 되지 않는 멤버 각각에 대 한 대체 하 여 가져온 *type_parameter* 해당 멤버 선언에서 *type_argument* 생성 된 형식입니다. 대체 프로세스의 형식 선언, 의미 체계 의미를 기반으로 하는 아니며 단순히 텍스트 대체 합니다.

예를 들어 제네릭 클래스 선언
```csharp
class Gen<T,U>
{
    public T[,] a;
    public void G(int i, T t, Gen<U,T> gt) {...}
    public U Prop { get {...} set {...} }
    public int H(double d) {...}
}
```
생성된 된 형식을 `Gen<int[],IComparable<string>>` 에 다음 멤버가 있습니다.
```csharp
public int[,][] a;
public void G(int i, int[] t, Gen<IComparable<string>,int[]> gt) {...}
public IComparable<string> Prop { get {...} set {...} }
public int H(double d) {...}
```

멤버의 형식을 `a` 제네릭 클래스 선언에서 `Gen` 는 "2 차원 배열을 `T`" 이므로 멤버의 형식을 `a` 위의 생성 된 형식에는 "1 차원 배열의 2차원배열`int`", 또는 `int[,][]`합니다.

형식의 인스턴스 함수 범위로 `this` 인스턴스 유형 인지 ([인스턴스 유형을](classes.md#the-instance-type)) 포함 하는 선언 합니다.

제네릭 클래스의 모든 멤버는 직접적으로 또는 생성 된 형식의 일부로 모든 바깥쪽 클래스에서 형식 매개 변수를 사용할 수 있습니다. 특정 닫을 때 생성 된 형식 ([열기 및 닫힌 형식을](types.md#open-and-closed-types))는 실행 시 생성 된 형식에 제공 되는 실제 형식 인수를 사용 하 여 형식 매개 변수를 사용할 때마다 바뀝니다. 예를 들어:
```csharp
class C<V>
{
    public V f1;
    public C<V> f2 = null;

    public C(V x) {
        this.f1 = x;
        this.f2 = this;
    }
}

class Application
{
    static void Main() {
        C<int> x1 = new C<int>(1);
        Console.WriteLine(x1.f1);        // Prints 1

        C<double> x2 = new C<double>(3.1415);
        Console.WriteLine(x2.f1);        // Prints 3.1415
    }
}
```

### <a name="inheritance"></a>상속

클래스 ***상속*** 직접 기본 클래스 형식의 멤버입니다. 상속은 클래스는 직접 기본 클래스 형식의 인스턴스 생성자, 소멸자 및 기본 클래스의 정적 생성자를 제외한 모든 멤버를 암시적으로 포함 하는 것을 의미 합니다. 상속의 몇 가지 중요 한 측면은:

*  상속은 전이 됩니다. 경우 `C` 에서 파생 됩니다 `B`, 및 `B` 에서 파생 됩니다 `A`, 한 다음 `C` 에 선언 된 멤버를 상속 `B` 에 선언 된 멤버 뿐만 아니라 `A`합니다.
*  파생된 클래스의 직접 기본 클래스를 확장합니다. 파생된 클래스를 상속하는 대상에 새 멤버를 추가할 수 있지만 상속된 멤버의 정의를 제거할 수 없습니다.
*  인스턴스 생성자, 소멸자 및 정적 생성자는 상속 되지 않지만 해당 선언 된 접근성에 관계 없이 다른 모든 멤버는 ([멤버 액세스](basic-concepts.md#member-access)). 그러나 해당 선언 된 액세스 가능성에 따라 상속 된 멤버 수 없습니다 파생된 클래스에서 액세스할 수 있습니다.
*  파생된 클래스 수 ***숨기기*** ([상속을 통해 숨기기](basic-concepts.md#hiding-through-inheritance)) 상속 된 멤버 이름 또는 시그니처가 같은 새로운 멤버를 선언 합니다. 그러나 상속된 된 멤버를 숨기는에서는 제거 되지 않습니다 해당 멤버 —는 해당 멤버는 파생된 클래스를 통해 직접 액세스할 수 없습니다.
*  클래스의 인스턴스 클래스 및 해당 기본 클래스와 암시적 변환에 선언 된 모든 인스턴스 필드의 집합을 포함 ([암시적 참조 변환](conversions.md#implicit-reference-conversions)) 해당 기본 클래스 형식에서 파생 된 클래스 형식 존재 합니다. 따라서 해당 기본 클래스의 인스턴스에 대 한 참조로 몇 가지 파생된 클래스의 인스턴스에 대 한 참조를 처리할 수 있습니다.
*  클래스는 가상 메서드, 속성 및 인덱서를 선언할 수 있습니다 및 파생된 클래스에는 이러한 함수 멤버의 구현을 재정의할 수 있습니다. 따라서 클래스를에서 함수 멤버 호출을 수행한 작업을 해당 하는 함수 멤버 호출에 사용 되는 인스턴스의 런타임 형식에 따라 여기서 원하는 다형성 동작을 나타낼 수 있습니다.

생성 된 클래스 형식의 상속 된 멤버는 직접 기본 클래스 형식의 멤버 ([기본 클래스](classes.md#base-classes)), 각 해당 형식에 대해 생성 된 형식의 형식 인수를 대체 하 여 찾을 수 있는 매개 변수를 *class_base* 사양입니다. 따라서 이러한 멤버 각각에 대 한 대체 하 여 변환 됩니다 *type_parameter* 해당 멤버 선언에서 *type_argument* 의 합니다 *class_base* 사양입니다.

```csharp
class B<U>
{
    public U F(long index) {...}
}

class D<T>: B<T[]>
{
    public T G(string s) {...}
}
```

위의 예에서 생성 된 형식 `D<int>` 상속 되지 않는 멤버가 `public int G(string s)` 형식 인수를 대체 하 여 얻은 `int` 형식 매개 변수에 대해 `T`합니다. `D<int>` 상속된 된 멤버를 클래스 선언에서 역시 `B`합니다. 이 상속 된 멤버는 기본 클래스 형식을 확인 하 여 결정 됩니다 `B<int[]>` 의 `D<int>` 대체 하 여 `int` 에 대 한 `T` 기본 클래스 사양에 `B<T[]>`입니다. 그런 다음에 형식 인수로 `B`, `int[]` 대체 하는 `U` 에서 `public U F(long index)`, 상속 된 멤버를 생성 `public int[] F(long index)`합니다.

### <a name="the-new-modifier"></a>New 한정자

A *class_member_declaration* 는를 사용 하 여 이름 또는 시그니처가 같은 상속된 된 멤버와 멤버를 선언할 수 있습니다. 이 경우 파생된 클래스 멤버를 라고 ***숨기기*** 기본 클래스 멤버입니다. 상속된 된 멤버 숨기기는 오류로 간주 하지는 않지만 컴파일러 경고가 발생 하도록 합니다. 경고를 표시 하지 않으려면 파생된 클래스 멤버의 선언을 포함할 수는 `new` 한정자는 파생된 멤버가 기본 멤버를 숨기려면 것을 나타냅니다. 이 항목 설명에 대 한 자세한 [상속을 통해 숨기기](basic-concepts.md#hiding-through-inheritance)합니다.

경우는 `new` 한정자는 상속 된 멤버를 숨기지 않는 선언에 포함 되어, 그 결과 경고가 발생 합니다. 이 경고를 제거 하 여 표시 되지 않는지를 `new` 한정자입니다.

### <a name="access-modifiers"></a>액세스 한정자

A *class_member_declaration* 5 등의 사용 가능한 선언 된 액세스 가능성 중 하나를 가질 수 있습니다 ([접근성을 선언](basic-concepts.md#declared-accessibility)): `public`를 `protected internal`를 `protected`, `internal` 또는 `private`합니다. 제외 하 고는 `protected internal` 둘 이상의 액세스 한정자를 지정 하는 컴파일 시간 오류는 조합 합니다. 경우는 *class_member_declaration* 액세스 한정자를 다루지 않습니다 `private` 것으로 간주 됩니다.

### <a name="constituent-types"></a>구성 요소 형식

멤버의 선언에 사용 되는 형식에는 해당 멤버의 구성 요소 형식 이라고 합니다. 가능한 구성 요소 유형은 상수, 필드, 속성, 이벤트 또는 인덱서의 유형, 메서드 또는 연산자의 반환 형식 및 메서드, 인덱서, 연산자 또는 인스턴스 생성자의 매개 변수 형식입니다. 구성 유형의 멤버를 해당 멤버 자체 만큼 액세스 가능 이상 이어야 합니다 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).

### <a name="static-and-instance-members"></a>정적 및 인스턴스 멤버

클래스의 멤버는 ***정적 멤버*** 하거나 ***인스턴스 멤버***합니다. 일반적으로 정적 멤버는 클래스 형식 및 개체 (클래스 형식의 인스턴스)에 속하는 것으로 인스턴스 멤버에 속한 것으로 생각 하는 것이 유용 합니다.

필드, 메서드, 속성, 이벤트, 연산자 또는 생성자 선언을 포함 하는 경우는 `static` 한정자, 정적 멤버를 선언 합니다. 또한 상수 또는 형식 선언은 암시적으로 정적 멤버를 선언합니다. 정적 멤버에는 다음과 같은 특징이 있습니다.

*  정적 멤버가 `M` 에서 참조 되는 *member_access* ([멤버 액세스](expressions.md#member-access)) 폼의 `E.M`, `E` 포함 하는 형식 표시 해야 합니다 `M`합니다. 에 대 한 컴파일 시간 오류 `E` 인스턴스를 나타냅니다.
*  정적 필드는 닫힌된 주어진된 클래스 형식의 모든 인스턴스에서 공유 하도록 정확히 하나의 저장 위치를 식별 합니다. 지정 된 닫힌된 클래스 유형 인스턴스 개수를 생성 없이 정적 필드의 사본 하나만 있습니다.
*  정적 함수 멤버 (메서드, 속성, 이벤트, 연산자 또는 생성자)는 특정 인스턴스에 작동 하지 않고 이며 컴파일 타임 오류를 가리키는 데 `this` 함수 멤버에서입니다.

필드, 메서드, 속성, 이벤트, 인덱서, 생성자 또는 소멸자가 선언 포함 되지 않습니다는 `static` 한정자를 인스턴스 멤버를 선언 합니다. (인스턴스 멤버는 비정적 멤버 라고도 함은.) 인스턴스 멤버에는 다음과 같은 특징이 있습니다.

*  때 인스턴스 멤버 `M` 에서 참조 되는 *member_access* ([멤버 액세스](expressions.md#member-access)) 양식의 `E.M`, `E` 를포함하는형식의인스턴스를표시해야합니다`M`. 에 대 한 바인딩 시간 오류 `E` 를 나타내는 형식입니다.
*  클래스의 모든 인스턴스 클래스의 모든 인스턴스 필드의 별도 집합을 포함합니다.
*  클래스의 인스턴스에 인스턴스 함수 멤버 (메서드, 속성, 인덱서, 인스턴스 생성자 또는 소멸자) 작동 하 고이 인스턴스를 액세스할 수 있습니다 `this` ([이 액세스](expressions.md#this-access)).

다음 예제에서는 정적 액세스 규칙 및 인스턴스 멤버를 보여 줍니다.
```csharp
class Test
{
    int x;
    static int y;

    void F() {
        x = 1;            // Ok, same as this.x = 1
        y = 1;            // Ok, same as Test.y = 1
    }

    static void G() {
        x = 1;            // Error, cannot access this.x
        y = 1;            // Ok, same as Test.y = 1
    }

    static void Main() {
        Test t = new Test();
        t.x = 1;          // Ok
        t.y = 1;          // Error, cannot access static member through instance
        Test.x = 1;       // Error, cannot access instance member through type
        Test.y = 1;       // Ok
    }
}
```

합니다 `F` 메서드는 인스턴스 함수 멤버를 보여 줍니다는 *simple_name* ([단순 이름](expressions.md#simple-names)) 인스턴스 멤버 및 정적 멤버에 액세스할 수 있습니다. 합니다 `G` 메서드를 보여 줍니다는 정적 함수 멤버인에서는 컴파일 타임 오류를 통해 인스턴스 멤버에 액세스 하는 *simple_name*합니다. `Main` 메서드를 보여 줍니다에 *member_access* ([멤버 액세스](expressions.md#member-access)) 인스턴스를 인스턴스 멤버에 액세스 해야 하 고 형식을 통해 정적 멤버에 액세스 해야 합니다.

### <a name="nested-types"></a>중첩 형식

클래스 또는 구조체 선언 내에서 선언 된 형식 호출 되는 ***중첩 형식이***합니다. 컴파일 단위 또는 네임 스페이스 내에서 선언 된 형식 호출 되는 ***중첩 되지 않은 형식***합니다.

예제
```csharp
using System;

class A
{
    class B
    {
        static void F() {
            Console.WriteLine("A.B.F");
        }
    }
}
```
클래스 `B` 중첩된 형식 이므로 클래스 내에 선언 `A`, 및 클래스 `A` 중첩 되지 않은 형식 이므로 컴파일 단위 내에 선언 합니다.

#### <a name="fully-qualified-name"></a>정규화 된 이름

정규화 된 이름 ([정규화 된 이름](basic-concepts.md#fully-qualified-names)) 중첩 된 형식에 대 한 `S.N` 여기서 `S` 유형 형식의 정규화 된 이름인 `N` 선언 됩니다.

#### <a name="declared-accessibility"></a>선언된 액세스 가능성

비 중첩 형식도 가질 수 있습니다 `public` 하거나 `internal` 접근성을 선언 하 고 있는 `internal` 내게 필요한 옵션은 기본적으로 선언 합니다. 중첩된 형식은 클래스 또는 구조체를 포함 하는 형식 인지에 따라 선언 된 내게 필요한 옵션의 하나 이상의 추가 형식 및 이러한 형태의 선언 된 접근성을도 포함할 수 있습니다.

*  클래스에서 선언 된 중첩된 형식이 선언 된 액세스 가능성의 5 가지 중 하나일 수 있습니다 (`public`, `protected internal`를 `protected`를 `internal`, 또는 `private`) 및 다른 클래스 멤버와 마찬가지로 기본값 `private` 선언 내게 필요한 옵션입니다.
*  구조체에 선언 된 중첩된 형식이 선언 된 액세스 가능성의 세 가지 형식 중 하나일 수 있습니다 (`public`, `internal`, 또는 `private`) 및 다른 구조체 멤버와 마찬가지로 기본값 `private` 접근성을 선언 합니다.

이 예제에서
```csharp
public class List
{
    // Private data structure
    private class Node
    { 
        public object Data;
        public Node Next;

        public Node(object data, Node next) {
            this.Data = data;
            this.Next = next;
        }
    }

    private Node first = null;
    private Node last = null;

    // Public interface
    public void AddToFront(object o) {...}
    public void AddToBack(object o) {...}
    public object RemoveFromFront() {...}
    public object RemoveFromBack() {...}
    public int Count { get {...} }
}
```
전용 중첩된 클래스 선언 `Node`합니다.

#### <a name="hiding"></a>숨기기

중첩된 형식은 숨길 수 있습니다 ([이름 숨기기](basic-concepts.md#name-hiding)) 기본 멤버입니다. `new` 숨기기를 명시적으로 표현 될 수 있도록 중첩된 형식 선언에서 한정자가 허용 됩니다. 이 예제에서
```csharp
using System;

class Base
{
    public static void M() {
        Console.WriteLine("Base.M");
    }
}

class Derived: Base 
{
    new public class M 
    {
        public static void F() {
            Console.WriteLine("Derived.M.F");
        }
    }
}

class Test 
{
    static void Main() {
        Derived.M.F();
    }
}
```
중첩된 클래스를 보여 줍니다 `M` 하는 메서드를 숨깁니다 `M` 에 정의 된 `Base`합니다.

#### <a name="this-access"></a>이 액세스

중첩된 형식 및 포함 하는 형식 관련해 서는 특수 한 관계가 없는 *this_access* ([이 액세스](expressions.md#this-access)). 특히 `this` 중첩된 형식 내에서 포함 하는 형식의 인스턴스 멤버 참조를 사용할 수 없습니다. 중첩된 된 형식을 포함 하는 형식의 인스턴스 멤버에 대 한 액세스 해야 하는 경우에 대 한 액세스를 제공 하 여 제공할 수 있습니다는 `this` 중첩 된 형식에 대 한 생성자 인수로 포함 하는 형식 인스턴스에 대 한 합니다. 다음 예제에서
```csharp
using System;

class C
{
    int i = 123;

    public void F() {
        Nested n = new Nested(this);
        n.G();
    }

    public class Nested
    {
        C this_c;

        public Nested(C c) {
            this_c = c;
        }

        public void G() {
            Console.WriteLine(this_c.i);
        }
    }
}

class Test
{
    static void Main() {
        C c = new C();
        c.F();
    }
}
```
이 기술을 보여 줍니다. 인스턴스의 `C` 의 인스턴스를 만듭니다 `Nested` 자체 전달 `this` 하 `Nested`의 생성자에 대 한 후속 액세스를 제공 하기 위해 `C`의 인스턴스 멤버입니다.

#### <a name="access-to-private-and-protected-members-of-the-containing-type"></a>포함 하는 형식의 private 및 protected 멤버에 대 한 액세스

중첩 된 형식에 있는 포함 하는 형식의 멤버를 포함 하 여 포함 하는 형식에 액세스할 수 있는 멤버의 모든 권한을 `private` 및 `protected` 접근성을 선언 합니다. 이 예제에서
```csharp
using System;

class C 
{
    private static void F() {
        Console.WriteLine("C.F");
    }

    public class Nested 
    {
        public static void G() {
            F();
        }
    }
}

class Test 
{
    static void Main() {
        C.Nested.G();
    }
}
```
클래스를 보여 줍니다 `C` 중첩된 된 클래스를 포함 하는 `Nested`합니다. 내 `Nested`, 메서드 `G` 정적 메서드를 호출 `F` 에 정의 된 `C`, 및 `F` private 선언에 내게 필요한 옵션입니다.

또한 중첩된 된 형식을 포함 하는 형식의 기본 형식에 정의 된 보호 된 멤버 액세스할 수 있습니다. 예제
```csharp
using System;

class Base 
{
    protected void F() {
        Console.WriteLine("Base.F");
    }
}

class Derived: Base 
{
    public class Nested 
    {
        public void G() {
            Derived d = new Derived();
            d.F();        // ok
        }
    }
}

class Test 
{
    static void Main() {
        Derived.Nested n = new Derived.Nested();
        n.G();
    }
}
```
중첩된 클래스 `Derived.Nested` 보호 된 메서드에 액세스 `F` 에 정의 된 `Derived`의 기본 클래스 `Base`의 인스턴스를 통해 호출 `Derived`합니다.

#### <a name="nested-types-in-generic-classes"></a>제네릭 클래스의 중첩된 형식

제네릭 클래스 선언에는 중첩된 형식 선언을 포함할 수 있습니다. 형식 매개 변수는 바깥쪽 클래스의 중첩된 형식 내에서 사용할 수 있습니다. 중첩된 형식 선언 중첩 된 형식에만 적용 되는 추가 형식 매개 변수를 포함할 수 있습니다.

제네릭 클래스 선언 내에 포함 된 모든 형식 선언은 암시적으로 제네릭 형식 선언이입니다. 제네릭 형식 안에 중첩 형식에 대 한 참조를 작성 하는 경우에 해당 형식 인수를 포함 하 여 포함 하는 생성 된 형식에 이름을 지정 해야 합니다. 그러나에서 외부 클래스 내에서 중첩된 된 형식을 사용할 수 있습니다; 한정자 없이 중첩 된 형식을 생성 하는 경우 외부 클래스의 인스턴스 유형은 암시적으로 사용할 수 있습니다. 다음 예제에서는에서 만든 생성된 된 형식을 참조 하 세 가지 올바른 `Inner`; 처음 두 동일 합니다.
```csharp
class Outer<T>
{
    class Inner<U>
    {
        public static void F(T t, U u) {...}
    }

    static void F(T t) {
        Outer<T>.Inner<string>.F(t, "abc");      // These two statements have
        Inner<string>.F(t, "abc");               // the same effect

        Outer<int>.Inner<string>.F(3, "abc");    // This type is different

        Outer.Inner<string>.F(t, "abc");         // Error, Outer needs type arg
    }
}
```

잘못 된 이지만 프로그래밍 스타일을 중첩된 된 형식에 형식 매개 변수 멤버 하거나 숨기려면 형식 매개 변수가 외부 형식에서 선언:
```csharp
class Outer<T>
{
    class Inner<T>        // Valid, hides Outer's T
    {
        public T t;       // Refers to Inner's T
    }
}
```

### <a name="reserved-member-names"></a>예약 된 멤버 이름

기본 C# 런타임 구현 속성, 이벤트 또는 인덱서는 각 원본 멤버 선언에 대 한를 용이 하 게 구현 멤버 선언, 해당 이름 및 형식과의 종류에 따라 두 가지 메서드 시그니처를 예약 해야 합니다. 기본 런타임 구현을 구성 하지 않는 경우에 멤버 중 일치 하는 시그니처를 가진 예약 서명을 선언 하는 프로그램에 대 한 컴파일 시간 오류 이러한 예약 사용 합니다.

예약된 된 이름 선언에 가져오지 마세요, 따라서 이러한에 참여 하지 않는 멤버 조회 합니다. 그러나 선언 관련 서명을 수행 상속에 참여 하는 예약 된 메서드 ([상속](classes.md#inheritance))를 사용 하 여 숨길 수는 `new` 한정자 ([new 한정자](classes.md#the-new-modifier)).

이러한 이름은 예약은 세 가지 용도로 사용 됩니다.

*  Get 메서드 이름으로 일반 식별자를 사용 하거나 C# 언어 기능에 대 한 액세스를 설정 하는 기본 구현을 허용 합니다.
*  Get 메서드 이름으로 일반 식별자를 사용 하 여 상호 운용 또는 C# 언어 기능에 대 한 액세스를 설정 하려면 다른 언어를 허용 합니다.
*  소스는 하나의 준수 컴파일러에서 허용 되는지 확인 하려면 수락한 경우 다른 만들어 예약 된 멤버의 특성 이름을 일관 된 모든 C# 구현에서.

소멸자의 선언 ([소멸자](classes.md#destructors))도 사용 될 서명 하면 ([소멸자에 대 한 예약 된 멤버 이름](classes.md#member-names-reserved-for-destructors)).

#### <a name="member-names-reserved-for-properties"></a>속성에 대 한 예약 된 멤버 이름

속성에 대 한 `P` ([속성](classes.md#properties)) 형식의 `T`, 다음 시그니처만 예약 됩니다.

```csharp
T get_P();
void set_P(T value);
```

속성은 읽기 전용 또는 쓰기 전용일 경우에 서명은 모두 예약 됩니다.

예제
```csharp
using System;

class A
{
    public int P {
        get { return 123; }
    }
}

class B: A
{
    new public int get_P() {
        return 456;
    }

    new public void set_P(int value) {
    }
}

class Test
{
    static void Main() {
        B b = new B();
        A a = b;
        Console.WriteLine(a.P);
        Console.WriteLine(b.P);
        Console.WriteLine(b.get_P());
    }
}
```
클래스 `A` 읽기 전용 속성을 정의 `P`에 대해 시그니처가 `get_P` 및 `set_P` 메서드. 클래스 `B` 에서 파생 `A` 하 고 이러한 예약 된 서명을 모두 숨깁니다. 이 예제에서는 출력을 생성합니다.
```
123
123
456
```

#### <a name="member-names-reserved-for-events"></a>이벤트에 대 한 예약 된 멤버 이름

이벤트에 대 한 `E` ([이벤트](classes.md#events)) 대리자 형식 `T`, 다음 시그니처만 예약 됩니다.
```csharp
void add_E(T handler);
void remove_E(T handler);
```

#### <a name="member-names-reserved-for-indexers"></a>인덱서에 대 한 예약 된 멤버 이름

인덱서 ([인덱서](classes.md#indexers)) 형식의 `T` 매개 변수 목록을 사용 하 여 `L`, 다음 시그니처만 예약 됩니다.
```csharp
T get_Item(L);
void set_Item(L, T value);
```

인덱서는 읽기 전용 또는 쓰기 전용일 경우에 서명은 모두 예약 됩니다.

또한 멤버 이름을 `Item` 예약 되어 있습니다.

#### <a name="member-names-reserved-for-destructors"></a>소멸자에 대 한 예약 된 멤버 이름

소멸자를 포함 하는 클래스에 대 한 ([소멸자](classes.md#destructors)), 다음과 같은 시그니처가 예약 됩니다.
```csharp
void Finalize();
```

## <a name="constants"></a>상수

A ***상수*** 는 상수 값을 표현 하는 클래스 멤버: 컴파일 타임에 계산할 수 있는 값입니다. A *constant_declaration* 지정 된 형식의 하나 이상의 상수를 소개 합니다.

```antlr
constant_declaration
    : attributes? constant_modifier* 'const' type constant_declarators ';'
    ;

constant_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    ;

constant_declarators
    : constant_declarator (',' constant_declarator)*
    ;

constant_declarator
    : identifier '=' constant_expression
    ;
```

A *constant_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)), `new` 한정자 ([new 한정자](classes.md#the-new-modifier)), 유효한 조합 된 네 가지 액세스 한정자 ([액세스 한정자](classes.md#access-modifiers)). 에 의해 선언 된 멤버의 모든 적용 된 특성 및 한정자를 *constant_declaration*합니다. 상수 정적 멤버 라고 하는 경우에을 *constant_declaration* 필요 하거나 허용 하지는 `static` 한정자입니다. 상수 선언에 여러 번 표시 하는 동일한 한정자에 대 한 오류는 것입니다.

*형식* 의 한 *constant_declaration* 선언에 의해 정의 된 멤버의 형식을 지정 합니다. 형식 목록이 나옵니다 *constant_declarator*s, 각각 새 멤버를 소개 합니다. *constant_declarator* 이루어져는 *식별자* 뒤에 멤버 이름을 나타내는 "`=`" 토큰, 뒤에 *constant_expression* ([ 상수 식](expressions.md#constant-expressions)) 해당 멤버의 값을 제공 합니다.

*형식* 상수에 지정 된 선언 해야 `sbyte`, `byte`, `short`를 `ushort`, `int`, `uint`, `long`를 `ulong`, `char`, `float`, `double`, `decimal`, `bool`합니다 `string`, *enum_type*, 또는 *reference_type*합니다. 각 *constant_expression* 대상 형식 또는 암시적으로 변환 하 여 대상 형식으로 변환할 수 있는 형식의 값을 생성 해야 합니다 ([암시적 변환을](conversions.md#implicit-conversions)).

합니다 *형식* 상수의 해야 적어도 상수 자체 수준 만큼 액세스 가능 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).

상수 값을 사용 하는 식에서 가져올은 *simple_name* ([단순 이름](expressions.md#simple-names)) 또는 *member_access* ([멤버 액세스](expressions.md#member-access)).

상수 자체에 참여할 수는 *constant_expression*합니다. 따라서 필요한 모든 구문에는 상수를 사용할 수 있습니다는 *constant_expression*합니다. 이러한 구문의 예로 `case` 레이블을 `goto case` 문을 `enum` 멤버 선언, 특성 및 기타 상수 선언 합니다.

에 설명 된 대로 [상수 식](expressions.md#constant-expressions), *constant_expression* 컴파일 시간에 완전히 계산 될 수 있는 식입니다. null이 아닌 값을 만들 수 있는 유일한 방법은 *reference_type* 이외의 `string` 적용 하는 것을 `new` 연산자 및 이후를 `new` 연산자를 사용할 수 없습니다는 *constant_ 식을*의 상수에 대 한 가능한 유일한 값 *reference_type*s 이외의 `string` 는 `null`합니다.

상수 값에 대 한 기호화 된 이름, 필요한 경우 하지만 때 해당 값의 형식은 상수 선언에서 허용 되지 않습니다 또는 의해 컴파일 시간에 값을 계산할 수 없는 경우는 *constant_expression*, `readonly` (필드 [읽기 전용 필드](classes.md#readonly-fields)) 대신 사용할 수 있습니다.

여러 상수를 선언 하는 상수 선언 동일한 특성, 한정자 및 형식을 사용 하 여 단일 상수 여러 번 선언 하는 것과 같습니다. 예
```csharp
class A
{
    public const double X = 1.0, Y = 2.0, Z = 3.0;
}
```
위의 식은 아래의 식과 동일합니다.
```csharp
class A
{
    public const double X = 1.0;
    public const double Y = 2.0;
    public const double Z = 3.0;
}
```

상수는 순환적 종속성 없는으로 동일한 프로그램 안에 다른 상수에 따라 달라 지도록 허용 됩니다. 컴파일러는 자동으로 적절 한 순서로 상수 선언 평가를 정렬 합니다. 예제
```csharp
class A
{
    public const int X = B.Z + 1;
    public const int Y = 10;
}

class B
{
    public const int Z = A.Y + 1;
}
```
컴파일러는 먼저 계산 `A.Y`, 그런 다음 계산 `B.Z`, 마지막으로 평가 하 고 `A.X`, 값을 생성 `10`, `11`, 및 `12`. 상수 선언 다른 프로그램에서 상수에 따라 달라질 수 있습니다 되지만 이러한 종속성 단방향에서 수만 있습니다. 경우 위 예제를 참조 `A` 및 `B` 선언 된 별도 프로그램의 수에 대 한 `A.X` 에 따라 달라 지도록 `B.Z`, 하지만 `B.Z` 동시에 종속 다음 수 `A.Y`.

## <a name="fields"></a>필드

A ***필드*** 개체 또는 클래스와 연결 된 변수를 나타내는 멤버가 있습니다. A *field_declaration* 지정 된 형식의 하나 이상의 필드를 소개 합니다.

```antlr
field_declaration
    : attributes? field_modifier* type variable_declarators ';'
    ;

field_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'static'
    | 'readonly'
    | 'volatile'
    | field_modifier_unsafe
    ;

variable_declarators
    : variable_declarator (',' variable_declarator)*
    ;

variable_declarator
    : identifier ('=' variable_initializer)?
    ;

variable_initializer
    : expression
    | array_initializer
    ;
```

A *field_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)), `new` 한정자 ([new 한정자](classes.md#the-new-modifier)), 유효한 조합 된 네 가지 액세스 한정자 ([액세스 한정자](classes.md#access-modifiers)), 및 `static` 한정자 ([정적 및 인스턴스 필드](classes.md#static-and-instance-fields)). 또한를 *field_declaration* 포함 될 수 있습니다는 `readonly` 한정자 ([읽기 전용 필드](classes.md#readonly-fields)) 또는 `volatile` 한정자 ([Volatile 필드](classes.md#volatile-fields)) 하나만 있습니다. 에 의해 선언 된 멤버의 모든 적용 된 특성 및 한정자를 *field_declaration*합니다. 해당 필드 선언에 여러 번 표시 하는 동일한 한정자에 대 한 오류입니다.

*형식* 의 한 *field_declaration* 선언에 의해 정의 된 멤버의 형식을 지정 합니다. 형식 목록이 나옵니다 *variable_declarator*s, 각각 새 멤버를 소개 합니다. *variable_declarator* 이루어져 있습니다를 *식별자* 뒤에 선택적으로 해당 멤버에 이름을 지정 하는 "`=`" 토큰으로 *variable_initializer* ([ 변수 이니셜라이저](classes.md#variable-initializers)) 해당 멤버의 초기 값을 제공 합니다.

합니다 *형식* 필드의 해야 적어도 필드 자체 만큼 액세스 가능 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).

사용 하는 식에서 가져올 필드의 값을 *simple_name* ([단순 이름](expressions.md#simple-names)) 또는 *member_access* ([멤버 액세스](expressions.md#member-access)). 사용 하 여 읽기 전용이 아닌 필드의 값은 수정 된 *할당* ([대입 연산자](expressions.md#assignment-operators)). 읽기 전용이 아닌 필드의 값은 후 위 증가 및 감소 연산자를 모두 가져와 사용 하 여 수정할 수 있습니다 ([후 위 증가 및 감소 연산자](expressions.md#postfix-increment-and-decrement-operators)) 전위 증가 및 감소 연산자 ([접두사 증가 및 감소 연산자](expressions.md#prefix-increment-and-decrement-operators)).

여러 필드를 선언 하는 필드 선언은 동일한 특성, 한정자 및 형식을 사용 하 여 단일 필드의 여러 선언 하는 것과 같습니다. 예
```csharp
class A
{
    public static int X = 1, Y, Z = 100;
}
```
위의 식은 아래의 식과 동일합니다.
```csharp
class A
{
    public static int X = 1;
    public static int Y;
    public static int Z = 100;
}
```

### <a name="static-and-instance-fields"></a>정적 및 인스턴스 필드

필드 선언 포함 되는 경우는 `static` 한정자를 선언에 의해 도입 된 필드는 ***정적 필드***합니다. 없는 경우 `static` 한정자가 있는 선언에 의해 도입 된 필드는 ***인스턴스 필드***합니다. 정적 필드 및 인스턴스 필드는 두 일부의 변수 ([변수](variables.md)) C#에서 지원 되며 때때로 이러한 라고 ***정적 변수*** 및 ***인스턴스 변수*** , 각각.

정적 필드는 특정 인스턴스에;의 일부가 아닙니다. 닫힌 형식의 모든 인스턴스 간에 공유 되는 대신 ([열기 및 닫힌 형식을](types.md#open-and-closed-types)). 닫힌된 클래스 유형 인스턴스 개수를 생성 없이 연결 된 응용 프로그램 도메인에 대 한 정적 필드의 사본 하나만 있습니다.

예를 들어:
```csharp
class C<V>
{
    static int count = 0;

    public C() {
        count++;
    }

    public static int Count {
        get { return count; }
    }
}

class Application
{
    static void Main() {
        C<int> x1 = new C<int>();
        Console.WriteLine(C<int>.Count);        // Prints 1

        C<double> x2 = new C<double>();
        Console.WriteLine(C<int>.Count);        // Prints 1

        C<int> x3 = new C<int>();
        Console.WriteLine(C<int>.Count);        // Prints 2
    }
}
```

인스턴스 필드 인스턴스에 속합니다. 특히 클래스의 모든 인스턴스는 해당 클래스의 모든 인스턴스 필드는 별도 집합을 포함합니다.

필드에서 참조 하는 경우는 *member_access* ([멤버 액세스](expressions.md#member-access)) 형식의 `E.M`이면 `M` 은 정적 필드 `E` 포함 하는 형식 표시 해야 합니다 `M` 경우에 `M` 인스턴스 필드, E를 포함 하는 형식 인스턴스의 나타내야 `M`합니다.

정적 간의 차이점 및 인스턴스 멤버 설명에 대 한 자세한 [정적 및 인스턴스 멤버](classes.md#static-and-instance-members)합니다.

### <a name="readonly-fields"></a>읽기 전용 필드

경우는 *field_declaration* 포함을 `readonly` 한정자를 선언에 의해 도입 된 필드는 ***읽기 전용 필드***합니다. 읽기 전용 필드에 직접 할당의 일부로 해당 선언 또는 인스턴스 생성자 또는 동일한 클래스의 정적 생성자 에서만 발생할 수 있습니다. (읽기 전용 필드는 할당할 수 있습니다를 여러 번 이러한 컨텍스트에서.) 특히, 직접 할당 하는 `readonly` 필드는 다음 경우에 허용 됩니다.

*  에 *variable_declarator* 필드를 도입 하는 (포함 하 여를 *variable_initializer* 선언에서).
*  필드 선언;를 포함 하는 클래스의 인스턴스 생성자에는 인스턴스 필드 에 대 한 필드 선언을 포함 하는 클래스의 정적 생성자에서 정적 필드입니다. 이러한 경우는 전달할 수만 컨텍스트를 `readonly` 필드를 `out` 또는 `ref` 매개 변수입니다.

에 할당 하는 `readonly` 필드 또는 변수로 전달를 `out` 또는 `ref` 다른 컨텍스트에서 매개 변수는 컴파일 시간 오류입니다.

#### <a name="using-static-readonly-fields-for-constants"></a>상수에 대 한 정적 읽기 전용 필드를 사용 하 여

`static readonly` 경우 상수 값에 대 한 기호화 된 이름이 필요 하지만 값의 형식에서 허용 되지 않습니다 때 필드 유용 합니다.는 `const` 선언 또는 경우 컴파일 타임에 값을 계산할 수 없습니다. 예제
```csharp
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);

    private byte red, green, blue;

    public Color(byte r, byte g, byte b) {
        red = r;
        green = g;
        blue = b;
    }
}
```
`Black`, `White`, `Red`, `Green`, 및 `Blue` 으로 멤버를 선언할 수 없습니다 `const` 멤버 하므로 컴파일 타임에 해당 값을 계산할 수 없습니다. 그러나 선언 `static readonly` 대신 훨씬 같은 효과가 있습니다.

#### <a name="versioning-of-constants-and-static-readonly-fields"></a>상수 및 정적 읽기 전용 필드의 버전 관리

상수 및 읽기 전용 필드 의미 체계가 서로 다른 이진 버전을 지정 합니다. 컴파일 타임에 상수 값을 가져오는 식에서 상수를 참조할 때 있지만 필드의 값 식에서 읽기 전용 필드를 참조 하는 경우 실행 시간까지 가져오지 않습니다. 별개의 두 프로그램으로 구성 된 응용 프로그램을 고려 합니다.
```csharp
using System;

namespace Program1
{
    public class Utils
    {
        public static readonly int X = 1;
    }
}

namespace Program2
{
    class Test
    {
        static void Main() {
            Console.WriteLine(Program1.Utils.X);
        }
    }
}
```

합니다 `Program1` 고 `Program2` 네임 스페이스 별도로 컴파일된 두 프로그램을 나타냅니다. 때문에 `Program1.Utils.X` 정적 읽기 전용 필드에서 출력 값으로 선언 되는 `Console.WriteLine` 문은 컴파일 타임에 알려지지 않은 하지만 런타임 시 가져온 대신 합니다. 따라서 경우 값 `X` 변경 및 `Program1` 를 다시 컴파일하면를 `Console.WriteLine` 문의 경우 새 값에도 출력 `Program2` 다시 컴파일할 되지 않습니다. 그러나 때로는 `X` 된 상수, 값 `X` 얻은 시 `Program2` 컴파일된, 및 변경의 영향을 받지 않은 상태로 유지 됩니다 `Program1` 될 때까지 `Program2` 다시 컴파일됩니다.

### <a name="volatile-fields"></a>Volatile 필드

경우는 *field_declaration* 포함을 `volatile` 한정자는 선언에서 정의한 필드는 ***volatile 필드***합니다.

비 volatile 필드에 대 한 명령을 다시 정렬할 수 있는 최적화 방법에서 제공 하는 동기화 되지 않은 필드에 액세스 하는 다중 스레드 프로그램에서 예기치 않은 및 예기치 않은 결과가 발생할 수 있습니다는 *lock_statement*  ([Lock 문에](statements.md#the-lock-statement)). 컴파일러, 런타임 시스템 또는 하드웨어에서 이러한 최적화를 수행할 수 있습니다. Volatile 필드에 대 한 이러한 다시 정렬 하는 최적화 제한 됩니다.

*  Volatile 필드의 읽기 호출 되는 ***volatile 읽기***합니다. Volatile 읽기는 "acquire 의미 체계"; 즉, 반드시 후 명령 시퀀스에서 발생 하는 메모리에 대 한 참조 하기 전에 발생 합니다.
*  Volatile 필드 쓰기 호출 되는 ***volatile 쓰기***합니다. Volatile 쓰기에 "release 의미 체계"; 즉, 반드시는 메모리 참조는 명령 시퀀스의 쓰기 명령 전에 발생 합니다.

이러한 제한 사항은 모든 스레드가 수행된 순서대로 다른 스레드가 휘발성 쓰기를 수행하게 합니다. 표준에 맞는 구현은 단일 총의 순서를 실행 하는 모든 스레드 표시 된 volatile 쓰기 제공할 필요가 없습니다. Volatile 필드의 형식은 다음 중 하나 여야 합니다.

*  A *reference_type*합니다.
*  형식 `byte`, `sbyte`, `short`, `ushort`, `int`를 `uint`, `char`, `float`, `bool`를 `System.IntPtr`, 또는` System.UIntPtr`합니다.
*  *enum_type* 열거형의 기본 형식을 `byte`, `sbyte`를 `short`를 `ushort`, `int`, 또는 `uint`합니다.

이 예제에서
```csharp
using System;
using System.Threading;

class Test
{
    public static int result;   
    public static volatile bool finished;

    static void Thread2() {
        result = 143;    
        finished = true; 
    }

    static void Main() {
        finished = false;

        // Run Thread2() in a new thread
        new Thread(new ThreadStart(Thread2)).Start();

        // Wait for Thread2 to signal that it has a result by setting
        // finished to true.
        for (;;) {
            if (finished) {
                Console.WriteLine("result = {0}", result);
                return;
            }
        }
    }
}
```
다음 출력을 생성합니다.
```
result = 143
```

이 예제에서는 메서드 `Main` 메서드를 실행 하는 새 스레드 시작 `Thread2`합니다. 이 메서드는 호출 비 volatile 필드에 값을 저장 `result`를 저장 한 다음 `true` volatile 필드에 `finished`입니다. 필드에 대 한 주 스레드가 대기 `finished` 로 설정 해야 `true`, 다음 필드를 읽고 `result`합니다. 이후 `finished` 선언한 `volatile`, main 메서드가 값을 읽어야 합니다. `143` 필드에서 `result`합니다. 경우 필드 `finished` 가 선언 되지 `volatile`를 저장소에 대 한 허용 될 `result` 저장소 후 주 스레드를 표시 하도록 `finished`, 및 값을 읽을 수 주 스레드에 대 한 `0` 에서 필드 `result`합니다. 선언 `finished` 으로 `volatile` 필드는 이러한 불일치를 방지 합니다.

### <a name="field-initialization"></a>필드 초기화

초기 값 필드의 정적 필드 또는 인스턴스 필드의 경우 든은 기본값 ([기본값](variables.md#default-values)) 필드의 형식입니다. 이 기본 초기화 발생 하 고 따라서 필드는 "초기화 되지 않은" 되지 전에 필드의 값을 관찰 하는 것이 불가능 합니다. 이 예제에서
```csharp
using System;

class Test
{
    static bool b;
    int i;

    static void Main() {
        Test t = new Test();
        Console.WriteLine("b = {0}, i = {1}", b, t.i);
    }
}
```
는 출력을 생성합니다.
```
b = False, i = 0
```
때문에 `b` 고 `i` 는 모두 자동으로 기본값으로 초기화 합니다.

### <a name="variable-initializers"></a>변수 이니셜라이저

필드 선언이 포함 될 수 있습니다 *variable_initializer*s입니다. 정적 필드에 대 한 변수 이니셜라이저 클래스 초기화 하는 동안 실행 되는 대입문에 해당 합니다. 예를 들어 필드를 변수 이니셜라이저 해당 클래스의 인스턴스를 만들 때 실행 되는 대입문을 합니다.

이 예제에서
```csharp
using System;

class Test
{
    static double x = Math.Sqrt(2.0);
    int i = 100;
    string s = "Hello";

    static void Main() {
        Test a = new Test();
        Console.WriteLine("x = {0}, i = {1}, s = {2}", x, a.i, a.s);
    }
}
```
는 출력을 생성합니다.
```
x = 1.4142135623731, i = 100, s = Hello
```
때문에 할당할 `x` 발생 할당 및 정적 필드 이니셜라이저를 실행할 때 `i` 및 `s` 인스턴스 필드 이니셜라이저를 실행할 때 발생 합니다.

에 설명 된 기본 값 초기화 [필드 초기화](classes.md#field-initialization) 변수 이니셜라이저는 필드를 포함 하 고 모든 필드에 발생 합니다. 따라서 클래스 초기화 될 때 해당 클래스의 모든 정적 필드는 기본값으로, 먼저 초기화 하 고 후 정적 필드 이니셜라이저 텍스트 순서 대로 실행 됩니다. 마찬가지로 클래스의 인스턴스를 만들 때 먼저 해당 인스턴스에 있는 모든 인스턴스 필드가 해당 기본값으로 초기화 됩니다 및 인스턴스 필드 이니셜라이저 텍스트 순서 대로 실행 됩니다.

기본값 상태로 사용 되는 변수 이니셜라이저를 사용 하 여 정적 필드에 대 한 것 같습니다. 그러나이 스타일의 문제로 것이 좋습니다. 이 예제에서
```csharp
using System;

class Test
{
    static int a = b + 1;
    static int b = a + 1;

    static void Main() {
        Console.WriteLine("a = {0}, b = {1}", a, b);
    }
}
```
이러한 동작을 수행 합니다. 순환 정의도 불구 하 고는 되며 b는 프로그램은 잘못 되었습니다. 그 결과 출력
```
a = 1, b = 2
```
때문에 정적 필드를 `a` 하 고 `b` 으로 초기화 됩니다 `0` (의 기본값 `int`) 해당 이니셜라이저가 실행 되기 전에 합니다. 경우에 대 한 이니셜라이저 `a` 를 실행 하 고 값 `b` 가 0 이면 등 `a` 으로 초기화 됩니다 `1`합니다. 경우에 대 한 이니셜라이저 `b` 를 실행 하 고 값 `a` 이미 `1`, 등 `b` 초기화 됩니다 `2`합니다.

#### <a name="static-field-initialization"></a>정적 필드 초기화

클래스의 정적 필드 변수 이니셜라이저 할당의 클래스 선언에 나타나는 텍스트 순서 대로 실행 되는 시퀀스에 해당 합니다. 경우 정적 생성자 ([정적 생성자](classes.md#static-constructors))가 클래스의 정적 필드 이니셜라이저는 실행 정적 생성자를 실행 하기 전에 즉시 발생 합니다. 그렇지 않은 경우 정적 필드 이니셜라이저를 해당 클래스의 정적 필드의 첫 번째 사용 하기 전에 구현에 따라 다릅니다 시간에 실행 됩니다. 이 예제에서
```csharp
using System;

class Test 
{ 
    static void Main() {
        Console.WriteLine("{0} {1}", B.Y, A.X);
    }

    public static int F(string s) {
        Console.WriteLine(s);
        return 1;
    }
}

class A
{
    public static int X = Test.F("Init A");
}

class B
{
    public static int Y = Test.F("Init B");
}
```
두 출력을 생성할 수 있습니다.
```
Init A
Init B
1 1
```
또는 출력을 추가 합니다.
```
Init B
Init A
1 1
```
때문에 실행 `X`의 이니셜라이저 및 `Y`의 이니셜라이저는 어떤 순서로 든 발생할 수 있습니다; 그리고 해당 필드에 대 한 참조 앞에 오는 제한만 됩니다. 그러나 예제의:
```csharp
using System;

class Test
{
    static void Main() {
        Console.WriteLine("{0} {1}", B.Y, A.X);
    }

    public static int F(string s) {
        Console.WriteLine(s);
        return 1;
    }
}

class A
{
    static A() {}

    public static int X = Test.F("Init A");
}

class B
{
    static B() {}

    public static int Y = Test.F("Init B");
}
```
출력 해야 합니다.
```
Init B
Init A
1 1
```
때문에 정적 생성자가 실행 하는 시기에 대 한 규칙 (에 정의 된 대로 [정적 생성자](classes.md#static-constructors))를 제공 `B`의 정적 생성자 (및 따라서 `B`의 정적 필드 이니셜라이저) 보다먼저실행해야`A`의 정적 생성자 및 필드 이니셜라이저입니다.

#### <a name="instance-field-initialization"></a>인스턴스 필드 초기화

인스턴스 생성자 중 하나에 진입할 때 즉시 실행 되는 할당의 시퀀스에 해당 하는 클래스의 인스턴스 필드 변수 이니셜라이저 ([생성자 이니셜라이저](classes.md#constructor-initializers))는 클래스입니다. 변수 이니셜라이저는 클래스 선언에 나타나는 텍스트 순서 대로 실행 됩니다. 클래스 인스턴스 만들기 및 초기화 프로세스에서 자세히 설명 되어 [인스턴스 생성자](classes.md#instance-constructors)합니다.

인스턴스 필드에 대 한 변수 이니셜라이저에서 예외는 생성 되는 인스턴스를 참조할 수 없습니다. 컴파일 타임 오류를 참조 하는 것이 따라서 `this` 변수 이니셜라이저에서 예외를 그대로를 통해 인스턴스 멤버를 참조 변수 이니셜라이저에서 예외에 대 한 컴파일 시간 오류를 *simple_name*합니다. 예제
```csharp
class A
{
    int x = 1;
    int y = x + 1;        // Error, reference to instance member of this
}
```
에 대 한 변수 이니셜라이저 `y` 만들어지는 인스턴스 멤버를 참조 하기 때문에 컴파일 타임 오류가 발생 합니다.

## <a name="methods"></a>메서드

***메서드***는 개체 또는 클래스에서 수행할 수 있는 계산이나 작업을 구현하는 멤버입니다. 메서드를 사용 하 여 선언 *method_declaration*s:

```antlr
method_declaration
    : method_header method_body
    ;

method_header
    : attributes? method_modifier* 'partial'? return_type member_name type_parameter_list?
      '(' formal_parameter_list? ')' type_parameter_constraints_clause*
    ;

method_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'static'
    | 'virtual'
    | 'sealed'
    | 'override'
    | 'abstract'
    | 'extern'
    | 'async'
    | method_modifier_unsafe
    ;

return_type
    : type
    | 'void'
    ;

member_name
    : identifier
    | interface_type '.' identifier
    ;

method_body
    : block
    | '=>' expression ';'
    | ';'
    ;
```

A *method_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)) 및 네 가지 액세스 한정자의 유효한 조합이 ([액세스 한정자 ](classes.md#access-modifiers)), `new` ([새 한정자](classes.md#the-new-modifier)), `static` ([정적 메서드와 인스턴스](classes.md#static-and-instance-methods)), `virtual` ([가상메서드](classes.md#virtual-methods)), `override` ([메서드를 재정의](classes.md#override-methods)), `sealed` ([메서드를 봉인](classes.md#sealed-methods)), `abstract` ([추상 메서드](classes.md#abstract-methods)), 및 `extern` ([외부 메서드](classes.md#external-methods)) 한정자.

선언에는 다음과 같은 경우 한정자의 유효한 조합이 있습니다.

*  선언에 대 한 액세스 한정자의 유효한 조합이 포함 ([액세스 한정자](classes.md#access-modifiers)).
*  선언 한정자를 동일한 여러 번 포함 되지 않습니다.
*  다음 한정자 중 하나만 선언 포함: `static`, `virtual`, 및 `override`합니다.
*  선언에는 다음 한정자 중 하나만 포함 합니다. `new` 및 `override`합니다.
*  선언에 포함 하는 경우는 `abstract` 한정자를 다음 선언을 포함 하지 않습니다 다음 한정자 중: `static`를 `virtual`, `sealed` 또는 `extern`합니다.
*  선언에 포함 하는 경우는 `private` 한정자를 다음 선언을 포함 하지 않습니다 다음 한정자 중: `virtual`를 `override`, 또는 `abstract`합니다.
*  선언에 포함 하는 경우는 `sealed` 한정자를 선언도 포함 됩니다는 `override` 한정자입니다.
*  선언을 포함 하는 경우는 `partial` 한다면 한정자를 포함 하지 않습니다 다음 한정자 중: `new`, `public`, `protected`, `internal`를 `private`, `virtual`를 `sealed`, `override` 하십시오 `abstract`, 또는 `extern`합니다.

포함 된 메서드를 `async` 한정자는 비동기 함수 및에 설명 된 규칙을 따릅니다 [비동기 함수](classes.md#async-functions)합니다.

합니다 *return_type* 메서드의 선언은 계산 및 확장 메서드에서 반환한 값의 형식을 지정 합니다. 합니다 *return_type* 는 `void` 메서드 값을 반환 하지 않는 경우. 선언에 포함 하는 경우는 `partial` 한정자, 반환 형식 가능 해야 합니다 `void`합니다.

합니다 *member_name* 메서드의 이름을 지정 합니다. 메서드는 명시적 인터페이스 멤버 구현 하지 않는 한 ([명시적 인터페이스 멤버 구현을](interfaces.md#explicit-interface-member-implementations)), *member_name* 되는 단순히 *식별자*합니다. 명시적 인터페이스 멤버 구현에 대 한 합니다 *member_name* 이루어져는 *interface_type* 뒤에 "`.`" 및 *식별자*합니다.

선택적 *type_parameter_list* 메서드의 형식 매개 변수 지정 ([매개 변수 입력](classes.md#type-parameters)). 경우는 *type_parameter_list* 메서드는 지정 된 된 ***제네릭 메서드***합니다. 메서드에 `extern` 한정자를 *type_parameter_list* 지정할 수 없습니다.

선택적 *formal_parameter_list* 메서드의 매개 변수 지정 ([메서드 매개 변수](classes.md#method-parameters)).

선택적 *type_parameter_constraints_clause*은 개별 형식 매개 변수에 대 한 제약 조건 지정 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)) 하는 경우에 지정할 수 있습니다 및는 *type_parameter_ 목록* 변수도 제공한 메서드가 없는 `override` 한정자입니다.

합니다 *return_type* 에서 참조 되는 형식의 각 합니다 *formal_parameter_list* 메서드의 해야 적어도 메서드 자체 만큼 액세스 가능 ([접근성 제약 조건](basic-concepts.md#accessibility-constraints)).

*method_body* 중 하나는 세미콜론을 ***문 본문*** 요소나 ***식 본문***합니다. 문 본문으로 구성 됩니다는 *블록*, 메서드가 호출 될 때 실행할 문을 지정 합니다. 식 본문이 이루어져 `=>` 뒤에 *식* 및 세미콜론 메서드가 호출 될 때 수행 하는 단일 식을 나타냅니다. 

에 대 한 `abstract` 하 고 `extern` 메서드는 *method_body* 세미콜론으로 구성 됩니다. 에 대 한 `partial` 메서드를 *method_body* 세미콜론, 블록 본문 또는 식 본문이 구성 될 수 있습니다. 다른 모든 메서드는 *method_body* 되었거나 블록 본문을 식 본문입니다.

경우는 *method_body* 선언을 포함 하지 않을 경우 다음을 세미콜론으로 구성 됩니다는 `async` 한정자입니다.

시그니처를 정의 하는 이름, 형식 매개 변수 목록 및 메서드의 정식 매개 변수 목록 ([시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading)) 메서드. 특히 메서드의 시그니처에 해당 이름의 형식 매개 변수 수, 한정자 및 형식 매개 변수 유형의 수가 구성 됩니다. 이러한 목적을 위해 형식 매개 변수 형식에서 발생 하는 메서드의 형식 매개 변수에 메서드의 형식 인수 목록에 있는 서 수 위치를 기준으로 하지만 해당 이름으로 식별 됩니다. 형식 매개 변수 또는 형식 매개 변수 이름을 반환 형식은 없으며 메서드 서명의 일부가 아닙니다.

메서드의 이름을 메서드 이름에 다른 모든 비-동일한 클래스에서 선언에서 달라 야 합니다. 또한 메서드의 시그니처는 동일한 클래스에서 선언 된 다른 모든 메서드의 시그니처와 달라 야 하 고 동일한 클래스에서 선언 하는 두 가지 방법으로만 다른 서명이 없을 `ref` 고 `out`입니다.

메서드의 *type_parameter*가 전체 범위에는 *method_declaration*, 해당 범위에서 전체 폼 형식에 사용할 수 있습니다 *return_type*를 *method_body*, 및 *type_parameter_constraints_clause*s 되지 않습니다 *특성*합니다.

모든 정식 매개 변수 및 형식 매개 변수 이름과 달라 야 합니다.

### <a name="method-parameters"></a>메서드 매개 변수

메서드의 매개 변수 있는 경우 여 선언 된 메서드의 *formal_parameter_list*합니다.

```antlr
formal_parameter_list
    : fixed_parameters
    | fixed_parameters ',' parameter_array
    | parameter_array
    ;

fixed_parameters
    : fixed_parameter (',' fixed_parameter)*
    ;

fixed_parameter
    : attributes? parameter_modifier? type identifier default_argument?
    ;

default_argument
    : '=' expression
    ;

parameter_modifier
    : 'ref'
    | 'out'
    | 'this'
    ;

parameter_array
    : attributes? 'params' array_type identifier
    ;
```

정식 매개 변수 목록이 하나 이상의 쉼표로 구분 된 매개 변수는 마지막만 될 수 있습니다는 *parameter_array*합니다.

*fixed_parameter* 선택적 집합으로 이루어져 *특성* ([특성](attributes.md)), 선택적인 `ref`를 `out` 또는 `this` 한정자는 *형식*, *식별자* 및 선택적 *default_argument*합니다. 각 *fixed_parameter* 지정 된 이름의 지정 된 형식의 매개 변수를 선언 합니다. `this` 한정자를 확장 메서드로 메서드를 지정 하 고 정적 메서드의 첫 번째 매개 변수 에서만 허용 됩니다. 확장 메서드에 추가로 나와 [확장 메서드](classes.md#extension-methods)합니다.

A *fixed_parameter* 사용 하 여를 *default_argument* 라고는 ***선택적 매개 변수***반면를 *fixed_parameter* 없이 *default_argument* 되는 ***필수 매개 변수***합니다. 필수 매개 변수는 선택적 매개 변수 후 나타나지 않을 수 있습니다는 *formal_parameter_list*합니다.

A `ref` 나 `out` 매개 변수에 사용할 수 없습니다는 *default_argument*합니다. 합니다 *식* 에 *default_argument* 다음 중 하나 여야 합니다.

*  *constant_expression*
*  폼의 식을 `new S()` 여기서 `S` 값 형식인
*  폼의 식을 `default(S)` 여기서 `S` 값 형식인

합니다 *식* id 또는 nullable 매개 변수의 형식 변환 하 여 암시적으로 변환할 수 있어야 합니다.

선택적 매개 변수를 구현 하는 partial 메서드 선언에서 발생 하는 경우 ([부분 메서드](classes.md#partial-methods))에 명시적 인터페이스 멤버 구현 ([명시적 인터페이스 멤버 구현을](interfaces.md#explicit-interface-member-implementations)) 또는 단일 매개 변수 인덱서 선언이 있다고 가정 ([인덱서](classes.md#indexers)) 컴파일러가 이러한 멤버를 생략할 수에 대 한 인수를 허용 하는 방식으로 호출 되지 수 있으므로 경고를 제공 해야 합니다.

A *parameter_array* 선택적 집합으로 이루어져 *특성* ([특성](attributes.md)), `params` 한정자는 *array_type*, 및 *식별자*합니다. 매개 변수 배열에 지정 된 이름의 지정 된 배열 형식의 단일 매개 변수를 선언합니다. 합니다 *array_type* 매개 변수의 배열에는 1 차원 배열 형식 이어야 합니다 ([배열 형식을](arrays.md#array-types)). 메서드 호출을 매개 변수 배열에 지정 된 주어진된 배열 형식의 단일 인수를 허용 하거나 지정 배열 요소 형식의 0 개 이상의 인수를 허용 합니다. 매개 변수 배열에 자세히 설명 되어 [매개 변수 배열](classes.md#parameter-arrays)합니다.

A *parameter_array* 선택적 매개 변수를 한 후 발생할 수 있지만 생략에 대 한 인수의 기본 값을 사용할 수 없습니다는 *parameter_array* 대신 초래 빈 배열 생성 합니다.

다음 예제에서는 다른 종류를의 매개 변수를 보여 줍니다.
```csharp
public void M(
    ref int      i,
    decimal      d,
    bool         b = false,
    bool?        n = false,
    string       s = "Hello",
    object       o = null,
    T            t = default(T),
    params int[] a
) { }
```

에 *formal_parameter_list* 에 대 한 `M`, `i` 필수 ref 매개 변수 `d` 필수 값 매개 변수 `b`를 `s`를 `o` 및 `t` 선택적 값 매개 변수 및 `a` 매개 변수 배열입니다.

메서드 선언 매개 변수, 형식 매개 변수 및 지역 변수에 대 한 별도 선언 공간을 만듭니다. 이름에서 지역 변수 선언 및 형식 매개 변수 목록 및 메서드의 정식 매개 변수 목록에서이 선언 공간에 도입 된 합니다 *블록* 메서드. 이 동일한 이름을 갖도록 메서드 선언 공간의 두 멤버에 대 한 오류입니다. 메서드 선언 공간 및 동일한 이름 가진 요소를 포함 하는 중첩 된 선언 공간의 지역 변수 선언 공간에 대 한 오류는 것입니다.

메서드 호출 ([메서드 호출](expressions.md#method-invocations)) 특정 해당 호출에는 복사본을 만들고, 정식 매개 변수 및 호출의 인수 목록과 메서드의 지역 변수 값 또는 변수 참조를 할당 합니다 새로 만든 정식 매개 변수입니다. 내 합니다 *블록* 메서드의 정식 매개 변수에서 해당 식별자에서 참조할 수 *simple_name* 식 ([단순 이름](expressions.md#simple-names)).

정식 매개 변수는 다음과 같은 네 가지 종류가 있습니다.

*  모든 한정자 없이 선언 된 값 매개 변수입니다.
*  매개 변수를 사용 하 여 선언 된 참조는 `ref` 한정자입니다.
*  출력 매개 변수를 사용 하 여 선언 된 `out` 한정자입니다.
*  선언 된 매개 변수 배열과 `params` 한정자입니다.

에 설명 된 대로 [시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading), `ref` 하 고 `out` 한정자는 메서드 시그니처의 일부로 하지만 `params` 한정자는 없습니다.

#### <a name="value-parameters"></a>값 매개 변수

없는 한정자를 사용 하 여 선언 된 매개 변수는 값 매개 변수입니다. 값 매개 변수를 메서드 호출에 제공 하는 해당 인수에서 초기 값을 가져오는 지역 변수에 해당 합니다.

메서드 호출을 해당 인수 암시적으로 변환할 수 있는 식 이어야 값 매개 변수는 정식 매개 변수를 사용 하는 경우 ([암시적 변환을](conversions.md#implicit-conversions)) 정식 매개 변수 형식입니다.

메서드는 값 매개 변수에 새 값을 할당 하도록 허용 됩니다. 이러한 할당 값 매개 변수에서 나타내는 로컬 저장소 위치에만 영향을 주며-메서드 호출에 지정 된 실제 인수에는 영향을 주지 않습니다.

#### <a name="reference-parameters"></a>참조 매개 변수

매개 변수를 사용 하 여 선언 된 `ref` 한정자는 참조 매개 변수입니다. 값 매개 변수를 달리 참조 매개 변수는 새 저장소 위치를 만들지 않습니다. 대신 참조 매개 변수는 메서드 호출의 인수로 지정 된 변수와 동일한 저장소 위치를 나타냅니다.

메서드 호출을 해당 인수 키워드 구성 되어야 합니다는 정식 매개 변수는 참조 매개 변수 이면 `ref` 뒤에 *variable_reference* ([결정 하는 것에 대 한 정확한 규칙 한정 된 할당](variables.md#precise-rules-for-determining-definite-assignment))의 형식 매개 변수 형식과 다릅니다. 변수 참조 매개 변수로 전달할 수 전에 확실 하 게 할당 되어야 합니다.

인 메서드 내부의 참조 매개 변수는 항상 정적으로 할당 합니다.

반복기로 선언 된 메서드 ([반복기](classes.md#iterators)) 참조 매개 변수를 사용할 수 없습니다.

이 예제에서
```csharp
using System;

class Test
{
    static void Swap(ref int x, ref int y) {
        int temp = x;
        x = y;
        y = temp;
    }

    static void Main() {
        int i = 1, j = 2;
        Swap(ref i, ref j);
        Console.WriteLine("i = {0}, j = {1}", i, j);
    }
}
```
는 출력을 생성합니다.
```
i = 2, j = 1
```

호출에 대 한 `Swap` 에 `Main`, `x` 나타냅니다 `i` 하 고 `y` 나타냅니다 `j`합니다. 따라서 호출 효과가 값의 교환을 `i` 고 `j`입니다.

메서드에서 여러 이름이 동일한 저장소 위치를 나타낼 수 하는 참조 매개 변수를 사용 하는 합니다. 예제
```csharp
class A
{
    string s;

    void F(ref string a, ref string b) {
        s = "One";
        a = "Two";
        b = "Three";
    }

    void G() {
        F(ref s, ref s);
    }
}
```
호출 `F` 에 `G` 에 대 한 참조를 전달 `s` 둘 다에 대해 `a` 고 `b`합니다. 이 호출의 경우 이름에 따라서 `s`, `a`, 및 `b` 동일한 저장소 위치, 모든 참조 및 인스턴스 필드를 수정 하는 모든 세 가지 할당 `s`합니다.

#### <a name="output-parameters"></a>출력 매개 변수

사용 하 여 선언 된 매개 변수는 `out` 한정자 출력 매개 변수입니다. 참조 매개 변수와 마찬가지로 출력 매개 변수 만들어지지는지 않습니다 새 저장소 위치. 대신, 출력 매개 변수는 메서드 호출의 인수로 지정 된 변수와 동일한 저장소 위치를 나타냅니다.

메서드 호출을 해당 인수 키워드는 이루어져야 정식 매개 변수가 출력 매개 변수 이면 `out` 뒤에 *variable_reference* ([결정 하는 것에 대 한 정확한 규칙 한정 된 할당](variables.md#precise-rules-for-determining-definite-assignment))의 형식 매개 변수 형식과 다릅니다. 변수를 필요 하지 명확 하 게 할당 output 매개 변수로 전달할 수 있습니다 하지만 변수는 출력 매개 변수로 전달 된 위치에 호출을 다음 변수의 정적으로 할당 된 간주 됩니다.

인 메서드 내부의 마찬가지로 로컬 변수를 output 매개 변수 처음 것으로 간주 되어 할당 되지 않은 해당 값을 사용 하기 전에 반드시 할당 해야 합니다.

메서드의 모든 출력 매개 변수는 메서드가 반환 되기 전에 확실 하 게 할당 되어야 합니다.

부분 메서드로 메서드를 선언 ([부분 메서드](classes.md#partial-methods)) 또는 반복기 ([반복기](classes.md#iterators)) 출력 매개 변수를 있을 수 없습니다.

출력 매개 변수는 일반적으로 여러 개의 반환 값을 생성 하는 메서드에서 사용 됩니다. 예를 들어:
```csharp
using System;

class Test
{
    static void SplitPath(string path, out string dir, out string name) {
        int i = path.Length;
        while (i > 0) {
            char ch = path[i - 1];
            if (ch == '\\' || ch == '/' || ch == ':') break;
            i--;
        }
        dir = path.Substring(0, i);
        name = path.Substring(i);
    }

    static void Main() {
        string dir, name;
        SplitPath("c:\\Windows\\System\\hello.txt", out dir, out name);
        Console.WriteLine(dir);
        Console.WriteLine(name);
    }
}
```

이 예제에서는 출력을 생성합니다.
```
c:\Windows\System\
hello.txt
```

`dir` 하 고 `name` 에 전달 되기 전에 변수에 할당 될 수 있습니다 `SplitPath`, 하는 것이 호출 다음에 정적으로 할당 하 고 합니다.

#### <a name="parameter-arrays"></a>매개 변수 배열

사용 하 여 선언 된 매개 변수는 `params` 한정자 매개 변수 배열입니다. 정식 매개 변수 목록에서 매개 변수 배열에 포함 된 경우 목록에서 마지막 매개 변수 여야 합니다 및 1 차원 배열 형식 이어야 합니다. 예를 들어, 형식 `string[]` 하 고 `string[][]` 매개 변수 배열의 형식이 있지만 형식으로 사용할 수 있습니다 `string[,]` 할 수 없습니다. 결합 하는 것이 불가능 합니다 `params` 한정자를 사용 하 여 한정자 `ref` 고 `out`입니다.

매개 변수 배열에 메서드 호출에서 두 가지 방법 중 하나에 지정 된 수에 대 한 인수를 허용 합니다.

*  매개 변수 배열로 암시적으로 변환할 수 있는 단일 식 수에 대 한 지정 된 인수 ([암시적 변환을](conversions.md#implicit-conversions)) 매개 변수 배열 형식입니다. 이 경우 매개 변수 배열의 값 매개 변수 처럼 정확 하 게 작동합니다.
*  호출 또는 각 인수는 암시적으로 변환할 수 있는 식을 매개 변수 배열에 대해 0 개 이상의 인수를 지정할 수 ([암시적 변환을](conversions.md#implicit-conversions)) 매개 변수 배열의 요소 형식입니다. 호출을 인수의 번호에 해당 하는 길이 사용 하 여 매개 변수 배열 형식의 인스턴스를 만듭니다, 그리고 요소의 지정 된 인수 값을 사용 하 여 배열 인스턴스를 초기화 및 새로 만든된 배열 인스턴스는 실제 사용 하 여이 예제의 경우 인수입니다.

호출에 가변 개수의 인수를 허용 하는 제외 하 고 매개 변수 배열에는 정확 하 게 값 매개 변수 ([매개 변수 값](classes.md#value-parameters)) 동일한 형식입니다.

이 예제에서
```csharp
using System;

class Test
{
    static void F(params int[] args) {
        Console.Write("Array contains {0} elements:", args.Length);
        foreach (int i in args) 
            Console.Write(" {0}", i);
        Console.WriteLine();
    }

    static void Main() {
        int[] arr = {1, 2, 3};
        F(arr);
        F(10, 20, 30, 40);
        F();
    }
}
```
는 출력을 생성합니다.
```
Array contains 3 elements: 1 2 3
Array contains 4 elements: 10 20 30 40
Array contains 0 elements:
```

첫 번째 호출 `F` 배열이 전달 `a` 값 매개 변수로 합니다. 두 번째 호출 `F` 4 개 요소를 자동으로 만듭니다 `int[]` 지정 된 요소 값 및 값 매개 변수로 인스턴스 배열을 전달 합니다. 마찬가지로, 세 번째 호출 `F` 0 요소를 만듭니다 `int[]` 값 매개 변수로 해당 인스턴스를 전달 합니다. 두 번째와 세 번째 호출은 작성 정확 하 게 동일합니다.
```csharp
F(new int[] {10, 20, 30, 40});
F(new int[] {});
```

매개 변수 배열 사용 하 여 메서드 오버 로드 확인을 수행할 때 일반적인 형태로 또는 확장 된 형태로 적용할 수 수 있습니다 ([적용 가능한 함수 멤버](expressions.md#applicable-function-member)). 메서드의 확장 된 폼이 메서드의 일반적인 형태를 적용할 수 없는 경우에 및 확장 형식과 동일한 서명 사용 하 여 해당 메서드는 동일한 형식에 이미 선언 되지 않은 경우에 사용할 수 있는 경우

이 예제에서
```csharp
using System;

class Test
{
    static void F(params object[] a) {
        Console.WriteLine("F(object[])");
    }

    static void F() {
        Console.WriteLine("F()");
    }

    static void F(object a0, object a1) {
        Console.WriteLine("F(object,object)");
    }

    static void Main() {
        F();
        F(1);
        F(1, 2);
        F(1, 2, 3);
        F(1, 2, 3, 4);
    }
}
```
는 출력을 생성합니다.
```
F();
F(object[]);
F(object,object);
F(object[]);
F(object[]);
```

예제에서는 두 개의 매개 변수 배열 사용 하 여 메서드의 확장된 가능한 폼 이미 포함 됩니다 클래스의 일반 메서드로. 이 확장된 형식을 고려 하지 않으므로, 오버 로드 확인을 수행할 때 및 첫 번째 및 세 번째 메서드 호출 하므로 일반 메서드를 선택 합니다. 클래스는 매개 변수 배열 사용 하 여 메서드를 선언 하는 경우 드물지 않습니다도 일반 메서드로 확장된 형식 중 일부를 포함 합니다. 배열 할당을 막을 수 있기 때문에 수행 하 여 인스턴스를 확장 된 형식 매개 변수 배열 사용한 메서드 때 발생 하는 호출 됩니다.

매개 변수 배열 형식의 경우 `object[]`, 메서드의 일반 양식 및 단일에 대 한 확장된 형식 간에 잠재적인 모호성이 발생 `object` 매개 변수입니다. 모호성에 대 한 이유는는 `object[]` 형식으로 암시적으로 변환할 수는 그 자체가 `object`합니다. 그러나 모호성 문제가 발생 하지, 하므로 필요한 경우 캐스트를 삽입 하 여 해결할 수 있습니다.

이 예제에서
```csharp
using System;

class Test
{
    static void F(params object[] args) {
        foreach (object o in args) {
            Console.Write(o.GetType().FullName);
            Console.Write(" ");
        }
        Console.WriteLine();
    }

    static void Main() {
        object[] a = {1, "Hello", 123.456};
        object o = a;
        F(a);
        F((object)a);
        F(o);
        F((object[])o);
    }
}
```
는 출력을 생성합니다.
```
System.Int32 System.String System.Double
System.Object[]
System.Object[]
System.Int32 System.String System.Double
```

첫 번째 및 마지막 호출에서 `F`의 정규형 `F` 매개 변수 형식과 인수 형식에서 암시적 변환이 존재 하기 때문에 적용 됩니다 (둘 다 형식의 `object[]`). 오버 로드 확인의 기본 폼을 선택 하는 따라서 `F`, 인수가 일반 값 매개 변수로 전달 됩니다. 두 번째 및 세 번째 호출에서의 일반적인 형태 `F` 매개 변수 형식과 인수 형식에서 암시적 변환이 존재 하기 때문에 적용 되지 않습니다 (형식 `object` 형식으로 암시적으로 변환할 수 없습니다. `object[]`). 그러나 확장 된 형태의 `F` 적용 될 수 있으므로 오버 로드 확인으로 선택 됩니다. 결과적으로 요소가 하나인 `object[]` 호출에 의해 만들어집니다 배열의 단일 요소에 지정 된 인수 값으로 초기화 됩니다 (에 대 한 참조 되는 자체는 `object[]`).

### <a name="static-and-instance-methods"></a>정적 및 인스턴스 메서드

메서드 선언을 포함 하는 경우는 `static` 한정자, 메서드는 정적 메서드를 라고는 합니다. 없는 경우 `static` 한정자가 있는 메서드는 인스턴스 메서드를 라고 합니다.

정적 메서드는 특정 인스턴스에 작동 하지 않고 이며 컴파일 타임 오류를 가리키는 데 `this` 정적 메서드에서.

인스턴스 메서드를 클래스의 인스턴스에 작동 하 고 해당 인스턴스를 액세스할 수 있습니다 `this` ([이 액세스](expressions.md#this-access)).

메서드를 참조 하는 경우는 *member_access* ([멤버 액세스](expressions.md#member-access)) 형식의 `E.M`이면 `M` 가 정적 메서드가 `E` 를포함하는형식을표시해야합니다`M`, 경우에 `M` 인스턴스 메서드 `E` 포함 하는 형식 인스턴스를 나타내야 `M`합니다.

정적 간의 차이점 및 인스턴스 멤버 설명에 대 한 자세한 [정적 및 인스턴스 멤버](classes.md#static-and-instance-members)합니다.

### <a name="virtual-methods"></a>가상 메서드

인스턴스 메서드 선언 포함 되는 경우는 `virtual` 한정자, 메서드가 가상 메서드를 포함 라고 합니다. 없는 경우 `virtual` 한정자가 있는 메서드는 비가상 메서드를 라고 합니다.

비가상 메서드의 구현은 variant: 구현은 동일 클래스의 인스턴스는 메서드를 호출 하는지 여부를 선언 하거나 파생된 클래스의 인스턴스. 반면, 가상 메서드의 구현은 파생 클래스로 대체 될 수 있습니다. 상속 된 가상 메서드의 구현을 대체 하는 프로세스 라고 ***재정의*** 메서드 ([메서드를 재정의](classes.md#override-methods)).

가상 메서드 호출에서는 합니다 ***런타임 형식*** 해당 호출을 사용 하는 인스턴스의 위치는 호출할 실제 메서드 구현이 결정 합니다. 비가상 메서드 호출에서는 합니다 ***컴파일 타임 형식*** 인스턴스의 결정 요인입니다. 라는 메서드가 정밀 하 게 말해 `N` 인수 목록을 사용 하 여 호출 `A` 컴파일 타임 형식 인스턴스에 대해 `C` 런타임 형식이 `R` (여기서 `R` 는 `C` 파생 된 클래스 또는 `C`), 다음과 같이 처리 됩니다.

*  먼저, 오버 로드 확인에 적용 됩니다 `C`, `N`, 및 `A`특정 메서드를 사용 하려면 `M` 상속에 선언 된 메서드 집합에서 `C`합니다. 에 설명 되어 [메서드 호출](expressions.md#method-invocations)합니다.
*  그런 다음 if `M` 비가상 메서드입니다 `M` 가 호출 됩니다.
*  이 고, 그렇지 `M` 가상 메서드를 이며 가장 많이 파생 된 구현의 `M` 기준으로 `R` 가 호출 됩니다.

모든 가상 메서드에 의해 클래스에서 선언 되거나 상속에 대 한 존재는 ***구현 최다 파생*** 해당 클래스에 대해 메서드. 가장 많이 파생 된 가상 메서드 구현의 `M` 클래스와 관련 하 여 `R` 다음과 같이 결정 됩니다.

*  경우 `R` 포함 된 소개 `virtual` 선언의 `M`, 가장 많이 파생 된 구현입니다 `M`합니다.
*  그렇지 않고 `R` 포함를 `override` 의 `M`, 가장 많이 파생 된 구현입니다 `M`합니다.
*  대부분의 구현을 파생 하는 고, 그렇지 `M` 기준으로 `R` 의 가장 많이 파생 된 구현으로 동일 `M` 의 직접 기본 클래스와 관련 하 여 `R`입니다.

다음 예제에서는 가상 및 비가상 메서드 간의 차이점을 보여 줍니다.
```csharp
using System;

class A
{
    public void F() { Console.WriteLine("A.F"); }

    public virtual void G() { Console.WriteLine("A.G"); }
}

class B: A
{
    new public void F() { Console.WriteLine("B.F"); }

    public override void G() { Console.WriteLine("B.G"); }
}

class Test
{
    static void Main() {
        B b = new B();
        A a = b;
        a.F();
        b.F();
        a.G();
        b.G();
    }
}
```

예에서 `A` 비가상 방법이 도입 되었습니다 `F` 가상 메서드 및 `G`합니다. 클래스 `B` 새 비가상 방법이 도입 되었습니다 `F`, 따라서는 상속 된 변수 숨기기 `F`, 또한 상속 된 메서드를 재정의 하 고 `G`입니다. 이 예제에서는 출력을 생성합니다.
```
A.F
B.F
B.G
B.G
```

문이 `a.G()` 호출 `B.G`아니라 `A.G`합니다. 인스턴스의 런타임 형식 이므로 (되 `B`), 인스턴스 컴파일 시간 형식이 아닌 (는 `A`), 호출할 실제 메서드 구현이 결정 합니다.

있기 때문에 메서드를 상속 된 메서드를 숨길 수 동일한 서명 사용 하 여 여러 가상 메서드를 포함 하는 클래스에 대 한 합니다. 이 가장 많이 파생 된 메서드를 제외한 모든 숨겨져 있으므로 모호성 문제를를 표시 하지 않습니다. 예제
```csharp
using System;

class A
{
    public virtual void F() { Console.WriteLine("A.F"); }
}

class B: A
{
    public override void F() { Console.WriteLine("B.F"); }
}

class C: B
{
    new public virtual void F() { Console.WriteLine("C.F"); }
}

class D: C
{
    public override void F() { Console.WriteLine("D.F"); }
}

class Test
{
    static void Main() {
        D d = new D();
        A a = d;
        B b = d;
        C c = d;
        a.F();
        b.F();
        c.F();
        d.F();
    }
}
```
`C` 하 고 `D` 시그니처가 동일한 두 개의 가상 메서드를 포함 하는 클래스:에서 도입 된 것 `A` 및에 도입 된 것 `C`. 도입 된 메서드 `C` 에서 상속 된 메서드를 숨깁니다. `A`합니다. 따라서의 재정의 선언이 `D` 에서 도입 된 메서드를 재정의 `C`, 수 이며 `D` 도입 된 메서드를 재정의 하 `A`합니다. 이 예제에서는 출력을 생성합니다.
```
B.F
B.F
D.F
D.F
```

인스턴스에 액세스 하 여 숨겨진된 가상 메서드를 호출할 수는 `D` 작음 통해 파생 형식이 없는 메서드 숨겨져 있지 않으면입니다.

### <a name="override-methods"></a>메서드를 재정의 합니다.

인스턴스 메서드 선언 포함 되는 경우는 `override` 한정자를 메서드 라고는 ***메서드를 재정의***합니다. 재정의 메서드 시그니처가 같은 상속된 된 가상 메서드를 재정의합니다. 가상 메서드 선언은 새 메서드를 도입하지만 재정의 메서드 선언은 해당 메서드의 새 구현을 제공하여 기존의 상속된 가상 메서드를 특수화합니다.

에 의해 재정의 메서드는 `override` 선언 이라고 합니다 ***기본 메서드를 재정의***합니다. 재정의 메서드에 대 한 `M` 클래스에 선언 `C`, 재정의 된 기본 메서드는 각 기본 클래스 유형의 검사 하 여 결정 됩니다 `C`부터 시작 하 여 직접 기본 클래스 형식의 `C` 각 진행 및 연속 직접 기본 클래스 형식에 지정 된 기본 클래스 형식에 액세스할 수 있는 메서드는 하나 이상 있는 때까지 동일한 서명을 가진 `M` 형식 인수의 대체 후 합니다. 재정의 된 기본 메서드를 찾기 위해, 메서드 있으면 액세스할 수 있는 비율은 `public`있으면 `protected`있으면 `protected internal`, 인스턴스인 경우 `internal` 같은 프로그램에서 선언 된 `C`합니다.

컴파일 타임 오류가 발생 하는 다음의 모든 재정의 선언에 대해 충족 되지 않으면:

*  재정의 된 기본 메서드는 위에서 설명한 대로 찾을 수 있습니다.
*  이러한 재정의 된 기본 메서드가 정확히 하나만 있습니다. 이 제한은 기본 클래스 형식을 생성 된 형식인 위치 형식 인수의 대체 하면 서명이 두 가지 방법 중 동일한 경우에 효과가 있습니다.
*  재정의 된 기본 메서드는 가상, 추상 되었거나 메서드를 재정의 합니다. 즉, 재정의 된 기본 메서드는 정적 또는 가상 일 수 없습니다.
*  재정의 된 기본 메서드를 봉인된 메서드가 아닙니다.
*  재정의 메서드 및 재정의 된 기본 메서드는 동일한 형식이 반환 합니다.
*  재정의 선언 및 재정의 된 기본 메서드 선언 된 접근성이 동일한 경우 즉, 재정의 선언 가상 메서드의 접근성을 변경할 수 없습니다. 그러나 재정의 된 기본 메서드는 내부 보호 되 고 선언 재정의 메서드를 재정의 메서드를 포함 하는 어셈블리 보다 다른 어셈블리에 선언 된 접근성 보호 되어야 합니다.
*  재정의 선언에서 형식 매개 변수-제약 조건 절을 지정 하지 않습니다. 대신 제약 조건은 재정의 된 기본 메서드에서 상속 됩니다. 참고는 재정의 된 메서드의 형식 매개 변수는 제약 조건을 상속 된 제약 조건에 대 한 형식 인수 바꿀 수 있습니다. 이 잘못 되었습니다. 값 형식 또는 sealed 형식 등과 같은 명시적으로 지정 하는 경우 제약 조건에 발생할 수 있습니다.

다음 예제에서는 제네릭 클래스에 대 한 재정의 규칙이 어떻게 작동 하는 방법을 보여 줍니다.
```csharp
abstract class C<T>
{
    public virtual T F() {...}
    public virtual C<T> G() {...}
    public virtual void H(C<T> x) {...}
}

class D: C<string>
{
    public override string F() {...}            // Ok
    public override C<string> G() {...}         // Ok
    public override void H(C<T> x) {...}        // Error, should be C<string>
}

class E<T,U>: C<U>
{
    public override U F() {...}                 // Ok
    public override C<U> G() {...}              // Ok
    public override void H(C<T> x) {...}        // Error, should be C<U>
}
```

재정의 선언 재정의 된 기본 메서드를 통해 액세스할 수는 *base_access* ([액세스를 기본](expressions.md#base-access)). 예제
```csharp
class A
{
    int x;

    public virtual void PrintFields() {
        Console.WriteLine("x = {0}", x);
    }
}

class B: A
{
    int y;

    public override void PrintFields() {
        base.PrintFields();
        Console.WriteLine("y = {0}", y);
    }
}
```
`base.PrintFields()` 에서 호출 `B` 를 호출 하는 `PrintFields` 에 선언 된 메서드 `A`합니다. A *base_access* 가상 호출 메커니즘을 사용 하지 않도록 설정 하 고 단순히 비가상 메서드로 기본 메서드를 처리 합니다. 호출 했습니다 `B` 된 기록 `((A)this).PrintFields()`, 재귀적으로 것 호출를 `PrintFields` 에 선언 된 메서드 `B`, 아니라 선언 `A`, 있으므로 `PrintFields` 가상 및 런타임 유형의 `((A)this)` 는 `B`합니다.

포함 하 여만 `override` 한정자 수 메서드는 다른 메서드를 재정의 합니다. 다른 모든 경우에서 상속 된 메서드와 동일한 시그니처가 있는 메서드는 단순히 상속 된 메서드를 숨깁니다. 예제
```csharp
class A
{
    public virtual void F() {}
}

class B: A
{
    public virtual void F() {}        // Warning, hiding inherited F()
}
```
`F` 의 메서드 `B` 포함 되지 않습니다는 `override` 한정자 재정의 되지 않습니다 및 합니다 `F` 에서 메서드 `A`합니다. 대신 합니다 `F` 에서 메서드 `B` 메서드를 숨기 `A`, 및 선언에 포함 되지 않아 보고 되는 경고를 `new` 한정자.

예제
```csharp
class A
{
    public virtual void F() {}
}

class B: A
{
    new private void F() {}        // Hides A.F within body of B
}

class C: B
{
    public override void F() {}    // Ok, overrides A.F
}
```
합니다 `F` 의 메서드 `B` 가상 숨깁니다 `F` 에서 상속 된 메서드 `A`합니다. 새 이후 `F` 에 `B` 개인 액세스 권한이 해당 범위에만 클래스 본문에 포함 `B` 로 확장 되지 않습니다 및 `C`합니다. 따라서 선언은 `F` 에서 `C` 를 재정의할 수는 `F` 에서 상속 되며, `A`합니다.

### <a name="sealed-methods"></a>봉인된 메서드

인스턴스 메서드 선언 포함 되는 경우는 `sealed` 한정자, 메서드를 라고 하는 ***메서드를 봉인***합니다. 인스턴스 메서드 선언에 포함 된 경우는 `sealed` 한정자를 포함 해야 합니다 `override` 한정자입니다. 사용 된 `sealed` 한정자는 파생된 클래스에서 추가 메서드를 재정의 하지 않도록 합니다.

예제
```csharp
using System;

class A
{
    public virtual void F() {
        Console.WriteLine("A.F");
    }

    public virtual void G() {
        Console.WriteLine("A.G");
    }
}

class B: A
{
    sealed override public void F() {
        Console.WriteLine("B.F");
    } 

    override public void G() {
        Console.WriteLine("B.G");
    } 
}

class C: B
{
    override public void G() {
        Console.WriteLine("C.G");
    } 
}
```
클래스 `B` 메서드를 재정의 하는 두 가지 제공:는 `F` 변수가 있는 메서드는 `sealed` 한정자 및 `G` 하지 않는 메서드. `B`봉인 된 사용의 `modifier` 방지 `C` 추가로 재정의에서 `F`합니다.

### <a name="abstract-methods"></a>추상 메서드

인스턴스 메서드 선언 포함 되는 경우는 `abstract` 한정자, 메서드를 라고 하는 ***추상 메서드에***합니다. 한정자를 가질 수 없습니다 경우에 추상 메서드를 암시적으로 가상 메서드 `virtual`합니다.

추상 메서드 선언은 새 가상 메서드로 있지만 해당 메서드의 구현을 제공 하지 않습니다. 대신, 비추상 파생된 클래스는 메서드를 재정의 하 여 고유한 구현을 제공 해야 합니다. 추상 메서드 구현을 제공 하지 않으므로 실제, 합니다 *method_body* 추상 메서드는 세미콜론 구성 하기만 하면 됩니다.

추상 메서드 선언은 추상 클래스 에서만 허용 됩니다 ([추상 클래스](classes.md#abstract-classes)).

예제
```csharp
public abstract class Shape
{
    public abstract void Paint(Graphics g, Rectangle r);
}

public class Ellipse: Shape
{
    public override void Paint(Graphics g, Rectangle r) {
        g.DrawEllipse(r);
    }
}

public class Box: Shape
{
    public override void Paint(Graphics g, Rectangle r) {
        g.DrawRect(r);
    }
}
```
`Shape` 클래스 자체를 그릴 수 있는 기하학적 도형 개체의 추상 개념을 정의 합니다. `Paint` 방법은 추상 때문에 의미 있는 기본값을 구현 하지 않습니다. 합니다 `Ellipse` 하 고 `Box` 클래스는 구체적인 `Shape` 구현 합니다. 이러한 클래스는 추상 이기 때문에 이러한 재정의 해야 하는 `Paint` 메서드 및 실제 구현을 제공 합니다.

에 대 한 컴파일 시간 오류를 *base_access* ([액세스를 기본](expressions.md#base-access)) 추상 메서드를 참조 합니다. 예제
```csharp
abstract class A
{
    public abstract void F();
}

class B: A
{
    public override void F() {
        base.F();                        // Error, base.F is abstract
    }
}
```
에 대 한 컴파일 타임 오류가 보고 되는 `base.F()` 호출 추상 메서드를 참조 하기 때문에 합니다.

추상 메서드 선언은 가상 메서드를 재정의할 수 있습니다. 이 강제로 다시 파생된 클래스에서 메서드를 구현 하는 추상 클래스를 허용 하며 메서드의 원래 구현을 사용할 수 없게 합니다. 예제
```csharp
using System;

class A
{
    public virtual void F() {
        Console.WriteLine("A.F");
    }
}

abstract class B: A
{
    public abstract override void F();
}

class C: B
{
    public override void F() {
        Console.WriteLine("C.F");
    }
}
```
클래스 `A` 가상 메서드를 클래스 선언 `B` 추상 메서드 및 클래스를 사용 하 여이 메서드를 재정의 `C` 자체 구현을 제공 하기 위해 추상 메서드를 재정의 합니다.

### <a name="external-methods"></a>외부 메서드

메서드 선언을 포함 하는 경우는 `extern` 한정자, 메서드를 라고 하는 ***외부 메서드의***합니다. 외부 메서드는 일반적으로 C# 이외의 언어를 사용 하 여 외부적으로 구현 됩니다. 외부 메서드 선언은 실제 구현을 제공 하기 때문에 합니다 *method_body* 외부 메서드의 세미콜론의 구성 하기만 하면 됩니다. 외부 메서드를 제네릭일 수 있습니다.

합니다 `extern` 한정자와 함께에서 일반적으로 사용 됩니다는 `DllImport` 특성 ([Win32 및 COM 구성 요소와 상호 운용](attributes.md#interoperation-with-com-and-win32-components)), Dll (동적 연결 라이브러리)에 의해 구현 되어야 하는 외부 메서드를 허용 합니다. 실행 환경 외부 메서드의 구현을 제공할 수 있습니다 가능해 집니다 다른 메커니즘을 지원할 수 있습니다.

외부 메서드를 포함 하는 경우는 `DllImport` 특성인 메서드 선언도 포함 해야 합니다는 `static` 한정자입니다. 이 예제에서는 사용 합니다 `extern` 한정자와 `DllImport` 특성:
```csharp
using System.Text;
using System.Security.Permissions;
using System.Runtime.InteropServices;

class Path
{
    [DllImport("kernel32", SetLastError=true)]
    static extern bool CreateDirectory(string name, SecurityAttribute sa);

    [DllImport("kernel32", SetLastError=true)]
    static extern bool RemoveDirectory(string name);

    [DllImport("kernel32", SetLastError=true)]
    static extern int GetCurrentDirectory(int bufSize, StringBuilder buf);

    [DllImport("kernel32", SetLastError=true)]
    static extern bool SetCurrentDirectory(string name);
}
```

### <a name="partial-methods-recap"></a>부분 메서드 (정리)

메서드 선언을 포함 하는 경우는 `partial` 한정자, 메서드를 라고 하는 ***부분 메서드***합니다. 부분 메서드는 부분 형식의 멤버로 선언할 수 있습니다 ([부분 형식](classes.md#partial-types)), 여러 가지 제한이 따릅니다. 부분 메서드에 추가로 나와 [부분 메서드](classes.md#partial-methods)합니다.

### <a name="extension-methods"></a>확장 메서드

메서드의 첫 번째 매개 변수를 포함 하는 경우는 `this` 한정자, 메서드를 라고 하는 ***확장 메서드***합니다. 확장 메서드는 제네릭이 아닌 비중첩 정적 클래스에서 선언할 수만 있습니다. 확장 메서드의 첫 번째 매개 변수는 이외의 없습니다 한정자를 사용할 수 있습니다 `this`, 및 매개 변수 형식에 대 한 포인터 형식일 수 없습니다.

다음은 예제 확장 메서드를 선언 하는 정적 클래스입니다.
```csharp
public static class Extensions
{
    public static int ToInt32(this string s) {
        return Int32.Parse(s);
    }

    public static T[] Slice<T>(this T[] source, int index, int count) {
        if (index < 0 || count < 0 || source.Length - index < count)
            throw new ArgumentException();
        T[] result = new T[count];
        Array.Copy(source, index, result, 0, count);
        return result;
    }
}
```

확장 메서드는 일반 정적 메서드. 또한 정적 바깥쪽 클래스 범위에 있는 확장 메서드를 호출할 수 인스턴스 메서드 호출 구문을 사용 하 여 ([확장 메서드 호출](expressions.md#extension-method-invocations)), 받는 사람 식을 첫 번째 인수로 사용 하 합니다.

다음 프로그램은 위에서 선언 된 확장 메서드를 사용 합니다.
```csharp
static class Program
{
    static void Main() {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in strings.Slice(1, 2)) {
            Console.WriteLine(s.ToInt32());
        }
    }
}
```

`Slice` 메서드는에서 사용할 수는 `string[]`, 및 `ToInt32` 메서드는에서 사용할 수 `string`이므로 확장 메서드로 선언 합니다. 프로그램의 의미는 다음을 사용 하 여 일반 정적 메서드 호출과 같습니다.
```csharp
static class Program
{
    static void Main() {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in Extensions.Slice(strings, 1, 2)) {
            Console.WriteLine(Extensions.ToInt32(s));
        }
    }
}
```

### <a name="method-body"></a>메서드 본문

합니다 *method_body* 메서드 선언에 블록 본문을 식 본문이 또는 세미콜론으로 하는 구성 합니다.

합니다 ***결과 형식이*** 메서드는 `void` 반환 형식이 `void`, 경우 메서드는 비동기 반환 형식 또는 `System.Threading.Tasks.Task`합니다. 비동기 메서드의 결과 형식을 해당 반환 형식이 며 반환 형식 사용 하 여 비동기 메서드의 결과 형식이 고, 그렇지 `System.Threading.Tasks.Task<T>` 는 `T`합니다.

메서드가 경우를 `void` 형식을 한 블록 본문을 발생 `return` 문 ([return 문을](statements.md#the-return-statement)) 블록에서 허용 되지 않습니다는 식을 지정 합니다. Void 메서드는 블록의 실행 정상적으로 완료 되는 경우 (즉, 제어 흐름이 메서드 본문의 끝)는 메서드를 단순히 현재 호출자에 게 반환 합니다.
    
메서드가 경우는 `void` 결과 식 본문을 식 `E` 이어야 합니다는 *statement_expression*, 본문은 폼의 블록 본문을 동일 하 고 `{ E; }`.
    
메서드는 void가 아닌 결과 형식이 면 및 블록 본문을 각 `return` 블록의 문은 결과 유형으로 암시적으로 변환할 수 있는 식을 지정 해야 합니다. 끝점 값 반환 하는 메서드에 블록 본문을 연결할 수 없어야 합니다. 즉, 블록 본문을 사용 하 여 값을 반환 메서드에서 제어 흐름 메서드 본문의 끝에 허용 되지 않습니다.
    
메서드는 void가 아닌 결과 형식이 있고 식 본문이 식 결과 형식으로 암시적으로 변환할 수 있어야 하 고 본문은 폼의 블록 본문을 동일 `{ return E; }`합니다.
    
예제
```csharp
class A
{
    public int F() {}            // Error, return value required

    public int G() {
        return 1;
    }

    public int H(bool b) {
        if (b) {
            return 1;
        }
        else {
            return 0;
        }
    }

    public int I(bool b) => b ? 1 : 0;
}
```
값 반환 `F` 컨트롤 메서드 본문의 끝을 벗어날 수 있으므로 메서드는 컴파일 타임 오류가 발생 합니다. 합니다 `G` 고 `H` return 문의 반환 값을 지정 하는 모든 가능한 실행 경로 종료 되므로 메서드는 올바른 합니다. `I` 메서드 올바른지 이므로 해당 본문에 단일 return 문으로을 사용 하 여 문 블록에 해당 합니다.

### <a name="method-overloading"></a>메서드 오버로드

메서드 오버 로드 확인 규칙에 설명 되어 있습니다 [형식 유추](expressions.md#type-inference)합니다.

## <a name="properties"></a>속성

A ***속성*** 는 개체 또는 클래스의 특징에 대 한 액세스를 제공 하는 멤버입니다. 속성의 예로, 고객의 이름 창의 캡션 글꼴의 크기 문자열의 길이 등에입니다. 속성은 필드의 기본 확장-모두 연결 된 형식이 멤버 라고 하며 필드 및 속성에 액세스 하기 위한 구문은 동일 합니다. 그러나 필드와 달리 속성은 저장 위치를 명시하지 않습니다. 대신, 속성에는 해당 값을 읽거나 쓸 때 실행될 문을 지정하는 ***접근자***가 있습니다. 속성 읽기 및 쓰기; 개체의 특성을 사용 하 여 작업을 연결 하기 위한 메커니즘을 제공 하므로 또한 이러한 특성을 계산할 허용 합니다.

속성은 사용 하 여 선언 됩니다 *property_declaration*s:

```antlr
property_declaration
    : attributes? property_modifier* type member_name property_body
    ;

property_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'static'
    | 'virtual'
    | 'sealed'
    | 'override'
    | 'abstract'
    | 'extern'
    | property_modifier_unsafe
    ;

property_body
    : '{' accessor_declarations '}' property_initializer?
    | '=>' expression ';'
    ;

property_initializer
    : '=' variable_initializer ';'
    ;
```

A *property_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)) 및 네 가지 액세스 한정자의 유효한 조합이 ([액세스 한정자 ](classes.md#access-modifiers)), `new` ([새 한정자](classes.md#the-new-modifier)), `static` ([정적 메서드와 인스턴스](classes.md#static-and-instance-methods)), `virtual` ([가상메서드](classes.md#virtual-methods)), `override` ([메서드를 재정의](classes.md#override-methods)), `sealed` ([메서드를 봉인](classes.md#sealed-methods)), `abstract` ([추상 메서드](classes.md#abstract-methods)), 및 `extern` ([외부 메서드](classes.md#external-methods)) 한정자.

속성 선언을 메서드 선언으로 동일한 규칙이 적용 됩니다 ([메서드](classes.md#methods)) 한정자의 유효한 조합을 관련 하 여 합니다.

합니다 *형식* 선언 속성의 선언에서 도입 된 속성의 종류를 지정 하며 *member_name* 속성의 이름을 지정 합니다. 속성에는 명시적 인터페이스 멤버 구현이 아닌 합니다 *member_name* 는 단순히 *식별자*합니다. 명시적 인터페이스 멤버 구현에 대 한 ([명시적 인터페이스 멤버 구현을](interfaces.md#explicit-interface-member-implementations)), *member_name* 이루어져는 *interface_type* 뒤에 " `.`"및 *식별자*합니다.

합니다 *형식* 속성의 해야 적어도 속성 자체 만큼 액세스 가능 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).

A *property_body* 하나 구성 될 수 있습니다는 ***접근자 본문*** 요소나 ***식 본문***합니다. 접근자 본문을 *accessor_declarations*는 묶어야 "`{`"및"`}`" 접근자를 선언 하는 토큰 ([접근자](classes.md#accessors)) 속성입니다. 접근자에는 읽기 및 쓰기 속성을 사용 하 여 연결 된 실행 가능 문을 지정 합니다.

구성 된 식 본문이 `=>` 뒤에 *식을* `E` 세미콜론은 문 본문을 동일 하 고 `{ get { return E; } }`, 따라서 사용할 수 있습니다만 getter 전용으로 지정 하 고 속성 getter의 결과가 단일 식을 사용 하 여 여기서 제공 됩니다.

A *property_initializer* 자동으로 구현 된 속성에 부여 될 수 있습니다 ([자동으로 구현 된 속성](classes.md#automatically-implemented-properties)), 이러한 내부 필드를 초기화 하 고 지정 된 값을 사용 하 여 속성을 *식*합니다.

경우에 속성에 액세스 하는 구문은 동일 필드, 속성을 분류 되지 않은 변수입니다. 따라서 불가능 속성으로 전달 하는 `ref` 또는 `out` 인수입니다.

속성 선언을 포함 하는 경우는 `extern` 한정자를 속성 이라고는 ***외부 속성***합니다. 외부 속성 선언에는 각 실제 구현을 제공 하기 때문에 해당 *accessor_declarations* 세미콜론으로 구성 됩니다.

### <a name="static-and-instance-properties"></a>정적 및 인스턴스 속성

속성 선언을 포함 하는 경우는 `static` 한정자를 속성 이라고는 ***정적 속성***합니다. 없는 경우 `static` 한정자가 있는 속성 이라고는 ***속성을 인스턴스***합니다.

정적 속성 특정 인스턴스와 연결 되며 컴파일 타임 오류를 가리키는 데 `this` 정적 속성의 접근자에서.

인스턴스 속성을 클래스의 특정 인스턴스와 연결 되며으로 해당 인스턴스에 액세스할 수 있습니다 `this` ([이 액세스](expressions.md#this-access))에서 해당 속성의 접근자입니다.

속성에서 참조 되는 경우는 *member_access* ([멤버 액세스](expressions.md#member-access)) 형식의 `E.M`이면 `M` 정적 속성인 `E` 를포함하는형식을표시해야합니다`M`, 경우에 `M` 인스턴스 속성을 E를 포함 하는 형식 인스턴스의 나타내야 `M`합니다.

정적 간의 차이점 및 인스턴스 멤버 설명에 대 한 자세한 [정적 및 인스턴스 멤버](classes.md#static-and-instance-members)합니다.

### <a name="accessors"></a>접근자

합니다 *accessor_declarations* 속성 읽기 및 쓰기 속성을 사용 하 여 연결 된 실행 가능 문을 지정 합니다.

```antlr
accessor_declarations
    : get_accessor_declaration set_accessor_declaration?
    | set_accessor_declaration get_accessor_declaration?
    ;

get_accessor_declaration
    : attributes? accessor_modifier? 'get' accessor_body
    ;

set_accessor_declaration
    : attributes? accessor_modifier? 'set' accessor_body
    ;

accessor_modifier
    : 'protected'
    | 'internal'
    | 'private'
    | 'protected' 'internal'
    | 'internal' 'protected'
    ;

accessor_body
    : block
    | ';'
    ;
```

접근자 선언을 이루어진를 *get_accessor_declaration*, *set_accessor_declaration*, 또는 둘 다. 각 접근자 선언의 토큰 이루어져 `get` 또는 `set` 뒤에 선택적인 *accessor_modifier* 와 *accessor_body*합니다.

사용 *accessor_modifier*s 다음과 같은 제한 사항이 적용 됩니다.

*  *accessor_modifier* 인터페이스 또는 명시적 인터페이스 멤버 구현에서 사용할 수 있습니다.
*  속성 또는 인덱서가 없는 `override` 한정자는 *accessor_modifier* 속성 또는 인덱서는 둘 다 포함 하는 경우에 허용 됩니다는 `get` 및 `set` 접근자 중 하나에 허용 됩니다 접근자입니다.
*  속성 또는 인덱서를 포함 하는 `override` 한정자가 접근자와 일치 해야 합니다는 *accessor_modifier*재정의 접근자의 경우.
*  합니다 *accessor_modifier* 속성 또는 인덱서 자체의 선언 된 접근성 보다 더 엄격 하 게 제한적인 접근성을 선언 해야 합니다. 정확 하 게 합니다.
   * 선언 된 접근성 속성 또는 인덱서 수 있는지 `public`는 *accessor_modifier* 중 하나일 수 있습니다 `protected internal`를 `internal`를 `protected`, 또는 `private`합니다.
   * 선언 된 접근성 속성 또는 인덱서 수 있는지 `protected internal`는 *accessor_modifier* 중 하나일 수 있습니다 `internal`에 `protected`, 또는 `private`합니다.
   * 선언 된 접근성 속성 또는 인덱서 수 있는지 `internal` 또는 `protected`서 *accessor_modifier* 여야 합니다 `private`합니다.
   * 선언 된 접근성 속성 또는 인덱서 수 있는지 `private`, no *accessor_modifier* 사용할 수 있습니다.

에 대 한 `abstract` 하 고 `extern` 속성을 *accessor_body* 지정 된 각 접근자는 단순히 세미콜론에 대 한 합니다. 각 extern이 아닌 비추상 속성 있을 *accessor_body* 세미콜론 일 경우에서는 ***자동으로 구현 된 속성*** ([자동으로 구현 된 속성 ](classes.md#automatically-implemented-properties)). 자동으로 구현 된 속성 get 접근자를 하나 이상 있어야 합니다. 모든 다른 비추상, extern이 아닌 속성의 접근자에는 *accessor_body* 는 *블록* 해당 접근자가 호출 될 때 실행할 문을 지정 하는 합니다.

`get` 접근자는 속성 형식의 반환 값을 사용 하 여 매개 변수가 없는 메서드에 해당 합니다. 속성 식에서 참조 될 때 할당의 대상으로 제외 합니다 `get` 속성의 접근자 속성의 값을 계산 하기 위해 호출 되 ([식의 값](expressions.md#values-of-expressions)). 본문을 `get` 접근자는 값을 반환 하는 것에 대 한 규칙을 따라야 합니다에 설명 된 메서드 [메서드 본문](classes.md#method-body)합니다. 특히, 모든 `return` 문의 본문에는 `get` 접근자 속성 형식을 암시적으로 변환할 수 있는 식을 지정 해야 합니다. 또한 끝점을 `get` 접근자를 연결할 수 있어야 합니다.

A `set` 접근자 메서드에 해당 하는 속성 형식의 단일 값 매개 변수를 사용 하 여 및 `void` 형식을 반환 합니다. 암시적 매개 변수를 `set` 접근자의 이름은 항상 `value`합니다. 속성이 할당의 대상으로 참조 되는 경우 ([대입 연산자](expressions.md#assignment-operators)), 또는의 피연산자로 `++` 하거나 `--` ([후 위 증가 및 감소 연산자](expressions.md#postfix-increment-and-decrement-operators), [ 전위 증가 및 감소 연산자](expressions.md#prefix-increment-and-decrement-operators)), `set` 인수를 사용 하 여 접근자가 호출 됩니다 (의 피연산자 또는 할당의 오른쪽에 있는 값인 합니다 `++` 또는 `--` 연산자)는 새 값을 제공 합니다 ([단순 할당](expressions.md#simple-assignment)). 본문을 `set` 접근자에 대 한 규칙을 따라야 `void` 에 설명 된 방법을 [메서드 본문](classes.md#method-body)합니다. 특히 `return` 문에서 `set` 접근자 본문 식을 지정할 수 없습니다. 있으므로 `set` 접근자에는 암시적으로 명명 된 매개 변수가 `value`에서 지역 변수 또는 상수 선언에 대 한 컴파일 시간 오류가 발생을 `set` 해당 이름을 가진 접근자입니다.

유무에 따라 합니다 `get` 및 `set` 접근자 속성을 다음과 같이 분류 됩니다.

*  모두 포함 하는 속성을 `get` 접근자 및 `set` 접근자를 라고는 ***읽기 / 쓰기*** 속성입니다.
*  만 있는 속성을 `get` 접근자를 라고는 ***읽기 전용*** 속성입니다. 이 할당 대상일 수 읽기 전용 속성에 대 한 컴파일 시간 오류입니다.
*  만 있는 속성을 `set` 접근자를 라고는 ***쓰기 전용*** 속성입니다. 제외 할당의 대상으로는 쓰기 전용 속성 식에서 참조 하는 컴파일 타임 오류가 것입니다.

예제
```csharp
public class Button: Control
{
    private string caption;

    public string Caption {
        get {
            return caption;
        }
        set {
            if (caption != value) {
                caption = value;
                Repaint();
            }
        }
    }

    public override void Paint(Graphics g, Rectangle r) {
        // Painting code goes here
    }
}
```
합니다 `Button` 컨트롤에는 공용 선언 `Caption` 속성입니다. `get` 의 접근자는 `Caption` 개인에 저장 된 문자열을 반환 하는 속성 `caption` 필드입니다. `set` 접근자는 새 값이 현재 값과 다른 경우 새 값을 저장 및 확인 하 고 컨트롤을 다시 그립니다. 속성 위에 표시 된 패턴을 따르는 경우가 많습니다:는 `get` 접근자는 단순히 개인 필드에 저장 된 값을 반환 하며 `set` 접근자는 private 필드를 수정 하 고 완벽 하 게 상태를 업데이트 하는 데 필요한 모든 추가 작업을 수행 합니다 개체입니다.

지정 된 `Button` 위의 사용 되는 클래스, 다음은 사용의 예로 `Caption` 속성:
```csharp
Button okButton = new Button();
okButton.Caption = "OK";            // Invokes set accessor
string s = okButton.Caption;        // Invokes get accessor
```

여기에 `set` 속성에 값을 할당 하 여 접근자가 호출 및 `get` 접근자는 속성 식에서 참조 하 여 호출 됩니다.

합니다 `get` 및 `set` 접근자 속성의 고유 멤버는 이므로 속성의 접근자를 개별적으로 선언할 수 있습니다. 따라서 서로 다른 액세스 가능성을 갖도록 하는 읽기 / 쓰기 속성의 두 접근자에 대 한 가능한 아닙니다. 이 예제에서
```csharp
class A
{
    private string name;

    public string Name {                // Error, duplicate member name
        get { return name; }
    }

    public string Name {                // Error, duplicate member name
        set { name = value; }
    }
}
```
단일 읽기 / 쓰기 속성을 선언 하지 않습니다. 대신, 읽기 전용으로 하나는 동일한 이름의 두 속성을 선언 하 고 쓰기 전용 하나. 동일한 클래스에 선언 된 두 명의 멤버 이름이 가질 수 있으므로 예제는 컴파일 타임 오류가 발생 하면 합니다.

상속 된 속성으로 같은 이름의 속성을 선언 하는 파생된 클래스에서 파생 된 속성 읽기와 쓰기에 대해 상속 된 속성을 숨깁니다. 예제
```csharp
class A
{
    public int P {
        set {...}
    }
}

class B: A
{
    new public int P {
        get {...}
    }
}
```
`P` 속성에서 `B` 숨깁니다 합니다 `P` 속성에서 `A` 읽기와 쓰기에 대해 합니다. 따라서 문에서
```csharp
B b = new B();
b.P = 1;          // Error, B.P is read-only
((A)b).P = 1;     // Ok, reference to A.P
```
에 대 한 할당 `b.P` 이후 읽기 전용 보고 컴파일 타임 오류가 발생 `P` 속성에서 `B` 쓰기 전용 숨깁니다 `P` 속성에서 `A`합니다. 단, 숨겨진 액세스 하는 캐스트를 사용할 수 있도록 `P` 속성입니다.

공용 필드와 달리 속성 개체의 내부 상태와 해당 공용 인터페이스 간의 분리를 제공합니다. 예를 살펴보겠습니다.
```csharp
class Label
{
    private int x, y;
    private string caption;

    public Label(int x, int y, string caption) {
        this.x = x;
        this.y = y;
        this.caption = caption;
    }

    public int X {
        get { return x; }
    }

    public int Y {
        get { return y; }
    }

    public Point Location {
        get { return new Point(x, y); }
    }

    public string Caption {
        get { return caption; }
    }
}
```

여기에 `Label` 클래스는 두 개의 `int` 필드 `x` 및 `y`, 해당 위치를 저장 합니다. 위치는 공개적으로으로 노출 되는 `X` 및 `Y` 속성와는 `Location` 형식의 속성 `Point`. 나중 버전의 경우 `Label`, 위치를 저장 하는 편리한 되기를 `Point` 변경 클래스의 공용 인터페이스에 영향을 주지 않고 내부적으로 수 있습니다.
```csharp
class Label
{
    private Point location;
    private string caption;

    public Label(int x, int y, string caption) {
        this.location = new Point(x, y);
        this.caption = caption;
    }

    public int X {
        get { return location.x; }
    }

    public int Y {
        get { return location.y; }
    }

    public Point Location {
        get { return location; }
    }

    public string Caption {
        get { return caption; }
    }
}
```

했습니다 `x` 하 고 `y` 대신 되었습니다 `public readonly` 필드 것이 더 하지를 이러한 변경 수는 `Label` 클래스.

상태 속성을 통해 노출 필드를 직접 노출 하는 경우 반드시 만큼 효율적 아닙니다. 특히 속성은 비가상 약간의 코드가 포함을 실행 환경에는 접근자의 실제 코드를 사용 하 여 접근자에 대 한 호출을 대체할 수 있으며. 이 프로세스는 이라고 ***인라인***, 속성 액세스를 효율적으로 필드 액세스를 사용 하면 아직 속성의 뛰어난 유연성을 유지 하 고 있습니다.

호출 이후를 `get` 접근자의 필드 값을 읽는 개념적으로 동일, 잘못 된 프로그래밍 스타일에 대 한 것으로 간주 됩니다 `get` observable 의도 하지 않은 접근자입니다. 예제
```csharp
class Counter
{
    private int next;

    public int Next {
        get { return next++; }
    }
}
```
값을 `Next` 속성 속성에 이전에 액세스 하는 횟수에 따라 달라 집니다. 따라서 눈에 띄는-부작용을 생성 속성에 액세스 하 고 대신 속성을 메서드로 구현 합니다.

"의도" 규칙에 대 한 `get` 접근자는 한다고 `get` 접근자 단순히 필드에 저장 된 값을 반환 하도록 항상 작성 해야 합니다. 실제로 `get` 접근자 종종 여러 필드에 액세스 하거나 메서드를 호출 하 여 속성의 값을 계산 합니다. 그러나 제대로 설계 된 `get` 접근자 개체의 상태 observable 변경 시키는 없는 작업을 수행 합니다.

속성을 사용 하 여 처음 참조 될 때까지 리소스의 초기화를 지연 시킬 수 있습니다. 예를 들어:
```csharp
using System.IO;

public class Console
{
    private static TextReader reader;
    private static TextWriter writer;
    private static TextWriter error;

    public static TextReader In {
        get {
            if (reader == null) {
                reader = new StreamReader(Console.OpenStandardInput());
            }
            return reader;
        }
    }

    public static TextWriter Out {
        get {
            if (writer == null) {
                writer = new StreamWriter(Console.OpenStandardOutput());
            }
            return writer;
        }
    }

    public static TextWriter Error {
        get {
            if (error == null) {
                error = new StreamWriter(Console.OpenStandardError());
            }
            return error;
        }
    }
}
```

합니다 `Console` 세 가지 속성이 포함 된 클래스 `In`, `Out`, 및 `Error`는 표준 입력, 출력 및 오류 장치 각각 나타냅니다. 이러한 멤버 속성으로 노출 하 여는 `Console` 실제로 사용 될 때까지 클래스 초기화를 지연 시킬 수 있습니다. 예를 들어, 첫 번째 참조 시는 `Out` 에서처럼 속성
```csharp
Console.Out.WriteLine("hello, world");
```
기본 `TextWriter` 출력 장치 생성 됩니다. 응용 프로그램에 대 한 참조를 만들면 하지만 합니다 `In` 및 `Error` 해당 장치에 대 한 속성을 다음 개체가 만들어집니다.

### <a name="automatically-implemented-properties"></a>자동으로 구현 된 속성

자동으로 구현 된 속성 (또는 ***auto 속성*** 줄여서), 세미콜론으로 전용 접근자 본문을 사용 하 여 추상이 아닌 extern이 아닌 속성입니다. Auto 속성 get 접근자가 있어야 합니다 및 set 접근자를 선택할 수도 있습니다.

속성을 자동으로 구현 된 속성으로 지정 하면 숨겨진된 지원 필드를 속성에 대해 자동으로 제공 되며 지원 필드를 읽고 접근자 구현 됩니다. Auto 속성 set 접근자가 없는, 지원 필드 것으로 간주 됩니다 `readonly` ([읽기 전용 필드](classes.md#readonly-fields)). 마찬가지로 `readonly` 필드에는 getter 전용 auto 속성 할당할 수도 있습니다를 바깥쪽 클래스의 생성자의 본문에 있습니다. 속성의 읽기 전용 지원 필드에 직접 할당을 할당합니다.

Auto 속성을 가질 수도 있습니다는 *property_initializer*,으로 지원 필드에 직접 적용 되는 *variable_initializer* ([변수 이니셜라이저](classes.md#variable-initializers)) .

다음 예제:
```csharp
public class Point {
    public int X { get; set; } = 0;
    public int Y { get; set; } = 0;
}
```
다음 선언에 해당 합니다.
```csharp
public class Point {
    private int __x = 0;
    private int __y = 0;
    public int X { get { return __x; } set { __x = value; } }
    public int Y { get { return __y; } set { __y = value; } }
}
```

다음 예제:
```csharp
public class ReadOnlyPoint
{
    public int X { get; }
    public int Y { get; }
    public ReadOnlyPoint(int x, int y) { X = x; Y = y; }
}
```
다음 선언에 해당 합니다.
```csharp
public class ReadOnlyPoint
{
    private readonly int __x;
    private readonly int __y;
    public int X { get { return __x; } }
    public int Y { get { return __y; } }
    public ReadOnlyPoint(int x, int y) { __x = x; __y = y; }
}
```

읽기 전용 필드에 할당 된 유효 생성자 내에서 발생 하기 때문에 알 수 있습니다.


### <a name="accessibility"></a>액세스 가능성

접근자에는 *accessor_modifier*를 액세스 가능 도메인 ([접근성 도메인](basic-concepts.md#accessibility-domains))의 선언 된 접근성을 사용 하 여 결정 됩니다 접근자의는 *accessor_modifier* . 접근자에 없는 경우는 *accessor_modifier*, 접근자의 접근성 도메인은 속성 또는 인덱서의 선언된 된 액세스 가능성에서 결정 됩니다.

현재 상태를 *accessor_modifier* 멤버 조회에 영향을 미치지 ([연산자](expressions.md#operators)) 또는 오버 로드 확인 ([오버 로드 확인](expressions.md#overload-resolution)). 속성 또는 인덱서 한정자는 속성 또는 인덱서는 바인딩되는 액세스의 컨텍스트에서 관계 없이 항상 확인 합니다.

특정 속성 또는 인덱서 선택 되 면 관련 된 특정 접근자의 접근성 도메인은 사용량 유효한 지 확인 하는 데 사용 됩니다.

*  값으로 사용 되는 경우 ([식의 값](expressions.md#values-of-expressions)), `get` 접근자 존재 하며 액세스할 수 있습니다.
*  사용법은 단순한 할당을 대상으로 하는 경우 ([단순 할당](expressions.md#simple-assignment)), `set` 접근자 존재 하며 액세스할 수 있습니다.
*  복합 할당의 대상으로 사용 되는 경우 ([복합 할당](expressions.md#compound-assignment)), 또는 대상으로 합니다 `++` 또는 `--` 연산자 ([함수 멤버](expressions.md#function-members).9, [ 호출 식](expressions.md#invocation-expressions)), 두 합니다 `get` 접근자 및 `set` 접근자 존재 하며 액세스할 수 있습니다.

다음 예제에서는 속성에에서 `A.Text` 속성에 의해 숨겨져 `B.Text`, 경우에 컨텍스트에서는 `set` 접근자가 호출 합니다. 반대로, 속성 `B.Count` 클래스에 액세스할 수 없는 `M`이므로 액세스할 수 있는 속성이 `A.Count` 대신 사용 됩니다.

```csharp
class A
{
    public string Text {
        get { return "hello"; }
        set { }
    }

    public int Count {
        get { return 5; }
        set { }
    }
}

class B: A
{
    private string text = "goodbye"; 
    private int count = 0;

    new public string Text {
        get { return text; }
        protected set { text = value; }
    }

    new protected int Count { 
        get { return count; }
        set { count = value; }
    }
}

class M
{
    static void Main() {
        B b = new B();
        b.Count = 12;             // Calls A.Count set accessor
        int i = b.Count;          // Calls A.Count get accessor
        b.Text = "howdy";         // Error, B.Text set accessor not accessible
        string s = b.Text;        // Calls B.Text get accessor
    }
}
```

인터페이스를 구현 하는 데 사용 되는 접근자 있을 수 없습니다는 *accessor_modifier*합니다. 인터페이스를 구현 해야 하나의 접근자가 사용 되었다면 다른 접근자를 사용 하 여 선언할 수 있습니다는 *accessor_modifier*:
```csharp
public interface I
{
    string Prop { get; }
}

public class C: I
{
    public Prop {
        get { return "April"; }       // Must not have a modifier here
        internal set {...}            // Ok, because I.Prop has no set accessor
    }
}
```

### <a name="virtual-sealed-override-and-abstract-property-accessors"></a>Sealed, 가상, 재정 및 추상 속성 접근자

`virtual` 속성 선언은 속성 접근자는 가상를 지정 합니다. `virtual` 한정자는 읽기 / 쓰기 속성의 접근자를 모두에 적용-읽기 / 쓰기 속성 하나만 접근자는 virtual 일 수 없는 합니다.

`abstract` 속성 선언을 지정 속성의 접근자 가상 하지만 접근자의 실제 구현을 제공 하지 않습니다. 대신, 비추상 파생된 클래스 속성을 재정의 하 여 접근자에 대 한 자체 구현을 제공 해야 합니다. 추상 속성 선언에 대 한 접근자 실제 구현을 제공 하기 때문에 해당 *accessor_body* 단순히를 세미콜론으로 구성 됩니다.

모두 포함 하는 속성 선언을 합니다 `abstract` 및 `override` 속성 추상 이며 기본 속성을 재정의 한정자를 지정 합니다. 이러한 속성의 접근자도 추상입니다.

추상 속성 선언은 추상 클래스 에서만 허용 됩니다 ([추상 클래스](classes.md#abstract-classes)). 지정 하는 속성 선언을 포함 하 여 파생된 클래스에서 상속된 된 가상 속성의 접근자를 재정의할 수 있습니다는 `override` 지시문입니다. 이 ***재정의 속성 선언은***합니다. 재정의 속성 선언은 새 속성을 선언 하지 않습니다. 대신, 기존 가상 속성의 접근자의 구현을 단순히 특수화 합니다.

재정의 속성 선언은 상속 된 속성과 정확 하 게 동일한 액세스 가능성 한정자, 형식 및 이름을 지정 해야 합니다. 경우는 상속 된 경우 속성은 단일 접근자만 (즉, 상속 된 속성이 읽기 전용 또는 쓰기 전용), 재정의 속성에는 해당 접근자만 포함 해야 합니다. 경우 상속 된 속성 접근자를 모두 포함 되어 있습니다 (즉, 경우 상속 된 속성은 읽기 / 쓰기), 재정의 속성은 단일 접근자 또는 접근자를 모두 포함할 수 있습니다.

재정의 속성 선언은 포함 될 수 있습니다는 `sealed` 한정자입니다. 이 한정자를 사용 하는 추가 속성을 재정의에서 파생된 클래스를 방지 합니다. 봉인 된 속성의 접근자도 봉인 됩니다.

선언 및 호출의 차이 제외 하 고 구문, 가상, sealed 재정 및 추상 접근자는 가상, sealed 재정 및 추상 메서드 똑같이 작동 합니다. 규칙에서 설명 하는 특히 [가상 메서드](classes.md#virtual-methods), [메서드를 재정의](classes.md#override-methods)합니다 [메서드를 봉인](classes.md#sealed-methods), 및 [추상 메서드](classes.md#abstract-methods) 적용 처럼 접근자에는 해당 폼의 메서드는 다음과 같습니다.

*  `get` 접근자 메서드에 해당 하는 매개 변수가 없는 속성 형식 및 포함 하는 속성과 같은 한정자의 값을 반환 합니다.
*  A `set` 접근자 메서드에 해당 하는 속성 형식의 단일 값 매개 변수를 사용 하 여를 `void` 형식 및 포함 하는 속성과 같은 한정자를 반환 합니다.

예제
```csharp
abstract class A
{
    int y;

    public virtual int X {
        get { return 0; }
    }

    public virtual int Y {
        get { return y; }
        set { y = value; }
    }

    public abstract int Z { get; set; }
}
```
`X` 가상 읽기 전용 속성은 `Y` 은 가상 읽기 / 쓰기 속성 및 `Z` 추상 읽기 / 쓰기 속성입니다. 때문에 `Z` 는 추상 클래스를 포함 하는 클래스 `A` 추상 선언도 해야 합니다.

파생 된 클래스 `A` 아래에 표시 됩니다.
```csharp
class B: A
{
    int z;

    public override int X {
        get { return base.X + 1; }
    }

    public override int Y {
        set { base.Y = value < 0? 0: value; }
    }

    public override int Z {
        get { return z; }
        set { z = value; }
    }
}
```

여기, 선언을 `X`, `Y`, 및 `Z` 속성 선언을 재정의 합니다. 각 속성 선언 된 접근성 한정자, 형식 및 해당 상속 된 속성의 이름에 정확히 일치합니다. 합니다 `get` 의 접근자 `X` 및 `set` 의 접근자 `Y` 사용 하 여는 `base` 상속 된 접근자에 액세스 하는 키워드입니다. 선언의 `Z` 추상 접근자를 모두 재정의-따라서 가지에서 해결 되지 않은 추상 함수 멤버 없이 `B`, 및 `B` 추상 클래스일 수 있습니다.

속성으로 선언 되는 경우는 `override`, 재정의 된 접근자 재정의 코드에 액세스할 수 있어야 합니다. 또한 선언 된 접근성 및 접근자 속성 또는 인덱서 자체를 모두의 재정의 된 멤버의 형식과 접근자는 일치 해야 합니다. 예를 들어:
```csharp
public class B
{
    public virtual int P {
        protected set {...}
        get {...}
    }
}

public class D: B
{
    public override int P {
        protected set {...}            // Must specify protected here
        get {...}                      // Must not have a modifier here
    }
}
```

## <a name="events"></a>이벤트

***이벤트*** 는 개체 또는 알림을 제공 하는 클래스를 사용 하도록 설정 하는 멤버입니다. 클라이언트를 제공 하 여 이벤트에 대 한 실행 코드를 추가할 수 있습니다 ***이벤트 처리기***합니다.

이벤트를 사용 하 여 선언 된 *event_declaration*s:

```antlr
event_declaration
    : attributes? event_modifier* 'event' type variable_declarators ';'
    | attributes? event_modifier* 'event' type member_name '{' event_accessor_declarations '}'
    ;

event_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'static'
    | 'virtual'
    | 'sealed'
    | 'override'
    | 'abstract'
    | 'extern'
    | event_modifier_unsafe
    ;

event_accessor_declarations
    : add_accessor_declaration remove_accessor_declaration
    | remove_accessor_declaration add_accessor_declaration
    ;

add_accessor_declaration
    : attributes? 'add' block
    ;

remove_accessor_declaration
    : attributes? 'remove' block
    ;
```

*event_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)) 및 네 가지 액세스 한정자의 유효한 조합이 ([액세스 한정자 ](classes.md#access-modifiers)), `new` ([새 한정자](classes.md#the-new-modifier)), `static` ([정적 메서드와 인스턴스](classes.md#static-and-instance-methods)), `virtual` ([가상메서드](classes.md#virtual-methods)), `override` ([메서드를 재정의](classes.md#override-methods)), `sealed` ([메서드를 봉인](classes.md#sealed-methods)), `abstract` ([추상 메서드](classes.md#abstract-methods)), 및 `extern` ([외부 메서드](classes.md#external-methods)) 한정자.

이벤트 선언 (method) 선언으로 동일한 규칙이 적용 됩니다 ([메서드](classes.md#methods)) 한정자의 유효한 조합을 관련 하 여 합니다.

*형식* 이벤트 선언 해야를 *delegate_type* ([참조 형식](types.md#reference-types)), 올바르고 *delegate_type* 이상 이어야 합니다으로 이벤트 자체 만큼 액세스 가능 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).

이벤트 선언이 포함 될 수 있습니다 *event_accessor_declarations*합니다. 그러나 그렇지 않은 경우, extern이 아닌 한 추상이 아닌 이벤트를 컴파일러가 자동으로 제공 ([필드와 유사한 이벤트](classes.md#field-like-events)); extern 이벤트에 대 한 접근자 외부적으로 제공 됩니다.

생략 하는 이벤트 선언 *event_accessor_declarations* 하나 이상의 이벤트를 정의 각각에 대 한 합니다 *variable_declarator*s입니다. 이러한 선언 된 멤버의 모든 적용 된 특성 및 한정자를 *event_declaration*합니다.

에 대 한 컴파일 시간 오류를 *event_declaration* 둘 다 포함 하는 `abstract` 한정자 중괄호로 구분 및 *event_accessor_declarations*합니다.

이벤트 선언이 포함 된 경우는 `extern` 한정자를 이벤트 라고는 ***외부 이벤트***합니다. 외부 이벤트 선언은 실제 구현을 제공 되므로 둘 다 포함에 대 한 오류를 `extern` 한정자와 *event_accessor_declarations*합니다.

에 대 한 컴파일 시간 오류를 *variable_declarator* 사용 하 여 이벤트 선언는 `abstract` 또는 `external` 한정자를 포함는 *variable_initializer*합니다.

이벤트의 왼쪽 피연산자로 사용할 수는 `+=` 하 고 `-=` 연산자 ([이벤트 할당](expressions.md#event-assignment)). 이러한 연산자는 사용 각각 이벤트 처리기를 연결 하거나 이벤트에서 이벤트 처리기를 제거 하 고 이러한 연산이 허용 되는 컨텍스트를 제어 하는 이벤트의 액세스 한정자.

이후 `+=` 고 `-=` 이벤트, 외부 코드를 선언 하는 형식 외부 이벤트에 허용 되는 유일한 작업 수 추가 및 이벤트 처리기를 제거 하지만 수 없습니다. 다른 방식으로 가져올 또는 이벤트의 기본 목록을 수정 처리기입니다.

폼의 작업에서 `x += y` 또는 `x -= y`면 `x` 이벤트 이며 참조의 선언을 포함 하는 형식 외부 이루어집니다 `x`, 작업의 결과 형식이 `void` (대신 유형의 `x`의 값을 사용 하 여 `x` 할당 후). 이 규칙에서 이벤트의 내부 대리자를 직접 검사 외부 코드를 금지 합니다.

다음 예제에서는 이벤트 처리기의 인스턴스에 연결 된 방법의 `Button` 클래스:
```csharp
public delegate void EventHandler(object sender, EventArgs e);

public class Button: Control
{
    public event EventHandler Click;
}

public class LoginDialog: Form
{
    Button OkButton;
    Button CancelButton;

    public LoginDialog() {
        OkButton = new Button(...);
        OkButton.Click += new EventHandler(OkButtonClick);
        CancelButton = new Button(...);
        CancelButton.Click += new EventHandler(CancelButtonClick);
    }

    void OkButtonClick(object sender, EventArgs e) {
        // Handle OkButton.Click event
    }

    void CancelButtonClick(object sender, EventArgs e) {
        // Handle CancelButton.Click event
    }
}
```

여기에 `LoginDialog` 인스턴스 생성자 두 개를 만듭니다 `Button` 인스턴스 및 이벤트 처리기를 연결 합니다 `Click` 이벤트입니다.

### <a name="field-like-events"></a>필드와 유사한 이벤트

클래스 또는 이벤트 선언이 포함 된 구조체의 프로그램 텍스트를 내 필드와 같은 특정 이벤트를 사용할 수 있습니다. 이 방식으로 사용할 이벤트 수 없습니다 `abstract` 나 `extern`를 명시적으로 포함 하지 않아야 하 고 *event_accessor_declarations*합니다. 이러한 이벤트 필드를 허용 하는 모든 컨텍스트에서 사용할 수 있습니다. 대리자를 포함 하는 필드 ([대리자](delegates.md))이 이벤트에 추가 된 이벤트 처리기의 목록을 가리킵니다. 필드를 포함 하는 이벤트 처리기에 추가한 경우 `null`합니다.

예제
```csharp
public delegate void EventHandler(object sender, EventArgs e);

public class Button: Control
{
    public event EventHandler Click;

    protected void OnClick(EventArgs e) {
        if (Click != null) Click(this, e);
    }

    public void Reset() {
        Click = null;
    }
}
```
`Click` 내에서 필드로 사용 되는 `Button` 클래스입니다. 예제에 따라 필드 수 검사, 수정 하 고 대리자 호출 식에 사용 합니다. `OnClick` 의 메서드를 `Button` "발생" 클래스는 `Click` 이벤트입니다. 이벤트 발생 개념은 이벤트가 나타내는 대리자를 호출하는 것과 정확히 동일하므로 이벤트 발생을 위한 특수한 언어 구문은 없습니다. 대리자가 null이 아닌지 확인 하 여 대리자 호출 앞에 note 합니다.

선언의 외부에 `Button` 클래스를 `Click` 멤버의 왼쪽 에서만 사용할 수는 `+=` 및 `-=` 에서처럼 연산자
```csharp
b.Click += new EventHandler(...);
```
대리자의 호출 목록에 추가 된 `Click` 이벤트 및
```csharp
b.Click -= new EventHandler(...);
```
대리자의 호출 목록에서 제거 된 `Click` 이벤트입니다.

필드와 유사한 이벤트를 컴파일할 때 컴파일러는 자동으로 대리자를 포함 하는 저장소가 만들고 추가 하거나 이벤트 처리기 대리자 필드를 제거 하는 이벤트에 대 한 접근자를 만듭니다. 추가 및 제거 작업은 스레드로부터 안전 하 게 될 수 있습니다 (하며 필요 하지 않습니다) 동안에는 수행할된 수는 잠금을 보유 ([lock 문](statements.md#the-lock-statement)) 인스턴스 이벤트를 포함 하는 개체 또는 형식 개체 ([익명 개체 만들기 식](expressions.md#anonymous-object-creation-expressions)) 정적 이벤트에 대 한 합니다.

따라서 인스턴스 이벤트 선언 형식:
```csharp
class X
{
    public event D Ev;
}
```
에 해당 하는 것으로 컴파일됩니다.
```csharp
class X
{
    private D __Ev;  // field to hold the delegate

    public event D Ev {
        add {
            /* add the delegate in a thread safe way */
        }

        remove {
            /* remove the delegate in a thread safe way */
        }
    }
}
```
클래스 내의 `X`에 대 한 참조 `Ev` 의 왼쪽에는 `+=` 및 `-=` 연산자를 추가 하면 및 remove 접근자를 호출 합니다. 다른 모든 참조가 `Ev` 숨겨진된 필드를 참조 하도록 컴파일된 `__Ev` 대신 ([멤버 액세스](expressions.md#member-access)). 이름을 "`__Ev`"은 임의의; 숨김된 필드를 가지기 모든 이름 또는 이름이 없는 전혀 합니다.

### <a name="event-accessors"></a>이벤트 접근자

이벤트 선언에서 일반적으로 생략 *event_accessor_declarations*에서 같이 `Button` 위의 예제입니다. 따라서 수행 하기 위한 한 가지 상황은는 이벤트당 하나의 필드는 저장소 비용을 허용 되지 경우 포함 됩니다. 이러한 경우 클래스를 포함할 수 있습니다 *event_accessor_declarations* 및 이벤트 처리기의 목록을 저장 하는 데는 개인 메커니즘을 사용 합니다.

합니다 *event_accessor_declarations* 이벤트의 이벤트 처리기 추가 및 제거와 관련 된 실행 가능 문을 지정 합니다.

접근자 선언을 이루어진를 *add_accessor_declaration* 와 *remove_accessor_declaration*합니다. 각 접근자 선언의 토큰 이루어져 `add` 또는 `remove` 뒤에 *블록*합니다. *블록* 연관는 *add_accessor_declaration* 이벤트 처리기에 추가 될 때 실행할 문을 지정 하며 *블록* 를연관*remove_accessor_declaration* 이벤트 처리기를 제거할 때 실행할 문을 지정 합니다.

각 *add_accessor_declaration* 및 *remove_accessor_declaration* 이벤트 형식의 단일 값 매개 변수를 사용 하 여 메서드에 해당 하 고 `void` 형식을 반환 합니다. 이벤트 접근자의 암시적 매개 변수 이름은 `value`합니다. 이벤트 이벤트 할당에 사용할 적절 한 이벤트 접근자 사용 됩니다. 특히 할당 연산자가 `+=` add 접근자를 사용 하 고 할당 연산자가 `-=` remove 접근자가 사용 됩니다. 두 경우 모두 대입 연산자의 오른쪽 피연산자는 이벤트 접근자에 대 한 인수로 사용 됩니다. 블록에는 *add_accessor_declaration* 또는 *remove_accessor_declaration* 규칙을 따라야 `void` 에 설명 된 방법 [메서드 본문](classes.md#method-body)합니다. 특히 `return` 이러한 블록의 문은 식을 지정할 수 없습니다.

이벤트 접근자에는 암시적으로 명명 된 매개 변수가 있으므로 `value`, 해당 이름을 가진에 대 한 이벤트 접근자에 선언 된 지역 변수 또는 상수에 대 한 것은 컴파일 시간 오류입니다.

예제
```csharp
class Control: Component
{
    // Unique keys for events
    static readonly object mouseDownEventKey = new object();
    static readonly object mouseUpEventKey = new object();

    // Return event handler associated with key
    protected Delegate GetEventHandler(object key) {...}

    // Add event handler associated with key
    protected void AddEventHandler(object key, Delegate handler) {...}

    // Remove event handler associated with key
    protected void RemoveEventHandler(object key, Delegate handler) {...}

    // MouseDown event
    public event MouseEventHandler MouseDown {
        add { AddEventHandler(mouseDownEventKey, value); }
        remove { RemoveEventHandler(mouseDownEventKey, value); }
    }

    // MouseUp event
    public event MouseEventHandler MouseUp {
        add { AddEventHandler(mouseUpEventKey, value); }
        remove { RemoveEventHandler(mouseUpEventKey, value); }
    }

    // Invoke the MouseUp event
    protected void OnMouseUp(MouseEventArgs args) {
        MouseEventHandler handler; 
        handler = (MouseEventHandler)GetEventHandler(mouseUpEventKey);
        if (handler != null)
            handler(this, args);
    }
}
```
`Control` 클래스 이벤트에 대 한 내부 저장소 메커니즘을 구현 합니다. `AddEventHandler` 메서드는 키를 사용 하 여 대리자 값을 연결 합니다 `GetEventHandler` 메서드는 현재 키와 연결 된 대리자를 반환 및 `RemoveEventHandler` 로 지정된 된 이벤트에 대 한 이벤트 처리기 대리자를 제거 하는 메서드. 연결에 대 한 비용은 되도록 기본 저장소 메커니즘은 아마도 `null` 키가 들어 있는 값을 위임 하 고 따라서 처리 되지 않은 이벤트 저장소를 사용 합니다.

### <a name="static-and-instance-events"></a>정적 및 인스턴스 이벤트

이벤트 선언이 포함 된 경우는 `static` 한정자를 이벤트 라고는 ***정적 이벤트***합니다. 없는 경우 `static` 한정자가 있는 이벤트 라고는 ***인스턴스 이벤트***합니다.

정적 이벤트를 특정 인스턴스와 연결 되며 컴파일 타임 오류를 가리키는 데 `this` 정적 이벤트의 접근자에서 합니다.

인스턴스 이벤트는 클래스의 특정된 인스턴스와 연결 된 및로이 인스턴스를 액세스할 수 있습니다 `this` ([이 액세스](expressions.md#this-access))에서 해당 이벤트의 접근자입니다.

이벤트에서 참조 하는 경우는 *member_access* ([멤버 액세스](expressions.md#member-access)) 형식의 `E.M`이면 `M` 이벤트를 사용 하는 정적 이벤트 `E` 를포함하는형식을표시해야합니다`M`, 경우에 `M` 인스턴스 이벤트가 E를 포함 하는 형식 인스턴스의 나타내야 `M`합니다.

정적 간의 차이점 및 인스턴스 멤버 설명에 대 한 자세한 [정적 및 인스턴스 멤버](classes.md#static-and-instance-members)합니다.

### <a name="virtual-sealed-override-and-abstract-event-accessors"></a>Sealed, 가상, 재정 및 추상 이벤트 접근자

`virtual` 이벤트 선언은 해당 이벤트의 접근자는 가상를 지정 합니다. `virtual` 한정자는 이벤트의 접근자를 모두에 적용 합니다.

`abstract` 이벤트 선언에 지정 된 이벤트의 접근자 가상 하지만 접근자의 실제 구현을 제공 하지 않습니다. 대신, 비추상 파생된 클래스는 이벤트를 재정의 하 여 접근자에 대 한 자체 구현을 제공 해야 합니다. 추상 이벤트 선언은 실제 구현을 제공 하기 때문에 중괄호로 구분 제공할 수 없습니다 *event_accessor_declarations*합니다.

모두 포함 하는 이벤트 선언 된 `abstract` 및 `override` 한정자 이벤트 추상 이며 재정의 기본 이벤트를 지정 합니다. 이러한 이벤트의 접근자도 추상입니다.

추상 이벤트 선언에서 추상 클래스 에서만 허용 됩니다 ([추상 클래스](classes.md#abstract-classes)).

지정 하는 이벤트 선언을 포함 하 여 파생된 클래스에서 상속 된 가상 이벤트의 접근자를 재정의할 수 있습니다는 `override` 한정자입니다. 이 ***이벤트 선언 재정의***합니다. 재정의 하는 이벤트 선언 새 이벤트를 선언 하지 않습니다. 대신, 기존 가상 이벤트의 접근자의 구현을 단순히 특수화 합니다.

재정의 하는 이벤트 선언 재정의 된 이벤트와 정확 하 게 동일한 액세스 가능성 한정자, 형식 및 이름을 지정 해야 합니다.

재정의 이벤트 선언이 포함 될 수 있습니다는 `sealed` 한정자입니다. 이 한정자를 사용 하는 추가 이벤트를 재정의에서 파생된 클래스를 방지 합니다. 봉인 된 이벤트의 접근자도 봉인 됩니다.

포함 하도록 재정의 이벤트 선언에 대 한 컴파일 시간 오류가 발생 한 `new` 한정자입니다.

선언 및 호출의 차이 제외 하 고 구문, 가상, sealed 재정 및 추상 접근자는 가상, sealed 재정 및 추상 메서드 똑같이 작동 합니다. 규칙에서 설명 하는 특히 [가상 메서드](classes.md#virtual-methods), [메서드를 재정의](classes.md#override-methods)합니다 [메서드를 봉인](classes.md#sealed-methods), 및 [추상 메서드](classes.md#abstract-methods) 적용 처럼 접근자는 해당 폼의 메서드를 했습니다. 이벤트 형식의 단일 값 매개 변수를 사용 하 여 메서드에 해당 하는 각 접근자는 `void` 형식 및 포함 하는 이벤트는 같은 한정자를 반환 합니다.

## <a name="indexers"></a>인덱서

***인덱서*** 는 동일한 방식으로 배열에서 인덱싱할 수 있도록 하는 멤버입니다. 인덱서를 사용 하 여 선언 된 *indexer_declaration*s:

```antlr
indexer_declaration
    : attributes? indexer_modifier* indexer_declarator indexer_body
    ;

indexer_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'virtual'
    | 'sealed'
    | 'override'
    | 'abstract'
    | 'extern'
    | indexer_modifier_unsafe
    ;

indexer_declarator
    : type 'this' '[' formal_parameter_list ']'
    | type interface_type '.' 'this' '[' formal_parameter_list ']'
    ;

indexer_body
    : '{' accessor_declarations '}' 
    | '=>' expression ';'
    ;
```

*indexer_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)) 및 네 가지 액세스 한정자의 유효한 조합이 ([액세스 한정자 ](classes.md#access-modifiers)), `new` ([새 한정자](classes.md#the-new-modifier)), `virtual` ([가상 메서드](classes.md#virtual-methods)), `override` ([메서드를 재정의](classes.md#override-methods) )를 `sealed` ([메서드를 봉인](classes.md#sealed-methods)), `abstract` ([추상 메서드](classes.md#abstract-methods)), 및 `extern` ([외부 메서드](classes.md#external-methods)) 한정자.

Indexer 선언을 메서드 선언으로 동일한 규칙이 적용 됩니다 ([메서드](classes.md#methods)) 한정자의 유효한 조합을 관련 하 여 static 한정자를 되는 한 가지 예외를 사용 하 여에서 허용 되지 않습니다는 인덱서 선언이 있다고 가정 합니다.

Modifiers `virtual`, `override`, 및 `abstract` 한 경우 제외 하 고 함께 사용할 수 없습니다. 합니다 `abstract` 고 `override` 추상 인덱서는 가상 인터페이스가 재정의할 수 있도록 한정자 함께 사용할 수 있습니다.

합니다 *형식* 인덱서의 선언은 선언에 의해 정의 된 인덱서의 요소 형식을 지정 합니다. 인덱서는 명시적 인터페이스 멤버 구현이 아닌 합니다 *형식* 키워드 뒤 `this`합니다. 명시적 인터페이스 멤버 구현에 대 한 합니다 *형식* 뒤에 *interface_type*, "`.`", 및 키워드 `this`합니다. 다른 멤버와 달리 인덱서는 사용자 정의 이름을 갖지 않습니다.

합니다 *formal_parameter_list* 인덱서에 매개 변수를 지정 합니다. 메서드는 해당 하는 인덱서의 정식 매개 변수 목록 ([메서드 매개 변수](classes.md#method-parameters)) 매개 변수가 하나 이상 지정 해야 한다는 점을 제외 하면, 및를 `ref` 고 `out` 매개 변수 한정자는 허용 되지 않습니다 .

*형식* 인덱서 및 각 형식에서 참조 되는 *formal_parameter_list* 적어도 인덱서 자체 만큼 액세스 가능 해야 합니다 ([접근성 제약 조건](basic-concepts.md#accessibility-constraints)).

*indexer_body* 하나 구성 될 수 있습니다는 ***접근자 본문*** 요소나 ***식 본문***합니다. 접근자 본문을 *accessor_declarations*는 묶어야 "`{`"및"`}`" 접근자를 선언 하는 토큰 ([접근자](classes.md#accessors)) 속성입니다. 접근자에는 읽기 및 쓰기 속성을 사용 하 여 연결 된 실행 가능 문을 지정 합니다.

구성 된 식 본문이 "`=>`" 뒤에 식이 `E` 세미콜론은 문 본문을 동일 하 고 `{ get { return E; } }`, 따라서 사용할 수 있습니다만 getter 전용 인덱서를 지정 하는 결과인 getter 인 및 단일 식으로 지정 합니다.

인덱서 요소에 액세스 하기 위한 구문은 동일 배열 요소에 대 한, 경우에 인덱서 요소 분류 되지 않은 변수입니다. 따라서 불가능으로 인덱서 요소를 전달 하는 `ref` 또는 `out` 인수입니다.

시그니처를 정의 하는 인덱서의 정식 매개 변수 목록 ([시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading)) 인덱서의 합니다. 특히, 인덱서의 시그니처는 정식 매개 변수의 형식과 수 이루어져 있습니다. 요소 형식 및 형식 매개 변수의 이름이 인덱서의 시그니처의 일부로 않습니다.

인덱서의 시그니처는 동일한 클래스에서 선언 된 다른 모든 인덱서의 시그니처와 달라 야 합니다.

인덱서 및 속성은 개념적으로 매우 유사 하지만 다음과 같이 다릅니다.

*  속성 인덱서 시그니처에으로 식별 되는 반면 해당 이름으로 식별 됩니다.
*  속성을 통해 액세스를 *simple_name* ([단순 이름](expressions.md#simple-names)) 또는 *member_access* ([멤버 액세스](expressions.md#member-access)) 인 반면, 인덱서 요소를 통해 액세스를 *element_access* ([인덱서 액세스](expressions.md#indexer-access)).
*  속성 수는 `static` 멤버 인덱서는 항상 인스턴스 멤버입니다.
*  A `get` 속성의 접근자 메서드에 해당 하는 매개 변수가 없는 반면를 `get` 인덱서의 접근자 메서드에 해당 하는 인덱서와 동일한 형식 매개 변수 목록 사용 하 여 합니다.
*  A `set` 라는 단일 매개 변수를 사용 하 여 메서드에 해당 하는 속성의 접근자 `value`반면를 `set` 인덱서의 접근자 메서드에 해당 하는 추가 매개 변수, 인덱서가와 동일한 형식 매개 변수 목록 사용 하 여 명명 된 `value`합니다.
*  해당 인덱서 매개 변수로 동일한 이름 가진 지역 변수 선언에 대 한 인덱서 접근자에 대 한 컴파일 시간 오류입니다.
*  구문을 사용 하 여 상속 된 속성에 액세스 하는 재정의 속성 선언에 `base.P`여기서 `P` 속성 이름입니다. 재정의 인덱서 선언에서 상속 된 인덱서 액세스 구문을 사용 하 여 `base[E]`여기서 `E` 은 식의 쉼표로 구분 된 목록입니다.
*  "자동으로 구현 된 인덱서" 개념이 있습니다. 것 세미콜론 접근자를 사용 하 여 추상이 아닌, 비 외부 인덱서를 오류가 발생 합니다.

이러한 차이 외에 정의 된 모든 규칙 [접근자](classes.md#accessors) 하 고 [자동으로 구현 된 속성](classes.md#automatically-implemented-properties) 속성 접근자에 대 한 인덱서 접근자를도에 적용 합니다.

Indexer 선언을 포함 하는 경우는 `extern` 한정자를 인덱서 라고는 ***외부 인덱서***합니다. 외부 indexer 선언을 각각의 실제 구현을 제공 하기 때문에 해당 *accessor_declarations* 세미콜론으로 구성 됩니다.

아래 예제에서는 선언 된 `BitArray` 의 비트 배열의 개별 비트에 액세스 하기 위한 인덱서를 구현 하는 클래스입니다.
```csharp
using System;

class BitArray
{
    int[] bits;
    int length;

    public BitArray(int length) {
        if (length < 0) throw new ArgumentException();
        bits = new int[((length - 1) >> 5) + 1];
        this.length = length;
    }

    public int Length {
        get { return length; }
    }

    public bool this[int index] {
        get {
            if (index < 0 || index >= length) {
                throw new IndexOutOfRangeException();
            }
            return (bits[index >> 5] & 1 << index) != 0;
        }
        set {
            if (index < 0 || index >= length) {
                throw new IndexOutOfRangeException();
            }
            if (value) {
                bits[index >> 5] |= 1 << index;
            }
            else {
                bits[index >> 5] &= ~(1 << index);
            }
        }
    }
}
```

인스턴스를 `BitArray` 해당 보다 상당히 적은 메모리를 사용 하는 클래스 `bool[]` (앞의 각 값 대신 하나의 비트만 차지 하므로 후자의 1 바이트), 같은 작업을 허용 하지만 `bool[]`입니다.

다음 `CountPrimes` 클래스가 사용 하는 `BitArray` 알고리즘과 고전 "체" prime 1 사이의 지정된 된 최대 수를 계산 합니다.
```csharp
class CountPrimes
{
    static int Count(int max) {
        BitArray flags = new BitArray(max + 1);
        int count = 1;
        for (int i = 2; i <= max; i++) {
            if (!flags[i]) {
                for (int j = i * 2; j <= max; j += i) flags[j] = true;
                count++;
            }
        }
        return count;
    }

    static void Main(string[] args) {
        int max = int.Parse(args[0]);
        int count = Count(max);
        Console.WriteLine("Found {0} primes between 1 and {1}", count, max);
    }
}
```

요소에 액세스 하는 구문은 `BitArray` 과 동일 하 게 정확 하 게 되는 `bool[]`합니다.

다음 예제에서는 두 개의 매개 변수를 사용 하 여 인덱서를 26 * 10 표 클래스를 보여 줍니다. 대문자 또는 소문자 A-z, 범위에서 첫 번째 매개 변수가 필요 하 고 두 번째 정수 0-9 범위 해야 합니다.

```csharp
using System;

class Grid
{
    const int NumRows = 26;
    const int NumCols = 10;

    int[,] cells = new int[NumRows, NumCols];

    public int this[char c, int col] {
        get {
            c = Char.ToUpper(c);
            if (c < 'A' || c > 'Z') {
                throw new ArgumentException();
            }
            if (col < 0 || col >= NumCols) {
                throw new IndexOutOfRangeException();
            }
            return cells[c - 'A', col];
        }

        set {
            c = Char.ToUpper(c);
            if (c < 'A' || c > 'Z') {
                throw new ArgumentException();
            }
            if (col < 0 || col >= NumCols) {
                throw new IndexOutOfRangeException();
            }
            cells[c - 'A', col] = value;
        }
    }
}
```

### <a name="indexer-overloading"></a>인덱서 오버 로드

인덱서 오버 로드 확인 규칙에 설명 되어 있습니다 [형식 유추](expressions.md#type-inference)합니다.

## <a name="operators"></a>연산자

***연산자*** 는 클래스의 인스턴스를 적용할 수 있는 식 연산자의 의미를 정의 하는 멤버입니다. 연산자를 사용 하 여 선언 된 *operator_declaration*s:

```antlr
operator_declaration
    : attributes? operator_modifier+ operator_declarator operator_body
    ;

operator_modifier
    : 'public'
    | 'static'
    | 'extern'
    | operator_modifier_unsafe
    ;

operator_declarator
    : unary_operator_declarator
    | binary_operator_declarator
    | conversion_operator_declarator
    ;

unary_operator_declarator
    : type 'operator' overloadable_unary_operator '(' type identifier ')'
    ;

overloadable_unary_operator
    : '+' | '-' | '!' | '~' | '++' | '--' | 'true' | 'false'
    ;

binary_operator_declarator
    : type 'operator' overloadable_binary_operator '(' type identifier ',' type identifier ')'
    ;

overloadable_binary_operator
    : '+'   | '-'   | '*'   | '/'   | '%'   | '&'   | '|'   | '^'   | '<<'
    | 'right_shift' | '=='  | '!='  | '>'   | '<'   | '>='  | '<='
    ;

conversion_operator_declarator
    : 'implicit' 'operator' type '(' type identifier ')'
    | 'explicit' 'operator' type '(' type identifier ')'
    ;

operator_body
    : block
    | '=>' expression ';'
    | ';'
    ;
```

연산자를 오버 로드할 수 있는 세 종류: 단항 연산자 ([단항 연산자](classes.md#unary-operators)), 이항 연산자 ([이항 연산자](classes.md#binary-operators)), 및 변환 연산자 ([변환 연산자 ](classes.md#conversion-operators)).

*operator_body* 중 하나는 세미콜론을 ***문 본문*** 요소나 ***식 본문***합니다. 문 본문으로 구성 됩니다는 *블록*, 연산자 호출 될 때 실행할 문을 지정 합니다. 합니다 *블록* 값을 반환 하는 것에 대 한 규칙을 따라야에 설명 된 방법을 [메서드 본문](classes.md#method-body)합니다. 식 본문이 이루어져 `=>` 식과 세미콜론, 뒤 및 연산자가 호출 되 면 하는 데 단일 식을 나타냅니다.

에 대 한 `extern` 연산자는 *operator_body* 세미콜론으로 구성 됩니다. 다른 모든 연산자에 대 한 합니다 *operator_body* 되었거나 블록 본문을 식 본문입니다.

모든 연산자 선언에는 다음 규칙이 적용 됩니다.

*  연산자 선언 모두 포함 해야 합니다는 `public` 및 `static` 한정자입니다.
*  연산자의 매개 변수 값 매개 변수 여야 합니다. ([매개 변수 값](variables.md#value-parameters)). 지정 하는 연산자 선언에 대 한 컴파일 타임 오류 `ref` 또는 `out` 매개 변수입니다.
*  연산자의 시그니처에 ([단항 연산자](classes.md#unary-operators)를 [이항 연산자](classes.md#binary-operators), [변환 연산자](classes.md#conversion-operators))에 선언 된 다른 모든 연산자의 시그니처와에서 달라 야 합니다 동일한 클래스입니다.
*  연산자 선언에서 참조 하는 모든 형식은 적어도 연산자 자체 수준 만큼 액세스 가능 이어야 합니다 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).
*  연산자 선언에 여러 번 표시 하는 동일한 한정자에 대 한 오류는 것입니다.

각 연산자 범주는 다음 섹션에 설명 된 대로 추가 제한을 적용 합니다.

다른 멤버와 마찬가지로 기본 클래스에서 선언 된 연산자는 파생된 클래스에서 상속 됩니다. 연산자 선언에는 반드시 클래스 또는 구조체 연산자는 연산자의 시그니처에 참여 하도록 선언 되는, 때문에 기본 클래스에 선언 된 운영자를 숨기려면 파생된 클래스에서 선언 하는 연산자에 대 한는 것이 불가능 합니다. 따라서는 `new` 한정자 필요 하지 이며 따라서 되지 허용 연산자 선언에 있습니다.

단항 및 이항 연산자에 대 한 추가 정보에서 찾을 수 있습니다 [연산자](expressions.md#operators)합니다.

변환 연산자에 대 한 추가 정보를 찾을 수 있습니다 [사용자 정의 변환은](conversions.md#user-defined-conversions)합니다.

### <a name="unary-operators"></a>단항 연산자

단항 연산자 선언에는 다음 규칙이 적용 됩니다. 여기서 `T` 클래스 또는 연산자 선언이 포함 된 구조체의 인스턴스 유형을 나타냅니다.

*  단항 `+`, `-`를 `!`, 또는 `~` 연산자 형식의 단일 매개 변수를 사용 해야 `T` 또는 `T?` 모든 형식을 반환할 수 있습니다.
*  단항 `++` 나 `--` 연산자 형식의 단일 매개 변수를 사용 해야 `T` 또는 `T?` 하며 동일한 형식 또는 형식에서 파생 된 반환 해야 합니다.
*  단항 `true` 또는 `false` 연산자 형식의 단일 매개 변수를 사용 해야 `T` 또는 `T?` 형식을 반환 해야 합니다 및 `bool`합니다.

단항 연산자의 서명은 연산자 토큰의 (`+`, `-`, `!`, `~`, `++`를 `--`, `true`, 또는 `false`) 및 단일 정식 매개 변수 형식입니다. 반환 형식은 단항 연산자의 서명의 일부가 아닌 하거나 형식 매개 변수의 이름입니다.

합니다 `true` 고 `false` 단항 연산자는 쌍 단위 선언 해야 합니다. 클래스 선언도 다른 선언 하지 않고 이러한 연산자 중 하나는 컴파일 타임 오류가 발생 합니다. `true` 하 고 `false` 연산자에 자세히 설명 되어 [사용자 정의 조건부 논리 연산자](expressions.md#user-defined-conditional-logical-operators) 하 고 [부울 식](expressions.md#boolean-expressions).

다음 예제에서는 구현 및의 후속 사용 `operator ++` 정수 벡터 클래스:
```csharp
public class IntVector
{
    public IntVector(int length) {...}

    public int Length {...}                 // read-only property

    public int this[int index] {...}        // read-write indexer

    public static IntVector operator ++(IntVector iv) {
        IntVector temp = new IntVector(iv.Length);
        for (int i = 0; i < iv.Length; i++)
            temp[i] = iv[i] + 1;
        return temp;
    }
}

class Test
{
    static void Main() {
        IntVector iv1 = new IntVector(4);    // vector of 4 x 0
        IntVector iv2;

        iv2 = iv1++;    // iv2 contains 4 x 0, iv1 contains 4 x 1
        iv2 = ++iv1;    // iv2 contains 4 x 2, iv1 contains 4 x 2
    }
}
```

연산자 메서드 후 위 증가 마찬가지로 피연산자를 1을 추가 하 여 생성 한 값을 반환 하는 방법 및 감소 연산자 ([후 위 증가 및 감소 연산자](expressions.md#postfix-increment-and-decrement-operators)), 접두사 증가 및 감소 연산자 ([전위 증가 및 감소 연산자](expressions.md#prefix-increment-and-decrement-operators)). 와 달리 c + +에서는이 메서드가 필요 직접 수정 하지는 피연산자의 값. 사실, 피연산자 값을 수정 후 위 증가 연산자의 표준 의미 체계를 위반 합니다.

### <a name="binary-operators"></a>이항 연산자

이항 연산자 선언에는 다음 규칙이 적용 됩니다. 여기서 `T` 클래스 또는 연산자 선언이 포함 된 구조체의 인스턴스 유형을 나타냅니다.

*  이진 앤 시프트 연산자는 하나 이상의 형식이 있어야 하는 두 개의 매개 변수를 사용 해야 합니다 `T` 또는 `T?`, 모든 형식을 반환할 수 있습니다.
*  이진 `<<` 또는 `>>` 연산자는 첫 번째 형식이 있어야 합니다. 두 매개 변수를 사용 해야 `T` 또는 `T?` 의 두 번째 형식이 있어야 하 고 `int` 또는 `int?`, 모든 형식을 반환할 수 있습니다.

이항 연산자의 서명은 연산자 토큰의 (`+`, `-`, `*`, `/`, `%`를 `&`, `|`를 `^`를 `<<`, `>>`, `==`, `!=`를 `>`, `<`를 `>=`, 또는 `<=`) 및 두 개의 형식 매개 변수의 형식입니다. 반환 형식 및 형식 매개 변수의 이름을 이항 연산자의 시그니처의 일부로 않습니다.

특정 이진 연산자에는 쌍 단위 선언이 필요 합니다. 쌍의 두 연산자의 모든 선언에 대 한 쌍의 다른 연산자의 일치 하는 선언 이어야 합니다. 두 연산자 선언에는 각 매개 변수에 대해 동일한 형식과 반환 형식이 있을 경우 일치 합니다. 다음과 같은 연산자에는 쌍 단위 선언이 필요 합니다.

*  `operator ==` 및 `operator !=`
*  `operator >` 및 `operator <`
*  `operator >=` 및 `operator <=`

### <a name="conversion-operators"></a>변환 연산자

변환 연산자 선언은 소개를 ***사용자 정의 변환이*** ([사용자 정의 변환은](conversions.md#user-defined-conversions)) 미리 정의 된 암시적 및 명시적 변환을 확대 하는 합니다.

포함 하는 변환 연산자 선언은 `implicit` 키워드는 사용자 정의 된 암시적 변환을 정의 합니다. 다양 한 상황, 멤버 호출 함수, 캐스트 식 및 할당을 포함 하 여 암시적으로 발생할 수 있습니다. 이에서 더 자세히 설명 [암시적 변환을](conversions.md#implicit-conversions)입니다.

포함 하는 변환 연산자 선언은 `explicit` 키워드는 사용자 정의 명시적 변환을 정의 합니다. 명시적 변환은 cast 식에서 발생할 수 있으며에 자세히 설명 되어 [명시적 변환](conversions.md#explicit-conversions)합니다.

변환 연산자 변환 연산자의 반환 형식으로 표시 된 대상 형식으로 변환 연산자의 매개 변수 형식으로 표시 된 원본 형식에서 변환 합니다.

지정 된 소스 형식에 대 한 `S` 대상 유형 및 `T`이면 `S` 또는 `T` nullable 형식 수 있도록 `S0` 및 `T0` 그렇지 않으면 해당 기본 형식 참조 `S0` 및 `T0` 됩니다 같음 `S` 고 `T` 각각. 클래스 또는 구조체를 선언할 수 원본 형식에서 변환 `S` 대상 형식으로 `T` 다음 모두 만족 하는 경우에:

*  `S0` 및 `T0` 가지 유형이 있습니다.
*  중 하나 `S0` 또는 `T0` 는 연산자 선언이 발생 하는 클래스 또는 구조체 형식입니다.
*  모두 `S0` 나 `T0` 되는 *interface_type*합니다.
*  사용자 정의 변환을 제외 하 고 변환에서 존재 하지 않습니다 `S` 하 `T` 주고 `T` 에 `S`합니다.

이러한 규칙에서는 모든 입력 매개 변수 연관 `S` 또는 `T` 상속 관계가 없는 다른 형식 사용 및 매개 변수는 무시 됩니다. 해당 형식에 모든 제약 조건이 있는 고유 형식으로 간주 됩니다.

예제
```csharp
class C<T> {...}

class D<T>: C<T>
{
    public static implicit operator C<int>(D<T> value) {...}      // Ok
    public static implicit operator C<string>(D<T> value) {...}   // Ok
    public static implicit operator C<T>(D<T> value) {...}        // Error
}
```
첫 번째 두 연산자 선언 되기 때문에 허용 됩니다의 목적 [인덱서](classes.md#indexers).3 `T` 하 고 `int` 및 `string` 각각에 없는 관계를 사용 하 여 고유 형식으로 간주 됩니다. 그러나 세 번째 연산자 이므로 오류로 `C<T>` 의 기본 클래스인 `D<T>`합니다.

두 번째 규칙에서 변환 연산자 또는 연산자가 선언 된 클래스 또는 구조체 형식에서 변환 해야 합니다. 예를 들어 있기 클래스 또는 구조체 형식에 대 한 `C` 에서 변환을 정의 하 고 `C` 를 `int` 들어오고 `int` 에 `C`, 아닌 `int` 를 `bool`.

직접 미리 정의 된 변환이 다시 정의 하는 것이 불가능 합니다. 따라서 변환 연산자는에서 변환할 수 없습니다 `object` 암시적 변환과 명시적 변환 간에 이미 존재 하므로 `object` 및 기타 모든 형식. 마찬가지로, 원본이 나 변환의 대상 형식 수 있습니다 다른 기본 형식 이므로 변환이 없습니다.

그러나 연산자를 지정 하는, 특정 형식 인수에 대해 변환이 이미 존재 하는 미리 정의 된 변환으로 제네릭 형식으로 선언 하는 것이 같습니다. 예제
```csharp
struct Convertible<T>
{
    public static implicit operator Convertible<T>(T value) {...}
    public static explicit operator T(Convertible<T> value) {...}
}
```
입력할 때 `object` 에 대 한 형식 인수로 지정 된 `T`, 두 번째 연산자는 이미 존재 하는 변환을 선언 (암시적, 및도 명시적, 형식 모두에서 변환이 존재 `object`).

두 형식 간에 미리 정의 된 변환이 있는 경우에는 해당 형식 간의 모든 사용자 정의 변환은 무시 됩니다. 구체적으로는 다음과 같습니다.

*  미리 정의 된 암시적 변환 경우 ([암시적 변환을](conversions.md#implicit-conversions)) 형식에서 존재 `S` 형식으로 `T`, 모든 사용자 정의 변환 (암시적 또는 명시적)에서 `S` 에 `T` 무시 됩니다.
*  미리 정의 된 명시적 변환 경우 ([명시적 변환](conversions.md#explicit-conversions)) 형식에서 존재 `S` 형식으로 `T`, 모든 사용자 정의 명시적 변환에서 `S` 에 `T` 무시 됩니다. 또한:

하는 경우 `T` 로 암시적으로 사용자 정의 인터페이스 형식 이므로 `S` 에 `T` 무시 됩니다.

로 암시적으로, 사용자 정의 그렇지 `S` 에 `T` 여전히 것으로 간주 됩니다.

모든 형식에 대 한 하지만 `object`, 연산자를 선언 하 여는 `Convertible<T>` 미리 정의 된 변환이 있는 형식 위의 충돌 하지 않습니다. 예를 들어:
```csharp
void F(int i, Convertible<int> n) {
    i = n;                          // Error
    i = (int)n;                     // User-defined explicit conversion
    n = i;                          // User-defined implicit conversion
    n = (Convertible<int>)i;        // User-defined implicit conversion
}
```

그러나 형식에 대 한 `object`, 미리 정의 된 변환의 모든 경우 사용할 수 있지만 사용자 정의 변환을 숨기기:

```csharp
void F(object o, Convertible<object> n) {
    o = n;                         // Pre-defined boxing conversion
    o = (object)n;                 // Pre-defined boxing conversion
    n = o;                         // User-defined implicit conversion
    n = (Convertible<object>)o;    // Pre-defined unboxing conversion
}
```

변환할 사용자 정의 변환은 허용 되지 않습니다 *interface_type*s입니다. 특히,이 제한 하면 사용자 정의 변환 하지 않고도 변환할 때 발생 하는 *interface_type*, 및 변환할은 *interface_type* 경우에 성공 개체 지정 된 구현 실제로 변환할 *interface_type*합니다.

변환 연산자의 서명이 소스 형식과 대상 유형으로 구성 됩니다. (이 유일한 형태의 멤버는 반환 형식 서명에서 참여 note 합니다.) 합니다 `implicit` 또는 `explicit` 변환 연산자의 분류 운영자의 서명의 일부가 아닙니다. 즉, 클래스 또는 구조체를 선언할 수 없습니다. 둘 다를 `implicit` 및 `explicit` 동일한 원본 및 대상 형식 사용 하 여 변환 연산자입니다.

일반적으로 암시적 변환은 사용자 정의 예외를 throw 하지 않는 및 정보가 손실 되지 않도록 설계 되어야 합니다. 사용자 정의 변환이 발생할 수 있습니다 예외 (예를 들어 있으므로 원본 인수가 범위를 벗어났습니다.) 또는 손실 정보 (예: 상위 비트가 삭제)을 해당 변환으로 변환 하는 명시적 변환을 정의 되어야 합니다.

예제
```csharp
using System;

public struct Digit
{
    byte value;

    public Digit(byte value) {
        if (value < 0 || value > 9) throw new ArgumentException();
        this.value = value;
    }

    public static implicit operator byte(Digit d) {
        return d.value;
    }

    public static explicit operator Digit(byte b) {
        return new Digit(b);
    }
}
```
변환 `Digit` 를 `byte` 되지 예외를 throw 하거나 내용은 있지만 손실 때문에 암시적 `byte` 하 `Digit` 은 이후 명시적 `Digit` 가능한 하위 집합을 나타낼 수 있습니다 값을 `byte`입니다.

## <a name="instance-constructors"></a>인스턴스 생성자

***인스턴스 생성자***는 클래스의 인스턴스를 초기화하는 데 필요한 작업을 구현하는 멤버입니다. 인스턴스 생성자를 사용 하 여 선언 된 *constructor_declaration*s:

```antlr
constructor_declaration
    : attributes? constructor_modifier* constructor_declarator constructor_body
    ;

constructor_modifier
    : 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'extern'
    | constructor_modifier_unsafe
    ;

constructor_declarator
    : identifier '(' formal_parameter_list? ')' constructor_initializer?
    ;

constructor_initializer
    : ':' 'base' '(' argument_list? ')'
    | ':' 'this' '(' argument_list? ')'
    ;

constructor_body
    : block
    | ';'
    ;
```

A *constructor_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)), 네 가지 액세스 한정자의 유효한 조합이 ([액세스 한정자 ](classes.md#access-modifiers)), 및 `extern` ([외부 메서드](classes.md#external-methods)) 한정자. 생성자 선언 여러 번 같은 한정자를 포함 하도록 허용 되지 않습니다.

합니다 *식별자* 의 한 *constructor_declarator* 인스턴스 생성자 선언 되는 클래스 이름을 지정 해야 합니다. 다른 이름을 지정 하는 경우 컴파일 타임 오류가 발생 합니다.

선택적 *formal_parameter_list* 인스턴스의 생성자가 동일한 규칙을 적용 합니다 *formal_parameter_list* 메서드 ([메서드](classes.md#methods)). 시그니처를 정의 하는 정식 매개 변수 목록 ([시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading)) 인스턴스 생성자의 프로세스를 여기서 제어 및 오버 로드 확인 ([형식 유추](expressions.md#type-inference)) 특정 선택 인스턴스 생성자를 호출에서 합니다.

참조 되는 형식의 각 합니다 *formal_parameter_list* 인스턴스의 생성자 적어도 생성자 자체 수준 만큼 액세스 가능 해야 ([내게 필요한 옵션의 제약 조건](basic-concepts.md#accessibility-constraints)).

선택적 *constructor_initializer* 호출에 지정 된 문을 실행 하기 전에 다른 인스턴스 생성자를 지정 합니다 *constructor_body* 이 인스턴스 생성자입니다. 이에서 더 자세히 설명 [생성자 이니셜라이저](classes.md#constructor-initializers)합니다.

생성자 선언에 포함 되어는 `extern` 한정자를 생성자 라고는 ***외부 생성자***합니다. 외부 생성자 선언에는 실제 구현을 제공 하기 때문에 해당 *constructor_body* 세미콜론으로 구성 됩니다. 다른 모든 생성자는 *constructor_body* 이루어져를 *블록* 클래스의 새 인스턴스를 초기화 하는 문을 지정 하는 합니다. 이 예제는 다음과 같습니다 합니다 *블록* 사용 하 여 인스턴스 메서드는 `void` 반환 형식 ([메서드 본문](classes.md#method-body)).

인스턴스 생성자 상속 되지 않습니다. 따라서 클래스 인스턴스 생성자가 없는 클래스에서 실제로 선언 이외의 합니다. 기본 생성자가 자동으로 제공 클래스에 인스턴스 생성자 선언이 없는 경우 ([기본 생성자](classes.md#default-constructors)).

인스턴스 생성자는 호출한 *object_creation_expression*s ([개체 만들기 식](expressions.md#object-creation-expressions)) 및 *constructor_initializer*s입니다.

### <a name="constructor-initializers"></a>생성자 이니셜라이저

모든 인스턴스 생성자 (클래스에 대 한 파일을 제외한 `object`) 암시적으로 바로 앞의 다른 인스턴스 생성자 호출을 포함 합니다 *constructor_body*합니다. 암시적으로 호출할 생성자에 의해 결정 됩니다 합니다 *constructor_initializer*:

*  형식의 인스턴스 생성자 이니셜라이저 `base(argument_list)` 또는 `base()` 에서 호출할 직접 기본 클래스는 인스턴스 생성자를 사용 하면 됩니다. 해당 생성자를 사용 하 여 선택 *argument_list* 하는 경우 표시 되 고의 오버 로드 확인 규칙 [오버 로드 확인](expressions.md#overload-resolution)합니다. 기본 생성자를 직접 기본 클래스에 포함 된 모든 액세스 가능한 인스턴스 생성자의 후보 인스턴스 생성자를 집합으로 구성 됩니다 ([기본 생성자](classes.md#default-constructors)) 없는 인스턴스 생성자에 선언 된 경우는 직접 기본 클래스입니다. 이 집합이 비어 있는 경우 또는 단일 최상의 인스턴스 생성자를 식별할 수 없는 경우 컴파일 타임 오류가 발생 합니다.
*  형식의 인스턴스 생성자 이니셜라이저 `this(argument-list)` 또는 `this()` 호출할 자체 클래스에서 인스턴스 생성자를 사용 하면 됩니다. 생성자를 사용 하 여 선택 *argument_list* 하는 경우 표시 되 고의 오버 로드 확인 규칙 [오버 로드 확인](expressions.md#overload-resolution)합니다. 자체 클래스에서 선언 하는 모든 가능한 인스턴스 생성자의 후보 인스턴스 생성자의 집합이 구성 됩니다. 이 집합이 비어 있는 경우 또는 단일 최상의 인스턴스 생성자를 식별할 수 없는 경우 컴파일 타임 오류가 발생 합니다. 인스턴스 생성자 선언 자체 생성자를 호출 하는 생성자 이니셜라이저를 포함 하는 경우 컴파일 타임 오류가 발생 합니다.

인스턴스 생성자에 폼의 생성자 이니셜라이저가 생성자 이니셜라이저가 없기 경우 `base()` 암시적으로 제공 됩니다. 따라서 형식의 인스턴스 생성자 선언
```csharp
C(...) {...}
```
동일
```csharp
C(...): base() {...}
```

제공한 매개 변수의 범위는 *formal_parameter_list* 선언 인스턴스 생성자의 해당 선언의 생성자 이니셜라이저를 포함 합니다. 따라서 생성자 이니셜라이저는 생성자의 매개 변수에 액세스 하도록 허용 됩니다. 예를 들어:
```csharp
class A
{
    public A(int x, int y) {}
}

class B: A
{
    public B(int x, int y): base(x + y, x - y) {}
}
```

인스턴스 생성자 이니셜라이저는 생성 되는 인스턴스를 액세스할 수 없습니다. 따라서 컴파일 타임 오류를 참조 하는 것 `this` 생성자 이니셜라이저 인수 식에서으로 것을 통해 인스턴스 멤버를 참조 하는 인수 식에 대 한 컴파일 시간 오류를 *simple_name*.

### <a name="instance-variable-initializers"></a>인스턴스 변수 이니셜라이저

경우는 인스턴스 생성자가 없는 생성자 이니셜라이저 또는 폼의 생성자 이니셜라이저가 `base(...)`, 해당 생성자에서 지정 된 초기화를 암시적으로 수행 합니다 *variable_initializer*의 인스턴스 필드는 해당 클래스에 선언 합니다. 이 항목의 생성자를 직접 기본 클래스 생성자가 암시적으로 호출 하기 전에 바로 실행 되는 할당의 시퀀스에 해당 합니다. 변수 이니셜라이저는 클래스 선언에 나타나는 텍스트 순서 대로 실행 됩니다.

### <a name="constructor-execution"></a>생성자 실행

변수 이니셜라이저는 대입문, 변환 및 이러한 대입문 기본 클래스 인스턴스 생성자가 호출 되기 전에 실행 됩니다. 이렇게 순서를 지정 하면 해당 인스턴스에 액세스할 수 있는 모든 문이 실행 되기 전에 모든 인스턴스 필드가 해당 변수 이니셜라이저에 의해 초기화 됩니다.

예제를 제공합니다.
```csharp
using System;

class A
{
    public A() {
        PrintFields();
    }

    public virtual void PrintFields() {}
}

class B: A
{
    int x = 1;
    int y;

    public B() {
        y = -1;
    }

    public override void PrintFields() {
        Console.WriteLine("x = {0}, y = {1}", x, y);
    }
}
```
때 `new B()` 의 인스턴스를 만드는 데 사용 됩니다 `B`에 다음 출력이 생성 됩니다.
```
x = 1, y = 0
```

변수의 `x` 1 이므로 변수 이니셜라이저에서 예외는 기본 클래스 인스턴스 생성자가 호출 되기 전에 실행 됩니다. 그러나 값 `y` 은 0 (기본값은 `int`) 때문에 할당 하는 `y` 기본 클래스 생성자는 반환 될 때까지 실행 되지 않습니다.

인스턴스 변수 이니셜라이저 및 생성자 이니셜라이저 하기 전에 자동으로 삽입 되는 명령문으로 생각 하는 것이 유용 합니다 *constructor_body*합니다. 이 예제에서
```csharp
using System;
using System.Collections;

class A
{
    int x = 1, y = -1, count;

    public A() {
        count = 0;
    }

    public A(int n) {
        count = n;
    }
}

class B: A
{
    double sqrt2 = Math.Sqrt(2.0);
    ArrayList items = new ArrayList(100);
    int max;

    public B(): this(100) {
        items.Add("default");
    }

    public B(int n): base(n - 1) {
        max = n;
    }
}
```
여러 변수 이니셜라이저를 포함합니다. 두 형태 모두의 생성자 이니셜라이저 포함 (`base` 고 `this`). 예제 코드에 해당 하는 아래에 나와 있는 경우 각 주석 (자동으로 삽입 된 생성자 호출에 사용 되는 구문은 유효 하지 않으면 하지만 으로만 작동 하는 메커니즘을 설명 하기 위해)를 자동으로 삽입 된 문을 나타냅니다.

```csharp
using System.Collections;

class A
{
    int x, y, count;

    public A() {
        x = 1;                       // Variable initializer
        y = -1;                      // Variable initializer
        object();                    // Invoke object() constructor
        count = 0;
    }

    public A(int n) {
        x = 1;                       // Variable initializer
        y = -1;                      // Variable initializer
        object();                    // Invoke object() constructor
        count = n;
    }
}

class B: A
{
    double sqrt2;
    ArrayList items;
    int max;

    public B(): this(100) {
        B(100);                      // Invoke B(int) constructor
        items.Add("default");
    }

    public B(int n): base(n - 1) {
        sqrt2 = Math.Sqrt(2.0);      // Variable initializer
        items = new ArrayList(100);  // Variable initializer
        A(n - 1);                    // Invoke A(int) constructor
        max = n;
    }
}
```

### <a name="default-constructors"></a>기본 생성자

클래스에 인스턴스 생성자 선언이 없는 경우 기본 인스턴스 생성자를 자동으로 제공 됩니다. 해당 기본 생성자는 단순히 직접 기본 클래스의 매개 변수가 없는 생성자를 호출합니다. 클래스는 추상 선언 된 접근성이 기본 생성자에 대 한 보호 됩니다. 그렇지 않으면 선언 된 접근성이 기본 생성자는 공용입니다. 따라서 기본 생성자는 항상

```csharp
protected C(): base() {}
```
또는
```csharp
public C(): base() {}
```
여기서 `C` 클래스의 이름입니다. 오버 로드 확인에 기본 클래스 생성자 이니셜라이저에 대 한 고유 최상의 후보를 확인할 수 없는 경우 컴파일 타임 오류가 발생 합니다.

예제
```csharp
class Message
{
    object sender;
    string text;
}
```
기본 생성자를 클래스에 인스턴스 생성자 선언이 없으면 때문에 제공 됩니다. 따라서이 예제는 동일 합니다.
```csharp
class Message
{
    object sender;
    string text;

    public Message(): base() {}
}
```

### <a name="private-constructors"></a>Private 생성자

때 클래스 `T` 만 개인 인스턴스 생성자를 선언, 외부의 프로그램 텍스트 클래스에 대 한 불가능 `T` 에서 파생 시키는 `T` 의 인스턴스를 직접 만들려면 `T`합니다. 따라서 클래스 정적 멤버만 포함 하 고 인스턴스화할 수 없습니다, 하는 경우 개인 빈 인스턴스 생성자를 추가 인스턴스화가 되지 것입니다. 예를 들어:
```csharp
public class Trig
{
    private Trig() {}        // Prevent instantiation

    public const double PI = 3.14159265358979323846;

    public static double Sin(double x) {...}
    public static double Cos(double x) {...}
    public static double Tan(double x) {...}
}
```

`Trig` 클래스 관련 메서드와 상수가, 그룹을 수행 하지만 인스턴스화할 수 없습니다. 따라서 단일 빈 개인 인스턴스 생성자를 선언합니다. 기본 생성자를 자동으로 생성 하지 않으려면 하나 이상의 인스턴스 생성자를 선언 되어야 합니다.

### <a name="optional-instance-constructor-parameters"></a>선택적 인스턴스 생성자 매개 변수

`this(...)` 형식의 생성자 이니셜라이저는 대개 오버 로드와 함께에서 선택적 인스턴스 생성자 매개 변수를 구현 합니다. 예제
```csharp
class Text
{
    public Text(): this(0, 0, null) {}

    public Text(int x, int y): this(x, y, null) {}

    public Text(int x, int y, string s) {
        // Actual constructor implementation
    }
}
```
첫 번째 두 개의 인스턴스 생성자는 단순히 누락 된 인수에 대 한 기본 값을 제공합니다. 둘 다 사용을 `this(...)` 실제로 새 인스턴스를 초기화 하는 작업을 수행 하는 세 번째 인스턴스 생성자를 호출 하는 생성자 이니셜라이저입니다. 효과 사용 하면 선택적 생성자 매개 변수는 다음과 같습니다.
```csharp
Text t1 = new Text();                    // Same as Text(0, 0, null)
Text t2 = new Text(5, 10);               // Same as Text(5, 10, null)
Text t3 = new Text(5, 20, "Hello");
```

## <a name="static-constructors"></a>정적 생성자

A ***정적 생성자*** 는 닫힌된 클래스 형식을 초기화 하는 데 필요한 작업을 구현 하는 멤버입니다. 정적 생성자를 사용 하 여 선언 된 *static_constructor_declaration*s:

```antlr
static_constructor_declaration
    : attributes? static_constructor_modifiers identifier '(' ')' static_constructor_body
    ;

static_constructor_modifiers
    : 'extern'? 'static'
    | 'static' 'extern'?
    | static_constructor_modifiers_unsafe
    ;

static_constructor_body
    : block
    | ';'
    ;
```

A *static_constructor_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)) 및 `extern` 한정자 ([외부메서드](classes.md#external-methods)).

합니다 *식별자* 의 한 *static_constructor_declaration* 정적 생성자 선언 되는 클래스 이름을 지정 해야 합니다. 다른 이름을 지정 하는 경우 컴파일 타임 오류가 발생 합니다.

정적 생성자 선언에 포함 되어는 `extern` 한정자를 정적 생성자를 라고는 ***외부 정적 생성자***합니다. 외부 정적 생성자 선언에는 실제 구현을 제공 하기 때문에 해당 *static_constructor_body* 세미콜론으로 구성 됩니다. 다른 모든 정적 생성자 선언에 대 한 합니다 *static_constructor_body* 이루어져를 *블록* 클래스를 초기화 하기 위해 실행할 문을 지정 하는 합니다. 이 예제는 다음과 같습니다 합니다 *method_body* 사용 하 여 정적 메서드는 `void` 반환 형식 ([메서드 본문](classes.md#method-body)).

정적 생성자는 상속 되지 않으며 직접 호출할 수 없습니다.

닫힌된 클래스 형식에 대 한 정적 생성자는 지정 된 응용 프로그램 도메인에서 한 번만 실행합니다. 정적 생성자의 실행은 다음 이벤트 중 첫 번째 응용 프로그램 도메인 내에서 발생 하 여 트리거됩니다.

*  클래스 형식의 인스턴스가 만들어집니다.
*  클래스 형식의 정적 멤버가 참조 됩니다.

클래스를 포함 하는 경우는 `Main` 메서드 ([응용 프로그램 시작](basic-concepts.md#application-startup))에 실행이 시작 정적 생성자 보다 먼저 실행 되는 클래스에 대 한는 `Main` 메서드가 호출 됩니다.

새 닫힌된 클래스 형식에 정적 필드의 새 집합을 먼저 초기화 ([정적 및 인스턴스 필드](classes.md#static-and-instance-fields))에 해당 특정 닫힌된 유형이 만들어집니다. 각 정적 필드를 기본값으로 초기화 됩니다 ([기본값](variables.md#default-values)). 다음으로 정적 필드 이니셜라이저 ([정적 필드 초기화](classes.md#static-field-initialization)) 정적 필드에 대해 실행 됩니다. 마지막으로, 정적 생성자가 실행 됩니다.

이 예제에서
```csharp
using System;

class Test
{
    static void Main() {
        A.F();
        B.F();
    }
}

class A
{
    static A() {
        Console.WriteLine("Init A");
    }
    public static void F() {
        Console.WriteLine("A.F");
    }
}

class B
{
    static B() {
        Console.WriteLine("Init B");
    }
    public static void F() {
        Console.WriteLine("B.F");
    }
}
```
출력을 생성 해야 합니다.
```
Init A
A.F
Init B
B.F
```
때문에 실행 `A`의 정적 생성자에 대 한 호출에 의해 트리거되면 `A.F`, 및 실행 `B`의 정적 생성자에 대 한 호출에 의해 트리거되는 `B.F`합니다.

기본값 상태로 사용 되는 변수 이니셜라이저를 사용 하 여 정적 필드를 허용 하는 순환 종속성을 생성 하는 것이 가능 합니다.

이 예제에서
```csharp
using System;

class A
{
    public static int X;

    static A() {
        X = B.Y + 1;
    }
}

class B
{
    public static int Y = A.X + 1;

    static B() {}

    static void Main() {
        Console.WriteLine("X = {0}, Y = {1}", A.X, B.Y);
    }
}
```
는 출력을 생성합니다.
```
X = 1, Y = 2
```

실행 하는 `Main` 메서드를 시스템에 대 한 이니셜라이저 처음 실행할 `B.Y`클래스에 이전, `B`의 정적 생성자입니다. `Y`이니셜라이저에서 `A`의 때문에 실행 하는 정적 생성자의 값 `A.X` 참조 됩니다. 정적 생성자 `A` 의 값을 계산 차례로 진행 `X`, 있으며 따라서 인출의 기본 값 `Y`, 0 인 합니다. `A.X` 1로 초기화 되므로 됩니다. 실행의 프로세스 `A`정적 필드 이니셜라이저 및 정적 생성자의 다음 완료 되 면의 초기 값을 계산 하려면 반환 `Y`, 결과 2가 됩니다.

정적 생성자가 각 폐쇄형 생성 된 클래스 형식에 대 한 정확히 한 번 실행, 이므로 제약 조건을 통해 컴파일 타임에 검사할 수 없습니다. 형식 매개 변수에 대 한 런타임 검사를 적용 하는 데 편리한 위치 ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)). 예를 들어, 다음과 같은 형식이 열거형 형식 인수는 적용할 정적 생성자를 사용 합니다.
```csharp
class Gen<T> where T: struct
{
    static Gen() {
        if (!typeof(T).IsEnum) {
            throw new ArgumentException("T must be an enum");
        }
    }
}
```

## <a name="destructors"></a>소멸자

A ***소멸자*** 는 클래스의 인스턴스를 소멸 하는 데 필요한 작업을 구현 하는 멤버입니다. 소멸자를 사용 하 여 선언 되는 *destructor_declaration*:

```antlr
destructor_declaration
    : attributes? 'extern'? '~' identifier '(' ')' destructor_body
    | destructor_declaration_unsafe
    ;

destructor_body
    : block
    | ';'
    ;
```

A *destructor_declaration* 집합이 포함 될 수 있습니다 *특성* ([특성](attributes.md)).

합니다 *식별자* 의 한 *destructor_declaration* 소멸자가 선언 되는 클래스 이름을 지정 해야 합니다. 다른 이름을 지정 하는 경우 컴파일 타임 오류가 발생 합니다.

소멸자 선언 포함 되는 경우는 `extern` 한정자를 소멸자를 라고는 ***외부 소멸자***합니다. 외부 소멸자 선언은 실제 구현을 제공 하기 때문에 해당 *destructor_body* 세미콜론으로 구성 됩니다. 다른 모든 소멸자에 대 한 합니다 *destructor_body* 이루어져를 *블록* 클래스의 인스턴스를 소멸 하기 위해 실행할 문을 지정 하는 합니다. A *destructor_body* 정확 하 게 일치 합니다 *method_body* 사용 하 여 인스턴스 메서드를 `void` 반환 형식 ([메서드 본문](classes.md#method-body)).

소멸자는 상속 되지 않습니다. 따라서 클래스에는 해당 클래스에서 선언 될 수 있는 것 이외의 없는 소멸자

소멸자를 매개 변수가 없어야 하는 데 필요 하므로 클래스를 가질 수 있도록, 최대, 소멸자가 하나씩 오버 로드 일 수 없습니다.

소멸자는 자동으로 호출 및 명시적으로 호출할 수 없습니다. 더 이상 해당 인스턴스를 사용 하는 코드에 대 한 가능한 경우 인스턴스를 소멸 대상이 됩니다. 실행 인스턴스에 대 한 소멸자의 인스턴스를 소멸할 수 있게 되 면 언제 발생할 수 있습니다. 순서로 해당 인스턴스의 상속 체인의 소멸자가 호출 된 인스턴스는 소멸 됩니다을 하는 경우 가장 많이 파생 이상 파생 합니다. 소멸자는 모든 스레드에서 실행할 수 있습니다. 에 대 한 자세한 설명은 시기 및 소멸자가 실행 되는 방식을 제어 하는 규칙을 참조 하세요 [자동 메모리 관리](basic-concepts.md#automatic-memory-management)합니다.

예제의 출력
```csharp
using System;

class A
{
    ~A() {
        Console.WriteLine("A's destructor");
    }
}

class B: A
{
    ~B() {
        Console.WriteLine("B's destructor");
    }
}

class Test
{
   static void Main() {
        B b = new B();
        b = null;
        GC.Collect();
        GC.WaitForPendingFinalizers();
   }
}
```
is
```
B's destructor
A's destructor
```
순서 대로 상속 체인의 소멸자가 호출 되므로 가장 많이 파생 이상 파생 합니다.

소멸자는 가상 메서드를 재정의 하 여 구현 됩니다 `Finalize` 에서 `System.Object`합니다. 이 메서드를 재정의 하거나 (또는 해당 재정의)를 호출 하는 C# 프로그램 허용 되지 않습니다 직접. 예를 들어 프로그램
```csharp
class A 
{
    override protected void Finalize() {}    // error

    public void F() {
        this.Finalize();                     // error
    }
}
```
두 가지 오류를 포함합니다.

컴파일러는이 메서드를 재정의 하지만 전혀 존재 하지 않는 경우에 따라 동작 합니다. 따라서이 프로그램:
```csharp
class A 
{
    void Finalize() {}                            // permitted
}
```
유효 하면 메서드가 표시 숨깁니다 `System.Object`의 `Finalize` 메서드.

동작의 소멸자에서 예외가 throw 되 면 참조 [예외를 처리 하는 방법을](exceptions.md#how-exceptions-are-handled)합니다.

## <a name="iterators"></a>반복기

함수 멤버 ([멤버 함수](expressions.md#function-members))은 반복기 블록이 사용 하 여 구현 ([블록](statements.md#blocks)) 호출 되는 ***반복기***합니다.

반복기 블록이 해당 하는 함수 멤버의 반환 형식 열거자 인터페이스 중 하나는 함수 멤버의 본문으로 사용할 수 있습니다 ([열거자 인터페이스](classes.md#enumerator-interfaces)) 또는 열거 가능 인터페이스 중 하나 ([열거 가능 인터페이스](classes.md#enumerable-interfaces)). 으로 발생할 수 있습니다는 *method_body*를 *operator_body* 하거나 *accessor_body*반면 이벤트, 인스턴스 생성자, 정적 생성자 및 소멸자 수 없습니다 반복기로 구현 됩니다.

정식 매개 변수 목록 지정 하는 함수 멤버에 대 한 컴파일 시간 오류 것은 반복기 블록이 사용 하 여 함수 멤버 구현 될 때 `ref` 또는 `out` 매개 변수입니다.

### <a name="enumerator-interfaces"></a>열거자 인터페이스

합니다 ***열거자 인터페이스*** 제네릭이 아닌 인터페이스는 `System.Collections.IEnumerator` 및 제네릭 인터페이스의 모든 인스턴스화에 `System.Collections.Generic.IEnumerator<T>`합니다. 간단히 하기 위해이 챕터에 이러한 인터페이스 라고 `IEnumerator` 고 `IEnumerator<T>`, 각각.

### <a name="enumerable-interfaces"></a>열거 가능 인터페이스

합니다 ***열거 가능 인터페이스*** 제네릭이 아닌 인터페이스는 `System.Collections.IEnumerable` 및 제네릭 인터페이스의 모든 인스턴스화에 `System.Collections.Generic.IEnumerable<T>`합니다. 간단히 하기 위해이 챕터에 이러한 인터페이스 라고 `IEnumerable` 고 `IEnumerable<T>`, 각각.

### <a name="yield-type"></a>형식 생성

동일한 형식의 모든 값의 시퀀스를 생성 하는 반복기입니다. 이 형식 이라고 합니다 ***형식을 생성*** 반복기의 합니다.

*  반환 하는 반복기는 yield 유형의 `IEnumerator` 나 `IEnumerable` 는 `object`합니다.
*  반환 하는 반복기는 yield 유형의 `IEnumerator<T>` 나 `IEnumerable<T>` 는 `T`합니다.

### <a name="enumerator-objects"></a>열거자 개체

인터페이스 형식 열거자를 반환 합니다. 함수 멤버 반복기 블록을 사용 하 여 구현 될 때 호출 하는 함수 멤버 실행 되지 않습니다 즉시 코드 반복기 블록에서. 대신에 ***열거자 개체*** 가 만들어져 반환 합니다. 반복기 블록에 지정 된 코드를 캡슐화 하는이 개체 및 반복기 블록에서 코드의 실행이 발생 하는 경우 열거자 개체의 `MoveNext` 메서드가 실행 됩니다. 열거자 개체에는 다음과 같은 특징이 있습니다.

*  구현 `IEnumerator` 하 고 `IEnumerator<T>`여기서 `T` 반복기의 yield 유형입니다.
*  `System.IDisposable`을 구현합니다.
*  인수 값의 복사본으로 초기화 됩니다 (있는 경우) 및 함수 멤버에 전달 된 인스턴스 값입니다.
*  네 가지 상태만 있기 ***하기 전에***, ***실행***를 ***일시 중단***, 및 ***후***, 처음부터 및는 ***하기 전에***  상태입니다.

열거자 개체는 일반적으로 반복기 블록에서 코드를 캡슐화 하 고 열거자 인터페이스를 구현 하는 열거자 컴파일러에서 생성 된 클래스의 인스턴스 되지만 다른 메서드 구현 가능 합니다. 열거자 클래스는 컴파일러에서 생성 되 면 해당 클래스를 중첩할 수는, 직접 또는 간접적으로 함수 멤버를 포함 하는 클래스에서 private 액세스 가능성이 더 및 컴파일러 사용 하도록 예약 된 이름을 가진 것 ([식별자 ](lexical-structure.md#identifiers)).

열거자 개체 위에 지정 된 것 보다 더 많은 인터페이스를 구현할 수 있습니다.

정확한 동작을 설명 하는 다음 섹션에서는 합니다 `MoveNext`, `Current`, 및 `Dispose` 의 멤버는 `IEnumerable` 및 `IEnumerable<T>` 인터페이스 구현을 열거자 개체에 의해 제공 합니다.

열거자 개체를 지원 하지 않습니다는 `IEnumerator.Reset` 메서드. 이 메서드를 호출 하면를 `System.NotSupportedException` throw 됩니다.

#### <a name="the-movenext-method"></a>MoveNext 메서드

`MoveNext` 열거자 개체의 메서드를 반복기 블록의 코드를 캡슐화 합니다. 호출 된 `MoveNext` 집합과 반복기 블록에서 코드를 실행 하는 메서드를 `Current` 적절 하 게 열거자 개체의 속성입니다. 수행한 작업을 정확히 `MoveNext` 열거자 개체의 상태에 따라 달라 집니다 때 `MoveNext` 가 호출 됩니다.

*  열거자 개체의 상태가 ***하기 전에***호출, `MoveNext`:
   * 상태를 변경 합니다 ***실행***합니다.
   * 매개 변수를 초기화 (포함 하 여 `this`) 인수 값 및 인스턴스 값 열거자 개체 초기화 될 때 저장 된 반복기 블록입니다.
   * (아래 설명 참조)으로 실행이 중단 될 때까지 반복기 블록 시작 부분에서 실행 합니다.
*  열거자 개체의 상태가 ***실행***를 호출한 결과로 `MoveNext` 지정 되지 않았습니다.
*  열거자 개체의 상태가 ***일시 중단***호출, `MoveNext`:
   * 상태를 변경 합니다 ***실행***합니다.
   * 반복기 블록의 실행이 일시 중단 된 마지막으로 저장 된 값으로 모든 지역 변수 및 매개 변수 (이 포함)의 값을 복원 합니다. Movenext 이전 호출 이후 변경 된 경우이 변수가 참조 하는 모든 개체의 내용을 참고 합니다.
   * 바로 다음 반복기 블록의 실행을 다시 시작을 `yield return` 문 실행의 일시 중단이 발생입니다 (아래 설명 참조)으로 실행이 중단 될 때까지 계속 됩니다.
*  열거자 개체의 상태가 ***한 후***, 호출 `MoveNext` 반환 `false`합니다.


때 `MoveNext` 반복기 블록을 실행 네 가지 방법으로 실행이 중단 될 수 있습니다: 여는 `yield return` 문는 `yield break` 문에서 발생 하는 반복기 블록의 끝에서 예외로 인해 throw 되 고 전파는 반복기 블록입니다.

*  경우는 `yield return` 문이 ([yield 문을](statements.md#the-yield-statement)):
   * 문에 지정 된 식 계산, 암시적으로 yield 형식으로 변환 되어에 할당 된 `Current` 열거자 개체의 속성입니다.
   * 반복기 본문의 실행을 일시 중단 됩니다. 모든 지역 변수 및 매개 변수의 값 (포함 `this`)이 위치를 그대로 저장 됩니다 `yield return` 문입니다. 경우는 `yield return` 문 내에서 하나 이상의 됩니다 `try` 연결 된 블록 `finally` 지금은 블록이 실행 되지 않습니다.
   * 열거자 개체의 상태가으로 변경 됩니다 ***일시 중단***합니다.
   * 합니다 `MoveNext` 메서드가 반환 되는 `true` 는 반복 성공적으로 이동 하는 데 다음 값을 나타내는 해당 호출자에 게 합니다.
*  경우는 `yield break` 문이 ([yield 문을](statements.md#the-yield-statement)):
   * 경우는 `yield break` 문 내에서 하나 이상의 됩니다 `try` 연결 된 블록 `finally` 블록이 실행 됩니다.
   * 열거자 개체의 상태가으로 변경 됩니다 ***후***합니다.
   * 합니다 `MoveNext` 메서드가 반환 되는 `false` 반복 완료 되었음을 나타내는 호출자로 합니다.
*  반복기 본문의 끝 발생 시:
   * 열거자 개체의 상태가으로 변경 됩니다 ***후***합니다.
   * 합니다 `MoveNext` 메서드가 반환 되는 `false` 반복 완료 되었음을 나타내는 호출자로 합니다.
*  예외가 throw 되 고 반복기 블록에서 전파 하면:
   * 적절 한 `finally` 반복기 본문의 요소는 예외 전파 하 여 실행 됩니다.
   * 열거자 개체의 상태가으로 변경 됩니다 ***후***합니다.
   * 호출자에 게 계속 예외 전파를 `MoveNext` 메서드.

#### <a name="the-current-property"></a>현재 속성

열거자 개체의 `Current` 속성은 영향을 받지 `yield return` 반복기 블록에서 문입니다.

열거자 개체의 경우는 ***일시 중단*** 상태, 값 `Current` 에 대 한 이전 호출에서 설정한 값은 `MoveNext`합니다. 열거자 개체의 경우는 ***하기 전에***를 ***실행***, 또는 ***후*** 상태를 결과 액세스 하는 `Current` 지정 되지 않았습니다.

Yield 사용 하는 반복기에 대 한 입력 이외의 `object`에 액세스 하는 결과 `Current` 열거자 개체를 통해 `IEnumerable` 구현에 액세스 하려면 해당 `Current` 열거자 개체를 통해 `IEnumerator<T>` 구현 및 결과를 캐스팅 `object`합니다.

#### <a name="the-dispose-method"></a>Dispose 메서드

`Dispose` 메서드를 사용는 열거자 개체를 가져와서 반복을 정리 합니다 ***후*** 상태입니다.

*  열거자 개체의 상태가 ***하기 전에***, 호출 `Dispose` 상태를 변경 합니다 ***후***합니다.
*  열거자 개체의 상태가 ***실행***를 호출한 결과로 `Dispose` 지정 되지 않았습니다.
*  열거자 개체의 상태가 ***일시 중단***호출, `Dispose`:
   * 상태를 변경 합니다 ***실행***합니다.
   * 실행 된 마지막 블록 마지막으로 실행 된 것 처럼 `yield return` 문이 된를 `yield break` 문입니다. 열거자 개체의 상태를로 예외를 throw 하 고 반복기 본문 밖으로 전파할 수 이면 ***한 후*** 예외를 호출자에 게 전파 되는 `Dispose` 메서드.
   * 상태를 변경 합니다 ***후***합니다.
*  열거자 개체의 상태가 ***한 후***호출, `Dispose` 영향을 주지 않습니다.

### <a name="enumerable-objects"></a>열거 가능한 개체

함수 멤버를 열거 가능한 인터페이스 형식을 반환은 반복기 블록이 사용 하 여 구현 될 때 호출 하는 함수 멤버 실행 되지 않습니다 즉시 코드 반복기 블록에서. 대신는 ***열거 가능한 개체*** 가 만들어져 반환 합니다. 열거 가능한 개체의 `GetEnumerator` 반환 반복기 블록에서 코드를 캡슐화 하는 열거자 개체를 지정 하 고 반복기 블록에서 코드의 실행이 발생 경우 열거자 개체의 `MoveNext` 메서드가 실행 됩니다. 열거 가능한 개체에는 다음과 같은 특징이 있습니다.

*  구현 `IEnumerable` 하 고 `IEnumerable<T>`여기서 `T` 반복기의 yield 유형입니다.
*  인수 값의 복사본으로 초기화 됩니다 (있는 경우) 및 함수 멤버에 전달 된 인스턴스 값입니다.

열거 가능한 개체는 일반적으로 반복기 블록에서 코드를 캡슐화 하 고 열거 가능한 인터페이스를 구현 하는 컴파일러에서 생성 된 enumerable 클래스의 인스턴스 되지만 다른 메서드 구현 가능 합니다. Enumerable 클래스는 컴파일러에서 생성 되 면 해당 클래스를 중첩할 수는, 직접 또는 간접적으로 함수 멤버를 포함 하는 클래스에서 private 액세스 가능성이 더 및 컴파일러 사용 하도록 예약 된 이름을 가진 것 ([식별자 ](lexical-structure.md#identifiers)).

열거 가능한 개체 위에 지정 된 것 보다 더 많은 인터페이스를 구현할 수 있습니다. 특히 열거 가능한 개체 구현할 수도 있습니다 `IEnumerator` 고 `IEnumerator<T>`, 열거 및 열거자로 제공할 수 있도록 합니다. 해당 형식의 구현, 처음 열거 가능한 개체의 `GetEnumerator` 메서드를 호출 하면 열거 가능한 개체 자체가 반환 됩니다. 열거 가능한 개체의 후속 호출 `GetEnumerator`이면 있는 열거 가능한 개체의 복사본을 반환 합니다. 따라서 반환 된 각 열거자에는 자체 상태 및 하나의 열거자에 대 한 변경 내용을 다른 레코드에 영향을 주지는 것입니다.

#### <a name="the-getenumerator-method"></a>GetEnumerator 메서드가

열거 가능한 개체의 구현을 제공 합니다 `GetEnumerator` 의 메서드를 `IEnumerable` 및 `IEnumerable<T>` 인터페이스입니다. 두 `GetEnumerator` 메서드 획득 하 고 사용할 수 있는 열거자 개체를 반환 하는 일반적인 구현을 공유 합니다. 열거자 개체 인수 값으로 초기화 되 고 인스턴스 열거 가능 개체를 초기화 하지만 그렇지 않으면 때 저장 된 값에 설명 된 대로 열거자 개체 함수 [열거자 개체](classes.md#enumerator-objects)합니다.

### <a name="implementation-example"></a>구현 예제

이 섹션에서는 표준 C# 구문 측면에서 반복기의 가능한 구현을 설명 합니다. 여기에 설명 된 구현은 Microsoft C# 컴파일러에 의해 사용 되는 동일한 원칙에 기반 하지만 위임된 구현 또는 하나의 가능한 되지는 않습니다.

다음 `Stack<T>` 구현 클래스는 `GetEnumerator` 반복기를 사용 하는 메서드. 위에서 아래 순 스택의의 요소를 열거 하는 반복기입니다.

```csharp
using System;
using System.Collections;
using System.Collections.Generic;

class Stack<T>: IEnumerable<T>
{
    T[] items;
    int count;

    public void Push(T item) {
        if (items == null) {
            items = new T[4];
        }
        else if (items.Length == count) {
            T[] newItems = new T[count * 2];
            Array.Copy(items, 0, newItems, 0, count);
            items = newItems;
        }
        items[count++] = item;
    }

    public T Pop() {
        T result = items[--count];
        items[count] = default(T);
        return result;
    }

    public IEnumerator<T> GetEnumerator() {
        for (int i = count - 1; i >= 0; --i) yield return items[i];
    }
}
```

`GetEnumerator` 메서드 다음에 표시 된 대로 반복기 블록에서 코드를 캡슐화 하는 열거자 컴파일러에서 생성 된 클래스의 인스턴스화로 변환할 수 있습니다.

```csharp
class Stack<T>: IEnumerable<T>
{
    ...

    public IEnumerator<T> GetEnumerator() {
        return new __Enumerator1(this);
    }

    class __Enumerator1: IEnumerator<T>, IEnumerator
    {
        int __state;
        T __current;
        Stack<T> __this;
        int i;

        public __Enumerator1(Stack<T> __this) {
            this.__this = __this;
        }

        public T Current {
            get { return __current; }
        }

        object IEnumerator.Current {
            get { return __current; }
        }

        public bool MoveNext() {
            switch (__state) {
                case 1: goto __state1;
                case 2: goto __state2;
            }
            i = __this.count - 1;
        __loop:
            if (i < 0) goto __state2;
            __current = __this.items[i];
            __state = 1;
            return true;
        __state1:
            --i;
            goto __loop;
        __state2:
            __state = 2;
            return false;
        }

        public void Dispose() {
            __state = 2;
        }

        void IEnumerator.Reset() {
            throw new NotSupportedException();
        }
    }
}
```

이전 번역을 반복기 블록에서 코드가 상태 시스템으로 설정 되 고 있는 `MoveNext` 열거자 클래스의 메서드. 또한 지역 변수 `i` 호출의 존재를 계속할 수 있도록 열거자 개체의 필드로 꺼져 `MoveNext`합니다.

다음 예제에서는 1부터 10 까지의 정수의 단순 곱셈표를 인쇄합니다. `FromTo` 예제의 메서드 열거 가능한 개체를 반환 하며 반복기를 사용 하 여 구현 됩니다.

```csharp
using System;
using System.Collections.Generic;

class Test
{
    static IEnumerable<int> FromTo(int from, int to) {
        while (from <= to) yield return from++;
    }

    static void Main() {
        IEnumerable<int> e = FromTo(1, 10);
        foreach (int x in e) {
            foreach (int y in e) {
                Console.Write("{0,3} ", x * y);
            }
            Console.WriteLine();
        }
    }
}
```

`FromTo` 메서드 다음에 표시 된 대로 반복기 블록에서 코드를 캡슐화 하는 컴파일러에서 생성 된 enumerable 클래스의 인스턴스화로 변환할 수 있습니다.

```csharp
using System;
using System.Threading;
using System.Collections;
using System.Collections.Generic;

class Test
{
    ...

    static IEnumerable<int> FromTo(int from, int to) {
        return new __Enumerable1(from, to);
    }

    class __Enumerable1:
        IEnumerable<int>, IEnumerable,
        IEnumerator<int>, IEnumerator
    {
        int __state;
        int __current;
        int __from;
        int from;
        int to;
        int i;

        public __Enumerable1(int __from, int to) {
            this.__from = __from;
            this.to = to;
        }

        public IEnumerator<int> GetEnumerator() {
            __Enumerable1 result = this;
            if (Interlocked.CompareExchange(ref __state, 1, 0) != 0) {
                result = new __Enumerable1(__from, to);
                result.__state = 1;
            }
            result.from = result.__from;
            return result;
        }

        IEnumerator IEnumerable.GetEnumerator() {
            return (IEnumerator)GetEnumerator();
        }

        public int Current {
            get { return __current; }
        }

        object IEnumerator.Current {
            get { return __current; }
        }

        public bool MoveNext() {
            switch (__state) {
            case 1:
                if (from > to) goto case 2;
                __current = from++;
                __state = 1;
                return true;
            case 2:
                __state = 2;
                return false;
            default:
                throw new InvalidOperationException();
            }
        }

        public void Dispose() {
            __state = 2;
        }

        void IEnumerator.Reset() {
            throw new NotSupportedException();
        }
    }
}
```

Enumerable 클래스는 열거 가능 인터페이스 및 열거자 인터페이스, 열거형 및 열거자로 제공할 수 있도록 구현 합니다. 처음으로 `GetEnumerator` 메서드를 호출 하면 열거 가능한 개체 자체가 반환 됩니다. 열거 가능한 개체의 후속 호출 `GetEnumerator`이면 있는 열거 가능한 개체의 복사본을 반환 합니다. 따라서 반환 된 각 열거자에는 자체 상태 및 하나의 열거자에 대 한 변경 내용을 다른 레코드에 영향을 주지는 것입니다. `Interlocked.CompareExchange` 스레드로부터 안전한 작업 메서드를 사용 합니다.

합니다 `from` 및 `to` 매개 변수는 enumerable 클래스의 필드로 설정 합니다. 때문에 `from` 은 추가 반복기 블록에서 수정할 `__from` 필드에 지정 된 초기 값을 저장 하기 위해 도입 되었습니다 `from` 각 열거자에 합니다.

합니다 `MoveNext` 메서드가 throw를 `InvalidOperationException` 때 호출 되 면 `__state` 는 `0`합니다. 이 첫 번째 호출 하지 않고 열거자 개체를 열거 가능한 개체의 사용을 방지 `GetEnumerator`합니다.

다음 예제에서는 간단한 트리에서 클래스를 보여 줍니다. 합니다 `Tree<T>` 구현 클래스 해당 `GetEnumerator` 반복기를 사용 하는 방법입니다. 반복기 중 위 순서로 트리의 요소를 열거 합니다.

```csharp
using System;
using System.Collections.Generic;

class Tree<T>: IEnumerable<T>
{
    T value;
    Tree<T> left;
    Tree<T> right;

    public Tree(T value, Tree<T> left, Tree<T> right) {
        this.value = value;
        this.left = left;
        this.right = right;
    }

    public IEnumerator<T> GetEnumerator() {
        if (left != null) foreach (T x in left) yield x;
        yield value;
        if (right != null) foreach (T x in right) yield x;
    }
}

class Program
{
    static Tree<T> MakeTree<T>(T[] items, int left, int right) {
        if (left > right) return null;
        int i = (left + right) / 2;
        return new Tree<T>(items[i], 
            MakeTree(items, left, i - 1),
            MakeTree(items, i + 1, right));
    }

    static Tree<T> MakeTree<T>(params T[] items) {
        return MakeTree(items, 0, items.Length - 1);
    }

    // The output of the program is:
    // 1 2 3 4 5 6 7 8 9
    // Mon Tue Wed Thu Fri Sat Sun

    static void Main() {
        Tree<int> ints = MakeTree(1, 2, 3, 4, 5, 6, 7, 8, 9);
        foreach (int i in ints) Console.Write("{0} ", i);
        Console.WriteLine();

        Tree<string> strings = MakeTree(
            "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun");
        foreach (string s in strings) Console.Write("{0} ", s);
        Console.WriteLine();
    }
}
```

`GetEnumerator` 메서드 다음에 표시 된 대로 반복기 블록에서 코드를 캡슐화 하는 열거자 컴파일러에서 생성 된 클래스의 인스턴스화로 변환할 수 있습니다.

```csharp
class Tree<T>: IEnumerable<T>
{
    ...

    public IEnumerator<T> GetEnumerator() {
        return new __Enumerator1(this);
    }

    class __Enumerator1 : IEnumerator<T>, IEnumerator
    {
        Node<T> __this;
        IEnumerator<T> __left, __right;
        int __state;
        T __current;

        public __Enumerator1(Node<T> __this) {
            this.__this = __this;
        }

        public T Current {
            get { return __current; }
        }

        object IEnumerator.Current {
            get { return __current; }
        }

        public bool MoveNext() {
            try {
                switch (__state) {

                case 0:
                    __state = -1;
                    if (__this.left == null) goto __yield_value;
                    __left = __this.left.GetEnumerator();
                    goto case 1;

                case 1:
                    __state = -2;
                    if (!__left.MoveNext()) goto __left_dispose;
                    __current = __left.Current;
                    __state = 1;
                    return true;

                __left_dispose:
                    __state = -1;
                    __left.Dispose();

                __yield_value:
                    __current = __this.value;
                    __state = 2;
                    return true;

                case 2:
                    __state = -1;
                    if (__this.right == null) goto __end;
                    __right = __this.right.GetEnumerator();
                    goto case 3;

                case 3:
                    __state = -3;
                    if (!__right.MoveNext()) goto __right_dispose;
                    __current = __right.Current;
                    __state = 3;
                    return true;

                __right_dispose:
                    __state = -1;
                    __right.Dispose();

                __end:
                    __state = 4;
                    break;

                }
            }
            finally {
                if (__state < 0) Dispose();
            }
            return false;
        }

        public void Dispose() {
            try {
                switch (__state) {

                case 1:
                case -2:
                    __left.Dispose();
                    break;

                case 3:
                case -3:
                    __right.Dispose();
                    break;

                }
            }
            finally {
                __state = 4;
            }
        }

        void IEnumerator.Reset() {
            throw new NotSupportedException();
        }
    }
}
```

에 사용 되는 컴파일러에서 생성 된 임시 개체는 `foreach` 로 문 리프팅되며 합니다 `__left` 및 `__right` 열거자 개체의 필드입니다. `__state` 열거자 개체의 필드 업데이트 신중 하 게 됩니다 있도록 올바른 `Dispose()` 메서드가 호출 됩니다 올바르게 경우 예외가 throw 됩니다. 간단한을 사용 하 여 번역 된 코드를 작성할 수는 `foreach` 문입니다.

## <a name="async-functions"></a>비동기 함수

메서드 ([메서드](classes.md#methods)) 또는 익명 함수 ([익명 함수 식](expressions.md#anonymous-function-expressions))으로 `async` 한정자 라고는 ***비동기 함수***합니다. 일반적으로 용어 ***비동기*** 모든 종류의 함수를 설명 하는 데 사용 되는 `async` 한정자입니다.

정식 매개 변수 목록 지정 하는 비동기 함수에 대 한 컴파일 타임 오류 `ref` 또는 `out` 매개 변수입니다.

합니다 *return_type* 의 비동기 메서드 중 하나 여야 합니다 `void` 또는 ***작업 종류***합니다. 작업 유형은 `System.Threading.Tasks.Task` 에서 생성 된 형식 및 `System.Threading.Tasks.Task<T>`합니다. 간단히 하기 위해이 챕터에 이러한 형식은 라고 `Task` 및 `Task<T>`, 각각. 작업 형식을 반환 비동기 메서드는 작업을 반환 하 라고 합니다.

작업 유형은의 정확한 정의 구현 정의 이지만 언어의 관점에서 작업 유형 성공 또는 오류가 발생 한 완료 되지 않은 상태 중 하나가 있습니다. 오류가 발생 한 작업 관련 예외를 기록합니다. 성공 `Task<T>` 형식의 결과 기록 `T`합니다. 작업 형식에는 대기 가능, 및의 피연산자가 될 수 있습니다 await 식 ([Await 식](expressions.md#await-expressions)).

비동기 함수 호출에 계산을 일시 중단 하는 기능 이용 하 여 await 식 ([Await 식](expressions.md#await-expressions)) 본문에 있습니다. 평가 될 수 있습니다 나중에 다시 시작할 일시 중단 된 시점에서 await 식 방법으로 ***다시 시작 대리자***합니다. 다시 시작 대리자 형식입니다 `System.Action`, 고 중단 된 await 식에서 비동기 함수 호출의 평가 다시 시작 됩니다 호출 되 면 합니다. 합니다 ***현재 호출자*** 비동기 함수의 호출 라인인 함수를 호출 하지 일시 중단 된 경우 원래 호출자 또는 다시 시작 대리자의 가장 최근 호출자입니다.

### <a name="evaluation-of-a-task-returning-async-function"></a>작업 반환 비동기 함수 계산

작업 반환 비동기 함수를 호출 하면 반환 된 작업 유형 생성할 인스턴스의 합니다. 이 호출 되는 ***task 반환*** 비동기 함수입니다. 작업이 처음에 불완전 한 상태입니다.

비동기 함수 본문은 다음 지점 제어 반환 함께 호출자에 게 반환 되는 중 (await 식에 도달)에 의해 일시 중단 또는 종료 될 때까지 계산 됩니다.

비동기 함수 본문에는 다음이 종료 되 면 반환 작업 완료 되지 않은 상태로 이동 됩니다.

*  함수 본문 return 문이 또는 본문의 끝에 도달의 결과로 종료 되 면 결과 값은 성공된 상태에 배치 되는 작업의 반환에 기록 됩니다.
*  함수 본문 예외로 인해 종료 되는 경우 ([throw 문](statements.md#the-throw-statement)) 예외는 faulted 상태로 전환 되는 task 반환에 기록 됩니다.

### <a name="evaluation-of-a-void-returning-async-function"></a>Void 반환 비동기 함수 계산

비동기 함수의 반환 형식이 `void`을 위에서 다음과 같이 달라 집니다 평가: 작업이 반환 되기 때문에 함수 완성 및 현재 스레드의 예외를 대신 통신 ***동기화 상황에 맞는***합니다. 동기화 컨텍스트의 정확한 정의 구현에 종속 된 이지만 표현인 현재 스레드가 실행 되 고 "where"입니다. 동기화 컨텍스트는 void 반환 비동기 함수 시작, 완료 되 면 또는 확인할 수 없는 예외를 throw 하는 경우에 알립니다.

이렇게 하면 얼마나 많은 void 반환 비동기 기능을 실행 하는 추적 하 고 발생 하는 예외를 전파 하는 방법을 결정 하는 컨텍스트.
