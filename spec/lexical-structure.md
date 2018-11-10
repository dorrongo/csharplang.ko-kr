# <a name="lexical-structure"></a>어휘 구조

## <a name="programs"></a>Programs

C# ***프로그램*** 은 공식적으로 ***컴파일 단위*** ([컴파일 단위](namespaces.md#compilation-units))로 알려진 하나 이상의 ***소스 파일*** 로 구성됩니다. 소스 파일이란 정렬된 유니코드 문자 시퀀스를 말합니다. 소스 파일은 일반적으로 파일 시스템의 파일과 일대일 대응하지만 서신은 필요하지 않습니다. 최대한의 이식성을 위해 파일 시스템의 파일을 u t F-8로 인코딩하는 것이 좋습니다.

개념적으로 말해서 프로그램은 다음 세 단계를 사용하여 컴파일됩니다:

1. 특정 문자 레퍼토리 및 인코딩 체계의 파일을 유니코드 문자 시퀀스로 변환하는, (Transformation)변환을 합니다.
2. 유니 코드 입력 문자 스트림을 토큰 스트림으로 변환하는, (Lexical analysis)어휘 분석을 합니다.
3. 토큰 스트림을 실행 가능한 코드로 변환하는, (Syntactic analysis)구문 분석을 합니다.

## <a name="grammars"></a>문법

이 사양은 두 문법을 사용하여 C# 프로그래밍 언어의 구문을 제공 합니다. 합니다 (Lexical grammar) ***어휘 문법*** ([어휘 문법](lexical-structure.md#lexical-grammar)) 은 유니코드 문자가 어떻게 조합되어 (line terminators)줄 종결자, 공백, 설명, 토큰 및 전처리 지시문을 형성하는지 그 방법을 정의합니다. (Syntactic grammar) ***구문 문법*** ([구문 문법](lexical-structure.md#syntactic-grammar)) 은 어떻게 어휘 문법에서 생성 된 토큰이 결합되어 C # 프로그램을 구성하는지 그 방법을 정의합니다.

### <a name="grammar-notation"></a>문법 표기법

어휘 및 구문 문법은 ANTLR 문법 도구의 표기법을 사용하여 Backus Naur 형식으로 제공됩니다.

### <a name="lexical-grammar"></a>어휘 문법

C#의 어휘 문법은 [어휘 분석](lexical-structure.md#lexical-analysis)과 [토큰](lexical-structure.md#tokens), 및 [전처리 지시문](lexical-structure.md#pre-processing-directives)에 표시됩니다. 어휘 문법의 터미널 기호는 유니코드 문자 집합의 문자이며, 어휘 문법은 문자가 결합되어 토큰 ([토큰](lexical-structure.md#tokens))과 공백 ([공백을](lexical-structure.md#white-space)), 주석 ([주석](lexical-structure.md#comments)) 및 전처리 지시문 ([전처리 지시문](lexical-structure.md#pre-processing-directives))을 형성하는 방법을 지정합니다.

C# 프로그램의 모든 소스 파일은 어휘 문법 ([어휘 분석](lexical-structure.md#lexical-analysis))의 *입력* 생성을 따라야 합니다.

### <a name="syntactic-grammar"></a>구문 문법

C#의 구문 문법은 각 챕터들과 그 부록에 표시됩니다. 구문 문법의 터미널 기호는 어휘 문법에서 정의된 토큰이고, 구문 문법은 토큰이 결합되어 C# 프로그램을 형성하는 방법을 지정합니다.

C# 프로그램의 모든 소스 파일은 구문 문법의 프로덕션 *compilation_unit*([컴파일 단위](namespaces.md#compilation-units))을 따라야 합니다.

## <a name="lexical-analysis"></a>어휘 분석

*입력* 프로덕션은 C# 소스 파일의 어휘 구조를 정의 합니다. C# 프로그램의 각 소스 파일은 이 어휘 문법 프로덕션에 맞아야 합니다.

```antlr
input
    : input_section?
    ;

input_section
    : input_section_part+
    ;

input_section_part
    : input_element* new_line
    | pp_directive
    ;

input_element
    : whitespace
    | comment
    | token
    ;
```

5 개의 기본 요소로 C# 소스 파일의 어휘 구조를 구성: 줄 종결자 ([줄 종결자](lexical-structure.md#line-terminators)), 공백 ([공백](lexical-structure.md#white-space)), 주석 ([주석](lexical-structure.md#comments)), 토큰 ([토큰](lexical-structure.md#tokens)), 전처리 지시문 및 ([전처리 지시문](lexical-structure.md#pre-processing-directives)). 이러한 기본 요소를 토큰만 C# 프로그램의 구문 문법에서 중요 한 ([구문 문법](lexical-structure.md#syntactic-grammar)).

C# 원본 파일을 처리 하는 어휘 파일 구문 분석에 대 한 입력 되는 토큰의 시퀀스로 줄이는 이루어져 있습니다. 줄 종결자, 공백 및 주석 토큰을 구분 하는 사용 될 수 있습니다 및 전처리 지시문 수는 건너 원본 파일의 섹션 시키지만 이러한 어휘 요소는 C# 프로그램의 구문 구조에 영향을 미치지 하는 그렇지 않은 경우.

