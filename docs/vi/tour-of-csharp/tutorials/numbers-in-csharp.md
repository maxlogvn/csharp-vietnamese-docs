---
title: Làm việc với số - Bài hướng dẫn mở đầu
description: Bài hướng dẫn này dạy bạn về các kiểu số trong C#. Nó bao gồm một chuỗi các bài học khám phá về số và các phép toán trong C#.
ms.date: 02/06/2026
---
# Hướng dẫn: Cách sử dụng số nguyên và số thực trong C\#

Bài hướng dẫn này dạy bạn về các kiểu số (numeric types) trong C#. Bạn sẽ viết một lượng nhỏ code, sau đó biên dịch và chạy code đó. Nó bao gồm một chuỗi các bài học khám phá về số và các phép toán trong C#. Những bài học này dạy bạn những kiến thức nền tảng của ngôn ngữ C#.

> [!TIP]
> **Mới học lập trình?** Hãy làm theo từng phần theo thứ tự. **Đã biết ngôn ngữ khác?** Bạn có thể đã biết sự khác biệt giữa số nguyên và số thực - hãy lướt qua phần cơ bản và tập trung vào phần [độ chính xác và giới hạn](#explore-integer-precision-and-limits) và [kiểu decimal](#work-with-decimal-types).

Trong bài hướng dẫn này, bạn sẽ:

> [!div class="checklist"]
>
> * Khởi chạy GitHub Codespace với môi trường phát triển C#.
> * Khám phá toán học với số nguyên.
> * Học về thứ tự ưu tiên phép toán.
> * Học về giới hạn và độ chính xác của số nguyên.
> * Học về kiểu số thực (floating point).
> * Học về kiểu decimal.

## Điều kiện tiên quyết

Bạn cần có một trong những lựa chọn sau:

- Tài khoản GitHub để sử dụng [GitHub Codespaces](https://github.com/codespaces). Nếu bạn chưa có, bạn có thể tạo một tài khoản miễn phí tại [GitHub.com](https://github.com).
- Một máy tính đã cài đặt các công cụ sau:
  - [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0).
  - [Visual Studio Code](https://code.visualstudio.com/download).
  - [C# DevKit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit).

## Khám phá toán học với số nguyên

Để bắt đầu GitHub Codespace với môi trường hướng dẫn, hãy mở trình duyệt tới kho lưu trữ [tutorial codespace](https://github.com/dotnet/tutorial-codespace). Chọn nút *Code* màu xanh, và tab *Codespaces*. Sau đó chọn dấu `+` để tạo Codespace mới sử dụng môi trường này. Nếu bạn đã hoàn thành bài hướng dẫn [hello world](./hello-world.md), bạn có thể mở codespace đó thay vì tạo mới.

1. Khi codespace của bạn đã tải xong, tạo một file mới trong thư mục *tutorials* có tên là *numbers.cs*.
1. Mở file mới của bạn.
1. Gõ hoặc copy đoạn code sau vào *numbers.cs*:

   ```csharp
   int a = 18;
   int b = 6;
   int c = a + b;
   Console.WriteLine(c);
   ```

1. Chạy code này bằng cách gõ các lệnh sau trong terminal tích hợp:

   ```dotnetcli
   cd ./tutorials
   dotnet numbers.cs
   ```

   Bạn vừa thấy một trong những phép toán cơ bản với số nguyên. Kiểu `int` đại diện cho một **integer (số nguyên)**, một số nguyên dương, âm hoặc bằng không. Bạn sử dụng ký hiệu `+` cho phép cộng. Các phép toán thông dụng khác cho số nguyên bao gồm:

   - `-` cho phép trừ
   - `*` cho phép nhân
   - `/` cho phép chia

1. Hãy bắt đầu khám phá những phép toán khác nhau đó. Thêm những dòng sau vào sau dòng ghi giá trị của `c`:

   ```csharp
   // subtraction
   c = a - b;
   Console.WriteLine(c);

   // multiplication
   c = a * b;
   Console.WriteLine(c);

   // division
   c = a / b;
   Console.WriteLine(c);
   ```

1. Chạy code này bằng cách gõ `dotnet numbers.cs` trong cửa sổ terminal.

Bạn cũng có thể thử nghiệm bằng cách viết nhiều phép toán trên cùng một dòng, nếu bạn muốn. Thử `c = a + b - 12 * 17;` chẳng hạn. Việc trộn biến và số hằng là hoàn toàn được phép.

> [!TIP]
> Khi bạn khám phá C# (hoặc bất kỳ ngôn ngữ lập trình nào), bạn có thể mắc lỗi khi viết code. **Trình biên dịch (compiler)** sẽ tìm ra những lỗi đó và thông báo cho bạn. Khi kết quả chứa thông báo lỗi, hãy xem kỹ code mẫu và code trong cửa sổ của bạn để biết cần sửa gì. Bạn cũng có thể nhờ Copilot tìm sự khác biệt hoặc phát hiện lỗi. Bài tập đó giúp bạn học cấu trúc của code C#.

Bạn đã hoàn thành bước đầu tiên. Trước khi bắt đầu phần tiếp theo, hãy di chuyển code hiện tại vào một **method (phương thức)** riêng. Một method là một loạt các câu lệnh được nhóm lại và đặt tên. Bạn gọi một method bằng cách viết tên method theo sau bởi `()`. Sắp xếp code của bạn vào các method giúp bạn dễ dàng bắt đầu với một ví dụ mới.

> [!TIP]
> **Tìm hiểu thêm:** Đọc về [phương thức và cấu trúc chương trình](../../fundamentals/program-structure/index.md) trong C# Fundamentals.

Khi hoàn thành, code của bạn sẽ trông như sau:

```csharp
WorkWithIntegers();

void WorkWithIntegers()
{
    int a = 18;
    int b = 6;
    int c = a + b;
    Console.WriteLine(c);


    // subtraction
    c = a - b;
    Console.WriteLine(c);

    // multiplication
    c = a * b;
    Console.WriteLine(c);

    // division
    c = a / b;
    Console.WriteLine(c);
}
```

## Khám phá thứ tự ưu tiên phép toán

1. Hãy comment dòng gọi `WorkWithIntegers()`. Thay đổi này làm cho đầu ra bớt hỗn loạn hơn khi bạn làm việc trong phần này:

   ```csharp
   //WorkWithIntegers();
   ```

   `//` bắt đầu một **comment** trong C#. Comments là bất kỳ văn bản nào bạn muốn giữ trong mã nguồn nhưng không thực thi như code. Trình biên dịch không tạo ra bất kỳ code thực thi nào từ comments. Bởi vì `WorkWithIntegers()` là một method, bạn chỉ cần comment một dòng.

1. Ngôn ngữ C# định nghĩa thứ tự ưu tiên của các phép toán khác nhau với các quy tắc tương tự như bạn đã học trong toán học. Phép nhân và chia có ưu tiên cao hơn phép cộng và trừ. Khám phá thứ tự ưu tiên đó bằng cách thêm đoạn code sau sau khi gọi `WorkWithIntegers()`, và gõ `dotnet numbers.cs` trong cửa sổ terminal:

   ```csharp
   int a = 5;
   int b = 4;
   int c = 2;
   int d = a + b * c;
   Console.WriteLine(d);
   ```

   Đầu ra cho thấy phép nhân được thực hiện trước phép cộng.

1. Bạn có thể buộc một thứ tự ưu tiên khác bằng cách thêm dấu ngoặc đơn vào phép toán hoặc các phép toán bạn muốn thực hiện trước. Thêm các dòng sau và chạy lại ứng dụng:

   ```csharp
   d = (a + b) * c;
   Console.WriteLine(d);
   ```

1. Khám phá thêm bằng cách kết hợp nhiều phép toán khác nhau. Thêm một vài dòng như sau. Thử chạy `dotnet numbers` một lần nữa trong cửa sổ terminal.

   ```csharp
   d = (a + b) - 6 * c + (12 * 4) / 3 + 12;
   Console.WriteLine(d);
   ```

   Bạn có thể nhận thấy một hành vi thú vị của số nguyên. Phép chia số nguyên luôn cho kết quả là số nguyên, ngay cả khi bạn mong đợi kết quả bao gồm phần thập phân.

1. Nếu bạn không thấy hành vi này, hãy thử code sau:

   ```csharp
   int e = 7;
   int f = 4;
   int g = 3;
   int h = (e + f) / g;
   Console.WriteLine(h);
   ```

1. Gõ `dotnet numbers.cs` một lần nữa trong cửa sổ terminal để xem kết quả.

Trước khi chuyển sang phần tiếp theo, hãy lấy tất cả code bạn đã viết trong phần này và đặt vào một method mới. Gọi method mới đó là `OrderPrecedence`. Code của bạn sẽ trông như sau:

```csharp
// WorkWithIntegers();
OrderPrecedence();

void WorkWithIntegers()
{
    int a = 18;
    int b = 6;
    int c = a + b;
    Console.WriteLine(c);


    // subtraction
    c = a - b;
    Console.WriteLine(c);

    // multiplication
    c = a * b;
    Console.WriteLine(c);

    // division
    c = a / b;
    Console.WriteLine(c);
}

void OrderPrecedence()
{
    int a = 5;
    int b = 4;
    int c = 2;
    int d = a + b * c;
    Console.WriteLine(d);

    d = (a + b) * c;
    Console.WriteLine(d);

    d = (a + b) - 6 * c + (12 * 4) / 3 + 12;
    Console.WriteLine(d);

    int e = 7;
    int f = 4;
    int g = 3;
    int h = (e + f) / g;
    Console.WriteLine(h);
}
```

## Khám phá độ chính xác và giới hạn của số nguyên

Ví dụ trước cho thấy phép chia số nguyên cắt bỏ phần thập phân của kết quả. Bạn có thể lấy **phần dư (remainder)** bằng cách sử dụng toán tử **remainder**, ký hiệu `%`.

1. Thử code sau sau khi gọi method `OrderPrecedence()`:

   ```csharp
   int a = 7;
   int b = 4;
   int c = 3;
   int d = (a + b) / c;
   int e = (a + b) % c;
   Console.WriteLine($"quotient: {d}");
   Console.WriteLine($"remainder: {e}");
   ```

1. Kiểu số nguyên (integer) trong C# khác với số nguyên toán học ở một điểm nữa: kiểu `int` có giới hạn tối thiểu và tối đa. Thử code sau để xem các giới hạn đó:

   ```csharp
   int max = int.MaxValue;
   int min = int.MinValue;
   Console.WriteLine($"The range of integers is {min} to {max}");
   ```

1. Nếu một phép tính tạo ra giá trị vượt quá các giới hạn đó, bạn sẽ gặp tình trạng **underflow** hoặc **overflow**. Kết quả dường như bị "quay vòng" từ giới hạn này sang giới hạn kia. Để xem ví dụ, thêm hai dòng này vào code của bạn:

   ```csharp
   int what = max + 3;
   Console.WriteLine($"An example of overflow: {what}");
   ```

Hãy ý rằng kết quả rất gần với số nguyên tối thiểu (âm). Nó bằng `min + 2`. Phép cộng đã **overflow** (tràn) khỏi các giá trị cho phép của số nguyên. Kết quả là một số âm lớn bởi vì overflow "quay vòng" từ giá trị số nguyên lớn nhất có thể xuống giá trị nhỏ nhất.

Nếu kiểu `int` không đáp ứng nhu cầu của bạn, hãy sử dụng các kiểu số khác với giới hạn và độ chính xác khác nhau. Chúng ta sẽ khám phá những kiểu số đó tiếp theo.

## Làm việc với kiểu double

Kiểu số `double` đại diện cho một số thực dấu phẩy động độ chính xác kép (double-precision floating point). Những thuật ngữ này có thể mới với bạn. Một **floating point (số thực)** rất hữu ích cho việc biểu diễn các số không nguyên có thể rất lớn hoặc rất nhỏ. **Double-precision (độ chính xác kép)** là một thuật ngữ tương đối mô tả số lượng chữ số nhị phân được sử dụng để lưu trữ giá trị. Số **double-precision** có gấp đôi số chữ số nhị phân so với **single-precision (độ chính xác đơn)**. Trên các máy tính hiện đại, người ta thường dùng double-precision hơn single-precision. Số **single-precision** được khai báo bằng từ khoá `float`. Hãy cùng khám phá.

1. Thêm đoạn code sau và xem kết quả:

   ```csharp
   double a = 5;
   double b = 4;
   double c = 2;
   double d = (a + b) / c;
   Console.WriteLine(d);
   ```

   Hãy ý rằng kết quả bao gồm phần thập phân của thương số.

1. Thử một biểu thức phức tạp hơn một chút với double. Bạn có thể sử dụng các giá trị sau, hoặc thay bằng số khác:

   ```csharp
   double a = 19;
   double b = 23;
   double c = 8;
   double d = (a + b) / c;
   Console.WriteLine(d);
   ```

1. Phạm vi của giá trị double lớn hơn nhiều so với số nguyên. Thử code sau mà bạn thêm vào những gì đã viết:

   ```csharp
   double max = double.MaxValue;
   double min = double.MinValue;
   Console.WriteLine($"The range of double is {min} to {max}");
   ```

   Những giá trị này được in theo ký hiệu khoa học (scientific notation). Số bên trái chữ `E` là phần định trị (significand). Số bên phải là số mũ (exponent), dưới dạng luỹ thừa của 10.

1. Giống như số thập phân trong toán học, double trong C# có thể có lỗi làm tròn. Thử code này:

   ```csharp
   double third = 1.0 / 3.0;
   Console.WriteLine(third);
   ```

   Bạn biết rằng `0.3` bằng `3/10` và không hoàn toàn bằng `1/3`. Tương tự, `0.33` bằng `33/100`. Giá trị đó gần với `1/3` hơn, nhưng vẫn không chính xác. Không quan trọng bạn thêm bao nhiêu chữ số thập phân, lỗi làm tròn vẫn tồn tại.

***Thách thức***

Hãy thử các phép tính khác với số lớn, số nhỏ, phép nhân và phép chia bằng kiểu `double`. Thử các phép tính phức tạp hơn. Sau khi bạn đã dành thời gian với thách thức, hãy lấy code bạn đã viết và đặt vào một method mới. Đặt tên method mới đó là `WorkWithDoubles`.

## Làm việc với kiểu decimal

Bạn đã thấy các kiểu số cơ bản trong C#: số nguyên (integer) và double. Còn một kiểu khác cần học: kiểu `decimal`. Kiểu `decimal` có phạm vi nhỏ hơn nhưng độ chính xác cao hơn `double`.

1. Hãy cùng xem xét:

   ```csharp
   decimal min = decimal.MinValue;
   decimal max = decimal.MaxValue;
   Console.WriteLine($"The range of the decimal type is {min} to {max}");
   ```

   Hãy ý rằng phạm vi nhỏ hơn kiểu `double`.

1. Bạn có thể thấy độ chính xác cao hơn của kiểu decimal bằng cách thử code sau:

   ```csharp
   double a = 1.0;
   double b = 3.0;
   Console.WriteLine(a / b);

   decimal c = 1.0M;
   decimal d = 3.0M;
   Console.WriteLine(c / d);
   ```

   Hãy ý rằng phép toán với kiểu decimal có nhiều chữ số bên phải dấu thập phân hơn.

   Hậu tố `M` trên các số cho biết một hằng số nên sử dụng kiểu `decimal`. Nếu không, trình biên dịch sẽ mặc định là kiểu `double`.

> [!NOTE]
> Chữ `M` là chữ có hình dạng dễ phân biệt nhất giữa hai từ khoá `double` và `decimal`.

***Thách thức***

Bây giờ bạn đã biết các kiểu số khác nhau, hãy viết code tính diện tích hình tròn có bán kính 2.50 cm. Hãy nhớ rằng diện tích hình tròn bằng bán kính bình phương nhân với PI. Một gợi ý: runtime có sẵn hằng số PI, [`Math.PI`](https://learn.microsoft.com/dotnet/api/system.math.pi) mà bạn có thể sử dụng cho giá trị đó. [`Math.PI`](https://learn.microsoft.com/dotnet/api/system.math.pi), giống như tất cả các hằng số được khai báo trong namespace `System.Math`, là một giá trị `double`. Vì lý do đó, bạn nên sử dụng `double` thay vì `decimal` cho thách thức này.

Bạn sẽ nhận được kết quả trong khoảng 19 đến 20.

<!-- markdownlint-disable MD033 -->
<details>

```csharp
double radius = 2.50;
double area = Math.PI * radius * radius;
Console.WriteLine(area);
```
</details>
<!-- markdownlint-enable MD033 -->

Hãy thử một vài công thức khác nếu bạn muốn.

## Dọn dẹp tài nguyên

GitHub tự động xoá Codespace của bạn sau 30 ngày không hoạt động. Nếu bạn dự định khám phá thêm nhiều bài hướng dẫn trong loạt bài này, bạn có thể để Codespace của bạn được duy trì. Nếu bạn sẵn sàng truy cập [trang web .NET](https://dotnet.microsoft.com/download/dotnet) để tải .NET SDK, bạn có thể xoá Codespace của mình. Để xoá Codespace, hãy mở trình duyệt và đi đến [Codespaces của bạn](https://github.com/codespaces). Bạn sẽ thấy một danh sách các codespace trong cửa sổ. Chọn ba dấu chấm (`...`) trong mục của codespace learn tutorial và chọn **delete**.

## Bước tiếp theo

Tiếp tục với bài hướng dẫn tiếp theo trong loạt bài này:

> [!div class="nextstepaction"]
> [Tuple và kiểu dữ liệu](tuples-and-types.md)

Hoặc khám phá các chủ đề liên quan trong C# Fundamentals:

- [Hệ thống kiểu dữ liệu C#](../../fundamentals/types/index.md) -- Tìm hiểu sâu hơn về các kiểu bạn đã sử dụng trong bài hướng dẫn này.
- [Phương thức và cấu trúc chương trình](../../fundamentals/program-structure/index.md) -- Tìm hiểu thêm về các method bạn đã tạo để tổ chức code.
- [Những gì bạn có thể xây dựng với C#](../what-you-can-build.md) -- Xem các loại ứng dụng bạn có thể tạo với những gì bạn đang học.
- [Các kiểu số nguyên](../../language-reference/builtin-types/integral-numeric-types.md)
- [Các kiểu số thực dấu phẩy động](../../language-reference/builtin-types/floating-point-numeric-types.md)
- [Chuyển đổi số có sẵn](../../language-reference/builtin-types/numeric-conversions.md)
