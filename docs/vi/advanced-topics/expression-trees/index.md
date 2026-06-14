---
title: "Expression Trees"
description: Tìm hiểu về expression trees (cây biểu thức). Xem cách biên dịch và chạy mã được biểu diễn bởi các cấu trúc dữ liệu dạng cây này, nơi mỗi node (nút) là một expression (biểu thức).
ms.date: 10/13/2025
ms.custom: updateeachrelease
---
# Expression Trees

*Expression Trees* (cây biểu thức) biểu diễn mã nguồn dưới dạng cấu trúc dữ liệu dạng cây, trong đó mỗi node (nút) là một expression (biểu thức), ví dụ như một lời gọi method (phương thức) hay một phép toán nhị phân như `x < y`.

Nếu bạn đã từng dùng LINQ, bạn đã có trải nghiệm với một thư viện phong phú nơi các kiểu `Func` là một phần của bộ API. (Nếu bạn chưa quen với LINQ, có lẽ bạn nên đọc [hướng dẫn về LINQ](../../linq/index.md) và bài viết về [biểu thức lambda](../../language-reference/operators/lambda-expressions.md) trước khi đọc bài này.) Expression Trees cung cấp khả năng tương tác phong phú hơn với các đối số là hàm.

Bạn viết các đối số hàm, thường sử dụng Lambda Expressions, khi tạo truy vấn LINQ. Trong một truy vấn LINQ điển hình, những đối số hàm đó được biến đổi thành một delegate (uỷ quyền) mà trình biên dịch tạo ra.

Bạn đã từng viết mã sử dụng Expression Trees rồi. Các LINQ API của Entity Framework nhận Expression Trees làm đối số cho LINQ Query Expression Pattern. Điều này cho phép [Entity Framework](/ef/) dịch truy vấn bạn viết bằng C# thành SQL và thực thi trong cơ sở dữ liệu. Một ví dụ khác là [Moq](https://github.com/Moq/moq), một framework mocking phổ biến cho .NET.

Khi bạn muốn có sự tương tác phong phú hơn, bạn cần sử dụng *Expression Trees*. Expression Trees biểu diễn mã nguồn như một cấu trúc mà bạn có thể xem xét, sửa đổi hoặc thực thi. Những công cụ này cho bạn khả năng thao tác với mã nguồn trong lúc chạy. Bạn viết mã để kiểm tra các thuật toán đang chạy, hoặc thêm vào những khả năng mới. Trong những tình huống nâng cao hơn, bạn có thể sửa đổi thuật toán đang chạy và thậm chí dịch các biểu thức C# sang một dạng khác để thực thi trong một môi trường khác.

Bạn có thể biên dịch và chạy mã được biểu diễn bởi expression trees. Việc xây dựng và chạy expression trees cho phép sửa đổi linh hoạt mã thực thi, thực thi các truy vấn LINQ trên nhiều cơ sở dữ liệu khác nhau, và tạo ra các truy vấn động. Để biết thêm thông tin về expression trees trong LINQ, hãy xem [Cách sử dụng expression trees để xây dựng truy vấn động](../../linq/how-to-build-dynamic-queries.md).

Expression Trees cũng được sử dụng trong dynamic language runtime (DLR) để cung cấp khả năng tương tác giữa các ngôn ngữ động và .NET, đồng thời cho phép các nhà phát triển trình biên dịch tạo ra expression trees thay vì Microsoft intermediate language (CIL). Để biết thêm thông tin về DLR, hãy xem [Tổng quan về Dynamic Language Runtime](../../../framework/reflection-and-codedom/dynamic-language-runtime-overview.md).

Bạn có thể để trình biên dịch C# hoặc Visual Basic tạo ra expression tree cho bạn dựa trên một anonymous lambda expression, hoặc bạn có thể tự tạo expression trees bằng cách sử dụng namespace [`System.Linq.Expressions`](https://learn.microsoft.com/dotnet/api/system.linq.expressions).

