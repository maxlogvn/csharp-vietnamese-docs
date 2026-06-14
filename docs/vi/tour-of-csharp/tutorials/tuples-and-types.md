---
title: Tuples and types - Hướng dẫn giới thiệu
description: Bài hướng dẫn này dạy bạn cách tạo kiểu dữ liệu (types) trong C#. Bạn sẽ viết mã C# và thấy kết quả biên dịch cũng như chạy mã khi học về cấu trúc của các kiểu dữ liệu.
ms.date: 02/06/2026
---

# Hướng dẫn: Tạo kiểu dữ liệu trong C\#

Bài hướng dẫn này sẽ dạy bạn cách tạo kiểu dữ liệu (types) trong C#. Bạn sẽ viết những đoạn mã nhỏ, sau đó biên dịch và chạy chúng. Bài hướng dẫn bao gồm một loạt các bài học khám phá những kiểu dữ liệu khác nhau trong C#. Những bài học này sẽ giúp bạn nắm vững nền tảng của ngôn ngữ C#.

> [!TIP]
> **Mới học lập trình?** Hãy làm lần lượt từng phần theo thứ tự -- tuples (bộ dữ liệu), records (bản ghi), rồi đến structs (cấu trúc) và classes (lớp). **Đã biết ngôn ngữ khác?** Nếu bạn đã biết về classes và structs, hãy tập trung vào [tuples](#tuples) và [record types](#create-record-types) vì có thể chúng còn mới với bạn.

Các bài hướng dẫn trước đã làm việc với văn bản và số. Chuỗi (string) và số (number) là những *simple types (kiểu đơn giản)*: mỗi kiểu chỉ lưu trữ một giá trị duy nhất. Khi chương trình của bạn lớn dần, bạn sẽ cần làm việc với các cấu trúc dữ liệu phức tạp hơn. C# cung cấp nhiều loại kiểu dữ liệu khác nhau mà bạn có thể tự định nghĩa khi cần cấu trúc dữ liệu với nhiều trường (fields), thuộc tính (properties) hoặc hành vi (behavior) hơn. Hãy cùng bắt đầu khám phá những kiểu dữ liệu đó.

Trong bài hướng dẫn này, bạn sẽ:

> [!div class="checklist"]
>
> * Tạo và thao tác với kiểu tuple (bộ dữ liệu).
> * Tạo kiểu record (bản ghi).
> * Tìm hiểu về các kiểu struct (cấu trúc), class (lớp) và interface.

## Điều kiện tiên quyết

Bạn cần có một trong những lựa chọn sau:

- Một tài khoản GitHub để sử dụng [GitHub Codespaces](https://github.com/codespaces). Nếu chưa có, bạn có thể tạo tài khoản miễn phí tại [GitHub.com](https://github.com).
- Một máy tính đã cài đặt các công cụ sau:
  - [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0).
  - [Visual Studio Code](https://code.visualstudio.com/download).
  - [C# DevKit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit).

Để sử dụng Codespaces, bạn cần có tài khoản GitHub. Nếu chưa có, bạn có thể tạo tài khoản miễn phí tại [GitHub.com](https://github.com).

## Tuples

Để khởi động GitHub Codespace với môi trường hướng dẫn, hãy mở trình duyệt và truy cập kho lưu trữ [tutorial codespace](https://github.com/dotnet/tutorial-codespace). Nhấn vào nút *Code* màu xanh lá, chọn tab *Codespaces*. Sau đó chọn dấu `+` để tạo một Codespace mới sử dụng môi trường này. Nếu bạn đã hoàn thành các bài hướng dẫn khác trong loạt bài này, bạn có thể mở codespace đó thay vì tạo mới.

1. Khi codespace của bạn đã sẵn sàng, tạo một file mới trong thư mục *tutorials* với tên *tuples.cs*.
1. Mở file mới của bạn.
1. Gõ hoặc sao chép đoạn mã sau vào *tuples.cs*:

   ```csharp
   var pt = (X: 1, Y: 2);

   var slope = (double)pt.Y / (double)pt.X;
   Console.WriteLine($"A line from the origin to the point {pt} has a slope of {slope}.");
   ```

1. Chạy chương trình bằng cách gõ các lệnh sau trong cửa sổ terminal tích hợp:

   ```dotnetcli
   cd tutorials
   dotnet tuples.cs
   ```

   *Tuples* là một chuỗi có thứ tự các giá trị với độ dài cố định. Mỗi phần tử của tuple có một kiểu và một tên tuỳ chọn.

   > [!TIP]
   > Khi bạn khám phá C# (hoặc bất kỳ ngôn ngữ lập trình nào), bạn sẽ mắc lỗi khi viết mã. **Trình biên dịch** sẽ tìm ra những lỗi đó và báo cho bạn. Khi kết quả đầu ra có thông báo lỗi, hãy xem kỹ mã mẫu và mã của bạn để biết cần sửa gì. Bạn cũng có thể hỏi Copilot để tìm sự khác biệt hoặc phát hiện lỗi. Bài tập này sẽ giúp bạn học cấu trúc của mã C#.

1. Thêm đoạn mã sau vào sau mã trước đó để sửa đổi một thành viên của tuple:

   ```csharp
   pt.X = pt.X + 5;
   Console.WriteLine($"The point is now at {pt}.");
   ```

1. Bạn cũng có thể tạo một tuple mới là bản sao đã sửa đổi của tuple gốc bằng cách sử dụng biểu thức `with`. Thêm đoạn mã sau vào sau mã hiện tại và gõ `dotnet tuples.cs` trong cửa sổ terminal để xem kết quả:

   ```csharp
   var pt2 = pt with { Y = 10 };
   Console.WriteLine($"The point 'pt2' is at {pt2}.");
   ```

   Tuple `pt2` chứa giá trị `X` của `pt` (6), và `pt2.Y` là 10. Tuples là các kiểu cấu trúc (structural types). Nói cách khác, kiểu tuple không có tên như `string` hay `int`. Một kiểu tuple được định nghĩa bởi số lượng thành viên, gọi là *arity*, và kiểu của các thành viên đó. Tên thành viên chỉ để thuận tiện. Bạn có thể gán một tuple cho một tuple khác có cùng arity và cùng kiểu ngay cả khi các thành viên có tên khác nhau.

1. Bạn có thể thêm đoạn mã sau vào sau mã đã viết:

   ```csharp
   var subscript = (A: 0, B: 0);
   subscript = pt;
   Console.WriteLine(subscript);
   ```

1. Hãy thử bằng cách gõ `dotnet tuples.cs` trong cửa sổ terminal. Variable `subscript` có hai thành viên, cả hai đều là số nguyên. Cả `subscript` và `pt` đều đại diện cho cùng một kiểu tuple: một tuple chứa hai thành viên `int`.

   Tuples rất dễ tạo: bạn khai báo nhiều thành viên được đặt trong dấu ngoặc đơn. Tất cả các khai báo sau đây định nghĩa các tuple khác nhau với arity và kiểu thành viên khác nhau.

1. Thêm đoạn mã sau để tạo các kiểu tuple mới:

   ```csharp
   var namedData = (Name: "Morning observation", Temp: 17, Wind: 4);
   var person = (FirstName: "", LastName: "");
   var order = (Product: "guitar picks", style: "triangle", quantity: 500, UnitPrice: 0.10m);
   ```

1. Hãy thử thay đổi này bằng cách gõ `dotnet tuples.cs` một lần nữa trong cửa sổ terminal.

Mặc dù tuples dễ tạo, nhưng khả năng của chúng có hạn. Kiểu tuple không có tên, vì vậy bạn không thể truyền tải ý nghĩa cho tập hợp các giá trị. Kiểu tuple không thể thêm hành vi. C# có những loại kiểu khác mà bạn có thể tạo khi kiểu của bạn cần định nghĩa hành vi.

> [!TIP]
> **Tìm hiểu thêm:** Khám phá [tuples và các lựa chọn kiểu khác](../../fundamentals/types/index.md) trong phần C# Fundamentals.

## Tạo kiểu record

Tuples hoạt động tốt khi bạn muốn có nhiều giá trị trong cùng một cấu trúc. Chúng nhẹ và bạn có thể khai báo ngay khi sử dụng. Khi chương trình của bạn lớn dần, bạn có thể thấy mình sử dụng cùng một kiểu tuple xuyên suốt mã. Nếu ứng dụng của bạn làm việc trong không gian đồ hoạ 2D, các tuple đại diện cho điểm có thể rất phổ biến. Khi gặp trường hợp này, hãy khai báo một kiểu `record` để lưu trữ các giá trị đó và cung cấp thêm khả năng.

1. Thêm đoạn mã sau để khai báo và sử dụng kiểu `record` đại diện cho một `Point`:

   ```csharp
   public record Point(int X, int Y);
   ```

   Đặt đoạn mã trên ở cuối file nguồn của bạn. Các khai báo kiểu như `record` phải đứng sau các câu lệnh thực thi trong một ứng dụng dạng file.

1. Thêm đoạn mã sau trước khai báo `record`:

   ```csharp
   Point pt3 = new Point(1, 1);
   var pt4 = pt3 with { Y = 10 };
   Console.WriteLine($"The two points are {pt3} and {pt4}");
   ```

   Khai báo `record` chỉ là một dòng mã cho kiểu `Point` lưu trữ các giá trị `X` và `Y` trong các thuộc tính chỉ đọc. Bạn dùng tên `Point` ở bất cứ đâu bạn sử dụng kiểu đó. Các kiểu được đặt tên đúng cách, như `Point`, cung cấp thông tin về cách kiểu đó được sử dụng. Đoạn mã bổ sung cho thấy cách sử dụng biểu thức `with` để tạo một điểm mới là bản sao đã sửa đổi của điểm hiện tại. Dòng `pt4 = pt3 with { Y = 10 }` có nghĩa là "`pt4` có cùng giá trị với `pt3` ngoại trừ `Y` được gán bằng 10". Bạn có thể thêm bất kỳ số lượng thuộc tính nào cần thay đổi trong một biểu thức `with`.

   Khai báo `record` ở trên chỉ là một dòng mã kết thúc bằng `;`. Bạn có thể thêm hành vi cho kiểu `record` bằng cách khai báo *members (thành viên)*. Một thành viên của record có thể là một hàm hoặc các phần tử dữ liệu khác. Các thành viên của một kiểu nằm trong khai báo kiểu, giữa các ký tự `{` và `}`.

1. Xoá `;` và thêm các dòng mã sau sau khai báo `record`:

   ```csharp
   {
       public double Slope() => (double)Y / (double)X;
   }
   ```

1. Thêm đoạn mã sau trước khai báo `record`, sau dòng chứa biểu thức `with`:

   ```csharp
   double slopeResult = pt4.Slope();
   Console.WriteLine($"The slope of {pt4} is {slopeResult}");
   ```

1. Gõ `dotnet tuples.cs` trong cửa sổ terminal để chạy phiên bản này.

   Bạn đã thêm tính chính thức cho *tuple* đại diện cho giá trị `X` và `Y`. Bạn đã biến nó thành một `record` định nghĩa một kiểu có tên và bao gồm một thành viên để tính độ dốc (slope). Kiểu `record` là dạng viết tắt của `record class`: một kiểu `class` bao gồm các hành vi bổ sung.

1. Bạn cũng có thể sửa đổi kiểu `Point` để biến nó thành `record struct`:

   ```csharp
   public record struct Point(int X, int Y)
   ```

   Một `record struct` là một kiểu `struct` bao gồm các hành vi bổ sung được thêm vào tất cả các kiểu `record`.

1. Hãy thử phiên bản này bằng cách gõ `dotnet tuples.cs` trong cửa sổ terminal.

## Các kiểu struct, class và interface

Tất cả các kiểu có tên cụ thể (concrete named types) trong C# đều là kiểu `class` hoặc `struct`, bao gồm cả kiểu `record`. `Class` là một *reference type (kiểu tham chiếu)*. `Struct` là một *value type (kiểu giá trị)*. Các biến của kiểu giá trị lưu trữ nội dung của instance trực tiếp trong bộ nhớ. Nói cách khác, một `record struct Point` lưu trữ hai số nguyên: `X` và `Y`. Các biến của kiểu tham chiếu lưu trữ một tham chiếu, hay con trỏ, đến vùng lưu trữ của instance. Nói cách khác, một `record class Point` lưu trữ một tham chiếu đến một khối bộ nhớ chứa các giá trị cho `X` và `Y`.

Trong thực tế, sự khác biệt này có nghĩa là các kiểu giá trị được sao chép khi gán, nhưng bản sao của một instance class là bản sao của *tham chiếu*. Tham chiếu được sao chép đó trỏ đến cùng một instance của điểm, với cùng vùng lưu trữ cho `X` và `Y`.

Bổ từ `record` hướng dẫn trình biên dịch viết một số thành viên cho bạn. Bạn có thể tìm hiểu thêm trong bài viết về [bản ghi](../../fundamentals/types/records.md) trong phần fundamentals.

Khi bạn khai báo một kiểu `record`, bạn đang tuyên bố rằng kiểu của bạn nên sử dụng một bộ hành vi mặc định cho việc so sánh bằng nhau, gán và sao chép các instance của kiểu đó. Records là lựa chọn tốt nhất khi trách nhiệm chính của kiểu là lưu trữ dữ liệu có liên quan. Khi bạn thêm nhiều hành vi hơn, hãy cân nhắc sử dụng kiểu `struct` hoặc `class` mà không có bổ từ `record`.

Sử dụng kiểu `struct` cho các kiểu giá trị khi bạn cần hành vi phức tạp hơn, nhưng trách nhiệm chính vẫn là lưu trữ giá trị. Sử dụng kiểu `class` để áp dụng các mô hình hướng đối tượng như đóng gói (encapsulation), kế thừa (inheritance) và đa hình (polymorphism).

Bạn cũng có thể định nghĩa kiểu `interface` để khai báo các hợp đồng hành vi mà các kiểu khác nhau phải triển khai. Cả kiểu `struct` và `class` đều có thể triển khai interface.

Bạn thường sử dụng tất cả các kiểu này trong các chương trình và thư viện lớn hơn. Sau khi cài đặt SDK, bạn có thể khám phá các kiểu đó qua hướng dẫn về [lớp](../../fundamentals/tutorials/classes.md) trong phần fundamentals.

Bạn đã hoàn thành bài hướng dẫn "Tạo kiểu dữ liệu trong C#".

## Dọn dẹp tài nguyên

GitHub tự động xoá Codespace của bạn sau 30 ngày không hoạt động. Nếu bạn dự định khám phá thêm các bài hướng dẫn khác trong loạt bài này, bạn có thể giữ nguyên Codespace của mình. Nếu bạn đã sẵn sàng truy cập [trang web .NET](https://dotnet.microsoft.com/download/dotnet) để tải .NET SDK, bạn có thể xoá Codespace của mình. Để xoá Codespace, hãy mở trình duyệt và truy cập [Codespaces của bạn](https://github.com/codespaces). Bạn sẽ thấy danh sách các codespace trong cửa sổ. Chọn ba dấu chấm (`...`) ở mục của codespace học tập và chọn **delete**.

## Bước tiếp theo

Tiếp tục với bài hướng dẫn tiếp theo trong loạt bài này:

> [!div class="nextstepaction"]
> [Rẽ nhánh và vòng lặp](branches-and-loops.md)

Hoặc khám phá các chủ đề liên quan trong C# Fundamentals:

- [Hệ thống kiểu dữ liệu C#](../../fundamentals/types/index.md) -- Tìm hiểu sâu hơn về các kiểu bạn đã sử dụng trong bài hướng dẫn này.
- [Bản ghi](../../fundamentals/types/records.md) -- Tìm hiểu thêm về records và khi nào nên sử dụng chúng.
- [Lớp](../../fundamentals/types/classes.md) -- Khám phá lập trình hướng đối tượng trong C#.
- [Những gì bạn có thể xây dựng với C#](../what-you-can-build.md) -- Xem các loại ứng dụng bạn có thể tạo với những kiến thức đang học.
