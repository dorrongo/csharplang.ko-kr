# <a name="documentation-comments"></a><span data-ttu-id="e8edd-101">문서 주석</span><span class="sxs-lookup"><span data-stu-id="e8edd-101">Documentation comments</span></span>

<span data-ttu-id="e8edd-102">C# XML 텍스트를 포함 하는 특수 주석 구문을 사용 하 여 해당 코드를 문서화 하는 프로그래머를 위한 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-102">C# provides a mechanism for programmers to document their code using a special comment syntax that contains XML text.</span></span> <span data-ttu-id="e8edd-103">소스 코드 파일에서 특정 형태가 필요 주석 앞에 있지는 소스 코드 요소를 이러한 주석에서 XML을 생성 하는 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-103">In source code files, comments having a certain form can be used to direct a tool to produce XML from those comments and the source code elements, which they precede.</span></span> <span data-ttu-id="e8edd-104">주석을 사용 하 여 이러한 구문 이라고 ***문서 주석을***합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-104">Comments using such syntax are called ***documentation comments***.</span></span> <span data-ttu-id="e8edd-105">바로 앞에 나오기 (예: 클래스, 대리자 또는 인터페이스) 사용자 정의 형식 또는 멤버 (예: 필드, 이벤트, 속성 또는 메서드).</span><span class="sxs-lookup"><span data-stu-id="e8edd-105">They must immediately precede a user-defined type (such as a class, delegate, or interface) or a member (such as a field, event, property, or method).</span></span> <span data-ttu-id="e8edd-106">XML 생성 도구를 호출 합니다 ***설명서 생성기***합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-106">The XML generation tool is called the ***documentation generator***.</span></span> <span data-ttu-id="e8edd-107">(이 생성기 될 수 있지만 하지 않아도, C# 컴파일러 자체.) 설명서 생성기에서 생성 된 출력 이라고 합니다 ***설명서 파일***합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-107">(This generator could be, but need not be, the C# compiler itself.) The output produced by the documentation generator is called the ***documentation file***.</span></span> <span data-ttu-id="e8edd-108">문서 파일에 대 한 입력으로 사용 됩니다는 ***설명서 뷰어***있으며를 일종의 형식 정보 및 해당 관련된 설명서의 시각적 표시를 생성 하기 위한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-108">A documentation file is used as input to a ***documentation viewer***; a tool intended to produce some sort of visual display of type information and its associated documentation.</span></span>

<span data-ttu-id="e8edd-109">이 사양에 문서 주석을 사용할 태그의 집합을 제안 하지만 이러한 태그의 사용은 필요 하지 있으며 다른 태그 사용할 수 원하는 경우 올바른 형식의 xml 규칙 장기를 따르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-109">This specification suggests a set of tags to be used in documentation comments, but use of these tags is not required, and other tags may be used if desired, as long the rules of well-formed XML are followed.</span></span>

## <a name="introduction"></a><span data-ttu-id="e8edd-110">소개</span><span class="sxs-lookup"><span data-stu-id="e8edd-110">Introduction</span></span>

