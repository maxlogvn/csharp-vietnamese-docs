---
title: Xây dựng Expression Trees
description: Tìm hiểu về các kỹ thuật xây dựng expression trees.
ms.date: 03/07/2023
---

# Xây dựng expression trees

Tất cả các expression tree bạn thấy cho tới nay đều do trình biên dịch C# tạo ra. Bạn tạo một lambda expression (biểu thức lambda) gán cho một variable (biến) có kiểu `Expression<Func<T>>` hoặc một kiểu tương tự. Trong nhiều tình huống, bạn cần xây dựng một expression (biểu thức) trong bộ nhớ tại thời điểm chạy (run time).

Expression trees là bất biến (immutable). Tính bất biến có nghĩa là bạn phải xây dựng cây từ leaves (lá) lên tới root (gốc). Các API bạn dùng để xây dựng expression trees phản ánh điều này: các method (phương thức) bạn dùng để xây dựng một node (nút) nhận tất cả các node con của nó làm tham số. Hãy cùng xem qua một vài ví dụ để minh hoạ các kỹ thuật này.

## Tạo các node

Bắt đầu với phép cộng mà bạn đã thấy trong các phần trước:

```csharp
Expression<Func<int>> sum = () => 1 + 2;
```

Để xây dựng expression tree đó, trước tiên bạn xây dựng các node lá. Các node lá là các hằng số (constants). Sử dụng method [`Expression.Constant`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.expression.constant) để tạo các node:

```csharp
var one = Expression.Constant(1, typeof(int));
var two = Expression.Constant(2, typeof(int));
```

Tiếp theo, xây dựng biểu thức cộng:

```csharp
var addition = Expression.Add(one, two);
```

Sau khi đã xây dựng biểu thức cộng, bạn tạo biểu thức lambda:

```csharp
var lambda = Expression.Lambda(addition);
```

Biểu thức lambda này không chứa tham số nào. Ở phần sau, bạn sẽ thấy cách ánh xạ các đối số (arguments) thành tham số (parameters) và xây dựng các biểu thức phức tạp hơn.

Đối với các biểu thức như thế này, bạn có thể kết hợp tất cả các lời gọi thành một câu lệnh duy nhất:

```csharp
var lambda2 = Expression.Lambda(
    Expression.Add(
        Expression.Constant(1, typeof(int)),
        Expression.Constant(2, typeof(int))
    )
);
```

## Xây dựng một cây

Phần trước đã trình bày những điều cơ bản về xây dựng expression tree trong bộ nhớ. Các cây phức tạp hơn thường có nhiều loại node hơn và nhiều node hơn trong cây. Hãy cùng xem thêm một ví dụ nữa và tìm hiểu hai loại node thường được xây dựng khi tạo expression trees: node tham số (argument nodes) và node lời gọi method (method call nodes). Chúng ta sẽ xây dựng một expression tree cho biểu thức sau:

```csharp
Expression<Func<double, double, double>> distanceCalc =
    (x, y) => Math.Sqrt(x * x + y * y);
```

Bạn bắt đầu bằng cách tạo các biểu thức tham số cho `x` và `y`:

```csharp
var xParameter = Expression.Parameter(typeof(double), "x");
var yParameter = Expression.Parameter(typeof(double), "y");
```

Tạo các biểu thức nhân và cộng theo pattern bạn đã thấy:

```csharp
var xSquared = Expression.Multiply(xParameter, xParameter);
var ySquared = Expression.Multiply(yParameter, yParameter);
var sum = Expression.Add(xSquared, ySquared);
```

Tiếp theo, bạn cần tạo một biểu thức lời gọi method (method call expression) cho lời gọi `Math.Sqrt`.

```csharp
var sqrtMethod = typeof(Math).GetMethod("Sqrt", new[] { typeof(double) }) ?? throw new InvalidOperationException("Math.Sqrt not found!");
var distance = Expression.Call(sqrtMethod, sum);
```

Lời gọi `GetMethod` có thể trả về `null` nếu method không được tìm thấy. Điều đó thường là do bạn đã viết sai tên method. Nếu không, nó có thể có nghĩa là assembly (tập hợp) cần thiết chưa được tải. Cuối cùng, bạn đặt lời gọi method vào một biểu thức lambda và đảm bảo định nghĩa các tham số cho biểu thức lambda:

```csharp
var distanceLambda = Expression.Lambda(
    distance,
    xParameter,
    yParameter);
```

Trong ví dụ phức tạp hơn này, bạn thấy thêm một vài kỹ thuật thường cần để tạo expression trees.

Đầu tiên, bạn cần tạo các object (đối tượng) đại diện cho tham số hoặc biến địa phương (local variables) trước khi sử dụng chúng. Sau khi đã tạo các object đó, bạn có thể dùng chúng trong expression tree ở bất cứ đâu cần.

