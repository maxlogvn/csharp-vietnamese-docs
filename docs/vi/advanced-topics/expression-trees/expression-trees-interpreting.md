---
title: Diễn giải biểu thức
description: Học cách viết mã để kiểm tra cấu trúc của một expression tree (cây biểu thức).
ms.date: 03/06/2023
---

# Diễn giải Interpret expressions

Ví dụ mã sau đây minh hoạ cách phân tích expression tree (cây biểu thức) đại diện cho lambda expression `num => num < 5` thành các phần của nó.

```csharp
// Add the following using directive to your code file:
// using System.Linq.Expressions;

// Create an expression tree.
Expression<Func<int, bool>> exprTree = num => num < 5;

// Decompose the expression tree.
ParameterExpression param = (ParameterExpression)exprTree.Parameters[0];
BinaryExpression operation = (BinaryExpression)exprTree.Body;
ParameterExpression left = (ParameterExpression)operation.Left;
ConstantExpression right = (ConstantExpression)operation.Right;

Console.WriteLine($"Decomposed expression: {param.Name} => {left.Name} {operation.NodeType} {right.Value}");

// This code produces the following output:

// Decomposed expression: num => num LessThan 5
```

Bây giờ, hãy viết một số mã để kiểm tra cấu trúc của một *expression tree (cây biểu thức)*. Mỗi node trong cây biểu thức là một object (đối tượng) của một class (lớp) dẫn xuất từ `Expression`.

Thiết kế đó giúp cho việc duyệt qua tất cả các node trong cây biểu thức trở thành một thao tác đệ quy tương đối đơn giản. Chiến lược chung là bắt đầu tại node gốc và xác định xem nó thuộc loại node nào.

Nếu node có node con, hãy đệ quy duyệt các node con. Tại mỗi node con, lặp lại quy trình đã dùng ở node gốc: xác định loại, và nếu loại đó có node con, hãy duyệt từng node con.

## Kiểm tra biểu thức không có node con

Hãy bắt đầu bằng cách duyệt từng node trong một cây biểu thức đơn giản. Sau đây là mã tạo ra một constant expression (biểu thức hằng) và sau đó kiểm tra các thuộc tính của nó:

```csharp
var constant = Expression.Constant(24, typeof(int));

Console.WriteLine($"This is a/an {constant.NodeType} expression type");
Console.WriteLine($"The type of the constant value is {constant.Type}");
Console.WriteLine($"The value of the constant value is {constant.Value}");
```

Đoạn mã trên in ra kết quả sau:

```output
This is a/an Constant expression type
The type of the constant value is System.Int32
The value of the constant value is 24
```

Bây giờ, hãy viết mã kiểm tra biểu thức này và ghi ra một số thuộc tính quan trọng về nó.

## Biểu thức cộng (Addition expression)

Hãy bắt đầu với ví dụ phép cộng từ phần giới thiệu của chủ đề này.

```csharp
Expression<Func<int>> sum = () => 1 + 2;
```

> [!NOTE]
> Đừng dùng `var` để khai báo cây biểu thức này, vì kiểu tự nhiên của delegate (uỷ quyền) là `Func<int>`, không phải `Expression<Func<int>>`.

Node gốc là một `LambdaExpression`. Để lấy được mã cần quan tâm ở phía bên phải của toán tử `=>`, bạn cần tìm một trong các node con của `LambdaExpression`. Bạn làm điều đó với tất cả các biểu thức trong phần này. Node cha giúp chúng ta tìm ra kiểu trả về của `LambdaExpression`.

Để kiểm tra từng node trong biểu thức này, bạn cần duyệt đệ quy nhiều node. Sau đây là cách triển khai đầu tiên đơn giản:

