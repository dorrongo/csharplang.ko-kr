# <a name="introduction"></a>소개

C#(“샵 참조”)은 간단하면서도 형식이 안전한 최신 개체 지향 프로그래밍 언어입니다. C# C 언어 제품군에는 해당 루트 및 C, c + + 및 Java 프로그래머에 게 익숙한 됩니다. C#으로 ECMA International로 표준화 되는 ***ECMA-334*** 표준 및 ISO/IEC로 여는 ***ISO/IEC 23270*** 표준. .NET Framework에 대 한 Microsoft의 C# 컴파일러는 이러한 두 표준은 표준에 맞는 구현 합니다.

C#은 개체 지향 언어이지만 ***구성 요소 지향*** 프로그래밍도 지원합니다. 현대의 소프트웨어 설계는 독립적이고 자체 설명적인 기능 패키지 형식을 갖는 소프트웨어 구성 요소에 점점 더 많이 의존하고 있습니다. 이러한 구성 요소의 핵심은 속성, 메서드 및 이벤트를 포함하는 프로그래밍 모델을 제공한다는 데 있습니다. 이러한 구성 요소는 구성 요소에 대한 선언적 정보를 제공하는 특성을 보유하며 자체 설명서를 통합하고 있습니다. C# 제공 직접 이러한 개념을 지 원하는 언어 구문을 만들어 소프트웨어 구성 요소를 사용 하는 뛰어난 자연 언어로 C# 수행 합니다.

강력 하 고 안정적인 응용 프로그램 생성에 도움이 되는 여러 C# 기능: ***가비지 수집*** 사용 되지 않는 개체에서 사용한 메모리를 자동적으로 회수 ***예외 처리*** 오류 감지 및 복구를 구조화 하 고 확장 가능한 방법을 제공 하며 ***형식이 안전한*** 언어의 디자인을 사용 하면 초기화 되지 않은 읽을 불가능 변수, 해당 경계 초과 또는 확인 되지 않은 형식 캐스트를 수행 하려면 인덱스 배열입니다.

C#에는 ***통합 형식 시스템***이 있습니다. `int` 및 `double`과 같은 기본 형식을 포함하는 모든 C# 형식은 단일 루트 `object`에서 상속됩니다. 따라서 일반적인 작업 집합을 공유하는 모든 형식과 모든 형식의 값을 일관된 방식으로 저장 및 전송하고 작업을 수행할 수 있습니다. 그뿐 아니라 C#은 사용자 정의 참조 형식 및 값 형식을 모두 지원하여 개체의 동적 할당과 더불어 간단한 구조의 인라인 저장소도 구현합니다.

C# 프로그램 및 라이브러리 수 시간이 지나면서 호환 되는 방식에서 되도록 강조한 것에 배치 된 ***버전 관리*** C#의 디자인 합니다. 다양한 프로그래밍 언어가 이 문제를 등한시하여 결과적으로 해당 언어로 작성된 프로그램이 최신 버전의 종속 라이브러리가 도입될 때 필요한 것보다 더 자주 중단되게 되었습니다. C# 설계의 측면 된 버전 관리 고려 사항 직접적인 영향을 포함할 별도 `virtual` 고 `override` 한정자, 메서드 오버 로드 확인에 대 한 규칙 및 명시적 인터페이스 멤버 선언에 대 한 지원.

이 장의 나머지 C# 언어의 필수 기능을 설명 합니다. 세부적인 및 경우에 따라 수학 방식으로 규칙 및 예외를 설명 하는 뒷부분에는 않지만이 장 명확 성과 떨어지더라도 간단한 설명을 위해 노력 합니다. 초기 프로그램의 작성 및 뒷부분의 읽기를 원활 하 게 하는 언어에 대 한 소개를 제공 하기 위함입니다.

## <a name="hello-world"></a>Hello World

“Hello, World” 프로그램은 프로그래밍 언어를 소개하는 데 일반적으로 사용됩니다. C#에서는 다음과 같습니다.

```csharp
using System;

class Hello
{
    static void Main() {
        Console.WriteLine("Hello, World");
    }
}
```

C# 소스 파일은 일반적으로 파일 확장명이 `.cs`입니다. "Hello, World" 프로그램이 파일에 저장 된 가정 `hello.cs`, 명령줄을 사용 하 여 Microsoft C# 컴파일러를 사용 하 여 프로그램을 컴파일할 수 있습니다
```
csc hello.cs
```
명명 된 실행 가능한 어셈블리를 생성 하는 `hello.exe`합니다. 실행 될 때이 응용 프로그램에서 생성 된 출력은
```
Hello, World
```

“Hello, World” 프로그램은 `System` 네임스페이스를 참조하는 `using` 지시문으로 시작합니다. 네임스페이스는 계층적으로 C# 프로그램 및 라이브러리를 구성하는 방법을 제공합니다. 네임스페이스에는 형식 및 다른 네임스페이스가 포함됩니다. 예를 들어 `System` 네임스페이스에는 많은 형식(예: 프로그램에 참조되는 `Console` 클래스) 및 많은 다른 네임스페이스(예: `IO` 및 `Collections`)가 포함되어 있습니다. 지정된 네임스페이스를 참조하는 `using` 지시문을 사용하여 해당 네임스페이스의 멤버인 형식을 정규화되지 않은 방식으로 사용할 수 있습니다. `using` 지시문 때문에, 프로그램은 `Console.WriteLine`을 `System.Console.WriteLine`의 약식으로 사용할 수 있습니다.

“Hello, World” 프로그램에서 선언된 `Hello` 클래스에는 단일 멤버인 `Main` 메서드가 있습니다. `Main` 사용 하 여 선언 된 메서드는 `static` 한정자. 인스턴스 메서드는 키워드 `this`를 사용하여 특정 바깥쪽 개체 인스턴스를 참조할 수 있지만 정적 메서드는 특정 개체에 대한 참조 없이 작동합니다. 관례상 `Main`이라는 정적 메서드가 프로그램의 진입점으로 사용됩니다.

프로그램의 출력은 `System` 네임스페이스에 있는 `Console` 클래스의 `WriteLine` 메서드에 의해 생성됩니다. 이 클래스는 기본적으로 자동으로 참조 하는 Microsoft C# 컴파일러는.NET Framework 클래스 라이브러리에서 제공 됩니다. 자체 C# 없는 별도 런타임 라이브러리를 참고 합니다. 대신,.NET Framework는 C#의 런타임 라이브러리입니다.

## <a name="program-structure"></a>프로그램 구조

C#의 핵심적인 조직 개념은 ***프로그램***, ***네임스페이스***, ***형식***, ***멤버*** 및 ***어셈블리***입니다. C# 프로그램은 하나 이상의 소스 파일로 구성됩니다. 프로그램은 멤버를 포함하고 네임스페이스로 구성될 수 있는 형식을 선언합니다. 클래스와 인터페이스는 형식의 예입니다. 필드, 메서드, 속성 및 이벤트는 멤버의 예입니다. C# 프로그램을 컴파일하면 실제로 어셈블리로 패키지됩니다. 어셈블리 일반적으로 파일 확장명이 `.exe` 또는 `.dll`구현 여부에 따라 ***응용 프로그램*** 하거나 ***라이브러리***합니다.

이 예제에서

```csharp
using System;

namespace Acme.Collections
{
    public class Stack
    {
        Entry top;

        public void Push(object data) {
            top = new Entry(top, data);
        }

        public object Pop() {
            if (top == null) throw new InvalidOperationException();
            object result = top.data;
            top = top.next;
            return result;
        }

        class Entry
        {
            public Entry next;
            public object data;
    
            public Entry(Entry next, object data) {
                this.next = next;
                this.data = data;
            }
        }
    }
}
```
이라는 클래스를 선언 `Stack` 라는 네임 스페이스에서 `Acme.Collections`합니다. 이 클래스의 정규화된 이름은 `Acme.Collections.Stack`입니다. 클래스에는 필드 `top`, 2개의 메서드 `Push` 및 `Pop`, 중첩된 클래스 `Entry` 등의 여러 멤버가 포함됩니다. `Entry` 클래스는 필드 `next` 및 필드 `data`, 생성자의 세 멤버가 포함됩니다. 예제의 소스 코드가 파일 `acme.cs`에 포함된다고 가정할 경우 다음 명령줄은

```
csc /t:library acme.cs
```
예제를 라이브러리(`Main` 진입점이 없는 코드)를 컴파일하고 `acme.dll`이라는 어셈블리를 생성합니다.

어셈블리의 형태로 실행 코드를 포함할 ***Intermediate Language*** 형태로 기호화 된 정보와 (IL) 명령 ***메타 데이터***입니다. 실행되기 전에 어셈블리의 IL 코드는 .NET 공용 언어 런타임의 JIT(Just-In-Time) 컴파일러에 의해 자동으로 프로세서 특정 코드로 변환됩니다.

어셈블리는 코드와 메타데이터를 모두 포함하는 기능의 자체 설명 단위이므로 C#에 `#include` 지시문 및 헤더 파일이 필요하지 않습니다. 특정 어셈블리에 포함된 공용 형식 및 멤버는 프로그램을 컴파일할 때 해당 어셈블리를 참조하는 것만으로 C# 프로그램에서 사용 가능해집니다. 예를 들어 이 프로그램에서는 `acme.dll` 어셈블리의 `Acme.Collections.Stack` 클래스를 사용합니다.

```csharp
using System;
using Acme.Collections;

class Test
{
    static void Main() {
        Stack s = new Stack();
        s.Push(1);
        s.Push(10);
        s.Push(100);
        Console.WriteLine(s.Pop());
        Console.WriteLine(s.Pop());
        Console.WriteLine(s.Pop());
    }
}
```
프로그램 파일에 저장 되는 경우 `test.cs`때 `test.cs` 컴파일되면 합니다 `acme.dll` 컴파일러의를 사용 하 여 어셈블리를 참조할 수 있습니다 `/r` 옵션:

```
csc /r:acme.dll test.cs
```
이를 통해 실행 시 출력을 생성하는 `test.exe`라는 실행 가능한 어셈블리가 만들어집니다.

```
100
10
1
```
C#은 프로그램의 소스 텍스트가 여러 소스 파일에 저장되도록 허용합니다. 다중 파일 C# 프로그램이 컴파일되면 모든 소스 파일이 함께 처리되고 소스 파일은 서로 자유롭게 참조될 수 있습니다. 개념적으로는 마치 모든 소스 파일이 처리되기 전에 하나의 큰 파일로 연결되는 것처럼 보입니다. 극소수의 경우를 제외하고 선언 순서는 중요하지 않으므로 C#에서는 정방향 선언이 절대 필요하지 않습니다. C#은 소스 파일을 하나의 공용 형식만 선언하도록 제한하거나 소스 파일 이름이 소스 파일에 선언된 형식과 일치하도록 요구하지 않습니다.

## <a name="types-and-variables"></a>형식 및 변수

