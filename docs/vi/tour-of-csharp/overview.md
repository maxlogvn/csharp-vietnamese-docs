---
title: Tổng quan
description: Mới học C#? Tìm hiểu những điều cơ bản về ngôn ngữ này. Bắt đầu với tổng quan này.
ms.date: 02/06/2026
---

# Tổng quan về ngôn ngữ C#

Bài viết này cung cấp cho bạn cái nhìn tổng quan về ngôn ngữ C#. Dù bạn đang viết chương trình đầu tiên hay là một lập trình viên giàu kinh nghiệm đang khám phá C#, bạn sẽ tìm thấy các khái niệm và tính năng chính tại đây.

> [!TIP]
> **Mới học lập trình?** Lướt qua bài viết này để có cái nhìn tổng thể, sau đó bắt đầu [các hướng dẫn cho người mới bắt đầu](./tutorials/index.md) để thực hành viết code.
>
> **Đến từ Java, JavaScript, hay Python?** Đọc các mẹo dành cho lập trình viên [Java](./tips-for-java-developers.md), [JavaScript](./tips-for-javascript-developers.md), hoặc [Python](./tips-for-python-developers.md) cùng với bài viết này.
>
> **Lập trình viên giàu kinh nghiệm nhưng mới với C#?** Bài viết này đề cập những điểm đặc trưng của C#. Xem [Bạn có thể xây dựng gì với C#](./what-you-can-build.md) để tìm workload phù hợp với mục tiêu của bạn.

Ngôn ngữ C# là ngôn ngữ phổ biến nhất cho [nền tảng .NET](../index.yml), một môi trường phát triển mã nguồn mở, miễn phí, đa nền tảng. Các chương trình C# có thể chạy trên nhiều thiết bị khác nhau, từ thiết bị Internet of Things (IoT) đến đám mây và mọi nơi ở giữa. Bạn có thể viết ứng dụng cho điện thoại, máy tính để bàn, máy tính xách tay và máy chủ. Xem [Bạn có thể xây dựng gì với C#](./what-you-can-build.md) để biết tổng quan về các loại ứng dụng.

C# là một ngôn ngữ đa năng, đa nền tảng giúp lập trình viên làm việc hiệu quả trong khi viết code có hiệu suất cao. C# có sự hỗ trợ rộng rãi trong hệ sinh thái và nhiều [workload](../../standard/glossary.md#workload). Dựa trên các nguyên tắc hướng đối tượng, nó kết hợp nhiều tính năng từ các mô hình khác, đặc biệt là lập trình hàm. Các tính năng cấp thấp hỗ trợ các tình huống hiệu suất cao mà không cần viết unsafe code (mã không an toàn). Hầu hết runtime (môi trường thực thi) và thư viện được viết bằng C#, và những tiến bộ trong C# thường mang lại lợi ích cho tất cả lập trình viên .NET.

C# thuộc họ ngôn ngữ C. [Cú pháp C#](../language-reference/keywords/index.md) quen thuộc nếu bạn đã từng dùng C, C++, JavaScript, TypeScript, hoặc Java. Giống như C và C++, dấu chấm phẩy (`;`) xác định kết thúc câu lệnh. Định danh trong C# phân biệt chữ hoa chữ thường. C# sử dụng dấu ngoặc nhọn `{` và `}`, các câu lệnh điều khiển như `if`, `else`, và `switch`, và các cấu trúc lặp như `for` và `while`. C# cũng có câu lệnh `foreach` cho bất kỳ kiểu collection (tập hợp) nào.

## Hello world

Chương trình "Hello, World" theo truyền thống thường được dùng để giới thiệu một ngôn ngữ lập trình. Dưới đây là chương trình đó trong C#:

```csharp
// This line prints "Hello, World"
Console.WriteLine("Hello, World");
```

Dòng bắt đầu bằng `//` được gọi là *single line comment (chú thích một dòng)*. Single line comments trong C# bắt đầu bằng `//` và kéo dài đến hết dòng hiện tại. C# cũng hỗ trợ *multi-line comments (chú thích nhiều dòng)*. Multi-line comments bắt đầu bằng `/*` và kết thúc bằng `*/`. Method (phương thức) `WriteLine` của class (lớp) `Console`, nằm trong namespace (không gian tên) `System`, tạo ra đầu ra của chương trình. Các thư viện class tiêu chuẩn cung cấp class này, và mọi chương trình C# đều tự động tham chiếu các thư viện này theo mặc định. Một dạng chương trình khác yêu cầu bạn khai báo class và method chứa điểm vào của chương trình. Compiler (trình biên dịch) sẽ tổng hợp các thành phần này khi bạn sử dụng top-level statements (câu lệnh cấp cao nhất).

