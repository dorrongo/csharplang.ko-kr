# <a name="namespaces"></a>네임스페이스

C# 프로그램은 네임 스페이스를 사용 하 여 구성 됩니다. "External" 조직의 시스템 및 프로그램에 대 한 "내부" 조직 시스템으로 사용 되는 네임 스페이스-다른 프로그램에 노출 되는 프로그램 요소를 제공 하는 방법입니다.

Using 지시문 ([지시문을 사용 하 여](namespaces.md#using-directives)) 네임 스페이스 사용을 용이 하 게 제공 됩니다.

## <a name="compilation-units"></a>컴파일 단위

A *compilation_unit* 소스 파일의 전체 구조를 정의 합니다. 컴파일 단위를 0 개 이상의 이루어져 *using_directive*s 0 개 이상의 뒤 *global_attributes* 뒤에 0 개 이상의 *namespace_member_declaration*s .

```antlr
compilation_unit
    : extern_alias_directive* using_directive* global_attributes? namespace_member_declaration*
    ;
```

하나 이상의 컴파일 단위의 C# 프로그램으로 구성 됩니다, 그리고 각각 별도 소스 파일에 포함 합니다. C# 프로그램이 컴파일되면 모든 컴파일 단위는 함께 처리 됩니다. 따라서 컴파일 단위 종속 될 수 있는 서로 가능한 순환 방식에서입니다.

*using_directive*의 컴파일 단위에 영향 합니다 *global_attributes* 하 고 *namespace_member_declaration*해당 컴파일 단위의 s 하지만 미치는 영향을 주지 않습니다 다른 컴파일 단위입니다.

합니다 *global_attributes* ([특성](attributes.md)) 컴파일 단위에 대상 어셈블리 및 모듈에 대 한 특성의 사양을 허용 합니다. 어셈블리 및 모듈 형식에 대 한 실제 컨테이너로 작동합니다. 어셈블리는 여러 물리적으로 별도 모듈로 구성 될 수 있습니다.

합니다 *namespace_member_declaration*s 프로그램의 각 컴파일 단위의 멤버 전역 네임 스페이스 라는 단일 선언 공간에 참여 합니다. 예를 들어:

파일 `A.cs`:
```csharp
class A {}
```

파일 `B.cs`:
```csharp
class B {}
```

이 경우 정규화 된 이름 사용 하 여 두 개의 클래스를 선언 두 컴파일 단위는 단일 전역 네임 스페이스 기여 `A` 고 `B`입니다. 두 컴파일 단위가 동일한 선언 공간에 영향을 하기 때문에 되었을 것 오류가 포함 된 각 동일한 이름 가진 멤버를 선언 하는 경우.

## <a name="namespace-declarations"></a>네임스페이스 선언

A *namespace_declaration* 키워드로 구성 됩니다 `namespace`네임 스페이스 이름 및 본문 뒤, 선택적으로, 세미콜론입니다.

```antlr
namespace_declaration
    : 'namespace' qualified_identifier namespace_body ';'?
    ;

qualified_identifier
    : identifier ('.' identifier)*
    ;

namespace_body
    : '{' extern_alias_directive* using_directive* namespace_member_declaration* '}'
    ;
```

A *namespace_declaration* 의 최상위 선언으로 발생할 수 있습니다는 *compilation_unit* 또는 다른 내에서 멤버 선언 *namespace_declaration*합니다. 경우는 *namespace_declaration* 의 최상위 선언으로 발생을 *compilation_unit*, 네임 스페이스는 전역 네임 스페이스의 구성원이 됩니다. 경우는 *namespace_declaration* 내에서 다른 발생 *namespace_declaration*, 내부 네임 스페이스 외부 네임 스페이스의 구성원이 됩니다. 두 경우 모두 네임 스페이스의 이름을 포함 하는 네임 스페이스 내에서 고유 해야 합니다.

네임 스페이스는 암시적으로 `public` 및 네임 스페이스 선언의 모든 액세스 한정자를 포함할 수 없습니다.

내를 *namespace_body*, 선택적 *using_directive*s 다른 네임 스페이스, 형식 및 멤버에 직접 대신의 정규화 된 이름을 통해 참조 될 수 있도록의 이름을 가져옵니다. 선택적 *namespace_member_declaration*s 네임 스페이스의 선언 공간으로 멤버를 제공 합니다. 모든 *using_directive*의멤버 선언 앞에 나타나야 합니다.

합니다 *qualified_identifier* 의 *namespace_declaration* 는 단일 식별자 또는 구분 식별자의 시퀀스 수 "`.`" 토큰입니다. 두 번째 형식은 구문적 여러 네임 스페이스 선언으로 중첩 없이 중첩된 된 네임 스페이스를 정의 하는 프로그램을 허용 합니다. 예를 들어 개체에 적용된

```csharp
namespace N1.N2
{
    class A {}

    class B {}
}
```
의미 체계가 같습니다.
```csharp
namespace N1
{
    namespace N2
    {
        class A {}

        class B {}
    }
}
```

네임 스페이스는 개방형, 및 두 네임 스페이스 정규화 된 이름이 같은 선언이 동일한 선언 공간 ([선언](basic-concepts.md#declarations)). 예제
```csharp
namespace N1.N2
{
    class A {}
}

namespace N1.N2
{
    class B {}
}
```
이 경우 정규화 된 이름 사용 하 여 두 개의 클래스를 선언으로 동일한 선언 공간에 영향을 위의 두 가지 네임 스페이스 선언 `N1.N2.A` 고 `N1.N2.B`입니다. 두 선언이 동일한 선언 공간에 있으므로 것이 더 경우 각 오류 동일한 이름의 멤버의 선언을 포함 합니다.

## <a name="extern-aliases"></a>Extern 별칭

*extern_alias_directive* 네임 스페이스를 별칭으로 사용 되는 식별자를 소개 합니다. 별칭이 지정 된 네임 스페이스의 사양 외부 프로그램의 소스 코드에 있으며 별칭이 지정 된 네임 스페이스의 중첩 된 네임 스페이스에도 적용 됩니다.

```antlr
extern_alias_directive
    : 'extern' 'alias' identifier ';'
    ;
```

범위는 *extern_alias_directive* 으로 확장 되는 *using_directive*개이면 *global_attributes* 및 *namespace_member_declaration*위 컴파일 단위 또는 네임 스페이스 본문의 합니다.

포함 된 컴파일 단위 또는 네임 스페이스 본문 내에서 *extern_alias_directive*에서 도입 된 식별자는 *extern_alias_directive* 별칭이 지정 된 네임 스페이스를 참조 하는 데 사용 될 수 있습니다. 에 대 한 컴파일 시간 오류가 발생 합니다 *식별자* 단어를 `global`입니다.

*extern_alias_directive* 을 특정 컴파일 단위 또는 네임 스페이스 본문에 별칭 사용할 수 있도록 하지만 기본 선언 공간에 새 멤버를 제공 하지는 않습니다. 즉, 한 *extern_alias_directive* 은 전이적이 아니므로 하지만 대신 컴파일 단위 또는 네임 스페이스 본문만 발생 하는 영향을 줍니다.

다음 프로그램 선언 하 고 두 개의 extern 별칭을 사용 `X` 및 `Y`, 각 네임 스페이스 계층의 루트를 나타내는입니다.
```csharp
extern alias X;
extern alias Y;

class Test
{
    X::N.A a;
    X::N.B b1;
    Y::N.B b2;
    Y::N.C c;
}
```

프로그램 선언 있는지 extern 별칭 `X` 고 `Y`, 별칭의 실제 정의 프로그램 외부에 있지만. 동일한 이름의 `N.B` 으로 이제 클래스를 참조할 수 `X.N.B` 하 고 `Y.N.B`, 또는 네임 스페이스 별칭 한정자를 사용 하 여 `X::N.B` 및 `Y::N.B`합니다. 프로그램에는 없는 외부 정의 제공 되는 extern 별칭을 선언 하는 경우 오류가 발생 합니다.

## <a name="using-directives"></a>using 지시문

***지시문을 사용 하 여*** 네임 스페이스 및 다른 네임 스페이스에 정의 된 형식을 사용할 수 있습니다. 이름 확인 프로세스의 영향 지시문을 사용 하 여 *namespace_or_type_name*s ([Namespace 및 형식 이름](basic-concepts.md#namespace-and-type-names)) 및 *simple_name*s ([단순 이름 ](expressions.md#simple-names)), 선언, using 지시문과 달리 하지만 컴파일 단위 또는 네임 스페이스는 사용할 기본 선언 공간에 새 멤버에 기여 하지 않습니다.

```antlr
using_directive
    : using_alias_directive
    | using_namespace_directive
    | using_static_directive
    ;
```

A *using_alias_directive* ([Using 별칭 지시문](namespaces.md#using-alias-directives)) 네임 스페이스 또는 형식에 대 한 별칭을 소개 합니다.

A *using_namespace_directive* ([네임 스페이스 지시문을 사용 하 여](namespaces.md#using-namespace-directives)) 네임 스페이스의 형식 멤버를 가져옵니다.

A *using_static_directive* ([Using 정적 지시문](namespaces.md#using-static-directives)) 중첩 된 형식 및 형식의 정적 멤버를 가져옵니다.

범위는 *using_directive* 으로 확장 되는 *namespace_member_declaration*직접 포함 하는 컴파일 단위 또는 네임 스페이스 본문의 합니다. 범위는 *using_directive* 해당 피어 포함 되지 않습니다 *using_directive*s입니다. 따라서 피어 링 *using_directive*s 서로 레코드에 영향을 주지는 않습니다 및 기록 되는 순서는 중요 하지 않습니다.

### <a name="using-alias-directives"></a>Using 별칭 지시문

A *using_alias_directive* 네임 스페이스 또는 바로 바깥쪽 컴파일 단위 또는 네임 스페이스 본문에서 형식을 별칭으로 사용 되는 식별자를 소개 합니다.

```antlr
using_alias_directive
    : 'using' identifier '=' namespace_or_type_name ';'
    ;
```

멤버 선언에서 포함 된 컴파일 단위 또는 네임 스페이스 본문과 *using_alias_directive*에서 도입 된 식별자는 *using_alias_directive* 사용할 수 참조를 지정 네임 스페이스 또는 형식입니다. 예를 들어:
```csharp
namespace N1.N2
{
    class A {}
}

namespace N3
{
    using A = N1.N2.A;

    class B: A {}
}
```

위의 멤버 선언에서 `N3` 네임 스페이스 `A` 별칭인 `N1.N2.A`, 및 따라서 클래스 `N3.B` 클래스에서 파생 되 `N1.N2.A`합니다. 별칭을 만들어 동일한 효과 얻을 수 있습니다 `R` 에 대 한 `N1.N2` 를 참조 하 고 `R.A`:
```csharp
namespace N3
{
    using R = N1.N2;

    class B: R.A {}
}
```

*식별자* 의 한 *using_alias_directive* 컴파일 단위 또는 직접 포함 하는 네임 스페이스 선언 공간 내에서 고유 해야 합니다 *using_alias_directive* . 예를 들어:
```csharp
namespace N3
{
    class A {}
}

namespace N3
{
    using A = N1.N2.A;        // Error, A already exists
}
```

위의 `N3` 이미 구성원을 포함 `A`이므로 대 한 컴파일 시간 오류를 *using_alias_directive* 해당 식별자를 사용 하도록 합니다. 두 개 이상에 대 한 컴파일 시간 오류를 마찬가지로 것 *using_alias_directive*s 같은 컴파일 단위 또는 네임 스페이스 본문에서 같은 이름의 별칭을 선언 합니다.

A *using_alias_directive* 을 특정 컴파일 단위 또는 네임 스페이스 본문에 별칭 사용할 수 있도록 하지만 기본 선언 공간에 새 멤버를 제공 하지는 않습니다. 즉, 한 *using_alias_directive* 전이 되지 않지만 대신 컴파일 단위 또는 네임 스페이스 본문만 발생 하는 영향을 줍니다. 예제
```csharp
namespace N3
{
    using R = N1.N2;
}

namespace N3
{
    class B: R.A {}            // Error, R unknown
}
```
범위는 *using_alias_directive* 도입 하는 `R` 포함 된 네임 스페이스 본문에서 멤버 선언에만 확장 되므로 `R` 두 번째 네임 스페이스 선언에서 알 수 없는 합니다. 그러나 배치 합니다 *using_alias_directive* 포함 된 컴파일 단위 하면 두 네임 스페이스 선언 내에서 사용할 수 있으려면 별칭:
```csharp
using R = N1.N2;

namespace N3
{
    class B: R.A {}
}

namespace N3
{
    class C: R.A {}
}
```

일반 멤버와 마찬가지로 이름으로 도입 *using_alias_directive*s 중첩 된 범위에서 이름이 비슷한 구성원이 숨겨집니다. 예제
```csharp
using R = N1.N2;

namespace N3
{
    class R {}

    class B: R.A {}        // Error, R has no member A
}
```
에 대 한 참조가 `R.A` 선언의 `B` 때문에 컴파일 타임 오류가 발생 `R` 가리킵니다 `N3.R`아니라 `N1.N2`합니다.

순서 *using_alias_directive*가 없는 성과의 해상도 기록 되는 *namespace_or_type_name* 에서 참조 하는 *using_alias_directive*영향을 받지 합니다 *using_alias_directive* 자체 또는 다른 *using_directive*위 컴파일 단위 또는 네임 스페이스 본문에서. 즉, 합니다 *namespace_or_type_name* 의 *using_alias_directive* 위 컴파일 단위 또는 네임 스페이스 본문 아니요 처럼 해결 됨 *using_directive*s입니다. A *using_alias_directive* 수 있지만 영향을 받는 *extern_alias_directive*위 컴파일 단위 또는 네임 스페이스 본문에서. 예제
```csharp
namespace N1.N2 {}

namespace N3
{
    extern alias E;

    using R1 = E.N;        // OK

    using R2 = N1;         // OK

    using R3 = N1.N2;      // OK

    using R4 = R2.N2;      // Error, R2 unknown
}
```
마지막 *using_alias_directive* 첫 번째 영향을 받지 않습니다 때문에 컴파일 타임 오류가 발생 *using_alias_directive*합니다. 첫 번째 *using_alias_directive* extern 별칭을 범위 이후 오류가 발생 하지 않습니다 `E` 포함 된 *using_alias_directive*합니다.

A *using_alias_directive* 표시는 네임 스페이스를 포함 하 여 형식이 나 네임 스페이스에 대 한 별칭을 만들 수 및 해당 네임 스페이스 내 모든 네임 스페이스 또는 형식에 중첩 합니다.

네임 스페이스 또는 형식 별칭을 통해 액세스 하는 네임 스페이스 또는 형식이 선언된 된 이름을 통해 액세스 하는 것과 동일한 결과 정확 하 게 생성 합니다. 예를 들어
```csharp
namespace N1.N2
{
    class A {}
}

namespace N3
{
    using R1 = N1;
    using R2 = N1.N2;

    class B
    {
        N1.N2.A a;            // refers to N1.N2.A
        R1.N2.A b;            // refers to N1.N2.A
        R2.A c;               // refers to N1.N2.A
    }
}
```
이름을 `N1.N2.A`, `R1.N2.A`, 및 `R2.A` 는 서로 동일 하며 모든 클래스를 참조할 정규화 된 이름이 `N1.N2.A`합니다.

별칭을 사용 하 여 폐쇄형된 생성된 형식, 이름 따르면 형식 인수를 제공 하지 않고는 언바운드 제네릭 형식 선언을 이름 수 없습니다. 예를 들어:
```csharp
namespace N1
{
    class A<T>
    {
        class B {}
    }
}

namespace N2
{
    using W = N1.A;          // Error, cannot name unbound generic type

    using X = N1.A.B;        // Error, cannot name unbound generic type

    using Y = N1.A<int>;     // Ok, can name closed constructed type

    using Z<T> = N1.A<T>;    // Error, using alias cannot have type parameters
}
```

### <a name="using-namespace-directives"></a>네임 스페이스 지시문을 사용 하 여

A *using_namespace_directive* 한정자 없이 사용할 각 유형에 대 한 식별자를 사용 하도록 설정 하는 바로 바깥쪽 컴파일 단위 또는 네임 스페이스 본문에는 네임 스페이스에 포함 된 형식을 가져옵니다.

```antlr
using_namespace_directive
    : 'using' namespace_name ';'
    ;
```

멤버 선언에서 컴파일 단위 또는 네임 스페이스 본문을 포함 하는 *using_namespace_directive*, 지정된 된 네임 스페이스에 포함 된 형식을 직접 참조할 수 있습니다. 예를 들어:
```csharp
namespace N1.N2
{
    class A {}
}

namespace N3
{
    using N1.N2;

    class B: A {}
}
```

위의 멤버 선언에서 합니다 `N3` 네임 스페이스의 형식 멤버가 `N1.N2` 직접 사용할 수 있고 따라서 클래스 `N3.B` 클래스에서 파생 되 `N1.N2.A`합니다.

A *using_namespace_directive* 특히 중첩 된 네임 스페이스를 가져오지 않습니다 하지만 지정된 된 네임 스페이스에 포함 된 형식을 가져옵니다. 예제
```csharp
namespace N1.N2
{
    class A {}
}

namespace N3
{
    using N1;

    class B: N2.A {}        // Error, N2 unknown
}
```
합니다 *using_namespace_directive* 에 포함 된 형식을 가져옵니다 `N1`에 중첩 된 네임 스페이스 하지 않지만 `N1`합니다. 따라서에 대 한 참조 `N2.A` 선언의 `B` 멤버가 라는 때문에 컴파일 타임 오류가 발생 `N2` 범위에 있습니다.

와 달리를 *using_alias_directive*, *using_namespace_directive* 식별자 바깥쪽 컴파일 단위 또는 네임 스페이스 본문 내에서 이미 정의 된 형식을 가져올 수 있습니다. 이름에서 가져온는 실제로 *using_namespace_directive* 바깥쪽 컴파일 단위 또는 네임 스페이스 본문에서 비슷한 이름의 멤버가 숨겨집니다. 예를 들어:
```csharp
namespace N1.N2
{
    class A {}

    class B {}
}

namespace N3
{
    using N1.N2;

    class A {}
}
```

멤버 선언에서 여기에는 `N3` 네임 스페이스 `A` 가리킵니다 `N3.A` 대신 `N1.N2.A`합니다.

둘 이상의 네임 스페이스 또는 형식으로 가져올 때 *using_namespace_directive*s 또는 *using_static_directive*같은 컴파일 단위 또는 네임 스페이스 본문에서의 형식이 동일한 이름에 대 한 참조 포함 해당 이름으로는 *type_name* 모호한 것으로 간주 됩니다. 예제
```csharp
namespace N1
{
    class A {}
}

namespace N2
{
    class A {}
}

namespace N3
{
    using N1;

    using N2;

    class B: A {}                // Error, A is ambiguous
}
```
둘 다 `N1` 및 `N2` 멤버를 포함 `A`, 이므로 `N3` 둘 다 참조를 가져옵니다 `A` 에서 `N3` 컴파일 시간 오류입니다. 이 이런 경우 충돌을 해결할 수 있습니다 하거나 한정자에 대 한 참조를 통해 `A`, 또는 도입 하 여는 *using_alias_directive* 특정을 선택 하는 `A`합니다. 예를 들어:
```csharp
namespace N3
{
    using N1;

    using N2;

    using A = N1.A;

    class B: A {}                // A means N1.A
}
```

또한 경우 둘 이상의 네임 스페이스 또는 형식에서 가져온 *using_namespace_directive*s 또는 *using_static_directive*같은 컴파일 단위 또는 네임 스페이스 본문에서의 형식이 나 멤버를 포함 합니다 이름이 같은 해당 이름으로 참조를 *simple_name* 모호한 것으로 간주 됩니다. 예제
```csharp
namespace N1
{
    class A {}
}

class C
{
    public static int A;
}

namespace N2
{
    using N1;
    using static C;

    class B
    {
        void M() 
        { 
            A a = new A();   // Ok, A is unambiguous as a type-name
            A.Equals(2);     // Error, A is ambiguous as a simple-name
        }
    }
}
```
`N1` 형식 멤버를 포함 `A`, 및 `C` 정적 메서드가 포함 `A`, 이므로 `N2` 참조를 둘 다 가져옵니다 `A` 로 *simple_name* 모호 하며 컴파일 타임에는 오류가 발생 했습니다. 

같은 *using_alias_directive*, *using_namespace_directive* 컴파일 단위 또는 네임 스페이스의 기본 선언 공간에 새 멤버를 제공 하지 않습니다 하지만 대신만 영향을 줌 합니다 컴파일 단위 또는 네임 스페이스 본문 나타나는입니다.

*namespace_name* 에서 참조 하는 *using_namespace_directive* 동일한 방식으로 해결 되는 *namespace_or_type_name* 에서 참조 하는  *using_alias_directive*합니다. 따라서 *using_namespace_directive*같은 컴파일 단위 또는 네임 스페이스 본문에서 서로 영향을 주지 않습니다 및 순서에 관계 없이 작성할 수 있습니다.

### <a name="using-static-directives"></a>Using 정적 지시문

A *using_static_directive* 중첩된 형식 및 되도록 각 멤버 및 형식 식별자를 사용 하도록 설정 하면 바로 바깥쪽 컴파일 단위 또는 네임 스페이스 본문에 형식 선언에 직접 포함 된 정적 멤버를 가져옵니다 자격 증명 없이 사용 합니다.

```antlr
using_static_directive
    : 'using' 'static' type_name ';'
    ;
```

멤버 선언에서 포함 된 컴파일 단위 또는 네임 스페이스 본문과 *using_static_directive*, 형식 및 선언에 직접 포함 된 확장 메서드) (제외 정적 멤버를 액세스할 수 있는 중첩는 지정 된 유형에 직접 참조할 수 있습니다. 예를 들어:

```csharp
namespace N1
{
    class A 
    {
        public class B{}
        public static B M(){ return new B(); }
    }
}

namespace N2
{
    using static N1.A;
    class C
    {
        void N() { B b = M(); }
    }
}
```

위의 멤버 선언에서 합니다 `N2` 정적 멤버 및 중첩 된 형식의 네임 스페이스 `N1.A` 직접 사용할 수 및 메서드 `N` 둘 다를 참조할 수는 `B` 및 `M` 의멤버`N1.A`.

A *using_static_directive* 특히 정적 메서드로 직접 확장 메서드를 가져오지 않습니다 하지만 확장 메서드 호출에 사용할 수 있게 ([확장 메서드 호출](expressions.md#extension-method-invocations)). 예제

```csharp
namespace N1 
{
    static class A 
    {
        public static void M(this string s){}
    }
}

namespace N2
{
    using static N1.A;

    class B
    {
        void N() 
        {
            M("A");      // Error, M unknown
            "B".M();     // Ok, M known as extension method
            N1.A.M("C"); // Ok, fully qualified
        }
    }
}
```
합니다 *using_static_directive* 확장 메서드를 가져옵니다 `M` 에 포함 된 `N1.A`, 하지만 확장 메서드로 합니다. 따라서 첫 번째 참조 `M` 의 본문에 `B.N` 멤버가 라는 때문에 컴파일 타임 오류가 발생 `M` 범위에 있습니다.

A *using_static_directive* 데이터만 가져옵니다 멤버 및 유형이 지정된 된 형식에서 직접 선언 된 기본 클래스에서 선언 된 멤버 및 유형이 없습니다.

TODO: 예제

여러 간의 모호성 *using_namespace_directives* 하 고 *using_static_directives* 에 설명 되어 [네임 스페이스 지시문을 사용 하 여](namespaces.md#using-namespace-directives)입니다.

## <a name="namespace-members"></a>Namespace 멤버

A *namespace_member_declaration* 이 *namespace_declaration* ([Namespace 선언](namespaces.md#namespace-declarations)) 또는 *type_declaration* ( [형식 선언을](namespaces.md#type-declarations)).

```antlr
namespace_member_declaration
    : namespace_declaration
    | type_declaration
    ;
```

컴파일 단위 또는 네임 스페이스 본문을 포함할 수 있습니다 *namespace_member_declaration*및 이러한 선언은 새 멤버를 포함 하는 컴파일 단위 또는 네임 스페이스 본문의 기본 선언 공간 참여 합니다.

## <a name="type-declarations"></a>형식 선언

A *type_declaration* 되는 *class_declaration* ([클래스 선언을](classes.md#class-declarations)), *struct_declaration* ([구조체 선언](structs.md#struct-declarations)), *interface_declaration* ([인터페이스 선언](interfaces.md#interface-declarations)), *enum_declaration* ([열거형 선언](enums.md#enum-declarations)), 또는 *delegate_declaration* ([대리자 선언](delegates.md#delegate-declarations)).

```antlr
type_declaration
    : class_declaration
    | struct_declaration
    | interface_declaration
    | enum_declaration
    | delegate_declaration
    ;
```

A *type_declaration* 컴파일 단위에서 최상위 선언 또는 네임 스페이스, 클래스 또는 구조체 내에서 멤버 선언으로 발생할 수 있습니다.

때 형식에 대 한 형식 선언을 `T` 발생 컴파일 단위에 최상위 선언으로 새로 선언 된 형식의 정규화 된 이름을 단순히 `T`합니다. 때 형식에 대 한 형식 선언을 `T` 클래스 또는 구조체는 정규화 된 이름 새로 선언 된 형식의 네임 스페이스 내에서 발생 `N.T`여기서 `N` 포함 된 네임 스페이스, 클래스 또는 구조체의 정규화 된 이름입니다.

클래스 내에서 선언 된 형식 또는 구조체에는 중첩된 형식 이라고 합니다. ([중첩 형식은](classes.md#nested-types)).

허용 되는 액세스 한정자 및 형식 선언에 대 한 기본 액세스는 선언이 발생 컨텍스트에 따라 ([접근성을 선언](basic-concepts.md#declared-accessibility)):

*  컴파일 단위 또는 네임 스페이스에 선언 된 형식을 가질 수 있습니다 `public` 또는 `internal` 액세스 합니다. 기본값은 `internal` 액세스 합니다.
*  클래스에 선언 된 형식을 가질 수 있습니다 `public`, `protected internal`를 `protected`합니다 `internal`, 또는 `private` 액세스 합니다. 기본값은 `private` 액세스 합니다.
*  구조체에 선언 된 형식을 가질 수 있습니다 `public`하십시오 `internal`, 또는 `private` 액세스 합니다. 기본값은 `private` 액세스 합니다.

## <a name="namespace-alias-qualifiers"></a>Namespace 별칭 한정자

합니다 ***네임 스페이스 별칭 한정자*** `::` 가능 형식 이름을 조회 새 형식과 멤버 미치는 영향을 받지 않습니다을 보장 합니다. 네임 스페이스 별칭 한정자는 항상 왼쪽 및 오른쪽 식별자 라고 하는 두 식별자 사이 표시 됩니다. 일반 달리 `.` 한정자, 왼쪽의 식별자는 `::` 한정자 조회는 extern 또는 별칭을 사용 하 여 으로만 위쪽.

A *qualified_alias_member* 다음과 같이 정의 됩니다.

```antlr
qualified_alias_member
    : identifier '::' identifier type_argument_list?
    ;
```

A *qualified_alias_member* 으로 사용할 수는 *namespace_or_type_name* ([Namespace 및 형식 이름](basic-concepts.md#namespace-and-type-names)) 또는의 왼쪽된 피연산자는 *member_access* ([멤버 액세스](expressions.md#member-access)).

A *qualified_alias_member* 에 두 가지 형식 중 하나:

*  `N::I<A1, ..., Ak>`여기서 `N` 하 고 `I` 식별자를 나타내는 및 `<A1, ..., Ak>` 형식 인수 목록입니다. (`K` 이 항상 하나 이상 있습니다.)
*  `N::I`여기서 `N` 및 `I` 식별자를 나타냅니다. (이 예제의 경우 `K` 0으로 간주 됩니다.)

의미는이 표기법을 사용 하는 *qualified_alias_member* 다음과 같이 결정 됩니다.

*  하는 경우 `N` 식별자 `global`, 전역 네임 스페이스에 대 한 검색은 `I`:
   * 전역 네임 스페이스 라는 네임 스페이스를 포함 하는 경우 `I` 하 고 `K` 가 0 이면 해당 *qualified_alias_member* 네임 스페이스를 참조 합니다.
   * 전역 네임 스페이스 이라는 제네릭이 아닌 형식을 포함 하는 경우 그러지 `I` 하 고 `K` 가 0 이면 해당 *qualified_alias_member* 해당 형식을 참조 합니다.
   * 전역 네임 스페이스에는 명명 된 형식을 포함 하는 경우 그러지 `I` 있는 `K` 매개 변수를 입력 하면 *qualified_alias_member* 지정 된 형식 인수를 사용 하 여 생성 하는 형식을 참조 합니다.
   * 이 고, 그렇지 합니다 *qualified_alias_member* 가 정의 되지 않은 하 고 컴파일 시간 오류가 발생 합니다.

*  네임 스페이스 선언을 사용 하 여 시작이 고, 그렇지 ([Namespace 선언](namespaces.md#namespace-declarations)) 즉시를 포함 하는 *qualified_alias_member* (있는 경우), 각 바깥쪽 네임 스페이스 선언을 사용 하 여 계속 (해당 되는 경우), 및 포함 된 컴파일 단위를 사용 하 여 종료 합니다 *qualified_alias_member*, 엔터티를 찾을 때까지 다음 단계를 실행:

   * 네임 스페이스 선언 또는 컴파일 단위를 포함 하는 경우는 *using_alias_directive* 연결 하는 `N` 형식과 해당 *qualified_alias_member* 정의 되지 않습니다 및 컴파일 타임 오류가 발생합니다.
   * 네임 스페이스 선언 또는 컴파일 단위를 포함 하는 경우는 *extern_alias_directive* 하거나 *using_alias_directive* 연결 하는 `N` 다음 네임 스페이스로:
     * 와 연결 된 네임 스페이스 `N` 라는 네임 스페이스를 포함 `I` 및 `K` 가 0 이면 해당 *qualified_alias_member* 네임 스페이스를 참조 합니다.
     * 네임 스페이스와 연결 된 경우 `N` 이라는 제네릭이 아닌 형식을 포함 `I` 하 고 `K` 가 0 이면 해당 *qualified_alias_member* 해당 형식을 참조 합니다.
     * 네임 스페이스와 연결 된 경우 `N` 이라는 형식을 포함 `I` 포함 `K` 매개 변수를 입력 하면 *qualified_alias_member* 지정 된 형식의 생성 된 해당 형식을 참조 인수입니다.
     * 이 고, 그렇지 합니다 *qualified_alias_member* 가 정의 되지 않은 하 고 컴파일 시간 오류가 발생 합니다.
*  이 고, 그렇지 합니다 *qualified_alias_member* 가 정의 되지 않은 하 고 컴파일 시간 오류가 발생 합니다.

Note 형식을 참조 하는 별칭을 사용 하 여 네임 스페이스 별칭 한정자를 사용 하면 컴파일 타임 오류가 발생 합니다. 참고 경우 식별자 `N` 됩니다 `global`, 경우에 연결 별칭을 조회 전역 네임 스페이스에서 수행 됩니다 `global` 형식 또는 네임 스페이스를 사용 하 여 합니다.

### <a name="uniqueness-of-aliases"></a>별칭의 고유성

각 컴파일 단위 및 네임 스페이스 본문에 extern 별칭에 대 한 별도 선언 공간 및 별칭을 사용 합니다. 따라서 extern 별칭 또는 별칭을 사용 하 여 이름을 extern 별칭의 집합 내에서 고유 해야 하는 동안 즉시 포함 된 컴파일 단위 또는 네임 스페이스 본문에 선언 된 별칭을 사용 하 여 별칭 대체가 형식 또는 네임 스페이스도 동일한 이름을 가질 수 있습니까 t에만 사용 되는 `::` 한정자입니다.

예제
```csharp
namespace N
{
    public class A {}

    public class B {}
}

namespace N
{
    using A = System.IO;

    class X
    {
        A.Stream s1;            // Error, A is ambiguous

        A::Stream s2;           // Ok
    }
}
```
이름을 `A` 때문에 두 번째 네임 스페이스 본문에서 두 가지 의미는 모두 클래스 `A` 여와 별칭 `A` 범위입니다. 이러한 이유로 사용 `A` 정규화 된 이름의 `A.Stream` 모호 하며 되려면 컴파일 타임 오류가 발생 합니다. 그러나 사용 `A` 사용 하 여 합니다 `::` 한정자 아니므로 오류 `A` 네임 스페이스 별칭 으로만 조회 합니다.
