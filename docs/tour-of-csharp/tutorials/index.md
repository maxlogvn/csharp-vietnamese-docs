---
title: Hướng dẫn tương tác
description: Học C# bằng GitHub Codespaces và bắt đầu với môi trường phát triển của riêng bạn.
ms.date: 02/09/2026
---

# Giới thiệu về C\#

Chào mừng bạn đến với loạt bài hướng dẫn giới thiệu về C#. Những bài học này bắt đầu với **mã nguồn tương tác** (interactive code) -- loại mã nguồn mà bạn có thể chạy thử và xem kết quả ngay lập tức -- thông qua **GitHub Codespaces** (một môi trường lập trình trực tuyến chạy trên trình duyệt, do GitHub cung cấp, giúp bạn không cần phải cài đặt gì trên máy tính cá nhân). Bạn có thể học những kiến thức cơ bản về C# từ [chuỗi video C# for Beginners](https://aka.ms/dotnet/beginnervideos/youtube/csharp) trước khi bắt đầu các bài học tương tác này.

> [!TIP]
> **Mới bắt đầu học lập trình?** Hãy bắt đầu với bài học số 1 ([Hello world - Xin chào thế giới](hello-world.md)) và làm lần lượt từng bài theo thứ tự. Các bài học được sắp xếp từ dễ đến khó, mỗi bài đều dựa trên kiến thức của bài trước.
> 
> **Đã biết một ngôn ngữ lập trình khác?** Bạn có thể lướt qua bài 1-2 và bắt đầu từ [Tuples and types](tuples-and-types.md) để tìm hiểu các khái niệm mới có thể chưa xuất hiện trong ngôn ngữ bạn đã biết.