```csharp
Expression<Func<int, int, int>> addition = (a, b) => a + b;

Console.WriteLine($"This expression is a {addition.NodeType} expression type");
Console.WriteLine($"The name of the lambda is {((addition.Name == null) ? "<null>" : addition.Name)}");
Console.WriteLine($"The return type is {addition.ReturnType.ToString()}");
Console.WriteLine($"The expression has {addition.Parameters.Count} arguments. They are:");
foreach (var argumentExpression in addition.Parameters)
{
    Console.WriteLine($"\tParameter Type: {argumentExpression.Type.ToString()}, Name: {argumentExpression.Name}");
}

var additionBody = (BinaryExpression)addition.Body;
Console.WriteLine($"The body is a {additionBody.NodeType} expression");
Console.WriteLine($"The left side is a {additionBody.Left.NodeType} expression");
var left = (ParameterExpression)additionBody.Left;
Console.WriteLine($"\tParameter Type: {left.Type.ToString()}, Name: {left.Name}");
Console.WriteLine($"The right side is a {additionBody.Right.NodeType} expression");
var right = (ParameterExpression)additionBody.Right;
Console.WriteLine($"\tParameter Type: {right.Type.ToString()}, Name: {right.Name}");
```

Mẫu này in ra kết quả sau:

```output
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 2 arguments. They are:
        Parameter Type: System.Int32, Name: a
        Parameter Type: System.Int32, Name: b
The body is a/an Add expression
The left side is a Parameter expression
        Parameter Type: System.Int32, Name: a
The right side is a Parameter expression
        Parameter Type: System.Int32, Name: b
```

Bạn có thể thấy có nhiều sự lặp lại trong đoạn mã trên. Hãy làm sạch nó và xây dựng một trình duyệt node biểu thức tổng quát hơn. Điều đó đòi hỏi chúng ta phải viết một thuật toán đệ quy. Bất kỳ node nào cũng có thể thuộc loại có node con. Bất kỳ node nào có node con đều yêu cầu chúng ta duyệt các node con đó và xác định node đó là gì. Sau đây là phiên bản đã được làm sạch, sử dụng đệ quy để duyệt các phép cộng:

```csharp
using System.Linq.Expressions;

namespace Visitors;
// Base Visitor class:
public abstract class Visitor
{
    private readonly Expression node;

    protected Visitor(Expression node) => this.node = node;

    public abstract void Visit(string prefix);

    public ExpressionType NodeType => node.NodeType;
    public static Visitor CreateFromExpression(Expression node) =>
        node.NodeType switch
        {
            ExpressionType.Constant => new ConstantVisitor((ConstantExpression)node),
            ExpressionType.Lambda => new LambdaVisitor((LambdaExpression)node),
            ExpressionType.Parameter => new ParameterVisitor((ParameterExpression)node),
            ExpressionType.Add => new BinaryVisitor((BinaryExpression)node),
            _ => throw new NotImplementedException($"Node not processed yet: {node.NodeType}"),
        };
}

// Lambda Visitor
public class LambdaVisitor : Visitor
{
    private readonly LambdaExpression node;
    public LambdaVisitor(LambdaExpression node) : base(node) => this.node = node;

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This expression is a {NodeType} expression type");
        Console.WriteLine($"{prefix}The name of the lambda is {((node.Name == null) ? "<null>" : node.Name)}");
        Console.WriteLine($"{prefix}The return type is {node.ReturnType}");
        Console.WriteLine($"{prefix}The expression has {node.Parameters.Count} argument(s). They are:");
        // Visit each parameter:
        foreach (var argumentExpression in node.Parameters)
        {
            var argumentVisitor = CreateFromExpression(argumentExpression);
            argumentVisitor.Visit(prefix + "\t");
        }
        Console.WriteLine($"{prefix}The expression body is:");
        // Visit the body:
        var bodyVisitor = CreateFromExpression(node.Body);
        bodyVisitor.Visit(prefix + "\t");
    }
}

// Binary Expression Visitor:
public class BinaryVisitor : Visitor
{
    private readonly BinaryExpression node;
    public BinaryVisitor(BinaryExpression node) : base(node) => this.node = node;

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This binary expression is a {NodeType} expression");
        var left = CreateFromExpression(node.Left);
        Console.WriteLine($"{prefix}The Left argument is:");
        left.Visit(prefix + "\t");
        var right = CreateFromExpression(node.Right);
        Console.WriteLine($"{prefix}The Right argument is:");
        right.Visit(prefix + "\t");
    }
}

// Parameter visitor:
public class ParameterVisitor : Visitor
{
    private readonly ParameterExpression node;
    public ParameterVisitor(ParameterExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This is an {NodeType} expression type");
        Console.WriteLine($"{prefix}Type: {node.Type}, Name: {node.Name}, ByRef: {node.IsByRef}");
    }
}

// Constant visitor:
public class ConstantVisitor : Visitor
{
    private readonly ConstantExpression node;
    public ConstantVisitor(ConstantExpression node) : base(node) => this.node = node;

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This is an {NodeType} expression type");
        Console.WriteLine($"{prefix}The type of the constant value is {node.Type}");
        Console.WriteLine($"{prefix}The value of the constant value is {node.Value}");
    }
}
```

