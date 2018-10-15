# <a name="basic-concepts"></a>기본 개념

## <a name="application-startup"></a>응용 프로그램 시작

가진 어셈블리에는 ***진입점*** 호출 되는 ***응용 프로그램***합니다. 응용 프로그램은 새를 실행 하는 경우 ***응용 프로그램 도메인*** 만들어집니다. 응용 프로그램의 여러 다른 인스턴스화를 동시에 동일한 컴퓨터에 있을 수 있고 각 고유한 응용 프로그램 도메인입니다.

응용 프로그램 상태에 대 한 컨테이너 역할을 하 여 응용 프로그램 격리를 활성화 하는 응용 프로그램 도메인입니다. 응용 프로그램 도메인 컨테이너 및 응용 프로그램에서 사용 하는 클래스 라이브러리에 정의 된 형식에 대 한 경계 역할도 합니다. 형식을 로드 한 응용 프로그램 도메인에 형식이 같은 다른 응용 프로그램 도메인에 로드와 다릅니다. 및 개체의 인스턴스 직접 응용 프로그램 도메인 간에 공유 되지 않습니다. 예를 들어, 각 응용 프로그램 도메인에 이러한 형식에 대 한 정적 변수의 자체 복사본이 및 유형에 대 한 정적 생성자 응용 프로그램 도메인당 한 번만 실행 됩니다. 구현을 자유롭게 응용 프로그램 도메인의 생성과 대 한 구현 별 정책 또는 메커니즘을 제공할 수 있습니다.

***응용 프로그램 시작*** 실행 환경에서 응용 프로그램의 진입점으로 참조 되는 지정 된 메서드를 호출할 때 발생 합니다. 이 진입점 메서드 이름은 항상 `Main`, 다음 서명 중 하나일 수 있습니다.

```csharp
static void Main() {...}

static void Main(string[] args) {...}

static int Main() {...}

static int Main(string[] args) {...}
```

