# <a name="arrays"></a><span data-ttu-id="4e266-101">배열</span><span class="sxs-lookup"><span data-stu-id="4e266-101">Arrays</span></span>

<span data-ttu-id="4e266-102">배열에는 여러 가지 계산 된 인덱스를 통해 액세스할 수 있는 변수를 포함 하는 데이터 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-102">An array is a data structure that contains a number of variables which are accessed through computed indices.</span></span> <span data-ttu-id="4e266-103">배열의 요소를 배열에 포함 된 변수는 동일한 형식의 모든 및이 형식을 배열의 요소 형식 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-103">The variables contained in an array, also called the elements of the array, are all of the same type, and this type is called the element type of the array.</span></span>

<span data-ttu-id="4e266-104">배열 차수가 각 배열 요소와 연결 된 인덱스의 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-104">An array has a rank which determines the number of indices associated with each array element.</span></span> <span data-ttu-id="4e266-105">배열의 차수는 배열의 차수 라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-105">The rank of an array is also referred to as the dimensions of the array.</span></span> <span data-ttu-id="4e266-106">배열 차수 1을 사용 하 여 호출 되는 ***1 차원 배열***합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-106">An array with a rank of one is called a ***single-dimensional array***.</span></span> <span data-ttu-id="4e266-107">하나를 호출 하는 보다 큰 차수의 배열을 ***다차원 배열***합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-107">An array with a rank greater than one is called a ***multi-dimensional array***.</span></span> <span data-ttu-id="4e266-108">특정 크기의 다차원 배열은 2 차원 배열, 3 차원 배열 및 등이 라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-108">Specific sized multi-dimensional arrays are often referred to as two-dimensional arrays, three-dimensional arrays, and so on.</span></span>

<span data-ttu-id="4e266-109">배열의 각 차원에 연결 된 길이가 정수 계열 숫자 보다 크거나 0입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-109">Each dimension of an array has an associated length which is an integral number greater than or equal to zero.</span></span> <span data-ttu-id="4e266-110">차원 길이 배열 형식에 속하지 않는 하지만 런타임 시 배열 형식의 인스턴스가 만들어질 때 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-110">The dimension lengths are not part of the type of the array, but rather are established when an instance of the array type is created at run-time.</span></span> <span data-ttu-id="4e266-111">해당 차원에 대 한 인덱스의 유효한 범위를 결정 하는 차원의 길이: 길이의 차원에 대 한 `N`, 인덱스에서 까지입니다 `0` 에 `N - 1` 포괄 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-111">The length of a dimension determines the valid range of indices for that dimension: For a dimension of length `N`, indices can range from `0` to `N - 1` inclusive.</span></span> <span data-ttu-id="4e266-112">배열에 있는 요소의 총 수는 배열의 각 차원 길이 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-112">The total number of elements in an array is the product of the lengths of each dimension in the array.</span></span> <span data-ttu-id="4e266-113">배열의 차원 중 하나 이상이 0 길이의 경우 비워 배열 이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-113">If one or more of the dimensions of an array have a length of zero, the array is said to be empty.</span></span>

<span data-ttu-id="4e266-114">배열의 요소 형식은 배열 형식을 비롯한 어떤 형식도 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-114">The element type of an array can be any type, including an array type.</span></span>

## <a name="array-types"></a><span data-ttu-id="4e266-115">배열 형식</span><span class="sxs-lookup"><span data-stu-id="4e266-115">Array types</span></span>

<span data-ttu-id="4e266-116">배열 형식으로 기록 되는 *non_array_type* 뒤에 하나 이상의 *rank_specifier*s:</span><span class="sxs-lookup"><span data-stu-id="4e266-116">An array type is written as a *non_array_type* followed by one or more *rank_specifier*s:</span></span>

```antlr
array_type
    : non_array_type rank_specifier+
    ;

non_array_type
    : type
    ;

rank_specifier
    : '[' dim_separator* ']'
    ;

dim_separator
    : ','
    ;
```

<span data-ttu-id="4e266-117">A *non_array_type* 중인 *유형* 즉 자체는 *array_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-117">A *non_array_type* is any *type* that is not itself an *array_type*.</span></span>