Khi một lambda expression được gán cho một biến kiểu [`Expression<TDelegate>`](https://learn.microsoft.com/dotnet/api/system.linq.expressions.expression-1), trình biên dịch sẽ phát ra mã để xây dựng một expression tree đại diện cho lambda expression đó.

Ví dụ mã sau đây minh hoạ cách để trình biên dịch C# tạo ra một expression tree đại diện cho lambda expression `num => num < 5`.

```csharp
Expression<Func<int, bool>> lambda = num => num < 5;
```

Bạn tự tạo expression trees trong mã của mình. Bạn xây dựng cây bằng cách tạo từng node và gắn các node vào nhau thành một cấu trúc cây. Bạn sẽ học cách tạo expressions trong bài viết về [xây dựng expression trees](expression-trees-building.md).

Expression trees là **bất biến (immutable)**. Nếu bạn muốn sửa đổi một expression tree, bạn phải xây dựng một expression tree mới bằng cách sao chép cây hiện tại và thay thế các node trong đó. Bạn sử dụng một expression tree visitor để duyệt qua expression tree hiện tại. Để biết thêm thông tin, hãy xem bài viết về [dịch expression trees](./expression-trees-translating.md).

Sau khi xây dựng xong một expression tree, bạn có thể [thực thi mã được biểu diễn bởi cây biểu thức](expression-trees-execution.md).

## Hạn chế

Trình biên dịch C# chỉ tạo ra expression trees từ expression lambdas (lambda một dòng). Nó không thể phân tích statement lambdas (lambda nhiều dòng). Để biết thêm thông tin về lambda expressions trong C#, hãy xem [biểu thức lambda](../../language-reference/operators/lambda-expressions.md).

Có một số thành phần ngôn ngữ C# mới hơn không thể dịch tốt sang expression trees. Expression trees không thể chứa biểu thức `await` hoặc lambda `async`. Nhiều tính năng được thêm vào từ C# 6 trở đi không xuất hiện chính xác như đã viết trong expression trees. Thay vào đó, các tính năng mới hơn được thể hiện trong expression trees bằng cú pháp cũ tương đương, nếu có thể. Một số cấu trúc khác thì không khả dụng. Điều này có nghĩa là mã diễn giải expression trees vẫn hoạt động giống nhau khi các tính năng ngôn ngữ mới được giới thiệu. Tuy nhiên, dù có những hạn chế này, expression trees vẫn cho phép bạn tạo ra các thuật toán động dựa trên việc diễn giải và sửa đổi mã được biểu diễn dưới dạng cấu trúc dữ liệu. Điều này giúp các thư viện phong phú như Entity Framework thực hiện được những gì chúng làm.

Expression trees không hỗ trợ các kiểu node expression mới. Việc giới thiệu các kiểu node mới sẽ là một thay đổi lớn (breaking change) cho tất cả các thư viện diễn giải expression trees. Danh sách dưới đây bao gồm hầu hết các thành phần ngôn ngữ C# không thể sử dụng:

- [Phương thức có điều kiện](../../language-reference/preprocessor-directives.md#conditional-compilation) (Conditional methods) bị loại bỏ khỏi đầu ra
- Truy cập [`base`](../../language-reference/keywords/base.md)
- Method group expressions (biểu thức nhóm phương thức), bao gồm [*address-of* (`&`)](../../language-reference/operators/pointer-related-operators.md) một method group và anonymous method expressions (biểu thức phương thức ẩn danh)
- Tham chiếu đến [hàm cục bộ](../../programming-guide/classes-and-structs/local-functions.md) (local functions)
- Statements (câu lệnh), bao gồm phép gán (`=`) và statement bodied expressions
- [Phương thức một phần](../../language-reference/keywords/partial-member.md) (Partial methods) chỉ có khai báo định nghĩa
- [Thao tác con trỏ không an toàn](../../language-reference/unsafe-code.md#pointer-types) (Unsafe pointer operations)
- [Thao tác `dynamic`](../../language-reference/builtin-types/reference-types.md#the-dynamic-type)
- [Toán tử kết hợp với vế trái là `null` hoặc `default`, toán tử gán null](../../language-reference/operators/assignment-operator.md#null-coalescing-assignment) (Coalescing operators) và [toán tử truyền null (`?.`)](../../language-reference/operators/null-coalescing-operator.md)
- [Bộ khởi tạo mảng đa chiều](../../language-reference/builtin-types/arrays.md#multidimensional-arrays) (Multi-dimensional array initializers), [indexed properties và dictionary initializers](../../programming-guide/classes-and-structs/object-and-collection-initializers.md#collection-initializers)
- [Biểu thức tập hợp](../../language-reference/operators/collection-expressions.md) (Collection expressions)
- [Biểu thức `throw`](../../language-reference/statements/exception-handling-statements.md#the-throw-expression)
- Truy cập [thành viên interface `static virtual` hoặc `abstract`](../../language-reference/keywords/interface.md#static-abstract-and-virtual-members) (static virtual or abstract interface members)
- Lambda expressions có [thuộc tính](../../language-reference/operators/lambda-expressions.md#attributes) (attributes)
- [Chuỗi nội suy](../../language-reference/tokens/interpolated.md) (Interpolated strings)
- UTF-8 string conversions hoặc [chuỗi ký tự UTF-8](../../language-reference/builtin-types/reference-types.md#utf-8-string-literals) (UTF-8 string literals)
- Lời gọi method sử dụng [đối số biến đổi](../../language-reference/keywords/method-parameters.md#params-modifier) (variable arguments), [đối số có tên hoặc đối số tuỳ chọn](../../programming-guide/classes-and-structs/named-and-optional-arguments.md) (named or optional arguments)
- Biểu thức sử dụng [`Index`](https://learn.microsoft.com/dotnet/api/system.index) hoặc [`Range`](https://learn.microsoft.com/dotnet/api/system.range), [toán tử chỉ mục từ cuối (`^`)](../../language-reference/operators/member-access-operators.md#index-from-end-operator-) hoặc [biểu thức range (`..`)](../../language-reference/operators/member-access-operators.md#range-operator-)
- [Biểu thức lambda `async` hoặc biểu thức `await`](../../language-reference/operators/lambda-expressions.md#async-lambdas) (async lambda expressions or await expressions), bao gồm [`await foreach` và `await using`](../../language-reference/operators/await.md#asynchronous-streams-and-disposables)
- [Tuple literals, tuple conversions, tuple `==` hoặc `!=`, hoặc biểu thức `with`](../../language-reference/builtin-types/value-tuples.md)
- [Discards (`_`)](../../fundamentals/functional/discards.md), [deconstructing assignment](../../fundamentals/functional/deconstruct.md), [toán tử `is` pattern matching hoặc biểu thức `switch` pattern matching](../../language-reference/operators/patterns.md)
- COM call với `ref` bị bỏ qua trên các đối số
- Tham số [`ref`](../../language-reference/keywords/ref.md), [`in`](../../language-reference/keywords/method-parameters.md#in-parameter-modifier) hoặc [`out`](../../language-reference/keywords/method-parameters.md#out-parameter-modifier), giá trị trả về `ref`, đối số `out`, hoặc bất kỳ giá trị nào của kiểu [`ref struct`](../../language-reference/builtin-types/ref-struct.md)
