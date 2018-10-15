# <a name="introduction"></a><span data-ttu-id="69639-101">소개</span><span class="sxs-lookup"><span data-stu-id="69639-101">Introduction</span></span>

<span data-ttu-id="69639-102">C#(“샵 참조”)은 간단하면서도 형식이 안전한 최신 개체 지향 프로그래밍 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-102">C# (pronounced "See Sharp") is a simple, modern, object-oriented, and type-safe programming language.</span></span> <span data-ttu-id="69639-103">C# C 언어 제품군에는 해당 루트 및 C, c + + 및 Java 프로그래머에 게 익숙한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-103">C# has its roots in the C family of languages and will be immediately familiar to C, C++, and Java programmers.</span></span> <span data-ttu-id="69639-104">C#으로 ECMA International로 표준화 되는 ***ECMA-334*** 표준 및 ISO/IEC로 여는 ***ISO/IEC 23270*** 표준.</span><span class="sxs-lookup"><span data-stu-id="69639-104">C# is standardized by ECMA International as the ***ECMA-334*** standard and by ISO/IEC as the ***ISO/IEC 23270*** standard.</span></span> <span data-ttu-id="69639-105">.NET Framework에 대 한 Microsoft의 C# 컴파일러는 이러한 두 표준은 표준에 맞는 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-105">Microsoft's C# compiler for the .NET Framework is a conforming implementation of both of these standards.</span></span>

<span data-ttu-id="69639-106">C#은 개체 지향 언어이지만 ***구성 요소 지향*** 프로그래밍도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-106">C# is an object-oriented language, but C# further includes support for ***component-oriented*** programming.</span></span> <span data-ttu-id="69639-107">현대의 소프트웨어 설계는 독립적이고 자체 설명적인 기능 패키지 형식을 갖는 소프트웨어 구성 요소에 점점 더 많이 의존하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-107">Contemporary software design increasingly relies on software components in the form of self-contained and self-describing packages of functionality.</span></span> <span data-ttu-id="69639-108">이러한 구성 요소의 핵심은 속성, 메서드 및 이벤트를 포함하는 프로그래밍 모델을 제공한다는 데 있습니다. 이러한 구성 요소는 구성 요소에 대한 선언적 정보를 제공하는 특성을 보유하며 자체 설명서를 통합하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-108">Key to such components is that they present a programming model with properties, methods, and events; they have attributes that provide declarative information about the component; and they incorporate their own documentation.</span></span> <span data-ttu-id="69639-109">C# 제공 직접 이러한 개념을 지 원하는 언어 구문을 만들어 소프트웨어 구성 요소를 사용 하는 뛰어난 자연 언어로 C# 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-109">C# provides language constructs to directly support these concepts, making C# a very natural language in which to create and use software components.</span></span>

<span data-ttu-id="69639-110">강력 하 고 안정적인 응용 프로그램 생성에 도움이 되는 여러 C# 기능: ***가비지 수집*** 사용 되지 않는 개체에서 사용한 메모리를 자동적으로 회수 ***예외 처리*** 오류 감지 및 복구를 구조화 하 고 확장 가능한 방법을 제공 하며 ***형식이 안전한*** 언어의 디자인을 사용 하면 초기화 되지 않은 읽을 불가능 변수, 해당 경계 초과 또는 확인 되지 않은 형식 캐스트를 수행 하려면 인덱스 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-110">Several C# features aid in the construction of robust and durable applications: ***Garbage collection*** automatically reclaims memory occupied by unused objects; ***exception handling*** provides a structured and extensible approach to error detection and recovery; and the ***type-safe*** design of the language makes it impossible to read from uninitialized variables, to index arrays beyond their bounds, or to perform unchecked type casts.</span></span>

<span data-ttu-id="69639-111">C#에는 ***통합 형식 시스템***이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-111">C# has a ***unified type system***.</span></span> <span data-ttu-id="69639-112">`int` 및 `double`과 같은 기본 형식을 포함하는 모든 C# 형식은 단일 루트 `object`에서 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-112">All C# types, including primitive types such as `int` and `double`, inherit from a single root `object` type.</span></span> <span data-ttu-id="69639-113">따라서 일반적인 작업 집합을 공유하는 모든 형식과 모든 형식의 값을 일관된 방식으로 저장 및 전송하고 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-113">Thus, all types share a set of common operations, and values of any type can be stored, transported, and operated upon in a consistent manner.</span></span> <span data-ttu-id="69639-114">그뿐 아니라 C#은 사용자 정의 참조 형식 및 값 형식을 모두 지원하여 개체의 동적 할당과 더불어 간단한 구조의 인라인 저장소도 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-114">Furthermore, C# supports both user-defined reference types and value types, allowing dynamic allocation of objects as well as in-line storage of lightweight structures.</span></span>

<span data-ttu-id="69639-115">C# 프로그램 및 라이브러리 수 시간이 지나면서 호환 되는 방식에서 되도록 강조한 것에 배치 된 ***버전 관리*** C#의 디자인 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-115">To ensure that C# programs and libraries can evolve over time in a compatible manner, much emphasis has been placed on ***versioning*** in C#'s design.</span></span> <span data-ttu-id="69639-116">다양한 프로그래밍 언어가 이 문제를 등한시하여 결과적으로 해당 언어로 작성된 프로그램이 최신 버전의 종속 라이브러리가 도입될 때 필요한 것보다 더 자주 중단되게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-116">Many programming languages pay little attention to this issue, and, as a result, programs written in those languages break more often than necessary when newer versions of dependent libraries are introduced.</span></span> <span data-ttu-id="69639-117">C# 설계의 측면 된 버전 관리 고려 사항 직접적인 영향을 포함할 별도 `virtual` 고 `override` 한정자, 메서드 오버 로드 확인에 대 한 규칙 및 명시적 인터페이스 멤버 선언에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="69639-117">Aspects of C#'s design that were directly influenced by versioning considerations include the separate `virtual` and `override` modifiers, the rules for method overload resolution, and support for explicit interface member declarations.</span></span>

<span data-ttu-id="69639-118">이 장의 나머지 C# 언어의 필수 기능을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-118">The rest of this chapter describes the essential features of the C# language.</span></span> <span data-ttu-id="69639-119">세부적인 및 경우에 따라 수학 방식으로 규칙 및 예외를 설명 하는 뒷부분에는 않지만이 장 명확 성과 떨어지더라도 간단한 설명을 위해 노력 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-119">Although later chapters describe rules and exceptions in a detail-oriented and sometimes mathematical manner, this chapter strives for clarity and brevity at the expense of completeness.</span></span> <span data-ttu-id="69639-120">초기 프로그램의 작성 및 뒷부분의 읽기를 원활 하 게 하는 언어에 대 한 소개를 제공 하기 위함입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-120">The intent is to provide the reader with an introduction to the language that will facilitate the writing of early programs and the reading of later chapters.</span></span>

## <a name="hello-world"></a><span data-ttu-id="69639-121">Hello World</span><span class="sxs-lookup"><span data-stu-id="69639-121">Hello world</span></span>

<span data-ttu-id="69639-122">“Hello, World” 프로그램은 프로그래밍 언어를 소개하는 데 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-122">The "Hello, World" program is traditionally used to introduce a programming language.</span></span> <span data-ttu-id="69639-123">C#에서는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-123">Here it is in C#:</span></span>

```csharp
using System;

class Hello
{
    static void Main() {
        Console.WriteLine("Hello, World");
    }
}
```

<span data-ttu-id="69639-124">C# 소스 파일은 일반적으로 파일 확장명이 `.cs`입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-124">C# source files typically have the file extension `.cs`.</span></span> <span data-ttu-id="69639-125">"Hello, World" 프로그램이 파일에 저장 된 가정 `hello.cs`, 명령줄을 사용 하 여 Microsoft C# 컴파일러를 사용 하 여 프로그램을 컴파일할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="69639-125">Assuming that the "Hello, World" program is stored in the file `hello.cs`, the program can be compiled with the Microsoft C# compiler using the command line</span></span>
```
csc hello.cs
```
<span data-ttu-id="69639-126">명명 된 실행 가능한 어셈블리를 생성 하는 `hello.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-126">which produces an executable assembly named `hello.exe`.</span></span> <span data-ttu-id="69639-127">실행 될 때이 응용 프로그램에서 생성 된 출력은</span><span class="sxs-lookup"><span data-stu-id="69639-127">The output produced by this application when it is run is</span></span>
```
Hello, World
```

<span data-ttu-id="69639-128">“Hello, World” 프로그램은 `System` 네임스페이스를 참조하는 `using` 지시문으로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-128">The "Hello, World" program starts with a `using` directive that references the `System` namespace.</span></span> <span data-ttu-id="69639-129">네임스페이스는 계층적으로 C# 프로그램 및 라이브러리를 구성하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-129">Namespaces provide a hierarchical means of organizing C# programs and libraries.</span></span> <span data-ttu-id="69639-130">네임스페이스에는 형식 및 다른 네임스페이스가 포함됩니다. 예를 들어 `System` 네임스페이스에는 많은 형식(예: 프로그램에 참조되는 `Console` 클래스) 및 많은 다른 네임스페이스(예: `IO` 및 `Collections`)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-130">Namespaces contain types and other namespaces—for example, the `System` namespace contains a number of types, such as the `Console` class referenced in the program, and a number of other namespaces, such as `IO` and `Collections`.</span></span> <span data-ttu-id="69639-131">지정된 네임스페이스를 참조하는 `using` 지시문을 사용하여 해당 네임스페이스의 멤버인 형식을 정규화되지 않은 방식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-131">A `using` directive that references a given namespace enables unqualified use of the types that are members of that namespace.</span></span> <span data-ttu-id="69639-132">`using` 지시문 때문에, 프로그램은 `Console.WriteLine`을 `System.Console.WriteLine`의 약식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-132">Because of the `using` directive, the program can use `Console.WriteLine` as shorthand for `System.Console.WriteLine`.</span></span>

<span data-ttu-id="69639-133">“Hello, World” 프로그램에서 선언된 `Hello` 클래스에는 단일 멤버인 `Main` 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-133">The `Hello` class declared by the "Hello, World" program has a single member, the method named `Main`.</span></span> <span data-ttu-id="69639-134">`Main` 사용 하 여 선언 된 메서드는 `static` 한정자.</span><span class="sxs-lookup"><span data-stu-id="69639-134">The `Main` method is declared with the `static` modifier.</span></span> <span data-ttu-id="69639-135">인스턴스 메서드는 키워드 `this`를 사용하여 특정 바깥쪽 개체 인스턴스를 참조할 수 있지만 정적 메서드는 특정 개체에 대한 참조 없이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-135">While instance methods can reference a particular enclosing object instance using the keyword `this`, static methods operate without reference to a particular object.</span></span> <span data-ttu-id="69639-136">관례상 `Main`이라는 정적 메서드가 프로그램의 진입점으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-136">By convention, a static method named `Main` serves as the entry point of a program.</span></span>

<span data-ttu-id="69639-137">프로그램의 출력은 `System` 네임스페이스에 있는 `Console` 클래스의 `WriteLine` 메서드에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-137">The output of the program is produced by the `WriteLine` method of the `Console` class in the `System` namespace.</span></span> <span data-ttu-id="69639-138">이 클래스는 기본적으로 자동으로 참조 하는 Microsoft C# 컴파일러는.NET Framework 클래스 라이브러리에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-138">This class is provided by the .NET Framework class libraries, which, by default, are automatically referenced by the Microsoft C# compiler.</span></span> <span data-ttu-id="69639-139">자체 C# 없는 별도 런타임 라이브러리를 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-139">Note that C# itself does not have a separate runtime library.</span></span> <span data-ttu-id="69639-140">대신,.NET Framework는 C#의 런타임 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-140">Instead, the .NET Framework is the runtime library of C#.</span></span>

## <a name="program-structure"></a><span data-ttu-id="69639-141">프로그램 구조</span><span class="sxs-lookup"><span data-stu-id="69639-141">Program structure</span></span>

<span data-ttu-id="69639-142">C#의 핵심적인 조직 개념은 ***프로그램***, ***네임스페이스***, ***형식***, ***멤버*** 및 ***어셈블리***입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-142">The key organizational concepts in C# are ***programs***, ***namespaces***, ***types***, ***members***, and ***assemblies***.</span></span> <span data-ttu-id="69639-143">C# 프로그램은 하나 이상의 소스 파일로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-143">C# programs consist of one or more source files.</span></span> <span data-ttu-id="69639-144">프로그램은 멤버를 포함하고 네임스페이스로 구성될 수 있는 형식을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-144">Programs declare types, which contain members and can be organized into namespaces.</span></span> <span data-ttu-id="69639-145">클래스와 인터페이스는 형식의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-145">Classes and interfaces are examples of types.</span></span> <span data-ttu-id="69639-146">필드, 메서드, 속성 및 이벤트는 멤버의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-146">Fields, methods, properties, and events are examples of members.</span></span> <span data-ttu-id="69639-147">C# 프로그램을 컴파일하면 실제로 어셈블리로 패키지됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-147">When C# programs are compiled, they are physically packaged into assemblies.</span></span> <span data-ttu-id="69639-148">어셈블리 일반적으로 파일 확장명이 `.exe` 또는 `.dll`구현 여부에 따라 ***응용 프로그램*** 하거나 ***라이브러리***합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-148">Assemblies typically have the file extension `.exe` or `.dll`, depending on whether they implement ***applications*** or ***libraries***.</span></span>

<span data-ttu-id="69639-149">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="69639-149">The example</span></span>

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
<span data-ttu-id="69639-150">이라는 클래스를 선언 `Stack` 라는 네임 스페이스에서 `Acme.Collections`합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-150">declares a class named `Stack` in a namespace called `Acme.Collections`.</span></span> <span data-ttu-id="69639-151">이 클래스의 정규화된 이름은 `Acme.Collections.Stack`입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-151">The fully qualified name of this class is `Acme.Collections.Stack`.</span></span> <span data-ttu-id="69639-152">클래스에는 필드 `top`, 2개의 메서드 `Push` 및 `Pop`, 중첩된 클래스 `Entry` 등의 여러 멤버가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-152">The class contains several members: a field named `top`, two methods named `Push` and `Pop`, and a nested class named `Entry`.</span></span> <span data-ttu-id="69639-153">`Entry` 클래스는 필드 `next` 및 필드 `data`, 생성자의 세 멤버가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-153">The `Entry` class further contains three members: a field named `next`, a field named `data`, and a constructor.</span></span> <span data-ttu-id="69639-154">예제의 소스 코드가 파일 `acme.cs`에 포함된다고 가정할 경우 다음 명령줄은</span><span class="sxs-lookup"><span data-stu-id="69639-154">Assuming that the source code of the example is stored in the file `acme.cs`, the command line</span></span>

```
csc /t:library acme.cs
```
<span data-ttu-id="69639-155">예제를 라이브러리(`Main` 진입점이 없는 코드)를 컴파일하고 `acme.dll`이라는 어셈블리를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-155">compiles the example as a library (code without a `Main` entry point) and produces an assembly named `acme.dll`.</span></span>

<span data-ttu-id="69639-156">어셈블리의 형태로 실행 코드를 포함할 ***Intermediate Language*** 형태로 기호화 된 정보와 (IL) 명령 ***메타 데이터***입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-156">Assemblies contain executable code in the form of ***Intermediate Language*** (IL) instructions, and symbolic information in the form of ***metadata***.</span></span> <span data-ttu-id="69639-157">실행되기 전에 어셈블리의 IL 코드는 .NET 공용 언어 런타임의 JIT(Just-In-Time) 컴파일러에 의해 자동으로 프로세서 특정 코드로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-157">Before it is executed, the IL code in an assembly is automatically converted to processor-specific code by the Just-In-Time (JIT) compiler of .NET Common Language Runtime.</span></span>

<span data-ttu-id="69639-158">어셈블리는 코드와 메타데이터를 모두 포함하는 기능의 자체 설명 단위이므로 C#에 `#include` 지시문 및 헤더 파일이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-158">Because an assembly is a self-describing unit of functionality containing both code and metadata, there is no need for `#include` directives and header files in C#.</span></span> <span data-ttu-id="69639-159">특정 어셈블리에 포함된 공용 형식 및 멤버는 프로그램을 컴파일할 때 해당 어셈블리를 참조하는 것만으로 C# 프로그램에서 사용 가능해집니다.</span><span class="sxs-lookup"><span data-stu-id="69639-159">The public types and members contained in a particular assembly are made available in a C# program simply by referencing that assembly when compiling the program.</span></span> <span data-ttu-id="69639-160">예를 들어 이 프로그램에서는 `acme.dll` 어셈블리의 `Acme.Collections.Stack` 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-160">For example, this program uses the `Acme.Collections.Stack` class from the `acme.dll` assembly:</span></span>

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
<span data-ttu-id="69639-161">프로그램 파일에 저장 되는 경우 `test.cs`때 `test.cs` 컴파일되면 합니다 `acme.dll` 컴파일러의를 사용 하 여 어셈블리를 참조할 수 있습니다 `/r` 옵션:</span><span class="sxs-lookup"><span data-stu-id="69639-161">If the program is stored in the file `test.cs`, when `test.cs` is compiled, the `acme.dll` assembly can be referenced using the compiler's `/r` option:</span></span>

```
csc /r:acme.dll test.cs
```
<span data-ttu-id="69639-162">이를 통해 실행 시 출력을 생성하는 `test.exe`라는 실행 가능한 어셈블리가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="69639-162">This creates an executable assembly named `test.exe`, which, when run, produces the output:</span></span>

```
100
10
1
```
<span data-ttu-id="69639-163">C#은 프로그램의 소스 텍스트가 여러 소스 파일에 저장되도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-163">C# permits the source text of a program to be stored in several source files.</span></span> <span data-ttu-id="69639-164">다중 파일 C# 프로그램이 컴파일되면 모든 소스 파일이 함께 처리되고 소스 파일은 서로 자유롭게 참조될 수 있습니다. 개념적으로는 마치 모든 소스 파일이 처리되기 전에 하나의 큰 파일로 연결되는 것처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-164">When a multi-file C# program is compiled, all of the source files are processed together, and the source files can freely reference each other—conceptually, it is as if all the source files were concatenated into one large file before being processed.</span></span> <span data-ttu-id="69639-165">극소수의 경우를 제외하고 선언 순서는 중요하지 않으므로 C#에서는 정방향 선언이 절대 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-165">Forward declarations are never needed in C# because, with very few exceptions, declaration order is insignificant.</span></span> <span data-ttu-id="69639-166">C#은 소스 파일을 하나의 공용 형식만 선언하도록 제한하거나 소스 파일 이름이 소스 파일에 선언된 형식과 일치하도록 요구하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-166">C# does not limit a source file to declaring only one public type nor does it require the name of the source file to match a type declared in the source file.</span></span>

## <a name="types-and-variables"></a><span data-ttu-id="69639-167">형식 및 변수</span><span class="sxs-lookup"><span data-stu-id="69639-167">Types and variables</span></span>

<span data-ttu-id="69639-168">C#에는 두 가지 종류의 형식, 즉 ***값 형식***과 ***참조 형식***이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-168">There are two kinds of types in C#: ***value types*** and ***reference types***.</span></span> <span data-ttu-id="69639-169">값 형식의 변수에는 해당 데이터가 직접 포함되지만 참조 형식의 변수에는 데이터(개체라고도 함)에 대한 참조가 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-169">Variables of value types directly contain their data whereas variables of reference types store references to their data, the latter being known as objects.</span></span> <span data-ttu-id="69639-170">참조 형식에서는 두 가지 변수가 같은 개체를 참조할 수 있으므로 한 변수에 대한 작업이 다른 변수에서 참조하는 개체에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-170">With reference types, it is possible for two variables to reference the same object and thus possible for operations on one variable to affect the object referenced by the other variable.</span></span> <span data-ttu-id="69639-171">값 형식에서는 변수에 데이터의 자체 사본이 들어 있으며 한 변수의 작업이 다른 변수에 영향을 미칠 수 없습니다(`ref` 및 `out` ref 및 out 매개 변수 제외).</span><span class="sxs-lookup"><span data-stu-id="69639-171">With value types, the variables each have their own copy of the data, and it is not possible for operations on one to affect the other (except in the case of `ref` and `out` parameter variables).</span></span>

