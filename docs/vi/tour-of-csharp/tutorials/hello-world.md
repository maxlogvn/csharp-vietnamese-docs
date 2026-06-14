---
title: Hello World - Hướng dẫn mở đầu
description: Trong hướng dẫn này, bạn sẽ tạo ứng dụng C# đầu tiên của mình. Bạn viết mã C# và tìm hiểu cấu trúc cơ bản cùng các kiểu dữ liệu trong C#.
ms.date: 02/06/2026
# customer intent: As an aspiring developer, I want to learn C#.
---
# Hướng dẫn: Khám phá ngôn ngữ C#

Hướng dẫn này sẽ dạy bạn C#. Bạn sẽ viết chương trình C# đầu tiên và thấy kết quả của việc biên dịch và chạy mã. Nó bao gồm một loạt bài học bắt đầu với chương trình "Hello World". Những bài học này dạy bạn những nền tảng cơ bản của ngôn ngữ C#.

> [!TIP]
> **Mới học lập trình?** Bắt đầu ngay tại đây - hướng dẫn này không yêu cầu kinh nghiệm trước. **Đã biết ngôn ngữ khác?** Bạn có thể muốn lướt qua các mẫu mã và nhảy tới [Số trong C#](numbers-in-csharp.md) hoặc [Rẽ nhánh và vòng lặp](branches-and-loops.md).

Trong hướng dẫn này, bạn sẽ:

> [!div class="checklist"]
>
> * Khởi chạy GitHub Codespace với môi trường phát triển C#.
> * Tạo ứng dụng C# đầu tiên của bạn.
> * Tạo và sử dụng variable (biến) để lưu trữ dữ liệu văn bản.
> * Sử dụng runtime APIs với dữ liệu văn bản.

## Điều kiện tiên quyết

Bạn cần có một trong các lựa chọn sau:

- Một tài khoản GitHub để sử dụng [GitHub Codespaces](https://github.com/codespaces). Nếu bạn chưa có, bạn có thể tạo một tài khoản miễn phí tại [GitHub.com](https://github.com).
- Một máy tính với các công cụ sau được cài đặt:
  - [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0).
  - [Visual Studio Code](https://code.visualstudio.com/download).
  - [C# DevKit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit).

## Mở Codespaces

Để khởi chạy GitHub Codespace với môi trường hướng dẫn, hãy mở trình duyệt và truy cập kho lưu trữ [tutorial codespace](https://github.com/dotnet/tutorial-codespace). Chọn nút *Code* màu xanh lá, sau đó chọn tab *Codespaces*. Tiếp theo, chọn dấu `+` để tạo một Codespace mới sử dụng môi trường này.

## Chạy chương trình đầu tiên của bạn

1. Khi codespace của bạn được tải, hãy tạo một file mới trong thư mục *tutorials* với tên *hello-world.cs*.
1. Mở file mới của bạn.
1. Gõ hoặc sao chép đoạn mã sau vào *hello-world.cs*:

   ```csharp
   Console.WriteLine("Hello, World!");
   ```

1. Trong cửa sổ terminal tích hợp, đặt thư mục *tutorials* làm thư mục hiện tại, và chạy chương trình của bạn:

   ```dotnetcli
   cd tutorials
   dotnet hello-world.cs
   ```

Bạn đã chạy chương trình C# đầu tiên của mình. Đó là một chương trình đơn giản in ra dòng chữ "Hello World!" Nó sử dụng method (phương thức) [`Console.WriteLine`](https://learn.microsoft.com/dotnet/api/system.console.writeline) để in dòng chữ đó. `Console` là một type (kiểu) đại diện cho cửa sổ console. `WriteLine` là một method của type `Console` dùng để in một dòng văn bản ra console.

Hãy tiếp tục và khám phá thêm. Phần còn lại của bài học này sẽ tìm hiểu cách làm việc với type `string`, đại diện cho văn bản trong C#. Giống như type `Console`, type `string` cũng có các method. Các method của `string` làm việc với văn bản.

## Khai báo và sử dụng biến

Chương trình đầu tiên của bạn in `string` "Hello World!" lên màn hình.

> [!TIP]
>
> Khi bạn khám phá C# (hoặc bất kỳ ngôn ngữ lập trình nào), bạn sẽ mắc lỗi khi viết mã. **Compiler (trình biên dịch)** sẽ tìm ra những lỗi đó và báo cho bạn. Khi kết quả đầu ra chứa thông báo lỗi, hãy xem kỹ mã mẫu và mã trong file `.cs` của bạn để biết cần sửa gì. Bài tập đó giúp bạn học cấu trúc của mã C#. Bạn cũng có thể hỏi Copilot để tìm sự khác biệt hoặc phát hiện lỗi.

Chương trình đầu tiên của bạn chỉ giới hạn ở việc in một thông báo. Bạn có thể viết các chương trình hữu ích hơn bằng cách sử dụng *variable (biến)*. Một *variable* là một ký hiệu bạn có thể dùng để chạy cùng một đoạn mã với các giá trị khác nhau. Hãy thử ngay!

1. Bắt đầu với đoạn mã sau:

   ```csharp
   string aFriend = "Bill";
   Console.WriteLine(aFriend);
   ```

   Dòng đầu tiên khai báo một variable `aFriend`, và gán cho nó một giá trị "Bill". Dòng thứ hai in tên đó ra.

1. Bạn có thể gán các giá trị khác nhau cho bất kỳ variable nào bạn đã khai báo. Bạn có thể đổi tên thành một người bạn của mình. Thêm hai dòng này vào sau đoạn mã bạn đã thêm. Đảm bảo bạn giữ lại khai báo của variable `aFriend` và giá trị khởi tạo của nó.

   > [!IMPORTANT]
   > Đừng xoá khai báo của `aFriend`.

1. Thêm đoạn mã sau vào cuối đoạn mã trước:

   ```csharp
   aFriend = "Maira";
   Console.WriteLine(aFriend);
   ```

   Hãy để ý rằng cùng một dòng mã in ra hai thông báo khác nhau, dựa trên giá trị được lưu trong variable `aFriend`. Bạn có thể nhận thấy từ "Hello" bị thiếu trong hai thông báo cuối. Hãy sửa điều đó ngay.

1. Sửa các dòng in thông báo thành đoạn mã sau:

   ```csharp
   Console.WriteLine("Hello " + aFriend);
   ```

1. Chạy lại ứng dụng bằng lệnh `dotnet hello-world.cs` để xem kết quả.

   Bạn đã dùng `+` để ghép **variable** với các **constant** string (chuỗi hằng). Có một cách tốt hơn. Bạn có thể đặt một variable giữa các ký tự `{` và `}` để bảo C# thay thế văn bản đó bằng giá trị của variable. Quá trình này được gọi là [Nội suy chuỗi](../../language-reference/tokens/interpolated.md).

1. Nếu bạn thêm `$` trước dấu mở ngoặc kép của string, bạn có thể bao gồm các variable, như `aFriend`, bên trong string giữa các dấu ngoặc nhọn. Hãy thử xem:

   ```csharp
   Console.WriteLine($"Hello {aFriend}");
   ```

1. Chạy lại ứng dụng bằng lệnh `dotnet hello-world.cs` để xem kết quả. Thay vì "Hello {aFriend}", thông báo sẽ là "Hello Maira".

## Làm việc với string

Lần chỉnh sửa cuối cùng là cái nhìn đầu tiên của bạn về những gì bạn có thể làm với string. Hãy khám phá thêm.

Bạn không bị giới hạn chỉ một variable giữa các dấu ngoặc nhọn.

1. Thử đoạn mã sau ở cuối ứng dụng của bạn:

   ```csharp
   string firstFriend = "Maria";
   string secondFriend = "Sage";
   Console.WriteLine($"My friends are {firstFriend} and {secondFriend}");
   ```

   String không chỉ là một tập hợp các chữ cái. Bạn có thể tìm độ dài của một string bằng cách sử dụng `Length`. `Length` là một **property (thuộc tính)** của string và nó trả về số ký tự trong string đó.

1. Thêm đoạn mã sau vào cuối ứng dụng của bạn:

   ```csharp
   Console.WriteLine($"The name {firstFriend} has {firstFriend.Length} letters.");
   Console.WriteLine($"The name {secondFriend} has {secondFriend.Length} letters.");
   ```

> [!TIP]
>
> Bây giờ là thời điểm tốt để tự mình khám phá. Bạn đã học rằng `Console.WriteLine()` ghi văn bản ra màn hình. Bạn đã học cách khai báo variable và nối các string với nhau. Hãy thử nghiệm trong mã của bạn. Trình soạn thảo có một tính năng gọi là *IntelliSense* gợi ý những gì bạn có thể làm. Gõ một dấu `.` sau chữ `d` trong `firstFriend`. Bạn sẽ thấy một danh sách các gợi ý về property và method bạn có thể sử dụng.

Bạn đã sử dụng một *method* (phương thức), [`Console.WriteLine`](https://learn.microsoft.com/dotnet/api/system.console.writeline), để in thông báo. Một *method* là một khối mã thực hiện một hành động nào đó. Nó có một cái tên để bạn có thể truy cập vào nó.

> [!TIP]
> **Tìm hiểu thêm:** Khám phá [chuỗi](../../programming-guide/strings/index.md) một cách chuyên sâu, hoặc đọc về [phương thức và cấu trúc chương trình](../../fundamentals/program-structure/index.md) trong phần C# Fundamentals.

## Loại bỏ khoảng trắng khỏi string

Giả sử string của bạn có khoảng trắng ở đầu hoặc cuối mà bạn không muốn hiển thị. Bạn muốn **trim (cắt bỏ)** khoảng trắng khỏi string.
Method [`String.Trim`](https://learn.microsoft.com/dotnet/api/system.string.trim) và các method liên quan [`String.TrimStart`](https://learn.microsoft.com/dotnet/api/system.string.trimstart) và [`String.TrimEnd`](https://learn.microsoft.com/dotnet/api/system.string.trimend) thực hiện việc này. Hãy sử dụng các method này để loại bỏ khoảng trắng ở đầu và cuối.

1. Thử đoạn mã sau:

   ```csharp
   string greeting = "      Hello World!       ";
   Console.WriteLine($"[{greeting}]");

   string trimmedGreeting = greeting.TrimStart();
   Console.WriteLine($"[{trimmedGreeting}]");

   trimmedGreeting = greeting.TrimEnd();
   Console.WriteLine($"[{trimmedGreeting}]");

   trimmedGreeting = greeting.Trim();
   Console.WriteLine($"[{trimmedGreeting}]");
   ```

Các dấu ngoặc vuông `[` và `]` giúp bạn hình dung các method `Trim`, `TrimStart`, và `TrimEnd` làm gì. Các dấu ngoặc cho thấy khoảng trắng bắt đầu và kết thúc ở đâu.

Mẫu này củng cố một vài khái niệm quan trọng khi làm việc với string. Các method thao tác trên string trả về các đối tượng string mới thay vì sửa đổi trực tiếp trên string gốc. Bạn có thể thấy rằng mỗi lần gọi bất kỳ method `Trim` nào đều trả về một string mới nhưng không thay đổi thông báo gốc.

## Tìm kiếm và thay thế văn bản trong string

Bạn có thể sử dụng các method khác để làm việc với string. Ví dụ, bạn có thể dùng lệnh tìm kiếm và thay thế trong trình soạn thảo hoặc xử lý văn bản. Method [`String.Replace`](https://learn.microsoft.com/dotnet/api/system.string.replace) làm điều tương tự trong string. Nó tìm kiếm một chuỗi con và thay thế nó bằng một văn bản khác. Method [`String.Replace`](https://learn.microsoft.com/dotnet/api/system.string.replace) nhận hai **parameter (tham số)**. Các parameter này là các string nằm giữa dấu ngoặc đơn. String đầu tiên là văn bản cần tìm. String thứ hai là văn bản để thay thế. Hãy tự mình thử.

1. Thêm đoạn mã này. Gõ nó vào để thấy các gợi ý khi bạn bắt đầu gõ `.Re` sau variable `sayHello`:

   ```csharp
   string sayHello = "Hello World!";
   Console.WriteLine(sayHello);
   sayHello = sayHello.Replace("Hello", "Greetings");
   Console.WriteLine(sayHello);
   ```

   Hai method hữu ích khác là làm cho string thành tất cả chữ hoa hoặc tất cả chữ thường. Hãy thử đoạn mã sau.

1. Gõ nó vào để xem **IntelliSense** cung cấp gợi ý như thế nào khi bạn bắt đầu gõ `To`:

   ```csharp
   Console.WriteLine(sayHello.ToUpper());
   Console.WriteLine(sayHello.ToLower());
   ```

   Một phần khác của thao tác *tìm kiếm và thay thế* là tìm văn bản trong một string. Bạn có thể sử dụng method [`String.Contains`](https://learn.microsoft.com/dotnet/api/system.string.contains) để tìm kiếm. Nó cho bạn biết liệu một string có chứa một chuỗi con bên trong nó hay không.

1. Thử đoạn mã sau để khám phá [`String.Contains`](https://learn.microsoft.com/dotnet/api/system.string.contains):

   ```csharp
   string songLyrics = "You say goodbye, and I say hello";
   Console.WriteLine(songLyrics.Contains("goodbye"));
   Console.WriteLine(songLyrics.Contains("greetings"));
   ```

   Method [`String.Contains`](https://learn.microsoft.com/dotnet/api/system.string.contains) trả về một giá trị *boolean* cho bạn biết liệu string bạn đang tìm có được tìm thấy hay không. Một *boolean* lưu trữ giá trị `true` hoặc `false`. Khi được hiển thị dưới dạng văn bản đầu ra, chúng được viết hoa: `True` và `False`. Bạn sẽ tìm hiểu thêm về giá trị *boolean* trong bài học sau.

## Thử thách

Hai method tương tự, [`String.StartsWith`](https://learn.microsoft.com/dotnet/api/system.string.startswith) và [`String.EndsWith`](https://learn.microsoft.com/dotnet/api/system.string.endswith), cũng tìm kiếm chuỗi con trong string. Các method này tìm một chuỗi con ở đầu hoặc ở cuối string. Hãy thử sửa đổi mẫu trước đó để dùng [`String.StartsWith`](https://learn.microsoft.com/dotnet/api/system.string.startswith) và [`String.EndsWith`](https://learn.microsoft.com/dotnet/api/system.string.endswith) thay vì [`String.Contains`](https://learn.microsoft.com/dotnet/api/system.string.contains). Tìm kiếm "You" hoặc "goodbye" ở đầu một string. Tìm kiếm "hello" hoặc "goodbye" ở cuối một string.

> [!NOTE]
>
> Hãy chú ý đến dấu câu khi bạn kiểm tra văn bản ở cuối string. Nếu string kết thúc bằng dấu chấm, bạn phải kiểm tra một string kết thúc bằng dấu chấm.

Bạn sẽ nhận được `true` khi bắt đầu bằng "You" và kết thúc bằng "hello", và `false` khi bắt đầu bằng hoặc kết thúc bằng "goodbye".

Bạn đã nghĩ ra điều gì đó giống như đoạn mã sau đây không (mở rộng để xem đáp án):

<!-- markdownlint-disable MD033 -->
<details>

```csharp
string songLyrics = "You say goodbye, and I say hello";
Console.WriteLine(songLyrics.StartsWith("You"));
Console.WriteLine(songLyrics.StartsWith("goodbye"));

Console.WriteLine(songLyrics.EndsWith("hello"));
Console.WriteLine(songLyrics.EndsWith("goodbye"));
```

</details>
<!-- markdownlint-enable MD033 -->

Để đọc thêm về type `string`:

- [Bài viết hướng dẫn C# về chuỗi](../../programming-guide/strings/index.md).
- [Mẹo làm việc với chuỗi](../../how-to/index.md#working-with-strings).

## Dọn dẹp tài nguyên

GitHub tự động xoá Codespace của bạn sau 30 ngày không hoạt động. Nếu bạn dự định khám phá thêm các hướng dẫn trong loạt bài này, bạn có thể để Codespace của bạn hoạt động. Nếu bạn đã sẵn sàng truy cập [trang .NET](https://dotnet.microsoft.com/download/dotnet) để tải .NET SDK, bạn có thể xoá Codespace của mình. Để xoá Codespace, hãy mở cửa sổ trình duyệt và điều hướng đến [Codespaces của bạn](https://github.com/codespaces). Bạn sẽ thấy danh sách các codespace của mình trong cửa sổ. Chọn ba dấu chấm (`...`) trong mục của codespace học tập và chọn "delete".

## Bước tiếp theo

Tiếp tục với hướng dẫn tiếp theo trong loạt bài này, hoặc khám phá các chủ đề liên quan trong C# Fundamentals:

> [!div class="nextstepaction"]
> [Khám phá số trong C#](numbers-in-csharp.md)

- [Chuỗi](../../programming-guide/strings/index.md) -- Tìm hiểu thêm về type `string` bạn đã sử dụng trong hướng dẫn này.
- [Phương thức và cấu trúc chương trình](../../fundamentals/program-structure/index.md) -- Hiểu cách các chương trình C# được tổ chức.
- [Ứng dụng dạng file](../../fundamentals/tutorials/file-based-programs.md) -- Tìm hiểu về lệnh `dotnet run` bạn đã dùng để chạy mã của mình.