C#에는 두 가지 종류의 형식, 즉 ***값 형식***과 ***참조 형식***이 있습니다. 값 형식의 변수에는 해당 데이터가 직접 포함되지만 참조 형식의 변수에는 데이터(개체라고도 함)에 대한 참조가 저장됩니다. 참조 형식에서는 두 가지 변수가 같은 개체를 참조할 수 있으므로 한 변수에 대한 작업이 다른 변수에서 참조하는 개체에 영향을 미칠 수 있습니다. 값 형식에서는 변수에 데이터의 자체 사본이 들어 있으며 한 변수의 작업이 다른 변수에 영향을 미칠 수 없습니다(`ref` 및 `out` ref 및 out 매개 변수 제외).

C#의 값 형식으로 세분화 됩니다 ***단순 형식***, ***열거형***를 ***구조체 형식은***, 및 ***nullable 형식***, 및 C# 참조 형식으로 세분화 됩니다 ***클래스 형식은***, ***인터페이스 형식***합니다 ***배열 형식***, 및 ***대리자 형식***합니다.

다음 표에서 C#의 형식 시스템의 개요를 제공합니다.

| __범주__    |                 | __설명__ |
|-----------------|-----------------|-----------------|
| 값 형식     | 단순 형식    | 부호 있는 정수: `sbyte`, `short`, `int`,`long` |
|                 |                 | 부호 없는 정수: `byte`, `ushort`, `uint`,`ulong` |
|                 |                 | 유니코드 문자: `char` |
|                 |                 | IEEE 부동 소수점: `float`, `double` |
|                 |                 | High-Precision 10진수:`decimal` |
|                 |                 | 부울: `bool` |
|                 | 열거형      | `enum E {...}` 양식의 사용자 정의 형식 |
|                 | 구조체 형식    | `struct S {...}` 양식의 사용자 정의 형식 |
|                 | Nullable 형식  | `null` 값을 갖는 다른 모든 값 형식의 확장 |
| 참조 형식 | 클래스 형식     | 다른 모든 형식의 기본 클래스: `object` |
|                 |                 | 유니코드 문자열: `string` |
|                 |                 | `class C {...}` 양식의 사용자 정의 형식 |
|                 | 인터페이스 형식 | `interface I {...}` 양식의 사용자 정의 형식 |
|                 | 배열 형식     | 단일 차원 및 다차원(예: `int[]` 및`int[,]`) |
|                 | 대리자 형식  | 폼의 사용자 정의 형식 예: `delegate int  D(...)` |

8가지 정수 형식은 부호 있는 형식 또는 부호 없는 형식으로 8비트, 16비트, 32비트 및 64비트 값에 대한 지원을 제공합니다.

두 부동 소수점 형식, `float` 고 `double`, 32 비트 단 정밀도 및 64 비트 배정밀도 IEEE 754 형식을 사용 하 여 표시 됩니다.

`decimal` 형식은 재무 및 통화 계산에 적합한 128비트 데이터 형식입니다.

C# `bool` 형식을 부울 값을 나타내는 데 사용 됩니다-인 값 `true` 또는 `false`합니다.

C#의 문자 및 문자열 처리에서는 유니코드 인코딩이 사용됩니다. `char` 형식은 UTF-16 코드 단위를 나타내고, `string` 형식은 UTF-16 코드 단위 시퀀스를 나타냅니다.

다음 표에서 C#의 숫자 형식이 요약 되어 있습니다.


| __범주__      | __비트__ | __Type__  | __범위/자릿수__ |
|-------------------|----------|-----------|---------------------|
| 부호 있는 정수   | 8        | `sbyte`   | ...-128에서 127 |
|                   | 16       | `short`   | -32, 768... 32, 767 |
|                   | 32       | `int`     | -2,147,483, 648... 2, 147, 483, 647 |
|                   | 64       | `long`    | -9,223,372,036,854,775, 808... 9, 223, 372, 036, 854, 775, 807 |
| 부호 없는 정수 | 8        | `byte`    | 0... 255 |
|                   | 16       | `ushort`  | 0... 65,535 |
|                   | 32       | `uint`    | 0... 4294967295 |
|                   | 64       | `ulong`   | 0... 18446744073709551615 |
| 부동 소수점    | 32       | `float`   | 1.5 × 10 ^ − 45 3.4 × 10 ^38, 전체 자릿수 7 자리 |
|                   | 64       | `double`  | 5.0 × 10 ^324 1.7 × 10 ^308, 전체 자릿수 15 자리 |
| Decimal           | 128      | `decimal` | 1.0 × 10 ^ −28 7.9 × 10 ^28, 28 자리 전체 자릿수 |

C# 프로그램에서는 ***형식 선언***을 사용하여 새 형식을 만듭니다. 형식 선언은 새 형식의 이름과 멤버를 지정합니다. 사용자 정의 가능한 형식의 C#의 범주 5: 형식, 구조체 형식, 인터페이스 형식, 열거형, 클래스 및 대리자 형식입니다.

클래스 형식의 데이터 멤버 (필드) 및 함수 멤버 (메서드, 속성 및 다른 사용자)을 포함 하는 데이터 구조를 정의 합니다. 클래스 형식은 단일 상속 및 다형성과 파생된 클래스가 기본 클래스를 확장하고 특수화할 수 있는 메커니즘을 지원합니다.

구조체 형식을 나타내는 데이터 멤버 및 함수 멤버를 사용 하 여 구조체 클래스 형식와 비슷합니다. 그러나 클래스와 달리 구조체 값 형식이 며 힙 할당이 필요 하지 않습니다. 구조체 형식은 사용자 지정 상속을 지원하지 않으며 모든 구조체 형식은 `object` 형식에서 암시적으로 상속됩니다.

공용 함수 멤버의 명명된 된 집합으로 계약을 정의 하는 인터페이스 형식입니다. 클래스 또는 구조체는 인터페이스를 구현 하는 인터페이스의 함수 멤버의 구현을 제공 해야 합니다. 여러 기본 인터페이스에서 상속할 수 및 클래스 또는 구조체는 여러 인터페이스를 구현할 수 있습니다.

대리자 형식이 특정 매개 변수 목록 및 반환 형식을 사용 하 여 메서드에 대 한 참조를 나타냅니다. 대리자는 메서드를 변수에 할당되고 매개 변수로 전달될 수 있는 엔터티로 취급할 수 있도록 합니다. 또한 대리자는 다른 언어에 나오는 함수 포인터의 개념과 비슷하지만 함수 포인터와 달리 대리자는 개체 지향적이며 형식 안전 방식입니다.

클래스, 구조체, 인터페이스 및 대리자 형식 모두 제네릭을 지원 하므로 수 수 매개 변수화 다른 형식을 사용 합니다.

명명 된 상수를 사용 하 여 고유 형식인 열거형 형식입니다. 모든 열거형 형식을는 기본 형식, 8 가지 정수 형식 중 하나 여야 합니다. 열거형 형식의 값 집합이 기본 형식의 값 집합과 동일 합니다.

C#은 형식의 단일 차원 및 다차원 배열을 지원합니다. 위에 나열된 형식과 달리, 배열 형식은 사용하기 전에 먼저 선언할 필요가 없습니다. 대신, 배열 형식은 형식 이름을 대괄호로 묶어 생성합니다. 예를 들어 `int[]` 의 1 차원 배열입니다 `int`, `int[,]` 의 2 차원 배열입니다 `int`, 및 `int[][]` 는 1 차원 배열의 1 차원 배열 `int`합니다.

Nullable 형식은 또한 사용할 수 있으려면 먼저 선언할 수 없습니다. 각 nullable이 아닌 값 형식에 대 한 `T` 해당 nullable 형식이 `T?`에 추가 값을 포함할 수 있는 `null`합니다. 예를 들어 `int?` 32 비트 정수 또는 값을 보유할 수 있는 형식인 `null`합니다.

C#의 형식 시스템은 모든 형식의 값 개체로 처리할 수 있도록 통합 됩니다. C#의 모든 형식은 `object` 클래스 형식에서 직접 또는 간접적으로 파생되고 `object`는 모든 형식의 기본 클래스입니다. 참조 형식의 값은 `object`로 인식함으로써 간단히 개체로 처리됩니다. 값 형식의 값은 수행 하 여 개체로 처리 됩니다 ***boxing*** 하 고 ***unboxing*** 작업 합니다. 다음 예제에서 `int` 값은 `object`로 변환되었다가 다시 `int`로 변환됩니다.

```csharp
using System;

class Test
{
    static void Main() {
        int i = 123;
        object o = i;          // Boxing
        int j = (int)o;        // Unboxing
    }
}
```
값 형식이 값 형식으로 변환 되 면 `object`"box" 라고도 하는 개체 인스턴스 값을 보유할 할당 되 고 값이 해당 box에 복사 됩니다. 반대로,는 `object` 참조 값 형식으로 캐스팅 됩니다, 올바른 값 형식의 상자는 참조 된 개체는 검사가 수행 됩니다 및 검사에 성공 하면 상자에 값이 복사 됩니다.

C# 통합된 형식 시스템을 효과적으로 값 형식이 요청 합니다."시" 개체가 될 수는 의미 통합 때문에 `object` 형식을 사용하는 범용 라이브러리는 참조 형식 및 값 형식 둘 다에 사용될 수 있습니다.

C#에는 필드, 배열 요소, 지역 변수 및 매개 변수를 포함하는 여러 종류의 ***변수***가 있습니다. 변수는 저장소 위치를 나타내고 수 있는 값을 결정 하는 형식이 모든 변수에 다음 표에 표시 된 것과 같이 변수에 저장 합니다.


| __변수 형식__    | __가능한 콘텐츠__ |
|-------------------------|-----------------------|
| Null을 허용하지 않는 값 형식 | 정확한 해당 형식의 값 |
| Null 허용 값 형식     | Null 값 또는 정확한 해당 형식의 값 |
| `object`                | Null 참조, 참조 형식의 개체에 대 한 참조 또는 값 형식의 boxed 값에 대 한 참조 |
| 클래스 형식              | 해당 클래스 형식에서 파생 된 클래스의 인스턴스에 대 한 참조를 null 참조, 해당 클래스 형식의 인스턴스에 대 한 참조 |
| 인터페이스 유형          | Null 참조, 해당 인터페이스 형식을 구현 하는 클래스 형식의 인스턴스에 대 한 참조 또는 해당 인터페이스 형식을 구현 하는 값 형식의 boxed 값에 대 한 참조 |
| 배열 형식              | Null 참조, 해당 배열 형식의 인스턴스에 대 한 참조 또는 호환 되는 배열 형식의 인스턴스에 대 한 참조 |
| 대리자 형식           | Null 참조 또는 해당 대리자 형식의 인스턴스에 대 한 참조 |

## <a name="expressions"></a>식

***식***은 ***피연산자*** 및 ***연산자***로 생성됩니다. 식의 연산자는 피연산자에 적용할 연산을 나타냅니다. 연산자의 예로 `+`, `-`, `*`, `/` 및 `new`가 있습니다. 피연산자의 예로는 리터럴, 필드, 지역 변수 및 식이 있습니다.

식에 여러 연산자가 포함되어 있으면 연산자의 ***우선 순위***에 따라 개별 연산자가 계산되는 순서가 제어됩니다. 예를 들어 `*` 연산자는 `+` 연산자보다 우선 순위가 더 높기 때문에 식 `x + y * z`는 `x + (y * z)`로 계산됩니다.