<span data-ttu-id="69639-172">C#의 값 형식으로 세분화 됩니다 ***단순 형식***, ***열거형***를 ***구조체 형식은***, 및 ***nullable 형식***, 및 C# 참조 형식으로 세분화 됩니다 ***클래스 형식은***, ***인터페이스 형식***합니다 ***배열 형식***, 및 ***대리자 형식***합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-172">C#'s value types are further divided into ***simple types***, ***enum types***, ***struct types***, and ***nullable types***, and C#'s reference types are further divided into ***class types***, ***interface types***, ***array types***, and ***delegate types***.</span></span>

<span data-ttu-id="69639-173">다음 표에서 C#의 형식 시스템의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-173">The following table provides an overview of C#'s type system.</span></span>

| <span data-ttu-id="69639-174">__범주__</span><span class="sxs-lookup"><span data-stu-id="69639-174">__Category__</span></span>    |                 | <span data-ttu-id="69639-175">__설명__</span><span class="sxs-lookup"><span data-stu-id="69639-175">__Description__</span></span> |
|-----------------|-----------------|-----------------|
| <span data-ttu-id="69639-176">값 형식</span><span class="sxs-lookup"><span data-stu-id="69639-176">Value types</span></span>     | <span data-ttu-id="69639-177">단순 형식</span><span class="sxs-lookup"><span data-stu-id="69639-177">Simple types</span></span>    | <span data-ttu-id="69639-178">부호 있는 정수: `sbyte`, `short`, `int`,`long`</span><span class="sxs-lookup"><span data-stu-id="69639-178">Signed integral: `sbyte`, `short`, `int`, `long`</span></span> |
|                 |                 | <span data-ttu-id="69639-179">부호 없는 정수: `byte`, `ushort`, `uint`,`ulong`</span><span class="sxs-lookup"><span data-stu-id="69639-179">Unsigned integral: `byte`, `ushort`, `uint`, `ulong`</span></span> |
|                 |                 | <span data-ttu-id="69639-180">유니코드 문자: `char`</span><span class="sxs-lookup"><span data-stu-id="69639-180">Unicode characters: `char`</span></span> |
|                 |                 | <span data-ttu-id="69639-181">IEEE 부동 소수점: `float`, `double`</span><span class="sxs-lookup"><span data-stu-id="69639-181">IEEE floating point: `float`, `double`</span></span> |
|                 |                 | <span data-ttu-id="69639-182">High-Precision 10진수:`decimal`</span><span class="sxs-lookup"><span data-stu-id="69639-182">High-precision decimal: `decimal`</span></span> |
|                 |                 | <span data-ttu-id="69639-183">부울: `bool`</span><span class="sxs-lookup"><span data-stu-id="69639-183">Boolean: `bool`</span></span> |
|                 | <span data-ttu-id="69639-184">열거형</span><span class="sxs-lookup"><span data-stu-id="69639-184">Enum types</span></span>      | <span data-ttu-id="69639-185">`enum E {...}` 양식의 사용자 정의 형식</span><span class="sxs-lookup"><span data-stu-id="69639-185">User-defined types of the form `enum E {...}`</span></span> |
|                 | <span data-ttu-id="69639-186">구조체 형식</span><span class="sxs-lookup"><span data-stu-id="69639-186">Struct types</span></span>    | <span data-ttu-id="69639-187">`struct S {...}` 양식의 사용자 정의 형식</span><span class="sxs-lookup"><span data-stu-id="69639-187">User-defined types of the form `struct S {...}`</span></span> |
|                 | <span data-ttu-id="69639-188">Nullable 형식</span><span class="sxs-lookup"><span data-stu-id="69639-188">Nullable types</span></span>  | <span data-ttu-id="69639-189">`null` 값을 갖는 다른 모든 값 형식의 확장</span><span class="sxs-lookup"><span data-stu-id="69639-189">Extensions of all other value types with a `null` value</span></span> |
| <span data-ttu-id="69639-190">참조 형식</span><span class="sxs-lookup"><span data-stu-id="69639-190">Reference types</span></span> | <span data-ttu-id="69639-191">클래스 형식</span><span class="sxs-lookup"><span data-stu-id="69639-191">Class types</span></span>     | <span data-ttu-id="69639-192">다른 모든 형식의 기본 클래스: `object`</span><span class="sxs-lookup"><span data-stu-id="69639-192">Ultimate base class of all other types: `object`</span></span> |
|                 |                 | <span data-ttu-id="69639-193">유니코드 문자열: `string`</span><span class="sxs-lookup"><span data-stu-id="69639-193">Unicode strings: `string`</span></span> |
|                 |                 | <span data-ttu-id="69639-194">`class C {...}` 양식의 사용자 정의 형식</span><span class="sxs-lookup"><span data-stu-id="69639-194">User-defined types of the form `class C {...}`</span></span> |
|                 | <span data-ttu-id="69639-195">인터페이스 형식</span><span class="sxs-lookup"><span data-stu-id="69639-195">Interface types</span></span> | <span data-ttu-id="69639-196">`interface I {...}` 양식의 사용자 정의 형식</span><span class="sxs-lookup"><span data-stu-id="69639-196">User-defined types of the form `interface I {...}`</span></span> |
|                 | <span data-ttu-id="69639-197">배열 형식</span><span class="sxs-lookup"><span data-stu-id="69639-197">Array types</span></span>     | <span data-ttu-id="69639-198">단일 차원 및 다차원(예: `int[]` 및`int[,]`)</span><span class="sxs-lookup"><span data-stu-id="69639-198">Single- and multi-dimensional, for example, `int[]` and `int[,]`</span></span> |
|                 | <span data-ttu-id="69639-199">대리자 형식</span><span class="sxs-lookup"><span data-stu-id="69639-199">Delegate types</span></span>  | <span data-ttu-id="69639-200">폼의 사용자 정의 형식 예: `delegate int  D(...)`</span><span class="sxs-lookup"><span data-stu-id="69639-200">User-defined types of the form e.g. `delegate int  D(...)`</span></span> |

<span data-ttu-id="69639-201">8가지 정수 형식은 부호 있는 형식 또는 부호 없는 형식으로 8비트, 16비트, 32비트 및 64비트 값에 대한 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-201">The eight integral types provide support for 8-bit, 16-bit, 32-bit, and 64-bit values in signed or unsigned form.</span></span>

<span data-ttu-id="69639-202">두 부동 소수점 형식, `float` 고 `double`, 32 비트 단 정밀도 및 64 비트 배정밀도 IEEE 754 형식을 사용 하 여 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-202">The two floating point types, `float` and `double`, are represented using the 32-bit single-precision and 64-bit double-precision IEEE 754 formats.</span></span>

<span data-ttu-id="69639-203">`decimal` 형식은 재무 및 통화 계산에 적합한 128비트 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-203">The `decimal` type is a 128-bit data type suitable for financial and monetary calculations.</span></span>

<span data-ttu-id="69639-204">C# `bool` 형식을 부울 값을 나타내는 데 사용 됩니다-인 값 `true` 또는 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-204">C#'s `bool` type is used to represent boolean values—values that are either `true` or `false`.</span></span>

<span data-ttu-id="69639-205">C#의 문자 및 문자열 처리에서는 유니코드 인코딩이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-205">Character and string processing in C# uses Unicode encoding.</span></span> <span data-ttu-id="69639-206">`char` 형식은 UTF-16 코드 단위를 나타내고, `string` 형식은 UTF-16 코드 단위 시퀀스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="69639-206">The `char` type represents a UTF-16 code unit, and the `string` type represents a sequence of UTF-16 code units.</span></span>

<span data-ttu-id="69639-207">다음 표에서 C#의 숫자 형식이 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-207">The following table summarizes C#'s numeric types.</span></span>


| <span data-ttu-id="69639-208">__범주__</span><span class="sxs-lookup"><span data-stu-id="69639-208">__Category__</span></span>      | <span data-ttu-id="69639-209">__비트__</span><span class="sxs-lookup"><span data-stu-id="69639-209">__Bits__</span></span> | <span data-ttu-id="69639-210">__Type__</span><span class="sxs-lookup"><span data-stu-id="69639-210">__Type__</span></span>  | <span data-ttu-id="69639-211">__범위/자릿수__</span><span class="sxs-lookup"><span data-stu-id="69639-211">__Range/Precision__</span></span> |
|-------------------|----------|-----------|---------------------|
| <span data-ttu-id="69639-212">부호 있는 정수</span><span class="sxs-lookup"><span data-stu-id="69639-212">Signed integral</span></span>   | <span data-ttu-id="69639-213">8</span><span class="sxs-lookup"><span data-stu-id="69639-213">8</span></span>        | `sbyte`   | <span data-ttu-id="69639-214">...-128에서 127</span><span class="sxs-lookup"><span data-stu-id="69639-214">-128...127</span></span> |
|                   | <span data-ttu-id="69639-215">16</span><span class="sxs-lookup"><span data-stu-id="69639-215">16</span></span>       | `short`   | <span data-ttu-id="69639-216">-32, 768... 32, 767</span><span class="sxs-lookup"><span data-stu-id="69639-216">-32,768...32,767</span></span> |
|                   | <span data-ttu-id="69639-217">32</span><span class="sxs-lookup"><span data-stu-id="69639-217">32</span></span>       | `int`     | <span data-ttu-id="69639-218">-2,147,483, 648... 2, 147, 483, 647</span><span class="sxs-lookup"><span data-stu-id="69639-218">-2,147,483,648...2,147,483,647</span></span> |
|                   | <span data-ttu-id="69639-219">64</span><span class="sxs-lookup"><span data-stu-id="69639-219">64</span></span>       | `long`    | <span data-ttu-id="69639-220">-9,223,372,036,854,775, 808... 9, 223, 372, 036, 854, 775, 807</span><span class="sxs-lookup"><span data-stu-id="69639-220">-9,223,372,036,854,775,808...9,223,372,036,854,775,807</span></span> |
| <span data-ttu-id="69639-221">부호 없는 정수</span><span class="sxs-lookup"><span data-stu-id="69639-221">Unsigned integral</span></span> | <span data-ttu-id="69639-222">8</span><span class="sxs-lookup"><span data-stu-id="69639-222">8</span></span>        | `byte`    | <span data-ttu-id="69639-223">0... 255</span><span class="sxs-lookup"><span data-stu-id="69639-223">0...255</span></span> |
|                   | <span data-ttu-id="69639-224">16</span><span class="sxs-lookup"><span data-stu-id="69639-224">16</span></span>       | `ushort`  | <span data-ttu-id="69639-225">0... 65,535</span><span class="sxs-lookup"><span data-stu-id="69639-225">0...65,535</span></span> |
|                   | <span data-ttu-id="69639-226">32</span><span class="sxs-lookup"><span data-stu-id="69639-226">32</span></span>       | `uint`    | <span data-ttu-id="69639-227">0... 4294967295</span><span class="sxs-lookup"><span data-stu-id="69639-227">0...4,294,967,295</span></span> |
|                   | <span data-ttu-id="69639-228">64</span><span class="sxs-lookup"><span data-stu-id="69639-228">64</span></span>       | `ulong`   | <span data-ttu-id="69639-229">0... 18446744073709551615</span><span class="sxs-lookup"><span data-stu-id="69639-229">0...18,446,744,073,709,551,615</span></span> |
| <span data-ttu-id="69639-230">부동 소수점</span><span class="sxs-lookup"><span data-stu-id="69639-230">Floating point</span></span>    | <span data-ttu-id="69639-231">32</span><span class="sxs-lookup"><span data-stu-id="69639-231">32</span></span>       | `float`   | <span data-ttu-id="69639-232">1.5 × 10 ^ − 45 3.4 × 10 ^38, 전체 자릿수 7 자리</span><span class="sxs-lookup"><span data-stu-id="69639-232">1.5 × 10^−45 to 3.4 × 10^38, 7-digit precision</span></span> |
|                   | <span data-ttu-id="69639-233">64</span><span class="sxs-lookup"><span data-stu-id="69639-233">64</span></span>       | `double`  | <span data-ttu-id="69639-234">5.0 × 10 ^324 1.7 × 10 ^308, 전체 자릿수 15 자리</span><span class="sxs-lookup"><span data-stu-id="69639-234">5.0 × 10^−324 to 1.7 × 10^308, 15-digit precision</span></span> |
| <span data-ttu-id="69639-235">Decimal</span><span class="sxs-lookup"><span data-stu-id="69639-235">Decimal</span></span>           | <span data-ttu-id="69639-236">128</span><span class="sxs-lookup"><span data-stu-id="69639-236">128</span></span>      | `decimal` | <span data-ttu-id="69639-237">1.0 × 10 ^ −28 7.9 × 10 ^28, 28 자리 전체 자릿수</span><span class="sxs-lookup"><span data-stu-id="69639-237">1.0 × 10^−28 to 7.9 × 10^28, 28-digit precision</span></span> |

<span data-ttu-id="69639-238">C# 프로그램에서는 ***형식 선언***을 사용하여 새 형식을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69639-238">C# programs use ***type declarations*** to create new types.</span></span> <span data-ttu-id="69639-239">형식 선언은 새 형식의 이름과 멤버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-239">A type declaration specifies the name and the members of the new type.</span></span> <span data-ttu-id="69639-240">사용자 정의 가능한 형식의 C#의 범주 5: 형식, 구조체 형식, 인터페이스 형식, 열거형, 클래스 및 대리자 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-240">Five of C#'s categories of types are user-definable: class types, struct types, interface types, enum types, and delegate types.</span></span>

<span data-ttu-id="69639-241">클래스 형식의 데이터 멤버 (필드) 및 함수 멤버 (메서드, 속성 및 다른 사용자)을 포함 하는 데이터 구조를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-241">A class type defines a data structure that contains data members (fields) and function members (methods, properties, and others).</span></span> <span data-ttu-id="69639-242">클래스 형식은 단일 상속 및 다형성과 파생된 클래스가 기본 클래스를 확장하고 특수화할 수 있는 메커니즘을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-242">Class types support single inheritance and polymorphism, mechanisms whereby derived classes can extend and specialize base classes.</span></span>

<span data-ttu-id="69639-243">구조체 형식을 나타내는 데이터 멤버 및 함수 멤버를 사용 하 여 구조체 클래스 형식와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-243">A struct type is similar to a class type in that it represents a structure with data members and function members.</span></span> <span data-ttu-id="69639-244">그러나 클래스와 달리 구조체 값 형식이 며 힙 할당이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-244">However, unlike classes, structs are value types and do not require heap allocation.</span></span> <span data-ttu-id="69639-245">구조체 형식은 사용자 지정 상속을 지원하지 않으며 모든 구조체 형식은 `object` 형식에서 암시적으로 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-245">Struct types do not support user-specified inheritance, and all struct types implicitly inherit from type `object`.</span></span>

<span data-ttu-id="69639-246">공용 함수 멤버의 명명된 된 집합으로 계약을 정의 하는 인터페이스 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-246">An interface type defines a contract as a named set of public function members.</span></span> <span data-ttu-id="69639-247">클래스 또는 구조체는 인터페이스를 구현 하는 인터페이스의 함수 멤버의 구현을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-247">A class or struct that implements an interface must provide implementations of the interface's function members.</span></span> <span data-ttu-id="69639-248">여러 기본 인터페이스에서 상속할 수 및 클래스 또는 구조체는 여러 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-248">An interface may inherit from multiple base interfaces, and a class or struct may implement multiple interfaces.</span></span>

<span data-ttu-id="69639-249">대리자 형식이 특정 매개 변수 목록 및 반환 형식을 사용 하 여 메서드에 대 한 참조를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="69639-249">A delegate type represents references to methods with a particular parameter list and return type.</span></span> <span data-ttu-id="69639-250">대리자는 메서드를 변수에 할당되고 매개 변수로 전달될 수 있는 엔터티로 취급할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-250">Delegates make it possible to treat methods as entities that can be assigned to variables and passed as parameters.</span></span> <span data-ttu-id="69639-251">또한 대리자는 다른 언어에 나오는 함수 포인터의 개념과 비슷하지만 함수 포인터와 달리 대리자는 개체 지향적이며 형식 안전 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-251">Delegates are similar to the concept of function pointers found in some other languages, but unlike function pointers, delegates are object-oriented and type-safe.</span></span>

<span data-ttu-id="69639-252">클래스, 구조체, 인터페이스 및 대리자 형식 모두 제네릭을 지원 하므로 수 수 매개 변수화 다른 형식을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-252">Class, struct, interface and delegate types all support generics, whereby they can be parameterized with other types.</span></span>

<span data-ttu-id="69639-253">명명 된 상수를 사용 하 여 고유 형식인 열거형 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-253">An enum type is a distinct type with named constants.</span></span> <span data-ttu-id="69639-254">모든 열거형 형식을는 기본 형식, 8 가지 정수 형식 중 하나 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-254">Every enum type has an underlying type, which must be one of the eight integral types.</span></span> <span data-ttu-id="69639-255">열거형 형식의 값 집합이 기본 형식의 값 집합과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-255">The set of values of an enum type is the same as the set of values of the underlying type.</span></span>

<span data-ttu-id="69639-256">C#은 형식의 단일 차원 및 다차원 배열을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-256">C# supports single- and multi-dimensional arrays of any type.</span></span> <span data-ttu-id="69639-257">위에 나열된 형식과 달리, 배열 형식은 사용하기 전에 먼저 선언할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-257">Unlike the types listed above, array types do not have to be declared before they can be used.</span></span> <span data-ttu-id="69639-258">대신, 배열 형식은 형식 이름을 대괄호로 묶어 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-258">Instead, array types are constructed by following a type name with square brackets.</span></span> <span data-ttu-id="69639-259">예를 들어 `int[]` 의 1 차원 배열입니다 `int`, `int[,]` 의 2 차원 배열입니다 `int`, 및 `int[][]` 는 1 차원 배열의 1 차원 배열 `int`합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-259">For example, `int[]` is a single-dimensional array of `int`, `int[,]` is a two-dimensional array of `int`, and `int[][]` is a single-dimensional array of single-dimensional arrays of `int`.</span></span>

<span data-ttu-id="69639-260">Nullable 형식은 또한 사용할 수 있으려면 먼저 선언할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-260">Nullable types also do not have to be declared before they can be used.</span></span> <span data-ttu-id="69639-261">각 nullable이 아닌 값 형식에 대 한 `T` 해당 nullable 형식이 `T?`에 추가 값을 포함할 수 있는 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-261">For each non-nullable value type `T` there is a corresponding nullable type `T?`, which can hold an additional value `null`.</span></span> <span data-ttu-id="69639-262">예를 들어 `int?` 32 비트 정수 또는 값을 보유할 수 있는 형식인 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-262">For instance, `int?` is a type that can hold any 32 bit integer or the value `null`.</span></span>