Thuật toán này là nền tảng của một thuật toán duyệt bất kỳ `LambdaExpression` nào. Đoạn mã bạn tạo chỉ xử lý một tập nhỏ các loại node cây biểu thức có thể gặp. Tuy nhiên, bạn vẫn có thể học được khá nhiều từ những gì nó tạo ra. (Trường hợp `default` trong method `Visitor.CreateFromExpression` sẽ in ra thông báo lỗi khi gặp một loại node mới. Nhờ đó, bạn biết cần thêm một loại biểu thức mới.)

Khi bạn chạy trình duyệt này trên biểu thức cộng ở trên, bạn nhận được kết quả sau:

```output
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 2 argument(s). They are:
        This is an Parameter expression type
        Type: System.Int32, Name: a, ByRef: False
        This is an Parameter expression type
        Type: System.Int32, Name: b, ByRef: False
The expression body is:
        This binary expression is a Add expression
        The Left argument is:
                This is an Parameter expression type
                Type: System.Int32, Name: a, ByRef: False
        The Right argument is:
                This is an Parameter expression type
                Type: System.Int32, Name: b, ByRef: False
```

Bây giờ bạn đã xây dựng được một trình duyệt tổng quát hơn, bạn có thể duyệt và xử lý nhiều loại biểu thức khác nhau.

## Biểu thức cộng với nhiều toán hạng hơn

Hãy thử một ví dụ phức tạp hơn, nhưng vẫn giới hạn ở các loại node chỉ là phép cộng:

```csharp
Expression<Func<int>> sum = () => 1 + 2 + 3 + 4;
```

Trước khi chạy các ví dụ này trên thuật toán duyệt, hãy thử một bài tập suy luận để đoán kết quả sẽ là gì. Hãy nhớ rằng toán tử `+` là một *toán tử nhị phân (binary operator)*: nó phải có hai node con, đại diện cho toán hạng trái và phải. Có một số cách để xây dựng một cây đúng:

```csharp
Expression<Func<int>> sum1 = () => 1 + (2 + (3 + 4));
Expression<Func<int>> sum2 = () => ((1 + 2) + 3) + 4;

Expression<Func<int>> sum3 = () => (1 + 2) + (3 + 4);
Expression<Func<int>> sum4 = () => 1 + ((2 + 3) + 4);
Expression<Func<int>> sum5 = () => (1 + (2 + 3)) + 4;
```

Bạn có thể thấy sự phân tách thành hai đáp án khả thi để làm nổi bật hướng đi hứa hẹn nhất. Cách đầu tiên đại diện cho biểu thức *kết hợp phải (right associative)*. Cách thứ hai đại diện cho biểu thức *kết hợp trái (left associative)*. Ưu điểm của cả hai định dạng này là chúng có thể mở rộng cho bất kỳ số lượng biểu thức cộng nào.