Định dạng thay thế này vẫn hợp lệ và chứa nhiều khái niệm cơ bản trong tất cả chương trình C#. Nhiều mẫu C# hiện có sử dụng định dạng tương đương sau:

```csharp
using System;
﻿namespace TourOfCsharp;

class Program
{
    static void Main()
    {
        // This line prints "Hello, World" 
        Console.WriteLine("Hello, World");
    }
}
```

Chương trình "Hello, World" ở trên bắt đầu bằng chỉ thị `using` tham chiếu tới namespace `System`. Namespace cung cấp một cách phân cấp để tổ chức các chương trình và thư viện C#. Namespace chứa các type (kiểu dữ liệu) và các namespace khác. Ví dụ, namespace `System` chứa nhiều type, chẳng hạn như class `Console` được tham chiếu trong chương trình, và nhiều namespace khác như `IO` và `Collections`. Chỉ thị `using` tham chiếu tới một namespace cho phép sử dụng các type thuộc namespace đó mà không cần tiền tố. Nhờ chỉ thị `using`, chương trình có thể dùng `Console.WriteLine` thay cho `System.Console.WriteLine`. Trong ví dụ trước, namespace đó đã được [bao gồm ngầm định](../language-reference/keywords/using-directive.md#the-global-modifier).

> [!NOTE]
> Chương trình trên khai báo class `Program` với một thành phần duy nhất: method tên `Main`. Nhiều mẫu và hướng dẫn C# hiện có sử dụng định dạng này. Theo quy ước, khi không có top-level statements, một static method (phương thức tĩnh) tên `Main` đóng vai trò là [điểm vào](../fundamentals/program-structure/main-command-line.md) của chương trình C#. Cả hai định dạng đều biên dịch ra cùng một mã. Bạn không cần phải dùng định dạng này — file-based apps và top-level statements là cách đơn giản hơn để bắt đầu.

## File-based apps

C# là một ngôn ngữ *compiled (biên dịch)*. Trong hầu hết chương trình C#, bạn dùng lệnh [`dotnet build`](../../core/tools/dotnet-build.md) để biên dịch một nhóm tệp nguồn thành gói nhị phân. Sau đó, bạn dùng lệnh [`dotnet run`](../../core/tools/dotnet-run.md) để chạy chương trình. (Bạn có thể đơn giản hóa quy trình này vì `dotnet run` sẽ biên dịch chương trình trước khi chạy nếu cần.) Các công cụ này hỗ trợ nhiều tùy chọn cấu hình và cờ dòng lệnh. Giao diện dòng lệnh (CLI) `dotnet`, được bao gồm trong .NET SDK, cung cấp nhiều [công cụ](../../core/tools/index.md) để tạo và sửa đổi các tệp C#.

Bắt đầu từ C# 14 và .NET 10, bạn có thể tạo *file-based apps*, giúp đơn giản hóa việc xây dựng và chạy chương trình C#. Bạn dùng lệnh `dotnet run` để chạy một chương trình chứa trong một tệp `*.cs` duy nhất. Ví dụ, nếu code sau được lưu trong tệp `hello-world.cs`, bạn có thể chạy nó bằng cách gõ `dotnet run hello-world.cs`:

```csharp
#!/usr/bin/env dotnet

Console.WriteLine("Hello, World!");
```

Dòng đầu tiên của chương trình chứa chuỗi `#!` (shebang) dành cho hệ điều hành unix. Điều này cho phép thực thi tệp trực tiếp bằng tên của nó khi quyền *execute* (`+x`) được thiết lập trên tệp. Ví dụ, bạn có thể chạy tệp C# trực tiếp từ dòng lệnh:

```bash
./hello-world.cs
```

Mã nguồn cho các chương trình này phải là một tệp duy nhất, nhưng ngoài ra mọi cú pháp C# đều hợp lệ. Bạn có thể dùng file-based apps cho các tiện ích dòng lệnh nhỏ, nguyên mẫu, hoặc các thử nghiệm khác.

## Các tính năng C# quen thuộc