대부분의 연산자는 ***오버로드***할 수 있습니다. 연산자 오버로드는 피연산자 중 하나 또는 둘 다가 사용자 정의 클래스 또는 구조체 형식인 연산에 대해 사용자 정의 연산자 구현을 지정할 수 있도록 허용합니다.

다음 표에서 순위가 가장 높은 우선 순위에 따라에서 연산자 범주를 나열 하는 C# 연산자를 보여 줍니다. 동일한 범주의 연산자는 우선 순위가 같습니다.


| __범주__                     | __식__    | __설명__ |
|----------------------------------|-------------------|-----------------|
| 기본 연산자                          | `x.m`             | 멤버 액세스 |
|                                  | `x(...)`          | 메서드 및 대리자 호출 |
|                                  | `x[...]`          | 배열 및 인덱서 액세스 |
|                                  | `x++`             | 후위 증가 |
|                                  | `x--`             | 후위 감소 |
|                                  | `new T(...)`      | 개체 및 대리자 생성 |
|                                  | `new T(...){...}` | 이니셜라이저를 사용 하 여 개체 만들기 |
|                                  | `new {...}`       | 익명 개체 이니셜라이저 |
|                                  | `new T[...]`      | 배열 만들기 |
|                                  | `typeof(T)`       | 가져올 `System.Type` 개체 `T` |
|                                  | `checked(x)`      | checked 컨텍스트에서 식 계산 |
|                                  | `unchecked(x)`    | unchecked 컨텍스트에서 식 계산 |
|                                  | `default(T)`      | 형식의 기본값 가져오기 `T` |
|                                  | `delegate {...}`  | 익명 함수(무명 메서드) |
| 단항                            | `+x`              | 클레임 |
|                                  | `-x`              | 부정 |
|                                  | `!x`              | 논리 부정 |
|                                  | `~x`              | 비트 부정 연산 |
|                                  | `++x`             | 전위 증가 |
|                                  | `--x`             | 전위 감소 |
|                                  | `(T)x`            | 명시적으로 변환 `x` 형식 `T` |
|                                  | `await x`         | 비동기적으로 대기할 `x` 완료 |
| 곱하기                   | `x * y`           | 곱하기 |
|                                  | `x / y`           | 나눗셈 기호 |
|                                  | `x % y`           | 나머지 |
| 더하기                         | `x + y`           | 더하기, 문자열 연결, 대리자 결합 |
|                                  | `x - y`           | 빼기, 대리자 제거 |
| 시프트                            | `x << y`          | 왼쪽 시프트 |
|                                  | `x >> y`          | 오른쪽 시프트 |
| 관계형 및 형식 테스트      | `x < y`           | 보다 작음 |
|                                  | `x > y`           | 보다 큼 |
|                                  | `x <= y`          | 작거나 같음 |
|                                  | `x >= y`          | 크거나 같음 |
|                                  | `x is T`          | 반환 `true` 경우 `x` 되는 `T`, `false` 그렇지 않은 경우 |
|                                  | `x as T`          | 반환 `x` 로 형식화 `T`, 또는 `null` 경우 `x` 아닙니다를 `T` |
| 같음                         | `x == y`          | Equal      |
|                                  | `x != y`          | 같지 않음 |
| 논리적 AND                      | `x & y`           | 정수 비트 AND, 부울 논리곱 AND |
| 논리 XOR                      | `x ^ y`           | 정수 비트 XOR, 부울 논리곱 XOR |
| 논리적 OR                       | ' x | y'           | 정수 비트 OR, 부울 논리곱 OR |
| 조건부 AND                  | `x && y`          | 평가 `y` 경우에만 `x` 는 `true` |
| 조건부 OR                   | ' x || y'          | 평가 `y` 경우에만 `x` 는 `false` |
| Null 결합                  | `X ?? y`          | 로 `y` 경우 `x` 됩니다 `null`를 `x` 그렇지 않은 경우 |
| 조건                      | `x ? y : z`       | 평가 `y` 하는 경우 `x` 됩니다 `true`, `z` 경우 `x` 됩니다 `false` |
| 대입 또는 익명 함수 | `x = y`           | 할당 |
|                                  | `x op= y`         | 복합 할당 지원 되는 연산자는 `*=` `/=` `%=` `+=` `-=` `<<=` `>>=` `&=` `^=` `|=` |
|                                  | `(T x) => y`      | 익명 함수(람다 식) |

## <a name="statements"></a>문

프로그램의 동작은 ***문***을 사용하여 표현됩니다. C#은 여러 다른 종류의 문을 지원하며 이중 많은 문이 포함 문에 대해 정의됩니다.

***블록***은 단일 문이 허용되는 컨텍스트에서 여러 문을 쓸 수 있도록 허용합니다. 블록은 구분 기호 `{`와 `}` 사이에 쓴 문 목록으로 구성됩니다.

***선언 문***은 지역 변수 및 상수를 선언하는 데 사용됩니다.

***식 문***은 식을 평가하는 데 사용됩니다. 할당을 사용 하 여 개체 메서드 호출을 포함 하는 문으로 사용할 수 있는 식의 `new` 연산자를 사용 하 여 할당 `=` 복합 할당 연산자를 사용 합니다 증가및감소작업`++`고 `--` 연산자 await 식 및 합니다.

***선택 문***은 일부 식 값에 따라 실행할 수 있는 다양한 문 중에서 하나를 선택하는 데 사용됩니다. 이 그룹에는 `if` 및 `switch` 문이 포함됩니다.

***반복 문*** 포함된 문을 반복적으로 실행 하는 데 사용 됩니다. 이 그룹에는 `while`, `do`, `for` 및 `foreach` 문이 포함됩니다.

***점프 문***은 제어를 전달하는 데 사용됩니다. 이 그룹에는 `break`, `continue`, `goto`, `throw`, `return` 및 `yield` 문이 포함됩니다.

`try`... `catch` 문은 블록 실행 중에 발생하는 예외를 catch하는 데 사용되고 `try`... `finally` 문은 예외 발생 여부에 관계 없이 항상 실행되는 종료 코드를 지정하는 데 사용됩니다.

합니다 `checked` 및 `unchecked` 문을 사용 하 여 오버플로 검사 정수 형식 산술 연산 및 변환에 대 한 컨텍스트를 제어 합니다.

`lock` 문은 지정된 개체에 대한 상호 배타적 잠금을 획득하고, 문을 실행한 후 잠금을 해제하는 데 사용됩니다.

`using` 문은 리소스를 획득하고, 문을 실행한 후 해당 리소스를 삭제하는 데 사용됩니다.

다음은 문의 각 종류의 예

__지역 변수 선언__

```csharp
static void Main() {
   int a;
   int b = 2, c = 3;
   a = 1;
   Console.WriteLine(a + b + c);
}
```


__지역 상수 선언__

```csharp
static void Main() {
    const float pi = 3.1415927f;
    const int r = 25;
    Console.WriteLine(pi * r * r);
}
```


__식 문__

```csharp
static void Main() {
    int i;
    i = 123;                // Expression statement
    Console.WriteLine(i);   // Expression statement
    i++;                    // Expression statement
    Console.WriteLine(i);   // Expression statement
}
```

__`if` 문__

```csharp
static void Main(string[] args) {
    if (args.Length == 0) {
        Console.WriteLine("No arguments");
    }
    else {
        Console.WriteLine("One or more arguments");
    }
}
```


__`switch` 문__

```csharp
static void Main(string[] args) {
    int n = args.Length;
    switch (n) {
        case 0:
            Console.WriteLine("No arguments");
            break;
        case 1:
            Console.WriteLine("One argument");
            break;
        default:
            Console.WriteLine("{0} arguments", n);
            break;
    }
}
```

__`while` 문__

```csharp
static void Main(string[] args) {
    int i = 0;
    while (i < args.Length) {
        Console.WriteLine(args[i]);
        i++;
    }
}
```


__`do` 문__

```csharp
static void Main() {
    string s;
    do {
        s = Console.ReadLine();
        if (s != null) Console.WriteLine(s);
    } while (s != null);
}
```

__`for` 문__

```csharp
static void Main(string[] args) {
    for (int i = 0; i < args.Length; i++) {
        Console.WriteLine(args[i]);
    }
}
```

__`foreach` 문__

```csharp
static void Main(string[] args) {
    foreach (string s in args) {
        Console.WriteLine(s);
    }
}
```

__`break` 문__

```csharp
static void Main() {
    while (true) {
        string s = Console.ReadLine();
        if (s == null) break;
        Console.WriteLine(s);
    }
}
```

__`continue` 문__

```csharp
static void Main(string[] args) {
    for (int i = 0; i < args.Length; i++) {
        if (args[i].StartsWith("/")) continue;
        Console.WriteLine(args[i]);
    }
}
```

__`goto` 문__

```csharp
static void Main(string[] args) {
    int i = 0;
    goto check;
    loop:
    Console.WriteLine(args[i++]);
    check:
    if (i < args.Length) goto loop;
}
```

__`return` 문__

```csharp
static int Add(int a, int b) {
    return a + b;
}

static void Main() {
    Console.WriteLine(Add(1, 2));
    return;
}
```

__`yield` 문__

```csharp
static IEnumerable<int> Range(int from, int to) {
    for (int i = from; i < to; i++) {
        yield return i;
    }
    yield break;
}

static void Main() {
    foreach (int x in Range(-10,10)) {
        Console.WriteLine(x);
    }
}
```

__`throw` 및 `try` 문__

```csharp
static double Divide(double x, double y) {
    if (y == 0) throw new DivideByZeroException();
    return x / y;
}

static void Main(string[] args) {
    try {
        if (args.Length != 2) {
            throw new Exception("Two numbers required");
        }
        double x = double.Parse(args[0]);
        double y = double.Parse(args[1]);
        Console.WriteLine(Divide(x, y));
    }
    catch (Exception e) {
        Console.WriteLine(e.Message);
    }
    finally {
        Console.WriteLine("Good bye!");
    }
}
```

__`checked` 및 `unchecked` 문__

```csharp
static void Main() {
    int i = int.MaxValue;
    checked {
        Console.WriteLine(i + 1);        // Exception
    }
    unchecked {
        Console.WriteLine(i + 1);        // Overflow
    }
}
```

__`lock` 문__

```csharp
class Account
{
    decimal balance;
    public void Withdraw(decimal amount) {
        lock (this) {
            if (amount > balance) {
                throw new Exception("Insufficient funds");
            }
            balance -= amount;
        }
    }
}
```

__`using` 문__

```csharp
static void Main() {
    using (TextWriter w = File.CreateText("test.txt")) {
        w.WriteLine("Line one");
        w.WriteLine("Line two");
        w.WriteLine("Line three");
    }
}
```

## <a name="classes-and-objects"></a>클래스 및 개체

***클래스***는 C#의 가장 기본적인 형식입니다. 클래스는 상태(필드)와 작업(메서드 및 기타 함수 멤버)을 하나의 단위로 결합하는 데이터 구조입니다. 클래스는 해당 클래스의 동적으로 생성된 ***인스턴스***(***개체***라고도 함)에 대한 정의를 제공합니다. 클래스는 ***상속*** 및 ***다형성***과 ***파생된 클래스***가 ***기본 클래스***를 확장하고 특수화할 수 있는 메커니즘을 지원합니다.