Thứ hai, bạn cần sử dụng một tập con của Reflection APIs để tạo một object [`MethodInfo`](https://learn.microsoft.com/dotnet/api/system.reflection.methodinfo) nhằm tạo expression tree truy cập vào method đó. Bạn phải giới hạn bản thân ở tập con các Reflection APIs có sẵn trên nền tảng .NET Core. Những kỹ thuật này cũng mở rộng cho các expression tree khác.

## Xây dựng mã chuyên sâu

Bạn không bị giới hạn trong những gì có thể xây dựng bằng các API này. Tuy nhiên, expression tree càng phức tạp thì mã càng khó quản lý và khó đọc.

Hãy xây dựng một expression tree tương đương với đoạn mã sau:

```csharp
Func<int, int> factorialFunc = (n) =>
{
    var res = 1;
    while (n > 1)
    {
        res = res * n;
        n--;
    }
    return res;
};
```

Đoạn mã trên không xây dựng expression tree, mà chỉ xây dựng delegate (uỷ quyền). Sử dụng class `Expression`, bạn không thể xây dựng các lambda dạng câu lệnh (statement lambdas). Dưới đây là mã cần thiết để xây dựng cùng chức năng đó. Không có API nào để xây dựng vòng lặp `while`, thay vào đó bạn cần xây dựng một vòng lặp (loop) chứa một điều kiện kiểm tra (conditional test) và một nhãn đích (label target) để thoát khỏi vòng lặp.

```csharp
var nArgument = Expression.Parameter(typeof(int), "n");
var result = Expression.Variable(typeof(int), "result");

// Creating a label that represents the return value
LabelTarget label = Expression.Label(typeof(int));

var initializeResult = Expression.Assign(result, Expression.Constant(1));

// This is the inner block that performs the multiplication,
// and decrements the value of 'n'
var block = Expression.Block(
    Expression.Assign(result,
        Expression.Multiply(result, nArgument)),
    Expression.PostDecrementAssign(nArgument)
);

// Creating a method body.
BlockExpression body = Expression.Block(
    new[] { result },
    initializeResult,
    Expression.Loop(
        Expression.IfThenElse(
            Expression.GreaterThan(nArgument, Expression.Constant(1)),
            block,
            Expression.Break(label, result)
        ),
        label
    )
);
```

Mã để xây dựng expression tree cho hàm giai thừa dài hơn đáng kể, phức tạp hơn, và có rất nhiều nhãn (labels), câu lệnh break (break statements) và các thành phần khác mà bạn thường muốn tránh trong công việc viết mã hàng ngày.

Đối với phần này, bạn đã viết mã để duyệt qua mọi node trong expression tree này và ghi thông tin về các node được tạo trong mẫu này. Bạn có thể [xem hoặc tải mã mẫu](https://github.com/dotnet/samples/tree/main/csharp/expression-trees) tại kho GitHub dotnet/docs. Hãy tự mình thử nghiệm bằng cách xây dựng và chạy các mẫu.

## Ánh xạ cấu trúc mã sang biểu thức

Ví dụ mã sau đây minh hoạ một expression tree đại diện cho biểu thức lambda `num => num < 5` bằng cách sử dụng API.

```csharp
// Manually build the expression tree for
// the lambda expression num => num < 5.
ParameterExpression numParam = Expression.Parameter(typeof(int), "num");
ConstantExpression five = Expression.Constant(5, typeof(int));
BinaryExpression numLessThanFive = Expression.LessThan(numParam, five);
Expression<Func<int, bool>> lambda1 =
    Expression.Lambda<Func<int, bool>>(
        numLessThanFive,
        new ParameterExpression[] { numParam });
```

Expression trees API cũng hỗ trợ các biểu thức gán (assignments) và điều khiển luồng (control flow) như vòng lặp (loops), khối điều kiện (conditional blocks), và khối `try-catch`. Bằng cách sử dụng API, bạn có thể tạo ra các expression tree phức tạp hơn những gì trình biên dịch C# có thể tạo từ biểu thức lambda. Ví dụ sau đây minh hoạ cách tạo một expression tree tính giai thừa của một số.

```csharp
// Creating a parameter expression.
ParameterExpression value = Expression.Parameter(typeof(int), "value");

// Creating an expression to hold a local variable.
ParameterExpression result = Expression.Parameter(typeof(int), "result");

// Creating a label to jump to from a loop.
LabelTarget label = Expression.Label(typeof(int));

// Creating a method body.
BlockExpression block = Expression.Block(
    // Adding a local variable.
    new[] { result },
    // Assigning a constant to a local variable: result = 1
    Expression.Assign(result, Expression.Constant(1)),
        // Adding a loop.
        Expression.Loop(
           // Adding a conditional block into the loop.
           Expression.IfThenElse(
               // Condition: value > 1
               Expression.GreaterThan(value, Expression.Constant(1)),
               // If true: result *= value --
               Expression.MultiplyAssign(result,
                   Expression.PostDecrementAssign(value)),
               // If false, exit the loop and go to the label.
               Expression.Break(label, result)
           ),
       // Label to jump to.
       label
    )
);

// Compile and execute an expression tree.
int factorial = Expression.Lambda<Func<int, int>>(block, value).Compile()(5);

Console.WriteLine(factorial);
// Prints 120.
```

Để biết thêm thông tin, hãy xem [Generating Dynamic Methods with Expression Trees in Visual Studio 2010](https://devblogs.microsoft.com/csharpfaq/generating-dynamic-methods-with-expression-trees-in-visual-studio-2010/), nội dung cũng áp dụng cho các phiên bản Visual Studio mới hơn.
