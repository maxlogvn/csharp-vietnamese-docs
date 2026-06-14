---
title: Pattern matching (So khớp mẫu)
description: Trong hướng dẫn này về pattern matching (so khớp mẫu), bạn sẽ học C#. Bạn sẽ viết code C# và xem kết quả biên dịch cũng như chạy code của mình.
ms.date: 02/09/2026
---
# Hướng dẫn: Sử dụng C# để so khớp dữ liệu với mẫu

Hướng dẫn này sẽ dạy bạn cách sử dụng pattern matching (so khớp mẫu) để kiểm tra dữ liệu trong C#. Bạn sẽ viết một lượng nhỏ code, sau đó biên dịch và chạy code đó. Hướng dẫn bao gồm một loạt bài học khám phá các loại pattern (mẫu) khác nhau được C# hỗ trợ. Những bài học này sẽ cung cấp cho bạn kiến thức nền tảng về ngôn ngữ C#.

> [!TIP]
> **Mới học lập trình?** Hãy làm theo từng phần theo thứ tự. **Đến từ ngôn ngữ khác?** Nếu bạn đã biết câu lệnh `switch`, hãy tập trung vào [exhaustive matches](#exhaustive-matches-voi-switch) (so khớp toàn diện) và [type patterns](#type-patterns-mẫu-kiểu) - đây là những tính năng đặc trưng của C#.

Trong hướng dẫn này, bạn sẽ:

> [!div class="checklist"]
>
> * Khởi chạy GitHub Codespace với môi trường phát triển C#.
> * Kiểm tra dữ liệu với các giá trị rời rạc.
> * So khớp dữ liệu enum (liệt kê) với giá trị.
> * Tạo exhaustive matches (so khớp toàn diện) bằng `switch` expressions (biểu thức switch).
> * So khớp các kiểu dữ liệu bằng type patterns (mẫu kiểu).

## Điều kiện tiên quyết

Bạn cần có một trong các lựa chọn sau:

- Tài khoản GitHub để sử dụng [GitHub Codespaces](https://github.com/codespaces). Nếu chưa có, bạn có thể tạo tài khoản miễn phí tại [GitHub.com](https://github.com).
- Một máy tính đã cài đặt các công cụ sau:
  - [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0).
  - [Visual Studio Code](https://code.visualstudio.com/download).
  - [C# DevKit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit).

## So khớp một giá trị

Các hướng dẫn trước đã giới thiệu về built-in types (kiểu dựng sẵn) và các kiểu bạn tự định nghĩa dưới dạng tuple (bộ) hoặc record (bản ghi). Bạn có thể kiểm tra các instance (thể hiện) của những kiểu này dựa trên một *pattern* (mẫu). Việc một instance có khớp với pattern hay không sẽ quyết định hành động mà chương trình của bạn thực hiện. Trong các ví dụ sau, bạn sẽ thấy dấu `?` sau tên kiểu. Ký hiệu này cho phép giá trị của kiểu đó có thể là null (ví dụ: `bool?` có thể là `true`, `false` hoặc `null`). Để biết thêm thông tin, hãy xem [Nullable value types](../../language-reference/builtin-types/nullable-value-types.md) (Kiểu giá trị có thể null). Hãy bắt đầu khám phá cách bạn có thể sử dụng patterns.

Để khởi chạy GitHub Codespace với môi trường hướng dẫn, hãy mở trình duyệt đến kho lưu trữ [tutorial codespace](https://github.com/dotnet/tutorial-codespace). Chọn nút *Code* màu xanh lá, sau đó chọn tab *Codespaces*. Tiếp theo, chọn dấu `+` để tạo Codespace mới sử dụng môi trường này. Nếu bạn đã hoàn thành các hướng dẫn khác trong loạt bài này, bạn có thể mở codespace đó.

1. Khi codespace của bạn đã tải xong, hãy tạo một file mới trong thư mục *tutorials* có tên là *patterns.cs*.
1. Mở file mới của bạn.

1. Tất cả các ví dụ trong hướng dẫn này đều sử dụng dữ liệu đầu vào dạng văn bản đại diện cho một loạt giao dịch ngân hàng dưới dạng CSV (giá trị phân cách bằng dấu phẩy). Trong mỗi mẫu, bạn có thể so khớp bản ghi với một pattern bằng cách sử dụng biểu thức `is` hoặc `switch`. Ví dụ đầu tiên này chia mỗi dòng dựa trên ký tự `,` và sau đó *so khớp* trường chuỗi đầu tiên với giá trị "DEPOSIT" hoặc "WITHDRAWAL" bằng biểu thức `is`. Khi khớp, số tiền giao dịch sẽ được cộng hoặc trừ vào số dư tài khoản hiện tại. Để xem nó hoạt động, hãy thêm code sau vào *patterns.cs*:

   ```csharp
   string bankRecords = """
       DEPOSIT,   10000, Initial balance
       DEPOSIT,     500, regular deposit
       WITHDRAWAL, 1000, rent
       DEPOSIT,    2000, freelance payment
       WITHDRAWAL,  300, groceries
       DEPOSIT,     700, gift from friend
       WITHDRAWAL,  150, utility bill
       DEPOSIT,    1200, tax refund
       WITHDRAWAL,  500, car maintenance
       DEPOSIT,     400, cashback reward
       WITHDRAWAL,  250, dining out
       DEPOSIT,    3000, bonus payment
       WITHDRAWAL,  800, loan repayment
       DEPOSIT,     600, stock dividends
       WITHDRAWAL,  100, subscription fee
       DEPOSIT,    1500, side hustle income
       WITHDRAWAL,  200, fuel expenses
       DEPOSIT,     900, refund from store
       WITHDRAWAL,  350, shopping
       DEPOSIT,    2500, project milestone payment
       WITHDRAWAL,  400, entertainment
       """;

   double currentBalance = 0.0;
   var reader = new StringReader(bankRecords);

   string? line;
   while ((line = reader.ReadLine()) is not null)
   {
       if (string.IsNullOrWhiteSpace(line)) continue;
       // Split the line based on comma delimiter and trim each part
       string[] parts = line.Split(',');

       string? transactionType = parts[0]?.Trim();
       if (double.TryParse(parts[1].Trim(), out double amount))
       {
           // Update the balance based on transaction type
           if (transactionType?.ToUpper() is "DEPOSIT")
               currentBalance += amount;
           else if (transactionType?.ToUpper() is "WITHDRAWAL")
               currentBalance -= amount;

           Console.WriteLine($"{line.Trim()} => Parsed Amount: {amount}, New Balance: {currentBalance}");
       }
   }
   ```

1. Sau đó, gõ dòng sau trong cửa sổ terminal:

   ```dotnetcli
   cd tutorials
   dotnet patterns.cs
   ```

1. Xem kết quả đầu ra.
   Bạn có thể thấy rằng mỗi dòng được xử lý bằng cách so sánh giá trị của văn bản trong trường đầu tiên.

Bạn cũng có thể xây dựng ví dụ trên bằng cách sử dụng toán tử `==` để kiểm tra xem hai giá trị `string` có bằng nhau hay không. So sánh một variable (biến) với một hằng số là một khối xây dựng cơ bản cho pattern matching. Hãy cùng khám phá thêm các khối xây dựng khác trong pattern matching.

> [!TIP]
> **Tìm hiểu thêm:** Đọc về [pattern matching](../../fundamentals/functional/pattern-matching.md) trong phần C# Fundamentals để có cái nhìn tổng quan toàn diện về tất cả các loại pattern.

## So khớp Enum

Một ứng dụng phổ biến khác của pattern matching là so khớp trên các giá trị của kiểu `enum` (liệt kê). Mẫu sau đây xử lý các bản ghi đầu vào để tạo ra một *tuple* (bộ) mà giá trị đầu tiên là một giá trị `enum` đánh dấu khoản tiền gửi hoặc rút tiền. Giá trị thứ hai là giá trị của giao dịch.

1. Thêm code sau vào cuối file nguồn của bạn. Nó định nghĩa enumeration `TransactionType`:

   ```csharp
   public enum TransactionType
   {
       Deposit,
       Withdrawal,
       Invalid
   }
   ```

1. Thêm một hàm để phân tích một giao dịch ngân hàng thành một tuple chứa loại giao dịch và giá trị giao dịch. Thêm code sau trước khai báo enum `TransactionType` của bạn:

   ```csharp
   static IEnumerable<(TransactionType type, double amount)> TransactionRecords(string inputText)
   {
       var reader = new StringReader(inputText);
       string? line;
       while ((line = reader.ReadLine()) is not null)
       {
           string[] parts = line.Split(',');

           string? transactionType = parts[0]?.Trim();
           if (double.TryParse(parts[1].Trim(), out double amount))
           {
               // Update the balance based on transaction type
               if (transactionType?.ToUpper() is "DEPOSIT")
                   yield return (TransactionType.Deposit, amount);
               else if (transactionType?.ToUpper() is "WITHDRAWAL")
                   yield return (TransactionType.Withdrawal, amount);
           }
           else {
           yield return (TransactionType.Invalid, 0.0);
           }
       }
   }
   ```

1. Thêm một vòng lặp mới để xử lý dữ liệu giao dịch bằng cách sử dụng enumeration `TransactionType` bạn đã khai báo:

   ```csharp
   currentBalance = 0.0;

   foreach (var transaction in TransactionRecords(bankRecords))
   {
       if (transaction.type == TransactionType.Deposit)
           currentBalance += transaction.amount;
       else if (transaction.type == TransactionType.Withdrawal)
           currentBalance -= transaction.amount;
       Console.WriteLine($"{transaction.type} => Parsed Amount: {transaction.amount}, New Balance: {currentBalance}");
   }
   ```

Ví dụ trên cũng sử dụng câu lệnh `if` để kiểm tra giá trị của một biểu thức `enum`. Một dạng khác của pattern matching sử dụng biểu thức `switch`. Hãy cùng khám phá cú pháp đó và cách bạn có thể sử dụng nó.

## Exhaustive matches với `switch`

Một chuỗi các câu lệnh `if` có thể kiểm tra một loạt các điều kiện. Tuy nhiên, trình biên dịch không thể biết liệu một chuỗi các câu lệnh `if` có *exhaustive* (toàn diện) hay không, hoặc liệu các điều kiện `if` sau có bị *subsumed* (bao hàm) bởi các điều kiện trước hay không. *Exhaustive* có nghĩa là một trong các mệnh đề `if` hoặc `else` trong chuỗi kiểm tra xử lý tất cả các đầu vào có thể có. Nếu một chuỗi các câu lệnh `if` là exhaustive, mọi đầu vào khả dĩ đều thoả mãn ít nhất một mệnh đề `if` hoặc `else`. *Subsumption* (sự bao hàm) có nghĩa là một mệnh đề `if` hoặc `else` sau không thể được chạm tới vì các mệnh đề `if` hoặc `else` trước đã khớp với tất cả các đầu vào có thể. Ví dụ, trong đoạn code mẫu sau, một mệnh đề không bao giờ khớp:

```csharp
int n = GetNumber();

if (n < 20)
    Console.WriteLine("n is less than 20");
else if (n < 10)
    Console.WriteLine("n is less than 10"); // unreachable
else
    Console.WriteLine("n is greater than 20");
```

Mệnh đề `else if` không bao giờ khớp vì mọi số nhỏ hơn 10 cũng đều nhỏ hơn 20. Biểu thức `switch` đảm bảo cả hai đặc điểm này đều được thoả mãn, giúp giảm thiểu lỗi trong ứng dụng của bạn. Hãy thử nghiệm nó.

1. Sao chép code sau. Thay thế hai câu lệnh `if` trong vòng lặp `foreach` của bạn bằng biểu thức `switch` bạn vừa sao chép.

   ```csharp
   currentBalance += transaction switch
   {
       (TransactionType.Deposit, var amount) => amount,
       (TransactionType.Withdrawal, var amount) => -amount,
       _ => 0.0,
   };
   ```

1. Gõ `dotnet patterns.cs` trong cửa sổ terminal để chạy mẫu mới.

   Khi bạn chạy code, bạn sẽ thấy nó hoạt động giống như trước.

1. Để minh hoạ *subsumption* (sự bao hàm), hãy sắp xếp lại các nhánh switch như trong đoạn sau:

   ```csharp
   currentBalance += transaction switch
   {
       (TransactionType.Deposit, var amount) => amount,
       _ => 0.0,
       (TransactionType.Withdrawal, var amount) => -amount,
   };
   ```

   Sau khi bạn sắp xếp lại các nhánh switch, hãy gõ `dotnet patterns.cs` trong cửa sổ terminal. Trình biên dịch sẽ báo lỗi vì nhánh `_` khớp với mọi giá trị. Kết quả là nhánh cuối cùng với `TransactionType.Withdrawal` không bao giờ chạy. Trình biên dịch cho bạn biết rằng có điều gì đó không ổn trong code của bạn.

   Trình biên dịch sẽ báo warning (cảnh báo) nếu biểu thức được kiểm tra trong biểu thức `switch` có thể chứa các giá trị không khớp với bất kỳ nhánh switch nào. Nếu một số giá trị không thể khớp với bất kỳ điều kiện nào, biểu thức `switch` không phải là *exhaustive*. Trình biên dịch cũng báo warning nếu một số giá trị đầu vào không khớp với bất kỳ nhánh switch nào.

1. Xoá dòng `_ => 0.0,` để các giá trị không hợp lệ không khớp.
1. Gõ `dotnet patterns.cs` để xem kết quả.

   Trình biên dịch báo warning. Dữ liệu kiểm tra là hợp lệ, vì vậy chương trình vẫn chạy. Tuy nhiên, bất kỳ dữ liệu không hợp lệ nào cũng sẽ gây ra lỗi khi chạy.

## Type patterns (Mẫu kiểu)

Để kết thúc hướng dẫn này, hãy khám phá thêm một khối xây dựng nữa của pattern matching: *type pattern* (mẫu kiểu). Một *type pattern* kiểm tra một biểu thức tại thời điểm chạy để xem nó có phải là kiểu được chỉ định hay không. Bạn có thể sử dụng phép kiểm tra kiểu với biểu thức `is` hoặc biểu thức `switch`. Hãy sửa đổi mẫu hiện tại theo hai cách. Đầu tiên, thay vì dùng tuple, hãy xây dựng các kiểu record `Deposit` và `Withdrawal` đại diện cho các giao dịch.

1. Thêm các khai báo sau vào cuối file code của bạn:

   ```csharp
   public record Deposit(double Amount, string description);
   public record Withdrawal(double Amount, string description);
   ```

1. Thêm method này ngay trước khai báo enumeration `TransactionType`. Nó phân tích văn bản và trả về một loạt các record:

   ```csharp
   static IEnumerable<object?> TransactionRecordType(string inputText)
   {
       var reader = new StringReader(inputText);
       string? line;
       while ((line = reader.ReadLine()) is not null)
       {
           string[] parts = line.Split(',');

           string? transactionType = parts[0]?.Trim();
           if (double.TryParse(parts[1].Trim(), out double amount))
           {
               // Update the balance based on transaction type
               if (transactionType?.ToUpper() is "DEPOSIT")
                   yield return new Deposit(amount, parts[2]);
               else if (transactionType?.ToUpper() is "WITHDRAWAL")
                   yield return new Withdrawal(amount, parts[2]);
           }
       }
   }
   ```

1. Thêm code sau sau vòng lặp `foreach` cuối cùng:

   ```csharp
   currentBalance = 0.0;

   foreach (var transaction in TransactionRecordType(bankRecords))
   {
       currentBalance += transaction switch
       {
           Deposit d => d.Amount,
           Withdrawal w => -w.Amount,
           _ => 0.0,
       };
       Console.WriteLine($" {transaction} => New Balance: {currentBalance}");
   }
   ```

1. Gõ `dotnet patterns.cs` trong cửa sổ terminal để xem kết quả. Phiên bản cuối cùng này kiểm tra đầu vào dựa trên một *type* (kiểu).

Pattern matching cung cấp một từ vựng để so sánh một biểu thức với các đặc điểm. Patterns có thể bao gồm kiểu của biểu thức, giá trị của các kiểu, giá trị thuộc tính và sự kết hợp của chúng. So sánh biểu thức với một pattern có thể rõ ràng hơn so với nhiều phép so sánh `if`. Bạn đã khám phá một số patterns bạn có thể sử dụng để so khớp biểu thức. Còn nhiều cách khác để sử dụng pattern matching trong ứng dụng của bạn. Khi bạn khám phá thêm, bạn có thể tìm hiểu thêm về pattern matching trong C# qua các bài viết sau:

- [So khớp mẫu trong C#](../../fundamentals/functional/pattern-matching.md)
- [Khám phá hướng dẫn so khớp mẫu](../../tutorials/patterns-objects.md)
- [Tình huống so khớp mẫu](../../fundamentals/tutorials/pattern-matching.md)
- [Hệ thống kiểu C#](../../fundamentals/types/index.md) - Tìm hiểu về các kiểu bạn đã so khớp trong hướng dẫn này.

## Dọn dẹp tài nguyên

GitHub tự động xoá Codespace của bạn sau 30 ngày không hoạt động. Bạn đã hoàn thành tất cả các hướng dẫn trong loạt bài này. Để xoá Codespace của bạn ngay bây giờ, hãy mở cửa sổ trình duyệt và truy cập [Codespaces của bạn](https://github.com/codespaces). Bạn sẽ thấy một danh sách các codespace của mình trong cửa sổ. Chọn ba dấu chấm (`...`) trong mục nhập cho codespace học tập và chọn **delete**.

## Các bước tiếp theo

Bạn đã hoàn thành tất cả các hướng dẫn giới thiệu! Dưới đây là hướng đi tiếp theo:

- [Ứng dụng dạng file](../../fundamentals/tutorials/file-based-programs.md) - Tìm hiểu về lệnh `dotnet run` bạn đã sử dụng trong suốt các hướng dẫn này.
- [Kiến thức nền tảng C#](../../fundamentals/program-structure/index.md) - Đi sâu hơn vào cấu trúc chương trình, kiểu dữ liệu và lập trình hướng đối tượng.
- [Những gì bạn có thể xây dựng với C#](../what-you-can-build.md) - Xem các loại ứng dụng bạn có thể tạo với những gì đã học.
- Tải xuống và cài đặt [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0).
- Tải xuống và cài đặt [Visual Studio Code](https://code.visualstudio.com/download).
- Tải xuống và cài đặt [C# DevKit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit).