<span data-ttu-id="69639-263">C#의 형식 시스템은 모든 형식의 값 개체로 처리할 수 있도록 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-263">C#'s type system is unified such that a value of any type can be treated as an object.</span></span> <span data-ttu-id="69639-264">C#의 모든 형식은 `object` 클래스 형식에서 직접 또는 간접적으로 파생되고 `object`는 모든 형식의 기본 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-264">Every type in C# directly or indirectly derives from the `object` class type, and `object` is the ultimate base class of all types.</span></span> <span data-ttu-id="69639-265">참조 형식의 값은 `object`로 인식함으로써 간단히 개체로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-265">Values of reference types are treated as objects simply by viewing the values as type `object`.</span></span> <span data-ttu-id="69639-266">값 형식의 값은 수행 하 여 개체로 처리 됩니다 ***boxing*** 하 고 ***unboxing*** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-266">Values of value types are treated as objects by performing ***boxing*** and ***unboxing*** operations.</span></span> <span data-ttu-id="69639-267">다음 예제에서 `int` 값은 `object`로 변환되었다가 다시 `int`로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-267">In the following example, an `int` value is converted to `object` and back again to `int`.</span></span>

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
<span data-ttu-id="69639-268">값 형식이 값 형식으로 변환 되 면 `object`"box" 라고도 하는 개체 인스턴스 값을 보유할 할당 되 고 값이 해당 box에 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-268">When a value of a value type is converted to type `object`, an object instance, also called a "box," is allocated to hold the value, and the value is copied into that box.</span></span> <span data-ttu-id="69639-269">반대로,는 `object` 참조 값 형식으로 캐스팅 됩니다, 올바른 값 형식의 상자는 참조 된 개체는 검사가 수행 됩니다 및 검사에 성공 하면 상자에 값이 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-269">Conversely, when an `object` reference is cast to a value type, a check is made that the referenced object is a box of the correct value type, and, if the check succeeds, the value in the box is copied out.</span></span>

<span data-ttu-id="69639-270">C# 통합된 형식 시스템을 효과적으로 값 형식이 요청 합니다."시" 개체가 될 수는 의미</span><span class="sxs-lookup"><span data-stu-id="69639-270">C#'s unified type system effectively means that value types can become objects "on demand."</span></span> <span data-ttu-id="69639-271">통합 때문에 `object` 형식을 사용하는 범용 라이브러리는 참조 형식 및 값 형식 둘 다에 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-271">Because of the unification, general-purpose libraries that use type `object` can be used with both reference types and value types.</span></span>

<span data-ttu-id="69639-272">C#에는 필드, 배열 요소, 지역 변수 및 매개 변수를 포함하는 여러 종류의 ***변수***가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-272">There are several kinds of ***variables*** in C#, including fields, array elements, local variables, and parameters.</span></span> <span data-ttu-id="69639-273">변수는 저장소 위치를 나타내고 수 있는 값을 결정 하는 형식이 모든 변수에 다음 표에 표시 된 것과 같이 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-273">Variables represent storage locations, and every variable has a type that determines what values can be stored in the variable, as shown by the following table.</span></span>


| <span data-ttu-id="69639-274">__변수 형식__</span><span class="sxs-lookup"><span data-stu-id="69639-274">__Type of Variable__</span></span>    | <span data-ttu-id="69639-275">__가능한 콘텐츠__</span><span class="sxs-lookup"><span data-stu-id="69639-275">__Possible Contents__</span></span> |
|-------------------------|-----------------------|
| <span data-ttu-id="69639-276">Null을 허용하지 않는 값 형식</span><span class="sxs-lookup"><span data-stu-id="69639-276">Non-nullable value type</span></span> | <span data-ttu-id="69639-277">정확한 해당 형식의 값</span><span class="sxs-lookup"><span data-stu-id="69639-277">A value of that exact type</span></span> |
| <span data-ttu-id="69639-278">Null 허용 값 형식</span><span class="sxs-lookup"><span data-stu-id="69639-278">Nullable value type</span></span>     | <span data-ttu-id="69639-279">Null 값 또는 정확한 해당 형식의 값</span><span class="sxs-lookup"><span data-stu-id="69639-279">A null value or a value of that exact type</span></span> |
| `object`                | <span data-ttu-id="69639-280">Null 참조, 참조 형식의 개체에 대 한 참조 또는 값 형식의 boxed 값에 대 한 참조</span><span class="sxs-lookup"><span data-stu-id="69639-280">A null reference, a reference to an object of any reference type, or a reference to a boxed value of any value type</span></span> |
| <span data-ttu-id="69639-281">클래스 형식</span><span class="sxs-lookup"><span data-stu-id="69639-281">Class type</span></span>              | <span data-ttu-id="69639-282">해당 클래스 형식에서 파생 된 클래스의 인스턴스에 대 한 참조를 null 참조, 해당 클래스 형식의 인스턴스에 대 한 참조</span><span class="sxs-lookup"><span data-stu-id="69639-282">A null reference, a reference to an instance of that class type, or a reference to an instance of a class derived from that class type</span></span> |
| <span data-ttu-id="69639-283">인터페이스 유형</span><span class="sxs-lookup"><span data-stu-id="69639-283">Interface type</span></span>          | <span data-ttu-id="69639-284">Null 참조, 해당 인터페이스 형식을 구현 하는 클래스 형식의 인스턴스에 대 한 참조 또는 해당 인터페이스 형식을 구현 하는 값 형식의 boxed 값에 대 한 참조</span><span class="sxs-lookup"><span data-stu-id="69639-284">A null reference, a reference to an instance of a class type that implements that interface type, or a reference to a boxed value of a value type that implements that interface type</span></span> |
| <span data-ttu-id="69639-285">배열 형식</span><span class="sxs-lookup"><span data-stu-id="69639-285">Array type</span></span>              | <span data-ttu-id="69639-286">Null 참조, 해당 배열 형식의 인스턴스에 대 한 참조 또는 호환 되는 배열 형식의 인스턴스에 대 한 참조</span><span class="sxs-lookup"><span data-stu-id="69639-286">A null reference, a reference to an instance of that array type, or a reference to an instance of a compatible array type</span></span> |
| <span data-ttu-id="69639-287">대리자 형식</span><span class="sxs-lookup"><span data-stu-id="69639-287">Delegate type</span></span>           | <span data-ttu-id="69639-288">Null 참조 또는 해당 대리자 형식의 인스턴스에 대 한 참조</span><span class="sxs-lookup"><span data-stu-id="69639-288">A null reference or a reference to an instance of that delegate type</span></span> |

## <a name="expressions"></a><span data-ttu-id="69639-289">식</span><span class="sxs-lookup"><span data-stu-id="69639-289">Expressions</span></span>

<span data-ttu-id="69639-290">***식***은 ***피연산자*** 및 ***연산자***로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-290">***Expressions*** are constructed from ***operands*** and ***operators***.</span></span> <span data-ttu-id="69639-291">식의 연산자는 피연산자에 적용할 연산을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="69639-291">The operators of an expression indicate which operations to apply to the operands.</span></span> <span data-ttu-id="69639-292">연산자의 예로 `+`, `-`, `*`, `/` 및 `new`가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-292">Examples of operators include `+`, `-`, `*`, `/`, and `new`.</span></span> <span data-ttu-id="69639-293">피연산자의 예로는 리터럴, 필드, 지역 변수 및 식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-293">Examples of operands include literals, fields, local variables, and expressions.</span></span>

<span data-ttu-id="69639-294">식에 여러 연산자가 포함되어 있으면 연산자의 ***우선 순위***에 따라 개별 연산자가 계산되는 순서가 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-294">When an expression contains multiple operators, the ***precedence*** of the operators controls the order in which the individual operators are evaluated.</span></span> <span data-ttu-id="69639-295">예를 들어 `*` 연산자는 `+` 연산자보다 우선 순위가 더 높기 때문에 식 `x + y * z`는 `x + (y * z)`로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-295">For example, the expression `x + y * z` is evaluated as `x + (y * z)` because the `*` operator has higher precedence than the `+` operator.</span></span>

<span data-ttu-id="69639-296">대부분의 연산자는 ***오버로드***할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-296">Most operators can be ***overloaded***.</span></span> <span data-ttu-id="69639-297">연산자 오버로드는 피연산자 중 하나 또는 둘 다가 사용자 정의 클래스 또는 구조체 형식인 연산에 대해 사용자 정의 연산자 구현을 지정할 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-297">Operator overloading permits user-defined operator implementations to be specified for operations where one or both of the operands are of a user-defined class or struct type.</span></span>

<span data-ttu-id="69639-298">다음 표에서 순위가 가장 높은 우선 순위에 따라에서 연산자 범주를 나열 하는 C# 연산자를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69639-298">The following table summarizes C#'s operators, listing the operator categories in order of precedence from highest to lowest.</span></span> <span data-ttu-id="69639-299">동일한 범주의 연산자는 우선 순위가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-299">Operators in the same category have equal precedence.</span></span>


| <span data-ttu-id="69639-300">__범주__</span><span class="sxs-lookup"><span data-stu-id="69639-300">__Category__</span></span>                     | <span data-ttu-id="69639-301">__식__</span><span class="sxs-lookup"><span data-stu-id="69639-301">__Expression__</span></span>    | <span data-ttu-id="69639-302">__설명__</span><span class="sxs-lookup"><span data-stu-id="69639-302">__Description__</span></span> |
|----------------------------------|-------------------|-----------------|
| <span data-ttu-id="69639-303">기본 연산자</span><span class="sxs-lookup"><span data-stu-id="69639-303">Primary</span></span>                          | `x.m`             | <span data-ttu-id="69639-304">멤버 액세스</span><span class="sxs-lookup"><span data-stu-id="69639-304">Member access</span></span> |
|                                  | `x(...)`          | <span data-ttu-id="69639-305">메서드 및 대리자 호출</span><span class="sxs-lookup"><span data-stu-id="69639-305">Method and delegate invocation</span></span> |
|                                  | `x[...]`          | <span data-ttu-id="69639-306">배열 및 인덱서 액세스</span><span class="sxs-lookup"><span data-stu-id="69639-306">Array and indexer access</span></span> |
|                                  | `x++`             | <span data-ttu-id="69639-307">후위 증가</span><span class="sxs-lookup"><span data-stu-id="69639-307">Post-increment</span></span> |
|                                  | `x--`             | <span data-ttu-id="69639-308">후위 감소</span><span class="sxs-lookup"><span data-stu-id="69639-308">Post-decrement</span></span> |
|                                  | `new T(...)`      | <span data-ttu-id="69639-309">개체 및 대리자 생성</span><span class="sxs-lookup"><span data-stu-id="69639-309">Object and delegate creation</span></span> |
|                                  | `new T(...){...}` | <span data-ttu-id="69639-310">이니셜라이저를 사용 하 여 개체 만들기</span><span class="sxs-lookup"><span data-stu-id="69639-310">Object creation with initializer</span></span> |
|                                  | `new {...}`       | <span data-ttu-id="69639-311">익명 개체 이니셜라이저</span><span class="sxs-lookup"><span data-stu-id="69639-311">Anonymous object initializer</span></span> |
|                                  | `new T[...]`      | <span data-ttu-id="69639-312">배열 만들기</span><span class="sxs-lookup"><span data-stu-id="69639-312">Array creation</span></span> |
|                                  | `typeof(T)`       | <span data-ttu-id="69639-313">가져올 `System.Type` 개체 `T`</span><span class="sxs-lookup"><span data-stu-id="69639-313">Obtain `System.Type` object for `T`</span></span> |
|                                  | `checked(x)`      | <span data-ttu-id="69639-314">checked 컨텍스트에서 식 계산</span><span class="sxs-lookup"><span data-stu-id="69639-314">Evaluate expression in checked context</span></span> |
|                                  | `unchecked(x)`    | <span data-ttu-id="69639-315">unchecked 컨텍스트에서 식 계산</span><span class="sxs-lookup"><span data-stu-id="69639-315">Evaluate expression in unchecked context</span></span> |
|                                  | `default(T)`      | <span data-ttu-id="69639-316">형식의 기본값 가져오기 `T`</span><span class="sxs-lookup"><span data-stu-id="69639-316">Obtain default value of type `T`</span></span> |
|                                  | `delegate {...}`  | <span data-ttu-id="69639-317">익명 함수(무명 메서드)</span><span class="sxs-lookup"><span data-stu-id="69639-317">Anonymous function (anonymous method)</span></span> |
| <span data-ttu-id="69639-318">단항</span><span class="sxs-lookup"><span data-stu-id="69639-318">Unary</span></span>                            | `+x`              | <span data-ttu-id="69639-319">클레임</span><span class="sxs-lookup"><span data-stu-id="69639-319">Identity</span></span> |
|                                  | `-x`              | <span data-ttu-id="69639-320">부정</span><span class="sxs-lookup"><span data-stu-id="69639-320">Negation</span></span> |
|                                  | `!x`              | <span data-ttu-id="69639-321">논리 부정</span><span class="sxs-lookup"><span data-stu-id="69639-321">Logical negation</span></span> |
|                                  | `~x`              | <span data-ttu-id="69639-322">비트 부정 연산</span><span class="sxs-lookup"><span data-stu-id="69639-322">Bitwise negation</span></span> |
|                                  | `++x`             | <span data-ttu-id="69639-323">전위 증가</span><span class="sxs-lookup"><span data-stu-id="69639-323">Pre-increment</span></span> |
|                                  | `--x`             | <span data-ttu-id="69639-324">전위 감소</span><span class="sxs-lookup"><span data-stu-id="69639-324">Pre-decrement</span></span> |
|                                  | `(T)x`            | <span data-ttu-id="69639-325">명시적으로 변환 `x` 형식 `T`</span><span class="sxs-lookup"><span data-stu-id="69639-325">Explicitly convert `x` to type `T`</span></span> |
|                                  | `await x`         | <span data-ttu-id="69639-326">비동기적으로 대기할 `x` 완료</span><span class="sxs-lookup"><span data-stu-id="69639-326">Asynchronously wait for `x` to complete</span></span> |
| <span data-ttu-id="69639-327">곱하기</span><span class="sxs-lookup"><span data-stu-id="69639-327">Multiplicative</span></span>                   | `x * y`           | <span data-ttu-id="69639-328">곱하기</span><span class="sxs-lookup"><span data-stu-id="69639-328">Multiplication</span></span> |
|                                  | `x / y`           | <span data-ttu-id="69639-329">나눗셈 기호</span><span class="sxs-lookup"><span data-stu-id="69639-329">Division</span></span> |
|                                  | `x % y`           | <span data-ttu-id="69639-330">나머지</span><span class="sxs-lookup"><span data-stu-id="69639-330">Remainder</span></span> |
| <span data-ttu-id="69639-331">더하기</span><span class="sxs-lookup"><span data-stu-id="69639-331">Additive</span></span>                         | `x + y`           | <span data-ttu-id="69639-332">더하기, 문자열 연결, 대리자 결합</span><span class="sxs-lookup"><span data-stu-id="69639-332">Addition, string concatenation, delegate combination</span></span> |
|                                  | `x - y`           | <span data-ttu-id="69639-333">빼기, 대리자 제거</span><span class="sxs-lookup"><span data-stu-id="69639-333">Subtraction, delegate removal</span></span> |
| <span data-ttu-id="69639-334">시프트</span><span class="sxs-lookup"><span data-stu-id="69639-334">Shift</span></span>                            | `x << y`          | <span data-ttu-id="69639-335">왼쪽 시프트</span><span class="sxs-lookup"><span data-stu-id="69639-335">Shift left</span></span> |
|                                  | `x >> y`          | <span data-ttu-id="69639-336">오른쪽 시프트</span><span class="sxs-lookup"><span data-stu-id="69639-336">Shift right</span></span> |
| <span data-ttu-id="69639-337">관계형 및 형식 테스트</span><span class="sxs-lookup"><span data-stu-id="69639-337">Relational and type testing</span></span>      | `x < y`           | <span data-ttu-id="69639-338">보다 작음</span><span class="sxs-lookup"><span data-stu-id="69639-338">Less than</span></span> |
|                                  | `x > y`           | <span data-ttu-id="69639-339">보다 큼</span><span class="sxs-lookup"><span data-stu-id="69639-339">Greater than</span></span> |
|                                  | `x <= y`          | <span data-ttu-id="69639-340">작거나 같음</span><span class="sxs-lookup"><span data-stu-id="69639-340">Less than or equal</span></span> |
|                                  | `x >= y`          | <span data-ttu-id="69639-341">크거나 같음</span><span class="sxs-lookup"><span data-stu-id="69639-341">Greater than or equal</span></span> |
|                                  | `x is T`          | <span data-ttu-id="69639-342">반환 `true` 경우 `x` 되는 `T`, `false` 그렇지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="69639-342">Return `true` if `x` is a `T`, `false` otherwise</span></span> |
|                                  | `x as T`          | <span data-ttu-id="69639-343">반환 `x` 로 형식화 `T`, 또는 `null` 경우 `x` 아닙니다를 `T`</span><span class="sxs-lookup"><span data-stu-id="69639-343">Return `x` typed as `T`, or `null` if `x` is not a `T`</span></span> |
| <span data-ttu-id="69639-344">같음</span><span class="sxs-lookup"><span data-stu-id="69639-344">Equality</span></span>                         | `x == y`          | <span data-ttu-id="69639-345">Equal</span><span class="sxs-lookup"><span data-stu-id="69639-345">Equal</span></span>      |
|                                  | `x != y`          | <span data-ttu-id="69639-346">같지 않음</span><span class="sxs-lookup"><span data-stu-id="69639-346">Not equal</span></span> |
| <span data-ttu-id="69639-347">논리적 AND</span><span class="sxs-lookup"><span data-stu-id="69639-347">Logical AND</span></span>                      | `x & y`           | <span data-ttu-id="69639-348">정수 비트 AND, 부울 논리곱 AND</span><span class="sxs-lookup"><span data-stu-id="69639-348">Integer bitwise AND, boolean logical AND</span></span> |
| <span data-ttu-id="69639-349">논리 XOR</span><span class="sxs-lookup"><span data-stu-id="69639-349">Logical XOR</span></span>                      | `x ^ y`           | <span data-ttu-id="69639-350">정수 비트 XOR, 부울 논리곱 XOR</span><span class="sxs-lookup"><span data-stu-id="69639-350">Integer bitwise XOR, boolean logical XOR</span></span> |
| <span data-ttu-id="69639-351">논리적 OR</span><span class="sxs-lookup"><span data-stu-id="69639-351">Logical OR</span></span>                       | <span data-ttu-id="69639-352">' x</span><span class="sxs-lookup"><span data-stu-id="69639-352">\`x</span></span> | <span data-ttu-id="69639-353">y'</span><span class="sxs-lookup"><span data-stu-id="69639-353">y\`</span></span>           | <span data-ttu-id="69639-354">정수 비트 OR, 부울 논리곱 OR</span><span class="sxs-lookup"><span data-stu-id="69639-354">Integer bitwise OR, boolean logical OR</span></span> |
| <span data-ttu-id="69639-355">조건부 AND</span><span class="sxs-lookup"><span data-stu-id="69639-355">Conditional AND</span></span>                  | `x && y`          | <span data-ttu-id="69639-356">평가 `y` 경우에만 `x` 는 `true`</span><span class="sxs-lookup"><span data-stu-id="69639-356">Evaluates `y` only if `x` is `true`</span></span> |
| <span data-ttu-id="69639-357">조건부 OR</span><span class="sxs-lookup"><span data-stu-id="69639-357">Conditional OR</span></span>                   | <span data-ttu-id="69639-358">' x</span><span class="sxs-lookup"><span data-stu-id="69639-358">\`x</span></span> || <span data-ttu-id="69639-359">y'</span><span class="sxs-lookup"><span data-stu-id="69639-359">y\`</span></span>          | <span data-ttu-id="69639-360">평가 `y` 경우에만 `x` 는 `false`</span><span class="sxs-lookup"><span data-stu-id="69639-360">Evaluates `y` only if `x` is `false`</span></span> |
| <span data-ttu-id="69639-361">Null 결합</span><span class="sxs-lookup"><span data-stu-id="69639-361">Null coalescing</span></span>                  | `X ?? y`          | <span data-ttu-id="69639-362">로 `y` 경우 `x` 됩니다 `null`를 `x` 그렇지 않은 경우</span><span class="sxs-lookup"><span data-stu-id="69639-362">Evaluates to `y` if `x` is `null`, to `x` otherwise</span></span> |
| <span data-ttu-id="69639-363">조건</span><span class="sxs-lookup"><span data-stu-id="69639-363">Conditional</span></span>                      | `x ? y : z`       | <span data-ttu-id="69639-364">평가 `y` 하는 경우 `x` 됩니다 `true`, `z` 경우 `x` 됩니다 `false`</span><span class="sxs-lookup"><span data-stu-id="69639-364">Evaluates `y` if `x` is `true`, `z` if `x` is `false`</span></span> |
| <span data-ttu-id="69639-365">대입 또는 익명 함수</span><span class="sxs-lookup"><span data-stu-id="69639-365">Assignment or anonymous function</span></span> | `x = y`           | <span data-ttu-id="69639-366">할당</span><span class="sxs-lookup"><span data-stu-id="69639-366">Assignment</span></span> |
|                                  | `x op= y`         | <span data-ttu-id="69639-367">복합 할당 지원 되는 연산자는 `*=` `/=` `%=` `+=` `-=` `<<=` `>>=` `&=` `^=` \`</span><span class="sxs-lookup"><span data-stu-id="69639-367">Compound assignment; supported operators are `*=` `/=` `%=` `+=` `-=` `<<=` `>>=` `&=` `^=` \`</span></span>|=` |
|                                  | `(T x) => y`      | <span data-ttu-id="69639-368">익명 함수(람다 식)</span><span class="sxs-lookup"><span data-stu-id="69639-368">Anonymous function (lambda expression)</span></span> |