<span data-ttu-id="4e266-118">배열 형식의 차수를 지정 하 여 가장 왼쪽에 있는 *rank_specifier* 에 *array_type*: A *rank_specifier* 배열 차수 1을 사용 하 여 배열 임을 나타냅니다와 숫자 "`,`" 토큰이 합니다 *rank_specifier*합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-118">The rank of an array type is given by the leftmost *rank_specifier* in the *array_type*: A *rank_specifier* indicates that the array is an array with a rank of one plus the number of "`,`" tokens in the *rank_specifier*.</span></span>

<span data-ttu-id="4e266-119">배열 형식의 요소 형식은 형식에서 가장 왼쪽에 있는 삭제를 일으키는 *rank_specifier*:</span><span class="sxs-lookup"><span data-stu-id="4e266-119">The element type of an array type is the type that results from deleting the leftmost *rank_specifier*:</span></span>

*  <span data-ttu-id="4e266-120">형식의 배열 형식 `T[R]` rank 통한 배열이 `R` 비 배열 요소 형식 및 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-120">An array type of the form `T[R]` is an array with rank `R` and a non-array element type `T`.</span></span>
*  <span data-ttu-id="4e266-121">형식의 배열 형식 `T[R][R1]...[Rn]` rank 통한 배열이 `R` 이 고 요소 형식이 `T[R1]...[Rn]`합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-121">An array type of the form `T[R][R1]...[Rn]` is an array with rank `R` and an element type `T[R1]...[Rn]`.</span></span>

<span data-ttu-id="4e266-122">실제로 *rank_specifier*의바로 최종 비 배열 요소 형식 앞에 왼쪽에서 읽힙니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-122">In effect, the *rank_specifier*s are read from left to right before the final non-array element type.</span></span> <span data-ttu-id="4e266-123">형식 `int[][,,][,]` 의 2 차원 배열의 3 차원 배열의 1 차원 배열이 `int`합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-123">The type `int[][,,][,]` is a single-dimensional array of three-dimensional arrays of two-dimensional arrays of `int`.</span></span>

<span data-ttu-id="4e266-124">배열 형식의 값은 런타임 시 수 `null` 또는 배열 형식의 인스턴스에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-124">At run-time, a value of an array type can be `null` or a reference to an instance of that array type.</span></span>

### <a name="the-systemarray-type"></a><span data-ttu-id="4e266-125">System.Array 형식</span><span class="sxs-lookup"><span data-stu-id="4e266-125">The System.Array type</span></span>

