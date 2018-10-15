# <a name="exceptions"></a>예외

C#에서 예외 시스템 수준 및 응용 프로그램 수준 모두 처리는 구조적이 고 일정 하며 형식이 안전한 방식을 제공 오류 조건입니다. C#의 예외 메커니즘은 매우 비슷한 c + +, 몇 가지 중요 한 차이점을 사용 하 여:

*  C#에서 모든 예외에서 파생 된 클래스 형식의 인스턴스에 의해 표현 합니다 `System.Exception`합니다. C + +에서 예외를 나타내는 모든 형식의 모든 값을 사용할 수 있습니다.
*  C#의 경우에 finally 블록 ([try 문](statements.md#the-try-statement)) 일반 실행 및 예외 조건에서 실행 되는 종료 코드를 쓰는 데 사용할 수 있습니다. 이러한 코드는 c + + 코드를 복제 하지 않고 작성 하기가 어렵습니다.
*  C#에서는 시스템 수준 예외 오버플로, 0으로 나누기 및 null 역참조와 같은 예외 클래스 정의 되며 응용 프로그램 수준 오류 조건와 합니다.

## <a name="causes-of-exceptions"></a>예외의 원인

두 가지 방법으로 예외가 throw 될 수 있습니다.

*  A `throw` 문 ([throw 문을](statements.md#the-throw-statement)) 즉시 및 무조건 예외를 throw 합니다. 컨트롤에 도달 하지 않습니다. 문 바로 다음의 `throw`합니다.
*  통합 문서 작업을 정상적으로 완료 될 수 없는 C# 문 및 식 처리 중 발생 하는 특정 예외 조건을 특정 상황에서 예외가 발생 합니다. 예를 들어 정수 나누기 연산 ([나누기 연산자](expressions.md#division-operator))를 throw 한 `System.DivideByZeroException` 분모가 0 이면 합니다. 참조 [일반적인 예외 클래스](exceptions.md#common-exception-classes) 이 방식으로 발생할 수 있는 다양 한 예외 목록에 대 한 합니다.

## <a name="the-systemexception-class"></a>System.Exception 클래스

`System.Exception` 클래스는 모든 예외의 기본 형식입니다. 이 클래스에는 모든 예외를 공유 하는 몇 가지 중요 한 속성이 있습니다.

*  `Message` 형식의 읽기 전용 속성인 `string` 읽을 설명은 예외에 대 한 이유를 포함 하는 합니다.
*  `InnerException` 형식의 읽기 전용 속성인 `Exception`합니다. 현재 예외를 발생 시킨 예외를 참조 하는 해당 값이 null 이면-즉, 현재 예외를 catch 블록에서 발생 처리는 `InnerException`합니다. 그렇지 않으면 해당 값은 null,이 예외가 다른 예외 원인은 하지 나타냅니다. 이 방식으로 함께 연결 하는 예외 개체의 수는 임의의 수 있습니다.

인스턴스 생성자에 대 한 호출에서 이러한 속성의 값을 지정할 수 있습니다 `System.Exception`합니다.

## <a name="how-exceptions-are-handled"></a>예외 처리 방법

예외를 처리 한 `try` 문 ([try 문](statements.md#the-try-statement)).

시스템 검색에 대 한 예외가 발생 하는 경우 가장 가까운 `catch` 예외의 런타임 형식에 따른 예외를 처리할 수 있는 절. 첫째, 현재 메서드가 검색 하는 어휘 적으로 묶는 `try` 문과 try 문 관련된 catch 절의 순서로 간주 됩니다. 현재 메서드를 호출한 메서드는 어휘 적으로 묶는 검색할 실패할 경우 `try` 현재 메서드에 대 한 호출 지점을 포함 하는 문입니다. 이 검색 될 때까지 계속는 `catch` 예외 클래스는 같은 클래스 또는 런타임 throw 되는 예외 형식의 기본 클래스의 이름을 지정 하 여 현재 예외를 처리할 수 있는 절을 찾을 수 있습니다. `catch` 절 예외 클래스를 명명 하지 않는 모든 예외를 처리할 수 있습니다.

일치 하는 catch 절 발견 되 면 시스템 준비 catch 절의 첫 번째 문으로 제어를 전송 합니다. Catch 절은 실행이 시작 되기 전에 시스템을 처음 실행할를 순서 대로 `finally` 자세한 try 문과 사용 하 여 연결 된 절 중첩 예외를 포착 하는 것입니다.

일치 하는 catch 절이 없으면 두 가지 중 하나가 발생 합니다.

*  정적 생성자에 일치 하는 catch 절에 대 한 검색이 도달 하는 경우 ([정적 생성자](classes.md#static-constructors)) 또는 정적 필드 이니셜라이저는 `System.TypeInitializationException` 정적 생성자의 호출을 트리거한 지점에서 throw 됩니다. 내부 예외를 `System.TypeInitializationException` 원래 throw 된 예외를 포함 합니다.
*  Catch 절을 일치 하는 검색 스레드를 처음 시작 하는 코드에 도달 하면 스레드 실행이 종료 됩니다. 이런 종료가 미치는 구현 시 정의 됩니다.

소멸자가 실행 하는 동안 발생 하는 예외는 특별 한 언급이 합니다. 소멸자가 실행 하는 동안 예외가 발생 하는 경우 해당 예외 잡히지 않는 해당 소멸자가 실행 종료 되 고 (있는 경우) 기본 클래스의 소멸자가 호출 하는 것입니다. 기본 클래스가 없는 경우 (의 경우로 `object` 형식) 또는 기본 클래스 소멸자가 되지 않은 경우는 예외는 무시 합니다.

## <a name="common-exception-classes"></a>일반적인 예외 클래스

특정 C# 작업에 의해 다음과 같은 예외가 throw 됩니다.

|                                      |                |
|--------------------------------------|----------------|
| `System.ArithmeticException`         | `System.DivideByZeroException`, `System.OverflowException` 등의 산술 연산 중에 발생하는 예외에 대한 기본 클래스입니다. | 
| `System.ArrayTypeMismatchException`  | 저장소 배열에 저장 된 요소의 실제 형식이 배열의 실제 형식과 호환 되지 않으므로 실패 하는 경우 throw 됩니다. | 
| `System.DivideByZeroException`       | 정수 값을 0으로 나누려 할 때 발생 합니다. | 
| `System.IndexOutOfRangeException`    | 0 보다 작거나 배열의 경계 외부에 있는 인덱스를 통해 배열을 인덱싱하려 하려고 할 때 throw 됩니다. | 
| `System.InvalidCastException`        | 기본 형식 또는 인터페이스에서 파생된 형식으로 변환 하는 명시적 변환을 런타임에 실패 하는 경우 throw 됩니다. | 
| `System.NullReferenceException`      | 경우에 throw를 `null` 참조가 참조 된 개체를 필요로 하는 방식으로 사용 됩니다. | 
| `System.OutOfMemoryException`        | 메모리를 할당 하려고 할 때 throw 됩니다 (통해 `new`)에 실패 합니다. | 
| `System.OverflowException`           | `checked` 컨텍스트의 산술 연산이 오버플로될 경우 throw됩니다. | 
| `System.StackOverflowException`      | 보류 중인 메서드 호출이 너무 많아서; 실행 스택이 부족할 때 throw 너무 깊거나 재귀 일반적으로 의미 합니다. | 
| `System.TypeInitializationException` | 정적 생성자 없음 예외를 throw 하는 경우에 throw `catch` 절 catch 할 수 있습니다. | 
