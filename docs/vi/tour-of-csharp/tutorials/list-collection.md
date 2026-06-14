---
title: Bộ sưu tập dữ liệu - Hướng dẫn nhập môn
description: Trong hướng dẫn này, bạn sử dụng GitHub Codespaces để tìm hiểu về bộ sưu tập (collection) trong C#. Bạn sẽ viết mã C# và xem kết quả biên dịch cùng chạy mã trong môi trường Codespaces.
ms.date: 02/09/2026
---
# Hướng dẫn: Học cách quản lý bộ sưu tập dữ liệu bằng List\<T> trong C#

Hướng dẫn nhập môn này cung cấp lời giới thiệu về ngôn ngữ C# và những kiến thức cơ bản về class (lớp) [`List<T>`](https://learn.microsoft.com/dotnet/api/system.collections.generic.list-1).

Hướng dẫn này dạy bạn C#. Bạn sẽ viết mã C# và xem kết quả biên dịch cũng như chạy mã đó. Nó bao gồm một loạt bài học để tạo, sửa đổi và khám phá các bộ sưu tập. Bạn sẽ làm việc chủ yếu với class [`List<T>`](https://learn.microsoft.com/dotnet/api/system.collections.generic.list-1).

> [!TIP]
> **Mới học lập trình?** Hãy làm lần lượt từng phần theo thứ tự. **Đã biết ngôn ngữ khác?** Nếu bạn đã quen với mảng động (dynamic array) hoặc danh sách (list), hãy đọc lướt phần cơ bản và tập trung vào [tìm kiếm và sắp xếp](#tìm-kiếm-và-sap-xếp-danh-sach), [danh sách với kiểu dữ liệu khác](#danh-sach-voi-cac-kieu-du-lieu-khac), và [bài tập thử thách](#bai-tap-thu-thach).

Trong hướng dẫn này, bạn sẽ:

> [!div class="checklist"]
>
> * Khởi chạy GitHub Codespace với môi trường phát triển C#.
> * Tạo các loại danh sách khác nhau.
> * Sửa đổi nội dung danh sách.
> * Tìm kiếm và sắp xếp danh sách.

## Điều kiện tiên quyết

Bạn cần có một trong các lựa chọn sau:

- Một tài khoản GitHub để sử dụng [GitHub Codespaces](https://github.com/codespaces). Nếu chưa có, bạn có thể tạo tài khoản miễn phí tại [GitHub.com](https://github.com).
- Một máy tính đã cài đặt các công cụ sau:
  - [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0).
  - [Visual Studio Code](https://code.visualstudio.com/download).
  - [C# DevKit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit).

## Ví dụ danh sách cơ bản

Để khởi động GitHub Codespace với môi trường hướng dẫn, hãy mở trình duyệt và truy cập kho lưu trữ [tutorial codespace](https://github.com/dotnet/tutorial-codespace). Chọn nút *Code* màu xanh lá, sau đó chọn tab *Codespaces*. Tiếp theo, chọn dấu `+` để tạo Codespace mới sử dụng môi trường này. Nếu bạn đã hoàn thành các hướng dẫn khác trong loạt bài này, bạn có thể mở lại codespace đó thay vì tạo mới.

1. Khi codespace của bạn đã sẵn sàng, hãy tạo một file mới trong thư mục *tutorials* và đặt tên là *lists.cs*.
1. Mở file mới của bạn.
1. Gõ hoặc sao chép đoạn mã sau vào *lists.cs*:

    ```csharp
    List<string> names = ["<name>", "Ana", "Felipe"];
    foreach (var name in names)
    {
        Console.WriteLine($"Hello {name.ToUpper()}!");
    }
    ```

1. Chạy mã bằng cách gõ lệnh sau trong cửa sổ terminal:

    ```dotnetcli
    cd tutorials
    dotnet lists.cs
    ```

Bạn đã tạo một danh sách các chuỗi (string), thêm ba cái tên vào danh sách đó, và in các tên đó ra dưới dạng chữ in hoa. Bạn đang sử dụng những khái niệm đã học trong các hướng dẫn trước để duyệt qua danh sách.

Đoạn mã hiển thị tên sử dụng tính năng [nội suy chuỗi](../../language-reference/tokens/interpolated.md). Khi bạn đặt trước một `string` bằng ký tự `$`, bạn có thể nhúng mã C# vào trong khai báo chuỗi. Chuỗi thực tế sẽ thay thế đoạn mã C# đó bằng giá trị mà nó tạo ra. Trong ví dụ này, nó thay thế `{name.ToUpper()}` bằng mỗi tên đã được chuyển thành chữ in hoa nhờ gọi method [`ToUpper()`](https://learn.microsoft.com/dotnet/api/system.string.toupper).

Hãy tiếp tục khám phá nhé.

## Sửa đổi nội dung danh sách

Bộ sưu tập bạn vừa tạo sử dụng kiểu [`List<T>`](https://learn.microsoft.com/dotnet/api/system.collections.generic.list-1). Kiểu này lưu trữ các chuỗi phần tử (element). Bạn chỉ định kiểu dữ liệu của các phần tử nằm giữa cặp dấu ngoặc nhọn.

> [!TIP]
> **Tìm hiểu thêm:** Khám phá [bộ sưu tập](../../../standard/collections/index.md) và [generics](../../fundamentals/types/generics.md) trong tài liệu C#.

Một khía cạnh quan trọng của kiểu [`List<T>`](https://learn.microsoft.com/dotnet/api/system.collections.generic.list-1) là nó có thể lớn lên hoặc co lại, vì vậy bạn có thể thêm hoặc xoá phần tử. Bạn có thể thấy kết quả bằng cách sửa đổi nội dung sau khi đã hiển thị nội dung của nó.

1. Thêm đoạn mã sau vào sau đoạn mã bạn đã viết (vòng lặp in nội dung):

    ```csharp
    Console.WriteLine();
    names.Add("Maria");
    names.Add("Bill");
    names.Remove("Ana");
    foreach (var name in names)
    {
        Console.WriteLine($"Hello {name.ToUpper()}!");
    }
    ```

    Bạn vừa thêm hai tên nữa vào cuối danh sách. Bạn cũng đã xoá một tên. Kết quả từ khối mã này hiển thị nội dung ban đầu, sau đó in một dòng trống và nội dung mới.

1. Kiểu [`List<T>`](https://learn.microsoft.com/dotnet/api/system.collections.generic.list-1) cũng cho phép bạn tham chiếu tới từng phần tử riêng lẻ bằng **chỉ mục (index)**. Bạn truy cập các phần tử bằng cách sử dụng cặp dấu `[` và `]`. Thêm đoạn mã sau vào những gì bạn đã viết và thử nghiệm:

    ```csharp
    Console.WriteLine($"My name is {names[0]}.");
    Console.WriteLine($"I've added {names[2]} and {names[3]} to the list.");
    ```

    Bạn không thể truy cập vượt quá cuối danh sách. Bạn có thể kiểm tra độ dài của danh sách bằng thuộc tính (property) [`Count`](https://learn.microsoft.com/dotnet/api/system.collections.generic.list-1.count).

1. Thêm đoạn mã sau:

    ```csharp
    Console.WriteLine($"The list has {names.Count} people in it");
    ```

    Gõ lại `dotnet lists.cs` trong cửa sổ terminal để xem kết quả. Trong C#, chỉ mục bắt đầu từ 0, vì vậy chỉ mục hợp lệ lớn nhất là số lượng phần tử trong danh sách trừ đi 1.

Để biết thêm thông tin về chỉ mục, hãy xem bài viết [Khám phá chỉ mục và phạm vi](../../tutorials/ranges-indexes.md).

## Tìm kiếm và sắp xếp danh sách

Các mẫu ví dụ sử dụng danh sách tương đối nhỏ, nhưng ứng dụng của bạn thường sẽ tạo ra danh sách với nhiều phần tử hơn, đôi khi lên tới hàng nghìn. Để tìm phần tử trong những bộ sưu tập lớn hơn này, bạn cần tìm kiếm danh sách. Method [`IndexOf`](https://learn.microsoft.com/dotnet/api/system.collections.generic.list-1.indexof) tìm kiếm một phần tử và trả về chỉ mục của phần tử đó. Nếu phần tử không có trong danh sách, `IndexOf` trả về `-1`.

1. Hãy thử nghiệm để xem nó hoạt động thế nào. Thêm đoạn mã sau vào những gì bạn đã viết:

    ```csharp
    var index = names.IndexOf("Felipe");
    if (index == -1)
    {
        Console.WriteLine($"When an item is not found, IndexOf returns {index}");
    }
    else
    {
        Console.WriteLine($"The name {names[index]} is at index {index}");
    }

    index = names.IndexOf("Not Found");
    if (index == -1)
    {
        Console.WriteLine($"When an item is not found, IndexOf returns {index}");
    }
    else
    {
        Console.WriteLine($"The name {names[index]} is at index {index}");
    }
    ```

    Bạn có thể không biết liệu một phần tử có nằm trong danh sách hay không, vì vậy hãy luôn kiểm tra chỉ mục trả về từ [`IndexOf`](https://learn.microsoft.com/dotnet/api/system.collections.generic.list-1.indexof). Nếu nó là `-1`, phần tử đó không được tìm thấy.

1. Bạn cũng có thể sắp xếp các phần tử trong danh sách của mình. Method [`Sort`](https://learn.microsoft.com/dotnet/api/system.collections.generic.list-1.sort) sắp xếp tất cả các phần tử trong danh sách theo thứ tự thông thường (theo bảng chữ cái đối với chuỗi). Thêm đoạn mã này và chạy lại:

    ```csharp
    names.Sort();
    foreach (var name in names)
    {
        Console.WriteLine($"Hello {name.ToUpper()}!");
    }
    ```

## Danh sách với các kiểu dữ liệu khác

Cho đến nay, bạn đã sử dụng kiểu `string` trong danh sách. Hãy tạo một [`List<T>`](https://learn.microsoft.com/dotnet/api/system.collections.generic.list-1) với một kiểu dữ liệu khác. Hãy xây dựng một tập hợp các số.

1. Thêm đoạn mã sau vào cuối file nguồn của bạn:

    ```csharp
    List<int> fibonacciNumbers = [1, 1];
    ```

    Đoạn mã đó tạo một danh sách các số nguyên (integer) và đặt hai số nguyên đầu tiên thành giá trị 1. *Dãy Fibonacci (Fibonacci Sequence)*, một dãy số, bắt đầu với hai số 1. Mỗi số Fibonacci tiếp theo được tìm bằng cách lấy tổng của hai số trước đó.

1. Thêm đoạn mã này:

    ```csharp
    var previous = fibonacciNumbers[fibonacciNumbers.Count - 1];
    var previous2 = fibonacciNumbers[fibonacciNumbers.Count - 2];

    fibonacciNumbers.Add(previous + previous2);

    foreach (var item in fibonacciNumbers)
    {
        Console.WriteLine(item);
    }
    ```

1. Gõ `dotnet lists.cs` trong cửa sổ terminal để xem kết quả.

## Bài tập thử thách

Hãy xem liệu bạn có thể kết hợp một số khái niệm từ bài học này và các bài học trước không. Mở rộng những gì bạn đã xây dựng với các số Fibonacci. Hãy thử viết mã để tạo ra 20 số đầu tiên trong dãy. (Gợi ý: số Fibonacci thứ 20 là 6765.)

Bạn đã tìm ra đoạn mã giống thế này chưa?

<!-- markdownlint-disable MD033 -->
<details>

```csharp
List<int> fibonacciNumbers = [1, 1];

while (fibonacciNumbers.Count < 20)
{
    var previous = fibonacciNumbers[fibonacciNumbers.Count - 1];
    var previous2 = fibonacciNumbers[fibonacciNumbers.Count - 2];

    fibonacciNumbers.Add(previous + previous2);
}
foreach (var item in fibonacciNumbers)
{
    Console.WriteLine(item);
}
```

Với mỗi vòng lặp, bạn lấy hai số nguyên cuối cùng trong danh sách, cộng chúng lại, và thêm giá trị đó vào danh sách. Vòng lặp tiếp tục cho đến khi bạn thêm đủ 20 phần tử vào danh sách.
</details>
<!-- markdownlint-enable MD033 -->

Bạn đã hoàn thành hướng dẫn về danh sách.

## Dọn dẹp tài nguyên

GitHub tự động xoá Codespace của bạn sau 30 ngày không hoạt động. Nếu bạn dự định khám phá thêm các hướng dẫn khác trong loạt bài này, bạn có thể để Codespace của mình hoạt động. Nếu bạn đã sẵn sàng truy cập [trang .NET](https://dotnet.microsoft.com/download/dotnet) để tải .NET SDK, bạn có thể xoá Codespace của mình. Để xoá Codespace, hãy mở trình duyệt và điều hướng đến [Codespaces của bạn](https://github.com/codespaces). Bạn sẽ thấy danh sách các codespace của mình trong cửa sổ. Chọn ba dấu chấm (`...`) trong mục của codespace học tập và chọn **delete**.

## Các bước tiếp theo

Tiếp tục với hướng dẫn tiếp theo trong loạt bài này:

> [!div class="nextstepaction"]
> [So khớp mẫu](pattern-matching.md)

Hoặc khám phá các chủ đề liên quan trong Kiến thức cơ bản về C#:

- [Generics trong C#](../../fundamentals/types/generics.md) — Tìm hiểu cú pháp `<T>` bạn đã sử dụng xuyên suốt hướng dẫn này.
- [Tổng quan về LINQ](../../linq/index.md) — Truy vấn và biến đổi bộ sưu tập bằng Language Integrated Query.
- [Những gì bạn có thể xây dựng với C#](../what-you-can-build.md) — Xem các loại ứng dụng bạn có thể tạo ra với những gì đang học.
- [Chọn kiểu bộ sưu tập](../../../standard/collections/selecting-a-collection-class.md)
- [Các kiểu bộ sưu tập thường dùng](../../../standard/collections/commonly-used-collection-types.md)
- [Khi nào nên dùng generic collection](../../../standard/collections/when-to-use-generic-collections.md)