<span data-ttu-id="4e266-126">형식 `System.Array` 모든 배열 형식의 추상 기본 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-126">The type `System.Array` is the abstract base type of all array types.</span></span> <span data-ttu-id="4e266-127">암시적 참조 변환 ([암시적 참조 변환](conversions.md#implicit-reference-conversions)) 모든 배열 형식에서 존재 `System.Array`, 및 명시적 참조 변환이 ([명시적 참조 변환을](conversions.md#explicit-reference-conversions)) 있습니다. `System.Array` 모든 배열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-127">An implicit reference conversion ([Implicit reference conversions](conversions.md#implicit-reference-conversions)) exists from any array type to `System.Array`, and an explicit reference conversion ([Explicit reference conversions](conversions.md#explicit-reference-conversions)) exists from `System.Array` to any array type.</span></span> <span data-ttu-id="4e266-128">사실은 `System.Array` 자체는 *array_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-128">Note that `System.Array` is not itself an *array_type*.</span></span> <span data-ttu-id="4e266-129">아니라는 것을 *class_type* 모든에서 *array_type*가 파생 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-129">Rather, it is a *class_type* from which all *array_type*s are derived.</span></span>

<span data-ttu-id="4e266-130">런타임 형식의 값에 `System.Array` 수 `null` 또는 배열 형식의 모든 인스턴스에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-130">At run-time, a value of type `System.Array` can be `null` or a reference to an instance of any array type.</span></span>

### <a name="arrays-and-the-generic-ilist-interface"></a><span data-ttu-id="4e266-131">배열 및 제네릭 IList 인터페이스</span><span class="sxs-lookup"><span data-stu-id="4e266-131">Arrays and the generic IList interface</span></span>

<span data-ttu-id="4e266-132">1 차원 배열 `T[]` 인터페이스를 구현 `System.Collections.Generic.IList<T>` (`IList<T>` 줄여서)와 해당 기본 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-132">A one-dimensional array `T[]` implements the interface `System.Collections.Generic.IList<T>` (`IList<T>` for short) and its base interfaces.</span></span> <span data-ttu-id="4e266-133">따라서 암시적 변환이 있기 `T[]` 에 `IList<T>` 와 해당 기본 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-133">Accordingly, there is an implicit conversion from `T[]` to `IList<T>` and its base interfaces.</span></span> <span data-ttu-id="4e266-134">또한에서 암시적 참조 변환이 없는 경우 `S` 에 `T` 한 다음 `S[]` 구현 `IList<T>` 에서 암시적 참조 변환 되며 `S[]` 를 `IList<T>` 및 기본 인터페이스 ( [암시적 참조 변환](conversions.md#implicit-reference-conversions)).</span><span class="sxs-lookup"><span data-stu-id="4e266-134">In addition, if there is an implicit reference conversion from `S` to `T` then `S[]` implements `IList<T>` and there is an implicit reference conversion from `S[]` to `IList<T>` and its base interfaces ([Implicit reference conversions](conversions.md#implicit-reference-conversions)).</span></span> <span data-ttu-id="4e266-135">명시적 참조 변환이 없는 경우 `S` 하 `T` 에서 명시적 참조 변환이 됩니다 `S[]` 하 `IList<T>` 와 해당 기본 인터페이스 ([명시적 참조 변환을](conversions.md#explicit-reference-conversions)).</span><span class="sxs-lookup"><span data-stu-id="4e266-135">If there is an explicit reference conversion from `S` to `T` then there is an explicit reference conversion from `S[]` to `IList<T>` and its base interfaces ([Explicit reference conversions](conversions.md#explicit-reference-conversions)).</span></span> <span data-ttu-id="4e266-136">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="4e266-136">For example:</span></span>
```csharp
using System.Collections.Generic;

class Test
{
    static void Main() {
        string[] sa = new string[5];
        object[] oa1 = new object[5];
        object[] oa2 = sa;

        IList<string> lst1 = sa;                    // Ok
        IList<string> lst2 = oa1;                   // Error, cast needed
        IList<object> lst3 = sa;                    // Ok
        IList<object> lst4 = oa1;                   // Ok

        IList<string> lst5 = (IList<string>)oa1;    // Exception
        IList<string> lst6 = (IList<string>)oa2;    // Ok
    }
}
```

<span data-ttu-id="4e266-137">할당 `lst2 = oa1` 변환 이후 컴파일 타임 오류가 `object[]` 에 `IList<string>` 없습니다 암시적 명시적 변환이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-137">The assignment `lst2 = oa1` generates a compile-time error since the conversion from `object[]` to `IList<string>` is an explicit conversion, not implicit.</span></span> <span data-ttu-id="4e266-138">캐스팅 `(IList<string>)oa1` 이후 실행 시 throw 하면 예외가 발생 합니다 `oa1` 참조는 `object[]` 아니라는 `string[]`합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-138">The cast `(IList<string>)oa1` will cause an exception to be thrown at run-time since `oa1` references an `object[]` and not a `string[]`.</span></span> <span data-ttu-id="4e266-139">그러나 캐스팅 `(IList<string>)oa2` 이후 throw 예외가 발생 하지 것입니다 `oa2` 참조는 `string[]`합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-139">However the cast `(IList<string>)oa2` will not cause an exception to be thrown since `oa2` references a `string[]`.</span></span>

<span data-ttu-id="4e266-140">때마다는 암시적 또는 명시적 참조에서 변환이 `S[]` 하 `IList<T>`에서 명시적 참조 변환이 이기도 `IList<T>` 기본 인터페이스 및 `S[]` ([명시적 참조 변환](conversions.md#explicit-reference-conversions)).</span><span class="sxs-lookup"><span data-stu-id="4e266-140">Whenever there is an implicit or explicit reference conversion from `S[]` to `IList<T>`, there is also an explicit reference conversion from `IList<T>` and its base interfaces to `S[]` ([Explicit reference conversions](conversions.md#explicit-reference-conversions)).</span></span>

<span data-ttu-id="4e266-141">때 배열 형식 `S[]` 구현 `IList<T>`에 구현된 된 인터페이스 멤버의 일부 예외를 throw 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-141">When an array type `S[]` implements `IList<T>`, some of the members of the implemented interface may throw exceptions.</span></span> <span data-ttu-id="4e266-142">인터페이스의 구현 하는 정확한 동작을이 사양의 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-142">The precise behavior of the implementation of the interface is beyond the scope of this specification.</span></span>

## <a name="array-creation"></a><span data-ttu-id="4e266-143">배열 만들기</span><span class="sxs-lookup"><span data-stu-id="4e266-143">Array creation</span></span>

<span data-ttu-id="4e266-144">배열 인스턴스에 의해 만들어집니다 *array_creation_expression*s ([배열 만들기 식을](expressions.md#array-creation-expressions)) 또는 필드 또는 지역 변수 선언을 포함 하는 *array_initializer*([배열 이니셜라이저](arrays.md#array-initializers)).</span><span class="sxs-lookup"><span data-stu-id="4e266-144">Array instances are created by *array_creation_expression*s ([Array creation expressions](expressions.md#array-creation-expressions)) or by field or local variable declarations that include an *array_initializer* ([Array initializers](arrays.md#array-initializers)).</span></span>

<span data-ttu-id="4e266-145">배열 인스턴스를 만들 때 순위와 각 차원의 길이 설정 및 인스턴스 전체 수명 동안 그대로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-145">When an array instance is created, the rank and length of each dimension are established and then remain constant for the entire lifetime of the instance.</span></span> <span data-ttu-id="4e266-146">즉, 기존 배열 인스턴스, 차수를 변경할 수 없는 아니고 차원 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-146">In other words, it is not possible to change the rank of an existing array instance, nor is it possible to resize its dimensions.</span></span>

<span data-ttu-id="4e266-147">배열 인스턴스는 항상 배열 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-147">An array instance is always of an array type.</span></span> <span data-ttu-id="4e266-148">`System.Array` 형식은 인스턴스화할 수 없는 추상 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-148">The `System.Array` type is an abstract type that cannot be instantiated.</span></span>

<span data-ttu-id="4e266-149">만든 배열의 요소 *array_creation_expression*s 항상 기본값으로 초기화 됩니다 ([기본값](variables.md#default-values)).</span><span class="sxs-lookup"><span data-stu-id="4e266-149">Elements of arrays created by *array_creation_expression*s are always initialized to their default value ([Default values](variables.md#default-values)).</span></span>

## <a name="array-element-access"></a><span data-ttu-id="4e266-150">배열 요소 액세스</span><span class="sxs-lookup"><span data-stu-id="4e266-150">Array element access</span></span>

<span data-ttu-id="4e266-151">배열 요소를 사용 하 여 액세스 하 *element_access* 식 ([배열 액세스](expressions.md#array-access)) 형식의 `A[I1, I2, ..., In]`여기서 `A` 배열 형식 및 각 식 `Ix` 되는 형식의 식입니다 `int`, `uint`를 `long`, `ulong`, 또는 이러한 형식 중 하나 이상에 암시적으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-151">Array elements are accessed using *element_access* expressions ([Array access](expressions.md#array-access)) of the form `A[I1, I2, ..., In]`, where `A` is an expression of an array type and each `Ix` is an expression of type `int`, `uint`, `long`, `ulong`, or can be implicitly converted to one or more of these types.</span></span> <span data-ttu-id="4e266-152">배열 요소 액세스의 결과 변수, 즉 인덱스에서 선택한 배열 요소.</span><span class="sxs-lookup"><span data-stu-id="4e266-152">The result of an array element access is a variable, namely the array element selected by the indices.</span></span>

<span data-ttu-id="4e266-153">사용 하 여 배열의 요소를 열거할 수는 `foreach` 문 ([foreach 문을](statements.md#the-foreach-statement)).</span><span class="sxs-lookup"><span data-stu-id="4e266-153">The elements of an array can be enumerated using a `foreach` statement ([The foreach statement](statements.md#the-foreach-statement)).</span></span>

## <a name="array-members"></a><span data-ttu-id="4e266-154">배열 멤버</span><span class="sxs-lookup"><span data-stu-id="4e266-154">Array members</span></span>

<span data-ttu-id="4e266-155">모든 배열 형식에서 선언 된 멤버를 상속 된 `System.Array` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-155">Every array type inherits the members declared by the `System.Array` type.</span></span>

## <a name="array-covariance"></a><span data-ttu-id="4e266-156">배열 공변성 (covariance)</span><span class="sxs-lookup"><span data-stu-id="4e266-156">Array covariance</span></span>

<span data-ttu-id="4e266-157">두에 대 한 *reference_type*s `A` 하 고 `B`하는 경우 암시적 참조 변환, ([암시적 참조 변환](conversions.md#implicit-reference-conversions)) 나 명시적 참조 변환을 ([ 명시적 참조 변환을](conversions.md#explicit-reference-conversions))에서 존재 `A` 하 `B`, 배열 형식에서 동일한 참조 변환도 존재 합니다 `A[R]` 배열 형식으로 `B[R]`여기서 `R` 중인 지정 된 *rank_specifier* (하지만 둘 다에 대해 동일한 배열 형식).</span><span class="sxs-lookup"><span data-stu-id="4e266-157">For any two *reference_type*s `A` and `B`, if an implicit reference conversion ([Implicit reference conversions](conversions.md#implicit-reference-conversions)) or explicit reference conversion ([Explicit reference conversions](conversions.md#explicit-reference-conversions)) exists from `A` to `B`, then the same reference conversion also exists from the array type `A[R]` to the array type `B[R]`, where `R` is any given *rank_specifier* (but the same for both array types).</span></span> <span data-ttu-id="4e266-158">이 관계 라고 ***배열 공변성 (covariance)*** 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-158">This relationship is known as ***array covariance***.</span></span> <span data-ttu-id="4e266-159">배열 공변성 (covariance) 특히 의미 하는 배열 형식의 값 `A[R]` 배열 형식의 인스턴스에 대 한 참조는 실제로 있을 `B[R]`경우에서 암시적 참조 변환이 존재 `B` 하려면 `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-159">Array covariance in particular means that a value of an array type `A[R]` may actually be a reference to an instance of an array type `B[R]`, provided an implicit reference conversion exists from `B` to `A`.</span></span>

<span data-ttu-id="4e266-160">배열 공 분산으로 인해 참조 형식 배열의 요소에 대 한 할당 배열 요소에 할당 되는 값이 허용 된 형식의 실제로 인지 확인 하는 런타임 검사를 포함 ([단순 할당](expressions.md#simple-assignment)).</span><span class="sxs-lookup"><span data-stu-id="4e266-160">Because of array covariance, assignments to elements of reference type arrays include a run-time check which ensures that the value being assigned to the array element is actually of a permitted type ([Simple assignment](expressions.md#simple-assignment)).</span></span> <span data-ttu-id="4e266-161">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="4e266-161">For example:</span></span>
```csharp
class Test
{
    static void Fill(object[] array, int index, int count, object value) {
        for (int i = index; i < index + count; i++) array[i] = value;
    }

    static void Main() {
        string[] strings = new string[100];
        Fill(strings, 0, 100, "Undefined");
        Fill(strings, 0, 10, null);
        Fill(strings, 90, 10, 0);
    }
}
```

<span data-ttu-id="4e266-162">에 대 한 할당 `array[i]` 에 `Fill` 메서드는 암시적으로 참조 하는 개체가 되도록 하는 런타임 검사를 포함 `value` 는 `null` 의실제요소형식이호환되는인스턴스또는`array`.</span><span class="sxs-lookup"><span data-stu-id="4e266-162">The assignment to `array[i]` in the `Fill` method implicitly includes a run-time check which ensures that the object referenced by `value` is either `null` or an instance that is compatible with the actual element type of `array`.</span></span> <span data-ttu-id="4e266-163">`Main`의 처음 두 호출 `Fill` 성공 하지만 세 번째 호출 하면을 `System.ArrayTypeMismatchException` 첫 번째 할당을 실행할 때 throw 될 `array[i]`합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-163">In `Main`, the first two invocations of `Fill` succeed, but the third invocation causes a `System.ArrayTypeMismatchException` to be thrown upon executing the first assignment to `array[i]`.</span></span> <span data-ttu-id="4e266-164">예외가 발생 하기 때문에 boxed `int` 에 저장할 수 없습니다는 `string` 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-164">The exception occurs because a boxed `int` cannot be stored in a `string` array.</span></span>

<span data-ttu-id="4e266-165">배열 공변성 (covariance) 특히 배열을로 확장 되지 않습니다 *value_type*s입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-165">Array covariance specifically does not extend to arrays of *value_type*s.</span></span> <span data-ttu-id="4e266-166">예를 들어, 변환할 수 없는 해당 콘텐츠는 `int[]` 로 처리할지를 `object[]`.</span><span class="sxs-lookup"><span data-stu-id="4e266-166">For example, no conversion exists that permits an `int[]` to be treated as an `object[]`.</span></span>

## <a name="array-initializers"></a><span data-ttu-id="4e266-167">배열 이니셜라이저</span><span class="sxs-lookup"><span data-stu-id="4e266-167">Array initializers</span></span>

<span data-ttu-id="4e266-168">필드 선언에서 배열 이니셜라이저를 지정할 수 있습니다 ([필드](classes.md#fields)), 지역 변수 선언 ([지역 변수 선언](statements.md#local-variable-declarations)), 및 배열 만들기 식 ([배열 만들기 식](expressions.md#array-creation-expressions)):</span><span class="sxs-lookup"><span data-stu-id="4e266-168">Array initializers may be specified in field declarations ([Fields](classes.md#fields)), local variable declarations ([Local variable declarations](statements.md#local-variable-declarations)), and array creation expressions ([Array creation expressions](expressions.md#array-creation-expressions)):</span></span>

```antlr
array_initializer
    : '{' variable_initializer_list? '}'
    | '{' variable_initializer_list ',' '}'
    ;

variable_initializer_list
    : variable_initializer (',' variable_initializer)*
    ;

variable_initializer
    : expression
    | array_initializer
    ;
```

<span data-ttu-id="4e266-169">배열 이니셜라이저를 묶어 변수 이니셜라이저의 시퀀스로 구성 됩니다. "`{`"및"`}`"토큰을 구분 하 여"`,`" 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-169">An array initializer consists of a sequence of variable initializers, enclosed by "`{`" and "`}`" tokens and separated by "`,`" tokens.</span></span> <span data-ttu-id="4e266-170">각 변수 이니셜라이저는 식 또는을 다차원 배열에 중첩 된 배열 이니셜라이저를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="4e266-170">Each variable initializer is an expression or, in the case of a multi-dimensional array, a nested array initializer.</span></span>

<span data-ttu-id="4e266-171">배열 이니셜라이저를 사용 하는 컨텍스트 초기화 되는 배열 형식을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-171">The context in which an array initializer is used determines the type of the array being initialized.</span></span> <span data-ttu-id="4e266-172">배열 만들기 식을 배열 형식이 즉시, 이니셜라이저 앞 또는 배열 이니셜라이저 식에서 유추 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-172">In an array creation expression, the array type immediately precedes the initializer, or is inferred from the expressions in the array initializer.</span></span> <span data-ttu-id="4e266-173">필드 또는 변수 선언에서 배열 유형 선언 되는 변수 또는 필드의 형식이입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-173">In a field or variable declaration, the array type is the type of the field or variable being declared.</span></span> <span data-ttu-id="4e266-174">배열 이니셜라이저를 사용 하면 필드 또는 변수 선언에 같은:</span><span class="sxs-lookup"><span data-stu-id="4e266-174">When an array initializer is used in a field or variable declaration, such as:</span></span>
```csharp
int[] a = {0, 2, 4, 6, 8};
```
<span data-ttu-id="4e266-175">해당 하는 배열 생성 식에 대 한 줄인 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-175">it is simply shorthand for an equivalent array creation expression:</span></span>
```csharp
int[] a = new int[] {0, 2, 4, 6, 8};
```

<span data-ttu-id="4e266-176">1 차원 배열에 대 한 배열 이니셜라이저 할당 배열의 요소 형식이 호환 되는 식의 시퀀스가 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-176">For a single-dimensional array, the array initializer must consist of a sequence of expressions that are assignment compatible with the element type of the array.</span></span> <span data-ttu-id="4e266-177">시작 인덱스 0에 있는 요소를 사용 하 여 오름차순으로 배열 요소를 초기화 하는 식입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-177">The expressions initialize array elements in increasing order, starting with the element at index zero.</span></span> <span data-ttu-id="4e266-178">배열 이니셜라이저 식의 수는 만들어지는 배열 인스턴스의 길이 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-178">The number of expressions in the array initializer determines the length of the array instance being created.</span></span> <span data-ttu-id="4e266-179">예를 들어, 위의 배열 이니셜라이저를 만듭니다는 `int[]` 길이가 5 인의 인스턴스를 다음 값을 사용 하 여 인스턴스를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-179">For example, the array initializer above creates an `int[]` instance of length 5 and then initializes the instance with the following values:</span></span>
```csharp
a[0] = 0; a[1] = 2; a[2] = 4; a[3] = 6; a[4] = 8;
```

<span data-ttu-id="4e266-180">다차원 배열의 배열 이니셜라이저에 중첩 된 배열의 차원 수 만큼 많은 수준의 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-180">For a multi-dimensional array, the array initializer must have as many levels of nesting as there are dimensions in the array.</span></span> <span data-ttu-id="4e266-181">가장 왼쪽의 차원에 해당 하는 가장 바깥쪽 중첩 수준 및 오른쪽에 있는 차원에 해당 하는 가장 안쪽의 중첩 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-181">The outermost nesting level corresponds to the leftmost dimension and the innermost nesting level corresponds to the rightmost dimension.</span></span> <span data-ttu-id="4e266-182">배열의 각 차원 길이 배열 이니셜라이저에 해당 하는 중첩 수준에 있는 요소 수가 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-182">The length of each dimension of the array is determined by the number of elements at the corresponding nesting level in the array initializer.</span></span> <span data-ttu-id="4e266-183">각 중첩 된 배열 이니셜라이저 요소 수가 다른 배열 이니셜라이저는 같은 수준으로 동일 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-183">For each nested array initializer, the number of elements must be the same as the other array initializers at the same level.</span></span> <span data-ttu-id="4e266-184">예제:</span><span class="sxs-lookup"><span data-stu-id="4e266-184">The example:</span></span>
```csharp
int[,] b = {{0, 1}, {2, 3}, {4, 5}, {6, 7}, {8, 9}};
```
<span data-ttu-id="4e266-185">왼쪽에 있는 차원에 대 한 5이 고 길이가 오른쪽에 있는 차원에 대 한 두 개를 사용 하 여 2 차원 배열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-185">creates a two-dimensional array with a length of five for the leftmost dimension and a length of two for the rightmost dimension:</span></span>
```csharp
int[,] b = new int[5, 2];
```
<span data-ttu-id="4e266-186">및 다음 초기화 배열은 다음 값을 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="4e266-186">and then initializes the array instance with the following values:</span></span>
```csharp
b[0, 0] = 0; b[0, 1] = 1;
b[1, 0] = 2; b[1, 1] = 3;
b[2, 0] = 4; b[2, 1] = 5;
b[3, 0] = 6; b[3, 1] = 7;
b[4, 0] = 8; b[4, 1] = 9;
```

<span data-ttu-id="4e266-187">맨 오른쪽 이외의 차원 길이가 0 인을 사용 하 여 주어진 경우 후속 크기 길이도 0으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-187">If a dimension other than the rightmost is given with length zero, the subsequent dimensions are assumed to also have length zero.</span></span> <span data-ttu-id="4e266-188">예제:</span><span class="sxs-lookup"><span data-stu-id="4e266-188">The example:</span></span>
```csharp
int[,] c = {};
```
<span data-ttu-id="4e266-189">왼쪽 및 오른쪽에 있는 차원에 대 한 0 길이의 2 차원 배열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-189">creates a two-dimensional array with a length of zero for both the leftmost and the rightmost dimension:</span></span>
```csharp
int[,] c = new int[0, 0];
```

<span data-ttu-id="4e266-190">배열 만들기 식을 배열 이니셜라이저 및 명시적 차원 길이 포함 하는 경우 길이 상수 식 이어야 합니다 하 고 각 중첩 수준에 있는 요소의 수에는 해당 차원 길이 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-190">When an array creation expression includes both explicit dimension lengths and an array initializer, the lengths must be constant expressions and the number of elements at each nesting level must match the corresponding dimension length.</span></span> <span data-ttu-id="4e266-191">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-191">Here are some examples:</span></span>
```csharp
int i = 3;
int[] x = new int[3] {0, 1, 2};        // OK
int[] y = new int[i] {0, 1, 2};        // Error, i not a constant
int[] z = new int[3] {0, 1, 2, 3};     // Error, length/initializer mismatch
```

<span data-ttu-id="4e266-192">여기에 대 한 이니셜라이저 `y` 차원 길이가 식이 상수 및 이니셜라이저가 없기 때문에 컴파일 타임 오류가 발생 `z` 때문에 컴파일 타임 오류가 발생 길이의 요소 수를 이니셜라이저 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4e266-192">Here, the initializer for `y` results in a compile-time error because the dimension length expression is not a constant, and the initializer for `z` results in a compile-time error because the length and the number of elements in the initializer do not agree.</span></span>
