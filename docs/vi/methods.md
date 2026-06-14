---
title: Tổng quan về methods
description: Tổng quan về methods, tham số và giá trị trả về của methods
ms.subservice: fundamentals
ms.date: 04/17/2025
---

# Methods trong C\#

Method (phương thức) là một khối mã chứa một chuỗi các câu lệnh. Khi bạn gọi một method và truyền argument (đối số) cho nó, chương trình sẽ thực thi các câu lệnh bên trong. Trong C#, mọi lệnh được thực thi đều nằm trong một method nào đó.

> [!NOTE]
> Bài viết này nói về named methods (method có tên). Để tìm hiểu về anonymous functions (hàm ẩn danh), hãy xem [Biểu thức lambda](language-reference/operators/lambda-expressions.md).

## Method signatures (chữ ký phương thức)

Khi khai báo một method trong `class`, `record` hoặc `struct`, bạn cần chỉ định:

- Mức truy cập (access level) tuỳ chọn, như `public` hoặc `private`. Mặc định là `private`.
- Các modifier tuỳ chọn như `abstract` hoặc `sealed`.
- Return type (Kiểu trả về), hoặc `void` nếu method không trả về gì.
- Tên method.
- Parameters (Tham số). Tham số được đặt trong ngoặc đơn và phân cách bằng dấu phẩy. Nếu không có tham số thì để ngoặc rỗng.

Tất cả những phần trên hợp lại tạo thành method signature (chữ ký phương thức).

> [!IMPORTANT]
> Kiểu trả về không phải là một phần của method signature khi xét tới method overloading (nạp chồng phương thức). Tuy nhiên, nó lại là một phần của method signature khi xác định tính tương thích giữa delegate (uỷ quyền) và method mà nó trỏ tới.

Ví dụ dưới đây định nghĩa một class tên `Motorcycle` chứa năm method:

```csharp
namespace MotorCycleExample
{
    abstract class Motorcycle
    {
        // Anyone can call this.
        public void StartEngine() {/* Method statements here */ }

        // Only derived classes can call this.
        protected void AddGas(int gallons) { /* Method statements here */ }

        // Derived classes can override the base class implementation.
        public virtual int Drive(int miles, int speed) { /* Method statements here */ return 1; }

        // Derived classes can override the base class implementation.
        public virtual int Drive(TimeSpan time, int speed) { /* Method statements here */ return 0; }

        // Derived classes must implement this.
        public abstract double GetTopSpeed();
    }
}
```

Class `Motorcycle` có một method được overload (nạp chồng) tên `Drive`. Hai method này có cùng tên nhưng danh sách tham số khác nhau.

## Cách gọi method (Method invocation)

Method có thể là *instance* hoặc *static*. Bạn phải tạo một object (đối tượng) thì mới gọi được instance method trên object đó; instance method làm việc với dữ liệu của object. Còn static method thì bạn gọi trực tiếp qua tên class mà không cần tạo object. Cố gắng gọi static method thông qua một object sẽ gây lỗi biên dịch.

Cú pháp gọi method giống như truy cập một field: sau tên object (nếu gọi instance method) hoặc tên type (kiểu dữ liệu) (nếu gọi static method), bạn thêm dấu chấm, tên method và ngoặc đơn. Các đối số (arguments) được đặt trong ngoặc và phân cách bằng dấu phẩy.

Định nghĩa method chỉ rõ tên và kiểu của từng tham số. Khi gọi method, bạn cần cung cấp các giá trị cụ thể (gọi là argument) cho mỗi tham số. Các argument này phải tương thích với kiểu của tham số, nhưng tên biến bạn dùng khi gọi không cần trùng với tên tham số trong method. Trong ví dụ dưới đây, method `Square` nhận một tham số kiểu `int` tên *i*. Lần gọi đầu tiên truyền vào một biến `int` tên *num*; lần thứ hai truyền hằng số; lần thứ ba truyền một biểu thức.

```csharp
public static class SquareExample
{
    public static void Main()
    {
        // Call with an int variable.
        int num = 4;
        int productA = Square(num);

        // Call with an integer literal.
        int productB = Square(12);

        // Call with an expression that evaluates to int.
        int productC = Square(productA * 3);
    }

    static int Square(int i)
    {
        // Store input argument in a local variable.
        int input = i;
        return input * input;
    }
}
```

