# <a name="conversions"></a><span data-ttu-id="7b523-101">변환</span><span class="sxs-lookup"><span data-stu-id="7b523-101">Conversions</span></span>

<span data-ttu-id="7b523-102">A ***변환*** 식을 특정 형식으로 처리 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-102">A ***conversion*** enables an expression to be treated as being of a particular type.</span></span> <span data-ttu-id="7b523-103">변환을 다른 형식으로 처리 됨을 지정 된 형식의 식의 않을 또는 형식 유형을 알 수 없는 식 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-103">A conversion may cause an expression of a given type to be treated as having a different type, or it may cause an expression without a type to get a type.</span></span> <span data-ttu-id="7b523-104">변환 될 수 있습니다 ***암시적*** 또는 ***명시적***에 명시적 캐스트가 필요 여부를 결정 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-104">Conversions can be ***implicit*** or ***explicit***, and this determines whether an explicit cast is required.</span></span> <span data-ttu-id="7b523-105">예를 들어, 형식 변환 `int` 형식으로 `long` 암시적 따라서 식의 형식 `int` 형식으로 암시적으로 처리 될 수 있습니다 `long`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-105">For instance, the conversion from type `int` to type `long` is implicit, so expressions of type `int` can implicitly be treated as type `long`.</span></span> <span data-ttu-id="7b523-106">형식에서 변환, `long` 형식으로 `int`, 명시적 이므로 명시적 캐스트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-106">The opposite conversion, from type `long` to type `int`, is explicit and so an explicit cast is required.</span></span>

```csharp
int a = 123;
long b = a;         // implicit conversion from int to long
int c = (int) b;    // explicit conversion from long to int
```

<span data-ttu-id="7b523-107">변환 중 일부는 언어에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-107">Some conversions are defined by the language.</span></span> <span data-ttu-id="7b523-108">프로그램에 고유한 변환을 정의할 수도 있습니다 ([사용자 정의 변환은](conversions.md#user-defined-conversions)).</span><span class="sxs-lookup"><span data-stu-id="7b523-108">Programs may also define their own conversions ([User-defined conversions](conversions.md#user-defined-conversions)).</span></span>

## <a name="implicit-conversions"></a><span data-ttu-id="7b523-109">암시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-109">Implicit conversions</span></span>

<span data-ttu-id="7b523-110">다음 변환은 암시적 변환으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-110">The following conversions are classified as implicit conversions:</span></span>

*  <span data-ttu-id="7b523-111">Identity 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-111">Identity conversions</span></span>
*  <span data-ttu-id="7b523-112">암시적 숫자 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-112">Implicit numeric conversions</span></span>
*  <span data-ttu-id="7b523-113">암시적 열거형 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-113">Implicit enumeration conversions.</span></span>
*  <span data-ttu-id="7b523-114">Nullable 암시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-114">Implicit nullable conversions</span></span>
*  <span data-ttu-id="7b523-115">Null 리터럴 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-115">Null literal conversions</span></span>
*  <span data-ttu-id="7b523-116">암시적 참조 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-116">Implicit reference conversions</span></span>
*  <span data-ttu-id="7b523-117">Boxing 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-117">Boxing conversions</span></span>
*  <span data-ttu-id="7b523-118">동적 암시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-118">Implicit dynamic conversions</span></span>
*  <span data-ttu-id="7b523-119">암시적 상수 식 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-119">Implicit constant expression conversions</span></span>
*  <span data-ttu-id="7b523-120">암시적 사용자 정의 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-120">User-defined implicit conversions</span></span>
*  <span data-ttu-id="7b523-121">익명 함수 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-121">Anonymous function conversions</span></span>
*  <span data-ttu-id="7b523-122">메서드 그룹 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-122">Method group conversions</span></span>

