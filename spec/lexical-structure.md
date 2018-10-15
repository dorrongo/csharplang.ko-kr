# <a name="lexical-structure"></a><span data-ttu-id="19a96-101">어휘 구조</span><span class="sxs-lookup"><span data-stu-id="19a96-101">Lexical structure</span></span>

## <a name="programs"></a><span data-ttu-id="19a96-102">Programs</span><span class="sxs-lookup"><span data-stu-id="19a96-102">Programs</span></span>

<span data-ttu-id="19a96-103">C# ***프로그램*** 하나 이상의 구성 ***파일만***공식적으로 알려진 ***컴파일 단위*** ([컴파일 단위](namespaces.md#compilation-units)).</span><span class="sxs-lookup"><span data-stu-id="19a96-103">A C# ***program*** consists of one or more ***source files***, known formally as ***compilation units*** ([Compilation units](namespaces.md#compilation-units)).</span></span> <span data-ttu-id="19a96-104">소스 파일은 유니코드 문자 시퀀스를 정렬된 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-104">A source file is an ordered sequence of Unicode characters.</span></span> <span data-ttu-id="19a96-105">소스 파일 일반적으로 파일을 사용 하 여 일대일로 대응 파일 시스템에 있지만이 대응 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-105">Source files typically have a one-to-one correspondence with files in a file system, but this correspondence is not required.</span></span> <span data-ttu-id="19a96-106">최대 이식성을 얻으려면 파일 시스템에서 파일을 u t F-8로 인코딩할 수는 것이 좋습니다 인코딩.</span><span class="sxs-lookup"><span data-stu-id="19a96-106">For maximal portability, it is recommended that files in a file system be encoded with the UTF-8 encoding.</span></span>

<span data-ttu-id="19a96-107">개념적인 측면에서 말하자면 컴파일되면 해당 프로그램은 세 가지 단계를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="19a96-107">Conceptually speaking, a program is compiled using three steps:</span></span>

1. <span data-ttu-id="19a96-108">변환 파일을 인코딩 체계를 특정 문자 레퍼토리가 상당히에서 유니코드 문자 시퀀스로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-108">Transformation, which converts a file from a particular character repertoire and encoding scheme into a sequence of Unicode characters.</span></span>
2. <span data-ttu-id="19a96-109">토큰 스트림의 입력된 유니코드 문자 스트림을 변환 하는 어휘 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-109">Lexical analysis, which translates a stream of Unicode input characters into a stream of tokens.</span></span>
3. <span data-ttu-id="19a96-110">토큰 스트림을 실행 코드로 변환 하는 구문 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-110">Syntactic analysis, which translates the stream of tokens into executable code.</span></span>

## <a name="grammars"></a><span data-ttu-id="19a96-111">문법</span><span class="sxs-lookup"><span data-stu-id="19a96-111">Grammars</span></span>

<span data-ttu-id="19a96-112">이 사양은 두 문법을 사용 하 여 C# 프로그래밍 언어의 구문을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-112">This specification presents the syntax of the C# programming language using two grammars.</span></span> <span data-ttu-id="19a96-113">합니다 ***어휘 문법*** ([어휘 문법](lexical-structure.md#lexical-grammar)) 유니코드 문자 형식 줄 종결자, 공백, 설명, 토큰 및 전처리 지시문을 결합 하는 방법을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-113">The ***lexical grammar*** ([Lexical grammar](lexical-structure.md#lexical-grammar)) defines how Unicode characters are combined to form line terminators, white space, comments, tokens, and pre-processing directives.</span></span> <span data-ttu-id="19a96-114">합니다 ***구문 문법*** ([구문 문법](lexical-structure.md#syntactic-grammar)) 프로그램을 만들기 위해 C# 어휘 문법의 결과 토큰을 결합 하는 방법을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-114">The ***syntactic grammar*** ([Syntactic grammar](lexical-structure.md#syntactic-grammar)) defines how the tokens resulting from the lexical grammar are combined to form C# programs.</span></span>

### <a name="grammar-notation"></a><span data-ttu-id="19a96-115">문법 표기법</span><span class="sxs-lookup"><span data-stu-id="19a96-115">Grammar notation</span></span>

<span data-ttu-id="19a96-116">어휘 및 구문 문법 ANTLR 문법 도구의 표기법을 사용 하 여 Backus Naur 폼에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-116">The lexical and syntactic grammars are presented in Backus-Naur form using the notation of the ANTLR grammar tool.</span></span>

### <a name="lexical-grammar"></a><span data-ttu-id="19a96-117">어휘 문법</span><span class="sxs-lookup"><span data-stu-id="19a96-117">Lexical grammar</span></span>

<span data-ttu-id="19a96-118">C#의 어휘 문법에서 제공 됩니다 [어휘 분석](lexical-structure.md#lexical-analysis)를 [토큰](lexical-structure.md#tokens), 및 [전처리 지시문](lexical-structure.md#pre-processing-directives)합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-118">The lexical grammar of C# is presented in [Lexical analysis](lexical-structure.md#lexical-analysis), [Tokens](lexical-structure.md#tokens), and [Pre-processing directives](lexical-structure.md#pre-processing-directives).</span></span> <span data-ttu-id="19a96-119">어휘 문법의 터미널 기호는 유니코드 문자 집합의 문자 및 어휘 문법 문자 형식 토큰에 결합 하는 방법을 지정 합니다 ([토큰](lexical-structure.md#tokens)), 공백 ([공백을](lexical-structure.md#white-space)), 주석 ([주석](lexical-structure.md#comments)), 전처리 지시문 및 ([전처리 지시문](lexical-structure.md#pre-processing-directives)).</span><span class="sxs-lookup"><span data-stu-id="19a96-119">The terminal symbols of the lexical grammar are the characters of the Unicode character set, and the lexical grammar specifies how characters are combined to form tokens ([Tokens](lexical-structure.md#tokens)), white space ([White space](lexical-structure.md#white-space)), comments ([Comments](lexical-structure.md#comments)), and pre-processing directives ([Pre-processing directives](lexical-structure.md#pre-processing-directives)).</span></span>

<span data-ttu-id="19a96-120">C# 프로그램의 모든 소스 파일을 따라야 합니다 *입력* 어휘 문법의 프로덕션 ([어휘 분석](lexical-structure.md#lexical-analysis)).</span><span class="sxs-lookup"><span data-stu-id="19a96-120">Every source file in a C# program must conform to the *input* production of the lexical grammar ([Lexical analysis](lexical-structure.md#lexical-analysis)).</span></span>

### <a name="syntactic-grammar"></a><span data-ttu-id="19a96-121">구문 문법</span><span class="sxs-lookup"><span data-stu-id="19a96-121">Syntactic grammar</span></span>

<span data-ttu-id="19a96-122">C#의 구문 문법 장과이 챕터를 참조 하는 부록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-122">The syntactic grammar of C# is presented in the chapters and appendices that follow this chapter.</span></span> <span data-ttu-id="19a96-123">구문 문법의 터미널 기호는 어휘 문법에서 정의한 토큰 및 구문 문법 토큰 C# 프로그램을 만들기 위해 결합 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-123">The terminal symbols of the syntactic grammar are the tokens defined by the lexical grammar, and the syntactic grammar specifies how tokens are combined to form C# programs.</span></span>

<span data-ttu-id="19a96-124">C# 프로그램의 모든 소스 파일을 따라야 합니다 *compilation_unit* 구문 문법의 프로덕션 ([컴파일 단위](namespaces.md#compilation-units)).</span><span class="sxs-lookup"><span data-stu-id="19a96-124">Every source file in a C# program must conform to the *compilation_unit* production of the syntactic grammar ([Compilation units](namespaces.md#compilation-units)).</span></span>

## <a name="lexical-analysis"></a><span data-ttu-id="19a96-125">어휘 분석</span><span class="sxs-lookup"><span data-stu-id="19a96-125">Lexical analysis</span></span>

<span data-ttu-id="19a96-126">합니다 *입력* 프로덕션 C# 소스 파일의 어휘 구조를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-126">The *input* production defines the lexical structure of a C# source file.</span></span> <span data-ttu-id="19a96-127">C# 프로그램의 각 소스 파일은이 어휘 문법 프로덕션에 맞아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-127">Each source file in a C# program must conform to this lexical grammar production.</span></span>

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

<span data-ttu-id="19a96-128">5 개의 기본 요소로 C# 소스 파일의 어휘 구조를 구성: 줄 종결자 ([줄 종결자](lexical-structure.md#line-terminators)), 공백 ([공백](lexical-structure.md#white-space)), 주석 ([주석](lexical-structure.md#comments)), 토큰 ([토큰](lexical-structure.md#tokens)), 전처리 지시문 및 ([전처리 지시문](lexical-structure.md#pre-processing-directives)).</span><span class="sxs-lookup"><span data-stu-id="19a96-128">Five basic elements make up the lexical structure of a C# source file: Line terminators ([Line terminators](lexical-structure.md#line-terminators)), white space ([White space](lexical-structure.md#white-space)), comments ([Comments](lexical-structure.md#comments)), tokens ([Tokens](lexical-structure.md#tokens)), and pre-processing directives ([Pre-processing directives](lexical-structure.md#pre-processing-directives)).</span></span> <span data-ttu-id="19a96-129">이러한 기본 요소를 토큰만 C# 프로그램의 구문 문법에서 중요 한 ([구문 문법](lexical-structure.md#syntactic-grammar)).</span><span class="sxs-lookup"><span data-stu-id="19a96-129">Of these basic elements, only tokens are significant in the syntactic grammar of a C# program ([Syntactic grammar](lexical-structure.md#syntactic-grammar)).</span></span>

<span data-ttu-id="19a96-130">C# 원본 파일을 처리 하는 어휘 파일 구문 분석에 대 한 입력 되는 토큰의 시퀀스로 줄이는 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-130">The lexical processing of a C# source file consists of reducing the file into a sequence of tokens which becomes the input to the syntactic analysis.</span></span> <span data-ttu-id="19a96-131">줄 종결자, 공백 및 주석 토큰을 구분 하는 사용 될 수 있습니다 및 전처리 지시문 수는 건너 원본 파일의 섹션 시키지만 이러한 어휘 요소는 C# 프로그램의 구문 구조에 영향을 미치지 하는 그렇지 않은 경우.</span><span class="sxs-lookup"><span data-stu-id="19a96-131">Line terminators, white space, and comments can serve to separate tokens, and pre-processing directives can cause sections of the source file to be skipped, but otherwise these lexical elements have no impact on the syntactic structure of a C# program.</span></span>