새 클래스는 클래스 선언을 사용하여 만들어집니다. 클래스 선언은 클래스의 특성 및 한정자, 클래스의 이름, 기본 클래스(제공된 경우), 클래스로 구현되는 인터페이스를 지정하는 헤더로 시작합니다. 헤더 다음에는 구분 기호 `{` 및 `}` 간에 작성되는 멤버 선언 목록으로 구성되는 클래스 본문이 나옵니다.

다음은 `Point`라는 간단한 클래스 선언입니다.

```csharp
public class Point
{
    public int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```
클래스의 인스턴스는 새 인스턴스에 대한 메모리를 할당하고, 인스턴스를 초기화하는 생성자를 호출하고, 인스턴스에 대한 참조를 반환하는 `new` 연산자를 사용하여 만들어집니다. 다음 문은 두 개의 만듭니다 `Point` 개체 및 해당 개체에 대 한 참조가 두 변수에 저장 합니다.

```
Point p1 = new Point(0, 0);
Point p2 = new Point(10, 20);
```
개체에서 사용한 메모리는 개체가 더 이상 사용에서 하는 경우 자동으로 회수 됩니다. C#에서 개체를 명시적으로 할당 취소할 필요도 없으며 가능하지도 않습니다.

### <a name="members"></a>멤버

클래스의 멤버는 ***정적 멤버*** 하거나 ***인스턴스 멤버***합니다. 정적 멤버는 클래스에 속하며 인스턴스 멤버는 개체(클래스의 인스턴스)에 속합니다.

다음 표에서 클래스는 포함할 수는 멤버 종류에 대 한 개요를 제공 합니다.


| __멤버__   | __설명__ |
|------------  |-----------------|
| 상수    | 클래스와 연결된 상수 값 |
| 필드       | 클래스의 변수 |
| 메서드      | 클래스가 수행할 수 있는 계산 및 작업 |
| 속성   | 클래스의 명명된 속성에 대한 읽기 및 쓰기와 관련된 작업 |
| 인덱서     | 클래스 인스턴스를 배열처럼 인덱싱하는 것과 관련된 작업 |
| 이벤트       | 클래스에 의해 생성될 수 있는 알림 |
| 연산자    | 클래스가 지원하는 변환 및 식 연산자 |
| 생성자 | 클래스의 인스턴스 또는 클래스 자체를 초기화하는 데 필요한 작업 |
| 소멸자  | 클래스의 인스턴스가 영구적으로 삭제되기 전에 수행 작업 |
| 유형        | 클래스에 의해 선언된 중첩 형식 |

### <a name="accessibility"></a>액세스 가능성

클래스의 각 멤버에는 멤버에 액세스할 수 있는 프로그램 텍스트의 영역을 제어하는 액세스 가능성이 연결되어 있습니다. 액세스 가능성은 5가지 형태로 제공됩니다. 각각은 다음 표에 요약되어 있습니다.


| __액세스 가능성__    | __의미__ |
|----------------------|-----------------|
| `public`             | 액세스가 제한되지 않음 |
| `protected`          | 이 클래스 또는 이 클래스에서 파생된 클래스로만 액세스가 제한됨 |
| `internal`           | 이 프로그램으로만 액세스가 제한됨 |
| `protected internal` | 이 프로그램 또는 이 클래스에서 파생된 클래스로만 액세스가 제한됨 |
| `private`            | 이 클래스로만 액세스가 제한됨 |

### <a name="type-parameters"></a>형식 매개 변수

클래스 정의는 클래스 이름 다음에 대괄호로 묶은 형식 매개 변수 이름 목록을 지정하여 형식 매개 변수 집합을 지정할 수 있습니다. 형식 매개 변수 수는 클래스 선언의 본문에 클래스의 멤버를 정의 하는 데 사용 됩니다. 다음 예제에서 `Pair`의 형식 매개 변수는 `TFirst` 및 `TSecond`입니다.

```csharp
public class Pair<TFirst,TSecond>
{
    public TFirst First;
    public TSecond Second;
}
```
형식 매개 변수를 사용 하도록 선언 하는 클래스 형식에는 제네릭 클래스 형식을 이라고 합니다. 구조체, 인터페이스 및 대리자 형식도 제네릭일 수 있습니다.

제네릭 클래스를 사용하는 경우 각 형식 매개 변수에 대해 다음과 같은 형식 인수가 제공되어야 합니다.

```csharp
Pair<int,string> pair = new Pair<int,string> { First = 1, Second = "two" };
int i = pair.First;     // TFirst is int
string s = pair.Second; // TSecond is string
```
예: 제공 된 형식 인수를 사용 하 여 제네릭 형식 `Pair<int,string>
    ` 위에서 생성 된 형식 이라고 합니다.

### <a name="base-classes"></a>기본 클래스

클래스 선언은 클래스 이름 및 형식 매개 변수 뒤에 콜론과 기본 클래스의 이름을 사용하여 기본 클래스를 지정할 수 있습니다. 기본 클래스 지정을 생략하면 `object` 형식에서 파생되는 클래스와 같습니다. 다음 예제에서 `Point3D`의 기본 클래스는 `Point`이고 `Point`의 기본 클래스는 `object`입니다.

```csharp
public class Point
{
    public int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

public class Point3D: Point
{
    public int z;

    public Point3D(int x, int y, int z): base(x, y) {
        this.z = z;
    }
}
```
클래스는 기본 클래스의 멤버를 상속합니다. 상속은 클래스 인스턴스 및 정적 생성자와 기본 클래스의 소멸자를 제외 하 고, 기본 클래스의 모든 멤버를 암시적으로 포함 하는 것을 의미 합니다. 파생된 클래스를 상속하는 대상에 새 멤버를 추가할 수 있지만 상속된 멤버의 정의를 제거할 수 없습니다. 앞의 예제에서 `Point3D`는 `Point`에서 `x` 및 `y` 필드를 상속하고 모든 `Point3D` 인스턴스는 세 개의 필드, 즉 `x`, `y` 및 `z`를 포함합니다.

클래스 형식에서 해당 기본 클래스 형식 간에 암시적 변환이 존재합니다. 따라서 클래스 형식의 변수는 해당 클래스의 인스턴스 또는 파생된 모든 클래스의 인스턴스를 참조할 수 있습니다. 예를 들어 이전 클래스 선언에서 형식 `Point`의 변수는 `Point` 또는 `Point3D`를 참조할 수 있습니다.

```csharp
Point a = new Point(10, 20);
Point b = new Point3D(10, 20, 30);
```

### <a name="fields"></a>필드

필드는 클래스 또는 클래스의 인스턴스와 연결 된 변수.

필드를 사용 하 여 선언 된 `static` 한정자를 정의 ***정적 필드***합니다. 정적 필드는 정확히 하나의 저장 위치를 식별합니다. 생성된 클래스 인스턴스 수에 관계없이 정적 필드의 복사본은 하나뿐입니다.

없이 선언 된 필드를 `static` 한정자를 정의 ***인스턴스 필드***합니다. 클래스의 모든 인스턴스는 해당 클래스의 모든 인스턴스 필드의 별도 복사본을 포함합니다.

다음 예제에서 `Color` 클래스의 각 인스턴스는 `r`, `g` 및 `b` 인스턴스 필드의 별도 복사본을 갖지만 `Black`, `White`, `Red`, `Green` 및 `Blue` 정적 필드의 복사본은 하나뿐입니다.

```csharp
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);
    private byte r, g, b;

    public Color(byte r, byte g, byte b) {
        this.r = r;
        this.g = g;
        this.b = b;
    }
}
```
앞의 예제와 같이 ***읽기 전용 필드***는 `readonly` 한정자를 사용하여 선언될 수 있습니다. 에 할당 된 `readonly` 필드의 일부로 필드의 선언 또는 동일한 클래스의 생성자에서 에서만 발생할 수 있습니다.

### <a name="methods"></a>메서드

***메서드***는 개체 또는 클래스에서 수행할 수 있는 계산이나 작업을 구현하는 멤버입니다. ***정적 메서드***는 클래스를 통해 액세스됩니다. ***인스턴스 메서드***는 클래스의 인스턴스를 통해 액세스됩니다.

메서드는 대개 비어 있는 목록이 남아 있을 ***매개 변수***, 값 또는 메서드에 전달 된 변수 참조를 나타내는 및 ***반환 형식***를 계산 하 고 반환한 값의 형식을 지정 하는 메서드입니다. 메서드의 반환 형식은 `void` 값을 반환 하지 않는 경우.

형식과 마찬가지로 메서드에는 메서드가 호출될 때 형식 인수가 지정되어야 하는 형식 매개 변수 집합도 있을 수 있습니다. 형식과 달리 형식 인수는 종종 메서드 호출의 인수에서 유추될 수 있으므로 명시적으로 지정할 필요가 없습니다.

메서드의 ***시그니처***는 메서드가 선언되는 클래스에서 고유해야 합니다. 메서드 시그니처는 메서드의 이름, 형식 매개 변수의 수, 해당 매개 변수의 수, 한정자 및 형식으로 구성됩니다. 메서드 시그니처는 반환 형식을 포함하지 않습니다.

#### <a name="parameters"></a>매개 변수

매개 변수는 메서드에 값 또는 변수 참조를 전달하는 데 사용됩니다. 메서드의 매개 변수는 메서드가 호출될 때 지정된 ***인수***에서 실제 값을 가져옵니다. 매개 변수에는 값 매개 변수, 참조 매개 변수, 출력 매개 변수 및 매개 변수 배열의 네 가지 종류가 있습니다.

***값 매개 변수***는 입력 매개 변수 전달에 사용됩니다. 값 매개 변수는 매개 변수에 전달된 인수에서 초기 값을 가져오는 지역 변수에 해당합니다. 값 매개 변수를 수정해도 매개 변수에 전달된 인수에는 영향을 주지 않습니다.

해당 인수를 생략할 수 있도록 기본값을 지정하면 값 매개 변수는 선택적일 수 있습니다.

***참조 매개 변수***는 입력 및 출력 매개 변수 전달 둘 다에 사용됩니다. 참조 매개 변수에 전달되는 인수는 변수여야 하며, 메서드를 실행하는 동안 참조 매개 변수는 인수 변수와 동일한 저장소 위치를 나타냅니다. 참조 매개 변수는 `ref` 한정자를 사용하여 선언됩니다. 다음 예제에서는 `ref` 매개 변수를 사용하는 방법을 보여 줍니다.

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
        Console.WriteLine("{0} {1}", i, j);            // Outputs "2 1"
    }
}
```
***출력 매개 변수***는 출력 매개 변수 전달에 사용됩니다. 출력 매개 변수는 호출자가 제공한 인수의 초기 값이 중요하지 않다는 점을 제외하고 참조 매개 변수와 비슷합니다. 출력 매개 변수는 `out` 한정자를 사용하여 선언됩니다. 다음 예제에서는 `out` 매개 변수를 사용하는 방법을 보여 줍니다.

```csharp
using System;

class Test
{
    static void Divide(int x, int y, out int result, out int remainder) {
        result = x / y;
        remainder = x % y;
    }

