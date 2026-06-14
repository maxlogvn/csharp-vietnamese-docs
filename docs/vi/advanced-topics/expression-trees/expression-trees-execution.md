---
title: Thực thi Expression Trees
description: Tìm hiểu về cách thực thi expression trees (cây biểu thức) bằng cách chuyển chúng thành các chỉ thị Intermediate Language (IL) có thể thực thi.
ms.date: 03/06/2023
---

# Thực thi Expression Trees

*Expression tree* (cây biểu thức) là một cấu trúc dữ liệu biểu diễn một đoạn mã. Nó không phải là mã đã được biên dịch và có thể thực thi. Nếu bạn muốn thực thi mã .NET được biểu diễn bởi một expression tree, bạn phải chuyển nó thành các chỉ thị IL có thể thực thi. Việc thực thi một expression tree có thể trả về một giá trị, hoặc chỉ thực hiện một hành động như gọi một method (phương thức).

Chỉ những expression tree biểu diễn lambda expression (biểu thức lambda) mới có thể thực thi được. Expression trees biểu diễn lambda expressions có kiểu [`LambdaExpression`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.lambdaexpression) hoặc [`Expression<TDelegate>`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.expression-1). Để thực thi các expression tree này, hãy gọi method [`LambdaExpression.Compile`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.lambdaexpression.compile) để tạo ra một delegate (uỷ quyền) có thể thực thi, sau đó gọi delegate đó.