C# dễ tiếp cận cho người mới bắt đầu nhưng cũng cung cấp các tính năng nâng cao cho lập trình viên giàu kinh nghiệm viết các ứng dụng chuyên biệt. Bạn có thể làm việc hiệu quả một cách nhanh chóng. Bạn có thể học các kỹ thuật chuyên sâu hơn khi cần cho ứng dụng của mình.

Các ứng dụng C# được hưởng lợi từ [quản lý bộ nhớ tự động](../../standard/automatic-memory-management.md) của runtime. Các ứng dụng C# cũng sử dụng [thư viện runtime](../../standard/runtime-libraries-overview.md) phong phú do .NET SDK cung cấp. Một số thành phần độc lập với nền tảng, như thư viện hệ thống tệp, collection dữ liệu và thư viện toán học. Một số khác chỉ dành riêng cho một [khối lượng công việc](./what-you-can-build.md) cụ thể, như thư viện web ASP.NET Core hoặc thư viện UI .NET MAUI. Một hệ sinh thái mã nguồn mở phong phú trên [NuGet](https://nuget.org) bổ sung cho các thư viện có sẵn trong runtime. Các thư viện này cung cấp thêm nhiều thành phần bạn có thể sử dụng.

C# là một ngôn ngữ *strongly typed (kiểu mạnh)*. Mọi variable (biến) bạn khai báo đều có một kiểu được biết tại thời điểm biên dịch. Compiler hoặc công cụ chỉnh sửa sẽ cho bạn biết nếu bạn đang sử dụng sai kiểu đó. Bạn có thể sửa những lỗi đó trước khi chạy chương trình. [Kiểu dữ liệu cơ bản](../fundamentals/types/index.md) được tích hợp trong ngôn ngữ và runtime: value types (kiểu giá trị) như `int`, `double`, `char`, reference types (kiểu tham chiếu) như string (chuỗi), array (mảng) và các collection khác. Khi bạn viết chương trình, bạn tạo ra các kiểu của riêng mình. Các kiểu đó có thể là struct (cấu trúc) cho value, hoặc class định nghĩa hành vi hướng đối tượng. Bạn có thể thêm modifier (bổ từ) `record` vào kiểu `struct` hoặc `class` để compiler tổng hợp code cho việc so sánh bằng nhau. Bạn cũng có thể tạo định nghĩa interface (giao diện) — chúng định nghĩa một hợp đồng, hay một tập hợp các member (thành phần), mà một kiểu implement (triển khai) interface đó phải cung cấp. Bạn cũng có thể định nghĩa generic types (kiểu chung) và generic methods (phương thức chung). [Kiểu tổng quát](../fundamentals/types/generics.md) sử dụng *type parameters (tham số kiểu)* để cung cấp một chỗ giữ chỗ cho kiểu thực tế khi được sử dụng.

Khi viết code, bạn định nghĩa các hàm, còn được gọi là method (phương thức), như là member của các kiểu `struct` và `class`. Các method này định nghĩa hành vi của kiểu dữ liệu của bạn. Bạn có thể overload (nạp chồng) method với số lượng hoặc kiểu tham số khác nhau. Method có thể tùy chọn trả về một giá trị. Ngoài method, các kiểu C# có thể có property (thuộc tính) — các thành phần dữ liệu được hỗ trợ bởi các hàm gọi là *accessor (trình truy cập)*. Các kiểu C# có thể định nghĩa event (sự kiện), cho phép một kiểu thông báo cho người đăng ký về các hành động quan trọng. C# hỗ trợ các kỹ thuật hướng đối tượng như inheritance (kế thừa) và polymorphism (đa hình) cho các kiểu `class`.

Các ứng dụng C# sử dụng [ngoại lệ](../fundamentals/exceptions/index.md) để báo cáo và xử lý lỗi. Cách này quen thuộc nếu bạn đã dùng C++ hoặc Java. Code của bạn throw (ném) một exception khi nó không thể thực hiện được điều đã định. Code khác, dù ở bất kỳ cấp độ nào trong call stack (ngăn xếp cuộc gọi), có thể tùy chọn phục hồi bằng cách sử dụng khối `try` - `catch`.

