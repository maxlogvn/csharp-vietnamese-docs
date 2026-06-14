---
title: Lời khuyên cho nhà phát triển JavaScript và TypeScript
description: "Bạn mới học C#, nhưng đã biết JavaScript hoặc TypeScript? Đây là bản đồ về những thứ tương tự, những tính năng trong C# không có trong JavaScript hoặc TypeScript, và những cách thay thế cho những tính năng bạn dùng nhưng không có trong C#"
ms.date: 02/06/2026
---
# Bản đồ dành cho nhà phát triển JavaScript và TypeScript học C\#

Nếu bạn đang gia nhập một team sử dụng C#, hoặc đang khám phá nó cho phát triển phía server hoặc full-stack, bài viết này sẽ giúp bạn làm quen nhanh chóng. Nó nêu bật những điểm quen thuộc từ JavaScript và TypeScript và những điểm mới trong C#.

C#, TypeScript và JavaScript đều thuộc họ ngôn ngữ C. Sự tương đồng giữa các ngôn ngữ này giúp bạn nhanh chóng làm việc hiệu quả với C#.

1. ***Cú pháp tương tự***: JavaScript, TypeScript và C# đều thuộc họ ngôn ngữ C. Sự tương đồng đó có nghĩa là bạn đã có thể đọc và hiểu C#. Có một vài khác biệt, nhưng phần lớn cú pháp giống với JavaScript và C. Dấu ngoặc nhọn và dấu chấm phẩy quen thuộc. Các câu lệnh điều khiển như `if`, `else` và `switch` giống nhau. Các vòng lặp `for`, `while` và `do...while` cũng giống. Các từ khoá `class` và `interface` có trong cả C# và TypeScript. Modifier (bổ từ) truy cập trong TypeScript và C#, từ `public` đến `private`, là giống nhau.
1. ***Token `=>`***: Cả ba ngôn ngữ đều hỗ trợ định nghĩa hàm gọn nhẹ. Trong C#, chúng được gọi là [*lambda expressions*](../language-reference/operators/lambda-expressions.md). Trong JavaScript, chúng thường được gọi là *arrow functions*.
1. ***Phân cấp hàm***: Cả ba ngôn ngữ đều hỗ trợ [local functions](../programming-guide/classes-and-structs/local-functions.md) (hàm nội bộ), tức là những hàm được định nghĩa bên trong các hàm khác.
1. ***Async / Await***: Cả ba ngôn ngữ đều dùng chung từ khoá `async` và `await` cho lập trình bất đồng bộ.
1. ***Garbage collection (thu gom rác)***: Cả ba ngôn ngữ đều dựa vào garbage collector để tự động quản lý bộ nhớ.
1. ***Event model (mô hình sự kiện)***: Cú pháp [`event`](../events-overview.md) của C# tương tự với mô hình sự kiện DOM (document object model) trong JavaScript.
1. ***Trình quản lý gói***: [NuGet](https://nuget.org) là trình quản lý gói phổ biến nhất cho C#, tương tự như npm cho ứng dụng JavaScript. Thư viện C# được phân phối dưới dạng [assembly](../../standard/assembly/index.md).

## Sơ lược cú pháp

Các ví dụ sau đây thể hiện một vài mẫu thông dụng bên cạnh nhau. Những so sánh này không đầy đủ, nhưng chúng cho bạn một cái nhìn nhanh về sự khác biệt cú pháp.

**Chú thích kiểu (type annotations):**

```typescript
// TypeScript
let name: string = "Hello";
let count: number = 5;
```

```csharp
// C#
string name = "Hello";
int count = 5;
```

**Async / await:**

```typescript
// TypeScript
async function fetchData(): Promise<string> {
    const response = await fetch(url);
    return await response.text();
}
```

```csharp
// C#
async Task<string> FetchDataAsync() {
    var response = await client.GetAsync(url);
    return await response.Content.ReadAsStringAsync();
}
```

Để tìm hiểu thêm, xem [Lập trình bất đồng bộ](../asynchronous-programming/index.md).

**Class (lớp):**

```typescript
// TypeScript
class Point {
    constructor(public x: number, public y: number) {}
}
```

```csharp
// C#
record Point(int X, int Y);
```

Để tìm hiểu thêm, xem [bản ghi](../fundamentals/types/records.md).

**Pattern matching (đối sánh mẫu):**

```typescript
// TypeScript - kiểm tra kiểu thủ công
if (typeof value === "string") { /* ... */ }
```

```csharp
// C# - pattern matching
if (value is string s) { /* use s */ }
```

Để tìm hiểu thêm, xem [đối sánh mẫu](../fundamentals/functional/pattern-matching.md).

## Sự khác biệt về mô hình runtime

Mặc dù C# và JavaScript có cú pháp tương tự, nhưng chúng vận hành rất khác nhau:

- JavaScript chạy trên một runtime như V8 và sử dụng event loop (vòng lặp sự kiện) để xử lý công việc bất đồng bộ.
- C# chạy trên .NET runtime (CLR), nơi mã được biên dịch thành Intermediate Language (IL) và sau đó được thực thi bằng JIT hoặc AOT compilation.

## Những điều mới mẻ dành cho bạn trong C\#

Khi bạn học C#, bạn sẽ gặp những khái niệm không có trong JavaScript. Một số khái niệm này có thể quen thuộc nếu bạn dùng TypeScript:

1. [***Hệ thống kiểu của C#***](../fundamentals/types/index.md): C# là một ngôn ngữ strongly typed (kiểu mạnh). Mỗi variable (biến) có một kiểu, và kiểu đó không thể thay đổi. Bạn định nghĩa kiểu `class` hoặc `struct`. Bạn có thể định nghĩa [`interface`](../fundamentals/types/interfaces.md) để định nghĩa hành vi được triển khai bởi các kiểu khác. TypeScript bao gồm nhiều khái niệm này, nhưng vì TypeScript được xây dựng trên JavaScript, hệ thống kiểu không chặt chẽ bằng.
1. [***Pattern matching (đối sánh mẫu)***](../fundamentals/functional/pattern-matching.md): Pattern matching (đối sánh mẫu) cho phép các câu lệnh và biểu thức điều kiện ngắn gọn dựa trên hình dạng của các cấu trúc dữ liệu phức tạp. Biểu thức [`is`](../language-reference/operators/is.md) kiểm tra một variable "có phải là" một khuôn mẫu nào đó. Biểu thức [`switch`](../language-reference/operators/switch-expression.md) dựa trên khuôn mẫu cung cấp cú pháp phong phú để kiểm tra một variable và đưa ra quyết định dựa trên đặc điểm của nó.
1. [***String interpolation (nội suy chuỗi)***](../language-reference/tokens/interpolated.md) và [***raw string literals (chuỗi văn bản thô)***](../language-reference/builtin-types/reference-types.md#string-literals): String interpolation cho phép bạn chèn các biểu thức đã được tính toán vào một chuỗi, thay vì dùng các định danh vị trí. Raw string literals cung cấp cách giảm thiểu các ký tự thoát (escape sequences) trong văn bản.
1. [***Kiểu nullable và non-nullable***](../fundamentals/null-safety/nullable-reference-types.md): C# hỗ trợ *nullable value types* (kiểu giá trị có thể null) và *nullable reference types* (kiểu tham chiếu có thể null) bằng cách thêm `?` vào sau một kiểu. Với kiểu nullable, trình biên dịch sẽ cảnh báo nếu bạn không kiểm tra `null` trước khi truy cập biểu thức. Với kiểu non-nullable, trình biên dịch cảnh báo nếu bạn có thể gán giá trị `null` cho variable đó. Những tính năng này có thể giảm thiểu lỗi [`NullReferenceException`](https://learn.microsoft.com/dotnet/api/system.nullreferenceexception) trong ứng dụng của bạn. Cú pháp này có thể quen thuộc từ việc TypeScript dùng `?` cho thuộc tính tuỳ chọn.
1. [***LINQ***](../linq/index.md): Language integrated query (LINQ) cung cấp một cú pháp chung để truy vấn và biến đổi dữ liệu, bất kể cách lưu trữ của chúng.

> [!TIP]
> Để tìm hiểu thêm về hệ thống kiểu của C# -- bao gồm `class` và `struct`, generics, và interface -- hãy xem [Hệ thống kiểu](../fundamentals/types/index.md) trong phần Fundamentals (Kiến thức nền tảng).

Khi bạn học thêm, những khác biệt khác sẽ dần rõ ràng, nhưng nhiều khác biệt trong số đó có phạm vi nhỏ hơn.

Một số tính năng và thói quen quen thuộc từ JavaScript và TypeScript không có trong C#:

1. ***Dynamic type (kiểu động)***: C# sử dụng kiểu tĩnh (static typing). Một khai báo variable bao gồm kiểu, và kiểu đó không thể thay đổi. Có một kiểu [`dynamic`](../language-reference/builtin-types/reference-types.md#the-dynamic-type) trong C# cung cấp ràng buộc runtime.
1. ***Prototypal inheritance (kế thừa nguyên mẫu)***: Kế thừa trong C# là một phần của khai báo kiểu. Một `class` trong C# khai rõ bất kỳ base class (lớp cơ sở) nào. Trong JavaScript, bạn đặt thuộc tính `__proto__` để đặt kiểu cơ sở cho bất kỳ instance (thể hiện) nào.
1. ***Ngôn ngữ thông dịch***: Code C# phải được biên dịch trước khi chạy. Code JavaScript có thể chạy trực tiếp trong trình duyệt.

Ngoài ra, một vài tính năng TypeScript khác cũng không có trong C#:

1. ***Union types***: Bắt đầu từ C# 15, C# hỗ trợ [kiểu hợp](../language-reference/builtin-types/union.md). Union định nghĩa một tập hợp đóng của các trường hợp có tên mà một giá trị có thể đại diện, và trình biên dịch đảm bảo việc so khớp khuôn mẫu (pattern matching) đầy đủ trên các trường hợp đó.
1. ***Decorators***: C# không có decorators. Một số decorators phổ biến, như `@sealed`, là từ khoá dành riêng trong C#. Những decorators phổ biến khác có thể có [thuộc tính dữ liệu](../language-reference/attributes/general.md) tương ứng. Với những decorators khác, bạn có thể tạo attribute của riêng mình.
1. ***Cú pháp dễ chịu hơn***: Trình biên dịch C# phân tích cú pháp chặt chẽ hơn so với JavaScript.

Nếu bạn đang xây dựng ứng dụng web, hãy cân nhắc sử dụng [Blazor](/aspnet/core/blazor/index) để xây dựng ứng dụng của mình. Blazor là một full-stack web framework được xây dựng cho C#. Component (thành phần) Blazor có thể chạy trên server, dưới dạng assembly .NET, hoặc trên client bằng WebAssembly. Blazor hỗ trợ tương tác với những thư viện JavaScript hoặc TypeScript yêu thích của bạn.

## Bước tiếp theo

- [Tham quan C#](./overview.md): Xem tổng quan ở mức cao về tất cả tính năng C#.
- [Hướng dẫn cơ bản](./tutorials/index.md): Học C# từng bước một với các bài học tương tác.
- [Những gì bạn có thể xây dựng với C#](./what-you-can-build.md): Khám phá các loại ứng dụng bạn có thể tạo bằng C#.
- [Kiến thức nền tảng C#](../fundamentals/program-structure/index.md): Đào sâu vào hệ thống kiểu, lập trình hướng đối tượng, và nhiều hơn nữa.