    static void Main() {
        int res, rem;
        Divide(10, 3, out res, out rem);
        Console.WriteLine("{0} {1}", res, rem);    // Outputs "3 1"
    }
}
```
***매개 변수 배열***은 다양한 개수의 인수가 메서드에 전달되도록 허용합니다. 매개 변수 배열은 `params` 한정자를 사용하여 선언됩니다. 메서드의 마지막 매개 변수만 매개 변수 배열일 수 있으며 매개 변수 배열의 형식은 1차원 배열 형식이어야 합니다. `Write` 하 고 `WriteLine` 의 메서드는 `System.Console` 클래스는 매개 변수 배열 사용의 좋은 예입니다. 이러한 메서드는 다음과 같이 선언됩니다.

```csharp
public class Console
{
    public static void Write(string fmt, params object[] args) {...}
    public static void WriteLine(string fmt, params object[] args) {...}
    ...
}
```
매개 변수 배열을 사용하는 메서드 내에서 매개 변수 배열은 배열 형식의 일반 매개 변수와 정확히 동일하게 동작합니다. 그러나 매개 변수 배열을 사용한 메서드 호출에서 매개 변수 배열 형식의 단일 인수 또는 매개 변수 배열에 있는 임의 개수의 요소 형식 인수를 전달할 수 있습니다. 후자의 경우 지정된 인수를 사용하여 배열 인스턴스가 자동으로 만들어지고 초기화됩니다. 다음 예제는

```csharp
Console.WriteLine("x={0} y={1} z={2}", x, y, z);
```
다음을 작성하는 것과 같습니다.

```csharp
string s = "x={0} y={1} z={2}";
object[] args = new object[3];
args[0] = x;
args[1] = y;
args[2] = z;
Console.WriteLine(s, args);
```

#### <a name="method-body-and-local-variables"></a>메서드 본문 및 지역 변수

메서드의 본문에는 메서드가 호출 될 때 실행할 문을 지정 합니다.

메서드 본문은 메서드 호출과 관련된 변수를 선언할 수 있습니다. 이러한 변수를 ***지역 변수***라고 합니다. 지역 변수 선언은 형식 이름, 변수 이름을 지정하며 초기 값을 지정할 수도 있습니다. 다음 예제에서는 초기 값이 0인 지역 변수 `i`와 초기 값이 없는 지역 변수 `j`를 선언합니다.

```csharp
using System;

class Squares
{
    static void Main() {
        int i = 0;
        int j;
        while (i < 10) {
            j = i * i;
            Console.WriteLine("{0} x {0} = {1}", i, j);
            i = i + 1;
        }
    }
}
```
C#에서는 해당 값을 얻기 위해 먼저 로컬 변수를 ***명확 하게 할당***해야 합니다. 예를 들어 이전 `i`의 선언에 초기 값이 포함되지 않으면 컴파일러는 `i`의 후속 사용에 대해 오류를 보고합니다. `i`는 프로그램에서 해당 시점에 명확하게 할당되지 않은 것이기 때문입니다.

메서드는 `return` 문을 사용하여 해당 호출자에게 컨트롤을 반환할 수 있습니다. `void`를 반환하는 메서드에서 `return` 문은 식을 지정할 수 없습니다. 메서드에서 반환 이외`void`, `return` 문을 반환 값을 계산 하는 식을 포함 해야 합니다.

#### <a name="static-and-instance-methods"></a>정적 및 인스턴스 메서드

메서드를 사용 하 여 선언 된 `static` 한정자가을 ***정적 메서드***합니다. 정적 메서드는 특정 인스턴스에 작동하지 않고 정적 멤버에 직접적으로만 액세스할 수 있습니다.

없이 선언 된 메서드를 `static` 한정자는 ***인스턴스 메서드***합니다. 인스턴스 메서드는 특정 인스턴스에 작동하며 정적 및 인스턴스 멤버 둘 다에 액세스할 수 있습니다. 인스턴스 메서드가 호출된 인스턴스는 `this`로 명시적으로 액세스할 수 있습니다. 정적 메서드에서 `this`를 참조하면 오류가 발생합니다.

다음 `Entity` 클래스에는 정적 멤버와 인스턴스 멤버가 모두 있습니다.

```csharp
class Entity
{
    static int nextSerialNo;
    int serialNo;

    public Entity() {
        serialNo = nextSerialNo++;
    }

    public int GetSerialNo() {
        return serialNo;
    }

    public static int GetNextSerialNo() {
        return nextSerialNo;
    }

    public static void SetNextSerialNo(int value) {
        nextSerialNo = value;
    }
}
```
각 `Entity` 인스턴스에는 일련 번호(및 여기에 표시되지 않는 일부 정보)가 포함되어 있습니다. `Entity` 생성자(인스턴스 메서드와 유사함)는 사용 가능한 다음 일련 번호를 사용하여 새 인스턴스를 초기화합니다. 생성자가 인스턴스 멤버이기 때문에 `serialNo` 인스턴스 필드 및 `nextSerialNo` 정적 필드 둘 다에 액세스하도록 허용됩니다.

`GetNextSerialNo` 및 `SetNextSerialNo` 정적 메서드는 `nextSerialNo` 정적 필드에 액세스할 수 있지만 `serialNo` 인스턴스 필드에 직접 액세스하면 오류가 발생합니다.

다음 예제에서는 사용 된 `Entity` 클래스입니다.

```csharp
using System;

class Test
{
    static void Main() {
        Entity.SetNextSerialNo(1000);
        Entity e1 = new Entity();
        Entity e2 = new Entity();
        Console.WriteLine(e1.GetSerialNo());           // Outputs "1000"
        Console.WriteLine(e2.GetSerialNo());           // Outputs "1001"
        Console.WriteLine(Entity.GetNextSerialNo());   // Outputs "1002"
    }
}
```
`SetNextSerialNo` 및 `GetNextSerialNo` 정적 메서드는 클래스에 대해 호출되지만 `GetSerialNo` 인스턴스 메서드는 클래스의 인스턴스에 대해 호출됩니다.

#### <a name="virtual-override-and-abstract-methods"></a>가상, 재정의 및 추상 메서드

인스턴스 메서드 선언에 `virtual` 한정자가 포함되면 해당 메서드를 ***가상 메서드***라고 합니다. 없는 경우 `virtual` 한정자가 있는 메서드를 라고는 ***비가상 메서드***합니다.

가상 메서드가 호출되면 호출이 발생하는 인스턴스의 ***런타임 형식***에 따라 호출할 실제 메서드 구현이 결정됩니다. 비가상 메서드 호출에서는 인스턴스의 ***컴파일 타임 형식***이 결정 요인입니다.

가상 메서드는 파생된 클래스에서 ***재정의***될 수 있습니다. 인스턴스 메서드 선언 포함 되는 경우는 `override` 한정자를 메서드 시그니처가 같은 상속된 된 가상 메서드를 재정의 합니다. 가상 메서드 선언은 새 메서드를 도입하지만 재정의 메서드 선언은 해당 메서드의 새 구현을 제공하여 기존의 상속된 가상 메서드를 특수화합니다.

***추상*** 메서드는 구현이 없는 가상 메서드입니다. 추상 메서드를 사용 하 여 선언 되는 `abstract` 한정자를 선언 하는 클래스에만 사용할 수 `abstract`입니다. 추상 메서드는 모든 비추상 파생 클래스에서 재정의해야 합니다.

다음 예제에서는 식 트리 노드를 나타내는 추상 클래스 `Expression`와 상수, 변수 참조 및 산술 연산에 대한 식 트리 노드를 구현하는 세 개의 파생 클래스 `Constant`, `VariableReference` 및 `Operation`을 선언합니다. (비슷하지만 이지만에 도입 된 식 트리 형식과와 혼동 해서는 [식 트리 형식](types.md#expression-tree-types)).

```csharp
using System;
using System.Collections;

public abstract class Expression
{
    public abstract double Evaluate(Hashtable vars);
}

public class Constant: Expression
{
    double value;

    public Constant(double value) {
        this.value = value;
    }

    public override double Evaluate(Hashtable vars) {
        return value;
    }
}

public class VariableReference: Expression
{
    string name;

    public VariableReference(string name) {
        this.name = name;
    }

    public override double Evaluate(Hashtable vars) {
        object value = vars[name];
        if (value == null) {
            throw new Exception("Unknown variable: " + name);
        }
        return Convert.ToDouble(value);
    }
}

public class Operation: Expression
{
    Expression left;
    char op;
    Expression right;

    public Operation(Expression left, char op, Expression right) {
        this.left = left;
        this.op = op;
        this.right = right;
    }

    public override double Evaluate(Hashtable vars) {
        double x = left.Evaluate(vars);
        double y = right.Evaluate(vars);
        switch (op) {
            case '+': return x + y;
            case '-': return x - y;
            case '*': return x * y;
            case '/': return x / y;
        }
        throw new Exception("Unknown operator");
    }
}
```
이전의 4개 클래스는 산술 연산자를 모델링하는 데 사용할 수 있습니다. 예를 들어 이러한 클래스의 인스턴스를 사용할 경우 식 `x + 3`을 다음과 같이 나타낼 수 있습니다.

```csharp
Expression e = new Operation(
    new VariableReference("x"),
    '+',
    new Constant(3));
```
`Expression` 인스턴스의 `Evaluate` 메서드는 지정된 식을 계산하고 `double` 값을 생성하기 위해 호출됩니다. 메서드는 인수로 `Hashtable` 변수 이름 (항목의 키)과 값 (항목의 값)를 포함 하는 합니다. `Evaluate` 메서드는 한 가상 abstract 메서드입니다. 즉, 비추상 파생된 클래스가 실제 구현을 제공 하도록 재정의 해야 합니다.

`Evaluate`의 `Constant` 구현은 단순히 저장된 상수를 반환합니다. `VariableReference`의 구현에서 해시 테이블 변수 이름 조회 하 고 결과 값을 반환 합니다. `Operation`의 구현은 먼저 왼쪽 및 오른쪽 피연산자를 계산하고(재귀적으로 해당 `Evaluate` 메서드 호출) 지정된 산술 연산을 수행합니다.

다음 프로그램에서는 `Expression` 클래스를 사용하여 `x` 및 `y`의 다른 값에 대해 식 `x * (y + 2)`를 계산합니다.

```csharp
using System;
using System.Collections;

class Test
{
    static void Main() {
        Expression e = new Operation(
            new VariableReference("x"),
            '*',
            new Operation(
                new VariableReference("y"),
                '+',
                new Constant(2)
            )
        );
        Hashtable vars = new Hashtable();
        vars["x"] = 3;
        vars["y"] = 5;
        Console.WriteLine(e.Evaluate(vars));        // Outputs "21"
        vars["x"] = 1.5;
        vars["y"] = 9;
        Console.WriteLine(e.Evaluate(vars));        // Outputs "16.5"
    }
}
```

#### <a name="method-overloading"></a>메서드 오버로드

메서드 ***오버로드***는 동일한 클래스가 고유한 시그니처를 갖는 한, 동일한 이름을 갖도록 허용합니다. 오버로드된 메서드의 호출을 컴파일할 때 컴파일러는 ***오버로드 확인***을 사용하여 호출할 특정 메서드를 결정합니다. 오버로드 확인은 인수와 가장 적합하게 일치하는 단일 메서드를 찾으며, 최상의 일치 메서드를 찾을 수 있는 경우 오류를 보고합니다. 다음 예제에서는 실제로 진행되는 오버로드 확인을 보여 줍니다. `Main` 메서드의 각 호출에 대한 주석은 실제로 호출되는 메서드를 보여 줍니다.

```csharp
class Test
{
    static void F() {
        Console.WriteLine("F()");
    }