## <a name="statements"></a><span data-ttu-id="69639-369">문</span><span class="sxs-lookup"><span data-stu-id="69639-369">Statements</span></span>

<span data-ttu-id="69639-370">프로그램의 동작은 ***문***을 사용하여 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-370">The actions of a program are expressed using ***statements***.</span></span> <span data-ttu-id="69639-371">C#은 여러 다른 종류의 문을 지원하며 이중 많은 문이 포함 문에 대해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-371">C# supports several different kinds of statements, a number of which are defined in terms of embedded statements.</span></span>

<span data-ttu-id="69639-372">***블록***은 단일 문이 허용되는 컨텍스트에서 여러 문을 쓸 수 있도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-372">A ***block*** permits multiple statements to be written in contexts where a single statement is allowed.</span></span> <span data-ttu-id="69639-373">블록은 구분 기호 `{`와 `}` 사이에 쓴 문 목록으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-373">A block consists of a list of statements written between the delimiters `{` and `}`.</span></span>

<span data-ttu-id="69639-374">***선언 문***은 지역 변수 및 상수를 선언하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-374">***Declaration statements*** are used to declare local variables and constants.</span></span>

<span data-ttu-id="69639-375">***식 문***은 식을 평가하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-375">***Expression statements*** are used to evaluate expressions.</span></span> <span data-ttu-id="69639-376">할당을 사용 하 여 개체 메서드 호출을 포함 하는 문으로 사용할 수 있는 식의 `new` 연산자를 사용 하 여 할당 `=` 복합 할당 연산자를 사용 합니다 증가및감소작업`++`고 `--` 연산자 await 식 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-376">Expressions that can be used as statements include method invocations, object allocations using the `new` operator, assignments using `=` and the compound assignment operators, increment and decrement operations using the `++` and `--` operators and await expressions.</span></span>

<span data-ttu-id="69639-377">***선택 문***은 일부 식 값에 따라 실행할 수 있는 다양한 문 중에서 하나를 선택하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-377">***Selection statements*** are used to select one of a number of possible statements for execution based on the value of some expression.</span></span> <span data-ttu-id="69639-378">이 그룹에는 `if` 및 `switch` 문이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-378">In this group are the `if` and `switch` statements.</span></span>

<span data-ttu-id="69639-379">***반복 문*** 포함된 문을 반복적으로 실행 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-379">***Iteration statements*** are used to repeatedly execute an embedded statement.</span></span> <span data-ttu-id="69639-380">이 그룹에는 `while`, `do`, `for` 및 `foreach` 문이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-380">In this group are the `while`, `do`, `for`, and `foreach` statements.</span></span>

<span data-ttu-id="69639-381">***점프 문***은 제어를 전달하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-381">***Jump statements*** are used to transfer control.</span></span> <span data-ttu-id="69639-382">이 그룹에는 `break`, `continue`, `goto`, `throw`, `return` 및 `yield` 문이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-382">In this group are the `break`, `continue`, `goto`, `throw`, `return`, and `yield` statements.</span></span>

<span data-ttu-id="69639-383">`try`... `catch` 문은 블록 실행 중에 발생하는 예외를 catch하는 데 사용되고 `try`... `finally` 문은 예외 발생 여부에 관계 없이 항상 실행되는 종료 코드를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-383">The `try`...`catch` statement is used to catch exceptions that occur during execution of a block, and the `try`...`finally` statement is used to specify finalization code that is always executed, whether an exception occurred or not.</span></span>

<span data-ttu-id="69639-384">합니다 `checked` 및 `unchecked` 문을 사용 하 여 오버플로 검사 정수 형식 산술 연산 및 변환에 대 한 컨텍스트를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-384">The `checked` and `unchecked` statements are used to control the overflow checking context for integral-type arithmetic operations and conversions.</span></span>

<span data-ttu-id="69639-385">`lock` 문은 지정된 개체에 대한 상호 배타적 잠금을 획득하고, 문을 실행한 후 잠금을 해제하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-385">The `lock` statement is used to obtain the mutual-exclusion lock for a given object, execute a statement, and then release the lock.</span></span>

<span data-ttu-id="69639-386">`using` 문은 리소스를 획득하고, 문을 실행한 후 해당 리소스를 삭제하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-386">The `using` statement is used to obtain a resource, execute a statement, and then dispose of that resource.</span></span>

<span data-ttu-id="69639-387">다음은 문의 각 종류의 예</span><span class="sxs-lookup"><span data-stu-id="69639-387">Below are examples of each kind of statement</span></span>

<span data-ttu-id="69639-388">__지역 변수 선언__</span><span class="sxs-lookup"><span data-stu-id="69639-388">__Local variable declarations__</span></span>

```csharp
static void Main() {
   int a;
   int b = 2, c = 3;
   a = 1;
   Console.WriteLine(a + b + c);
}
```


<span data-ttu-id="69639-389">__지역 상수 선언__</span><span class="sxs-lookup"><span data-stu-id="69639-389">__Local constant declaration__</span></span>

```csharp
static void Main() {
    const float pi = 3.1415927f;
    const int r = 25;
    Console.WriteLine(pi * r * r);
}
```


<span data-ttu-id="69639-390">__식 문__</span><span class="sxs-lookup"><span data-stu-id="69639-390">__Expression statement__</span></span>

```csharp
static void Main() {
    int i;
    i = 123;                // Expression statement
    Console.WriteLine(i);   // Expression statement
    i++;                    // Expression statement
    Console.WriteLine(i);   // Expression statement
}
```

<span data-ttu-id="69639-391">__`if` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-391">__`if` statement__</span></span>

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


<span data-ttu-id="69639-392">__`switch` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-392">__`switch` statement__</span></span>

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

<span data-ttu-id="69639-393">__`while` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-393">__`while` statement__</span></span>

```csharp
static void Main(string[] args) {
    int i = 0;
    while (i < args.Length) {
        Console.WriteLine(args[i]);
        i++;
    }
}
```


<span data-ttu-id="69639-394">__`do` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-394">__`do` statement__</span></span>

```csharp
static void Main() {
    string s;
    do {
        s = Console.ReadLine();
        if (s != null) Console.WriteLine(s);
    } while (s != null);
}
```

<span data-ttu-id="69639-395">__`for` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-395">__`for` statement__</span></span>

```csharp
static void Main(string[] args) {
    for (int i = 0; i < args.Length; i++) {
        Console.WriteLine(args[i]);
    }
}
```

<span data-ttu-id="69639-396">__`foreach` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-396">__`foreach` statement__</span></span>

```csharp
static void Main(string[] args) {
    foreach (string s in args) {
        Console.WriteLine(s);
    }
}
```

<span data-ttu-id="69639-397">__`break` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-397">__`break` statement__</span></span>

```csharp
static void Main() {
    while (true) {
        string s = Console.ReadLine();
        if (s == null) break;
        Console.WriteLine(s);
    }
}
```

<span data-ttu-id="69639-398">__`continue` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-398">__`continue` statement__</span></span>

```csharp
static void Main(string[] args) {
    for (int i = 0; i < args.Length; i++) {
        if (args[i].StartsWith("/")) continue;
        Console.WriteLine(args[i]);
    }
}
```

<span data-ttu-id="69639-399">__`goto` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-399">__`goto` statement__</span></span>

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

<span data-ttu-id="69639-400">__`return` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-400">__`return` statement__</span></span>

```csharp
static int Add(int a, int b) {
    return a + b;
}

static void Main() {
    Console.WriteLine(Add(1, 2));
    return;
}
```

<span data-ttu-id="69639-401">__`yield` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-401">__`yield` statement__</span></span>

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

<span data-ttu-id="69639-402">__`throw` 및 `try` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-402">__`throw` and `try` statements__</span></span>

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

<span data-ttu-id="69639-403">__`checked` 및 `unchecked` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-403">__`checked` and `unchecked` statements__</span></span>

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

<span data-ttu-id="69639-404">__`lock` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-404">__`lock` statement__</span></span>

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

<span data-ttu-id="69639-405">__`using` 문__</span><span class="sxs-lookup"><span data-stu-id="69639-405">__`using` statement__</span></span>

```csharp
static void Main() {
    using (TextWriter w = File.CreateText("test.txt")) {
        w.WriteLine("Line one");
        w.WriteLine("Line two");
        w.WriteLine("Line three");
    }
}
```

## <a name="classes-and-objects"></a><span data-ttu-id="69639-406">클래스 및 개체</span><span class="sxs-lookup"><span data-stu-id="69639-406">Classes and objects</span></span>

<span data-ttu-id="69639-407">***클래스***는 C#의 가장 기본적인 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-407">***Classes*** are the most fundamental of C#'s types.</span></span> <span data-ttu-id="69639-408">클래스는 상태(필드)와 작업(메서드 및 기타 함수 멤버)을 하나의 단위로 결합하는 데이터 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-408">A class is a data structure that combines state (fields) and actions (methods and other function members) in a single unit.</span></span> <span data-ttu-id="69639-409">클래스는 해당 클래스의 동적으로 생성된 ***인스턴스***(***개체***라고도 함)에 대한 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-409">A class provides a definition for dynamically created ***instances*** of the class, also known as ***objects***.</span></span> <span data-ttu-id="69639-410">클래스는 ***상속*** 및 ***다형성***과 ***파생된 클래스***가 ***기본 클래스***를 확장하고 특수화할 수 있는 메커니즘을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-410">Classes support ***inheritance*** and ***polymorphism***, mechanisms whereby ***derived classes*** can extend and specialize ***base classes***.</span></span>

<span data-ttu-id="69639-411">새 클래스는 클래스 선언을 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="69639-411">New classes are created using class declarations.</span></span> <span data-ttu-id="69639-412">클래스 선언은 클래스의 특성 및 한정자, 클래스의 이름, 기본 클래스(제공된 경우), 클래스로 구현되는 인터페이스를 지정하는 헤더로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-412">A class declaration starts with a header that specifies the attributes and modifiers of the class, the name of the class, the base class (if given), and the interfaces implemented by the class.</span></span> <span data-ttu-id="69639-413">헤더 다음에는 구분 기호 `{` 및 `}` 간에 작성되는 멤버 선언 목록으로 구성되는 클래스 본문이 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="69639-413">The header is followed by the class body, which consists of a list of member declarations written between the delimiters `{` and `}`.</span></span>

<span data-ttu-id="69639-414">다음은 `Point`라는 간단한 클래스 선언입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-414">The following is a declaration of a simple class named `Point`:</span></span>

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
<span data-ttu-id="69639-415">클래스의 인스턴스는 새 인스턴스에 대한 메모리를 할당하고, 인스턴스를 초기화하는 생성자를 호출하고, 인스턴스에 대한 참조를 반환하는 `new` 연산자를 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="69639-415">Instances of classes are created using the `new` operator, which allocates memory for a new instance, invokes a constructor to initialize the instance, and returns a reference to the instance.</span></span> <span data-ttu-id="69639-416">다음 문은 두 개의 만듭니다 `Point` 개체 및 해당 개체에 대 한 참조가 두 변수에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-416">The following statements create two `Point` objects and store references to those objects in two variables:</span></span>

```
Point p1 = new Point(0, 0);
Point p2 = new Point(10, 20);
```
<span data-ttu-id="69639-417">개체에서 사용한 메모리는 개체가 더 이상 사용에서 하는 경우 자동으로 회수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-417">The memory occupied by an object is automatically reclaimed when the object is no longer in use.</span></span> <span data-ttu-id="69639-418">C#에서 개체를 명시적으로 할당 취소할 필요도 없으며 가능하지도 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-418">It is neither necessary nor possible to explicitly deallocate objects in C#.</span></span>

### <a name="members"></a><span data-ttu-id="69639-419">멤버</span><span class="sxs-lookup"><span data-stu-id="69639-419">Members</span></span>

<span data-ttu-id="69639-420">클래스의 멤버는 ***정적 멤버*** 하거나 ***인스턴스 멤버***합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-420">The members of a class are either ***static members*** or ***instance members***.</span></span> <span data-ttu-id="69639-421">정적 멤버는 클래스에 속하며 인스턴스 멤버는 개체(클래스의 인스턴스)에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-421">Static members belong to classes, and instance members belong to objects (instances of classes).</span></span>

<span data-ttu-id="69639-422">다음 표에서 클래스는 포함할 수는 멤버 종류에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-422">The following table provides an overview of the kinds of members a class can contain.</span></span>


| <span data-ttu-id="69639-423">__멤버__</span><span class="sxs-lookup"><span data-stu-id="69639-423">__Member__</span></span>   | <span data-ttu-id="69639-424">__설명__</span><span class="sxs-lookup"><span data-stu-id="69639-424">__Description__</span></span> |
|------------  |-----------------|
| <span data-ttu-id="69639-425">상수</span><span class="sxs-lookup"><span data-stu-id="69639-425">Constants</span></span>    | <span data-ttu-id="69639-426">클래스와 연결된 상수 값</span><span class="sxs-lookup"><span data-stu-id="69639-426">Constant values associated with the class</span></span> |
| <span data-ttu-id="69639-427">필드</span><span class="sxs-lookup"><span data-stu-id="69639-427">Fields</span></span>       | <span data-ttu-id="69639-428">클래스의 변수</span><span class="sxs-lookup"><span data-stu-id="69639-428">Variables of the class</span></span> |
| <span data-ttu-id="69639-429">메서드</span><span class="sxs-lookup"><span data-stu-id="69639-429">Methods</span></span>      | <span data-ttu-id="69639-430">클래스가 수행할 수 있는 계산 및 작업</span><span class="sxs-lookup"><span data-stu-id="69639-430">Computations and actions that can be performed by the class</span></span> |
| <span data-ttu-id="69639-431">속성</span><span class="sxs-lookup"><span data-stu-id="69639-431">Properties</span></span>   | <span data-ttu-id="69639-432">클래스의 명명된 속성에 대한 읽기 및 쓰기와 관련된 작업</span><span class="sxs-lookup"><span data-stu-id="69639-432">Actions associated with reading and writing named properties of the class</span></span> |
| <span data-ttu-id="69639-433">인덱서</span><span class="sxs-lookup"><span data-stu-id="69639-433">Indexers</span></span>     | <span data-ttu-id="69639-434">클래스 인스턴스를 배열처럼 인덱싱하는 것과 관련된 작업</span><span class="sxs-lookup"><span data-stu-id="69639-434">Actions associated with indexing instances of the class like an array</span></span> |
| <span data-ttu-id="69639-435">이벤트</span><span class="sxs-lookup"><span data-stu-id="69639-435">Events</span></span>       | <span data-ttu-id="69639-436">클래스에 의해 생성될 수 있는 알림</span><span class="sxs-lookup"><span data-stu-id="69639-436">Notifications that can be generated by the class</span></span> |
| <span data-ttu-id="69639-437">연산자</span><span class="sxs-lookup"><span data-stu-id="69639-437">Operators</span></span>    | <span data-ttu-id="69639-438">클래스가 지원하는 변환 및 식 연산자</span><span class="sxs-lookup"><span data-stu-id="69639-438">Conversions and expression operators supported by the class</span></span> |
| <span data-ttu-id="69639-439">생성자</span><span class="sxs-lookup"><span data-stu-id="69639-439">Constructors</span></span> | <span data-ttu-id="69639-440">클래스의 인스턴스 또는 클래스 자체를 초기화하는 데 필요한 작업</span><span class="sxs-lookup"><span data-stu-id="69639-440">Actions required to initialize instances of the class or the class itself</span></span> |
| <span data-ttu-id="69639-441">소멸자</span><span class="sxs-lookup"><span data-stu-id="69639-441">Destructors</span></span>  | <span data-ttu-id="69639-442">클래스의 인스턴스가 영구적으로 삭제되기 전에 수행 작업</span><span class="sxs-lookup"><span data-stu-id="69639-442">Actions to perform before instances of the class are permanently discarded</span></span> |
| <span data-ttu-id="69639-443">유형</span><span class="sxs-lookup"><span data-stu-id="69639-443">Types</span></span>        | <span data-ttu-id="69639-444">클래스에 의해 선언된 중첩 형식</span><span class="sxs-lookup"><span data-stu-id="69639-444">Nested types declared by the class</span></span> |

### <a name="accessibility"></a><span data-ttu-id="69639-445">액세스 가능성</span><span class="sxs-lookup"><span data-stu-id="69639-445">Accessibility</span></span>

<span data-ttu-id="69639-446">클래스의 각 멤버에는 멤버에 액세스할 수 있는 프로그램 텍스트의 영역을 제어하는 액세스 가능성이 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-446">Each member of a class has an associated accessibility, which controls the regions of program text that are able to access the member.</span></span> <span data-ttu-id="69639-447">액세스 가능성은 5가지 형태로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-447">There are five possible forms of accessibility.</span></span> <span data-ttu-id="69639-448">각각은 다음 표에 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-448">These are summarized in the following table.</span></span>


| <span data-ttu-id="69639-449">__액세스 가능성__</span><span class="sxs-lookup"><span data-stu-id="69639-449">__Accessibility__</span></span>    | <span data-ttu-id="69639-450">__의미__</span><span class="sxs-lookup"><span data-stu-id="69639-450">__Meaning__</span></span> |
|----------------------|-----------------|
| `public`             | <span data-ttu-id="69639-451">액세스가 제한되지 않음</span><span class="sxs-lookup"><span data-stu-id="69639-451">Access not limited</span></span> |
| `protected`          | <span data-ttu-id="69639-452">이 클래스 또는 이 클래스에서 파생된 클래스로만 액세스가 제한됨</span><span class="sxs-lookup"><span data-stu-id="69639-452">Access limited to this class or classes derived from this class</span></span> |
| `internal`           | <span data-ttu-id="69639-453">이 프로그램으로만 액세스가 제한됨</span><span class="sxs-lookup"><span data-stu-id="69639-453">Access limited to this program</span></span> |
| `protected internal` | <span data-ttu-id="69639-454">이 프로그램 또는 이 클래스에서 파생된 클래스로만 액세스가 제한됨</span><span class="sxs-lookup"><span data-stu-id="69639-454">Access limited to this program or classes derived from this class</span></span> |
| `private`            | <span data-ttu-id="69639-455">이 클래스로만 액세스가 제한됨</span><span class="sxs-lookup"><span data-stu-id="69639-455">Access limited to this class</span></span> |

### <a name="type-parameters"></a><span data-ttu-id="69639-456">형식 매개 변수</span><span class="sxs-lookup"><span data-stu-id="69639-456">Type parameters</span></span>

