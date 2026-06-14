---
title: Dịch Expression Trees
description: Học cách truy cập từng node trong biểu thức cây khi xây dựng một bản sao đã được sửa đổi của biểu thức cây đó.
ms.date: 03/07/2023
---
# Biểu thức cây

Trong bài viết này, bạn sẽ học cách truy cập từng node trong một biểu thức cây (expression tree) đồng thời xây dựng một bản sao đã được sửa đổi của biểu thức cây đó. Bạn dịch biểu thức cây để hiểu được các thuật toán, nhờ đó có thể chuyển đổi chúng sang một môi trường khác. Bạn có thể thay đổi thuật toán đã được tạo ra. Bạn có thể thêm ghi log (logging), chặn các lời gọi method (intercept method calls) và theo dõi chúng, hoặc các mục đích khác.

Mã bạn viết để dịch một biểu thức cây là phần mở rộng của những gì bạn đã thấy trước đây khi truy cập tất cả các node trong một cây. Khi bạn dịch một biểu thức cây, bạn sẽ truy cập tất cả các node, và trong khi truy cập chúng, bạn xây dựng một cây mới. Cây mới có thể chứa tham chiếu đến các node gốc, hoặc các node mới mà bạn đã đặt vào trong cây.

Hãy cùng truy cập một biểu thức cây và tạo ra một cây mới với một số node được thay thế. Trong ví dụ này, chúng ta sẽ thay thế bất kỳ hằng số (constant) nào bằng một hằng số lớn gấp 10 lần. Các phần còn lại của biểu thức cây được giữ nguyên. Thay vì đọc giá trị của hằng số và thay thế nó bằng một hằng số mới, bạn thực hiện thay thế này bằng cách thay thế node hằng số bằng một node mới thực hiện phép nhân.

Ở đây, khi bạn tìm thấy một node hằng số, bạn tạo một node nhân mới với các node con là hằng số gốc và hằng số `10`:

```csharp
private static Expression ReplaceNodes(Expression original)
{
    if (original.NodeType == ExpressionType.Constant)
    {
        return Expression.Multiply(original, Expression.Constant(10));
    }
    else if (original.NodeType == ExpressionType.Add)
    {
        var binaryExpression = (BinaryExpression)original;
        return Expression.Add(
            ReplaceNodes(binaryExpression.Left),
            ReplaceNodes(binaryExpression.Right));
    }
    return original;
}
```

Tạo một cây mới bằng cách thay thế node gốc bằng node thay thế. Bạn xác minh các thay đổi bằng cách biên dịch và thực thi cây đã được thay thế.

```csharp
var one = Expression.Constant(1, typeof(int));
var two = Expression.Constant(2, typeof(int));
var addition = Expression.Add(one, two);
var sum = ReplaceNodes(addition);
var executableFunc = Expression.Lambda(sum);

var func = (Func<int>)executableFunc.Compile();
var answer = func();
Console.WriteLine(answer);
```

Xây dựng một cây mới là sự kết hợp giữa việc truy cập các node trong cây hiện tại, tạo ra các node mới và chèn chúng vào cây. Ví dụ trên cho thấy tầm quan trọng của việc biểu thức cây là bất biến (immutable). Lưu ý rằng cây mới được tạo ra trong đoạn mã trên chứa hỗn hợp các node mới được tạo và các node từ cây hiện tại. Các node có thể được sử dụng trong cả hai cây vì các node trong cây hiện tại không thể bị sửa đổi. Việc tái sử dụng các node mang lại hiệu quả đáng kể về bộ nhớ. Các node giống nhau có thể được sử dụng xuyên suốt một cây, hoặc trong nhiều biểu thức cây khác nhau. Vì các node không thể bị sửa đổi, cùng một node có thể được tái sử dụng bất cứ khi nào cần.

## Duyệt và thực thi phép cộng

Hãy xác minh cây mới bằng cách xây dựng một visitor thứ hai để duyệt cây các node phép cộng và tính toán kết quả. Thực hiện một vài sửa đổi đối với visitor mà bạn đã thấy trước đây. Trong phiên bản mới này, visitor trả về tổng một phần của phép cộng tính đến thời điểm hiện tại. Đối với một biểu thức hằng số, nó đơn giản là giá trị của biểu thức hằng số đó. Đối với một biểu thức phép cộng, kết quả là tổng của toán hạng trái và phải, sau khi các cây con đó đã được duyệt.