    static void F(object x) {
        Console.WriteLine("F(object)");
    }

    static void F(int x) {
        Console.WriteLine("F(int)");
    }

    static void F(double x) {
        Console.WriteLine("F(double)");
    }

    static void F<T>(T x) {
        Console.WriteLine("F<T>(T)");
    }

    static void F(double x, double y) {
        Console.WriteLine("F(double, double)");
    }

    static void Main() {
        F();                 // Invokes F()
        F(1);                // Invokes F(int)
        F(1.0);              // Invokes F(double)
        F("abc");            // Invokes F(object)
        F((double)1);        // Invokes F(double)
        F((object)1);        // Invokes F(object)
        F<int>(1);           // Invokes F<T>(T)
        F(1, 1);             // Invokes F(double, double)
    }
}
```
예제와 같이, 인수를 정확한 매개 변수 형식으로 명시적으로 캐스팅하거나 형식 인수를 명시적으로 제공하여 항상 특정 메서드를 선택할 수 있습니다.

### <a name="other-function-members"></a>기타 함수 멤버

실행 코드를 포함하는 멤버를 통칭하여 클래스의 ***함수 멤버***라고 합니다. 이전 섹션에서는 함수 멤버의 기본 종류인 메서드에 대해 설명합니다. 이 섹션에서는 C#에서 지 원하는 함수 멤버의 다른 종류를 설명 합니다: 생성자, 속성, 인덱서, 이벤트, 연산자 및 소멸자입니다.

다음 코드는 라는 제네릭 클래스를 보여 줍니다. `List<T>`, growable 개체 목록을 구현 합니다. 이 클래스는 함수 멤버의 가장 일반적인 몇 가지 예제를 포함합니다.


```csharp
public class List<T> {
    // Constant...
    const int defaultCapacity = 4;

    // Fields...
    T[] items;
    int count;

    // Constructors...
    public List(int capacity = defaultCapacity) {
        items = new T[capacity];
    }

    // Properties...
    public int Count {
        get { return count; }
    }
    public int Capacity {
        get {
            return items.Length;
        }
        set {
            if (value < count) value = count;
            if (value != items.Length) {
                T[] newItems = new T[value];
                Array.Copy(items, 0, newItems, 0, count);
                items = newItems;
            }
        }
    }

    // Indexer...
    public T this[int index] {
        get {
            return items[index];
        }
        set {
            items[index] = value;
            OnChanged();
        }
    }

    // Methods...
    public void Add(T item) {
        if (count == Capacity) Capacity = count * 2;
        items[count] = item;
        count++;
        OnChanged();
    }
    protected virtual void OnChanged() {
        if (Changed != null) Changed(this, EventArgs.Empty);
    }
    public override bool Equals(object other) {
        return Equals(this, other as List<T>);
    }
    static bool Equals(List<T> a, List<T> b) {
        if (a == null) return b == null;
        if (b == null || a.count != b.count) return false;
        for (int i = 0; i < a.count; i++) {
            if (!object.Equals(a.items[i], b.items[i])) {
                return false;
            }
        }
        return true;
    }

    // Event...
    public event EventHandler Changed;

    // Operators...
    public static bool operator ==(List<T> a, List<T> b) {
        return Equals(a, b);
    }
    public static bool operator !=(List<T> a, List<T> b) {
        return !Equals(a, b);
    }
}
```

#### <a name="constructors"></a>생성자

C#은 인스턴스 및 정적 생성자를 모두 지원합니다. ***인스턴스 생성자***는 클래스의 인스턴스를 초기화하는 데 필요한 작업을 구현하는 멤버입니다. ***정적 생성자***는 처음 로드될 때 클래스 자체를 인스턴스화하는 데 필요한 작업을 구현하는 멤버입니다.

생성자는 반환 형식이 없고 포함하는 클래스와 동일한 이름을 갖는 메서드처럼 선언됩니다. 생성자 선언에 포함 된 경우는 `static` 한정자를 정적 생성자를 선언 합니다. 그렇지 않으면 인스턴스 생성자를 선언합니다.

인스턴스 생성자를 오버 로드할 수 있습니다. 예를 들어 `List<T>
` 클래스는 2개의 인스턴스 생성자, 즉, 매개 변수가 없는 생성자와 `int` 매개 변수를 취하는 생성자를 선언합니다. 인스턴스 생성자는 `new` 연산자를 사용하여 호출됩니다. 다음 문은 두 할당할 `List<string>
` 각각의 생성자를 사용 하 여 인스턴스를 `List` 클래스입니다.

```csharp
List<string> list1 = new List<string>();
List<string> list2 = new List<string>(10);
```
다른 멤버와 달리 인스턴스 생성자는 상속되지 않으며 클래스에는 클래스에서 실제로 선언된 인스턴스 생성자만 포함됩니다. 클래스에 대해 인스턴스 생성자가 제공되지 않으면 매개 변수가 없는 빈 인스턴스 생성자가 자동으로 제공됩니다.

#### <a name="properties"></a>속성

***속성***은 필드의 기본 확장입니다. 둘 다 연결된 형식으로 명명되는 멤버이며, 필드 및 속성에 액세스하는 구문은 동일합니다. 그러나 필드와 달리 속성은 저장 위치를 명시하지 않습니다. 대신, 속성에는 해당 값을 읽거나 쓸 때 실행될 문을 지정하는 ***접근자***가 있습니다.

속성 선언 끝나는 제외 하 고 필드 처럼 선언 됩니다는 `get` 접근자 및/또는 `set` 구분 기호 사이 기록 된 접근자 `{` 및 `}` 세미콜론으로 종료 하는 대신 합니다. 둘 다 포함 된 속성을 `get` 접근자 및 `set` 접근자가는 ***읽기 / 쓰기 속성***만 있는 속성을 `get` 접근자가를 ***읽기 전용 속성***, 및 만 있는 속성을 `set` 접근자를 ***쓰기 전용 속성***합니다.

`get` 접근자는 속성 형식의 반환 값을 사용 하 여 매개 변수가 없는 메서드에 해당 합니다. 속성 식에서 참조 될 때 할당의 대상으로 제외 하 고는 `get` 속성의 접근자 속성의 값을 계산 호출 됩니다.

A `set` 라는 단일 매개 변수를 사용 하 여 메서드에 해당 하는 접근자 `value` 및 반환 형식이 없습니다. 속성의 피연산자 또는 할당의 대상으로 참조 되는 경우 `++` 나 `--`, `set` 접근자가 새 값을 제공 하는 인수를 사용 하 여 호출 됩니다.

`List<T>
` 클래스에는 두 개의 속성 선언 `Count` 및 `Capacity`는 읽기 전용 및 읽기 / 쓰기, 각각. 다음은 이러한 속성 사용의 예입니다.

```csharp
List<string> names = new List<string>();
names.Capacity = 100;            // Invokes set accessor
int i = names.Count;             // Invokes get accessor
int j = names.Capacity;          // Invokes get accessor
```
필드 및 메서드와 마찬가지로, C#은 인스턴스 속성 및 정적 속성을 모두 지원합니다. 정적 속성으로 선언 되는 `static` 한정자와 인스턴스 속성 없이 선언 됩니다.

속성의 접근자는 가상일 수 있습니다. 속성 선언에 `virtual`, `abstract`, 또는 `override` 한정자가 포함되면 속성의 접근자에 적용됩니다.

#### <a name="indexers"></a>인덱서

***인덱서***는 개체가 배열과 같은 방식으로 인덱싱될 수 있도록 하는 멤버입니다. 인덱서는이 멤버의 이름을 제외 하 고 속성 처럼 선언 됩니다 `this` 구분 기호 사이 기록 된 매개 변수 목록 뒤 `[` 고 `]`입니다. 매개 변수는 인덱서의 접근자에서 사용할 수 있습니다. 속성과 마찬가지로 인덱서는 읽기/쓰기, 읽기 전용 및 쓰기 전용일 수 있으며 인덱서의 접근자는 가상일 수 있습니다.

`List` 클래스는 `int` 매개 변수를 사용하는 단일 읽기/쓰기 인덱서를 선언합니다. 인덱서는 `List` 인스턴스를 `int` 값으로 인덱싱할 수 있도록 합니다. 예

```csharp
List<string> names = new List<string>();
names.Add("Liz");
names.Add("Martha");
names.Add("Beth");
for (int i = 0; i < names.Count; i++) {
    string s = names[i];
    names[i] = s.ToUpper();
}
```
인덱서는 오버로드될 수 있습니다. 즉, 해당 매개 변수의 수와 형식이 다를 경우 한 클래스가 여러 인덱서를 선언할 수 있습니다.

#### <a name="events"></a>이벤트

***이벤트***는 클래스 또는 개체가 알림을 제공할 수 있도록 하는 멤버입니다. 이벤트 선언을 포함 된다는 점을 제외 하 고 필드 처럼 선언 됩니다는 `event` 키워드 및 형식에는 대리자 형식 이어야 합니다.

이벤트 멤버를 선언하는 클래스 내에서 이벤트는 대리자 형식의 필드처럼 동작합니다(이벤트가 추상이 아니고 접근자를 선언하지 않을 경우). 필드는 이벤트에 추가된 이벤트 처리기를 나타내는 대리자에 대한 참조를 저장합니다. 필드는 이벤트 핸들이 없는 경우 `null`합니다.

`List<T>
` 클래스는 `Changed`라는 단일 이벤트 멤버를 선언합니다. 이것은 새 항목이 목록에 추가되었음을 나타냅니다. 합니다 `Changed` 이벤트를 발생 합니다 `OnChanged` 는 첫 번째 이벤트 인지를 확인 하는 가상 메서드를 `null` (처리기가 있는 것을 의미). 이벤트 발생 개념은 이벤트가 나타내는 대리자를 호출하는 것과 정확히 동일하므로 이벤트 발생을 위한 특수한 언어 구문은 없습니다.

클라이언트는 ***이벤트 처리기***를 통해 이벤트에 반응합니다. 이벤트 처리기는 `+=` 연산자를 사용하여 추가되고, `-=` 연산자를 사용하여 제거됩니다. 다음 예제에서는 이벤트 처리기를 `List<string>
`의 `Changed` 이벤트에 추가합니다.

```csharp
using System;

class Test
{
    static int changeCount;

    static void ListChanged(object sender, EventArgs e) {
        changeCount++;
    }