<span data-ttu-id="69639-457">클래스 정의는 클래스 이름 다음에 대괄호로 묶은 형식 매개 변수 이름 목록을 지정하여 형식 매개 변수 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-457">A class definition may specify a set of type parameters by following the class name with angle brackets enclosing a list of type parameter names.</span></span> <span data-ttu-id="69639-458">형식 매개 변수 수는 클래스 선언의 본문에 클래스의 멤버를 정의 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-458">The type parameters can the be used in the body of the class declarations to define the members of the class.</span></span> <span data-ttu-id="69639-459">다음 예제에서 `Pair`의 형식 매개 변수는 `TFirst` 및 `TSecond`입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-459">In the following example, the type parameters of `Pair` are `TFirst` and `TSecond`:</span></span>

```csharp
public class Pair<TFirst,TSecond>
{
    public TFirst First;
    public TSecond Second;
}
```
<span data-ttu-id="69639-460">형식 매개 변수를 사용 하도록 선언 하는 클래스 형식에는 제네릭 클래스 형식을 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-460">A class type that is declared to take type parameters is called a generic class type.</span></span> <span data-ttu-id="69639-461">구조체, 인터페이스 및 대리자 형식도 제네릭일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-461">Struct, interface and delegate types can also be generic.</span></span>

<span data-ttu-id="69639-462">제네릭 클래스를 사용하는 경우 각 형식 매개 변수에 대해 다음과 같은 형식 인수가 제공되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-462">When the generic class is used, type arguments must be provided for each of the type parameters:</span></span>

```csharp
Pair<int,string> pair = new Pair<int,string> { First = 1, Second = "two" };
int i = pair.First;     // TFirst is int
string s = pair.Second; // TSecond is string
```
<span data-ttu-id="69639-463">예: 제공 된 형식 인수를 사용 하 여 제네릭 형식 `Pair<int,string>
    ` 위에서 생성 된 형식 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-463">A generic type with type arguments provided, like `Pair<int,string>
    ` above, is called a constructed type.</span></span>

### <a name="base-classes"></a><span data-ttu-id="69639-464">기본 클래스</span><span class="sxs-lookup"><span data-stu-id="69639-464">Base classes</span></span>

<span data-ttu-id="69639-465">클래스 선언은 클래스 이름 및 형식 매개 변수 뒤에 콜론과 기본 클래스의 이름을 사용하여 기본 클래스를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-465">A class declaration may specify a base class by following the class name and type parameters with a colon and the name of the base class.</span></span> <span data-ttu-id="69639-466">기본 클래스 지정을 생략하면 `object` 형식에서 파생되는 클래스와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-466">Omitting a base class specification is the same as deriving from type `object`.</span></span> <span data-ttu-id="69639-467">다음 예제에서 `Point3D`의 기본 클래스는 `Point`이고 `Point`의 기본 클래스는 `object`입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-467">In the following example, the base class of `Point3D` is `Point`, and the base class of `Point` is `object`:</span></span>

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
<span data-ttu-id="69639-468">클래스는 기본 클래스의 멤버를 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-468">A class inherits the members of its base class.</span></span> <span data-ttu-id="69639-469">상속은 클래스 인스턴스 및 정적 생성자와 기본 클래스의 소멸자를 제외 하 고, 기본 클래스의 모든 멤버를 암시적으로 포함 하는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-469">Inheritance means that a class implicitly contains all members of its base class, except for the instance and static constructors, and the destructors of the base class.</span></span> <span data-ttu-id="69639-470">파생된 클래스를 상속하는 대상에 새 멤버를 추가할 수 있지만 상속된 멤버의 정의를 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-470">A derived class can add new members to those it inherits, but it cannot remove the definition of an inherited member.</span></span> <span data-ttu-id="69639-471">앞의 예제에서 `Point3D`는 `Point`에서 `x` 및 `y` 필드를 상속하고 모든 `Point3D` 인스턴스는 세 개의 필드, 즉 `x`, `y` 및 `z`를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-471">In the previous example, `Point3D` inherits the `x` and `y` fields from `Point`, and every `Point3D` instance contains three fields, `x`, `y`, and `z`.</span></span>

<span data-ttu-id="69639-472">클래스 형식에서 해당 기본 클래스 형식 간에 암시적 변환이 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-472">An implicit conversion exists from a class type to any of its base class types.</span></span> <span data-ttu-id="69639-473">따라서 클래스 형식의 변수는 해당 클래스의 인스턴스 또는 파생된 모든 클래스의 인스턴스를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-473">Therefore, a variable of a class type can reference an instance of that class or an instance of any derived class.</span></span> <span data-ttu-id="69639-474">예를 들어 이전 클래스 선언에서 형식 `Point`의 변수는 `Point` 또는 `Point3D`를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-474">For example, given the previous class declarations, a variable of type `Point` can reference either a `Point` or a `Point3D`:</span></span>

```csharp
Point a = new Point(10, 20);
Point b = new Point3D(10, 20, 30);
```

### <a name="fields"></a><span data-ttu-id="69639-475">필드</span><span class="sxs-lookup"><span data-stu-id="69639-475">Fields</span></span>

<span data-ttu-id="69639-476">필드는 클래스 또는 클래스의 인스턴스와 연결 된 변수.</span><span class="sxs-lookup"><span data-stu-id="69639-476">A field is a variable that is associated with a class or with an instance of a class.</span></span>

<span data-ttu-id="69639-477">필드를 사용 하 여 선언 된 `static` 한정자를 정의 ***정적 필드***합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-477">A field declared with the `static` modifier defines a ***static field***.</span></span> <span data-ttu-id="69639-478">정적 필드는 정확히 하나의 저장 위치를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-478">A static field identifies exactly one storage location.</span></span> <span data-ttu-id="69639-479">생성된 클래스 인스턴스 수에 관계없이 정적 필드의 복사본은 하나뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-479">No matter how many instances of a class are created, there is only ever one copy of a static field.</span></span>

<span data-ttu-id="69639-480">없이 선언 된 필드를 `static` 한정자를 정의 ***인스턴스 필드***합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-480">A field declared without the `static` modifier defines an ***instance field***.</span></span> <span data-ttu-id="69639-481">클래스의 모든 인스턴스는 해당 클래스의 모든 인스턴스 필드의 별도 복사본을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-481">Every instance of a class contains a separate copy of all the instance fields of that class.</span></span>

<span data-ttu-id="69639-482">다음 예제에서 `Color` 클래스의 각 인스턴스는 `r`, `g` 및 `b` 인스턴스 필드의 별도 복사본을 갖지만 `Black`, `White`, `Red`, `Green` 및 `Blue` 정적 필드의 복사본은 하나뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-482">In the following example, each instance of the `Color` class has a separate copy of the `r`, `g`, and `b` instance fields, but there is only one copy of the `Black`, `White`, `Red`, `Green`, and `Blue` static fields:</span></span>

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
<span data-ttu-id="69639-483">앞의 예제와 같이 ***읽기 전용 필드***는 `readonly` 한정자를 사용하여 선언될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-483">As shown in the previous example, ***read-only fields*** may be declared with a `readonly` modifier.</span></span> <span data-ttu-id="69639-484">에 할당 된 `readonly` 필드의 일부로 필드의 선언 또는 동일한 클래스의 생성자에서 에서만 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-484">Assignment to a `readonly` field can only occur as part of the field's declaration or in a constructor in the same class.</span></span>

### <a name="methods"></a><span data-ttu-id="69639-485">메서드</span><span class="sxs-lookup"><span data-stu-id="69639-485">Methods</span></span>

<span data-ttu-id="69639-486">***메서드***는 개체 또는 클래스에서 수행할 수 있는 계산이나 작업을 구현하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-486">A ***method*** is a member that implements a computation or action that can be performed by an object or class.</span></span> <span data-ttu-id="69639-487">***정적 메서드***는 클래스를 통해 액세스됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-487">***Static methods*** are accessed through the class.</span></span> <span data-ttu-id="69639-488">***인스턴스 메서드***는 클래스의 인스턴스를 통해 액세스됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-488">***Instance methods*** are accessed through instances of the class.</span></span>

<span data-ttu-id="69639-489">메서드는 대개 비어 있는 목록이 남아 있을 ***매개 변수***, 값 또는 메서드에 전달 된 변수 참조를 나타내는 및 ***반환 형식***를 계산 하 고 반환한 값의 형식을 지정 하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-489">Methods have a (possibly empty) list of ***parameters***, which represent values or variable references passed to the method, and a ***return type***, which specifies the type of the value computed and returned by the method.</span></span> <span data-ttu-id="69639-490">메서드의 반환 형식은 `void` 값을 반환 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="69639-490">A method's return type is `void` if it does not return a value.</span></span>

<span data-ttu-id="69639-491">형식과 마찬가지로 메서드에는 메서드가 호출될 때 형식 인수가 지정되어야 하는 형식 매개 변수 집합도 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-491">Like types, methods may also have a set of type parameters, for which type arguments must be specified when the method is called.</span></span> <span data-ttu-id="69639-492">형식과 달리 형식 인수는 종종 메서드 호출의 인수에서 유추될 수 있으므로 명시적으로 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-492">Unlike types, the type arguments can often be inferred from the arguments of a method call and need not be explicitly given.</span></span>

<span data-ttu-id="69639-493">메서드의 ***시그니처***는 메서드가 선언되는 클래스에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-493">The ***signature*** of a method must be unique in the class in which the method is declared.</span></span> <span data-ttu-id="69639-494">메서드 시그니처는 메서드의 이름, 형식 매개 변수의 수, 해당 매개 변수의 수, 한정자 및 형식으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-494">The signature of a method consists of the name of the method, the number of type parameters and the number, modifiers, and types of its parameters.</span></span> <span data-ttu-id="69639-495">메서드 시그니처는 반환 형식을 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-495">The signature of a method does not include the return type.</span></span>

#### <a name="parameters"></a><span data-ttu-id="69639-496">매개 변수</span><span class="sxs-lookup"><span data-stu-id="69639-496">Parameters</span></span>

<span data-ttu-id="69639-497">매개 변수는 메서드에 값 또는 변수 참조를 전달하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-497">Parameters are used to pass values or variable references to methods.</span></span> <span data-ttu-id="69639-498">메서드의 매개 변수는 메서드가 호출될 때 지정된 ***인수***에서 실제 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="69639-498">The parameters of a method get their actual values from the ***arguments*** that are specified when the method is invoked.</span></span> <span data-ttu-id="69639-499">매개 변수에는 값 매개 변수, 참조 매개 변수, 출력 매개 변수 및 매개 변수 배열의 네 가지 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-499">There are four kinds of parameters: value parameters, reference parameters, output parameters, and parameter arrays.</span></span>

<span data-ttu-id="69639-500">***값 매개 변수***는 입력 매개 변수 전달에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-500">A ***value parameter*** is used for input parameter passing.</span></span> <span data-ttu-id="69639-501">값 매개 변수는 매개 변수에 전달된 인수에서 초기 값을 가져오는 지역 변수에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-501">A value parameter corresponds to a local variable that gets its initial value from the argument that was passed for the parameter.</span></span> <span data-ttu-id="69639-502">값 매개 변수를 수정해도 매개 변수에 전달된 인수에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-502">Modifications to a value parameter do not affect the argument that was passed for the parameter.</span></span>

<span data-ttu-id="69639-503">해당 인수를 생략할 수 있도록 기본값을 지정하면 값 매개 변수는 선택적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-503">Value parameters can be optional, by specifying a default value so that corresponding arguments can be omitted.</span></span>

<span data-ttu-id="69639-504">***참조 매개 변수***는 입력 및 출력 매개 변수 전달 둘 다에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-504">A ***reference parameter*** is used for both input and output parameter passing.</span></span> <span data-ttu-id="69639-505">참조 매개 변수에 전달되는 인수는 변수여야 하며, 메서드를 실행하는 동안 참조 매개 변수는 인수 변수와 동일한 저장소 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="69639-505">The argument passed for a reference parameter must be a variable, and during execution of the method, the reference parameter represents the same storage location as the argument variable.</span></span> <span data-ttu-id="69639-506">참조 매개 변수는 `ref` 한정자를 사용하여 선언됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-506">A reference parameter is declared with the `ref` modifier.</span></span> <span data-ttu-id="69639-507">다음 예제에서는 `ref` 매개 변수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69639-507">The following example shows the use of `ref` parameters.</span></span>

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
<span data-ttu-id="69639-508">***출력 매개 변수***는 출력 매개 변수 전달에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-508">An ***output parameter*** is used for output parameter passing.</span></span> <span data-ttu-id="69639-509">출력 매개 변수는 호출자가 제공한 인수의 초기 값이 중요하지 않다는 점을 제외하고 참조 매개 변수와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-509">An output parameter is similar to a reference parameter except that the initial value of the caller-provided argument is unimportant.</span></span> <span data-ttu-id="69639-510">출력 매개 변수는 `out` 한정자를 사용하여 선언됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-510">An output parameter is declared with the `out` modifier.</span></span> <span data-ttu-id="69639-511">다음 예제에서는 `out` 매개 변수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69639-511">The following example shows the use of `out` parameters.</span></span>

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
<span data-ttu-id="69639-512">***매개 변수 배열***은 다양한 개수의 인수가 메서드에 전달되도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-512">A ***parameter array*** permits a variable number of arguments to be passed to a method.</span></span> <span data-ttu-id="69639-513">매개 변수 배열은 `params` 한정자를 사용하여 선언됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-513">A parameter array is declared with the `params` modifier.</span></span> <span data-ttu-id="69639-514">메서드의 마지막 매개 변수만 매개 변수 배열일 수 있으며 매개 변수 배열의 형식은 1차원 배열 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-514">Only the last parameter of a method can be a parameter array, and the type of a parameter array must be a single-dimensional array type.</span></span> <span data-ttu-id="69639-515">`Write` 하 고 `WriteLine` 의 메서드는 `System.Console` 클래스는 매개 변수 배열 사용의 좋은 예입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-515">The `Write` and `WriteLine` methods of the `System.Console` class are good examples of parameter array usage.</span></span> <span data-ttu-id="69639-516">이러한 메서드는 다음과 같이 선언됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-516">They are declared as follows.</span></span>

```csharp
public class Console
{
    public static void Write(string fmt, params object[] args) {...}
    public static void WriteLine(string fmt, params object[] args) {...}
    ...
}
```
<span data-ttu-id="69639-517">매개 변수 배열을 사용하는 메서드 내에서 매개 변수 배열은 배열 형식의 일반 매개 변수와 정확히 동일하게 동작합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-517">Within a method that uses a parameter array, the parameter array behaves exactly like a regular parameter of an array type.</span></span> <span data-ttu-id="69639-518">그러나 매개 변수 배열을 사용한 메서드 호출에서 매개 변수 배열 형식의 단일 인수 또는 매개 변수 배열에 있는 임의 개수의 요소 형식 인수를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-518">However, in an invocation of a method with a parameter array, it is possible to pass either a single argument of the parameter array type or any number of arguments of the element type of the parameter array.</span></span> <span data-ttu-id="69639-519">후자의 경우 지정된 인수를 사용하여 배열 인스턴스가 자동으로 만들어지고 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-519">In the latter case, an array instance is automatically created and initialized with the given arguments.</span></span> <span data-ttu-id="69639-520">다음 예제는</span><span class="sxs-lookup"><span data-stu-id="69639-520">This example</span></span>

```csharp
Console.WriteLine("x={0} y={1} z={2}", x, y, z);
```
<span data-ttu-id="69639-521">다음을 작성하는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-521">is equivalent to writing the following.</span></span>

```csharp
string s = "x={0} y={1} z={2}";
object[] args = new object[3];
args[0] = x;
args[1] = y;
args[2] = z;
Console.WriteLine(s, args);
```

#### <a name="method-body-and-local-variables"></a><span data-ttu-id="69639-522">메서드 본문 및 지역 변수</span><span class="sxs-lookup"><span data-stu-id="69639-522">Method body and local variables</span></span>

<span data-ttu-id="69639-523">메서드의 본문에는 메서드가 호출 될 때 실행할 문을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-523">A method's body specifies the statements to execute when the method is invoked.</span></span>

<span data-ttu-id="69639-524">메서드 본문은 메서드 호출과 관련된 변수를 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-524">A method body can declare variables that are specific to the invocation of the method.</span></span> <span data-ttu-id="69639-525">이러한 변수를 ***지역 변수***라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-525">Such variables are called ***local variables***.</span></span> <span data-ttu-id="69639-526">지역 변수 선언은 형식 이름, 변수 이름을 지정하며 초기 값을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-526">A local variable declaration specifies a type name, a variable name, and possibly an initial value.</span></span> <span data-ttu-id="69639-527">다음 예제에서는 초기 값이 0인 지역 변수 `i`와 초기 값이 없는 지역 변수 `j`를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-527">The following example declares a local variable `i` with an initial value of zero and a local variable `j` with no initial value.</span></span>

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
<span data-ttu-id="69639-528">C#에서는 해당 값을 얻기 위해 먼저 로컬 변수를 ***명확 하게 할당***해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-528">C# requires a local variable to be ***definitely assigned*** before its value can be obtained.</span></span> <span data-ttu-id="69639-529">예를 들어 이전 `i`의 선언에 초기 값이 포함되지 않으면 컴파일러는 `i`의 후속 사용에 대해 오류를 보고합니다. `i`는 프로그램에서 해당 시점에 명확하게 할당되지 않은 것이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-529">For example, if the declaration of the previous `i` did not include an initial value, the compiler would report an error for the subsequent usages of `i` because `i` would not be definitely assigned at those points in the program.</span></span>

<span data-ttu-id="69639-530">메서드는 `return` 문을 사용하여 해당 호출자에게 컨트롤을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-530">A method can use `return` statements to return control to its caller.</span></span> <span data-ttu-id="69639-531">`void`를 반환하는 메서드에서 `return` 문은 식을 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-531">In a method returning `void`, `return` statements cannot specify an expression.</span></span> <span data-ttu-id="69639-532">메서드에서 반환 이외`void`, `return` 문을 반환 값을 계산 하는 식을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-532">In a method returning non-`void`, `return` statements must include an expression that computes the return value.</span></span>

#### <a name="static-and-instance-methods"></a><span data-ttu-id="69639-533">정적 및 인스턴스 메서드</span><span class="sxs-lookup"><span data-stu-id="69639-533">Static and instance methods</span></span>

<span data-ttu-id="69639-534">메서드를 사용 하 여 선언 된 `static` 한정자가을 ***정적 메서드***합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-534">A method declared with a `static` modifier is a ***static method***.</span></span> <span data-ttu-id="69639-535">정적 메서드는 특정 인스턴스에 작동하지 않고 정적 멤버에 직접적으로만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-535">A static method does not operate on a specific instance and can only directly access static members.</span></span>

<span data-ttu-id="69639-536">없이 선언 된 메서드를 `static` 한정자는 ***인스턴스 메서드***합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-536">A method declared without a `static` modifier is an ***instance method***.</span></span> <span data-ttu-id="69639-537">인스턴스 메서드는 특정 인스턴스에 작동하며 정적 및 인스턴스 멤버 둘 다에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-537">An instance method operates on a specific instance and can access both static and instance members.</span></span> <span data-ttu-id="69639-538">인스턴스 메서드가 호출된 인스턴스는 `this`로 명시적으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-538">The instance on which an instance method was invoked can be explicitly accessed as `this`.</span></span> <span data-ttu-id="69639-539">정적 메서드에서 `this`를 참조하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-539">It is an error to refer to `this` in a static method.</span></span>

<span data-ttu-id="69639-540">다음 `Entity` 클래스에는 정적 멤버와 인스턴스 멤버가 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-540">The following `Entity` class has both static and instance members.</span></span>

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
<span data-ttu-id="69639-541">각 `Entity` 인스턴스에는 일련 번호(및 여기에 표시되지 않는 일부 정보)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-541">Each `Entity` instance contains a serial number (and presumably some other information that is not shown here).</span></span> <span data-ttu-id="69639-542">`Entity` 생성자(인스턴스 메서드와 유사함)는 사용 가능한 다음 일련 번호를 사용하여 새 인스턴스를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-542">The `Entity` constructor (which is like an instance method) initializes the new instance with the next available serial number.</span></span> <span data-ttu-id="69639-543">생성자가 인스턴스 멤버이기 때문에 `serialNo` 인스턴스 필드 및 `nextSerialNo` 정적 필드 둘 다에 액세스하도록 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-543">Because the constructor is an instance member, it is permitted to access both the `serialNo` instance field and the `nextSerialNo` static field.</span></span>

<span data-ttu-id="69639-544">`GetNextSerialNo` 및 `SetNextSerialNo` 정적 메서드는 `nextSerialNo` 정적 필드에 액세스할 수 있지만 `serialNo` 인스턴스 필드에 직접 액세스하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-544">The `GetNextSerialNo` and `SetNextSerialNo` static methods can access the `nextSerialNo` static field, but it would be an error for them to directly access the `serialNo` instance field.</span></span>

<span data-ttu-id="69639-545">다음 예제에서는 사용 된 `Entity` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-545">The following example shows the use of the `Entity` class.</span></span>

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
<span data-ttu-id="69639-546">`SetNextSerialNo` 및 `GetNextSerialNo` 정적 메서드는 클래스에 대해 호출되지만 `GetSerialNo` 인스턴스 메서드는 클래스의 인스턴스에 대해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-546">Note that the `SetNextSerialNo` and `GetNextSerialNo` static methods are invoked on the class whereas the `GetSerialNo` instance method is invoked on instances of the class.</span></span>

#### <a name="virtual-override-and-abstract-methods"></a><span data-ttu-id="69639-547">가상, 재정의 및 추상 메서드</span><span class="sxs-lookup"><span data-stu-id="69639-547">Virtual, override, and abstract methods</span></span>

<span data-ttu-id="69639-548">인스턴스 메서드 선언에 `virtual` 한정자가 포함되면 해당 메서드를 ***가상 메서드***라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-548">When an instance method declaration includes a `virtual` modifier, the method is said to be a ***virtual method***.</span></span> <span data-ttu-id="69639-549">없는 경우 `virtual` 한정자가 있는 메서드를 라고는 ***비가상 메서드***합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-549">When no `virtual` modifier is present, the method is said to be a ***non-virtual method***.</span></span>

<span data-ttu-id="69639-550">가상 메서드가 호출되면 호출이 발생하는 인스턴스의 ***런타임 형식***에 따라 호출할 실제 메서드 구현이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-550">When a virtual method is invoked, the ***run-time type*** of the instance for which that invocation takes place determines the actual method implementation to invoke.</span></span> <span data-ttu-id="69639-551">비가상 메서드 호출에서는 인스턴스의 ***컴파일 타임 형식***이 결정 요인입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-551">In a nonvirtual method invocation, the ***compile-time type*** of the instance is the determining factor.</span></span>

<span data-ttu-id="69639-552">가상 메서드는 파생된 클래스에서 ***재정의***될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-552">A virtual method can be ***overridden*** in a derived class.</span></span> <span data-ttu-id="69639-553">인스턴스 메서드 선언 포함 되는 경우는 `override` 한정자를 메서드 시그니처가 같은 상속된 된 가상 메서드를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-553">When an instance method declaration includes an `override` modifier, the method overrides an inherited virtual method with the same signature.</span></span> <span data-ttu-id="69639-554">가상 메서드 선언은 새 메서드를 도입하지만 재정의 메서드 선언은 해당 메서드의 새 구현을 제공하여 기존의 상속된 가상 메서드를 특수화합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-554">Whereas a virtual method declaration introduces a new method, an override method declaration specializes an existing inherited virtual method by providing a new implementation of that method.</span></span>

<span data-ttu-id="69639-555">***추상*** 메서드는 구현이 없는 가상 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-555">An ***abstract*** method is a virtual method with no implementation.</span></span> <span data-ttu-id="69639-556">추상 메서드를 사용 하 여 선언 되는 `abstract` 한정자를 선언 하는 클래스에만 사용할 수 `abstract`입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-556">An abstract method is declared with the `abstract` modifier and is permitted only in a class that is also declared `abstract`.</span></span> <span data-ttu-id="69639-557">추상 메서드는 모든 비추상 파생 클래스에서 재정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-557">An abstract method must be overridden in every non-abstract derived class.</span></span>

<span data-ttu-id="69639-558">다음 예제에서는 식 트리 노드를 나타내는 추상 클래스 `Expression`와 상수, 변수 참조 및 산술 연산에 대한 식 트리 노드를 구현하는 세 개의 파생 클래스 `Constant`, `VariableReference` 및 `Operation`을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-558">The following example declares an abstract class, `Expression`, which represents an expression tree node, and three derived classes, `Constant`, `VariableReference`, and `Operation`, which implement expression tree nodes for constants, variable references, and arithmetic operations.</span></span> <span data-ttu-id="69639-559">(비슷하지만 이지만에 도입 된 식 트리 형식과와 혼동 해서는 [식 트리 형식](types.md#expression-tree-types)).</span><span class="sxs-lookup"><span data-stu-id="69639-559">(This is similar to, but not to be confused with the expression tree types introduced in [Expression tree types](types.md#expression-tree-types)).</span></span>

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
<span data-ttu-id="69639-560">이전의 4개 클래스는 산술 연산자를 모델링하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-560">The previous four classes can be used to model arithmetic expressions.</span></span> <span data-ttu-id="69639-561">예를 들어 이러한 클래스의 인스턴스를 사용할 경우 식 `x + 3`을 다음과 같이 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-561">For example, using instances of these classes, the expression `x + 3` can be represented as follows.</span></span>

```csharp
Expression e = new Operation(
    new VariableReference("x"),
    '+',
    new Constant(3));