Nếu bạn chạy biểu thức này qua trình duyệt, bạn sẽ thấy kết quả sau, xác nhận rằng biểu thức cộng đơn giản là *kết hợp trái (left associative)*.

Để chạy mẫu này và thấy toàn bộ cây biểu thức, bạn cần thay đổi một điều trong cây biểu thức nguồn. Khi cây biểu thức chứa tất cả các hằng số, cây kết quả chỉ đơn giản chứa giá trị hằng `10`. Trình biên dịch thực hiện tất cả các phép cộng và rút gọn biểu thức về dạng đơn giản nhất. Chỉ cần thêm một variable (biến) vào biểu thức là đủ để thấy cây gốc:

```csharp
Expression<Func<int, int>> sum = (a) => 1 + a + 3 + 4;
```

Tạo một trình duyệt cho tổng này và chạy nó, bạn sẽ thấy kết quả:

```output
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 1 argument(s). They are:
        This is an Parameter expression type
        Type: System.Int32, Name: a, ByRef: False
The expression body is:
        This binary expression is a Add expression
        The Left argument is:
                This binary expression is a Add expression
                The Left argument is:
                        This binary expression is a Add expression
                        The Left argument is:
                                This is an Constant expression type
                                The type of the constant value is System.Int32
                                The value of the constant value is 1
                        The Right argument is:
                                This is an Parameter expression type
                                Type: System.Int32, Name: a, ByRef: False
                The Right argument is:
                        This is an Constant expression type
                        The type of the constant value is System.Int32
                        The value of the constant value is 3
        The Right argument is:
                This is an Constant expression type
                The type of the constant value is System.Int32
                The value of the constant value is 4
```

Bạn có thể chạy bất kỳ mẫu nào khác qua mã trình duyệt và xem cây mà nó biểu diễn. Sau đây là ví dụ về biểu thức `sum3` ở trên (với một tham số bổ sung để ngăn trình biên dịch tính toán hằng số):

```csharp
Expression<Func<int, int, int>> sum3 = (a, b) => (1 + a) + (3 + b);
```

Sau đây là kết quả từ trình duyệt:

```output
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 2 argument(s). They are:
        This is an Parameter expression type
        Type: System.Int32, Name: a, ByRef: False
        This is an Parameter expression type
        Type: System.Int32, Name: b, ByRef: False
The expression body is:
        This binary expression is a Add expression
        The Left argument is:
                This binary expression is a Add expression
                The Left argument is:
                        This is an Constant expression type
                        The type of the constant value is System.Int32
                        The value of the constant value is 1
                The Right argument is:
                        This is an Parameter expression type
                        Type: System.Int32, Name: a, ByRef: False
        The Right argument is:
                This binary expression is a Add expression
                The Left argument is:
                        This is an Constant expression type
                        The type of the constant value is System.Int32
                        The value of the constant value is 3
                The Right argument is:
                        This is an Parameter expression type
                        Type: System.Int32, Name: b, ByRef: False
```

Lưu ý rằng dấu ngoặc đơn không nằm trong kết quả. Không có node nào trong cây biểu thức đại diện cho dấu ngoặc đơn trong biểu thức đầu vào. Cấu trúc của cây biểu thức chứa tất cả thông tin cần thiết để thể hiện thứ tự ưu tiên.

## Mở rộng mẫu này

Mẫu này chỉ xử lý các cây biểu thức cơ bản nhất. Đoạn mã bạn đã thấy trong phần này chỉ xử lý các số nguyên hằng và toán tử nhị phân `+`. Là một mẫu cuối cùng, hãy cập nhật trình duyệt để xử lý một biểu thức phức tạp hơn. Hãy làm cho nó hoạt động với biểu thức giai thừa sau:

```csharp
Expression<Func<int, int>> factorial = (n) =>
    n == 0 ?
    1 :
    Enumerable.Range(1, n).Aggregate((product, factor) => product * factor);
```