    static void Main() {
        List<string> names = new List<string>();
        names.Changed += new EventHandler(ListChanged);
        names.Add("Liz");
        names.Add("Martha");
        names.Add("Beth");
        Console.WriteLine(changeCount);        // Outputs "3"
    }
}
```
이벤트의 기본 저장소를 제어하려고 하는 고급 시나리오의 경우 이벤트 선언에서 속성의 `set` 접근자와 비슷한 `add` 및 `remove` 접근자를 명시적으로 제공할 수 있습니다.

#### <a name="operators"></a>연산자

***연산자***는 클래스 인스턴스에 특정 식 연산자를 적용하는 것의 의미를 정의하는 멤버입니다. 세 가지 종류의 연산자, 즉, 단항 연산자, 이항 연산자 및 변환 연산자를 정의할 수 있습니다. 모든 연산자는 `public` 및 `static`으로 선언해야 합니다.

`List<T>
` 클래스는 두 가지 연산자인 `operator==` 및 `operator!=`를 선언하므로 해당 연산자를 `List` 인스턴스에 적용하는 새로운 의미를 식에 지정합니다. 연산자에서 두 개의 일치를 정의 하는 특히 `List<T>
` 비교를 사용 하 여 포함 된 개체는 각각의 인스턴스로 해당 `Equals` 메서드. 다음 예제에서는 `==` 연산자를 사용하여 두 `List<int>
` 인스턴스를 비교합니다.

```csharp
using System;

class Test
{
    static void Main() {
        List<int> a = new List<int>();
        a.Add(1);
        a.Add(2);
        List<int> b = new List<int>();
        b.Add(1);
        b.Add(2);
        Console.WriteLine(a == b);        // Outputs "True"
        b.Add(3);
        Console.WriteLine(a == b);        // Outputs "False"
    }
}
```

두 목록은 같은 순서로 같은 값을 갖는 동일한 수의 개체를 포함하므로 첫 번째 `Console.WriteLine`은 `True`를 출력합니다. `List<T>
`에서 `operator==`이 정의되지 않았으면 `a` 및 `b`은 다른 `List<int>
` 인스턴스를 참조하므로 첫 번째 `Console.WriteLine`은 `False`를 출력합니다.

#### <a name="destructors"></a>소멸자

A ***소멸자*** 는 클래스의 인스턴스를 소멸 하는 데 필요한 작업을 구현 하는 멤버입니다. 소멸자는 매개 변수를 사용할 수 없습니다, 액세스 가능성 한정자를 가질 수 없습니다 및 명시적으로 호출할 수 없습니다. 인스턴스에 대 한 소멸자는 가비지 수집 중 자동으로 호출 됩니다.

가비지 수집기는 유연 하 게 결정할 개체를 수집 하 고 소멸자를 실행 하는 경우 허용 됩니다. 특히 소멸자 호출의 타이밍 결정적 아니며 모든 스레드에서 소멸자를 실행할 수 있습니다. 이러한 및 기타 이유로 클래스는 가능한 다른 솔루션이 없는 경우에 소멸자를 구현 해야 합니다.

`using` 문은 개체 소멸을 위한 더 나은 방법을 제공합니다.

## <a name="structs"></a>구조체

***구조체***는 클래스처럼 데이터 멤버 및 함수 멤버를 포함할 수 있는 데이터 구조이지만 값 형식이며 힙 할당이 필요하지 않다는 점이 클래스와 다릅니다. 구조체 형식의 변수는 구조체의 데이터를 직접 저장하지만 클래스 형식의 변수는 동적으로 할당된 개체에 대한 참조를 저장합니다. 구조체 형식은 사용자 지정 상속을 지원하지 않으며 모든 구조체 형식은 `object` 형식에서 암시적으로 상속됩니다.

구조체는 값 의미 체계를 갖는 작은 데이터 구조에 특히 유용합니다. 복소수, 좌표계의 점 또는 사전의 키-값 쌍이 모두 구조체의 좋은 예입니다. 작은 데이터 구조에 클래스 대신 구조체를 사용하는 것은 응용 프로그램이 사용하는 메모리 할당 수에서 큰 차이를 보일 수 있습니다. 예를 들어 다음 프로그램은 100개의 점 배열을 만들고 초기화합니다. `Point`가 클래스로 구현될 경우 배열에 대해 1개, 100개 요소에 대해 각각 1개씩 101개의 별도 개체가 인스턴스화됩니다.

```csharp
class Point
{
    public int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

class Test
{
    static void Main() {
        Point[] points = new Point[100];
        for (int i = 0; i < 100; i++) points[i] = new Point(i, i);
    }
}
```
대안은 있도록 `Point` 구조체입니다.

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
이제 1개의 개체만 인스턴스화되고(배열에 대해 1개) `Point` 인스턴스는 배열에 인라인으로 저장됩니다.

구조체 생성자는 `new` 연산자로 호출되지만 메모리가 할당된다는 것을 의미하지는 않습니다. 개체를 동적으로 할당하고 그에 대한 참조를 반환하는 대신, 구조체 생성자는 단순히 구조체 값 자체(일반적으로 스택의 임시 위치에 있음)를 반환하며 이 값은 필요할 때 복사됩니다.

클래스에서는 두 가지 변수가 같은 개체를 참조할 수 있으므로 한 변수에 대한 작업이 다른 변수에서 참조하는 개체에 영향을 미칠 수 있습니다. 구조체에서는 변수 각각에 데이터의 자체 사본이 들어 있으며 한 변수의 작업이 다른 변수에 영향을 미칠 수 없습니다. 예를 들어, 다음 코드 조각에서 생성 된 출력 종속 여부 `Point` 가 클래스 또는 구조체입니다.

```csharp
Point a = new Point(10, 10);
Point b = a;
a.x = 20;
Console.WriteLine(b.x);
```
경우 `Point` 클래스는 출력은 `20` 있으므로 `a` 및 `b` 동일한 개체를 참조 합니다. 경우 `Point` 는 구조체, 출력은 `10` 때문에 할당 `a` 하 `b` 값의 복사본을 만듭니다이 복사본의 후속 대입에 의해 영향을 받지 않습니다. 및 `a.x`합니다.

이전 예제에는 구조체의 제한 사항 중 두 가지를 집중적으로 보여 줍니다. 첫째, 일반적으로 전체 구조체를 복사하는 것이 개체 참조를 복사하는 것보다 덜 효율적이므로 대입 및 값 매개 변수 전달이 참조 형식보다 덜 경제적일 수 있습니다. 둘째, `ref` 및 `out` 매개 변수를 제외하고, 구조체에 대한 참조를 만들 수 없으므로 다양한 상황에서 사용하는 것이 불가능합니다.

## <a name="arrays"></a>배열

***배열***은 계산된 인덱스를 통해 액세스되는 여러 변수를 포함하는 데이터 구조입니다. 배열에 포함된 변수, 즉 배열의 ***요소***라고도 하는 배열은 모두 같은 형식이며, 이 형식을 배열의 ***요소 형식***이라고 합니다.

배열 형식은 참조 형식이고 배열 변수의 선언은 배열 인스턴스에 대한 참조를 위한 공간을 설정합니다. 실제 배열 인스턴스는 런타임에 사용 하 여 동적으로 생성 됩니다는 `new` 연산자입니다. 합니다 `new` 작업을 지정 합니다 ***길이*** 인스턴스의 새 배열 인스턴스의 수명 동안 고정 됨. 배열 요소의 인덱스 범위는 `0`에서 `Length - 1` 사이입니다. `new` 연산자는 배열의 요소를 모든 숫자 형식에 대해 0이고, 모든 참조 형식에 대해 `null`인 기본값으로 자동으로 초기화합니다.

다음 예제에서는 `int` 요소의 배열을 만들고, 배열을 초기화하고, 배열의 콘텐츠를 출력합니다.

```csharp
using System;

class Test
{
    static void Main() {
        int[] a = new int[10];
        for (int i = 0; i < a.Length; i++) {
            a[i] = i * i;
        }
        for (int i = 0; i < a.Length; i++) {
            Console.WriteLine("a[{0}] = {1}", i, a[i]);
        }
    }
}
```
이 예제에서는 ***1차원 배열***을 만들고 작업을 수행합니다. C#에서는 ***다차원 배열s***을 지원하지 않습니다. 배열 형식의 ***순위***라고도 하는 배열 형식의 차원 수는 배열 형식의 대괄호 사이에 사용된 쉼표 수에 1을 더한 값입니다. 다음 예제에서는 1 차원, 2 차원 및 3 차원 배열을 할당합니다.

```csharp
int[] a1 = new int[10];
int[,] a2 = new int[10, 5];
int[,,] a3 = new int[10, 5, 2];
```
`a1` 배열에는 10개의 요소가 들어 있고 `a2` 배열에는 50(10 × 5)개의 요소가 들어 있고 `a3` 배열에는 100(10 × 5 × 2)개 요소가 들어 있습니다.

배열의 요소 형식은 배열 형식을 비롯한 어떤 형식도 될 수 있습니다. 배열 형식의 요소가 있는 배열을 ***가변 배열***이라고도 합니다. 요소 배열의 길이가 항상 동일할 필요는 없기 때문입니다. 다음 예제에서는 `int` 배열의 배열을 할당합니다.

```csharp
int[][] a = new int[3][];
a[0] = new int[10];
a[1] = new int[5];
a[2] = new int[20];
```
첫 번째 줄은 형식이 `int[]`이고 초기 값이 `null`인 3개 요소가 있는 배열을 만듭니다. 다음 줄은 가변 길이의 개별 배열 인스턴스에 대한 참조로 3개 요소를 초기화합니다.

합니다 `new` 연산자를 사용 하 여 배열 요소의 초기 값을 허용을 ***배열 이니셜라이저***, 구분 기호 사이 기록 된 식의 목록입니다 `{` 및 `}`합니다. 다음 예제에서는 3개 요소로 `int[]`를 할당하고 초기화합니다.

```csharp
int[] a = new int[] {1, 2, 3};
```
배열의 길이 사이의 식 수에서 유추 되 `{` 고 `}`입니다. 지역 변수 및 필드 선언은 배열 형식을 다시 시작할 필요가 없도록 좀 더 줄일 수 있습니다.

```csharp
int[] a = {1, 2, 3};
```
앞의 두 예제는 다음 예제와 동일합니다.

```csharp
int[] t = new int[3];
t[0] = 1;
t[1] = 2;
t[2] = 3;
int[] a = t;
```
## <a name="interfaces"></a>인터페이스

***인터페이스***는 클래스 및 구조체에서 구현될 수 있는 계약을 정의합니다. 인터페이스는 메서드, 속성, 이벤트 및 인덱서를 포함할 수 있습니다. 인터페이스는 정의하는 멤버의 구현을 제공하지 않으며 단순히 인터페이스를 구현하는 클래스 또는 구조체에서 제공해야 하는 멤버를 지정합니다.

인터페이스는 ***다중 상속***을 사용할 수 있습니다. 다음 예제에서 인터페이스 `IComboBox`는 `ITextBox` 및 `IListBox`를 둘 다 상속합니다.

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
클래스 및 구조체는 여러 인터페이스를 구현할 수 있습니다. 다음 예제에서 클래스 `EditBox`는 `IControl` 및 `IDataBound`를 둘 다 구현합니다.

```csharp
interface IDataBound
{
    void Bind(Binder b);
}

public class EditBox: IControl, IDataBound
{
    public void Paint() {...}
    public void Bind(Binder b) {...}
}
```
클래스 또는 구조체가 특정 인터페이스를 구현하는 경우 해당 클래스 또는 구조체의 인스턴스를 해당 인터페이스 형식으로 암시적으로 변환할 수 있습니다. 예

```csharp
EditBox editBox = new EditBox();
IControl control = editBox;
IDataBound dataBound = editBox;
```
인스턴스가 정적으로 특정 인터페이스를 구현하는 것으로 알려지지 않은 경우 동적 형식 캐스팅을 사용할 수 있습니다. 다음 문은 개체를 가져오려면 동적 형식 캐스팅을 사용 하는 예를 들어 `IControl` 고 `IDataBound` 인터페이스 구현. 개체의 실제 형식 이므로 `EditBox`, 캐스팅은 성공 합니다.

```csharp
object obj = new EditBox();
IControl control = (IControl)obj;
IDataBound dataBound = (IDataBound)obj;
```
이전 `EditBox` 클래스를 `Paint` 메서드에서 `IControl` 인터페이스 및 `Bind` 메서드를 `IDataBound` 인터페이스를 사용 하 여 구현 됩니다 `public` 멤버입니다. 또한 C# 지원 ***명시적 인터페이스 멤버 구현을***, 클래스를 사용 하는 구조체 구성원 작업을 방지할 수 또는 `public`합니다. 명시적 인터페이스 멤버 구현은 정규화된 인터페이스 멤버 이름을 사용하여 작성됩니다. 예를 들어 `EditBox` 클래스는 다음과 같이 명시적 인터페이스 멤버 구현을 사용하여 `IControl.Paint` 및 `IDataBound.Bind` 메서드를 구현할 수 있습니다.

```csharp
public class EditBox: IControl, IDataBound
{
    void IControl.Paint() {...}
    void IDataBound.Bind(Binder b) {...}
}
```
명시적 인터페이스 멤버는 인터페이스 형식을 통해서만 액세스할 수 있습니다. 구현의 예를 들어 `IControl.Paint` 이전 제공한 `EditBox` 클래스 에서만 사용 하 여 호출할 수는 `EditBox` 에 대 한 참조를 `IControl` 인터페이스 형식입니다.

```csharp
EditBox editBox = new EditBox();
editBox.Paint();                        // Error, no such method
IControl control = editBox;
control.Paint();                        // Ok
```

## <a name="enums"></a>열거형

***열거형 형식***은 명명된 상수 집합을 갖는 고유 값 형식입니다. 다음 예제에서는 선언 하 고 명명 된 열거형 형식을 사용 합니다. `Color` 세 개의 상수 값을 사용 하 여 `Red`를 `Green`, 및 `Blue`합니다.

```csharp
using System;

enum Color
{
    Red,
    Green,
    Blue
}

class Test
{
    static void PrintColor(Color color) {
        switch (color) {
            case Color.Red:
                Console.WriteLine("Red");
                break;
            case Color.Green:
                Console.WriteLine("Green");
                break;
            case Color.Blue:
                Console.WriteLine("Blue");
                break;
            default:
                Console.WriteLine("Unknown color");
                break;
        }
    }