> [!TIP]
> Để tìm hiểu thêm về types, methods và exceptions, hãy truy cập phần [C# căn bản](../fundamentals/program-structure/index.md). Phần này trình bày chi tiết về [hệ thống kiểu](../fundamentals/types/index.md), [lập trình hướng đối tượng](../fundamentals/object-oriented/index.md) và [xử lý ngoại lệ](../fundamentals/exceptions/index.md).

## Các tính năng đặc trưng của C#

Một số yếu tố của C# có thể ít quen thuộc hơn.

C# cung cấp [đối sánh mẫu](../fundamentals/functional/pattern-matching.md). Các biểu thức này cho phép bạn kiểm tra dữ liệu và đưa ra quyết định dựa trên đặc điểm của nó. Pattern matching cung cấp cú pháp tuyệt vời cho luồng điều khiển dựa trên dữ liệu. Code sau đây cho thấy cách các method cho phép toán boolean *and*, *or* và *xor* có thể được biểu diễn bằng cú pháp pattern matching:

```csharp
public static bool Or(bool left, bool right) =>
    (left, right) switch
    {
        (true, true) => true,
        (true, false) => true,
        (false, true) => true,
        (false, false) => false,
    };

public static bool And(bool left, bool right) =>
    (left, right) switch
    {
        (true, true) => true,
        (true, false) => false,
        (false, true) => false,
        (false, false) => false,
    };

public static bool Xor(bool left, bool right) =>
    (left, right) switch
    {
        (true, true) => false,
        (true, false) => true,
        (false, true) => true,
        (false, false) => false,
    };
```

Các biểu thức pattern matching có thể được đơn giản hóa bằng cách sử dụng `_` làm catchall cho bất kỳ giá trị nào. Ví dụ sau cho thấy cách bạn có thể đơn giản hóa method *and*:

```csharp
public static bool ReducedAnd(bool left, bool right) =>
    (left, right) switch
    {
        (true, true) => true,
        (_, _) => false,
    };
```

Các ví dụ trên cũng khai báo *tuple (bộ)*, một cấu trúc dữ liệu nhẹ. Một tuple là một chuỗi các giá trị có thứ tự, độ dài cố định với tên tùy chọn và kiểu riêng lẻ. Bạn đặt chuỗi này trong dấu `(` và `)`. Khai báo `(left, right)` định nghĩa một tuple với hai giá trị boolean: `left` và `right`. Mỗi nhánh switch khai báo một giá trị tuple như `(true, true)`. Tuple cung cấp cú pháp tiện lợi để khai báo một giá trị đơn với nhiều giá trị thuộc bất kỳ kiểu nào.

*Collection expressions (biểu thức tập hợp)* cung cấp một cú pháp chung để cung cấp giá trị collection. Bạn viết các giá trị hoặc biểu thức giữa dấu `[` và `]` và compiler chuyển đổi biểu thức đó thành kiểu collection cần thiết:

```csharp
int[] numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
List<string> names = ["Alice", "Bob", "Charlie", "David"];

IEnumerable<int> moreNumbers = [.. numbers, 11, 12, 13];
IEnumerable<string> empty = [];
```

Ví dụ trước cho thấy các kiểu collection khác nhau mà bạn có thể khởi tạo bằng collection expressions. Một ví dụ sử dụng `[]` — collection expression rỗng — để khai báo một collection trống. Một ví dụ khác sử dụng `..` — *spread element (toán tử trải rộng)* — để mở rộng một collection và thêm tất cả các giá trị của nó vào collection expression.

Bạn có thể sử dụng *index (chỉ mục)* và *range expressions (biểu thức phạm vi)* để lấy một hoặc nhiều phần tử từ một collection có thể đánh chỉ mục:

```csharp
string second = names[1]; // 0-based index
string last = names[^1]; // ^1 is the last element
int[] smallNumbers = numbers[0..5]; // elements at indexes 0 to 4
```

Index `^` chỉ *từ cuối* thay vì từ đầu. Phần tử `^0` là phần tử nằm sau phần tử cuối của collection, vì vậy `^1` là phần tử cuối cùng. `..` trong range expression biểu thị phạm vi các phần tử cần bao gồm. Range bắt đầu bằng index đầu tiên và bao gồm tất cả các phần tử cho đến, nhưng không bao gồm, phần tử ở index cuối.

Để biết thêm thông tin về index và range expressions, xem bài viết [Khám phá chỉ mục và phạm vi](../tutorials/ranges-indexes.md).

[LINQ](../linq/index.md) cung cấp cú pháp dựa trên pattern chung để truy vấn hoặc biến đổi bất kỳ collection dữ liệu nào. LINQ hợp nhất cú pháp để truy vấn collection trong bộ nhớ, dữ liệu có cấu trúc như XML hoặc JSON, cơ sở dữ liệu, và thậm chí các API dữ liệu đám mây. Bạn học một bộ cú pháp và có thể tìm kiếm và thao tác dữ liệu bất kể nó được lưu trữ ở đâu. Truy vấn sau tìm tất cả sinh viên có điểm trung bình (GPA) lớn hơn 3.5:

```csharp
var honorRoll = from student in Students
                where student.GPA > 3.5
                select student;
```

Truy vấn trên hoạt động với nhiều kiểu lưu trữ được đại diện bởi `Students`. Nó có thể là một collection các object (đối tượng), một bảng cơ sở dữ liệu, một blob lưu trữ đám mây, hoặc một cấu trúc XML. Cùng một cú pháp truy vấn hoạt động cho mọi kiểu lưu trữ.

[Mô hình lập trình bất đồng bộ dựa trên Task](../asynchronous-programming/index.md) cho phép bạn viết code trông như chạy synchronous (đồng bộ) mặc dù nó thực sự chạy asynchronous (bất đồng bộ). Nó sử dụng các từ khóa `async` và `await` để mô tả các method không đồng bộ và khi một biểu thức được đánh giá bất đồng bộ. Mẫu sau đây await (chờ) một yêu cầu web không đồng bộ. Khi thao tác không đồng bộ hoàn thành, method trả về độ dài của phản hồi:

```csharp
public static async Task<int> GetPageLengthAsync(string endpoint)
{
    var client = new HttpClient();
    var uri = new Uri(endpoint);
    byte[] content = await client.GetByteArrayAsync(uri);
    return content.Length;
}
```

C# cũng hỗ trợ câu lệnh `await foreach` để lặp qua một collection được hỗ trợ bởi một thao tác bất đồng bộ, như API phân trang GraphQL. Mẫu sau đọc dữ liệu theo từng khối (chunk), trả về một iterator (bộ lặp) cung cấp quyền truy cập vào từng phần tử khi nó có sẵn:

```csharp
public static async IAsyncEnumerable<int> ReadSequence()
{
    int index = 0;
    while (index < 100)
    {
        int[] nextChunk = await GetNextChunk(index);
        if (nextChunk.Length == 0)
        {
            yield break;
        }
        foreach (var item in nextChunk)
        {
            yield return item;
        }
        index++;
    }
}
```

Caller (người gọi) có thể lặp qua collection bằng câu lệnh `await foreach`:

```csharp
await foreach (var number in ReadSequence())
{
    Console.WriteLine(number);
}
```

Cuối cùng, là một phần của hệ sinh thái .NET, bạn có thể sử dụng [Visual Studio](https://visualstudio.microsoft.com/vs) hoặc [Visual Studio Code](https://code.visualstudio.com) với [C# DevKit](https://code.visualstudio.com/docs/csharp/get-started). Các công cụ này cung cấp hiểu biết phong phú về C#, bao gồm code bạn viết. Chúng cũng cung cấp khả năng debugging (gỡ lỗi).

> [!TIP]
> Để tìm hiểu thêm về pattern matching, LINQ và lập trình bất đồng bộ, hãy xem các phần [kỹ thuật hàm](../fundamentals/functional/pattern-matching.md), [tổng quan LINQ](../linq/index.md) và [lập trình bất đồng bộ](../asynchronous-programming/index.md).

## Bước tiếp theo

Bài viết này đã cung cấp một cái nhìn tổng quan nhanh về ngôn ngữ C#. Dưới đây là hướng đi tiếp theo, tùy thuộc vào kinh nghiệm của bạn:

- **Bắt đầu code:** Làm theo [các hướng dẫn cho người mới bắt đầu](./tutorials/index.md) để học C# từng bước.
- **Đi sâu hơn:** Truy cập phần [C# căn bản](../fundamentals/program-structure/index.md) để tìm hiểu chi tiết về hệ thống kiểu, lập trình hướng đối tượng và xử lý lỗi.
- **Xây dựng một ứng dụng:** Khám phá [bạn có thể xây dựng gì với C#](./what-you-can-build.md) để tìm ý tưởng phù hợp với bạn.
- **Đến từ một ngôn ngữ khác?** Đọc hướng dẫn dành cho lập trình viên [Java](./tips-for-java-developers.md), [JavaScript](./tips-for-javascript-developers.md) hoặc [Python](./tips-for-python-developers.md).
- **Xây dựng file-based apps:** Học cách [xây dựng file-based apps](../fundamentals/tutorials/file-based-programs.md) cho các chương trình nhỏ và nguyên mẫu.