<span data-ttu-id="e8edd-111">특수 한 형태 필요 주석 앞에 있지는 소스 코드 요소를 이러한 주석에서 XML을 생성 하는 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-111">Comments having a special form can be used to direct a tool to produce XML from those comments and the source code elements, which they precede.</span></span> <span data-ttu-id="e8edd-112">이러한 주석은 슬래시 세 개를 사용 하 여 시작 하는 단일 줄 주석 (`///`), 슬래시 및 두 개의 별을 시작 하는 주석 구분 또는 (`/**`).</span><span class="sxs-lookup"><span data-stu-id="e8edd-112">Such comments are single-line comments that start with three slashes (`///`), or delimited comments that start with a slash and two stars (`/**`).</span></span> <span data-ttu-id="e8edd-113">바로 앞에 나오기 (예: 클래스, 대리자 또는 인터페이스) 사용자 정의 형식 또는 이러한 주석을 추가 하는 멤버 (예: 필드, 이벤트, 속성 또는 메서드).</span><span class="sxs-lookup"><span data-stu-id="e8edd-113">They must immediately precede a user-defined type (such as a class, delegate, or interface) or a member (such as a field, event, property, or method) that they annotate.</span></span> <span data-ttu-id="e8edd-114">특성 섹션 ([특성 사양](attributes.md#attribute-specification)) 문서 주석 형식 또는 멤버에 적용 된 특성 앞에 야 하므로 선언의 일부분으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-114">Attribute sections ([Attribute specification](attributes.md#attribute-specification)) are considered part of declarations, so documentation comments must precede attributes applied to a type or member.</span></span>

<span data-ttu-id="e8edd-115">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-115">__Syntax:__</span></span>

```antlr
single_line_doc_comment
    : '///' input_character*
    ;

delimited_doc_comment
    : '/**' delimited_comment_section* asterisk+ '/'
    ;
```

<span data-ttu-id="e8edd-116">에 *single_line_doc_comment*경우는 *공백* 문자 다음을 `///` 의 각 문자를 *single_line_doc_comment*s 인접 한 현재 *single_line_doc_comment*, 한 다음는 *공백* 문자는 XML 출력에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-116">In a *single_line_doc_comment*, if there is a *whitespace* character following the `///` characters on each of the *single_line_doc_comment*s adjacent to the current *single_line_doc_comment*, then that *whitespace* character is not included in the XML output.</span></span>

<span data-ttu-id="e8edd-117">구분 기호로 분리 된-doc-주석, 두 번째 줄에서 첫 번째 공백이 아닌 문자가 별표와 동일한 패턴의 선택적 공백 문자 및 별표 문자 반복 됩니다 구분-doc-주석 내에서 줄의 각 부분에 그런 다음 반복된 패턴의 문자는 XML 출력에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-117">In a delimited-doc-comment, if the first non-whitespace character on the second line is an asterisk and the same pattern of optional whitespace characters and an asterisk character is repeated at the beginning of each of the line within the delimited-doc-comment, then the characters of the repeated pattern are not included in the XML output.</span></span> <span data-ttu-id="e8edd-118">패턴 뒤와 별표 문자 앞 공백 문자를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-118">The pattern may include whitespace characters after, as well as before, the asterisk character.</span></span>

<span data-ttu-id="e8edd-119">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-119">__Example:__</span></span>

```csharp
/// <summary>Class <c>Point</c> models a point in a two-dimensional
/// plane.</summary>
///
public class Point 
{
    /// <summary>method <c>draw</c> renders the point.</summary>
    void draw() {...}
}
```

<span data-ttu-id="e8edd-120">문서 주석 내의 텍스트는 XML 규칙에 따라 올바른 형식 이어야 합니다 (http://www.w3.org/TR/REC-xml)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-120">The text within documentation comments must be well formed according to the rules of XML (http://www.w3.org/TR/REC-xml).</span></span> <span data-ttu-id="e8edd-121">이면 XML 형식이 잘못 된 형식의 경고가 생성 되 고 문서 파일에 오류가 발생 했습니다 라는 주석이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-121">If the XML is ill formed, a warning is generated and the documentation file will contain a comment saying that an error was encountered.</span></span>

<span data-ttu-id="e8edd-122">권장 되는 집합에 정의 되어 있지만 개발자가 고유한 태그 집합을 만들 [권장 태그](documentation-comments.md#recommended-tags)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-122">Although developers are free to create their own set of tags, a recommended set is defined in [Recommended tags](documentation-comments.md#recommended-tags).</span></span> <span data-ttu-id="e8edd-123">권장 태그 중 일부는 특별한 의미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-123">Some of the recommended tags have special meanings:</span></span>

*  <span data-ttu-id="e8edd-124">`<param>` 태그는 매개 변수를 설명 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-124">The `<param>` tag is used to describe parameters.</span></span> <span data-ttu-id="e8edd-125">이러한 태그를 사용 하는 경우 지정 된 매개 변수가 있고 모든 매개 변수는 문서 주석에서 설명 하는 설명서 생성기 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-125">If such a tag is used, the documentation generator must verify that the specified parameter exists and that all parameters are described in documentation comments.</span></span> <span data-ttu-id="e8edd-126">이러한 확인에 실패할 경우 설명서 생성기는 경고가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-126">If such verification fails, the documentation generator issues a warning.</span></span>
*  <span data-ttu-id="e8edd-127">`cref` 특성을 태그에 연결하여 코드 요소에 대한 참조를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-127">The `cref` attribute can be attached to any tag to provide a reference to a code element.</span></span> <span data-ttu-id="e8edd-128">설명서 생성기는이 코드 요소가 존재 하는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-128">The documentation generator must verify that this code element exists.</span></span> <span data-ttu-id="e8edd-129">확인에 실패 하는 경우 설명서 생성기는 경고가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-129">If the verification fails, the documentation generator issues a warning.</span></span> <span data-ttu-id="e8edd-130">에 설명 된 이름을 검색을 `cref` 특성인 설명서 생성기 네임 스페이스 표시 여부에 따라 지켜야 합니다 `using` 문은 소스 코드 내에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-130">When looking for a name described in a `cref` attribute, the documentation generator must respect namespace visibility according to `using` statements appearing within the source code.</span></span> <span data-ttu-id="e8edd-131">코드 요소를 위한 일반, 일반적인 제네릭 구문 (예: "`List<T>`") 잘못 된 XML을 생성 하기 때문에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-131">For code elements that are generic, the normal generic syntax (ie "`List<T>`") cannot be used because it produces invalid XML.</span></span> <span data-ttu-id="e8edd-132">중괄호가 대괄호 대신 사용할 수 있습니다 (ie "`List{T}`"), 또는 XML 이스케이프 구문을 사용할 수 있습니다 (즉 "`List&lt;T&gt;`").</span><span class="sxs-lookup"><span data-stu-id="e8edd-132">Braces can be used instead of brackets (ie "`List{T}`"), or the XML escape syntax can be used (ie "`List&lt;T&gt;`").</span></span>
*  <span data-ttu-id="e8edd-133">`<summary>` 태그 형식 또는 멤버에 대 한 추가 정보를 표시할 설명서 뷰어를 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-133">The `<summary>` tag is intended to be used by a documentation viewer to display additional information about a type or member.</span></span>
*  <span data-ttu-id="e8edd-134">`<include>` 태그 외부 XML 파일에서 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-134">The `<include>` tag includes information from an external XML file.</span></span>

<span data-ttu-id="e8edd-135">주의 깊게 살펴보십시오 설명서 파일 형식 및 멤버에 대 한 전체 정보를 제공 하지 않습니다 (예를 들어이 포함 되지 않은 모든 형식 정보).</span><span class="sxs-lookup"><span data-stu-id="e8edd-135">Note carefully that the documentation file does not provide full information about the type and members (for example, it does not contain any type information).</span></span> <span data-ttu-id="e8edd-136">형식 또는 멤버에 대 한 이러한 정보를 가져오려면 실제 형식 또는 멤버에서 리플렉션 사용 하 여 함께에서 설명서 파일을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-136">To get such information about a type or member, the documentation file must be used in conjunction with reflection on the actual type or member.</span></span>

## <a name="recommended-tags"></a><span data-ttu-id="e8edd-137">권장된 태그</span><span class="sxs-lookup"><span data-stu-id="e8edd-137">Recommended tags</span></span>

<span data-ttu-id="e8edd-138">설명서 생성기는 수락 하 고 XML 규칙에 따라 유효한 모든 태그를 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-138">The documentation generator must accept and process any tag that is valid according to the rules of XML.</span></span> <span data-ttu-id="e8edd-139">다음 태그가 사용자 설명서에서 자주 사용 되는 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-139">The following tags provide commonly used functionality in user documentation.</span></span> <span data-ttu-id="e8edd-140">(물론, 다른 태그가 있을 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="e8edd-140">(Of course, other tags are possible.)</span></span>


| <span data-ttu-id="e8edd-141">__태그__</span><span class="sxs-lookup"><span data-stu-id="e8edd-141">__Tag__</span></span>          | <span data-ttu-id="e8edd-142">__섹션__</span><span class="sxs-lookup"><span data-stu-id="e8edd-142">__Section__</span></span>                                            | <span data-ttu-id="e8edd-143">__용도__</span><span class="sxs-lookup"><span data-stu-id="e8edd-143">__Purpose__</span></span>                                            |
|------------------|--------------------------------------------------------|--------------------------------------------------------|
| `<c>`            | [`<c>`](documentation-comments.md#c)                   | <span data-ttu-id="e8edd-144">코드 형태의 글꼴로 텍스트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-144">Set text in a code-like font</span></span>                           | 
| `<code>`         | [`<code>`](documentation-comments.md#code)             | <span data-ttu-id="e8edd-145">원본 코드나 프로그램 출력 줄을 하나 이상 설정</span><span class="sxs-lookup"><span data-stu-id="e8edd-145">Set one or more lines of source code or program output</span></span> |
| `<example>`      | [`<example>`](documentation-comments.md#example)       | <span data-ttu-id="e8edd-146">예를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-146">Indicate an example</span></span>                                    |
| `<exception>`    | [`<exception>`](documentation-comments.md#exception)   | <span data-ttu-id="e8edd-147">메서드에서 예외를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-147">Identifies the exceptions a method can throw</span></span>           |
| `<include>`      | [`<include>`](documentation-comments.md#include)       | <span data-ttu-id="e8edd-148">외부 파일에서 XML을 포함</span><span class="sxs-lookup"><span data-stu-id="e8edd-148">Includes XML from an external file</span></span>                     |
| `<list>`         | [`<list>`](documentation-comments.md#list)             | <span data-ttu-id="e8edd-149">목록 또는 테이블을 만듭니다</span><span class="sxs-lookup"><span data-stu-id="e8edd-149">Create a list or table</span></span>                                 |
| `<para>`         | [`<para>`](documentation-comments.md#para)             | <span data-ttu-id="e8edd-150">텍스트에 추가 될 구조를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-150">Permit structure to be added to text</span></span>                   |
| `<param>`        | [`<param>`](documentation-comments.md#param)           | <span data-ttu-id="e8edd-151">메서드 또는 생성자에 대 한 매개 변수를 설명</span><span class="sxs-lookup"><span data-stu-id="e8edd-151">Describe a parameter for a method or constructor</span></span>       |
| `<paramref>`     | [`<paramref>`](documentation-comments.md#paramref)     | <span data-ttu-id="e8edd-152">단어 매개 변수 이름 인지 확인</span><span class="sxs-lookup"><span data-stu-id="e8edd-152">Identify that a word is a parameter name</span></span>               |
| `<permission>`   | [`<permission>`](documentation-comments.md#permission) | <span data-ttu-id="e8edd-153">문서는 멤버의 보안 액세스 가능성</span><span class="sxs-lookup"><span data-stu-id="e8edd-153">Document the security accessibility of a member</span></span>        |
| `<remark>`       | [`<remark>`](documentation-comments.md#remark)         | <span data-ttu-id="e8edd-154">형식에 대 한 추가 정보를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-154">Describe additional information about a type</span></span>           |
| `<returns>`      | [`<returns>`](documentation-comments.md#returns)       | <span data-ttu-id="e8edd-155">메서드의 반환 값 설명</span><span class="sxs-lookup"><span data-stu-id="e8edd-155">Describe the return value of a method</span></span>                  |
| `<see>`          | [`<see>`](documentation-comments.md#see)               | <span data-ttu-id="e8edd-156">링크를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-156">Specify a link</span></span>                                         |
| `<seealso>`      | [`<seealso>`](documentation-comments.md#seealso)       | <span data-ttu-id="e8edd-157">참고 항목을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-157">Generate a See Also entry</span></span>                              |
| `<summary>`      | [`<summary>`](documentation-comments.md#summary)       | <span data-ttu-id="e8edd-158">형식 또는 형식의 멤버를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-158">Describe a type or a member of a type</span></span>                  |
| `<value>`        | [`<value>`](documentation-comments.md#value)           | <span data-ttu-id="e8edd-159">속성 설명</span><span class="sxs-lookup"><span data-stu-id="e8edd-159">Describe a property</span></span>                                    |
| `<typeparam>`    |                                                        | <span data-ttu-id="e8edd-160">제네릭 형식 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-160">Describe a generic type parameter</span></span>                      |
| `<typeparamref>` |                                                        | <span data-ttu-id="e8edd-161">단어 형식 매개 변수 이름 식별</span><span class="sxs-lookup"><span data-stu-id="e8edd-161">Identify that a word is a type parameter name</span></span>          |

### `<c>`

<span data-ttu-id="e8edd-162">이 태그 설명 내의 텍스트의 일부 코드 블록에 사용 되는 것과 같은 특수 한 글꼴로 설정 되어야 함을 나타낼 수 있는 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-162">This tag provides a mechanism to indicate that a fragment of text within a description should be set in a special font such as that used for a block of code.</span></span> <span data-ttu-id="e8edd-163">실제 코드 줄을 사용 하 여 `<code>` ([`<code>`](documentation-comments.md#code)).</span><span class="sxs-lookup"><span data-stu-id="e8edd-163">For lines of actual code, use `<code>` ([`<code>`](documentation-comments.md#code)).</span></span>

<span data-ttu-id="e8edd-164">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-164">__Syntax:__</span></span>

```xml
<c>text</c>
```

<span data-ttu-id="e8edd-165">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-165">__Example:__</span></span>

```csharp
/// <summary>Class <c>Point</c> models a point in a two-dimensional
/// plane.</summary>

public class Point 
{
    // ...
}
```

### `<code>`

<span data-ttu-id="e8edd-166">이 태그 소스 코드나 프로그램 출력의 하나 이상의 줄 일부 특수 한 글꼴로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-166">This tag is used to set one or more lines of source code or program output in some special font.</span></span> <span data-ttu-id="e8edd-167">내 러 티브에 작은 코드 조각을 사용 하 여 `<c>` ([`<c>`](documentation-comments.md#c)).</span><span class="sxs-lookup"><span data-stu-id="e8edd-167">For small code fragments in narrative, use `<c>` ([`<c>`](documentation-comments.md#c)).</span></span>

<span data-ttu-id="e8edd-168">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-168">__Syntax:__</span></span>

```xml
<code>source code or program output</code>
```

<span data-ttu-id="e8edd-169">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-169">__Example:__</span></span>

```csharp
/// <summary>This method changes the point's location by
///    the given x- and y-offsets.
/// <example>For example:
/// <code>
///    Point p = new Point(3,5);
///    p.Translate(-1,3);
/// </code>
/// results in <c>p</c>'s having the value (2,8).
/// </example>
/// </summary>

public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}   
```

### `<example>`

<span data-ttu-id="e8edd-170">이 태그는 메서드 또는 기타 라이브러리 멤버 사용할 수 있습니다 하는 방법을 지정 하는 주석 내에서 예제 코드를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-170">This tag allows example code within a comment, to specify how a method or other library member may be used.</span></span> <span data-ttu-id="e8edd-171">일반적으로 또한 여기에 태그를 사용 하 `<code>` ([`<code>`](documentation-comments.md#code))도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-171">Ordinarily, this would also involve use of the tag `<code>` ([`<code>`](documentation-comments.md#code)) as well.</span></span>

<span data-ttu-id="e8edd-172">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-172">__Syntax:__</span></span>

```xml
<example>description</example>
```

<span data-ttu-id="e8edd-173">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-173">__Example:__</span></span>

<span data-ttu-id="e8edd-174">참조 `<code>` ([`<code>`](documentation-comments.md#code)) 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-174">See `<code>` ([`<code>`](documentation-comments.md#code)) for an example.</span></span>

### `<exception>`

<span data-ttu-id="e8edd-175">이 태그는 메서드에서 예외를 문서화 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-175">This tag provides a way to document the exceptions a method can throw.</span></span>

<span data-ttu-id="e8edd-176">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-176">__Syntax:__</span></span>

```xml
<exception cref="member">description</exception>
```

<span data-ttu-id="e8edd-177">형식에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="e8edd-177">where</span></span>

* <span data-ttu-id="e8edd-178">`member` 멤버의 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-178">`member` is the name of a member.</span></span> <span data-ttu-id="e8edd-179">설명서 생성기는 지정된 된 멤버 있는지 확인 한 변환 `member` 설명서 파일의 정식 요소 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-179">The documentation generator checks that the given member exists and translates `member` to the canonical element name in the documentation file.</span></span>
* <span data-ttu-id="e8edd-180">`description` 예외가 throw 되는 상황의 설명이입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-180">`description` is a description of the circumstances in which the exception is thrown.</span></span>

<span data-ttu-id="e8edd-181">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-181">__Example:__</span></span>

```csharp
public class DataBaseOperations
{
    /// <exception cref="MasterFileFormatCorruptException"></exception>
    /// <exception cref="MasterFileLockedOpenException"></exception>
    public static void ReadRecord(int flag) {
        if (flag == 1)
            throw new MasterFileFormatCorruptException();
        else if (flag == 2)
            throw new MasterFileLockedOpenException();
        // ...
    } 
}
```

### `<include>`

<span data-ttu-id="e8edd-182">이 태그를 사용 하면 외부 소스 코드 파일에 있는 XML 문서에서 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-182">This tag allows including information from an XML document that is external to the source code file.</span></span> <span data-ttu-id="e8edd-183">외부 파일은 올바른 형식의 XML 문서를 이어야 하 고 XPath 식을 포함 하는 문서에서 어떤 XML을 지정 하는 문서에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-183">The external file must be a well-formed XML document, and an XPath expression is applied to that document to specify what XML from that document to include.</span></span> <span data-ttu-id="e8edd-184">`<include>` 태그 외부 문서에서 선택한 XML로 대체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-184">The `<include>` tag is then replaced with the selected XML from the external document.</span></span>

<span data-ttu-id="e8edd-185">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-185">__Syntax:__</span></span>

```
<include file="filename" path="xpath" />
```

<span data-ttu-id="e8edd-186">형식에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="e8edd-186">where</span></span>

* <span data-ttu-id="e8edd-187">`filename` 외부 XML 파일의 파일 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-187">`filename` is the file name of an external XML file.</span></span> <span data-ttu-id="e8edd-188">파일 이름 포함 태그를 포함 하는 파일을 기준으로 해석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-188">The file name is interpreted relative to the file that contains the include tag.</span></span>
* <span data-ttu-id="e8edd-189">`xpath` 외부 XML 파일에서 XML의 일부를 선택 하는 XPath 식이입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-189">`xpath` is an XPath expression that selects some of the XML in the external XML file.</span></span>

<span data-ttu-id="e8edd-190">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-190">__Example:__</span></span>

<span data-ttu-id="e8edd-191">같은 선언을 포함 하는 소스 코드:</span><span class="sxs-lookup"><span data-stu-id="e8edd-191">If the source code contained a declaration like:</span></span>

```csharp
/// <include file="docs.xml" path='extradoc/class[@name="IntList"]/*' />
public class IntList { ... }
```

<span data-ttu-id="e8edd-192">및 "docs.xml" 외부 파일에 다음 내용이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-192">and the external file "docs.xml" had the following contents:</span></span>

```xml
<?xml version="1.0"?>
<extradoc>
  <class name="IntList">
     <summary>
        Contains a list of integers.
     </summary>
  </class>
  <class name="StringList">
     <summary>
        Contains a list of integers.
     </summary>
  </class>
</extradoc>
```

<span data-ttu-id="e8edd-193">그런 다음 동일한 설명서는 소스 코드를 포함 하는 경우에 따라 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-193">then the same documentation is output as if the source code contained:</span></span>

```csharp
/// <summary>
///    Contains a list of integers.
/// </summary>
public class IntList { ... }
```

### `<list>`

<span data-ttu-id="e8edd-194">이 태그는 목록 또는 항목의 테이블을 만드는 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-194">This tag is used to create a list or table of items.</span></span> <span data-ttu-id="e8edd-195">포함할 수 있습니다는 `<listheader>` 테이블 또는 정의 목록의 머리글 행을 정의 하는 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-195">It may contain a `<listheader>` block to define the heading row of either a table or definition list.</span></span> <span data-ttu-id="e8edd-196">(테이블에 대 한 항목을 정의할 때 `term` 머리글에 제공 해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="e8edd-196">(When defining a table, only an entry for `term` in the heading need be supplied.)</span></span>

<span data-ttu-id="e8edd-197">지정 된 목록의 각 항목을 `<item>` 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-197">Each item in the list is specified with an `<item>` block.</span></span> <span data-ttu-id="e8edd-198">정의 목록을 만들 때 둘 다 `term` 고 `description` 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-198">When creating a definition list, both `term` and `description` must be specified.</span></span> <span data-ttu-id="e8edd-199">그러나에 대 한 테이블, 글머리 기호 목록 또는 번호 매기기 목록만 `description` 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-199">However, for a table, bulleted list, or numbered list, only `description` need be specified.</span></span>

<span data-ttu-id="e8edd-200">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-200">__Syntax:__</span></span>

```xml
<list type="bullet" | "number" | "table">
   <listheader>
      <term>term</term>
      <description>*description*</description>
   </listheader>
   <item>
      <term>term</term>
      <description>*description*</description>
   </item>
    ...
   <item>
      <term>term</term>
      <description>description</description>
   </item>
</list>
```

<span data-ttu-id="e8edd-201">형식에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="e8edd-201">where</span></span>

* <span data-ttu-id="e8edd-202">`term` 해당 정의 용어를 정의 하려면 `description`합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-202">`term` is the term to define, whose definition is in `description`.</span></span>
* <span data-ttu-id="e8edd-203">`description` 글머리 기호 또는 번호 매기기 목록에서 항목 또는 정의 되는 `term`합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-203">`description` is either an item in a bullet or numbered list, or the definition of a `term`.</span></span>

<span data-ttu-id="e8edd-204">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-204">__Example:__</span></span>

```csharp
public class MyClass
{
    /// <summary>Here is an example of a bulleted list:
    /// <list type="bullet">
    /// <item>
    /// <description>Item 1.</description>
    /// </item>
    /// <item>
    /// <description>Item 2.</description>
    /// </item>
    /// </list>
    /// </summary>
    public static void Main () {
        // ...
    }
}
```

### `<para>`

<span data-ttu-id="e8edd-205">이 태그와 같은 다른 태그 안에 사용 하는 `<summary>` ([`<remark>`](documentation-comments.md#remark)) 또는 `<returns>` ([`<returns>`](documentation-comments.md#returns)), 텍스트를 추가할 수는 구조를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-205">This tag is for use inside other tags, such as `<summary>` ([`<remark>`](documentation-comments.md#remark)) or `<returns>` ([`<returns>`](documentation-comments.md#returns)), and permits structure to be added to text.</span></span>

<span data-ttu-id="e8edd-206">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-206">__Syntax:__</span></span>

```xml
<para>content</para>
```

<span data-ttu-id="e8edd-207">여기서 `content` 단락의 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-207">where `content` is the text of the paragraph.</span></span>

<span data-ttu-id="e8edd-208">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-208">__Example:__</span></span>

```csharp
/// <summary>This is the entry point of the Point class testing program.
/// <para>This program tests each method and operator, and
/// is intended to be run after any non-trivial maintenance has
/// been performed on the Point class.</para></summary>
public static void Main() {
    // ...
}
```

### `<param>`

<span data-ttu-id="e8edd-209">이 태그는 메서드, 생성자 또는 인덱서 매개 변수를 설명 하기 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-209">This tag is used to describe a parameter for a method, constructor, or indexer.</span></span>

<span data-ttu-id="e8edd-210">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-210">__Syntax:__</span></span>

```xml
<param name="name">description</param>
```

<span data-ttu-id="e8edd-211">형식에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="e8edd-211">where</span></span>

* <span data-ttu-id="e8edd-212">`name` 매개 변수의 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-212">`name` is the name of the parameter.</span></span>
* <span data-ttu-id="e8edd-213">`description` 매개 변수의 설명이입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-213">`description` is a description of the parameter.</span></span>

<span data-ttu-id="e8edd-214">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-214">__Example:__</span></span>

```csharp
/// <summary>This method changes the point's location to
///    the given coordinates.</summary>
/// <param name="xor">the new x-coordinate.</param>
/// <param name="yor">the new y-coordinate.</param>
public void Move(int xor, int yor) {
    X = xor;
    Y = yor;
}
```

### `<paramref>`

<span data-ttu-id="e8edd-215">이 태그는 단어 매개 변수임을 나타내기 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-215">This tag is used to indicate that a word is a parameter.</span></span> <span data-ttu-id="e8edd-216">문서 파일을 다른 방식으로이 매개 변수 형식을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-216">The documentation file can be processed to format this parameter in some distinct way.</span></span>

<span data-ttu-id="e8edd-217">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-217">__Syntax:__</span></span>

```xml
<paramref name="name"/>
```

<span data-ttu-id="e8edd-218">여기서 `name` 매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-218">where `name` is the name of the parameter.</span></span>

<span data-ttu-id="e8edd-219">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-219">__Example:__</span></span>

```csharp
/// <summary>This constructor initializes the new Point to
///    (<paramref name="xor"/>,<paramref name="yor"/>).</summary>
/// <param name="xor">the new Point's x-coordinate.</param>
/// <param name="yor">the new Point's y-coordinate.</param>

public Point(int xor, int yor) {
    X = xor;
    Y = yor;
}
```

### `<permission>`

<span data-ttu-id="e8edd-220">이 태그는 문서화 멤버의 보안 액세스 가능성을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-220">This tag allows the security accessibility of a member to be documented.</span></span>

<span data-ttu-id="e8edd-221">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-221">__Syntax:__</span></span>

```xml
<permission cref="member">description</permission>
```

<span data-ttu-id="e8edd-222">형식에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="e8edd-222">where</span></span>

* <span data-ttu-id="e8edd-223">`member` 멤버의 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-223">`member` is the name of a member.</span></span> <span data-ttu-id="e8edd-224">설명서 생성기는 지정 된 코드 요소가 있는지 확인 한 변환 *멤버* 설명서 파일의 정식 요소 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-224">The documentation generator checks that the given code element exists and translates *member* to the canonical element name in the documentation file.</span></span>
* <span data-ttu-id="e8edd-225">`description` 멤버에 대 한 액세스의 설명이입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-225">`description` is a description of the access to the member.</span></span>

<span data-ttu-id="e8edd-226">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-226">__Example:__</span></span>

```csharp
/// <permission cref="System.Security.PermissionSet">Everyone can
/// access this method.</permission>

public static void Test() {
    // ...
}
```

### `<remark>`

<span data-ttu-id="e8edd-227">이 태그는 형식에 대 한 추가 정보를 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-227">This tag is used to specify extra information about a type.</span></span> <span data-ttu-id="e8edd-228">(사용 하 여 `<summary>` ([`<summary>`](documentation-comments.md#summary)) 자체 형식 및 형식 멤버를 설명 합니다.)</span><span class="sxs-lookup"><span data-stu-id="e8edd-228">(Use `<summary>` ([`<summary>`](documentation-comments.md#summary)) to describe the type itself and the members of a type.)</span></span>

<span data-ttu-id="e8edd-229">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-229">__Syntax:__</span></span>

```xml
<remark>description</remark>
```

<span data-ttu-id="e8edd-230">여기서 `description` 텍스트는 주석입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-230">where `description` is the text of the remark.</span></span>

<span data-ttu-id="e8edd-231">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-231">__Example:__</span></span>

```csharp
/// <summary>Class <c>Point</c> models a point in a 
/// two-dimensional plane.</summary>
/// <remark>Uses polar coordinates</remark>
public class Point 
{
    // ...
}
```

### `<returns>`

<span data-ttu-id="e8edd-232">이 태그는 메서드의 반환 값을 설명 하기 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-232">This tag is used to describe the return value of a method.</span></span>

<span data-ttu-id="e8edd-233">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-233">__Syntax:__</span></span>

```xml
<returns>description</returns>
```

<span data-ttu-id="e8edd-234">여기서 `description` 반환 값에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-234">where `description` is a description of the return value.</span></span>

<span data-ttu-id="e8edd-235">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-235">__Example:__</span></span>

```csharp
/// <summary>Report a point's location as a string.</summary>
/// <returns>A string representing a point's location, in the form (x,y),
///    without any leading, trailing, or embedded whitespace.</returns>
public override string ToString() {
    return "(" + X + "," + Y + ")";
}
```

### `<see>`

<span data-ttu-id="e8edd-236">이 태그 링크를 텍스트 내에서 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-236">This tag allows a link to be specified within text.</span></span> <span data-ttu-id="e8edd-237">사용 하 여 `<seealso>` ([`<seealso>`](documentation-comments.md#seealso)) 섹션에 표시 되는 텍스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-237">Use `<seealso>` ([`<seealso>`](documentation-comments.md#seealso)) to indicate text that is to appear in a See Also section.</span></span>

<span data-ttu-id="e8edd-238">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-238">__Syntax:__</span></span>

```xml
<see cref="member"/>
```

<span data-ttu-id="e8edd-239">여기서 `member` 멤버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-239">where `member` is the name of a member.</span></span> <span data-ttu-id="e8edd-240">설명서 생성기는 지정 된 코드 요소가 있으며 변경 확인 *멤버* 를 생성 된 문서 파일의 요소 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-240">The documentation generator checks that the given code element exists and changes *member* to the element name in the generated documentation file.</span></span>

<span data-ttu-id="e8edd-241">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-241">__Example:__</span></span>

```csharp
/// <summary>This method changes the point's location to
///    the given coordinates.</summary>
/// <see cref="Translate"/>
public void Move(int xor, int yor) {
    X = xor;
    Y = yor;
}

/// <summary>This method changes the point's location by
///    the given x- and y-offsets.
/// </summary>
/// <see cref="Move"/>
public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}
```

### `<seealso>`

<span data-ttu-id="e8edd-242">이 태그 항목을 참고 항목 섹션에 대해 생성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-242">This tag allows an entry to be generated for the See Also section.</span></span> <span data-ttu-id="e8edd-243">사용 하 여 `<see>` ([`<see>`](documentation-comments.md#see)) 텍스트 내부에서 링크를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-243">Use `<see>` ([`<see>`](documentation-comments.md#see)) to specify a link from within text.</span></span>

<span data-ttu-id="e8edd-244">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-244">__Syntax:__</span></span>

```xml
<seealso cref="member"/>
```

<span data-ttu-id="e8edd-245">여기서 `member` 멤버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-245">where `member` is the name of a member.</span></span> <span data-ttu-id="e8edd-246">설명서 생성기는 지정 된 코드 요소가 있으며 변경 확인 *멤버* 를 생성 된 문서 파일의 요소 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-246">The documentation generator checks that the given code element exists and changes *member* to the element name in the generated documentation file.</span></span>

<span data-ttu-id="e8edd-247">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-247">__Example:__</span></span>

```csharp
/// <summary>This method determines whether two Points have the same
///    location.</summary>
/// <seealso cref="operator=="/>
/// <seealso cref="operator!="/>
public override bool Equals(object o) {
    // ...
}
```

### `<summary>`

이 태그는 형식 또는 형식 멤버를 설명 하기 위해 사용할 수 있습니다. <span data-ttu-id="e8edd-249">사용 하 여 `<remark>` ([`<remark>`](documentation-comments.md#remark)) 자체 형식을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-249">Use `<remark>` ([`<remark>`](documentation-comments.md#remark)) to describe the type itself.</span></span>

<span data-ttu-id="e8edd-250">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-250">__Syntax:__</span></span>

```xml
<summary>description</summary>
```

<span data-ttu-id="e8edd-251">여기서 `description` 형식 또는 멤버 요약이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-251">where `description` is a summary of the type or member.</span></span>

<span data-ttu-id="e8edd-252">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-252">__Example:__</span></span>

```csharp
/// <summary>This constructor initializes the new Point to (0,0).</summary>
public Point() : this(0,0) {
}
```

### `<value>`

<span data-ttu-id="e8edd-253">이 태그는 속성을을 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-253">This tag allows a property to be described.</span></span>

<span data-ttu-id="e8edd-254">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-254">__Syntax:__</span></span>

```xml
<value>property description</value>
```

<span data-ttu-id="e8edd-255">여기서 `property description` 속성에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-255">where `property description` is a description for the property.</span></span>

<span data-ttu-id="e8edd-256">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-256">__Example:__</span></span>

```csharp
/// <value>Property <c>X</c> represents the point's x-coordinate.</value>
public int X
{
    get { return x; }
    set { x = value; }
}
```

### `<typeparam>`

<span data-ttu-id="e8edd-257">이 태그는 클래스, 구조체, 인터페이스, 대리자 또는 메서드는 제네릭 형식 매개 변수를 설명 하기 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-257">This tag is used to describe a generic type parameter for a class, struct, interface, delegate, or method.</span></span>

<span data-ttu-id="e8edd-258">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-258">__Syntax:__</span></span>

```xml
<typeparam name="name">description</typeparam>
```

<span data-ttu-id="e8edd-259">여기서 `name` 형식 매개 변수의 이름 및 `description` 해당 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-259">where `name` is the name of the type parameter, and `description` is its description.</span></span>

<span data-ttu-id="e8edd-260">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-260">__Example:__</span></span>

```csharp
/// <summary>A generic list class.</summary>
/// <typeparam name="T">The type stored by the list.</typeparam>
public class MyList<T> {
    ...
}
```

### `<typeparamref>`

<span data-ttu-id="e8edd-261">이 태그는 단어 형식 매개 변수 인지 나타내기 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-261">This tag is used to indicate that a word is a type parameter.</span></span> <span data-ttu-id="e8edd-262">문서 파일을 다른 방식으로이 형식 매개 변수 형식을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-262">The documentation file can be processed to format this type parameter in some distinct way.</span></span>

<span data-ttu-id="e8edd-263">__구문:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-263">__Syntax:__</span></span>

```xml
<typeparamref name="name"/>
```

<span data-ttu-id="e8edd-264">여기서 `name` 형식 매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-264">where `name` is the name of the type parameter.</span></span>

<span data-ttu-id="e8edd-265">__예제:__</span><span class="sxs-lookup"><span data-stu-id="e8edd-265">__Example:__</span></span>

```csharp
/// <summary>This method fetches data and returns a list of <typeparamref name="T"/>.</summary>
/// <param name="query">query to execute</param>
public List<T> FetchData<T>(string query) {
    ...
}
```

## <a name="processing-the-documentation-file"></a><span data-ttu-id="e8edd-266">문서 파일 처리</span><span class="sxs-lookup"><span data-stu-id="e8edd-266">Processing the documentation file</span></span>

<span data-ttu-id="e8edd-267">설명서 생성기 설명서 주석을 사용 하 여 태그가 지정 되는 소스 코드의 각 요소에 대 한 ID 문자열을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-267">The documentation generator generates an ID string for each element in the source code that is tagged with a documentation comment.</span></span> <span data-ttu-id="e8edd-268">이 ID 문자열 소스 요소를 고유 하 게 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-268">This ID string uniquely identifies a source element.</span></span> <span data-ttu-id="e8edd-269">설명서 뷰어 설명서 적용 되는 해당 메타 데이터/리플렉션 항목을 식별 하는 ID 문자열을 사용할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-269">A documentation viewer can use an ID string to identify the corresponding metadata/reflection item to which the documentation applies.</span></span>

<span data-ttu-id="e8edd-270">문서 파일을 소스 코드의 계층적 표현이 아닙니다. 대신, 각 요소에 대해 생성 된 ID 문자열을 사용 하 여 플랫 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-270">The documentation file is not a hierarchical representation of the source code; rather, it is a flat list with a generated ID string for each element.</span></span>

### <a name="id-string-format"></a><span data-ttu-id="e8edd-271">ID 문자열 형식</span><span class="sxs-lookup"><span data-stu-id="e8edd-271">ID string format</span></span>

<span data-ttu-id="e8edd-272">설명서 생성기는 ID 문자열을 생성할 때 다음 규칙을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-272">The documentation generator observes the following rules when it generates the ID strings:</span></span>

*  <span data-ttu-id="e8edd-273">문자열에 공백이 배치되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-273">No white space is placed in the string.</span></span>

*  <span data-ttu-id="e8edd-274">첫 번째 부분 문자열 뒤에 콜론 문자 하나를 통해 문서화 되 고 멤버의 종류를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-274">The first part of the string identifies the kind of member being documented, via a single character followed by a colon.</span></span> <span data-ttu-id="e8edd-275">다음과 같은 유형의 멤버를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-275">The following kinds of members are defined:</span></span>

   | <span data-ttu-id="e8edd-276">__문자__</span><span class="sxs-lookup"><span data-stu-id="e8edd-276">__Character__</span></span> | <span data-ttu-id="e8edd-277">__설명__</span><span class="sxs-lookup"><span data-stu-id="e8edd-277">__Description__</span></span>                                             |
   |---------------|-------------------------------------------------------------|
   | <span data-ttu-id="e8edd-278">E</span><span class="sxs-lookup"><span data-stu-id="e8edd-278">E</span></span>             | <span data-ttu-id="e8edd-279">이벤트(event)</span><span class="sxs-lookup"><span data-stu-id="e8edd-279">Event</span></span>                                                       |
   | <span data-ttu-id="e8edd-280">F</span><span class="sxs-lookup"><span data-stu-id="e8edd-280">F</span></span>             | <span data-ttu-id="e8edd-281">필드</span><span class="sxs-lookup"><span data-stu-id="e8edd-281">Field</span></span>                                                       |
   | <span data-ttu-id="e8edd-282">M</span><span class="sxs-lookup"><span data-stu-id="e8edd-282">M</span></span>             | <span data-ttu-id="e8edd-283">메서드 (생성자, 소멸자, 연산자 등)</span><span class="sxs-lookup"><span data-stu-id="e8edd-283">Method (including constructors, destructors, and operators)</span></span> |
   | <span data-ttu-id="e8edd-284">N</span><span class="sxs-lookup"><span data-stu-id="e8edd-284">N</span></span>             | <span data-ttu-id="e8edd-285">네임스페이스</span><span class="sxs-lookup"><span data-stu-id="e8edd-285">Namespace</span></span>                                                   |
   | <span data-ttu-id="e8edd-286">P</span><span class="sxs-lookup"><span data-stu-id="e8edd-286">P</span></span>             | <span data-ttu-id="e8edd-287">속성 (인덱서 포함)</span><span class="sxs-lookup"><span data-stu-id="e8edd-287">Property (including indexers)</span></span>                               |
   | <span data-ttu-id="e8edd-288">T</span><span class="sxs-lookup"><span data-stu-id="e8edd-288">T</span></span>             | <span data-ttu-id="e8edd-289">형식 (예: 클래스, 대리자, 열거형, 인터페이스 및 구조체)</span><span class="sxs-lookup"><span data-stu-id="e8edd-289">Type (such as class, delegate, enum, interface, and struct)</span></span> |
   | <span data-ttu-id="e8edd-290">!</span><span class="sxs-lookup"><span data-stu-id="e8edd-290">!</span></span>             | <span data-ttu-id="e8edd-291">오류 문자열입니다. 문자열의 나머지 부분 오류에 대 한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-291">Error string; the rest of the string provides information about the error.</span></span> <span data-ttu-id="e8edd-292">예를 들어 설명서 생성기는 확인할 수 없는 링크에 대 한 오류 정보를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-292">For example, the documentation generator generates error information for links that cannot be resolved.</span></span> |

*  <span data-ttu-id="e8edd-293">문자열의, 두 번째 부분은 네임 스페이스의 루트부터 요소는 정규화 된 이름을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-293">The second part of the string is the fully qualified name of the element, starting at the root of the namespace.</span></span> <span data-ttu-id="e8edd-294">요소, 바깥쪽 형식 및 네임 스페이스의 이름은 마침표로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-294">The name of the element, its enclosing type(s), and namespace are separated by periods.</span></span> <span data-ttu-id="e8edd-295">항목 자체의 이름에 마침표를으로 교체 될 때 `#(U+0023)` 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-295">If the name of the item itself has periods, they are replaced by `#(U+0023)` characters.</span></span> <span data-ttu-id="e8edd-296">(가정 없음 요소 이름에이 문자에.)</span><span class="sxs-lookup"><span data-stu-id="e8edd-296">(It is assumed that no element has this character in its name.)</span></span>
*  <span data-ttu-id="e8edd-297">메서드와 인수를 사용 하 여 속성에 대 한 인수는 괄호로 묶인 같이 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-297">For methods and properties with arguments, the argument list follows, enclosed in parentheses.</span></span> <span data-ttu-id="e8edd-298">인수 없이 대해서 괄호는 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-298">For those without arguments, the parentheses are omitted.</span></span> <span data-ttu-id="e8edd-299">인수는 쉼표로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-299">The arguments are separated by commas.</span></span> <span data-ttu-id="e8edd-300">각 인수의 인코딩은 같습니다 CLI 서명을 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-300">The encoding of each argument is the same as a CLI signature, as follows:</span></span>
   *  <span data-ttu-id="e8edd-301">인수는 다음과 같이 수정 해당 정규화 된 이름을 기반으로 하는 설명서 이름별으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-301">Arguments are represented by their documentation name, which is based on their fully qualified name, modified as follows:</span></span>
      * <span data-ttu-id="e8edd-302">제네릭 형식을 나타내는 인수를 추가 했습니다. "'" 문자 다음에 형식 매개 변수 수</span><span class="sxs-lookup"><span data-stu-id="e8edd-302">Arguments that represent generic types have an appended "'" character followed by the number of type parameters</span></span>
      * <span data-ttu-id="e8edd-303">인수가 필요 합니다 `out` 또는 `ref` 한정자가는 `@` 해당 형식 이름 다음입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-303">Arguments having the `out` or `ref` modifier have an `@` following their type name.</span></span> <span data-ttu-id="e8edd-304">인수를 통해 또는 값으로 전달 `params` 없는 특수 표기법을 했습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-304">Arguments passed by value or via `params` have no special notation.</span></span>
      * <span data-ttu-id="e8edd-305">인수 배열에는 표현 `[lowerbound:size, ... , lowerbound:size]` 여기서 쉼표 수는 한, 순위 및 하한값 및 각 차원 크기를 확인 하는 경우 10 진수로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-305">Arguments that are arrays are represented as `[lowerbound:size, ... , lowerbound:size]` where the number of commas is the rank less one, and the lower bounds and size of each dimension, if known, are represented in decimal.</span></span> <span data-ttu-id="e8edd-306">하한값 또는 크기를 지정 하지 않으면 하는 경우 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-306">If a lower bound or size is not specified, it is omitted.</span></span> <span data-ttu-id="e8edd-307">하한값과 특정 차원에 대 한 크기를 생략 하면는 "`:`"도 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-307">If the lower bound and size for a particular dimension are omitted, the "`:`" is omitted as well.</span></span> <span data-ttu-id="e8edd-308">가변된 배열 하나로 표시 됩니다 "`[]`" 별 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-308">Jagged arrays are represented by one "`[]`" per level.</span></span>
      * <span data-ttu-id="e8edd-309">Void 이외의 포인터 형식을 포함 하는 인수를 사용 하 여 표시 됩니다는 `*` 형식 이름 다음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-309">Arguments that have pointer types other than void are represented using a `*` following the type name.</span></span> <span data-ttu-id="e8edd-310">Void 포인터의 형식 이름을 사용 하 여 표현 됩니다 `System.Void`합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-310">A void pointer is represented using a type name of `System.Void`.</span></span>
      * <span data-ttu-id="e8edd-311">형식에 정의 된 제네릭 형식 매개 변수를 참조 하는 인수를 사용 하 여 인코딩됩니다는 "'" 형식 매개 변수의 0부터 시작 인덱스 뒤에 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-311">Arguments that refer to generic type parameters defined on types are encoded using the "\`" character followed by the zero-based index of the type parameter.</span></span>
      * <span data-ttu-id="e8edd-312">이중-억음 악센트 기호를 사용 하는 메서드에 정의 된 제네릭 형식 매개 변수를 사용 하는 인수 "\`\`" 대신는 "\`" 형식에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-312">Arguments that use generic type parameters defined in methods use a double-backtick "\`\`" instead of the "\`" used for types.</span></span>
      * <span data-ttu-id="e8edd-313">생성 된 제네릭 형식이 참조 하는 인수 뒤에 제네릭 형식인을 사용 하 여 인코딩됩니다. "{0}" 뒤에 형식 인수는 쉼표로 구분 된 목록, 뒤에 "}".</span><span class="sxs-lookup"><span data-stu-id="e8edd-313">Arguments that refer to constructed generic types are encoded using the generic type, followed by "{", followed by a comma-separated list of type arguments, followed by "}".</span></span>

### <a name="id-string-examples"></a><span data-ttu-id="e8edd-314">ID 문자열의 예</span><span class="sxs-lookup"><span data-stu-id="e8edd-314">ID string examples</span></span>

<span data-ttu-id="e8edd-315">다음 예제에서는 각각 C# 코드를 함께 포함할 수 있는 문서 주석이 각 소스 요소에서 생성 된 ID 문자열의 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-315">The following examples each show a fragment of C# code, along with the ID string produced from each source element capable of having a documentation comment:</span></span>

*  <span data-ttu-id="e8edd-316">형식은 일반 정보를 사용 하 여 보강 된 해당 정규화 된 이름을 사용 하 여 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-316">Types are represented using their fully qualified name, augmented with generic information:</span></span>

   ```csharp
   enum Color { Red, Blue, Green }

   namespace Acme
   {
       interface IProcess {...}

       struct ValueType {...}

       class Widget: IProcess
       {
           public class NestedClass {...}
           public interface IMenuItem {...}
           public delegate void Del(int i);
           public enum Direction { North, South, East, West }
       }

       class MyList<T>
       {
           class Helper<U,V> {...}
       }
   }

   "T:Color"
   "T:Acme.IProcess"
   "T:Acme.ValueType"
   "T:Acme.Widget"
   "T:Acme.Widget.NestedClass"
   "T:Acme.Widget.IMenuItem"
   "T:Acme.Widget.Del"
   "T:Acme.Widget.Direction"
   "T:Acme.MyList`1"
   "T:Acme.MyList`1.Helper`2"
   ```

*  <span data-ttu-id="e8edd-317">필드는 정규화 된 이름으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-317">Fields are represented by their fully qualified name:</span></span>

   ```csharp
   namespace Acme
   {
       struct ValueType
       {
           private int total;
       }
   
       class Widget: IProcess
       {
           public class NestedClass
           {
               private int value;
           }
   
           private string message;
           private static Color defaultColor;
           private const double PI = 3.14159;
           protected readonly double monthlyAverage;
           private long[] array1;
           private Widget[,] array2;
           private unsafe int *pCount;
           private unsafe float **ppValues;
       }
   }

   "F:Acme.ValueType.total"
   "F:Acme.Widget.NestedClass.value"
   "F:Acme.Widget.message"
   "F:Acme.Widget.defaultColor"
   "F:Acme.Widget.PI"
   "F:Acme.Widget.monthlyAverage"
   "F:Acme.Widget.array1"
   "F:Acme.Widget.array2"
   "F:Acme.Widget.pCount"
   "F:Acme.Widget.ppValues"
   ```

*  <span data-ttu-id="e8edd-318">생성자.</span><span class="sxs-lookup"><span data-stu-id="e8edd-318">Constructors.</span></span>

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           static Widget() {...}
           public Widget() {...}
           public Widget(string s) {...}
       }
   }

   "M:Acme.Widget.#cctor"
   "M:Acme.Widget.#ctor"
   "M:Acme.Widget.#ctor(System.String)"
   ```

*  <span data-ttu-id="e8edd-319">소멸자입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-319">Destructors.</span></span>

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           ~Widget() {...}
       }
   }
   
   "M:Acme.Widget.Finalize"
   ```

*  <span data-ttu-id="e8edd-320">메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-320">Methods.</span></span>

   ```csharp
   namespace Acme
   {
       struct ValueType
       {
           public void M(int i) {...}
       }

       class Widget: IProcess
       {
           public class NestedClass
           {
               public void M(int i) {...}
           }

           public static void M0() {...}
           public void M1(char c, out float f, ref ValueType v) {...}
           public void M2(short[] x1, int[,] x2, long[][] x3) {...}
           public void M3(long[][] x3, Widget[][,,] x4) {...}
           public unsafe void M4(char *pc, Color **pf) {...}
           public unsafe void M5(void *pv, double *[][,] pd) {...}
           public void M6(int i, params object[] args) {...}
       }

       class MyList<T>
       {
           public void Test(T t) { }
       }

       class UseList
       {
           public void Process(MyList<int> list) { }
           public MyList<T> GetValues<T>(T inputValue) { return null; }
       }
   }

   "M:Acme.ValueType.M(System.Int32)"
   "M:Acme.Widget.NestedClass.M(System.Int32)"
   "M:Acme.Widget.M0"
   "M:Acme.Widget.M1(System.Char,System.Single@,Acme.ValueType@)"
   "M:Acme.Widget.M2(System.Int16[],System.Int32[0:,0:],System.Int64[][])"
   "M:Acme.Widget.M3(System.Int64[][],Acme.Widget[0:,0:,0:][])"
   "M:Acme.Widget.M4(System.Char*,Color**)"
   "M:Acme.Widget.M5(System.Void*,System.Double*[0:,0:][])"
   "M:Acme.Widget.M6(System.Int32,System.Object[])"
   "M:Acme.MyList`1.Test(`0)"
   "M:Acme.UseList.Process(Acme.MyList{System.Int32})"
   "M:Acme.UseList.GetValues``(``0)"
   ```

*  <span data-ttu-id="e8edd-321">속성 및 인덱서를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-321">Properties and indexers.</span></span>

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public int Width { get {...} set {...} }
           public int this[int i] { get {...} set {...} }
           public int this[string s, int i] { get {...} set {...} }
       }
   }

   "P:Acme.Widget.Width"
   "P:Acme.Widget.Item(System.Int32)"
   "P:Acme.Widget.Item(System.String,System.Int32)"
   ```

*  <span data-ttu-id="e8edd-322">이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-322">Events.</span></span>

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public event Del AnEvent;
       }
   }

   "E:Acme.Widget.AnEvent"
   ```

*  <span data-ttu-id="e8edd-323">단항 연산자.</span><span class="sxs-lookup"><span data-stu-id="e8edd-323">Unary operators.</span></span>

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public static Widget operator+(Widget x) {...}
       }
   }

   "M:Acme.Widget.op_UnaryPlus(Acme.Widget)"
   ```

   <span data-ttu-id="e8edd-324">완전 한 집합이 사용 되는 단항 연산자 함수 이름과 다음과 같습니다: `op_UnaryPlus`, `op_UnaryNegation`, `op_LogicalNot`, `op_OnesComplement`, `op_Increment`를 `op_Decrement`, `op_True`, 및 `op_False`합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-324">The complete set of unary operator function names used is as follows: `op_UnaryPlus`, `op_UnaryNegation`, `op_LogicalNot`, `op_OnesComplement`, `op_Increment`, `op_Decrement`, `op_True`, and `op_False`.</span></span>

*  <span data-ttu-id="e8edd-325">이항 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-325">Binary operators.</span></span>

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public static Widget operator+(Widget x1, Widget x2) {...}
       }
   }

   "M:Acme.Widget.op_Addition(Acme.Widget,Acme.Widget)"
   ```

   <span data-ttu-id="e8edd-326">사용 되는 이항 연산자 함수 이름과 전체 집합은 다음과 같습니다: `op_Addition`, `op_Subtraction`, `op_Multiply`, `op_Division`, `op_Modulus`를 `op_BitwiseAnd`, `op_BitwiseOr`를 `op_ExclusiveOr`, `op_LeftShift`, `op_RightShift`, `op_Equality`, `op_Inequality`, `op_LessThan`, `op_LessThanOrEqual`합니다 `op_GreaterThan`, 및 `op_GreaterThanOrEqual`합니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-326">The complete set of binary operator function names used is as follows: `op_Addition`, `op_Subtraction`, `op_Multiply`, `op_Division`, `op_Modulus`, `op_BitwiseAnd`, `op_BitwiseOr`, `op_ExclusiveOr`, `op_LeftShift`, `op_RightShift`, `op_Equality`, `op_Inequality`, `op_LessThan`, `op_LessThanOrEqual`, `op_GreaterThan`, and `op_GreaterThanOrEqual`.</span></span>

*  <span data-ttu-id="e8edd-327">변환 연산자에 후행 "`~`" 반환 형식 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8edd-327">Conversion operators have a trailing "`~`" followed by the return type.</span></span>

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public static explicit operator int(Widget x) {...}
           public static implicit operator long(Widget x) {...}
       }
   }

   "M:Acme.Widget.op_Explicit(Acme.Widget)~System.Int32"
   "M:Acme.Widget.op_Implicit(Acme.Widget)~System.Int64"
   ```

## <a name="an-example"></a><span data-ttu-id="e8edd-328">예제</span><span class="sxs-lookup"><span data-stu-id="e8edd-328">An example</span></span>

### <a name="c-source-code"></a><span data-ttu-id="e8edd-329">C# 소스 코드</span><span class="sxs-lookup"><span data-stu-id="e8edd-329">C# source code</span></span>

<span data-ttu-id="e8edd-330">다음 예제에서는의 소스 코드는 `Point` 클래스:</span><span class="sxs-lookup"><span data-stu-id="e8edd-330">The following example shows the source code of a `Point` class:</span></span>

```csharp
namespace Graphics
{

/// <summary>Class <c>Point</c> models a point in a two-dimensional plane.
/// </summary>
public class Point 
{

    /// <summary>Instance variable <c>x</c> represents the point's
    ///    x-coordinate.</summary>
    private int x;

    /// <summary>Instance variable <c>y</c> represents the point's
    ///    y-coordinate.</summary>
    private int y;

    /// <value>Property <c>X</c> represents the point's x-coordinate.</value>
    public int X
    {
        get { return x; }
        set { x = value; }
    }

    /// <value>Property <c>Y</c> represents the point's y-coordinate.</value>
    public int Y
    {
        get { return y; }
        set { y = value; }
    }

    /// <summary>This constructor initializes the new Point to
    ///    (0,0).</summary>
    public Point() : this(0,0) {}

    /// <summary>This constructor initializes the new Point to
    ///    (<paramref name="xor"/>,<paramref name="yor"/>).</summary>
    /// <param><c>xor</c> is the new Point's x-coordinate.</param>
    /// <param><c>yor</c> is the new Point's y-coordinate.</param>
    public Point(int xor, int yor) {
        X = xor;
        Y = yor;
    }

    /// <summary>This method changes the point's location to
    ///    the given coordinates.</summary>
    /// <param><c>xor</c> is the new x-coordinate.</param>
    /// <param><c>yor</c> is the new y-coordinate.</param>
    /// <see cref="Translate"/>
    public void Move(int xor, int yor) {
        X = xor;
        Y = yor;
    }

    /// <summary>This method changes the point's location by
    ///    the given x- and y-offsets.
    /// <example>For example:
    /// <code>
    ///    Point p = new Point(3,5);
    ///    p.Translate(-1,3);
    /// </code>
    /// results in <c>p</c>'s having the value (2,8).
    /// </example>
    /// </summary>
    /// <param><c>xor</c> is the relative x-offset.</param>
    /// <param><c>yor</c> is the relative y-offset.</param>
    /// <see cref="Move"/>
    public void Translate(int xor, int yor) {
        X += xor;
        Y += yor;
    }

    /// <summary>This method determines whether two Points have the same
    ///    location.</summary>
    /// <param><c>o</c> is the object to be compared to the current object.
    /// </param>
    /// <returns>True if the Points have the same location and they have
    ///    the exact same type; otherwise, false.</returns>
    /// <seealso cref="operator=="/>
    /// <seealso cref="operator!="/>
    public override bool Equals(object o) {
        if (o == null) {
            return false;
        }

        if (this == o) {
            return true;
        }

        if (GetType() == o.GetType()) {
            Point p = (Point)o;
            return (X == p.X) && (Y == p.Y);
        }
        return false;
    }

    /// <summary>Report a point's location as a string.</summary>
    /// <returns>A string representing a point's location, in the form (x,y),
    ///    without any leading, training, or embedded whitespace.</returns>
    public override string ToString() {
        return "(" + X + "," + Y + ")";
    }

    /// <summary>This operator determines whether two Points have the same
    ///    location.</summary>
    /// <param><c>p1</c> is the first Point to be compared.</param>
    /// <param><c>p2</c> is the second Point to be compared.</param>
    /// <returns>True if the Points have the same location and they have
    ///    the exact same type; otherwise, false.</returns>
    /// <seealso cref="Equals"/>
    /// <seealso cref="operator!="/>
    public static bool operator==(Point p1, Point p2) {
        if ((object)p1 == null || (object)p2 == null) {
            return false;
        }

        if (p1.GetType() == p2.GetType()) {
            return (p1.X == p2.X) && (p1.Y == p2.Y);
        }

        return false;
    }

    /// <summary>This operator determines whether two Points have the same
    ///    location.</summary>
    /// <param><c>p1</c> is the first Point to be compared.</param>
    /// <param><c>p2</c> is the second Point to be compared.</param>
    /// <returns>True if the Points do not have the same location and the
    ///    exact same type; otherwise, false.</returns>
    /// <seealso cref="Equals"/>
    /// <seealso cref="operator=="/>
    public static bool operator!=(Point p1, Point p2) {
        return !(p1 == p2);
    }

    /// <summary>This is the entry point of the Point class testing
    /// program.
    /// <para>This program tests each method and operator, and
    /// is intended to be run after any non-trivial maintenance has
    /// been performed on the Point class.</para></summary>
    public static void Main() {
        // class test code goes here
    }
}
}
```

### <a name="resulting-xml"></a><span data-ttu-id="e8edd-331">결과 XML</span><span class="sxs-lookup"><span data-stu-id="e8edd-331">Resulting XML</span></span>

<span data-ttu-id="e8edd-332">다음은 클래스에 대 한 소스 코드를 지정 하는 경우 하나의 설명서 생성기에서 생성 된 출력 `Point`위에 표시 된:</span><span class="sxs-lookup"><span data-stu-id="e8edd-332">Here is the output produced by one documentation generator when given the source code for class `Point`, shown above:</span></span>

```xml
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>Point</name>
    </assembly>
    <members>
        <member name="T:Graphics.Point">
            <summary>Class <c>Point</c> models a point in a two-dimensional
            plane.
            </summary>
        </member>

        <member name="F:Graphics.Point.x">
            <summary>Instance variable <c>x</c> represents the point's
            x-coordinate.</summary>
        </member>

        <member name="F:Graphics.Point.y">
            <summary>Instance variable <c>y</c> represents the point's
            y-coordinate.</summary>
        </member>

        <member name="M:Graphics.Point.#ctor">
            <summary>This constructor initializes the new Point to
        (0,0).</summary>
        </member>

        <member name="M:Graphics.Point.#ctor(System.Int32,System.Int32)">
            <summary>This constructor initializes the new Point to
            (<paramref name="xor"/>,<paramref name="yor"/>).</summary>
            <param><c>xor</c> is the new Point's x-coordinate.</param>
            <param><c>yor</c> is the new Point's y-coordinate.</param>
        </member>

        <member name="M:Graphics.Point.Move(System.Int32,System.Int32)">
            <summary>This method changes the point's location to
            the given coordinates.</summary>
            <param><c>xor</c> is the new x-coordinate.</param>
            <param><c>yor</c> is the new y-coordinate.</param>
            <see cref="M:Graphics.Point.Translate(System.Int32,System.Int32)"/>
        </member>

        <member
            name="M:Graphics.Point.Translate(System.Int32,System.Int32)">
            <summary>This method changes the point's location by
            the given x- and y-offsets.
            <example>For example:
            <code>
            Point p = new Point(3,5);
            p.Translate(-1,3);
            </code>
            results in <c>p</c>'s having the value (2,8).
            </example>
            </summary>
            <param><c>xor</c> is the relative x-offset.</param>
            <param><c>yor</c> is the relative y-offset.</param>
            <see cref="M:Graphics.Point.Move(System.Int32,System.Int32)"/>
        </member>

        <member name="M:Graphics.Point.Equals(System.Object)">
            <summary>This method determines whether two Points have the same
            location.</summary>
            <param><c>o</c> is the object to be compared to the current
            object.
            </param>
            <returns>True if the Points have the same location and they have
            the exact same type; otherwise, false.</returns>
            <seealso
      cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
            <seealso
      cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
        </member>

        <member name="M:Graphics.Point.ToString">
            <summary>Report a point's location as a string.</summary>
            <returns>A string representing a point's location, in the form
            (x,y),
            without any leading, training, or embedded whitespace.</returns>
        </member>

        <member
       name="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)">
            <summary>This operator determines whether two Points have the
            same
            location.</summary>
            <param><c>p1</c> is the first Point to be compared.</param>
            <param><c>p2</c> is the second Point to be compared.</param>
            <returns>True if the Points have the same location and they have
            the exact same type; otherwise, false.</returns>
            <seealso cref="M:Graphics.Point.Equals(System.Object)"/>
            <seealso
     cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
        </member>

        <member
      name="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)">
            <summary>This operator determines whether two Points have the
            same
            location.</summary>
            <param><c>p1</c> is the first Point to be compared.</param>
            <param><c>p2</c> is the second Point to be compared.</param>
            <returns>True if the Points do not have the same location and
            the
            exact same type; otherwise, false.</returns>
            <seealso cref="M:Graphics.Point.Equals(System.Object)"/>
            <seealso
      cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
        </member>

        <member name="M:Graphics.Point.Main">
            <summary>This is the entry point of the Point class testing
            program.
            <para>This program tests each method and operator, and
            is intended to be run after any non-trivial maintenance has
            been performed on the Point class.</para></summary>
        </member>

        <member name="P:Graphics.Point.X">
            <value>Property <c>X</c> represents the point's
            x-coordinate.</value>
        </member>

        <member name="P:Graphics.Point.Y">
            <value>Property <c>Y</c> represents the point's
            y-coordinate.</value>
        </member>
    </members>
</doc>
```
