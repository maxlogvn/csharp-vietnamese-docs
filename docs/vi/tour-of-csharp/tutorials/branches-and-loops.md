---
title: "Rẽ nhánh và vòng lặp - Hướng dẫn nhập môn"
description: "Trong hướng dẫn này về rẽ nhánh và vòng lặp, bạn sẽ viết mã C# để khám phá cú pháp ngôn ngữ hỗ trợ rẽ nhánh có điều kiện và vòng lặp để thực thi các câu lệnh lặp đi lặp lại. Bạn viết mã C# và xem kết quả biên dịch cũng như chạy mã trực tiếp trên trình duyệt."
ms.date: 02/09/2026
---

# Hướng dẫn: Câu lệnh `if` và vòng lặp trong C# - logic điều kiện

Hướng dẫn này sẽ dạy bạn cách viết mã C# để kiểm tra các variable (biến) và thay đổi luồng thực thi dựa trên các biến đó. Bạn sẽ viết mã C# và xem kết quả biên dịch cũng như chạy thử. Hướng dẫn bao gồm một loạt bài học khám phá các cấu trúc rẽ nhánh và vòng lặp trong C#. Những bài học này sẽ giúp bạn nắm vững những kiến thức nền tảng của ngôn ngữ C#.

> [!TIP]
> **Mới học lập trình?** Hãy làm lần lượt từng phần theo thứ tự. **Đã biết ngôn ngữ khác?** Cú pháp `if`/`else` và vòng lặp chắc hẳn rất quen thuộc - hãy tập trung vào [vòng lặp lồng nhau](#created-nested-loops) và [bài tập thử thách](#combine-branches-and-loops) để thực hành các mẫu đặc trưng của C#.

Trong hướng dẫn này, bạn sẽ:

> [!div class="checklist"]
>
> * Khởi chạy GitHub Codespace với môi trường phát triển C#.
> * Khám phá câu lệnh `if` và `else`.
> * Sử dụng vòng lặp để lặp lại các thao tác.
> * Làm việc với vòng lặp lồng nhau.
> * Kết hợp rẽ nhánh và vòng lặp.

## Điều kiện tiên quyết

Bạn cần có một trong các lựa chọn sau:

- Một tài khoản GitHub để sử dụng [GitHub Codespaces](https://github.com/codespaces). Nếu chưa có, hãy tạo một tài khoản miễn phí tại [GitHub.com](https://github.com).
- Một máy tính đã cài các công cụ sau:
  - [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0).
  - [Visual Studio Code](https://code.visualstudio.com/download).
  - [C# DevKit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit).

## Sử dụng câu lệnh if

Để khởi chạy GitHub Codespace với môi trường hướng dẫn, hãy mở trình duyệt và truy cập kho lưu trữ [tutorial codespace](https://github.com/dotnet/tutorial-codespace). Chọn nút *Code* màu xanh lá, sau đó chọn tab *Codespaces*. Tiếp theo, chọn dấu `+` để tạo một Codespace mới sử dụng môi trường này. Nếu bạn đã hoàn thành các hướng dẫn khác trong loạt bài này, bạn có thể mở lại codespace đó thay vì tạo mới.

1. Khi codespace của bạn đã sẵn sàng, hãy tạo một file mới trong thư mục *tutorials* với tên *branches-loops.cs*.
1. Mở file mới của bạn.
1. Gõ hoặc sao chép đoạn mã sau vào *branches-loops.cs*:

   ```csharp
   int a = 5;
   int b = 6;
   if (a + b > 10)
       Console.WriteLine("The answer is greater than 10.");
   ```

1. Hãy thử chạy đoạn mã này bằng cách gõ lệnh sau trong terminal tích hợp:

   ```dotnetcli
   cd tutorials
   dotnet branches-loops.cs
   ```

   Bạn sẽ thấy dòng chữ "The answer is greater than 10." được in ra console.

1. Thay đổi khai báo của `b` sao cho tổng nhỏ hơn 10:

   ```csharp
   int b = 3;
   ```

1. Gõ lại `dotnet branches-loops.cs` trong cửa sổ terminal.

   Vì kết quả nhỏ hơn 10 nên không có gì được in ra. **Điều kiện** bạn đang kiểm tra là sai (false). Bạn chưa có mã nào để thực thi vì bạn mới chỉ viết một trong hai nhánh có thể có của câu lệnh `if`: nhánh đúng (true).

> [!TIP]
> Trong quá trình khám phá C# (hoặc bất kỳ ngôn ngữ lập trình nào), bạn có thể sẽ mắc lỗi khi viết mã. Trình biên dịch sẽ tìm ra và báo cáo các lỗi đó. Hãy xem kỹ thông báo lỗi và đoạn mã đã gây ra lỗi. Bạn cũng có thể nhờ Copilot tìm ra sự khác biệt hoặc phát hiện lỗi. Thông báo lỗi từ trình biên dịch thường sẽ giúp bạn tìm ra vấn đề.

Ví dụ đầu tiên này cho thấy sức mạnh của `if` và kiểu Boolean. Một *Boolean* là một biến có thể nhận một trong hai giá trị: `true` hoặc `false`. C# định nghĩa một kiểu đặc biệt, `bool`, dành cho các biến Boolean. Câu lệnh `if` kiểm tra giá trị của một `bool`. Khi giá trị là `true`, câu lệnh theo sau `if` sẽ được thực thi. Ngược lại, nó sẽ bị bỏ qua. Quá trình kiểm tra điều kiện và thực thi câu lệnh dựa trên các điều kiện đó thực sự rất mạnh mẽ. Hãy cùng khám phá thêm.

## Làm cho if và else hoạt động cùng nhau

Để thực thi các đoạn mã khác nhau ở cả nhánh đúng và nhánh sai, bạn cần tạo một nhánh `else` chạy khi điều kiện là sai. Hãy thử một nhánh `else`.

1. Thêm hai dòng cuối cùng trong đoạn mã sau (bạn đã có bốn dòng đầu tiên):

   ```csharp
   int a = 5;
   int b = 3;
   if (a + b > 10)
       Console.WriteLine("The answer is greater than 10");
   else
       Console.WriteLine("The answer is not greater than 10");
   ```

   Câu lệnh theo sau từ khóa `else` chỉ thực thi khi điều kiện đang kiểm tra là `false`. Việc kết hợp `if` và `else` với các điều kiện Boolean cung cấp cho bạn tất cả sức mạnh cần thiết để xử lý cả hai trường hợp `true` và `false`.

   > [!IMPORTANT]
   > Việc thụt dòng dưới các câu lệnh `if` và `else` là dành cho người đọc. Ngôn ngữ C# không coi trọng việc thụt dòng hay khoảng trắng. Câu lệnh theo sau từ khóa `if` hoặc `else` sẽ thực thi dựa trên điều kiện. Tất cả các mẫu trong hướng dẫn này đều tuân theo một thông lệ phổ biến là thụt dòng dựa trên luồng điều khiển của các câu lệnh.

   Vì thụt dòng không quan trọng, bạn cần sử dụng `{` và `}` để chỉ ra khi nào bạn muốn có nhiều hơn một câu lệnh thuộc về khối thực thi có điều kiện. Các lập trình viên C# thường sử dụng dấu ngoặc nhọn cho tất cả các mệnh đề `if` và `else`.

1. Ví dụ sau tương tự như những gì bạn đã tạo ở ví dụ trước, nhưng có thêm `{` và `}`. Hãy sửa mã của bạn để khớp với đoạn mã sau:

   ```csharp
   int a = 5;
   int b = 3;
   if (a + b > 10)
   {
       Console.WriteLine("The answer is greater than 10");
   }
   else
   {
       Console.WriteLine("The answer is not greater than 10");
   }
   ```

   > [!TIP]
   > Trong suốt phần còn lại của hướng dẫn này, các mẫu mã đều bao gồm dấu ngoặc nhọn, tuân theo các thông lệ được chấp nhận.

1. Bạn có thể thử nghiệm với các điều kiện phức tạp hơn. Thêm đoạn mã sau vào sau đoạn mã bạn đã viết:

   ```csharp
   int a = 5;
   int b = 3;
   int c = 4;
   if ((a + b + c > 10) && (a == b))
   {
       Console.WriteLine("The answer is greater than 10");
       Console.WriteLine("And the first number is equal to the second");
   }
   else
   {
       Console.WriteLine("The answer is not greater than 10");
       Console.WriteLine("Or the first number is not equal to the second");
   }
   ```

   Ký hiệu `==` dùng để kiểm tra **sự bằng nhau**. Việc sử dụng `==` giúp phân biệt phép kiểm tra bằng nhau với phép gán, như bạn đã thấy trong `a = 5`.

   `&&` đại diện cho "và" (and). Nó có nghĩa là cả hai điều kiện phải đúng thì câu lệnh trong nhánh đúng mới được thực thi. Các ví dụ này cũng cho thấy bạn có thể có nhiều câu lệnh trong mỗi nhánh có điều kiện, miễn là bạn đặt chúng trong `{` và `}`.

1. Bạn cũng có thể sử dụng `||` để đại diện cho "hoặc" (or). Thêm đoạn mã sau vào sau những gì bạn đã viết:

   ```csharp
   if ((a + b + c > 10) || (a == b))
   ```

1. Hãy thay đổi các giá trị của `a`, `b`, và `c` cũng như chuyển đổi giữa `&&` và `||` để khám phá thêm. Bạn sẽ hiểu rõ hơn về cách hoạt động của các toán tử `&&` và `||`.

1. Bạn đã hoàn thành bước đầu tiên. Trước khi bắt đầu phần tiếp theo, hãy chuyển đoạn mã hiện tại vào một method (phương thức) riêng. Việc này sẽ giúp bạn dễ dàng bắt đầu với một ví dụ mới hơn. Đặt đoạn mã hiện tại vào một method có tên là `ExploreIf()`. Gọi nó từ đầu chương trình của bạn. Sau khi hoàn tất các thay đổi này, mã của bạn sẽ trông như sau:

   ```csharp
   ExploreIf();

   void ExploreIf()
   {
       int a = 5;
       int b = 3;
       if (a + b > 10)
       {
           Console.WriteLine("The answer is greater than 10");
       }
       else
       {
           Console.WriteLine("The answer is not greater than 10");
       }

       int c = 4;
       if ((a + b + c > 10) && (a > b))
       {
           Console.WriteLine("The answer is greater than 10");
           Console.WriteLine("And the first number is greater than the second");
       }
       else
       {
           Console.WriteLine("The answer is not greater than 10");
           Console.WriteLine("Or the first number is not greater than the second");
       }

       if ((a + b + c > 10) || (a > b))
       {
           Console.WriteLine("The answer is greater than 10");
           Console.WriteLine("Or the first number is greater than the second");
       }
       else
       {
           Console.WriteLine("The answer is not greater than 10");
           Console.WriteLine("And the first number is not greater than the second");
       }
   }
   ```

1. Hãy comment dòng gọi `ExploreIf()` lại để đầu ra bớt rối khi bạn làm việc ở phần này:

   ```csharp
   //ExploreIf();
   ```

`//` bắt đầu một **comment (chú thích)** trong C#. Comments là bất kỳ văn bản nào bạn muốn giữ lại trong mã nguồn nhưng không thực thi như mã lệnh. Trình biên dịch sẽ không tạo ra bất kỳ mã thực thi nào từ comments.

## Sử dụng vòng lặp để lặp lại các thao tác

Một khái niệm quan trọng khác để xây dựng các chương trình lớn hơn là **vòng lặp** (loops). Sử dụng vòng lặp để lặp lại các câu lệnh mà bạn muốn thực thi nhiều hơn một lần.

> [!TIP]
> **Tìm hiểu thêm:** Đọc về [câu lệnh lặp](../../language-reference/statements/iteration-statements.md) và [câu lệnh chọn](../../language-reference/statements/selection-statements.md) trong tài liệu tham khảo ngôn ngữ C#.

1. Thêm đoạn mã này sau lời gọi `ExploreIf`:

   ```csharp
   int counter = 0;
   while (counter < 10)
   {
       Console.WriteLine($"Hello World! The counter is {counter}");
       counter++;
   }
   ```

   Câu lệnh `while` kiểm tra một điều kiện và thực thi câu lệnh theo sau `while`. Nó lặp lại việc kiểm tra điều kiện và thực thi các câu lệnh đó cho đến khi điều kiện trở thành sai.

   Có một toán tử mới khác trong ví dụ này. `++` sau variable (biến) `counter` là **increment (toán tử tăng)**. Nó cộng 1 vào giá trị của `counter` và lưu giá trị đó trở lại biến `counter`.

   > [!IMPORTANT]
   > Hãy đảm bảo rằng điều kiện của vòng lặp `while` thay đổi thành sai khi bạn thực thi mã. Nếu không, bạn sẽ tạo ra một **infinite loop (vòng lặp vô hạn)** khiến chương trình không bao giờ kết thúc. Mẫu này không minh hoạ hành vi đó vì bạn sẽ phải buộc chương trình thoát bằng cách sử dụng **CTRL-C** hoặc các cách khác.

   Vòng lặp `while` kiểm tra điều kiện trước khi thực thi đoạn mã theo sau `while`.

1. Vòng lặp `do` ... `while` thực thi mã trước, sau đó mới kiểm tra điều kiện. Vòng lặp *do while* được thể hiện trong đoạn mã sau:

   ```csharp
   int counter = 0;
   do
   {
       Console.WriteLine($"Hello World! The counter is {counter}");
       counter++;
   } while (counter < 10);
   ```

   Vòng lặp `do` này và vòng lặp `while` trước đó tạo ra cùng một kết quả đầu ra.

Hãy chuyển sang một câu lệnh vòng lặp cuối cùng.

## Làm việc với vòng lặp for

Một câu lệnh vòng lặp phổ biến khác mà bạn thấy trong mã C# là vòng lặp `for`.

1. Hãy thử đoạn mã này:

   ```csharp
   for (int counter = 0; counter < 10; counter++)
   {
       Console.WriteLine($"Hello World! The counter is {counter}");
   }
   ```

   Vòng lặp `for` ở trên thực hiện cùng công việc như vòng lặp `while` và vòng lặp `do` bạn đã sử dụng. Câu lệnh `for` có ba phần để kiểm soát cách nó hoạt động:

   - Phần đầu tiên là **for initializer (bộ khởi tạo for)**: `int counter = 0;` khai báo `counter` là biến vòng lặp và đặt giá trị ban đầu của nó là `0`.
   - Phần giữa là **for condition (điều kiện for)**: `counter < 10` khai báo rằng vòng lặp `for` này tiếp tục thực thi miễn là giá trị của `counter` nhỏ hơn 10.
   - Phần cuối là **for iterator (bộ lặp for)**: `counter++` chỉ định cách sửa đổi biến vòng lặp sau khi thực thi khối lệnh theo sau câu lệnh `for`. Ở đây, nó chỉ định rằng `counter` tăng lên 1 mỗi lần khối lệnh được thực thi.

1. Hãy tự mình thử nghiệm với các điều kiện này. Thử từng thay đổi sau:

   - Thay đổi bộ khởi tạo để bắt đầu ở một giá trị khác.
   - Thay đổi điều kiện để dừng ở một giá trị khác.

   Khi bạn đã xong, hãy chuyển sang phần tiếp theo để tự mình viết mã và áp dụng những gì đã học.

   Có một câu lệnh vòng lặp khác không được đề cập trong hướng dẫn này: câu lệnh `foreach`. Câu lệnh `foreach` lặp lại câu lệnh của nó cho mỗi mục trong một chuỗi các mục. Bạn thường sử dụng nó với *collections (bộ sưu tập)*. Nó sẽ được đề cập trong hướng dẫn tiếp theo.

## Tạo vòng lặp lồng nhau

Bạn có thể lồng một vòng lặp `while`, `do`, hoặc `for` bên trong một vòng lặp khác. Bằng cách kết hợp từng mục trong vòng lặp ngoài với từng mục trong vòng lặp trong, bạn tạo ra một ma trận. Hãy xây dựng một tập hợp các cặp chữ-số để biểu diễn các hàng và cột.

1. Thêm vòng lặp `for` sau để tạo ra các hàng:

   ```csharp
   for (int row = 1; row < 11; row++)
   {
       Console.WriteLine($"The row is {row}");
   }
   ```

1. Thêm một vòng lặp khác để tạo ra các cột:

   ```csharp
   for (char column = 'a'; column < 'k'; column++)
   {
       Console.WriteLine($"The column is {column}");
   }
   ```

1. Cuối cùng, lồng vòng lặp cột bên trong vòng lặp hàng để tạo thành các cặp:

   ```csharp
   for (int row = 1; row < 11; row++)
   {
       for (char column = 'a'; column < 'k'; column++)
       {
           Console.WriteLine($"The cell is ({row}, {column})");
       }
   }
   ```

   Vòng lặp ngoài tăng lên một lần cho mỗi lần chạy đầy đủ của vòng lặp trong. Hãy đảo ngược thứ tự lồng giữa hàng và cột, và tự xem sự thay đổi. Khi xong, hãy đặt đoạn mã từ phần này vào một method (phương thức) có tên là `ExploreLoops()`.

## Kết hợp rẽ nhánh và vòng lặp

Bây giờ bạn đã sử dụng câu lệnh `if` và các cấu trúc vòng lặp trong C#, hãy thử xem bạn có thể viết mã C# để tìm tổng của tất cả các số nguyên từ 1 đến 20 mà chia hết cho 3 hay không. Dưới đây là một vài gợi ý:

- Toán tử `%` cho bạn số dư của phép chia.
- Câu lệnh `if` cung cấp điều kiện để kiểm tra xem một số có nằm trong tổng hay không.
- Vòng lặp `for` có thể giúp bạn lặp lại một loạt các bước cho tất cả các số từ 1 đến 20.

Hãy tự mình thử trước. Sau đó kiểm tra lại kết quả của bạn. Gợi ý: bạn sẽ nhận được 63 là đáp án.

Bạn đã ra được kết quả giống như thế này chưa?

<!-- markdownlint-disable MD033 -->
<details>

```csharp
int sum = 0;
for (int number = 1; number < 21; number++)
{
    if (number % 3 == 0)
    {
        sum = sum + number;
    }
}
Console.WriteLine($"The sum is {sum}");
```

</details>
<!-- markdownlint-enable MD033 -->

Bạn đã hoàn thành hướng dẫn "rẽ nhánh và vòng lặp".

## Dọn dẹp tài nguyên

GitHub tự động xoá Codespace của bạn sau 30 ngày không hoạt động. Nếu bạn dự định khám phá thêm các hướng dẫn khác trong loạt bài này, bạn có thể để Codespace của mình hoạt động. Nếu bạn đã sẵn sàng truy cập [trang web .NET](https://dotnet.microsoft.com/download/dotnet) để tải .NET SDK, bạn có thể xoá Codespace của mình. Để xoá Codespace, hãy mở cửa sổ trình duyệt và điều hướng đến [Codespaces của bạn](https://github.com/codespaces). Bạn sẽ thấy danh sách các codespace của mình trong cửa sổ. Chọn ba dấu chấm (`...`) ở mục của codespace học tập và chọn **delete**.

## Bước tiếp theo

Tiếp tục với hướng dẫn tiếp theo trong loạt bài này:

> [!div class="nextstepaction"]
> [Tìm hiểu về bộ sưu tập](list-collection.md)

Hoặc khám phá các chủ đề liên quan trong Kiến thức nền tảng C#:

- [So khớp mẫu](../../fundamentals/functional/pattern-matching.md) — Một giải pháp thay thế mạnh mẽ cho các chuỗi `if`/`else` phức tạp.
- [Phương thức và cấu trúc chương trình](../../fundamentals/program-structure/index.md) — Tìm hiểu cách tổ chức các method (phương thức) bạn đã tạo trong hướng dẫn này.
- [Những gì bạn có thể xây dựng với C#](../what-you-can-build.md) — Xem các loại ứng dụng bạn có thể tạo ra với những gì bạn đang học.
- [Câu lệnh chọn](../../language-reference/statements/selection-statements.md)
- [Câu lệnh lặp](../../language-reference/statements/iteration-statements.md)