<span data-ttu-id="7b523-123">암시적으로 다양 한 함수 멤버 호출을 포함 하 여 환경에서에서 발생할 수 있습니다 ([동적 오버 로드 확인 검사 하는 컴파일 타임](expressions.md#compile-time-checking-of-dynamic-overload-resolution)), 캐스트 식 ([캐스트 식](expressions.md#cast-expressions)), 및 할당 ([대입 연산자](expressions.md#assignment-operators)).</span><span class="sxs-lookup"><span data-stu-id="7b523-123">Implicit conversions can occur in a variety of situations, including function member invocations ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)), cast expressions ([Cast expressions](expressions.md#cast-expressions)), and assignments ([Assignment operators](expressions.md#assignment-operators)).</span></span>

<span data-ttu-id="7b523-124">미리 정의 된 암시적 변환이 항상 성공 하 고 throw 되는 예외를 일으키지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-124">The pre-defined implicit conversions always succeed and never cause exceptions to be thrown.</span></span> <span data-ttu-id="7b523-125">올바르게 설계 된 사용자 정의 된 암시적 변환도 이러한 특징을 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-125">Properly designed user-defined implicit conversions should exhibit these characteristics as well.</span></span>

<span data-ttu-id="7b523-126">형식 변환의 목적 `object` 고 `dynamic` 동일 하다 고 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-126">For the purposes of conversion, the types `object` and `dynamic` are considered equivalent.</span></span>

<span data-ttu-id="7b523-127">그러나 동적 변환을 ([암시적 동적 변환을](conversions.md#implicit-dynamic-conversions) 하 고 [명시적 동적 변환을](conversions.md#explicit-dynamic-conversions)) 형식의 식에만 적용 `dynamic` ([동적 형식](types.md#the-dynamic-type)).</span><span class="sxs-lookup"><span data-stu-id="7b523-127">However, dynamic conversions ([Implicit dynamic conversions](conversions.md#implicit-dynamic-conversions) and [Explicit dynamic conversions](conversions.md#explicit-dynamic-conversions)) apply only to expressions of type `dynamic` ([The dynamic type](types.md#the-dynamic-type)).</span></span>

### <a name="identity-conversion"></a><span data-ttu-id="7b523-128">Identity 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-128">Identity conversion</span></span>

<span data-ttu-id="7b523-129">Id 변환이 모든 형식에서 동일한 형식으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-129">An identity conversion converts from any type to the same type.</span></span> <span data-ttu-id="7b523-130">이 변환은 해당 형식으로 변환할 수는 필수 형식이 이미 있는 엔터티의 한다고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-130">This conversion exists such that an entity that already has a required type can be said to be convertible to that type.</span></span>

*  <span data-ttu-id="7b523-131">개체 및 동적 동일 하다 고 간주 이므로 간의 id 변환이 `object` 하 고 `dynamic`, 및 서로 동일의 모든 항목을 바꿀 때 생성 된 형식 `dynamic` 사용 하 여 `object`.</span><span class="sxs-lookup"><span data-stu-id="7b523-131">Because object and dynamic are considered equivalent there is an identity conversion between `object` and `dynamic`, and between constructed types that are the same when replacing all occurrences of `dynamic` with `object`.</span></span>

### <a name="implicit-numeric-conversions"></a><span data-ttu-id="7b523-132">암시적 숫자 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-132">Implicit numeric conversions</span></span>

<span data-ttu-id="7b523-133">암시적 숫자 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-133">The implicit numeric conversions are:</span></span>

*  <span data-ttu-id="7b523-134">`sbyte` 하 `short`, `int`, `long`, `float`를 `double`, 또는 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-134">From `sbyte` to `short`, `int`, `long`, `float`, `double`, or `decimal`.</span></span>
*  <span data-ttu-id="7b523-135">`byte` 하 `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `float`, `double`, 또는 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-135">From `byte` to `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `float`, `double`, or `decimal`.</span></span>
*  <span data-ttu-id="7b523-136">`short` 하 `int`를 `long`, `float`를 `double`, 또는 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-136">From `short` to `int`, `long`, `float`, `double`, or `decimal`.</span></span>
*  <span data-ttu-id="7b523-137">`ushort` 하 `int`, `uint`, `long`, `ulong`를 `float`, `double`, 또는 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-137">From `ushort` to `int`, `uint`, `long`, `ulong`, `float`, `double`, or `decimal`.</span></span>
*  <span data-ttu-id="7b523-138">`int` 하 `long`를 `float`를 `double`, 또는 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-138">From `int` to `long`, `float`, `double`, or `decimal`.</span></span>
*  <span data-ttu-id="7b523-139">`uint` 하 `long`를 `ulong`, `float`를 `double`, 또는 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-139">From `uint` to `long`, `ulong`, `float`, `double`, or `decimal`.</span></span>
*  <span data-ttu-id="7b523-140">`long` 하 `float`를 `double`, 또는 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-140">From `long` to `float`, `double`, or `decimal`.</span></span>
*  <span data-ttu-id="7b523-141">`ulong` 하 `float`를 `double`, 또는 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-141">From `ulong` to `float`, `double`, or `decimal`.</span></span>
*  <span data-ttu-id="7b523-142">`char` 하 `ushort`, `int`, `uint`, `long`, `ulong`, `float`를 `double`, 또는 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-142">From `char` to `ushort`, `int`, `uint`, `long`, `ulong`, `float`, `double`, or `decimal`.</span></span>
*  <span data-ttu-id="7b523-143">`float` 에 `double`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-143">From `float` to `double`.</span></span>

<span data-ttu-id="7b523-144">변환할 `int`, `uint`, `long`, 또는 `ulong` 에 `float` 들어오고 `long` 또는 `ulong` 를 `double` 정밀도 손실 될 수 있지만 두지 원인 크기는 손실 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-144">Conversions from `int`, `uint`, `long`, or `ulong` to `float` and from `long` or `ulong` to `double` may cause a loss of precision, but will never cause a loss of magnitude.</span></span> <span data-ttu-id="7b523-145">다른 암시적 숫자 변환에는 모든 정보가 손실 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-145">The other implicit numeric conversions never lose any information.</span></span>

<span data-ttu-id="7b523-146">으로 암시적 변환은 없습니다 합니다 `char` 입력을 다른 정수 계열 형식의 값을 자동으로 변환 하지 않습니다는 `char` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-146">There are no implicit conversions to the `char` type, so values of the other integral types do not automatically convert to the `char` type.</span></span>

### <a name="implicit-enumeration-conversions"></a><span data-ttu-id="7b523-147">열거형 암시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-147">Implicit enumeration conversions</span></span>

<span data-ttu-id="7b523-148">변환 하는 열거형 암시적 변환을 허용 합니다 *decimal_integer_literal* `0` 에 변환할 *enum_type* 및 모든 *nullable_type* 입니다 내부 형식에 *enum_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-148">An implicit enumeration conversion permits the *decimal_integer_literal* `0` to be converted to any *enum_type* and to any *nullable_type* whose underlying type is an *enum_type*.</span></span> <span data-ttu-id="7b523-149">후자의 경우 변환이 기본으로 전환 하 여 계산 *enum_type* 결과 줄 바꿈 ([Nullable 형식](types.md#nullable-types)).</span><span class="sxs-lookup"><span data-stu-id="7b523-149">In the latter case the conversion is evaluated by converting to the underlying *enum_type* and wrapping the result ([Nullable types](types.md#nullable-types)).</span></span>

### <a name="implicit-interpolated-string-conversions"></a><span data-ttu-id="7b523-150">보간된 문자열의 암시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-150">Implicit interpolated string conversions</span></span>

<span data-ttu-id="7b523-151">암시적 보간된 문자열 변환 허용을 *interpolated_string_expression* ([보간된 문자열](expressions.md#interpolated-strings))로 변환할 `System.IFormattable` 또는 `System.FormattableString` (구현 하는 `System.IFormattable`).</span><span class="sxs-lookup"><span data-stu-id="7b523-151">An implicit interpolated string conversion permits an *interpolated_string_expression* ([Interpolated strings](expressions.md#interpolated-strings)) to be converted to `System.IFormattable` or `System.FormattableString` (which implements `System.IFormattable`).</span></span>

<span data-ttu-id="7b523-152">이 변환을 적용 될 때 문자열 값은 하지 보간된 문자열에서 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-152">When this conversion is applied a string value is not composed from the interpolated string.</span></span> <span data-ttu-id="7b523-153">대신의 인스턴스이고 `System.FormattableString` 만든 이면에 설명 된 대로 [보간된 문자열](expressions.md#interpolated-strings)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-153">Instead an instance of `System.FormattableString` is created, as further described in [Interpolated strings](expressions.md#interpolated-strings).</span></span>

### <a name="implicit-nullable-conversions"></a><span data-ttu-id="7b523-154">Nullable 암시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-154">Implicit nullable conversions</span></span>

<span data-ttu-id="7b523-155">Nullable이 아닌 값 형식에서 작동 하는 미리 정의 된 암시적 변환이 이러한 형식의 null 허용 형식으로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-155">Predefined implicit conversions that operate on non-nullable value types can also be used with nullable forms of those types.</span></span> <span data-ttu-id="7b523-156">각각의 미리 정의 된 암시적 id 및 nullable이 아닌 값 형식에서 변환 하는 숫자 변환에 대 한 `S` nullable이 아닌 값 형식에 `T`, 다음과 같은 암시적 nullable 변환이 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-156">For each of the predefined implicit identity and numeric conversions that convert from a non-nullable value type `S` to a non-nullable value type `T`, the following implicit nullable conversions exist:</span></span>

*  <span data-ttu-id="7b523-157">암시적 변환이 `S?` 에 `T?`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-157">An implicit conversion from `S?` to `T?`.</span></span>
*  <span data-ttu-id="7b523-158">암시적 변환이 `S` 에 `T?`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-158">An implicit conversion from `S` to `T?`.</span></span>

<span data-ttu-id="7b523-159">Null 허용의 암시적 변환이 평가에서 변환 하는 기본 변환을 기반 `S` 에 `T` 다음과 같이 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-159">Evaluation of an implicit nullable conversion based on an underlying conversion from `S` to `T` proceeds as follows:</span></span>

*  <span data-ttu-id="7b523-160">nullable 변환 되는 경우 `S?` 에 `T?`:</span><span class="sxs-lookup"><span data-stu-id="7b523-160">If the nullable conversion is from `S?` to `T?`:</span></span>
    * <span data-ttu-id="7b523-161">원본 값이 null (`HasValue` 속성은 false), 결과 형식의 null 값 `T?`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-161">If the source value is null (`HasValue` property is false), the result is the null value of type `T?`.</span></span>
    * <span data-ttu-id="7b523-162">변환에서 래핑 해제를으로 평가 되는 고, 그렇지 `S?` 하 `S`고 뒤에 변환 하는 기본 `S` 하 `T`뒤에 래핑, ([Nullable 형식](types.md#nullable-types)) 에서`T` 에 `T?`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-162">Otherwise, the conversion is evaluated as an unwrapping from `S?` to `S`, followed by the underlying conversion from `S` to `T`, followed by a wrapping ([Nullable types](types.md#nullable-types)) from `T` to `T?`.</span></span>

*  <span data-ttu-id="7b523-163">nullable 변환 되는 경우 `S` 에 `T?`, 변환에서 기본 변환으로 평가 됩니다 `S` 에 `T` 뒤에에서 배치 `T` 를 `T?`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-163">If the nullable conversion is from `S` to `T?`, the conversion is evaluated as the underlying conversion from `S` to `T` followed by a wrapping from `T` to `T?`.</span></span>

### <a name="null-literal-conversions"></a><span data-ttu-id="7b523-164">Null 리터럴 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-164">Null literal conversions</span></span>

<span data-ttu-id="7b523-165">암시적 변환이 존재 합니다 `null` 모든 nullable 형식 리터럴.</span><span class="sxs-lookup"><span data-stu-id="7b523-165">An implicit conversion exists from the `null` literal to any nullable type.</span></span> <span data-ttu-id="7b523-166">이 변환은 null 값을 생성 ([Nullable 형식](types.md#nullable-types)) 지정된 된 nullable 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-166">This conversion produces the null value ([Nullable types](types.md#nullable-types)) of the given nullable type.</span></span>

### <a name="implicit-reference-conversions"></a><span data-ttu-id="7b523-167">암시적 참조 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-167">Implicit reference conversions</span></span>

<span data-ttu-id="7b523-168">암시적 참조 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-168">The implicit reference conversions are:</span></span>

*  <span data-ttu-id="7b523-169">모든 *reference_type* 하 `object` 및 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-169">From any *reference_type* to `object` and `dynamic`.</span></span>
*  <span data-ttu-id="7b523-170">*class_type* `S` 하나로 *class_type* `T`제공 `S` 에서 파생 된 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-170">From any *class_type* `S` to any *class_type* `T`, provided `S` is derived from `T`.</span></span>
*  <span data-ttu-id="7b523-171">*class_type* `S` 하나로 *interface_type* `T`제공 `S` 구현 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-171">From any *class_type* `S` to any *interface_type* `T`, provided `S` implements `T`.</span></span>
*  <span data-ttu-id="7b523-172">*interface_type* `S` 하나로 *interface_type* `T`제공 `S` 에서 파생 된 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-172">From any *interface_type* `S` to any *interface_type* `T`, provided `S` is derived from `T`.</span></span>
*  <span data-ttu-id="7b523-173">*array_type* `S` 요소 형식을 가진 `SE` 에 *array_type* `T` 요소 형식을 가진 `TE`경우 다음 모두:</span><span class="sxs-lookup"><span data-stu-id="7b523-173">From an *array_type* `S` with an element type `SE` to an *array_type* `T` with an element type `TE`, provided all of the following are true:</span></span>
    * <span data-ttu-id="7b523-174">`S` 및 `T` 요소 형식에 의해서만 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-174">`S` and `T` differ only in element type.</span></span> <span data-ttu-id="7b523-175">다시 말해 `S` 및 `T` 차원 수가 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-175">In other words, `S` and `T` have the same number of dimensions.</span></span>
    * <span data-ttu-id="7b523-176">둘 다 `SE` 하 고 `TE` 됩니다 *reference_type*s입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-176">Both `SE` and `TE` are *reference_type*s.</span></span>
    * <span data-ttu-id="7b523-177">암시적 참조 변환이 존재 `SE` 에 `TE`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-177">An implicit reference conversion exists from `SE` to `TE`.</span></span>
*  <span data-ttu-id="7b523-178">모든 *array_type* 에 `System.Array` 및 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-178">From any *array_type* to `System.Array` and the interfaces it implements.</span></span>
*  <span data-ttu-id="7b523-179">1 차원 배열 형식에서 `S[]` 하 `System.Collections.Generic.IList<T>` 및 해당 기본 인터페이스를 암시적 id 또는 참조 변환이 제공 `S` 에 `T`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-179">From a single-dimensional array type `S[]` to `System.Collections.Generic.IList<T>` and its base interfaces, provided that there is an implicit identity or reference conversion from `S` to `T`.</span></span>
*  <span data-ttu-id="7b523-180">모든 *delegate_type* 에 `System.Delegate` 및 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-180">From any *delegate_type* to `System.Delegate` and the interfaces it implements.</span></span>
*  <span data-ttu-id="7b523-181">에 null 리터럴에서 *reference_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-181">From the null literal to any *reference_type*.</span></span>
*  <span data-ttu-id="7b523-182">*reference_type* 에 *reference_type* `T` 으로 암시적 id 또는 참조 변환이 있는 경우를 *reference_type* `T0` 및 `T0` 에 identity 변환할 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-182">From any *reference_type* to a *reference_type* `T` if it has an implicit identity or reference conversion to a *reference_type* `T0` and `T0` has an identity conversion to `T`.</span></span>
*  <span data-ttu-id="7b523-183">모든 *reference_type* 인터페이스 또는 대리자 형식으로 `T` 인터페이스 또는 대리자 형식에 암시적 id 또는 참조 변환이 있으면 `T0` 및 `T0` 은 변환 ([ 변형 변환이](interfaces.md#variance-conversion))를 `T`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-183">From any *reference_type* to an interface or delegate type `T` if it has an implicit identity or reference conversion to an interface or delegate type `T0` and `T0` is variance-convertible ([Variance conversion](interfaces.md#variance-conversion)) to `T`.</span></span>
*  <span data-ttu-id="7b523-184">암시적 변환이 포함 된 참조 형식에 알려지지 않은 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-184">Implicit conversions involving type parameters that are known to be reference types.</span></span> <span data-ttu-id="7b523-185">참조 [형식 매개 변수를 포함 하는 암시적 변환은](conversions.md#implicit-conversions-involving-type-parameters) 형식 매개 변수를 포함 하는 암시적 변환에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-185">See [Implicit conversions involving type parameters](conversions.md#implicit-conversions-involving-type-parameters) for more details on implicit conversions involving type parameters.</span></span>

<span data-ttu-id="7b523-186">암시적 참조 변환 사이의 이러한 변환은 *reference_type*항상 성공으로 입증할 수 고 따라서 런타임에 검사를 요구 하는 s입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-186">The implicit reference conversions are those conversions between *reference_type*s that can be proven to always succeed, and therefore require no checks at run-time.</span></span>

<span data-ttu-id="7b523-187">참조 변환, 암시적 또는 명시적 변환 되는 개체의 참조 id를 변경 되어서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-187">Reference conversions, implicit or explicit, never change the referential identity of the object being converted.</span></span> <span data-ttu-id="7b523-188">즉, 변환은 참조 변환이 참조의 형식 변경 될 수 있지만,이 변경 되지 않습니다 형식 또는 참조 되는 개체의 값.</span><span class="sxs-lookup"><span data-stu-id="7b523-188">In other words, while a reference conversion may change the type of the reference, it never changes the type or value of the object being referred to.</span></span>

### <a name="boxing-conversions"></a><span data-ttu-id="7b523-189">Boxing 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-189">Boxing conversions</span></span>

<span data-ttu-id="7b523-190">boxing 변환이 허용을 *value_type* 참조 형식으로 암시적으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-190">A boxing conversion permits a *value_type* to be implicitly converted to a reference type.</span></span> <span data-ttu-id="7b523-191">Boxing 변환에서 존재 *non_nullable_value_type* 에 `object` 하 고 `dynamic`를 `System.ValueType` 및 모든 *interface_type* 구현한는 *non_ nullable_value_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-191">A boxing conversion exists from any *non_nullable_value_type* to `object` and `dynamic`, to `System.ValueType` and to any *interface_type* implemented by the *non_nullable_value_type*.</span></span> <span data-ttu-id="7b523-192">또한 프로그램 *enum_type* 형식으로 변환할 수 `System.Enum`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-192">Furthermore an *enum_type* can be converted to the type `System.Enum`.</span></span>

<span data-ttu-id="7b523-193">boxing 변환이 존재를 *nullable_type* 참조 형식으로 boxing 변환이 경우에 있는 기본 *non_nullable_value_type* 참조 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-193">A boxing conversion exists from a *nullable_type* to a reference type, if and only if a boxing conversion exists from the underlying *non_nullable_value_type* to the reference type.</span></span>

<span data-ttu-id="7b523-194">값 형식에는 인터페이스 형식으로 boxing 변환 `I` 인터페이스 형식으로는 boxing 변환이 있는지 `I0` 및 `I0` 에 identity 변환할 `I`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-194">A value type has a boxing conversion to an interface type `I` if it has a boxing conversion to an interface type `I0` and `I0` has an identity conversion to `I`.</span></span>

<span data-ttu-id="7b523-195">값 형식은 인터페이스 형식으로는 boxing 변환이 `I` 인터페이스 또는 대리자 형식에는 boxing 변환이 있을 경우 `I0` 하 고 `I0` 변환 됩니다 ([변형 변환이](interfaces.md#variance-conversion)) 를`I`.</span><span class="sxs-lookup"><span data-stu-id="7b523-195">A value type has a boxing conversion to an interface type `I` if it has a boxing conversion to an interface or delegate type `I0` and `I0` is variance-convertible ([Variance conversion](interfaces.md#variance-conversion)) to `I`.</span></span>

<span data-ttu-id="7b523-196">값을 *non_nullable_value_type* 이루어져 있습니다 개체 인스턴스를 할당 하 고 복사는 *value_type* 해당 인스턴스로 값.</span><span class="sxs-lookup"><span data-stu-id="7b523-196">Boxing a value of a *non_nullable_value_type* consists of allocating an object instance and copying the *value_type* value into that instance.</span></span> <span data-ttu-id="7b523-197">구조체 형식에 넣을 수 있습니다 `System.ValueType`구조체에 대 한 기본 클래스 이므로, ([상속](structs.md#inheritance)).</span><span class="sxs-lookup"><span data-stu-id="7b523-197">A struct can be boxed to the type `System.ValueType`, since that is a base class for all structs ([Inheritance](structs.md#inheritance)).</span></span>

<span data-ttu-id="7b523-198">값을 *nullable_type* 다음과 같이 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-198">Boxing a value of a *nullable_type* proceeds as follows:</span></span>

*  <span data-ttu-id="7b523-199">원본 값이 null 이면 (`HasValue` 속성이 false 이면), 결과 대상 형식의 null 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-199">If the source value is null (`HasValue` property is false), the result is a null reference of the target type.</span></span>
*  <span data-ttu-id="7b523-200">그렇지 않으면 결과 boxed 참조 `T` 압축을 풀고 원본 값을 boxing 하 여 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-200">Otherwise, the result is a reference to a boxed `T` produced by unwrapping and boxing the source value.</span></span>

<span data-ttu-id="7b523-201">Boxing 변환에 자세히 설명 되어 [Boxing 변환](types.md#boxing-conversions)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-201">Boxing conversions are described further in [Boxing conversions](types.md#boxing-conversions).</span></span>

### <a name="implicit-dynamic-conversions"></a><span data-ttu-id="7b523-202">동적 암시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-202">Implicit dynamic conversions</span></span>

<span data-ttu-id="7b523-203">형식의 식에서 암시적 동적 변환이 존재 `dynamic` 형식으로 `T`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-203">An implicit dynamic conversion exists from an expression of type `dynamic` to any type `T`.</span></span> <span data-ttu-id="7b523-204">변환 바인딩된 동적으로 ([동적 바인딩](expressions.md#dynamic-binding))를 런타임에 식의 런타임 형식에서 암시적 변환이 발생을 검색 하는 것이 즉 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-204">The conversion is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)), which means that an implicit conversion will be sought at run-time from the run-time type of the expression to `T`.</span></span> <span data-ttu-id="7b523-205">변환 작업 없이 있으면 런타임 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-205">If no conversion is found, a run-time exception is thrown.</span></span>

<span data-ttu-id="7b523-206">이 암시적 변환은의 시작 부분에서 권장 하는 것 처럼 보이는 위반 하는 참고 [암시적 변환을](conversions.md#implicit-conversions) 암시적 변환이 예외를 발생 시키는 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-206">Note that this implicit conversion seemingly violates the advice in the beginning of [Implicit conversions](conversions.md#implicit-conversions) that an implicit conversion should never cause an exception.</span></span> <span data-ttu-id="7b523-207">그러나 없는 자체 변환 하지만 *찾기* 예외를 발생 시키는 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-207">However it is not the conversion itself, but the *finding* of the conversion that causes the exception.</span></span> <span data-ttu-id="7b523-208">런타임 예외 위험이 동적 바인딩 사용 하 여에 정렬이 내재 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-208">The risk of run-time exceptions is inherent in the use of dynamic binding.</span></span> <span data-ttu-id="7b523-209">변환의 동적 바인딩 원하지 않는 경우 식 먼저 변환할 수 `object`, 한 다음 원하는 형식.</span><span class="sxs-lookup"><span data-stu-id="7b523-209">If dynamic binding of the conversion is not desired, the expression can be first converted to `object`, and then to the desired type.</span></span>

<span data-ttu-id="7b523-210">다음 예제에서는 암시적 동적 변환을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-210">The following example illustrates implicit dynamic conversions:</span></span>

```csharp
object o  = "object"
dynamic d = "dynamic";

string s1 = o; // Fails at compile-time -- no conversion exists
string s2 = d; // Compiles and succeeds at run-time
int i     = d; // Compiles but fails at run-time -- no conversion exists
```

<span data-ttu-id="7b523-211">에 할당 `s2` 및 `i` 암시적 동적 변환 작업의 바인딩을 런타임까지 일시 중단 된 둘 다 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-211">The assignments to `s2` and `i` both employ implicit dynamic conversions, where the binding of the operations is suspended until run-time.</span></span> <span data-ttu-id="7b523-212">실행 시의 런타임 형식에서 암시적 변환의 찾는 `d`  --  `string` -대상 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-212">At run-time, implicit conversions are sought from the run-time type of `d` -- `string` -- to the target type.</span></span> <span data-ttu-id="7b523-213">변환이 `string` 없습니다 `int`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-213">A conversion is found to `string` but not to `int`.</span></span>

### <a name="implicit-constant-expression-conversions"></a><span data-ttu-id="7b523-214">암시적 상수 식 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-214">Implicit constant expression conversions</span></span>

<span data-ttu-id="7b523-215">다음과 같은 변환이 허용 하는 상수 식을 암시적 변환이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-215">An implicit constant expression conversion permits the following conversions:</span></span>

*  <span data-ttu-id="7b523-216">A *constant_expression* ([상수 식](expressions.md#constant-expressions)) 형식의 `int` 형식으로 변환 될 수 있습니다 `sbyte`를 `byte`를 `short`, `ushort`를 `uint`, 또는 `ulong`의 값을 제공 합니다 *constant_expression* 대상 형식의 범위 내입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-216">A *constant_expression* ([Constant expressions](expressions.md#constant-expressions)) of type `int` can be converted to type `sbyte`, `byte`, `short`, `ushort`, `uint`, or `ulong`, provided the value of the *constant_expression* is within the range of the destination type.</span></span>
*  <span data-ttu-id="7b523-217">A *constant_expression* 형식의 `long` 형식으로 변환 될 수 있습니다 `ulong`의 값을 제공 합니다 *constant_expression* 는 음수가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-217">A *constant_expression* of type `long` can be converted to type `ulong`, provided the value of the *constant_expression* is not negative.</span></span>

### <a name="implicit-conversions-involving-type-parameters"></a><span data-ttu-id="7b523-218">형식 매개 변수를 포함 하는 암시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-218">Implicit conversions involving type parameters</span></span>

<span data-ttu-id="7b523-219">지정 된 형식 매개 변수는 다음과 같은 암시적 변환이 존재 `T`:</span><span class="sxs-lookup"><span data-stu-id="7b523-219">The following implicit conversions exist for a given type parameter `T`:</span></span>

*  <span data-ttu-id="7b523-220">`T` 유효한 기본 클래스에 `C`에서 `T` 의 모든 기본 클래스 `C`, 및 `T` 구현한 인터페이스 `C`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-220">From `T` to its effective base class `C`, from `T` to any base class of `C`, and from `T` to any interface implemented by `C`.</span></span> <span data-ttu-id="7b523-221">에 런타임 경우 `T` 값 형식이 boxing 변환으로 변환 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-221">At run-time, if `T` is a value type, the conversion is executed as a boxing conversion.</span></span> <span data-ttu-id="7b523-222">그렇지 않으면 변환이 암시적 참조 변환 또는 id 변환을 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-222">Otherwise, the conversion is executed as an implicit reference conversion or identity conversion.</span></span>
*  <span data-ttu-id="7b523-223">`T` 인터페이스 형식으로 `I` 에서 `T`의 효과적인 인터페이스 집합 들어오고 `T` 의 기본 인터페이스 `I`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-223">From `T` to an interface type `I` in `T`'s effective interface set and from `T` to any base interface of `I`.</span></span> <span data-ttu-id="7b523-224">에 런타임 경우 `T` 값 형식이 boxing 변환으로 변환 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-224">At run-time, if `T` is a value type, the conversion is executed as a boxing conversion.</span></span> <span data-ttu-id="7b523-225">그렇지 않으면 변환이 암시적 참조 변환 또는 id 변환을 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-225">Otherwise, the conversion is executed as an implicit reference conversion or identity conversion.</span></span>
*  <span data-ttu-id="7b523-226">`T` 형식 매개 변수에 `U`제공 `T` 에 따라 달라 집니다 `U` ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="7b523-226">From `T` to a type parameter `U`, provided `T` depends on `U` ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span> <span data-ttu-id="7b523-227">런타임 경우 at `U` 이 값 형식이 면 `T` 및 `U` 반드시 동일한 형식이 고 변환이 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-227">At run-time, if `U` is a value type, then `T` and `U` are necessarily the same type and no conversion is performed.</span></span> <span data-ttu-id="7b523-228">그렇지 않은 경우, `T` 값 형식이 boxing 변환으로 변환 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-228">Otherwise, if `T` is a value type, the conversion is executed as a boxing conversion.</span></span> <span data-ttu-id="7b523-229">그렇지 않으면 변환이 암시적 참조 변환 또는 id 변환을 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-229">Otherwise, the conversion is executed as an implicit reference conversion or identity conversion.</span></span>
*  <span data-ttu-id="7b523-230">null 리터럴을 `T`제공 `T` 참조 형식일 것으로 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-230">From the null literal to `T`, provided `T` is known to be a reference type.</span></span>
*  <span data-ttu-id="7b523-231">`T` 참조 형식으로 `I` 참조 형식으로 변환 하는 암시적 변환이 있는지 `S0` 하 고 `S0` 에 id 변환이 `S`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-231">From `T` to a reference type `I` if it has an implicit conversion to a reference type `S0` and `S0` has an identity conversion to `S`.</span></span> <span data-ttu-id="7b523-232">변환은 동일한 방식으로 변환으로을 실행 하는 데 런타임 시 `S0`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-232">At run-time the conversion is executed the same way as the conversion to `S0`.</span></span>
*  <span data-ttu-id="7b523-233">`T` 인터페이스 형식으로 `I` 인터페이스 또는 대리자 형식으로 암시적 변환이 있는 경우 `I0` 하 고 `I0` 변환 됩니다 하 `I` ([변형 변환이](interfaces.md#variance-conversion) ).</span><span class="sxs-lookup"><span data-stu-id="7b523-233">From `T` to an interface type `I` if it has an implicit conversion to an interface or delegate type `I0` and `I0` is variance-convertible to `I` ([Variance conversion](interfaces.md#variance-conversion)).</span></span> <span data-ttu-id="7b523-234">에 런타임 경우 `T` 값 형식이 boxing 변환으로 변환 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-234">At run-time, if `T` is a value type, the conversion is executed as a boxing conversion.</span></span> <span data-ttu-id="7b523-235">그렇지 않으면 변환이 암시적 참조 변환 또는 id 변환을 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-235">Otherwise, the conversion is executed as an implicit reference conversion or identity conversion.</span></span>

<span data-ttu-id="7b523-236">하는 경우 `T` 참조 형식인 것으로 알려진 ([입력 매개 변수 제약 조건이](classes.md#type-parameter-constraints)), 위의 변환은 모든 암시적 참조 변환으로 분류 됩니다 ([암시적 참조 변환](conversions.md#implicit-reference-conversions)).</span><span class="sxs-lookup"><span data-stu-id="7b523-236">If `T` is known to be a reference type ([Type parameter constraints](classes.md#type-parameter-constraints)), the conversions above are all classified as implicit reference conversions ([Implicit reference conversions](conversions.md#implicit-reference-conversions)).</span></span> <span data-ttu-id="7b523-237">하는 경우 `T` 는 참조 형식으로 알 수 없는 위의 변환은 boxing 변환으로 분류 됩니다 ([Boxing 변환](conversions.md#boxing-conversions)).</span><span class="sxs-lookup"><span data-stu-id="7b523-237">If `T` is not known to be a reference type, the conversions above are classified as boxing conversions ([Boxing conversions](conversions.md#boxing-conversions)).</span></span>

### <a name="user-defined-implicit-conversions"></a><span data-ttu-id="7b523-238">암시적 사용자 정의 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-238">User-defined implicit conversions</span></span>

<span data-ttu-id="7b523-239">사용자 정의 된 암시적 변환이 선택적 표준 암시적 변환이 뒤에 다른 선택적 표준 암시적 변환이 암시적 사용자 정의 변환 연산자를 실행 하 여 다음 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-239">A user-defined implicit conversion consists of an optional standard implicit conversion, followed by execution of a user-defined implicit conversion operator, followed by another optional standard implicit conversion.</span></span> <span data-ttu-id="7b523-240">암시적 사용자 정의 변환 평가 대 한 정확한 규칙에 설명 되어 있습니다 [암시적 사용자 정의 변환 처리](conversions.md#processing-of-user-defined-implicit-conversions)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-240">The exact rules for evaluating user-defined implicit conversions are described in [Processing of user-defined implicit conversions](conversions.md#processing-of-user-defined-implicit-conversions).</span></span>

### <a name="anonymous-function-conversions-and-method-group-conversions"></a><span data-ttu-id="7b523-241">익명 함수 변환 및 메서드 그룹 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-241">Anonymous function conversions and method group conversions</span></span>

<span data-ttu-id="7b523-242">익명 함수 및 메서드 그룹에 자체의 형식 필요가 없지만 형식 또는 식 트리 형식의 대리자를 암시적으로 변환 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-242">Anonymous functions and method groups do not have types in and of themselves, but may be implicitly converted to delegate types or expression tree types.</span></span> <span data-ttu-id="7b523-243">익명 함수 변환에 자세히 설명 되어 있습니다 [익명 함수 변환](conversions.md#anonymous-function-conversions) 및에 메서드 그룹 변환 [메서드 그룹 변환](conversions.md#method-group-conversions)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-243">Anonymous function conversions are described in more detail in [Anonymous function conversions](conversions.md#anonymous-function-conversions) and method group conversions in [Method group conversions](conversions.md#method-group-conversions).</span></span>

## <a name="explicit-conversions"></a><span data-ttu-id="7b523-244">명시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-244">Explicit conversions</span></span>

<span data-ttu-id="7b523-245">다음 변환은 명시적 변환으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-245">The following conversions are classified as explicit conversions:</span></span>

*  <span data-ttu-id="7b523-246">모든 암시적 변환입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-246">All implicit conversions.</span></span>
*  <span data-ttu-id="7b523-247">명시적 숫자 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-247">Explicit numeric conversions.</span></span>
*  <span data-ttu-id="7b523-248">명시적 열거형 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-248">Explicit enumeration conversions.</span></span>
*  <span data-ttu-id="7b523-249">명시적 nullable 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-249">Explicit nullable conversions.</span></span>
*  <span data-ttu-id="7b523-250">명시적 참조 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-250">Explicit reference conversions.</span></span>
*  <span data-ttu-id="7b523-251">명시적 인터페이스 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-251">Explicit interface conversions.</span></span>
*  <span data-ttu-id="7b523-252">Unboxing 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-252">Unboxing conversions.</span></span>
*  <span data-ttu-id="7b523-253">동적 명시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-253">Explicit dynamic conversions</span></span>
*  <span data-ttu-id="7b523-254">사용자 정의 명시적 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-254">User-defined explicit conversions.</span></span>

<span data-ttu-id="7b523-255">명시적 변환은 cast 식에서 발생할 수 있습니다 ([캐스트 식](expressions.md#cast-expressions)).</span><span class="sxs-lookup"><span data-stu-id="7b523-255">Explicit conversions can occur in cast expressions ([Cast expressions](expressions.md#cast-expressions)).</span></span>

<span data-ttu-id="7b523-256">명시적 변환의 집합에는 모든 암시적 변환이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-256">The set of explicit conversions includes all implicit conversions.</span></span> <span data-ttu-id="7b523-257">즉, 중복 된 캐스트 식이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-257">This means that redundant cast expressions are allowed.</span></span>

<span data-ttu-id="7b523-258">명시적 변환은 암시적 변환 되지 않은 값은 명시적 요구를 충분히 서로 다른 형식의 도메인에 걸쳐 항상 성공으로 입증할 수 없는 변환, 내용은 손실 될 수도 있는 변환 및 변환 표기법입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-258">The explicit conversions that are not implicit conversions are conversions that cannot be proven to always succeed, conversions that are known to possibly lose information, and conversions across domains of types sufficiently different to merit explicit notation.</span></span>

### <a name="explicit-numeric-conversions"></a><span data-ttu-id="7b523-259">명시적 숫자 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-259">Explicit numeric conversions</span></span>

<span data-ttu-id="7b523-260">명시적 숫자 변환에서 변환 되는 *numeric_type* 간 *numeric_type* 는 암시적 숫자 변환이 ([암시적 숫자 변환](conversions.md#implicit-numeric-conversions)) 아직 없으면:</span><span class="sxs-lookup"><span data-stu-id="7b523-260">The explicit numeric conversions are the conversions from a *numeric_type* to another *numeric_type* for which an implicit numeric conversion ([Implicit numeric conversions](conversions.md#implicit-numeric-conversions)) does not already exist:</span></span>

*  <span data-ttu-id="7b523-261">`sbyte` 하 `byte`를 `ushort`, `uint`를 `ulong`, 또는 `char`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-261">From `sbyte` to `byte`, `ushort`, `uint`, `ulong`, or `char`.</span></span>
*  <span data-ttu-id="7b523-262">`byte` 하 `sbyte` 고 `char`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-262">From `byte` to `sbyte` and `char`.</span></span>
*  <span data-ttu-id="7b523-263">`short` 하 `sbyte`, `byte`, `ushort`, `uint`를 `ulong`, 또는 `char`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-263">From `short` to `sbyte`, `byte`, `ushort`, `uint`, `ulong`, or `char`.</span></span>
*  <span data-ttu-id="7b523-264">`ushort` 하 `sbyte`를 `byte`를 `short`, 또는 `char`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-264">From `ushort` to `sbyte`, `byte`, `short`, or `char`.</span></span>
*  <span data-ttu-id="7b523-265">`int` 하 `sbyte`, `byte`, `short`, `ushort`를 `uint`, `ulong`, 또는 `char`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-265">From `int` to `sbyte`, `byte`, `short`, `ushort`, `uint`, `ulong`, or `char`.</span></span>
*  <span data-ttu-id="7b523-266">`uint` 하 `sbyte`, `byte`, `short`, `ushort`를 `int`, 또는 `char`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-266">From `uint` to `sbyte`, `byte`, `short`, `ushort`, `int`, or `char`.</span></span>
*  <span data-ttu-id="7b523-267">`long` 하 `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`를 `ulong`, 또는 `char`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-267">From `long` to `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `ulong`, or `char`.</span></span>
*  <span data-ttu-id="7b523-268">`ulong` 하 `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`를 `long`, 또는 `char`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-268">From `ulong` to `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, or `char`.</span></span>
*  <span data-ttu-id="7b523-269">`char` 하 `sbyte`를 `byte`, 또는 `short`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-269">From `char` to `sbyte`, `byte`, or `short`.</span></span>
*  <span data-ttu-id="7b523-270">`float` 하 `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, 또는 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-270">From `float` to `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, or `decimal`.</span></span>
*  <span data-ttu-id="7b523-271">`double` 하 `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, 또는 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-271">From `double` to `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, or `decimal`.</span></span>
*  <span data-ttu-id="7b523-272">`decimal` 하 `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, 또는 `double`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-272">From `decimal` to `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, or `double`.</span></span>

<span data-ttu-id="7b523-273">있기 때문에 모든 명시적 및 암시적 숫자 변환에 포함 하는 명시적 변환을 항상에서 변환할 *numeric_type* 다른 *numeric_type* 캐스트 식 (사용 하 여 [캐스트 식](expressions.md#cast-expressions)).</span><span class="sxs-lookup"><span data-stu-id="7b523-273">Because the explicit conversions include all implicit and explicit numeric conversions, it is always possible to convert from any *numeric_type* to any other *numeric_type* using a cast expression ([Cast expressions](expressions.md#cast-expressions)).</span></span>

<span data-ttu-id="7b523-274">명시적 숫자 변환 정보가 손실 될 또는 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-274">The explicit numeric conversions possibly lose information or possibly cause exceptions to be thrown.</span></span> <span data-ttu-id="7b523-275">명시적 숫자 변환은 다음과 같이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-275">An explicit numeric conversion is processed as follows:</span></span>

*  <span data-ttu-id="7b523-276">정수 계열 형식에서 다른 정수 계열 형식으로 변환의 처리에 따라 달라 집니다 오버플로 검사 컨텍스트에 ([checked 및 unchecked 연산자](expressions.md#the-checked-and-unchecked-operators)) 변환 되는 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-276">For a conversion from an integral type to another integral type, the processing depends on the overflow checking context ([The checked and unchecked operators](expressions.md#the-checked-and-unchecked-operators)) in which the conversion takes place:</span></span>
    * <span data-ttu-id="7b523-277">에 `checked` 컨텍스트에서 소스 피연산자의 값이 대상 형식의 범위 내에 있지만 throw 하는 경우 변환이 성공는 `System.OverflowException` 소스 피연산자의 값이 대상 형식의 범위를 벗어난 경우.</span><span class="sxs-lookup"><span data-stu-id="7b523-277">In a `checked` context, the conversion succeeds if the value of the source operand is within the range of the destination type, but throws a `System.OverflowException` if the value of the source operand is outside the range of the destination type.</span></span>
    * <span data-ttu-id="7b523-278">에 `unchecked` 컨텍스트에 변환이 항상 성공 하 고 다음과 같이 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-278">In an `unchecked` context, the conversion always succeeds, and proceeds as follows.</span></span>
        * <span data-ttu-id="7b523-279">소스 형식이 대상 형식보다 큰 경우 소스 값은 가장 중요한 비트인 해당 "extra"를 삭제함으로써 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-279">If the source type is larger than the destination type, then the source value is truncated by discarding its "extra" most significant bits.</span></span> <span data-ttu-id="7b523-280">그런 다음, 결과는 대상 형식의 값으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-280">The result is then treated as a value of the destination type.</span></span>
        * <span data-ttu-id="7b523-281">소스 형식이 대상 형식보다 작은 경우 소스 값은 대상 형식과 크기가 같도록 부호 확장 또는 0 확장 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-281">If the source type is smaller than the destination type, then the source value is either sign-extended or zero-extended so that it is the same size as the destination type.</span></span> <span data-ttu-id="7b523-282">부호 확장은 소스 형식이 서명된 경우 사용되며, 소스 형식이 서명되지 않은 경우 0 확장이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-282">Sign-extension is used if the source type is signed; zero-extension is used if the source type is unsigned.</span></span> <span data-ttu-id="7b523-283">그런 다음, 결과는 대상 형식의 값으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-283">The result is then treated as a value of the destination type.</span></span>
        * <span data-ttu-id="7b523-284">소스 형식이 대상 형식과 동일한 크기인 경우 소스 값은 대상 형식의 값으로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-284">If the source type is the same size as the destination type, then the source value is treated as a value of the destination type.</span></span>
*  <span data-ttu-id="7b523-285">변환에 대 한 `decimal` 정수 계열 형식으로 원본 값이 0에 가장 가까운 정수 값으로 반올림 됩니다 및 정수 계열 값이 변환의 결과가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-285">For a conversion from `decimal` to an integral type, the source value is rounded towards zero to the nearest integral value, and this integral value becomes the result of the conversion.</span></span> <span data-ttu-id="7b523-286">결과 정수 값을 대상 형식의 범위를 벗어난 경우는 `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-286">If the resulting integral value is outside the range of the destination type, a `System.OverflowException` is thrown.</span></span>
*  <span data-ttu-id="7b523-287">변환에 대 한 `float` 나 `double` 정수 계열 형식으로 처리 하는 종속 오버플로 검사 컨텍스트에 ([checked 및 unchecked 연산자](expressions.md#the-checked-and-unchecked-operators)) 변환 되는 배치:</span><span class="sxs-lookup"><span data-stu-id="7b523-287">For a conversion from `float` or `double` to an integral type, the processing depends on the overflow checking context ([The checked and unchecked operators](expressions.md#the-checked-and-unchecked-operators)) in which the conversion takes place:</span></span>
    * <span data-ttu-id="7b523-288">에 `checked` 컨텍스트 변환 다음과 같이 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-288">In a `checked` context, the conversion proceeds as follows:</span></span>
        * <span data-ttu-id="7b523-289">피연산자의 값이 NaN 또는 무한 한 `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-289">If the value of the operand is NaN or infinite, a `System.OverflowException` is thrown.</span></span>
        * <span data-ttu-id="7b523-290">그렇지 않으면 소스 피연산자는 0에 가장 가까운 정수 값으로 반올림 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-290">Otherwise, the source operand is rounded towards zero to the nearest integral value.</span></span> <span data-ttu-id="7b523-291">정수 계열 값이 대상 형식의 범위 내에 있으면이 값은 변환의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-291">If this integral value is within the range of the destination type then this value is the result of the conversion.</span></span>
        * <span data-ttu-id="7b523-292">그렇지 않으면 `System.OverflowException`이 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-292">Otherwise, a `System.OverflowException` is thrown.</span></span>
    * <span data-ttu-id="7b523-293">에 `unchecked` 컨텍스트에 변환이 항상 성공 하 고 다음과 같이 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-293">In an `unchecked` context, the conversion always succeeds, and proceeds as follows.</span></span>
        * <span data-ttu-id="7b523-294">피연산자의 값 NaN 또는 무한 인 경우 변환 결과 값인 지정 되지 않은 대상 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-294">If the value of the operand is NaN or infinite, the result of the conversion is an unspecified value of the destination type.</span></span>
        * <span data-ttu-id="7b523-295">그렇지 않으면 소스 피연산자는 0에 가장 가까운 정수 값으로 반올림 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-295">Otherwise, the source operand is rounded towards zero to the nearest integral value.</span></span> <span data-ttu-id="7b523-296">정수 계열 값이 대상 형식의 범위 내에 있으면이 값은 변환의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-296">If this integral value is within the range of the destination type then this value is the result of the conversion.</span></span>
        * <span data-ttu-id="7b523-297">그렇지 않은 경우 변환의 결과 대상 형식의 값을 알 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="7b523-297">Otherwise, the result of the conversion is an unspecified value of the destination type.</span></span>
*  <span data-ttu-id="7b523-298">변환에 대 한 `double` 하 `float`의 `double` 값은 반올림 가장 가까운 `float` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-298">For a conversion from `double` to `float`, the `double` value is rounded to the nearest `float` value.</span></span> <span data-ttu-id="7b523-299">경우는 `double` 값이 너무 작아서로 나타낼 수는 `float`, 결과 양의 0 또는 음의 0입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-299">If the `double` value is too small to represent as a `float`, the result becomes positive zero or negative zero.</span></span> <span data-ttu-id="7b523-300">경우는 `double` 값이 너무 커서로 나타낼 수는 `float`, 결과 양의 무한대 또는 음의 무한대입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-300">If the `double` value is too large to represent as a `float`, the result becomes positive infinity or negative infinity.</span></span> <span data-ttu-id="7b523-301">경우는 `double` 값이 NaN, 결과가 NaN 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-301">If the `double` value is NaN, the result is also NaN.</span></span>
*  <span data-ttu-id="7b523-302">변환에 대 한 `float` 또는 `double` 하 `decimal`, 소스 값으로 변환 됩니다 `decimal` 표현이 필요한 경우 가장 가까운 28 소수 자릿수가 반올림 ([10 진수 형식](types.md#the-decimal-type)).</span><span class="sxs-lookup"><span data-stu-id="7b523-302">For a conversion from `float` or `double` to `decimal`, the source value is converted to `decimal` representation and rounded to the nearest number after the 28th decimal place if required ([The decimal type](types.md#the-decimal-type)).</span></span> <span data-ttu-id="7b523-303">원본 값이 너무 작아로 나타낼 수 없는 경우는 `decimal`, 결과 0이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-303">If the source value is too small to represent as a `decimal`, the result becomes zero.</span></span> <span data-ttu-id="7b523-304">원본 값이 NaN, 무한대 또는 너무 커서로 나타낼 수는 `decimal`, `System.OverflowException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-304">If the source value is NaN, infinity, or too large to represent as a `decimal`, a `System.OverflowException` is thrown.</span></span>
*  <span data-ttu-id="7b523-305">변환에 대 한 `decimal` 하 `float` 또는 `double`의 `decimal` 값은 반올림 가장 가까운 `double` 또는 `float` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-305">For a conversion from `decimal` to `float` or `double`, the `decimal` value is rounded to the nearest `double` or `float` value.</span></span> <span data-ttu-id="7b523-306">이 변환의 정밀도 떨어지는는 예외를 throw 하지 않습니다 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-306">While this conversion may lose precision, it never causes an exception to be thrown.</span></span>

### <a name="explicit-enumeration-conversions"></a><span data-ttu-id="7b523-307">명시적 열거형 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-307">Explicit enumeration conversions</span></span>

<span data-ttu-id="7b523-308">명시적 열거형 변환은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-308">The explicit enumeration conversions are:</span></span>

*  <span data-ttu-id="7b523-309">`sbyte`, `byte`, `short`, `ushort`, `int`를 `uint`, `long`, `ulong`, `char`, `float`, `double`, 또는 `decimal` 모든 를*enum_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-309">From `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, or `decimal` to any *enum_type*.</span></span>
*  <span data-ttu-id="7b523-310">*enum_type* 하 `sbyte`, `byte`, `short`를 `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, 또는 `decimal`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-310">From any *enum_type* to `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, or `decimal`.</span></span>
*  <span data-ttu-id="7b523-311">모든 *enum_type* 다른 *enum_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-311">From any *enum_type* to any other *enum_type*.</span></span>

<span data-ttu-id="7b523-312">두 형식 간의 명시적 열거형 변환은 모든 참여 하 고 처리 하 여 처리 됩니다 *enum_type* 의 내부 형식으로 *enum_type*, 암시적 또는 명시적를 만든 후 수행 결과 형식 간의 변환 숫자입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-312">An explicit enumeration conversion between two types is processed by treating any participating *enum_type* as the underlying type of that *enum_type*, and then performing an implicit or explicit numeric conversion between the resulting types.</span></span> <span data-ttu-id="7b523-313">예를 들어를 *enum_type* `E` 사용 하 여의 내부 형식 및 `int`, 변환 `E` 하 `byte` 명시적 숫자 변환으로 처리 됩니다 ([Explicit 숫자 변환](conversions.md#explicit-numeric-conversions))에서 `int` 하 `byte`에서 변환이 `byte` 하 `E` 암시적 숫자 변환으로 처리 됩니다 ([암시적 숫자 변환](conversions.md#implicit-numeric-conversions)) `byte` 에 `int`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-313">For example, given an *enum_type* `E` with and underlying type of `int`, a conversion from `E` to `byte` is processed as an explicit numeric conversion ([Explicit numeric conversions](conversions.md#explicit-numeric-conversions)) from `int` to `byte`, and a conversion from `byte` to `E` is processed as an implicit numeric conversion ([Implicit numeric conversions](conversions.md#implicit-numeric-conversions)) from `byte` to `int`.</span></span>

### <a name="explicit-nullable-conversions"></a><span data-ttu-id="7b523-314">명시적 nullable 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-314">Explicit nullable conversions</span></span>

<span data-ttu-id="7b523-315">***Null을 허용 하는 명시적 변환을*** 허용 미리도 이러한 형식의 null 허용 형식으로 사용할 nullable이 아닌 값 형식에서 작동 하는 명시적 변환을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-315">***Explicit nullable conversions*** permit predefined explicit conversions that operate on non-nullable value types to also be used with nullable forms of those types.</span></span> <span data-ttu-id="7b523-316">Nullable이 아닌 값 형식에서 변환 하는 미리 정의 된 명시적 변환의 각 `S` nullable이 아닌 값 형식 `T` ([Id 변환을](conversions.md#identity-conversion), [암시적숫자변환](conversions.md#implicit-numeric-conversions), [암시적 열거형 변환](conversions.md#implicit-enumeration-conversions)를 [명시적 숫자 변환](conversions.md#explicit-numeric-conversions), 및 [명시적 열거형 변환](conversions.md#explicit-enumeration-conversions)), 다음 nullable 변환 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-316">For each of the predefined explicit conversions that convert from a non-nullable value type `S` to a non-nullable value type `T` ([Identity conversion](conversions.md#identity-conversion), [Implicit numeric conversions](conversions.md#implicit-numeric-conversions), [Implicit enumeration conversions](conversions.md#implicit-enumeration-conversions), [Explicit numeric conversions](conversions.md#explicit-numeric-conversions), and [Explicit enumeration conversions](conversions.md#explicit-enumeration-conversions)), the following nullable conversions exist:</span></span>

*  <span data-ttu-id="7b523-317">변환 하는 명시적 변환을 `S?` 에 `T?`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-317">An explicit conversion from `S?` to `T?`.</span></span>
*  <span data-ttu-id="7b523-318">변환 하는 명시적 변환을 `S` 에 `T?`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-318">An explicit conversion from `S` to `T?`.</span></span>
*  <span data-ttu-id="7b523-319">변환 하는 명시적 변환을 `S?` 에 `T`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-319">An explicit conversion from `S?` to `T`.</span></span>

<span data-ttu-id="7b523-320">평가 nullable 변환에서 변환 하는 기본 변환을 기반 `S` 에 `T` 다음과 같이 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-320">Evaluation of a nullable conversion based on an underlying conversion from `S` to `T` proceeds as follows:</span></span>

*  <span data-ttu-id="7b523-321">nullable 변환 되는 경우 `S?` 에 `T?`:</span><span class="sxs-lookup"><span data-stu-id="7b523-321">If the nullable conversion is from `S?` to `T?`:</span></span>
    * <span data-ttu-id="7b523-322">원본 값이 null (`HasValue` 속성은 false), 결과 형식의 null 값 `T?`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-322">If the source value is null (`HasValue` property is false), the result is the null value of type `T?`.</span></span>
    * <span data-ttu-id="7b523-323">변환에서 래핑 해제를으로 평가 되는 고, 그렇지 `S?` 에 `S`고 뒤에 변환 하는 기본 `S` 에 `T`에서 래핑 뒤 `T` 에 `T?`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-323">Otherwise, the conversion is evaluated as an unwrapping from `S?` to `S`, followed by the underlying conversion from `S` to `T`, followed by a wrapping from `T` to `T?`.</span></span>
*  <span data-ttu-id="7b523-324">nullable 변환 되는 경우 `S` 에 `T?`, 변환에서 기본 변환으로 평가 됩니다 `S` 에 `T` 뒤에에서 배치 `T` 를 `T?`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-324">If the nullable conversion is from `S` to `T?`, the conversion is evaluated as the underlying conversion from `S` to `T` followed by a wrapping from `T` to `T?`.</span></span>
*  <span data-ttu-id="7b523-325">nullable 변환 되는 경우 `S?` 하 `T`, 변환에서 래핑 해제를로 평가 됩니다 `S?` 에 `S` 뒤에 변환 하는 기본 `S` 에 `T`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-325">If the nullable conversion is from `S?` to `T`, the conversion is evaluated as an unwrapping from `S?` to `S` followed by the underlying conversion from `S` to `T`.</span></span>

<span data-ttu-id="7b523-326">값이 null 허용 값을 래핑 해제 하려고 한 경우 예외가 throw 됩니다 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-326">Note that an attempt to unwrap a nullable value will throw an exception if the value is `null`.</span></span>

### <a name="explicit-reference-conversions"></a><span data-ttu-id="7b523-327">명시적 참조 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-327">Explicit reference conversions</span></span>

<span data-ttu-id="7b523-328">명시적 참조 변환은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-328">The explicit reference conversions are:</span></span>

*  <span data-ttu-id="7b523-329">`object` 하 고 `dynamic` 다른 *reference_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-329">From `object` and `dynamic` to any other *reference_type*.</span></span>
*  <span data-ttu-id="7b523-330">*class_type* `S` 하나로 *class_type* `T`제공 `S` 의 기본 클래스인 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-330">From any *class_type* `S` to any *class_type* `T`, provided `S` is a base class of `T`.</span></span>
*  <span data-ttu-id="7b523-331">*class_type* `S` 하나로 *interface_type* `T`제공 `S` 봉인 되거나 제공 되지 않은 `S` 구현 하지 않는 `T`.</span><span class="sxs-lookup"><span data-stu-id="7b523-331">From any *class_type* `S` to any *interface_type* `T`, provided `S` is not sealed and provided `S` does not implement `T`.</span></span>
*  <span data-ttu-id="7b523-332">*interface_type* `S` 하나로 *class_type* `T`제공 `T` 봉인 되거나 제공 되지 `T` 구현 `S`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-332">From any *interface_type* `S` to any *class_type* `T`, provided `T` is not sealed or provided `T` implements `S`.</span></span>
*  <span data-ttu-id="7b523-333">*interface_type* `S` 하나로 *interface_type* `T`제공 `S` 에서 파생 되지 않은 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-333">From any *interface_type* `S` to any *interface_type* `T`, provided `S` is not derived from `T`.</span></span>
*  <span data-ttu-id="7b523-334">*array_type* `S` 요소 형식을 가진 `SE` 에 *array_type* `T` 요소 형식을 가진 `TE`경우 다음 모두:</span><span class="sxs-lookup"><span data-stu-id="7b523-334">From an *array_type* `S` with an element type `SE` to an *array_type* `T` with an element type `TE`, provided all of the following are true:</span></span>
    * <span data-ttu-id="7b523-335">`S` 및 `T` 요소 형식에 의해서만 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-335">`S` and `T` differ only in element type.</span></span> <span data-ttu-id="7b523-336">다시 말해 `S` 및 `T` 차원 수가 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-336">In other words, `S` and `T` have the same number of dimensions.</span></span>
    * <span data-ttu-id="7b523-337">둘 다 `SE` 하 고 `TE` 됩니다 *reference_type*s입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-337">Both `SE` and `TE` are *reference_type*s.</span></span>
    * <span data-ttu-id="7b523-338">명시적 참조 변환이 존재 `SE` 에 `TE`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-338">An explicit reference conversion exists from `SE` to `TE`.</span></span>
*  <span data-ttu-id="7b523-339">`System.Array` 인터페이스를 구현 하 고 *array_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-339">From `System.Array` and the interfaces it implements to any *array_type*.</span></span>
*  <span data-ttu-id="7b523-340">1 차원 배열 형식에서 `S[]` 하 `System.Collections.Generic.IList<T>` 및 해당 기본 인터페이스에서 명시적 참조 변환이 제공 `S` 에 `T`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-340">From a single-dimensional array type `S[]` to `System.Collections.Generic.IList<T>` and its base interfaces, provided that there is an explicit reference conversion from `S` to `T`.</span></span>
*  <span data-ttu-id="7b523-341">`System.Collections.Generic.IList<S>` 및 1 차원 배열 형식에 기본 인터페이스 `T[]`에서 사용 되는 명시적 id 또는 참조 변환이 있는 경우 `S` 하려면 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-341">From `System.Collections.Generic.IList<S>` and its base interfaces to a single-dimensional array type `T[]`, provided that there is an explicit identity or reference conversion from `S` to `T`.</span></span>
*  <span data-ttu-id="7b523-342">`System.Delegate` 인터페이스를 구현 하 고 *delegate_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-342">From `System.Delegate` and the interfaces it implements to any *delegate_type*.</span></span>
*  <span data-ttu-id="7b523-343">참조 형식에 대 한 참조 형식에서 `T` 참조 형식으로 변환 하는 명시적 참조 변환이 있는지 `T0` 하 고 `T0` id 변환이 `T`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-343">From a reference type to a reference type `T` if it has an explicit reference conversion to a reference type `T0` and `T0` has an identity conversion `T`.</span></span>
*  <span data-ttu-id="7b523-344">인터페이스 또는 대리자 형식에 대 한 참조 형식에서 `T` 인터페이스 또는 대리자 형식으로 명시적 참조 변환이 있을 경우 `T0` 고 `T0` 변형 가능은 하 `T` 또는 `T` 는 분산-변환할 `T0` ([변형 변환이](interfaces.md#variance-conversion)).</span><span class="sxs-lookup"><span data-stu-id="7b523-344">From a reference type to an interface or delegate type `T` if it has an explicit reference conversion to an interface or delegate type `T0` and either `T0` is variance-convertible to `T` or `T` is variance-convertible to `T0` ([Variance conversion](interfaces.md#variance-conversion)).</span></span>
*  <span data-ttu-id="7b523-345">`D<S1...Sn>` 하 `D<T1...Tn>` 여기서 `D<X1...Xn>` 제네릭 대리자 형식인 `D<S1...Sn>` 동일 하거나 호환 되지 `D<T1...Tn>`, 및 각 형식 매개 변수에 `Xi` 의 `D` 다음 포함:</span><span class="sxs-lookup"><span data-stu-id="7b523-345">From `D<S1...Sn>` to `D<T1...Tn>` where `D<X1...Xn>` is a generic delegate type, `D<S1...Sn>` is not compatible with or identical to `D<T1...Tn>`, and for each type parameter `Xi` of `D` the following holds:</span></span>
    * <span data-ttu-id="7b523-346">하는 경우 `Xi` 다음 변형의 경우 아닙니다 `Si` 동일 `Ti`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-346">If `Xi` is invariant, then `Si` is identical to `Ti`.</span></span>
    * <span data-ttu-id="7b523-347">하는 경우 `Xi` 는 공변 (covariant)는 암시적 또는 명시적 id 또는 참조 변환이에서 됩니다 `Si` 를 `Ti`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-347">If `Xi` is covariant, then there is an implicit or explicit identity or reference conversion from `Si` to `Ti`.</span></span>
    * <span data-ttu-id="7b523-348">하는 경우 `Xi` 반공 분산 이면 `Si` 및 `Ti` 은 동일한 또는 둘 다 참조 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-348">If `Xi` is contravariant, then `Si` and `Ti` are either identical or both reference types.</span></span>
*  <span data-ttu-id="7b523-349">명시적 변환 관련 된 참조 형식에 알려지지 않은 매개 변수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-349">Explicit conversions involving type parameters that are known to be reference types.</span></span> <span data-ttu-id="7b523-350">형식 매개 변수를 포함 하는 명시적 변환에 대 한 자세한 내용은 참조 하세요. [형식 매개 변수를 포함 하는 명시적 변환은](conversions.md#explicit-conversions-involving-type-parameters)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-350">For more details on explicit conversions involving type parameters, see [Explicit conversions involving type parameters](conversions.md#explicit-conversions-involving-type-parameters).</span></span>

<span data-ttu-id="7b523-351">명시적 참조 변환은 정확한 지 확인에 런타임 검사를 해야 하는 참조 형식 간의 변환입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-351">The explicit reference conversions are those conversions between reference-types that require run-time checks to ensure they are correct.</span></span>

<span data-ttu-id="7b523-352">명시적 참조를 성공적으로 변환 런타임에 소스 피연산자의 값은 `null`, 소스 피연산자가 참조 하는 개체의 실제 형식에 대 한 암시적 참조가 대상 형식으로 변환 될 수 있는 형식 이어야 합니다. 또는 변환 ([암시적 참조 변환을](conversions.md#implicit-reference-conversions)) boxing 변환이 나 ([Boxing 변환](conversions.md#boxing-conversions)).</span><span class="sxs-lookup"><span data-stu-id="7b523-352">For an explicit reference conversion to succeed at run-time, the value of the source operand must be `null`, or the actual type of the object referenced by the source operand must be a type that can be converted to the destination type by an implicit reference conversion ([Implicit reference conversions](conversions.md#implicit-reference-conversions)) or boxing conversion ([Boxing conversions](conversions.md#boxing-conversions)).</span></span> <span data-ttu-id="7b523-353">명시적 참조 변환이 실패 하는 경우는 `System.InvalidCastException` throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-353">If an explicit reference conversion fails, a `System.InvalidCastException` is thrown.</span></span>

<span data-ttu-id="7b523-354">참조 변환, 암시적 또는 명시적 변환 되는 개체의 참조 id를 변경 되어서는 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-354">Reference conversions, implicit or explicit, never change the referential identity of the object being converted.</span></span> <span data-ttu-id="7b523-355">즉, 변환은 참조 변환이 참조의 형식 변경 될 수 있지만,이 변경 되지 않습니다 형식 또는 참조 되는 개체의 값.</span><span class="sxs-lookup"><span data-stu-id="7b523-355">In other words, while a reference conversion may change the type of the reference, it never changes the type or value of the object being referred to.</span></span>

### <a name="unboxing-conversions"></a><span data-ttu-id="7b523-356">Unboxing 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-356">Unboxing conversions</span></span>

<span data-ttu-id="7b523-357">Unboxing 변환 허용 참조 형식을 명시적으로 변환할 수는 *value_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-357">An unboxing conversion permits a reference type to be explicitly converted to a *value_type*.</span></span> <span data-ttu-id="7b523-358">Unboxing 변환 유형에 서 존재 `object`, `dynamic` 하 고 `System.ValueType` 에 *non_nullable_value_type*, 및에서 *interface_type* 에 *non_ nullable_value_type* 를 구현 하는 *interface_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-358">An unboxing conversion exists from the types `object`, `dynamic` and `System.ValueType` to any *non_nullable_value_type*, and from any *interface_type* to any *non_nullable_value_type* that implements the *interface_type*.</span></span> <span data-ttu-id="7b523-359">또한 입력 `System.Enum` boxed를 취소할 수 있습니다 *enum_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-359">Furthermore type `System.Enum` can be unboxed to any *enum_type*.</span></span>

<span data-ttu-id="7b523-360">Unboxing 변환 하기 위해 참조 형식에서 존재를 *nullable_type* 있으면 unboxing 변환 참조 형식에서 기본 *non_nullable_value_type* 의  *nullable_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-360">An unboxing conversion exists from a reference type to a *nullable_type* if an unboxing conversion exists from the reference type to the underlying *non_nullable_value_type* of the *nullable_type*.</span></span>

<span data-ttu-id="7b523-361">값 형식 `S` 에 인터페이스 형식에서 unboxing 변환 `I` 인터페이스 형식에서 unboxing 변환 있는지 `I0` 및 `I0` 에 id 변환이 `I`.</span><span class="sxs-lookup"><span data-stu-id="7b523-361">A value type `S` has an unboxing conversion from an interface type `I` if it has an unboxing conversion from an interface type `I0` and `I0` has an identity conversion to `I`.</span></span>

<span data-ttu-id="7b523-362">값 형식 `S` 에 인터페이스 형식에서 unboxing 변환 `I` 인터페이스 또는 대리자 형식에서 unboxing 변환 되었으면 `I0` 고 `I0` 변환 됩니다를 `I` 또는 `I`변형 가능은 하 `I0` ([변형 변환이](interfaces.md#variance-conversion)).</span><span class="sxs-lookup"><span data-stu-id="7b523-362">A value type `S` has an unboxing conversion from an interface type `I` if it has an unboxing conversion from an interface or delegate type `I0` and either `I0` is variance-convertible to `I` or `I` is variance-convertible to `I0` ([Variance conversion](interfaces.md#variance-conversion)).</span></span>

<span data-ttu-id="7b523-363">개체 인스턴스에 boxed 값은 첫 번째 검사 unboxing 작업으로 구성 됩니다는 지정 된 *value_type*, 다음 인스턴스에서 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-363">An unboxing operation consists of first checking that the object instance is a boxed value of the given *value_type*, and then copying the value out of the instance.</span></span> <span data-ttu-id="7b523-364">Null 참조를 unboxing을 *nullable_type* 의 null 값을 생성 합니다 *nullable_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-364">Unboxing a null reference to a *nullable_type* produces the null value of the *nullable_type*.</span></span> <span data-ttu-id="7b523-365">구조체에 연결할 수 형식에서 boxed `System.ValueType`구조체에 대 한 기본 클래스 이므로, ([상속](structs.md#inheritance)).</span><span class="sxs-lookup"><span data-stu-id="7b523-365">A struct can be unboxed from the type `System.ValueType`, since that is a base class for all structs ([Inheritance](structs.md#inheritance)).</span></span>

<span data-ttu-id="7b523-366">Unboxing 변환에 자세히 설명 되어 [Unboxing 변환](types.md#unboxing-conversions)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-366">Unboxing conversions are described further in [Unboxing conversions](types.md#unboxing-conversions).</span></span>

### <a name="explicit-dynamic-conversions"></a><span data-ttu-id="7b523-367">동적 명시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-367">Explicit dynamic conversions</span></span>

<span data-ttu-id="7b523-368">형식의 식에서 명시적 동적 변환이 존재 `dynamic` 형식으로 `T`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-368">An explicit dynamic conversion exists from an expression of type `dynamic` to any type `T`.</span></span> <span data-ttu-id="7b523-369">변환 바인딩된 동적으로 ([동적 바인딩](expressions.md#dynamic-binding))를 런타임에 식의 런타임 형식에서 변환 하는 명시적 변환을 검색 하는 것이 즉 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-369">The conversion is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)), which means that an explicit conversion will be sought at run-time from the run-time type of the expression to `T`.</span></span> <span data-ttu-id="7b523-370">변환 작업 없이 있으면 런타임 예외가 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-370">If no conversion is found, a run-time exception is thrown.</span></span>

<span data-ttu-id="7b523-371">변환의 동적 바인딩 원하지 않는 경우 식 먼저 변환할 수 `object`, 한 다음 원하는 형식.</span><span class="sxs-lookup"><span data-stu-id="7b523-371">If dynamic binding of the conversion is not desired, the expression can be first converted to `object`, and then to the desired type.</span></span>

<span data-ttu-id="7b523-372">다음 클래스 정의 되었다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-372">Assume the following class is defined:</span></span>
```csharp
class C
{
    int i;

    public C(int i) { this.i = i; }

    public static explicit operator C(string s) 
    {
        return new C(int.Parse(s));
    }
}
```

<span data-ttu-id="7b523-373">다음 예제에서는 명시적 동적 변환을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-373">The following example illustrates explicit dynamic conversions:</span></span>
```csharp
object o  = "1";
dynamic d = "2";

var c1 = (C)o; // Compiles, but explicit reference conversion fails
var c2 = (C)d; // Compiles and user defined conversion succeeds
```

<span data-ttu-id="7b523-374">변환 하는 가장 좋은 `o` 에 `C` 명시적 참조 변환이 되도록 컴파일 타임에 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-374">The best conversion of `o` to `C` is found at compile-time to be an explicit reference conversion.</span></span> <span data-ttu-id="7b523-375">때문에 런타임 시 실패 하는이 `"1"` 팩트에 있지는 `C`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-375">This fails at run-time, because `"1"` is not in fact a `C`.</span></span> <span data-ttu-id="7b523-376">그러나 변환 `d` 하 `C` 명시적 동적 변환을로 일시 중지 런타임, 여기서 사용자 정의 변수의 런타임 형식에서 변환 `d`  --  `string` -에 `C` 발견 되 면 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-376">The conversion of `d` to `C` however, as an explicit dynamic conversion, is suspended to run-time, where a user defined conversion from the run-time type of `d` -- `string` -- to `C` is found, and succeeds.</span></span>

### <a name="explicit-conversions-involving-type-parameters"></a><span data-ttu-id="7b523-377">형식 매개 변수를 포함 하는 명시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-377">Explicit conversions involving type parameters</span></span>

<span data-ttu-id="7b523-378">지정 된 형식 매개 변수는 다음과 같은 명시적 변환이 존재 `T`:</span><span class="sxs-lookup"><span data-stu-id="7b523-378">The following explicit conversions exist for a given type parameter `T`:</span></span>

*  <span data-ttu-id="7b523-379">유효한 기본 클래스에서 `C` 의 `T` 하 `T` 의 모든 기본 클래스에서 `C` 에 `T`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-379">From the effective base class `C` of `T` to `T` and from any base class of `C` to `T`.</span></span> <span data-ttu-id="7b523-380">에 런타임 경우 `T` 값 형식이 변환 unboxing 변환으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-380">At run-time, if `T` is a value type, the conversion is executed as an unboxing conversion.</span></span> <span data-ttu-id="7b523-381">그렇지 않으면 변환이 명시적 참조 변환이 또는 id 변환을 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-381">Otherwise, the conversion is executed as an explicit reference conversion or identity conversion.</span></span>
*  <span data-ttu-id="7b523-382">모든 인터페이스 형식에서 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-382">From any interface type to `T`.</span></span> <span data-ttu-id="7b523-383">에 런타임 경우 `T` 값 형식이 변환 unboxing 변환으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-383">At run-time, if `T` is a value type, the conversion is executed as an unboxing conversion.</span></span> <span data-ttu-id="7b523-384">그렇지 않으면 변환이 명시적 참조 변환이 또는 id 변환을 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-384">Otherwise, the conversion is executed as an explicit reference conversion or identity conversion.</span></span>
*  <span data-ttu-id="7b523-385">`T` 하나로 *interface_type* `I` 아직 없는 암시적 변환이 제공 `T` 에 `I`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-385">From `T` to any *interface_type* `I` provided there is not already an implicit conversion from `T` to `I`.</span></span> <span data-ttu-id="7b523-386">에 런타임 경우 `T` 값 형식이 변환 뒤에 변환 하는 명시적 참조 변환을 boxing 변환으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-386">At run-time, if `T` is a value type, the conversion is executed as a boxing conversion followed by an explicit reference conversion.</span></span> <span data-ttu-id="7b523-387">그렇지 않으면 변환이 명시적 참조 변환이 또는 id 변환을 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-387">Otherwise, the conversion is executed as an explicit reference conversion or identity conversion.</span></span>
*  <span data-ttu-id="7b523-388">형식 매개 변수에서 `U` 하 `T`제공 `T` 에 따라 달라 집니다 `U` ([형식 매개 변수 제약 조건](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="7b523-388">From a type parameter `U` to `T`, provided `T` depends on `U` ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span> <span data-ttu-id="7b523-389">런타임 경우 at `U` 이 값 형식이 면 `T` 및 `U` 반드시 동일한 형식이 고 변환이 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-389">At run-time, if `U` is a value type, then `T` and `U` are necessarily the same type and no conversion is performed.</span></span> <span data-ttu-id="7b523-390">그렇지 않은 경우, `T` 값 형식이 변환 unboxing 변환으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-390">Otherwise, if `T` is a value type, the conversion is executed as an unboxing conversion.</span></span> <span data-ttu-id="7b523-391">그렇지 않으면 변환이 명시적 참조 변환이 또는 id 변환을 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-391">Otherwise, the conversion is executed as an explicit reference conversion or identity conversion.</span></span>

<span data-ttu-id="7b523-392">하는 경우 `T` 는 참조 형식으로 알려진, 위의 변환은 모든 변환으로 분류 됩니다 명시적 참조 ([명시적 참조 변환을](conversions.md#explicit-reference-conversions)).</span><span class="sxs-lookup"><span data-stu-id="7b523-392">If `T` is known to be a reference type, the conversions above are all classified as explicit reference conversions ([Explicit reference conversions](conversions.md#explicit-reference-conversions)).</span></span> <span data-ttu-id="7b523-393">하는 경우 `T` 는 참조 형식으로 알 수 없는 위의 변환은 unboxing 변환으로 분류 됩니다 ([Unboxing 변환](conversions.md#unboxing-conversions)).</span><span class="sxs-lookup"><span data-stu-id="7b523-393">If `T` is not known to be a reference type, the conversions above are classified as unboxing conversions ([Unboxing conversions](conversions.md#unboxing-conversions)).</span></span>

<span data-ttu-id="7b523-394">위의 규칙을 허용 하지 않습니다 인터페이스가 아닌 형식에 제한 되지 않은 형식 매개 변수에서 직접 명시적 변환 다르다는 점에 놀라실 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-394">The above rules do not permit a direct explicit conversion from an unconstrained type parameter to a non-interface type, which might be surprising.</span></span> <span data-ttu-id="7b523-395">이 규칙에 대 한 이유는 혼동을 방지 하기를 이러한 변환이 명확한의 의미 체계를 확인 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-395">The reason for this rule is to prevent confusion and make the semantics of such conversions clear.</span></span> <span data-ttu-id="7b523-396">예를 들어, 다음 선언을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="7b523-396">For example, consider the following declaration:</span></span>
```csharp
class X<T>
{
    public static long F(T t) {
        return (long)t;                // Error 
    }
}
```

<span data-ttu-id="7b523-397">경우 직접 명시적 변환 `t` 하 `int` 쉽게 예상할 수 허용 되는 `X<int>.F(7)` 반환 `7L`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-397">If the direct explicit conversion of `t` to `int` were permitted, one might easily expect that `X<int>.F(7)` would return `7L`.</span></span> <span data-ttu-id="7b523-398">그러나 것 하지 형식 바인딩 시간에 숫자 것으로 알려진 경우에 표준 숫자 변환 간주 되기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-398">However, it would not, because the standard numeric conversions are only considered when the types are known to be numeric at binding-time.</span></span> <span data-ttu-id="7b523-399">의미 체계를 확인 하기 위해 명확 하 고 위의 예제에서는 대신 써야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-399">In order to make the semantics clear, the above example must instead be written:</span></span>
```csharp
class X<T>
{
    public static long F(T t) {
        return (long)(object)t;        // Ok, but will only work when T is long
    }
}
```

<span data-ttu-id="7b523-400">이 코드는 컴파일되지 이제 실행 되지만 `X<int>.F(7)` boxed 이후 실행 시 예외를 throw 한 다음는 `int` 로 바로 변환 될 수 없습니다는 `long`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-400">This code will now compile but executing `X<int>.F(7)` would then throw an exception at run-time, since a boxed `int` cannot be converted directly to a `long`.</span></span>

### <a name="user-defined-explicit-conversions"></a><span data-ttu-id="7b523-401">사용자 정의 명시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-401">User-defined explicit conversions</span></span>

<span data-ttu-id="7b523-402">사용자 정의 명시적 변환 선택적 표준 명시적 변환이 다른 선택적 표준 명시적 변환 뒤에 사용자 정의 된 암시적 또는 명시적 변환 연산자를 실행 하 여 다음 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-402">A user-defined explicit conversion consists of an optional standard explicit conversion, followed by execution of a user-defined implicit or explicit conversion operator, followed by another optional standard explicit conversion.</span></span> <span data-ttu-id="7b523-403">사용자 정의 명시적 변환 평가 대 한 정확한 규칙에 설명 되어 있습니다 [사용자 정의 명시적 변환 처리](conversions.md#processing-of-user-defined-explicit-conversions)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-403">The exact rules for evaluating user-defined explicit conversions are described in [Processing of user-defined explicit conversions](conversions.md#processing-of-user-defined-explicit-conversions).</span></span>

## <a name="standard-conversions"></a><span data-ttu-id="7b523-404">표준 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-404">Standard conversions</span></span>

<span data-ttu-id="7b523-405">표준 변환은 사용자 정의 변환의 일부로 발생할 수 있는 이러한 미리 정의 된 변환입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-405">The standard conversions are those pre-defined conversions that can occur as part of a user-defined conversion.</span></span>

### <a name="standard-implicit-conversions"></a><span data-ttu-id="7b523-406">표준 암시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-406">Standard implicit conversions</span></span>

<span data-ttu-id="7b523-407">다음과 같은 암시적 변환이 표준 암시적 변환으로 분류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-407">The following implicit conversions are classified as standard implicit conversions:</span></span>

*  <span data-ttu-id="7b523-408">Identity 변환 ([Id 변환을](conversions.md#identity-conversion))</span><span class="sxs-lookup"><span data-stu-id="7b523-408">Identity conversions ([Identity conversion](conversions.md#identity-conversion))</span></span>
*  <span data-ttu-id="7b523-409">암시적 숫자 변환 ([암시적 숫자 변환](conversions.md#implicit-numeric-conversions))</span><span class="sxs-lookup"><span data-stu-id="7b523-409">Implicit numeric conversions ([Implicit numeric conversions](conversions.md#implicit-numeric-conversions))</span></span>
*  <span data-ttu-id="7b523-410">암시적 nullable 변환 ([암시적 nullable 변환](conversions.md#implicit-nullable-conversions))</span><span class="sxs-lookup"><span data-stu-id="7b523-410">Implicit nullable conversions ([Implicit nullable conversions](conversions.md#implicit-nullable-conversions))</span></span>
*  <span data-ttu-id="7b523-411">암시적 참조 변환 ([암시적 참조 변환](conversions.md#implicit-reference-conversions))</span><span class="sxs-lookup"><span data-stu-id="7b523-411">Implicit reference conversions ([Implicit reference conversions](conversions.md#implicit-reference-conversions))</span></span>
*  <span data-ttu-id="7b523-412">Boxing 변환 ([Boxing 변환](conversions.md#boxing-conversions))</span><span class="sxs-lookup"><span data-stu-id="7b523-412">Boxing conversions ([Boxing conversions](conversions.md#boxing-conversions))</span></span>
*  <span data-ttu-id="7b523-413">암시적 상수 식 변환 ([암시적 동적 변환을](conversions.md#implicit-dynamic-conversions))</span><span class="sxs-lookup"><span data-stu-id="7b523-413">Implicit constant expression conversions ([Implicit dynamic conversions](conversions.md#implicit-dynamic-conversions))</span></span>
*  <span data-ttu-id="7b523-414">형식 매개 변수를 포함 하는 암시적 변환은 ([형식 매개 변수를 포함 하는 암시적 변환은](conversions.md#implicit-conversions-involving-type-parameters))</span><span class="sxs-lookup"><span data-stu-id="7b523-414">Implicit conversions involving type parameters ([Implicit conversions involving type parameters](conversions.md#implicit-conversions-involving-type-parameters))</span></span>

<span data-ttu-id="7b523-415">특히 표준 암시적 변환이 암시적 변환을 사용자 정의 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-415">The standard implicit conversions specifically exclude user-defined implicit conversions.</span></span>

### <a name="standard-explicit-conversions"></a><span data-ttu-id="7b523-416">표준 명시적 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-416">Standard explicit conversions</span></span>

<span data-ttu-id="7b523-417">표준 명시적 변환은 모든 표준 암시적 변환 및 반대 표준 암시적 변환이 존재 하는 명시적 변환의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-417">The standard explicit conversions are all standard implicit conversions plus the subset of the explicit conversions for which an opposite standard implicit conversion exists.</span></span> <span data-ttu-id="7b523-418">즉, 표준 암시적 변환이 있는 경우 형식에서 `A` 형식으로 `B`, 형식에서 표준 명시적 변환이 존재 합니다 `A` 형식으로 `B` 형식에서 `B` 형식으로 `A`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-418">In other words, if a standard implicit conversion exists from a type `A` to a type `B`, then a standard explicit conversion exists from type `A` to type `B` and from type `B` to type `A`.</span></span>

## <a name="user-defined-conversions"></a><span data-ttu-id="7b523-419">사용자 정의 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-419">User-defined conversions</span></span>

<span data-ttu-id="7b523-420">C# 확대 하 여 미리 정의 된 암시적 변환과 명시적 변환에서는 ***사용자 정의 변환은***합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-420">C# allows the pre-defined implicit and explicit conversions to be augmented by ***user-defined conversions***.</span></span> <span data-ttu-id="7b523-421">변환 연산자를 선언 하 여 도입 된 사용자 정의 변환 ([변환 연산자](classes.md#conversion-operators)) 클래스 및 구조체 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-421">User-defined conversions are introduced by declaring conversion operators ([Conversion operators](classes.md#conversion-operators)) in class and struct types.</span></span>

### <a name="permitted-user-defined-conversions"></a><span data-ttu-id="7b523-422">사용자 정의 변환은 허용</span><span class="sxs-lookup"><span data-stu-id="7b523-422">Permitted user-defined conversions</span></span>

<span data-ttu-id="7b523-423">C#만 선언 될 특정 사용자 정의 변환은 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-423">C# permits only certain user-defined conversions to be declared.</span></span> <span data-ttu-id="7b523-424">특히 변환 하는 기존 암시적 또는 명시적 변환을 다시 정의할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-424">In particular, it is not possible to redefine an already existing implicit or explicit conversion.</span></span>

<span data-ttu-id="7b523-425">지정 된 소스 형식에 대 한 `S` 대상 유형 및 `T`이면 `S` 또는 `T` nullable 형식 수 있도록 `S0` 및 `T0` 그렇지 않으면 해당 기본 형식 참조 `S0` 및 `T0` 됩니다 같음 `S` 고 `T` 각각.</span><span class="sxs-lookup"><span data-stu-id="7b523-425">For a given source type `S` and target type `T`, if `S` or `T` are nullable types, let `S0` and `T0` refer to their underlying types, otherwise `S0` and `T0` are equal to `S` and `T` respectively.</span></span> <span data-ttu-id="7b523-426">클래스 또는 구조체를 선언할 수 원본 형식에서 변환 `S` 대상 형식으로 `T` 다음 모두 만족 하는 경우에:</span><span class="sxs-lookup"><span data-stu-id="7b523-426">A class or struct is permitted to declare a conversion from a source type `S` to a target type `T` only if all of the following are true:</span></span>

*  <span data-ttu-id="7b523-427">`S0` 및 `T0` 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-427">`S0` and `T0` are different types.</span></span>
*  <span data-ttu-id="7b523-428">중 하나 `S0` 또는 `T0` 는 연산자 선언이 발생 하는 클래스 또는 구조체 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-428">Either `S0` or `T0` is the class or struct type in which the operator declaration takes place.</span></span>
*  <span data-ttu-id="7b523-429">모두 `S0` 나 `T0` 되는 *interface_type*합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-429">Neither `S0` nor `T0` is an *interface_type*.</span></span>
*  <span data-ttu-id="7b523-430">사용자 정의 변환을 제외 하 고 변환에서 존재 하지 않습니다 `S` 하 `T` 주고 `T` 에 `S`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-430">Excluding user-defined conversions, a conversion does not exist from `S` to `T` or from `T` to `S`.</span></span>

<span data-ttu-id="7b523-431">사용자 정의 변환에 적용 되는 제한 사항 설명에 대 한 자세한 [변환 연산자](classes.md#conversion-operators)합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-431">The restrictions that apply to user-defined conversions are discussed further in [Conversion operators](classes.md#conversion-operators).</span></span>

### <a name="lifted-conversion-operators"></a><span data-ttu-id="7b523-432">리프트 변환 연산자</span><span class="sxs-lookup"><span data-stu-id="7b523-432">Lifted conversion operators</span></span>

<span data-ttu-id="7b523-433">Nullable이 아닌 값 형식에서 변환 하는 사용자 정의 변환 연산자를 지정 된 `S` nullable이 아닌 값 형식 `T`, ***변환 연산자를 리프트*** 에서 변환 하는 존재 `S?` 에`T?`.</span><span class="sxs-lookup"><span data-stu-id="7b523-433">Given a user-defined conversion operator that converts from a non-nullable value type `S` to a non-nullable value type `T`, a ***lifted conversion operator*** exists that converts from `S?` to `T?`.</span></span> <span data-ttu-id="7b523-434">이 리프트 변환 연산자에서 래핑 해제를 수행 `S?` 에 `S` 뒤에 사용자 정의 변환 `S` 에 `T` 뒤에에서 배치 `T` 에 `T?`점을 제외 하 고, null 소중한 `S?` 값을 null로 직접 변환 `T?`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-434">This lifted conversion operator performs an unwrapping from `S?` to `S` followed by the user-defined conversion from `S` to `T` followed by a wrapping from `T` to `T?`, except that a null valued `S?` converts directly to a null valued `T?`.</span></span>

<span data-ttu-id="7b523-435">리프트 변환 연산자에 해당 기본 사용자 정의 변환 연산자와 같은 암시적 또는 명시적 분류 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-435">A lifted conversion operator has the same implicit or explicit classification as its underlying user-defined conversion operator.</span></span> <span data-ttu-id="7b523-436">"사용자 정의 변환" 사용을 적용할 용어 사용자 정의 및 변환 연산자를 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-436">The term "user-defined conversion" applies to the use of both user-defined and lifted conversion operators.</span></span>

### <a name="evaluation-of-user-defined-conversions"></a><span data-ttu-id="7b523-437">사용자 정의 변환에 대 한 평가</span><span class="sxs-lookup"><span data-stu-id="7b523-437">Evaluation of user-defined conversions</span></span>

<span data-ttu-id="7b523-438">사용자 정의 변환이 호출 해당 형식에서 값을 변환 합니다 ***원본 유형***를 다른 형식으로 호출 합니다 ***대상 유형***.</span><span class="sxs-lookup"><span data-stu-id="7b523-438">A user-defined conversion converts a value from its type, called the ***source type***, to another type, called the ***target type***.</span></span> <span data-ttu-id="7b523-439">사용자 정의 변환의 평가 센터 찾기에는 ***가장 구체적인*** 특정 소스 및 대상 형식에 대 한 사용자 정의 변환 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-439">Evaluation of a user-defined conversion centers on finding the ***most specific*** user-defined conversion operator for the particular source and target types.</span></span> <span data-ttu-id="7b523-440">이 결정 여러 단계로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-440">This determination is broken into several steps:</span></span>

*  <span data-ttu-id="7b523-441">클래스 및 사용자 정의 변환 연산자 고려해 야 하는 구조체의 집합을 찾기.</span><span class="sxs-lookup"><span data-stu-id="7b523-441">Finding the set of classes and structs from which user-defined conversion operators will be considered.</span></span> <span data-ttu-id="7b523-442">이 집합의 소스 형식 및 해당 기본 클래스 및 대상 형식과 해당 기본 클래스 (클래스 및 구조체는 사용자 정의 연산자를 선언할 수 있습니다 하 고 비 클래스 형식에 기본 클래스가 없고 있는 암시적 가정)으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-442">This set consists of the source type and its base classes and the target type and its base classes (with the implicit assumptions that only classes and structs can declare user-defined operators, and that non-class types have no base classes).</span></span> <span data-ttu-id="7b523-443">원본 또는 대상 유형이 경우이 단계를 위해 한 *nullable_type*등의 기본 형식 대신 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-443">For the purposes of this step, if either the source or target type is a *nullable_type*, their underlying type is used instead.</span></span>
*  <span data-ttu-id="7b523-444">형식의 해당 집합에서 결정 하는 사용자 정의 변환 연산자를 리프트 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-444">From that set of types, determining which user-defined and lifted conversion operators are applicable.</span></span> <span data-ttu-id="7b523-445">변환 연산자를 적용 하기 위해 있어야 표준 변환을 수행할 수 있습니다 ([표준 변환](conversions.md#standard-conversions)) 피연산자 원본 형식에서 연산자 및 해당 형식의 표준 변환을 수행할 수 있어야 대상 형식으로 연산자의 결과 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-445">For a conversion operator to be applicable, it must be possible to perform a standard conversion ([Standard conversions](conversions.md#standard-conversions)) from the source type to the operand type of the operator, and it must be possible to perform a standard conversion from the result type of the operator to the target type.</span></span>
*  <span data-ttu-id="7b523-446">해당 사용자 정의 연산자의 집합에서 명확 하 게 가장 관련 된 어떤 운영자를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-446">From the set of applicable user-defined operators, determining which operator is unambiguously the most specific.</span></span> <span data-ttu-id="7b523-447">일반적인 측면에서 가장 구체적인 연산자는 피연산자 형식이 소스 형식으로 "가장 가까운" 이며 결과 형식이 대상 형식으로 "가장 가까운" 연산자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-447">In general terms, the most specific operator is the operator whose operand type is "closest" to the source type and whose result type is "closest" to the target type.</span></span> <span data-ttu-id="7b523-448">사용자 정의 변환 연산자는 리프트 변환 연산자 보다 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-448">User-defined conversion operators are preferred over lifted conversion operators.</span></span> <span data-ttu-id="7b523-449">가장 구체적인 사용자 정의 변환 연산자를 설정 하는 것에 대 한 정확한 규칙은 다음 섹션에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-449">The exact rules for establishing the most specific user-defined conversion operator are defined in the following sections.</span></span>

<span data-ttu-id="7b523-450">가장 구체적인 사용자 정의 변환 연산자를 식별 한 후 사용자 정의 변환의 실제 실행에는 최대 세 가지 단계가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-450">Once a most specific user-defined conversion operator has been identified, the actual execution of the user-defined conversion involves up to three steps:</span></span>

*  <span data-ttu-id="7b523-451">먼저 필요한 경우 원본 유형에 서 또는 리프트 된 사용자 정의 변환 연산자의 피연산자 형식으로 변환 하는 표준 변환이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-451">First, if required, performing a standard conversion from the source type to the operand type of the user-defined or lifted conversion operator.</span></span>
*  <span data-ttu-id="7b523-452">다음으로 변환 하는 데 사용자 정의 또는 리프트 변환 연산자를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-452">Next, invoking the user-defined or lifted conversion operator to perform the conversion.</span></span>
*  <span data-ttu-id="7b523-453">마지막으로, 필요한 경우에 대상 형식으로 변환의 사용자 정의 또는 리프트 된 연산자의 결과 형식은의 표준 변환이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-453">Finally, if required, performing a standard conversion from the result type of the user-defined or lifted conversion operator to the target type.</span></span>

<span data-ttu-id="7b523-454">사용자 정의 변환 되지의 평가 둘 이상의 사용자 정의 또는 리프트 변환 연산자에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-454">Evaluation of a user-defined conversion never involves more than one user-defined or lifted conversion operator.</span></span> <span data-ttu-id="7b523-455">즉, 형식 변환 `S` 형식으로 `T` 에서 사용자 정의 변환을 실행 되지 `S` 에 `X` 에서 사용자 정의 변환을 실행 하 고 `X` 를 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-455">In other words, a conversion from type `S` to type `T` will never first execute a user-defined conversion from `S` to `X` and then execute a user-defined conversion from `X` to `T`.</span></span>

<span data-ttu-id="7b523-456">사용자 정의 된 암시적 또는 명시적 변환에 대 한 평가의 정확한 정의 다음 섹션에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-456">Exact definitions of evaluation of user-defined implicit or explicit conversions are given in the following sections.</span></span> <span data-ttu-id="7b523-457">정의 사용 하면 다음과 같은 용어가 사용:</span><span class="sxs-lookup"><span data-stu-id="7b523-457">The definitions make use of the following terms:</span></span>

*  <span data-ttu-id="7b523-458">표준 암시적 변환 경우 ([표준 암시적 변환이](conversions.md#standard-implicit-conversions)) 형식에서 존재 `A` 형식으로 `B`, 모두 및 `A` 나 `B` 는 *interface_type*s, 한 다음 `A` 이라고 ***에 의해 포함 된*** `B`, 및 `B` 이라고 ***encompass*** `A`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-458">If a standard implicit conversion ([Standard implicit conversions](conversions.md#standard-implicit-conversions)) exists from a type `A` to a type `B`, and if neither `A` nor `B` are *interface_type*s, then `A` is said to be ***encompassed by*** `B`, and `B` is said to ***encompass*** `A`.</span></span>
*  <span data-ttu-id="7b523-459">합니다 ***최상위 형식*** 형식 집합이 집합의 다른 모든 형식을 포함 하는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-459">The ***most encompassing type*** in a set of types is the one type that encompasses all other types in the set.</span></span> <span data-ttu-id="7b523-460">다른 모든 형식을 포함 하는 단일 형식이 없는, 하는 경우 집합에 최상위 형식이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-460">If no single type encompasses all other types, then the set has no most encompassing type.</span></span> <span data-ttu-id="7b523-461">직관적인 측면에서 최상위 형식은 집합의 "큰" 유형에-는 각각 다른 형식의 암시적으로 변환할 수는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-461">In more intuitive terms, the most encompassing type is the "largest" type in the set—the one type to which each of the other types can be implicitly converted.</span></span>
*  <span data-ttu-id="7b523-462">합니다 ***형식이 포함 된 가장*** 형식 집합이 집합의 다른 모든 형식으로 포함 되는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-462">The ***most encompassed type*** in a set of types is the one type that is encompassed by all other types in the set.</span></span> <span data-ttu-id="7b523-463">단일 형식이 없는 다른 모든 형식으로 롤포워드되지 않았습니다, 경우 집합에는 형식 가장 하지 않습니다 포함 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-463">If no single type is encompassed by all other types, then the set has no most encompassed type.</span></span> <span data-ttu-id="7b523-464">직관적인 측면에서 최하위 형식은 집합의 "작은" 형식-각 다른 형식에 암시적으로 변환할 수는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-464">In more intuitive terms, the most encompassed type is the "smallest" type in the set—the one type that can be implicitly converted to each of the other types.</span></span>

### <a name="processing-of-user-defined-implicit-conversions"></a><span data-ttu-id="7b523-465">암시적 사용자 정의 변환 처리</span><span class="sxs-lookup"><span data-stu-id="7b523-465">Processing of user-defined implicit conversions</span></span>

<span data-ttu-id="7b523-466">형식에서 사용자 정의 된 암시적 변환이 `S` 형식으로 `T` 다음과 같이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-466">A user-defined implicit conversion from type `S` to type `T` is processed as follows:</span></span>

*  <span data-ttu-id="7b523-467">형식을 확인할 `S0` 고 `T0`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-467">Determine the types `S0` and `T0`.</span></span> <span data-ttu-id="7b523-468">하는 경우 `S` 또는 `T` nullable 형식 `S0` 하 고 `T0` 가 해당 기본 형식인 경우이 고, 그렇지 `S0` 및 `T0` 같은지 `S` 및 `T` 각각.</span><span class="sxs-lookup"><span data-stu-id="7b523-468">If `S` or `T` are nullable types, `S0` and `T0` are their underlying types, otherwise `S0` and `T0` are equal to `S` and `T` respectively.</span></span>
*  <span data-ttu-id="7b523-469">형식의 집합을 찾을 `D`는 사용자 정의 변환 연산자 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-469">Find the set of types, `D`, from which user-defined conversion operators will be considered.</span></span> <span data-ttu-id="7b523-470">이 집합으로 구성 됩니다 `S0` (하는 경우 `S0` 는 클래스 또는 구조체)의 기본 클래스 `S0` (경우 `S0` 클래스인), 및 `T0` (경우 `T0` 클래스 또는 구조체).</span><span class="sxs-lookup"><span data-stu-id="7b523-470">This set consists of `S0` (if `S0` is a class or struct), the base classes of `S0` (if `S0` is a class), and `T0` (if `T0` is a class or struct).</span></span>
*  <span data-ttu-id="7b523-471">해당 사용자 정의 및 리프트 변환 연산자 집합을 찾을 `U`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-471">Find the set of applicable user-defined and lifted conversion operators, `U`.</span></span> <span data-ttu-id="7b523-472">이 구성 된이 집합을 사용자 정의 및 리프트 된 암시적 변환 연산자는 클래스 또는 구조체 선언 `D` 포괄 하는 형식에서 변환 하는 `S` 에 의해 포함 된 형식으로 `T`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-472">This set consists of the user-defined and lifted implicit conversion operators declared by the classes or structs in `D` that convert from a type encompassing `S` to a type encompassed by `T`.</span></span> <span data-ttu-id="7b523-473">경우 `U` 는 비어 있는 경우 변환이 정의 되지 않으며 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-473">If `U` is empty, the conversion is undefined and a compile-time error occurs.</span></span>
*  <span data-ttu-id="7b523-474">가장 구체적인 원본 유형을 찾습니다 `SX`에서 연산자의 `U`:</span><span class="sxs-lookup"><span data-stu-id="7b523-474">Find the most specific source type, `SX`, of the operators in `U`:</span></span>
    * <span data-ttu-id="7b523-475">연산자 중 하나가 되 면 `U` 에서 변환 `S`, 한 다음 `SX` 는 `S`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-475">If any of the operators in `U` convert from `S`, then `SX` is `S`.</span></span>
    * <span data-ttu-id="7b523-476">그렇지 않으면 `SX` 원본 형식에서 연산자의 결합 된 집합의 최하위 형식인 `U`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-476">Otherwise, `SX` is the most encompassed type in the combined set of source types of the operators in `U`.</span></span> <span data-ttu-id="7b523-477">가장 하나만 포함 하는 경우에 형식을 찾을 수 없는 한 변환이 모호 하 고 컴파일 타임 오류가 발생 하는 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-477">If exactly one most encompassed type cannot be found, then the conversion is ambiguous and a compile-time error occurs.</span></span>
*  <span data-ttu-id="7b523-478">가장 구체적인 대상 형식과 찾을 `TX`에서 연산자의 `U`:</span><span class="sxs-lookup"><span data-stu-id="7b523-478">Find the most specific target type, `TX`, of the operators in `U`:</span></span>
    * <span data-ttu-id="7b523-479">연산자 중 하나가 되 면 `U` 변환할 `T`, 한 다음 `TX` 는 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-479">If any of the operators in `U` convert to `T`, then `TX` is `T`.</span></span>
    * <span data-ttu-id="7b523-480">그렇지 않으면 `TX` 대상 유형의에서 연산자의 조합된 된 집합의 최상위 형식인 `U`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-480">Otherwise, `TX` is the most encompassing type in the combined set of target types of the operators in `U`.</span></span> <span data-ttu-id="7b523-481">정확히 하나의 최상위 형식 찾을 수 없는 경우 다음 변환이 모호 합니다. 및 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-481">If exactly one most encompassing type cannot be found, then the conversion is ambiguous and a compile-time error occurs.</span></span>
*  <span data-ttu-id="7b523-482">가장 구체적인 변환 연산자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-482">Find the most specific conversion operator:</span></span>
    * <span data-ttu-id="7b523-483">하는 경우 `U` 로 변환 하는 사용자 정의 변환 연산자를 하나만 포함 `SX` 에 `TX`, 가장 구체적인 변환 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-483">If `U` contains exactly one user-defined conversion operator that converts from `SX` to `TX`, then this is the most specific conversion operator.</span></span>
    * <span data-ttu-id="7b523-484">그렇지 않고 `U` 로 변환 하는 정확히 하나의 리프트 변환 연산자를 포함 `SX` 에 `TX`, 가장 구체적인 변환 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-484">Otherwise, if `U` contains exactly one lifted conversion operator that converts from `SX` to `TX`, then this is the most specific conversion operator.</span></span>
    * <span data-ttu-id="7b523-485">이 고, 그렇지 변환이 모호 하 고 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-485">Otherwise, the conversion is ambiguous and a compile-time error occurs.</span></span>
*  <span data-ttu-id="7b523-486">마지막으로 변환이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-486">Finally, apply the conversion:</span></span>
    * <span data-ttu-id="7b523-487">하는 경우 `S` 아닙니다 `SX`의 표준 암시적 변환이 다음 `S` 에 `SX` 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-487">If `S` is not `SX`, then a standard implicit conversion from `S` to `SX` is performed.</span></span>
    * <span data-ttu-id="7b523-488">변환할 가장 구체적인 변환 연산자가 호출 `SX` 에 `TX`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-488">The most specific conversion operator is invoked to convert from `SX` to `TX`.</span></span>
    * <span data-ttu-id="7b523-489">하는 경우 `TX` 아닙니다 `T`의 표준 암시적 변환이 다음 `TX` 에 `T` 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-489">If `TX` is not `T`, then a standard implicit conversion from `TX` to `T` is performed.</span></span>

### <a name="processing-of-user-defined-explicit-conversions"></a><span data-ttu-id="7b523-490">사용자 정의 명시적 변환 처리</span><span class="sxs-lookup"><span data-stu-id="7b523-490">Processing of user-defined explicit conversions</span></span>

<span data-ttu-id="7b523-491">형식에서 사용자 정의 명시적 변환 `S` 형식으로 `T` 다음과 같이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-491">A user-defined explicit conversion from type `S` to type `T` is processed as follows:</span></span>

*  <span data-ttu-id="7b523-492">형식을 확인할 `S0` 고 `T0`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-492">Determine the types `S0` and `T0`.</span></span> <span data-ttu-id="7b523-493">하는 경우 `S` 또는 `T` nullable 형식 `S0` 하 고 `T0` 가 해당 기본 형식인 경우이 고, 그렇지 `S0` 및 `T0` 같은지 `S` 및 `T` 각각.</span><span class="sxs-lookup"><span data-stu-id="7b523-493">If `S` or `T` are nullable types, `S0` and `T0` are their underlying types, otherwise `S0` and `T0` are equal to `S` and `T` respectively.</span></span>
*  <span data-ttu-id="7b523-494">형식의 집합을 찾을 `D`는 사용자 정의 변환 연산자 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-494">Find the set of types, `D`, from which user-defined conversion operators will be considered.</span></span> <span data-ttu-id="7b523-495">이 집합으로 구성 됩니다 `S0` (하는 경우 `S0` 는 클래스 또는 구조체)의 기본 클래스 `S0` (경우 `S0` 클래스인), `T0` (경우 `T0` 클래스 또는 구조체), 및의 기본 클래스 `T0` (경우 `T0`는 클래스).</span><span class="sxs-lookup"><span data-stu-id="7b523-495">This set consists of `S0` (if `S0` is a class or struct), the base classes of `S0` (if `S0` is a class), `T0` (if `T0` is a class or struct), and the base classes of `T0` (if `T0` is a class).</span></span>
*  <span data-ttu-id="7b523-496">해당 사용자 정의 및 리프트 변환 연산자 집합을 찾을 `U`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-496">Find the set of applicable user-defined and lifted conversion operators, `U`.</span></span> <span data-ttu-id="7b523-497">이 집합은 사용자 정의 및 구성 리프트 된 암시적 또는 명시적 변환 연산자는 클래스 또는 구조체 선언 `D` 포괄 하는 형식에서 변환 하는 하거나에 의해 포함 된 `S` 에의해포함된클래스나형식`T`.</span><span class="sxs-lookup"><span data-stu-id="7b523-497">This set consists of the user-defined and lifted implicit or explicit conversion operators declared by the classes or structs in `D` that convert from a type encompassing or encompassed by `S` to a type encompassing or encompassed by `T`.</span></span> <span data-ttu-id="7b523-498">경우 `U` 는 비어 있는 경우 변환이 정의 되지 않으며 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-498">If `U` is empty, the conversion is undefined and a compile-time error occurs.</span></span>
*  <span data-ttu-id="7b523-499">가장 구체적인 원본 유형을 찾습니다 `SX`에서 연산자의 `U`:</span><span class="sxs-lookup"><span data-stu-id="7b523-499">Find the most specific source type, `SX`, of the operators in `U`:</span></span>
    * <span data-ttu-id="7b523-500">연산자 중 하나가 되 면 `U` 에서 변환 `S`, 한 다음 `SX` 는 `S`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-500">If any of the operators in `U` convert from `S`, then `SX` is `S`.</span></span>
    * <span data-ttu-id="7b523-501">그렇지 않으면 연산자 중 하나 `U` 을 포함 하는 형식에서 변환 `S`, 다음 `SX` 원본 유형의 해당 연산자의 조합된 된 집합의 최하위 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-501">Otherwise, if any of the operators in `U` convert from types that encompass `S`, then `SX` is the most encompassed type in the combined set of source types of those operators.</span></span> <span data-ttu-id="7b523-502">없는 대부분 포함 하는 경우에 형식을 찾을 수를 한 변환이 모호 하 고 컴파일 타임 오류가 발생 하는 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-502">If no most encompassed type can be found, then the conversion is ambiguous and a compile-time error occurs.</span></span>
    * <span data-ttu-id="7b523-503">그렇지 않으면 `SX` 결합된 된 집합에 있는 연산자의 원본 유형 중에서 최상위 형식인 `U`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-503">Otherwise, `SX` is the most encompassing type in the combined set of source types of the operators in `U`.</span></span> <span data-ttu-id="7b523-504">정확히 하나의 최상위 형식 찾을 수 없는 경우 다음 변환이 모호 합니다. 및 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-504">If exactly one most encompassing type cannot be found, then the conversion is ambiguous and a compile-time error occurs.</span></span>
*  <span data-ttu-id="7b523-505">가장 구체적인 대상 형식과 찾을 `TX`에서 연산자의 `U`:</span><span class="sxs-lookup"><span data-stu-id="7b523-505">Find the most specific target type, `TX`, of the operators in `U`:</span></span>
    * <span data-ttu-id="7b523-506">연산자 중 하나가 되 면 `U` 변환할 `T`, 한 다음 `TX` 는 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-506">If any of the operators in `U` convert to `T`, then `TX` is `T`.</span></span>
    * <span data-ttu-id="7b523-507">그렇지 않으면 연산자 중 하나 `U` 하 여 포함 된 형식으로 변환 `T`, 다음 `TX` 대상 유형의 해당 연산자의 조합된 된 집합의 최상위 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-507">Otherwise, if any of the operators in `U` convert to types that are encompassed by `T`, then `TX` is the most encompassing type in the combined set of target types of those operators.</span></span> <span data-ttu-id="7b523-508">정확히 하나의 최상위 형식 찾을 수 없는 경우 다음 변환이 모호 합니다. 및 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-508">If exactly one most encompassing type cannot be found, then the conversion is ambiguous and a compile-time error occurs.</span></span>
    * <span data-ttu-id="7b523-509">그렇지 않으면 `TX` 대상 유형의에서 연산자의 조합된 된 집합의 최하위 형식인 `U`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-509">Otherwise, `TX` is the most encompassed type in the combined set of target types of the operators in `U`.</span></span> <span data-ttu-id="7b523-510">없는 대부분 포함 하는 경우에 형식을 찾을 수를 한 변환이 모호 하 고 컴파일 타임 오류가 발생 하는 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-510">If no most encompassed type can be found, then the conversion is ambiguous and a compile-time error occurs.</span></span>
*  <span data-ttu-id="7b523-511">가장 구체적인 변환 연산자를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-511">Find the most specific conversion operator:</span></span>
    * <span data-ttu-id="7b523-512">하는 경우 `U` 로 변환 하는 사용자 정의 변환 연산자를 하나만 포함 `SX` 에 `TX`, 가장 구체적인 변환 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-512">If `U` contains exactly one user-defined conversion operator that converts from `SX` to `TX`, then this is the most specific conversion operator.</span></span>
    * <span data-ttu-id="7b523-513">그렇지 않고 `U` 로 변환 하는 정확히 하나의 리프트 변환 연산자를 포함 `SX` 에 `TX`, 가장 구체적인 변환 연산자입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-513">Otherwise, if `U` contains exactly one lifted conversion operator that converts from `SX` to `TX`, then this is the most specific conversion operator.</span></span>
    * <span data-ttu-id="7b523-514">이 고, 그렇지 변환이 모호 하 고 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-514">Otherwise, the conversion is ambiguous and a compile-time error occurs.</span></span>
*  <span data-ttu-id="7b523-515">마지막으로 변환이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-515">Finally, apply the conversion:</span></span>
    * <span data-ttu-id="7b523-516">하는 경우 `S` 아닙니다 `SX`에서 표준 명시적 변환이 다음 `S` 에 `SX` 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-516">If `S` is not `SX`, then a standard explicit conversion from `S` to `SX` is performed.</span></span>
    * <span data-ttu-id="7b523-517">변환할 가장 구체적인 사용자 정의 변환 연산자가 호출 `SX` 에 `TX`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-517">The most specific user-defined conversion operator is invoked to convert from `SX` to `TX`.</span></span>
    * <span data-ttu-id="7b523-518">하는 경우 `TX` 아닙니다 `T`에서 표준 명시적 변환이 다음 `TX` 에 `T` 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-518">If `TX` is not `T`, then a standard explicit conversion from `TX` to `T` is performed.</span></span>

## <a name="anonymous-function-conversions"></a><span data-ttu-id="7b523-519">익명 함수 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-519">Anonymous function conversions</span></span>

<span data-ttu-id="7b523-520">*anonymous_method_expression* 하거나 *lambda_expression* 익명 함수로 분류 됩니다 ([익명 함수 식](expressions.md#anonymous-function-expressions)).</span><span class="sxs-lookup"><span data-stu-id="7b523-520">An *anonymous_method_expression* or *lambda_expression* is classified as an anonymous function ([Anonymous function expressions](expressions.md#anonymous-function-expressions)).</span></span> <span data-ttu-id="7b523-521">식 형식 없지만 호환 되는 대리자 형식 또는 식 트리 형식을 암시적으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-521">The expression does not have a type but can be implicitly converted to a compatible delegate type or expression tree type.</span></span> <span data-ttu-id="7b523-522">특히, 익명 함수 `F` 대리자 형식과 호환 되는 `D` 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-522">Specifically, an anonymous function `F` is compatible with a delegate type `D` provided:</span></span>

*  <span data-ttu-id="7b523-523">하는 경우 `F` 포함를 *anonymous_function_signature*, 한 다음 `D` 및 `F` 매개 변수 수가 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-523">If `F` contains an *anonymous_function_signature*, then `D` and `F` have the same number of parameters.</span></span>
*  <span data-ttu-id="7b523-524">경우 `F` 없습니다를 *anonymous_function_signature*, 한 다음 `D` 의 매개 변수가 없는으로 모든 형식의 매개 변수를 0 개 이상 있을 수 있습니다 `D` 에 `out` 매개 변수 한정자.</span><span class="sxs-lookup"><span data-stu-id="7b523-524">If `F` does not contain an *anonymous_function_signature*, then `D` may have zero or more parameters of any type, as long as no parameter of `D` has the `out` parameter modifier.</span></span>
*  <span data-ttu-id="7b523-525">하는 경우 `F` 에 명시적으로 형식화 된 매개 변수 목록이, 각 매개 변수에 `D` 에서 해당 매개 변수로 동일한 형식 및 한정자가 `F`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-525">If `F` has an explicitly typed parameter list, each parameter in `D` has the same type and modifiers as the corresponding parameter in `F`.</span></span>
*  <span data-ttu-id="7b523-526">하는 경우 `F` 는 암시적으로 형식화 된 매개 변수 목록이 `D` 아무런 `ref` 또는 `out` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-526">If `F` has an implicitly typed parameter list, `D` has no `ref` or `out` parameters.</span></span>
*  <span data-ttu-id="7b523-527">경우 본문 `F` 이 고 식 `D` 에 `void` 반환 형식 또는 `F` 는 비동기 및 `D` 반환 형식이 `Task`때 각 매개 변수에 `F` 의 형식이 지정 되며를 해당 매개 변수에 `D`, 본문 `F` 유효한 식입니다 (wrt [식을](expressions.md))으로 사용할 수 있는 *statement_expression* ([식 문은](statements.md#expression-statements)).</span><span class="sxs-lookup"><span data-stu-id="7b523-527">If the body of `F` is an expression, and either `D` has a `void` return type or `F` is async and `D` has the return type `Task`, then when each parameter of `F` is given the type of the corresponding parameter in `D`, the body of `F` is a valid expression (wrt [Expressions](expressions.md)) that would be permitted as a *statement_expression* ([Expression statements](statements.md#expression-statements)).</span></span>
*  <span data-ttu-id="7b523-528">경우 본문 `F` 이 고, 문 블록 `D` 에 `void` 반환 형식 또는 `F` 는 비동기 및 `D` 반환 형식이 `Task`때 각 매개 변수에 `F` 의 형식이 지정 되며 해당 매개 변수 `D`, 본문 `F` 유효한 문 블록 (wrt [블록](statements.md#blocks)) 않는 `return` 문에서 식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-528">If the body of `F` is a statement block, and either `D` has a `void` return type or `F` is async and `D` has the return type `Task`, then when each parameter of `F` is given the type of the corresponding parameter in `D`, the body of `F` is a valid statement block (wrt [Blocks](statements.md#blocks)) in which no `return` statement specifies an expression.</span></span>
*  <span data-ttu-id="7b523-529">경우 본문 `F` 식, 및 *중 하나* `F` 은 비동기가 아닌 및 `D` void가 아닌 반환 형식이 `T`를 *또는* `F` 는 비동기 및 `D` 반환 형식을 갖는 `Task<T>`때 각 매개 변수에 `F` 에서 해당 매개 변수의 형식이 지정 되며 `D`, 본문 `F` 유효한 식입니다 (wrt [ 식을](expressions.md))로 암시적으로 변환할 수는 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-529">If the body of `F` is an expression, and *either* `F` is non-async and `D` has a non-void return type `T`, *or* `F` is async and `D` has a return type `Task<T>`, then when each parameter of `F` is given the type of the corresponding parameter in `D`, the body of `F` is a valid expression (wrt [Expressions](expressions.md)) that is implicitly convertible to `T`.</span></span>
*  <span data-ttu-id="7b523-530">경우 본문 `F` , 문 블록은 및 *어느* `F` 은 비동기가 아닌 및 `D` void가 아닌 반환 형식이 `T`, *또는* `F` 는 비동기 및 `D` 반환 형식이 `Task<T>`때 각 매개 변수에 `F` 에서 해당 매개 변수의 형식이 지정 되며 `D`, 본문 `F` 는 유효한 문 블록 (wrt [블록 ](statements.md#blocks)) 각 연결할 수 없는 끝점을 사용 하 여 `return` 문은 암시적으로 변환할 수 있는 식을 지정 `T`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-530">If the body of `F` is a statement block, and *either* `F` is non-async and `D` has a non-void return type `T`, *or* `F` is async and `D` has a return type `Task<T>`, then when each parameter of `F` is given the type of the corresponding parameter in `D`, the body of `F` is a valid statement block (wrt [Blocks](statements.md#blocks)) with a non-reachable end point in which each `return` statement specifies an expression that is implicitly convertible to `T`.</span></span>

<span data-ttu-id="7b523-531">작업 형식에 대 한이 섹션에서는 약식 간 결함을 위해 `Task` 하 고 `Task<T>` ([비동기 함수](classes.md#async-functions)).</span><span class="sxs-lookup"><span data-stu-id="7b523-531">For the purpose of brevity, this section uses the short form for the task types `Task` and `Task<T>` ([Async functions](classes.md#async-functions)).</span></span>

<span data-ttu-id="7b523-532">람다 식 `F` 는 식 트리 형식과 호환 되는지 `Expression<D>` 하는 경우 `F` 대리자 형식과 호환 되는 `D`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-532">A lambda expression `F` is compatible with an expression tree type `Expression<D>` if `F` is compatible with the delegate type `D`.</span></span> <span data-ttu-id="7b523-533">Note 무명 메서드, 람다 식만에 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-533">Note that this does not apply to anonymous methods, only lambda expressions.</span></span>

<span data-ttu-id="7b523-534">특정 람다 식을 식 트리 형식으로 변환할 수 없습니다: 경우에 변환을 *존재*, 컴파일 시 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-534">Certain lambda expressions cannot be converted to expression tree types: Even though the conversion *exists*, it fails at compile-time.</span></span> <span data-ttu-id="7b523-535">이 경우 람다 식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-535">This is the case if the lambda expression:</span></span>

*  <span data-ttu-id="7b523-536">에 *블록* 본문</span><span class="sxs-lookup"><span data-stu-id="7b523-536">Has a *block* body</span></span>
*  <span data-ttu-id="7b523-537">단순 또는 복합 할당 연산자를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-537">Contains simple or compound assignment operators</span></span>
*  <span data-ttu-id="7b523-538">동적으로 바인딩된 식을 포함</span><span class="sxs-lookup"><span data-stu-id="7b523-538">Contains a dynamically bound expression</span></span>
*  <span data-ttu-id="7b523-539">비동기는</span><span class="sxs-lookup"><span data-stu-id="7b523-539">Is async</span></span>

<span data-ttu-id="7b523-540">이 예제에서는 제네릭 대리자 형식을 사용할 `Func<A,R>` 형식의 인수를 사용 하는 함수를 나타내는 `A` 형식의 값을 반환 하 고 `R`:</span><span class="sxs-lookup"><span data-stu-id="7b523-540">The examples that follow use a generic delegate type `Func<A,R>` which represents a function that takes an argument of type `A` and returns a value of type `R`:</span></span>
```csharp
delegate R Func<A,R>(A arg);
```

<span data-ttu-id="7b523-541">할당에서</span><span class="sxs-lookup"><span data-stu-id="7b523-541">In the assignments</span></span>
```csharp
Func<int,int> f1 = x => x + 1;                 // Ok

Func<int,double> f2 = x => x + 1;              // Ok

Func<double,int> f3 = x => x + 1;              // Error

Func<int, Task<int>> f4 = async x => x + 1;    // Ok
```
<span data-ttu-id="7b523-542">각 익명 함수의 매개 변수와 반환 형식이 익명 함수는 할당 된 변수 형식에서 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-542">the parameter and return types of each anonymous function are determined from the type of the variable to which the anonymous function is assigned.</span></span>

<span data-ttu-id="7b523-543">첫 번째 할당에서는 대리자 형식으로 익명 함수를 성공적으로 변환 `Func<int,int>` 때문에, `x` 형식이 지정 되며 `int`합니다 `x+1` 형식으로 암시적으로 변환할 수 있는 유효한 식입니다 `int`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-543">The first assignment successfully converts the anonymous function to the delegate type `Func<int,int>` because, when `x` is given type `int`, `x+1` is a valid expression that is implicitly convertible to type `int`.</span></span>

<span data-ttu-id="7b523-544">마찬가지로 두 번째 할당을 성공적으로 익명 함수를 대리자 형식 변환 `Func<int,double>` 있으므로 결과인 `x+1` (형식의 `int`) 형식으로 암시적으로 변환할 수 `double`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-544">Likewise, the second assignment successfully converts the anonymous function to the delegate type `Func<int,double>` because the result of `x+1` (of type `int`) is implicitly convertible to type `double`.</span></span>

<span data-ttu-id="7b523-545">그러나 세 번째 할당 되므로 컴파일 타임 오류가 때 `x` 형식이 지정 되며 `double`, 결과인 `x+1` (형식의 `double`) 형식으로 암시적으로 변환 되지 않습니다 `int`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-545">However, the third assignment is a compile-time error because, when `x` is given type `double`, the result of `x+1` (of type `double`) is not implicitly convertible to type `int`.</span></span>

<span data-ttu-id="7b523-546">네 번째 할당 대리자 형식으로 익명 비동기 함수를 성공적으로 변환 `Func<int, Task<int>>` 있으므로 결과인 `x+1` (형식의 `int`) 결과 유형으로 암시적으로 변환할 수 `int` 작업형식의`Task<int>`.</span><span class="sxs-lookup"><span data-stu-id="7b523-546">The fourth assignment successfully converts the anonymous async function to the delegate type `Func<int, Task<int>>` because the result of `x+1` (of type `int`) is implicitly convertible to the result type `int` of the task type `Task<int>`.</span></span>

<span data-ttu-id="7b523-547">익명 함수는 오버 로드 확인에 영향을 줄 및 형식 유추에 참여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-547">Anonymous functions may influence overload resolution, and participate in type inference.</span></span> <span data-ttu-id="7b523-548">참조 [멤버 함수](expressions.md#function-members) 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-548">See [Function members](expressions.md#function-members) for further details.</span></span>

### <a name="evaluation-of-anonymous-function-conversions-to-delegate-types"></a><span data-ttu-id="7b523-549">대리자 형식으로 익명 함수 변환에 대 한 평가</span><span class="sxs-lookup"><span data-stu-id="7b523-549">Evaluation of anonymous function conversions to delegate types</span></span>

<span data-ttu-id="7b523-550">익명 함수 이며 평가 당시 활성 상태인 캡처된 외부 변수 (비어 있을 수 있는) 집합을 참조 하는 대리자 인스턴스를 생성 하는 익명 함수는 대리자 형식으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-550">Conversion of an anonymous function to a delegate type produces a delegate instance which references the anonymous function and the (possibly empty) set of captured outer variables that are active at the time of the evaluation.</span></span> <span data-ttu-id="7b523-551">대리자를 호출 하면 익명 함수 본문 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-551">When the delegate is invoked, the body of the anonymous function is executed.</span></span> <span data-ttu-id="7b523-552">본문의 코드는 대리자가 참조 하는 캡처된 외부 변수 집합을 사용 하 여 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-552">The code in the body is executed using the set of captured outer variables referenced by the delegate.</span></span>

<span data-ttu-id="7b523-553">익명 함수에서 생성 된 대리자의 호출 목록에는 단일 항목을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-553">The invocation list of a delegate produced from an anonymous function contains a single entry.</span></span> <span data-ttu-id="7b523-554">정확한 대상 개체 및 대리자 대상 메서드의 지정 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-554">The exact target object and target method of the delegate are unspecified.</span></span> <span data-ttu-id="7b523-555">특히 지정 되지 않습니다 대리자의 대상 개체 인지 `null`, `this` 바깥쪽 함수 멤버 또는 일부 다른 개체의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-555">In particular, it is unspecified whether the target object of the delegate is `null`, the `this` value of the enclosing function member, or some other object.</span></span>

<span data-ttu-id="7b523-556">동일한 대리자 형식에 동일한 (비어 있을 수 있는) 인스턴스 집합을 캡처된 외부 변수를 사용 하 여과 의미상 동일 익명 함수 변환 허용 (있고 필요 하지 않습니다) 동일한 대리자 인스턴스를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-556">Conversions of semantically identical anonymous functions with the same (possibly empty) set of captured outer variable instances to the same delegate types are permitted (but not required) to return the same delegate instance.</span></span> <span data-ttu-id="7b523-557">과 의미상 동일 용어는 익명 함수 실행을, 모든 경우에 생성 됩니다 동일한 인수를 지정 된 동일한 효력을 평균값으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-557">The term semantically identical is used here to mean that execution of the anonymous functions will, in all cases, produce the same effects given the same arguments.</span></span> <span data-ttu-id="7b523-558">이 규칙은 최적화 되도록 다음과 같은 코드를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-558">This rule permits code such as the following to be optimized.</span></span>

```csharp
delegate double Function(double x);

class Test
{
    static double[] Apply(double[] a, Function f) {
        double[] result = new double[a.Length];
        for (int i = 0; i < a.Length; i++) result[i] = f(a[i]);
        return result;
    }

    static void F(double[] a, double[] b) {
        a = Apply(a, (double x) => Math.Sin(x));
        b = Apply(b, (double y) => Math.Sin(y));
        ...
    }
}
```

<span data-ttu-id="7b523-559">두 익명 함수 대리자를 동일한 (비어 있음) 외부 캡처된 변수의 및 익명 함수 의미상 동일 하므로 설정 하므로, 컴파일러는 동일한 대상 메서드를 참조 하는 대리자가 하도록 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-559">Since the two anonymous function delegates have the same (empty) set of captured outer variables, and since the anonymous functions are semantically identical, the compiler is permitted to have the delegates refer to the same target method.</span></span> <span data-ttu-id="7b523-560">실제로 컴파일러는 모두 익명 함수 식에서 똑같은 대리자 인스턴스를 반환 하도록 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-560">Indeed, the compiler is permitted to return the very same delegate instance from both anonymous function expressions.</span></span>

### <a name="evaluation-of-anonymous-function-conversions-to-expression-tree-types"></a><span data-ttu-id="7b523-561">익명 함수 식 트리 형식으로의 변환의 평가</span><span class="sxs-lookup"><span data-stu-id="7b523-561">Evaluation of anonymous function conversions to expression tree types</span></span>

<span data-ttu-id="7b523-562">식 트리를 생성 하는 익명 함수는 식 트리 형식으로 변환 ([식 트리 형식](types.md#expression-tree-types)).</span><span class="sxs-lookup"><span data-stu-id="7b523-562">Conversion of an anonymous function to an expression tree type produces an expression tree ([Expression tree types](types.md#expression-tree-types)).</span></span> <span data-ttu-id="7b523-563">보다 정확 하 게 평가 익명 함수 변환의 익명 함수 자체의 구조를 나타내는 개체 구조를 생성 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-563">More precisely, evaluation of the anonymous function conversion leads to the construction of an object structure that represents the structure of the anonymous function itself.</span></span> <span data-ttu-id="7b523-564">만들기 위한 정확한 프로세스 뿐만 아니라 식 트리를 정확한 구조는 정의 된 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-564">The precise structure of the expression tree, as well as the exact process for creating it, are implementation defined.</span></span>

### <a name="implementation-example"></a><span data-ttu-id="7b523-565">구현 예제</span><span class="sxs-lookup"><span data-stu-id="7b523-565">Implementation example</span></span>

<span data-ttu-id="7b523-566">이 섹션에서는 다른 C# 구문 측면에서 익명 함수 변환의 가능한 구현을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-566">This section describes a possible implementation of anonymous function conversions in terms of other C# constructs.</span></span> <span data-ttu-id="7b523-567">여기에 설명 된 구현은 Microsoft C# 컴파일러에 의해 사용 되는 동일한 원칙에 기반 하지만 위임된 구현 되지는 않습니다 자신과 하나만 가능한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-567">The implementation described here is based on the same principles used by the Microsoft C# compiler, but it is by no means a mandated implementation, nor is it the only one possible.</span></span> <span data-ttu-id="7b523-568">아주 잠시 동안만이 사양의 범위 외부의 정확한 의미 체계는 식 트리로 변환 언급 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-568">It only briefly mentions conversions to expression trees, as their exact semantics are outside the scope of this specification.</span></span>

<span data-ttu-id="7b523-569">이 섹션의 나머지 부분은 다른 특징을 가진 익명 함수를 포함 하는 코드의 몇 가지 예를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-569">The remainder of this section gives several examples of code that contains anonymous functions with different characteristics.</span></span> <span data-ttu-id="7b523-570">각 예를 들어만 다른 C# 구문을 사용 하는 코드를 해당 번역이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-570">For each example, a corresponding translation to code that uses only other C# constructs is provided.</span></span> <span data-ttu-id="7b523-571">이 예제에서는 식별자에에서 `D` 다음 대리자 형식을 나타내는으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-571">In the examples, the identifier `D` is assumed by represent the following delegate type:</span></span>
```csharp
public delegate void D();
```

<span data-ttu-id="7b523-572">가장 간단한 형태의 익명 함수를은 없는 외부 변수를 캡처하는 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-572">The simplest form of an anonymous function is one that captures no outer variables:</span></span>
```csharp
class Test
{
    static void F() {
        D d = () => { Console.WriteLine("test"); };
    }
}
```

<span data-ttu-id="7b523-573">익명 함수의 코드가 배치 되는 컴파일러에서 생성 된 정적 메서드를 참조 하는 대리자 인스턴스화를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-573">This can be translated to a delegate instantiation that references a compiler generated static method in which the code of the anonymous function is placed:</span></span>
```csharp
class Test
{
    static void F() {
        D d = new D(__Method1);
    }

    static void __Method1() {
        Console.WriteLine("test");
    }
}
```

<span data-ttu-id="7b523-574">다음 예제에서는 익명 함수 참조의 인스턴스 멤버 `this`:</span><span class="sxs-lookup"><span data-stu-id="7b523-574">In the following example, the anonymous function references instance members of `this`:</span></span>
```csharp
class Test
{
    int x;

    void F() {
        D d = () => { Console.WriteLine(x); };
    }
}
```

<span data-ttu-id="7b523-575">익명 함수의 코드를 포함 하는 컴파일러에서 생성 된 인스턴스 메서드를 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-575">This can be translated to a compiler generated instance method containing the code of the anonymous function:</span></span>
```csharp
class Test
{
    int x;

    void F() {
        D d = new D(__Method1);
    }

    void __Method1() {
        Console.WriteLine(x);
    }
}
```

<span data-ttu-id="7b523-576">이 예제에서는 익명 함수는 지역 변수를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-576">In this example, the anonymous function captures a local variable:</span></span>
```csharp
class Test
{
    void F() {
        int y = 123;
        D d = () => { Console.WriteLine(y); };
    }
}
```

<span data-ttu-id="7b523-577">로컬 변수의 수명은 이제를 확장 하 이상 익명 함수 대리자의 수명입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-577">The lifetime of the local variable must now be extended to at least the lifetime of the anonymous function delegate.</span></span> <span data-ttu-id="7b523-578">이 지역 변수를 컴파일러에서 생성 된 클래스의 필드에 "호이스팅" 하 여 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-578">This can be achieved by "hoisting" the local variable into a field of a compiler generated class.</span></span> <span data-ttu-id="7b523-579">지역 변수의 인스턴스화 ([로컬 변수의 인스턴스화](expressions.md#instantiation-of-local-variables)) 인스턴스의 필드에 액세스에 해당 하는 로컬 변수에 액세스 하는 컴파일러에서 생성 된 클래스의 인스턴스를 만드는 다음 해당 컴파일러에서 생성 된 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-579">Instantiation of the local variable ([Instantiation of local variables](expressions.md#instantiation-of-local-variables)) then corresponds to creating an instance of the compiler generated class, and accessing the local variable corresponds to accessing a field in the instance of the compiler generated class.</span></span> <span data-ttu-id="7b523-580">또한 익명 함수는 컴파일러에서 생성 된 클래스의 인스턴스 메서드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-580">Furthermore, the anonymous function becomes an instance method of the compiler generated class:</span></span>
```csharp
class Test
{
    void F() {
        __Locals1 __locals1 = new __Locals1();
        __locals1.y = 123;
        D d = new D(__locals1.__Method1);
    }

    class __Locals1
    {
        public int y;

        public void __Method1() {
            Console.WriteLine(y);
        }
    }
}
```

<span data-ttu-id="7b523-581">마지막으로 다음 익명 함수 캡처 `this` 다른 수명 사용 하 여 두 개의 로컬 변수 뿐만 아니라:</span><span class="sxs-lookup"><span data-stu-id="7b523-581">Finally, the following anonymous function captures `this` as well as two local variables with different lifetimes:</span></span>
```csharp
class Test
{
    int x;

    void F() {
        int y = 123;
        for (int i = 0; i < 10; i++) {
            int z = i * 2;
            D d = () => { Console.WriteLine(x + y + z); };
        }
    }
}
```

<span data-ttu-id="7b523-582">각 문에 대해 컴파일러에서 생성 된 클래스를 만들 여기서 블록에 지역 변수는 다른 블록에서 지역 변수는 독립적인 수명 수 있도록 캡처됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-582">Here, a compiler generated class is created for each statement block in which locals are captured such that the locals in the different blocks can have independent lifetimes.</span></span> <span data-ttu-id="7b523-583">인스턴스의 `__Locals2`, 로컬 변수를 포함 하는 내부 문 블록에 대 한 컴파일러에서 생성 된 클래스 `z` 의 인스턴스를 참조 하는 필드와 `__Locals1`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-583">An instance of `__Locals2`, the compiler generated class for the inner statement block, contains the local variable `z` and a field that references an instance of `__Locals1`.</span></span>  <span data-ttu-id="7b523-584">인스턴스의 `__Locals1`, 로컬 변수를 포함 하는 외부 문 블록에 대 한 컴파일러에서 생성 된 클래스 `y` 를 참조 하는 필드와 `this` 바깥쪽 함수 멤버의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-584">An instance of `__Locals1`, the compiler generated class for the outer statement block, contains the local variable `y` and a field that references `this` of the enclosing function member.</span></span> <span data-ttu-id="7b523-585">이러한 데이터 구조에 연결할 수 있기를 사용 하 여 모든 인스턴스를 통해 외부 변수 캡처할 `__Local2`, 익명 함수의 코드를 해당 클래스의 인스턴스 메서드로 구현할 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-585">With these data structures it is possible to reach all captured outer variables through an instance of `__Local2`, and the code of the anonymous function can thus be implemented as an instance method of that class.</span></span>

```csharp
class Test
{
    void F() {
        __Locals1 __locals1 = new __Locals1();
        __locals1.__this = this;
        __locals1.y = 123;
        for (int i = 0; i < 10; i++) {
            __Locals2 __locals2 = new __Locals2();
            __locals2.__locals1 = __locals1;
            __locals2.z = i * 2;
            D d = new D(__locals2.__Method1);
        }
    }

    class __Locals1
    {
        public Test __this;
        public int y;
    }

    class __Locals2
    {
        public __Locals1 __locals1;
        public int z;

        public void __Method1() {
            Console.WriteLine(__locals1.__this.x + __locals1.y + z);
        }
    }
}
```

<span data-ttu-id="7b523-586">익명 함수 식 트리로 변환 하는 경우에 기술은 여기 적용할 로컬 변수를 캡처를 사용할 수 있습니다: 식 트리에서 컴파일러에서 생성 된 개체에 대 한 참조를 저장 될 수 있으며 로컬 변수에 액세스할 수 있습니다. 이러한 개체에 액세스 하는 필드 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-586">The same technique applied here to capture local variables can also be used when converting anonymous functions to expression trees: References to the compiler generated objects can be stored in the expression tree, and access to the local variables can be represented as field accesses on these objects.</span></span> <span data-ttu-id="7b523-587">이 방식의 장점은 "리프트" 로컬 변수를 식 트리 및 대리자 간에 공유할 수 있도록 한다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-587">The advantage of this approach is that it allows the "lifted" local variables to be shared between delegates and expression trees.</span></span>

## <a name="method-group-conversions"></a><span data-ttu-id="7b523-588">메서드 그룹 변환</span><span class="sxs-lookup"><span data-stu-id="7b523-588">Method group conversions</span></span>

<span data-ttu-id="7b523-589">암시적으로 변환 ([암시적 변환을](conversions.md#implicit-conversions)) 메서드 그룹에서 존재 ([식 분류](expressions.md#expression-classifications)) 호환 되는 대리자 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-589">An implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) exists from a method group ([Expression classifications](expressions.md#expression-classifications)) to a compatible delegate type.</span></span> <span data-ttu-id="7b523-590">지정 된 대리자 형식 `D` 및 식을 `E` 메서드 그룹으로 분류 되는의 암시적 변환이 존재 `E` 에 `D` 경우 `E` 해당 정규형 (에서 적용 되는 하나 이상의 메서드를 포함 [적용 가능한 함수 멤버](expressions.md#applicable-function-member))의 한정자 및 형식 매개 변수는 사용 하 여 생성 된 인수 목록에 `D`다음에 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-590">Given a delegate type `D` and an expression `E` that is classified as a method group, an implicit conversion exists from `E` to `D` if `E` contains at least one method that is applicable in its normal form ([Applicable function member](expressions.md#applicable-function-member)) to an argument list constructed by use of the parameter types and modifiers of `D`, as described in the following.</span></span>

<span data-ttu-id="7b523-591">메서드 그룹 변환의 컴파일 타임 응용 프로그램 `E` 대리자 형식에 `D` 다음에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-591">The compile-time application of a conversion from a method group `E` to a delegate type `D` is described in the following.</span></span> <span data-ttu-id="7b523-592">암시적 변환이 존재 `E` 에 `D` 오류 없이 컴파일 타임 응용 프로그램 변환의 성공 한다는 사실을 보장 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-592">Note that the existence of an implicit conversion from `E` to `D` does not guarantee that the compile-time application of the conversion will succeed without error.</span></span>

*  <span data-ttu-id="7b523-593">단일 메서드 `M` 메서드 호출에 해당 선택 ([메서드 호출](expressions.md#method-invocations)) 형식의 `E(A)`, 다음 수정:</span><span class="sxs-lookup"><span data-stu-id="7b523-593">A single method `M` is selected corresponding to a method invocation ([Method invocations](expressions.md#method-invocations)) of the form `E(A)`, with the following modifications:</span></span>
    * <span data-ttu-id="7b523-594">인수 목록 `A` 은 식, 변수 및 형식 및 한정자를 사용 하 여 각 분류 목록 (`ref` 또는 `out`)에서 해당 매개 변수를 *formal_parameter_list* 의`D`.</span><span class="sxs-lookup"><span data-stu-id="7b523-594">The argument list `A` is a list of expressions, each classified as a variable and with the type and modifier (`ref` or `out`) of the corresponding parameter in the *formal_parameter_list* of `D`.</span></span>
    * <span data-ttu-id="7b523-595">간주 후보 메서드는 해당 기본 폼에 적용 되는 방법만 ([적용 가능한 함수 멤버](expressions.md#applicable-function-member)), 해당 확장된 형식에만 적용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-595">The candidate methods considered are only those methods that are applicable in their normal form ([Applicable function member](expressions.md#applicable-function-member)), not those applicable only in their expanded form.</span></span>
*  <span data-ttu-id="7b523-596">하는 경우의 알고리즘 [메서드 호출](expressions.md#method-invocations) 컴파일 타임 오류가 발생 하는 다음 오류를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-596">If the algorithm of [Method invocations](expressions.md#method-invocations) produces an error, then a compile-time error occurs.</span></span> <span data-ttu-id="7b523-597">알고리즘은 단일 최상의 메서드를 생성 하는 고, 그렇지 `M` 는 동일한 매개 변수 수가 `D` 변환이 있는 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-597">Otherwise the algorithm produces a single best method `M` having the same number of parameters as `D` and the conversion is considered to exist.</span></span>
*  <span data-ttu-id="7b523-598">선택한 메서드 `M` 호환 되어야 합니다 ([대리자 호환성](delegates.md#delegate-compatibility)) 대리자 형식을 사용 하 여 `D`, 또는 그렇지 않으면 컴파일 타임 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-598">The selected method `M` must be compatible ([Delegate compatibility](delegates.md#delegate-compatibility)) with the delegate type `D`, or otherwise, a compile-time error occurs.</span></span>
*  <span data-ttu-id="7b523-599">경우 선택한 메서드 `M` 되는 인스턴스 메서드를 사용 하 여 연결 된 인스턴스 식이 `E` 대리자의 대상 개체를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-599">If the selected method `M` is an instance method, the instance expression associated with `E` determines the target object of the delegate.</span></span>
*  <span data-ttu-id="7b523-600">선택한 메서드 M 확장 메서드가 인스턴스 식에는 멤버 액세스를 사용 하 여 표시 되는 경우 해당 인스턴스 식이 대리자의 대상 개체를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-600">If the selected method M is an extension method which is denoted by means of a member access on an instance expression, that instance expression determines the target object of the delegate.</span></span>
*  <span data-ttu-id="7b523-601">변환의 결과 형식의 값 `D`, 선택한 메서드 및 대상 개체를 참조 하는 새로 만든된 대리자 즉 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-601">The result of the conversion is a value of type `D`, namely a newly created delegate that refers to the selected method and target object.</span></span>
*  <span data-ttu-id="7b523-602">이 프로세스는 확장 메서드는 대리자를 만들 경우 발생할 수 있습니다는 알고리즘 [메서드 호출](expressions.md#method-invocations) 인스턴스 메서드를 찾지 못하면 하지만 호출 처리 성공 `E(A)` 확장으로 메서드 호출 ([확장 메서드 호출](expressions.md#extension-method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="7b523-602">Note that this process can lead to the creation of a delegate to an extension method, if the algorithm of [Method invocations](expressions.md#method-invocations) fails to find an instance method but succeeds in processing the invocation of `E(A)` as an extension method invocation ([Extension method invocations](expressions.md#extension-method-invocations)).</span></span> <span data-ttu-id="7b523-603">따라서 만든 대리자의 첫 번째 인수가 뿐만 아니라 확장 메서드를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-603">A delegate thus created captures the extension method as well as its first argument.</span></span>

<span data-ttu-id="7b523-604">다음 예제에서는 메서드 그룹 변환 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-604">The following example demonstrates method group conversions:</span></span>
```csharp
delegate string D1(object o);

delegate object D2(string s);

delegate object D3();

delegate string D4(object o, params object[] a);

delegate string D5(int i);

class Test
{
    static string F(object o) {...}

    static void G() {
        D1 d1 = F;            // Ok
        D2 d2 = F;            // Ok
        D3 d3 = F;            // Error -- not applicable
        D4 d4 = F;            // Error -- not applicable in normal form
        D5 d5 = F;            // Error -- applicable but not compatible

    }
}
```

<span data-ttu-id="7b523-605">에 대 한 할당 `d1` 메서드 그룹을 암시적으로 변환 `F` 형식의 값으로 `D1`입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-605">The assignment to `d1` implicitly converts the method group `F` to a value of type `D1`.</span></span>

<span data-ttu-id="7b523-606">에 대 한 할당 `d2` 에 더 적게 파생 된 (변성이) 매개 변수 형식 및 더 파생 (공변 (covariant)) 반환 형식 메서드에 대리자를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-606">The assignment to `d2` shows how it is possible to create a delegate to a method that has less derived (contra-variant) parameter types and a more derived (covariant) return type.</span></span>

<span data-ttu-id="7b523-607">에 대 한 할당 `d3` 메서드에 적용할 수 없는 경우 변환 작업 없이 존재 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-607">The assignment to `d3` shows how no conversion exists if the method is not applicable.</span></span>

<span data-ttu-id="7b523-608">에 대 한 할당 `d4` 메서드 일반적인 형태로 적용할 수 있어야 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-608">The assignment to `d4` shows how the method must be applicable in its normal form.</span></span>

<span data-ttu-id="7b523-609">에 대 한 할당 `d5` 메서드와 대리자의 매개 변수 및 반환 형식을 참조 형식에 대해서만 다를 수는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-609">The assignment to `d5` shows how parameter and return types of the delegate and method are allowed to differ only for reference types.</span></span>

<span data-ttu-id="7b523-610">모든 다른 암시적 변환과 명시적 변환, 마찬가지로 캐스트 연산자를 메서드 그룹 변환 명시적으로 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-610">As with all other implicit and explicit conversions, the cast operator can be used to explicitly perform a method group conversion.</span></span> <span data-ttu-id="7b523-611">따라서 예제</span><span class="sxs-lookup"><span data-stu-id="7b523-611">Thus, the example</span></span>
```csharp
object obj = new EventHandler(myDialog.OkClick);
```
<span data-ttu-id="7b523-612">대신 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-612">could instead be written</span></span>
```csharp
object obj = (EventHandler)myDialog.OkClick;
```

<span data-ttu-id="7b523-613">메서드 그룹 오버 로드 확인에 영향을 줄 및 형식 유추에 참여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-613">Method groups may influence overload resolution, and participate in type inference.</span></span> <span data-ttu-id="7b523-614">참조 [멤버 함수](expressions.md#function-members) 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-614">See [Function members](expressions.md#function-members) for further details.</span></span>

<span data-ttu-id="7b523-615">메서드 그룹 변환의 런타임 평가 다음과 같이 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-615">The run-time evaluation of a method group conversion proceeds as follows:</span></span>

*  <span data-ttu-id="7b523-616">대리자의 대상 개체와 연결 된 인스턴스 식에서 도달한 경우 컴파일 타임에 선택한 메서드는 인스턴스 메서드 또는 인스턴스 메서드로 액세스 하는 확장 메서드는, `E`:</span><span class="sxs-lookup"><span data-stu-id="7b523-616">If the method selected at compile-time is an instance method, or it is an extension method which is accessed as an instance method, the target object of the delegate is determined from the instance expression associated with `E`:</span></span>
    * <span data-ttu-id="7b523-617">인스턴스 식은 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-617">The instance expression is evaluated.</span></span> <span data-ttu-id="7b523-618">이 평가 예외를 발생 시키는 경우에 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-618">If this evaluation causes an exception, no further steps are executed.</span></span>
    * <span data-ttu-id="7b523-619">인스턴스 식의 경우는 *reference_type*, 인스턴스 식에서 계산 된 값은 대상 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-619">If the instance expression is of a *reference_type*, the value computed by the instance expression becomes the target object.</span></span> <span data-ttu-id="7b523-620">경우 선택한 메서드는 인스턴스 메서드를 이며 대상 개체가 `null`, `System.NullReferenceException` throw 되 고 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-620">If the selected method is an instance method and the target object is `null`, a `System.NullReferenceException` is thrown and no further steps are executed.</span></span>
    * <span data-ttu-id="7b523-621">인스턴스 식의 경우는 *value_type*, boxing 작업이 ([Boxing 변환](types.md#boxing-conversions)) 개체에 값을 변환 하기 위해 수행 됩니다 대상 개체가 되 고이 개체 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-621">If the instance expression is of a *value_type*, a boxing operation ([Boxing conversions](types.md#boxing-conversions)) is performed to convert the value to an object, and this object becomes the target object.</span></span>
*  <span data-ttu-id="7b523-622">선택한 메서드는 정적 메서드 호출의 일부인 그렇지 않은 경우 및 대리자의 대상 개체가 `null`합니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-622">Otherwise the selected method is part of a static method call, and the target object of the delegate is `null`.</span></span>
*  <span data-ttu-id="7b523-623">대리자 형식의 새 인스턴스를 `D` 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-623">A new instance of the delegate type `D` is allocated.</span></span> <span data-ttu-id="7b523-624">새 인스턴스를 할당할 수 있는 충분 한 메모리가 없을 경우는 `System.OutOfMemoryException` throw 되 고 추가 단계 없이 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-624">If there is not enough memory available to allocate the new instance, a `System.OutOfMemoryException` is thrown and no further steps are executed.</span></span>
*  <span data-ttu-id="7b523-625">위의 계산 대상 개체에 대 한 참조 및 컴파일 타임에 확인 된 메서드에 대 한 참조를 사용 하 여 새 대리자 인스턴스를 초기화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7b523-625">The new delegate instance is initialized with a reference to the method that was determined at compile-time and a reference to the target object computed above.</span></span>