Cách gọi phổ biến nhất là positional arguments -- bạn truyền argument theo đúng thứ tự các tham số của method. Do đó bạn có thể gọi các method của class `Motorcycle` như sau. Ví dụ, lời gọi method `Drive` có hai argument tương ứng với hai tham số: argument đầu tiên là giá trị cho `miles`, argument thứ hai là giá trị cho `speed`.

```csharp
class TestMotorcycle : Motorcycle
{
    public override double GetTopSpeed() => 108.4;

    static void Main()
    {
        var moto = new TestMotorcycle();

        moto.StartEngine();
        moto.AddGas(15);
        _ = moto.Drive(5, 20);
        double speed = moto.GetTopSpeed();
        Console.WriteLine($"My top speed is {speed}");
    }
}
```

Bạn cũng có thể dùng *named arguments* (đối số có tên) thay vì positional arguments. Khi dùng named arguments, bạn chỉ định tên tham số, dấu hai chấm, rồi giá trị. Các argument có thể theo thứ tự bất kỳ, miễn là có đủ argument bắt buộc. Ví dụ sau dùng named arguments để gọi method `TestMotorcycle.Drive` -- các named arguments được truyền theo thứ tự ngược với danh sách tham số.

```csharp
namespace NamedMotorCycle;

class TestMotorcycle : Motorcycle
{
    public override int Drive(int miles, int speed) =>
        (int)Math.Round((double)miles / speed, 0);

    public override double GetTopSpeed() => 108.4;

    static void Main()
    {
        var moto = new TestMotorcycle();
        moto.StartEngine();
        moto.AddGas(15);
        int travelTime = moto.Drive(speed: 60, miles: 170);
        Console.WriteLine($"Travel time: approx. {travelTime} hours");
    }
}
// The example displays the following output:
//      Travel time: approx. 3 hours
```

Bạn có thể kết hợp positional arguments và named arguments trong cùng một lời gọi. Tuy nhiên, positional arguments chỉ được đặt sau named arguments nếu các named arguments đó đang đứng đúng vị trí. Ví dụ dưới đây gọi method `TestMotorcycle.Drive` với một positional argument và một named argument.

```csharp
int travelTime = moto.Drive(170, speed: 55);
```

## Kế thừa và ghi đè method (Inherited and overridden methods)