표시 된 대로 진입점 선택적으로 반환할 수 있습니다는 `int` 값입니다. 이 반환 값을 응용 프로그램 종료에서 사용 ([응용 프로그램 종료](basic-concepts.md#application-termination)).

진입점 필요에 따라 하나의 형식 매개 변수가 있을 수 있습니다. 매개 변수 이름을 지정할 수 있지만 매개 변수 형식의 해야 `string[]`합니다. 실행 환경을 만들고 전달 정식 매개 변수가 있는 경우는 `string[]` 인수는 명령줄 인수를 포함 하는 응용 프로그램이 시작 된 경우를 지정 합니다. `string[]` 인수가 null 되지 않지만 명령줄 인수 없이 지정 된 경우 길이가 0 수 있습니다.

C#는 메서드 오버 로딩을 지원 하므로 클래스 또는 구조체를 포함할 수 있습니다 일부 메서드의 정의가 여러 개 제공 각 메서드의 서명이 다릅니다. 그러나 하나의 프로그램 내에서 클래스 또는 구조체 없습니다 포함 될 수 있습니다 호출 하는 메서드가 둘 이상 `Main` 정의가 한정 응용 프로그램 진입점으로 사용할 수 있도록 합니다. 하지만 다른 오버 로드 된 버전의 `Main` 는 허용 둘 이상의 매개 변수를 나가 유일한 매개 변수는 형식이 아닌 제공 `string[]`합니다.

응용 프로그램의 여러 클래스 또는 구조체 수 있습니다. 라는 메서드를 포함 하도록 이러한 클래스나 구조체의 두 개 이상의 가능성이 `Main` 정의가 한정 응용 프로그램 진입점으로 사용할 수 있도록 합니다. 이러한 경우에 외부 메커니즘 (예: 명령줄 컴파일러 옵션) 다음 중 하나를 선택 하려면 사용 해야 `Main` 진입점 메서드.

C#에서 모든 메서드는 클래스 또는 구조체의 멤버로 정의 되어야 합니다. 일반적으로 선언 된 접근성 ([접근성을 선언](basic-concepts.md#declared-accessibility)) 메서드의 액세스 한정자에 의해 결정 됩니다 ([액세스 한정자](classes.md#access-modifiers))에 선언과 마찬가지로 선언 된 지정 형식의 액세스 가능성은 해당 선언에 지정 된 액세스 한정자에 의해 결정 됩니다. 순서로 지정 된 형식의 지정 된 메서드를 호출할 수, 형식 및 멤버를 모두 액세스할 수 있어야 합니다. 그러나 응용 프로그램 진입점이 특별 한 경우. 특히, 실행 환경에는 해당 선언 된 접근성에 관계 없이 및 해당 바깥쪽 형식 선언에 선언 된 접근성에 관계 없이 응용 프로그램의 진입점을 액세스할 수 있습니다.

응용 프로그램 진입점 메서드는 제네릭 클래스 선언에서 되지 않을 수 있습니다.

다른 모든 측면에서 진입점 메서드의 진입점이 아닌 것 처럼 동작 합니다.

## <a name="application-termination"></a>응용 프로그램 종료

***응용 프로그램 종료*** 실행 환경에 컨트롤을 반환 합니다.

응용 프로그램의 반환 형식이 ***진입점*** 메서드는 `int`, 반환 되는 값은 응용 프로그램의 역할도 ***종료 상태 코드***합니다. 이 코드의 목적은 성공 또는 실패를 실행 환경으로의 통신을 허용 하는 것입니다.

진입점 메서드 반환 형식의 경우 `void`, 오른쪽 중괄호에 도달 (`}`)를 종료 하는 메서드 또는 실행을 `return` 종료 상태 코드에 없는 식이 포함 된 문의 결과 `0`합니다.

응용 프로그램의 종료 하기 전에 모든 아직 가비지 수집 되지 않은 개체에 대 한 소멸자는 호출 이러한 정리 억제 하지 않는 한 (라이브러리 메서드를 호출 하 여 `GC.SuppressFinalize`예를 들어).

## <a name="declarations"></a>선언

프로그램의 구성 요소를 정의 하는 C# 프로그램의 선언입니다. C# 프로그램이 구성 되는 네임 스페이스를 사용 하 여 ([네임 스페이스](namespaces.md)), 형식을 포함할 수 있는 선언 및 중첩 된 네임 스페이스 선언 합니다. 형식 선언 ([형식 선언을](namespaces.md#type-declarations)) 클래스를 정의 하는 데 사용 됩니다 ([클래스](classes.md)), 구조체 ([구조체](structs.md)), 인터페이스 ([인터페이스](interfaces.md) )를 열거형 ([열거형](enums.md)), 및 대리자 ([대리자](delegates.md)). 형식 선언의 형식에서 형식 선언에 허용 되는 멤버의 종류에 따라 달라 집니다. 예를 들어, 클래스 선언 상수에 대 한 선언을 포함할 수 있습니다 ([상수](classes.md#constants)), 필드 ([필드](classes.md#fields)), 메서드 ([메서드](classes.md#methods)), 속성 ([ 속성](classes.md#properties)), 이벤트 ([이벤트](classes.md#events)), 인덱서 ([인덱서](classes.md#indexers)), 연산자 ([연산자](classes.md#operators)), 인스턴스 생성자 ([ 인스턴스 생성자](classes.md#instance-constructors)), 정적 생성자 ([정적 생성자](classes.md#static-constructors)), 소멸자 ([소멸자](classes.md#destructors)), 중첩 형식 및 ([중첩 형식은](classes.md#nested-types)).

선언에서 이름을 정의 합니다 ***선언 공간*** 선언 속한 합니다. 제외 하 고 멤버를 오버 로드 된 ([시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading)), 선언 공간에서 동일한 이름 가진 멤버를 정의 하는 두 개 이상의 선언이 있어야 하면 컴파일 타임 오류가 발생 합니다. 다양 한 같은 이름 가진 멤버를 포함 하도록 선언 공간에는 것이 불가능 합니다. 예를 들어 선언 공간을 포함할 수 있습니다 하지 메서드와 필드를 같은 이름으로.

다음에 설명 된 대로 여러 가지 선언 공백이 있습니다.

*  프로그램의 모든 소스 파일 내의 *namespace_member_declaration*없습니다 바깥쪽 s *namespace_declaration* 이라는 단일 결합 된 선언 공간의 멤버인는 ***전역 선언 공간***입니다.
*  프로그램의 모든 소스 파일 내의 *namespace_member_declaration*내 *namespace_declaration*정규화 된 네임 스페이스 이름이 포함 된 단일 결합 된 선언의 멤버인 공간입니다.
*  각 클래스, 구조체 또는 인터페이스 선언에는 새 선언 공간을 만듭니다. 이름을 통해이 선언 공간에 도입 된 *class_member_declaration*개이면 *struct_member_declaration*개이면 *interface_member_declaration*s, 또는 *type_parameter*s입니다. 오버 로드 된 인스턴스 생성자를 제외 하 고 선언 및 정적 생성자 선언, 클래스 또는 구조체는 클래스 또는 구조체와 같은 이름 사용 하는 멤버 선언이 포함할 수 없습니다. 클래스, 구조체 또는 인터페이스의 오버 로드 된 메서드 및 인덱서 선언이 허용 합니다. 또한 클래스 또는 구조체 선언의 인스턴스 오버 로드 된 생성자 및 연산자를 허용합니다. 예를 들어, 클래스, 구조체 또는 인터페이스 선언을 포함할 수 있습니다 여러 메서드는 동일한 이름 가진 이러한 메서드 선언은 해당 서명을 다른 제공 ([시그니처 및 오버 로드](basic-concepts.md#signatures-and-overloading)). 기본 클래스는 클래스의 선언 공간에 영향을 주지를 기본 인터페이스는 인터페이스 선언 공간에 영향을 주지 note 합니다. 따라서 파생된 클래스 또는 인터페이스를 상속된 된 멤버와 동일한 이름 가진 멤버를 선언할 수입니다. 이러한 멤버 라고 ***숨기기*** 상속 된 멤버입니다.
*  각 대리자 선언을 새 선언 공간을 만듭니다. 정식 매개 변수를 통해이 선언 공간에 도입 된 이름 (*fixed_parameter*s 및 *parameter_array*s) 및 *type_parameter*s입니다.
*  각 열거형 선언은 새 선언 공간을 만듭니다. 이름을 통해이 선언 공간에 도입 된 *enum_member_declarations*합니다.
*  각 메서드 선언, 인덱서, 연산자 선언, 인스턴스 생성자 선언 선언과 익명 함수 라는 새 선언 공간을 만듭니다는 ***지역 변수 선언 공간***입니다. 정식 매개 변수를 통해이 선언 공간에 도입 된 이름 (*fixed_parameter*s 및 *parameter_array*s) 및 *type_parameter*s입니다. 함수 멤버 또는 익명 함수 본문에 있는 경우 지역 변수 선언 공간 내에 중첩 될으로 간주 됩니다. 이 지역 변수 선언 공간 및 동일한 이름 가진 요소를 포함 하는 중첩 된 지역 변수 선언 공간에 대 한 오류입니다. 따라서 중첩 된 선언 공간 내에서 수 없는 바깥쪽 선언 공간에서 로컬 변수 또는 지역 변수와 동일한 이름을 가진 상수 또는 상수를 선언 합니다. 두 선언 공간을 모두 선언 공간 다른 값을 포함으로 동일한 이름 가진 요소를 포함 하는 것이 가능 합니다.
*  각 *블록* 또는 *switch_block* , 뿐만 *에 대 한*를 *foreach* 하 고 *사용 하 여* 문을 만듭니다는 지역 변수 및 지역 상수에 대 한 지역 변수 선언 공간입니다. 이름을 통해이 선언 공간에 도입 된 *local_variable_declaration*s 및 *local_constant_declaration*s입니다. 블록 또는 함수 멤버 또는 익명 함수 본문 내에서 발생 하는 해당 매개 변수에 대 한 함수로 선언 된 지역 변수 선언 공간 내에서 중첩 되는 note 합니다. 즉 로컬 변수와 이름이 같은 매개 변수를 사용 하 여 메서드가 있으면 오류가 표시 됩니다.
*  각 *블록* 하거나 *switch_block* 레이블에 대 한 별도 선언 공간을 만듭니다. 이름을 통해이 선언 공간에 도입 된 *labeled_statement*및 이름을 통해 참조 되 *goto_statement*s입니다. 합니다 ***선언 공간 레이블을*** 블록의 모든 중첩 된 블록을 포함 합니다. 따라서 중첩된 된 블록 내에서 수 없는 바깥쪽 블록의 레이블로 동일한 이름 사용 하 여 레이블을 선언 합니다.

이름이 선언 되는 텍스트 순서는 일반적으로 중요 하지 않습니다. 특히 텍스트 순서 선언 및 네임 스페이스, 상수, 메서드, 속성, 이벤트, 인덱서, 연산자, 인스턴스 생성자, 소멸자, 정적 생성자 및 형식 사용에 대 한 중요 하지 않습니다. 선언 순서는 다음과 같은 방법에서 중요 합니다.

*  필드 선언 및 지역 변수 선언에 대 한 선언 순서 대로 (있는 경우) 해당 이니셜라이저가 실행 되는 순서를 결정 합니다.
*  지역 변수는 사용 하기 전에 정의 되어야 합니다 ([범위](basic-concepts.md#scopes)).
*  열거형 멤버 선언에 대 한 선언 순서 대로 ([열거형 멤버](enums.md#enum-members)) 때 상당한 *constant_expression* 값이 생략 됩니다.

네임 스페이스의 선언 공간 "종료"를 열고 두 네임 스페이스 정규화 된 이름이 같은 선언이 동일한 선언 공간 됩니다. 예
```csharp
namespace Megacorp.Data
{
    class Customer
    {
        ...
    }
}

namespace Megacorp.Data
{
    class Order
    {
        ...
    }
}
```

이 경우 정규화 된 이름 사용 하 여 두 개의 클래스를 선언으로 동일한 선언 공간에 영향을 위의 두 가지 네임 스페이스 선언 `Megacorp.Data.Customer` 고 `Megacorp.Data.Order`입니다. 두 선언이 동일한 선언 공간, 때문에 발생할 수 컴파일 타임 오류를 각각 동일한 이름 가진 클래스의 선언을 포함 하는 경우.

위에 지정 된 대로 선언 공간 블록의 모든 중첩 된 블록을 포함합니다. 따라서 다음 예제에에서는 `F` 및 `G` 때문에 컴파일 타임 오류가 발생 되는 메서드 이름을 `i` 바깥쪽 블록에서 선언 되 고 내부 블록에 다시 선언할 수 없습니다. 그러나를 `H` 하 고 `I` 이후 두 메서드는 유효한 `i`의 별도 중첩 되지 않은 블록에서 선언 됩니다.

```csharp
class A
{
    void F() {
        int i = 0;
        if (true) {
            int i = 1;            
        }
    }

    void G() {
        if (true) {
            int i = 0;
        }
        int i = 1;                
    }

    void H() {
        if (true) {
            int i = 0;
        }
        if (true) {
            int i = 1;
        }
    }

    void I() {
        for (int i = 0; i < 10; i++)
            H();
        for (int i = 0; i < 10; i++)
            H();
    }
}
```

## <a name="members"></a>멤버

네임 스페이스 및 형식에는 ***멤버***합니다. 엔터티의 멤버 뒤에 엔터티에 대 한 참조를 사용 하 여 시작 하는 정규화 된 이름을 사용 하 여 일반 공급 되는 "`.`" 토큰, 멤버의 이름 뒤에.

형식의 멤버는 형식 선언에서 선언 하거나 또는 ***상속*** 형식의 기본 클래스입니다. 기본 클래스에서 상속 되는 형식, 파생 된 형식의 멤버로 인스턴스 생성자, 소멸자 및 정적 생성자를 제외 하 고 기본 클래스의 모든 멤버에 표시 합니다. 기본 클래스 멤버의 선언 된 접근성이 멤버의 상속 여부를 제어 하지는 않습니다-상속 인스턴스 생성자, 정적 생성자 또는 소멸자가 없는 멤버를 확장 합니다. 그러나 상속된 된 멤버를 해당 선언 된 접근성 때문 하거나 파생된 형식에서 액세스할 수 없습니다 ([접근성을 선언](basic-concepts.md#declared-accessibility)) 또는 형식 자체에서 선언에 의해 숨겨져 있기 때문에 ([통해 숨기기 상속](basic-concepts.md#hiding-through-inheritance)).

### <a name="namespace-members"></a>Namespace 멤버

네임 스페이스 및 형식 바깥쪽 네임 스페이스에는의 멤버는 ***전역 네임 스페이스***합니다. 이 전역 선언 공간에 선언 된 이름에 직접 해당 합니다.

네임 스페이스 및 네임 스페이스 내에 선언 된 유형에 해당 네임 스페이스의 멤버입니다. 이 네임 스페이스의 선언 공간에 선언 된 이름에 직접 해당 합니다.

네임스페이스에는 액세스 제한이 없습니다. Private, protected 또는 internal 네임 스페이스를 선언 하는 것이 불가능 하 고 네임 스페이스 이름은 항상 공개적으로 액세스할 수 있습니다.

### <a name="struct-members"></a>구조체 멤버

구조체의 멤버는 구조체에서 선언 된 멤버와 구조체의 직접 기본 클래스에서 상속 된 멤버 `System.ValueType` 간접 기본 클래스 및 `object`합니다.

단순 형식의 멤버 단순 유형에 따라 구조체 형식 별칭의 멤버에 직접 해당합니다.

*  멤버 `sbyte` 의 멤버는 `System.SByte` 구조체입니다.
*  멤버 `byte` 의 멤버는 `System.Byte` 구조체입니다.
*  멤버 `short` 의 멤버는 `System.Int16` 구조체입니다.
*  멤버 `ushort` 의 멤버는 `System.UInt16` 구조체입니다.
*  멤버 `int` 의 멤버는 `System.Int32` 구조체입니다.
*  멤버 `uint` 의 멤버는 `System.UInt32` 구조체입니다.
*  멤버 `long` 의 멤버는 `System.Int64` 구조체입니다.
*  멤버 `ulong` 의 멤버는 `System.UInt64` 구조체입니다.
*  멤버 `char` 의 멤버는 `System.Char` 구조체입니다.
*  멤버 `float` 의 멤버는 `System.Single` 구조체입니다.
*  멤버 `double` 의 멤버는 `System.Double` 구조체입니다.
*  멤버 `decimal` 의 멤버는 `System.Decimal` 구조체입니다.
*  멤버 `bool` 의 멤버는 `System.Boolean` 구조체입니다.

### <a name="enumeration-members"></a>열거형 멤버

열거형의 멤버는 열거형의 선언 된 상수 및 열거형의 직접 기본 클래스에서 상속 된 멤버 `System.Enum` 및 간접 기본 클래스 `System.ValueType` 고 `object`입니다.

### <a name="class-members"></a>클래스 멤버

클래스의 멤버는 클래스에서 선언 된 멤버 및 기본 클래스에서 상속 된 멤버 (클래스를 제외 하 고 `object` 있는 기본 클래스 없음). 기본 클래스에서 상속 된 멤버는 상수, 필드, 메서드, 속성, 이벤트, 인덱서, 연산자 및 유형의 기본 클래스인 하지만 하지는 인스턴스 생성자, 소멸자 및 기본 클래스의 정적 생성자를 포함 합니다. 기본 클래스 멤버의 액세스 가능성에 관계 없이 상속 됩니다.

클래스 선언에는 상수, 필드, 메서드, 속성, 이벤트, 인덱서, 연산자, 인스턴스 생성자, 소멸자, 정적 생성자 및 형식 선언을 포함할 수 있습니다.

멤버 `object` 고 `string` 해당 클래스 형식의 멤버에 직접 해당 별칭:

*  멤버 `object` 의 멤버는 `System.Object` 클래스입니다.
*  멤버 `string` 의 멤버는 `System.String` 클래스입니다.

### <a name="interface-members"></a>인터페이스 멤버

인터페이스의 멤버는 인터페이스의 모든 기본 인터페이스 및 인터페이스에서 선언 된 멤버입니다. 클래스 멤버 `object` 엄격 하 게 말하자면 모든 인터페이스의 멤버를 하지 않습니다 ([인터페이스 멤버](interfaces.md#interface-members)). 그러나 클래스 멤버 `object` 임의의 인터페이스 형식에서 멤버 조회를 통해 사용할 수 있습니다 ([멤버 조회](expressions.md#member-lookup)).

### <a name="array-members"></a>배열 멤버

배열 멤버는 클래스에서 상속 된 멤버 `System.Array`합니다.

### <a name="delegate-members"></a>대리자 멤버

대리자는 클래스에서 상속 된 멤버 `System.Delegate`합니다.

## <a name="member-access"></a>멤버 액세스

멤버 액세스 제어를 허용 하는 멤버를 선언 합니다. 멤버의 액세스 가능성 선언 된 액세스 가능성에 의해 설정 됩니다 ([접근성을 선언](basic-concepts.md#declared-accessibility)) 멤버의 결합 된 위 형식의 액세스 가능성을 가진 경우입니다.

특정 멤버에 대 한 액세스 허용 되 면 멤버 라고 ***액세스할 수 있는***합니다. 반대로, 특정 멤버에 대 한 액세스 허용 되지 않는 경우 멤버 라고 ***액세스할 수 없는***합니다. 텍스트 위치는 액세스가 이루어지는 액세스 가능 도메인에 포함 되 면 멤버에 대 한 액세스가 허용 됩니다 ([접근성 도메인](basic-concepts.md#accessibility-domains)) 멤버입니다.

### <a name="declared-accessibility"></a>선언된 액세스 가능성

합니다 ***접근성을 선언*** 의 구성원은 다음 중 하나일 수 있습니다.

*  가 포함 하 여 선택 하는 공용을 `public` 멤버 선언에서 한정자입니다. 직관적인 의미 `public` "액세스가 제한 되지 않음" 됩니다.
*  포함 하 여 선택 되어 보호는 `protected` 멤버 선언에서 한정자입니다. 직관적인 의미 `protected` "포함 하는 클래스 또는 형식에 대해서만 액세스 클래스에서 파생 되는 포함 하 는".
*  가 포함 하 여 선택 하는 내부는 `internal` 멤버 선언에서 한정자입니다. 직관적인 의미 `internal` "이이 프로그램에 대해서만 액세스"가 있습니다.
*  내부 (즉 protected 또는 internal), 보호 모두를 포함 하 여 선택 하는 `protected` 및 `internal` 멤버 선언에서 한정자입니다. 직관적인 의미 `protected internal` "이이 프로그램에 대해서만 액세스 또는 포함 하는 클래스에서 파생 된 형식"입니다.
*  가 포함 하 여 선택 하는 개인을 `private` 멤버 선언에서 한정자입니다. 직관적인 의미 `private` "액세스를 포함 하는 형식 제한" 됩니다.

멤버 선언이 발생 하는 컨텍스트에 따라, 특정 형식의 선언 된 접근성만 허용 됩니다. 또한 멤버 선언 액세스 한정자를 포함 하지 않습니다는 선언이 발생 하는 컨텍스트 선언 된 기본을 결정 합니다.

*  네임 스페이스에서는 암시적으로 있음 `public` 접근성을 선언 합니다. 액세스 한정자가 없습니다 네임 스페이스 선언에서 허용 됩니다.
*  컴파일 단위 또는 네임 스페이스에 선언 된 형식을 가질 수 있습니다 `public` 나 `internal` 내게 필요한 옵션 및 기본적으로 선언 된 `internal` 접근성을 선언 합니다.
*  클래스 멤버 선언 된 액세스 가능성의 다섯 가지 종류 중 하나를 포함할 수 있으며 기본적으로 `private` 접근성을 선언 합니다. (형식 선언 클래스의 멤버는 5 가지 선언 된 접근성 중 하나일 수 있습니다 하는 대로 네임 스페이스의 멤버 수만 있는 선언 된 형식은 `public` 또는 `internal` 접근성을 선언 합니다.)
*  구조체 멤버를 가질 수 있습니다 `public`, `internal`, 또는 `private` 내게 필요한 옵션 및 기본적으로 선언 된 `private` 구조체는 암시적으로 봉인 되므로 접근성을 선언 합니다. 구조체 멤버 (즉, 해당 구조체에서 상속 되지 않습니다) 구조체에서 도입 된 사용할 수 없습니다 `protected` 또는 `protected internal` 접근성을 선언 합니다. (구조체의 멤버 수 있는 형식을 선언 `public`, `internal`, 또는 `private` 네임 스페이스의 멤버 수만 있는 선언 된 형식은 접근성을 선언 `public` 또는 `internal` 접근성을 선언 합니다.)
*  인터페이스 멤버를 암시적으로 사용할 `public` 접근성을 선언 합니다. 액세스 한정자가 없습니다 인터페이스 멤버 선언에서 허용 됩니다.
*  열거형 멤버를 암시적으로 있는 `public` 접근성을 선언 합니다. 액세스 한정자가 없습니다 열거형 멤버 선언에서 허용 됩니다.

### <a name="accessibility-domains"></a>접근성 도메인

합니다 ***접근성 도메인*** 멤버의 프로그램 텍스트 멤버에 대 한 액세스 허용 됩니다 (분리 된) 섹션 구성 됩니다. 멤버의 액세스 가능성 도메인을 정의 하는 용도로 멤버 라고 ***최상위*** 형식에 선언 하지 않은 경우 멤버 라고 ***중첩*** 다른 형식 내에서 선언 되는 경우. 또한 합니다 ***프로그램 텍스트*** 모든 프로그램에 포함 된 텍스트 형식의 프로그램 텍스트를 정의 하 고 프로그램의 모든 소스 파일에 포함 된 텍스트를 프로그래밍 하는 모든 정의 된 프로그램의는 *type_declaration*등, 필요에 따라 형식 내에서 중첩 된 형식을 해당 형식의 합니다.

미리 정의 된 형식의 액세스 가능 도메인 (같은 `object`, `int`, 또는 `double`) 제한 되지 않습니다.

최상위의 접근성 도메인 형식 바인딩되지 않은 `T` ([바인딩되며 형식에 바인딩되지 않은](types.md#bound-and-unbound-types)) 프로그램에 선언 된 `P` 다음과 같이 정의 됩니다.

*  경우 선언된 된 접근성 `T` 됩니다 `public`의 접근성 도메인 `T` 의 프로그램 텍스트입니다 `P` 및 참조 하는 프로그램 `P`합니다.
*  `T`에 대해 선언된 액세스 가능성이 `internal`인 경우 `T`의 액세스 가능 도메인은 `P`의 프로그램 텍스트입니다.

이러한 정의 바인딩되지 않은 최상위 형식의 액세스 가능 도메인은 항상 최소한 다음을 입력 하는 프로그램의 프로그램 텍스트 선언 됩니다.

생성된 된 형식에 대 한 액세스 가능성 도메인 `T<A1, ..., An>` 언바운드 제네릭 형식의 액세스 가능 도메인의 교집합 `T` , 형식 인수의 접근성 도메인 `A1, ..., An`합니다.

중첩 된 멤버의 접근성 도메인 `M` 형식에서 선언 `T` 프로그램 내 `P` 다음과 같이 정의 됩니다 (에 `M` 자체 형식 되었을 수 있습니다).

*  `M`에 대해 선언된 액세스 가능성이 `public`인 경우 `M`의 액세스 가능 도메인은 `T`의 액세스 가능 도메인입니다.
*  경우 선언된 된 접근성 `M` 됩니다 `protected internal`, `D` 의 프로그램 텍스트의 합집합 `P` 에서 파생 된 모든 형식의 프로그램 텍스트 `T`, 외부 선언 된 `P`합니다. 접근성 도메인 `M` 의 접근성 도메인의 교집합 `T` 사용 하 여 `D`입니다.
*  경우 선언된 된 접근성 `M` 는 `protected`, let `D` 의 프로그램 텍스트의 합집합 `T` 에서 파생 된 모든 형식의 프로그램 텍스트 `T`합니다. 접근성 도메인 `M` 의 접근성 도메인의 교집합 `T` 사용 하 여 `D`입니다.
*  `M`에 대해 선언된 액세스 가능성이 `internal`인 경우 `M`의 액세스 가능 도메인은 `T`의 프로그램 텍스트를 가진 `P`의 액세스 가능 도메인의 교집합 부분입니다.
*  `M`에 대해 선언된 액세스 가능성이 `private`인 경우 `M`의 액세스 가능 도메인은 `T`의 프로그램 텍스트입니다.

이러한 정의 중첩 된 멤버의 접근성 도메인은 항상 최소한 따릅니다 멤버가 선언 된 형식의 프로그램 텍스트입니다. 또한 멤버의 액세스 가능 도메인은 멤버가 선언 된 형식의 액세스 가능 도메인은 보다 더 포함 되지를 따릅니다.

직관적인 관점에서 형식 또는 멤버 `M` 은 액세스가 허용 되는지 확인 하려면 다음 단계를 실행 액세스:

*  첫째, `M` 컴파일 타임 오류가 발생 하는 해당 형식에 액세스할 수 없는 경우 (것과 반대로 컴파일 단위 또는 네임 스페이스), 형식 내에서 선언 됩니다.
*  그런 다음 if `M` 는 `public`, 액세스가 허용 됩니다.
*  그렇지 않은 경우, `M` 됩니다 `protected internal`는 프로그램 내에서 발생 하는 경우 액세스가 허용 됩니다 `M` 선언 되는 클래스에서 파생 된 클래스 내에서 발생 하는 경우 또는 `M` 선언 되 고 파생을 통해 수행 클래스 유형 ([보호 된 멤버 액세스 예를 들어](basic-concepts.md#protected-access-for-instance-members)).
*  그렇지 않은 경우, `M` 됩니다 `protected`는 클래스 내에서 발생 하는 경우 액세스가 허용 됩니다 `M` 선언 되는 클래스에서 파생 된 클래스 내에서 발생 하는 경우 또는 `M` 선언 되 고 파생을 통해 수행 클래스 유형 ([보호 된 멤버 액세스 예를 들어](basic-concepts.md#protected-access-for-instance-members)).
*  그렇지 않은 경우, `M` 은 `internal`에는 프로그램 내에서 발생 하는 경우 액세스가 허용 됩니다 `M` 선언 됩니다.
*  그렇지 않은 경우, `M` 은 `private`에는 형식 내에서 발생 하는 경우 액세스가 허용 됩니다 `M` 선언 됩니다.
*  이 고, 그렇지 형식 또는 멤버에 액세스할 수 없는 및 컴파일 타임 오류가 발생 합니다.

예제
```csharp
public class A
{
    public static int X;
    internal static int Y;
    private static int Z;
}

internal class B
{
    public static int X;
    internal static int Y;
    private static int Z;

    public class C
    {
        public static int X;
        internal static int Y;
        private static int Z;
    }

    private class D
    {
        public static int X;
        internal static int Y;
        private static int Z;
    }
}
```
클래스 및 멤버 액세스 가능성 도메인에

*  접근성 도메인 `A` 고 `A.X` 제한 되지 않습니다.
*  접근성 도메인 `A.Y`, `B`를 `B.X`, `B.Y`를 `B.C`를 `B.C.X`, 및 `B.C.Y` 포함 하는 프로그램의 프로그램 텍스트입니다.
*  접근성 도메인 `A.Z` 의 프로그램 텍스트 `A`합니다.
*  접근성 도메인 `B.Z` 하 고 `B.D` 의 프로그램 텍스트입니다 `B`의 프로그램 텍스트를 포함 하 여 `B.C` 및 `B.D`합니다.
*  접근성 도메인 `B.C.Z` 의 프로그램 텍스트 `B.C`합니다.
*  접근성 도메인 `B.D.X` 하 고 `B.D.Y` 의 프로그램 텍스트입니다 `B`의 프로그램 텍스트를 포함 하 여 `B.C` 및 `B.D`합니다.
*  접근성 도메인 `B.D.Z` 의 프로그램 텍스트 `B.D`합니다.

위의 예제와 같이 멤버의 액세스 가능성 도메인을 포함 하는 보다 크지 않습니다. 예를 들어, 경우에 모든 `X` 멤버는 public 선언 된 액세스 가능성을 제외한 모든 `A.X` 액세스 가능 도메인을 포함 하는 형식에 의해 제한 됩니다.

에 설명 된 대로 [멤버](basic-concepts.md#members), 예를 들어 생성자, 소멸자 및 정적 생성자를 제외 하 고 기본 클래스의 모든 멤버는 파생된 형식에서 상속 됩니다. 기본 클래스의 private 멤버 포함 됩니다. 그러나 개인 멤버의 액세스 가능 도메인은 멤버가 선언 된 형식의 프로그램 텍스트만을 포함 됩니다. 예제
```csharp
class A
{
    int x;

    static void F(B b) {
        b.x = 1;        // Ok
    }
}

class B: A
{
    static void F(B b) {
        b.x = 1;        // Error, x not accessible
    }
}
```
합니다 `B` 클래스는 private 멤버를 상속 `x` 에서 `A` 클래스입니다. 내에서 액세스할 수만 전용 멤버 이므로 합니다 *class_body* 의 `A`합니다. 따라서에 대 한 액세스 `b.x` 성공 합니다 `A.F` 메서드이지만에서 실패를 `B.F` 메서드.

### <a name="protected-access-for-instance-members"></a>인스턴스 멤버에 대 한 보호 된 액세스

경우는 `protected` 인스턴스 멤버에 선언 된 클래스의 프로그램 텍스트 외부 액세스 및 시기를 `protected internal` 인스턴스 멤버는 선언 되는 프로그램의 프로그램 텍스트 외부 액세스, 액세스 내에서 발생 해야 합니다.는 이전에 선언 되는 클래스에서 파생 되는 클래스 선언입니다. 또한 액세스는 여기에서 생성 되는 클래스 형식 또는 해당 파생된 클래스 형식의 인스턴스를 통해 수행 합니다. 하나의 파생된 클래스 멤버는 동일한 기본 클래스에서 상속 하는 경우에 다른 파생된 클래스의 protected 멤버에 액세스 하지 못하도록 방지 하는이 제한 합니다.

수 있도록 `B` 보호 된 인스턴스 멤버를 선언 하는 기본 클래스일 `M`, 말고 `D` 에서 파생 된 클래스 수 `B`입니다. 내 합니다 *class_body* 의 `D`에 대 한 액세스 `M` 다음 형식 중 하나를 수행:

*  정규화 되지 않은 *type_name* 하거나 *primary_expression* 양식의 `M`합니다.
*  *primary_expression* 양식의 `E.M`, 형식의 제공 `E` 는 `T` 에서 파생 된 클래스 또는 `T`여기서 `T` 클래스 형식인 `D`, 또는 클래스 형식이 생성 `D`
*  A *primary_expression* 양식의 `base.M`합니다.

이러한 형태의 액세스 하는 것 외에도 파생된 클래스에서 기본 클래스의 보호 된 인스턴스 생성자에 액세스할 수는 *constructor_initializer* ([생성자 이니셜라이저](classes.md#constructor-initializers)).

예제
```csharp
public class A
{
    protected int x;

    static void F(A a, B b) {
        a.x = 1;        // Ok
        b.x = 1;        // Ok
    }
}

public class B: A
{
    static void F(A a, B b) {
        a.x = 1;        // Error, must access through instance of B
        b.x = 1;        // Ok
    }
}
```
내 `A`, 액세스 하는 것이 불가능 `x` 둘 다의 인스턴스를 통해 `A` 및 `B`든에서 액세스가 이루어지는의 인스턴스를 통해 때문 `A` 에서 파생 된 클래스 또는 `A`합니다. 그러나 내 `B`에 액세스할 수 없는 `x` 의 인스턴스를 통해 `A`, 하므로 `A` 에서 파생 되지 않습니다 `B`.

예제
```csharp
class C<T>
{
    protected T x;
}

class D<T>: C<T>
{
    static void F() {
        D<T> dt = new D<T>();
        D<int> di = new D<int>();
        D<string> ds = new D<string>();
        dt.x = default(T);
        di.x = 123;
        ds.x = "test";
    }
}
```
세 가지 할당을 `x` 모두를 제네릭 형식에서 생성 된 클래스 형식의 인스턴스를 통해 발생할 없기 때문에 허용 됩니다.

### <a name="accessibility-constraints"></a>내게 필요한 옵션의 제약 조건

C# 언어의 몇 가지 구문에는 형식이 되도록 필요 ***만큼 액세스 가능 이상*** 멤버 또는 다른 형식입니다. 형식 `T` 멤버 또는 형식으로 액세스할 수 있도록 이라고 `M` 하는 경우의 접근성 도메인 `T` 의 접근성 도메인은 `M`합니다. 즉, `T` 이상으로 액세스할 수 `M` 경우 `T` 에 액세스할 수 있는 모든 컨텍스트에서 `M` 액세스할 수 있습니다.

다음 내게 필요한 옵션 제약 조건이 있습니다.

*  클래스 형식의 직접 기본 클래스는 적어도 클래스 형식 자체 수준만큼 액세스 가능해야 합니다.
*  인터페이스 형식의 명시적 기본 인터페이스는 적어도 인터페이스 형식 자체 수준만큼 액세스 가능해야 합니다.
*  대리자 형식의 반환 형식 및 매개 변수 형식은 적어도 대리자 형식 자체 수준만큼 액세스 가능해야 합니다.
*  상수의 형식은 적어도 상수 자체 수준만큼 액세스 가능해야 합니다.
*  필드의 형식은 적어도 필드 자체 수준만큼 액세스 가능해야 합니다.
*  메서드의 반환 형식 및 매개 변수 형식은 적어도 메서드 자체 수준만큼 액세스 가능해야 합니다.
*  속성의 형식은 적어도 속성 자체 수준만큼 액세스 가능해야 합니다.
*  이벤트의 형식은 적어도 이벤트 자체 수준만큼 액세스 가능해야 합니다.
*  인덱서의 형식 및 매개 변수 형식은 적어도 인덱서 자체 수준만큼 액세스 가능해야 합니다.
*  연산자의 반환 형식 및 매개 변수 형식은 적어도 연산자 자체 수준만큼 액세스 가능해야 합니다.
*  인스턴스 생성자의 매개 변수 형식은 적어도 인스턴스 생성자 자체 수준 만큼 액세스 가능 이어야 합니다.

예제
```csharp
class A {...}

public class B: A {...}
```
합니다 `B` 있으므로 클래스는 컴파일 타임 오류가 발생 `A` 이상으로 액세스할 수 없는 `B`합니다.

예와 마찬가지로
```csharp
class A {...}

public class B
{
    A F() {...}

    internal A G() {...}

    public A H() {...}
}
```
합니다 `H` 의 메서드 `B` 반환 형식 때문에 컴파일 타임 오류가 발생 `A` 이상 방법으로 액세스할 수 없는 합니다.

## <a name="signatures-and-overloading"></a>시그니처 및 오버 로드

메서드, 인스턴스 생성자, 인덱서 및 연산자에 따라 구분 됩니다 자신의 ***서명을***:

*  메서드 시그니처 메서드, 형식 매개 변수의 개수, 종류 및 종류 (값, 참조 또는 출력)의 왼쪽에서 오른쪽 순서로 것으로 간주 하는 정식 매개 변수의 각 이름을 이루어져 있습니다. 이러한 목적을 위해 형식 매개 변수 형식에서 발생 하는 메서드의 형식 매개 변수에 메서드의 형식 인수 목록에 있는 서 수 위치를 기준으로 하지만 해당 이름으로 식별 됩니다. 메서드 서명의 포함 되지 않습니다 반환 형식으로는 `params` 가장 오른쪽 매개 변수 및 선택적 형식 매개 변수 제약 조건에 대해 지정 될 수 있는 한정자입니다.
*  인스턴스 생성자 서명의 형식 및 종류 (값, 참조 또는 출력)의 왼쪽에서 오른쪽 순서로 것으로 간주 하는 정식 매개 변수의 각 구성 됩니다. 인스턴스 생성자의 시그니처에 포함 하지 않습니다는 `params` 가장 오른쪽 매개 변수에 대해 지정 될 수 있는 한정자입니다.
*  인덱서의 시그니처 각각 왼쪽에서 오른쪽 순서로 것으로 간주 하는 정식 매개 변수의 형식으로 구성 됩니다. 인덱서의 시그니처는 포함 되지 않습니다 요소 형식에도 포함 되지 않습니다는 `params` 가장 오른쪽 매개 변수에 대해 지정 될 수 있는 한정자입니다.
*  연산자의 시그니처에 연산자 및 각각 왼쪽에서 오른쪽 순서로 것으로 간주 하는 정식 매개 변수의 형식 이름으로 구성 됩니다. 연산자의 시그니처에 결과 형식은 포함 되지 않습니다.

시그니처는 사용 하도록 설정 하는 메커니즘 ***오버 로드*** 클래스, 구조체 및 인터페이스의 멤버입니다.

*  메서드의 오버 로드는 클래스, 구조체 또는 인터페이스는 클래스, 구조체 또는 인터페이스 내에서 고유 시그니처가 동일한 이름의 여러 메서드를 선언할 수를 허용 합니다.
*  이러한 시그니처는 해당 클래스 또는 구조체 내에서 고유 제공 클래스 또는 여러 인스턴스 생성자를 선언 하는 구조체를 허용 인스턴스 생성자의 오버 로드 합니다.
*  이러한 시그니처는 해당 클래스, 구조체 또는 인터페이스 내에서 고유 제공 클래스, 구조체 또는 여러 인덱서를 선언 하는 인터페이스를 허용 인덱서 오버 로드 합니다.
*  연산자 오버 로드는 클래스 또는 구조체는 클래스 또는 구조체 내에서 고유 시그니처가 동일한 이름의 여러 연산자를 선언할 수를 허용 합니다.

하지만 `out` 하 고 `ref` 매개 변수 한정자를 시그니처의 일부로 간주 되, 단일 형식에 선언 된 멤버 시그니처의 전적으로 달라 `ref` 고 `out`입니다. 컴파일 타임 오류가 발생 하는 경우 모든 매개 변수를 가진 두 메서드에 동일한 서명 사용 하 여 동일한 형식의 두 멤버는 선언 `out` 한정자로 변경 된 `ref` 한정자입니다. 서명이 일치 하는 다른 용도로 (예를 들어 숨기기 나 재정의), `ref` 고 `out` 시그니처의 일부로 간주 되 고 서로 일치 하지 않습니다. (이 제한은 C# 프로그램에는 인프라 CLI (공용 언어)에 다른 메서드를 정의 하는 방법을 제공 하지 않는 실행을 쉽게 번역할 수 있도록 `ref` 고 `out`.)

형식 서명의 용도로 `object` 및 `dynamic` 동일한 것으로 간주 됩니다. 단일 형식에 선언 된 멤버 달라질 수 있습니다 따라서 하지 서명에서 전적으로 `object` 고 `dynamic`입니다.

다음 예제에서는 해당 서명이 함께 오버 로드 된 메서드 선언 집합을 보여 줍니다.
```csharp
interface ITest
{
    void F();                        // F()

    void F(int x);                   // F(int)

    void F(ref int x);               // F(ref int)

    void F(out int x);               // F(out int)      error

    void F(int x, int y);            // F(int, int)

    int F(string s);                 // F(string)

    int F(int x);                    // F(int)          error

    void F(string[] a);              // F(string[])

    void F(params string[] a);       // F(string[])     error
}
```

모든 `ref` 하 고 `out` 매개 변수 한정자 ([메서드 매개 변수](classes.md#method-parameters)) 서명의 일부입니다. 따라서 `F(int)` 고 `F(ref int)` 고유한 서명 됩니다. 그러나 `F(ref int)` 하 고 `F(out int)` 시그니처에 여만 다르므로 동일한 인터페이스 내에서 선언할 수 없습니다 `ref` 및 `out`합니다. 반환 형식은 참고 또한 하며 `params` 한정자의 일부가 아닌 서명을 있으므로 또는 포함 또는 제외의 반환 형식에 따라 전적으로 오버 로드할 수 없습니다는 `params` 한정자. 따라서 메서드 선언을 `F(int)` 및 `F(params string[])` 컴파일 타임 오류가 발생 하는 위에서 확인 합니다.

## <a name="scopes"></a>범위

합니다 ***범위*** 이름의 있는 이름의 한정자 없이 이름으로 선언 된 엔터티를 참조할 수는 프로그램 텍스트의 영역입니다. 그러나 범위 수 ***중첩***, 및 내부 범위에서 외부 범위에서 이름의 의미를 다시 선언할 수 있습니다 (이 따른 제한의 제거 하지 않습니다 [선언](basic-concepts.md#declarations) 중첩된 된 블록 내에서 한 것 지역 변수는 바깥쪽 블록에 동일한 이름 가진 지역 변수를 선언할 수). 외부 범위에서 이름을 다음 이라고 ***숨겨진*** 프로그램의 지역에서 내부 범위에서 텍스트 설명 및 이름을 정규화 하 여 외부 이름에 대 한 액세스는 가능 합니다.

*  으로 선언 된 네임 스페이스 멤버의 범위를 *namespace_member_declaration* ([Namespace 멤버](namespaces.md#namespace-members)) 없는 바깥쪽 *namespace_declaration* 전체 프로그램이 텍스트입니다.
*  선언 된 네임 스페이스 멤버의 범위를 *namespace_member_declaration* 내는 *namespace_declaration* 정규화 된 이름이 `N` 는 *namespace_body*  의 모든 *namespace_declaration* 정규화 된 이름이 `N` 시작 또는 `N`뒤에 마침표, 합니다.
*  정의한 이름의 범위는 *extern_alias_directive* 으로 확장 되는 *using_directive*개이면 *global_attributes* 및 *namespace_member_ 선언*직접 포함 하는 컴파일 단위 또는 네임 스페이스 본문의 합니다. *extern_alias_directive* 기본 선언 공간에 새 멤버를 제공 하지 않습니다. 즉, 한 *extern_alias_directive* 은 전이적이 아니므로 하지만 대신 컴파일 단위 또는 네임 스페이스 본문만 발생 하는 영향을 줍니다.
*  이름 범위 정의 또는 가져온를 *using_directive* ([지시문을 사용 하 여](namespaces.md#using-directives))으로 확장 되는 *namespace_member_declaration*의  *compilation_unit* 하거나 *namespace_body* 나타나는 합니다 *using_directive* 발생 합니다. A *using_directive* 특정 내에서 사용할 수 있는 0 개 이상의 네임 스페이스, 형식 또는 멤버 이름 확인 될 수 있습니다 *compilation_unit* 또는 *namespace_body*, 되지 않지만 새 멤버를 내부 선언 공간에 영향을 줍니다. 즉, 한 *using_directive* 전이 되지 않지만 대신에 영향을 줍니다는 *compilation_unit* 또는 *namespace_body* 에서 발생 하는 합니다.
*  으로 선언 된 형식 매개 변수의 범위를 *type_parameter_list* 에 *class_declaration* ([클래스 선언을](classes.md#class-declarations))는는 *class_base*하십시오 *type_parameter_constraints_clause*s, 및 *class_body* 의 *class_declaration*.
*  으로 선언 된 형식 매개 변수의 범위를 *type_parameter_list* 에 *struct_declaration* ([구조체 선언](structs.md#struct-declarations))는는 *struct_interfaces* , *type_parameter_constraints_clause*s, 및 *struct_body* 의 *struct_declaration*합니다.
*  으로 선언 된 형식 매개 변수의 범위를 *type_parameter_list* 에 *interface_declaration* ([인터페이스 선언](interfaces.md#interface-declarations))는는 *interface_base* , *type_parameter_constraints_clause*s, 및 *interface_body* 의 *interface_declaration*합니다.
*  으로 선언 된 형식 매개 변수의 범위를 *type_parameter_list* 에 *delegate_declaration* ([대리자 선언](delegates.md#delegate-declarations))는는 *return_type*, *formal_parameter_list*, 및 *type_parameter_constraints_clause*는 s *delegate_declaration*합니다.
*  선언 된 멤버의 범위를 *class_member_declaration* ([본문 클래스](classes.md#class-body))는는 *class_body* 선언이 발생에서 합니다. 클래스 멤버의 범위를 확장 하는 또한 합니다 *class_body* 의 파생 클래스의 액세스 가능 도메인에 포함 된 ([접근성 도메인](basic-concepts.md#accessibility-domains)) 멤버의 합니다.
*  선언 된 멤버의 범위는 *struct_member_declaration* ([구조체 멤버](structs.md#struct-members))는는 *struct_body* 선언이 발생에서 합니다.
*  선언 된 멤버의 범위는 *enum_member_declaration* ([열거형 멤버](enums.md#enum-members))는는 *enum_body* 선언이 발생에서 합니다.
*  에 선언 된 매개 변수의 범위를 *method_declaration* ([메서드](classes.md#methods))은 합니다 *method_body* 의 *method_declaration*.
*  에 선언 된 매개 변수의 범위는 *indexer_declaration* ([인덱서](classes.md#indexers))은 합니다 *accessor_declarations* 는 *indexer_declaration*.
*  에 선언 된 매개 변수의 범위는 *operator_declaration* ([연산자](classes.md#operators))은 합니다 *블록* 의 *operator_declaration*.
*  에 선언 된 매개 변수의 범위를 *constructor_declaration* ([인스턴스 생성자](classes.md#instance-constructors))은 합니다 *constructor_initializer* 및 *블록* 해당 *constructor_declaration*합니다.
*  에 선언 된 매개 변수의 범위를 *lambda_expression* ([익명 함수 식](expressions.md#anonymous-function-expressions))은 합니다 *anonymous_function_body* 는 *lambda_ 식*
*  에 선언 된 매개 변수의 범위는 *anonymous_method_expression* ([익명 함수 식](expressions.md#anonymous-function-expressions))은 합니다 *블록* 는 *anonymous_method _expression*합니다.
*  레이블의 범위에서 선언 된를 *labeled_statement* ([문을 레이블이 지정 된](statements.md#labeled-statements))는는 *블록* 선언이 발생에서 합니다.
*  에 선언 된 지역 변수의 범위를 *local_variable_declaration* ([지역 변수 선언](statements.md#local-variable-declarations)) 블록입니다 선언이 발생에서 합니다.
*  에 선언 된 지역 변수의 범위를 *switch_block* 의 `switch` 문 ([switch 문](statements.md#the-switch-statement))은 합니다 *switch_block*.
*  에 선언 된 지역 변수의 범위를 *for_initializer* 의 `for` 문 ([는 문에 대 한](statements.md#the-for-statement))는 합니다 *for_initializer*,  *for_condition*는 *for_iterator*, 및 포함 된 *문* 의 `for` 문입니다.
*  범위의 지역 상수 선언에 *local_constant_declaration* ([지역 상수 선언](statements.md#local-constant-declarations)) 블록입니다 선언이 발생에서 합니다. 지역 상수 앞에 오는 텍스트 위치에서 참조 하는 컴파일 시간 오류는 해당 *constant_declarator*합니다.
*  일부로 선언 된 변수의 범위를 *foreach_statement*, *using_statement*, *lock_statement* 하거나 *query_expression* 는 지정 된 구문의 확장에 의해 결정 합니다.

네임 스페이스, 클래스, 구조체 또는 열거형 멤버의 범위 내에서 멤버의 선언 앞에 오는 텍스트 위치에서 멤버를 참조 하는 것이 같습니다. 예
```csharp
class A
{
    void F() {
        i = 1;
    }

    int i = 0;
}
```
여기에 사용할 `F` 가리키도록 `i` 먼저 선언 해야 합니다.

지역 변수의 범위 내는 것은 컴파일 타임 오류 지역 변수 앞에 오는 텍스트 위치를 가리키도록 합니다 *local_variable_declarator* 지역 변수입니다. 예
```csharp
class A
{
    int i = 0;

    void F() {
        i = 1;                  // Error, use precedes declaration
        int i;
        i = 2;
    }

    void G() {
        int j = (j = 1);        // Valid
    }

    void H() {
        int a = 1, b = ++a;    // Valid
    }
}
```

에 `F` 위의 메서드를 첫 번째 할당을 `i` 외부 범위에서 선언 된 필드 참조 하지 않습니다. 아니라 참조 지역 변수 및 변수 선언 앞에 오는 텍스트가 때문에 컴파일 타임 오류가 발생 합니다. 에 `G` 메서드를 사용 `j` 선언에 대 한 이니셜라이저에서 `j` 를 사용 하 여 앞에 오지 않습니다 때문에 유효를 *local_variable_declarator*합니다. 에 `H` 메서드를 선택 하 여 후속 *local_variable_declarator* 이전에 선언 된 지역 변수를 올바르게 가리킵니다 *local_variable_declarator* 동일한  *local_variable_declaration*합니다.

지역 변수에 대 한 범위 지정 규칙 식 컨텍스트에서 사용 되는 이름의 의미는 항상 블록 내에서 동일 하 게 보장 하도록 설계 되었습니다. 지역 변수의 범위는 블록의 끝에만 해당 선언에서에서 확장 한다면 그런 다음 위의 예제에서 첫 번째 할당에서는 인스턴스 변수에 할당 하 고 두 번째 할당도 록 로컬 변수에 할당 블록의 문은 까지로 경우 컴파일 타임 오류입니다.

블록 내에서 이름의 의미가 이름을 사용 하는 컨텍스트에 따라 달라질 수 있습니다. 예제
```csharp
using System;

class A {}

class Test
{
    static void Main() {
        string A = "hello, world";
        string s = A;                            // expression context

        Type t = typeof(A);                      // type context

        Console.WriteLine(s);                    // writes "hello, world"
        Console.WriteLine(t);                    // writes "A"
    }
}
```
이름을 `A` 식 컨텍스트에서 로컬 변수를 참조 하는 데 사용 됩니다 `A` 클래스를 참조 하는 유형 컨텍스트에서 `A`합니다.

### <a name="name-hiding"></a>이름 숨기기

엔터티의 범위는 일반적으로 엔터티의 선언 공간 보다 자세한 프로그램 텍스트를 포함합니다. 특히 엔터티 범위 이름이 같은 엔터티를 포함 하는 새 선언 공간을 정의 하는 선언이 포함 될 수 있습니다. 이러한 선언이 발생 되도록 원래 엔터티입니다 ***숨겨진***합니다. 반대로, 엔터티 라고 ***표시*** 하지으로 숨겨집니다.

이름 숨기기에 중첩 되 고 상속을 통해 범위와 일치 하는 경우를 통해 범위가 겹치는 경우 발생 합니다. 두 가지 유형의 숨기기의 특징은 다음 섹션에 설명 되어 있습니다.

#### <a name="hiding-through-nesting"></a>통한 숨기기

중첩을 사용한 이름 숨기기 중첩 네임 스페이스 또는 형식 클래스 또는 구조체 내에서 및 매개 변수 및 로컬 변수 선언으로 인해 중첩의 결과로 네임 스페이스 내의 형식으로 인해 발생할 수 있습니다.

예제
```csharp
class A
{
    int i = 0;

    void F() {
        int i = 1;
    }

    void G() {
        i = 1;
    }
}
```
내에서 `F` 메서드, 인스턴스 변수 `i` 지역 변수에서 숨겨져 `i`, 하지만 내 합니다 `G` 메서드를 `i` 여전히 인스턴스 변수를 참조 합니다.

내부 범위에서 이름을 숨깁니다 외부 범위에서 이름, 해당 이름의 오버 로드 된 모든 숨깁니다. 예제
```csharp
class Outer
{
    static void F(int i) {}

    static void F(string s) {}

    class Inner
    {
        void G() {
            F(1);              // Invokes Outer.Inner.F
            F("Hello");        // Error
        }

        static void F(long l) {}
    }
}
```
호출 `F(1)` 를 호출 하는 `F` 에 선언 된 `Inner` 때문에 모든 외부 항목의 `F` 내부 선언에 의해 숨겨집니다. 동일한 이유로 호출 `F("Hello")` 컴파일 타임 오류가 발생 합니다.

#### <a name="hiding-through-inheritance"></a>상속을 통해 숨기기

이름 숨기기 상속을 통해 클래스 또는 구조체에는 기본 클래스에서 상속 된 이름을 다시 선언할 때 발생 합니다. 이 유형의 이름 숨기기 다음 형식 중 하나를 사용 합니다.

*  상수, 필드, 속성, 이벤트 또는 클래스나 구조체에 도입 된 형식 이름이 같은 모든 기본 클래스 멤버를 숨깁니다.
*  클래스 또는 구조체에 도입 된 메서드는 동일한 이름의 모든 메서드가 아닌 기본 클래스 멤버와 동일한 서명이 (메서드 이름 및 매개 변수 수, 한정자 및 형식)를 사용 하 여 모든 기본 클래스 메서드를 숨깁니다.
*  클래스 또는 구조체에서 인덱서 (매개 변수 개수 및 형식) 동일한 서명 사용 하 여 모든 기본 클래스 인덱서를 숨깁니다.

연산자 선언을 제어 하는 규칙 ([연산자](classes.md#operators)) 기본 클래스의 연산자와 동일한 서명 사용 하 여 연산자를 선언 하는 파생된 클래스에 대 한 불가능 하기 때문입니다. 따라서 연산자 숨기지 않습니다 서로 합니다.

외부 범위에서 이름 숨기기 달리 상속된 된 범위에서 액세스 가능한 이름을 숨기면 경고 메시지가 표시 됩니다. 예제
```csharp
class Base
{
    public void F() {}
}

class Derived: Base
{
    public void F() {}        // Warning, hiding an inherited name
}
```
선언의 `F` 에서 `Derived` 보고 되는 경고를 발생 합니다. 상속된 된 이름을 숨기기 이므로 하지 오류가 발생 하는 기본 클래스의 별도 진화를 방해는입니다. 예를 들어 위와 같은 상황이 발생 하기 때문에 이후 버전의 `Base` 도입을 `F` 클래스의 이전 버전에 없는 메서드입니다. 위와 같은 상황이 오류가 같다고, 다음 변경 내용이 다른 버전의 클래스 라이브러리의 기본 클래스 발생할 수 있습니다 파생된 클래스를 사용할 수 없게 합니다.

상속된 된 이름을 숨기기 인해 경고를 사용 하 여 제거할 수는 `new` 한정자:
```csharp
class Base
{
    public void F() {}
}

class Derived: Base
{
    new public void F() {}
}
```

`new` 한정자가 나타내는 합니다 `F` 에서 `Derived` 상속 된 멤버를 숨기려면 것 실제로 고 "new"입니다.

새 멤버의 선언에는 새 멤버의 범위 내 에서만 상속 된 멤버를 숨깁니다.

```csharp
class Base
{
    public static void F() {}
}

class Derived: Base
{
    new private static void F() {}    // Hides Base.F in Derived only
}

class MoreDerived: Derived
{
    static void G() { F(); }          // Invokes Base.F
}
```

선언의 위의 예에서 `F` 에 `Derived` 숨깁니다 합니다 `F` 에서 상속 된는 `Base`, 하지만 새 `F` 에서 `Derived` 개인 액세스 권한이 해당 범위로 확장 되지 않습니다 `MoreDerived` . 따라서 호출 `F()` 에 `MoreDerived.G` 유효 하 고 호출 `Base.F`합니다.

## <a name="namespace-and-type-names"></a>Namespace 및 형식 이름

C# 프로그램의 여러 컨텍스트 필요는 *namespace_name* 또는 *type_name* 를 지정 해야 합니다.

```antlr
namespace_name
    : namespace_or_type_name
    ;

type_name
    : namespace_or_type_name
    ;

namespace_or_type_name
    : identifier type_argument_list?
    | namespace_or_type_name '.' identifier type_argument_list?
    | qualified_alias_member
    ;
```

A *namespace_name* 되는 *namespace_or_type_name* 네임 스페이스를 참조 하는 합니다. 아래 설명 된 대로 확인을 수행 합니다 *namespace_or_type_name* 의 *namespace_name* 네임 스페이스를 참조 해야 합니다 또는 그렇지 않으면 컴파일 타임 오류가 발생 합니다. 형식 인수 없이 ([형식 인수가](types.md#type-arguments))에 있을 수는 *namespace_name* (형식 형식 인수를 가질 수 있음)만 합니다.

A *type_name* 되는 *namespace_or_type_name* 형식을 참조 하는 합니다. 아래 설명 된 대로 확인을 수행를 *namespace_or_type_name* 의 *type_name* 형식을 참조 해야 합니다 또는 그렇지 않으면 컴파일 타임 오류가 발생 합니다.

경우는 *namespace_or_type_name* 멤버인 정규화-별칭-해당 의미는에 설명 된 대로 [Namespace 별칭 한정자](namespaces.md#namespace-alias-qualifiers)합니다. 그렇지 않은 경우는 *namespace_or_type_name* 에 네 가지 형태 중 하나:

*  `I`
*  `I<A1, ..., Ak>`
*  `N.I`
*  `N.I<A1, ..., Ak>`

여기서 `I` 는 단일 식별자 `N` 되는 *namespace_or_type_name* 및 `<A1, ..., Ak>` 선택적 *type_argument_list*합니다. 없는 경우 *type_argument_list* 가 지정 하는 것이 좋습니다 `k` 0입니다.

의미는 *namespace_or_type_name* 다음과 같이 결정 됩니다.

*   경우는 *namespace_or_type_name* 형식인 `I` 또는 양식의 `I<A1, ..., Ak>`:
    * 하는 경우 `K` 가 0 및 *namespace_or_type_name* 제네릭 메서드 선언 내에 나타납니다 ([메서드](classes.md#methods)) 및 해당 선언 형식 매개 변수를 포함 하는 경우 ([형식 매개 변수](classes.md#type-parameters)) 이름의 `I`, 해당 *namespace_or_type_name* 해당 형식 매개 변수를 가리킵니다.
    * 그렇지 않은 경우, 합니다 *namespace_or_type_name* 형식 선언에서 다음 각 인스턴스 유형에 대해 나타납니다 `T` ([인스턴스 유형을](classes.md#the-instance-type)) 해당 형식의 인스턴스를 사용 하 여 시작 선언 및 (있는 경우) 각 바깥쪽 클래스 또는 구조체 선언의 인스턴스 형식을 사용 하 여 계속 합니다.
        * 하는 경우 `K` 0 이며 선언의 `T` 이름의 형식 매개 변수가 포함 `I`, 해당 *namespace_or_type_name* 해당 형식 매개 변수를 가리킵니다.
        * 그렇지 않은 경우를 *namespace_or_type_name* 형식 선언의 본문 내에 표시 하 고 `T` 이름의 중첩된 액세스할 수 있는 형식을 포함 해당 기본 형식 또는 `I` 및 `K` 형식 매개 변수 해당 *namespace_or_type_name* 지정 된 형식 인수를 사용 하 여 생성 하는 형식을 참조 합니다. 이러한 형식이 둘 이상 있으면 더 많이 파생 된 형식 내에서 선언 된 형식이 선택 됩니다. 형식이 아닌 멤버 (상수, 필드, 메서드, 속성, 인덱서, 연산자, 인스턴스 생성자, 소멸자 및 정적 생성자) 및 다양 한 개수의 형식 매개 변수를 사용 하 여 형식 멤버의 의미를 결정할 때 무시 됩니다는 *namespace_or_type_name*합니다.
    * 이전 단계를 각 네임 스페이스에 대 한 다음 실패 한 경우 `N`네임 스페이스를 사용 하 여 시작 합니다 *namespace_or_type_name* 각 바깥쪽 네임 스페이스 (있을 경우)를 사용 하 여 계속 해 서 끝나는 발생 합니다 전역 네임 스페이스는 엔터티를 찾을 때까지 다음 단계를 실행 합니다.
        * 경우 `K` 가 0 및 `I` 네임 스페이스의 이름은 `N`, 다음:
            * 경우 위치 위치는 *namespace_or_type_name* 발생에 대 한 네임 스페이스 선언을 괄호로 묶여 `N` 네임 스페이스 선언을 포함 하는 *extern_alias_directive* 또는 *using_alias_directive* 이름을 연결 하는 `I` 형식 또는 네임 스페이스를 사용 하 여 해당 *namespace_or_type_name* 모호 하 고 컴파일 시간 오류가 발생 합니다.
            * 이 고, 그렇지 합니다 *namespace_or_type_name* 라는 네임 스페이스 참조 `I` 에서 `N`합니다.
        * 그렇지 않은 경우, `N` 이름의 액세스할 수 있는 형식이 포함 되어 `I` 및 `K` 다음 매개 변수를 입력 합니다.
            * 하는 경우 `K` 0 및 위치는 여기서는 *namespace_or_type_name* 발생에 대 한 네임 스페이스 선언을 괄호로 묶여 `N` 네임 스페이스 선언을 포함 하 고는 *extern_alias_directive*  나 *using_alias_directive* 이름을 연결 하는 `I` 네임 스페이스 또는 형식을 사용 하 여 해당 *namespace_or_type_name* 모호 하며 컴파일 타임에는 오류가 발생합니다.
            * 그렇지 않은 경우는 *namespace_or_type_name* 지정 된 형식 인수를 사용 하 여 생성 된 형식을 참조 합니다.
        * 그렇지 않은 경우, 위치 여기서 합니다 *namespace_or_type_name* 발생에 대 한 네임 스페이스 선언을 괄호로 묶여 `N`:
            * 하는 경우 `K` 이 0이 고 네임 스페이스 선언에는 *extern_alias_directive* 또는 *using_alias_directive* 이름을 연결 하는 `I` 가져온된 네임 스페이스를 사용 하 여 또는 형식, 해당 *namespace_or_type_name* 해당 네임 스페이스 또는 형식을 가리킵니다.
            * 네임 스페이스 및 형식 선언에서 가져온 경우는 *using_namespace_directive*s 및 *using_alias_directive*네임 스페이스 선언 중 하나만 액세스할 수 있는 형식을 포함 이름의 `I` 하 고 `K` 매개 변수를 입력 하면 *namespace_or_type_name* 지정 된 형식 인수를 사용 하 여 생성 하는 형식을 참조 합니다.
            * 네임 스페이스 및 형식 선언에서 가져온 경우는 *using_namespace_directive*s 및 *using_alias_directive*네임 스페이스 선언의 s 둘 이상의 액세스할 수 있는 형식을 포함 이름의 `I` 및 `K` 매개 변수를 입력 하면 *namespace_or_type_name* 모호 합니다. 오류가 발생 합니다.
    * 이 고, 그렇지 합니다 *namespace_or_type_name* 가 정의 되지 않은 하 고 컴파일 시간 오류가 발생 합니다.
*  이 고, 그렇지 합니다 *namespace_or_type_name* 형식인 `N.I` 또는 양식의 `N.I<A1, ..., Ak>`합니다. `N` 먼저 됨을 *namespace_or_type_name*합니다. 하는 경우의 해결 방법을 `N` 정상적이 지 않습니다 컴파일 타임 오류가 발생 합니다. 그렇지 않으면 `N.I` 또는 `N.I<A1, ..., Ak>` 같이 확인 됩니다.
    * 경우 `K` 0 및 `N` 네임 스페이스를 참조 하 고 `N` 이름의 중첩된 된 네임 스페이스를 포함 `I`, 해당 *namespace_or_type_name* 중첩 된 네임 스페이스를 참조 합니다.
    * 그렇지 `N` 네임 스페이스를 참조 및 `N` 이름의 액세스할 수 있는 형식이 포함 되어 `I` 및 `K` 매개 변수를 입력 하면 *namespace_or_type_name* 해당 형식을 참조 지정 된 형식 인수를 사용 하 여 생성 합니다.
    * 그렇지 않은 경우, `N` (가능한 경우 생성 된) 클래스 또는 구조체 형식을 참조 및 `N` 이름의 중첩된 액세스할 수 있는 형식을 포함 한 모든 기본 클래스 `I` 하 고 `K` 매개 변수를 입력 하면 *네임 스페이스 _or_type_name* 지정 된 형식 인수를 사용 하 여 생성 하는 형식을 참조 합니다. 이러한 형식이 둘 이상 있으면 더 많이 파생 된 형식 내에서 선언 된 형식이 선택 됩니다. 경우의 의미를 확인 `N.I` 결정 하는 기본 클래스 지정을 확인 하는 일부로 `N` 직접 기본 클래스의 다음 `N` 개체로 간주 됩니다 ([기본 클래스](classes.md#base-classes)).
    * 이 고, 그렇지 `N.I` 잘못 된 *namespace_or_type_name*, 컴파일 시간 오류가 발생 합니다.

A *namespace_or_type_name* 정적 클래스를 참조 하도록 허용 됩니다 ([정적 클래스](classes.md#static-classes)) 경우에만

*  *namespace_or_type_name* 은 합니다 `T` 에 *namespace_or_type_name* 폼의 `T.I`, 또는
*  *namespace_or_type_name* 는 `T` 에 *typeof_expression* ([인수 목록](expressions.md#argument-lists)1) 형식의 `typeof(T)`.

### <a name="fully-qualified-names"></a>정규화 된 이름

모든 네임 스페이스 및 형식에는 ***정규화 된 이름을***를 고유 하 게 식별 하는 네임 스페이스 또는 다른 모든 형식과 합니다. 형식 또는 네임 스페이스의 정규화 된 이름을 `N` 다음과 같이 결정 됩니다.

*  하는 경우 `N` 멤버인 정규화 된 이름은 전역 네임 스페이스는 `N`합니다.
*  그렇지 않으면 해당 정규화 된 이름을 `S.N`여기서 `S` 네임 스페이스 또는 형식의는 정규화 된 이름인 `N` 선언 됩니다.

즉, 정규화 된 이름의 `N` 로 안내 하는 식별자의 전체 계층적 경로인 `N`전역 네임 스페이스에서 시작 합니다. 형식 또는 네임 스페이스의 모든 멤버 고유 이름이 있어야 하므로 항상 형식 또는 네임 스페이스의 정규화 된 이름을 고유함을 따릅니다.

아래 예제에는 연결 된 해당 정규화 된 이름이 여러 네임 스페이스 및 형식 선언을 보여 줍니다.
```csharp
class A {}                // A

namespace X               // X
{
    class B               // X.B
    {
        class C {}        // X.B.C
    }

    namespace Y           // X.Y
    {
        class D {}        // X.Y.D
    }
}

namespace X.Y             // X.Y
{
    class E {}            // X.Y.E
}
```

## <a name="automatic-memory-management"></a>자동 메모리 관리

C# 개발자가 수동으로 할당 하 고 개체에 의해 점유 메모리에서 해제는 자동 메모리 관리를 사용 합니다. 자동 메모리 관리 정책이 구현 되는 ***가비지 수집기***합니다. 개체의 메모리 관리 수명 주기는 다음과 같습니다.

1. 개체를 만들 때 할당 된 메모리, 생성자를 실행 및 개체 라이브 것으로 간주 됩니다.
2. 개체 또는 그 일부를 실행 가능한 모든 연속 하 여 액세스할 수 없으면, 소멸자를 실행 이외의 개체 간주 되 더 이상 사용에서 고 소멸 대상이 됩니다. C# 컴파일러와 가비지 수집기가 개체에 대 한 참조는 나중에 사용할 수 있습니다를 확인 하는 코드를 분석할 수도 있습니다. 예를 들어 범위 내에 있는 로컬 변수는 개체에 기존 참조 하지만 해당 로컬 변수는 프로시저에서 가리킨 현재 실행의 실행 가능한 모든 연속에서 참조 되지 않는 경우 가비지 수집기가 될 수 있습니다 (하지만 아닙니다. 에 필요) 사용에서을 더 이상 개체를 처리 합니다.
3. 개체를 소멸할 수 있으면 나중에 지정 되지 않은 몇 가지 시간 소멸자 ([소멸자](classes.md#destructors)) (있는 경우) 개체가 실행 됩니다. 정상적인 소멸자는 개체에 대 한 구현 관련 Api에는이 동작을 재정의할 수 수 있지만 한 번만 실행 됩니다.
4. 개체 또는 그 일부를 실행, 소멸자를 실행 하는 등의 가능한 모든 연속 하 여 액세스할 수 없는 경우 개체에 대 한 소멸자가 실행 되 면 개체 액세스할 수 없는 것으로 간주 됩니다 및 개체 컬렉션에 대 한 대상이 됩니다.
5. 마지막으로, 특정 시간에 개체 컬렉션을 사용할 수 있게 되 면 가비지 수집기가 메모리를 해제 개체와 관련 된 합니다.

가비지 수집기는 개체 사용에 대 한 정보를 유지 관리 하 고 개체와 개체가 위치를 변경 하는 더 이상 사용에서 되거나 액세스할 수 없는 경우 새로 생성된 된 개체를 찾을 수 있는 메모리 위치와 같은 메모리 관리 의사 결정을 확인 합니다.이 정보를 사용 합니다.

가비지 수집기의 존재 여부를 가정 하는 다른 언어와 마찬가지로 C#는 설계 되어 가비지 수집기는 다양 한 범위의 메모리 관리 정책 구현할 수 있습니다. 예를 들어 C# 필요가 없습니다 소멸자를 실행 하는 것에 자격이 되는 개체는 수집 수 또는 특정 순서에 관계 없이 또는 특정 스레드에서 소멸자를 실행 하는 것입니다.

가비지 수집의 동작을 제어할 수 클래스에서 정적 메서드를 통해 어느 정도 `System.GC`합니다. 이 클래스는 소멸자 수 실행 (또는 실행 되지)가 발생 하는 컬렉션을 요청에 사용할 수 있습니다 및 등입니다.

가비지 수집기가 개체를 수집 하 고 소멸자를 실행 하는 경우 유연 하 게 결정할 허용 하므로 표준에 맞는 구현에 다음 코드에 의해 표시 되는 다른 출력을 생성할 수 있습니다. 프로그램
```csharp
using System;

class A
{
    ~A() {
        Console.WriteLine("Destruct instance of A");
    }
}

class B
{
    object Ref;

    public B(object o) {
        Ref = o;
    }

    ~B() {
        Console.WriteLine("Destruct instance of B");
    }
}

class Test
{
    static void Main() {
        B b = new B(new A());
        b = null;
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```
클래스의 인스턴스를 만듭니다 `A` 클래스의 인스턴스 `B`합니다. 이러한 개체가 가비지 수집에 적합 하 게 될 때 변수의 `b` 값이 할당 됩니다 `null`아니므로이 시간 후에 액세스할 모든 사용자가 작성 한 코드에 대 한 가능한, 합니다. 출력 될 수 있음
```
Destruct instance of A
Destruct instance of B
```
또는
```
Destruct instance of B
Destruct instance of A
```
언어 순서 없는 제약 조건을 설정 때문에 개체에서 가비지 수집 됩니다.

경우에 따라 "를 소멸할 수" 및 "컬렉션에 대 한 적격"의 차이 중요할 수 있습니다. 예를 들어 개체에 적용된
```csharp
using System;

class A
{
    ~A() {
        Console.WriteLine("Destruct instance of A");
    }

    public void F() {
        Console.WriteLine("A.F");
        Test.RefA = this;
    }
}

class B
{
    public A Ref;

    ~B() {
        Console.WriteLine("Destruct instance of B");
        Ref.F();
    }
}

class Test
{
    public static A RefA;
    public static B RefB;

    static void Main() {
        RefB = new B();
        RefA = new A();
        RefB.Ref = RefA;
        RefB = null;
        RefA = null;

        // A and B now eligible for destruction
        GC.Collect();
        GC.WaitForPendingFinalizers();

        // B now eligible for collection, but A is not
        if (RefA != null)
            Console.WriteLine("RefA is not null");
    }
}
```

위의 프로그램에서 가비지 수집기의 소멸자를 실행 하 고 싶다면 `A` 소멸자 전에 `B`,이 프로그램의 출력 수 있습니다:
```
Destruct instance of A
Destruct instance of B
A.F
RefA is not null
```

인스턴스의 `A` 사용 되지 않았습니다 및 `A`의 소멸자가 실행 되는 수의 메서드에 대 한 `A` (이 예제의 경우 `F`) 다른 소멸자에서 호출할 수 있습니다. 또한 참고를 소멸자는 실행이 다시 주 프로그램에서 사용할 수 있게 하는 개체를 발생할 수 있습니다. 이 예에서 실행 `B`소멸자 발생의 인스턴스에 `A` 는 이전에 사용 되지 않으면 라이브 참조에서 액세스할 수 있게 `Test.RefA`합니다. 호출한 후 `WaitForPendingFinalizers`, 인스턴스의 `B` 인스턴스가 되지만 컬렉션에 적합 한 `A` 를 참조 하지 않으면 `Test.RefA`합니다.

예기치 않은 동작과 혼동을 방지 하려면 것이 좋습니다 일반적으로 소멸자에 대 한만 해당 개체의 필드에 저장 된 데이터 정리를 수행 하 고 참조 된 개체 또는 정적 필드에 작업을 수행할 필요가 있습니다.

소멸자를 사용 하는 대신 구현 클래스를 사용 하는 것은 `System.IDisposable` 인터페이스입니다. 이 통해 리소스로 개체에 액세스 하 여 일반적으로 개체의 리소스를 해제 하는 시기를 결정 하는 개체의 클라이언트는 `using` 문 ([는 문을 사용 하 여](statements.md#the-using-statement)).

## <a name="execution-order"></a>실행 순서

C# 프로그램의 실행에는 각 실행 스레드에의 한 부작용 중요 실행 시점에 유지 됩니다 있도록 진행 됩니다. A ***부작용*** 읽기 또는 쓰기 volatile 필드의, 비 volatile 변수에 쓰기 예외를 throw 하 고 외부 리소스를 쓸으로 정의 됩니다. 이러한 부작용의 순서를 유지 해야 하는 중요 한 실행 지점은 volatile 필드에 대 한 참조 ([Volatile 필드](classes.md#volatile-fields)), `lock` 문 ([lock 문에](statements.md#the-lock-statement)), 및 스레드 생성 및 종료 합니다. 실행 환경에서는 다음 제약 조건에 따라 C# 프로그램에서의 실행 순서를 변경 하려면:

*  데이터 종속성 실행의 스레드 내에서 유지 됩니다. 즉, 각 변수의 값은 원래 프로그램 순서로 스레드에서 모든 문이 실행 된 것 처럼 계산 됩니다.
*  초기화 순서 규칙에서 유지 됩니다 ([필드 초기화](classes.md#field-initialization) 하 고 [변수 이니셜라이저](classes.md#variable-initializers)).
*  Volatile 읽기 및 쓰기와 관련 하 여 의도의 순서는 유지 ([Volatile 필드](classes.md#volatile-fields)). 또한 실행 환경 해당 식의 값을 사용 하지 않도록 하 고 필요한 부작용이 없습니다 (volatile 필드에 액세스 하거나 메서드를 호출 하 여 발생 한 모든 포함)이 생성 되는 추론할 수 있습니다 하는 경우 식의 일부를 평가 하지 해야 합니다. 비동기 이벤트 (예: 다른 스레드에 의해 throw 된 예외)에 의해 프로그램 실행이 중단 되며 때 눈에 띄는 부작용 원래 프로그램 순서로 표시 되는지 보장 되지 않습니다.