Đoạn mã này đại diện cho một cách triển khai khả thi cho hàm *giai thừa (factorial)* trong toán học. Cách bạn viết mã này làm nổi bật hai hạn chế của việc xây dựng cây biểu thức bằng cách gán lambda expression cho `Expression`. Thứ nhất, statement lambda (lambda câu lệnh) không được phép. Điều đó có nghĩa là bạn không thể dùng vòng lặp, khối lệnh, câu lệnh if/else và các cấu trúc điều khiển khác thường thấy trong C#. Bạn bị giới hạn ở việc sử dụng expressions (biểu thức). Thứ hai, bạn không thể gọi đệ quy cùng một biểu thức. Bạn có thể làm điều đó nếu nó đã là một delegate, nhưng bạn không thể gọi nó dưới dạng cây biểu thức. Trong phần về [xây dựng cây biểu thức](expression-trees-building.md), bạn sẽ học các kỹ thuật để vượt qua những hạn chế này.

Trong biểu thức này, bạn sẽ gặp các node thuộc tất cả các loại sau:

1. Equal (biểu thức nhị phân)
2. Multiply (biểu thức nhị phân)
3. Conditional (biểu thức `? :`)
4. Method Call Expression (gọi `Range()` và `Aggregate()`)

Một cách để sửa đổi thuật toán duyệt là tiếp tục chạy nó và ghi lại loại node mỗi khi bạn gặp mệnh đề `default`. Sau một vài lần chạy, bạn sẽ thấy tất cả các node tiềm năng. Lúc đó, bạn đã có mọi thứ cần thiết. Kết quả sẽ giống như thế này:

```csharp
public static Visitor CreateFromExpression(Expression node) =>
    node.NodeType switch
    {
        ExpressionType.Constant    => new ConstantVisitor((ConstantExpression)node),
        ExpressionType.Lambda      => new LambdaVisitor((LambdaExpression)node),
        ExpressionType.Parameter   => new ParameterVisitor((ParameterExpression)node),
        ExpressionType.Add         => new BinaryVisitor((BinaryExpression)node),
        ExpressionType.Equal       => new BinaryVisitor((BinaryExpression)node),
        ExpressionType.Multiply    => new BinaryVisitor((BinaryExpression)node),
        ExpressionType.Conditional => new ConditionalVisitor((ConditionalExpression)node),
        ExpressionType.Call        => new MethodCallVisitor((MethodCallExpression)node),
        _ => throw new NotImplementedException($"Node not processed yet: {node.NodeType}"),
    };
```

`ConditionalVisitor` và `MethodCallVisitor` xử lý hai node đó:

```csharp
public class ConditionalVisitor : Visitor
{
    private readonly ConditionalExpression node;
    public ConditionalVisitor(ConditionalExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This expression is a {NodeType} expression");
        var testVisitor = Visitor.CreateFromExpression(node.Test);
        Console.WriteLine($"{prefix}The Test for this expression is:");
        testVisitor.Visit(prefix + "\t");
        var trueVisitor = Visitor.CreateFromExpression(node.IfTrue);
        Console.WriteLine($"{prefix}The True clause for this expression is:");
        trueVisitor.Visit(prefix + "\t");
        var falseVisitor = Visitor.CreateFromExpression(node.IfFalse);
        Console.WriteLine($"{prefix}The False clause for this expression is:");
        falseVisitor.Visit(prefix + "\t");
    }
}

public class MethodCallVisitor : Visitor
{
    private readonly MethodCallExpression node;
    public MethodCallVisitor(MethodCallExpression node) : base(node)
    {
        this.node = node;
    }

    public override void Visit(string prefix)
    {
        Console.WriteLine($"{prefix}This expression is a {NodeType} expression");
        if (node.Object == null)
            Console.WriteLine($"{prefix}This is a static method call");
        else
        {
            Console.WriteLine($"{prefix}The receiver (this) is:");
            var receiverVisitor = Visitor.CreateFromExpression(node.Object);
            receiverVisitor.Visit(prefix + "\t");
        }

        var methodInfo = node.Method;
        Console.WriteLine($"{prefix}The method name is {methodInfo.DeclaringType}.{methodInfo.Name}");
        // There is more here, like generic arguments, and so on.
        Console.WriteLine($"{prefix}The Arguments are:");
        foreach (var arg in node.Arguments)
        {
            var argVisitor = Visitor.CreateFromExpression(arg);
            argVisitor.Visit(prefix + "\t");
        }
    }
}
```