```csharp
var one = Expression.Constant(1, typeof(int));
var two = Expression.Constant(2, typeof(int));
var three = Expression.Constant(3, typeof(int));
var four = Expression.Constant(4, typeof(int));
var addition = Expression.Add(one, two);
var add2 = Expression.Add(three, four);
var sum = Expression.Add(addition, add2);

// Declare the delegate, so you can call it
// from itself recursively:
Func<Expression, int> aggregate = null!;
// Aggregate, return constants, or the sum of the left and right operand.
// Major simplification: Assume every binary expression is an addition.
aggregate = (exp) =>
    exp.NodeType == ExpressionType.Constant ?
    (int)((ConstantExpression)exp).Value :
    aggregate(((BinaryExpression)exp).Left) + aggregate(((BinaryExpression)exp).Right);

var theSum = aggregate(sum);
Console.WriteLine(theSum);
```

Có khá nhiều mã ở đây, nhưng các khái niệm đều dễ tiếp cận. Mã này truy cập các node con theo kiểu tìm kiếm theo chiều sâu (depth-first search). Khi gặp một node hằng số, visitor trả về giá trị của hằng số đó. Sau khi visitor đã truy cập cả hai node con, các node con đó đã tính ra tổng cho cây con đó. Node phép cộng lúc này có thể tính tổng của nó. Khi tất cả các node trong biểu thức cây đã được truy cập, tổng đã được tính xong. Bạn có thể theo dõi quá trình thực thi bằng cách chạy mẫu trong trình gỡ lỗi (debugger) và theo dõi từng bước.

Hãy làm cho việc theo dõi cách các node được phân tích và cách tổng được tính toán dễ dàng hơn bằng cách duyệt cây. Đây là phiên bản cập nhật của method `Aggregate` bao gồm khá nhiều thông tin theo dõi:

```csharp
private static int Aggregate(Expression exp)
{
    if (exp.NodeType == ExpressionType.Constant)
    {
        var constantExp = (ConstantExpression)exp;
        Console.Error.WriteLine($"Found Constant: {constantExp.Value}");
        if (constantExp.Value is int value)
        {
            return value;
        }
        else
        {
            return 0;
        }
    }
    else if (exp.NodeType == ExpressionType.Add)
    {
        var addExp = (BinaryExpression)exp;
        Console.Error.WriteLine("Found Addition Expression");
        Console.Error.WriteLine("Computing Left node");
        var leftOperand = Aggregate(addExp.Left);
        Console.Error.WriteLine($"Left is: {leftOperand}");
        Console.Error.WriteLine("Computing Right node");
        var rightOperand = Aggregate(addExp.Right);
        Console.Error.WriteLine($"Right is: {rightOperand}");
        var sum = leftOperand + rightOperand;
        Console.Error.WriteLine($"Computed sum: {sum}");
        return sum;
    }
    else throw new NotSupportedException("Haven't written this yet");
}
```

Chạy nó trên biểu thức `sum` sẽ cho ra kết quả sau:

```output
10
Found Addition Expression
Computing Left node
Found Addition Expression
Computing Left node
Found Constant: 1
Left is: 1
Computing Right node
Found Constant: 2
Right is: 2
Computed sum: 3
Left is: 3
Computing Right node
Found Addition Expression
Computing Left node
Found Constant: 3
Left is: 3
Computing Right node
Found Constant: 4
Right is: 4
Computed sum: 7
Right is: 7
Computed sum: 10
10
```

Theo dõi kết quả đầu ra và đối chiếu với đoạn mã phía trên. Bạn sẽ có thể hiểu cách mã truy cập từng node và tính tổng khi nó đi qua cây và tìm ra tổng.

Bây giờ, hãy xem một lần chạy khác, với biểu thức được tạo bởi `sum1`:

```csharp
Expression<Func<int>> sum1 = () => 1 + (2 + (3 + 4));
```

Đây là kết quả đầu ra từ việc kiểm tra biểu thức này:

```output
Found Addition Expression
Computing Left node
Found Constant: 1
Left is: 1
Computing Right node
Found Addition Expression
Computing Left node
Found Constant: 2
Left is: 2
Computing Right node
Found Addition Expression
Computing Left node
Found Constant: 3
Left is: 3
Computing Right node
Found Constant: 4
Right is: 4
Computed sum: 7
Right is: 7
Computed sum: 9
Right is: 9
Computed sum: 10
10
```

Mặc dù kết quả cuối cùng giống nhau, nhưng cách duyệt cây khác nhau. Các node được duyệt theo một thứ tự khác, vì cây được xây dựng với các phép toán khác nhau được thực hiện trước.

