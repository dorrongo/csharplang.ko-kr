# <a name="attributes"></a>특성

C# 언어의 대부분 프로그램에서 정의 된 엔터티에 대 한 선언적 정보를 지정할 수가 있습니다. 사용 하 여 데코 레이트 하 여 클래스에서 메서드의 액세스 가능성은 지정 하는 예를 들어 합니다 *method_modifier*s `public`, `protected`, `internal`, 및 `private`합니다.

C# 프로그래머 라고 하는 선언적 정보의 새 종류를 사용 하도록 설정 ***특성***합니다. 다음 프로그래머에 게 다양 한 프로그램 엔터티에 특성을 연결 하 고 런타임 환경의 특성 정보를 검색할 수 있습니다. 예를 들어 프레임 워크를 정의할 수는 `HelpAttribute` 해당 프로그램 요소에서 해당 설명서로의 매핑 수 있도록 특정 프로그램 요소 (예: 클래스 및 메서드)에 배치할 수 있는 특성입니다.

특성은 특성 클래스의 선언을 통해 정의 됩니다 ([특성 클래스가](attributes.md#attribute-classes))에 위치와 명명 된 매개 변수가 있을 수 ([위치 및 명명 된 매개 변수](attributes.md#positional-and-named-parameters)). 특성은 특성 사양을 사용 하 여 C# 프로그램의 엔터티에 연결 됩니다 ([특성 사양](attributes.md#attribute-specification)), 특성 인스턴스로 런타임에 검색할 수 있습니다 ([인스턴스 특성](attributes.md#attribute-instances)).

## <a name="attribute-classes"></a>특성 클래스

추상 클래스에서 파생 된 클래스 `System.Attribute`직접 또는 간접적으로 여부와 관계 없이 되는 ***특성 클래스***합니다. 특성 클래스의 선언 정의 종류의 새 ***특성*** 선언에 배치할 수 있습니다. 규칙에 따라 특성 클래스의 접미사가 붙은 `Attribute`합니다. 특성의 사용 하 여 포함 하거나이 접미사를 생략할 수 있습니다.

### <a name="attribute-usage"></a>특성 사용

특성 `AttributeUsage` ([The AttributeUsage 특성](attributes.md#the-attributeusage-attribute)) 특성 클래스를 사용할 수 있는 방법을 설명 하는 데 사용 됩니다.

`AttributeUsage` 위치 매개 변수 ([위치 및 명명 된 매개 변수](attributes.md#positional-and-named-parameters)) 특성 클래스를 사용할 수 있습니다 선언의 종류를 지정할 수 있도록 합니다. 이 예제에서

```csharp
using System;

[AttributeUsage(AttributeTargets.Class | AttributeTargets.Interface)]
public class SimpleAttribute: Attribute 
{
    ...
}
```

명명 된 특성 클래스를 정의 `SimpleAttribute` 에 배치할 수 있습니다 *class_declaration*s 및 *interface_declaration*만 합니다. 이 예제에서

```csharp
[Simple] class Class1 {...}

[Simple] interface Interface1 {...}
```

여러 번 사용 된 `Simple` 특성입니다. 이름을 사용 하 여이 특성이 정의 되어 있지만 `SimpleAttribute`이 특성을 사용 하는 경우는 `Attribute` 접미사 생략할 수 있으며, 짧은 이름에 결과 `Simple`합니다. 따라서 위의 예제에서는 다음과 의미 체계가 같습니다.

```csharp
[SimpleAttribute] class Class1 {...}

[SimpleAttribute] interface Interface1 {...}
```

`AttributeUsage` 명명 된 매개 변수 ([위치 및 명명 된 매개 변수](attributes.md#positional-and-named-parameters)) 이라는 `AllowMultiple`, 특성 지정 된 엔터티에 대 한 두 번 이상 지정할 수 있는지 여부를 나타냅니다. 하는 경우 `AllowMultiple` 특성에 대 한 클래스는 물론 다음 특성 클래스는를 ***다중 사용 특성 클래스***, 엔터티의 두 번 이상 지정할 수 있습니다. 하는 경우 `AllowMultiple` 특성에 대 한 클래스 false 또는 지정 되지 않으면 해당 특성 클래스는를 ***1 회용 특성 클래스***, 엔터티에 대해 한 번만 지정할 수 있습니다.

이 예제에서

```csharp
using System;

[AttributeUsage(AttributeTargets.Class, AllowMultiple = true)]
public class AuthorAttribute: Attribute
{
    private string name;

    public AuthorAttribute(string name) {
        this.name = name;
    }

    public string Name {
        get { return name; }
    }
}
```

라는 다중 사용 특성 클래스를 정의 `AuthorAttribute`합니다. 이 예제에서

```csharp
[Author("Brian Kernighan"), Author("Dennis Ritchie")] 
class Class1
{
    ...
}
```

두 가지 용도 사용 하 여 클래스 선언을 보여 줍니다는 `Author` 특성입니다.

`AttributeUsage` 호출 하는 다른 명명 된 매개 변수가 `Inherited`, 특성, 기본 클래스에서 지정 된 경우 해당 기본 클래스에서 파생 된 클래스에서 상속 되었는지 여부를 나타냅니다. 경우 `Inherited` 클래스가 true 이면 특성에 대 한 다음 해당 특성에 상속 됩니다. 경우 `Inherited` 특성 클래스는 false를 해당 특성은 상속 되지 않습니다. 이 지정 된 경우 해당 기본값은 true입니다.

특성 클래스 `X` 없는 `AttributeUsage` 특성에서와 같이 연결 합니다.

```csharp
using System;

class X: Attribute {...}
```

다음과 같습니다.

```csharp
using System;

[AttributeUsage(
    AttributeTargets.All,
    AllowMultiple = false,
    Inherited = true)
]
class X: Attribute {...}
```

### <a name="positional-and-named-parameters"></a>위치 인수와 명명 된 매개 변수

특성 클래스를 가질 수 있습니다 ***위치 매개 변수*** 하 고 ***명명 된 매개 변수***합니다. 각 public 인스턴스 생성자는 특성 클래스에 대 한 올바른 시퀀스로 해당 특성 클래스에 대 한 위치 매개 변수를 정의합니다. 특성 클래스에 대 한 각 속성과 비정적 공용 읽기 / 쓰기 필드인 특성 클래스에 대 한 명명된 된 매개 변수를 정의합니다.

이 예제에서

```csharp
using System;

[AttributeUsage(AttributeTargets.Class)]
public class HelpAttribute: Attribute
{
    public HelpAttribute(string url) {        // Positional parameter
        ...
    }

    public string Topic {                     // Named parameter
        get {...}
        set {...}
    }

    public string Url {
        get {...}
    }
}
```

명명 된 특성 클래스를 정의 `HelpAttribute` 위치 매개 변수를 `url`, 및 하나의 명명 된 매개 변수, `Topic`합니다. Static이 아니고, 공용 속성 이지만 `Url` 읽기 / 쓰기 아니므로 명명된 된 매개 변수를 정의 하지 않습니다.

이 특성 클래스는 다음과 같이 사용할 수 있습니다.

```csharp
[Help("http://www.mycompany.com/.../Class1.htm")]
class Class1
{
    ...
}

[Help("http://www.mycompany.com/.../Misc.htm", Topic = "Class2")]
class Class2
{
    ...
}
```

### <a name="attribute-parameter-types"></a>특성 매개 변수 형식

특성 클래스에 대 한 위치 및 명명 된 매개 변수 유형은 제한 합니다 ***매개 변수 형식 특성***는:

*  다음 형식 중 하나: `bool`, `byte`, `char`, `double`, `float`, `int`, `long`를 `sbyte`, `short`를 `string`를 `uint`, `ulong`, `ushort`.
*  `object` 형식
*  `System.Type` 형식
*  열거형 형식에 public 액세스 가능성이 있으며 있는 것은 중첩 된 형식을 (있는 경우)도 public 접근성이 있어야 제공 ([특성 사양](attributes.md#attribute-specification)).
*  위 형식의 1 차원 배열입니다.
*  특성 사양에서 위치 또는 명명 된 매개 변수로 생성자 인수 또는 이러한 형식 중 하나가 없는 public 필드를 사용할 수 없습니다.

## <a name="attribute-specification"></a>특성 사양

***특성 사양*** 선언에는 이전에 정의 된 특성의 응용 프로그램입니다. 특성 선언에 지정 된 추가 선언 정보 부분입니다. 특성 (특성을 포함 하는 어셈블리 또는 모듈에서 지정) 하는 전역 범위에서 지정할 수 있습니다 및에 대 한 *type_declaration*s ([형식 선언을](namespaces.md#type-declarations)), *class_member_declaration* s ([입력 매개 변수 제약 조건이](classes.md#type-parameter-constraints)), *interface_member_declaration*s ([인터페이스 멤버](interfaces.md#interface-members)), *struct_member _declaration*s ([구조체 멤버](structs.md#struct-members)), *enum_member_declaration*s ([열거형 멤버](enums.md#enum-members)), *accessor_declarations*  ([접근자](classes.md#accessors)), *event_accessor_declarations* ([필드와 유사한 이벤트](classes.md#field-like-events)), 및 *formal_parameter_list*s ([메서드 매개 변수](classes.md#method-parameters)).

에 지정 된 특성 ***섹션에서는 특성***합니다. 특성 섹션을 쉼표로 구분 된 목록을 하나 이상의 특성을 감싸는 대괄호 쌍으로 구성 합니다. 해당 목록에 지정 된 특성 및 동일한 프로그램 엔터티를 연결 하는 섹션 순서 정렬 순서는 중요 하지 않습니다. 예를 들어 특성 사양 `[A][B]`, `[B][A]`를 `[A,B]`, 및 `[B,A]` 동일 합니다.

```antlr
global_attributes
    : global_attribute_section+
    ;

global_attribute_section
    : '[' global_attribute_target_specifier attribute_list ']'
    | '[' global_attribute_target_specifier attribute_list ',' ']'
    ;

global_attribute_target_specifier
    : global_attribute_target ':'
    ;

global_attribute_target
    : 'assembly'
    | 'module'
    ;

attributes
    : attribute_section+
    ;

attribute_section
    : '[' attribute_target_specifier? attribute_list ']'
    | '[' attribute_target_specifier? attribute_list ',' ']'
    ;

attribute_target_specifier
    : attribute_target ':'
    ;

attribute_target
    : 'field'
    | 'event'
    | 'method'
    | 'param'
    | 'property'
    | 'return'
    | 'type'
    ;

attribute_list
    : attribute (',' attribute)*
    ;

attribute
    : attribute_name attribute_arguments?
    ;

attribute_name
    : type_name
    ;

attribute_arguments
    : '(' positional_argument_list? ')'
    | '(' positional_argument_list ',' named_argument_list ')'
    | '(' named_argument_list ')'
    ;

positional_argument_list
    : positional_argument (',' positional_argument)*
    ;

positional_argument
    : attribute_argument_expression
    ;

named_argument_list
    : named_argument (','  named_argument)*
    ;

named_argument
    : identifier '=' attribute_argument_expression
    ;

attribute_argument_expression
    : expression
    ;
```

특성으로 구성 됩니다는 *attribute_name* 및 선택적 인수 및 명명 된 인수 목록입니다. 위치 인수 (있는 경우) 명명 된 인수 앞에 야 합니다. 구성 위치 인수는 *attribute_argument_expression*; 명명된 된 인수 뒤에 등호 뒤에 이름, 구성는 *attribute_argument_expression*는 함께 간단한 할당으로 동일한 규칙으로 제한 됩니다. 명명 된 인수의 순서가 중요 합니다.

합니다 *attribute_name* 특성 클래스를 식별 합니다. 경우 형태로 *attribute_name* 됩니다 *type_name* 다음 특성 클래스에이 이름을 참조 해야 합니다. 그렇지 않으면 컴파일 타임 오류가 발생합니다. 이 예제에서

```csharp
class Class1 {}

[Class1] class Class2 {}    // Error
```

사용 하려고 했기 때문에 컴파일 타임 오류가 발생 `Class1` 클래스를 특성으로 `Class1` 특성 클래스가 아닙니다.

특정 컨텍스트 둘 이상의 대상에 특성의 사양을 허용합니다. 프로그램을 포함 하 여 대상을 명시적으로 지정할 수는 *attribute_target_specifier*합니다. 특성은 전역 수준에서 배치 되는 경우는 *global_attribute_target_specifier* 필요 합니다. 다른 모든 위치에서 적절 한 기본값은 적용 되지만 *attribute_target_specifier* 확인 하거나 특정 모호한 경우에서 기본값을 재정의 하려면 (또는 모호 하지 않은 경우에서 기본값을 확인만)에 사용할 수 있습니다. 따라서, 일반적으로 *attribute_target_specifier*전역 수준에서 제외 하 고 s를 생략할 수 있습니다. 잠재적으로 모호한 컨텍스트는 다음과 같이 해결 됩니다.

*  전역 범위에서 지정 된 특성 대상 어셈블리 또는 대상 모듈에 적용할 수 있습니다. 따라서이 컨텍스트에 대 한 기본값이 존재를 *attribute_target_specifier* 이 컨텍스트에서 항상 필요 합니다. 현재 상태를 `assembly` *attribute_target_specifier* 대상 특성 적용 된다고 어셈블리;의 현재 상태를 `module` *attribute_target_specifier* 대상 모듈에는 특성이 적용 되는 것을 나타냅니다.
*  Delegate 선언에서 지정 된 특성 선언 되는 대리자 또는 해당 반환 값에 적용할 수 있습니다. 없는 경우에는 *attribute_target_specifier*, 특성이 대리자에 적용 됩니다. 현재 상태를 `type` *attribute_target_specifier* 대리자; 특성 적용 된다고의 존재를 `return` *attribute_target_specifier* 반환 값에는 특성이 적용 되는 것을 나타냅니다.
*  메서드 선언에서 지정 된 특성 선언 되는 메서드 또는 해당 반환 값에 적용할 수 있습니다. 없는 경우에는 *attribute_target_specifier*, 메서드에 특성이 적용 됩니다. 현재 상태를 `method` *attribute_target_specifier* ; 메서드에 특성 적용 된다고의 존재를 `return` *attribute_target_specifier* 나타냅니다 특성에는 반환 값에 적용 됩니다.
*  연산자 선언에 지정 된 특성 선언 되는 연산자 또는 해당 반환 값에 적용할 수 있습니다. 없는 경우에는 *attribute_target_specifier*, 특성 연산자에 적용 됩니다. 현재 상태를 `method` *attribute_target_specifier* 연산자 특성 적용 된다고의 존재를 `return` *attribute_target_specifier* 반환 값에는 특성이 적용 되는 것을 나타냅니다.
*  이벤트 접근자를 생략 하는 이벤트 선언에서 지정 된 특성 선언 되는 이벤트, (이벤트가 추상이 아닌) 하는 경우 연결 된 필드 또는 관련된 추가 적용 하 고 메서드를 제거할 수 있습니다. 없는 경우에는 *attribute_target_specifier*, 이벤트에 특성이 적용 됩니다. 현재 상태를 `event` *attribute_target_specifier* 이벤트 특성 적용 된다고의 존재를 `field` *attribute_target_specifier* 나타냅니다 특성 필드에 적용 합니다. 및의 현재 상태를 `method` *attribute_target_specifier* 메서드에 특성 적용 된다고 합니다.
*  속성 또는 인덱서의 선언에 대 한 get 접근자 선언에 지정 된 특성이 연결된 된 메서드 또는 해당 반환 값에 적용할 수 있습니다. 없는 경우에는 *attribute_target_specifier*, 메서드에 특성이 적용 됩니다. 현재 상태를 `method` *attribute_target_specifier* ; 메서드에 특성 적용 된다고의 존재를 `return` *attribute_target_specifier* 나타냅니다 특성에는 반환 값에 적용 됩니다.
*  속성 또는 인덱서의 선언에 대 한 set 접근자에 지정 된 특성의 유일한 암시적 매개 변수 또는 연결된 된 메서드를 적용할 수 있습니다. 없는 경우에는 *attribute_target_specifier*, 메서드에 특성이 적용 됩니다. 현재 상태를 `method` *attribute_target_specifier* ; 메서드에 특성 적용 된다고의 존재를 `param` *attribute_target_specifier* 나타냅니다 매개 변수에;는 특성이 적용 되는 현재 상태를 `return` *attribute_target_specifier* 특성 반환 값에 적용 되도록 나타냅니다.
*  이벤트 선언 또는 연결된 된 메서드의 유일한 매개 변수를 적용할 수에 add 또는 remove 접근자 선언에 지정 된 특성입니다. 없는 경우에는 *attribute_target_specifier*, 메서드에 특성이 적용 됩니다. 현재 상태를 `method` *attribute_target_specifier* ; 메서드에 특성 적용 된다고의 존재를 `param` *attribute_target_specifier* 나타냅니다 매개 변수에;는 특성이 적용 되는 현재 상태를 `return` *attribute_target_specifier* 특성 반환 값에 적용 되도록 나타냅니다.

다른 컨텍스트에서 포함 여부는 *attribute_target_specifier* 허용 하지만 불필요 한 합니다. 예를 들어, 클래스 선언 수 포함 하거나 지정자를 생략 `type`:

```csharp
[type: Author("Brian Kernighan")]
class Class1 {}

[Author("Dennis Ritchie")]
class Class2 {}
```

잘못 된을 지정 하면 오류가 발생 *attribute_target_specifier*합니다. 예를 들어 지정자 `param` 클래스 선언에서 사용할 수 없습니다.

```csharp
[param: Author("Brian Kernighan")]        // Error
class Class1 {}
```

규칙에 따라 특성 클래스의 접미사가 붙은 `Attribute`합니다. *attribute_name* 양식의 *type_name* 포함 하거나이 접미사를 생략할 수 있습니다. 있으면 특성 클래스 둘 다 사용 하 여 하지 않고이 접미사는 모호성을 사용할 수 있는지 및 컴파일 타임 오류가 발생 합니다. 경우는 *attribute_name* 철자가 되도록 해당 가장 오른쪽 *식별자* 축 자 식별자 ([식별자](lexical-structure.md#identifiers)), 접미사가 없는 특성만 일치 하면 다음 따라서 해결 해야 하는 이러한 모호성을 사용 하도록 설정 합니다. 이 예제에서

```csharp
using System;

[AttributeUsage(AttributeTargets.All)]
public class X: Attribute
{}

[AttributeUsage(AttributeTargets.All)]
public class XAttribute: Attribute
{}

[X]                     // Error: ambiguity
class Class1 {}

[XAttribute]            // Refers to XAttribute
class Class2 {}

[@X]                    // Refers to X
class Class3 {}

[@XAttribute]           // Refers to XAttribute
class Class4 {}
```

두 특성 클래스 표시 `X` 고 `XAttribute`입니다. 특성 `[X]` 되며 중 하나를 참조할 수 있으므로 모호한 `X` 또는 `XAttribute`합니다. 축 자 식별자를 사용 하 여 정확한 의도를 이러한 드문 경우에 지정할 수 있습니다. 특성 `[XAttribute]` 모호 하지 않은 경우 (특성 클래스가 되었으면 하지만 `XAttributeAttribute`!). 경우 클래스의 선언을 `X` 제거 되 면 두 특성 모두 라는 특성 클래스를 참조 하는 다음 `XAttribute`같이:

```csharp
using System;

[AttributeUsage(AttributeTargets.All)]
public class XAttribute: Attribute
{}

[X]                     // Refers to XAttribute
class Class1 {}

[XAttribute]            // Refers to XAttribute
class Class2 {}

[@X]                    // Error: no attribute named "X"
class Class3 {}
```

이 클래스를 사용 하는 1 회용 특성 두 번 이상 동일한 엔터티에 컴파일 타임 오류입니다. 이 예제에서

```csharp
using System;

[AttributeUsage(AttributeTargets.Class)]
public class HelpStringAttribute: Attribute
{
    string value;

    public HelpStringAttribute(string value) {
        this.value = value;
    }

    public string Value {
        get {...}
    }
}

[HelpString("Description of Class1")]
[HelpString("Another description of Class1")]
public class Class1 {}
```

사용 하려고 했기 때문에 컴파일 타임 오류가 발생 `HelpString`에 1 회용 특성 클래스에 두 번 이상 선언 시 `Class1`합니다.

식을 `E` 되는 *attribute_argument_expression* 다음 문 중 모두 만족 하는 경우:

*  유형의 `E` 특성 매개 변수 형식입니다 ([매개 변수 형식 특성](attributes.md#attribute-parameter-types)).
*  컴파일 타임의 값에 `E` 다음 중 하나를 확인할 수 있습니다.
   * 상수 값입니다.
   * `System.Type` 개체입니다.
   * 1 차원 배열의 *attribute_argument_expression*s입니다.

예를 들어:

```csharp
using System;

[AttributeUsage(AttributeTargets.Class)]
public class TestAttribute: Attribute
{
    public int P1 {
        get {...}
        set {...}
    }

    public Type P2 {
        get {...}
        set {...}
    }

    public object P3 {
        get {...}
        set {...}
    }
}

[Test(P1 = 1234, P3 = new int[] {1, 3, 5}, P2 = typeof(float))]
class MyClass {}
```

A *typeof_expression* ([typeof 연산자](expressions.md#the-typeof-operator)) 사용 하는 제네릭이 아닌 형식, 폐쇄형된 생성된 형식, 또는 바인딩되지 않은 제네릭 형식이 특성 인수 식을 참조할 수 있지만 참조할 수 없습니다는 형식을 엽니다. 이렇게 하면 컴파일 시간 식을 해결할 수 있습니다.

```csharp
class A: Attribute
{
    public A(Type t) {...}
}

class G<T>
{
    [A(typeof(T))] T t;                  // Error, open type in attribute
}

class X
{
    [A(typeof(List<int>))] int x;        // Ok, closed constructed type
    [A(typeof(List<>))] int y;           // Ok, unbound generic type
}
```

## <a name="attribute-instances"></a>특성 인스턴스

***특성 인스턴스가*** 런타임 시 특성을 나타내는 인스턴스입니다. 특성은 특성 클래스를 위치 인수를 사용 하 여 정의 되 고 명명 된 인수입니다. 특성 인스턴스는 위치와 명명 된 인수를 사용 하 여 초기화 되는 특성 클래스의 인스턴스입니다.

다음 섹션에 설명 된 대로 컴파일 타임 및 런타임 모두 처리를 포함 하는 특성 인스턴스를 검색 합니다.

### <a name="compilation-of-an-attribute"></a>특성의 컴파일

컴파일하는 *특성* 특성 클래스를 사용 하 여 `T`, *positional_argument_list* `P` 고 *named_argument_list* `N`, 다음 단계로 구성 됩니다.

*  컴파일에 대 한 컴파일 시간 처리 단계는 *object_creation_expression* 양식의 `new T(P)`합니다. 이 단계는 컴파일 타임 오류가를 발생 시키거나 결정 인스턴스 생성자 `C` 에서 `T` 런타임 시 호출할 수 있습니다.
*  경우 `C` 되지 않은 public 액세스 가능성을 컴파일 타임 오류가 발생 합니다.
*  각 *named_argument* `Arg` 에서 `N`:
   * 수 있도록 `Name` 수는 *식별자* 의 합니다 *named_argument* `Arg`합니다.
   * `Name` 비정적 읽기 / 쓰기 공용 필드 또는 속성을 식별 해야 `T`합니다. 경우 `T` 그러한 필드 또는 속성에 컴파일 타임 오류가 발생 하는 입력 합니다.
*  특성의 런타임 인스턴스화에 대 한 다음 정보를 보관: 특성 클래스 `T`, 인스턴스 생성자 `C` 온 `T`의 *positional_argument_list* `P` 하며 *named_argument_list* `N`합니다.

### <a name="run-time-retrieval-of-an-attribute-instance"></a>특성 인스턴스의 런타임 검색

컴파일하는 *특성* 특성 클래스를 생성 `T`, 인스턴스 생성자 `C` 에 `T`, *positional_argument_list* `P`, 및 *named_argument_list* `N`합니다. 주어진이 정보로 특성 인스턴스를 다음 단계를 사용 하 여 런타임 시 검색할 수 있습니다.

*  실행에 대 한 런타임 처리 단계는 *object_creation_expression* 양식의 `new T(P)`, 인스턴스 생성자를 사용 하 여 `C` 컴파일 시간에 따라. 이러한 단계는 예외를 발생 시키거나 인스턴스를 생성 `O` 의 `T`합니다.
*  각 *named_argument* `Arg` 에서 `N`, 순서에서:
   * 수 있도록 `Name` 수는 *식별자* 의 합니다 *named_argument* `Arg`합니다. 하는 경우 `Name` 비정적 공용 읽기 / 쓰기 필드 또는 속성으로 식별 하지 않습니다 `O`, 예외가 throw 됩니다.
   * 수 있도록 `Value` 평가의 결과 *attribute_argument_expression* 의 `Arg`합니다.
   * 하는 경우 `Name` 에서 필드를 식별 `O`, 그런 다음이 필드를 설정 `Value`합니다.
   * 그렇지 않으면 `Name` 에서 속성을 식별 `O`합니다. 이 속성을 설정 `Value`합니다.
   * 결과 `O`, 특성 클래스의 인스턴스 `T` 로 초기화 된는 합니다 *positional_argument_list* `P` 하며 *named_argument_list* `N`.

## <a name="reserved-attributes"></a>예약 된 특성

소수의 특성 어떤 방식으로든에서 언어를 영향을 줍니다. 이러한 특성은 다음과 같습니다.

*  `System.AttributeUsageAttribute` ([The AttributeUsage 특성](attributes.md#the-attributeusage-attribute))에 특성 클래스를 사용할 수 있는 방법에 설명 하는 데 사용 됩니다.
*  `System.Diagnostics.ConditionalAttribute` ([The 조건부 특성](attributes.md#the-conditional-attribute))에 조건부 메서드를 정의 하는 데 사용 됩니다.
*  `System.ObsoleteAttribute` ([The Obsolete 특성](attributes.md#the-obsolete-attribute))에 사용 되지 않는 멤버를 표시 하는 데 사용 됩니다.
*  `System.Runtime.CompilerServices.CallerLineNumberAttribute`를 `System.Runtime.CompilerServices.CallerFilePathAttribute` 하 고 `System.Runtime.CompilerServices.CallerMemberNameAttribute` ([호출자 정보 특성](attributes.md#caller-info-attributes)), 선택적 매개 변수를 호출 컨텍스트에 대 한 정보를 제공 하는 데 사용 되는 합니다.

### <a name="the-attributeusage-attribute"></a>AttributeUsage 특성

특성 `AttributeUsage` 특성 클래스를 사용할 수 있는 방식으로 설명 하는 데 사용 됩니다.

사용 하 여 데코 레이트 된 클래스는 `AttributeUsage` 특성에서 파생 되어야 합니다 `System.Attribute`를 직접 또는 간접적으로 합니다. 그렇지 않으면 컴파일 타임 오류가 발생합니다.

```csharp
namespace System
{
    [AttributeUsage(AttributeTargets.Class)]
    public class AttributeUsageAttribute: Attribute
    {
        public AttributeUsageAttribute(AttributeTargets validOn) {...}
        public virtual bool AllowMultiple { get {...} set {...} }
        public virtual bool Inherited { get {...} set {...} }
        public virtual AttributeTargets ValidOn { get {...} }
    }

    public enum AttributeTargets
    {
        Assembly     = 0x0001,
        Module       = 0x0002,
        Class        = 0x0004,
        Struct       = 0x0008,
        Enum         = 0x0010,
        Constructor  = 0x0020,
        Method       = 0x0040,
        Property     = 0x0080,
        Field        = 0x0100,
        Event        = 0x0200,
        Interface    = 0x0400,
        Parameter    = 0x0800,
        Delegate     = 0x1000,
        ReturnValue  = 0x2000,

        All = Assembly | Module | Class | Struct | Enum | Constructor | 
            Method | Property | Field | Event | Interface | Parameter | 
            Delegate | ReturnValue
    }
}
```

### <a name="the-conditional-attribute"></a>조건부 특성

특성 `Conditional` 의 정의 사용 하도록 설정 ***조건부 메서드이므로*** 하 고 ***조건부 특성 클래스***합니다.

```csharp
namespace System.Diagnostics
{
    [AttributeUsage(AttributeTargets.Method | AttributeTargets.Class, AllowMultiple = true)]
    public class ConditionalAttribute: Attribute
    {
        public ConditionalAttribute(string conditionString) {...}
        public string ConditionString { get {...} }
    }
}
```

#### <a name="conditional-methods"></a>조건부 메서드

메서드를 사용 하 여 데코 레이트 된 `Conditional` 특성이 조건부 메서드. `Conditional` 특성 조건부 컴파일 기호를 테스트 하 여 상태를 나타냅니다. 조건부 메서드를 호출 포함 되거나 호출 시이 기호가 정의 되었는지 여부에 따라 생략 됩니다. 기호가 정의 된 경우 호출 포함 합니다. 그렇지 않으면 호출 (수신기의 평가 및 호출의 매개 변수 포함)은 생략 됩니다.

조건부 메서드는 다음과 같은 제한 사항이 적용 됩니다.

*  조건부 메서드는 메서드가 이어야 합니다는 *class_declaration* 하거나 *struct_declaration*합니다. 컴파일 타임 오류가 발생 하는 경우는 `Conditional` 인터페이스 선언에서 메서드에 특성을 지정 합니다.
*  조건부 메서드는 반환 형식이 있어야 합니다. `void`합니다.
*  조건부 메서드를 사용 하 여 표시 되 면 안 된 `override` 한정자입니다. 하지만 조건부 메서드를 사용 하 여 표시 될 수도 있습니다는 `virtual` 한정자 합니다. 이러한 메서드의 재정의 암시적 조건부 및 사용 하 여 명시적으로 표시 해서는 안을 `Conditional` 특성입니다.
*  조건부 메서드는 인터페이스 메서드의 구현을 아니어야 합니다. 그렇지 않으면 컴파일 타임 오류가 발생합니다.

또한 컴파일 시간 오류가 발생 하는 조건부 메서드를 사용 하는 경우는 *delegate_creation_expression*합니다. 이 예제에서

```csharp
#define DEBUG

using System;
using System.Diagnostics;

class Class1 
{
    [Conditional("DEBUG")]
    public static void M() {
        Console.WriteLine("Executed Class1.M");
    }
}

class Class2
{
    public static void Test() {
        Class1.M();
    }
}
```

선언 `Class1.M` 조건부 메서드로 합니다. `Class2``Test` 메서드에서이 메서드를 호출 합니다. 조건부 컴파일 기호를 이후 `DEBUG` 정의 된 경우 `Class2.Test` 은 호출, 호출 `M`합니다. 경우 기호가 `DEBUG` 하지을 정의한 후 `Class2.Test` 호출 하지는 `Class1.M`합니다.

호출 시 조건부 컴파일 기호로 포함 또는 제외 조건부 메서드 호출의 제어 하는 것이 반드시 합니다. 예제

파일 `class1.cs`:

```csharp
using System.Diagnostics;

class Class1 
{
    [Conditional("DEBUG")]
    public static void F() {
        Console.WriteLine("Executed Class1.F");
    }
}
```

파일 `class2.cs`:

```csharp
#define DEBUG

class Class2
{
    public static void G() {
        Class1.F();                // F is called
    }
}
```

파일 `class3.cs`:

```csharp
#undef DEBUG

class Class3
{
    public static void H() {
        Class1.F();                // F is not called
    }
}
```

클래스 `Class2` 하 고 `Class3` 조건부 메서드 호출이 각각 포함 `Class1.F`, 여부에 따라 조건부는 `DEBUG` 정의 됩니다. 컨텍스트에서이 기호 정의 되므로 `Class2` 아닌 `Class3`에 대 한 호출 `F` 에서 `Class2` 호출 하는 동안 포함 되어 `F` 에서 `Class3` 생략 됩니다.

상속 체인의 조건부 메서드를 사용 하는 혼동 될 수 있습니다. 통해 조건부 메서드 호출 `base`, 폼의 `base.M`, 일반 조건부 메서드 호출 규칙이 적용 됩니다. 예제

파일 `class1.cs`:

```csharp
using System;
using System.Diagnostics;

class Class1 
{
    [Conditional("DEBUG")]
    public virtual void M() {
        Console.WriteLine("Class1.M executed");
    }
}
```

파일 `class2.cs`:

```csharp
using System;

class Class2: Class1
{
    public override void M() {
        Console.WriteLine("Class2.M executed");
        base.M();                        // base.M is not called!
    }
}
```

파일 `class3.cs`:

```csharp
#define DEBUG

using System;

class Class3
{
    public static void Test() {
        Class2 c = new Class2();
        c.M();                            // M is called
    }
}
```

`Class2` 호출을 포함 합니다 `M` 기본 클래스에서 정의 합니다. 기본 메서드는 기호 유무에 따라 조건부 때문에이 호출이 생략 됩니다 `DEBUG`, 정의 되지 않습니다. 따라서 메서드는 콘솔에 씁니다 "`Class2.M executed`"만 합니다. 적절히 사용 *pp_declaration*s는 이러한 문제를 방지할 수 있습니다.

#### <a name="conditional-attribute-classes"></a>조건부 특성 클래스

특성 클래스 ([특성 클래스가](attributes.md#attribute-classes)) 하나 이상의으로 데코 레이트 `Conditional` 특성은는 ***조건부 특성 클래스***합니다. 에 선언 된 조건부 컴파일 기호를 사용 하 여 조건부 특성 클래스는 연결 되므로 해당 `Conditional` 특성입니다. 이 예제에서:

```csharp
using System;
using System.Diagnostics;
[Conditional("ALPHA")]
[Conditional("BETA")]
public class TestAttribute : Attribute {}
```

선언 `TestAttribute` 조건부 컴파일 기호를 사용 하 여 연결 하는 조건부 특성 클래스로 `ALPHA` 고 `BETA`입니다.

특성 사양 ([특성 사양](attributes.md#attribute-specification)) 조건부 특성의 경우 포함 된 해당 연결 된 조건부 컴파일 기호 중 하나 이상이 고, 그렇지 시점 사양에 정의 된 특성 사양 생략 됩니다.

포함 또는 제외의 조건부 특성 클래스의 특성 사양 조건부 컴파일 기호 지정 시점으로 제어 됩니다 하는 것이 반드시 합니다. 예제

파일 `test.cs`:

```csharp
using System;
using System.Diagnostics;

[Conditional("DEBUG")]

public class TestAttribute : Attribute {}
```

파일 `class1.cs`:

```csharp
#define DEBUG

[Test]                // TestAttribute is specified

class Class1 {}
```

파일 `class2.cs`:

```csharp
#undef DEBUG

[Test]                 // TestAttribute is not specified

class Class2 {}
```

클래스 `Class1` 하 고 `Class2` 는 특성으로 데코레이팅된 각 `Test`, 여부에 따라 조건부는 `DEBUG` 정의 됩니다. 컨텍스트에서이 기호 정의 되므로 `Class1` 아닌 `Class2`, 사양의 `Test` 특성을 `Class1` 지정 하는 동안 포함 됩니다는 `Test` 특성을 `Class2` 생략 됩니다.

### <a name="the-obsolete-attribute"></a>Obsolete 특성

특성 `Obsolete` 형식 및 더 이상 사용 해야 하는 형식의 멤버를 표시 하는 데 사용 됩니다.

```csharp
namespace System
{
    [AttributeUsage(
        AttributeTargets.Class | 
        AttributeTargets.Struct |
        AttributeTargets.Enum | 
        AttributeTargets.Interface | 
        AttributeTargets.Delegate |
        AttributeTargets.Method | 
        AttributeTargets.Constructor |
        AttributeTargets.Property | 
        AttributeTargets.Field |
        AttributeTargets.Event,
        Inherited = false)
    ]
    public class ObsoleteAttribute: Attribute
    {
        public ObsoleteAttribute() {...}
        public ObsoleteAttribute(string message) {...}
        public ObsoleteAttribute(string message, bool error) {...}
        public string Message { get {...} }
        public bool IsError { get {...} }
    }
}
```

형식 또는 멤버가 사용 하 여 데코 레이트 된 프로그램을 사용 하는 경우는 `Obsolete` 특성, 컴파일러가 경고 또는 오류가 발생 합니다. 특히, 컴파일러가 경고 또는 오류 매개 변수가 제공 되 고 기본값이 없는 오류 매개 변수를 제공 하는 경우 `false`합니다. 컴파일러에서 오류가 발생 하는 경우 오류 매개 변수가 지정 되 고 기본값이 `true`합니다.

예제

```csharp
[Obsolete("This class is obsolete; use class B instead")]
class A
{
    public void F() {}
}

class B
{
    public void F() {}
}

class Test
{
    static void Main() {
        A a = new A();         // Warning
        a.F();
    }
}
```

클래스 `A` 으로 데코 레이트 된는 `Obsolete` 특성입니다. 사용할 때마다 `A` 에서 `Main` 지정된 된 메시지를 포함 하는 경고 결과 "이이 클래스는 사용 되지 않습니다. 클래스 B 대신 사용 합니다. "

### <a name="caller-info-attributes"></a>호출자 정보 특성

로깅 및 보고와 같은 용도로 유용한 경우가 함수 멤버 호출 코드에 대 한 특정 컴파일 시간 정보를 얻을 수 있습니다. 호출자 정보 특성에는 이러한 정보를 투명 하 게 전달 하는 방법을 제공 합니다.

호출자 정보 특성 중 하나를 사용 하 여 선택적 매개 변수 주석이 지정 되어 있는 경우 호출에서 해당 인수를 생략 하면 발생 하지 않습니다 반드시 대체 해야 하는 기본 매개 변수 값. 대신 호출 컨텍스트에 대해 지정 된 정보를 사용할 수 있는 경우 해당 정보는 인수 값으로 전달 됩니다.

예를 들어:

```csharp
using System.Runtime.CompilerServices

...

public void Log(
    [CallerLineNumber] int line = -1,
    [CallerFilePath]   string path = null,
    [CallerMemberName] string name = null
)
{
    Console.WriteLine((line < 0) ? "No line" : "Line "+ line);
    Console.WriteLine((path == null) ? "No file path" : path);
    Console.WriteLine((name == null) ? "No member name" : name);
}
```

에 대 한 호출 `Log()` 인수 없이 호출의 줄 번호 및 파일 경로는 호출이 발생 한 멤버의 이름을 인쇄 합니다.

호출자 정보 특성 대리자 선언을 포함 하 여 선택적 매개 변수 어디에서 나 발생할 수 있습니다. 그러나 특정 호출자 정보 특성 매개 변수 형식으로 암시적 변환이 대체 값에서은 항상 특성 수는 매개 변수의 형식에 제한이 없습니다.

이 동일한 호출자 정보 특성 매개 변수 정의 및 partial 메서드 선언의 일부를 구현 하는 오류입니다. 구현에 발생 하는 호출자 정보 특성은 무시 됩니다. 반면 호출자 정보 특성 정의에 적용 됩니다.

호출자 정보 오버 로드 확인에 영향을 주지 않습니다. 오버 로드 확인 다른 생략 된 선택적 매개 변수는 무시 동일한 방식으로 이러한 매개 변수를 무시 호출자의 소스 코드에서 여전히 생략 하면 선택적 매개 변수에 특성 사용된 하는 대로 ([오버 로드 확인](expressions.md#overload-resolution)).

호출자 정보는 함수의 소스 코드에서 명시적으로 호출 될 때에 대체 됩니다. 암시적 부모 생성자 호출 같은 암시적 호출 원본 위치를 갖지 않으며 호출자 정보를 대체 합니다. 또한 동적으로 바인딩되는 호출이 호출자 정보를 대체 하지 않습니다 됩니다. 때 이러한 경우 특성이 지정 된 매개 변수가 생략 되는 호출자 정보, 매개 변수는 지정 된 기본 값 대신 사용 됩니다.

예외에는 쿼리 식입니다. 구문 확장 간주 됩니다 및 호출자 정보 호출자 정보 특성을 사용 하 여 선택적 매개 변수를 생략 하려면 확장할 호출을 하는 경우 대체 됩니다. 사용 되는 위치에는 호출에서 생성 된 쿼리 절의 위치가입니다.

다음 순서 대로 기본 설정 된 둘 이상의 호출자 정보 특성을 지정 된 매개 변수에서 지정 하는 경우: `CallerLineNumber`하십시오 `CallerFilePath`, `CallerMemberName`합니다.

#### <a name="the-callerlinenumber-attribute"></a>CallerLineNumber 특성

`System.Runtime.CompilerServices.CallerLineNumberAttribute` 표준 암시적 변환을 때 선택적 매개 변수에서 허용 됩니다 ([표준 암시적 변환이](conversions.md#standard-implicit-conversions))에서 상수 값을 `int.MaxValue` 매개 변수의 형식입니다. 이렇게 하면 오류 없이 해당 값까지 모든 음수가 아닌 줄 번호를 전달할 수 있습니다.

소스 코드의 위치에서 함수 호출을 사용 하 여 선택적 매개 변수를 생략 하는 경우는 `CallerLineNumberAttribute`, 해당 위치의 줄 번호를 나타내는 숫자 리터럴을 기본 매개 변수 값을 대신 호출에 대 한 인수로 사용 됩니다.

호출에서 여러 줄에 걸쳐 있는 경우 선택한 줄은 구현에 따라 다릅니다.

줄 번호를 영향을 받을 수 있는 참고 `#line` 지시문 ([지시문 줄](lexical-structure.md#line-directives)).

#### <a name="the-callerfilepath-attribute"></a>CallerFilePath 특성

합니다 `System.Runtime.CompilerServices.CallerFilePathAttribute` 표준 암시적 변환을 때 선택적 매개 변수에서 허용 됩니다 ([표준 암시적 변환이](conversions.md#standard-implicit-conversions))에서 `string` 매개 변수의 형식입니다.

소스 코드의 위치에서 함수 호출을 사용 하 여 선택적 매개 변수를 생략 하는 경우는 `CallerFilePathAttribute`, 해당 위치의 파일 경로 나타내는 문자열 리터럴 매개 변수 기본값 대신 호출에 대 한 인수로 사용 됩니다.

파일 경로의 형식은 구현에 따라 다릅니다.

파일 경로 따라 달라질 수 있습니다 `#line` 지시문 ([지시문 줄](lexical-structure.md#line-directives)).

#### <a name="the-callermembername-attribute"></a>CallerMemberName 특성

합니다 `System.Runtime.CompilerServices.CallerMemberNameAttribute` 표준 암시적 변환을 때 선택적 매개 변수에서 허용 됩니다 ([표준 암시적 변환이](conversions.md#standard-implicit-conversions))에서 `string` 매개 변수의 형식입니다.

소스 코드와 선택적 매개 변수를 생략 자체 또는 해당 반환 형식, 매개 변수 또는 형식 매개 변수에 함수 멤버에 적용 되는 위치 특성 또는 함수 멤버의 본문 내에서 함수 호출을 하는 경우는 `CallerMemberNameAttribute`에 해당 멤버의 이름을 나타내는 문자열 리터럴 매개 변수 기본값 대신 호출에 대 한 인수로 사용 됩니다.

제네릭 메서드 내에서 발생 하는 호출에 대 한 메서드 이름 자체 형식 매개 변수 목록 없이 사용 됩니다.

명시적 인터페이스 멤버 구현 내에서 발생 하는 호출에 대 한 메서드 이름 자체 이전 인터페이스 한정자 없이 사용 됩니다.

속성 또는 이벤트 접근자 내에서 발생 하는 호출에 사용 되는 멤버 이름 속성 또는 이벤트 자체의 됩니다.

인덱서 접근자 내에서 발생 하는 호출을 사용 하는 멤버 이름이에서 제공 하는 `IndexerNameAttribute` ([The IndexerName 특성](attributes.md#the-indexername-attribute)) 있는 경우 인덱서 멤버 또는 기본 이름을 `Item` 그렇지 않은 경우.

멤버의 인스턴스 생성자, 정적 생성자, 소멸자 및 연산자 선언 내에서 발생 하는 호출에 사용 된 이름은 구현에 따라 다릅니다.

## <a name="attributes-for-interoperation"></a>상호 운용성에 대 한 특성

참고:이 섹션에서는 C#의 Microsoft.NET 구현에만 적용 됩니다.

### <a name="interoperation-with-com-and-win32-components"></a>Win32 및 COM 구성 요소와 상호 운용

.NET 런타임 많은 COM 및 Win32 Dll을 사용 하 여 작성 된 구성 요소와 상호 운용 하도록 C# 프로그램을 사용 하도록 설정 하는 특성을 제공 합니다. 예를 들어 합니다 `DllImport` 특성에서 사용할 수 있습니다는 `static extern` 메서드의 구현에서 Win32 DLL을 찾을 임을 나타내려면 메서드. 이러한 특성에 포함 됩니다는 `System.Runtime.InteropServices` 네임 스페이스 및 이러한 특성에 대 한 자세한 설명서는 설명서에에서 나와 있는.NET 런타임입니다.

### <a name="interoperation-with-other-net-languages"></a>다른.NET 언어와 상호 운용

#### <a name="the-indexername-attribute"></a>IndexerName 특성

인덱서 인덱싱된 속성을 사용 하 여.NET에서 구현 되 고.NET 메타 데이터에서 이름이입니다. 없으면 `IndexerName` 인덱서를 그 이름 특성이 `Item` 기본적으로 사용 됩니다. `IndexerName` 특성을 사용 하면 개발자가이 기본값을 재정의 하 고 다른 이름을 지정 합니다.

```csharp
namespace System.Runtime.CompilerServices.CSharp
{
    [AttributeUsage(AttributeTargets.Property)]
    public class IndexerNameAttribute: Attribute
    {
        public IndexerNameAttribute(string indexerName) {...}
        public string Value { get {...} } 
    }
}
```
