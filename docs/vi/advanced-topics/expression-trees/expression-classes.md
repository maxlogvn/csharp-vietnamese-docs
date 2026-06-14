---
title: Hỗ trợ .NET Runtime cho Expression Trees
description: Tìm hiểu về các kiểu dữ liệu trong .NET runtime hỗ trợ expression trees, cách tạo expression trees và các kỹ thuật làm việc với API expression tree.
ms.date: 03/06/2023
---

# Hỗ trợ .NET Runtime cho Expression Trees

Có rất nhiều class (lớp) trong .NET runtime làm việc với Expression Trees (cây biểu thức). Bạn có thể xem danh sách đầy đủ tại [`System.Linq.Expressions`](https://learn.microsoft.com/dotnet/api/system.linq.expressions). Thay vì liệt kê toàn bộ, hãy cùng tìm hiểu cách thiết kế của các runtime class này.

Trong thiết kế ngôn ngữ, expression (biểu thức) là một đoạn mã được tính toán và trả về một giá trị. Expression có thể đơn giản: constant expression (biểu thức hằng) `1` trả về giá trị hằng là 1. Chúng cũng có thể phức tạp hơn: Expression `(-B + Math.Sqrt(B*B - 4 * A * C)) / (2 * A)` trả về một nghiệm của phương trình bậc hai (trong trường hợp phương trình có nghiệm).

## System.Linq.Expression và các kiểu dẫn xuất

Một trong những khó khăn khi làm việc với expression trees là có rất nhiều loại expression khác nhau xuất hiện ở nhiều vị trí trong chương trình. Hãy xem xét một assignment expression (biểu thức gán). Vế bên phải của phép gán có thể là một constant value, một variable (biến), một method call expression (biểu thức gọi phương thức), hoặc nhiều loại khác. Sự linh hoạt của ngôn ngữ đồng nghĩa với việc bạn có thể gặp nhiều loại expression khác nhau ở bất kỳ node (nút) nào khi duyệt qua một expression tree. Do đó, cách đơn giản nhất là làm việc với kiểu expression cơ bản. Tuy nhiên, đôi khi bạn cần biết thêm chi tiết. Class `Expression` cơ bản có thuộc tính `NodeType` phục vụ cho mục đích này. Nó trả về kiểu `ExpressionType`, một enumeration (kiểu liệt kê) các loại expression có thể có. Khi đã biết type (kiểu) của node, bạn ép kiểu (cast) nó sang type đó và thực hiện các hành động cụ thể dựa trên loại expression node đó. Bạn có thể tìm kiếm các node type nhất định, sau đó làm việc với các thuộc tính cụ thể của loại expression đó.

Ví dụ, đoạn mã sau in ra tên của một variable cho một variable access expression (biểu thức truy cập biến). Đoạn mã dưới đây minh hoạ cách kiểm tra node type, ép kiểu sang variable access expression, rồi kiểm tra các thuộc tính của loại expression cụ thể đó:

```csharp
Expression<Func<int, int>> addFive = (num) => num + 5;

if (addFive is LambdaExpression lambdaExp)
{
    var parameter = lambdaExp.Parameters[0];  -- first

    Console.WriteLine(parameter.Name);
    Console.WriteLine(parameter.Type);
}
```

## Tạo Expression Trees

Class `System.Linq.Expression` cũng chứa nhiều static method (phương thức tĩnh) để tạo expression (biểu thức). Các method này tạo một expression node bằng cách sử dụng các đối số được cung cấp cho các node con của nó. Bằng cách này, bạn xây dựng một expression từ các node lá của nó. Ví dụ, đoạn mã sau tạo một Add expression:

```csharp
// Addition is an add expression for "1 + 2"
var one = Expression.Constant(1, typeof(int));
var two = Expression.Constant(2, typeof(int));
var addition = Expression.Add(one, two);
```

Qua ví dụ đơn giản này, bạn có thể thấy có nhiều kiểu dữ liệu tham gia vào việc tạo và làm việc với expression trees. Sự phức tạp đó là cần thiết để cung cấp khả năng phong phú mà ngôn ngữ C# mang lại.

## Điều hướng API

Có các Expression node type tương ứng với gần như tất cả các thành phần cú pháp của ngôn ngữ C#. Mỗi type có các method cụ thể cho loại thành phần ngôn ngữ đó. Đó là một lượng kiến thức khá lớn để ghi nhớ cùng lúc. Thay vì cố gắng học thuộc lòng, đây là các kỹ thuật bạn có thể sử dụng để làm việc với Expression trees:

1. Xem các thành phần của enum `ExpressionType` để xác định các node có thể bạn cần kiểm tra. Danh sách này giúp bạn khi muốn duyệt và hiểu một expression tree.
1. Xem các static member của class `Expression` để xây dựng một expression. Các method này có thể tạo ra bất kỳ loại expression nào từ tập hợp các node con của nó.
1. Xem class `ExpressionVisitor` để xây dựng một expression tree đã được sửa đổi.

Bạn sẽ tìm hiểu thêm khi xem xét từng lĩnh vực trong ba lĩnh vực trên. Chắc chắn bạn sẽ tìm thấy những gì mình cần khi bắt đầu với một trong ba bước đó.