Và kết quả cho cây biểu thức sẽ là:

```output
This expression is a/an Lambda expression type
The name of the lambda is <null>
The return type is System.Int32
The expression has 1 argument(s). They are:
        This is an Parameter expression type
        Type: System.Int32, Name: n, ByRef: False
The expression body is:
        This expression is a Conditional expression
        The Test for this expression is:
                This binary expression is a Equal expression
                The Left argument is:
                        This is an Parameter expression type
                        Type: System.Int32, Name: n, ByRef: False
                The Right argument is:
                        This is an Constant expression type
                        The type of the constant value is System.Int32
                        The value of the constant value is 0
        The True clause for this expression is:
                This is an Constant expression type
                The type of the constant value is System.Int32
                The value of the constant value is 1
        The False clause for this expression is:
                This expression is a Call expression
                This is a static method call
                The method name is System.Linq.Enumerable.Aggregate
                The Arguments are:
                        This expression is a Call expression
                        This is a static method call
                        The method name is System.Linq.Enumerable.Range
                        The Arguments are:
                                This is an Constant expression type
                                The type of the constant value is System.Int32
                                The value of the constant value is 1
                                This is an Parameter expression type
                                Type: System.Int32, Name: n, ByRef: False
                        This expression is a Lambda expression type
                        The name of the lambda is <null>
                        The return type is System.Int32
                        The expression has 2 arguments. They are:
                                This is an Parameter expression type
                                Type: System.Int32, Name: product, ByRef: False
                                This is an Parameter expression type
                                Type: System.Int32, Name: factor, ByRef: False
                        The expression body is:
                                This binary expression is a Multiply expression
                                The Left argument is:
                                        This is an Parameter expression type
                                        Type: System.Int32, Name: product, ByRef: False
                                The Right argument is:
                                        This is an Parameter expression type
                                        Type: System.Int32, Name: factor, ByRef: False
```

## Mở rộng thư viện mẫu

Các mẫu trong phần này trình bày các kỹ thuật cốt lõi để duyệt và kiểm tra các node trong cây biểu thức. Chúng đã đơn giản hoá các loại node bạn sẽ gặp để tập trung vào nhiệm vụ chính là duyệt và truy cập các node trong cây biểu thức.

Thứ nhất, các trình duyệt chỉ xử lý các hằng số là số nguyên. Giá trị hằng số có thể thuộc bất kỳ kiểu số nào khác, và ngôn ngữ C# hỗ trợ chuyển đổi và thăng cấp giữa các kiểu đó. Một phiên bản mạnh mẽ hơn của đoạn mã này sẽ phản ánh tất cả những khả năng đó.

Ngay cả ví dụ cuối cùng cũng chỉ nhận diện một tập con các loại node khả dụng. Bạn vẫn có thể đưa vào nhiều biểu thức khiến nó bị lỗi. Một triển khai đầy đủ được bao gồm trong .NET Standard với tên gọi [`ExpressionVisitor`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.expressionvisitor) và có thể xử lý tất cả các loại node.

Cuối cùng, thư viện được dùng trong bài viết này được xây dựng cho mục đích minh hoạ và học tập. Nó không được tối ưu hoá. Nó làm rõ cấu trúc và làm nổi bật các kỹ thuật dùng để duyệt các node và phân tích những gì có ở đó.

Dù có những hạn chế đó, bạn vẫn đang trên con đường tốt để viết các thuật toán đọc và hiểu cây biểu thức.