Tất cả các bài hướng dẫn đều sử dụng **ứng dụng dạng tệp** (file-based apps) -- nghĩa là bạn sẽ viết mã nguồn trong các tệp `.cs` và chạy chúng trực tiếp từ dòng lệnh, thay vì dùng một giao diện đồ họa phức tạp. Bạn có thể dùng [GitHub Codespace](https://github.com/dotnet/tutorial-codespace) của chúng tôi hoặc cài đặt [.NET SDK](../../../core/install/index.yml) (**SDK** - Bộ công cụ phát triển phần mềm, viết tắt của Software Development Kit) là đã sẵn sàng để bắt đầu.

<!--markdownlint-disable-next-line MD034 -->
> [!VIDEO https://www.youtube.com/embed/9THmGiSPjBQ?si=3kUKFtOMLpEzeq7J]

Những bài học đầu tiên giải thích các khái niệm C# bằng những đoạn mã ngắn. Bạn sẽ học những kiến thức cơ bản về **cú pháp C#** (C# syntax) -- bộ quy tắc về cách viết mã nguồn C# đúng -- và cách làm việc với các **kiểu dữ liệu** (data types), chẳng hạn như:
- **Chuỗi** (`string`): dùng để lưu trữ văn bản, ví dụ `"Xin chào"`.
- **Số** (`number`): dùng để lưu trữ các giá trị số, ví dụ `42` hoặc `3.14`.
- **Boolean** (`bool`): dùng để lưu trữ giá trị đúng/sai, ví dụ `true` hoặc `false`.

Tất cả đều mang tính tương tác và bạn sẽ có thể viết cũng như chạy mã nguồn chỉ trong vài phút. Những bài học đầu tiên này không yêu cầu bạn phải có kiến thức lập trình hay biết ngôn ngữ C# từ trước. Mỗi bài học đều được xây dựng dựa trên bài học trước đó, vì vậy bạn nên làm theo đúng thứ tự. Tuy nhiên, nếu bạn đã có kinh nghiệm lập trình, bạn có thể bỏ qua hoặc lướt nhanh các bài đầu và bắt đầu với bất kỳ khái niệm mới nào.

Để sử dụng GitHub Codespaces, bạn cần tạo một tài khoản [GitHub](https://github.com) miễn phí.

## Hello world (Xin chào thế giới)

Trong bài hướng dẫn [Hello world](hello-world.md) -- chương trình "Hello world" là chương trình đơn giản nhất trong lập trình, chỉ in ra dòng chữ "Hello, World!" để kiểm tra xem mọi thứ đã hoạt động chưa -- bạn sẽ tạo chương trình C# cơ bản nhất. Bạn sẽ khám phá **kiểu `string`** (kiểu chuỗi, dùng để lưu trữ và thao tác với văn bản) và cách làm việc với văn bản.

## Numbers in C# (Số trong C#)

Trong bài hướng dẫn [Numbers in C#](numbers-in-csharp.md), bạn sẽ học cách máy tính lưu trữ số và cách thực hiện các phép tính với những **kiểu số** (numeric types) khác nhau, ví dụ:
- **Số nguyên** (`int`, `long`): số không có phần thập phân, như `5` hoặc `-100`.
- **Số thực** (`float`, `double`, `decimal`): số có phần thập phân, như `3.14` hoặc `2.71828`.

Bạn sẽ học những kiến thức cơ bản về **làm tròn số** (rounding) và cách thực hiện các phép toán bằng C#.

## Tuples and types (Tuple và kiểu dữ liệu)

Trong bài hướng dẫn [Tuples and types](tuples-and-types.md), bạn sẽ học cách tạo ra các **kiểu dữ liệu** (types) trong C#. Các kiểu dữ liệu là "khuôn mẫu" để tạo ra các đối tượng dữ liệu trong chương trình. Bạn có thể tạo các kiểu:
- **Tuple** (bộ): một nhóm các giá trị tạm thời, không cần định nghĩa kiểu trước. Ví dụ: `("Hoa", 20)` lưu tên và tuổi.
- **Record** (bản ghi): một kiểu dữ liệu bất biến (không thể thay đổi sau khi tạo), thường dùng để lưu trữ dữ liệu thuần túy.
- **Struct** (cấu trúc): một kiểu dữ liệu nhỏ gọn, được lưu trữ trực tiếp trong bộ nhớ (kiểu giá trị - value type).
- **Class** (lớp): một kiểu dữ liệu tham chiếu (reference type), là nền tảng của lập trình hướng đối tượng trong C#.

**Value type** (kiểu giá trị) là kiểu dữ liệu mà giá trị của nó được lưu trực tiếp trong bộ nhớ. **Reference type** (kiểu tham chiếu) là kiểu dữ liệu mà biến chỉ lưu **địa chỉ** (tham chiếu) đến vùng nhớ chứa dữ liệu thực sự. Khả năng của mỗi kiểu dữ liệu này phản ánh những mục đích sử dụng khác nhau của chúng.

## Branches and loops (Rẽ nhánh và vòng lặp)

Bài hướng dẫn [Branches and loops](branches-and-loops.md) dạy bạn những kiến thức cơ bản về **luồng điều khiển** (control flow) -- cách chương trình quyết định thực thi dòng lệnh nào dựa trên các điều kiện khác nhau. Cụ thể:
- **Branch** (rẽ nhánh): chương trình kiểm tra một điều kiện (ví dụ: `nếu điểm số >= 5 thì "Đỗ", nếu không thì "Trượt"`) và chọn một đường đi thích hợp. Các từ khóa thường dùng: `if`, `else`, `switch`.
- **Loop** (vòng lặp): chương trình lặp lại một khối lệnh nhiều lần cho đến khi điều kiện dừng được thỏa mãn. Các từ khóa thường dùng: `for`, `while`, `foreach`.

Bạn sẽ học cách lựa chọn các đường dẫn thực thi mã nguồn khác nhau dựa trên giá trị được lưu trong các **biến** (variables) -- các "hộp chứa" dùng để lưu trữ dữ liệu trong bộ nhớ. Đây chính là nền tảng giúp chương trình đưa ra quyết định và lựa chọn các hành động khác nhau.

## List collection (Tập hợp danh sách)

Bài học [List collection](list-collection.md) sẽ giới thiệu cho bạn về **List** (danh sách) -- một **collection** (tập hợp, bộ sưu tập) dùng để lưu trữ một chuỗi (dãy) các phần tử có cùng kiểu dữ liệu. Ví dụ: `List<string>` lưu danh sách các chuỗi văn bản, `List<int>` lưu danh sách các số nguyên. Bạn sẽ học cách:
- **Thêm** (add) phần tử vào danh sách.
- **Xóa** (remove) phần tử khỏi danh sách.
- **Tìm kiếm** (search) phần tử trong danh sách.
- **Sắp xếp** (sort) các phần tử trong danh sách.

Bạn cũng sẽ khám phá các loại danh sách khác nhau, như `List<T>` (danh sách có thứ tự có thể thay đổi kích thước) và `IEnumerable<T>` (một khái niệm trừu tượng hơn, đại diện cho bất kỳ chuỗi dữ liệu nào có thể duyệt qua được).

## Pattern matching (So khớp mẫu)

Bài học [Pattern matching](pattern-matching.md) cung cấp phần giới thiệu về **so khớp mẫu** (pattern matching) -- một kỹ thuật mạnh mẽ trong C#. Pattern matching cho phép bạn so sánh một **biểu thức** (expression) với một **mẫu** (pattern). Kết quả so khớp sẽ quyết định logic chương trình nào được thực thi tiếp theo. Các mẫu có thể so sánh:
- **Kiểu dữ liệu** (type pattern): kiểm tra xem một đối tượng có thuộc một kiểu nào đó hay không, ví dụ: `if (x is int)`.
- **Thuộc tính** (property pattern): kiểm tra giá trị của các thuộc tính bên trong một đối tượng.
- **Nội dung danh sách** (list pattern): kiểm tra nội dung và cấu trúc của một danh sách.

Bạn có thể kết hợp nhiều mẫu bằng cách sử dụng logic `and` (và -- tất cả điều kiện phải đúng), `or` (hoặc -- chỉ cần một điều kiện đúng), và `not` (phủ định -- đảo ngược điều kiện). Pattern matching cung cấp một vốn từ vựng phong phú để kiểm tra dữ liệu và đưa ra quyết định trong chương trình dựa trên kết quả kiểm tra đó.

## Tiếp theo là gì?

Sau khi hoàn thành các bài hướng dẫn này, hãy tiếp tục hành trình học tập của bạn:

- [Xây dựng ứng dụng dạng tệp (Build file-based apps)](../../fundamentals/tutorials/file-based-programs.md): Học cách tạo và chạy các chương trình C# dạng một tệp (single-file) từ **dòng lệnh** (command line) -- giao diện văn bản nơi bạn gõ lệnh để điều khiển máy tính.
- [Những gì bạn có thể xây dựng với C# (What you can build with C#)](../what-you-can-build.md): Khám phá các loại ứng dụng bạn có thể tạo ra với C#, từ ứng dụng web, ứng dụng desktop, game cho đến ứng dụng di động.
- [Hệ thống kiểu dữ liệu C# (C# type system)](../../fundamentals/types/index.md): Đi sâu hơn vào **hệ thống kiểu dữ liệu** (type system) của C#, bao gồm **value types** (kiểu giá trị), **reference types** (kiểu tham chiếu), **generics** (kiểu tổng quát -- cho phép viết mã linh hoạt với nhiều kiểu dữ liệu khác nhau), và nhiều khái niệm nâng cao khác.
- [Kiến thức nền tảng C# (C# fundamentals)](../../fundamentals/program-structure/index.md): Tìm hiểu về **cấu trúc chương trình** (program structure), **lập trình hướng đối tượng** (object-oriented programming - OOP) -- một phương pháp lập trình tổ chức mã nguồn xoay quanh các "đối tượng" có dữ liệu và hành vi -- và **xử lý lỗi** (error handling) -- cách chương trình phản ứng khi có lỗi xảy ra thay vì bị treo hoặc crash.