> [!NOTE]
> Nếu kiểu của delegate không được biết, nghĩa là lambda expression thuộc kiểu [`LambdaExpression`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.lambdaexpression) chứ không phải [`Expression<TDelegate>`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.expression-1), hãy gọi method [`Delegate.DynamicInvoke`](https://learn.microsoft.com/dotnet/api/system.delegate.dynamicinvoke) trên delegate thay vì gọi trực tiếp.

Nếu một expression tree không biểu diễn một lambda expression, bạn có thể tạo một lambda expression mới có expression tree gốc làm body (phần thân) của nó, bằng cách gọi method [`Expression.Lambda<TDelegate>`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.expression.lambda). Sau đó, bạn có thể thực thi lambda expression như đã mô tả ở phần trước.

## Lambda expressions thành functions (hàm)

Bạn có thể chuyển bất kỳ `LambdaExpression` nào, hoặc bất kỳ kiểu dẫn xuất nào từ `LambdaExpression`, thành IL có thể thực thi. Các kiểu expression khác không thể được chuyển trực tiếp thành mã. Hạn chế này hầu như không ảnh hưởng gì trong thực tế. Lambda expressions là những kiểu expression duy nhất mà bạn muốn thực thi bằng cách chuyển thành intermediate language (IL) có thể thực thi. (Hãy nghĩ xem việc thực thi trực tiếp một [`ConstantExpression`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.constantexpression) có ý nghĩa gì không?) Bất kỳ expression tree nào là [`LambdaExpression`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.lambdaexpression), hoặc kiểu dẫn xuất từ `LambdaExpression`, đều có thể được chuyển thành IL. Kiểu expression [`Expression<TDelegate>`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.expression-1) là ví dụ cụ thể duy nhất trong thư viện .NET Core. Nó được dùng để biểu diễn một expression ánh xạ tới bất kỳ kiểu delegate nào. Bởi vì kiểu này ánh xạ tới một kiểu delegate, .NET có thể kiểm tra expression và sinh IL cho một delegate phù hợp khớp với signature (chữ ký) của lambda expression. Kiểu delegate dựa trên kiểu expression. Bạn phải biết kiểu trả về và danh sách tham số nếu bạn muốn sử dụng đối tượng delegate một cách strongly typed (an toàn về kiểu). Method `LambdaExpression.Compile()` trả về kiểu `Delegate`. Bạn phải cast (ép kiểu) nó về đúng kiểu delegate để có các công cụ kiểm tra danh sách tham số hoặc kiểu trả về tại thời điểm biên dịch.

Trong hầu hết các trường hợp, tồn tại một ánh xạ đơn giản giữa một expression và delegate tương ứng của nó. Ví dụ, một expression tree được biểu diễn bởi `Expression<Func<int>>` sẽ được chuyển thành delegate kiểu `Func<int>`. Đối với một lambda expression với bất kỳ kiểu trả về và danh sách tham số nào, luôn có một kiểu delegate là kiểu đích (target type) cho mã thực thi được biểu diễn bởi lambda expression đó.

Kiểu [`LambdaExpression`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.lambdaexpression) chứa các thành viên [`LambdaExpression.Compile`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.lambdaexpression.compile) và [`LambdaExpression.CompileToMethod`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.lambdaexpression.compiletomethod) mà bạn sẽ sử dụng để chuyển một expression tree thành mã thực thi. Method `Compile` tạo ra một delegate. Method `CompileToMethod` cập nhật một đối tượng [`MethodBuilder`](https://learn.microsoft.com/dotnet/api/system.reflection.emit.methodbuilder) với IL đại diện cho đầu ra đã biên dịch của expression tree.

> [!IMPORTANT]
> `CompileToMethod` chỉ khả dụng trong .NET Framework, không có trong .NET Core hoặc .NET 5 trở lên.

Bạn cũng có thể tuỳ chọn cung cấp một [`DebugInfoGenerator`](https://learn.microsoft.com/dotnet/api/system.runtime.compilerservices.debuginfogenerator) để nhận thông tin gỡ lỗi symbol cho đối tượng delegate đã được sinh ra. `DebugInfoGenerator` cung cấp đầy đủ thông tin gỡ lỗi về delegate đã được sinh.

Bạn có thể chuyển một expression thành delegate bằng đoạn mã sau:

```csharp
Expression<Func<int>> add = () => 1 + 2;
var func = add.Compile(); // Create Delegate
var answer = func(); // Invoke Delegate
Console.WriteLine(answer);
```

Ví dụ mã sau đây minh hoạ các kiểu cụ thể được sử dụng khi bạn biên dịch và thực thi một expression tree.

```csharp
Expression<Func<int, bool>> expr = num => num < 5;

// Compiling the expression tree into a delegate.
Func<int, bool> result = expr.Compile();

// Invoking the delegate and writing the result to the console.
Console.WriteLine(result(4));

// Prints True.

// You can also use simplified syntax
// to compile and run an expression tree.
// The following line can replace two previous statements.
Console.WriteLine(expr.Compile()(4));

// Also prints True.
```

Ví dụ mã sau đây minh hoạ cách thực thi một expression tree biểu diễn phép luỹ thừa bằng cách tạo một lambda expression và thực thi nó. Kết quả là giá trị luỹ thừa được hiển thị.

```csharp
// The expression tree to execute.
BinaryExpression be = Expression.Power(Expression.Constant(2d), Expression.Constant(3d));

// Create a lambda expression.
Expression<Func<double>> le = Expression.Lambda<Func<double>>(be);

// Compile the lambda expression.
Func<double> compiledExpression = le.Compile();

// Execute the lambda expression.
double result = compiledExpression();

// Display the result.
Console.WriteLine(result);

// This code produces the following output:
// 8
```

## Thực thi và vòng đời

Bạn thực thi mã bằng cách gọi delegate được tạo ra khi bạn gọi `LambdaExpression.Compile()`. Đoạn mã phía trước, `add.Compile()`, trả về một delegate. Bạn gọi delegate đó bằng cách gọi `func()`, và nó sẽ thực thi mã.

Delegate đó đại diện cho mã trong expression tree. Bạn có thể giữ lại tham chiếu đến delegate đó và gọi nó sau này. Bạn không cần phải biên dịch lại expression tree mỗi lần muốn thực thi mã mà nó biểu diễn. (Hãy nhớ rằng expression trees là immutable (bất biến), và việc biên dịch cùng một expression tree sau đó sẽ tạo ra một delegate thực thi cùng một mã.)

> [!CAUTION]
> Đừng tạo ra bất kỳ cơ chế caching phức tạp nào để tăng hiệu suất bằng cách tránh các lệnh gọi `Compile` không cần thiết. So sánh hai expression tree bất kỳ để xác định xem chúng có biểu diễn cùng một thuật toán hay không là một thao tác tốn thời gian. Thời gian tính toán bạn tiết kiệm được khi tránh các lệnh gọi `LambdaExpression.Compile()` thêm vào có khả năng bị tiêu tốn nhiều hơn bởi thời gian thực thi mã xác định xem hai expression tree khác nhau có tạo ra cùng mã thực thi hay không.

## Lưu ý quan trọng

Biên dịch một lambda expression thành một delegate và gọi delegate đó là một trong những thao tác đơn giản nhất bạn có thể thực hiện với một expression tree. Tuy nhiên, dù chỉ với thao tác đơn giản này, vẫn có những điều bạn cần lưu ý.

Lambda Expressions tạo ra closures (bao đóng) trên bất kỳ biến cục bộ nào được tham chiếu trong expression. Bạn phải đảm bảo rằng bất kỳ biến nào là một phần của delegate đều có thể sử dụng được tại vị trí bạn gọi `Compile` và khi bạn thực thi delegate kết quả. Trình biên dịch đảm bảo rằng các biến nằm trong phạm vi (scope). Tuy nhiên, nếu expression của bạn truy cập vào một biến triển khai `IDisposable`, mã của bạn có thể giải phóng (dispose) đối tượng trong khi nó vẫn được expression tree giữ lại.

Ví dụ, đoạn mã sau đây hoạt động tốt vì `int` không triển khai `IDisposable`:

```csharp
private static Func<int, int> CreateBoundFunc()
{
    var constant = 5; // constant is captured by the expression tree
    Expression<Func<int, int>> expression = (b) => constant + b;
    var rVal = expression.Compile();
    return rVal;
}
```

Delegate đã ghi lại (capture) một tham chiếu đến biến cục bộ `constant`. Biến đó có thể được truy cập bất kỳ lúc nào sau đó, khi function (hàm) được trả về bởi `CreateBoundFunc` thực thi.

Tuy nhiên, hãy xem xét class (lớp) hơi khiên cưỡng sau đây triển khai [`IDisposable`](https://learn.microsoft.com/dotnet/api/system.idisposable):

```csharp
public class Resource : IDisposable
{
    private bool _isDisposed = false;
    public int Argument
    {
        get
        {
            if (!_isDisposed)
                return 5;
            else throw new ObjectDisposedException("Resource");
        }
    }

    public void Dispose()
    {
        _isDisposed = true;
    }
}
```

Nếu bạn sử dụng nó trong một expression như trong đoạn mã sau, bạn sẽ nhận được [`ObjectDisposedException`](https://learn.microsoft.com/dotnet/api/system.objectdisposedexception) khi thực thi mã được tham chiếu bởi thuộc tính `Resource.Argument`:

```csharp
private static Func<int, int> CreateBoundResource()
{
    using (var constant = new Resource()) // constant is captured by the expression tree
    {
        Expression<Func<int, int>> expression = (b) => constant.Argument + b;
        var rVal = expression.Compile();
        return rVal;
    }
}
```

Delegate được trả về từ method này đã bao đóng (close over) đối tượng `constant`, nhưng đối tượng này đã bị giải phóng (disposed). (Nó bị giải phóng vì được khai báo trong câu lệnh `using`.)

Khi bạn thực thi delegate được trả về từ method này, bạn sẽ gặp `ObjectDisposedException` tại thời điểm thực thi.

Có vẻ kỳ lạ khi gặp lỗi runtime (lúc chạy) từ một cấu trúc được tạo ra tại thời điểm biên dịch, nhưng đó là thế giới bạn bước vào khi làm việc với expression trees.

Có rất nhiều biến thể của vấn đề này, nên rất khó để đưa ra hướng dẫn chung nhằm tránh nó. Hãy cẩn thận khi truy cập các biến cục bộ khi định nghĩa expressions, và cẩn thận khi truy cập trạng thái (state) trong đối tượng hiện tại (được biểu diễn bởi `this`) khi tạo một expression tree được trả về qua một API công khai.

Mã trong expression của bạn có thể tham chiếu đến các method hoặc property (thuộc tính) trong các assembly (tập hợp) khác. Assembly đó phải có thể truy cập được khi expression được định nghĩa, khi nó được biên dịch, và khi delegate kết quả được gọi. Bạn sẽ gặp lỗi `ReferencedAssemblyNotFoundException` trong trường hợp assembly không tồn tại.

## Tổng kết

Expression Trees biểu diễn lambda expressions có thể được biên dịch để tạo ra một delegate mà bạn có thể thực thi. Expression trees cung cấp một cơ chế để thực thi mã được biểu diễn bởi một expression tree.

Expression Tree biểu diễn mã sẽ được thực thi cho bất kỳ cấu trúc nào bạn tạo ra. Miễn là môi trường nơi bạn biên dịch và thực thi mã khớp với môi trường nơi bạn tạo expression, mọi thứ sẽ hoạt động như mong đợi. Khi điều đó không xảy ra, các lỗi có thể dự đoán trước và chúng sẽ bị phát hiện trong những lần kiểm thử đầu tiên của bạn với bất kỳ mã nào sử dụng expression trees.
