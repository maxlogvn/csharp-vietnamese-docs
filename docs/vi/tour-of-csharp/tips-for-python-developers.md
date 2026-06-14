---
title: Mẹo dành cho lập trình viên Python
description: Mới học C# nhưng đã biết Python? Đây là lộ trình những điểm tương đồng, những tính năng trong C# mà Python không có, và những giải pháp thay thế cho các tính năng Python không có trong C#.
ms.date: 02/06/2026
---

# Lộ trình cho lập trình viên Python học C\#

Nếu bạn đang chuyển từ Python sang C# cho một vai trò hoặc dự án mới, bài viết này sẽ giúp bạn làm quen nhanh chóng. Nó chỉ ra những điểm tương đồng từ Python và những điểm khác biệt trong C#.

C# và Python chia sẻ nhiều khái niệm tương tự nhau. Những cấu trúc quen thuộc này giúp bạn học C# khi đã biết Python.

1. ***Object-oriented (Hướng đối tượng)***: Cả Python và C# đều là ngôn ngữ hướng đối tượng. Mọi khái niệm về class (lớp) trong Python đều áp dụng được trong C#, dù cú pháp có khác nhau.
1. ***Đa nền tảng (Cross-platform)***: Cả Python và C# đều là ngôn ngữ đa nền tảng. Ứng dụng viết bằng ngôn ngữ nào cũng có thể chạy trên nhiều nền tảng.
1. ***Dọn rác (Garbage collection)***: Cả hai ngôn ngữ đều sử dụng quản lý bộ nhớ tự động thông qua dọn rác. Runtime (môi trường thực thi) thu hồi bộ nhớ từ những object (đối tượng) không còn được tham chiếu.
1. ***Kiểu mạnh (Strongly typed)***: Cả Python và C# đều là ngôn ngữ kiểu mạnh. Việc ép kiểu không xảy ra ngầm định. Có một số khác biệt sẽ được đề cập sau, vì C# là kiểu tĩnh (statically typed) trong khi Python là kiểu động (dynamically typed).
1. ***Bất đồng bộ / Chờ (Async / Await)***: Tính năng `async` và `await` của Python được lấy cảm hứng trực tiếp từ hỗ trợ `async` và `await` của C#.
1. ***Pattern matching (đối sánh mẫu)***: Biểu thức `match` và pattern matching (đối sánh mẫu) của Python tương tự biểu thức `switch` [đối sánh mẫu](../fundamentals/functional/pattern-matching.md) của C#. Bạn dùng chúng để kiểm tra một biểu thức dữ liệu phức tạp nhằm xác định xem nó có khớp với một mẫu hay không.
1. ***Từ khoá câu lệnh (Statement keywords)***: Python và C# chia sẻ nhiều từ khoá như `if`, `else`, `while`, `for` và nhiều từ khoá khác. Dù không phải mọi cú pháp đều giống hệt nhau, nhưng có đủ sự tương đồng để bạn có thể đọc được C# nếu đã biết Python.

## Sơ qua về cú pháp

Các ví dụ sau đây cho thấy một vài mẫu thông dụng được đặt cạnh nhau. Những so sánh này không đầy đủ, nhưng chúng giúp bạn nhanh chóng cảm nhận được sự khác biệt về cú pháp.

**Type annotations (chú thích kiểu):**

```python
# Python
name: str = "Hello"
count: int = 5
```

```csharp
// C#
string name = "Hello";
int count = 5;
```

**Lọc danh sách (list comprehension so với LINQ):**

```python
# Python
result = [x for x in items if x > 5]
```

```csharp
// C#
var result = items.Where(x => x > 5).ToList();
```

Tìm hiểu thêm: [Tổng quan về LINQ](../linq/index.md)

**Phạm vi khối lệnh (thụt dòng so với dấu ngoặc nhọn):**

```python
# Python
if count > 0:
    print("positive")
```

```csharp
// C#
if (count > 0)
{
    Console.WriteLine("positive");
}
```

**Định nghĩa class:**

```python
# Python
class Point:
    def __init__(self, x: int, y: int):
        self.x = x
        self.y = y
```