### Tạo một bản sao đã sửa đổi

Tạo một dự án **Console Application** mới. Thêm chỉ thị `using` cho namespace `System.Linq.Expressions` vào file. Thêm lớp `AndAlsoModifier` vào dự án của bạn.

```csharp
public class AndAlsoModifier : ExpressionVisitor
{
    public Expression Modify(Expression expression)
    {
        return Visit(expression);
    }

    protected override Expression VisitBinary(BinaryExpression b)
    {
        if (b.NodeType == ExpressionType.AndAlso)
        {
            Expression left = this.Visit(b.Left);
            Expression right = this.Visit(b.Right);

            // Make this binary expression an OrElse operation instead of an AndAlso operation.
            return Expression.MakeBinary(ExpressionType.OrElse, left, right, b.IsLiftedToNull, b.Method);
        }

        return base.VisitBinary(b);
    }
}
```

Lớp này kế thừa lớp [`ExpressionVisitor`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.expressionvisitor) và được chuyên biệt hoá để sửa đổi các biểu thức đại diện cho phép toán `AND` có điều kiện. Nó thay đổi các phép toán này từ `AND` có điều kiện thành `OR` có điều kiện. Lớp này ghi đè method [`VisitBinary`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.expressionvisitor.visitbinary) của kiểu cơ sở, vì các biểu thức `AND` có điều kiện được biểu diễn dưới dạng biểu thức nhị phân (binary expressions). Trong method `VisitBinary`, nếu biểu thức được truyền vào đại diện cho một phép toán `AND` có điều kiện, mã sẽ xây dựng một biểu thức mới chứa toán tử `OR` có điều kiện thay vì toán tử `AND` có điều kiện. Nếu biểu thức được truyền vào `VisitBinary` không đại diện cho một phép toán `AND` có điều kiện, method sẽ uỷ quyền (defer) cho implement của lớp cơ sở. Các method của lớp cơ sở xây dựng các node tương tự như các biểu thức cây được truyền vào, nhưng các node đó có các cây con được thay thế bằng các biểu thức cây được tạo ra một cách đệ quy bởi visitor.

Thêm chỉ thị `using` cho namespace `System.Linq.Expressions` vào file. Thêm mã vào method `Main` trong file Program.cs để tạo một biểu thức cây và truyền nó cho method sửa đổi.

```csharp
Expression<Func<string, bool>> expr = name => name.Length > 10 && name.StartsWith("G");
Console.WriteLine(expr);

AndAlsoModifier treeModifier = new AndAlsoModifier();
Expression modifiedExpr = treeModifier.Modify((Expression)expr);

Console.WriteLine(modifiedExpr);

/*  This code produces the following output:

    name => ((name.Length > 10) && name.StartsWith("G"))
    name => ((name.Length > 10) || name.StartsWith("G"))
*/
```

Mã này tạo một biểu thức chứa phép toán `AND` có điều kiện. Sau đó, nó tạo một instance của lớp `AndAlsoModifier` và truyền biểu thức cho method `Modify` của lớp này. Cả biểu thức cây gốc và biểu thức cây đã sửa đổi đều được xuất ra để hiển thị sự thay đổi. Biên dịch và chạy ứng dụng.

## Tìm hiểu thêm

Mẫu này cho thấy một tập con nhỏ của mã bạn sẽ xây dựng để duyệt và diễn giải các thuật toán được biểu diễn bởi một biểu thức cây. Để biết thông tin về việc xây dựng một thư viện đa năng dịch các biểu thức cây sang ngôn ngữ khác, hãy đọc [loạt bài viết này](https://learn.microsoft.com/archive/blogs/mattwar/linq-building-an-iqueryable-provider-series) của Matt Warren. Loạt bài viết này đi sâu vào chi tiết về cách dịch bất kỳ mã nào bạn có thể tìm thấy trong một biểu thức cây.

Bạn đã thấy sức mạnh thực sự của biểu thức cây. Bạn có thể kiểm tra một tập hợp mã, thực hiện bất kỳ thay đổi nào bạn muốn trên mã đó, và thực thi phiên bản đã thay đổi. Vì biểu thức cây là bất biến, bạn tạo ra các cây mới bằng cách sử dụng các thành phần của cây hiện có. Việc tái sử dụng các node giúp giảm thiểu lượng bộ nhớ cần thiết để tạo ra các biểu thức cây đã được sửa đổi.