Ngoài các thành viên được định nghĩa trong type, type còn kế thừa các thành viên từ class cha. Vì tất cả các type đều kế thừa trực tiếp hoặc gián tiếp từ [`Object`](https://learn.microsoft.com/dotnet/api/system.object), nên type nào cũng có sẵn các method như [`Object.Equals(Object)`](https://learn.microsoft.com/dotnet/api/system.object.equals#system-object-equals-system-object-), [`Object.GetType`](https://learn.microsoft.com/dotnet/api/system.object.gettype) và [`Object.ToString`](https://learn.microsoft.com/dotnet/api/system.object.tostring). Ví dụ sau tạo class `Person`, khởi tạo hai object và gọi `Person.Equals` để kiểm tra xem chúng có bằng nhau không. Method `Equals` không được định nghĩa trong `Person` -- nó được kế thừa từ [`Object`](https://learn.microsoft.com/dotnet/api/system.object).

```csharp
public class Person
{
    public string FirstName = default!;
}

public static class ClassTypeExample
{
    public static void Main()
    {
        Person p1 = new() { FirstName = "John" };
        Person p2 = new() { FirstName = "John" };
        Console.WriteLine($"p1 = p2: {p1.Equals(p2)}");
    }
}
// The example displays the following output:
//      p1 = p2: False
```

Các type có thể ghi đè (override) method được kế thừa bằng từ khoá `override` và cung cấp cách triển khai (implementation) mới. Method signature phải giống với method gốc. Ví dụ sau giống với ví dụ trên nhưng có ghi đè method [`Object.Equals(Object)`](https://learn.microsoft.com/dotnet/api/system.object.equals#system-object-equals-system-object-) (và cả [`Object.GetHashCode`](https://learn.microsoft.com/dotnet/api/system.object.gethashcode), vì hai method này cần nhất quán với nhau).

```csharp
namespace methods;

public class Person
{
    public string FirstName = default!;

    public override bool Equals(object? obj) =>
        obj is Person p2 &&
        FirstName.Equals(p2.FirstName);

    public override int GetHashCode() => FirstName.GetHashCode();
}

public static class Example
{
    public static void Main()
    {
        Person p1 = new() { FirstName = "John" };
        Person p2 = new() { FirstName = "John" };
        Console.WriteLine($"p1 = p2: {p1.Equals(p2)}");
    }
}
// The example displays the following output:
//      p1 = p2: True
```

## Truyền tham số (Passing parameters)

Trong C#, type có hai loại: *value types* (kiểu giá trị) và *reference types* (kiểu tham chiếu). Danh sách các value types có sẵn bạn có thể xem tại [Kiểu](./language-reference/builtin-types/built-in-types.md). Theo mặc định, cả value types và reference types đều được truyền bằng giá trị (passed by value) vào method.

### Truyền tham số bằng giá trị (Passing parameters by value)

Khi bạn truyền một value type vào method bằng giá trị, method nhận được một bản sao của dữ liệu, không phải dữ liệu gốc. Vì vậy, mọi thay đổi bên trong method sẽ không ảnh hưởng tới biến gốc bên ngoài.

Ví dụ sau truyền một value type (kiểu `int`) vào method bằng giá trị. Method `ModifyValue` cố gắng đổi giá trị từ 20 thành 30, nhưng sau khi method kết thúc, biến gốc vẫn giữ nguyên giá trị 20.

```csharp
public static class ByValueExample
{
    public static void Main()
    {
        var value = 20;
        Console.WriteLine("In Main, value = {0}", value);
        ModifyValue(value);
        Console.WriteLine("Back in Main, value = {0}", value);
    }

    static void ModifyValue(int i)
    {
        i = 30;
        Console.WriteLine("In ModifyValue, parameter value = {0}", i);
        return;
    }
}
// The example displays the following output:
//      In Main, value = 20
//      In ModifyValue, parameter value = 30
//      Back in Main, value = 20
```

Khi truyền một reference type vào method bằng giá trị, method nhận được một bản sao của *tham chiếu*, không phải object gốc. Nghĩa là method biết object đó nằm ở đâu trong bộ nhớ. Nếu bạn thay đổi một thuộc tính của object thông qua tham chiếu này, object gốc sẽ bị ảnh hưởng. Nhưng nếu bạn gán object mới cho tham chiếu đó, object gốc không thay đổi.

Ví dụ sau định nghĩa class `SampleRefType` (một reference type), gán 44 cho field `value`, rồi truyền nó vào method `ModifyObject`. Khác với ví dụ value type ở trên, lần này sự thay đổi bên trong method có ảnh hưởng tới object gốc -- field `value` của `rt` trong `Main` cũng bị đổi thành 33.

```csharp
public class SampleRefType
{
    public int value;
}

public static class ByRefTypeExample
{
    public static void Main()
    {
        var rt = new SampleRefType { value = 44 };
        ModifyObject(rt);
        Console.WriteLine(rt.value);
    }

    static void ModifyObject(SampleRefType obj) => obj.value = 33;
}
```

### Truyền tham số bằng tham chiếu (Passing parameters by reference)

Khi bạn muốn thay đổi giá trị của một argument và giữ sự thay đổi đó sau khi method kết thúc, hãy truyền tham số by reference (bằng tham chiếu). Bạn dùng từ khoá [`ref`](language-reference/keywords/ref.md) hoặc [`out`](language-reference/keywords/method-parameters.md#out-parameter-modifier). Nếu bạn muốn tránh sao chép dữ liệu nhưng vẫn ngăn sửa đổi, dùng từ khoá [`in`](language-reference/keywords/method-parameters.md#in-parameter-modifier).

Ví dụ sau giống với ví dụ value type ở trên, nhưng lần này giá trị được truyền bằng tham chiếu. Khi method `ModifyValue` thay đổi giá trị, biến gốc cũng thay đổi theo.

```csharp
public static class ByRefExample
{
    public static void Main()
    {
        var value = 20;
        Console.WriteLine("In Main, value = {0}", value);
        ModifyValue(ref value);
        Console.WriteLine("Back in Main, value = {0}", value);
    }

    private static void ModifyValue(ref int i)
    {
        i = 30;
        Console.WriteLine("In ModifyValue, parameter value = {0}", i);
        return;
    }
}
// The example displays the following output:
//      In Main, value = 20
//      In ModifyValue, parameter value = 30
//      Back in Main, value = 30
```

Một ứng dụng phổ biến của tham số by ref là hoán đổi giá trị hai biến. Bạn truyền hai biến vào method bằng tham chiếu, method sẽ đổi chỗ giá trị cho nhau.

```csharp
public static class RefSwapExample
{
    static void Main()
    {
        int i = 2, j = 3;
        Console.WriteLine($"i = {i}  j = {j}");

        Swap(ref i, ref j);

        Console.WriteLine($"i = {i}  j = {j}");
    }

    static void Swap(ref int x, ref int y) =>
        (y, x) = (x, y);
}
// The example displays the following output:
//      i = 2  j = 3
//      i = 3  j = 2
```

Truyền tham số reference type bằng tham chiếu còn cho phép bạn thay đổi chính object mà tham chiếu đang trỏ tới, chứ không chỉ thay đổi nội dung bên trong object.

### Tham số tập hợp (Parameter collections)

Đôi khi bạn không biết trước sẽ có bao nhiêu argument khi gọi method. Từ khoá `params` cho phép bạn khai báo một tham số tập hợp (parameter collection) -- method có thể nhận số lượng argument khác nhau mỗi lần gọi. Tham số có `params` phải là kiểu tập hợp (collection type) và phải nằm cuối cùng trong danh sách tham số.

Khi gọi method, bạn có thể truyền đối số cho tham số `params` theo bốn cách:

- Truyền một collection đúng kiểu chứa các phần tử mong muốn. Ví dụ dùng [biểu thức tập hợp](./language-reference/operators/collection-expressions.md) để compiler tự tạo collection phù hợp.
- Truyền một danh sách các giá trị ngăn cách bằng dấu phẩy. Compiler sẽ tự tạo collection tương ứng.
- Truyền `null`.
- Không truyền gì cả.

Ví dụ sau định nghĩa method `GetVowels` trả về tất cả nguyên âm từ một parameter collection. Method `Main` minh hoạ cả bốn cách gọi.

```csharp
static class ParamsExample
{
    static void Main()
    {
        string fromArray = GetVowels(["apple", "banana", "pear"]);
        Console.WriteLine($"Vowels from collection expression: '{fromArray}'");

        string fromMultipleArguments = GetVowels("apple", "banana", "pear");
        Console.WriteLine($"Vowels from multiple arguments: '{fromMultipleArguments}'");

        string fromNull = GetVowels(null);
        Console.WriteLine($"Vowels from null: '{fromNull}'");

        string fromNoValue = GetVowels();
        Console.WriteLine($"Vowels from no value: '{fromNoValue}'");
    }

    static string GetVowels(params IEnumerable<string>? input)
    {
        if (input == null || !input.Any())
        {
            return string.Empty;
        }

        char[] vowels = ['A', 'E', 'I', 'O', 'U'];
        return string.Concat(
            input.SelectMany(
                word => word.Where(letter => vowels.Contains(char.ToUpper(letter)))));
    }
}

// The example displays the following output:
//     Vowels from array: 'aeaaaea'
//     Vowels from multiple arguments: 'aeaaaea'
//     Vowels from null: ''
//     Vowels from no value: ''
```

Trước C# 13, `params` chỉ dùng được với mảng một chiều.

## Tham số tuỳ chọn và đối số (Optional parameters and arguments)

Khi định nghĩa method, bạn có thể chỉ định tham số là bắt buộc (required) hay tuỳ chọn (optional). Mặc định là bắt buộc. Tham số tuỳ chọn có giá trị mặc định -- nếu người gọi không truyền argument, giá trị mặc định sẽ được dùng.

Giá trị mặc định có thể là một trong các dạng sau:

- Hằng số (constant), như một literal string hoặc số.
- Biểu thức dạng `default(SomeType)`, với `SomeType` là value type hoặc reference type. Nếu là reference type thì tương đương `null`. Bạn cũng có thể dùng literal `default` vì compiler tự suy ra kiểu từ khai báo tham số.
- Biểu thức dạng `new ValType()`, với `ValType` là value type. Cách này gọi hàm tạo không tham số ngầm định (implicit parameterless constructor).

  > [!NOTE]
  > Nếu dùng `new ValType()` mà ValType có hàm tạo không tham số tường minh (explicit parameterless constructor), compiler sẽ báo lỗi vì giá trị mặc định phải là hằng số tại thời điểm biên dịch. Hãy dùng `default(ValType)` hoặc literal `default` để thay thế. Xem thêm [Khởi tạo struct và giá trị mặc định](language-reference/builtin-types/struct.md#struct-initialization-and-default-values).

Nếu method có cả tham số bắt buộc và tuỳ chọn, tham số tuỳ chọn phải đứng cuối cùng.

Ví dụ sau định nghĩa method `ExampleMethod` với một tham số bắt buộc và hai tham số tuỳ chọn.

```csharp
public class Options
{
    public void ExampleMethod(int required, int optionalInt = default,
                              string? description = default)
    {
        var msg = $"{description ?? "N/A"}: {required} + {optionalInt} = {required + optionalInt}";
        Console.WriteLine(msg);
    }
}
```

Người gọi phải cung cấp argument cho tất cả tham số tuỳ chọn từ đầu cho tới tham số tuỳ chọn cuối cùng được truyền. Ví dụ, nếu bạn truyền argument cho `description` thì cũng phải truyền luôn cho `optionalInt`. `opt.ExampleMethod(2, 2, "Addition of 2 and 2");` là hợp lệ; `opt.ExampleMethod(2, , "Addition of 2 and 0");` sẽ báo lỗi "Argument missing".

Nếu bạn dùng named arguments hoặc kết hợp positional và named arguments, bạn có thể bỏ qua bất kỳ argument nào đứng sau positional argument cuối cùng.

Ví dụ sau gọi `ExampleMethod` ba lần. Hai lần đầu dùng positional arguments (lần một bỏ qua cả hai optional, lần hai bỏ qua argument cuối). Lần thứ ba dùng positional argument cho tham số bắt buộc nhưng dùng named argument cho `description` và bỏ qua `optionalInt`.

```csharp
public static class OptionsExample
{
    public static void Main()
    {
        var opt = new Options();
        opt.ExampleMethod(10);
        opt.ExampleMethod(10, 2);
        opt.ExampleMethod(12, description: "Addition with zero:");
    }
}
// The example displays the following output:
//      N/A: 10 + 0 = 10
//      N/A: 10 + 2 = 12
//      Addition with zero:: 12 + 0 = 12
```

Optional parameters ảnh hưởng tới *overload resolution* (giải quyết nạp chồng) -- cách compiler chọn overload nào để gọi:

- Một method là ứng viên nếu mỗi tham số của nó khớp với một argument theo tên hoặc vị trí, và argument đó có thể chuyển đổi sang kiểu tham số.
- Nếu có nhiều ứng viên, compiler sẽ áp dụng quy tắc ưu tiên chuyển đổi cho các argument được chỉ định. Các argument bị bỏ qua của optional parameters không được tính.
- Nếu hai ứng viên tương đương nhau, compiler ưu tiên ứng viên không có optional parameters bị bỏ qua.

## Giá trị trả về (Return values)

Method có thể trả về giá trị cho bên gọi. Nếu kiểu trả về (đứng trước tên method) không phải `void`, method phải dùng từ khoá `return` để trả về giá trị -- có thể là biến, hằng số hoặc biểu thức hợp với kiểu trả về. Từ khoá `return` cũng ngay lập tức dừng method lại.

Nếu kiểu trả về là `void`, bạn vẫn có thể dùng `return` không kèm giá trị để dừng method sớm. Nếu không có `return`, method sẽ tự dừng khi chạy tới cuối khối mã.

Ví dụ, hai method sau dùng `return` để trả về số nguyên:

```csharp
class SimpleMath
{
    public int AddTwoNumbers(int number1, int number2) =>
        number1 + number2;

    public int SquareANumber(int number) =>
        number * number;
}
```

Các ví dụ trên là expression bodied members (thành viên thân biểu thức) -- method chỉ gồm một biểu thức duy nhất và giá trị của biểu thức đó là giá trị trả về.

Bạn cũng có thể viết method theo kiểu statement body với câu lệnh `return` thông thường:

```csharp
class SimpleMathExtension
{
    public int DivideTwoNumbers(int number1, int number2)
    {
        return number1 / number2;
    }
}
```

Để dùng giá trị method trả về, bạn gán nó cho một biến:

```csharp
int result = obj.DivideTwoNumbers(6,2);
// The result is 3.
Console.WriteLine(result);
```

Method cũng có thể được gọi ở bất kỳ chỗ nào cần một giá trị cùng kiểu. Hai đoạn mã sau làm cùng một việc:

```csharp
int result = obj.AddTwoNumbers(1, 2);
result = obj.SquareANumber(result);
// The result is 9.
Console.WriteLine(result);
```

```csharp
result = obj.SquareANumber(obj.AddTwoNumbers(1, 2));
// The result is 9.
Console.WriteLine(result);
```

Đôi khi bạn muốn method trả về nhiều hơn một giá trị. Bạn có thể dùng *tuple* để làm việc này. Kiểu tuple (tuple type) định nghĩa kiểu dữ liệu cho từng phần tử. Literal tuple cung cấp giá trị thực tế. Trong ví dụ dưới đây, `(string, string, string, int)` là kiểu tuple trả về từ method `GetPersonalInfo`. Biểu thức `(per.FirstName, per.MiddleName, per.LastName, per.Age)` là tuple literal.

```csharp
public (string, string, string, int) GetPersonalInfo(string id)
{
    PersonInfo per = PersonInfo.RetrieveInfoById(id);
    return (per.FirstName, per.MiddleName, per.LastName, per.Age);
}
```

Bên gọi có thể nhận kết quả như sau:

```csharp
var person = GetPersonalInfo("111111111");
Console.WriteLine($"{person.Item1} {person.Item3}: age = {person.Item4}");
```

Bạn cũng có thể đặt tên cho các phần tử tuple:

```csharp
public (string FName, string MName, string LName, int Age) GetPersonalInfo(string id)
{
    PersonInfo per = PersonInfo.RetrieveInfoById(id);
    return (per.FirstName, per.MiddleName, per.LastName, per.Age);
}
```

Lúc này bạn dùng tên thay vì `Item1`, `Item2`,...:

```csharp
var person = GetPersonalInfo("111111111");
Console.WriteLine($"{person.FName} {person.LName}: age = {person.Age}");
```

Nếu method nhận một array (mảng) làm tham số và sửa đổi giá trị các phần tử, method không cần trả về array. Vì C# truyền tất cả reference types bằng giá trị, và giá trị của biến array chính là địa chỉ của array đó. Trong ví dụ sau, các thay đổi với mảng `values` trong method `DoubleValues` có hiệu lực ở bên ngoài method.

```csharp
public static class ArrayValueExample
{
    static void Main()
    {
        int[] values = [2, 4, 6, 8];
        DoubleValues(values);
        foreach (var value in values)
        {
            Console.Write("{0}  ", value);
        }
    }

    public static void DoubleValues(int[] arr)
    {
        for (var ctr = 0; ctr <= arr.GetUpperBound(0); ctr++)
        {
            arr[ctr] *= 2;
        }
    }
}
// The example displays the following output:
//       4  8  12  16
```

## Extension members (thành viên mở rộng)

Thông thường có hai cách thêm method vào một type có sẵn:

- Sửa mã nguồn của type đó. Nhưng nếu bạn thêm field dữ liệu private, đây sẽ là một breaking change (thay đổi phá vỡ).
- Định nghĩa method mới trong một derived class. Cách này không dùng được với struct hay enum, và cũng không thêm được method vào sealed class.

Extension members cho phép bạn "thêm" thành viên vào type có sẵn mà không cần sửa type hay dùng kế thừa. Extension method không nhất thiết phải nằm cùng assembly với type nó mở rộng. Bạn gọi extension method như thể nó là thành viên có sẵn của type đó.

Xem thêm [Thành viên mở rộng](programming-guide/classes-and-structs/extension-methods.md).

## Async Methods (phương thức bất đồng bộ)

Tính năng async cho phép bạn gọi các method bất đồng bộ (asynchronous method) mà không cần dùng callback tường minh hay tự chia nhỏ mã thủ công.

Nếu đánh dấu method bằng modifier [async](language-reference/keywords/async.md), bạn có thể dùng toán tử [await](language-reference/operators/await.md) trong method đó. Khi gặp biểu thức `await`, nếu task chưa hoàn thành, điều khiển trả về bên gọi và method tạm dừng cho tới khi task xong.

> [!NOTE]
> Một async method trả về bên gọi khi nó gặp `await` đầu tiên trên task chưa hoàn thành, hoặc khi chạy tới cuối method -- tuỳ điều kiện nào tới trước.

Async method thường có kiểu trả về là [`Task<T>`](https://learn.microsoft.com/dotnet/api/system.threading.tasks.task-1), [`Task`](https://learn.microsoft.com/dotnet/api/system.threading.tasks.task), [`IAsyncEnumerable<T>`](https://learn.microsoft.com/dotnet/api/system.collections.generic.iasyncenumerable-1) hoặc `void`. Kiểu `void` chủ yếu dùng cho event handlers (bắt buộc phải là `void`). Async method trả về `void` không thể await được, và bên gọi không thể bắt exception mà method ném ra. Async method cũng có thể có [kiểu trả về giống Task bất kỳ](language-reference/keywords/async.md#return-types).

Trong ví dụ sau, `DelayAsync` là async method trả về số nguyên. Vì là async, khai báo method phải có kiểu trả về `Task<int>`. Do đó, biểu thức `await` trong `DoSomethingAsync` cho ra một số nguyên.

```csharp
class Program
{
    static Task Main() => DoSomethingAsync();

    static async Task DoSomethingAsync()
    {
        Task<int> delayTask = DelayAsync();
        int result = await delayTask;

        // The previous two statements may be combined into
        // the following statement.
        //int result = await DelayAsync();

        Console.WriteLine($"Result: {result}");
    }

    static async Task<int> DelayAsync()
    {
        await Task.Delay(100);
        return 5;
    }
}
// Example output:
//   Result: 5
```

Async method không thể khai báo tham số [in](language-reference/keywords/method-parameters.md#in-parameter-modifier), [ref](language-reference/keywords/ref.md) hay [out](language-reference/keywords/method-parameters.md#out-parameter-modifier), nhưng có thể gọi các method khác có những tham số đó.

Xem thêm: [Lập trình bất đồng bộ](asynchronous-programming/index.md) và [Kiểu trả về bất đồng bộ](asynchronous-programming/async-return-types.md).

## Expression-bodied members (thành viên thân biểu thức)

Nếu method chỉ trả về kết quả của một biểu thức hoặc chỉ có một câu lệnh duy nhất, bạn có thể viết ngắn gọn bằng `=>`:

```csharp
public Point Move(int dx, int dy) => new Point(x + dx, y + dy);
public void Print() => Console.WriteLine(First + " " + Last);
// Works with operators, properties, and indexers too.
public static Complex operator +(Complex a, Complex b) => a.Add(b);
public string Name => First + " " + Last;
public Customer this[long id] => store.LookupCustomer(id);
```

Nếu method trả về `void` hoặc là async method, thân method phải là statement expression (giống lambda). Với properties và indexers, chúng phải là read-only và bạn không cần từ khoá `get`.

## Iterators (bộ lặp)

Iterator cho phép bạn duyệt qua một collection (như list hay array) theo cách tuỳ chỉnh. Iterator dùng câu lệnh [yield return](language-reference/statements/yield.md) để trả về từng phần tử một. Khi gặp `yield return`, vị trí hiện tại được lưu lại để lần sau người gọi có thể yêu cầu phần tử tiếp theo.

Kiểu trả về của iterator có thể là [`IEnumerable`](https://learn.microsoft.com/dotnet/api/system.collections.ienumerable), [`IEnumerable<T>`](https://learn.microsoft.com/dotnet/api/system.collections.generic.ienumerable-1), [`IAsyncEnumerable<T>`](https://learn.microsoft.com/dotnet/api/system.collections.generic.iasyncenumerable-1), [`IEnumerator`](https://learn.microsoft.com/dotnet/api/system.collections.ienumerator) hoặc [`IEnumerator<T>`](https://learn.microsoft.com/dotnet/api/system.collections.generic.ienumerator-1).

Xem thêm [Bộ lặp](programming-guide/concepts/iterators.md).

## Xem thêm

- [Bổ từ truy cập](language-reference/keywords/access-modifiers.md)
- [Class tĩnh và thành viên class tĩnh](programming-guide/classes-and-structs/static-classes-and-static-class-members.md)
- [Kế thừa](fundamentals/object-oriented/inheritance.md)
- [Class trừu tượng, sealed và thành viên](programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)
- [params](language-reference/keywords/method-parameters.md#params-modifier)
- [out](language-reference/keywords/method-parameters.md#out-parameter-modifier)
- [ref](language-reference/keywords/ref.md)
- [in](language-reference/keywords/method-parameters.md#in-parameter-modifier)
- [Truyền tham số](language-reference/keywords/method-parameters.md)