```
<span data-ttu-id="69639-562">`Expression` 인스턴스의 `Evaluate` 메서드는 지정된 식을 계산하고 `double` 값을 생성하기 위해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-562">The `Evaluate` method of an `Expression` instance is invoked to evaluate the given expression and produce a `double` value.</span></span> <span data-ttu-id="69639-563">메서드는 인수로 `Hashtable` 변수 이름 (항목의 키)과 값 (항목의 값)를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-563">The method takes as an argument a `Hashtable` that contains variable names (as keys of the entries) and values (as values of the entries).</span></span> <span data-ttu-id="69639-564">`Evaluate` 메서드는 한 가상 abstract 메서드입니다. 즉, 비추상 파생된 클래스가 실제 구현을 제공 하도록 재정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-564">The `Evaluate` method is a virtual abstract method, meaning that non-abstract derived classes must override it to provide an actual implementation.</span></span>

<span data-ttu-id="69639-565">`Evaluate`의 `Constant` 구현은 단순히 저장된 상수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-565">A `Constant`'s implementation of `Evaluate` simply returns the stored constant.</span></span> <span data-ttu-id="69639-566">`VariableReference`의 구현에서 해시 테이블 변수 이름 조회 하 고 결과 값을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-566">A `VariableReference`'s implementation looks up the variable name in the hashtable and returns the resulting value.</span></span> <span data-ttu-id="69639-567">`Operation`의 구현은 먼저 왼쪽 및 오른쪽 피연산자를 계산하고(재귀적으로 해당 `Evaluate` 메서드 호출) 지정된 산술 연산을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-567">An `Operation`'s implementation first evaluates the left and right operands (by recursively invoking their `Evaluate` methods) and then performs the given arithmetic operation.</span></span>

<span data-ttu-id="69639-568">다음 프로그램에서는 `Expression` 클래스를 사용하여 `x` 및 `y`의 다른 값에 대해 식 `x * (y + 2)`를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-568">The following program uses the `Expression` classes to evaluate the expression `x * (y + 2)` for different values of `x` and `y`.</span></span>

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

#### <a name="method-overloading"></a><span data-ttu-id="69639-569">메서드 오버로드</span><span class="sxs-lookup"><span data-stu-id="69639-569">Method overloading</span></span>

<span data-ttu-id="69639-570">메서드 ***오버로드***는 동일한 클래스가 고유한 시그니처를 갖는 한, 동일한 이름을 갖도록 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-570">Method ***overloading*** permits multiple methods in the same class to have the same name as long as they have unique signatures.</span></span> <span data-ttu-id="69639-571">오버로드된 메서드의 호출을 컴파일할 때 컴파일러는 ***오버로드 확인***을 사용하여 호출할 특정 메서드를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-571">When compiling an invocation of an overloaded method, the compiler uses ***overload resolution*** to determine the specific method to invoke.</span></span> <span data-ttu-id="69639-572">오버로드 확인은 인수와 가장 적합하게 일치하는 단일 메서드를 찾으며, 최상의 일치 메서드를 찾을 수 있는 경우 오류를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-572">Overload resolution finds the one method that best matches the arguments or reports an error if no single best match can be found.</span></span> <span data-ttu-id="69639-573">다음 예제에서는 실제로 진행되는 오버로드 확인을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69639-573">The following example shows overload resolution in effect.</span></span> <span data-ttu-id="69639-574">`Main` 메서드의 각 호출에 대한 주석은 실제로 호출되는 메서드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69639-574">The comment for each invocation in the `Main` method shows which method is actually invoked.</span></span>

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
<span data-ttu-id="69639-575">예제와 같이, 인수를 정확한 매개 변수 형식으로 명시적으로 캐스팅하거나 형식 인수를 명시적으로 제공하여 항상 특정 메서드를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-575">As shown by the example, a particular method can always be selected by explicitly casting the arguments to the exact parameter types and/or explicitly supplying type arguments.</span></span>

### <a name="other-function-members"></a><span data-ttu-id="69639-576">기타 함수 멤버</span><span class="sxs-lookup"><span data-stu-id="69639-576">Other function members</span></span>

<span data-ttu-id="69639-577">실행 코드를 포함하는 멤버를 통칭하여 클래스의 ***함수 멤버***라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-577">Members that contain executable code are collectively known as the ***function members*** of a class.</span></span> <span data-ttu-id="69639-578">이전 섹션에서는 함수 멤버의 기본 종류인 메서드에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-578">The preceding section describes methods, which are the primary kind of function members.</span></span> <span data-ttu-id="69639-579">이 섹션에서는 C#에서 지 원하는 함수 멤버의 다른 종류를 설명 합니다: 생성자, 속성, 인덱서, 이벤트, 연산자 및 소멸자입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-579">This section describes the other kinds of function members supported by C#: constructors, properties, indexers, events, operators, and destructors.</span></span>

<span data-ttu-id="69639-580">다음 코드는 라는 제네릭 클래스를 보여 줍니다. `List<T>`, growable 개체 목록을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-580">The following code shows a generic class called `List<T>`, which implements a growable list of objects.</span></span> <span data-ttu-id="69639-581">이 클래스는 함수 멤버의 가장 일반적인 몇 가지 예제를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-581">The class contains several examples of the most common kinds of function members.</span></span>


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

#### <a name="constructors"></a><span data-ttu-id="69639-582">생성자</span><span class="sxs-lookup"><span data-stu-id="69639-582">Constructors</span></span>

<span data-ttu-id="69639-583">C#은 인스턴스 및 정적 생성자를 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-583">C# supports both instance and static constructors.</span></span> <span data-ttu-id="69639-584">***인스턴스 생성자***는 클래스의 인스턴스를 초기화하는 데 필요한 작업을 구현하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-584">An ***instance constructor*** is a member that implements the actions required to initialize an instance of a class.</span></span> <span data-ttu-id="69639-585">***정적 생성자***는 처음 로드될 때 클래스 자체를 인스턴스화하는 데 필요한 작업을 구현하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-585">A ***static constructor*** is a member that implements the actions required to initialize a class itself when it is first loaded.</span></span>

<span data-ttu-id="69639-586">생성자는 반환 형식이 없고 포함하는 클래스와 동일한 이름을 갖는 메서드처럼 선언됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-586">A constructor is declared like a method with no return type and the same name as the containing class.</span></span> <span data-ttu-id="69639-587">생성자 선언에 포함 된 경우는 `static` 한정자를 정적 생성자를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-587">If a constructor declaration includes a `static` modifier, it declares a static constructor.</span></span> <span data-ttu-id="69639-588">그렇지 않으면 인스턴스 생성자를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-588">Otherwise, it declares an instance constructor.</span></span>

<span data-ttu-id="69639-589">인스턴스 생성자를 오버 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-589">Instance constructors can be overloaded.</span></span> <span data-ttu-id="69639-590">예를 들어 `List<T>
` 클래스는 2개의 인스턴스 생성자, 즉, 매개 변수가 없는 생성자와 `int` 매개 변수를 취하는 생성자를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-590">For example, the `List<T>
` class declares two instance constructors, one with no parameters and one that takes an `int` parameter.</span></span> <span data-ttu-id="69639-591">인스턴스 생성자는 `new` 연산자를 사용하여 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-591">Instance constructors are invoked using the `new` operator.</span></span> <span data-ttu-id="69639-592">다음 문은 두 할당할 `List<string>
` 각각의 생성자를 사용 하 여 인스턴스를 `List` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-592">The following statements allocate two `List<string>
` instances using each of the constructors of the `List` class.</span></span>

```csharp
List<string> list1 = new List<string>();
List<string> list2 = new List<string>(10);
```
<span data-ttu-id="69639-593">다른 멤버와 달리 인스턴스 생성자는 상속되지 않으며 클래스에는 클래스에서 실제로 선언된 인스턴스 생성자만 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-593">Unlike other members, instance constructors are not inherited, and a class has no instance constructors other than those actually declared in the class.</span></span> <span data-ttu-id="69639-594">클래스에 대해 인스턴스 생성자가 제공되지 않으면 매개 변수가 없는 빈 인스턴스 생성자가 자동으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-594">If no instance constructor is supplied for a class, then an empty one with no parameters is automatically provided.</span></span>

#### <a name="properties"></a><span data-ttu-id="69639-595">속성</span><span class="sxs-lookup"><span data-stu-id="69639-595">Properties</span></span>

<span data-ttu-id="69639-596">***속성***은 필드의 기본 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-596">***Properties*** are a natural extension of fields.</span></span> <span data-ttu-id="69639-597">둘 다 연결된 형식으로 명명되는 멤버이며, 필드 및 속성에 액세스하는 구문은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-597">Both are named members with associated types, and the syntax for accessing fields and properties is the same.</span></span> <span data-ttu-id="69639-598">그러나 필드와 달리 속성은 저장 위치를 명시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-598">However, unlike fields, properties do not denote storage locations.</span></span> <span data-ttu-id="69639-599">대신, 속성에는 해당 값을 읽거나 쓸 때 실행될 문을 지정하는 ***접근자***가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-599">Instead, properties have ***accessors*** that specify the statements to be executed when their values are read or written.</span></span>

<span data-ttu-id="69639-600">속성 선언 끝나는 제외 하 고 필드 처럼 선언 됩니다는 `get` 접근자 및/또는 `set` 구분 기호 사이 기록 된 접근자 `{` 및 `}` 세미콜론으로 종료 하는 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-600">A property is declared like a field, except that the declaration ends with a `get` accessor and/or a `set` accessor written between the delimiters `{` and `}` instead of ending in a semicolon.</span></span> <span data-ttu-id="69639-601">둘 다 포함 된 속성을 `get` 접근자 및 `set` 접근자가는 ***읽기 / 쓰기 속성***만 있는 속성을 `get` 접근자가를 ***읽기 전용 속성***, 및 만 있는 속성을 `set` 접근자를 ***쓰기 전용 속성***합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-601">A property that has both a `get` accessor and a `set` accessor is a ***read-write property***, a property that has only a `get` accessor is a ***read-only property***, and a property that has only a `set` accessor is a ***write-only property***.</span></span>

<span data-ttu-id="69639-602">`get` 접근자는 속성 형식의 반환 값을 사용 하 여 매개 변수가 없는 메서드에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-602">A `get` accessor corresponds to a parameterless method with a return value of the property type.</span></span> <span data-ttu-id="69639-603">속성 식에서 참조 될 때 할당의 대상으로 제외 하 고는 `get` 속성의 접근자 속성의 값을 계산 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-603">Except as the target of an assignment, when a property is referenced in an expression, the `get` accessor of the property is invoked to compute the value of the property.</span></span>

<span data-ttu-id="69639-604">A `set` 라는 단일 매개 변수를 사용 하 여 메서드에 해당 하는 접근자 `value` 및 반환 형식이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-604">A `set` accessor corresponds to a method with a single parameter named `value` and no return type.</span></span> <span data-ttu-id="69639-605">속성의 피연산자 또는 할당의 대상으로 참조 되는 경우 `++` 나 `--`, `set` 접근자가 새 값을 제공 하는 인수를 사용 하 여 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-605">When a property is referenced as the target of an assignment or as the operand of `++` or `--`, the `set` accessor is invoked with an argument that provides the new value.</span></span>

<span data-ttu-id="69639-606">`List<T>
` 클래스에는 두 개의 속성 선언 `Count` 및 `Capacity`는 읽기 전용 및 읽기 / 쓰기, 각각.</span><span class="sxs-lookup"><span data-stu-id="69639-606">The `List<T>
` class declares two properties, `Count` and `Capacity`, which are read-only and read-write, respectively.</span></span> <span data-ttu-id="69639-607">다음은 이러한 속성 사용의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-607">The following is an example of use of these properties.</span></span>

```csharp
List<string> names = new List<string>();
names.Capacity = 100;            // Invokes set accessor
int i = names.Count;             // Invokes get accessor
int j = names.Capacity;          // Invokes get accessor
```
<span data-ttu-id="69639-608">필드 및 메서드와 마찬가지로, C#은 인스턴스 속성 및 정적 속성을 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-608">Similar to fields and methods, C# supports both instance properties and static properties.</span></span> <span data-ttu-id="69639-609">정적 속성으로 선언 되는 `static` 한정자와 인스턴스 속성 없이 선언 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-609">Static properties are declared with the `static` modifier, and instance properties are declared without it.</span></span>

<span data-ttu-id="69639-610">속성의 접근자는 가상일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-610">The accessor(s) of a property can be virtual.</span></span> <span data-ttu-id="69639-611">속성 선언에 `virtual`, `abstract`, 또는 `override` 한정자가 포함되면 속성의 접근자에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-611">When a property declaration includes a `virtual`, `abstract`, or `override` modifier, it applies to the accessor(s) of the property.</span></span>

#### <a name="indexers"></a><span data-ttu-id="69639-612">인덱서</span><span class="sxs-lookup"><span data-stu-id="69639-612">Indexers</span></span>

<span data-ttu-id="69639-613">***인덱서***는 개체가 배열과 같은 방식으로 인덱싱될 수 있도록 하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-613">An ***indexer*** is a member that enables objects to be indexed in the same way as an array.</span></span> <span data-ttu-id="69639-614">인덱서는이 멤버의 이름을 제외 하 고 속성 처럼 선언 됩니다 `this` 구분 기호 사이 기록 된 매개 변수 목록 뒤 `[` 고 `]`입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-614">An indexer is declared like a property except that the name of the member is `this` followed by a parameter list written between the delimiters `[` and `]`.</span></span> <span data-ttu-id="69639-615">매개 변수는 인덱서의 접근자에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-615">The parameters are available in the accessor(s) of the indexer.</span></span> <span data-ttu-id="69639-616">속성과 마찬가지로 인덱서는 읽기/쓰기, 읽기 전용 및 쓰기 전용일 수 있으며 인덱서의 접근자는 가상일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-616">Similar to properties, indexers can be read-write, read-only, and write-only, and the accessor(s) of an indexer can be virtual.</span></span>

<span data-ttu-id="69639-617">`List` 클래스는 `int` 매개 변수를 사용하는 단일 읽기/쓰기 인덱서를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-617">The `List` class declares a single read-write indexer that takes an `int` parameter.</span></span> <span data-ttu-id="69639-618">인덱서는 `List` 인스턴스를 `int` 값으로 인덱싱할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-618">The indexer makes it possible to index `List` instances with `int` values.</span></span> <span data-ttu-id="69639-619">예</span><span class="sxs-lookup"><span data-stu-id="69639-619">For example</span></span>

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
<span data-ttu-id="69639-620">인덱서는 오버로드될 수 있습니다. 즉, 해당 매개 변수의 수와 형식이 다를 경우 한 클래스가 여러 인덱서를 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-620">Indexers can be overloaded, meaning that a class can declare multiple indexers as long as the number or types of their parameters differ.</span></span>

#### <a name="events"></a><span data-ttu-id="69639-621">이벤트</span><span class="sxs-lookup"><span data-stu-id="69639-621">Events</span></span>

<span data-ttu-id="69639-622">***이벤트***는 클래스 또는 개체가 알림을 제공할 수 있도록 하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-622">An ***event*** is a member that enables a class or object to provide notifications.</span></span> <span data-ttu-id="69639-623">이벤트 선언을 포함 된다는 점을 제외 하 고 필드 처럼 선언 됩니다는 `event` 키워드 및 형식에는 대리자 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-623">An event is declared like a field except that the declaration includes an `event` keyword and the type must be a delegate type.</span></span>

<span data-ttu-id="69639-624">이벤트 멤버를 선언하는 클래스 내에서 이벤트는 대리자 형식의 필드처럼 동작합니다(이벤트가 추상이 아니고 접근자를 선언하지 않을 경우).</span><span class="sxs-lookup"><span data-stu-id="69639-624">Within a class that declares an event member, the event behaves just like a field of a delegate type (provided the event is not abstract and does not declare accessors).</span></span> <span data-ttu-id="69639-625">필드는 이벤트에 추가된 이벤트 처리기를 나타내는 대리자에 대한 참조를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-625">The field stores a reference to a delegate that represents the event handlers that have been added to the event.</span></span> <span data-ttu-id="69639-626">필드는 이벤트 핸들이 없는 경우 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-626">If no event handles are present, the field is `null`.</span></span>

<span data-ttu-id="69639-627">`List<T>
` 클래스는 `Changed`라는 단일 이벤트 멤버를 선언합니다. 이것은 새 항목이 목록에 추가되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="69639-627">The `List<T>
` class declares a single event member called `Changed`, which indicates that a new item has been added to the list.</span></span> <span data-ttu-id="69639-628">합니다 `Changed` 이벤트를 발생 합니다 `OnChanged` 는 첫 번째 이벤트 인지를 확인 하는 가상 메서드를 `null` (처리기가 있는 것을 의미).</span><span class="sxs-lookup"><span data-stu-id="69639-628">The `Changed` event is raised by the `OnChanged` virtual method, which first checks whether the event is `null` (meaning that no handlers are present).</span></span> <span data-ttu-id="69639-629">이벤트 발생 개념은 이벤트가 나타내는 대리자를 호출하는 것과 정확히 동일하므로 이벤트 발생을 위한 특수한 언어 구문은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-629">The notion of raising an event is precisely equivalent to invoking the delegate represented by the event—thus, there are no special language constructs for raising events.</span></span>

<span data-ttu-id="69639-630">클라이언트는 ***이벤트 처리기***를 통해 이벤트에 반응합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-630">Clients react to events through ***event handlers***.</span></span> <span data-ttu-id="69639-631">이벤트 처리기는 `+=` 연산자를 사용하여 추가되고, `-=` 연산자를 사용하여 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-631">Event handlers are attached using the `+=` operator and removed using the `-=` operator.</span></span> <span data-ttu-id="69639-632">다음 예제에서는 이벤트 처리기를 `List<string>
`의 `Changed` 이벤트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-632">The following example attaches an event handler to the `Changed` event of a `List<string>
`.</span></span>

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
<span data-ttu-id="69639-633">이벤트의 기본 저장소를 제어하려고 하는 고급 시나리오의 경우 이벤트 선언에서 속성의 `set` 접근자와 비슷한 `add` 및 `remove` 접근자를 명시적으로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-633">For advanced scenarios where control of the underlying storage of an event is desired, an event declaration can explicitly provide `add` and `remove` accessors, which are somewhat similar to the `set` accessor of a property.</span></span>

#### <a name="operators"></a><span data-ttu-id="69639-634">연산자</span><span class="sxs-lookup"><span data-stu-id="69639-634">Operators</span></span>

<span data-ttu-id="69639-635">***연산자***는 클래스 인스턴스에 특정 식 연산자를 적용하는 것의 의미를 정의하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-635">An ***operator*** is a member that defines the meaning of applying a particular expression operator to instances of a class.</span></span> <span data-ttu-id="69639-636">세 가지 종류의 연산자, 즉, 단항 연산자, 이항 연산자 및 변환 연산자를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-636">Three kinds of operators can be defined: unary operators, binary operators, and conversion operators.</span></span> <span data-ttu-id="69639-637">모든 연산자는 `public` 및 `static`으로 선언해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-637">All operators must be declared as `public` and `static`.</span></span>

<span data-ttu-id="69639-638">`List<T>
` 클래스는 두 가지 연산자인 `operator==` 및 `operator!=`를 선언하므로 해당 연산자를 `List` 인스턴스에 적용하는 새로운 의미를 식에 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-638">The `List<T>
` class declares two operators, `operator==` and `operator!=`, and thus gives new meaning to expressions that apply those operators to `List` instances.</span></span> <span data-ttu-id="69639-639">연산자에서 두 개의 일치를 정의 하는 특히 `List<T>
` 비교를 사용 하 여 포함 된 개체는 각각의 인스턴스로 해당 `Equals` 메서드.</span><span class="sxs-lookup"><span data-stu-id="69639-639">Specifically, the operators define equality of two `List<T>
` instances as comparing each of the contained objects using their `Equals` methods.</span></span> <span data-ttu-id="69639-640">다음 예제에서는 `==` 연산자를 사용하여 두 `List<int>
` 인스턴스를 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-640">The following example uses the `==` operator to compare two `List<int>
` instances.</span></span>

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

<span data-ttu-id="69639-641">두 목록은 같은 순서로 같은 값을 갖는 동일한 수의 개체를 포함하므로 첫 번째 `Console.WriteLine`은 `True`를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-641">The first `Console.WriteLine` outputs `True` because the two lists contain the same number of objects with the same values in the same order.</span></span> <span data-ttu-id="69639-642">`List<T>
`에서 `operator==`이 정의되지 않았으면 `a` 및 `b`은 다른 `List<int>
` 인스턴스를 참조하므로 첫 번째 `Console.WriteLine`은 `False`를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-642">Had `List<T>
` not defined `operator==`, the first `Console.WriteLine` would have output `False` because `a` and `b` reference different `List<int>
` instances.</span></span>

#### <a name="destructors"></a><span data-ttu-id="69639-643">소멸자</span><span class="sxs-lookup"><span data-stu-id="69639-643">Destructors</span></span>

<span data-ttu-id="69639-644">A ***소멸자*** 는 클래스의 인스턴스를 소멸 하는 데 필요한 작업을 구현 하는 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-644">A ***destructor*** is a member that implements the actions required to destruct an instance of a class.</span></span> <span data-ttu-id="69639-645">소멸자는 매개 변수를 사용할 수 없습니다, 액세스 가능성 한정자를 가질 수 없습니다 및 명시적으로 호출할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-645">Destructors cannot have parameters, they cannot have accessibility modifiers, and they cannot be invoked explicitly.</span></span> <span data-ttu-id="69639-646">인스턴스에 대 한 소멸자는 가비지 수집 중 자동으로 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-646">The destructor for an instance is invoked automatically during garbage collection.</span></span>

<span data-ttu-id="69639-647">가비지 수집기는 유연 하 게 결정할 개체를 수집 하 고 소멸자를 실행 하는 경우 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-647">The garbage collector is allowed wide latitude in deciding when to collect objects and run destructors.</span></span> <span data-ttu-id="69639-648">특히 소멸자 호출의 타이밍 결정적 아니며 모든 스레드에서 소멸자를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-648">Specifically, the timing of destructor invocations is not deterministic, and destructors may be executed on any thread.</span></span> <span data-ttu-id="69639-649">이러한 및 기타 이유로 클래스는 가능한 다른 솔루션이 없는 경우에 소멸자를 구현 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-649">For these and other reasons, classes should implement destructors only when no other solutions are feasible.</span></span>

<span data-ttu-id="69639-650">`using` 문은 개체 소멸을 위한 더 나은 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-650">The `using` statement provides a better approach to object destruction.</span></span>

## <a name="structs"></a><span data-ttu-id="69639-651">구조체</span><span class="sxs-lookup"><span data-stu-id="69639-651">Structs</span></span>

<span data-ttu-id="69639-652">***구조체***는 클래스처럼 데이터 멤버 및 함수 멤버를 포함할 수 있는 데이터 구조이지만 값 형식이며 힙 할당이 필요하지 않다는 점이 클래스와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="69639-652">Like classes, ***structs*** are data structures that can contain data members and function members, but unlike classes, structs are value types and do not require heap allocation.</span></span> <span data-ttu-id="69639-653">구조체 형식의 변수는 구조체의 데이터를 직접 저장하지만 클래스 형식의 변수는 동적으로 할당된 개체에 대한 참조를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-653">A variable of a struct type directly stores the data of the struct, whereas a variable of a class type stores a reference to a dynamically allocated object.</span></span> <span data-ttu-id="69639-654">구조체 형식은 사용자 지정 상속을 지원하지 않으며 모든 구조체 형식은 `object` 형식에서 암시적으로 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-654">Struct types do not support user-specified inheritance, and all struct types implicitly inherit from type `object`.</span></span>

<span data-ttu-id="69639-655">구조체는 값 의미 체계를 갖는 작은 데이터 구조에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-655">Structs are particularly useful for small data structures that have value semantics.</span></span> <span data-ttu-id="69639-656">복소수, 좌표계의 점 또는 사전의 키-값 쌍이 모두 구조체의 좋은 예입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-656">Complex numbers, points in a coordinate system, or key-value pairs in a dictionary are all good examples of structs.</span></span> <span data-ttu-id="69639-657">작은 데이터 구조에 클래스 대신 구조체를 사용하는 것은 응용 프로그램이 사용하는 메모리 할당 수에서 큰 차이를 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-657">The use of structs rather than classes for small data structures can make a large difference in the number of memory allocations an application performs.</span></span> <span data-ttu-id="69639-658">예를 들어 다음 프로그램은 100개의 점 배열을 만들고 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-658">For example, the following program creates and initializes an array of 100 points.</span></span> <span data-ttu-id="69639-659">`Point`가 클래스로 구현될 경우 배열에 대해 1개, 100개 요소에 대해 각각 1개씩 101개의 별도 개체가 인스턴스화됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-659">With `Point` implemented as a class, 101 separate objects are instantiated—one for the array and one each for the 100 elements.</span></span>

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
<span data-ttu-id="69639-660">대안은 있도록 `Point` 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-660">An alternative is to make `Point` a struct.</span></span>

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
<span data-ttu-id="69639-661">이제 1개의 개체만 인스턴스화되고(배열에 대해 1개) `Point` 인스턴스는 배열에 인라인으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-661">Now, only one object is instantiated—the one for the array—and the `Point` instances are stored in-line in the array.</span></span>

<span data-ttu-id="69639-662">구조체 생성자는 `new` 연산자로 호출되지만 메모리가 할당된다는 것을 의미하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-662">Struct constructors are invoked with the `new` operator, but that does not imply that memory is being allocated.</span></span> <span data-ttu-id="69639-663">개체를 동적으로 할당하고 그에 대한 참조를 반환하는 대신, 구조체 생성자는 단순히 구조체 값 자체(일반적으로 스택의 임시 위치에 있음)를 반환하며 이 값은 필요할 때 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-663">Instead of dynamically allocating an object and returning a reference to it, a struct constructor simply returns the struct value itself (typically in a temporary location on the stack), and this value is then copied as necessary.</span></span>

<span data-ttu-id="69639-664">클래스에서는 두 가지 변수가 같은 개체를 참조할 수 있으므로 한 변수에 대한 작업이 다른 변수에서 참조하는 개체에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-664">With classes, it is possible for two variables to reference the same object and thus possible for operations on one variable to affect the object referenced by the other variable.</span></span> <span data-ttu-id="69639-665">구조체에서는 변수 각각에 데이터의 자체 사본이 들어 있으며 한 변수의 작업이 다른 변수에 영향을 미칠 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-665">With structs, the variables each have their own copy of the data, and it is not possible for operations on one to affect the other.</span></span> <span data-ttu-id="69639-666">예를 들어, 다음 코드 조각에서 생성 된 출력 종속 여부 `Point` 가 클래스 또는 구조체입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-666">For example, the output produced by the following code fragment depends on whether `Point` is a class or a struct.</span></span>

```csharp
Point a = new Point(10, 10);
Point b = a;
a.x = 20;
Console.WriteLine(b.x);
```
<span data-ttu-id="69639-667">경우 `Point` 클래스는 출력은 `20` 있으므로 `a` 및 `b` 동일한 개체를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-667">If `Point` is a class, the output is `20` because `a` and `b` reference the same object.</span></span> <span data-ttu-id="69639-668">경우 `Point` 는 구조체, 출력은 `10` 때문에 할당 `a` 하 `b` 값의 복사본을 만듭니다이 복사본의 후속 대입에 의해 영향을 받지 않습니다. 및 `a.x`합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-668">If `Point` is a struct, the output is `10` because the assignment of `a` to `b` creates a copy of the value, and this copy is unaffected by the subsequent assignment to `a.x`.</span></span>

<span data-ttu-id="69639-669">이전 예제에는 구조체의 제한 사항 중 두 가지를 집중적으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69639-669">The previous example highlights two of the limitations of structs.</span></span> <span data-ttu-id="69639-670">첫째, 일반적으로 전체 구조체를 복사하는 것이 개체 참조를 복사하는 것보다 덜 효율적이므로 대입 및 값 매개 변수 전달이 참조 형식보다 덜 경제적일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-670">First, copying an entire struct is typically less efficient than copying an object reference, so assignment and value parameter passing can be more expensive with structs than with reference types.</span></span> <span data-ttu-id="69639-671">둘째, `ref` 및 `out` 매개 변수를 제외하고, 구조체에 대한 참조를 만들 수 없으므로 다양한 상황에서 사용하는 것이 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-671">Second, except for `ref` and `out` parameters, it is not possible to create references to structs, which rules out their usage in a number of situations.</span></span>

## <a name="arrays"></a><span data-ttu-id="69639-672">배열</span><span class="sxs-lookup"><span data-stu-id="69639-672">Arrays</span></span>

<span data-ttu-id="69639-673">***배열***은 계산된 인덱스를 통해 액세스되는 여러 변수를 포함하는 데이터 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-673">An ***array*** is a data structure that contains a number of variables that are accessed through computed indices.</span></span> <span data-ttu-id="69639-674">배열에 포함된 변수, 즉 배열의 ***요소***라고도 하는 배열은 모두 같은 형식이며, 이 형식을 배열의 ***요소 형식***이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-674">The variables contained in an array, also called the ***elements*** of the array, are all of the same type, and this type is called the ***element type*** of the array.</span></span>

<span data-ttu-id="69639-675">배열 형식은 참조 형식이고 배열 변수의 선언은 배열 인스턴스에 대한 참조를 위한 공간을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-675">Array types are reference types, and the declaration of an array variable simply sets aside space for a reference to an array instance.</span></span> <span data-ttu-id="69639-676">실제 배열 인스턴스는 런타임에 사용 하 여 동적으로 생성 됩니다는 `new` 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-676">Actual array instances are created dynamically at run-time using the `new` operator.</span></span> <span data-ttu-id="69639-677">합니다 `new` 작업을 지정 합니다 ***길이*** 인스턴스의 새 배열 인스턴스의 수명 동안 고정 됨.</span><span class="sxs-lookup"><span data-stu-id="69639-677">The `new` operation specifies the ***length*** of the new array instance, which is then fixed for the lifetime of the instance.</span></span> <span data-ttu-id="69639-678">배열 요소의 인덱스 범위는 `0`에서 `Length - 1` 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-678">The indices of the elements of an array range from `0` to `Length - 1`.</span></span> <span data-ttu-id="69639-679">`new` 연산자는 배열의 요소를 모든 숫자 형식에 대해 0이고, 모든 참조 형식에 대해 `null`인 기본값으로 자동으로 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-679">The `new` operator automatically initializes the elements of an array to their default value, which, for example, is zero for all numeric types and `null` for all reference types.</span></span>

<span data-ttu-id="69639-680">다음 예제에서는 `int` 요소의 배열을 만들고, 배열을 초기화하고, 배열의 콘텐츠를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-680">The following example creates an array of `int` elements, initializes the array, and prints out the contents of the array.</span></span>

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
<span data-ttu-id="69639-681">이 예제에서는 ***1차원 배열***을 만들고 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-681">This example creates and operates on a ***single-dimensional array***.</span></span> <span data-ttu-id="69639-682">C#에서는 ***다차원 배열s***을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-682">C# also supports ***multi-dimensional arrays***.</span></span> <span data-ttu-id="69639-683">배열 형식의 ***순위***라고도 하는 배열 형식의 차원 수는 배열 형식의 대괄호 사이에 사용된 쉼표 수에 1을 더한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-683">The number of dimensions of an array type, also known as the ***rank*** of the array type, is one plus the number of commas written between the square brackets of the array type.</span></span> <span data-ttu-id="69639-684">다음 예제에서는 1 차원, 2 차원 및 3 차원 배열을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-684">The following example allocates a one-dimensional, a two-dimensional, and a three-dimensional array.</span></span>

```csharp
int[] a1 = new int[10];
int[,] a2 = new int[10, 5];
int[,,] a3 = new int[10, 5, 2];
```
<span data-ttu-id="69639-685">`a1` 배열에는 10개의 요소가 들어 있고 `a2` 배열에는 50(10 × 5)개의 요소가 들어 있고 `a3` 배열에는 100(10 × 5 × 2)개 요소가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-685">The `a1` array contains 10 elements, the `a2` array contains 50 (10 × 5) elements, and the `a3` array contains 100 (10 × 5 × 2) elements.</span></span>

<span data-ttu-id="69639-686">배열의 요소 형식은 배열 형식을 비롯한 어떤 형식도 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-686">The element type of an array can be any type, including an array type.</span></span> <span data-ttu-id="69639-687">배열 형식의 요소가 있는 배열을 ***가변 배열***이라고도 합니다. 요소 배열의 길이가 항상 동일할 필요는 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-687">An array with elements of an array type is sometimes called a ***jagged array*** because the lengths of the element arrays do not all have to be the same.</span></span> <span data-ttu-id="69639-688">다음 예제에서는 `int` 배열의 배열을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-688">The following example allocates an array of arrays of `int`:</span></span>

```csharp
int[][] a = new int[3][];
a[0] = new int[10];
a[1] = new int[5];
a[2] = new int[20];
```
<span data-ttu-id="69639-689">첫 번째 줄은 형식이 `int[]`이고 초기 값이 `null`인 3개 요소가 있는 배열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69639-689">The first line creates an array with three elements, each of type `int[]` and each with an initial value of `null`.</span></span> <span data-ttu-id="69639-690">다음 줄은 가변 길이의 개별 배열 인스턴스에 대한 참조로 3개 요소를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-690">The subsequent lines then initialize the three elements with references to individual array instances of varying lengths.</span></span>

<span data-ttu-id="69639-691">합니다 `new` 연산자를 사용 하 여 배열 요소의 초기 값을 허용을 ***배열 이니셜라이저***, 구분 기호 사이 기록 된 식의 목록입니다 `{` 및 `}`합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-691">The `new` operator permits the initial values of the array elements to be specified using an ***array initializer***, which is a list of expressions written between the delimiters `{` and `}`.</span></span> <span data-ttu-id="69639-692">다음 예제에서는 3개 요소로 `int[]`를 할당하고 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-692">The following example allocates and initializes an `int[]` with three elements.</span></span>

```csharp
int[] a = new int[] {1, 2, 3};
```
<span data-ttu-id="69639-693">배열의 길이 사이의 식 수에서 유추 되 `{` 고 `}`입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-693">Note that the length of the array is inferred from the number of expressions between `{` and `}`.</span></span> <span data-ttu-id="69639-694">지역 변수 및 필드 선언은 배열 형식을 다시 시작할 필요가 없도록 좀 더 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-694">Local variable and field declarations can be shortened further such that the array type does not have to be restated.</span></span>

```csharp
int[] a = {1, 2, 3};
```
<span data-ttu-id="69639-695">앞의 두 예제는 다음 예제와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-695">Both of the previous examples are equivalent to the following:</span></span>

```csharp
int[] t = new int[3];
t[0] = 1;
t[1] = 2;
t[2] = 3;
int[] a = t;
```
## <a name="interfaces"></a><span data-ttu-id="69639-696">인터페이스</span><span class="sxs-lookup"><span data-stu-id="69639-696">Interfaces</span></span>

<span data-ttu-id="69639-697">***인터페이스***는 클래스 및 구조체에서 구현될 수 있는 계약을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-697">An ***interface*** defines a contract that can be implemented by classes and structs.</span></span> <span data-ttu-id="69639-698">인터페이스는 메서드, 속성, 이벤트 및 인덱서를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-698">An interface can contain methods, properties, events, and indexers.</span></span> <span data-ttu-id="69639-699">인터페이스는 정의하는 멤버의 구현을 제공하지 않으며 단순히 인터페이스를 구현하는 클래스 또는 구조체에서 제공해야 하는 멤버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-699">An interface does not provide implementations of the members it defines—it merely specifies the members that must be supplied by classes or structs that implement the interface.</span></span>

<span data-ttu-id="69639-700">인터페이스는 ***다중 상속***을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-700">Interfaces may employ ***multiple inheritance***.</span></span> <span data-ttu-id="69639-701">다음 예제에서 인터페이스 `IComboBox`는 `ITextBox` 및 `IListBox`를 둘 다 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-701">In the following example, the interface `IComboBox` inherits from both `ITextBox` and `IListBox`.</span></span>

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
<span data-ttu-id="69639-702">클래스 및 구조체는 여러 인터페이스를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-702">Classes and structs can implement multiple interfaces.</span></span> <span data-ttu-id="69639-703">다음 예제에서 클래스 `EditBox`는 `IControl` 및 `IDataBound`를 둘 다 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-703">In the following example, the class `EditBox` implements both `IControl` and `IDataBound`.</span></span>

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
<span data-ttu-id="69639-704">클래스 또는 구조체가 특정 인터페이스를 구현하는 경우 해당 클래스 또는 구조체의 인스턴스를 해당 인터페이스 형식으로 암시적으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-704">When a class or struct implements a particular interface, instances of that class or struct can be implicitly converted to that interface type.</span></span> <span data-ttu-id="69639-705">예</span><span class="sxs-lookup"><span data-stu-id="69639-705">For example</span></span>

```csharp
EditBox editBox = new EditBox();
IControl control = editBox;
IDataBound dataBound = editBox;
```
<span data-ttu-id="69639-706">인스턴스가 정적으로 특정 인터페이스를 구현하는 것으로 알려지지 않은 경우 동적 형식 캐스팅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-706">In cases where an instance is not statically known to implement a particular interface, dynamic type casts can be used.</span></span> <span data-ttu-id="69639-707">다음 문은 개체를 가져오려면 동적 형식 캐스팅을 사용 하는 예를 들어 `IControl` 고 `IDataBound` 인터페이스 구현.</span><span class="sxs-lookup"><span data-stu-id="69639-707">For example, the following statements use dynamic type casts to obtain an object's `IControl` and `IDataBound` interface implementations.</span></span> <span data-ttu-id="69639-708">개체의 실제 형식 이므로 `EditBox`, 캐스팅은 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-708">Because the actual type of the object is `EditBox`, the casts succeed.</span></span>

```csharp
object obj = new EditBox();
IControl control = (IControl)obj;
IDataBound dataBound = (IDataBound)obj;
```
<span data-ttu-id="69639-709">이전 `EditBox` 클래스를 `Paint` 메서드에서 `IControl` 인터페이스 및 `Bind` 메서드를 `IDataBound` 인터페이스를 사용 하 여 구현 됩니다 `public` 멤버입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-709">In the previous `EditBox` class, the `Paint` method from the `IControl` interface and the `Bind` method from the `IDataBound` interface are implemented using `public` members.</span></span> <span data-ttu-id="69639-710">또한 C# 지원 ***명시적 인터페이스 멤버 구현을***, 클래스를 사용 하는 구조체 구성원 작업을 방지할 수 또는 `public`합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-710">C# also supports ***explicit interface member implementations***, using which the class or struct can avoid making the members `public`.</span></span> <span data-ttu-id="69639-711">명시적 인터페이스 멤버 구현은 정규화된 인터페이스 멤버 이름을 사용하여 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-711">An explicit interface member implementation is written using the fully qualified interface member name.</span></span> <span data-ttu-id="69639-712">예를 들어 `EditBox` 클래스는 다음과 같이 명시적 인터페이스 멤버 구현을 사용하여 `IControl.Paint` 및 `IDataBound.Bind` 메서드를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-712">For example, the `EditBox` class could implement the `IControl.Paint` and `IDataBound.Bind` methods using explicit interface member implementations as follows.</span></span>

```csharp
public class EditBox: IControl, IDataBound
{
    void IControl.Paint() {...}
    void IDataBound.Bind(Binder b) {...}
}
```
<span data-ttu-id="69639-713">명시적 인터페이스 멤버는 인터페이스 형식을 통해서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-713">Explicit interface members can only be accessed via the interface type.</span></span> <span data-ttu-id="69639-714">구현의 예를 들어 `IControl.Paint` 이전 제공한 `EditBox` 클래스 에서만 사용 하 여 호출할 수는 `EditBox` 에 대 한 참조를 `IControl` 인터페이스 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-714">For example, the implementation of `IControl.Paint` provided by the previous `EditBox` class can only be invoked by first converting the `EditBox` reference to the `IControl` interface type.</span></span>

```csharp
EditBox editBox = new EditBox();
editBox.Paint();                        // Error, no such method
IControl control = editBox;
control.Paint();                        // Ok
```

## <a name="enums"></a><span data-ttu-id="69639-715">열거형</span><span class="sxs-lookup"><span data-stu-id="69639-715">Enums</span></span>

<span data-ttu-id="69639-716">***열거형 형식***은 명명된 상수 집합을 갖는 고유 값 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-716">An ***enum type*** is a distinct value type with a set of named constants.</span></span> <span data-ttu-id="69639-717">다음 예제에서는 선언 하 고 명명 된 열거형 형식을 사용 합니다. `Color` 세 개의 상수 값을 사용 하 여 `Red`를 `Green`, 및 `Blue`합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-717">The following example declares and uses an enum type named `Color` with three constant values, `Red`, `Green`, and `Blue`.</span></span>

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
<span data-ttu-id="69639-718">각 열거형 형식이 정수 계열 형식이 호출에 ***내부 형식*** 열거형 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-718">Each enum type has a corresponding integral type called the ***underlying type*** of the enum type.</span></span> <span data-ttu-id="69639-719">내부 형식을 명시적으로 선언 하지 않는 열거형 형식에 기본 형식 `int`합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-719">An enum type that does not explicitly declare an underlying type has an underlying type of `int`.</span></span> <span data-ttu-id="69639-720">열거형 형식의 저장소 형식 및 가능한 값의 범위는 해당 기본 형식에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-720">An enum type's storage format and range of possible values are determined by its underlying type.</span></span> <span data-ttu-id="69639-721">열거형 형식에 사용할 수 있는 값의 집합은은 열거형 멤버에 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-721">The set of values that an enum type can take on is not limited by its enum members.</span></span> <span data-ttu-id="69639-722">특히 열거형의 기본 형식의 모든 값은 열거형 형식으로 캐스팅 될 수 이며 해당 열거형의 유효한 고유 값.</span><span class="sxs-lookup"><span data-stu-id="69639-722">In particular, any value of the underlying type of an enum can be cast to the enum type and is a distinct valid value of that enum type.</span></span>

<span data-ttu-id="69639-723">다음 예제에서는 명명 된 열거형 형식을 선언 `Alignment` 기본 유형으로 `sbyte`입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-723">The following example declares an enum type named `Alignment` with an underlying type of `sbyte`.</span></span>

```csharp
enum Alignment: sbyte
{
    Left = -1,
    Center = 0,
    Right = 1
}
```
<span data-ttu-id="69639-724">앞의 예제에서와 같이 열거형 멤버 선언에는 멤버의 값을 지정 하는 상수 식을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-724">As shown by the previous example, an enum member declaration can include a constant expression that specifies the value of the member.</span></span> <span data-ttu-id="69639-725">각 열거형 멤버에 대 한 상수 값을 열거형의 내부 형식 범위에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-725">The constant value for each enum member must be in the range of the underlying type of the enum.</span></span> <span data-ttu-id="69639-726">열거형 멤버 선언 값을 명시적으로 지정 하지 않으면, 0 (열거형 형식에서 첫 번째 멤버 경우) 값 또는 텍스트가 앞에 있는 열거형 멤버는 1을 더한 값 멤버 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-726">When an enum member declaration does not explicitly specify a value, the member is given the value zero (if it is the first member in the enum type) or the value of the textually preceding enum member plus one.</span></span>

<span data-ttu-id="69639-727">열거형 값을 정수로 변환 된 값과 반대로 캐스트를 사용 하 여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-727">Enum values can be converted to integral values and vice versa using type casts.</span></span> <span data-ttu-id="69639-728">예</span><span class="sxs-lookup"><span data-stu-id="69639-728">For example</span></span>

```csharp
int i = (int)Color.Blue;        // int i = 2;
Color c = (Color)2;             // Color c = Color.Blue;
```
<span data-ttu-id="69639-729">모든 열거형 형식의 기본 값은 정수 계열 값 0은 열거형 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-729">The default value of any enum type is the integral value zero converted to the enum type.</span></span> <span data-ttu-id="69639-730">여기서 변수는 자동으로 기본값으로 초기화 하는 경우에서 열거형 형식의 변수를 지정 된 값입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-730">In cases where variables are automatically initialized to a default value, this is the value given to variables of enum types.</span></span> <span data-ttu-id="69639-731">열거형 형식의 쉽게 사용할 수는 리터럴 기본값에 대 한 순서로 `0` 열거형 형식으로 암시적으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-731">In order for the default value of an enum type to be easily available, the literal `0` implicitly converts to any enum type.</span></span> <span data-ttu-id="69639-732">따라서 다음이 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-732">Thus, the following is permitted.</span></span>

```csharp
Color c = 0;
```

## <a name="delegates"></a><span data-ttu-id="69639-733">대리자</span><span class="sxs-lookup"><span data-stu-id="69639-733">Delegates</span></span>

<span data-ttu-id="69639-734">***대리자***는 특정 매개 변수 목록 및 반환 형식이 있는 메서드에 대한 참조를 나타내는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-734">A ***delegate type*** represents references to methods with a particular parameter list and return type.</span></span> <span data-ttu-id="69639-735">대리자는 메서드를 변수에 할당되고 매개 변수로 전달될 수 있는 엔터티로 취급할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-735">Delegates make it possible to treat methods as entities that can be assigned to variables and passed as parameters.</span></span> <span data-ttu-id="69639-736">또한 대리자는 다른 언어에 나오는 함수 포인터의 개념과 비슷하지만 함수 포인터와 달리 대리자는 개체 지향적이며 형식 안전 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-736">Delegates are similar to the concept of function pointers found in some other languages, but unlike function pointers, delegates are object-oriented and type-safe.</span></span>

<span data-ttu-id="69639-737">다음 예제에서는 `Function`라는 대리자 형식을 선언하고 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-737">The following example declares and uses a delegate type named `Function`.</span></span>

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
<span data-ttu-id="69639-738">`Function` 대리자 형식의 인스턴스는 `double` 인수를 사용하고 `double` 값을 반환하는 메서드를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-738">An instance of the `Function` delegate type can reference any method that takes a `double` argument and returns a `double` value.</span></span> <span data-ttu-id="69639-739">`Apply` 메서드가 적용 되는 지정 `Function` 의 요소에는 `double[]`을 반환을 `double[]` 결과 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="69639-739">The `Apply` method applies a given `Function` to the elements of a `double[]`, returning a `double[]` with the results.</span></span> <span data-ttu-id="69639-740">`Main` 메서드에서 `Apply`는 세 가지 다른 함수를 `double[]`에 적용하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-740">In the `Main` method, `Apply` is used to apply three different functions to a `double[]`.</span></span>

<span data-ttu-id="69639-741">대리자는 정적 메서드(예: 이전 예제의 `Square` 또는 `Math.Sin`) 또는 인스턴스 메서드(예: 이전 예제의 `m.Multiply`)를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-741">A delegate can reference either a static method (such as `Square` or `Math.Sin` in the previous example) or an instance method (such as `m.Multiply` in the previous example).</span></span> <span data-ttu-id="69639-742">인스턴스 메서드를 참조하는 대리자는 특정 개체도 참조하며, 인스턴스 메서드가 대리자를 통해 호출되는 경우 해당 개체도 이 호출에서 `this`가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-742">A delegate that references an instance method also references a particular object, and when the instance method is invoked through the delegate, that object becomes `this` in the invocation.</span></span>

<span data-ttu-id="69639-743">또한 즉석에서 만들어지는 "인라인 메서드"인 익명 함수를 사용하여 대리자를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-743">Delegates can also be created using anonymous functions, which are "inline methods" that are created on the fly.</span></span> <span data-ttu-id="69639-744">익명 함수는 주변 메서드의 지역 변수를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-744">Anonymous functions can see the local variables of the surrounding methods.</span></span> <span data-ttu-id="69639-745">따라서 위의 승수 예제 작성할 수 있습니다 보다 쉽게 사용 하지 않고는 `Multiplier` 클래스:</span><span class="sxs-lookup"><span data-stu-id="69639-745">Thus, the multiplier example above can be written more easily without using a `Multiplier` class:</span></span>

```csharp
double[] doubles =  Apply(a, (double x) => x * 2.0);
```
<span data-ttu-id="69639-746">대리자의 흥미롭고 유용한 속성은 참조하는 메서드의 클래스를 알지 못하거나 관심을 두지 않는다는 것입니다. 참조되는 메서드가 대리자와 동일한 매개 변수 및 반환 형식을 갖는다는 것만 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-746">An interesting and useful property of a delegate is that it does not know or care about the class of the method it references; all that matters is that the referenced method has the same parameters and return type as the delegate.</span></span>

## <a name="attributes"></a><span data-ttu-id="69639-747">특성</span><span class="sxs-lookup"><span data-stu-id="69639-747">Attributes</span></span>

<span data-ttu-id="69639-748">C# 프로그램의 형식, 멤버 및 기타 엔터티는 동작의 특정 측면을 제어하는 한정자를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-748">Types, members, and other entities in a C# program support modifiers that control certain aspects of their behavior.</span></span> <span data-ttu-id="69639-749">예를 들어 메서드의 액세스 가능성은 `public`, `protected`, `internal` 및 `private` 한정자를 사용하여 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-749">For example, the accessibility of a method is controlled using the `public`, `protected`, `internal`, and `private` modifiers.</span></span> <span data-ttu-id="69639-750">C#은 선언적 정보의 사용자 정의 형식을 프로그램 엔터티에 연결하고 런타임에 검색할 수 있도록 이러한 기능을 일반화합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-750">C# generalizes this capability such that user-defined types of declarative information can be attached to program entities and retrieved at run-time.</span></span> <span data-ttu-id="69639-751">프로그램은 ***특성***을 정의하고 사용하여 이러한 추가적인 선언적 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-751">Programs specify this additional declarative information by defining and using ***attributes***.</span></span>

<span data-ttu-id="69639-752">다음 예제에서는 관련 설명서에 대한 링크를 제공하기 위해 프로그램 엔터티에 배치될 수 있는 `HelpAttribute` 특성을 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-752">The following example declares a `HelpAttribute` attribute that can be placed on program entities to provide links to their associated documentation.</span></span>

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
<span data-ttu-id="69639-753">모든 특성 클래스에서 파생 된 `System.Attribute` 기본.NET Framework에서 제공 하는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="69639-753">All attribute classes derive from the `System.Attribute` base class provided by the .NET Framework.</span></span> <span data-ttu-id="69639-754">연결된 선언 바로 앞에 대괄호로 묶은 특성 이름을 인수와 함께 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-754">Attributes can be applied by giving their name, along with any arguments, inside square brackets just before the associated declaration.</span></span> <span data-ttu-id="69639-755">특성의 이름이 끝나는 경우 `Attribute`, 특성 참조 될 때 이름의 해당 부분을 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-755">If an attribute's name ends in `Attribute`, that part of the name can be omitted when the attribute is referenced.</span></span> <span data-ttu-id="69639-756">예를 들어 `HelpAttribute` 특성을 다음과 같이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69639-756">For example, the `HelpAttribute` attribute can be used as follows.</span></span>

```csharp
[Help("http://msdn.microsoft.com/.../MyClass.htm")]
public class Widget
{
    [Help("http://msdn.microsoft.com/.../MyClass.htm", Topic = "Display")]
    public void Display(string text) {}
}
```
<span data-ttu-id="69639-757">이 예제에서는 연결을 `HelpAttribute` 에 `Widget` 클래스 및 다른 `HelpAttribute` 에 `Display` 클래스의 메서드.</span><span class="sxs-lookup"><span data-stu-id="69639-757">This example attaches a `HelpAttribute` to the `Widget` class and another `HelpAttribute` to the `Display` method in the class.</span></span> <span data-ttu-id="69639-758">특성 클래스의 공용 생성자는 프로그램 엔터티에 특성을 추가할 때 제공해야 하는 정보를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-758">The public constructors of an attribute class control the information that must be provided when the attribute is attached to a program entity.</span></span> <span data-ttu-id="69639-759">특성 클래스의 공용 읽기/쓰기 속성을 참조하여 추가 정보를 제공할 수 있습니다(예: 앞에 나온 `Topic` 속성 참조).</span><span class="sxs-lookup"><span data-stu-id="69639-759">Additional information can be provided by referencing public read-write properties of the attribute class (such as the reference to the `Topic` property previously).</span></span>

<span data-ttu-id="69639-760">다음 예제에서는 런타임에 특정된 응용 프로그램 엔터티에 대 한 특성 정보를 검색할 수 있는 방법을 보여 줍니다. 리플렉션을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="69639-760">The following example shows how attribute information for a given program entity can be retrieved at run-time using reflection.</span></span>

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
<span data-ttu-id="69639-761">리플렉션을 통해 특정 특성이 요청되면 특성 클래스에 대한 생성자가 프로그램 소스에 제공된 정보와 함께 호출되고 결과 특성 인스턴스가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-761">When a particular attribute is requested through reflection, the constructor for the attribute class is invoked with the information provided in the program source, and the resulting attribute instance is returned.</span></span> <span data-ttu-id="69639-762">속성을 통해 추가 정보를 제공한 경우 해당 속성은 특성 인스턴스가 반환되기 전에 지정된 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="69639-762">If additional information was provided through properties, those properties are set to the given values before the attribute instance is returned.</span></span>