```csharp
// C#
record Point(int X, int Y);
```

Tìm hiểu thêm: [bản ghi](../fundamentals/types/records.md)

## Những khác biệt chính

Khi học C#, bạn sẽ khám phá những khái niệm quan trọng mà C# khác với Python:

1. [***Thụt dòng so với token***](./tutorials/branches-and-loops.md): Trong Python, xuống dòng và thụt dòng là các yếu tố cú pháp quan trọng. Trong C#, khoảng trắng không có ý nghĩa đặc biệt. Các token như `;` dùng để phân cách câu lệnh, và các token khác như `{` và `}` kiểm soát phạm vi khối lệnh cho `if` và các khối lệnh khác. Tuy nhiên, để dễ đọc, hầu hết các kiểu viết mã (bao gồm kiểu được dùng trong tài liệu này) đều sử dụng thụt dòng để củng cố phạm vi khối lệnh được khai báo bởi `{` và `}`.
1. [***Kiểu tĩnh (Static typing)***](../fundamentals/types/index.md): Trong C#, khai báo variable (biến) bao gồm cả kiểu của nó. Gán lại variable cho một object (đối tượng) thuộc kiểu khác sẽ gây ra lỗi biên dịch. Trong Python, kiểu có thể thay đổi khi gán lại.
1. [***Kiểu nullable***](../fundamentals/null-safety/nullable-reference-types.md): Variable trong C# có thể là *nullable* (có thể null) hoặc *non-nullable* (không thể null). Kiểu non-nullable là kiểu không thể là null (hay nothing). Nó luôn tham chiếu tới một object hợp lệ. Ngược lại, kiểu nullable có thể tham chiếu tới một object hợp lệ hoặc null.
1. [***LINQ***](../linq/index.md): Các từ khoá biểu thức truy vấn tạo nên Language Integrated Query (LINQ) không phải là từ khoá trong Python. Tuy nhiên, các thư viện Python như `itertools`, `more-itertools` và `py-linq` cung cấp chức năng tương tự.
1. [***Generics***](../fundamentals/types/generics.md): Generics (kiểu tổng quát) trong C# sử dụng kiểu tĩnh (static typing) để đưa ra các khẳng định về tham số được cung cấp cho các tham số kiểu. Một giải thuật generic có thể cần chỉ định các ràng buộc mà kiểu tham số phải thoả mãn.

> [!TIP]
> Để tìm hiểu thêm về hệ thống kiểu của C# — bao gồm `class` so với `struct`, generics và interface — hãy truy cập bài tổng quan [Hệ thống kiểu](../fundamentals/types/index.md) trong phần Kiến thức nền tảng (Fundamentals).

Cuối cùng, một số tính năng của Python không có trong C#:

1. ***Structural typing / duck typing (kiểu cấu trúc / kiểu vịt)***: Trong C#, các kiểu có tên và khai báo. Ngoại trừ [bộ dữ liệu](../language-reference/builtin-types/value-tuples.md), các kiểu có cùng cấu trúc không thể thay thế cho nhau.
1. ***REPL***: C# không có vòng lặp Read-Eval-Print (REPL) để tạo mẫu nhanh các giải pháp.
1. ***Khoảng trắng có ý nghĩa***: Bạn cần sử dụng đúng dấu ngoặc nhọn `{` và `}` để đánh dấu phạm vi khối lệnh.

Học C# khi đã biết Python là một hành trình suôn sẻ. Hai ngôn ngữ có những khái niệm và cách diễn đạt tương tự nhau.

## Các bước tiếp theo

- [Tham quan C#](./overview.md): Xem tổng quan cấp cao về tất cả các tính năng của C#.
- [Hướng dẫn cho người mới bắt đầu](./tutorials/index.md): Học C# từng bước với các bài học tương tác.
- [Những gì bạn có thể xây dựng với C#](./what-you-can-build.md): Khám phá các loại ứng dụng bạn có thể tạo bằng C#.
- [Kiến thức nền tảng C#](../fundamentals/program-structure/index.md): Đi sâu vào hệ thống kiểu, lập trình hướng đối tượng và nhiều hơn nữa.