<span data-ttu-id="19a96-132">보간된 문자열 리터럴의 경우 ([보간된 문자열 리터럴을](lexical-structure.md#interpolated-string-literals)) 단일 토큰 어휘 분석을 통해 처음에 생성 되지만 나뉩니다 어휘 분석 반복적으로 적용 되는 여러 입력된 요소 까지 모든 보간된 문자열 리터럴을 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-132">In the case of interpolated string literals ([Interpolated string literals](lexical-structure.md#interpolated-string-literals)) a single token is initially produced by lexical analysis, but is broken up into several input elements which are repeatedly subjected to lexical analysis until all interpolated string literals have been resolved.</span></span> <span data-ttu-id="19a96-133">결과 토큰을 구문 분석에 대 한 입력으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-133">The resulting tokens then serve as input to the syntactic analysis.</span></span>

<span data-ttu-id="19a96-134">어휘 문법 요소를 여러 소스 파일의 문자 시퀀스로 일치 하는 경우 어휘 처리를 통해 가장 긴 가능한 어휘 요소를 형성 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-134">When several lexical grammar productions match a sequence of characters in a source file, the lexical processing always forms the longest possible lexical element.</span></span> <span data-ttu-id="19a96-135">예를 들어 문자 시퀀스 `//` 어휘 요소는 단일 보다 길기 때문에 한 줄 주석의 시작으로 처리 됩니다 `/` 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-135">For example, the character sequence `//` is processed as the beginning of a single-line comment because that lexical element is longer than a single `/` token.</span></span>

### <a name="line-terminators"></a><span data-ttu-id="19a96-136">줄 종결자</span><span class="sxs-lookup"><span data-stu-id="19a96-136">Line terminators</span></span>

<span data-ttu-id="19a96-137">줄 종결자는 줄을 C# 소스 파일의 문자를 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-137">Line terminators divide the characters of a C# source file into lines.</span></span>

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

<span data-ttu-id="19a96-138">호환 소스 코드 파일의 끝 표시자를 추가 하는 편집 도구 제대로 시퀀스로 표시 하는 파일을 소스를 사용 하도록 설정 하려면 줄을 종료 하 고에 대 한 C# 프로그램의 모든 소스 파일에 순서 대로 다음과 같은 변환이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-138">For compatibility with source code editing tools that add end-of-file markers, and to enable a source file to be viewed as a sequence of properly terminated lines, the following transformations are applied, in order, to every source file in a C# program:</span></span>

*  <span data-ttu-id="19a96-139">소스 파일의 마지막 문자 Z 제어 문자가 문자 인지 (`U+001A`),이 문자를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-139">If the last character of the source file is a Control-Z character (`U+001A`), this character is deleted.</span></span>
*  <span data-ttu-id="19a96-140">캐리지 리턴 문자 (`U+000D`) 및 소스 파일의 마지막 문자는 캐리지 리턴 없는 경우 해당 원본 파일은 비어 있지 않은 경우 소스 파일의 끝에 추가 됩니다 (`U+000D`), 줄 바꿈 (`U+000A`), 줄 구분 기호 (`U+2028`), 또는 단락 구분 기호 (`U+2029`).</span><span class="sxs-lookup"><span data-stu-id="19a96-140">A carriage-return character (`U+000D`) is added to the end of the source file if that source file is non-empty and if the last character of the source file is not a carriage return (`U+000D`), a line feed (`U+000A`), a line separator (`U+2028`), or a paragraph separator (`U+2029`).</span></span>

### <a name="comments"></a><span data-ttu-id="19a96-141">설명</span><span class="sxs-lookup"><span data-stu-id="19a96-141">Comments</span></span>

<span data-ttu-id="19a96-142">두 가지 형태의 주석이 지원 됩니다: 단일 줄 주석 및 구분 기호로 분리 된 주석입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-142">Two forms of comments are supported: single-line comments and delimited comments.</span></span> <span data-ttu-id="19a96-143">***한 줄 주석이*** 문자로 시작 `//` 하 고 소스 줄의 끝에 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-143">***Single-line comments*** start with the characters `//` and extend to the end of the source line.</span></span> <span data-ttu-id="19a96-144">***주석 구분*** 문자를 사용 하 여 시작 `/*` 및 끝 문자를 사용 하 여 `*/`입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-144">***Delimited comments*** start with the characters `/*` and end with the characters `*/`.</span></span> <span data-ttu-id="19a96-145">구분 기호로 분리 된 주석 여러 줄으로 나누어 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-145">Delimited comments may span multiple lines.</span></span>

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

<span data-ttu-id="19a96-146">주석을 중첩 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="19a96-146">Comments do not nest.</span></span> <span data-ttu-id="19a96-147">문자 시퀀스 `/*` 및 `*/` 내에서 특별 한 의미가 `//` 주석 처리 및 문자 시퀀스 `//` 및 `/*` 구분 기호로 분리 된 주석 내에서 특별 한 의미가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-147">The character sequences `/*` and `*/` have no special meaning within a `//` comment, and the character sequences `//` and `/*` have no special meaning within a delimited comment.</span></span>

<span data-ttu-id="19a96-148">주석 문자 및 문자열 리터럴 내에서 처리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-148">Comments are not processed within character and string literals.</span></span>

<span data-ttu-id="19a96-149">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="19a96-149">The example</span></span>
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
<span data-ttu-id="19a96-150">구분 기호로 분리 된 주석을 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-150">includes a delimited comment.</span></span>

<span data-ttu-id="19a96-151">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="19a96-151">The example</span></span>
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
<span data-ttu-id="19a96-152">여러 줄 주석을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-152">shows several single-line comments.</span></span>

### <a name="white-space"></a><span data-ttu-id="19a96-153">공백</span><span class="sxs-lookup"><span data-stu-id="19a96-153">White space</span></span>

<span data-ttu-id="19a96-154">공백 문자는 유니코드 클래스를 포함 하는 공백 문자 z의 모든 문자 뿐만 아니라 가로 탭 문자, 세로 탭 문자인 및 형식 문자를 피드로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-154">White space is defined as any character with Unicode class Zs (which includes the space character) as well as the horizontal tab character, the vertical tab character, and the form feed character.</span></span>

```antlr
whitespace
    : '<Any character with Unicode class Zs>'
    | '<Horizontal tab character (U+0009)>'
    | '<Vertical tab character (U+000B)>'
    | '<Form feed character (U+000C)>'
    ;
```

## <a name="tokens"></a><span data-ttu-id="19a96-155">토큰</span><span class="sxs-lookup"><span data-stu-id="19a96-155">Tokens</span></span>

<span data-ttu-id="19a96-156">토큰의 몇 가지 종류가 있습니다: 식별자, 키워드, 리터럴, 연산자 및 문장 부호입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-156">There are several kinds of tokens: identifiers, keywords, literals, operators, and punctuators.</span></span> <span data-ttu-id="19a96-157">공백 문자 및 주석은 토큰을 없지만 토큰에 대 한 구분 기호로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-157">White space and comments are not tokens, though they act as separators for tokens.</span></span>

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

### <a name="unicode-character-escape-sequences"></a><span data-ttu-id="19a96-158">유니코드 문자 이스케이프 시퀀스</span><span class="sxs-lookup"><span data-stu-id="19a96-158">Unicode character escape sequences</span></span>

<span data-ttu-id="19a96-159">유니코드 문자 이스케이프 시퀀스를 유니코드 문자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-159">A Unicode character escape sequence represents a Unicode character.</span></span> <span data-ttu-id="19a96-160">유니코드 문자 이스케이프 시퀀스 식별자에서 처리 됩니다 ([식별자](lexical-structure.md#identifiers)), 문자 리터럴 ([문자 리터럴](lexical-structure.md#character-literals)), 및 일반 문자열 리터럴 ([문자열 리터럴](lexical-structure.md#string-literals)).</span><span class="sxs-lookup"><span data-stu-id="19a96-160">Unicode character escape sequences are processed in identifiers ([Identifiers](lexical-structure.md#identifiers)), character literals ([Character literals](lexical-structure.md#character-literals)), and regular string literals ([String literals](lexical-structure.md#string-literals)).</span></span> <span data-ttu-id="19a96-161">다른 위치 (예: 연산자, 문장 부호, 또는 키워드)에 유니코드 문자 이스케이프 처리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-161">A Unicode character escape is not processed in any other location (for example, to form an operator, punctuator, or keyword).</span></span>

```antlr
unicode_escape_sequence
    : '\\u' hex_digit hex_digit hex_digit hex_digit
    | '\\U' hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit
    ;
```

<span data-ttu-id="19a96-162">유니코드 이스케이프 시퀀스를 나타내는 16 진수 숫자 다음 형성 된 단일 유니코드 문자를 "`\u`"또는"`\U`" 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-162">A Unicode escape sequence represents the single Unicode character formed by the hexadecimal number following the "`\u`" or "`\U`" characters.</span></span> <span data-ttu-id="19a96-163">C#을 사용 하는 16 비트 유니코드 코드 포인트에서 문자 및 문자열 값 인코딩을 U + 10ffff 까지의 범위 u+10000에서에서 유니코드 문자는 문자 리터럴에서 허용 되지 않습니다 하 고 유니코드 서로게이트 쌍을 사용 하 여 문자열 리터럴 안에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-163">Since C# uses a 16-bit encoding of Unicode code points in characters and string values, a Unicode character in the range U+10000 to U+10FFFF is not permitted in a character literal and is represented using a Unicode surrogate pair in a string literal.</span></span> <span data-ttu-id="19a96-164">0x10FFFF 위에 코드 포인트를 사용 하 여 유니코드 문자 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-164">Unicode characters with code points above 0x10FFFF are not supported.</span></span>

<span data-ttu-id="19a96-165">여러 변환은 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-165">Multiple translations are not performed.</span></span> <span data-ttu-id="19a96-166">예를 들어, 문자열 리터럴 "`\u005Cu005C`"에 해당 하 는"`\u005C`" 대신 "`\`"입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-166">For instance, the string literal "`\u005Cu005C`" is equivalent to "`\u005C`" rather than "`\`".</span></span> <span data-ttu-id="19a96-167">유니코드 값을 `\u005C` 는 문자 "`\`"입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-167">The Unicode value `\u005C` is the character "`\`".</span></span>

<span data-ttu-id="19a96-168">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="19a96-168">The example</span></span>
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
<span data-ttu-id="19a96-169">몇 가지 사용 방법을 보여 줍니다 `\u0066`, 문자에 대 한 이스케이프 시퀀스는 "`f`"입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-169">shows several uses of `\u0066`, which is the escape sequence for the letter "`f`".</span></span> <span data-ttu-id="19a96-170">프로그램은</span><span class="sxs-lookup"><span data-stu-id="19a96-170">The program is equivalent to</span></span>
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

### <a name="identifiers"></a><span data-ttu-id="19a96-171">식별자</span><span class="sxs-lookup"><span data-stu-id="19a96-171">Identifiers</span></span>

<span data-ttu-id="19a96-172">이 섹션에 제공 된 식별자 규칙을 정확 하 게 일치 해당 권장 Unicode Standard Annex 31를 제외 하 고 밑줄 문자로 초기 (그대로 C 프로그래밍 언어에서 일반적인), 유니코드 이스케이프 시퀀스는 허용 됩니다. 식별자에서 허용 및 "`@`" 키워드를 식별자로 사용할 수 있도록 접두사로 문자는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-172">The rules for identifiers given in this section correspond exactly to those recommended by the Unicode Standard Annex 31, except that underscore is allowed as an initial character (as is traditional in the C programming language), Unicode escape sequences are permitted in identifiers, and the "`@`" character is allowed as a prefix to enable keywords to be used as identifiers.</span></span>

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

<span data-ttu-id="19a96-173">위에서 언급 한 유니코드 문자 클래스에 대 한 자세한 내용은 유니코드 표준, 버전 3.0, 4.5 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="19a96-173">For information on the Unicode character classes mentioned above, see The Unicode Standard, Version 3.0, section 4.5.</span></span>

<span data-ttu-id="19a96-174">유효한 식별자의 예로 "`identifier1`","`_identifier2`", 및 "`@if`"입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-174">Examples of valid identifiers include "`identifier1`", "`_identifier2`", and "`@if`".</span></span>

<span data-ttu-id="19a96-175">표준에 맞는 프로그램 식별자는 Unicode Standard Annex 15에 정의 된 대로 유니코드 정규화 형식 C에서 정의 된 정규 형식에서 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-175">An identifier in a conforming program must be in the canonical format defined by Unicode Normalization Form C, as defined by Unicode Standard Annex 15.</span></span> <span data-ttu-id="19a96-176">정규화 형식 C에 없는 식별자를 발견할 때 동작은 구현 시 정의 됩니다. 그러나 진단 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-176">The behavior when encountering an identifier not in Normalization Form C is implementation-defined; however, a diagnostic is not required.</span></span>

<span data-ttu-id="19a96-177">접두사 "`@`" 다른 프로그래밍 언어와 상호 작용 하는 경우에 유용 식별자로 키워드를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-177">The prefix "`@`" enables the use of keywords as identifiers, which is useful when interfacing with other programming languages.</span></span> <span data-ttu-id="19a96-178">문자 `@` 면 실제로 식별자의 일부가 아니므로 식별자 접두사 없이 일반 식별자로 다른 언어로 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-178">The character `@` is not actually part of the identifier, so the identifier might be seen in other languages as a normal identifier, without the prefix.</span></span> <span data-ttu-id="19a96-179">식별자를 `@` 접두사 라고는 ***축 자 식별자***합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-179">An identifier with an `@` prefix is called a ***verbatim identifier***.</span></span> <span data-ttu-id="19a96-180">사용 된 `@` 키워드 없는 식별자에 대 한 접두사를 사용할 수는 있지만 스타일의 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-180">Use of the `@` prefix for identifiers that are not keywords is permitted, but strongly discouraged as a matter of style.</span></span>

<span data-ttu-id="19a96-181">예제:</span><span class="sxs-lookup"><span data-stu-id="19a96-181">The example:</span></span>
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
<span data-ttu-id="19a96-182">이라는 클래스를 정의 "`class`"라는 정적 메서드"with`static`"하는 명명 된 매개 변수"`bool`"입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-182">defines a class named "`class`" with a static method named "`static`" that takes a parameter named "`bool`".</span></span> <span data-ttu-id="19a96-183">메모 유니코드 이스케이프 하므로 토큰 키워드에 허용 되지 않는 "`cl\u0061ss`"는 식별자 이며 동일한 식별자를 "`@class`"입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-183">Note that since Unicode escapes are not permitted in keywords, the token "`cl\u0061ss`" is an identifier, and is the same identifier as "`@class`".</span></span>

<span data-ttu-id="19a96-184">두 개의 식별자 것으로 간주 됩니다 동일한 순서로 다음과 같은 변환이 적용 된 후 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-184">Two identifiers are considered the same if they are identical after the following transformations are applied, in order:</span></span>

*  <span data-ttu-id="19a96-185">접두사 "`@`"를 사용 하는 경우 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-185">The prefix "`@`", if used, is removed.</span></span>
*  <span data-ttu-id="19a96-186">각 *unicode_escape_sequence* 해당 유니코드 문자로 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-186">Each *unicode_escape_sequence* is transformed into its corresponding Unicode character.</span></span>
*  <span data-ttu-id="19a96-187">모든 *formatting_character*가 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-187">Any *formatting_character*s are removed.</span></span>

<span data-ttu-id="19a96-188">식별자를 포함 하는 두 개의 연속 밑줄 문자 (`U+005F`) 구현에서 사용 하도록 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-188">Identifiers containing two consecutive underscore characters (`U+005F`) are reserved for use by the implementation.</span></span> <span data-ttu-id="19a96-189">예를 들어 구현을 두 개의 밑줄로 시작 하는 확장 된 키워드를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-189">For example, an implementation might provide extended keywords that begin with two underscores.</span></span>

### <a name="keywords"></a><span data-ttu-id="19a96-190">키워드</span><span class="sxs-lookup"><span data-stu-id="19a96-190">Keywords</span></span>

<span data-ttu-id="19a96-191">A ***키워드*** 예약 되며 앞에 오는 경우를 제외 하 고 식별자로 사용할 수 없습니다 하 문자는 식별자와 같은 시퀀스를 `@` 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-191">A ***keyword*** is an identifier-like sequence of characters that is reserved, and cannot be used as an identifier except when prefaced by the `@` character.</span></span>

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

<span data-ttu-id="19a96-192">문법의 일부 지역에서는 특정 식별자 특별 한 의미가 있지만 키워드가 되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-192">In some places in the grammar, specific identifiers have special meaning, but are not keywords.</span></span> <span data-ttu-id="19a96-193">이러한 식별자는 "상황에 맞는 키워드" 라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-193">Such identifiers are sometimes referred to as "contextual keywords".</span></span> <span data-ttu-id="19a96-194">예를 들어, 속성 선언 내는 "`get`"및"`set`" 식별자는 특별 한 의미가 ([접근자](classes.md#accessors)).</span><span class="sxs-lookup"><span data-stu-id="19a96-194">For example, within a property declaration, the "`get`" and "`set`" identifiers have special meaning ([Accessors](classes.md#accessors)).</span></span> <span data-ttu-id="19a96-195">이외의 다른 식별자 `get` 또는 `set` 수 없습니다 이러한 위치에 있으므로이 사용 하이 여 이러한 단어를 식별자로 사용 하 여 충돌 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-195">An identifier other than `get` or `set` is never permitted in these locations, so this use does not conflict with a use of these words as identifiers.</span></span> <span data-ttu-id="19a96-196">다른 경우에 같은 식별자와 마찬가지로 "`var`"에서 암시적으로 형식화 된 지역 변수 선언 ([지역 변수 선언](statements.md#local-variable-declarations)), 상황별 키워드는 선언 된 이름이 충돌할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-196">In other cases, such as with the identifier "`var`" in implicitly typed local variable declarations ([Local variable declarations](statements.md#local-variable-declarations)), a contextual keyword can conflict with declared names.</span></span> <span data-ttu-id="19a96-197">이러한 경우에는 선언 된 이름 식별자의 상황별 키워드로 사용 보다 우선 순위를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-197">In such cases, the declared name takes precedence over the use of the identifier as a contextual keyword.</span></span>

### <a name="literals"></a><span data-ttu-id="19a96-198">리터럴</span><span class="sxs-lookup"><span data-stu-id="19a96-198">Literals</span></span>

<span data-ttu-id="19a96-199">A ***리터럴*** 값의 소스 코드 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-199">A ***literal*** is a source code representation of a value.</span></span>

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

#### <a name="boolean-literals"></a><span data-ttu-id="19a96-200">부울 리터럴</span><span class="sxs-lookup"><span data-stu-id="19a96-200">Boolean literals</span></span>

<span data-ttu-id="19a96-201">부울 리터럴 값이 두 개: `true` 고 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-201">There are two boolean literal values: `true` and `false`.</span></span>

```antlr
boolean_literal
    : 'true'
    | 'false'
    ;
```

<span data-ttu-id="19a96-202">형식의 *boolean_literal* 는 `bool`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-202">The type of a *boolean_literal* is `bool`.</span></span>

#### <a name="integer-literals"></a><span data-ttu-id="19a96-203">정수 리터럴</span><span class="sxs-lookup"><span data-stu-id="19a96-203">Integer literals</span></span>

<span data-ttu-id="19a96-204">정수 리터럴 형식의 값을 쓰는 데 사용 됩니다 `int`, `uint`를 `long`, 및 `ulong`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-204">Integer literals are used to write values of types `int`, `uint`, `long`, and `ulong`.</span></span> <span data-ttu-id="19a96-205">정수 리터럴에 있는 두 가지 가능한 형식: 10 진수 및 16 진수입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-205">Integer literals have two possible forms: decimal and hexadecimal.</span></span>

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

<span data-ttu-id="19a96-206">리터럴 정수의 형식은 다음과 같이 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-206">The type of an integer literal is determined as follows:</span></span>

*  <span data-ttu-id="19a96-207">해당 값을 나타낼 수 있는 이러한 형식 중 첫 번째 리터럴 접미사가 없는 경우에: `int`, `uint`를 `long`, `ulong`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-207">If the literal has no suffix, it has the first of these types in which its value can be represented: `int`, `uint`, `long`, `ulong`.</span></span>
*  <span data-ttu-id="19a96-208">리터럴이 오는 경우 `U` 또는 `u`, 해당 값을 나타낼 수 있는 이러한 형식 중 첫 번째 있기: `uint`, `ulong`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-208">If the literal is suffixed by `U` or `u`, it has the first of these types in which its value can be represented: `uint`, `ulong`.</span></span>
*  <span data-ttu-id="19a96-209">리터럴이 오는 경우 `L` 또는 `l`, 해당 값을 나타낼 수 있는 이러한 형식 중 첫 번째 있기: `long`, `ulong`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-209">If the literal is suffixed by `L` or `l`, it has the first of these types in which its value can be represented: `long`, `ulong`.</span></span>
*  <span data-ttu-id="19a96-210">리터럴이 오는 경우 `UL`, `Ul`, `uL`, `ul`를 `LU`를 `Lu`, `lU`, 또는 `lu`, 형식 `ulong`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-210">If the literal is suffixed by `UL`, `Ul`, `uL`, `ul`, `LU`, `Lu`, `lU`, or `lu`, it is of type `ulong`.</span></span>

<span data-ttu-id="19a96-211">정수 리터럴이 나타내는 값의 범위를 벗어나는 인지는 `ulong` 컴파일 타임 오류가 발생 하는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-211">If the value represented by an integer literal is outside the range of the `ulong` type, a compile-time error occurs.</span></span>

<span data-ttu-id="19a96-212">스타일의 문제로, 제안 하는 "`L`"대신 사용할 수"`l`" 형식의 리터럴을 작성할 때 `long`문자를 혼동 하기 쉬운 이므로, "`l`"숫자"과`1`" 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-212">As a matter of style, it is suggested that "`L`" be used instead of "`l`" when writing literals of type `long`, since it is easy to confuse the letter "`l`" with the digit "`1`".</span></span>

<span data-ttu-id="19a96-213">가능한 가장 작은 허용 하도록 `int` 고 `long` 쓸 10 진수 정수 리터럴로 다음 두 규칙이 존재 하는 값:</span><span class="sxs-lookup"><span data-stu-id="19a96-213">To permit the smallest possible `int` and `long` values to be written as decimal integer literals, the following two rules exist:</span></span>

* <span data-ttu-id="19a96-214">경우는 *decimal_integer_literal* 2147483648 값 (2 ^31) 없으며 *integer_type_suffix* 바로 다음에 오는 단항 빼기 연산자 토큰이 토큰으로 표시 됩니다 ([단항 빼기 연산자](expressions.md#unary-minus-operator)), 결과 형식의 상수는 `int` -2147483648 값을 사용 하 여 (-2 ^31).</span><span class="sxs-lookup"><span data-stu-id="19a96-214">When a *decimal_integer_literal* with the value 2147483648 (2^31) and no *integer_type_suffix* appears as the token immediately following a unary minus operator token ([Unary minus operator](expressions.md#unary-minus-operator)), the result is a constant of type `int` with the value -2147483648 (-2^31).</span></span> <span data-ttu-id="19a96-215">다른 모든 상황에서 이러한를 *decimal_integer_literal* 유형의 `uint`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-215">In all other situations, such a *decimal_integer_literal* is of type `uint`.</span></span>
* <span data-ttu-id="19a96-216">경우는 *decimal_integer_literal* 9223372036854775808 값 (2 ^63) 없으며 *integer_type_suffix* 또는 *integer_type_suffix* `L` 또는 `l` 바로 다음에 오는 단항 빼기 연산자 토큰이 토큰으로 표시 됩니다 ([단항 빼기 연산자](expressions.md#unary-minus-operator)), 결과 형식의 상수는 `long` 값-9223372036854775808 (-2 ^63).</span><span class="sxs-lookup"><span data-stu-id="19a96-216">When a *decimal_integer_literal* with the value 9223372036854775808 (2^63) and no *integer_type_suffix* or the *integer_type_suffix* `L` or `l` appears as the token immediately following a unary minus operator token ([Unary minus operator](expressions.md#unary-minus-operator)), the result is a constant of type `long` with the value -9223372036854775808 (-2^63).</span></span> <span data-ttu-id="19a96-217">다른 모든 상황에서 이러한를 *decimal_integer_literal* 유형의 `ulong`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-217">In all other situations, such a *decimal_integer_literal* is of type `ulong`.</span></span>

#### <a name="real-literals"></a><span data-ttu-id="19a96-218">실제 리터럴</span><span class="sxs-lookup"><span data-stu-id="19a96-218">Real literals</span></span>

<span data-ttu-id="19a96-219">실제 리터럴 형식의 값을 쓰는 데 사용 됩니다 `float`하십시오 `double`, 및 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-219">Real literals are used to write values of types `float`, `double`, and `decimal`.</span></span>

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

<span data-ttu-id="19a96-220">없으면 *real_type_suffix* 가 지정 된 형식의 실수 리터럴이 `double`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-220">If no *real_type_suffix* is specified, the type of the real literal is `double`.</span></span> <span data-ttu-id="19a96-221">이 고, 그렇지 실제 형식 접미사는 다음과 같이 실제 리터럴 형식을 결정:</span><span class="sxs-lookup"><span data-stu-id="19a96-221">Otherwise, the real type suffix determines the type of the real literal, as follows:</span></span>

*  <span data-ttu-id="19a96-222">그 뒤에 실수 리터럴을 `F` 또는 `f` 유형의 `float`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-222">A real literal suffixed by `F` or `f` is of type `float`.</span></span> <span data-ttu-id="19a96-223">예를 들어, 리터럴 `1f`, `1.5f`를 `1e10f`, 및 `123.456F` 형식의 모든 `float`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-223">For example, the literals `1f`, `1.5f`, `1e10f`, and `123.456F` are all of type `float`.</span></span>
*  <span data-ttu-id="19a96-224">그 뒤에 실수 리터럴을 `D` 또는 `d` 유형의 `double`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-224">A real literal suffixed by `D` or `d` is of type `double`.</span></span> <span data-ttu-id="19a96-225">예를 들어, 리터럴 `1d`, `1.5d`를 `1e10d`, 및 `123.456D` 형식의 모든 `double`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-225">For example, the literals `1d`, `1.5d`, `1e10d`, and `123.456D` are all of type `double`.</span></span>
*  <span data-ttu-id="19a96-226">그 뒤에 실수 리터럴을 `M` 또는 `m` 유형의 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-226">A real literal suffixed by `M` or `m` is of type `decimal`.</span></span> <span data-ttu-id="19a96-227">예를 들어, 리터럴 `1m`, `1.5m`를 `1e10m`, 및 `123.456M` 형식의 모든 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-227">For example, the literals `1m`, `1.5m`, `1e10m`, and `123.456M` are all of type `decimal`.</span></span> <span data-ttu-id="19a96-228">이 리터럴은 변환할를 `decimal` 정확한 값을 가져오고 사용 하 여 가장 가까운 표현할 수 있는 값으로 반올림 하 여 필요한 경우 값 은행원의 반올림 ([decimal 형식](types.md#the-decimal-type)).</span><span class="sxs-lookup"><span data-stu-id="19a96-228">This literal is converted to a `decimal` value by taking the exact value, and, if necessary, rounding to the nearest representable value using banker's rounding ([The decimal type](types.md#the-decimal-type)).</span></span> <span data-ttu-id="19a96-229">리터럴의 명백한 규모에 관계 없이 값이 반올림 됩니다 아니면 값이 0 (후자의 경우 크기와 부호가 값은 0)에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-229">Any scale apparent in the literal is preserved unless the value is rounded or the value is zero (in which latter case the sign and scale will be 0).</span></span> <span data-ttu-id="19a96-230">따라서 리터럴 `2.900m` 기호를 사용 하 여 10 진수를 구문 분석할 `0`, 계수 `2900`, 및 크기 조정 `3`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-230">Hence, the literal `2.900m` will be parsed to form the decimal with sign `0`, coefficient `2900`, and scale `3`.</span></span>

<span data-ttu-id="19a96-231">지정한 리터럴에 지정한 형식으로 표현할 수 없는 경우 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-231">If the specified literal cannot be represented in the indicated type, a compile-time error occurs.</span></span>

<span data-ttu-id="19a96-232">형식의 실제 리터럴 값 `float` 또는 `double` IEEE를 사용 하 여 결정 됩니다 "가장 가까운 수로 반올림 됨" 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-232">The value of a real literal of type `float` or `double` is determined by using the IEEE "round to nearest" mode.</span></span>

<span data-ttu-id="19a96-233">실수 리터럴을, 소수 자릿수는 소수점 뒤 항상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-233">Note that in a real literal, decimal digits are always required after the decimal point.</span></span> <span data-ttu-id="19a96-234">예를 들어 `1.3F` 실수 리터럴 하지만 `1.F` 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-234">For example, `1.3F` is a real literal but `1.F` is not.</span></span>

#### <a name="character-literals"></a><span data-ttu-id="19a96-235">문자 리터럴</span><span class="sxs-lookup"><span data-stu-id="19a96-235">Character literals</span></span>

<span data-ttu-id="19a96-236">문자 리터럴은 단일 문자를 나타내며 큰따옴표의 문자에서와 같이 일반적으로 이루어져 `'a'`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-236">A character literal represents a single character, and usually consists of a character in quotes, as in `'a'`.</span></span>

<span data-ttu-id="19a96-237">참고: ANTLR 문법 표기법을 사용 하면 다음 혼동 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-237">Note: The ANTLR grammar notation makes the following confusing!</span></span> <span data-ttu-id="19a96-238">ANTLR를 작성 하는 경우에 `\'` 작은따옴표의 약자 `'`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-238">In ANTLR, when you write `\'` it stands for a single quote `'`.</span></span> <span data-ttu-id="19a96-239">작성 하는 경우 및 `\\` 단일 백슬래시의 약자 `\`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-239">And when you write `\\` it stands for a single backslash `\`.</span></span> <span data-ttu-id="19a96-240">따라서 리터럴 문자에 대 한 첫 번째 규칙은 문자, 작은따옴표, 차례로 작은따옴표를 사용 하 여 시작을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-240">Therefore the first rule for a character literal means it starts with a single quote, then a character, then a single quote.</span></span> <span data-ttu-id="19a96-241">11 개의 가능한 단순 이스케이프 시퀀스 이며 `\'`, `\"`, `\\`, `\0`, `\a`, `\b`, `\f`, `\n`, `\r`, `\t`, `\v`.</span><span class="sxs-lookup"><span data-stu-id="19a96-241">And the eleven possible simple escape sequences are `\'`, `\"`, `\\`, `\0`, `\a`, `\b`, `\f`, `\n`, `\r`, `\t`, `\v`.</span></span>

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

<span data-ttu-id="19a96-242">백슬래시 문자 뒤에 오는 문자 (`\`)에 *문자* 는 다음 문자 중 하나 여야 합니다: `'`, `"`를 `\`, `0`, `a`, `b` , `f`, `n`, `r`, `t`, `u`, `U`, `x`, `v`.</span><span class="sxs-lookup"><span data-stu-id="19a96-242">A character that follows a backslash character (`\`) in a *character* must be one of the following characters: `'`, `"`, `\`, `0`, `a`, `b`, `f`, `n`, `r`, `t`, `u`, `U`, `x`, `v`.</span></span> <span data-ttu-id="19a96-243">그렇지 않으면 컴파일 타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-243">Otherwise, a compile-time error occurs.</span></span>

<span data-ttu-id="19a96-244">16 진수 이스케이프 시퀀스는 16 진수 숫자 다음과 같은 구성 값을 사용 하 여 단일 유니코드 문자를 나타내는 "`\x`"입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-244">A hexadecimal escape sequence represents a single Unicode character, with the value formed by the hexadecimal number following "`\x`".</span></span>

<span data-ttu-id="19a96-245">리터럴 문자를 나타내는 값 보다 크면 `U+FFFF`, 컴파일 시간 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-245">If the value represented by a character literal is greater than `U+FFFF`, a compile-time error occurs.</span></span>

<span data-ttu-id="19a96-246">유니코드 문자 이스케이프 시퀀스 ([유니코드 문자 이스케이프 시퀀스인](lexical-structure.md#unicode-character-escape-sequences)) 문자 리터럴에 범위에서 여야 합니다 `U+0000` 에 `U+FFFF`입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-246">A Unicode character escape sequence ([Unicode character escape sequences](lexical-structure.md#unicode-character-escape-sequences)) in a character literal must be in the range `U+0000` to `U+FFFF`.</span></span>

<span data-ttu-id="19a96-247">아래 표에 설명 된 대로 단순 이스케이프 시퀀스를 유니코드 문자 인코딩을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-247">A simple escape sequence represents a Unicode character encoding, as described in the table below.</span></span>


| <span data-ttu-id="19a96-248">__이스케이프 시퀀스__</span><span class="sxs-lookup"><span data-stu-id="19a96-248">__Escape sequence__</span></span> | <span data-ttu-id="19a96-249">__문자 이름__</span><span class="sxs-lookup"><span data-stu-id="19a96-249">__Character name__</span></span> | <span data-ttu-id="19a96-250">__유니코드 인코딩__</span><span class="sxs-lookup"><span data-stu-id="19a96-250">__Unicode encoding__</span></span> |
|---------------------|--------------------|----------------------|
| `\'`                | <span data-ttu-id="19a96-251">작은따옴표</span><span class="sxs-lookup"><span data-stu-id="19a96-251">Single quote</span></span>       | `0x0027`             | 
| `\"`                | <span data-ttu-id="19a96-252">큰따옴표</span><span class="sxs-lookup"><span data-stu-id="19a96-252">Double quote</span></span>       | `0x0022`             | 
| `\\`                | <span data-ttu-id="19a96-253">백슬래시</span><span class="sxs-lookup"><span data-stu-id="19a96-253">Backslash</span></span>          | `0x005C`             | 
| `\0`                | <span data-ttu-id="19a96-254">Null</span><span class="sxs-lookup"><span data-stu-id="19a96-254">Null</span></span>               | `0x0000`             | 
| `\a`                | <span data-ttu-id="19a96-255">경고</span><span class="sxs-lookup"><span data-stu-id="19a96-255">Alert</span></span>              | `0x0007`             | 
| `\b`                | <span data-ttu-id="19a96-256">백스페이스</span><span class="sxs-lookup"><span data-stu-id="19a96-256">Backspace</span></span>          | `0x0008`             | 
| `\f`                | <span data-ttu-id="19a96-257">폼 피드</span><span class="sxs-lookup"><span data-stu-id="19a96-257">Form feed</span></span>          | `0x000C`             | 
| `\n`                | <span data-ttu-id="19a96-258">줄 바꿈</span><span class="sxs-lookup"><span data-stu-id="19a96-258">New line</span></span>           | `0x000A`             | 
| `\r`                | <span data-ttu-id="19a96-259">캐리지 리턴</span><span class="sxs-lookup"><span data-stu-id="19a96-259">Carriage return</span></span>    | `0x000D`             | 
| `\t`                | <span data-ttu-id="19a96-260">가로 탭</span><span class="sxs-lookup"><span data-stu-id="19a96-260">Horizontal tab</span></span>     | `0x0009`             | 
| `\v`                | <span data-ttu-id="19a96-261">세로 탭</span><span class="sxs-lookup"><span data-stu-id="19a96-261">Vertical tab</span></span>       | `0x000B`             | 

<span data-ttu-id="19a96-262">형식의 *character_literal* 는 `char`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-262">The type of a *character_literal* is `char`.</span></span>

#### <a name="string-literals"></a><span data-ttu-id="19a96-263">문자열 리터럴</span><span class="sxs-lookup"><span data-stu-id="19a96-263">String literals</span></span>

<span data-ttu-id="19a96-264">C# 두 가지 형태의 문자열 리터럴 지원: ***정규 문자열 리터럴은*** 하 고 ***축 자 문자열 리터럴은***합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-264">C# supports two forms of string literals: ***regular string literals*** and ***verbatim string literals***.</span></span>

<span data-ttu-id="19a96-265">일반 문자열 리터럴 구성에서 같이 큰따옴표로 묶인 0 개 이상의 문자 `"hello"`, 모두 단순 이스케이프 시퀀스를 포함할 수 있습니다 (같은 `\t` 탭 문자), 16 진수 및 유니코드 이스케이프 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-265">A regular string literal consists of zero or more characters enclosed in double quotes, as in `"hello"`, and may include both simple escape sequences (such as `\t` for the tab character), and hexadecimal and Unicode escape sequences.</span></span>

<span data-ttu-id="19a96-266">축 자 문자열 리터럴은 이루어져는 `@` 큰따옴표 문자, 0 개 이상의 문자 및 닫는 큰따옴표 문자 뒤에 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-266">A verbatim string literal consists of an `@` character followed by a double-quote character, zero or more characters, and a closing double-quote character.</span></span> <span data-ttu-id="19a96-267">간단한 예로 `@"hello"`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-267">A simple example is `@"hello"`.</span></span> <span data-ttu-id="19a96-268">축 자 문자열 리터럴 구분 기호 사이 있는 문자를 정확 하 게 해석 되며 되 고 있는 유일한 예외는 *quote_escape_sequence*합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-268">In a verbatim string literal, the characters between the delimiters are interpreted verbatim, the only exception being a *quote_escape_sequence*.</span></span> <span data-ttu-id="19a96-269">특히, 단순 이스케이프 시퀀스 및 16 진수 및 유니코드 이스케이프 시퀀스가 처리 되지 않습니다 축 자 문자열 리터럴.</span><span class="sxs-lookup"><span data-stu-id="19a96-269">In particular, simple escape sequences, and hexadecimal and Unicode escape sequences are not processed in verbatim string literals.</span></span> <span data-ttu-id="19a96-270">축 자 문자열 리터럴 여러 줄으로 나누어 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-270">A verbatim string literal may span multiple lines.</span></span>

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

<span data-ttu-id="19a96-271">백슬래시 문자 뒤에 오는 문자 (`\`)에 *regular_string_literal_character* 는 다음 문자 중 하나 여야 합니다: `'`, `"`를 `\`, `0`, `a` , `b`, `f`, `n`, `r`, `t`, `u`, `U`, `x`, `v`.</span><span class="sxs-lookup"><span data-stu-id="19a96-271">A character that follows a backslash character (`\`) in a *regular_string_literal_character* must be one of the following characters: `'`, `"`, `\`, `0`, `a`, `b`, `f`, `n`, `r`, `t`, `u`, `U`, `x`, `v`.</span></span> <span data-ttu-id="19a96-272">그렇지 않으면 컴파일 타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-272">Otherwise, a compile-time error occurs.</span></span>

<span data-ttu-id="19a96-273">이 예제에서</span><span class="sxs-lookup"><span data-stu-id="19a96-273">The example</span></span>
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
<span data-ttu-id="19a96-274">다양 한 문자열 리터럴 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-274">shows a variety of string literals.</span></span> <span data-ttu-id="19a96-275">마지막 문자열 리터럴에 `j`, 축 자 문자열 리터럴 여러 줄에 걸쳐 있는 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-275">The last string literal, `j`, is a verbatim string literal that spans multiple lines.</span></span> <span data-ttu-id="19a96-276">줄 바꿈 문자로 같은 공백 문자를 포함 하 여 따옴표 사이 있는 문자를 그대로 보존 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-276">The characters between the quotation marks, including white space such as new line characters, are preserved verbatim.</span></span>

<span data-ttu-id="19a96-277">16 진수 이스케이프 시퀀스는 다양 한 16 진수 숫자, 문자열 리터럴 있을 수 있으므로 `"\x123"` 16 진수 값 123 사용 하 여 단일 문자를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-277">Since a hexadecimal escape sequence can have a variable number of hex digits, the string literal `"\x123"` contains a single character with hex value 123.</span></span> <span data-ttu-id="19a96-278">16 진수 값 3 문자 뒤에 12 사용 하 여 문자를 포함 하는 문자열을 만들려면 하나 작성할 수 `"\x00123"` 또는 `"\x12" + "3"` 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-278">To create a string containing the character with hex value 12 followed by the character 3, one could write `"\x00123"` or `"\x12" + "3"` instead.</span></span>

<span data-ttu-id="19a96-279">형식의 *string_literal* 는 `string`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-279">The type of a *string_literal* is `string`.</span></span>

<span data-ttu-id="19a96-280">각 문자열 리터럴 새 문자열 인스턴스에서 반드시 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-280">Each string literal does not necessarily result in a new string instance.</span></span> <span data-ttu-id="19a96-281">두 개 이상의 문자열 리터럴을 하는 경우 문자열 같음 연산자에 따라 해당 하는 ([같음 연산자를 문자열](expressions.md#string-equality-operators)) 동일한 문자열 인스턴스를 해당 문자열 리터럴을 참조할 동일한 프로그램에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-281">When two or more string literals that are equivalent according to the string equality operator ([String equality operators](expressions.md#string-equality-operators)) appear in the same program, these string literals refer to the same string instance.</span></span> <span data-ttu-id="19a96-282">예를 들어, 생성 한 출력</span><span class="sxs-lookup"><span data-stu-id="19a96-282">For instance, the output produced by</span></span>
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
<span data-ttu-id="19a96-283">`True` 두 개의 리터럴 동일한 문자열 인스턴스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-283">is `True` because the two literals refer to the same string instance.</span></span>

#### <a name="interpolated-string-literals"></a><span data-ttu-id="19a96-284">보간된 문자열 리터럴</span><span class="sxs-lookup"><span data-stu-id="19a96-284">Interpolated string literals</span></span>

<span data-ttu-id="19a96-285">보간된 문자열 리터럴을 문자열 리터럴로 유사 하지만 구분 구멍이 포함 `{` 고 `}`, 식 여기서 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-285">Interpolated string literals are similar to string literals, but contain holes delimited by `{` and `}`, wherein expressions can occur.</span></span> <span data-ttu-id="19a96-286">런타임 시 식 위치에 구멍 발생 하는 문자열에 대체의 텍스트 형식 필요 하기 위한 목적으로 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-286">At runtime, the expressions are evaluated with the purpose of having their textual forms substituted into the string at the place where the hole occurs.</span></span> <span data-ttu-id="19a96-287">구문 및 의미 체계의 문자열 보간의 섹션에 설명 된 ([보간된 문자열](expressions.md#interpolated-strings)).</span><span class="sxs-lookup"><span data-stu-id="19a96-287">The syntax and semantics of string interpolation are described in section ([Interpolated strings](expressions.md#interpolated-strings)).</span></span>

<span data-ttu-id="19a96-288">문자열 리터럴와 같은 일반 또는 약어 보간된 문자열 리터럴은 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-288">Like string literals, interpolated string literals can be either regular or verbatim.</span></span> <span data-ttu-id="19a96-289">보간된 정규 문자열 리터럴은로 구분 됩니다 `$"` 하 고 `"`, 약어 보간된 문자열 리터럴 구분 되 고 `$@"` 및 `"`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-289">Interpolated regular string literals are delimited by `$"` and `"`, and interpolated verbatim string literals are delimited by `$@"` and `"`.</span></span>

<span data-ttu-id="19a96-290">다른 리터럴와 같은 어휘 분석 리터럴 보간된 문자열의 처음 아래 문법에 따라 단일 토큰에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-290">Like other literals, lexical analysis of an interpolated string literal initially results in a single token, as per the grammar below.</span></span> <span data-ttu-id="19a96-291">그러나 구문 분석 하기 전에 리터럴 보간된 문자열의 단일 토큰 취약 한 부분을 포함 하는 문자열의 부분에 대 한 여러 토큰으로 구분 됩니다 및 취약 한 부분에서 발생 하는 입력된 요소가 다시 분석 어휘 적으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-291">However, before syntactic analysis, the single token of an interpolated string literal is broken into several tokens for the parts of the string enclosing the holes, and the input elements occurring in the holes are lexically analysed again.</span></span> <span data-ttu-id="19a96-292">다시 처리할 수 있지만, 어휘 적으로 수정한 경우는 결과적으로 일련의 처리를 구문 분석을 위해 토큰 보다 보간된 문자열 리터럴을 생성할 수 있습니다이.</span><span class="sxs-lookup"><span data-stu-id="19a96-292">This may in turn produce more interpolated string literals to be processed, but, if lexically correct, will eventually lead to a sequence of tokens for syntactic analysis to process.</span></span>

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

<span data-ttu-id="19a96-293">*interpolated_string_literal* 토큰 여러 토큰 및 기타 나타나는 순서 대로 요소를 다음과 같이 입력 하는 대로 해석 되는 *interpolated_string_literal*:</span><span class="sxs-lookup"><span data-stu-id="19a96-293">An *interpolated_string_literal* token is reinterpreted as multiple tokens and other input elements as follows, in order of occurrence in the *interpolated_string_literal*:</span></span>

* <span data-ttu-id="19a96-294">다음의 항목은 별도 개별 토큰으로 다시 해석: 앞에 오는 `$` 부호 *interpolated_regular_string_whole*, *interpolated_regular_string_start*, *interpolated_regular_string_mid*하십시오 *interpolated_regular_string_end*하십시오 *interpolated_verbatim_string_whole*,  *interpolated_verbatim_string_start*하십시오 *interpolated_verbatim_string_mid* 하 고 *interpolated_verbatim_string_end*합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-294">Occurrences of the following are reinterpreted as separate individual tokens: the leading `$` sign, *interpolated_regular_string_whole*, *interpolated_regular_string_start*, *interpolated_regular_string_mid*, *interpolated_regular_string_end*, *interpolated_verbatim_string_whole*, *interpolated_verbatim_string_start*, *interpolated_verbatim_string_mid* and *interpolated_verbatim_string_end*.</span></span>
* <span data-ttu-id="19a96-295">횟수 *regular_balanced_text* 하 고 *verbatim_balanced_text* 이들 사이 다시 처리로 *input_section* ([어휘 분석 ](lexical-structure.md#lexical-analysis)) 및 입력 요소의 결과 시퀀스로 해석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-295">Occurrences of *regular_balanced_text* and *verbatim_balanced_text* between these are reprocessed as an *input_section* ([Lexical analysis](lexical-structure.md#lexical-analysis)) and are reinterpreted as the resulting sequence of input elements.</span></span> <span data-ttu-id="19a96-296">다시 해석 됩니다 보간된 문자열 리터럴 토큰에 포함 될 수 있습니다 이러한 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-296">These may in turn include interpolated string literal tokens to be reinterpreted.</span></span>

<span data-ttu-id="19a96-297">구문 분석에 토큰을 다시 결합 합니다는 *interpolated_string_expression* ([보간된 문자열](expressions.md#interpolated-strings)).</span><span class="sxs-lookup"><span data-stu-id="19a96-297">Syntactic analysis will recombine the tokens into an *interpolated_string_expression* ([Interpolated strings](expressions.md#interpolated-strings)).</span></span>

<span data-ttu-id="19a96-298">TODO 예제</span><span class="sxs-lookup"><span data-stu-id="19a96-298">Examples TODO</span></span>


#### <a name="the-null-literal"></a><span data-ttu-id="19a96-299">Null 리터럴</span><span class="sxs-lookup"><span data-stu-id="19a96-299">The null literal</span></span>

```antlr
null_literal
    : 'null'
    ;
```

<span data-ttu-id="19a96-300">합니다 *null_literal* 참조 형식 또는 nullable 형식에 암시적으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-300">The  *null_literal* can be implicitly converted to a reference type or nullable type.</span></span>

### <a name="operators-and-punctuators"></a><span data-ttu-id="19a96-301">연산자 및 문장 부호</span><span class="sxs-lookup"><span data-stu-id="19a96-301">Operators and punctuators</span></span>

<span data-ttu-id="19a96-302">연산자 및 문장 부호의 몇 가지 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-302">There are several kinds of operators and punctuators.</span></span> <span data-ttu-id="19a96-303">연산자는 식에서 하나 이상의 피연산자와 관련 된 작업을 설명 하기 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-303">Operators are used in expressions to describe operations involving one or more operands.</span></span> <span data-ttu-id="19a96-304">예를 들어 식 `a + b` 사용 하는 `+` 연산자는 두 피연산자를 추가할 `a` 및 `b`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-304">For example, the expression `a + b` uses the `+` operator to add the two operands `a` and `b`.</span></span> <span data-ttu-id="19a96-305">문장 부호를 그룹화 하 고 분리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-305">Punctuators are for grouping and separating.</span></span>

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

<span data-ttu-id="19a96-306">세로 막대는 합니다 *right_shift* 하 고 *right_shift_assignment* 프로덕션 구문 문법에서 어떤 종류의 문자가 없는 다른 프로덕션 달리 (하더라도 나타내는 데 사용 됩니다 공백) 토큰 사이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-306">The vertical bar in the *right_shift* and *right_shift_assignment* productions are used to indicate that, unlike other productions in the syntactic grammar, no characters of any kind (not even whitespace) are allowed between the tokens.</span></span> <span data-ttu-id="19a96-307">이러한 프로덕션을 올바르게 처리할 수 있도록 특별히 처리할지 *type_parameter_list*s ([형식 매개 변수](classes.md#type-parameters)).</span><span class="sxs-lookup"><span data-stu-id="19a96-307">These productions are treated specially in order to enable the correct  handling of *type_parameter_list*s ([Type parameters](classes.md#type-parameters)).</span></span>

## <a name="pre-processing-directives"></a><span data-ttu-id="19a96-308">전처리 지시문</span><span class="sxs-lookup"><span data-stu-id="19a96-308">Pre-processing directives</span></span>

<span data-ttu-id="19a96-309">전처리 지시문은 조건부로 보고서 오류 및 경고 조건에 소스 파일의 섹션을 건너뛸 소스 코드의 고유 영역을 설명 하는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-309">The pre-processing directives provide the ability to conditionally skip sections of source files, to report error and warning conditions, and to delineate distinct regions of source code.</span></span> <span data-ttu-id="19a96-310">"전처리 지시문" 라는 용어는 C 및 c + + 프로그래밍 언어를 사용 하 여 일관성을 위해서만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-310">The term "pre-processing directives" is used only for consistency with the C and C++ programming languages.</span></span> <span data-ttu-id="19a96-311">C#의 경우에 없는 별도 사전 처리 단계 전처리 지시문 어휘 분석 단계의 일부로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-311">In C#, there is no separate pre-processing step; pre-processing directives are processed as part of the lexical analysis phase.</span></span>

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

<span data-ttu-id="19a96-312">다음 전처리 지시문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-312">The following pre-processing directives are available:</span></span>

*  <span data-ttu-id="19a96-313">`#define` 및 `#undef`를 정의 조건부 컴파일 기호를 각각 정의 하는 데 사용 되는 ([선언 지시문](lexical-structure.md#declaration-directives)).</span><span class="sxs-lookup"><span data-stu-id="19a96-313">`#define` and `#undef`, which are used to define and undefine, respectively, conditional compilation symbols ([Declaration directives](lexical-structure.md#declaration-directives)).</span></span>
*  <span data-ttu-id="19a96-314">`#if`를 `#elif`, `#else`, 및 `#endif`, 조건에 따라 소스 코드의 섹션을 건너뛸 하는 데 사용 되는 ([조건부 컴파일 지시문](lexical-structure.md#conditional-compilation-directives)).</span><span class="sxs-lookup"><span data-stu-id="19a96-314">`#if`, `#elif`, `#else`, and `#endif`, which are used to conditionally skip sections of source code ([Conditional compilation directives](lexical-structure.md#conditional-compilation-directives)).</span></span>
*  <span data-ttu-id="19a96-315">`#line`에 오류와 경고를 생성 하는 줄 번호를 제어 하는 데 사용 됩니다 ([지시문을 줄](lexical-structure.md#line-directives)).</span><span class="sxs-lookup"><span data-stu-id="19a96-315">`#line`, which is used to control line numbers emitted for errors and warnings ([Line directives](lexical-structure.md#line-directives)).</span></span>
*  <span data-ttu-id="19a96-316">`#error` 및 `#warning`을 오류 및 경고를 각각 실행 하는 데 사용 되는 ([진단 지시문](lexical-structure.md#diagnostic-directives)).</span><span class="sxs-lookup"><span data-stu-id="19a96-316">`#error` and `#warning`, which are used to issue errors and warnings, respectively ([Diagnostic directives](lexical-structure.md#diagnostic-directives)).</span></span>
*  <span data-ttu-id="19a96-317">`#region` 및 `#endregion`를 명시적으로 소스 코드의 섹션을 표시 하는 데 사용 되는 ([Region 지시문](lexical-structure.md#region-directives)).</span><span class="sxs-lookup"><span data-stu-id="19a96-317">`#region` and `#endregion`, which are used to explicitly mark sections of source code ([Region directives](lexical-structure.md#region-directives)).</span></span>
*  <span data-ttu-id="19a96-318">`#pragma`에 컴파일러에 선택적 컨텍스트 정보를 지정 하는 데 사용 됩니다 ([Pragma 지시문](lexical-structure.md#pragma-directives)).</span><span class="sxs-lookup"><span data-stu-id="19a96-318">`#pragma`, which is used to specify optional contextual information to the compiler ([Pragma directives](lexical-structure.md#pragma-directives)).</span></span>

<span data-ttu-id="19a96-319">전처리 지시문은 항상 별도의 소스 코드 줄을 차지 하며 항상 시작을 `#` 문자 및 전처리 지시문 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-319">A pre-processing directive always occupies a separate line of source code and always begins with a `#` character and a pre-processing directive name.</span></span> <span data-ttu-id="19a96-320">앞에 공백이 있을 수 있습니다는 `#` 문자 및는 `#` 문자와 지시문 이름.</span><span class="sxs-lookup"><span data-stu-id="19a96-320">White space may occur before the `#` character and between the `#` character and the directive name.</span></span>

<span data-ttu-id="19a96-321">포함 하는 소스 줄을 `#define`, `#undef`, `#if`, `#elif`를 `#else`를 `#endif`, `#line`, 또는 `#endregion` 지시문 줄 주석으로 종료 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-321">A source line containing a `#define`, `#undef`, `#if`, `#elif`, `#else`, `#endif`, `#line`, or `#endregion` directive may end with a single-line comment.</span></span> <span data-ttu-id="19a96-322">주석 구분 (의 `/* */` 주석의 스타일) 전처리 지시문이 포함 된 소스 줄에서 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-322">Delimited comments (the `/* */` style of comments) are not permitted on source lines containing pre-processing directives.</span></span>

<span data-ttu-id="19a96-323">전처리 지시문은 토큰이 및 C#의 구문 문법의 일부가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-323">Pre-processing directives are not tokens and are not part of the syntactic grammar of C#.</span></span> <span data-ttu-id="19a96-324">그러나 전처리 지시문 포함 하거나 제외할 토큰 시퀀스로 사용할 수 있으며 해당 방식으로 영향을 줄 수는 C# 프로그램의 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-324">However, pre-processing directives can be used to include or exclude sequences of tokens and can in that way affect the meaning of a C# program.</span></span> <span data-ttu-id="19a96-325">예를 들어, 프로그램을 컴파일할 때:</span><span class="sxs-lookup"><span data-stu-id="19a96-325">For example, when compiled, the program:</span></span>
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
<span data-ttu-id="19a96-326">프로그램으로 토큰의 정확한 순서에 결과:</span><span class="sxs-lookup"><span data-stu-id="19a96-326">results in the exact same sequence of tokens as the program:</span></span>
```csharp
class C
{
    void F() {}
    void I() {}
}
```

<span data-ttu-id="19a96-327">따라서 어휘, 두 프로그램은 매우 다르므로 구문상, 반면 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-327">Thus, whereas lexically, the two programs are quite different, syntactically, they are identical.</span></span>

### <a name="conditional-compilation-symbols"></a><span data-ttu-id="19a96-328">조건부 컴파일 기호</span><span class="sxs-lookup"><span data-stu-id="19a96-328">Conditional compilation symbols</span></span>

<span data-ttu-id="19a96-329">제공 하는 조건부 컴파일 기능을 `#if`, `#elif`를 `#else`, 및 `#endif` 지시문은 전처리 다음 식을 통해 제어 됩니다 ([전처리 식](lexical-structure.md#pre-processing-expressions)) 및 조건부 컴파일 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-329">The conditional compilation functionality provided by the `#if`, `#elif`, `#else`, and `#endif` directives is controlled through pre-processing expressions ([Pre-processing expressions](lexical-structure.md#pre-processing-expressions)) and conditional compilation symbols.</span></span>

```antlr
conditional_symbol
    : '<Any identifier_or_keyword except true or false>'
    ;
```

<span data-ttu-id="19a96-330">조건부 컴파일 기호는 두 가지 가능한 상태: ***정의*** 하거나 ***정의 되지 않은***합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-330">A conditional compilation symbol has two possible states: ***defined*** or ***undefined***.</span></span> <span data-ttu-id="19a96-331">소스 파일의 어휘 처리를 시작할 때 조건부 컴파일 기호를 하지 않는 정의 외부 메커니즘 (예: 명령줄 컴파일러 옵션)에 의해 명시적으로 정의 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-331">At the beginning of the lexical processing of a source file, a conditional compilation symbol is undefined unless it has been explicitly defined by an external mechanism (such as a command-line compiler option).</span></span> <span data-ttu-id="19a96-332">경우는 `#define` 지시문 처리 하는 해당 지시문에 명명 된 조건부 컴파일 기호를 해당 소스 파일에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-332">When a `#define` directive is processed, the conditional compilation symbol named in that directive becomes defined in that source file.</span></span> <span data-ttu-id="19a96-333">기호 정의 될 때까지 계속는 `#undef` 소스 파일의 끝에 도달할 때까지 또는 처리 되는 동일한 기호에 대 한 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-333">The symbol remains defined until an `#undef` directive for that same symbol is processed, or until the end of the source file is reached.</span></span> <span data-ttu-id="19a96-334">이 사항의 시사점 `#define` 및 `#undef` 하나의 소스 파일의 지시문 동일한 프로그램에서 다른 소스 파일에 영향을 주지 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-334">An implication of this is that `#define` and `#undef` directives in one source file have no effect on other source files in the same program.</span></span>

<span data-ttu-id="19a96-335">정의 된 조건부 컴파일 기호를 부울 값이 사전 처리 하는 식에서 참조 하는 경우 `true`, 정의 되지 않은 조건부 컴파일 기호를 부울 값이 있고 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-335">When referenced in a pre-processing expression, a defined conditional compilation symbol has the boolean value `true`, and an undefined conditional compilation symbol has the boolean value `false`.</span></span> <span data-ttu-id="19a96-336">요구 사항은 없습니다 전처리 식에서 참조 된 전에 선언 명시적으로 조건부 컴파일 기호 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-336">There is no requirement that conditional compilation symbols be explicitly declared before they are referenced in pre-processing expressions.</span></span> <span data-ttu-id="19a96-337">대신, 선언 되지 않은 기호는 단순히 정의 되지 있고 따라서 값 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-337">Instead, undeclared symbols are simply undefined and thus have the value `false`.</span></span>

<span data-ttu-id="19a96-338">조건부 컴파일 기호에 대 한 네임 스페이스를 고유 되어 C# 프로그램에서 명명 된 기타 모든 엔터티를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-338">The name space for conditional compilation symbols is distinct and separate from all other named entities in a C# program.</span></span> <span data-ttu-id="19a96-339">조건부 컴파일 기호에서 참조할 수 있습니다 `#define` 고 `#undef` 지시문 및 전처리 식입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-339">Conditional compilation symbols can only be referenced in `#define` and `#undef` directives and in pre-processing expressions.</span></span>

### <a name="pre-processing-expressions"></a><span data-ttu-id="19a96-340">전처리 식</span><span class="sxs-lookup"><span data-stu-id="19a96-340">Pre-processing expressions</span></span>

<span data-ttu-id="19a96-341">전처리 식에서 발생할 수 있습니다 `#if` 고 `#elif` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-341">Pre-processing expressions can occur in `#if` and `#elif` directives.</span></span> <span data-ttu-id="19a96-342">연산자 `!`, `==`를 `!=`, `&&` 및 `||` 전처리 식에서 허용 됩니다 및 그룹화에 대 한 괄호를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-342">The operators `!`, `==`, `!=`, `&&` and `||` are permitted in pre-processing expressions, and parentheses may be used for grouping.</span></span>

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

<span data-ttu-id="19a96-343">정의 된 조건부 컴파일 기호를 부울 값이 사전 처리 하는 식에서 참조 하는 경우 `true`, 정의 되지 않은 조건부 컴파일 기호를 부울 값이 있고 `false`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-343">When referenced in a pre-processing expression, a defined conditional compilation symbol has the boolean value `true`, and an undefined conditional compilation symbol has the boolean value `false`.</span></span>

<span data-ttu-id="19a96-344">항상 사전 처리 식의 평가는 부울 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-344">Evaluation of a pre-processing expression always yields a boolean value.</span></span> <span data-ttu-id="19a96-345">사전 처리 하는 식 계산 규칙은 상수 식에 대 한 것과 동일 ([상수 식](expressions.md#constant-expressions))는 사용자 정의 된 엔터티만 참조할 수 있는 조건부 컴파일 기호는 점을 제외 하 고, .</span><span class="sxs-lookup"><span data-stu-id="19a96-345">The rules of evaluation for a pre-processing expression are the same as those for a constant expression ([Constant expressions](expressions.md#constant-expressions)), except that the only user-defined entities that can be referenced are conditional compilation symbols.</span></span>

### <a name="declaration-directives"></a><span data-ttu-id="19a96-346">선언 지시문</span><span class="sxs-lookup"><span data-stu-id="19a96-346">Declaration directives</span></span>

<span data-ttu-id="19a96-347">선언 지시문은 조건부 컴파일 기호를 정의 또는 정의 해제 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-347">The declaration directives are used to define or undefine conditional compilation symbols.</span></span>

```antlr
pp_declaration
    : whitespace? '#' whitespace? 'define' whitespace conditional_symbol pp_new_line
    | whitespace? '#' whitespace? 'undef' whitespace conditional_symbol pp_new_line
    ;

pp_new_line
    : whitespace? single_line_comment? new_line
    ;
```

<span data-ttu-id="19a96-348">처리는 `#define` 지시문 하면 정의 된 상태가 지정 된 조건부 컴파일 기호 지시문 뒤에 오는 소스 줄을 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-348">The processing of a `#define` directive causes the given conditional compilation symbol to become defined, starting with the source line that follows the directive.</span></span> <span data-ttu-id="19a96-349">마찬가지로 처리는 `#undef` 지시문으로 인해 정의 되지 않은 지시문 뒤에 오는 소스 줄을 사용 하 여 시작 되도록 지정 된 조건부 컴파일 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-349">Likewise, the processing of an `#undef` directive causes the given conditional compilation symbol to become undefined, starting with the source line that follows the directive.</span></span>

<span data-ttu-id="19a96-350">모든 `#define` 하 고 `#undef` 소스 파일의 지시문은 첫 번째 앞에 있어야 합니다. *토큰* ([토큰](lexical-structure.md#tokens)) 원본 파일의 그렇지 않으면 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-350">Any `#define` and `#undef` directives in a source file must occur before the first *token* ([Tokens](lexical-structure.md#tokens)) in the source file; otherwise a compile-time error occurs.</span></span> <span data-ttu-id="19a96-351">직관적인 말해 `#define` 및 `#undef` 지시문 소스 파일의 "실제 코드"를 빨라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-351">In intuitive terms, `#define` and `#undef` directives must precede any "real code" in the source file.</span></span>

<span data-ttu-id="19a96-352">예제:</span><span class="sxs-lookup"><span data-stu-id="19a96-352">The example:</span></span>
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
<span data-ttu-id="19a96-353">유효 하기 때문에 `#define` 지시문의 첫 번째 토큰 앞에 야 (합니다 `namespace` 키워드) 소스 파일에서.</span><span class="sxs-lookup"><span data-stu-id="19a96-353">is valid because the `#define` directives precede the first token (the `namespace` keyword) in the source file.</span></span>

<span data-ttu-id="19a96-354">때문에 다음 예제에서는 컴파일 타임 오류가 발생 한 `#define` 실제 코드를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-354">The following example results in a compile-time error because a `#define` follows real code:</span></span>
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

<span data-ttu-id="19a96-355">A `#define` 모든 중간 있을 하지 않고 이미 정의 되어 있는 조건부 컴파일 기호를 정의할 수 있습니다 `#undef` 해당 기호에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-355">A `#define` may define a conditional compilation symbol that is already defined, without there being any intervening `#undef` for that symbol.</span></span> <span data-ttu-id="19a96-356">조건부 컴파일 기호를 정의 하는 아래 예제에서는 `A` 다음 다시 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-356">The example below defines a conditional compilation symbol `A` and then defines it again.</span></span>
```csharp
#define A
#define A
```

<span data-ttu-id="19a96-357">`#undef` 있습니다 "해제" 정의 되지 않은 조건부 컴파일 기호를 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-357">A `#undef` may "undefine" a conditional compilation symbol that is not defined.</span></span> <span data-ttu-id="19a96-358">아래 예제에서는 조건부 컴파일 기호를 정의 `A` 다음 하지만 두 번 해제 하 고 두 번째 `#undef` 효과도 없으며, 여전히 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-358">The example below defines a conditional compilation symbol `A` and then undefines it twice; although the second `#undef` has no effect, it is still valid.</span></span>
```csharp
#define A
#undef A
#undef A
```

### <a name="conditional-compilation-directives"></a><span data-ttu-id="19a96-359">조건부 컴파일 지시문</span><span class="sxs-lookup"><span data-stu-id="19a96-359">Conditional compilation directives</span></span>

<span data-ttu-id="19a96-360">조건부 컴파일 지시문은 조건부로 포함 하거나 소스 파일 부분을 제외 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-360">The conditional compilation directives are used to conditionally include or exclude portions of a source file.</span></span>

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

<span data-ttu-id="19a96-361">구문에 표시 된 대로 조건부 컴파일 지시문의 순서로 구성 된 집합으로 작성 되어야 합니다는 `#if` 지시문을 0 개 이상의 `#elif` 지시문, 0 또는 1 `#else` 지시문 및 `#endif` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-361">As indicated by the syntax, conditional compilation directives must be written as sets consisting of, in order, an `#if` directive, zero or more `#elif` directives, zero or one `#else` directive, and an `#endif` directive.</span></span> <span data-ttu-id="19a96-362">지시문 사이의 소스 코드의 조건부 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-362">Between the directives are conditional sections of source code.</span></span> <span data-ttu-id="19a96-363">각 섹션 바로 앞 지시문에 의해 제어 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-363">Each section is controlled by the immediately preceding directive.</span></span> <span data-ttu-id="19a96-364">조건부 섹션을 자체 포함 될 수 중첩 된 조건부 컴파일 지시문 완전 한 집합을 형성 하는 이러한 지시문 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-364">A conditional section may itself contain nested conditional compilation directives provided these directives form complete sets.</span></span>

<span data-ttu-id="19a96-365">A *pp_conditional* 포함 된 중 하나만 선택 *conditional_section*어휘 정상적인 처리에 대 한 s:</span><span class="sxs-lookup"><span data-stu-id="19a96-365">A *pp_conditional* selects at most one of the contained *conditional_section*s for normal lexical processing:</span></span>

*  <span data-ttu-id="19a96-366">*pp_expression*의 합니다 `#if` 하 고 `#elif` 지시문 하나 생성 될 때까지 순서 대로 평가 됩니다 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-366">The *pp_expression*s of the `#if` and `#elif` directives are evaluated in order until one yields `true`.</span></span> <span data-ttu-id="19a96-367">식을 생성 하는 경우 `true`서 *conditional_section* 해당 지시문을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-367">If an expression yields `true`, the *conditional_section* of the corresponding directive is selected.</span></span>
*  <span data-ttu-id="19a96-368">모든 *pp_expression*s yield `false`, 경우에 `#else` 지시문을 사용할 수 있는지를 *conditional_section* 의 `#else` 지시문을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-368">If all *pp_expression*s yield `false`, and if an `#else` directive is present, the *conditional_section* of the `#else` directive is selected.</span></span>
*  <span data-ttu-id="19a96-369">그렇지 않으면, 아니요 *conditional_section* 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-369">Otherwise, no *conditional_section* is selected.</span></span>

<span data-ttu-id="19a96-370">선택한 *conditional_section*정상으로 처리 되는 있는 경우 *input_section*: 어휘 문법 섹션에 포함 된 소스 코드를 준수 해야 합니다; 원본의 토큰이 생성 됩니다 섹션의 코드 있고 섹션에서 전처리 지시문 효력을 발휘 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-370">The selected *conditional_section*, if any, is processed as a normal *input_section*: the source code contained in the section must adhere to the lexical grammar; tokens are generated from the source code in the section; and pre-processing directives in the section have the prescribed effects.</span></span>

<span data-ttu-id="19a96-371">나머지 *conditional_section*s에 있는 경우으로 처리 됩니다 *skipped_section*전처리 지시문 제외 하 고 s:, 섹션에서 소스 코드의 어휘를 준수 하지 해야 문법; 아니요 토큰이; 섹션에서 소스 코드에서 생성 됩니다. 및 섹션에서 전처리 지시문 어휘 적으로 정확 해야 하지만 그렇지 않으면 처리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-371">The remaining *conditional_section*s, if any, are processed as *skipped_section*s: except for pre-processing directives, the source code in the section need not adhere to the lexical grammar; no tokens are generated from the source code in the section; and pre-processing directives in the section must be lexically correct but are not otherwise processed.</span></span> <span data-ttu-id="19a96-372">내를 *conditional_section* 으로 처리 되는 *skipped_section*, 모든 중첩 *conditional_section*s (포함 된 중첩 `#if`... `#endif` 고 `#region`... `#endregion` 생성)으로 처리 됩니다 *skipped_section*s입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-372">Within a *conditional_section* that is being processed as a *skipped_section*, any nested *conditional_section*s (contained in nested `#if`...`#endif` and `#region`...`#endregion` constructs) are also processed as *skipped_section*s.</span></span>

<span data-ttu-id="19a96-373">다음 예제에서는 어떻게 조건부 컴파일을 지시문을 중첩을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-373">The following example illustrates how conditional compilation directives can nest:</span></span>
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

<span data-ttu-id="19a96-374">전처리 지시문을 제외 하 고 생략된 된 소스 코드 어휘 분석 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-374">Except for pre-processing directives, skipped source code is not subject to lexical analysis.</span></span> <span data-ttu-id="19a96-375">예를 들어, 다음은에 종결 되지 않은 주석 불구 하 고 잘못 된 `#else` 섹션:</span><span class="sxs-lookup"><span data-stu-id="19a96-375">For example, the following is valid despite the unterminated comment in the `#else` section:</span></span>
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

<span data-ttu-id="19a96-376">그러나 Note, 전처리 지시문은 소스 코드의 건너뛴된 섹션 에서도 구문적으로 올바른 것으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-376">Note, however, that pre-processing directives are required to be lexically correct even in skipped sections of source code.</span></span>

<span data-ttu-id="19a96-377">여러 줄 입력된 요소 내에서 사용 하는 경우에 전처리 지시문 처리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-377">Pre-processing directives are not processed when they appear inside multi-line input elements.</span></span> <span data-ttu-id="19a96-378">예를 들어 프로그램:</span><span class="sxs-lookup"><span data-stu-id="19a96-378">For example, the program:</span></span>
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
<span data-ttu-id="19a96-379">출력 결과:</span><span class="sxs-lookup"><span data-stu-id="19a96-379">results in the output:</span></span>
```
hello,
#if Debug
        world
#else
        Nebraska
#endif
```

<span data-ttu-id="19a96-380">평가에 따라 달라질 수 있습니다 처리 되는 전처리 지시문 집합이 특이 한 경우에는 *pp_expression*합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-380">In peculiar cases, the set of pre-processing directives that is processed might depend on the evaluation of the *pp_expression*.</span></span> <span data-ttu-id="19a96-381">예제:</span><span class="sxs-lookup"><span data-stu-id="19a96-381">The example:</span></span>
```csharp
#if X
    /*
#else
    /* */ class Q { }
#endif
```
<span data-ttu-id="19a96-382">항상 동일한 토큰 스트림을 생성 (`class` `Q` `{` `}`)의 여부에 관계 없이 `X` 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-382">always produces the same token stream (`class` `Q` `{` `}`), regardless of whether or not `X` is defined.</span></span> <span data-ttu-id="19a96-383">경우 `X` 가 정의 지시문만이 처리 됩니다 `#if` 및 `#endif`때문에 여러 줄 주석.</span><span class="sxs-lookup"><span data-stu-id="19a96-383">If `X` is defined, the only processed directives are `#if` and `#endif`, due to the multi-line comment.</span></span> <span data-ttu-id="19a96-384">경우 `X` 는 정의 되지 않은 다음 세 가지 지시문 (`#if`, `#else`, `#endif`) 지시문 집합의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-384">If `X` is undefined, then three directives (`#if`, `#else`, `#endif`) are part of the directive set.</span></span>

### <a name="diagnostic-directives"></a><span data-ttu-id="19a96-385">진단 지시문</span><span class="sxs-lookup"><span data-stu-id="19a96-385">Diagnostic directives</span></span>

<span data-ttu-id="19a96-386">진단 지시문을 사용 하 여 명시적으로 오류 및 기타 컴파일 시간 오류 및 경고와 마찬가지로에 보고 되는 경고 메시지를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-386">The diagnostic directives are used to explicitly generate error and warning messages that are reported in the same way as other compile-time errors and warnings.</span></span>

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

<span data-ttu-id="19a96-387">예제:</span><span class="sxs-lookup"><span data-stu-id="19a96-387">The example:</span></span>
```csharp
#warning Code review needed before check-in

#if Debug && Retail
    #error A build can't be both debug and retail
#endif

class Test {...}
```
<span data-ttu-id="19a96-388">항상 ("코드 검토 체크 인하기 전에 필요한"), 경고를 생성 하 고 컴파일 시간 오류를 생성 ("빌드 수 없음 디버그와 일반 정품") 하는 경우 조건부 기호 `Debug` 및 `Retail` 가 둘 다 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-388">always produces a warning ("Code review needed before check-in"), and produces a compile-time error ("A build can't be both debug and retail") if the conditional symbols `Debug` and `Retail` are both defined.</span></span> <span data-ttu-id="19a96-389">한 *pp_message* 임의의 텍스트를 포함할 수 있습니다; 특히이 필요 없습니다 잘 구성 된 토큰을 단어의 작은따옴표에 표시 된 대로 `can't`입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-389">Note that a *pp_message* can contain arbitrary text; specifically, it need not contain well-formed tokens, as shown by the single quote in the word `can't`.</span></span>

### <a name="region-directives"></a><span data-ttu-id="19a96-390">Region 지시문</span><span class="sxs-lookup"><span data-stu-id="19a96-390">Region directives</span></span>

<span data-ttu-id="19a96-391">Region 지시문은 명시적으로 소스 코드의 영역을 표시 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-391">The region directives are used to explicitly mark regions of source code.</span></span>

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

<span data-ttu-id="19a96-392">의미 없는 지역;에 연결 된 지역 사용 됩니다 프로그래머가 또는 자동화 된 도구로 소스 코드의 섹션을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-392">No semantic meaning is attached to a region; regions are intended for use by the programmer or by automated tools to mark a section of source code.</span></span> <span data-ttu-id="19a96-393">에 지정 된 메시지를 `#region` 또는 `#endregion` 지시문 마찬가지로 의미가 없는; 지역을 식별할를 으로만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-393">The message specified in a `#region` or `#endregion` directive likewise has no semantic meaning; it merely serves to identify the region.</span></span> <span data-ttu-id="19a96-394">일치 하는 `#region` 하 고 `#endregion` 지시문은 다른 있을 *pp_message*s입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-394">Matching `#region` and `#endregion` directives may have different *pp_message*s.</span></span>

<span data-ttu-id="19a96-395">영역의 어휘 처리:</span><span class="sxs-lookup"><span data-stu-id="19a96-395">The lexical processing of a region:</span></span>
```csharp
#region
...
#endregion
```
<span data-ttu-id="19a96-396">폼의 조건부 컴파일 지시문을 처리 하는 어휘에 정확 하 게 해당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-396">corresponds exactly to the lexical processing of a conditional compilation directive of the form:</span></span>
```csharp
#if true
...
#endif
```

### <a name="line-directives"></a><span data-ttu-id="19a96-397">Line 지시문</span><span class="sxs-lookup"><span data-stu-id="19a96-397">Line directives</span></span>

<span data-ttu-id="19a96-398">줄 지시문 alter 줄 번호 및 소스 파일 이름과 경고 및 오류와 같은 출력에 컴파일러에 의해 보고 되는 호출자 정보 특성에서 사용 되는 데 사용할 수 있습니다 ([호출자 정보 특성](attributes.md#caller-info-attributes)).</span><span class="sxs-lookup"><span data-stu-id="19a96-398">Line directives may be used to alter the line numbers and source file names that are reported by the compiler in output such as warnings and errors, and that are used by caller info attributes ([Caller info attributes](attributes.md#caller-info-attributes)).</span></span>

<span data-ttu-id="19a96-399">줄 지시문을 다른 텍스트 입력에서 C# 소스 코드를 생성 하는 메타 프로그래밍 도구에서 가장 일반적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-399">Line directives are most commonly used in meta-programming tools that generate C# source code from some other text input.</span></span>

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

<span data-ttu-id="19a96-400">없는 경우 `#line` 지시문이 컴파일러 true 줄 번호 및 소스 파일 이름을 출력으로 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-400">When no `#line` directives are present, the compiler reports true line numbers and source file names in its output.</span></span> <span data-ttu-id="19a96-401">처리할 때을 `#line` 지시문을 포함 하는 *line_indicator* 없는 `default`, 컴파일러는 지정 된 줄 번호 (및 파일 이름을 지정 하는 경우)으로 지시문 다음 줄을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-401">When processing a `#line` directive that includes a *line_indicator* that is not `default`, the compiler treats the line after the directive as having the given line number (and file name, if specified).</span></span>

<span data-ttu-id="19a96-402">`#line default` 지시문 모든 이전 #line 지시문의 결과 되돌립니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-402">A `#line default` directive reverses the effect of all preceding #line directives.</span></span> <span data-ttu-id="19a96-403">없는 것 처럼 정확 하 게 컴파일러가 다음 줄에 대해 true 줄 정보를 보고 `#line` 지시문 처리 했습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-403">The compiler reports true line information for subsequent lines, precisely as if no `#line` directives had been processed.</span></span>

<span data-ttu-id="19a96-404">`#line hidden` 지시문 파일에 영향을 주지 않으며 오류를 보고 하는 줄 번호 메시지를 하지만 소스 수준 디버깅 하는 영향 을지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-404">A `#line hidden` directive has no effect on the file and line numbers reported in error messages, but does affect source level debugging.</span></span> <span data-ttu-id="19a96-405">사이 모든 줄을 디버깅할 때를 `#line hidden` 지시문과 후속 `#line` 지시문 (없는 `#line hidden`) 줄 번호 정보가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-405">When debugging, all lines between a `#line hidden` directive and the subsequent `#line` directive (that is not `#line hidden`) have no line number information.</span></span> <span data-ttu-id="19a96-406">디버거에서 코드를 단계별로 실행할 때 이러한 줄 전적으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-406">When stepping through code in the debugger, these lines will be skipped entirely.</span></span>

<span data-ttu-id="19a96-407">*file_name* 와 달리 일반 문자열 리터럴에서 이스케이프 문자 처리 되지 않습니다;는 "`\`"는 일반적인 백슬래시 문자를 단순히 지정 하는 문자는 *file_name*.</span><span class="sxs-lookup"><span data-stu-id="19a96-407">Note that a *file_name* differs from a regular string literal in that escape characters are not processed; the "`\`" character simply designates an ordinary backslash character within a *file_name*.</span></span>

### <a name="pragma-directives"></a><span data-ttu-id="19a96-408">Pragma 지시문</span><span class="sxs-lookup"><span data-stu-id="19a96-408">Pragma directives</span></span>

<span data-ttu-id="19a96-409">`#pragma` 전처리 지시문은 컴파일러 위한 선택적 컨텍스트 정보를 지정 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-409">The `#pragma` preprocessing directive is used to specify optional contextual information to the compiler.</span></span> <span data-ttu-id="19a96-410">에 제공 된 정보는 `#pragma` 지시문 프로그램 의미 체계를 변경 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-410">The information supplied in a `#pragma` directive will never change program semantics.</span></span>

```antlr
pp_pragma
    : whitespace? '#' whitespace? 'pragma' whitespace pragma_body pp_new_line
    ;

pragma_body
    : pragma_warning_body
    ;
```

<span data-ttu-id="19a96-411">C#은 제공 `#pragma` 컴파일러 경고를 제어 하는 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-411">C# provides `#pragma` directives to control compiler warnings.</span></span> <span data-ttu-id="19a96-412">이후 버전의 언어를 추가로 포함 될 수 있습니다 `#pragma` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-412">Future versions of the language may include additional `#pragma` directives.</span></span> <span data-ttu-id="19a96-413">하지만 다른 C# 컴파일러와의 상호 운용성을 위해 Microsoft C# 컴파일러에 알 수 없는 컴파일 오류가 발생 하지 않습니다 `#pragma` 지시문; 경고를 생성 이러한 지시문 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-413">To ensure interoperability with other C# compilers, the Microsoft C# compiler does not issue compilation errors for unknown `#pragma` directives; such directives do however generate warnings.</span></span>

#### <a name="pragma-warning"></a><span data-ttu-id="19a96-414">Pragma 경고</span><span class="sxs-lookup"><span data-stu-id="19a96-414">Pragma warning</span></span>

<span data-ttu-id="19a96-415">`#pragma warning` 후속 프로그램 텍스트를 컴파일하는 동안 메시지 경고의 특정 집합 또는 사용 하지 않도록 설정 하거나 모든 복원 지시문 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-415">The `#pragma warning` directive is used to disable or restore all or a particular set of warning messages during compilation of the subsequent program text.</span></span>

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

<span data-ttu-id="19a96-416">`#pragma warning` 지시문 경고 목록을 생략 하는 모든 경고에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-416">A `#pragma warning` directive that omits the warning list affects all warnings.</span></span> <span data-ttu-id="19a96-417">`#pragma warning` 지시문을 포함 경고 목록에 목록에 지정 된 경고에만 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-417">A `#pragma warning` directive the includes a warning list affects only those warnings that are specified in the list.</span></span>

<span data-ttu-id="19a96-418">`#pragma warning disable` 모든 지시문 비활성화 또는 지정된 된 경고 집합.</span><span class="sxs-lookup"><span data-stu-id="19a96-418">A `#pragma warning disable` directive disables all or the given set of warnings.</span></span>

<span data-ttu-id="19a96-419">`#pragma warning restore` 모든 지시문 복원 또는 컴파일 단위의 시작 부분에 적용 된 상태 경고의 지정된 된 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-419">A `#pragma warning restore` directive restores all or the given set of warnings to the state that was in effect at the beginning of the compilation unit.</span></span> <span data-ttu-id="19a96-420">특정 경고를 외부에서 비활성화 된 경우, `#pragma warning restore` (모든 여부 또는 특정 경고) 해당 경고를 다시 활성화 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-420">Note that if a particular warning was disabled externally, a `#pragma warning restore` (whether for all or the specific warning) will not re-enable that warning.</span></span>

<span data-ttu-id="19a96-421">다음 예제에서는 사용 방법을 보여 줍니다. `#pragma warning` 일시적으로 경고를 해제 하려면 보고 사용 되지 않습니다 하는 경우 Microsoft C# 컴파일러에서 경고 번호를 사용 하 여 멤버가 참조 되기 합니다.</span><span class="sxs-lookup"><span data-stu-id="19a96-421">The following example shows use of `#pragma warning` to temporarily disable the warning reported when obsoleted members are referenced, using the warning number from the Microsoft C# compiler.</span></span>
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