보간된 문자열 리터럴의 경우 ([보간된 문자열 리터럴을](lexical-structure.md#interpolated-string-literals)) 단일 토큰 어휘 분석을 통해 처음에 생성 되지만 나뉩니다 어휘 분석 반복적으로 적용 되는 여러 입력된 요소 까지 모든 보간된 문자열 리터럴을 해결 되었습니다. 결과 토큰을 구문 분석에 대 한 입력으로 사용할 수 있습니다.

어휘 문법 요소를 여러 소스 파일의 문자 시퀀스로 일치 하는 경우 어휘 처리를 통해 가장 긴 가능한 어휘 요소를 형성 합니다. 예를 들어 문자 시퀀스 `//` 어휘 요소는 단일 보다 길기 때문에 한 줄 주석의 시작으로 처리 됩니다 `/` 토큰입니다.

### <a name="line-terminators"></a>줄 종결자

줄 종결자는 줄을 C# 소스 파일의 문자를 나눕니다.

```antlr
new_line
    : '<Carriage return character (U+000D)>'
    | '<Line feed character (U+000A)>'
    | '<Carriage return character (U+000D) followed by line feed character (U+000A)>'
    | '<Next line character (U+0085)>'
    | '<Line separator character (U+2028)>'
    | '<Paragraph separator character (U+2029)>'
    ;
```

호환 소스 코드 파일의 끝 표시자를 추가 하는 편집 도구 제대로 시퀀스로 표시 하는 파일을 소스를 사용 하도록 설정 하려면 줄을 종료 하 고에 대 한 C# 프로그램의 모든 소스 파일에 순서 대로 다음과 같은 변환이 적용 됩니다.

*  소스 파일의 마지막 문자 Z 제어 문자가 문자 인지 (`U+001A`),이 문자를 삭제 합니다.
*  캐리지 리턴 문자 (`U+000D`) 및 소스 파일의 마지막 문자는 캐리지 리턴 없는 경우 해당 원본 파일은 비어 있지 않은 경우 소스 파일의 끝에 추가 됩니다 (`U+000D`), 줄 바꿈 (`U+000A`), 줄 구분 기호 (`U+2028`), 또는 단락 구분 기호 (`U+2029`).

### <a name="comments"></a>설명

두 가지 형태의 주석이 지원 됩니다: 단일 줄 주석 및 구분 기호로 분리 된 주석입니다. ***한 줄 주석이*** 문자로 시작 `//` 하 고 소스 줄의 끝에 확장 합니다. ***주석 구분*** 문자를 사용 하 여 시작 `/*` 및 끝 문자를 사용 하 여 `*/`입니다. 구분 기호로 분리 된 주석 여러 줄으로 나누어 입력할 수 있습니다.

```antlr
comment
    : single_line_comment
    | delimited_comment
    ;

single_line_comment
    : '//' input_character*
    ;

input_character
    : '<Any Unicode character except a new_line_character>'
    ;

new_line_character
    : '<Carriage return character (U+000D)>'
    | '<Line feed character (U+000A)>'
    | '<Next line character (U+0085)>'
    | '<Line separator character (U+2028)>'
    | '<Paragraph separator character (U+2029)>'
    ;

delimited_comment
    : '/*' delimited_comment_section* asterisk* '/'
    ;

delimited_comment_section
    : '/'
    | asterisk* not_slash_or_asterisk
    ;

asterisk
    : '*'
    ;

not_slash_or_asterisk
    : '<Any Unicode character except / or *>'
    ;
```

주석을 중첩 하지 마십시오. 문자 시퀀스 `/*` 및 `*/` 내에서 특별 한 의미가 `//` 주석 처리 및 문자 시퀀스 `//` 및 `/*` 구분 기호로 분리 된 주석 내에서 특별 한 의미가 없습니다.

주석 문자 및 문자열 리터럴 내에서 처리 되지 않습니다.

이 예제에서
```csharp
/* Hello, world program
   This program writes "hello, world" to the console
*/
class Hello
{
    static void Main() {
        System.Console.WriteLine("hello, world");
    }
}
```
구분 기호로 분리 된 주석을 포함 되어 있습니다.

이 예제에서
```csharp
// Hello, world program
// This program writes "hello, world" to the console
//
class Hello // any name will do for this class
{
    static void Main() { // this method must be named "Main"
        System.Console.WriteLine("hello, world");
    }
}
```
여러 줄 주석을 보여 줍니다.

### <a name="white-space"></a>공백

공백 문자는 유니코드 클래스를 포함 하는 공백 문자 z의 모든 문자 뿐만 아니라 가로 탭 문자, 세로 탭 문자인 및 형식 문자를 피드로 정의 됩니다.

```antlr
whitespace
    : '<Any character with Unicode class Zs>'
    | '<Horizontal tab character (U+0009)>'
    | '<Vertical tab character (U+000B)>'
    | '<Form feed character (U+000C)>'
    ;
```

## <a name="tokens"></a>토큰

토큰의 몇 가지 종류가 있습니다: 식별자, 키워드, 리터럴, 연산자 및 문장 부호입니다. 공백 문자 및 주석은 토큰을 없지만 토큰에 대 한 구분 기호로 작동 합니다.

```antlr
token
    : identifier
    | keyword
    | integer_literal
    | real_literal
    | character_literal
    | string_literal
    | interpolated_string_literal
    | operator_or_punctuator
    ;
```

### <a name="unicode-character-escape-sequences"></a>유니코드 문자 이스케이프 시퀀스

유니코드 문자 이스케이프 시퀀스를 유니코드 문자를 나타냅니다. 유니코드 문자 이스케이프 시퀀스 식별자에서 처리 됩니다 ([식별자](lexical-structure.md#identifiers)), 문자 리터럴 ([문자 리터럴](lexical-structure.md#character-literals)), 및 일반 문자열 리터럴 ([문자열 리터럴](lexical-structure.md#string-literals)). 다른 위치 (예: 연산자, 문장 부호, 또는 키워드)에 유니코드 문자 이스케이프 처리 되지 않습니다.

```antlr
unicode_escape_sequence
    : '\\u' hex_digit hex_digit hex_digit hex_digit
    | '\\U' hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit
    ;
```

유니코드 이스케이프 시퀀스를 나타내는 16 진수 숫자 다음 형성 된 단일 유니코드 문자를 "`\u`"또는"`\U`" 문자입니다. C#을 사용 하는 16 비트 유니코드 코드 포인트에서 문자 및 문자열 값 인코딩을 U + 10ffff 까지의 범위 u+10000에서에서 유니코드 문자는 문자 리터럴에서 허용 되지 않습니다 하 고 유니코드 서로게이트 쌍을 사용 하 여 문자열 리터럴 안에 표시 됩니다. 0x10FFFF 위에 코드 포인트를 사용 하 여 유니코드 문자 지원 되지 않습니다.

여러 변환은 수행 되지 않습니다. 예를 들어, 문자열 리터럴 "`\u005Cu005C`"에 해당 하 는"`\u005C`" 대신 "`\`"입니다. 유니코드 값을 `\u005C` 는 문자 "`\`"입니다.

이 예제에서
```csharp
class Class1
{
    static void Test(bool \u0066) {
        char c = '\u0066';
        if (\u0066)
            System.Console.WriteLine(c.ToString());
    }        
}
```
몇 가지 사용 방법을 보여 줍니다 `\u0066`, 문자에 대 한 이스케이프 시퀀스는 "`f`"입니다. 프로그램은
```csharp
class Class1
{
    static void Test(bool f) {
        char c = 'f';
        if (f)
            System.Console.WriteLine(c.ToString());
    }        
}
```

### <a name="identifiers"></a>식별자

이 섹션에 제공 된 식별자 규칙을 정확 하 게 일치 해당 권장 Unicode Standard Annex 31를 제외 하 고 밑줄 문자로 초기 (그대로 C 프로그래밍 언어에서 일반적인), 유니코드 이스케이프 시퀀스는 허용 됩니다. 식별자에서 허용 및 "`@`" 키워드를 식별자로 사용할 수 있도록 접두사로 문자는 사용할 수 있습니다.

```antlr
identifier
    : available_identifier
    | '@' identifier_or_keyword
    ;

available_identifier
    : '<An identifier_or_keyword that is not a keyword>'
    ;

identifier_or_keyword
    : identifier_start_character identifier_part_character*
    ;

identifier_start_character
    : letter_character
    | '_'
    ;

identifier_part_character
    : letter_character
    | decimal_digit_character
    | connecting_character
    | combining_character
    | formatting_character
    ;

letter_character
    : '<A Unicode character of classes Lu, Ll, Lt, Lm, Lo, or Nl>'
    | '<A unicode_escape_sequence representing a character of classes Lu, Ll, Lt, Lm, Lo, or Nl>'
    ;

combining_character
    : '<A Unicode character of classes Mn or Mc>'
    | '<A unicode_escape_sequence representing a character of classes Mn or Mc>'
    ;

decimal_digit_character
    : '<A Unicode character of the class Nd>'
    | '<A unicode_escape_sequence representing a character of the class Nd>'
    ;

connecting_character
    : '<A Unicode character of the class Pc>'
    | '<A unicode_escape_sequence representing a character of the class Pc>'
    ;

formatting_character
    : '<A Unicode character of the class Cf>'
    | '<A unicode_escape_sequence representing a character of the class Cf>'
    ;
```

위에서 언급 한 유니코드 문자 클래스에 대 한 자세한 내용은 유니코드 표준, 버전 3.0, 4.5 섹션을 참조 하세요.

유효한 식별자의 예로 "`identifier1`","`_identifier2`", 및 "`@if`"입니다.

표준에 맞는 프로그램 식별자는 Unicode Standard Annex 15에 정의 된 대로 유니코드 정규화 형식 C에서 정의 된 정규 형식에서 이어야 합니다. 정규화 형식 C에 없는 식별자를 발견할 때 동작은 구현 시 정의 됩니다. 그러나 진단 필요 하지 않습니다.

접두사 "`@`" 다른 프로그래밍 언어와 상호 작용 하는 경우에 유용 식별자로 키워드를 사용 하도록 설정 합니다. 문자 `@` 면 실제로 식별자의 일부가 아니므로 식별자 접두사 없이 일반 식별자로 다른 언어로 보일 수 있습니다. 식별자를 `@` 접두사 라고는 ***축 자 식별자***합니다. 사용 된 `@` 키워드 없는 식별자에 대 한 접두사를 사용할 수는 있지만 스타일의 것이 좋습니다.

예제:
```csharp
class @class
{
    public static void @static(bool @bool) {
        if (@bool)
            System.Console.WriteLine("true");
        else
            System.Console.WriteLine("false");
    }    
}

class Class1
{
    static void M() {
        cl\u0061ss.st\u0061tic(true);
    }
}
```
이라는 클래스를 정의 "`class`"라는 정적 메서드"with`static`"하는 명명 된 매개 변수"`bool`"입니다. 메모 유니코드 이스케이프 하므로 토큰 키워드에 허용 되지 않는 "`cl\u0061ss`"는 식별자 이며 동일한 식별자를 "`@class`"입니다.

두 개의 식별자 것으로 간주 됩니다 동일한 순서로 다음과 같은 변환이 적용 된 후 동일 합니다.

*  접두사 "`@`"를 사용 하는 경우 제거 됩니다.
*  각 *unicode_escape_sequence* 해당 유니코드 문자로 변환 됩니다.
*  모든 *formatting_character*가 제거 되었습니다.

식별자를 포함 하는 두 개의 연속 밑줄 문자 (`U+005F`) 구현에서 사용 하도록 예약 합니다. 예를 들어 구현을 두 개의 밑줄로 시작 하는 확장 된 키워드를 제공할 수 있습니다.

### <a name="keywords"></a>키워드

A ***키워드*** 예약 되며 앞에 오는 경우를 제외 하 고 식별자로 사용할 수 없습니다 하 문자는 식별자와 같은 시퀀스를 `@` 문자입니다.

```antlr
keyword
    : 'abstract' | 'as'       | 'base'       | 'bool'      | 'break'
    | 'byte'     | 'case'     | 'catch'      | 'char'      | 'checked'
    | 'class'    | 'const'    | 'continue'   | 'decimal'   | 'default'
    | 'delegate' | 'do'       | 'double'     | 'else'      | 'enum'
    | 'event'    | 'explicit' | 'extern'     | 'false'     | 'finally'
    | 'fixed'    | 'float'    | 'for'        | 'foreach'   | 'goto'
    | 'if'       | 'implicit' | 'in'         | 'int'       | 'interface'
    | 'internal' | 'is'       | 'lock'       | 'long'      | 'namespace'
    | 'new'      | 'null'     | 'object'     | 'operator'  | 'out'
    | 'override' | 'params'   | 'private'    | 'protected' | 'public'
    | 'readonly' | 'ref'      | 'return'     | 'sbyte'     | 'sealed'
    | 'short'    | 'sizeof'   | 'stackalloc' | 'static'    | 'string'
    | 'struct'   | 'switch'   | 'this'       | 'throw'     | 'true'
    | 'try'      | 'typeof'   | 'uint'       | 'ulong'     | 'unchecked'
    | 'unsafe'   | 'ushort'   | 'using'      | 'virtual'   | 'void'
    | 'volatile' | 'while'
    ;
```

문법의 일부 지역에서는 특정 식별자 특별 한 의미가 있지만 키워드가 되지는 않습니다. 이러한 식별자는 "상황에 맞는 키워드" 라고도 합니다. 예를 들어, 속성 선언 내는 "`get`"및"`set`" 식별자는 특별 한 의미가 ([접근자](classes.md#accessors)). 이외의 다른 식별자 `get` 또는 `set` 수 없습니다 이러한 위치에 있으므로이 사용 하이 여 이러한 단어를 식별자로 사용 하 여 충돌 하지 않습니다. 다른 경우에 같은 식별자와 마찬가지로 "`var`"에서 암시적으로 형식화 된 지역 변수 선언 ([지역 변수 선언](statements.md#local-variable-declarations)), 상황별 키워드는 선언 된 이름이 충돌할 수 있습니다. 이러한 경우에는 선언 된 이름 식별자의 상황별 키워드로 사용 보다 우선 순위를 갖습니다.

### <a name="literals"></a>리터럴

A ***리터럴*** 값의 소스 코드 표현입니다.

```antlr
literal
    : boolean_literal
    | integer_literal
    | real_literal
    | character_literal
    | string_literal
    | null_literal
    ;
```

#### <a name="boolean-literals"></a>부울 리터럴

부울 리터럴 값이 두 개: `true` 고 `false`입니다.

```antlr
boolean_literal
    : 'true'
    | 'false'
    ;
```

형식의 *boolean_literal* 는 `bool`합니다.

#### <a name="integer-literals"></a>정수 리터럴

정수 리터럴 형식의 값을 쓰는 데 사용 됩니다 `int`, `uint`를 `long`, 및 `ulong`합니다. 정수 리터럴에 있는 두 가지 가능한 형식: 10 진수 및 16 진수입니다.

```antlr
integer_literal
    : decimal_integer_literal
    | hexadecimal_integer_literal
    ;

decimal_integer_literal
    : decimal_digit+ integer_type_suffix?
    ;

decimal_digit
    : '0' | '1' | '2' | '3' | '4' | '5' | '6' | '7' | '8' | '9'
    ;

integer_type_suffix
    : 'U' | 'u' | 'L' | 'l' | 'UL' | 'Ul' | 'uL' | 'ul' | 'LU' | 'Lu' | 'lU' | 'lu'
    ;

hexadecimal_integer_literal
    : '0x' hex_digit+ integer_type_suffix?
    | '0X' hex_digit+ integer_type_suffix?
    ;

hex_digit
    : '0' | '1' | '2' | '3' | '4' | '5' | '6' | '7' | '8' | '9'
    | 'A' | 'B' | 'C' | 'D' | 'E' | 'F' | 'a' | 'b' | 'c' | 'd' | 'e' | 'f';
```

리터럴 정수의 형식은 다음과 같이 결정 됩니다.

*  해당 값을 나타낼 수 있는 이러한 형식 중 첫 번째 리터럴 접미사가 없는 경우에: `int`, `uint`를 `long`, `ulong`합니다.
*  리터럴이 오는 경우 `U` 또는 `u`, 해당 값을 나타낼 수 있는 이러한 형식 중 첫 번째 있기: `uint`, `ulong`합니다.
*  리터럴이 오는 경우 `L` 또는 `l`, 해당 값을 나타낼 수 있는 이러한 형식 중 첫 번째 있기: `long`, `ulong`합니다.
*  리터럴이 오는 경우 `UL`, `Ul`, `uL`, `ul`를 `LU`를 `Lu`, `lU`, 또는 `lu`, 형식 `ulong`합니다.

정수 리터럴이 나타내는 값의 범위를 벗어나는 인지는 `ulong` 컴파일 타임 오류가 발생 하는 형식입니다.

스타일의 문제로, 제안 하는 "`L`"대신 사용할 수"`l`" 형식의 리터럴을 작성할 때 `long`문자를 혼동 하기 쉬운 이므로, "`l`"숫자"과`1`" 합니다.

가능한 가장 작은 허용 하도록 `int` 고 `long` 쓸 10 진수 정수 리터럴로 다음 두 규칙이 존재 하는 값:

* 경우는 *decimal_integer_literal* 2147483648 값 (2 ^31) 없으며 *integer_type_suffix* 바로 다음에 오는 단항 빼기 연산자 토큰이 토큰으로 표시 됩니다 ([단항 빼기 연산자](expressions.md#unary-minus-operator)), 결과 형식의 상수는 `int` -2147483648 값을 사용 하 여 (-2 ^31). 다른 모든 상황에서 이러한를 *decimal_integer_literal* 유형의 `uint`합니다.
* 경우는 *decimal_integer_literal* 9223372036854775808 값 (2 ^63) 없으며 *integer_type_suffix* 또는 *integer_type_suffix* `L` 또는 `l` 바로 다음에 오는 단항 빼기 연산자 토큰이 토큰으로 표시 됩니다 ([단항 빼기 연산자](expressions.md#unary-minus-operator)), 결과 형식의 상수는 `long` 값-9223372036854775808 (-2 ^63). 다른 모든 상황에서 이러한를 *decimal_integer_literal* 유형의 `ulong`합니다.

#### <a name="real-literals"></a>실제 리터럴

실제 리터럴 형식의 값을 쓰는 데 사용 됩니다 `float`하십시오 `double`, 및 `decimal`합니다.

```antlr
real_literal
    : decimal_digit+ '.' decimal_digit+ exponent_part? real_type_suffix?
    | '.' decimal_digit+ exponent_part? real_type_suffix?
    | decimal_digit+ exponent_part real_type_suffix?
    | decimal_digit+ real_type_suffix
    ;

exponent_part
    : 'e' sign? decimal_digit+
    | 'E' sign? decimal_digit+
    ;

sign
    : '+'
    | '-'
    ;

real_type_suffix
    : 'F' | 'f' | 'D' | 'd' | 'M' | 'm'
    ;
```

없으면 *real_type_suffix* 가 지정 된 형식의 실수 리터럴이 `double`합니다. 이 고, 그렇지 실제 형식 접미사는 다음과 같이 실제 리터럴 형식을 결정:

*  그 뒤에 실수 리터럴을 `F` 또는 `f` 유형의 `float`합니다. 예를 들어, 리터럴 `1f`, `1.5f`를 `1e10f`, 및 `123.456F` 형식의 모든 `float`합니다.
*  그 뒤에 실수 리터럴을 `D` 또는 `d` 유형의 `double`합니다. 예를 들어, 리터럴 `1d`, `1.5d`를 `1e10d`, 및 `123.456D` 형식의 모든 `double`합니다.
*  그 뒤에 실수 리터럴을 `M` 또는 `m` 유형의 `decimal`합니다. 예를 들어, 리터럴 `1m`, `1.5m`를 `1e10m`, 및 `123.456M` 형식의 모든 `decimal`합니다. 이 리터럴은 변환할를 `decimal` 정확한 값을 가져오고 사용 하 여 가장 가까운 표현할 수 있는 값으로 반올림 하 여 필요한 경우 값 은행원의 반올림 ([decimal 형식](types.md#the-decimal-type)). 리터럴의 명백한 규모에 관계 없이 값이 반올림 됩니다 아니면 값이 0 (후자의 경우 크기와 부호가 값은 0)에 유지 됩니다. 따라서 리터럴 `2.900m` 기호를 사용 하 여 10 진수를 구문 분석할 `0`, 계수 `2900`, 및 크기 조정 `3`합니다.

지정한 리터럴에 지정한 형식으로 표현할 수 없는 경우 컴파일 타임 오류가 발생 합니다.

형식의 실제 리터럴 값 `float` 또는 `double` IEEE를 사용 하 여 결정 됩니다 "가장 가까운 수로 반올림 됨" 모드입니다.

실수 리터럴을, 소수 자릿수는 소수점 뒤 항상 필요 합니다. 예를 들어 `1.3F` 실수 리터럴 하지만 `1.F` 아닙니다.

#### <a name="character-literals"></a>문자 리터럴

문자 리터럴은 단일 문자를 나타내며 큰따옴표의 문자에서와 같이 일반적으로 이루어져 `'a'`합니다.

참고: ANTLR 문법 표기법을 사용 하면 다음 혼동 있습니다. ANTLR를 작성 하는 경우에 `\'` 작은따옴표의 약자 `'`합니다. 작성 하는 경우 및 `\\` 단일 백슬래시의 약자 `\`합니다. 따라서 리터럴 문자에 대 한 첫 번째 규칙은 문자, 작은따옴표, 차례로 작은따옴표를 사용 하 여 시작을 의미 합니다. 11 개의 가능한 단순 이스케이프 시퀀스 이며 `\'`, `\"`, `\\`, `\0`, `\a`, `\b`, `\f`, `\n`, `\r`, `\t`, `\v`.

```antlr
character_literal
    : '\'' character '\''
    ;

character
    : single_character
    | simple_escape_sequence
    | hexadecimal_escape_sequence
    | unicode_escape_sequence
    ;

single_character
    : '<Any character except \' (U+0027), \\ (U+005C), and new_line_character>'
    ;

simple_escape_sequence
    : '\\\'' | '\\"' | '\\\\' | '\\0' | '\\a' | '\\b' | '\\f' | '\\n' | '\\r' | '\\t' | '\\v'
    ;

hexadecimal_escape_sequence
    : '\\x' hex_digit hex_digit? hex_digit? hex_digit?;
```

백슬래시 문자 뒤에 오는 문자 (`\`)에 *문자* 는 다음 문자 중 하나 여야 합니다: `'`, `"`를 `\`, `0`, `a`, `b` , `f`, `n`, `r`, `t`, `u`, `U`, `x`, `v`. 그렇지 않으면 컴파일 타임 오류가 발생합니다.

16 진수 이스케이프 시퀀스는 16 진수 숫자 다음과 같은 구성 값을 사용 하 여 단일 유니코드 문자를 나타내는 "`\x`"입니다.

리터럴 문자를 나타내는 값 보다 크면 `U+FFFF`, 컴파일 시간 오류가 발생 합니다.

유니코드 문자 이스케이프 시퀀스 ([유니코드 문자 이스케이프 시퀀스인](lexical-structure.md#unicode-character-escape-sequences)) 문자 리터럴에 범위에서 여야 합니다 `U+0000` 에 `U+FFFF`입니다.

아래 표에 설명 된 대로 단순 이스케이프 시퀀스를 유니코드 문자 인코딩을 나타냅니다.


| __이스케이프 시퀀스__ | __문자 이름__ | __유니코드 인코딩__ |
|---------------------|--------------------|----------------------|
| `\'`                | 작은따옴표       | `0x0027`             | 
| `\"`                | 큰따옴표       | `0x0022`             | 
| `\\`                | 백슬래시          | `0x005C`             | 
| `\0`                | Null               | `0x0000`             | 
| `\a`                | 경고              | `0x0007`             | 
| `\b`                | 백스페이스          | `0x0008`             | 
| `\f`                | 폼 피드          | `0x000C`             | 
| `\n`                | 줄 바꿈           | `0x000A`             | 
| `\r`                | 캐리지 리턴    | `0x000D`             | 
| `\t`                | 가로 탭     | `0x0009`             | 
| `\v`                | 세로 탭       | `0x000B`             | 

형식의 *character_literal* 는 `char`합니다.

#### <a name="string-literals"></a>문자열 리터럴

C# 두 가지 형태의 문자열 리터럴 지원: ***정규 문자열 리터럴은*** 하 고 ***축 자 문자열 리터럴은***합니다.

일반 문자열 리터럴 구성에서 같이 큰따옴표로 묶인 0 개 이상의 문자 `"hello"`, 모두 단순 이스케이프 시퀀스를 포함할 수 있습니다 (같은 `\t` 탭 문자), 16 진수 및 유니코드 이스케이프 시퀀스입니다.

축 자 문자열 리터럴은 이루어져는 `@` 큰따옴표 문자, 0 개 이상의 문자 및 닫는 큰따옴표 문자 뒤에 문자입니다. 간단한 예로 `@"hello"`합니다. 축 자 문자열 리터럴 구분 기호 사이 있는 문자를 정확 하 게 해석 되며 되 고 있는 유일한 예외는 *quote_escape_sequence*합니다. 특히, 단순 이스케이프 시퀀스 및 16 진수 및 유니코드 이스케이프 시퀀스가 처리 되지 않습니다 축 자 문자열 리터럴. 축 자 문자열 리터럴 여러 줄으로 나누어 입력할 수 있습니다.

```antlr
string_literal
    : regular_string_literal
    | verbatim_string_literal
    ;

regular_string_literal
    : '"' regular_string_literal_character* '"'
    ;

regular_string_literal_character
    : single_regular_string_literal_character
    | simple_escape_sequence
    | hexadecimal_escape_sequence
    | unicode_escape_sequence
    ;

single_regular_string_literal_character
    : '<Any character except " (U+0022), \\ (U+005C), and new_line_character>'
    ;

verbatim_string_literal
    : '@"' verbatim_string_literal_character* '"'
    ;

verbatim_string_literal_character
    : single_verbatim_string_literal_character
    | quote_escape_sequence
    ;

single_verbatim_string_literal_character
    : '<any character except ">'
    ;

quote_escape_sequence
    : '""'
    ;
```

백슬래시 문자 뒤에 오는 문자 (`\`)에 *regular_string_literal_character* 는 다음 문자 중 하나 여야 합니다: `'`, `"`를 `\`, `0`, `a` , `b`, `f`, `n`, `r`, `t`, `u`, `U`, `x`, `v`. 그렇지 않으면 컴파일 타임 오류가 발생합니다.

이 예제에서
```csharp
string a = "hello, world";                   // hello, world
string b = @"hello, world";                  // hello, world

string c = "hello \t world";                 // hello      world
string d = @"hello \t world";                // hello \t world

string e = "Joe said \"Hello\" to me";       // Joe said "Hello" to me
string f = @"Joe said ""Hello"" to me";      // Joe said "Hello" to me

string g = "\\\\server\\share\\file.txt";    // \\server\share\file.txt
string h = @"\\server\share\file.txt";       // \\server\share\file.txt

string i = "one\r\ntwo\r\nthree";
string j = @"one
two
three";
```
다양 한 문자열 리터럴 보여 줍니다. 마지막 문자열 리터럴에 `j`, 축 자 문자열 리터럴 여러 줄에 걸쳐 있는 됩니다. 줄 바꿈 문자로 같은 공백 문자를 포함 하 여 따옴표 사이 있는 문자를 그대로 보존 됩니다.

16 진수 이스케이프 시퀀스는 다양 한 16 진수 숫자, 문자열 리터럴 있을 수 있으므로 `"\x123"` 16 진수 값 123 사용 하 여 단일 문자를 포함 합니다. 16 진수 값 3 문자 뒤에 12 사용 하 여 문자를 포함 하는 문자열을 만들려면 하나 작성할 수 `"\x00123"` 또는 `"\x12" + "3"` 대신 합니다.

형식의 *string_literal* 는 `string`합니다.

각 문자열 리터럴 새 문자열 인스턴스에서 반드시 발생 하지 않습니다. 두 개 이상의 문자열 리터럴을 하는 경우 문자열 같음 연산자에 따라 해당 하는 ([같음 연산자를 문자열](expressions.md#string-equality-operators)) 동일한 문자열 인스턴스를 해당 문자열 리터럴을 참조할 동일한 프로그램에 표시 합니다. 예를 들어, 생성 한 출력
```csharp
class Test
{
    static void Main() {
        object a = "hello";
        object b = "hello";
        System.Console.WriteLine(a == b);
    }
}
```
`True` 두 개의 리터럴 동일한 문자열 인스턴스를 참조 합니다.

#### <a name="interpolated-string-literals"></a>보간된 문자열 리터럴

보간된 문자열 리터럴을 문자열 리터럴로 유사 하지만 구분 구멍이 포함 `{` 고 `}`, 식 여기서 발생할 수 있습니다. 런타임 시 식 위치에 구멍 발생 하는 문자열에 대체의 텍스트 형식 필요 하기 위한 목적으로 평가 됩니다. 구문 및 의미 체계의 문자열 보간의 섹션에 설명 된 ([보간된 문자열](expressions.md#interpolated-strings)).

문자열 리터럴와 같은 일반 또는 약어 보간된 문자열 리터럴은 수 있습니다. 보간된 정규 문자열 리터럴은로 구분 됩니다 `$"` 하 고 `"`, 약어 보간된 문자열 리터럴 구분 되 고 `$@"` 및 `"`합니다.

다른 리터럴와 같은 어휘 분석 리터럴 보간된 문자열의 처음 아래 문법에 따라 단일 토큰에서 발생합니다. 그러나 구문 분석 하기 전에 리터럴 보간된 문자열의 단일 토큰 취약 한 부분을 포함 하는 문자열의 부분에 대 한 여러 토큰으로 구분 됩니다 및 취약 한 부분에서 발생 하는 입력된 요소가 다시 분석 어휘 적으로 됩니다. 다시 처리할 수 있지만, 어휘 적으로 수정한 경우는 결과적으로 일련의 처리를 구문 분석을 위해 토큰 보다 보간된 문자열 리터럴을 생성할 수 있습니다이.

```antlr
interpolated_string_literal
    : '$' interpolated_regular_string_literal
    | '$' interpolated_verbatim_string_literal
    ;

interpolated_regular_string_literal
    : interpolated_regular_string_whole
    | interpolated_regular_string_start  interpolated_regular_string_literal_body interpolated_regular_string_end
    ;

interpolated_regular_string_literal_body
    : regular_balanced_text
    | interpolated_regular_string_literal_body interpolated_regular_string_mid regular_balanced_text
    ;

interpolated_regular_string_whole
    : '"' interpolated_regular_string_character* '"'
    ;

interpolated_regular_string_start
    : '"' interpolated_regular_string_character* '{'
    ;

interpolated_regular_string_mid
    : interpolation_format? '}' interpolated_regular_string_characters_after_brace? '{'
    ;

interpolated_regular_string_end
    : interpolation_format? '}' interpolated_regular_string_characters_after_brace? '"'
    ;

interpolated_regular_string_characters_after_brace
    : interpolated_regular_string_character_no_brace
    | interpolated_regular_string_characters_after_brace interpolated_regular_string_character
    ;

interpolated_regular_string_character
    : single_interpolated_regular_string_character
    | simple_escape_sequence
    | hexadecimal_escape_sequence
    | unicode_escape_sequence
    | open_brace_escape_sequence
    | close_brace_escape_sequence
    ;

interpolated_regular_string_character_no_brace
    : '<Any interpolated_regular_string_character except close_brace_escape_sequence and any hexadecimal_escape_sequence or unicode_escape_sequence designating } (U+007D)>'
    ;

single_interpolated_regular_string_character
    : '<Any character except \" (U+0022), \\ (U+005C), { (U+007B), } (U+007D), and new_line_character>'
    ;

open_brace_escape_sequence
    : '{{'
    ;

    close_brace_escape_sequence
    : '}}'
    ;
    
regular_balanced_text
    : regular_balanced_text_part+
    ;

regular_balanced_text_part
    : single_regular_balanced_text_character
    | delimited_comment
    | '@' identifier_or_keyword
    | string_literal
    | interpolated_string_literal
    | '(' regular_balanced_text ')'
    | '[' regular_balanced_text ']'
    | '{' regular_balanced_text '}'
    ;
    
single_regular_balanced_text_character
    : '<Any character except / (U+002F), @ (U+0040), \" (U+0022), $ (U+0024), ( (U+0028), ) (U+0029), [ (U+005B), ] (U+005D), { (U+007B), } (U+007D) and new_line_character>'
    | '</ (U+002F), if not directly followed by / (U+002F) or * (U+002A)>'
    ;
    
interpolation_format
    : interpolation_format_character+
    ;
    
interpolation_format_character
    : '<Any character except \" (U+0022), : (U+003A), { (U+007B) and } (U+007D)>'
    ;
    
interpolated_verbatim_string_literal
    : interpolated_verbatim_string_whole
    | interpolated_verbatim_string_start interpolated_verbatim_string_literal_body interpolated_verbatim_string_end
    ;

interpolated_verbatim_string_literal_body
    : verbatim_balanced_text
    | interpolated_verbatim_string_literal_body interpolated_verbatim_string_mid verbatim_balanced_text
    ;
    
interpolated_verbatim_string_whole
    : '@"' interpolated_verbatim_string_character* '"'
    ;
    
interpolated_verbatim_string_start
    : '@"' interpolated_verbatim_string_character* '{'
    ;
    
interpolated_verbatim_string_mid
    : interpolation_format? '}' interpolated_verbatim_string_characters_after_brace? '{'
    ;
    
interpolated_verbatim_string_end
    : interpolation_format? '}' interpolated_verbatim_string_characters_after_brace? '"'
    ;
    
interpolated_verbatim_string_characters_after_brace
    : interpolated_verbatim_string_character_no_brace
    | interpolated_verbatim_string_characters_after_brace interpolated_verbatim_string_character
    ;
    
interpolated_verbatim_string_character
    : single_interpolated_verbatim_string_character
    | quote_escape_sequence
    | open_brace_escape_sequence
    | close_brace_escape_sequence
    ;
    
interpolated_verbatim_string_character_no_brace
    : '<Any interpolated_verbatim_string_character except close_brace_escape_sequence>'
    ;
    
single_interpolated_verbatim_string_character
    : '<Any character except \" (U+0022), { (U+007B) and } (U+007D)>'
    ;
    
verbatim_balanced_text
    : verbatim_balanced_text_part+
    ;

verbatim_balanced_text_part
    : single_verbatim_balanced_text_character
    | comment
    | '@' identifier_or_keyword
    | string_literal
    | interpolated_string_literal
    | '(' verbatim_balanced_text ')'
    | '[' verbatim_balanced_text ']'
    | '{' verbatim_balanced_text '}'
    ;
    
single_verbatim_balanced_text_character
    : '<Any character except / (U+002F), @ (U+0040), \" (U+0022), $ (U+0024), ( (U+0028), ) (U+0029), [ (U+005B), ] (U+005D), { (U+007B) and } (U+007D)>'
    | '</ (U+002F), if not directly followed by / (U+002F) or * (U+002A)>'
    ;
```

*interpolated_string_literal* 토큰 여러 토큰 및 기타 나타나는 순서 대로 요소를 다음과 같이 입력 하는 대로 해석 되는 *interpolated_string_literal*:

* 다음의 항목은 별도 개별 토큰으로 다시 해석: 앞에 오는 `$` 부호 *interpolated_regular_string_whole*, *interpolated_regular_string_start*, *interpolated_regular_string_mid*하십시오 *interpolated_regular_string_end*하십시오 *interpolated_verbatim_string_whole*,  *interpolated_verbatim_string_start*하십시오 *interpolated_verbatim_string_mid* 하 고 *interpolated_verbatim_string_end*합니다.
* 횟수 *regular_balanced_text* 하 고 *verbatim_balanced_text* 이들 사이 다시 처리로 *input_section* ([어휘 분석 ](lexical-structure.md#lexical-analysis)) 및 입력 요소의 결과 시퀀스로 해석 됩니다. 다시 해석 됩니다 보간된 문자열 리터럴 토큰에 포함 될 수 있습니다 이러한 합니다.

구문 분석에 토큰을 다시 결합 합니다는 *interpolated_string_expression* ([보간된 문자열](expressions.md#interpolated-strings)).

TODO 예제


#### <a name="the-null-literal"></a>Null 리터럴

```antlr
null_literal
    : 'null'
    ;
```

합니다 *null_literal* 참조 형식 또는 nullable 형식에 암시적으로 변환할 수 있습니다.

### <a name="operators-and-punctuators"></a>연산자 및 문장 부호

연산자 및 문장 부호의 몇 가지 종류가 있습니다. 연산자는 식에서 하나 이상의 피연산자와 관련 된 작업을 설명 하기 위해 사용 됩니다. 예를 들어 식 `a + b` 사용 하는 `+` 연산자는 두 피연산자를 추가할 `a` 및 `b`합니다. 문장 부호를 그룹화 하 고 분리 됩니다.

```antlr
operator_or_punctuator
    : '{'  | '}'  | '['  | ']'  | '('   | ')'  | '.'  | ','  | ':'  | ';'
    | '+'  | '-'  | '*'  | '/'  | '%'   | '&'  | '|'  | '^'  | '!'  | '~'
    | '='  | '<'  | '>'  | '?'  | '??'  | '::' | '++' | '--' | '&&' | '||'
    | '->' | '==' | '!=' | '<=' | '>='  | '+=' | '-=' | '*=' | '/=' | '%='
    | '&=' | '|=' | '^=' | '<<' | '<<=' | '=>'
    ;

right_shift
    : '>>'
    ;

right_shift_assignment
    : '>>='
    ;
```

세로 막대는 합니다 *right_shift* 하 고 *right_shift_assignment* 프로덕션 구문 문법에서 어떤 종류의 문자가 없는 다른 프로덕션 달리 (하더라도 나타내는 데 사용 됩니다 공백) 토큰 사이 허용 됩니다. 이러한 프로덕션을 올바르게 처리할 수 있도록 특별히 처리할지 *type_parameter_list*s ([형식 매개 변수](classes.md#type-parameters)).

## <a name="pre-processing-directives"></a>전처리 지시문

전처리 지시문은 조건부로 보고서 오류 및 경고 조건에 소스 파일의 섹션을 건너뛸 소스 코드의 고유 영역을 설명 하는 기능을 제공 합니다. "전처리 지시문" 라는 용어는 C 및 c + + 프로그래밍 언어를 사용 하 여 일관성을 위해서만 사용 됩니다. C#의 경우에 없는 별도 사전 처리 단계 전처리 지시문 어휘 분석 단계의 일부로 처리 됩니다.

```antlr
pp_directive
    : pp_declaration
    | pp_conditional
    | pp_line
    | pp_diagnostic
    | pp_region
    | pp_pragma
    ;
```

다음 전처리 지시문을 사용할 수 있습니다.

*  `#define` 및 `#undef`를 정의 조건부 컴파일 기호를 각각 정의 하는 데 사용 되는 ([선언 지시문](lexical-structure.md#declaration-directives)).
*  `#if`를 `#elif`, `#else`, 및 `#endif`, 조건에 따라 소스 코드의 섹션을 건너뛸 하는 데 사용 되는 ([조건부 컴파일 지시문](lexical-structure.md#conditional-compilation-directives)).
*  `#line`에 오류와 경고를 생성 하는 줄 번호를 제어 하는 데 사용 됩니다 ([지시문을 줄](lexical-structure.md#line-directives)).
*  `#error` 및 `#warning`을 오류 및 경고를 각각 실행 하는 데 사용 되는 ([진단 지시문](lexical-structure.md#diagnostic-directives)).
*  `#region` 및 `#endregion`를 명시적으로 소스 코드의 섹션을 표시 하는 데 사용 되는 ([Region 지시문](lexical-structure.md#region-directives)).
*  `#pragma`에 컴파일러에 선택적 컨텍스트 정보를 지정 하는 데 사용 됩니다 ([Pragma 지시문](lexical-structure.md#pragma-directives)).

전처리 지시문은 항상 별도의 소스 코드 줄을 차지 하며 항상 시작을 `#` 문자 및 전처리 지시문 이름입니다. 앞에 공백이 있을 수 있습니다는 `#` 문자 및는 `#` 문자와 지시문 이름.

포함 하는 소스 줄을 `#define`, `#undef`, `#if`, `#elif`를 `#else`를 `#endif`, `#line`, 또는 `#endregion` 지시문 줄 주석으로 종료 될 수 있습니다. 주석 구분 (의 `/* */` 주석의 스타일) 전처리 지시문이 포함 된 소스 줄에서 허용 되지 않습니다.

전처리 지시문은 토큰이 및 C#의 구문 문법의 일부가 아닙니다. 그러나 전처리 지시문 포함 하거나 제외할 토큰 시퀀스로 사용할 수 있으며 해당 방식으로 영향을 줄 수는 C# 프로그램의 의미 합니다. 예를 들어, 프로그램을 컴파일할 때:
```csharp
#define A
#undef B

class C
{
#if A
    void F() {}
#else
    void G() {}
#endif

#if B
    void H() {}
#else
    void I() {}
#endif
}
```
프로그램으로 토큰의 정확한 순서에 결과:
```csharp
class C
{
    void F() {}
    void I() {}
}
```

따라서 어휘, 두 프로그램은 매우 다르므로 구문상, 반면 동일 합니다.

### <a name="conditional-compilation-symbols"></a>조건부 컴파일 기호

제공 하는 조건부 컴파일 기능을 `#if`, `#elif`를 `#else`, 및 `#endif` 지시문은 전처리 다음 식을 통해 제어 됩니다 ([전처리 식](lexical-structure.md#pre-processing-expressions)) 및 조건부 컴파일 기호입니다.

```antlr
conditional_symbol
    : '<Any identifier_or_keyword except true or false>'
    ;
```

조건부 컴파일 기호는 두 가지 가능한 상태: ***정의*** 하거나 ***정의 되지 않은***합니다. 소스 파일의 어휘 처리를 시작할 때 조건부 컴파일 기호를 하지 않는 정의 외부 메커니즘 (예: 명령줄 컴파일러 옵션)에 의해 명시적으로 정의 되었습니다. 경우는 `#define` 지시문 처리 하는 해당 지시문에 명명 된 조건부 컴파일 기호를 해당 소스 파일에 정의 됩니다. 기호 정의 될 때까지 계속는 `#undef` 소스 파일의 끝에 도달할 때까지 또는 처리 되는 동일한 기호에 대 한 지시문입니다. 이 사항의 시사점 `#define` 및 `#undef` 하나의 소스 파일의 지시문 동일한 프로그램에서 다른 소스 파일에 영향을 주지 합니다.

정의 된 조건부 컴파일 기호를 부울 값이 사전 처리 하는 식에서 참조 하는 경우 `true`, 정의 되지 않은 조건부 컴파일 기호를 부울 값이 있고 `false`합니다. 요구 사항은 없습니다 전처리 식에서 참조 된 전에 선언 명시적으로 조건부 컴파일 기호 되도록 합니다. 대신, 선언 되지 않은 기호는 단순히 정의 되지 있고 따라서 값 `false`합니다.

조건부 컴파일 기호에 대 한 네임 스페이스를 고유 되어 C# 프로그램에서 명명 된 기타 모든 엔터티를 분리 합니다. 조건부 컴파일 기호에서 참조할 수 있습니다 `#define` 고 `#undef` 지시문 및 전처리 식입니다.

### <a name="pre-processing-expressions"></a>전처리 식

전처리 식에서 발생할 수 있습니다 `#if` 고 `#elif` 지시문입니다. 연산자 `!`, `==`를 `!=`, `&&` 및 `||` 전처리 식에서 허용 됩니다 및 그룹화에 대 한 괄호를 사용할 수 있습니다.

```antlr
pp_expression
    : whitespace? pp_or_expression whitespace?
    ;

pp_or_expression
    : pp_and_expression
    | pp_or_expression whitespace? '||' whitespace? pp_and_expression
    ;

pp_and_expression
    : pp_equality_expression
    | pp_and_expression whitespace? '&&' whitespace? pp_equality_expression
    ;

pp_equality_expression
    : pp_unary_expression
    | pp_equality_expression whitespace? '==' whitespace? pp_unary_expression
    | pp_equality_expression whitespace? '!=' whitespace? pp_unary_expression
    ;

pp_unary_expression
    : pp_primary_expression
    | '!' whitespace? pp_unary_expression
    ;

pp_primary_expression
    : 'true'
    | 'false'
    | conditional_symbol
    | '(' whitespace? pp_expression whitespace? ')'
    ;
```

정의 된 조건부 컴파일 기호를 부울 값이 사전 처리 하는 식에서 참조 하는 경우 `true`, 정의 되지 않은 조건부 컴파일 기호를 부울 값이 있고 `false`합니다.

항상 사전 처리 식의 평가는 부울 값을 생성합니다. 사전 처리 하는 식 계산 규칙은 상수 식에 대 한 것과 동일 ([상수 식](expressions.md#constant-expressions))는 사용자 정의 된 엔터티만 참조할 수 있는 조건부 컴파일 기호는 점을 제외 하 고, .

### <a name="declaration-directives"></a>선언 지시문

선언 지시문은 조건부 컴파일 기호를 정의 또는 정의 해제 하는 데 사용 됩니다.

```antlr
pp_declaration
    : whitespace? '#' whitespace? 'define' whitespace conditional_symbol pp_new_line
    | whitespace? '#' whitespace? 'undef' whitespace conditional_symbol pp_new_line
    ;

pp_new_line
    : whitespace? single_line_comment? new_line
    ;
```

처리는 `#define` 지시문 하면 정의 된 상태가 지정 된 조건부 컴파일 기호 지시문 뒤에 오는 소스 줄을 사용 하 여 시작 합니다. 마찬가지로 처리는 `#undef` 지시문으로 인해 정의 되지 않은 지시문 뒤에 오는 소스 줄을 사용 하 여 시작 되도록 지정 된 조건부 컴파일 기호입니다.

모든 `#define` 하 고 `#undef` 소스 파일의 지시문은 첫 번째 앞에 있어야 합니다. *토큰* ([토큰](lexical-structure.md#tokens)) 원본 파일의 그렇지 않으면 컴파일 타임 오류가 발생 합니다. 직관적인 말해 `#define` 및 `#undef` 지시문 소스 파일의 "실제 코드"를 빨라야 합니다.

예제:
```csharp
#define Enterprise

#if Professional || Enterprise
    #define Advanced
#endif

namespace Megacorp.Data
{
    #if Advanced
    class PivotTable {...}
    #endif
}
```
유효 하기 때문에 `#define` 지시문의 첫 번째 토큰 앞에 야 (합니다 `namespace` 키워드) 소스 파일에서.

때문에 다음 예제에서는 컴파일 타임 오류가 발생 한 `#define` 실제 코드를 따릅니다.
```csharp
#define A
namespace N
{
    #define B
    #if B
    class Class1 {}
    #endif
}
```

A `#define` 모든 중간 있을 하지 않고 이미 정의 되어 있는 조건부 컴파일 기호를 정의할 수 있습니다 `#undef` 해당 기호에 대 한 합니다. 조건부 컴파일 기호를 정의 하는 아래 예제에서는 `A` 다음 다시 정의 합니다.
```csharp
#define A
#define A
```

`#undef` 있습니다 "해제" 정의 되지 않은 조건부 컴파일 기호를 합니다. 아래 예제에서는 조건부 컴파일 기호를 정의 `A` 다음 하지만 두 번 해제 하 고 두 번째 `#undef` 효과도 없으며, 여전히 유효 합니다.
```csharp
#define A
#undef A
#undef A
```

### <a name="conditional-compilation-directives"></a>조건부 컴파일 지시문

조건부 컴파일 지시문은 조건부로 포함 하거나 소스 파일 부분을 제외 하는 데 사용 됩니다.

```antlr
pp_conditional
    : pp_if_section pp_elif_section* pp_else_section? pp_endif
    ;

pp_if_section
    : whitespace? '#' whitespace? 'if' whitespace pp_expression pp_new_line conditional_section?
    ;

pp_elif_section
    : whitespace? '#' whitespace? 'elif' whitespace pp_expression pp_new_line conditional_section?
    ;

pp_else_section:
    | whitespace? '#' whitespace? 'else' pp_new_line conditional_section?
    ;

pp_endif
    : whitespace? '#' whitespace? 'endif' pp_new_line
    ;

conditional_section
    : input_section
    | skipped_section
    ;

skipped_section
    : skipped_section_part+
    ;

skipped_section_part
    : skipped_characters? new_line
    | pp_directive
    ;

skipped_characters
    : whitespace? not_number_sign input_character*
    ;

not_number_sign
    : '<Any input_character except #>'
    ;
```

구문에 표시 된 대로 조건부 컴파일 지시문의 순서로 구성 된 집합으로 작성 되어야 합니다는 `#if` 지시문을 0 개 이상의 `#elif` 지시문, 0 또는 1 `#else` 지시문 및 `#endif` 지시문입니다. 지시문 사이의 소스 코드의 조건부 섹션이 있습니다. 각 섹션 바로 앞 지시문에 의해 제어 됩니다. 조건부 섹션을 자체 포함 될 수 중첩 된 조건부 컴파일 지시문 완전 한 집합을 형성 하는 이러한 지시문 제공 합니다.

A *pp_conditional* 포함 된 중 하나만 선택 *conditional_section*어휘 정상적인 처리에 대 한 s:

*  *pp_expression*의 합니다 `#if` 하 고 `#elif` 지시문 하나 생성 될 때까지 순서 대로 평가 됩니다 `true`합니다. 식을 생성 하는 경우 `true`서 *conditional_section* 해당 지시문을 선택 합니다.
*  모든 *pp_expression*s yield `false`, 경우에 `#else` 지시문을 사용할 수 있는지를 *conditional_section* 의 `#else` 지시문을 선택 합니다.
*  그렇지 않으면, 아니요 *conditional_section* 을 선택 합니다.

선택한 *conditional_section*정상으로 처리 되는 있는 경우 *input_section*: 어휘 문법 섹션에 포함 된 소스 코드를 준수 해야 합니다; 원본의 토큰이 생성 됩니다 섹션의 코드 있고 섹션에서 전처리 지시문 효력을 발휘 합니다.

나머지 *conditional_section*s에 있는 경우으로 처리 됩니다 *skipped_section*전처리 지시문 제외 하 고 s:, 섹션에서 소스 코드의 어휘를 준수 하지 해야 문법; 아니요 토큰이; 섹션에서 소스 코드에서 생성 됩니다. 및 섹션에서 전처리 지시문 어휘 적으로 정확 해야 하지만 그렇지 않으면 처리 되지 않습니다. 내를 *conditional_section* 으로 처리 되는 *skipped_section*, 모든 중첩 *conditional_section*s (포함 된 중첩 `#if`... `#endif` 고 `#region`... `#endregion` 생성)으로 처리 됩니다 *skipped_section*s입니다.

다음 예제에서는 어떻게 조건부 컴파일을 지시문을 중첩을 보여 줍니다.
```csharp
#define Debug       // Debugging on
#undef Trace        // Tracing off

class PurchaseTransaction
{
    void Commit() {
        #if Debug
            CheckConsistency();
            #if Trace
                WriteToLog(this.ToString());
            #endif
        #endif
        CommitHelper();
    }
}
```

전처리 지시문을 제외 하 고 생략된 된 소스 코드 어휘 분석 적용 되지 않습니다. 예를 들어, 다음은에 종결 되지 않은 주석 불구 하 고 잘못 된 `#else` 섹션:
```csharp
#define Debug        // Debugging on

class PurchaseTransaction
{
    void Commit() {
        #if Debug
            CheckConsistency();
        #else
            /* Do something else
        #endif
    }
}
```

그러나 Note, 전처리 지시문은 소스 코드의 건너뛴된 섹션 에서도 구문적으로 올바른 것으로 필요 합니다.

여러 줄 입력된 요소 내에서 사용 하는 경우에 전처리 지시문 처리 되지 않습니다. 예를 들어 프로그램:
```csharp
class Hello
{
    static void Main() {
        System.Console.WriteLine(@"hello, 
#if Debug
        world
#else
        Nebraska
#endif
        ");
    }
}
```
출력 결과:
```
hello,
#if Debug
        world
#else
        Nebraska
#endif
```

평가에 따라 달라질 수 있습니다 처리 되는 전처리 지시문 집합이 특이 한 경우에는 *pp_expression*합니다. 예제:
```csharp
#if X
    /*
#else
    /* */ class Q { }
#endif
```
항상 동일한 토큰 스트림을 생성 (`class` `Q` `{` `}`)의 여부에 관계 없이 `X` 정의 됩니다. 경우 `X` 가 정의 지시문만이 처리 됩니다 `#if` 및 `#endif`때문에 여러 줄 주석. 경우 `X` 는 정의 되지 않은 다음 세 가지 지시문 (`#if`, `#else`, `#endif`) 지시문 집합의 일부가 됩니다.

### <a name="diagnostic-directives"></a>진단 지시문

진단 지시문을 사용 하 여 명시적으로 오류 및 기타 컴파일 시간 오류 및 경고와 마찬가지로에 보고 되는 경고 메시지를 생성 합니다.

```antlr
pp_diagnostic
    : whitespace? '#' whitespace? 'error' pp_message
    | whitespace? '#' whitespace? 'warning' pp_message
    ;

pp_message
    : new_line
    | whitespace input_character* new_line
    ;
```

예제:
```csharp
#warning Code review needed before check-in

#if Debug && Retail
    #error A build can't be both debug and retail
#endif

class Test {...}
```
항상 ("코드 검토 체크 인하기 전에 필요한"), 경고를 생성 하 고 컴파일 시간 오류를 생성 ("빌드 수 없음 디버그와 일반 정품") 하는 경우 조건부 기호 `Debug` 및 `Retail` 가 둘 다 정의 합니다. 한 *pp_message* 임의의 텍스트를 포함할 수 있습니다; 특히이 필요 없습니다 잘 구성 된 토큰을 단어의 작은따옴표에 표시 된 대로 `can't`입니다.

### <a name="region-directives"></a>Region 지시문

Region 지시문은 명시적으로 소스 코드의 영역을 표시 하는 데 사용 됩니다.

```antlr
pp_region
    : pp_start_region conditional_section? pp_end_region
    ;

pp_start_region
    : whitespace? '#' whitespace? 'region' pp_message
    ;

pp_end_region
    : whitespace? '#' whitespace? 'endregion' pp_message
    ;
```

의미 없는 지역;에 연결 된 지역 사용 됩니다 프로그래머가 또는 자동화 된 도구로 소스 코드의 섹션을 표시 합니다. 에 지정 된 메시지를 `#region` 또는 `#endregion` 지시문 마찬가지로 의미가 없는; 지역을 식별할를 으로만 작동 합니다. 일치 하는 `#region` 하 고 `#endregion` 지시문은 다른 있을 *pp_message*s입니다.

영역의 어휘 처리:
```csharp
#region
...
#endregion
```
폼의 조건부 컴파일 지시문을 처리 하는 어휘에 정확 하 게 해당 됩니다.
```csharp
#if true
...
#endif
```

### <a name="line-directives"></a>Line 지시문

줄 지시문 alter 줄 번호 및 소스 파일 이름과 경고 및 오류와 같은 출력에 컴파일러에 의해 보고 되는 호출자 정보 특성에서 사용 되는 데 사용할 수 있습니다 ([호출자 정보 특성](attributes.md#caller-info-attributes)).

줄 지시문을 다른 텍스트 입력에서 C# 소스 코드를 생성 하는 메타 프로그래밍 도구에서 가장 일반적으로 사용 됩니다.

```antlr
pp_line
    : whitespace? '#' whitespace? 'line' whitespace line_indicator pp_new_line
    ;

line_indicator
    : decimal_digit+ whitespace file_name
    | decimal_digit+
    | 'default'
    | 'hidden'
    ;

file_name
    : '"' file_name_character+ '"'
    ;

file_name_character
    : '<Any input_character except ">'
    ;
```

없는 경우 `#line` 지시문이 컴파일러 true 줄 번호 및 소스 파일 이름을 출력으로 보고 합니다. 처리할 때을 `#line` 지시문을 포함 하는 *line_indicator* 없는 `default`, 컴파일러는 지정 된 줄 번호 (및 파일 이름을 지정 하는 경우)으로 지시문 다음 줄을 처리 합니다.

`#line default` 지시문 모든 이전 #line 지시문의 결과 되돌립니다. 없는 것 처럼 정확 하 게 컴파일러가 다음 줄에 대해 true 줄 정보를 보고 `#line` 지시문 처리 했습니다.

`#line hidden` 지시문 파일에 영향을 주지 않으며 오류를 보고 하는 줄 번호 메시지를 하지만 소스 수준 디버깅 하는 영향 을지 않습니다. 사이 모든 줄을 디버깅할 때를 `#line hidden` 지시문과 후속 `#line` 지시문 (없는 `#line hidden`) 줄 번호 정보가 없습니다. 디버거에서 코드를 단계별로 실행할 때 이러한 줄 전적으로 건너뜁니다.

*file_name* 와 달리 일반 문자열 리터럴에서 이스케이프 문자 처리 되지 않습니다;는 "`\`"는 일반적인 백슬래시 문자를 단순히 지정 하는 문자는 *file_name*.

### <a name="pragma-directives"></a>Pragma 지시문

`#pragma` 전처리 지시문은 컴파일러 위한 선택적 컨텍스트 정보를 지정 하는 데 사용 됩니다. 에 제공 된 정보는 `#pragma` 지시문 프로그램 의미 체계를 변경 되지 것입니다.

```antlr
pp_pragma
    : whitespace? '#' whitespace? 'pragma' whitespace pragma_body pp_new_line
    ;

pragma_body
    : pragma_warning_body
    ;
```

C#은 제공 `#pragma` 컴파일러 경고를 제어 하는 지시문입니다. 이후 버전의 언어를 추가로 포함 될 수 있습니다 `#pragma` 지시문입니다. 하지만 다른 C# 컴파일러와의 상호 운용성을 위해 Microsoft C# 컴파일러에 알 수 없는 컴파일 오류가 발생 하지 않습니다 `#pragma` 지시문; 경고를 생성 이러한 지시문 수행 합니다.

#### <a name="pragma-warning"></a>Pragma 경고

`#pragma warning` 후속 프로그램 텍스트를 컴파일하는 동안 메시지 경고의 특정 집합 또는 사용 하지 않도록 설정 하거나 모든 복원 지시문 데 사용 됩니다.

```antlr
pragma_warning_body
    : 'warning' whitespace warning_action
    | 'warning' whitespace warning_action whitespace warning_list
    ;

warning_action
    : 'disable'
    | 'restore'
    ;

warning_list
    : decimal_digit+ (whitespace? ',' whitespace? decimal_digit+)*
    ;
```

`#pragma warning` 지시문 경고 목록을 생략 하는 모든 경고에 영향을 줍니다. `#pragma warning` 지시문을 포함 경고 목록에 목록에 지정 된 경고에만 영향을 줍니다.

`#pragma warning disable` 모든 지시문 비활성화 또는 지정된 된 경고 집합.

`#pragma warning restore` 모든 지시문 복원 또는 컴파일 단위의 시작 부분에 적용 된 상태 경고의 지정된 된 집합입니다. 특정 경고를 외부에서 비활성화 된 경우, `#pragma warning restore` (모든 여부 또는 특정 경고) 해당 경고를 다시 활성화 되지 않습니다.

다음 예제에서는 사용 방법을 보여 줍니다. `#pragma warning` 일시적으로 경고를 해제 하려면 보고 사용 되지 않습니다 하는 경우 Microsoft C# 컴파일러에서 경고 번호를 사용 하 여 멤버가 참조 되기 합니다.
```csharp
using System;

class Program
{
    [Obsolete]
    static void Foo() {}

    static void Main() {
#pragma warning disable 612
    Foo();
#pragma warning restore 612
    }
}
```