    static void Main() {
        Color c = Color.Red;
        PrintColor(c);
        PrintColor(Color.Blue);
    }
}
```
각 열거형 형식이 정수 계열 형식이 호출에 ***내부 형식*** 열거형 형식입니다. 내부 형식을 명시적으로 선언 하지 않는 열거형 형식에 기본 형식 `int`합니다. 열거형 형식의 저장소 형식 및 가능한 값의 범위는 해당 기본 형식에 따라 결정 됩니다. 열거형 형식에 사용할 수 있는 값의 집합은은 열거형 멤버에 제한 되지 않습니다. 특히 열거형의 기본 형식의 모든 값은 열거형 형식으로 캐스팅 될 수 이며 해당 열거형의 유효한 고유 값.

다음 예제에서는 명명 된 열거형 형식을 선언 `Alignment` 기본 유형으로 `sbyte`입니다.

```csharp
enum Alignment: sbyte
{
    Left = -1,
    Center = 0,
    Right = 1
}
```
앞의 예제에서와 같이 열거형 멤버 선언에는 멤버의 값을 지정 하는 상수 식을 포함할 수 있습니다. 각 열거형 멤버에 대 한 상수 값을 열거형의 내부 형식 범위에 있어야 합니다. 열거형 멤버 선언 값을 명시적으로 지정 하지 않으면, 0 (열거형 형식에서 첫 번째 멤버 경우) 값 또는 텍스트가 앞에 있는 열거형 멤버는 1을 더한 값 멤버 지정 됩니다.

열거형 값을 정수로 변환 된 값과 반대로 캐스트를 사용 하 여 수 있습니다. 예

```csharp
int i = (int)Color.Blue;        // int i = 2;
Color c = (Color)2;             // Color c = Color.Blue;
```
모든 열거형 형식의 기본 값은 정수 계열 값 0은 열거형 형식으로 변환 합니다. 여기서 변수는 자동으로 기본값으로 초기화 하는 경우에서 열거형 형식의 변수를 지정 된 값입니다. 열거형 형식의 쉽게 사용할 수는 리터럴 기본값에 대 한 순서로 `0` 열거형 형식으로 암시적으로 변환 합니다. 따라서 다음이 허용됩니다.

```csharp
Color c = 0;
```

## <a name="delegates"></a>대리자

***대리자***는 특정 매개 변수 목록 및 반환 형식이 있는 메서드에 대한 참조를 나타내는 형식입니다. 대리자는 메서드를 변수에 할당되고 매개 변수로 전달될 수 있는 엔터티로 취급할 수 있도록 합니다. 또한 대리자는 다른 언어에 나오는 함수 포인터의 개념과 비슷하지만 함수 포인터와 달리 대리자는 개체 지향적이며 형식 안전 방식입니다.

다음 예제에서는 `Function`라는 대리자 형식을 선언하고 사용합니다.

```csharp
using System;

delegate double Function(double x);

class Multiplier
{
    double factor;

    public Multiplier(double factor) {
        this.factor = factor;
    }

    public double Multiply(double x) {
        return x * factor;
    }
}

class Test
{
    static double Square(double x) {
        return x * x;
    }

    static double[] Apply(double[] a, Function f) {
        double[] result = new double[a.Length];
        for (int i = 0; i < a.Length; i++) result[i] = f(a[i]);
        return result;
    }

    static void Main() {
        double[] a = {0.0, 0.5, 1.0};
        double[] squares = Apply(a, Square);
        double[] sines = Apply(a, Math.Sin);
        Multiplier m = new Multiplier(2.0);
        double[] doubles =  Apply(a, m.Multiply);
    }
}
```
`Function` 대리자 형식의 인스턴스는 `double` 인수를 사용하고 `double` 값을 반환하는 메서드를 참조할 수 있습니다. `Apply` 메서드가 적용 되는 지정 `Function` 의 요소에는 `double[]`을 반환을 `double[]` 결과 사용 하 여. `Main` 메서드에서 `Apply`는 세 가지 다른 함수를 `double[]`에 적용하는 데 사용됩니다.

대리자는 정적 메서드(예: 이전 예제의 `Square` 또는 `Math.Sin`) 또는 인스턴스 메서드(예: 이전 예제의 `m.Multiply`)를 참조할 수 있습니다. 인스턴스 메서드를 참조하는 대리자는 특정 개체도 참조하며, 인스턴스 메서드가 대리자를 통해 호출되는 경우 해당 개체도 이 호출에서 `this`가 됩니다.

또한 즉석에서 만들어지는 "인라인 메서드"인 익명 함수를 사용하여 대리자를 만들 수도 있습니다. 익명 함수는 주변 메서드의 지역 변수를 볼 수 있습니다. 따라서 위의 승수 예제 작성할 수 있습니다 보다 쉽게 사용 하지 않고는 `Multiplier` 클래스:

```csharp
double[] doubles =  Apply(a, (double x) => x * 2.0);
```
대리자의 흥미롭고 유용한 속성은 참조하는 메서드의 클래스를 알지 못하거나 관심을 두지 않는다는 것입니다. 참조되는 메서드가 대리자와 동일한 매개 변수 및 반환 형식을 갖는다는 것만 중요합니다.

## <a name="attributes"></a>특성

C# 프로그램의 형식, 멤버 및 기타 엔터티는 동작의 특정 측면을 제어하는 한정자를 지원합니다. 예를 들어 메서드의 액세스 가능성은 `public`, `protected`, `internal` 및 `private` 한정자를 사용하여 제어됩니다. C#은 선언적 정보의 사용자 정의 형식을 프로그램 엔터티에 연결하고 런타임에 검색할 수 있도록 이러한 기능을 일반화합니다. 프로그램은 ***특성***을 정의하고 사용하여 이러한 추가적인 선언적 정보를 지정합니다.

다음 예제에서는 관련 설명서에 대한 링크를 제공하기 위해 프로그램 엔터티에 배치될 수 있는 `HelpAttribute` 특성을 선언합니다.

```csharp
using System;

public class HelpAttribute: Attribute
{
    string url;
    string topic;

    public HelpAttribute(string url) {
        this.url = url;
    }

    public string Url {
        get { return url; }
    }

    public string Topic {
        get { return topic; }
        set { topic = value; }
    }
}
```
모든 특성 클래스에서 파생 된 `System.Attribute` 기본.NET Framework에서 제공 하는 클래스입니다. 연결된 선언 바로 앞에 대괄호로 묶은 특성 이름을 인수와 함께 적용할 수 있습니다. 특성의 이름이 끝나는 경우 `Attribute`, 특성 참조 될 때 이름의 해당 부분을 생략할 수 있습니다. 예를 들어 `HelpAttribute` 특성을 다음과 같이 사용할 수 있습니다.

```csharp
[Help("http://msdn.microsoft.com/.../MyClass.htm")]
public class Widget
{
    [Help("http://msdn.microsoft.com/.../MyClass.htm", Topic = "Display")]
    public void Display(string text) {}
}
```
이 예제에서는 연결을 `HelpAttribute` 에 `Widget` 클래스 및 다른 `HelpAttribute` 에 `Display` 클래스의 메서드. 특성 클래스의 공용 생성자는 프로그램 엔터티에 특성을 추가할 때 제공해야 하는 정보를 제어합니다. 특성 클래스의 공용 읽기/쓰기 속성을 참조하여 추가 정보를 제공할 수 있습니다(예: 앞에 나온 `Topic` 속성 참조).

다음 예제에서는 런타임에 특정된 응용 프로그램 엔터티에 대 한 특성 정보를 검색할 수 있는 방법을 보여 줍니다. 리플렉션을 사용 하 여 합니다.

```csharp
using System;
using System.Reflection;

class Test
{
    static void ShowHelp(MemberInfo member) {
        HelpAttribute a = Attribute.GetCustomAttribute(member,
            typeof(HelpAttribute)) as HelpAttribute;
        if (a == null) {
            Console.WriteLine("No help for {0}", member);
        }
        else {
            Console.WriteLine("Help for {0}:", member);
            Console.WriteLine("  Url={0}, Topic={1}", a.Url, a.Topic);
        }
    }

    static void Main() {
        ShowHelp(typeof(Widget));
        ShowHelp(typeof(Widget).GetMethod("Display"));
    }
}
```
리플렉션을 통해 특정 특성이 요청되면 특성 클래스에 대한 생성자가 프로그램 소스에 제공된 정보와 함께 호출되고 결과 특성 인스턴스가 반환됩니다. 속성을 통해 추가 정보를 제공한 경우 해당 속성은 특성 인스턴스가 반환되기 전에 지정된 값으로 설정됩니다.
